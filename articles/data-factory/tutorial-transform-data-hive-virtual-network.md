---
title: "Przekształcanie danych za pomocą programu Hive w usłudze Azure Virtual Network | Microsoft Docs"
description: "Ten samouczek zawiera instrukcje krok po kroku przekształcania danych przy użyciu działania programu Hive w usłudze Azure Data Factory."
services: data-factory
documentationcenter: 
author: shengcmsft
manager: jhubbard
editor: spelluru
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/22/2018
ms.author: shengc
ms.openlocfilehash: 30456a30c12d39ceb14dec6cd60015916cb7ae27
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/23/2018
---
# <a name="transform-data-in-azure-virtual-network-using-hive-activity-in-azure-data-factory"></a>Przekształcanie danych w usłudze Azure Virtual Network przy użyciu działania programu Hive w usłudze Azure Data Factory
W tym samouczku program Azure PowerShell umożliwia tworzenie potoku fabryki danych, który przekształca dane przy użyciu działania programu Hive w klastrze usługi HDInsight, który znajduje się w usłudze Azure Virtual Network (VNet). Ten samouczek obejmuje następujące procedury:

> [!div class="checklist"]
> * Tworzenie fabryki danych. 
> * Redagowanie i konfigurowanie własnego środowiska Integration Runtime
> * Tworzenie i wdrażanie połączonych usług
> * Redagowanie i wdrażanie potoku zawierającego działanie programu Hive
> * Uruchamianie potoku
> * Monitorowanie działania potoku 
> * Sprawdzanie danych wyjściowych 

