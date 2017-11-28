---
title: "aaaManage DNS strefy w usłudze Azure DNS - Azure CLI 1.0 | Dokumentacja firmy Microsoft"
description: "Możesz zarządzać stref DNS przy użyciu interfejsu wiersza polecenia platformy Azure w wersji 1.0. W tym artykule przedstawiono sposób tooupdate, usunąć i utworzyć strefy DNS w usłudze Azure DNS."
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
ms.openlocfilehash: cb9790cc46626ef7f38a43edb57511104fe6057e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-azure-dns-using-hello-azure-cli-10"></a><span data-ttu-id="ffab9-104">Jak toomanage strefy DNS w usłudze Azure DNS przy użyciu hello Azure CLI w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="ffab9-104">How toomanage DNS Zones in Azure DNS using hello Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ffab9-105">Portal</span><span class="sxs-lookup"><span data-stu-id="ffab9-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="ffab9-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ffab9-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="ffab9-107">Interfejs wiersza polecenia platformy Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="ffab9-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="ffab9-108">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="ffab9-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="ffab9-109">Ten przewodnik przedstawia, jak toomanage serwery DNS strefy za pomocą wieloplatformowych hello Azure CLI 1.0, która jest dostępna dla systemu Windows, Mac i Linux.</span><span class="sxs-lookup"><span data-stu-id="ffab9-109">This guide shows how toomanage your DNS zones by using hello cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="ffab9-110">Można również zarządzać stref DNS przy użyciu [programu Azure PowerShell](dns-operations-dnszones.md) lub hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ffab9-110">You can also manage your DNS zones using [Azure PowerShell](dns-operations-dnszones.md) or hello Azure portal.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="ffab9-111">Zadanie hello toocomplete wersje interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="ffab9-111">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="ffab9-112">Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="ffab9-112">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="ffab9-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania modele wdrażania.</span><span class="sxs-lookup"><span data-stu-id="ffab9-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) - our CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="ffab9-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="ffab9-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) - our next generation CLI for hello resource management deployment model.</span></span>

## <a name="introduction"></a><span data-ttu-id="ffab9-115">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="ffab9-115">Introduction</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-cli-setup](../../includes/dns-cli-setup-include.md)]

## <a name="getting-help"></a><span data-ttu-id="ffab9-116">Uzyskiwanie pomocy</span><span class="sxs-lookup"><span data-stu-id="ffab9-116">Getting help</span></span>

<span data-ttu-id="ffab9-117">Wszystkie polecenia 1.0 interfejsu wiersza polecenia dotyczące tooAzure DNS rozpoczynać `azure network dns`.</span><span class="sxs-lookup"><span data-stu-id="ffab9-117">All CLI 1.0 commands relating tooAzure DNS start with `azure network dns`.</span></span> <span data-ttu-id="ffab9-118">Pomoc jest dostępna dla każdego polecenia za pomocą hello `--help` opcji (forma krótka `-h`).</span><span class="sxs-lookup"><span data-stu-id="ffab9-118">Help is available for each command using hello `--help` option (short form `-h`).</span></span>  <span data-ttu-id="ffab9-119">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="ffab9-119">For example:</span></span>

```azurecli
azure network dns -h
azure network dns zone -h
azure network dns zone create -h
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="ffab9-120">Tworzenie strefy DNS</span><span class="sxs-lookup"><span data-stu-id="ffab9-120">Create a DNS zone</span></span>

<span data-ttu-id="ffab9-121">Strefa DNS jest tworzony przy użyciu hello `azure network dns zone create` polecenia.</span><span class="sxs-lookup"><span data-stu-id="ffab9-121">A DNS zone is created using hello `azure network dns zone create` command.</span></span> <span data-ttu-id="ffab9-122">Aby uzyskać pomoc, zobacz `azure network dns zone create -h`.</span><span class="sxs-lookup"><span data-stu-id="ffab9-122">For help, see `azure network dns zone create -h`.</span></span>

<span data-ttu-id="ffab9-123">Witaj poniższy przykład tworzy strefę DNS o nazwie *contoso.com* w hello grupy zasobów o nazwie *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="ffab9-123">hello following example creates a DNS zone called *contoso.com* in hello resource group called *MyResourceGroup*:</span></span>

```azurecli
azure network dns zone create MyResourceGroup contoso.com
```

### <a name="toocreate-a-dns-zone-with-tags"></a><span data-ttu-id="ffab9-124">toocreate strefy DNS przy użyciu tagów</span><span class="sxs-lookup"><span data-stu-id="ffab9-124">toocreate a DNS zone with tags</span></span>

<span data-ttu-id="ffab9-125">Hello poniższy przykład przedstawia sposób toocreate DNS strefy przy użyciu dwóch [znaczniki usługi Azure Resource Manager](dns-zones-records.md#tags), *project = demo* i *env = test*, za pomocą hello `--tags` parametr (forma krótka `-t`):</span><span class="sxs-lookup"><span data-stu-id="ffab9-125">hello following example shows how toocreate a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*, by using hello `--tags` parameter (short form `-t`):</span></span>

```azurecli
azure network dns zone create MyResourceGroup contoso.com -t "project=demo";"env=test"
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="ffab9-126">Pobierz strefę DNS</span><span class="sxs-lookup"><span data-stu-id="ffab9-126">Get a DNS zone</span></span>

