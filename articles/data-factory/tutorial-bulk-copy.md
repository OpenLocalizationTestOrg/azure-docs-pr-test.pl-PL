---
title: "Zbiorcze kopiowanie danych przy użyciu usługi Azure Data Factory | Microsoft Docs"
description: "Dowiedz się, jak używać usługi Azure Data Factory i działania kopiowania do zbiorczego kopiowania danych ze źródłowego magazynu danych do docelowego magazynu danych."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: spelluru
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/22/2018
ms.author: jingwang
ms.openlocfilehash: 9971eb9e069d9fe1148c293c3459a8b11d931c2a
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/23/2018
---
# <a name="copy-multiple-tables-in-bulk-by-using-azure-data-factory"></a>Zbiorcze kopiowanie wielu tabel przy użyciu usługi Azure Data Factory
W tym samouczku przedstawiono **kopiowanie wielu tabel z bazy danych Azure SQL Database do usługi Azure SQL Data Warehouse**. Tego samego wzorca można użyć także w innych scenariuszach kopiowania. Na przykład kopiowanie tabel z programu SQL Server/Oracle do usługi Azure SQL Database/Data Warehouse/Azure Blob, kopiowanie różnych ścieżek z obiektów blob do tabeli bazy danych Azure SQL Database.

> [!NOTE]
> Ten artykuł dotyczy wersji 2 usługi Data Factory, która jest obecnie dostępna w wersji zapoznawczej. Jeśli używasz dostępnej ogólnie wersji 1 usługi Data Factory, zobacz [dokumentację dotyczącą usługi Data Factory w wersji 1](v1/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

Na poziomie ogólnym ten samouczek obejmuje następujące kroki:

> [!div class="checklist"]
> * Tworzenie fabryki danych.
> * Tworzenie połączonych usług Azure SQL Database, Azure SQL Data Warehouse i Azure Storage.
> * Tworzenie zestawów danych Azure SQL Database i Azure SQL Data Warehouse.
> * Tworzenie potoku w celu wyszukania tabel do skopiowania i innego potoku w celu wykonania samej operacji kopiowania. 
> * Uruchamianie działania potoku.
> * Monitorowanie uruchomień potoku i działań.

W tym samouczku jest używany program Azure PowerShell. Aby dowiedzieć się więcej o zastosowaniu innych narzędzi/zestawów SDK do tworzenia fabryki danych, zapoznaj się z przewodnikami [Szybki start](quickstart-create-data-factory-dot-net.md). 

## <a name="end-to-end-workflow"></a>Kompletny przepływ pracy
Ten scenariusz obejmuje kilka tabel w usłudze Azure SQL Database, które chcemy skopiować do magazynu SQL Data Warehouse. Oto sekwencja logiczna kroków przepływu pracy, który następuje w potokach:

![Przepływ pracy](media/tutorial-bulk-copy/tutorial-copy-multiple-tables.png)

* Pierwszy potok wyszukuje listę tabel, które należy skopiować do magazynów danych ujścia.  Alternatywnie można utrzymywać tabelę metadanych, która zawiera listę wszystkich tabel do skopiowania do magazynu danych ujścia. Następnie potok wywołuje inny potok, który działa na wszystkich tabelach w bazie danych i wykonuje operację kopiowania danych.
* Drugi potok przeprowadza rzeczywiste kopiowanie. Pobiera listę tabel jako parametr. Dla każdej tabeli na liście skopiuj konkretną tabelę w bazie danych Azure SQL Database do odpowiedniej tabeli w magazynie SQL Data Warehouse przy użyciu [kopiowania etapowego za pośrednictwem usługi Blob Storage i bazy PolyBase](connector-azure-sql-data-warehouse.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) w celu uzyskania najlepszej wydajności. W tym przykładzie pierwszy potok przekazuje listę tabel jako wartość parametru. 

Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne](https://azure.microsoft.com/free/) konto.

## <a name="prerequisites"></a>Wymagania wstępne

* Zainstalowanie programu **Azure PowerShell**. Wykonaj instrukcje podane w temacie [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/install-azurerm-ps).
* **Konto usługi Azure Storage**. Konto usługi Azure Storage jest używane jako przejściowy magazyn obiektów blob w operacji kopiowania zbiorczego. 
* **Usługa Azure SQL Database**. Ta baza danych zawiera dane źródłowe. 
* **Magazyn Azure SQL Data Warehouse**. Ten magazyn danych służy do przechowywania danych skopiowanych z bazy SQL Database. 

### <a name="prepare-sql-database-and-sql-data-warehouse"></a>Przygotowywanie bazy danych SQL Database i magazynu SQL Data Warehouse

**Przygotowywanie źródłowej bazy Azure SQL Database**:

Utwórz bazę Azure SQL Database z przykładowymi danymi Adventure Works LT zgodnie z artykułem [Tworzenie bazy danych Azure SQL](../sql-database/sql-database-get-started-portal.md). Ten samouczek kopiuje wszystkie tabele z tej przykładowej bazy danych do magazynu danych SQL.

**Przygotowywanie magazynu ujścia Azure SQL Data Warehouse**:

1. Jeśli nie masz magazynu Azure SQL Data Warehouse, utwórz go, wykonując czynności przedstawione w artykule [Create an Azure SQL Warehouse (Tworzenie magazynu Azure SQL Data Warehouse)](../sql-data-warehouse/sql-data-warehouse-get-started-tutorial.md).

2. Tworzenie odpowiednich schematów tabel w magazynie SQL Data Warehouse. Można użyć [narzędzia migracji](https://www.microsoft.com/download/details.aspx?id=49100) do **migracji schematów** z bazy danych Azure SQL Database do magazynu Azure SQL Data Warehouse. Usługa Azure Data Factory służy do migrowania/kopiowania danych na późniejszym etapie.

## <a name="azure-services-to-access-sql-server"></a>Usługi platformy Azure umożliwiające dostęp do serwera SQL

Zarówno dla bazy SQL Database, jak i dla magazynu SQL Data Warehouse, zezwól usługom Azure na dostęp do serwera SQL. Upewnij się, że ustawienie **Zezwalaj na dostęp do usług platformy Azure** dla serwera SQL Azure zostało **WŁĄCZONE**. Ustawienie to pozwala usłudze Data Factory na odczyt danych z bazy Azure SQL Database i zapis danych w magazynie Azure SQL Data Warehouse. W celu sprawdzenia i włączenia tego ustawienia wykonaj następujące kroki:

1. Kliknij centrum **Więcej usług** po lewej stronie, a następnie kliknij przycisk **Serwery SQL**.
2. Wybierz swój serwer, a następnie kliknij przycisk **Zapora** w obszarze **USTAWIENIA**.
3. Na stronie **Ustawienia zapory** kliknij pozycję **WŁĄCZ** dla ustawienia **Zezwalaj na dostęp do usług platformy Azure**.

## <a name="create-a-data-factory"></a>Tworzenie fabryki danych

1. Uruchom program **PowerShell**. Nie zamykaj programu Azure PowerShell, zanim nie wykonasz wszystkich instrukcji z tego samouczka. Jeśli go zamkniesz i otworzysz ponownie, musisz uruchomić te polecenia jeszcze raz.

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
2. Uruchom polecenie cmdlet **Set-AzureRmDataFactoryV2**, aby utworzyć fabrykę danych. Przed uruchomieniem polecenia zastąp symbole zastępcze własnymi wartościami. 

    ```powershell
    $resourceGroupName = "<your resource group to create the factory>"
    $dataFactoryName = "<specify the name of data factory to create. It must be globally unique.>"
    Set-AzureRmDataFactoryV2 -ResourceGroupName $resourceGroupName -Location "East US" -Name $dataFactoryName
    ```

    Pamiętaj o następujących kwestiach:

    * Nazwa fabryki danych Azure musi być globalnie unikatowa. Jeśli zostanie wyświetlony następujący błąd, zmień nazwę i spróbuj ponownie.

        ```
        The specified Data Factory name 'ADFv2QuickStartDataFactory' is already in use. Data Factory names must be globally unique.
        ```

    * Aby tworzyć wystąpienia usługi Data Factory, musisz być współautorem lub administratorem subskrypcji platformy Azure.
    * Obecnie usługa Data Factory w wersji 2 umożliwia tworzenie fabryk danych tylko w regionach Wschodnie stany USA, Wschodnie stany USA 2 i Europa Zachodnia. Magazyny danych (Azure Storage, Azure SQL Database itp.) i jednostki obliczeniowe (HDInsight itp.) używane przez fabrykę danych mogą mieścić się w innych regionach.

## <a name="create-linked-services"></a>Tworzenie połączonych usług

W tym samouczku utworzysz trzy połączone usługi dla źródłowego, ujściowego i przejściowego magazynu obiektów blob, co obejmuje połączenia z magazynami danych:

### <a name="create-the-source-azure-sql-database-linked-service"></a>Tworzenie źródłowej połączonej usługi Azure SQL Database

1. Utwórz plik JSON o nazwie **AzureSQLDatabaseLinkedService.json** w folderze **C:\ADFv2TutorialBulkCopy** o następującej zawartości: (utwórz folder ADFv2TutorialBulkCopy, jeśli jeszcze nie istnieje).

    > [!IMPORTANT]
    > Zastąp wartości &lt;servername&gt;, &lt;databasename&gt;, &lt;username&gt;@&lt;servername&gt; i &lt;password&gt; wartościami z bazy Azure SQL Database przed zapisaniem pliku.

    ```json
    {
        "name": "AzureSqlDatabaseLinkedService",
        "properties": {
            "type": "AzureSqlDatabase",
            "typeProperties": {
                "connectionString": {
                    "type": "SecureString",
                    "value": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
                }
            }
        }
    }
    ```

2. W programie **Azure PowerShell** przejdź do folderu **ADFv2TutorialBulkCopy**.

3. Uruchom polecenie cmdlet **Set-AzureRmDataFactoryV2LinkedService**, aby utworzyć połączoną usługę: **AzureSqlDatabaseLinkedService**. 

    ```powershell
    Set-AzureRmDataFactoryV2LinkedService -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "AzureSqlDatabaseLinkedService" -File ".\AzureSqlDatabaseLinkedService.json"
    ```

    Oto przykładowe dane wyjściowe:

    ```json
    LinkedServiceName : AzureSqlDatabaseLinkedService
    ResourceGroupName : <resourceGroupName>
    DataFactoryName   : <dataFactoryName>
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureSqlDatabaseLinkedService
    ```

### <a name="create-the-sink-azure-sql-data-warehouse-linked-service"></a>Tworzenie połączonej usługi ujścia Azure SQL Data Warehouse

1. W folderze **C:\ADFv2TutorialBulkCopy** utwórz plik JSON o nazwie **AzureSqlDWLinkedService.json** z następującą zawartością:

    > [!IMPORTANT]
    > Zastąp wartości &lt;servername&gt;, &lt;databasename&gt;, &lt;username&gt;@&lt;servername&gt; i &lt;password&gt; wartościami z bazy Azure SQL Database przed zapisaniem pliku.

    ```json
    {
        "name": "AzureSqlDWLinkedService",
        "properties": {
            "type": "AzureSqlDW",
            "typeProperties": {
                "connectionString": {
                    "type": "SecureString",
                    "value": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
            }
        }
    }
    ```

2. Aby utworzyć połączoną usługę **AzureSqlDWLinkedService**, uruchom polecenie cmdlet **Set-AzureRmDataFactoryV2LinkedService**.

    ```powershell
    Set-AzureRmDataFactoryV2LinkedService -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "AzureSqlDWLinkedService" -File ".\AzureSqlDWLinkedService.json"
    ```

    Oto przykładowe dane wyjściowe:

    ```json
    LinkedServiceName : AzureSqlDWLinkedService
    ResourceGroupName : <resourceGroupName>
    DataFactoryName   : <dataFactoryName>
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureSqlDWLinkedService
    ```

### <a name="create-the-staging-azure-storage-linked-service"></a>Tworzenie przejściowej połączonej usługi Azure Storage

W tym samouczku magazyn obiektów blob platformy Azure służy jako obszar przejściowy, pozwalający na włączenie programu PolyBase w celu podniesienia wydajności kopiowania.

1. W folderze **C:\ADFv2TutorialBulkCopy** utwórz plik JSON o nazwie **AzureStorageLinkedService.json** z następującą zawartością:

    > [!IMPORTANT]
    > Przed zapisaniem pliku zastąp wartości &lt;accountName&gt; i &lt;accountKey&gt; nazwą i kluczem konta usługi Azure Storage.

    ```json
    {
        "name": "AzureStorageLinkedService",
        "properties": {
            "type": "AzureStorage",
            "typeProperties": {
                "connectionString": {
                    "type": "SecureString",
                    "value": "DefaultEndpointsProtocol=https;AccountName=<accountName>;AccountKey=<accountKey>"
                }
            }
        }
    }
    ```

2. Aby utworzyć połączoną usługę **AzureStorageLinkedService**, uruchom polecenie cmdlet **Set-AzureRmDataFactoryV2LinkedService**.

    ```powershell
    Set-AzureRmDataFactoryV2LinkedService -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "AzureStorageLinkedService" -File ".\AzureStorageLinkedService.json"
    ```

    Oto przykładowe dane wyjściowe:

    ```json
    LinkedServiceName : AzureStorageLinkedService
    ResourceGroupName : <resourceGroupName>
    DataFactoryName   : <dataFactoryName>
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureStorageLinkedService
    ```

## <a name="create-datasets"></a>Tworzenie zestawów danych

W tym samouczku utworzysz zestawy danych źródła i ujścia, określające lokalizację przechowywania danych:

### <a name="create-a-dataset-for-source-sql-database"></a>Tworzenie zestawu danych źródłowej bazy danych SQL Database

1. W folderze **C:\ADFv2TutorialBulkCopy** utwórz plik JSON o nazwie **AzureSqlDatabaseDataset.json** z następującą zawartością. Nazwa „tableName” to nazwa tymczasowa, ponieważ w późniejszym czasie do pobierania danych używane jest zapytanie SQL w działaniu kopiowania.

    ```json
    {
        "name": "AzureSqlDatabaseDataset",
        "properties": {
            "type": "AzureSqlTable",
            "linkedServiceName": {
                "referenceName": "AzureSqlDatabaseLinkedService",
                "type": "LinkedServiceReference"
            },
            "typeProperties": {
                "tableName": "dummy"
            }
        }
    }
    ```

2. Aby utworzyć zestaw danych **AzureSqlDatabaseDataset**, uruchom polecenie cmdlet **Set-AzureRmDataFactoryV2Dataset**.

    ```powershell
    Set-AzureRmDataFactoryV2Dataset -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "AzureSqlDatabaseDataset" -File ".\AzureSqlDatabaseDataset.json"
    ```

    Oto przykładowe dane wyjściowe:

    ```json
    DatasetName       : AzureSqlDatabaseDataset
    ResourceGroupName : <resourceGroupname>
    DataFactoryName   : <dataFactoryName>
    Structure         :
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureSqlTableDataset
    ```

### <a name="create-a-dataset-for-sink-sql-data-warehouse"></a>Tworzenie zestawu danych ujścia magazynu SQL Data Warehouse

1. Utwórz plik JSON o nazwie **AzureSqlDWDataset.json** w folderze **C:\ADFv2TutorialBulkCopy**, z następującą zawartością: „tableName” ustawione jako parametr, następnie działanie kopiowania odwołujące się do tego zestawu danych przekazuje rzeczywistą wartość do zestawu danych.

    ```json
    {
        "name": "AzureSqlDWDataset",
        "properties": {
            "type": "AzureSqlDWTable",
            "linkedServiceName": {
                "referenceName": "AzureSqlDWLinkedService",
                "type": "LinkedServiceReference"
            },
            "typeProperties": {
                "tableName": {
                    "value": "@{dataset().DWTableName}",
                    "type": "Expression"
                }
            },
            "parameters":{
                "DWTableName":{
                    "type":"String"
                }
            }
        }
    }
    ```

2. Aby utworzyć zestaw danych **AzureSqlDWDataset**, uruchom polecenie cmdlet **Set-AzureRmDataFactoryV2Dataset**.

    ```powershell
    Set-AzureRmDataFactoryV2Dataset -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "AzureSqlDWDataset" -File ".\AzureSqlDWDataset.json"
    ```

    Oto przykładowe dane wyjściowe:

    ```json
    DatasetName       : AzureSqlDWDataset
    ResourceGroupName : <resourceGroupname>
    DataFactoryName   : <dataFactoryName>
    Structure         :
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureSqlDwTableDataset
    ```

## <a name="create-pipelines"></a>Tworzenie potoków

W tym samouczku utworzysz dwa potoki:

### <a name="create-the-pipeline-iterateandcopysqltables"></a>Tworzenie potoku „IterateAndCopySQLTables”

Ten potok pobiera listę tabel jako parametr. Dla każdej tabeli na liście kopiuje dane z tabeli w bazie Azure SQL Database do usługi Azure SQL Data Warehouse przy użyciu kopiowania przejściowego i programu PolyBase.

1. W folderze **C:\ADFv2TutorialBulkCopy** utwórz plik JSON o nazwie **IterateAndCopySQLTables.json** z następującą zawartością:

    ```json
    {
        "name": "IterateAndCopySQLTables",
        "properties": {
            "activities": [
                {
                    "name": "IterateSQLTables",
                    "type": "ForEach",
                    "typeProperties": {
                        "isSequential": "false",
                        "items": {
                            "value": "@pipeline().parameters.tableList",
                            "type": "Expression"
                        },
                        "activities": [
                            {
                                "name": "CopyData",
                                "description": "Copy data from SQL database to SQL DW",
                                "type": "Copy",
                                "inputs": [
                                    {
                                        "referenceName": "AzureSqlDatabaseDataset",
                                        "type": "DatasetReference"
                                    }
                                ],
                                "outputs": [
                                    {
                                        "referenceName": "AzureSqlDWDataset",
                                        "type": "DatasetReference",
                                        "parameters": {
                                            "DWTableName": "[@{item().TABLE_SCHEMA}].[@{item().TABLE_NAME}]"
                                        }
                                    }
                                ],
                                "typeProperties": {
                                    "source": {
                                        "type": "SqlSource",
                                        "sqlReaderQuery": "SELECT * FROM [@{item().TABLE_SCHEMA}].[@{item().TABLE_NAME}]"
                                    },
                                    "sink": {
                                        "type": "SqlDWSink",
                                        "preCopyScript": "TRUNCATE TABLE [@{item().TABLE_SCHEMA}].[@{item().TABLE_NAME}]",
                                        "allowPolyBase": true
                                    },
                                    "enableStaging": true,
                                    "stagingSettings": {
                                        "linkedServiceName": {
                                            "referenceName": "AzureStorageLinkedService",
                                            "type": "LinkedServiceReference"
                                        }
                                    }
                                }
                            }
                        ]
                    }
                }
            ],
            "parameters": {
                "tableList": {
                    "type": "Object"
                }
            }
        }
    }
    ```

2. W celu utworzenia potoku: **IterateAndCopySQLTables** uruchom polecenie cmdlet **Set-AzureRmDataFactoryV2Pipeline**.

    ```powershell
    Set-AzureRmDataFactoryV2Pipeline -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "IterateAndCopySQLTables" -File ".\IterateAndCopySQLTables.json"
    ```

    Oto przykładowe dane wyjściowe:

    ```json
    PipelineName      : IterateAndCopySQLTables
    ResourceGroupName : <resourceGroupName>
    DataFactoryName   : <dataFactoryName>
    Activities        : {IterateSQLTables}
    Parameters        : {[tableList, Microsoft.Azure.Management.DataFactory.Models.ParameterSpecification]}
    ```

### <a name="create-the-pipeline-gettablelistandtriggercopydata"></a>Tworzenie potoku „GetTableListAndTriggerCopyData”

Ten potok wykonuje dwie czynności:

* Wyszukuje tabelę systemową bazy Azure SQL Database w celu pobrania listy tabel do skopiowania.
* Wyzwala potok „IterateAndCopySQLTables”, który przeprowadza rzeczywiste kopiowanie danych.

1. W folderze **C:\ADFv2TutorialBulkCopy** utwórz plik JSON o nazwie **GetTableListAndTriggerCopyData.json** z następującą zawartością:

    ```json
    {
        "name":"GetTableListAndTriggerCopyData",
        "properties":{
            "activities":[
                { 
                    "name": "LookupTableList",
                    "description": "Retrieve the table list from Azure SQL dataabse",
                    "type": "Lookup",
                    "typeProperties": {
                        "source": {
                            "type": "SqlSource",
                            "sqlReaderQuery": "SELECT TABLE_SCHEMA, TABLE_NAME FROM information_schema.TABLES WHERE TABLE_TYPE = 'BASE TABLE' and TABLE_SCHEMA = 'SalesLT' and TABLE_NAME <> 'ProductModel'"
                        },
                        "dataset": {
                            "referenceName": "AzureSqlDatabaseDataset",
                            "type": "DatasetReference"
                        },
                        "firstRowOnly": false
                    }
                },
                {
                    "name": "TriggerCopy",
                    "type": "ExecutePipeline",
                    "typeProperties": {
                        "parameters": {
                            "tableList": {
                                "value": "@activity('LookupTableList').output.value",
                                "type": "Expression"
                            }
                        },
                        "pipeline": {
                            "referenceName": "IterateAndCopySQLTables",
                            "type": "PipelineReference"
                        },
                        "waitOnCompletion": true
                    },
                    "dependsOn": [
                        {
                            "activity": "LookupTableList",
                            "dependencyConditions": [
                                "Succeeded"
                            ]
                        }
                    ]
                }
            ]
        }
    }
    ```

2. W celu utworzenia potoku: **GetTableListAndTriggerCopyData** uruchom polecenie cmdlet **Set-AzureRmDataFactoryV2Pipeline**.

    ```powershell
    Set-AzureRmDataFactoryV2Pipeline -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "GetTableListAndTriggerCopyData" -File ".\GetTableListAndTriggerCopyData.json"
    ```

    Oto przykładowe dane wyjściowe:

    ```json
    PipelineName      : GetTableListAndTriggerCopyData
    ResourceGroupName : <resourceGroupName>
    DataFactoryName   : <dataFactoryName>
    Activities        : {LookupTableList, TriggerCopy}
    Parameters        :
    ```

## <a name="start-and-monitor-pipeline-run"></a>Uruchamianie i monitorowanie działania potoku

1. Uruchom działanie potoku dla głównego potoku „GetTableListAndTriggerCopyData” i zarejestruj identyfikator uruchomienia potoku do przyszłego monitorowania. Potok dodatkowo uruchamia potok „IterateAndCopySQLTables” zgodnie z definicją w działaniu ExecutePipeline.

    ```powershell
    $runId = Invoke-AzureRmDataFactoryV2Pipeline -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -PipelineName 'GetTableListAndTriggerCopyData'
    ```

2.  Uruchom następujący skrypt, aby stale sprawdzać stan uruchomienia potoku **GetTableListAndTriggerCopyData** oraz wydrukować ostateczny wynik uruchomienia potoku i działania.

    ```powershell
    while ($True) {
        $run = Get-AzureRmDataFactoryV2PipelineRun -ResourceGroupName $resourceGroupName -DataFactoryName $DataFactoryName -PipelineRunId $runId

        if ($run) {
            if ($run.Status -ne 'InProgress') {
                Write-Host "Pipeline run finished. The status is: " $run.Status -foregroundcolor "Yellow"
                Write-Host "Pipeline run details:" -foregroundcolor "Yellow"
                $run
                break
            }
            Write-Host  "Pipeline is running...status: InProgress" -foregroundcolor "Yellow"
        }

        Start-Sleep -Seconds 15
    }

    $result = Get-AzureRmDataFactoryV2ActivityRun -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -PipelineRunId $runId -RunStartedAfter (Get-Date).AddMinutes(-30) -RunStartedBefore (Get-Date).AddMinutes(30)
    Write-Host "Activity run details:" -foregroundcolor "Yellow"
    $result
    ```

    Oto dane wyjściowe przykładowego przebiegu:

    ```json
    Pipeline run details:
    ResourceGroupName : <resourceGroupName>
    DataFactoryName   : <dataFactoryName>
    RunId             : 0000000000-00000-0000-0000-000000000000
    PipelineName      : GetTableListAndTriggerCopyData
    LastUpdated       : 9/18/2017 4:08:15 PM
    Parameters        : {}
    RunStart          : 9/18/2017 4:06:44 PM
    RunEnd            : 9/18/2017 4:08:15 PM
    DurationInMs      : 90637
    Status            : Succeeded
    Message           : 

    Activity run details:
    ResourceGroupName : <resourceGroupName>
    DataFactoryName   : <dataFactoryName>
    ActivityName      : LookupTableList
    PipelineRunId     : 0000000000-00000-0000-0000-000000000000
    PipelineName      : GetTableListAndTriggerCopyData
    Input             : {source, dataset, firstRowOnly}
    Output            : {count, value, effectiveIntegrationRuntime}
    LinkedServiceName : 
    ActivityRunStart  : 9/18/2017 4:06:46 PM
    ActivityRunEnd    : 9/18/2017 4:07:09 PM
    DurationInMs      : 22995
    Status            : Succeeded
    Error             : {errorCode, message, failureType, target}

    ResourceGroupName : <resourceGroupName>
    DataFactoryName   : <dataFactoryName>
    ActivityName      : TriggerCopy
    PipelineRunId     : 0000000000-00000-0000-0000-000000000000
    PipelineName      : GetTableListAndTriggerCopyData
    Input             : {pipeline, parameters, waitOnCompletion}
    Output            : {pipelineRunId}
    LinkedServiceName : 
    ActivityRunStart  : 9/18/2017 4:07:11 PM
    ActivityRunEnd    : 9/18/2017 4:08:14 PM
    DurationInMs      : 62581
    Status            : Succeeded
    Error             : {errorCode, message, failureType, target}
    ```

3. Możesz uzyskać identyfikator uruchomienia potoku „**IterateAndCopySQLTables**” i sprawdzić szczegółowe wyniki uruchomienia działania zgodnie z poniższymi instrukcjami.

    ```powershell
    Write-Host "Pipeline 'IterateAndCopySQLTables' run result:" -foregroundcolor "Yellow"
    ($result | Where-Object {$_.ActivityName -eq "TriggerCopy"}).Output.ToString()
    ```

    Oto dane wyjściowe przykładowego przebiegu:

    ```json
    {
        "pipelineRunId": "7514d165-14bf-41fb-b5fb-789bea6c9e58"
    }
    ```

    ```powershell
    $result2 = Get-AzureRmDataFactoryV2ActivityRun -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -PipelineRunId <copy above run ID> -RunStartedAfter (Get-Date).AddMinutes(-30) -RunStartedBefore (Get-Date).AddMinutes(30)
    $result2
    ```

3. Połącz się z magazynem ujścia Azure SQL Data Warehouse i upewnij się, że dane zostały poprawnie skopiowane z bazy danych Azure SQL Database.

## <a name="next-steps"></a>Następne kroki
W ramach tego samouczka wykonano następujące procedury: 

> [!div class="checklist"]
> * Tworzenie fabryki danych.
> * Tworzenie połączonych usług Azure SQL Database, Azure SQL Data Warehouse i Azure Storage.
> * Tworzenie zestawów danych Azure SQL Database i Azure SQL Data Warehouse.
> * Tworzenie potoku w celu wyszukania tabel do skopiowania i innego potoku w celu wykonania samej operacji kopiowania. 
> * Uruchamianie działania potoku.
> * Monitorowanie uruchomień potoku i działań.

Przejdź do poniższego samouczka, aby dowiedzieć się, jak przyrostowo kopiować dane z lokalizacji źródłowej do docelowej:
> [!div class="nextstepaction"]
>[Przyrostowe kopiowanie danych](tutorial-incremental-copy-powershell.md)