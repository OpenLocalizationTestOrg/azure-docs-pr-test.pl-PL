---
title: "Kopiowanie danych z programu SQL Server do usługi Blob Storage przy użyciu usługi Azure Data Factory | Microsoft Docs"
description: "Dowiedz się, jak skopiować dane z lokalnego magazynu danych do chmury platformy Azure przy użyciu własnego środowiska Integration Runtime w usłudze Azure Data Factory."
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
ms.date: 01/22/2018
ms.author: jingwang
ms.openlocfilehash: 221af59c211cc6ce0471718908db1544ca2d75ed
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/23/2018
---
# <a name="tutorial-copy-data-from-an-on-premises-sql-server-database-to-azure-blob-storage"></a>Samouczek: kopiowanie danych z lokalnej bazy danych programu SQL Server do usługi Azure Blob Storage
W tym samouczku użyjesz programu Azure PowerShell, aby utworzyć potok usługi Data Factory, który kopiuje dane z lokalnej bazy danych programu SQL Server do usługi Azure Blob Storage. Utworzysz własne środowisko Integration Runtime (Self-hosted), służące do przenoszenia danych między lokalnym magazynem danych i magazynem danych w chmurze. 

> [!NOTE]
> Ten artykuł dotyczy wersji 2 usługi Azure Data Factory, która jest obecnie dostępna w wersji zapoznawczej. Jeśli używasz dostępnej ogólnie wersji 1 usługi Data Factory, zobacz [dokumentację dotyczącą usługi Data Factory w wersji 1](v1/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> Ten artykuł nie zawiera szczegółowego wprowadzenia do usługi Data Factory. Aby uzyskać więcej informacji, zobacz [Wprowadzenie do usługi Azure Data Factory](introduction.md). 

Ten samouczek obejmuje wykonanie następujących kroków:

> [!div class="checklist"]
> * Tworzenie fabryki danych.
> * Utwórz własne środowisko Integration Runtime.
> * Tworzenie połączonych zestawów programu SQL Server i usługi Azure Storage. 
> * Tworzenie zestawów danych programu SQL Server i usługi Azure Blob.
> * Tworzenie potoku z działaniem kopiowania do przenoszenia danych.
> * Uruchamianie przebiegu potoku.
> * Monitorowanie uruchomienia potoku.

## <a name="prerequisites"></a>Wymagania wstępne
### <a name="azure-subscription"></a>Subskrypcja platformy Azure
Jeśli nie masz jeszcze subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/).

### <a name="azure-roles"></a>Role platformy Azure
Aby utworzyć wystąpienia usługi Data Factory, konto użytkownika używane do logowania się na platformie Azure musi mieć przypisaną rolę *współautora* lub *właściciela* albo być *administratorem* subskrypcji platformy Azure. 

W witrynie Azure Portal wybierz swoją nazwę użytkownika w prawym górnym rogu i wybierz pozycję **Uprawnienia**, aby wyświetlić uprawnienia, które masz w subskrypcji. Jeśli masz dostęp do wielu subskrypcji, wybierz odpowiednią subskrypcję. Aby uzyskać przykładowe instrukcje dotyczące dodawania użytkownika do roli, zobacz artykuł [Dodawanie ról](../billing/billing-add-change-azure-subscription-administrator.md).

### <a name="sql-server-2014-2016-and-2017"></a>Program SQL Server 2014, 2016 oraz 2017
Podczas pracy z tym samouczkiem użyjesz lokalnej bazy danych programu SQL Server jako *źródłowego* magazynu danych. Potok usługi Data Factory tworzony w tym samouczku kopiuje dane z tej lokalnej bazy danych programu SQL Server (źródła) do usługi Azure Blob Storage (ujścia). Następnie utworzysz tabelę o nazwie **emp** w bazie danych programu SQL Server i wstawisz kilka przykładowych wpisów w tabeli. 

1. Uruchom program SQL Server Management Studio. Jeśli program nie jest jeszcze zainstalowany na używanej maszynie, przejdź do strony [pobierania programu SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms). 

2. Połącz się z wystąpieniem programu SQL Server przy użyciu swoich poświadczeń. 

3. Utwórz przykładową bazę danych. W widoku drzewa kliknij prawym przyciskiem myszy pozycję **Bazy danych**, a następnie wybierz pozycję **Nowa baza danych**. 
 
4. W oknie **Nowa baza danych** wprowadź nazwę bazy danych, a następnie wybierz przycisk **OK**. 

5. Aby utworzyć tabelę **emp** i wstawić do niej przykładowe dane, uruchom następujący skrypt zapytania w bazie danych:

   ```
       INSERT INTO emp VALUES ('John', 'Doe')
       INSERT INTO emp VALUES ('Jane', 'Doe')
       GO
   ```

