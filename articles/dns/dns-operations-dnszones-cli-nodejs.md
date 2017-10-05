---
title: "Zarządzanie strefami DNS w usłudze Azure DNS - Azure CLI 1.0 | Dokumentacja firmy Microsoft"
description: "Możesz zarządzać stref DNS przy użyciu interfejsu wiersza polecenia platformy Azure w wersji 1.0. W tym artykule pokazano, jak aktualizowanie, usuwanie i tworzenie stref DNS w usłudze Azure DNS."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 8ab63bc4-5135-4ed8-8c0b-5f0712b9afed
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/21/2016
ms.author: gwallace
ms.openlocfilehash: 588c87749f049eff5b9e0729f6769c8367ba41e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-dns-zones-in-azure-dns-using-the-azure-cli-10"></a><span data-ttu-id="6a9da-104">Jak zarządzać stref DNS w usłudze Azure DNS przy użyciu 1.0 interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="6a9da-104">How to manage DNS Zones in Azure DNS using the Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="6a9da-105">Portal</span><span class="sxs-lookup"><span data-stu-id="6a9da-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="6a9da-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6a9da-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="6a9da-107">Interfejs wiersza polecenia platformy Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="6a9da-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="6a9da-108">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="6a9da-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="6a9da-109">W tym przewodniku pokazano, jak zarządzać stref DNS przy użyciu 1.0 interfejsu wiersza polecenia platformy Azure i platform, która jest dostępna dla systemu Windows, Mac i Linux.</span><span class="sxs-lookup"><span data-stu-id="6a9da-109">This guide shows how to manage your DNS zones by using the cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="6a9da-110">Można również zarządzać stref DNS przy użyciu [programu Azure PowerShell](dns-operations-dnszones.md) lub w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6a9da-110">You can also manage your DNS zones using [Azure PowerShell](dns-operations-dnszones.md) or the Azure portal.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="6a9da-111">Wersje interfejsu wiersza polecenia umożliwiające wykonanie zadania</span><span class="sxs-lookup"><span data-stu-id="6a9da-111">CLI versions to complete the task</span></span>

<span data-ttu-id="6a9da-112">Zadanie można wykonać przy użyciu jednej z następujących wersji interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="6a9da-112">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="6a9da-113">[Interfejs wiersza polecenia platformy Azure 1.0](dns-operations-dnszones-cli-nodejs.md) — nasz interfejs wiersza polecenia dla klasycznego modelu wdrażania i modelu wdrażania na potrzeby zarządzania zasobami.</span><span class="sxs-lookup"><span data-stu-id="6a9da-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) - our CLI for the classic and resource management deployment models.</span></span>
* <span data-ttu-id="6a9da-114">[Interfejs wiersza polecenia platformy Azure 2.0](dns-operations-dnszones-cli.md) — nasz interfejs wiersza polecenia nowej generacji dla modelu wdrażania na potrzeby zarządzania zasobami.</span><span class="sxs-lookup"><span data-stu-id="6a9da-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) - our next generation CLI for the resource management deployment model.</span></span>

## <a name="introduction"></a><span data-ttu-id="6a9da-115">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="6a9da-115">Introduction</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-cli-setup](../../includes/dns-cli-setup-include.md)]

## <a name="getting-help"></a><span data-ttu-id="6a9da-116">Uzyskiwanie pomocy</span><span class="sxs-lookup"><span data-stu-id="6a9da-116">Getting help</span></span>

<span data-ttu-id="6a9da-117">Wszystkie polecenia interfejsu wiersza polecenia 1.0 odnoszących się do usługi Azure DNS rozpoczynać `azure network dns`.</span><span class="sxs-lookup"><span data-stu-id="6a9da-117">All CLI 1.0 commands relating to Azure DNS start with `azure network dns`.</span></span> <span data-ttu-id="6a9da-118">Pomoc jest dostępna dla każdego polecenia za pomocą `--help` opcji (forma krótka `-h`).</span><span class="sxs-lookup"><span data-stu-id="6a9da-118">Help is available for each command using the `--help` option (short form `-h`).</span></span>  <span data-ttu-id="6a9da-119">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="6a9da-119">For example:</span></span>

