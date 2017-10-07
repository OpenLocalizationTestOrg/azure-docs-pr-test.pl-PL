---
title: "aaaAbout urządzenia sieci VPN między lokalizacjami połączenia platformy Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule omówiono urządzenia sieci VPN i parametry protokołu IPsec dla połączeń obejmujących wiele lokalizacji usługi S2S VPN Gateway. Tooconfiguration instrukcje i przykłady zostały podane linki."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager, azure-service-management
ms.assetid: ba449333-2716-4b7f-9889-ecc521e4d616
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/14/2017
ms.author: yushwang;cherylmc
ms.openlocfilehash: 8b84afbf93d807342ecd56ab369d5909a13343e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="about-vpn-devices-and-ipsecike-parameters-for-site-to-site-vpn-gateway-connections"></a>Informacje na temat urządzeń sieci VPN i parametrów protokołu IPsec/IKE dla połączeń bramy VPN typu lokacja-lokacja

Urządzenia sieci VPN jest wymagane tooconfigure połączenia sieci VPN między lokalizacjami lokacja-lokacja (S2S) przy użyciu bramy sieci VPN. Połączenia lokacja-lokacja może być używane toocreate hybrydowego lub w dowolnym momencie bezpiecznych połączeń między sieci lokalnej i sieci wirtualne. Ten artykuł zawiera listę zweryfikowanych urządzeń sieci VPN oraz listę parametrów protokołu IPsec/IKE dla bram sieci VPN.

