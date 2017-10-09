<!--author=alkohli last changed: 08/16/2016-->

#### <a name="toocreate-a-volume"></a>toocreate woluminu
1. Na urządzeniu hello **Szybki Start** kliknij przycisk **Dodaj wolumin** toostart powitania w Kreatorze dodawania woluminu.
2. W hello Dodaj kreatora woluminów, w obszarze **podstawowe ustawienia**:
   
   1. Wpisz wartość pola **Nazwa** dla woluminu.
   2. Na liście rozwijanej hello, wybierz hello **typ użycia** dla woluminu. W przypadku obciążeń, które wymagają lokalnych gwarancji, małych opóźnień i większej wydajności, wybierz wolumin typu **Przypięty lokalnie**. W przypadku wszystkich innych danych wybierz wolumin typu **Warstwowy**. Jeśli używasz tego woluminu na potrzeby danych archiwalnych, wybierz opcję **Użyj tego woluminu w przypadku rzadziej używanych danych archiwalnych**. 
      
       Wolumin przypięty lokalnie jest alokowany nieelastycznie i gwarantuje, że hello główne dane na woluminie hello pozostaje toohello lokalne urządzenia i nie zostaną przeniesione toohello chmury.  Jeśli tworzysz wolumin przypięty lokalnie, urządzenia hello wyszukuje dostępne miejsce w warstwach lokalne powitania tooprovision hello ilość hello żądany rozmiar. Witaj operacji tworzenia woluminu przypiętego lokalnie może obejmować przenoszenie istniejących danych z chmury toohello urządzenia hello i czas hello toocreate hello woluminu może trwać długo. Łączny czas Hello zależy od rozmiaru hello hello elastycznie woluminu, dostępnej przepustowości sieci i danych hello na urządzeniu. 
      
       Wolumin warstwowy jest alokowany elastycznie i można go szybko utworzyć. Wybieranie **Użyj tego woluminu w przypadku rzadziej używanych danych archiwalnych** dla woluminu warstwowego celem danych archiwalnych zmiany hello rozmiaru fragmentu deduplikacji dla woluminu too512 KB. Jeśli to pole nie jest zaznaczone, odpowiedni wolumin warstwowy hello używa rozmiaru fragmentu wynoszącego 64 KB. Większy rozmiar fragmentu deduplikacji umożliwia hello urządzenia tooexpedite hello transferu dużej ilości danych archiwalnych toohello chmury.
   3. Określ hello **alokowana pojemność** dla woluminu. Zanotuj hello pojemności dostępnej w oparciu wybrany typ woluminu hello. Witaj określony rozmiar woluminu nie może przekraczać hello dostępnego miejsca.
      
       Można alokować woluminy przypięte lokalnie w górę too8.5 TB lub woluminy warstwowe się too200 TB na urządzeniu 8100 hello. Na urządzeniu 8600 większych hello można udostępnić woluminów przypiętych lokalnie too22.5 TB lub woluminy warstwowe się too500 TB. Lokalne miejsce na urządzeniu hello jest hello wymagane toohost pracy zestaw woluminów warstwowych, tworzenie woluminów przypiętych lokalnie ma wpływ na powitania miejsce dostępne do alokowania na woluminach warstwowych. Jeśli zatem tworzysz wolumin przypięty lokalnie, miejsce dostępne na potrzeby tworzenia woluminów warstwowych zmniejszy się. Podobnie jeśli został utworzony wolumin warstwowy, zostanie zmniejszona hello dostępnego miejsca na potrzeby tworzenia woluminów przypiętych lokalnie.
      
       Jeśli dostarczasz woluminu przypiętego lokalnie 8,5 TB (maksymalny dozwolony rozmiar) na urządzeniu 8100 zostały wyczerpane wszystkich hello lokalne miejsce dostępne na urządzeniu hello. Nie będzie możliwe toocreate woluminów warstwowych z nieprawidłowość punktu i jego nowszych wersjach jako istnieje już miejsca lokalnego na powitania urządzenia toohost hello zestaw roboczy hello warstwowej woluminu. Istniejące woluminy warstwowe również wpływają na dostępne miejsce hello. Jeśli na przykład masz urządzenie 8100 z woluminami warstwowymi o wielkości około 106 TB, tylko 4 TB są dostępne dla woluminów przypiętych lokalnie.
      
       Witaj poniższy obraz przedstawia hello **podstawowe ustawienia** okno dialogowe dla woluminu przypiętego lokalnie.
      
        ![Dodawanie woluminu lokalnego](./media/storsimple-create-volume-u2/add-local-volume-include.png)
      
       Witaj poniższy obraz przedstawia hello **podstawowe ustawienia** okno dialogowe woluminu warstwowego.
      
        ![Dodawanie woluminu lokalnego](./media/storsimple-create-volume-u2/add-tiered-volume-include.png)
   
   1. Kliknij ikonę strzałki hello ![ikona strzałki](./media/storsimple-create-volume-u2/HCS_ArrowIcon-include.png) toogo toohello następnej strony.
3. W hello **dodatkowe ustawienia** okna dialogowego, Dodaj nowy rekord kontroli dostępu (ACR):
   
   1. Wypełnij pole **Nazwa** dla rekordu ACR.
   2. W obszarze **Nazwa inicjatora iSCSI**, podaj hello iSCSI kwalifikowana nazwa (IQN) hosta z systemem Windows. Jeśli nie masz hello IQN, przejdź zbyt[hello Get IQN hosta z systemem Windows Server](#get-the-iqn-of-a-windows-server-host).
   3. W obszarze **domyślnego tworzenia kopii zapasowej dla tego woluminu?**, wybierz pozycję hello **włączyć** pole wyboru. Witaj domyślnego tworzenia kopii zapasowej tworzy zasady, która jest wykonywana co 22:30 każdego dnia (czas urządzenia) i tworzy migawkę chmury dla tego woluminu.
      
      > [!NOTE]
      > Po hello kopii zapasowej jest włączona w tym miejscu, nie można przywrócić. Należy tooedit hello woluminu toomodify to ustawienie.
      > 
      > 
      
      ![Dodawanie woluminu](./media/storsimple-create-volume-u2/AddVolumeAdditionalSettings1.png)
4. Kliknij ikonę znacznika wyboru hello ![ikona znacznika wyboru](./media/storsimple-create-volume-u2/HCS_CheckIcon-include.png). Wolumin zostanie utworzona z hello określone ustawienia.

