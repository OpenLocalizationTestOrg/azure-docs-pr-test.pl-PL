---
title: "aaaGet wprowadzenie do usługi Azure Notification Hubs przy użyciu usługi Baidu | Dokumentacja firmy Microsoft"
description: "Z tego samouczka, dowiesz się, jak toouse usługi Azure Notification Hubs toopush powiadomienia tooAndroid urządzeń przy użyciu usługi Baidu."
services: notification-hubs
documentationcenter: android
author: ysxu
manager: erikre
editor: 
ms.assetid: 23bde1ea-f978-43b2-9eeb-bfd7b9edc4c1
ms.service: notification-hubs
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: mobile-baidu
ms.workload: mobile
ms.date: 08/19/2016
ms.author: yuaxu
ms.openlocfilehash: 2767fdd3bb04674e7a531634237cc05cd8c21cb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-using-baidu"></a>Rozpoczynanie pracy z usługą Azure Notification Hubs przy użyciu usługi Baidu
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Omówienie
Wypychane w chmurze Baidu to chińska usługa w chmurze czy można używać urządzeń toomobile powiadomień wypychanych toosend. Ta usługa jest przydatna w Chinach, gdzie dostarczanie powiadomień wypychanych tooAndroid jest złożony z powodu obecności hello różnych sklepów z aplikacjami i wypychania usług, oprócz toohello dostępności urządzeń z systemem Android, które nie są zazwyczaj połączone tooGCM (Google Cloud Messaging).

## <a name="prerequisites"></a>Wymagania wstępne
Dla tego samouczka wymagane są następujące elementy:

* Zestaw SDK systemu android (założono, że używane jest środowisko Eclipse), który można pobrać z hello <a href="http://go.microsoft.com/fwlink/?LinkId=389797">witryny systemu Android</a>
* [Zestaw SDK usługi Mobile Services dla systemu Android]
* [Baidu Push zestawu SDK systemu Android]

> [!NOTE]
> toocomplete tego samouczka, musi mieć aktywne konto platformy Azure. Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-baidu-get-started%2F).
> 
> 

## <a name="create-a-baidu-account"></a>Tworzenia konta usługi Baidu
toouse Baidu, musisz mieć konto Baidu. Jeśli masz już konto, zaloguj się za toohello [portalu Baidu] i pominąć toohello następnego kroku. W przeciwnym razie zobacz następujące instrukcje na temat hello toocreate konta usługi Baidu.  

1. Przejdź toohello [portalu Baidu] i kliknij przycisk hello**登录**(**logowania**) łącza. Kliknij przycisk**立即注册**procesu rejestracji konta hello toostart.
   
   ![][1]
2. Wprowadź szczegóły hello wymagane — phone/poczta e-mail adres, hasło i kod weryfikacyjny — i kliknij przycisk **Signup**.
   
   ![][2]
3. Powoduje wysłanie adresu e-mail toohello e-mail wprowadzony z tooactivate łącze konta usługi Baidu.
   
   ![][3]
4. Zaloguj się za tooyour konto e-mail, Otwórz wiadomość hello Baidu i kliknij tooactivate link aktywacji hello konta usługi Baidu.
   
   ![][4]

Po aktywowaniu konta usługi Baidu Zaloguj toohello [portalu Baidu].

## <a name="register-as-a-baidu-developer"></a>Rejestrowanie się jako deweloper usługi Baidu
1. Po zalogowaniu toohello [portalu Baidu], kliknij przycisk**更多 >>** (**więcej**).
   
      ![][5]
2. Przewiń w dół w hello**站长与开发者服务 (Webmaster i usług deweloperskich)** sekcji, a następnie kliknij przycisk**百度开放云平台**(**Baidu otwartej platformy chmury**).
   
      ![][6]
3. Na następnej stronie powitania kliknij**开发者服务**(**usług deweloperskich**) na powitania prawym górnym rogu.
   
      ![][7]
4. Na następnej stronie powitania kliknij**注册开发者**(**zarejestrowany deweloperzy**) z menu hello na powitania prawym górnym rogu.
   
      ![][8]
5. Wprowadź imię i nazwisko, opis oraz numer telefonu komórkowego do odebrania weryfikacyjnej wiadomości tekstowej, a następnie kliknij pozycję **送验证码** (**Wyślij kod weryfikacyjny**). Międzynarodowych numerów telefonów należy tooenclose numer kierunkowy kraju hello w nawiasach. Na przykład numer dla Stanów Zjednoczonych ma postać **(1)1234567890**.
   
      ![][9]
