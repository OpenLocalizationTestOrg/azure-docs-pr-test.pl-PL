---
title: "Rozpoczynanie pracy z usługą Azure Notification Hubs przy użyciu usługi Baidu | Microsoft Docs"
description: "Korzystając z tego samouczka, dowiesz się, jak za pomocą usługi Azure Notification Hubs wysyłać powiadomienia wypychane do urządzeń z systemem Android przy użyciu usługi Baidu."
services: notification-hubs
documentationcenter: android
author: kpiteira
manager: erikre
editor: 
ms.assetid: 23bde1ea-f978-43b2-9eeb-bfd7b9edc4c1
ms.service: notification-hubs
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: mobile-baidu
ms.workload: mobile
ms.date: 08/29/2017
ms.author: kapiteir
ms.openlocfilehash: 91f20a6e0ff6c2dd512879e9ab3c9369dab5d8ff
ms.sourcegitcommit: 5735491874429ba19607f5f81cd4823e4d8c8206
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/16/2017
---
# <a name="get-started-with-notification-hubs-using-baidu"></a>Rozpoczynanie pracy z usługą Azure Notification Hubs przy użyciu usługi Baidu
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

Powiadomienia wypychane w chmurze Baidu to chińska usługa w chmurze służąca do wysyłania powiadomień wypychanych do urządzeń przenośnych. 

Ponieważ usługa Google Play i rozwiązanie FCM (Firebase Cloud Messaging) nie są dostępne w Chinach, konieczne jest korzystanie z innych sklepów z aplikacjami oraz usług wypychania. Jedną z nich jest usługa Baidu, obecnie używana przez usługę Notification Hubs.

## <a name="prerequisites"></a>Wymagania wstępne
Dla tego samouczka wymagane są następujące elementy:

* Zestaw Android SDK (założono, że jest używany program Android Studio), który można pobrać z <a href="http://go.microsoft.com/fwlink/?LinkId=389797">witryny systemu Android</a>
* [zestaw Android SDK dla powiadomień push w usłudze Baidu]

> [!NOTE]
> Do wykonania kroków tego samouczka potrzebne jest aktywne konto platformy Azure. Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-baidu-get-started%2F).
> 
> 

## <a name="create-a-baidu-account"></a>Tworzenia konta usługi Baidu
Aby korzystać z usługi Baidu, musisz mieć konto Baidu. Jeśli masz już konto, zaloguj się do [portalu Baidu] i przejdź do następnego kroku. W przeciwnym razie zapoznaj się z poniższymi instrukcjami dotyczącymi sposobu tworzenia konta usługi Baidu.  

1. Przejdź do [portalu Baidu] i kliknij link **登录** (**Zaloguj się**). Kliknij pozycję **立即注册** (**Zarejestruj się**), aby rozpocząć proces rejestracji konta.
   
    ![Rejestracja w usłudze Baidu](./media/notification-hubs-baidu-get-started/BaiduRegistration.png)

2. Wprowadź wymagane szczegóły (telefon lub adres e-mail, hasło i kod weryfikacyjny), a następnie kliknij przycisk 注册 (**Zarejestruj się**).
   
    ![Dane wprowadzane podczas rejestracji w usłudze Baidu](./media/notification-hubs-baidu-get-started/BaiduRegistrationInput.png)

3. Na podany adres e-mail zostanie wysłana wiadomość e-mail zawierająca link umożliwiający aktywację konta usługi Baidu.
   
    ![Potwierdzenie rejestracji w usłudze Baidu](./media/notification-hubs-baidu-get-started/BaiduConfirmation.png)

4. Zaloguj się do konta e-mail, otwórz aktywacyjną wiadomość e-mail usługi Baidu, a następnie kliknij link aktywacyjny, aby aktywować konto usługi Baidu.
   
    ![Wiadomość e-mail dotycząca aktywacji usługi Baidu](./media/notification-hubs-baidu-get-started/BaiduActivationEmail.png)

Po aktywowaniu konta usługi Baidu zaloguj się do [portalu Baidu].

## <a name="create-a-baidu-cloud-push-project"></a>Tworzenie projektu powiadomień wypychanych w chmurze Baidu
Podczas tworzenia projektu powiadomień wypychanych w chmurze Baidu otrzymasz identyfikator aplikacji, klucz interfejsu API i klucz tajny.

