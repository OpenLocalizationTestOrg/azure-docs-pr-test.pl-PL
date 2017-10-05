---
title: "Przykład infrastruktury platformy Azure wskazówki | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat klucza projekt i implementację wskazówki dotyczące wdrażania infrastruktury przykład na platformie Azure."
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
ms.openlocfilehash: b18be0d81d6fad7328edb47c9b69af4eecd3b971
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="example-azure-infrastructure-walkthrough-for-linux-vms"></a><span data-ttu-id="5c867-103">Przykład wskazówki infrastruktury platformy Azure dla maszyn wirtualnych systemu Linux</span><span class="sxs-lookup"><span data-stu-id="5c867-103">Example Azure infrastructure walkthrough for Linux VMs</span></span>

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

<span data-ttu-id="5c867-104">W tym artykule przedstawiono zbudowaniu przykład infrastruktury aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5c867-104">This article walks through building out an example application infrastructure.</span></span> <span data-ttu-id="5c867-105">Firma Microsoft szczegółowo projektowania infrastruktury dla prostego sklepu online, która gromadzi wszystkie wskazówki i decyzji dotyczących konwencji nazewnictwa, zestawów dostępności, sieci wirtualnych i usług równoważenia obciążenia i faktycznie wdrażania maszyn wirtualnych (VM).</span><span class="sxs-lookup"><span data-stu-id="5c867-105">We detail designing an infrastructure for a simple on-line store that brings together all the guidelines and decisions around naming conventions, availability sets, virtual networks and load balancers, and actually deploying your virtual machines (VMs).</span></span>

## <a name="example-workload"></a><span data-ttu-id="5c867-106">Przykładowe obciążenie</span><span class="sxs-lookup"><span data-stu-id="5c867-106">Example workload</span></span>
<span data-ttu-id="5c867-107">Firma Adventure Works Cycles chce utworzyć aplikację sklep online na platformie Azure, która składa się z:</span><span class="sxs-lookup"><span data-stu-id="5c867-107">Adventure Works Cycles wants to build an on-line store application in Azure that consists of:</span></span>

* <span data-ttu-id="5c867-108">Dwa serwery nginx z frontonu w warstwa sieci web klienta</span><span class="sxs-lookup"><span data-stu-id="5c867-108">Two nginx servers running the client front-end in a web tier</span></span>
* <span data-ttu-id="5c867-109">Dwa serwery nginx, przetwarzanie danych i zamówień w warstwie aplikacji</span><span class="sxs-lookup"><span data-stu-id="5c867-109">Two nginx servers processing data and orders in an application tier</span></span>
* <span data-ttu-id="5c867-110">Dwie bazy danych MongoDB serwerów częścią podzielonej klastra do przechowywania danych produktu i zamówień w warstwy bazy danych</span><span class="sxs-lookup"><span data-stu-id="5c867-110">Two MongoDB servers part of a sharded cluster for storing product data and orders in a database tier</span></span>
* <span data-ttu-id="5c867-111">Dwa kontrolery domeny usługi Active Directory dla konta klienta i dostawców w warstwie uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="5c867-111">Two Active Directory domain controllers for customer accounts and suppliers in an authentication tier</span></span>
* <span data-ttu-id="5c867-112">Wszystkie serwery znajdują się w dwóch podsieci:</span><span class="sxs-lookup"><span data-stu-id="5c867-112">All the servers are located in two subnets:</span></span>
  * <span data-ttu-id="5c867-113">frontonu podsieci dla serwerów sieci web</span><span class="sxs-lookup"><span data-stu-id="5c867-113">a front-end subnet for the web servers</span></span> 
  * <span data-ttu-id="5c867-114">podsieć wewnętrznych serwerów aplikacji, bazy danych MongoDB klastra i kontrolerów domeny</span><span class="sxs-lookup"><span data-stu-id="5c867-114">a back-end subnet for the application servers, MongoDB cluster, and domain controllers</span></span>

![Diagram różnych warstw dla infrastruktury aplikacji](./media/infrastructure-example/example-tiers.png)

<span data-ttu-id="5c867-116">Bezpieczne przychodzącego ruchu w sieci web musi być równoważeniem obciążenia między serwerami sieci web jako klienci Przeglądaj sklepu online.</span><span class="sxs-lookup"><span data-stu-id="5c867-116">Incoming secure web traffic must be load-balanced among the web servers as customers browse the on-line store.</span></span> <span data-ttu-id="5c867-117">Kolejność przetwarzania ruchu sieciowego w postaci HTTP żąda od serwerów musi być równoważeniem obciążenia między serwerami aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="5c867-117">Order processing traffic in the form of HTTP requests from the web servers must be load-balanced among the application servers.</span></span> <span data-ttu-id="5c867-118">Ponadto należy zaprojektować infrastruktury wysokiej dostępności.</span><span class="sxs-lookup"><span data-stu-id="5c867-118">Additionally, the infrastructure must be designed for high availability.</span></span>

