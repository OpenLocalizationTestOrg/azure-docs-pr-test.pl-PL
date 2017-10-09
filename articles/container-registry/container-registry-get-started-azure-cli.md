---
title: aaaCreate prywatnej rejestru kontenera Docker - wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft
description: "Rozpocząć tworzenie i zarządzanie nimi prywatnej rejestrów kontenera Docker z hello Azure CLI 2.0"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 29e20d75-bf39-4f7d-815f-a2e47209be7d
ms.service: container-registry
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/06/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f0d876a70b71a5e1bd564fbc9198f693dfe8a347
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-cli-20"></a><span data-ttu-id="0c83c-103">Utwórz prywatne rejestru kontenera Docker przy użyciu hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0c83c-103">Create a private Docker container registry using hello Azure CLI 2.0</span></span>
<span data-ttu-id="0c83c-104">Używanie poleceń w hello [Azure CLI 2.0](https://github.com/Azure/azure-cli) toocreate rejestru kontenera i zarządzać jego ustawienia z komputera z systemem Linux, Mac lub Windows.</span><span class="sxs-lookup"><span data-stu-id="0c83c-104">Use commands in hello [Azure CLI 2.0](https://github.com/Azure/azure-cli) toocreate a container registry and manage its settings from your Linux, Mac, or Windows computer.</span></span> <span data-ttu-id="0c83c-105">Można również utworzyć i zarządzać nimi za pomocą hello rejestrów kontenera [portalu Azure](container-registry-get-started-portal.md) lub programowo hello rejestru kontenera [interfejsu API REST](https://go.microsoft.com/fwlink/p/?linkid=834376).</span><span class="sxs-lookup"><span data-stu-id="0c83c-105">You can also create and manage container registries using hello [Azure portal](container-registry-get-started-portal.md) or programmatically with hello Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span></span>


* <span data-ttu-id="0c83c-106">Tło i pojęcia dla [hello — omówienie](container-registry-intro.md)</span><span class="sxs-lookup"><span data-stu-id="0c83c-106">For background and concepts, see [hello overview](container-registry-intro.md)</span></span>
* <span data-ttu-id="0c83c-107">Aby uzyskać pomoc dotyczącą polecenia interfejsu wiersza polecenia kontenera rejestru (`az acr` poleceń), Przekaż hello `-h` polecenia tooany parametru.</span><span class="sxs-lookup"><span data-stu-id="0c83c-107">For help on Container Registry CLI commands (`az acr` commands), pass hello `-h` parameter tooany command.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="0c83c-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="0c83c-108">Prerequisites</span></span>
* <span data-ttu-id="0c83c-109">**Azure CLI 2.0**: tooinstall i rozpoczynanie pracy z hello 2.0 interfejsu wiersza polecenia, zobacz hello [instrukcje dotyczące instalacji](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="0c83c-109">**Azure CLI 2.0**: tooinstall and get started with hello CLI 2.0, see hello [installation instructions](/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="0c83c-110">Zaloguj się za tooyour subskrypcji platformy Azure, uruchamiając `az login`.</span><span class="sxs-lookup"><span data-stu-id="0c83c-110">Log in tooyour Azure subscription by running `az login`.</span></span> <span data-ttu-id="0c83c-111">Aby uzyskać więcej informacji, zobacz [wprowadzenie hello 2.0 interfejsu wiersza polecenia](/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="0c83c-111">For more information, see [Get started with hello CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>
* <span data-ttu-id="0c83c-112">**Grupa zasobów**: utwórz [grupę zasobów](../azure-resource-manager/resource-group-overview.md#resource-groups) przed utworzeniem rejestru kontenerów lub użyj istniejącej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="0c83c-112">**Resource group**: Create a [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) before creating a container registry, or use an existing resource group.</span></span> <span data-ttu-id="0c83c-113">Upewnij się, że grupa zasobów hello znajduje się w lokalizacji hello usługa Rejestr kontenera [dostępne](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="0c83c-113">Make sure hello resource group is in a location where hello Container Registry service is [available](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="0c83c-114">grupy zasobów przy użyciu toocreate hello 2.0 interfejsu wiersza polecenia, zobacz [hello odwołanie 2.0 interfejsu wiersza polecenia](/cli/azure/group).</span><span class="sxs-lookup"><span data-stu-id="0c83c-114">toocreate a resource group using hello CLI 2.0, see [hello CLI 2.0 reference](/cli/azure/group).</span></span>
* <span data-ttu-id="0c83c-115">**Konto magazynu** (opcjonalnie): Utwórz standardowy Azure [konta magazynu](../storage/common/storage-introduction.md) tooback hello kontener klucza rejestru hello tej samej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="0c83c-115">**Storage account** (optional): Create a standard Azure [storage account](../storage/common/storage-introduction.md) tooback hello container registry in hello same location.</span></span> <span data-ttu-id="0c83c-116">Jeśli nie określisz konta magazynu podczas tworzenia rejestru z `az acr create`, hello polecenie tworzy go dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="0c83c-116">If you don't specify a storage account when creating a registry with `az acr create`, hello command creates one for you.</span></span> <span data-ttu-id="0c83c-117">toocreate przy użyciu konta magazynu hello 2.0 interfejsu wiersza polecenia, zobacz [hello odwołanie 2.0 interfejsu wiersza polecenia](/cli/azure/storage/account).</span><span class="sxs-lookup"><span data-stu-id="0c83c-117">toocreate a storage account using hello CLI 2.0, see [hello CLI 2.0 reference](/cli/azure/storage/account).</span></span> <span data-ttu-id="0c83c-118">Usługa Premium Storage nie jest obecnie obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="0c83c-118">Currently Premium Storage is not supported.</span></span>
* <span data-ttu-id="0c83c-119">**Nazwy głównej usługi** (opcjonalnie): podczas tworzenia rejestru hello interfejsu wiersza polecenia, po domyślnie go nie ustawiono dostępu.</span><span class="sxs-lookup"><span data-stu-id="0c83c-119">**Service principal** (optional): When you create a registry with hello CLI, by default it is not set up for access.</span></span> <span data-ttu-id="0c83c-120">W zależności od potrzeb, możesz przypisać istniejący Rejestr tooa główną usługi Azure Active Directory (lub Utwórz i Przypisz nowy), lub Włącz rejestru hello konta administratora.</span><span class="sxs-lookup"><span data-stu-id="0c83c-120">Depending on your needs, you can assign an existing Azure Active Directory service principal tooa registry (or create and assign a new one), or enable hello registry's admin user account.</span></span> <span data-ttu-id="0c83c-121">Zobacz hello sekcje w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="0c83c-121">See hello sections later in this article.</span></span> <span data-ttu-id="0c83c-122">Aby uzyskać więcej informacji na temat dostępu do rejestru, zobacz [Uwierzytelnij z rejestru kontenera hello](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="0c83c-122">For more information about registry access, see [Authenticate with hello container registry](container-registry-authentication.md).</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="0c83c-123">Tworzenie rejestru kontenerów</span><span class="sxs-lookup"><span data-stu-id="0c83c-123">Create a container registry</span></span>
<span data-ttu-id="0c83c-124">Uruchom hello `az acr create` toocreate polecenia rejestru kontenera.</span><span class="sxs-lookup"><span data-stu-id="0c83c-124">Run hello `az acr create` command toocreate a container registry.</span></span>

> [!TIP]
> <span data-ttu-id="0c83c-125">Podczas tworzenia rejestru określ globalnie unikatową nazwę domeny najwyższego poziomu, która będzie zawierać tylko litery i cyfry.</span><span class="sxs-lookup"><span data-stu-id="0c83c-125">When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers.</span></span> <span data-ttu-id="0c83c-126">Nazwa rejestru Hello w przykładach hello jest `myRegistry1`, ale podstawić własną unikatową nazwę.</span><span class="sxs-lookup"><span data-stu-id="0c83c-126">hello registry name in hello examples is `myRegistry1`, but substitute a unique name of your own.</span></span>
>
>

<span data-ttu-id="0c83c-127">Witaj następujące polecenia używa hello minimalnego parametry toocreate kontenera rejestru `myRegistry1` w grupie zasobów hello `myResourceGroup`i przy użyciu hello *podstawowe* sku:</span><span class="sxs-lookup"><span data-stu-id="0c83c-127">hello following command uses hello minimal parameters toocreate container registry `myRegistry1` in hello resource group `myResourceGroup`, and using hello *Basic* sku:</span></span>

```azurecli
az acr create --name myRegistry1 --resource-group myResourceGroup --sku Basic
```

* <span data-ttu-id="0c83c-128">Parametr `--storage-account-name` jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="0c83c-128">`--storage-account-name` is optional.</span></span> <span data-ttu-id="0c83c-129">Jeśli nie jest określony, konto magazynu jest tworzony z nazwą składającą się z nazwy rejestru hello i sygnaturę czasową w hello określonej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="0c83c-129">If not specified, a storage account is created with a name consisting of hello registry name and a timestamp in hello specified resource group.</span></span>

<span data-ttu-id="0c83c-130">Po utworzeniu rejestru hello dane wyjściowe hello jest podobne toohello następujące:</span><span class="sxs-lookup"><span data-stu-id="0c83c-130">When hello registry is created, hello output is similar toohello following:</span></span>

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-06T18:36:29.124842+00:00",
  "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myResourceGroup/providers/Microsoft.ContainerRegistry
/registries/myRegistry1",
  "location": "southcentralus",
  "loginServer": "myregistry1.azurecr.io",
  "name": "myRegistry1",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "myregistry123456789"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}

```


<span data-ttu-id="0c83c-131">Zwróć szczególną uwagę na następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="0c83c-131">Take special note:</span></span>

* <span data-ttu-id="0c83c-132">`id`— Identyfikator rejestru hello w ramach subskrypcji, który jest wymagany, jeśli chcesz, aby tooassign nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="0c83c-132">`id` - Identifier for hello registry in your subscription, which you need if you want tooassign a service principal.</span></span>
* <span data-ttu-id="0c83c-133">`loginServer`-hello Pełna nazwa należy określić zbyt[Zaloguj się w rejestrze toohello](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="0c83c-133">`loginServer` - hello fully qualified name you specify too[log in toohello registry](container-registry-authentication.md).</span></span> <span data-ttu-id="0c83c-134">W tym przykładzie nazwa hello jest `myregistry1.exp.azurecr.io` (tylko małe litery).</span><span class="sxs-lookup"><span data-stu-id="0c83c-134">In this example, hello name is `myregistry1.exp.azurecr.io` (all lowercase).</span></span>

## <a name="assign-a-service-principal"></a><span data-ttu-id="0c83c-135">Przypisywanie nazwy głównej usługi</span><span class="sxs-lookup"><span data-stu-id="0c83c-135">Assign a service principal</span></span>
<span data-ttu-id="0c83c-136">Za pomocą interfejsu wiersza polecenia 2.0 polecenia tooassign rejestr tooa główną usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0c83c-136">Use CLI 2.0 commands tooassign an Azure Active Directory service principal tooa registry.</span></span> <span data-ttu-id="0c83c-137">Witaj nazwy głównej usługi w tych przykładach przypisany hello właściciela roli, ale można przypisać [innych ról](../active-directory/role-based-access-control-configure.md) Jeśli chcesz.</span><span class="sxs-lookup"><span data-stu-id="0c83c-137">hello service principal in these examples is assigned hello Owner role, but you can assign [other roles](../active-directory/role-based-access-control-configure.md) if you want.</span></span>

### <a name="create-a-service-principal-and-assign-access-toohello-registry"></a><span data-ttu-id="0c83c-138">Tworzenie nazwy głównej usługi i przypisywanie dostępu toohello rejestru</span><span class="sxs-lookup"><span data-stu-id="0c83c-138">Create a service principal and assign access toohello registry</span></span>
<span data-ttu-id="0c83c-139">W hello następujące polecenia, nowej nazwy głównej usługi jest przypisywana właściciela roli dostępu toohello rejestru identyfikator przekazany z hello `--scopes` parametru.</span><span class="sxs-lookup"><span data-stu-id="0c83c-139">In hello following command, a new service principal is assigned Owner role access toohello registry identifier passed with hello `--scopes` parameter.</span></span> <span data-ttu-id="0c83c-140">Określ silne hasło z hello `--password` parametru.</span><span class="sxs-lookup"><span data-stu-id="0c83c-140">Specify a strong password with hello `--password` parameter.</span></span>

```azurecli
az ad sp create-for-rbac --scopes /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --password myPassword
```



### <a name="assign-an-existing-service-principal"></a><span data-ttu-id="0c83c-141">Przypisywanie istniejącej nazwy głównej usługi</span><span class="sxs-lookup"><span data-stu-id="0c83c-141">Assign an existing service principal</span></span>
<span data-ttu-id="0c83c-142">Jeśli już masz nazwy głównej usługi i chcesz tooassign jej właściciela roli dostępu toohello rejestru, uruchom polecenie toohello podobne, poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="0c83c-142">If you already have a service principal and want tooassign it Owner role access toohello registry, run a command similar toohello following example.</span></span> <span data-ttu-id="0c83c-143">Przekaż identyfikator podmiotu zabezpieczeń aplikacji usługi hello przy użyciu hello `--assignee` parametru:</span><span class="sxs-lookup"><span data-stu-id="0c83c-143">You pass hello service principal app ID using hello `--assignee` parameter:</span></span>

```azurecli
az role assignment create --scope /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --assignee myAppId
```



## <a name="manage-admin-credentials"></a><span data-ttu-id="0c83c-144">Zarządzanie poświadczeniami administratora</span><span class="sxs-lookup"><span data-stu-id="0c83c-144">Manage admin credentials</span></span>
<span data-ttu-id="0c83c-145">Konto administratora jest automatycznie tworzone dla każdego rejestru kontenera i jest domyślnie wyłączone.</span><span class="sxs-lookup"><span data-stu-id="0c83c-145">An admin account is automatically created for each container registry and is disabled by default.</span></span> <span data-ttu-id="0c83c-146">Witaj w następujących przykładach `az acr` poświadczenia administratora hello toomanage rejestru kontenera polecenia interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="0c83c-146">hello following examples show `az acr` CLI commands toomanage hello admin credentials for your container registry.</span></span>

### <a name="obtain-admin-user-credentials"></a><span data-ttu-id="0c83c-147">Uzyskiwanie poświadczeń użytkownika administratora</span><span class="sxs-lookup"><span data-stu-id="0c83c-147">Obtain admin user credentials</span></span>
```azurecli
az acr credential show -n myRegistry1
```

### <a name="enable-admin-user-for-an-existing-registry"></a><span data-ttu-id="0c83c-148">Włączanie użytkownika administratora dla istniejącego rejestru</span><span class="sxs-lookup"><span data-stu-id="0c83c-148">Enable admin user for an existing registry</span></span>
```azurecli
az acr update -n myRegistry1 --admin-enabled true
```

### <a name="disable-admin-user-for-an-existing-registry"></a><span data-ttu-id="0c83c-149">Wyłączanie użytkownika administratora dla istniejącego rejestru</span><span class="sxs-lookup"><span data-stu-id="0c83c-149">Disable admin user for an existing registry</span></span>
```azurecli
az acr update -n myRegistry1 --admin-enabled false
```

## <a name="list-images-and-tags"></a><span data-ttu-id="0c83c-150">Tworzenie listy obrazów i tagów</span><span class="sxs-lookup"><span data-stu-id="0c83c-150">List images and tags</span></span>
<span data-ttu-id="0c83c-151">Użyj hello `az acr` polecenia interfejsu wiersza polecenia tooquery hello obrazów i tagów w repozytorium.</span><span class="sxs-lookup"><span data-stu-id="0c83c-151">Use hello `az acr` CLI commands tooquery hello images and tags in a repository.</span></span>

> [!NOTE]
> <span data-ttu-id="0c83c-152">Obecnie rejestru kontenera nie obsługuje hello `docker search` tooquery polecenia dla obrazów i tagów.</span><span class="sxs-lookup"><span data-stu-id="0c83c-152">Currently, Container Registry does not support hello `docker search` command tooquery for images and tags.</span></span>


### <a name="list-repositories"></a><span data-ttu-id="0c83c-153">Tworzenie listy repozytoriów</span><span class="sxs-lookup"><span data-stu-id="0c83c-153">List repositories</span></span>
<span data-ttu-id="0c83c-154">Hello poniższym przykładzie przedstawiono repozytoria hello w rejestrze, w formacie JSON (JavaScript Object Notation):</span><span class="sxs-lookup"><span data-stu-id="0c83c-154">hello following example lists hello repositories in a registry, in JSON (JavaScript Object Notation) format:</span></span>

```azurecli
az acr repository list -n myRegistry1 -o json
```

### <a name="list-tags"></a><span data-ttu-id="0c83c-155">Tworzenie listy tagów</span><span class="sxs-lookup"><span data-stu-id="0c83c-155">List tags</span></span>
<span data-ttu-id="0c83c-156">Witaj poniższy przykład zawiera tagi hello na powitania **przykłady/nginx** repozytorium, w formacie JSON:</span><span class="sxs-lookup"><span data-stu-id="0c83c-156">hello following example lists hello tags on hello **samples/nginx** repository, in JSON format:</span></span>

```azurecli
az acr repository show-tags -n myRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a><span data-ttu-id="0c83c-157">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0c83c-157">Next steps</span></span>
* [<span data-ttu-id="0c83c-158">Pierwszy obraz przy użyciu interfejsu wiersza polecenia Docker hello push</span><span class="sxs-lookup"><span data-stu-id="0c83c-158">Push your first image using hello Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