1. Po zalogowaniu się do [portalu Baidu] kliknij pozycję **更多>>** (**więcej**).
   
    ![Rejestracja — więcej opcji](./media/notification-hubs-baidu-get-started/BaiduRegistrationMore.png)

2. Przewiń w dół w sekcji **站长与开发者服务** (**Usługi dla webmasterów i deweloperów**) i kliknij pozycję **百度云推送** (**Usługa Baidu Cloud Push**).
   
    ![Otwarta platforma chmury Baidu](./media/notification-hubs-baidu-get-started/BaiduOpenCloudPlatform.png)

3. Na następnej stronie kliknij pozycję **登录** (**Zaloguj się**) w prawym górnym rogu.
   
    ![Opcja Zaloguj się w usłudze Baidu](./media/notification-hubs-baidu-get-started/BaiduLogin.png)

4. Następnie kliknij na tej stronie pozycję **创建应用** (**Utwórz aplikację**).

    ![Opcja Utwórz aplikację w usłudze Baidu](./media/notification-hubs-baidu-get-started/BaiduCreateApplication.png)

5. Na następnej stronie kliknij pozycję 创建新应用 (**Utwórz nową aplikację**).
   
    ![Opcja Utwórz nową aplikację w usłudze Baidu](./media/notification-hubs-baidu-get-started/BaiduCreateNewApplication.png)

6. Wprowadź nazwę aplikacji, a następnie kliknij pozycję 创建 (**Utwórz**).
   
    ![](./media/notification-hubs-baidu-get-started/BaiduCreateApplicationDoCreate.png)

7. Po pomyślnym utworzeniu projektu powiadomień wypychanych w chmurze Baidu zostanie wyświetlona strona zawierająca następujące dane: **AppID** (Identyfikator aplikacji), **API Key** (Klucz interfejsu API) i **Secret Key** (Klucz tajny). Zanotuj klucz interfejsu API i klucz tajny. Użyjemy ich później.
   
    ![Klucze tajne powiadomień push w usłudze Baidu](./media/notification-hubs-baidu-get-started/BaiduGetSecrets.png)

8. Skonfiguruj projekt dla powiadomień push, klikając pozycję 创建通知 (**Utwórz powiadomienie**) w okienku po lewej stronie.
   
    ![](./media/notification-hubs-baidu-get-started/BaiduCreateNotification.png)


## <a name="configure-a-new-notification-hub"></a>Konfigurowanie nowego centrum powiadomień
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]


&emsp;&emsp;6. W centrum powiadomień wybierz pozycję **Usługi powiadomień**, a następnie wybierz pozycję **Baidu (Android China)**.

&emsp;&emsp;![Azure Notification Hubs — Baidu](./media/notification-hubs-baidu-get-started/AzureNotificationServicesBaidu.png)

&emsp;&emsp;7. Przewiń w dół do sekcji Ustawienia powiadomień Baidu. Wprowadź klucz interfejsu API oraz klucz tajny uzyskany w konsoli Baidu dla projektu powiadomień push w chmurze Baidu. Następnie kliknij przycisk Save (Zapisz).

&emsp;&emsp;![Azure Notification Hubs — klucze tajne w usłudze Baidu](./media/notification-hubs-baidu-get-started/NotificationHubBaiduConfigure.png)

Twoje centrum powiadomień jest teraz skonfigurowane do pracy z usługą Baidu. Uzyskano również **parametry połączenia** do rejestrowania aplikacji w celu odbierania i wysyłania powiadomień push.

Zanotuj wartości `DefaultListenSharedAccessSignature` i `DefaultFullSharedAccessSignature` z okna dostępu do informacji o połączeniu.

## <a name="connect-your-app-to-the-notification-hub"></a>Łączenie aplikacji z centrum powiadomień
1. W programie Android Studio utwórz nowy projekt dla systemu Android, klikając kolejno pozycje File (Plik) > New (Nowy) > New Project (Nowy projekt).

    ![Azure Notification Hubs — nowy projekt w usłudze Baidu](./media/notification-hubs-baidu-get-started/AndroidNewProject.png)