<span data-ttu-id="ffab9-127">Użyj tooretrieve strefę DNS `azure network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="ffab9-127">tooretrieve a DNS zone, use `azure network dns zone show`.</span></span> <span data-ttu-id="ffab9-128">Aby uzyskać pomoc, zobacz `azure network dns zone show -h`.</span><span class="sxs-lookup"><span data-stu-id="ffab9-128">For help, see `azure network dns zone show -h`.</span></span>

<span data-ttu-id="ffab9-129">Witaj poniższy przykład zwraca strefę DNS hello *contoso.com* i skojarzonych danych z grupy zasobów *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="ffab9-129">hello following example returns hello DNS zone *contoso.com* and its associated data from resource group *MyResourceGroup*.</span></span> 

```azurecli
azure network dns zone show MyResourceGroup contoso.com
```

<span data-ttu-id="ffab9-130">Poniższy przykład Hello jest hello odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="ffab9-130">hello following example is hello response.</span></span>

```
info:    Executing command network dns zone show
+ Looking up hello dns zone "contoso.com"
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

<span data-ttu-id="ffab9-131">Należy pamiętać, że rekordy DNS nie są zwracane przez `azure network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="ffab9-131">Note that DNS records are not returned by `azure network dns zone show`.</span></span> <span data-ttu-id="ffab9-132">toolist rekordy DNS, użyj `azure network dns record-set list`.</span><span class="sxs-lookup"><span data-stu-id="ffab9-132">toolist DNS records, use `azure network dns record-set list`.</span></span>


## <a name="list-dns-zones"></a><span data-ttu-id="ffab9-133">Lista stref DNS</span><span class="sxs-lookup"><span data-stu-id="ffab9-133">List DNS zones</span></span>

<span data-ttu-id="ffab9-134">tooenumerate stref DNS, użyj `azure network dns zone list`.</span><span class="sxs-lookup"><span data-stu-id="ffab9-134">tooenumerate DNS zones, use `azure network dns zone list`.</span></span> <span data-ttu-id="ffab9-135">Aby uzyskać pomoc, zobacz `azure network dns zone list -h`.</span><span class="sxs-lookup"><span data-stu-id="ffab9-135">For help, see `azure network dns zone list -h`.</span></span>

<span data-ttu-id="ffab9-136">Określanie grupy zasobów hello wyświetla tylko tych stref w grupie zasobów hello:</span><span class="sxs-lookup"><span data-stu-id="ffab9-136">Specifying hello resource group lists only those zones within hello resource group:</span></span>

```azurecli
azure network dns zone list MyResourceGroup
```

<span data-ttu-id="ffab9-137">Pominięcie hello grupa zasobów zawiera listę wszystkich stref w subskrypcji hello:</span><span class="sxs-lookup"><span data-stu-id="ffab9-137">Omitting hello resource group lists all zones in hello subscription:</span></span>

```azurecli
azure network dns zone list 
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="ffab9-138">Zaktualizuj strefę DNS</span><span class="sxs-lookup"><span data-stu-id="ffab9-138">Update a DNS zone</span></span>

<span data-ttu-id="ffab9-139">Zmiany tooa zasobów strefy DNS będzie możliwe przy użyciu `azure network dns zone set`.</span><span class="sxs-lookup"><span data-stu-id="ffab9-139">Changes tooa DNS zone resource can be made using `azure network dns zone set`.</span></span> <span data-ttu-id="ffab9-140">Aby uzyskać pomoc, zobacz `azure network dns zone set -h`.</span><span class="sxs-lookup"><span data-stu-id="ffab9-140">For help, see `azure network dns zone set -h`.</span></span>

