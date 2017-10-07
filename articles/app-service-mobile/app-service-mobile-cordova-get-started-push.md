---
title: "aaaAdd tooApache powiadomień wypychanych aplikacji Cordova za pomocą usługi Azure Mobile Apps | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toosend Azure Mobile Apps toouse push aplikacji oprogramowania Apache Cordova tooyour powiadomienia."
services: app-service\mobile
documentationcenter: javascript
manager: syntaxc4
editor: 
author: ggailey777
ms.assetid: 92c596a9-875c-4840-b0e1-69198817576f
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 8e1b23d6145b446b6f01599337b677e2f2b31d7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-apache-cordova-app"></a>Dodawanie aplikacji oprogramowania Apache Cordova tooyour powiadomień wypychanych
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Omówienie
W tym samouczku można dodać projekt toohello [Apache Cordova szybki start] powiadomień wypychanych, aby powiadomienie wypychane zostanie wysłane toohello urządzenia, za każdym razem, gdy wstawieniu rekordu.

Jeśli nie używasz hello pobrany Projekt serwera szybki start, muszą hello pakiet rozszerzenia powiadomień wypychanych. Aby uzyskać więcej informacji, zobacz [pracować z serwera wewnętrznej bazy danych hello .NET SDK usługi Azure Mobile Apps][1].

## <a name="prerequisites"></a>Wymagania wstępne
Ten samouczek obejmuje aplikacji oprogramowania Apache Cordova opracowanych za pomocą programu Visual Studio 2015 uruchamianego na powitania Emulator systemu Google Android, urządzenia z systemem Android, urządzenia z systemem Windows i urządzenia z systemem iOS.

toocomplete tego samouczka należy:

* Komputer z programem [Visual Studio Community 2015] [ 2] lub nowszy.
* [Visual Studio Tools for Apache Cordova][4].
* [Aktywne konto platformy Azure][3].
* Ukończono [szybki start dla oprogramowania Apache Cordova] [ 5] projektu.
* (Android) A [konto Google] [ 6] z ze zweryfikowanym adresem e-mail.
* (iOS) [Członkostwo w programie dla deweloperów firmy Apple] [ 7] i urządzenia z systemem iOS (iOS Simulator nie obsługuje push).
* (System Windows) A [konto dewelopera w Sklepie Windows] [ 8] i urządzeń z systemem Windows 10.

## <a name="configure-hub"></a>Konfigurowanie Centrum powiadomień
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

[Obejrzyj film wideo przedstawiający kroki opisane w tej sekcji][9]

## <a name="update-hello-server-project"></a>Aktualizowanie powitania serwera projektu
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="add-push-to-app"></a>Modyfikowanie aplikacji platformy Cordova
Upewnij się, że Twój projekt aplikacji oprogramowania Apache Cordova jest gotowy toohandle powiadomienia wypychane przez Instalowanie wtyczki wypychania Cordova hello oraz wszelkich usług powiadomień wypychanych specyficzne dla platformy.

#### <a name="update-hello-cordova-version-in-your-project"></a>Zaktualizuj wersję oprogramowania Cordova hello w projekcie.
Jeśli projekt używa oprogramowania Apache Cordova w wersji starszej niż v6.1.1, zaktualizuj powitania klienta projektu. tooupdate hello projektu:

* Kliknij prawym przyciskiem myszy `config.xml` tooopen hello konfiguracji projektanta.
* Wybierz kartę platformy hello.
* Wybierz 6.1.1 hello **interfejsu Cordova CLI** pola tekstowego.
* Wybierz **kompilacji**, następnie **Kompiluj rozwiązanie** tooupdate hello projektu.

#### <a name="install-hello-push-plugin"></a>Instalowanie wtyczki wypychania hello
Aplikacji oprogramowania Apache Cordova nie obsługują natywnie możliwości urządzenia lub sieci.  Te możliwości są udostępniane przez wtyczek, które są publikowane, albo na [npm] [ 10] lub w witrynie GitHub.  Witaj `phonegap-plugin-push` wtyczka jest powiadomień wypychanych toohandle używane sieci.

