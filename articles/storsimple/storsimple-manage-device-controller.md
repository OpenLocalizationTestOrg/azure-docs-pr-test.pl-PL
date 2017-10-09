---
title: "Kontrolery urządzeń StorSimple aaaManage | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toostop, uruchom ponownie, zamknij lub zresetować kontrolerów urządzenia StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 4ee989d0-956f-4c14-951e-fd4e490ea09d
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/11/2016
ms.author: alkohli
ms.openlocfilehash: 9a86aa0f4a8fd96c36df206774972602c47a49a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-storsimple-device-controllers"></a>Zarządzanie kontrolerów urządzenia StorSimple
## <a name="overview"></a>Omówienie
W tym samouczku opisano hello różne operacje, które mogą być wykonywane na kontrolerach urządzenia StorSimple. kontrolery Hello w urządzeniu StorSimple są kontrolery nadmiarowy (peer) w konfiguracji aktywny / pasywny. W danym momencie tylko jeden kontroler jest aktywna i przetwarza wszystkie operacje hello dysku i sieci. Witaj inny kontroler jest w trybie pasywnym. W przypadku niepowodzenia hello aktywnym kontrolerze kontrolera pasywnym hello staje się aktywny automatycznie.

Ten samouczek zawiera kontrolery urządzeń hello toomanage instrukcje krok po kroku przy użyciu:

* **Kontrolery** sekcji hello **konserwacji** strony w hello usługi Menedżer StorSimple
* Program Windows PowerShell dla StorSimple.

Zaleca się zarządzanie hello kontrolery urządzeń za pomocą usługi Menedżer StorSimple hello. Jeśli akcję można wykonać tylko przy użyciu programu Windows PowerShell dla urządzenia StorSimple, samouczek hello sprawia, że je zapisać.

Po przeczytaniu tego samouczka, będą mieć możliwość:

* Ponowne uruchamianie lub zamykanie kontrolera urządzenia StorSimple
* Wyłącz urządzenia StorSimple
* Resetuj domyślne toofactory urządzenia StorSimple

## <a name="restart-or-shut-down-a-single-controller"></a>Ponowne uruchamianie lub zamykanie jednego kontrolera
Zamknięcie lub ponowne uruchomienie kontrolera nie jest wymagana w ramach normalnego działania. Operacji zamknięcia na kontrolerze jednego urządzenia są często używane tylko w przypadkach, w których wymagana jest wymiana składnik sprzętowy urządzenia nie powiodło się. Ponowne uruchomienie kontrolera może być konieczne również w sytuacji, w których wpływ na wydajność w nadmiernego wykorzystania pamięci lub nieprawidłowo kontrolera. Możesz także toorestart kontrolera po wymianie pomyślne kontrolera, jeśli chcesz, aby tooenable i zastąpione hello kontroler testów.

Ponowne uruchamianie urządzenia nie jest inicjatory destrukcyjne tooconnected, przy założeniu, że jest dostępny kontroler pasywnym hello. Jeśli pasywnym kontrolera jest niedostępny lub ją wyłączyć, ponowne uruchomienie hello active kontroler może spowodować hello przerwy w świadczeniu usługi i przestoje.

