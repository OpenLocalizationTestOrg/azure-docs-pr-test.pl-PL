<!--author=SharS last changed: 12/01/15-->

### <a name="step-1-authorize-a-device-toochange-hello-service-data-encryption-key-in-hello-azure-classic-portal"></a>Krok 1: Zezwolić urządzeniu toochange hello klucza szyfrowania danych usługi w hello klasycznego portalu Azure
Zazwyczaj administratora urządzenia hello żądania, czy administrator usługi hello autoryzować klucze szyfrowania danych usługi urządzenia toochange. administrator usługi Hello następnie autoryzacji hello urządzenia toochange hello klucza.

Wykonanie tego kroku w hello klasycznego portalu Azure. administrator usługi Hello można wybierz urządzenie z wyświetloną listę hello znajdujących się kwalifikujące się toobe autoryzacji. urządzenia Hello jest to klucz szyfrowania danych usługi hello toostart autoryzowanych zmienić procesu.

#### <a name="which-devices-can-be-authorized-toochange-service-data-encryption-keys"></a>Urządzenia, które mogą być autoryzowane klucze szyfrowania danych usługi toochange?
Urządzenie musi spełniać następujące kryteria, aby można było zmiany klucza szyfrowania danych usługi autoryzowanych tooinitiate hello:

* Witaj, urządzenie musi być online toobe kwalifikuje się do autoryzacji zmiany klucza szyfrowania danych usługi.
* Można autoryzować powitalne tym samym urządzeniu ponownie po 30 minutach zmiany hello klucz nie został zainicjowany.
* Inne urządzenie, można zezwolić pod warunkiem, że zmiany klucza hello nie została zainicjowana przez urządzenie wcześniej upoważnionego hello. Po autoryzacji hello nowe urządzenie hello starym urządzeniem nie można zainicjować hello zmiany.
* Nie można autoryzować urządzenia, gdy hello przerzucania klucza szyfrowania danych usługi hello jest w toku.
* W przypadku niektórych urządzeń hello zarejestrowany w usludze hello ma przerzuceniem hello szyfrowania, podczas gdy inne nie zawierają można autoryzować urządzenia. W takich przypadkach hello kwalifikujących się urządzeń są hello te, które zostały wykonane zmiany klucza szyfrowania danych usługi hello.

> [!NOTE]
> W hello klasycznego portalu Azure StorSimple urządzenia wirtualne nie są wyświetlane na liście hello urządzeń, które mogą być autoryzowany zmiany klucza hello toostart.
> 
> 

Wykonaj następujące kroki tooselect hello i autoryzować tooinitiate hello usługi danych szyfrowania klucza zmiana urządzenia.

#### <a name="tooauthorize-a-device-toochange-hello-key"></a>tooauthorize klucz hello toochange urządzenia
1. Na stronie pulpitu nawigacyjnego usługi powitania kliknij **klucza szyfrowania danych usługi zmiany**.
   
    ![Klucz szyfrowania usługi zmiany](./media/storsimple-change-data-encryption-key/HCS_ChangeServiceDataEncryptionKey-include.png)
2. W hello **klucza szyfrowania danych usługi zmiany** oknie dialogowym Wybierz i autoryzować tooinitiate hello usługi danych szyfrowania klucza zmiana urządzenia. listy rozwijanej Hello ma wszystkie urządzenia kwalifikujących się hello, które mogą być autoryzowane.
3. Kliknij ikonę znacznika wyboru hello ![ikona znacznika wyboru](./media/storsimple-change-data-encryption-key/HCS_CheckIcon-include.png).

### <a name="step-2-use-windows-powershell-for-storsimple-tooinitiate-hello-service-data-encryption-key-change"></a>Krok 2: Użyj środowiska Windows PowerShell dla StorSimple tooinitiate hello danych szyfrowania klucza zmiany usługi
Wykonanie tego kroku w hello środowiska Windows PowerShell dla StorSimple interfejsu na powitania autoryzacji urządzenia StorSimple.

> [!NOTE]
> Żadne operacje nie można wykonać w hello klasycznego portalu Azure usługi Menedżer StorSimple do czasu ukończenia hello przerzucania klucza.
> 
> 

Jeśli używasz interfejsu programu Windows PowerShell toohello tooconnect w konsoli szeregowej urządzenia hello wykonać hello następujące kroki.

#### <a name="tooinitiate-hello-service-data-encryption-key-change"></a>zmiana klucza szyfrowania danych usługi hello tooinitiate
1. Wybierz opcję 1 toolog na z pełnym dostępem.
2. Witaj wiersza polecenia wpisz:
   
     `Invoke-HcsmServiceDataEncryptionKeyChange`
3. Po pomyślnym ukończeniu hello polecenia cmdlet otrzymasz nowy klucz szyfrowania danych usługi. Skopiuj i Zapisz ten klucz do użycia w kroku 3 tego procesu. Ten klucz będzie używany tooupdate hello wszystkich pozostałych urządzeń zarejestrowanych w usłudze Menedżer StorSimple hello.
   
   > [!NOTE]
   > Ten proces musi zostać zainicjowany w ciągu czterech godzin autoryzowania urządzenia StorSimple.
   > 
   > 
   
   Ten nowy klucz jest następnie wysyłana toohello usługi toobe wypychana tooall hello urządzeń, które są zarejestrowane w usłudze hello. Na pulpicie nawigacyjnym usługi hello pojawi się alert. Usługa Hello spowoduje wyłączenie wszystkich operacji hello na urządzeniach zarejestrowanych hello i hello administratora urządzenia będą musieli tooupdate klucza szyfrowania danych usługi hello na powitania innych urządzeń. Jednak hello operacji We/Wy (wysyłanie danych w chmurze toohello hostów) zostanie nie jest zakłócona.
   
   Jeśli masz jednego urządzenia zarejestrowane usługi tooyour, hello przerzucania proces został już ukończony i można przejść hello następnego kroku. Jeśli masz wiele usługi tooyour zarejestrowanych urządzeń, przejdź toostep 3.

### <a name="step-3-update-hello-service-data-encryption-key-on-other-storsimple-devices"></a>Krok 3: Zaktualizuj klucz szyfrowania danych usługi hello na innych urządzeń StorSimple
Te czynności należy wykonać w interfejsie programu Windows PowerShell hello urządzenia StorSimple, jeśli masz wiele usługi Menedżer StorSimple tooyour zarejestrowanych urządzeń. Witaj klucza, który został uzyskany w kroku 2: Użyj środowiska Windows PowerShell dla StorSimple tooinitiate hello usługi szyfrowania klucza zmian danych musi być używane tooupdate hello wszystkie pozostałe urządzenia StorSimple w zarejestrowany hello usługi Menedżer StorSimple.

Wykonaj powitania po szyfrowania danych usługi hello tooupdate kroki na urządzeniu.

#### <a name="tooupdate-hello-service-data-encryption-key"></a>klucz szyfrowania danych usługi hello tooupdate
1. Użyj środowiska Windows PowerShell dla StorSimple tooconnect toohello konsoli. Wybierz opcję 1 toolog na z pełnym dostępem.
2. Witaj wiersza polecenia wpisz:
   
    `Invoke-HcsmServiceDataEncryptionKeyChange – ServiceDataEncryptionKey`
3. Podaj klucz szyfrowania danych usługi hello, które zostały uzyskane w [krok 2: Użyj środowiska Windows PowerShell dla StorSimple tooinitiate hello danych szyfrowania klucza zmiany usługi](#to-initiate-the-service-data-encryption-key-change).

