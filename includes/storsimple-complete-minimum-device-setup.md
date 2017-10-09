<!--author=alkohli last changed: 9/17/15-->

#### <a name="toocomplete-hello-minimum-storsimple-device-setup"></a>toocomplete hello minimalnej konfiguracji urządzenia StorSimple
1. W hello **urządzeń** hello wybierz urządzenie, kliknij strzałkę hello względem strony określonego urządzenia toohello toogo hello urządzenia nazwa. 
   
    ![Strona Urządzenia z urządzeniem w trybie online](./media/storsimple-complete-minimum-device-setup/HCS_DevicesPageM-include.png) 
2. Kliknij ikonę szybkiego startu ![ikona Szybki Start](./media/storsimple-complete-minimum-device-setup/HCS_QuickStartIcon-include.png) tooaccess hello strony szybki start urządzenia. Kliknij przycisk **przeprowadzić konfigurację urządzenia** toostart hello **konfiguracji urządzenia** kreatora.
   
    ![Strona Szybki start urządzenia](./media/storsimple-complete-minimum-device-setup/Device_Quick_Start_page_1M.png)
3. Na powitania **podstawowe ustawienia** pozycję hello następujące:
   
   1. Określ **przyjazną nazwę** dla urządzenia. Witaj domyślna nazwa urządzenia odzwierciedla takie informacje jak model urządzenia hello i numer seryjny. Przyjazna nazwa zapasowej toomanage znaków too64 można przypisać urządzenia.
   2. Zestaw hello **strefy czasowej** oparte na powitania lokalizacji geograficznej, w których hello jest wdrażane urządzenie. Wszystkie zaplanowane operacje urządzenia będą wykonywane w ramach tej strefy czasowej.
   3. W obszarze **Ustawienia DNS** podaj adres w polu **Pomocniczy serwer DNS**. Jeśli korzystasz z protokołu IPv6, hello pole zostanie wypełnione na podstawie prefiksu IPv6 hello w hello interfejsu programu Windows PowerShell. 
      Jeśli nie skonfigurowano hello pomocniczy serwer DNS, nie będzie dozwolone toosave konfiguracji urządzenia.
   4. W obszarze interfejsów z włączoną obsługą interfejsu iSCSI włącz co najmniej jedną sieć dla interfejsu iSCSI. Co najmniej jeden interfejs sieciowy musi toobe włączoną obsługę chmury i jeden interfejs mieć toobe włączono interfejs iSCSI. Interfejs DATA 0 ma automatycznie włączoną obsługę chmury.
      
      ![Podstawowe ustawienia minimalnej konfiguracji urządzenia StorSimple](./media/storsimple-complete-minimum-device-setup/HCS_MinDeviceSetupBasicSettings1-include.png)
4. Kliknij ikonę strzałki hello. ![Ikona strzałki StorSimple](./media/storsimple-complete-minimum-device-setup/HCS_ArrowIcon-include.png)
5. Na powitania **interfejsów sieciowych** Podaj hello stałe adresy IP dla kontrolera 0 i kontrolera 1. Jeśli hello dane 0 interfejs został skonfigurowany dla protokołu IPv4, hello stałe toobe potrzeby adresy IP dostępne w hello formacie IPv4. Jeśli podano prefiks podczas konfiguracji protokołu IPv6, hello stałe adresy IP zostaną wypełnione automatycznie w tych polach.

    > [!NOTE] 
    > - stałe adresy IP kontrolera Hello wymagane toobe wolne adresów IP w podsieci hello dostępny adres IP urządzenia hello.
    > - Witaj, stałe adresy IP dla kontrolera hello są używane do obsługi urządzeń toohello aktualizacje hello i dlatego hello stałe adresy IP muszą być rutowalne i umożliwiać tooconnect toohello Internet.

    ![Interfejsy sieciowe minimalnej konfiguracji urządzenia StorSimple](./media/storsimple-complete-minimum-device-setup/HCS_MinDeviceSetupNetworkInterfaces2-include.png)

1. Kliknij ikonę znacznika wyboru hello ![Ikona znacznika wyboru StorSimple](./media/storsimple-complete-minimum-device-setup/HCS_CheckIcon-include.png).
   Nastąpi powrót urządzenia toohello **Szybki Start** strony.
   
   > [!NOTE]
   > Można zmodyfikować hello wszystkich innych ustawień urządzenia w dowolnym momencie po zalogowaniu się do hello **Konfiguruj** strony.
   > 
   > 

![Zobacz film](./media/storsimple-complete-minimum-device-setup/Video_icon.png) **Zobacz film**

toowatch film wideo przedstawiający sposób toocomplete hello minimalnej konfiguracji urządzenia, kliknij przycisk [tutaj](https://azure.microsoft.com/documentation/videos/minimum-storsimple-device-setup/).

