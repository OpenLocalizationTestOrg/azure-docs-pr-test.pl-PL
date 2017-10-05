---
title: "Dostawcy zasobów platformy Azure i typy zasobów | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano dostawców zasobów obsługujących usługi Resource Manager, ich schematów i dostępne wersje interfejsu API i regionów, które można udostępniać zasoby."
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
ms.openlocfilehash: 6a9128f45d4199404019cee594842d59c7f1aaf3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="resource-providers-and-types"></a><span data-ttu-id="bd764-103">Dostawcy zasobów i typów</span><span class="sxs-lookup"><span data-stu-id="bd764-103">Resource providers and types</span></span>

<span data-ttu-id="bd764-104">Podczas wdrażania zasobów, często konieczne pobranie informacji o dostawcy zasobów i typów.</span><span class="sxs-lookup"><span data-stu-id="bd764-104">When deploying resources, you frequently need to retrieve information about the resource providers and types.</span></span> <span data-ttu-id="bd764-105">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="bd764-105">In this article, you learn to:</span></span>

* <span data-ttu-id="bd764-106">Wyświetlanie wszystkich dostawców zasobów na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="bd764-106">View all resource providers in Azure</span></span>
* <span data-ttu-id="bd764-107">Sprawdzaj stan rejestracji dostawcy zasobów</span><span class="sxs-lookup"><span data-stu-id="bd764-107">Check registration status of a resource provider</span></span>
* <span data-ttu-id="bd764-108">Rejestrowanie dostawcy zasobów</span><span class="sxs-lookup"><span data-stu-id="bd764-108">Register a resource provider</span></span>
* <span data-ttu-id="bd764-109">Wyświetlanie typów zasobów dla dostawcy zasobów</span><span class="sxs-lookup"><span data-stu-id="bd764-109">View resource types for a resource provider</span></span>
* <span data-ttu-id="bd764-110">Prawidłowe lokalizacje widoku dla typu zasobu</span><span class="sxs-lookup"><span data-stu-id="bd764-110">View valid locations for a resource type</span></span>
* <span data-ttu-id="bd764-111">Widok prawidłowych wersji interfejsu API dla typu zasobu</span><span class="sxs-lookup"><span data-stu-id="bd764-111">View valid API versions for a resource type</span></span>

<span data-ttu-id="bd764-112">Można wykonywać następujące czynności, za pośrednictwem portalu, programu PowerShell lub wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bd764-112">You can perform these steps through the portal, PowerShell, or Azure CLI.</span></span>

## <a name="powershell"></a><span data-ttu-id="bd764-113">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bd764-113">PowerShell</span></span>

<span data-ttu-id="bd764-114">Aby wyświetlić wszystkich dostawców zasobów na platformie Azure i stan rejestracji subskrypcji, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="bd764-114">To see all resource providers in Azure, and the registration status for your subscription, use:</span></span>

```powershell
Get-AzureRmResourceProvider -ListAvailable | Select-Object ProviderNamespace, RegistrationState
```

<span data-ttu-id="bd764-115">Która zwróci wyniki podobne do:</span><span class="sxs-lookup"><span data-stu-id="bd764-115">Which returns results similar to:</span></span>

