

## <a name="generate-hello-certificate-signing-request-file"></a>Generowanie pliku żądania podpisania certyfikatu hello
Witaj Apple Push Notification Service (APNS) używa certyfikatów tooauthenticate powiadomień wypychanych. Wykonaj te instrukcje toocreate hello niezbędne wypychania certyfikatu toosend i odbierane powiadomienia. Aby uzyskać więcej informacji dotyczących tych pojęć Zobacz oficjalne hello [Apple Push Notification Service](http://go.microsoft.com/fwlink/p/?LinkId=272584) dokumentacji.

Generowanie pliku certyfikatu podpisywania żądania obsługi hello, który jest używany przez Apple toogenerate podpisanego certyfikatu powiadomień wypychanych.

1. Na komputerze Mac Uruchom narzędzie Keychain Access hello. Można go otworzyć z hello **narzędzia** folderu lub hello **innych** folderu na konsoli uruchamiania hello.
2. Kliknij opcję **Keychain Access**, rozwiń węzeł **Asystent certyfikatu**, a następnie kliknij opcję **Żądaj certyfikatu od urzędu certyfikacji...**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-request-cert-from-ca.png)
3. Wybierz użytkownika **adres E-mail użytkownika** i **nazwa pospolita** , upewnij się, że **zapisane toodisk** jest zaznaczone, a następnie kliknij przycisk **Kontynuuj**. Pozostaw hello **adres E-mail urzędu certyfikacji** pola puste, ponieważ nie jest to wymagane.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-csr-info.png)
4. Wpisz nazwę pliku certyfikatu podpisywania żądania obsługi hello w **Zapisz jako**, wybierz lokalizację hello w **gdzie**, następnie kliknij przycisk **zapisać**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-save-csr.png)
   
      To plik CSR hello jest zapisywany w lokalizacji hello wybrane. lokalizacją domyślną Hello jest hello pulpitu. Należy pamiętać hello lokalizację wybraną dla tego pliku.

Następnie zostanie zarejestrować aplikację w firmie Apple, Włącz powiadomienia wypychane i przekazać ten toocreate CSR wyeksportowany certyfikat powiadomień wypychanych.

## <a name="register-your-app-for-push-notifications"></a>Rejestrowanie aplikacji dla usługi powiadomień wypychanych
toobe toosend stanie wypychania powiadomień tooan aplikacji dla systemu iOS, należy zarejestrować aplikacji z firmy Apple, a także rejestru dla powiadomień wypychanych.  

1. Jeśli nie zarejestrowano jeszcze aplikacji, przejdź toohello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">systemu iOS w portalu inicjowania obsługi</a> hello Centrum deweloperów firmy Apple, logowanie za pomocą Identyfikatora firmy Apple, kliknij **identyfikatory**, następnie kliknij przycisk **identyfikatorów aplikacji** , a na koniec kliknij hello  **+**  zarejestrować tooregister nowej aplikacji.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids.png)
      
2. Zaktualizuj następujące trzy pola dla nowej aplikacji hello, a następnie kliknij przycisk **Kontynuuj**:
   
   * **Nazwa**: wpisz nazwę opisową aplikacji hello **nazwa** w hello **opis Identyfikatora aplikacji** sekcji.
   * **Identyfikator pakietu**: w obszarze hello **jawny identyfikator aplikacji** wprowadź **identyfikator pakietu** w postaci hello `<Organization Identifier>.<Product Name>` jak wspomniano w hello [dystrybucji aplikacji Przewodnik](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/ConfiguringYourApp/ConfiguringYourApp.html#//apple_ref/doc/uid/TP40012582-CH28-SW8). Witaj *identyfikator organizacji* i *nazwa produktu* Użyj musi hello organizacji identyfikator i nazwa produktu, które będą używane podczas tworzenia projektu w programie XCode. W zrzucie się ekranu poniżej pozycja hello *NotificationHubs* służy jako identyfikator organizacji i *GetStarted* jest używana jako nazwa produktu hello. Zagwarantowanie, że odpowiada wartości hello, który będzie używany w projekcie XCode umożliwi możesz toouse hello poprawnego profilu publikowania z XCode. 
   * **Powiadomienia wypychane**: hello wyboru **powiadomień wypychanych** opcję hello **usługi aplikacji** sekcji.
     
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-appid-info.png)
     
      To wygenerowanie Identyfikatora aplikacji oraz wyświetlenie informacji hello tooconfirm. Kliknij przycisk **zarejestrować** tooconfirm hello nowy identyfikator aplikacji.
     
      Po kliknięciu **zarejestrować**, zobaczysz hello **rejestracja ukończona** ekranu, jak pokazano poniżej. Kliknij przycisk **Gotowe**.
      
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-registration-complete.png)


