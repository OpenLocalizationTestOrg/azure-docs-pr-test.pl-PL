---
title: "Przykłady konfiguracji routera klienta ExpressRoute | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera przykłady konfiguracji routera dla routerów Cisco i Juniper."
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: 564826bc-017a-4683-a385-37c9fa814948
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/10/2016
ms.author: cherylmc
ms.openlocfilehash: 032e584dc5abf59e9e3e8d80673b402f1fbf721b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="router-configuration-samples-to-set-up-and-manage-routing"></a><span data-ttu-id="922e6-103">Przykłady konfiguracji routera do konfigurowania i zarządzania nią routingu</span><span class="sxs-lookup"><span data-stu-id="922e6-103">Router configuration samples to set up and manage routing</span></span>
<span data-ttu-id="922e6-104">Ta strona zawiera interfejs i przykłady konfiguracji routingu dla systemu IOS-XE Cisco i Juniper MX routerów serii.</span><span class="sxs-lookup"><span data-stu-id="922e6-104">This page provides interface and routing configuration samples for Cisco IOS-XE and Juniper MX series routers.</span></span> <span data-ttu-id="922e6-105">Te powinny być przykłady tylko do celów informacyjnych i nie mogą być używane, ponieważ jest.</span><span class="sxs-lookup"><span data-stu-id="922e6-105">These are intended to be samples for guidance only and must not be used as is.</span></span> <span data-ttu-id="922e6-106">Możesz pracować z dostawcą pozwoli uzyskać odpowiedni konfiguracji sieci.</span><span class="sxs-lookup"><span data-stu-id="922e6-106">You can work with your vendor to come up with appropriate configurations for your network.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="922e6-107">Przykłady na tej stronie mają być wyłącznie w celu uzyskania wskazówek.</span><span class="sxs-lookup"><span data-stu-id="922e6-107">Samples in this page are intended to be purely for guidance.</span></span> <span data-ttu-id="922e6-108">Należy skontaktować się z zespołu sprzedaży / techniczne z dostawcą i sieci zespołu pozwoli uzyskać odpowiedni konfiguracji zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="922e6-108">You must work with your vendor's sales / technical team and your networking team to come up with appropriate configurations to meet your needs.</span></span> <span data-ttu-id="922e6-109">Microsoft nie będzie obsługiwał problemy związane z konfiguracji opisanych w tej strony.</span><span class="sxs-lookup"><span data-stu-id="922e6-109">Microsoft will not support issues related to configurations listed in this page.</span></span> <span data-ttu-id="922e6-110">Należy się z dostawcą urządzenia pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="922e6-110">You must contact your device vendor for support issues.</span></span>
> 
> 

## <a name="mtu-and-tcp-mss-settings-on-router-interfaces"></a><span data-ttu-id="922e6-111">Ustawienia MTU i TCP MSS w interfejsach routera</span><span class="sxs-lookup"><span data-stu-id="922e6-111">MTU and TCP MSS settings on router interfaces</span></span>
* <span data-ttu-id="922e6-112">Rozmiar jednostki MTU interfejsu ExpressRoute jest 1500, która jest typowy domyślny rozmiar jednostki MTU interfejsu Ethernet na routerze.</span><span class="sxs-lookup"><span data-stu-id="922e6-112">The MTU for the ExpressRoute interface is 1500, which is the typical default MTU for an Ethernet interface on a router.</span></span> <span data-ttu-id="922e6-113">Jeśli router domyślnie ma inny rozmiar jednostki MTU, jest niepotrzebna określenie wartości w interfejsie routera.</span><span class="sxs-lookup"><span data-stu-id="922e6-113">Unless your router has a different MTU by default, there is no need to specify a value on the router interface.</span></span>
* <span data-ttu-id="922e6-114">W przeciwieństwie do bramy sieci VPN platformy Azure MSS TCP dla obwodu usługi ExpressRoute nie trzeba określić.</span><span class="sxs-lookup"><span data-stu-id="922e6-114">Unlike an Azure VPN Gateway, the TCP MSS for an ExpressRoute circuit does not need to be specified.</span></span>

