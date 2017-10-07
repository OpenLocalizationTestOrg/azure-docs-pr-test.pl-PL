---
title: "aaaExample wskazówki infrastruktury platformy Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat hello klucza projekt i implementację wskazówki dotyczące wdrażania infrastruktury przykład na platformie Azure."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 281fc2c0-b533-45fa-81a3-728c0049c73d
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b6b307c0112203aa83e1fada81966fc265397a40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="example-azure-infrastructure-walkthrough-for-linux-vms"></a><span data-ttu-id="14762-103">Przykład wskazówki infrastruktury platformy Azure dla maszyn wirtualnych systemu Linux</span><span class="sxs-lookup"><span data-stu-id="14762-103">Example Azure infrastructure walkthrough for Linux VMs</span></span>

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

<span data-ttu-id="14762-104">W tym artykule przedstawiono zbudowaniu przykład infrastruktury aplikacji.</span><span class="sxs-lookup"><span data-stu-id="14762-104">This article walks through building out an example application infrastructure.</span></span> <span data-ttu-id="14762-105">Firma Microsoft szczegółowo projektowania infrastruktury dla prostego sklepu online, która gromadzi wszystkie hello wskazówki i decyzji dotyczących konwencji nazewnictwa, zestawów dostępności, sieci wirtualnych i usług równoważenia obciążenia i faktycznie wdrażania maszyn wirtualnych (VM).</span><span class="sxs-lookup"><span data-stu-id="14762-105">We detail designing an infrastructure for a simple on-line store that brings together all hello guidelines and decisions around naming conventions, availability sets, virtual networks and load balancers, and actually deploying your virtual machines (VMs).</span></span>

## <a name="example-workload"></a><span data-ttu-id="14762-106">Przykładowe obciążenie</span><span class="sxs-lookup"><span data-stu-id="14762-106">Example workload</span></span>
<span data-ttu-id="14762-107">Firma Adventure Works Cycles chce toobuild na platformie Azure, która składa się z aplikacji sklepu online:</span><span class="sxs-lookup"><span data-stu-id="14762-107">Adventure Works Cycles wants toobuild an on-line store application in Azure that consists of:</span></span>

* <span data-ttu-id="14762-108">Dwa serwery nginx z powitania klienta frontonu w warstwa sieci web</span><span class="sxs-lookup"><span data-stu-id="14762-108">Two nginx servers running hello client front-end in a web tier</span></span>
* <span data-ttu-id="14762-109">Dwa serwery nginx, przetwarzanie danych i zamówień w warstwie aplikacji</span><span class="sxs-lookup"><span data-stu-id="14762-109">Two nginx servers processing data and orders in an application tier</span></span>
* <span data-ttu-id="14762-110">Dwie bazy danych MongoDB serwerów częścią podzielonej klastra do przechowywania danych produktu i zamówień w warstwy bazy danych</span><span class="sxs-lookup"><span data-stu-id="14762-110">Two MongoDB servers part of a sharded cluster for storing product data and orders in a database tier</span></span>
* <span data-ttu-id="14762-111">Dwa kontrolery domeny usługi Active Directory dla konta klienta i dostawców w warstwie uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="14762-111">Two Active Directory domain controllers for customer accounts and suppliers in an authentication tier</span></span>
* <span data-ttu-id="14762-112">Wszystkie serwery hello znajdują się w dwóch podsieci:</span><span class="sxs-lookup"><span data-stu-id="14762-112">All hello servers are located in two subnets:</span></span>
  * <span data-ttu-id="14762-113">podsieci frontonu hello serwerów sieci web</span><span class="sxs-lookup"><span data-stu-id="14762-113">a front-end subnet for hello web servers</span></span> 
  * <span data-ttu-id="14762-114">podsieć wewnętrznych serwerów aplikacji hello, bazy danych MongoDB klastra i kontrolerów domeny</span><span class="sxs-lookup"><span data-stu-id="14762-114">a back-end subnet for hello application servers, MongoDB cluster, and domain controllers</span></span>

![Diagram różnych warstw dla infrastruktury aplikacji](./media/infrastructure-example/example-tiers.png)

<span data-ttu-id="14762-116">Bezpieczne przychodzącego ruchu w sieci web muszą być równoważeniem obciążenia między serwerami sieci web hello jak klienci Przeglądaj hello sklepu online.</span><span class="sxs-lookup"><span data-stu-id="14762-116">Incoming secure web traffic must be load-balanced among hello web servers as customers browse hello on-line store.</span></span> <span data-ttu-id="14762-117">Kolejność przetwarzania ruchu sieciowego w postaci hello HTTP żąda od hello sieci web, które serwery muszą być równoważeniem obciążenia między serwerami aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="14762-117">Order processing traffic in hello form of HTTP requests from hello web servers must be load-balanced among hello application servers.</span></span> <span data-ttu-id="14762-118">Ponadto należy zaprojektować hello infrastruktury wysokiej dostępności.</span><span class="sxs-lookup"><span data-stu-id="14762-118">Additionally, hello infrastructure must be designed for high availability.</span></span>

