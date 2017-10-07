---
title: "aaaOverview Oracle sytuacji odzyskiwania po awarii w środowisku platformy Azure | Dokumentacja firmy Microsoft"
description: "Scenariusza odzyskiwania po awarii dla bazy danych Oracle 12c w środowisku platformy Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 6/2/2017
ms.author: rclaus
ms.openlocfilehash: 1fa69e1ba044b46b27695fec92fd9ca82df796f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="disaster-recovery-for-an-oracle-database-12c-database-in-an-azure-environment"></a><span data-ttu-id="17455-103">Odzyskiwanie po awarii dla bazy danych programu Oracle Database 12c w środowisku platformy Azure</span><span class="sxs-lookup"><span data-stu-id="17455-103">Disaster recovery for an Oracle Database 12c database in an Azure environment</span></span>

## <a name="assumptions"></a><span data-ttu-id="17455-104">Wartości domyślne</span><span class="sxs-lookup"><span data-stu-id="17455-104">Assumptions</span></span>

- <span data-ttu-id="17455-105">Należy dobrze poznać zasady środowiska platformy Azure i Oracle Data Guard projektu.</span><span class="sxs-lookup"><span data-stu-id="17455-105">You have an understanding of Oracle Data Guard design and Azure environments.</span></span>


## <a name="goals"></a><span data-ttu-id="17455-106">Cele</span><span class="sxs-lookup"><span data-stu-id="17455-106">Goals</span></span>
- <span data-ttu-id="17455-107">Projektowanie topologii hello i konfiguracji, które spełniają wymagania odzyskiwanie po awarii.</span><span class="sxs-lookup"><span data-stu-id="17455-107">Design hello topology and configuration that meet your disaster recovery (DR) requirements.</span></span>

## <a name="scenario-1-primary-and-dr-sites-on-azure"></a><span data-ttu-id="17455-108">Scenariusz 1: Lokacji głównej i odzyskiwania po awarii lokacji na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="17455-108">Scenario 1: Primary and DR sites on Azure</span></span>

<span data-ttu-id="17455-109">Klient ma Oracle bazy danych Ustaw hello lokacji głównej.</span><span class="sxs-lookup"><span data-stu-id="17455-109">A customer has an Oracle database set up on hello primary site.</span></span> <span data-ttu-id="17455-110">Lokacja A DR znajduje się w innym regionie.</span><span class="sxs-lookup"><span data-stu-id="17455-110">A DR site is in a different region.</span></span> <span data-ttu-id="17455-111">powitania klienta używa Oracle Data Guard Szybkie odzyskiwanie między tymi lokacjami.</span><span class="sxs-lookup"><span data-stu-id="17455-111">hello customer uses Oracle Data Guard for quick recovery between these sites.</span></span> <span data-ttu-id="17455-112">lokacja główna Hello ma również pomocniczej bazy danych raportowania i innych celów.</span><span class="sxs-lookup"><span data-stu-id="17455-112">hello primary site also has a secondary database for reporting and other uses.</span></span> 

### <a name="topology"></a><span data-ttu-id="17455-113">Topologia</span><span class="sxs-lookup"><span data-stu-id="17455-113">Topology</span></span>

<span data-ttu-id="17455-114">Poniżej przedstawiono podsumowanie hello Azure Instalatora:</span><span class="sxs-lookup"><span data-stu-id="17455-114">Here is a summary of hello Azure setup:</span></span>

