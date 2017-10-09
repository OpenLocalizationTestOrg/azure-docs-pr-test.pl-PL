<!--author=alkohli last changed: 02/06/17-->

#### <a name="tooinstall-an-update-from-hello-azure-portal"></a>tooinstall aktualizacji z hello portalu Azure

1. Na stronie usługi StorSimple hello wybierz urządzenie. Przejdź za**urządzeń** > **konserwacji**.
2. U dołu hello hello strony, kliknij przycisk **Wyszukaj aktualizacje**. Zadanie jest tworzone tooscan dostępności aktualizacji. Użytkownik jest powiadamiany o hello zadanie zostało ukończone pomyślnie.
3. W hello **aktualizacji oprogramowania** sekcji na powitania takie same, hello nowe aktualizacje oprogramowania są dostępne. Firma Microsoft zaleca przejrzenie hello informacje o wersji przed zainstalowaniem aktualizacji na urządzeniu.
4. U dołu hello hello strony, kliknij przycisk **Zainstaluj aktualizacje**, a następnie **OK**.
5. W hello **instalowania aktualizacji** okno dialogowe, upewnij się, że zostały wykonane hello zalecenia, a następnie wybierz **I zrozumieć hello powyżej wymagań i am tooupgrade gotowe urządzenie** i kliknij przycisk wyboru hello przycisk.
   
    ![Komunikat z potwierdzeniem](./media/storsimple-install-update2-via-portal/InstallUpdate12_2M.png)
6. Zostanie rozpoczęty zestaw testów wymagań wstępnych. Testy te obejmują:
   
   * **Sprawdzanie kondycji kontrolera** tooverify zarówno tekst hello kontrolery urządzeń są w dobrej kondycji i w trybie online.
   * **Sprawdzanie kondycji składnika sprzętu** tooverify czy hello wszystkie składniki sprzętowe w urządzeniu StorSimple są w dobrej kondycji.
   * **Sprawdza dane 0** tooverify, że dane 0 jest włączone na urządzeniu. Jeśli ten interfejs nie jest włączony, należy go włączyć i ponowić próbę.
   * **DANE 2 i dane 3 kontroli** tooverify interfejsy sieciowe dane 2 i 3 dane nie są włączone. Jeśli te interfejsy są włączone, należy wyłączyć te i spróbuj tooupdate urządzenia. Ten test jest przeprowadzany tylko wtedy, gdy aktualizowane jest urządzenie z oprogramowaniem w wersji ogólnie dostępnej. Urządzenia z wersjami oprogramowania 0.1, 0.2 i 0.3 nie wymagają tego testu.
   * **Sprawdź bramy** na dowolnym urządzeniu uruchomione wcześniejsze tooUpdate wersji 1. To sprawdzenie odbywa się na wszystkie urządzenia hello oprogramowaniem 1 przed aktualizacją, ale nie powiedzie się na urządzeniach hello, które skonfigurowano dla interfejsu sieciowego, inne niż dane 0 bramę.
     
     Aktualizacja Hello jest stosowana, gdy wszystkie testy zostały wykonane pomyślnie. Użytkownik jest powiadamiany o kontroli hello są w toku.
     
     ![Powiadomienie poprzedzające testy](./media/storsimple-install-update2-via-portal/InstallUpdate12_3M.png)
     
     Hello poniżej przedstawiono przykład, w którym nie powiodło się sprawdzenie hello. Należy sprawdzić, czy zarówno kontrolery urządzeń hello dobrej kondycji i w trybie online. Należy również kondycję hello toocheck hello składniki sprzętowe. W tym przykładzie uwagi wymagają składniki Controller 0 i Controller 1. Jeśli nie można rozwiązać te problemy przez siebie może być konieczne toocontact Support firmy Microsoft.
     
       ![Nieudane testy](./media/storsimple-install-update2-via-portal/HCS_PreUpgradeChecksFailed-include.png)
7. Po kontroli hello pomyślnym zakończeniu zadania aktualizacji zostanie utworzony. Użytkownik jest powiadamiany o pomyślnym utworzeniu zadania aktualizacji hello.
   
    ![Tworzenie zadania aktualizacji](./media/storsimple-install-update2-via-portal/InstallUpdate12_44M.png)
   
    Aktualizacja Hello następnie jest stosowana na urządzeniu.
    
8. postęp hello toomonitor hello zadanie aktualizacji, kliknij przycisk **zadania**. Na powitania **zadania** strony, zostanie wyświetlony hello aktualizacji w toku.
9. Aktualizacja Hello zajmuje kilka godzin toocomplete. Wybierz zadanie aktualizacji hello i kliknij przycisk **szczegóły** tooview hello szczegóły zadania hello w dowolnym momencie.
10. Po zakończeniu zadania hello Przejdź toohello **konserwacji** stronie, a następnie przewiń w dół za**aktualizacji oprogramowania**.

