---
title: "Przykłady konfiguracji routera klienta aaaExpressRoute | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 5c91f24e6082e01c3e8df91b4fcfda46a6c29fa8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="router-configuration-samples-tooset-up-and-manage-routing"></a><span data-ttu-id="5d420-103">Konfiguracja routera przykłady tooset się i zarządzanie nimi routingu</span><span class="sxs-lookup"><span data-stu-id="5d420-103">Router configuration samples tooset up and manage routing</span></span>
<span data-ttu-id="5d420-104">Ta strona zawiera interfejs i przykłady konfiguracji routingu dla systemu IOS-XE Cisco i Juniper MX routerów serii.</span><span class="sxs-lookup"><span data-stu-id="5d420-104">This page provides interface and routing configuration samples for Cisco IOS-XE and Juniper MX series routers.</span></span> <span data-ttu-id="5d420-105">Służą one przykłady toobe przeznaczone tylko do celów informacyjnych i nie mogą być używane, ponieważ jest.</span><span class="sxs-lookup"><span data-stu-id="5d420-105">These are intended toobe samples for guidance only and must not be used as is.</span></span> <span data-ttu-id="5d420-106">Można pracować z toocome Twojego dostawcy z konfiguracjami odpowiednie dla danej sieci.</span><span class="sxs-lookup"><span data-stu-id="5d420-106">You can work with your vendor toocome up with appropriate configurations for your network.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="5d420-107">Przykłady na tej stronie są toobe przeznaczone wyłącznie w celu uzyskania wskazówek.</span><span class="sxs-lookup"><span data-stu-id="5d420-107">Samples in this page are intended toobe purely for guidance.</span></span> <span data-ttu-id="5d420-108">Należy skontaktować się z zespołu sprzedaży / techniczne z dostawcą i Twojej sieci toocome zespołu się z odpowiedniej konfiguracji toomeet potrzeb.</span><span class="sxs-lookup"><span data-stu-id="5d420-108">You must work with your vendor's sales / technical team and your networking team toocome up with appropriate configurations toomeet your needs.</span></span> <span data-ttu-id="5d420-109">Microsoft nie będzie obsługiwał problemy związane z tooconfigurations wymienione na tej stronie.</span><span class="sxs-lookup"><span data-stu-id="5d420-109">Microsoft will not support issues related tooconfigurations listed in this page.</span></span> <span data-ttu-id="5d420-110">Należy się z dostawcą urządzenia pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="5d420-110">You must contact your device vendor for support issues.</span></span>
> 
> 

## <a name="mtu-and-tcp-mss-settings-on-router-interfaces"></a><span data-ttu-id="5d420-111">Ustawienia MTU i TCP MSS w interfejsach routera</span><span class="sxs-lookup"><span data-stu-id="5d420-111">MTU and TCP MSS settings on router interfaces</span></span>
* <span data-ttu-id="5d420-112">Hello rozmiar jednostki MTU interfejsu ExpressRoute hello jest 1500, czyli hello typowy domyślny rozmiar jednostki MTU interfejsu Ethernet na routerze.</span><span class="sxs-lookup"><span data-stu-id="5d420-112">hello MTU for hello ExpressRoute interface is 1500, which is hello typical default MTU for an Ethernet interface on a router.</span></span> <span data-ttu-id="5d420-113">Jeśli router domyślnie ma inny rozmiar jednostki MTU, w nie mają toospecify nie konieczności wartości hello interfejs routera.</span><span class="sxs-lookup"><span data-stu-id="5d420-113">Unless your router has a different MTU by default, there is no need toospecify a value on hello router interface.</span></span>
* <span data-ttu-id="5d420-114">W przeciwieństwie do bramy sieci VPN Azure hello TCP MSS dla obwodu usługi ExpressRoute nie jest konieczne toobe określony.</span><span class="sxs-lookup"><span data-stu-id="5d420-114">Unlike an Azure VPN Gateway, hello TCP MSS for an ExpressRoute circuit does not need toobe specified.</span></span>

<span data-ttu-id="5d420-115">Poniższe przykłady konfiguracji routera mają zastosowanie tooall komunikacji równorzędnych.</span><span class="sxs-lookup"><span data-stu-id="5d420-115">Router configuration samples below apply tooall peerings.</span></span> <span data-ttu-id="5d420-116">Przegląd [komunikacji równorzędnych ExpressRoute](expressroute-circuit-peerings.md) i [wymagania dotyczące routingu usługi ExpressRoute](expressroute-routing.md) uzyskać więcej informacji o routingu.</span><span class="sxs-lookup"><span data-stu-id="5d420-116">Review [ExpressRoute peerings](expressroute-circuit-peerings.md) and [ExpressRoute routing requirements](expressroute-routing.md) for more details on routing.</span></span>


