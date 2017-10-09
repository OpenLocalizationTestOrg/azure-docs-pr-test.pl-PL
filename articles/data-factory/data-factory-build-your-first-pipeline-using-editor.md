---
title: aaaBuild pierwszy fabryki danych (Azure portal) | Dokumentacja firmy Microsoft
description: "W tym samouczku utworzysz potok fabryki danych Azure próbki, przy użyciu Edytor fabryki danych w hello portalu Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: d5b14e9e-e358-45be-943c-5297435d402d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: fc80776001b181a59c04d80d2e05c20b107a63f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-portal"></a>Samouczek: tworzenie pierwszej fabryki danych platformy Azure przy użyciu witryny Azure Portal
> [!div class="op_single_selector"]
> * [Przegląd i wymagania wstępne](data-factory-build-your-first-pipeline.md)
> * [Witryna Azure Portal](data-factory-build-your-first-pipeline-using-editor.md)
> * [Program Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [Program PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Szablon usługi Resource Manager](data-factory-build-your-first-pipeline-using-arm.md)
> * [Interfejs API REST](data-factory-build-your-first-pipeline-using-rest-api.md)


W tym artykule dowiesz się, jak toouse [portalu Azure](https://portal.azure.com/) toocreate Twojego pierwszego fabryki danych Azure. Samouczek hello toodo przy użyciu innych narzędzi/SDK, wybierz jedną z opcji hello z listy rozwijanej hello. 

Witaj potoku, w tym samouczku ma jedno działanie: **działania HDInsight Hive**. To działanie uruchamia skrypt hive w klastrze Azure HDInsight czy transformacji wejściowych danych wyjściowych tooproduce danych. potok Hello jest zaplanowane toorun po miesiącu między hello określono godziny rozpoczęcia i zakończenia. 

> [!NOTE]
> Witaj potoku danych w tym samouczku przekształca dane wyjściowe tooproduce danych wejściowych. Samouczek na temat danych toocopy przy użyciu fabryki danych Azure, zobacz [samouczek: kopiowanie danych z magazynu obiektów Blob tooSQL bazy danych](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> Potok może obejmować więcej niż jedno działanie. I tworzenia łańcucha dwa działania (Uruchom jedno działanie po drugim), ustawiając hello wyjściowy zestaw danych z jednego działania jako hello wejściowy zestaw danych z hello innych działań. Więcej informacji znajduje się w artykule dotyczącym [planowania i wykonywania w usłudze Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).

## <a name="prerequisites"></a>Wymagania wstępne
1. Zapoznaj się z artykułem [— samouczek Przegląd](data-factory-build-your-first-pipeline.md) artykułu i pełne hello **wymagań wstępnych** czynności.
2. W tym artykule nie zawiera omówienie hello usługi fabryka danych Azure. Firma Microsoft zaleca zapoznanie [tooAzure wprowadzenie fabryki danych](data-factory-introduction.md) artykuł, aby szczegółowy przegląd hello usługi.  

## <a name="create-data-factory"></a>Tworzenie fabryki danych
Fabryka danych może obejmować jeden lub wiele potoków. Potok może obejmować jedno lub wiele działań. Na przykład toocopy działanie kopiowania danych z magazynu danych docelowy tooa źródłowego i HDInsight Hive działania toorun tootransform skryptu Hive wejściowe dane wyjściowe tooproduct danych. Zacznijmy od utworzenia hello fabryki danych w tym kroku.

1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).
2. Kliknij przycisk **nowy** w menu po lewej stronie powitania kliknij **dane i analiza**i kliknij przycisk **fabryki danych**.

   ![Blok tworzenia](./media/data-factory-build-your-first-pipeline-using-editor/create-blade.png)
3. W hello **nowa fabryka danych** bloku, wprowadź **GetStartedDF** dla hello nazwy.

   ![Blok Nowa fabryka danych](./media/data-factory-build-your-first-pipeline-using-editor/new-data-factory-blade.png)

   > [!IMPORTANT]
   > Nazwa fabryki danych Azure hello Hello musi być **unikatowych**. Jeśli wystąpi błąd hello: **nazwa fabryki danych "GetStartedDF" nie jest dostępny**. Zmień nazwę hello hello fabryki danych (na przykład yournameGetStartedDF), a następnie spróbuj ponownie utworzyć. Artykuł [Data Factory — Naming Rules](data-factory-naming-rules.md) (Fabryka danych — zasady nazewnictwa) zawiera zasady nazewnictwa artefaktów usługi Fabryka danych.
   >
   > Nazwa fabryki danych hello Hello może zostać zarejestrowana jako **DNS** nazwy w przyszłości hello i dlatego stać się publicznie widoczna.
   >
   >
4. Wybierz hello **subskrypcji platformy Azure** miejscu toobe fabryki danych hello utworzony.
5. Wybierz istniejącą **grupę zasobów** lub utwórz grupę zasobów. Samouczek hello, Utwórz grupę zasobów o nazwie: **ADFGetStartedRG**.
6. Wybierz hello **lokalizacji** hello fabryki danych. Tylko regiony obsługiwane przez hello usługi fabryka danych są wyświetlane na liście rozwijanej hello.
7. Wybierz **toodashboard numeru Pin**. 
8. Kliknij przycisk **Utwórz** na powitania **nowa fabryka danych** bloku.

   > [!IMPORTANT]
   > toocreate wystąpienia fabryki danych, musi być członkiem hello [współautora fabryki danych](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) roli na poziomie grupy zasobów subskrypcji hello.
   >
   >
7. Na pulpicie nawigacyjnym hello, zobacz następujące hello kafelka ze stanem: Wdrażanie fabryki danych.    

   ![Stan tworzenia fabryki danych](./media/data-factory-build-your-first-pipeline-using-editor/creating-data-factory-image.png)
8. Gratulacje! Udało Ci się utworzyć pierwszą fabrykę danych. Po hello fabryki danych został utworzony pomyślnie, zobacz strony fabryki danych hello, który umożliwia hello zawartość hello fabryki danych.     

    ![Blok Fabryka danych](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-blade.png)

Przed utworzeniem potok w fabryce danych hello, należy toocreate kilku jednostek fabryki danych najpierw. Najpierw utwórz danych toolink połączonych usług danych tooyour magazyny/oblicza przechowywania, zdefiniuj dane wejściowe i zestawów danych toorepresent wejścia/wyjścia dane w magazynach połączone dane wyjściowe, a następnie utwórz hello potoku do działania, która używa tych zestawów danych.

## <a name="create-linked-services"></a>Tworzenie połączonych usług
W tym kroku możesz połączyć konta magazynu Azure i fabrykę danych tooyour klastra Azure HDInsight na żądanie. blokady konta usługi Azure Storage Hello hello danych wejściowych i wyjściowych do potoku hello w tym przykładzie. Hello usługi HDInsight połączony jest używane toorun określony w działaniu hello hello potoku, w tym przykładzie skrypt Hive. Zidentyfikuj co [magazynu danych](data-factory-data-movement-activities.md)/[obliczeniowe usług](data-factory-compute-linked-services.md) są używane w danym scenariuszu i łączenie fabryki danych toohello tych usług za tworzenie połączonych usług.  

### <a name="create-azure-storage-linked-service"></a>Tworzenie połączonej usługi Azure Storage
W tym kroku możesz połączyć fabrykę danych tooyour konta magazynu Azure. W tym samouczku użyjesz hello tego samego konta magazynu Azure toostore wejścia/wyjścia danych i hello HQL plik skryptu.

1. Kliknij przycisk **tworzenie i wdrażanie** na powitania **FABRYKI danych** bloku **GetStartedDF**. Powinny pojawić się hello Edytor fabryki danych.

   ![Kafelek Utwórz i wdróż](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-author-deploy.png)
2. Kliknij przycisk **Nowy magazyn danych** i wybierz opcję **Azure Storage**.

   ![Nowy magazyn danych — Azure Storage — menu](./media/data-factory-build-your-first-pipeline-using-editor/new-data-store-azure-storage-menu.png)
3. Powinny pojawić się hello skryptu JSON do tworzenia usługi Azure Storage połączonej usługi w edytorze hello.

   ![Połączona usługa Azure Storage](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. Zastąp **nazwa konta** hello nazwą konta magazynu Azure i **klucz konta** z klucz dostępu hello hello kontem magazynu platformy Azure. toolearn sposób dostępu do magazynu tooget klucza, zobacz hello informacji na temat sposobu tooview, kopiowania i regenerate magazynu dostępu do kluczy w [Zarządzanie kontem magazynu](../storage/common/storage-create-storage-account.md#manage-your-storage-account).
5. Kliknij przycisk **Wdróż** na pasku toodeploy hello połączone usługi poleceń hello.

    ![Przycisk Wdróż](./media/data-factory-build-your-first-pipeline-using-editor/deploy-button.png)

   Witaj po hello połączonej usługi został wdrożony pomyślnie, **projekt 1** powinien zniknąć okna, aby zobaczyć **AzureStorageLinkedService** w widoku drzewa hello powitania po lewej stronie.

    ![Połączona usługa Storage w menu](./media/data-factory-build-your-first-pipeline-using-editor/StorageLinkedServiceInTree.png)    

### <a name="create-azure-hdinsight-linked-service"></a>Tworzenie połączonej usługi Azure HDInsight
W tym kroku możesz połączyć fabrykę danych tooyour klastra usługi HDInsight na żądanie. klaster usługi HDInsight Hello jest automatycznie tworzone w czasie wykonywania i usuwane po zakończeniu przetwarzania i bezczynności hello określoną ilość czasu.

1. W hello **Edytor fabryki danych**, kliknij przycisk **... więcej**, kliknij przycisk **Nowe obliczenie** i wybierz **Klaster usługi HDInsight na żądanie**.

    ![Nowe obliczenie](./media/data-factory-build-your-first-pipeline-using-editor/new-compute-menu.png)
2. Skopiuj i Wklej powitania po toohello fragment **projekt 1** okna. fragment kodu JSON Hello opisuje hello właściwości, które są używane toocreate hello HDInsight klastra na żądanie.

    ```JSON
    {
        "name": "HDInsightOnDemandLinkedService",
        "properties": {
            "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "linkedServiceName": "AzureStorageLinkedService"
            }
        }
    }
    ```

    Witaj Poniższa tabela zawiera opisy właściwości JSON hello używane we fragmencie hello:

   | Właściwość | Opis |
   |:--- |:--- |
   | ClusterSize |Określa rozmiar hello hello klastra usługi HDInsight. |
   | TimeToLive | Określa czas bezczynności tej hello hello klastra usługi HDInsight, przed usunięciem. |
   | linkedServiceName | Określa konto magazynu hello, które jest używane toostore hello dzienniki, generowanych przez usługi HDInsight. |

    Należy zwrócić uwagę hello następujące punkty:

   * Witaj fabryki danych tworzy **opartych na systemie Linux** klastra usługi HDInsight za pomocą hello JSON. Szczegółowe informacje znajdują się w artykule [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) (Połączona usługa HDInsight na żądanie).
   * Możesz użyć **własnego klastra usługi HDInsight** zamiast klastra usługi HDInsight na żądanie. Szczegółowe informacje znajdują się w artykule [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) (Połączona usługa HDInsight).
   * Tworzy klaster usługi HDInsight Hello **domyślny kontener** w magazynie obiektów blob hello określone w hello JSON (**linkedServiceName**). Po usunięciu klastra hello HDInsight nie usunie tego kontenera. To zachowanie jest celowe. W przypadku połączonej usługi HDInsight na żądanie klaster usługi HDInsight jest tworzony przy każdym przetwarzaniu wycinka — o ile w tym momencie nie istnieje aktywny klaster (**timeToLive**). klaster Hello są automatycznie usuwane po zakończeniu przetwarzania hello.

       Po przetworzeniu większej liczby wycinków w usłudze Azure Blob Storage będzie widocznych wiele kontenerów. Jeśli nie ma potrzeby do rozwiązywania problemów hello zadań, możesz toodelete ich magazynu hello tooreduce kosztów. nazwy Hello kontenery wykonaj wzorca: "adf**yourdatafactoryname**-**linkedservicename**- datetimestamp". Użyj narzędzia takiego jak [Eksploratora magazynu](http://storageexplorer.com/) magazynu obiektów blob toodelete kontenerów w platformy Azure.

     Szczegółowe informacje znajdują się w artykule [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) (Połączona usługa HDInsight na żądanie).
3. Kliknij przycisk **Wdróż** na pasku toodeploy hello połączone usługi poleceń hello.

    ![Wdrażanie połączonej usługi HDInsight na żądanie](./media/data-factory-build-your-first-pipeline-using-editor/ondemand-hdinsight-deploy.png)
4. Upewnij się, że wyświetlany jest zarówno **AzureStorageLinkedService** i **HDInsightOnDemandLinkedService** w widoku drzewa hello powitania po lewej stronie.

    ![Widok drzewa z połączonymi usługami](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-linked-services.png)

## <a name="create-datasets"></a>Tworzenie zestawów danych
W tym kroku utwórz wprowadzania hello toorepresent zestawów danych i wysyłania danych do przetwarzania Hive. Te zestawy danych można znaleźć toohello **AzureStorageLinkedService** został utworzony we wcześniejszej części tego samouczka. Witaj tooan punktów połączonej usługi konta usługi Azure Storage i zestawów danych, określ kontener, folder, nazwa pliku w magazynie hello, która przechowuje dane wejściowe i wyjściowe danych.   

### <a name="create-input-dataset"></a>Tworzenie wejściowego zestawu danych
1. W hello **Edytor fabryki danych**, kliknij przycisk **... Więcej** na pasku poleceń powitania kliknij **nowy zestaw danych**i wybierz **magazynu obiektów Blob Azure**.

    ![Nowy zestaw danych](./media/data-factory-build-your-first-pipeline-using-editor/new-data-set.png)
2. Skopiuj i Wklej powitania po fragment okna toohello projekt-1. We fragmencie JSON hello, tworzysz zestawu danych o nazwie **AzureBlobInput** reprezentujący dane wejściowe dla działania w potoku hello. Ponadto należy określić czy danych wejściowych hello znajduje się w kontenerze obiektów blob hello o nazwie **adfgetstarted** i hello folder o nazwie **inputdata**.

    ```JSON
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
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
    Witaj Poniższa tabela zawiera opisy właściwości JSON hello używane we fragmencie hello:

   | Właściwość | Opis |
   |:--- |:--- |
   | type |Właściwość type Hello ustawiono zbyt**AzureBlob** ponieważ danych znajduje się w magazynie obiektów blob platformy Azure. |
   | linkedServiceName |Odwołuje się toohello **AzureStorageLinkedService** utworzony wcześniej. |
   | folderPath | Określa obiekt blob hello **kontenera** i hello **folderu** zawiera obiekty BLOB wejściowego. | 
   | fileName |Ta właściwość jest opcjonalna. W przypadku pominięcia tej właściwości, pobierane są wszystkie pliki hello z hello folderPath. W tym samouczku tylko hello **input.log** jest przetwarzany. |
   | type |pliki dziennika Hello są w formacie tekstowym, więc używamy **TextFormat**. |
   | columnDelimiter |kolumn w plikach dziennika hello są rozdzielane **przecinka (`,`)** |
   | frequency/interval |częstotliwość ustawiona zbyt**miesiąca** i interwał **1**, co oznacza, że hello wejściowych wycinków dostępnych co miesiąc. |
   | external | Ta właściwość jest ustawiona zbyt**true** czy hello danych wejściowych nie jest generowany przez tego potoku. W tym samouczku hello input.log plik nie jest generowany przez tego potoku, możemy ustawić hello tootrue właściwości. |

    Aby uzyskać więcej informacji o tych właściwościach JSON, zobacz [artykuł dotyczący łącznika obiektu blob platformy Azure](data-factory-azure-blob-connector.md#dataset-properties).
3. Kliknij przycisk **Wdróż** polecenie hello paska toodeploy hello nowo utworzony w zestawie danych. Zestaw danych hello w hello widok drzewa po lewej stronie powitania powinna zostać wyświetlona.

### <a name="create-output-dataset"></a>Tworzenie wyjściowego zestawu danych
Można teraz utworzyć hello wyjściowego zestawu danych toorepresent hello danych wyjściowych danych przechowywanych w hello magazynu obiektów Blob platformy Azure.

1. W hello **Edytor fabryki danych**, kliknij przycisk **... Więcej** na pasku poleceń powitania kliknij **nowy zestaw danych**i wybierz **magazynu obiektów Blob Azure**.  
2. Skopiuj i Wklej powitania po fragment okna toohello projekt-1. We fragmencie JSON hello, tworzysz zestawu danych o nazwie **AzureBlobOutput**i określając hello struktury danych hello jest generowany przez hello skryptu Hive. Ponadto należy określić czy hello wyniki są przechowywane w kontenerze obiektów blob hello o nazwie **adfgetstarted** i hello folder o nazwie **partitioneddata**. Witaj **dostępności** sekcja określa, że wyjściowy zestaw danych hello jest tworzony co miesiąc.

    ```JSON
    {
      "name": "AzureBlobOutput",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
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
    Zobacz **utworzyć zestaw danych wejściowych hello** sekcji, aby uzyskać opis tych właściwości. Nie należy ustawiać właściwości zewnętrznych hello na wyjściowy zestaw danych, zgodnie z zestawu danych hello jest generowany przez hello usługi fabryka danych.
3. Kliknij przycisk **Wdróż** polecenie hello paska toodeploy hello nowo utworzony w zestawie danych.
4. Sprawdź, czy pomyślnie utworzono ten zestaw danych hello.

    ![Widok drzewa z połączonymi usługami](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-data-set.png)

## <a name="create-pipeline"></a>Tworzenie potoku
W tym kroku opisano tworzenie pierwszego potoku za pomocą działania **HDInsightHive**. Wejściowy jest dostępny co miesiąc (częstotliwość: miesiąc, interwał: 1), wycinek danych wyjściowych jest tworzony co miesiąc, a właściwość harmonogramu hello działania hello jest ustawić toomonthly. Ustawienia Hello hello wyjściowego zestawu danych i harmonogram działania hello muszą być zgodne. Wyjściowy zestaw danych jest obecnie, jakie dysków hello harmonogramu, dlatego należy utworzyć wyjściowy zestaw danych, nawet wtedy, gdy działanie hello nie generuje żadnego wyniku. Jeśli działanie hello nie przyjmuje żadnych danych, możesz pominąć tworzenie zestawu danych wejściowych hello. na końcu hello w tej sekcji opisano Hello właściwości używane w hello następującego formatu JSON.

1. W hello **Edytor fabryki danych**, kliknij przycisk **wielokropek (...) Więcej poleceń** , a następnie kliknij przycisk **nowy potok**.

    ![Przycisk nowy potok](./media/data-factory-build-your-first-pipeline-using-editor/new-pipeline-button.png)
2. Skopiuj i Wklej powitania po fragment okna toohello projekt-1.

   > [!IMPORTANT]
   > Zastąp **storageaccountname** hello nazwą konta magazynu w hello JSON.
   >
   >

    ```JSON
    {
        "name": "MyFirstPipeline",
        "properties": {
            "description": "My first Azure Data Factory pipeline",
            "activities": [
                {
                    "type": "HDInsightHive",
                    "typeProperties": {
                        "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                        "scriptLinkedService": "AzureStorageLinkedService",
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
            "start": "2017-07-01T00:00:00Z",
            "end": "2017-07-02T00:00:00Z",
            "isPaused": false
        }
    }
    ```

    We fragmencie JSON hello tworzysz potok, który składa się z jednego działania używającej tooprocess Hive danych w klastrze usługi HDInsight.

    plik skryptu Hive Hello, **partitionweblogs.hql**, są przechowywane w hello kontem magazynu platformy Azure (określonego przez element scriptLinkedService hello, nazywany **AzureStorageLinkedService**) i w  **skrypt** folderu w kontenerze hello **adfgetstarted**.

    Witaj **definiuje** sekcja jest używane toospecify hello środowiska uruchomieniowego ustawień, które są przekazywane skryptu hive toohello jako wartości konfiguracji gałęzi (np. ${hiveconf: inputtable}, {hiveconf:partitionedtable} $).

    Witaj **start** i **zakończenia** hello aktywny okres potoku hello określa właściwości hello potoku.

    W działaniu hello JSON, możesz określić, tego skryptu Hive hello zostanie uruchomiona na określony przez hello obliczeń hello **linkedServiceName** — **HDInsightOnDemandLinkedService**.

   > [!NOTE]
   > Zobacz sekcję "JSON potoku" w [potoki i działań w fabryce danych Azure](data-factory-create-pipelines.md) szczegółowe informacje na temat właściwości JSON używane w przykładzie hello.
   >
   >
3. Potwierdź hello następujące czynności:

   1. **Input.log** plik istnieje w hello **inputdata** folderu hello **adfgetstarted** kontenera w hello magazynu obiektów blob platformy Azure
   2. **partitionweblogs.hql** plik istnieje w hello **skryptu** folderu hello **adfgetstarted** kontenera w hello magazynu obiektów blob platformy Azure. Wstępny pełny hello etapami hello [— samouczek Przegląd](data-factory-build-your-first-pipeline.md) Jeśli nie widzisz tych plików.
   3. Upewnij się, że zastąpione **storageaccountname** hello nazwą konta magazynu w hello potoku JSON.
4. Kliknij przycisk **Wdróż** na pasku toodeploy hello potoku poleceń hello. Ponieważ hello **start** i **zakończenia** czasy są ustawiane w przeszłości hello i **isPaused** jest zestaw toofalse, potoku hello (działania w potoku hello) uruchamia natychmiast po wdrożeniu.
5. Upewnij się, że potoku hello w widoku drzewa hello jest wyświetlany.

    ![Widok drzewa z potokiem](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-pipeline.png)
6. Gratulacje! Udało Ci się utworzyć pierwszy potok!

## <a name="monitor-pipeline"></a>Monitorowanie potoku
### <a name="monitor-pipeline-using-diagram-view"></a>Monitorowanie potoku przy użyciu widoku diagramu
1. Kliknij przycisk **X** tooclose Edytor fabryki danych bloków toonavigate kopii toohello bloku fabryki danych i kliknij przycisk **Diagram**.

    ![Kafelek Diagram](./media/data-factory-build-your-first-pipeline-using-editor/diagram-tile.png)
2. W widoku diagramu hello zapoznać się z omówieniem potoki hello i zestawów danych użytych w tym samouczku.

    ![Widok diagramu](./media/data-factory-build-your-first-pipeline-using-editor/diagram-view-2.png)
3. tooview wszystkie działania w potoku hello, kliknij prawym przyciskiem myszy potoku w hello diagram i kliknij przycisk Otwórz potoku.

    ![Menu Otwórz potok](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-menu.png)
4. Upewnij się, że widoczny hello HDInsightHive działania w potoku hello.

    ![Widok Otwórz potok](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-view.png)

    toonavigate kopii toohello poprzedni widok, kliknij przycisk **fabryki danych** hello nawigacją menu u góry hello.
5. W hello **widoku diagramu**, kliknij dwukrotnie plik zestawu danych hello **AzureBlobInput**. Upewnij się, że wycinek hello jest w **gotowe** stanu. Może potrwać kilka minut dla tooshow wycinka hello w stanie gotowe. Jeśli nie następuje po poczekaj przez pewien czas, zobacz, jeśli masz pliku wejściowego hello (input.log) umieszczone w prawo kontenera hello (adfgetstarted) i folderu (inputdata).

   ![Wycinek danych wejściowych w stanie gotowości](./media/data-factory-build-your-first-pipeline-using-editor/input-slice-ready.png)
6. Kliknij przycisk **X** tooclose **AzureBlobInput** bloku.
7. W hello **widoku diagramu**, kliknij dwukrotnie plik zestawu danych hello **AzureBlobOutput**. Użytkownik widzi tego hello wycinek, który jest obecnie przetwarzane.

   ![Zestaw danych](./media/data-factory-build-your-first-pipeline-using-editor/dataset-blade.png)
8. Po zakończeniu przetwarzania zostanie wyświetlony wycinek hello **gotowe** stanu.

   ![Zestaw danych](./media/data-factory-build-your-first-pipeline-using-editor/dataset-slice-ready.png)  

   > [!IMPORTANT]
   > Tworzenie klastra usługi HDInsight na żądanie zwykle trwa trochę czasu (około 20 minut). W związku z tym spodziewać się potoku hello trwać zbyt **około 30 minut** tooprocess hello wycinka.
   >
   >

9. Gdy wycinek hello jest **gotowe** stanu, należy sprawdzić hello **partitioneddata** folderu w hello **adfgetstarted** kontenera w magazynie obiektów blob na powitania dane wyjściowe.  

   ![Dane wyjściowe](./media/data-factory-build-your-first-pipeline-using-editor/three-ouptut-files.png)
10. Kliknij przycisk Szczegóły toosee wycinka hello o nim w **wycinka danych** bloku.

   ![Szczegóły wycinka danych](./media/data-factory-build-your-first-pipeline-using-editor/data-slice-details.png)  
11. Kliknij przycisk uruchamiania w hello działania **listy odbywa się działanie** toosee szczegółowe informacje o działaniu można uruchomić (działanie gałęzi w naszym scenariuszu) w **szczegóły uruchomienia działania** okna.   

   ![Szczegóły uruchamiania działania](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-blade.png)    

   Z plików dziennika hello widać, zapytanie Hive hello, które zostało wykonane i informacje o stanie. Dzienniki te są przydatne w przypadku rozwiązywania różnych problemów.
   Więcej szczegółowych informacji znajduje się w artykule [Monitor and manage pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) (Monitorowanie potoków i zarządzanie nimi przy użyciu bloków w witrynie Azure Portal).

> [!IMPORTANT]
> Plik wejściowy Hello zostaje usunięta, gdy hello wycinek jest przetwarzany pomyślnie. W związku z tym hello plik wejściowy (input.log) toohello inputdata folder kontenera adfgetstarted hello przekazywania wycinek hello toorerun lub Witaj ponownie samouczek.
>
>

### <a name="monitor-pipeline-using-monitor--manage-app"></a>Monitorowanie potoku przy użyciu aplikacji Monitorowanie i zarządzanie
Można również użyć monitora i zarządzanie toomonitor aplikacji z potoków. Szczegółowe informacje dotyczące korzystania z aplikacji znajdują się w artykule [Monitor and manage Azure Data Factory pipelines using Monitoring and Management App](data-factory-monitor-manage-app.md) (Monitorowanie potoków usługi Azure Data Factory oraz zarządzanie nimi za pomocą aplikacji Monitorowanie i zarządzanie).

1. Kliknij przycisk **Monitor & Zarządzaj** kafelka na stronie głównej hello w fabryce danych.

    ![Kafelek Monitorowanie i zarządzanie](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-tile.png)
2. Powinna zostać wyświetlona **aplikacja Monitorowanie i zarządzanie**. Zmień hello **godzina rozpoczęcia** i **czas zakończenia** toomatch start i end razy potoku sieci i kliknij **Zastosuj**.

    ![Aplikacja Monitorowanie i zarządzanie](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-app.png)
3. Wybierz przedział działania w hello **okien działania** listy toosee uzyskać szczegółowe informacje o nim.

    ![Szczegóły okna działania](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-details.png)

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

## <a name="see-also"></a>Zobacz też
| Temat | Opis |
|:--- |:--- |
| [Potoki](data-factory-create-pipelines.md) |Ten artykuł pomaga w zrozumieniu potoki i działań w fabryce danych Azure i w jaki sposób toouse ich tooconstruct end-to-end danymi przepływy pracy dla Twojego scenariusza lub firmy. |
| [Zestawy danych](data-factory-create-datasets.md) |Ten artykuł ułatwia zapoznanie się z zestawami danych w usłudze Azure Data Factory. |
| [Planowanie i wykonywanie](data-factory-scheduling-and-execution.md) |W tym artykule opisano aspekty planowania i wykonywania hello modelu aplikacji fabryki danych Azure. |
| [Monitorowanie potoków i zarządzanie nimi za pomocą aplikacji do monitorowania](data-factory-monitor-manage-app.md) |W tym artykule opisano sposób toomonitor, zarządzania i debugowania potoki przy użyciu hello monitorowanie & aplikacji do zarządzania. |
