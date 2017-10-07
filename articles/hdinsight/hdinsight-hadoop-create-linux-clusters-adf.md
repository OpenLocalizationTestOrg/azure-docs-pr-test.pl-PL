---
title: "klastry Hadoop na żądanie przy użyciu fabryki danych - Azure HDInsight aaaCreate | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate, klastrów Hadoop na żądanie, w usłudze HDInsight przy użyciu fabryki danych Azure."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: spelluru
manager: jhubbard
editor: cgronlun
ms.assetid: 1f3b3a78-4d16-4d99-ba6e-06f7bb185d6a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/20/2017
ms.author: spelluru
ms.openlocfilehash: c869776ac270e37dec710b5fc8d2a792d9263129
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-on-demand-hadoop-clusters-in-hdinsight-using-azure-data-factory"></a>Tworzenie na żądanie klastrów platformy Hadoop w usłudze HDInsight przy użyciu fabryki danych Azure
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

[Fabryka danych Azure](../data-factory/data-factory-introduction.md) to usługa integracji danych opartych na chmurze, która organizuje i zautomatyzować przepływ hello i przekształcania danych. On można tworzyć HDInsight Hadoop tooprocess just in time klastra wycinek danych wejściowych i usunąć hello klastra po zakończeniu przetwarzania hello. Zalety hello przy użyciu klastra usługi Hadoop w HDInsight na żądanie, należą:

- Tylko płatności dla zadania czas hello jest uruchomiona na powitania klastra usługi HDInsight Hadoop (oraz można skonfigurować krótki czas bezczynności). Witaj rozliczeń dla klastrów usługi HDInsight jest proporcjonalnie za minutę, czy są używane lub nie. Gdy używasz usługi HDInsight połączony na żądanie w fabryce danych klastrów hello są tworzone na żądanie. I klastrów hello są usuwane automatycznie po zakończeniu zadania hello. W związku z tym płacisz tylko za uruchomione czasu i krótki czas bezczynności (ustawienie time-to-live) hello zadanie hello.
- Można utworzyć przepływu pracy za pomocą potoku fabryki danych. Na przykład można mieć hello potoku toocopy danych z lokalnego programu SQL Server tooan magazynu obiektów blob platformy Azure, dane hello proces przez uruchomienie skryptu Hive i Pig skrypt w klastrze usługi HDInsight Hadoop na żądanie. Następnie skopiuj hello wynik tooan danych Azure SQL Data Warehouse dla tooconsume aplikacji analizy Biznesowej.
- Można zaplanować hello przepływu pracy toorun okresowo (co godzinę, codziennie, co tydzień, co miesiąc, itp.).

W fabryce danych Azure fabryki danych może mieć co najmniej jeden potoki danych. Potoku danych ma co najmniej jednego działania. Istnieją dwa typy działań: [działań przepływu danych](../data-factory/data-factory-data-movement-activities.md) i [działań przekształcania danych](../data-factory/data-factory-data-transformation-activities.md). Używasz danych toomove działania (obecnie tylko działanie kopiowania) przeniesienia danych z magazynu danych źródła danych magazynu tooa docelowego. Możesz użyć danych przekształcania działania tootransform/przetwarzania danych. Działanie Hive HDInsight jest jednym z hello transformacji działania obsługiwane przez fabryki danych. Używasz hello Hive transformacji działania w tym samouczku.

Toouse działania hive można skonfigurować klaster usługi HDInsight Hadoop lub klastra usługi Hadoop w HDInsight na żądanie. W tym samouczku hello Hive działania w potoku fabryki danych hello jest toouse skonfigurowany klaster usługi HDInsight na żądanie. W związku z tym hello działanie zostanie uruchomione tooprocess wycinka danych, po co się stanie:

1. Klastra usługi HDInsight Hadoop jest tworzony automatycznie dla możesz tooprocess just in time hello wycinka.  
2. dane wejściowe Hello są przetwarzane, uruchamiając skrypt HiveQL na powitania klastra.
3. Witaj klastra usługi HDInsight Hadoop jest usuwany po zakończeniu przetwarzania hello i hello klastra jest w stanie bezczynności hello skonfigurowane ilość czasu (ustawienie timeToLive). Jeśli hello dalej wycinek danych jest dostępna do przetwarzania z tego czasu bezczynności timeToLive, hello tego samego klastra jest używany tooprocess hello wycinka.  

