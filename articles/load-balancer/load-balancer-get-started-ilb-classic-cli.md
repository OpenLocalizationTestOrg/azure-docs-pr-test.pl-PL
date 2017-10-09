---
title: "aaaCreate wewnętrzne załadować równoważenia - klasycznego wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak hello toocreate usługi równoważenia obciążenia wewnętrznego przy użyciu wiersza polecenia platformy Azure w hello klasycznego modelu wdrażania"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: becbbbde-a118-4269-9444-d3153f00bf34
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: ef29dfda5f7a75a411bbabe8b688a31c6bf81113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-using-hello-azure-cli"></a><span data-ttu-id="28e2f-103">Rozpoczynanie pracy tworzenia wewnętrznego modułu równoważenia obciążenia (klasyczne) przy użyciu hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="28e2f-103">Get started creating an internal load balancer (classic) using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="28e2f-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="28e2f-104">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [<span data-ttu-id="28e2f-105">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="28e2f-105">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [<span data-ttu-id="28e2f-106">Usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="28e2f-106">Cloud services</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="28e2f-107">Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="28e2f-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="28e2f-108">W tym artykule omówiono przy użyciu hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="28e2f-108">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="28e2f-109">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="28e2f-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="28e2f-110">Dowiedz się, jak za[wykonaj te czynności przy użyciu modelu Resource Manager hello](load-balancer-get-started-ilb-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="28e2f-110">Learn how too[perform these steps using hello Resource Manager model](load-balancer-get-started-ilb-arm-cli.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="toocreate-an-internal-load-balancer-set-for-virtual-machines"></a><span data-ttu-id="28e2f-111">toocreate wewnętrznego modułu równoważenia obciążenia dla maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="28e2f-111">toocreate an internal load balancer set for virtual machines</span></span>

<span data-ttu-id="28e2f-112">toocreate wewnętrznego modułu równoważenia obciążenia ustaw i hello serwerów, które będzie wysyłać ich tooit ruchu, należy wykonać następujące hello:</span><span class="sxs-lookup"><span data-stu-id="28e2f-112">toocreate an internal load balancer set and hello servers that will send their traffic tooit, you must do hello following:</span></span>

1. <span data-ttu-id="28e2f-113">Utwórz wystąpienie wewnętrzne Równoważenie obciążenia sieciowego, który będzie hello punkt końcowy przychodzącego ruchu toobe równoważone między serwerami hello zestawu z równoważeniem obciążenia.</span><span class="sxs-lookup"><span data-stu-id="28e2f-113">Create an instance of Internal Load Balancing that will be hello endpoint of incoming traffic toobe load balanced across hello servers of a load-balanced set.</span></span>
2. <span data-ttu-id="28e2f-114">Dodawanie punktów końcowych odpowiadającego toohello maszyn wirtualnych, które będzie otrzymywał hello ruchu przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="28e2f-114">Add endpoints corresponding toohello virtual machines that will be receiving hello incoming traffic.</span></span>
3. <span data-ttu-id="28e2f-115">Konfigurowanie serwerów hello, które będą wysyłane się, że hello ruchu toobe o zrównoważonym obciążeniu toosend ich ruchu toohello wirtualny adres IP (VIP) wystąpienia hello wewnętrzne Równoważenie obciążenia sieciowego.</span><span class="sxs-lookup"><span data-stu-id="28e2f-115">Configure hello servers that will be sending hello traffic toobe load balanced toosend their traffic toohello virtual IP (VIP) address of hello Internal Load Balancing instance.</span></span>

## <a name="step-by-step-creating-an-internal-load-balancer-using-cli"></a><span data-ttu-id="28e2f-116">Szczegółowy opis tworzenia wewnętrznego modułu równoważenia obciążenia przy użyciu interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="28e2f-116">Step by step creating an internal load balancer using CLI</span></span>

<span data-ttu-id="28e2f-117">Ten przewodnik zawiera jak toocreate wewnętrznego modułu równoważenia obciążenia na podstawie scenariusza hello powyżej.</span><span class="sxs-lookup"><span data-stu-id="28e2f-117">This guide shows how toocreate an internal load balancer based on hello scenario above.</span></span>

1. <span data-ttu-id="28e2f-118">Jeśli po raz pierwszy używasz interfejsu wiersza polecenia Azure, zobacz [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](../cli-install-nodejs.md) i wykonaj instrukcje hello zapasowej punktu toohello, gdzie należy wybrać konto platformy Azure i subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="28e2f-118">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="28e2f-119">Uruchom hello **trybie azure config** polecenia tooswitch tooclassic tryb, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="28e2f-119">Run hello **azure config mode** command tooswitch tooclassic mode, as shown below.</span></span>

    ```azurecli
    azure config mode asm
    ```

    <span data-ttu-id="28e2f-120">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="28e2f-120">Expected output:</span></span>

        info:    New mode is asm

## <a name="create-endpoint-and-load-balancer-set"></a><span data-ttu-id="28e2f-121">Tworzenie punktu końcowego i zestawu modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="28e2f-121">Create endpoint and load balancer set</span></span>

<span data-ttu-id="28e2f-122">Hello scenariusz zakłada hello maszyn wirtualnych "DB1" i "Bazy danych DB2" w usłudze w chmurze o nazwie "mytestcloud".</span><span class="sxs-lookup"><span data-stu-id="28e2f-122">hello scenario assumes hello virtual machines "DB1" and "DB2" in a cloud service called "mytestcloud".</span></span> <span data-ttu-id="28e2f-123">Obie maszyny wirtualne korzystają z sieci wirtualnej o nazwie „testvnet” z podsiecią o nazwie „subnet-1”.</span><span class="sxs-lookup"><span data-stu-id="28e2f-123">Both virtual machines are using a virtual network called my "testvnet" with subnet "subnet-1".</span></span>

<span data-ttu-id="28e2f-124">W tym przewodniku opisano sposób tworzenia zestawu wewnętrznego modułu równoważenia obciążenia przy użyciu portu 1433 jako portu publicznego i lokalnego.</span><span class="sxs-lookup"><span data-stu-id="28e2f-124">This guide will create an internal load balancer set using port 1433 as private port and 1433 as local port.</span></span>

<span data-ttu-id="28e2f-125">To jest typowy scenariusz, w którym masz SQL maszyn wirtualnych na powitania zaplecza przy użyciu serwerów baz danych hello tooguarantee obciążenia wewnętrznego modułu równoważenia nie będą widoczne, bezpośrednio za pomocą publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="28e2f-125">This is a common scenario where you have SQL virtual machines on hello back end using an internal load balancer tooguarantee hello database servers won't be exposed directly using a public IP address.</span></span>

### <a name="step-1"></a><span data-ttu-id="28e2f-126">Krok 1</span><span class="sxs-lookup"><span data-stu-id="28e2f-126">Step 1</span></span>

<span data-ttu-id="28e2f-127">Utwórz zestaw wewnętrznego modułu równoważenia obciążenia za pomocą polecenia `azure network service internal-load-balancer add`.</span><span class="sxs-lookup"><span data-stu-id="28e2f-127">Create an internal load balancer set using `azure network service internal-load-balancer add`.</span></span>

```azurecli
azure service internal-load-balancer add --serviceName mytestcloud --internalLBName ilbset --subnet-name subnet-1 --static-virtualnetwork-ipaddress 192.168.2.7
```

<span data-ttu-id="28e2f-128">Użyj polecenia `azure service internal-load-balancer --help`, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="28e2f-128">Check out `azure service internal-load-balancer --help` for more information.</span></span>

<span data-ttu-id="28e2f-129">Możesz sprawdzić właściwości usługi równoważenia obciążenia wewnętrznego hello za pomocą polecenia hello `azure service internal-load-balancer list` *nazwa usługi w chmurze*.</span><span class="sxs-lookup"><span data-stu-id="28e2f-129">You can check hello internal load balancer properties using hello command `azure service internal-load-balancer list` *cloud service name*.</span></span>

<span data-ttu-id="28e2f-130">W tym miejscu następujący przykład danych wyjściowych hello:</span><span class="sxs-lookup"><span data-stu-id="28e2f-130">Here follows an example of hello output:</span></span>

    azure service internal-load-balancer list my-testcloud
    info:    Executing command service internal-load-balancer list
    + Getting cloud service deployment
    data:    Name    Type     SubnetName  StaticVirtualNetworkIPAddress
    data:    ------  -------  ----------  -----------------------------
    data:    ilbset  Private  subnet-1    192.168.2.7
    info:    service internal-load-balancer list command OK


### <a name="step-2"></a><span data-ttu-id="28e2f-131">Krok 2</span><span class="sxs-lookup"><span data-stu-id="28e2f-131">Step 2</span></span>

<span data-ttu-id="28e2f-132">Możesz skonfigurować hello wewnętrznego modułu równoważenia obciążenia ustawić po dodaniu hello pierwszym punktem końcowym.</span><span class="sxs-lookup"><span data-stu-id="28e2f-132">You configure hello internal load balancer set when you add hello first endpoint.</span></span> <span data-ttu-id="28e2f-133">Skojarzysz hello punktu końcowego, maszyny wirtualnej i badania portu toohello wewnętrznego modułu równoważenia obciążenia w tym kroku.</span><span class="sxs-lookup"><span data-stu-id="28e2f-133">You will associate hello endpoint, virtual machine and probe port toohello internal load balancer set in this step.</span></span>

```azurecli
azure vm endpoint create db1 1433 --local-port 1433 --protocol tcp --probe-port 1433 --probe-protocol tcp --probe-interval 300 --probe-timeout 600 --internal-load-balancer-name ilbset
```

### <a name="step-3"></a><span data-ttu-id="28e2f-134">Krok 3</span><span class="sxs-lookup"><span data-stu-id="28e2f-134">Step 3</span></span>

<span data-ttu-id="28e2f-135">Sprawdzić z konfiguracji usługi równoważenia obciążenia hello `azure vm show` *nazwę maszyny wirtualnej*</span><span class="sxs-lookup"><span data-stu-id="28e2f-135">Verify hello load balancer configuration using `azure vm show` *virtual machine name*</span></span>

```azurecli
azure vm show DB1
```

<span data-ttu-id="28e2f-136">Witaj dane wyjściowe będą mieć:</span><span class="sxs-lookup"><span data-stu-id="28e2f-136">hello output will be:</span></span>

    azure vm show DB1
    info:    Executing command vm show
    + Getting virtual machines
    data:    DNSName "mytestcloud.cloudapp.net"
    data:    Location "East US 2"
    data:    VMName "DB1"
    data:    IPAddress "192.168.2.4"
    data:    InstanceStatus "ReadyRole"
    data:    InstanceSize "Standard_D1"
    data:    Image "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-20151022-en.us-127GB.vhd"
    data:    OSDisk hostCaching "ReadWrite"
    data:    OSDisk name "db1-DB1-0-201511120457370846"
    data:    OSDisk mediaLink "https://XXXX.blob.core.windows.net/vhd"
    data:    OSDisk sourceImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-20151022-en.us-127GB.vhd"
    data:    OSDisk operatingSystem "Windows"
    data:    OSDisk iOType "Standard"
    data:    ReservedIPName ""
    data:    VirtualIPAddresses 0 address "137.116.64.107"
    data:    VirtualIPAddresses 0 name "db1ContractContract"
    data:    VirtualIPAddresses 0 isDnsProgrammed true
    data:    VirtualIPAddresses 1 address "192.168.2.7"
    data:    VirtualIPAddresses 1 name "ilbset"
    data:    Network Endpoints 0 localPort 5986
    data:    Network Endpoints 0 name "PowerShell"
    data:    Network Endpoints 0 port 5986
    data:    Network Endpoints 0 protocol "tcp"
    data:    Network Endpoints 0 virtualIPAddress "137.116.64.107"
    data:    Network Endpoints 0 enableDirectServerReturn false
    data:    Network Endpoints 1 localPort 3389
    data:    Network Endpoints 1 name "Remote Desktop"
    data:    Network Endpoints 1 port 60173
    data:    Network Endpoints 1 protocol "tcp"
    data:    Network Endpoints 1 virtualIPAddress "137.116.64.107"
    data:    Network Endpoints 1 enableDirectServerReturn false
    data:    Network Endpoints 2 localPort 1433
    data:    Network Endpoints 2 name "tcp-1433-1433"
    data:    Network Endpoints 2 port 1433
    data:    Network Endpoints 2 loadBalancerProbe port 1433
    data:    Network Endpoints 2 loadBalancerProbe protocol "tcp"
    data:    Network Endpoints 2 loadBalancerProbe intervalInSeconds 300
    data:    Network Endpoints 2 loadBalancerProbe timeoutInSeconds 600
    data:    Network Endpoints 2 protocol "tcp"
    data:    Network Endpoints 2 virtualIPAddress "192.168.2.7"
    data:    Network Endpoints 2 enableDirectServerReturn false
    data:    Network Endpoints 2 loadBalancerName "ilbset"
    info:    vm show command OK

## <a name="create-a-remote-desktop-endpoint-for-a-virtual-machine"></a><span data-ttu-id="28e2f-137">Tworzenie punktu końcowego pulpitu zdalnego maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="28e2f-137">Create a remote desktop endpoint for a virtual machine</span></span>

<span data-ttu-id="28e2f-138">Ruch sieciowy tooforward zdalny punkt końcowy pulpitu można utworzyć na podstawie port publiczny port lokalny tooa dla określonej maszyny wirtualnej przy użyciu `azure vm endpoint create`.</span><span class="sxs-lookup"><span data-stu-id="28e2f-138">You can create a remote desktop endpoint tooforward network traffic from a public port tooa local port for a specific virtual machine using `azure vm endpoint create`.</span></span>

```azurecli
azure vm endpoint create web1 54580 -k 3389
```

## <a name="remove-virtual-machine-from-load-balancer"></a><span data-ttu-id="28e2f-139">Usuwanie maszyny wirtualnej z modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="28e2f-139">Remove virtual machine from load balancer</span></span>

<span data-ttu-id="28e2f-140">Możesz usunąć maszynę wirtualną z wewnętrznego modułu równoważenia obciążenia ustawione przez usuwanie punktu końcowego hello skojarzone.</span><span class="sxs-lookup"><span data-stu-id="28e2f-140">You can remove a virtual machine from an internal load balancer set by deleting hello associated endpoint.</span></span> <span data-ttu-id="28e2f-141">Po usunięciu punktu końcowego hello hello maszyny wirtualnej nie należą już zestaw modułów równoważenia obciążenia toohello.</span><span class="sxs-lookup"><span data-stu-id="28e2f-141">Once hello endpoint is removed, hello virtual machine won't belong toohello load balancer set anymore.</span></span>

<span data-ttu-id="28e2f-142">Za pomocą powyższego przykładu hello, można usunąć punktu końcowego hello utworzone dla maszyny wirtualnej "DB1" z wewnętrznego modułu równoważenia obciążenia "ilbset" za pomocą polecenia hello `azure vm endpoint delete`.</span><span class="sxs-lookup"><span data-stu-id="28e2f-142">Using hello example above, you can remove hello endpoint created for virtual machine "DB1" from internal load balancer "ilbset" by using hello command `azure vm endpoint delete`.</span></span>

```azurecli
azure vm endpoint delete DB1 tcp-1433-1433
```

<span data-ttu-id="28e2f-143">Użyj polecenia `azure vm endpoint --help`, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="28e2f-143">Check out `azure vm endpoint --help` for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="28e2f-144">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="28e2f-144">Next steps</span></span>

<span data-ttu-id="28e2f-145">[Configure a load balancer distribution mode using source IP affinity](load-balancer-distribution-mode.md) (Konfigurowanie trybu dystrybucji modułu równoważenia obciążenia przy użyciu koligacji źródłowych adresów IP)</span><span class="sxs-lookup"><span data-stu-id="28e2f-145">[Configure a load balancer distribution mode using source IP affinity](load-balancer-distribution-mode.md)</span></span>

<span data-ttu-id="28e2f-146">[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md) (Konfigurowanie ustawień limitu czasu bezczynności protokołu TCP dla modułu równoważenia obciążenia)</span><span class="sxs-lookup"><span data-stu-id="28e2f-146">[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md)</span></span>