```azurecli
azure network dns -h
azure network dns zone -h
azure network dns zone create -h
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="6a9da-120">Tworzenie strefy DNS</span><span class="sxs-lookup"><span data-stu-id="6a9da-120">Create a DNS zone</span></span>

<span data-ttu-id="6a9da-121">Do tworzenia strefy DNS służy polecenie `azure network dns zone create`.</span><span class="sxs-lookup"><span data-stu-id="6a9da-121">A DNS zone is created using the `azure network dns zone create` command.</span></span> <span data-ttu-id="6a9da-122">Aby uzyskać pomoc, zobacz `azure network dns zone create -h`.</span><span class="sxs-lookup"><span data-stu-id="6a9da-122">For help, see `azure network dns zone create -h`.</span></span>

<span data-ttu-id="6a9da-123">Poniższy przykład tworzy strefę DNS o nazwie *contoso.com* w grupie zasobów o nazwie *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="6a9da-123">The following example creates a DNS zone called *contoso.com* in the resource group called *MyResourceGroup*:</span></span>

```azurecli
azure network dns zone create MyResourceGroup contoso.com
```

### <a name="to-create-a-dns-zone-with-tags"></a><span data-ttu-id="6a9da-124">Aby utworzyć strefę DNS za pomocą tagów</span><span class="sxs-lookup"><span data-stu-id="6a9da-124">To create a DNS zone with tags</span></span>

<span data-ttu-id="6a9da-125">Poniższy przykład przedstawia sposób tworzenia strefy DNS przy użyciu dwóch [znaczniki usługi Azure Resource Manager](dns-zones-records.md#tags), *projektu = demo* i *env = test*, za pomocą `--tags` parametr (forma krótka `-t`):</span><span class="sxs-lookup"><span data-stu-id="6a9da-125">The following example shows how to create a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*, by using the `--tags` parameter (short form `-t`):</span></span>

```azurecli
azure network dns zone create MyResourceGroup contoso.com -t "project=demo";"env=test"
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="6a9da-126">Pobierz strefę DNS</span><span class="sxs-lookup"><span data-stu-id="6a9da-126">Get a DNS zone</span></span>

<span data-ttu-id="6a9da-127">Aby uzyskać dostęp do strefy DNS, należy użyć `azure network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="6a9da-127">To retrieve a DNS zone, use `azure network dns zone show`.</span></span> <span data-ttu-id="6a9da-128">Aby uzyskać pomoc, zobacz `azure network dns zone show -h`.</span><span class="sxs-lookup"><span data-stu-id="6a9da-128">For help, see `azure network dns zone show -h`.</span></span>

<span data-ttu-id="6a9da-129">Poniższy przykład zwraca strefę DNS *contoso.com* i skojarzonych danych z grupy zasobów *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="6a9da-129">The following example returns the DNS zone *contoso.com* and its associated data from resource group *MyResourceGroup*.</span></span> 

```azurecli
azure network dns zone show MyResourceGroup contoso.com
```

<span data-ttu-id="6a9da-130">Odpowiedzią jest poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="6a9da-130">The following example is the response.</span></span>

```
info:    Executing command network dns zone show
+ Looking up the dns zone "contoso.com"
data:    Id                              : /subscriptions/.../contoso.com
data:    Name                            : contoso.com
data:    Type                            : Microsoft.Network/dnszones
data:    Location                        : global
data:    Number of record sets           : 2
data:    Max number of record sets       : 5000
data:    Name servers:
data:        ns1-01.azure-dns.com.
data:        ns2-01.azure-dns.net.
data:        ns3-01.azure-dns.org.
data:        ns4-01.azure-dns.info.
data:    Tags                            : project=demo;env=test
info:    network dns zone show command OK
```

<span data-ttu-id="6a9da-131">Należy pamiętać, że rekordy DNS nie są zwracane przez `azure network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="6a9da-131">Note that DNS records are not returned by `azure network dns zone show`.</span></span> <span data-ttu-id="6a9da-132">Aby wyświetlić listę rekordów DNS, użyj `azure network dns record-set list`.</span><span class="sxs-lookup"><span data-stu-id="6a9da-132">To list DNS records, use `azure network dns record-set list`.</span></span>


## <a name="list-dns-zones"></a><span data-ttu-id="6a9da-133">Lista stref DNS</span><span class="sxs-lookup"><span data-stu-id="6a9da-133">List DNS zones</span></span>

<span data-ttu-id="6a9da-134">Aby wyliczyć stref DNS, należy użyć `azure network dns zone list`.</span><span class="sxs-lookup"><span data-stu-id="6a9da-134">To enumerate DNS zones, use `azure network dns zone list`.</span></span> <span data-ttu-id="6a9da-135">Aby uzyskać pomoc, zobacz `azure network dns zone list -h`.</span><span class="sxs-lookup"><span data-stu-id="6a9da-135">For help, see `azure network dns zone list -h`.</span></span>

<span data-ttu-id="6a9da-136">Określenie grupy zasobów zawiera tylko tych stref w grupie zasobów:</span><span class="sxs-lookup"><span data-stu-id="6a9da-136">Specifying the resource group lists only those zones within the resource group:</span></span>

```azurecli
azure network dns zone list MyResourceGroup
```

<span data-ttu-id="6a9da-137">Pominięcie grupa zasobów zawiera listę wszystkich stref w subskrypcji:</span><span class="sxs-lookup"><span data-stu-id="6a9da-137">Omitting the resource group lists all zones in the subscription:</span></span>

