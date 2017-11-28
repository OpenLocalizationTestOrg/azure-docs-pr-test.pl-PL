---
title: "aaaManage DNS strefy w usłudze Azure DNS - PowerShell | Dokumentacja firmy Microsoft"
description: "Możesz zarządzać stref DNS przy użyciu programu Azure Powershell. W tym artykule opisano sposób tooupdate, usunąć i utworzyć strefy DNS w usłudze Azure DNS"
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
ms.openlocfilehash: 261b89f72213aa9784034d47ff9d1c55a4e80d65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-using-powershell"></a><span data-ttu-id="4500a-104">Jak toomanage stref DNS przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="4500a-104">How toomanage DNS Zones using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4500a-105">Portal</span><span class="sxs-lookup"><span data-stu-id="4500a-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="4500a-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4500a-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="4500a-107">Interfejs wiersza polecenia platformy Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="4500a-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="4500a-108">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="4500a-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="4500a-109">W tym artykule opisano, jak toomanage serwery DNS strefy przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4500a-109">This article shows you how toomanage your DNS zones by using Azure PowerShell.</span></span> <span data-ttu-id="4500a-110">Można również zarządzać stref DNS przy użyciu wieloplatformowych hello [interfejsu wiersza polecenia Azure](dns-operations-dnszones-cli.md) lub hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="4500a-110">You can also manage your DNS zones using hello cross-platform [Azure CLI](dns-operations-dnszones-cli.md) or hello Azure portal.</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-powershell-setup](../../includes/dns-powershell-setup-include.md)]


## <a name="create-a-dns-zone"></a><span data-ttu-id="4500a-111">Tworzenie strefy DNS</span><span class="sxs-lookup"><span data-stu-id="4500a-111">Create a DNS zone</span></span>

<span data-ttu-id="4500a-112">Strefa DNS jest tworzona przy użyciu hello `New-AzureRmDnsZone` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4500a-112">A DNS zone is created by using hello `New-AzureRmDnsZone` cmdlet.</span></span>

<span data-ttu-id="4500a-113">Witaj poniższy przykład tworzy strefę DNS o nazwie *contoso.com* w hello grupy zasobów o nazwie *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="4500a-113">hello following example creates a DNS zone called *contoso.com* in hello resource group called *MyResourceGroup*:</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

