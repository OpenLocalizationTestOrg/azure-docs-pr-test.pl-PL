---
title: aaaBuild pierwszy fabryki danych (Visual Studio) | Dokumentacja firmy Microsoft
description: "Ten samouczek zawiera instrukcje tworzenia przykładowego potoku dla usługi Azure Data Factory przy użyciu programu Visual Studio."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 7398c0c9-7a03-4628-94b3-f2aaef4a72c5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 0c5eb01b685d978d80916da0293cc2d3701b2d57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-data-factory-by-using-visual-studio"></a>Samouczek: Tworzenie fabryki danych za pomocą programu Visual Studio
> [!div class="op_single_selector" title="Tools/SDKs"]
> * [Przegląd i wymagania wstępne](data-factory-build-your-first-pipeline.md)
> * [Witryna Azure Portal](data-factory-build-your-first-pipeline-using-editor.md)
> * [Program Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [Program PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Szablon usługi Resource Manager](data-factory-build-your-first-pipeline-using-arm.md)
> * [Interfejs API REST](data-factory-build-your-first-pipeline-using-rest-api.md)

W tym samouczku przedstawiono sposób toocreate fabryki danych Azure za pomocą programu Visual Studio. Tworzenie projektu programu Visual Studio za pomocą szablonu projektu fabryki danych hello, definiowanie jednostek fabryki danych (połączone usługi, zestawy danych i potoku) w formacie JSON i następnie publikowania/wdrożyć te chmury toohello jednostek. 

Witaj potoku, w tym samouczku ma jedno działanie: **działania HDInsight Hive**. To działanie uruchamia skrypt hive w klastrze Azure HDInsight czy transformacji wejściowych danych wyjściowych tooproduce danych. potok Hello jest zaplanowane toorun po miesiącu między hello określono godziny rozpoczęcia i zakończenia. 

> [!NOTE]
> W tym samouczku nie pokazano, jak skopiować dane za pomocą usługi Azure Data Factory. Samouczek na temat danych toocopy przy użyciu fabryki danych Azure, zobacz [samouczek: kopiowanie danych z magazynu obiektów Blob tooSQL bazy danych](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> Potok może obejmować więcej niż jedno działanie. I tworzenia łańcucha dwa działania (Uruchom jedno działanie po drugim), ustawiając hello wyjściowy zestaw danych z jednego działania jako hello wejściowy zestaw danych z hello innych działań. Więcej informacji znajduje się w artykule dotyczącym [planowania i wykonywania w usłudze Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).


## <a name="walkthrough-create-and-publish-data-factory-entities"></a>Przewodnik: Tworzenie i publikowanie jednostek usługi Data Factory
Poniżej przedstawiono kroki hello, które należy wykonać w ramach tego przewodnika:

1. Utwórz dwie połączone usługi: **AzureStorageLinkedService1** i **HDInsightOnDemandLinkedService1**. 
   
    W tym samouczku wejścia i wyjścia danych dla działania hive hello są w hello tego samego magazynu obiektów Blob Azure. Możesz użyć na żądanie HDInsight klastra tooprocess istniejących danych wejściowych tooproduce danych wyjściowych. klaster usługi HDInsight na żądanie Hello jest utworzony automatycznie przez fabryki danych Azure w czasie wykonywania, gdy dane wejściowe hello jest gotowy toobe przetwarzane. Należy toolink dane są przechowywane lub oblicza tooyour fabryki danych, dzięki czemu usługi fabryka danych hello można łączyć toothem w czasie wykonywania. W związku z tym połączyć fabrykę danych toohello konto magazynu platformy Azure przy użyciu hello AzureStorageLinkedService1, a łączenie z klastrem usługi HDInsight na żądanie za pomocą hello HDInsightOnDemandLinkedService1. Podczas publikowania, należy określić nazwę hello toobe fabryki danych hello utworzony lub istniejącą fabrykę danych.  
2. Utwórz dwa zestawy danych: **InputDataset** i **OutputDataset**, które reprezentują hello wejścia/wyjścia danych przechowywanych w hello magazynu obiektów blob platformy Azure. 
   
    Te definicje zestawu danych znajdują się toohello połączoną usługą magazynu Azure utworzony w poprzednim kroku hello. Dla hello InputDataset Określ kontener obiektów blob hello (adfgetstarted) i hello folderu (inptutdata), który zawiera obiekt blob o hello danych wejściowych. Dla hello OutputDataset Określ kontener obiektów blob hello (adfgetstarted) i folderu hello (partitioneddata), który zawiera dane wyjściowe hello. Należy określić również inne właściwości, takie jak struktura, dostępność i zasady.
3. Utwórz potok o nazwie **MyFirstPipeline**. 
  
    W tym przewodniku potoku hello jest tylko jedno działanie: **działania Hive HDInsight**. To działanie przekształcania danych wejściowych tooproduce danych wyjściowych przez uruchomienie skryptu hive w klastrze usługi HDInsight na żądanie. toolearn więcej informacji na temat działania hive, zobacz [działania gałęzi](data-factory-hive-activity.md) 
4. Utwórz fabrykę danych o nazwie **DataFactoryUsingVS**. Wdrażanie hello fabryki danych i wszystkich jednostek fabryki danych (połączone usługi, tabele i hello potoku).
5. Po opublikowaniu, używane bloki portalu Azure i potoku hello toomonitor monitorowanie & aplikacji do zarządzania. 
  
### <a name="prerequisites"></a>Wymagania wstępne
1. Zapoznaj się z artykułem [— samouczek Przegląd](data-factory-build-your-first-pipeline.md) artykułu i pełne hello **wymagań wstępnych** czynności. Możesz też wybrać hello **omówienie i wymagania wstępne** opcji na liście rozwijanej hello hello top tooswitch toohello artykuł. Po ukończeniu wymagania wstępne hello przełączać artykułu wstecz toothis za pomocą **programu Visual Studio** opcji na liście rozwijanej hello.
2. toocreate wystąpienia fabryki danych, musi być członkiem hello [współautora fabryki danych](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) roli na poziomie grupy zasobów subskrypcji hello.  
3. Musi mieć zainstalowane na komputerze następujące hello:
   * Visual Studio 2013 lub Visual Studio 2015
   * Pobierz zestaw Azure SDK dla programu Visual Studio 2013 lub Visual Studio 2015. Przejdź za[strony pobierania Azure](https://azure.microsoft.com/downloads/) i kliknij przycisk **VS 2013** lub **VS 2015** w hello **.NET** sekcji.
   * Pobierz najnowszy dodatek fabryki danych Azure hello for Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) lub [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005). Można także zaktualizować hello wtyczki, wykonując następujące kroki hello: polecenie hello menu **narzędzia** -> **rozszerzenia i aktualizacje** -> **Online**  ->  **Galerii programu visual Studio** -> **narzędzia fabryki danych Microsoft Azure dla programu Visual Studio** -> **aktualizacji**.

Teraz można użyć programu Visual Studio toocreate fabryki danych Azure.

### <a name="create-visual-studio-project"></a>Tworzenie projektu programu Visual Studio
1. Uruchom program **Visual Studio 2013** lub **Visual Studio 2015**. Kliknij przycisk **pliku**, punktu zbyt**nowy**i kliknij przycisk **projektu**. Powinny pojawić się hello **nowy projekt** okno dialogowe.  
2. W hello **nowy projekt** okno dialogowe, wybierz opcję hello **DataFactory** szablonu, a następnie kliknij przycisk **pusty projekt fabryki danych**.   

    ![Okno dialogowe Nowy projekt](./media/data-factory-build-your-first-pipeline-using-vs/new-project-dialog.png)
3. Wprowadź **nazwa** dla projektu hello **lokalizacji**oraz nazwę hello **rozwiązania**i kliknij przycisk **OK**.

    ![Eksplorator rozwiązań](./media/data-factory-build-your-first-pipeline-using-vs/solution-explorer.png)

### <a name="create-linked-services"></a>Tworzenie połączonych usług
W tym kroku utworzysz dwie połączone usługi: **Azure Storage** i **HDInsight na żądanie**. 

Hello Azure Storage połączone usługi łączy fabrykę danych toohello konta usługi Azure Storage, podając informacje o połączeniu hello. Usługi fabryka danych używa hello parametrów połączenia z toohello tooconnect hello połączone ustawienia usługi Azure storage w czasie wykonywania. Ten magazyn zawiera wejściowego i danych wyjściowych do potoku hello i hello hive plik skryptu używany przez działanie hive hello. 

Z usługą HDInsight połączony na żądanie hello klastra usługi HDInsight jest tworzony automatycznie w czasie wykonywania podczas hello danych wejściowych jest gotowy tooprocessed. Witaj klastra jest usuwany po zakończeniu przetwarzania i bezczynności hello określoną ilość czasu. 

> [!NOTE]
> Aby utworzyć fabryki danych Określanie nazwy i ustawienia w czasie hello publikowania rozwiązania fabryki danych.

#### <a name="create-azure-storage-linked-service"></a>Tworzenie połączonej usługi Azure Storage
1. Kliknij prawym przyciskiem myszy **połączonych usług** w Eksploratorze rozwiązań hello za punkt**Dodaj**i kliknij przycisk **nowy element**.      
2. W hello **Dodaj nowy element** okno dialogowe, wybierz opcję **połączonej usługi magazynu Azure** hello listy i kliknij przycisk **Dodaj**.
    ![Połączona usługa Azure Storage](./media/data-factory-build-your-first-pipeline-using-vs/new-azure-storage-linked-service.png)
3. Zastąp `<accountname>` i `<accountkey>` hello nazwą konta magazynu Azure i klucza. toolearn sposób dostępu do magazynu tooget klucza, zobacz hello informacji na temat sposobu tooview, kopiowania i regenerate magazynu dostępu do kluczy w [Zarządzanie kontem magazynu](../storage/common/storage-create-storage-account.md#manage-your-storage-account).
    ![Połączona usługa Azure Storage](./media/data-factory-build-your-first-pipeline-using-vs/azure-storage-linked-service.png)
4. Zapisz hello **AzureStorageLinkedService1.json** pliku.

#### <a name="create-azure-hdinsight-linked-service"></a>Tworzenie połączonej usługi Azure HDInsight
1. W hello **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy **połączonych usług**, punktu zbyt**Dodaj**i kliknij przycisk **nowy element**.
2. Wybierz pozycję **Połączona usługa HDInsight na żądanie** i kliknij przycisk **Dodaj**.
3. Zastąp hello **JSON** z powitania po JSON:

     ```json
    {
        "name": "HDInsightOnDemandLinkedService",
        "properties": {
        "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "linkedServiceName": "AzureStorageLinkedService1"
            }
        }
    }
    ```

    Witaj Poniższa tabela zawiera opisy właściwości JSON hello używane we fragmencie hello:

    Właściwość | Opis
    -------- | ----------- 
    ClusterSize | Określa rozmiar hello hello klastra usługi HDInsight Hadoop.
    TimeToLive | Określa czas bezczynności tej hello hello klastra usługi HDInsight, przed usunięciem.
    linkedServiceName | Określa konto magazynu hello, które jest używane toostore hello dzienników, które są generowane przez klaster usługi HDInsight Hadoop. 

    > [!IMPORTANT]
    > Tworzy klaster usługi HDInsight Hello **domyślny kontener** w magazynie obiektów blob hello określone w hello JSON (linkedServiceName). Po usunięciu klastra hello HDInsight nie usunie tego kontenera. To zachowanie jest celowe. W przypadku połączonej usługi HDInsight na żądanie klaster usługi HDInsight jest tworzony przy każdym przetwarzaniu wycinka — o ile w tym momencie nie istnieje aktywny klaster (timeToLive). klaster Hello są automatycznie usuwane po zakończeniu przetwarzania hello.
    > 
    > Po przetworzeniu większej liczby wycinków w usłudze Azure Blob Storage będzie widocznych wiele kontenerów. Jeśli nie ma potrzeby do rozwiązywania problemów hello zadań, możesz toodelete ich magazynu hello tooreduce kosztów. nazwy Hello kontenery wykonaj wzorca: `adf<yourdatafactoryname>-<linkedservicename>-datetimestamp`. Użyj narzędzia takiego jak [Eksploratora magazynu](http://storageexplorer.com/) magazynu obiektów blob toodelete kontenerów w platformy Azure.

    Więcej informacji na temat właściwości kodu JSON znajduje się w artykule [Compute linked services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) (Połączone usługi na potrzeby obliczeń). 
4. Zapisz hello **HDInsightOnDemandLinkedService1.json** pliku.

### <a name="create-datasets"></a>Tworzenie zestawów danych
W tym kroku utwórz wprowadzania hello toorepresent zestawów danych i wysyłania danych do przetwarzania Hive. Te zestawy danych można znaleźć toohello **AzureStorageLinkedService1** został utworzony we wcześniejszej części tego samouczka. Witaj tooan punktów połączonej usługi konta usługi Azure Storage i zestawów danych, określ kontener, folder, nazwa pliku w magazynie hello, która przechowuje dane wejściowe i wyjściowe danych.   

#### <a name="create-input-dataset"></a>Tworzenie wejściowego zestawu danych
1. W hello **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy **tabel**, punktu zbyt**Dodaj**i kliknij przycisk **nowy element**.
2. Wybierz **obiektów Blob platformy Azure** z listy hello, Zmień nazwę hello pliku hello zbyt**InputDataSet.json**i kliknij przycisk **Dodaj**.
3. Zastąp hello **JSON** w edytorze hello z powitania po fragment kodu JSON:

    ```json
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService1",
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
    Ta Wstawka kodu JSON definiuje zestaw danych o nazwie **AzureBlobInput** reprezentujący dane wejściowe dla hello hive działania w potoku hello. Określ, że danych wejściowych hello znajduje się w kontenerze obiektów blob hello o nazwie `adfgetstarted` i hello folder o nazwie `inputdata`.

    Witaj Poniższa tabela zawiera opisy właściwości JSON hello używane we fragmencie hello:

    Właściwość | Opis |
    -------- | ----------- |
    type |Właściwość type Hello ustawiono zbyt**AzureBlob** ponieważ danych znajduje się w magazynie obiektów Blob Azure.
    linkedServiceName | Odwołuje się toohello AzureStorageLinkedService1 utworzony wcześniej.
    fileName |Ta właściwość jest opcjonalna. W przypadku pominięcia tej właściwości, pobierane są wszystkie pliki hello z hello folderPath. W takim przypadku tylko input.log hello jest przetwarzany.
    type | pliki dziennika Hello są w formacie tekstowym, więc używamy TextFormat. |
    columnDelimiter | kolumn w plikach dziennika hello są rozdzielone znakiem hello przecinkami (`,`)
    frequency/interval | tooMonth Ustaw częstotliwość i interwał wynosi 1, co oznacza, że wejściowy wycinków hello są dostępne co miesiąc.
    external | Ta właściwość ma wartość tootrue, jeśli hello danych wejściowych dla działania hello nie jest generowany przez hello potoku. Ta właściwość jest określana tylko w przypadku wejściowych zestawów danych. W przypadku hello wejściowego zestawu danych hello pierwsze działanie zawsze wartość on tootrue.
4. Zapisz hello **InputDataset.json** pliku.

#### <a name="create-output-dataset"></a>Tworzenie wyjściowego zestawu danych
Można teraz utworzyć hello wyjściowego zestawu danych toorepresent danych wyjściowych danych przechowywanych w hello magazynu obiektów Blob platformy Azure.

1. W hello **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy **tabel**, punktu zbyt**Dodaj**i kliknij przycisk **nowy element**.
2. Wybierz **obiektów Blob platformy Azure** z listy hello, Zmień nazwę hello pliku hello zbyt**OutputDataset.json**i kliknij przycisk **Dodaj**.
3. Zastąp hello **JSON** w edytorze hello z powitania po JSON:
    
    ```json
    {
        "name": "AzureBlobOutput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService1",
            "typeProperties": {
                "folderPath": "adfgetstarted/partitioneddata",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "availability": {
                "frequency": "Month",
                "interval": 1
            }
        }
    }
    ```
    fragment kodu JSON Hello definiuje zestaw danych o nazwie **AzureBlobOutput** czy reprezentuje dane wyjściowe generowane przez działanie hive hello w potoku hello danych. Określ, czy hello danych jest generowany przez działanie hive hello zostaną umieszczone dane wyjściowe w kontenerze obiektów blob hello o nazwie `adfgetstarted` i hello folder o nazwie `partitioneddata`. 
    
    Witaj **dostępności** sekcja określa, że wyjściowy zestaw danych hello jest tworzony co miesiąc. Hello wyjściowego zestawu danych dysków hello harmonogram hello potoku. potok Hello jest uruchamiane co miesiąc między jego czas rozpoczęcia i zakończenia. 

    Zobacz **utworzyć zestaw danych wejściowych hello** sekcji, aby uzyskać opis tych właściwości. Nie należy ustawiać właściwości zewnętrznych hello na wyjściowy zestaw danych, zgodnie z zestawu danych hello jest generowany przez potok hello.
4. Zapisz hello **OutputDataset.json** pliku.

### <a name="create-pipeline"></a>Tworzenie potoku
Utworzono hello połączoną usługą magazynu Azure i wejściowych i wyjściowych zestawów danych do tej pory. Teraz utworzysz potok z działaniem **HDInsightHive**. Witaj **wejściowych** gałęzi hello jest zestaw działań za**AzureBlobInput** i **dane wyjściowe** ustawiono zbyt**AzureBlobOutput**. Wycinek wejściowy zestaw danych jest dostępna co miesiąc (częstotliwość: miesiąc, interwał: 1), i wycinek danych wyjściowych hello jest tworzony co miesiąc za. 

1. W hello **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy **potoki**, punktu zbyt**Dodaj**i kliknij przycisk **nowy element.**
2. Wybierz **Hive potoku przekształcania** hello listy i kliknij przycisk **Dodaj**.
3. Zastąp hello **JSON** z następującego fragmentu hello:

    > [!IMPORTANT]
    > Zastąp `<storageaccountname>` hello nazwą konta magazynu.

    ```json
    {
        "name": "MyFirstPipeline",
        "properties": {
            "description": "My first Azure Data Factory pipeline",
            "activities": [
                {
                    "type": "HDInsightHive",
                    "typeProperties": {
                        "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                        "scriptLinkedService": "AzureStorageLinkedService1",
                        "defines": {
                            "inputtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/inputdata",
                            "partitionedtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/partitioneddata"
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
                    "scheduler": {
                        "frequency": "Month",
                        "interval": 1
                    },
                    "name": "RunSampleHiveActivity",
                    "linkedServiceName": "HDInsightOnDemandLinkedService"
                }
            ],
            "start": "2016-04-01T00:00:00Z",
            "end": "2016-04-02T00:00:00Z",
            "isPaused": false
        }
    }
    ```

    > [!IMPORTANT]
    > Zastąp `<storageaccountname>` hello nazwą konta magazynu.

    fragment kodu JSON Hello definiuje potok, który składa się z jednego działania (Hive działanie). To działanie uruchamia Hive danych wejściowych skryptu tooprocess na dane tooproduce klastra usługi HDInsight na żądanie. W sekcji działania hello kod JSON potoku hello, zobacz tylko jedno działanie w tablicy hello z typem ustawić także**HDInsightHive**. 

    W hello typu właściwości, które są tooHDInsight określonego działania Hive można określić, jakie połączoną usługą magazynu Azure ma plik skryptu hive hello, plik skryptu toohello ścieżka hello oraz pliku skryptu toohello parametrów. 

    plik skryptu Hive Hello, **partitionweblogs.hql**, są przechowywane na koncie magazynu Azure hello (określonego przez element scriptLinkedService hello), a w hello `script` folderu w kontenerze hello `adfgetstarted`.

    Witaj `defines` sekcja jest używane toospecify hello środowiska uruchomieniowego ustawień, które są przekazywane skryptu hive toohello jako wartości konfiguracji gałąź (np. `${hiveconf:inputtable}`, `${hiveconf:partitionedtable})`.

    Witaj **start** i **zakończenia** hello aktywny okres potoku hello określa właściwości hello potoku. Należy skonfigurować hello toobe zestawu danych tworzone co miesiąc, w związku z tym tylko wtedy, gdy wycinek jest generowany przez potok hello (ponieważ miesiąca hello jest taka sama w daty rozpoczęcia i zakończenia).

    W działaniu hello JSON, możesz określić, tego skryptu Hive hello zostanie uruchomiona na określony przez hello obliczeń hello **linkedServiceName** — **HDInsightOnDemandLinkedService**.
4. Zapisz hello **HiveActivity1.json** pliku.

### <a name="add-partitionweblogshql-and-inputlog-as-a-dependency"></a>Dodawanie plików partitionweblogs.hql i input.log jako zależności
1. Kliknij prawym przyciskiem myszy **zależności** w hello **Eksploratora rozwiązań** okna, wskaż zbyt**Dodaj**i kliknij przycisk **istniejący element**.  
2. Przejdź toohello **C:\ADFGettingStarted** i wybierz **partitionweblogs.hql**, **input.log** plików, a następnie kliknij przycisk **Dodaj**. Utworzona tych plików w ramach wymagań wstępnych z hello [— samouczek Przegląd](data-factory-build-your-first-pipeline.md).

Opublikowanie rozwiązania hello w następnym kroku hello hello **partitionweblogs.hql** plik jest przekazany toohello **skryptu** folderu w hello `adfgetstarted` kontenera obiektów blob.   

### <a name="publishdeploy-data-factory-entities"></a>Publikowanie/wdrażanie jednostek usługi Fabryka danych
W tym kroku należy opublikować hello fabryki danych jednostek (połączone usługi, zestawy danych i potoku) w toohello Twojego projektu usługi fabryka danych Azure. W procesie hello publikowania należy określić nazwę hello z fabryki danych. 

1. Kliknij prawym przyciskiem myszy projekt w Eksploratorze rozwiązań hello, a następnie kliknij przycisk **publikowania**.
2. Jeśli widzisz **Zaloguj tooyour konta Microsoft** okno dialogowe, wprowadź swoje poświadczenia dla konta hello subskrypcji platformy Azure, a następnie kliknij przycisk **Zaloguj**.
3. Powinny zostać wyświetlone następujące okno dialogowe hello:

   ![Okno dialogowe publikowania](./media/data-factory-build-your-first-pipeline-using-vs/publish.png)
4. W hello **fabryki danych skonfiguruj** pozycję hello następujące kroki:

    ![Publikowanie — ustawienia nowej fabryki danych](media/data-factory-build-your-first-pipeline-using-vs/publish-new-data-factory.png)

   1. Zaznacz opcję **Utwórz nową fabrykę danych**.
   2. Wprowadź unikatową **nazwa** hello fabryki danych. Na przykład: **DataFactoryUsingVS09152016**. Nazwa Hello musi być globalnie unikatowa.
   3. Wybierz subskrypcję prawym hello hello **subskrypcji** pola. 
        > [!IMPORTANT]
        > Jeśli nie ma żadnej subskrypcji. Upewnij się, czy użytkownik zalogowany przy użyciu konta administratora lub współadministratora subskrypcji hello.
   4. Wybierz hello **grupy zasobów** dla toobe fabryki danych hello utworzony.
   5. Wybierz hello **region** hello fabryki danych.
   6. Kliknij przycisk **dalej** tooswitch toohello **publikowania elementów** strony. (Naciśnij przycisk **kartę** toomove poza hello nazwę pola tooif hello **dalej** przycisk jest niedostępny.)

    > [!IMPORTANT]
    > Jeśli wystąpi błąd hello **nazwa fabryki danych "DataFactoryUsingVS" nie jest dostępna** podczas publikowania, Zmień nazwę hello (na przykład yournameDataFactoryUsingVS). Artykuł [Data Factory — Naming Rules](data-factory-naming-rules.md) (Fabryka danych — zasady nazewnictwa) zawiera zasady nazewnictwa artefaktów usługi Fabryka danych.   
1. W hello **publikowania elementów** upewnij się, że wszystkie hello fabryki danych jednostek są zaznaczone, a następnie kliknij przycisk **dalej** tooswitch toohello **Podsumowanie** strony.

    ![Strona publikowania elementów](media/data-factory-build-your-first-pipeline-using-vs/publish-items-page.png)     
2. Przejrzyj podsumowanie hello i kliknij przycisk **dalej** toostart hello wdrożenie procesu i sprawdź hello **stan wdrożenia**.

    ![Strona podsumowania](media/data-factory-build-your-first-pipeline-using-vs/summary-page.png)
3. W hello **stan wdrożenia** strony, powinien zostać wyświetlony stan hello hello procesu wdrażania. Po ukończeniu wdrażania hello, kliknij przycisk Zakończ.

Toonote ważne kwestie:

- Jeśli wystąpi błąd hello: **Ta subskrypcja nie jest zarejestrowany toouse przestrzeni nazw Microsoft.DataFactory**, wykonaj jedną z następujących hello i spróbuj ponownie opublikować:
    - W programie Azure PowerShell Uruchom hello następujące polecenia tooregister hello fabryki danych dostawcy.
        ```PowerShell   
        Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
        ```
        Powitania po tooconfirm polecenie można uruchomić tego hello fabryki danych dostawca został zarejestrowany.

        ```PowerShell
        Get-AzureRmResourceProvider
        ```
    - Logowanie przy użyciu hello subskrypcji platformy Azure w toohello [portalu Azure](https://portal.azure.com) i przejdź do bloku usługi fabryka danych tooa tworzenie fabryki danych w hello portalu Azure (lub). Ta akcja rejestruje automatycznie hello dostawcy dla Ciebie.
- Nazwa fabryki danych hello Hello mogą być zarejestrowana jako nazwa DNS w przyszłości hello i dlatego stać się publicznie widoczna.
- wystąpienia fabryki danych toocreate, potrzebujesz toobe administratora lub współadministratora hello subskrypcji platformy Azure

### <a name="monitor-pipeline"></a>Monitorowanie potoku
W tym kroku należy monitorować potoku hello przy użyciu widoku diagramu hello fabryki danych. 

#### <a name="monitor-pipeline-using-diagram-view"></a>Monitorowanie potoku przy użyciu widoku diagramu
1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com/), hello następujące kroki:
   1. Kliknij kolejno pozycje **Więcej usług** i **Fabryki danych**.
       
        ![Przeglądanie fabryk danych](./media/data-factory-build-your-first-pipeline-using-vs/browse-datafactories.png)
   2. Nazwa hello wybierz fabrykę danych (na przykład: **DataFactoryUsingVS09152016**) z listy hello fabryk danych.
   
       ![Wybór fabryki danych](./media/data-factory-build-your-first-pipeline-using-vs/select-first-data-factory.png)
2. Na stronie głównej hello na fabrykę danych, kliknij przycisk **Diagram**.

    ![Kafelek Diagram](./media/data-factory-build-your-first-pipeline-using-vs/diagram-tile.png)
3. W widoku diagramu hello zapoznać się z omówieniem potoki hello i zestawów danych użytych w tym samouczku.

    ![Widok diagramu](./media/data-factory-build-your-first-pipeline-using-vs/diagram-view-2.png)
4. tooview wszystkie działania w potoku hello, kliknij prawym przyciskiem myszy potoku w hello diagram i kliknij przycisk Otwórz potoku.

    ![Menu Otwórz potok](./media/data-factory-build-your-first-pipeline-using-vs/open-pipeline-menu.png)
5. Upewnij się, że widoczny hello HDInsightHive działania w potoku hello.

    ![Widok Otwórz potok](./media/data-factory-build-your-first-pipeline-using-vs/open-pipeline-view.png)

    toonavigate kopii toohello poprzedni widok, kliknij przycisk **fabryki danych** hello nawigacją menu u góry hello.
6. W hello **widoku diagramu**, kliknij dwukrotnie plik zestawu danych hello **AzureBlobInput**. Upewnij się, że wycinek hello jest w **gotowe** stanu. Może potrwać kilka minut dla tooshow wycinka hello w stanie gotowe. Jeśli nie następuje po poczekaj przez pewien czas, zobaczyć, czy wystąpiły pliku wejściowego hello (input.log) umieszczona w kontenerze prawo hello (`adfgetstarted`) i folder (`inputdata`). I upewnij się, że hello **zewnętrznych** zbyt ustawiono właściwość w zestawie danych wejściowych hello**true**. 

   ![Wycinek danych wejściowych w stanie gotowości](./media/data-factory-build-your-first-pipeline-using-vs/input-slice-ready.png)
7. Kliknij przycisk **X** tooclose **AzureBlobInput** bloku.
8. W hello **widoku diagramu**, kliknij dwukrotnie plik zestawu danych hello **AzureBlobOutput**. Użytkownik widzi tego hello wycinek, który jest obecnie przetwarzane.

   ![Zestaw danych](./media/data-factory-build-your-first-pipeline-using-vs/dataset-blade.png)
9. Po zakończeniu przetwarzania zostanie wyświetlony wycinek hello **gotowe** stanu.

   > [!IMPORTANT]
   > Tworzenie klastra usługi HDInsight na żądanie zwykle trwa trochę czasu (około 20 minut). W związku z tym spodziewać się hello potoku tootake **około 30 minut** tooprocess hello wycinka.  
   
    ![Zestaw danych](./media/data-factory-build-your-first-pipeline-using-vs/dataset-slice-ready.png)    
10. Gdy wycinek hello jest **gotowe** stanu, należy sprawdzić hello `partitioneddata` folderu w hello `adfgetstarted` kontenera w magazynie obiektów blob na powitania dane wyjściowe.  

    ![Dane wyjściowe](./media/data-factory-build-your-first-pipeline-using-vs/three-ouptut-files.png)
11. Kliknij przycisk Szczegóły toosee wycinka hello o nim w **wycinka danych** bloku.

    ![Szczegóły wycinka danych](./media/data-factory-build-your-first-pipeline-using-vs/data-slice-details.png)  
12. Kliknij przycisk uruchamiania w hello działania **listy odbywa się działanie** toosee szczegółowe informacje o działaniu można uruchomić (działanie gałęzi w naszym scenariuszu) w **szczegóły uruchomienia działania** okna. 
  
    ![Szczegóły uruchamiania działania](./media/data-factory-build-your-first-pipeline-using-vs/activity-window-blade.png)    

    Z plików dziennika hello widać, zapytanie Hive hello, które zostało wykonane i informacje o stanie. Dzienniki te są przydatne w przypadku rozwiązywania różnych problemów.  

Zobacz [monitorowanie zestawów danych i potoku](data-factory-monitor-manage-pipelines.md) instrukcje jak toouse hello Azure toomonitor portalu hello potoku i zestawy danych zostały utworzone w tym samouczku.

#### <a name="monitor-pipeline-using-monitor--manage-app"></a>Monitorowanie potoku przy użyciu aplikacji Monitorowanie i zarządzanie
Można również użyć monitora i zarządzanie toomonitor aplikacji z potoków. Szczegółowe informacje dotyczące korzystania z aplikacji znajdują się w artykule [Monitor and manage Azure Data Factory pipelines using Monitoring and Management App](data-factory-monitor-manage-app.md) (Monitorowanie potoków usługi Azure Data Factory oraz zarządzanie nimi za pomocą aplikacji Monitorowanie i zarządzanie).

1. Kliknij kafelek Monitorowanie i zarządzanie.

    ![Kafelek Monitorowanie i zarządzanie](./media/data-factory-build-your-first-pipeline-using-vs/monitor-and-manage-tile.png)
2. Powinna zostać wyświetlona aplikacja Monitorowanie i zarządzanie. Zmiany hello **godzina rozpoczęcia** i **czas zakończenia** toomatch start (2016-04-01 00:00:00) godziny i zakończenia (04-02-2016 00:00:00) potoku, i kliknij przycisk **Zastosuj**.

    ![Aplikacja Monitorowanie i zarządzanie](./media/data-factory-build-your-first-pipeline-using-vs/monitor-and-manage-app.png)
3. toosee Szczegóły okna działania, wybierz je w hello **listę okien działania** toosee uzyskać szczegółowe informacje o nim.
    ![Szczegóły okna działania](./media/data-factory-build-your-first-pipeline-using-vs/activity-window-details.png)

> [!IMPORTANT]
> Plik wejściowy Hello zostaje usunięta, gdy hello wycinek jest przetwarzany pomyślnie. W związku z tym wycinek hello toorerun lub Witaj ponownie samouczek, Przekaż hello plik wejściowy (input.log) toohello `inputdata` folderu hello `adfgetstarted` kontenera.

### <a name="additional-notes"></a>Uwagi dodatkowe
- Fabryka danych może obejmować jeden lub wiele potoków. Potok może obejmować jedno lub wiele działań. Na przykład dane wejściowe toocopy działanie kopiowania danych z magazynu danych docelowy tooa źródłowego i HDInsight Hive działania toorun tootransform skryptu Hive. Zobacz [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats) dla wszystkich hello źródeł i wychwytywanie obsługiwane przez hello działanie kopiowania. Zobacz [obliczeniowe połączonych usług](data-factory-compute-linked-services.md) hello lista usługi obliczeniowe obsługiwane przez fabryki danych.
- Połączone usługi łączenie magazyny danych lub obliczeniowe fabryki danych Azure tooan usług. Zobacz [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats) dla wszystkich hello źródeł i wychwytywanie obsługiwane przez hello działanie kopiowania. Zobacz [obliczeniowe połączonych usług](data-factory-compute-linked-services.md) hello lista usługi obliczeniowe obsługiwane przez fabryki danych i [działania przekształcania](data-factory-data-transformation-activities.md) może być na nich.
- Zobacz [przeniesienia danych z / tooAzure obiektu Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) szczegółowe informacje na temat właściwości JSON używane w hello Azure Storage połączone definicji usługi.
- Możesz użyć własnego klastra usługi HDInsight zamiast klastra usługi HDInsight na żądanie. Szczegółowe informacje znajdują się w artykule [Compute Linked Services](data-factory-compute-linked-services.md) (Połączone usługi obliczeniowe).
-  Witaj fabryki danych tworzy **opartych na systemie Linux** klastra usługi HDInsight można z hello poprzedzających JSON. Szczegółowe informacje znajdują się w artykule [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) (Połączona usługa HDInsight na żądanie).
- Tworzy klaster usługi HDInsight Hello **domyślny kontener** w magazynie obiektów blob hello określone w hello JSON (linkedServiceName). Po usunięciu klastra hello HDInsight nie usunie tego kontenera. To zachowanie jest celowe. W przypadku połączonej usługi HDInsight na żądanie klaster usługi HDInsight jest tworzony przy każdym przetwarzaniu wycinka — o ile w tym momencie nie istnieje aktywny klaster (timeToLive). klaster Hello są automatycznie usuwane po zakończeniu przetwarzania hello.
    
    Po przetworzeniu większej liczby wycinków w usłudze Azure Blob Storage będzie widocznych wiele kontenerów. Jeśli nie ma potrzeby do rozwiązywania problemów hello zadań, możesz toodelete ich magazynu hello tooreduce kosztów. nazwy Hello kontenery wykonaj wzorca: `adf**yourdatafactoryname**-**linkedservicename**-datetimestamp`. Użyj narzędzia takiego jak [Eksploratora magazynu](http://storageexplorer.com/) magazynu obiektów blob toodelete kontenerów w platformy Azure.
- Wyjściowy zestaw danych jest obecnie, jakie dysków hello harmonogramu, dlatego należy utworzyć wyjściowy zestaw danych, nawet wtedy, gdy działanie hello nie generuje żadnego wyniku. Jeśli działanie hello nie przyjmuje żadnych danych, możesz pominąć tworzenie zestawu danych wejściowych hello. 
- W tym samouczku nie pokazano, jak skopiować dane za pomocą usługi Azure Data Factory. Samouczek na temat danych toocopy przy użyciu fabryki danych Azure, zobacz [samouczek: kopiowanie danych z magazynu obiektów Blob tooSQL bazy danych](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).


## <a name="use-server-explorer-tooview-data-factories"></a>Użyj fabryki danych tooview Eksploratora serwera
1. W **programu Visual Studio**, kliknij przycisk **widoku** hello menu i kliknij przycisk **Eksploratora serwera**.
2. W oknie Eksploratora serwera hello, rozwiń węzeł **Azure** i rozwiń **fabryki danych**. Jeśli widzisz **Zaloguj tooVisual Studio**, wprowadź hello **konta** skojarzone z subskrypcją platformy Azure i kliknij przycisk **Kontynuuj**. Wprowadź **hasło** i kliknij przycisk **Zaloguj**. Visual Studio próbuje tooget informacji na temat wszystkich fabryki danych Azure w ramach subskrypcji. Zobacz hello stan tej operacji w hello **listy zadań fabryki danych** okna.

    ![Eksplorator serwera](./media/data-factory-build-your-first-pipeline-using-vs/server-explorer.png)
3. Kliknij prawym przyciskiem myszy fabryki danych i wybierz **tooNew wyeksportować fabryki danych projektu** toocreate na istniejącą fabrykę danych na podstawie projektu programu Visual Studio.

    ![Eksportowanie fabryki danych](./media/data-factory-build-your-first-pipeline-using-vs/export-data-factory-menu.png)

## <a name="update-data-factory-tools-for-visual-studio"></a>Aktualizacja narzędzi usługi Fabryka danych dla programu Visual Studio
tooupdate fabryki danych Azure tools dla programu Visual Studio hello następujące kroki:

1. Kliknij przycisk **narzędzia** na powitania menu i wybierz **rozszerzenia i aktualizacje**.
2. Wybierz **aktualizacje** w lewym okienku hello, a następnie wybierz **galerii programu Visual Studio**.
3. Wybierz pozycję **Narzędzia usługi Fabryka danych Azure dla programu Visual Studio** i kliknij przycisk **Aktualizuj**. Jeśli tego wpisu nie jest widoczny, masz już najnowszą wersję narzędzia hello hello.

## <a name="use-configuration-files"></a>Korzystanie z plików konfiguracji
Pliki konfiguracji w programie Visual Studio tooconfigure właściwości można użyć dla połączonej usługi/tabel/potoków inaczej dla każdego środowiska.

Należy wziąć pod uwagę powitania po definicji JSON połączoną usługą magazynu Azure. toospecify **connectionString** z różnych wartości accountname i accountkey oparte na powitania środowiska (deweloperów testu/produkcja) toowhich wdrażasz jednostek fabryki danych. Możesz uzyskać takie zachowanie, stosując oddzielny plik konfiguracji dla każdego środowiska.

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "description": "",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

### <a name="add-a-configuration-file"></a>Dodawanie pliku konfiguracji
Dodaj plik konfiguracji dla każdego środowiska, wykonując następujące kroki hello:   

1. Kliknij prawym przyciskiem myszy hello fabryki danych projektu w rozwiązaniu programu Visual Studio, wskaż zbyt**Dodaj**i kliknij przycisk **nowy element**.
2. Wybierz **konfiguracji** z listy hello zainstalowane szablony powitania po lewej stronie, wybierz **pliku konfiguracyjnego**, wprowadź **nazwa** hello konfiguracji pliku, a następnie kliknij przycisk **Dodaj**.

    ![Dodawanie pliku konfiguracji](./media/data-factory-build-your-first-pipeline-using-vs/add-config-file.png)
3. Dodaj parametry konfiguracji i ich wartości hello następującego formatu:

    ```json
    {
        "$schema": "http://datafactories.schema.management.azure.com/vsschemas/V1/Microsoft.DataFactory.Config.json",
        "AzureStorageLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        ],
        "AzureSqlLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value":  "Server=tcp:spsqlserver.database.windows.net,1433;Database=spsqldb;User ID=spelluru;Password=Sowmya123;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        ]
    }
    ```

    W tym przykładzie opisano konfigurację właściwości connectionString połączonej usługi Azure Storage oraz połączonej usługi SQL Azure. Zwróć uwagę, że składnia hello określania nazwy jest [JsonPath](http://goessner.net/articles/JsonPath/).   

    Jeśli JSON ma właściwość, która ma tablicę wartości, jak pokazano w hello następującego kodu:  

    ```json
    "structure": [
          {
              "name": "FirstName",
            "type": "String"
          },
          {
            "name": "LastName",
            "type": "String"
        }
    ],
    ```

    Skonfiguruj właściwości, jak pokazano w hello następującego pliku konfiguracji (Użyj liczony od zera indeksowania):

    ```json
    {
        "name": "$.properties.structure[0].name",
        "value": "FirstName"
    }
    {
        "name": "$.properties.structure[0].type",
        "value": "String"
    }
    {
        "name": "$.properties.structure[1].name",
        "value": "LastName"
    }
    {
        "name": "$.properties.structure[1].type",
        "value": "String"
    }
    ```

### <a name="property-names-with-spaces"></a>Nazwy właściwości zawierające spacje
Jeśli nazwa właściwości zawiera spacje, Użyj nawiasów kwadratowych, jak pokazano w hello poniższy przykład (nazwa serwera bazy danych):

```json
 {
     "name": "$.properties.activities[1].typeProperties.webServiceParameters.['Database server name']",
     "value": "MyAsqlServer.database.windows.net"
 }
```

### <a name="deploy-solution-using-a-configuration"></a>Wdrożenie rozwiązania przy użyciu konfiguracji
Publikując jednostek fabryki danych Azure w wersji programu VS, można będzie określić konfigurację hello mają toouse dla tej operacji publikowania.

toopublish jednostki w projekcie usługi fabryka danych Azure przy użyciu pliku konfiguracji:   

1. Kliknij prawym przyciskiem myszy projekt fabryki danych i kliknij przycisk **publikowania** toosee hello **publikowania elementów** okno dialogowe.
2. Wybierz istniejącą fabrykę danych lub określ wartości dla tworzenie fabryki danych na powitania **fabryki danych skonfiguruj** , a następnie kliknij przycisk **dalej**.   
3. Na powitania **publikowania elementów** stron: Zobacz listy rozwijanej z dostępnych konfiguracji hello **Wybieranie konfiguracji wdrożenia** pola.

    ![Wybieranie pliku konfiguracji](./media/data-factory-build-your-first-pipeline-using-vs/select-config-file.png)
4. Wybierz hello **pliku konfiguracyjnego** czy chcesz toouse i kliknij przycisk **dalej**.
5. Upewnij się, że widoczne hello nazwę pliku JSON w hello **Podsumowanie** i kliknij przycisk **dalej**.
6. Kliknij przycisk **Zakończ** po zakończeniu operacji wdrażania hello.

Podczas wdrażania, hello wartości z pliku konfiguracji hello są używane tooset wartości właściwości w plikach JSON hello przed jednostek hello tooAzure wdrożonej usługi fabryka danych.   

## <a name="use-azure-key-vault"></a>Korzystanie z rozwiązania Azure Key Vault
Nie jest zalecane i często przed poufnych danych toocommit zasad zabezpieczeń takich jak repozytorium kodu toohello ciągów połączenia. Zobacz [ADF bezpiecznego publikowania](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) w toolearn GitHub o poufne informacje są przechowywane w magazynie kluczy Azure i używa go podczas publikowania jednostek fabryki danych. Hello bezpiecznego publikowania rozszerzenia dla programu Visual Studio umożliwia toobe kluczy tajnych hello przechowywane w magazynie klucza i tylko toothem odwołania są określone w połączonych usług / konfiguracji wdrażania. Te odwołania są rozpoznawane podczas publikowania tooAzure jednostek fabryki danych. Te pliki mogą być następnie repozytorium zatwierdzone toosource bez narażania żadnych kluczy tajnych.

## <a name="summary"></a>Podsumowanie
W tym samouczku danych tooprocess fabryki danych Azure została utworzona przez uruchomienie skryptu Hive w klastrze HDInsight hadoop. Użyto hello Edytor fabryki danych w hello Azure toodo portalu hello następujące kroki:  

1. Tworzenie **fabryki danych** Azure.
2. Utworzyć dwie **połączone usługi**:
   1. **Usługa Azure Storage** połączone usługi toolink Twojego magazynu Azure blob storage przechowuje pliki danych wejściowych/wyjściowych toohello usługi fabryka danych.
   2. **Usługa Azure HDInsight** na żądanie połączone usługi toolink fabrykę danych toohello klastra usługi HDInsight Hadoop na żądanie. Fabryka danych Azure tworzy HDInsight Hadoop dane wejściowe w czasie tooprocess klastra i danych wyjściowych produktu.
3. Utworzone dwie **zestawów danych**, które opisują danych wejściowych i wyjściowych dla działania HDInsight Hive w potoku hello.
4. Utworzyć **potok** za pomocą działania **programu Hive w usłudze HDInsight**.  

## <a name="next-steps"></a>Następne kroki
W tym artykule opisano tworzenie potoku za pomocą działania przekształcenia (działanie usługi HDInsight), które uruchamia skrypt programu Hive w klastrze usługi HDInsight na żądanie. toosee toouse toocopy działanie kopiowania danych z tooAzure obiektów Blob platformy Azure SQL, zobacz temat [samouczek: kopiowanie danych z tooAzure obiektów blob platformy Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

Powiązane z dwóch działań (Uruchom jedno działanie po drugim), ustawiając hello wyjściowy zestaw danych z jednego działania jako hello wejściowy zestaw danych z hello innych działań. Szczegółowe informacje znajdują się w artykule [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) (Planowanie i wykonywanie w usłudze Data Factory). 


## <a name="see-also"></a>Zobacz też
| Temat | Opis |
|:--- |:--- |
| [Potoki](data-factory-create-pipelines.md) |Ten artykuł pomaga w zrozumieniu potoki i działań w fabryce danych Azure i w jaki sposób toouse ich przepływów pracy opartych na danych tooconstruct dla Twojego scenariusza lub firmy. |
| [Zestawy danych](data-factory-create-datasets.md) |Ten artykuł ułatwia zapoznanie się z zestawami danych w usłudze Azure Data Factory. |
| [Działania przekształcania danych](data-factory-data-transformation-activities.md) |Ten artykuł zawiera listę działań przekształcania danych (takich jak przekształcenie programu Hive w usłudze HDInsight używane w tym samouczku) obsługiwanych w usłudze Fabryka danych Azure. |
| [Planowanie i wykonywanie](data-factory-scheduling-and-execution.md) |W tym artykule opisano aspekty planowania i wykonywania hello modelu aplikacji fabryki danych Azure. |
| [Monitorowanie potoków i zarządzanie nimi za pomocą aplikacji do monitorowania](data-factory-monitor-manage-app.md) |W tym artykule opisano sposób toomonitor, zarządzania i debugowania potoki przy użyciu hello monitorowanie & aplikacji do zarządzania. |