W tym samouczku hello skrypt HiveQL skojarzone z działaniem hive hello wykonuje hello następujące akcje:

1. Tworzy tabelę zewnętrzną odwołania hello web nieprzetworzone dane dziennika przechowywanych w magazynie obiektów Blob platformy Azure.
2. Partycje hello nieprzetworzone dane przez rok i miesiąc.
3. Magazyny hello danych podzielonej na partycje w hello magazynu obiektów blob platformy Azure.

W tym samouczku hello skrypt HiveQL skojarzone z działaniem hive hello tworzy tabelę zewnętrzną odwołania hello raw web dziennika danych przechowywanych w hello magazynu obiektów Blob Azure. Poniżej przedstawiono hello Przykładowe wiersze dla każdego miesiąca w pliku wejściowym hello.

```
2014-01-01,02:01:09,SAMPLEWEBSITE,GET,/blogposts/mvc4/step2.png,X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,53175,871
2014-02-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
2014-03-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
```

partycje skrypt HiveQL Hello hello nieprzetworzone dane przez rok i miesiąc. Tworzy trzy foldery dane wyjściowe na podstawie danych wprowadzonych z poprzednich hello. Każdy folder zawiera plik z wpisów z każdego miesiąca.

```
adfgetstarted/partitioneddata/year=2014/month=1/000000_0
adfgetstarted/partitioneddata/year=2014/month=2/000000_0
adfgetstarted/partitioneddata/year=2014/month=3/000000_0
```

Aby uzyskać listę działań przekształcania danych fabryki danych w działaniu tooHive dodanie, zobacz [transformacji i analizy przy użyciu fabryki danych Azure](../data-factory/data-factory-data-transformation-activities.md).

> [!NOTE]
> Obecnie można tworzyć tylko klastra usługi HDInsight w wersji 3.2 z fabryki danych Azure.

## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem powitalne instrukcje w tym artykule, musi mieć hello następujące elementy:

* [Subskrypcja platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Azure PowerShell.

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

### <a name="prepare-storage-account"></a>Przygotowanie konta magazynu
Możesz użyć toothree kont magazynu w tym scenariuszu:

- domyślne konto magazynu dla klastra usługi HDInsight hello
- Konto magazynu dla danych wejściowych hello
- Konto magazynu dla danych wyjściowych hello

Samouczek hello toosimplify, możesz użyć jednego magazynu konta tooserve hello trzy funkcje. Przykładowy skrypt programu Azure PowerShell Hello, w tej sekcji wykonuje hello następujące zadania:

1. Zaloguj się za tooAzure.
2. Utwórz grupę zasobów platformy Azure.
3. Tworzenie konta usługi Azure Storage.
4. Tworzenie kontenera obiektów Blob na koncie magazynu hello
5. Skopiuj następujące dwa pliki toohello obiektów Blob kontenera hello:

   * Plik danych wejściowych: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log)
   * Skrypt HiveQL: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql)

     Oba pliki są przechowywane w publicznego kontenera obiektów Blob.


**tooprepare hello magazynu i skopiuj hello plików przy użyciu programu Azure PowerShell:**
> [!IMPORTANT]
> Określ nazwy grupy zasobów platformy Azure hello i hello kontem magazynu platformy Azure, który zostanie utworzony przez skrypt hello.
> Zapisz **Nazwa grupy zasobów**, **nazwy konta magazynu**, i **klucz konta magazynu** wyjściowych przez skrypt hello. Należy je w następnej sekcji hello.

```powershell
$resourceGroupName = "<Azure Resource Group Name>"
$storageAccountName = "<Azure Storage Account Name>"
$location = "East US 2"

$sourceStorageAccountName = "hditutorialdata"  
$sourceContainerName = "adfhiveactivity"

$destStorageAccountName = $storageAccountName
$destContainerName = "adfgetstarted" # don't change this value.

####################################
# Connect tooAzure
####################################
#region - Connect tooAzure subscription
Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
try{Get-AzureRmContext}
catch{Login-AzureRmAccount}
#endregion

####################################
# Create a resource group, storage, and container
####################################

#region - create Azure resources
Write-Host "`nCreating resource group, storage account and blob container ..." -ForegroundColor Green

