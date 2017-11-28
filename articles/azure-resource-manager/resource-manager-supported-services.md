---
title: "aaaAzure dostawców zasobów i typów zasobów | Dokumentacja firmy Microsoft"
description: "Zawiera opis dostawcy zasobów hello obsługujących usługi Resource Manager, schematów i dostępne wersje interfejsu API i regiony hello może obsługiwać zasoby hello."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 3c7a6fe4-371a-40da-9ebe-b574f583305b
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: tomfitz
ms.openlocfilehash: 23db1d3808a20166f3b44ec801e1bcc46fbb9bd3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="resource-providers-and-types"></a><span data-ttu-id="9749f-103">Dostawcy zasobów i typów</span><span class="sxs-lookup"><span data-stu-id="9749f-103">Resource providers and types</span></span>

<span data-ttu-id="9749f-104">W przypadku wdrażania zasobów, należy często tooretrieve informacji na temat hello dostawców zasobów i typów.</span><span class="sxs-lookup"><span data-stu-id="9749f-104">When deploying resources, you frequently need tooretrieve information about hello resource providers and types.</span></span> <span data-ttu-id="9749f-105">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="9749f-105">In this article, you learn to:</span></span>

* <span data-ttu-id="9749f-106">Wyświetlanie wszystkich dostawców zasobów na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="9749f-106">View all resource providers in Azure</span></span>
* <span data-ttu-id="9749f-107">Sprawdzaj stan rejestracji dostawcy zasobów</span><span class="sxs-lookup"><span data-stu-id="9749f-107">Check registration status of a resource provider</span></span>
* <span data-ttu-id="9749f-108">Rejestrowanie dostawcy zasobów</span><span class="sxs-lookup"><span data-stu-id="9749f-108">Register a resource provider</span></span>
* <span data-ttu-id="9749f-109">Wyświetlanie typów zasobów dla dostawcy zasobów</span><span class="sxs-lookup"><span data-stu-id="9749f-109">View resource types for a resource provider</span></span>
* <span data-ttu-id="9749f-110">Prawidłowe lokalizacje widoku dla typu zasobu</span><span class="sxs-lookup"><span data-stu-id="9749f-110">View valid locations for a resource type</span></span>
* <span data-ttu-id="9749f-111">Widok prawidłowych wersji interfejsu API dla typu zasobu</span><span class="sxs-lookup"><span data-stu-id="9749f-111">View valid API versions for a resource type</span></span>

<span data-ttu-id="9749f-112">Można wykonywać następujące czynności, za pośrednictwem portalu hello, programu PowerShell lub wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9749f-112">You can perform these steps through hello portal, PowerShell, or Azure CLI.</span></span>

## <a name="powershell"></a><span data-ttu-id="9749f-113">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9749f-113">PowerShell</span></span>

<span data-ttu-id="9749f-114">toosee wszystkich dostawców zasobów platformy Azure i hello stan rejestracji subskrypcji, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="9749f-114">toosee all resource providers in Azure, and hello registration status for your subscription, use:</span></span>

```powershell
Get-AzureRmResourceProvider -ListAvailable | Select-Object ProviderNamespace, RegistrationState
```

<span data-ttu-id="9749f-115">Która zwróci wyniki podobne do:</span><span class="sxs-lookup"><span data-stu-id="9749f-115">Which returns results similar to:</span></span>

