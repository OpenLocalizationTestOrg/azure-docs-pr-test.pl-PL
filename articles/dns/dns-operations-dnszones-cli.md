---
title: "aaaManage DNS strefy w usłudze Azure DNS - Azure CLI 2.0 | Dokumentacja firmy Microsoft"
description: "Możesz zarządzać stref DNS używa interfejsu wiersza polecenia platformy Azure w wersji 2.0. W tym artykule przedstawiono sposób tooupdate, usunąć i utworzyć strefy DNS w usłudze Azure DNS."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 8ab63bc4-5135-4ed8-8c0b-5f0712b9afed
ms.service: dns
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: gwallace
ms.openlocfilehash: 3945a558b2db3490e50678d8395a47e55a85c8fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-azure-dns-using-hello-azure-cli-20"></a><span data-ttu-id="fa2d3-104">Jak toomanage strefy DNS w usłudze Azure DNS przy użyciu hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="fa2d3-104">How toomanage DNS Zones in Azure DNS using hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="fa2d3-105">Portal</span><span class="sxs-lookup"><span data-stu-id="fa2d3-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="fa2d3-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fa2d3-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="fa2d3-107">Interfejs wiersza polecenia platformy Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="fa2d3-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="fa2d3-108">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="fa2d3-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)


<span data-ttu-id="fa2d3-109">Ten przewodnik przedstawia, jak toomanage serwery DNS strefy za pomocą wieloplatformowych hello Azure CLI, która jest dostępna dla systemu Windows, Mac i Linux.</span><span class="sxs-lookup"><span data-stu-id="fa2d3-109">This guide shows how toomanage your DNS zones by using hello cross-platform Azure CLI, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="fa2d3-110">Można również zarządzać stref DNS przy użyciu [programu Azure PowerShell](dns-operations-dnszones.md) lub hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="fa2d3-110">You can also manage your DNS zones using [Azure PowerShell](dns-operations-dnszones.md) or hello Azure portal.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="fa2d3-111">Zadanie hello toocomplete wersje interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="fa2d3-111">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="fa2d3-112">Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="fa2d3-112">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="fa2d3-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania modele wdrażania.</span><span class="sxs-lookup"><span data-stu-id="fa2d3-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) - our CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="fa2d3-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="fa2d3-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) - our next generation CLI for hello resource management deployment model.</span></span>

## <a name="introduction"></a><span data-ttu-id="fa2d3-115">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="fa2d3-115">Introduction</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

## <a name="set-up-azure-cli-20-for-azure-dns"></a><span data-ttu-id="fa2d3-116">Konfigurowanie interfejsu wiersza polecenia platformy Azure 2.0 dla usługi Azure DNS</span><span class="sxs-lookup"><span data-stu-id="fa2d3-116">Set up Azure CLI 2.0 for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="fa2d3-117">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="fa2d3-117">Before you begin</span></span>

<span data-ttu-id="fa2d3-118">Sprawdź, czy masz hello poniższych elementach przed rozpoczęciem konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="fa2d3-118">Verify that you have hello following items before beginning your configuration.</span></span>

