---
title: "Przykłady konfiguracji routera klienta aaaExpressRoute | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera przykłady konfiguracji routera dla routerów Cisco i Juniper."
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: d6ea716f-d5ee-4a61-92b0-640d6e7d6974
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/10/2016
ms.author: cherylmc
ms.openlocfilehash: b5faca0666bda6173e54abb0b6560d5f8bf8bfc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="router-configuration-samples-tooset-up-and-manage-nat"></a><span data-ttu-id="406cb-103">Konfiguracja routera przykłady tooset się i zarządzanie nimi translatora adresów Sieciowych</span><span class="sxs-lookup"><span data-stu-id="406cb-103">Router configuration samples tooset up and manage NAT</span></span>
<span data-ttu-id="406cb-104">Ta strona zawiera przykłady konfiguracji translatora adresów Sieciowych dla Cisco ASA i Juniper SRX routery serii.</span><span class="sxs-lookup"><span data-stu-id="406cb-104">This page provides NAT configuration samples for Cisco ASA and Juniper SRX series routers.</span></span> <span data-ttu-id="406cb-105">Służą one przykłady toobe przeznaczone tylko do celów informacyjnych i nie mogą być używane, ponieważ jest.</span><span class="sxs-lookup"><span data-stu-id="406cb-105">These are intended toobe samples for guidance only and must not be used as is.</span></span> <span data-ttu-id="406cb-106">Można pracować z toocome Twojego dostawcy z konfiguracjami odpowiednie dla danej sieci.</span><span class="sxs-lookup"><span data-stu-id="406cb-106">You can work with your vendor toocome up with appropriate configurations for your network.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="406cb-107">Przykłady na tej stronie są toobe przeznaczone wyłącznie w celu uzyskania wskazówek.</span><span class="sxs-lookup"><span data-stu-id="406cb-107">Samples in this page are intended toobe purely for guidance.</span></span> <span data-ttu-id="406cb-108">Należy skontaktować się z zespołu sprzedaży / techniczne z dostawcą i Twojej sieci toocome zespołu się z odpowiedniej konfiguracji toomeet potrzeb.</span><span class="sxs-lookup"><span data-stu-id="406cb-108">You must work with your vendor's sales / technical team and your networking team toocome up with appropriate configurations toomeet your needs.</span></span> <span data-ttu-id="406cb-109">Microsoft nie będzie obsługiwał problemy związane z tooconfigurations wymienione na tej stronie.</span><span class="sxs-lookup"><span data-stu-id="406cb-109">Microsoft will not support issues related tooconfigurations listed in this page.</span></span> <span data-ttu-id="406cb-110">Należy się z dostawcą urządzenia pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="406cb-110">You must contact your device vendor for support issues.</span></span>
> 
> 

* <span data-ttu-id="406cb-111">Poniższe przykłady konfiguracji routera mają zastosowanie tooAzure komunikacji równorzędnych publicznego i firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="406cb-111">Router configuration samples below apply tooAzure Public and Microsoft peerings.</span></span> <span data-ttu-id="406cb-112">Nie należy skonfigurować translatora adresów Sieciowych dla platformy Azure prywatnej komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="406cb-112">You must not configure NAT for Azure private peering.</span></span> <span data-ttu-id="406cb-113">Przegląd [komunikacji równorzędnych ExpressRoute](expressroute-circuit-peerings.md) i [wymagania ExpressRoute NAT](expressroute-nat.md) więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="406cb-113">Review [ExpressRoute peerings](expressroute-circuit-peerings.md) and [ExpressRoute NAT requirements](expressroute-nat.md) for more details.</span></span>

* <span data-ttu-id="406cb-114">Należy użyć oddzielnego pul IP translatora adresów Sieciowych dla toohello połączenie internetowe i ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="406cb-114">You MUST use separate NAT IP pools for connectivity toohello internet and ExpressRoute.</span></span> <span data-ttu-id="406cb-115">Za pomocą hello puli sam IP translatora adresów Sieciowych między hello internet i ExpressRoute spowoduje asymetrycznego routingu i utratę łączności.</span><span class="sxs-lookup"><span data-stu-id="406cb-115">Using hello same NAT IP pool across hello internet and ExpressRoute will result in asymmetric routing and loss of connectivity.</span></span>


