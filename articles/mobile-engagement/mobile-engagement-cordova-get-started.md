---
title: aaaGet Started with Azure Mobile Engagement dla oprogramowania Cordova/Phonegap
description: "Dowiedz się, jak toouse usługi Azure Mobile Engagement z funkcją analizy i powiadomieniami Wypychanymi dla aplikacji Cordova/Phonegap."
services: mobile-engagement
documentationcenter: Mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 54fe9113-e239-4ed7-9fd1-a502d7ac7f47
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-phonegap
ms.devlang: js
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: e67dabbdf7886802bb058f38964e558d5ae6854c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-cordovaphonegap"></a>Rozpoczynanie pracy z usługą Azure Mobile Engagement dla oprogramowania Cordova/Phonegap
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

W tym temacie opisano sposób użycia i wysyłania wypychania powiadomień toosegmented użytkownikom aplikacji dla aplikacji mobilnych opracowanych za pomocą oprogramowania Cordova toounderstand usługi Azure Mobile Engagement toouse.

W tym samouczku utworzymy pustą aplikację Cordova za pomocą komputera Mac, a następnie zintegrujemy zestaw Mobile Engagement SDK. Rozwiązanie będzie zbierać dane analityczne i odbierać powiadomienia wypychane za pomocą systemu Apple Push Notification System (APNS) dla systemów iOS oraz usługi Google Cloud Messaging (GCM) dla systemów Android. Wdrożymy ten tooan z systemem iOS lub Android urządzenia do testowania. 

> [!NOTE]
> toocomplete tego samouczka, musi mieć aktywne konto platformy Azure. Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-cordova-get-started).
> 
> 

Ten samouczek wymaga następujących hello:

* Środowisko XCode, które można zainstalować ze sklepu Mac App Store (w przypadku wdrożenia tooiOS)
* [Android SDK oraz Emulator](http://developer.android.com/sdk/installing/index.html) (w przypadku wdrożenia tooAndroid)
* Certyfikat powiadomień wypychanych (.p12), który można uzyskać z Centrum deweloperów firmy Apple dla rozwiązań systemu APNS
* Numer GCM projektu, który można uzyskać z konsoli dla deweloperów Google dla usługi GCM
* [Wtyczka Mobile Engagement Cordova](https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-engagement)

> [!NOTE]
> Można znaleźć kodu źródłowego hello i hello plik ReadMe dla wtyczki Cordova hello na [GitHub](https://github.com/Azure/azure-mobile-engagement-cordova)
> 
> 

## <a id="setup-azme"></a>Konfigurowanie usługi Mobile Engagement dla aplikacji Cordova
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Połączenie z zapleczem usługi Mobile Engagement toohello aplikacji
Ten samouczek przedstawia "podstawową integrację", który czy hello minimalny wymagany toocollect danych i wysyłania powiadomień wypychanych. 

Utworzymy podstawową aplikację z integracją hello toodemonstrate Cordova:

### <a name="create-a-new-cordova-project"></a>Tworzenie nowego projektu Cordova
1. Uruchom *Terminal* okno na Twojej Mac maszyny i typ powitania po, co spowoduje utworzenie nowego projektu oprogramowania Cordova z hello domyślny szablon. Upewnij się, że publikowanie hello profil możesz ostatecznie toodeploy użycia aplikacji systemu iOS używa frazy "com.mycompany.myapp" jako hello identyfikator aplikacji. 
   
        $ cordova create azme-cordova com.mycompany.myapp
        $ cd azme-cordova
2. Wykonaj następujące tooconfigure hello projektu dla **iOS** i uruchom go w hello symulatora systemu iOS:
   
        $ cordova platform add ios 
        $ cordova run ios
3. Wykonaj następujące tooconfigure hello projektu dla **Android** i uruchom go w emulatorze systemu Android hello. Upewnij się, że ustawienia emulatora Android SDK uwzględniają cel w formie interfejsów API firmy Google (Google Inc.) hello procesor CPU / ABI jako menedżerem ARM interfejsów API firmy Google.  
   
        $ cordova platform add android
        $ cordova run android
4. Dodaj wtyczkę konsoli Cordova hello. 

    ```
    $ cordova plugin add cordova-plugin-console
    ``` 

### <a name="connect-your-app-toomobile-engagement-backend"></a>Połącz zapleczu swojej aplikacji tooMobile zaangażowania
1. Zainstaluj wtyczkę Azure Mobile Engagement Cordova hello zapewniając hello wartości zmiennych tooconfigure hello wtyczki:
   
        cordova plugin add cordova-plugin-ms-azure-mobile-engagement    
             --variable AZME_IOS_CONNECTION_STRING=<iOS Connection String> 
            --variable AZME_IOS_REACH_ICON=... (icon name WITH extension) 
            --variable AZME_ANDROID_CONNECTION_STRING=<Android Connection String> 
            --variable AZME_ANDROID_REACH_ICON=... (icon name WITHOUT extension)       
            --variable AZME_ANDROID_GOOGLE_PROJECT_NUMBER=... (From your Google Cloud console for sending push notifications) 
            --variable AZME_ACTION_URL =... (URL scheme which triggers hello app for deep linking)
            --variable AZME_ENABLE_NATIVE_LOG=true|false
            --variable AZME_ENABLE_PLUGIN_LOG=true|false

*Android Reach ikona* : musi być nazwą hello hello zasobu bez rozszerzenia i prefiksu drawable (np: mynotificationicon), a plik ikony hello musi być skopiowany do projektu systemu android (Platform/android/res/drawable)

*iOS Reach Icon* : musi być nazwą hello hello zasobu z rozszerzeniem (np: mynotificationicon.png), a plik ikony hello musi zostać dodany do projektu systemu iOS z XCode (przy użyciu hello Menu Dodaj pliki)

## <a id="monitor"></a>Włączanie monitorowania w czasie rzeczywistym
1. W projekcie Cordova hello — Edytuj **www/js/index.js** wywołania hello tooadd tooMobile Engagement toodeclare nowe działanie po hello *deviceReady* odebraniu zdarzenia.
   
         onDeviceReady: function() {
                Engagement.startActivity("myPage",{});
            }
2. Uruchamianie aplikacji hello:
   
   * **W przypadku systemu iOS**
     
       W `Terminal` okna Uruchom aplikację w nowym wystąpieniu narzędzia Simulator, wykonując następujące hello:
     
           cordova run ios
   * **W przypadku systemu Android**
     
       W `Terminal` okna Uruchom aplikację w nowym wystąpieniu emulatora, wykonując następujące hello:
     
           cordova run android
3. Można wyświetlić następujące hello w dziennikach konsoli hello:
   
        [Engagement] Agent: Session started
        [Engagement] Agent: Activity 'myPage' started
        [Engagement] Connection: Established
        [Engagement] Connection: Sent: appInfo
        [Engagement] Connection: Sent: startSession
        [Engagement] Connection: Sent: activity name='myPage'

## <a id="monitor"></a>Łączenie aplikacji z funkcją monitorowania w czasie rzeczywistym
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Włączanie powiadomień wypychanych i funkcji komunikatów w aplikacji
Usługa Mobile Engagement umożliwia toointeract z użytkownikami przy użyciu powiadomień wypychanych i komunikatów w kontekście kampanii hello w aplikacji. Ten moduł ma nazwę REACH w portalu Mobile Engagement hello.
Witaj poniższe sekcje umożliwią skonfigurowanie tooreceive Twojej aplikacji je.

### <a name="configure-push-credentials-for-mobile-engagement"></a>Konfigurowanie poświadczeń wypychania dla usługi Mobile Engagement
tooallow Mobile Engagement toosend powiadomień wypychanych w Twoim imieniu, należy mieć do niej dostęp tooyour Apple iOS certyfikatu lub klucza interfejsu API serwera GCM toogrant. 

1. Przejdź tooyour portalu Mobile Engagement. Upewnij się, pracy w aplikacji hello możemy jest używany dla tego projektu, a następnie kliknij polecenie hello **Engage** u dołu hello:
   
    ![][1]
2. Na stronie ustawień hello nastąpi przejście do portalu usługi Engagement. Kliknij hello **natywnych powiadomień wypychanych** sekcji:
   
    ![][2]
3. Skonfiguruj certyfikat systemu iOS/klucz interfejsu API serwera GCM Server
   
    **[iOS]**
   
    a. Wybierz element .p12, prześlij go i wpisz hasło:
   
    ![][3]
   
    **[Android]**
   
    a. Kliknij ikonę edycji hello przed **klucz interfejsu API** w sekcji Ustawienia GCM hello i hello wyświetlonym, Wklej klucz serwera GCM Server hello i kliknij przycisk **OK**. 
   
    ![][4]

### <a name="enable-push-notifications-in-hello-cordova-app"></a>Włączanie powiadomień wypychanych w aplikacji Cordova hello
Edytuj **www/js/index.js** tooadd hello wywołania tooMobile zaangażowania toorequest powiadomień wypychanych oraz zadeklarować mechanizm obsługi:

     onDeviceReady: function() {
           Engagement.initializeReach(  
                 // on OpenUrl  
                 function(_url) {   
                 alert(_url);   
                 });  
            Engagement.startActivity("myPage",{});  
        }

### <a name="run-hello-app"></a>Uruchamianie aplikacji hello
**[iOS]**

1. Firma Microsoft będzie Użyj XCode toobuild i wdrażania aplikacji hello na powiadomienia wypychane tootest urządzenia hello, ponieważ system iOS umożliwia tylko powiadomienia wypychane tooan rzeczywistego urządzenia. Przejdź do lokalizacji toohello, w której utworzono projekt Cordova, a następnie przejdź zbyt**...\platforms\ios** lokalizacji. Otwórz plik natywny .xcodeproj hello w środowisku XCode. 
2. Tworzenie i wdrażanie hello Cordova aplikacji toohello iOS urządzenia przy użyciu konta hello, które ma hello zawierający certyfikatów hello przekazanym właśnie toohello portalu Mobile Engagement i hello identyfikator aplikacji, który odpowiada hello co podane podczas tworzenia profilu inicjowania obsługi administracyjnej Witaj aplikacji Cordova. Można wyewidencjonować hello *identyfikator pakietu* w Twojej **zasobów\*-info.plist** plików w środowisku XCode toomatch on się. 
3. Zostanie wyświetlone menu podręczne standardowe iOS hello na urządzeniu z informacją, że aplikacja hello żądania uprawnień toosend powiadomienia. Udziel uprawnienia hello. 

**[Android]**

Ponieważ powiadomienia GCM są obsługiwane w emulatorze systemu Android hello możesz użyć aplikacji systemu Android toorun hello hello emulatora. 

    cordova run android

## <a id="send"></a>Wyślij aplikacji tooyour powiadomień
Teraz utworzymy prostą kampanię powiadomień wypychanych, która będzie wysyłać aplikacji tooyour wypychania, działającej na urządzeniu hello:

1. Przejdź toohello **osiągnąć** kartę w portalu usługi Mobile Engagement
2. Kliknij przycisk **nowy anons** toocreate kampanii wypychania
   
    ![][6]
3. Podaj dane wejściowe toocreate kampanii **[Android]**
   
   * Podaj **nazwę** kampanii. 
   * Wybierz hello **typ dostawy** jako *powiadomienie systemowe* *proste*
   * Wybierz hello **czas dostawy** jako *"Any Time"*
   * Podaj **tytuł** powiadomienia, który będzie hello pierwszy wiersz hello wypychania.
   * Podaj **komunikat** powiadomienia, który będzie służyć jako treść wiadomości powitania. 
     
     ![][11]
4. Podaj dane wejściowe toocreate kampanii **[iOS]**
   
   * Podaj **nazwę** kampanii. 
   * Wybierz hello **czas dostawy** jako *"tylko poza aplikacją"*
   * Podaj **tytuł** powiadomienia, który będzie hello pierwszy wiersz hello wypychania.
   * Podaj **komunikat** powiadomienia, który będzie służyć jako treść wiadomości powitania. 
     
     ![][12]
5. Przewiń w dół i w hello sekcji zawartości wybierz **tylko powiadomienie**
   
    ![][8]
6. [Opcjonalnie] Możesz też podać adres URL akcji. Upewnij się, że adres wykorzystuje schemat adresów URL podany podczas konfigurowania wtyczki hello **AZME\_PRZEKIEROWANIA\_adres URL** zmiennej np. *myapp://test*.  
7. Ustawienie hello najprostsze kampanii możliwe jest gotowe. Teraz przewiń ponownie w dół i kliknij przycisk hello **Utwórz** przycisk toosave kampanii.
8. Na koniec **aktywuj** swoją kampanię.
   
    ![][10]
9. W ramach kampanii na urządzeniu lub w emulatorze powinno pojawić się powiadomienie wypychane. 

## <a id="next-steps"></a>Następne kroki
[Przegląd wszystkich metod dostępnych przy użyciu zestawu Cordova Mobile Engagement SDK](https://github.com/Azure/azure-mobile-engagement-cordova)

<!-- Images. -->

[1]: ./media/mobile-engagement-cordova-get-started/engage-button.png
[2]: ./media/mobile-engagement-cordova-get-started/engagement-portal.png
[3]: ./media/mobile-engagement-cordova-get-started/native-push-settings.png
[4]: ./media/mobile-engagement-cordova-get-started/api-key.png
[6]: ./media/mobile-engagement-cordova-get-started/new-announcement.png
[8]: ./media/mobile-engagement-cordova-get-started/campaign-content.png
[10]: ./media/mobile-engagement-cordova-get-started/campaign-activate.png
[11]: ./media/mobile-engagement-cordova-get-started/campaign-first-params-android.png
[12]: ./media/mobile-engagement-cordova-get-started/campaign-first-params-ios.png