- <span data-ttu-id="17455-115">Dwie witryny (lokacji głównej i lokacji odzyskiwania po awarii)</span><span class="sxs-lookup"><span data-stu-id="17455-115">Two sites (a primary site and a DR site)</span></span>
- <span data-ttu-id="17455-116">Dwie sieci wirtualne</span><span class="sxs-lookup"><span data-stu-id="17455-116">Two virtual networks</span></span>
- <span data-ttu-id="17455-117">Dwóch baz danych Oracle Data Guard (podstawowe i stan gotowości)</span><span class="sxs-lookup"><span data-stu-id="17455-117">Two Oracle databases with Data Guard (primary and standby)</span></span>
- <span data-ttu-id="17455-118">Dwóch baz danych Oracle Golden bramy lub Data Guard (tylko w lokacji głównej)</span><span class="sxs-lookup"><span data-stu-id="17455-118">Two Oracle databases with Golden Gate or Data Guard (primary site only)</span></span>
- <span data-ttu-id="17455-119">Dwie usługi aplikacji, podstawowego i jeden w lokacji hello DR</span><span class="sxs-lookup"><span data-stu-id="17455-119">Two application services, one primary and one on hello DR site</span></span>
- <span data-ttu-id="17455-120">*Zestawu dostępności* używany dla usługi bazy danych i aplikacji w lokacji głównej hello</span><span class="sxs-lookup"><span data-stu-id="17455-120">An *availability set,* which is used for database and application service on hello primary site</span></span>
- <span data-ttu-id="17455-121">Jeden jumpbox w każdej lokacji, która ogranicza sieci prywatnej toohello dostępu i zezwala na logowanie przez administratora</span><span class="sxs-lookup"><span data-stu-id="17455-121">One jumpbox on each site, which restricts access toohello private network and only allows sign-in by an administrator</span></span>
- <span data-ttu-id="17455-122">Jumpbox, usługa aplikacji, bazy danych i Brama sieci VPN w różnych podsieciach</span><span class="sxs-lookup"><span data-stu-id="17455-122">A jumpbox, application service, database, and VPN gateway on separate subnets</span></span>
- <span data-ttu-id="17455-123">Grupa NSG wymuszone w aplikacji i podsieci bazy danych</span><span class="sxs-lookup"><span data-stu-id="17455-123">NSG enforced on application and database subnets</span></span>

![Zrzut ekranu przedstawiający stronę topologii hello DR](./media/oracle-disaster-recovery/oracle_topology_01.png)

## <a name="scenario-2-primary-site-on-premises-and-dr-site-on-azure"></a><span data-ttu-id="17455-125">Scenariusz 2: Lokalne lokacji głównej i lokacji odzyskiwania po awarii na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="17455-125">Scenario 2: Primary site on-premises and DR site on Azure</span></span>

<span data-ttu-id="17455-126">Klient ma Konfiguracja bazy danych Oracle lokalnymi (lokacji głównej).</span><span class="sxs-lookup"><span data-stu-id="17455-126">A customer has an on-premises Oracle database setup (primary site).</span></span> <span data-ttu-id="17455-127">Lokacja A DR jest na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="17455-127">A DR site is on Azure.</span></span> <span data-ttu-id="17455-128">Oracle Data Guard służy do szybkiego odzyskania między tymi lokacjami.</span><span class="sxs-lookup"><span data-stu-id="17455-128">Oracle Data Guard is used for quick recovery between these sites.</span></span> <span data-ttu-id="17455-129">lokacja główna Hello ma również pomocniczej bazy danych raportowania i innych celów.</span><span class="sxs-lookup"><span data-stu-id="17455-129">hello primary site also has a secondary database for reporting and other uses.</span></span> 

<span data-ttu-id="17455-130">Istnieją dwa podejścia do tej instalacji.</span><span class="sxs-lookup"><span data-stu-id="17455-130">There are two approaches for this setup.</span></span>

### <a name="approach-1-direct-connections-between-on-premises-and-azure-requiring-open-tcp-ports-on-hello-firewall"></a><span data-ttu-id="17455-131">Podejście 1: Bezpośrednich połączeń między lokalną i platformą Azure, wymagających otwartych portów TCP w zaporze hello</span><span class="sxs-lookup"><span data-stu-id="17455-131">Approach 1: Direct connections between on-premises and Azure, requiring open TCP ports on hello firewall</span></span> 

<span data-ttu-id="17455-132">Nie zaleca się bezpośredniego połączenia, ponieważ udostępniają toohello porty TCP hello poza world.</span><span class="sxs-lookup"><span data-stu-id="17455-132">We don't recommend direct connections because they expose hello TCP ports toohello outside world.</span></span>

