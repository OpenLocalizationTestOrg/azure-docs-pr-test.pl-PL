---
title: "aaaExample wskazówki infrastruktury platformy Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat hello klucza projekt i implementację wskazówki dotyczące wdrażania infrastruktury przykład na platformie Azure."
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7032b586-e4e5-4954-952f-fdfc03fc1980
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bd6b6e904404bea0b5be37dfce6d60039daae636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="example-azure-infrastructure-walkthrough-for-windows-vms"></a><span data-ttu-id="9ddbc-103">Przykład wskazówki infrastruktury platformy Azure dla maszyn wirtualnych systemu Windows</span><span class="sxs-lookup"><span data-stu-id="9ddbc-103">Example Azure infrastructure walkthrough for Windows VMs</span></span>

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

<span data-ttu-id="9ddbc-104">W tym artykule przedstawiono zbudowaniu przykład infrastruktury aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9ddbc-104">This article walks through building out an example application infrastructure.</span></span> <span data-ttu-id="9ddbc-105">Firma Microsoft szczegółowo projektowania infrastruktury dla prostego sklepu online, która gromadzi wszystkie hello wskazówki i decyzji dotyczących konwencji nazewnictwa, zestawów dostępności, sieci wirtualnych i usług równoważenia obciążenia i faktycznie wdrażania maszyn wirtualnych (VM).</span><span class="sxs-lookup"><span data-stu-id="9ddbc-105">We detail designing an infrastructure for a simple on-line store that brings together all hello guidelines and decisions around naming conventions, availability sets, virtual networks and load balancers, and actually deploying your virtual machines (VMs).</span></span>

## <a name="example-workload"></a><span data-ttu-id="9ddbc-106">Przykładowe obciążenie</span><span class="sxs-lookup"><span data-stu-id="9ddbc-106">Example workload</span></span>
<span data-ttu-id="9ddbc-107">Firma Adventure Works Cycles chce toobuild na platformie Azure, która składa się z aplikacji sklepu online:</span><span class="sxs-lookup"><span data-stu-id="9ddbc-107">Adventure Works Cycles wants toobuild an on-line store application in Azure that consists of:</span></span>

* <span data-ttu-id="9ddbc-108">Dwa serwery IIS z powitania klienta frontonu w warstwa sieci web</span><span class="sxs-lookup"><span data-stu-id="9ddbc-108">Two IIS servers running hello client front-end in a web tier</span></span>
* <span data-ttu-id="9ddbc-109">Przetwarzanie danych i zamówień w warstwie aplikacji dwóch serwerów usług IIS</span><span class="sxs-lookup"><span data-stu-id="9ddbc-109">Two IIS servers processing data and orders in an application tier</span></span>
* <span data-ttu-id="9ddbc-110">Dwa wystąpienia programu Microsoft SQL Server z grupami dostępności AlwaysOn (dwa serwery SQL i monitora węzła większość) do przechowywania danych produktu i zamówień w warstwy bazy danych</span><span class="sxs-lookup"><span data-stu-id="9ddbc-110">Two Microsoft SQL Server instances with AlwaysOn availability groups (two SQL Servers and a majority node witness) for storing product data and orders in a database tier</span></span>
* <span data-ttu-id="9ddbc-111">Dwa kontrolery domeny usługi Active Directory dla konta klienta i dostawców w warstwie uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="9ddbc-111">Two Active Directory domain controllers for customer accounts and suppliers in an authentication tier</span></span>
* <span data-ttu-id="9ddbc-112">Wszystkie serwery hello znajdują się w dwóch podsieci:</span><span class="sxs-lookup"><span data-stu-id="9ddbc-112">All hello servers are located in two subnets:</span></span>
  * <span data-ttu-id="9ddbc-113">podsieci frontonu hello serwerów sieci web</span><span class="sxs-lookup"><span data-stu-id="9ddbc-113">a front-end subnet for hello web servers</span></span> 
  * <span data-ttu-id="9ddbc-114">podsieć wewnętrznych serwerów aplikacji hello, klaster serwera SQL i kontrolerów domeny</span><span class="sxs-lookup"><span data-stu-id="9ddbc-114">a back-end subnet for hello application servers, SQL cluster, and domain controllers</span></span>

