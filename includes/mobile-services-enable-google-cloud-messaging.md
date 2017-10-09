
1. Przejdź toohello [Google Cloud Console](https://console.developers.google.com/project), zaloguj się przy użyciu poświadczeń konta Google. 
2. Kliknij opcję **Create Project** (Utwórz projekt), wpisz nazwę projektu, a następnie kliknij przycisk **Create** (Utwórz). Jeśli jest to wymagane, wykonać hello weryfikację SMS i kliknij przycisk **Utwórz** ponownie.
   
    ![Tworzenie nowego projektu](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-new-project.png)   
   
     Wpisz nową nazwę w polu **Project name** (Nazwa projektu) i kliknij pozycję **Create project** (Utwórz projekt).
3. Kliknij przycisk hello **narzędzia i inne** przycisk, a następnie kliknij przycisk **informacji o projekcie**. Zanotuj hello **numer projektu**. Konieczne będzie tooset tej wartości jako hello `SenderId` zmiennej w powitania klienta aplikacji.
   
    ![Narzędzia i nie tylko](./media/mobile-services-enable-google-cloud-messaging/notification-hubs-utilities-and-more.png)
4. W hello projektu pulpitu nawigacyjnego, w obszarze **mobilnych interfejsów API**, kliknij przycisk **Google Cloud Messaging**, następnie na następnej stronie powitania kliknij **Włącz interfejs API** i zaakceptuj postanowienia hello usługi. 
   
    ![Włączanie usługi GCM](./media/mobile-services-enable-google-cloud-messaging/enable-GCM.png)
   
    ![Włączanie usługi GCM](./media/mobile-services-enable-google-cloud-messaging/enable-gcm-2.png) 
5. Na pulpicie nawigacyjnym projektu hello, kliknij przycisk **poświadczenia** > **poświadczenie tworzenia** > **klucz interfejsu API**. 
   
    ![](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-create-server-key.png)
6. W obszarze **Create a new key** (Utwórz nowy klucz) kliknij opcję **Server key** (Klucz serwera), wpisz nazwę klucza, a następnie kliknij przycisk **Create** (Utwórz).
7. Zanotuj hello **klucz interfejsu API** wartość.
   
    Spowoduje to tooenable wartość klucza interfejsu API Azure tooauthenticate za pomocą usługi GCM i wysyłania powiadomień wypychanych w imieniu aplikacji.

