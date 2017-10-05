---
title: "Tworzenie reguły modułu równoważenia obciążenia Azure dla klastra"
description: "Konfigurowanie usługi równoważenia obciążenia Azure otworzyć porty dla klastra usługi sieć szkieletowa usług Azure."
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
ms.openlocfilehash: c99c4d9f343ca97fd3cd363fb54feaf5507bb77c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="open-ports-for-a-service-fabric-cluster"></a><span data-ttu-id="4a270-103">Otwieranie portów dla klastra sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="4a270-103">Open ports for a Service Fabric cluster</span></span>

<span data-ttu-id="4a270-104">Moduł równoważenia obciążenia z klastra usługi sieć szkieletowa usług Azure kieruje ruch do aplikacji uruchomionej w węźle.</span><span class="sxs-lookup"><span data-stu-id="4a270-104">The load balancer deployed with your Azure Service Fabric cluster directs traffic to your app running on a node.</span></span> <span data-ttu-id="4a270-105">Jeśli zmienisz aplikację do używania innego portu, musi ujawniać tego portu (lub trasy innego portu) w usłudze równoważenia obciążenia Azure.</span><span class="sxs-lookup"><span data-stu-id="4a270-105">If you change your app to use a different port, you must expose that port (or route a different port) in the Azure Load Balancer.</span></span>