<span data-ttu-id="5c867-119">Projekt wynikowy musi uwzględniać:</span><span class="sxs-lookup"><span data-stu-id="5c867-119">The resulting design must incorporate:</span></span>

* <span data-ttu-id="5c867-120">Subskrypcja platformy Azure i konta</span><span class="sxs-lookup"><span data-stu-id="5c867-120">An Azure subscription and account</span></span>
* <span data-ttu-id="5c867-121">Pojedyncza grupa zasobów</span><span class="sxs-lookup"><span data-stu-id="5c867-121">A single resource group</span></span>
* <span data-ttu-id="5c867-122">Azure Managed Disks</span><span class="sxs-lookup"><span data-stu-id="5c867-122">Azure Managed Disks</span></span>
* <span data-ttu-id="5c867-123">Sieć wirtualną z dwiema podsieciami</span><span class="sxs-lookup"><span data-stu-id="5c867-123">A virtual network with two subnets</span></span>
* <span data-ttu-id="5c867-124">Zestawy dostępności dla maszyn wirtualnych o podobną rolę</span><span class="sxs-lookup"><span data-stu-id="5c867-124">Availability sets for the VMs with a similar role</span></span>
* <span data-ttu-id="5c867-125">Maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="5c867-125">Virtual machines</span></span>

<span data-ttu-id="5c867-126">Wszystkie powyższe wykonaj te konwencji nazewnictwa:</span><span class="sxs-lookup"><span data-stu-id="5c867-126">All the above follow these naming conventions:</span></span>

* <span data-ttu-id="5c867-127">Adventure Works Cycles używa **[obciążenia IT]-[lokalizacja]-[zasobów platformy Azure]** jako prefiksu</span><span class="sxs-lookup"><span data-stu-id="5c867-127">Adventure Works Cycles uses **[IT workload]-[location]-[Azure resource]** as a prefix</span></span>
  * <span data-ttu-id="5c867-128">Na przykład "**azos**" (magazyn Azure On-line) jest nazwą obciążenia IT i "**użyj**" (wschodnie stany USA 2) to lokalizacja</span><span class="sxs-lookup"><span data-stu-id="5c867-128">For this example, "**azos**" (Azure On-line Store) is the IT workload name and "**use**" (East US 2) is the location</span></span>
* <span data-ttu-id="5c867-129">W sieciach wirtualnych za pomocą AZOS-użycie-VN**[numer]**</span><span class="sxs-lookup"><span data-stu-id="5c867-129">Virtual networks use AZOS-USE-VN**[number]**</span></span>
* <span data-ttu-id="5c867-130">Zestawy dostępności używać azos-Użyj — jako-**[rola]**</span><span class="sxs-lookup"><span data-stu-id="5c867-130">Availability sets use azos-use-as-**[role]**</span></span>
* <span data-ttu-id="5c867-131">Nazwy maszyn wirtualnych użyć azos-Użyj-vm -**[vmname]**</span><span class="sxs-lookup"><span data-stu-id="5c867-131">Virtual machine names use azos-use-vm-**[vmname]**</span></span>

## <a name="azure-subscriptions-and-accounts"></a><span data-ttu-id="5c867-132">Subskrypcje platformy Azure i konta</span><span class="sxs-lookup"><span data-stu-id="5c867-132">Azure subscriptions and accounts</span></span>
<span data-ttu-id="5c867-133">Firma Adventure Works Cycles używa ich subskrypcji Enterprise, o nazwie Adventure Works Enterprise subskrypcji, zapewnienie rozliczeń dla tej obciążenia IT.</span><span class="sxs-lookup"><span data-stu-id="5c867-133">Adventure Works Cycles is using their Enterprise subscription, named Adventure Works Enterprise Subscription, to provide billing for this IT workload.</span></span>

## <a name="storage"></a><span data-ttu-id="5c867-134">Magazyn</span><span class="sxs-lookup"><span data-stu-id="5c867-134">Storage</span></span>
<span data-ttu-id="5c867-135">Firma Adventure Works Cycles ustalić, czy powinny używać dysków zarządzanych Azure.</span><span class="sxs-lookup"><span data-stu-id="5c867-135">Adventure Works Cycles determined that they should use Azure Managed Disks.</span></span> <span data-ttu-id="5c867-136">Podczas tworzenia maszyn wirtualnych, są używane zarówno warstw magazynowania dostępne magazynu:</span><span class="sxs-lookup"><span data-stu-id="5c867-136">When creating VMs, both storage available storage tiers are used:</span></span>