```powershell
ProviderNamespace                RegistrationState
-------------------------------- ------------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

<span data-ttu-id="9749f-116">Rejestrowanie dostawcy zasobów umożliwia skonfigurowanie toowork Twojej subskrypcji hello dostawcy zasobów.</span><span class="sxs-lookup"><span data-stu-id="9749f-116">Registering a resource provider configures your subscription toowork with hello resource provider.</span></span> <span data-ttu-id="9749f-117">zakres Hello rejestracji jest zawsze hello subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="9749f-117">hello scope for registration is always hello subscription.</span></span> <span data-ttu-id="9749f-118">Domyślnie automatycznie zarejestrowano wielu dostawców zasobów.</span><span class="sxs-lookup"><span data-stu-id="9749f-118">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="9749f-119">Jednak może być konieczne toomanually zarejestrować niektórzy dostawcy zasobów.</span><span class="sxs-lookup"><span data-stu-id="9749f-119">However, you may need toomanually register some resource providers.</span></span> <span data-ttu-id="9749f-120">tooregister dostawcy zasobów, musi mieć uprawnienie tooperform hello `/register/action` operacji hello dostawcy zasobów.</span><span class="sxs-lookup"><span data-stu-id="9749f-120">tooregister a resource provider, you must have permission tooperform hello `/register/action` operation for hello resource provider.</span></span> <span data-ttu-id="9749f-121">Ta operacja jest dołączony do hello współautora i ról właściciela.</span><span class="sxs-lookup"><span data-stu-id="9749f-121">This operation is included in hello Contributor and Owner roles.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

<span data-ttu-id="9749f-122">Która zwróci wyniki podobne do:</span><span class="sxs-lookup"><span data-stu-id="9749f-122">Which returns results similar to:</span></span>

```powershell
ProviderNamespace : Microsoft.Batch
RegistrationState : Registering
ResourceTypes     : {batchAccounts, operations, locations, locations/quotas}
Locations         : {West Europe, East US, East US 2, West US...}
```

<span data-ttu-id="9749f-123">Nie można wyrejestrować dostawcy zasobów, gdy nadal masz typów zasobów z tego dostawcy zasobów w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="9749f-123">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="9749f-124">informacje toosee dla dostawcy określonego zasobu, użyj:</span><span class="sxs-lookup"><span data-stu-id="9749f-124">toosee information for a particular resource provider, use:</span></span>

```powershell
Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

<span data-ttu-id="9749f-125">Która zwróci wyniki podobne do:</span><span class="sxs-lookup"><span data-stu-id="9749f-125">Which returns results similar to:</span></span>

```powershell
{ProviderNamespace : Microsoft.Batch
RegistrationState : Registered
ResourceTypes     : {batchAccounts}
Locations         : {West Europe, East US, East US 2, West US...}

...
```

<span data-ttu-id="9749f-126">typy zasobów hello toosee dostawcy zasobów, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="9749f-126">toosee hello resource types for a resource provider, use:</span></span>

```powershell
(Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes.ResourceTypeName
```

<span data-ttu-id="9749f-127">Polecenie to zwraca:</span><span class="sxs-lookup"><span data-stu-id="9749f-127">Which returns:</span></span>

```powershell
batchAccounts
operations
locations
locations/quotas
```

<span data-ttu-id="9749f-128">wersja interfejsu API Hello odpowiada tooa wersji operacji interfejsu API REST, które są wydawane przez dostawcę zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="9749f-128">hello API version corresponds tooa version of REST API operations that are released by hello resource provider.</span></span> <span data-ttu-id="9749f-129">Jak dostawca zasobów umożliwia korzystanie z nowych funkcji, zwalnia nowej wersji hello interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="9749f-129">As a resource provider enables new features, it releases a new version of hello REST API.</span></span> 

<span data-ttu-id="9749f-130">Użyj tooget hello dostępne wersje interfejsu API dla typu zasobu:</span><span class="sxs-lookup"><span data-stu-id="9749f-130">tooget hello available API versions for a resource type, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).ApiVersions
```

<span data-ttu-id="9749f-131">Polecenie to zwraca:</span><span class="sxs-lookup"><span data-stu-id="9749f-131">Which returns:</span></span>

```powershell
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

<span data-ttu-id="9749f-132">Menedżer zasobów jest obsługiwane we wszystkich regionach, ale hello zasoby, które można wdrożyć mogą nie być obsługiwane we wszystkich regionach.</span><span class="sxs-lookup"><span data-stu-id="9749f-132">Resource Manager is supported in all regions, but hello resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="9749f-133">Ponadto może być mają zastosowanie ograniczenia dotyczące subskrypcji, które uniemożliwić korzystanie z niektórych regionach, które obsługują hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="9749f-133">In addition, there may be limitations on your subscription that prevent you from using some regions that support hello resource.</span></span> 

