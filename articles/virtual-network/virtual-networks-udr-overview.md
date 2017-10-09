---
title: "trasy zdefiniowane przez aaaUser i przesyłania dalej protokołu IP na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak trasy zdefiniowane przez użytkownika tooconfigure (przez) i przesyłania dalej protokołu IP tooforward ruchu toonetwork urządzeń wirtualnych na platformie Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: c39076c4-11b7-4b46-a904-817503c4b486
ms.service: virtual-network
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f1f1d46166d5a7c776f472b7ade1354d943ece10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="user-defined-routes-and-ip-forwarding"></a>Trasy zdefiniowane przez użytkownika i przekazywanie adresów IP

Po dodaniu maszynach wirtualnych (VM) tooa sieć wirtualną (VNet) na platformie Azure można zauważyć maszyn wirtualnych hello automatycznie są możliwe toocommunicate ze sobą za pośrednictwem sieci hello. Nie trzeba toospecify bramy, nawet jeśli hello maszyn wirtualnych znajdują się w różnych podsieciach. Witaj dotyczy to także komunikacji z toohello maszyn wirtualnych hello publicznego Internetu i sieci lokalnej tooyour nawet gdy połączenie hybrydowe z platformy Azure tooyour własnych centrum danych jest obecny.

Taki przepływ komunikacji jest możliwa, ponieważ Azure korzysta z szeregu toodefine trasy systemu sposób przepływu ruchu w sieci IP. Trasy systemowe sterują przepływem hello komunikacji hello następujące scenariusze:

* Z poziomu hello tej samej podsieci.
* Z tooanother podsieci w sieci wirtualnej.
* Z maszyn wirtualnych toohello Internet.
* Z sieci wirtualnej tooanother sieci wirtualnej za pośrednictwem bramy sieci VPN.
* Z tooanother sieci wirtualnej sieci wirtualnej za pośrednictwem sieci wirtualnej komunikacji równorzędnej (łańcucha usługi).
* Z sieci wirtualnej sieci lokalnej tooyour za pośrednictwem bramy sieci VPN.

na poniższym rysunku Hello przedstawiono prostą konfigurację obejmującą sieć wirtualną, dwie podsieci i kilka maszyn wirtualnych wraz z hello tras systemowych, umożliwiających tooflow ruchu IP.

![Trasy systemowe platformy Azure](./media/virtual-networks-udr-overview/Figure1.png)

Chociaż hello korzystanie z tras systemowych umożliwia ruch sieciowy automatycznie w danym wdrożeniu, istnieją przypadki, w których chcesz toocontrol hello routingiem pakietów przez urządzenie wirtualne. Można więc tworząc trasy zdefiniowane przez użytkownika, który określisz hello następnego skoku dla pakietów przepływających zamiast tego urządzenia wirtualnego toogo tooyour tooa określonej podsieci i włączenie IP hello przesyłania dalej dla maszyny Wirtualnej uruchomionej jako urządzenie wirtualne hello.

Hello na poniższej ilustracji przedstawiono przykład tras zdefiniowanych przez użytkownika i przesyłania pakietów tooforce IP wysyłane tooone podsieci z innego toogo przez urządzenie wirtualne w trzeciej podsieci.

![Trasy systemowe platformy Azure](./media/virtual-networks-udr-overview/Figure2.png)

> [!IMPORTANT]
> Trasy zdefiniowane przez użytkownika są stosowane tootraffic wychodzącego z podsieci z wszystkich zasobów (takich jak interfejsów sieciowych dołączonych tooVMs) w podsieci hello. Nie można utworzyć trasy toospecify jak ruchu wprowadza podsieci hello Internetu, na przykład. urządzenia Hello przesyłasz toocannot ruchu należeć hello tej samej podsieci, w których pochodzą hello ruchu. Dla urządzeń zawsze należy utworzyć oddzielne podsieci. 
> 
> 

## <a name="route-resource"></a>Zasób trasy
Pakiety są przesyłane za pośrednictwem sieci TCP/IP w oparciu o tabelę tras zdefiniowaną w każdym węźle w sieci fizycznej hello. Tabela tras jest kolekcją indywidualnych tras używane toodecide gdzie tooforward pakiety na podstawie hello docelowy adres IP. Trasa składa się z następujących hello:

