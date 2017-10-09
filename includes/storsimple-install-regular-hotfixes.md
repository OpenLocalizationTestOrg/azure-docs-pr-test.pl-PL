<!--author=SharS last changed: 9/17/15-->

#### <a name="tooinstall-regular-hotfixes-via-windows-powershell-for-storsimple"></a>tooinstall regularne poprawek za pomocą środowiska Windows PowerShell dla urządzenia StorSimple
1. Łączenie z konsolą szeregową urządzenia toohello. Aby uzyskać więcej informacji, zobacz [krok 1: połączenie konsoli szeregowej toohello](../articles/storsimple/storsimple-update-device.md#step1).
2. W menu konsoli szeregowej hello, wybierz opcję 1, **Zaloguj się przy użyciu pełnego dostępu**. Wpisz hasło hello. Witaj domyślne hasło jest **Password1**.
3. Witaj wiersza polecenia wpisz:
   
    ```
    Start-HcsHotfix
    ```
   
    > [!IMPORTANT]
    >
    > Polecenie to ma zastosowanie tylko tooregular poprawki. Uruchom to polecenie na tylko jeden kontroler, ale zostaną zaktualizowane obu kontrolerów.
    > Tryb failover kontrolera mogą pojawić się podczas procesu aktualizacji hello; jednak hello trybu failover nie wpłynie na dostępność systemu lub operacji.

4. Po wyświetleniu monitu podaj hello ścieżki toohello udostępniony folder sieciowy zawierający pliki poprawek hello.
5. Pojawi się monit o potwierdzenie. Typ **Y** tooproceed hello instalacji poprawki.