6. Otrzymasz wiadomość SMS zawierającą numer weryfikacyjny, jak pokazano w hello poniższy przykład:
   
      ![][10]
7. Wprowadź numer weryfikacyjny hello z wiadomość hello w**验证码**(**kod potwierdzenia**).
8. Na koniec Ukończ hello developer rejestracja akceptowania hello Baidu umowę, a następnie klikając polecenie**提交**(**przesyłania**). Zostanie wyświetlony hello następujące strony w pomyślnym ukończeniu rejestracji:
   
      ![][11]

## <a name="create-a-baidu-cloud-push-project"></a>Tworzenie projektu powiadomień wypychanych w chmurze Baidu
Podczas tworzenia projektu powiadomień wypychanych w chmurze Baidu otrzymasz identyfikator aplikacji, klucz interfejsu API i klucz tajny.

1. Po zalogowaniu toohello [portalu Baidu], kliknij przycisk**更多 >>** (**więcej**).
   
      ![][5]
2. Przewiń w dół w hello**站长与开发者服务**(**Webmaster i usług deweloperskich**) i kliknij pozycję**百度开放云平台**(**Baidu otwartej platformy chmury**).
   
      ![][6]
3. Na następnej stronie powitania kliknij**开发者服务**(**usług deweloperskich**) na powitania prawym górnym rogu.
   
      ![][7]
4. Na następnej stronie powitania kliknij**云推送**(**Cloud Push**) z hello**云服务**(**usługi w chmurze**) sekcji.
   
      ![][12]
5. Gdy jesteś deweloperem zarejestrowany, zostanie wyświetlony**管理控制台**(**konsoli zarządzania**) w menu u góry hello. Kliknij pozycję **开发者服务管理** (**Zarządzanie usługami dla deweloperów**).
   
      ![][13]
6. Na następnej stronie powitania kliknij**创建工程**(**tworzenia projektu**).
   
      ![][14]
7. Wprowadź nazwę aplikacji, a następnie kliknij pozycję **创建** (**Utwórz**).
   
      ![][15]
8. Po pomyślnym utworzeniu projektu powiadomień wypychanych w chmurze Baidu zostanie wyświetlona strona zawierająca następujące dane: **AppID** (Identyfikator aplikacji), **API Key** (Klucz interfejsu API) i **Secret Key** (Klucz tajny). Zanotuj klucz interfejsu API hello i klucz tajny, który zostanie wykorzystany później.
   
      ![][16]
9. Konfigurowanie hello projektu powiadomień wypychanych, klikając**云推送**(**wypychane w chmurze**) w okienku po lewej stronie powitania.
   
      ![][31]
10. Na następnej stronie powitania kliknij hello**推送设置**(**Push ustawienia**) przycisku.
    
    ![][32]  
11. Na stronie konfiguracji hello Dodaj hello nazwy pakietu, który będzie używany w projekcie systemu Android w hello**应用包名**(**pakiet aplikacji**) do pola, a następnie kliknij przycisk**保存设置**() **Zapisać**).  
    
    ![][33]

Zobacz hello**保存成功!** (**Zapisano pomyślnie!**).

## <a name="configure-your-notification-hub"></a>Konfigurowanie centrum powiadomień
1. Zaloguj się toohello [klasycznego portalu Azure], a następnie kliknij przycisk **+ nowy** u dołu ekranu hello hello.
2. Kliknij pozycję **App Services**, pozycję **Service Bus** i pozycję **Centrum powiadomień**, a następnie kliknij pozycję **Szybkie tworzenie**.
3. Podaj nazwę użytkownika **Centrum powiadomień**, wybierz pozycję hello **Region** i hello **Namespace** gdzie zostanie utworzone Centrum powiadomień, a następnie kliknij  **Tworzenie nowego centrum powiadomień**.  
   
      ![][17]
4. Kliknij przestrzeń nazw hello, w której utworzono Centrum powiadomień, a następnie kliknij przycisk **usługi Notification Hubs** u góry hello.
   
      ![][18]
5. Centrum powiadomień hello wybierz utworzony, a następnie kliknij przycisk **Konfigurowanie** z górnego menu hello.
   
      ![][19]
