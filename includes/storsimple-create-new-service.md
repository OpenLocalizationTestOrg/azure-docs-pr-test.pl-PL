<!--author=alkohli last changed:01/14/2016-->


#### <a name="toocreate-a-new-service"></a>toocreate nowej usługi
1. Przy użyciu poświadczeń konta Microsoft, zaloguj się na toohello klasycznego portalu Azure pod tym adresem URL: [https://manage.windowsazure.com/](https://manage.windowsazure.com/).
2. W hello klasycznego portalu Azure, kliknij przycisk **nowy** > **usług danych** > **Menedżer StorSimple** > **szybki Utwórz**.
3. W formularzu hello wyświetlany hello następujące:
   
   1. Podaj unikatową nazwę usługi w polu **Nazwa**. Jest to przyjazna nazwa, która może być używana usługa hello tooidentify. Witaj nazwa może zawierać od 2 do 50 znaków, które mogą być litery, cyfry i łączniki. Witaj nazwa musi zaczynać i kończyć literą lub cyfrą.
   2. Wypełnij pole **Lokalizacja** dla usługi. Ogólnie rzecz biorąc wybierz lokalizację najbliżej toohello region geograficzny, w którym ma toodeploy urządzenia. Można również toofactor w hello następujące czynności: 
      
      * Jeśli masz istniejące obciążenia na platformie Azure, również będą toodeploy na urządzeniu StorSimple, należy użyć tego centrum danych.
      * Usługi StorSimple Manager i Azure Storage mogą być w dwóch różnych lokalizacjach. W takim przypadku należy są wymagane toocreate hello Menedżer StorSimple i konto magazynu Azure oddzielnie. toocreate konta magazynu platformy Azure, przejdź do usługi Magazyn Azure toohello w hello klasycznego portalu Azure i wykonaj kroki hello w [Tworzenie konta usługi Azure Storage](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account). Po utworzeniu tego konta, dodaj go toohello usługi Menedżer StorSimple, wykonując kroki hello [Konfigurowanie nowego konta magazynu dla usługi hello](../articles/storsimple/storsimple-deployment-walkthrough.md#configure-a-new-storage-account-for-the-service).
   3. Wybierz **subskrypcji** z listy rozwijanej hello. Subskrypcja Hello jest tooyour połączony z kontem rozliczeniowym. To pole nie jest widoczne, jeśli istnieje tylko jedna subskrypcja.
   4. Wybierz **Utwórz nowe konto magazynu** tooautomatically Utwórz konto magazynu z usługą hello. To konto magazynu będzie miało specjalną nazwę, np. „storsimplebwv8c6dcnf”. Jeśli potrzebujesz danych w innej lokalizacji, usuń zaznaczenie tego pola. 
   5. Kliknij przycisk **Utwórz usługę Menedżer StorSimple** toocreate hello usługi.
   
   ![Utwórz usługę StorSimple Manager](./media/storsimple-create-new-service/HCS_CreateAService-include.png)
   
   Będzie ukierunkowanej toohello **usługi** strony docelowej. Tworzenie usługi Hello może potrwać kilka minut. Po pomyślnym utworzeniu usługi hello, będzie można odpowiednio powiadomiony i hello stanu usługi hello zmieni się zbyt**Active**.
   
   ![Tworzenie usług](./media/storsimple-create-new-service/HCS_StorSimpleManagerServicePage-include.png)

![Zobacz film](./media/storsimple-create-new-service/Video_icon.png) **Zobacz film**

toowatch film wideo przedstawiający sposób toocreate nową usługę Menedżer StorSimple, kliknij przycisk [tutaj](https://azure.microsoft.com/documentation/videos/create-a-storsimple-manager-service/).