## <a name="cisco-asa-firewalls"></a><span data-ttu-id="406cb-116">Cisco ASA zapór</span><span class="sxs-lookup"><span data-stu-id="406cb-116">Cisco ASA firewalls</span></span>
### <a name="pat-configuration-for-traffic-from-customer-network-toomicrosoft"></a><span data-ttu-id="406cb-117">PAWEŁ konfiguracji dla ruchu z tooMicrosoft sieci klienta</span><span class="sxs-lookup"><span data-stu-id="406cb-117">PAT configuration for traffic from customer network tooMicrosoft</span></span>
    object network MSFT-PAT
      range <SNAT-START-IP> <SNAT-END-IP>


    object-group network MSFT-Range
      network-object <IP> <Subnet_Mask>

    object-group network on-prem-range-1
      network-object <IP> <Subnet-Mask>

    object-group network on-prem-range-2
      network-object <IP> <Subnet-Mask>

    object-group network on-prem
      network-object object on-prem-range-1
      network-object object on-prem-range-2

    nat (outside,inside) source dynamic on-prem pat-pool MSFT-PAT destination static MSFT-Range MSFT-Range

### <a name="pat-configuration-for-traffic-from-microsoft-toocustomer-network"></a><span data-ttu-id="406cb-118">Konfiguracja PAWEŁ ruch z sieci toocustomer firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="406cb-118">PAT configuration for traffic from Microsoft toocustomer network</span></span>

<span data-ttu-id="406cb-119">**Interfejsy i kierunek:**</span><span class="sxs-lookup"><span data-stu-id="406cb-119">**Interfaces and Direction:**</span></span>

    Source Interface (where hello traffic enters hello ASA): inside
    Destination Interface (where hello traffic exits hello ASA): outside

<span data-ttu-id="406cb-120">**Konfiguracja:**</span><span class="sxs-lookup"><span data-stu-id="406cb-120">**Configuration:**</span></span>

<span data-ttu-id="406cb-121">Pula translacji adresów Sieciowych:</span><span class="sxs-lookup"><span data-stu-id="406cb-121">NAT Pool:</span></span>

    object network outbound-PAT
        host <NAT-IP>

<span data-ttu-id="406cb-122">Serwer docelowy:</span><span class="sxs-lookup"><span data-stu-id="406cb-122">Target Server:</span></span>

    object network Customer-Network
        network-object <IP> <Subnet-Mask>

<span data-ttu-id="406cb-123">Grupy obiektów dla adresów IP klienta</span><span class="sxs-lookup"><span data-stu-id="406cb-123">Object Group for Customer IP Addresses</span></span>

    object-group network MSFT-Network-1
        network-object <MSFT-IP> <Subnet-Mask>

    object-group network MSFT-PAT-Networks
        network-object object MSFT-Network-1

<span data-ttu-id="406cb-124">Polecenia translatora adresów Sieciowych:</span><span class="sxs-lookup"><span data-stu-id="406cb-124">NAT Commands:</span></span>

    nat (inside,outside) source dynamic MSFT-PAT-Networks pat-pool outbound-PAT destination static Customer-Network Customer-Network


## <a name="juniper-srx-series-routers"></a><span data-ttu-id="406cb-125">Juniper SRX serii routery</span><span class="sxs-lookup"><span data-stu-id="406cb-125">Juniper SRX series routers</span></span>
### <a name="1-create-redundant-ethernet-interfaces-for-hello-cluster"></a><span data-ttu-id="406cb-126">1. Tworzenie nadmiarowych interfejsów Ethernet hello klastra</span><span class="sxs-lookup"><span data-stu-id="406cb-126">1. Create redundant Ethernet interfaces for hello cluster</span></span>
    interfaces {
        reth0 {
            description "tooInternal Network";
            vlan-tagging;
            redundant-ether-options {
                redundancy-group 1;
            }
            unit 100 {
                vlan-id 100;
                family inet {
                    address <IP-Address/Subnet-mask>;
                }
            }
        }
        reth1 {
            description "tooMicrosoft via Edge Router";
            vlan-tagging;
            redundant-ether-options {
                redundancy-group 2;
            }
            unit 100 {
                description "tooMicrosoft via Edge Router";
                vlan-id 100;
                family inet {
                    address <IP-Address/Subnet-mask>;
                }
            }
        }
    }


