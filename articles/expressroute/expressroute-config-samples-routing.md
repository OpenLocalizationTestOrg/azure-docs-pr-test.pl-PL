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
# <a name="router-configuration-samples-tooset-up-and-manage-routing"></a>Konfiguracja routera przykłady tooset się i zarządzanie nimi routingu
Ta strona zawiera interfejs i przykłady konfiguracji routingu dla systemu IOS-XE Cisco i Juniper MX routerów serii. Służą one przykłady toobe przeznaczone tylko do celów informacyjnych i nie mogą być używane, ponieważ jest. Można pracować z toocome Twojego dostawcy z konfiguracjami odpowiednie dla danej sieci. 

> [!IMPORTANT]
> Przykłady na tej stronie są toobe przeznaczone wyłącznie w celu uzyskania wskazówek. Należy skontaktować się z zespołu sprzedaży / techniczne z dostawcą i Twojej sieci toocome zespołu się z odpowiedniej konfiguracji toomeet potrzeb. Microsoft nie będzie obsługiwał problemy związane z tooconfigurations wymienione na tej stronie. Należy się z dostawcą urządzenia pomocy technicznej.
> 
> 

## <a name="mtu-and-tcp-mss-settings-on-router-interfaces"></a>Ustawienia MTU i TCP MSS w interfejsach routera
* Hello rozmiar jednostki MTU interfejsu ExpressRoute hello jest 1500, czyli hello typowy domyślny rozmiar jednostki MTU interfejsu Ethernet na routerze. Jeśli router domyślnie ma inny rozmiar jednostki MTU, w nie mają toospecify nie konieczności wartości hello interfejs routera.
* W przeciwieństwie do bramy sieci VPN Azure hello TCP MSS dla obwodu usługi ExpressRoute nie jest konieczne toobe określony.

Poniższe przykłady konfiguracji routera mają zastosowanie tooall komunikacji równorzędnych. Przegląd [komunikacji równorzędnych ExpressRoute](expressroute-circuit-peerings.md) i [wymagania dotyczące routingu usługi ExpressRoute](expressroute-routing.md) uzyskać więcej informacji o routingu.


## <a name="cisco-ios-xe-based-routers"></a>Cisco IOS-XE na podstawie routery
Hello próbek w tej sekcji dotyczą żadnych router, na którym uruchomiono rodziny systemów operacyjnych IOS XE hello.

### <a name="1-configuring-interfaces-and-sub-interfaces"></a>1. Konfigurowanie w interfejsach i podrzędne
Konieczne będzie tooMicrosoft połączyć z interfejsem sub na komunikację równorzędną w każdym router. Interfejs podsieci można zidentyfikować z Identyfikatorem sieci VLAN lub pary skumulowany identyfikatorów sieci VLAN i adresu IP.

**Definicja interfejsu Dot1Q**

W tym przykładzie przedstawiono definicję interfejsu podrzędnego hello interfejsu podrzędnego z jednego identyfikatora sieci VLAN. Identyfikator sieci VLAN Hello jest unikatowy dla komunikacji równorzędnej. Witaj oktet ostatniego adresu IPv4 zawsze jest liczbą nieparzystą.

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <VLAN_ID>
     ip address <IPv4_Address><Subnet_Mask>

**Definicja interfejsu QinQ**

W tym przykładzie przedstawiono definicję interfejsu podrzędnego hello interfejsu podrzędnego z dwóch identyfikatorów sieci VLAN. powitalne zewnętrzne identyfikator sieci VLAN (s-tag), jeśli używana jest hello sama we wszystkich hello komunikacji równorzędnych. wewnętrzny Hello identyfikator sieci VLAN (c znacznik) jest unikatowy dla komunikacji równorzędnej. Witaj oktet ostatniego adresu IPv4 zawsze jest liczbą nieparzystą.

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <s-tag> seconddot1Q <c-tag>
     ip address <IPv4_Address><Subnet_Mask>