```powershell
ProviderNamespace                RegistrationState
-------------------------------- ------------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

<span data-ttu-id="bd764-116">Rejestrowanie dostawcy zasobów służy do konfigurowania subskrypcji do pracy z dostawcy zasobów.</span><span class="sxs-lookup"><span data-stu-id="bd764-116">Registering a resource provider configures your subscription to work with the resource provider.</span></span> <span data-ttu-id="bd764-117">Subskrypcja jest zawsze zakres rejestracji.</span><span class="sxs-lookup"><span data-stu-id="bd764-117">The scope for registration is always the subscription.</span></span> <span data-ttu-id="bd764-118">Domyślnie automatycznie zarejestrowano wielu dostawców zasobów.</span><span class="sxs-lookup"><span data-stu-id="bd764-118">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="bd764-119">Jednak należy ręcznie zarejestrować niektórzy dostawcy zasobów.</span><span class="sxs-lookup"><span data-stu-id="bd764-119">However, you may need to manually register some resource providers.</span></span> <span data-ttu-id="bd764-120">Aby zarejestrować dostawcy zasobów, musi mieć uprawnienia do wykonywania `/register/action` operacji dla dostawcy zasobów.</span><span class="sxs-lookup"><span data-stu-id="bd764-120">To register a resource provider, you must have permission to perform the `/register/action` operation for the resource provider.</span></span> <span data-ttu-id="bd764-121">Ta operacja znajduje rolę współautora i właściciela.</span><span class="sxs-lookup"><span data-stu-id="bd764-121">This operation is included in the Contributor and Owner roles.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

<span data-ttu-id="bd764-122">Która zwróci wyniki podobne do:</span><span class="sxs-lookup"><span data-stu-id="bd764-122">Which returns results similar to:</span></span>

```powershell
ProviderNamespace : Microsoft.Batch
RegistrationState : Registering
ResourceTypes     : {batchAccounts, operations, locations, locations/quotas}
Locations         : {West Europe, East US, East US 2, West US...}
```

<span data-ttu-id="bd764-123">Nie można wyrejestrować dostawcy zasobów, gdy nadal masz typów zasobów z tego dostawcy zasobów w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="bd764-123">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="bd764-124">Aby wyświetlić informacje dotyczące dostawcy określonego zasobu, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="bd764-124">To see information for a particular resource provider, use:</span></span>

```powershell
Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

<span data-ttu-id="bd764-125">Która zwróci wyniki podobne do:</span><span class="sxs-lookup"><span data-stu-id="bd764-125">Which returns results similar to:</span></span>

```powershell
{ProviderNamespace : Microsoft.Batch
RegistrationState : Registered
ResourceTypes     : {batchAccounts}
Locations         : {West Europe, East US, East US 2, West US...}

...
```

<span data-ttu-id="bd764-126">Aby wyświetlić typy zasobów dla dostawcy zasobów, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="bd764-126">To see the resource types for a resource provider, use:</span></span>

```powershell
(Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes.ResourceTypeName
```

<span data-ttu-id="bd764-127">Polecenie to zwraca:</span><span class="sxs-lookup"><span data-stu-id="bd764-127">Which returns:</span></span>

```powershell
batchAccounts
operations
locations
locations/quotas
```

<span data-ttu-id="bd764-128">Wersja interfejsu API odpowiada wersji operacji interfejsu API REST, które są wydawane przez dostawcę zasobów.</span><span class="sxs-lookup"><span data-stu-id="bd764-128">The API version corresponds to a version of REST API operations that are released by the resource provider.</span></span> <span data-ttu-id="bd764-129">Jak dostawca zasobów umożliwia korzystanie z nowych funkcji, udostępnia nową wersję interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="bd764-129">As a resource provider enables new features, it releases a new version of the REST API.</span></span> 

<span data-ttu-id="bd764-130">Aby uzyskać dostępne wersje interfejsu API dla typu zasobu, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="bd764-130">To get the available API versions for a resource type, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).ApiVersions
```

<span data-ttu-id="bd764-131">Polecenie to zwraca:</span><span class="sxs-lookup"><span data-stu-id="bd764-131">Which returns:</span></span>

```powershell
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

<span data-ttu-id="bd764-132">Menedżer zasobów jest obsługiwane we wszystkich regionach, ale zasoby, które można wdrożyć mogą nie być obsługiwane we wszystkich regionach.</span><span class="sxs-lookup"><span data-stu-id="bd764-132">Resource Manager is supported in all regions, but the resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="bd764-133">Ponadto może być mają zastosowanie ograniczenia dotyczące subskrypcji, które uniemożliwią używanie niektórych regionów, które obsługują zasobu.</span><span class="sxs-lookup"><span data-stu-id="bd764-133">In addition, there may be limitations on your subscription that prevent you from using some regions that support the resource.</span></span> 

<span data-ttu-id="bd764-134">Aby uzyskać obsługiwane lokalizacje dla typu zasobu, należy użyć.</span><span class="sxs-lookup"><span data-stu-id="bd764-134">To get the supported locations for a resource type, use.</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).Locations
```

<span data-ttu-id="bd764-135">Polecenie to zwraca:</span><span class="sxs-lookup"><span data-stu-id="bd764-135">Which returns:</span></span>

```powershell
West Europe
East US
East US 2
West US
...
```

## <a name="azure-cli"></a><span data-ttu-id="bd764-136">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="bd764-136">Azure CLI</span></span>
<span data-ttu-id="bd764-137">Aby wyświetlić wszystkich dostawców zasobów na platformie Azure i stan rejestracji subskrypcji, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="bd764-137">To see all resource providers in Azure, and the registration status for your subscription, use:</span></span>

```azurecli
az provider list --query "[].{Provider:namespace, Status:registrationState}" --out table
```

<span data-ttu-id="bd764-138">Która zwróci wyniki podobne do:</span><span class="sxs-lookup"><span data-stu-id="bd764-138">Which returns results similar to:</span></span>

```azurecli
Provider                         Status
-------------------------------- ----------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