```azurecli
azure network dns zone list 
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="6a9da-138">Zaktualizuj strefę DNS</span><span class="sxs-lookup"><span data-stu-id="6a9da-138">Update a DNS zone</span></span>

<span data-ttu-id="6a9da-139">Można wprowadzać zmiany do zasobu strefy DNS przy użyciu `azure network dns zone set`.</span><span class="sxs-lookup"><span data-stu-id="6a9da-139">Changes to a DNS zone resource can be made using `azure network dns zone set`.</span></span> <span data-ttu-id="6a9da-140">Aby uzyskać pomoc, zobacz `azure network dns zone set -h`.</span><span class="sxs-lookup"><span data-stu-id="6a9da-140">For help, see `azure network dns zone set -h`.</span></span>

<span data-ttu-id="6a9da-141">To polecenie nie powoduje aktualizacji zestawów rekordów DNS w strefie (zobacz [jak rekordy DNS zarządzanie](dns-operations-recordsets-cli-nodejs.md)).</span><span class="sxs-lookup"><span data-stu-id="6a9da-141">This command does not update any of the DNS record sets within the zone (see [How to Manage DNS records](dns-operations-recordsets-cli-nodejs.md)).</span></span> <span data-ttu-id="6a9da-142">Jest używane wyłącznie do właściwości zasobu strefy samej aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="6a9da-142">It is only used to update properties of the zone resource itself.</span></span> <span data-ttu-id="6a9da-143">Te właściwości są obecnie ograniczone do [usługi Azure Resource Manager "tagi"](dns-zones-records.md#tags) dla zasobu strefy.</span><span class="sxs-lookup"><span data-stu-id="6a9da-143">These properties are currently limited to the [Azure Resource Manager 'tags'](dns-zones-records.md#tags) for the zone resource.</span></span>

<span data-ttu-id="6a9da-144">Poniższy przykład przedstawia sposób aktualizowania elementów tag w strefie DNS.</span><span class="sxs-lookup"><span data-stu-id="6a9da-144">The following example shows how to update the tags on a DNS zone.</span></span> <span data-ttu-id="6a9da-145">Istniejące znaczniki zostały zastąpione przez określona wartość.</span><span class="sxs-lookup"><span data-stu-id="6a9da-145">The existing tags are replaced by the value specified.</span></span>

```azurecli
azure network dns zone set MyResourceGroup contoso.com -t "team=support"
```

## <a name="delete-a-dns-zone"></a><span data-ttu-id="6a9da-146">Usuń strefę DNS</span><span class="sxs-lookup"><span data-stu-id="6a9da-146">Delete a DNS Zone</span></span>

<span data-ttu-id="6a9da-147">Można usunąć strefy DNS przy użyciu `azure network dns zone delete`.</span><span class="sxs-lookup"><span data-stu-id="6a9da-147">DNS zones can be deleted using `azure network dns zone delete`.</span></span> <span data-ttu-id="6a9da-148">Aby uzyskać pomoc, zobacz `azure network dns zone delete -h`.</span><span class="sxs-lookup"><span data-stu-id="6a9da-148">For help, see `azure network dns zone delete -h`.</span></span>

> [!NOTE]
> <span data-ttu-id="6a9da-149">Usunięcie strefy DNS powoduje usunięcie wszystkich rekordów DNS w strefie.</span><span class="sxs-lookup"><span data-stu-id="6a9da-149">Deleting a DNS zone also deletes all DNS records within the zone.</span></span> <span data-ttu-id="6a9da-150">Tej operacji nie można cofnąć.</span><span class="sxs-lookup"><span data-stu-id="6a9da-150">This operation cannot be undone.</span></span> <span data-ttu-id="6a9da-151">Strefa DNS jest używana, usług za pomocą strefie zakończy się niepowodzeniem po usunięciu strefy.</span><span class="sxs-lookup"><span data-stu-id="6a9da-151">If the DNS zone is in use, services using the zone will fail when the zone is deleted.</span></span>
>
><span data-ttu-id="6a9da-152">Aby chronić przed usunięciem strefy przypadkowe, zobacz [jak chronić strefy DNS i rekordy](dns-protect-zones-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="6a9da-152">To protect against accidental zone deletion, see [How to protect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>

<span data-ttu-id="6a9da-153">To polecenie wyświetla monit o potwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="6a9da-153">This command prompts for confirmation.</span></span> <span data-ttu-id="6a9da-154">Opcjonalny `--quiet` przełącznika (forma krótka `-q`) powoduje pominięcie tego wiersza.</span><span class="sxs-lookup"><span data-stu-id="6a9da-154">The optional `--quiet` switch (short form `-q`) suppresses this prompt.</span></span>

<span data-ttu-id="6a9da-155">Poniższy przykład przedstawia sposób usunięcia strefy *contoso.com* z grupy zasobów *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="6a9da-155">The following example shows how to delete the zone *contoso.com* from resource group *MyResourceGroup*.</span></span>

```azurecli
azure network dns zone delete MyResourceGroup contoso.com
```

## <a name="next-steps"></a><span data-ttu-id="6a9da-156">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6a9da-156">Next steps</span></span>

<span data-ttu-id="6a9da-157">Dowiedz się, jak [zarządzać zestawów rekordów i rekordami](dns-getstarted-create-recordset-cli-nodejs.md) w strefie DNS.</span><span class="sxs-lookup"><span data-stu-id="6a9da-157">Learn how to [manage record sets and records](dns-getstarted-create-recordset-cli-nodejs.md) in your DNS zone.</span></span>

<span data-ttu-id="6a9da-158">Dowiedz się, jak [Delegowanie domeny do usługi Azure DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="6a9da-158">Learn how to [delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>