> [!IMPORTANT]
> Jeśli występują problemy z połączeniem między lokalnymi urządzeniami sieci VPN i bramy sieci VPN, należy zapoznać się zbyt[znane problemy ze zgodnością urządzenia](#known).
>
>

### <a name="items-toonote-when-viewing-hello-tables"></a>Elementy toonote podczas wyświetlania hello tabel:

* Nastąpiła zmiana terminologii w zakresie bram Azure VPN Gateway. Tylko hello nazwy zostały zmienione. Nie nastąpiła żadna zmiana funkcjonalności.
  * Routing statyczny = PolicyBased
  * Routing dynamiczny = RouteBased
* Specyfikacje dla bramy sieci VPN wysokowydajną i Brama sieci VPN z siecią typu RouteBased hello są takie same, chyba że określono inaczej. Na przykład urządzenia sieci VPN hello zweryfikowane, zgodnych z bramy sieci VPN z siecią typu RouteBased również są zgodne z hello bramy sieci VPN wysokowydajnej.

## <a name="devicetable"></a>Zweryfikowane urządzenia sieci VPN i przewodniki konfiguracji urządzenia

> [!NOTE]
> Podczas konfigurowania połączenia typu lokacja-lokacja wymagane jest użycie publicznego adresu IPv4 dla urządzenia sieci VPN.
>

We współpracy z dostawcami urządzeń zweryfikowaliśmy szereg standardowych urządzeń sieci VPN. Wszystkie urządzenia hello w hello rodziny urządzeń w następującej listy hello powinien współpracować z bramy sieci VPN. Zobacz [o ustawienia bramy sieci VPN](vpn-gateway-about-vpn-gateway-settings.md#vpntype) na użytek (PolicyBased lub RouteBased) hello rozwiązanie bramy sieci VPN, ma tooconfigure wpisz hello toounderstand sieci VPN.

toohelp skonfigurować urządzenie sieci VPN, zapoznaj się toohello łącza, które odpowiadają tooappropriate rodziny. Witaj łącza tooconfiguration instrukcje znajdują się w sposób optymalny. W celu uzyskania pomocy technicznej w zakresie urządzenia sieci VPN należy skontaktować się z jego producentem.

|**Dostawca**          |**Rodzina urządzeń**     |**Minimalna wersja systemu operacyjnego** |**Instrukcje dotyczące konfiguracji typu PolicyBased** |**Instrukcje dotyczące konfiguracji typu RouteBased** |
| ---                | ---                  | ---                   | ---            | ---           |
| A10 Networks, Inc. |Thunder CFW           |ACOS 4.1.1             |Niezgodne  |[Przewodnik po konfiguracji](https://www.a10networks.com/resources/deployment-guides/a10-thunder-cfw-ipsec-vpn-interoperability-azure-vpn-gateways)|
| Allied Telesis     |Routery sieci VPN z serii AR |2.9.2                  |Wkrótce     |Niezgodne  |
| Barracuda Networks, Inc. |Barracuda NextGen Firewall z serii F |PolicyBased: 5.4.3<br>RouteBased: 6.2.0 |[Przewodnik po konfiguracji](https://techlib.barracuda.com/NGF/AzurePolicyBasedVPNGW) |[Przewodnik po konfiguracji](https://techlib.barracuda.com/NGF/AzureRouteBasedVPNGW) |
| Barracuda Networks, Inc. |Barracuda NextGen Firewall z serii X |Barracuda Firewall 6.5 |[Przewodnik po konfiguracji](https://techlib.barracuda.com/BFW/ConfigAzureVPNGateway) |Niezgodne |
| Brocade            |Vyatta 5400 vRouter   |Virtual Router 6.6R3 GA|[Przewodnik po konfiguracji](http://www1.brocade.com/downloads/documents/html_product_manuals/vyatta/vyatta_5400_manual/wwhelp/wwhimpl/js/html/wwhelp.htm#href=VPN_Site-to-Site%20IPsec%20VPN/Preface.1.1.html) |Niezgodne |
| Check Point |Security Gateway |R77.30 |[Przewodnik po konfiguracji](https://supportcenter.checkpoint.com/supportcenter/portal?eventSubmit_doGoviewsolutiondetails=&solutionid=sk101275) |[Przewodnik po konfiguracji](https://supportcenter.checkpoint.com/supportcenter/portal?eventSubmit_doGoviewsolutiondetails=&solutionid=sk101275) |
| Cisco              |ASA       |8.3 |[Przykłady konfiguracji](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ASA) |Niezgodne |
| Cisco |ASR |PolicyBased: IOS 15.1<br>RouteBased: IOS 15.2 |[Przykłady konfiguracji](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ASR) |[Przykłady konfiguracji](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ASR) |
| Cisco |ISR |PolicyBased: IOS 15.0<br>RouteBased*: IOS 15.1 |[Przykłady konfiguracji](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ISR) |[Przykłady konfiguracji*](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ISR) |
| Citrix |NetScaler MPX, SDX, VPX |10.1 lub nowsze |[Przewodnik po konfiguracji](https://docs.citrix.com/en-us/netscaler/11-1/system/cloudbridge-connector-introduction/cloudbridge-connector-azure.html) |Niezgodne |
| F5 |Seria BIG-IP |12.0 |[Przewodnik po konfiguracji](https://devcentral.f5.com/articles/connecting-to-windows-azure-with-the-big-ip) |[Przewodnik po konfiguracji](https://devcentral.f5.com/articles/big-ip-to-azure-dynamic-ipsec-tunneling) |
| Fortinet |FortiGate |FortiOS 5.4.2 |  |[Przewodnik po konfiguracji](http://cookbook.fortinet.com/ipsec-vpn-microsoft-azure-54) |
| Internet Initiative Japan (IIJ) |Seria SEIL |SEIL/X 4.60<br>SEIL/B1 4.60<br>SEIL/x86 3.20 |[Przewodnik po konfiguracji](http://www.iij.ad.jp/biz/seil/ConfigAzureSEILVPN.pdf) |Niezgodne |
| Juniper |SRX |PolicyBased: JunOS 10.2<br>Routebased: JunOS 11.4 |[Przykłady konfiguracji](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/SRX) |[Przykłady konfiguracji](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/SRX) |
| Juniper |Seria J |PolicyBased: JunOS 10.4r9<br>RouteBased: JunOS 11.4 |[Przykłady konfiguracji](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/JSeries) |[Przykłady konfiguracji](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/JSeries) |
| Juniper |ISG |ScreenOS 6.3 |[Przykłady konfiguracji](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/ISG) |[Przykłady konfiguracji](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/ISG) |
| Juniper |SSG |ScreenOS 6.2 |[Przykłady konfiguracji](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/SSG) |[Przykłady konfiguracji](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/SSG) |
| Microsoft |Routing and Remote Access Service |Windows Server 2012 |Niezgodne |[Przykłady konfiguracji](http://go.microsoft.com/fwlink/p/?LinkId=717761) |
| Open Systems AG |Mission Control Security Gateway |Nie dotyczy |[Przewodnik po konfiguracji](https://www.open.ch/_pdf/Azure/AzureVPNSetup_Installation_Guide.pdf) |Niezgodne |
| Openswan |Openswan |2.6.32 |(Wkrótce) |Niezgodne |
| Palo Alto Networks |Wszystkie urządzenia z systemem PAN-OS |PAN-OS<br>PolicyBased: wersja 6.1.5 lub nowsza<br>RouteBased: 7.1.4 |[Przewodnik po konfiguracji](https://live.paloaltonetworks.com/t5/Configuration-Articles/How-to-Configure-VPN-Tunnel-Between-a-Palo-Alto-Networks/ta-p/59065) |[Przewodnik po konfiguracji](https://live.paloaltonetworks.com/t5/Integration-Articles/Configuring-IKEv2-VPN-for-Microsoft-Azure-Environment/ta-p/60340) |
| SonicWall |Seria TZ, seria NSA<br>Seria SuperMassive<br>Seria E-Class NSA |SonicOS 5.8.x<br>SonicOS 5.9.x<br>SonicOS 6.x |[Przewodnik po konfiguracji dla platformy SonicOS 6.2](http://documents.software.dell.com/sonicos/6.2/microsoft-azure-configuration-guide?ParentProduct=646)<br>[Przewodnik po konfiguracji dla platformy SonicOS 5.9](http://documents.software.dell.com/sonicos/5.9/microsoft-azure-configuration-guide?ParentProduct=850) |[Przewodnik po konfiguracji dla platformy SonicOS 6.2](http://documents.software.dell.com/sonicos/6.2/microsoft-azure-configuration-guide?ParentProduct=646)<br>[Przewodnik po konfiguracji dla platformy SonicOS 5.9](http://documents.software.dell.com/sonicos/5.9/microsoft-azure-configuration-guide?ParentProduct=850) |
| WatchGuard |Wszystkie |Fireware XTM<br> PolicyBased: v11.11.x<br>RouteBased: v11.12.x |[Przewodnik po konfiguracji](http://watchguardsupport.force.com/publicKB?type=KBArticle&SFDCID=kA2F00000000LI7KAM&lang=en_US) |[Przewodnik po konfiguracji](http://watchguardsupport.force.com/publicKB?type=KBArticle&SFDCID=kA22A000000XZogSAG&lang=en_US)|

(*) Routery z serii ISR 7200 obsługują tylko sieci VPN typu PolicyBased.

## <a name="additionaldevices"></a>Niezweryfikowane urządzenia sieci VPN

Jeśli nie widzisz urządzenia wymienione w tabeli urządzenia VPN zweryfikowane hello urządzenia mogą pracować z połączenia lokacja-lokacja. Dodatkową pomoc oraz instrukcje dotyczące konfiguracji można uzyskać, kontaktując się z producentem urządzenia.

## <a name="editing"></a>Edytowanie przykładów konfiguracji urządzenia

Po pobraniu próbki konfiguracji urządzenia sieci VPN hello pod warunkiem, będą potrzebne tooreplace niektóre hello wartości tooreflect hello ustawienia do środowiska.

### <a name="tooedit-a-sample"></a>tooedit próbki:

1. Przykład Witaj Otwórz za pomocą Notatnika.
2. Wyszukaj i Zamień wszystkie <*tekst*> ciągów o wartości hello, które odnoszą się tooyour środowiska. Należy się tooinclude < i >. Jeśli określono nazwę, nazwę hello, którą wybierzesz powinny być unikatowe. Jeśli polecenie nie działa, zapoznaj się z dokumentacją producenta urządzenia.

| **Przykładowy tekst** | **Zmień na** |
| --- | --- |
| &lt;RP_OnPremisesNetwork&gt; |Nazwę tego obiektu definiuje użytkownik. Przykład: myOnPremisesNetwork |
| &lt;RP_AzureNetwork&gt; |Nazwę tego obiektu definiuje użytkownik. Przykład: myAzureNetwork |
| &lt;RP_AccessList&gt; |Nazwę tego obiektu definiuje użytkownik. Przykład: myAzureAccessList |
| &lt;RP_IPSecTransformSet&gt; |Nazwę tego obiektu definiuje użytkownik. Przykład: myIPSecTransformSet |
| &lt;RP_IPSecCryptoMap&gt; |Nazwę tego obiektu definiuje użytkownik. Przykład: myIPSecCryptoMap |
| &lt;SP_AzureNetworkIpRange&gt; |Określ zakres. Przykład: 192.168.0.0 |
| &lt;SP_AzureNetworkSubnetMask&gt; |Określ maskę podsieci. Przykład: 255.255.0.0 |
| &lt;SP_OnPremisesNetworkIpRange&gt; |Określ zakres lokalny. Przykład: 10.2.1.0 |
| &lt;SP_OnPremisesNetworkSubnetMask&gt; |Określ lokalną maskę podsieci. Przykład: 255.255.255.0 |
| &lt;SP_AzureGatewayIpAddress&gt; |Ta sieć wirtualna tooyour określonych informacji i znajduje się w portalu zarządzania hello jako **adresu IP bramy**. |
| &lt;SP_PresharedKey&gt; |Te informacje są tooyour określonej sieci wirtualnej i znajduje się w hello portalu zarządzania, jak zarządzać klucza. |

## <a name="ipsec"></a>Parametry protokołu IPsec/IKE

> [!NOTE]
> Chociaż wartości hello wymienione w poniższej tabeli hello obecnie są obsługiwane przez bramę sieci VPN hello, nie jest brak mechanizm toospecify, lub wybierz określona kombinacja parametrów lub algorytmów z hello bramy sieci VPN. Należy określić wszystkie ograniczenia z hello lokalnego urządzenia sieci VPN. Ponadto należy określić ograniczenie wartości **MSS** wynoszące **1350**.
> 
>

W hello następujących tabel:

* SA — skojarzenia zabezpieczeń
* Protokół IKE — faza 1 jest również określany jako „Tryb główny”
* Protokół IKE — faza 2 jest również określany jako „Tryb szybki”

### <a name="ike-phase-1-main-mode-parameters"></a>Parametry protokołu IKE — faza 1 (tryb główny)

| **Właściwość**          |**PolicyBased**    | **RouteBased**    |
| ---                   | ---               | ---               |
| Wersja IKE           |IKEv1              |IKEv2              |
| Grupa Diffie’ego-Hellmana  |Grupa 2 (1024 bity) |Grupa 2 (1024 bity) |
| Metoda uwierzytelniania |Klucz wstępny     |Klucz wstępny     |
| Szyfrowanie i algorytmy wyznaczania wartości skrótu |1. AES256, SHA256<br>2. AES256, SHA1<br>3. AES128, SHA1<br>4. 3DES, SHA1 |1. AES256, SHA1<br>2. AES256, SHA256<br>3. AES128, SHA1<br>4. AES128, SHA256<br>5. 3DES, SHA1<br>6. 3DES, SHA256 |
| Okres istnienia skojarzeń zabezpieczeń           |28 800 sekund     |28 800 sekund     |

### <a name="ike-phase-2-quick-mode-parameters"></a>Parametry protokołu IKE — faza 2 (tryb szybki)

| **Właściwość**                  |**PolicyBased**| **RouteBased**                              |
| ---                           | ---           | ---                                         |
| Wersja IKE                   |IKEv1          |IKEv2                                        |
| Szyfrowanie i algorytmy wyznaczania wartości skrótu |1. AES256, SHA256<br>2. AES256, SHA1<br>3. AES128, SHA1<br>4. 3DES, SHA1 |[Oferty skojarzeń zabezpieczeń trybu szybkiego RouteBased](#RouteBasedOffers) |
| Okres istnienia skojarzeń zabezpieczeń (czas)            |3600 sekund  |27 000 sekund                                |
| Okres istnienia skojarzeń zabezpieczeń (bajty)           |102 400 000 KB | -                                           |
| Doskonałe utajnienie przekazywania (PFS) |Nie             |[Oferty skojarzeń zabezpieczeń trybu szybkiego RouteBased](#RouteBasedOffers) |
| Wykrywanie nieaktywnych elementów równorzędnych (DPD, Dead Peer Detection)     |Nieobsługiwane  |Obsługiwane                                    |


### <a name ="RouteBasedOffers"></a>Oferty skojarzeń zabezpieczeń protokołu IPsec połączenia VPN typu RouteBased (skojarzenia zabezpieczeń trybu szybkiego protokołu IKE)

Witaj poniższej tabeli wymieniono oferty skojarzeń zabezpieczeń IPsec (trybu szybkiego IKE). Oferty są wymienione hello kolejności preferencji tej oferty hello jest przedstawiony lub akceptowane.

#### <a name="azure-gateway-as-initiator"></a>Brama Azure jako inicjator

|-  |**Szyfrowanie**|**Uwierzytelnianie**|**Grupa PFS**|
|---| ---          |---               |---          |
| 1 |GCM AES256    |GCM (AES256)      |Brak         |
| 2 |AES256        |SHA1              |Brak         |
| 3 |3DES          |SHA1              |Brak         |
| 4 |AES256        |SHA256            |Brak         |
| 5 |AES128        |SHA1              |Brak         |
| 6 |3DES          |SHA256            |Brak         |

#### <a name="azure-gateway-as-responder"></a>Brama Azure jako obiekt odpowiadający

|-  |**Szyfrowanie**|**Uwierzytelnianie**|**Grupa PFS**|
|---| ---          | ---              |---          |
| 1 |GCM AES256    |GCM (AES256)      |Brak         |
| 2 |AES256        |SHA1              |Brak         |
| 3 |3DES          |SHA1              |Brak         |
| 4 |AES256        |SHA256            |Brak         |
| 5 |AES128        |SHA1              |Brak         |
| 6 |3DES          |SHA256            |Brak         |
| 7 |DES           |SHA1              |Brak         |
| 8 |AES256        |SHA1              |1            |
| 9 |AES256        |SHA1              |2            |
| 10|AES256        |SHA1              |14           |
| 11|AES128        |SHA1              |1            |
| 12|AES128        |SHA1              |2            |
| 13|AES128        |SHA1              |14           |
| 14|3DES          |SHA1              |1            |
| 15|3DES          |SHA1              |2            |
| 16|3DES          |SHA256            |2            |
| 17|AES256        |SHA256            |1            |
| 18|AES256        |SHA256            |2            |
| 19|AES256        |SHA256            |14           |
| 20|AES256        |SHA1              |24           |
| 21|AES256        |SHA256            |24           |
| 22|AES128        |SHA256            |Brak         |
| 23|AES128        |SHA256            |1            |
| 24|AES128        |SHA256            |2            |
| 25|AES128        |SHA256            |14           |
| 26|3DES          |SHA1              |14           |

* Wartość NULL szyfrowania ESP protokołu IPsec możesz określić z bramami sieci VPN typu RouteBased i HighPerformance. Szyfrowanie oparte na wartości null nie zapewnia ochrony toodata podczas przesyłania i należy używać tylko w przypadku maksymalną przepustowość i minimum opóźnienie jest wymagana. Klienci mogą wybrać toouse to w scenariuszach komunikacji do wirtualnymi i podczas szyfrowania jest stosowana w innym miejscu w rozwiązaniu hello.
* Dla łączności między lokalizacjami za pośrednictwem hello Internet za pomocą ustawienia bramy sieci VPN platformy Azure domyślnej hello szyfrowania i algorytmów wyznaczania wartości skrótu wymienionych w tabelach hello powyżej tooensure zabezpieczeń, krytyczne komunikacji.

## <a name="known"></a>Znane problemy dotyczące zgodności urządzeń

> [!IMPORTANT]
> Są one hello znane problemy ze zgodnością między urządzeniami sieci VPN innych firm i bram sieci VPN platformy Azure. Hello Azure zespołu jest aktywnie z dostawcami hello tooaddress hello problemy wymienione w tym miejscu. Po hello problemy zostaną rozwiązane, ta strona będzie aktualizowana hello najbardziej aktualne informacje. Sprawdzaj ją okresowo.
>
>

### <a name="feb-16-2017"></a>16 lutego 2017 r.

**Urządzenia sieci Palo Alto z too7.1.4 wcześniejszych wersji** dla platformy Azure sieci VPN opartej na trasach: Jeśli za pomocą urządzenia sieci VPN z sieci Palo Alto too7.1.4 wcześniejszych wersji systemu operacyjnego PRZESUWANIE i występują łączności wystawia tooAzure bramy sieci VPN opartej na trasach wykonaj następujące kroki hello:

1. Sprawdź wersję oprogramowania układowego hello urządzenia Palo Alto sieci. Jeśli danej wersji systemu operacyjnego PRZESUWANIE jest starsza niż 7.1.4, Uaktualnij too7.1.4.
2. Na urządzeniu sieci Palo Alto hello, zmień hello Faza 2 SA (lub skojarzenia zabezpieczeń trybu szybkiego) too28 okres istnienia, 800 sekund (8 godzin) podczas łączenia toohello bramy sieci VPN platformy Azure.
3. Jeśli nadal występują problemy z łącznością, należy otworzyć żądania obsługi z hello portalu Azure.