<span data-ttu-id="922e6-115">Poniższe przykłady konfiguracji routera mają zastosowanie do wszystkich komunikacji równorzędnych.</span><span class="sxs-lookup"><span data-stu-id="922e6-115">Router configuration samples below apply to all peerings.</span></span> <span data-ttu-id="922e6-116">Przegląd [komunikacji równorzędnych ExpressRoute](expressroute-circuit-peerings.md) i [wymagania dotyczące routingu usługi ExpressRoute](expressroute-routing.md) uzyskać więcej informacji o routingu.</span><span class="sxs-lookup"><span data-stu-id="922e6-116">Review [ExpressRoute peerings](expressroute-circuit-peerings.md) and [ExpressRoute routing requirements](expressroute-routing.md) for more details on routing.</span></span>


## <a name="cisco-ios-xe-based-routers"></a><span data-ttu-id="922e6-117">Cisco IOS-XE na podstawie routery</span><span class="sxs-lookup"><span data-stu-id="922e6-117">Cisco IOS-XE based routers</span></span>
<span data-ttu-id="922e6-118">Przykłady w tej sekcji dotyczą żadnych router, na którym uruchomiono rodziny systemów operacyjnych IOS XE.</span><span class="sxs-lookup"><span data-stu-id="922e6-118">The samples in this section apply for any router running the IOS-XE OS family.</span></span>

### <a name="1-configuring-interfaces-and-sub-interfaces"></a><span data-ttu-id="922e6-119">1. Konfigurowanie w interfejsach i podrzędne</span><span class="sxs-lookup"><span data-stu-id="922e6-119">1. Configuring interfaces and sub-interfaces</span></span>
<span data-ttu-id="922e6-120">Konieczne będzie interfejs sub na równorzędna każdego routera, gdy nawiązujesz połączenie do firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="922e6-120">You will require a sub interface per peering in every router you connect to Microsoft.</span></span> <span data-ttu-id="922e6-121">Interfejs podsieci można zidentyfikować z Identyfikatorem sieci VLAN lub pary skumulowany identyfikatorów sieci VLAN i adresu IP.</span><span class="sxs-lookup"><span data-stu-id="922e6-121">A sub interface can be identified with a VLAN ID or a stacked pair of VLAN IDs and an IP address.</span></span>

<span data-ttu-id="922e6-122">**Definicja interfejsu Dot1Q**</span><span class="sxs-lookup"><span data-stu-id="922e6-122">**Dot1Q interface definition**</span></span>

<span data-ttu-id="922e6-123">W tym przykładzie przedstawiono definicję interfejsu podrzędnego interfejsu podrzędnego z jednego identyfikatora sieci VLAN.</span><span class="sxs-lookup"><span data-stu-id="922e6-123">This sample provides the sub-interface definition for a sub-interface with a single VLAN ID.</span></span> <span data-ttu-id="922e6-124">Identyfikator sieci VLAN jest unikatowy dla komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="922e6-124">The VLAN ID is unique per peering.</span></span> <span data-ttu-id="922e6-125">Ostatni oktet adresu IPv4 zawsze jest liczbą nieparzystą.</span><span class="sxs-lookup"><span data-stu-id="922e6-125">The last octet of your IPv4 address will always be an odd number.</span></span>

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <VLAN_ID>
     ip address <IPv4_Address><Subnet_Mask>

<span data-ttu-id="922e6-126">**Definicja interfejsu QinQ**</span><span class="sxs-lookup"><span data-stu-id="922e6-126">**QinQ interface definition**</span></span>

<span data-ttu-id="922e6-127">W tym przykładzie przedstawiono definicję interfejsu podrzędnego interfejsu podrzędnego z dwóch identyfikatorów sieci VLAN.</span><span class="sxs-lookup"><span data-stu-id="922e6-127">This sample provides the sub-interface definition for a sub-interface with a two VLAN IDs.</span></span> <span data-ttu-id="922e6-128">Zewnętrzne identyfikator sieci VLAN (s-tag), jeśli używana jest taka sama we wszystkich komunikacji równorzędnych.</span><span class="sxs-lookup"><span data-stu-id="922e6-128">The outer VLAN ID (s-tag), if used remains the same across all the peerings.</span></span> <span data-ttu-id="922e6-129">Wewnętrzny identyfikator sieci VLAN (c znacznik) jest unikatowy dla komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="922e6-129">The inner VLAN ID (c-tag) is unique per peering.</span></span> <span data-ttu-id="922e6-130">Ostatni oktet adresu IPv4 zawsze jest liczbą nieparzystą.</span><span class="sxs-lookup"><span data-stu-id="922e6-130">The last octet of your IPv4 address will always be an odd number.</span></span>

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <s-tag> seconddot1Q <c-tag>
     ip address <IPv4_Address><Subnet_Mask>

