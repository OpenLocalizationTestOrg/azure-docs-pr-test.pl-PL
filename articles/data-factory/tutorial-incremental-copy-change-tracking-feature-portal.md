---
title: "Przyrostowe kopiowanie danych przy użyciu rozwiązania Change Tracking i usługi Azure Data Factory | Microsoft Docs"
description: "W tym samouczku utworzysz potok usługi Azure Data Factory służący do przyrostowego kopiowania danych różnicowych z wielu tabel w lokalnej bazie danych SQL Server do bazy danych Azure SQL Database. "
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
ms.date: 01/12/2018
ms.author: jingwang
ms.openlocfilehash: 93df74da6e9db1bd03885179cd3917205ab3b4ee
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/23/2018
---
# <a name="incrementally-load-data-from-azure-sql-database-to-azure-blob-storage-using-change-tracking-information"></a>Przyrostowe ładowanie danych z bazy danych Azure SQL Database do magazynu Azure Blob Storage z użyciem informacji o śledzeniu zmian 
W tym samouczku utworzysz fabrykę usługi Azure Data Factory z potokiem służącym do ładowania danych przyrostowych na podstawie informacji o **śledzeniu zmian** w źródłowej bazie danych Azure SQL Database do magazynu Azure Blob Storage.  

Ten samouczek obejmuje następujące procedury:

> [!div class="checklist"]
> * Przygotowywanie magazynu danych źródłowych
> * Tworzenie fabryki danych.
> * Tworzenie połączonych usług. 
> * Tworzenie zestawów danych źródła, ujścia i śledzenia zmian.
> * Tworzenie, uruchamianie i monitorowanie potoku pełnego kopiowania
> * Dodawanie lub aktualizowanie danych w tabeli źródłowej
> * Tworzenie, uruchamianie i monitorowanie potoku kopiowania przyrostowego

