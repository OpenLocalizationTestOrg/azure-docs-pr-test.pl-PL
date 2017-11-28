---
title: "wprowadzenie do usługi Azure DNS za pomocą usługi Azure CLI 2.0 aaaGet | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate DNS strefy i rejestrowanie w usłudze Azure DNS. To jest toocreate przewodnik krok po kroku i zarządzanie pierwszą strefę DNS i rekordów przy użyciu hello Azure CLI 2.0."
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fb0aa0a6-d096-4d6a-b2f6-eda1c64f6182
ms.service: dns
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: jonatul
ms.openlocfilehash: 8a894941e9910d5cc35394a1be9dbca9792613f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-azure-cli-20"></a><span data-ttu-id="57306-104">Rozpoczynanie pracy z usługą Azure DNS przy użyciu interfejsu wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="57306-104">Get started with Azure DNS using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="57306-105">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="57306-105">Azure portal</span></span>](dns-getstarted-portal.md)
> * [<span data-ttu-id="57306-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="57306-106">PowerShell</span></span>](dns-getstarted-powershell.md)
> * [<span data-ttu-id="57306-107">Interfejs wiersza polecenia platformy Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="57306-107">Azure CLI 1.0</span></span>](dns-getstarted-cli-nodejs.md)
> * [<span data-ttu-id="57306-108">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="57306-108">Azure CLI 2.0</span></span>](dns-getstarted-cli.md)

<span data-ttu-id="57306-109">W tym artykule przedstawiono toocreate kroki hello pierwszy strefy DNS i przy użyciu rekordu hello 2.0 interfejsu wiersza polecenia platformy Azure i platform, która jest dostępna dla systemu Windows, Mac i Linux.</span><span class="sxs-lookup"><span data-stu-id="57306-109">This article walks you through hello steps toocreate your first DNS zone and record using hello cross-platform Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="57306-110">Można również wykonywać następujące czynności, za pomocą hello portalu Azure lub programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="57306-110">You can also perform these steps using hello Azure portal or Azure PowerShell.</span></span>

<span data-ttu-id="57306-111">Strefa DNS jest rekordy DNS hello toohost używane dla określonej domeny.</span><span class="sxs-lookup"><span data-stu-id="57306-111">A DNS zone is used toohost hello DNS records for a particular domain.</span></span> <span data-ttu-id="57306-112">toostart hosting domeny w usłudze Azure DNS należy toocreate strefy DNS dla tej nazwy domeny.</span><span class="sxs-lookup"><span data-stu-id="57306-112">toostart hosting your domain in Azure DNS, you need toocreate a DNS zone for that domain name.</span></span> <span data-ttu-id="57306-113">Każdy rekord DNS domeny zostanie utworzony w tej strefie DNS.</span><span class="sxs-lookup"><span data-stu-id="57306-113">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="57306-114">Na koniec toopublish serwery DNS strefy toohello Internet, należy serwery nazw hello tooconfigure hello domeny.</span><span class="sxs-lookup"><span data-stu-id="57306-114">Finally, toopublish your DNS zone toohello Internet, you need tooconfigure hello name servers for hello domain.</span></span> <span data-ttu-id="57306-115">Poniżej opisano każdy z tych kroków.</span><span class="sxs-lookup"><span data-stu-id="57306-115">Each of these steps is described below.</span></span>

<span data-ttu-id="57306-116">W poniższych instrukcjach przyjęto został już zainstalowany i zalogowany tooAzure 2.0 interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="57306-116">These instructions assume you have already installed and signed in tooAzure CLI 2.0.</span></span> <span data-ttu-id="57306-117">Aby uzyskać pomoc, zobacz [jak toomanage DNS strefy używa interfejsu wiersza polecenia platformy Azure w wersji 2.0](dns-operations-dnszones-cli.md).</span><span class="sxs-lookup"><span data-stu-id="57306-117">For help, see [How toomanage DNS zones using Azure CLI 2.0](dns-operations-dnszones-cli.md).</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="57306-118">Utwórz grupę zasobów hello</span><span class="sxs-lookup"><span data-stu-id="57306-118">Create hello resource group</span></span>

<span data-ttu-id="57306-119">Przed utworzeniem hello strefę DNS, grupy zasobów jest utworzyć strefę DNS hello toocontain.</span><span class="sxs-lookup"><span data-stu-id="57306-119">Before creating hello DNS zone, a resource group is created toocontain hello DNS Zone.</span></span> <span data-ttu-id="57306-120">Oto Hello hello polecenia.</span><span class="sxs-lookup"><span data-stu-id="57306-120">hello following shows hello command.</span></span>

```azurecli
az group create --name MyResourceGroup --location "West US"
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="57306-121">Tworzenie strefy DNS</span><span class="sxs-lookup"><span data-stu-id="57306-121">Create a DNS zone</span></span>

<span data-ttu-id="57306-122">Strefa DNS jest tworzony przy użyciu hello `az network dns zone create` polecenia.</span><span class="sxs-lookup"><span data-stu-id="57306-122">A DNS zone is created using hello `az network dns zone create` command.</span></span> <span data-ttu-id="57306-123">toosee pomocy dla tego polecenia, wpisz `az network dns zone create -h`.</span><span class="sxs-lookup"><span data-stu-id="57306-123">toosee help for this command, type `az network dns zone create -h`.</span></span>

<span data-ttu-id="57306-124">Witaj poniższy przykład tworzy strefę DNS o nazwie *contoso.com* w grupie zasobów hello *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="57306-124">hello following example creates a DNS zone called *contoso.com* in hello resource group *MyResourceGroup*.</span></span> <span data-ttu-id="57306-125">Użyj toocreate przykład hello strefy DNS, podstawiając hello własne wartości.</span><span class="sxs-lookup"><span data-stu-id="57306-125">Use hello example toocreate a DNS zone, substituting hello values for your own.</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n contoso.com
```


## <a name="create-a-dns-record"></a><span data-ttu-id="57306-126">Tworzenie rekordu DNS</span><span class="sxs-lookup"><span data-stu-id="57306-126">Create a DNS record</span></span>

<span data-ttu-id="57306-127">toocreate rekord DNS, użyj hello `az network dns record-set [record type] add-record` polecenia.</span><span class="sxs-lookup"><span data-stu-id="57306-127">toocreate a DNS record, use hello `az network dns record-set [record type] add-record` command.</span></span> <span data-ttu-id="57306-128">Aby uzyskać pomoc, na przykład dotyczącą rekordów A, zobacz `azure network dns record-set A add-record -h`.</span><span class="sxs-lookup"><span data-stu-id="57306-128">For help, for A records for example, see `azure network dns record-set A add-record -h`.</span></span>

<span data-ttu-id="57306-129">Witaj poniższy przykład tworzy rekord z hello nazwie względnej "www" w strefie DNS "contoso.com" w grupie zasobów "MyResourceGroup" hello.</span><span class="sxs-lookup"><span data-stu-id="57306-129">hello following example creates a record with hello relative name "www" in hello DNS Zone "contoso.com", in resource group "MyResourceGroup".</span></span> <span data-ttu-id="57306-130">Hello pełni kwalifikowana nazwa zestawu rekordów hello jest "www.contoso.com".</span><span class="sxs-lookup"><span data-stu-id="57306-130">hello fully-qualified name of hello record set is "www.contoso.com".</span></span> <span data-ttu-id="57306-131">Typ rekordu Hello jest "A", o adresie IP "1.2.3.4", a używana jest domyślna TTL 3600 sekund (1 godzina).</span><span class="sxs-lookup"><span data-stu-id="57306-131">hello record type is "A", with IP address "1.2.3.4", and a default TTL of 3600 seconds (1 hour) is used.</span></span>

```azurecli
az network dns record-set a add-record -g MyResourceGroup -z contoso.com -n www -a 1.2.3.4
```

<span data-ttu-id="57306-132">Dla innych typów rekordów do zestawów rekordów z więcej niż jeden rekord dla alternatywne wartości TTL i toomodify istniejące rekordy, zobacz [przy użyciu zestawów rekordów i rekordami DNS Zarządzanie hello Azure CLI 2.0](dns-operations-recordsets-cli.md).</span><span class="sxs-lookup"><span data-stu-id="57306-132">For other record types, for record sets with more than one record, for alternative TTL values, and toomodify existing records, see [Manage DNS records and record sets using hello Azure CLI 2.0](dns-operations-recordsets-cli.md).</span></span>


## <a name="view-records"></a><span data-ttu-id="57306-133">Wyświetlanie rekordów</span><span class="sxs-lookup"><span data-stu-id="57306-133">View records</span></span>

<span data-ttu-id="57306-134">toolist hello rekordów DNS w strefie, użyj:</span><span class="sxs-lookup"><span data-stu-id="57306-134">toolist hello DNS records in your zone, use:</span></span>

```azurecli
az network dns record-set list -g MyResourceGroup -z contoso.com
```


## <a name="update-name-servers"></a><span data-ttu-id="57306-135">Aktualizowanie serwerów nazw</span><span class="sxs-lookup"><span data-stu-id="57306-135">Update name servers</span></span>

<span data-ttu-id="57306-136">Gdy użytkownik stwierdzi, że Twoje strefy DNS i rekordy są skonfigurowane poprawnie należy tooconfigure domenę toouse hello Azure DNS nazwy serwerów nazw.</span><span class="sxs-lookup"><span data-stu-id="57306-136">Once you are satisfied that your DNS zone and records have been set up correctly, you need tooconfigure your domain name toouse hello Azure DNS name servers.</span></span> <span data-ttu-id="57306-137">Dzięki temu innym użytkownikom w hello Internet toofind rekordów DNS.</span><span class="sxs-lookup"><span data-stu-id="57306-137">This enables other users on hello Internet toofind your DNS records.</span></span>

<span data-ttu-id="57306-138">Witaj serwerów nazw dla strefy są podane przez hello `az network dns zone show` polecenia.</span><span class="sxs-lookup"><span data-stu-id="57306-138">hello name servers for your zone are given by hello `az network dns zone show` command.</span></span> <span data-ttu-id="57306-139">toosee hello nazw serwerów nazw użyj dane wyjściowe JSON, jak pokazano w hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="57306-139">toosee hello name server names, use JSON output, as shown in hello following example.</span></span>

```azurecli
az network dns zone show -g MyResourceGroup -n contoso.com -o json

{
  "etag": "00000003-0000-0000-b40d-0996b97ed101",
  "id": "/subscriptions/a385a691-bd93-41b0-8084-8213ebc5bff7/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "contoso.com",
  "nameServers": [
    "ns1-01.azure-dns.com.",
    "ns2-01.azure-dns.net.",
    "ns3-01.azure-dns.org.",
    "ns4-01.azure-dns.info."
  ],
  "numberOfRecordSets": 3,
  "resourceGroup": "myresourcegroup",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

<span data-ttu-id="57306-140">Te serwery nazw powinien mieć skonfigurowaną rejestratora nazw domen hello (którego go zakupiono hello nazwa domeny).</span><span class="sxs-lookup"><span data-stu-id="57306-140">These name servers should be configured with hello domain name registrar (where you purchased hello domain name).</span></span> <span data-ttu-id="57306-141">Rejestrator zaoferuje tooset opcji hello hello serwery nazw dla domeny hello.</span><span class="sxs-lookup"><span data-stu-id="57306-141">Your registrar will offer hello option tooset up hello name servers for hello domain.</span></span> <span data-ttu-id="57306-142">Aby uzyskać więcej informacji, zobacz [delegować tooAzure Twojego domeny DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="57306-142">For more information, see [Delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>

## <a name="delete-all-resources"></a><span data-ttu-id="57306-143">Usuwanie wszystkich zasobów</span><span class="sxs-lookup"><span data-stu-id="57306-143">Delete all resources</span></span>
 
<span data-ttu-id="57306-144">toodelete wszystkie zasoby są tworzone w tym artykule, wykonaj powitania po kroku:</span><span class="sxs-lookup"><span data-stu-id="57306-144">toodelete all resources created in this article, take hello following step:</span></span>

```azurecli
az group delete --name MyResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="57306-145">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="57306-145">Next steps</span></span>

<span data-ttu-id="57306-146">toolearn więcej informacji na temat usługi Azure DNS, zobacz [Omówienie usługi Azure DNS](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="57306-146">toolearn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span></span>

<span data-ttu-id="57306-147">toolearn więcej na temat zarządzania strefami DNS w usłudze Azure DNS, zobacz [stref DNS zarządzania w usłudze Azure DNS za pomocą usługi Azure CLI 2.0](dns-operations-dnszones-cli.md).</span><span class="sxs-lookup"><span data-stu-id="57306-147">toolearn more about managing DNS zones in Azure DNS, see [Manage DNS zones in Azure DNS using Azure CLI 2.0](dns-operations-dnszones-cli.md).</span></span>

<span data-ttu-id="57306-148">toolearn więcej informacji o zarządzaniu rekordy DNS w usłudze Azure DNS, zobacz [zestawami rekordów i rekordami DNS zarządzania w usłudze Azure DNS za pomocą usługi Azure CLI 2.0](dns-operations-recordsets-cli.md).</span><span class="sxs-lookup"><span data-stu-id="57306-148">toolearn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets in Azure DNS using Azure CLI 2.0](dns-operations-recordsets-cli.md).</span></span>
