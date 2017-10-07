---
title: aaaInvoke Spark programy z fabryki danych Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak programy Spark tooinvoke z fabryki danych Azure przy użyciu hello działania MapReduce."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: fd98931c-cab5-4d66-97cb-4c947861255c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: f88943ece7ee3d21dedbd857609f1b2713b62741
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="invoke-spark-programs-from-azure-data-factory-pipelines"></a>Wywoływanie programów Spark z potoków fabryki danych Azure

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

## <a name="introduction"></a>Wprowadzenie
Działanie Spark jest jednym z hello [działań przekształcania danych](data-factory-data-transformation-activities.md) obsługiwane przez usługi fabryka danych Azure. To działanie jest uruchomione hello określony program Spark w klastrze Apache Spark w usłudze Azure HDInsight.    

> [!IMPORTANT]
> - Działanie Spark nie obsługuje klastrów HDInsight Spark, które używają usługi Azure Data Lake Store jako podstawowy magazyn.
> - Działanie Spark obsługuje tylko istniejące (własne) klastry HDInsight Spark. Nie obsługuje usługi HDInsight połączony na żądanie.

## <a name="walkthrough-create-a-pipeline-with-spark-activity"></a>Wskazówki: tworzenie potoku z działaniem Spark
Poniżej przedstawiono hello toocreate typowe etapy potoku fabryki danych z działaniem Spark.  

1. Tworzenie fabryki danych.
2. Utwórz magazyn Azure skojarzony z fabryką danych toohello klastra Spark w usłudze HDInsight toolink usługi Azure Storage połączone.     
2. Utwórz toolink usługi Azure HDInsight połączone klastra Apache Spark w fabryce danych Azure HDInsight toohello.
3. Tworzenie zestawu danych, który odwołuje się toohello połączoną usługą magazynu Azure. Obecnie należy określić wyjściowy zestaw danych działania nawet jeśli dostępny jest nie wytworzonych.  
4. Utworzyć potok z działaniem Spark, odnoszący się do usługi HDInsight połączone toohello utworzone w #2. Hello jest skonfigurowane z zestawem danych hello, utworzony w poprzednim kroku hello jako wyjściowego zestawu danych. Witaj wyjściowy zestaw danych jest jakie dysków hello harmonogram (co godzinę, codziennie, itp.). W związku z tym należy określić hello wyjściowy zestaw danych nawet, jeśli działanie hello nie tworzy naprawdę danych wyjściowych.

### <a name="prerequisites"></a>Wymagania wstępne
1. Utwórz **ogólnego przeznaczenia konta magazynu Azure** przez następujące instrukcje w przewodniku hello: [Utwórz konto magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account).  
2. Utwórz **klastra Apache Spark w usłudze Azure HDInsight** przez następujące instrukcje w samouczku hello: [klastra Utwórz Apache Spark w usłudze Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md). Kojarzenie hello kontem magazynu platformy Azure, który został utworzony w kroku #1 z tym klastrem.  
3. Pobierz i przejrzyj plik skryptu języka python hello **test.py** w lokalizacji: [https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py).  
3.  Przekaż **test.py** toohello **pyFiles** folderu w hello **adfspark** kontenera w magazynie obiektów Blob platformy Azure. Utwórz hello kontenera i folderu hello, jeśli nie istnieją.

### <a name="create-data-factory"></a>Tworzenie fabryki danych
Zacznijmy od utworzenia hello fabryki danych w tym kroku.