![Diagram różnych warstw dla infrastruktury aplikacji](./media/infrastructure-example/example-tiers.png)

<span data-ttu-id="9ddbc-116">Bezpieczne przychodzącego ruchu w sieci web muszą być równoważeniem obciążenia między serwerami sieci web hello jak klienci Przeglądaj hello sklepu online.</span><span class="sxs-lookup"><span data-stu-id="9ddbc-116">Incoming secure web traffic must be load-balanced among hello web servers as customers browse hello on-line store.</span></span> <span data-ttu-id="9ddbc-117">Kolejność przetwarzania ruchu sieciowego w postaci hello HTTP żądań sieci Web hello, serwery muszą być równoważony między serwerami aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="9ddbc-117">Order processing traffic in hello form of HTTP requests from hello web servers must be balanced among hello application servers.</span></span> <span data-ttu-id="9ddbc-118">Ponadto należy zaprojektować hello infrastruktury wysokiej dostępności.</span><span class="sxs-lookup"><span data-stu-id="9ddbc-118">Additionally, hello infrastructure must be designed for high availability.</span></span>

<span data-ttu-id="9ddbc-119">Projekt wynikowy Hello musi uwzględniać:</span><span class="sxs-lookup"><span data-stu-id="9ddbc-119">hello resulting design must incorporate:</span></span>

* <span data-ttu-id="9ddbc-120">Subskrypcja platformy Azure i konta</span><span class="sxs-lookup"><span data-stu-id="9ddbc-120">An Azure subscription and account</span></span>
* <span data-ttu-id="9ddbc-121">Pojedyncza grupa zasobów</span><span class="sxs-lookup"><span data-stu-id="9ddbc-121">A single resource group</span></span>
* <span data-ttu-id="9ddbc-122">Azure Managed Disks</span><span class="sxs-lookup"><span data-stu-id="9ddbc-122">Azure Managed Disks</span></span>
* <span data-ttu-id="9ddbc-123">Sieć wirtualną z dwiema podsieciami</span><span class="sxs-lookup"><span data-stu-id="9ddbc-123">A virtual network with two subnets</span></span>
* <span data-ttu-id="9ddbc-124">Zestawy dostępności dla hello maszyn wirtualnych z podobną rolę</span><span class="sxs-lookup"><span data-stu-id="9ddbc-124">Availability sets for hello VMs with a similar role</span></span>
* <span data-ttu-id="9ddbc-125">Maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="9ddbc-125">Virtual machines</span></span>

<span data-ttu-id="9ddbc-126">Wszystkie powyższe hello wykonaj te konwencji nazewnictwa:</span><span class="sxs-lookup"><span data-stu-id="9ddbc-126">All hello above follow these naming conventions:</span></span>

* <span data-ttu-id="9ddbc-127">Adventure Works Cycles używa **[obciążenia IT]-[lokalizacja]-[zasobów platformy Azure]** jako prefiksu</span><span class="sxs-lookup"><span data-stu-id="9ddbc-127">Adventure Works Cycles uses **[IT workload]-[location]-[Azure resource]** as a prefix</span></span>
  * <span data-ttu-id="9ddbc-128">Na przykład "**azos**" (magazyn Azure On-line) jest hello imię i nazwisko obciążenia IT i "**użyj**" hello lokalizacji jest (wschodnie stany USA 2)</span><span class="sxs-lookup"><span data-stu-id="9ddbc-128">For this example, "**azos**" (Azure On-line Store) is hello IT workload name and "**use**" (East US 2) is hello location</span></span>
