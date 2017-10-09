1. Zaloguj się w hello [Azure Portal].
2. Kliknij kolejno opcje **+NOWE** > **Sieci Web i mobilność** > **Aplikacja mobilna**, a następnie podaj nazwę zaplecza aplikacji mobilnej.
3. Dla hello **grupy zasobów**, wybierz istniejącą grupę zasobów lub Utwórz nową (używając hello tej samej nazwie co aplikacja). 
   
    Możesz wybrać inny plan usługi App Service lub utworzyć nowy. Aby uzyskać więcej informacji na temat planów usługi aplikacji i jak toocreate nowego planu w różnych cen warstwy, a w preferowanej lokalizacji, zobacz [szczegółowe omówienie planów usługi aplikacji Azure](../articles/app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
4. Dla hello **planu usługi aplikacji**, hello plan domyślny (w hello [warstwy standardowa](https://azure.microsoft.com/pricing/details/app-service/)) jest zaznaczone. Możesz też wybrać inny plan lub [Utwórz nową](../articles/app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md#create-an-app-service-plan). Witaj planu usługi aplikacji określają ustawienia hello [lokalizację, funkcje, koszt i zasoby obliczeniowe](https://azure.microsoft.com/pricing/details/app-service/) skojarzone z aplikacją. 
   
    Po podjęciu decyzji o hello planu, kliknij przycisk **Utwórz**. Spowoduje to utworzenie zaplecza aplikacji mobilnej hello. 
5. W hello **ustawienia** bloku zaplecze nowej aplikacji mobilnej powitania kliknij **szybki start** > platforma aplikacji klienta > **połączyć z bazą danych**. 
   
    ![](./media/app-service-mobile-dotnet-backend-create-new-service/dotnet-backend-create-data-connection.png)
6. W hello **Dodaj połączenie danych** bloku, kliknij przycisk **bazy danych SQL** > **Utwórz nową bazę danych**, bazy danych hello typu **nazwa**, Wybierz warstwę cenową, a następnie kliknij przycisk **serwera**.  Możesz użyć tej nowej bazy danych ponownie. Jeśli masz już bazę danych w hello tej samej lokalizacji, zamiast tego możesz **Użyj istniejącej bazy danych**. Witaj bazy danych w innej lokalizacji nie jest zalecane toobandwidth kosztów i większego opóźnienia.
   
    ![](./media/app-service-mobile-dotnet-backend-create-new-service/dotnet-backend-create-db.png)
7. W hello **nowy serwer** bloku, wpisz unikatową nazwą serwera w hello **nazwy serwera** Podaj identyfikator logowania i hasło, sprawdź **Zezwalaj usługom platformy azure tooaccess serwera**i kliknij przycisk **OK**. Spowoduje to utworzenie nowej bazy danych hello.
8. Po powrocie do hello **Dodaj połączenie danych** bloku, kliknij przycisk **ciąg połączenia**, wpisz hello wartości identyfikator logowania i hasło dla bazy danych i kliknij przycisk **OK**. Poczekaj kilka minut, aż hello toobe bazy danych pomyślnie wdrożone przed kontynuowaniem.

<!-- URLs. -->
[Azure Portal]: https://portal.azure.com/
