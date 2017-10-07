---
title: "Konfiguracja urządzenia StorSimple hello aaaModify | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toouse hello tooreconfigure usługi Menedżer StorSimple urządzenia StorSimple, która została już wdrożona."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: bb679264-8d46-429c-9ef7-630dc3b4a423
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/19/2017
ms.author: v-sharos
ms.openlocfilehash: 10a54c191260bf1baba58d28cdbfa0ed72217f48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomodify-your-storsimple-device-configuration"></a>Użyj toomodify usługi Menedżer StorSimple hello konfiguracji urządzenia StorSimple
## <a name="overview"></a>Omówienie
Witaj klasycznego portalu Azure **Konfiguruj** strona zawiera wszystkie parametry hello urządzenia, które można skonfigurować na urządzeniu StorSimple, który jest zarządzany przez usługę Menedżer StorSimple. W tym samouczku opisano, jak używasz hello **Konfiguruj** hello tooperform strony następujących zadań na poziomie urządzeń:

* Zmodyfikuj ustawienia urządzenia 
* Zmodyfikuj ustawienia czasu 
* Zmodyfikuj ustawienia DNS 
* Modyfikowanie interfejsy sieciowe
* Zamień lub ponowne przypisywanie adresów IP

## <a name="modify-device-settings"></a>Zmodyfikuj ustawienia urządzenia
Ustawienia urządzenia Hello obejmują hello przyjazna nazwa urządzenia hello i hello opis urządzenia.

> [!NOTE] 
> Nie można zmodyfikować nazwy urządzenia hello w hello klasycznego portalu Azure. Zmiana nazwy urządzenia hello nie jest obsługiwane.

Urządzenia StorSimple, który jest połączony toohello usługi Menedżer StorSimple przypisano nazwę domyślną. Nazwa domyślna Hello zazwyczaj odzwierciedla hello numer seryjny urządzenia hello. Na przykład domyślna nazwa urządzenia jest 15 znaków, takich jak 8600 SHX0991003G44HT, wskazuje hello następujące czynności:

* **8600** — model urządzenia hello wskazuje.
* **SHX** — wskazuje hello produkcyjnym lokacji.
* **0991003** -wskazuje określony produkt.
* **G44HT**— Witaj toocreate zwiększany unikatowe numery seryjne są ostatnich 5 cyfr. Może być zestawem sekwencyjnych.

Można określić opis urządzenia. Opis urządzenia zwykle pomaga zidentyfikować hello właściciela i lokalizacji fizycznej hello hello urządzenia. pole opisu Hello musi zawierać mniej niż 256 znaków.

## <a name="modify-time-settings"></a>Zmodyfikuj ustawienia czasu
Urządzenie musi synchronizować czas w kolejności tooauthenticate z dostawcą usług magazynu w chmurze. Wybierz z listy rozwijanej hello strefy czasowej i określ tootwo serwery protokołu NTP (Network Time). podstawowy serwer NTP Hello jest wymagana i określono, jeśli używasz programu Windows PowerShell dla StorSimple tooconfigure urządzenia. Można określić domyślnego hello systemu Windows Server **time.windows.com** jako serwer NTP. Można wyświetlić konfiguracji hello do serwera podstawowego NTP za pośrednictwem hello klasycznego portalu Azure, ale muszą używać toochange interfejsu programu Windows PowerShell hello go.

Konfiguracja serwera NTP dodatkowej Hello jest opcjonalna. Możesz użyć hello klasycznego portalu tooconfigure pomocniczy serwer NTP. 

Podczas konfigurowania serwera NTP hello, upewnij się, że sieć zezwala toopass ruch NTP hello z sieci centrum danych toohello Internet. Podczas określania publicznego serwera NTP, użytkownik musi upewnić się, czy zapory sieciowe i inne urządzenia zabezpieczeń są skonfigurowane tooallow NTP ruchu tootravel tooand z hello spoza sieci. Jeśli ruch NTP dwukierunkowego nie jest dozwolone, należy użyć wewnętrzny serwer NTP (kontrolera domeny systemu Windows zapewnia tę funkcję). Jeśli urządzenie nie może zsynchronizować czasu, nie może być możliwe toocommunicate u swojego dostawcy magazynu w chmurze.