Można zainstalować dodatek wypychania hello w jeden z następujących sposobów:

**Z hello wiersza polecenia:**

Wykonaj hello następujące polecenie:

    cordova plugin add phonegap-plugin-push

**Z poziomu programu Visual Studio:**

1. W Eksploratorze rozwiązań Otwórz hello `config.xml` kliknij plik **wtyczek** > **niestandardowy**, wybierz pozycję **Git** jako źródła instalacji, a następnie wprowadź `https://github.com/phonegap/phonegap-plugin-push`jako źródło hello.

   ![][img1]

2. Kliknij przycisk hello strzałkę dalej źródła instalacji toohello.
3. W **SENDER_ID**, jeśli masz już identyfikator liczbowych projektu dla projektu konsoli dla deweloperów Google hello, możesz dodać ją tutaj. W przeciwnym razie wprowadź wartość symbolu zastępczego, takich jak 777777.  Jeśli ma być przeznaczona dla systemu Android, należy zaktualizować tę wartość w pliku config.xml później.
4. Kliknij pozycję **Dodaj**.

Dodatek wypychania Hello jest zainstalowany.

#### <a name="install-hello-device-plugin"></a>Instalowanie wtyczki urządzenia hello
Wykonaj hello sama procedura stosowana tooinstall hello wypychania wtyczki.  Dodaj wtyczkę urządzenia hello z listy wtyczek Core hello (kliknij **wtyczek** > **Core** toofind go). Należy to nazwa wtyczki tooobtain hello platformy.

#### <a name="register-your-device-on-application-start-up"></a>Zarejestruj urządzenie przy uruchamianiu aplikacji
Początkowo przeprowadzamy minimalnego kodu dla systemu Android. Później należy zmodyfikować hello toorun aplikacji dla systemu iOS lub Windows 10.

1. Dodaj wywołanie za**registerForPushNotifications** podczas wywołania zwrotnego hello, proces logowania hello lub u dołu hello hello **onDeviceReady** metody:

        // Login toohello service.
        client.login('google')
            .then(function () {
                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh hello todoItems
                refreshDisplay();

                // Wire up hello UI Event Handler for hello Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                    // Added tooregister for push notifications.
                registerForPushNotifications();

            }, handleError);

    Ten przykład przedstawia wywoływanie **registerForPushNotifications** po pomyślnym uwierzytelnieniu.  Możesz wywołać `registerForPushNotifications()` tyle razy, ile jest wymagana.

2. Dodaj nowy hello **registerForPushNotifications** metody w następujący sposób:

        // Register for Push Notifications. Requires that phonegap-plugin-push be installed.
        var pushRegistration = null;
        function registerForPushNotifications() {
          pushRegistration = PushNotification.init({
              android: { senderID: 'Your_Project_ID' },
              ios: { alert: 'true', badge: 'true', sound: 'true' },
              wns: {}
          });

        // Handle hello registration event.
        pushRegistration.on('registration', function (data) {
          // Get hello native platform of hello device.
          var platform = device.platform;
          // Get hello handle returned during registration.
          var handle = data.registrationId;
          // Set hello device-specific message template.
          if (platform == 'android' || platform == 'Android') {
              // Register for GCM notifications.
              client.push.register('gcm', handle, {
                  mytemplate: { body: { data: { message: "{$(messageParam)}" } } }
              });
          } else if (device.platform === 'iOS') {
              // Register for notifications.
              client.push.register('apns', handle, {
                  mytemplate: { body: { aps: { alert: "{$(messageParam)}" } } }
              });
          } else if (device.platform === 'windows') {
              // Register for WNS notifications.
              client.push.register('wns', handle, {
                  myTemplate: {
                      body: '<toast><visual><binding template="ToastText01"><text id="1">$(messageParam)</text></binding></visual></toast>',
                      headers: { 'X-WNS-Type': 'wns/toast' } }
              });
          }
        });

        pushRegistration.on('notification', function (data, d2) {
          alert('Push Received: ' + data.message);
        });

        pushRegistration.on('error', handleError);
        }