* <span data-ttu-id="5c867-137">**Magazynu w warstwie standardowa** dla serwerów sieci web, serwerów aplikacji i kontrolerów domeny i dysków z danymi.</span><span class="sxs-lookup"><span data-stu-id="5c867-137">**Standard storage** for the web servers, application servers, and domain controllers and their data disks.</span></span>
* <span data-ttu-id="5c867-138">**Magazyn w warstwie Premium** dla serwerów klastra podzielonej bazy danych MongoDB i dysków z danymi.</span><span class="sxs-lookup"><span data-stu-id="5c867-138">**Premium storage** for the MongoDB sharded cluster servers and their data disks.</span></span>

## <a name="virtual-network-and-subnets"></a><span data-ttu-id="5c867-139">Sieć wirtualna i podsieci</span><span class="sxs-lookup"><span data-stu-id="5c867-139">Virtual network and subnets</span></span>
<span data-ttu-id="5c867-140">Ponieważ sieci wirtualnej nie wymaga trwających łączności z siecią lokalną cykle pracy Adventure, zdecydowano, że w sieci wirtualnej tylko w chmurze.</span><span class="sxs-lookup"><span data-stu-id="5c867-140">Because the virtual network does not need ongoing connectivity to the Adventure Work Cycles on-premises network, they decided on a cloud-only virtual network.</span></span>

<span data-ttu-id="5c867-141">Sieć wirtualna tylko w chmurze one utworzone przy użyciu następujących ustawień przy użyciu portalu Azure:</span><span class="sxs-lookup"><span data-stu-id="5c867-141">They created a cloud-only virtual network with the following settings using the Azure portal:</span></span>

* <span data-ttu-id="5c867-142">Nazwa: AZOS-użycie VN01</span><span class="sxs-lookup"><span data-stu-id="5c867-142">Name: AZOS-USE-VN01</span></span>
* <span data-ttu-id="5c867-143">Lokalizacji: Wschodnie stany USA 2</span><span class="sxs-lookup"><span data-stu-id="5c867-143">Location: East US 2</span></span>
* <span data-ttu-id="5c867-144">Przestrzeń adresową sieci wirtualnej: 10.0.0.0/8</span><span class="sxs-lookup"><span data-stu-id="5c867-144">Virtual network address space: 10.0.0.0/8</span></span>
* <span data-ttu-id="5c867-145">Pierwszej podsieci:</span><span class="sxs-lookup"><span data-stu-id="5c867-145">First subnet:</span></span>
  * <span data-ttu-id="5c867-146">Nazwa: frontonu</span><span class="sxs-lookup"><span data-stu-id="5c867-146">Name: FrontEnd</span></span>
  * <span data-ttu-id="5c867-147">Przestrzeń adresowa: 10.0.1.0/24</span><span class="sxs-lookup"><span data-stu-id="5c867-147">Address space: 10.0.1.0/24</span></span>
* <span data-ttu-id="5c867-148">Drugi podsieci:</span><span class="sxs-lookup"><span data-stu-id="5c867-148">Second subnet:</span></span>
  * <span data-ttu-id="5c867-149">Nazwa: wewnętrznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="5c867-149">Name: BackEnd</span></span>
  * <span data-ttu-id="5c867-150">Przestrzeń adresowa: 10.0.2.0/24</span><span class="sxs-lookup"><span data-stu-id="5c867-150">Address space: 10.0.2.0/24</span></span>

## <a name="availability-sets"></a><span data-ttu-id="5c867-151">Zestawy dostępności</span><span class="sxs-lookup"><span data-stu-id="5c867-151">Availability sets</span></span>
<span data-ttu-id="5c867-152">Aby zachować wysoką dostępność wszystkie cztery warstwy ich magazynu online, firma Adventure Works Cycles stanowi na cztery zestawy dostępności:</span><span class="sxs-lookup"><span data-stu-id="5c867-152">To maintain high availability of all four tiers of their on-line store, Adventure Works Cycles decided on four availability sets:</span></span>

* <span data-ttu-id="5c867-153">**azos używany jako web** dla serwerów sieci web</span><span class="sxs-lookup"><span data-stu-id="5c867-153">**azos-use-as-web** for the web servers</span></span>
* <span data-ttu-id="5c867-154">**azos używany jako aplikacji** dla serwerów aplikacji</span><span class="sxs-lookup"><span data-stu-id="5c867-154">**azos-use-as-app** for the application servers</span></span>
* <span data-ttu-id="5c867-155">**azos używany jako db** dla serwerów w klastrze podzielonej bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="5c867-155">**azos-use-as-db** for the servers in the MongoDB sharded cluster</span></span>
* <span data-ttu-id="5c867-156">**azos używany jako dc** dla kontrolerów domeny</span><span class="sxs-lookup"><span data-stu-id="5c867-156">**azos-use-as-dc** for the domain controllers</span></span>

