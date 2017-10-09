---
title: "aaaCreate regułę modułu równoważenia obciążenia Azure dla klastra"
description: "Skonfiguruj porty tooopen modułu równoważenia obciążenia Azure dla klastra usługi sieć szkieletowa usług Azure."
services: service-fabric
documentationcenter: na
author: thraka
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/22/2017
ms.author: adegeo
ms.openlocfilehash: 4a40f62422bd895d782be8cbaace5f4e1af81db3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="open-ports-for-a-service-fabric-cluster"></a><span data-ttu-id="9e537-103">Otwieranie portów dla klastra sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="9e537-103">Open ports for a Service Fabric cluster</span></span>

<span data-ttu-id="9e537-104">usługi równoważenia obciążenia Hello wdrożone z klastrem usługi sieć szkieletowa usług Azure kieruje ruch tooyour aplikacji uruchomionej na węźle.</span><span class="sxs-lookup"><span data-stu-id="9e537-104">hello load balancer deployed with your Azure Service Fabric cluster directs traffic tooyour app running on a node.</span></span> <span data-ttu-id="9e537-105">Jeśli zmienisz toouse Twojej aplikacji innego portu, musi ujawniać tego portu (lub trasy innego portu) w hello modułu równoważenia obciążenia Azure.</span><span class="sxs-lookup"><span data-stu-id="9e537-105">If you change your app toouse a different port, you must expose that port (or route a different port) in hello Azure Load Balancer.</span></span>

