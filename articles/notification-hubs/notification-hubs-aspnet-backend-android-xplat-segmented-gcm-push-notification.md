---
title: "aaaNotification koncentratory fundamentalne wiadomości Samouczek — systemu Android"
description: "Dowiedz się, jak toosend usługi centra powiadomień Azure Service Bus toouse fundamentalne urządzeń tooAndroid powiadomień wiadomości."
services: notification-hubs
documentationcenter: android
author: ysxu
manager: erikre
editor: 
ms.assetid: 3c23cb80-9d35-4dde-b26d-a7bfd4cb8f81
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: e6eb41bec95c67d7dc059f560194966d04400494
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-breaking-news"></a><span data-ttu-id="79873-103">Użyj usługi Notification Hubs toosend fundamentalne wiadomości</span><span class="sxs-lookup"><span data-stu-id="79873-103">Use Notification Hubs toosend breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="79873-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="79873-104">Overview</span></span>
<span data-ttu-id="79873-105">W tym temacie opisano sposób toouse usługi Azure Notification Hubs toobroadcast najważniejszych wiadomości powiadomienia tooan aplikacji systemu Android.</span><span class="sxs-lookup"><span data-stu-id="79873-105">This topic shows you how toouse Azure Notification Hubs toobroadcast breaking news notifications tooan Android app.</span></span> <span data-ttu-id="79873-106">Po zakończeniu będzie być może tooregister zakłócenia w kategorii wiadomości i odbierać tylko powiadomienia wypychane dla tych kategorii.</span><span class="sxs-lookup"><span data-stu-id="79873-106">When complete, you will be able tooregister for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="79873-107">Ten scenariusz jest wspólnego wzorca dla wielu aplikacji, w której powiadomienia mają toogroups toobe wysyłane użytkowników, które wcześniej zostały zadeklarowane zainteresowanie je, np. czytnik danych RSS, aplikacje wentylatory utworów muzycznych itp.</span><span class="sxs-lookup"><span data-stu-id="79873-107">This scenario is a common pattern for many apps where notifications have toobe sent toogroups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="79873-108">Scenariusze emisji są włączone, umieszczając w niej co najmniej jeden *tagi* podczas tworzenia rejestracji w Centrum powiadomień hello.</span><span class="sxs-lookup"><span data-stu-id="79873-108">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in hello notification hub.</span></span> <span data-ttu-id="79873-109">Gdy tooa tag wysyłane są powiadomienia, wszystkie urządzenia, które zostały zarejestrowane dla tagu hello będzie wysyłane powiadomienie hello.</span><span class="sxs-lookup"><span data-stu-id="79873-109">When notifications are sent tooa tag, all devices that have registered for hello tag will receive hello notification.</span></span> <span data-ttu-id="79873-110">Ponieważ tagi są po prostu ciągów, nie mają toobe udostępnione wcześniej.</span><span class="sxs-lookup"><span data-stu-id="79873-110">Because tags are simply strings, they do not have toobe provisioned in advance.</span></span> <span data-ttu-id="79873-111">Aby uzyskać więcej informacji na temat tagów, zobacz zbyt[routingu centra powiadomień i wyrażeń tagów](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="79873-111">For more information about tags, refer too[Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79873-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="79873-112">Prerequisites</span></span>
<span data-ttu-id="79873-113">W tym temacie opiera się na aplikacji hello utworzony w [Rozpoczynanie pracy z usługą Notification Hubs][get-started].</span><span class="sxs-lookup"><span data-stu-id="79873-113">This topic builds on hello app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="79873-114">Przed rozpoczęciem tego samouczka należy zostały już wykonane [Rozpoczynanie pracy z usługą Notification Hubs][get-started].</span><span class="sxs-lookup"><span data-stu-id="79873-114">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-toohello-app"></a><span data-ttu-id="79873-115">Dodaj aplikację toohello wybór kategorii</span><span class="sxs-lookup"><span data-stu-id="79873-115">Add category selection toohello app</span></span>
<span data-ttu-id="79873-116">pierwszym krokiem Hello jest hello tooadd interfejsu użytkownika elementy tooyour istniejącego głównego działania umożliwiające hello użytkownika tooselect kategorii tooregister.</span><span class="sxs-lookup"><span data-stu-id="79873-116">hello first step is tooadd hello UI elements tooyour existing main activity that enable hello user tooselect categories tooregister.</span></span> <span data-ttu-id="79873-117">Witaj kategorie wybrane przez użytkownika są przechowywane na urządzeniu hello.</span><span class="sxs-lookup"><span data-stu-id="79873-117">hello categories selected by a user are stored on hello device.</span></span> <span data-ttu-id="79873-118">Po uruchomieniu aplikacji hello rejestracji urządzenia jest tworzony w Centrum powiadomień z kategorii hello wybrany jako znaczniki.</span><span class="sxs-lookup"><span data-stu-id="79873-118">When hello app starts, a device registration is created in your notification hub with hello selected categories as tags.</span></span>

1. <span data-ttu-id="79873-119">Otwórz plik res/layout/activity_main.xml i Zastąp zawartość hello hello następujący:</span><span class="sxs-lookup"><span data-stu-id="79873-119">Open your res/layout/activity_main.xml file, and substitute hello content with hello following:</span></span>
   
        <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
            xmlns:tools="http://schemas.android.com/tools"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:paddingBottom="@dimen/activity_vertical_margin"
            android:paddingLeft="@dimen/activity_horizontal_margin"
            android:paddingRight="@dimen/activity_horizontal_margin"
            android:paddingTop="@dimen/activity_vertical_margin"
            tools:context="com.example.breakingnews.MainActivity"
            android:orientation="vertical">
   
                <CheckBox
                    android:id="@+id/worldBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_world" />
                <CheckBox
                    android:id="@+id/politicsBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_politics" />
                <CheckBox
                    android:id="@+id/businessBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_business" />
                <CheckBox
                    android:id="@+id/technologyBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_technology" />
                <CheckBox
                    android:id="@+id/scienceBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_science" />
                <CheckBox
                    android:id="@+id/sportsBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_sports" />
                <Button
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:onClick="subscribe"
                    android:text="@string/button_subscribe" />
        </LinearLayout>
2. <span data-ttu-id="79873-120">Otwórz plik res/values/strings.xml i Dodaj hello następujące wiersze:</span><span class="sxs-lookup"><span data-stu-id="79873-120">Open your res/values/strings.xml file and add hello following lines:</span></span>
   
        <string name="button_subscribe">Subscribe</string>
        <string name="label_world">World</string>
        <string name="label_politics">Politics</string>
        <string name="label_business">Business</string>
        <string name="label_technology">Technology</string>
        <string name="label_science">Science</string>
        <string name="label_sports">Sports</string>
   
    <span data-ttu-id="79873-121">Układu graficznego main_activity.xml powinna wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="79873-121">Your main_activity.xml graphical layout should now look like this:</span></span>
   
    ![][A1]
3. <span data-ttu-id="79873-122">Teraz Utwórz klasę **powiadomienia** w hello same pakiety z **MainActivity** klasy.</span><span class="sxs-lookup"><span data-stu-id="79873-122">Now create a class **Notifications** in hello same package as your **MainActivity** class.</span></span>
   
        import java.util.HashSet;
        import java.util.Set;
   
        import android.content.Context;
        import android.content.SharedPreferences;
        import android.os.AsyncTask;
        import android.util.Log;
        import android.widget.Toast;
   
        import com.google.android.gms.gcm.GoogleCloudMessaging;
        import com.microsoft.windowsazure.messaging.NotificationHub;
   
        public class Notifications {
            private static final String PREFS_NAME = "BreakingNewsCategories";
            private GoogleCloudMessaging gcm;
            private NotificationHub hub;
            private Context context;
            private String senderId;
   
            public Notifications(Context context, String senderId, String hubName, 
                                    String listenConnectionString) {
                this.context = context;
                this.senderId = senderId;
   
                gcm = GoogleCloudMessaging.getInstance(context);
                hub = new NotificationHub(hubName, listenConnectionString, context);
            }
   
            public void storeCategoriesAndSubscribe(Set<String> categories)
            {
                SharedPreferences settings = context.getSharedPreferences(PREFS_NAME, 0);
                settings.edit().putStringSet("categories", categories).commit();
                subscribeToCategories(categories);
            }
   
            public Set<String> retrieveCategories() {
                SharedPreferences settings = context.getSharedPreferences(PREFS_NAME, 0);
                return settings.getStringSet("categories", new HashSet<String>());
            }
   
            public void subscribeToCategories(final Set<String> categories) {
                new AsyncTask<Object, Object, Object>() {
                    @Override
                    protected Object doInBackground(Object... params) {
                        try {
                            String regid = gcm.register(senderId);
   
                            String templateBodyGCM = "{\"data\":{\"message\":\"$(messageParam)\"}}";
   
                            hub.registerTemplate(regid,"simpleGCMTemplate", templateBodyGCM, 
                                categories.toArray(new String[categories.size()]));
                        } catch (Exception e) {
                            Log.e("MainActivity", "Failed tooregister - " + e.getMessage());
                            return e;
                        }
                        return null;
                    }
   
                    protected void onPostExecute(Object result) {
                        String message = "Subscribed for categories: "
                                + categories.toString();
                        Toast.makeText(context, message,
                                Toast.LENGTH_LONG).show();
                    }
                }.execute(null, null, null);
            }
   
        }
   
    <span data-ttu-id="79873-123">Ta klasa korzysta z hello Magazyn lokalny toostore hello kategorii wiadomości, czy to urządzenie ma tooreceive.</span><span class="sxs-lookup"><span data-stu-id="79873-123">This class uses hello local storage toostore hello categories of news that this device has tooreceive.</span></span> <span data-ttu-id="79873-124">Zawiera również metody tooregister dla tych kategorii.</span><span class="sxs-lookup"><span data-stu-id="79873-124">It also contains methods tooregister for these categories.</span></span>
4. <span data-ttu-id="79873-125">W Twojej **MainActivity** klasy Usuń prywatne pól dla **NotificationHub** i **GoogleCloudMessaging**, i Dodaj pole do **powiadomienia**:</span><span class="sxs-lookup"><span data-stu-id="79873-125">In your **MainActivity** class remove your private fields for **NotificationHub** and **GoogleCloudMessaging**, and add a field for **Notifications**:</span></span>
   
        // private GoogleCloudMessaging gcm;
        // private NotificationHub hub;
        private Notifications notifications;
5. <span data-ttu-id="79873-126">Następnie w hello **onCreate** metody, Usuń inicjowanie hello hello **Centrum** pola i hello **registerWithNotificationHubs** — metoda.</span><span class="sxs-lookup"><span data-stu-id="79873-126">Then, in hello **onCreate** method, remove hello initialization of hello **hub** field and hello **registerWithNotificationHubs** method.</span></span> <span data-ttu-id="79873-127">Następnie dodaj następujące wiersze, które inicjuje wystąpienie klasy hello hello **powiadomienia** klasy.</span><span class="sxs-lookup"><span data-stu-id="79873-127">Then add hello following lines which initialize an instance of hello **Notifications** class.</span></span> 

        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
            MyHandler.mainActivity = this;

            NotificationsManager.handleNotifications(this, SENDER_ID,
                    MyHandler.class);

            notifications = new Notifications(this, SENDER_ID, HubName, HubListenConnectionString);

            notifications.subscribeToCategories(notifications.retrieveCategories());
        }

    <span data-ttu-id="79873-128">`HubName`i `HubListenConnectionString` już powinien być ustawiony z hello `<hub name>` i `<connection string with listen access>` symbole zastępcze z powiadomienia Centrum nazwy i hello parametrów połączenia dla *DefaultListenSharedAccessSignature* uzyskany wcześniej.</span><span class="sxs-lookup"><span data-stu-id="79873-128">`HubName` and `HubListenConnectionString` should already be set with hello `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and hello connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>

    > [AZURE.NOTE] <span data-ttu-id="79873-129">Ponieważ poświadczenia, które są dystrybuowane wraz z aplikacji przez klienta nie są zazwyczaj bezpieczna, hello klucz dostępu do nasłuchiwania należy dystrybuować tylko z aplikacji klienta.</span><span class="sxs-lookup"><span data-stu-id="79873-129">Because credentials that are distributed with a client app are not generally secure, you should only distribute hello key for listen access with your client app.</span></span> <span data-ttu-id="79873-130">Nasłuchiwanie umożliwia dostęp, nie można zmodyfikować tooregister Twojej aplikacji dla powiadomień, ale istniejące rejestracje i nie mogą być wysyłane powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="79873-130">Listen access enables your app tooregister for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="79873-131">klucz pełny dostęp Hello jest używany w usłudze zabezpieczonych wewnętrznej bazy danych do wysyłania powiadomień i zmianę istniejącego rejestracji.</span><span class="sxs-lookup"><span data-stu-id="79873-131">hello full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>


1. <span data-ttu-id="79873-132">Następnie należy dodać importuje powitania po i `subscribe` hello toohandle metody subskrypcji przycisk kliknij zdarzenie:</span><span class="sxs-lookup"><span data-stu-id="79873-132">Then, add hello following imports and `subscribe` method toohandle hello subscribe button click event:</span></span>
   
        import android.widget.CheckBox;
        import java.util.HashSet;
        import java.util.Set;
   
        public void subscribe(View sender) {
            final Set<String> categories = new HashSet<String>();
   
            CheckBox world = (CheckBox) findViewById(R.id.worldBox);
            if (world.isChecked())
                categories.add("world");
            CheckBox politics = (CheckBox) findViewById(R.id.politicsBox);
            if (politics.isChecked())
                categories.add("politics");
            CheckBox business = (CheckBox) findViewById(R.id.businessBox);
            if (business.isChecked())
                categories.add("business");
            CheckBox technology = (CheckBox) findViewById(R.id.technologyBox);
            if (technology.isChecked())
                categories.add("technology");
            CheckBox science = (CheckBox) findViewById(R.id.scienceBox);
            if (science.isChecked())
                categories.add("science");
            CheckBox sports = (CheckBox) findViewById(R.id.sportsBox);
            if (sports.isChecked())
                categories.add("sports");
   
            notifications.storeCategoriesAndSubscribe(categories);
        }
   
    <span data-ttu-id="79873-133">Ta metoda tworzy listę kategorii i używa hello **powiadomienia** klasy toostore hello listy w magazynie lokalnym hello i zarejestruj hello odpowiednie tagi w Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="79873-133">This method creates a list of categories and uses hello **Notifications** class toostore hello list in hello local storage and register hello corresponding tags with your notification hub.</span></span> <span data-ttu-id="79873-134">Zmiana kategorii rejestracji hello zostaje odtworzone w hello nowych kategorii.</span><span class="sxs-lookup"><span data-stu-id="79873-134">When categories are changed, hello registration is recreated with hello new categories.</span></span>

<span data-ttu-id="79873-135">Aplikacji jest teraz możliwe toostore zestaw kategorii w lokalnej pamięci masowej na powitania urządzenia i rejestruje hello Centrum powiadomień, gdy wybór kategorii hello hello zmiany wprowadzane przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="79873-135">Your app is now able toostore a set of categories in local storage on hello device and register with hello notification hub whenever hello user changes hello selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="79873-136">Rejestrowanie się w celu powiadomienia</span><span class="sxs-lookup"><span data-stu-id="79873-136">Register for notifications</span></span>
<span data-ttu-id="79873-137">Następujące kroki, zarejestruj się w Centrum powiadomień hello podczas uruchamiania przy użyciu hello kategorie, które były przechowywane w magazynie lokalnym.</span><span class="sxs-lookup"><span data-stu-id="79873-137">These steps register with hello notification hub on startup using hello categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="79873-138">Ponieważ registrationId hello przypisane przez Google Cloud Messaging (GCM) można zmienić w dowolnym momencie, należy zarejestrować powiadomienia o często tooavoid powiadomień błędów.</span><span class="sxs-lookup"><span data-stu-id="79873-138">Because hello registrationId assigned by Google Cloud Messaging (GCM) can change at any time, you should register for notifications frequently tooavoid notification failures.</span></span> <span data-ttu-id="79873-139">W tym przykładzie rejestruje powiadomienia o każdym uruchomieniu danej aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="79873-139">This example registers for notification every time that hello app starts.</span></span> <span data-ttu-id="79873-140">Dla aplikacji, które są uruchamiane często więcej niż raz dziennie, prawdopodobnie Jeśli możesz pominąć rejestrację toopreserve przepustowości od poprzedniej rejestracji hello upłynął krótszy niż doba.</span><span class="sxs-lookup"><span data-stu-id="79873-140">For apps that are run frequently, more than once a day, you can probably skip registration toopreserve bandwidth if less than a day has passed since hello previous registration.</span></span>
> 
> 

1. <span data-ttu-id="79873-141">Dodaj następującego kodu na końcu hello hello hello **onCreate** metoda hello **MainActivity** klasy:</span><span class="sxs-lookup"><span data-stu-id="79873-141">Add hello following code at hello end of hello **onCreate** method in hello **MainActivity** class:</span></span>
   
        notifications.subscribeToCategories(notifications.retrieveCategories());
   
    <span data-ttu-id="79873-142">Dzięki temu że każdym uruchomieniu aplikacji hello pobiera kategorie hello z magazynu lokalnego i żąda rejestracja dla tych kategorii.</span><span class="sxs-lookup"><span data-stu-id="79873-142">This makes sure that every time hello app starts it retrieves hello categories from local storage and requests a registeration for these categories.</span></span> 
2. <span data-ttu-id="79873-143">Następnie zaktualizuj hello `onStart()` metody hello `MainActivity` klas w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="79873-143">Then update hello `onStart()` method of hello `MainActivity` class as follows:</span></span>
   
    <span data-ttu-id="79873-144">@Overridechronione {void onStart()</span><span class="sxs-lookup"><span data-stu-id="79873-144">@Override  protected void onStart() {</span></span>
   
        super.onStart();
        isVisible = true;
   
        Set<String> categories = notifications.retrieveCategories();
   
        CheckBox world = (CheckBox) findViewById(R.id.worldBox);
        world.setChecked(categories.contains("world"));
        CheckBox politics = (CheckBox) findViewById(R.id.politicsBox);
        politics.setChecked(categories.contains("politics"));
        CheckBox business = (CheckBox) findViewById(R.id.businessBox);
        business.setChecked(categories.contains("business"));
        CheckBox technology = (CheckBox) findViewById(R.id.technologyBox);
        technology.setChecked(categories.contains("technology"));
        CheckBox science = (CheckBox) findViewById(R.id.scienceBox);
        science.setChecked(categories.contains("science"));
        CheckBox sports = (CheckBox) findViewById(R.id.sportsBox);
        sports.setChecked(categories.contains("sports"));
    <span data-ttu-id="79873-145">}</span><span class="sxs-lookup"><span data-stu-id="79873-145">}</span></span>
   
    <span data-ttu-id="79873-146">Spowoduje to zaktualizowanie hello głównego działania na podstawie stanu hello zapisane wcześniej kategorii.</span><span class="sxs-lookup"><span data-stu-id="79873-146">This updates hello main activity based on hello status of previously saved categories.</span></span>

<span data-ttu-id="79873-147">Aplikacja Hello jest teraz ukończona i może przechowywać zestawu kategorii hello urządzenia magazynu lokalnego używane tooregister hello Centrum powiadomień przy każdym zmiany użytkowników hello hello wybór kategorii.</span><span class="sxs-lookup"><span data-stu-id="79873-147">hello app is now complete and can store a set of categories in hello device local storage used tooregister with hello notification hub whenever hello user changes hello selection of categories.</span></span> <span data-ttu-id="79873-148">Następnie zdefiniujemy wewnętrznej bazy danych, który może wysyłać kategorii powiadomienia toothis aplikacji.</span><span class="sxs-lookup"><span data-stu-id="79873-148">Next, we will define a backend that can send category notifications toothis app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="79873-149">Wysyłanie powiadomień oznakowany</span><span class="sxs-lookup"><span data-stu-id="79873-149">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-hello-app-and-generate-notifications"></a><span data-ttu-id="79873-150">Uruchamianie aplikacji hello i generować powiadomienia</span><span class="sxs-lookup"><span data-stu-id="79873-150">Run hello app and generate notifications</span></span>
1. <span data-ttu-id="79873-151">W programie Android Studio tworzenie aplikacji hello, a następnie uruchom go na urządzeniu lub emulatorze.</span><span class="sxs-lookup"><span data-stu-id="79873-151">In Android Studio, build hello app and start it on a device or emulator.</span></span>
   
    <span data-ttu-id="79873-152">Należy pamiętać, że przełącza, aplikacja hello, które interfejs użytkownika zawiera zestaw, który umożliwia wybranie hello toosubscribe kategorii do.</span><span class="sxs-lookup"><span data-stu-id="79873-152">Note that hello app UI provides a set of toggles that lets you choose hello categories toosubscribe to.</span></span>
2. <span data-ttu-id="79873-153">Włącz co najmniej jeden przełącza kategorie, a następnie kliknij przycisk **Subskrybuj**.</span><span class="sxs-lookup"><span data-stu-id="79873-153">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="79873-154">Aplikacja Hello konwertuje kategorii hello wybrane tagi i żąda nowej rejestracji urządzenia hello wybrane tagów z Centrum powiadomień hello.</span><span class="sxs-lookup"><span data-stu-id="79873-154">hello app converts hello selected categories into tags and requests a new device registration for hello selected tags from hello notification hub.</span></span> <span data-ttu-id="79873-155">Witaj zarejestrowanych kategorie są zwracane i wyświetlane w wyskakujące powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="79873-155">hello registered categories are returned and displayed in a toast notification.</span></span>
3. <span data-ttu-id="79873-156">Wyślij nowe powiadomienie, uruchamiając hello aplikacji konsoli .NET.</span><span class="sxs-lookup"><span data-stu-id="79873-156">Send a new notification by running hello .NET Console app.</span></span>  <span data-ttu-id="79873-157">Alternatywnie możesz wysłać oznakowanych szablonu powiadomienia za pomocą karty debugowanie hello Centrum powiadomień w hello [klasycznego portalu Azure].</span><span class="sxs-lookup"><span data-stu-id="79873-157">Alternatively, you can send tagged template notifications using hello debug tab of your notification hub in hello [Azure Classic Portal].</span></span>
   
    <span data-ttu-id="79873-158">Powiadomienia o kategoriach hello wybrane są wyświetlane jako wyskakujące powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="79873-158">Notifications for hello selected categories appear as toast notifications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="79873-159">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="79873-159">Next steps</span></span>
<span data-ttu-id="79873-160">W tym samouczku opisano sposób toobroadcast krytyczne według kategorii wiadomości.</span><span class="sxs-lookup"><span data-stu-id="79873-160">In this tutorial we learned how toobroadcast breaking news by category.</span></span> <span data-ttu-id="79873-161">Należy rozważyć wykonanie jednej hello następujące samouczki dotyczące innych zaawansowanych scenariuszy centra powiadomień:</span><span class="sxs-lookup"><span data-stu-id="79873-161">Consider completing one of hello following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="79873-162">[Użyj usługi Notification Hubs toobroadcast zlokalizowane najważniejszych wiadomości]</span><span class="sxs-lookup"><span data-stu-id="79873-162">[Use Notification Hubs toobroadcast localized breaking news]</span></span>
  
    <span data-ttu-id="79873-163">Dowiedz się, jak fundamentalne wysyłania tooenable aplikacji wiadomości powitania tooexpand zlokalizowane powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="79873-163">Learn how tooexpand hello breaking news app tooenable sending localized notifications.</span></span>

<!-- Images. -->
[A1]: ./media/notification-hubs-aspnet-backend-android-breaking-news/android-breaking-news1.PNG

<!-- URLs.-->
[get-started]: notification-hubs-android-push-notification-google-gcm-get-started.md
[Użyj usługi Notification Hubs toobroadcast zlokalizowane najważniejszych wiadomości]: /manage/services/notification-hubs/breaking-news-localized-dotnet/
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users
[Mobile Service]: /develop/mobile/tutorials/get-started/
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[klasycznego portalu Azure]: https://manage.windowsazure.com
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