2.  Wprowadź wartość w polu Application Name (Nazwa aplikacji) i upewnij się, że w polu Minimum Required SDK (Minimalna wymagana wersja zestawu SDK) jest ustawiona wersja API 16: Android 4.1. **Upewnij się, że nazwa pakietu (应用包名) jest taka sama, jak w portalu powiadomień push w chmurze Baidu**.

    ![Azure Notification Hubs — minimalna wymagana wersja zestawu SDK1 usługi Baidu](./media/notification-hubs-baidu-get-started/AndroidMinSDK.png)
    ![Azure Notification Hubs — minimalna wymagana wersja zestawu SDK2 usługi Baidu](./media/notification-hubs-baidu-get-started/AndroidMinSDK2.png)

3.  Kliknij przycisk Next (Dalej) i postępuj zgodnie z instrukcjami w kreatorze do momentu wyświetlenia okna Create Activity (Tworzenie działania). Upewnij się, że wybrano pozycję Empty Activity (Puste działanie), a następnie wybierz polecenie Finish (Zakończ), aby utworzyć nową aplikację dla systemu Android.

    ![Azure Notification Hubs — działanie dodawania w usłudze Baidu](./media/notification-hubs-baidu-get-started/AndroidAddActivity.png)

4.  Upewnij się, że w polu Project Build Target (Docelowa kompilacja projektu) określono prawidłową wartość.

5.  Następnie dodaj biblioteki usługi Azure Notification Hubs. W pliku `Build.Gradle` dla aplikacji dodaj następujące wiersze w sekcji dependencies.

    ```javascript
    compile 'com.microsoft.azure:notification-hubs-android-sdk:0.4@aar'
    compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@aar'
    ```

    Dodaj następujące repozytorium po sekcji dependencies.

    ```javascript
    repositories {
        maven {
            url "http://dl.bintray.com/microsoftazuremobile/SDK"
        }
    }
    ```

    W celu uniknięcia konfliktów na liście należy dodać następujący kod do pliku **Manifest.xml**.

    ```xml
    <manifest package="YOUR.PACKAGE.NAME"
    xmlns:tools="http://schemas.android.com/tools"
    xmlns:android="http://schemas.android.com/apk/res/android">
    ```

    Natomiast do tagu `<application/>` należy dodać poniższy kod:

    ```xml
    <application
        tools:replace="android:allowBackup,icon,theme,label">
    ```

6.  Pobierz i rozpakuj [zestaw Android SDK dla powiadomień push w usłudze Baidu]. Skopiuj plik `pushservice-x.y.z jar` z folderu libs. Następnie skopiuj pliki `.so` z folderów `src/main/jniLibs` (utwórz nowy folder) aplikacji dla systemu Android.

    ![Azure Notification Hubs — pliki lib w zestawie SDK usługi Baidu](./media/notification-hubs-baidu-get-started/BaiduSDKLib.png)

7. Prawym przyciskiem myszy kliknij plik pushervice-x.y.z.jar w folderze libs, a następnie kliknij polecenie Add as Library (Dodaj jako bibliotekę), aby uwzględnić ten plik lib w projekcie.

    ![Azure Notification Hubs — polecenie Add as Library (Dodaj jako bibliotekę) w usłudze Baidu](./media/notification-hubs-baidu-get-started/BaiduAddAsALib.jpg)

8. Otwórz plik **AndroidManifest.xml** projektu dla systemu Android i dodaj uprawnienia wymagane przez zestaw SDK usługi Baidu. **Zastąp wartość `YOURPACKAGENAME` nazwą pakietu**.

    ```xml
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
    <uses-permission android:name="android.permission.EXPAND_STATUS_BAR" />
    !! <uses-permission android:name="baidu.push.permission.WRITE_PUSHINFOPROVIDER.YOURPACKAGENAME" />
    !!<permission android:name="baidu.push.permission.WRITE_PUSHINFOPROVIDER.YOURPACKAGENAME"android:protectionLevel="normal" />

    ```

