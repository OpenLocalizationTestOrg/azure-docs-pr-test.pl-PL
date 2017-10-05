---
title: "Wysyłanie powiadomień wypychanych bezpiecznego przy użyciu usługi Azure Notification Hubs"
description: "Dowiedz się, jak wysyłać powiadomienia wypychane bezpieczny do aplikacji systemu Android na platformie Azure. Przykłady kodu napisane w języku Java i C#."
documentationcenter: android
keywords: "Wypychanie powiadomień, powiadomienia wypychane push wiadomości, powiadomień wypychanych systemu android"
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: daf3de1c-f6a9-43c4-8165-a76bfaa70893
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: android
ms.devlang: java
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 29f8c516e611c13fb73c7edc15e7c52708c75bb0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="sending-secure-push-notifications-with-azure-notification-hubs"></a><span data-ttu-id="97ccd-105">Wysyłanie powiadomień wypychanych bezpiecznego przy użyciu usługi Azure Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="97ccd-105">Sending Secure Push Notifications with Azure Notification Hubs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="97ccd-106">Aplikacje uniwersalne systemu Windows</span><span class="sxs-lookup"><span data-stu-id="97ccd-106">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="97ccd-107">iOS</span><span class="sxs-lookup"><span data-stu-id="97ccd-107">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="97ccd-108">Android</span><span class="sxs-lookup"><span data-stu-id="97ccd-108">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="97ccd-109">Omówienie</span><span class="sxs-lookup"><span data-stu-id="97ccd-109">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="97ccd-110">Do wykonania kroków tego samouczka potrzebne jest aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="97ccd-110">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="97ccd-111">Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="97ccd-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="97ccd-112">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="97ccd-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="97ccd-113">Obsługa powiadomień wypychanych w Microsoft Azure pozwala uzyskać dostęp, łatwy w użyciu multiplatform, infrastruktury wiadomości wypychanych skalowanej, co znacznie upraszcza implementację powiadomień wypychanych zarówno konsumenckie i korporacyjne aplikacji dla systemu platformy urządzeń przenośnych.</span><span class="sxs-lookup"><span data-stu-id="97ccd-113">Push notification support in Microsoft Azure enables you to access an easy-to-use, multiplatform, scaled-out push message infrastructure, which greatly simplifies the implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="97ccd-114">Z powodu przepisami ograniczeń dotyczących zabezpieczeń, czasami aplikacji może mają zostać uwzględnione coś w powiadomienie, które nie są przesyłane za pośrednictwem infrastruktury powiadomień wypychanych standardowa.</span><span class="sxs-lookup"><span data-stu-id="97ccd-114">Due to regulatory or security constraints, sometimes an application might want to include something in the notification that cannot be transmitted through the standard push notification infrastructure.</span></span> <span data-ttu-id="97ccd-115">Ten przewodnik opisuje sposób do osiągnięcia w tym samym środowisku, wysyłając informacje poufne za pośrednictwem uwierzytelnionego bezpiecznego połączenia między urządzeniem z systemem Android klienta i zaplecza aplikacji.</span><span class="sxs-lookup"><span data-stu-id="97ccd-115">This tutorial describes how to achieve the same experience by sending sensitive information through a secure, authenticated connection between the client Android device and the app backend.</span></span>

<span data-ttu-id="97ccd-116">Na wysokim poziomie przepływ wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="97ccd-116">At a high level, the flow is as follows:</span></span>

1. <span data-ttu-id="97ccd-117">Zaplecza aplikacji:</span><span class="sxs-lookup"><span data-stu-id="97ccd-117">The app back-end:</span></span>
   * <span data-ttu-id="97ccd-118">Magazyny bezpiecznego ładunku w wewnętrznej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="97ccd-118">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="97ccd-119">Wysyła identyfikator tego powiadomienia na urządzeniu z systemem Android (nie informacji o są wysyłane).</span><span class="sxs-lookup"><span data-stu-id="97ccd-119">Sends the ID of this notification to the Android device (no secure information is sent).</span></span>