### <a name="2-create-two-security-zones"></a><span data-ttu-id="406cb-127">2. Utwórz dwie strefy zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="406cb-127">2. Create two security zones</span></span>
* <span data-ttu-id="406cb-128">Zaufania strefy do sieci wewnętrznej i niezaufanej sieci zewnętrznych ukierunkowane routery brzegowe</span><span class="sxs-lookup"><span data-stu-id="406cb-128">Trust Zone for internal network and Untrust Zone for external network facing Edge Routers</span></span>
* <span data-ttu-id="406cb-129">Przypisz odpowiednich interfejsów toohello stref</span><span class="sxs-lookup"><span data-stu-id="406cb-129">Assign appropriate interfaces toohello zones</span></span>
* <span data-ttu-id="406cb-130">Zezwalaj usługom na powitania interfejsów</span><span class="sxs-lookup"><span data-stu-id="406cb-130">Allow services on hello interfaces</span></span>

    <span data-ttu-id="406cb-131">zabezpieczeń strefy {{zaufania strefy zabezpieczeń {hosta-— ruch przychodzący {systemu services {ping;                   } protokołów {bgp;                   interfejsy}} {reth0.100;               {}} niezaufanej strefy zabezpieczeń {hosta-— ruch przychodzący {systemu services {ping;                   } protokołów {bgp;                   interfejsy}} {reth1.100;               }           }       }   }</span><span class="sxs-lookup"><span data-stu-id="406cb-131">security {       zones {           security-zone Trust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth0.100;               }           }           security-zone Untrust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth1.100;               }           }       }   }</span></span>


### <a name="3-create-security-policies-between-zones"></a><span data-ttu-id="406cb-132">3. Tworzenie zasad zabezpieczeń między strefami</span><span class="sxs-lookup"><span data-stu-id="406cb-132">3. Create security policies between zones</span></span>
    security {
        policies {
            from-zone Trust to-zone Untrust {
                policy allow-any {
                    match {
                        source-address any;
                        destination-address any;
                        application any;
                    }
                    then {
                        permit;
                    }
                }
            }
            from-zone Untrust to-zone Trust {
                policy allow-any {
                    match {
                        source-address any;
                        destination-address any;
                        application any;
                    }
                    then {
                        permit;
                    }
                }
            }
        }
    }


### <a name="4-configure-nat-policies"></a><span data-ttu-id="406cb-133">4. Konfigurowanie zasad translatora adresów Sieciowych</span><span class="sxs-lookup"><span data-stu-id="406cb-133">4. Configure NAT policies</span></span>
* <span data-ttu-id="406cb-134">Utwórz dwie pule translatora adresów Sieciowych.</span><span class="sxs-lookup"><span data-stu-id="406cb-134">Create two NAT pools.</span></span> <span data-ttu-id="406cb-135">Microsoft toohello klienta będzie używane tooNAT ruchu wychodzącego tooMicrosoft i inne.</span><span class="sxs-lookup"><span data-stu-id="406cb-135">One will be used tooNAT traffic outbound tooMicrosoft and other from Microsoft toohello customer.</span></span>
* <span data-ttu-id="406cb-136">Tworzenie reguł ruchu odpowiednich hello tooNAT</span><span class="sxs-lookup"><span data-stu-id="406cb-136">Create rules tooNAT hello respective traffic</span></span>
  
       security {
           nat {
               source {
                   pool SNAT-To-ExpressRoute {
                       routing-instance {
                           External-ExpressRoute;
                       }
                       address {
                           <NAT-IP-address/Subnet-mask>;
                       }
                   }
                   pool SNAT-From-ExpressRoute {
                       routing-instance {
                           Internal;
                       }
                       address {
                           <NAT-IP-address/Subnet-mask>;
                       }
                   }
                   rule-set Outbound_NAT {
                       from routing-instance Internal;
                       toorouting-instance External-ExpressRoute;
                       rule SNAT-Out {
                           match {
                               source-address 0.0.0.0/0;
                           }
                           then {
                               source-nat {
                                   pool {
                                       SNAT-To-ExpressRoute;
                                   }
                               }
                           }
                       }
                   }
                   rule-set Inbound-NAT {
                       from routing-instance External-ExpressRoute;
                       toorouting-instance Internal;
                       rule SNAT-In {
                           match {
                               source-address 0.0.0.0/0;
                           }
                           then {
                               source-nat {
                                   pool {
                                       SNAT-From-ExpressRoute;
                                   }
                               }
                           }
                       }
                   }
               }
           }
       }

