<!--author=alkohli last changed: 9/17/15-->

#### <a name="toocomplete-hello-minimum-storsimple-device-setup"></a>toocomplete hello minimalnej konfiguracji urządzenia StorSimple
1. Wybierz urządzenie hello, a następnie kliknij przycisk **Szybki Start**. Kliknij przycisk **przeprowadzić konfigurację urządzenia** kreatora toostart hello konfiguracji urządzenia.
2. W Kreatorze urządzenia Konfiguruj hello **podstawowe ustawienia** okna dialogowego pozycję hello następujące:
   
   1. Określ **przyjazną nazwę** dla urządzenia. Witaj domyślna nazwa urządzenia odzwierciedla takie informacje jak model urządzenia hello i numer seryjny. Przyjazna nazwa zapasowej toomanage znaków too64 można przypisać urządzenia.
   2. Zestaw hello **strefy czasowej** oparte na powitania lokalizacji geograficznej, w których hello jest wdrażane urządzenie. Wszystkie zaplanowane operacje urządzenia będą wykonywane w ramach tej strefy czasowej.
   3. W obszarze **Ustawienia DNS** podaj adres w polu **Pomocniczy serwer DNS**. Jeśli korzystasz z protokołu IPv6, hello pole zostanie wypełnione na podstawie prefiksu IPv6 hello w hello interfejsu programu Windows PowerShell. 
      Jeśli nie skonfigurowano hello pomocniczy serwer DNS, nie będzie dozwolone toosave konfiguracji urządzenia.
   4. W obszarze interfejsów z włączoną obsługą interfejsu iSCSI włącz co najmniej jedną sieć dla interfejsu iSCSI. Co najmniej jeden interfejs sieciowy musi toobe włączoną obsługę chmury i jeden interfejs mieć toobe włączono interfejs iSCSI. Interfejs DATA 0 ma automatycznie włączoną obsługę chmury.
      
      ![Podstawowe ustawienia minimalnej konfiguracji urządzenia StorSimple](./media/storsimple-complete-minimum-device-setup-u1/HCS_MinDeviceSetupBasicSettings1-include.png)
3. Kliknij ikonę strzałki hello. ![Ikona strzałki StorSimple](./media/storsimple-complete-minimum-device-setup/HCS_ArrowIcon-include.png)
4. W hello **interfejsów sieciowych** okna dialogowego podaj hello stałe adresy IP dla kontrolera 0 i kontrolera 1. **stałe adresy IP kontrolera Hello wymagane toobe wolne adresów IP w podsieci hello dostępny adres IP urządzenia hello.** Jeśli hello dane 0 interfejs został skonfigurowany dla protokołu IPv4, hello stałe toobe potrzeby adresy IP dostępne w hello formacie IPv4. Jeśli podano prefiks podczas konfiguracji protokołu IPv6, hello stałe adresy IP zostaną wypełnione automatycznie w tych polach.

    ![Interfejsy sieciowe minimalnej konfiguracji urządzenia StorSimple](./media/storsimple-complete-minimum-device-setup-u1/HCS_MinDeviceSetupNetworkInterfaces2-include.png)

    Witaj, stałe adresy IP dla kontrolera hello są używane do obsługi urządzeń toohello aktualizacje hello i dlatego hello stałe adresy IP muszą być rutowalne i umożliwiać tooconnect toohello Internet. Możesz sprawdzić, czy stałe adresy IP kontrolera są rutowalne przy użyciu hello [Test-HcsmConnection] [ Test] polecenia cmdlet. Poniższy przykład przedstawia stałe adresy IP kontrolera są routingiem toohello Internet i mogą uzyskiwać dostęp do Hello hello serwerów Microsoft Update. 

     ![Polecenie Test-HcsmConnection pokazujące rutowalne adresy IP](./media/storsimple-complete-minimum-device-setup-u1/Test-HcsmConnectionOutputRegisteredDevice.png)

1. Kliknij ikonę znacznika wyboru hello ![Ikona znacznika wyboru StorSimple](./media/storsimple-complete-minimum-device-setup/HCS_CheckIcon-include.png).
   Nastąpi powrót urządzenia toohello **Szybki Start** strony.
   
   > [!NOTE]
   > Można zmodyfikować hello wszystkich innych ustawień urządzenia w dowolnym momencie po zalogowaniu się do hello **Konfiguruj** strony.
   > 
   > 

<!--Link reference-->
[Test]: https://technet.microsoft.com/library/dn715782(v=wps.630).aspx