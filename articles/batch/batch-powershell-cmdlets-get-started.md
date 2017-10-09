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
# <a name="manage-batch-resources-with-powershell-cmdlets"></a><span data-ttu-id="0c3a9-103">Zarządzanie zasobami usługi Batch za pomocą poleceń cmdlet programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="0c3a9-103">Manage Batch resources with PowerShell cmdlets</span></span>

<span data-ttu-id="0c3a9-104">Z hello poleceń cmdlet programu PowerShell usługi partia zadań Azure, można wykonać i wiele hello skryptu tego samego zadania wykonywane z hello API partii hello portalu Azure i hello Azure interfejsu wiersza polecenia (CLI).</span><span class="sxs-lookup"><span data-stu-id="0c3a9-104">With hello Azure Batch PowerShell cmdlets, you can perform and script many of hello same tasks you carry out with hello Batch APIs, hello Azure portal, and hello Azure Command-Line Interface (CLI).</span></span> <span data-ttu-id="0c3a9-105">Jest to szybkie wprowadzenie toohello polecenia cmdlet można użyć toomanage kont usługi partia zadań i pracy z zasobami usługi partia zadań takich jak pule, zadań i zadań.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-105">This is a quick introduction toohello cmdlets you can use toomanage your Batch accounts and work with your Batch resources such as pools, jobs, and tasks.</span></span>

