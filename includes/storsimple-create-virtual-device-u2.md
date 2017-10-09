#### <a name="toocreate-a-virtual-device"></a>toocreate urządzenie wirtualne
1. W hello portalu Azure, przejdź do pozycji toohello **Menedżer StorSimple** usługi.
2. Przejdź toohello **urządzeń** strony. Kliknij przycisk **Utwórz urządzenie wirtualne** u dołu hello hello **urządzeń** strony.
3. W hello **okno dialogowe Tworzenie urządzenia wirtualnego**, określ hello poniższe informacje.
   
    ![Tworzenie urządzenia wirtualnego StorSimple](./media/storsimple-create-virtual-device-u2/CreatePremiumsva1.png)
   
   1. **Nazwa** — unikatowa nazwa urządzenia wirtualnego.
   2. **Model** — wybierz model hello hello urządzenia wirtualnego. To pole jest widoczne tylko, jeśli używasz wersji Update 2 lub nowszej. Model urządzenia 8010 oferuje 30 TB pamięci standardowej, a 8020 ma 64 TB magazynu w usłudze Premium Storage. Wybierz 8010,
   3. scenariusze pobierania z poziomu elementu toodeploy z kopii zapasowych. Wybierz 8020 toodeploy wysokiej wydajności, obciążenia o małych opóźnieniach lub używane jako urządzenia dodatkowego do odzyskiwania po awarii.
   4. **Wersja** — wybierz wersję hello hello urządzenia wirtualnego. W przypadku wybrania modelu urządzenia 8020, następnie hello pole wersji nie będą widzieć toohello użytkownika. Ta opcja jest nieobecny czy wszystkie hello fizycznych urządzeń zarejestrowanych w usłudze tej usługi są uruchomione Update 1 (lub nowszej). To pole jest widoczne tylko wtedy, gdy masz kombinację przed aktualizacją 1 i Update 1 fizyczne urządzenia zarejestrowanego w aplecie hello sama usługa. Podany hello wersję urządzenia wirtualnego hello określają, które fizyczne urządzenie można pracy awaryjnej lub klonować z jest ważne, aby utworzyć odpowiednią wersję urządzenia wirtualnego hello. Wybierz pozycję:
      
      * Wersja Update 0.3, jeśli będziesz włączać tryb pracy awaryjnej lub odzyskiwanie po awarii z fizycznego urządzenia z uruchomioną wersją Update 0.3 lub starszą. 
      * Wersja Update 1, jeśli będziesz włączać tryb pracy awaryjnej lub klonować z fizycznego urządzenia z uruchomioną wersją Update 1 (lub nowszą). 
   5. **Sieć wirtualna** — Określ sieć wirtualną mają toouse z tego urządzenia wirtualnego. Jeśli używany Magazyn w warstwie Premium (Update 2 lub nowszym), należy wybrać sieć wirtualna, która jest obsługiwana z hello konta Premium Storage. Hello nieobsługiwane sieci wirtualne będą wyszarzone na liście rozwijanej hello. W przypadku wybrania nieobsługiwanej sieci wirtualnej zostanie wyświetlone ostrzeżenie. 
   6. **Konto magazynu na potrzeby tworzenia urządzenia wirtualnego** — wybierz obraz konta magazynu toohold hello hello urządzenia wirtualnego podczas inicjowania obsługi. To konto magazynu powinna być w hello tym samym regionie co urządzenie wirtualne hello i siecią wirtualną. Nie można stosować do przechowywania danych przez hello fizycznego lub hello urządzenia wirtualnego. Domyślnie do tego celu zostanie utworzone nowe konto magazynu. Jednak jeśli wiesz, że masz już konto magazynu, który nadaje się do tego celu, można ją wybierz z listy hello. W przypadku tworzenia urządzeń wirtualnych premium, hello listy rozwijanej będą wyświetlane tylko konta magazynu Premium. 
      
      > [!NOTE]
      > Witaj urządzenie wirtualne może pracować tylko z kontami magazynu Azure hello. Inne dostawcom usług w chmurze, takich jak Amazon, HP i OpenStack (obsługiwanych przez urządzenie fizyczne hello) nie są obsługiwane dla urządzenia wirtualnego StorSimple hello.
      > 
      > 
   7. Kliknij przycisk hello tooindicate znacznik wyboru, że rozumiesz, że hello danych przechowywanych na urządzeniu wirtualnym hello będzie udostępniana w centrum danych firmy Microsoft. Kiedy używasz tylko urządzenia fizycznego, klucz szyfrowania jest przechowywany z urządzeniem, więc firma Microsoft nie może go odszyfrować. 
      
       Kiedy używasz urządzenia wirtualnego, zarówno klucz szyfrowania hello, jak i klucz odszyfrowujący hello są przechowywane w Microsoft Azure. Aby uzyskać więcej informacji, zobacz temat [Zagadnienia dotyczące zabezpieczeń podczas używania urządzenia wirtualnego](../articles/storsimple/storsimple-security.md#storsimple-virtual-device-security).
   8. Kliknij przycisk hello wyboru Ikona toocreate hello wirtualne urządzenie. Witaj urządzenia może potrwać około 30 minut toobe, udostępnione.
      
      ![Etap tworzenia urządzenia wirtualnego StorSimple](./media/storsimple-create-virtual-device-u2/StorSimple_VirtualDeviceCreating1M.png)

