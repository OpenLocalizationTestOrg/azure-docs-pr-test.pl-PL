---
title: "Zarządzanie strefami DNS w usłudze Azure DNS - PowerShell | Dokumentacja firmy Microsoft"
description: "Możesz zarządzać stref DNS przy użyciu programu Azure Powershell. W tym artykule opisano sposób aktualizowanie, usuwanie i tworzenie stref DNS w usłudze Azure DNS"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: a67992ab-8166-4052-9b28-554c5a39e60c
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/14/2016
ms.author: gwallace
ms.openlocfilehash: 92f1da660d875c76d5d826669d6c1d12018c3d0a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-dns-zones-using-powershell"></a><span data-ttu-id="e8b17-104">Jak zarządzać stref DNS przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="e8b17-104">How to manage DNS Zones using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e8b17-105">Portal</span><span class="sxs-lookup"><span data-stu-id="e8b17-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="e8b17-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e8b17-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="e8b17-107">Interfejs wiersza polecenia platformy Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="e8b17-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="e8b17-108">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="e8b17-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="e8b17-109">W tym artykule przedstawiono sposób zarządzania stref DNS przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e8b17-109">This article shows you how to manage your DNS zones by using Azure PowerShell.</span></span> <span data-ttu-id="e8b17-110">Można również zarządzać stref DNS przy użyciu wielu platform [interfejsu wiersza polecenia Azure](dns-operations-dnszones-cli.md) lub w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e8b17-110">You can also manage your DNS zones using the cross-platform [Azure CLI](dns-operations-dnszones-cli.md) or the Azure portal.</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-powershell-setup](../../includes/dns-powershell-setup-include.md)]


## <a name="create-a-dns-zone"></a><span data-ttu-id="e8b17-111">Tworzenie strefy DNS</span><span class="sxs-lookup"><span data-stu-id="e8b17-111">Create a DNS zone</span></span>

<span data-ttu-id="e8b17-112">Strefa DNS jest tworzona za pomocą polecenia cmdlet `New-AzureRmDnsZone`.</span><span class="sxs-lookup"><span data-stu-id="e8b17-112">A DNS zone is created by using the `New-AzureRmDnsZone` cmdlet.</span></span>

<span data-ttu-id="e8b17-113">Poniższy przykład tworzy strefę DNS o nazwie *contoso.com* w grupie zasobów o nazwie *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="e8b17-113">The following example creates a DNS zone called *contoso.com* in the resource group called *MyResourceGroup*:</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