9. Dodaj następującą konfigurację w elemencie aplikacji po elemencie działania `.MainActivity`, zastępując ciąg *yourprojectname* odpowiednią wartością (np. `com.example.BaiduTest`):

    ```xml
    <activity
        android:name="com.baidu.android.pushservice.richmedia.MediaViewActivity"
        android:configChanges="orientation|keyboardHidden"
        android:label="MediaViewActivity" />
    <activity
        android:name="com.baidu.android.pushservice.richmedia.MediaListActivity"
        android:configChanges="orientation|keyboardHidden"
        android:label="MediaListActivity"
        android:launchMode="singleTask" />
 
    <!-- Push application definition message -->
    <receiver android:name=".MyPushMessageReceiver">
        <intent-filter>

            <!-- receive push message-->
            <action android:name="com.baidu.android.pushservice.action.MESSAGE" />
            <!-- receive bind,unbind,fetch,delete.. message-->
            <action android:name="com.baidu.android.pushservice.action.RECEIVE" />
            <action android:name="com.baidu.android.pushservice.action.notification.CLICK" />
        </intent-filter>
    </receiver>

    <receiver
        android:name="com.baidu.android.pushservice.PushServiceReceiver"
        android:process=":bdservice_v1">
        <intent-filter>
            <action android:name="android.intent.action.BOOT_COMPLETED" />
            <action android:name="android.net.conn.CONNECTIVITY_CHANGE" />
            <action android:name="com.baidu.android.pushservice.action.notification.SHOW" />
            <action android:name="com.baidu.android.pushservice.action.media.CLICK" />
            <action android:name="android.intent.action.MEDIA_MOUNTED" />
            <action android:name="android.intent.action.USER_PRESENT" />
            <action android:name="android.intent.action.ACTION_POWER_CONNECTED" />
            <action android:name="android.intent.action.ACTION_POWER_DISCONNECTED" />
        </intent-filter>
    </receiver>

    <receiver
        android:name="com.baidu.android.pushservice.RegistrationReceiver"
        android:process=":bdservice_v1">
        <intent-filter>
            <action android:name="com.baidu.android.pushservice.action.METHOD" />
            <action android:name="com.baidu.android.pushservice.action.BIND_SYNC" />
        </intent-filter>
        <intent-filter>
            <action android:name="android.intent.action.PACKAGE_REMOVED" />

            <data android:scheme="package" />
        </intent-filter>
    </receiver>

    <service
        android:name="com.baidu.android.pushservice.PushService"
        android:exported="true"
        android:process=":bdservice_v1">
        <intent-filter>
            <action android:name="com.baidu.android.pushservice.action.PUSH_SERVICE" />
        </intent-filter>
    </service>

    <service
        android:name="com.baidu.android.pushservice.CommandService"
        android:exported="true" />

    <!-- Adapt the ContentProvider declaration required for the Android N system, and the write permissions include the application package name-->
    <provider
        android:name="com.baidu.android.pushservice.PushInfoProvider"
        android:authorities="com.baidu.push.example.bdpush"
        android:exported="true"
        android:protectionLevel="signature"
        android:writePermission="baidu.push.permission.WRITE_PUSHINFOPROVIDER. yourprojectname  " />

    <!-- API Key of the Baidu application -->
    <meta-data
        android:name="api_key"
        !!   android:value="api_key" />
    </application>
    ```

10. Dodaj do projektu nową klasę o nazwie `ConfigurationSettings.java`.

    ```java
    public class ConfigurationSettings {
        public static String API_KEY = "...";
        public static String NotificationHubName = "...";
        public static String NotificationHubConnectionString = "...";
    }
    ```
    
    Dla ciągu `API_KEY` ustaw wartość API_KEY uzyskaną z projektu w chmurze Baidu.
    
    Dla ciągu `NotificationHubName` ustaw nazwę centrum powiadomień z witryny [Azure Portal], a następnie ustaw wartość `DefaultListenSharedAccessSignature` z witryny [Azure Portal] dla elementu `NotificationHubConnectionString`.

11. Otwórz plik MainActivity.java i dodaj następujący kod do metody onCreate:

    ```java
    PushManager.startWork(this, PushConstants.LOGIN_TYPE_API_KEY,  API_KEY );
    ```

