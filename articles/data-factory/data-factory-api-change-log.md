---
title: "aaaData fabryki — dziennik zmian interfejsu API platformy .NET | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano istotne zmiany, funkcje, poprawki itp... w określonej wersji interfejsu API platformy .NET dla hello fabryki danych Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 8208271b-7f4c-4214-b665-d2ff503c4470
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: spelluru
ms.openlocfilehash: 1d44b45c3dc8f9d483d1f1cef7068edacc610932
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---net-api-change-log"></a>Fabryka danych Azure — dziennik zmian interfejs API .NET
Ten artykuł zawiera informacje dotyczące zmiany tooAzure SDK fabryki danych w określonej wersji. Fabryka danych Azure można znaleźć hello najnowszy pakiet NuGet [tutaj](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories)

## <a name="version-4110"></a>Wersja 4.11.0
Funkcja dodatków:

* Witaj następujących typów połączonych usług zostały dodane:
  * [OnPremisesMongoDbLinkedService](https://msdn.microsoft.com/library/mt765129.aspx)
  * [AmazonRedshiftLinkedService](https://msdn.microsoft.com/library/mt765121.aspx)
  * [AwsAccessKeyLinkedService](https://msdn.microsoft.com/library/mt765144.aspx)
* dodano następujące typy obiektów dataset Hello:
  * [MongoDbCollectionDataset](https://msdn.microsoft.com/library/mt765145.aspx)
  * [AmazonS3Dataset](https://msdn.microsoft.com/library/mt765112.aspx)
* następujące Hello skopiuj źródła, których typy zostały dodane:
  * [MongoDbSource](https://msdn.microsoft.com/library/mt765123.aspx)

## <a name="version-4100"></a>Wersja 4.10.0
* dodano następujące właściwości opcjonalne Hello tooTextFormat:
  * [SkipLineCount](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.textformat.skiplinecount.aspx)
  * [FirstRowAsHeader](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.textformat.firstrowasheader.aspx)
  * [TreatEmptyAsNull](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.textformat.treatemptyasnull.aspx)
* Witaj następujących typów połączonych usług zostały dodane:
  * [OnPremisesCassandraLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.onpremisescassandralinkedservice.aspx)
  * [SalesforceLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.salesforcelinkedservice.aspx)
* dodano następujące typy obiektów dataset Hello:
  * [OnPremisesCassandraTableDataset](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.onpremisescassandratabledataset.aspx)
* następujące Hello skopiuj źródła, których typy zostały dodane:
  * [CassandraSource](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.cassandrasource.aspx)
* Dodaj [WebServiceInputs](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.azuremlbatchexecutionactivity.webserviceinputs.aspx) tooAzureMLBatchExecutionActivity właściwości
  * Włącz przekazywanie eksperymentu uczenia maszynowego Azure tooan wielu danych wejściowych usługi sieci web

## <a name="version-491"></a>Wersja 4.9.1
### <a name="bug-fix"></a>Poprawka błędu
* Zastąpić uwierzytelniania opartego na WebApi dla [WebLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.weblinkedservice.authenticationtype.aspx).

## <a name="version-490"></a>Wersja 4.9.0
### <a name="feature-additions"></a>Dodawanie funkcji
* Dodaj [EnableStaging](https://msdn.microsoft.com/library/mt767916.aspx) i [StagingSettings](https://msdn.microsoft.com/library/mt767918.aspx) tooCopyActivity właściwości. Zobacz [przemieszczane kopiowania](data-factory-copy-activity-performance.md#staged-copy) szczegółowe informacje na temat funkcji hello.

### <a name="bug-fix"></a>Poprawka błędu
* Wprowadzenie przeciążenia [ActivityWindowOperationExtensions.List](https://msdn.microsoft.com/library/mt767915.aspx) metodę, która przyjmuje [ActivityWindowsByActivityListParameters](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.activitywindowsbyactivitylistparameters.aspx) wystąpienia.
* Oznacz [WriteBatchSize](https://msdn.microsoft.com/library/dn884293.aspx) i [WriteBatchTimeout](https://msdn.microsoft.com/library/dn884245.aspx) jako opcjonalne w CopySink.

## <a name="version-480"></a>Wersja 4.8.0
### <a name="feature-additions"></a>Dodawanie funkcji
* Dodano Hello następujące opcjonalne właściwości działania tooCopy wpisz tooenable dostrajania wydajności kopiowania:
  * [ParallelCopies](https://msdn.microsoft.com/library/mt767910.aspx)
  * [CloudDataMovementUnits](https://msdn.microsoft.com/library/mt767912.aspx)

## <a name="version-470"></a>Wersja 4.7.0
### <a name="feature-additions"></a>Dodawanie funkcji
* Dodano nowy typ StorageFormat [OrcFormat](https://msdn.microsoft.com/library/mt723391.aspx) wpisz toocopy pliki w formacie (ORC) kolumnowym zoptymalizowane wiersza.
* Dodaj [AllowPolyBase](https://msdn.microsoft.com/library/mt723396.aspx) i tooSqlDWSink właściwości usługi.
  * Umożliwia korzystanie hello PolyBase toocopy danych do usługi SQL Data Warehouse.

## <a name="version-461"></a>Wersji 4.6.1
### <a name="bug-fixes"></a>Poprawki błędów
* Rozwiązuje żądania HTTP do wyświetlania listy działania systemu windows.
  * Usuwa Nazwa grupy zasobów hello i nazwa fabryki danych hello hello ładunku żądania.

## <a name="version-460"></a>Wersja 4.6.0
### <a name="feature-additions"></a>Dodawanie funkcji
* Witaj następujące właściwości zostały dodane za[PipelineProperties](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.pipelineproperties_properties.aspx):
  * [PipelineMode](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.pipelineproperties.pipelinemode.aspx)
  * [ExpirationTime](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.pipelineproperties.expirationtime.aspx)
  * [Zestawy danych](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.pipelineproperties.datasets.aspx)
* Witaj następujące właściwości zostały dodane za[PipelineRuntimeInfo](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.common.models.pipelineruntimeinfo.aspx):
  * [PipelineState](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.common.models.pipelineruntimeinfo.pipelinestate.aspx)
* Dodano nowe [StorageFormat](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.storageformat.aspx) typu [JsonFormat](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.jsonformat.aspx) wpisz toodefine zestawów danych, którego dane są w formacie JSON.

## <a name="version-450"></a>Wersja 4.5.0
### <a name="feature-additions"></a>Dodawanie funkcji
* Dodaje [listy operacji dla działania okna](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.activitywindowoperationsextensions.aspx).
  * Dodaje metody tooretrieve działania w systemie windows z filtrami na podstawie typów jednostek hello (oznacza to, fabryk danych, zestawy danych, potoki i działania).
* Witaj następujących typów połączonych usług zostały dodane:
  * [ODataLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.odatalinkedservice.aspx), [WebLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.weblinkedservice.aspx)
* dodano następujące typy obiektów dataset Hello:
  * [ODataResourceDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.odataresourcedataset.aspx), [WebTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.webtabledataset.aspx)
* następujące Hello skopiuj źródła, których typy zostały dodane:     
  * [WebSource](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.websource.aspx)

## <a name="version-440"></a>Wersja 4.4.0
### <a name="feature-additions"></a>Dodawanie funkcji
* Witaj następującego typu połączonej usługi został dodany jako źródła danych i sink dla działania kopiowania:
  * [AzureStorageSasLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.azurestoragesaslinkedservice.aspx). Zobacz [połączonej usługi SAS magazynu Azure](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) informacje koncepcyjne i przykłady.

## <a name="version-430"></a>Wersja 4.3.0
### <a name="feature-additions"></a>Dodawanie funkcji
* Witaj następujących był typu połączonej usługi został dodany jako źródła danych dla działania kopiowania:
  * [HdfsLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.hdfslinkedservice.aspx). Zobacz [przenoszenia danych z systemu plików HDFS przy użyciu fabryki danych](data-factory-hdfs-connector.md) informacje koncepcyjne i przykłady.
  * [OnPremisesOdbcLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.onpremisesodbclinkedservice.aspx). Zobacz [przenoszenia danych z ODBC magazynów przy użyciu fabryki danych Azure](data-factory-odbc-connector.md) informacje koncepcyjne i przykłady.

## <a name="version-420"></a>Wersja 4.2.0
### <a name="feature-additions"></a>Dodawanie funkcji
* dodano następujące nowego typu działania Hello: [AzureMLUpdateResourceActivity](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuremlupdateresourceactivity.aspx). Aby uzyskać szczegółowe informacje o działaniu hello, zobacz [modeli aktualizowanie uczenie Maszynowe Azure przy użyciu hello działanie aktualizacji zasobu](data-factory-azure-ml-batch-execution-activity.md).
* Nowe właściwości opcjonalne [updateResourceEndpoint](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuremllinkedservice.updateresourceendpoint.aspx) dodano toohello [AzureMLLinkedService klasy](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuremllinkedservice.aspx).
* [LongRunningOperationInitialTimeout](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.datafactorymanagementclient.longrunningoperationinitialtimeout.aspx) i [LongRunningOperationRetryTimeout](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.datafactorymanagementclient.longrunningoperationretrytimeout.aspx) właściwości zostały dodane toohello [DataFactoryManagementClient](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.datafactorymanagementclient.aspx) klasy.
* Zezwalaj na konfigurację hello przekroczeń limitu czasu dla klienta wywołania toohello usługi fabryka danych.

## <a name="version-410"></a>Wersja 4.1.0
### <a name="feature-additions"></a>Dodawanie funkcji
* Witaj następujących typów połączonych usług zostały dodane:
  * [AzureDataLakeStoreLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx)
  * [AzureDataLakeAnalyticsLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx)
* Dodano Hello następujące typy działań:
  * [DataLakeAnalyticsUSQLActivity](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datalakeanalyticsusqlactivity.aspx)
* dodano następujące typy obiektów dataset Hello:
  * [AzureDataLakeStoreDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestoredataset.aspx)
* Witaj następujące typy źródłowy i odbiorczy dla aktywności kopiowania zostały dodane:
  * [AzureDataLakeStoreSource](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestoresource.aspx)
  * [AzureDataLakeStoreSink](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestoresink.aspx)

## <a name="version-401"></a>Wersja 4.0.1
### <a name="breaking-changes"></a>Fundamentalne zmiany
Zmieniono Hello następujące klasy. nowe nazwy Hello sprzed hello oryginalnej nazwy klas 4.0.0 wersji.

| Nazwa w 4.0.0 | Nazwa w 4.0.1 |
|:--- |:--- |
| AzureSqlDataWarehouseDataset |[AzureSqlDataWarehouseTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuresqldatawarehousetabledataset.aspx) |
| AzureSqlDataset |[AzureSqlTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuresqltabledataset.aspx) |
| AzureDataset |[AzureTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuretabledataset.aspx) |
| OracleDataset |[OracleTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.oracletabledataset.aspx) |
| RelationalDataset |[RelationalTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.relationaltabledataset.aspx) |
| SqlServerDataset |[SqlServerTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.sqlservertabledataset.aspx) |

## <a name="version-400"></a>Wersja 4.0.0
### <a name="breaking-changes"></a>Fundamentalne zmiany
* Zmieniono Hello następujących klas/interfejsów.

| Stara nazwa | Nowa nazwa |
|:--- |:--- |
| ITableOperations |[IDatasetOperations](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.idatasetoperations.aspx) |
| Tabela |[Zestaw danych](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.dataset.aspx) |
| TableProperties |[DatasetProperties](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetproperties.aspx) |
| TableTypeProprerties |[DatasetTypeProperties](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasettypeproperties.aspx) |
| TableCreateOrUpdateParameters |[DatasetCreateOrUpdateParameters](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetcreateorupdateparameters.aspx) |
| TableCreateOrUpdateResponse |[DatasetCreateOrUpdateResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetcreateorupdateresponse.aspx) |
| TableGetResponse |[DatasetGetResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetgetresponse.aspx) |
| TableListResponse |[DatasetListResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetlistresponse.aspx) |
| CreateOrUpdateWithRawJsonContentParameters |[DatasetCreateOrUpdateWithRawJsonContentParameters](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetcreateorupdatewithrawjsoncontentparameters.aspx) |

* Witaj **listy** metody zwracają teraz wyników stronicowania. Jeśli odpowiedź na powitania zawiera niepusty **NextLink** właściwość, powitania klienta aplikacji musi toocontinue pobrano hello następnej strony, dopóki wszystkie strony są zwracane.  Oto przykład:

    ```csharp
    PipelineListResponse response = client.Pipelines.List("ResourceGroupName", "DataFactoryName");
    var pipelines = new List<Pipeline>(response.Pipelines);

    string nextLink = response.NextLink;
    while (!string.IsNullOrEmpty(nextLink))
    {
        PipelineListResponse nextResponse = client.Pipelines.ListNext(nextLink);
        pipelines.AddRange(nextResponse.Pipelines);

        nextLink = nextResponse.NextLink;
    }
    ```
* **Lista** potoku interfejsu API zwraca tylko hello podsumowania potoku zamiast szczegółowych informacji. Na przykład działania w potoku podsumowanie zawierać tylko nazwę i typ.

### <a name="feature-additions"></a>Dodawanie funkcji
* Witaj [SqlDWSink](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.sqldwsink.aspx) klasa obsługuje dwie nowe właściwości **SliceIdentifierColumnName** i **SqlWriterCleanupScript**, toosupport idempotentności kopiowania tooAzure danych SQL Magazyn. Zobacz hello [magazyn danych SQL Azure](data-factory-azure-sql-data-warehouse-connector.md) artykułu, aby uzyskać więcej informacji o tych właściwościach.
* Obsługujemy teraz uruchamiania procedury składowanej usługi Azure SQL Database i Azure SQL Data Warehouse źródła jako część hello działanie kopiowania. Witaj [SqlSource](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.sqlsource.aspx) i [SqlDWSource](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.sqldwsource.aspx) klasy mają hello następujące właściwości: **SqlReaderStoredProcedureName** i **StoredProcedureParameters** . Zobacz hello [bazy danych SQL Azure](data-factory-azure-sql-connector.md#sqlsource) i [magazyn danych SQL Azure](data-factory-azure-sql-data-warehouse-connector.md#sqldwsource) artykuły w witrynie Azure.com, aby uzyskać więcej informacji o tych właściwościach.  
