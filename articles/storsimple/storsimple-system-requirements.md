---
title: wymagania systemowe aaaStorSimple | Dokumentacja firmy Microsoft
description: "Zawiera opis oprogramowania, sieci i wymagania dotyczące wysokiej dostępności i najlepsze rozwiązania dotyczące rozwiązania Microsoft Azure StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 2b6ca34a-d758-48e7-ab1e-4fdd80cf48d4
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/06/2017
ms.author: alkohli
ms.openlocfilehash: ec0bb5ad2f2d4c9901da2d95147dd9daa178f6b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-software-high-availability-and-networking-requirements"></a>Oprogramowanie StorSimple, wysokiej dostępności i wymagań sieciowych
## <a name="overview"></a>Omówienie
Zapraszamy tooMicrosoft Azure StorSimple. W tym artykule opisano wymagania systemowe i najlepsze rozwiązania dla urządzenia StorSimple i hello magazynu klientów uzyskujących dostęp do urządzenia hello. Firma Microsoft zaleca się przejrzenie informacji hello dokładnie przed wdrażanie systemu StorSimple, a następnie Odwołaj tooit w razie potrzeby podczas wdrażania kolejnych operacji.

wymagania systemowe Hello obejmują:

* **Wymagania dotyczące oprogramowania dla klientów magazynu** — w tym artykule opisano hello obsługiwanych systemów operacyjnych i wszelkie dodatkowe wymagania dotyczące tych systemów operacyjnych.
* **Wymagania dotyczące sieci dla urządzenia StorSimple hello** — informacje na temat portów hello tego toobe potrzeby otwórz w Twojej tooallow zapory dla ruchu iSCSI, chmury lub zarządzania.
* **Wymagania dotyczące wysokiej dostępności dla urządzenia StorSimple** — w tym artykule opisano wymagania dotyczące wysokiej dostępności i najlepszych praktyk komputera urządzenia i hosta StorSimple. 

## <a name="software-requirements-for-storage-clients"></a>Wymagania dotyczące oprogramowania dla klientów magazynu
Witaj, następujące wymagania dotyczące oprogramowania dotyczą hello magazynu klientów, które uzyskują dostęp do urządzenia StorSimple.

