#### <a name="configure-hello-ios-project-in-xamarin-studio"></a>Konfigurowanie projektu iOS hello w programie Xamarin Studio
1. Otwórz w Xamarin.Studio, **Info.plist**i hello aktualizacji **identyfikator pakietu** z hello pakietu utworzonego wcześniej z identyfikatorem aplikacji nowego Identyfikatora

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-21.png)
2. Przewiń w dół za**tryby tła**. Wybierz hello **Włącz tryby tła** pole i hello **zdalnego powiadomienia** pole.

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-22.png)
3. Kliknij dwukrotnie plik projektu w hello panelu rozwiązania tooopen **opcje projektu**.
4. W obszarze **kompilacji**, wybierz **iOS podpisywania pakietu**, wybierz hello odpowiedniego tożsamości i profil inicjowania obsługi administracyjnej właśnie skonfigurowany dla tego projektu.

   ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-20.png)

   Dzięki temu projektu hello używa nowego profilu hello do podpisywania kodu. Witaj inicjowania obsługi administracyjnej dokumentacji oficjalnego urządzenia Xamarin, zobacz [Inicjowanie obsługi administracyjnej urządzeń Xamarin].

#### <a name="configure-hello-ios-project-in-visual-studio"></a>Konfigurowanie projektu iOS hello w programie Visual Studio
1. W programie Visual Studio, kliknij prawym przyciskiem myszy projekt hello, a następnie kliknij przycisk **właściwości**.
2. Na stronach właściwości powitania kliknij hello **aplikacji systemu iOS** kartę i hello aktualizacji **identyfikator** o identyfikatorze hello, który został utworzony wcześniej.

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-23.png)
3. W hello **iOS podpisywania pakietu** karcie hello wybierz odpowiedni tożsamości i inicjowania obsługi profilu można właśnie skonfigurowane zapasowej dla tego projektu.

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-24.png)

    Dzięki temu projektu hello używa nowego profilu hello do podpisywania kodu. Witaj inicjowania obsługi administracyjnej dokumentacji oficjalnego urządzenia Xamarin, zobacz [Inicjowanie obsługi administracyjnej urządzeń Xamarin].
4. Kliknij dwukrotnie Info.plist tooopen, a następnie Włącz **RemoteNotifications** w obszarze **tryby tła**.

[Inicjowanie obsługi administracyjnej urządzeń Xamarin]: http://developer.xamarin.com/guides/ios/getting_started/installation/device_provisioning/