1. W hello Centrum deweloperów w obszarze identyfikatory aplikacji zlokalizuj identyfikator aplikacji hello, który właśnie utworzony i kliknij jego wiersz.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids2.png)
   
      Kliknięcie Identyfikatora aplikacji hello są wyświetlane takie szczegóły aplikacji hello. Kliknij przycisk hello **Edytuj** u dołu hello.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-edit-appid.png)
      
2. Przewiń toohello dolnej części ekranu hello, a następnie kliknij przycisk hello **Utwórz certyfikat...**  przycisk sekcji hello **certyfikat SSL Push programowanie**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-create-cert.png)
   
      Spowoduje to wyświetlenie Asystenta "Dodaj certyfikat iOS" hello.
   
   > [!NOTE]
   > Instrukcje w tym samouczku obejmują użycie certyfikatu deweloperskiego. Witaj, sam proces jest używane podczas rejestrowania certyfikatu produkcyjnego. Upewnij się, że używasz hello sam typ certyfikatu podczas wysyłania powiadomień.
   > 
   > 
3. Kliknij przycisk **wybierz plik**, Przeglądaj toohello lokalizacji, w którym zapisano plik CSR hello utworzonego w pierwszym zadaniem hello, a następnie kliknij przycisk **Generuj**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-cert-choose-csr.png)
4. Po utworzeniu hello certyfikatu przez portal powitania kliknij hello **Pobierz** przycisk **gotowe**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-download-cert.png)
   
      Pobiera certyfikat hello i zapisuje go tooyour komputera w folderze pobrane.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-downloaded.png)
   
   > [!NOTE]
   > Domyślnie program hello pobrany plik certyfikatu deweloperskiego nosi **aps_development.cer**.
   > 
   > 
5. Kliknij dwukrotnie hello pobrany certyfikat powiadomień wypychanych **aps_development.cer**.
   
      Spowoduje to zainstalowanie nowego świadectwa hello w hello łańcucha kluczy, jak pokazano poniżej:
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-in-keychain.png)
   
   > [!NOTE]
   > Nazwa Hello certyfikatu może być inna, ale będzie ona poprzedzona ciągiem **Apple Development iOS Push Services:**.
   > 
   > 
6. W narzędziu Keychain Access kliknij prawym przyciskiem myszy hello nowy certyfikat powiadomień wypychanych utworzony w hello **certyfikaty** kategorii. Kliknij przycisk **wyeksportować**, nazwij plik hello, wybierz hello **.p12** format, a następnie kliknij przycisk **zapisać**.
   
    ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-export-cert-p12.png)
   
    Upewnij się, zanotuj hello nazwę pliku i lokalizację hello wyeksportowanego certyfikatu .p12. Będzie ona używana tooenable uwierzytelniania przy użyciu usługi APNS.
   
   > [!NOTE]
   > W tym samouczku opisano proces tworzenia pliku QuickStart.p12. Nazwa i lokalizacja pliku mogą się różnić.
   > 
   > 

## <a name="create-a-provisioning-profile-for-hello-app"></a>Utwórz profil inicjowania obsługi administracyjnej dla aplikacji hello
1. W hello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">systemu iOS w portalu inicjowania obsługi</a>, wybierz pozycję **profile inicjowania obsługi**, wybierz pozycję **wszystkie**, a następnie kliknij przycisk hello  **+**  toocreate przycisk Nowy profil. Spowoduje to uruchomienie hello **Dodaj profil inicjowania obsługi systemu iOS** Kreatora
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-provisioning-profile.png)
2. Wybierz **tworzenie aplikacji dla systemu iOS** w obszarze **programowanie** jako typ profilu inicjowania obsługi hello, a następnie kliknij przycisk **Kontynuuj**. 
3. Następnie wybierz nowo utworzony hello identyfikator aplikacji hello **identyfikator aplikacji** listy rozwijanej, a następnie kliknij przycisk **Kontynuuj**
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-select-appid-for-provisioning.png)
4. W hello **wybierz certyfikaty** ekranu, wybierz certyfikat programowania zwykle używany do podpisywania kodu, a następnie kliknij przycisk **Kontynuuj**. To nie jest hello wypychania certyfikat, który został utworzony.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-cert.png)
5. Następnie wybierz pozycję hello **urządzeń** toouse testowania, a następnie kliknij przycisk **Kontynuuj**
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-devices.png)
6. Na koniec wybierz nazwę dla profilu hello w **nazwa profilu**, kliknij przycisk **Generuj**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-name-profile.png)
7. Po utworzeniu nowego profilu inicjowania obsługi administracyjnej hello kliknij toodownload ją i zainstaluj go na komputerze deweloperskim Xcode. Następnie kliknij przycisk **Gotowe**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-profile-ready.png)