<span data-ttu-id="ffab9-141">To polecenie nie powoduje aktualizacji hello zestawów rekordów DNS w strefie hello (zobacz [jak rekordy DNS tooManage](dns-operations-recordsets-cli-nodejs.md)).</span><span class="sxs-lookup"><span data-stu-id="ffab9-141">This command does not update any of hello DNS record sets within hello zone (see [How tooManage DNS records](dns-operations-recordsets-cli-nodejs.md)).</span></span> <span data-ttu-id="ffab9-142">Jest tylko tooupdate używanych właściwości zasobu strefy hello, sama.</span><span class="sxs-lookup"><span data-stu-id="ffab9-142">It is only used tooupdate properties of hello zone resource itself.</span></span> <span data-ttu-id="ffab9-143">Te właściwości są obecnie ograniczone toohello [usługi Azure Resource Manager "tagi"](dns-zones-records.md#tags) hello strefy zasobu.</span><span class="sxs-lookup"><span data-stu-id="ffab9-143">These properties are currently limited toohello [Azure Resource Manager 'tags'](dns-zones-records.md#tags) for hello zone resource.</span></span>

<span data-ttu-id="ffab9-144">Witaj poniższy przykład przedstawia sposób tooupdate hello znaczniki strefy DNS.</span><span class="sxs-lookup"><span data-stu-id="ffab9-144">hello following example shows how tooupdate hello tags on a DNS zone.</span></span> <span data-ttu-id="ffab9-145">znaczniki istniejących Hello są zastępowane przez hello wybrana.</span><span class="sxs-lookup"><span data-stu-id="ffab9-145">hello existing tags are replaced by hello value specified.</span></span>

```azurecli
azure network dns zone set MyResourceGroup contoso.com -t "team=support"
```

## <a name="delete-a-dns-zone"></a><span data-ttu-id="ffab9-146">Usuń strefę DNS</span><span class="sxs-lookup"><span data-stu-id="ffab9-146">Delete a DNS Zone</span></span>

<span data-ttu-id="ffab9-147">Można usunąć strefy DNS przy użyciu `azure network dns zone delete`.</span><span class="sxs-lookup"><span data-stu-id="ffab9-147">DNS zones can be deleted using `azure network dns zone delete`.</span></span> <span data-ttu-id="ffab9-148">Aby uzyskać pomoc, zobacz `azure network dns zone delete -h`.</span><span class="sxs-lookup"><span data-stu-id="ffab9-148">For help, see `azure network dns zone delete -h`.</span></span>

> [!NOTE]
> <span data-ttu-id="ffab9-149">Usunięcie strefy DNS powoduje usunięcie wszystkich rekordów DNS w strefie hello.</span><span class="sxs-lookup"><span data-stu-id="ffab9-149">Deleting a DNS zone also deletes all DNS records within hello zone.</span></span> <span data-ttu-id="ffab9-150">Tej operacji nie można cofnąć.</span><span class="sxs-lookup"><span data-stu-id="ffab9-150">This operation cannot be undone.</span></span> <span data-ttu-id="ffab9-151">Strefa DNS hello jest używany, usługi przy użyciu strefy hello zakończy się niepowodzeniem po usunięciu hello strefy.</span><span class="sxs-lookup"><span data-stu-id="ffab9-151">If hello DNS zone is in use, services using hello zone will fail when hello zone is deleted.</span></span>
>
><span data-ttu-id="ffab9-152">Zobacz tooprotect przed usunięciem strefy przypadkowemu [jak tooprotect DNS strefy i rejestruje](dns-protect-zones-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="ffab9-152">tooprotect against accidental zone deletion, see [How tooprotect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>

<span data-ttu-id="ffab9-153">To polecenie wyświetla monit o potwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="ffab9-153">This command prompts for confirmation.</span></span> <span data-ttu-id="ffab9-154">opcjonalne Hello `--quiet` przełącznika (forma krótka `-q`) pomija tego wiersza.</span><span class="sxs-lookup"><span data-stu-id="ffab9-154">hello optional `--quiet` switch (short form `-q`) suppresses this prompt.</span></span>

<span data-ttu-id="ffab9-155">Witaj poniższy przykład przedstawia sposób toodelete hello strefy *contoso.com* z grupy zasobów *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="ffab9-155">hello following example shows how toodelete hello zone *contoso.com* from resource group *MyResourceGroup*.</span></span>

```azurecli
azure network dns zone delete MyResourceGroup contoso.com
```

## <a name="next-steps"></a><span data-ttu-id="ffab9-156">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ffab9-156">Next steps</span></span>

<span data-ttu-id="ffab9-157">Dowiedz się, jak za[zarządzać zestawów rekordów i rekordami](dns-getstarted-create-recordset-cli-nodejs.md) w strefie DNS.</span><span class="sxs-lookup"><span data-stu-id="ffab9-157">Learn how too[manage record sets and records](dns-getstarted-create-recordset-cli-nodejs.md) in your DNS zone.</span></span>

<span data-ttu-id="ffab9-158">Dowiedz się, jak za[delegować tooAzure Twojego domeny DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="ffab9-158">Learn how too[delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>