<span data-ttu-id="14762-119">Projekt wynikowy Hello musi uwzględniać:</span><span class="sxs-lookup"><span data-stu-id="14762-119">hello resulting design must incorporate:</span></span>

* <span data-ttu-id="14762-120">Subskrypcja platformy Azure i konta</span><span class="sxs-lookup"><span data-stu-id="14762-120">An Azure subscription and account</span></span>
* <span data-ttu-id="14762-121">Pojedyncza grupa zasobów</span><span class="sxs-lookup"><span data-stu-id="14762-121">A single resource group</span></span>
* <span data-ttu-id="14762-122">Azure Managed Disks</span><span class="sxs-lookup"><span data-stu-id="14762-122">Azure Managed Disks</span></span>
* <span data-ttu-id="14762-123">Sieć wirtualną z dwiema podsieciami</span><span class="sxs-lookup"><span data-stu-id="14762-123">A virtual network with two subnets</span></span>
* <span data-ttu-id="14762-124">Zestawy dostępności dla hello maszyn wirtualnych z podobną rolę</span><span class="sxs-lookup"><span data-stu-id="14762-124">Availability sets for hello VMs with a similar role</span></span>
* <span data-ttu-id="14762-125">Maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="14762-125">Virtual machines</span></span>

<span data-ttu-id="14762-126">Wszystkie powyższe hello wykonaj te konwencji nazewnictwa:</span><span class="sxs-lookup"><span data-stu-id="14762-126">All hello above follow these naming conventions:</span></span>

* <span data-ttu-id="14762-127">Adventure Works Cycles używa **[obciążenia IT]-[lokalizacja]-[zasobów platformy Azure]** jako prefiksu</span><span class="sxs-lookup"><span data-stu-id="14762-127">Adventure Works Cycles uses **[IT workload]-[location]-[Azure resource]** as a prefix</span></span>
  * <span data-ttu-id="14762-128">Na przykład "**azos**" (magazyn Azure On-line) jest hello imię i nazwisko obciążenia IT i "**użyj**" hello lokalizacji jest (wschodnie stany USA 2)</span><span class="sxs-lookup"><span data-stu-id="14762-128">For this example, "**azos**" (Azure On-line Store) is hello IT workload name and "**use**" (East US 2) is hello location</span></span>
* <span data-ttu-id="14762-129">W sieciach wirtualnych za pomocą AZOS-użycie-VN**[numer]**</span><span class="sxs-lookup"><span data-stu-id="14762-129">Virtual networks use AZOS-USE-VN**[number]**</span></span>
* <span data-ttu-id="14762-130">Zestawy dostępności używać azos-Użyj — jako-**[rola]**</span><span class="sxs-lookup"><span data-stu-id="14762-130">Availability sets use azos-use-as-**[role]**</span></span>
* <span data-ttu-id="14762-131">Nazwy maszyn wirtualnych użyć azos-Użyj-vm -**[vmname]**</span><span class="sxs-lookup"><span data-stu-id="14762-131">Virtual machine names use azos-use-vm-**[vmname]**</span></span>

## <a name="azure-subscriptions-and-accounts"></a><span data-ttu-id="14762-132">Subskrypcje platformy Azure i konta</span><span class="sxs-lookup"><span data-stu-id="14762-132">Azure subscriptions and accounts</span></span>
<span data-ttu-id="14762-133">Adventure Works Cycles korzysta z ich subskrypcją przedsiębiorstwa, o nazwie Adventure Works Enterprise subskrypcji, rozliczeń dla tej obciążenia IT tooprovide.</span><span class="sxs-lookup"><span data-stu-id="14762-133">Adventure Works Cycles is using their Enterprise subscription, named Adventure Works Enterprise Subscription, tooprovide billing for this IT workload.</span></span>

## <a name="storage"></a><span data-ttu-id="14762-134">Magazyn</span><span class="sxs-lookup"><span data-stu-id="14762-134">Storage</span></span>
<span data-ttu-id="14762-135">Firma Adventure Works Cycles ustalić, czy powinny używać dysków zarządzanych Azure.</span><span class="sxs-lookup"><span data-stu-id="14762-135">Adventure Works Cycles determined that they should use Azure Managed Disks.</span></span> <span data-ttu-id="14762-136">Podczas tworzenia maszyn wirtualnych, są używane zarówno warstw magazynowania dostępne magazynu:</span><span class="sxs-lookup"><span data-stu-id="14762-136">When creating VMs, both storage available storage tiers are used:</span></span>

