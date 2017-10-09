<!--author=SharS last changed: 9/17/15-->

#### <a name="tooinstall-maintenance-mode-hotfixes-via-windows-powershell-for-storsimple"></a>tooinstall poprawki trybu konserwacji programu Windows PowerShell dla urządzenia StorSimple
> [!IMPORTANT]
> W trybie konserwacji najpierw należy tooapply hello poprawki na jeden kontroler i na tekst hello inny kontroler.
> 
> 

1. Umieść hello urządzenia w trybie konserwacji. Zobacz [krok 2: tryb konserwacji wprowadź](../articles/storsimple/storsimple-update-device.md#step2) instrukcje na temat tooenter tryb konserwacji.
2. tooapply hello poprawek, wpisz:
   
     `Start-HcsHotfix` 
3. Po wyświetleniu monitu podaj hello ścieżki toohello udostępniony folder sieciowy zawierający pliki poprawek hello.
4. Pojawi się monit o potwierdzenie. Typ **Y** tooproceed hello instalacji poprawki.
5. Po zastosowano poprawki hello na jeden kontroler, logowanie toohello inny kontroler. Zastosuj poprawkę hello, jak hello poprzedniego kontrolera.
6. Po zastosowaniu poprawki hello, wyjść z trybu konserwacji. Zobacz [krok 4: tryb konserwacji zakończenia](../articles/storsimple/storsimple-update-device.md#step4) instrukcje.