### <a name="2-setting-up-ebgp-sessions"></a><span data-ttu-id="922e6-131">2. Konfigurowanie sesji eBGP</span><span class="sxs-lookup"><span data-stu-id="922e6-131">2. Setting up eBGP sessions</span></span>
<span data-ttu-id="922e6-132">Należy skonfigurować sesję protokołu BGP z firmy Microsoft dla każdej komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="922e6-132">You must setup a BGP session with Microsoft for every peering.</span></span> <span data-ttu-id="922e6-133">Poniższy przykład umożliwia skonfigurować sesję protokołu BGP z firmą Microsoft.</span><span class="sxs-lookup"><span data-stu-id="922e6-133">The sample below enables you to setup a BGP session with Microsoft.</span></span> <span data-ttu-id="922e6-134">Jeśli adres IPv4 dla interfejsu sub a.b.c.d, adres IP sąsiadów BGP (Microsoft) będzie a.b.c.d+1.</span><span class="sxs-lookup"><span data-stu-id="922e6-134">If the IPv4 address you used for your sub interface was a.b.c.d, the IP address of the BGP neighbor (Microsoft) will be a.b.c.d+1.</span></span> <span data-ttu-id="922e6-135">Ostatni oktet adresu IPv4 sąsiadów BGP będą zawsze miały liczbą parzystą.</span><span class="sxs-lookup"><span data-stu-id="922e6-135">The last octet of the BGP neighbor's IPv4 address will always be an even number.</span></span>

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
     neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="3-setting-up-prefixes-to-be-advertised-over-the-bgp-session"></a><span data-ttu-id="922e6-136">3. Konfigurowanie prefiksy anonsowanie sesji BGP</span><span class="sxs-lookup"><span data-stu-id="922e6-136">3. Setting up prefixes to be advertised over the BGP session</span></span>
<span data-ttu-id="922e6-137">Można skonfigurować router tak, aby anonsowania prefiksów wybierz do firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="922e6-137">You can configure your router to advertise select prefixes to Microsoft.</span></span> <span data-ttu-id="922e6-138">Możesz to zrobić przy użyciu poniższych przykładowych.</span><span class="sxs-lookup"><span data-stu-id="922e6-138">You can do so using the sample below.</span></span>

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
      network <Prefix_to_be_advertised> mask <Subnet_mask>
      neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="4-route-maps"></a><span data-ttu-id="922e6-139">4. Mapuje trasy</span><span class="sxs-lookup"><span data-stu-id="922e6-139">4. Route maps</span></span>
<span data-ttu-id="922e6-140">Można użyć mapy trasy i prefiksu list prefiksy filtru propagowane do sieci.</span><span class="sxs-lookup"><span data-stu-id="922e6-140">You can use route-maps and prefix lists to filter prefixes propagated into your network.</span></span> <span data-ttu-id="922e6-141">Poniższy przykład służy do wykonywania tego zadania.</span><span class="sxs-lookup"><span data-stu-id="922e6-141">You can use the sample below to accomplish the task.</span></span> <span data-ttu-id="922e6-142">Upewnij się, że Instalator wyświetla odpowiedni prefiks.</span><span class="sxs-lookup"><span data-stu-id="922e6-142">Ensure that you have appropriate prefix lists setup.</span></span>

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
      network <Prefix_to_be_advertised> mask <Subnet_mask>
      neighbor <IP#2_used_by_Azure> activate
      neighbor <IP#2_used_by_Azure> route-map <MS_Prefixes_Inbound> in
     exit-address-family
    !
    route-map <MS_Prefixes_Inbound> permit 10
     match ip address prefix-list <MS_Prefixes>
    !


