---
title: "Konfiguracja urządzenia serii StorSimple 8000 hello aaaModify | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toouse hello tooreconfigure usługi Menedżer StorSimple urządzenie zostało już wdrożone urządzenie StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/19/2017
ms.author: alkohli
ms.openlocfilehash: 79711b45eafe732c1eed1e562b05e3837fbc9d03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomodify-your-storsimple-device-configuration"></a>Użyj toomodify usługi Menedżer StorSimple urządzenia hello konfiguracji urządzenia StorSimple

## <a name="overview"></a>Omówienie

Witaj w portalu Azure **ustawienia urządzenia** części hello **ustawienia** blok zawiera wszystkie parametry hello urządzenia, które można skonfigurować na urządzeniu StorSimple, który jest zarządzany przez Menedżera urządzeń StorSimple Usługa. W tym samouczku opisano, jak używasz hello **ustawienia** hello tooperform bloku następujących zadań na poziomie urządzeń:

* Modyfikowanie przyjazna nazwa urządzenia
* Zmodyfikuj ustawienia czasu urządzenia
* Przypisz pomocniczy serwer DNS
* Modyfikowanie interfejsy sieciowe
* Zamień lub ponowne przypisywanie adresów IP

## <a name="modify-device-friendly-name"></a>Modyfikowanie przyjazna nazwa urządzenia

Można użyć nazwy urządzenia hello Azure toochange portalu hello i przypisz go unikatową przyjazną nazwę wybranego. Użyj hello **ustawienia ogólne** bloku na Twoje urządzenie toomodify hello przyjazna nazwa urządzenia. Witaj przyjazna nazwa może zawierać żadnych znaków i może zawierać maksymalnie 64 znaki.

> [!NOTE] 
> Nazwa urządzenia hello w portalu Azure hello można modyfikować tylko przed ukończeniem instalacji urządzenia hello. Po zakończeniu hello minimalnej konfiguracji urządzenia nie można zmienić nazwy urządzenia hello.

![Nazwa urządzenia jest ogólnie ustawienia](./media/storsimple-8000-modify-device-config/modify-general-settings3.png)

Urządzenia StorSimple, który jest połączony toohello usługi Menedżer StorSimple urządzenia przypisano nazwę domyślną. Nazwa domyślna Hello zazwyczaj odzwierciedla hello numer seryjny urządzenia hello. Na przykład domyślna nazwa urządzenia jest 15 znaków, takich jak 8600 SHX0991003G44HT, wskazuje hello następujące czynności:

* **8600** — model urządzenia hello wskazuje.
* **SHX** — wskazuje hello produkcyjnym lokacji.
* **0991003** -wskazuje określony produkt.
* **G44HT**— Witaj toocreate zwiększany unikatowe numery seryjne są ostatnich 5 cyfr. Może być zestawem sekwencyjnych.

## <a name="modify-device-description"></a>Zmodyfikuj opis urządzenia

Użyj hello **ustawienia ogólne** bloku w opisie urządzenia toomodify hello urządzenia.

![Opis urządzenia w obszarze Ustawienia ogólne](./media/storsimple-8000-modify-device-config/modify-general-settings4.png)

Opis urządzenia zwykle pomaga zidentyfikować hello właściciela i lokalizacji fizycznej hello hello urządzenia. pole opisu Hello musi zawierać mniej niż 256 znaków.

## <a name="modify-time-settings"></a>Zmodyfikuj ustawienia czasu

Urządzenie musi synchronizować czas w kolejności tooauthenticate z dostawcą usług magazynu w chmurze. Użyj hello **ustawienia ogólne** bloku na ustawienia czasu urządzenia toomodify hello urządzenia.

