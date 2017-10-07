---
title: wymagania systemowe tablicy wirtualnych Azure StorSimple aaaMicrosoft | Dokumentacja firmy Microsoft
description: "Więcej informacji na temat wymagania programowe i sieciowe powitania dla macierzy wirtualnego StorSimple"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: ea1d3bca-e71b-453d-aa82-440d2638f5e3
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/17/2017
ms.author: alkohli
ms.openlocfilehash: 7a124873fdd806d409c7279851456e6347e7ec0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-system-requirements"></a>Wymagania systemowe macierzy wirtualnej StorSimple
## <a name="overview"></a>Omówienie
W tym artykule opisano wymagania systemowe hello tablica wirtualne Microsoft Azure StorSimple oraz hello magazynu klientów uzyskujących dostęp do tablicy hello. Firma Microsoft zaleca się przejrzenie informacji hello dokładnie przed wdrażanie systemu StorSimple, a następnie Odwołaj tooit w razie potrzeby podczas wdrażania kolejnych operacji.

wymagania systemowe Hello obejmują:

* **Wymagania dotyczące oprogramowania dla klientów magazynu** — w tym artykule opisano hello obsługiwanych platform wirtualizacji, przeglądarki sieci web, inicjatorzy iSCSI, SMB klientów, wymagania minimalne urządzenia wirtualnego i wszelkie dodatkowe wymagania dotyczące tych systemów operacyjnych.
* **Wymagania dotyczące sieci dla urządzenia StorSimple hello** — informacje na temat portów hello tego toobe potrzeby otwórz w Twojej tooallow zapory dla ruchu iSCSI, chmury lub zarządzania.

wymagania systemowe StorSimple Hello publikowane informacje w tym artykule dotyczą tooStorSimple tylko tablice wirtualnego.