New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
New-AzureRmStorageAccount `
    -ResourceGroupName $resourceGroupName `
    -Name $destStorageAccountName `
    -type Standard_LRS `
    -Location $location

$destStorageAccountKey = (Get-AzureRmStorageAccountKey `
    -ResourceGroupName $resourceGroupName `
    -Name $destStorageAccountName)[0].Value

$sourceContext = New-AzureStorageContext `
    -StorageAccountName $sourceStorageAccountName `
    -Anonymous
$destContext = New-AzureStorageContext `
    -StorageAccountName $destStorageAccountName `
    -StorageAccountKey $destStorageAccountKey

New-AzureStorageContainer -Name $destContainerName -Context $destContext
#endregion

####################################
# Copy files
####################################
#region - copy files
Write-Host "`nCopying files ..." -ForegroundColor Green

$blobs = Get-AzureStorageBlob `
    -Context $sourceContext `
    -Container $sourceContainerName

$blobs|Start-AzureStorageBlobCopy `
    -DestContext $destContext `
    -DestContainer $destContainerName

Write-Host "`nCopied files ..." -ForegroundColor Green
Get-AzureStorageBlob -Context $destContext -Container $destContainerName
#endregion

Write-host "`nYou will use hello following values:" -ForegroundColor Green
write-host "`nResource group name: $resourceGroupName"
Write-host "Storage Account Name: $destStorageAccountName"
write-host "Storage Account Key: $destStorageAccountKey"

