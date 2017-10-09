---
title: "aaaPowerShell do zarządzania urządzeniami StorSimple | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse środowiska Windows PowerShell dla StorSimple toomanage urządzenia StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 0ff3bb0d-897a-4676-bdcb-402c2628dac5
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/18/2016
ms.author: alkohli@microsoft.com
ms.openlocfilehash: 1adcbb8bb89e3e3b4f328aac198690476c2a78cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-windows-powershell-for-storsimple-tooadminister-your-device"></a>Używanie programu Windows PowerShell dla StorSimple tooadminister urządzenia z systemem
## <a name="overview"></a>Omówienie
Program Windows PowerShell dla StorSimple udostępnia interfejs wiersza polecenia służącego toomanage urządzenia Microsoft Azure StorSimple. Jak nazwa hello sugeruje, jest oparty na programie Windows PowerShell, interfejsu wiersza polecenia, który korzysta z wbudowanej w ograniczonego obszaru działania. Z perspektywy hello hello użytkownika w wierszu polecenia hello ograniczonego obszaru działania jest wyświetlany jako ograniczona wersja programu Windows PowerShell. Przy zachowaniu niektórych hello podstawowe funkcje programu Windows PowerShell, ten interfejs ma dodatkowe dedykowanych poleceń cmdlet, które są przeznaczone dla zarządzania urządzenia Microsoft Azure StorSimple. 

W tym artykule opisano hello środowiska Windows PowerShell dla funkcji StorSimple, w tym, jak można łączyć interfejsu toothis oraz zawiera łącza toostep po kroku procedury lub przepływów pracy, które można wykonywać przy użyciu tego interfejsu. przepływy pracy Hello obejmują jak tooregister urządzenia, skonfiguruj interfejs sieciowy hello na urządzeniu, zainstaluj aktualizacje, które wymagają hello toobe urządzenia w trybie konserwacji, zmienić stan urządzenia hello, i rozwiązać wszelkie napotkane problemy, które mogą wystąpić.

Po przeczytaniu tego artykułu, będą mieć możliwość:

* Podłącz urządzenie StorSimple tooyour przy użyciu programu Windows PowerShell dla urządzenia StorSimple.
* Administrowanie urządzenia StorSimple przy użyciu programu Windows PowerShell dla urządzenia StorSimple.
* Uzyskaj pomoc w programie Windows PowerShell dla StorSimple.