## <a name="cisco-ios-xe-based-routers"></a><span data-ttu-id="5d420-117">Cisco IOS-XE na podstawie routery</span><span class="sxs-lookup"><span data-stu-id="5d420-117">Cisco IOS-XE based routers</span></span>
<span data-ttu-id="5d420-118">Hello próbek w tej sekcji dotyczą żadnych router, na którym uruchomiono rodziny systemów operacyjnych IOS XE hello.</span><span class="sxs-lookup"><span data-stu-id="5d420-118">hello samples in this section apply for any router running hello IOS-XE OS family.</span></span>

### <a name="1-configuring-interfaces-and-sub-interfaces"></a><span data-ttu-id="5d420-119">1. Konfigurowanie w interfejsach i podrzędne</span><span class="sxs-lookup"><span data-stu-id="5d420-119">1. Configuring interfaces and sub-interfaces</span></span>
<span data-ttu-id="5d420-120">Konieczne będzie tooMicrosoft połączyć z interfejsem sub na komunikację równorzędną w każdym router.</span><span class="sxs-lookup"><span data-stu-id="5d420-120">You will require a sub interface per peering in every router you connect tooMicrosoft.</span></span> <span data-ttu-id="5d420-121">Interfejs podsieci można zidentyfikować z Identyfikatorem sieci VLAN lub pary skumulowany identyfikatorów sieci VLAN i adresu IP.</span><span class="sxs-lookup"><span data-stu-id="5d420-121">A sub interface can be identified with a VLAN ID or a stacked pair of VLAN IDs and an IP address.</span></span>

<span data-ttu-id="5d420-122">**Definicja interfejsu Dot1Q**</span><span class="sxs-lookup"><span data-stu-id="5d420-122">**Dot1Q interface definition**</span></span>

<span data-ttu-id="5d420-123">W tym przykładzie przedstawiono definicję interfejsu podrzędnego hello interfejsu podrzędnego z jednego identyfikatora sieci VLAN.</span><span class="sxs-lookup"><span data-stu-id="5d420-123">This sample provides hello sub-interface definition for a sub-interface with a single VLAN ID.</span></span> <span data-ttu-id="5d420-124">Identyfikator sieci VLAN Hello jest unikatowy dla komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="5d420-124">hello VLAN ID is unique per peering.</span></span> <span data-ttu-id="5d420-125">Witaj oktet ostatniego adresu IPv4 zawsze jest liczbą nieparzystą.</span><span class="sxs-lookup"><span data-stu-id="5d420-125">hello last octet of your IPv4 address will always be an odd number.</span></span>

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <VLAN_ID>
     ip address <IPv4_Address><Subnet_Mask>

<span data-ttu-id="5d420-126">**Definicja interfejsu QinQ**</span><span class="sxs-lookup"><span data-stu-id="5d420-126">**QinQ interface definition**</span></span>

<span data-ttu-id="5d420-127">W tym przykładzie przedstawiono definicję interfejsu podrzędnego hello interfejsu podrzędnego z dwóch identyfikatorów sieci VLAN.</span><span class="sxs-lookup"><span data-stu-id="5d420-127">This sample provides hello sub-interface definition for a sub-interface with a two VLAN IDs.</span></span> <span data-ttu-id="5d420-128">powitalne zewnętrzne identyfikator sieci VLAN (s-tag), jeśli używana jest hello sama we wszystkich hello komunikacji równorzędnych.</span><span class="sxs-lookup"><span data-stu-id="5d420-128">hello outer VLAN ID (s-tag), if used remains hello same across all hello peerings.</span></span> <span data-ttu-id="5d420-129">wewnętrzny Hello identyfikator sieci VLAN (c znacznik) jest unikatowy dla komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="5d420-129">hello inner VLAN ID (c-tag) is unique per peering.</span></span> <span data-ttu-id="5d420-130">Witaj oktet ostatniego adresu IPv4 zawsze jest liczbą nieparzystą.</span><span class="sxs-lookup"><span data-stu-id="5d420-130">hello last octet of your IPv4 address will always be an odd number.</span></span>

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <s-tag> seconddot1Q <c-tag>
     ip address <IPv4_Address><Subnet_Mask>

