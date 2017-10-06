---
title: "Wewnętrzny moduł równoważenia obciążenia dla usług w chmurze Azure aaaCreate | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak usługa równoważenia w hello klasycznego modelu wdrażania przy użyciu programu PowerShell obciążenia toocreate jako wewnętrzne"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 57966056-0f46-4f95-a295-483ca1ad135d
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: fe7975bca7bec3248626b0ad0fad6823e278ade2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-for-cloud-services"></a><span data-ttu-id="dccd6-103">Wprowadzenie do tworzenia wewnętrznego modułu równoważenia obciążenia (klasycznego) dla usług w chmurze</span><span class="sxs-lookup"><span data-stu-id="dccd6-103">Get started creating an internal load balancer (classic) for cloud services</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="dccd6-104">Program PowerShell</span><span class="sxs-lookup"><span data-stu-id="dccd6-104">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [<span data-ttu-id="dccd6-105">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="dccd6-105">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [<span data-ttu-id="dccd6-106">Usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="dccd6-106">Cloud services</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

> [!IMPORTANT]
> <span data-ttu-id="dccd6-107">Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="dccd6-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="dccd6-108">W tym artykule omówiono przy użyciu hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="dccd6-108">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="dccd6-109">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="dccd6-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="dccd6-110">Dowiedz się, jak za[wykonaj te czynności przy użyciu modelu Resource Manager hello](load-balancer-get-started-ilb-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="dccd6-110">Learn how too[perform these steps using hello Resource Manager model](load-balancer-get-started-ilb-arm-ps.md).</span></span>

## <a name="configure-internal-load-balancer-for-cloud-services"></a><span data-ttu-id="dccd6-111">Konfigurowanie wewnętrznego modułu równoważenia obciążenia dla usług w chmurze</span><span class="sxs-lookup"><span data-stu-id="dccd6-111">Configure internal load balancer for cloud services</span></span>

<span data-ttu-id="dccd6-112">Wewnętrzny moduł równoważenia obciążenia może być zastosowany zarówno do maszyn wirtualnych, jak i usług w chmurze.</span><span class="sxs-lookup"><span data-stu-id="dccd6-112">Internal load balancer is supported for both virtual machines and cloud services.</span></span> <span data-ttu-id="dccd6-113">Punkt końcowy usługi równoważenia obciążenia wewnętrznego utworzone w usłudze w chmurze, który znajduje się poza regionalną sieć wirtualną będzie dostępna tylko w obrębie hello usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="dccd6-113">An internal load balancer endpoint created in a cloud service that is outside a regional virtual network will be accessible only within hello cloud service.</span></span>

<span data-ttu-id="dccd6-114">Konfiguracja usługi równoważenia obciążenia wewnętrznego Hello ma toobe ustawić podczas tworzenia hello hello pierwszym wdrożeniu hello w usłudze w chmurze, jak pokazano w poniższym przykładzie hello.</span><span class="sxs-lookup"><span data-stu-id="dccd6-114">hello internal load balancer configuration has toobe set during hello creation of hello first deployment in hello cloud service, as shown in hello sample below.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dccd6-115">Poniższe kroki hello toorun wymagań wstępnych jest toohave sieci wirtualnej już utworzone dla hello wdrożenie chmury.</span><span class="sxs-lookup"><span data-stu-id="dccd6-115">A prerequisite toorun hello steps below is toohave a virtual network already created for hello cloud deployment.</span></span> <span data-ttu-id="dccd6-116">Konieczne będzie hello sieci wirtualnej nazwy i podsieci nazwę toocreate hello wewnętrzne Równoważenie obciążenia sieciowego.</span><span class="sxs-lookup"><span data-stu-id="dccd6-116">You will need hello virtual network name and subnet name toocreate hello Internal Load Balancing.</span></span>

### <a name="step-1"></a><span data-ttu-id="dccd6-117">Krok 1</span><span class="sxs-lookup"><span data-stu-id="dccd6-117">Step 1</span></span>

<span data-ttu-id="dccd6-118">Otwórz plik konfiguracji usługi hello (cscfg) dla danego wdrożenia chmury w programie Visual Studio i Dodaj powitania po ostatniej hello toocreate sekcji wewnętrzne Równoważenie obciążenia sieciowego w obszarze hello "`</Role>`" elementu hello konfiguracji sieci.</span><span class="sxs-lookup"><span data-stu-id="dccd6-118">Open hello service configuration file (.cscfg) for your cloud deployment in Visual Studio and add hello following section toocreate hello Internal Load Balancing under hello last "`</Role>`" item for hello network configuration.</span></span>

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="name of hello load balancer">
        <FrontendIPConfiguration type="private" subnet="subnet-name" staticVirtualNetworkIPAddress="static-IP-address"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

<span data-ttu-id="dccd6-119">Dodajmy hello wartości hello sieci konfiguracji pliku tooshow wyglądu.</span><span class="sxs-lookup"><span data-stu-id="dccd6-119">Let's add hello values for hello network configuration file tooshow how it will look.</span></span> <span data-ttu-id="dccd6-120">Przykład Witaj przyjęto założenie, że utworzono sieci wirtualnej o nazwie "test_vnet" z 10.0.0.0/24 podsieci o nazwie test_subnet i statycznego adresu IP 10.0.0.4.</span><span class="sxs-lookup"><span data-stu-id="dccd6-120">In hello example, assume you created a VNet called "test_vnet" with a subnet 10.0.0.0/24 called test_subnet and a static IP 10.0.0.4.</span></span> <span data-ttu-id="dccd6-121">Moduł równoważenia obciążenia Hello będzie miała nazwę testLB.</span><span class="sxs-lookup"><span data-stu-id="dccd6-121">hello load balancer will be named testLB.</span></span>

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="testLB">
        <FrontendIPConfiguration type="private" subnet="test_subnet" staticVirtualNetworkIPAddress="10.0.0.4"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

<span data-ttu-id="dccd6-122">Aby uzyskać więcej informacji o schemacie modułu równoważenia obciążenia hello, zobacz [modułu równoważenia obciążenia Dodaj](https://msdn.microsoft.com/library/azure/dn722411.aspx).</span><span class="sxs-lookup"><span data-stu-id="dccd6-122">For more information about hello load balancer schema, see [Add load balancer](https://msdn.microsoft.com/library/azure/dn722411.aspx).</span></span>

### <a name="step-2"></a><span data-ttu-id="dccd6-123">Krok 2</span><span class="sxs-lookup"><span data-stu-id="dccd6-123">Step 2</span></span>

<span data-ttu-id="dccd6-124">Zmień hello usługi definicji (csdef) pliku tooadd punkty końcowe toohello wewnętrzne Równoważenie obciążenia sieciowego.</span><span class="sxs-lookup"><span data-stu-id="dccd6-124">Change hello service definition (.csdef) file tooadd endpoints toohello Internal Load Balancing.</span></span> <span data-ttu-id="dccd6-125">obecnie Hello utworzeniu wystąpienia roli, pliku definicji usługi hello doda toohello wystąpień roli hello wewnętrzne Równoważenie obciążenia sieciowego.</span><span class="sxs-lookup"><span data-stu-id="dccd6-125">hello moment a role instance is created, hello service definition file will add hello role instances toohello Internal Load Balancing.</span></span>

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" loadBalancer="load-balancer-name" />
    </Endpoints>
</WorkerRole>
```

<span data-ttu-id="dccd6-126">Następujące hello takie same wartości w powyższym przykładzie hello możemy dodać pliku definicji usługi hello wartości toohello.</span><span class="sxs-lookup"><span data-stu-id="dccd6-126">Following hello same values from hello example above, let's add hello values toohello service definition file.</span></span>

```xml
<WorkerRole name="WorkerRole1" vmsize="A7" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="endpoint1" protocol="http" localPort="80" port="80" loadBalancer="testLB" />
    </Endpoints>
</WorkerRole>
```

<span data-ttu-id="dccd6-127">ruch sieciowy Hello będzie równoważone za pomocą usługi równoważenia obciążenia testLB hello przy użyciu portu 80 dla żądań przychodzących, wysyłanie tooworker wystąpień roli również na porcie 80.</span><span class="sxs-lookup"><span data-stu-id="dccd6-127">hello network traffic will be load balanced using hello testLB load balancer using port 80 for incoming requests, sending tooworker role instances also on port 80.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dccd6-128">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="dccd6-128">Next steps</span></span>

<span data-ttu-id="dccd6-129">[Configure a load balancer distribution mode using source IP affinity](load-balancer-distribution-mode.md) (Konfigurowanie trybu dystrybucji modułu równoważenia obciążenia przy użyciu koligacji źródłowych adresów IP)</span><span class="sxs-lookup"><span data-stu-id="dccd6-129">[Configure a load balancer distribution mode using source IP affinity](load-balancer-distribution-mode.md)</span></span>

<span data-ttu-id="dccd6-130">[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md) (Konfigurowanie ustawień limitu czasu bezczynności protokołu TCP dla modułu równoważenia obciążenia)</span><span class="sxs-lookup"><span data-stu-id="dccd6-130">[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md)</span></span>

