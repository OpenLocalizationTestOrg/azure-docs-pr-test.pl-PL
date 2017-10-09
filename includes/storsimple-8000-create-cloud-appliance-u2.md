#### <a name="toocreate-a-cloud-appliance"></a>toocreate urządzenia chmury

1. W hello portalu Azure, przejdź do pozycji toohello **Menedżera urządzeń StorSimple** usługi.
2. Przejdź toohello **urządzeń** bloku. Hello paska poleceń w bloku podsumowania hello usługi, kliknij **urządzenia chmury Utwórz**.
    ![Tworzenie urządzenia StorSimple w chmurze](./media/storsimple-8000-create-cloud-appliance-u2/sca-create1.png)
3. W hello **urządzenia chmury Utwórz** bloku, określ hello poniższe informacje.
   
    ![Tworzenie urządzenia StorSimple w chmurze](./media/storsimple-8000-create-cloud-appliance-u2/sca-create2m.png)
   
   1. **Nazwa** — unikatowa nazwa urządzenia w chmurze.
   2. **Model** — wybierz model urządzenia chmury hello hello. Urządzenie 8010 oferuje 30 TB magazynu Standard Storage, a 8020 ma 64 TB magazynu w usłudze Premium Storage. Określ 8010 scenariusze pobierania z poziomu elementu toodeploy z kopii zapasowych. Wybierz 8020 toodeploy wysoka wydajność, małe opóźnienia obciążeń, lub użyj jako urządzenia dodatkowego do odzyskiwania po awarii.
   3. **Wersja** — wybierz wersję hello hello urządzenia chmury. Wersja Hello odpowiada toohello wersja obrazu wirtualnego dysku twardego hello będący urządzenia chmury hello toocreate używane. Podana wersja hello chmury hello urządzenia określa fizyczne urządzenia pracy awaryjnej lub klonować z, ważne jest, że utworzyć odpowiednią wersję urządzenia chmury hello.
   4. **Sieć wirtualna** — Określ sieć wirtualną mają toouse z tego urządzenia do chmury. Jeśli używany Magazyn w warstwie Premium, należy wybrać sieć wirtualna, która jest obsługiwana z hello konta Premium Storage. Witaj nieobsługiwane sieci wirtualne są wygaszone liście rozwijanej hello. W przypadku wybrania nieobsługiwanej sieci wirtualnej jest wyświetlane ostrzeżenie.
   5. **Podsieci** — oparte na sieci wirtualnej hello zaznaczone, lista rozwijana hello Wyświetla hello skojarzonych podsieci. Przypisz urządzenia chmury tooyour podsieci.
   6. **Konto magazynu** — wybierz obraz konta magazynu toohold hello hello chmury urządzenia podczas inicjowania obsługi. To konto magazynu powinna być w hello tego samego regionu hello urządzenia chmury i sieci wirtualnej. Nie można stosować do przechowywania danych hello fizycznego lub hello urządzenia chmury. Domyślnie do tego celu jest tworzone nowe konto magazynu. Jednak jeśli wiesz, że masz już konto magazynu, który nadaje się do tego celu, można ją wybierz z listy hello. W przypadku tworzenia urządzenia chmury premium, hello listy rozwijanej są wyświetlane tylko konta Premium magazynu.
      
      > [!NOTE]
      > urządzenia chmury Hello może pracować tylko z kontami magazynu Azure hello.
    
   7. Wybierz tooindicate wyboru hello, że rozumiesz, że hello dane przechowywane na urządzeniu chmury hello jest obsługiwana w centrum danych firmy Microsoft.
       * Kiedy używasz tylko urządzenia fizycznego, klucz szyfrowania jest przechowywany z urządzeniem, więc firma Microsoft nie może go odszyfrować.

       * Kiedy używasz urządzenia chmury, zarówno klucz szyfrowania hello, jak i klucz odszyfrowujący hello są przechowywane w Microsoft Azure. Aby uzyskać więcej informacji, zapoznaj się z [zagadnieniami dotyczącymi zabezpieczeń podczas używania urządzenia w chmurze](../articles/storsimple/storsimple-security.md#storsimple-virtual-device-security).
   8. Kliknij przycisk **Utwórz** tooprovision hello chmury urządzenia. Witaj urządzenia może potrwać około 30 minut toobe, udostępnione. Użytkownik jest powiadamiany o pomyślnym utworzeniu hello urządzenia chmury. Przejdź do bloku tooDevices i urządzenia chmury hello toodisplay odświeża hello listę urządzeń. Stan urządzenia hello Hello jest **gotowe tooset się**.
      
      ![Gotowe tooset urządzenia chmury StorSimple się](./media/storsimple-8000-create-cloud-appliance-u2/sca-create3.png)