<span data-ttu-id="9749f-134">Użyj tooget hello obsługiwane lokalizacje dla typu zasobu.</span><span class="sxs-lookup"><span data-stu-id="9749f-134">tooget hello supported locations for a resource type, use.</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).Locations
```

<span data-ttu-id="9749f-135">Polecenie to zwraca:</span><span class="sxs-lookup"><span data-stu-id="9749f-135">Which returns:</span></span>

```powershell
West Europe
East US
East US 2
West US
...
```

## <a name="azure-cli"></a><span data-ttu-id="9749f-136">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9749f-136">Azure CLI</span></span>
<span data-ttu-id="9749f-137">toosee wszystkich dostawców zasobów platformy Azure i hello stan rejestracji subskrypcji, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="9749f-137">toosee all resource providers in Azure, and hello registration status for your subscription, use:</span></span>

```azurecli
az provider list --query "[].{Provider:namespace, Status:registrationState}" --out table
```

<span data-ttu-id="9749f-138">Która zwróci wyniki podobne do:</span><span class="sxs-lookup"><span data-stu-id="9749f-138">Which returns results similar to:</span></span>

```azurecli
Provider                         Status
-------------------------------- ----------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

<span data-ttu-id="9749f-139">Rejestrowanie dostawcy zasobów umożliwia skonfigurowanie toowork Twojej subskrypcji hello dostawcy zasobów.</span><span class="sxs-lookup"><span data-stu-id="9749f-139">Registering a resource provider configures your subscription toowork with hello resource provider.</span></span> <span data-ttu-id="9749f-140">zakres Hello rejestracji jest zawsze hello subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="9749f-140">hello scope for registration is always hello subscription.</span></span> <span data-ttu-id="9749f-141">Domyślnie automatycznie zarejestrowano wielu dostawców zasobów.</span><span class="sxs-lookup"><span data-stu-id="9749f-141">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="9749f-142">Jednak może być konieczne toomanually zarejestrować niektórzy dostawcy zasobów.</span><span class="sxs-lookup"><span data-stu-id="9749f-142">However, you may need toomanually register some resource providers.</span></span> <span data-ttu-id="9749f-143">tooregister dostawcy zasobów, musi mieć uprawnienie tooperform hello `/register/action` operacji hello dostawcy zasobów.</span><span class="sxs-lookup"><span data-stu-id="9749f-143">tooregister a resource provider, you must have permission tooperform hello `/register/action` operation for hello resource provider.</span></span> <span data-ttu-id="9749f-144">Ta operacja jest dołączony do hello współautora i ról właściciela.</span><span class="sxs-lookup"><span data-stu-id="9749f-144">This operation is included in hello Contributor and Owner roles.</span></span>

```azurecli
az provider register --namespace Microsoft.Batch
```

<span data-ttu-id="9749f-145">Która zwraca komunikat do tej rejestracji jest w toku.</span><span class="sxs-lookup"><span data-stu-id="9749f-145">Which returns a message that registration is on-going.</span></span>

<span data-ttu-id="9749f-146">Nie można wyrejestrować dostawcy zasobów, gdy nadal masz typów zasobów z tego dostawcy zasobów w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="9749f-146">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="9749f-147">informacje toosee dla dostawcy określonego zasobu, użyj:</span><span class="sxs-lookup"><span data-stu-id="9749f-147">toosee information for a particular resource provider, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch
```

<span data-ttu-id="9749f-148">Która zwróci wyniki podobne do:</span><span class="sxs-lookup"><span data-stu-id="9749f-148">Which returns results similar to:</span></span>

```azurecli
{
    "id": "/subscriptions/####-####/providers/Microsoft.Batch",
    "namespace": "Microsoft.Batch",
    "registrationsState": "Registering",
    "resourceTypes:" [
        ...
    ]
}
```

<span data-ttu-id="9749f-149">typy zasobów hello toosee dostawcy zasobów, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="9749f-149">toosee hello resource types for a resource provider, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[*].resourceType" --out table
```

<span data-ttu-id="9749f-150">Polecenie to zwraca:</span><span class="sxs-lookup"><span data-stu-id="9749f-150">Which returns:</span></span>

```azurecli
Result
---------------
batchAccounts
operations
locations
locations/quotas
```

<span data-ttu-id="9749f-151">wersja interfejsu API Hello odpowiada tooa wersji operacji interfejsu API REST, które są wydawane przez dostawcę zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="9749f-151">hello API version corresponds tooa version of REST API operations that are released by hello resource provider.</span></span> <span data-ttu-id="9749f-152">Jak dostawca zasobów umożliwia korzystanie z nowych funkcji, zwalnia nowej wersji hello interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="9749f-152">As a resource provider enables new features, it releases a new version of hello REST API.</span></span> 