## <a name="virtual-machines"></a><span data-ttu-id="5c867-157">Maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="5c867-157">Virtual machines</span></span>
<span data-ttu-id="5c867-158">Firma Adventure Works Cycles decyzję o następujących nazwach na swoich maszynach wirtualnych platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="5c867-158">Adventure Works Cycles decided on the following names for their Azure VMs:</span></span>

* <span data-ttu-id="5c867-159">**azos użycie vm-web01** na pierwszym serwerze sieci web</span><span class="sxs-lookup"><span data-stu-id="5c867-159">**azos-use-vm-web01** for the first web server</span></span>
* <span data-ttu-id="5c867-160">**azos użycie vm-web02** drugiego serwera sieci web</span><span class="sxs-lookup"><span data-stu-id="5c867-160">**azos-use-vm-web02** for the second web server</span></span>
* <span data-ttu-id="5c867-161">**azos użycie vm-app01** dla pierwszego serwera aplikacji</span><span class="sxs-lookup"><span data-stu-id="5c867-161">**azos-use-vm-app01** for the first application server</span></span>
* <span data-ttu-id="5c867-162">**azos użycie vm-app02** dla drugiego serwera aplikacji</span><span class="sxs-lookup"><span data-stu-id="5c867-162">**azos-use-vm-app02** for the second application server</span></span>
* <span data-ttu-id="5c867-163">**azos użycie vm-db01** dla pierwszego serwera bazy danych MongoDB w klastrze</span><span class="sxs-lookup"><span data-stu-id="5c867-163">**azos-use-vm-db01** for the first MongoDB server in the cluster</span></span>
* <span data-ttu-id="5c867-164">**azos użycie vm-db02** drugiego serwera bazy danych MongoDB w klastrze</span><span class="sxs-lookup"><span data-stu-id="5c867-164">**azos-use-vm-db02** for the second MongoDB server in the cluster</span></span>
* <span data-ttu-id="5c867-165">**azos użycie vm-dc01** dla pierwszego kontrolera domeny</span><span class="sxs-lookup"><span data-stu-id="5c867-165">**azos-use-vm-dc01** for the first domain controller</span></span>
* <span data-ttu-id="5c867-166">**azos użycie vm-dc02** dla kontrolera domeny</span><span class="sxs-lookup"><span data-stu-id="5c867-166">**azos-use-vm-dc02** for the second domain controller</span></span>

<span data-ttu-id="5c867-167">Oto wynikowej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="5c867-167">Here is the resulting configuration.</span></span>

![Infrastruktura aplikacji końcowego wdrożona na platformie Azure](./media/infrastructure-example/example-config.png)

<span data-ttu-id="5c867-169">Ta konfiguracja obejmuje:</span><span class="sxs-lookup"><span data-stu-id="5c867-169">This configuration incorporates:</span></span>

* <span data-ttu-id="5c867-170">Tylko w chmurze sieci wirtualnej z dwoma podsieciami (frontonu i wewnętrznej bazy danych)</span><span class="sxs-lookup"><span data-stu-id="5c867-170">A cloud-only virtual network with two subnets (FrontEnd and BackEnd)</span></span>
* <span data-ttu-id="5c867-171">Dyskach platformy Azure zarządzanych za pomocą dysków w wersjach Standard i Premium</span><span class="sxs-lookup"><span data-stu-id="5c867-171">Azure Managed Disks using both Standard and Premium disks</span></span>
* <span data-ttu-id="5c867-172">Cztery zestawy dostępności, jeden dla każdej warstwy magazynu online</span><span class="sxs-lookup"><span data-stu-id="5c867-172">Four availability sets, one for each tier of the on-line store</span></span>
* <span data-ttu-id="5c867-173">Maszyny wirtualne w czterech warstwach</span><span class="sxs-lookup"><span data-stu-id="5c867-173">The virtual machines for the four tiers</span></span>
* <span data-ttu-id="5c867-174">Zestaw o zrównoważonym obciążeniu zewnętrznych dla ruchu w sieci web z protokołem HTTPS z Internetu na serwerach sieci web</span><span class="sxs-lookup"><span data-stu-id="5c867-174">An external load balanced set for HTTPS-based web traffic from the Internet to the web servers</span></span>
* <span data-ttu-id="5c867-175">Zestaw dla ruchu w sieci web niezaszyfrowane z serwerów sieci web na serwery aplikacji o zrównoważonym obciążeniu wewnętrzny</span><span class="sxs-lookup"><span data-stu-id="5c867-175">An internal load balanced set for unencrypted web traffic from the web servers to the application servers</span></span>
* <span data-ttu-id="5c867-176">Pojedyncza grupa zasobów</span><span class="sxs-lookup"><span data-stu-id="5c867-176">A single resource group</span></span>
