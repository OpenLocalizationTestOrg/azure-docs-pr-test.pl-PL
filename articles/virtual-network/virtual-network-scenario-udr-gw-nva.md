---
title: "aaaHybrid połączenia z aplikacji warstwy 2 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toodeploy urządzeń wirtualnych i przez toocreate środowisku wielowarstwową aplikację na platformie Azure"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 1f509bec-bdd1-470d-8aa4-3cf2bb7f6134
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/05/2016
ms.author: jdial
ms.openlocfilehash: 53599862289dbf9c6ab3289b0cb8dda6430f20f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-appliance-scenario"></a>Scenariusz urządzenie wirtualne
Typowy scenariusz większych klientów platformy Azure jest tooprovide potrzeby hello toohello dwuwarstwowej aplikacji widocznej Internet, umożliwiając warstwy dostępu toohello wstecz od lokalnego centrum danych. Ten dokument przeprowadzi użytkownika przy użyciu użytkownika zdefiniowanych tras przez, Brama sieci VPN i sieci wirtualnych urządzeń toodeploy scenariusza środowisku dwuwarstwowej, które spełnia następujące wymagania hello:

* Aplikacja sieci Web musi być dostępny z hello tylko publicznej sieci Internet.
* Aplikacja hello hostingu serwera sieci Web musi być w stanie tooaccess serwer aplikacji zaplecza.
* Cały ruch z aplikacji sieci web toohello internetowej hello musi przechodzić przez urządzenie wirtualne zapory. To urządzenie wirtualne będą używane tylko ruchu internetowego.
* Całego ruchu kierowanego toohello serwera aplikacji musi przechodzić przez urządzenie wirtualne zapory. Ta maszyna będzie służyć do serwera końcowego zaplecza toohello dostępu i odbierane z sieci lokalnej hello za pośrednictwem bramy sieci VPN dostępu.
* Administratorzy muszą być urządzenie wirtualne zapory hello stanie toomanage z ich komputerami lokalnymi, przy użyciu innej zapory używane wyłącznie do celów zarządzania urządzenie wirtualne.

Jest to standardowe scenariusz DMZ strefą DMZ i chronionej sieci. Taki scenariusz może być skonstruowany w Azure za pomocą grup NSG, urządzenie wirtualne zapory lub obie te grupy. Witaj w poniższej tabeli przedstawiono niektóre hello zalet i wad między grupy NSG oraz zapory urządzenia wirtualnego.

|  | Specjaliści | Wady |
| --- | --- | --- |
| GRUPA NSG |Bez kosztów. <br/>Zintegrowane usługi Azure RBAC. <br/>Reguły można tworzyć w szablonów ARM. |Złożoność może się różnić w większych środowiskach. |
| Zapora |Pełną kontrolę nad płaszczyzna danych. <br/>Centralne zarządzanie za pomocą konsoli zapory. |Koszt urządzenia zapory. <br/>Nie jest zintegrowany z Azure RBAC. |

rozwiązanie Hello poniżej używa tooimplement urządzenie wirtualne zapory scenariusza sieci DMZ/chronione.

## <a name="considerations"></a>Zagadnienia do rozważenia
Możesz wdrożyć środowiska hello przedstawionych powyżej na platformie Azure przy użyciu różnych funkcji dostępnych już dziś, wykonując następujące czynności.

* **Sieć wirtualną (VNet)**. Sieć wirtualną platformy Azure działa w podobny sposób tooan lokalnej sieci i być segmentem w co najmniej jeden izolacja ruchu tooprovide podsieci i separacji.
* **Urządzenie wirtualne**. Kilka partnerów Podaj urządzenie wirtualne w hello Azure Marketplace, używanej do hello zapór trzech opisanych powyżej. 
* **Zdefiniowane przez użytkownika tras (przez)**. Tabele tras może zawierać Udr używane przez usługi Azure networking toocontrol hello przepływu pakietów w sieci wirtualnej. Te tabele tras może być zastosowane toosubnets. Jedną z najnowszych funkcji hello na platformie Azure jest hello możliwości tooapply toohello tabeli tras GatewaySubnet, zapewniając tooforward możliwości hello cały ruch rozpoczynająca hello sieci wirtualnej platformy Azure z urządzenia wirtualnego tooa połączenia hybrydowego.
* **Przesyłanie dalej IP**. Domyślnie program hello Azure networking aparat przekazywać pakiety toovirtual karty sieciowe (NIC) tylko wtedy, gdy pakietów hello docelowy adres IP odpowiada hello adresu IP karty Sieciowej. W związku z tym jeśli przez definiuje, czy pakiet należy wysłać tooa podane urządzenie wirtualne, hello Azure networking aparat spowoduje pominięcie pakietu. tooensure pakietów hello jest dostarczany tooa maszyny Wirtualnej (w tym przypadku urządzenia wirtualnego), który nie jest hello rzeczywistego przeznaczenia dla pakietów hello, należy tooenable przesyłania dalej protokołu IP dla urządzenia wirtualnego hello.
* **Sieciowe grupy zabezpieczeń (NSG)**. w poniższym przykładzie Hello nie korzystają z grup NSG, ale można użyć grupy NSG stosowana toohello podsieci i/lub kart sieciowych w tym rozwiązania toofurther filtrować hello ruch do i z tych podsieci i karty sieciowe.

