---
title: "Kontrolery urządzeń serii StorSimple 8000 aaaManage | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toostop, uruchom ponownie, zamknij lub zresetować kontrolerów urządzenia StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/19/2017
ms.author: alkohli
ms.openlocfilehash: 5c59582b7ccf7cfeae9e7efbd0e4df9dc1d3871c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-storsimple-device-controllers"></a>Zarządzanie kontrolerów urządzenia StorSimple

## <a name="overview"></a>Omówienie

W tym samouczku opisano hello różne operacje, które mogą być wykonywane na kontrolerach urządzenia StorSimple. kontrolery Hello w urządzeniu StorSimple są kontrolery nadmiarowy (peer) w konfiguracji aktywny / pasywny. W danym momencie tylko jeden kontroler jest aktywna i przetwarza wszystkie operacje hello dysku i sieci. Witaj inny kontroler jest w trybie pasywnym. W przypadku niepowodzenia hello aktywnym kontrolerze kontrolera pasywnym hello automatycznie staje się aktywny.

Ten samouczek zawiera kontrolery urządzeń hello toomanage instrukcje krok po kroku przy użyciu:

* **Kontrolery** bloku dla urządzenia w hello usługi Menedżer StorSimple urządzenia.
* Program Windows PowerShell dla StorSimple.

Zaleca się zarządzanie hello kontrolery urządzeń za pomocą usługi Menedżer StorSimple urządzenia hello. Jeśli akcję można wykonać tylko przy użyciu programu Windows PowerShell dla urządzenia StorSimple, samouczek hello sprawia, że je zapisać.

Po przeczytaniu tego samouczka, będą mieć możliwość:

* Ponowne uruchamianie lub zamykanie kontrolera urządzenia StorSimple
* Wyłącz urządzenia StorSimple
* Resetuj domyślne toofactory urządzenia StorSimple

## <a name="restart-or-shut-down-a-single-controller"></a>Ponowne uruchamianie lub zamykanie jednego kontrolera
Zamknięcie lub ponowne uruchomienie kontrolera nie jest wymagana w ramach normalnego działania. Operacji zamknięcia na kontrolerze jednego urządzenia są często używane tylko w przypadkach, w których wymagana jest wymiana składnik sprzętowy urządzenia nie powiodło się. Ponowne uruchomienie kontrolera może być konieczne również w sytuacji, w których wpływ na wydajność w nadmiernego wykorzystania pamięci lub nieprawidłowo kontrolera. Możesz także toorestart kontrolera po wymianie pomyślne kontrolera, jeśli chcesz, aby tooenable i zastąpione hello kontroler testów.

Ponowne uruchamianie urządzenia nie jest inicjatory destrukcyjne tooconnected, przy założeniu, że jest dostępny kontroler pasywnym hello. Jeśli pasywnym kontrolera jest niedostępny lub ją wyłączyć, ponowne uruchomienie hello active kontroler może spowodować hello przerwy w świadczeniu usługi i przestoje.