6. W widoku drzewa kliknij prawym przyciskiem myszy utworzoną bazę danych, a następnie wybierz pozycję **Nowe zapytanie**.

### <a name="azure-storage-account"></a>Konto usługi Azure Storage
W tym samouczku używasz konta usługi Azure Storage ogólnego przeznaczenia (a dokładniej usługi Azure Blob Storage) jako docelowego magazynu danych (ujścia). Jeśli nie masz konta usługi Azure Storage ogólnego przeznaczenia, zobacz [Tworzenie konta magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account). Potok usługi Data Factory tworzony w tym samouczku kopiuje dane z lokalnej bazy danych programu SQL Server (źródła) do tego konta usługi Azure Blob Storage (ujścia). 

#### <a name="get-storage-account-name-and-account-key"></a>Pobieranie nazwy konta i klucza konta magazynu
W tym samouczku używasz nazwy i klucza swojego konta usługi Azure Storage. Pobierz nazwę i klucz konta usługi Storage, wykonując następujące czynności: 

1. Zaloguj się do witryny [Azure Portal](https://portal.azure.com) przy użyciu nazwy użytkownika i hasła do konta platformy Azure. 

2. W okienku po lewej stronie wybierz pozycję **Więcej usług**, zastosuj filtrowanie według słowa kluczowego **magazyn**, a następnie wybierz pozycję **Konta magazynu**.

    ![Wyszukiwanie konta magazynu](media/tutorial-hybrid-copy-powershell/search-storage-account.png)

3. Na liście kont magazynu znajdź swoje konto magazynu, w razie potrzeby używając filtrowania, a następnie wybierz to konto. 

4. W oknie **Konto magazynu** wybierz pozycję **Klucze dostępu**.

    ![Pobieranie nazwy i klucza konta magazynu](media/tutorial-hybrid-copy-powershell/storage-account-name-key.png)

5. Skopiuj wartości z pól **Nazwa konta magazynu** i **klucz1** i wklej je do Notatnika lub innego edytora do późniejszego użycia z tym samouczkiem. 

#### <a name="create-the-adftutorial-container"></a>Tworzenie kontenera adftutorial 
W tej sekcji utworzysz kontener obiektów blob o nazwie **adftutorial** w usłudze Azure Blob Storage. 

1. W oknie **Konto magazynu** przełącz się do widoku **Przegląd**, a następnie wybierz pozycję **Obiekty blob**. 

    ![Wybieranie opcji Obiekty blob](media/tutorial-hybrid-copy-powershell/select-blobs.png)

2. W oknie **Blob Service** wybierz pozycję **Kontener**. 

    ![Przycisk dodawania kontenera](media/tutorial-hybrid-copy-powershell/add-container-button.png)

3. W oknie **Nowy kontener** w polu **Nazwa** wpisz nazwę **adftutorial**, a następnie wybierz pozycję **OK**. 

    ![Wprowadzanie nazwy kontenera](media/tutorial-hybrid-copy-powershell/new-container-dialog.png)

4. Kliknij pozycję **adftutorial** na liście kontenerów.  

    ![Wybieranie kontenera](media/tutorial-hybrid-copy-powershell/seelct-adftutorial-container.png)

5. Pozostaw otwarte okno **kontenera** **adftutorial**. Będzie ona używana do weryfikacji danych wyjściowych na końcu tego samouczka. Usługa Data Factory automatycznie tworzy folder wyjściowy w tym kontenerze, więc Ty nie musisz go tworzyć.

    ![Okno kontenera](media/tutorial-hybrid-copy-powershell/container-page.png)

### <a name="windows-powershell"></a>Windows PowerShell

#### <a name="install-azure-powershell"></a>Instalowanie programu Azure PowerShell
Zainstaluj najnowszą wersję programu Azure PowerShell, jeśli nie masz jej jeszcze na swojej maszynie. 

1. Przejdź do strony [Pobierz zestawy SDK dla platformy Azure](https://azure.microsoft.com/downloads/). 

2. W obszarze **Narzędzia wiersza polecenia** w sekcji **PowerShell** wybierz pozycję **Wersja instalacyjna dla systemu Windows**. 

3. Aby zainstalować program Azure PowerShell, uruchom plik MSI. 

Aby uzyskać szczegółowe informacje, zobacz [How to install and configure Azure PowerShell (Jak zainstalować i skonfigurować program Azure PowerShell)](/powershell/azure/install-azurerm-ps). 

#### <a name="log-in-to-powershell"></a>Logowanie do programu PowerShell

1. Uruchom program PowerShell na maszynie i pozostaw ten program otwarty aż do zakończenia pracy z tym samouczkiem Szybki start. Jeśli go zamkniesz i otworzysz ponownie, musisz uruchomić te polecenia jeszcze raz.

    ![Uruchamianie programu PowerShell](media/tutorial-hybrid-copy-powershell/search-powershell.png)

2. Uruchom poniższe polecenie, a następnie wprowadź nazwę użytkownika platformy Azure oraz hasło, których używasz do logowania się w witrynie Azure Portal:
       
    ```powershell
    Login-AzureRmAccount
    ```        

3. Jeśli masz wiele subskrypcji platformy Azure, uruchom poniższe polecenie, aby wybrać subskrypcję, z którą chcesz pracować. Zastąp parametr **SubscriptionId** identyfikatorem Twojej subskrypcji platformy Azure:

    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<SubscriptionId>"       
    ```

## <a name="create-a-data-factory"></a>Tworzenie fabryki danych

1. Zdefiniuj zmienną nazwy grupy zasobów, której użyjesz później w poleceniach programu PowerShell. Skopiuj poniższe polecenie do programu PowerShell, podaj nazwę [grupy zasobów platformy Azure](../azure-resource-manager/resource-group-overview.md) w podwójnych cudzysłowach (na przykład `"adfrg"`), a następnie uruchom polecenie. 
   
     ```powershell
    $resourceGroupName = "ADFTutorialResourceGroup"
    ```

2. Aby utworzyć grupę zasobów platformy Azure, uruchom następujące polecenie: 

    ```powershell
    New-AzureRmResourceGroup $resourceGroupName $location
    ``` 

    Jeśli grupa zasobów już istnieje, możesz zrezygnować z jej zastąpienia. Przypisz inną wartość do zmiennej `$resourceGroupName` i ponownie uruchom polecenie.

3. Zdefiniuj zmienną nazwy fabryki danych, której możesz użyć później w poleceniach programu PowerShell. Nazwa musi zaczynać się od litery lub cyfry i może zawierać tylko litery, cyfry i znak łącznika (-).

    > [!IMPORTANT]
    >  Zaktualizuj nazwę fabryki danych, nadając jej globalnie unikatową nazwę. Na przykład: ADFTutorialFactorySP1127. 

    ```powershell
    $dataFactoryName = "ADFTutorialFactory"
    ```

4. Zdefiniuj zmienną lokalizacji fabryki danych: 

    ```powershell
    $location = "East US"
    ```  

5. Aby utworzyć fabrykę danych, uruchom następujące polecenie cmdlet `Set-AzureRmDataFactoryV2`: 
    
    ```powershell       
    Set-AzureRmDataFactoryV2 -ResourceGroupName $resourceGroupName -Location $location -Name $dataFactoryName 
    ```

> [!NOTE]
> 
> * Nazwa fabryki danych musi być globalnie unikatowa. Jeśli zostanie wyświetlony następujący błąd, zmień nazwę i spróbuj ponownie.
>    ```
>    The specified data factory name 'ADFv2TutorialDataFactory' is already in use. Data factory names must be globally unique.
>    ```
> * Aby utworzyć wystąpienia usługi Data Factory, konto użytkownika używane do logowania się na platformie Azure musi mieć przypisaną rolę *współautora* lub *właściciela* albo być *administratorem* subskrypcji platformy Azure.
> * Obecnie usługa Data Factory w wersji 2 umożliwia tworzenie fabryk danych tylko w regionach Wschodnie stany USA, Wschodnie stany USA 2 i Europa Zachodnia. Magazyny danych (Azure Storage, Azure SQL Database itd.) i jednostki obliczeniowe (Azure HDInsight itd.) używane przez fabrykę danych mogą mieścić się w innych regionach.
> 
> 

## <a name="create-a-self-hosted-integration-runtime"></a>Tworzenie własnego środowiska Integration Runtime

W tej sekcji utworzysz własne środowisko Integration Runtime i skojarzysz je z maszyną lokalną za pomocą bazy danych programu SQL Server. Własne środowisko Integration Runtime jest składnikiem, który kopiuje dane z bazy danych programu SQL Server na Twojej maszynie do usługi Azure Blob Storage. 

1. Utwórz zmienną dla nazwy środowiska Integration Runtime. Użyj unikatowej nazwy i zanotuj ją. Będziesz jej używać w dalszej części tego samouczka. 

    ```powershell
   $integrationRuntimeName = "ADFTutorialIR"
    ```

2. Utwórz własne środowisko Integration Runtime. 

    Oto przykładowe dane wyjściowe:

    ```json
    Id                : /subscriptions/<subscription ID>/resourceGroups/ADFTutorialResourceGroup/providers/Microsoft.DataFactory/factories/onpremdf0914/integrationruntimes/myonpremirsp0914
    Type              : SelfHosted
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : onpremdf0914
    Name              : myonpremirsp0914
    Description       :
    ```

3. Uruchom następujące polecenie, aby pobrać stan utworzonego środowiska Integration Runtime:

    ```powershell
   Get-AzureRmDataFactoryV2IntegrationRuntime -name $integrationRuntimeName -ResourceGroupName $resourceGroupName -DataFactoryName $dataFactoryName -Status
    ```

    Oto przykładowe dane wyjściowe:
    
    ```json
    Nodes                     : {}
    CreateTime                : 9/14/2017 10:01:21 AM
    InternalChannelEncryption :
    Version                   :
    Capabilities              : {}
    ScheduledUpdateDate       :
    UpdateDelayOffset         :
    LocalTimeZoneOffset       :
    AutoUpdate                :
    ServiceUrls               : {eu.frontend.clouddatahub.net, *.servicebus.windows.net}
    ResourceGroupName         : <ResourceGroup name>
    DataFactoryName           : <DataFactory name>
    Name                      : <Integration Runtime name>
    State                     : NeedRegistration
    ```

4. Uruchom następujące polecenie, aby pobrać *klucze uwierzytelniania* w celu zarejestrowania własnego środowiska Integration Runtime za pomocą usługi Data Factory w chmurze. Skopiuj jeden z kluczy (pomijając cudzysłowy) na potrzeby rejestracji własnego środowiska Integration Runtime, które zainstalujesz na swojej maszynie w następnym kroku. 

    ```powershell
    Get-AzureRmDataFactoryV2IntegrationRuntimeKey -Name $integrationRuntimeName -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName | ConvertTo-Json
    ```
    
    Oto przykładowe dane wyjściowe:
    
    ```json
    {
        "AuthKey1":  "IR@0000000000-0000-0000-0000-000000000000@xy0@xy@xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx=",
        "AuthKey2":  "IR@0000000000-0000-0000-0000-000000000000@xy0@xy@yyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyy="
    }
    ```

## <a name="install-the-integration-runtime"></a>Instalowanie środowiska Integration Runtime
1. Pobierz [środowisko Integration Runtime usługi Azure Data Factory](https://www.microsoft.com/download/details.aspx?id=39717) na lokalną maszynę z systemem Windows, a następnie uruchom instalację. 

2. Na **stronie powitalnej Kreatora instalacji środowiska Microsoft Integration Runtime** wybierz przycisk **Dalej**.  

3. W oknie **Umowa Licencyjna Użytkownika Oprogramowania** zaakceptuj warunki i umowę licencyjną, a następnie wybierz przycisk **Dalej**. 

4. W oknie **Folder docelowy** wybierz przycisk **Dalej**. 

5. W oknie **Gotowe do zainstalowania środowiska Microsoft Integration Runtime** wybierz pozycję **Zainstaluj**. 

6. Jeśli zostanie wyświetlony komunikat ostrzegawczy informujący o tym, że konfigurowany komputer przejdzie w tryb uśpienia lub hibernacji, jeśli nie będzie używany, wybierz przycisk **OK**. 

7. Jeśli zostanie wyświetlone okno **Opcje zasilania**, zamknij je i przejdź do okna Instalatora. 

8. W oknie **zakończenia pracy z Kreatorem instalacji środowiska Microsoft Integration Runtime** wybierz pozycję **Zakończ**.

9. W oknie **Rejestrowanie środowiska Integration Runtime (Self-hosted)** wklej klucz zapisany w poprzedniej sekcji i wybierz pozycję **Zarejestruj**. 

    ![Rejestrowanie środowiska Integration Runtime](media/tutorial-hybrid-copy-powershell/register-integration-runtime.png)

    Gdy własne środowisko Integration Runtime zostanie pomyślnie zarejestrowane, zostanie wyświetlony następujący komunikat: 

    ![Pomyślnie zarejestrowano](media/tutorial-hybrid-copy-powershell/registered-successfully.png)

10. W oknie **Nowy węzeł Integration Runtime (Self-hosted)** wybierz pozycję **Dalej**. 

    ![Okno Nowy węzeł Integration Runtime (Self-hosted)](media/tutorial-hybrid-copy-powershell/new-integration-runtime-node-page.png)

11. W oknie **Kanał komunikacji intranetowej** wybierz pozycję **Pomiń**.  
    Możesz wybrać certyfikację protokołów TLS/SSL w celu zabezpieczenia komunikacji w środowisku Integration Runtime z wieloma węzłami.

    ![Okno Kanał komunikacji intranetowej](media/tutorial-hybrid-copy-powershell/intranet-communication-channel-page.png)

12. W oknie **Rejestrowanie produktu Integration Runtime (Self-hosted)** kliknij pozycję **Uruchom program Configuration Manager**. 

13. Gdy węzeł zostanie połączony z usługą w chmurze, zostanie wyświetlony następujący komunikat:

    ![Węzeł jest połączony](media/tutorial-hybrid-copy-powershell/node-is-connected.png)

14. Przetestuj łączność z bazą danych programu SQL Server, wykonując następujące kroki:

    ![Karta Diagnostyka](media/tutorial-hybrid-copy-powershell/config-manager-diagnostics-tab.png)   

    a. W oknie programu **Configuration Manager** przejdź na kartę **Diagnostyka**.

    b. W polu **Typ źródła danych** wybierz pozycję **SqlServer**.

    d. Wprowadź nazwę serwera.

    d. Wprowadź nazwę bazy danych. 

    e. Wybierz tryb uwierzytelniania. 

    f. Wprowadź nazwę użytkownika. 

    g. Wprowadź hasło powiązane z tą nazwą użytkownika.

    h. Wybierz przycisk **Testuj**, aby upewnić się, że środowisko Integration Runtime może połączyć się z wystąpieniem programu SQL Server.  
    Jeśli połączenie zostanie pomyślnie nawiązane, zostanie wyświetlona ikona zielonego znacznika wyboru. W przeciwnym razie zostanie wyświetlony komunikat o błędzie skojarzony z określonym błędem. Rozwiąż wszelkie problemy i upewnij się, że środowisko Integration Runtime może połączyć się z wystąpieniem programu SQL Server.

    Zanotuj wszystkie powyższe wartości do późniejszego użycia z tym samouczkiem.
    
## <a name="create-linked-services"></a>Tworzenie połączonych usług
Utwórz połączone usługi w fabryce danych w celu połączenia swoich magazynów danych i usług obliczeniowych z fabryką danych. W tym samouczku połączysz swoje konto usługi Azure Storage i lokalne wystąpienie programu SQL Server z magazynem danych. Połączone usługi mają informacje o połączeniu, których usługa Data Factory używa w środowisku uruchomieniowym do łączenia się z nimi. 

### <a name="create-an-azure-storage-linked-service-destinationsink"></a>Tworzenie połączonej usługi Azure Storage (obiektu docelowego/ujścia)
W tym kroku opisano łączenie konta usługi Azure Storage z fabryką danych.

1. W folderze *C:\ADFv2Tutorial* utwórz plik JSON o nazwie *AzureStorageLinkedService.json*, używając poniższego kodu. Jeśli folder *ADFv2Tutorial* jeszcze nie istnieje, utwórz go.  

    > [!IMPORTANT]
    > Przed zapisaniem pliku zastąp wartości \<accountName> i \<accountKey> nazwą i kluczem konta usługi Azure Storage. Te wartości zapisano podczas wykonywania czynności opisanych w sekcji [Wymagania wstępne](#get-storage-account-name-and-account-key).

   ```json
    {
        "properties": {
            "type": "AzureStorage",
            "typeProperties": {
                "connectionString": {
                    "type": "SecureString",
                    "value": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>;EndpointSuffix=core.windows.net"
                }
            }
        },
        "name": "AzureStorageLinkedService"
    }
   ```

2. W programie PowerShell przejdź do folderu *C:\ADFv2Tutorial*.

3. Aby utworzyć połączoną usługę o nazwie AzureStorageLinkedService, uruchom następujące polecenie cmdlet `Set-AzureRmDataFactoryV2LinkedService`: 

   ```powershell
   Set-AzureRmDataFactoryV2LinkedService -DataFactoryName $dataFactoryName -ResourceGroupName $ResourceGroupName -Name "AzureStorageLinkedService" -File ".\AzureStorageLinkedService.json"
   ```

   Oto przykładowe dane wyjściowe:

    ```json
    LinkedServiceName : AzureStorageLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : onpremdf0914
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureStorageLinkedService
    ```

    Jeśli zostanie zwrócony błąd „nie znaleziono pliku”, sprawdź, czy plik istnieje, uruchamiając polecenie `dir`. Jeśli nazwa pliku ma rozszerzenie *txt* (na przykład AzureStorageLinkedService.json.txt), usuń je, a następnie ponownie uruchom polecenie programu PowerShell. 

### <a name="create-and-encrypt-a-sql-server-linked-service-source"></a>Tworzenie i szyfrowanie połączonej usługi SQL Server (źródło)
W tym kroku połączysz lokalne wystąpienie programu SQL Server z fabryką danych.

1. W folderze *C:\ADFv2Tutorial* utwórz plik JSON o nazwie *SqlServerLinkedService.json*, używając następującego kodu:

    > [!IMPORTANT]
    > Wybierz właściwą sekcję na podstawie metody uwierzytelniania używanej do nawiązywania połączenia z programem SQL Server.

    **Nawiązywanie połączenia przy użyciu uwierzytelniania SQL (sa):**

    ```json
    {
        "properties": {
            "type": "SqlServer",
            "typeProperties": {
                "connectionString": {
                    "type": "SecureString",
                    "value": "Server=<servername>;Database=<databasename>;User ID=<username>;Password=<password>;Timeout=60"
                }
            },
            "connectVia": {
                "type": "integrationRuntimeReference",
                "referenceName": "<integration runtime name>"
            }
        },
        "name": "SqlServerLinkedService"
    }
   ```    

    **Nawiązywanie połączenia przy użyciu uwierzytelniania systemu Windows:**

    ```json
    {
        "properties": {
            "type": "SqlServer",
            "typeProperties": {
                "connectionString": {
                    "type": "SecureString",
                    "value": "Server=<server>;Database=<database>;Integrated Security=True"
                },
                "userName": "<user> or <domain>\\<user>",
                "password": {
                    "type": "SecureString",
                    "value": "<password>"
                }
            },
            "connectVia": {
                "type": "integrationRuntimeReference",
                "referenceName": "<integration runtime name>"
            }
        },
        "name": "SqlServerLinkedService"
    }    
    ```

    > [!IMPORTANT]
    > - Wybierz właściwą sekcję na podstawie metody uwierzytelniania używanej do nawiązywania połączenia z wystąpieniem programu SQL Server.
    > - Zastąp wartość **\<integration runtime name>** nazwą Twojego środowiska Integration Runtime.
    > - Przed zapisaniem pliku zastąp wartości **\<servername>**, **\<databasename>**, **\<username>** i **\<password** wartościami odpowiednimi dla wystąpienia programu SQL Server.
    > - Jeśli musisz użyć znaku ukośnika (\\) w nazwie konta użytkownika lub nazwie serwera, poprzedź go znakiem ucieczki (\\). Na przykład: *mydomain\\\\myuser*. 

2. Aby zaszyfrować dane poufne (nazwę użytkownika, hasło itp.), uruchom polecenie cmdlet `New-AzureRmDataFactoryV2LinkedServiceEncryptedCredential`.  
    To zapewnia szyfrowanie poświadczeń za pomocą interfejsu API ochrony danych (DPAPI). Zaszyfrowane poświadczenia są przechowywane lokalnie w węźle środowiska Integration Runtime (Self-hosted) (maszyna lokalna). Ładunek danych wyjściowych może zostać przekierowany do innego pliku JSON (w tym przypadku *encryptedLinkedService.json*), który zawiera zaszyfrowane poświadczenia.
    
   ```powershell
   New-AzureRmDataFactoryV2LinkedServiceEncryptedCredential -DataFactoryName $dataFactoryName -ResourceGroupName $ResourceGroupName -IntegrationRuntimeName $integrationRuntimeName -File ".\SQLServerLinkedService.json" > encryptedSQLServerLinkedService.json
   ```

3. Uruchom następujące polecenie, aby utworzyć element EncryptedSqlServerLinkedService:

   ```powershell
   Set-AzureRmDataFactoryV2LinkedService -DataFactoryName $dataFactoryName -ResourceGroupName $ResourceGroupName -Name "EncryptedSqlServerLinkedService" -File ".\encryptedSqlServerLinkedService.json"
   ```


## <a name="create-datasets"></a>Tworzenie zestawów danych
W tym kroku utworzysz zestawy danych wejściowych i wyjściowych. Reprezentują one dane wejściowe i wyjściowe operacji kopiowania, która kopiuje dane z lokalnej bazy danych programu SQL Server do usługi Azure Blob Storage.

### <a name="create-a-dataset-for-the-source-sql-server-database"></a>Tworzenie zestawu danych źródłowej bazy danych programu SQL Server
W tym kroku zdefiniujesz zestaw danych, który reprezentuje dane w wystąpieniu bazy danych programu SQL Server. Typ zestawu danych to SqlServerTable. Odwołuje się on do połączonej usługi programu SQL Server utworzonej w poprzednim kroku. Połączona usługa ma informacje o połączeniu, których usługa Data Factory używa do nawiązywania połączenia z wystąpieniem programu SQL Server w środowisku uruchomieniowym. Ten zestaw danych określa tabelę SQL w bazie danych, która zawiera dane. W tym samouczku dane źródłowe zawiera tabela **emp**. 

1. Utwórz plik JSON o nazwie *SqlServerDataset.json* w folderze *C:\ADFv2Tutorial*, używając następującego kodu:  

    ```json
    {
       "properties": {
            "type": "SqlServerTable",
            "typeProperties": {
                "tableName": "dbo.emp"
            },
            "structure": [
                 {
                    "name": "ID",
                    "type": "String"
                },
                {
                    "name": "FirstName",
                    "type": "String"
                },
                {
                    "name": "LastName",
                    "type": "String"
                }
            ],
            "linkedServiceName": {
                "referenceName": "EncryptedSqlServerLinkedService",
                "type": "LinkedServiceReference"
            }
        },
        "name": "SqlServerDataset"
    }
    ```

2. Aby utworzyć zestaw danych SqlServerDataset, uruchom polecenie cmdlet `Set-AzureRmDataFactoryV2Dataset`.

    ```powershell
    Set-AzureRmDataFactoryV2Dataset -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "SqlServerDataset" -File ".\SqlServerDataset.json"
    ```

    Oto przykładowe dane wyjściowe:

    ```json
    DatasetName       : SqlServerDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : onpremdf0914
    Structure         : {"name": "ID" "type": "String", "name": "FirstName" "type": "String", "name": "LastName" "type": "String"}
    Properties        : Microsoft.Azure.Management.DataFactory.Models.SqlServerTableDataset
    ```

### <a name="create-a-dataset-for-azure-blob-storage-sink"></a>Tworzenie zestawu danych usługi Azure Blob Storage (ujścia)
W tym kroku zdefiniujesz zestaw danych reprezentujący dane, które mają zostać skopiowane do usługi Azure Blob Storage. Typ tego zestawu danych to AzureBlob. Odwołuje się on do połączonej usługi Azure Storage utworzonej wcześniej w tym samouczku. 

Połączona usługa ma informacje o połączeniu, których usługa Data Factory używa w środowisku uruchomieniowym do nawiązania połączenia z kontem usługi Azure Storage. Ten zestaw danych określa folder w usłudze Azure Storage, do którego kopiowane są dane z bazy danych programu SQL Server. W tym samouczku jest to folder *adftutorial/fromonprem*, gdzie `adftutorial` to kontener obiektów blob, a `fromonprem` to folder. 

1. Utwórz plik JSON o nazwie *AzureBlobDataset.json* w folderze *C:\ADFv2Tutorial*, używając następującego kodu:

    ```json
    {
        "properties": {
            "type": "AzureBlob",
            "typeProperties": {
                "folderPath": "adftutorial/fromonprem",
                "format": {
                    "type": "TextFormat"
                }
            },
            "linkedServiceName": {
                "referenceName": "AzureStorageLinkedService",
                "type": "LinkedServiceReference"
            }
        },
        "name": "AzureBlobDataset"
    }
    ```

2. Aby utworzyć zestaw danych AzureBlobDataset, uruchom polecenie cmdlet `Set-AzureRmDataFactoryV2Dataset`.

    ```powershell
    Set-AzureRmDataFactoryV2Dataset -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "AzureBlobDataset" -File ".\AzureBlobDataset.json"
    ```

    Oto przykładowe dane wyjściowe:

    ```json
    DatasetName       : AzureBlobDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : onpremdf0914
    Structure         :
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureBlobDataset
    ```

## <a name="create-a-pipeline"></a>Tworzenie potoku
W tym samouczku jest tworzony potok za pomocą działania kopiowania. Działanie kopiowania używa zestawu danych SqlServerDataset jako wejściowego zestawu danych oraz zestawu danych AzureBlobDataset jako wyjściowego zestawu danych. Typ źródła jest ustawiony na wartość *SqlSource*, a typ ujścia — na wartość *BlobSink*.

1. Utwórz plik JSON o nazwie *SqlServerToBlobPipeline.json* w folderze *C:\ADFv2Tutorial*, używając następującego kodu:

    ```json
    {
       "name": "SQLServerToBlobPipeline",
        "properties": {
            "activities": [       
                {
                    "type": "Copy",
                    "typeProperties": {
                        "source": {
                            "type": "SqlSource"
                        },
                        "sink": {
                            "type":"BlobSink"
                        }
                    },
                    "name": "CopySqlServerToAzureBlobActivity",
                    "inputs": [
                        {
                            "referenceName": "SqlServerDataset",
                            "type": "DatasetReference"
                        }
                    ],
                    "outputs": [
                        {
                            "referenceName": "AzureBlobDataset",
                            "type": "DatasetReference"
                        }
                    ]
                }
            ]
        }
    }
    ```

2. Aby utworzyć potok SQLServerToBlobPipeline, uruchom polecenie cmdlet `Set-AzureRmDataFactoryV2Pipeline`.

    ```powershell
    Set-AzureRmDataFactoryV2Pipeline -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "SQLServerToBlobPipeline" -File ".\SQLServerToBlobPipeline.json"
    ```

    Oto przykładowe dane wyjściowe:

    ```json
    PipelineName      : SQLServerToBlobPipeline
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : onpremdf0914
    Activities        : {CopySqlServerToAzureBlobActivity}
    Parameters        :  
    ```

## <a name="create-a-pipeline-run"></a>Tworzenie uruchomienia potoku
Uruchom działanie potoku dla potoku SQLServerToBlobPipeline i zapisz identyfikator działania potoku do monitorowania w przyszłości.

```powershell
$runId = Invoke-AzureRmDataFactoryV2Pipeline -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -PipelineName 'SQLServerToBlobPipeline'
```

## <a name="monitor-the-pipeline-run"></a>Monitorowanie działania potoku

1. Aby stale sprawdzać stan działania potoku SQLServerToBlobPipeline, uruchom następujący skrypt w programie PowerShell, a następnie wydrukuj wynik końcowy:

    ```powershell
    while ($True) {
        $result = Get-AzureRmDataFactoryV2ActivityRun -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -PipelineRunId $runId -RunStartedAfter (Get-Date).AddMinutes(-30) -RunStartedBefore (Get-Date).AddMinutes(30)

        if (($result | Where-Object { $_.Status -eq "InProgress" } | Measure-Object).count -ne 0) {
            Write-Host "Pipeline run status: In Progress" -foregroundcolor "Yellow"
            Start-Sleep -Seconds 30
        }
        else {
            Write-Host "Pipeline 'SQLServerToBlobPipeline' run finished. Result:" -foregroundcolor "Yellow"
            $result
            break
        }
    }
    ```

    Oto dane wyjściowe przykładowego przebiegu:

    ```jdon
    ResourceGroupName : <resourceGroupName>
    DataFactoryName   : <dataFactoryName>
    ActivityName      : copy
    PipelineRunId     : 4ec8980c-62f6-466f-92fa-e69b10f33640
    PipelineName      : SQLServerToBlobPipeline
    Input             :  
    Output            :  
    LinkedServiceName :
    ActivityRunStart  : 9/13/2017 1:35:22 PM
    ActivityRunEnd    : 9/13/2017 1:35:42 PM
    DurationInMs      : 20824
    Status            : Succeeded
    Error             : {errorCode, message, failureType, target}
    ```

2. Aby uzyskać identyfikator działania potoku SQLServerToBlobPipeline i sprawdzić szczegółowe wyniki uruchomienia działania, uruchom następujące polecenie: 

    ```powershell
    Write-Host "Pipeline 'SQLServerToBlobPipeline' run result:" -foregroundcolor "Yellow"
    ($result | Where-Object {$_.ActivityName -eq "CopySqlServerToAzureBlobActivity"}).Output.ToString()
    ```

    Oto dane wyjściowe przykładowego przebiegu:

    ```json
    {
      "dataRead": 36,
      "dataWritten": 24,
      "rowsCopied": 2,
      "copyDuration": 3,
      "throughput": 0.01171875,
      "errors": [],
      "effectiveIntegrationRuntime": "MyIntegrationRuntime",
      "billedDuration": 3
    }
    ```

## <a name="verify-the-output"></a>Sprawdzanie danych wyjściowych
Potok automatycznie tworzy folder wyjściowy o nazwie *fromonprem* w kontenerze obiektów blob `adftutorial`. Upewnij się, że plik *dbo.emp.txt* jest widoczny w folderze wyjściowym. 

1. W witrynie Azure Portal w oknie kontenera **adftutorial** kliknij przycisk **Odśwież**, aby wyświetlić folder wyjściowy.

    ![Utworzony folder wyjściowy](media/tutorial-hybrid-copy-powershell/fromonprem-folder.png)
2. Wybierz pozycję `fromonprem` na liście folderów. 
3. Upewnij się jest wyświetlany plik o nazwie `dbo.emp.txt`.

    ![Plik wyjściowy](media/tutorial-hybrid-copy-powershell/fromonprem-file.png)


## <a name="next-steps"></a>Następne kroki
Potok w tym przykładzie kopiuje dane z jednej lokalizacji do innej lokalizacji w usłudze Azure Blob Storage. W tym samouczku omówiono:

> [!div class="checklist"]
> * Tworzenie fabryki danych.
> * Utwórz własne środowisko Integration Runtime.
> * Tworzenie połączonych zestawów programu SQL Server i usługi Azure Storage. 
> * Tworzenie zestawów danych programu SQL Server i usługi Azure Blob.
> * Tworzenie potoku z działaniem kopiowania do przenoszenia danych.
> * Uruchamianie przebiegu potoku.
> * Monitorowanie uruchomienia potoku.

Lista magazynów danych obsługiwanych przez usługę Data Factory znajduje się w artykule dotyczącym [obsługiwanych magazynów danych](copy-activity-overview.md#supported-data-stores-and-formats).

Przejdź do poniższego samouczka, aby dowiedzieć się o zbiorczym kopiowaniu danych z lokalizacji źródłowej do docelowej:

> [!div class="nextstepaction"]
>[Zbiorcze kopiowanie danych](tutorial-bulk-copy.md)
