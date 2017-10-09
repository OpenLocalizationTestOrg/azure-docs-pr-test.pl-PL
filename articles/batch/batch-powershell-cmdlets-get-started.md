---
title: "aaaGet uruchomiony przy użyciu programu PowerShell dla usługi partia zadań Azure | Dokumentacja firmy Microsoft"
description: "Toohello szybkie wprowadzenie poleceń cmdlet programu Azure PowerShell, mogą wykorzystać zasoby partii toomanage."
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: f9ad62c5-27bf-4e6b-a5bf-c5f5914e6199
ms.service: batch
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: powershell
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3e4d12e9c1e52a5b2db2dd44346edda93b7ef92b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-batch-resources-with-powershell-cmdlets"></a>Zarządzanie zasobami usługi Batch za pomocą poleceń cmdlet programu PowerShell

Z hello poleceń cmdlet programu PowerShell usługi partia zadań Azure, można wykonać i wiele hello skryptu tego samego zadania wykonywane z hello API partii hello portalu Azure i hello Azure interfejsu wiersza polecenia (CLI). Jest to szybkie wprowadzenie toohello polecenia cmdlet można użyć toomanage kont usługi partia zadań i pracy z zasobami usługi partia zadań takich jak pule, zadań i zadań.

Aby uzyskać pełną listę poleceń cmdlet partii i składnię szczegółowe poleceń cmdlet Zobacz hello [dokumentacji poleceń cmdlet partii zadań Azure](/powershell/module/azurerm.batch/#batch).

Informacje w tym artykule dotyczą poleceń cmdlet programu Azure PowerShell w wersji 3.0.0. Firma Microsoft zaleca się zaktualizowanie programu Azure PowerShell często tootake zalet usługi aktualizacji i ulepszeń.

## <a name="prerequisites"></a>Wymagania wstępne
Wykonaj następujące operacje toouse programu Azure PowerShell toomanage hello zasobami partii.

* [Zainstaluj i skonfiguruj program Azure PowerShell](/powershell/azure/overview)
* Uruchom hello **Login-AzureRmAccount** polecenia cmdlet tooconnect tooyour subskrypcji (hello partii zadań Azure statku poleceń cmdlet w module usługi Azure Resource Manager hello):
  
    `Login-AzureRmAccount`
* **Zarejestruj przestrzeń nazw dostawcy partii hello**. Ta operacja wymaga tylko toobe wykonać **raz dla subskrypcji**.
  
    `Register-AzureRMResourceProvider -ProviderNamespace Microsoft.Batch`

## <a name="manage-batch-accounts-and-keys"></a>Zarządzanie kontami i kluczami usługi Batch
### <a name="create-a-batch-account"></a>Tworzenie konta usługi Batch
Polecenie **New-AzureRmBatchAccount** umożliwia utworzenie konta usługi Batch w określonej grupie zasobów. Jeśli nie masz już grupę zasobów, utwórz ją, uruchamiając hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) polecenia cmdlet. Określ jedną z hello Azure regionach hello **lokalizacji** parametrów, takich jak "Środkowe stany USA". Na przykład:

    New-AzureRmResourceGroup –Name MyBatchResourceGroup –location "Central US"

Następnie utwórz konta usługi partia zadań w grupie zasobów hello, określając nazwę konta hello w <*nazwa_konta*> i hello lokalizację i nazwę grupy zasobów. Tworzenie konta usługi partia zadań hello może zająć niektórych toocomplete czasu. Na przykład:

    New-AzureRmBatchAccount –AccountName <account_name> –Location "Central US" –ResourceGroupName <res_group_name>

> [!NOTE]
> Konto usługi partia zadań Hello nazwa musi być unikatowa toohello region platformy Azure dla grupy zasobów hello, zawierać od 3 do 24 znaków i korzystać tylko małe litery i cyfry.
> 
> 

### <a name="get-account-access-keys"></a>Pobieranie kluczy dostępu do konta
**Get-AzureRmBatchAccountKeys** zawiera klucze dostępu hello skojarzone z kontem usługi partia zadań Azure. Na przykład uruchom powitania po tooget klucze podstawowe i pomocnicze hello hello konta została utworzona.

    $Account = Get-AzureRmBatchAccountKeys –AccountName <account_name>

    $Account.PrimaryAccountKey

    $Account.SecondaryAccountKey

