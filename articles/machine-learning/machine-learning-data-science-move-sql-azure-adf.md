---
title: "aaaMove danych z lokalnego programu SQL Server tooSQL Azure z fabryką danych Azure | Dokumentacja firmy Microsoft"
description: "Skonfiguruj potok fabryki danych AZURE, który Redaguj dwa działania migracji danych, które razem przenoszenia danych w trybie dziennym między bazami danych lokalnych i w chmurze hello."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 36837c83-2015-48be-b850-c4346aa5ae8a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 7f7e78c7a84a259539221d3235b76bb5a3cf9866
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-on-premises-sql-server-toosql-azure-with-azure-data-factory"></a>Przenoszenia danych z lokalnego tooSQL serwera SQL Azure z fabryką danych Azure
W tym temacie przedstawiono, jak dane toomove z lokalnej bazy danych SQL Server tooa bazy danych SQL Azure za pomocą usługi Azure Blob Storage za pomocą hello fabryki danych Azure (ADF).

Dla tabeli, która zawiera podsumowanie różne opcje przenoszenia danych tooan bazy danych SQL Azure, zobacz [Przenieś tooan danych bazy danych SQL Azure dla usługi Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).

## <a name="intro"></a>Wprowadzenie: Co to jest ADF i kiedy ma być używane toomigrate danych?
Fabryka danych Azure to usługa integracji pełni zarządzanych danych oparte na chmurze, która organizuje i zautomatyzować przepływ hello i przekształcania danych. Witaj klucza w modelu ADF hello dotyczy potoku. Potok to logiczne grupowanie działań, z których każdy definiuje tooperform akcje hello na powitania danych zawartych w zestawach danych. Połączone usługi są używane toodefine hello informacji potrzebnych do zasobów danych toohello tooconnect fabryki danych.

Z fabryki danych AZURE istniejące usługi przetwarzania danych mogą być składane w potokach danych, które są wysokiej dostępności i zarządzane w chmurze hello. Potoki tych danych może zostać zaplanowane tooingest, przygotowanie, przekształcenie, analizowanie i publikować dane, a ADF zarządza i organizuje dane złożone hello i przetwarzania zależności. Można hello szybkie wbudowanych i wdrożone w chmury, łączenie coraz lokalnych rozwiązań i źródeł danych w chmurze.

Należy rozważyć użycie ADF:

* Po toobe potrzeb stale migracji w scenariuszu hybrydowym, który uzyskuje dostęp zarówno do danych lokalnych i w chmurze zasobów
* gdy danych hello jest nietransakcyjnego lub toobe potrzeb modyfikacji lub mieć logiki biznesowej dodać tooit, gdy migrowane.

ADF umożliwia hello planowania i monitorowania zadań przy użyciu prostych skryptów JSON, które zarządzają hello przepływu danych w regularnych odstępach czasu. ADF ma również innych funkcji, takich jak obsługa złożonych operacji. Aby uzyskać więcej informacji dotyczących fabryki danych AZURE, zobacz dokumentację hello na [fabryki danych Azure (ADF)](https://azure.microsoft.com/services/data-factory/).

## <a name="scenario"></a>Witaj scenariusza
Skonfigurowanie potok fabryki danych AZURE, który Redaguj dwóch działań migracji danych. Razem one przenoszenie danych w trybie dziennym między lokalną bazą danych SQL i bazy danych SQL Azure w chmurze hello. dwa działania Hello są:

* Kopiowanie danych z tooan bazy danych programu SQL Server lokalne konto magazynu obiektów Blob Azure
* Kopiowanie danych z tooan konta magazynu obiektów Blob Azure hello bazy danych SQL Azure.

> [!NOTE]
> Witaj kroki opisane w tym miejscu zostały dostosowane z hello bardziej szczegółowe samouczek dostarczone przez zespół ADF hello: [przenoszenie danych między lokalnych źródeł i w chmurze z brama zarządzania danymi](../data-factory/data-factory-move-data-between-onprem-and-cloud.md) odwołuje się do toohello odpowiednich sekcjach tego tematu podano, gdy jest to konieczne.
>
>

## <a name="prereqs"></a>Wymagania wstępne
Ten samouczek zakłada, że masz:

* **Subskrypcji platformy Azure**. Jeśli nie masz subskrypcji, możesz zarejestrować się, aby uzyskać dostęp do [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).
* **Konto magazynu Azure**. Używasz konta magazynu Azure do przechowywania danych hello w tym samouczku. Jeśli nie masz konta magazynu platformy Azure, zobacz hello [Utwórz konto magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account) artykułu. Po utworzeniu konta magazynu hello, musisz mieć konto hello tooobtain się, że klucz używany tooaccess hello magazynu. Zobacz [zarządzanie kluczami dostępu do magazynu](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).
* Dostęp tooan **bazy danych SQL Azure**. Jeśli konieczne jest ustawienie bazy danych SQL Azure, hello tpoic [wprowadzenie do korzystania z bazy danych SQL Azure Microsoft ](../sql-database/sql-database-get-started.md) informacje na temat sposobu tooprovision nowe wystąpienie bazy danych SQL Azure.
* Zainstalowano i skonfigurowano **programu Azure PowerShell** lokalnie. Aby uzyskać instrukcje, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).