<span data-ttu-id="4500a-114">Hello poniższy przykład przedstawia sposób toocreate DNS strefy przy użyciu dwóch [znaczniki usługi Azure Resource Manager](dns-zones-records.md#tags), *project = demo* i *env = test*:</span><span class="sxs-lookup"><span data-stu-id="4500a-114">hello following example shows how toocreate a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*:</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="4500a-115">Pobierz strefę DNS</span><span class="sxs-lookup"><span data-stu-id="4500a-115">Get a DNS zone</span></span>

<span data-ttu-id="4500a-116">tooretrieve strefy DNS, użyj hello `Get-AzureRmDnsZone` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4500a-116">tooretrieve a DNS zone, use hello `Get-AzureRmDnsZone` cmdlet.</span></span> <span data-ttu-id="4500a-117">Ta operacja zwraca obiekt odpowiadającą tooan istniejących strefę w usłudze Azure DNS strefy DNS.</span><span class="sxs-lookup"><span data-stu-id="4500a-117">This operation returns a DNS zone object corresponding tooan existing zone in Azure DNS.</span></span> <span data-ttu-id="4500a-118">Witaj obiekt zawiera dane dotyczące hello strefy (na przykład hello liczba zestawów rekordów), ale nie zawiera zestawów rekordów hello sami (zobacz `Get-AzureRmDnsRecordSet`).</span><span class="sxs-lookup"><span data-stu-id="4500a-118">hello object contains data about hello zone (such as hello number of record sets), but does not contain hello record sets themselves (see `Get-AzureRmDnsRecordSet`).</span></span>

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

## <a name="list-dns-zones"></a><span data-ttu-id="4500a-119">Lista stref DNS</span><span class="sxs-lookup"><span data-stu-id="4500a-119">List DNS zones</span></span>

<span data-ttu-id="4500a-120">Pomijając hello nazwę strefy z `Get-AzureRmDnsZone`, można wyliczyć wszystkich stref w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="4500a-120">By omitting hello zone name from `Get-AzureRmDnsZone`, you can enumerate all zones in a resource group.</span></span> <span data-ttu-id="4500a-121">Ta operacja zwraca tablicę obiektów stref.</span><span class="sxs-lookup"><span data-stu-id="4500a-121">This operation returns an array of zone objects.</span></span>

```powershell
$zoneList = Get-AzureRmDnsZone -ResourceGroupName MyAzureResourceGroup
```

<span data-ttu-id="4500a-122">Pomijając hello Nazwa strefy i hello Nazwa grupy zasobów z `Get-AzureRmDnsZone`, można wyliczyć wszystkich stref w hello subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4500a-122">By omitting both hello zone name and hello resource group name from `Get-AzureRmDnsZone`, you can enumerate all zones in hello Azure subscription.</span></span>

```powershell
$zoneList = Get-AzureRmDnsZone
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="4500a-123">Zaktualizuj strefę DNS</span><span class="sxs-lookup"><span data-stu-id="4500a-123">Update a DNS zone</span></span>

<span data-ttu-id="4500a-124">Zmienia tooa zasobów strefy DNS może się przy użyciu `Set-AzureRmDnsZone`.</span><span class="sxs-lookup"><span data-stu-id="4500a-124">Changes tooa DNS zone resource can be made by using `Set-AzureRmDnsZone`.</span></span> <span data-ttu-id="4500a-125">To polecenie cmdlet nie zaktualizować hello zestawów rekordów DNS w strefie hello (zobacz [jak rekordy DNS tooManage](dns-operations-recordsets.md)).</span><span class="sxs-lookup"><span data-stu-id="4500a-125">This cmdlet does not update any of hello DNS record sets within hello zone (see [How tooManage DNS records](dns-operations-recordsets.md)).</span></span> <span data-ttu-id="4500a-126">Ma ona używana tylko właściwości tooupdate zasób strefy hello samej siebie.</span><span class="sxs-lookup"><span data-stu-id="4500a-126">It's only used tooupdate properties of hello zone resource itself.</span></span> <span data-ttu-id="4500a-127">właściwości strefy zapisywalny Hello są obecnie ograniczone toohello [usługi Azure Resource Manager "tagów" dla zasobu strefy hello](dns-zones-records.md#tags).</span><span class="sxs-lookup"><span data-stu-id="4500a-127">hello writable zone properties are currently limited toohello [Azure Resource Manager ‘tags’ for hello zone resource](dns-zones-records.md#tags).</span></span>

<span data-ttu-id="4500a-128">Użyj jednej z następujących dwóch sposobów tooupdate hello strefę DNS:</span><span class="sxs-lookup"><span data-stu-id="4500a-128">Use one of hello following two ways tooupdate a DNS zone:</span></span>

### <a name="specify-hello-zone-using-hello-zone-name-and-resource-group"></a><span data-ttu-id="4500a-129">Określ strefę hello przy użyciu hello strefy nazwy i grupie zasobów</span><span class="sxs-lookup"><span data-stu-id="4500a-129">Specify hello zone using hello zone name and resource group</span></span>

<span data-ttu-id="4500a-130">Takie podejście zastępuje istniejące znaczniki strefy hello hello wartości.</span><span class="sxs-lookup"><span data-stu-id="4500a-130">This approach replaces hello existing zone tags with hello values specified.</span></span>

```powershell
Set-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

### <a name="specify-hello-zone-using-a-zone-object"></a><span data-ttu-id="4500a-131">Określ strefę hello przy użyciu obiektu $zone</span><span class="sxs-lookup"><span data-stu-id="4500a-131">Specify hello zone using a $zone object</span></span>

<span data-ttu-id="4500a-132">Takie podejście pobiera hello istniejący obiekt strefy, modyfikuje hello tagów, a następnie zatwierdza zmiany hello.</span><span class="sxs-lookup"><span data-stu-id="4500a-132">This approach retrieves hello existing zone object, modifies hello tags, and then commits hello changes.</span></span> <span data-ttu-id="4500a-133">W ten sposób istniejące znaczniki będzie możliwe.</span><span class="sxs-lookup"><span data-stu-id="4500a-133">In this way, existing tags can be preserved.</span></span>

```powershell
# Get hello zone object
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup

# Remove an existing tag
$zone.Tags.Remove("project")

# Add a new tag
$zone.Tags.Add("status","approved")

# Commit changes
Set-AzureRmDnsZone -Zone $zone
```

<span data-ttu-id="4500a-134">Korzystając z `Set-AzureRmDnsZone` z obiektem $zone [sprawdza Etag](dns-zones-records.md#etags) służą tooensure równoległe zmiany nie zostaną zastąpione.</span><span class="sxs-lookup"><span data-stu-id="4500a-134">When using `Set-AzureRmDnsZone` with a $zone object, [Etag checks](dns-zones-records.md#etags) are used tooensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="4500a-135">Można opcjonalnie hello `-Overwrite` przełącznika toosuppress kontrole.</span><span class="sxs-lookup"><span data-stu-id="4500a-135">You can use hello optional `-Overwrite` switch toosuppress these checks.</span></span>

## <a name="delete-a-dns-zone"></a><span data-ttu-id="4500a-136">Usuń strefę DNS</span><span class="sxs-lookup"><span data-stu-id="4500a-136">Delete a DNS Zone</span></span>

<span data-ttu-id="4500a-137">Można usunąć strefy DNS przy użyciu hello `Remove-AzureRmDnsZone` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4500a-137">DNS zones can be deleted using hello `Remove-AzureRmDnsZone` cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="4500a-138">Usunięcie strefy DNS powoduje usunięcie wszystkich rekordów DNS w strefie hello.</span><span class="sxs-lookup"><span data-stu-id="4500a-138">Deleting a DNS zone also deletes all DNS records within hello zone.</span></span> <span data-ttu-id="4500a-139">Tej operacji nie można cofnąć.</span><span class="sxs-lookup"><span data-stu-id="4500a-139">This operation cannot be undone.</span></span> <span data-ttu-id="4500a-140">Strefa DNS hello jest używany, usługi przy użyciu strefy hello zakończy się niepowodzeniem po usunięciu hello strefy.</span><span class="sxs-lookup"><span data-stu-id="4500a-140">If hello DNS zone is in use, services using hello zone will fail when hello zone is deleted.</span></span>
>
><span data-ttu-id="4500a-141">Zobacz tooprotect przed usunięciem strefy przypadkowemu [jak tooprotect DNS strefy i rejestruje](dns-protect-zones-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="4500a-141">tooprotect against accidental zone deletion, see [How tooprotect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>


<span data-ttu-id="4500a-142">Użyj jednej z następujących dwóch sposobów toodelete hello strefę DNS:</span><span class="sxs-lookup"><span data-stu-id="4500a-142">Use one of hello following two ways toodelete a DNS zone:</span></span>

### <a name="specify-hello-zone-using-hello-zone-name-and-resource-group-name"></a><span data-ttu-id="4500a-143">Określ strefę hello przy użyciu nazwy strefy hello i nazwa grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="4500a-143">Specify hello zone using hello zone name and resource group name</span></span>

```powershell
Remove-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

### <a name="specify-hello-zone-using-a-zone-object"></a><span data-ttu-id="4500a-144">Określ strefę hello przy użyciu obiektu $zone</span><span class="sxs-lookup"><span data-stu-id="4500a-144">Specify hello zone using a $zone object</span></span>

<span data-ttu-id="4500a-145">Można określić toobe strefy hello usunąć przy użyciu `$zone` obiektu zwróconego przez `Get-AzureRmDnsZone`.</span><span class="sxs-lookup"><span data-stu-id="4500a-145">You can specify hello zone toobe deleted using a `$zone` object returned by `Get-AzureRmDnsZone`.</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
Remove-AzureRmDnsZone -Zone $zone
```

<span data-ttu-id="4500a-146">Obiekt strefy Hello również mogą być przetwarzane potokowo zamiast przekazywana jako parametr:</span><span class="sxs-lookup"><span data-stu-id="4500a-146">hello zone object can also be piped instead of being passed as a parameter:</span></span>

```powershell
Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup | Remove-AzureRmDnsZone

```

<span data-ttu-id="4500a-147">Jak `Set-AzureRmDnsZone`, określając hello strefy przy użyciu `$zone` obiektu umożliwia Etag sprawdza tooensure równoległe zmiany nie zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="4500a-147">As with `Set-AzureRmDnsZone`, specifying hello zone using a `$zone` object enables Etag checks tooensure concurrent changes are not deleted.</span></span> <span data-ttu-id="4500a-148">Użyj hello `-Overwrite` przełącznika toosuppress kontrole.</span><span class="sxs-lookup"><span data-stu-id="4500a-148">Use hello `-Overwrite` switch toosuppress these checks.</span></span>

## <a name="confirmation-prompts"></a><span data-ttu-id="4500a-149">Monituje o potwierdzenie</span><span class="sxs-lookup"><span data-stu-id="4500a-149">Confirmation prompts</span></span>

<span data-ttu-id="4500a-150">Witaj `New-AzureRmDnsZone`, `Set-AzureRmDnsZone`, i `Remove-AzureRmDnsZone` o potwierdzenie obsługuje wszystkie polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4500a-150">hello `New-AzureRmDnsZone`, `Set-AzureRmDnsZone`, and `Remove-AzureRmDnsZone` cmdlets all support confirmation prompts.</span></span>

<span data-ttu-id="4500a-151">Zarówno `New-AzureRmDnsZone` i `Set-AzureRmDnsZone` monituje o potwierdzenie, jeśli hello `$ConfirmPreference` PowerShell preferencji Zmienna ma wartość `Medium` lub niższej.</span><span class="sxs-lookup"><span data-stu-id="4500a-151">Both `New-AzureRmDnsZone` and `Set-AzureRmDnsZone` prompt for confirmation if hello `$ConfirmPreference` PowerShell preference variable has a value of `Medium` or lower.</span></span> <span data-ttu-id="4500a-152">Powodu toohello potencjalnie duże znaczenie usunięcia strefę DNS hello `Remove-AzureRmDnsZone` polecenie cmdlet monituje o potwierdzenie, jeśli hello `$ConfirmPreference` PowerShell zmienna ma żadnej wartości innych niż `None`.</span><span class="sxs-lookup"><span data-stu-id="4500a-152">Due toohello potentially high impact of deleting a DNS zone, hello `Remove-AzureRmDnsZone` cmdlet prompts for confirmation if hello `$ConfirmPreference` PowerShell variable has any value other than `None`.</span></span>

<span data-ttu-id="4500a-153">Ponieważ hello wartości domyślnej dla `$ConfirmPreference` jest `High`, tylko `Remove-AzureRmDnsZone` monituje o potwierdzenie domyślnie.</span><span class="sxs-lookup"><span data-stu-id="4500a-153">Since hello default value for `$ConfirmPreference` is `High`, only `Remove-AzureRmDnsZone` prompts for confirmation by default.</span></span>

<span data-ttu-id="4500a-154">Można zastąpić bieżący hello `$ConfirmPreference` ustawienie za pomocą hello `-Confirm` parametru.</span><span class="sxs-lookup"><span data-stu-id="4500a-154">You can override hello current `$ConfirmPreference` setting using hello `-Confirm` parameter.</span></span> <span data-ttu-id="4500a-155">Jeśli określisz `-Confirm` lub `-Confirm:$True` , hello polecenie cmdlet monituje o potwierdzenie przed go uruchamia.</span><span class="sxs-lookup"><span data-stu-id="4500a-155">If you specify `-Confirm` or `-Confirm:$True` , hello cmdlet prompts you for confirmation before it runs.</span></span> <span data-ttu-id="4500a-156">Jeśli określisz `-Confirm:$False` , hello polecenie cmdlet monituje o potwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="4500a-156">If you specify `-Confirm:$False` , hello cmdlet does not prompt you for confirmation.</span></span>

<span data-ttu-id="4500a-157">Aby uzyskać więcej informacji na temat `-Confirm` i `$ConfirmPreference`, zobacz [o zmiennych preferencji](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span><span class="sxs-lookup"><span data-stu-id="4500a-157">For more information about `-Confirm` and `$ConfirmPreference`, see [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4500a-158">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4500a-158">Next steps</span></span>

<span data-ttu-id="4500a-159">Dowiedz się, jak za[zarządzać zestawów rekordów i rekordami](dns-operations-recordsets.md) w strefie DNS.</span><span class="sxs-lookup"><span data-stu-id="4500a-159">Learn how too[manage record sets and records](dns-operations-recordsets.md) in your DNS zone.</span></span>
<br>
<span data-ttu-id="4500a-160">Dowiedz się, jak za[delegować tooAzure Twojego domeny DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="4500a-160">Learn how too[delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>
<br>
<span data-ttu-id="4500a-161">Przejrzyj hello [dokumentacji programu PowerShell usługi Azure DNS](/powershell/module/azurerm.dns).</span><span class="sxs-lookup"><span data-stu-id="4500a-161">Review hello [Azure DNS PowerShell reference documentation](/powershell/module/azurerm.dns).</span></span>

