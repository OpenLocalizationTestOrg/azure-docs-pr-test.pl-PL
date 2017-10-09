<!--author=SharS last changed: 11/18/16-->

#### <a name="tooinstall-regular-updates-via-windows-powershell-for-storsimple"></a>tooinstall regularne aktualizacje za pomocą środowiska Windows PowerShell dla urządzenia StorSimple
1. Otwieranie konsoli szeregowej urządzenia hello i wybierz opcję 1, **Zaloguj się przy użyciu pełnego dostępu**. Wpisz hasło hello. Witaj domyślne hasło jest *Password1*. 
2. Witaj wiersza polecenia wpisz:
   
     `Get-HcsUpdateAvailability`
   
    Jeśli aktualizacje są dostępne i czy są aktualizacje hello destrukcyjne lub Brak, otrzymasz powiadomienie.
3. Witaj wiersza polecenia wpisz:
   
     `Start-HcsUpdate`
   
    rozpocznie się proces aktualizacji Hello.

> [!IMPORTANT]
> * Polecenie to ma zastosowanie tylko tooregular aktualizacje. Uruchom to polecenie na tylko jeden kontroler, ale zostaną zaktualizowane obu kontrolerów. 
> * Tryb failover kontrolera mogą pojawić się podczas procesu aktualizacji hello; jednak hello trybu failover nie wpłynie na dostępność systemu lub operacji.
> 
> 