> [!NOTE]
> Ta procedura wykorzystuje hello [portalu Azure](https://portal.azure.com/).
>
>

## <a name="upload-data"></a>Przekazywanie hello danych tooyour lokalnego programu SQL Server
Używamy hello [dataset taksówki NYC](http://chriswhong.com/open-data/foil_nyc_taxi/) procesu migracji hello toodemonstrate. Witaj taksówki NYC zestaw danych jest dostępne, zgodnie z opisem w tym blogu w magazynie obiektów blob platformy Azure [danych taksówki NYC](http://www.andresmh.com/nyctaxitrips/). dane Hello ma dwa pliki, hello trip_data.csv pliku, który zawiera szczegóły podróży, oraz hello trip_far.csv pliku, który zawiera szczegółowe informacje o klasie hello płatnej w odniesieniu do każdej podróży. Przykładowe i opis te pliki znajdują się w [opis zestawu danych rund taksówki NYC](machine-learning-data-science-process-sql-walkthrough.md#dataset).

Można dostosować procedury hello podaną poniżej tooa zbiór danych użytkownika lub wykonaj kroki hello, zgodnie z opisem przy użyciu hello taksówki NYC zestawu danych. tooupload hello dataset taksówki NYC do lokalnej bazy danych programu SQL Server, wykonaj procedurę hello opisane w temacie [zbiorczego importowania danych do bazy danych serwera SQL](machine-learning-data-science-process-sql-walkthrough.md#dbload). Te instrukcje dotyczą programu SQL Server na maszynie wirtualnej platformy Azure, ale hello procedurę przekazywania toohello lokalnego programu SQL Server jest hello takie same.

## <a name="create-adf"></a>Tworzenie fabryki danych Azure
instrukcje dotyczące tworzenia nowych fabryki danych Azure i grupy zasobów w hello Hello [portalu Azure](https://portal.azure.com/) podano [tworzenie fabryki danych Azure](../data-factory/data-factory-build-your-first-pipeline-using-editor.md#create-data-factory). Nowe wystąpienie ADF nazwa hello *adfdsp* i nazwę grupy zasobów dla hello utworzony *adfdsprg*.

## <a name="install-and-configure-up-hello-data-management-gateway"></a>Instalowanie i konfigurowanie zapasowej hello brama zarządzania danymi
tooenable Twojego potoki w toowork fabryki danych Azure z lokalnym programem SQL Server należy tooadd go jako fabryki danych toohello połączonej usługi. toocreate połączonej usługi dla lokalnego programu SQL Server, należy:

* Pobierz i zainstaluj bramę zarządzania danymi firmy Microsoft na powitania na komputerze lokalnym.
* Skonfiguruj usługę hello połączone hello lokalnych danych źródła toouse hello bramy.

Brama zarządzania danymi Hello serializuje i deserializuje hello źródłowy i odbiorczy danych na komputerze hello, gdzie jest hostowana.

Aby uzyskać instrukcje dotyczące konfiguracji oraz szczegółowe informacje w bramie zarządzania danymi, zobacz [przenoszenie danych między lokalnych źródeł i w chmurze z brama zarządzania danymi](../data-factory/data-factory-move-data-between-onprem-and-cloud.md)

## <a name="adflinkedservices"></a>Tworzenie połączonej usługi tooconnect toohello zasobów danych
Połączona usługa definiuje hello informacji potrzebnych do fabryki danych Azure tooconnect tooa danych zasobów. Hello procedury krok po kroku tworzenia połączonych usług znajduje się w [utworzenia połączonych usług](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-linked-services).

Firma Microsoft udostępnia trzy zasoby w tym scenariuszu, dla którego połączone usługi są potrzebne.

1. [Połączona usługa dla lokalnego programu SQL Server](#adf-linked-service-onprem-sql)
2. [Połączonej usługi magazynu obiektów Blob Azure](#adf-linked-service-blob-store)
3. [Połączonej usługi bazy danych Azure SQL](#adf-linked-service-azure-sql)

### <a name="adf-linked-service-onprem-sql"></a>Połączona usługa lokalnej bazy danych SQL Server
Usługa hello połączone toocreate hello lokalnego programu SQL Server:

* Kliknij przycisk hello **magazynu danych** w strony docelowej ADF hello w klasycznym portalu Azure
* Wybierz **SQL** , a następnie wprowadź hello *username* i *hasło* poświadczeń dla hello lokalnego programu SQL Server. Należy servername hello tooenter jako **nazwa wystąpienia pełną servername ukośnik odwrotny (servername\instancename)**. Nazwa hello połączona usługa *adfonpremsql*.

### <a name="adf-linked-service-blob-store"></a>Połączona usługa obiektu blob
toocreate hello połączonej usługi dla konta magazynu obiektów Blob Azure hello:

* Kliknij przycisk hello **magazynu danych** w strony docelowej ADF hello w klasycznym portalu Azure
* Wybierz **konta magazynu Azure**
* Wprowadź hello Azure Blob Storage klucza i kontener nazwę konta. Witaj nazwy połączonej usługi *adfds*.

### <a name="adf-linked-service-azure-sql"></a>Połączonej usługi bazy danych Azure SQL
toocreate hello połączonej usługi dla bazy danych SQL Azure hello:

* Kliknij przycisk hello **magazynu danych** w strony docelowej ADF hello w klasycznym portalu Azure
* Wybierz **Azure SQL** , a następnie wprowadź hello *username* i *hasło* poświadczenia hello bazy danych SQL Azure. Witaj *username* muszą być określone jako  *user@servername* .   

## <a name="adf-tables"></a>Definiowanie i tworzenie tabel toospecify jak tooaccess hello zbiory danych
Tworzenie tabel zawierających dostępności hello zestawów danych, lokalizacji i struktura hello hello zgodnie z procedurami opartych na skryptach. Pliki w formacie JSON są używane toodefine hello tabel. Aby uzyskać więcej informacji o strukturze hello tych plików, zobacz [zestawów danych](../data-factory/data-factory-create-datasets.md).

> [!NOTE]
> Należy wykonać hello `Add-AzureAccount` polecenia cmdlet przed wykonaniem hello [AzureDataFactoryTable nowy](https://msdn.microsoft.com/library/azure/dn835096.aspx) tooconfirm polecenia cmdlet, które hello subskrypcji prawo Azure jest wybrany do wykonania polecenia hello. Aby uzyskać dokumentację tego polecenia cmdlet, zobacz [Add-AzureAccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0).
>
>

definicje Hello opartych na formacie JSON w tabelach hello Użyj hello następujące nazwy:

* Witaj **nazwy tabeli** hello lokalnego programu SQL server jest *nyctaxi_data*
* Witaj **nazwa kontenera** w hello magazynu obiektów Blob Azure jest konto *containername*  

Trzy definicje tabel są wymagane dla tego potoku ADF:

1. [SQL lokalnej tabeli](#adf-table-onprem-sql)
2. [Tabela obiektów blob](#adf-table-blob-store)
3. [SQL tabeli platformy Azure](#adf-table-azure-sql)

> [!NOTE]
> Te procedury użyj toodefine programu Azure PowerShell i Utwórz hello działania ADF. Jednak te zadania może być również wykonywane przy użyciu hello portalu Azure. Aby uzyskać więcej informacji, zobacz [utworzyć zestawy danych](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-datasets).
>
>

### <a name="adf-table-onprem-sql"></a>SQL lokalnej tabeli
Definicja tabeli Hello hello lokalnego programu SQL Server jest określony w hello następującego pliku JSON:

        {
            "name": "OnPremSQLTable",
            "properties":
            {
                "location":
                {
                "type": "OnPremisesSqlServerTableLocation",
                "tableName": "nyctaxi_data",
                "linkedServiceName": "adfonpremsql"
                },
                "availability":
                {
                "frequency": "Day",
                "interval": 1,   
                "waitOnExternal":
                {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
                }

                }
            }
        }

nazwy kolumn Hello nie były dołączane tutaj. Można wybrać podrzędna na nazwy kolumn hello przez włączenie ich w tym miejscu (Aby uzyskać szczegółowe informacje, przejrzyj hello [dokumentacji ADF](../data-factory/data-factory-data-movement-activities.md) tematu.

Skopiuj hello JSON definicji tabeli hello w pliku o nazwie *onpremtabledef.json* pliku i zapisz go tooa znane lokalizacji (tutaj zakłada, że toobe *C:\temp\onpremtabledef.json*). Tworzenie tabeli hello w ADF za hello następującego polecenia cmdlet programu Azure PowerShell:

    New-AzureDataFactoryTable -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp –File C:\temp\onpremtabledef.json


### <a name="adf-table-blob-store"></a>Tabela obiektów blob
Definicja tabeli hello hello danych wyjściowych lokalizacji obiektu blob znajduje się w następujących hello (mapuje hello pozyskanych danych z obiektu blob tooAzure lokalnych):

        {
            "name": "OutputBlobTable",
            "properties":
            {
                "location":
                {
                "type": "AzureBlobLocation",
                "folderPath": "containername",
                "format":
                {
                "type": "TextFormat",
                "columnDelimiter": "\t"
                },
                "linkedServiceName": "adfds"
                },
                "availability":
                {
                "frequency": "Day",
                "interval": 1
                }
            }
        }

Skopiuj hello JSON definicji tabeli hello w pliku o nazwie *bloboutputtabledef.json* pliku i zapisz go tooa znane lokalizacji (tutaj zakłada, że toobe *C:\temp\bloboutputtabledef.json*). Tworzenie tabeli hello w ADF za hello następującego polecenia cmdlet programu Azure PowerShell:

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\bloboutputtabledef.json  

### <a name="adf-table-azure-sq"></a>SQL tabeli platformy Azure
Definicja tabeli hello powitalne danych wyjściowych SQL Azure znajduje się w następujących hello (w tym schemacie mapuje dane hello pochodzące z obiektu blob hello):

    {
        "name": "OutputSQLAzureTable",
        "properties":
        {
            "structure":
            [
                { "name": "column1", type": "String"},
                { "name": "column2", type": "String"}                
            ],
            "location":
            {
                "type": "AzureSqlTableLocation",
                "tableName": "your_db_name",
                "linkedServiceName": "adfdssqlazure_linked_servicename"
            },
            "availability":
            {
                "frequency": "Day",
                "interval": 1            
            }
        }
    }

Skopiuj hello JSON definicji tabeli hello w pliku o nazwie *AzureSqlTable.json* pliku i zapisz go tooa znane lokalizacji (tutaj zakłada, że toobe *C:\temp\AzureSqlTable.json*). Tworzenie tabeli hello w ADF za hello następującego polecenia cmdlet programu Azure PowerShell:

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\AzureSqlTable.json  


## <a name="adf-pipeline"></a>Definiowanie i utworzyć potok hello
Określ hello działań, które należy toohello potoku i utworzyć potok hello z hello zgodnie z procedurami opartych na skryptach. Plik JSON jest używane toodefine hello potoku właściwości.

* Witaj skryptu przyjęto założenie, że hello **nazwy potoku** jest *AMLDSProcessPipeline*.
* Należy również zauważyć, że ustawiliśmy hello okresowości toobe potoku hello wykonane na codziennie podstawę i użyj hello domyślny czas wykonania zadania hello (00: 00 UTC).

> [!NOTE]
> Hello następujące procedury przy użyciu programu Azure PowerShell toodefine a utworzyć potok fabryki danych AZURE hello. Jednak to zadanie może być również wykonywane przy użyciu portalu Azure. Aby uzyskać więcej informacji, zobacz [tworzenie potoku](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-pipeline).
>
>

Przy użyciu definicji tabeli hello podane wcześniej, definicja potoku hello hello ADF jest określana w następujący sposób:

        {
            "name": "AMLDSProcessPipeline",
            "properties":
            {
                "description" : "This pipeline has one Copy activity that copies data from an on-premises SQL tooAzure blob",
                 "activities":
                [
                    {
                        "name": "CopyFromSQLtoBlob",
                        "description": "Copy data from on-premises SQL server tooblob",     
                        "type": "CopyActivity",
                        "inputs": [ {"name": "OnPremSQLTable"} ],
                        "outputs": [ {"name": "OutputBlobTable"} ],
                        "transformation":
                        {
                            "source":
                            {                               
                                "type": "SqlSource",
                                "sqlReaderQuery": "select * from nyctaxi_data"
                            },
                            "sink":
                            {
                                "type": "BlobSink"
                            }   
                        },
                        "Policy":
                        {
                            "concurrency": 3,
                            "executionPriorityOrder": "NewestFirst",
                            "style": "StartOfInterval",
                            "retry": 0,
                            "timeout": "01:00:00"
                        }       

                     },

                    {
                        "name": "CopyFromBlobtoSQLAzure",
                        "description": "Push data tooSql Azure",        
                        "type": "CopyActivity",
                        "inputs": [ {"name": "OutputBlobTable"} ],
                        "outputs": [ {"name": "OutputSQLAzureTable"} ],
                        "transformation":
                        {
                            "source":
                            {                               
                                "type": "BlobSource"
                            },
                            "sink":
                            {
                                "type": "SqlSink",
                                "WriteBatchTimeout": "00:5:00",                
                            }            
                        },
                        "Policy":
                        {
                            "concurrency": 3,
                            "executionPriorityOrder": "NewestFirst",
                            "style": "StartOfInterval",
                            "retry": 2,
                            "timeout": "02:00:00"
                        }
                     }
                ]
            }
        }

Skopiuj tej definicji JSON potoku hello w pliku o nazwie *pipelinedef.json* pliku i zapisz go tooa znane lokalizacji (w tym miejscu zakłada, że toobe *C:\temp\pipelinedef.json*). Tworzenie potoku hello w ADF z następującego polecenia cmdlet programu Azure PowerShell hello:

    New-AzureDataFactoryPipeline  -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\pipelinedef.json

Upewnij się, że można wyświetlić potoku hello na powitania wyświetlani ADF w hello klasycznego portalu Azure w następujący (po kliknięciu przycisku hello diagram)

![Potok fabryki danych AZURE](media/machine-learning-data-science-move-sql-azure-adf/DJP1kji.png)

## <a name="adf-pipeline-start"></a>Uruchom hello potoku
Obecnie można uruchomić potoku Hello przy użyciu hello następujące polecenie:

    Set-AzureDataFactoryPipelineActivePeriod -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp -StartDateTime startdateZ –EndDateTime enddateZ –Name AMLDSProcessPipeline

Witaj *datą rozpoczęcia* i *enddate* wartości parametru muszą toobe zastąpione hello rzeczywistej daty, między którymi ma hello toorun potoku.

Po potoku hello jest wykonywana, powinno być możliwe toosee hello danych będą wyświetlane w kontenerze hello wybrane dla obiektu blob hello, jeden plik na dzień.

Należy pamiętać, że nie ma możemy wykorzystać hello funkcjonalność danych toopipe ADF przyrostowo. Aby uzyskać więcej informacji na temat toodo to i inne funkcje udostępniane przez ADF, zobacz temat hello [dokumentacji ADF](https://azure.microsoft.com/services/data-factory/).