Write-host "`nScript completed" -ForegroundColor Green
```

Jeśli potrzebujesz pomocy dotyczącej hello skrypt programu PowerShell, zobacz [hello Using Azure PowerShell z usługą Azure Storage](../storage/common/storage-powershell-guide-full.md). Jeśli chcesz toouse wiersza polecenia platformy Azure, zobacz hello [dodatku](#appendix) sekcji hello skryptu wiersza polecenia platformy Azure.

**tooexamine hello magazynu konto i hello zawartość**

1. Zaloguj się na toohello [portalu Azure](https://portal.azure.com).
2. Kliknij przycisk **grup zasobów** w okienku po lewej stronie powitania.
3. Kliknij dwukrotnie nazwę grupy zasobów hello utworzone za pomocą skryptu programu PowerShell. Użyj filtru hello, jeśli masz zbyt wiele grup zasobów na liście.
4. Na powitania **zasobów** kafelka, powinna mieć jeden zasób z listy, chyba że współużytkować hello grupy zasobów z innymi projektami. Ten zasób jest hello konta magazynu o nazwie hello określone wcześniej. Kliknij nazwę konta magazynu hello.
5. Kliknij przycisk hello **obiekty BLOB** Kafelki.
6. Kliknij przycisk hello **adfgetstarted** kontenera. Zobacz dwa foldery: **inputdata** i **skryptu**.
7. Otwórz hello folder i sprawdź hello plików w folderach hello. Hello inputdata zawiera plik input.log hello z danych wejściowych i hello skryptu folder zawiera plik skryptu hello HiveQL.

## <a name="create-a-data-factory-using-resource-manager-template"></a>Tworzenie fabryki danych przy użyciu szablonu usługi Resource Manager
Konta magazynu hello, hello danych wejściowych i hello skrypt HiveQL przygotowane są gotowe toocreate fabryki danych Azure. Istnieje kilka metod tworzenia fabryki danych. Przez wdrożenie szablonu usługi Azure Resource Manager przy użyciu hello portalu Azure, w tym samouczku tworzenie fabryki danych. Można także wdrożyć przy użyciu szablonu usługi Resource Manager [interfejsu wiersza polecenia Azure](../azure-resource-manager/resource-group-template-deploy-cli.md) i [programu Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template). Dla innych metod tworzenia fabryki danych, zobacz [samouczek: Tworzenie pierwszego fabrykę danych](../data-factory/data-factory-build-your-first-pipeline.md).

1. Kliknij przycisk hello toosign obrazu w tooAzure i otwórz hello szablonu usługi Resource Manager w hello portalu Azure. Szablon Hello znajduje się w https://hditutorialdata.blob.core.windows.net/adfhiveactivity/data-factory-hdinsight-on-demand.json. Zobacz hello [jednostek fabryki danych w szablonie hello](#data-factory-entities-in-the-template) sekcji, aby uzyskać szczegółowe informacje na temat jednostek zdefiniowanych w szablonie hello. 

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fadfhiveactivity%2Fdata-factory-hdinsight-on-demand.json" target="_blank"><img src="./media/hdinsight-hadoop-create-linux-clusters-adf/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. Wybierz **Użyj istniejącego** opcję hello **grupy zasobów** ustawienie i wybierz hello nazwę grupy zasobów hello utworzony w poprzednim kroku hello (przy użyciu skryptu programu PowerShell).
3. Wprowadź nazwę dla fabryki danych hello (**nazwa fabryki danych**). Ta nazwa musi być globalnie unikatowa.
4. Wprowadź hello **nazwy konta magazynu** i **klucz konta magazynu** zapisanej w poprzednim kroku hello.
5. Wybierz **akceptuję warunki toohello** powyższych po odczytaniu za pośrednictwem **warunków i postanowień**.
6. Wybierz **toodashboard numeru Pin** opcji.
6. Kliknij przycisk **zakupu/utworzyć**. Zobacz kafelka na powitania pulpit nawigacyjny o nazwie **wdrażanie szablonu wdrożenia**. Poczekaj na powitania **grupy zasobów** zostanie otwarty blok grupy zasobów. Możesz również kliknąć Kafelek hello pod nazwą Twojej grupy nazwa tooopen hello zasobów bloku grupy zasobów.
6. Kliknięcie grupy zasobów hello hello kafelka tooopen bloku grupy zasobów hello nie jest jeszcze otwarty. Teraz powinien zostać wyświetlony zasobów fabryki danych więcej oprócz wymienionych zasobów konta magazynu toohello.
7. Kliknij nazwę hello w fabryce danych (wartość określona dla hello **nazwa fabryki danych** parametru).
8. W bloku fabryki danych powitania kliknij hello **Diagram** kafelka. Witaj diagram przedstawia jedno działanie z zestawem danych wejściowych i wyjściowy zestaw danych:

    ![Azure diagram potoku działania Hive HDInsight fabryki danych na żądanie](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-pipeline-diagram.png)

    nazwy Hello są definiowane w szablonie usługi Resource Manager hello.
9. Kliknij dwukrotnie **AzureBlobOutput**.
10. Na powitania **ostatnie zaktualizowane wycinków**, powinien zostać wyświetlony jeden wycinek typu. Jeśli jest w stanie hello **w toku**, poczekaj, aż zostanie on zmieniony zbyt**gotowe**. Zwykle trwa około **20 minut** toocreate klastra usługi HDInsight.

### <a name="check-hello-data-factory-output"></a>Sprawdź dane wyjściowe fabryki danych hello

1. Użyj hello same procedury w programie hello ostatniej sesji toocheck hello kontenery hello adfgetstarted kontenera. Istnieją dwa nowe kontenery dodatkowo zbyt**adfgetsarted**:

   * Kontener o nazwie następującym wzorzec hello: `adf<yourdatafactoryname>-linkedservicename-datetimestamp`. Ten kontener jest hello domyślny kontener dla klastra usługi HDInsight hello.
   * adfjobs: ten kontener jest kontener hello ADF hello z dziennikami zadań.

     dane wyjściowe fabryki danych Hello są przechowywane w **afgetstarted** zgodnie z konfiguracją w hello szablonu usługi Resource Manager.
2. Kliknij przycisk **adfgetstarted**.
3. Kliknij dwukrotnie **partitioneddata**. Zostanie wyświetlony **roku = 2014** folderu, ponieważ wszystkie dzienniki sieci web hello są dniu 2014 roku.

    ![Azure HDInsight fabryki danych na żądanie Hive potoku dane wyjściowe działania](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-year.png)

    Jeśli możesz przejść do szczegółów listy hello, zostanie wyświetlona trzy foldery stycznia, lutego i marca. I ma dziennika dla każdego miesiąca.

    ![Azure HDInsight fabryki danych na żądanie Hive potoku dane wyjściowe działania](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-month.png)

## <a name="data-factory-entities-in-hello-template"></a>Obiekty fabryki danych w szablonie hello
Oto, jak hello najwyższego poziomu szablonu usługi Resource Manager dla fabryki danych wygląda następująco:

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": { ...
    },
    "variables": { ...
    },
    "resources": [
        {
            "name": "[parameters('dataFactoryName')]",
            "apiVersion": "[variables('apiVersion')]",
            "type": "Microsoft.DataFactory/datafactories",
            "location": "westus",
            "resources": [
                { ... },
                { ... },
                { ... },
                { ... }
            ]
        }
    ]
}
```