![Łączność IPv6](./media/virtual-network-scenario-udr-gw-nva/figure01.png)

W tym przykładzie jest subskrypcji, która zawiera następujące hello:

* 2 grup zasobów, nie są wyświetlane na diagramie hello. 
  * **ONPREMRG**. Zawiera wszystkie niezbędne zasoby toosimulate sieci lokalnej.
  * **AZURERG**. Zawiera wszystkie zasoby niezbędne do hello sieci wirtualnej platformy Azure środowiska. 
* Sieć wirtualną o nazwie **onpremvnet** używane toomimic lokalnego centrum danych segmentem wymienione poniżej.
  * **onpremsn1**. Podsieci zawierającej maszynę wirtualną (VM) systemem Ubuntu toomimic na serwerze lokalnym.
  * **onpremsn2**. Podsieć zawierająca maszyny Wirtualnej z systemem Ubuntu toomimic na komputerze lokalnym używane przez administratora.
* Brak co urządzenie wirtualne zapory o nazwie **OPFW** na **onpremvnet** używane zbyt toomaintain tunel**azurevnet**.
* Sieć wirtualną o nazwie **azurevnet** segmentowanych wymienione poniżej.
  * **azsn1**. Używane wyłącznie do zapory zewnętrznej hello podsieci zapory zewnętrznej. Cały ruch internetowy wejdzie do tej podsieci. Ta podsieć zawiera tylko zapory zewnętrznej toohello karta sieciowa jest połączona.
  * **azsn2**. Hosting maszyny Wirtualnej z systemem jako serwera sieci web, do której będą mieli dostęp z Internetu hello podsieci frontonu.
  * **azsn3**. Hosting maszyny Wirtualnej z systemem serwer aplikacji zaplecza, w której będą mieli dostęp przez serwer sieci web frontonu hello podsieci wewnętrznej bazy danych.
  * **azsn4**. Zarządzanie podsieć używana wyłącznie tooprovide zarządzania dostępu tooall wirtualnego urządzenia zapory. Ta podsieć zawiera tylko z kartą Sieciową dla każdego urządzenie wirtualne zapory używany w rozwiązaniu hello.
  * **GatewaySubnet**. Podsieć połączenia hybrydowe platformy Azure wymagane dla połączenia tooprovide ExpressRoute, jak i bramy sieci VPN między sieciami wirtualnymi platformy Azure i innych sieci. 
* Istnieją 3 urządzenie wirtualne zapory w hello **azurevnet** sieci. 
  * **AZF1**. Toohello zapory zewnętrznej widoczne publicznej sieci Internet za pomocą zasób publicznego adresu IP na platformie Azure. Należy tooensure ma szablonu z witryny Marketplace hello lub bezpośrednio z dostawcą urządzenia, że przepisy 3-NIC urządzenie wirtualne.
  * **AZF2**. Wewnętrzny zapory używane toocontrol ruch między **azsn2** i **azsn3**. Dotyczy to również 3-NIC urządzenie wirtualne.
  * **AZF3**. Zarządzanie zaporą dostępny tooadministrators z hello lokalnego centrum danych i połączonych tooa zarządzania podsieci używane toomanage wszystkie urządzenia zapory. Można znaleźć karty Sieciowej 2 Szablony urządzenie wirtualne w hello Marketplace, lub zażądać bezpośrednio z dostawcą urządzenia.