### <a name="2-setting-up-ebgp-sessions"></a>2. Konfigurowanie sesji eBGP
Należy skonfigurować sesję protokołu BGP z firmy Microsoft dla każdej komunikacji równorzędnej. Poniższy przykład Hello umożliwia toosetup sesję protokołu BGP z firmą Microsoft. Jeśli hello adresu IPv4, który był używany dla interfejsu sub a.b.c.d, hello adres IP sąsiadów BGP hello (Microsoft) będzie a.b.c.d+1. ostatni oktet Hello adresu IPv4 sąsiadów BGP hello jest zawsze liczbą parzystą.

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
     neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="3-setting-up-prefixes-toobe-advertised-over-hello-bgp-session"></a>3. Konfigurowanie toobe prefiksów anonsowanych hello sesji BGP
Można skonfigurować tooMicrosoft Wybierz prefiksy tooadvertise Twojego router. Możesz to zrobić, za pomocą hello w poniższym przykładzie.

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
      network <Prefix_to_be_advertised> mask <Subnet_mask>
      neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="4-route-maps"></a>4. Mapuje trasy
Można użyć mapy trasy oraz prefiks listę prefiksów toofilter propagowane do sieci. Możesz użyć hello przykładu poniżej tooaccomplish hello zadania. Upewnij się, że Instalator wyświetla odpowiedni prefiks.

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


## <a name="juniper-mx-series-routers"></a>Routery serii juniper MX
Witaj próbek w tej sekcji dotyczą wszystkie routery serii Juniper MX.

### <a name="1-configuring-interfaces-and-sub-interfaces"></a>1. Konfigurowanie w interfejsach i podrzędne

**Definicja interfejsu Dot1Q**

W tym przykładzie przedstawiono definicję interfejsu podrzędnego hello interfejsu podrzędnego z jednego identyfikatora sieci VLAN. Identyfikator sieci VLAN Hello jest unikatowy dla komunikacji równorzędnej. Witaj oktet ostatniego adresu IPv4 zawsze jest liczbą nieparzystą.

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


**Definicja interfejsu QinQ**

W tym przykładzie przedstawiono definicję interfejsu podrzędnego hello interfejsu podrzędnego z dwóch identyfikatorów sieci VLAN. powitalne zewnętrzne identyfikator sieci VLAN (s-tag), jeśli używana jest hello sama we wszystkich hello komunikacji równorzędnych. wewnętrzny Hello identyfikator sieci VLAN (c znacznik) jest unikatowy dla komunikacji równorzędnej. Witaj oktet ostatniego adresu IPv4 zawsze jest liczbą nieparzystą.

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

### <a name="2-setting-up-ebgp-sessions"></a>2. Konfigurowanie sesji eBGP
Należy skonfigurować sesję protokołu BGP z firmy Microsoft dla każdej komunikacji równorzędnej. Poniższy przykład Hello umożliwia toosetup sesję protokołu BGP z firmą Microsoft. Jeśli hello adresu IPv4, który był używany dla interfejsu sub a.b.c.d, hello adres IP sąsiadów BGP hello (Microsoft) będzie a.b.c.d+1. ostatni oktet Hello adresu IPv4 sąsiadów BGP hello jest zawsze liczbą parzystą.

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

### <a name="3-setting-up-prefixes-toobe-advertised-over-hello-bgp-session"></a>3. Konfigurowanie toobe prefiksów anonsowanych hello sesji BGP
Można skonfigurować tooMicrosoft Wybierz prefiksy tooadvertise Twojego router. Możesz to zrobić, za pomocą hello w poniższym przykładzie.

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


### <a name="4-route-maps"></a>4. Mapuje trasy
Można użyć mapy trasy oraz prefiks listę prefiksów toofilter propagowane do sieci. Możesz użyć hello przykładu poniżej tooaccomplish hello zadania. Upewnij się, że Instalator wyświetla odpowiedni prefiks.

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

## <a name="next-steps"></a>Następne kroki
Zobacz hello [ExpressRoute — często zadawane pytania](expressroute-faqs.md) więcej szczegółów.