<span data-ttu-id="9e537-106">Po wdrożeniu sieci tooAzure klastra sieci szkieletowej usług równoważenia obciążenia został utworzony automatycznie.</span><span class="sxs-lookup"><span data-stu-id="9e537-106">When you deployed your service fabric cluster tooAzure, a load balancer was automatically created for you.</span></span> <span data-ttu-id="9e537-107">Jeśli nie masz usługi równoważenia obciążenia, zobacz [skonfigurowania funkcji równoważenia obciążenia internetowy](..\load-balancer\load-balancer-get-started-internet-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9e537-107">If you do not have a load balancer, see [Configure an Internet-facing load balancer](..\load-balancer\load-balancer-get-started-internet-portal.md).</span></span>

## <a name="configure-service-fabric"></a><span data-ttu-id="9e537-108">Konfigurowanie sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="9e537-108">Configure service fabric</span></span>

<span data-ttu-id="9e537-109">Aplikacja usługi Service Fabric **ServiceManifest.xml** hello punkty końcowe aplikacji oczekuje toouse definiuje pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="9e537-109">Your Service Fabric application **ServiceManifest.xml** config file defines hello endpoints your application expects toouse.</span></span> <span data-ttu-id="9e537-110">Po hello config plik został zaktualizowany toodefine punktu końcowego, hello modułu równoważenia obciążenia musi być zaktualizowany tooexpose tego (lub innej) portu.</span><span class="sxs-lookup"><span data-stu-id="9e537-110">After hello config file has been updated toodefine an endpoint, hello load balancer must be updated tooexpose that (or a different) port.</span></span> <span data-ttu-id="9e537-111">Aby uzyskać więcej informacji dotyczących sposobu toocreate hello punkt końcowy usługi sieci szkieletowej, zobacz [Konfiguracja punktu końcowego](service-fabric-service-manifest-resources.md).</span><span class="sxs-lookup"><span data-stu-id="9e537-111">For more information on how toocreate hello service fabric endpoint, see [Setup an Endpoint](service-fabric-service-manifest-resources.md).</span></span>

## <a name="create-a-load-balancer-rule"></a><span data-ttu-id="9e537-112">Tworzenie reguły modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="9e537-112">Create a load balancer rule</span></span>

<span data-ttu-id="9e537-113">Reguły modułu równoważenia obciążenia otwiera port połączonych z Internetem i przekazuje ruch toohello wewnętrznego węzła port używany przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="9e537-113">A load balancer rule opens up an internet-facing port and forwards traffic toohello internal node's port used by your application.</span></span> <span data-ttu-id="9e537-114">Jeśli nie masz usługi równoważenia obciążenia, zobacz [skonfigurowania funkcji równoważenia obciążenia internetowy](..\load-balancer\load-balancer-get-started-internet-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9e537-114">If you do not have a load balancer, see [Configure an Internet-facing load balancer](..\load-balancer\load-balancer-get-started-internet-portal.md).</span></span>

<span data-ttu-id="9e537-115">toocreate reguły modułu równoważenia obciążenia, należy hello toocollect następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="9e537-115">toocreate a load balancer rule, you need toocollect hello following information:</span></span>

- <span data-ttu-id="9e537-116">Nazwa modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="9e537-116">Load balancer name.</span></span>
- <span data-ttu-id="9e537-117">Grupa zasobów hello obciążenia równoważenia i klastra sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="9e537-117">Resource group of hello load balancer and service fabric cluster.</span></span>
- <span data-ttu-id="9e537-118">Portu zewnętrznego.</span><span class="sxs-lookup"><span data-stu-id="9e537-118">External port.</span></span>
- <span data-ttu-id="9e537-119">Port wewnętrzny.</span><span class="sxs-lookup"><span data-stu-id="9e537-119">Internal port.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="9e537-120">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9e537-120">Azure CLI</span></span>
>[!NOTE]
><span data-ttu-id="9e537-121">Nazwa hello toodetermine hello usługi równoważenia obciążenia, należy użyć tego polecenia get tooquickly listę wszystkich usług równoważenia obciążenia i hello skojarzonych grup zasobów.</span><span class="sxs-lookup"><span data-stu-id="9e537-121">If you need toodetermine hello name of hello load balancer, use this command tooquickly get a list of all load balancers and hello associated resource groups.</span></span>
>
>`az network lb list --query "[].{ResourceGroup: resourceGroup, Name: name}"`
>

<span data-ttu-id="9e537-122">Potrwa to tylko toocreate jednego polecenia reguły modułu równoważenia obciążenia z hello **interfejsu wiersza polecenia Azure**.</span><span class="sxs-lookup"><span data-stu-id="9e537-122">It only takes a single command toocreate a load balancer rule with hello **Azure CLI**.</span></span> <span data-ttu-id="9e537-123">Wystarczy tooknow zarówno nazwę hello hello obciążenia równoważenia i zasobów grupy toocreate nową regułę.</span><span class="sxs-lookup"><span data-stu-id="9e537-123">You just need tooknow both hello name of hello load balancer and resource group toocreate a new rule.</span></span>

```azurecli
az network lb rule create --backend-port 40000 --frontend-port 39999 --protocol Tcp --lb-name LB-svcfab3 -g svcfab_cli -n my-app-rule
```

<span data-ttu-id="9e537-124">Witaj polecenia interfejsu wiersza polecenia Azure ma kilka parametrów, które zostały opisane w poniższej tabeli hello:</span><span class="sxs-lookup"><span data-stu-id="9e537-124">hello Azure CLI command has a few parameters that are described in hello following table:</span></span>

| <span data-ttu-id="9e537-125">Parametr</span><span class="sxs-lookup"><span data-stu-id="9e537-125">Parameter</span></span> | <span data-ttu-id="9e537-126">Opis</span><span class="sxs-lookup"><span data-stu-id="9e537-126">Description</span></span> |
| --------- | ----------- |
| `--backend-port`  | <span data-ttu-id="9e537-127">nasłuchuje aplikacja Hello portu hello usługi sieci szkieletowej.</span><span class="sxs-lookup"><span data-stu-id="9e537-127">hello port hello service fabric application is listening to.</span></span> |
| `--frontend-port` | <span data-ttu-id="9e537-128">Witaj Witaj portu załadować ujawnia równoważenia dla połączeń zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="9e537-128">hello port hello load balancer exposes for external connections.</span></span> |
| `-lb-name` | <span data-ttu-id="9e537-129">Nazwa Hello hello załadować toochange równoważenia.</span><span class="sxs-lookup"><span data-stu-id="9e537-129">hello name of hello load balancer toochange.</span></span> |
| `-g`       | <span data-ttu-id="9e537-130">Grupa zasobów Hello ma hello modułu równoważenia obciążenia oraz klastra sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="9e537-130">hello resource group that has both hello load balancer and service fabric cluster.</span></span> |
| `-n`       | <span data-ttu-id="9e537-131">Wybrana nazwa reguły hello Hello.</span><span class="sxs-lookup"><span data-stu-id="9e537-131">hello chosen name of hello rule.</span></span> |


>[!NOTE]
><span data-ttu-id="9e537-132">Aby uzyskać więcej informacji na temat toocreate modułu równoważenia obciążenia z hello wiersza polecenia platformy Azure, zobacz temat [Utwórz usługę równoważenia obciążenia z hello Azure CLI](..\load-balancer\load-balancer-get-started-internet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="9e537-132">For more information on how toocreate a load balancer with hello Azure CLI, see [Create a load balancer with hello Azure CLI](..\load-balancer\load-balancer-get-started-internet-arm-cli.md).</span></span>

## <a name="powershell"></a><span data-ttu-id="9e537-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9e537-133">PowerShell</span></span>

>[!NOTE]
><span data-ttu-id="9e537-134">Nazwa hello toodetermine hello usługi równoważenia obciążenia, należy użyć tego polecenia get tooquickly listę wszystkich usług równoważenia obciążenia i grup zasobów.</span><span class="sxs-lookup"><span data-stu-id="9e537-134">If you need toodetermine hello name of hello load balancer, use this command tooquickly get a list of all load balancers and associated resource groups.</span></span>
>
>`Get-AzureRmLoadBalancer | Select Name, ResourceGroupName`

<span data-ttu-id="9e537-135">PowerShell jest nieco bardziej skomplikowane niż hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9e537-135">PowerShell is a little more complicated than hello Azure CLI.</span></span> <span data-ttu-id="9e537-136">Koncepcyjnie wykonaj następujące kroki toocreate hello reguły.</span><span class="sxs-lookup"><span data-stu-id="9e537-136">Conceptually, do hello following steps toocreate a rule.</span></span>

1. <span data-ttu-id="9e537-137">Pobierz hello modułu równoważenia obciążenia z platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9e537-137">Get hello load balancer from Azure.</span></span>
2. <span data-ttu-id="9e537-138">Utwórz regułę.</span><span class="sxs-lookup"><span data-stu-id="9e537-138">Create a rule.</span></span>
3. <span data-ttu-id="9e537-139">Dodaj hello reguły toohello — moduł równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="9e537-139">Add hello rule toohello load balancer.</span></span>
4. <span data-ttu-id="9e537-140">Zaktualizuj hello modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="9e537-140">Update hello load balancer.</span></span>

```powershell
# Get hello load balancer
$lb = Get-AzureRmLoadBalancer -Name LB-svcfab3 -ResourceGroupName svcfab_cli

# Create hello rule based on information from hello load balancer.
$lbrule = New-AzureRmLoadBalancerRuleConfig -Name my-app-rule7 -Protocol Tcp -FrontendPort 39990 -BackendPort 40009 `
                                            -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
                                            -BackendAddressPool  $lb.BackendAddressPools[0] `
                                            -Probe $lb.Probes[0]

# Add hello rule toohello load balancer
$lb.LoadBalancingRules.Add($lbrule)

# Update hello load balancer on Azure
$lb | Set-AzureRmLoadBalancer
```

<span data-ttu-id="9e537-141">Dotyczące hello `New-AzureRmLoadBalancerRuleConfig` polecenia hello `-FrontendPort` udostępnia usługi równoważenia obciążenia hello reprezentuje hello port dla połączeń zewnętrznych i hello `-BackendPort` nasłuchuje reprezentuje hello portu hello usługi sieć szkieletowa aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9e537-141">Regarding hello `New-AzureRmLoadBalancerRuleConfig` command, hello `-FrontendPort` represents hello port hello load balancer exposes for external connections, and hello `-BackendPort` represents hello port hello service fabric app is listening to.</span></span>

>[!NOTE]
><span data-ttu-id="9e537-142">Aby uzyskać więcej informacji na toocreate modułu równoważenia obciążenia przy użyciu programu PowerShell, zobacz temat [tworzenia modułu równoważenia obciążenia przy użyciu programu PowerShell](..\load-balancer\load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="9e537-142">For more information on how toocreate a load balancer with PowerShell, see [Create a load balancer with PowerShell](..\load-balancer\load-balancer-get-started-internet-arm-ps.md).</span></span>