6. Przewiń w dół toohello **ustawienia powiadomień baidu** i wprowadź klucz hello interfejsu API i klucz tajny uzyskany z konsoli Baidu hello wcześniej dla projektu wypychania w chmurze Baidu. Kliknij pozycję **Zapisz**.
   
      ![][20]
7. Kliknij przycisk hello **pulpitu nawigacyjnego** u góry hello hello Centrum powiadomień, a następnie kliknij pozycję **Wyświetl parametry połączenia**.
   
      ![][21]
8. Zanotuj hello **DefaultListenSharedAccessSignature** i **DefaultFullSharedAccessSignature** z hello **dostęp do informacji o połączeniu** okna.
   
    ![][22]

## <a name="connect-your-app-toohello-notification-hub"></a>Łączenie aplikacji toohello Centrum powiadomień
1. W środowisku Eclipse ADT utwórz nowy projekt dla systemu Android: **File** > **New** > **Android Application Project** (Plik — Nowy — Projekt aplikacji dla systemu Android).
   
    ![][23]
2. Wprowadź **Nazwa aplikacji** i upewnij się, że hello **SDK wymagane Minimum** wersja jest ustawiana za**API 16: Android 4.1**.
   
    ![][24]
3. Kliknij przycisk **dalej** i kontynuować hello kreatora po do hello **tworzenie działania** zostanie wyświetlone okno. Upewnij się, że **puste działanie** jest wybrany, a następnie wybierz przycisk **Zakończ** toocreate nową aplikację systemu Android.
   
    ![][25]
4. Upewnij się, że hello **docelowym kompilacji projektu** została poprawnie ustawiona.
   
    ![][26]
