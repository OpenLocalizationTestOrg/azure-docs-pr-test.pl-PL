---
title: "Używanie programu Azure PowerShell z usługą Azure Storage | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć i zarządzać kontami magazynu; przy użyciu poleceń cmdlet programu Azure PowerShell dla usługi Azure Storage Praca z obiektów blob, tabel, kolejek i plików. Konfigurowanie i zapytania analityka magazynu, a następnie utwórz sygnatur dostępu współdzielonego."
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
ms.openlocfilehash: 51e3e93ebedd31370857e61a00139294bcee9237
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-powershell-with-azure-storage"></a>Używanie programu Azure PowerShell z usługą Azure Storage
## <a name="overview"></a>Omówienie
Program Azure PowerShell jest moduł, który udostępnia polecenia cmdlet do zarządzania za pomocą środowiska Windows PowerShell. Jest to język skryptów i powłoka wiersza polecenia oparta na zadaniach zaprojektowana pod kątem administrowania systemem. Przy użyciu programu PowerShell można łatwo kontrolować i automatyzować administrowanie Azure usługi i aplikacje. Na przykład służy poleceń cmdlet do wykonania tych samych czynności, które można wykonywać za pomocą [portalu Azure](https://portal.azure.com).

W tym przewodniku, możemy Eksploruj sposób użycia [polecenia cmdlet usługi Azure Storage](/powershell/module/azurerm.storage/#storage) do wykonywania różnych zadań programowania i administracji z usługą Azure Storage.

W tym przewodniku założono, że przy użyciu doświadczenie [usługi Azure Storage](https://azure.microsoft.com/documentation/services/storage/) i [programu Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx). Przewodnik udostępnia wiele skryptów do zaprezentowania użycia programu PowerShell z usługą Azure Storage. Należy zaktualizować zmienne skryptu na podstawie konfiguracji przed uruchomieniem każdego skryptu.

Pierwsza sekcja, w tym przewodniku zapewnia szybkiego dostępu w usłudze Azure Storage i programu PowerShell. Aby uzyskać szczegółowe informacje i instrukcje, Rozpocznij od [wymagań wstępnych dotyczących używania programu Azure PowerShell z usługą Azure Storage](#prerequisites-for-using-azure-powershell-with-azure-storage).

## <a name="getting-started-with-azure-storage-and-powershell-in-5-minutes"></a>Wprowadzenie do korzystania z usługi Azure Storage i programu PowerShell w ciągu 5 minut
W tej sekcji przedstawiono sposób uzyskać dostępu do usługi Azure Storage za pomocą programu PowerShell w ciągu 5 minut.

**Jesteś nowym użytkownikiem usługi Azure:** subskrypcji Microsoft Azure i konta Microsoft skojarzonego z jego subskrypcją. Aby uzyskać informacje na temat opcji zakupu platformy Azure, zobacz [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/), [opcjami zakupu](https://azure.microsoft.com/pricing/purchase-options/), i [oferty Członkowskie](https://azure.microsoft.com/pricing/member-offers/) (dla członków MSDN, Microsoft Partner Network, BizSpark i innych programów firmy Microsoft).

Zobacz [przypisywanie ról administratorów w usłudze Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) uzyskać więcej informacji o subskrypcji platformy Azure.

**Po utworzeniu subskrypcji Microsoft Azure i konto:**

1. Pobierz i zainstaluj najnowszą [programu Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest).
2. Start środowisko systemu Windows PowerShell zintegrowane skryptów (ISE): W komputerze lokalnym, przejdź do **Start** menu. Typ **narzędzia administracyjne** i kliknij go uruchomić. W **narzędzia administracyjne** okna, kliknij prawym przyciskiem myszy **programu Windows PowerShell ISE**, kliknij przycisk **Uruchom jako Administrator**.
3. W **programu Windows PowerShell ISE**, kliknij przycisk **pliku** > **nowy** Aby utworzyć nowy plik skryptu.
4. Teraz przedstawimy prostego skryptu, który pokazuje podstawowych poleceń programu PowerShell dostęp do magazynu Azure. Skrypt najpierw poprosi Azure poświadczenia konta, aby dodać Azure konta lokalnego środowiska PowerShell. Następnie skrypt ustawiania domyślnych subskrypcji platformy Azure i Utwórz nowe konto magazynu na platformie Azure. Następnie skrypt utworzyć nowy kontener w tym nowe konto magazynu i przekazać istniejący plik obrazu (blob) do tego kontenera. Po skrypt znajduje się lista wszystkich obiektów blob w tym kontenerze, utworzy nowy katalog docelowy w komputerze lokalnym i pobranie pliku obrazu.
5. W poniższej sekcji kodu, wybierz skrypt między uwagi **#begin** i **#end**. Naciśnij klawisze CTRL + C, aby skopiować go do Schowka.

    ```powershell
    # begin
    # Update with the name of your subscription.
    $SubscriptionName = "YourSubscriptionName"
       
    # Give a name to your new storage account. It must be lowercase!
    $StorageAccountName = "yourstorageaccountname"
       
    # Choose "West US" as an example.
    $Location = "West US"
       
    # Give a name to your new container.
    $ContainerName = "imagecontainer"
       
    # Have an image file and a source directory in your local computer.
    $ImageToUpload = "C:\Images\HelloWorld.png"
       
    # A destination directory in your local computer.
    $DestinationFolder = "C:\DownloadImages"
       
    # Add your Azure account to the local PowerShell environment.
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
       
    # Download blobs from the container:
    # Get a reference to a list of all blobs in a container.
    $blobs = Get-AzureStorageBlob -Container $ContainerName
       
    # Create the destination directory.
    New-Item -Path $DestinationFolder -ItemType Directory -Force  
       
    # Download blobs into the local destination directory.
    $blobs | Get-AzureStorageBlobContent –Destination $DestinationFolder
       
    # end
    ```

6. W **programu Windows PowerShell ISE**, naciśnij klawisze CTRL + V, aby skopiować skrypt. Kliknij przycisk **pliku** > **zapisać**. W **Zapisz jako** oknie dialogowym wpisz nazwę pliku skryptu, takie jak "mystoragescript." Kliknij pozycję **Zapisz**.
7. Teraz musisz zaktualizować zmienne skryptu na podstawie własnych ustawień konfiguracji. Należy zaktualizować **$SubscriptionName** zmiennej przy użyciu posiadanej subskrypcji. Można zachować zmienne określone w skrypcie lub zaktualizuj je zgodnie z wymaganiami.
   
   * **$SubscriptionName:** należy zaktualizować tę zmienną z własną nazwę subskrypcji. Wykonaj jedną z następujących trzech sposobów, aby zlokalizować nazwę Twojej subskrypcji:
     
    a. W **programu Windows PowerShell ISE**, kliknij przycisk **pliku** > **nowy** Aby utworzyć nowy plik skryptu. Skopiuj poniższy skrypt do nowego pliku skryptu, a następnie kliknij przycisk **debugowania** > **Uruchom**. Poniższy skrypt najpierw poprosi Azure poświadczenia konta, aby dodać Azure konta lokalnego środowiska PowerShell, a następnie wyświetlić wszystkie subskrypcje, które są podłączone do lokalnej sesji programu PowerShell. Zanotuj nazwę subskrypcji, która ma być używany podczas korzystania z tego samouczka:
     
    ```powershell
    Add-AzureAccount 
      Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName
    ```

    b. Aby znaleźć i skopiować nazwę subskrypcji w [portalu Azure](https://portal.azure.com), w menu centralnym po lewej stronie kliknij **subskrypcje**. Skopiuj nazwę subskrypcji, która ma być używany podczas uruchamiania skryptów w tym przewodniku.
     
     ![Azure Portal](./media/storage-powershell-guide-full/Subscription_Previewportal.png)

    c. Aby znaleźć i skopiować nazwę subskrypcji w [klasycznego portalu Azure](https://manage.windowsazure.com/), przewiń w dół i kliknij przycisk **ustawienia** po lewej stronie portalu. Kliknij przycisk **subskrypcje** umożliwia wyświetlenie listy subskrypcji. Skopiuj nazwę subskrypcji, która ma być używany podczas uruchamiania skryptów podane w tym przewodniku.
     
     ![klasyczny portal Azure](./media/storage-powershell-guide-full/Subscription_currentportal.png)

   * **$StorageAccountName:** użyć nazwy podanej w skrypcie lub wprowadź nową nazwę dla konta magazynu. **Ważne:** nazwę konta magazynu musi być unikatowa na platformie Azure. Musi być pisane małymi literami, zbyt!
   * **$Location:** Użyj danego "zachodnie stany USA" w skrypcie lub wybierz inne lokalizacje Azure, takich jak wschodnie stany USA, Europa Północna, Europa i tak dalej.
   * **$ContainerName:** użyć nazwy podanej w skrypcie lub wprowadź nową nazwę dla Twojego kontenera.
   * **$ImageToUpload:** wprowadź ścieżkę do obrazu na komputerze lokalnym, takich jak: "C:\Images\HelloWorld.png".
   * **$DestinationFolder:** wprowadź ścieżkę do katalogu lokalnego do przechowywania pliki pobierane z usługi Azure Storage, takich jak: "C:\DownloadImages".
8. Po zaktualizowaniu zmienne skryptu w pliku "mystoragescript.ps1", kliknij przycisk **pliku** > **zapisać**. Następnie kliknij przycisk **debugowania** > **Uruchom** lub naciśnij klawisz **F5** do uruchomienia skryptu.  

Po uruchomieniu skryptu, ma lokalne miejsce docelowe folder, który zawiera plik pobrany obraz. Poniższy zrzut ekranu przedstawia przykład danych wyjściowych:

![Pobieranie obiektów blob](./media/storage-powershell-guide-full/Blobdownload.png)

> [!NOTE]
> W sekcji "Wprowadzenie do magazynu Azure i programu PowerShell w ciągu 5 minut" zapewnić szybkie wprowadzenie dotyczące sposobu używania programu Azure PowerShell z usługą Azure Storage. Aby uzyskać szczegółowe informacje i instrukcje, firma Microsoft zachęca do odczytu w poniższych sekcjach.
> 

## <a name="prerequisites-for-using-azure-powershell-with-azure-storage"></a>Wymagania wstępne dotyczące korzystania z programu Azure PowerShell z usługą Azure Storage
Potrzebujesz subskrypcji platformy Azure i konta, aby uruchomić polecenia cmdlet programu PowerShell podane w tym przewodniku, jak opisano powyżej.

Program Azure PowerShell jest moduł, który udostępnia polecenia cmdlet do zarządzania za pomocą środowiska Windows PowerShell. Aby uzyskać informacje na temat instalowania i konfigurowania programu Azure PowerShell, zobacz [jak instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview). Zaleca się pobrać i zainstalować lub uaktualnić moduł Azure PowerShell najnowsze przed rozpoczęciem korzystania z tego przewodnika.

Można uruchomić polecenia cmdlet w konsoli środowiska Windows PowerShell standard lub Windows PowerShell Integrated Scripting Environment (ISE). Na przykład, aby otworzyć **programu Windows PowerShell ISE**, przejdź do Start menu, wpisz narzędzia administracyjne i kliknij, aby go uruchomić. W oknie Narzędzia administracyjne kliknij prawym przyciskiem myszy program Windows PowerShell ISE, kliknij polecenie Uruchom jako Administrator.

## <a name="how-to-manage-storage-accounts-in-azure"></a>Jak zarządzać kontami magazynu na platformie Azure

Spójrzmy na zarządzanie kontami magazynu na platformie Azure przy użyciu programu PowerShell

### <a name="how-to-set-a-default-azure-subscription"></a>Jak ustawić domyślnego subskrypcji platformy Azure
Aby zarządzać magazynem Azure przy użyciu programu Azure PowerShell, należy uwierzytelnić środowiskiem klienta na platformie Azure przy użyciu uwierzytelniania usługi Azure Active Directory lub uwierzytelniania opartego na certyfikatach. Aby uzyskać szczegółowe informacje, zobacz [jak instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) samouczka. W tym przewodniku korzysta z uwierzytelniania usługi Azure Active Directory.

1. W środowisku Windows PowerShell ISE, wpisz następujące polecenie, aby dodać Azure konta lokalnego środowiska PowerShell:

    ```powershell
    Add-AzureAccount
    ```

2. W oknie "Logowania w celu Microsoft Azure" wpisz adres e-mail i hasło skojarzone z Twoim kontem. Nastąpi uwierzytelnienie i zapisanie informacji o poświadczeniach na platformie Azure, a następnie zamknięcie okna.

3. Następnie uruchom następujące polecenie, aby wyświetlić konta platformy Azure w lokalnym środowisku PowerShell i sprawdź, czy Twoje konto jest wyświetlane:
   
    ```powershell
    Get-AzureAccount
    ```
4. Następnie uruchom następujące polecenie cmdlet, aby wyświetlić wszystkie subskrypcje, które są podłączone do lokalnej sesji programu PowerShell i sprawdź, czy subskrypcja jest wyświetlane:

    ```powershell
    Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName`
    ```
5. Aby ustawić domyślnego subskrypcji platformy Azure, uruchom polecenie cmdlet AzureSubscription wybierz:

    ```powershell
    $SubscriptionName = 'Your subscription Name'
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
    ```

6. Sprawdź nazwę subskrypcji domyślne przy użyciu polecenia cmdlet Get-AzureSubscription:

    ```powershell
    Get-AzureSubscription -Default
    ```

7. Aby wyświetlić wszystkie dostępne polecenia cmdlet programu PowerShell dla usługi Azure Storage, uruchom polecenie:
    
    ```powershell
    Get-Command -Module Azure -Noun *Storage*`
    ```

### <a name="how-to-create-a-new-azure-storage-account"></a>Jak utworzyć nowe konto magazynu Azure
Aby korzystać z magazynu Azure, konieczne będzie konto magazynu. Po skonfigurowaniu komputera do nawiązania połączenia subskrypcji, można utworzyć nowe konto magazynu Azure.

1. Uruchom polecenie cmdlet Get-AzureLocation do znajdowania lokalizacji datacenter dostępne:

    ```powershell
    Get-AzureLocation | Format-Table -Property Name, AvailableServices, StorageAccountTypes
    ```

2. Następnie uruchom polecenie cmdlet New-AzureStorageAccount Aby utworzyć nowe konto magazynu. Poniższy przykład tworzy nowe konto magazynu w centrum danych "Zachodnie stany USA".
   
    ```powershell
    $location = "West US"
    $StorageAccountName = "yourstorageaccount"
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $location
    ```

> [!IMPORTANT]
> Nazwa konta magazynu musi być unikatowa w obrębie platformy Azure i muszą być małymi literami. Ograniczenia i konwencje nazewnictwa, zobacz [o kontach magazynu Azure](storage-create-storage-account.md) i [nazewnictwa i odwołuje się do kontenerów, obiektów blob i metadanych](http://msdn.microsoft.com/library/azure/dd135715.aspx).
> 
> 

### <a name="how-to-set-a-default-azure-storage-account"></a>Jak ustawić domyślnego konta magazynu platformy Azure
Może mieć wielu kont magazynu w ramach subskrypcji. Można wybrać jedną z nich i ustawić go jako domyślne konto magazynu dla wszystkich poleceń magazynu w tej samej sesji programu PowerShell. Umożliwia to uruchamianie poleceń programu Azure PowerShell magazynu bez jawne określenie kontekst magazynu.

1. Aby skonfigurować domyślne konto magazynu dla Twojej subskrypcji, można uruchomić polecenie cmdlet Set-AzureSubscription.

    ```powershell
    $SubscriptionName = "Your subscription name"
    $StorageAccountName = "yourstorageaccount"  
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
    ```

2. Następnie uruchom polecenie cmdlet Get-AzureSubscription, aby sprawdzić, czy konto magazynu jest skojarzony z domyślnego konta subskrypcji. To polecenie zwraca właściwości subskrypcji w bieżącej subskrypcji, w tym konta magazynu.

    ```powershell
    Get-AzureSubscription –Current
    ```

### <a name="how-to-list-all-azure-storage-accounts-in-a-subscription"></a>Jak wyświetlić wszystkie konta magazynu Azure w ramach subskrypcji
Każda subskrypcja platformy Azure może mieć maksymalnie 100 kont magazynu. Aby uzyskać najbardziej aktualne informacje dotyczące limity, zobacz [subskrypcji platformy Azure i ograniczenia usługi, przydziały i ograniczenia](../azure-subscription-service-limits.md).

Uruchom następujące polecenie cmdlet, aby znaleźć nazwę i stanu kont magazynu w bieżącej subskrypcji:

```powershell
Get-AzureStorageAccount | Format-Table -Property StorageAccountName, Location, AccountType, StorageAccountStatus
```

### <a name="how-to-create-an-azure-storage-context"></a>Jak utworzyć kontekst magazynu Azure
Kontekst magazynu platformy Azure jest obiektu w programie PowerShell, aby hermetyzować poświadczeń magazynu. Przy użyciu kontekst magazynu podczas uruchamiania wszystkie kolejne polecenia cmdlet umożliwia uwierzytelnić żądania bez jawne określenie konta magazynu i klucza dostępu. Kontekst magazynu można utworzyć na wiele sposobów, na przykład za pomocą magazynu konta nazwy i klucza dostępu, token sygnatury dostępu Współdzielonego dostępu współdzielonego, parametry połączenia lub anonimowych. Aby uzyskać więcej informacji, zobacz [AzureStorageContext nowy](/powershell/module/azure.storage/new-azurestoragecontext).  

Użyj jednej z następujących trzech sposobów, aby utworzyć kontekst magazynu:

* Uruchom [Get-AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) polecenia cmdlet, aby dowiedzieć się, podstawowy klucz dostępu dla konta magazynu Azure. Następnie wywołaj [AzureStorageContext nowy](/powershell/module/azure.storage/new-azurestoragecontext) polecenia cmdlet można utworzyć kontekstu magazynu:

    ```powershell
    $StorageAccountName = "yourstorageaccount"
    $StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
    $Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
    ```

* Generowanie tokenu sygnatury dostępu współdzielonego dla kontenera magazynu systemu Azure i przy jego użyciu można utworzyć kontekstu magazynu:

    ```powershell
    $sasToken = New-AzureStorageContainerSASToken -Container abc -Permission rl
    $Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -SasToken $sasToken
    ```

    Aby uzyskać więcej informacji, zobacz [AzureStorageContainerSASToken nowy](/powershell/module/azure.storage/new-azurestoragecontainersastoken) i [przy użyciu dostępu sygnatur dostępu Współdzielonego](storage-dotnet-shared-access-signature-part-1.md).

* W niektórych przypadkach możesz określić punktów końcowych usługi podczas tworzenia nowego kontekst magazynu. Może to być konieczne, gdy niestandardowej nazwy domeny dla konta magazynu zostały zarejestrowane w usłudze obiektów Blob lub chcesz używać do uzyskiwania dostępu do zasobów magazynu sygnatury dostępu współdzielonego. W parametrach połączenia ustawiono punktów końcowych usługi i go użyć do utworzenia nowego kontekst magazynu, jak pokazano poniżej:

    ```powershell
    $ConnectionString = "DefaultEndpointsProtocol=http;BlobEndpoint=<blobEndpoint>;QueueEndpoint=<QueueEndpoint>;TableEndpoint=<TableEndpoint>;AccountName=<AccountName>;AccountKey=<AccountKey>"
    $Ctx = New-AzureStorageContext -ConnectionString $ConnectionString
    ```

Aby uzyskać więcej informacji na temat konfigurowania parametrów połączenia magazynu, zobacz [Konfigurowanie parametrów połączenia](storage-configure-connection-string.md).

Teraz, skonfiguruj komputer i przedstawiono sposób zarządzać subskrypcjami i konta magazynu przy użyciu programu Azure PowerShell, przejdź do następnej sekcji, aby dowiedzieć się, jak zarządzać obiekty BLOB platformy Azure i migawki obiektu blob.

### <a name="how-to-retrieve-and-regenerate-azure-storage-keys"></a>Jak pobrać i ponowne generowanie kluczy magazynu Azure
Konto magazynu Azure ma dwa klucze konta. Następujące polecenie cmdlet służy do pobierania kluczy.

```powershell
Get-AzureStorageKey -StorageAccountName "yourstorageaccount"
```

Użyj następującego polecenia cmdlet można pobrać określonego klucza. Prawidłowe wartości to podstawowe i pomocnicze.  

```powershell
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Primary
    
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Secondary
```

Jeśli chcesz ponownie wygenerować klucze, użyj następującego polecenia cmdlet. Prawidłowe wartości właściwości KeyType - to "Primary" i "Secondary"

```powershell
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Primary"
    
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Secondary"
```

## <a name="how-to-manage-azure-blobs"></a>Jak zarządzać obiekty BLOB platformy Azure
Magazyn obiektów Blob Azure to usługa do przechowywania dużych ilości danych bez struktury, takich jak dane tekstowe lub binarne, którego mogą uzyskać dostęp z dowolnego miejsca na świecie za pośrednictwem protokołu HTTP lub HTTPS. W tej sekcji założono, że znasz już pojęcia dotyczące usługi magazynu obiektów Blob Azure. Aby uzyskać szczegółowe informacje, zobacz [Rozpoczynanie pracy z magazynem obiektów Blob przy użyciu platformy .NET](storage-dotnet-how-to-use-blobs.md) i [pojęcia dotyczące usługi Blob](http://msdn.microsoft.com/library/azure/dd179376.aspx).

### <a name="how-to-create-a-container"></a>Jak utworzyć kontener
Każdy obiekt blob w magazynie Azure musi być w kontenerze. Można utworzyć kontener prywatnego za pomocą polecenia cmdlet New-AzureStorageContainer:

```powershell
$StorageContainerName = "yourcontainername"
New-AzureStorageContainer -Name $StorageContainerName -Permission Off
```

> [!NOTE]
> Istnieją trzy poziomy anonimowy dostęp do odczytu: **poza**, **obiektu Blob**, i **kontenera**. Aby uniemożliwić dostęp anonimowy do obiektów blob, ustaw dla parametru uprawnienia **poza**. Domyślnie nowy kontener jest prywatny i jest możliwy tylko przez właściciela konta. Umożliwia anonimowego publiczny dostęp do odczytu do zasobów obiektów blob, ale nie do metadanych kontenera lub listę obiektów blob w kontenerze, ustaw uprawnienia dla parametru **obiektu Blob**. Umożliwia pełną publiczny dostęp do odczytu do zasobów, metadanych kontenera i listę obiektów blob w kontenerze obiektu blob, ustaw dla parametru uprawnienia **kontenera**. Aby uzyskać więcej informacji, zobacz [Zarządzanie anonimowy dostęp do odczytu do kontenerów i obiektów blob](storage-manage-access-to-resources.md).
> 
> 

### <a name="how-to-upload-a-blob-into-a-container"></a>Jak przekazać obiekt blob do kontenera
Azure Blob Storage obsługuje blokowe i stronicowe obiekty blob. Aby uzyskać więcej informacji, zobacz [opis blokowych obiektów blob, Dołącz obiektów blob i stronicowe obiekty BLOB](http://msdn.microsoft.com/library/azure/ee691964.aspx).

Aby przekazać obiektów blob w kontenerze, można użyć [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) polecenia cmdlet. Domyślnie to polecenie operacji przekazywania plików lokalnych do blokowego obiektu blob. Aby określić typ obiektu blob, można użyć parametru - BlobType.

W poniższym przykładzie uruchamiane [Get-ChildItem](http://technet.microsoft.com/library/hh849800.aspx) polecenia cmdlet, aby pobrać wszystkie pliki w określonym folderze, a następnie przekazuje je do następnego polecenia cmdlet, za pomocą operatora potoku. [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) polecenia cmdlet przekazuje lokalnych plików z kontenera:

```powershell
Get-ChildItem –Path C:\Images\* | Set-AzureStorageBlobContent -Container "yourcontainername"
```

### <a name="how-to-download-blobs-from-a-container"></a>Jak pobrać obiekty BLOB z kontenera
W poniższym przykładzie pokazano, jak pobrać obiekty BLOB z kontenera. Przykład najpierw nawiąże połączenie z magazynem Azure przy użyciu kontekstu konta magazynu, w tym nazwę konta magazynu i jego podstawowy klucz dostępu. Następnie pobiera odwołanie obiektu blob przy użyciu przykładzie [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) polecenia cmdlet. Następnie w przykładzie użyto [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) polecenia cmdlet, aby pobierać obiekty BLOB do folderu docelowego lokalnego.

```powershell
#Define the variables.
$ContainerName = "yourcontainername"
$DestinationFolder = "C:\DownloadImages"

#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#List all blobs in a container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Download blobs from a container.
New-Item -Path $DestinationFolder -ItemType Directory -Force
$blobs | Get-AzureStorageBlobContent -Destination $DestinationFolder -Context $Ctx
```

### <a name="how-to-copy-blobs-from-one-storage-container-to-another"></a>Kopiowanie obiektów blob z jeden kontener magazynu do innego
Asynchronicznie należy skopiować obiekty BLOB na kontach magazynu i regionów. W poniższym przykładzie pokazano sposób kopiowania obiektów blob z jeden kontener magazynu do innego w dwóch różnych kont magazynu. Przykład najpierw ustawia zmienne dla konta magazynu źródłowego i docelowego, a następnie tworzy kontekst magazynu dla poszczególnych kont. Następnie przykładowy kod kopiuje obiekty BLOB w kontenerze źródła do kontenera docelowego przy użyciu [Start AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) polecenia cmdlet. W przykładzie założono, że konta magazynu źródłowego i docelowego i kontenerów już istnieje.

```powershell
#Define the source storage account and context.
$SourceStorageAccountName = "yoursourcestorageaccount"
$SourceStorageAccountKey = "Storage key for yoursourcestorageaccount"
$SrcContainerName = "yoursrccontainername"
$SourceContext = New-AzureStorageContext -StorageAccountName $SourceStorageAccountName -StorageAccountKey $SourceStorageAccountKey

#Define the destination storage account and context.
$DestStorageAccountName = "yourdeststorageaccount"
$DestStorageAccountKey = "Storage key for yourdeststorageaccount"
$DestContainerName = "destcontainername"
$DestContext = New-AzureStorageContext -StorageAccountName $DestStorageAccountName -StorageAccountKey $DestStorageAccountKey

#Get a reference to blobs in the source container.
$blobs = Get-AzureStorageBlob -Container $SrcContainerName -Context $SourceContext

#Copy blobs from one container to another.
$blobs| Start-AzureStorageBlobCopy -DestContainer $DestContainerName -DestContext $DestContext
```

Należy pamiętać, że w tym przykładzie wykonuje asynchroniczne kopiowania. Można monitorować stan poszczególnych kopii uruchamiając [Get-AzureStorageBlobCopyState](/powershell/module/azure.storage/start-azurestorageblobcopystate) polecenia cmdlet.

### <a name="how-to-copy-blobs-from-a-secondary-location"></a>Kopiowanie obiektów blob z lokalizacji dodatkowej
Obiekty BLOB można skopiować z lokalizacji dodatkowej RA-GRS włączone konta.

```powershell
#define secondary storage context using a connection string constructed from secondary endpoints.
$SrcContext = New-AzureStorageContext -ConnectionString "DefaultEndpointsProtocol=https;AccountName=***;AccountKey=***;BlobEndpoint=http://***-secondary.blob.core.windows.net;FileEndpoint=http://***-secondary.file.core.windows.net;QueueEndpoint=http://***-secondary.queue.core.windows.net; TableEndpoint=http://***-secondary.table.core.windows.net;"
Start-AzureStorageBlobCopy –Container *** -Blob *** -Context $SrcContext –DestContainer *** -DestBlob *** -DestContext $DestContext
```

### <a name="how-to-delete-a-blob"></a>Jak usunąć obiektu blob
Aby usunąć obiekt blob, najpierw pobrać odwołanie do obiektu blob, a następnie wywołać polecenie cmdlet Remove-AzureStorageBlob na nim. Poniższy przykład powoduje usunięcie wszystkich obiektów blob w danym kontenerze. Przykład najpierw ustawia zmienne dla konta magazynu, a następnie tworzy kontekst magazynu. Następnie pobiera odwołanie obiektu blob przy użyciu przykładzie [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) polecenia cmdlet i uruchamia [AzureStorageBlob Usuń](/powershell/module/azure.storage/remove-azurestorageblob) polecenia cmdlet, aby usunąć obiekty BLOB z kontenera w magazynie Azure.

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "containername"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference to all the blobs in the container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Delete blobs in a specified container.
$blobs| Remove-AzureStorageBlob
```

## <a name="how-to-manage-azure-blob-snapshots"></a>Jak zarządzać migawki obiektu blob systemu Azure
Azure umożliwia tworzenie migawki obiektu blob. Migawka jest tylko do odczytu wersji obiektu blob, która jest wykonywana w punkcie w czasie. Po utworzeniu migawki, to można można odczytać, kopiowane, lub usunięte, ale nie został zmodyfikowany. Migawki umożliwiają tworzenie kopii zapasowej obiektu blob, pojawiającą się w chwili. Aby uzyskać więcej informacji, zobacz [tworzenia migawki obiektu Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).

### <a name="how-to-create-a-blob-snapshot"></a>Tworzenie migawki obiektu blob
Aby utworzyć snaphot obiektu blob, najpierw pobrać odwołanie do obiektu blob, a następnie wywołać `ICloudBlob.CreateSnapshot` dla niego metodę. Poniższy przykład najpierw ustawia zmienne dla konta magazynu, a następnie tworzy kontekst magazynu. Następnie pobiera odwołanie obiektu blob przy użyciu przykładzie [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) polecenia cmdlet i uruchamia [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) metodę w celu utworzenia migawki.

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "yourcontainername"
$BlobName = "yourblobname"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference to a blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $ContainerName -Blob $BlobName

#Create a snapshot of the blob.
$snap = $blob.ICloudBlob.CreateSnapshot()
```

### <a name="how-to-list-a-blobs-snapshots"></a>Sposób wyświetlania migawki obiektu blob
Można utworzyć dowolną liczbę migawek do obiektu blob. Można wyświetlić listę migawki skojarzone z z obiektu blob do śledzenia sieci bieżącej migawki. W poniższym przykładzie użyto wstępnie zdefiniowanych obiektów blob i wywołania [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) polecenia cmdlet, aby wyświetlić listę migawki tego obiektu blob.  

```powershell
#Define the blob name.
$BlobName = "yourblobname"

#List the snapshots of a blob.
Get-AzureStorageBlob –Context $Ctx -Prefix $BlobName -Container $ContainerName  | Where-Object  { $_.ICloudBlob.IsSnapshot -and $_.Name -eq $BlobName }
```

### <a name="how-to-copy-a-snapshot-of-a-blob"></a>Jak skopiować migawki obiektu blob
Możesz skopiować migawki obiektu blob do przywrócenia migawki. Aby uzyskać szczegółowe informacje i ograniczenia, zobacz [tworzenia migawki obiektu Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx). Poniższy przykład najpierw ustawia zmienne dla konta magazynu, a następnie tworzy kontekst magazynu. Następnie w przykładzie zdefiniowano zmienne nazwa kontenera i obiektów blob. Przykład pobiera odwołanie obiektu blob przy użyciu [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) polecenia cmdlet i uruchamia [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) metodę w celu utworzenia migawki. Następnie, w przykładzie uruchamiane są [Start AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) polecenia cmdlet można skopiować migawki obiektu blob przy użyciu obiektu ICloudBlob dla źródłowego obiektu blob. Należy zaktualizować zmienne na podstawie konfiguracji przed uruchomieniem w przykładzie. Należy pamiętać, że w poniższym przykładzie założono, że źródłowy i docelowy kontenery i źródłowego obiektu blob już istnieje.

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Define the variables.
$SrcContainerName = "yoursourcecontainername"
$DestContainerName = "yourdestcontainername"
$SrcBlobName = "yourblobname"
$DestBlobName = "CopyBlobName"

#Get a reference to a blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $SrcContainerName -Blob $SrcBlobName

#Create a snapshot of a blob.
$snap = $blob.ICloudBlob.CreateSnapshot()

#Copy the snapshot to another container.
Start-AzureStorageBlobCopy –Context $Ctx -ICloudBlob $snap -DestBlob $DestBlobName -DestContainer $DestContainerName
```

Teraz, kiedy znasz sposobu zarządzania obiekty BLOB platformy Azure i obiektów blob migawki przy użyciu programu Azure PowerShell, przejdź do następnej sekcji, aby dowiedzieć się, jak zarządzać tabel, kolejek i plików.

## <a name="how-to-manage-azure-tables-and-table-entities"></a>Jak zarządzać tabelach platformy Azure i jednostek tabeli
Azure usługi Magazyn tabel jest magazynem danych NoSQL, która służy do przechowywania i zapytań dotyczących dużych zestawów strukturalnych danych nierelacyjnych. Główne składniki usługi są tabele, jednostki i właściwości. Tabela jest kolekcji jednostek. Jednostka jest zbiór właściwości. Każdy obiekt może mieć maksymalnie 252 właściwości, które są wszystkie pary nazwa wartość. W tej sekcji założono, że znasz już pojęcia dotyczące usługi Magazyn tabel Azure. Aby uzyskać szczegółowe informacje, zobacz [opis modelu danych usługi tabel](http://msdn.microsoft.com/library/azure/dd179338.aspx) i [Rozpoczynanie pracy z magazynem tabel Azure przy użyciu platformy .NET](storage-dotnet-how-to-use-tables.md).

W poniższych podsekcjach dowiesz się, jak zarządzać usługą magazynu tabel Azure przy użyciu programu Azure PowerShell. Omówione scenariusze obejmują **tworzenie**, **usuwanie**, i **pobierania** **tabel**, jak również **Dodawanie**, **badania**, i **usuwania jednostek tabeli**.

### <a name="how-to-create-a-table"></a>Tworzenie tabeli
Każda tabela musi znajdować się na koncie magazynu platformy Azure. Poniższy przykład przedstawia sposób tworzenia tabeli w usłudze Azure Storage. Przykład najpierw nawiąże połączenie z usługi Azure Storage przy użyciu kontekstu konta magazynu, która zawiera nazwę konta magazynu i klucza dostępu. Następnie używa [AzureStorageTable nowy](/powershell/module/azure.storage/new-azurestoragetable) polecenia cmdlet, aby utworzyć tabelę w usłudze Azure Storage.

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey

#Create a new table.
$tabName = "yourtablename"
New-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-to-retrieve-a-table"></a>Jak pobrać tabeli
Można zbadać i pobrać jednego lub wszystkich tabel na koncie magazynu. W poniższym przykładzie pokazano, jak pobrać danej tabeli za pomocą [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) polecenia cmdlet.

```powershell
#Retrieve a table.
$tabName = "yourtablename"
Get-AzureStorageTable –Name $tabName –Context $Ctx
```

Wywołanie polecenia cmdlet Get-AzureStorageTable bez żadnych parametrów, pobiera wszystkie tabele magazynu dla konta magazynu.

### <a name="how-to-delete-a-table"></a>Sposób usuwania tabeli
Z konta magazynu można usunąć tabeli, za pomocą [AzureStorageTable Usuń](/powershell/module/azure.storage/remove-azurestoragetable) polecenia cmdlet.  

```powershell
#Delete a table.
$tabName = "yourtablename"
Remove-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-to-manage-table-entities"></a>Jak zarządzać jednostek tabeli
Obecnie programu Azure PowerShell nie udostępnia polecenia cmdlet do zarządzania jednostek tabeli bezpośrednio. Aby wykonywać operacje na jednostkach tabeli, można użyć klasy podane w [biblioteki klienta magazynu Azure dla platformy .NET](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).

#### <a name="how-to-add-table-entities"></a>Jak dodać jednostek tabeli
Aby dodać jednostkę do tabeli, należy najpierw utworzyć obiekt, który definiuje właściwości jednostki. Jednostka może mieć maksymalnie 255 właściwości, w tym 3 Właściwości systemowe: **PartitionKey**, **RowKey**, i **sygnatury czasowej**. Jest odpowiedzialny za wstawiania i aktualizowania wartości **PartitionKey** i **RowKey**. Serwer zarządza wartością **sygnatury czasowej**, która nie może być modyfikowany. Razem **PartitionKey** i **RowKey** jednoznacznie zidentyfikować każdej jednostki w tabeli.

* **PartitionKey**: Określa jednostki przechowywanego w partycji.
* **RowKey**: unikatowo identyfikuje jednostek w partycji.

Można zdefiniować maksymalnie 252 właściwości niestandardowych dla jednostki. Aby uzyskać więcej informacji, zobacz [opis modelu danych usługi tabel](http://msdn.microsoft.com/library/azure/dd179338.aspx).

W poniższym przykładzie pokazano, jak dodać jednostek do tabeli. W przykładzie przedstawiono sposób pobierania tabeli pracowników i Dodaj do niej kilku jednostek. Najpierw nawiązaniem połączenia z magazynem Azure przy użyciu kontekstu konta magazynu, która zawiera nazwę konta magazynu i klucza dostępu. Następnie pobiera przy użyciu danej tabeli [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) polecenia cmdlet. Jeśli tabela nie istnieje, [AzureStorageTable nowy](/powershell/module/azure.storage/new-azurestoragetable) polecenia cmdlet służy do tworzenia tabeli w usłudze Azure Storage. Następnie w przykładzie zdefiniowano niestandardowe funkcji Dodaj jednostki do Dodaj jednostki do tabeli, określając każdej jednostki partycji i klucz wiersza. Wywołania funkcji jednostki Dodaj [New-Object](http://technet.microsoft.com/library/hh849885.aspx) polecenia cmdlet na [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) klasy w celu utworzenia obiektu jednostki. Później, przykład wywołuje [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) metody dla tego obiektu jednostki, aby dodać go do tabeli.

```powershell
#Function Add-Entity: Adds an employee entity to a table.
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

#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Retrieve the table if it already exists.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx -ErrorAction Ignore

#Create a new table if it does not exist.
if ($table -eq $null)
{
   $table = New-AzureStorageTable –Name $TableName -Context $Ctx
}

#Add multiple entities to a table.
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row1 -Name Chris -Id 1
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row2 -Name Jessie -Id 2
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row1 -Name Christine -Id 3
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row2 -Name Steven -Id 4
```

#### <a name="how-to-query-table-entities"></a>Jak wykonać zapytanie dotyczące jednostek tabeli
Aby sprawdzić tabelę, użyj [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) klasy. W poniższym przykładzie założono, zostały już uruchomiono skrypt podanych w sposobu, w jaki można dodać jednostki części tego przewodnika. Przykład najpierw nawiąże połączenie z magazynem Azure przy użyciu kontekst magazynu, który zawiera nazwę konta magazynu i klucza dostępu. Następnie próbuje pobrać za pomocą tabeli utworzonej wcześniej "pracownicy" [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) polecenia cmdlet. Wywoływanie [New-Object](http://technet.microsoft.com/library/hh849885.aspx) polecenia cmdlet w klasie Microsoft.WindowsAzure.Storage.Table.TableQuery tworzy nowy obiekt zapytania. Przykład szuka obiektów, które mają kolumnę 'ID', którego wartość wynosi 1, ponieważ określony w filtrze ciągu. Aby uzyskać szczegółowe informacje, zobacz [badania tabel i jednostek](http://msdn.microsoft.com/library/azure/dd894031.aspx). Po uruchomieniu to zapytanie zwraca wszystkich jednostek spełniających kryteria filtrowania.

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Get a reference to a table.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx

#Create a table query.
$query = New-Object Microsoft.WindowsAzure.Storage.Table.TableQuery

#Define columns to select.
$list = New-Object System.Collections.Generic.List[string]
$list.Add("RowKey")
$list.Add("ID")
$list.Add("Name")

#Set query details.
$query.FilterString = "ID gt 0"
$query.SelectColumns = $list
$query.TakeCount = 20

#Execute the query.
$entities = $table.CloudTable.ExecuteQuery($query)

#Display entity properties with the table format.
$entities  | Format-Table PartitionKey, RowKey, @{ Label = "Name"; Expression={$_.Properties["Name"].StringValue}}, @{ Label = "ID"; Expression={$_.Properties["ID"].Int32Value}} -AutoSize
```

#### <a name="how-to-delete-table-entities"></a>Sposób usuwania jednostek tabeli
Można usunąć jednostki przy użyciu jego kluczy partycji i wiersza. W poniższym przykładzie założono, zostały już uruchomiono skrypt podanych w sposobu, w jaki można dodać jednostki części tego przewodnika. Przykład najpierw nawiąże połączenie z magazynem Azure przy użyciu kontekst magazynu, który zawiera nazwę konta magazynu i klucza dostępu. Następnie próbuje pobrać za pomocą tabeli utworzonej wcześniej "pracownicy" [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) polecenia cmdlet. Jeśli tabela istnieje, [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) metody do pobierania jednostki na podstawie jego wartości klucza partycji i wiersza. Przekazuj jednostki do [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) do usunięcia.

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve the table.
$TableName = "Employees"
$table = Get-AzureStorageTable -Name $TableName -Context $Ctx -ErrorAction Ignore

#If the table exists, start deleting its entities.
if ($table -ne $null) 
{
    #Together the PartitionKey and RowKey uniquely identify every  
    #entity within a table.
    $tableResult = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Retrieve("Partition2", "Row1"))
    $entity = $tableResult.Result
    if ($entity -ne $null)
    {
        #Delete the entity.
        $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Delete($entity))
    }
}
```

## <a name="how-to-manage-azure-queues-and-queue-messages"></a>Jak zarządzać kolejek platformy Azure i wiadomości w kolejce
Azure Queue Storage to usługa do przechowywania dużej liczby komunikatów, do której można uzyskać dostęp z dowolnego miejsca na świecie za pośrednictwem uwierzytelnionego połączenia za pomocą protokołu HTTP lub HTTPS. W tej sekcji założono, że znasz już pojęcia dotyczące usługi magazynu kolejek Azure. Aby uzyskać szczegółowe informacje, zobacz [Rozpoczynanie pracy z magazynem kolejek Azure przy użyciu platformy .NET](storage-dotnet-how-to-use-queues.md).

W tej sekcji opisano sposób zarządzania usługą magazynu kolejek Azure przy użyciu programu Azure PowerShell. Omówione scenariusze obejmują **wstawianie** i **usuwanie** kolejki komunikatów, a także **tworzenie**, **usuwanie**, i **pobierania kolejek**.

### <a name="how-to-create-a-queue"></a>Tworzenie kolejki
Poniższy przykład najpierw nawiąże połączenie z usługi Azure Storage przy użyciu kontekstu konta magazynu, która zawiera nazwę konta magazynu i klucza dostępu. Następnie wywołuje [AzureStorageQueue nowy](/powershell/module/azure.storage/new-azurestoragequeue) polecenia cmdlet, aby utworzyć kolejkę o nazwie "queuename".

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$QueueName = "queuename"
$Queue = New-AzureStorageQueue –Name $QueueName -Context $Ctx
```

Aby uzyskać informacji na temat konwencji nazewnictwa dla usługi kolejek platformy Azure, zobacz [nazewnictwo kolejek i metadanych](http://msdn.microsoft.com/library/azure/dd179349.aspx).

### <a name="how-to-retrieve-a-queue"></a>Jak pobrać kolejki
Można zbadać i pobrać określonej kolejki, a także listę wszystkich kolejek na koncie magazynu. W poniższym przykładzie pokazano, jak pobrać przy użyciu określonej kolejki [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) polecenia cmdlet.

```powershell
#Retrieve a queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue –Name $QueueName –Context $Ctx
```

Jeśli należy wywołać [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) polecenia cmdlet bez parametrów, pobiera listę wszystkich kolejek.

### <a name="how-to-delete-a-queue"></a>Sposób usuwania kolejki
Aby usunąć kolejkę i wszystkie zawarte w niej komunikaty, wywołaj polecenie cmdlet Remove-AzureStorageQueue. Poniższy przykład pokazuje, jak można usunąć za pomocą polecenia cmdlet Remove-AzureStorageQueue określonej kolejki.

```powershell
#Delete a queue.
$QueueName = "yourqueuename"
Remove-AzureStorageQueue –Name $QueueName –Context $Ctx
```

#### <a name="how-to-insert-a-message-into-a-queue"></a>Jak można wstawić komunikatu do kolejki
Aby wstawić komunikat do istniejącej kolejki, najpierw utwórz nowe wystąpienie klasy [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) klasy. Następnie wywołaj metodę [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx). CloudQueueMessage można utworzyć z ciągu (w formacie UTF-8) lub tablicy bajtów.

W poniższym przykładzie pokazano, jak dodać wiadomości do kolejki. Przykład najpierw nawiąże połączenie z usługi Azure Storage przy użyciu kontekstu konta magazynu, która zawiera nazwę konta magazynu i klucza dostępu. Następnie pobiera przy użyciu określonej kolejki [Get-AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) polecenia cmdlet. Jeśli kolejka istnieje, [New-Object](http://technet.microsoft.com/library/hh849885.aspx) polecenia cmdlet służy do tworzenia wystąpienia [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) klasy. Później, przykład wywołuje [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) metody w tym obiekcie komunikat, aby dodać je do kolejki. Oto kod, który pobiera kolejki i wstawia komunikat "MessageInfo":

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve the queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

#If the queue exists, add a new message.
if ($Queue -ne $null) {
   # Create a new message using a constructor of the CloudQueueMessage class.
   $QueueMessage = New-Object -TypeName Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage -ArgumentList MessageInfo

   # Add a new message to the queue.
   $Queue.CloudQueue.AddMessage($QueueMessage)
}
```

#### <a name="how-to-de-queue-at-the-next-message"></a>Jak cofnąć kolejka kolejnego komunikatu
Twój kod usuwa komunikat z kolejki w dwóch etapach. Podczas wywoływania [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) metody, otrzymasz następnej wiadomości w kolejce. Komunikat zwrócony z funkcji **GetMessage** staje się niewidoczny dla innego kodu odczytującego komunikaty z tej kolejki. Aby zakończyć usuwanie komunikatu z kolejki, musisz również wywołać [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) metody. Ten dwuetapowy proces usuwania komunikatów gwarantuje, że jeśli kod nie będzie w stanie przetworzyć komunikatu z powodu awarii sprzętu lub oprogramowania, inne wystąpienie kodu będzie w stanie uzyskać ten sam komunikat i ponowić próbę. Twój kod wywołuje funkcję **DeleteMessage** natychmiast po przetworzeniu komunikatu.

```powershell
# Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

# Retrieve the queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

$InvisibleTimeout = [System.TimeSpan]::FromSeconds(10)

# Get the message object from the queue.
$QueueMessage = $Queue.CloudQueue.GetMessage($InvisibleTimeout)
# Delete the message.
$Queue.CloudQueue.DeleteMessage($QueueMessage)
```

## <a name="how-to-manage-azure-file-shares-and-files"></a>Jak zarządzać udziały plików platformy Azure i plików
Magazyn plików Azure oferuje współużytkowany magazyn dla aplikacji używających standardowego protokołu SMB. Maszyny wirtualne Microsoft Azure i usługi w chmurze mogą udostępniać dane między składnikami aplikacji za pośrednictwem zainstalowanych udziałów i aplikacji lokalnych mają dostęp do danych plików w udziale za pośrednictwem programu Azure PowerShell lub interfejsu API magazynu plików.

Aby uzyskać więcej informacji dotyczących usługi Magazyn plików Azure, zobacz [Rozpoczynanie pracy z magazynem plików Azure w systemie Windows](storage-dotnet-how-to-use-files.md) i [interfejsu API REST usługi plików](http://msdn.microsoft.com/library/azure/dn167006.aspx).

## <a name="how-to-set-and-query-storage-analytics"></a>Jak ustawić i analiza magazynu zapytań
Można użyć [analityka magazynu Azure](storage-analytics.md) zbieranie metryk dla kont magazynu Azure i rejestrowanie danych dotyczących żądania wysyłane na koncie magazynu. Metryki magazynu służy do monitorowania prawidłowości konta magazynu i magazynu rejestrowania do diagnozowania i rozwiązywania problemów z kontem magazynu. Istnieje możliwość skonfigurowania monitorowania przy użyciu portalu Azure lub programu Windows PowerShell, albo programowo z użyciem biblioteki klienta usługi storage. Rejestrowanie magazynu wykonywany po stronie serwera i umożliwia utworzenie rekordów szczegółów dla żądań pomyślnie i niepomyślnie na koncie magazynu. Dzienniki te umożliwiają szczegóły odczytu, zapisu i usuwania działań przed tabel, kolejek i obiektów blob, a także przyczyny żądań zakończonych niepowodzeniem.

Aby dowiedzieć się, jak włączyć i wyświetlania metryk magazynu danych przy użyciu programu PowerShell, zobacz [jak włączyć metryki magazynu przy użyciu programu PowerShell](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell).

Aby dowiedzieć się, jak włączyć i pobrać rejestrowania magazynu danych przy użyciu programu PowerShell, zobacz [jak włączyć rejestrowanie magazynu przy użyciu programu PowerShell](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) i [znajdowanie rejestrowania magazynu danych dziennika](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata).
Aby uzyskać szczegółowe informacje dotyczące rozwiązywania problemów z magazynowaniem za pomocą metryki magazynu i rejestrowanie magazynu, zobacz [monitorowanie, diagnozowanie i rozwiązywanie problemów z programem Microsoft Azure Storage](storage-monitoring-diagnosing-troubleshooting.md).

## <a name="how-to-manage-shared-access-signature-sas-and-stored-access-policy"></a>Jak zarządzać dostępu sygnatury dostępu Współdzielonego i przechowywane zasad dostępu
Sygnatury dostępu współdzielonego są ważnym elementem modelu zabezpieczeń dla dowolnej aplikacji przy użyciu usługi Azure Storage. Są one przydatne zapewniające dostęp jest ograniczony do konta magazynu do klientów, które nie powinny mieć klucz konta. Domyślnie obiekty BLOB, tabel i kolejek w ramach tego konta może uzyskiwać dostęp tylko właściciel konta magazynu. Jeśli daną usługą lub aplikacją musi udostępniać tych zasobów innym klientom bez udostępniania klucz dostępu, dostępne są trzy opcje:

* Ustaw uprawnienia kontenera, aby zezwolić na anonimowy dostęp do odczytu do kontenera i jego obiektów blob. Jest to niedozwolone dla tabel lub kolejek.
* Użyj sygnatury dostępu współdzielonego, że przyznaje ograniczone prawa dostępu do kontenerów, obiektów blob, kolejek i tabel dla określonego interwału.
* Zasady dostępu do przechowywanych umożliwia uzyskanie dodatkowy poziom kontroli nad sygnatur dostępu współdzielonego dla kontenera lub jego obiektów blob, kolejki lub tabeli. Zasady dostępu przechowywanych umożliwia zmianę godziny rozpoczęcia, czas wygaśnięcia lub uprawnienia dla podpisu lub odwołać go po nim został wystawiony.

Sygnatury dostępu współdzielonego, można w jednym z dwóch formach:

* **Ad hoc SAS**: podczas tworzenia ad hoc SAS, godzina rozpoczęcia, czas wygaśnięcia i uprawnienia dla sygnatury dostępu Współdzielonego są określone w identyfikatorze URI sygnatury dostępu Współdzielonego. Ten typ sygnatury dostępu Współdzielonego może zostać utworzony w kontenerze, obiektów blob, tabeli lub kolejki i jest z systemem innym niż odwoływalny.
* **Sygnatury dostępu Współdzielonego z zasadami dostępu do przechowywanych**: zasady dostępu do przechowywanych jest zdefiniowany w kontenerze zasobu kontenera obiektów blob, tabel lub kolejek — i służy do zarządzania ograniczeniami dla jednego lub więcej sygnatur dostępu współdzielonego. Po skojarzeniu sygnatury dostępu Współdzielonego za pomocą zasad dostępu przechowywane, sygnatury dostępu Współdzielonego dziedziczy ograniczenia — czas rozpoczęcia, czas wygaśnięcia i uprawnienia - zdefiniowane zasady dostępu przechowywane. Ten typ sygnatury dostępu Współdzielonego jest odwoływalny.

Aby uzyskać więcej informacji, zobacz [przy użyciu dostępu sygnatur dostępu Współdzielonego](storage-dotnet-shared-access-signature-part-1.md) i [Zarządzanie anonimowy dostęp do odczytu do kontenerów i obiektów blob](storage-manage-access-to-resources.md).

W kolejnych sekcjach dowiesz się, jak utworzyć zasady dostępu współdzielonego podpisu tokenu i przechowywane dostęp do tabel Azure. Program Azure PowerShell udostępnia podobne polecenia cmdlet dla kontenerów, obiektów blob i kolejek oraz. Aby uruchomić skrypty w tej sekcji, Pobierz [Azure PowerShell w wersji 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) lub nowszym.

### <a name="how-to-create-a-policy-based-shared-access-signature-token"></a>Jak utworzyć token sygnatura dostępu współdzielonego opartych na zasadach
Aby utworzyć nowe zasady dostępu do przechowywanych, należy użyć polecenia cmdlet New-AzureStorageTableStoredAccessPolicy. Następnie wywołaj metodę [AzureStorageTableSASToken nowy](/powershell/module/azure.storage/new-azurestoragetablesastoken) , aby utworzyć nowy token podpisu na podstawie zasad dostępu współdzielonego dla tabeli magazynu Azure.

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
New-AzureStorageTableSASToken -Name $tableName -Policy $policy -Context $Ctx
```

### <a name="how-to-create-an-ad-hoc-non-revocable-shared-access-signature-token"></a>Jak utworzyć token ad hoc sygnatura dostępu współdzielonego (z systemem innym niż — odwoływalny)
Użyj [AzureStorageTableSASToken nowy](/powershell/module/azure.storage/new-azurestoragetablesastoken) , aby utworzyć nowy ad hoc (z systemem innym niż — odwoływalny) Sygnatura dostępu współdzielonego token dla tabeli magazynu Azure:

```powershell
New-AzureStorageTableSASToken -Name $tableName -Permission "rqud" -StartTime "2015-01-01" -ExpiryTime "2015-02-01" -Context $Ctx
```
    
### <a name="how-to-create-a-stored-access-policy"></a>Tworzenie zasad dostępu przechowywane
Utwórz nowe zasady dostępu do przechowywanych dla tabeli usługi Azure Storage za pomocą polecenia cmdlet New-AzureStorageTableStoredAccessPolicy:

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
```
    
### <a name="how-to-update-a-stored-access-policy"></a>Jak zaktualizować zasad dostępu przechowywane
Za pomocą polecenia cmdlet Set-AzureStorageTableStoredAccessPolicy zaktualizować istniejące zasady dostępu do przechowywanych dla tabeli magazynu Azure:

```powershell
Set-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Permission "rd" -NoExpiryTime -NoStartTime -Context $Ctx
```

### <a name="how-to-delete-a-stored-access-policy"></a>Jak usunąć zasadę przechowywanych dostępu
Aby usunąć zasady dostępu przechowywane w tabeli magazynu Azure, użyj polecenia cmdlet Remove-AzureStorageTableStoredAccessPolicy:

```powershell
Remove-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Context $Ctx
```

## <a name="how-to-use-azure-storage-for-us-government-and-azure-china"></a>Jak używać magazynu Azure dla instytucji rządowych USA i Chińskiej wersji platformy Azure
Środowiska platformy Azure jest niezależnie od wdrożenia programu Microsoft Azure, takich jak [Azure dla instytucji rządowych USA administracji](https://azure.microsoft.com/features/gov/), [AzureCloud globalne Azure](https://portal.azure.com), i [AzureChinaCloud dla platformy Azure obsługiwane przez 21Vianet w Chinach](http://www.windowsazure.cn/). Można wdrażać nowe środowisk Azure dla instytucji rządowych USA i Chińskiej wersji platformy Azure.

Aby używać usługi Azure Storage z AzureChinaCloud, musisz utworzyć kontekst magazynu, który jest skojarzony z AzureChinaCloud. Wykonaj następujące kroki, które ułatwią rozpoczęcie pracy:

1. Uruchom [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) polecenia cmdlet, aby wyświetlić dostępne środowisk Azure:
   
    ```powershell
    Get-AzureEnvironment
    ```

2. Dodaj konto chińskiej wersji platformy Azure do środowiska Windows PowerShell:
   
    ```powershell
    Add-AzureAccount –Environment AzureChinaCloud
    ```

3. Tworzenie magazynu kontekstu konta AzureChinaCloud:
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureChinaCloud
    ```

Aby używać magazynu Azure z [stany USA Azure dla instytucji rządowych](https://azure.microsoft.com/features/gov/), należy zdefiniować nowe środowisko i następnie tworzy nowy kontekst magazynu z tym środowiskiem:

1. Uruchom [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) polecenia cmdlet, aby wyświetlić dostępne środowisk Azure:

    ```powershell
    Get-AzureEnvironment
    ```

2. Dodaj konto Azure instytucji rządowych Stanów Zjednoczonych do środowiska Windows PowerShell:
   
    ```powershell
    Add-AzureAccount –Environment AzureUSGovernment
    ```

3. Tworzenie magazynu kontekstu konta AzureUSGovernment:
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureUSGovernment
    ```
     
Aby uzyskać więcej informacji, zobacz:

* [Przewodnik dewelopera usługi Microsoft Azure dla instytucji rządowych](../azure-government-developer-guide.md).
* [Omówienie różnic podczas tworzenia aplikacji w usłudze Chin](https://msdn.microsoft.com/library/azure/dn578439.aspx)

## <a name="next-steps"></a>Następne kroki
W tym przewodniku kiedy znasz już sposobu zarządzania usługi Azure Storage przy użyciu programu Azure PowerShell. Poniżej przedstawiono niektóre pokrewne artykuły i zasoby dowiedzieć się więcej o nich.

* [Dokumentacja usługi Azure Storage](https://azure.microsoft.com/documentation/services/storage/)
* [Polecenia cmdlet programu PowerShell usługi Azure Storage](/powershell/module/azurerm.storage/#storage)
* [Dokumentacja programu PowerShell systemu Windows](https://msdn.microsoft.com/library/ms714469.aspx)

[Getting started with Azure Storage and PowerShell in 5 minutes]: #getstart
[Prerequisites for using Azure PowerShell with Azure Storage]: #pre
[How to manage storage accounts in Azure]: #manageaccount
[How to set a default Azure subscription]: #setdefsub
[How to create a new Azure storage account]: #createaccount
[How to set a default Azure storage account]: #defaultaccount
[How to list all Azure storage accounts in a subscription]: #listaccounts
[How to create an Azure storage context]: #createctx
[How to manage Azure blobs and blob snapshots]: #manageblobs
[How to create a container]: #container
[How to upload a blob into a container]: #uploadblob
[How to download blobs from a container]: #downblob
[How to copy blobs from one storage container to another]: #copyblob
[How to delete a blob]: #deleteblob
[How to manage Azure blob snapshots]: #manageshots
[How to create a blob snapshot]: #createshot
[How to list snapshots of a blob]: #listshot
[How to copy a snapshot of a blob]: #copyshot
[How to manage Azure tables and table entities]: #managetables
[How to create a table]: #createtable
[How to retrieve a table]: #gettable
[How to delete a table]: #remtable
[How to manage table entities]: #mngentity
[How to add table entities]: #addentity
[How to query table entities]: #queryentity
[How to delete table entities]: #deleteentity
[How to manage Azure queues and queue messages]: #managequeues
[How to create a queue]: #createqueue
[How to retrieve a queue]: #getqueue
[How to delete a queue]: #remqueue
[How to manage queue messages]: #mngqueuemsg
[How to insert a message into a queue]: #addqueuemsg
[How to de-queue at the next message]: #dequeuemsg
[How to manage Azure file shares and files]: #files
[How to set and query storage analytics]: #stganalytics
[How to manage Shared Access Signature (SAS) and Stored Access Policy]: #sas
[How to use Azure Storage for U.S. government and Azure China]: #gov
[Next Steps]: #next