> [!NOTE]
> * Program Windows PowerShell dla StorSimple polecenia cmdlet pozwalają toomanage urządzenia StorSimple z konsoli szeregowej lub zdalnie za pośrednictwem komunikacji zdalnej programu Windows PowerShell. Aby uzyskać więcej informacji na temat każdego hello poszczególnych poleceń cmdlet, które mogą być używane w tym interfejsie Przejdź zbyt[referencyjnej poleceń cmdlet środowiska Windows PowerShell dla urządzenia StorSimple](https://technet.microsoft.com/library/dn688168.aspx).
> * polecenia cmdlet programu Azure PowerShell StorSimple Hello są inną kolekcję poleceń cmdlet, które umożliwiają tooautomate poziom usługi StorSimple i zadania migracji z wiersza polecenia hello. Aby uzyskać więcej informacji na temat hello poleceń cmdlet programu Azure PowerShell dla urządzenia StorSimple Przejdź toohello [dokumentacji poleceń cmdlet Azure StorSimple](/powershell/module/azure/?view=azuresmps-3.7.0).
> 
> 

Aby dostęp do hello środowiska Windows PowerShell dla urządzenia StorSimple przy użyciu jednej z następujących metod hello:

* [Łączenie z konsolą szeregową urządzenia tooStorSimple](#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console)
* [Połączyć się zdalnie tooStorSimple przy użyciu programu Windows PowerShell](#connect-remotely-to-storsimple-using-windows-powershell-for-storsimple)

## <a name="connect-toowindows-powershell-for-storsimple-via-hello-device-serial-console"></a>Łączenie tooWindows środowiska PowerShell dla urządzenia StorSimple za pośrednictwem konsoli szeregowej urządzenia hello
Możesz [Pobierz program PuTTY](http://www.putty.org/) lub podobnych emulacji terminala oprogramowania tooconnect tooWindows programu PowerShell dla StorSimple. Należy tooconfigure PuTTY w szczególności tooaccess hello urządzenia Microsoft Azure StorSimple. Witaj poniższe tematy zawierają szczegółowe kroki dotyczące tooconfigure PuTTy i podłącz urządzenie toohello. Także opisano różne opcje menu konsoli szeregowej hello.

### <a name="putty-settings"></a>Ustawienia programu PuTTY
Należy upewnić się, że po interfejsu programu Windows PowerShell toohello tooconnect ustawienia programu PuTTY z konsoli szeregowej hello hello.

#### <a name="tooconfigure-putty"></a>tooconfigure programu PuTTY
1. W hello PuTTY **ponowna konfiguracja** okno dialogowe, w hello **kategorii** okienku wybierz **klawiatury**.
2. Upewnij się, że hello następujące opcje są zaznaczone (są hello ustawienia domyślne po rozpoczęciu nowej sesji). 
   
   | Element klawiatury | Wybierz pozycję |
   | --- | --- |
   | Klawisza |Formant-? (127) |
   | Strona główna i na końcu kluczy |Standardowa |
   | Klawisze funkcyjne i klawiatury numerycznej |ESC [n ~ |
   | Stan początkowy kluczy kursora |Normalny |
   | Początkowy stan numerycznej |Normalny |
   | Włącz funkcje dodatkowe klawiatury |Formant Alt różni się od AltGr |
   
    ![Obsługiwane ustawienia programu Putty](./media/storsimple-windows-powershell-administration/IC740877.png)
3. Kliknij przycisk **Zastosuj**.
4. W hello **kategorii** okienku wybierz **tłumaczenia**.
5. W hello **zestaw znaków zdalnego** pola listy, wybierz opcję **UTF-8**.
6. W obszarze **Obsługa znaków Rysowanie linii**, wybierz pozycję **punktów kodowych Unicode Użyj Rysowanie linii**. Witaj poniższej ilustracji przedstawiono hello poprawne opcje PuTTY.
   
    ![Ustawienia programu Putty UTF](./media/storsimple-windows-powershell-administration/IC740878.png)
7. Kliknij przycisk **Zastosuj**.

Można teraz używać konsoli szeregowej urządzenia toohello PuTTY tooconnect, wykonując następujące kroki hello.

[!INCLUDE [storsimple-use-putty](../../includes/storsimple-use-putty.md)]

### <a name="about-hello-serial-console"></a>O hello konsoli szeregowej
Gdy uzyskujesz dostęp do interfejsu programu Windows PowerShell hello urządzenia StorSimple za pośrednictwem konsoli szeregowej hello są prezentowane komunikat transparentu, następuje opcji menu. 

wiadomości powitania Transparent zawiera podstawowe informacje o urządzeniu StorSimple, takich jak hello model, nazwę, wersję zainstalowanego oprogramowania i stanu hello kontrolera, które uzyskują dostęp do. następujące obraz powitania przedstawiono przykład komunikat transparentu.

![Komunikat transparentu szeregowe](./media/storsimple-windows-powershell-administration/IC741098.png)

> [!IMPORTANT]
> Można użyć tooidentify komunikat transparentu hello, czy kontroler hello są połączone toois aktywny i pasywne.
> 
> 

Po pokazuje obraz powitania hello różnych opcji w obszarze działania, które są dostępne w menu konsoli szeregowej hello.

![Zarejestruj urządzenie 2](./media/storsimple-windows-powershell-administration/IC740906.png)

Możesz wybrać hello następujące ustawienia:

1. **Zaloguj się przy użyciu pełnego dostępu** ta opcja umożliwia toohello tooconnect (z właściwymi poświadczeniami hello) **SSAdminConsole** obszaru działania na kontrolerze lokalne powitania. (kontroler lokalne powitania jest hello kontroler, który obecnie uzyskują dostęp do za pośrednictwem konsoli szeregowej hello urządzenia StorSimple). Tę opcję można również tooallow tooaccess Microsoft Support nieograniczony tootroubleshoot obszaru działania (sesji pomocy technicznej) wszelkie problemy dostępnego urządzenia. Po wybraniu opcji 1 toolog na można zezwolić inżynier Microsoft Support hello tooaccess nieograniczony obszaru działania przez uruchomienie konkretnego polecenia cmdlet. Aby uzyskać więcej informacji, zobacz zbyt[rozpocząć sesję pomocy technicznej](storsimple-contact-microsoft-support.md#start-a-support-session-in-windows-powershell-for-storsimple).
2. **Zaloguj się na kontrolerze toopeer z pełnym dostępem** ta opcja jest hello takie same jak opcja 1, z tą różnicą, że możesz połączyć (z właściwymi poświadczeniami hello) toohello **SSAdminConsole** obszaru działania na powitania równorzędnej kontrolera. Ponieważ urządzenia StorSimple hello jest urządzeniem wysokiej dostępności z dwoma kontrolerami w konfiguracji aktywny / pasywny, równorzędnej odwołuje się toohello inny kontroler w hello urządzenia, które chcesz uzyskać dostęp za pośrednictwem konsoli szeregowej hello).
   Podobne toooption 1, ta opcja może być również używane tooallow Microsoft Support tooaccess bez ograniczeń w obszarze działania na kontrolerze elementu równorzędnego.
3. **Połącz z ograniczonym dostępem** ta opcja jest używana tooaccess interfejsu programu Windows PowerShell w trybie ograniczonym. Nie monit o poświadczenia dostępu. Ta opcja łączy tooa więcej ograniczonym obszarem działania w porównaniu toooptions 1 i 2.  Niektóre zadania hello, które są dostępne za pośrednictwem opcja 1 który **nie* można wykonać w tym obszarze działania są:
   
   * Resetowanie ustawień fabrycznych toohello
   * Zmień hasło hello
   * Włącz lub wyłącz dostęp do pomocy technicznej
   * Stosowanie aktualizacji
   * Instalowanie poprawek 

    > [!NOTE]
    > Jeśli pamiętasz hasła administratora urządzenia hello i nie można połączyć za pomocą opcji 1 lub 2 jest opcja hello preferowany.

4. **Zmień język** ta opcja umożliwia język wyświetlania hello toochange hello interfejsu programu Windows PowerShell. obsługiwane języki Hello są angielski, japoński, rosyjski, francuski, koreański Południowa, hiszpański, włoski, niemiecki, chiński i portugalski — Brazylia.

## <a name="connect-remotely-toostorsimple-using-windows-powershell-for-storsimple"></a>Połączyć się zdalnie tooStorSimple przy użyciu programu Windows PowerShell dla urządzenia StorSimple
Można użyć urządzenia StorSimple tooyour tooconnect komunikacji zdalnej programu Windows PowerShell. Po podłączeniu w ten sposób, nie będą widzieć menu. (Możesz zobaczyć menu w tylko w przypadku używania konsoli szeregowej hello na powitania tooconnect urządzenia. Połączenie zdalne przejście bezpośrednio toohello równoważne "opcja 1 — pełny dostęp" na konsoli szeregowej hello.) Za pomocą komunikacji zdalnej programu Windows PowerShell należy połączyć tooa określonego obszaru działania. Można również określić język wyświetlania hello. 

Witaj język wyświetlania jest niezależny od języka hello, który należy określić przy użyciu hello **Zmień język** opcję w menu konsoli szeregowej hello. Ustawienia regionalne hello urządzenia hello nawiązujesz połączenie z, jeśli nie zostanie określona automatycznie pobierze zdalnego programu PowerShell.

> [!NOTE]
> Jeśli pracujesz z hostów wirtualnych Microsoft Azure i urządzenia wirtualnego StorSimple, można użyć programu Windows PowerShell usług zdalnych i hello hosta wirtualnego tooconnect toohello urządzenia wirtualnego. Jeśli w lokalizacji udział na hoście hello, na które toosave informacje z sesji środowiska Windows PowerShell hello, należy zwrócić uwagę, że tego powitalne wszyscy główna zawiera tylko użytkownicy uwierzytelnieni. W związku z tym jeśli zdefiniowano hello tooallow dostępu osoby, połączenie bez podania poświadczeń hello nieuwierzytelnione anonimowe podmiot zabezpieczeń, który będzie używany i zostanie wyświetlony komunikat o błędzie. host musi włączyć hello konta gościa, a następnie nadaj hello gościa konta pełny dostęp toohello udziału lub udostępnić ten problem, na powitania toofix należy określić prawidłowe poświadczenia wraz z hello polecenia cmdlet programu Windows PowerShell.
> 
> 

Można użyć protokołu HTTP lub HTTPS tooconnect za pośrednictwem komunikacji zdalnej programu Windows PowerShell. Użyj instrukcji hello w hello następujące samouczki:

* [Połącz zdalnie przy użyciu protokołu HTTP](storsimple-remote-connect.md#connect-through-http)
* [Połącz przy użyciu protokołu HTTPS](storsimple-remote-connect.md#connect-through-https)

## <a name="connection-security-considerations"></a>Zagadnienia dotyczące zabezpieczeń połączenia
Podczas decydowania jak tooWindows tooconnect programu PowerShell dla StorSimple, należy wziąć pod uwagę następujące hello:

* Łączenie bezpośrednio toohello konsoli szeregowej urządzenia jest bezpieczne, ale nie jest łączącego konsoli szeregowej toohello za pośrednictwem przełączników sieciowych. Należy uważać na powitania ryzyko związane z zabezpieczeniami podczas łączenia seryjny toodevice za pośrednictwem przełączników sieciowych.
* Łączących się za pośrednictwem sesji HTTP może oferować lepsze bezpieczeństwo niż łączących się za pośrednictwem konsoli szeregowej hello za pośrednictwem sieci. Chociaż nie jest to najbezpieczniejsza metoda hello, jest dopuszczalne w zaufanych sieciach.
* Łączących się za pośrednictwem sesji HTTPS jest hello najbardziej bezpieczne i hello zalecana opcja.

## <a name="administer-your-storsimple-device-using-windows-powershell-for-storsimple"></a>Administrowanie urządzenia StorSimple przy użyciu programu Windows PowerShell dla urządzenia StorSimple
Witaj poniższej tabeli przedstawiono podsumowanie wszystkich hello typowych zadań zarządzania i złożonych przepływów pracy, które mogą być wykonywane w ramach interfejsu programu Windows PowerShell hello urządzenia StorSimple. Aby uzyskać więcej informacji na temat każdego przepływu pracy kliknij przycisk hello odpowiedni wpis w tabeli hello.

#### <a name="windows-powershell-for-storsimple-workflows"></a>Program Windows PowerShell dla StorSimple przepływy pracy
| Jeśli chcesz toodo, to... | Użyj tej procedury. |
| --- | --- |
| Zarejestruj urządzenie |[Konfigurowanie i rejestrowanie urządzenia hello przy użyciu programu Windows PowerShell dla urządzenia StorSimple](storsimple-deployment-walkthrough.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple) |
| Konfigurowanie serwera proxy sieci Web</br>Wyświetl ustawienia serwera proxy sieci web |[Skonfiguruj serwer proxy sieci web dla urządzenia StorSimple](storsimple-configure-web-proxy.md) |
| Zmodyfikuj ustawienia interfejsu sieciowego 0 danych na urządzeniu |[Modyfikowanie danych interfejs sieciowy 0 dla urządzenia StorSimple](storsimple-modify-data-0.md) |
| Zatrzymaj kontrolera </br> Ponowne uruchamianie lub zamykanie kontrolera </br> Wyłącz urządzenia</br>Zresetuj ustawienia domyślne toofactory urządzenia hello |[Zarządzanie kontrolerami urządzenia](storsimple-manage-device-controller.md) |
| Zainstaluj aktualizacje trybu konserwacji i poprawki |[Aktualizowanie urządzenia](storsimple-update-device.md) |
| Przejście do trybu konserwacji </br>Zamknij tryb konserwacji |[Tryby urządzenia StorSimple](storsimple-device-modes.md) |
| Utwórz pakiet pomocy technicznej</br>Odszyfruj i Edytuj pakiet pomocy technicznej |[Tworzenie i zarządzanie nimi pakietu obsługi](storsimple-create-manage-support-package.md) |
| Rozpocznij sesję pomocy technicznej</br> |[Rozpocznij sesję pomocy technicznej w programie Windows PowerShell dla urządzenia StorSimple](storsimple-create-manage-support-package.md#manually-create-a-support-package) |

## <a name="get-help-in-windows-powershell-for-storsimple"></a>Uzyskaj pomoc w programie Windows PowerShell dla urządzenia StorSimple
W programie Windows PowerShell dla urządzenia StorSimple polecenia cmdlet pomoc jest dostępna. Online, aktualnych wersji Pomocy jest również dostępna, którego można użyć tooupdate hello pomoc w Twoim systemie.

Uzyskiwanie pomocy w tym interfejsie jest podobne toothat w programie Windows PowerShell, a większość hello pomocy dotyczące poleceń cmdlet będzie działać. Pomoc dla środowiska Windows PowerShell online można znaleźć w bibliotece TechNet hello: [skryptów programu Windows PowerShell](http://go.microsoft.com/fwlink/?LinkID=108518).

Witaj poniżej znajduje się krótki opis typów hello pomocy dla tego interfejsu programu Windows PowerShell, w tym, jak tooupdate hello pomocy.

#### <a name="tooget-help-for-a-cmdlet"></a>tooget pomocy dla polecenia cmdlet
* tooget pomocy dla polecenia cmdlet lub funkcji, hello Użyj następującego polecenia:`Get-Help <cmdlet-name>`
* tooget pomocy online dla każdego polecenia cmdlet, za pomocą poprzedniego polecenia cmdlet hello hello `-Online` parametru:`Get-Help <cmdlet-name> -Online`
* Aby uzyskać pełną pomoc, można użyć hello `–Full` parametru i przykłady, użyj hello `–Examples` parametru.

#### <a name="tooupdate-help"></a>tooupdate pomocy
Można łatwo aktualizować hello pomocy hello interfejsu programu Windows PowerShell. Wykonaj hello następujące kroki tooupdate hello pomoc w Twoim systemie.

#### <a name="tooupdate-cmdlet-help"></a>polecenia cmdlet tooupdate pomocy
1. Uruchom program Windows PowerShell z hello **Uruchom jako administrator** opcji.
2. Witaj wiersza polecenia wpisz:`Update-Help`
3. Witaj zaktualizowane zostaną zainstalowane pliki pomocy.
4. Po hello pliki pomocy zostały zainstalowane, wpisz: `Get-Help Get-Command`. Spowoduje to wyświetlenie listy poleceń cmdlet, dla których jest dostępna Pomoc.

> [!NOTE]
> tooget listę wszystkich hello poleceń cmdlet dostępnych w obszarze działania, zaloguj się w odpowiedniej opcji menu toohello i uruchom hello `Get-Command` polecenia cmdlet.
> 
> 

## <a name="next-steps"></a>Następne kroki
Jeśli wystąpią problemy z urządzeniem StorSimple podczas wykonywania jednej z hello powyżej przepływy pracy, zobacz zbyt[narzędzia do rozwiązywania problemów z wdrożeniami StorSimple](storsimple-troubleshoot-deployment.md#tools-for-troubleshooting-storsimple-deployments).