> [!IMPORTANT]
> * **Działającego kontrolera powinien nigdy nie zostać usunięty, ponieważ skutkowałoby to utratą nadmiarowości i zwiększone ryzyko przestoju.**
> * Witaj Poniższa procedura ma zastosowanie tylko toohello urządzenia fizycznego StorSimple. Aby dowiedzieć się jak toostart, zatrzymywanie i ponowne uruchomienie urządzenia wirtualnego hello, zobacz [pracy z urządzeniem wirtualnym hello](storsimple-virtual-device-u2.md#work-with-the-storsimple-virtual-device).
> 
> 

Można ponownie uruchomić lub zamknąć kontrolera jednego urządzenia za pomocą hello klasycznego portalu Azure usługi Menedżer StorSimple hello lub środowiska Windows PowerShell dla urządzenia StorSimple

Wykonaj kontrolerów urządzeń z klasycznego portalu Azure, hello toomanage hello następujące kroki.

#### <a name="toorestart-or-shut-down-a-controller-in-classic-portal"></a>toorestart lub zamykania kontrolera w klasycznym portalu
1. Przejdź za**urządzenia > Konserwacja**.
2. Przejdź za**stan sprzętu** i sprawdź, czy stan hello obu kontrolerów hello na urządzeniu jest **dobra kondycja**.
   
    ![Sprawdź, czy kontrolery urządzeń StorSimple są w dobrej kondycji](./media/storsimple-manage-device-controller/IC766017.png)
3. Od dołu hello hello **konserwacji** kliknij przycisk **Zarządzaj kontrolerami**.
   
    ![Zarządzanie kontrolerami urządzenia StorSimple](./media/storsimple-manage-device-controller/IC766018.png)</br>
   
   > [!NOTE]
   > Jeśli nie widzisz **Zarządzaj kontrolerami**, wówczas należy tooinstall aktualizacji. Aby uzyskać więcej informacji, zobacz [aktualizacja urządzenia StorSimple](storsimple-update-device.md).
   > 
   > 
4. W hello **Zmień ustawienia kontrolera** okna dialogowego pozycję hello następujące:
   
   1. Z hello **Wybierz kontroler** listy rozwijanej, wybierz hello kontrolera, które mają toomanage. Opcje Hello są kontrolera 0 i kontrolera 1. Te kontrolery są również identyfikowane jako aktywnych lub pasywnych.
      
      > [!NOTE]
      > Nie można zarządzać kontrolera, jeśli jest niedostępny lub włączenia wyłączone i nie zostanie wyświetlony na liście rozwijanej hello.
      > 
      > 
   2. Z hello **wybierz akcję** listy rozwijanej wybierz pozycję **ponowne uruchomienie kontrolera** lub **Zamknij kontroler**.
      
       ![Uruchom ponownie kontroler pasywnym urządzenia StorSimple](./media/storsimple-manage-device-controller/IC766020.png)
   3. Kliknij ikonę znacznika wyboru hello ![Ikona znacznika wyboru](./media/storsimple-manage-device-controller/IC740895.png).

To spowoduje ponowne uruchamianie lub zamykanie hello kontrolera. Hello w poniższej tabeli przedstawiono szczegóły hello co się stanie, w zależności od opcji hello dokonanym w hello **Zmień ustawienia kontrolera** okno dialogowe.  

| Wybór # | Jeśli chcesz... | Dzieje się tak. |
| --- | --- | --- |
| 1. |Uruchom ponownie kontroler pasywnym hello. |Zostanie utworzone zadanie toorestart hello kontrolera, a użytkownik otrzyma powiadomienie po pomyślnym utworzeniu zadania hello. Spowoduje to zainicjowanie hello kontrolera ponownego uruchomienia komputera. Można monitorować proces ponownego uruchamiania hello uzyskując dostęp do **usługi > pulpit nawigacyjny > Sprawdź dzienniki operacji** , a następnie filtrowania przez usługę tooyour określonych parametrów. |
| 2. |Uruchom ponownie hello aktywnym kontrolerze. |Zobaczysz hello następujące ostrzeżenie: "po ponownym uruchomieniu kontrolera active hello hello urządzenia zostaną przełączone awaryjnie toohello pasywnym kontrolera. Czy chcesz toocontinue?" </br>Jeśli wybierzesz tooproceed tej operacji, hello następne kroki będą identyczne toothose używane toorestart hello pasywnym kontrolera (zobacz wybór 1). |
| 3. |Zamknij hello pasywnym kontroler. |Zostanie wyświetlony po wiadomość hello: "po zakończeniu zamknij należy toopush hello power znajdującego się na Twojej tooturn kontrolera go na. Czy na pewno chcesz tooshut w dół tego kontrolera?" </br>Jeśli wybierzesz tooproceed tej operacji, hello następne kroki będą identyczne toothose używane toorestart hello pasywnym kontrolera (zobacz wybór 1). |
| 4. |Zamknij hello aktywnym kontrolerze. |Zostanie wyświetlony po wiadomość hello: "po zakończeniu zamknij należy toopush hello power znajdującego się na Twojej tooturn kontrolera go na. Czy na pewno chcesz tooshut w dół tego kontrolera?" </br>Jeśli wybierzesz tooproceed tej operacji, hello następne kroki będą identyczne toothose używane toorestart hello pasywnym kontrolera (zobacz wybór 1). |

#### <a name="toorestart-or-shut-down-a-controller-in-windows-powershell-for-storsimple"></a>toorestart lub zamykania kontrolera w programie Windows PowerShell dla urządzenia StorSimple
Wykonaj następujące kroki tooshut dół hello, lub uruchom ponownie pojedynczy kontroler na urządzeniu StorSimple z hello klasycznego portalu Azure.

1. Urządzenie hello dostępu za pomocą konsoli szeregowej hello lub sesji telnet z komputera zdalnego. Połącz tooController 0 lub kontrolera 1 przez hello następujące kroki [konsolą szeregową urządzenia przy użyciu programu PuTTY tooconnect toohello](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).
2. W menu konsoli szeregowej hello, wybierz opcję 1, **Zaloguj się przy użyciu pełnego dostępu**.
3. W komunikacie transparentu hello, zanotuj kontrolera hello zostało nawiązane za (kontrolera 0 lub 1 kontrolera) i czy jest ona hello aktywnych lub pasywnych kontrolera (rezerwy) hello.
   
   * tooshut dół jednego kontrolera, w wierszu hello typu:
     
       `Stop-HcsController`
     
       Kontroler hello, które są podłączone do zostanie zamknięty. Zatrzymanie hello aktywnym kontrolerze, następnie go zostaną przełączone awaryjnie kontrolera pasywnym toohello przed jego zamknięciem.
   * toorestart kontrolera, w wierszu hello, wpisz:
     
       `Restart-HcsController`
     
       Uruchom ponownie kontroler hello, które są podłączone do. Po ponownym uruchomieniu kontrolera active hello przed ponownym uruchomieniem hello zostaną przełączone awaryjnie toohello pasywnym kontrolera.

## <a name="shut-down-a-storsimple-device"></a>Wyłącz urządzenia StorSimple
W tej sekcji opisano sposób tooshut uruchomionej lub urządzenie StorSimple nie powiodło się z komputerem zdalnym. Urządzenia jest wyłączona po zamykanie zarówno hello kontrolery urządzeń. Wyłączenie urządzenia odbywa się podczas urządzenia hello jest przenoszony fizycznie lub pochodzi z usługi.

> [!IMPORTANT]
> Przed zamknięciem hello urządzenia, Sprawdź kondycję hello hello składniki. Przejdź za**urządzenia > konserwacja > Stan sprzętu** i sprawdź, czy stan hello LED wszystkich składników hello jest zielony. Dobra urządzenie ma stan zielony. Jeśli urządzenie jest jest zamknięta tooreplace nieprawidłowo działający składnik, zostanie wyświetlony nie powiodło się (czerwony) lub obniżeniem statusu (żółty) dla hello odpowiednich składników.
> 
> 

#### <a name="tooshut-down-a-storsimple-device"></a>tooshut dół urządzenia StorSimple
1. Użyj hello [ponowne uruchamianie lub zamykanie kontrolera](#restart-or-shut-down-a-single-controller) tooidentify procedury i zamykania kontrolera pasywnym hello na urządzeniu. Można wykonać tej operacji w hello klasycznego portalu Azure lub programu Windows PowerShell dla urządzenia StorSimple.
2. Powtórz hello powyżej tooshut krok w dół hello aktywnym kontrolerze.
3. Teraz należy toolook na powitania wstecz rzutu hello urządzenia. Po dwóch kontrolerów hello są całkowicie zamknięty, hello stanu LED na obu kontrolerów hello powinny być migający red. Należy tooturn poza urządzenia hello całkowicie w tej chwili przerzucania hello power zmienia się na zasilania i chłodzenia modułów (PCMs) toohello OFF pozycji. To należy wyłączyć hello urządzenia.

<!--#### tooshut down a StorSimple device in Windows PowerShell for StorSimple

1. Connect toohello serial console of hello StorSimple device by following hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-serial-console).

1. In hello serial console menu, verify from hello banner message that hello controller you are connected toois hello passive controller. If you are connected toohello active controller, disconnect from this controller and connect toohello other controller.

1. In hello serial console menu, choose option 1, **log in with full access**.

1. At hello prompt, type:

    `Stop-HCSController`

    This should shut down hello current controller. tooverify whether hello shutdown has finished, check hello back of hello device. hello controller status LED should be solid red.

1. Repeat steps 1 through 4 tooconnect toohello active controller and then shut it down.

1. After both hello controllers are completely shut down, hello status LEDs on both should be blinking red. If you need tooturn off hello device completely at this time, flip hello power switches on both Power and Cooling Modules (PCMs) toohello OFF position.-->

## <a name="reset-hello-device-toofactory-default-settings"></a>Zresetuj ustawienia domyślne toofactory urządzenia hello
> [!IMPORTANT]
> Jeśli potrzebujesz tooreset ustawienia domyślne toofactory urządzenia, skontaktuj się z Microsoft Support. Witaj procedurze opisanej poniżej stosuje się tylko w połączeniu z Support firmy Microsoft.
> 
> 

W tej procedurze opisano sposób tooreset Microsoft Azure StorSimple urządzenia toofactory ustawienia domyślne przy użyciu programu Windows PowerShell dla urządzenia StorSimple.
Zresetowanie urządzenia usuwa wszystkie dane i ustawienia z całego klastra hello domyślnie.

Wykonaj następujące kroki tooreset hello ustawienia domyślne programu Microsoft Azure StorSimple urządzenia toofactory:

### <a name="tooreset-hello-device-toodefault-settings-in-windows-powershell-for-storsimple"></a>tooreset hello toodefault ustawienia urządzenia w programie Windows PowerShell dla urządzenia StorSimple
1. Urządzenie hello dostępu za pomocą jego konsoli szeregowej. Sprawdź tooensure komunikat transparentu hello czy połączony toohello aktywnym kontrolerze.
2. W menu konsoli szeregowej hello, wybierz opcję 1, **Zaloguj się przy użyciu pełnego dostępu**.
3. W wierszu hello wpisz hello następujące polecenia tooreset hello cały klaster, usuwając wszystkie ustawienia danych, metadane i kontrolera:
   
    `Reset-HcsFactoryDefault`
   
    tooinstead zresetować pojedynczy kontroler, użyj hello [HcsFactoryDefault resetowania](http://technet.microsoft.com/library/dn688132.aspx) polecenia cmdlet z hello `-scope` parametru.)
   
    Witaj zostanie wykonany ponowny rozruch systemu wiele razy. Użytkownik zostanie powiadomiony, gdy resetowania hello zostało pomyślnie ukończone. W zależności od modelu systemu hello może upłynąć 45 do 60 minut na urządzeniu 8100 i 60 90 minut 8600 toofinish tego procesu.
   
   > [!TIP]
   > * Jeśli używasz 1.2 aktualizacji lub wcześniej używane hello `–SkipFirmwareVersionCheck` sprawdzenie wersji oprogramowania układowego hello tooskip parametru (w przeciwnym razie zostanie wyświetlony błąd niezgodności oprogramowania układowego: ze względu na niezgodność wersji oprogramowania układowego hello tooa nie może być kontynuowana Resetowanie do ustawień fabrycznych. ).
   > * procedury resetowania fabryki Hello może zakończyć się niepowodzeniem dla urządzenia StorSimple, które są uruchomione w portalu dla instytucji rządowych hello Update 1 lub 1.1 i wykonano pomyślnie kontrolera pojedyncza lub Podwójna zastępczy (z kontrolerami zastąpienia, które zostały dostarczone z przed aktualizacją 1 oprogramowanie). Dzieje się tak podczas resetowania fabryki hello czy obraz został zweryfikowany hello obecność pliku SHA1 przed aktualizacją oprogramowania 1 na kontrolerze hello, który nie istnieje. Jeśli widzisz tej fabryki resetowania błędu, skontaktuj się z Microsoft Support tooassist program hello następne kroki. Ten problem nie występuje z kontrolerami zastąpienia, które zostały wysłane z fabryki hello Update 1 lub nowszym oprogramowania.
   > 
   > 

## <a name="questions-and-answers-about-managing-device-controllers"></a>Pytania i odpowiedzi dotyczące zarządzania kontrolerami urządzenia
W tej sekcji możemy utworzono podsumowanie niektóre hello — często zadawane pytania dotyczące zarządzania kontrolery urządzeń StorSimple.

**PYTANIE** Co się stanie, jeśli oba hello kontrolerów w urządzeniu są w dobrej kondycji i został włączony i ponowne uruchamianie lub zamykanie aktywnym kontrolerze hello?

**ODPOWIEDŹ** W przypadku obu kontrolerów hello na urządzeniu dobrej kondycji i został włączony, zostanie wyświetlony monit o potwierdzenie. Można wybrać opcję:

* **Uruchom ponownie kontroler active hello** — użytkownik zostanie powiadomiony, że ponowne uruchomienie kontrolera usługi active spowoduje hello toofail urządzenia za pośrednictwem toohello pasywnym kontrolera. Kontroler Hello zostanie uruchomiony ponownie.
* **Zamknij aktywny kontroler** — użytkownik zostanie powiadomiony, że zamykanie active kontrolera spowoduje Przestój. Należy również przycisku zasilania hello toopush na tooturn urządzenia hello na powitania kontrolera.

**PYTANIE** Co się stanie, jeśli hello pasywnym kontrolera w urządzeniu jest niedostępny lub włączenia wyłączone i I ponowne uruchamianie lub zamykanie aktywnym kontrolerze hello?

**ODPOWIEDŹ** Jeśli kontroler pasywnym hello na urządzeniu jest niedostępna lub wyłączona wyłączone i użytkownik wybierze:

* **Uruchom ponownie kontroler active hello** — użytkownik zostanie powiadomiony, że kontynuowanie operacji hello spowoduje tymczasowe przerwy w świadczeniu usługi hello i zostanie wyświetlony monit o potwierdzenie.
* **Zamknij aktywny kontroler** — użytkownik zostanie powiadomiony, że kontynuowanie operacji hello spowoduje Przestój i że konieczne będzie toopush przycisku zasilania hello na jeden lub oba tooturn kontrolerów na urządzeniu hello. Pojawi się monit o potwierdzenie.

**PYTANIE** Jeśli zamknięcie lub ponowne uruchomienie kontrolera hello nie powiedzie się tooprogress?

**ODPOWIEDŹ** Ponowne uruchamianie lub zamykanie kontroler może się niepowodzeniem, jeśli:

* Trwa aktualizacja urządzenia.
* Ponowne uruchomienie kontrolera jest już w toku.
* Zamknięcie kontrolera jest już w toku.

**PYTANIE** Jak może Ci zorientować się, jeśli kontroler został uruchomiony ponownie lub zamknąć?

**ODPOWIEDŹ** Możesz sprawdzić stan kontrolera hello na stronie konserwacji hello. Wskazuje stan kontrolera Hello czy kontroler został ponownie uruchomiony lub zamknięty. Ponadto strony alerty hello będzie zawierać alert informacyjny, jeśli kontroler hello została ponownie uruchomiona lub zamknięta. operacji zamknięcia i ponownego uruchomienia kontrolera Hello są także rejestrowane w hello dzienników operacji. Aby uzyskać więcej informacji na temat dzienniki operacji Przejdź zbyt[Sprawdź dzienniki operacji hello](storsimple-service-dashboard.md#view-the-operations-logs).

**PYTANIE** Znajduje wszystkie toohello wpływ operacji We/Wy wyniku kontrolera trybu failover?

**ODPOWIEDŹ** połączenia TCP Hello między inicjatorów i aktywnym kontrolerze zostanie zresetowany w wyniku kontrolera pracy awaryjnej, ale przywróciła w sytuacji, gdy kontroler pasywnym hello zakłada operacji. Podczas trwania hello tej operacji może być wstrzymaniu operacje wejścia/wyjścia między inicjatorów urządzeniem hello tymczasowe (mniej niż 30 sekund).

**PYTANIE** Jak powrócić po został zamknięty i usunięty Mój tooservice kontrolera?

**ODPOWIEDŹ** tooreturn tooservice kontrolera, należy wstawić go do obudowy hello zgodnie z opisem w [zastąpić modułu kontroler na urządzeniu StorSimple](storsimple-controller-replacement.md).

## <a name="next-steps"></a>Następne kroki
* Jeśli wystąpią problemy z kontrolerów urządzenia StorSimple, których nie można rozpoznać przy użyciu procedury hello wymienione w tym samouczku [skontaktuj się z Microsoft Support](storsimple-contact-microsoft-support.md).
* toolearn więcej informacji na temat używania usługi Menedżer StorSimple hello Przejdź zbyt[Użyj hello tooadminister usługi Menedżer StorSimple, urządzenia StorSimple](storsimple-manager-service-administration.md).