<span data-ttu-id="bd764-139">Rejestrowanie dostawcy zasobów służy do konfigurowania subskrypcji do pracy z dostawcy zasobów.</span><span class="sxs-lookup"><span data-stu-id="bd764-139">Registering a resource provider configures your subscription to work with the resource provider.</span></span> <span data-ttu-id="bd764-140">Subskrypcja jest zawsze zakres rejestracji.</span><span class="sxs-lookup"><span data-stu-id="bd764-140">The scope for registration is always the subscription.</span></span> <span data-ttu-id="bd764-141">Domyślnie automatycznie zarejestrowano wielu dostawców zasobów.</span><span class="sxs-lookup"><span data-stu-id="bd764-141">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="bd764-142">Jednak należy ręcznie zarejestrować niektórzy dostawcy zasobów.</span><span class="sxs-lookup"><span data-stu-id="bd764-142">However, you may need to manually register some resource providers.</span></span> <span data-ttu-id="bd764-143">Aby zarejestrować dostawcy zasobów, musi mieć uprawnienia do wykonywania `/register/action` operacji dla dostawcy zasobów.</span><span class="sxs-lookup"><span data-stu-id="bd764-143">To register a resource provider, you must have permission to perform the `/register/action` operation for the resource provider.</span></span> <span data-ttu-id="bd764-144">Ta operacja znajduje rolę współautora i właściciela.</span><span class="sxs-lookup"><span data-stu-id="bd764-144">This operation is included in the Contributor and Owner roles.</span></span>

```azurecli
az provider register --namespace Microsoft.Batch
```

<span data-ttu-id="bd764-145">Która zwraca komunikat do tej rejestracji jest w toku.</span><span class="sxs-lookup"><span data-stu-id="bd764-145">Which returns a message that registration is on-going.</span></span>

<span data-ttu-id="bd764-146">Nie można wyrejestrować dostawcy zasobów, gdy nadal masz typów zasobów z tego dostawcy zasobów w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="bd764-146">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="bd764-147">Aby wyświetlić informacje dotyczące dostawcy określonego zasobu, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="bd764-147">To see information for a particular resource provider, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch
```

<span data-ttu-id="bd764-148">Która zwróci wyniki podobne do:</span><span class="sxs-lookup"><span data-stu-id="bd764-148">Which returns results similar to:</span></span>

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

<span data-ttu-id="bd764-149">Aby wyświetlić typy zasobów dla dostawcy zasobów, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="bd764-149">To see the resource types for a resource provider, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[*].resourceType" --out table
```

<span data-ttu-id="bd764-150">Polecenie to zwraca:</span><span class="sxs-lookup"><span data-stu-id="bd764-150">Which returns:</span></span>

```azurecli
Result
---------------
batchAccounts
operations
locations
locations/quotas
```

<span data-ttu-id="bd764-151">Wersja interfejsu API odpowiada wersji operacji interfejsu API REST, które są wydawane przez dostawcę zasobów.</span><span class="sxs-lookup"><span data-stu-id="bd764-151">The API version corresponds to a version of REST API operations that are released by the resource provider.</span></span> <span data-ttu-id="bd764-152">Jak dostawca zasobów umożliwia korzystanie z nowych funkcji, udostępnia nową wersję interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="bd764-152">As a resource provider enables new features, it releases a new version of the REST API.</span></span> 

<span data-ttu-id="bd764-153">Aby uzyskać dostępne wersje interfejsu API dla typu zasobu, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="bd764-153">To get the available API versions for a resource type, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].apiVersions | [0]" --out table
```

<span data-ttu-id="bd764-154">Polecenie to zwraca:</span><span class="sxs-lookup"><span data-stu-id="bd764-154">Which returns:</span></span>

```azurecli
Result
---------------
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