![Opis urządzenia w obszarze Ustawienia ogólne](./media/storsimple-8000-modify-device-config/modify-general-settings2.png)

 Wybierz strefę czasową z listy rozwijanej hello. Można określić tootwo serwery protokołu NTP (Network Time):

 - **Podstawowy serwer NTP** -hello konfiguracji jest wymagana i określono, jeśli używasz programu Windows PowerShell dla StorSimple tooconfigure urządzenia. Można określić domyślnego hello systemu Windows Server **time.windows.com** jako serwer NTP. Można wyświetlić konfiguracji hello do serwera podstawowego NTP za pośrednictwem hello portalu Azure, ale muszą używać toochange interfejsu programu Windows PowerShell hello go. Użyj hello `Set-HcsNTPClientServerAddress` polecenia cmdlet toomodify hello podstawowy serwer NTP urządzenia. Aby uzyskać więcej informacji Przejdź toosynxtax dla polecenia cmdlet [Set-HcsNTPClientServerAddress] (https://technet.microsoft.com/library/dn688138.aspx).

- **Pomocniczy serwer NTP** — Konfiguracja hello jest opcjonalne. Możesz użyć portalu tooconfigure hello pomocniczy serwer NTP.

Podczas konfigurowania serwera NTP hello, upewnij się, że sieć zezwala toopass ruch NTP hello z sieci centrum danych toohello Internet. Podczas określania publicznego serwera NTP, użytkownik musi upewnić się, czy zapory sieciowe i inne urządzenia zabezpieczeń są skonfigurowane tooallow NTP ruchu tootravel tooand z hello spoza sieci. Jeśli ruch NTP dwukierunkowego nie jest dozwolone, należy użyć wewnętrzny serwer NTP (kontrolera domeny systemu Windows zapewnia tę funkcję). Jeśli urządzenie nie może zsynchronizować czasu, nie może być możliwe toocommunicate u swojego dostawcy magazynu w chmurze.

toosee listę serwerów NTP publiczne, przejdź toohello [Web Serwery NTP](http://support.ntp.org/bin/view/Servers/WebHome).

### <a name="what-happens-if-hello-device-is-deployed-in-a-different-time-zone"></a>Co się stanie, jeśli urządzenie hello jest wdrażana w innej strefie czasowej?

Jeśli urządzenie hello jest wdrażana w innej strefie czasowej, strefa czasowa hello urządzenia zostanie zmieniona. Biorąc pod uwagę, że wszystkie zasady tworzenia kopii zapasowej hello Użyj strefy czasowej hello urządzenia, zasad tworzenia kopii zapasowych hello automatycznie dopasuje zgodnie z nową strefą czasową hello. Interwencja użytkownika nie jest wymagane.

## <a name="modify-dns-settings"></a>Zmodyfikuj ustawienia DNS

Serwer DNS jest używany, gdy urządzenie próbuje toocommunicate z dostawcą usług magazynu w chmurze. Użyj hello **ustawień sieciowych** bloku na tooview Twojego urządzenia i zmodyfikować ustawienia DNS hello skonfigurowane. 

![Ustawienia DNS w ustawieniach sieci](./media/storsimple-8000-modify-device-config/modify-network-settings1.png)

Wysokiej dostępności są wymagane tooconfigure zarówno hello podstawowego i hello pomocniczych serwerów DNS podczas wdrażania urządzenie początkowe hello.

**Podstawowy serwer DNS** -używanych hello środowiska Windows PowerShell dla StorSimple toofirst podczas instalacji początkowej hello określić hello podstawowy serwer DNS. Można ponownie skonfigurować podstawowy serwer DNS hello tylko za pośrednictwem interfejsu programu Windows PowerShell hello. Użyj hello `Set-HcsDNSClientServerAddress` polecenia cmdlet toomodify hello podstawowy serwer DNS urządzenia. Aby uzyskać więcej informacji, odwiedź toosynxtax [HcsDNSClientServerAddress zestaw](https://technet.microsoft.com/library/dn688138.aspx) polecenia cmdlet.

**Pomocniczy serwer DNS** -toomodify hello pomocniczy serwer DNS, użyj hello `Set-HcsDNSClientServerAddress` polecenia cmdlet w interfejsie programu Windows PowerShell hello hello urządzenia lub **ustawień sieciowych** bloku urządzenia StorSimple w hello Azure Portal.

toomodify hello pomocniczy serwer DNS w portalu Azure, wykonaj hello następujące kroki.

1. Przejdź tooyour usługi Menedżer urządzeń StorSimple. Z listy hello urządzenia wybierz i kliknij urządzenie.

2. W hello **ustawienia** bloku Przejdź zbyt**ustawienia urządzenia > sieci**. Spowoduje to otwarcie zapasowej hello **ustawień sieciowych** bloku. Kliknij przycisk **ustawienia DNS** kafelka. Zmodyfikuj adres IP serwera DNS hello dodatkowej.

    ![Modyfikowanie dodatkowej adderss IP serwera DNS](./media/storsimple-8000-modify-device-config/modify-secondary-dns1.png)

4. Na pasku poleceń hello, kliknij **zapisać** i po wyświetleniu monitu o potwierdzenie, kliknij przycisk **OK**.

    ![Zapisz i potwierdzenie zmian](./media/storsimple-8000-modify-device-config/modify-secondary-dns-2.png)



## <a name="modify-network-interfaces"></a>Modyfikowanie interfejsy sieciowe

Urządzenie ma sześć interfejsów sieciowych urządzenia, z których cztery są 1 GbE i dwa z nich są 10 GbE. Te interfejsy są oznaczone jako dane 0 – 5 danych. DANE 0, 1 danych, dane 4 i 5 danych są 1 GbE, a dane 2 i dane 3 10 GbE interfejsów.

Użyj hello **ustawień sieciowych** bloku tooconfigure każdego hello interfejsy toobe używane.

![Konfigurowanie interfejsów sieciowych za pośrednictwem ustawień sieci](./media/storsimple-8000-modify-device-config/modify-network-settings3.png)

tooensure wysoką dostępność, zaleca się ma co najmniej dwa interfejsy iSCSI i dwa interfejsy włączoną obsługę chmury na urządzeniu. Firma Microsoft zaleca, ale nie wymagają wyłączone nieużywane interfejsów.

Dla każdego interfejsu sieciowego są wyświetlane hello następujące parametry:

* **Szybkość** — nie można skonfigurować użytkownika parametru. DANE 0, 1 danych, dane 4 i 5 danych są zawsze 1 GbE, a dane 2 i dane 3 10 GbE interfejsów.
  
  > [!NOTE]
  > Szybkość i dupleks są zawsze auto negocjowane. Duże ramki nie są obsługiwane.
  
* **Stan interfejsu** — interfejs może być włączona lub wyłączona. Jeśli opcja jest włączona, urządzenia hello podejmie toouse hello interfejsu. Zaleca się włączenie tylko tych interfejsów, które są połączone toohello sieci i używane. Wyłącz wszystkie interfejsy, które nie są używane.
* **Typ interfejsu** — ten parametr umożliwia ruchu iSCSI tooisolate od ruchu magazynu w chmurze. Ten parametr może mieć jedną z następujących hello:
  
  * **Chmura włączone** — po włączeniu urządzenia hello użyje tego toocommunicate interfejsu hello chmury.
  * **iSCSI włączone** — po włączeniu urządzenia hello użyje tego interfejsu toocommunicate hello hosta iSCSI.
    
    Zalecamy izolowanie ruchu iSCSI od ruchu magazynu w chmurze. Należy również zauważyć, jeśli host jest w obrębie hello tej samej podsieci jako urządzenie, nie trzeba tooassign bramę; Jednak jeśli host znajduje się w innej podsieci niż urządzenia, konieczne będzie tooassign bramy.
* **Adres IP** — po skonfigurowaniu wszystkich interfejsów sieciowych hello, musisz skonfigurować wirtualnego adresu IP (VIP). Może to być IPv4 lub IPv6 lub oba. Interfejsy sieciowe urządzenia hello obsługuje zarówno hello IPv4, jak i rodzin adresów IPv6. Przy użyciu protokołu IPv4, należy określić adres IP 32-bitowych (*xxx.xxx.xxx.xxx*) w notacji dziesiętnej kropki. Podczas korzystania z protokołu IPv6, wystarczy podać prefiks 4-cyfrowego i 128-bitowy adres będą generowane automatycznie dla interfejsu sieci urządzenia na podstawie tego prefiksu.
* **Podsieci** — to odwołuje się toohello maskę podsieci i jest skonfigurowana za pośrednictwem interfejsu programu Windows PowerShell hello.
* **Brama** — jest to brama domyślna hello, które mają być używane przez ten interfejs podczas prób toocommunicate węzłów, które nie są dostępne w ramach hello tą samą przestrzenią adresów IP (podsieci). Witaj brama domyślna musi być w hello sam przestrzeni adresów (podsieć) jako adres IP interfejsu hello, zgodnie z ustaleniami hello maski podsieci.
* **Stały adres IP** — to pole jest dostępne tylko podczas konfigurowania hello dane 0 interfejsu. Dla operacji, takich jak aktualizacje lub rozwiązywania problemów z urządzeniem hello, może być konieczne tooconnect bezpośrednio toohello urządzenia kontrolera. Witaj stały adres IP może być używane tooaccess zarówno hello aktywne, jak i pasywnym kontrolera hello na urządzeniu.

> [!NOTE]
> * poprawne działanie tooensure, sprawdź szybkość interfejsu hello i dupleks na powitania przełącznika, który jest połączony interfejs każdego urządzenia. Interfejsy przełącznika negocjowanych albo z ani można skonfigurować dla Gigabit Ethernet (1000 MB/s) i być pełny dupleks. Interfejsy działających w niższych szybkościach lub półdupleksu spowoduje problemy z wydajnością.
> * toominimize zakłóceń i przestoje, zaleca się włączenie portfast na każdym hello przełącznika, które porty, które hello interfejsu sieci iSCSI, urządzenia będą łączyć się. Daje to pewność, że połączenie sieciowe może zostać szybko ustanowiona w przypadku hello trybu failover.

### <a name="configure-data-0"></a>Konfigurowanie danych 0

Interfejs DATA 0 ma włączoną obsługę chmury domyślnie. Podczas konfigurowania dane 0, ma również tooconfigure wymagane dwie stałe adresy IP, po jednej dla każdego kontrolera. Te stałe adresy IP mogą być używane tooaccess kontrolery urządzeń hello bezpośrednio i są przydatne podczas instalowania aktualizacji na urządzeniu hello lub jeśli dostęp do kontrolerów hello hello w celu rozwiązywania problemów.

Można ponownie skonfigurować hello kontrolerów IP za pomocą bloku ustawienia 0 danych hello stałej.

![Skonfiguruj interfejs sieci - DATA 0](./media/storsimple-8000-modify-device-config/modify-network-settings2.png)

> [!NOTE]
> Witaj, stałe adresy IP dla kontrolera hello są używane do obsługi hello aktualizacje toohello urządzenia. W związku z tym hello stałe adresy IP muszą być rutowalne i umożliwiać tooconnect toohello Internet.

### <a name="configure-data-1---data-5"></a>Konfigurowanie danych 1 - dane 5

Dla danych 1 - interfejsów sieciowych 5 danych, można skonfigurować wszystkie ustawienia sieciowe hello pokazane na powitania po zrzut ekranu:

![Skonfiguruj interfejsy sieciowe dane 1 - 5 danych](./media/storsimple-8000-modify-device-config/modify-network-settings4.png)


## <a name="swap-or-reassign-ips"></a>Zamień lub ponowne przypisywanie adresów IP

Obecnie Jeśli żadnego interfejsu sieciowego na kontrolera hello jest przypisany adres VIP, który jest używany (przez hello tego samego urządzenia lub innego urządzenia w sieci hello), kontrolera hello zakończy się niepowodzeniem, za pośrednictwem. Zamień lub ponowne przypisywanie adresów VIP dla urządzenia interfejsu sieciowego, należy postępować zgodnie prawidłowe procedury można tworzyć sytuacji zduplikowanego adresu IP.

Wykonaj następujące kroki tooswap hello lub ponowne przypisywanie adresów VIP dla żadnego z interfejsów sieciowych hello hello:

#### <a name="tooreassign-ips"></a>tooreassign adresów IP

1. Wyczyść hello adres IP dla obu interfejsów.
2. Po hello adresy IP są wyczyszczone, należy przypisać nowe adresy IP hello toohello odpowiednich interfejsów.

## <a name="next-steps"></a>Następne kroki

* Dowiedz się, jak za[konfigurowanie wielościeżkowego wejścia/wyjścia dla urządzenia StorSimple](storsimple-8000-configure-mpio-windows-server.md).
* Dowiedz się, jak za[Użyj hello tooadminister usługi Menedżera urządzeń StorSimple, urządzenia StorSimple](storsimple-8000-manager-service-administration.md).