* <span data-ttu-id="9ddbc-129">W sieciach wirtualnych za pomocą AZOS-użycie-VN**[numer]**</span><span class="sxs-lookup"><span data-stu-id="9ddbc-129">Virtual networks use AZOS-USE-VN**[number]**</span></span>
* <span data-ttu-id="9ddbc-130">Zestawy dostępności używać azos-Użyj — jako-**[rola]**</span><span class="sxs-lookup"><span data-stu-id="9ddbc-130">Availability sets use azos-use-as-**[role]**</span></span>
* <span data-ttu-id="9ddbc-131">Nazwy maszyn wirtualnych użyć azos-Użyj-vm -**[vmname]**</span><span class="sxs-lookup"><span data-stu-id="9ddbc-131">Virtual machine names use azos-use-vm-**[vmname]**</span></span>

## <a name="azure-subscriptions-and-accounts"></a><span data-ttu-id="9ddbc-132">Subskrypcje platformy Azure i konta</span><span class="sxs-lookup"><span data-stu-id="9ddbc-132">Azure subscriptions and accounts</span></span>
<span data-ttu-id="9ddbc-133">Adventure Works Cycles korzysta z ich subskrypcją przedsiębiorstwa, o nazwie Adventure Works Enterprise subskrypcji, rozliczeń dla tej obciążenia IT tooprovide.</span><span class="sxs-lookup"><span data-stu-id="9ddbc-133">Adventure Works Cycles is using their Enterprise subscription, named Adventure Works Enterprise Subscription, tooprovide billing for this IT workload.</span></span>

## <a name="storage"></a><span data-ttu-id="9ddbc-134">Magazyn</span><span class="sxs-lookup"><span data-stu-id="9ddbc-134">Storage</span></span>
<span data-ttu-id="9ddbc-135">Firma Adventure Works Cycles ustalić, czy powinny używać dysków zarządzanych Azure.</span><span class="sxs-lookup"><span data-stu-id="9ddbc-135">Adventure Works Cycles determined that they should use Azure Managed Disks.</span></span> <span data-ttu-id="9ddbc-136">Podczas tworzenia maszyn wirtualnych, są używane zarówno warstw magazynowania dostępne magazynu:</span><span class="sxs-lookup"><span data-stu-id="9ddbc-136">When creating VMs, both storage available storage tiers are used:</span></span>

* <span data-ttu-id="9ddbc-137">**Magazynu w warstwie standardowa** hello serwerów sieci web, serwerów aplikacji i kontrolerów domeny i dysków z danymi.</span><span class="sxs-lookup"><span data-stu-id="9ddbc-137">**Standard storage** for hello web servers, application servers, and domain controllers and their data disks.</span></span>
* <span data-ttu-id="9ddbc-138">**Magazyn w warstwie Premium** hello maszynach wirtualnych serwera SQL i dysków z danymi.</span><span class="sxs-lookup"><span data-stu-id="9ddbc-138">**Premium storage** for hello SQL Server VMs and their data disks.</span></span>

## <a name="virtual-network-and-subnets"></a><span data-ttu-id="9ddbc-139">Sieć wirtualna i podsieci</span><span class="sxs-lookup"><span data-stu-id="9ddbc-139">Virtual network and subnets</span></span>
<span data-ttu-id="9ddbc-140">Ponieważ hello sieci wirtualnej sieci lokalnej cykle pracy Adventure toohello bieżące połączenie nie jest konieczne, zdecydowano, że w sieci wirtualnej tylko w chmurze.</span><span class="sxs-lookup"><span data-stu-id="9ddbc-140">Because hello virtual network does not need ongoing connectivity toohello Adventure Work Cycles on-premises network, they decided on a cloud-only virtual network.</span></span>

<span data-ttu-id="9ddbc-141">One tworzone tylko na chmurze sieci wirtualnej z następującego ustawienia za pomocą portalu Azure hello hello:</span><span class="sxs-lookup"><span data-stu-id="9ddbc-141">They created a cloud-only virtual network with hello following settings using hello Azure portal:</span></span>

