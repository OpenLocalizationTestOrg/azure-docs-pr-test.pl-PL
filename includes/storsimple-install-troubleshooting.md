<!--author=alkohli last changed: 03/17/16-->

## <a name="troubleshooting-update-failures"></a>Rozwiązywanie problemów dotyczących niepowodzenia aktualizacji
**Co zrobić, jeśli zostanie wyświetlone powiadomienie, że hello sprawdzania przed uaktualnieniem zakończyć się niepowodzeniem?**

Jeśli sprawdzanie wymagań wstępnych nie powiedzie się, upewnij się, że sprawdzono, pasek powiadomień szczegółowe hello u dołu strony hello hello. Zawiera wskazówki, jak toowhich Sprawdzanie wymagań wstępnych nie powiodło się. Witaj Poniższa ilustracja przedstawia wystąpienie, w której znajduje się takie powiadomienie. W takim przypadku sprawdzenie kondycji kontrolera hello i sprawdzanie kondycji składnika sprzętu nie powiodło się. W obszarze hello **stan sprzętu** sekcji widać, który zarówno **kontrolera 0** i **kontrolera 1** składniki wymagają uwagi.

  ![Niepowodzenie testu wstępnego](./media/storsimple-install-troubleshooting/HCS_PreUpdateCheckFailed-include.png)

Konieczne będzie toomake się, że zarówno kontrolery są w dobrej kondycji i w trybie online. Również należy się upewnić, że wszystkie składniki sprzętowe hello w urządzeniu StorSimple hello są pokazywane toobe dobrej kondycji na stronie konserwacji hello toomake. Następnie możesz tooinstall aktualizacji. Jeśli nie ma problemów składników sprzętowych hello stanie toofix, będzie konieczne toocontact Microsoft Support następne kroki.

**Co zrobić, jeśli wyświetlony komunikat o błędzie "Nie można zainstalować aktualizacji" i hello zalecenie jest rozwiązywanie problemów z przewodnika toodetermine hello przyczynę błędu na powitania aktualizacji toohello toorefer?**

Jeden prawdopodobną przyczyną tego problemu może być, nie masz serwerów Microsoft Update toohello łączności. Jest to sprawdzanie ręczne, które należy wykonać toobe. W przypadku utraty połączenia toohello aktualizacji serwera, zadania aktualizacji nie powiedzie się. Możesz sprawdzić łączność hello, uruchamiając następujące polecenie cmdlet z interfejsu programu Windows PowerShell hello urządzenia StorSimple hello:

 `Test-Connection -Source <Fixed IP of your device controller> -Destination <Any IP or computer name outside of datacenter>`

Uruchom polecenie cmdlet hello na obu kontrolerów.

Jeśli po sprawdzeniu istnieje połączenie hello i kontynuować toosee ten problem, skontaktuj się z Microsoft Support, dalsze czynności.

**Co zrobić, jeśli zostanie wyświetlony błąd aktualizacji podczas aktualizowania tooUpdate Twojego urządzenia 4 i obu kontrolerów hello działają aktualizacji 4?**

W przypadku obu kontrolerów hello uruchomiona hello tej samej wersji oprogramowania, a jeśli istnieje Niepowodzenie aktualizacji, począwszy od aktualizacji 4, kontrolerów hello nie przechodzą w trybie odzyskiwania. Tej sytuacji mogą wystąpić, jeśli hello poprawek oprogramowania urządzenia (aktualizacja kolejności 1) jest kontrolerów hello tooboth zastosowane pomyślnie, ale inne poprawki (kolejność 2 i 3 kolejności) są jeszcze toobe zastosowane. Począwszy od aktualizacji 4, kontrolerów hello przejdzie do trybu odzyskiwania tylko wtedy, gdy dwa kontrolery hello są uruchomione wersje oprogramowania. 

Jeśli hello użytkownik widzi błąd aktualizacji po uruchomieniu aktualizacji 4 obu kontrolerów, zalecamy Poczekaj kilka minut i ponów próbę aktualizacji. Jeśli hello ponownych prób nie powiedzie się, a następnie należy skontaktować się z Microsoft Support.