| Obsługiwane systemy operacyjne | Wersja wymagana | Dodatkowe wymagania dotyczące/uwagi |
| --- | --- | --- |
| Windows Server |2008 R2 Z DODATKIEM SP1, 2012, 2012R2, 2016 |Woluminy iSCSI StorSimple można używać na tylko hello następujące typy dysku systemu Windows:<ul><li>Wolumin prosty na dysku podstawowym</li><li>Proste i dublowane wolumin na dysku dynamicznym</li></ul>Obsługiwane są tylko hello oprogramowania inicjatorów iSCSI obecne w systemie operacyjnym hello. Inicjatorów iSCSI sprzętu nie są obsługiwane.<br></br>Windows Server 2012 oraz alokowanie 2016 i funkcji odciążonego transferu danych są obsługiwane, jeśli używasz woluminu StorSimple iSCSI.<br><br>StorSimple można tworzyć alokowane elastycznie i pełni woluminów. Nie można go tworzyć woluminów inicjowanych częściowo.<br><br>Ponowne formatowanie woluminu alokowane elastycznie może zająć dużo czasu. Zaleca się usunięcie hello woluminu, a następnie utworzenie nową zamiast ponownego formatowania. Jednak jeśli jednak preferować tooreformat woluminu:<ul><li>Uruchom następujące polecenie przed hello ponownego formatowania tooavoid miejsca odzyskiwanie opóźnienia hello: <br>`fsutil behavior set disabledeletenotify 1`</br></li><li>Po zakończeniu formatowania hello następujące hello użyj polecenia Włącz toore odzyskiwanie miejsca:<br>`fsutil behavior set disabledeletenotify 0`</br></li><li>Zastosuj poprawkę hello systemu Windows Server 2012, zgodnie z opisem w [KB 2878635](https://support.microsoft.com/kb/2870270) tooyour komputera systemu Windows Server.</li></ul></li></ul></ul> Jeśli konfigurujesz StorSimple Snapshot Manager lub kartę StorSimple dla programu SharePoint, przejdź zbyt[wymagań dotyczących oprogramowania dla składników opcjonalnych](#software-requirements-for-optional-components). |
| VMWare ESX |5.5 i 6.0 |Obsługiwane z programem VMWare vSphere jako klient. Funkcja VAAI bloku jest obsługiwana z programem VMware vSphere urządzenia StorSimple. |
| Linux RHEL/CentOS |5, 6 i 7 |Obsługa klientów iSCSI Linux z wersjami inicjatora iSCSI Otwórz 5, 6 i 7. |
| Linux |SUSE Linux 11 | |

> [!NOTE]
> IBM AIX nie jest obecnie obsługiwane z StorSimple.
> 
> 

## <a name="software-requirements-for-optional-components"></a>Wymagania dotyczące oprogramowania dla składników opcjonalnych
Witaj, następujące wymagania dotyczące oprogramowania dotyczą hello opcjonalnych składników StorSimple (StorSimple Snapshot Manager i karty StorSimple dla programu SharePoint).

| Składnik | Platforma hosta | Dodatkowe wymagania dotyczące/uwagi |
| --- | --- | --- |
| StorSimple Snapshot Manager |Windows Server 2008 R2 z dodatkiem SP1, 2012, 2012R2 |Użycie programu StorSimple Snapshot Manager w systemie Windows Server jest wymagany dla kopii zapasowej/przywracania dublowany dysków dynamicznych i wszelkich spójnych z aplikacją kopii zapasowych.<br> StorSimple Snapshot Manager jest obsługiwana tylko w przypadku systemu Windows Server 2008 R2 z dodatkiem SP1 (64-bitowy), Windows 2012 R2 i Windows Server 2012.<ul><li>Jeśli używasz systemu Windows Server 2012, należy zainstalować .NET 3.5 — 4.5, przed zainstalowaniem programu StorSimple Snapshot Manager.</li><li>Jeśli korzystasz z systemu Windows Server 2008 R2 z dodatkiem SP1, należy zainstalować program Windows Management Framework 3.0, przed zainstalowaniem programu StorSimple Snapshot Manager.</li></ul> |
| Adapter usługi StorSimple dla programu SharePoint |Windows Server 2008 R2 z dodatkiem SP1, 2012, 2012R2 |<ul><li>Karta StorSimple dla programu SharePoint jest obsługiwana tylko w programie SharePoint 2010 oraz SharePoint 2013.</li><li>SPZ wymaga programu SQL Server Enterprise Edition w wersji 2008 R2 lub 2012.</li></ul> |

## <a name="networking-requirements-for-your-storsimple-device"></a>Wymagań sieciowych dotyczących urządzenia StorSimple
Urządzenia StorSimple to urządzenie w trybie blokady. Porty muszą jednak toobe otwarty w Twojej tooallow zapory dla inicjatora iSCSI, chmur i ruch związany z zarządzaniem. Witaj poniższej tabeli wymieniono hello porty wymagające toobe otwarty w zaporze. W tej tabeli *w* lub *przychodzących* odwołuje się toohello kierunek, w którym przychodzące żądania klientów dostępu urządzenia. *Limit* lub *wychodzących* odwołuje się toohello kierunek, w którym urządzenia StorSimple wysyła dane zewnętrznie, poza wdrożenia hello: na przykład wychodzących toohello Internet.

| Nr portu<sup>1,2</sup> | Przychodzący lub wychodzący | Zakres portów | Wymagane | Uwagi |
| --- | --- | --- | --- | --- |
| TCP 80 (HTTP)<sup>3</sup> |limit |WAN |Nie |<ul><li>Wychodzący port jest używany do aktualizacji tooretrieve dostęp do Internetu.</li><li>Serwer proxy ruchu wychodzącego sieci web Hello jest konfigurowane przez użytkownika.</li><li>aktualizacje systemu tooallow, ten port również należy otworzyć kontrolera hello stałe adresy IP.</li></ul> |
| TCP 443 (HTTPS)<sup>3</sup> |limit |WAN |Tak |<ul><li>Wychodzący port jest używany do uzyskiwania dostępu do danych w chmurze hello.</li><li>Serwer proxy ruchu wychodzącego sieci web Hello jest konfigurowane przez użytkownika.</li><li>aktualizacje systemu tooallow, ten port również należy otworzyć kontrolera hello stałe adresy IP.</li><li>Port ten jest również używany na obu kontrolerów hello na wyrzucanie elementów bezużytecznych.</li></ul> |
| UDP 53 (DNS) |limit |WAN |W niektórych przypadkach; Zobacz uwagi. |Ten port jest wymagany tylko wtedy, gdy używasz serwera DNS w Internecie. |
| UDP 123 (NTP) |limit |WAN |W niektórych przypadkach; Zobacz uwagi. |Ten port jest wymagany tylko wtedy, gdy używasz serwera NTP internetowego. |
| TCP 9354 |limit |WAN |Tak |port wychodzący Hello jest używany przez toocommunicate urządzenia StorSimple hello z hello usługi Menedżer StorSimple. |
| 3260 (iSCSI) |W |SIECI LAN |Nie |Ten port jest używany tooaccess danych za pośrednictwem interfejsu iSCSI. |
| 5985 |W |SIECI LAN |Nie |Port wejściowy jest używany przez toocommunicate StorSimple Snapshot Manager hello urządzenia StorSimple.<br>Port ten jest również używany podczas zdalnego nawiązywania połączenia tooWindows środowiska PowerShell dla urządzenia StorSimple za pośrednictwem protokołu HTTP. |
| 5986 |W |SIECI LAN |Nie |Port ten jest używany podczas zdalnego nawiązywania połączenia tooWindows środowiska PowerShell dla urządzenia StorSimple przy użyciu protokołu HTTPS. |

<sup>1</sup> nie portów przychodzących muszą toobe otwarte na hello publicznej sieci Internet.

<sup>2</sup> Jeśli wiele portów przenoszenia konfiguracji bramy, kolejność kierowany ruch wychodzący hello będzie ustalana na podstawie kolejności routingu portów hello opisanego w [routingu portu](#routing-metric), poniżej.

<sup>3</sup> kontrolera hello stałe adresy IP na urządzeniu StorSimple musi obsługiwać Routing i stanie tooconnect toohello Internet bezpośrednio lub za pośrednictwem hello skonfigurowany serwer proxy sieci web. Hello stałe adresy IP są używane do obsługi hello aktualizacje toohello urządzenia. Jeśli kontrolery urządzeń hello nie można połączyć toohello Internet za pośrednictwem hello stałe adresy IP, nie będzie możliwe tooupdate urządzenia StorSimple.

> [!IMPORTANT]
> Upewnij się, czy Zapora hello nie zmodyfikować lub odszyfrować żaden ruch protokołu SSL między hello urządzenia StorSimple i Azure.
> 
> 

### <a name="url-patterns-for-firewall-rules"></a>Wzorce adresu URL dla reguł zapory
Administratorzy sieci można skonfigurować często zaawansowanych zapory oparte na powitania adresu URL wzorce toofilter hello reguły ruchu przychodzącego i hello ruch wychodzący. Witaj usługi Menedżer StorSimple i urządzeń StorSimple, na których są zależne od innych aplikacji firmy Microsoft, takich jak usługi Azure Service Bus, Azure Active Directory kontroli dostępu konta magazynu i serwerach Microsoft Update. wzorce adresu URL Hello skojarzone z tymi aplikacjami można tooconfigure używanych reguł zapory. Jest ważne toounderstand, który wzorców adresów URL hello skojarzone z tymi aplikacjami można zmienić. Z kolei spowoduje wymagają toomonitor administratora sieci hello i zaktualizować reguł zapory dla Twojego urządzenia StorSimple, jak i w razie potrzeby.

Firma Microsoft zaleca, aby ustawić regułach zapory dla ruchu wychodzącego, oparte na StorSimple liberally stałe adresy IP, w większości przypadków. Można jednak użyć hello informacje poniżej tooset zaawansowanych reguł zapory, które są potrzebne toocreate bezpiecznych środowiskach.

> [!NOTE]
> urządzenie Hello (źródło) adresów IP powinien być zawsze ustawiony interfejsów sieciowych tooall hello włączone. docelowy Hello adresów IP powinna być ustawiona zbyt[zakresy IP centrum danych Azure](https://www.microsoft.com/en-us/download/confirmation.aspx?id=41653).
> 
> 

#### <a name="url-patterns-for-azure-portal"></a>Wzorce adresu URL dla portalu Azure
| Wzorzec URL | Składnik/funkcji | Adresy IP urządzeń |
| --- | --- | --- |
| `https://*.storsimple.windowsazure.com/*`<br>`https://*.accesscontrol.windows.net/*`<br>`https://*.servicebus.windows.net/*` |Usługa StorSimple Manager<br>Usługa kontroli dostępu<br>Azure Service Bus |Interfejsy sieciowe z obsługą chmury |
| `https://*.backup.windowsazure.com` |Rejestracja urządzenia |Tylko dane 0 |
| `http://crl.microsoft.com/pki/*`<br>`http://www.microsoft.com/pki/*` |Odwoływanie certyfikatów |Interfejsy sieciowe z obsługą chmury |
| `https://*.core.windows.net/*` <br>`https://*.data.microsoft.com`<br>`http://*.msftncsi.com` |Monitorowanie i kontami magazynu Azure |Interfejsy sieciowe z obsługą chmury |
| `http://*.windowsupdate.microsoft.com`<br>`https://*.windowsupdate.microsoft.com`<br>`http://*.update.microsoft.com`<br> `https://*.update.microsoft.com`<br>`http://*.windowsupdate.com`<br>`http://download.microsoft.com`<br>`http://wustat.windows.com`<br>`http://ntservicepack.microsoft.com` |Serwerów Microsoft Update<br> |Tylko stałe adresy IP kontrolera |
| `http://*.deploy.akamaitechnologies.com` |Akamai CDN |Tylko stałe adresy IP kontrolera |
| `https://*.partners.extranet.microsoft.com/*` |Pakiet pomocy technicznej |Interfejsy sieciowe z obsługą chmury |

#### <a name="url-patterns-for-azure-government-portal"></a>Wzorce adresu URL portalu Azure dla instytucji rządowych
| Wzorzec URL | Składnik/funkcji | Adresy IP urządzeń |
| --- | --- | --- |
| `https://*.storsimple.windowsazure.us/*`<br>`https://*.accesscontrol.usgovcloudapi.net/*`<br>`https://*.servicebus.usgovcloudapi.net/*` |Usługa StorSimple Manager<br>Usługa kontroli dostępu<br>Azure Service Bus |Interfejsy sieciowe z obsługą chmury |
| `https://*.backup.windowsazure.us` |Rejestracja urządzenia |Tylko dane 0 |
| `http://crl.microsoft.com/pki/*`<br>`http://www.microsoft.com/pki/*` |Odwoływanie certyfikatów |Interfejsy sieciowe z obsługą chmury |
| `https://*.core.usgovcloudapi.net/*` <br>`https://*.data.microsoft.com`<br>`http://*.msftncsi.com` |Monitorowanie i kontami magazynu Azure |Interfejsy sieciowe z obsługą chmury |
| `http://*.windowsupdate.microsoft.com`<br>`https://*.windowsupdate.microsoft.com`<br>`http://*.update.microsoft.com`<br> `https://*.update.microsoft.com`<br>`http://*.windowsupdate.com`<br>`http://download.microsoft.com`<br>`http://wustat.windows.com`<br>`http://ntservicepack.microsoft.com` |Serwerów Microsoft Update<br> |Tylko stałe adresy IP kontrolera |
| `http://*.deploy.akamaitechnologies.com` |Akamai CDN |Tylko stałe adresy IP kontrolera |
| `https://*.partners.extranet.microsoft.com/*` |Pakiet pomocy technicznej |Interfejsy sieciowe z obsługą chmury |

### <a name="routing-metric"></a>Metryka routingu
Metryka routingu jest skojarzony z interfejsów hello i hello bramy, który trasy toohello danych hello określony sieci. Metryka routingu jest używany przez hello routingu protokołu toocalculate hello najlepsze ścieżki tooa danego przeznaczenia, jeśli dowie się toohello istnieje wiele ścieżek tego samego miejsca docelowego. Witaj niższe hello routingu metryki, hello wyższy poziom hello preferencji.

W hello kontekstu StorSimple, jeśli wiele interfejsów sieciowych i bram skonfigurowany toochannel ruchu, metryki routingu hello wejścia play toodetermine hello względną kolejność, w których hello interfejsy będzie pobrać używane. Nie można zmienić metryki routingu Hello przez użytkownika hello. Można jednak użyć hello `Get-HcsRoutingTable` tooprint polecenia cmdlet w tabeli routingu hello (i metryk) na urządzeniu StorSimple. Więcej informacji na temat polecenia cmdlet Get-HcsRoutingTable w [StorSimple Rozwiązywanie problemów z wdrożenia](storsimple-troubleshoot-deployment.md).

Hello routingu metryki algorytmy są różne w zależności od wersji oprogramowania hello działającej na urządzeniu StorSimple.

**TooUpdate wcześniejszych wersjach 1**

Dotyczy to również wersji wcześniejszych tooUpdate 1, takich jak hello GA 0,1, 0,2 albo 0,3 wersje oprogramowania. kolejność Hello oparciu metryki routingu jest następujący:

   *Ostatnio skonfigurowany interfejs sieciowy Ethernet 10 > Interfejs sieciowy inne 10 GbE > ostatnio skonfigurowany interfejs sieciowy Ethernet 1 > inne 1 GbE interfejsu sieciowego*

**Wersje, począwszy od aktualizacji 1 i wcześniejszych tooUpdate 2**

W tym wersje oprogramowania, takich jak 1, 1.1 lub 1.2. kolejność Hello oparciu metryki routingu decyzji w następujący sposób:

   *DANE 0 > ostatnio skonfigurowany interfejs sieciowy Ethernet 10 > Interfejs sieciowy inne 10 GbE > ostatnio skonfigurowany interfejs sieciowy Ethernet 1 > inne 1 GbE interfejsu sieciowego*

   W pakiecie Update 1 metrykę routingu hello danych 0 staje się hello najniższy; w związku z tym ruch chmury hello jest kierowany przez dane 0. Zwróć uwagę to, jeśli istnieje więcej niż jeden interfejs sieciowy z obsługą chmury na urządzeniu StorSimple.

**Wersje, począwszy od aktualizacji 2**

Aktualizacja 2 ma kilka ulepszeń związanych z siecią i metryki routingu hello została zmieniona. zachowanie Hello można wyjaśnić w następujący sposób.

* Zestaw wartości ustalonej przypisano toonetwork interfejsów.     
* Należy wziąć pod uwagę tabeli przykładzie pokazano poniżej z toohello przypisanych wartości różnych interfejsów sieciowych gdy są one włączone w chmurze lub chmury: wyłączona, ale skonfigurowanej bramy. Uwaga hello wartości przypisane w tym miejscu są przykładowe wartości.

    | Interfejs sieciowy | Włączoną obsługę chmury | Chmura wyłączonymi z bramy |
    |-----|---------------|---------------------------|
    | Dane 0  | 1            | -                        |
    | Dane 1  | 2            | 20                       |
    | Dane 2  | 3            | 30                       |
    | Dane 3  | 4            | 40                       |
    | Dane 4  | 5            | 50                       |
    | Dane 5  | 6            | 60                       |


* kolejność Hello, w którym ruch w chmurze hello zostaną przesłane za pośrednictwem interfejsów sieciowych hello jest:
  
    *Dane 0 > danych 1 > Data 2 > danych 3 > dane 4 > dane 5*
  
    Można to wyjaśnić hello poniższy przykład.
  
    Należy wziąć pod uwagę urządzenia StorSimple z dwoma interfejsami sieciowymi włączoną obsługę chmury, dane 0 do dane 5. Dane od 1 do 4 danych są wyłączone chmury, ale ma skonfigurowanej bramy. będzie Hello kolejność, w którym ruch będą kierowane do tego urządzenia:
  
    *Dane 0 (1) > dane 5 (6) > danych 1 (20) > dane 2 (30) > danych 3 (40) > dane 4 (50)*
  
    *gdzie liczby hello w nawiasach wskazują hello odpowiednich metryk routingu.*
  
    W przypadku niepowodzenia dane 0 hello ruchu w chmurze będzie pobrać kierowane do dane 5. Biorąc pod uwagę, że brama jest skonfigurowana w innych sieciach, gdyby zarówno dane 0, jak i dane 5 toofail, ruch w chmurze hello będzie przejście przez 1 danych.
* Jeśli interfejs sieciowy z obsługą chmury nie powiedzie się, to 3 ponowne próby z interfejsem 30 toohello tooconnect drugi opóźnienia. Jeśli ponawiania prób hello zakończą się niepowodzeniem, hello jest routingiem toohello dalej dostępny włączoną obsługę chmury interfejs zgodnie z ustaleniami hello tabeli routingu. Jeśli wszystkie hello włączoną obsługę chmury interfejsów sieciowych zakończyć się niepowodzeniem, a następnie hello urządzenia zostaną przełączone awaryjnie toohello inny kontroler (ponowny rozruch w tym przypadku).
* W przypadku awarii VIP dla interfejsu sieci iSCSI, będzie 3 ponowne próby z opóźnieniem 2 sekundy. To zachowanie jest przebywała hello same z hello poprzednich wersji. Jeśli wszystkie interfejsy sieciowe iSCSI hello zakończą się niepowodzeniem, kontroler trybu failover zostanie przeprowadzona (wraz z ponownego uruchomienia).
* Alert jest zgłaszany również na urządzeniu StorSimple, po awarii adresu VIP. Aby uzyskać więcej informacji, przejdź zbyt[alertów krótkimi opisami](storsimple-manage-alerts.md).
* W postaci liczby ponownych prób iSCSI ma pierwszeństwo przed chmury.
  
    Należy wziąć pod uwagę hello poniższy przykład: A StorSimple, urządzenie ma włączone dwa interfejsy sieci, dane 0 i 1 danych. Dane 0 jest włączoną obsługę chmury danych 1 jest zarówno chmury i włączono interfejs iSCSI. Żadne inne interfejsy sieciowe na tym urządzeniu są włączone dla chmury lub iSCSI.
  
    Jeśli dane 1 kończy się niepowodzeniem, podane go hello ostatniego interfejsu sieci iSCSI, spowoduje tooData pracy awaryjnej kontrolera 1 hello na inny kontroler.

### <a name="networking-best-practices"></a>Najlepsze rozwiązania w zakresie sieci
Ponadto toohello powyżej wymagań, aby uzyskać optymalną wydajność hello rozwiązania StorSimple sieciowych należy stosować toohello następujące najlepsze rozwiązania:

* Upewnij się, że urządzenia StorSimple ma dedykowany 40 MB/s przepustowości (lub więcej) dostępne przez cały czas. Nie należy udostępniać tego przepustowości (lub alokacji, należy zagwarantować przy użyciu zasad QoS hello) z innymi aplikacjami.
* Upewnij się, że toohello łączność sieci Internet jest dostępna przez cały czas. Sporadyczne lub zawodnych Internet połączeń toohello urządzeń, w tym bez łączności z Internetem, spowoduje nieobsługiwaną konfiguracją.
* Izolowanie ruchu iSCSI i chmury hello przez używania dedykowanych interfejsów sieciowych na twoim urządzeniu dostęp iSCSI i chmury. Aby uzyskać więcej informacji, zobacz temat jak zbyt[zmodyfikować interfejsów sieciowych](storsimple-modify-device-config.md#modify-network-interfaces) na urządzeniu StorSimple.
* Nie należy używać konfiguracji Link Aggregation Control Protocol (LACP) interfejsów sieciowych. To jest nieobsługiwana konfiguracja.

## <a name="high-availability-requirements-for-storsimple"></a>Wymagania dotyczące wysokiej dostępności dla urządzenia StorSimple
Hello platforma sprzętowa, która jest zawarta w rozwiązaniu StorSimple hello zapewnia dostępność i niezawodność funkcje, które zapewnia podstawę dla infrastruktury magazynu o wysokiej dostępności, odpornej na uszkodzenia w centrum danych. Jednak istnieją wymagania i najlepsze rozwiązania, które należy przestrzegać toohelp zapewnienia hello dostępności rozwiązania StorSimple. Przed wdrożeniem StorSimple, należy dokładnie przejrzeć hello następujące wymagania i najlepsze rozwiązania dotyczące urządzenia StorSimple hello i połączone komputerach-hostach.

Aby uzyskać więcej informacji na temat monitorowania i konserwowania składniki sprzętowe hello urządzenia StorSimple Przejdź zbyt[składniki sprzętowe toomonitor usługi Menedżer StorSimple hello i stan](storsimple-monitor-hardware-status.md) i [StorSimple Wymiana sprzętu składnika](storsimple-hardware-component-replacement.md).

### <a name="high-availability-requirements-and-procedures-for-your-storsimple-device"></a>Wymagania dotyczące wysokiej dostępności i procedury dotyczące urządzenia StorSimple
Hello Przejrzyj następujące informacje, należy dokładnie tooensure hello wysokiej dostępności urządzenia StorSimple.

#### <a name="pcms"></a>PCMs
Urządzenia StorSimple obejmują nadmiarowe, wyłączania zasilania i chłodzenia modułów (PCMs). Każdy PCM ma za mało usługi tooprovide pojemności dla całej obudowy hello. tooensure wysokiej dostępności, zarówno PCMs musi być zainstalowany.

* Połącz z PCMs toodifferent power źródeł tooprovide dostępności, jeśli źródła zasilania nie powiedzie się.
* W przypadku niepowodzenia PCM żądanie zastępczy natychmiast.
* Usuwanie nie powiodło się PCM tylko wtedy, gdy masz hello zastąpienia i są gotowe tooinstall go.
* Nie usuwaj PCMs obu jednocześnie. Moduł PCM Hello zawiera hello modułu baterii kopii zapasowej. Usuwanie zarówno z hello PCMs spowoduje zamknięcie bez ochrony baterii i hello stan urządzenia nie zostaną zapisane. Aby uzyskać więcej informacji na temat baterii hello Przejdź zbyt[Obsługa hello kopii zapasowej baterii modułu](storsimple-battery-replacement.md#maintain-the-backup-battery-module).

#### <a name="controller-modules"></a>Moduły kontrolera
Urządzenia StorSimple obejmują moduły nadmiarowe, wyłączania kontrolera. Moduły kontrolera Hello działać w sposób aktywny/pasywny. W dowolnym momencie jeden moduł kontrolera jest aktywna i udostępnia usługi, podczas hello jest procesem pasywnym inny moduł kontrolera. Moduł kontrolera pasywnym Hello jest włączona i jest aktywna, jeśli moduł active kontrolera hello nie powiedzie się lub jest usunięte. Każdy moduł kontroler ma za mało usługi tooprovide pojemności dla całej obudowy hello. Zarówno modułów kontrolera musi być zainstalowany tooensure wysokiej dostępności.

* Upewnij się, czy obu modułów kontrolera są zainstalowane przez cały czas.
* Jeśli moduł kontrolera nie powiedzie się, żądanie zastępczy natychmiast.
* Usuń moduł kontrolera nie powiodło się tylko wtedy, gdy masz hello zastąpienia i są gotowe tooinstall go. Usunięcie modułu przez dłuższy czas wpłynie powietrza hello i dlatego hello chłodzenia hello systemu.
* Upewnij się, że hello sieci połączeń tooboth kontrolera moduły są identyczne i hello interfejsów sieciowych podłączonych ma konfiguracji sieciowej identyczne.
* Jeśli moduł kontrolera awarią lub koniecznością wymiany, upewnij się, że hello inny moduł kontroler jest w stanie aktywnym przed wymianą hello moduł kontrolera nie powiodło się. tooverify czy kontrolera jest aktywny, przejdź zbyt[Identyfikuj hello aktywnym kontrolerze na urządzeniu](storsimple-controller-replacement.md#identify-the-active-controller-on-your-device).
* Nie usuwaj obu modułów kontroler na powitania tym samym czasie. Jeśli kontroler trybu failover jest w toku, nie Zamknij moduł rezerwy kontrolera hello lub usunąć jej z obudowy hello.
* Przejściu w tryb failover kontrolera Zaczekaj co najmniej pięć minut przed usunięciem albo moduł kontrolera.

#### <a name="network-interfaces"></a>Interfejsy sieciowe
StorSimple urządzenia kontrolera modules ma cztery 1 GB i 10 dwa interfejsy sieci Gigabit Ethernet.

* Upewnij się, że hello sieci połączeń tooboth kontrolera moduły są identyczne, i interfejsy sieciowe hello, że hello kontrolera modułu interfejsy są połączone toohave konfiguracji sieci identyczne.
* Jeśli to możliwe, należy wdrożyć połączenia sieciowe w różnych przełączników dostępności usługi tooensure w zdarzeniu hello awaria urządzenia sieci.
* W przypadku odłączania tylko hello lub ostatnia pozostała hello interfejsu włączono interfejs iSCSI (z adresy IP przypisane), najpierw wyłącz interfejs hello, a następnie odłącz kable hello. Jeśli najpierw zostanie odłączone hello interfejsu, następnie spowoduje toofail aktywnym kontrolerze hello za pośrednictwem toohello pasywnym kontrolera. Jeśli kontroler pasywnym hello ma również odpowiedniego interfejsy odłączony, zarówno kontrolery hello zostanie uruchomiony wielokrotnie przed rozpoczęciem na jeden kontroler.
* Podłącz co najmniej dwie sieci toohello interfejsy danych z każdego modułu kontrolera.
* Po włączeniu Witaj dwie 10 GbE interfejsy wdrożyć tymi w ramach różnych przełączników.
* Jeśli to możliwe, użyj funkcji MPIO na tooensure serwerów, że serwery hello może tolerować łącza, sieci lub interfejsu.

Aby uzyskać więcej informacji na temat sieci Twojego urządzenia pod kątem wysokiej dostępności i wydajności za Przejdź[zainstalować do urządzenia StorSimple 8100](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) lub [zainstalować do urządzenia StorSimple 8600](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).

#### <a name="ssds-and-hdds"></a>Dyski SSD i dysków twardych
Urządzenia StorSimple obejmują dysków półprzewodnikowych (SSD) oraz stacje dysków twardych (HDD), które są chronione przy użyciu dublowanych miejsc do. Użyj miejsc dublowanych gwarantuje, że urządzenie hello będzie w stanie tootolerate hello awarii jednego lub więcej dysków SSD i dysków twardych.

* Upewnij się, że zainstalowano wszystkie moduły SSD i HDD.
* W przypadku niepowodzenia dysków SSD i HDD żądanie zastępczy natychmiast.
* Jeśli dysków SSD i HDD nie powiedzie się lub wymagana jest wymiana, upewnij się, czy usunąć tylko hello dysków SSD i HDD, która wymaga zastąpienia.
* Nie usuwaj więcej niż jeden dysków SSD i HDD systemu hello w dowolnym momencie w czasie.
  Awarii 2 lub więcej dysków określonego typu (dysk twardy, dysk SSD) lub niepowodzenie kolejnych w krótkim czasie może skutkować utratą danych nieprawidłowego działania i możliwości systemu. W takim przypadku [skontaktuj się z Microsoft Support](storsimple-contact-microsoft-support.md) Aby uzyskać pomoc.
* Podczas wymiany, monitorować hello **stan sprzętu** w hello **konserwacji** strony dla hello dysków w hello dyski SSD i dysków twardych. Stan zielony wyboru wskazuje, że dyski hello są w dobrej kondycji lub OK punktu czerwony wykrzyknik wskazuje, nie powiodło się dysków SSD i HDD.
* Zaleca się skonfigurowanie migawki w chmurze dla wszystkich woluminów należy tooprotect w przypadku awarii systemu.

#### <a name="ebod-enclosure"></a>Obudowa EBOD
Model urządzenia StorSimple 8600 obejmuje obudowa rozszerzony Bunch dla dysków (EBOD) w obudowie głównej toohello dodanie. EBOD zawiera kontrolery EBOD i stacje dysków twardych (HDD), które są chronione przy użyciu dublowane spacji. Użyj miejsc dublowanych gwarantuje, że urządzenie hello będzie w stanie tootolerate hello awarii jednego lub więcej dysków twardych. Hello obudowa EBOD jest podstawowy obudowy toohello połączonych za pośrednictwem nadmiarowych kabli SAS.

* Upewnij się, że oba EBOD obudowa kontrolera modułów kabli SAS i wszystkich dysków twardych hello są instalowane przez cały czas.
* Jeśli moduł EBOD obudowa kontrolera nie powiedzie się, żądanie zastępczy natychmiast.
* Jeśli moduł EBOD obudowa kontrolera nie powiedzie się, upewnij się, że hello inny moduł kontrolera jest aktywna, przed wymianą hello modułu nie powiodło się. tooverify czy kontrolera jest aktywny, przejdź zbyt[Identyfikuj hello aktywnym kontrolerze na urządzeniu](storsimple-controller-replacement.md#identify-the-active-controller-on-your-device).
* Podczas wymiany modułu EBOD kontrolera stale monitorować stan hello składnika hello hello usługi Menedżer StorSimple, uzyskując dostęp do **konserwacji** > **stan sprzętu**.
* Jeśli kabel SAS nie powiedzie się lub wymagana jest wymiana (Microsoft Support powinien być zaangażowany toomake takiego określenia), upewnij się, usunięcie tylko kabel SAS hello, który wymaga zastąpienia.
* Nie należy jednocześnie usuwać zarówno kabli SAS z systemu hello w dowolnym momencie w czasie.

### <a name="high-availability-recommendations-for-your-host-computers"></a>Zalecenia dotyczące wysokiej dostępności dla komputerów hostów
Uważnie przejrzyj te najlepsze rozwiązania w zakresie tooensure hello wysoką dostępność urządzenia StorSimple podłączonego tooyour hostów.

* Konfigurowanie StorSimple z [konfiguracje klastrów serwera plików z dwoma węzłami][1]. Przez usunięcie pojedynczego punktu awarii i tworzenia w nadmiarowość na powitania po stronie hosta, hello całe rozwiązanie staje się wysokiej dostępności.
* Użyj stale dostępnych udziałów (CA) z systemem Windows Server 2012 (protokół SMB 3.0) wysokiej dostępności w trybie failover hello kontrolerów magazynu. Aby uzyskać dodatkowe informacje dotyczące konfigurowania klastrów serwera plików i stale dostępnych udziałów w systemie Windows Server 2012, można znaleźć toothis [pokaz wideo](http://channel9.msdn.com/Events/IT-Camps/IT-Camps-On-Demand-Windows-Server-2012/DEMO-Continuously-Available-File-Shares).

## <a name="next-steps"></a>Następne kroki
* [Więcej informacji na temat limitów systemu StorSimple](storsimple-limits.md).
* [Dowiedz się, jak toodeploy rozwiązania StorSimple](storsimple-deployment-walkthrough-u2.md).

<!--Reference links-->
[1]: https://technet.microsoft.com/library/cc731844(v=WS.10).aspx