## <a name="user-defined-routing-udr"></a>Zdefiniowane przez użytkownika routingu (przez)
Każdej podsieci platformy Azure można toodefine tabeli używanej przez połączone tooa jak jest kierowany ruch zainicjowane w tej podsieci. Jeśli są zdefiniowane nie Udr, Azure korzysta z domyślnego tras tooallow ruch tooflow z jednej podsieci tooanother. toobetter zrozumieć Udr, odwiedź stronę [co to są trasy zdefiniowane przez użytkownika i przesyłania dalej protokołu IP](virtual-networks-udr-overview.md#ip-forwarding).

tooensure komunikacja odbywa się za pośrednictwem urządzenia zapory prawo hello, oparte na powitania ostatnie wymaganie powyżej, wymagają następujących hello toocreate zawierający Udr w tabeli tras **azurevnet**.

### <a name="azgwudr"></a>azgwudr
W tym scenariuszu hello ruchu wynikających z lokalnymi tooAzure będą używane toomanage hello zapór, nawiązując połączenie za tylko**AZF3**, i że ruchu musi przechodzić przez zaporę wewnętrznej hello, **AZF2**. W związku z tym w hello konieczne jest tylko jedna trasa **GatewaySubnet** jak pokazano poniżej.

| Element docelowy | Następny przeskok | Wyjaśnienie |
| --- | --- | --- |
| 10.0.4.0/24 |10.0.3.11 |Umożliwia lokalnymi ruchu tooreach zarządzania zapory **AZF3** |

### <a name="azsn2udr"></a>azsn2udr
| Element docelowy | Następny przeskok | Wyjaśnienie |
| --- | --- | --- |
| 10.0.3.0/24 |10.0.2.11 |Umożliwia podsieci wewnętrznej bazy danych toohello ruchu obsługującego serwer aplikacji hello za pośrednictwem **AZF2** |
| 0.0.0.0/0 |10.0.2.10 |Umożliwia innych toobe ruch kierowany przez **AZF1** |

### <a name="azsn3udr"></a>azsn3udr
| Element docelowy | Następny przeskok | Wyjaśnienie |
| --- | --- | --- |
| 10.0.2.0/24 |10.0.3.10 |Zezwala na ruch za**azsn2** tooflow z aplikacji serwera toohello serwer sieci Web za pośrednictwem **AZF2** |

Należy również toocreate tabel tras dla podsieci hello w **onpremvnet** toomimic hello lokalnego centrum danych.

### <a name="onpremsn1udr"></a>onpremsn1udr
| Element docelowy | Następny przeskok | Wyjaśnienie |
| --- | --- | --- |
| 192.168.2.0/24 |192.168.1.4 |Zezwala na ruch za**onpremsn2** za pośrednictwem **OPFW** |

### <a name="onpremsn2udr"></a>onpremsn2udr
| Element docelowy | Następny przeskok | Wyjaśnienie |
| --- | --- | --- |
| 10.0.3.0/24 |192.168.2.4 |Umożliwia podsieci toohello kopii ruchu na platformie Azure za pośrednictwem **OPFW** |
| 192.168.1.0/24 |192.168.2.4 |Zezwala na ruch za**onpremsn1** za pośrednictwem **OPFW** |

## <a name="ip-forwarding"></a>Przesyłanie dalej IP
PRZEZ i przekazywanie adresów IP są funkcje, których można używać w kombinacji tooallow urządzeń wirtualnych toobe używane toocontrol przepływ ruchu w sieci wirtualnej platformy Azure.  Urządzenie wirtualne jest tylko maszynę Wirtualną, która uruchamia ruchu sieciowego toohandle aplikacji używane w sposób, takie jak Zapora lub urządzenie NAT.

Ta maszyna wirtualna musi być możliwe tooreceive ruchu przychodzącego, który jest Nieuwzględnione tooitself. tooallow ruch tooreceive maszyn wirtualnych skierowana tooother miejsc docelowych, należy włączyć przesyłania dalej protokołu IP dla hello maszyny Wirtualnej. To ustawienie nie jest to ustawienie w systemie operacyjnym gościa hello Azure. Toorun potrzeb nadal Twoje urządzenie wirtualne niektóre typ toohandle aplikacji hello ruchu przychodzącego i kierowania go odpowiednio.

toolearn więcej informacji na temat przekazywania adresów IP, odwiedź stronę [co to są trasy zdefiniowane przez użytkownika i przesyłania dalej protokołu IP](virtual-networks-udr-overview.md#ip-forwarding).

Na przykład załóżmy, że masz powitania po zakończeniu instalacji w sieci wirtualnej platformy Azure:

* Podsieci **onpremsn1** zawiera maszynę Wirtualną o nazwie **onpremvm1**.
* Podsieci **onpremsn2** zawiera maszynę Wirtualną o nazwie **onpremvm2**.
* Urządzenie wirtualne o nazwie **OPFW** jest połączony za**onpremsn1** i **onpremsn2**.
* Trasy zdefiniowane przez użytkownika są połączone za**onpremsn1** Określa, że cały ruch zbyt**onpremsn2** musi zostać wysłany**OPFW**.

W tym momencie Jeśli **onpremvm1** próbuje tooestablish połączenia z **onpremvm2**, hello przez będą używane i ruch wysyłany jest zbyt**OPFW** jako hello następnego przeskoku. Należy pamiętać o tym, które hello miejsca docelowego rzeczywiste pakietu nie został zmieniony, nadal wyświetlany jest tekst **onpremvm2** jest miejscem docelowym hello. 

Bez przesyłania dalej protokołu IP włączone dla **OPFW**, hello Azure logiki sieci wirtualnych spowoduje porzucenie pakietów hello, ponieważ pozwala jedynie pakiety wysyłane toobe tooa wirtualna Jeśli hello adres IP maszyny Wirtualnej jest miejscem docelowym hello hello pakietu.

Z przesyłania dalej protokołu IP hello logiki sieci wirtualnej platformy Azure będzie przesyłać tooOPFW pakietów hello, bez zmiany jego oryginalny adres docelowy. **OPFW** musi obsługiwać pakietów hello i ustalić, jakie toodo z nimi.

W scenariuszu hello powyżej toowork, należy włączyć przesyłania dalej protokołu IP kart sieciowych hello dla **OPFW**, **AZF1**, **AZF2**, i **AZF3** służące do Routing (wszystkie karty sieciowe z wyjątkiem hello te połączonego toohello zarządzania podsieci). 

## <a name="firewall-rules"></a>Reguły zapory
Zgodnie z powyższym opisem tylko przesyłania dalej protokołu IP zapewnia, że pakiety są wysyłane toohello urządzenia wirtualnego. Urządzenia nadal wymaga toodecide, jakie toodo z tych pakietów. W scenariuszu hello powyżej konieczne będzie hello toocreate reguły w urządzeń:

### <a name="opfw"></a>OPFW
OPFW reprezentuje lokalnego urządzenia zawierające hello następujące reguły:

* **Trasy**: cały ruch too10.0.0.0/16 (**azurevnet**) musi być przesyłane przez tunel **ONPREMAZURE**.
* **Zasady**: zezwolić na cały ruch dwukierunkowy między **port2** i **ONPREMAZURE**.

### <a name="azf1"></a>AZF1
AZF1 reprezentuje urządzenie wirtualne Azure zawierających hello następujące reguły:

* **Zasady**: zezwolić na cały ruch dwukierunkowy między **port1** i **port2**.

### <a name="azf2"></a>AZF2
AZF2 reprezentuje urządzenie wirtualne Azure zawierających hello następujące reguły:

* **Trasy**: cały ruch too10.0.0.0/16 (**onpremvnet**) muszą być wysyłane na adres IP bramy Azure toohello (np. 10.0.0.1) za pośrednictwem **port1**.
* **Zasady**: zezwolić na cały ruch dwukierunkowy między **port1** i **port2**.

## <a name="network-security-groups-nsgs"></a>Grupy zabezpieczeń sieci (NSG)
W tym scenariuszu nie są używane grupy NSG. Można jednak zastosować grupy NSG tooeach podsieci toorestrict ruchu przychodzącego i wychodzącego. Na przykład można zastosować hello następujące grupy NSG reguły toohello zewnętrznych PD podsieci.

**Przychodzące**

* Zezwalaj na cały ruch TCP z hello Internet tooport 80 w żadnej maszyny Wirtualnej w hello podsieci.
* Odmowa cały ruch z hello Internet.

**Wychodzące**

* Odmów wszystkich toohello ruchu internetowego.

## <a name="high-level-steps"></a>Wysokiego poziomu kroków
toodeploy tego scenariusza, wykonaj hello wysokiego poziomu poniższe kroki.

1. Tooyour logowania subskrypcji platformy Azure.
2. Jeśli toodeploy hello toomimic sieci wirtualnej lokalnej sieci, należy udostępnić hello zasoby, które są częścią **ONPREMRG**.
3. Zapewnij hello zasoby, które są częścią **AZURERG**.
4. Tunel hello świadczenia z **onpremvnet** za**azurevnet**.
5. Po udostępnieniu wszystkie zasoby, zaloguj się za**onpremvm2** i ping 10.0.3.101 tootest połączenia między **onpremsn2** i **azsn3**.