<span data-ttu-id="4a270-106">Po wdrożeniu klastra sieci szkieletowej usług Azure modułu równoważenia obciążenia został utworzony automatycznie.</span><span class="sxs-lookup"><span data-stu-id="4a270-106">When you deployed your service fabric cluster to Azure, a load balancer was automatically created for you.</span></span> <span data-ttu-id="4a270-107">Jeśli nie masz usługi równoważenia obciążenia, zobacz [skonfigurowania funkcji równoważenia obciążenia internetowy](..\load-balancer\load-balancer-get-started-internet-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4a270-107">If you do not have a load balancer, see [Configure an Internet-facing load balancer](..\load-balancer\load-balancer-get-started-internet-portal.md).</span></span>

## <a name="configure-service-fabric"></a><span data-ttu-id="4a270-108">Konfigurowanie sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="4a270-108">Configure service fabric</span></span>

<span data-ttu-id="4a270-109">Aplikacja usługi Service Fabric **ServiceManifest.xml** pliku konfiguracyjnego definiuje punkty końcowe aplikacji zamierza użyć.</span><span class="sxs-lookup"><span data-stu-id="4a270-109">Your Service Fabric application **ServiceManifest.xml** config file defines the endpoints your application expects to use.</span></span> <span data-ttu-id="4a270-110">Po plik konfiguracji został zaktualizowany tak, aby zdefiniować punkt końcowy, Usługa równoważenia obciążenia muszą zostać zaktualizowane do udostępnienia, który (lub innej) portu.</span><span class="sxs-lookup"><span data-stu-id="4a270-110">After the config file has been updated to define an endpoint, the load balancer must be updated to expose that (or a different) port.</span></span> <span data-ttu-id="4a270-111">Aby uzyskać więcej informacji na temat tworzenia punktu końcowego sieci szkieletowej usług, zobacz [Konfiguracja punktu końcowego](service-fabric-service-manifest-resources.md).</span><span class="sxs-lookup"><span data-stu-id="4a270-111">For more information on how to create the service fabric endpoint, see [Setup an Endpoint](service-fabric-service-manifest-resources.md).</span></span>

## <a name="create-a-load-balancer-rule"></a><span data-ttu-id="4a270-112">Tworzenie reguły modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="4a270-112">Create a load balancer rule</span></span>

<span data-ttu-id="4a270-113">Reguły modułu równoważenia obciążenia otwiera port połączonych z Internetem i przekazuje ruch do portu węzeł wewnętrzny używany przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="4a270-113">A load balancer rule opens up an internet-facing port and forwards traffic to the internal node's port used by your application.</span></span> <span data-ttu-id="4a270-114">Jeśli nie masz usługi równoważenia obciążenia, zobacz [skonfigurowania funkcji równoważenia obciążenia internetowy](..\load-balancer\load-balancer-get-started-internet-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4a270-114">If you do not have a load balancer, see [Configure an Internet-facing load balancer](..\load-balancer\load-balancer-get-started-internet-portal.md).</span></span>

<span data-ttu-id="4a270-115">Aby utworzyć regułę modułu równoważenia obciążenia, które należy zebrać następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="4a270-115">To create a load balancer rule, you need to collect the following information:</span></span>

- <span data-ttu-id="4a270-116">Nazwa modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="4a270-116">Load balancer name.</span></span>
- <span data-ttu-id="4a270-117">Grupa zasobów klastra sieci szkieletowej usług i usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="4a270-117">Resource group of the load balancer and service fabric cluster.</span></span>
- <span data-ttu-id="4a270-118">Portu zewnętrznego.</span><span class="sxs-lookup"><span data-stu-id="4a270-118">External port.</span></span>
- <span data-ttu-id="4a270-119">Port wewnętrzny.</span><span class="sxs-lookup"><span data-stu-id="4a270-119">Internal port.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="4a270-120">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="4a270-120">Azure CLI</span></span>
>[!NOTE]
><span data-ttu-id="4a270-121">Jeśli trzeba określić nazwę modułu równoważenia obciążenia, użyj tego polecenia, aby szybko uzyskać listę wszystkich usług równoważenia obciążenia i grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="4a270-121">If you need to determine the name of the load balancer, use this command to quickly get a list of all load balancers and the associated resource groups.</span></span>
>
>`az network lb list --query "[].{ResourceGroup: resourceGroup, Name: name}"`
>

<span data-ttu-id="4a270-122">Wymaga tylko jednego polecenia, aby utworzyć regułę modułu równoważenia obciążenia z **interfejsu wiersza polecenia Azure**.</span><span class="sxs-lookup"><span data-stu-id="4a270-122">It only takes a single command to create a load balancer rule with the **Azure CLI**.</span></span> <span data-ttu-id="4a270-123">Wystarczy znać nazwę grupy równoważenia i zasobów obciążenia, aby utworzyć nową regułę.</span><span class="sxs-lookup"><span data-stu-id="4a270-123">You just need to know both the name of the load balancer and resource group to create a new rule.</span></span>

```azurecli
az network lb rule create --backend-port 40000 --frontend-port 39999 --protocol Tcp --lb-name LB-svcfab3 -g svcfab_cli -n my-app-rule
```

<span data-ttu-id="4a270-124">Polecenie wiersza polecenia platformy Azure ma kilka parametrów, które zostały opisane w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="4a270-124">The Azure CLI command has a few parameters that are described in the following table:</span></span>

| <span data-ttu-id="4a270-125">Parametr</span><span class="sxs-lookup"><span data-stu-id="4a270-125">Parameter</span></span> | <span data-ttu-id="4a270-126">Opis</span><span class="sxs-lookup"><span data-stu-id="4a270-126">Description</span></span> |
| --------- | ----------- |
| `--backend-port`  | <span data-ttu-id="4a270-127">Nasłuchuje portu aplikacji sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="4a270-127">The port the service fabric application is listening to.</span></span> |
| `--frontend-port` | <span data-ttu-id="4a270-128">Udostępnia portu usługi równoważenia obciążenia dla połączeń zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="4a270-128">The port the load balancer exposes for external connections.</span></span> |
| `-lb-name` | <span data-ttu-id="4a270-129">Nazwa modułu równoważenia obciążenia, aby zmienić.</span><span class="sxs-lookup"><span data-stu-id="4a270-129">The name of the load balancer to change.</span></span> |
| `-g`       | <span data-ttu-id="4a270-130">Grupy zasobów, usługi równoważenia obciążenia i klastra sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="4a270-130">The resource group that has both the load balancer and service fabric cluster.</span></span> |
| `-n`       | <span data-ttu-id="4a270-131">Nazwa wybranej reguły.</span><span class="sxs-lookup"><span data-stu-id="4a270-131">The chosen name of the rule.</span></span> |


>[!NOTE]
><span data-ttu-id="4a270-132">Aby uzyskać więcej informacji na temat tworzenia modułu równoważenia obciążenia z wiersza polecenia platformy Azure, zobacz [Utwórz usługę równoważenia obciążenia z wiersza polecenia platformy Azure](..\load-balancer\load-balancer-get-started-internet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="4a270-132">For more information on how to create a load balancer with the Azure CLI, see [Create a load balancer with the Azure CLI](..\load-balancer\load-balancer-get-started-internet-arm-cli.md).</span></span>

## <a name="powershell"></a><span data-ttu-id="4a270-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4a270-133">PowerShell</span></span>

>[!NOTE]
><span data-ttu-id="4a270-134">Jeśli trzeba określić nazwę modułu równoważenia obciążenia, użyj tego polecenia, aby szybko uzyskać listę wszystkich usług równoważenia obciążenia i grup zasobów.</span><span class="sxs-lookup"><span data-stu-id="4a270-134">If you need to determine the name of the load balancer, use this command to quickly get a list of all load balancers and associated resource groups.</span></span>
>
>`Get-AzureRmLoadBalancer | Select Name, ResourceGroupName`

<span data-ttu-id="4a270-135">PowerShell jest nieco bardziej skomplikowane niż wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4a270-135">PowerShell is a little more complicated than the Azure CLI.</span></span> <span data-ttu-id="4a270-136">Koncepcyjnie wykonaj następujące kroki, aby utworzyć regułę.</span><span class="sxs-lookup"><span data-stu-id="4a270-136">Conceptually, do the following steps to create a rule.</span></span>

1. <span data-ttu-id="4a270-137">Pobierz moduł równoważenia obciążenia z platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4a270-137">Get the load balancer from Azure.</span></span>
2. <span data-ttu-id="4a270-138">Utwórz regułę.</span><span class="sxs-lookup"><span data-stu-id="4a270-138">Create a rule.</span></span>
3. <span data-ttu-id="4a270-139">Dodaj regułę modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="4a270-139">Add the rule to the load balancer.</span></span>
4. <span data-ttu-id="4a270-140">Aktualizacja usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="4a270-140">Update the load balancer.</span></span>

```powershell
# Get the load balancer
$lb = Get-AzureRmLoadBalancer -Name LB-svcfab3 -ResourceGroupName svcfab_cli

# Create the rule based on information from the load balancer.
$lbrule = New-AzureRmLoadBalancerRuleConfig -Name my-app-rule7 -Protocol Tcp -FrontendPort 39990 -BackendPort 40009 `
                                            -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
                                            -BackendAddressPool  $lb.BackendAddressPools[0] `
                                            -Probe $lb.Probes[0]

# Add the rule to the load balancer
$lb.LoadBalancingRules.Add($lbrule)

# Update the load balancer on Azure
$lb | Set-AzureRmLoadBalancer
```

<span data-ttu-id="4a270-141">Dotyczące `New-AzureRmLoadBalancerRuleConfig` polecenia `-FrontendPort` reprezentuje port udostępnia usługi równoważenia obciążenia dla połączeń zewnętrznych i `-BackendPort` reprezentuje port nasłuchuje aplikacji sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="4a270-141">Regarding the `New-AzureRmLoadBalancerRuleConfig` command, the `-FrontendPort` represents the port the load balancer exposes for external connections, and the `-BackendPort` represents the port the service fabric app is listening to.</span></span>

>[!NOTE]
><span data-ttu-id="4a270-142">Aby uzyskać więcej informacji na temat tworzenia modułu równoważenia obciążenia przy użyciu programu PowerShell, zobacz [tworzenia modułu równoważenia obciążenia przy użyciu programu PowerShell](..\load-balancer\load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="4a270-142">For more information on how to create a load balancer with PowerShell, see [Create a load balancer with PowerShell](..\load-balancer\load-balancer-get-started-internet-arm-ps.md).</span></span>

