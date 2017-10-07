---
title: "wprowadzenie do usługi Azure DNS przy użyciu programu PowerShell aaaGet | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate DNS strefy i rejestrowanie w usłudze Azure DNS. To jest toocreate przewodnik krok po kroku i zarządzanie nimi z pierwszą strefę DNS oraz rejestrowania przy użyciu programu PowerShell."
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
ms.openlocfilehash: 0f9dead1e4b44fcc74c84a024c41cdfaeb02b5d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-powershell"></a><span data-ttu-id="4a460-104">Rozpoczynanie pracy z usługą Azure DNS przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="4a460-104">Get Started with Azure DNS using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4a460-105">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="4a460-105">Azure portal</span></span>](dns-getstarted-portal.md)
> * [<span data-ttu-id="4a460-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4a460-106">PowerShell</span></span>](dns-getstarted-powershell.md)
> * [<span data-ttu-id="4a460-107">Interfejs wiersza polecenia platformy Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="4a460-107">Azure CLI 1.0</span></span>](dns-getstarted-cli-nodejs.md)
> * [<span data-ttu-id="4a460-108">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="4a460-108">Azure CLI 2.0</span></span>](dns-getstarted-cli.md)

<span data-ttu-id="4a460-109">W tym artykule przedstawiono hello kroki toocreate z pierwszą strefę DNS i rejestrowanie przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4a460-109">This article walks you through hello steps toocreate your first DNS zone and record using Azure PowerShell.</span></span> <span data-ttu-id="4a460-110">Można również wykonywać te czynności przy użyciu portalu Azure hello lub hello wiersza polecenia platformy Azure i platform.</span><span class="sxs-lookup"><span data-stu-id="4a460-110">You can also perform these steps using hello Azure portal or hello cross-platform Azure CLI.</span></span>

<span data-ttu-id="4a460-111">Strefa DNS jest rekordy DNS hello toohost używane dla określonej domeny.</span><span class="sxs-lookup"><span data-stu-id="4a460-111">A DNS zone is used toohost hello DNS records for a particular domain.</span></span> <span data-ttu-id="4a460-112">toostart hosting domeny w usłudze Azure DNS należy toocreate strefy DNS dla tej nazwy domeny.</span><span class="sxs-lookup"><span data-stu-id="4a460-112">toostart hosting your domain in Azure DNS, you need toocreate a DNS zone for that domain name.</span></span> <span data-ttu-id="4a460-113">Każdy rekord DNS domeny zostanie utworzony w tej strefie DNS.</span><span class="sxs-lookup"><span data-stu-id="4a460-113">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="4a460-114">Na koniec toopublish serwery DNS strefy toohello Internet, należy serwery nazw hello tooconfigure hello domeny.</span><span class="sxs-lookup"><span data-stu-id="4a460-114">Finally, toopublish your DNS zone toohello Internet, you need tooconfigure hello name servers for hello domain.</span></span> <span data-ttu-id="4a460-115">Poniżej opisano każdy z tych kroków.</span><span class="sxs-lookup"><span data-stu-id="4a460-115">Each of these steps is described below.</span></span>

<span data-ttu-id="4a460-116">W poniższych instrukcjach przyjęto został już zainstalowany i zalogowany tooAzure środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4a460-116">These instructions assume you have already installed and signed in tooAzure PowerShell.</span></span> <span data-ttu-id="4a460-117">Aby uzyskać pomoc, zobacz [jak toomanage DNS strefy przy użyciu programu PowerShell](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="4a460-117">For help, see [How toomanage DNS zones using PowerShell](dns-operations-dnszones.md).</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="4a460-118">Utwórz grupę zasobów hello</span><span class="sxs-lookup"><span data-stu-id="4a460-118">Create hello resource group</span></span>

