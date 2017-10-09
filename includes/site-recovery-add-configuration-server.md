1. Uruchom plik instalacji Instalator Unified hello.
2. W **przed rozpoczęciem**, wybierz pozycję **zainstalować hello konfiguracji serwera i serwera przetwarzania**.

    ![Przed rozpoczęciem](./media/site-recovery-add-configuration-server/combined-wiz1.png)

3. W **licencji na oprogramowanie innych firm**, kliknij przycisk **akceptuję** toodownload i zainstaluj MySQL.

    ![Oprogramowanie innych producentów](./media/site-recovery-add-configuration-server/combined-wiz2.png)
4. W **rejestracji**, wybierz pozycję hello klucza rejestracji pobranego z hello magazynu.

    ![Rejestracja](./media/site-recovery-add-configuration-server/combined-wiz3.png)
5. W **internetowe**, określ, jak dostawca uruchomiony na serwerze konfiguracji hello łączy tooAzure usługi Site Recovery za pośrednictwem hello hello Internet.

   a. Tooconnect z powitania serwera proxy, który jest obecnie skonfigurowane na maszynie hello, zaznacz **połączyć tooAzure Przywracanie lokacji z użyciem serwera proxy**.

   b. Tooconnect dostawcy hello bezpośrednio, wybierz opcję **łączą się bezpośrednio tooAzure odzyskiwania lokacji bez serwera proxy**.

   c. Jeśli hello istniejący serwer proxy wymaga uwierzytelniania lub chcesz toouse niestandardowego serwera proxy dla połączenia z dostawcą hello, wybierz **Połącz przy użyciu niestandardowych ustawień serwera proxy**.

     * Jeśli używasz niestandardowego serwera proxy, należy toospecify hello adres, port oraz poświadczenia.
     * Jeśli używasz serwera proxy, możesz już zezwolono hello adresów URL opisanych w [wymagania wstępne](#prerequisites).

     ![Zapora](./media/site-recovery-add-configuration-server/combined-wiz4.png)
6. W **Sprawdzanie wymagań wstępnych**, Instalator uruchamia się, że instalacja może zostać uruchomiona toomake wyboru. Jeśli zostanie wyświetlone ostrzeżenie o hello **wyboru synchronizacji czasem globalnym**, sprawdź tego czasu hello na powitania zegara systemowego (**Data i godzina** ustawienia) jest hello takie same jak hello strefy czasowej.

    ![Wymagania wstępne](./media/site-recovery-add-configuration-server/combined-wiz5.png)
7. W **konfiguracji MySQL**, Utwórz poświadczenia logowania w wystąpieniu serwera MySQL toohello, który jest zainstalowany.

    ![MySQL](./media/site-recovery-add-configuration-server/combined-wiz6.png)
8. W **szczegóły środowiska**wybierz, czy chcesz zacząć tooreplicate maszyn wirtualnych VMware. Jeśli jesteś, Instalator sprawdza, czy zainstalowana jest PowerCLI 6.0.

    ![MySQL](./media/site-recovery-add-configuration-server/combined-wiz7.png)

9. W **zainstalować lokalizacji**, wybierz, gdzie mają plików binarnych hello tooinstall i przechowywania w pamięci podręcznej hello. wybranego dysku Hello musi mieć co najmniej 5 GB dostępnego miejsca na dysku, ale zalecamy dysk pamięci podręcznej z co najmniej 600 GB wolnego miejsca.

    ![Lokalizacja instalacji](./media/site-recovery-add-configuration-server/combined-wiz8.png)
10. W **wybór sieci**, określ hello odbiornika (kartę sieciową i SSL port), na które wysyła hello konfiguracji serwera i odbiera dane replikacji. Port 9443 hello domyślny port jest używany do wysyłania i odbierania ruchu związanego z replikacją, ale można modyfikować tej toosuit numer portu wymagania w danym środowisku. Dodawanie portu toohello 9443 firma Microsoft również otworzyć portu 443, który jest używany przez operacje replikacji tooorchestrate serwera sieci web. Nie należy używać portu 443 do wysyłania i odbierania ruchu związanego z replikacją.

    ![Wybór sieci](./media/site-recovery-add-configuration-server/combined-wiz9.png)


11. W **Podsumowanie**, przejrzyj hello informacje i kliknij przycisk **zainstalować**. Po zakończeniu instalacji generowane jest hasło. Będzie ono potrzebne po włączeniu replikacji, dlatego skopiuj je i przechowuj w bezpiecznym miejscu.

    ![Podsumowanie](./media/site-recovery-add-configuration-server/combined-wiz10.png)

Po zakończeniu rejestracji serwer hello jest wyświetlany na powitania **ustawienia** > **serwerów** bloku w magazynie hello.