1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).
2. Kliknij przycisk **nowy** w menu po lewej stronie powitania kliknij **dane i analiza**i kliknij przycisk **fabryki danych**.
3. W hello **nowa fabryka danych** bloku, wprowadź **SparkDF** dla hello nazwy.

   > [!IMPORTANT]
   > Nazwa fabryki danych Azure hello Hello musi być **unikatowych**. Jeśli zostanie wyświetlony błąd hello: **nazwa fabryki danych "SparkDF" nie jest dostępny**. Zmień nazwę hello fabryki danych hello (na przykład yournameSparkDFdate i spróbuj ponownie utworzyć. Artykuł [Data Factory — Naming Rules](data-factory-naming-rules.md) (Fabryka danych — zasady nazewnictwa) zawiera zasady nazewnictwa artefaktów usługi Fabryka danych.   
4. Wybierz hello **subskrypcji platformy Azure** miejscu toobe fabryki danych hello utworzony.
5. Wybierz istniejący **grupy zasobów** lub Utwórz grupę zasobów platformy Azure.
6. Wybierz **toodashboard numeru Pin** opcji.  
6. Kliknij przycisk **Utwórz** na powitania **nowa fabryka danych** bloku.

   > [!IMPORTANT]
   > toocreate wystąpienia fabryki danych, musi być członkiem hello [współautora fabryki danych](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) roli na poziomie grupy zasobów subskrypcji hello.
7. Zobacz hello fabryki danych tworzona w hello **pulpitu nawigacyjnego** z hello portalu Azure w następujący sposób:   
8. Po hello fabryki danych został utworzony pomyślnie, zobacz strony fabryki danych hello, który umożliwia hello zawartość hello fabryki danych. Jeśli nie ma strony fabryki danych hello, kliknij Kafelek hello fabrykę danych na pulpicie nawigacyjnym hello.

    ![Blok Fabryka danych](./media/data-factory-spark/data-factory-blade.png)

### <a name="create-linked-services"></a>Tworzenie połączonych usług
W tym kroku utwórz dwa połączone usługi, co toolink fabrykę danych tooyour klastra Spark, a hello innych toolink fabrykę danych tooyour magazynu Azure.  

#### <a name="create-azure-storage-linked-service"></a>Tworzenie połączonej usługi Azure Storage
W tym kroku możesz połączyć fabrykę danych tooyour konta magazynu Azure. Zestaw danych utworzone w kroku później w tym przewodniku odnosi się toothis połączone usługi. Hello usługi HDInsight połączone, zdefiniowanego w następnym kroku hello zbyt odwołuje się toothis połączone usługi.  

1. Kliknij przycisk **tworzenie i wdrażanie** na powitania **fabryki danych** bloku fabryką danych. Powinny pojawić się hello Edytor fabryki danych.
2. Kliknij przycisk **Nowy magazyn danych** i wybierz opcję **Azure Storage**.

   ![Nowy magazyn danych — Azure Storage — menu](./media/data-factory-spark/new-data-store-azure-storage-menu.png)
3. Powinny pojawić się hello **skryptu JSON** do tworzenia usługi Azure Storage połączonej usługi w edytorze hello.

   ![Połączona usługa Azure Storage](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. Zastąp **nazwa konta** i **klucz konta** z hello nazwy i klucza dostępu konta magazynu Azure. toolearn sposób dostępu do magazynu tooget klucza, zobacz hello informacji na temat sposobu tooview, kopiowania i regenerate magazynu dostępu do kluczy w [Zarządzanie kontem magazynu](../storage/common/storage-create-storage-account.md#manage-your-storage-account).
5. toodeploy hello połączonej usługi, kliknij przycisk **Wdróż** na powitania paska poleceń. Witaj po hello połączonej usługi został wdrożony pomyślnie, **projekt 1** powinien zniknąć okna, aby zobaczyć **AzureStorageLinkedService** w widoku drzewa hello powitania po lewej stronie.

#### <a name="create-hdinsight-linked-service"></a>Tworzenie usługi HDInsight połączone
W tym kroku utworzysz toolink usługi Azure HDInsight połączone fabrykę danych toohello klastra Spark w usłudze HDInsight. klaster usługi HDInsight Hello jest programu Spark hello używane toorun określony w działaniu Spark hello hello potoku, w tym przykładzie.  

1. Kliknij przycisk **... Więcej** na powitania narzędzi, kliknij przycisk **nowych obliczeń**, a następnie kliknij przycisk **klastra usługi HDInsight**.

    ![Tworzenie usługi HDInsight połączone](media/data-factory-spark/new-hdinsight-linked-service.png)
2. Skopiuj i Wklej powitania po toohello fragment **projekt 1** okna. W edytorze JSON hello hello następujące kroki:
    1. Określ hello **URI** hello Spark w usłudze HDInsight klastra. Na przykład: `https://<sparkclustername>.azurehdinsight.net/`.
    2. Określ nazwę hello hello **użytkownika** kto ma dostęp toohello Spark klastra.
    3. Określ hello **hasło** dla użytkownika.
    4. Określ hello **połączonej usługi magazynu Azure** skojarzonego z hello klastra Spark w usłudze HDInsight. W tym przykładzie jest: **AzureStorageLinkedService**.

    ```json
    {
        "name": "HDInsightLinkedService",
        "properties": {
            "type": "HDInsight",
            "typeProperties": {
                "clusterUri": "https://<sparkclustername>.azurehdinsight.net/",
                "userName": "admin",
                "password": "**********",
                "linkedServiceName": "AzureStorageLinkedService"
            }
        }
    }
    ```

    > [!IMPORTANT]
    > - Działanie Spark nie obsługuje klastrów HDInsight Spark, które używają usługi Azure Data Lake Store jako podstawowy magazyn.
    > - Działanie Spark obsługuje tylko istniejące (własne) klastra Spark w usłudze HDInsight. Nie obsługuje usługi HDInsight połączony na żądanie.

    Zobacz [połączoną usługą usługi HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) szczegółowe informacje o hello HDInsight połączonej usługi.
3.  toodeploy hello połączonej usługi, kliknij przycisk **Wdróż** na powitania paska poleceń.  

### <a name="create-output-dataset"></a>Tworzenie wyjściowego zestawu danych
Witaj wyjściowy zestaw danych jest jakie dysków hello harmonogram (co godzinę, codziennie, itp.). W związku z tym należy określić wyjściowy zestaw danych dla hello spark działania w potoku hello mimo, że działanie hello nie tworzy naprawdę żadnych danych wyjściowych. Określenie zestawem danych wejściowych dla działania hello jest opcjonalne.

1. W hello **Edytor fabryki danych**, kliknij przycisk **... Więcej** na pasku poleceń powitania kliknij **nowy zestaw danych**i wybierz **magazynu obiektów Blob Azure**.  
2. Skopiuj i Wklej powitania po fragment okna toohello projekt-1. fragment kodu JSON Hello definiuje zestaw danych o nazwie **OutputDataset**. Ponadto należy określić czy hello wyniki są przechowywane w kontenerze obiektów blob hello o nazwie **adfspark** i hello folder o nazwie **pyFiles/wyjścia**. Jak wspomniano wcześniej, ten zestaw danych jest fikcyjny zestawu danych. program Spark Hello w tym przykładzie nie generuje żadnego wyniku. Witaj **dostępności** sekcja określa, że wyjściowy zestaw danych hello jest tworzony codziennie.  

    ```json
    {
        "name": "OutputDataset",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "sparkoutput.txt",
                "folderPath": "adfspark/pyFiles/output",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": "\t"
                }
            },
            "availability": {
                "frequency": "Day",
                "interval": 1
            }
        }
    }
    ```
3. toodeploy hello zestawu danych, kliknij przycisk **Wdróż** na powitania paska poleceń.


### <a name="create-pipeline"></a>Tworzenie potoku
W tym kroku możesz utworzyć potok wraz z **HDInsightSpark** działania. Wyjściowy zestaw danych jest obecnie, jakie dysków hello harmonogramu, dlatego należy utworzyć wyjściowy zestaw danych, nawet wtedy, gdy działanie hello nie generuje żadnego wyniku. Jeśli działanie hello nie przyjmuje żadnych danych, możesz pominąć tworzenie zestawu danych wejściowych hello. W związku z tym nie wejściowy zestaw danych został określony w tym przykładzie.

1. W hello **Edytor fabryki danych**, kliknij przycisk **... Więcej** na hello pasek poleceń, a następnie kliknij przycisk **nowy potok**.
2. Zastąp hello skryptu w oknie hello projekt 1 hello następującego skryptu:

    ```json
    {
        "name": "SparkPipeline",
        "properties": {
            "activities": [
                {
                    "type": "HDInsightSpark",
                    "typeProperties": {
                        "rootPath": "adfspark\\pyFiles",
                        "entryFilePath": "test.py",
                        "getDebugInfo": "Always"
                    },
                    "outputs": [
                        {
                            "name": "OutputDataset"
                        }
                    ],
                    "name": "MySparkActivity",
                    "linkedServiceName": "HDInsightLinkedService"
                }
            ],
            "start": "2017-02-05T00:00:00Z",
            "end": "2017-02-06T00:00:00Z"
        }
    }
    ```
    Należy zwrócić uwagę hello następujące punkty:
    - Witaj **typu** właściwość jest ustawiona zbyt**HDInsightSpark**.
    - Witaj **właściwość rootPath** ustawiono zbyt**adfspark\\pyFiles** gdzie adfspark jest pyFiles i kontener obiektów Blob Azure hello jest poprawnie folderu, w tym kontenerze. W tym przykładzie hello magazynu obiektów Blob Azure jest hello, który jest skojarzony z klastrem Spark hello. Możesz przekazać tooa pliku hello innego magazynu Azure. Jeśli tak zrobisz, należy utworzyć toolink usługi Azure Storage połączone tej fabryki danych toohello konta magazynu. Następnie określ nazwę hello hello połączone usługi jako wartość hello **sparkJobLinkedService** właściwości. Zobacz [właściwości działania Spark](#spark-activity-properties) szczegóły dotyczące tej właściwości oraz inne właściwości obsługiwanych przez hello działania Spark.  
    - Witaj **entryFilePath** ustawiono toohello **test.py**, czyli plik python hello.
    - Witaj **getDebugInfo** właściwość jest ustawiona zbyt**zawsze**, co oznacza, że pliki dziennika hello są zawsze generowany (powodzenie lub niepowodzenie).

        > [!IMPORTANT]
        > Firma Microsoft zaleca, aby nie ustawisz tę właściwość za`Always` w środowisku produkcyjnym, chyba że są Rozwiązywanie problemów.
    - Witaj **generuje** sekcja ma jeden wyjściowy zestaw danych. Należy określić wyjściowy zestaw danych, nawet jeśli hello spark program nie zwraca żadnych danych wyjściowych. Hello wyjściowego zestawu danych dysków hello harmonogram dla potoku hello (co godzinę, codziennie, itp.).  

        Aby uzyskać szczegółowe informacje o obsługiwanych przez działanie Spark właściwości hello, zobacz [Spark właściwości działania](#spark-activity-properties) sekcji.
3. toodeploy hello potoku, kliknij przycisk **Wdróż** na powitania paska poleceń.

### <a name="monitor-pipeline"></a>Monitorowanie potoku
1. Kliknij przycisk **X** tooclose bloków Edytor fabryki danych i toonavigate ponownie strony głównej toohello fabryki danych. Kliknij przycisk **monitorowanie i zarządzanie** hello toolaunch monitorowania aplikacji w innej karty.

    ![Monitorowanie i zarządzanie nimi kafelka](media/data-factory-spark/monitor-and-manage-tile.png)
2. Zmień hello **godzina rozpoczęcia** filtru u góry hello zbyt**2/1/2017**i kliknij przycisk **Zastosuj**.
3. Tylko jedno okno działania powinna zostać wyświetlona z powodu godziny (2017-02-02) potoku hello między hello tylko jeden dzień rozpoczęcia (2017-02-01) i zakończenia. Upewnij się, że hello wycinka danych jest w **gotowe** stanu.

    ![Monitor hello potoku](media/data-factory-spark/monitor-and-manage-app.png)    
4. Wybierz hello **okno działania** toosee szczegóły dotyczące uruchamiania działania hello. Jeśli występuje błąd, zobaczysz szczegółowe informacje o nim w okienku po prawej stronie powitania.

### <a name="verify-hello-results"></a>Sprawdź wyniki hello

1. Uruchom **notesu Jupyter** przechodząc do klastra Spark w usłudze HDInsight: https://CLUSTERNAME.azurehdinsight.net/jupyter. Można również uruchomić Pulpit nawigacyjny klastra dla klastra Spark w usłudze HDInsight, a następnie uruchom **notesu Jupyter**.
2. Kliknij przycisk **nowy** -> **PySpark** toostart nowy notes.

    ![Nowego notesu Jupyter](media/data-factory-spark/jupyter-new-book.png)
3. Uruchom hello następujące polecenia kopiowania/wklejania hello tekstu i naciskając klawisz **SHIFT + ENTER** na końcu hello hello drugiej instrukcji.  

    ```sql
    %%sql

    SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"
    ```
4. Upewnij się, że widoczny hello danych z tabeli hvac hello:  

    ![Wyniki zapytania Jupyter](media/data-factory-spark/jupyter-notebook-results.png)

Zobacz [uruchamiania zapytań Spark SQL](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md#run-a-hive-query-using-spark-sql) sekcji, aby uzyskać szczegółowe instrukcje. 

### <a name="troubleshooting"></a>Rozwiązywanie problemów
Ponieważ ustawisz **getDebugInfo** za**zawsze**, zostanie wyświetlony **dziennika** podfolder hello **pyFiles** folderu w kontenerze obiektu Blob Azure. Witaj pliku dziennika w folderze dziennika hello zawiera dodatkowe szczegóły. Ten plik dziennika jest szczególnie przydatna w przypadku, gdy występuje błąd. W środowisku produkcyjnym można tooset on zbyt**błąd**.

Aby uzyskać dodatkowe informacje o rozwiązywaniu, hello następujące kroki:


1. Przejdź do zbyt`https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`.

    ![Aplikacja YARN interfejsu użytkownika](media/data-factory-spark/yarnui-application.png)  
2. Kliknij przycisk **dzienniki** jednego hello Uruchom prób.

    ![Strona aplikacji](media/data-factory-spark/yarn-applications.png)
3. Dodatkowe informacje o błędzie na stronie dziennika hello powinna zostać wyświetlona.

    ![Błąd dziennika](media/data-factory-spark/yarnui-application-error.png)

Witaj następujące sekcje zawierają informacje dotyczące klastra Apache Spark toouse jednostek fabryki danych i działania Spark w fabryce danych.

## <a name="spark-activity-properties"></a>Właściwości działania Spark
Oto definicji JSON próbki hello potoku z działaniem Spark:    

```json
{
    "name": "SparkPipeline",
    "properties": {
        "activities": [
            {
                "type": "HDInsightSpark",
                "typeProperties": {
                    "rootPath": "adfspark\\pyFiles",
                    "entryFilePath": "test.py",
                    "arguments": [ "arg1", "arg2" ],
                    "sparkConfig": {
                        "spark.python.worker.memory": "512m"
                    }
                    "getDebugInfo": "Always"
                },
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ],
                "name": "MySparkActivity",
                "description": "This activity invokes hello Spark program",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-01T00:00:00Z",
        "end": "2017-02-02T00:00:00Z"
    }
}
```

Witaj poniższej tabeli opisano właściwości JSON hello używane w definicji JSON hello:

| Właściwość | Opis | Wymagane |
| -------- | ----------- | -------- |
| name | Nazwa działania hello w potoku hello. | Tak |
| description | Tekst opisujący jakie działanie hello jest. | Nie |
| type | Tej właściwości należy ustawić tooHDInsightSpark. | Tak |
| linkedServiceName | Nazwa hello HDInsight połączonej usługi, na których hello Spark program będzie uruchamiany. | Tak |
| Właściwość rootPath | Witaj kontenera obiektów Blob platformy Azure i folder zawierający plik Spark hello. Nazwa pliku Hello jest rozróżniana wielkość liter. | Tak |
| entryFilePath | Względna ścieżka folderu głównego toohello hello pakietu kodu Spark. | Tak |
| className | Klasy głównym aplikacji Java/Spark | Nie |
| Argumenty | Lista argumentów wiersza polecenia toohello Spark program. | Nie |
| proxyUser | program Spark hello tooexecute tooimpersonate Hello użytkownika konta | Nie |
| sparkConfig | Określ wartości dla właściwości konfiguracji Spark wymienione w temacie hello: [konfiguracji Spark — właściwości aplikacji](https://spark.apache.org/docs/latest/configuration.html#available-properties). | Nie |
| getDebugInfo | Określa, kiedy pliki dziennika Spark hello są kopiowane toohello magazynu Azure używanego przez klaster usługi HDInsight (lub) został określony przez sparkJobLinkedService. Dozwolone wartości: None, zawsze lub niepowodzenie. Wartość domyślna: Brak. | Nie |
| sparkJobLinkedService | Witaj połączoną usługą magazynu Azure zawierający plik zadania hello Spark, zależności i dzienniki.  Jeśli nie określisz wartości dla tej właściwości, jest używany Magazyn hello skojarzony z klastrem usługi HDInsight. | Nie |

## <a name="folder-structure"></a>Struktura folderów
Hello Spark działania nie obsługuje skryptu w wierszu jako Pig i do gałęzi działań. Zadań Spark jest również extensible więcej niż zadań Pig/Hive. W przypadku zadań Spark, możesz podać wiele zależności takich jak jar pakietów (umieszczona w języku java hello ścieżki klasy), pliki języka python (umieszczona na powitania PYTHONPATH) i innych plików.

Utwórz hello następujące struktury folderów w hello odwołuje się hello HDInsight połączone usługi magazynu obiektów Blob platformy Azure. Natomiast przekazywanie plików zależnych toohello odpowiednie podfoldery w folderze głównym hello reprezentowany przez **entryFilePath**. Na przykład Przekaż podfolder pyFiles toohello pliki języka python oraz jar pliki toohello słoików podfolder folderu głównego hello. W czasie wykonywania usługi fabryka danych oczekuje hello następujące struktury folderów w hello magazynu obiektów Blob platformy Azure:     

| Ścieżka | Opis | Wymagane | Typ |
| ---- | ----------- | -------- | ---- |
| . | Ścieżka katalogu głównego Hello hello Spark zadania w hello połączoną usługą magazynu    | Tak | Folder |
| &lt;zdefiniowane przez użytkownika&gt; | Ścieżka pliku wpis toohello zadania Spark hello Hello | Tak | Plik |
| . / jars | Wszystkie pliki w tym folderze są przekazywane i umieszczane na powitania klasy java hello klastra | Nie | Folder |
| . / pyFiles | Wszystkie pliki w tym folderze są przekazywane i umieszczane na powitania PYTHONPATH hello klastra | Nie | Folder |
| . / pliki | Wszystkie pliki w tym folderze są przekazywane i dotyczącymi Moduł wykonujący katalog roboczy | Nie | Folder |
| . / archiwa | Wszystkie pliki w tym folderze są nieskompresowanych | Nie | Folder |
| . / dzienników | Witaj folder, w którym są przechowywane dzienniki hello klastra Spark.| Nie | Folder |

Oto przykład do magazynu zawierającego dwa pliki zadania Spark w hello odwołuje się hello HDInsight połączone usługi Magazyn obiektów Blob Azure.

```
SparkJob1
    main.jar
    files
        input1.txt
        input2.txt
    jars
        package1.jar
        package2.jar
    logs

SparkJob2
    main.py
    pyFiles
        scrip1.py
        script2.py
    logs
```
