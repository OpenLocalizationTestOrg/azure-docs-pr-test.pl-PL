---
title: "aaaAzure przykłady interfejsu wiersza polecenia | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 8001b7e72480cfd0122325f7fb81c32aaad072d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples-for-networking"></a><span data-ttu-id="c499e-103">Przykładów dla interfejsu wiersza polecenia platformy Azure do obsługi sieci</span><span class="sxs-lookup"><span data-stu-id="c499e-103">Azure CLI Samples for networking</span></span>

<span data-ttu-id="c499e-104">Witaj Poniższa tabela zawiera linki toobash skrypty utworzone przy użyciu interfejsu wiersza polecenia Azure hello.</span><span class="sxs-lookup"><span data-stu-id="c499e-104">hello following table includes links toobash scripts built using hello Azure CLI.</span></span>

| | |
|-|-|
|<span data-ttu-id="c499e-105">**Łączność między zasobami Azure**</span><span class="sxs-lookup"><span data-stu-id="c499e-105">**Connectivity between Azure resources**</span></span>||
| [<span data-ttu-id="c499e-106">Tworzenie sieci wirtualnej dla aplikacji wielowarstwowych</span><span class="sxs-lookup"><span data-stu-id="c499e-106">Create a virtual network for multi-tier applications</span></span>](./scripts/virtual-network-cli-sample-multi-tier-application.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="c499e-107">Tworzy sieć wirtualną z podsieci frontonu i zaplecza.</span><span class="sxs-lookup"><span data-stu-id="c499e-107">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="c499e-108">Podsieci frontonu toohello ruchu jest ograniczony tooHTTP i SSH, podczas toohello ruchu podsieci wewnętrznej jest ograniczona tooMySQL, port 3306.</span><span class="sxs-lookup"><span data-stu-id="c499e-108">Traffic toohello front-end subnet is limited tooHTTP and SSH, while traffic toohello back-end subnet is limited tooMySQL, port 3306.</span></span> |
| [<span data-ttu-id="c499e-109">Dwie wirtualne sieci równorzędne</span><span class="sxs-lookup"><span data-stu-id="c499e-109">Peer two virtual networks</span></span>](./scripts/virtual-network-cli-sample-peer-two-virtual-networks.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="c499e-110">Tworzy i łączy dwie sieci wirtualne w hello tego samego regionu.</span><span class="sxs-lookup"><span data-stu-id="c499e-110">Creates and connects two virtual networks in hello same region.</span></span> |
| [<span data-ttu-id="c499e-111">Kierować ruchem przez urządzenie wirtualne sieci</span><span class="sxs-lookup"><span data-stu-id="c499e-111">Route traffic through a network virtual appliance</span></span>](./scripts/virtual-network-cli-sample-route-traffic-through-nva.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="c499e-112">Tworzy sieć wirtualną z podsieci frontonu i zaplecza i maszynę Wirtualną, która jest możliwe tooroute ruch między podsieciami hello dwa.</span><span class="sxs-lookup"><span data-stu-id="c499e-112">Creates a virtual network with front-end and back-end subnets and a VM that is able tooroute traffic between hello two subnets.</span></span> |
| [<span data-ttu-id="c499e-113">Filtrowanie ruchu przychodzącego i wychodzącego ruchu sieciowego maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="c499e-113">Filter inbound and outbound VM network traffic</span></span>](./scripts/virtual-network-filter-network-traffic.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="c499e-114">Tworzy sieć wirtualną z podsieci frontonu i zaplecza.</span><span class="sxs-lookup"><span data-stu-id="c499e-114">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="c499e-115">Ruchu przychodzącego ruchu sieciowego podsieci frontonu toohello jest ograniczona tooHTTP, HTTPS i SSH.</span><span class="sxs-lookup"><span data-stu-id="c499e-115">Inbound network traffic toohello front-end subnet is limited tooHTTP, HTTPS and SSH.</span></span> <span data-ttu-id="c499e-116">Ruch wychodzący toohello Internet z podsieci wewnętrznej hello jest niedozwolone.</span><span class="sxs-lookup"><span data-stu-id="c499e-116">Outbound traffic toohello Internet from hello back-end subnet is not permitted.</span></span> |
|<span data-ttu-id="c499e-117">**Kierunek ruchu i równoważenia obciążenia**</span><span class="sxs-lookup"><span data-stu-id="c499e-117">**Load balancing and traffic direction**</span></span>||
| [<span data-ttu-id="c499e-118">Ładowanie równowagi ruchu tooVMs wysokiej dostępności</span><span class="sxs-lookup"><span data-stu-id="c499e-118">Load balance traffic tooVMs for high availability</span></span>](./scripts/load-balancer-linux-cli-sample-nlb.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="c499e-119">Tworzy kilka maszyny wirtualne o wysokiej dostępności i konfiguracji równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="c499e-119">Creates several virtual machines in a highly available and load balanced configuration.</span></span> |
| [<span data-ttu-id="c499e-120">Wiele witryn sieci Web na maszynach wirtualnych Równoważenie obciążenia</span><span class="sxs-lookup"><span data-stu-id="c499e-120">Load balance multiple websites on VMs</span></span>](./scripts/load-balancer-linux-cli-load-balance-multiple-websites-vm.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="c499e-121">Tworzy dwie maszyny wirtualne z wielu konfiguracji adresów IP, połączone tooan Azure zestawu dostępności, dostępny za pośrednictwem usługi równoważenia obciążenia Azure.</span><span class="sxs-lookup"><span data-stu-id="c499e-121">Creates two VMs with multiple IP configurations, joined tooan Azure Availability Set, accessible through an Azure Load Balancer.</span></span> |
| [<span data-ttu-id="c499e-122">Bezpośrednie ruchu w różnych regionach aplikacji wysokiej dostępności</span><span class="sxs-lookup"><span data-stu-id="c499e-122">Direct traffic across multiple regions for high application availability</span></span>](./scripts/traffic-manager-cli-websites-high-availability.md?toc=%2fazure%2fnetworking%2ftoc.json) |  <span data-ttu-id="c499e-123">Tworzy dwa planów usługi aplikacji, dwie aplikacje sieci web profilu Menedżera ruchu i dwa punkty końcowe Menedżera ruchu.</span><span class="sxs-lookup"><span data-stu-id="c499e-123">Creates two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> |
| | |