#### <a name="topology"></a><span data-ttu-id="17455-133">Topologia</span><span class="sxs-lookup"><span data-stu-id="17455-133">Topology</span></span>

<span data-ttu-id="17455-134">Poniżej znajduje się podsumowanie hello Azure Instalatora:</span><span class="sxs-lookup"><span data-stu-id="17455-134">Following is a summary of hello Azure setup:</span></span>

- <span data-ttu-id="17455-135">Jeden odzyskiwania po awarii lokacji</span><span class="sxs-lookup"><span data-stu-id="17455-135">One DR site</span></span> 
- <span data-ttu-id="17455-136">Jedną sieć wirtualną</span><span class="sxs-lookup"><span data-stu-id="17455-136">One virtual network</span></span>
- <span data-ttu-id="17455-137">Co baza danych Oracle przy użyciu funkcji Guard danych (aktywny)</span><span class="sxs-lookup"><span data-stu-id="17455-137">One Oracle database with Data Guard (active)</span></span>
- <span data-ttu-id="17455-138">Usługa jedną aplikację w witrynie hello DR</span><span class="sxs-lookup"><span data-stu-id="17455-138">One application service on hello DR site</span></span>
- <span data-ttu-id="17455-139">Jumpbox jeden, co ogranicza sieci prywatnej toohello dostępu i zezwala na logowanie przez administratora</span><span class="sxs-lookup"><span data-stu-id="17455-139">One jumpbox, which restricts access toohello private network and only allows sign-in by an administrator</span></span>
- <span data-ttu-id="17455-140">Jumpbox, usługa aplikacji, bazy danych i Brama sieci VPN w różnych podsieciach</span><span class="sxs-lookup"><span data-stu-id="17455-140">A jumpbox, application service, database, and VPN gateway on separate subnets</span></span>
- <span data-ttu-id="17455-141">Grupa NSG wymuszone w aplikacji i podsieci bazy danych</span><span class="sxs-lookup"><span data-stu-id="17455-141">NSG enforced on application and database subnets</span></span>
- <span data-ttu-id="17455-142">Tooallow/reguły NSG ruchu przychodzącego dla portu TCP 1521 (lub portu zdefiniowane przez użytkownika)</span><span class="sxs-lookup"><span data-stu-id="17455-142">An NSG policy/rule tooallow inbound TCP port 1521 (or a user-defined port)</span></span>
- <span data-ttu-id="17455-143">Grupa NSG reguły/toorestrict tylko hello adresy adresów IP/sieci wirtualnej hello tooaccess lokalnymi (baza danych lub aplikacji)</span><span class="sxs-lookup"><span data-stu-id="17455-143">An NSG policy/rule toorestrict only hello IP address/addresses on-premises (DB or application) tooaccess hello virtual network</span></span>

![Zrzut ekranu przedstawiający stronę topologii hello DR](./media/oracle-disaster-recovery/oracle_topology_02.png)