* <span data-ttu-id="14762-137">**Magazynu w warstwie standardowa** hello serwerów sieci web, serwerów aplikacji i kontrolerów domeny i dysków z danymi.</span><span class="sxs-lookup"><span data-stu-id="14762-137">**Standard storage** for hello web servers, application servers, and domain controllers and their data disks.</span></span>
* <span data-ttu-id="14762-138">**Magazyn w warstwie Premium** hello bazy danych MongoDB podzielonej klastra serwerów i dysków z danymi.</span><span class="sxs-lookup"><span data-stu-id="14762-138">**Premium storage** for hello MongoDB sharded cluster servers and their data disks.</span></span>

## <a name="virtual-network-and-subnets"></a><span data-ttu-id="14762-139">Sieć wirtualna i podsieci</span><span class="sxs-lookup"><span data-stu-id="14762-139">Virtual network and subnets</span></span>
<span data-ttu-id="14762-140">Ponieważ hello sieci wirtualnej sieci lokalnej cykle pracy Adventure toohello bieżące połączenie nie jest konieczne, zdecydowano, że w sieci wirtualnej tylko w chmurze.</span><span class="sxs-lookup"><span data-stu-id="14762-140">Because hello virtual network does not need ongoing connectivity toohello Adventure Work Cycles on-premises network, they decided on a cloud-only virtual network.</span></span>

<span data-ttu-id="14762-141">One tworzone tylko na chmurze sieci wirtualnej z następującego ustawienia za pomocą portalu Azure hello hello:</span><span class="sxs-lookup"><span data-stu-id="14762-141">They created a cloud-only virtual network with hello following settings using hello Azure portal:</span></span>

* <span data-ttu-id="14762-142">Nazwa: AZOS-użycie VN01</span><span class="sxs-lookup"><span data-stu-id="14762-142">Name: AZOS-USE-VN01</span></span>
* <span data-ttu-id="14762-143">Lokalizacji: Wschodnie stany USA 2</span><span class="sxs-lookup"><span data-stu-id="14762-143">Location: East US 2</span></span>
* <span data-ttu-id="14762-144">Przestrzeń adresową sieci wirtualnej: 10.0.0.0/8</span><span class="sxs-lookup"><span data-stu-id="14762-144">Virtual network address space: 10.0.0.0/8</span></span>
* <span data-ttu-id="14762-145">Pierwszej podsieci:</span><span class="sxs-lookup"><span data-stu-id="14762-145">First subnet:</span></span>
  * <span data-ttu-id="14762-146">Nazwa: frontonu</span><span class="sxs-lookup"><span data-stu-id="14762-146">Name: FrontEnd</span></span>
  * <span data-ttu-id="14762-147">Przestrzeń adresowa: 10.0.1.0/24</span><span class="sxs-lookup"><span data-stu-id="14762-147">Address space: 10.0.1.0/24</span></span>
* <span data-ttu-id="14762-148">Drugi podsieci:</span><span class="sxs-lookup"><span data-stu-id="14762-148">Second subnet:</span></span>
  * <span data-ttu-id="14762-149">Nazwa: wewnętrznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="14762-149">Name: BackEnd</span></span>
  * <span data-ttu-id="14762-150">Przestrzeń adresowa: 10.0.2.0/24</span><span class="sxs-lookup"><span data-stu-id="14762-150">Address space: 10.0.2.0/24</span></span>

## <a name="availability-sets"></a><span data-ttu-id="14762-151">Zestawy dostępności</span><span class="sxs-lookup"><span data-stu-id="14762-151">Availability sets</span></span>
<span data-ttu-id="14762-152">Wysoka dostępność toomaintain wszystkie cztery warstwy ich magazynu online, firma Adventure Works Cycles na cztery zestawy dostępności:</span><span class="sxs-lookup"><span data-stu-id="14762-152">toomaintain high availability of all four tiers of their on-line store, Adventure Works Cycles decided on four availability sets:</span></span>

* <span data-ttu-id="14762-153">**azos używany jako web** hello serwerów sieci web</span><span class="sxs-lookup"><span data-stu-id="14762-153">**azos-use-as-web** for hello web servers</span></span>
* <span data-ttu-id="14762-154">**azos używany jako aplikacji** dla serwerów aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="14762-154">**azos-use-as-app** for hello application servers</span></span>
* <span data-ttu-id="14762-155">**azos używany jako db** hello serwerów w klastrze podzielonej hello bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="14762-155">**azos-use-as-db** for hello servers in hello MongoDB sharded cluster</span></span>
* <span data-ttu-id="14762-156">**azos używany jako dc** hello kontrolerów domeny</span><span class="sxs-lookup"><span data-stu-id="14762-156">**azos-use-as-dc** for hello domain controllers</span></span>

