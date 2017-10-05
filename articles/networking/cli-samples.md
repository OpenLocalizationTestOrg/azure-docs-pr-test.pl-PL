---
title: "Przykłady Azure CLI | Dokumentacja firmy Microsoft"
description: "Przykłady Azure CLI"
services: virtual-network
documentationcenter: virtual-network
author: KumudD
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 04/25/2017
ms.author: kumud
ms.openlocfilehash: 7977460f61bfdabd399e45e86d9bbf2e5083992b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cli-samples-for-networking"></a><span data-ttu-id="d4624-103">Przykładów dla interfejsu wiersza polecenia platformy Azure do obsługi sieci</span><span class="sxs-lookup"><span data-stu-id="d4624-103">Azure CLI Samples for networking</span></span>

<span data-ttu-id="d4624-104">Poniższa tabela zawiera linki do bash skrypty utworzone przy użyciu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d4624-104">The following table includes links to bash scripts built using the Azure CLI.</span></span>

| | |
|-|-|
|<span data-ttu-id="d4624-105">**Łączność między zasobami Azure**</span><span class="sxs-lookup"><span data-stu-id="d4624-105">**Connectivity between Azure resources**</span></span>||
| [<span data-ttu-id="d4624-106">Tworzenie sieci wirtualnej dla aplikacji wielowarstwowych</span><span class="sxs-lookup"><span data-stu-id="d4624-106">Create a virtual network for multi-tier applications</span></span>](./scripts/virtual-network-cli-sample-multi-tier-application.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="d4624-107">Tworzy sieć wirtualną z podsieci frontonu i zaplecza.</span><span class="sxs-lookup"><span data-stu-id="d4624-107">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="d4624-108">Ruch do podsieci frontonu jest ograniczona do HTTP i SSH, gdy ruch do podsieci wewnętrznej jest ograniczony do MySQL, port 3306.</span><span class="sxs-lookup"><span data-stu-id="d4624-108">Traffic to the front-end subnet is limited to HTTP and SSH, while traffic to the back-end subnet is limited to MySQL, port 3306.</span></span> |
| [<span data-ttu-id="d4624-109">Dwie wirtualne sieci równorzędne</span><span class="sxs-lookup"><span data-stu-id="d4624-109">Peer two virtual networks</span></span>](./scripts/virtual-network-cli-sample-peer-two-virtual-networks.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="d4624-110">Tworzy i łączy dwie sieci wirtualne w tym samym regionie.</span><span class="sxs-lookup"><span data-stu-id="d4624-110">Creates and connects two virtual networks in the same region.</span></span> |
| [<span data-ttu-id="d4624-111">Kierować ruchem przez urządzenie wirtualne sieci</span><span class="sxs-lookup"><span data-stu-id="d4624-111">Route traffic through a network virtual appliance</span></span>](./scripts/virtual-network-cli-sample-route-traffic-through-nva.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="d4624-112">Tworzy sieć wirtualną z podsieci frontonu i zaplecza i maszynę Wirtualną, która może kierować ruchem między dwiema podsieciami.</span><span class="sxs-lookup"><span data-stu-id="d4624-112">Creates a virtual network with front-end and back-end subnets and a VM that is able to route traffic between the two subnets.</span></span> |
| [<span data-ttu-id="d4624-113">Filtrowanie ruchu przychodzącego i wychodzącego ruchu sieciowego maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="d4624-113">Filter inbound and outbound VM network traffic</span></span>](./scripts/virtual-network-filter-network-traffic.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="d4624-114">Tworzy sieć wirtualną z podsieci frontonu i zaplecza.</span><span class="sxs-lookup"><span data-stu-id="d4624-114">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="d4624-115">Ruch sieciowy przychodzący do podsieci frontonu jest ograniczone do protokołu HTTP, HTTPS i SSH.</span><span class="sxs-lookup"><span data-stu-id="d4624-115">Inbound network traffic to the front-end subnet is limited to HTTP, HTTPS and SSH.</span></span> <span data-ttu-id="d4624-116">Ruch wychodzący do Internetu z podsieci wewnętrznej jest niedozwolone.</span><span class="sxs-lookup"><span data-stu-id="d4624-116">Outbound traffic to the Internet from the back-end subnet is not permitted.</span></span> |
|<span data-ttu-id="d4624-117">**Kierunek ruchu i równoważenia obciążenia**</span><span class="sxs-lookup"><span data-stu-id="d4624-117">**Load balancing and traffic direction**</span></span>||
| [<span data-ttu-id="d4624-118">Ruch równoważenia obciążenia do maszyn wirtualnych wysokiej dostępności</span><span class="sxs-lookup"><span data-stu-id="d4624-118">Load balance traffic to VMs for high availability</span></span>](./scripts/load-balancer-linux-cli-sample-nlb.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="d4624-119">Tworzy kilka maszyny wirtualne o wysokiej dostępności i konfiguracji równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="d4624-119">Creates several virtual machines in a highly available and load balanced configuration.</span></span> |
| [<span data-ttu-id="d4624-120">Wiele witryn sieci Web na maszynach wirtualnych Równoważenie obciążenia</span><span class="sxs-lookup"><span data-stu-id="d4624-120">Load balance multiple websites on VMs</span></span>](./scripts/load-balancer-linux-cli-load-balance-multiple-websites-vm.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="d4624-121">Tworzy dwie maszyny wirtualne z wielu konfiguracji adresów IP, dołączony do platformy Azure zestawu dostępności, dostępny za pośrednictwem usługi równoważenia obciążenia Azure.</span><span class="sxs-lookup"><span data-stu-id="d4624-121">Creates two VMs with multiple IP configurations, joined to an Azure Availability Set, accessible through an Azure Load Balancer.</span></span> |
| [<span data-ttu-id="d4624-122">Bezpośrednie ruchu w różnych regionach aplikacji wysokiej dostępności</span><span class="sxs-lookup"><span data-stu-id="d4624-122">Direct traffic across multiple regions for high application availability</span></span>](./scripts/traffic-manager-cli-websites-high-availability.md?toc=%2fazure%2fnetworking%2ftoc.json) |  <span data-ttu-id="d4624-123">Tworzy dwa planów usługi aplikacji, dwie aplikacje sieci web profilu Menedżera ruchu i dwa punkty końcowe Menedżera ruchu.</span><span class="sxs-lookup"><span data-stu-id="d4624-123">Creates two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> |
| | |
