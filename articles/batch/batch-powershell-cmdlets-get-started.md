---
title: "Rozpoczęcie pracy z programem PowerShell dla usługi Azure Batch | Microsoft Docs"
description: "Krótkie wprowadzenie do poleceń cmdlet programu Azure PowerShell, których można użyć do zarządzania zasobami usługi Batch."
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
ms.openlocfilehash: e33be6ed658e00250ea1e80cd7da4d348fb18296
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="manage-batch-resources-with-powershell-cmdlets"></a><span data-ttu-id="0fc76-103">Zarządzanie zasobami usługi Batch za pomocą poleceń cmdlet programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="0fc76-103">Manage Batch resources with PowerShell cmdlets</span></span>

<span data-ttu-id="0fc76-104">Za pomocą poleceń cmdlet PowerShell usługi Azure Batch można wykonywać oraz tworzyć skrypty dla wielu tych samych zadań, które wykonuje się za pomocą interfejsów API usługi Batch, witryny Azure Portal oraz interfejsu wiersza polecenia Azure (CLI).</span><span class="sxs-lookup"><span data-stu-id="0fc76-104">With the Azure Batch PowerShell cmdlets, you can perform and script many of the same tasks you carry out with the Batch APIs, the Azure portal, and the Azure Command-Line Interface (CLI).</span></span> <span data-ttu-id="0fc76-105">Oto krótkie wprowadzenie do poleceń cmdlet, których można używać do zarządzania kontami usługi Batch oraz pracy z zasobami usługi Batch, np. pulami i zadaniami.</span><span class="sxs-lookup"><span data-stu-id="0fc76-105">This is a quick introduction to the cmdlets you can use to manage your Batch accounts and work with your Batch resources such as pools, jobs, and tasks.</span></span>

