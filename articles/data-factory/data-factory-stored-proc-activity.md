---
title: "aaaSQL działania dotyczącego procedury składowanej serwera"
description: "Dowiedz się, jak używasz tooinvoke programu SQL Server działania dotyczącego procedury składowanej hello procedurę przechowywaną w bazie danych SQL Azure lub usługi Azure SQL Data Warehouse z potoku fabryki danych."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1c46ed69-4049-44ec-9b46-e90e964a4a8e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: spelluru
ms.openlocfilehash: 9116f80eefc59d95e866b2ba1de2feb1bdc4b1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sql-server-stored-procedure-activity"></a>Działanie procedury przechowywane programu SQL Server
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Działanie gałęzi](data-factory-hive-activity.md) 
> * [Działanie pig](data-factory-pig-activity.md)
> * [Działania MapReduce](data-factory-map-reduce.md)
> * [Działaniu przesyłania strumieniowego usługi Hadoop](data-factory-hadoop-streaming-activity.md)
> * [Działanie Spark](data-factory-spark.md)
> * [Działanie wykonywania wsadowego w usłudze Machine Learning](data-factory-azure-ml-batch-execution-activity.md)
> * [Działania aktualizowania zasobów w usłudze Machine Learning](data-factory-azure-ml-update-resource-activity.md)
> * [Działania procedur składowanych](data-factory-stored-proc-activity.md)
> * [Działania języka U-SQL usługi Data Lake Analytics](data-factory-usql-activity.md)
> * [Działania niestandardowe .NET](data-factory-use-custom-activities.md)

## <a name="overview"></a>Omówienie
Użyj działania przekształcania danych w fabryce danych [potoku](data-factory-create-pipelines.md) tootransform i przetwarzanie danych pierwotnych do przewidywania i szczegółowych informacji. Witaj działania dotyczącego procedury składowanej jest jednym z hello transformacji działania, które obsługuje fabryki danych. W tym artykule opiera się na powitania [działań przekształcania danych](data-factory-data-transformation-activities.md) artykułu, który przedstawia ogólny przegląd transformacji danych i działań przekształcania hello obsługiwany w fabryce danych.

Program hello tooinvoke działania dotyczącego procedury składowanej procedury składowanej w jednym z hello następujące dane są przechowywane w przedsiębiorstwie lub na maszynie wirtualnej platformy Azure (VM): 

- Usługa Azure SQL Database
- Azure SQL Data Warehouse
- Baza danych programu SQL Server.  Jeśli używasz programu SQL Server, należy zainstalować brama zarządzania danymi na powitania, które same komputera, czy hosty hello bazy danych lub na osobnym komputerze, który ma toohello dostępu do bazy danych. Brama zarządzania danymi jest składnik, który nawiązuje połączenie danych źródeł na lokalnym/na maszynie Wirtualnej platformy Azure z usługami w chmurze w sposób bezpieczny i zarządzanie nimi. Zobacz [brama zarządzania danymi](data-factory-data-management-gateway.md) artykułu, aby uzyskać szczegółowe informacje.