| Właściwość | Opis | Ograniczenia | Zagadnienia do rozważenia |
| --- | --- | --- | --- |
| Przedrostek adresu |dotyczy Hello docelowego CIDR toowhich hello trasa, na przykład 10.1.0.0/16. |Musi być prawidłowy zakres CIDR reprezentujący adresy w hello publicznej sieci Internet, sieci wirtualnej platformy Azure lub lokalnego centrum danych. |Upewnij się, że hello **prefiks adresu** nie zawiera adresu hello hello **następnego przeskoku**, w przeciwnym razie pakiety wpadną w pętlę, przechodząc od źródła hello toohello następnego przeskoku nigdy nie docierając Lokalizacja docelowa Hello. |
| Typ następnego skoku |Typ Hello pakietów hello Azure przeskoku powinny być przesyłane do. |Musi mieć jedną z hello następujące wartości: <br/> **Sieć wirtualna** Reprezentuje lokalną sieć wirtualną hello. Na przykład, jeśli masz dwie podsieci 10.1.0.0/16 i 10.2.0.0/16 w tej samej sieci wirtualnej hello, hello trasa dla każdej podsieci w tabeli tras hello będzie mieć wartość następnego skoku z *sieci wirtualnej*. <br/> **Brama sieci wirtualnej** Reprezentuje usługę Azure S2S VPN Gateway. <br/> **Internet**. Reprezentuje hello domyślną bramę sieci Internet podał hello infrastruktury platformy Azure. <br/> **Urządzenie wirtualne**. Reprezentuje urządzenie wirtualne dodane tooyour sieci wirtualnej platformy Azure. <br/> **Brak**. Reprezentuje czarną dziurę. Pakiety przesyłane dalej tooa czarnej dziury nie zostaną w ogóle przekazane. |Należy rozważyć użycie **urządzenie wirtualne** toodirect ruchu tooa maszyny Wirtualnej lub usługi równoważenia obciążenia Azure wewnętrznego adresu IP.  Tego typu umożliwia hello Specyfikacja adresu IP, zgodnie z poniższym opisem. Należy rozważyć użycie **Brak** wpisz toostop pakiety z przechodzenia tooa danego przeznaczenia. |
| Adres następnego skoku |adres następnego przeskoku Hello zawiera hello adres IP, które powinny zostać przekazane pakiety. Wartości następnego skoku są dozwolone tylko w przypadku tras, których typ następnego przeskoku hello jest *urządzenie wirtualne*. |Musi być adresem IP, który jest dostępny w sieci wirtualnej, w których stosowane hello trasy zdefiniowane przez użytkownika, bez pośrednictwa hello **Brama sieci wirtualnej**. adres IP Hello ma toobe hello wirtualne w tej samej sieci, jeśli jest ono stosowane lub peered sieci wirtualnej. |Jeśli hello adres IP reprezentuje Maszynę wirtualną, upewnij się, możesz włączyć [przesyłanie dalej IP](#IP-forwarding) Azure hello maszyny Wirtualnej. Jeśli hello IP adres reprezentuje hello wewnętrzny adres IP usługi równoważenia obciążenia Azure, upewnij się, że masz dopasowywania reguły dla każdego portu równoważenia obciążenia mają tooload równowagi.|

W programie Azure PowerShell niektóre wartości "Typ następnego przeskoku" hello mają różne nazwy elementu:

* Sieć wirtualna to VnetLocal,
* Brama sieci wirtualnej to VirtualNetworkGateway,
* Urządzenie wirtualne to VirtualAppliance,
* Internet to Internet
* Brak to None.

### <a name="system-routes"></a>Trasy systemowe
Każda podsieć utworzona w sieci wirtualnej jest automatycznie kojarzony z tabeli tras, która zawiera następujące reguły dotyczące tras systemowych hello:

* **Reguła lokalnej sieci wirtualnej**: ta reguła jest tworzona automatycznie dla każdej podsieci w sieci wirtualnej. Określa, że istnieje bezpośrednie połączenie między maszynami wirtualnymi hello w hello sieci wirtualnej i żadnego pośredniego następnego skoku nie istnieje.
* **Reguła lokalna**: Ta reguła stosuje się zakres adresów lokalnych toohello ruch kierowany tooall i używa bramy sieci VPN jako miejsca docelowego hello następnego skoku.
* **Reguła sieci Internet**: Ta reguła obsługuje wszystkie toohello ruch kierowany publicznej sieci Internet (0.0.0.0/0 prefiks adresu) i bramą internetową infrastruktury hello używa jako hello następnego przeskoku dla wszystkich toohello ruch kierowany Internet.

### <a name="user-defined-routes"></a>Trasy definiowane przez użytkownika
Dla większości środowisk wystarczy hello trasy systemowe zdefiniowane już przez platformę Azure. Można jednak konieczne toocreate tabelę tras i dodać co najmniej jednej trasy w szczególnych przypadkach, takich jak:

* Wymuszanie tunelowania toohello Internet za pośrednictwem sieci lokalnej.
* Korzystanie z urządzeń lokalnych w środowisku platformy Azure.

W powyższych scenariuszy hello będzie mieć toocreate tabelę tras i dodać tooit trasy zdefiniowane przez użytkownika. Może występować wiele tabel tras i hello sama tabela może być skojarzony tooone lub więcej podsieci. A każda podsieć może być tylko skojarzona tooa jedną tabelą tras. Wszystkie maszyny wirtualne i usługi w chmurze w podsieci użyć hello trasy tabeli skojarzonej toothat podsieci.

Korzysta ona z tras systemowych do momentu tabelę tras jest toohello skojarzonych podsieci. Jeśli skojarzenie istnieje, routing odbywa się w oparciu o najdłuższe dopasowanie prefiksu (Longest Prefix Match, LPM) wybierane spośród tras definiowanych przez użytkownika i tras systemowych. Jeśli istnieje więcej niż jedna trasa z hello LPM tego samego odpowiada, a następnie, wybór trasy odbywa się w następującej kolejności hello:

1. Trasa zdefiniowana przez użytkownika
2. Trasa protokołu BGP (jeśli używane są połączenia ExpressRoute)
3. Trasa systemowa

toolearn trasy zdefiniowane przez użytkownika toocreate zobacz [jak tooCreate tras i włączanie przesyłania dalej IP na platformie Azure](virtual-network-create-udr-arm-template.md).

> [!IMPORTANT]
> Trasy zdefiniowane przez użytkownika są tylko zastosowane tooAzure maszyn wirtualnych i usług w chmurze. Na przykład chcąc tooadd urządzenie wirtualne zapory między siecią lokalną a Azure, trzeba będzie toocreate trasy zdefiniowanej przez użytkownika dla tabel tras platformy przekazujący całego ruchu kierowanego toohello przestrzeni adresów lokalnych toohello wirtualnego urządzenia. Można również dodać zdefiniowany przez użytkownika tras (przez) toohello GatewaySubnet tooforward cały ruch z lokalnymi tooAzure za pośrednictwem hello urządzenie wirtualne. Ta możliwość została ostatnio dodana.
> 
> 

### <a name="bgp-routes"></a>Trasy protokołu BGP
Jeśli masz połączenie ExpressRoute między siecią lokalną a Azure, można włączyć trasy protokołu BGP toopropagate z Twojej tooAzure sieci lokalnej. Te trasy protokołu BGP są używane w hello trasy definiowane przez sam sposób jak tras systemowych i użytkownika w każdej podsieci platformy Azure. Więcej informacji można znaleźć w artykule [ExpressRoute — wprowadzenie](../expressroute/expressroute-introduction.md).

> [!IMPORTANT]
> Istnieje możliwość skonfigurowania tunelowania przez sieć lokalną, tworząc trasy zdefiniowane przez użytkownika dla podsieci 0.0.0.0/0, korzystającą z bramy sieci VPN hello jako hello następnego przeskoku działu toouse środowiska platformy Azure. Metoda ta działa jednak tylko w przypadku korzystania z bramy sieci VPN, a nie połączeń ExpressRoute. W przypadku połączeń ExpressRoute wymuszanie tunelowania jest konfigurowane za pomocą protokołu BGP.
> 
> 

## <a name="ip-forwarding"></a>Przekazywanie IP
Jak opisano powyżej, jednym toocreate głównych powodów hello trasy zdefiniowane przez użytkownika jest urządzenie wirtualne tooa tooforward ruchu. Urządzenie wirtualne jest tylko maszynę Wirtualną, która uruchamia ruchu sieciowego toohandle aplikacji używane w sposób, takie jak Zapora lub urządzenie NAT.

Ta maszyna wirtualna musi być możliwe tooreceive ruchu przychodzącego, który jest Nieuwzględnione tooitself. tooallow ruch tooreceive maszyn wirtualnych skierowana tooother miejsc docelowych, należy włączyć przesyłania dalej protokołu IP dla hello maszyny Wirtualnej. To ustawienie nie jest to ustawienie w systemie operacyjnym gościa hello Azure.

## <a name="next-steps"></a>Następne kroki
* Dowiedz się, jak za[tworzyć trasy w modelu wdrażania usługi Resource Manager hello](virtual-network-create-udr-arm-template.md) i kojarzyć je toosubnets. 
* Dowiedz się, jak za[tworzyć trasy w hello klasycznego modelu wdrażania](virtual-network-create-udr-classic-ps.md) i kojarzyć je toosubnets.