### <a name="2-setting-up-ebgp-sessions"></a><span data-ttu-id="5d420-131">2. Konfigurowanie sesji eBGP</span><span class="sxs-lookup"><span data-stu-id="5d420-131">2. Setting up eBGP sessions</span></span>
<span data-ttu-id="5d420-132">Należy skonfigurować sesję protokołu BGP z firmy Microsoft dla każdej komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="5d420-132">You must setup a BGP session with Microsoft for every peering.</span></span> <span data-ttu-id="5d420-133">Poniższy przykład Hello umożliwia toosetup sesję protokołu BGP z firmą Microsoft.</span><span class="sxs-lookup"><span data-stu-id="5d420-133">hello sample below enables you toosetup a BGP session with Microsoft.</span></span> <span data-ttu-id="5d420-134">Jeśli hello adresu IPv4, który był używany dla interfejsu sub a.b.c.d, hello adres IP sąsiadów BGP hello (Microsoft) będzie a.b.c.d+1.</span><span class="sxs-lookup"><span data-stu-id="5d420-134">If hello IPv4 address you used for your sub interface was a.b.c.d, hello IP address of hello BGP neighbor (Microsoft) will be a.b.c.d+1.</span></span> <span data-ttu-id="5d420-135">ostatni oktet Hello adresu IPv4 sąsiadów BGP hello jest zawsze liczbą parzystą.</span><span class="sxs-lookup"><span data-stu-id="5d420-135">hello last octet of hello BGP neighbor's IPv4 address will always be an even number.</span></span>

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
     neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="3-setting-up-prefixes-toobe-advertised-over-hello-bgp-session"></a><span data-ttu-id="5d420-136">3. Konfigurowanie toobe prefiksów anonsowanych hello sesji BGP</span><span class="sxs-lookup"><span data-stu-id="5d420-136">3. Setting up prefixes toobe advertised over hello BGP session</span></span>
<span data-ttu-id="5d420-137">Można skonfigurować tooMicrosoft Wybierz prefiksy tooadvertise Twojego router.</span><span class="sxs-lookup"><span data-stu-id="5d420-137">You can configure your router tooadvertise select prefixes tooMicrosoft.</span></span> <span data-ttu-id="5d420-138">Możesz to zrobić, za pomocą hello w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="5d420-138">You can do so using hello sample below.</span></span>

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
      network <Prefix_to_be_advertised> mask <Subnet_mask>
      neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="4-route-maps"></a><span data-ttu-id="5d420-139">4. Mapuje trasy</span><span class="sxs-lookup"><span data-stu-id="5d420-139">4. Route maps</span></span>
<span data-ttu-id="5d420-140">Można użyć mapy trasy oraz prefiks listę prefiksów toofilter propagowane do sieci.</span><span class="sxs-lookup"><span data-stu-id="5d420-140">You can use route-maps and prefix lists toofilter prefixes propagated into your network.</span></span> <span data-ttu-id="5d420-141">Możesz użyć hello przykładu poniżej tooaccomplish hello zadania.</span><span class="sxs-lookup"><span data-stu-id="5d420-141">You can use hello sample below tooaccomplish hello task.</span></span> <span data-ttu-id="5d420-142">Upewnij się, że Instalator wyświetla odpowiedni prefiks.</span><span class="sxs-lookup"><span data-stu-id="5d420-142">Ensure that you have appropriate prefix lists setup.</span></span>

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


## <a name="juniper-mx-series-routers"></a><span data-ttu-id="5d420-143">Routery serii juniper MX</span><span class="sxs-lookup"><span data-stu-id="5d420-143">Juniper MX series routers</span></span>
<span data-ttu-id="5d420-144">Witaj próbek w tej sekcji dotyczą wszystkie routery serii Juniper MX.</span><span class="sxs-lookup"><span data-stu-id="5d420-144">hello samples in this section apply for any Juniper MX series routers.</span></span>

### <a name="1-configuring-interfaces-and-sub-interfaces"></a><span data-ttu-id="5d420-145">1. Konfigurowanie w interfejsach i podrzędne</span><span class="sxs-lookup"><span data-stu-id="5d420-145">1. Configuring interfaces and sub-interfaces</span></span>

<span data-ttu-id="5d420-146">**Definicja interfejsu Dot1Q**</span><span class="sxs-lookup"><span data-stu-id="5d420-146">**Dot1Q interface definition**</span></span>

<span data-ttu-id="5d420-147">W tym przykładzie przedstawiono definicję interfejsu podrzędnego hello interfejsu podrzędnego z jednego identyfikatora sieci VLAN.</span><span class="sxs-lookup"><span data-stu-id="5d420-147">This sample provides hello sub-interface definition for a sub-interface with a single VLAN ID.</span></span> <span data-ttu-id="5d420-148">Identyfikator sieci VLAN Hello jest unikatowy dla komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="5d420-148">hello VLAN ID is unique per peering.</span></span> <span data-ttu-id="5d420-149">Witaj oktet ostatniego adresu IPv4 zawsze jest liczbą nieparzystą.</span><span class="sxs-lookup"><span data-stu-id="5d420-149">hello last octet of your IPv4 address will always be an odd number.</span></span>

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


<span data-ttu-id="5d420-150">**Definicja interfejsu QinQ**</span><span class="sxs-lookup"><span data-stu-id="5d420-150">**QinQ interface definition**</span></span>