> [!IMPORTANT]
> * **Działającego kontrolera powinien nigdy nie zostać usunięty, ponieważ skutkowałoby to utratą nadmiarowości i zwiększone ryzyko przestoju.**
> * Witaj Poniższa procedura ma zastosowanie tylko toohello urządzenia fizycznego StorSimple. Aby dowiedzieć się jak toostart, zatrzymywanie i ponowne uruchomienie hello urządzenia chmury StorSimple, zobacz [pracować z urządzenia do chmury hello](storsimple-8000-cloud-appliance-u2.md##work-with-the-storsimple-cloud-appliance).

Można ponownie uruchomić lub zamknąć kontrolera jednego urządzenia za pośrednictwem hello portalu Azure usługi Menedżer StorSimple urządzenia hello lub środowiska Windows PowerShell dla urządzenia StorSimple.

toomanage kontrolerów urządzeń z hello portalu Azure, wykonaj hello następujące kroki.

#### <a name="toorestart-or-shut-down-a-controller-in-azure-portal"></a>toorestart lub zamykania kontrolera w portalu Azure
1. W usłudze Menedżer StorSimple urządzeniu Przejdź zbyt**urządzeń**. Wybierz urządzenie z listy hello urządzeń. 

    ![Wybierz urządzenie](./media/storsimple-8000-manage-device-controller/manage-controller1.png)

2. Przejdź za**Ustawienia > kontrolerów**.
   
    ![Sprawdź, czy kontrolery urządzeń StorSimple są w dobrej kondycji](./media/storsimple-8000-manage-device-controller/manage-controller2.png)
3. W hello **kontrolerów** bloku, sprawdź, czy stan hello obu kontrolerów hello na urządzeniu jest **dobra kondycja**. Wybierz kontroler, kliknij prawym przyciskiem myszy, a następnie wybierz **Uruchom ponownie** lub **zamknąć**.

    ![Uruchom ponownie lub zamknąć kontrolery urządzeń StorSimple](./media/storsimple-8000-manage-device-controller/manage-controller3.png)

4. Zadanie jest tworzony toorestart lub zamknij hello kontroler i prezentowany dotyczy ostrzeżenia, jeśli istnieją. toomonitor hello w ponownego uruchomienia lub zamknięcia, przejdź zbyt**usługi > Dzienniki aktywności** , a następnie przeprowadź filtrowanie przez usługę tooyour określonych parametrów. Jeśli kontroler został zamknięty, a następnie konieczne będzie toopush hello zasilania przycisk tooturn na powitania kontrolera tooturn go.

#### <a name="toorestart-or-shut-down-a-controller-in-windows-powershell-for-storsimple"></a>toorestart lub zamykania kontrolera w programie Windows PowerShell dla urządzenia StorSimple
Wykonaj następujące kroki tooshut dół hello, lub uruchom ponownie pojedynczy kontroler na urządzeniu StorSimple z hello środowiska Windows PowerShell dla urządzenia StorSimple.

1. Urządzenie hello dostępu za pośrednictwem konsoli szeregowej hello lub sesji telnet z komputera zdalnego. tooconnect tooController 0 lub 1 kontrolera, wykonaj kroki hello w [konsolą szeregową urządzenia przy użyciu programu PuTTY tooconnect toohello](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).
2. W menu konsoli szeregowej hello, wybierz opcję 1, **Zaloguj się przy użyciu pełnego dostępu**.
3. W komunikacie transparentu hello, zanotuj kontrolera hello zostało nawiązane za (kontrolera 0 lub 1 kontrolera) i czy jest ona hello aktywnych lub pasywnych kontrolera (rezerwy) hello.
   
   * tooshut dół jednego kontrolera, w wierszu hello typu:
     
       `Stop-HcsController`
     
       Zamyka hello kontrolera, które są podłączone do. Zatrzymanie hello aktywnym kontrolerze urządzenia hello nie powiedzie się za pośrednictwem kontrolera pasywnym toohello.

   * toorestart kontrolera, w wierszu hello, wpisz:
     
       `Restart-HcsController`
     
       Spowoduje to ponowne uruchomienie kontrolera hello, które są podłączone do. Po ponownym uruchomieniu kontrolera active hello nie jest on za pośrednictwem kontrolera pasywnym toohello przed ponownym uruchomieniem hello.

## <a name="shut-down-a-storsimple-device"></a>Wyłącz urządzenia StorSimple

W tej sekcji opisano sposób tooshut uruchomionej lub urządzenie StorSimple nie powiodło się z komputerem zdalnym. Urządzenie jest wyłączone, po obu kontrolerów urządzeń hello są zamknięte. Wyłączenie urządzenia odbywa się podczas urządzenia hello jest przenoszony fizycznie lub pochodzi z usługi.

> [!IMPORTANT]
> Przed zamknięciem hello urządzenia, Sprawdź kondycję hello hello składniki. Przejdź tooyour urządzenia, a następnie kliknij przycisk **Ustawienia > kondycji sprzętu**. W hello **sprzętu i stan kondycji** bloku, sprawdź, czy stan hello LED wszystkich składników hello jest zielony. Dobra urządzenie ma stan zielony. Jeśli urządzenie jest jest zamknięta tooreplace nieprawidłowo działający składnik, zostanie wyświetlony nie powiodło się (czerwony) lub obniżeniem statusu (żółty) dla hello odpowiednich składników.


#### <a name="tooshut-down-a-storsimple-device"></a>tooshut dół urządzenia StorSimple

1. Użyj hello [ponowne uruchamianie lub zamykanie kontrolera](#restart-or-shut-down-a-single-controller) tooidentify procedury i zamykania kontrolera pasywnym hello na urządzeniu. Tę operację można wykonać w portalu Azure hello lub w programie Windows PowerShell dla urządzenia StorSimple.
2. Powtórz hello powyżej tooshut krok w dół hello aktywnym kontrolerze.
3. Należy teraz przyjrzymy się hello wstecz rzutu hello urządzenia. Po dwóch kontrolerów hello są całkowicie zamknięty, hello stanu LED na obu kontrolerów hello powinny być migający red. Należy tooturn poza urządzenia hello całkowicie w tej chwili przerzucania hello power zmienia się na zasilania i chłodzenia modułów (PCMs) toohello OFF pozycji. To należy wyłączyć hello urządzenia.

## <a name="reset-hello-device-toofactory-default-settings"></a>Zresetuj ustawienia domyślne toofactory urządzenia hello

> [!IMPORTANT]
> Jeśli potrzebujesz tooreset ustawienia domyślne toofactory urządzenia, skontaktuj się z Microsoft Support. Witaj procedurze opisanej poniżej stosuje się tylko w połączeniu z Support firmy Microsoft.

W tej procedurze opisano sposób tooreset Microsoft Azure StorSimple urządzenia toofactory ustawienia domyślne przy użyciu programu Windows PowerShell dla urządzenia StorSimple.
Zresetowanie urządzenia usuwa wszystkie dane i ustawienia z całego klastra hello domyślnie.

Wykonaj następujące kroki tooreset hello ustawienia domyślne programu Microsoft Azure StorSimple urządzenia toofactory:

### <a name="tooreset-hello-device-toodefault-settings-in-windows-powershell-for-storsimple"></a>tooreset hello toodefault ustawienia urządzenia w programie Windows PowerShell dla urządzenia StorSimple
1. Urządzenie hello dostępu za pomocą jego konsoli szeregowej. Sprawdź tooensure komunikat transparentu hello czy połączony toohello **Active** kontrolera.
2. W menu konsoli szeregowej hello, wybierz opcję 1, **Zaloguj się przy użyciu pełnego dostępu**.
3. W wierszu hello wpisz hello następujące polecenia tooreset hello cały klaster, usuwając wszystkie ustawienia danych, metadane i kontrolera:
   
    `Reset-HcsFactoryDefault`
   
    tooinstead zresetować pojedynczy kontroler, użyj hello [HcsFactoryDefault resetowania](http://technet.microsoft.com/library/dn688132.aspx) polecenia cmdlet z hello `-scope` parametru.)
   
    Witaj zostanie wykonany ponowny rozruch systemu wiele razy. Użytkownik zostanie powiadomiony, gdy resetowania hello zostało pomyślnie ukończone. W zależności od modelu systemu hello może upłynąć 45 do 60 minut na urządzeniu 8100 i 60 90 minut 8600 toofinish tego procesu.
   
## <a name="questions-and-answers-about-managing-device-controllers"></a>Pytania i odpowiedzi dotyczące zarządzania kontrolerami urządzenia
W tej sekcji możemy utworzono podsumowanie niektóre hello — często zadawane pytania dotyczące zarządzania kontrolery urządzeń StorSimple.

**PYTANIE** Co się stanie, jeśli oba hello kontrolerów w urządzeniu są w dobrej kondycji i został włączony i ponowne uruchamianie lub zamykanie aktywnym kontrolerze hello?

**ODPOWIEDŹ** W przypadku obu kontrolerów hello na urządzeniu dobrej kondycji i został włączony, zostanie wyświetlony monit o potwierdzenie. Można wybrać opcję:

* **Uruchom ponownie kontroler active hello** — zostanie wyświetlona informacja, że ponowne uruchomienie kontrolera usługi active spowodowane hello toofail urządzenia za pośrednictwem toohello pasywnym kontrolera. Uruchamia ponownie Hello kontrolera.
* **Zamknij aktywny kontroler** — zostanie wyświetlona informacja, że zamykanie active kontrolera powoduje Przestój. Należy również przycisku zasilania hello toopush na tooturn urządzenia hello na powitania kontrolera.

**PYTANIE** Co się stanie, jeśli hello pasywnym kontrolera w urządzeniu jest niedostępny lub włączenia wyłączone i I ponowne uruchamianie lub zamykanie aktywnym kontrolerze hello?

**ODPOWIEDŹ** Jeśli kontroler pasywnym hello na urządzeniu jest niedostępna lub wyłączona wyłączone i użytkownik wybierze:

* **Uruchom ponownie kontroler active hello** — otrzymasz powiadomienie, że kontynuowanie operacji hello spowoduje tymczasowe przerwy w świadczeniu usługi hello i zostanie wyświetlony monit o potwierdzenie.
* **Zamknij aktywny kontroler** — zostanie wyświetlona informacja, że kontynuowanie operacji hello powoduje Przestój. Należy również przycisku zasilania hello toopush na jeden lub oba tooturn kontrolerów hello urządzenia. Zostanie wyświetlony monit o potwierdzenie.

**PYTANIE** Jeśli zamknięcie lub ponowne uruchomienie kontrolera hello nie powiedzie się tooprogress?

**ODPOWIEDŹ** Ponowne uruchamianie lub zamykanie kontroler może się niepowodzeniem, jeśli:

* Trwa aktualizacja urządzenia.
* Ponowne uruchomienie kontrolera jest już w toku.
* Zamknięcie kontrolera jest już w toku.

**PYTANIE** Jak może Ci zorientować się, jeśli kontroler został uruchomiony ponownie lub zamknąć?

**ODPOWIEDŹ** Możesz sprawdzić stan kontrolera hello w bloku kontrolera. Stan kontrolera Hello wskaże, czy kontroler jest w hello proces ponownego uruchamiania lub zamykania. Ponadto hello **alerty** bloku zawierać alert informacyjny, jeśli kontroler hello jest ponownie uruchomiona lub zamknięta. operacji zamknięcia i ponownego uruchomienia kontrolera Hello są także rejestrowane w dziennikach acitivity hello. Aby uzyskać więcej informacji o dziennikach acitivity Przejdź zbyt[wyświetlać dzienniki aktywności hello](storsimple-8000-service-dashboard.md#view-the-activity-logs).

**PYTANIE** Znajduje wszystkie toohello wpływ operacji We/Wy wyniku kontrolera trybu failover?

**ODPOWIEDŹ** połączenia TCP Hello między inicjatorów i aktywnym kontrolerze zostanie zresetowany w wyniku kontrolera pracy awaryjnej, ale przywróciła w sytuacji, gdy kontroler pasywnym hello zakłada operacji. Podczas trwania hello tej operacji może być wstrzymaniu operacje wejścia/wyjścia między inicjatorów urządzeniem hello tymczasowe (mniej niż 30 sekund).

**PYTANIE** Jak powrócić po został zamknięty i usunięty Mój tooservice kontrolera?

**ODPOWIEDŹ** tooreturn tooservice kontrolera, należy wstawić go do obudowy hello zgodnie z opisem w [zastąpić modułu kontroler na urządzeniu StorSimple](storsimple-8000-controller-replacement.md).

## <a name="next-steps"></a>Następne kroki
* Jeśli wystąpią problemy z kontrolerów urządzenia StorSimple, których nie można rozpoznać przy użyciu procedury hello wymienione w tym samouczku [skontaktuj się z Microsoft Support](storsimple-8000-contact-microsoft-support.md).
* toolearn więcej informacji na temat używania usługi Menedżer urządzeń StorSimple hello Przejdź zbyt[Użyj hello tooadminister usługi Menedżera urządzeń StorSimple, urządzenia StorSimple](storsimple-8000-manager-service-administration.md).