### <a name="define-data-factory"></a>Definiowanie fabryki danych
Fabryka danych definiuje się w szablonie usługi Resource Manager hello pokazane na powitania następujące przykładowe:  

```json
"resources": [
{
    "name": "[parameters('dataFactoryName')]",
    "apiVersion": "[variables('apiVersion')]",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "westus",
}
```
Hello dataFactoryName jest hello nazwa fabryki danych hello przez użytkownika podczas wdrażania szablonu hello. Fabryka danych jest obecnie obsługiwane tylko w regionach wschodnie stany USA, zachodnie stany USA i Europa Północna, Europa hello.

### <a name="defining-entities-within-hello-data-factory"></a>Definiowanie jednostek w fabryce danych hello
Hello następujące jednostek fabryki danych są definiowane w szablonie JSON hello:

* [Połączona usługa Azure Storage](#azure-storage-linked-service)
* [Połączona usługa HDInsight na żądanie](#hdinsight-on-demand-linked-service)
* [Wejściowy zestaw danych obiektów blob platformy Azure](#azure-blob-input-dataset)
* [Wyjściowy zestaw danych obiektów blob platformy Azure](#azure-blob-output-dataset)
* [Potok danych z działaniem kopiowania](#data-pipeline)

#### <a name="azure-storage-linked-service"></a>Połączona usługa Azure Storage
Hello Azure Storage połączone usługi łączy fabrykę danych toohello konta magazynu platformy Azure. W tym samouczku hello tego samego konta magazynu jest używany jako hello domyślne konto magazynu usługi HDInsight, Magazyn danych wejściowych i przechowywania danych wyjściowych. W związku z tym można zdefiniować tylko jednego magazynu Azure połączonej usługi. W definicji usługi hello połączone Określ nazwę hello i klucza konta magazynu Azure. Zobacz [połączonej usługi magazynu Azure](../data-factory/data-factory-azure-blob-connector.md#azure-storage-linked-service) szczegółowe informacje o toodefine właściwości używane w formacie JSON połączonej usługi magazynu Azure.

```json
{
    "name": "[variables('storageLinkedServiceName')]",
    "type": "linkedservices",
    "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]" ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]"
        }
    }
}
```
Witaj **connectionString** używa hello parametry storageAccountName i storageAccountKey. Podczas wdrażania szablonu hello można określić wartości tych parametrów.  

#### <a name="hdinsight-on-demand-linked-service"></a>Połączona usługa HDInsight na żądanie
W hello HDInsight na żądanie połączone definicji usługi, można określić wartości parametrów konfiguracji, które są używane przez toocreate usługi fabryka danych hello klastra usługi HDInsight Hadoop w czasie wykonywania. Zobacz [obliczeniowe połączonych usług](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) artykuł szczegółowe informacje o toodefine właściwości używane w formacie JSON na żądanie połączoną usługą usługi HDInsight.  

```json

{
    "type": "linkedservices",
    "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "sshUserName": "myuser",                            
            "sshPassword": "MyPassword!",
            "linkedServiceName": "[variables('storageLinkedServiceName')]"
        }
    }
}
```
Należy zwrócić uwagę hello następujące punkty:

* Witaj fabryki danych tworzy **opartych na systemie Linux** klastra usługi HDInsight dla Ciebie.
* Witaj klastra usługi HDInsight Hadoop jest tworzony w hello sam regionu co konto magazynu hello.
* Powiadomienie hello *timeToLive* ustawienie. fabryki danych Hello automatycznie usuwa hello klastra, po bezczynności hello klastra przez 30 minut.
* Tworzy klaster usługi HDInsight Hello **domyślny kontener** w magazynie obiektów blob hello określone w hello JSON (**linkedServiceName**). Po usunięciu klastra hello HDInsight nie usunie tego kontenera. To zachowanie jest celowe. Z usługą HDInsight połączony na żądanie, klastra usługi HDInsight jest tworzony za każdym razem, gdy wycinek musi toobe przetwarzane, o ile istnieje istniejącego klastra na żywo (**timeToLive**) i zostaną usunięte po zakończeniu przetwarzania hello.

Szczegółowe informacje znajdują się w artykule [On-demand HDInsight Linked Service](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) (Połączona usługa HDInsight na żądanie).

> [!IMPORTANT]
> Po przetworzeniu większej liczby wycinków w usłudze Azure Blob Storage będzie widocznych wiele kontenerów. Jeśli nie ma potrzeby do rozwiązywania problemów hello zadań, możesz toodelete ich magazynu hello tooreduce kosztów. nazwy Hello kontenery wykonaj wzorca: "adf**yourdatafactoryname**-**linkedservicename**- datetimestamp". Użyj narzędzia takiego jak [Eksploratora magazynu](http://storageexplorer.com/) magazynu obiektów blob toodelete kontenerów w platformy Azure.

#### <a name="azure-blob-input-dataset"></a>Wejściowy zestaw danych obiektów blob platformy Azure
W definicji zestawu danych wejściowych hello należy określić nazwy hello folder, plik zawierający dane wejściowe hello i kontener obiektów blob. Zobacz [właściwości zestawu danych obiektów Blob platformy Azure](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) szczegółowe informacje o toodefine właściwości używane JSON zestawu danych obiektów Blob platformy Azure.

```json

{
    "type": "datasets",
    "name": "[variables('blobInputDatasetName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('storageLinkedServiceName')]",
        "typeProperties": {
            "fileName": "input.log",
            "folderPath": "adfgetstarted/inputdata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}

```

Zwróć uwagę hello następujące ustawienia określone w definicji JSON hello:

```json
"fileName": "input.log",
"folderPath": "adfgetstarted/inputdata",
```

#### <a name="azure-blob-output-dataset"></a>Wyjściowy zestaw danych obiektów blob platformy Azure
W definicji zestawu danych wyjściowych hello należy określić nazwy hello kontenera obiektów blob i folderu, która przechowuje dane wyjściowe hello. Zobacz [właściwości zestawu danych obiektów Blob platformy Azure](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) szczegółowe informacje o toodefine właściwości używane JSON zestawu danych obiektów Blob platformy Azure.  

```json

{
    "type": "datasets",
    "name": "[variables('blobOutputDatasetName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('storageLinkedServiceName')]",
        "typeProperties": {
            "folderPath": "adfgetstarted/partitioneddata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1,
            "style": "EndOfInterval"
        }
    }
}
```

Witaj folderPath określa hello folder toohello ścieżki, która przechowuje dane wyjściowe hello:

```json
"folderPath": "adfgetstarted/partitioneddata",
```

Witaj [dostępności zestawu danych](../data-factory/data-factory-create-datasets.md#dataset-availability) ustawienie wygląda następująco:

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "style": "EndOfInterval"
},
```

W fabryce danych Azure wyjściowej potoku hello dysków dostępności zestawu danych. W tym przykładzie wycinek hello jest tworzony co miesiąc na powitania ostatni dzień miesiąca (EndOfInterval). Aby uzyskać więcej informacji, zobacz [planowania fabryki danych i wykonywania](../data-factory/data-factory-scheduling-and-execution.md).

#### <a name="data-pipeline"></a>Potok danych
Należy zdefiniować potok, który przekształca danych przez uruchomienie skryptu Hive w klastrze usługi Azure HDInsight na żądanie. Zobacz [JSON potoku](../data-factory/data-factory-create-pipelines.md#pipeline-json) opisy toodefine elementów JSON potoku, w tym przykładzie.

```json
{
    "type": "datapipelines",
    "name": "[parameters('dataFactoryName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('hdInsightOnDemandLinkedServiceName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/datasets/', variables('blobInputDatasetName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/datasets/', variables('blobOutputDatasetName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "description": "Azure Data Factory pipeline with an Hadoop Hive activity",
        "activities": [
            {
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                    "scriptLinkedService": "[variables('storageLinkedServiceName')]",
                    "defines": {
                        "inputtable": "[concat('wasb://adfgetstarted@', parameters('storageAccountName'), '.blob.core.windows.net/inputdata')]",
                        "partitionedtable": "[concat('wasb://adfgetstarted@', parameters('storageAccountName'), '.blob.core.windows.net/partitioneddata')]"
                    }
                },
                "inputs": [
                    {
                        "name": "AzureBlobInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "policy": {
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "RunSampleHiveActivity",
                "linkedServiceName": "HDInsightOnDemandLinkedService"
            }
        ],
        "start": "2016-01-01T00:00:00Z",
        "end": "2016-01-31T00:00:00Z",
        "isPaused": false
    }
}
```

potok Hello zawiera jedno działanie, HDInsightHive działania. Jak zarówno rozpoczęcia i zakończenia daty są styczeń 2016 r., dane tylko jeden miesiąc (wycinek) jest przetwarzane. Zarówno *start* i *zakończenia* hello działania mają datę przeszłą, więc hello fabryki danych przetwarza dane dla miesiąca hello natychmiast. Jeśli zakończenie hello jest datą przyszłą, fabryki danych hello tworzy innego wycinek hello nastąpi. Aby uzyskać więcej informacji, zobacz [planowania fabryki danych i wykonywania](../data-factory/data-factory-scheduling-and-execution.md).

## <a name="clean-up-hello-tutorial"></a>Wyczyść hello samouczka

### <a name="delete-hello-blob-containers-created-by-on-demand-hdinsight-cluster"></a>Usuń kontenerów obiektów blob hello utworzoną przez klaster usługi HDInsight na żądanie
Z usługą HDInsight połączony na żądanie klaster usługi HDInsight jest tworzony za każdym razem, gdy wycinek musi toobe przetwarzane, o ile istnieje istniejącego klastra na żywo (timeToLive); i hello klastra zostaną usunięte po zakończeniu przetwarzania hello. Dla każdego klastra fabryki danych Azure tworzy kontener obiektów blob w hello używane jako konto stroage domyślne powitania dla klastra hello magazynu obiektów blob platformy Azure. Nawet po usunięciu klastra usługi HDInsight hello domyślnego kontenera magazynu obiektów blob i hello skojarzone konto magazynu nie zostaną usunięte. To zachowanie jest celowe. Po przetworzeniu większej liczby wycinków w usłudze Azure Blob Storage będzie widocznych wiele kontenerów. Jeśli nie ma potrzeby do rozwiązywania problemów hello zadań, możesz toodelete ich magazynu hello tooreduce kosztów. nazwy Hello kontenery wykonaj wzorca: `adfyourdatafactoryname-linkedservicename-datetimestamp`.

Usuń hello **adfjobs** i **adfyourdatafactoryname-linkedservicename-datetimestamp** folderów. kontener adfjobs Hello zawiera z fabryki danych Azure z dziennikami zadań.

### <a name="delete-hello-resource-group"></a>Usuń grupę zasobów hello
[Usługa Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) jest używane toodeploy, zarządzanie i monitorowanie rozwiązania jako grupa.  Usunięcie grupy zasobów powoduje usunięcie wszystkich składników hello wewnątrz hello grupy.  

1. Zaloguj się na toohello [portalu Azure](https://portal.azure.com).
2. Kliknij przycisk **grup zasobów** w okienku po lewej stronie powitania.
3. Kliknij nazwę grupy zasobów hello utworzone za pomocą skryptu programu PowerShell. Użyj filtru hello, jeśli masz zbyt wiele grup zasobów na liście. Witaj, grupy zasobów zostanie otwarty w nowym bloku.
4. Na powitania **zasobów** kafelka, użytkownik ma hello domyślne konto magazynu i fabryki danych hello, chyba że współużytkować hello grupy zasobów z innymi projektami na liście.
5. Kliknij przycisk **usunąć** u góry hello hello bloku. To spowoduje usunięcie konta magazynu hello i hello dane przechowywane na koncie magazynu hello.
6. Wprowadź hello zasobów grupy nazwa tooconfirm usunięcia, a następnie kliknij przycisk **usunąć**.

W przypadku, gdy nie ma konta magazynu hello toodelete podczas usuwania grupy zasobów hello, należy wziąć pod uwagę powitania po architektura oddzielając hello danych biznesowych z hello domyślne konto magazynu. W takim przypadku jedna grupa zasobów dla konta magazynu hello hello danych biznesowych i hello innej grupie zasobów dla hello domyślne konto magazynu dla usługi HDInsight połączonej usługi i hello fabryki danych. Po usunięciu hello drugiej grupy zasobów nie wpływa na konto magazynu danych biznesowych hello. toodo tak:

* Dodaj hello następujące grupy zasobów najwyższego poziomu toohello wraz z hello Microsoft.DataFactory/datafactories zasobów w szablonie usługi Resource Manager. Tworzy konto magazynu:

    ```json
    {
        "name": "[parameters('defaultStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": {

        },
        "properties": {
            "accountType": "Standard_LRS"
        }
    },
    ```
* Dodaj nowe konto nowego magazynu punktu toohello połączonej usługi:

    ```json
    {
        "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]" ],
        "type": "linkedservices",
        "name": "[variables('defaultStorageLinkedServiceName')]",
        "apiVersion": "[variables('apiVersion')]",
        "properties": {
            "type": "AzureStorage",
            "typeProperties": {
                "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('defaultStorageAccountName'),';AccountKey=',listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('defaultStorageAccountName')), variables('defaultApiVersion')).key1)]"
            }
        }
    },
    ```
* Skonfiguruj hello HDInsight na żądanie połączone usługi z dodatkowych dependsOn i additionalLinkedServiceNames:

    ```json
    {
        "dependsOn": [
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('defaultStorageLinkedServiceName'))]",
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('storageLinkedServiceName'))]"

        ],
        "type": "linkedservices",
        "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
        "apiVersion": "[variables('apiVersion')]",
        "properties": {
            "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "sshUserName": "myuser",                            
                "sshPassword": "MyPassword!",
                "linkedServiceName": "[variables('storageLinkedServiceName')]",
                "additionalLinkedServiceNames": "[variables('defaultStorageLinkedServiceName')]"
            }
        }
    },            
    ```
## <a name="next-steps"></a>Następne kroki
W tym artykule wiesz już, jak tooprocess klastra usługi HDInsight toouse fabryki danych Azure toocreate na żądanie zadań Hive. tooread więcej:

* [Samouczek Hadoop: rozpoczynanie pracy z opartą na systemie Linux platformą Hadoop w usłudze HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
* [Tworzenie klastrów opartych na systemie Linux platformą Hadoop w usłudze HDInsight](hdinsight-hadoop-provision-linux-clusters.md)
* [Dokumentacja dotycząca usługi HDInsight](https://azure.microsoft.com/documentation/services/hdinsight/)
* [Dokumentacja fabryki danych](https://azure.microsoft.com/documentation/services/data-factory/)

## <a name="appendix"></a>Dodatek

### <a name="azure-cli-script"></a>Skryptu interfejsu wiersza polecenia platformy Azure
Można użyć interfejsu wiersza polecenia Azure, zamiast przy użyciu programu Azure PowerShell toodo hello samouczka. toouse wiersza polecenia platformy Azure, najpierw zainstaluj wiersza polecenia platformy Azure zgodnie z instrukcjami hello:

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

#### <a name="use-azure-cli-tooprepare-hello-storage-and-copy-hello-files"></a>Użyj interfejsu wiersza polecenia Azure tooprepare hello magazynu i skopiuj pliki hello

```
azure login

azure config mode arm

azure group create --name "<Azure Resource Group Name>" --location "East US 2"

azure storage account create --resource-group "<Azure Resource Group Name>" --location "East US 2" --type "LRS" <Azure Storage Account Name>

azure storage account keys list --resource-group "<Azure Resource Group Name>" "<Azure Storage Account Name>"
azure storage container create "adfgetstarted" --account-name "<Azure Storage AccountName>" --account-key "<Azure Storage Account Key>"

azure storage blob copy start "https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log" --dest-account-name "<Azure Storage Account Name>" --dest-account-key "<Azure Storage Account Key>" --dest-container "adfgetstarted"
azure storage blob copy start "https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql" --dest-account-name "<Azure Storage Account Name>" --dest-account-key "<Azure Storage Account Key>" --dest-container "adfgetstarted"
```

Nazwa kontenera Hello jest *adfgetstarted*. Zachować, ponieważ jest on. W przeciwnym razie należy szablonu usługi Resource Manager hello tooupdate. Aby uzyskać pomoc dotyczącą tego skryptu interfejsu wiersza polecenia, zobacz [hello używanie interfejsu wiersza polecenia Azure z usługą Azure Storage](../storage/common/storage-azure-cli.md).