5. Pobierz plik notification-hubs-0.4.jar hello z hello **pliki** kartę hello [Notification-Hubs-Android-SDK w serwisie Bintray](https://bintray.com/microsoftazuremobile/SDK/Notification-Hubs-Android-SDK/0.4). Dodaj hello pliku toohello **libs** folderu projektu Eclipse i Odśwież hello *biblioteki* folderu.
6. Pobierz i Rozpakuj hello [Baidu Push zestawu SDK systemu Android], otwórz hello **libs** folder, a następnie hello kopiowania **pushservice-x.y.z** jar plików i hello **armeabi**  &  **mips** folderów w hello **biblioteki** folderu aplikacji systemu Android.
7. Otwórz hello **AndroidManifest.xml** dla systemu android projektu i dodać hello uprawnienia, które są wymagane przez hello zestaw SDK usługi Baidu.
   
        <uses-permission android:name="android.permission.INTERNET" />
        <uses-permission android:name="android.permission.READ_PHONE_STATE" />
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.WRITE_SETTINGS" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
        <uses-permission android:name="android.permission.DISABLE_KEYGUARD" />
        <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
        <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
        <uses-permission android:name="android.permission.ACCESS_DOWNLOAD_MANAGER" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION" />
8. Dodaj hello **android: name** tooyour właściwości **aplikacji** element **AndroidManifest.xml**, zastępując *yourprojectname* (dla przykład **com.przyklad.baidutest**). Upewnij się, że ta nazwa projektu jest zgodna hello jedną skonfigurowaną w konsoli Baidu hello.
   
        <application android:name="yourprojectname.DemoApplication"
9. Dodaj powitania po konfiguracji w elemencie aplikacji hello po hello **. MainActivity** elementu działania, zastępując *yourprojectname* (na przykład **com.przyklad.baidutest**):
   
        <receiver android:name="yourprojectname.MyPushMessageReceiver">
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.MESSAGE" />
                <action android:name="com.baidu.android.pushservice.action.RECEIVE" />
                <action android:name="com.baidu.android.pushservice.action.notification.CLICK" />
            </intent-filter>
        </receiver>
   
        <receiver android:name="com.baidu.android.pushservice.PushServiceReceiver"
            android:process=":bdservice_v1">
            <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED" />
                <action android:name="android.net.conn.CONNECTIVITY_CHANGE" />
                <action android:name="com.baidu.android.pushservice.action.notification.SHOW" />
            </intent-filter>
        </receiver>
   
        <receiver android:name="com.baidu.android.pushservice.RegistrationReceiver"
            android:process=":bdservice_v1">
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.METHOD" />
                <action android:name="com.baidu.android.pushservice.action.BIND_SYNC" />
            </intent-filter>
            <intent-filter>
                <action android:name="android.intent.action.PACKAGE_REMOVED"/>
                <data android:scheme="package" />
            </intent-filter>
        </receiver>
   
        <service
            android:name="com.baidu.android.pushservice.PushService"
            android:exported="true"
            android:process=":bdservice_v1"  >
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.PUSH_SERVICE" />
            </intent-filter>
        </service>
10. Dodaj nową klasę o nazwie **ConfigurationSettings.java** toohello projektu.
    
     ![][28]
    
     ![][29]
11. Dodaj powitania po tooit kodu:
    
        public class ConfigurationSettings {
                public static String API_KEY = "...";
                public static String NotificationHubName = "...";
                public static String NotificationHubConnectionString = "...";
            }
    
    Ustaw wartość hello **API_KEY** o co został z projektu w chmurze Baidu hello wcześniej pobrany, **NotificationHubName** z nazwą Centrum powiadomień z hello klasycznego portalu Azure i  **NotificationHubConnectionString** wartość defaultlistensharedaccesssignature z hello klasycznego portalu Azure.
12. Dodaj nową klasę o nazwie **DemoApplication.java**i Dodaj powitania po tooit kodu:
    
        import com.baidu.frontia.FrontiaApplication;
    
        public class DemoApplication extends FrontiaApplication {
            @Override
            public void onCreate() {
                super.onCreate();
            }
        }
13. Dodaj nową klasę o nazwie **MyPushMessageReceiver.java**i Dodaj powitania po tooit kodu. Jest klasą hello, który uchwytów hello powiadomienia wypychane, które są odbierane z serwera powiadomień wypychanych Baidu hello.
    
        import java.util.List;
        import android.content.Context;
        import android.os.AsyncTask;
        import android.util.Log;
        import com.baidu.frontia.api.FrontiaPushMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub;
    
        public class MyPushMessageReceiver extends FrontiaPushMessageReceiver {
            /** TAG tooLog */
            public static NotificationHub hub = null;
            public static String mChannelId, mUserId;
            public static final String TAG = MyPushMessageReceiver.class
                    .getSimpleName();
    
            @Override
            public void onBind(Context context, int errorCode, String appid,
                    String userId, String channelId, String requestId) {
                String responseString = "onBind errorCode=" + errorCode + " appid="
                        + appid + " userId=" + userId + " channelId=" + channelId
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
                mChannelId = channelId;
                mUserId = userId;
    
                try {
                    if (hub == null) {
                        hub = new NotificationHub(
                                ConfigurationSettings.NotificationHubName,
                                ConfigurationSettings.NotificationHubConnectionString,
                                context);
                        Log.i(TAG, "Notification hub initialized");
                    }
                } catch (Exception e) {
                   Log.e(TAG, e.getMessage());
                }
    
                registerWithNotificationHubs();
            }
    
            private void registerWithNotificationHubs() {
               new AsyncTask<Void, Void, Void>() {
                  @Override
                  protected Void doInBackground(Void... params) {
                     try {
                         hub.registerBaidu(mUserId, mChannelId);
                         Log.i(TAG, "Registered with Notification Hub - '"
                                 + ConfigurationSettings.NotificationHubName + "'"
                                 + " with UserId - '"
                                 + mUserId + "' and Channel Id - '"
                                 + mChannelId + "'");
                     } catch (Exception e) {
                         Log.e(TAG, e.getMessage());
                     }
                     return null;
                 }
               }.execute(null, null, null);
            }
    
            @Override
            public void onSetTags(Context context, int errorCode,
                    List<String> sucessTags, List<String> failTags, String requestId) {
                String responseString = "onSetTags errorCode=" + errorCode
                        + " sucessTags=" + sucessTags + " failTags=" + failTags
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onDelTags(Context context, int errorCode,
                    List<String> sucessTags, List<String> failTags, String requestId) {
                String responseString = "onDelTags errorCode=" + errorCode
                        + " sucessTags=" + sucessTags + " failTags=" + failTags
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onListTags(Context context, int errorCode, List<String> tags,
                    String requestId) {
                String responseString = "onListTags errorCode=" + errorCode + " tags="
                        + tags;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onUnbind(Context context, int errorCode, String requestId) {
                String responseString = "onUnbind errorCode=" + errorCode
                        + " requestId = " + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onNotificationClicked(Context context, String title,
                    String description, String customContentString) {
                String notifyString = "title=\"" + title + "\" description=\""
                        + description + "\" customContent=" + customContentString;
                Log.d(TAG, notifyString);
            }
    
            @Override
            public void onMessage(Context context, String message,
                    String customContentString) {
                String messageString = "message=\"" + message + "\" customContentString=" + customContentString;
                Log.d(TAG, messageString);
            }
        }
14. Otwórz **MainActivity.java**i dodaj następujące toohello hello **onCreate** metody:
    
            PushManager.startWork(getApplicationContext(),
                    PushConstants.LOGIN_TYPE_API_KEY, ConfigurationSettings.API_KEY);
15. Otwórz następujące instrukcje import u góry hello hello:
    
            import com.baidu.android.pushservice.PushConstants;
            import com.baidu.android.pushservice.PushManager;

## <a name="send-notifications-tooyour-app"></a>Wyślij powiadomienia tooyour aplikacji
Możesz szybko przetestować odbieranie powiadomień w aplikacji, wysyłając powiadomienia w hello [portalu Azure](https://portal.azure.com/) przy użyciu hello **wysyłania** znajdującego się na powitania Centrum powiadomień, jak pokazano w po ekranie powitania:

![](./media/notification-hubs-baidu-get-started/notification-hub-test-send-baidu.png)

Powiadomienia wypychane są zwykle wysyłane za pośrednictwem usługi zaplecza, takiej jak Mobile Services czy ASP.NET, z użyciem zgodnej biblioteki. Jeśli biblioteka nie jest dostępna dla Twojej zaplecza, można użyć interfejsu API REST hello bezpośrednio toosend komunikaty powiadomień.

W tym samouczku będziemy Zachowaj prostotę i przedstawiono testowanie aplikacji klienckiej przez wysyłanie powiadomień dotyczących usługi notification hubs w aplikacji konsoli usługi zaplecza przy użyciu hello zestawu .NET SDK. Firma Microsoft zaleca hello [toousers powiadomienia toopush użyciu usługi Notification Hubs](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) samouczka jako hello następnego kroku do wysyłania powiadomień z zaplecza ASP.NET. Jednak po podejścia hello może służyć do wysyłania powiadomień:

* **Interfejs REST**: powiadomienia mogą być obsługiwane na dowolnej platformie zaplecza za pomocą hello [interfejsu REST](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).
* **Microsoft Azure powiadomień koncentratory .NET SDK**: W hello Menedżera pakietów Nuget dla programu Visual Studio, uruchom [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).
* **Node.js**: [jak toouse centra powiadomień w oprogramowaniu Node.js](notification-hubs-nodejs-push-notification-tutorial.md).
* **Aplikacje mobilne**: na przykład jak toosend powiadomień z zaplecza Azure App Service Mobile Apps, który jest zintegrowany z usługą Notification Hubs, zobacz [aplikacji mobilnej tooyour powiadomień wypychanych Dodaj](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).
* **Java / PHP**: przykład sposobu toosend powiadomienia za pomocą hello interfejsów API REST, zobacz "jak toouse usługi Notification Hubs za pomocą języka Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).

## <a name="optional-send-notifications-from-a-net-console-app"></a>(Opcjonalnie) Wysyłanie powiadomień z poziomu aplikacji konsolowej .NET
W tej sekcji przedstawiono sposób wysyłania powiadomienia za pomocą aplikacji konsolowej .NET.

1. Utwórz nową aplikację konsoli języka Visual C#:
   
    ![][30]
2. W oknie konsoli Menedżera pakietów hello, ustaw hello **domyślny projekt** tooyour nowy projekt aplikacji konsoli, a następnie w oknie konsoli hello, wykonaj następujące polecenie hello:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    Ta instrukcja dodaje toohello odwołanie do zestawu SDK usługi Azure Notification Hubs za pomocą hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pakietu Microsoft.Azure.Notification Hubs NuGet</a>.
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
3. Witaj Otwórz plik **Program.cs** i dodaj następujące hello instrukcję using:
   
        using Microsoft.Azure.NotificationHubs;
4. W Twojej `Program` klasy, Dodaj następujące metody hello i Zastąp *DefaultFullSharedAccessSignatureSASConnectionString* i *NotificationHubName* z wartościami hello.
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("DefaultFullSharedAccessSignatureSASConnectionString", "NotificationHubName");
            string message = "{\"title\":\"((Notification title))\",\"description\":\"Hello from Azure\"}";
            var result = await hub.SendBaiduNativeNotificationAsync(message);
        }
5. Dodaj hello następujące wiersze w Twojej **Main** metody:
   
         SendNotificationAsync();
         Console.ReadLine();

## <a name="test-your-app"></a>Testowanie aplikacji
tootest połączyć tę aplikację przy użyciu rzeczywistego telefonu, po prostu hello phone tooyour komputera za pomocą kabla USB. Ta akcja spowoduje załadowanie aplikacji na telefon hello dołączony.

tootest tę aplikację w emulatorze hello na powitania Eclipse górnym pasku narzędzi, kliknij przycisk **Uruchom**, a następnie wybierz aplikację: uruchamia hello emulatora, obciążenia, i działa hello aplikacji.

Aplikacja Hello pobiera hello "userId" i "channelId" z hello usługi powiadomień wypychanych Baidu i rejestruje hello Centrum powiadomień.

toosend powiadomienie testowe, można użyć karty debugowania hello hello klasycznego portalu Azure. Jeśli utworzono hello aplikacji konsoli .NET dla programu Visual Studio, wystarczy nacisnąć klawisz F5 hello w aplikacji hello toorun programu Visual Studio. Aplikacja Hello wysyła powiadomienie, które pojawia się w hello górnym obszarze powiadomień urządzenia lub emulatora.

<!-- Images. -->
[1]: ./media/notification-hubs-baidu-get-started/BaiduRegistration.png
[2]: ./media/notification-hubs-baidu-get-started/BaiduRegistrationInput.png
[3]: ./media/notification-hubs-baidu-get-started/BaiduConfirmation.png
[4]: ./media/notification-hubs-baidu-get-started/BaiduActivationEmail.png
[5]: ./media/notification-hubs-baidu-get-started/BaiduRegistrationMore.png
[6]: ./media/notification-hubs-baidu-get-started/BaiduOpenCloudPlatform.png
[7]: ./media/notification-hubs-baidu-get-started/BaiduDeveloperServices.png
[8]: ./media/notification-hubs-baidu-get-started/BaiduDeveloperRegistration.png
[9]: ./media/notification-hubs-baidu-get-started/BaiduDevRegistrationInput.png
[10]: ./media/notification-hubs-baidu-get-started/BaiduDevRegistrationConfirmation.png
[11]: ./media/notification-hubs-baidu-get-started/BaiduDevConfirmationFinal.png
[12]: ./media/notification-hubs-baidu-get-started/BaiduCloudPush.png
[13]: ./media/notification-hubs-baidu-get-started/BaiduDevSvcMgmt.png
[14]: ./media/notification-hubs-baidu-get-started/BaiduCreateProject.png
[15]: ./media/notification-hubs-baidu-get-started/BaiduCreateProjectInput.png
[16]: ./media/notification-hubs-baidu-get-started/BaiduProjectKeys.png
[17]: ./media/notification-hubs-baidu-get-started/AzureNHCreation.png
[18]: ./media/notification-hubs-baidu-get-started/NotificationHubs.png
[19]: ./media/notification-hubs-baidu-get-started/NotificationHubsConfigure.png
[20]: ./media/notification-hubs-baidu-get-started/NotificationHubBaiduConfigure.png
[21]: ./media/notification-hubs-baidu-get-started/NotificationHubsConnectionStringView.png
[22]: ./media/notification-hubs-baidu-get-started/NotificationHubsConnectionString.png
[23]: ./media/notification-hubs-baidu-get-started/EclipseNewProject.png
[24]: ./media/notification-hubs-baidu-get-started/EclipseProjectCreation.png
[25]: ./media/notification-hubs-baidu-get-started/EclipseBlankActivity.png
[26]: ./media/notification-hubs-baidu-get-started/EclipseProjectBuildProperty.png
[27]: ./media/notification-hubs-baidu-get-started/EclipseBaiduReferences.png
[28]: ./media/notification-hubs-baidu-get-started/EclipseNewClass.png
[29]: ./media/notification-hubs-baidu-get-started/EclipseConfigSettingsClass.png
[30]: ./media/notification-hubs-baidu-get-started/ConsoleProject.png
[31]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig1.png
[32]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig2.png
[33]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig3.png

<!-- URLs. -->
[Zestaw SDK usługi Mobile Services dla systemu Android]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[Baidu Push zestawu SDK systemu Android]: http://developer.baidu.com/wiki/index.php?title=docs/cplat/push/sdk/clientsdk
[klasycznego portalu Azure]: https://manage.windowsazure.com/
[portalu Baidu]: http://www.baidu.com/
