1. Uruchamianie hello Azure Site Recovery UnifiedSetup.exe
2. W **przed rozpoczęciem**, wybierz pozycję **dodać dodatkowych procesów serwerów tooscale limit wdrożenia**.

  ![Dodawanie serwera przetwarzania](./media/site-recovery-add-process-server/ps-page-1.png)

3. W **szczegóły konfiguracji serwera**, określ adres IP hello powitania serwera konfiguracji i hello hasło.

  ![Dodawanie serwera przetwarzania 2](./media/site-recovery-add-process-server/ps-page-2.png)
4. W **internetowe**, określ, jak dostawca uruchomiony na powitania serwera konfiguracji łączy tooAzure usługi Site Recovery za pośrednictwem hello hello Internet.

  ![Dodawanie serwera przetwarzania 3](./media/site-recovery-add-process-server/ps-page-3.png)

   * Tooconnect z powitania serwera proxy, który jest obecnie skonfigurowane na maszynie hello, zaznacz **Połącz przy użyciu istniejących ustawień serwera proxy**.
   * Tooconnect dostawcy hello bezpośrednio, wybierz opcję **Połącz bezpośrednio bez serwera proxy**.
   * Jeśli hello istniejący serwer proxy wymaga uwierzytelniania lub chcesz toouse niestandardowego serwera proxy dla połączenia z dostawcą hello, wybierz **Połącz przy użyciu niestandardowych ustawień serwera proxy**.

     * Jeśli używasz niestandardowego serwera proxy, należy toospecify hello adres, port oraz poświadczenia.
     * Jeśli używasz serwera proxy, możesz już zezwolono adresy URL usługi toohello dostępu.

5. W **Sprawdzanie wymagań wstępnych**, Instalator uruchamia się, że instalacja może zostać uruchomiona toomake wyboru. Jeśli zostanie wyświetlone ostrzeżenie o hello **wyboru synchronizacji czasem globalnym**, sprawdź tego czasu hello na powitania zegara systemowego (**Data i godzina** ustawienia) jest hello takie same jak hello strefy czasowej.

     ![Dodawanie serwera przetwarzania 4](./media/site-recovery-add-process-server/ps-page-4.png)

6. W **szczegóły środowiska**wybierz, czy chcesz zacząć tooreplicate maszyn wirtualnych VMware. Jeśli tak, instalator sprawdzi, czy jest zainstalowany program PowerCLI 6.0.

     ![Dodawanie serwera przetwarzania 5](./media/site-recovery-add-process-server/ps-page-5.png)

7. W **zainstalować lokalizacji**, wybierz, gdzie mają plików binarnych hello tooinstall i przechowywania w pamięci podręcznej hello. wybranego dysku Hello musi mieć co najmniej 5 GB dostępnego miejsca na dysku, ale zalecamy dysk pamięci podręcznej z co najmniej 600 GB wolnego miejsca.
     ![Dodawanie serwera przetwarzania 5](./media/site-recovery-add-process-server/ps-page-6.png)

8. W **wybór sieci**, określ hello odbiornika (kartę sieciową i SSL port) na które powitania serwera konfiguracji wysyła i odbiera dane replikacji. Port 9443 hello domyślny port jest używany do wysyłania i odbierania ruchu związanego z replikacją, ale można modyfikować tej toosuit numer portu wymagania w danym środowisku. Dodawanie portu toohello 9443 firma Microsoft również otworzyć portu 443, który jest używany przez operacje replikacji tooorchestrate serwera sieci web. Nie należy używać portu 443 do wysyłania i odbierania ruchu związanego z replikacją.

     ![Dodawanie serwera przetwarzania 6](./media/site-recovery-add-process-server/ps-page-7.png)
9. W **Podsumowanie**, przejrzyj hello informacje i kliknij przycisk **zainstalować**. Po zakończeniu instalacji generowane jest hasło. Będzie ono potrzebne po włączeniu replikacji, dlatego skopiuj je i przechowuj w bezpiecznym miejscu.

     ![Dodawanie serwera przetwarzania 7](./media/site-recovery-add-process-server/ps-page-8.png)