2. <span data-ttu-id="97ccd-120">Aplikacją na urządzeniu, podczas odbierania powiadomienia:</span><span class="sxs-lookup"><span data-stu-id="97ccd-120">The app on the device, when receiving the notification:</span></span>
   * <span data-ttu-id="97ccd-121">Urządzenie z systemem Android kontaktuje się z zaplecza żąda bezpiecznego ładunku.</span><span class="sxs-lookup"><span data-stu-id="97ccd-121">The Android device contacts the back-end requesting the secure payload.</span></span>
   * <span data-ttu-id="97ccd-122">Aplikację można wyświetlić ładunku jako powiadomienie na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="97ccd-122">The app can show the payload as a notification on the device.</span></span>

<span data-ttu-id="97ccd-123">Należy pamiętać, że w poprzednim przepływu (i w tym samouczku) przyjęto założenie, że urządzenia są przechowywane token uwierzytelniania w magazynie lokalnym, po zalogowaniu się użytkownika.</span><span class="sxs-lookup"><span data-stu-id="97ccd-123">It is important to note that in the preceding flow (and in this tutorial), we assume that the device stores an authentication token in local storage, after the user logs in.</span></span> <span data-ttu-id="97ccd-124">Gwarantuje to całkowicie nie zakłóca pracy, jak urządzenia mogą pobierać ładunku bezpiecznego powiadomienia za pomocą tego tokenu.</span><span class="sxs-lookup"><span data-stu-id="97ccd-124">This guarantees a completely seamless experience, as the device can retrieve the notification’s secure payload using this token.</span></span> <span data-ttu-id="97ccd-125">Jeśli aplikacja nie przechowuje tokeny uwierzytelniania na urządzeniu lub tokeny te mogą wygasnąć, aplikacji urządzenia, po otrzymaniu powiadomienia wypychane powinien być wyświetlany ogólny powiadomienie monitowania użytkownika do uruchomienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="97ccd-125">If your application does not store authentication tokens on the device, or if these tokens can be expired, the device app, upon receiving the push notification should display a generic notification prompting the user to launch the app.</span></span> <span data-ttu-id="97ccd-126">Następnie aplikacja uwierzytelnia użytkownika i zawiera ładunek powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="97ccd-126">The app then authenticates the user and shows the notification payload.</span></span>

<span data-ttu-id="97ccd-127">Ten samouczek pokazuje, jak wysyłać powiadomienia wypychane bezpieczne.</span><span class="sxs-lookup"><span data-stu-id="97ccd-127">This tutorial shows how to send secure push notifications.</span></span> <span data-ttu-id="97ccd-128">Opiera się na [Powiadom użytkowników](notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md) samouczku, dlatego należy wykonać kroki opisane w tym samouczku najpierw Jeśli jeszcze.</span><span class="sxs-lookup"><span data-stu-id="97ccd-128">It builds on the [Notify Users](notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md) tutorial, so you should complete the steps in that tutorial first if you haven't already.</span></span>

