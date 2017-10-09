---
title: "dane aaaMove — brama zarządzania danymi | Dokumentacja firmy Microsoft"
description: "Konfigurowanie danych toomove bramy danych między lokalnymi i hello chmury. Użyj bramy zarządzania danymi w fabryce danych Azure toomove danych."
keywords: "Brama danych, integracja danych przenoszenia danych, poświadczeń bramy"
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: 7bf6d8fd-04b5-499d-bd19-eff217aa4a9c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
ms.openlocfilehash: 314341c142d5260c785b7e82081774f044450e81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-between-on-premises-sources-and-hello-cloud-with-data-management-gateway"></a>Przenoszenie danych między lokalnych źródeł i w chmurze hello z brama zarządzania danymi
Ten artykuł zawiera omówienie integrację danych lokalnych magazynów danych i magazyny danych chmury przy użyciu fabryki danych. Opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu i innych danych fabryki podstawowe pojęcia dotyczące artykułów: [zestawów danych](data-factory-create-datasets.md) i [potoki](data-factory-create-pipelines.md).

## <a name="data-management-gateway"></a>Brama zarządzania danymi
Brama zarządzania danymi należy zainstalować na Twojej tooenable maszyny lokalnej przenoszenia danych z lokalnego magazynu danych. Brama Hello może zostać zainstalowana na powitania, które same komputera jako magazynu danych hello lub na innym komputerze, tak długo, jak brama hello można połączyć z usługą Magazyn danych toohello.

> [!IMPORTANT]
> Zobacz [brama zarządzania danymi](data-factory-data-management-gateway.md) artykułu, aby uzyskać więcej informacji dotyczących bramy zarządzania danymi. 

Witaj następujące przewodniku zademonstrowano, jak toocreate fabryki danych z potok, który przenosi dane z lokalnymi **programu SQL Server** bazy danych magazynu obiektów blob Azure tooan. W ramach hello wskazówki zainstalowaniu i skonfigurowaniu hello brama zarządzania danymi na tym komputerze.

## <a name="walkthrough-copy-on-premises-data-toocloud"></a>Wskazówki: kopiowanie lokalnych danych toocloud
W tym przewodniku hello następujące kroki: 

1. Tworzenie fabryki danych.
2. Tworzenie bramy zarządzania danymi. 
3. Tworzenie połączonej usługi dla źródłowy i odbiorczy magazynów danych.
4. Utwórz dane wejściowe toorepresent zestawów danych i dane wyjściowe.
5. Utworzyć potok z danych hello toomove działania kopiowania.

## <a name="prerequisites-for-hello-tutorial"></a>Wymagania wstępne dotyczące samouczka hello
Przed rozpoczęciem tego przewodnika, musi mieć hello następujące wymagania wstępne:

* **Subskrypcja platformy Azure**.  Jeśli nie masz subskrypcji, możesz utworzyć konto bezpłatnej wersji próbnej w zaledwie kilka minut. Zobacz hello [bezpłatnej wersji próbnej](http://azure.microsoft.com/pricing/free-trial/) artykułu, aby uzyskać szczegółowe informacje.
* **Konto magazynu Azure**. Użyj magazynu obiektów blob hello **docelowego/ujście** magazynu danych, w tym samouczku. Jeśli nie masz konta magazynu platformy Azure, zobacz hello [Utwórz konto magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account) artykuł, aby toocreate kroki, jeden.
* **SQL Server**. Użyj lokalnej bazy danych programu SQL Server jako **źródła** magazynu danych w tym samouczku. 

## <a name="create-data-factory"></a>Tworzenie fabryki danych
W tym kroku użyjesz hello Azure toocreate portalu o nazwie wystąpienia fabryki danych Azure **ADFTutorialOnPremDF**.

1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com).
2. Kliknij przycisk **+ nowy**, kliknij przycisk **analizy i analiza**i kliknij przycisk **fabryki danych**.

   ![Nowy-> Fabryka danych](./media/data-factory-move-data-between-onprem-and-cloud/NewDataFactoryMenu.png)  