<span data-ttu-id="0fc76-106">Pełna lista poleceń cmdlet w usłudze Batch oraz szczegółowa składnia poleceń cmdlet znajdują się w [dokumentacji dotyczącej poleceń cmdlet w usłudze Azure Batch](/powershell/module/azurerm.batch/#batch).</span><span class="sxs-lookup"><span data-stu-id="0fc76-106">For a complete list of Batch cmdlets and detailed cmdlet syntax, see the [Azure Batch cmdlet reference](/powershell/module/azurerm.batch/#batch).</span></span>

<span data-ttu-id="0fc76-107">Informacje w tym artykule dotyczą poleceń cmdlet programu Azure PowerShell w wersji 3.0.0.</span><span class="sxs-lookup"><span data-stu-id="0fc76-107">This article is based on cmdlets in Azure PowerShell version 3.0.0.</span></span> <span data-ttu-id="0fc76-108">Zaleca się częstą aktualizację programu Azure PowerShell, aby mieć możliwość korzystania z aktualizacji i rozszerzeń usługi.</span><span class="sxs-lookup"><span data-stu-id="0fc76-108">We recommend that you update your Azure PowerShell frequently to take advantage of service updates and enhancements.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0fc76-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="0fc76-109">Prerequisites</span></span>
<span data-ttu-id="0fc76-110">Wykonaj poniższe operacje, aby używać programu Azure PowerShell do zarządzania zasobami usługi Batch.</span><span class="sxs-lookup"><span data-stu-id="0fc76-110">Perform the following operations to use Azure PowerShell to manage your Batch resources.</span></span>

* [<span data-ttu-id="0fc76-111">Zainstaluj i skonfiguruj program Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0fc76-111">Install and configure Azure PowerShell</span></span>](/powershell/azure/overview)
* <span data-ttu-id="0fc76-112">Uruchom polecenie cmdlet **Login-AzureRmAccount**, aby podłączyć się do subskrypcji (polecenia cmdlet usługi Azure Batch są dostarczane w module usługi Azure Resource Manager):</span><span class="sxs-lookup"><span data-stu-id="0fc76-112">Run the **Login-AzureRmAccount** cmdlet to connect to your subscription (the Azure Batch cmdlets ship in the Azure Resource Manager module):</span></span>
  
    `Login-AzureRmAccount`
* <span data-ttu-id="0fc76-113">**Zarejestruj się w przestrzeni nazw dostawcy usługi Batch**.</span><span class="sxs-lookup"><span data-stu-id="0fc76-113">**Register with the Batch provider namespace**.</span></span> <span data-ttu-id="0fc76-114">Tę operację należy wykonać tylko **raz w całym okresie obowiązywania subskrypcji**.</span><span class="sxs-lookup"><span data-stu-id="0fc76-114">This operation only needs to be performed **once per subscription**.</span></span>
  
    `Register-AzureRMResourceProvider -ProviderNamespace Microsoft.Batch`

## <a name="manage-batch-accounts-and-keys"></a><span data-ttu-id="0fc76-115">Zarządzanie kontami i kluczami usługi Batch</span><span class="sxs-lookup"><span data-stu-id="0fc76-115">Manage Batch accounts and keys</span></span>
### <a name="create-a-batch-account"></a><span data-ttu-id="0fc76-116">Tworzenie konta usługi Batch</span><span class="sxs-lookup"><span data-stu-id="0fc76-116">Create a Batch account</span></span>
<span data-ttu-id="0fc76-117">Polecenie **New-AzureRmBatchAccount** umożliwia utworzenie konta usługi Batch w określonej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="0fc76-117">**New-AzureRmBatchAccount** creates a Batch account in a specified resource group.</span></span> <span data-ttu-id="0fc76-118">Jeśli nie masz jeszcze grupy zasobów, utwórz ją, uruchamiając polecenie cmdlet [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="0fc76-118">If you don't already have a resource group, create one by running the [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.</span></span> <span data-ttu-id="0fc76-119">W parametrze **Location** określ jeden z regionów świadczenia usługi Azure, na przykład „Środkowe stany USA”.</span><span class="sxs-lookup"><span data-stu-id="0fc76-119">Specify one of the Azure regions in the **Location** parameter, such as "Central US".</span></span> <span data-ttu-id="0fc76-120">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="0fc76-120">For example:</span></span>

    New-AzureRmResourceGroup –Name MyBatchResourceGroup –location "Central US"

<span data-ttu-id="0fc76-121">Następnie utwórz konto usługi Batch w grupie zasobów, określając nazwę konta w parametrze <*account_name*> i lokalizację oraz nazwę grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="0fc76-121">Then, create a Batch account in the resource group, specifying a name for the account in <*account_name*> and the location and name of your resource group.</span></span> <span data-ttu-id="0fc76-122">Tworzenie konta usługi Batch może zająć nieco czasu.</span><span class="sxs-lookup"><span data-stu-id="0fc76-122">Creating the Batch account can take some time to complete.</span></span> <span data-ttu-id="0fc76-123">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="0fc76-123">For example:</span></span>

    New-AzureRmBatchAccount –AccountName <account_name> –Location "Central US" –ResourceGroupName <res_group_name>

> [!NOTE]
> <span data-ttu-id="0fc76-124">Nazwa konta usługi Batch musi być unikatowa dla regionu Azure dla grupy zasobów, zawierać od 3 do 24 znaków i tylko małe litery i cyfry.</span><span class="sxs-lookup"><span data-stu-id="0fc76-124">The Batch account name must be unique to the Azure region for the resource group, contain between 3 and 24 characters, and use lowercase letters and numbers only.</span></span>
> 
> 

### <a name="get-account-access-keys"></a><span data-ttu-id="0fc76-125">Pobieranie kluczy dostępu do konta</span><span class="sxs-lookup"><span data-stu-id="0fc76-125">Get account access keys</span></span>
<span data-ttu-id="0fc76-126">Polecenie **Get-AzureRmBatchAccountKeys** umożliwia wyświetlenie kluczy dostępu powiązanych z kontem usługi Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="0fc76-126">**Get-AzureRmBatchAccountKeys** shows the access keys associated with an Azure Batch account.</span></span> <span data-ttu-id="0fc76-127">Na przykład uruchom następujące polecenia, aby pobrać klucz podstawowy i klucz pomocniczy do utworzonego konta.</span><span class="sxs-lookup"><span data-stu-id="0fc76-127">For example, run the following to get the primary and secondary keys of the account you created.</span></span>

    $Account = Get-AzureRmBatchAccountKeys –AccountName <account_name>

    $Account.PrimaryAccountKey

    $Account.SecondaryAccountKey

### <a name="generate-a-new-access-key"></a><span data-ttu-id="0fc76-128">Generowanie nowego klucza dostępu</span><span class="sxs-lookup"><span data-stu-id="0fc76-128">Generate a new access key</span></span>
<span data-ttu-id="0fc76-129">Polecenie **New-AzureRmBatchAccountKey** umożliwia generowanie nowego klucza podstawowego lub klucza pomocniczego do konta usługi Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="0fc76-129">**New-AzureRmBatchAccountKey** generates a new primary or secondary account key for an Azure Batch account.</span></span> <span data-ttu-id="0fc76-130">Na przykład, aby wygenerować nowy klucz podstawowy do konta usługi Batch, wpisz:</span><span class="sxs-lookup"><span data-stu-id="0fc76-130">For example, to generate a new primary key for your Batch account, type:</span></span>

    New-AzureRmBatchAccountKey -AccountName <account_name> -KeyType Primary

> [!NOTE]
> <span data-ttu-id="0fc76-131">Aby wygenerować nowy klucz pomocniczy, wpisz „Secondary” dla parametru **KeyType**.</span><span class="sxs-lookup"><span data-stu-id="0fc76-131">To generate a new secondary key, specify "Secondary" for the **KeyType** parameter.</span></span> <span data-ttu-id="0fc76-132">Ponowne generowanie klucza podstawowego i klucza pomocniczego należy wykonywać oddzielnie.</span><span class="sxs-lookup"><span data-stu-id="0fc76-132">You have to regenerate the primary and secondary keys separately.</span></span>
> 
> 

### <a name="delete-a-batch-account"></a><span data-ttu-id="0fc76-133">Usuwanie konta usługi Batch</span><span class="sxs-lookup"><span data-stu-id="0fc76-133">Delete a Batch account</span></span>
<span data-ttu-id="0fc76-134">Polecenie **Remove-AzureRmBatchAccount** umożliwia usunięcie konta usługi Batch.</span><span class="sxs-lookup"><span data-stu-id="0fc76-134">**Remove-AzureRmBatchAccount** deletes a Batch account.</span></span> <span data-ttu-id="0fc76-135">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="0fc76-135">For example:</span></span>

    Remove-AzureRmBatchAccount -AccountName <account_name>

<span data-ttu-id="0fc76-136">Po wyświetleniu monitu potwierdź, że chcesz usunąć konto.</span><span class="sxs-lookup"><span data-stu-id="0fc76-136">When prompted, confirm you want to remove the account.</span></span> <span data-ttu-id="0fc76-137">Usunięcie konta może potrwać trochę czasu.</span><span class="sxs-lookup"><span data-stu-id="0fc76-137">Account removal can take some time to complete.</span></span>

## <a name="create-a-batchaccountcontext-object"></a><span data-ttu-id="0fc76-138">Tworzenie obiektu BatchAccountContext</span><span class="sxs-lookup"><span data-stu-id="0fc76-138">Create a BatchAccountContext object</span></span>
<span data-ttu-id="0fc76-139">Aby uwierzytelniać się przy użyciu poleceń cmdlet programu PowerShell w usłudze Batch podczas tworzenia pul, zadań, podzadań oraz innych zasobów w usłudze Batch oraz zarządzania nimi, najpierw utwórz obiekt BatchAccountContext, aby przechować nazwę konta i klucze do konta:</span><span class="sxs-lookup"><span data-stu-id="0fc76-139">To authenticate using the Batch PowerShell cmdlets when you create and manage Batch pools, jobs, tasks, and other resources, first create a BatchAccountContext object to store your account name and keys:</span></span>

    $context = Get-AzureRmBatchAccountKeys -AccountName <account_name>

<span data-ttu-id="0fc76-140">Obiekt BatchAccountContext zostaje przeniesiony do poleceń cmdlet, które używają parametru **BatchContext**.</span><span class="sxs-lookup"><span data-stu-id="0fc76-140">You pass the BatchAccountContext object into cmdlets that use the **BatchContext** parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="0fc76-141">Domyślnie do uwierzytelniania używany jest klucz podstawowy do konta, ale można jawnie wybrać klucz do użycia przez zmianę właściwości obiektu BatchAccountContext **KeyInUse**: `$context.KeyInUse = "Secondary"`.</span><span class="sxs-lookup"><span data-stu-id="0fc76-141">By default, the account's primary key is used for authentication, but you can explicitly select the key to use by changing your BatchAccountContext object’s **KeyInUse** property: `$context.KeyInUse = "Secondary"`.</span></span>
> 
> 

## <a name="create-and-modify-batch-resources"></a><span data-ttu-id="0fc76-142">Tworzenie i modyfikowanie zasobów usługi Batch</span><span class="sxs-lookup"><span data-stu-id="0fc76-142">Create and modify Batch resources</span></span>
<span data-ttu-id="0fc76-143">Do tworzenia zasobów w ramach konta usługi Batch służą takie polecenia cmdlet jak **New-AzureBatchPool**, **New-AzureBatchJob** oraz **New-AzureBatchTask**.</span><span class="sxs-lookup"><span data-stu-id="0fc76-143">Use cmdlets such as **New-AzureBatchPool**, **New-AzureBatchJob**, and **New-AzureBatchTask** to create resources under a Batch account.</span></span> <span data-ttu-id="0fc76-144">Istnieją odpowiednie polecenia cmdlet **Get-** i **Set-** do aktualizacji właściwości istniejących zasobów oraz polecenia cmdlet **Remove-** do usuwania zasobów w ramach konta usługi Batch.</span><span class="sxs-lookup"><span data-stu-id="0fc76-144">There are corresponding **Get-** and **Set-** cmdlets to update the properties of existing resources, and  **Remove-** cmdlets to remove resources under a Batch account.</span></span>

<span data-ttu-id="0fc76-145">Podczas korzystania z wielu tych poleceń cmdlet oprócz przekazywania obiektu BatchContext należy utworzyć lub przekazać obiekty, które zawierają szczegółowe ustawienia zasobów, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="0fc76-145">When using many of these cmdlets, in addition to passing a BatchContext object, you need to create or pass objects that contain detailed resource settings, as shown in the following example.</span></span> <span data-ttu-id="0fc76-146">Dodatkowe przykłady zamieszczono w szczegółowych plikach pomocy każdego polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0fc76-146">See the detailed help for each cmdlet for additional examples.</span></span>

### <a name="create-a-batch-pool"></a><span data-ttu-id="0fc76-147">Tworzenie puli usługi Batch</span><span class="sxs-lookup"><span data-stu-id="0fc76-147">Create a Batch pool</span></span>
<span data-ttu-id="0fc76-148">Podczas tworzenia lub aktualizowania puli usługi Batch należy wybrać konfigurację usługi w chmurze lub konfigurację maszyny wirtualnej dla systemu operacyjnego węzłów obliczeniowych — zobacz artykuł [Batch feature overview (Omówienie funkcji usługi Batch)](batch-api-basics.md#pool).</span><span class="sxs-lookup"><span data-stu-id="0fc76-148">When creating or updating a Batch pool, you select either the cloud service configuration or the virtual machine configuration for the operating system on the compute nodes (see [Batch feature overview](batch-api-basics.md#pool)).</span></span> <span data-ttu-id="0fc76-149">Jeśli wybierzesz konfigurację usługi w chmurze, węzły obliczeniowe będą obrazami z jednej z [wersji systemu operacyjnego gościa platformy Azure](../cloud-services/cloud-services-guestos-update-matrix.md#releases).</span><span class="sxs-lookup"><span data-stu-id="0fc76-149">If you specify the cloud service configuration, your compute nodes are imaged with one of the [Azure Guest OS releases](../cloud-services/cloud-services-guestos-update-matrix.md#releases).</span></span> <span data-ttu-id="0fc76-150">Jeśli wybierzesz konfigurację maszyny wirtualnej, możesz określić jeden z obsługiwanych obrazów maszyn wirtualnych z systemem Linux lub Windows wymienionych w witrynie [Azure Virtual Machines Marketplace][vm_marketplace] lub udostępnić samodzielnie przygotowany obraz niestandardowy.</span><span class="sxs-lookup"><span data-stu-id="0fc76-150">If you specify the virtual machine configuration, you can either specify one of the supported Linux or Windows VM images listed in the [Azure Virtual Machines Marketplace][vm_marketplace], or provide a custom image that you have prepared.</span></span>

<span data-ttu-id="0fc76-151">Po uruchomieniu polecenia **New-AzureBatchPool** należy przekazać ustawienia systemu operacyjnego w obiekcie PSCloudServiceConfiguration lub PSVirtualMachineConfiguration.</span><span class="sxs-lookup"><span data-stu-id="0fc76-151">When you run **New-AzureBatchPool**, pass the operating system settings in a PSCloudServiceConfiguration or PSVirtualMachineConfiguration object.</span></span> <span data-ttu-id="0fc76-152">Na przykład poniższe polecenie cmdlet tworzy nową pulę usługi Batch z małymi węzłami obliczeniowymi w konfiguracji usługi w chmurze i obrazami najnowszej wersji systemu operacyjnego z rodziny 3 (Windows Server 2012).</span><span class="sxs-lookup"><span data-stu-id="0fc76-152">For example, the following cmdlet creates a new Batch pool with size Small compute nodes in the cloud service configuration, imaged with the latest operating system version of family 3 (Windows Server 2012).</span></span> <span data-ttu-id="0fc76-153">W tym miejscu parametr **CloudServiceConfiguration** określa zmienną *$configuration* jako obiekt PSCloudServiceConfiguration.</span><span class="sxs-lookup"><span data-stu-id="0fc76-153">Here, the **CloudServiceConfiguration** parameter specifies the *$configuration* variable as the PSCloudServiceConfiguration object.</span></span> <span data-ttu-id="0fc76-154">Parametr **BatchContext** określa uprzednio zdefiniowaną zmienną *$context* jako obiekt BatchAccountContext.</span><span class="sxs-lookup"><span data-stu-id="0fc76-154">The **BatchContext** parameter specifies a previously defined variable *$context* as the BatchAccountContext object.</span></span>

    $configuration = New-Object -TypeName "Microsoft.Azure.Commands.Batch.Models.PSCloudServiceConfiguration" -ArgumentList @(4,"*")

    New-AzureBatchPool -Id "AutoScalePool" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -AutoScaleFormula '$TargetDedicated=4;' -BatchContext $context

<span data-ttu-id="0fc76-155">Docelowa liczba węzłów obliczeniowych w nowej puli jest określana przez formułę skalowania automatycznego.</span><span class="sxs-lookup"><span data-stu-id="0fc76-155">The target number of compute nodes in the new pool is determined by an autoscaling formula.</span></span> <span data-ttu-id="0fc76-156">W takim przypadku formuła wygląda po prostu w taki sposób — **$TargetDedicated=4**, co oznacza, że liczba węzłów obliczeniowych w puli nie przekracza 4.</span><span class="sxs-lookup"><span data-stu-id="0fc76-156">In this case, the formula is simply **$TargetDedicated=4**, indicating the number of compute nodes in the pool is 4 at most.</span></span>

## <a name="query-for-pools-jobs-tasks-and-other-details"></a><span data-ttu-id="0fc76-157">Zapytania dotyczące puli, zadań, podzadań oraz innych szczegółów</span><span class="sxs-lookup"><span data-stu-id="0fc76-157">Query for pools, jobs, tasks, and other details</span></span>
<span data-ttu-id="0fc76-158">Takie polecenia cmdlet jak **Get-AzureBatchPool**, **Get-AzureBatchJob** oraz **Get-AzureBatchTask** służą do przesyłania zapytań dotyczących jednostek utworzonych w ramach konta usługi Batch.</span><span class="sxs-lookup"><span data-stu-id="0fc76-158">Use cmdlets such as **Get-AzureBatchPool**, **Get-AzureBatchJob**, and **Get-AzureBatchTask** to query for entities created under a Batch account.</span></span>

### <a name="query-for-data"></a><span data-ttu-id="0fc76-159">Zapytania dotyczące danych</span><span class="sxs-lookup"><span data-stu-id="0fc76-159">Query for data</span></span>
<span data-ttu-id="0fc76-160">Przykładowo polecenie **Get-AzureBatchPools** służy do znajdowania pul.</span><span class="sxs-lookup"><span data-stu-id="0fc76-160">As an example, use **Get-AzureBatchPools** to find your pools.</span></span> <span data-ttu-id="0fc76-161">Domyślnie umożliwia to przesłanie zapytań dotyczących wszystkich pul w ramach konta, zakładając, że obiekt BatchAccountContext został już zapisany w zmiennej *$context*:</span><span class="sxs-lookup"><span data-stu-id="0fc76-161">By default this queries for all pools under your account, assuming you already stored the BatchAccountContext object in *$context*:</span></span>

    Get-AzureBatchPool -BatchContext $context

### <a name="use-an-odata-filter"></a><span data-ttu-id="0fc76-162">Korzystanie z filtru OData</span><span class="sxs-lookup"><span data-stu-id="0fc76-162">Use an OData filter</span></span>
<span data-ttu-id="0fc76-163">Można skonfigurować filtr OData przy użyciu parametru **Filtr** w taki sposób, by znajdowane były tylko obiekty, które interesują użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0fc76-163">You can supply an OData filter using the **Filter** parameter to find only the objects you’re interested in.</span></span> <span data-ttu-id="0fc76-164">Np. można znaleźć wszystkie pule z identyfikatorami zaczynającymi się od „myPool”:</span><span class="sxs-lookup"><span data-stu-id="0fc76-164">For example, you can find all pools with ids starting with “myPool”:</span></span>

    $filter = "startswith(id,'myPool')"

    Get-AzureBatchPool -Filter $filter -BatchContext $context

<span data-ttu-id="0fc76-165">Ta metoda nie jest tak elastyczna jak w przypadku korzystania z parametru „Where-Object” w lokalnym potoku.</span><span class="sxs-lookup"><span data-stu-id="0fc76-165">This method is not as flexible as using “Where-Object” in a local pipeline.</span></span> <span data-ttu-id="0fc76-166">Jednak zapytanie zostaje przesłane bezpośrednio do usługi Batch, więc całe filtrowanie odbywa się po stronie serwera, co pozwala na oszczędność przepustowości internetowej.</span><span class="sxs-lookup"><span data-stu-id="0fc76-166">However, the query gets sent to the Batch service directly so that all filtering happens on the server side, saving Internet bandwidth.</span></span>

### <a name="use-the-id-parameter"></a><span data-ttu-id="0fc76-167">Korzystanie z parametru Id</span><span class="sxs-lookup"><span data-stu-id="0fc76-167">Use the Id parameter</span></span>
<span data-ttu-id="0fc76-168">Alternatywą dla filtru OData jest użycie parametru **Id**.</span><span class="sxs-lookup"><span data-stu-id="0fc76-168">An alternative to an OData filter is to use the **Id** parameter.</span></span> <span data-ttu-id="0fc76-169">Aby przesłać zapytanie dotyczące określonej puli o identyfikatorze „myPool”:</span><span class="sxs-lookup"><span data-stu-id="0fc76-169">To query for a specific pool with id "myPool":</span></span>

    Get-AzureBatchPool -Id "myPool" -BatchContext $context

<span data-ttu-id="0fc76-170">Parametr **Id** obsługuje tylko wyszukiwanie pełnych identyfikatorów, a nie symboli wieloznacznych czy filtrów typu OData.</span><span class="sxs-lookup"><span data-stu-id="0fc76-170">The **Id** parameter supports only full-id search, not wildcards or OData-style filters.</span></span>

### <a name="use-the-maxcount-parameter"></a><span data-ttu-id="0fc76-171">Korzystanie z parametru MaxCount</span><span class="sxs-lookup"><span data-stu-id="0fc76-171">Use the MaxCount parameter</span></span>
<span data-ttu-id="0fc76-172">Domyślnie każde polecenie cmdlet zwraca maksymalnie 1000 obiektów.</span><span class="sxs-lookup"><span data-stu-id="0fc76-172">By default, each cmdlet returns a maximum of 1000 objects.</span></span> <span data-ttu-id="0fc76-173">W przypadku osiągnięcia tego limitu zmień ustawienia filtru w taki sposób, aby zwracał mniej obiektów, lub jawnie ustaw wartość maksymalną przy użyciu parametru **MaxCount** (Maksymalna liczba).</span><span class="sxs-lookup"><span data-stu-id="0fc76-173">If you reach this limit, either refine your filter to bring back fewer objects, or explicitly set a maximum using the **MaxCount** parameter.</span></span> <span data-ttu-id="0fc76-174">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="0fc76-174">For example:</span></span>

    Get-AzureBatchTask -MaxCount 2500 -BatchContext $context

<span data-ttu-id="0fc76-175">Aby usunąć górną granicę, ustaw parametr **MaxCount** na wartość 0 lub mniejszą.</span><span class="sxs-lookup"><span data-stu-id="0fc76-175">To remove the upper bound, set **MaxCount** to 0 or less.</span></span>

### <a name="use-the-powershell-pipeline"></a><span data-ttu-id="0fc76-176">Korzystanie z potoku programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="0fc76-176">Use the PowerShell pipeline</span></span>
<span data-ttu-id="0fc76-177">Polecenia cmdlet usługi Batch mogą użyć potoku programu PowerShell do przesyłania danych między poleceniami cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0fc76-177">Batch cmdlets can leverage the PowerShell pipeline to send data between cmdlets.</span></span> <span data-ttu-id="0fc76-178">Powoduje to taki sam skutek co określenie parametru, ale sprawia, że praca z wieloma jednostkami jest łatwiejsza.</span><span class="sxs-lookup"><span data-stu-id="0fc76-178">This has the same effect as specifying a parameter, but makes working with multiple entities easier.</span></span>

<span data-ttu-id="0fc76-179">Na przykład znalezienie i wyświetlenie wszystkich zadań na Twoim koncie:</span><span class="sxs-lookup"><span data-stu-id="0fc76-179">For example, find and display all tasks under your account:</span></span>

    Get-AzureBatchJob -BatchContext $context | Get-AzureBatchTask -BatchContext $context

<span data-ttu-id="0fc76-180">Ponowne uruchomienie (ponowny rozruch) każdego węzła obliczeniowego w puli:</span><span class="sxs-lookup"><span data-stu-id="0fc76-180">Restart (reboot) every compute node in a pool:</span></span>

    Get-AzureBatchComputeNode -PoolId "myPool" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

## <a name="application-package-management"></a><span data-ttu-id="0fc76-181">Zarządzanie pakietem aplikacji</span><span class="sxs-lookup"><span data-stu-id="0fc76-181">Application package management</span></span>
<span data-ttu-id="0fc76-182">Pakiety aplikacji zapewniają uproszczony sposób na wdrażanie aplikacji do węzłów obliczeniowych w pulach.</span><span class="sxs-lookup"><span data-stu-id="0fc76-182">Application packages provide a simplified way to deploy applications to the compute nodes in your pools.</span></span> <span data-ttu-id="0fc76-183">Przy użyciu poleceń cmdlet programu PowerShell usługi Batch możesz przekazywać pakiety aplikacji na swoim koncie usługi Batch i zarządzać nimi oraz wdrażać wersje pakietów do węzłów obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="0fc76-183">With the Batch PowerShell cmdlets, you can upload and manage application packages in your Batch account, and deploy package versions to compute nodes.</span></span>

<span data-ttu-id="0fc76-184">**Tworzenie** aplikacji:</span><span class="sxs-lookup"><span data-stu-id="0fc76-184">**Create** an application:</span></span>

    New-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

<span data-ttu-id="0fc76-185">**Dodawanie** pakietu aplikacji:</span><span class="sxs-lookup"><span data-stu-id="0fc76-185">**Add** an application package:</span></span>

    New-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0" -Format zip -FilePath package001.zip

<span data-ttu-id="0fc76-186">Ustaw **wersję domyślną** aplikacji:</span><span class="sxs-lookup"><span data-stu-id="0fc76-186">Set the **default version** for the application:</span></span>

    Set-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -DefaultVersion "1.0"

<span data-ttu-id="0fc76-187">**Wyświetlanie listy** pakietów aplikacji</span><span class="sxs-lookup"><span data-stu-id="0fc76-187">**List** an application's packages</span></span>

    $application = Get-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

    $application.ApplicationPackages

<span data-ttu-id="0fc76-188">**Usuwanie** pakietu aplikacji</span><span class="sxs-lookup"><span data-stu-id="0fc76-188">**Delete** an application package</span></span>

    Remove-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0"

<span data-ttu-id="0fc76-189">**Usuwanie** aplikacji</span><span class="sxs-lookup"><span data-stu-id="0fc76-189">**Delete** an application</span></span>

    Remove-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

> [!NOTE]
> <span data-ttu-id="0fc76-190">Przed usunięciem aplikacji musisz usunąć wszystkie wersje pakietu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0fc76-190">You must delete all of an application's application package versions before you delete the application.</span></span> <span data-ttu-id="0fc76-191">Jeśli spróbujesz usunąć aplikację, która zawiera obecnie pakiety aplikacji, zostanie wyświetlony komunikat o błędzie „Konflikt”.</span><span class="sxs-lookup"><span data-stu-id="0fc76-191">You will receive a 'Conflict' error if you try to delete an application that currently has application packages.</span></span>
> 
> 

### <a name="deploy-an-application-package"></a><span data-ttu-id="0fc76-192">Wdrażanie pakietu aplikacji</span><span class="sxs-lookup"><span data-stu-id="0fc76-192">Deploy an application package</span></span>
<span data-ttu-id="0fc76-193">Podczas tworzenia puli możesz określić co najmniej jeden pakiet aplikacji dla wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="0fc76-193">You can specify one or more application packages for deployment when you create a pool.</span></span> <span data-ttu-id="0fc76-194">Jeśli określisz pakiet w czasie tworzenia puli, zostanie wdrożony w każdym węźle w przypadku dołączenia węzła do puli.</span><span class="sxs-lookup"><span data-stu-id="0fc76-194">When you specify a package at pool creation time, it is deployed to each node as the node joins pool.</span></span> <span data-ttu-id="0fc76-195">Pakiety są też wdrażane, gdy węzeł zostaje uruchomiony ponownie lub odtworzony z obrazu.</span><span class="sxs-lookup"><span data-stu-id="0fc76-195">Packages are also deployed when a node is rebooted or reimaged.</span></span>

<span data-ttu-id="0fc76-196">Określ opcję `-ApplicationPackageReference` podczas tworzenia puli, aby wdrożyć pakiet aplikacji do węzłów dołączanych do puli.</span><span class="sxs-lookup"><span data-stu-id="0fc76-196">Specify the `-ApplicationPackageReference` option when creating a pool to deploy an application package to the pool's nodes as they join the pool.</span></span> <span data-ttu-id="0fc76-197">Najpierw utwórz obiekt **PSApplicationPackageReference** i skonfiguruj go, używając identyfikatora aplikacji i wersji pakietu, który chcesz wdrożyć do węzłów obliczeniowych puli:</span><span class="sxs-lookup"><span data-stu-id="0fc76-197">First, create a **PSApplicationPackageReference** object, and configure it with the application Id and package version you want to deploy to the pool's compute nodes:</span></span>

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "1.0"

<span data-ttu-id="0fc76-198">Teraz utwórz pulę i określ obiekt odwołania do pakietu jako argument opcji `ApplicationPackageReferences`:</span><span class="sxs-lookup"><span data-stu-id="0fc76-198">Now create the pool, and specify the package reference object as the argument to the `ApplicationPackageReferences` option:</span></span>

    New-AzureBatchPool -Id "PoolWithAppPackage" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -BatchContext $context -ApplicationPackageReferences $appPackageReference

<span data-ttu-id="0fc76-199">Więcej informacji dotyczących pakietów aplikacji można znaleźć w temacie [Deploy applications to compute nodes with Batch application packages (Wdrażanie aplikacji w węzłach obliczeniowych za pomocą pakietów aplikacji usługi Batch)](batch-application-packages.md).</span><span class="sxs-lookup"><span data-stu-id="0fc76-199">You can find more information on application packages in [Deploy applications to compute nodes with Batch application packages](batch-application-packages.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0fc76-200">Najpierw [połącz konto usługi Azure Storage](#linked-storage-account-autostorage) z kontem usługi Batch, aby użyć pakietów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0fc76-200">You must [link an Azure Storage account](#linked-storage-account-autostorage) to your Batch account to use application packages.</span></span>
> 
> 

### <a name="update-a-pools-application-packages"></a><span data-ttu-id="0fc76-201">Aktualizowanie pakietów aplikacji puli</span><span class="sxs-lookup"><span data-stu-id="0fc76-201">Update a pool's application packages</span></span>
<span data-ttu-id="0fc76-202">Aby zaktualizować aplikacje przypisane do istniejącej puli, najpierw utwórz obiekt PSApplicationPackageReference z żądanymi właściwościami (identyfikatorem aplikacji oraz wersją pakietu):</span><span class="sxs-lookup"><span data-stu-id="0fc76-202">To update the applications assigned to an existing pool, first create a PSApplicationPackageReference object with the desired properties (application Id and package version):</span></span>

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "2.0"

<span data-ttu-id="0fc76-203">Następnie pobierz pulę z usługi Batch, wyczyść wszystkie istniejące pakiety, dodaj nasze nowe odwołanie do pakietu i zaktualizuj usługę Batch przy użyciu nowych ustawień puli:</span><span class="sxs-lookup"><span data-stu-id="0fc76-203">Next, get the pool from Batch, clear out any existing packages, add our new package reference, and update the Batch service with the new pool settings:</span></span>

    $pool = Get-AzureBatchPool -BatchContext $context -Id "PoolWithAppPackage"

    $pool.ApplicationPackageReferences.Clear()

    $pool.ApplicationPackageReferences.Add($appPackageReference)

    Set-AzureBatchPool -BatchContext $context -Pool $pool

<span data-ttu-id="0fc76-204">Właściwości puli w usłudze Batch zostały zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="0fc76-204">You've now updated the pool's properties in the Batch service.</span></span> <span data-ttu-id="0fc76-205">Jednak aby rzeczywiście wdrożyć nowy pakiet aplikacji do węzłów obliczeniowych w puli, musisz uruchomić ponownie te węzły lub odtworzyć je z obrazu.</span><span class="sxs-lookup"><span data-stu-id="0fc76-205">To actually deploy the new application package to compute nodes in the pool, however, you must restart or reimage those nodes.</span></span> <span data-ttu-id="0fc76-206">Każdy węzeł w puli możesz uruchomić ponownie za pomocą tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="0fc76-206">You can restart every node in a pool with this command:</span></span>

    Get-AzureBatchComputeNode -PoolId "PoolWithAppPackage" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

> [!TIP]
> <span data-ttu-id="0fc76-207">Do węzłów obliczeniowych w puli możesz wdrożyć wiele pakietów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0fc76-207">You can deploy multiple application packages to the compute nodes in a pool.</span></span> <span data-ttu-id="0fc76-208">Jeśli chcesz *dodać* pakiet aplikacji zamiast zastępowania aktualnie wdrożonych pakietów, pomiń wiersz `$pool.ApplicationPackageReferences.Clear()` powyżej.</span><span class="sxs-lookup"><span data-stu-id="0fc76-208">If you'd like to *add* an application package instead of replacing the currently deployed packages, omit the `$pool.ApplicationPackageReferences.Clear()` line above.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="0fc76-209">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0fc76-209">Next steps</span></span>
* <span data-ttu-id="0fc76-210">Szczegóły składni poleceń cmdlet oraz przykłady znajdują się w [dokumentacji dotyczącej poleceń cmdlet w usłudze Azure Batch](/powershell/module/azurerm.batch/#batch).</span><span class="sxs-lookup"><span data-stu-id="0fc76-210">For detailed cmdlet syntax and examples, see [Azure Batch cmdlet reference](/powershell/module/azurerm.batch/#batch).</span></span>
* <span data-ttu-id="0fc76-211">Aby uzyskać więcej informacji dotyczących aplikacji i pakietów aplikacji w usłudze Batch, zobacz temat [Deploy applications to compute nodes with Batch application packages (Wdrażanie aplikacji w węzłach obliczeniowych za pomocą pakietów aplikacji usługi Batch)](batch-application-packages.md).</span><span class="sxs-lookup"><span data-stu-id="0fc76-211">For more information about applications and application packages in Batch, see [Deploy applications to compute nodes with Batch application packages](batch-application-packages.md).</span></span>

[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/