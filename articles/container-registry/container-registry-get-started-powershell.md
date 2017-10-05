---
title: Repozytoria rejestru kontenera platformy Azure | Dokumentacja firmy Microsoft
description: "Jak używać repozytoria rejestru kontenera Azure obrazy usługi Docker"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/30/2017
ms.author: cristyg
ms.openlocfilehash: 1e5d5ea5b1ec121fe008abc48178b1d58f540ce1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-private-docker-container-registry-using-the-azure-powershell"></a><span data-ttu-id="ad425-103">Utwórz prywatne rejestru kontenera Docker przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ad425-103">Create a private Docker container registry using the Azure PowerShell</span></span>
<span data-ttu-id="ad425-104">Używanie poleceń w [programu Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview) Tworzenie rejestru kontenera i zarządzanie nimi jego ustawienia z komputera z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="ad425-104">Use commands in [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview) to create a container registry and manage its settings from your Windows computer.</span></span> <span data-ttu-id="ad425-105">Można również tworzyć i zarządzać przy użyciu rejestrów kontenera [portalu Azure](container-registry-get-started-portal.md), [interfejsu wiersza polecenia Azure](container-registry-get-started-azure-cli.md), lub programowo z rejestru kontenera [interfejsu API REST](https://go.microsoft.com/fwlink/p/?linkid=834376).</span><span class="sxs-lookup"><span data-stu-id="ad425-105">You can also create and manage container registries using the [Azure portal](container-registry-get-started-portal.md), the [Azure CLI](container-registry-get-started-azure-cli.md), or programmatically with the Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span></span>


* <span data-ttu-id="ad425-106">Podstawy oraz pojęcia zostały przedstawione w części [ — omówienie](container-registry-intro.md)</span><span class="sxs-lookup"><span data-stu-id="ad425-106">For background and concepts, see [the overview](container-registry-intro.md)</span></span>
* <span data-ttu-id="ad425-107">Aby uzyskać pełną listę obsługiwanych poleceń cmdlet, zobacz [poleceń cmdlet do zarządzania Azure kontenera rejestru](https://docs.microsoft.com/en-us/powershell/module/azurerm.containerregistry/).</span><span class="sxs-lookup"><span data-stu-id="ad425-107">For a full list of supported cmdlets, see [Azure Container Registry Management Cmdlets](https://docs.microsoft.com/en-us/powershell/module/azurerm.containerregistry/).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="ad425-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ad425-108">Prerequisites</span></span>
* <span data-ttu-id="ad425-109">**Program Azure PowerShell**: Aby zainstalować i rozpocząć pracę z programem Azure PowerShell, zobacz [instrukcje dotyczące instalacji](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="ad425-109">**Azure PowerShell**: To install and get started with Azure PowerShell, see the [installation instructions](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="ad425-110">Zaloguj się do subskrypcji platformy Azure, uruchamiając polecenie `Login-AzureRMAccount`.</span><span class="sxs-lookup"><span data-stu-id="ad425-110">Log in to your Azure subscription by running `Login-AzureRMAccount`.</span></span> <span data-ttu-id="ad425-111">Aby uzyskać więcej informacji, zobacz [wprowadzenie do programu Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azurep).</span><span class="sxs-lookup"><span data-stu-id="ad425-111">For more information, see [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azurep).</span></span>
* <span data-ttu-id="ad425-112">**Grupa zasobów**: utwórz [grupę zasobów](../azure-resource-manager/resource-group-overview.md#resource-groups) przed utworzeniem rejestru kontenerów lub użyj istniejącej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="ad425-112">**Resource group**: Create a [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) before creating a container registry, or use an existing resource group.</span></span> <span data-ttu-id="ad425-113">Upewnij się, że grupa zasobów znajduje się w lokalizacji, w której usługa Container Registry jest [dostępna](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="ad425-113">Make sure the resource group is in a location where the Container Registry service is [available](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="ad425-114">Aby utworzyć grupę zasobów, przy użyciu programu Azure PowerShell, zobacz [dokumentacji programu PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps#create-a-resource-group).</span><span class="sxs-lookup"><span data-stu-id="ad425-114">To create a resource group using Azure PowerShell, see [the PowerShell reference](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps#create-a-resource-group).</span></span>
* <span data-ttu-id="ad425-115">**Konto magazynu** (opcjonalnie): utwórz standardowe [konto magazynu](../storage/common/storage-introduction.md) platformy Azure, aby obsługiwać rejestr kontenerów w tej samej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="ad425-115">**Storage account** (optional): Create a standard Azure [storage account](../storage/common/storage-introduction.md) to back the container registry in the same location.</span></span> <span data-ttu-id="ad425-116">Jeśli nie określisz konta magazynu podczas tworzenia rejestru przy użyciu polecenia `New-AzureRMContainerRegistry`, polecenie spowoduje utworzenie go dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="ad425-116">If you don't specify a storage account when creating a registry with `New-AzureRMContainerRegistry`, the command creates one for you.</span></span> <span data-ttu-id="ad425-117">Aby utworzyć konto magazynu przy użyciu programu PowerShell, zobacz [dokumentacji programu PowerShell](https://docs.microsoft.com/en-us/powershell/module/azure/new-azurestorageaccount).</span><span class="sxs-lookup"><span data-stu-id="ad425-117">To create a storage account using PowerShell, see [the PowerShell reference](https://docs.microsoft.com/en-us/powershell/module/azure/new-azurestorageaccount).</span></span> <span data-ttu-id="ad425-118">Usługa Premium Storage nie jest obecnie obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="ad425-118">Currently Premium Storage is not supported.</span></span>
* <span data-ttu-id="ad425-119">**Nazwy głównej usługi** (opcjonalnie): podczas tworzenia rejestru przy użyciu programu PowerShell, domyślnie go nie ustawiono dostępu.</span><span class="sxs-lookup"><span data-stu-id="ad425-119">**Service principal** (optional): When you create a registry with PowerShell, by default it is not set up for access.</span></span> <span data-ttu-id="ad425-120">W zależności od potrzeb można przypisać istniejącej nazwy głównej usługi Azure Active Directory do rejestru lub Utwórz i przypisz nowe.</span><span class="sxs-lookup"><span data-stu-id="ad425-120">Depending on your needs, you can assign an existing Azure Active Directory service principal to a registry or create and assign a new one.</span></span> <span data-ttu-id="ad425-121">Alternatywnie można włączyć konta administratora w rejestrze.</span><span class="sxs-lookup"><span data-stu-id="ad425-121">Alternatively, you can enable the registry's admin user account.</span></span> <span data-ttu-id="ad425-122">Zobacz sekcje w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="ad425-122">See the sections later in this article.</span></span> <span data-ttu-id="ad425-123">Więcej informacji dotyczących dostępu do rejestru znajduje się w temacie [Authenticate with a container registry](container-registry-authentication.md) (Uwierzytelnianie za pomocą rejestru kontenera).</span><span class="sxs-lookup"><span data-stu-id="ad425-123">For more information about registry access, see [Authenticate with the container registry](container-registry-authentication.md).</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="ad425-124">Tworzenie rejestru kontenerów</span><span class="sxs-lookup"><span data-stu-id="ad425-124">Create a container registry</span></span>
<span data-ttu-id="ad425-125">Uruchom polecenie `New-AzureRMContainerRegistry`, aby utworzyć rejestr kontenera.</span><span class="sxs-lookup"><span data-stu-id="ad425-125">Run the `New-AzureRMContainerRegistry` command to create a container registry.</span></span>

> [!TIP]
> <span data-ttu-id="ad425-126">Podczas tworzenia rejestru określ globalnie unikatową nazwę domeny najwyższego poziomu, która będzie zawierać tylko litery i cyfry.</span><span class="sxs-lookup"><span data-stu-id="ad425-126">When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers.</span></span> <span data-ttu-id="ad425-127">W przykładach nazwa rejestru to `MyRegistry`, ale możesz ją zastąpić własną, unikatową nazwą.</span><span class="sxs-lookup"><span data-stu-id="ad425-127">The registry name in the examples is `MyRegistry`, but substitute a unique name of your own.</span></span>
>
>

<span data-ttu-id="ad425-128">Następujące polecenie używa minimalnej liczby parametrów do utworzenia kontenera rejestru `MyRegistry` w grupie zasobów `MyResourceGroup` w lokalizacji Południowo-środkowe stany USA:</span><span class="sxs-lookup"><span data-stu-id="ad425-128">The following command uses the minimal parameters to create container registry `MyRegistry` in the resource group `MyResourceGroup` in the South Central US location:</span></span>

```PowerShell
$Registry = New-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

* <span data-ttu-id="ad425-129">Parametr `-StorageAccountName` jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="ad425-129">`-StorageAccountName` is optional.</span></span> <span data-ttu-id="ad425-130">Jeśli nie określono inaczej, nazwa konta magazynu utworzonego we wskazanej grupie zasobów składa się z nazwy rejestru i sygnatury czasowej.</span><span class="sxs-lookup"><span data-stu-id="ad425-130">If not specified, a storage account is created with a name consisting of the registry name and a timestamp in the specified resource group.</span></span>

## <a name="assign-a-service-principal"></a><span data-ttu-id="ad425-131">Przypisywanie nazwy głównej usługi</span><span class="sxs-lookup"><span data-stu-id="ad425-131">Assign a service principal</span></span>
<span data-ttu-id="ad425-132">Przypisz usługi Azure Active Directory za pomocą poleceń programu PowerShell [nazwy głównej usługi](../azure-resource-manager/resource-group-authenticate-service-principal.md) rejestru.</span><span class="sxs-lookup"><span data-stu-id="ad425-132">Use PowerShell commands to assign an Azure Active Directory [service principal](../azure-resource-manager/resource-group-authenticate-service-principal.md) to a registry.</span></span> <span data-ttu-id="ad425-133">W tych przykładach do nazwy głównej usługi przypisano rolę Właściciel, ale możesz przypisywać [inne role](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="ad425-133">The service principal in these examples is assigned the Owner role, but you can assign [other roles](../active-directory/role-based-access-control-configure.md) if you want.</span></span>

### <a name="create-a-service-principal"></a><span data-ttu-id="ad425-134">Tworzenie nazwy głównej usługi</span><span class="sxs-lookup"><span data-stu-id="ad425-134">Create a service principal</span></span>
<span data-ttu-id="ad425-135">W poniższym poleceniu utworzono nową główną nazwę usługi.</span><span class="sxs-lookup"><span data-stu-id="ad425-135">In the following command, a new service principal is created.</span></span> <span data-ttu-id="ad425-136">Określ silne hasło przy użyciu parametru `-Password`.</span><span class="sxs-lookup"><span data-stu-id="ad425-136">Specify a strong password with the `-Password` parameter.</span></span>

```PowerShell
$ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName ApplicationDisplayName -Password "MyPassword"
```

### <a name="assign-a-new-or-existing-service-principal"></a><span data-ttu-id="ad425-137">Przypisanie nazwy głównej usługi nowego lub istniejącego</span><span class="sxs-lookup"><span data-stu-id="ad425-137">Assign a new or existing service principal</span></span>
<span data-ttu-id="ad425-138">Nowej lub istniejącej nazwy głównej usługi można przypisać do rejestru.</span><span class="sxs-lookup"><span data-stu-id="ad425-138">You can assign a new or an existing service principal to a registry.</span></span> <span data-ttu-id="ad425-139">Aby przypisać właściciela roli dostępu do rejestru, uruchom polecenie podobne do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="ad425-139">To assign it Owner role access to the registry, run a command similar to the following example:</span></span>

```PowerShell
New-AzureRMRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Registry.Id
```

##<a name="sign-in-to-the-registry-with-the-service-principal"></a><span data-ttu-id="ad425-140">Zaloguj się w rejestrze z nazwy głównej usługi</span><span class="sxs-lookup"><span data-stu-id="ad425-140">Sign in to the registry with the service principal</span></span>
<span data-ttu-id="ad425-141">Po przypisaniu nazwy głównej usługi w rejestrze, należy zalogować się przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="ad425-141">After assigning the service principal to the registry, you can sign in using the following command:</span></span>

```PowerShell
docker login -u $ServicePrincipal.ApplicationId -p myPassword
```

## <a name="manage-admin-credentials"></a><span data-ttu-id="ad425-142">Zarządzanie poświadczeniami administratora</span><span class="sxs-lookup"><span data-stu-id="ad425-142">Manage admin credentials</span></span>
<span data-ttu-id="ad425-143">Konto administratora jest automatycznie tworzone dla każdego rejestru kontenera i jest domyślnie wyłączone.</span><span class="sxs-lookup"><span data-stu-id="ad425-143">An admin account is automatically created for each container registry and is disabled by default.</span></span> <span data-ttu-id="ad425-144">Poniżej przedstawiono polecenia programu PowerShell do zarządzania poświadczeń administratora dla kontenera rejestru.</span><span class="sxs-lookup"><span data-stu-id="ad425-144">The following examples show PowerShell commands to manage the admin credentials for your container registry.</span></span>

### <a name="obtain-admin-user-credentials"></a><span data-ttu-id="ad425-145">Uzyskiwanie poświadczeń użytkownika administratora</span><span class="sxs-lookup"><span data-stu-id="ad425-145">Obtain admin user credentials</span></span>
```PowerShell
Get-AzureRMContainerRegistryCredential -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

### <a name="enable-admin-user-for-an-existing-registry"></a><span data-ttu-id="ad425-146">Włączanie użytkownika administratora dla istniejącego rejestru</span><span class="sxs-lookup"><span data-stu-id="ad425-146">Enable admin user for an existing registry</span></span>
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -EnableAdminUser
```

### <a name="disable-admin-user-for-an-existing-registry"></a><span data-ttu-id="ad425-147">Wyłączanie użytkownika administratora dla istniejącego rejestru</span><span class="sxs-lookup"><span data-stu-id="ad425-147">Disable admin user for an existing registry</span></span>
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -DisableAdminUser
```

## <a name="next-steps"></a><span data-ttu-id="ad425-148">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ad425-148">Next steps</span></span>
* <span data-ttu-id="ad425-149">[Push your first image using the Docker CLI](container-registry-get-started-docker-cli.md) (Wypychanie pierwszego obrazu za pomocą interfejsu wiersza polecenia platformy Docker)</span><span class="sxs-lookup"><span data-stu-id="ad425-149">[Push your first image using the Docker CLI](container-registry-get-started-docker-cli.md)</span></span>