12. Dodaj nową klasę o nazwie `MyPushMessageReceiver.java` i dodaj do niej następujący kod. To jest klasa, która obsługuje powiadomienia wypychane odbierane z serwera powiadomień wypychanych Baidu.

    ```java
    package your.package.name;

    import android.content.Context;
    import android.content.Intent;
    import android.os.AsyncTask;
    import android.text.TextUtils;
    import android.util.Log;

    import com.baidu.android.pushservice.PushMessageReceiver;
    import com.microsoft.windowsazure.messaging.NotificationHub;
    import org.json.JSONException;
    import org.json.JSONObject;

    import java.util.List;

    public class MyPushMessageReceiver extends PushMessageReceiver {

        public static final String TAG = MyPushMessageReceiver.class
                .getSimpleName();
        public static NotificationHub hub = null;
        public static String mChannelId, mUserId;

        @Override
        public void onBind(Context context, int errorCode, String appid,
                        String userId, String channelId, String requestId) {
            String responseString = "onBind errorCode=" + errorCode + " appid="
                    + appid + " userId=" + userId + " channelId=" + channelId
                    + " requestId=" + requestId;
            Log.d(TAG, responseString);

            if (errorCode == 0) {
                // Binding successful
                Log.d(TAG, " Binding successful");
            }
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
            mChannelId = channelId;
            mUserId = userId;

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
        public void onMessage(Context context, String message,
                            String customContentString) {
            String messageString = " onMessage=\"" + message
                    + "\" customContentString=" + customContentString;
            Log.d(TAG, messageString);
            if (!TextUtils.isEmpty(customContentString)) {
                JSONObject customJson = null;
                try {
                    customJson = new JSONObject(customContentString);
                    String myvalue = null;
                    if (!customJson.isNull("mykey")) {
                        myvalue = customJson.getString("mykey");
                    }
                } catch (JSONException e) {
                    e.printStackTrace();
                }
            }

        }

        @Override
        public void onNotificationArrived(Context context, String title, String description, String customContentString) {
            String notifyString = " Notice Arrives onNotificationArrived  title=\"" + title
                    + "\" description=\"" + description + "\" customContent="
                    + customContentString;
            Log.d(TAG, notifyString);
            if (!TextUtils.isEmpty(customContentString)) {
                JSONObject customJson = null;
                try {
                    customJson = new JSONObject(customContentString);
                    String myvalue = null;
                    if (!customJson.isNull("mykey")) {
                        myvalue = customJson.getString("mykey");
                    }
                } catch (JSONException e) {
                    // TODO Auto-generated catch block
                    e.printStackTrace();
                }
            }
        }

        @Override
        public void onNotificationClicked(Context context, String title, String description, String customContentString) {
            String notifyString = " onNotificationClicked title=\"" + title + "\" description=\""
                    + description + "\" customContent=" + customContentString;
            Log.d(TAG, notifyString);
            Intent intent = new Intent(context.getApplicationContext(),MainActivity.class);
            intent.putExtra("title",title);
            intent.putExtra("description",description);
            intent.putExtra("isFromNotify",true);
            intent.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK);
            context.getApplicationContext().startActivity(intent);

        }

        @Override
        public void onSetTags(Context context, int errorCode,
                            List<String> successTags, List<String> failTags, String requestId) {
            String responseString = "onSetTags errorCode=" + errorCode
                    + " successTags=" + successTags + " failTags=" + failTags
                    + " requestId=" + requestId;
            Log.d(TAG, responseString);

        }

        @Override
        public void onDelTags(Context context, int errorCode,
                            List<String> successTags, List<String> failTags, String requestId) {
            String responseString = "onDelTags errorCode=" + errorCode
                    + " successTags=" + successTags + " failTags=" + failTags
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

            if (errorCode == 0) {
                // Unbinding is successful
                Log.d(TAG, " Unbinding is successful ");
            }
        }
    }
    ```

## <a name="send-notifications-to-your-app"></a>Wysyłanie powiadomień do aplikacji

Odbieranie powiadomień możesz szybko przetestować w witrynie [Azure Portal], w tym celu użyj przycisku **Wyślij** na ekranie konfiguracji centrum powiadomień, jak pokazano na następującym zrzucie ekranu:

![](./media/notification-hubs-baidu-get-started/BaiduTestSendButton.png)
![](./media/notification-hubs-baidu-get-started/BaiduTestSend.png)

Powiadomienia wypychane są zwykle wysyłane za pośrednictwem usługi zaplecza, takiej jak Mobile Services czy ASP.NET, z użyciem zgodnej biblioteki. Jeśli biblioteka nie jest dostępna w danym zapleczu, powiadomienia można wysyłać bezpośrednio za pomocą interfejsu API REST.

Dla uproszczenia w tym samouczku użyto aplikacji konsoli w celu zademonstrowania, w jaki sposób wysyłać powiadomienia przy użyciu zestawu .NET SDK. Zaleca się jednak, aby w następnym kroku zapoznać się z samouczkiem [Wysyłanie powiadomień push do użytkowników przy użyciu usługi Notification Hubs](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) dotyczącym wysyłania powiadomień przy użyciu zaplecza ASP.NET. 

