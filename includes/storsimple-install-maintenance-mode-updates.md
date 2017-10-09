<!--author=SharS last changed: 9/17/15-->

#### <a name="tooinstall-maintenance-mode-updates-via-windows-powershell-for-storsimple"></a>aktualizacje trybu konserwacji tooinstall za pomocą środowiska Windows PowerShell dla urządzenia StorSimple
1. Jeśli jeszcze tego nie zrobiono tego wcześniej, dostęp do konsoli szeregowej urządzenia hello i wybierz opcję 1, **Zaloguj się przy użyciu pełnego dostępu**. 
2. Wpisz hasło hello. Witaj domyślne hasło jest **Password1**.
3. Witaj wiersza polecenia wpisz:
   
     `Get-HcsUpdateAvailability` 
4. Jeśli aktualizacje są dostępne i czy są aktualizacje hello destrukcyjne lub Brak, otrzymasz powiadomienie. aktualizacje destrukcyjne tooapply, potrzebujesz tooput hello urządzenia w trybie konserwacji. Zobacz [krok 2: tryb konserwacji wprowadź](../articles/storsimple/storsimple-update-device.md#step2) instrukcje.
5. Gdy urządzenie jest w trybie konserwacji, hello wiersza polecenia, wpisz:`Start-HcsUpdate`
6. Pojawi się monit o potwierdzenie. Po potwierdzeniu hello aktualizacji będzie można zainstalować na kontrolerze hello, którego obecnie używasz. Po zainstalowaniu aktualizacji hello hello controller zostanie ponownie uruchomiony. 
7. Monitorowanie stanu hello aktualizacji. Wpisz:
   
    `Get-HcsUpdateStatus`
   
    Jeśli hello `RunInProgress` jest `True`, aktualizacja hello jest nadal w toku. Jeśli `RunInProgress` jest `False`, wskazuje hello aktualizacja została ukończona.  
8. Po zainstalowaniu aktualizacji hello na powitania bieżący kontroler i została uruchomiona ponownie, Połącz toohello inny kontroler i wykonaj kroki od 1 do 6.
9. Po aktualizacji obu kontrolerów wyjść z trybu konserwacji. Zobacz [krok 4: tryb konserwacji zakończenia](../articles/storsimple/storsimple-update-device.md#step4) instrukcje.

