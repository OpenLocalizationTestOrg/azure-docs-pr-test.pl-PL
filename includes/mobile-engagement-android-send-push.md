
### <a name="update-manifest-file-tooenable-notifications"></a>Aktualizacja pliku manifestu tooenable powiadomienia
Kopiuj do pliku Manifest.xml między hello zasoby obsługi komunikatów w aplikacji hello poniżej `<application>` i `</application>` tagów.

        <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT" />
                <data android:mimeType="text/plain" />
              </intent-filter>
        </activity>
        <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
            <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT" />
                <data android:mimeType="text/html" />
            </intent-filter>
        </activity>
        <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementPollActivity" android:theme="@android:style/Theme.Light" android:exported="false">
            <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="android.intent.category.DEFAULT" />
            </intent-filter>
        </activity>
        <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity" android:theme="@android:style/Theme.Dialog" android:exported="false">
            <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
                <category android:name="android.intent.category.DEFAULT"/>
            </intent-filter>
        </activity>
        <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver" android:exported="false">
            <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
            </intent-filter>
        </receiver>
        <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachDownloadReceiver">
            <intent-filter>
                <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
            </intent-filter>
        </receiver>

### <a name="specify-an-icon-for-notifications"></a>Określanie ikony dla powiadomień
Wklej powitania po fragment kodu XML w pliku Manifest.xml między hello `<application>` i `</application>` tagów.

        <meta-data android:name="engagement:reach:notification:icon" android:value="engagement_close"/>

Definiuje hello ikonę, która jest wyświetlana zarówno w systemie i powiadomień w aplikacji. Ta czynność jest opcjonalna w przypadku powiadomień wewnętrznych aplikacji, lecz obowiązkowa w przypadku powiadomień systemowych. System Android będzie odrzucać powiadomienia systemowe z nieprawidłowymi ikonami.

Upewnij się, że używasz ikony znajdującej się w jednym z hello **obiektów drawable** folderów (takie jak ``engagement_close.png``). Folder **mipmap** nie jest obsługiwany.

> [!NOTE]
> Nie należy używać hello **uruchamiania** ikony. Ma ona inną rozdzielczość i zazwyczaj w folderach mipmap hello, które nie są obsługiwane.
> 
> 

W przypadku aplikacji rzeczywistych można użyć ikony odpowiedniej dla powiadomień zgodnie z [zaleceniami dotyczącymi projektowania w systemie Android](http://developer.android.com/design/patterns/notifications.html).

> [!TIP]
> toobe toouse się, że poprawne rozdzielczość ikony można przyjrzeć się [te przykłady](https://www.google.com/design/icons).
> Przewiń w dół toohello **powiadomień** sekcji, kliknij ikonę, a następnie kliknij `PNGS` zestaw obiektów drawable toodownload hello ikon. Foldery obiektów drawable i jakie które toouse rozwiązania dla poszczególnych wersji ikony hello jest widoczny.
> 
> 

### <a name="enable-your-app-tooreceive-gcm-push-notifications"></a>Włączanie powiadomień wypychanych usługi GCM tooreceive aplikacji
1. Wklej następujący hello do pliku Manifest.xml między hello `<application>` i `</application>` tagi po zastąpieniu hello **identyfikator nadawcy** uzyskanego z konsoli Firebase projektu. Witaj \n jest zamierzony dlatego należy upewnić się, że zakończysz numeru projektu hello.
   
        <meta-data android:name="engagement:gcm:sender" android:value="************\n" />
2. Wklej poniższy kod hello do pliku Manifest.xml między hello `<application>` i `</application>` tagów. Zastąp nazwę pakietu hello <Your package name>.
   
        <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMEnabler"
        android:exported="false">
            <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT" />
            </intent-filter>
        </receiver>
   
        <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMReceiver" android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.REGISTRATION" />
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<Your package name>" />
            </intent-filter>
        </receiver>
3. Dodaj ostatni zestaw uprawnień, które są wyróżnione przed hello hello `<application>` tagu. Zastąp `<Your package name>` przez hello rzeczywistą nazwą pakietu aplikacji.
   
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="<Your package name>.permission.C2D_MESSAGE" />
        <permission android:name="<Your package name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

