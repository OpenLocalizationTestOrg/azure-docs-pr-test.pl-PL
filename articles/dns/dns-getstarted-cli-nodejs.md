---
title: "wprowadzenie do usługi Azure DNS przy użyciu interfejsu wiersza polecenia platformy Azure w wersji 1.0 aaaGet | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate DNS strefy i rejestrowanie w usłudze Azure DNS. To jest toocreate przewodnik krok po kroku i zarządzanie pierwszą strefę DNS i rekordów przy użyciu hello Azure CLI w wersji 1.0."
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fb0aa0a6-d096-4d6a-b2f6-eda1c64f6182
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: jonatul
ms.openlocfilehash: e200c848ad261160e593306dbb8a1d92bf26880b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-azure-cli-10"></a><span data-ttu-id="aa219-104">Rozpoczynanie pracy z usługą Azure DNS przy użyciu interfejsu wiersza polecenia platformy Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="aa219-104">Get started with Azure DNS using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="aa219-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="aa219-105">Azure portal</span></span>](dns-getstarted-portal.md)
> * [<span data-ttu-id="aa219-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="aa219-106">PowerShell</span></span>](dns-getstarted-powershell.md)
> * [<span data-ttu-id="aa219-107">Interfejs wiersza polecenia platformy Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="aa219-107">Azure CLI 1.0</span></span>](dns-getstarted-cli-nodejs.md)
> * [<span data-ttu-id="aa219-108">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="aa219-108">Azure CLI 2.0</span></span>](dns-getstarted-cli.md)

<span data-ttu-id="aa219-109">W tym artykule przedstawiono toocreate kroki hello pierwszy strefy DNS i przy użyciu rekordu hello 1.0 interfejsu wiersza polecenia platformy Azure i platform, która jest dostępna dla systemu Windows, Mac i Linux.</span><span class="sxs-lookup"><span data-stu-id="aa219-109">This article walks you through hello steps toocreate your first DNS zone and record using hello cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="aa219-110">Można również wykonywać następujące czynności, za pomocą hello portalu Azure lub programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="aa219-110">You can also perform these steps using hello Azure portal or Azure PowerShell.</span></span>

<span data-ttu-id="aa219-111">Strefa DNS jest rekordy DNS hello toohost używane dla określonej domeny.</span><span class="sxs-lookup"><span data-stu-id="aa219-111">A DNS zone is used toohost hello DNS records for a particular domain.</span></span> <span data-ttu-id="aa219-112">toostart hosting domeny w usłudze Azure DNS należy toocreate strefy DNS dla tej nazwy domeny.</span><span class="sxs-lookup"><span data-stu-id="aa219-112">toostart hosting your domain in Azure DNS, you need toocreate a DNS zone for that domain name.</span></span> <span data-ttu-id="aa219-113">Każdy rekord DNS domeny zostanie utworzony w tej strefie DNS.</span><span class="sxs-lookup"><span data-stu-id="aa219-113">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="aa219-114">Na koniec toopublish serwery DNS strefy toohello Internet, należy serwery nazw hello tooconfigure hello domeny.</span><span class="sxs-lookup"><span data-stu-id="aa219-114">Finally, toopublish your DNS zone toohello Internet, you need tooconfigure hello name servers for hello domain.</span></span> <span data-ttu-id="aa219-115">Poniżej opisano każdy z tych kroków.</span><span class="sxs-lookup"><span data-stu-id="aa219-115">Each of these steps is described below.</span></span>

<span data-ttu-id="aa219-116">W poniższych instrukcjach przyjęto został już zainstalowany i zalogowany tooAzure 1.0 interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="aa219-116">These instructions assume you have already installed and signed in tooAzure CLI 1.0.</span></span> <span data-ttu-id="aa219-117">Aby uzyskać pomoc, zobacz [jak toomanage DNS strefy przy użyciu interfejsu wiersza polecenia platformy Azure w wersji 1.0](dns-operations-dnszones-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="aa219-117">For help, see [How toomanage DNS zones using Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md).</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="aa219-118">Utwórz grupę zasobów hello</span><span class="sxs-lookup"><span data-stu-id="aa219-118">Create hello resource group</span></span>

<span data-ttu-id="aa219-119">Przed utworzeniem hello strefę DNS, grupy zasobów jest utworzyć strefę DNS hello toocontain.</span><span class="sxs-lookup"><span data-stu-id="aa219-119">Before creating hello DNS zone, a resource group is created toocontain hello DNS Zone.</span></span> <span data-ttu-id="aa219-120">Oto Hello hello polecenia.</span><span class="sxs-lookup"><span data-stu-id="aa219-120">hello following shows hello command.</span></span>

```azurecli
azure group create --name MyResourceGroup --location "West US"
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="aa219-121">Tworzenie strefy DNS</span><span class="sxs-lookup"><span data-stu-id="aa219-121">Create a DNS zone</span></span>

<span data-ttu-id="aa219-122">Strefa DNS jest tworzony przy użyciu hello `azure network dns zone create` polecenia.</span><span class="sxs-lookup"><span data-stu-id="aa219-122">A DNS zone is created using hello `azure network dns zone create` command.</span></span> <span data-ttu-id="aa219-123">toosee pomocy dla tego polecenia, wpisz `azure network dns zone create -h`.</span><span class="sxs-lookup"><span data-stu-id="aa219-123">toosee help for this command, type `azure network dns zone create -h`.</span></span>

<span data-ttu-id="aa219-124">Witaj poniższy przykład tworzy strefę DNS o nazwie *contoso.com* w hello grupy zasobów o nazwie *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="aa219-124">hello following example creates a DNS zone called *contoso.com* in hello resource group called *MyResourceGroup*.</span></span> <span data-ttu-id="aa219-125">Użyj toocreate przykład hello strefy DNS, podstawiając hello własne wartości.</span><span class="sxs-lookup"><span data-stu-id="aa219-125">Use hello example toocreate a DNS zone, substituting hello values for your own.</span></span>

```azurecli
azure network dns zone create MyResourceGroup contoso.com
```


## <a name="create-a-dns-record"></a><span data-ttu-id="aa219-126">Tworzenie rekordu DNS</span><span class="sxs-lookup"><span data-stu-id="aa219-126">Create a DNS record</span></span>

<span data-ttu-id="aa219-127">toocreate rekord DNS, użyj hello `azure network dns record-set add-record` polecenia.</span><span class="sxs-lookup"><span data-stu-id="aa219-127">toocreate a DNS record, use hello `azure network dns record-set add-record` command.</span></span> <span data-ttu-id="aa219-128">Aby uzyskać pomoc, zobacz `azure network dns record-set add-record -h`.</span><span class="sxs-lookup"><span data-stu-id="aa219-128">For help, see `azure network dns record-set add-record -h`.</span></span>

<span data-ttu-id="aa219-129">Witaj poniższy przykład tworzy rekord z hello nazwie względnej "www" w strefie DNS "contoso.com" w grupie zasobów "MyResourceGroup" hello.</span><span class="sxs-lookup"><span data-stu-id="aa219-129">hello following example creates a record with hello relative name "www" in hello DNS Zone "contoso.com", in resource group "MyResourceGroup".</span></span> <span data-ttu-id="aa219-130">Hello pełni kwalifikowana nazwa zestawu rekordów hello jest "www.contoso.com".</span><span class="sxs-lookup"><span data-stu-id="aa219-130">hello fully-qualified name of hello record set is "www.contoso.com".</span></span> <span data-ttu-id="aa219-131">Typ rekordu Hello jest "A", o adresie IP "1.2.3.4", a używana jest domyślna TTL 3600 sekund (1 godzina).</span><span class="sxs-lookup"><span data-stu-id="aa219-131">hello record type is "A", with IP address "1.2.3.4", and a default TTL of 3600 seconds (1 hour) is used.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

<span data-ttu-id="aa219-132">Dla innych typów rekordów do zestawów rekordów z więcej niż jeden rekord dla alternatywne wartości TTL i toomodify istniejące rekordy, zobacz [przy użyciu zestawów rekordów i rekordami DNS Zarządzanie hello Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="aa219-132">For other record types, for record sets with more than one record, for alternative TTL values, and toomodify existing records, see [Manage DNS records and record sets using hello Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md).</span></span>


## <a name="view-records"></a><span data-ttu-id="aa219-133">Wyświetlanie rekordów</span><span class="sxs-lookup"><span data-stu-id="aa219-133">View records</span></span>

<span data-ttu-id="aa219-134">toolist hello rekordów DNS w strefie, użyj:</span><span class="sxs-lookup"><span data-stu-id="aa219-134">toolist hello DNS records in your zone, use:</span></span>

```azurecli
azure network dns record-set list MyResourceGroup contoso.com
```


## <a name="update-name-servers"></a><span data-ttu-id="aa219-135">Aktualizowanie serwerów nazw</span><span class="sxs-lookup"><span data-stu-id="aa219-135">Update name servers</span></span>

<span data-ttu-id="aa219-136">Gdy użytkownik stwierdzi, że Twoje strefy DNS i rekordy są skonfigurowane poprawnie należy tooconfigure domenę toouse hello Azure DNS nazwy serwerów nazw.</span><span class="sxs-lookup"><span data-stu-id="aa219-136">Once you are satisfied that your DNS zone and records have been set up correctly, you need tooconfigure your domain name toouse hello Azure DNS name servers.</span></span> <span data-ttu-id="aa219-137">Dzięki temu innym użytkownikom w hello Internet toofind rekordów DNS.</span><span class="sxs-lookup"><span data-stu-id="aa219-137">This enables other users on hello Internet toofind your DNS records.</span></span>

<span data-ttu-id="aa219-138">Witaj serwerów nazw dla strefy są podane przez hello `azure network dns zone show` polecenia:</span><span class="sxs-lookup"><span data-stu-id="aa219-138">hello name servers for your zone are given by hello `azure network dns zone show` command:</span></span>

```azurecli
azure network dns zone show MyResourceGroup contoso.com

info:    Executing command network dns zone show
+ Looking up hello dns zone "contoso.com"
data:    Id                              : /subscriptions/a385a691-bd93-41b0-8084-8213ebc5bff7/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com
data:    Name                            : contoso.com
data:    Type                            : Microsoft.Network/dnszones
data:    Location                        : global
data:    Number of record sets           : 3
data:    Max number of record sets       : 5000
data:    Name servers:
data:        ns1-01.azure-dns.com.
data:        ns2-01.azure-dns.net.
data:        ns3-01.azure-dns.org.
data:        ns4-01.azure-dns.info.
data:    Tags                            :
info:    network dns zone show command OK
```

<span data-ttu-id="aa219-139">Te serwery nazw powinien mieć skonfigurowaną rejestratora nazw domen hello (którego go zakupiono hello nazwa domeny).</span><span class="sxs-lookup"><span data-stu-id="aa219-139">These name servers should be configured with hello domain name registrar (where you purchased hello domain name).</span></span> <span data-ttu-id="aa219-140">Rejestrator zaoferuje tooset opcji hello hello serwery nazw dla domeny hello.</span><span class="sxs-lookup"><span data-stu-id="aa219-140">Your registrar will offer hello option tooset up hello name servers for hello domain.</span></span> <span data-ttu-id="aa219-141">Aby uzyskać więcej informacji, zobacz [delegować tooAzure Twojego domeny DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="aa219-141">For more information, see [Delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>

## <a name="delete-all-resources"></a><span data-ttu-id="aa219-142">Usuwanie wszystkich zasobów</span><span class="sxs-lookup"><span data-stu-id="aa219-142">Delete all resources</span></span>
 
<span data-ttu-id="aa219-143">toodelete wszystkie zasoby są tworzone w tym artykule, wykonaj powitania po kroku:</span><span class="sxs-lookup"><span data-stu-id="aa219-143">toodelete all resources created in this article, take hello following step:</span></span>

```azurecli
azure group delete --name MyResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="aa219-144">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="aa219-144">Next steps</span></span>

<span data-ttu-id="aa219-145">toolearn więcej informacji na temat usługi Azure DNS, zobacz [Omówienie usługi Azure DNS](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="aa219-145">toolearn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span></span>

<span data-ttu-id="aa219-146">toolearn więcej na temat zarządzania strefami DNS w usłudze Azure DNS, zobacz [stref DNS zarządzania w usłudze Azure DNS przy użyciu interfejsu wiersza polecenia platformy Azure w wersji 1.0](dns-operations-dnszones-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="aa219-146">toolearn more about managing DNS zones in Azure DNS, see [Manage DNS zones in Azure DNS using Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md).</span></span>

<span data-ttu-id="aa219-147">toolearn więcej informacji o zarządzaniu rekordy DNS w usłudze Azure DNS, zobacz [zestawami rekordów i rekordami DNS zarządzania w usłudze Azure DNS przy użyciu interfejsu wiersza polecenia platformy Azure w wersji 1.0](dns-operations-recordsets-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="aa219-147">toolearn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets in Azure DNS using Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md).</span></span>