> [!NOTE]
> Ten artykuł dotyczy wersji 2 usługi Data Factory, która jest obecnie dostępna w wersji zapoznawczej. Jeśli używasz dostępnej ogólnie wersji 1 usługi Data Factory, zobacz [dokumentację dotyczącą usługi Data Factory w wersji 1](v1/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne](https://azure.microsoft.com/free/) konto.

## <a name="prerequisites"></a>Wymagania wstępne
- **Konto usługi Azure Storage**. Utwórz skrypt programu Hive i przekaż go do usługi Azure Storage. Dane wyjściowe skryptu programu Hive są przechowywane na tym koncie magazynu. W tym przykładzie klaster usługi HDInsight używa tego konta usługi Azure Storage jako magazynu głównego. 
- **Azure Virtual Network.** Jeśli nie masz sieci wirtualnej platformy Azure, utwórz ją, wykonując [te instrukcje](../virtual-network/virtual-network-get-started-vnet-subnet.md). W tym przykładzie usługa HDInsight znajduje się w usłudze Azure Virtual Network. Oto przykładowa konfiguracja usługi Azure Virtual Network. 

    ![Tworzenie sieci wirtualnej](media/tutorial-transform-data-using-hive-in-vnet/create-virtual-network.png)
- **Klaster usługi HDInsight.** Utwórz klaster usługi HDInsight i przyłącz go do sieci wirtualnej utworzonej w poprzednim kroku, postępując zgodnie z opisem podanym w tym artykule: [Extend Azure HDInsight using an Azure Virtual Network (Rozszerzenie usługi Azure HDInsight za pomocą usługi Azure Virtual Network)](../hdinsight/hdinsight-extend-hadoop-virtual-network.md). Oto przykładowa konfiguracja usługi HDInsight w sieci wirtualnej. 

    ![Usługa HDInsight w sieci wirtualnej](media/tutorial-transform-data-using-hive-in-vnet/hdinsight-in-vnet-configuration.png)
- Zainstalowanie programu **Azure PowerShell**. Wykonaj instrukcje podane w temacie [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/install-azurerm-ps).

### <a name="upload-hive-script-to-your-blob-storage-account"></a>Przekazywanie skryptu programu Hive do konta usługi Blob Storage

1. Utwórz plik SQL programu Hive SQL o nazwie **hivescript.hql** i następującej zawartości:

   ```sql
   DROP TABLE IF EXISTS HiveSampleOut; 
   CREATE EXTERNAL TABLE HiveSampleOut (clientid string, market string, devicemodel string, state string)
   ROW FORMAT DELIMITED FIELDS TERMINATED BY ' ' 
   STORED AS TEXTFILE LOCATION '${hiveconf:Output}';

   INSERT OVERWRITE TABLE HiveSampleOut
   Select 
       clientid,
       market,
       devicemodel,
       state
   FROM hivesampletable
   ```
2. W usłudze Azure Blob Storage utwórz kontener o nazwie **adftutorial**, jeśli nie istnieje.
3. Utwórz folder o nazwie **hivescripts**.
4. Przekaż plik **hivescript.hql** do podfolderu **hivescripts**.

 

## <a name="create-a-data-factory"></a>Tworzenie fabryki danych


1. Ustaw nazwę grupy zasobów. Ten samouczek zawiera procedurę tworzenia grupy zasobów. Możesz jednak użyć istniejącej grupy zasobów. 

    ```powershell
    $resourceGroupName = "ADFTutorialResourceGroup" 
    ```
2. Podaj nazwę fabryki danych. Musi ona być unikatowa w skali globalnej.

    ```powershell
    $dataFactoryName = "MyDataFactory09142017"
    ```
3. Określ nazwę potoku. 

    ```powershell
    $pipelineName = "MyHivePipeline" # 
    ```
4. Określ nazwę środowiska Integration Runtime (Self-Hosted). Środowisko Integration Runtime (Self-Hosted) jest wymagane, gdy fabryka danych musi uzyskać dostęp do zasobów (takich jak usługa Azure SQL Database) w sieci wirtualnej. 
    ```powershell
    $selfHostedIntegrationRuntimeName = "MySelfHostedIR09142017" 
    ```
2. Uruchom program **PowerShell**. Nie zamykaj programu Azure PowerShell aż do końca tego samouczka Szybki start. Jeśli go zamkniesz i otworzysz ponownie, musisz uruchomić te polecenia jeszcze raz. Obecnie usługa Data Factory w wersji 2 umożliwia tworzenie fabryk danych tylko w regionach Wschodnie stany USA, Wschodnie stany USA 2 i Europa Zachodnia. Magazyny danych (Azure Storage, Azure SQL Database itp.) i jednostki obliczeniowe (HDInsight itp.) używane przez fabrykę danych mogą mieścić się w innych regionach.

    Uruchom poniższe polecenie i wprowadź nazwę użytkownika oraz hasło, których używasz do logowania się w witrynie Azure Portal:
        
    ```powershell
    Login-AzureRmAccount
    ```        
    Uruchom poniższe polecenie, aby wyświetlić wszystkie subskrypcje dla tego konta:

    ```powershell
    Get-AzureRmSubscription
    ```
    Uruchom poniższe polecenie, aby wybrać subskrypcję, z którą chcesz pracować. Zastąp parametr **SubscriptionId** identyfikatorem Twojej subskrypcji platformy Azure:

    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<SubscriptionId>"    
    ```  
3. Utwórz grupę zasobów: ADFTutorialResourceGroup, jeśli jeszcze nie istnieje w Twojej subskrypcji. 

    ```powershell
    New-AzureRmResourceGroup -Name $resourceGroupName -Location "East Us" 
    ```
4. Utwórz fabrykę danych. 

    ```powershell
     $df = Set-AzureRmDataFactoryV2 -Location EastUS -Name $dataFactoryName -ResourceGroupName $resourceGroupName
    ```

    Wykonaj następujące polecenie, aby wyświetlić dane wyjściowe: 

    ```powershell
    $df
    ```

## <a name="create-self-hosted-ir"></a>Tworzenie środowiska IR (Self-hosted)
W tej sekcji utworzysz środowisko Integration Runtime (Self-hosted) i skojarzysz je z maszyną wirtualną platformy Azure w tej samej usłudze Azure Virtual Network, gdzie znajduje się Twój klaster usługi HDInsight.

1. Utwórz środowisko Integration Runtime (Self-hosted). Użyj unikatowej nazwy w przypadku, gdy istnieje inne środowisko Integration Runtime o takiej samej nazwie.

   ```powershell
   Set-AzureRmDataFactoryV2IntegrationRuntime -ResourceGroupName $resourceGroupName -DataFactoryName $dataFactoryName -Name $selfHostedIntegrationRuntimeName -Type SelfHosted
   ```
    To polecenie tworzy logiczną rejestrację środowiska Integration Runtime (Self-hosted). 
2. Aby pobrać klucze uwierzytelniania w celu zarejestrowania środowiska Integration Runtime (Self-hosted), użyj programu PowerShell. Skopiuj jeden z kluczy w celu zarejestrowania środowiska Integration Runtime (Self-hosted).

   ```powershell
   Get-AzureRmDataFactoryV2IntegrationRuntimeKey -ResourceGroupName $resourceGroupName -DataFactoryName $dataFactoryName -Name $selfHostedIntegrationRuntimeName | ConvertTo-Json
   ```

   Oto przykładowe dane wyjściowe: 

   ```powershell
   {
       "AuthKey1":  "IR@0000000000000000000000000000000000000=",
       "AuthKey2":  "IR@0000000000000000000000000000000000000="
   }
   ```
    Zanotuj wartość pozycji **AuthKey1** bez znaków cudzysłowu. 
3. Utwórz maszynę wirtualną platformy Azure i przyłącz ją do tej samej sieci wirtualnej, która zawiera Twój klaster usługi HDInsight. Aby uzyskać szczegółowe informacje, zobacz [How to create virtual machines (Jak utworzyć maszyny wirtualne)](../virtual-network/virtual-network-get-started-vnet-subnet.md#create-vms). Dołącz je do usługi Azure Virtual Network. 
4. Na maszynę wirtualną platformy Azure pobierz [środowisko Integration Runtime (Self-hosted)](https://www.microsoft.com/download/details.aspx?id=39717). Użyj klucza uwierzytelniania uzyskanego w poprzednim kroku, aby ręcznie zarejestrować środowisko Integration Runtime (Self-hosted). 

   ![Rejestrowanie środowiska Integration Runtime](media/tutorial-transform-data-using-hive-in-vnet/register-integration-runtime.png)

   Gdy środowisko Integration Runtime (Self-hosted) zostanie pomyślnie zarejestrowane, zostanie wyświetlony następujący komunikat: ![Pomyślnie zarejestrowane](media/tutorial-transform-data-using-hive-in-vnet/registered-successfully.png)

   Gdy węzeł zostanie połączony z usługą w chmurze, zostanie wyświetlona następująca strona: ![Węzeł jest połączony](media/tutorial-transform-data-using-hive-in-vnet/node-is-connected.png)

## <a name="author-linked-services"></a>Redagowanie połączonych usług

W tej sekcji zredagujesz i wdrożysz dwie połączone usługi:
- Połączoną usługę Azure Storage, która łączy konto usługi Azure Storage z fabryką danych. Ten magazyn jest podstawowym magazynem używanym przez Twój klaster usługi HDInsight. W takim przypadku użyjemy konta usługi Azure Storage również do przechowywania skryptu programu Hive i przekazywania skryptu na wyjście.
- Połączoną usługę Azure HDInsight. Usługa Azure Data Factory przesyła skrypt programu Hive do tego klastra usługi HDInsight w celu wykonania.

### <a name="azure-storage-linked-service"></a>Połączona usługa Azure Storage

Utwórz plik w formacie JSON za pomocą preferowanego edytora, skopiuj poniższą definicję formatu JSON dotyczącą połączonej usługi Azure Storage, a następnie zapisz plik jako **MyStorageLinkedService.json**.

```json
{
    "name": "MyStorageLinkedService",
    "properties": {
      "type": "AzureStorage",
      "typeProperties": {
        "connectionString": {
          "value": "DefaultEndpointsProtocol=https;AccountName=<storageAccountName>;AccountKey=<storageAccountKey>",
          "type": "SecureString"
        }
      },
      "connectVia": {
        "referenceName": "MySelfhostedIR",
        "type": "IntegrationRuntimeReference"
      }  
    }
}
```

Zastąp wartości **&lt;accountname&gt; i &lt;accountkey&gt;** nazwą konta usługi Azure Storage oraz jej kluczem.

### <a name="hdinsight-linked-service"></a>Połączona usługa HDInsight

Utwórz plik w formacie JSON za pomocą preferowanego edytora, skopiuj poniższą definicję formatu JSON dotyczącą połączonej usługi Azure HDIsight, a następnie zapisz plik jako **MyHDInsightLinkedService.json**.

```
{
  "name": "MyHDInsightLinkedService",
  "properties": {     
      "type": "HDInsight",
      "typeProperties": {
          "clusterUri": "https://<clustername>.azurehdinsight.net",
          "userName": "<username>",
          "password": {
            "value": "<password>",
            "type": "SecureString"
          },
          "linkedServiceName": {
            "referenceName": "MyStorageLinkedService",
            "type": "LinkedServiceReference"
          }
      },
      "connectVia": {
        "referenceName": "MySelfhostedIR",
        "type": "IntegrationRuntimeReference"
      }
  }
}
```

Zaktualizuj wartości następujących właściwości w definicji połączonej usługi:

- **userName**. Nazwa użytkownika logowania do klastra określona podczas tworzenia klastra. 
- **password**. Hasło użytkownika.
- **clusterUri**. Podaj adres URL klastra usługi HDInsight w formacie https://<clustername>.azurehdinsight.net.  W tym artykule przyjęto założenie, że masz dostęp do klastra za pośrednictwem Internetu. Na przykład możesz połączyć się z klastrem pod adresem `https://clustername.azurehdinsight.net`. Ten adres używa publicznej bramy, która jest niedostępna w przypadku używania sieciowych grup zabezpieczeń lub tras zdefiniowanych przez użytkownika (UDR) do ograniczania dostępu z Internetu. Aby fabryka danych mogła przekazać zadania do klastra usługi HDInsight w usłudze Azure Virtual Network, musisz skonfigurować swoją usługę Azure Virtual Network tak, aby adres URL mógł zostać rozpoznany jako prywatny adres IP bramy używany przez usługę HDInsight.

  1. W witrynie Azure Portal otwórz sieć wirtualną, w której znajduje się usługa HDInsight. Otwórz interfejs sieciowy mający nazwę zaczynającą się od `nic-gateway-0`. Zanotuj jego prywatny adres IP. Na przykład 10.6.0.15. 
  2. Jeśli usługa Azure Virtual Network ma serwer usługi DNS, zaktualizuj rekord usługi DNS tak, aby adres URL klastra usługi HDInsight `https://<clustername>.azurehdinsight.net` można było rozpoznać jako `10.6.0.15`. Jest to zalecane podejście. Jeśli w usłudze Azure Virtual Network nie masz serwera DNS, możesz tymczasowo obejść to, edytując plik hosts (C:\Windows\System32\drivers\etc) wszystkich maszyn wirtualnych, które są zarejestrowane jako węzły środowiska Integration Runtime (Self-hosted) przez dodanie wpisu podobnego do tego: 
  
        `10.6.0.15 myHDIClusterName.azurehdinsight.net`

## <a name="create-linked-services"></a>Tworzenie połączonych usług
W programie PowerShell przejdź do folderu, w którym zostały utworzone pliki w formacie JSON, a następnie uruchom następujące polecenie, aby wdrożyć połączone usługi: 

1. W programie PowerShell przejdź do folderu, w którym utworzono pliki w formacie JSON.
2. Uruchom poniższe polecenie, aby utworzyć połączoną usługę Azure Storage. 

    ```powershell
    Set-AzureRmDataFactoryV2LinkedService -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "MyStorageLinkedService" -File "MyStorageLinkedService.json"
    ```
3. Uruchom poniższe polecenie, aby utworzyć połączoną usługę Azure HDInsight. 

    ```powershell
    Set-AzureRmDataFactoryV2LinkedService -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "MyHDInsightLinkedService" -File "MyHDInsightLinkedService.json"
    ```

## <a name="author-a-pipeline"></a>Redagowanie potoku
W tym kroku utworzysz nowy potok za pomocą działania programu Hive. Działanie wykonuje skrypt programu Hive służący do zwracania danych z przykładowej tabeli i zapisania ich w ramach ścieżki zdefiniowanej przez użytkownika. Utwórz plik w formacie JSON za pomocą preferowanego edytora, skopiuj poniższą definicję formatu JSON dotyczącą definicji potoku, a następnie zapisz go jako **MyHivePipeline.json**.


```json
{
  "name": "MyHivePipeline",
  "properties": {
    "activities": [
      {
        "name": "MyHiveActivity",
        "type": "HDInsightHive",
        "linkedServiceName": {
            "referenceName": "MyHDILinkedService",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
          "scriptPath": "adftutorial\\hivescripts\\hivescript.hql",
          "getDebugInfo": "Failure",
          "defines": {           
            "Output": "wasb://<Container>@<StorageAccount>.blob.core.windows.net/outputfolder/"
          },
          "scriptLinkedService": {
            "referenceName": "MyStorageLinkedService",
            "type": "LinkedServiceReference"
          }
        }
      }
    ]
  }
}

```

Pamiętaj o następujących kwestiach:

- Argument **scriptPath** wskazuje ścieżkę do skryptu programu Hive na koncie Azure Storage użytym dla usługi MyStorageLinkedService. W ścieżce jest rozróżniana wielkość liter.
- **Output** jest argumentem używanym w skrypcie programu Hive. Użyj formatu `wasb://<Container>@<StorageAccount>.blob.core.windows.net/outputfolder/`, aby wskazać istniejący folder w usłudze Azure Storage. W ścieżce jest rozróżniana wielkość liter. 

Przejdź do folderu, w którym zostały utworzone pliki w formacie JSON, a następnie uruchom następujące polecenie, aby wdrożyć potok: 


```powershell
Set-AzureRmDataFactoryV2Pipeline -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name $pipelineName -File "MyHivePipeline.json"
```

## <a name="start-the-pipeline"></a>Uruchamianie potoku 

1. Uruchamianie przebiegu potoku. Umożliwia to również przechwycenie identyfikatora uruchomienia potoku w celu monitorowania w przyszłości.

    ```powershell
    $runId = Invoke-AzureRmDataFactoryV2Pipeline -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -PipelineName $pipelineName
   ```
2. Uruchom następujący skrypt, aby stale sprawdzać stan uruchomienia potoku do momentu zakończenia jego działania.

    ```powershell
    while ($True) {
        $result = Get-AzureRmDataFactoryV2ActivityRun -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -PipelineRunId $runId -RunStartedAfter (Get-Date).AddMinutes(-30) -RunStartedBefore (Get-Date).AddMinutes(30)

        if(!$result) {
            Write-Host "Waiting for pipeline to start..." -foregroundcolor "Yellow"
        }
        elseif (($result | Where-Object { $_.Status -eq "InProgress" } | Measure-Object).count -ne 0) {
            Write-Host "Pipeline run status: In Progress" -foregroundcolor "Yellow"
        }
        else {
            Write-Host "Pipeline '"$pipelineName"' run finished. Result:" -foregroundcolor "Yellow"
            $result
            break
        }
        ($result | Format-List | Out-String)
        Start-Sleep -Seconds 15
    }
    
    Write-Host "Activity `Output` section:" -foregroundcolor "Yellow"
    $result.Output -join "`r`n"

    Write-Host "Activity `Error` section:" -foregroundcolor "Yellow"
    $result.Error -join "`r`n"
    ```

   Oto dane wyjściowe przykładowego przebiegu:

    ```json
    Pipeline run status: In Progress
    
    ResourceGroupName : ADFV2SampleRG2
    DataFactoryName   : SampleV2DataFactory2
    ActivityName      : MyHiveActivity
    PipelineRunId     : 000000000-0000-0000-000000000000000000
    PipelineName      : MyHivePipeline
    Input             : {getDebugInfo, scriptPath, scriptLinkedService, defines}
    Output            :
    LinkedServiceName :
    ActivityRunStart  : 9/18/2017 6:58:13 AM
    ActivityRunEnd    :
    DurationInMs      :
    Status            : InProgress
    Error             :
    
    Pipeline ' MyHivePipeline' run finished. Result:
    
    ResourceGroupName : ADFV2SampleRG2
    DataFactoryName   : SampleV2DataFactory2
    ActivityName      : MyHiveActivity
    PipelineRunId     : 0000000-0000-0000-0000-000000000000
    PipelineName      : MyHivePipeline
    Input             : {getDebugInfo, scriptPath, scriptLinkedService, defines}
    Output            : {logLocation, clusterInUse, jobId, ExecutionProgress...}
    LinkedServiceName :
    ActivityRunStart  : 9/18/2017 6:58:13 AM
    ActivityRunEnd    : 9/18/2017 6:59:16 AM
    DurationInMs      : 63636
    Status            : Succeeded
    Error             : {errorCode, message, failureType, target}
    
    Activity Output section:
    "logLocation": "wasbs://adfjobs@adfv2samplestor.blob.core.windows.net/HiveQueryJobs/000000000-0000-47c3-9b28-1cdc7f3f2ba2/18_09_2017_06_58_18_023/Status"
    "clusterInUse": "https://adfv2HivePrivate.azurehdinsight.net"
    "jobId": "job_1505387997356_0024"
    "ExecutionProgress": "Succeeded"
    "effectiveIntegrationRuntime": "MySelfhostedIR"
    Activity Error section:
    "errorCode": ""
    "message": ""
    "failureType": ""
    "target": "MyHiveActivity"
    ```
4. Sprawdź folder `outputfolder` dla nowego pliku utworzonego w wyniku zapytania programu Hive, powinien on wyglądać podobnie do następujących przykładowych danych wyjściowych: 

   ```
   8 en-US SCH-i500 California
   23 en-US Incredible Pennsylvania
   212 en-US SCH-i500 New York
   212 en-US SCH-i500 New York
   212 en-US SCH-i500 New York
   212 en-US SCH-i500 New York
   212 en-US SCH-i500 New York
   212 en-US SCH-i500 New York
   212 en-US SCH-i500 New York
   212 en-US SCH-i500 New York
   212 en-US SCH-i500 New York
   212 en-US SCH-i500 New York
   212 en-US SCH-i500 New York
   212 en-US SCH-i500 New York
   246 en-US SCH-i500 District Of Columbia
   246 en-US SCH-i500 District Of Columbia
   ```

## <a name="next-steps"></a>Następne kroki
W ramach tego samouczka wykonano następujące procedury: 

> [!div class="checklist"]
> * Tworzenie fabryki danych. 
> * Redagowanie i konfigurowanie własnego środowiska Integration Runtime
> * Tworzenie i wdrażanie połączonych usług
> * Redagowanie i wdrażanie potoku zawierającego działanie programu Hive
> * Uruchamianie potoku
> * Monitorowanie działania potoku 
> * Sprawdzanie danych wyjściowych 

Przejdź do następującego samouczka, aby dowiedzieć się więcej o przekształcaniu danych za pomocą klastra Spark na platformie Azure:

> [!div class="nextstepaction"]
>[Branching and chaining Data Factory control flow (Rozgałęzianie i tworzenie łańcucha przepływu sterowania fabryki danych)](tutorial-control-flow.md)