### <a name="generate-a-new-access-key"></a>Generowanie nowego klucza dostępu
Polecenie **New-AzureRmBatchAccountKey** umożliwia generowanie nowego klucza podstawowego lub klucza pomocniczego do konta usługi Azure Batch. Na przykład toogenerate nowego klucza podstawowego dla konta wsadowego, wpisz:

    New-AzureRmBatchAccountKey -AccountName <account_name> -KeyType Primary

> [!NOTE]
> toogenerate klucza pomocniczego, określ "Pomocniczy" hello **KeyType** parametru. Masz klucze podstawowe i pomocnicze hello tooregenerate oddzielnie.
> 
> 

### <a name="delete-a-batch-account"></a>Usuwanie konta usługi Batch
Polecenie **Remove-AzureRmBatchAccount** umożliwia usunięcie konta usługi Batch. Na przykład:

    Remove-AzureRmBatchAccount -AccountName <account_name>

Po wyświetleniu monitu Potwierdź, że chcesz tooremove hello konta. Usunięcie konta może zająć niektórych toocomplete czasu.

## <a name="create-a-batchaccountcontext-object"></a>Tworzenie obiektu BatchAccountContext
tooauthenticate przy użyciu hello poleceń cmdlet programu PowerShell partii, gdy tworzenie i Zarządzanie pulami partii, zadania, zadania i inne zasoby, najpierw utwórz toostore obiektu BatchAccountContext nazwę konta i kluczy:

    $context = Get-AzureRmBatchAccountKeys -AccountName <account_name>

Przekazujesz hello BatchAccountContext obiektu do poleceń cmdlet tego hello użyj **BatchContext** parametru.

> [!NOTE]
> Domyślnie klucza podstawowego konta hello jest używany do uwierzytelniania, ale jawnie wybrać toouse klucza hello zmieniając obiektu BatchAccountContext **KeyInUse** właściwości: `$context.KeyInUse = "Secondary"`.
> 
> 

## <a name="create-and-modify-batch-resources"></a>Tworzenie i modyfikowanie zasobów usługi Batch
Użyj polecenia cmdlet, takich jak **AzureBatchPool nowy**, **AzureBatchJob nowy**, i **AzureBatchTask nowy** toocreate zasobów w ramach konta usługi partia zadań. Istnieją odpowiadające im **Get -** i **Set -** poleceń cmdlet tooupdate hello właściwości istniejących zasobów i **Remove -** zasobów tooremove poleceń cmdlet w ramach konta usługi partia zadań.

Korzystając z wielu z tych poleceń cmdlet w toopassing dodanie obiektu BatchContext, należy toocreate lub Przekaż obiektów zawierających ustawienia szczegółowe zasobów, jak pokazano w hello poniższy przykład. Zobacz hello szczegółową pomoc dla poszczególnych poleceń cmdlet, aby uzyskać dodatkowe przykłady.