> [!IMPORTANT]
> Podczas kopiowania danych do usługi Azure SQL Database lub SQL Server, można skonfigurować hello **SqlSink** w tooinvoke działania kopiowania procedury składowanej przy użyciu hello **sqlWriterStoredProcedureName** właściwości. Aby uzyskać więcej informacji, zobacz [wywołaj procedurę składowaną z działania kopiowania](data-factory-invoke-stored-procedure-from-copy-activity.md). Aby uzyskać szczegółowe informacje dotyczące właściwości hello, zobacz następujące artykuły łącznika: [bazy danych SQL Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [programu SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties). Wywoływanie procedury składowanej podczas kopiowania danych do usługi Azure SQL Data Warehouse przy użyciu aktywność kopiowania nie jest obsługiwane. Jednak hello przechowywane procedury działania tooinvoke procedury składowanej można użyć w usłudze SQL Data Warehouse. 
>  
> Podczas kopiowania danych z bazy danych SQL Azure lub programu SQL Server lub magazyn danych SQL Azure, możesz skonfigurować **SqlSource** w tooinvoke działania kopiowania danych tooread procedurę składowaną z hello źródłowej bazy danych przy użyciu hello  **sqlReaderStoredProcedureName** właściwości. Aby uzyskać więcej informacji, zobacz następujące artykuły łącznika hello: [bazy danych SQL Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [programu SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [magazyn danych SQL Azure](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)          


następujące wskazówki używa Hello hello działania dotyczącego procedury składowanej w potoku tooinvoke procedurę przechowywaną w bazie danych Azure SQL. 

## <a name="walkthrough"></a>Przewodnik
### <a name="sample-table-and-stored-procedure"></a>Przykładowa tabela i procedury składowanej
1. Utwórz następujące hello **tabeli** w bazie danych SQL Azure przy użyciu programu SQL Server Management Studio lub innych narzędzi potrafisz. Kolumna datetimestamp Hello jest hello Data i godzina, o których wygenerowano hello odpowiedni identyfikator.

    ```SQL
    CREATE TABLE dbo.sampletable
    (
        Id uniqueidentifier,
        datetimestamp nvarchar(127)
    )
    GO

    CREATE CLUSTERED INDEX ClusteredID ON dbo.sampletable(Id);
    GO
    ```
    Identyfikator jest unikatowy hello zidentyfikowane i kolumny datetimestamp hello jest hello Data i godzina, o których wygenerowano hello odpowiedni identyfikator.
    
    ![Dane przykładowe](./media/data-factory-stored-proc-activity/sample-data.png)

    W tym przykładzie procedury przechowywane hello jest baza danych SQL Azure. Jeśli hello procedury składowanej magazyn danych SQL Azure i bazy danych serwera SQL, podejście hello jest podobne. Dla bazy danych programu SQL Server, należy zainstalować [brama zarządzania danymi](data-factory-data-management-gateway.md).
2. Utwórz następujące hello **procedury składowanej** która wstawia dane do toohello **sampletable**.

    ```SQL
    CREATE PROCEDURE sp_sample @DateTime nvarchar(127)
    AS

    BEGIN
        INSERT INTO [sampletable]
        VALUES (newid(), @DateTime)
    END
    ```

   > [!IMPORTANT]
   > **Nazwa** i **wielkości liter** z hello parametr (DateTime w tym przykładzie) musi być zgodna z parametr określony w potoku hello/aktywność JSON. W definicji procedury składowanej hello, upewnij się, że  **@**  służy jako prefiksu dla parametru hello.

### <a name="create-a-data-factory"></a>Tworzenie fabryki danych
1. Zaloguj się za[portalu Azure](https://portal.azure.com/).
2. Kliknij przycisk **nowy** w menu po lewej stronie powitania kliknij **analizy i analiza**i kliknij przycisk **fabryki danych**.

    ![Nowa fabryka danych](media/data-factory-stored-proc-activity/new-data-factory.png)    
3. W hello **nowa fabryka danych** bloku, wprowadź **SProcDF** dla hello nazwy. Nazwy fabryki danych Azure są **unikatowych**. Należy tooprefix hello nazwa fabryki danych hello nazwą użytkownika, po pomyślnym utworzeniu hello tooenable hello fabryki.

   ![Nowa fabryka danych](media/data-factory-stored-proc-activity/new-data-factory-blade.png)         
4. Wybierz użytkownika **subskrypcji platformy Azure**.
5. Aby uzyskać **grupy zasobów**, wykonaj jedną z hello następujące kroki:
   1. Kliknij przycisk **Utwórz nowy** , a następnie wprowadź nazwę grupy zasobów hello.
   2. Kliknij przycisk **Użyj istniejącego** i wybierz istniejącą grupę zasobów.  
6. Wybierz hello **lokalizacji** hello fabryki danych.
7. Wybierz **toodashboard numeru Pin** dzięki czemu można zobaczyć fabryki danych hello na pulpicie nawigacyjnym hello następnym zalogowaniu.
8. Kliknij przycisk **Utwórz** na powitania **nowa fabryka danych** bloku.
9. Zobacz hello fabryki danych tworzona w hello **pulpitu nawigacyjnego** z hello portalu Azure. Po hello fabryki danych został utworzony pomyślnie, zobacz strony fabryki danych hello, który umożliwia hello zawartość hello fabryki danych.

   ![Strona główna fabryki danych](media/data-factory-stored-proc-activity/data-factory-home-page.png)

### <a name="create-an-azure-sql-linked-service"></a>Tworzenie usługi SQL Azure połączone
Po utworzeniu hello fabryki danych, możesz utworzyć Azure połączoną usługą SQL łączącą bazy danych Azure SQL, zawierającą hello sampletable tabeli i sp_sample przechowywane procedury, tooyour fabryki danych.

1. Kliknij przycisk **tworzenie i wdrażanie** na powitania **fabryki danych** bloku **SProcDF** toolaunch hello Edytor fabryki danych.
2. Kliknij przycisk **nowy magazyn danych** hello pasek poleceń i wybierz **bazy danych SQL Azure**. Powinny pojawić się, że hello skryptu JSON do tworzenia usługi Azure SQL połączonej usługi w edytorze hello.

   ![Nowy magazyn danych](media/data-factory-stored-proc-activity/new-data-store.png)
3. W hello skryptu JSON wprowadź następujące zmiany hello:

   1. Zastąp `<servername>` o nazwie powitania serwera bazy danych SQL Azure.
   2. Zastąp `<databasename>` z hello bazy danych, w której utworzono tabelę hello i hello procedury składowanej.
   3. Zastąp `<username@servername>` z hello konta użytkownika, które ma toohello dostępu do bazy danych.
   4. Zastąp `<password>` hello hasła dla konta użytkownika hello.

      ![Nowy magazyn danych](media/data-factory-stored-proc-activity/azure-sql-linked-service.png)
4. toodeploy hello połączonej usługi, kliknij przycisk **Wdróż** na powitania paska poleceń. Upewnij się, że widoczne hello AzureSqlLinkedService w drzewie hello wyświetlić powitania po lewej stronie.

    ![Widok drzewa połączonej usługi](media/data-factory-stored-proc-activity/tree-view.png)

### <a name="create-an-output-dataset"></a>Tworzenie wyjściowego zestawu danych
Należy określić wyjściowy zestaw danych działania procedura składowana nawet, jeśli procedury składowanej hello nie zwraca żadnych danych. Wynika to z jego hello wyjściowy zestaw danych, które dyski hello harmonogram działania hello (częstotliwość hello działanie jest uruchamiane — co godzinę, codziennie, itp.). Witaj wyjściowego zestawu danych musi używać **połączona usługa** przywołujący tooan bazy danych SQL Azure lub usługi Azure SQL Data Warehouse lub baza danych SQL Server w której ma zostać hello toorun procedury składowanej. Witaj wyjściowego zestawu danych może służyć jako wynik hello toopass sposób hello przechowywane procedury dla dalszego przetwarzania przez inne działanie ([łańcucha działania](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) w potoku hello. Jednak automatycznie fabryki danych nie zapisuje dane wyjściowe hello toothis procedury przechowywanej zestawu danych. Jest to hello tej tabeli SQL tooa zapisy hello punktów zestawu danych wyjściowych do procedury składowanej. W niektórych przypadkach może być hello wyjściowy zestaw danych **fikcyjny dataset** (procedury przechowywanej zestawu danych, który wskazuje tooa tabeli, która naprawdę nie przechowuje dane wyjściowe hello). Ten fikcyjny zestaw danych jest używany tylko toospecify hello harmonogramu uruchamiania hello przechowywane procedury działania. 

1. Kliknij przycisk **... Więcej** na powitania narzędzi, kliknij przycisk **nowy zestaw danych**i kliknij przycisk **Azure SQL**. **Nowy zestaw danych** w poleceniu hello paska i wybierz pozycję **Azure SQL**.

    ![Widok drzewa połączonej usługi](media/data-factory-stored-proc-activity/new-dataset.png)
2. Skopiuj/Wklej hello następującego skryptu JSON w edytorze JSON toohello.

    ```JSON
    {                
        "name": "sprocsampleout",
        "properties": {
            "type": "AzureSqlTable",
            "linkedServiceName": "AzureSqlLinkedService",
            "typeProperties": {
                "tableName": "sampletable"
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```
3. toodeploy hello zestawu danych, kliknij przycisk **Wdróż** na powitania paska poleceń. Upewnij się, że hello dataset w widoku drzewa hello jest wyświetlany.

    ![Widok drzewa z połączonych usług](media/data-factory-stored-proc-activity/tree-view-2.png)

### <a name="create-a-pipeline-with-sqlserverstoredprocedure-activity"></a>Utworzyć potok z działaniem SqlServerStoredProcedure
Teraz Utwórzmy potoku z działania procedury składowanej. 

Zwróć uwagę hello następujące właściwości: 

- Witaj **typu** właściwość jest ustawiona zbyt**SqlServerStoredProcedure**. 
- Witaj **storedProcedureName** w typie właściwości ustawiono zbyt**sp_sample** (procedury składowanej nazwy hello).
- Witaj **storedProcedureParameters** sekcja zawiera jeden parametr o nazwie **wartości daty i godziny**. Nazwa i wielkość liter w wyrazie parametru hello w formacie JSON muszą być zgodne, nazwa hello i wielkość liter w wyrazie hello parametru w definicji procedury hello przechowywane. Jeśli należy przekazać wartość null dla parametru, należy użyć składni hello: `"param1": null` (tylko małe litery).
 
1. Kliknij przycisk **... Więcej** hello pasek poleceń i kliknij przycisk **nowy potok**.
2. Skopiuj i Wklej powitania po fragment kodu JSON:   

    ```JSON
    {
        "name": "SprocActivitySamplePipeline",
        "properties": {
            "activities": [
                {
                    "type": "SqlServerStoredProcedure",
                    "typeProperties": {
                        "storedProcedureName": "sp_sample",
                        "storedProcedureParameters": {
                            "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)"
                        }
                    },
                    "outputs": [
                        {
                            "name": "sprocsampleout"
                        }
                    ],
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                    },
                    "name": "SprocActivitySample"
                }
            ],
             "start": "2017-04-02T00:00:00Z",
             "end": "2017-04-02T05:00:00Z",
            "isPaused": false
        }
    }
    ```
3. toodeploy hello potoku, kliknij przycisk **Wdróż** na powitania narzędzi.  

### <a name="monitor-hello-pipeline"></a>Monitor hello potoku
1. Kliknij przycisk **X** tooclose Edytor fabryki danych bloków toonavigate kopii toohello bloku fabryki danych i kliknij przycisk **Diagram**.

    ![Diagram kafelka](media/data-factory-stored-proc-activity/data-factory-diagram-tile.png)
2. W hello **widoku diagramu**, zobacz Omówienie potoki hello i używać zestawów danych w tym samouczku.

    ![Diagram kafelka](media/data-factory-stored-proc-activity/data-factory-diagram-view.png)
3. Hello widoku diagramu, kliknij dwukrotnie hello dataset `sprocsampleout`. Zostanie wyświetlony wycinków hello w stanie gotowe. Powinien istnieć pięć wycinków, ponieważ wycinek jest tworzone dla każdej godziny między hello godzinę rozpoczęcia i zakończenia z hello JSON.

    ![Diagram kafelka](media/data-factory-stored-proc-activity/data-factory-slices.png)
4. Gdy wycinek jest **gotowe** stanu, uruchom `select * from sampletable` zapytania dotyczącego hello tooverify bazy danych Azure SQL, która hello danych została umieszczona w tabeli toohello hello przechowywane procedury.

   ![dane wyjściowe](./media/data-factory-stored-proc-activity/output.png)

   Zobacz [potoku hello Monitor](data-factory-monitor-manage-pipelines.md) szczegółowe informacje o monitorowaniu potoki fabryki danych Azure.  


## <a name="specify-an-input-dataset"></a>Określ zestaw danych wejściowych
W przewodniku hello działania procedury składowanej nie ma żadnych wejściowe zestawy danych. Jeśli określisz zestaw danych wejściowych, hello działania procedury składowanej nie działa do momentu hello wejściowego zestawu danych jest dostępny (w stanie gotowe). Hello zestawu danych może być zewnętrzny zestaw danych (który nie jest generowany przez innego działania w hello tego samego potoku) lub wewnętrzny zestawu danych, który jest generowany przez działanie w strumieniu przychodzącym (hello działania wykonywane przed tego działania). Można określić wiele zestawów wejściowych danych hello przechowywane procedury działania. Jeśli tak zrobisz hello działania procedury składowanej działa tylko wtedy, gdy wszystkie fragmenty wejściowy zestaw danych hello są dostępne (w stanie gotowe). Witaj wejściowy zestaw danych nie mogą być używane w procedurze hello przechowywane jako parametr. Jest tylko zależności hello toocheck używane przed początkowy hello przechowywane procedury działania.

## <a name="chaining-with-other-activities"></a>Łańcuch serwerów z innymi działaniami
Jeśli toochain działania nadrzędnego tego działania, należy określić hello dane wyjściowe działania nadrzędnego hello jako dane wejściowe tego działania. Po wykonaniu tej hello działania procedury składowanej nie jest możliwe dopiero po zakończeniu działania nadrzędnego hello i hello wyjściowy zestaw danych działania nadrzędnego hello jest dostępna (w stanie gotowe). Wyjściowe zestawy danych z wielu działań nadrzędnego może służyć jako wejściowe zestawy danych hello przechowywane procedury działania. Po wykonaniu tej czynności hello przechowywane działania procedura działa tylko wtedy, gdy wszystkie fragmenty wejściowy zestaw danych hello są dostępne.  

Poniższy przykład hello, hello dane wyjściowe działania kopiowania hello jest: OutputDataset, która jest wartością wejściową hello przechowywane procedury działania. W związku z tym hello działania procedury składowanej nie uruchamia dopiero po zakończeniu działania kopiowania hello i hello OutputDataset jest dostępny (w stanie gotowe). Jeśli określisz wiele zestawów danych wejściowych hello działania procedury składowanej nie działa, dopóki wszystkie fragmenty wejściowy zestaw danych hello są dostępne (w stanie gotowe). Witaj wejściowe zestawy danych nie można użyć bezpośrednio jako parametry toohello przechowywane procedury działania. 

Aby uzyskać więcej informacji na tworzenie łańcucha działań, zobacz [wielu działań w potoku](data-factory-create-pipelines.md#multiple-activities-in-a-pipeline)

```json
{

    "name": "ADFTutorialPipeline",
    "properties": {
        "description": "Copy data from a blob tooblob",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [ { "name": "InputDataset" } ],
                "outputs": [ { "name": "OutputDataset" } ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst"
                },
                "name": "CopyFromBlobToSQL"
            },
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "SPSproc"
                },
                "inputs": [ { "name": "OutputDataset" } ],
                "outputs": [ { "name": "SQLOutputDataset" } ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "RunStoredProcedure"
            }

        ],
        "start": "2017-04-12T00:00:00Z",
        "end": "2017-04-13T00:00:00Z",
        "isPaused": false,
    }
}
```

Podobnie, toolink hello magazynu procedury działania o **działania podrzędne** (działania hello, uruchamiane po hello procedury składowanej zakończeniu działania), określ hello wyjściowy zestaw danych działania procedura hello przechowywane jako dane wejściowe działania podrzędne hello w potoku hello.

> [!IMPORTANT]
> Podczas kopiowania danych do usługi Azure SQL Database lub SQL Server, można skonfigurować hello **SqlSink** w tooinvoke działania kopiowania procedury składowanej przy użyciu hello **sqlWriterStoredProcedureName** właściwości. Aby uzyskać więcej informacji, zobacz [wywołaj procedurę składowaną z działania kopiowania](data-factory-invoke-stored-procedure-from-copy-activity.md). Szczegółowe informacje o właściwości hello, zobacz następujące artykuły łącznika hello: [bazy danych SQL Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [programu SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).
>  
> Podczas kopiowania danych z bazy danych SQL Azure lub programu SQL Server lub magazyn danych SQL Azure, możesz skonfigurować **SqlSource** w tooinvoke działania kopiowania danych tooread procedurę składowaną z hello źródłowej bazy danych przy użyciu hello  **sqlReaderStoredProcedureName** właściwości. Aby uzyskać więcej informacji, zobacz następujące artykuły łącznika hello: [bazy danych SQL Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [programu SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [magazyn danych SQL Azure](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)          

## <a name="json-format"></a>JSON format
Oto formatu JSON hello określających działania dotyczącego procedury składowanej:

```JSON
{
    "name": "SQLSPROCActivity",
    "description": "description",
    "type": "SqlServerStoredProcedure",
    "inputs":  [ { "name": "inputtable"  } ],
    "outputs":  [ { "name": "outputtable" } ],
    "typeProperties":
    {
        "storedProcedureName": "<name of hello stored procedure>",
        "storedProcedureParameters":  
        {
            "param1": "param1Value"
            …
        }
    }
}
```

Witaj w poniższej tabeli opisano te właściwości JSON:

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| name | Nazwa działania hello |Tak |
| description |Tekst opisujący, jakie działanie hello jest używany dla |Nie |
| type | Musi mieć wartość: **SqlServerStoredProcedure** | Tak |
| Dane wejściowe | Opcjonalny. Jeśli określisz wejściowy zestaw danych, musi być dostępny (w stanie "Gotowe") dla hello przechowywane procedury toorun działania. Witaj wejściowy zestaw danych nie mogą być używane w procedurze hello przechowywane jako parametr. Jest tylko zależności hello toocheck używane przed początkowy hello przechowywane procedury działania. |Nie |
| dane wyjściowe | Należy określić zestaw danych wyjściowych dla działania procedury składowanej. Wyjściowy zestaw danych określa hello **harmonogram** hello przechowywane procedury działania (co godzinę, co tydzień, co miesiąc, itp.). <br/><br/>Witaj wyjściowego zestawu danych musi używać **połączona usługa** przywołujący tooan bazy danych SQL Azure lub usługi Azure SQL Data Warehouse lub baza danych SQL Server w której ma zostać hello toorun procedury składowanej. <br/><br/>Witaj wyjściowego zestawu danych może służyć jako wynik hello toopass sposób hello przechowywane procedury dla dalszego przetwarzania przez inne działanie ([łańcucha działania](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) w potoku hello. Jednak automatycznie fabryki danych nie zapisuje dane wyjściowe hello toothis procedury przechowywanej zestawu danych. Jest to hello tej tabeli SQL tooa zapisy hello punktów zestawu danych wyjściowych do procedury składowanej. <br/><br/>W niektórych przypadkach może być hello wyjściowy zestaw danych **fikcyjny dataset**, który jest używany tylko toospecify hello harmonogramu uruchamiania hello przechowywane procedury działania. |Tak |
| storedProcedureName |Określ nazwę hello hello przechowywane procedury hello bazy danych Azure SQL lub w bazie danych magazynu danych SQL Azure lub programu SQL Server, reprezentowanego przez hello połączone usługi, która hello używa tabeli danych wyjściowych. |Tak |
| storedProcedureParameters |Określ wartości dla parametrów procedury składowanej. Jeśli potrzebujesz toopass wartości null dla parametru, należy użyć składni hello: "param1": wartość null (małe litery). Zobacz powitania po toolearn próbki o korzystaniu z tej właściwości. |Nie |

## <a name="passing-a-static-value"></a>Przekazywanie wartości statycznej
Teraz załóżmy należy rozważyć dodanie inną kolumnę o nazwie "Scenariusza" w tabeli hello zawierające wartości statycznej o nazwie "Próbki dokumentu".

![Przykładowe dane 2](./media/data-factory-stored-proc-activity/sample-data-2.png)

**Tabela:**

```SQL
CREATE TABLE dbo.sampletable2
(
    Id uniqueidentifier,
    datetimestamp nvarchar(127),
    scenario nvarchar(127)
)
GO

CREATE CLUSTERED INDEX ClusteredID ON dbo.sampletable2(Id);
```

**Procedura składowana:**

```SQL
CREATE PROCEDURE sp_sample2 @DateTime nvarchar(127) , @Scenario nvarchar(127)

AS

BEGIN
    INSERT INTO [sampletable2]
    VALUES (newid(), @DateTime, @Scenario)
END
```

Teraz, Przekaż hello **scenariusza** wartość parametru i hello z hello przechowywane procedury działania. Witaj **typeProperties** części hello poprzedzających próbki prawdopodobnie powitania po fragment kodu:

```JSON
"typeProperties":
{
    "storedProcedureName": "sp_sample",
    "storedProcedureParameters":
    {
        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)",
        "Scenario": "Document sample"
    }
}
```

**Zestaw danych z fabryki danych:**

```JSON
{
    "name": "sprocsampleout2",
    "properties": {
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "sampletable2"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

**Potok fabryki danych**

```JSON
{
    "name": "SprocActivitySamplePipeline2",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_sample2",
                    "storedProcedureParameters": {
                        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)",
                        "Scenario": "Document sample"
                    }
                },
                "outputs": [
                    {
                        "name": "sprocsampleout2"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "SprocActivitySample"
            }
        ],
        "start": "2016-10-02T00:00:00Z",
        "end": "2016-10-02T05:00:00Z"
    }
}
```