<span data-ttu-id="bd764-155">Menedżer zasobów jest obsługiwane we wszystkich regionach, ale zasoby, które można wdrożyć mogą nie być obsługiwane we wszystkich regionach.</span><span class="sxs-lookup"><span data-stu-id="bd764-155">Resource Manager is supported in all regions, but the resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="bd764-156">Ponadto może być mają zastosowanie ograniczenia dotyczące subskrypcji, które uniemożliwią używanie niektórych regionów, które obsługują zasobu.</span><span class="sxs-lookup"><span data-stu-id="bd764-156">In addition, there may be limitations on your subscription that prevent you from using some regions that support the resource.</span></span> 

<span data-ttu-id="bd764-157">Aby uzyskać obsługiwane lokalizacje dla typu zasobu, należy użyć.</span><span class="sxs-lookup"><span data-stu-id="bd764-157">To get the supported locations for a resource type, use.</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].locations | [0]" --out table
```

<span data-ttu-id="bd764-158">Polecenie to zwraca:</span><span class="sxs-lookup"><span data-stu-id="bd764-158">Which returns:</span></span>

```azurecli
Result
---------------
West Europe
East US
East US 2
West US
...
```

## <a name="portal"></a><span data-ttu-id="bd764-159">Portal</span><span class="sxs-lookup"><span data-stu-id="bd764-159">Portal</span></span>

<span data-ttu-id="bd764-160">Aby wyświetlić wszystkich dostawców zasobów na platformie Azure i stan rejestracji subskrypcji, wybierz **subskrypcje**.</span><span class="sxs-lookup"><span data-stu-id="bd764-160">To see all resource providers in Azure, and the registration status for your subscription, select **Subscriptions**.</span></span>

![Wybierz subskrypcje](./media/resource-manager-supported-services/select-subscriptions.png)

<span data-ttu-id="bd764-162">Wybierz subskrypcję, aby wyświetlić.</span><span class="sxs-lookup"><span data-stu-id="bd764-162">Choose the subscription to view.</span></span>

![Określ subskrypcję](./media/resource-manager-supported-services/subscription.png)

<span data-ttu-id="bd764-164">Wybierz **dostawców zasobów** i wyświetlić listę dostępnych dostawców zasobów.</span><span class="sxs-lookup"><span data-stu-id="bd764-164">Select **Resource providers** and view the list of available resource providers.</span></span>

![Pokaż dostawców zasobów](./media/resource-manager-supported-services/show-resource-providers.png)

<span data-ttu-id="bd764-166">Rejestrowanie dostawcy zasobów służy do konfigurowania subskrypcji do pracy z dostawcy zasobów.</span><span class="sxs-lookup"><span data-stu-id="bd764-166">Registering a resource provider configures your subscription to work with the resource provider.</span></span> <span data-ttu-id="bd764-167">Subskrypcja jest zawsze zakres rejestracji.</span><span class="sxs-lookup"><span data-stu-id="bd764-167">The scope for registration is always the subscription.</span></span> <span data-ttu-id="bd764-168">Domyślnie automatycznie zarejestrowano wielu dostawców zasobów.</span><span class="sxs-lookup"><span data-stu-id="bd764-168">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="bd764-169">Jednak należy ręcznie zarejestrować niektórzy dostawcy zasobów.</span><span class="sxs-lookup"><span data-stu-id="bd764-169">However, you may need to manually register some resource providers.</span></span> <span data-ttu-id="bd764-170">Aby zarejestrować dostawcy zasobów, musi mieć uprawnienia do wykonywania `/register/action` operacji dla dostawcy zasobów.</span><span class="sxs-lookup"><span data-stu-id="bd764-170">To register a resource provider, you must have permission to perform the `/register/action` operation for the resource provider.</span></span> <span data-ttu-id="bd764-171">Ta operacja znajduje rolę współautora i właściciela.</span><span class="sxs-lookup"><span data-stu-id="bd764-171">This operation is included in the Contributor and Owner roles.</span></span> <span data-ttu-id="bd764-172">Aby zarejestrować dostawcy zasobów, wybierz **zarejestrować**.</span><span class="sxs-lookup"><span data-stu-id="bd764-172">To register a resource provider, select **Register**.</span></span>

![Rejestrowanie dostawcy zasobów](./media/resource-manager-supported-services/register-provider.png)

<span data-ttu-id="bd764-174">Nie można wyrejestrować dostawcy zasobów, gdy nadal masz typów zasobów z tego dostawcy zasobów w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="bd764-174">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="bd764-175">Aby wyświetlić informacje dotyczące dostawcy określonego zasobu, wybierz **więcej usług**.</span><span class="sxs-lookup"><span data-stu-id="bd764-175">To see information for a particular resource provider, select **More services**.</span></span>

![Wybierz więcej usług](./media/resource-manager-supported-services/more-services.png)

<span data-ttu-id="bd764-177">Wyszukaj **Eksploratora zasobów** i wybierz ją z dostępnych opcji.</span><span class="sxs-lookup"><span data-stu-id="bd764-177">Search for **Resource Explorer** and select it from the available options.</span></span>

![Wybierz Eksploratora zasobów](./media/resource-manager-supported-services/select-resource-explorer.png)

<span data-ttu-id="bd764-179">Wybierz **dostawców**.</span><span class="sxs-lookup"><span data-stu-id="bd764-179">Select **Providers**.</span></span>

![Wybierz dostawców](./media/resource-manager-supported-services/select-providers.png)

<span data-ttu-id="bd764-181">Wybierz dostawcę zasobów i typ zasobu, który chcesz wyświetlić.</span><span class="sxs-lookup"><span data-stu-id="bd764-181">Select the resource provider and resource type that you want to view.</span></span>

![Wybierz typ zasobu](./media/resource-manager-supported-services/select-resource-type.png)

<span data-ttu-id="bd764-183">Menedżer zasobów jest obsługiwane we wszystkich regionach, ale zasoby, które można wdrożyć mogą nie być obsługiwane we wszystkich regionach.</span><span class="sxs-lookup"><span data-stu-id="bd764-183">Resource Manager is supported in all regions, but the resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="bd764-184">Ponadto może być mają zastosowanie ograniczenia dotyczące subskrypcji, które uniemożliwią używanie niektórych regionów, które obsługują zasobu.</span><span class="sxs-lookup"><span data-stu-id="bd764-184">In addition, there may be limitations on your subscription that prevent you from using some regions that support the resource.</span></span> <span data-ttu-id="bd764-185">Eksplorator zasobów Wyświetla prawidłowe lokalizacje dla typu zasobu.</span><span class="sxs-lookup"><span data-stu-id="bd764-185">The resource explorer displays valid locations for the resource type.</span></span>

![Pokaż lokalizacje](./media/resource-manager-supported-services/show-locations.png)

<span data-ttu-id="bd764-187">Wersja interfejsu API odpowiada wersji operacji interfejsu API REST, które są wydawane przez dostawcę zasobów.</span><span class="sxs-lookup"><span data-stu-id="bd764-187">The API version corresponds to a version of REST API operations that are released by the resource provider.</span></span> <span data-ttu-id="bd764-188">Jak dostawca zasobów umożliwia korzystanie z nowych funkcji, udostępnia nową wersję interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="bd764-188">As a resource provider enables new features, it releases a new version of the REST API.</span></span> <span data-ttu-id="bd764-189">Eksplorator zasobów wyświetla prawidłowych wersji interfejsu API dla typu zasobu.</span><span class="sxs-lookup"><span data-stu-id="bd764-189">The resource explorer displays valid API versions for the resource type.</span></span>

![Pokaż wersje interfejsu API](./media/resource-manager-supported-services/show-api-versions.png)

## <a name="next-steps"></a><span data-ttu-id="bd764-191">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bd764-191">Next steps</span></span>
* <span data-ttu-id="bd764-192">Aby uzyskać informacje dotyczące tworzenia szablonów usługi Resource Manager, zobacz [szablonów Authoring Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="bd764-192">To learn about creating Resource Manager templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="bd764-193">Aby dowiedzieć się więcej na temat wdrażania zasobów, zobacz [wdrażania aplikacji przy użyciu szablonu usługi Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="bd764-193">To learn about deploying resources, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="bd764-194">Aby wyświetlić operacje dla dostawców zasobów, zobacz [interfejsu API REST Azure](/rest/api/).</span><span class="sxs-lookup"><span data-stu-id="bd764-194">To view the operations for a resource provider, see [Azure REST API](/rest/api/).</span></span>

