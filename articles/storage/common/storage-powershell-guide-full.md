---
title: "aaaUsing programu Azure PowerShell z usługą Azure Storage | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello poleceń cmdlet programu Azure PowerShell dla usługi Azure Storage toocreate i zarządzanie kontami magazynu; Praca z obiektów blob, tabel, kolejek i plików. Konfigurowanie i zapytania analityka magazynu, a następnie utwórz sygnatur dostępu współdzielonego."
services: storage
documentationcenter: na
author: robinsh
manager: timlt
ms.assetid: f4704f58-abc6-4f89-8b6d-1b1659746f5a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/03/2017
ms.author: robinsh
ms.openlocfilehash: 17d638e741911ceafb9777d5c2fce7bfe533e50c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-powershell-with-azure-storage"></a>Używanie programu Azure PowerShell z usługą Azure Storage
## <a name="overview"></a>Omówienie
Program Azure PowerShell jest moduł, który udostępnia polecenia cmdlet toomanage Azure za pomocą programu Windows PowerShell. Jest to język skryptów i powłoka wiersza polecenia oparta na zadaniach zaprojektowana pod kątem administrowania systemem. Przy użyciu programu PowerShell można łatwo kontrolować i automatyzować administrację hello Azure usługi i aplikacje. Na przykład można użyć hello tooperform poleceń cmdlet hello same zadania, można wykonać za pomocą hello [portalu Azure](https://portal.azure.com).

W tym przewodniku, firma Microsoft będzie Eksploruj jak toouse hello [polecenia cmdlet usługi Azure Storage](/powershell/module/azurerm.storage/#storage) tooperform różnych zadań programowania i administracji z usługą Azure Storage.

W tym przewodniku założono, że przy użyciu doświadczenie [usługi Azure Storage](https://azure.microsoft.com/documentation/services/storage/) i [programu Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx). Przewodnik Hello zawiera liczby skryptów toodemonstrate hello użycia programu PowerShell z usługą Azure Storage. Należy zaktualizować hello zmienne skryptu na podstawie konfiguracji przed uruchomieniem każdego skryptu.

Pierwsza sekcja Hello w tym przewodniku zapewnia szybkiego dostępu w usłudze Azure Storage i programu PowerShell. Aby uzyskać szczegółowe informacje i instrukcje, Rozpocznij od hello [wymagań wstępnych dotyczących używania programu Azure PowerShell z usługą Azure Storage](#prerequisites-for-using-azure-powershell-with-azure-storage).

## <a name="getting-started-with-azure-storage-and-powershell-in-5-minutes"></a>Wprowadzenie do korzystania z usługi Azure Storage i programu PowerShell w ciągu 5 minut
W tej sekcji opisano sposób tooaccess usługi Azure Storage za pomocą programu PowerShell w ciągu 5 minut.

**Nowe tooAzure:** subskrypcji Microsoft Azure i konta Microsoft skojarzonego z jego subskrypcją. Aby uzyskać informacje na temat opcji zakupu platformy Azure, zobacz [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/), [opcjami zakupu](https://azure.microsoft.com/pricing/purchase-options/), i [oferty Członkowskie](https://azure.microsoft.com/pricing/member-offers/) (dla członków MSDN, Microsoft Partner Network, BizSpark i innych programów firmy Microsoft).

Zobacz [przypisywanie ról administratorów w usłudze Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) uzyskać więcej informacji o subskrypcji platformy Azure.

**Po utworzeniu subskrypcji Microsoft Azure i konto:**

1. Pobierz i zainstaluj najnowsze hello [programu Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest).
2. Start środowisko systemu Windows PowerShell zintegrowane skryptów (ISE): W komputerze lokalnym, przejdź toohello **Start** menu. Typ **narzędzia administracyjne** i kliknij przycisk toorun go. W hello **narzędzia administracyjne** okna, kliknij prawym przyciskiem myszy **programu Windows PowerShell ISE**, kliknij przycisk **Uruchom jako Administrator**.
3. W **programu Windows PowerShell ISE**, kliknij przycisk **pliku** > **nowy** toocreate nowy plik skryptu.
4. Teraz przedstawimy prosty skrypt, który zawiera podstawowe tooaccess poleceń programu PowerShell usługi Azure Storage. skryptu Hello najpierw poprosi użytkownika tooadd poświadczenia konta Azure konta Azure toohello PowerShell środowisku lokalnym. Następnie skryptu hello ustawiania domyślnych hello subskrypcji platformy Azure i Utwórz nowe konto magazynu na platformie Azure. Następnie skryptu hello utworzyć nowy kontener w tym nowe konto magazynu i przekaż istniejącego kontenera toothat obrazu pliku (blob). Po skryptu hello znajduje się lista wszystkich obiektów blob w tym kontenerze, utworzy nowy katalog docelowy w komputerze lokalnym i Pobierz hello pliku obrazu.
5. W następujących sekcji kodu hello, wybierz skrypt hello między uwagi hello **#begin** i **#end**. Naciśnij klawisze CTRL + C toocopy on toohello Schowka.

    ```powershell
    # begin
    # Update with hello name of your subscription.
    $SubscriptionName = "YourSubscriptionName"
       
    # Give a name tooyour new storage account. It must be lowercase!
    $StorageAccountName = "yourstorageaccountname"
       
    # Choose "West US" as an example.
    $Location = "West US"
       
    # Give a name tooyour new container.
    $ContainerName = "imagecontainer"
       
    # Have an image file and a source directory in your local computer.
    $ImageToUpload = "C:\Images\HelloWorld.png"
       
    # A destination directory in your local computer.
    $DestinationFolder = "C:\DownloadImages"
       
    # Add your Azure account toohello local PowerShell environment.
    Add-AzureAccount
       
    # Set a default Azure subscription.
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
       
    # Create a new storage account.
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $Location
       
    # Set a default storage account.
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
       
    # Create a new container.
    New-AzureStorageContainer -Name $ContainerName -Permission Off
       
    # Upload a blob into a container.
    Set-AzureStorageBlobContent -Container $ContainerName -File $ImageToUpload
       
    # List all blobs in a container.
    Get-AzureStorageBlob -Container $ContainerName
       
    # Download blobs from hello container:
    # Get a reference tooa list of all blobs in a container.
    $blobs = Get-AzureStorageBlob -Container $ContainerName
       
    # Create hello destination directory.
    New-Item -Path $DestinationFolder -ItemType Directory -Force  
       
    # Download blobs into hello local destination directory.
    $blobs | Get-AzureStorageBlobContent –Destination $DestinationFolder
       
    # end
    ```

6. W **programu Windows PowerShell ISE**, naciśnij klawisze CTRL + V toocopy hello skryptu. Kliknij przycisk **pliku** > **zapisać**. W hello **Zapisz jako** okno dialogowe, nazwa typu hello hello pliku skryptu, takie jak "mystoragescript." Kliknij pozycję **Zapisz**.
7. Teraz należy zmienne skryptu hello tooupdate na podstawie własnych ustawień konfiguracji. Należy zaktualizować hello **$SubscriptionName** zmiennej przy użyciu posiadanej subskrypcji. Możesz zachować hello inne zmienne określone w skrypcie hello lub zaktualizuj je zgodnie z wymaganiami.
   
   * **$SubscriptionName:** należy zaktualizować tę zmienną z własną nazwę subskrypcji. Wykonaj jedną z hello następujące trzy sposoby toolocate hello nazwa Twojej subskrypcji:
     
    a. W **programu Windows PowerShell ISE**, kliknij przycisk **pliku** > **nowy** toocreate nowy plik skryptu. Kopia hello następujący skrypt toohello nowy plik skryptu i kliknij przycisk **debugowania** > **Uruchom**. Hello poniższy skrypt zostanie najpierw poproś użytkownika tooadd poświadczenia konta Azure konta Azure toohello PowerShell środowisku lokalnym a następnie wyświetlać wszystkie subskrypcje hello, które są połączone toohello lokalnej sesji programu PowerShell. Zanotuj nazwę hello subskrypcji hello mają toouse podczas korzystania z tego samouczka:
     
    ```powershell
    Add-AzureAccount 
      Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName
    ```

    b. toolocate i skopiuj subskrypcji nazwisko hello [portalu Azure](https://portal.azure.com), w hello menu centralnym na powitania po lewej, kliknij przycisk **subskrypcje**. Skopiuj hello Nazwa subskrypcji mają toouse podczas uruchamiania skryptów hello w tym przewodniku.
     
     ![Azure Portal](./media/storage-powershell-guide-full/Subscription_Previewportal.png)

    c. toolocate i skopiuj subskrypcji nazwisko hello [klasycznego portalu Azure](https://manage.windowsazure.com/), przewiń w dół i kliknij przycisk **ustawienia** na powitania po lewej stronie portalu hello. Kliknij przycisk **subskrypcje** toosee listę subskrypcji. Nazwa hello kopii subskrypcji, która ma toouse podczas uruchamiania skryptów hello podane w tym przewodniku.
     
     ![klasyczny portal Azure](./media/storage-powershell-guide-full/Subscription_currentportal.png)

   * **$StorageAccountName:** Użyj hello otrzymuje nazwę w skrypcie hello, lub wprowadź nową nazwę dla konta magazynu. **Ważne:** hello nazwa konta magazynu hello musi być unikatowa na platformie Azure. Musi być pisane małymi literami, zbyt!
   * **$Location:** użyć hello "Zachodnie stany USA" podany w skrypcie hello lub wybrać innych lokalizacji platformy Azure, takich jak wschodnie stany USA, Europa Północna, Europa i tak dalej.
   * **$ContainerName:** Użyj hello otrzymuje nazwę w skrypcie hello lub wprowadź nową nazwę dla Twojego kontenera.
   * **$ImageToUpload:** wprowadź obraz tooa ścieżkę na komputerze lokalnym, na przykład: "C:\Images\HelloWorld.png".
   * **$DestinationFolder:** wprowadź ścieżkę tooa katalogu lokalnego toostore pliki pobierane z usługi Magazyn Azure, takich jak: "C:\DownloadImages".
8. Po zaktualizowaniu hello zmienne skryptu w pliku "mystoragescript.ps1" hello, kliknij przycisk **pliku** > **zapisać**. Następnie kliknij przycisk **debugowania** > **Uruchom** lub naciśnij klawisz **F5** toorun hello skryptu.  

Po uruchomieniu skryptu hello powinien mieć folderu lokalne miejsce docelowe, który zawiera hello pobrany plik obrazu. powitania po zrzut ekranu przedstawia przykład danych wyjściowych:

![Pobieranie obiektów blob](./media/storage-powershell-guide-full/Blobdownload.png)

> [!NOTE]
> Witaj "Wprowadzenie do magazynu Azure i programu PowerShell w ciągu 5 minut" sekcji podano szybkie wprowadzenie na temat toouse programu Azure PowerShell z usługą Azure Storage. Aby uzyskać szczegółowe informacje i instrukcje, firma Microsoft zachęca hello tooread następujące sekcje.
> 

## <a name="prerequisites-for-using-azure-powershell-with-azure-storage"></a>Wymagania wstępne dotyczące korzystania z programu Azure PowerShell z usługą Azure Storage
Należy korzystać z platformy Azure i przystąpienie do subskrypcji toorun hello poleceń cmdlet programu PowerShell podane w tym przewodniku, zgodnie z powyższym opisem.

Program Azure PowerShell jest moduł, który udostępnia polecenia cmdlet toomanage Azure za pomocą programu Windows PowerShell. Aby uzyskać informacje na temat instalowania i konfigurowania programu Azure PowerShell, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview). Zaleca się pobrać i zainstalować lub uaktualnić najnowsze modułu Azure PowerShell toohello przed rozpoczęciem korzystania z tego przewodnika.

Możesz uruchamiać polecenia cmdlet hello w konsoli środowiska Windows PowerShell standardowe hello lub hello Windows PowerShell Integrated Scripting Environment (ISE). Na przykład tooopen **programu Windows PowerShell ISE**, przejdź do toohello Start menu, wpisz narzędzia administracyjne i kliknij przycisk toorun go. W oknie Narzędzia administracyjne hello kliknij prawym przyciskiem myszy program Windows PowerShell ISE, kliknij polecenie Uruchom jako Administrator.

## <a name="how-toomanage-storage-accounts-in-azure"></a>Jak kont magazynu toomanage na platformie Azure

Spójrzmy na zarządzanie kontami magazynu na platformie Azure przy użyciu programu PowerShell

### <a name="how-tooset-a-default-azure-subscription"></a>Jak tooset domyślne subskrypcji platformy Azure
toomanage usługi Azure Storage za pomocą programu Azure PowerShell, należy tooauthenticate środowiskiem klienta na platformie Azure przy użyciu uwierzytelniania usługi Azure Active Directory lub uwierzytelniania opartego na certyfikatach. Aby uzyskać szczegółowe informacje, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) samouczka. W tym przewodniku korzysta z uwierzytelniania usługi Azure Active Directory hello.

1. W środowisku Windows PowerShell ISE wpisz następujące polecenie tooadd hello konta Azure toohello PowerShell środowisku lokalnym:

    ```powershell
    Add-AzureAccount
    ```

2. W oknie "Zaloguj się za tooMicrosoft Azure" hello, wpisz adresy e-mail hello i hasło skojarzone z Twoim kontem. Azure służy do uwierzytelniania i zapisuje informacji o poświadczeniach hello, a następnie zamyka okno hello.

3. Następnie uruchom następujące polecenie tooview hello Azure kont w lokalnym środowisku PowerShell i sprawdź, czy Twoje konto jest wyświetlane hello:
   
    ```powershell
    Get-AzureAccount
    ```
4. Następnie uruchom następujące polecenie cmdlet tooview hello wszystkie subskrypcje hello, które są połączone toohello lokalnej sesji programu PowerShell i sprawdź, czy subskrypcja jest wyświetlane:

    ```powershell
    Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName`
    ```
5. tooset domyślne subskrypcji platformy Azure, uruchom polecenie cmdlet hello AzureSubscription wybierz:

    ```powershell
    $SubscriptionName = 'Your subscription Name'
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
    ```

6. Sprawdź nazwę hello hello domyślne subskrypcji przy użyciu polecenia cmdlet Get-AzureSubscription hello:

    ```powershell
    Get-AzureSubscription -Default
    ```

7. toosee Uruchom wszystkie hello dostępne polecenia cmdlet programu PowerShell dla usługi Azure Storage:
    
    ```powershell
    Get-Command -Module Azure -Noun *Storage*`
    ```

### <a name="how-toocreate-a-new-azure-storage-account"></a>Jak toocreate nowe konto magazynu Azure
toouse magazynu Azure, konieczne będzie konto magazynu. Po skonfigurowaniu subskrypcji tooyour tooconnect komputera, można utworzyć nowe konto magazynu platformy Azure.

1. Uruchom wszystkie lokalizacje dostępne datacenter hello toofind polecenia cmdlet Get-AzureLocation hello:

    ```powershell
    Get-AzureLocation | Format-Table -Property Name, AvailableServices, StorageAccountTypes
    ```

2. Następnie przeprowadź toocreate polecenia cmdlet New-AzureStorageAccount hello nowe konto magazynu. Witaj poniższy przykład tworzy nowe konto magazynu w centrum danych "Zachodnie stany USA" hello.
   
    ```powershell
    $location = "West US"
    $StorageAccountName = "yourstorageaccount"
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $location
    ```

> [!IMPORTANT]
> Hello nazwa konta magazynu musi być unikatowa w obrębie platformy Azure i muszą być małymi literami. Ograniczenia i konwencje nazewnictwa, zobacz [o kontach magazynu Azure](../storage-create-storage-account.md) i [nazewnictwa i odwołuje się do kontenerów, obiektów blob i metadanych](http://msdn.microsoft.com/library/azure/dd135715.aspx).
> 
> 

### <a name="how-tooset-a-default-azure-storage-account"></a>Jak tooset domyślne konto magazynu Azure
Może mieć wielu kont magazynu w ramach subskrypcji. Można wybrać jedną z nich i ustaw go jako hello domyślne konto magazynu dla wszystkich hello magazynu polecenia w hello sama sesja programu PowerShell. Dzięki temu możesz toorun hello Azure PowerShell magazynu polecenia bez jawne określenie hello kontekst magazynu.

1. tooset domyślne konto magazynu dla Twojej subskrypcji, możesz uruchomić polecenie cmdlet Set-AzureSubscription hello.

    ```powershell
    $SubscriptionName = "Your subscription name"
    $StorageAccountName = "yourstorageaccount"  
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
    ```

2. Następnie przeprowadź tooverify polecenia cmdlet Get-AzureSubscription hello czy konto magazynu hello jest skojarzony z domyślnego konta subskrypcji. To polecenie zwraca hello właściwości subskrypcji na powitania bieżącej subskrypcji w tym konta magazynu.

    ```powershell
    Get-AzureSubscription –Current
    ```

### <a name="how-toolist-all-azure-storage-accounts-in-a-subscription"></a>Jak toolist magazynu Azure wszystkich kont w ramach subskrypcji
Każda subskrypcja platformy Azure może zawierać maksymalnie too100 kont magazynu. Hello najbardziej aktualne informacje dotyczące limitów znajdują się w temacie [subskrypcji platformy Azure i ograniczenia usługi, przydziały i ograniczenia](../../azure-subscription-service-limits.md).

Uruchom następujące polecenia cmdlet toofind nazwę hello i stanu kont magazynu hello w bieżącej subskrypcji hello hello:

```powershell
Get-AzureStorageAccount | Format-Table -Property StorageAccountName, Location, AccountType, StorageAccountStatus
```

### <a name="how-toocreate-an-azure-storage-context"></a>Jak toocreate kontekst magazynu Azure
Kontekst magazynu Azure jest obiektem w poświadczenia magazynu hello tooencapsulate programu PowerShell. Używanie kontekst magazynu podczas uruchamiania każdego kolejne polecenia cmdlet umożliwia tooauthenticate możesz żądania bez jawne określenie hello konta magazynu i klucza dostępu. Kontekst magazynu można utworzyć na wiele sposobów, na przykład za pomocą magazynu konta nazwy i klucza dostępu, token sygnatury dostępu Współdzielonego dostępu współdzielonego, parametry połączenia lub anonimowych. Aby uzyskać więcej informacji, zobacz [AzureStorageContext nowy](/powershell/module/azure.storage/new-azurestoragecontext).  

Użyj jednej z następujących trzech sposobów toocreate hello kontekst magazynu:

* Uruchom hello [Get-AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) toofind polecenia cmdlet limit klucz dostępu do magazynu podstawowego hello konta magazynu Azure. Następnie wywołaj hello [AzureStorageContext nowy](/powershell/module/azure.storage/new-azurestoragecontext) toocreate polecenia cmdlet kontekst magazynu:

    ```powershell
    $StorageAccountName = "yourstorageaccount"
    $StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
    $Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
    ```

* Generuj token sygnatury dostępu współdzielonego dla kontenera magazynu systemu Azure i korzystać z niego toocreate kontekst magazynu:

    ```powershell
    $sasToken = New-AzureStorageContainerSASToken -Container abc -Permission rl
    $Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -SasToken $sasToken
    ```

    Aby uzyskać więcej informacji, zobacz [AzureStorageContainerSASToken nowy](/powershell/module/azure.storage/new-azurestoragecontainersastoken) i [przy użyciu dostępu sygnatur dostępu Współdzielonego](../storage-dotnet-shared-access-signature-part-1.md).

* W niektórych przypadkach może być punktów końcowych usługi hello toospecify podczas tworzenia nowego kontekst magazynu. Może to być konieczne, gdy zarejestrowano niestandardowej nazwy domeny dla konta magazynu z usługą Blob hello lub toouse sygnatury dostępu współdzielonego mają dostęp do zasobów magazynu. W parametrach połączenia ustawiono hello punktów końcowych usługi i użyj go toocreate nowy kontekst magazynu, jak pokazano poniżej:

    ```powershell
    $ConnectionString = "DefaultEndpointsProtocol=http;BlobEndpoint=<blobEndpoint>;QueueEndpoint=<QueueEndpoint>;TableEndpoint=<TableEndpoint>;AccountName=<AccountName>;AccountKey=<AccountKey>"
    $Ctx = New-AzureStorageContext -ConnectionString $ConnectionString
    ```

Aby uzyskać więcej informacji na temat tooconfigure parametry połączenia magazynu, zobacz [Konfigurowanie parametrów połączenia](../storage-configure-connection-string.md).

Teraz, możesz skonfigurować komputer i przedstawiono sposób toomanage subskrypcji i kont magazynu przy użyciu programu Azure PowerShell Przejdź dalej toolearn sekcji toohello, jak obiekty BLOB toomanage Azure i migawki obiektu blob.

### <a name="how-tooretrieve-and-regenerate-azure-storage-keys"></a>Jak tooretrieve i regenerate klucze magazynu Azure
Konto magazynu Azure ma dwa klucze konta. Możesz użyć następującego polecenia cmdlet tooretrieve hello klucze.

```powershell
Get-AzureStorageKey -StorageAccountName "yourstorageaccount"
```

Użyj następującego polecenia cmdlet tooretrieve określonego klucza hello. Prawidłowe wartości to podstawowe i pomocnicze.  

```powershell
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Primary
    
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Secondary
```

Jeśli chcesz tooregenerate klucze, użyj następującego polecenia cmdlet hello. Prawidłowe wartości właściwości KeyType - to "Primary" i "Secondary"

```powershell
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Primary"
    
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Secondary"
```

## <a name="how-toomanage-azure-blobs"></a>Jak obiekty BLOB toomanage Azure
Magazyn obiektów Blob Azure to usługa do przechowywania dużych ilości danych bez struktury, takich jak dane tekstowe lub binarne, który można uzyskać z dowolnego miejsca w Witaj świecie za pośrednictwem protokołu HTTP lub HTTPS. W tej sekcji założono, że znasz już pojęcia dotyczące usługi magazynu obiektów Blob Azure hello. Aby uzyskać szczegółowe informacje, zobacz [Rozpoczynanie pracy z magazynem obiektów Blob przy użyciu platformy .NET](../blobs/storage-dotnet-how-to-use-blobs.md) i [pojęcia dotyczące usługi Blob](http://msdn.microsoft.com/library/azure/dd179376.aspx).

### <a name="how-toocreate-a-container"></a>Jak toocreate kontenera
Każdy obiekt blob w magazynie Azure musi być w kontenerze. Można utworzyć za pomocą polecenia cmdlet hello AzureStorageContainer nowy kontener prywatnych:

```powershell
$StorageContainerName = "yourcontainername"
New-AzureStorageContainer -Name $StorageContainerName -Permission Off
```

> [!NOTE]
> Istnieją trzy poziomy anonimowy dostęp do odczytu: **poza**, **obiektu Blob**, i **kontenera**. tooprevent anonimowego dostępu zbyt tooblobs, parametr uprawnienia hello zestawu**poza**. Domyślnie nowy kontener hello jest prywatny i jest możliwy tylko przez właściciela konta hello. odczytu tooallow publicznego anonimowy dostęp do zasobów tooblob, ale nie toocontainer metadanych lub toohello listę obiektów blob w kontenerze hello, ustaw parametr uprawnienia hello zbyt**obiektu Blob**. tooallow publicznego Pełny odczyt dostęp do zasobów tooblob metadanych kontenera i hello listę obiektów blob w kontenerze hello, ustaw parametr uprawnienia hello zbyt**kontenera**. Aby uzyskać więcej informacji, zobacz [Zarządzanie toocontainers anonimowy dostęp do odczytu i obiekty BLOB](../blobs/storage-manage-access-to-resources.md).
> 
> 

### <a name="how-tooupload-a-blob-into-a-container"></a>Jak tooupload obiektu blob do kontenera
Azure Blob Storage obsługuje blokowe i stronicowe obiekty blob. Aby uzyskać więcej informacji, zobacz [opis blokowych obiektów blob, Dołącz obiektów blob i stronicowe obiekty BLOB](http://msdn.microsoft.com/library/azure/ee691964.aspx).

tooupload obiekty BLOB w kontenerze tooa, można użyć hello [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) polecenia cmdlet. Domyślnie to polecenie wysyła hello lokalne pliki tooa — obiekt blob blokowy. Typ hello toospecify hello obiektu blob, można użyć parametru - BlobType hello.

Witaj poniższym przykładzie uruchamiane są hello [Get-ChildItem](http://technet.microsoft.com/library/hh849800.aspx) tooget polecenia cmdlet hello wszystkie pliki w określonym folderze hello, a następnie przesyła je dalej polecenia cmdlet toohello za pomocą operatora potoku hello. Witaj [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) kontenera tooyour pliki lokalne powitania przekazuje polecenia cmdlet:

```powershell
Get-ChildItem –Path C:\Images\* | Set-AzureStorageBlobContent -Container "yourcontainername"
```

### <a name="how-toodownload-blobs-from-a-container"></a>Jak toodownload obiektów blob z kontenera
Witaj poniższy przykład pokazuje, jak toodownload obiektów blob z kontenera. przykład Witaj najpierw ustanawia tooAzure połączenia magazynu przy użyciu kontekstu konta magazynu hello, w tym nazwy konta magazynu hello i jego podstawowy klucz dostępu. Następnie przykład Witaj pobiera odwołanie do obiektu blob przy użyciu hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) polecenia cmdlet. Następnie przykład Witaj używa hello [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) obiekty BLOB toodownload polecenia cmdlet do folderu docelowego lokalne powitania.

```powershell
#Define hello variables.
$ContainerName = "yourcontainername"
$DestinationFolder = "C:\DownloadImages"

#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#List all blobs in a container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Download blobs from a container.
New-Item -Path $DestinationFolder -ItemType Directory -Force
$blobs | Get-AzureStorageBlobContent -Destination $DestinationFolder -Context $Ctx
```

### <a name="how-toocopy-blobs-from-one-storage-container-tooanother"></a>Jak toocopy obiektów blob z jednego tooanother kontenera magazynu
Asynchronicznie należy skopiować obiekty BLOB na kontach magazynu i regionów. Witaj poniższym przykładzie pokazano, jak toocopy obiektów blob z jednego magazynu tooanother kontenera w dwóch różnych kont magazynu. przykład Witaj najpierw ustawia zmienne dla konta magazynu źródłowego i docelowego, a następnie tworzy kontekst magazynu dla poszczególnych kont. Następnie przykład Witaj kopiuje obiekty BLOB z hello źródła kontenera toohello docelowy kontener przy użyciu hello [Start AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) polecenia cmdlet. przykład Witaj przyjęto założenie, że konta magazynu źródłowego i docelowego hello i kontenery już istnieje.

```powershell
#Define hello source storage account and context.
$SourceStorageAccountName = "yoursourcestorageaccount"
$SourceStorageAccountKey = "Storage key for yoursourcestorageaccount"
$SrcContainerName = "yoursrccontainername"
$SourceContext = New-AzureStorageContext -StorageAccountName $SourceStorageAccountName -StorageAccountKey $SourceStorageAccountKey

#Define hello destination storage account and context.
$DestStorageAccountName = "yourdeststorageaccount"
$DestStorageAccountKey = "Storage key for yourdeststorageaccount"
$DestContainerName = "destcontainername"
$DestContext = New-AzureStorageContext -StorageAccountName $DestStorageAccountName -StorageAccountKey $DestStorageAccountKey

#Get a reference tooblobs in hello source container.
$blobs = Get-AzureStorageBlob -Container $SrcContainerName -Context $SourceContext

#Copy blobs from one container tooanother.
$blobs| Start-AzureStorageBlobCopy -DestContainer $DestContainerName -DestContext $DestContext
```

Należy pamiętać, że w tym przykładzie wykonuje asynchroniczne kopiowania. Możesz monitorować stan hello każdej kopii uruchamiając hello [Get-AzureStorageBlobCopyState](/powershell/module/azure.storage/start-azurestorageblobcopystate) polecenia cmdlet.

### <a name="how-toocopy-blobs-from-a-secondary-location"></a>Jak toocopy obiektów blob z lokalizacji dodatkowej
Obiekty BLOB można skopiować z lokalizacji dodatkowej hello RA-GRS włączone konta.

```powershell
#define secondary storage context using a connection string constructed from secondary endpoints.
$SrcContext = New-AzureStorageContext -ConnectionString "DefaultEndpointsProtocol=https;AccountName=***;AccountKey=***;BlobEndpoint=http://***-secondary.blob.core.windows.net;FileEndpoint=http://***-secondary.file.core.windows.net;QueueEndpoint=http://***-secondary.queue.core.windows.net; TableEndpoint=http://***-secondary.table.core.windows.net;"
Start-AzureStorageBlobCopy –Container *** -Blob *** -Context $SrcContext –DestContainer *** -DestBlob *** -DestContext $DestContext
```

### <a name="how-toodelete-a-blob"></a>Jak toodelete obiektu blob
toodelete obiektu blob, najpierw pobrać odwołanie do obiektu blob, a następnie wywołaj polecenie cmdlet Remove-AzureStorageBlob hello na nim. Poniższy przykład Hello usuwa wszystkie hello obiekty BLOB w danym kontenerze. przykład Witaj najpierw ustawia zmienne dla konta magazynu, a następnie tworzy kontekst magazynu. Następnie przykład Witaj pobiera odwołanie do obiektu blob przy użyciu hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) hello polecenia cmdlet i działa [AzureStorageBlob Usuń](/powershell/module/azure.storage/remove-azurestorageblob) obiekty BLOB tooremove polecenia cmdlet z kontenera w magazynie Azure.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "containername"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference tooall hello blobs in hello container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Delete blobs in a specified container.
$blobs| Remove-AzureStorageBlob
```

## <a name="how-toomanage-azure-blob-snapshots"></a>Jak toomanage Azure blob migawki
Azure umożliwia tworzenie migawki obiektu blob. Migawka jest tylko do odczytu wersji obiektu blob, która jest wykonywana w punkcie w czasie. Po utworzeniu migawki, to można można odczytać, kopiowane, lub usunięte, ale nie został zmodyfikowany. Migawki zapewniają tooback sposób się obiektu blob znajduje się na chwilę w czasie. Aby uzyskać więcej informacji, zobacz [tworzenia migawki obiektu Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).

### <a name="how-toocreate-a-blob-snapshot"></a>Jak toocreate migawki obiektu blob
toocreate snaphot obiektu blob, najpierw pobrać odwołanie do obiektu blob, a następnie wywołać hello `ICloudBlob.CreateSnapshot` dla niego metodę. Witaj poniższym przykładzie najpierw ustawia zmienne dla konta magazynu, a następnie tworzy kontekst magazynu. Następnie przykład Witaj pobiera odwołanie do obiektu blob przy użyciu hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) hello polecenia cmdlet i działa [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) toocreate metody migawki.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "yourcontainername"
$BlobName = "yourblobname"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference tooa blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $ContainerName -Blob $BlobName

#Create a snapshot of hello blob.
$snap = $blob.ICloudBlob.CreateSnapshot()
```

### <a name="how-toolist-a-blobs-snapshots"></a>Jak migawki toolist obiektu blob
Można utworzyć dowolną liczbę migawek do obiektu blob. Możesz wyświetlić listę hello migawki skojarzone z tootrack Twojego obiektu blob z bieżącej migawki. Witaj poniższym przykładzie użyto wstępnie zdefiniowanych obiektów blob i wywołania hello [Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) migawek hello toolist polecenia cmdlet tego obiektu blob.  

```powershell
#Define hello blob name.
$BlobName = "yourblobname"

#List hello snapshots of a blob.
Get-AzureStorageBlob –Context $Ctx -Prefix $BlobName -Container $ContainerName  | Where-Object  { $_.ICloudBlob.IsSnapshot -and $_.Name -eq $BlobName }
```

### <a name="how-toocopy-a-snapshot-of-a-blob"></a>Jak toocopy migawki obiektu blob
Możesz skopiować migawki obiektu blob toorestore hello migawki. Aby uzyskać szczegółowe informacje i ograniczenia, zobacz [tworzenia migawki obiektu Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx). Witaj poniższym przykładzie najpierw ustawia zmienne dla konta magazynu, a następnie tworzy kontekst magazynu. Przykład Witaj definiuje następnie hello zmienne nazwa kontenera i obiektów blob. przykład Witaj pobiera odwołanie do obiektu blob przy użyciu hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) hello polecenia cmdlet i działa [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) toocreate metody migawki. Następnie przykład Witaj uruchamia hello [Start AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) polecenia cmdlet toocopy hello migawki obiektu blob przy użyciu obiektu ICloudBlob hello na powitania źródłowego obiektu blob. Należy się, że zmienne hello tooupdate zgodnie z konfiguracją przed uruchomionych przykład Witaj. Należy zauważyć, że ten hello poniższy przykład przyjęto założenie, że hello źródłowego i docelowego kontenery i hello źródłowego obiektu blob już istnieje.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Define hello variables.
$SrcContainerName = "yoursourcecontainername"
$DestContainerName = "yourdestcontainername"
$SrcBlobName = "yourblobname"
$DestBlobName = "CopyBlobName"

#Get a reference tooa blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $SrcContainerName -Blob $SrcBlobName

#Create a snapshot of a blob.
$snap = $blob.ICloudBlob.CreateSnapshot()

#Copy hello snapshot tooanother container.
Start-AzureStorageBlobCopy –Context $Ctx -ICloudBlob $snap -DestBlob $DestBlobName -DestContainer $DestContainerName
```

Teraz, gdy uzyskanych jak obiekty BLOB toomanage Azure i obiektów blob migawki przy użyciu programu Azure PowerShell Przejdź toohello dalej toolearn sekcji jak toomanage tabel, kolejek i plików.

## <a name="how-toomanage-azure-tables-and-table-entities"></a>Jak toomanage Azure tabele i tabela jednostek
Azure usługi Magazyn tabel jest magazynem danych NoSQL, którego można użyć toostore i zapytań dotyczących dużych zestawów strukturalnych danych nierelacyjnych. głównymi składnikami usługi hello Hello są tabele, jednostki i właściwości. Tabela jest kolekcji jednostek. Jednostka jest zbiór właściwości. Każdy obiekt może zawierać maksymalnie too252 właściwości, które są wszystkie pary nazwa wartość. W tej sekcji założono, że znasz już pojęcia dotyczące usługi Magazyn tabel Azure hello. Aby uzyskać szczegółowe informacje, zobacz [hello opis modelu danych usługi tabel](http://msdn.microsoft.com/library/azure/dd179338.aspx) i [Rozpoczynanie pracy z magazynem tabel Azure przy użyciu platformy .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md).

Następujące podpunkty hello dowiesz się, jak usługa toomanage magazynu tabel Azure przy użyciu programu Azure PowerShell. Witaj omówione scenariusze obejmują **tworzenie**, **usuwanie**, i **pobierania** **tabel**, jak również **Dodawanie**, **badania**, i **usuwania jednostek tabeli**.

### <a name="how-toocreate-a-table"></a>Jak toocreate tabeli
Każda tabela musi znajdować się na koncie magazynu platformy Azure. Witaj poniższym przykładzie pokazano, jak toocreate tabeli w usłudze Azure Storage. przykład Witaj najpierw ustanawia tooAzure połączenia magazynu przy użyciu kontekstu konta magazynu hello, w tym nazwy konta magazynu hello i jego klucz dostępu. Następnie używa hello [AzureStorageTable nowy](/powershell/module/azure.storage/new-azurestoragetable) toocreate polecenia cmdlet tabeli w usłudze Azure Storage.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey

#Create a new table.
$tabName = "yourtablename"
New-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-tooretrieve-a-table"></a>Jak tooretrieve tabeli
Można zbadać i pobrać jednego lub wszystkich tabel na koncie magazynu. Witaj poniższym przykładzie pokazano, jak przy użyciu danej tabeli tooretrieve hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) polecenia cmdlet.

```powershell
#Retrieve a table.
$tabName = "yourtablename"
Get-AzureStorageTable –Name $tabName –Context $Ctx
```

Wywołanie polecenia cmdlet Get-AzureStorageTable hello bez żadnych parametrów, pobiera wszystkie tabele magazynu dla konta magazynu.

### <a name="how-toodelete-a-table"></a>Jak toodelete tabeli
Z konta magazynu można usunąć tabeli, za pomocą hello [AzureStorageTable Usuń](/powershell/module/azure.storage/remove-azurestoragetable) polecenia cmdlet.  

```powershell
#Delete a table.
$tabName = "yourtablename"
Remove-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-toomanage-table-entities"></a>Jak toomanage Tabela jednostek
Obecnie programu Azure PowerShell nie zapewnia bezpośrednio jednostek tabeli toomanage polecenia cmdlet. tooperform operacje na jednostkach tabeli, można użyć klasy hello podany w hello [biblioteki klienta magazynu Azure dla platformy .NET](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).

#### <a name="how-tooadd-table-entities"></a>Jak tooadd Tabela jednostek
Tabela tooa jednostek tooadd najpierw utworzyć obiekt, który definiuje właściwości jednostki. Jednostka może mieć właściwości too255, łącznie z 3 Właściwości systemowe: **PartitionKey**, **RowKey**, i **sygnatury czasowej**. Jest odpowiedzialny za wstawiania i aktualizowania wartości hello **PartitionKey** i **RowKey**. Hello podlegało zarządzaniu przez serwer wartość hello **sygnatury czasowej**, która nie może być modyfikowany. Razem hello **PartitionKey** i **RowKey** jednoznacznie zidentyfikować każdej jednostki w tabeli.

* **PartitionKey**: Określa jednostki hello są przechowywane w partycji hello.
* **RowKey**: unikatowo identyfikuje hello jednostek w partycji hello.

Można zdefiniować niestandardowe właściwości too252 dla jednostki. Aby uzyskać więcej informacji, zobacz [hello opis modelu danych usługi tabel](http://msdn.microsoft.com/library/azure/dd179338.aspx).

Witaj poniższym przykładzie pokazano, jak tooadd jednostek tooa tabeli. przykład Witaj pokazuje, jak tooretrieve hello tabeli pracowników i dodać kilka podmiotów do niego. Po pierwsze, nawiązaniem połączenia tooAzure magazynu przy użyciu kontekstu konta magazynu hello, w tym nazwy konta magazynu hello i jego klucz dostępu. Następnie pobiera ona hello podanej tabeli za pomocą hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) polecenia cmdlet. Jeśli hello tabela nie istnieje, hello [AzureStorageTable nowy](/powershell/module/azure.storage/new-azurestoragetable) polecenia cmdlet jest używane toocreate tabeli w usłudze Azure Storage. Następnie przykład Witaj definiuje funkcję niestandardowych Dodaj jednostki tooadd jednostek toohello tabeli przez określenie poszczególnych partycji i klucz wiersza. Witaj Dodaj jednostki Witaj wywołania funkcji [New-Object](http://technet.microsoft.com/library/hh849885.aspx) polecenia cmdlet na powitania [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) toocreate klasy do obiektu jednostki. Później, przykład Witaj wywołuje hello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) metody w tym tooadd obiekt jednostki go tooa tabeli.

```powershell
#Function Add-Entity: Adds an employee entity tooa table.
function Add-Entity() {
    [CmdletBinding()]
    param(
       $table,
       [String]$partitionKey,
       [String]$rowKey,
       [String]$name,
       [Int]$id
    )

  $entity = New-Object -TypeName Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity -ArgumentList $partitionKey, $rowKey
  $entity.Properties.Add("Name", $name)
  $entity.Properties.Add("ID", $id)

  $result = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Insert($entity))
}

#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Retrieve hello table if it already exists.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx -ErrorAction Ignore

#Create a new table if it does not exist.
if ($table -eq $null)
{
   $table = New-AzureStorageTable –Name $TableName -Context $Ctx
}

#Add multiple entities tooa table.
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row1 -Name Chris -Id 1
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row2 -Name Jessie -Id 2
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row1 -Name Christine -Id 3
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row2 -Name Steven -Id 4
```

#### <a name="how-tooquery-table-entities"></a>Jak tooquery Tabela jednostek
tooquery tabelę, użyj hello [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) klasy. Witaj poniższym przykładzie przyjęto założenie, zostały już uruchomione hello skrypt podanych w hello jak tooadd jednostek części tego przewodnika. przykład Witaj najpierw ustanawia tooAzure połączenia magazynu przy użyciu hello kontekst magazynu, który zawiera nazwy konta magazynu hello i klucza dostępu. Następnie próbuje tabeli hello wcześniej utworzony "pracownicy" tooretrieve przy użyciu hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) polecenia cmdlet. Wywoływanie hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) polecenia cmdlet na powitania klasy Microsoft.WindowsAzure.Storage.Table.TableQuery tworzy nowy obiekt zapytania. przykład Witaj szuka hello obiektów, które mają kolumnę 'ID', którego wartość wynosi 1, ponieważ określony w filtrze ciągu. Aby uzyskać szczegółowe informacje, zobacz [badania tabel i jednostek](http://msdn.microsoft.com/library/azure/dd894031.aspx). Po uruchomieniu to zapytanie zwraca wszystkich jednostek spełniających kryteria filtru hello.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Get a reference tooa table.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx

#Create a table query.
$query = New-Object Microsoft.WindowsAzure.Storage.Table.TableQuery

#Define columns tooselect.
$list = New-Object System.Collections.Generic.List[string]
$list.Add("RowKey")
$list.Add("ID")
$list.Add("Name")

#Set query details.
$query.FilterString = "ID gt 0"
$query.SelectColumns = $list
$query.TakeCount = 20

#Execute hello query.
$entities = $table.CloudTable.ExecuteQuery($query)

#Display entity properties with hello table format.
$entities  | Format-Table PartitionKey, RowKey, @{ Label = "Name"; Expression={$_.Properties["Name"].StringValue}}, @{ Label = "ID"; Expression={$_.Properties["ID"].Int32Value}} -AutoSize
```

#### <a name="how-toodelete-table-entities"></a>Jak toodelete Tabela jednostek
Można usunąć jednostki przy użyciu jego kluczy partycji i wiersza. Witaj poniższym przykładzie przyjęto założenie, zostały już uruchomione hello skrypt podanych w hello jak tooadd jednostek części tego przewodnika. przykład Witaj najpierw ustanawia tooAzure połączenia magazynu przy użyciu hello kontekst magazynu, który zawiera nazwy konta magazynu hello i klucza dostępu. Następnie próbuje tabeli hello wcześniej utworzony "pracownicy" tooretrieve przy użyciu hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) polecenia cmdlet. Jeśli istnieje tabela hello, przykład Witaj wywołuje hello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) tooretrieve metody jednostki na podstawie jego wartości klucza partycji i wiersza. Przekazuj hello jednostki toohello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) toodelete metody.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve hello table.
$TableName = "Employees"
$table = Get-AzureStorageTable -Name $TableName -Context $Ctx -ErrorAction Ignore

#If hello table exists, start deleting its entities.
if ($table -ne $null) 
{
    #Together hello PartitionKey and RowKey uniquely identify every  
    #entity within a table.
    $tableResult = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Retrieve("Partition2", "Row1"))
    $entity = $tableResult.Result
    if ($entity -ne $null)
    {
        #Delete hello entity.
        $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Delete($entity))
    }
}
```

## <a name="how-toomanage-azure-queues-and-queue-messages"></a>Jak toomanage Azure kolejki i wiadomości w kolejce
Magazyn kolejek Azure to usługa do przechowywania dużej liczby komunikatów, które można uzyskać z dowolnego miejsca w Witaj świecie za pośrednictwem uwierzytelnionego połączenia za pomocą protokołu HTTP lub HTTPS. W tej sekcji założono, że znasz już pojęcia dotyczące usługi magazynu kolejek Azure hello. Aby uzyskać szczegółowe informacje, zobacz [Rozpoczynanie pracy z magazynem kolejek Azure przy użyciu platformy .NET](../storage-dotnet-how-to-use-queues.md).

W tej sekcji opisano sposób toomanage magazynu kolejek Azure usługi przy użyciu programu Azure PowerShell. Hello omówione scenariusze obejmują **wstawianie** i **usuwanie** kolejki komunikatów, a także **tworzenie**, **usuwanie**i **pobierania kolejek**.

### <a name="how-toocreate-a-queue"></a>Jak toocreate kolejki
Witaj poniższym przykładzie najpierw ustanawia tooAzure połączenia magazynu przy użyciu kontekstu konta magazynu hello, w tym nazwy konta magazynu hello i jego klucz dostępu. Następnie wywołuje [AzureStorageQueue nowy](/powershell/module/azure.storage/new-azurestoragequeue) toocreate polecenia cmdlet kolejki o nazwie "queuename".

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$QueueName = "queuename"
$Queue = New-AzureStorageQueue –Name $QueueName -Context $Ctx
```

Aby uzyskać informacji na temat konwencji nazewnictwa dla usługi kolejek platformy Azure, zobacz [nazewnictwo kolejek i metadanych](http://msdn.microsoft.com/library/azure/dd179349.aspx).

### <a name="how-tooretrieve-a-queue"></a>Jak tooretrieve kolejki
Można zbadać i pobrać określonej kolejki, a także listę wszystkich kolejek hello na koncie magazynu. Witaj poniższym przykładzie pokazano, jak przy użyciu określonej kolejki tooretrieve hello [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) polecenia cmdlet.

```powershell
#Retrieve a queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue –Name $QueueName –Context $Ctx
```

Jeśli wywołujesz hello [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) polecenia cmdlet bez parametrów, pobiera listę wszystkich kolejek hello.

### <a name="how-toodelete-a-queue"></a>Jak toodelete kolejki
toodelete kolejkę i wszystkie wiadomości powitania zawartych w nim polecenia cmdlet Remove-AzureStorageQueue hello wywołania. Witaj poniższy przykład pokazuje, jak przy użyciu określonej kolejki toodelete hello polecenia cmdlet Remove-AzureStorageQueue.

```powershell
#Delete a queue.
$QueueName = "yourqueuename"
Remove-AzureStorageQueue –Name $QueueName –Context $Ctx
```

#### <a name="how-tooinsert-a-message-into-a-queue"></a>Jak tooinsert wiadomości w kolejce
tooinsert komunikat do istniejącej kolejki, najpierw utwórz nowe wystąpienie klasy hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) klasy. Następnie wywołaj hello [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) metody. CloudQueueMessage można utworzyć z ciągu (w formacie UTF-8) lub tablicy bajtów.

Hello poniższy przykład pokazuje, jak tooadd komunikatu tooa kolejki. przykład Witaj najpierw ustanawia tooAzure połączenia magazynu przy użyciu kontekstu konta magazynu hello, w tym nazwy konta magazynu hello i jego klucz dostępu. Następnie pobiera ona hello określonej kolejki przy użyciu hello [Get-AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) polecenia cmdlet. Jeśli hello kolejka istnieje, hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) polecenia cmdlet jest używane toocreate wystąpienia hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) klasy. Później, przykład Witaj wywołuje hello [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) metody w tej wiadomości obiektu tooadd go tooa kolejki. Oto kod, który pobiera kolejki i wstawia wiadomości powitania "MessageInfo":

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve hello queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

#If hello queue exists, add a new message.
if ($Queue -ne $null) {
   # Create a new message using a constructor of hello CloudQueueMessage class.
   $QueueMessage = New-Object -TypeName Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage -ArgumentList MessageInfo

   # Add a new message toohello queue.
   $Queue.CloudQueue.AddMessage($QueueMessage)
}
```

#### <a name="how-toode-queue-at-hello-next-message"></a>Jak kolejki toode na powitania obok komunikatu
Twój kod usuwa komunikat z kolejki w dwóch etapach. Podczas wywoływania hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) metody, otrzymasz hello następnej wiadomości w kolejce. Komunikat zwrócony z **GetMessage** staje się niewidoczny tooany innego kodu odczytującego komunikaty z tej kolejki. toofinish usuwania wiadomość hello z kolejki hello, musisz również wywołać hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) metody. Ten dwuetapowy proces usuwania komunikatów gwarantuje, że jeśli kod nie powiedzie się tooprocess, który można uzyskać komunikatu powodu awarii toohardware lub oprogramowania, inne wystąpienie kodu tę samą wiadomość hello i spróbuj ponownie. Twój kod wywołuje **DeleteMessage** natychmiast po przetworzeniu wiadomość hello.

```powershell
# Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

# Retrieve hello queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

$InvisibleTimeout = [System.TimeSpan]::FromSeconds(10)

# Get hello message object from hello queue.
$QueueMessage = $Queue.CloudQueue.GetMessage($InvisibleTimeout)
# Delete hello message.
$Queue.CloudQueue.DeleteMessage($QueueMessage)
```

## <a name="how-toomanage-azure-file-shares-and-files"></a>Jak toomanage plików na platformę Azure udostępnia i pliki
Magazyn plików Azure oferuje współużytkowany magazyn dla aplikacji używających standardowego protokołu SMB hello. Maszyny wirtualne Microsoft Azure i usługi w chmurze mogą udostępniać dane między składnikami aplikacji za pośrednictwem zainstalowanych udziałów i lokalnych aplikacji można uzyskać dostępu do danych plików w udziale za pomocą interfejsu API magazynu plików hello lub Azure PowerShell.

Aby uzyskać więcej informacji dotyczących usługi Magazyn plików Azure, zobacz [Rozpoczynanie pracy z magazynem plików Azure w systemie Windows](../storage-dotnet-how-to-use-files.md) i [interfejsu API REST usługi plików](http://msdn.microsoft.com/library/azure/dn167006.aspx).

## <a name="how-tooset-and-query-storage-analytics"></a>Jak tooset i zapytań analiz magazynu
Można użyć [analityka magazynu Azure](../storage-analytics.md) toocollect metryki dla konta magazynu platformy Azure i dane dziennika o żądaniach wysyłane tooyour konta magazynu. Można użyć magazynu metryki toomonitor hello kondycji konta magazynu oraz magazynu toodiagnose rejestrowania i rozwiązywać problemy z kontem magazynu. Można skonfigurować monitorowanie za pomocą hello portalu Azure lub programu Windows PowerShell, albo programowo z użyciem biblioteki klienta usługi storage hello. Rejestrowanie magazynu wykonywany po stronie serwera i umożliwia toorecord szczegóły zarówno udane, jak i nieudane żądania na koncie magazynu. Te dzienniki Włącz szczegóły toosee odczytu, zapisu i usuwania operacje z tabel, kolejek i obiektów blob także hello powody żądań zakończonych niepowodzeniem.

toolearn tooenable i wyświetlanie danych metryk magazynu przy użyciu programu PowerShell, zobacz temat [jak tooenable metryki magazynu przy użyciu programu PowerShell](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell).

toolearn tooenable i pobrać rejestrowania magazynu danych przy użyciu programu PowerShell, zobacz temat [jak tooenable magazynu rejestrowanie przy użyciu programu PowerShell](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) i [znajdowanie rejestrowania magazynu danych dziennika](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata).
Aby uzyskać szczegółowe informacje na temat używania metryki magazynu i rejestrowania problemów z magazynowaniem tootroubleshoot magazynu, zobacz [monitorowanie, diagnozowanie i rozwiązywanie problemów z programem Microsoft Azure Storage](../storage-monitoring-diagnosing-troubleshooting.md).

## <a name="how-toomanage-shared-access-signature-sas-and-stored-access-policy"></a>Jak udostępnione toomanage podpis dostępu (SAS) i przechowywane zasady dostępu
Sygnatury dostępu współdzielonego są ważnym elementem modelu zabezpieczeń powitania dla dowolnej aplikacji przy użyciu usługi Azure Storage. Są one przydatne zapewniające tooclients konta magazynu tooyour ograniczone uprawnienia, które nie powinny mieć hello klucz konta. Domyślnie obiekty BLOB, tabel i kolejek w ramach tego konta może uzyskiwać dostęp tylko jego właściciel hello hello konta magazynu. Jeśli daną usługą lub aplikacją musi toomake Ci klienci tooother dostępne zasoby bez udostępniania klucz dostępu, dostępne są trzy opcje:

* Ustaw kontenera uprawnienia toopermit anonimowy dostęp do odczytu toohello kontenera i jego obiektów blob. Jest to niedozwolone dla tabel lub kolejek.
* Użyj sygnatury dostępu współdzielonego przyznająca toocontainers praw dostępu ograniczonego, obiekty BLOB, kolejek i tabel dla określonego interwału.
* Użyj tooobtain zasad dostępu do przechowywanych dodatkowy poziom kontroli nad sygnatur dostępu współdzielonego dla kontenera lub jego obiektów blob, kolejki lub tabeli. Witaj przechowywanych zasada dostępu zezwala na możesz czas rozpoczęcia hello toochange, czas wygaśnięcia lub uprawnień do podpisu, lub toorevoke po nim został wydany.

Sygnatury dostępu współdzielonego, można w jednym z dwóch formach:

* **Ad hoc SAS**: podczas tworzenia sygnatury dostępu Współdzielonego ad hoc, godzina rozpoczęcia hello, czas wygaśnięcia i uprawnienia dla hello SAS są określone na powitania identyfikatora URI połączenia SAS. Ten typ sygnatury dostępu Współdzielonego może zostać utworzony w kontenerze, obiektów blob, tabeli lub kolejki i jest z systemem innym niż odwoływalny.
* **Sygnatury dostępu Współdzielonego z zasadami dostępu do przechowywanych**: zasady dostępu do przechowywanych jest zdefiniowany w kontenerze zasobu kontenera obiektów blob, tabel lub kolejek — i umożliwia toomanage ograniczenia dla co najmniej jeden sygnatur dostępu współdzielonego. Po skojarzeniu sygnatury dostępu Współdzielonego za pomocą zasad dostępu przechowywane, hello SAS dziedziczy ograniczenia hello — uprawnienia - zdefiniowane zasady dostępu hello przechowywane, czas wygaśnięcia i godzina rozpoczęcia hello. Ten typ sygnatury dostępu Współdzielonego jest odwoływalny.

Aby uzyskać więcej informacji, zobacz [przy użyciu dostępu sygnatur dostępu Współdzielonego](../storage-dotnet-shared-access-signature-part-1.md) i [Zarządzanie toocontainers anonimowy dostęp do odczytu i obiekty BLOB](../blobs/storage-manage-access-to-resources.md).

W kolejnych sekcjach hello przedstawiono sposób toocreate zasady dostępu współdzielonego podpisu tokenu i przechowywane dostęp do tabel Azure. Program Azure PowerShell udostępnia podobne polecenia cmdlet dla kontenerów, obiektów blob i kolejek oraz. skrypty hello toorun w tej sekcji, Pobierz hello [Azure PowerShell w wersji 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) lub nowszym.

### <a name="how-toocreate-a-policy-based-shared-access-signature-token"></a>Jak token sygnatura dostępu współdzielonego toocreate oparta na zasadach
Użyj toocreate polecenia cmdlet New-AzureStorageTableStoredAccessPolicy hello Nowa zasada dostępu przechowywane. Następnie wywołaj metodę hello [AzureStorageTableSASToken nowy](/powershell/module/azure.storage/new-azurestoragetablesastoken) toocreate polecenia cmdlet nowy token podpisu na podstawie zasad dostępu współdzielonego dla tabeli magazynu Azure.

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
New-AzureStorageTableSASToken -Name $tableName -Policy $policy -Context $Ctx
```

### <a name="how-toocreate-an-ad-hoc-non-revocable-shared-access-signature-token"></a>Jak toocreate token ad hoc sygnatura dostępu współdzielonego (z systemem innym niż — odwoływalny)
Użyj hello [AzureStorageTableSASToken nowy](/powershell/module/azure.storage/new-azurestoragetablesastoken) toocreate polecenia cmdlet nowy ad hoc (z systemem innym niż — odwoływalny) Sygnatura dostępu współdzielonego token dla tabeli magazynu Azure:

```powershell
New-AzureStorageTableSASToken -Name $tableName -Permission "rqud" -StartTime "2015-01-01" -ExpiryTime "2015-02-01" -Context $Ctx
```
    
### <a name="how-toocreate-a-stored-access-policy"></a>Jak toocreate zasad dostępu przechowywane
Użyj hello AzureStorageTableStoredAccessPolicy nowe polecenia cmdlet toocreate Nowa zasada dostępu przechowywanych dla tabeli magazynu Azure:

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
```
    
### <a name="how-tooupdate-a-stored-access-policy"></a>Jak tooupdate zasad dostępu przechowywane
Użyj tooupdate polecenia cmdlet Set-AzureStorageTableStoredAccessPolicy hello istniejących zasad dostępu do przechowywanych dla tabeli magazynu Azure:

```powershell
Set-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Permission "rd" -NoExpiryTime -NoStartTime -Context $Ctx
```

### <a name="how-toodelete-a-stored-access-policy"></a>Jak toodelete zasad dostępu przechowywane
Użyj toodelete polecenia cmdlet Remove-AzureStorageTableStoredAccessPolicy hello zasad dostępu do przechowywanych w tabeli magazynu Azure:

```powershell
Remove-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Context $Ctx
```

## <a name="how-toouse-azure-storage-for-us-government-and-azure-china"></a>Jak toouse magazynu Azure dla instytucji rządowych USA i Chińskiej wersji platformy Azure
Środowiska platformy Azure jest niezależnie od wdrożenia programu Microsoft Azure, takich jak [Azure dla instytucji rządowych USA administracji](https://azure.microsoft.com/features/gov/), [AzureCloud globalne Azure](https://portal.azure.com), i [AzureChinaCloud dla platformy Azure obsługiwane przez 21Vianet w Chinach](http://www.windowsazure.cn/). Można wdrażać nowe środowisk Azure dla instytucji rządowych USA i Chińskiej wersji platformy Azure.

toouse magazynu Azure z AzureChinaCloud należy toocreate kontekst magazynu, który jest skojarzony z AzureChinaCloud. Wykonaj te kroki tooget, możesz uruchomić:

1. Uruchom hello [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) toosee polecenia cmdlet hello dostępnego środowiska platformy Azure:
   
    ```powershell
    Get-AzureEnvironment
    ```

2. Dodaj tooWindows konta chińskiej wersji platformy Azure PowerShell:
   
    ```powershell
    Add-AzureAccount –Environment AzureChinaCloud
    ```

3. Tworzenie magazynu kontekstu konta AzureChinaCloud:
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureChinaCloud
    ```

toouse usługi Azure Storage z [stany USA Azure dla instytucji rządowych](https://azure.microsoft.com/features/gov/), należy zdefiniować nowe środowisko i następnie tworzy nowy kontekst magazynu z tym środowiskiem:

1. Uruchom hello [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) toosee polecenia cmdlet hello dostępnego środowiska platformy Azure:

    ```powershell
    Get-AzureEnvironment
    ```

2. Dodaj tooWindows konta Azure instytucji rządowych Stanów Zjednoczonych środowiska PowerShell:
   
    ```powershell
    Add-AzureAccount –Environment AzureUSGovernment
    ```

3. Tworzenie magazynu kontekstu konta AzureUSGovernment:
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureUSGovernment
    ```
     
Aby uzyskać więcej informacji, zobacz:

* [Przewodnik dewelopera usługi Microsoft Azure dla instytucji rządowych](../../azure-government/documentation-government-developer-guide.md).
* [Omówienie różnic podczas tworzenia aplikacji w usłudze Chin](https://msdn.microsoft.com/library/azure/dn578439.aspx)

## <a name="next-steps"></a>Następne kroki
W tym przewodniku, kiedy znasz już jak toomanage usługi Azure Storage przy użyciu programu Azure PowerShell. Poniżej przedstawiono niektóre pokrewne artykuły i zasoby dowiedzieć się więcej o nich.

* [Dokumentacja usługi Azure Storage](https://azure.microsoft.com/documentation/services/storage/)
* [Polecenia cmdlet programu PowerShell usługi Azure Storage](/powershell/module/azurerm.storage/#storage)
* [Dokumentacja programu PowerShell systemu Windows](https://msdn.microsoft.com/library/ms714469.aspx)

[Getting started with Azure Storage and PowerShell in 5 minutes]: #getstart
[Prerequisites for using Azure PowerShell with Azure Storage]: #pre
[How toomanage storage accounts in Azure]: #manageaccount
[How tooset a default Azure subscription]: #setdefsub
[How toocreate a new Azure storage account]: #createaccount
[How tooset a default Azure storage account]: #defaultaccount
[How toolist all Azure storage accounts in a subscription]: #listaccounts
[How toocreate an Azure storage context]: #createctx
[How toomanage Azure blobs and blob snapshots]: #manageblobs
[How toocreate a container]: #container
[How tooupload a blob into a container]: #uploadblob
[How toodownload blobs from a container]: #downblob
[How toocopy blobs from one storage container tooanother]: #copyblob
[How toodelete a blob]: #deleteblob
[How toomanage Azure blob snapshots]: #manageshots
[How toocreate a blob snapshot]: #createshot
[How toolist snapshots of a blob]: #listshot
[How toocopy a snapshot of a blob]: #copyshot
[How toomanage Azure tables and table entities]: #managetables
[How toocreate a table]: #createtable
[How tooretrieve a table]: #gettable
[How toodelete a table]: #remtable
[How toomanage table entities]: #mngentity
[How tooadd table entities]: #addentity
[How tooquery table entities]: #queryentity
[How toodelete table entities]: #deleteentity
[How toomanage Azure queues and queue messages]: #managequeues
[How toocreate a queue]: #createqueue
[How tooretrieve a queue]: #getqueue
[How toodelete a queue]: #remqueue
[How toomanage queue messages]: #mngqueuemsg
[How tooinsert a message into a queue]: #addqueuemsg
[How toode-queue at hello next message]: #dequeuemsg
[How toomanage Azure file shares and files]: #files
[How tooset and query storage analytics]: #stganalytics
[How toomanage Shared Access Signature (SAS) and Stored Access Policy]: #sas
[How toouse Azure Storage for U.S. government and Azure China]: #gov
[Next Steps]: #next