* <span data-ttu-id="fa2d3-119">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fa2d3-119">An Azure subscription.</span></span> <span data-ttu-id="fa2d3-120">Jeśli nie masz jeszcze subskrypcji platformy Azure, możesz aktywować [korzyści dla subskrybentów MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) lub utworzyć [bezpłatne konto](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fa2d3-120">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="fa2d3-121">Zainstaluj najnowszą wersję hello hello Azure CLI 2.0, dostępne dla systemu Windows, Linux lub MAC.</span><span class="sxs-lookup"><span data-stu-id="fa2d3-121">Install hello latest version of hello Azure CLI 2.0, available for Windows, Linux, or MAC.</span></span> <span data-ttu-id="fa2d3-122">Więcej informacji znajduje się w temacie [instalacji hello Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="fa2d3-122">More information is available at [Install hello Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

### <a name="sign-in-tooyour-azure-account"></a><span data-ttu-id="fa2d3-123">Zaloguj się tooyour konto platformy Azure</span><span class="sxs-lookup"><span data-stu-id="fa2d3-123">Sign in tooyour Azure account</span></span>

<span data-ttu-id="fa2d3-124">Otwórz okno konsoli i uwierzytelnij się przy użyciu swoich poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="fa2d3-124">Open a console window and authenticate with your credentials.</span></span> <span data-ttu-id="fa2d3-125">Aby uzyskać więcej informacji, zapoznaj się z dziennikiem w tooAzure z hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="fa2d3-125">For more information, see Log in tooAzure from hello Azure CLI</span></span>

```
az login
```

### <a name="select-hello-subscription"></a><span data-ttu-id="fa2d3-126">Wybierz subskrypcję hello</span><span class="sxs-lookup"><span data-stu-id="fa2d3-126">Select hello subscription</span></span>

<span data-ttu-id="fa2d3-127">Sprawdź subskrypcje hello hello konta.</span><span class="sxs-lookup"><span data-stu-id="fa2d3-127">Check hello subscriptions for hello account.</span></span>

```
az account list
```

<span data-ttu-id="fa2d3-128">Wybierz z toouse Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fa2d3-128">Choose which of your Azure subscriptions toouse.</span></span>

```azurecli
az account set --subscription "subscription name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="fa2d3-129">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="fa2d3-129">Create a resource group</span></span>

<span data-ttu-id="fa2d3-130">Usługa Azure Resource Manager wymaga, aby wszystkie grupy zasobów określały lokalizację.</span><span class="sxs-lookup"><span data-stu-id="fa2d3-130">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="fa2d3-131">Służy to jako hello domyślna lokalizacja dla zasobów w danej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="fa2d3-131">This is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="fa2d3-132">Jednak ponieważ wszystkie zasoby DNS są globalne, a nie regionalne, wybór hello lokalizacja grupy zasobów nie ma wpływu na usługi Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="fa2d3-132">However, because all DNS resources are global, not regional, hello choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="fa2d3-133">Ten krok można pominąć, jeśli używasz istniejącej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="fa2d3-133">You can skip this step if you are using an existing resource group.</span></span>

```azurecli
az group create --name myresourcegroup --location "West US"
```

## <a name="getting-help"></a><span data-ttu-id="fa2d3-134">Uzyskiwanie pomocy</span><span class="sxs-lookup"><span data-stu-id="fa2d3-134">Getting help</span></span>

<span data-ttu-id="fa2d3-135">Wszystkie polecenia 2.0 interfejsu wiersza polecenia dotyczące tooAzure DNS rozpoczynać `az network dns`.</span><span class="sxs-lookup"><span data-stu-id="fa2d3-135">All CLI 2.0 commands relating tooAzure DNS start with `az network dns`.</span></span> <span data-ttu-id="fa2d3-136">Pomoc jest dostępna dla każdego polecenia za pomocą hello `--help` opcji (forma krótka `-h`).</span><span class="sxs-lookup"><span data-stu-id="fa2d3-136">Help is available for each command using hello `--help` option (short form `-h`).</span></span>  <span data-ttu-id="fa2d3-137">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="fa2d3-137">For example:</span></span>

```azurecli
az network dns --help
az network dns zone --help
az network dns zone create --help
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="fa2d3-138">Tworzenie strefy DNS</span><span class="sxs-lookup"><span data-stu-id="fa2d3-138">Create a DNS zone</span></span>

<span data-ttu-id="fa2d3-139">Strefa DNS jest tworzony przy użyciu hello `az network dns zone create` polecenia.</span><span class="sxs-lookup"><span data-stu-id="fa2d3-139">A DNS zone is created using hello `az network dns zone create` command.</span></span> <span data-ttu-id="fa2d3-140">Aby uzyskać pomoc, zobacz `az network dns zone create -h`.</span><span class="sxs-lookup"><span data-stu-id="fa2d3-140">For help, see `az network dns zone create -h`.</span></span>

<span data-ttu-id="fa2d3-141">Witaj poniższy przykład tworzy strefę DNS o nazwie *contoso.com* w hello grupy zasobów o nazwie *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="fa2d3-141">hello following example creates a DNS zone called *contoso.com* in hello resource group called *MyResourceGroup*:</span></span>

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com
```

### <a name="toocreate-a-dns-zone-with-tags"></a><span data-ttu-id="fa2d3-142">toocreate strefy DNS przy użyciu tagów</span><span class="sxs-lookup"><span data-stu-id="fa2d3-142">toocreate a DNS zone with tags</span></span>

<span data-ttu-id="fa2d3-143">Hello poniższy przykład przedstawia sposób toocreate DNS strefy przy użyciu dwóch [znaczniki usługi Azure Resource Manager](dns-zones-records.md#tags), *project = demo* i *env = test*, za pomocą hello `--tags` parametr (forma krótka `-t`):</span><span class="sxs-lookup"><span data-stu-id="fa2d3-143">hello following example shows how toocreate a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*, by using hello `--tags` parameter (short form `-t`):</span></span>

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com --tags "project=demo" "env=test"
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="fa2d3-144">Pobierz strefę DNS</span><span class="sxs-lookup"><span data-stu-id="fa2d3-144">Get a DNS zone</span></span>

<span data-ttu-id="fa2d3-145">Użyj tooretrieve strefę DNS `az network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="fa2d3-145">tooretrieve a DNS zone, use `az network dns zone show`.</span></span> <span data-ttu-id="fa2d3-146">Aby uzyskać pomoc, zobacz `az network dns zone show --help`.</span><span class="sxs-lookup"><span data-stu-id="fa2d3-146">For help, see `az network dns zone show --help`.</span></span>

<span data-ttu-id="fa2d3-147">Witaj poniższy przykład zwraca strefę DNS hello *contoso.com* i skojarzonych danych z grupy zasobów *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="fa2d3-147">hello following example returns hello DNS zone *contoso.com* and its associated data from resource group *MyResourceGroup*.</span></span> 

```azurecli
az network dns zone show --resource-group myresourcegroup --name contoso.com
```

<span data-ttu-id="fa2d3-148">Poniższy przykład Hello jest hello odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="fa2d3-148">hello following example is hello response.</span></span>

```json
{
  "etag": "00000002-0000-0000-3d4d-64aa3689d201",
  "id": "/subscriptions/147a22e9-2356-4e56-b3de-1f5842ae4a3b/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "contoso.com",
  "nameServers": [
    "ns1-04.azure-dns.com.",
    "ns2-04.azure-dns.net.",
    "ns3-04.azure-dns.org.",
    "ns4-04.azure-dns.info."
  ],
  "numberOfRecordSets": 4,
  "resourceGroup": "myresourcegroup",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

<span data-ttu-id="fa2d3-149">Należy pamiętać, że rekordy DNS nie są zwracane przez `az network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="fa2d3-149">Note that DNS records are not returned by `az network dns zone show`.</span></span> <span data-ttu-id="fa2d3-150">toolist rekordy DNS, użyj `az network dns record-set list`.</span><span class="sxs-lookup"><span data-stu-id="fa2d3-150">toolist DNS records, use `az network dns record-set list`.</span></span>


## <a name="list-dns-zones"></a><span data-ttu-id="fa2d3-151">Lista stref DNS</span><span class="sxs-lookup"><span data-stu-id="fa2d3-151">List DNS zones</span></span>

<span data-ttu-id="fa2d3-152">tooenumerate stref DNS, użyj `az network dns zone list`.</span><span class="sxs-lookup"><span data-stu-id="fa2d3-152">tooenumerate DNS zones, use `az network dns zone list`.</span></span> <span data-ttu-id="fa2d3-153">Aby uzyskać pomoc, zobacz `az network dns zone list --help`.</span><span class="sxs-lookup"><span data-stu-id="fa2d3-153">For help, see `az network dns zone list --help`.</span></span>

<span data-ttu-id="fa2d3-154">Określanie grupy zasobów hello wyświetla tylko tych stref w grupie zasobów hello:</span><span class="sxs-lookup"><span data-stu-id="fa2d3-154">Specifying hello resource group lists only those zones within hello resource group:</span></span>

```azurecli
az network dns zone list --resource-group MyResourceGroup
```

<span data-ttu-id="fa2d3-155">Pominięcie hello grupa zasobów zawiera listę wszystkich stref w subskrypcji hello:</span><span class="sxs-lookup"><span data-stu-id="fa2d3-155">Omitting hello resource group lists all zones in hello subscription:</span></span>

```azurecli
az network dns zone list 
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="fa2d3-156">Zaktualizuj strefę DNS</span><span class="sxs-lookup"><span data-stu-id="fa2d3-156">Update a DNS zone</span></span>

<span data-ttu-id="fa2d3-157">Zmiany tooa zasobów strefy DNS będzie możliwe przy użyciu `az network dns zone update`.</span><span class="sxs-lookup"><span data-stu-id="fa2d3-157">Changes tooa DNS zone resource can be made using `az network dns zone update`.</span></span> <span data-ttu-id="fa2d3-158">Aby uzyskać pomoc, zobacz `az network dns zone update --help`.</span><span class="sxs-lookup"><span data-stu-id="fa2d3-158">For help, see `az network dns zone update --help`.</span></span>

<span data-ttu-id="fa2d3-159">To polecenie nie powoduje aktualizacji hello zestawów rekordów DNS w strefie hello (zobacz [jak rekordy DNS tooManage](dns-operations-recordsets-cli.md)).</span><span class="sxs-lookup"><span data-stu-id="fa2d3-159">This command does not update any of hello DNS record sets within hello zone (see [How tooManage DNS records](dns-operations-recordsets-cli.md)).</span></span> <span data-ttu-id="fa2d3-160">Jest tylko tooupdate używanych właściwości zasobu strefy hello, sama.</span><span class="sxs-lookup"><span data-stu-id="fa2d3-160">It is only used tooupdate properties of hello zone resource itself.</span></span> <span data-ttu-id="fa2d3-161">Te właściwości są obecnie ograniczone toohello [usługi Azure Resource Manager "tagi"](dns-zones-records.md#tags) hello strefy zasobu.</span><span class="sxs-lookup"><span data-stu-id="fa2d3-161">These properties are currently limited toohello [Azure Resource Manager 'tags'](dns-zones-records.md#tags) for hello zone resource.</span></span>

<span data-ttu-id="fa2d3-162">Witaj poniższy przykład przedstawia sposób tooupdate hello znaczniki strefy DNS.</span><span class="sxs-lookup"><span data-stu-id="fa2d3-162">hello following example shows how tooupdate hello tags on a DNS zone.</span></span> <span data-ttu-id="fa2d3-163">znaczniki istniejących Hello są zastępowane przez hello wybrana.</span><span class="sxs-lookup"><span data-stu-id="fa2d3-163">hello existing tags are replaced by hello value specified.</span></span>

```azurecli
az network dns zone update --resource-group myresourcegroup --name contoso.com --set tags.team=support
```

## <a name="delete-a-dns-zone"></a><span data-ttu-id="fa2d3-164">Usuń strefę DNS</span><span class="sxs-lookup"><span data-stu-id="fa2d3-164">Delete a DNS zone</span></span>

<span data-ttu-id="fa2d3-165">Można usunąć strefy DNS przy użyciu `az network dns zone delete`.</span><span class="sxs-lookup"><span data-stu-id="fa2d3-165">DNS zones can be deleted using `az network dns zone delete`.</span></span> <span data-ttu-id="fa2d3-166">Aby uzyskać pomoc, zobacz `az network dns zone delete --help`.</span><span class="sxs-lookup"><span data-stu-id="fa2d3-166">For help, see `az network dns zone delete --help`.</span></span>

> [!NOTE]
> <span data-ttu-id="fa2d3-167">Usunięcie strefy DNS powoduje usunięcie wszystkich rekordów DNS w strefie hello.</span><span class="sxs-lookup"><span data-stu-id="fa2d3-167">Deleting a DNS zone also deletes all DNS records within hello zone.</span></span> <span data-ttu-id="fa2d3-168">Tej operacji nie można cofnąć.</span><span class="sxs-lookup"><span data-stu-id="fa2d3-168">This operation cannot be undone.</span></span> <span data-ttu-id="fa2d3-169">Strefa DNS hello jest używany, usługi przy użyciu strefy hello zakończy się niepowodzeniem po usunięciu hello strefy.</span><span class="sxs-lookup"><span data-stu-id="fa2d3-169">If hello DNS zone is in use, services using hello zone will fail when hello zone is deleted.</span></span>
>
><span data-ttu-id="fa2d3-170">Zobacz tooprotect przed usunięciem strefy przypadkowemu [jak tooprotect DNS strefy i rejestruje](dns-protect-zones-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="fa2d3-170">tooprotect against accidental zone deletion, see [How tooprotect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>

<span data-ttu-id="fa2d3-171">To polecenie wyświetla monit o potwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="fa2d3-171">This command prompts for confirmation.</span></span> <span data-ttu-id="fa2d3-172">opcjonalne Hello `--yes` przełącznik pomija tego wiersza.</span><span class="sxs-lookup"><span data-stu-id="fa2d3-172">hello optional `--yes` switch suppresses this prompt.</span></span>

<span data-ttu-id="fa2d3-173">Witaj poniższy przykład przedstawia sposób toodelete hello strefy *contoso.com* z grupy zasobów *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="fa2d3-173">hello following example shows how toodelete hello zone *contoso.com* from resource group *MyResourceGroup*.</span></span>

```azurecli
az network dns zone delete --resource-group myresourcegroup --name contoso.com
```

## <a name="next-steps"></a><span data-ttu-id="fa2d3-174">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fa2d3-174">Next steps</span></span>

<span data-ttu-id="fa2d3-175">Dowiedz się, jak za[zarządzać zestawów rekordów i rekordami](dns-getstarted-create-recordset-cli.md) w strefie DNS.</span><span class="sxs-lookup"><span data-stu-id="fa2d3-175">Learn how too[manage record sets and records](dns-getstarted-create-recordset-cli.md) in your DNS zone.</span></span>

<span data-ttu-id="fa2d3-176">Dowiedz się, jak za[delegować tooAzure Twojego domeny DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="fa2d3-176">Learn how too[delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>