* <span data-ttu-id="9ddbc-142">Nazwa: AZOS-użycie VN01</span><span class="sxs-lookup"><span data-stu-id="9ddbc-142">Name: AZOS-USE-VN01</span></span>
* <span data-ttu-id="9ddbc-143">Lokalizacji: Wschodnie stany USA 2</span><span class="sxs-lookup"><span data-stu-id="9ddbc-143">Location: East US 2</span></span>
* <span data-ttu-id="9ddbc-144">Przestrzeń adresową sieci wirtualnej: 10.0.0.0/8</span><span class="sxs-lookup"><span data-stu-id="9ddbc-144">Virtual network address space: 10.0.0.0/8</span></span>
* <span data-ttu-id="9ddbc-145">Pierwszej podsieci:</span><span class="sxs-lookup"><span data-stu-id="9ddbc-145">First subnet:</span></span>
  * <span data-ttu-id="9ddbc-146">Nazwa: frontonu</span><span class="sxs-lookup"><span data-stu-id="9ddbc-146">Name: FrontEnd</span></span>
  * <span data-ttu-id="9ddbc-147">Przestrzeń adresowa: 10.0.1.0/24</span><span class="sxs-lookup"><span data-stu-id="9ddbc-147">Address space: 10.0.1.0/24</span></span>
* <span data-ttu-id="9ddbc-148">Drugi podsieci:</span><span class="sxs-lookup"><span data-stu-id="9ddbc-148">Second subnet:</span></span>
  * <span data-ttu-id="9ddbc-149">Nazwa: wewnętrznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="9ddbc-149">Name: BackEnd</span></span>
  * <span data-ttu-id="9ddbc-150">Przestrzeń adresowa: 10.0.2.0/24</span><span class="sxs-lookup"><span data-stu-id="9ddbc-150">Address space: 10.0.2.0/24</span></span>

## <a name="availability-sets"></a><span data-ttu-id="9ddbc-151">Zestawy dostępności</span><span class="sxs-lookup"><span data-stu-id="9ddbc-151">Availability sets</span></span>
<span data-ttu-id="9ddbc-152">Wysoka dostępność toomaintain wszystkie cztery warstwy ich magazynu online, firma Adventure Works Cycles na cztery zestawy dostępności:</span><span class="sxs-lookup"><span data-stu-id="9ddbc-152">toomaintain high availability of all four tiers of their on-line store, Adventure Works Cycles decided on four availability sets:</span></span>

* <span data-ttu-id="9ddbc-153">**azos używany jako web** hello serwerów sieci web</span><span class="sxs-lookup"><span data-stu-id="9ddbc-153">**azos-use-as-web** for hello web servers</span></span>
* <span data-ttu-id="9ddbc-154">**azos używany jako aplikacji** dla serwerów aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="9ddbc-154">**azos-use-as-app** for hello application servers</span></span>
* <span data-ttu-id="9ddbc-155">**azos używany jako sql** dla hello serwerów SQL</span><span class="sxs-lookup"><span data-stu-id="9ddbc-155">**azos-use-as-sql** for hello SQL Servers</span></span>
* <span data-ttu-id="9ddbc-156">**azos używany jako dc** hello kontrolerów domeny</span><span class="sxs-lookup"><span data-stu-id="9ddbc-156">**azos-use-as-dc** for hello domain controllers</span></span>

## <a name="virtual-machines"></a><span data-ttu-id="9ddbc-157">Maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="9ddbc-157">Virtual machines</span></span>
<span data-ttu-id="9ddbc-158">Firma Adventure Works Cycles na powitania po nazw dla swoich maszynach wirtualnych platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="9ddbc-158">Adventure Works Cycles decided on hello following names for their Azure VMs:</span></span>