## <a name="juniper-mx-series-routers"></a><span data-ttu-id="922e6-143">Routery serii juniper MX</span><span class="sxs-lookup"><span data-stu-id="922e6-143">Juniper MX series routers</span></span>
<span data-ttu-id="922e6-144">Przykłady w tej sekcji dotyczą wszystkie routery serii Juniper MX.</span><span class="sxs-lookup"><span data-stu-id="922e6-144">The samples in this section apply for any Juniper MX series routers.</span></span>

### <a name="1-configuring-interfaces-and-sub-interfaces"></a><span data-ttu-id="922e6-145">1. Konfigurowanie w interfejsach i podrzędne</span><span class="sxs-lookup"><span data-stu-id="922e6-145">1. Configuring interfaces and sub-interfaces</span></span>

<span data-ttu-id="922e6-146">**Definicja interfejsu Dot1Q**</span><span class="sxs-lookup"><span data-stu-id="922e6-146">**Dot1Q interface definition**</span></span>

<span data-ttu-id="922e6-147">W tym przykładzie przedstawiono definicję interfejsu podrzędnego interfejsu podrzędnego z jednego identyfikatora sieci VLAN.</span><span class="sxs-lookup"><span data-stu-id="922e6-147">This sample provides the sub-interface definition for a sub-interface with a single VLAN ID.</span></span> <span data-ttu-id="922e6-148">Identyfikator sieci VLAN jest unikatowy dla komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="922e6-148">The VLAN ID is unique per peering.</span></span> <span data-ttu-id="922e6-149">Ostatni oktet adresu IPv4 zawsze jest liczbą nieparzystą.</span><span class="sxs-lookup"><span data-stu-id="922e6-149">The last octet of your IPv4 address will always be an odd number.</span></span>

    interfaces {
        vlan-tagging;
        <Interface_Number> {
            unit <Number> {
                vlan-id <VLAN_ID>;
                family inet {
                    address <IPv4_Address/Subnet_Mask>;
                }
            }
        }
    }


<span data-ttu-id="922e6-150">**Definicja interfejsu QinQ**</span><span class="sxs-lookup"><span data-stu-id="922e6-150">**QinQ interface definition**</span></span>

<span data-ttu-id="922e6-151">W tym przykładzie przedstawiono definicję interfejsu podrzędnego interfejsu podrzędnego z dwóch identyfikatorów sieci VLAN.</span><span class="sxs-lookup"><span data-stu-id="922e6-151">This sample provides the sub-interface definition for a sub-interface with a two VLAN IDs.</span></span> <span data-ttu-id="922e6-152">Zewnętrzne identyfikator sieci VLAN (s-tag), jeśli używana jest taka sama we wszystkich komunikacji równorzędnych.</span><span class="sxs-lookup"><span data-stu-id="922e6-152">The outer VLAN ID (s-tag), if used remains the same across all the peerings.</span></span> <span data-ttu-id="922e6-153">Wewnętrzny identyfikator sieci VLAN (c znacznik) jest unikatowy dla komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="922e6-153">The inner VLAN ID (c-tag) is unique per peering.</span></span> <span data-ttu-id="922e6-154">Ostatni oktet adresu IPv4 zawsze jest liczbą nieparzystą.</span><span class="sxs-lookup"><span data-stu-id="922e6-154">The last octet of your IPv4 address will always be an odd number.</span></span>

    interfaces {
        <Interface_Number> {
            flexible-vlan-tagging;
            unit <Number> {
                vlan-tags outer <S-tag> inner <C-tag>;
                family inet {
                    address <IPv4_Address/Subnet_Mask>;
                }                           
            }                               
        }                                   
    }                           

