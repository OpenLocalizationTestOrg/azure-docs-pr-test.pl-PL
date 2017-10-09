<!--author=alkohli last changed: 07/19/2017-->

#### <a name="toocreate-a-volume"></a>toocreate woluminu
1. Z hello Tabelaryczny spis urządzeń hello w hello **urządzeń** bloku, wybierz swoje urządzenie. Kliknij pozycję **+ Dodaj wolumin**.

    ![Dodawanie nowego woluminu](./media/storsimple-8000-create-volume-u2/step5createvol1.png)

2. W hello **Dodaj wolumin** bloku:
   
   1. Witaj **wybierz urządzenie** pole jest wypełniane automatycznie z bieżącego urządzenia.

   2. Z listy rozwijanej hello Wybierz kontener woluminów hello wymagających tooadd woluminu. 

   3.  Wpisz wartość pola **Nazwa** dla woluminu. Wolumin nie można zmienić po utworzeniu hello woluminu.

   4. Na liście rozwijanej hello, wybierz hello **typu** dla woluminu. W przypadku obciążeń, które wymagają lokalnych gwarancji, małych opóźnień i większej wydajności, wybierz wolumin typu **Przypięty lokalnie**. W przypadku wszystkich innych danych wybierz wolumin typu **Warstwowy**. Jeśli używasz tego woluminu na potrzeby danych archiwalnych, wybierz opcję **Użyj tego woluminu w przypadku rzadziej używanych danych archiwalnych**.
      
       Wolumin warstwowy jest alokowany elastycznie i można go szybko utworzyć. Wybieranie **Użyj tego woluminu w przypadku rzadziej używanych danych archiwalnych** dla woluminu warstwowego celem danych archiwalnych zmiany hello rozmiaru fragmentu deduplikacji dla woluminu too512 KB. Jeśli to pole nie jest zaznaczone, odpowiedni wolumin warstwowy hello używa rozmiaru fragmentu wynoszącego 64 KB. Większy rozmiar fragmentu deduplikacji umożliwia hello urządzenia tooexpedite hello transferu dużej ilości danych archiwalnych toohello chmury.
       
       Wolumin przypięty lokalnie jest alokowany nieelastycznie i gwarantuje, że hello główne dane na woluminie hello pozostaje toohello lokalne urządzenia i nie zostaną przeniesione toohello chmury.  Jeśli tworzysz wolumin przypięty lokalnie, urządzenia hello wyszukuje dostępne miejsce w warstwach lokalne powitania tooprovision hello ilość hello żądany rozmiar. Witaj operacji tworzenia woluminu przypiętego lokalnie może obejmować przenoszenie istniejących danych z chmury toohello urządzenia hello i czas hello toocreate hello woluminu może trwać długo. Łączny czas Hello zależy od rozmiaru hello hello elastycznie woluminu, dostępnej przepustowości sieci i danych hello na urządzeniu.

   5. Określ hello **alokowana pojemność** dla woluminu. Zanotuj hello pojemności dostępnej w oparciu wybrany typ woluminu hello. Witaj określony rozmiar woluminu nie może przekraczać hello dostępnego miejsca.
      
       Można alokować woluminy przypięte lokalnie w górę too8.5 TB lub woluminy warstwowe się too200 TB na urządzeniu 8100 hello. Na urządzeniu 8600 większych hello można udostępnić woluminów przypiętych lokalnie too22.5 TB lub woluminy warstwowe się too500 TB. Lokalne miejsce na urządzeniu hello jest hello wymagane toohost pracy zestaw woluminów warstwowych, tworzenie woluminów przypiętych lokalnie ma wpływ na powitania miejsce dostępne do alokowania na woluminach warstwowych. Dlatego jeśli tworzysz wolumin przypięty lokalnie, miejsce dostępne na potrzeby tworzenia woluminów warstwowych zmniejsza się. Podobnie jeśli został utworzony wolumin warstwowy, zostanie zmniejszona hello dostępnego miejsca na potrzeby tworzenia woluminów przypiętych lokalnie.
      
       Jeśli dostarczasz woluminu przypiętego lokalnie 8,5 TB (maksymalny dozwolony rozmiar) na urządzeniu 8100 zostały wyczerpane wszystkich hello lokalne miejsce dostępne na urządzeniu hello. Nie można tworzyć woluminów warstwowych od tego momentu i jego nowszych wersjach, ponieważ nie ma już miejsca lokalnego na powitania urządzenia toohost hello zestaw roboczy hello warstwowej woluminu. Istniejące woluminy warstwowe również wpływają na dostępne miejsce hello. Jeśli na przykład masz urządzenie 8100 z woluminami warstwowymi o wielkości około 106 TB, tylko 4 TB są dostępne dla woluminów przypiętych lokalnie.

    6. W hello **połączone hosty** kliknij strzałkę hello. 

        ![Połączone hosty](./media/storsimple-8000-create-volume-u2/step5createvol2.png)

    7. W hello **połączone hosty** bloku, wybierz istniejący ACR lub Dodaj nowe ACR, wykonując następujące kroki hello:

       1. Wypełnij pole **Nazwa** dla rekordu ACR.
       2. W obszarze **Nazwa inicjatora iSCSI**, podaj hello iSCSI kwalifikowana nazwa (IQN) hosta z systemem Windows. Jeśli nie masz hello IQN, przejdź zbyt[hello Get IQN hosta z systemem Windows Server](#get-the-iqn-of-a-windows-server-host).

    9. Kliknij przycisk **Utwórz**. Wolumin zostanie utworzona z hello określone ustawienia.

        ![Kliknięcie pozycji Utwórz](./media/storsimple-8000-create-volume-u2/step5createvol3.png)

        > [!NOTE]
        > Należy pamiętać, hello wolumin, który został utworzony w tym miejscu nie jest chroniony. Z tego woluminu tootake zaplanowane tworzenie kopii zapasowych należy toocreate i Skojarz zasady tworzenia kopii zapasowej. 

