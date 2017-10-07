---
title: "Samouczek: tworzenie potoku za pomocą działania kopiowania przy użyciu programu Visual Studio | Microsoft Docs"
description: "Ten samouczek zawiera instrukcje tworzenia potoku usługi Azure Data Factory za pomocą działania kopiowania przy użyciu programu Visual Studio."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1751185b-ce0a-4ab2-a9c3-e37b4d149ca3
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: d99d8875807bab41f5122ab95a09f83f82923529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-visual-studio"></a>Samouczek: tworzenie potoku za pomocą działania kopiowania przy użyciu programu Visual Studio
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

W tym artykule dowiesz się, jak toouse hello toocreate programu Microsoft Visual Studio fabryki danych z potok, który kopiuje dane z bazy danych Azure SQL tooan magazynu obiektów blob platformy Azure. Jeśli nowy tooAzure fabryki danych, zapoznaj się z artykułem hello [tooAzure wprowadzenie fabryki danych](data-factory-introduction.md) artykuł przed wykonaniem tego samouczka.   

W tym samouczku opisano tworzenie potoku z jednym działaniem (Działanie kopiowania). działanie kopiowania Hello kopiuje dane z magazynu danych obsługiwanych ujścia magazynu tooa obsługiwane dane. Aby zapoznać się z listą magazynów danych obsługiwanych jako źródła i ujścia, zobacz [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats). działanie Hello jest obsługiwany przez ogólnie dostępna usługa, która można skopiować dane między różnych magazynach danych w sposób bezpieczny, niezawodny i skalowalności. Aby uzyskać więcej informacji na temat hello działanie kopiowania, zobacz [działań przepływu danych](data-factory-data-movement-activities.md).

Potok może obejmować więcej niż jedno działanie. I tworzenia łańcucha dwa działania (Uruchom jedno działanie po drugim), ustawiając hello wyjściowy zestaw danych z jednego działania jako hello wejściowy zestaw danych z hello innych działań. Aby uzyskać więcej informacji, zobacz sekcję dotyczącą [wielu działań w potoku](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).

> [!NOTE] 
> Witaj potoku danych w tym samouczku kopiuje dane z magazynu danych źródła danych magazynu tooa docelowego. Samouczek na temat danych tootransform przy użyciu fabryki danych Azure, zobacz [samouczek: Tworzenie danych tootransform potoku, przy użyciu klastra usługi Hadoop](data-factory-build-your-first-pipeline.md).

## <a name="prerequisites"></a>Wymagania wstępne
1. Zapoznaj się z artykułem [— samouczek Przegląd](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) artykułu i pełne hello **wymagań wstępnych** czynności.       
2. toocreate wystąpienia fabryki danych, musi być członkiem hello [współautora fabryki danych](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) roli na poziomie grupy zasobów subskrypcji hello.
3. Musi mieć zainstalowane na komputerze następujące hello: 
   * Visual Studio 2013 lub Visual Studio 2015
   * Pobierz zestaw Azure SDK dla programu Visual Studio 2013 lub Visual Studio 2015. Przejdź za[strony pobierania Azure](https://azure.microsoft.com/downloads/) i kliknij przycisk **VS 2013** lub **VS 2015** w hello **.NET** sekcji.
   * Pobierz najnowszy dodatek fabryki danych Azure hello for Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) lub [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005). Można także zaktualizować hello wtyczki, wykonując następujące kroki hello: polecenie hello menu **narzędzia** -> **rozszerzenia i aktualizacje** -> **Online**  ->  **Galerii programu visual Studio** -> **narzędzia fabryki danych Microsoft Azure dla programu Visual Studio** -> **aktualizacji**.

## <a name="steps"></a>Kroki
Poniżej przedstawiono kroki hello, które należy wykonać w ramach tego samouczka:

1. Utwórz **połączone usługi** w fabryce danych hello. Ten krok polega na utworzeniu dwóch połączonych usług: Azure Storage i Azure SQL Database. 
    
    Witaj AzureStorageLinkedService łączy fabrykę danych toohello konta magazynu platformy Azure. Utworzono kontener i przekazany w ramach konta magazynu danych toothis [wymagania wstępne](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

    AzureSqlLinkedService łączy fabrykę danych toohello bazy danych Azure SQL. dane Hello, który jest skopiowany z magazynu obiektów blob hello są przechowywane w tej bazie danych. W ramach [wymagań wstępnych](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) w tej bazie danych została utworzona tabela SQL.     
2. Utwórz dane wejściowe i wyjściowe **zestawów danych** w fabryce danych hello.  
    
    Hello Azure połączoną usługą magazynu określa parametry połączenia hello, która używa usługi fabryka danych w czasie wykonywania tooconnect tooyour kontem magazynu platformy Azure. I zestawu danych wejściowych obiektu blob hello określa hello kontenera i folderu hello, który zawiera hello danych wejściowych.  

    Podobnie hello usługi baza danych SQL Azure połączone określa hello parametry połączenia, które korzysta z usługi fabryka danych w czasie wykonywania tooconnect tooyour — bazy danych Azure SQL. I tabeli hello hello bazy danych toowhich hello danych z magazynu obiektów blob hello jest kopiowany określa hello danych wyjściowych SQL tabeli dataset.
3. Utwórz **potoku** w fabryce danych hello. W tym kroku jest tworzony potok za pomocą działania kopiowania.   
    
    działanie kopiowania Hello kopiuje dane z obiektu blob w tabeli tooa magazynu obiektów blob platformy Azure hello w bazie danych Azure SQL hello. Działanie kopiowania służy w potoku danych toocopy z dowolnego miejsca docelowego tooany obsługiwane obsługiwanej źródłowej. Listę obsługiwanych magazynów danych można znaleźć w artykule [Działania związane z przenoszeniem danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats). 
4. Utworzenie **fabryki danych** Azure podczas wdrażania jednostek usługi Data Factory (połączone usługi, zestawy danych/tabele i potoki). 

## <a name="create-visual-studio-project"></a>Tworzenie projektu programu Visual Studio
1. Uruchom program **Visual Studio 2015**. Kliknij przycisk **pliku**, punktu zbyt**nowy**i kliknij przycisk **projektu**. Powinny pojawić się hello **nowy projekt** okno dialogowe.  
2. W hello **nowy projekt** okno dialogowe, wybierz opcję hello **DataFactory** szablonu, a następnie kliknij przycisk **pusty projekt fabryki danych**.  
   
    ![Okno dialogowe Nowy projekt](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-project-dialog.png)
3. Określ nazwę hello hello projektu, lokalizacji dla rozwiązania hello i hello rozwiązania, a następnie kliknij przycisk **OK**.
   
    ![Eksplorator rozwiązań](./media/data-factory-copy-activity-tutorial-using-visual-studio/solution-explorer.png)    

## <a name="create-linked-services"></a>Tworzenie połączonych usług
Połączone usługi są tworzone w toolink fabryki danych dane są przechowywane i obliczeniowe fabryki danych toohello usług. W tym samouczku nie przedstawiono korzystania z żadnych usług obliczeniowych, takich jak Azure HDInsight czy Azure Data Lake Analytics. Zostają użyte dwa magazyny danych typu Azure Storage (źródło) i Azure SQL Database (lokalizacja docelowa). 

Tak więc tworzy się dwie połączone usługi: AzureStorage i AzureSqlDatabase.  

Hello Azure Storage połączone usługi łączy fabrykę danych toohello konta magazynu platformy Azure. To konto magazynu jest hello jedną w którym utworzono kontener i hello dane przekazane jako część [wymagania wstępne](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

Azure SQL połączone usługi łączy fabrykę danych toohello bazy danych Azure SQL. dane Hello, który jest skopiowany z magazynu obiektów blob hello są przechowywane w tej bazie danych. Utworzono hello pustych elementów tabeli w tej bazie danych jako część [wymagania wstępne](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

Połączone usługi łączenie magazyny danych lub obliczeniowe fabryki danych Azure tooan usług. Zobacz [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats) dla wszystkich hello źródeł i wychwytywanie obsługiwane przez hello działanie kopiowania. Zobacz [obliczeniowe połączonych usług](data-factory-compute-linked-services.md) hello lista usługi obliczeniowe obsługiwane przez fabryki danych. Ten samouczek nie obejmuje używania żadnej usługi obliczeniowej. 

### <a name="create-hello-azure-storage-linked-service"></a>Utwórz hello połączoną usługą magazynu Azure
1. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy **połączonych usług**, punktu zbyt**Dodaj**i kliknij przycisk **nowy element**.      
2. W hello **Dodaj nowy element** okno dialogowe, wybierz opcję **połączonej usługi magazynu Azure** hello listy i kliknij przycisk **Dodaj**. 
   
    ![Nowa połączona usługa](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-linked-service-dialog.png)
3. Zastąp `<accountname>` i `<accountkey>`* hello nazwą konta magazynu Azure i klucza. 
   
    ![Połączona usługa Azure Storage](./media/data-factory-copy-activity-tutorial-using-visual-studio/azure-storage-linked-service.png)
4. Zapisz hello **AzureStorageLinkedService1.json** pliku.

    Aby uzyskać więcej informacji o właściwościach JSON w definicji usługi hello połączone, zobacz [łącznika usługi Azure Blob Storage](data-factory-azure-blob-connector.md#linked-service-properties) artykułu.

### <a name="create-hello-azure-sql-linked-service"></a>Utwórz hello Azure połączoną usługą SQL
1. Kliknij prawym przyciskiem myszy **połączonych usług** węzła w hello **Eksploratora rozwiązań** ponownie punktu zbyt**Dodaj**i kliknij przycisk **nowy element**. 
2. Tym razem wybierz pozycję **Połączona usługa SQL Azure** i kliknij przycisk **Dodaj**. 
3. W hello **pliku AzureSqlLinkedService1.json**, Zastąp `<servername>`, `<databasename>`, `<username@servername>`, i `<password>` z nazwy serwera Azure SQL, bazy danych, konto użytkownika i hasło.    
4. Zapisz hello **AzureSqlLinkedService1.json** pliku. 
    
    Aby uzyskać więcej informacji o tych właściwościach JSON, zobacz artykuł dotyczący [łącznika usługi Azure SQL Database](data-factory-azure-sql-connector.md#linked-service-properties).


## <a name="create-datasets"></a>Tworzenie zestawów danych
W poprzednim kroku hello utworzono toolink połączone usługi konta magazynu Azure i fabryki danych tooyour bazy danych Azure SQL. W tym kroku należy zdefiniować dwa zestawy danych o nazwie InputDataset i OutputDataset reprezentujące danych wejściowych i wyjściowych danych przechowywanych w magazynach danych hello odwołuje się AzureStorageLinkedService1 i AzureSqlLinkedService1 odpowiednio.

Hello Azure połączoną usługą magazynu określa parametry połączenia hello, która używa usługi fabryka danych w czasie wykonywania tooconnect tooyour kontem magazynu platformy Azure. I zestawu danych wejściowych obiektu blob hello (InputDataset) określa hello kontenera i folderu hello, który zawiera hello danych wejściowych.  

Podobnie hello usługi baza danych SQL Azure połączone określa hello parametry połączenia, które korzysta z usługi fabryka danych w czasie wykonywania tooconnect tooyour — bazy danych Azure SQL. I hello danych wyjściowych SQL tabeli dataset (OututDataset) określa hello tabeli w hello bazy danych toowhich powitalne dane z magazynu obiektów blob hello są kopiowane. 

### <a name="create-input-dataset"></a>Tworzenie wejściowego zestawu danych
W tym kroku utworzysz zestaw danych o nazwie InputDataset, który wskazuje plik obiektu blob tooa (emp.txt) w folderze głównym hello kontenera obiektów blob (adftutorial) w hello reprezentowany przez hello AzureStorageLinkedService1 połączone usługi Magazyn Azure. Brak określić wartość dla nazwy pliku hello (lub Pomiń je), danych z wszystkich obiektów blob w folderze wejściowych hello są skopiowanych toohello docelowego. W tym samouczku należy określić wartość dla hello fileName. 

W tym miejscu możesz użyć hello termin "tabele" zamiast "zestawy danych". Tabela jest prostokątny zestawu danych i hello tylko typ zestawu danych obsługiwane w tej chwili. 

1. Kliknij prawym przyciskiem myszy **tabel** w hello **Eksploratora rozwiązań**, punktu zbyt**Dodaj**i kliknij przycisk **nowy element**.
2. W hello **Dodaj nowy element** okno dialogowe, wybierz opcję **obiektów Blob platformy Azure**i kliknij przycisk **Dodaj**.   
3. Zamień tekst JSON hello hello następującego tekstu i Zapisz hello **AzureBlobLocation1.json** pliku. 

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
      "linkedServiceName": "AzureStorageLinkedService1",
      "typeProperties": {
        "folderPath": "adftutorial/",
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

### <a name="create-output-dataset"></a>Tworzenie wyjściowego zestawu danych
W tym kroku tworzony jest wyjściowy zestaw danych o nazwie **OutputDataset**. Ten zestaw danych wskazuje tooa tabeli SQL w bazie danych Azure SQL hello reprezentowany przez **AzureSqlLinkedService1**. 

1. Kliknij prawym przyciskiem myszy **tabel** w hello **Eksploratora rozwiązań** ponownie punktu zbyt**Dodaj**i kliknij przycisk **nowy element**.
2. W hello **Dodaj nowy element** okno dialogowe, wybierz opcję **Azure SQL**i kliknij przycisk **Dodaj**. 
3. Zamień tekst JSON hello hello następującego formatu JSON i Zapisz hello **AzureSqlTableLocation1.json** pliku.

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
       "linkedServiceName": "AzureSqlLinkedService1",
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

## <a name="create-pipeline"></a>Tworzenie potoku
W tym kroku opisano tworzenie potoku za pomocą **działania kopiowania**, w którym parametr **InputDataset** jest używany jako dane wejściowe, a parametr **OutputDataset** jako dane wyjściowe.

Wyjściowy zestaw danych jest obecnie, jakie dysków hello harmonogramu. W tym samouczku wyjściowy zestaw danych jest skonfigurowane tooproduce wycinek godzinę. potok Hello ma czas rozpoczęcia i godzina zakończenia, będące w ciągu jednego dnia od siebie, który wynosi 24 godziny. W związku z tym 24 wycinków wyjściowy zestaw danych są produkowane przez hello potoku. 

1. Kliknij prawym przyciskiem myszy **potoki** w hello **Eksploratora rozwiązań**, punktu zbyt**Dodaj**i kliknij przycisk **nowy element**.  
2. Wybierz **kopiowania danych potoku** w hello **Dodaj nowy element** okno dialogowe i kliknij przycisk **Dodaj**. 
3. Zamień hello JSON hello następującego formatu JSON i Zapisz hello **CopyActivity1.json** pliku.

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
             "style": "StartOfInterval",
             "retry": 0,
             "timeout": "01:00:00"
           }
         }
       ],
       "start": "2017-05-11T00:00:00Z",
       "end": "2017-05-12T00:00:00Z",
       "isPaused": false
     }
    }
    ```   
    - W sekcji działania hello jest tylko jedno działanie którego **typu** ustawiono zbyt**kopiowania**. Aby uzyskać więcej informacji o działaniu kopiowania hello, zobacz [działań przepływu danych](data-factory-data-movement-activities.md). W rozwiązaniach usługi Data Factory można również użyć [działań dotyczących przekształcania danych](data-factory-data-transformation-activities.md).
    - Dane wejściowe dla działania hello jest ustawiony za**InputDataset** i danych wyjściowych dla działania hello jest ustawiony za**OutputDataset**. 
    - W hello **typeProperties** sekcji **BlobSource** jest określony jako typ źródła hello i **SqlSink** jest określony jako typ ujścia hello. Aby uzyskać pełną listę obsługiwanych przez działanie kopiowania hello jako źródła i wychwytywanie magazyny danych, zobacz [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats). toolearn jak przechowywać toouse określonych danych obsługiwane jako źródło/ujście, kliknij łącze hello hello tabeli.  
     
    Zastąp wartość hello hello **start** właściwość o hello bieżącego dnia i **zakończenia** wartości z hello następnego dnia. Można określić tylko część daty hello i Pomiń hello czas część hello Data i godzina. Na przykład "2016-02-03", która odpowiada za "2016-02-03T00:00:00Z"
     
    Zarówno data/godzina rozpoczęcia, jak i data/godzina zakończenia muszą być w [formacie ISO](http://en.wikipedia.org/wiki/ISO_8601). Przykładowo: 2016-10-14T16:32:41Z. Witaj **zakończenia** czasu jest opcjonalne, ale możemy użyć w tym samouczku. 
     
    Jeśli nie określisz wartości hello **zakończenia** właściwości, jest on obliczany jako "**start + 48 godzin**". potok hello toorun przez czas nieokreślony, określ **9999-09-09** jako wartość hello hello **zakończenia** właściwości.
     
    W hello poprzedzających przykład istnieją 24 wycinków danych, jak każdy wycinek danych jest tworzone co godzinę.

    Opisy właściwości JSON w definicji potoku znajdują się w artykule dotyczącym [tworzenia potoków](data-factory-create-pipelines.md). Opisy właściwości JSON w definicji działania kopiowania znajdują się w artykule dotyczącym [działań związanych z przenoszeniem danych](data-factory-data-movement-activities.md). Opisy właściwości JSON obsługiwanych przez BlobSource można znaleźć w [artykule dotyczącym łącznika usługi Azure Blob](data-factory-azure-blob-connector.md). Opisy właściwości JSON obsługiwanych przez SqlSink można znaleźć w artykule [dotyczącym łącznika usługi Azure SQL Database](data-factory-azure-sql-connector.md).

## <a name="publishdeploy-data-factory-entities"></a>Publikowanie/wdrażanie jednostek usługi Fabryka danych
W tym kroku publikowane są utworzone wcześniej obiekty usługi Data Factory (połączone usługi, zestawy danych i potok). Należy także określić nazwę hello hello nowe toobe fabryki danych utworzone toohold tych jednostek.  

1. Kliknij prawym przyciskiem myszy projekt w Eksploratorze rozwiązań hello, a następnie kliknij przycisk **publikowania**. 
2. Jeśli widzisz **Zaloguj tooyour konta Microsoft** okno dialogowe, wprowadź swoje poświadczenia dla konta hello subskrypcji platformy Azure, a następnie kliknij przycisk **Zaloguj**.
3. Powinny zostać wyświetlone następujące okno dialogowe hello:
   
   ![Okno dialogowe publikowania](./media/data-factory-copy-activity-tutorial-using-visual-studio/publish.png)
4. W hello strony fabryki danych konfiguracji hello następujące kroki: 
   
   1. Zaznacz opcję **Utwórz nową fabrykę danych**.
   2. Wprowadź wartość **VSTutorialFactory** w polu **Nazwa**.  
      
      > [!IMPORTANT]
      > Nazwa fabryki danych Azure hello Hello musi być globalnie unikatowe. Jeśli zostanie wyświetlony błąd o nazwie hello fabryki danych podczas publikowania, Zmień nazwę hello hello fabryki danych (na przykład yournameVSTutorialFactory) i spróbuj ponownie opublikować. Artykuł [Data Factory — Naming Rules](data-factory-naming-rules.md) (Fabryka danych — zasady nazewnictwa) zawiera zasady nazewnictwa artefaktów usługi Fabryka danych.        
      > 
      > 
   3. Wybierz subskrypcję platformy Azure dla hello **subskrypcji** pola.
      
      > [!IMPORTANT]
      > Jeśli nie ma żadnej subskrypcji. Upewnij się, czy użytkownik zalogowany przy użyciu konta administratora lub współadministratora subskrypcji hello.  
      > 
      > 
   4. Wybierz hello **grupy zasobów** dla toobe fabryki danych hello utworzony. 
   5. Wybierz hello **region** hello fabryki danych. Tylko regiony obsługiwane przez hello usługi fabryka danych są wyświetlane na liście rozwijanej hello.
   6. Kliknij przycisk **dalej** tooswitch toohello **publikowania elementów** strony.
      
       ![Strona konfiguracji fabryki danych](media/data-factory-copy-activity-tutorial-using-visual-studio/configure-data-factory-page.png)   
5. W hello **publikowania elementów** upewnij się, że wszystkie hello fabryki danych jednostek są zaznaczone, a następnie kliknij przycisk **dalej** tooswitch toohello **Podsumowanie** strony.
   
   ![Strona publikowania elementów](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-items-page.png)     
6. Przejrzyj podsumowanie hello i kliknij przycisk **dalej** toostart hello wdrożenie procesu i sprawdź hello **stan wdrożenia**.
   
   ![Strona publikowania podsumowania](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-summary-page.png)
7. W hello **stan wdrożenia** strony, powinien zostać wyświetlony stan hello hello procesu wdrażania. Po ukończeniu wdrażania hello, kliknij przycisk Zakończ.
 
   ![Strona stanu wdrożenia](media/data-factory-copy-activity-tutorial-using-visual-studio/deployment-status.png)

Należy zwrócić uwagę hello następujące punkty: 

* Jeśli wystąpi błąd hello: "Ta subskrypcja nie jest zarejestrowany toouse przestrzeni nazw Microsoft.DataFactory", wykonaj jedną z następujących hello i spróbuj ponownie opublikować: 
  
  * W programie Azure PowerShell Uruchom hello następujące polecenia tooregister hello fabryki danych dostawcy. 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    Powitania po tooconfirm polecenie można uruchomić tego hello fabryki danych dostawca został zarejestrowany. 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * Logowanie przy użyciu hello subskrypcji platformy Azure do hello [portalu Azure](https://portal.azure.com) i przejdź do bloku usługi fabryka danych tooa tworzenie fabryki danych w hello portalu Azure (lub). Ta akcja rejestruje automatycznie hello dostawcy dla Ciebie.
* Nazwa fabryki danych hello Hello mogą być zarejestrowana jako nazwa DNS w przyszłości hello i dlatego stać się publicznie widoczna.

> [!IMPORTANT]
> toocreate wystąpienia fabryki danych, należy toobe admin/współadministrator z hello subskrypcji platformy Azure

## <a name="monitor-pipeline"></a>Monitorowanie potoku
Przejdź na stronę główną toohello fabrykę danych:

1. Zaloguj się za[portalu Azure](https://portal.azure.com).
2. Kliknij przycisk **więcej usług** hello menu po lewej stronie i kliknij przycisk **fabryki danych**.

    ![Przeglądanie fabryk danych](media/data-factory-copy-activity-tutorial-using-visual-studio/browse-data-factories.png)
3. Wpisz nazwę hello w fabryce danych.

    ![Nazwa fabryki danych](media/data-factory-copy-activity-tutorial-using-visual-studio/enter-data-factory-name.png) 
4. Kliknij przycisk fabrykę danych w hello wyniki listy toosee hello strony głównej fabryką danych.

    ![Strona główna fabryki danych](media/data-factory-copy-activity-tutorial-using-visual-studio/data-factory-home-page.png)
5. Postępuj zgodnie z instrukcjami [monitorowanie zestawów danych i potoku](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) toomonitor hello potoku i zestawy danych zostały utworzone w tym samouczku. Obecnie program Visual Studio nie obsługuje monitorowania potoków usługi Data Factory. 

## <a name="summary"></a>Podsumowanie
W tym samouczku danych toocopy fabryki danych Azure została utworzona z bazy danych Azure SQL tooan obiektów blob platformy Azure. Użyto fabryki danych hello toocreate programu Visual Studio, połączone usługi, zestawy danych i potoku. Poniżej przedstawiono ogólne kroki hello, wykonane w tym samouczku:  

1. Tworzenie **fabryki danych** Azure.
2. Tworzenie **połączonych usług**:
   1. **Usługi Azure Storage** połączone konta magazynu Azure, która przechowuje dane wejściowe toolink usługi.     
   2. **Azure SQL** połączone z bazy danych Azure SQL, która przechowuje dane wyjściowe hello toolink usługi. 
3. Tworzenie **zestawów danych** opisujących dane wejściowe i wyjściowe dla potoków.
4. Tworzenie **potoku** za pomocą **działania kopiowania**, w którym źródłem jest element **BlobSource**, a ujściem element **SqlSink**. 

toosee toouse danych tootransform działania Hive HDInsight przy użyciu klastra Azure HDInsight, zobacz temat [ samouczek: Tworzenie pierwszego potoku dane tootransform przy użyciu klastra usługi Hadoop](data-factory-build-your-first-pipeline.md).

Powiązane z dwóch działań (Uruchom jedno działanie po drugim), ustawiając hello wyjściowy zestaw danych z jednego działania jako hello wejściowy zestaw danych z hello innych działań. Szczegółowe informacje znajdują się w artykule [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) (Planowanie i wykonywanie w usłudze Data Factory). 

## <a name="view-all-data-factories-in-server-explorer"></a>Wyświetlanie wszystkich fabryk danych w Eksploratorze serwera
W tej sekcji opisano sposób toouse hello Eksploratora serwera w Visual Studio tooview wszystkie hello fabryki danych w ramach subskrypcji platformy Azure i tworzenia projektu programu Visual Studio, w oparciu o istniejącą fabrykę danych. 

1. W **programu Visual Studio**, kliknij przycisk **widoku** hello menu i kliknij przycisk **Eksploratora serwera**.
2. W oknie Eksploratora serwera hello, rozwiń węzeł **Azure** i rozwiń **fabryki danych**. Jeśli widzisz **Zaloguj tooVisual Studio**, wprowadź hello **konta** skojarzone z subskrypcją platformy Azure i kliknij przycisk **Kontynuuj**. Wprowadź **hasło** i kliknij przycisk **Zaloguj**. Visual Studio próbuje tooget informacji na temat wszystkich fabryki danych Azure w ramach subskrypcji. Zobacz hello stan tej operacji w hello **listy zadań fabryki danych** okna.

    ![Eksplorator serwera](./media/data-factory-copy-activity-tutorial-using-visual-studio/server-explorer.png)

## <a name="create-a-visual-studio-project-for-an-existing-data-factory"></a>Tworzenie projektu programu Visual Studio dla istniejącej fabryki danych

- Kliknij prawym przyciskiem myszy w Eksploratorze serwera fabryki danych i wybierz **tooNew wyeksportować fabryki danych projektu** toocreate na istniejącą fabrykę danych na podstawie projektu programu Visual Studio.

    ![Eksportowanie projektu programu VS tooa fabryki danych](./media/data-factory-copy-activity-tutorial-using-visual-studio/export-data-factory-menu.png)  

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


## <a name="next-steps"></a>Następne kroki
W tym samouczku użyto magazynu obiektów blob platformy Azure jako magazynu danych źródła oraz bazy danych SQL na platformie Azure jako magazynu danych docelowych w operacji kopiowania. Witaj Poniższa tabela zawiera listę magazynów danych obsługiwane jako źródeł i miejsc docelowych przez działanie kopiowania hello: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

toolearn o jak magazyn danych toocopy z danych, kliknij łącze hello hello magazynu danych w tabeli hello.