### <a name="approach-2-site-to-site-vpn"></a><span data-ttu-id="17455-145">Podejście 2: VPN lokacja lokacja</span><span class="sxs-lookup"><span data-stu-id="17455-145">Approach 2: Site-to-site VPN</span></span>
<span data-ttu-id="17455-146">Sieć VPN lokacja lokacja jest lepszym rozwiązaniem.</span><span class="sxs-lookup"><span data-stu-id="17455-146">Site-to-site VPN is a better approach.</span></span> <span data-ttu-id="17455-147">Aby uzyskać więcej informacji na temat konfigurowania sieci VPN, zobacz [tworzenie sieci wirtualnej za pomocą połączenia sieci VPN typu lokacja-lokacja za pomocą interfejsu wiersza polecenia](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span><span class="sxs-lookup"><span data-stu-id="17455-147">For more information about setting up a VPN, see [Create a virtual network with a Site-to-Site VPN connection using CLI](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span></span>

#### <a name="topology"></a><span data-ttu-id="17455-148">Topologia</span><span class="sxs-lookup"><span data-stu-id="17455-148">Topology</span></span>

<span data-ttu-id="17455-149">Poniżej znajduje się podsumowanie hello Azure Instalatora:</span><span class="sxs-lookup"><span data-stu-id="17455-149">Following is a summary of hello Azure setup:</span></span>

- <span data-ttu-id="17455-150">Jeden odzyskiwania po awarii lokacji</span><span class="sxs-lookup"><span data-stu-id="17455-150">One DR site</span></span> 
- <span data-ttu-id="17455-151">Jedną sieć wirtualną</span><span class="sxs-lookup"><span data-stu-id="17455-151">One virtual network</span></span> 
- <span data-ttu-id="17455-152">Co baza danych Oracle przy użyciu funkcji Guard danych (aktywny)</span><span class="sxs-lookup"><span data-stu-id="17455-152">One Oracle database with Data Guard (active)</span></span>
- <span data-ttu-id="17455-153">Usługa jedną aplikację w witrynie hello DR</span><span class="sxs-lookup"><span data-stu-id="17455-153">One application service on hello DR site</span></span>
- <span data-ttu-id="17455-154">Jumpbox jeden, co ogranicza sieci prywatnej toohello dostępu i zezwala na logowanie przez administratora</span><span class="sxs-lookup"><span data-stu-id="17455-154">One jumpbox, which restricts access toohello private network and only allows sign-in by an administrator</span></span>
- <span data-ttu-id="17455-155">Jumpbox, usługa aplikacji, bazy danych i Brama sieci VPN są w różnych podsieciach</span><span class="sxs-lookup"><span data-stu-id="17455-155">A jumpbox, application service, database, and VPN gateway are on separate subnets</span></span>
- <span data-ttu-id="17455-156">Grupa NSG wymuszone w aplikacji i podsieci bazy danych</span><span class="sxs-lookup"><span data-stu-id="17455-156">NSG enforced on application and database subnets</span></span>
- <span data-ttu-id="17455-157">Połączenia sieci VPN lokacja lokacja między lokalną i platformą Azure</span><span class="sxs-lookup"><span data-stu-id="17455-157">Site-to-site VPN connection between on-premises and Azure</span></span>

![Zrzut ekranu przedstawiający stronę topologii hello DR](./media/oracle-disaster-recovery/oracle_topology_03.png)

## <a name="additional-reading"></a><span data-ttu-id="17455-159">Dodatkowe materiały</span><span class="sxs-lookup"><span data-stu-id="17455-159">Additional reading</span></span>

- [<span data-ttu-id="17455-160">Projektowania i implementacji bazy danych programu Oracle na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="17455-160">Design and implement an Oracle database on Azure</span></span>](oracle-design.md)
- [<span data-ttu-id="17455-161">Skonfiguruj Oracle Data Guard</span><span class="sxs-lookup"><span data-stu-id="17455-161">Configure Oracle Data Guard</span></span>](configure-oracle-dataguard.md)
- [<span data-ttu-id="17455-162">Konfigurowanie bramy Golden Oracle</span><span class="sxs-lookup"><span data-stu-id="17455-162">Configure Oracle Golden Gate</span></span>](configure-oracle-golden-gate.md)
- [<span data-ttu-id="17455-163">Oracle kopii zapasowych i odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="17455-163">Oracle backup and recovery</span></span>](oracle-backup-recovery.md)


## <a name="next-steps"></a><span data-ttu-id="17455-164">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="17455-164">Next steps</span></span>

- [<span data-ttu-id="17455-165">Samouczek: Tworzenie maszyn wirtualnych wysokiej dostępności</span><span class="sxs-lookup"><span data-stu-id="17455-165">Tutorial: Create highly available VMs</span></span>](../../linux/create-cli-complete.md)
- [<span data-ttu-id="17455-166">Eksploruj przykłady Azure CLI wdrożenia maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="17455-166">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)