* <span data-ttu-id="9ddbc-159">**azos użycie vm-web01** dla hello na pierwszym serwerze sieci web</span><span class="sxs-lookup"><span data-stu-id="9ddbc-159">**azos-use-vm-web01** for hello first web server</span></span>
* <span data-ttu-id="9ddbc-160">**azos użycie vm-web02** hello drugiego serwera sieci web</span><span class="sxs-lookup"><span data-stu-id="9ddbc-160">**azos-use-vm-web02** for hello second web server</span></span>
* <span data-ttu-id="9ddbc-161">**azos użycie vm-app01** dla pierwszego serwera aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="9ddbc-161">**azos-use-vm-app01** for hello first application server</span></span>
* <span data-ttu-id="9ddbc-162">**azos użycie vm-app02** dla drugiego serwera aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="9ddbc-162">**azos-use-vm-app02** for hello second application server</span></span>
* <span data-ttu-id="9ddbc-163">**azos użycie vm-sql01** hello pierwszego serwera programu SQL Server w klastrze hello</span><span class="sxs-lookup"><span data-stu-id="9ddbc-163">**azos-use-vm-sql01** for hello first SQL Server server in hello cluster</span></span>
* <span data-ttu-id="9ddbc-164">**azos użycie vm-sql02** hello drugiego serwera programu SQL Server w klastrze hello</span><span class="sxs-lookup"><span data-stu-id="9ddbc-164">**azos-use-vm-sql02** for hello second SQL Server server in hello cluster</span></span>
* <span data-ttu-id="9ddbc-165">**azos użycie vm-dc01** dla hello pierwszego kontrolera domeny</span><span class="sxs-lookup"><span data-stu-id="9ddbc-165">**azos-use-vm-dc01** for hello first domain controller</span></span>
* <span data-ttu-id="9ddbc-166">**azos użycie vm-dc02** dla hello kontrolera domeny</span><span class="sxs-lookup"><span data-stu-id="9ddbc-166">**azos-use-vm-dc02** for hello second domain controller</span></span>

<span data-ttu-id="9ddbc-167">Oto hello Wynikowa konfiguracja.</span><span class="sxs-lookup"><span data-stu-id="9ddbc-167">Here is hello resulting configuration.</span></span>

![Infrastruktura aplikacji końcowego wdrożona na platformie Azure](./media/infrastructure-example/example-config.png)

<span data-ttu-id="9ddbc-169">Ta konfiguracja obejmuje:</span><span class="sxs-lookup"><span data-stu-id="9ddbc-169">This configuration incorporates:</span></span>

* <span data-ttu-id="9ddbc-170">Tylko w chmurze sieci wirtualnej z dwoma podsieciami (frontonu i wewnętrznej bazy danych)</span><span class="sxs-lookup"><span data-stu-id="9ddbc-170">A cloud-only virtual network with two subnets (FrontEnd and BackEnd)</span></span>
* <span data-ttu-id="9ddbc-171">Dyskach platformy Azure zarządzanego z dyskami w wersjach Standard i Premium</span><span class="sxs-lookup"><span data-stu-id="9ddbc-171">Azure Managed Disks with both Standard and Premium disks</span></span>
* <span data-ttu-id="9ddbc-172">Cztery zestawy dostępności, jeden dla każdej warstwy hello sklep online</span><span class="sxs-lookup"><span data-stu-id="9ddbc-172">Four availability sets, one for each tier of hello on-line store</span></span>
* <span data-ttu-id="9ddbc-173">maszyny wirtualne Hello hello czterech warstw</span><span class="sxs-lookup"><span data-stu-id="9ddbc-173">hello virtual machines for hello four tiers</span></span>
* <span data-ttu-id="9ddbc-174">Zestaw o zrównoważonym obciążeniu zewnętrznych dla ruchu web oparty na protokole HTTPS z serwerów sieci web toohello internetowych hello</span><span class="sxs-lookup"><span data-stu-id="9ddbc-174">An external load balanced set for HTTPS-based web traffic from hello Internet toohello web servers</span></span>
* <span data-ttu-id="9ddbc-175">Zestaw dla ruchu w sieci web niezaszyfrowane z serwerów aplikacji toohello serwerów sieci web hello o zrównoważonym obciążeniu wewnętrzny</span><span class="sxs-lookup"><span data-stu-id="9ddbc-175">An internal load balanced set for unencrypted web traffic from hello web servers toohello application servers</span></span>
* <span data-ttu-id="9ddbc-176">Pojedyncza grupa zasobów</span><span class="sxs-lookup"><span data-stu-id="9ddbc-176">A single resource group</span></span>