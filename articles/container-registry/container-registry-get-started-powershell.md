---
title: repozytoria rejestru kontenera aaaAzure | Dokumentacja firmy Microsoft
description: "Jak toouse magazynach rejestru kontenera Azure obrazy usługi Docker"
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
ms.openlocfilehash: 448fb812f537c9502041ce5fb372b0681a9dac4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-powershell"></a><span data-ttu-id="f7f4e-103">Utwórz prywatne rejestru kontenera Docker przy użyciu hello Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f7f4e-103">Create a private Docker container registry using hello Azure PowerShell</span></span>
<span data-ttu-id="f7f4e-104">Używanie poleceń w [programu Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview) toocreate rejestru kontenera i zarządzać jego ustawienia z komputera z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="f7f4e-104">Use commands in [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview) toocreate a container registry and manage its settings from your Windows computer.</span></span> <span data-ttu-id="f7f4e-105">Można również utworzyć i zarządzać nimi za pomocą hello rejestrów kontenera [portalu Azure](container-registry-get-started-portal.md), hello [interfejsu wiersza polecenia Azure](container-registry-get-started-azure-cli.md), lub programowo hello rejestru kontenera [interfejsu API REST](https://go.microsoft.com/fwlink/p/?linkid=834376).</span><span class="sxs-lookup"><span data-stu-id="f7f4e-105">You can also create and manage container registries using hello [Azure portal](container-registry-get-started-portal.md), hello [Azure CLI](container-registry-get-started-azure-cli.md), or programmatically with hello Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span></span>


* <span data-ttu-id="f7f4e-106">Tło i pojęcia dla [hello — omówienie](container-registry-intro.md)</span><span class="sxs-lookup"><span data-stu-id="f7f4e-106">For background and concepts, see [hello overview](container-registry-intro.md)</span></span>
* <span data-ttu-id="f7f4e-107">Aby uzyskać pełną listę obsługiwanych poleceń cmdlet, zobacz [poleceń cmdlet do zarządzania Azure kontenera rejestru](https://docs.microsoft.com/en-us/powershell/module/azurerm.containerregistry/).</span><span class="sxs-lookup"><span data-stu-id="f7f4e-107">For a full list of supported cmdlets, see [Azure Container Registry Management Cmdlets](https://docs.microsoft.com/en-us/powershell/module/azurerm.containerregistry/).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="f7f4e-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f7f4e-108">Prerequisites</span></span>
* <span data-ttu-id="f7f4e-109">**Program Azure PowerShell**: tooinstall i rozpocząć pracę z programem Azure PowerShell, zobacz hello [instrukcje dotyczące instalacji](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="f7f4e-109">**Azure PowerShell**: tooinstall and get started with Azure PowerShell, see hello [installation instructions](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="f7f4e-110">Zaloguj się za tooyour subskrypcji platformy Azure, uruchamiając `Login-AzureRMAccount`.</span><span class="sxs-lookup"><span data-stu-id="f7f4e-110">Log in tooyour Azure subscription by running `Login-AzureRMAccount`.</span></span> <span data-ttu-id="f7f4e-111">Aby uzyskać więcej informacji, zobacz [wprowadzenie do programu Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azurep).</span><span class="sxs-lookup"><span data-stu-id="f7f4e-111">For more information, see [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azurep).</span></span>
* <span data-ttu-id="f7f4e-112">**Grupa zasobów**: utwórz [grupę zasobów](../azure-resource-manager/resource-group-overview.md#resource-groups) przed utworzeniem rejestru kontenerów lub użyj istniejącej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="f7f4e-112">**Resource group**: Create a [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) before creating a container registry, or use an existing resource group.</span></span> <span data-ttu-id="f7f4e-113">Upewnij się, że grupa zasobów hello znajduje się w lokalizacji hello usługa Rejestr kontenera [dostępne](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="f7f4e-113">Make sure hello resource group is in a location where hello Container Registry service is [available](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="f7f4e-114">toocreate grupę zasobów, przy użyciu programu Azure PowerShell, zobacz [hello w programie PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps#create-a-resource-group).</span><span class="sxs-lookup"><span data-stu-id="f7f4e-114">toocreate a resource group using Azure PowerShell, see [hello PowerShell reference](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps#create-a-resource-group).</span></span>
* <span data-ttu-id="f7f4e-115">**Konto magazynu** (opcjonalnie): Utwórz standardowy Azure [konta magazynu](../storage/common/storage-introduction.md) tooback hello kontener klucza rejestru hello tej samej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="f7f4e-115">**Storage account** (optional): Create a standard Azure [storage account](../storage/common/storage-introduction.md) tooback hello container registry in hello same location.</span></span> <span data-ttu-id="f7f4e-116">Jeśli nie określisz konta magazynu podczas tworzenia rejestru z `New-AzureRMContainerRegistry`, hello polecenie tworzy go dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="f7f4e-116">If you don't specify a storage account when creating a registry with `New-AzureRMContainerRegistry`, hello command creates one for you.</span></span> <span data-ttu-id="f7f4e-117">toocreate magazynu konta za pomocą programu PowerShell, zobacz [hello w programie PowerShell](https://docs.microsoft.com/en-us/powershell/module/azure/new-azurestorageaccount).</span><span class="sxs-lookup"><span data-stu-id="f7f4e-117">toocreate a storage account using PowerShell, see [hello PowerShell reference](https://docs.microsoft.com/en-us/powershell/module/azure/new-azurestorageaccount).</span></span> <span data-ttu-id="f7f4e-118">Usługa Premium Storage nie jest obecnie obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="f7f4e-118">Currently Premium Storage is not supported.</span></span>
* <span data-ttu-id="f7f4e-119">**Nazwy głównej usługi** (opcjonalnie): podczas tworzenia rejestru przy użyciu programu PowerShell, domyślnie go nie ustawiono dostępu.</span><span class="sxs-lookup"><span data-stu-id="f7f4e-119">**Service principal** (optional): When you create a registry with PowerShell, by default it is not set up for access.</span></span> <span data-ttu-id="f7f4e-120">W zależności od potrzeb możesz przypisać istniejący Rejestr tooa główną usługi Azure Active Directory lub Utwórz i Przypisz nowy.</span><span class="sxs-lookup"><span data-stu-id="f7f4e-120">Depending on your needs, you can assign an existing Azure Active Directory service principal tooa registry or create and assign a new one.</span></span> <span data-ttu-id="f7f4e-121">Alternatywnie można włączyć rejestru hello konta administratora.</span><span class="sxs-lookup"><span data-stu-id="f7f4e-121">Alternatively, you can enable hello registry's admin user account.</span></span> <span data-ttu-id="f7f4e-122">Zobacz hello sekcje w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="f7f4e-122">See hello sections later in this article.</span></span> <span data-ttu-id="f7f4e-123">Aby uzyskać więcej informacji na temat dostępu do rejestru, zobacz [Uwierzytelnij z rejestru kontenera hello](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="f7f4e-123">For more information about registry access, see [Authenticate with hello container registry](container-registry-authentication.md).</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="f7f4e-124">Tworzenie rejestru kontenerów</span><span class="sxs-lookup"><span data-stu-id="f7f4e-124">Create a container registry</span></span>
<span data-ttu-id="f7f4e-125">Uruchom hello `New-AzureRMContainerRegistry` toocreate polecenia rejestru kontenera.</span><span class="sxs-lookup"><span data-stu-id="f7f4e-125">Run hello `New-AzureRMContainerRegistry` command toocreate a container registry.</span></span>

> [!TIP]
> <span data-ttu-id="f7f4e-126">Podczas tworzenia rejestru określ globalnie unikatową nazwę domeny najwyższego poziomu, która będzie zawierać tylko litery i cyfry.</span><span class="sxs-lookup"><span data-stu-id="f7f4e-126">When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers.</span></span> <span data-ttu-id="f7f4e-127">Nazwa rejestru Hello w przykładach hello jest `MyRegistry`, ale podstawić własną unikatową nazwę.</span><span class="sxs-lookup"><span data-stu-id="f7f4e-127">hello registry name in hello examples is `MyRegistry`, but substitute a unique name of your own.</span></span>
>
>

<span data-ttu-id="f7f4e-128">Witaj następujące polecenia używa hello minimalnego parametry toocreate kontenera rejestru `MyRegistry` w grupie zasobów hello `MyResourceGroup` w hello lokalizacji południowo-środkowe stany:</span><span class="sxs-lookup"><span data-stu-id="f7f4e-128">hello following command uses hello minimal parameters toocreate container registry `MyRegistry` in hello resource group `MyResourceGroup` in hello South Central US location:</span></span>

```PowerShell
$Registry = New-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

* <span data-ttu-id="f7f4e-129">Parametr `-StorageAccountName` jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="f7f4e-129">`-StorageAccountName` is optional.</span></span> <span data-ttu-id="f7f4e-130">Jeśli nie jest określony, konto magazynu jest tworzony z nazwą składającą się z nazwy rejestru hello i sygnaturę czasową w hello określonej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="f7f4e-130">If not specified, a storage account is created with a name consisting of hello registry name and a timestamp in hello specified resource group.</span></span>

## <a name="assign-a-service-principal"></a><span data-ttu-id="f7f4e-131">Przypisywanie nazwy głównej usługi</span><span class="sxs-lookup"><span data-stu-id="f7f4e-131">Assign a service principal</span></span>
<span data-ttu-id="f7f4e-132">Użyj tooassign poleceń programu PowerShell usługi Azure Active Directory [nazwy głównej usługi](../azure-resource-manager/resource-group-authenticate-service-principal.md) tooa rejestru.</span><span class="sxs-lookup"><span data-stu-id="f7f4e-132">Use PowerShell commands tooassign an Azure Active Directory [service principal](../azure-resource-manager/resource-group-authenticate-service-principal.md) tooa registry.</span></span> <span data-ttu-id="f7f4e-133">Witaj nazwy głównej usługi w tych przykładach przypisany hello właściciela roli, ale można przypisać [innych ról](../active-directory/role-based-access-control-configure.md) Jeśli chcesz.</span><span class="sxs-lookup"><span data-stu-id="f7f4e-133">hello service principal in these examples is assigned hello Owner role, but you can assign [other roles](../active-directory/role-based-access-control-configure.md) if you want.</span></span>

### <a name="create-a-service-principal"></a><span data-ttu-id="f7f4e-134">Tworzenie nazwy głównej usługi</span><span class="sxs-lookup"><span data-stu-id="f7f4e-134">Create a service principal</span></span>
<span data-ttu-id="f7f4e-135">W hello następujące polecenia utworzono nową główną nazwę usługi.</span><span class="sxs-lookup"><span data-stu-id="f7f4e-135">In hello following command, a new service principal is created.</span></span> <span data-ttu-id="f7f4e-136">Określ silne hasło z hello `-Password` parametru.</span><span class="sxs-lookup"><span data-stu-id="f7f4e-136">Specify a strong password with hello `-Password` parameter.</span></span>

```PowerShell
$ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName ApplicationDisplayName -Password "MyPassword"
```

### <a name="assign-a-new-or-existing-service-principal"></a><span data-ttu-id="f7f4e-137">Przypisanie nazwy głównej usługi nowego lub istniejącego</span><span class="sxs-lookup"><span data-stu-id="f7f4e-137">Assign a new or existing service principal</span></span>
<span data-ttu-id="f7f4e-138">Można przypisać nowej lub istniejącej rejestr tooa główną usługi.</span><span class="sxs-lookup"><span data-stu-id="f7f4e-138">You can assign a new or an existing service principal tooa registry.</span></span> <span data-ttu-id="f7f4e-139">tooassign jej właściciela roli dostępu toohello rejestru, uruchom polecenie toohello podobne, poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="f7f4e-139">tooassign it Owner role access toohello registry, run a command similar toohello following example:</span></span>

```PowerShell
New-AzureRMRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Registry.Id
```

##<a name="sign-in-toohello-registry-with-hello-service-principal"></a><span data-ttu-id="f7f4e-140">Zaloguj się w rejestrze toohello hello nazwy głównej usługi</span><span class="sxs-lookup"><span data-stu-id="f7f4e-140">Sign in toohello registry with hello service principal</span></span>
<span data-ttu-id="f7f4e-141">Po przypisaniu rejestr toohello główna usługi hello, musisz zalogować się przy użyciu hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="f7f4e-141">After assigning hello service principal toohello registry, you can sign in using hello following command:</span></span>

```PowerShell
docker login -u $ServicePrincipal.ApplicationId -p myPassword
```

## <a name="manage-admin-credentials"></a><span data-ttu-id="f7f4e-142">Zarządzanie poświadczeniami administratora</span><span class="sxs-lookup"><span data-stu-id="f7f4e-142">Manage admin credentials</span></span>
<span data-ttu-id="f7f4e-143">Konto administratora jest automatycznie tworzone dla każdego rejestru kontenera i jest domyślnie wyłączone.</span><span class="sxs-lookup"><span data-stu-id="f7f4e-143">An admin account is automatically created for each container registry and is disabled by default.</span></span> <span data-ttu-id="f7f4e-144">Witaj poniższe przykłady przedstawiają poleceń programu PowerShell poświadczenia administratora hello toomanage rejestru kontenera.</span><span class="sxs-lookup"><span data-stu-id="f7f4e-144">hello following examples show PowerShell commands toomanage hello admin credentials for your container registry.</span></span>

### <a name="obtain-admin-user-credentials"></a><span data-ttu-id="f7f4e-145">Uzyskiwanie poświadczeń użytkownika administratora</span><span class="sxs-lookup"><span data-stu-id="f7f4e-145">Obtain admin user credentials</span></span>
```PowerShell
Get-AzureRMContainerRegistryCredential -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

### <a name="enable-admin-user-for-an-existing-registry"></a><span data-ttu-id="f7f4e-146">Włączanie użytkownika administratora dla istniejącego rejestru</span><span class="sxs-lookup"><span data-stu-id="f7f4e-146">Enable admin user for an existing registry</span></span>
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -EnableAdminUser
```

### <a name="disable-admin-user-for-an-existing-registry"></a><span data-ttu-id="f7f4e-147">Wyłączanie użytkownika administratora dla istniejącego rejestru</span><span class="sxs-lookup"><span data-stu-id="f7f4e-147">Disable admin user for an existing registry</span></span>
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -DisableAdminUser
```

## <a name="next-steps"></a><span data-ttu-id="f7f4e-148">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f7f4e-148">Next steps</span></span>
* [<span data-ttu-id="f7f4e-149">Pierwszy obraz przy użyciu interfejsu wiersza polecenia Docker hello push</span><span class="sxs-lookup"><span data-stu-id="f7f4e-149">Push your first image using hello Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