toosee listę serwerów NTP publiczne, przejdź toohello [Web Serwery NTP](http://support.ntp.org/bin/view/Servers/WebHome). 

### <a name="what-happens-if-hello-device-is-deployed-in-a-different-time-zone"></a>Co się stanie, jeśli urządzenie hello jest wdrażana w innej strefie czasowej?
Jeśli urządzenie hello jest wdrażana w innej strefie czasowej, strefa czasowa hello urządzenia zostanie zmieniona. Biorąc pod uwagę, że wszystkie zasady tworzenia kopii zapasowej hello Użyj strefy czasowej hello urządzenia, zasad tworzenia kopii zapasowych hello automatycznie dopasuje zgodnie z nową strefą czasową hello. Interwencja użytkownika nie jest wymagane.

## <a name="modify-dns-settings"></a>Zmodyfikuj ustawienia DNS
Serwer DNS jest używany, gdy urządzenie próbuje toocommunicate z dostawcą usług magazynu w chmurze. Wysokiej dostępności są wymagane tooconfigure zarówno hello podstawowego i hello pomocniczych serwerów DNS podczas wdrażania urządzenie początkowe hello. tooreconfigure hello podstawowy serwer DNS, konieczne będzie interfejsu programu Windows PowerShell hello toouse na urządzeniu StorSimple.

toomodify hello pomocniczy serwer DNS, można użyć hello klasycznego portalu Azure.

## <a name="modify-network-interfaces"></a>Modyfikowanie interfejsy sieciowe
Urządzenie ma sześć interfejsów sieciowych urządzenia, z których cztery są 1 GbE i dwa z nich są 10 GbE. Te interfejsy są oznaczone jako dane 0 – 5 danych. DANE 0, 1 danych, dane 4 i 5 danych są 1 GbE, a dane 2 i dane 3 10 GbE interfejsów.

Skonfiguruj **ustawienia interfejsu sieciowego** dla każdego toobe interfejsy hello używane. tooensure wysoką dostępność, zaleca się ma co najmniej dwa interfejsy iSCSI i dwa interfejsy włączoną obsługę chmury na urządzeniu. Firma Microsoft zaleca, ale nie wymagają wyłączone nieużywane interfejsów.

Po skonfigurowaniu wszystkich interfejsów sieciowych hello, skonfiguruj wirtualnego adresu IP (VIP).

Interfejs DATA 0 ma włączoną obsługę chmury domyślnie. Podczas konfigurowania dane 0, ma również tooconfigure wymagane dwie stałe adresy IP, po jednej dla każdego kontrolera. Te stałe adresy IP mogą być używane tooaccess kontrolery urządzeń hello bezpośrednio i są przydatne podczas instalowania aktualizacji na urządzeniu hello lub jeśli dostęp do kontrolerów hello hello w celu rozwiązywania problemów.

W StorSimple 8000 serii Update 1 hello metrykę routingu danych 0 ustawiono toohello najniższy; w związku z tym jeśli urządzenie działa StorSimple 8000 serii Update 1, cały ruch z chmury hello, zostaną przesłane za pośrednictwem interfejsu dane 0. Zwróć uwagę to, jeśli masz więcej niż jeden interfejs sieciowy z obsługą chmury na urządzeniu StorSimple.

> [!NOTE]
> Witaj, stałe adresy IP dla kontrolera hello są używane do obsługi hello aktualizacje toohello urządzenia. W związku z tym hello stałe adresy IP muszą być rutowalne i umożliwiać tooconnect toohello Internet.
> 
> 

Dla każdego interfejsu sieciowego są wyświetlane hello następujące parametry:

* **Szybkość** — nie można skonfigurować użytkownika parametru. DANE 0, 1 danych, dane 4 i 5 danych są zawsze 1 GbE, a dane 2 i dane 3 10 GbE interfejsów.
  
  > [!NOTE]
  > Szybkość i dupleks są zawsze auto negocjowane. Duże ramki nie są obsługiwane.
  > 
  > 
* **Stan interfejsu** — interfejs może być włączona lub wyłączona. Jeśli opcja jest włączona, urządzenia hello podejmie toouse hello interfejsu. Zaleca się włączenie tylko tych interfejsów, które są połączone toohello sieci i używane. Wyłącz wszystkie interfejsy, które nie są używane.
* **Typ interfejsu** — ten parametr umożliwia ruchu iSCSI tooisolate od ruchu magazynu w chmurze. Ten parametr może mieć jedną z następujących hello:
  
  * **Chmura włączone** — po włączeniu urządzenia hello użyje tego toocommunicate interfejsu hello chmury.
  * **iSCSI włączone** — po włączeniu urządzenia hello użyje tego interfejsu toocommunicate hello hosta iSCSI.
    
    Zalecamy izolowanie ruchu iSCSI od ruchu magazynu w chmurze. Należy również zauważyć, jeśli host jest w obrębie hello tej samej podsieci jako urządzenie, nie trzeba tooassign bramę; Jednak jeśli host znajduje się w innej podsieci niż urządzenia, konieczne będzie tooassign bramy.
* **Adres IP** — może to być IPv4 lub IPv6 lub oba. Interfejsy sieciowe urządzenia hello obsługuje zarówno hello IPv4, jak i rodzin adresów IPv6. Przy użyciu protokołu IPv4, należy określić adres IP 32-bitowych (*xxx.xxx.xxx.xxx*) w notacji dziesiętnej kropki. Podczas korzystania z protokołu IPv6, wystarczy podać prefiks 4-cyfrowego i 128-bitowy adres będą generowane automatycznie dla interfejsu sieci urządzenia na podstawie tego prefiksu.
* **Podsieci** — to odwołuje się toohello maskę podsieci i jest skonfigurowana za pośrednictwem interfejsu programu Windows PowerShell hello.
* **Brama** — jest to brama domyślna hello, które mają być używane przez ten interfejs podczas prób toocommunicate węzłów, które nie są dostępne w ramach hello tą samą przestrzenią adresów IP (podsieci). Witaj brama domyślna musi być w hello sam przestrzeni adresów (podsieć) jako adres IP interfejsu hello, zgodnie z ustaleniami hello maski podsieci.
* **Stały adres IP** — to pole jest dostępne tylko podczas konfigurowania hello dane 0 interfejsu. Dla operacji, takich jak aktualizacje lub rozwiązywania problemów z urządzeniem hello, może być konieczne tooconnect bezpośrednio toohello urządzenia kontrolera. Witaj stały adres IP może być używane tooaccess zarówno hello aktywne, jak i pasywnym kontrolera hello na urządzeniu.

Można ponownie skonfigurować kontrolera 0 i kontrolera 1 za pośrednictwem hello klasycznego portalu Azure.

> [!NOTE]
> * poprawne działanie tooensure, sprawdź szybkość interfejsu hello i dupleks na powitania przełącznika, który jest połączony interfejs każdego urządzenia. Interfejsy przełącznika negocjowanych albo z ani można skonfigurować dla Gigabit Ethernet (1000 MB/s) i być pełny dupleks. Interfejsy działających w niższych szybkościach lub półdupleksu spowoduje problemy z wydajnością.
> * toominimize zakłóceń i przestoje, zaleca się włączenie portfast na każdym hello przełącznika, które porty, które hello interfejsu sieci iSCSI, urządzenia będą łączyć się. Daje to pewność, że połączenie sieciowe może zostać szybko ustanowiona w przypadku hello trybu failover.
> 
> 

## <a name="swap-or-reassign-ips"></a>Zamień lub ponowne przypisywanie adresów IP
Obecnie Jeśli żadnego interfejsu sieciowego na kontrolera hello jest przypisany adres VIP, który jest używany (przez hello tego samego urządzenia lub innego urządzenia w sieci hello), kontrolera hello zakończy się niepowodzeniem, za pośrednictwem. Dlatego trzeba toofollow hello prawidłowe procedury, jeśli są wymiany adresów VIP hello urządzenia interfejsu sieciowego, ponieważ spowoduje utworzenie zduplikowanego sytuacji IP.

Wykonaj następujące kroki tooswap hello lub ponowne przypisywanie adresów VIP dla żadnego z interfejsów sieciowych hello hello:

#### <a name="tooreassign-ips"></a>tooreassign adresów IP
1. Wyczyść hello adres IP dla obu interfejsów.
2. Po hello adresy IP są wyczyszczone, należy przypisać nowe adresy IP hello toohello odpowiednich interfejsów.

## <a name="next-steps"></a>Następne kroki
* Dowiedz się, jak za[konfigurowanie wielościeżkowego wejścia/wyjścia dla urządzenia StorSimple](storsimple-configure-mpio-windows-server.md).
* Dowiedz się, jak za[Użyj hello tooadminister usługi Menedżer StorSimple, urządzenia StorSimple](storsimple-manager-service-administration.md).