> [!NOTE]
> Ten artykuł dotyczy wersji 2 usługi Data Factory, która jest obecnie dostępna w wersji zapoznawczej. Jeśli używasz dostępnej ogólnie wersji 1 usługi Data Factory, zobacz [dokumentację dotyczącą usługi Data Factory w wersji 1](v1/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

## <a name="overview"></a>Omówienie
W rozwiązaniu integracji danych przyrostowe ładowanie danych po początkowych operacjach ładowania danych to powszechnie używany scenariusz. W niektórych przypadkach dane zmienione w określonym czasie w magazynie danych źródła można łatwo podzielić (na przykład na podstawie właściwości LastModifyTime i CreationTime). W niektórych przypadkach nie można jednak w jednoznaczny sposób zidentyfikować danych różnicowych pochodzących z ostatniej operacji przetwarzania danych. Technologia Change Tracking obsługiwana przez magazyny danych, takie jak baza danych Azure SQL Database i serwer SQL Server, może służyć do identyfikowania danych różnicowych.  W tym samouczku opisano sposób używania usługi Azure Data Factory w wersji 2 do pracy z technologią Change Tracking w celu przyrostowego ładowania danych różnicowych z bazy danych Azure SQL Database do magazynu Azure Blob Storage.  Aby uzyskać bardziej konkretne informacje na temat technologii Change Tracking w bazie danych SQL, zobacz [Technologia Change Tracking w programie SQL Server](/sql/relational-databases/track-changes/about-change-tracking-sql-server). 

## <a name="end-to-end-workflow"></a>Kompletny przepływ pracy
Poniżej przedstawiono kroki kompleksowego przepływu pracy służące do przyrostowego ładowania danych przy użyciu technologii Change Tracking.

> [!NOTE]
> Technologia Change Tracking jest obsługiwana zarówno przez bazę danych Azure SQL Database, jak i serwer SQL Server. W tym samouczku baza danych Azure SQL Database jest używana jako magazyn danych źródłowych. Możesz również użyć lokalnego serwera SQL Server. 

1. **Początkowe ładowanie danych historycznych** (uruchamiane raz):
    1. Włącz technologię Change Tracking w źródłowej bazie danych Azure SQL Database.
    2. Pobierz wartość początkową parametru SYS_CHANGE_VERSION w bazie danych Azure SQL Database jako linię bazową na potrzeby przechwytywania zmienionych danych.
    3. Załaduj pełne dane z bazy danych Azure SQL Database do magazynu Azure Blob Storage. 
2. **Przyrostowe ładowanie danych różnicowych zgodnie z harmonogramem** (uruchamiane okresowo po początkowym załadowaniu danych):
    1. Pobierz starą i nową wartość parametru SYS_CHANGE_VERSION.
    3. Załaduj dane różnicowe, łącząc klucze podstawowe zmienionych wierszy (między dwiema wartościami parametru SYS_CHANGE_VERSION) z tabeli **sys.change_tracking_tables** z danymi w **tabeli źródłowej**, a następnie przenieś dane różnicowe do lokalizacji docelowej.
    4. Zaktualizuj wartość parametru SYS_CHANGE_VERSION na potrzeby następnego ładowania danych różnicowych.

## <a name="high-level-solution"></a>Rozwiązanie ogólne
W tym samouczku utworzysz dwa potoki, za pomocą których zostaną wykonane następujące dwie operacje:  

1. **Ładowanie początkowe:** utworzysz potok z działaniem kopiowania, które kopiuje wszystkie dane z magazynu danych źródłowych (baza danych Azure SQL Database) do docelowego magazynu danych (magazyn Azure Blob Storage).

    ![Pełne ładowanie danych](media/tutorial-incremental-copy-change-tracking-feature-portal/full-load-flow-diagram.png)
1.  **Ładowanie przyrostowe:** utworzysz potok z następującymi działaniami, który będzie okresowo uruchamiany. 
    1. Utwórz **dwa działania wyszukiwania**, aby pobrać starą i nową wartość parametru SYS_CHANGE_VERSION z bazy danych Azure SQL Database i przekazać ją do działania kopiowania.
    2. Utwórz **jedno działanie kopiowania**, aby skopiować wstawione, zaktualizowane lub usunięte dane między dwiema wartościami parametru SYS_CHANGE_VERSION z bazy danych Azure SQL Database do magazynu Azure Blob Storage.
    3. Utwórz **jedno działanie procedury składowanej**, aby zaktualizować wartość parametru SYS_CHANGE_VERSION na potrzeby następnego uruchomienia potoku.

    ![Diagram przepływu ładowania przyrostowego](media/tutorial-incremental-copy-change-tracking-feature-portal/incremental-load-flow-diagram.png)


Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne](https://azure.microsoft.com/free/) konto.

## <a name="prerequisites"></a>Wymagania wstępne
* **Usługa Azure SQL Database**. Baza danych jest używana jako magazyn danych **źródłowych**. Jeśli nie masz bazy danych Azure SQL Database, utwórz ją, wykonując czynności przedstawione w artykule [Create an Azure SQL database (Tworzenie bazy danych Azure SQL Database)](../sql-database/sql-database-get-started-portal.md).
* **Konto usługi Azure Storage**. Magazyn obiektów blob jest używany jako magazyn danych **źródłowych**. Jeśli nie masz konta usługi Azure Storage, utwórz je, wykonując czynności przedstawione w artykule [Tworzenie konta magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account). Utwórz kontener o nazwie **adftutorial**. 

### <a name="create-a-data-source-table-in-your-azure-sql-database"></a>Tworzenie tabeli danych źródłowych w bazie danych Azure SQL
1. Uruchom program **SQL Server Management Studio**, a następnie nawiąż połączenie z serwerem Azure SQL Server. 
2. W **Eksploratorze serwera** kliknij prawym przyciskiem używaną **bazę danych**, a następnie wybierz pozycję **Nowe zapytanie**.
3. Uruchom poniższe polecenie SQL dla bazy danych Azure SQL, aby utworzyć tabelę o nazwie `data_source_table` jako magazyn danych źródłowych.  
    
    ```sql
    create table data_source_table
    (
        PersonID int NOT NULL,
        Name varchar(255),
        Age int
        PRIMARY KEY (PersonID)
    );

    INSERT INTO data_source_table
        (PersonID, Name, Age)
    VALUES
        (1, 'aaaa', 21),
        (2, 'bbbb', 24),
        (3, 'cccc', 20),
        (4, 'dddd', 26),
        (5, 'eeee', 22);

    ```
4. Włącz mechanizm **Change Tracking** w bazie danych i tabeli źródłowej (data_source_table), uruchamiając następujące zapytanie SQL: 

    > [!NOTE]
    > - Zastąp &lt;nazwę bazy danych&gt; nazwą bazy danych Azure SQL Database zawierającą tabelę data_source_table. 
    > - W bieżącym przykładzie zmienione dane są przechowywane przez dwa dni. W przypadku ładowania zmienionych danych nie rzadziej niż co trzy dni niektóre zmienione dane nie zostaną uwzględnione.  Jednym rozwiązaniem jest zmiana wartości parametru CHANGE_RETENTION na większą. Alternatywnie należy zapewnić, że okres ładowania zmienionych danych będzie wynosił maksymalnie dwa dni. Aby uzyskać więcej informacji, zobacz [Włącz śledzenie zmian dla bazy danych zmian](/sql/relational-databases/track-changes/enable-and-disable-change-tracking-sql-server#enable-change-tracking-for-a-database)
 
    ```sql
    ALTER DATABASE <your database name>
    SET CHANGE_TRACKING = ON  
    (CHANGE_RETENTION = 2 DAYS, AUTO_CLEANUP = ON)  
  
    ALTER TABLE data_source_table
    ENABLE CHANGE_TRACKING  
    WITH (TRACK_COLUMNS_UPDATED = ON)
    ```
5. Utwórz nową tabelę i ustaw wartość parametru ChangeTracking_version na wartość domyślną, uruchamiając następujące zapytanie: 

    ```sql
    create table table_store_ChangeTracking_version
    (
        TableName varchar(255),
        SYS_CHANGE_VERSION BIGINT,
    );

    DECLARE @ChangeTracking_version BIGINT
    SET @ChangeTracking_version = CHANGE_TRACKING_CURRENT_VERSION();  

    INSERT INTO table_store_ChangeTracking_version
    VALUES ('data_source_table', @ChangeTracking_version)
    ```
    
    > [!NOTE]
    > Jeśli dane nie ulegną zmianie po włączeniu śledzenia zmian dla bazy danych SQL Database, wartość wersji śledzenia zmian to 0.
6. Uruchom następujące zapytanie, aby utworzyć procedurę składowaną w bazie danych Azure SQL Database. Potok wywołuje tę procedurę składowaną w celu zaktualizowania wersji śledzenia zmian w tabeli utworzonej w poprzednim kroku. 

    ```sql
    CREATE PROCEDURE Update_ChangeTracking_Version @CurrentTrackingVersion BIGINT, @TableName varchar(50)
    AS
    
    BEGIN
    
        UPDATE table_store_ChangeTracking_version
        SET [SYS_CHANGE_VERSION] = @CurrentTrackingVersion
    WHERE [TableName] = @TableName
    
    END    
    ```

### <a name="azure-powershell"></a>Azure PowerShell
Zainstaluj najnowsze moduły programu Azure PowerShell, wykonując instrukcje podane w temacie [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/install-azurerm-ps).

## <a name="create-a-data-factory"></a>Tworzenie fabryki danych

1. Kliknij przycisk **Nowy** w lewym menu, kliknij pozycję **Dane + analiza**, a następnie kliknij pozycję **Data Factory**. 
   
   ![Nowy-> Fabryka danych](./media/tutorial-incremental-copy-change-tracking-feature-portal/new-azure-data-factory-menu.png)
2. Na stronie **Nowa fabryka danych** wprowadź wartość **ADFTutorialDataFactory** w polu **Nazwa**. 
      
     ![Strona Nowa fabryka danych](./media/tutorial-incremental-copy-change-tracking-feature-portal/new-azure-data-factory.png)
 
   Nazwa fabryki danych platformy Azure musi być **globalnie unikatowa**. Jeśli wystąpi poniższy błąd, zmień nazwę fabryki danych (np. twojanazwaADFTutorialDataFactory) i spróbuj utworzyć ją ponownie. Artykuł [Data Factory — Naming Rules (Usługa Data Factory — reguły nazewnictwa)](naming-rules.md) zawiera reguły nazewnictwa artefaktów usługi Data Factory.
  
       `Data factory name “ADFTutorialDataFactory” is not available`
3. Wybierz **subskrypcję** Azure, w której chcesz utworzyć fabrykę danych. 
4. Dla opcji **Grupa zasobów** wykonaj jedną z następujących czynności:
     
      - Wybierz pozycję **Użyj istniejącej**, a następnie wybierz istniejącą grupę zasobów z listy rozwijanej. 
      - Wybierz pozycję **Utwórz nową**, a następnie wprowadź nazwę grupy zasobów.   
         
        Informacje na temat grup zasobów znajdują się w artykule [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md) (Używanie grup zasobów do zarządzania zasobami platformy Azure).  
4. Wybierz wartość **V2 (wersja zapoznawcza)** dla **wersji**.
5. Na liście **lokalizacja** wybierz lokalizację fabryki danych. Na liście rozwijanej są wyświetlane tylko obsługiwane lokalizacje. Magazyny danych (Azure Storage, Azure SQL Database itp.) i jednostki obliczeniowe (HDInsight itp.) używane przez fabrykę danych mogą mieścić się w innych regionach.
6. Wybierz opcję **Przypnij do pulpitu nawigacyjnego**.     
7. Kliknij przycisk **Utwórz**.      
8. Na pulpicie nawigacyjnym jest widoczny następujący kafelek ze stanem: **Wdrażanie fabryki danych**. 

    ![kafelek Wdrażanie fabryki danych](media/tutorial-incremental-copy-change-tracking-feature-portal/deploying-data-factory.png)
9. Po zakończeniu tworzenia zostanie wyświetlona strona **Fabryka danych**, jak pokazano na poniższej ilustracji.
   
   ![Strona główna fabryki danych](./media/tutorial-incremental-copy-change-tracking-feature-portal/data-factory-home-page.png)
10. Kliknij kafelek **Tworzenie i monitorowanie**, aby w osobnej karcie uruchomić interfejs użytkownika usługi Azure Data Factory.
11. Na stronie **Wprowadzenie** przejdź do karty **Edycja** w lewym panelu, jak pokazano na poniższej ilustracji: 

    ![Przycisk Utwórz potok](./media/tutorial-incremental-copy-change-tracking-feature-portal/get-started-page.png)

## <a name="create-linked-services"></a>Tworzenie połączonych usług
Połączone usługi tworzy się w fabryce danych w celu połączenia magazynów danych i usług obliczeniowych z fabryką danych. W tej sekcji utworzysz usługi połączone ze swoim kontem usługi Azure Storage i bazą danych Azure SQL. 

### <a name="create-azure-storage-linked-service"></a>Tworzenie połączonej usługi Azure Storage.
W tym kroku opisano łączenie konta usługi Azure Storage z fabryką danych.

1. Kliknij kolejno pozycje **Połączenia** i **+ Nowy**.

   ![Przycisk Nowe połączenie](./media/tutorial-incremental-copy-change-tracking-feature-portal/new-connection-button-storage.png)
2. W oknie **Nowa połączona usługa** wybierz pozycję **Azure Blob Storage**, a następnie kliknij pozycję **Kontynuuj**. 

   ![Wybieranie pozycji Azure Blob Storage](./media/tutorial-incremental-copy-change-tracking-feature-portal/select-azure-storage.png)
3. W oknie **Nowa połączona usługa** wykonaj następujące czynności: 

    1. Wprowadź wartość **AzureStorageLinkedService** w polu **Nazwa**. 
    2. W polu **Nazwa konta magazynu** wybierz konto usługi Azure Storage. 
    3. Kliknij pozycję **Zapisz**. 
    
   ![Ustawienia konta usługi Azure Storage](./media/tutorial-incremental-copy-change-tracking-feature-portal/azure-storage-linked-service-settings.png)


### <a name="create-azure-sql-database-linked-service"></a>Utwórz połączoną usługę Azure SQL Database.
W tym kroku opisano sposób łączenia bazy danych Azure SQL Database z fabryką danych.

1. Kliknij kolejno pozycje **Połączenia** i **+ Nowy**.
2. W oknie **Nowa połączona usługa** wybierz pozycję **Azure SQL Database**, a następnie kliknij pozycję **Kontynuuj**. 
3. W oknie **Nowa połączona usługa** wykonaj następujące czynności: 

    1. Wprowadź wartość **AzureSqlDatabaseLinkedService** w polu **Nazwa**. 
    2. W polu **Nazwa serwera** wybierz serwer usługi Azure SQL.
    4. W polu **Nazwa bazy danych** wybierz bazę danych usługi Azure SQL. 
    5. W polu **Nazwa użytkownika** podaj nazwę użytkownika. 
    6. W polu **Hasło** podaj hasło użytkownika. 
    7. Kliknij pozycję **Testuj połączenie** w celu przetestowania połączenia.
    8. Kliknij przycisk **Zapisz**, aby zapisać połączoną usługę. 
    
       ![Ustawienia połączonej usługi Azure SQL Database](./media/tutorial-incremental-copy-change-tracking-feature-portal/azure-sql-database-linked-service-settings.png)

## <a name="create-datasets"></a>Tworzenie zestawów danych
W tym kroku utworzysz zestawy danych reprezentujące źródło danych, docelową lokalizację danych  i lokalizację, w której będzie przechowywana wartość parametru SYS_CHANGE_VERSION.

### <a name="create-a-dataset-to-represent-source-data"></a>Tworzenie zestawu danych reprezentującego źródło danych 
W tym kroku utworzysz zestaw danych reprezentujący źródło danych. 

1. W widoku drzewa kliknij kolejno pozycje **+ (plus)** i **Zestaw danych**. 

   ![Menu Nowy zestaw danych](./media/tutorial-incremental-copy-change-tracking-feature-portal/new-dataset-menu.png)
2. Wybierz pozycję **Azure SQL Database** i kliknij pozycję **Zakończ**. 

   ![Typ zestawu danych będącego źródłem — Azure SQL Database](./media/tutorial-incremental-copy-change-tracking-feature-portal/select-azure-sql-database.png)
3. Zostanie wyświetlona nowa karta służąca do konfigurowania zestawu danych. Zestaw danych powinien być też widoczny w widoku drzewa. W oknie **Właściwości** zmień nazwę zestawu danych na **SourceDataset**.

   ![Nazwa zestawu danych będącego źródłem](./media/tutorial-incremental-copy-change-tracking-feature-portal/source-dataset-name.png)    
4. Przejdź do karty **Połączenie** i wykonaj następujące czynności: 
    
    1. Wybierz wartość **AzureSqlDatabaseLinkedService** w polu **Połączona usługa**. 
    2. Wybierz element **[dbo].[tabela_będąca_źródłem_danych]** dla pozycji **Tabela**. 

   ![Połączenie ze źródłem](./media/tutorial-incremental-copy-change-tracking-feature-portal/source-dataset-connection.png)

### <a name="create-a-dataset-to-represent-data-copied-to-sink-data-store"></a>Utwórz zestaw danych reprezentujący dane skopiowane do magazynu danych będącego ujściem. 
W tym kroku utworzysz zestaw danych reprezentujący dane skopiowane z magazynu danych źródłowych. Jako jedno z wymagań wstępnych w magazynie Azure Blob Storage został utworzony kontener adftutorial. Utwórz kontener, jeśli nie istnieje, lub zmień nazwę istniejącego kontenera. W tym samouczku nazwa pliku wyjściowego jest generowana dynamicznie przy użyciu wyrażenia: `@CONCAT('Incremental-', pipeline().RunId, '.txt')`.

1. W widoku drzewa kliknij kolejno pozycje **+ (plus)** i **Zestaw danych**. 

   ![Menu Nowy zestaw danych](./media/tutorial-incremental-copy-change-tracking-feature-portal/new-dataset-menu.png)
2. Wybierz pozycję **Azure Blob Storage**, a następnie kliknij przycisk **Zakończ**. 

   ![Typ zestawu danych będącego ujściem — Azure Blob Storage](./media/tutorial-incremental-copy-change-tracking-feature-portal/source-dataset-type.png)
3. Zostanie wyświetlona nowa karta służąca do konfigurowania zestawu danych. Zestaw danych powinien być też widoczny w widoku drzewa. W oknie **Właściwości** zmień nazwę zestawu danych na **SinkDataset**.

   ![Zestaw danych będący ujściem — nazwa](./media/tutorial-incremental-copy-change-tracking-feature-portal/sink-dataset-name.png)
4. Przejdź do karty **Połączenie** w oknie Właściwości i wykonaj następujące czynności:

    1. Wybierz pozycję **AzureStorageLinkedService** w polu **Połączona usługa**.
    2. Wprowadź ciąg **adftutorial/incchgtracking** w części **folder** ścieżki **filePath**.
    3. Wprowadź ciąg **@CONCAT('Incremental-', pipeline().RunId, '.txt')** w części **file** ścieżki **filePath**.  

       ![Zestaw danych będący ujściem — połączenie](./media/tutorial-incremental-copy-change-tracking-feature-portal/sink-dataset-connection.png)

### <a name="create-a-dataset-to-represent-change-tracking-data"></a>Tworzenie zestawu danych reprezentującego dane rozwiązania Change Tracking 
W tym kroku utworzysz zestaw danych służący do przechowywania wartości wersji śledzenia zmian.  Utworzono tabelę wersja_rozwiązania_ChangeTracking_magazynu_tabel jako część wymagań wstępnych.

1. W widoku drzewa kliknij kolejno pozycje **+ (plus)** i **Zestaw danych**. 
2. Wybierz pozycję **Azure SQL Database** i kliknij pozycję **Zakończ**. 
3. Zostanie wyświetlona nowa karta służąca do konfigurowania zestawu danych. Zestaw danych powinien być też widoczny w widoku drzewa. W oknie **Właściwości** zmień nazwę zestawu danych na **ChangeTrackingDataset**.
4. Przejdź do karty **Połączenie** i wykonaj następujące czynności: 
    
    1. Wybierz wartość **AzureSqlDatabaseLinkedService** w polu **Połączona usługa**. 
    2. Wybierz pozycję **[dbo]. [wersja_rozwiązania_ChangeTracking_magazynu_tabel]** w polu **Tabela**. 

## <a name="create-a-pipeline-for-the-full-copy"></a>Tworzenie potoku na potrzeby pełnego kopiowania
W tym kroku utworzysz potok z działaniem kopiowania, które kopiuje wszystkie dane z magazynu danych źródłowych (baza danych Azure SQL Database) do docelowego magazynu danych (magazyn Azure Blob Storage).

1. Kliknij pozycję **+ (plus)** w lewym okienku, a następnie kliknij pozycję **Potok**. 

    ![Menu Nowy potok](./media/tutorial-incremental-copy-change-tracking-feature-portal/new-pipeline-menu.png)
2. Zostanie wyświetlona nowa karta służąca do konfigurowania potoku. Potok powinien być też widoczny w widoku drzewa. W oknie **Właściwości** zmień nazwę potoku na **FullCopyPipeline**.

    ![Menu Nowy potok](./media/tutorial-incremental-copy-change-tracking-feature-portal/full-copy-pipeline-name.png)
3. W przyborniku **Działania** rozwiń pozycję **Przepływ danych**, a następnie przeciągnij i upuść działanie **Copy** (Kopiowanie) do powierzchni projektanta potoku i ustaw nazwę **FullCopyActivity**. 

    ![Nazwa pełnego działania Copy (Kopiowanie)](./media/tutorial-incremental-copy-change-tracking-feature-portal/full-copy-activity-name.png)
4. Przejdź na kartę **Źródło** i wybierz pozycję **SourceDataset** w polu **Zestaw danych będący źródłem**. 

    ![Działanie Copy (Kopiowanie) — źródło](./media/tutorial-incremental-copy-change-tracking-feature-portal/copy-activity-source.png)
5. Przejdź na kartę **Sink** i wybierz pozycję **SinkDataset** w polu **Zestaw danych będący ujściem**. 

    ![Działanie Copy (Kopiowanie) — ujście](./media/tutorial-incremental-copy-change-tracking-feature-portal/copy-activity-sink.png)
6. Aby zweryfikować definicję potoku, kliknij pozycję **Weryfikuj** na pasku narzędzi. Potwierdź, że weryfikacja nie zwróciła błędu. Zamknij okno **Raport weryfikacji potoku**, klikając pozycję **>>**. 

    ![Weryfikowanie potoku](./media/tutorial-incremental-copy-change-tracking-feature-portal/full-copy-pipeline-validate.png)
7. Aby opublikować jednostki (połączone usługi, zestawy danych i potoki), kliknij pozycję **Opublikuj**. Poczekaj na pomyślne zakończenie publikowania. 

    ![Przycisk Opublikuj](./media/tutorial-incremental-copy-change-tracking-feature-portal/publish-button.png)
8. Poczekaj na wyświetlenie komunikatu **Pomyślnie opublikowano**. 

    ![Publikowanie powiodło się](./media/tutorial-incremental-copy-change-tracking-feature-portal/publishing-succeeded.png)
9. Powiadomienia można również wyświetlić, klikając przycisk **Pokaż powiadomienia** po lewej stronie. Aby zamknąć okno powiadomień, kliknij przycisk **X**.

    ![Wyświetlanie powiadomień](./media/tutorial-incremental-copy-change-tracking-feature-portal/show-notifications.png)


### <a name="run-the-full-copy-pipeline"></a>Uruchamianie potoku pełnego kopiowania
Kliknij pozycję **Wyzwól** na pasku narzędzi dla potoku, a następnie kliknij pozycję **Wyzwól teraz**. 

![Menu Wyzwól teraz](./media/tutorial-incremental-copy-change-tracking-feature-portal/trigger-now-menu.png)

### <a name="monitor-the-full-copy-pipeline"></a>Monitorowanie potoku pełnego kopiowania

1. Kliknij kartę **Monitorowanie** po lewej stronie. Na liście zostanie wyświetlone uruchomienie potoku i jego stan. Aby odświeżyć listę, kliknij pozycję **Odśwież**. Linki w kolumnie Działania umożliwiają wyświetlanie uruchomień działań skojarzonych z uruchomieniem potoku oraz ponowne uruchamianie potoku. 

    ![Uruchomienia potoków](./media/tutorial-incremental-copy-change-tracking-feature-portal/monitor-full-copy-pipeline-run.png)
2. Aby wyświetlić uruchomienia działań skojarzone z uruchomieniem potoku, kliknij link **Wyświetl uruchomienia działań** w kolumnie **Akcje**. W potoku jest tylko jedno działanie, dlatego na liście jest wyświetlana tylko jedna pozycja. Aby powrócić do widoku Uruchomienia potoku, kliknij link **Potoki** u góry strony. 

    ![Uruchomienia działania](./media/tutorial-incremental-copy-change-tracking-feature-portal/activity-runs-full-copy.png)

### <a name="review-the-results"></a>Sprawdzanie wyników
Zostanie wyświetlony plik o nazwie `incremental-<GUID>.txt` w folderze `incchgtracking` kontenera `adftutorial`. 

![Plik wyjściowy z pełnego kopiowania](media\tutorial-incremental-copy-change-tracking-feature-portal\full-copy-output-file.png)

Ten plik powinien zawierać dane z bazy danych Azure SQL Database:

```
1,aaaa,21
2,bbbb,24
3,cccc,20
4,dddd,26
5,eeee,22
```

## <a name="add-more-data-to-the-source-table"></a>Dodawanie większej ilości danych do tabeli źródłowej

Uruchom następujące zapytanie względem bazy danych Azure SQL Database, aby dodać wiersz, a następnie go zaktualizować. 

```sql
INSERT INTO data_source_table
(PersonID, Name, Age)
VALUES
(6, 'new','50');


UPDATE data_source_table
SET [Age] = '10', [name]='update' where [PersonID] = 1

``` 

## <a name="create-a-pipeline-for-the-delta-copy"></a>Tworzenie potoku na potrzeby kopii przyrostowej
W tym kroku utworzysz potok z następującymi działaniami, który będzie okresowo uruchamiany. Za pomocą **działań wyszukiwania** zostanie pobrana stara i nowa wartość parametru SYS_CHANGE_VERSION z bazy danych Azure SQL Database, która zostanie następnie przekazana do działania kopiowania. Za pomocą **działania kopiowania** zostaną skopiowane wstawione, zaktualizowane lub usunięte dane między dwiema wartościami parametru SYS_CHANGE_VERSION z bazy danych Azure SQL Database do magazynu Azure Blob Storage. Za pomocą **działania procedury składowanej** zostanie zaktualizowana wartość parametru SYS_CHANGE_VERSION na potrzeby następnego uruchomienia potoku.

1. W interfejsie użytkownika usługi Data Factory, przejdź na kartę **Edycja**. Kliknij pozycję **+ (plus)** w lewym okienku, a następnie kliknij pozycję **Potok**. 

    ![Menu Nowy potok](./media/tutorial-incremental-copy-change-tracking-feature-portal/new-pipeline-menu-2.png)
2. Zostanie wyświetlona nowa karta służąca do konfigurowania potoku. Potok powinien być też widoczny w widoku drzewa. W oknie **Właściwości** zmień nazwę potoku na **IncrementalCopyPipeline**.

    ![Nazwa potoku](./media/tutorial-incremental-copy-change-tracking-feature-portal/incremental-copy-pipeline-name.png)
3. Rozwiń pozycję **SQL Database** w przyborniku **Działania**, a następnie przeciągnij i upuść działanie **Lookup** (Wyszukiwanie) do powierzchni projektanta potoku. Ustaw nazwę działania na **LookupLastChangeTrackingVersionActivity**. To działanie pobiera wersję rozwiązania Change Tracking używaną podczas ostatniej operacji kopiowania, które jest przechowywana w tabeli **wersja_rozwiązania_ChangeTracking_magazynu_tabel**.

    ![Działanie Lookup (Wyszukiwanie) — nazwa](./media/tutorial-incremental-copy-change-tracking-feature-portal/first-lookup-activity-name.png)
4. Przejdź do obszaru **Ustawienia** w oknie **Właściwości** i wybierz pozycję **ChangeTrackingDataset** w polu **Źródłowy zestaw danych**. 

    ![Działanie Lookup (Wyszukiwanie) — ustawienia](./media/tutorial-incremental-copy-change-tracking-feature-portal/first-lookup-activity-settings.png)
5. Przeciągnij działanie **Lookup** (Wyszukiwanie) z przybornika **Działania** do powierzchni projektanta potoku. Ustaw nazwę działania na **LookupCurrentChangeTrackingVersionActivity**. To działanie pobiera bieżącą wersję rozwiązania Change Tracking.

    ![Działanie Lookup (Wyszukiwanie) — nazwa](./media/tutorial-incremental-copy-change-tracking-feature-portal/second-lookup-activity-name.png)
6. Przejdź do karty **Ustawienia** w oknie **Właściwości** i wykonaj następujące czynności:

    1. Wybierz pozycję **SourceDataset** dla pola **Zestaw danych będący źródłem**.
    2. Wybierz pozycję **Zapytanie** w polu **Użyj zapytania**. 
    3. W obszarze **Zapytanie** wprowadź następujące zapytanie SQL. 

        ```sql
        SELECT CHANGE_TRACKING_CURRENT_VERSION() as CurrentChangeTrackingVersion
        ```

    ![Działanie Lookup (Wyszukiwanie) — ustawienia](./media/tutorial-incremental-copy-change-tracking-feature-portal/second-lookup-activity-settings.png)
7. W przyborniku **Działania** rozwiń pozycję **Przepływ danych**, a następnie przeciągnij i upuść działanie **Copy** (Kopiowanie) do powierzchni projektanta potoku. Ustaw nazwę działania na **IncrementalCopyActivity**. To działanie kopiuje dane między ostatnią i bieżącą wersją rozwiązania Change Tracking w docelowym magazynie danych. 

    ![Działanie Copy (Kopiowanie) — nazwa](./media/tutorial-incremental-copy-change-tracking-feature-portal/incremental-copy-activity-name.png)
8. Przejdź do karty **Źródło** w oknie **Właściwości** i wykonaj następujące czynności:

    1. Wybierz pozycję **SourceDataset** w obszarze **Zestaw danych będący źródłem**. 
    2. Wybierz pozycję **Zapytanie** w polu **Użyj zapytania**. 
    3. W obszarze **Zapytanie** wprowadź następujące zapytanie SQL. 

        ```sql
        select data_source_table.PersonID,data_source_table.Name,data_source_table.Age, CT.SYS_CHANGE_VERSION, SYS_CHANGE_OPERATION from data_source_table RIGHT OUTER JOIN CHANGETABLE(CHANGES data_source_table, @{activity('LookupLastChangeTrackingVersionActivity').output.firstRow.SYS_CHANGE_VERSION}) as CT on data_source_table.PersonID = CT.PersonID where CT.SYS_CHANGE_VERSION <= @{activity('LookupCurrentChangeTrackingVersionActivity').output.firstRow.CurrentChangeTrackingVersion}
        ```
    
    ![Działanie Copy (Kopiowanie) — ustawienia źródła](./media/tutorial-incremental-copy-change-tracking-feature-portal/inc-copy-source-settings.png)
9. Przejdź na kartę **Sink** i wybierz pozycję **SinkDataset** w polu **Zestaw danych będący ujściem**. 

    ![Działanie Copy (Kopiowanie) — ustawienia ujścia](./media/tutorial-incremental-copy-change-tracking-feature-portal/inc-copy-sink-settings.png)
10. **Połącz działania Lookup (Wyszukiwanie) z działaniem Copy (Kopiowanie)** — po kolei. Przeciągnij **zielony** przycisk dołączony do działania **Lookup** (Wyszukiwanie) do działania **Copy** (Kopiowanie). 

    ![Łączenie działań Lookup (Wyszukiwanie) i Copy (Kopiowanie)](./media/tutorial-incremental-copy-change-tracking-feature-portal/connect-lookup-and-copy.png)
11. Przeciągnij działanie **Stored Procedure** (Procedura składowana) z przybornika **Działania** do powierzchni projektanta potoku. Ustaw nazwę działania na **StoredProceduretoUpdateChangeTrackingActivity**. To działanie aktualizuje wersję rozwiązania Change Tracking w tabeli **wersja_rozwiązania_ChangeTracking_magazynu_danych**.

    ![Działanie procedury składowanej — nazwa](./media/tutorial-incremental-copy-change-tracking-feature-portal/stored-procedure-activity-name.png)
12. Przejdź do karty *Konto SQL** i wybierz wartość **AzureSqlDatabaseLinkedService** w polu **Połączona usługa**. 

    ![Działanie Stored Procedure (Procedura składowana) — konto SQL](./media/tutorial-incremental-copy-change-tracking-feature-portal/sql-account-tab.png)
13. Przejdź do karty **Procedura składowana** i wykonaj następujące czynności: 

    1. Wprowadź wartość **Update_ChangeTracking_Version** w polu **nazwy procedury składowanej**.  
    2. W sekcji **Parametry procedury składowanej** użyj przycisku **+ Nowy**, aby dodać dwa poniższe parametry:

        | Name (Nazwa) | Typ | Wartość | 
        | ---- | ---- | ----- | 
        | CurrentTrackingVersion | INT64 | @{activity('LookupCurrentChangeTrackingVersionActivity').output.firstRow.CurrentChangeTrackingVersion} | 
        | TableName | Ciąg | @{activity('LookupLastChangeTrackingVersionActivity').output.firstRow.TableName} | 
    
        ![Działanie Stored Procedure (Procedura składowana) — parametry](./media/tutorial-incremental-copy-change-tracking-feature-portal/stored-procedure-parameters.png)
14. **Połącz działanie Copy (Kopiowanie) z działaniem Stored Procedure (Procedura składowana)**. Przeciągnij i upuść **zielony** przycisk dołączony do działania Copy (Kopiowanie) w obszarze działania Stored Procedure (Procedura składowana). 

    ![Łączenie działań Copy (Kopiowanie) i Stored Procedure (Procedura składowana)](./media/tutorial-incremental-copy-change-tracking-feature-portal/connect-copy-stored-procedure.png)
15. Na pasku narzędzi kliknij pozycję **Weryfikuj**. Potwierdź, że weryfikacja nie zwróciła błędów. Zamknij okno **Raport weryfikacji potoku**, klikając pozycję **>>**. 

    ![Przycisk Weryfikuj](./media/tutorial-incremental-copy-change-tracking-feature-portal/validate-button.png)
16.  Opublikuj jednostki (usługi połączone, zestawy danych i potoki) w usłudze Data Factory, klikając przycisk **Publikuj**. Poczekaj na wyświetlenie komunikatu **Publikowanie powiodło się**. 

        ![Przycisk Opublikuj](./media/tutorial-incremental-copy-change-tracking-feature-portal/publish-button-2.png)    

### <a name="run-the-incremental-copy-pipeline"></a>Uruchamianie potoku kopiowania przyrostowego
Kliknij pozycję **Wyzwól** na pasku narzędzi dla potoku, a następnie kliknij pozycję **Wyzwól teraz**. 

![Menu Wyzwól teraz](./media/tutorial-incremental-copy-change-tracking-feature-portal/trigger-now-menu-2.png)

### <a name="monitor-the-incremental-copy-pipeline"></a>Monitorowanie potoku kopiowania przyrostowego
1. Kliknij kartę **Monitorowanie** po lewej stronie. Na liście zostanie wyświetlone uruchomienie potoku i jego stan. Aby odświeżyć listę, kliknij pozycję **Odśwież**. Linki w kolumnie **Działania** umożliwiają wyświetlanie uruchomień działań skojarzonych z uruchomieniem potoku oraz ponowne uruchamianie potoku. 

    ![Uruchomienia potoków](./media/tutorial-incremental-copy-change-tracking-feature-portal/inc-copy-pipeline-runs.png)
2. Aby wyświetlić uruchomienia działań skojarzone z uruchomieniem potoku, kliknij link **Wyświetl uruchomienia działań** w kolumnie **Akcje**. W potoku jest tylko jedno działanie, dlatego na liście jest wyświetlana tylko jedna pozycja. Aby powrócić do widoku Uruchomienia potoku, kliknij link **Potoki** u góry strony. 

    ![Uruchomienia działania](./media/tutorial-incremental-copy-change-tracking-feature-portal/inc-copy-activity-runs.png)


### <a name="review-the-results"></a>Sprawdzanie wyników
W folderze `incchgtracking` kontenera `adftutorial` widoczny będzie drugi plik. 

![Plik wyjściowy z kopii przyrostowej](media\tutorial-incremental-copy-change-tracking-feature-portal\incremental-copy-output-file.png)

Ten plik powinien zawierać tylko dane przyrostowe z bazy danych Azure SQL Database. Rekord z wartością `U` znajduje się w zaktualizowanym wierszu w bazie danych, a rekord z wartością `I` to jeden dodany wiersz. 

```
1,update,10,2,U
6,new,50,1,I
```
Pierwsze trzy kolumny to zmienione dane z tabeli data_source_table. Ostatnie dwie kolumny to metadane z tabeli systemowej śledzenia zmian. Czwarta kolumna to wartość parametru SYS_CHANGE_VERSION dla każdego zmienionego wiersza. Piąta kolumna to wartość operacji: U — aktualizacja, I — wstawienie.  Aby uzyskać szczegółowe informacje o śledzeniu zmian, zobacz [CHANGETABLE](/sql/relational-databases/system-functions/changetable-transact-sql). 

```
==================================================================
PersonID Name    Age    SYS_CHANGE_VERSION    SYS_CHANGE_OPERATION
==================================================================
1        update  10     2                     U
6        new     50     1                     I
```

    
## <a name="next-steps"></a>Następne kroki
Przejdź do następującego samouczka, aby dowiedzieć się więcej o przekształcaniu danych za pomocą klastra Spark na platformie Azure:

> [!div class="nextstepaction"]
>[Przekształcanie danych przy użyciu klastra Spark w chmurze](tutorial-transform-data-spark-portal.md)



