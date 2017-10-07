---
title: "aaaSend wypychania powiadomień tooChrome aplikacji za pomocą usługi Azure Notification Hubs | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toosend usługi Azure Notification Hubs toouse push tooa powiadomień aplikacji dla programu Chrome."
services: notification-hubs
keywords: "powiadomienia wypychane na urządzeniach przenośnych, powiadomienia wypychane, powiadomienie wypychane, powiadomienia wypychane w przeglądarce chrome"
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 75d4ff59-d04a-455f-bd44-0130a68e641f
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-chrome
ms.devlang: JavaScript
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 7dec8ab02622563bc3730a2e96820da8932d22f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="send-push-notifications-toochrome-apps-with-azure-notification-hubs"></a>Wyślij powiadomienia tooChrome aplikacji za pomocą usługi Azure Notification Hubs wypychania
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

W tym temacie pokazano, jak toosend usługi Azure Notification Hubs toouse push tooa powiadomień aplikacji dla programu Chrome, który będzie wyświetlany w kontekście hello hello przeglądarki Google Chrome. W tym samouczku utworzymy aplikację dla programu Chrome, która odbiera powiadomienia wypychane za pomocą usługi [Google Cloud Messaging (GCM)](https://developers.google.com/cloud-messaging/). 

> [!NOTE]
> toocomplete tego samouczka, musi mieć aktywne konto platformy Azure. Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%notification-hubs-chrome-get-started%2F).
> 
> 

Witaj samouczek przeprowadzi Cię przez te powiadomienia wypychane tooenable podstawowe kroki:

* [Włączanie usługi Google Cloud Messaging](#register)
* [Konfigurowanie centrum powiadomień](#configure-hub)
* [Połącz toohello Centrum powiadomień aplikacji dla programu Chrome](#connect-app)
* [Wyślij tooyour powiadomień wypychanych aplikacji dla programu Chrome](#send)
* [Dodatkowe funkcje i możliwości](#next-steps)

> [!NOTE]
> Powiadomienia wypychane aplikacji dla programu Chrome nie są ogólne powiadomienia w przeglądarce — są to modelu rozszerzeń przeglądarki określonych toohello (zobacz [Chrome Apps omówienie] szczegółowe informacje). Ponadto toohello przeglądarkę dla komputerów, aplikacji dla programu Chrome Uruchom na urządzeń przenośnych (Android i iOS) przy użyciu oprogramowania Apache Cordova. Zobacz [Chrome Apps on Mobile] toolearn więcej.
> 
> 

Konfigurowanie usługi GCM i Azure Notification Hubs jest identyczne tooconfiguring dla systemu Android, ponieważ [Google Cloud Messaging dla programu Chrome] jest przestarzała i hello sama usługa GCM obsługuje teraz urządzenia z systemem Android i wystąpienia programu Chrome.

## <a id="register"></a>Włączanie usługi Google Cloud Messaging
1. Przejdź toohello [Google Cloud Console] witryny sieci Web, zaloguj się przy użyciu poświadczeń konta Google, a następnie kliknij przycisk hello **tworzenia projektu** przycisku. Wprowadź odpowiednią **Nazwa projektu**, a następnie kliknij przycisk hello **Utwórz** przycisku.
   
       ![Google Cloud Console - Create Project][1]
2. Zanotuj hello **numer projektu** na powitania **projekty** strony dla hello projektu, który został właśnie utworzony. Zostanie ona użyta jako hello **identyfikator nadawcy usługi GCM** w hello tooregister aplikacji dla programu Chrome z usługą GCM.
   
       ![Google Cloud Console - Project Number][2]
3. W okienku po lewej stronie powitania kliknij **APIs & auth**, następnie przewiń w dół i kliknij przycisk tooenable Przełącz hello **Google Cloud Messaging dla systemu Android**. Nie masz tooenable **Google Cloud Messaging dla programu Chrome**.
   
       ![Google Cloud Console - Server Key][3]
4. W okienku po lewej stronie powitania kliknij **poświadczenia** > **Utwórz nowy klucz** > **klucz serwera** > **Utwórz**.
   
       ![Google Cloud Console - Credentials][4]
5. Zwróć uwagę na powitania serwera **klucz interfejsu API**. Spowoduje to skonfigurować w dalej powiadomień tooenable w Centrum go tooGCM powiadomień wypychanych toosend.
   
       ![Google Cloud Console - API Key][5]

## <a id="configure-hub"></a>Konfigurowanie centrum powiadomień
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

&emsp;&emsp;6.   W hello **ustawienia** bloku, wybierz opcję **usługi powiadomień** , a następnie **Google (GCM)**. Wprowadź klucz interfejsu API hello i Zapisz.

&emsp;&emsp;![Azure Notification Hubs — Google (GCM)](./media/notification-hubs-android-get-started/notification-hubs-gcm-api.png)

## <a id="connect-app"></a>Połącz toohello Centrum powiadomień aplikacji dla programu Chrome
Centrum powiadomień jest teraz skonfigurowany toowork z usługą GCM i masz hello połączenie ciągów tooregister Twojego tooboth aplikacji odbierania i wysyłania powiadomień wypychanych. LK

### <a name="create-a-new-chrome-app"></a>Tworzenie nowej aplikacji dla programu Chrome
Poniższy przykład Hello jest oparty na powitania [przykładu usługi GCM aplikacji Chrome] i używa hello zalecany sposób toocreate aplikacji dla programu Chrome. Wyróżnione hello czynności związanych szczególnie tooAzure usługi Notification Hubs. 

> [!NOTE]
> Zaleca się pobrać hello źródła dla aplikacji dla programu Chrome z [przykładu Centrum powiadomień aplikacji dla programu Chrome].
> 
> 

Hello aplikacji dla programu Chrome została utworzona przy użyciu języka JavaScript i można użyć dowolnego edytora tekstu jej utworzenia. Poniżej przedstawiono wygląd tworzonej aplikacji dla programu Chrome.

![Aplikacja dla programu Google Chrome][15]

1. Utwórz folder i nadaj mu nazwę `ChromePushApp`. Oczywiście nazwa hello jest dowolnego — Jeśli nazwy inny, upewnij się, że zastępuje ścieżki hello hello wymaganych segmentach kodu.
2. Pobierz hello [bibliotekę crypto-js] w folderze hello utworzonego w drugim kroku hello. Ten folder biblioteki będzie zawierać dwa podfoldery: `components` i `rollups`.
3. Utwórz plik `manifest.json`. Wszystkie aplikacje Chrome bazują na plik manifestu zawierający metadane aplikacji hello i większość co ważniejsze, wszystkie uprawnienia przyznane toohello aplikacji po jej zainstalowaniu przez użytkownika hello.
   
        {
          "name": "NH-GCM Notifications",
          "description": "Chrome platform app.",
          "manifest_version": 2,
          "version": "0.1",
          "app": {
            "background": {
              "scripts": ["background.js"]
            }
          },
          "permissions": ["gcm", "storage", "notifications", "https://*.servicebus.windows.net/*"],
          "icons": { "128": "gcm_128.png" }
        }
   
    Powiadomienie hello `permissions` element, który określa, że aplikacji dla programu Chrome będzie możliwe tooreceive powiadomienia wypychane z usługi GCM. Należy także określić hello URI centra powiadomień Azure gdzie hello aplikacji dla programu Chrome będzie tooregister wywołania REST.
    Nasza Przykładowa aplikacja używa również pliku ikony `gcm_128.png`, znajdziesz w źródle hello, pochodzącym z oryginalnego przykładu usługi GCM hello. Można zastąpić go dowolnym obrazem spełniającym hello [kryteria ikony](https://developer.chrome.com/apps/manifest/icons).
4. Utwórz plik o nazwie `background.js` z hello następującego kodu:
   
        // Returns a new notification ID used in hello notification.
        function getNotificationId() {
          var id = Math.floor(Math.random() * 9007199254740992) + 1;
          return id.toString();
        }
   
        function messageReceived(message) {
          // A message is an object with a data property that
          // consists of key-value pairs.
   
          // Concatenate all key-value pairs tooform a display string.
          var messageString = "";
          for (var key in message.data) {
            if (messageString != "")
              messageString += ", "
            messageString += key + ":" + message.data[key];
          }
          console.log("Message received: " + messageString);
   
          // Pop up a notification tooshow hello GCM message.
          chrome.notifications.create(getNotificationId(), {
            title: 'GCM Message',
            iconUrl: 'gcm_128.png',
            type: 'basic',
            message: messageString
          }, function() {});
        }
   
        var registerWindowCreated = false;
   
        function firstTimeRegistration() {
          chrome.storage.local.get("registered", function(result) {
   
            registerWindowCreated = true;
            chrome.app.window.create(
              "register.html",
              {  width: 520,
                 height: 500,
                 frame: 'chrome'
              },
              function(appWin) {}
            );
          });
        }
   
        // Set up a listener for GCM message event.
        chrome.gcm.onMessage.addListener(messageReceived);
   
        // Set up listeners tootrigger hello first-time registration.
        chrome.runtime.onInstalled.addListener(firstTimeRegistration);
        chrome.runtime.onStartup.addListener(firstTimeRegistration);
   
    To jest plik hello, który powoduje wyświetlenie okna przeglądarki Chrome aplikacji hello HTML (**register.html**), a także definiuje obsługi hello **messageReceived** toohandle hello przychodzących powiadomień wypychanych.
5. Utwórz plik o nazwie `register.html` — definiuje hello UI hello aplikacji dla programu Chrome. 
   
   > [!NOTE]
   > W tym przykładzie użyto biblioteki **CryptoJS w wersji 3.1.2**. Jeśli pobrano inną wersję biblioteki hello, upewnij się, że prawidłowo zastąpiono wersję hello w hello `src` ścieżki.
   > 
   > 
   
        <html>
   
        <head>
        <title>GCM Registration</title>
        <script src="register.js"></script>
        <script src="CryptoJS v3.1.2/rollups/hmac-sha256.js"></script>
        <script src="CryptoJS v3.1.2/components/enc-base64-min.js"></script>
        </head>
   
        <body>
   
        Sender ID:<br/><input id="senderId" type="TEXT" size="20"><br/>
        <button id="registerWithGCM">Register with GCM</button>
        <br/>
        <br/>
        <br/>
   
        Notification Hub Name:<br/><input id="hubName" type="TEXT" style="width:400px"><br/><br/>
        Connection String:<br/><textarea id="connectionString" type="TEXT" style="width:400px;height:60px"></textarea>
   
        <br/>
   
        <button id="registerWithNH" disabled="true">Register with Azure Notification Hubs</button>
   
        <br/>
        <br/>
   
        <textarea id="console" type="TEXT" readonly style="width:500px;height:200px;background-color:#e5e5e5;padding:5px"></textarea>
   
        </body>
   
        </html>
6. Utwórz plik o nazwie `register.js` hello kod poniżej. Ten plik zawiera skrypt hello za `register.html`. Chrome Apps nie jest dozwolone wykonywanie śródwierszowe, więc masz toocreate oddzielny skrypt pomocniczy dla interfejsu użytkownika.
   
        var registrationId = "";
        var hubName        = "", connectionString = "";
        var originalUri    = "", targetUri = "", endpoint = "", sasKeyName = "", sasKeyValue = "", sasToken = "";
   
        window.onload = function() {
           document.getElementById("registerWithGCM").onclick = registerWithGCM;  
           document.getElementById("registerWithNH").onclick = registerWithNH;
           updateLog("You have not registered yet. Please provider sender ID and register with GCM and then with  Notification Hubs.");
        }
   
        function updateLog(status) {
          currentStatus = document.getElementById("console").innerHTML;
          if (currentStatus != "") {
            currentStatus = currentStatus + "\n\n";
          }
   
          document.getElementById("console").innerHTML = currentStatus  + status;
        }
   
        function registerWithGCM() {
          var senderId = document.getElementById("senderId").value.trim();
          chrome.gcm.register([senderId], registerCallback);
   
          // Prevent register button from being clicked again before hello registration finishes.
          document.getElementById("registerWithGCM").disabled = true;
        }
   
        function registerCallback(regId) {
          registrationId = regId;
          document.getElementById("registerWithGCM").disabled = false;
   
          if (chrome.runtime.lastError) {
            // When hello registration fails, handle hello error and retry the
            // registration later.
            updateLog("Registration failed: " + chrome.runtime.lastError.message);
            return;
          }
   
          updateLog("Registration with GCM succeeded.");
          document.getElementById("registerWithNH").disabled = false;
   
          // Mark that hello first-time registration is done.
          chrome.storage.local.set({registered: true});
        }
   
        function registerWithNH() {
          hubName = document.getElementById("hubName").value.trim();
          connectionString = document.getElementById("connectionString").value.trim();
          splitConnectionString();
          generateSaSToken();
          sendNHRegistrationRequest();
        }
   
        // From http://msdn.microsoft.com/library/dn495627.aspx
        function splitConnectionString()
        {
          var parts = connectionString.split(';');
          if (parts.length != 3)
          throw "Error parsing connection string";
   
          parts.forEach(function(part) {
            if (part.indexOf('Endpoint') == 0) {
            endpoint = 'https' + part.substring(11);
            } else if (part.indexOf('SharedAccessKeyName') == 0) {
            sasKeyName = part.substring(20);
            } else if (part.indexOf('SharedAccessKey') == 0) {
            sasKeyValue = part.substring(16);
            }
          });
   
          originalUri = endpoint + hubName;
        }
   
        function generateSaSToken()
        {
          targetUri = encodeURIComponent(originalUri.toLowerCase()).toLowerCase();
          var expiresInMins = 10; // 10 minute expiration
   
          // Set expiration in seconds.
          var expireOnDate = new Date();
          expireOnDate.setMinutes(expireOnDate.getMinutes() + expiresInMins);
          var expires = Date.UTC(expireOnDate.getUTCFullYear(), expireOnDate
            .getUTCMonth(), expireOnDate.getUTCDate(), expireOnDate
            .getUTCHours(), expireOnDate.getUTCMinutes(), expireOnDate
            .getUTCSeconds()) / 1000;
          var tosign = targetUri + '\n' + expires;
   
          // Using CryptoJS.
          var signature = CryptoJS.HmacSHA256(tosign, sasKeyValue);
          var base64signature = signature.toString(CryptoJS.enc.Base64);
          var base64UriEncoded = encodeURIComponent(base64signature);
   
          // Construct authorization string.
          sasToken = "SharedAccessSignature sr=" + targetUri + "&sig="
                          + base64UriEncoded + "&se=" + expires + "&skn=" + sasKeyName;
        }
   
        function sendNHRegistrationRequest()
        {
          var registrationPayload =
          "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
          "<entry xmlns=\"http://www.w3.org/2005/Atom\">" +
              "<content type=\"application/xml\">" +
                  "<GcmRegistrationDescription xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/netservices/2010/10/servicebus/connect\">" +
                      "<GcmRegistrationId>{GCMRegistrationId}</GcmRegistrationId>" +
                  "</GcmRegistrationDescription>" +
              "</content>" +
          "</entry>";
   
          // Update hello payload with hello registration ID obtained earlier.
          registrationPayload = registrationPayload.replace("{GCMRegistrationId}", registrationId);
   
          var url = originalUri + "/registrations/?api-version=2014-09";
          var client = new XMLHttpRequest();
   
          client.onload = function () {
            if (client.readyState == 4) {
              if (client.status == 200) {
                updateLog("Notification Hub Registration succesful!");
                updateLog(client.responseText);
              } else {
                updateLog("Notification Hub Registration did not succeed!");
                updateLog("HTTP Status: " + client.status + " : " + client.statusText);
                updateLog("HTTP Response: " + "\n" + client.responseText);
              }
            }
          };
   
          client.onerror = function () {
                updateLog("ERROR - Notification Hub Registration did not succeed!");
          }
   
          client.open("POST", url, true);
          client.setRequestHeader("Content-Type", "application/atom+xml;type=entry;charset=utf-8");
          client.setRequestHeader("Authorization", sasToken);
          client.setRequestHeader("x-ms-version", "2014-09");
   
          try {
              client.send(registrationPayload);
          }
          catch(err) {
              updateLog(err.message);
          }
        }
   
    Witaj powyżej skryptu ma hello następujących parametrów klucza:
   
   * **window.onLoad** definiuje zdarzenia kliknięcia przycisków hello hello dwóch przycisków na powitania interfejsu użytkownika. Jeden służy z usługą GCM i hello innych używa hello Identyfikatora rejestracji zwróconego po rejestracji w usłudze GCM tooregister przy użyciu usługi Azure Notification Hubs.
   * **updateLog** to funkcja hello, która pozwala nam toohandle prostych funkcji logowania.
   * **registerWithGCM** jest hello pierwszy obsługi kliknięcia przycisku, dzięki czemu hello `chrome.gcm.register` wywołania tooGCM tooregister hello bieżącego aplikacji dla programu Chrome wystąpienia.
   * **registerCallback** jest hello funkcja wywołania zwrotnego, która jest wywoływana po zwraca hello wywołanie rejestracji usługi GCM.
   * **registerWithNH** jest hello drugi obsługi kliknięcia przycisku, który służy do rejestrowania przy użyciu usługi Notification Hubs. Pobiera `hubName` i `connectionString` (hello użytkownika, który został określony) i rzemieślniczych hello wywołania API REST rejestracji centra powiadomień.
   * **splitConnectionString** i **generateSaSToken** są pomocnikami reprezentującymi implementację JavaScript hello procesu tworzenia tokenu SaS, który musi być używany w wszystkie wywołania interfejsu API REST. Aby uzyskać więcej informacji, zobacz temat [Common Concepts](http://msdn.microsoft.com/library/dn495627.aspx) (Wspólne pojęcia).
   * **sendNHRegistrationRequest** jest wywołania funkcji hello, która sprawia, że REST protokołu HTTP tooAzure Notification Hubs.
   * **registrationPayload** definiuje ładunek XML rejestracji hello. Aby uzyskać więcej informacji, zobacz temat [Create Registration NH REST API] (Interfejs API REST rejestracji w usłudze Notification Hubs). Możemy zaktualizować hello w nim identyfikator rejestracji otrzymany z usługi GCM.
   * **Klient** jest wystąpieniem **XMLHttpRequest** używanym hello toomake wysłanie żądania POST protokołu HTTP. Należy pamiętać, że aktualizujemy hello `Authorization` nagłówek z `sasToken`. Pomyślne wykonanie tego wywołania spowoduje zarejestrowanie tego wystąpienia aplikacji dla programu Chrome w usłudze Azure Notification Hubs.

Witaj ogólna struktura folderów dla tego projektu powinna wyglądać następująco: ![aplikacji w programie Google Chrome — struktura folderów][21]

### <a name="set-up-and-test-your-chrome-app"></a>Instalowanie i testowanie aplikacji dla programu Chrome
1. Otwórz przeglądarkę Chrome. Otwórz **stronę Rozszerzenia programu Chrome** i włącz **Tryb programisty**.
   
       ![Google Chrome - Enable Developer Mode][16]
2. Kliknij przycisk **Wczytaj rozszerzenie** i przejdź do folderu toohello, w którym utworzono pliki hello. Możesz również użyć hello **Chrome Apps & Extensions Developer Tool**. To narzędzie jest aplikacji dla programu Chrome w sobie (instalowaną ze sklepu Chrome Web Store hello) i zapewnia zaawansowane możliwości debugowania dla programowania aplikacji dla programu Chrome.
   
       ![Google Chrome - Load Unpacked Extension][17]
3. Jeśli hello aplikacji dla programu Chrome została utworzona bez żadnych błędów, zostanie wyświetlona w aplikacji dla programu Chrome widoczne.
   
       ![Google Chrome - Chrome App Display][18]
4. Wprowadź hello **numer projektu** którą uzyskano wcześniej z hello **Google Cloud Console** jako identyfikator nadawcy hello, a następnie kliknij przycisk **rejestracji w usłudze GCM**. Musi zostać wyświetlony wiadomość hello **rejestracji w usłudze GCM zakończyło się pomyślnie.**
   
       ![Google Chrome - Chrome App Customization][19]
5. Wprowadź użytkownika **nazwę Centrum powiadomień** i hello **DefaultListenSharedAccessSignature** uzyskaną wcześniej hello portalu, a następnie kliknij przycisk **zarejestrować w usłudze Azure Notification Hubs**. Musi zostać wyświetlony wiadomość hello **pomyślnej rejestracji Centrum powiadomień!** i identyfikator hello szczegóły hello rejestracji odpowiedzi, która zawiera hello rejestracji usługi Azure Notification Hubs.
   
       ![Google Chrome - Specify Notification Hub Details][20]  

## <a name="send"></a>Wyślij powiadomienie tooyour aplikacji dla programu Chrome
W celach testowych wyślemy powiadomienia wypychane programu Chrome przy użyciu aplikacji konsolowej programu .NET. 

> [!NOTE]
> Powiadomienia wypychane można wysyłać przy użyciu usługi Notification Hubs z poziomu dowolnego zaplecza za pośrednictwem naszego publicznego <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">interfejsu REST</a>. Odwiedź nasz [portal dokumentacji](https://azure.microsoft.com/documentation/services/notification-hubs/), aby uzyskać więcej przykładów dla różnych platform.
> 
> 

1. W programie Visual Studio z hello **pliku** menu, wybierz opcję **nowy** , a następnie **projektu**. W obszarze **Visual C#** kliknij pozycję **Windows**, kliknij pozycję **Aplikacja konsolowa**, a następnie kliknij przycisk **OK**.  Spowoduje to utworzenie nowego projektu aplikacji konsolowej.
2. Z hello **narzędzia** menu, kliknij przycisk **Menedżer pakietów biblioteki** , a następnie **Konsola Menedżera pakietów**. Spowoduje to wyświetlenie konsoli Menedżera pakietów hello.
3. W oknie konsoli hello wykonaj następujące polecenie hello:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
       This adds a reference toohello Azure Service Bus SDK with hello <a href="http://nuget.org/packages/  WindowsAzure.ServiceBus/">WindowsAzure.ServiceBus NuGet package</a>.
4. Otwórz `Program.cs` i dodaj następujące hello `using` instrukcji:
   
        using Microsoft.Azure.NotificationHubs;
5. W hello `Program` klasy, Dodaj hello następujące metody:
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            String message = "{\"data\":{\"message\":\"Hello Chrome from Azure Notification Hubs\"}}";
            await hub.SendGcmNativeNotificationAsync(message);
        }
   
       Make sure tooreplace hello `<hub name>` placeholder with hello name of hello notification hub that appears in hello [portal](https://portal.azure.com) in your Notification Hub blade. Also, replace hello connection string placeholder with hello connection string called `DefaultFullSharedAccessSignature` that you obtained in hello notification hub configuration section.
   
   > [!NOTE]
   > Upewnij się, że użyto parametrów połączenia hello z **pełne** dostępu nie **nasłuchiwania** dostępu. Witaj **nasłuchiwania** dostępu ciąg połączenia nie powoduje przyznania uprawnień toosend powiadomień wypychanych.
   > 
   > 
6. Dodaj następujące hello odwołuje się hello `Main` metody:
   
         SendNotificationAsync();
         Console.ReadLine();
7. Upewnij się, że program Chrome jest uruchomiony, a następnie uruchom aplikację konsolową hello.
8. Powinny pojawić się następujące hello powiadomienia wyskakującego okienka na pulpicie.
   
       ![Google Chrome - Notification][13]
9. Możesz też sprawdzić wszystkie powiadomienia przy użyciu okna powiadomień programu Chrome hello hello zadań (w systemie Windows) gdy program Chrome jest uruchomiony.
   
       ![Google Chrome - Notifications List][14]

> [!NOTE]
> Nie trzeba toohave hello aplikacji dla programu Chrome uruchomione lub Otwórz w przeglądarce hello (chociaż hello przeglądarka Chrome musi być uruchomiona). W oknie przeglądarki Chrome powiadomienia hello umożliwia również wyświetlenie skonsolidowanego widoku wszystkich powiadomień.
> 
> 

## <a name="next-steps"> </a>Następne kroki
Dowiedz się więcej o usłudze Notification Hubs w temacie [Notification Hubs Overview] (Notification Hubs — omówienie).

tootarget określonych użytkowników, zobacz toohello [Azure Notification Hubs Powiadom użytkowników] samouczka. 

Jeśli chcesz toosegment użytkowników na grupy zainteresowań, możesz wykonać hello [usługi Azure Notification Hubs fundamentalne wiadomości] samouczka.

<!-- Images. -->
[1]: ./media/notification-hubs-chrome-get-started/GoogleConsoleCreateProject.PNG
[2]: ./media/notification-hubs-chrome-get-started/GoogleProjectNumber.png
[3]: ./media/notification-hubs-chrome-get-started/EnableGCM.png
[4]: ./media/notification-hubs-chrome-get-started/CreateServerKey.png
[5]: ./media/notification-hubs-chrome-get-started/ServerKey.png
[6]: ./media/notification-hubs-chrome-get-started/CreateNH.png
[7]: ./media/notification-hubs-chrome-get-started/NHNamespace.png
[8]: ./media/notification-hubs-chrome-get-started/NamespaceConfigure.png
[9]: ./media/notification-hubs-chrome-get-started/NHConfigure.png
[10]: ./media/notification-hubs-chrome-get-started/NHConfigureGCM.png
[11]: ./media/notification-hubs-chrome-get-started/NHDashboard.png
[12]: ./media/notification-hubs-chrome-get-started/NHConnString.png
[13]: ./media/notification-hubs-chrome-get-started/ChromeNotification.png
[14]: ./media/notification-hubs-chrome-get-started/ChromeNotificationWindow.png
[15]: ./media/notification-hubs-chrome-get-started/ChromeApp.png
[16]: ./media/notification-hubs-chrome-get-started/ChromeExtensions.png
[17]: ./media/notification-hubs-chrome-get-started/ChromeLoadExtension.png
[18]: ./media/notification-hubs-chrome-get-started/ChromeAppLoaded.png
[19]: ./media/notification-hubs-chrome-get-started/ChromeAppGCM.png
[20]: ./media/notification-hubs-chrome-get-started/ChromeAppNH.png
[21]: ./media/notification-hubs-chrome-get-started/FinalFolderView.png

<!-- URLs. -->
[przykładu Centrum powiadomień aplikacji dla programu Chrome]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToChromeApps
[Google Cloud Console]: http://cloud.google.com/console
[Azure Classic Portal]: https://manage.windowsazure.com/
[Notification Hubs Overview]: notification-hubs-push-notification-overview.md (Notification Hubs — omówienie)
[Chrome Apps omówienie]: https://developer.chrome.com/apps/about_apps (Omówienie aplikacji dla programu Chrome)
[przykładu usługi GCM aplikacji Chrome]: https://github.com/GoogleChrome/chrome-app-samples/tree/master/samples/gcm-notifications
[Installable Web Apps]: https://developers.google.com/chrome/apps/docs/
[Chrome Apps on Mobile]: https://developer.chrome.com/apps/chrome_apps_on_mobile (Aplikacja dla programu Chrome na urządzeniach przenośnych)
[Create Registration NH REST API]: http://msdn.microsoft.com/library/azure/dn223265.aspx (Interfejs API REST tworzenia rejestracji w usłudze Notification Hubs)
[bibliotekę crypto-js]: http://code.google.com/p/crypto-js/
[GCM with Chrome Apps]: https://developer.chrome.com/apps/cloudMessaging
[Google Cloud Messaging dla programu Chrome]: https://developer.chrome.com/apps/cloudMessagingV1
[Azure Notification Hubs Powiadom użytkowników]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md (Powiadamianie użytkowników przy użyciu usługi Azure Notification Hubs)
[usługi Azure Notification Hubs fundamentalne wiadomości]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md (Powiadamianie o najważniejszych wiadomościach przy użyciu usługi Azure Notification Hubs)