<span data-ttu-id="5d420-151">W tym przykładzie przedstawiono definicję interfejsu podrzędnego hello interfejsu podrzędnego z dwóch identyfikatorów sieci VLAN.</span><span class="sxs-lookup"><span data-stu-id="5d420-151">This sample provides hello sub-interface definition for a sub-interface with a two VLAN IDs.</span></span> <span data-ttu-id="5d420-152">powitalne zewnętrzne identyfikator sieci VLAN (s-tag), jeśli używana jest hello sama we wszystkich hello komunikacji równorzędnych.</span><span class="sxs-lookup"><span data-stu-id="5d420-152">hello outer VLAN ID (s-tag), if used remains hello same across all hello peerings.</span></span> <span data-ttu-id="5d420-153">wewnętrzny Hello identyfikator sieci VLAN (c znacznik) jest unikatowy dla komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="5d420-153">hello inner VLAN ID (c-tag) is unique per peering.</span></span> <span data-ttu-id="5d420-154">Witaj oktet ostatniego adresu IPv4 zawsze jest liczbą nieparzystą.</span><span class="sxs-lookup"><span data-stu-id="5d420-154">hello last octet of your IPv4 address will always be an odd number.</span></span>

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

### <a name="2-setting-up-ebgp-sessions"></a><span data-ttu-id="5d420-155">2. Konfigurowanie sesji eBGP</span><span class="sxs-lookup"><span data-stu-id="5d420-155">2. Setting up eBGP sessions</span></span>
<span data-ttu-id="5d420-156">Należy skonfigurować sesję protokołu BGP z firmy Microsoft dla każdej komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="5d420-156">You must setup a BGP session with Microsoft for every peering.</span></span> <span data-ttu-id="5d420-157">Poniższy przykład Hello umożliwia toosetup sesję protokołu BGP z firmą Microsoft.</span><span class="sxs-lookup"><span data-stu-id="5d420-157">hello sample below enables you toosetup a BGP session with Microsoft.</span></span> <span data-ttu-id="5d420-158">Jeśli hello adresu IPv4, który był używany dla interfejsu sub a.b.c.d, hello adres IP sąsiadów BGP hello (Microsoft) będzie a.b.c.d+1.</span><span class="sxs-lookup"><span data-stu-id="5d420-158">If hello IPv4 address you used for your sub interface was a.b.c.d, hello IP address of hello BGP neighbor (Microsoft) will be a.b.c.d+1.</span></span> <span data-ttu-id="5d420-159">ostatni oktet Hello adresu IPv4 sąsiadów BGP hello jest zawsze liczbą parzystą.</span><span class="sxs-lookup"><span data-stu-id="5d420-159">hello last octet of hello BGP neighbor's IPv4 address will always be an even number.</span></span>

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

### <a name="3-setting-up-prefixes-toobe-advertised-over-hello-bgp-session"></a><span data-ttu-id="5d420-160">3. Konfigurowanie toobe prefiksów anonsowanych hello sesji BGP</span><span class="sxs-lookup"><span data-stu-id="5d420-160">3. Setting up prefixes toobe advertised over hello BGP session</span></span>
<span data-ttu-id="5d420-161">Można skonfigurować tooMicrosoft Wybierz prefiksy tooadvertise Twojego router.</span><span class="sxs-lookup"><span data-stu-id="5d420-161">You can configure your router tooadvertise select prefixes tooMicrosoft.</span></span> <span data-ttu-id="5d420-162">Możesz to zrobić, za pomocą hello w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="5d420-162">You can do so using hello sample below.</span></span>

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


### <a name="4-route-maps"></a><span data-ttu-id="5d420-163">4. Mapuje trasy</span><span class="sxs-lookup"><span data-stu-id="5d420-163">4. Route maps</span></span>
<span data-ttu-id="5d420-164">Można użyć mapy trasy oraz prefiks listę prefiksów toofilter propagowane do sieci.</span><span class="sxs-lookup"><span data-stu-id="5d420-164">You can use route-maps and prefix lists toofilter prefixes propagated into your network.</span></span> <span data-ttu-id="5d420-165">Możesz użyć hello przykładu poniżej tooaccomplish hello zadania.</span><span class="sxs-lookup"><span data-stu-id="5d420-165">You can use hello sample below tooaccomplish hello task.</span></span> <span data-ttu-id="5d420-166">Upewnij się, że Instalator wyświetla odpowiedni prefiks.</span><span class="sxs-lookup"><span data-stu-id="5d420-166">Ensure that you have appropriate prefix lists setup.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="5d420-167">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5d420-167">Next Steps</span></span>
<span data-ttu-id="5d420-168">Zobacz hello [ExpressRoute — często zadawane pytania](expressroute-faqs.md) więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="5d420-168">See hello [ExpressRoute FAQ](expressroute-faqs.md) for more details.</span></span>

