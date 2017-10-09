
### <a name="update-manifest-file-tooenable-notifications"></a><span data-ttu-id="ebf4b-101">Aktualizacja pliku manifestu tooenable powiadomienia</span><span class="sxs-lookup"><span data-stu-id="ebf4b-101">Update manifest file tooenable notifications</span></span>
<span data-ttu-id="ebf4b-102">Kopiuj do pliku Manifest.xml między hello zasoby obsługi komunikatów w aplikacji hello poniżej `<application>` i `</application>` tagów.</span><span class="sxs-lookup"><span data-stu-id="ebf4b-102">Copy hello in-app messaging resources below into your Manifest.xml between hello `<application>` and `</application>` tags.</span></span>

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

### <a name="specify-an-icon-for-notifications"></a><span data-ttu-id="ebf4b-103">Określanie ikony dla powiadomień</span><span class="sxs-lookup"><span data-stu-id="ebf4b-103">Specify an icon for notifications</span></span>
<span data-ttu-id="ebf4b-104">Wklej powitania po fragment kodu XML w pliku Manifest.xml między hello `<application>` i `</application>` tagów.</span><span class="sxs-lookup"><span data-stu-id="ebf4b-104">Paste hello following XML snippet in your Manifest.xml between hello `<application>` and `</application>` tags.</span></span>

        <meta-data android:name="engagement:reach:notification:icon" android:value="engagement_close"/>

<span data-ttu-id="ebf4b-105">Definiuje hello ikonę, która jest wyświetlana zarówno w systemie i powiadomień w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ebf4b-105">This defines hello icon that is displayed both in system and in-app notifications.</span></span> <span data-ttu-id="ebf4b-106">Ta czynność jest opcjonalna w przypadku powiadomień wewnętrznych aplikacji, lecz obowiązkowa w przypadku powiadomień systemowych.</span><span class="sxs-lookup"><span data-stu-id="ebf4b-106">It is optional for in-app notifications however mandatory for system notifications.</span></span> <span data-ttu-id="ebf4b-107">System Android będzie odrzucać powiadomienia systemowe z nieprawidłowymi ikonami.</span><span class="sxs-lookup"><span data-stu-id="ebf4b-107">Android will rejects system notifications with invalid icons.</span></span>

<span data-ttu-id="ebf4b-108">Upewnij się, że używasz ikony znajdującej się w jednym z hello **obiektów drawable** folderów (takie jak ``engagement_close.png``).</span><span class="sxs-lookup"><span data-stu-id="ebf4b-108">Make sure you are using an icon that exists in one of hello **drawable** folders (like ``engagement_close.png``).</span></span> <span data-ttu-id="ebf4b-109">Folder **mipmap** nie jest obsługiwany.</span><span class="sxs-lookup"><span data-stu-id="ebf4b-109">**mipmap** folder isn't supported.</span></span>

> [!NOTE]
> <span data-ttu-id="ebf4b-110">Nie należy używać hello **uruchamiania** ikony.</span><span class="sxs-lookup"><span data-stu-id="ebf4b-110">You should not use hello **launcher** icon.</span></span> <span data-ttu-id="ebf4b-111">Ma ona inną rozdzielczość i zazwyczaj w folderach mipmap hello, które nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="ebf4b-111">It has a different resolution and is usually in hello mipmap folders, which we don't support.</span></span>
> 
> 

<span data-ttu-id="ebf4b-112">W przypadku aplikacji rzeczywistych można użyć ikony odpowiedniej dla powiadomień zgodnie z [zaleceniami dotyczącymi projektowania w systemie Android](http://developer.android.com/design/patterns/notifications.html).</span><span class="sxs-lookup"><span data-stu-id="ebf4b-112">For real apps, you can use an icon that is suitable for notifications per [Android design guidelines](http://developer.android.com/design/patterns/notifications.html).</span></span>

> [!TIP]
> <span data-ttu-id="ebf4b-113">toobe toouse się, że poprawne rozdzielczość ikony można przyjrzeć się [te przykłady](https://www.google.com/design/icons).</span><span class="sxs-lookup"><span data-stu-id="ebf4b-113">toobe sure toouse correct icon resolutions, you can look at [these examples](https://www.google.com/design/icons).</span></span>
> <span data-ttu-id="ebf4b-114">Przewiń w dół toohello **powiadomień** sekcji, kliknij ikonę, a następnie kliknij `PNGS` zestaw obiektów drawable toodownload hello ikon.</span><span class="sxs-lookup"><span data-stu-id="ebf4b-114">Scroll down toohello **Notification** section, click an icon, and then click `PNGS` toodownload hello icon drawable set.</span></span> <span data-ttu-id="ebf4b-115">Foldery obiektów drawable i jakie które toouse rozwiązania dla poszczególnych wersji ikony hello jest widoczny.</span><span class="sxs-lookup"><span data-stu-id="ebf4b-115">You can see what drawable folders with which resolution toouse for each version of hello icon.</span></span>
> 
> 

### <a name="enable-your-app-tooreceive-gcm-push-notifications"></a><span data-ttu-id="ebf4b-116">Włączanie powiadomień wypychanych usługi GCM tooreceive aplikacji</span><span class="sxs-lookup"><span data-stu-id="ebf4b-116">Enable your app tooreceive GCM push notifications</span></span>
1. <span data-ttu-id="ebf4b-117">Wklej następujący hello do pliku Manifest.xml między hello `<application>` i `</application>` tagi po zastąpieniu hello **identyfikator nadawcy** uzyskanego z konsoli Firebase projektu.</span><span class="sxs-lookup"><span data-stu-id="ebf4b-117">Paste hello following into your Manifest.xml between hello `<application>` and `</application>` tags after replacing hello **Sender ID** obtained from your Firebase project console.</span></span> <span data-ttu-id="ebf4b-118">Witaj \n jest zamierzony dlatego należy upewnić się, że zakończysz numeru projektu hello.</span><span class="sxs-lookup"><span data-stu-id="ebf4b-118">hello \n is intentional so make sure that you end hello project number with it.</span></span>
   
        <meta-data android:name="engagement:gcm:sender" android:value="************\n" />
2. <span data-ttu-id="ebf4b-119">Wklej poniższy kod hello do pliku Manifest.xml między hello `<application>` i `</application>` tagów.</span><span class="sxs-lookup"><span data-stu-id="ebf4b-119">Paste hello code below into your Manifest.xml between hello `<application>` and `</application>` tags.</span></span> <span data-ttu-id="ebf4b-120">Zastąp nazwę pakietu hello <Your package name>.</span><span class="sxs-lookup"><span data-stu-id="ebf4b-120">Replace hello package name <Your package name>.</span></span>
   
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
3. <span data-ttu-id="ebf4b-121">Dodaj ostatni zestaw uprawnień, które są wyróżnione przed hello hello `<application>` tagu.</span><span class="sxs-lookup"><span data-stu-id="ebf4b-121">Add hello last set of permissions that are highlighted before hello `<application>` tag.</span></span> <span data-ttu-id="ebf4b-122">Zastąp `<Your package name>` przez hello rzeczywistą nazwą pakietu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ebf4b-122">Replace `<Your package name>` by hello actual package name of your application.</span></span>
   
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="<Your package name>.permission.C2D_MESSAGE" />
        <permission android:name="<Your package name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

