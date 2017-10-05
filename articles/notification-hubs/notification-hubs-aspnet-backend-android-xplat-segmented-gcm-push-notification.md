---
title: "Centra powiadomień fundamentalne wiadomości samouczek - Android"
description: "Dowiedz się, jak używać usługi Azure Service Bus Notification Hubs można wysłać powiadomienia o najważniejszych wiadomościach do urządzeń z systemem Android."
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
ms.openlocfilehash: 76ec01c874fceedab7d76b2ef58e4b45b5489f58
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-notification-hubs-to-send-breaking-news"></a><span data-ttu-id="b0614-103">Wysyłanie najważniejszych wiadomości przy użyciu usługi Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="b0614-103">Use Notification Hubs to send breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="b0614-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="b0614-104">Overview</span></span>
<span data-ttu-id="b0614-105">W tym temacie przedstawiono sposób użycia usługi Azure Notification Hubs wysyłać powiadomienia o najważniejszych wiadomościach do aplikacji systemu Android.</span><span class="sxs-lookup"><span data-stu-id="b0614-105">This topic shows you how to use Azure Notification Hubs to broadcast breaking news notifications to an Android app.</span></span> <span data-ttu-id="b0614-106">Po zakończeniu będzie można rejestrować zakłócenia w kategorii wiadomości i odbierać tylko powiadomienia wypychane dla tych kategorii.</span><span class="sxs-lookup"><span data-stu-id="b0614-106">When complete, you will be able to register for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="b0614-107">Ten scenariusz jest wspólnego wzorca dla wielu aplikacji, gdzie powiadomienia muszą być wysłane do grup użytkowników, które wcześniej zostały zadeklarowane zainteresowanie je, np. czytnik danych RSS, aplikacje wentylatory utworów muzycznych itp.</span><span class="sxs-lookup"><span data-stu-id="b0614-107">This scenario is a common pattern for many apps where notifications have to be sent to groups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="b0614-108">Scenariusze emisji są włączone, umieszczając w niej co najmniej jeden *tagi* podczas tworzenia rejestracji w Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="b0614-108">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in the notification hub.</span></span> <span data-ttu-id="b0614-109">Gdy powiadomienia są wysyłane do tagu, wszystkie urządzenia, które zostały zarejestrowane dla tagu będą otrzymywać powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="b0614-109">When notifications are sent to a tag, all devices that have registered for the tag will receive the notification.</span></span> <span data-ttu-id="b0614-110">Ponieważ tagi są po prostu ciągów, nie mają być przygotowana z wyprzedzeniem.</span><span class="sxs-lookup"><span data-stu-id="b0614-110">Because tags are simply strings, they do not have to be provisioned in advance.</span></span> <span data-ttu-id="b0614-111">Aby uzyskać więcej informacji na temat tagów, zapoznaj się [routingu centra powiadomień i wyrażeń tagów](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="b0614-111">For more information about tags, refer to [Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b0614-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b0614-112">Prerequisites</span></span>
<span data-ttu-id="b0614-113">W tym temacie opiera się na aplikacji utworzony w [Rozpoczynanie pracy z usługą Notification Hubs][get-started].</span><span class="sxs-lookup"><span data-stu-id="b0614-113">This topic builds on the app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="b0614-114">Przed rozpoczęciem tego samouczka należy zostały już wykonane [Rozpoczynanie pracy z usługą Notification Hubs][get-started].</span><span class="sxs-lookup"><span data-stu-id="b0614-114">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-to-the-app"></a><span data-ttu-id="b0614-115">Dodaj wybrane kategorii do aplikacji</span><span class="sxs-lookup"><span data-stu-id="b0614-115">Add category selection to the app</span></span>
<span data-ttu-id="b0614-116">Pierwszym krokiem jest dodanie elementów interfejsu użytkownika do z istniejących działanie główne, które umożliwiają użytkownikowi wybierz kategorie, aby zarejestrować.</span><span class="sxs-lookup"><span data-stu-id="b0614-116">The first step is to add the UI elements to your existing main activity that enable the user to select categories to register.</span></span> <span data-ttu-id="b0614-117">Kategorie wybrane przez użytkownika są przechowywane na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="b0614-117">The categories selected by a user are stored on the device.</span></span> <span data-ttu-id="b0614-118">Po uruchomieniu aplikacji, rejestracji urządzenia jest tworzony w Centrum powiadomień z wybranych kategorii jako znaczniki.</span><span class="sxs-lookup"><span data-stu-id="b0614-118">When the app starts, a device registration is created in your notification hub with the selected categories as tags.</span></span>

1. <span data-ttu-id="b0614-119">Otwórz plik res/layout/activity_main.xml i Zastąp zawartość z następującymi:</span><span class="sxs-lookup"><span data-stu-id="b0614-119">Open your res/layout/activity_main.xml file, and substitute the content with the following:</span></span>
   
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
2. <span data-ttu-id="b0614-120">Otwórz plik res/values/strings.xml i dodaj następujące wiersze:</span><span class="sxs-lookup"><span data-stu-id="b0614-120">Open your res/values/strings.xml file and add the following lines:</span></span>
   
        <string name="button_subscribe">Subscribe</string>
        <string name="label_world">World</string>
        <string name="label_politics">Politics</string>
        <string name="label_business">Business</string>
        <string name="label_technology">Technology</string>
        <string name="label_science">Science</string>
        <string name="label_sports">Sports</string>
   
    <span data-ttu-id="b0614-121">Układu graficznego main_activity.xml powinna wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="b0614-121">Your main_activity.xml graphical layout should now look like this:</span></span>
   
    ![][A1]
3. <span data-ttu-id="b0614-122">Teraz Utwórz klasę **powiadomienia** w pakiecie programu **MainActivity** klasy.</span><span class="sxs-lookup"><span data-stu-id="b0614-122">Now create a class **Notifications** in the same package as your **MainActivity** class.</span></span>
   
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
                            Log.e("MainActivity", "Failed to register - " + e.getMessage());
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
   
    <span data-ttu-id="b0614-123">Ta klasa używa lokalnego magazynu do przechowywania kategorii wiadomości, który to urządzenie musi odebrać.</span><span class="sxs-lookup"><span data-stu-id="b0614-123">This class uses the local storage to store the categories of news that this device has to receive.</span></span> <span data-ttu-id="b0614-124">Zawiera również metody do rejestrowania dla tych kategorii.</span><span class="sxs-lookup"><span data-stu-id="b0614-124">It also contains methods to register for these categories.</span></span>
4. <span data-ttu-id="b0614-125">W Twojej **MainActivity** klasy Usuń prywatne pól dla **NotificationHub** i **GoogleCloudMessaging**, i Dodaj pole do **powiadomienia**:</span><span class="sxs-lookup"><span data-stu-id="b0614-125">In your **MainActivity** class remove your private fields for **NotificationHub** and **GoogleCloudMessaging**, and add a field for **Notifications**:</span></span>
   
        // private GoogleCloudMessaging gcm;
        // private NotificationHub hub;
        private Notifications notifications;
5. <span data-ttu-id="b0614-126">Następnie w **onCreate** metody, Usuń inicjowanie **Centrum** pola i **registerWithNotificationHubs** metody.</span><span class="sxs-lookup"><span data-stu-id="b0614-126">Then, in the **onCreate** method, remove the initialization of the **hub** field and the **registerWithNotificationHubs** method.</span></span> <span data-ttu-id="b0614-127">Następnie dodaj następujące wiersze, które inicjuje wystąpienie klasy **powiadomienia** klasy.</span><span class="sxs-lookup"><span data-stu-id="b0614-127">Then add the following lines which initialize an instance of the **Notifications** class.</span></span> 

        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
            MyHandler.mainActivity = this;

            NotificationsManager.handleNotifications(this, SENDER_ID,
                    MyHandler.class);

            notifications = new Notifications(this, SENDER_ID, HubName, HubListenConnectionString);

            notifications.subscribeToCategories(notifications.retrieveCategories());
        }

    <span data-ttu-id="b0614-128">`HubName`i `HubListenConnectionString` już powinien być ustawiony z `<hub name>` i `<connection string with listen access>` symbole zastępcze nazwą Centrum powiadomień i parametry połączenia dla *DefaultListenSharedAccessSignature* uzyskany wcześniej.</span><span class="sxs-lookup"><span data-stu-id="b0614-128">`HubName` and `HubListenConnectionString` should already be set with the `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and the connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>

    > [AZURE.NOTE] <span data-ttu-id="b0614-129">Ponieważ poświadczenia, które są dystrybuowane wraz z aplikacji przez klienta nie są zazwyczaj bezpieczna, klucz dostępu do nasłuchiwania należy dystrybuować tylko z aplikacji klienta.</span><span class="sxs-lookup"><span data-stu-id="b0614-129">Because credentials that are distributed with a client app are not generally secure, you should only distribute the key for listen access with your client app.</span></span> <span data-ttu-id="b0614-130">Nasłuchiwanie umożliwia dostęp, nie można zmodyfikować aplikację, aby zarejestrować dla powiadomień, ale istniejące rejestracje i nie mogą być wysyłane powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="b0614-130">Listen access enables your app to register for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="b0614-131">Klucz pełny dostęp jest używany w usłudze zabezpieczonych wewnętrznej bazy danych do wysyłania powiadomień i zmianę istniejącego rejestracji.</span><span class="sxs-lookup"><span data-stu-id="b0614-131">The full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>


1. <span data-ttu-id="b0614-132">Następnie dodaj następujące instrukcje importu i `subscribe` można obsłużyć przycisk Subskrybuj kliknij zdarzenie:</span><span class="sxs-lookup"><span data-stu-id="b0614-132">Then, add the following imports and `subscribe` method to handle the subscribe button click event:</span></span>
   
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
   
    <span data-ttu-id="b0614-133">Ta metoda tworzy listę kategorii i używa **powiadomienia** klasy przechowywania listy w magazynie lokalnym i rejestracji, odpowiednie znaczniki w Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="b0614-133">This method creates a list of categories and uses the **Notifications** class to store the list in the local storage and register the corresponding tags with your notification hub.</span></span> <span data-ttu-id="b0614-134">Zmiana kategorii rejestracji zostaje odtworzone w nowej kategorii.</span><span class="sxs-lookup"><span data-stu-id="b0614-134">When categories are changed, the registration is recreated with the new categories.</span></span>

<span data-ttu-id="b0614-135">Aplikacja jest teraz możliwość przechowywania zestawu kategorii w lokalnej pamięci masowej na urządzeniu i Zarejestruj w Centrum powiadomień, zawsze, gdy użytkownik zmieni się zaznaczenie kategorii.</span><span class="sxs-lookup"><span data-stu-id="b0614-135">Your app is now able to store a set of categories in local storage on the device and register with the notification hub whenever the user changes the selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="b0614-136">Rejestrowanie się w celu powiadomienia</span><span class="sxs-lookup"><span data-stu-id="b0614-136">Register for notifications</span></span>
<span data-ttu-id="b0614-137">Następujące kroki, zarejestruj się w Centrum powiadomień przy uruchamianiu przy użyciu kategorii, które były przechowywane w magazynie lokalnym.</span><span class="sxs-lookup"><span data-stu-id="b0614-137">These steps register with the notification hub on startup using the categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="b0614-138">Ponieważ registrationId przypisane przez Google Cloud Messaging (GCM) można zmienić w dowolnym momencie, należy zarejestrować powiadomień często uniknąć niepowodzeń powiadomień.</span><span class="sxs-lookup"><span data-stu-id="b0614-138">Because the registrationId assigned by Google Cloud Messaging (GCM) can change at any time, you should register for notifications frequently to avoid notification failures.</span></span> <span data-ttu-id="b0614-139">W tym przykładzie rejestruje powiadomienia każdym uruchomieniu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b0614-139">This example registers for notification every time that the app starts.</span></span> <span data-ttu-id="b0614-140">Dla aplikacji, które są uruchamiane często więcej niż raz dziennie, można prawdopodobnie pominąć rejestrację, aby zachować przepustowość, jeśli krótszy niż doba upłynął od czasu poprzedniej rejestracji.</span><span class="sxs-lookup"><span data-stu-id="b0614-140">For apps that are run frequently, more than once a day, you can probably skip registration to preserve bandwidth if less than a day has passed since the previous registration.</span></span>
> 
> 

1. <span data-ttu-id="b0614-141">Dodaj następujący kod na końcu **onCreate** metody w **MainActivity** klasy:</span><span class="sxs-lookup"><span data-stu-id="b0614-141">Add the following code at the end of the **onCreate** method in the **MainActivity** class:</span></span>
   
        notifications.subscribeToCategories(notifications.retrieveCategories());
   
    <span data-ttu-id="b0614-142">Dzięki temu przy każdym uruchomieniu aplikacji it pobiera kategorie z magazynu lokalnego i żąda rejestracja dla tych kategorii.</span><span class="sxs-lookup"><span data-stu-id="b0614-142">This makes sure that every time the app starts it retrieves the categories from local storage and requests a registeration for these categories.</span></span> 
2. <span data-ttu-id="b0614-143">Następnie zaktualizuj `onStart()` metody `MainActivity` klas w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="b0614-143">Then update the `onStart()` method of the `MainActivity` class as follows:</span></span>
   
    <span data-ttu-id="b0614-144">@Overridechronione {void onStart()</span><span class="sxs-lookup"><span data-stu-id="b0614-144">@Override  protected void onStart() {</span></span>
   
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
    <span data-ttu-id="b0614-145">}</span><span class="sxs-lookup"><span data-stu-id="b0614-145">}</span></span>
   
    <span data-ttu-id="b0614-146">Spowoduje to zaktualizowanie głównego działania na podstawie kategorii uprzednio zapisanego stanu.</span><span class="sxs-lookup"><span data-stu-id="b0614-146">This updates the main activity based on the status of previously saved categories.</span></span>

<span data-ttu-id="b0614-147">Aplikacja jest teraz ukończona i może przechowywać zestawu kategorii w magazynie lokalnym urządzenia używane do rejestrowania w Centrum powiadomień, zawsze, gdy użytkownik zmieni się zaznaczenie kategorii.</span><span class="sxs-lookup"><span data-stu-id="b0614-147">The app is now complete and can store a set of categories in the device local storage used to register with the notification hub whenever the user changes the selection of categories.</span></span> <span data-ttu-id="b0614-148">Następnie zdefiniujemy wewnętrznej bazy danych, który może wysyłać powiadomienia kategorii do tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b0614-148">Next, we will define a backend that can send category notifications to this app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="b0614-149">Wysyłanie powiadomień oznakowany</span><span class="sxs-lookup"><span data-stu-id="b0614-149">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-the-app-and-generate-notifications"></a><span data-ttu-id="b0614-150">Uruchom aplikację i generować powiadomienia</span><span class="sxs-lookup"><span data-stu-id="b0614-150">Run the app and generate notifications</span></span>
1. <span data-ttu-id="b0614-151">W programie Android Studio kompilowania aplikacji, a następnie uruchom go na urządzeniu lub emulatorze.</span><span class="sxs-lookup"><span data-stu-id="b0614-151">In Android Studio, build the app and start it on a device or emulator.</span></span>
   
    <span data-ttu-id="b0614-152">Należy pamiętać, że aplikacja interfejsu użytkownika zawiera zestaw przełącza umożliwiające wybierz kategorie, aby subskrybować.</span><span class="sxs-lookup"><span data-stu-id="b0614-152">Note that the app UI provides a set of toggles that lets you choose the categories to subscribe to.</span></span>
2. <span data-ttu-id="b0614-153">Włącz co najmniej jeden przełącza kategorie, a następnie kliknij przycisk **Subskrybuj**.</span><span class="sxs-lookup"><span data-stu-id="b0614-153">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="b0614-154">Konwertuje wybranych kategorii do tagów i żąda nowej rejestracji urządzeń dla wybranych tagów z Centrum powiadomień aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b0614-154">The app converts the selected categories into tags and requests a new device registration for the selected tags from the notification hub.</span></span> <span data-ttu-id="b0614-155">Zarejestrowany kategorie są zwracane i wyświetlane w wyskakujące powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="b0614-155">The registered categories are returned and displayed in a toast notification.</span></span>
3. <span data-ttu-id="b0614-156">Wyślij nowe powiadomienie za pomocą aplikacji konsoli .NET.</span><span class="sxs-lookup"><span data-stu-id="b0614-156">Send a new notification by running the .NET Console app.</span></span>  <span data-ttu-id="b0614-157">Alternatywnie możesz wysłać oznakowanych szablonu powiadomienia za pomocą karty debugowanie w Centrum powiadomień [klasycznego portalu Azure].</span><span class="sxs-lookup"><span data-stu-id="b0614-157">Alternatively, you can send tagged template notifications using the debug tab of your notification hub in the [Azure Classic Portal].</span></span>
   
    <span data-ttu-id="b0614-158">Powiadomienia dotyczące wybranych kategorii są wyświetlane jako wyskakujące powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="b0614-158">Notifications for the selected categories appear as toast notifications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b0614-159">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b0614-159">Next steps</span></span>
<span data-ttu-id="b0614-160">W tym samouczku opisano sposób emisji najważniejszych wiadomości według kategorii.</span><span class="sxs-lookup"><span data-stu-id="b0614-160">In this tutorial we learned how to broadcast breaking news by category.</span></span> <span data-ttu-id="b0614-161">Należy rozważyć wykonanie jednej z następujących samouczków, w których są wyróżniane innych zaawansowanych scenariuszy centra powiadomień:</span><span class="sxs-lookup"><span data-stu-id="b0614-161">Consider completing one of the following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="b0614-162">[Emisji zlokalizowanych najważniejszych wiadomości przy użyciu usługi Notification Hubs]</span><span class="sxs-lookup"><span data-stu-id="b0614-162">[Use Notification Hubs to broadcast localized breaking news]</span></span>
  
    <span data-ttu-id="b0614-163">Dowiedz się, jak rozszerzyć aplikację wiadomości podziału, aby umożliwić wysyłanie powiadomień zlokalizowane.</span><span class="sxs-lookup"><span data-stu-id="b0614-163">Learn how to expand the breaking news app to enable sending localized notifications.</span></span>

<!-- Images. -->
[A1]: ./media/notification-hubs-aspnet-backend-android-breaking-news/android-breaking-news1.PNG

<!-- URLs.-->
[get-started]: notification-hubs-android-push-notification-google-gcm-get-started.md
<span data-ttu-id="b0614-164">[Emisji zlokalizowanych najważniejszych wiadomości przy użyciu usługi Notification Hubs]: /manage/services/notification-hubs/breaking-news-localized-dotnet/</span><span class="sxs-lookup"><span data-stu-id="b0614-164">[Use Notification Hubs to broadcast localized breaking news]: /manage/services/notification-hubs/breaking-news-localized-dotnet/</span></span>
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users
[Mobile Service]: /develop/mobile/tutorials/get-started/
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-To for Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
<span data-ttu-id="b0614-165">[klasycznego portalu Azure]: https://manage.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="b0614-165">[Azure Classic Portal]: https://manage.windowsazure.com</span></span>
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