## <a name="virtual-machines"></a><span data-ttu-id="14762-157">Maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="14762-157">Virtual machines</span></span>
<span data-ttu-id="14762-158">Firma Adventure Works Cycles na powitania po nazw dla swoich maszynach wirtualnych platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="14762-158">Adventure Works Cycles decided on hello following names for their Azure VMs:</span></span>

* <span data-ttu-id="14762-159">**azos użycie vm-web01** dla hello na pierwszym serwerze sieci web</span><span class="sxs-lookup"><span data-stu-id="14762-159">**azos-use-vm-web01** for hello first web server</span></span>
* <span data-ttu-id="14762-160">**azos użycie vm-web02** hello drugiego serwera sieci web</span><span class="sxs-lookup"><span data-stu-id="14762-160">**azos-use-vm-web02** for hello second web server</span></span>
* <span data-ttu-id="14762-161">**azos użycie vm-app01** dla pierwszego serwera aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="14762-161">**azos-use-vm-app01** for hello first application server</span></span>
* <span data-ttu-id="14762-162">**azos użycie vm-app02** dla drugiego serwera aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="14762-162">**azos-use-vm-app02** for hello second application server</span></span>
* <span data-ttu-id="14762-163">**azos użycie vm-db01** dla pierwszego serwera bazy danych MongoDB hello hello klastra</span><span class="sxs-lookup"><span data-stu-id="14762-163">**azos-use-vm-db01** for hello first MongoDB server in hello cluster</span></span>
* <span data-ttu-id="14762-164">**azos użycie vm-db02** hello drugiego serwera bazy danych MongoDB w klastrze hello</span><span class="sxs-lookup"><span data-stu-id="14762-164">**azos-use-vm-db02** for hello second MongoDB server in hello cluster</span></span>
* <span data-ttu-id="14762-165">**azos użycie vm-dc01** dla hello pierwszego kontrolera domeny</span><span class="sxs-lookup"><span data-stu-id="14762-165">**azos-use-vm-dc01** for hello first domain controller</span></span>
* <span data-ttu-id="14762-166">**azos użycie vm-dc02** dla hello kontrolera domeny</span><span class="sxs-lookup"><span data-stu-id="14762-166">**azos-use-vm-dc02** for hello second domain controller</span></span>

<span data-ttu-id="14762-167">Oto hello Wynikowa konfiguracja.</span><span class="sxs-lookup"><span data-stu-id="14762-167">Here is hello resulting configuration.</span></span>

![Infrastruktura aplikacji końcowego wdrożona na platformie Azure](./media/infrastructure-example/example-config.png)

<span data-ttu-id="14762-169">Ta konfiguracja obejmuje:</span><span class="sxs-lookup"><span data-stu-id="14762-169">This configuration incorporates:</span></span>

* <span data-ttu-id="14762-170">Tylko w chmurze sieci wirtualnej z dwoma podsieciami (frontonu i wewnętrznej bazy danych)</span><span class="sxs-lookup"><span data-stu-id="14762-170">A cloud-only virtual network with two subnets (FrontEnd and BackEnd)</span></span>
* <span data-ttu-id="14762-171">Dyskach platformy Azure zarządzanych za pomocą dysków w wersjach Standard i Premium</span><span class="sxs-lookup"><span data-stu-id="14762-171">Azure Managed Disks using both Standard and Premium disks</span></span>
* <span data-ttu-id="14762-172">Cztery zestawy dostępności, jeden dla każdej warstwy hello sklep online</span><span class="sxs-lookup"><span data-stu-id="14762-172">Four availability sets, one for each tier of hello on-line store</span></span>
* <span data-ttu-id="14762-173">maszyny wirtualne Hello hello czterech warstw</span><span class="sxs-lookup"><span data-stu-id="14762-173">hello virtual machines for hello four tiers</span></span>
* <span data-ttu-id="14762-174">Zestaw o zrównoważonym obciążeniu zewnętrznych dla ruchu web oparty na protokole HTTPS z serwerów sieci web toohello internetowych hello</span><span class="sxs-lookup"><span data-stu-id="14762-174">An external load balanced set for HTTPS-based web traffic from hello Internet toohello web servers</span></span>
* <span data-ttu-id="14762-175">Zestaw dla ruchu w sieci web niezaszyfrowane z serwerów aplikacji toohello serwerów sieci web hello o zrównoważonym obciążeniu wewnętrzny</span><span class="sxs-lookup"><span data-stu-id="14762-175">An internal load balanced set for unencrypted web traffic from hello web servers toohello application servers</span></span>
* <span data-ttu-id="14762-176">Pojedyncza grupa zasobów</span><span class="sxs-lookup"><span data-stu-id="14762-176">A single resource group</span></span>