<span data-ttu-id="4a460-119">Przed utworzeniem hello strefę DNS, grupy zasobów jest utworzyć strefę DNS hello toocontain.</span><span class="sxs-lookup"><span data-stu-id="4a460-119">Before creating hello DNS zone, a resource group is created toocontain hello DNS Zone.</span></span> <span data-ttu-id="4a460-120">Oto Hello hello polecenia.</span><span class="sxs-lookup"><span data-stu-id="4a460-120">hello following shows hello command.</span></span>

```powershell
New-AzureRMResourceGroup -name MyResourceGroup -location "westus"
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="4a460-121">Tworzenie strefy DNS</span><span class="sxs-lookup"><span data-stu-id="4a460-121">Create a DNS zone</span></span>

<span data-ttu-id="4a460-122">Strefa DNS jest tworzona przy użyciu hello `New-AzureRmDnsZone` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4a460-122">A DNS zone is created by using hello `New-AzureRmDnsZone` cmdlet.</span></span> <span data-ttu-id="4a460-123">Witaj poniższy przykład tworzy strefę DNS o nazwie *contoso.com* w hello grupy zasobów o nazwie *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="4a460-123">hello following example creates a DNS zone called *contoso.com* in hello resource group called *MyResourceGroup*.</span></span> <span data-ttu-id="4a460-124">Użyj toocreate przykład hello strefy DNS, podstawiając hello własne wartości.</span><span class="sxs-lookup"><span data-stu-id="4a460-124">Use hello example toocreate a DNS zone, substituting hello values for your own.</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyResourceGroup
```

## <a name="create-a-dns-record"></a><span data-ttu-id="4a460-125">Tworzenie rekordu DNS</span><span class="sxs-lookup"><span data-stu-id="4a460-125">Create a DNS record</span></span>

<span data-ttu-id="4a460-126">Tworzenie zestawów rekordów przy użyciu hello `New-AzureRmDnsRecordSet` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4a460-126">You create record sets by using hello `New-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="4a460-127">Witaj poniższy przykład tworzy rekord z hello nazwie względnej "www" w strefie DNS "contoso.com" w grupie zasobów "MyResourceGroup" hello.</span><span class="sxs-lookup"><span data-stu-id="4a460-127">hello following example creates a record with hello relative name "www" in hello DNS Zone "contoso.com", in resource group "MyResourceGroup".</span></span> <span data-ttu-id="4a460-128">Hello pełni kwalifikowana nazwa zestawu rekordów hello jest "www.contoso.com".</span><span class="sxs-lookup"><span data-stu-id="4a460-128">hello fully-qualified name of hello record set is "www.contoso.com".</span></span> <span data-ttu-id="4a460-129">Typ rekordu Hello jest "A", o adresie IP "1.2.3.4", a hello TTL jest 3600 sekund.</span><span class="sxs-lookup"><span data-stu-id="4a460-129">hello record type is "A", with IP address "1.2.3.4", and hello TTL is 3600 seconds.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName contoso.com -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4")
```

<span data-ttu-id="4a460-130">Dla innych typów rekordów do zestawów rekordów z więcej niż jeden rekord, a istniejące rekordy toomodify, zobacz [rekordy DNS, zarządzanie i zestawów rekordów przy użyciu programu Azure PowerShell](dns-operations-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="4a460-130">For other record types, for record sets with more than one record, and toomodify existing records, see [Manage DNS records and record sets using Azure PowerShell](dns-operations-recordsets.md).</span></span> 


## <a name="view-records"></a><span data-ttu-id="4a460-131">Wyświetlanie rekordów</span><span class="sxs-lookup"><span data-stu-id="4a460-131">View records</span></span>

<span data-ttu-id="4a460-132">toolist hello rekordów DNS w strefie, użyj:</span><span class="sxs-lookup"><span data-stu-id="4a460-132">toolist hello DNS records in your zone, use:</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName contoso.com -ResourceGroupName MyResourceGroup
```


## <a name="update-name-servers"></a><span data-ttu-id="4a460-133">Aktualizowanie serwerów nazw</span><span class="sxs-lookup"><span data-stu-id="4a460-133">Update name servers</span></span>