3. (Android) W hello poprzedzających kodu, Zastąp `Your_Project_ID` liczbowym hello identyfikator projektu dla aplikacji z [konsoli dla deweloperów Google][18].

## <a name="optional-configure-and-run-hello-app-on-android"></a>(Opcjonalnie) Konfigurowanie i uruchamianie aplikacji hello w systemie Android
Ukończenie tego powiadomienia wypychane tooenable sekcji dla systemu Android.

#### <a name="enable-gcm"></a>Włącz Firebase Cloud Messaging
Ponieważ firma Microsoft przeznaczonych hello platformy systemu Google Android początkowo, należy włączyć Firebase Cloud Messaging.

[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

#### <a name="configure-backend"></a>Konfigurowanie przy użyciu FCM hello aplikacji mobilnej zaplecza toosend wypychania żądań
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

#### <a name="configure-your-cordova-app-for-android"></a>Konfigurowanie aplikacji platformy Cordova dla systemu Android
W aplikacji platformy Cordova, otwórz plik config.xml i Zastąp `Your_Project_ID` liczbowym hello identyfikator projektu dla aplikacji z hello [konsoli dla deweloperów Google][18].

        <plugin name="phonegap-plugin-push" version="1.7.1" src="https://github.com/phonegap/phonegap-plugin-push.git">
            <variable name="SENDER_ID" value="Your_Project_ID" />
        </plugin>

Otwórz index.js i zaktualizuj toouse kodu hello swój identyfikator projektu liczbowych.

        pushRegistration = PushNotification.init({
            android: { senderID: 'Your_Project_ID' },
            ios: { alert: 'true', badge: 'true', sound: 'true' },
            wns: {}
        });

#### <a name="configure-device"></a>Konfigurowanie urządzenia z systemem Android do debugowania USB
Przed wdrożeniem programu tooyour aplikacji urządzenia z systemem Android należy tooenable debugowanie USB.  Na telefonie z systemem Android, wykonaj następujące czynności:

1. Przejdź za**ustawienia** > **informacje o telefonie**, naciśnij przycisk hello **numer kompilacji** dopóki (około siedem razy) jest włączony tryb dewelopera.
2. W **ustawienia** > **opcje dewelopera** włączyć **debugowanie USB**, a następnie połącz programowania tooyour telefonów z systemem Android komputera za pomocą kabla USB.

Firma Microsoft przetestowane to przy użyciu węzła Google 5 X urządzeniu z systemem Android 6.0 (Marshmallow).  Jednak techniki hello są często używane przez wszystkie nowoczesne wersji dla systemu Android.

#### <a name="install-google-play-services"></a>Zainstaluj usługi Google Play
Dodatek wypychania Hello zależy od systemu Android usług Google Play dla powiadomień wypychanych.

1. W programie Visual Studio, kliknij przycisk **narzędzia** > **Android** > **Android SDK Manager**, rozwiń węzeł hello **dodatki** folder i wyboru hello pole toomake się, że każdy z następujących zestawów SDK hello jest zainstalowany.

   * Android 2.3 lub nowszej
   * Poprawki repozytorium Google 27 lub nowszej
   * Usług Google Play 9.0.2 lub nowszej

2. Kliknij przycisk **instalowania pakietów** i poczekaj, aż hello toocomplete instalacji.

Witaj bieżącego wymagane biblioteki są wymienione w hello [phonegap wtyczka wypychana instalacja dokumentacji][19].

#### <a name="test-push-notifications-in-hello-app-on-android"></a>Testowych powiadomień wypychanych w aplikacji hello w systemie Android
Możesz teraz hello testowych powiadomień wypychanych, uruchamiając aplikację i wstawianie elementów w tabeli TodoItem hello. Można przetestować z hello tego samego urządzenia lub z drugiego urządzenia, tak długo, jak używasz hello sam wewnętrznej bazy danych. Testowanie aplikacji Cordova na platformie Android hello w jednym z hello następujące sposoby:

* **Na urządzeniu fizycznym:** dołączyć komputer programowanie tooyour urządzenia z systemem Android za pomocą kabla USB.  Zamiast **Emulator systemu Google Android**, wybierz pozycję **urządzenia**. Visual Studio wdroży urządzenia toohello aplikacji hello, a następnie uruchomi aplikacji hello.  Następnie zakłócają aplikacji hello na urządzeniu hello.

  Udoskonalić programowanie.  Takie jak udostępnianie aplikacji ekranu [Mobizen] [ 20] mogą pomóc w tworzeniu aplikacji systemu Android.  Mobizen projekcję przeglądarce sieci web tooa Android ekranu na komputerze.

* **Na emulatorze systemu Android:** są dodatkowe czynności konfiguracyjne wymagane podczas uruchamiania emulatora.

    Upewnij się, że wdrażasz tooa urządzenia wirtualnego, który ma ustawić jako cel hello interfejsy API Google, jak pokazano w hello Android Virtual Device (AVD) manager.

    ![](./media/app-service-mobile-cordova-get-started-push/google-apis-avd-settings.png)

    Jeśli chcesz toouse szybsze x86 emulatora, możesz [zainstalować sterownik HAXM hello] [ 11] i skonfigurować hello emulatora toouse go.

    Dodanie urządzenia Android toohello konto Google, klikając **aplikacje** > **ustawienia** > **Dodaj konto**, następnie postępuj zgodnie z monitami hello.

    ![](./media/app-service-mobile-cordova-get-started-push/add-google-account.png)

    Uruchamianie aplikacji todolist hello jako przed i Wstaw nowe zadanie do wykonania. Teraz, w obszarze powiadomień hello jest wyświetlana ikona powiadomienia. Można także otworzyć hello powiadomień szuflady tooview hello pełny tekst hello powiadomień.

    ![](./media/app-service-mobile-cordova-get-started-push/android-notifications.png)

## <a name="optional-configure-and-run-on-ios"></a>(Opcjonalnie) Konfigurowanie i uruchamianie w systemie iOS
Ta sekcja dotyczy uruchamiania projektu oprogramowania Cordova hello na urządzeniach z systemem iOS. Jeśli nie pracujesz z urządzeniami z systemem iOS, możesz pominąć tę sekcję.

#### <a name="install-and-run-hello-ios-remote-build-agent-on-a-mac-or-cloud-service"></a>Zainstaluj i uruchom hello zdalnego systemu iOS agenta kompilacji w usłudze Mac lub w chmurze
Przed uruchomieniem aplikacji Cordova w systemie iOS przy użyciu programu Visual Studio, wykonanie kroków hello w hello [iOS przewodnik konfiguracji] [ 12] tooinstall i hello wykonywania zdalnego agenta kompilacji.

Upewnij się, że można tworzyć hello aplikacji dla systemu iOS. Witaj kroki opisane w przewodniku instalacji hello są wymagane toobuild dla systemu iOS w programie Visual Studio. Jeśli nie masz Mac, można tworzyć dla systemu iOS w usłudze, takich jak MacInCloud przy użyciu hello zdalnego agenta kompilacji. Aby uzyskać więcej informacji, zobacz [uruchamianie aplikacji systemu iOS w chmurze hello][21].

> [!NOTE]
> XCode 7 lub nowszy jest wymagany toouse hello wypychania dodatku w systemie iOS.

#### <a name="find-hello-id-toouse-as-your-app-id"></a>Znajdź hello identyfikator toouse jako Identyfikatora aplikacji
Zanim zarejestrujesz aplikację dla powiadomień wypychanych, otwórz plik config.xml w aplikacji platformy Cordova, Znajdź hello `id` wartość w elemencie widget hello atrybutu i skopiować go do późniejszego użycia. Identyfikator hello w hello po XML, jest `io.cordova.myapp7777777`.

        <widget defaultlocale="en-US" id="io.cordova.myapp7777777"
          version="1.0.0" windows-packageVersion="1.1.0.0" xmlns="http://www.w3.org/ns/widgets"
            xmlns:cdv="http://cordova.apache.org/ns/1.0" xmlns:vs="http://schemas.microsoft.com/appx/2014/htmlapps">

Później za pomocą tego identyfikatora po utworzeniu Identyfikatora aplikacji w portalu dla deweloperów firmy Apple. Jeśli tworzysz inny identyfikator aplikacji w portalu dla deweloperów hello, należy wykonać kilka dodatkowych czynności w dalszej części tego samouczka. Identyfikator Hello w elemencie widget musi odpowiadać hello identyfikator aplikacji na powitania portalu dla deweloperów.

#### <a name="register-hello-app-for-push-notifications-on-apples-developer-portal"></a>Rejestrowanie aplikacji hello powiadomień wypychanych na portalu dla deweloperów firmy Apple
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

[Obejrzyj wideo przedstawiające podobne kroki](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-5-Set-up-apns-for-push)

#### <a name="configure-azure-toosend-push-notifications"></a>Konfigurowanie powiadomień wypychanych Azure toosend
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

#### <a name="verify-that-your-app-id-matches-your-cordova-app"></a>Sprawdź, czy identyfikator aplikacji zgodna aplikacji platformy Cordova
Jeśli już utworzony na Twoim koncie deweloperów firmy Apple identyfikator aplikacji hello odpowiada identyfikator hello elementu widget hello w pliku config.xml, możesz pominąć ten krok. Witaj identyfikatory nie są zgodne, wykonaj następujące kroki hello:

1. Usuń folder platform hello z projektu.
2. Usuń folder wtyczek hello z projektu.
3. Usuń hello node_modules folder z projektu.
4. Aktualizacja atrybutu id hello elementu widget hello w pliku config.xml toouse hello utworzonego w ramach Twojego konta dewelopera Apple Identyfikatora aplikacji.
5. Ponownie skompiluj projekt.

##### <a name="test-push-notifications-in-your-ios-app"></a>Testowych powiadomień wypychanych w aplikacji systemu iOS
1. W programie Visual Studio, upewnij się, że **iOS** został wybrany jako cel wdrożenia hello, a następnie wybierz pozycję **urządzenia** toorun na urządzeniu z systemem iOS połączonych.

    Można uruchamiać na tooyour podłączone urządzenie z systemem iOS komputera za pomocą programu iTunes. Witaj symulatora systemu iOS nie obsługuje powiadomień wypychanych.

2. Naciśnij klawisz hello **Uruchom** przycisk lub **F5** w Visual Studio toobuild hello projektu i rozpocząć hello aplikacji na urządzeniu z systemem iOS, a następnie kliknij **OK** tooaccept powiadomień wypychanych.

   > [!NOTE]
   > Aplikacja Hello zażąda potwierdzenia dla powiadomień wypychanych podczas pierwszego uruchomienia hello.

3. W aplikacji hello typu zadania, a następnie kliknij przycisk hello plus (+) ikona.
4. Sprawdź, czy powiadomienie odebraniu, a następnie kliknij przycisk OK toodismiss hello powiadomień.

## <a name="optional-configure-and-run-on-windows"></a>(Opcjonalnie) Konfigurowanie i uruchamianie w systemie Windows
Ta sekcja dotyczy uruchamiania projektu aplikacji oprogramowania Apache Cordova hello na urządzeniach z systemem Windows 10 (dodatek wypychania PhoneGap hello jest obsługiwana w systemie Windows 10). Jeśli nie pracujesz z urządzeniami z systemem Windows, możesz pominąć tę sekcję.

#### <a name="register-your-windows-app-for-push-notifications-with-wns"></a>Rejestrowanie aplikacji systemu Windows dla powiadomień wypychanych z usługą WNS
Opcje magazynu hello toouse w programie Visual Studio, wybierz element docelowy z systemem Windows z listy platformy rozwiązania hello, tak samo, jak **Windows x64** lub **Windows x86** (uniknąć **Windows AnyCPU** Aby powiadomienia wypychane).

[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

[Obejrzyj film wideo przedstawiający podobne kroki][13]

#### <a name="configure-hello-notification-hub-for-wns"></a>Konfigurowanie Centrum powiadomień hello przypadku usługi WNS
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="configure-your-cordova-app-toosupport-windows-push-notifications"></a>Konfigurowanie powiadomień wypychanych systemu Windows toosupport aplikacji Cordova
Hello Otwórz projektanta konfiguracji (kliknij prawym przyciskiem myszy na plik config.xml i wybierz **Widok projektanta**) wybierz pozycję hello **Windows** , a następnie wybierz **systemu Windows 10** w obszarze **Windows docelowa wersja**.

powiadomienia wypychane toosupport w domyślnej (debugowanie) tworzy build.json otwartych plików. Skopiuj "wersja" Konfiguracja tooyour debugowania.

        "windows": {
            "release": {
                "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
                "publisherId": "CN=yourpublisherID"
            }
        }

Po zaktualizowaniu hello hello build.json powinna zawierać hello następującego kodu:

    "windows": {
        "release": {
            "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
            "publisherId": "CN=yourpublisherID"
            },
        "debug": {
            "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
            "publisherId": "CN=yourpublisherID"
            }
        }

Tworzenie aplikacji hello i sprawdź, czy użytkownik nie ma błędów. Twoja aplikacja kliencka powinna teraz rejestrować hello powiadomień z zaplecza aplikacji mobilnej hello. W tej sekcji należy powtórzyć dla każdego projektu systemu Windows w rozwiązaniu.

#### <a name="test-push-notifications-in-your-windows-app"></a>Testowych powiadomień wypychanych w aplikacji systemu Windows
W programie Visual Studio, upewnij się, że platforma systemu Windows jest wybrany jako cel wdrożenia hello, takich jak **Windows x64** lub **Windows x86**. Aplikacja hello toorun na komputerach z systemem Windows 10 hosting Visual Studio, wybierz **komputera lokalnego**.

Naciśnij klawisz hello uruchomienia projektu hello toobuild przycisk i uruchomić aplikacji hello.

W aplikacji hello, wpisz nazwę nowego zadania do wykonania, a następnie kliknij przycisk hello plus (+) tooadd ikonę go.

Sprawdź, czy otrzyma powiadomienie po dodaniu elementu hello.

## <a name="next-steps"></a>Następne kroki
* Przeczytaj informacje o [usługi Notification Hubs] [ 17] toolearn o powiadomień wypychanych.
* Jeśli jeszcze nie Kontynuuj samouczek hello przez [Dodawanie uwierzytelniania] [ 14] tooyour aplikacji oprogramowania Apache Cordova.

Dowiedz się, jak toouse hello zestawów SDK.

* [Zestaw Apache Cordova SDK][15]
* [Zestaw ASP.NET Server SDK][1]
* [Zestaw node.js Server SDK][16]

<!-- Images -->
[img1]: ./media/app-service-mobile-cordova-get-started-push/add-push-plugin.png

<!-- URLs -->
[1]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[2]: http://www.visualstudio.com/
[3]: https://azure.microsoft.com/pricing/free-trial/
[4]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx
[5]: app-service-mobile-cordova-get-started.md
[6]: http://go.microsoft.com/fwlink/p/?LinkId=268302
[7]: https://developer.apple.com/programs/
[8]: https://developer.microsoft.com/en-us/store/register
[9]: https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-3-Create-azure-notification-hub
[10]: https://www.npmjs.com/
[11]: https://taco.visualstudio.com/en-us/docs/run-app-apache/#HAXM
[12]: http://taco.visualstudio.com/en-us/docs/ios-guide/
[13]: https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-6-Set-up-wns-for-push
[14]: app-service-mobile-cordova-get-started-users.md
[15]: app-service-mobile-cordova-how-to-use-client-library.md
[16]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[17]: ../notification-hubs/notification-hubs-push-notification-overview.md
[18]: https://console.developers.google.com/home/dashboard
[19]: https://github.com/phonegap/phonegap-plugin-push/blob/master/docs/INSTALLATION.md
[20]: https://www.mobizen.com/
[21]: http://taco.visualstudio.com/en-us/docs/build_ios_cloud/