<span data-ttu-id="9749f-153">Użyj tooget hello dostępne wersje interfejsu API dla typu zasobu:</span><span class="sxs-lookup"><span data-stu-id="9749f-153">tooget hello available API versions for a resource type, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].apiVersions | [0]" --out table
```

<span data-ttu-id="9749f-154">Polecenie to zwraca:</span><span class="sxs-lookup"><span data-stu-id="9749f-154">Which returns:</span></span>

```azurecli
Result
---------------
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

<span data-ttu-id="9749f-155">Menedżer zasobów jest obsługiwane we wszystkich regionach, ale hello zasoby, które można wdrożyć mogą nie być obsługiwane we wszystkich regionach.</span><span class="sxs-lookup"><span data-stu-id="9749f-155">Resource Manager is supported in all regions, but hello resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="9749f-156">Ponadto może być mają zastosowanie ograniczenia dotyczące subskrypcji, które uniemożliwić korzystanie z niektórych regionach, które obsługują hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="9749f-156">In addition, there may be limitations on your subscription that prevent you from using some regions that support hello resource.</span></span> 

<span data-ttu-id="9749f-157">Użyj tooget hello obsługiwane lokalizacje dla typu zasobu.</span><span class="sxs-lookup"><span data-stu-id="9749f-157">tooget hello supported locations for a resource type, use.</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].locations | [0]" --out table
```

<span data-ttu-id="9749f-158">Polecenie to zwraca:</span><span class="sxs-lookup"><span data-stu-id="9749f-158">Which returns:</span></span>

```azurecli
Result
---------------
West Europe
East US
East US 2
West US
...
```

## <a name="portal"></a><span data-ttu-id="9749f-159">Portal</span><span class="sxs-lookup"><span data-stu-id="9749f-159">Portal</span></span>

<span data-ttu-id="9749f-160">Wybierz wszystkich dostawców zasobów platformy Azure i hello stanu rejestracji subskrypcji toosee **subskrypcje**.</span><span class="sxs-lookup"><span data-stu-id="9749f-160">toosee all resource providers in Azure, and hello registration status for your subscription, select **Subscriptions**.</span></span>

![Wybierz subskrypcje](./media/resource-manager-supported-services/select-subscriptions.png)

<span data-ttu-id="9749f-162">Wybierz hello tooview subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="9749f-162">Choose hello subscription tooview.</span></span>

![Określ subskrypcję](./media/resource-manager-supported-services/subscription.png)

<span data-ttu-id="9749f-164">Wybierz **dostawców zasobów** i wyświetlanie hello listy dostępnych dostawców zasobów.</span><span class="sxs-lookup"><span data-stu-id="9749f-164">Select **Resource providers** and view hello list of available resource providers.</span></span>

![Pokaż dostawców zasobów](./media/resource-manager-supported-services/show-resource-providers.png)

<span data-ttu-id="9749f-166">Rejestrowanie dostawcy zasobów umożliwia skonfigurowanie toowork Twojej subskrypcji hello dostawcy zasobów.</span><span class="sxs-lookup"><span data-stu-id="9749f-166">Registering a resource provider configures your subscription toowork with hello resource provider.</span></span> <span data-ttu-id="9749f-167">zakres Hello rejestracji jest zawsze hello subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="9749f-167">hello scope for registration is always hello subscription.</span></span> <span data-ttu-id="9749f-168">Domyślnie automatycznie zarejestrowano wielu dostawców zasobów.</span><span class="sxs-lookup"><span data-stu-id="9749f-168">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="9749f-169">Jednak może być konieczne toomanually zarejestrować niektórzy dostawcy zasobów.</span><span class="sxs-lookup"><span data-stu-id="9749f-169">However, you may need toomanually register some resource providers.</span></span> <span data-ttu-id="9749f-170">tooregister dostawcy zasobów, musi mieć uprawnienie tooperform hello `/register/action` operacji hello dostawcy zasobów.</span><span class="sxs-lookup"><span data-stu-id="9749f-170">tooregister a resource provider, you must have permission tooperform hello `/register/action` operation for hello resource provider.</span></span> <span data-ttu-id="9749f-171">Ta operacja jest dołączony do hello współautora i ról właściciela.</span><span class="sxs-lookup"><span data-stu-id="9749f-171">This operation is included in hello Contributor and Owner roles.</span></span> <span data-ttu-id="9749f-172">Wybierz tooregister dostawcę zasobów **zarejestrować**.</span><span class="sxs-lookup"><span data-stu-id="9749f-172">tooregister a resource provider, select **Register**.</span></span>

![Rejestrowanie dostawcy zasobów](./media/resource-manager-supported-services/register-provider.png)

<span data-ttu-id="9749f-174">Nie można wyrejestrować dostawcy zasobów, gdy nadal masz typów zasobów z tego dostawcy zasobów w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="9749f-174">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="9749f-175">Wybierz informacje toosee dla dostawcy określonego zasobu, **więcej usług**.</span><span class="sxs-lookup"><span data-stu-id="9749f-175">toosee information for a particular resource provider, select **More services**.</span></span>

![Wybierz więcej usług](./media/resource-manager-supported-services/more-services.png)

<span data-ttu-id="9749f-177">Wyszukaj **Eksploratora zasobów** i wybierz ją z hello dostępnych opcji.</span><span class="sxs-lookup"><span data-stu-id="9749f-177">Search for **Resource Explorer** and select it from hello available options.</span></span>

![Wybierz Eksploratora zasobów](./media/resource-manager-supported-services/select-resource-explorer.png)

<span data-ttu-id="9749f-179">Wybierz **dostawców**.</span><span class="sxs-lookup"><span data-stu-id="9749f-179">Select **Providers**.</span></span>

![Wybierz dostawców](./media/resource-manager-supported-services/select-providers.png)

<span data-ttu-id="9749f-181">Dostawca zasobów wybierz hello i zasobu typu, które mają tooview.</span><span class="sxs-lookup"><span data-stu-id="9749f-181">Select hello resource provider and resource type that you want tooview.</span></span>

![Wybierz typ zasobu](./media/resource-manager-supported-services/select-resource-type.png)

<span data-ttu-id="9749f-183">Menedżer zasobów jest obsługiwane we wszystkich regionach, ale hello zasoby, które można wdrożyć mogą nie być obsługiwane we wszystkich regionach.</span><span class="sxs-lookup"><span data-stu-id="9749f-183">Resource Manager is supported in all regions, but hello resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="9749f-184">Ponadto może być mają zastosowanie ograniczenia dotyczące subskrypcji, które uniemożliwić korzystanie z niektórych regionach, które obsługują hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="9749f-184">In addition, there may be limitations on your subscription that prevent you from using some regions that support hello resource.</span></span> <span data-ttu-id="9749f-185">Eksplorator zasobów Hello Wyświetla prawidłowe lokalizacje dla typu zasobu hello.</span><span class="sxs-lookup"><span data-stu-id="9749f-185">hello resource explorer displays valid locations for hello resource type.</span></span>

![Pokaż lokalizacje](./media/resource-manager-supported-services/show-locations.png)

<span data-ttu-id="9749f-187">wersja interfejsu API Hello odpowiada tooa wersji operacji interfejsu API REST, które są wydawane przez dostawcę zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="9749f-187">hello API version corresponds tooa version of REST API operations that are released by hello resource provider.</span></span> <span data-ttu-id="9749f-188">Jak dostawca zasobów umożliwia korzystanie z nowych funkcji, zwalnia nowej wersji hello interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="9749f-188">As a resource provider enables new features, it releases a new version of hello REST API.</span></span> <span data-ttu-id="9749f-189">Eksplorator zasobów Hello Wyświetla prawidłowych wersji interfejsu API dla typu zasobu hello.</span><span class="sxs-lookup"><span data-stu-id="9749f-189">hello resource explorer displays valid API versions for hello resource type.</span></span>

![Pokaż wersje interfejsu API](./media/resource-manager-supported-services/show-api-versions.png)

## <a name="next-steps"></a><span data-ttu-id="9749f-191">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9749f-191">Next steps</span></span>
* <span data-ttu-id="9749f-192">toolearn o tworzeniu szablonów usługi Resource Manager, zobacz [szablonów Authoring Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="9749f-192">toolearn about creating Resource Manager templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="9749f-193">toolearn dotyczących wdrażania zasobów, zobacz [wdrażania aplikacji przy użyciu szablonu usługi Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="9749f-193">toolearn about deploying resources, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="9749f-194">operacje hello tooview dla dostawcy zasobów, zobacz [interfejsu API REST Azure](/rest/api/).</span><span class="sxs-lookup"><span data-stu-id="9749f-194">tooview hello operations for a resource provider, see [Azure REST API](/rest/api/).</span></span>