<span data-ttu-id="e8b17-114">Poniższy przykład przedstawia sposób tworzenia strefy DNS przy użyciu dwóch [znaczniki usługi Azure Resource Manager](dns-zones-records.md#tags), *project = demo* i *env = test*:</span><span class="sxs-lookup"><span data-stu-id="e8b17-114">The following example shows how to create a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*:</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="e8b17-115">Pobierz strefę DNS</span><span class="sxs-lookup"><span data-stu-id="e8b17-115">Get a DNS zone</span></span>

<span data-ttu-id="e8b17-116">Aby uzyskać dostęp do strefy DNS, należy użyć `Get-AzureRmDnsZone` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e8b17-116">To retrieve a DNS zone, use the `Get-AzureRmDnsZone` cmdlet.</span></span> <span data-ttu-id="e8b17-117">Ta operacja zwraca obiekt strefy DNS odpowiadającej istniejącej strefy w usłudze Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="e8b17-117">This operation returns a DNS zone object corresponding to an existing zone in Azure DNS.</span></span> <span data-ttu-id="e8b17-118">Obiekt zawiera dane dotyczące strefy (na przykład liczba zestawów rekordów), ale nie zawiera zestawów rekordów, same (zobacz `Get-AzureRmDnsRecordSet`).</span><span class="sxs-lookup"><span data-stu-id="e8b17-118">The object contains data about the zone (such as the number of record sets), but does not contain the record sets themselves (see `Get-AzureRmDnsRecordSet`).</span></span>

```powershell
Get-AzureRmDnsZone -Name contoso.com –ResourceGroupName MyAzureResourceGroup

Name                  : contoso.com
ResourceGroupName     : myresourcegroup
Etag                  : 00000003-0000-0000-8ec2-f4879750d201
Tags                  : {project, env}
NameServers           : {ns1-01.azure-dns.com., ns2-01.azure-dns.net., ns3-01.azure-dns.org.,
                        ns4-01.azure-dns.info.}
NumberOfRecordSets    : 2
MaxNumberOfRecordSets : 5000
```

## <a name="list-dns-zones"></a><span data-ttu-id="e8b17-119">Lista stref DNS</span><span class="sxs-lookup"><span data-stu-id="e8b17-119">List DNS zones</span></span>

<span data-ttu-id="e8b17-120">Pomijając nazwę strefy z `Get-AzureRmDnsZone`, można wyliczyć wszystkich stref w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="e8b17-120">By omitting the zone name from `Get-AzureRmDnsZone`, you can enumerate all zones in a resource group.</span></span> <span data-ttu-id="e8b17-121">Ta operacja zwraca tablicę obiektów stref.</span><span class="sxs-lookup"><span data-stu-id="e8b17-121">This operation returns an array of zone objects.</span></span>

```powershell
$zoneList = Get-AzureRmDnsZone -ResourceGroupName MyAzureResourceGroup
```

<span data-ttu-id="e8b17-122">Pomijając zarówno nazwę strefy, jak i nazwę grupy zasobów z `Get-AzureRmDnsZone`, można wyliczyć wszystkich stref w subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e8b17-122">By omitting both the zone name and the resource group name from `Get-AzureRmDnsZone`, you can enumerate all zones in the Azure subscription.</span></span>

```powershell
$zoneList = Get-AzureRmDnsZone
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="e8b17-123">Zaktualizuj strefę DNS</span><span class="sxs-lookup"><span data-stu-id="e8b17-123">Update a DNS zone</span></span>

<span data-ttu-id="e8b17-124">Można wprowadzać zmiany do zasobu strefy DNS przy użyciu `Set-AzureRmDnsZone`.</span><span class="sxs-lookup"><span data-stu-id="e8b17-124">Changes to a DNS zone resource can be made by using `Set-AzureRmDnsZone`.</span></span> <span data-ttu-id="e8b17-125">To polecenie cmdlet nie zaktualizować zestawów rekordów DNS w strefie (zobacz [jak rekordy DNS zarządzanie](dns-operations-recordsets.md)).</span><span class="sxs-lookup"><span data-stu-id="e8b17-125">This cmdlet does not update any of the DNS record sets within the zone (see [How to Manage DNS records](dns-operations-recordsets.md)).</span></span> <span data-ttu-id="e8b17-126">Jest używane wyłącznie do właściwości zasobu strefy samej aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="e8b17-126">It's only used to update properties of the zone resource itself.</span></span> <span data-ttu-id="e8b17-127">Właściwości strefy zapisu są obecnie ograniczone do [usługi Azure Resource Manager "tagów" dla zasobu strefy](dns-zones-records.md#tags).</span><span class="sxs-lookup"><span data-stu-id="e8b17-127">The writable zone properties are currently limited to the [Azure Resource Manager ‘tags’ for the zone resource](dns-zones-records.md#tags).</span></span>

<span data-ttu-id="e8b17-128">Użyj jednej z dwóch sposobów do aktualizacji strefy DNS:</span><span class="sxs-lookup"><span data-stu-id="e8b17-128">Use one of the following two ways to update a DNS zone:</span></span>

### <a name="specify-the-zone-using-the-zone-name-and-resource-group"></a><span data-ttu-id="e8b17-129">Określ strefę za pomocą grupy strefy nazwy i zasobów</span><span class="sxs-lookup"><span data-stu-id="e8b17-129">Specify the zone using the zone name and resource group</span></span>

<span data-ttu-id="e8b17-130">Ta metoda zastępuje istniejące znaczniki strefy podane wartości.</span><span class="sxs-lookup"><span data-stu-id="e8b17-130">This approach replaces the existing zone tags with the values specified.</span></span>

```powershell
Set-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

### <a name="specify-the-zone-using-a-zone-object"></a><span data-ttu-id="e8b17-131">Określ strefę za pomocą obiektu $zone</span><span class="sxs-lookup"><span data-stu-id="e8b17-131">Specify the zone using a $zone object</span></span>

<span data-ttu-id="e8b17-132">Takie podejście pobiera istniejący obiekt strefy, modyfikuje tagi, a następnie zatwierdza zmiany.</span><span class="sxs-lookup"><span data-stu-id="e8b17-132">This approach retrieves the existing zone object, modifies the tags, and then commits the changes.</span></span> <span data-ttu-id="e8b17-133">W ten sposób istniejące znaczniki będzie możliwe.</span><span class="sxs-lookup"><span data-stu-id="e8b17-133">In this way, existing tags can be preserved.</span></span>

```powershell
# Get the zone object
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup

# Remove an existing tag
$zone.Tags.Remove("project")

# Add a new tag
$zone.Tags.Add("status","approved")

# Commit changes
Set-AzureRmDnsZone -Zone $zone
```

<span data-ttu-id="e8b17-134">Korzystając z `Set-AzureRmDnsZone` z obiektem $zone [sprawdza Etag](dns-zones-records.md#etags) są używane do zapewnienia równoległe zmiany nie zostaną zastąpione.</span><span class="sxs-lookup"><span data-stu-id="e8b17-134">When using `Set-AzureRmDnsZone` with a $zone object, [Etag checks](dns-zones-records.md#etags) are used to ensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="e8b17-135">Można użyć opcjonalnego `-Overwrite` przełącznik, aby pominąć kontrole.</span><span class="sxs-lookup"><span data-stu-id="e8b17-135">You can use the optional `-Overwrite` switch to suppress these checks.</span></span>

## <a name="delete-a-dns-zone"></a><span data-ttu-id="e8b17-136">Usuń strefę DNS</span><span class="sxs-lookup"><span data-stu-id="e8b17-136">Delete a DNS Zone</span></span>

<span data-ttu-id="e8b17-137">Można usunąć strefy DNS przy użyciu `Remove-AzureRmDnsZone` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e8b17-137">DNS zones can be deleted using the `Remove-AzureRmDnsZone` cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="e8b17-138">Usunięcie strefy DNS powoduje usunięcie wszystkich rekordów DNS w strefie.</span><span class="sxs-lookup"><span data-stu-id="e8b17-138">Deleting a DNS zone also deletes all DNS records within the zone.</span></span> <span data-ttu-id="e8b17-139">Tej operacji nie można cofnąć.</span><span class="sxs-lookup"><span data-stu-id="e8b17-139">This operation cannot be undone.</span></span> <span data-ttu-id="e8b17-140">Strefa DNS jest używana, usług za pomocą strefie zakończy się niepowodzeniem po usunięciu strefy.</span><span class="sxs-lookup"><span data-stu-id="e8b17-140">If the DNS zone is in use, services using the zone will fail when the zone is deleted.</span></span>
>
><span data-ttu-id="e8b17-141">Aby chronić przed usunięciem strefy przypadkowe, zobacz [jak chronić strefy DNS i rekordy](dns-protect-zones-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="e8b17-141">To protect against accidental zone deletion, see [How to protect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>


<span data-ttu-id="e8b17-142">Użyj jednej z dwóch sposobów można usunąć strefy DNS:</span><span class="sxs-lookup"><span data-stu-id="e8b17-142">Use one of the following two ways to delete a DNS zone:</span></span>

### <a name="specify-the-zone-using-the-zone-name-and-resource-group-name"></a><span data-ttu-id="e8b17-143">Określ strefę przy użyciu nazwy strefy i nazwy grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="e8b17-143">Specify the zone using the zone name and resource group name</span></span>

```powershell
Remove-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

### <a name="specify-the-zone-using-a-zone-object"></a><span data-ttu-id="e8b17-144">Określ strefę za pomocą obiektu $zone</span><span class="sxs-lookup"><span data-stu-id="e8b17-144">Specify the zone using a $zone object</span></span>

<span data-ttu-id="e8b17-145">Można określić strefy, które mają zostać usunięte przy użyciu `$zone` obiektu zwróconego przez `Get-AzureRmDnsZone`.</span><span class="sxs-lookup"><span data-stu-id="e8b17-145">You can specify the zone to be deleted using a `$zone` object returned by `Get-AzureRmDnsZone`.</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
Remove-AzureRmDnsZone -Zone $zone
```

<span data-ttu-id="e8b17-146">Obiekt strefy może również być przekazywane w potoku zamiast przekazywana jako parametr:</span><span class="sxs-lookup"><span data-stu-id="e8b17-146">The zone object can also be piped instead of being passed as a parameter:</span></span>

```powershell
Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup | Remove-AzureRmDnsZone

```

<span data-ttu-id="e8b17-147">Jak `Set-AzureRmDnsZone`, określając przy użyciu strefy `$zone` obiektu umożliwia Etag kontroli w celu zapewnienia, równoległe zmiany nie zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="e8b17-147">As with `Set-AzureRmDnsZone`, specifying the zone using a `$zone` object enables Etag checks to ensure concurrent changes are not deleted.</span></span> <span data-ttu-id="e8b17-148">Użyj `-Overwrite` przełącznik, aby pominąć kontrole.</span><span class="sxs-lookup"><span data-stu-id="e8b17-148">Use the `-Overwrite` switch to suppress these checks.</span></span>

## <a name="confirmation-prompts"></a><span data-ttu-id="e8b17-149">Monituje o potwierdzenie</span><span class="sxs-lookup"><span data-stu-id="e8b17-149">Confirmation prompts</span></span>

<span data-ttu-id="e8b17-150">`New-AzureRmDnsZone`, `Set-AzureRmDnsZone`, I `Remove-AzureRmDnsZone` o potwierdzenie obsługuje wszystkie polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e8b17-150">The `New-AzureRmDnsZone`, `Set-AzureRmDnsZone`, and `Remove-AzureRmDnsZone` cmdlets all support confirmation prompts.</span></span>

<span data-ttu-id="e8b17-151">Zarówno `New-AzureRmDnsZone` i `Set-AzureRmDnsZone` monituje o potwierdzenie, jeśli `$ConfirmPreference` PowerShell preferencji Zmienna ma wartość `Medium` lub niższej.</span><span class="sxs-lookup"><span data-stu-id="e8b17-151">Both `New-AzureRmDnsZone` and `Set-AzureRmDnsZone` prompt for confirmation if the `$ConfirmPreference` PowerShell preference variable has a value of `Medium` or lower.</span></span> <span data-ttu-id="e8b17-152">Z powodu potencjalnie duże znaczenie usunięcia strefę DNS `Remove-AzureRmDnsZone` polecenie cmdlet monituje o potwierdzenie, jeśli `$ConfirmPreference` PowerShell zmienna ma żadnej wartości innych niż `None`.</span><span class="sxs-lookup"><span data-stu-id="e8b17-152">Due to the potentially high impact of deleting a DNS zone, the `Remove-AzureRmDnsZone` cmdlet prompts for confirmation if the `$ConfirmPreference` PowerShell variable has any value other than `None`.</span></span>

<span data-ttu-id="e8b17-153">Ponieważ domyślna wartość `$ConfirmPreference` jest `High`, tylko `Remove-AzureRmDnsZone` monituje o potwierdzenie domyślnie.</span><span class="sxs-lookup"><span data-stu-id="e8b17-153">Since the default value for `$ConfirmPreference` is `High`, only `Remove-AzureRmDnsZone` prompts for confirmation by default.</span></span>

<span data-ttu-id="e8b17-154">Można zastąpić bieżącą `$ConfirmPreference` ustawienie przy użyciu `-Confirm` parametru.</span><span class="sxs-lookup"><span data-stu-id="e8b17-154">You can override the current `$ConfirmPreference` setting using the `-Confirm` parameter.</span></span> <span data-ttu-id="e8b17-155">Jeśli określisz `-Confirm` lub `-Confirm:$True` , polecenie cmdlet monituje o potwierdzenie przed go uruchamia.</span><span class="sxs-lookup"><span data-stu-id="e8b17-155">If you specify `-Confirm` or `-Confirm:$True` , the cmdlet prompts you for confirmation before it runs.</span></span> <span data-ttu-id="e8b17-156">Jeśli określisz `-Confirm:$False` , polecenie cmdlet monituje o potwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="e8b17-156">If you specify `-Confirm:$False` , the cmdlet does not prompt you for confirmation.</span></span>

<span data-ttu-id="e8b17-157">Aby uzyskać więcej informacji na temat `-Confirm` i `$ConfirmPreference`, zobacz [o zmiennych preferencji](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span><span class="sxs-lookup"><span data-stu-id="e8b17-157">For more information about `-Confirm` and `$ConfirmPreference`, see [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e8b17-158">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e8b17-158">Next steps</span></span>

<span data-ttu-id="e8b17-159">Dowiedz się, jak [zarządzać zestawów rekordów i rekordami](dns-operations-recordsets.md) w strefie DNS.</span><span class="sxs-lookup"><span data-stu-id="e8b17-159">Learn how to [manage record sets and records](dns-operations-recordsets.md) in your DNS zone.</span></span>
<br>
<span data-ttu-id="e8b17-160">Dowiedz się, jak [Delegowanie domeny do usługi Azure DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="e8b17-160">Learn how to [delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>
<br>
<span data-ttu-id="e8b17-161">Przegląd [dokumentacji programu PowerShell usługi Azure DNS](/powershell/module/azurerm.dns).</span><span class="sxs-lookup"><span data-stu-id="e8b17-161">Review the [Azure DNS PowerShell reference documentation](/powershell/module/azurerm.dns).</span></span>

