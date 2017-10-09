<!--author=alkohli last changed: 01/12/17-->

#### <a name="toocomplete-hello-minimum-storsimple-device-setup"></a>toocomplete hello minimalnej konfiguracji urządzenia StorSimple

   > [!NOTE]
   > Nie można zmienić nazwy urządzenia hello, po zakończeniu hello minimalnej konfiguracji urządzenia.
   
1. Z hello Tabelaryczny spis urządzeń w hello **urządzeń** bloku, wybierz i kliknij urządzenie. urządzenie Hello jest **gotowe tooset się** stanu. Witaj **konfiguracji urządzenia** Otwiera blok.

     ![Interfejsy sieciowe minimalnej konfiguracji urządzenia StorSimple](./media/storsimple-8000-complete-minimum-device-setup-u2/step4minconfig1.png)

2. W hello **konfiguracji urządzenia** bloku:
   
   1. Określ **przyjazną nazwę** dla urządzenia. Witaj domyślna nazwa urządzenia odzwierciedla takie informacje jak model urządzenia hello i numer seryjny. Przyjazna nazwa zapasowej toomanage znaków too64 można przypisać urządzenia.
   2. Zestaw hello **strefy czasowej** oparte na powitania lokalizacji geograficznej, w których hello jest wdrażane urządzenie. Wszystkie zaplanowane operacje urządzenia są wykonywane w ramach tej strefy czasowej.
   3. W obszarze hello **dane 0 ustawienia**:

       1. DANE 0, który interfejs sieciowy pokazuje, jak włączyć hello sieci (IP, podsieci, bramy) skonfigurowanych ustawień za pomocą Kreatora instalacji hello. Interfejs DATA 0 jest także automatycznie włączony dla chmury i interfejsu iSCSI.

       2. Podaj informacje o hello stałe adresy IP dla kontrolera 0 i kontrolera 1. **stałe adresy IP kontrolera Hello wymagane toobe wolne adresów IP w podsieci hello dostępny adres IP urządzenia hello.** Jeśli hello dane 0 interfejs został skonfigurowany dla protokołu IPv4, hello stałe toobe potrzeby adresy IP dostępne w hello formacie IPv4. Jeśli podano prefiks podczas konfiguracji protokołu IPv6, stałe adresy IP hello są wypełniane automatycznie w tych polach.

            ![Interfejsy sieciowe minimalnej konfiguracji urządzenia StorSimple](./media/storsimple-8000-complete-minimum-device-setup-u2/step4minconfig2.png)

            Witaj, stałe adresy IP dla kontrolera hello są używane do obsługi hello aktualizacje toohello urządzenia. W związku z tym hello stałe adresy IP muszą być rutowalne i umożliwiać tooconnect toohello Internet. Możesz sprawdzić, czy stałe adresy IP kontrolera są rutowalne przy użyciu hello [Test-HcsmConnection] [ Test] polecenia cmdlet. Poniższy przykład przedstawia stałe adresy IP kontrolera są routingiem toohello Internet i mogą uzyskiwać dostęp do Hello hello serwerów Microsoft Update.

            ![Polecenie Test-HcsmConnection pokazujące rutowalne adresy IP](./media/storsimple-8000-complete-minimum-device-setup-u2/step4minconfig3.png)

1. Kliknij przycisk **OK**. Uruchamia Hello konfiguracji urządzenia. Po zakończeniu konfiguracji urządzenia hello są powiadamiani o. Witaj zmiany stanu urządzenia zbyt**Online** w hello **urządzeń** bloku.

    ![Interfejsy sieciowe minimalnej konfiguracji urządzenia StorSimple](./media/storsimple-8000-complete-minimum-device-setup-u2/step4minconfig4.png)

<!--Link reference-->
[Test]: https://technet.microsoft.com/library/dn715782(v=wps.630).aspx
