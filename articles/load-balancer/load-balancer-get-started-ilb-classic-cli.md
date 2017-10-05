---
title: "Tworzenie wewnętrznego modułu równoważenia obciążenia — interfejs wiersza polecenia platformy Azure (model klasyczny) | Microsoft Docs"
description: "Dowiedz się, jak utworzyć wewnętrzny moduł równoważenia obciążenia w klasycznym modelu wdrażania przy użyciu interfejsu wiersza polecenia Azure"
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
ms.openlocfilehash: d24b95f75b5ffd1116b07cf9f8bac33767a9c835
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-using-the-azure-cli"></a><span data-ttu-id="b35e6-103">Wprowadzenie do tworzenia wewnętrznego modułu równoważenia obciążenia (w modelu klasycznym) przy użyciu interfejsu wiersza polecenia Azure</span><span class="sxs-lookup"><span data-stu-id="b35e6-103">Get started creating an internal load balancer (classic) using the Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b35e6-104">Program PowerShell</span><span class="sxs-lookup"><span data-stu-id="b35e6-104">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [<span data-ttu-id="b35e6-105">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b35e6-105">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [<span data-ttu-id="b35e6-106">Usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="b35e6-106">Cloud services</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="b35e6-107">Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="b35e6-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="b35e6-108">Ten artykuł dotyczy klasycznego modelu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="b35e6-108">This article covers using the classic deployment model.</span></span> <span data-ttu-id="b35e6-109">Firma Microsoft zaleca, aby w przypadku większości nowych wdrożeń korzystać z modelu opartego na programie Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b35e6-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="b35e6-110">Dowiedz się, jak [wykonać te kroki przy użyciu modelu usługi Resource Manager](load-balancer-get-started-ilb-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b35e6-110">Learn how to [perform these steps using the Resource Manager model](load-balancer-get-started-ilb-arm-cli.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="to-create-an-internal-load-balancer-set-for-virtual-machines"></a><span data-ttu-id="b35e6-111">Tworzenie zestawu wewnętrznego modułu równoważenia obciążenia dla maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="b35e6-111">To create an internal load balancer set for virtual machines</span></span>

<span data-ttu-id="b35e6-112">Aby utworzyć zestaw wewnętrznego modułu równoważenia obciążenia, a także serwery, które będą przesyłać do niego ruch, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b35e6-112">To create an internal load balancer set and the servers that will send their traffic to it, you must do the following:</span></span>

1. <span data-ttu-id="b35e6-113">Utwórz wystąpienie wewnętrznego równoważenia obciążenia, które będzie punktem końcowym przychodzącego ruchu sieciowego, aby obciążenie było zrównoważone między serwerami w zestawie o zrównoważonym obciążeniu.</span><span class="sxs-lookup"><span data-stu-id="b35e6-113">Create an instance of Internal Load Balancing that will be the endpoint of incoming traffic to be load balanced across the servers of a load-balanced set.</span></span>
2. <span data-ttu-id="b35e6-114">Dodaj punkty końcowe odpowiadające maszynom wirtualnym, które będą otrzymywać ruch przychodzący.</span><span class="sxs-lookup"><span data-stu-id="b35e6-114">Add endpoints corresponding to the virtual machines that will be receiving the incoming traffic.</span></span>
3. <span data-ttu-id="b35e6-115">Skonfiguruj serwery wysyłające ruch, którego obciążenie ma zostać zrównoważone, aby wysyłały ruch na wirtualny adres IP (VIP) wystąpienia wewnętrznego równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="b35e6-115">Configure the servers that will be sending the traffic to be load balanced to send their traffic to the virtual IP (VIP) address of the Internal Load Balancing instance.</span></span>

## <a name="step-by-step-creating-an-internal-load-balancer-using-cli"></a><span data-ttu-id="b35e6-116">Szczegółowy opis tworzenia wewnętrznego modułu równoważenia obciążenia przy użyciu interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="b35e6-116">Step by step creating an internal load balancer using CLI</span></span>

<span data-ttu-id="b35e6-117">W tym przewodniku opisano sposób tworzenia wewnętrznego modułu równoważenia obciążenia w oparciu o powyższy scenariusz.</span><span class="sxs-lookup"><span data-stu-id="b35e6-117">This guide shows how to create an internal load balancer based on the scenario above.</span></span>

1. <span data-ttu-id="b35e6-118">Jeśli po raz pierwszy używasz interfejsu wiersza polecenia Azure, zobacz artykuł [Instalowanie i konfigurowania interfejsu wiersza polecenia Azure](../cli-install-nodejs.md) i postępuj zgodnie z instrukcjami aż do punktu, w którym należy wybrać konto platformy Azure i subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="b35e6-118">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="b35e6-119">Uruchom polecenie **azure config mode**, aby przełączyć tryb na klasyczny, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="b35e6-119">Run the **azure config mode** command to switch to classic mode, as shown below.</span></span>

    ```azurecli
    azure config mode asm
    ```

    <span data-ttu-id="b35e6-120">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="b35e6-120">Expected output:</span></span>

        info:    New mode is asm

## <a name="create-endpoint-and-load-balancer-set"></a><span data-ttu-id="b35e6-121">Tworzenie punktu końcowego i zestawu modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="b35e6-121">Create endpoint and load balancer set</span></span>

<span data-ttu-id="b35e6-122">Na potrzeby scenariusza przyjmuje się, że utworzono maszyny wirtualne „DB1” i „DB2” w usłudze w chmurze o nazwie „mytestcloud”.</span><span class="sxs-lookup"><span data-stu-id="b35e6-122">The scenario assumes the virtual machines "DB1" and "DB2" in a cloud service called "mytestcloud".</span></span> <span data-ttu-id="b35e6-123">Obie maszyny wirtualne korzystają z sieci wirtualnej o nazwie „testvnet” z podsiecią o nazwie „subnet-1”.</span><span class="sxs-lookup"><span data-stu-id="b35e6-123">Both virtual machines are using a virtual network called my "testvnet" with subnet "subnet-1".</span></span>

<span data-ttu-id="b35e6-124">W tym przewodniku opisano sposób tworzenia zestawu wewnętrznego modułu równoważenia obciążenia przy użyciu portu 1433 jako portu publicznego i lokalnego.</span><span class="sxs-lookup"><span data-stu-id="b35e6-124">This guide will create an internal load balancer set using port 1433 as private port and 1433 as local port.</span></span>

<span data-ttu-id="b35e6-125">Jest to typowy scenariusz, w którym na zapleczu występują maszyny wirtualne SQL korzystające z wewnętrznego modułu równoważenia obciążenia, aby zagwarantować, że serwery bazy danych nie będą dostępne bezpośrednio przez publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="b35e6-125">This is a common scenario where you have SQL virtual machines on the back end using an internal load balancer to guarantee the database servers won't be exposed directly using a public IP address.</span></span>

### <a name="step-1"></a><span data-ttu-id="b35e6-126">Krok 1</span><span class="sxs-lookup"><span data-stu-id="b35e6-126">Step 1</span></span>

<span data-ttu-id="b35e6-127">Utwórz zestaw wewnętrznego modułu równoważenia obciążenia za pomocą polecenia `azure network service internal-load-balancer add`.</span><span class="sxs-lookup"><span data-stu-id="b35e6-127">Create an internal load balancer set using `azure network service internal-load-balancer add`.</span></span>

```azurecli
azure service internal-load-balancer add --serviceName mytestcloud --internalLBName ilbset --subnet-name subnet-1 --static-virtualnetwork-ipaddress 192.168.2.7
```

<span data-ttu-id="b35e6-128">Użyj polecenia `azure service internal-load-balancer --help`, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="b35e6-128">Check out `azure service internal-load-balancer --help` for more information.</span></span>

<span data-ttu-id="b35e6-129">Możesz sprawdzić właściwości wewnętrznego modułu równoważenia obciążenia za pomocą polecenia `azure service internal-load-balancer list` *nazwa usługi w chmurze*.</span><span class="sxs-lookup"><span data-stu-id="b35e6-129">You can check the internal load balancer properties using the command `azure service internal-load-balancer list` *cloud service name*.</span></span>

<span data-ttu-id="b35e6-130">Przykładowe dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="b35e6-130">Here follows an example of the output:</span></span>

    azure service internal-load-balancer list my-testcloud
    info:    Executing command service internal-load-balancer list
    + Getting cloud service deployment
    data:    Name    Type     SubnetName  StaticVirtualNetworkIPAddress
    data:    ------  -------  ----------  -----------------------------
    data:    ilbset  Private  subnet-1    192.168.2.7
    info:    service internal-load-balancer list command OK


### <a name="step-2"></a><span data-ttu-id="b35e6-131">Krok 2</span><span class="sxs-lookup"><span data-stu-id="b35e6-131">Step 2</span></span>

<span data-ttu-id="b35e6-132">Konfiguracja zestawu wewnętrznego modułu równoważenia obciążenia zachodzi podczas dodawania pierwszego punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="b35e6-132">You configure the internal load balancer set when you add the first endpoint.</span></span> <span data-ttu-id="b35e6-133">W tym kroku punkt końcowy, maszyna wirtualna i port sondy zostaną skojarzone z zestawem wewnętrznego modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="b35e6-133">You will associate the endpoint, virtual machine and probe port to the internal load balancer set in this step.</span></span>

```azurecli
azure vm endpoint create db1 1433 --local-port 1433 --protocol tcp --probe-port 1433 --probe-protocol tcp --probe-interval 300 --probe-timeout 600 --internal-load-balancer-name ilbset
```

### <a name="step-3"></a><span data-ttu-id="b35e6-134">Krok 3</span><span class="sxs-lookup"><span data-stu-id="b35e6-134">Step 3</span></span>

<span data-ttu-id="b35e6-135">Sprawdź konfigurację modułu równoważenia obciążenia za pomocą polecenia `azure vm show` *nazwa maszyny wirtualnej*</span><span class="sxs-lookup"><span data-stu-id="b35e6-135">Verify the load balancer configuration using `azure vm show` *virtual machine name*</span></span>

```azurecli
azure vm show DB1
```

<span data-ttu-id="b35e6-136">Dane wyjściowe to:</span><span class="sxs-lookup"><span data-stu-id="b35e6-136">The output will be:</span></span>

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

## <a name="create-a-remote-desktop-endpoint-for-a-virtual-machine"></a><span data-ttu-id="b35e6-137">Tworzenie punktu końcowego pulpitu zdalnego maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="b35e6-137">Create a remote desktop endpoint for a virtual machine</span></span>

<span data-ttu-id="b35e6-138">Możesz utworzyć punkt końcowy pulpitu zdalnego w celu przesyłania ruchu sieciowego z portu publicznego do lokalnego dla danej maszyny wirtualnej za pomocą polecenia `azure vm endpoint create`.</span><span class="sxs-lookup"><span data-stu-id="b35e6-138">You can create a remote desktop endpoint to forward network traffic from a public port to a local port for a specific virtual machine using `azure vm endpoint create`.</span></span>

```azurecli
azure vm endpoint create web1 54580 -k 3389
```

## <a name="remove-virtual-machine-from-load-balancer"></a><span data-ttu-id="b35e6-139">Usuwanie maszyny wirtualnej z modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="b35e6-139">Remove virtual machine from load balancer</span></span>

<span data-ttu-id="b35e6-140">Możesz usunąć maszynę wirtualną z zestawu wewnętrznego modułu równoważenia obciążenia przez usunięcie skojarzonego punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="b35e6-140">You can remove a virtual machine from an internal load balancer set by deleting the associated endpoint.</span></span> <span data-ttu-id="b35e6-141">Po usunięciu punktu końcowego maszyna wirtualna nie będzie należeć do zestawu modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="b35e6-141">Once the endpoint is removed, the virtual machine won't belong to the load balancer set anymore.</span></span>

<span data-ttu-id="b35e6-142">Korzystając z powyższego przykładu, możesz usunąć punkt końcowy utworzony dla maszyny wirtualnej „DB1” z wewnętrznego modułu równoważenia obciążenia „ilbset” za pomocą polecenia `azure vm endpoint delete`.</span><span class="sxs-lookup"><span data-stu-id="b35e6-142">Using the example above, you can remove the endpoint created for virtual machine "DB1" from internal load balancer "ilbset" by using the command `azure vm endpoint delete`.</span></span>

```azurecli
azure vm endpoint delete DB1 tcp-1433-1433
```

<span data-ttu-id="b35e6-143">Użyj polecenia `azure vm endpoint --help`, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="b35e6-143">Check out `azure vm endpoint --help` for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b35e6-144">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b35e6-144">Next steps</span></span>

<span data-ttu-id="b35e6-145">[Configure a load balancer distribution mode using source IP affinity](load-balancer-distribution-mode.md) (Konfigurowanie trybu dystrybucji modułu równoważenia obciążenia przy użyciu koligacji źródłowych adresów IP)</span><span class="sxs-lookup"><span data-stu-id="b35e6-145">[Configure a load balancer distribution mode using source IP affinity](load-balancer-distribution-mode.md)</span></span>

<span data-ttu-id="b35e6-146">[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md) (Konfigurowanie ustawień limitu czasu bezczynności protokołu TCP dla modułu równoważenia obciążenia)</span><span class="sxs-lookup"><span data-stu-id="b35e6-146">[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md)</span></span>