### <a name="2-setting-up-ebgp-sessions"></a><span data-ttu-id="922e6-155">2. Konfigurowanie sesji eBGP</span><span class="sxs-lookup"><span data-stu-id="922e6-155">2. Setting up eBGP sessions</span></span>
<span data-ttu-id="922e6-156">Należy skonfigurować sesję protokołu BGP z firmy Microsoft dla każdej komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="922e6-156">You must setup a BGP session with Microsoft for every peering.</span></span> <span data-ttu-id="922e6-157">Poniższy przykład umożliwia skonfigurować sesję protokołu BGP z firmą Microsoft.</span><span class="sxs-lookup"><span data-stu-id="922e6-157">The sample below enables you to setup a BGP session with Microsoft.</span></span> <span data-ttu-id="922e6-158">Jeśli adres IPv4 dla interfejsu sub a.b.c.d, adres IP sąsiadów BGP (Microsoft) będzie a.b.c.d+1.</span><span class="sxs-lookup"><span data-stu-id="922e6-158">If the IPv4 address you used for your sub interface was a.b.c.d, the IP address of the BGP neighbor (Microsoft) will be a.b.c.d+1.</span></span> <span data-ttu-id="922e6-159">Ostatni oktet adresu IPv4 sąsiadów BGP będą zawsze miały liczbą parzystą.</span><span class="sxs-lookup"><span data-stu-id="922e6-159">The last octet of the BGP neighbor's IPv4 address will always be an even number.</span></span>

    routing-options {
        autonomous-system <Customer_ASN>;
    }
    }
    protocols {
        bgp { 
            group <Group_Name> { 
                peer-as 12076;              
                neighbor <IP#2_used_by_Azure>;
            }                               
        }                                   
    }

### <a name="3-setting-up-prefixes-to-be-advertised-over-the-bgp-session"></a><span data-ttu-id="922e6-160">3. Konfigurowanie prefiksy anonsowanie sesji BGP</span><span class="sxs-lookup"><span data-stu-id="922e6-160">3. Setting up prefixes to be advertised over the BGP session</span></span>
<span data-ttu-id="922e6-161">Można skonfigurować router tak, aby anonsowania prefiksów wybierz do firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="922e6-161">You can configure your router to advertise select prefixes to Microsoft.</span></span> <span data-ttu-id="922e6-162">Możesz to zrobić przy użyciu poniższych przykładowych.</span><span class="sxs-lookup"><span data-stu-id="922e6-162">You can do so using the sample below.</span></span>

    policy-options {
        policy-statement <Policy_Name> {
            term 1 {
                from protocol OSPF;
        route-filter <Prefix_to_be_advertised/Subnet_Mask> exact;
                then {
                    accept;
                }
            }
        }
    }
    protocols {
        bgp { 
            group <Group_Name> { 
                export <Policy_Name>
                peer-as 12076;              
                neighbor <IP#2_used_by_Azure>;
            }                               
        }                                   
    }


### <a name="4-route-maps"></a><span data-ttu-id="922e6-163">4. Mapuje trasy</span><span class="sxs-lookup"><span data-stu-id="922e6-163">4. Route maps</span></span>
<span data-ttu-id="922e6-164">Można użyć mapy trasy i prefiksu list prefiksy filtru propagowane do sieci.</span><span class="sxs-lookup"><span data-stu-id="922e6-164">You can use route-maps and prefix lists to filter prefixes propagated into your network.</span></span> <span data-ttu-id="922e6-165">Poniższy przykład służy do wykonywania tego zadania.</span><span class="sxs-lookup"><span data-stu-id="922e6-165">You can use the sample below to accomplish the task.</span></span> <span data-ttu-id="922e6-166">Upewnij się, że Instalator wyświetla odpowiedni prefiks.</span><span class="sxs-lookup"><span data-stu-id="922e6-166">Ensure that you have appropriate prefix lists setup.</span></span>

    policy-options {
        prefix-list MS_Prefixes {
            <IP_Prefix_1/Subnet_Mask>;
            <IP_Prefix_2/Subnet_Mask>;
        }
        policy-statement <MS_Prefixes_Inbound> {
            term 1 {
                from {
        prefix-list MS_Prefixes;
                }
                then {
                    accept;
                }
            }
        }
    }
    protocols {
        bgp { 
            group <Group_Name> { 
                export <Policy_Name>
                import <MS_Prefixes_Inbound>
                peer-as 12076;              
                neighbor <IP#2_used_by_Azure>;
            }                               
        }                                   
    }

## <a name="next-steps"></a><span data-ttu-id="922e6-167">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="922e6-167">Next Steps</span></span>
<span data-ttu-id="922e6-168">Szczegółowe informacje znajdują się w artykule [ExpressRoute FAQ](expressroute-faqs.md) (Usługa ExpressRoute — często zadawane pytania).</span><span class="sxs-lookup"><span data-stu-id="922e6-168">See the [ExpressRoute FAQ](expressroute-faqs.md) for more details.</span></span>