### <a name="5-configure-bgp-tooadvertise-selective-prefixes-in-each-direction"></a><span data-ttu-id="406cb-137">5. Skonfiguruj prefiksy selektywne tooadvertise protokołu BGP w każdym kierunku</span><span class="sxs-lookup"><span data-stu-id="406cb-137">5. Configure BGP tooadvertise selective prefixes in each direction</span></span>
<span data-ttu-id="406cb-138">Zobacz toosamples w [przykłady konfiguracji Routing ](expressroute-config-samples-routing.md) strony.</span><span class="sxs-lookup"><span data-stu-id="406cb-138">Refer toosamples in [Routing configuration samples ](expressroute-config-samples-routing.md) page.</span></span>

### <a name="6-create-policies"></a><span data-ttu-id="406cb-139">6. Tworzenie zasad</span><span class="sxs-lookup"><span data-stu-id="406cb-139">6. Create policies</span></span>
    routing-options {
                  autonomous-system <Customer-ASN>;
    }
    policy-options {
        prefix-list Microsoft-Prefixes {
            <IP-Address/Subnet-Mask;
            <IP-Address/Subnet-Mask;
        }
        prefix-list private-ranges {
            10.0.0.0/8;
            172.16.0.0/12;
            192.168.0.0/16;
            100.64.0.0/10;
        }
        policy-statement Advertise-NAT-Pools {
            from {
                protocol static;
                route-filter <NAT-Pool-Address/Subnet-mask> prefix-length-range /32-/32;
            }
            then accept;
        }
        policy-statement Accept-from-Microsoft {
            term 1 {
                from {
                    instance External-ExpressRoute;
                    prefix-list-filter Microsoft-Prefixes orlonger;
                }
                then accept;
            }
            term deny {
                then reject;
            }
        }
        policy-statement Accept-from-Internal {
            term no-private {
                from {
                    instance Internal;
                    prefix-list-filter private-ranges orlonger;
                }
                then reject;
            }
            term bgp {
                from {
                    instance Internal;
                    protocol bgp;
                }
                then accept;
            }
            term deny {
                then reject;
            }
        }
    }
    routing-instances {
        Internal {
            instance-type virtual-router;
            interface reth0.100;
            routing-options {
                static {
                    route <NAT-Pool-IP-Address/Subnet-mask> discard;
                }
                instance-import Accept-from-Microsoft;
            }
            protocols {
                bgp {
                    group customer {
                        export <Advertise-NAT-Pools>;
                        peer-as <Customer-ASN-1>;
                        neighbor <BGP-Neighbor-IP-Address>;
                    }
                }
            }
        }
        External-ExpressRoute {
            instance-type virtual-router;
            interface reth1.100;
            routing-options {
                static {
                    route <NAT-Pool-IP-Address/Subnet-mask> discard;
                }
                instance-import Accept-from-Internal;
            }
            protocols {
                bgp {
                    group edge-router {
                        export <Advertise-NAT-Pools>;
                        peer-as <Customer-Public-ASN>;
                        neighbor <BGP-Neighbor-IP-Address>;
                    }
                }
            }
        }
    }

## <a name="next-steps"></a><span data-ttu-id="406cb-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="406cb-140">Next steps</span></span>
<span data-ttu-id="406cb-141">Zobacz hello [ExpressRoute — często zadawane pytania](expressroute-faqs.md) więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="406cb-141">See hello [ExpressRoute FAQ](expressroute-faqs.md) for more details.</span></span>