> [!NOTE]
> <span data-ttu-id="97ccd-129">Ten samouczek zakłada, że utworzony i skonfigurowany Centrum powiadomień, zgodnie z opisem w [wprowadzenie do korzystania z usługi Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="97ccd-129">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-the-android-project"></a><span data-ttu-id="97ccd-130">Modyfikowanie projektu dla systemu Android</span><span class="sxs-lookup"><span data-stu-id="97ccd-130">Modify the Android project</span></span>
<span data-ttu-id="97ccd-131">Teraz, aby modyfikować Twojej aplikacji zaplecza wysłać tylko *identyfikator* powiadomienia wypychane, należy zmienić aplikacji systemu Android w celu obsługi tego powiadomienia i wywołania zwrotnego z zaplecza można pobrać zabezpieczoną wiadomość, który będzie wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="97ccd-131">Now that you modified your app back-end to send just the *id* of a push notification, you have to change your Android app to handle that notification and call back your back-end to retrieve the secure message to be displayed.</span></span>
<span data-ttu-id="97ccd-132">Na osiągnięcie tego celu, należy upewnić się, że aplikacji systemu Android potrafi do samodzielnego uwierzytelnienia z poziomu zaplecza, gdy odbiera powiadomienia wypychane.</span><span class="sxs-lookup"><span data-stu-id="97ccd-132">To achieve this goal, you have to make sure that your Android app knows how to authenticate itself with your back-end when it receives the push notifications.</span></span>

<span data-ttu-id="97ccd-133">Firma Microsoft będzie teraz zmodyfikować *logowania* przepływu, aby zapisać wartości nagłówka uwierzytelniania w udostępnionych preferencji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="97ccd-133">We will now modify the *login* flow in order to save the authentication header value in the shared preferences of your app.</span></span> <span data-ttu-id="97ccd-134">Mechanizmy analogiczne może służyć do przechowywania wszelkich token uwierzytelniania (np. tokenów OAuth), który aplikacji będą musieli używać bez konieczności wprowadzania poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="97ccd-134">Analogous mechanisms can be used to store any authentication token (e.g. OAuth tokens) that the app will have to use without requiring user credentials.</span></span>

1. <span data-ttu-id="97ccd-135">W projekcie aplikacji systemu Android, Dodaj następujące ograniczenia w górnej części **MainActivity** klasy:</span><span class="sxs-lookup"><span data-stu-id="97ccd-135">In your Android app project, add the following constants at the top of the **MainActivity** class:</span></span>
   
        public static final String NOTIFY_USERS_PROPERTIES = "NotifyUsersProperties";
        public static final String AUTHORIZATION_HEADER_PROPERTY = "AuthorizationHeader";
2. <span data-ttu-id="97ccd-136">Nadal **MainActivity** klasy, zaktualizuj `getAuthorizationHeader()` metoda zawiera następujący kod:</span><span class="sxs-lookup"><span data-stu-id="97ccd-136">Still in the **MainActivity** class, update the `getAuthorizationHeader()` method to contain the following code:</span></span>
   
        private String getAuthorizationHeader() throws UnsupportedEncodingException {
            EditText username = (EditText) findViewById(R.id.usernameText);
            EditText password = (EditText) findViewById(R.id.passwordText);
            String basicAuthHeader = username.getText().toString()+":"+password.getText().toString();
            basicAuthHeader = Base64.encodeToString(basicAuthHeader.getBytes("UTF-8"), Base64.NO_WRAP);
   
            SharedPreferences sp = getSharedPreferences(NOTIFY_USERS_PROPERTIES, Context.MODE_PRIVATE);
            sp.edit().putString(AUTHORIZATION_HEADER_PROPERTY, basicAuthHeader).commit();
   
            return basicAuthHeader;
        }
3. <span data-ttu-id="97ccd-137">Dodaj następujące `import` instrukcje w górnej części **MainActivity** pliku:</span><span class="sxs-lookup"><span data-stu-id="97ccd-137">Add the following `import` statements at the top of the **MainActivity** file:</span></span>
   
        import android.content.SharedPreferences;

<span data-ttu-id="97ccd-138">Teraz zostanie zmieniona obsługi, które jest wywoływane w przypadku otrzymania powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="97ccd-138">Now we will change the handler that is called when the notification is received.</span></span>

1. <span data-ttu-id="97ccd-139">W **MyHandler** klasy zmiany `OnReceive()` metoda zawiera:</span><span class="sxs-lookup"><span data-stu-id="97ccd-139">In the **MyHandler** class change the `OnReceive()` method to contain:</span></span>
   
        public void onReceive(Context context, Bundle bundle) {
            ctx = context;
            String secureMessageId = bundle.getString("secureId");
            retrieveNotification(secureMessageId);
        }
2. <span data-ttu-id="97ccd-140">Następnie dodaj `retrieveNotification()` metoda zastępuje symbol zastępczy `{back-end endpoint}` z punktem końcowym zaplecza uzyskane podczas wdrażania sieci wewnętrznej:</span><span class="sxs-lookup"><span data-stu-id="97ccd-140">Then add the `retrieveNotification()` method, replacing the placeholder `{back-end endpoint}` with the back-end endpoint obtained while deploying your back-end:</span></span>
   
        private void retrieveNotification(final String secureMessageId) {
            SharedPreferences sp = ctx.getSharedPreferences(MainActivity.NOTIFY_USERS_PROPERTIES, Context.MODE_PRIVATE);
            final String authorizationHeader = sp.getString(MainActivity.AUTHORIZATION_HEADER_PROPERTY, null);
   
            new AsyncTask<Object, Object, Object>() {
                @Override
                protected Object doInBackground(Object... params) {
                    try {
                        HttpUriRequest request = new HttpGet("{back-end endpoint}/api/notifications/"+secureMessageId);
                        request.addHeader("Authorization", "Basic "+authorizationHeader);
                        HttpResponse response = new DefaultHttpClient().execute(request);
                        if (response.getStatusLine().getStatusCode() != HttpStatus.SC_OK) {
                            Log.e("MainActivity", "Error retrieving secure notification" + response.getStatusLine().getStatusCode());
                            throw new RuntimeException("Error retrieving secure notification");
                        }
                        String secureNotificationJSON = EntityUtils.toString(response.getEntity());
                        JSONObject secureNotification = new JSONObject(secureNotificationJSON);
                        sendNotification(secureNotification.getString("Payload"));
                    } catch (Exception e) {
                        Log.e("MainActivity", "Failed to retrieve secure notification - " + e.getMessage());
                        return e;
                    }
                    return null;
                }
            }.execute(null, null, null);
        }

<span data-ttu-id="97ccd-141">Ta metoda wywołuje Twojej aplikacji zaplecza do pobierania zawartości powiadomienia przy użyciu poświadczeń przechowywanych w udostępnionych preferencji i wyświetla je jako normalne powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="97ccd-141">This method calls your app back-end to retrieve the notification content using the credentials stored in the shared preferences and displays it as a normal notification.</span></span> <span data-ttu-id="97ccd-142">Wygląda powiadomienie dla użytkownika aplikacji, dokładnie tak samo jak inne powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="97ccd-142">The notification looks to the app user exactly like any other push notification.</span></span>

<span data-ttu-id="97ccd-143">Należy pamiętać, że preferowane do obsługi przypadków brakujących właściwości nagłówka uwierzytelniania lub odrzucenia przez zaplecza.</span><span class="sxs-lookup"><span data-stu-id="97ccd-143">Note that it is preferable to handle the cases of missing authentication header property or rejection by the back-end.</span></span> <span data-ttu-id="97ccd-144">Obsługę określonych przypadkach zależą od większości użytkowników docelowych.</span><span class="sxs-lookup"><span data-stu-id="97ccd-144">The specific handling of these cases depend mostly on your target user experience.</span></span> <span data-ttu-id="97ccd-145">Jedną z opcji jest powiadomienia z monitem ogólnego dla użytkownika do uwierzytelniania można pobrać rzeczywiste powiadomienia mają być wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="97ccd-145">One option is to display a notification with a generic prompt for the user to authenticate to retrieve the actual notification.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="97ccd-146">Uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="97ccd-146">Run the Application</span></span>
<span data-ttu-id="97ccd-147">Aby uruchomić aplikację, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="97ccd-147">To run the application, do the following:</span></span>

1. <span data-ttu-id="97ccd-148">Upewnij się, że **AppBackend** jest wdrożona na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="97ccd-148">Make sure **AppBackend** is deployed in Azure.</span></span> <span data-ttu-id="97ccd-149">Jeśli używasz programu Visual Studio, uruchom **AppBackend** aplikacji interfejsu API sieci Web.</span><span class="sxs-lookup"><span data-stu-id="97ccd-149">If using Visual Studio, run the **AppBackend** Web API application.</span></span> <span data-ttu-id="97ccd-150">Zostanie wyświetlona strona sieci web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="97ccd-150">An ASP.NET web page is displayed.</span></span>
2. <span data-ttu-id="97ccd-151">W środowisku Eclipse Uruchom aplikację na fizyczne urządzenie z systemem Android lub emulator.</span><span class="sxs-lookup"><span data-stu-id="97ccd-151">In Eclipse, run the app on a physical Android device or the emulator.</span></span>
3. <span data-ttu-id="97ccd-152">W aplikacji systemu Android interfejsu użytkownika wprowadź nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="97ccd-152">In the Android app UI, enter a username and password.</span></span> <span data-ttu-id="97ccd-153">Mogą to być dowolny ciąg, ale muszą one mieć taką samą wartość.</span><span class="sxs-lookup"><span data-stu-id="97ccd-153">These can be any string, but they must be the same value.</span></span>
4. <span data-ttu-id="97ccd-154">W aplikacji systemu Android interfejsu użytkownika, kliknij przycisk **Zaloguj**.</span><span class="sxs-lookup"><span data-stu-id="97ccd-154">In the Android app UI, click **Log in**.</span></span> <span data-ttu-id="97ccd-155">Następnie kliknij przycisk **wysyłania wypychania**.</span><span class="sxs-lookup"><span data-stu-id="97ccd-155">Then click **Send push**.</span></span>

