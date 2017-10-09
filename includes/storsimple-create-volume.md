<!--author=SharS last changed: 02/04/2016-->

#### <a name="toocreate-a-volume"></a>toocreate woluminu
1. Na urządzeniu hello **Szybki Start** kliknij przycisk **Dodaj wolumin**. Spowoduje to uruchomienie powitania w Kreatorze dodawania woluminu.
2. W hello Dodaj kreatora woluminów, w obszarze **podstawowe ustawienia**, hello następujące:
   
   1. Wypełnij pole **Nazwa** dla woluminu.
   2. Określ hello **alokowana pojemność** dla woluminu w GB lub TB. Witaj, pojemność woluminu musi wynosić od 1 GB do 64 TB dla urządzenia fizycznego.
   3. Na liście rozwijanej hello, wybierz hello **typ użycia** dla woluminu. 
   4. Jeśli używasz tego woluminu na potrzeby danych archiwalnych, wybierz hello **Użyj tego woluminu w przypadku rzadziej używanych danych archiwalnych** pole wyboru. W pozostałych przypadkach zaznacz opcję **Wolumin warstwowy**. (Woluminy warstwowe były dawniej nazywane woluminami głównymi).
      
        ![Dodawanie woluminu](./media/storsimple-create-volume/ScreenshotUpdate1VolumeFlow.png)
      
      1. Kliknij ikonę strzałki hello ![ikona strzałki](./media/storsimple-create-volume/HCS_ArrowIcon-include.png) toogo toohello następnej strony.
3. W hello **dodatkowe ustawienia** okna dialogowego, Dodaj nowy rekord kontroli dostępu (ACR):
   
   1. Wypełnij pole **Nazwa** dla rekordu ACR.
   2. W obszarze **Nazwa inicjatora iSCSI**, podaj hello iSCSI kwalifikowana nazwa (IQN) hosta z systemem Windows. Jeśli nie masz hello IQN, przejdź zbyt[hello Get IQN hosta z systemem Windows Server](#get-the-iqn-of-a-windows-server-host).
   3. Zaleca się włączenie domyślnego tworzenia kopii zapasowej przez zaznaczenie hello **włączyć domyślnego tworzenia kopii zapasowej dla tego woluminu** pole wyboru. Witaj domyślnego tworzenia kopii zapasowej spowoduje utworzenie zasad, która jest wykonywana co 22:30 każdego dnia (czas urządzenia) i tworzy migawkę chmury dla tego woluminu.
      
      > [!NOTE]
      > Po hello kopii zapasowej jest włączona w tym miejscu, nie można przywrócić. Konieczne będzie tooedit hello woluminu toomodify to ustawienie.
      > 
      > 
      
        ![Dodawanie woluminu](./media/storsimple-create-volume/AddVolume2-include.png)
4. Kliknij ikonę znacznika wyboru hello ![ikona znacznika wyboru](./media/storsimple-create-volume/HCS_CheckIcon-include.png). Wolumin zostanie utworzony z hello określone ustawienia.

![Zobacz film](./media/storsimple-create-volume/Video_icon.png) **Zobacz film**

toowatch film wideo przedstawiający sposób toocreate woluminu StorSimple, kliknij przycisk [tutaj](https://azure.microsoft.com/documentation/videos/create-a-storsimple-volume/).

