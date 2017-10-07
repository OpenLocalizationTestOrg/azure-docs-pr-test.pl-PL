---
title: 'Samouczek: Tworzenie danych toocopy potoku fabryki danych Azure (Azure portal) | Dokumentacja firmy Microsoft'
description: "W tym samouczku toocreate portalu Azure potoku fabryki danych Azure używających toocopy działanie kopiowania danych z bazy danych Azure SQL tooan magazynu obiektów blob platformy Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: d9317652-0170-4fd3-b9b2-37711272162b
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: fadd840fe9a15cd8831cdb25dccbd10ac42fa161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-use-azure-portal-toocreate-a-data-factory-pipeline-toocopy-data"></a>Samouczek: Użyj toocreate portalu Azure danych toocopy potoku fabryki danych 
> [!div class="op_single_selector"]
> * [Przegląd i wymagania wstępne](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Kreator kopiowania](data-factory-copy-data-wizard-tutorial.md)
> * [Witryna Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Program Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [Program PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Szablon usługi Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [Interfejs API REST](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [Interfejs API .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

W tym artykule dowiesz się, jak toouse [portalu Azure](https://portal.azure.com) toocreate fabryki danych z potok, który kopiuje dane z bazy danych Azure SQL tooan magazynu obiektów blob platformy Azure. Jeśli nowy tooAzure fabryki danych, zapoznaj się z artykułem hello [tooAzure wprowadzenie fabryki danych](data-factory-introduction.md) artykuł przed wykonaniem tego samouczka.   

W tym samouczku opisano tworzenie potoku z jednym działaniem (Działanie kopiowania). działanie kopiowania Hello kopiuje dane z magazynu danych obsługiwanych ujścia magazynu tooa obsługiwane dane. Aby zapoznać się z listą magazynów danych obsługiwanych jako źródła i ujścia, zobacz [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats). działanie Hello jest obsługiwany przez ogólnie dostępna usługa, która można skopiować dane między różnych magazynach danych w sposób bezpieczny, niezawodny i skalowalności. Aby uzyskać więcej informacji na temat hello działanie kopiowania, zobacz [działań przepływu danych](data-factory-data-movement-activities.md).

Potok może obejmować więcej niż jedno działanie. I tworzenia łańcucha dwa działania (Uruchom jedno działanie po drugim), ustawiając hello wyjściowy zestaw danych z jednego działania jako hello wejściowy zestaw danych z hello innych działań. Aby uzyskać więcej informacji, zobacz sekcję dotyczącą [wielu działań w potoku](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline). 

> [!NOTE] 
> Witaj potoku danych w tym samouczku kopiuje dane z magazynu danych źródła danych magazynu tooa docelowego. Samouczek na temat danych tootransform przy użyciu fabryki danych Azure, zobacz [samouczek: Tworzenie danych tootransform potoku, przy użyciu klastra usługi Hadoop](data-factory-build-your-first-pipeline.md).

## <a name="prerequisites"></a>Wymagania wstępne
Wymagania wstępne wymienione w hello ukończyć [wymagania wstępne dotyczące samouczka](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) artykuł przed wykonaniem tego samouczka.

## <a name="steps"></a>Kroki
Poniżej przedstawiono kroki hello, które należy wykonać w ramach tego samouczka:

1. Utworzenie **fabryki danych** na platformie Azure. W tym kroku opisano tworzenie fabryki danych o nazwie ADFTutorialDataFactory. 
2. Utwórz **połączone usługi** w fabryce danych hello. Ten krok polega na utworzeniu dwóch połączonych usług: Azure Storage i Azure SQL Database. 
    
    Witaj AzureStorageLinkedService łączy fabrykę danych toohello konta magazynu platformy Azure. Utworzono kontener i przekazany w ramach konta magazynu danych toothis [wymagania wstępne](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

    AzureSqlLinkedService łączy fabrykę danych toohello bazy danych Azure SQL. dane Hello, który jest skopiowany z magazynu obiektów blob hello są przechowywane w tej bazie danych. W ramach [wymagań wstępnych](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) w tej bazie danych została utworzona tabela SQL.   
3. Utwórz dane wejściowe i wyjściowe **zestawów danych** w fabryce danych hello.  
    
    Hello Azure połączoną usługą magazynu określa parametry połączenia hello, która używa usługi fabryka danych w czasie wykonywania tooconnect tooyour kontem magazynu platformy Azure. I zestawu danych wejściowych obiektu blob hello określa hello kontenera i folderu hello, który zawiera hello danych wejściowych.  

    Podobnie hello usługi baza danych SQL Azure połączone określa hello parametry połączenia, które korzysta z usługi fabryka danych w czasie wykonywania tooconnect tooyour — bazy danych Azure SQL. I tabeli hello hello bazy danych toowhich hello danych z magazynu obiektów blob hello jest kopiowany określa hello danych wyjściowych SQL tabeli dataset.
4. Utwórz **potoku** w fabryce danych hello. W tym kroku jest tworzony potok za pomocą działania kopiowania.   
    
    działanie kopiowania Hello kopiuje dane z obiektu blob w tabeli tooa magazynu obiektów blob platformy Azure hello w bazie danych Azure SQL hello. Działanie kopiowania służy w potoku danych toocopy z dowolnego miejsca docelowego tooany obsługiwane obsługiwanej źródłowej. Listę obsługiwanych magazynów danych można znaleźć w artykule [Działania związane z przenoszeniem danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats). 
5. Monitor hello potoku. W tym kroku zostanie **monitor** hello wycinków wejściowych i wyjściowych zestawów danych przy użyciu portalu Azure. 

## <a name="create-data-factory"></a>Tworzenie fabryki danych
> [!IMPORTANT]
> Pełne [wymagania wstępne dotyczące samouczka hello](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) Jeśli jeszcze tego nie zrobiono.   

Fabryka danych może obejmować jeden lub wiele potoków. Potok może obejmować jedno lub wiele działań. Na przykład toocopy działanie kopiowania danych z magazynu danych docelowy tooa źródłowego i HDInsight Hive działania toorun tootransform skryptu Hive wejściowe dane wyjściowe tooproduct danych. Zacznijmy od utworzenia hello fabryki danych w tym kroku.

1. Po zalogowaniu toohello [portalu Azure](https://portal.azure.com/), kliknij przycisk **nowy** w menu po lewej stronie powitania kliknij **dane i analiza**i kliknij przycisk **fabryki danych**. 
   
   ![Nowy-> Fabryka danych](./media/data-factory-copy-activity-tutorial-using-azure-portal/NewDataFactoryMenu.png)    
2. W hello **nowa fabryka danych** bloku:
   
   1. Wprowadź **ADFTutorialDataFactory** dla hello **nazwa**. 
      
         ![Blok Nowa fabryka danych](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-new-data-factory.png)
      
       Nazwa fabryki danych Azure hello Hello musi być **unikatowych**. Jeśli zostanie wyświetlony następujący błąd hello, Zmień nazwę hello hello fabryki danych (na przykład yournameADFTutorialDataFactory) i spróbuj ponownie utworzyć. Artykuł [Data Factory — Naming Rules](data-factory-naming-rules.md) (Fabryka danych — zasady nazewnictwa) zawiera zasady nazewnictwa artefaktów usługi Fabryka danych.
      
           Data factory name “ADFTutorialDataFactory” is not available  
      
       ![Nazwa fabryki danych jest niedostępna](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-data-factory-not-available.png)
   2. Wybierz platformy Azure **subskrypcji** w której ma zostać hello toocreate usługi fabryka danych. 
   3. Dla hello **grupy zasobów**, wykonaj jedną z hello następujące kroki:
      
      - Wybierz **Użyj istniejącego**, a następnie wybierz istniejącą grupę zasobów z listy rozwijanej hello. 
      - Wybierz **Utwórz nowy**i wprowadź nazwę hello grupy zasobów.   
         
          Niektóre kroki hello w tym samouczku Załóżmy, że nazwa hello: **ADFTutorialResourceGroup** hello grupy zasobów. toolearn temat grup zasobów, zobacz [toomanage przy użyciu zasobów grup zasobów platformy Azure](../azure-resource-manager/resource-group-overview.md).  
   4. Wybierz hello **lokalizacji** hello fabryki danych. Tylko regiony obsługiwane przez hello usługi fabryka danych są wyświetlane na liście rozwijanej hello.
   5. Wybierz **toodashboard numeru Pin**.     
   6. Kliknij przycisk **Utwórz**.
      
      > [!IMPORTANT]
      > toocreate wystąpienia fabryki danych, musi być członkiem hello [współautora fabryki danych](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) roli na poziomie grupy zasobów subskrypcji hello.
      > 
      > Nazwa fabryki danych hello Hello mogą być zarejestrowana jako nazwa DNS w przyszłości hello i dlatego stać się publicznie widoczna.                
      > 
      > 
3. Na pulpicie nawigacyjnym hello, zobacz następujące hello Kafelek o stanie: **fabryki danych wdrażanie**. 

    ![kafelek Wdrażanie fabryki danych](media/data-factory-copy-activity-tutorial-using-azure-portal/deploying-data-factory.png)
4. Po zakończeniu tworzenia hello Zobacz hello **fabryki danych** bloku, jak pokazano w obrazie hello.
   
   ![Strona główna fabryki danych](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-data-factory-home-page.png)

## <a name="create-linked-services"></a>Tworzenie połączonych usług
Połączone usługi są tworzone w toolink fabryki danych dane są przechowywane i obliczeniowe fabryki danych toohello usług. W tym samouczku nie przedstawiono korzystania z żadnych usług obliczeniowych, takich jak Azure HDInsight czy Azure Data Lake Analytics. Zostają użyte dwa magazyny danych typu Azure Storage (źródło) i Azure SQL Database (lokalizacja docelowa). 

W związku z tym tworzy się dwie połączone usługi o nazwie AzureStorageLinkedService i AzureSqlLinkedService typu: AzureStorage i AzureSqlDatabase.  

Witaj AzureStorageLinkedService łączy fabrykę danych toohello konta magazynu platformy Azure. To konto magazynu jest hello jedną w którym utworzono kontener i hello dane przekazane jako część [wymagania wstępne](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

AzureSqlLinkedService łączy fabrykę danych toohello bazy danych Azure SQL. dane Hello, który jest skopiowany z magazynu obiektów blob hello są przechowywane w tej bazie danych. Utworzono hello pustych elementów tabeli w tej bazie danych jako część [wymagania wstępne](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).  

### <a name="create-azure-storage-linked-service"></a>Tworzenie połączonej usługi Azure Storage
W tym kroku możesz połączyć fabrykę danych tooyour konta magazynu platformy Azure. W tej sekcji można określić nazwę hello i klucza konta magazynu Azure.  

1. W hello **fabryki danych** bloku, kliknij przycisk **tworzenie i wdrażanie** kafelka.
   
   ![Kafelek Utwórz i wdróż](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-author-deploy-tile.png) 
2. Zobacz hello **Edytor fabryki danych** pokazane na powitania po obrazu: 

    ![Edytor fabryki danych](./media/data-factory-copy-activity-tutorial-using-azure-portal/data-factory-editor.png)
3. W edytorze powitania kliknij **nowy magazyn danych** przycisk na powitania narzędzi i wybierz **magazynu Azure** z menu rozwijanego hello. Powinny pojawić się hello JSON szablonu do tworzenia w prawym okienku hello Azure połączoną usługą magazynu. 
   
    ![Przycisk Nowy magazyn danych w edytorze](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-newdatastore-button.png)    
3. Zastąp `<accountname>` i `<accountkey>` z hello konta nazwy i konta wartości klucza dla konta magazynu Azure. 
   
    ![Skrypt JSON w edytorze usługi Blob Storage](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-blob-storage-json.png)    
4. Kliknij przycisk **Wdróż** na powitania narzędzi. Powinny pojawić się hello wdrożone **AzureStorageLinkedService** w drzewie hello teraz wyświetlić. 
   
    ![Przycisk Wdróż w edytorze usługi Blob Storage](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-blob-storage-deploy.png)

    Aby uzyskać więcej informacji o właściwościach JSON w definicji usługi hello połączone, zobacz [łącznika usługi Azure Blob Storage](data-factory-azure-blob-connector.md#linked-service-properties) artykułu.

### <a name="create-a-linked-service-for-hello-azure-sql-database"></a>Tworzenie połączonej usługi dla hello bazy danych SQL Azure
W tym kroku możesz połączyć fabrykę danych tooyour bazy danych Azure SQL. W tej sekcji można określić nazwy serwera Azure SQL hello, nazwa bazy danych, nazwę użytkownika i hasło użytkownika. 

1. W hello **Edytor fabryki danych**, kliknij przycisk **nowy magazyn danych** przycisk na powitania narzędzi i wybierz **bazy danych SQL Azure** z menu rozwijanego hello. Witaj JSON szablonu tworzenia hello Azure połączoną usługą SQL w okienku po prawej stronie powitania powinna zostać wyświetlona.
2. Zastąp parametry `<servername>`, `<databasename>`, `<username>@<servername>` i `<password>`, wpisując nazwy serwera SQL Azure, bazy danych i konta użytkownika oraz hasło. 
3. Kliknij przycisk **Wdróż** hello toocreate narzędzi i wdrożyć hello **AzureSqlLinkedService**.
4. Upewnij się, że widoczny **AzureSqlLinkedService** w widoku drzewa hello w obszarze **połączone usługi**.  

    Aby uzyskać więcej informacji o tych właściwościach JSON, zobacz artykuł dotyczący [łącznika usługi Azure SQL Database](data-factory-azure-sql-connector.md#linked-service-properties).

## <a name="create-datasets"></a>Tworzenie zestawów danych
W poprzednim kroku hello utworzono toolink połączone usługi konta magazynu Azure i fabryki danych tooyour bazy danych Azure SQL. W tym kroku należy zdefiniować dwa zestawy danych o nazwie InputDataset i OutputDataset reprezentujące danych wejściowych i wyjściowych danych przechowywanych w magazynach danych hello odwołuje się AzureStorageLinkedService i AzureSqlLinkedService odpowiednio.

Hello Azure połączoną usługą magazynu określa parametry połączenia hello, która używa usługi fabryka danych w czasie wykonywania tooconnect tooyour kontem magazynu platformy Azure. I zestawu danych wejściowych obiektu blob hello (InputDataset) określa hello kontenera i folderu hello, który zawiera hello danych wejściowych.  

Podobnie hello usługi baza danych SQL Azure połączone określa hello parametry połączenia, które korzysta z usługi fabryka danych w czasie wykonywania tooconnect tooyour — bazy danych Azure SQL. I hello danych wyjściowych SQL tabeli dataset (OututDataset) określa hello tabeli w hello bazy danych toowhich powitalne dane z magazynu obiektów blob hello są kopiowane. 

### <a name="create-input-dataset"></a>Tworzenie wejściowego zestawu danych
W tym kroku utworzysz zestaw danych o nazwie InputDataset, który wskazuje plik obiektu blob tooa (emp.txt) w folderze głównym hello kontenera obiektów blob (adftutorial) w hello reprezentowany przez hello AzureStorageLinkedService połączone usługi Magazyn Azure. Brak określić wartość dla nazwy pliku hello (lub Pomiń je), danych z wszystkich obiektów blob w folderze wejściowych hello są skopiowanych toohello docelowego. W tym samouczku należy określić wartość dla hello fileName. 

1. W hello **edytor** dla hello fabryki danych, kliknij przycisk **... Więcej**, kliknij przycisk **nowy zestaw danych**i kliknij przycisk **magazynu obiektów Blob Azure** z menu rozwijanego hello. 
   
    ![Menu Nowy zestaw danych](./media/data-factory-copy-activity-tutorial-using-azure-portal/new-dataset-menu.png)
2. Zastąp JSON w okienku po prawej stronie powitania powitania po fragment kodu JSON: 
   
    ```json
    {
      "name": "InputDataset",
      "properties": {
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
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
          "folderPath": "adftutorial/",
          "fileName": "emp.txt",
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "external": true,
        "availability": {
          "frequency": "Hour",
          "interval": 1
        }
      }
    }
    ```   

    Witaj Poniższa tabela zawiera opisy właściwości JSON hello używane we fragmencie hello:

    | Właściwość | Opis |
    |:--- |:--- |
    | type | Właściwość type Hello ustawiono zbyt**AzureBlob** ponieważ danych znajduje się w magazynie obiektów blob platformy Azure. |
    | linkedServiceName | Odwołuje się toohello **AzureStorageLinkedService** utworzony wcześniej. |
    | folderPath | Określa obiekt blob hello **kontenera** i hello **folderu** zawiera obiekty BLOB wejściowego. W tym samouczku adftutorial jest hello kontenera obiektów blob i hello folderu głównego. | 
    | fileName | Ta właściwość jest opcjonalna. W przypadku pominięcia tej właściwości, pobierane są wszystkie pliki z hello folderPath. W tym samouczku **emp.txt** określona dla hello nazwę pliku, tak aby plik zostaje pobrana do przetwarzania. |
    | format -> type |Plik wejściowy Hello jest w formacie tekstowym hello, więc używamy **TextFormat**. |
    | columnDelimiter | Witaj kolumn w pliku wejściowym hello są rozdzielane **przecinka (`,`)**. |
    | frequency/interval | częstotliwość Hello ustawiono zbyt**godzina** i interwał jest ustawiany za**1**, co oznacza, że hello wejściowych dostępnych wycinków **co godzinę**. Innymi słowy, hello usługi fabryka danych sprawdza dane wejściowe co godzinę w folderze głównym hello kontenera obiektów blob (**adftutorial**) określone. Wyszukuje hello danych w ramach hello potoku rozpoczęcia i zakończenia godzin, nie przed lub po tych godzinach.  |
    | external | Ta właściwość jest ustawiona zbyt**true** czy hello danych nie jest generowany przez tego potoku. Witaj danych wejściowych w tym samouczku jest hello emp.txt pliku, który nie jest generowany w tym potoku, możemy ustawić tootrue tej właściwości. |

    Aby uzyskać więcej informacji o tych właściwościach JSON, zobacz [artykuł dotyczący łącznika obiektu blob platformy Azure](data-factory-azure-blob-connector.md#dataset-properties).      
3. Kliknij przycisk **Wdróż** hello toocreate narzędzi i wdrożyć hello **InputDataset** zestawu danych. Upewnij się, że widoczny hello **InputDataset** w widoku drzewa hello.

### <a name="create-output-dataset"></a>Tworzenie wyjściowego zestawu danych
Hello usługi baza danych SQL Azure połączone określa hello parametry połączenia, które korzysta z usługi fabryka danych w czasie wykonywania tooconnect tooyour — bazy danych Azure SQL. Utwórz w tym kroku Hello danych wyjściowych SQL tabeli dataset (OututDataset) określa, że tabela hello hello bazy danych toowhich hello danych z magazynu obiektów blob hello jest kopiowany.

1. W hello **edytor** dla hello fabryki danych, kliknij przycisk **... Więcej**, kliknij przycisk **nowy zestaw danych**i kliknij przycisk **Azure SQL** z menu rozwijanego hello. 
2. Zastąp JSON w okienku po prawej stronie powitania powitania po fragment kodu JSON:

    ```json   
    {
      "name": "OutputDataset",
      "properties": {
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
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
          "tableName": "emp"
        },
        "availability": {
          "frequency": "Hour",
          "interval": 1
        }
      }
    }
    ```     

    Witaj Poniższa tabela zawiera opisy właściwości JSON hello używane we fragmencie hello:

    | Właściwość | Opis |
    |:--- |:--- |
    | type | Właściwość type Hello ustawiono zbyt**AzureSqlTable** , ponieważ dane są kopiowane tooa tabeli w bazie danych Azure SQL. |
    | linkedServiceName | Odwołuje się toohello **AzureSqlLinkedService** utworzony wcześniej. |
    | tableName | Określony hello **tabeli** toowhich hello dane są kopiowane. | 
    | frequency/interval | Witaj częstotliwość ustawiono zbyt**godzina** i interwał **1**, co oznacza, że wycinki danych wyjściowych hello są produkowane **co godzinę** między hello potoku rozpoczęcia i zakończenia godzin przed nie lub Po tych godzinach.  |

    Istnieją trzy kolumny — **identyfikator**, **imię**, i **nazwisko** — Witaj pustych elementów tabeli w bazie danych hello. Identyfikator jest kolumny tożsamości, więc musisz tylko toospecify **imię** i **nazwisko** tutaj.

    Aby uzyskać więcej informacji o tych właściwościach JSON, zobacz [artykuł dotyczący łącznika usługi Azure SQL](data-factory-azure-sql-connector.md#dataset-properties).
3. Kliknij przycisk **Wdróż** hello toocreate narzędzi i wdrożyć hello **OutputDataset** zestawu danych. Upewnij się, że widoczny hello **OutputDataset** w widoku drzewa hello w obszarze **zestawów danych**. 

## <a name="create-pipeline"></a>Tworzenie potoku
W tym kroku opisano tworzenie potoku za pomocą **działania kopiowania**, w którym parametr **InputDataset** jest używany jako dane wejściowe, a parametr **OutputDataset** jako dane wyjściowe.

Wyjściowy zestaw danych jest obecnie, jakie dysków hello harmonogramu. W tym samouczku wyjściowy zestaw danych jest skonfigurowane tooproduce wycinek godzinę. potok Hello ma czas rozpoczęcia i godzina zakończenia, będące w ciągu jednego dnia od siebie, który wynosi 24 godziny. W związku z tym 24 wycinków wyjściowy zestaw danych są produkowane przez hello potoku. 

1. W hello **edytor** dla hello fabryki danych, kliknij przycisk **... Więcej** i **Nowy potok**. Alternatywnie możesz kliknąć prawym przyciskiem myszy **potoki** w widoku drzewa hello i kliknij **nowy potok**.
2. Zastąp JSON w okienku po prawej stronie powitania powitania po fragment kodu JSON: 

    ```json   
    {
      "name": "ADFTutorialPipeline",
      "properties": {
        "description": "Copy data from a blob tooAzure SQL table",
        "activities": [
          {
            "name": "CopyFromBlobToSQL",
            "type": "Copy",
            "inputs": [
              {
                "name": "InputDataset"
              }
            ],
            "outputs": [
              {
                "name": "OutputDataset"
              }
            ],
            "typeProperties": {
              "source": {
                "type": "BlobSource"
              },
              "sink": {
                "type": "SqlSink",
                "writeBatchSize": 10000,
                "writeBatchTimeout": "60:00:00"
              }
            },
            "Policy": {
              "concurrency": 1,
              "executionPriorityOrder": "NewestFirst",
              "retry": 0,
              "timeout": "01:00:00"
            }
          }
        ],
        "start": "2017-05-11T00:00:00Z",
        "end": "2017-05-12T00:00:00Z"
      }
    } 
    ```   
    
    Należy zwrócić uwagę hello następujące punkty:
   
    - W sekcji działania hello jest tylko jedno działanie którego **typu** ustawiono zbyt**kopiowania**. Aby uzyskać więcej informacji o działaniu kopiowania hello, zobacz [działań przepływu danych](data-factory-data-movement-activities.md). W rozwiązaniach usługi Data Factory można również użyć [działań dotyczących przekształcania danych](data-factory-data-transformation-activities.md).
    - Dane wejściowe dla działania hello jest ustawiony za**InputDataset** i danych wyjściowych dla działania hello jest ustawiony za**OutputDataset**. 
    - W hello **typeProperties** sekcji **BlobSource** jest określony jako typ źródła hello i **SqlSink** jest określony jako typ ujścia hello. Aby uzyskać pełną listę obsługiwanych przez działanie kopiowania hello jako źródła i wychwytywanie magazyny danych, zobacz [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats). toolearn jak przechowywać toouse określonych danych obsługiwane jako źródło/ujście, kliknij łącze hello hello tabeli.
    - Zarówno data/godzina rozpoczęcia, jak i data/godzina zakończenia muszą być w [formacie ISO](http://en.wikipedia.org/wiki/ISO_8601). Przykładowo: 2016-10-14T16:32:41Z. Witaj **zakończenia** czasu jest opcjonalne, ale możemy użyć w tym samouczku. Jeśli nie określisz wartości hello **zakończenia** właściwości, jest on obliczany jako "**start + 48 godzin**". potok hello toorun przez czas nieokreślony, określ **9999-09-09** jako wartość hello hello **zakończenia** właściwości.
     
    W hello poprzedzających przykład istnieją 24 wycinków danych, jak każdy wycinek danych jest tworzone co godzinę.

    Opisy właściwości JSON w definicji potoku znajdują się w artykule dotyczącym [tworzenia potoków](data-factory-create-pipelines.md). Opisy właściwości JSON w definicji działania kopiowania znajdują się w artykule dotyczącym [działań związanych z przenoszeniem danych](data-factory-data-movement-activities.md). Opisy właściwości JSON obsługiwanych przez BlobSource można znaleźć w [artykule dotyczącym łącznika usługi Azure Blob](data-factory-azure-blob-connector.md). Opisy właściwości JSON obsługiwanych przez SqlSink można znaleźć w artykule [dotyczącym łącznika usługi Azure SQL Database](data-factory-azure-sql-connector.md).
3. Kliknij przycisk **Wdróż** hello toocreate narzędzi i wdrożyć hello **ADFTutorialPipeline**. Upewnij się, że potoku hello w widoku drzewa hello jest wyświetlany. 
4. Teraz, zamknij hello **edytor** bloku, klikając **X**. Kliknij przycisk **X** ponownie hello toosee **fabryki danych** strony głównej hello **ADFTutorialDataFactory**.

**Gratulacje!** Pomyślnie utworzono fabryki danych Azure z potoku toocopy danych z bazy danych Azure SQL tooan magazynu obiektów blob platformy Azure. 


## <a name="monitor-pipeline"></a>Monitorowanie potoku
W tym kroku użyjesz hello Azure toomonitor portalu, co się dzieje w fabryce danych Azure.    

### <a name="monitor-pipeline-using-monitor--manage-app"></a>Monitorowanie potoku przy użyciu aplikacji Monitorowanie i zarządzanie
Witaj poniższej procedurze pokazano, jak toomonitor potoków w fabryce danych za pomocą aplikacji do monitorowania i Zarządzaj hello: 

1. Kliknij przycisk **Monitor & Zarządzaj** kafelka na stronie głównej hello w fabryce danych.
   
    ![Kafelek Monitorowanie i zarządzanie](./media/data-factory-copy-activity-tutorial-using-azure-portal/monitor-manage-tile.png) 
2. **Aplikacja Monitorowanie i zarządzanie** powinna zostać wyświetlona na osobnej karcie. 

    > [!NOTE]
    > Jeśli przeglądarka sieci web hello jest zablokowany na "Autoryzowanie...", wykonaj jedną z następujących hello: hello wyczyść **zablokować pliki cookie innych firm, a dane lokacji** pole wyboru (lub) utworzyć wyjątek **login.microsoftonline.com**, a następnie spróbuj ponownie tooopen hello aplikacji.

    ![Aplikacja Monitorowanie i zarządzanie](./media/data-factory-copy-activity-tutorial-using-azure-portal/monitor-and-manage-app.png)
3. Zmień hello **godzina rozpoczęcia** i **czas zakończenia** tooinclude start (2017-05-11) i zakończenia godzin (2017-05-12) potoku sieci i kliknij **Zastosuj**.     
3. Zobacz hello **okien działania** skojarzone z każdej godziny między potoku rozpoczęcia i zakończenia godzin na liście hello w środkowym okienku hello. 
4. toosee Szczegóły okna działania wybierz hello okno działania w hello **okien działania** listy. 
    ![Szczegóły okna działania](./media/data-factory-copy-activity-tutorial-using-azure-portal/activity-window-details.png)

    W Eksploratorze okna działania na powitania prawo, zostanie wyświetlony tego hello wycinków się bieżący czas UTC toohello (20:12:00) są przetwarzane (w kolor zielony). Hello wycinków 8-9 PM, PM 9 10, 10-11 PM, 23: 00 - 00: 00 nie zostały jeszcze przetworzone.

    Witaj **prób** sekcji w prawym okienku informacje na temat uruchamiania dla wycinka danych hello działania hello hello. Jeśli wystąpił błąd, zawiera szczegółowe informacje o błędzie hello. Na przykład hello dane wejściowe, folder lub kontener nie istnieje i hello wycinek przetwarzania kończy się niepowodzeniem, zostanie wyświetlony komunikat o błędzie z informacją o danym kontenerze hello lub folder nie istnieje.

    ![Próby uruchomienia działania](./media/data-factory-copy-activity-tutorial-using-azure-portal/activity-run-attempts.png) 
4. Uruchom **programu SQL Server Management Studio**, Połącz toohello bazy danych SQL Azure i sprawdź, czy wiersze hello są wstawiane toohello **pustych elementów** tabeli w bazie danych hello.
    
    ![wyniki zapytania sql](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-sql-query-results.png)

Szczegółowe informacje dotyczące korzystania z aplikacji znajdują się w artykule [Monitor and manage Azure Data Factory pipelines using Monitoring and Management App](data-factory-monitor-manage-app.md) (Monitorowanie potoków usługi Fabryka danych Azure oraz zarządzanie nimi za pomocą aplikacji Monitorowanie i zarządzanie).

### <a name="monitor-pipeline-using-diagram-view"></a>Monitorowanie potoku przy użyciu widoku diagramu
Można również potokach danych monitora przy użyciu widoku diagramu hello.  

1. W hello **fabryki danych** bloku, kliknij przycisk **Diagram**.
   
    ![Blok Fabryka danych — kafelek Diagram](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-datafactoryblade-diagramtile.png)
2. Powinny pojawić się toohello podobne diagram powitania po obrazu: 
   
    ![Widok diagramu](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-diagram-blade.png)  
5. W widoku diagramu hello, kliknij dwukrotnie **InputDataset** toosee wycinków hello zestawu danych.  
   
    ![Zestawy danych z wybranym zestawem InputDataset](./media/data-factory-copy-activity-tutorial-using-azure-portal/DataSetsWithInputDatasetFromBlobSelected.png)   
5. Kliknij przycisk **zobaczyć więcej** link toosee wszystkie fragmenty danych hello. Zostaną wyświetlone wycinki w zakresie 24 godzin od czasu rozpoczęcia do zakończenia potoku. 
   
    ![Wszystkie wycinki danych wejściowych](./media/data-factory-copy-activity-tutorial-using-azure-portal/all-input-slices.png)  
   
    Zwróć uwagę, że wszystkie tekst hello wycinków danych się bieżący czas UTC toohello **gotowe** ponieważ hello **emp.txt** plik istnieje cały czas hello w kontenerze obiektów blob hello: **adftutorial\input**. Hello wycinki dla przyszłych godzin hello nie są w stanie gotowe jeszcze. Upewnij się, że brak wycinków widoczne w hello **ostatnio nie powiodło się wycinków** sekcji u dołu hello.
6. Zamknij hello bloków, dopóki Zobacz hello diagram widoku (lub) przewijania toosee po lewej stronie powitania diagram wyświetlić. Następnie kliknij dwukrotnie pozycję **OutputDataset**. 
8. Kliknij przycisk **zobaczyć więcej** łącze na powitania **tabeli** bloku **OutputDataset** toosee wszystkie hello wycinków.

    ![blok Wycinki danych](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-dataslices-blade.png) 
9. Przenieś wszystkie tekst hello wycinków bieżący czas UTC toohello się powiadomienie z **do czasu wykonywania** Stan = > **w toku** ==> **gotowe** stanu. Witaj wycinków z ostatnich hello (przed bieżącym czasem) są przetwarzane z najnowszą toooldest domyślnie. Na przykład w przypadku hello bieżący czas UTC 8:12:00, wcześniejsze wycinek 18: 00 - 7 PM hello są przetwarzane hello wycinek dla 19: 00 - 8 PM. wycinek 20: 00 - 21: 00 Hello są przetwarzane na końcu hello interwału czasu hello domyślnie po 21: 00.  
10. Kliknij wycinek żadnych danych z listy hello i powinna zostać wyświetlona hello **wycinka danych** bloku. Element danych skojarzony z oknem działania jest nazywany wycinkiem. Wycinkiem może być jeden plik lub wiele plików.  
    
     ![blok Wycinek danych](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-dataslice-blade.png)
    
     Jeśli hello wycinka nie jest hello **gotowe** stanu, można zobaczyć hello niegotowe wycinki strumienia wychodzącego nie jest gotowa i blokuje hello bieżący fragment wykonywanie w hello **wycinków strumienia wychodzącego, które nie są gotowe** listy.
11. W hello **WYCINKA danych** bloku, powinien zostać wyświetlony na liście hello u dołu hello odbywa się działanie wszystkich. Kliknij przycisk **uruchamiania działania** toosee hello **szczegóły uruchomienia działania** bloku. 
    
    ![Szczegóły uruchamiania działania](./media/data-factory-copy-activity-tutorial-using-azure-portal/ActivityRunDetails.png)

    W tym bloku można zobaczyć, jaki zajęło dużo hello operacji kopiowania, jakie przepływności, liczby bajtów danych zostały odczytu i czasem rozpoczęcia zapisywane, uruchom, uruchomieniu godziny zakończenia, itp.  
12. Kliknij przycisk **X** tooclose wszystkie bloki hello dopóki wrócić toohello macierzystego bloku hello **ADFTutorialDataFactory**.
13. (opcjonalnie) kliknij przycisk hello **zestawów danych** Kafelek lub **potoki** bloków hello tooget kafelka przejrzane hello powyższych kroków. 
14. Uruchom **programu SQL Server Management Studio**, Połącz toohello bazy danych SQL Azure i sprawdź, czy wiersze hello są wstawiane toohello **pustych elementów** tabeli w bazie danych hello.
    
    ![wyniki zapytania sql](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-sql-query-results.png)


## <a name="summary"></a>Podsumowanie
W tym samouczku danych toocopy fabryki danych Azure została utworzona z bazy danych Azure SQL tooan obiektów blob platformy Azure. Użyto fabryki danych hello Azure toocreate portalu hello, połączone usługi, zestawy danych i potoku. Poniżej przedstawiono ogólne kroki hello, wykonane w tym samouczku:  

1. Tworzenie **fabryki danych** Azure.
2. Tworzenie **połączonych usług**:
   1. **Usługi Azure Storage** połączone konta magazynu Azure, która przechowuje dane wejściowe toolink usługi.     
   2. **Azure SQL** połączone z bazy danych Azure SQL, która przechowuje dane wyjściowe hello toolink usługi. 
3. Tworzenie **zestawów danych** opisujących dane wejściowe i wyjściowe dla potoków.
4. Tworzenie **potoku** za pomocą **działania kopiowania**, w którym źródłem jest element **BlobSource**, a ujściem element **SqlSink**.  

## <a name="next-steps"></a>Następne kroki
W tym samouczku użyto magazynu obiektów blob platformy Azure jako magazynu danych źródła oraz bazy danych SQL na platformie Azure jako magazynu danych docelowych w operacji kopiowania. Witaj Poniższa tabela zawiera listę magazynów danych obsługiwane jako źródeł i miejsc docelowych przez działanie kopiowania hello: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

toolearn o jak magazyn danych toocopy z danych, kliknij łącze hello hello magazynu danych w tabeli hello.