### <a name="create-a-batch-pool"></a>Tworzenie puli usługi Batch
Podczas tworzenia lub aktualizowania puli partii, wybraniu konfiguracji usługi w chmurze hello lub hello konfiguracji maszyny wirtualnej dla hello systemu operacyjnego na powitania węzły obliczeniowe (zobacz [Przegląd funkcji partii](batch-api-basics.md#pool)). Jeśli określisz konfiguracji usługi w chmurze hello węzłów obliczeniowych obraz zostanie utworzony z jednym hello [wersje systemu operacyjnego gościa Azure](../cloud-services/cloud-services-guestos-update-matrix.md#releases). Jeśli określisz hello konfiguracji maszyny wirtualnej, można określić jedną hello obsługiwane Linux lub maszyny Wirtualnej systemu Windows obrazy hello wymienionych w [Marketplace maszyny wirtualne Azure][vm_marketplace], lub podać niestandardowy obraz, który już przygotowane.

Po uruchomieniu **AzureBatchPool nowy**, przekazywanie obiektu PSCloudServiceConfiguration lub PSVirtualMachineConfiguration hello ustawień systemu operacyjnego. Na przykład hello następujące polecenie cmdlet tworzy nową pulę partii z węzłów obliczeniowych mały rozmiar w konfiguracji usługi chmury hello obrazami z najnowszą wersją systemu operacyjnego hello rodziny 3 (Windows Server 2012). W tym miejscu hello **CloudServiceConfiguration** parametr określa hello *$configuration* zmiennej jako hello PSCloudServiceConfiguration obiektu. Witaj **BatchContext** parametr określa uprzednio zdefiniowanej zmiennej *$context* jako hello BatchAccountContext obiektu.

    $configuration = New-Object -TypeName "Microsoft.Azure.Commands.Batch.Models.PSCloudServiceConfiguration" -ArgumentList @(4,"*")

    New-AzureBatchPool -Id "AutoScalePool" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -AutoScaleFormula '$TargetDedicated=4;' -BatchContext $context

Hello docelowy węzłów obliczeniowych w nowej puli hello jest określana na podstawie formuły Skalowanie automatyczne. W takim przypadku formuła hello jest po prostu **$TargetDedicated = 4**, określającą hello liczbę węzłów obliczeniowych w puli hello jest maksymalnie 4.

## <a name="query-for-pools-jobs-tasks-and-other-details"></a>Zapytania dotyczące puli, zadań, podzadań oraz innych szczegółów
Użyj polecenia cmdlet, takich jak **Get-AzureBatchPool**, **Get-AzureBatchJob**, i **Get-AzureBatchTask** tooquery dla jednostek utworzone w ramach konta usługi partia zadań.

### <a name="query-for-data"></a>Zapytania dotyczące danych
Na przykład użyć **Get-AzureBatchPools** toofind Twojego pule. Domyślnie to zapytanie dla wszystkich pul na koncie, zakładając, że możesz już przechowywane hello BatchAccountContext obiektu w *$context*:

    Get-AzureBatchPool -BatchContext $context

### <a name="use-an-odata-filter"></a>Korzystanie z filtru OData
Możesz podać filtru OData przy użyciu hello **filtru** toofind parametru tylko hello interesują Cię obiekty. Np. można znaleźć wszystkie pule z identyfikatorami zaczynającymi się od „myPool”:

    $filter = "startswith(id,'myPool')"

    Get-AzureBatchPool -Filter $filter -BatchContext $context

Ta metoda nie jest tak elastyczna jak w przypadku korzystania z parametru „Where-Object” w lokalnym potoku. Jednak hello zapytania są wysyłane toohello usługa partia zadań bezpośrednio dzięki temu wszystkie filtrowania odbywa się na powitania po stronie serwera, zapisywanie przepustowości połączenia z Internetem.

### <a name="use-hello-id-parameter"></a>Użyj parametru Id hello
Filtr OData alternatywnych tooan jest toouse hello **identyfikator** parametru. tooquery dla określonej puli z identyfikatorem "myPool":

    Get-AzureBatchPool -Id "myPool" -BatchContext $context

Witaj **identyfikator** parametru obsługuje tylko pełny identyfikator wyszukiwania, nie symboli wieloznacznych lub OData-style filtrów.

### <a name="use-hello-maxcount-parameter"></a>Użyj parametru MaxCount hello
Domyślnie każde polecenie cmdlet zwraca maksymalnie 1000 obiektów. Jeśli osiągnięciu tego limitu uściślić toobring Twojego filtr ponownie mniejszą liczbę obiektów albo jawnie ustawiona przy użyciu hello maksymalnie **MaxCount** parametru. Na przykład:

    Get-AzureBatchTask -MaxCount 2500 -BatchContext $context

Ustaw tooremove hello górną granicę, **MaxCount** too0 lub mniej.

### <a name="use-hello-powershell-pipeline"></a>Użyj hello potoku środowiska PowerShell
Polecenia cmdlet partii można wykorzystać hello PowerShell potoku toosend danych między poleceniami cmdlet. To ustawienie hello efektu takie same jak określenie parametru, ale powoduje, że praca z wieloma jednostkami.

Na przykład znalezienie i wyświetlenie wszystkich zadań na Twoim koncie:

    Get-AzureBatchJob -BatchContext $context | Get-AzureBatchTask -BatchContext $context

Ponowne uruchomienie (ponowny rozruch) każdego węzła obliczeniowego w puli:

    Get-AzureBatchComputeNode -PoolId "myPool" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

## <a name="application-package-management"></a>Zarządzanie pakietem aplikacji
Pakiety aplikacji umożliwiają uproszczony toohello aplikacji toodeploy obliczeniowe węzłów w Twojej puli. Z poleceń cmdlet programu PowerShell partii hello można przekazać i Zarządzaj pakietami aplikacji w ramach konta usługi partia zadań i wdrożyć węzły toocompute wersje pakietu.

**Tworzenie** aplikacji:

    New-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

**Dodawanie** pakietu aplikacji:

    New-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0" -Format zip -FilePath package001.zip

Zestaw hello **wersja domyślna** dla aplikacji hello:

    Set-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -DefaultVersion "1.0"

**Wyświetlanie listy** pakietów aplikacji

    $application = Get-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

    $application.ApplicationPackages

**Usuwanie** pakietu aplikacji

    Remove-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0"

**Usuwanie** aplikacji

    Remove-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

> [!NOTE]
> Przed usunięciem aplikacji hello należy usunąć wszystkie wersji pakietu aplikacji dla aplikacji. Zostanie wyświetlony błąd "Konflikt", Jeśli spróbujesz toodelete aplikacji, która ma obecnie pakietów aplikacji.
> 
> 

### <a name="deploy-an-application-package"></a>Wdrażanie pakietu aplikacji
Podczas tworzenia puli możesz określić co najmniej jeden pakiet aplikacji dla wdrożenia. Po określeniu pakietu w czasie tworzenia puli jest węzeł tooeach wdrożonych jako hello węzła sprzężenia puli. Pakiety są też wdrażane, gdy węzeł zostaje uruchomiony ponownie lub odtworzony z obrazu.

Określ hello `-ApplicationPackageReference` podczas tworzenia toodeploy puli węzłów pakietu toohello puli aplikacji jako dołączenia hello puli. Najpierw utwórz **PSApplicationPackageReference** obiektu i skonfigurować go z hello identyfikatorów i wersją aplikacji ma węzły obliczeniowe toodeploy toohello puli:

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "1.0"

Teraz Utwórz pulę hello i określ obiektu odwołania pakietu hello hello argument toohello `ApplicationPackageReferences` opcji:

    New-AzureBatchPool -Id "PoolWithAppPackage" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -BatchContext $context -ApplicationPackageReferences $appPackageReference

Można znaleźć więcej informacji na temat pakietów aplikacji w [wdrożyć aplikacje toocompute węzły z pakietami aplikacji partii](batch-application-packages.md).

> [!IMPORTANT]
> Należy [połączyć konto usługi Azure Storage](#linked-storage-account-autostorage) tooyour partii konta toouse pakietów aplikacji.
> 
> 

### <a name="update-a-pools-application-packages"></a>Aktualizowanie pakietów aplikacji puli
przypisane tooan istniejącą pulę aplikacji hello tooupdate najpierw utwórz obiekt PSApplicationPackageReference z właściwościami hello żądanego (wersja identyfikator i pakietów aplikacji):

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "2.0"

Następnie Pobierz pulę hello z partii, wyczyszczenie wszelkie istniejące pakiety Dodaj nasze nowe odwołanie do pakietu i hello partii usługi aktualizacji przy użyciu nowych ustawień puli hello:

    $pool = Get-AzureBatchPool -BatchContext $context -Id "PoolWithAppPackage"

    $pool.ApplicationPackageReferences.Clear()

    $pool.ApplicationPackageReferences.Add($appPackageReference)

    Set-AzureBatchPool -BatchContext $context -Pool $pool

Użytkownik zaktualizował teraz właściwości puli hello w hello usługa partia zadań. tooactually wdrażanie hello nowego pakietu toocompute węzłów aplikacji w puli hello, jednak należy ponownie uruchomić lub odtworzyć tych węzłów. Każdy węzeł w puli możesz uruchomić ponownie za pomocą tego polecenia:

    Get-AzureBatchComputeNode -PoolId "PoolWithAppPackage" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

> [!TIP]
> Można wdrażać wielu aplikacji pakietów toohello węzłów obliczeniowych w puli. Jeśli chcesz zbyt*dodać* pakietu aplikacji zamiast zastępowania pakietów hello obecnie wdrożona, Pomiń hello `$pool.ApplicationPackageReferences.Clear()` wiersz powyżej.
> 
> 

## <a name="next-steps"></a>Następne kroki
* Szczegóły składni poleceń cmdlet oraz przykłady znajdują się w [dokumentacji dotyczącej poleceń cmdlet w usłudze Azure Batch](/powershell/module/azurerm.batch/#batch).
* Aby uzyskać więcej informacji o aplikacji i pakietów aplikacji w partii, zobacz [wdrożyć aplikacje toocompute węzły z pakietami aplikacji partii](batch-application-packages.md).

[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/