<span data-ttu-id="4a460-134">Gdy użytkownik stwierdzi, że Twoje strefy DNS i rekordy są skonfigurowane poprawnie należy tooconfigure domenę toouse hello Azure DNS nazwy serwerów nazw.</span><span class="sxs-lookup"><span data-stu-id="4a460-134">Once you are satisfied that your DNS zone and records have been set up correctly, you need tooconfigure your domain name toouse hello Azure DNS name servers.</span></span> <span data-ttu-id="4a460-135">Dzięki temu innym użytkownikom w hello Internet toofind rekordów DNS.</span><span class="sxs-lookup"><span data-stu-id="4a460-135">This enables other users on hello Internet toofind your DNS records.</span></span>

<span data-ttu-id="4a460-136">Witaj serwerów nazw dla strefy są podane przez hello `Get-AzureRmDnsZone` polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="4a460-136">hello name servers for your zone are given by hello `Get-AzureRmDnsZone` cmdlet:</span></span>

```powershell
Get-AzureRmDnsZone -ZoneName contoso.com -ResourceGroupName MyResourceGroup

Name                  : contoso.com
ResourceGroupName     : myresourcegroup
Etag                  : 00000003-0000-0000-b40d-0996b97ed101
Tags                  : {}
NameServers           : {ns1-01.azure-dns.com., ns2-01.azure-dns.net., ns3-01.azure-dns.org., ns4-01.azure-dns.info.}
NumberOfRecordSets    : 3
MaxNumberOfRecordSets : 5000
```

<span data-ttu-id="4a460-137">Te serwery nazw powinien mieć skonfigurowaną rejestratora nazw domen hello (którego go zakupiono hello nazwa domeny).</span><span class="sxs-lookup"><span data-stu-id="4a460-137">These name servers should be configured with hello domain name registrar (where you purchased hello domain name).</span></span> <span data-ttu-id="4a460-138">Rejestrator zaoferuje tooset opcji hello hello serwery nazw dla domeny hello.</span><span class="sxs-lookup"><span data-stu-id="4a460-138">Your registrar will offer hello option tooset up hello name servers for hello domain.</span></span> <span data-ttu-id="4a460-139">Aby uzyskać więcej informacji, zobacz [delegować tooAzure Twojego domeny DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="4a460-139">For more information, see [Delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>

## <a name="delete-all-resources"></a><span data-ttu-id="4a460-140">Usuwanie wszystkich zasobów</span><span class="sxs-lookup"><span data-stu-id="4a460-140">Delete all resources</span></span>

<span data-ttu-id="4a460-141">toodelete wszystkie zasoby są tworzone w tym artykule, wykonaj powitania po kroku:</span><span class="sxs-lookup"><span data-stu-id="4a460-141">toodelete all resources created in this article, take hello following step:</span></span>

```powershell
Remove-AzureRMResourceGroup -Name MyResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="4a460-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4a460-142">Next steps</span></span>

<span data-ttu-id="4a460-143">toolearn więcej informacji na temat usługi Azure DNS, zobacz [Omówienie usługi Azure DNS](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4a460-143">toolearn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span></span>

<span data-ttu-id="4a460-144">toolearn więcej na temat zarządzania strefami DNS w usłudze Azure DNS, zobacz [stref DNS zarządzania w usłudze Azure DNS przy użyciu programu PowerShell](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="4a460-144">toolearn more about managing DNS zones in Azure DNS, see [Manage DNS zones in Azure DNS using PowerShell](dns-operations-dnszones.md).</span></span>

<span data-ttu-id="4a460-145">toolearn więcej informacji o zarządzaniu rekordy DNS w usłudze Azure DNS, zobacz [zestawami rekordów i rekordami DNS zarządzania w usłudze Azure DNS przy użyciu programu PowerShell](dns-operations-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="4a460-145">toolearn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets in Azure DNS using PowerShell](dns-operations-recordsets.md).</span></span>