3. W hello **nowa fabryka danych** wprowadź **ADFTutorialOnPremDF** dla hello nazwy.

    ![Dodaj tooStartboard](./media/data-factory-move-data-between-onprem-and-cloud/OnPremNewDataFactoryAddToStartboard.png)

   > [!IMPORTANT]
   > Nazwa fabryki danych Azure hello Hello musi być globalnie unikatowe. Jeśli wystąpi błąd hello: **nazwa fabryki danych "ADFTutorialOnPremDF" nie jest dostępna**, Zmień nazwę hello hello fabryki danych (na przykład yournameADFTutorialOnPremDF) i spróbuj ponownie utworzyć. Użyj tej nazwy, zamiast ADFTutorialOnPremDF podczas wykonywania pozostałych czynności w tym samouczku.
   >
   > Nazwa fabryki danych hello Hello może zostać zarejestrowana jako **DNS** nazwy w przyszłości hello i dlatego stać się publicznie widoczna.
   >
   >
4. Wybierz hello **subskrypcji platformy Azure** miejscu toobe fabryki danych hello utworzony.
5. Wybierz istniejącą **grupę zasobów** lub utwórz grupę zasobów. Samouczek hello, Utwórz grupę zasobów o nazwie: **ADFTutorialResourceGroup**.
6. Kliknij przycisk **Utwórz** na powitania **nowa fabryka danych** strony.

   > [!IMPORTANT]
   > toocreate wystąpienia fabryki danych, musi być członkiem hello [współautora fabryki danych](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) roli na poziomie grupy zasobów subskrypcji hello.
   >
   >
7. Po zakończeniu tworzenia Zobacz hello **fabryki danych** strony, jak pokazano w powitania po obrazu:

   ![Strona główna fabryki danych](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDataFactoryHomePage.png)

## <a name="create-gateway"></a>Tworzenie bramy
1. W hello **fabryki danych** kliknij przycisk **tworzenie i wdrażanie** hello toolaunch kafelka **edytora** hello fabryki danych.

    ![Kafelek Utwórz i wdróż](./media/data-factory-move-data-between-onprem-and-cloud/author-deploy-tile.png)
2. W hello Edytor fabryki danych, kliknij przycisk **... Więcej** na hello narzędzi, a następnie kliknij przycisk **nowej bramy danych**. Alternatywnie możesz kliknąć prawym przyciskiem myszy **bram danych** w hello widok drzewa i kliknij przycisk **nowej bramy danych**.

   ![Nową bramę danych na pasku narzędzi](./media/data-factory-move-data-between-onprem-and-cloud/NewDataGateway.png)
3. W hello **Utwórz** wprowadź **adftutorialgateway** dla hello **nazwa**i kliknij przycisk **OK**.     

    ![Utwórz stronę bramy](./media/data-factory-move-data-between-onprem-and-cloud/OnPremCreateGatewayBlade.png)

    > [!NOTE]
    > W tym przewodniku należy utworzyć bramę logicznej hello z tylko jeden węzeł (komputera lokalnego systemu Windows). Możesz skalować w poziomie bramy zarządzania danymi hello bramy można skojarzyć wielu komputerach lokalnych. Możesz skalować w górę zwiększając liczbę zadań przepływu danych, które można uruchomić jednocześnie w węźle. Ta funkcja jest również dostępny do logicznego bramy z jednego węzła. Zobacz [skalowanie brama zarządzania danymi w fabryce danych Azure](data-factory-data-management-gateway-high-availability-scalability.md) artykułu, aby uzyskać szczegółowe informacje.  
