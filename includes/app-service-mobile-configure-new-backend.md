
1. Kliknij przycisk hello **usługi aplikacji** przycisk Wybierz użytkownika zaplecza aplikacji mobilnej, wybierz **szybkiego startu**, a następnie wybierz platformę klienta (systemy iOS, Android, Xamarin, Cordova).

    ![Witryna Azure Portal z wyróżnioną pozycją Mobile Apps — szybki start][quickstart]

2. Jeśli nie skonfigurowano połączenia z bazą danych, utwórz go, wykonując następujące hello:

    ![Portal Azure Mobile Apps Connect toodatabase][connect]

    a. Utwórz nową bazę danych SQL i serwer.

    ![Witryna Azure Portal z opcją tworzenia nowej bazy danych i serwera funkcji Mobile Apps][server]

    b. Poczekaj, aż hello połączenie danych został utworzony pomyślnie.

    ![Powiadomienie witryny Azure Portal o pomyślnym utworzeniu połączenia danych][notification]

    c. Połączenie danych musi się powieść.

    ![Powiadomienie witryny Azure Portal „Masz już połączenie danych”][already-connection]

3. W obszarze **2. Utwórz tabelę interfejsu API** wybierz dla języka Node.js opcję **Język zaplecza**. 
 
4. Zaakceptuj potwierdzenie hello, a następnie wybierz **Utwórz tabelę TodoItem**.  
    Ta akcja spowoduje utworzenie nowej tabeli elementów do wykonania w bazie danych. 

    >[!IMPORTANT]
    > Przełączenie istniejącej tooNode.js zaplecza spowoduje zastąpienie całej zawartości. Zamiast tego zobacz zaplecze .NET toocreate [działać z serwerem hello zaplecza .NET SDK dla aplikacji mobilnych][instructions].

<!-- Images. -->
[quickstart]: ./media/app-service-mobile-configure-new-backend/quickstart.png
[connect]: ./media/app-service-mobile-configure-new-backend/connect-to-bd.png
[notification]: ./media/app-service-mobile-configure-new-backend/notification-data-connection-create.png
[server]: ./media/app-service-mobile-configure-new-backend/create-new-server.png
[already-connection]: ./media/app-service-mobile-configure-new-backend/already-connection.png

<!-- URLs -->
[instructions]: ../articles/app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#create-app
