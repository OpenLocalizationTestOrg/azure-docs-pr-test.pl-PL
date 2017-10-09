<!--author=alkohli last changed:02/10/2017-->


#### <a name="toocreate-a-new-service"></a>toocreate nowej usługi

1. Korzystanie z toolog poświadczeń konta Microsoft na toohello [portalu Azure](https://portal.azure.com/).

2. W portalu Azure hello, kliknij przycisk  **+**  , a następnie w witrynie marketplace hello, kliknij przycisk **zobaczyć wszystkie**.

    ![Tworzenie usługi Menedżer urządzeń StorSimple](./media/storsimple-8000-create-new-service/createssdevman1.png)

    Wyszukaj pozycję _Urządzenie fizyczne StorSimple_. Wybierz i kliknij pozycję **Seria urządzeń fizycznych StorSimple**, a następnie kliknij pozycję **Utwórz**. Alternatywnie w hello portalu Azure kliknij  **+**  , a następnie w obszarze **magazynu**, kliknij przycisk **fizycznych serii urządzenia StorSimple**.

    ![Tworzenie usługi Menedżer urządzeń StorSimple](./media/storsimple-8000-create-new-service/createssdevman11.png)

3. W hello **Menedżera urządzeń StorSimple** bloku hello następujące kroki:
   
   1. Podaj **unikatową nazwę zasobu** dla swojej usługi. Ta nazwa jest przyjazną nazwę, która może być używana usługa hello tooidentify. Witaj nazwa może zawierać od 2 do 50 znaków, które mogą być litery, cyfry i łączniki. Witaj nazwa musi zaczynać i kończyć literą lub cyfrą.

   2. Wybierz **subskrypcji** z listy rozwijanej hello. Subskrypcja Hello jest tooyour połączony z kontem rozliczeniowym. To pole nie jest widoczne, jeśli istnieje tylko jedna subskrypcja.

   3. W obszarze **Grupa zasobów** wybierz opcję **użycia istniejącej** grupy lub **utworzenia nowej**. Aby uzyskać więcej informacji, zobacz [Grupy zasobów na platformie Azure](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-infrastructure-resource-groups-guidelines/).
   
   4. Wypełnij pole **Lokalizacja** dla usługi. Ogólnie rzecz biorąc wybierz lokalizację najbliżej toohello region geograficzny, w którym ma toodeploy urządzenia. Można również toofactor w hello następujące zagadnienia: 
      
      * Jeśli masz istniejące obciążenia na platformie Azure, również będą toodeploy na urządzeniu StorSimple, należy użyć tego centrum danych.
      * Usługi Menedżer urządzeń StorSimple i Azure Storage mogą działać w dwóch różnych lokalizacjach. W takim przypadku należy są wymagane toocreate hello Menedżera urządzeń StorSimple i konto magazynu Azure oddzielnie. toocreate konta magazynu platformy Azure, przejdź do usługi Magazyn Azure toohello w hello portalu Azure i wykonaj kroki hello w [Tworzenie konta usługi Azure Storage](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account). Po utworzeniu tego konta, dodaj go usługi Menedżer StorSimple urządzenia toohello wykonując kroki hello w [Konfigurowanie nowego konta magazynu dla usługi hello](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#configure-a-new-storage-account-for-the-service).

   5. Wybierz **Utwórz nowe konto magazynu** tooautomatically Utwórz konto magazynu z usługą hello. Podaj nazwę tego konta magazynu. Jeśli potrzebujesz danych w innej lokalizacji, usuń zaznaczenie tego pola.

   6. Sprawdź **toodashboard numeru Pin** Chcąc usługi toothis szybkie łącze do pulpitu nawigacyjnego.
      
   7. Kliknij przycisk **Utwórz** toocreate hello Menedżera urządzeń StorSimple.

       ![Tworzenie usługi Menedżer urządzeń StorSimple](./media/storsimple-8000-create-new-service/createssdevman2.png)
   
Tworzenie usługi Hello zajmuje kilka minut. Po pomyślnym utworzeniu usługi hello, zostanie wyświetlone powiadomienie i otwiera nowy blok usługi hello.
   
![Tworzenie usługi Menedżer urządzeń StorSimple](./media/storsimple-8000-create-new-service/createssdevman5.png)