<span data-ttu-id="0c3a9-106">Aby uzyskać pełną listę poleceń cmdlet partii i składnię szczegółowe poleceń cmdlet Zobacz hello [dokumentacji poleceń cmdlet partii zadań Azure](/powershell/module/azurerm.batch/#batch).</span><span class="sxs-lookup"><span data-stu-id="0c3a9-106">For a complete list of Batch cmdlets and detailed cmdlet syntax, see hello [Azure Batch cmdlet reference](/powershell/module/azurerm.batch/#batch).</span></span>

<span data-ttu-id="0c3a9-107">Informacje w tym artykule dotyczą poleceń cmdlet programu Azure PowerShell w wersji 3.0.0.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-107">This article is based on cmdlets in Azure PowerShell version 3.0.0.</span></span> <span data-ttu-id="0c3a9-108">Firma Microsoft zaleca się zaktualizowanie programu Azure PowerShell często tootake zalet usługi aktualizacji i ulepszeń.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-108">We recommend that you update your Azure PowerShell frequently tootake advantage of service updates and enhancements.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0c3a9-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="0c3a9-109">Prerequisites</span></span>
<span data-ttu-id="0c3a9-110">Wykonaj następujące operacje toouse programu Azure PowerShell toomanage hello zasobami partii.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-110">Perform hello following operations toouse Azure PowerShell toomanage your Batch resources.</span></span>

* [<span data-ttu-id="0c3a9-111">Zainstaluj i skonfiguruj program Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0c3a9-111">Install and configure Azure PowerShell</span></span>](/powershell/azure/overview)
* <span data-ttu-id="0c3a9-112">Uruchom hello **Login-AzureRmAccount** polecenia cmdlet tooconnect tooyour subskrypcji (hello partii zadań Azure statku poleceń cmdlet w module usługi Azure Resource Manager hello):</span><span class="sxs-lookup"><span data-stu-id="0c3a9-112">Run hello **Login-AzureRmAccount** cmdlet tooconnect tooyour subscription (hello Azure Batch cmdlets ship in hello Azure Resource Manager module):</span></span>
  
    `Login-AzureRmAccount`
* <span data-ttu-id="0c3a9-113">**Zarejestruj przestrzeń nazw dostawcy partii hello**.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-113">**Register with hello Batch provider namespace**.</span></span> <span data-ttu-id="0c3a9-114">Ta operacja wymaga tylko toobe wykonać **raz dla subskrypcji**.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-114">This operation only needs toobe performed **once per subscription**.</span></span>
  
    `Register-AzureRMResourceProvider -ProviderNamespace Microsoft.Batch`

## <a name="manage-batch-accounts-and-keys"></a><span data-ttu-id="0c3a9-115">Zarządzanie kontami i kluczami usługi Batch</span><span class="sxs-lookup"><span data-stu-id="0c3a9-115">Manage Batch accounts and keys</span></span>
### <a name="create-a-batch-account"></a><span data-ttu-id="0c3a9-116">Tworzenie konta usługi Batch</span><span class="sxs-lookup"><span data-stu-id="0c3a9-116">Create a Batch account</span></span>
<span data-ttu-id="0c3a9-117">Polecenie **New-AzureRmBatchAccount** umożliwia utworzenie konta usługi Batch w określonej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-117">**New-AzureRmBatchAccount** creates a Batch account in a specified resource group.</span></span> <span data-ttu-id="0c3a9-118">Jeśli nie masz już grupę zasobów, utwórz ją, uruchamiając hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-118">If you don't already have a resource group, create one by running hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.</span></span> <span data-ttu-id="0c3a9-119">Określ jedną z hello Azure regionach hello **lokalizacji** parametrów, takich jak "Środkowe stany USA".</span><span class="sxs-lookup"><span data-stu-id="0c3a9-119">Specify one of hello Azure regions in hello **Location** parameter, such as "Central US".</span></span> <span data-ttu-id="0c3a9-120">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="0c3a9-120">For example:</span></span>

    New-AzureRmResourceGroup –Name MyBatchResourceGroup –location "Central US"

<span data-ttu-id="0c3a9-121">Następnie utwórz konta usługi partia zadań w grupie zasobów hello, określając nazwę konta hello w <*nazwa_konta*> i hello lokalizację i nazwę grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-121">Then, create a Batch account in hello resource group, specifying a name for hello account in <*account_name*> and hello location and name of your resource group.</span></span> <span data-ttu-id="0c3a9-122">Tworzenie konta usługi partia zadań hello może zająć niektórych toocomplete czasu.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-122">Creating hello Batch account can take some time toocomplete.</span></span> <span data-ttu-id="0c3a9-123">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="0c3a9-123">For example:</span></span>

    New-AzureRmBatchAccount –AccountName <account_name> –Location "Central US" –ResourceGroupName <res_group_name>

> [!NOTE]
> <span data-ttu-id="0c3a9-124">Konto usługi partia zadań Hello nazwa musi być unikatowa toohello region platformy Azure dla grupy zasobów hello, zawierać od 3 do 24 znaków i korzystać tylko małe litery i cyfry.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-124">hello Batch account name must be unique toohello Azure region for hello resource group, contain between 3 and 24 characters, and use lowercase letters and numbers only.</span></span>
> 
> 

### <a name="get-account-access-keys"></a><span data-ttu-id="0c3a9-125">Pobieranie kluczy dostępu do konta</span><span class="sxs-lookup"><span data-stu-id="0c3a9-125">Get account access keys</span></span>
<span data-ttu-id="0c3a9-126">**Get-AzureRmBatchAccountKeys** zawiera klucze dostępu hello skojarzone z kontem usługi partia zadań Azure.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-126">**Get-AzureRmBatchAccountKeys** shows hello access keys associated with an Azure Batch account.</span></span> <span data-ttu-id="0c3a9-127">Na przykład uruchom powitania po tooget klucze podstawowe i pomocnicze hello hello konta została utworzona.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-127">For example, run hello following tooget hello primary and secondary keys of hello account you created.</span></span>

    $Account = Get-AzureRmBatchAccountKeys –AccountName <account_name>

    $Account.PrimaryAccountKey

    $Account.SecondaryAccountKey

### <a name="generate-a-new-access-key"></a><span data-ttu-id="0c3a9-128">Generowanie nowego klucza dostępu</span><span class="sxs-lookup"><span data-stu-id="0c3a9-128">Generate a new access key</span></span>
<span data-ttu-id="0c3a9-129">Polecenie **New-AzureRmBatchAccountKey** umożliwia generowanie nowego klucza podstawowego lub klucza pomocniczego do konta usługi Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-129">**New-AzureRmBatchAccountKey** generates a new primary or secondary account key for an Azure Batch account.</span></span> <span data-ttu-id="0c3a9-130">Na przykład toogenerate nowego klucza podstawowego dla konta wsadowego, wpisz:</span><span class="sxs-lookup"><span data-stu-id="0c3a9-130">For example, toogenerate a new primary key for your Batch account, type:</span></span>

    New-AzureRmBatchAccountKey -AccountName <account_name> -KeyType Primary

> [!NOTE]
> <span data-ttu-id="0c3a9-131">toogenerate klucza pomocniczego, określ "Pomocniczy" hello **KeyType** parametru.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-131">toogenerate a new secondary key, specify "Secondary" for hello **KeyType** parameter.</span></span> <span data-ttu-id="0c3a9-132">Masz klucze podstawowe i pomocnicze hello tooregenerate oddzielnie.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-132">You have tooregenerate hello primary and secondary keys separately.</span></span>
> 
> 

### <a name="delete-a-batch-account"></a><span data-ttu-id="0c3a9-133">Usuwanie konta usługi Batch</span><span class="sxs-lookup"><span data-stu-id="0c3a9-133">Delete a Batch account</span></span>
<span data-ttu-id="0c3a9-134">Polecenie **Remove-AzureRmBatchAccount** umożliwia usunięcie konta usługi Batch.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-134">**Remove-AzureRmBatchAccount** deletes a Batch account.</span></span> <span data-ttu-id="0c3a9-135">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="0c3a9-135">For example:</span></span>

    Remove-AzureRmBatchAccount -AccountName <account_name>

<span data-ttu-id="0c3a9-136">Po wyświetleniu monitu Potwierdź, że chcesz tooremove hello konta.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-136">When prompted, confirm you want tooremove hello account.</span></span> <span data-ttu-id="0c3a9-137">Usunięcie konta może zająć niektórych toocomplete czasu.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-137">Account removal can take some time toocomplete.</span></span>

## <a name="create-a-batchaccountcontext-object"></a><span data-ttu-id="0c3a9-138">Tworzenie obiektu BatchAccountContext</span><span class="sxs-lookup"><span data-stu-id="0c3a9-138">Create a BatchAccountContext object</span></span>
<span data-ttu-id="0c3a9-139">tooauthenticate przy użyciu hello poleceń cmdlet programu PowerShell partii, gdy tworzenie i Zarządzanie pulami partii, zadania, zadania i inne zasoby, najpierw utwórz toostore obiektu BatchAccountContext nazwę konta i kluczy:</span><span class="sxs-lookup"><span data-stu-id="0c3a9-139">tooauthenticate using hello Batch PowerShell cmdlets when you create and manage Batch pools, jobs, tasks, and other resources, first create a BatchAccountContext object toostore your account name and keys:</span></span>

    $context = Get-AzureRmBatchAccountKeys -AccountName <account_name>

<span data-ttu-id="0c3a9-140">Przekazujesz hello BatchAccountContext obiektu do poleceń cmdlet tego hello użyj **BatchContext** parametru.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-140">You pass hello BatchAccountContext object into cmdlets that use hello **BatchContext** parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="0c3a9-141">Domyślnie klucza podstawowego konta hello jest używany do uwierzytelniania, ale jawnie wybrać toouse klucza hello zmieniając obiektu BatchAccountContext **KeyInUse** właściwości: `$context.KeyInUse = "Secondary"`.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-141">By default, hello account's primary key is used for authentication, but you can explicitly select hello key toouse by changing your BatchAccountContext object’s **KeyInUse** property: `$context.KeyInUse = "Secondary"`.</span></span>
> 
> 

## <a name="create-and-modify-batch-resources"></a><span data-ttu-id="0c3a9-142">Tworzenie i modyfikowanie zasobów usługi Batch</span><span class="sxs-lookup"><span data-stu-id="0c3a9-142">Create and modify Batch resources</span></span>
<span data-ttu-id="0c3a9-143">Użyj polecenia cmdlet, takich jak **AzureBatchPool nowy**, **AzureBatchJob nowy**, i **AzureBatchTask nowy** toocreate zasobów w ramach konta usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-143">Use cmdlets such as **New-AzureBatchPool**, **New-AzureBatchJob**, and **New-AzureBatchTask** toocreate resources under a Batch account.</span></span> <span data-ttu-id="0c3a9-144">Istnieją odpowiadające im **Get -** i **Set -** poleceń cmdlet tooupdate hello właściwości istniejących zasobów i **Remove -** zasobów tooremove poleceń cmdlet w ramach konta usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-144">There are corresponding **Get-** and **Set-** cmdlets tooupdate hello properties of existing resources, and  **Remove-** cmdlets tooremove resources under a Batch account.</span></span>

<span data-ttu-id="0c3a9-145">Korzystając z wielu z tych poleceń cmdlet w toopassing dodanie obiektu BatchContext, należy toocreate lub Przekaż obiektów zawierających ustawienia szczegółowe zasobów, jak pokazano w hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-145">When using many of these cmdlets, in addition toopassing a BatchContext object, you need toocreate or pass objects that contain detailed resource settings, as shown in hello following example.</span></span> <span data-ttu-id="0c3a9-146">Zobacz hello szczegółową pomoc dla poszczególnych poleceń cmdlet, aby uzyskać dodatkowe przykłady.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-146">See hello detailed help for each cmdlet for additional examples.</span></span>

### <a name="create-a-batch-pool"></a><span data-ttu-id="0c3a9-147">Tworzenie puli usługi Batch</span><span class="sxs-lookup"><span data-stu-id="0c3a9-147">Create a Batch pool</span></span>
<span data-ttu-id="0c3a9-148">Podczas tworzenia lub aktualizowania puli partii, wybraniu konfiguracji usługi w chmurze hello lub hello konfiguracji maszyny wirtualnej dla hello systemu operacyjnego na powitania węzły obliczeniowe (zobacz [Przegląd funkcji partii](batch-api-basics.md#pool)).</span><span class="sxs-lookup"><span data-stu-id="0c3a9-148">When creating or updating a Batch pool, you select either hello cloud service configuration or hello virtual machine configuration for hello operating system on hello compute nodes (see [Batch feature overview](batch-api-basics.md#pool)).</span></span> <span data-ttu-id="0c3a9-149">Jeśli określisz konfiguracji usługi w chmurze hello węzłów obliczeniowych obraz zostanie utworzony z jednym hello [wersje systemu operacyjnego gościa Azure](../cloud-services/cloud-services-guestos-update-matrix.md#releases).</span><span class="sxs-lookup"><span data-stu-id="0c3a9-149">If you specify hello cloud service configuration, your compute nodes are imaged with one of hello [Azure Guest OS releases](../cloud-services/cloud-services-guestos-update-matrix.md#releases).</span></span> <span data-ttu-id="0c3a9-150">Jeśli określisz hello konfiguracji maszyny wirtualnej, można określić jedną hello obsługiwane Linux lub maszyny Wirtualnej systemu Windows obrazy hello wymienionych w [Marketplace maszyny wirtualne Azure][vm_marketplace], lub podać niestandardowy obraz, który już przygotowane.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-150">If you specify hello virtual machine configuration, you can either specify one of hello supported Linux or Windows VM images listed in hello [Azure Virtual Machines Marketplace][vm_marketplace], or provide a custom image that you have prepared.</span></span>

<span data-ttu-id="0c3a9-151">Po uruchomieniu **AzureBatchPool nowy**, przekazywanie obiektu PSCloudServiceConfiguration lub PSVirtualMachineConfiguration hello ustawień systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-151">When you run **New-AzureBatchPool**, pass hello operating system settings in a PSCloudServiceConfiguration or PSVirtualMachineConfiguration object.</span></span> <span data-ttu-id="0c3a9-152">Na przykład hello następujące polecenie cmdlet tworzy nową pulę partii z węzłów obliczeniowych mały rozmiar w konfiguracji usługi chmury hello obrazami z najnowszą wersją systemu operacyjnego hello rodziny 3 (Windows Server 2012).</span><span class="sxs-lookup"><span data-stu-id="0c3a9-152">For example, hello following cmdlet creates a new Batch pool with size Small compute nodes in hello cloud service configuration, imaged with hello latest operating system version of family 3 (Windows Server 2012).</span></span> <span data-ttu-id="0c3a9-153">W tym miejscu hello **CloudServiceConfiguration** parametr określa hello *$configuration* zmiennej jako hello PSCloudServiceConfiguration obiektu.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-153">Here, hello **CloudServiceConfiguration** parameter specifies hello *$configuration* variable as hello PSCloudServiceConfiguration object.</span></span> <span data-ttu-id="0c3a9-154">Witaj **BatchContext** parametr określa uprzednio zdefiniowanej zmiennej *$context* jako hello BatchAccountContext obiektu.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-154">hello **BatchContext** parameter specifies a previously defined variable *$context* as hello BatchAccountContext object.</span></span>

    $configuration = New-Object -TypeName "Microsoft.Azure.Commands.Batch.Models.PSCloudServiceConfiguration" -ArgumentList @(4,"*")

    New-AzureBatchPool -Id "AutoScalePool" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -AutoScaleFormula '$TargetDedicated=4;' -BatchContext $context

<span data-ttu-id="0c3a9-155">Hello docelowy węzłów obliczeniowych w nowej puli hello jest określana na podstawie formuły Skalowanie automatyczne.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-155">hello target number of compute nodes in hello new pool is determined by an autoscaling formula.</span></span> <span data-ttu-id="0c3a9-156">W takim przypadku formuła hello jest po prostu **$TargetDedicated = 4**, określającą hello liczbę węzłów obliczeniowych w puli hello jest maksymalnie 4.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-156">In this case, hello formula is simply **$TargetDedicated=4**, indicating hello number of compute nodes in hello pool is 4 at most.</span></span>

## <a name="query-for-pools-jobs-tasks-and-other-details"></a><span data-ttu-id="0c3a9-157">Zapytania dotyczące puli, zadań, podzadań oraz innych szczegółów</span><span class="sxs-lookup"><span data-stu-id="0c3a9-157">Query for pools, jobs, tasks, and other details</span></span>
<span data-ttu-id="0c3a9-158">Użyj polecenia cmdlet, takich jak **Get-AzureBatchPool**, **Get-AzureBatchJob**, i **Get-AzureBatchTask** tooquery dla jednostek utworzone w ramach konta usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-158">Use cmdlets such as **Get-AzureBatchPool**, **Get-AzureBatchJob**, and **Get-AzureBatchTask** tooquery for entities created under a Batch account.</span></span>

### <a name="query-for-data"></a><span data-ttu-id="0c3a9-159">Zapytania dotyczące danych</span><span class="sxs-lookup"><span data-stu-id="0c3a9-159">Query for data</span></span>
<span data-ttu-id="0c3a9-160">Na przykład użyć **Get-AzureBatchPools** toofind Twojego pule.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-160">As an example, use **Get-AzureBatchPools** toofind your pools.</span></span> <span data-ttu-id="0c3a9-161">Domyślnie to zapytanie dla wszystkich pul na koncie, zakładając, że możesz już przechowywane hello BatchAccountContext obiektu w *$context*:</span><span class="sxs-lookup"><span data-stu-id="0c3a9-161">By default this queries for all pools under your account, assuming you already stored hello BatchAccountContext object in *$context*:</span></span>

    Get-AzureBatchPool -BatchContext $context

### <a name="use-an-odata-filter"></a><span data-ttu-id="0c3a9-162">Korzystanie z filtru OData</span><span class="sxs-lookup"><span data-stu-id="0c3a9-162">Use an OData filter</span></span>
<span data-ttu-id="0c3a9-163">Możesz podać filtru OData przy użyciu hello **filtru** toofind parametru tylko hello interesują Cię obiekty.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-163">You can supply an OData filter using hello **Filter** parameter toofind only hello objects you’re interested in.</span></span> <span data-ttu-id="0c3a9-164">Np. można znaleźć wszystkie pule z identyfikatorami zaczynającymi się od „myPool”:</span><span class="sxs-lookup"><span data-stu-id="0c3a9-164">For example, you can find all pools with ids starting with “myPool”:</span></span>

    $filter = "startswith(id,'myPool')"

    Get-AzureBatchPool -Filter $filter -BatchContext $context

<span data-ttu-id="0c3a9-165">Ta metoda nie jest tak elastyczna jak w przypadku korzystania z parametru „Where-Object” w lokalnym potoku.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-165">This method is not as flexible as using “Where-Object” in a local pipeline.</span></span> <span data-ttu-id="0c3a9-166">Jednak hello zapytania są wysyłane toohello usługa partia zadań bezpośrednio dzięki temu wszystkie filtrowania odbywa się na powitania po stronie serwera, zapisywanie przepustowości połączenia z Internetem.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-166">However, hello query gets sent toohello Batch service directly so that all filtering happens on hello server side, saving Internet bandwidth.</span></span>

### <a name="use-hello-id-parameter"></a><span data-ttu-id="0c3a9-167">Użyj parametru Id hello</span><span class="sxs-lookup"><span data-stu-id="0c3a9-167">Use hello Id parameter</span></span>
<span data-ttu-id="0c3a9-168">Filtr OData alternatywnych tooan jest toouse hello **identyfikator** parametru.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-168">An alternative tooan OData filter is toouse hello **Id** parameter.</span></span> <span data-ttu-id="0c3a9-169">tooquery dla określonej puli z identyfikatorem "myPool":</span><span class="sxs-lookup"><span data-stu-id="0c3a9-169">tooquery for a specific pool with id "myPool":</span></span>

    Get-AzureBatchPool -Id "myPool" -BatchContext $context

<span data-ttu-id="0c3a9-170">Witaj **identyfikator** parametru obsługuje tylko pełny identyfikator wyszukiwania, nie symboli wieloznacznych lub OData-style filtrów.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-170">hello **Id** parameter supports only full-id search, not wildcards or OData-style filters.</span></span>

### <a name="use-hello-maxcount-parameter"></a><span data-ttu-id="0c3a9-171">Użyj parametru MaxCount hello</span><span class="sxs-lookup"><span data-stu-id="0c3a9-171">Use hello MaxCount parameter</span></span>
<span data-ttu-id="0c3a9-172">Domyślnie każde polecenie cmdlet zwraca maksymalnie 1000 obiektów.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-172">By default, each cmdlet returns a maximum of 1000 objects.</span></span> <span data-ttu-id="0c3a9-173">Jeśli osiągnięciu tego limitu uściślić toobring Twojego filtr ponownie mniejszą liczbę obiektów albo jawnie ustawiona przy użyciu hello maksymalnie **MaxCount** parametru.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-173">If you reach this limit, either refine your filter toobring back fewer objects, or explicitly set a maximum using hello **MaxCount** parameter.</span></span> <span data-ttu-id="0c3a9-174">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="0c3a9-174">For example:</span></span>

    Get-AzureBatchTask -MaxCount 2500 -BatchContext $context

<span data-ttu-id="0c3a9-175">Ustaw tooremove hello górną granicę, **MaxCount** too0 lub mniej.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-175">tooremove hello upper bound, set **MaxCount** too0 or less.</span></span>

### <a name="use-hello-powershell-pipeline"></a><span data-ttu-id="0c3a9-176">Użyj hello potoku środowiska PowerShell</span><span class="sxs-lookup"><span data-stu-id="0c3a9-176">Use hello PowerShell pipeline</span></span>
<span data-ttu-id="0c3a9-177">Polecenia cmdlet partii można wykorzystać hello PowerShell potoku toosend danych między poleceniami cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-177">Batch cmdlets can leverage hello PowerShell pipeline toosend data between cmdlets.</span></span> <span data-ttu-id="0c3a9-178">To ustawienie hello efektu takie same jak określenie parametru, ale powoduje, że praca z wieloma jednostkami.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-178">This has hello same effect as specifying a parameter, but makes working with multiple entities easier.</span></span>

<span data-ttu-id="0c3a9-179">Na przykład znalezienie i wyświetlenie wszystkich zadań na Twoim koncie:</span><span class="sxs-lookup"><span data-stu-id="0c3a9-179">For example, find and display all tasks under your account:</span></span>

    Get-AzureBatchJob -BatchContext $context | Get-AzureBatchTask -BatchContext $context

<span data-ttu-id="0c3a9-180">Ponowne uruchomienie (ponowny rozruch) każdego węzła obliczeniowego w puli:</span><span class="sxs-lookup"><span data-stu-id="0c3a9-180">Restart (reboot) every compute node in a pool:</span></span>

    Get-AzureBatchComputeNode -PoolId "myPool" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

## <a name="application-package-management"></a><span data-ttu-id="0c3a9-181">Zarządzanie pakietem aplikacji</span><span class="sxs-lookup"><span data-stu-id="0c3a9-181">Application package management</span></span>
<span data-ttu-id="0c3a9-182">Pakiety aplikacji umożliwiają uproszczony toohello aplikacji toodeploy obliczeniowe węzłów w Twojej puli.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-182">Application packages provide a simplified way toodeploy applications toohello compute nodes in your pools.</span></span> <span data-ttu-id="0c3a9-183">Z poleceń cmdlet programu PowerShell partii hello można przekazać i Zarządzaj pakietami aplikacji w ramach konta usługi partia zadań i wdrożyć węzły toocompute wersje pakietu.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-183">With hello Batch PowerShell cmdlets, you can upload and manage application packages in your Batch account, and deploy package versions toocompute nodes.</span></span>

<span data-ttu-id="0c3a9-184">**Tworzenie** aplikacji:</span><span class="sxs-lookup"><span data-stu-id="0c3a9-184">**Create** an application:</span></span>

    New-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

<span data-ttu-id="0c3a9-185">**Dodawanie** pakietu aplikacji:</span><span class="sxs-lookup"><span data-stu-id="0c3a9-185">**Add** an application package:</span></span>

    New-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0" -Format zip -FilePath package001.zip

<span data-ttu-id="0c3a9-186">Zestaw hello **wersja domyślna** dla aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="0c3a9-186">Set hello **default version** for hello application:</span></span>

    Set-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -DefaultVersion "1.0"

<span data-ttu-id="0c3a9-187">**Wyświetlanie listy** pakietów aplikacji</span><span class="sxs-lookup"><span data-stu-id="0c3a9-187">**List** an application's packages</span></span>

    $application = Get-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

    $application.ApplicationPackages

<span data-ttu-id="0c3a9-188">**Usuwanie** pakietu aplikacji</span><span class="sxs-lookup"><span data-stu-id="0c3a9-188">**Delete** an application package</span></span>

    Remove-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0"

<span data-ttu-id="0c3a9-189">**Usuwanie** aplikacji</span><span class="sxs-lookup"><span data-stu-id="0c3a9-189">**Delete** an application</span></span>

    Remove-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

> [!NOTE]
> <span data-ttu-id="0c3a9-190">Przed usunięciem aplikacji hello należy usunąć wszystkie wersji pakietu aplikacji dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-190">You must delete all of an application's application package versions before you delete hello application.</span></span> <span data-ttu-id="0c3a9-191">Zostanie wyświetlony błąd "Konflikt", Jeśli spróbujesz toodelete aplikacji, która ma obecnie pakietów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-191">You will receive a 'Conflict' error if you try toodelete an application that currently has application packages.</span></span>
> 
> 

### <a name="deploy-an-application-package"></a><span data-ttu-id="0c3a9-192">Wdrażanie pakietu aplikacji</span><span class="sxs-lookup"><span data-stu-id="0c3a9-192">Deploy an application package</span></span>
<span data-ttu-id="0c3a9-193">Podczas tworzenia puli możesz określić co najmniej jeden pakiet aplikacji dla wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-193">You can specify one or more application packages for deployment when you create a pool.</span></span> <span data-ttu-id="0c3a9-194">Po określeniu pakietu w czasie tworzenia puli jest węzeł tooeach wdrożonych jako hello węzła sprzężenia puli.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-194">When you specify a package at pool creation time, it is deployed tooeach node as hello node joins pool.</span></span> <span data-ttu-id="0c3a9-195">Pakiety są też wdrażane, gdy węzeł zostaje uruchomiony ponownie lub odtworzony z obrazu.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-195">Packages are also deployed when a node is rebooted or reimaged.</span></span>

<span data-ttu-id="0c3a9-196">Określ hello `-ApplicationPackageReference` podczas tworzenia toodeploy puli węzłów pakietu toohello puli aplikacji jako dołączenia hello puli.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-196">Specify hello `-ApplicationPackageReference` option when creating a pool toodeploy an application package toohello pool's nodes as they join hello pool.</span></span> <span data-ttu-id="0c3a9-197">Najpierw utwórz **PSApplicationPackageReference** obiektu i skonfigurować go z hello identyfikatorów i wersją aplikacji ma węzły obliczeniowe toodeploy toohello puli:</span><span class="sxs-lookup"><span data-stu-id="0c3a9-197">First, create a **PSApplicationPackageReference** object, and configure it with hello application Id and package version you want toodeploy toohello pool's compute nodes:</span></span>

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "1.0"

<span data-ttu-id="0c3a9-198">Teraz Utwórz pulę hello i określ obiektu odwołania pakietu hello hello argument toohello `ApplicationPackageReferences` opcji:</span><span class="sxs-lookup"><span data-stu-id="0c3a9-198">Now create hello pool, and specify hello package reference object as hello argument toohello `ApplicationPackageReferences` option:</span></span>

    New-AzureBatchPool -Id "PoolWithAppPackage" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -BatchContext $context -ApplicationPackageReferences $appPackageReference

<span data-ttu-id="0c3a9-199">Można znaleźć więcej informacji na temat pakietów aplikacji w [wdrożyć aplikacje toocompute węzły z pakietami aplikacji partii](batch-application-packages.md).</span><span class="sxs-lookup"><span data-stu-id="0c3a9-199">You can find more information on application packages in [Deploy applications toocompute nodes with Batch application packages](batch-application-packages.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0c3a9-200">Należy [połączyć konto usługi Azure Storage](#linked-storage-account-autostorage) tooyour partii konta toouse pakietów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-200">You must [link an Azure Storage account](#linked-storage-account-autostorage) tooyour Batch account toouse application packages.</span></span>
> 
> 

### <a name="update-a-pools-application-packages"></a><span data-ttu-id="0c3a9-201">Aktualizowanie pakietów aplikacji puli</span><span class="sxs-lookup"><span data-stu-id="0c3a9-201">Update a pool's application packages</span></span>
<span data-ttu-id="0c3a9-202">przypisane tooan istniejącą pulę aplikacji hello tooupdate najpierw utwórz obiekt PSApplicationPackageReference z właściwościami hello żądanego (wersja identyfikator i pakietów aplikacji):</span><span class="sxs-lookup"><span data-stu-id="0c3a9-202">tooupdate hello applications assigned tooan existing pool, first create a PSApplicationPackageReference object with hello desired properties (application Id and package version):</span></span>

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "2.0"

<span data-ttu-id="0c3a9-203">Następnie Pobierz pulę hello z partii, wyczyszczenie wszelkie istniejące pakiety Dodaj nasze nowe odwołanie do pakietu i hello partii usługi aktualizacji przy użyciu nowych ustawień puli hello:</span><span class="sxs-lookup"><span data-stu-id="0c3a9-203">Next, get hello pool from Batch, clear out any existing packages, add our new package reference, and update hello Batch service with hello new pool settings:</span></span>

    $pool = Get-AzureBatchPool -BatchContext $context -Id "PoolWithAppPackage"

    $pool.ApplicationPackageReferences.Clear()

    $pool.ApplicationPackageReferences.Add($appPackageReference)

    Set-AzureBatchPool -BatchContext $context -Pool $pool

<span data-ttu-id="0c3a9-204">Użytkownik zaktualizował teraz właściwości puli hello w hello usługa partia zadań.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-204">You've now updated hello pool's properties in hello Batch service.</span></span> <span data-ttu-id="0c3a9-205">tooactually wdrażanie hello nowego pakietu toocompute węzłów aplikacji w puli hello, jednak należy ponownie uruchomić lub odtworzyć tych węzłów.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-205">tooactually deploy hello new application package toocompute nodes in hello pool, however, you must restart or reimage those nodes.</span></span> <span data-ttu-id="0c3a9-206">Każdy węzeł w puli możesz uruchomić ponownie za pomocą tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="0c3a9-206">You can restart every node in a pool with this command:</span></span>

    Get-AzureBatchComputeNode -PoolId "PoolWithAppPackage" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

> [!TIP]
> <span data-ttu-id="0c3a9-207">Można wdrażać wielu aplikacji pakietów toohello węzłów obliczeniowych w puli.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-207">You can deploy multiple application packages toohello compute nodes in a pool.</span></span> <span data-ttu-id="0c3a9-208">Jeśli chcesz zbyt*dodać* pakietu aplikacji zamiast zastępowania pakietów hello obecnie wdrożona, Pomiń hello `$pool.ApplicationPackageReferences.Clear()` wiersz powyżej.</span><span class="sxs-lookup"><span data-stu-id="0c3a9-208">If you'd like too*add* an application package instead of replacing hello currently deployed packages, omit hello `$pool.ApplicationPackageReferences.Clear()` line above.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="0c3a9-209">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0c3a9-209">Next steps</span></span>
* <span data-ttu-id="0c3a9-210">Szczegóły składni poleceń cmdlet oraz przykłady znajdują się w [dokumentacji dotyczącej poleceń cmdlet w usłudze Azure Batch](/powershell/module/azurerm.batch/#batch).</span><span class="sxs-lookup"><span data-stu-id="0c3a9-210">For detailed cmdlet syntax and examples, see [Azure Batch cmdlet reference](/powershell/module/azurerm.batch/#batch).</span></span>
* <span data-ttu-id="0c3a9-211">Aby uzyskać więcej informacji o aplikacji i pakietów aplikacji w partii, zobacz [wdrożyć aplikacje toocompute węzły z pakietami aplikacji partii](batch-application-packages.md).</span><span class="sxs-lookup"><span data-stu-id="0c3a9-211">For more information about applications and application packages in Batch, see [Deploy applications toocompute nodes with Batch application packages](batch-application-packages.md).</span></span>

[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/