* Dla urządzeń z serii 8000, przejdź zbyt[wymagania systemowe dla danego urządzenia z serii StorSimple 8000](storsimple-system-requirements.md).
* Dla urządzeń z serii 7000, przejdź zbyt[wymagania systemowe dla urządzenia StorSimple 5000 7000 serii](http://onlinehelp.storsimple.com/1_StorSimple_System_Requirements).

## <a name="software-requirements"></a>Wymagania dotyczące oprogramowania
wymagania dotyczące oprogramowania Hello zawierają informacje hello hello obsługiwane przeglądarki sieci web, wersji protokołu SMB, platformami wirtualizacji i wymagania dotyczące minimalnej urządzenia wirtualnego hello.

### <a name="supported-virtualization-platforms"></a>Platformy obsługiwane wirtualizacji
| **Funkcja hypervisor** | **Wersja** |
| --- | --- |
| Funkcja Hyper-V |Windows Server 2008 R2 z dodatkiem SP1 lub nowszy |
| VMware ESXi |5.5 lub nowszy |

### <a name="virtual-device-requirements"></a>Wymagania dotyczące urządzeń wirtualnych
| **Składnik** | **Wymaganie** |
| --- | --- |
| Minimalna liczba procesorów wirtualnych (rdzenie) |4 |
| Minimalna ilość pamięci (RAM) |8 GB <br> Serwer plików, 8 GB mniej niż 2 miliony plików i 16 GB 2-4 miliony plików|
| Miejsce na dysku<sup>1</sup> |Dysk systemu operacyjnego - 80 GB <br></br>Dysk danych — 500 GB too8 TB |
| Minimalna liczba interfejsów sieci |1 |
| Przepustowość minimalna Internet<sup>2</sup> |5 MB/s |

<sup>1</sup> — elastycznej obsługi administracyjnej

<sup>2</sup> — wymagania dotyczące sieci może się różnić w zależności od hello codzienne częstotliwości zmian danych. Na przykład jeśli urządzenie wymaga tooback 10 GB lub więcej zmian w ciągu dnia, następnie hello tworzenia codziennej kopii zapasowej za pośrednictwem połączenia 5 MB/s może zająć godziny too4.25 (Jeśli nie można skompresować lub deduplikowany hello danych).

### <a name="supported-web-browsers"></a>Obsługiwane przeglądarki sieci web
| **Składnik** | **Wersja** | **Dodatkowe wymagania dotyczące/uwagi** |
| --- | --- | --- |
| Przeglądarka Microsoft Edge |Najnowsza wersja | |
| Program Internet Explorer |Najnowsza wersja |Z programu Internet Explorer 11 |
| Google Chrome |Najnowsza wersja |Przetestowana Chrome 46 |

### <a name="supported-storage-clients"></a>Klienci obsługiwanego magazynu
Witaj, następujące wymagania dotyczące oprogramowania dotyczą hello inicjatorów iSCSI, które uzyskują dostęp do macierzy wirtualnego StorSimple (skonfigurowany jako serwer iSCSI).

| **Obsługiwane systemy operacyjne** | **Wersja wymagana** | **Dodatkowe wymagania dotyczące/uwagi** |
| --- | --- | --- |
| Windows Server |2008 R2 Z DODATKIEM SP1, 2012, 2012 R2 |StorSimple można tworzyć alokowane elastycznie i pełni woluminów. Nie można go tworzyć woluminów inicjowanych częściowo. Woluminy StorSimple iSCSI są obsługiwane tylko w przypadku: <ul><li>Proste woluminy na dyskach podstawowych systemu Windows.</li><li>Windows NTFS formatowania woluminu.</li> |

Witaj, następujące wymagania dotyczące oprogramowania dotyczą hello klientów protokołu SMB, które uzyskują dostęp do macierzy wirtualnego StorSimple (skonfigurowany jako serwer plików).

| **Wersja protokołu SMB** |
| --- |
| SMB 2.x |
| SMB 3.0 |
| SMB 3.02 |

> [!IMPORTANT]
> Nie Kopiuj i przechowywać pliki chronione przez serwer plików systemu Windows System szyfrowania plików (EFS) toohello tablicy wirtualnego StorSimple; Spowoduje to nieobsługiwaną konfiguracją. 
> 

### <a name="supported-storage-format"></a>Obsługiwany format przechowywania
Tylko magazynu obiektów blob Azure bloku hello jest obsługiwana. Stronicowe obiekty BLOB nie są obsługiwane. Więcej informacji [o blokowe i stronicowe obiekty BLOB](https://docs.microsoft.com/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs).

## <a name="networking-requirements"></a>Wymagania dotyczące sieci
Witaj poniższej tabeli wymieniono hello porty wymagające toobe otwarty w Twojej tooallow zapory iSCSI, SMB, w chmurze lub ruch związany z zarządzaniem. W tej tabeli *w* lub *przychodzących* odwołuje się toohello kierunek, w którym przychodzące żądania klientów dostępu urządzenia. *Limit* lub *wychodzących* odwołuje się toohello kierunek, w którym urządzenia StorSimple wysyła dane zewnętrznie, poza wdrożenia hello: na przykład wychodzących toohello Internet.

| **Nr portu<sup>1</sup>** | **Przychodzący lub wychodzący** | **Zakres portów** | **Wymagane** | **Uwagi** |
| --- | --- | --- | --- | --- |
| TCP 80 (HTTP) |limit |WAN |Nie |Wychodzący port jest używany do aktualizacji tooretrieve dostęp do Internetu. <br></br>Serwer proxy ruchu wychodzącego sieci web Hello jest konfigurowane przez użytkownika. |
| TCP 443 (HTTPS) |limit |WAN |Tak |Wychodzący port jest używany do uzyskiwania dostępu do danych w chmurze hello. <br></br>Serwer proxy ruchu wychodzącego sieci web Hello jest konfigurowane przez użytkownika. |
| UDP 53 (DNS) |limit |WAN |W niektórych przypadkach; Zobacz uwagi. |Ten port jest wymagany tylko wtedy, gdy używasz serwera DNS w Internecie. <br></br> Należy pamiętać, że wdrażania serwera plików, firma Microsoft zaleca używanie lokalnego serwera DNS. |
| UDP 123 (NTP) |limit |WAN |W niektórych przypadkach; Zobacz uwagi. |Ten port jest wymagany tylko wtedy, gdy używasz serwera NTP internetowego.<br></br> Należy zwrócić uwagę, jeżeli wdrażanie serwera plików, zaleca się synchronizowanie czasu z kontrolerów domeny usługi Active Directory. |
| TCP 80 (HTTP) |W |SIECI LAN |Tak |Jest to hello portu wejściowego dla lokalnego interfejsu użytkownika na urządzeniu StorSimple hello w celu zarządzania lokalnego. <br></br> Należy pamiętać, że dostęp do hello lokalnego interfejsu użytkownika za pośrednictwem protokołu HTTP spowoduje automatyczne przekierowanie tooHTTPS. |
| TCP 443 (HTTPS) |W |SIECI LAN |Tak |Jest to hello portu wejściowego dla lokalnego interfejsu użytkownika na urządzeniu StorSimple hello w celu zarządzania lokalnego. |
| 3260 TCP (iSCSI) |W |SIECI LAN |Nie |Ten port jest używany tooaccess danych za pośrednictwem interfejsu iSCSI. |

<sup>1</sup> nie portów przychodzących muszą toobe otwarte na hello publicznej sieci Internet.

> [!IMPORTANT]
> Upewnij się, czy Zapora hello nie zmodyfikować lub odszyfrować żaden ruch protokołu SSL między hello urządzenia StorSimple i Azure.
> 
> 

### <a name="url-patterns-for-firewall-rules"></a>Wzorce adresu URL dla reguł zapory
Administratorzy sieci można skonfigurować często zaawansowanych zapory oparte na powitania adresu URL wzorce toofilter hello reguły ruchu przychodzącego i hello ruch wychodzący. Sieci wirtualne tablicy i hello usługi Menedżer StorSimple urządzenia są zależne od innych aplikacji firmy Microsoft, takich jak usługi Azure Service Bus, Azure Active Directory kontroli dostępu konta magazynu i serwerach Microsoft Update. wzorce adresu URL Hello skojarzone z tymi aplikacjami można tooconfigure używanych reguł zapory. Jest ważne toounderstand, który wzorców adresów URL hello skojarzone z tymi aplikacjami można zmienić. Z kolei spowoduje wymagają toomonitor administratora sieci hello i zaktualizować reguł zapory dla Twojego urządzenia StorSimple, jak i w razie potrzeby. 

Firma Microsoft zaleca, aby ustawić regułach zapory dla ruchu wychodzącego, oparte na StorSimple liberally stałe adresy IP, w większości przypadków. Można jednak użyć hello informacje poniżej tooset zaawansowanych reguł zapory, które są potrzebne toocreate bezpiecznych środowiskach.

> [!NOTE]
> 
> * urządzenie Hello (źródło) adresów IP powinien być zawsze ustawiony interfejsów sieciowych z obsługą chmury hello tooall. 
> * docelowy Hello adresów IP powinna być ustawiona zbyt[zakresy IP centrum danych Azure](https://www.microsoft.com/en-us/download/confirmation.aspx?id=41653).
> 
> 

| Wzorzec URL | Składnik/funkcji |
| --- | --- |
| `https://*.storsimple.windowsazure.com/*`<br>`https://*.accesscontrol.windows.net/*`<br>`https://*.servicebus.windows.net/*` |Usługa menedżera urządzenia StorSimple<br>Usługa kontroli dostępu<br>Azure Service Bus |
| `http://*.backup.windowsazure.com` |Rejestracja urządzenia |
| `http://crl.microsoft.com/pki/*`<br>`http://www.microsoft.com/pki/*` |Odwoływanie certyfikatów |
| `https://*.core.windows.net/*`<br>`https://*.data.microsoft.com`<br>`http://*.msftncsi.com` |Monitorowanie i kontami magazynu Azure |
| `http://*.windowsupdate.microsoft.com`<br>`https://*.windowsupdate.microsoft.com`<br>`http://*.update.microsoft.com`<br> `https://*.update.microsoft.com`<br>`http://*.windowsupdate.com`<br>`http://download.microsoft.com`<br>`http://wustat.windows.com`<br>`http://ntservicepack.microsoft.com` |Serwerów Microsoft Update<br> |
| `http://*.deploy.akamaitechnologies.com` |Akamai CDN |
| `https://*.partners.extranet.microsoft.com/*` |Pakiet pomocy technicznej |
| `http://*.data.microsoft.com ` |Usługa telemetrii w systemie Windows, zobacz hello [aktualizacja obsługi klienta i dane telemetryczne diagnostycznych](https://support.microsoft.com/en-us/kb/3068708) |

## <a name="next-step"></a>Następny krok
* [Przygotowanie toodeploy portalu hello tablica wirtualnego StorSimple](storsimple-virtual-array-deploy1-portal-prep.md)

