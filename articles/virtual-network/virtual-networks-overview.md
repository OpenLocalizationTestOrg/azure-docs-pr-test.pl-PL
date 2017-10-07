---
title: aaaAzure sieci wirtualnej | Dokumentacja firmy Microsoft
description: "Więcej informacji na temat pojęć sieci wirtualnej platformy Azure i funkcje."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 9633de4b-a867-4ddf-be3c-a332edf02e24
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/23/2017
ms.author: jdial
ms.openlocfilehash: 55ae6a131d882ad893aeffcaa4127bc47beda552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-network"></a>Azure Virtual Network

Witaj umożliwia usługi sieci wirtualnej platformy Azure możesz toosecurely Uzyskuj dostęp do zasobów platformy Azure tooeach innych sieci wirtualnych (sieci wirtualne). Sieci wirtualnej jest reprezentację sieci w chmurze hello. Sieci wirtualnej jest logiczną izolacją hello subskrypcji tooyour chmury Azure w wersji dedykowanej. Można również połączyć sieć lokalną tooyour sieci wirtualnych. Witaj, na poniższej ilustracji przedstawiono niektóre możliwości hello hello Azure Virtual Network service:

![Diagram sieciowy](./media/virtual-networks-overview/virtual-network-overview.png)

toolearn więcej informacji na temat hello następujące możliwości sieci wirtualnej platformy Azure, kliknij hello możliwości:
- **[Izolacja:](#isolation)**  sieci wirtualne są odizolowane od siebie. Można utworzyć oddzielne sieci wirtualnych do tworzenia, testowania i produkcji tego hello Użyj tego samego bloków adresów CIDR. Z drugiej strony możesz utworzyć wiele sieci wirtualnych, użyj innego bloków adresów CIDR i połączyć ze sobą sieci. Sieć wirtualną można podzielić na wiele podsieci. Platforma Azure udostępnia rozpoznawania nazw wewnętrznych dla maszyn wirtualnych i wystąpień roli usługi w chmurze połączone tooa sieci wirtualnej. Opcjonalnie można skonfigurować toouse sieci wirtualnej własne serwery DNS, zamiast rozpoznawania nazw wewnętrznych platformy Azure.
- **[Połączenie z Internetem:](#internet)**  toohello Internet, domyślnie dostęp do wszystkich maszyn wirtualnych Azure (VM) i usługi w chmurze wystąpień roli ma tooa połączonych sieci wirtualnej. Można również włączyć dostęp do przychodzących toospecific zasobów, zgodnie z potrzebami.
- **[Łączność zasobów platformy Azure:](#within-vnet)**  zasobów platformy Azure, takich jak usługi w chmurze i maszyn wirtualnych może być połączone toohello tej samej sieci wirtualnej. Witaj zasobów mogą się łączyć tooeach innych używania prywatnych adresów IP, nawet jeśli znajdują się w różnych podsieciach. Platforma Azure udostępnia domyślny routing między podsieciami, sieci wirtualnych i sieci lokalnej, dlatego nie masz tooconfigure i Zarządzaj trasami.
- **[Łączność sieci wirtualnej:](#connect-vnets)**  sieci wirtualnych może być połączone tooeach innych, włączanie zasoby podłączone tooany toocommunicate sieci wirtualnej z dowolnego zasobu w innych sieci wirtualnej.
- **[Połączenie lokalne:](#connect-on-premises)**  sieci wirtualnych może być sieci lokalnych tooon połączonych za pośrednictwem sieci prywatnej połączeń między siecią a Azure lub za pośrednictwem połączenia sieci VPN typu lokacja lokacja za pośrednictwem hello Internet.
- **[Filtrowanie ruchu:](#filtering)**  ruchu sieciowego wystąpień roli maszyny Wirtualnej i usługi w chmurze można użyć do filtrowania ruchu przychodzącego i wychodzącego przez źródłowy adres IP i port docelowy adres IP i portu i protokołu.
- **[Routing:](#routing)**  można opcjonalnie zastąpić domyślne Azure routingu, konfigurowanie własnego trasy lub użyj trasy protokołu BGP za pośrednictwem bramy sieci.

## <a name = "isolation"></a>Izolacja sieci i segmentacji

Można zaimplementować wiele sieci wirtualnych w każdym Azure [subskrypcji](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription) i Azure [region](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#region). Każda sieć wirtualna jest odizolowana od innych sieci wirtualnych. Dla każdej sieci wirtualnej można:
- Określ niestandardowe prywatnych przestrzeni adresów IP przy użyciu prywatnych i publicznych adresów (RFC 1918). Azure przypisuje toohello połączonych zasobów sieci wirtualnej prywatnego adresu IP z hello przestrzeń adresów, które można przypisać.
- Segment hello sieci wirtualnej do co najmniej jednej podsieci i przydzielić część hello sieci wirtualnej adres miejsca tooeach podsieci.
- Korzystanie z rozpoznawania nazw platformy Azure lub Podaj własny serwer DNS do użytku przez zasoby podłączone tooa sieci wirtualnej. więcej informacji na temat rozpoznawania nazw w sieci wirtualnych, przeczytaj hello toolearn [rozpoznawanie nazw dla maszyn wirtualnych i usług w chmurze](virtual-networks-name-resolution-for-vms-and-role-instances.md) artykułu.

## <a name = "internet"></a>Połącz toohello Internet
Wszystkie zasoby tooa połączonych sieci wirtualnej mają łączność wychodząca toohello Internet domyślnie. Witaj prywatnego adresu IP zasobu hello jest adres sieciowy źródła przetłumaczyła publicznego adresu IP (SNAT) tooa hello infrastruktury platformy Azure. więcej informacji na temat wychodzące połączenie z Internetem, przeczytaj hello toolearn [Opis połączeń wychodzących na platformie Azure](..\load-balancer\load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json#standalone-vm-with-no-instance-level-public-ip-address) artykułu. Możesz zmienić hello domyślne łączności dzięki implementacji niestandardowego routingu i filtrowanie ruchu.

toocommunicate ruchu przychodzącego tooAzure zasobów z hello Internet lub toocommunicate toohello wychodzących, Internet bez SNAT, zasobu można przypisać do publicznego adresu IP. więcej informacji na temat publiczne adresy IP, przeczytaj hello toolearn [publicznego adresu IP, adresy](virtual-network-public-ip-address.md) artykułu.

## <a name="within-vnet"></a>Łączenie zasobów platformy Azure
Możesz połączyć kilka tooa zasobów Azure sieci wirtualnej, takie jak maszyn wirtualnych (VM), usługi w chmurze środowiska usługi App Service i zestawy skalowania maszyny wirtualnej. Maszyny wirtualne połączyć tooa podsieci w sieci wirtualnej za pośrednictwem interfejsu sieciowego (NIC). więcej informacji na temat kart sieciowych, przeczytaj hello toolearn [interfejsy sieciowe](virtual-network-network-interface.md) artykułu.

## <a name="connect-vnets"></a>Łączenie sieci wirtualnej

Możesz połączyć sieci wirtualnych tooeach innych, włączanie zasoby połączone toocommunicate sieci wirtualnej tooeither ze sobą za pośrednictwem sieci wirtualnych. Można użyć jednego lub obu hello następujące opcje tooconnect sieci wirtualnych tooeach inne:
- **Komunikacja równorzędna:** umożliwia zasoby podłączone toodifferent sieci wirtualnych platformy Azure w ramach hello tej samej lokalizacji platformy Azure toocommunicate ze sobą. Witaj przepustowości i opóźnień między hello sieci wirtualnych jest hello sam tak, jakby zasoby hello był połączony toohello tej samej sieci wirtualnej. toolearn więcej informacji na temat komunikacji równorzędnej, przeczytaj hello [równorzędna sieci wirtualnej](virtual-network-peering-overview.md) artykułu.
- **Połączenia do wirtualnymi:** umożliwia zasoby podłączone toodifferent sieci wirtualnej platformy Azure w ramach hello tej samej lub innej lokalizacji platformy Azure. W przeciwieństwie do komunikacji równorzędnej, przepustowości jest ograniczona między sieciami wirtualnymi, ponieważ ruch musi przepływać przez bramę sieci VPN platformy Azure. więcej informacji na temat łączenia sieci wirtualnych z połączeniem wirtualnymi do odczytu hello toolearn [skonfigurować połączenia do wirtualnymi](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artykułu.

## <a name="connect-on-premises"></a>Połączyć sieć lokalną tooan

Można połączyć z tooa sieci lokalnej sieci wirtualnej przy użyciu dowolnej kombinacji hello następujące opcje:
- **Punkt lokacja wirtualnej sieci prywatnej (VPN):** między jednej sieci połączonych tooyour PC i hello sieci wirtualnej. Tego typu połączenia jest doskonałym, jeśli tylko rozpoczniesz pracę z platformą Azure, lub dla deweloperów, ponieważ wymaga żadnych zmian tooyour istniejącej sieci. Hello połączenie korzysta z komunikacji tooprovide szyfrowane protokół SSTP hello za pośrednictwem hello Internet między hello PC i hello sieci wirtualnej. Opóźnienie Hello VPN punkt lokacja jest nieprzewidywalne, ponieważ hello ruch przechodzi hello Internet.
- **Sieć VPN lokacja lokacja:** między urządzenie sieci VPN i bramy sieci VPN platformy Azure. Ten typ połączenia pozwala dowolnego zasobu lokalnego autoryzować tooaccess sieci wirtualnej. połączenie Hello jest VPN IPSec i IKE, zapewniająca szyfrowaną komunikację za pośrednictwem hello Internet między urządzeniami lokalnymi i hello bramy sieci VPN platformy Azure. Opóźnienie Hello połączenia lokacja lokacja jest nieprzewidywalne, ponieważ hello ruch przechodzi hello Internet.
- **Usługa Azure ExpressRoute:** ustanowić między siecią a Azure, za pośrednictwem partner usługi ExpressRoute. To połączenie jest prywatne. Ruch omija hello Internet. Opóźnienie Hello połączenia ExpressRoute jest przewidywalne, ponieważ ruch nie przechodzenia hello Internet.

więcej informacji na temat wszystkich hello poprzedniej opcji połączenia, przeczytaj hello toolearn [Diagram topologii połączenia](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#diagrams) artykułu.

## <a name="filtering"></a>Filtrowanie ruchu sieciowego
Można filtrować ruch sieciowy między podsieciami przy użyciu jednego lub obu hello następujące opcje:
- **Sieciowe grupy zabezpieczeń (NSG):** każda grupa NSG może zawierać wiele reguł zabezpieczeń dla ruchu przychodzącego i wychodzącego umożliwiających toofilter ruch źródłowy i docelowy adres IP, portu i protokołu. Można stosować grupy NSG tooeach karty Sieciowej na maszynie wirtualnej. Można także zastosować grupy NSG podsieci toohello karty Sieciowej, lub innych zasobów platformy Azure jest połączona. więcej informacji na temat grup NSG, przeczytaj hello toolearn [sieciowej grupy zabezpieczeń](virtual-networks-nsg.md) artykułu.
- **Sieci wirtualne urządzenia (NVA):** NVA jest uruchomione oprogramowanie, które wykonuje funkcję sieci, takie jak Zapora maszyny Wirtualnej. Wyświetl listę dostępnych NVAs w hello [portalu Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/category/networking?page=1&subcategories=appliances). NVAs są również dostępne, które zapewniają funkcje ruchu Optymalizacja sieci WAN i innych sieci. NVAs zwykle są używane przez użytkownika lub trasy protokołu BGP. Można również użyć ruchu toofilter NVA między sieciami wirtualnymi.

## <a name="routing"></a>Kierować ruchem sieciowym

Platforma Azure tworzy tabele tras, umożliwiających podsieci tooany połączonych zasobów w dowolnej sieci wirtualnej toocommunicate ze sobą, domyślnie. Można zaimplementować jedną lub obie następujące opcje toooverride hello hello trasy domyślne, które tworzy Azure:
- **Trasy zdefiniowane przez użytkownika:** tworzenia tabel tras niestandardowych trasy, które kontrolują, których ruch jest kierowany toofor każdej podsieci. więcej informacji na temat trasy zdefiniowane przez użytkownika, odczytać hello toolearn [trasy zdefiniowane przez użytkownika](virtual-networks-udr-overview.md) artykułu.
- **Trasy protokołu BGP:** Jeśli połączyć sieci wirtualnej sieci lokalnej tooyour przy użyciu połączenia bramy sieci VPN platformy Azure lub usługi ExpressRoute, można propagować tooyour trasy protokołu BGP sieci wirtualnych.

## <a name="pricing"></a>Cennik

Jest bezpłatna dla sieci wirtualnych, podsieci, tabele tras lub sieciowej grupy zabezpieczeń. Wychodzące użycia przepustowości połączenia internetowego, publicznego adresu IP adresów sieci wirtualnej komunikacji równorzędnej, bram sieci VPN i ExpressRoute każdego mają swoje własne cennik struktury. Widok hello [sieci wirtualnej](https://azure.microsoft.com/pricing/details/virtual-network), [bramy sieci VPN](https://azure.microsoft.com/pricing/details/vpn-gateway), i [ExpressRoute](https://azure.microsoft.com/pricing/details/expressroute) cennik strony, aby uzyskać więcej informacji.

## <a name="faq"></a>Często zadawane pytania

tooreview często zadawane pytania dotyczące sieci wirtualnej, zobacz hello [często zadawane pytania dotyczące sieci wirtualnych](virtual-networks-faq.md) artykułu.


## <a name="next-steps"></a>Następne kroki

- Tworzenie pierwszej sieci wirtualnej i połączyć kilka tooit maszyn wirtualnych, wykonując kroki hello w hello [tworzenie pierwszej sieci wirtualnej](virtual-network-get-started-vnet-subnet.md) artykułu.
- Utwórz tooa połączenie punkt lokacja sieci wirtualnej, wykonując kroki hello hello [skonfigurować połączenie punkt lokacja](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artykułu.
- Dowiedz się więcej o niektórych hello innego klucza [sieci możliwości](../networking/networking-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json) platformy Azure.