4. W hello **Konfiguruj** kliknij przycisk **Zainstaluj bezpośrednio na tym komputerze**. Ta akcja pobiera hello pakiet instalacyjny bramy hello, instaluje konfiguruje i rejestruje hello bramę na komputerze hello.  

   > [!NOTE]
   > Użyj programu Internet Explorer lub przeglądarki sieci web zgodne Microsoft ClickOnce.
   >
   > Jeśli używasz programu Chrome, przejdź toohello [sklepu Chrome web store](https://chrome.google.com/webstore/), wyszukaj ze słowem kluczowym "ClickOnce", wybierz jedno z rozszerzeń ClickOnce hello i zainstaluj go.
   >
   > Witaj tego samego dla przeglądarki Firefox (Instalowanie dodatku). Kliknij przycisk **Otwórz Menu** przycisk na pasku narzędzi hello (**trzy poziome linie** w hello prawym górnym rogu), kliknij przycisk **dodatki**, wyszukaj ze słowem kluczowym "ClickOnce", wybierz jedną z hello Rozszerzenia ClickOnce, a następnie zainstaluj go.    
   >
   >

    ![Brama — Konfigurowanie strony](./media/data-factory-move-data-between-onprem-and-cloud/OnPremGatewayConfigureBlade.png)

    W ten sposób jest hello Najprostszym sposobem (jednym kliknięciem) toodownload, zainstalować, skonfigurować i zarejestrować bramę hello w jeden pojedynczy krok. Zostanie wyświetlony hello **Menedżera konfiguracji bramy zarządzania danymi firmy Microsoft** aplikacja jest zainstalowana na tym komputerze. Możesz również znaleźć hello wykonywalnego **ConfigManager.exe** w folderze hello: **C:\Program Files\Microsoft danych zarządzania Gateway\2.0\Shared**.

    Można również pobrać i zainstalować bramę ręcznie przy użyciu łącza hello na tej stronie i zarejestrowanie go za pomocą klucza hello pokazano hello **nowy klucz** pola tekstowego.

    Zobacz [brama zarządzania danymi](data-factory-data-management-gateway.md) artykułu dla wszystkich hello szczegółowe informacje o hello bramy.

   > [!NOTE]
   > Należy mieć uprawnienia administratora na powitania tooinstall komputera lokalnego i pomyślnie skonfigurować hello brama zarządzania danymi. Możesz dodać kolejnych użytkowników toohello **użytkownicy bramy zarządzania danymi** lokalnej grupy systemu Windows. Witaj członkami tej grupy można użyć hello Menedżera konfiguracji bramy zarządzania danymi narzędzia tooconfigure hello bramy.
   >
   >
5. Poczekaj kilka minut lub poczekaj na wyświetlenie hello następującego komunikatu powiadomienia:

    ![Pomyślnie zainstalowano bramy](./media/data-factory-move-data-between-onprem-and-cloud/gateway-install-success.png)
6. Uruchom **Menedżera konfiguracji bramy zarządzania danymi** aplikacji na komputerze. W hello **wyszukiwania** wpisz **brama zarządzania danymi** tooaccess tego narzędzia. Możesz również znaleźć hello wykonywalnego **ConfigManager.exe** w folderze hello: **C:\Program Files\Microsoft danych zarządzania Gateway\2.0\Shared**

    ![Menedżer konfiguracji bramy](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDMGConfigurationManager.png)
7. Upewnij się, że widoczny `adftutorialgateway is connected toohello cloud service` wiadomości. Witaj pasek Wyświetla dolnej hello stanu **połączona usługa w chmurze toohello** wraz z **zielony znacznik wyboru**.

    Na powitania **Home** karcie, możesz również wykonać hello następujące operacje:

   * **Zarejestruj** bramy przy użyciu klucza z portalu Azure za pomocą przycisku Zarejestruj hello hello.
   * **Zatrzymaj** hello danych usługa hosta bramy zarządzania na komputerze bramy.
   * **Zaplanuj aktualizacje** toobe zainstalowany w określonym czasie hello dnia.
   * Widoku, gdy został bramy hello **ostatniej aktualizacji**.
   * Określ czas, w którym można zainstalować bramę toohello aktualizacji.
8. Przełącz toohello **ustawienia** kartę hello certyfikatu podanego w hello **certyfikatu** sekcja jest używane tooencrypt/odszyfrowywania poświadczenia dla magazynu danych lokalnych hello określoną na powitania portalu. (opcjonalnie) Kliknij przycisk **zmiany** toouse własnego certyfikatu zamiast tego. Domyślnie przy użyciu brama hello hello certyfikatu, który został wygenerowany automatycznie przez hello usługi fabryka danych.

    ![Konfiguracja certyfikatu bramy](./media/data-factory-move-data-between-onprem-and-cloud/gateway-certificate.png)

    Możesz również wykonać hello następujących czynności na powitania **ustawienia** karty:

   * Wyświetl lub wyeksportować certyfikat hello jest używany przez bramę hello.
   * Zmień punkt końcowy HTTPS hello używany przez bramę hello.    
   * Ustaw toobe serwera proxy HTTP używany przez bramę hello.     
9. (opcjonalnie) Przełącz toohello **diagnostyki** pozycję Sprawdź hello **Włącz pełne rejestrowanie** opcję, jeśli chcesz tooenable pełne rejestrowanie, której można tootroubleshoot wszelkie problemy z bramą hello. Witaj rejestrowane informacje znajdują się w **Podgląd zdarzeń** w obszarze **Dzienniki aplikacji i usług** -> **brama zarządzania danymi** węzła.

    ![Karta diagnostyki](./media/data-factory-move-data-between-onprem-and-cloud/diagnostics-tab.png)

    Można również wykonać następujące akcje w hello hello **diagnostyki** karty:

   * Użyj **Testuj połączenie** sekcji tooan lokalnego źródła danych przy użyciu bramy hello.
   * Kliknij przycisk **Wyświetl dzienniki** hello toosee brama zarządzania danymi logowania w oknie Podgląd zdarzeń.
   * Kliknij przycisk **Wyślij dzienniki** tooupload z dziennikami z ostatnich siedmiu dni tooMicrosoft toofacilitate rozwiązywania problemów z problemów związanych z pliku zip.
10. Na powitania **diagnostyki** na karcie hello **Testuj połączenie** zaznacz **SqlServer** hello typu danych hello przechowywania, wprowadź nazwę hello powitania serwera bazy danych, nazwę Witaj bazy danych, określ typ uwierzytelniania, wprowadź nazwę użytkownika i hasło i kliknij przycisk **testu** tootest czy brama hello można połączyć z usługą toohello bazy danych.
11. Przełącznik toohello przeglądarki sieci web w hello **portalu Azure**, kliknij przycisk **OK** na powitania **Konfiguruj** strony, a następnie na powitania **nowej bramy danych** Strona.
12. Powinny pojawić się **adftutorialgateway** w obszarze **bram danych** w widoku drzewa hello powitania po lewej stronie.  Jeśli klikniesz przycisk, powinien pojawić się hello skojarzone JSON.

## <a name="create-linked-services"></a>Tworzenie połączonych usług
W tym kroku, Utwórz dwie połączonej usługi: **AzureStorageLinkedService** i **SqlServerLinkedService**. Witaj **SqlServerLinkedService** łączy lokalną bazą danych programu SQL Server i hello **AzureStorageLinkedService** połączonej usługi łączy fabrykę danych toohello magazynu obiektów blob platformy Azure. W dalszej części tego przewodnika, który kopiuje dane z magazynu obiektów blob platformy Azure toohello bazy danych w programu SQL Server lokalne hello jest utworzyć potok.

#### <a name="add-a-linked-service-tooan-on-premises-sql-server-database"></a>Dodawanie bazy danych programu SQL Server połączonej usługi tooan lokalnej
1. W hello **Edytor fabryki danych**, kliknij przycisk **nowy magazyn danych** na powitania narzędzi i wybierz **programu SQL Server**.

   ![Nowa usługa SQL Server połączone](./media/data-factory-move-data-between-onprem-and-cloud/NewSQLServer.png)
2. W hello **edytora JSON** na powitania prawo, hello następujące kroki:

   1. Dla hello **gatewayName**, określ **adftutorialgateway**.    
   2. W hello **connectionString**, hello następujące kroki:    

      1. Aby uzyskać **servername**, wprowadź nazwę hello powitania serwera, który hostuje hello bazy danych SQL Server.
      2. Aby uzyskać **databasename**, wprowadź nazwę hello hello bazy danych.
      3. Kliknij przycisk **Szyfruj** przycisk na powitania narzędzi. Zostanie wyświetlony hello aplikacji Menedżera poświadczeń.

         ![Aplikacja Menedżera poświadczeń](./media/data-factory-move-data-between-onprem-and-cloud/credentials-manager-application.png)
      4. W hello **ustawienie poświadczeń** okno dialogowe, określ typ uwierzytelniania, nazwę użytkownika i hasło, a następnie kliknij przycisk **OK**. W przypadku pomyślnego nawiązania połączenia hello hello zaszyfrowane poświadczenia są przechowywane w hello JSON i zamyka okno dialogowe hello.
      5. Zamknij kartę puste przeglądarki hello uruchomić okno dialogowe hello, jeśli nie zostaną automatycznie zamknięte i wrócić toohello kartę hello portalu Azure.

         Na komputerze bramy hello, te poświadczenia są **zaszyfrowanych** za pomocą certyfikatu, który hello fabryki danych jest właścicielem usługi. Jeśli chcesz toouse hello certyfikatu, który jest skojarzony z hello brama zarządzania danymi zamiast tego zobacz [bezpiecznie ustawić poświadczenia](#set-credentials-and-security).    
   3. Kliknij przycisk **Wdróż** na pasku hello toodeploy usługi SQL Server połączone poleceń hello. Usługa hello połączone w widoku drzewa hello powinna zostać wyświetlona.

      ![Usługi SQL Server połączone w widoku drzewa hello](./media/data-factory-move-data-between-onprem-and-cloud/sql-linked-service-in-tree-view.png)    

#### <a name="add-a-linked-service-for-an-azure-storage-account"></a>Dodaj połączonej usługi dla konta magazynu platformy Azure
1. W hello **Edytor fabryki danych**, kliknij przycisk **nowy magazyn danych** hello pasek poleceń i kliknij przycisk **magazynu Azure**.
2. Wprowadź nazwę hello konta magazynu Azure hello **nazwa konta**.
3. Wprowadź klucz powitania dla konta magazynu Azure hello **klucz konta**.
4. Kliknij przycisk **Wdróż** toodeploy hello **AzureStorageLinkedService**.

## <a name="create-datasets"></a>Tworzenie zestawów danych
W tym kroku Tworzenie danych wejściowych i wyjściowych zestawów danych, które zawierają dane wejściowe i wyjściowe dla operacji kopiowania hello (bazy danych serwera SQL lokalnymi = > magazynu obiektów blob platformy Azure). Przed utworzeniem zestawów danych, hello następujące kroki (szczegółowy opis kroków następująca liście hello):

* Tworzenie tabeli o nazwie **pustych elementów** w hello dodany jako fabryki danych toohello połączonej usługi bazy danych serwera SQL i Wstaw kilka przykładowych wpisów do tabeli hello.
* Tworzenie kontenera obiektów blob o nazwie **adftutorial** w hello Azure blob dodany jako połączonej usługi fabryki danych toohello konta magazynu.

### <a name="prepare-on-premises-sql-server-for-hello-tutorial"></a>Przygotowanie lokalnego programu SQL Server w samouczku hello
1. W bazie danych hello określony dla hello lokalnego programu SQL Server połączone usługi (**SqlServerLinkedService**), użyj powitania po hello toocreate skryptu SQL **pustych elementów** tabeli w bazie danych hello.

    ```SQL   
    CREATE TABLE dbo.emp
    (
        ID int IDENTITY(1,1) NOT NULL,
        FirstName varchar(50),
        LastName varchar(50),
        CONSTRAINT PK_emp PRIMARY KEY (ID)
    )
    GO
    ```
2. Wstaw niektóre przykładowe do tabeli hello:

    ```SQL
    INSERT INTO emp VALUES ('John', 'Doe')
    INSERT INTO emp VALUES ('Jane', 'Doe')
    ```

### <a name="create-input-dataset"></a>Tworzenie wejściowego zestawu danych

1. W hello **Edytor fabryki danych**, kliknij przycisk **... Więcej**, kliknij przycisk **nowy zestaw danych** hello pasek poleceń i kliknij przycisk **tabeli programu SQL Server**.
2. Zastąp hello JSON w okienku po prawej stronie powitania hello następującego tekstu:

    ```JSON   
    {        
        "name": "EmpOnPremSQLTable",
        "properties": {
            "type": "SqlServerTable",
            "linkedServiceName": "SqlServerLinkedService",
            "typeProperties": {
                "tableName": "emp"
            },
            "external": true,
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "externalData": {
                    "retryInterval": "00:01:00",
                    "retryTimeout": "00:10:00",
                    "maximumRetry": 3
                }
            }
        }
    }     
    ```     
   Należy zwrócić uwagę hello następujące punkty:

   * **Typ** ustawiono zbyt**SqlServerTable**.
   * **tableName** ustawiono zbyt**pustych elementów**.
   * **linkedServiceName** ustawiono zbyt**SqlServerLinkedService** (tej połączonej usługi ma utworzone we wcześniejszej części tego przewodnika.).
   * Wejściowy zestaw danych nie jest generowany przez inny potok w fabryce danych Azure, należy ustawić **zewnętrznych** za**true**. Wskazuje on, że hello danych wejściowych jest także toohello zewnętrznej usługi fabryka danych Azure. Opcjonalnie można określić żadnych zasad danych zewnętrznych przy użyciu hello **externalData** element hello **zasad** sekcji.    

   Zobacz [przenoszenie danych do/z programu SQL Server](data-factory-sqlserver-connector.md) szczegółowe informacje na temat właściwości JSON.
3. Kliknij przycisk **Wdróż** polecenie hello paska toodeploy hello dataset.  

### <a name="create-output-dataset"></a>Tworzenie wyjściowego zestawu danych

1. W hello **Edytor fabryki danych**, kliknij przycisk **nowy zestaw danych** hello pasek poleceń i kliknij przycisk **magazynu obiektów Blob Azure**.
2. Zastąp hello JSON w okienku po prawej stronie powitania hello następującego tekstu:

    ```JSON   
    {
        "name": "OutputBlobTable",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "folderPath": "adftutorial/outfromonpremdf",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
     }
    ```   
   Należy zwrócić uwagę hello następujące punkty:

   * **Typ** ustawiono zbyt**AzureBlob**.
   * **linkedServiceName** ustawiono zbyt**AzureStorageLinkedService** (w kroku 2 została utworzona tej połączonej usługi).
   * **folderPath** ustawiono zbyt**adftutorial/outfromonpremdf** gdzie outfromonpremdf jest hello w kontenerze adftutorial hello. Utwórz hello **adftutorial** kontener, jeśli jeszcze nie istnieje.
   * Hello **dostępności** ustawiono zbyt**co godzinę** (**częstotliwość** ustawić także**godzina** i **interwał** ustawić także **1**).  Witaj usługi fabryka danych generuje wycinek danych wyjściowych co godzinę w hello **pustych elementów** tabeli w hello bazy danych SQL Azure.

   Jeśli nie określisz **fileName** dla **tabeli wyników**, hello wygenerowanych plików w hello **folderPath** mają nazwy w hello następującego formatu: danych.<Guid>. txt (na przykład:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).

   tooset **folderPath** i **fileName** dynamicznie w oparciu hello **SliceStart** czasu, użyj właściwości partitionedBy hello. W hello poniższy przykład, folderPath korzysta rok, miesiąc i dzień z hello SliceStart (czas rozpoczęcia przetwarzania wycinka hello), a nazwa pliku godzinę z hello SliceStart. Na przykład, jeśli wycinek jest tworzonym dla 2014-10-20T08:00:00, nazwa_folderu hello ustawiono toowikidatagateway/wikisampledataout/2014/10/20 i hello fileName ustawiono too08.csv.

    ```JSON
    "folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
    "fileName": "{Hour}.csv",
    "partitionedBy":
    [

        { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
    ],
    ```

    Zobacz [przenoszenie danych do/z magazynu obiektów Blob Azure](data-factory-azure-blob-connector.md) szczegółowe informacje na temat właściwości JSON.
3. Kliknij przycisk **Wdróż** polecenie hello paska toodeploy hello dataset. Upewnij się, że oba zestawy danych hello w widoku drzewa hello jest widoczny.  

## <a name="create-pipeline"></a>Tworzenie potoku
W tym kroku utworzysz **potoku** z jednym **działanie kopiowania** używającą **EmpOnPremSQLTable** jako dane wejściowe i **OutputBlobTable** jako dane wyjściowe.

1. Kliknij w Edytor fabryki danych **... Więcej** i **Nowy potok**.
2. Zastąp hello JSON w okienku po prawej stronie powitania hello następującego tekstu:    

    ```JSON   
     {
         "name": "ADFTutorialPipelineOnPrem",
         "properties": {
         "description": "This pipeline has one Copy activity that copies data from an on-prem SQL tooAzure blob",
         "activities": [
           {
             "name": "CopyFromSQLtoBlob",
             "description": "Copy data from on-prem SQL server tooblob",
             "type": "Copy",
             "inputs": [
               {
                 "name": "EmpOnPremSQLTable"
               }
             ],
             "outputs": [
               {
                 "name": "OutputBlobTable"
               }
             ],
             "typeProperties": {
               "source": {
                 "type": "SqlSource",
                 "sqlReaderQuery": "select * from emp"
               },
               "sink": {
                 "type": "BlobSink"
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
         "start": "2016-07-05T00:00:00Z",
         "end": "2016-07-06T00:00:00Z",
         "isPaused": false
       }
     }
    ```   
   > [!IMPORTANT]
   > Zastąp wartość hello hello **start** właściwość o hello bieżącego dnia i **zakończenia** wartości z hello następnego dnia.
   >
   >

   Należy zwrócić uwagę hello następujące punkty:

   * W sekcji działania hello jest tylko działania którego **typu** ustawiono zbyt**kopiowania**.
   * **Dane wejściowe** dla działania hello jest ustawiony za**EmpOnPremSQLTable** i **dane wyjściowe** dla działania hello jest ustawiony za**OutputBlobTable**.
   * W hello **typeProperties** sekcji **SqlSource** jest określony jako hello **typ źródła** i ** BlobSink ** jest określony jako hello **sink typu**.
   * Zapytanie SQL `select * from emp` określono hello **sqlReaderQuery** właściwość **SqlSource**.

   Zarówno data/godzina rozpoczęcia, jak i data/godzina zakończenia muszą być w [formacie ISO](http://en.wikipedia.org/wiki/ISO_8601). Na przykład: 2014-10-14T16:32:41Z. Witaj **zakończenia** czasu jest opcjonalne, ale możemy użyć w tym samouczku.

   Jeśli nie określisz wartości hello **zakończenia** właściwości, jest on obliczany jako "**start + 48 godzin**". potok hello toorun przez czas nieokreślony, określ **9/9/9999** jako wartość hello hello **zakończenia** właściwości.

   Definiujesz hello czas trwania w których hello są przetwarzane wycinków danych oparte na powitania **dostępności** właściwości, które zostały zdefiniowane dla każdego zestawu danych z fabryki danych Azure.

   Przykład Witaj istnieją 24 wycinków danych jak każdy wycinek danych jest tworzone co godzinę.        
3. Kliknij przycisk **Wdróż** na pasku toodeploy hello dataset poleceń hello (tabela jest prostokątny zestawu danych). Potwierdzenie tego potoku hello zostaną wyświetlone w widoku drzewa hello w **potoki** węzła.  
4. Teraz, kliknij przycisk **X** dwukrotnie tooclose hello strony tooget wstecz toohello **fabryki danych** stronę hello **ADFTutorialOnPremDF**.

**Gratulacje!** Pomyślnie utworzono fabryki danych Azure, połączone usługi, zestawów danych oraz potoku i zaplanowane hello potoku.

#### <a name="view-hello-data-factory-in-a-diagram-view"></a>Fabryka danych hello widoku w widoku diagramu
1. W hello **portalu Azure**, kliknij przycisk **Diagram** kafelka na stronie głównej hello hello **ADFTutorialOnPremDF** fabryki danych. :

    ![Diagram łącza](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramLink.png)
2. Powinny pojawić się toohello podobne diagram powitania po obrazu:

    ![Widok diagramu](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramView.png)

    Powiększ, pomniejszyć powiększenia too100%, toofit powiększenia, automatycznie potoki pozycji i zestawów danych i Pokaż elementy powiązane informacje (wyróżnia elementy nadrzędne i podrzędne wybranego elementu).  Możesz kliknąć dwukrotnie właściwości toosee obiektu (dataset wejścia/wyjścia lub potoku) dla niego.

## <a name="monitor-pipeline"></a>Monitorowanie potoku
W tym kroku użyjesz hello Azure toomonitor portalu, co się dzieje w fabryce danych Azure. Można również użyć zestawy danych toomonitor poleceń cmdlet programu PowerShell i potoki. Aby uzyskać szczegółowe informacje o monitorowaniu, zobacz [monitorować i zarządzać potoki](data-factory-monitor-manage-pipelines.md).

1. Na diagramie powitania kliknij dwukrotnie **EmpOnPremSQLTable**.  

    ![Wycinki EmpOnPremSQLTable](./media/data-factory-move-data-between-onprem-and-cloud/OnPremSQLTableSlicesBlade.png)
2. Należy zauważyć, że wszystkie dane hello wycinków zapasowej znajdują się w **gotowe** stanu, ponieważ czas trwania potoku hello (czas rozpoczęcia czasu tooend) jest w przeszłości hello. To również, że wstawiono hello danych w bazie danych programu SQL Server hello i będzie cały czas hello. Upewnij się, że brak wycinków widoczne w hello **wycinków Problem** sekcji u dołu hello. tooview wszystkie fragmenty hello, kliknij przycisk **Zobacz więcej** u dołu listy hello wycinków hello.
3. Teraz, w hello **zestawów danych** kliknij przycisk **OutputBlobTable**.

    ![Wycinki OputputBlobTable](./media/data-factory-move-data-between-onprem-and-cloud/OutputBlobTableSlicesBlade.png)
4. Kliknij wycinek żadnych danych z listy hello i powinna zostać wyświetlona hello **wycinka danych** strony. Widać, że działanie jest uruchomione wycinek hello. Użytkownik widzi tylko jedno działanie Uruchom zwykle.  

    ![Blok wycinek danych](./media/data-factory-move-data-between-onprem-and-cloud/DataSlice.png)

    Jeśli hello wycinka nie jest hello **gotowe** stanu, można zobaczyć hello niegotowe wycinki strumienia wychodzącego nie jest gotowa i blokuje hello bieżący fragment wykonywanie w hello **wycinków strumienia wychodzącego, które nie są gotowe** listy.
5. Kliknij przycisk hello **uruchamiania działania** z listy hello na powitania dolnej toosee **szczegóły uruchomienia działania**.

   ![Strona szczegółów uruchomienia działania](./media/data-factory-move-data-between-onprem-and-cloud/ActivityRunDetailsBlade.png)

   Zobaczysz informacje, takie jak przepustowość, czas trwania i brama hello użyty tootransfer hello danych.
6. Kliknij przycisk **X** tooclose wszystkie hello aż do strony
7. wrócić toohello strony głównej dla hello **ADFTutorialOnPremDF**.
8. (opcjonalnie) Kliknij przycisk **potoki**, kliknij przycisk **ADFTutorialOnPremDF**oraz szczegółowy tabel wejściowych (**zużyto**) lub wyjściowych zestawów danych (**produkcji**).
9. Użyj narzędzia takiego jak [Eksploratora usługi Storage Microsoft](http://storageexplorer.com/) tooverify utworzony obiekt blob/plik dla każdej godziny.

   ![Eksplorator usługi Azure Storage](./media/data-factory-move-data-between-onprem-and-cloud/OnPremAzureStorageExplorer.png)

## <a name="next-steps"></a>Następne kroki
* Zobacz [brama zarządzania danymi](data-factory-data-management-gateway.md) artykułu dla wszystkich hello szczegółowe informacje o hello brama zarządzania danymi.
* Zobacz [kopiowanie danych z obiektu Blob Azure tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) toolearn o jak toouse działanie kopiowania toomove danych ze źródła danych przechowywane tooa ujście danych magazynu.
