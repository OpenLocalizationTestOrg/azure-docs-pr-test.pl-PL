#### <a name="toocreate-a-new-service"></a>toocreate nowej usługi

1.  Przy użyciu poświadczeń konta Microsoft, zaloguj się na toohello portalu Azure pod tym adresem URL: <https://portal.azure.com/>. Jeśli wdrażane urządzenia hello w portalu dla instytucji rządowych, zaloguj się w: <https://portal.azure.us/>

2.  W portalu Azure hello, kliknij przycisk **+ nowy** &gt; **magazynu** &gt; **serii wirtualnego StorSimple**.

    ![Tworzenie nowej usługi](./media/storsimple-virtual-array-create-new-service/createnewservice2.png) 

3.  W hello **Menedżera urządzeń StorSimple** bloku, który zostanie otwarty, hello następujące:

    1.  Podaj **unikatową nazwę zasobu** dla swojej usługi. Nazwa zasobu Hello jest przyjazna nazwa, która może być używana usługa hello tooidentify. Witaj nazwa może zawierać od 2 do 50 znaków, które mogą być litery, cyfry i łączniki. Witaj nazwa musi zaczynać i kończyć literą lub cyfrą.

    2.  Wybierz **subskrypcji** z listy rozwijanej hello. Subskrypcja Hello jest tooyour połączony z kontem rozliczeniowym. To pole nie jest widoczne, jeśli istnieje tylko jedna subskrypcja.

    3.  Aby uzyskać **grupy zasobów**, wybierz istniejącą lub Utwórz nową grupę. Aby uzyskać więcej informacji, zobacz [Grupy zasobów na platformie Azure](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-infrastructure-resource-groups-guidelines/).

    4.  Wypełnij pole **Lokalizacja** dla usługi. Zobacz [regiony platformy Azure](https://azure.microsoft.com/regions/#services) Aby uzyskać więcej informacji o tym, które usługi są dostępne w danym regionie. Ogólnie rzecz biorąc, wybierz **lokalizacji** najbliżej regionu geograficznego toohello miejscu toodeploy urządzenia. Można również toofactor w hello następujące czynności:

        -   Jeśli masz istniejące obciążenia na platformie Azure, również będą toodeploy na urządzeniu StorSimple, zalecane jest użycie tego centrum danych.

        -   Magazyn Menedżera urządzeń StorSimple i Azure może być w dwóch różnych lokalizacjach. W takim przypadku należy są wymagane toocreate hello Menedżera urządzeń StorSimple i konto magazynu Azure oddzielnie. toocreate konta magazynu platformy Azure, przejdź do usługi Magazyn Azure toohello w hello portalu Azure i wykonaj kroki hello w [Tworzenie konta usługi Azure Storage](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/#create-a-storage-account). Po utworzeniu tego konta, dodaj go usługi Menedżer StorSimple urządzenia toohello wykonując kroki hello w [Konfigurowanie nowego konta magazynu dla usługi hello](https://azure.microsoft.com/en-us/documentation/articles/storsimple-deployment-walkthrough/#configure-a-new-storage-account-for-the-service).

        -   Jeśli wdrażane urządzenia wirtualnego hello w hello Portal dla instytucji rządowych, hello usługi Menedżer StorSimple urządzenia jest dostępny w lokalizacji nam Iowa i Virginia nam.

    5.  Wybierz **Utwórz nowe konto magazynu Azure** tooautomatically Utwórz konto magazynu z usługą hello. Określ **nazwy konta magazynu**. Jeśli potrzebujesz danych w innej lokalizacji, usuń zaznaczenie tego pola.

    6.  Sprawdź **toodashboard numeru Pin** Chcąc usługi toothis szybkie łącze do pulpitu nawigacyjnego.

    7.  Kliknij przycisk **Utwórz** toocreate hello Menedżera urządzeń StorSimple.

        ![Tworzenie nowej usługi](./media/storsimple-virtual-array-create-new-service/createnewservice4.png)  

Jesteś ukierunkowanej toohello **usługi** strony docelowej. Tworzenie usługi Hello zajmuje kilka minut. Po pomyślnym utworzeniu usługi hello, będzie można odpowiednio powiadomiony i hello stanu usługi hello zmieni się zbyt**Active**.