Poniżej przedstawiono różne metody wysyłania powiadomień:
* **Interfejs REST**: powiadomienia mogą być obsługiwane na dowolnej platformie zaplecza za pomocą [interfejsu REST](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).
* **Zestaw SDK .NET dla usługi Microsoft Azure Notification Hubs**: w menedżerze pakietów NuGet dla programu Visual Studio uruchom polecenie [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).
* **Node.js**: [Jak używać usługi Notification Hubs z poziomu środowiska Node.js](notification-hubs-nodejs-push-notification-tutorial.md).
* **Mobile Apps**: aby zapoznać się z przykładem wysyłania powiadomień z poziomu usługi Azure App Service Mobile Apps zintegrowanej z usługą Notification Hubs, zobacz [Dodawanie powiadomień wypychanych do aplikacji mobilnej](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).
* **Java / PHP**: aby zapoznać się z przykładem wysyłania powiadomień przy użyciu interfejsów API REST, zobacz „How to use Notification Hubs from Java/PHP” (Jak używać usługi Notification Hubs za pomocą języka Java/PHP) — [Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md).

## <a name="optional-send-notifications-from-a-net-console-app"></a>(Opcjonalnie) Wysyłanie powiadomień z poziomu aplikacji konsolowej .NET
W tej sekcji przedstawiono sposób wysyłania powiadomienia za pomocą aplikacji konsolowej .NET.

1. Utwórz nową aplikację konsoli języka Visual C#:
   
    ![](./media/notification-hubs-baidu-get-started/ConsoleProject.png)

2. W oknie Konsola menedżera pakietów ustaw nowy projekt aplikacji konsoli jako **Projekt domyślny**, a następnie w oknie konsoli uruchom następujące polecenie:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    Ta instrukcja powoduje dodanie odwołania do zestawu SDK usługi Azure Notification Hubs z użyciem <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pakietu NuGet Microsoft.Azure.Notification Hubs</a>.
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)

3. Otwórz plik `Program.cs` i dodaj następującą instrukcję Using:
   
    ```csharp
    using Microsoft.Azure.NotificationHubs;
    ```

4. W Twojej klasie `Program` dodaj następującą metodę i zastąp elementy `DefaultFullSharedAccessSignatureSASConnectionString` i `NotificationHubName` uzyskanymi wartościami.
   
    ```csharp
    private static async void SendNotificationAsync()
    {
        NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("DefaultFullSharedAccessSignatureSASConnectionString", "NotificationHubName");
        string message = "{\"title\":\"((Notification title))\",\"description\":\"Hello from Azure\"}";
        var result = await hub.SendBaiduNativeNotificationAsync(message);
    }
    ```

5. Dodaj następujące wiersze do metody `Main`:

    ```csharp
    SendNotificationAsync();
    Console.ReadLine();
    ```

## <a name="test-your-app"></a>Testowanie aplikacji

Aby przetestować tę aplikację przy użyciu rzeczywistego telefonu, podłącz telefon do komputera za pomocą kabla USB. To działanie spowoduje załadowanie aplikacji do podłączonego telefonu.

Aby przetestować tę aplikację przy użyciu emulatora, na górnym pasku narzędzi Android Studio kliknij pozycję **Run** (Uruchom), a następnie wybierz aplikację. Spowoduje to uruchomienie emulatora, a następnie załadowanie i uruchomienie aplikacji.

Aplikacja pobiera wartości parametrów `userId` i `channelId` z usługi powiadomień push Baidu i wykonuje rejestrację w centrum powiadomień.

Testowe powiadomienie można wysłać przy użyciu karty debugowania w witrynie [Azure Portal]. Jeśli utworzono aplikację konsolową .NET dla programu Visual Studio, naciśnij klawisz F5 w programie Visual Studio, aby uruchomić aplikację. Aplikacja wyśle powiadomienie, które zostanie wyświetlone w górnym obszarze powiadomień urządzenia lub emulatora.

<!-- URLs. -->
[Mobile Services Android SDK]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[zestaw Android SDK dla powiadomień push w usłudze Baidu]: http://push.baidu.com/sdk/push_client_sdk_for_android
[Azure Portal]: https://portal.azure.com/
[portalu Baidu]: http://www.baidu.com/
