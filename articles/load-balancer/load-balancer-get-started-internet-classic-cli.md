---
title: "aaaCreate internetowy załadować równoważenia - klasycznego wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate Internet równoważenia obciążenia przy użyciu modelu wdrażania klasycznego hello wiersza polecenia platformy Azure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: e433a824-4a8a-44d2-8765-a74f52d4e584
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: e6070cbc574f74bca0cccb960ff192847d6511bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-hello-azure-cli"></a><span data-ttu-id="a423f-103">Rozpocząć tworzenie internetowy modułu równoważenia obciążenia (klasyczne) w hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a423f-103">Get started creating an Internet facing load balancer (classic) in hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a423f-104">Klasyczna witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a423f-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="a423f-105">Program PowerShell</span><span class="sxs-lookup"><span data-stu-id="a423f-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="a423f-106">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a423f-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="a423f-107">Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="a423f-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="a423f-108">Przed rozpoczęciem pracy z zasobów platformy Azure, jest ważne toounderstand, że Azure ma obecnie dwa modele wdrażania: usługi Azure Resource Manager i model klasyczny.</span><span class="sxs-lookup"><span data-stu-id="a423f-108">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="a423f-109">Przed rozpoczęciem pracy z dowolnym zasobem Azure należy zapoznać się z [modelami i narzędziami wdrażania](../azure-classic-rm.md).</span><span class="sxs-lookup"><span data-stu-id="a423f-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="a423f-110">Hello dokumentację dotyczącą różnych narzędzi można wyświetlić, klikając karty hello u góry hello tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="a423f-110">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span> <span data-ttu-id="a423f-111">W tym artykule omówiono hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="a423f-111">This article covers hello classic deployment model.</span></span> <span data-ttu-id="a423f-112">Możesz również [Dowiedz się, jak usługa równoważenia przy użyciu usługi Azure Resource Manager obciążenia toocreate Internetem](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="a423f-112">You can also [Learn how toocreate an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="step-by-step-creating-an-internet-facing-load-balancer-using-cli"></a><span data-ttu-id="a423f-113">Szczegółowy opis tworzenia modułu równoważenia obciążenia dostępnego z Internetu przy użyciu interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="a423f-113">Step by step creating an Internet facing load balancer using CLI</span></span>

<span data-ttu-id="a423f-114">W tym przewodniku pokazuje, jak toocreate Internet równoważenia obciążenia na powitania scenariusz powyżej.</span><span class="sxs-lookup"><span data-stu-id="a423f-114">This guide shows how toocreate an Internet load balancer based on hello scenario above.</span></span>

1. <span data-ttu-id="a423f-115">Jeśli po raz pierwszy używasz interfejsu wiersza polecenia Azure, zobacz [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](../cli-install-nodejs.md) i wykonaj instrukcje hello zapasowej punktu toohello, gdzie należy wybrać konto platformy Azure i subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="a423f-115">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="a423f-116">Uruchom hello **trybie azure config** polecenia tooswitch tooclassic tryb, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="a423f-116">Run hello **azure config mode** command tooswitch tooclassic mode, as shown below.</span></span>

    ```azurecli
    azure config mode asm
    ```

    <span data-ttu-id="a423f-117">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="a423f-117">Expected output:</span></span>

        info:    New mode is asm

## <a name="create-endpoint-and-load-balancer-set"></a><span data-ttu-id="a423f-118">Tworzenie punktu końcowego i zestawu modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="a423f-118">Create endpoint and load balancer set</span></span>

<span data-ttu-id="a423f-119">Utworzono "sieci Web 2" i Hello scenariusz zakłada hello maszyn wirtualnych "sieci Web 1".</span><span class="sxs-lookup"><span data-stu-id="a423f-119">hello scenario assumes hello virtual machines "web1" and "web2" were created.</span></span>
<span data-ttu-id="a423f-120">W tym przewodniku opisano sposób tworzenia modułu równoważenia obciążenia przy użyciu portu 80 jako portu publicznego i lokalnego.</span><span class="sxs-lookup"><span data-stu-id="a423f-120">This guide will create a load balancer set using port 80 as public port and port 80 as local port.</span></span> <span data-ttu-id="a423f-121">Port sondy jest również konfigurowany na porcie 80, a moduł równoważenia obciążenia o nazwie hello ustawić "lbset".</span><span class="sxs-lookup"><span data-stu-id="a423f-121">A probe port is also configured on port 80 and named hello load balancer set "lbset".</span></span>

### <a name="step-1"></a><span data-ttu-id="a423f-122">Krok 1</span><span class="sxs-lookup"><span data-stu-id="a423f-122">Step 1</span></span>

<span data-ttu-id="a423f-123">Tworzenie pierwszego punktu końcowego hello i ustawić za pomocą modułu równoważenia obciążenia `azure network vm endpoint create` dla maszyny wirtualnej "sieci Web 1".</span><span class="sxs-lookup"><span data-stu-id="a423f-123">Create hello first endpoint and load balancer set using `azure network vm endpoint create` for virtual machine "web1".</span></span>

```azurecli
azure vm endpoint create web1 80 --local-port 80 --protocol tcp --probe-port 80 --load-balanced-set-name lbset
```

## <a name="step-2"></a><span data-ttu-id="a423f-124">Krok 2</span><span class="sxs-lookup"><span data-stu-id="a423f-124">Step 2</span></span>

<span data-ttu-id="a423f-125">Dodaj drugi zestaw usługi równoważenia obciążenia toohello maszyny wirtualnej "sieci Web 2".</span><span class="sxs-lookup"><span data-stu-id="a423f-125">Add a second virtual machine "web2" toohello load balancer set.</span></span>

```azurecli
azure vm endpoint create web2 80 --local-port 80 --protocol tcp --probe-port 80 --load-balanced-set-name lbset
```

## <a name="step-3"></a><span data-ttu-id="a423f-126">Krok 3</span><span class="sxs-lookup"><span data-stu-id="a423f-126">Step 3</span></span>

<span data-ttu-id="a423f-127">Sprawdzić z konfiguracji usługi równoważenia obciążenia hello `azure vm show` .</span><span class="sxs-lookup"><span data-stu-id="a423f-127">Verify hello load balancer configuration using `azure vm show` .</span></span>

```azurecli
azure vm show web1
```

<span data-ttu-id="a423f-128">Witaj dane wyjściowe będą mieć:</span><span class="sxs-lookup"><span data-stu-id="a423f-128">hello output will be:</span></span>

    data:    DNSName "contoso.cloudapp.net"
    data:    Location "East US"
    data:    VMName "web1"
    data:    IPAddress "10.0.0.5"
    data:    InstanceStatus "ReadyRole"
    data:    InstanceSize "Standard_D1"
    data:    Image "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-2015
    6-en.us-127GB.vhd"
    data:    OSDisk hostCaching "ReadWrite"
    data:    OSDisk name "joaoma-1-web1-0-201509251804250879"
    data:    OSDisk mediaLink "https://XXXXXXXXXXXXXXX.blob.core.windows.
    /vhds/joaomatest-web1-2015-09-25.vhd"
    data:    OSDisk sourceImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Se
    r-2012-R2-20150916-en.us-127GB.vhd"
    data:    OSDisk operatingSystem "Windows"
    data:    OSDisk iOType "Standard"
    data:    ReservedIPName ""
    data:    VirtualIPAddresses 0 address "XXXXXXXXXXXXXXXX"
    data:    VirtualIPAddresses 0 name "XXXXXXXXXXXXXXXXXXXX"
    data:    VirtualIPAddresses 0 isDnsProgrammed true
    data:    Network Endpoints 0 loadBalancedEndpointSetName "lbset"
    data:    Network Endpoints 0 localPort 80
    data:    Network Endpoints 0 name "tcp-80-80"
    data:    Network Endpoints 0 port 80
    data:    Network Endpoints 0 loadBalancerProbe port 80
    data:    Network Endpoints 0 loadBalancerProbe protocol "tcp"
    data:    Network Endpoints 0 loadBalancerProbe intervalInSeconds 15
    data:    Network Endpoints 0 loadBalancerProbe timeoutInSeconds 31
    data:    Network Endpoints 0 protocol "tcp"
    data:    Network Endpoints 0 virtualIPAddress "XXXXXXXXXXXX"
    data:    Network Endpoints 0 enableDirectServerReturn false
    data:    Network Endpoints 1 localPort 5986
    data:    Network Endpoints 1 name "PowerShell"
    data:    Network Endpoints 1 port 5986
    data:    Network Endpoints 1 protocol "tcp"
    data:    Network Endpoints 1 virtualIPAddress "XXXXXXXXXXXX"
    data:    Network Endpoints 1 enableDirectServerReturn false
    data:    Network Endpoints 2 localPort 3389
    data:    Network Endpoints 2 name "Remote Desktop"
    data:    Network Endpoints 2 port 58081
    info:    vm show command OK

## <a name="create-a-remote-desktop-endpoint-for-a-virtual-machine"></a><span data-ttu-id="a423f-129">Tworzenie punktu końcowego pulpitu zdalnego maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="a423f-129">Create a remote desktop endpoint for a virtual machine</span></span>

<span data-ttu-id="a423f-130">Ruch sieciowy tooforward zdalny punkt końcowy pulpitu można utworzyć na podstawie port publiczny port lokalny tooa dla określonej maszyny wirtualnej przy użyciu `azure vm endpoint create`.</span><span class="sxs-lookup"><span data-stu-id="a423f-130">You can create a remote desktop endpoint tooforward network traffic from a public port tooa local port for a specific virtual machine using `azure vm endpoint create`.</span></span>

```azurecli
azure vm endpoint create web1 54580 -k 3389
```

## <a name="remove-virtual-machine-from-load-balancer"></a><span data-ttu-id="a423f-131">Usuwanie maszyny wirtualnej z modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="a423f-131">Remove virtual machine from load balancer</span></span>

<span data-ttu-id="a423f-132">Masz toohello punkt końcowym skojarzony hello toodelete załadować zestawu modułu równoważenia z hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a423f-132">You have toodelete hello endpoint associated toohello load balancer set from hello virtual machine.</span></span> <span data-ttu-id="a423f-133">Po usunięciu punktu końcowego hello hello maszyny wirtualnej nie należy już zestaw modułów równoważenia obciążenia toohello.</span><span class="sxs-lookup"><span data-stu-id="a423f-133">Once hello endpoint is removed, hello virtual machine doesn't belong toohello load balancer set anymore.</span></span>

<span data-ttu-id="a423f-134">Za pomocą powyższego przykładu hello, można usunąć punktu końcowego hello utworzone dla maszyny wirtualnej "sieci Web 1" z modułu równoważenia obciążenia "lbset" za pomocą polecenia hello `azure vm endpoint delete`.</span><span class="sxs-lookup"><span data-stu-id="a423f-134">Using hello example above, you can remove hello endpoint created for virtual machine "web1" from load balancer "lbset" using hello command `azure vm endpoint delete`.</span></span>

```azurecli
azure vm endpoint delete web1 tcp-80-80
```

> [!NOTE]
> <span data-ttu-id="a423f-135">Można eksplorować więcej opcji toomanage punktów końcowych przy użyciu polecenia hello`azure vm endpoint --help`</span><span class="sxs-lookup"><span data-stu-id="a423f-135">You can explore more options toomanage endpoints using hello command `azure vm endpoint --help`</span></span>

## <a name="next-steps"></a><span data-ttu-id="a423f-136">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a423f-136">Next steps</span></span>

<span data-ttu-id="a423f-137">[Get started configuring an internal load balancer](load-balancer-get-started-ilb-arm-ps.md) (Wprowadzenie do konfigurowania wewnętrznego modułu równoważenia obciążenia)</span><span class="sxs-lookup"><span data-stu-id="a423f-137">[Get started configuring an internal load balancer](load-balancer-get-started-ilb-arm-ps.md)</span></span>

<span data-ttu-id="a423f-138">[Configure a load balancer distribution mode](load-balancer-distribution-mode.md) (Konfigurowanie trybu dystrybucji modułu równoważenia obciążenia)</span><span class="sxs-lookup"><span data-stu-id="a423f-138">[Configure a load balancer distribution mode](load-balancer-distribution-mode.md)</span></span>

<span data-ttu-id="a423f-139">[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md) (Konfigurowanie ustawień limitu czasu bezczynności protokołu TCP dla modułu równoważenia obciążenia)</span><span class="sxs-lookup"><span data-stu-id="a423f-139">[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md)</span></span>
