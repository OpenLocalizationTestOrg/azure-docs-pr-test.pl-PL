---
title: "aaaSending Secure powiadomień wypychanych przy użyciu usługi Azure Notification Hubs"
description: "Dowiedz się, jak bezpieczne toosend push aplikacji systemu Android tooan powiadomienia z platformy Azure. Przykłady kodu napisane w języku Java i C#."
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
ms.openlocfilehash: d07943c4691ed07acb987086228ef565e6281d57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sending-secure-push-notifications-with-azure-notification-hubs"></a><span data-ttu-id="6e9fd-105">Wysyłanie powiadomień wypychanych bezpiecznego przy użyciu usługi Azure Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="6e9fd-105">Sending Secure Push Notifications with Azure Notification Hubs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6e9fd-106">Aplikacje uniwersalne systemu Windows</span><span class="sxs-lookup"><span data-stu-id="6e9fd-106">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="6e9fd-107">iOS</span><span class="sxs-lookup"><span data-stu-id="6e9fd-107">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="6e9fd-108">Android</span><span class="sxs-lookup"><span data-stu-id="6e9fd-108">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="6e9fd-109">Omówienie</span><span class="sxs-lookup"><span data-stu-id="6e9fd-109">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6e9fd-110">toocomplete tego samouczka, musi mieć aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6e9fd-110">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="6e9fd-111">Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="6e9fd-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="6e9fd-112">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="6e9fd-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="6e9fd-113">Obsługa powiadomień wypychanych w Microsoft Azure umożliwia tooaccess infrastruktury wiadomości wypychanych łatwy w użyciu, wieloplatformową skalowalnych w poziomie, który jest znacznie ułatwione hello stosowania powiadomienia wypychane dla aplikacji zarówno konsumenckie i korporacyjne dla platformy urządzeń przenośnych.</span><span class="sxs-lookup"><span data-stu-id="6e9fd-113">Push notification support in Microsoft Azure enables you tooaccess an easy-to-use, multiplatform, scaled-out push message infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="6e9fd-114">Czasami ze względu na ograniczenia tooregulatory lub zabezpieczeń, aplikacja może być tooinclude coś w hello powiadomienie, które nie są przesyłane za pośrednictwem infrastruktury powiadomień wypychanych standardowe hello.</span><span class="sxs-lookup"><span data-stu-id="6e9fd-114">Due tooregulatory or security constraints, sometimes an application might want tooinclude something in hello notification that cannot be transmitted through hello standard push notification infrastructure.</span></span> <span data-ttu-id="6e9fd-115">W tym samouczku opisano, jak tooachieve hello tego samego środowiska poprzez wysłanie poufnych informacji za pośrednictwem uwierzytelnionego bezpiecznego połączenia między urządzenia Android powitania klienta i zaplecza aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="6e9fd-115">This tutorial describes how tooachieve hello same experience by sending sensitive information through a secure, authenticated connection between hello client Android device and hello app backend.</span></span>

<span data-ttu-id="6e9fd-116">Na wysokim poziomie przepływu hello jest następujący:</span><span class="sxs-lookup"><span data-stu-id="6e9fd-116">At a high level, hello flow is as follows:</span></span>

1. <span data-ttu-id="6e9fd-117">Witaj zaplecze aplikacji:</span><span class="sxs-lookup"><span data-stu-id="6e9fd-117">hello app back-end:</span></span>
   * <span data-ttu-id="6e9fd-118">Magazyny bezpiecznego ładunku w wewnętrznej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="6e9fd-118">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="6e9fd-119">Wysyła identyfikator hello tego powiadomienia toohello urządzenia z systemem Android (nie informacji o są wysyłane).</span><span class="sxs-lookup"><span data-stu-id="6e9fd-119">Sends hello ID of this notification toohello Android device (no secure information is sent).</span></span>
2. <span data-ttu-id="6e9fd-120">Aplikacja Hello na urządzeniu hello podczas odbierania powiadomień hello:</span><span class="sxs-lookup"><span data-stu-id="6e9fd-120">hello app on hello device, when receiving hello notification:</span></span>
   * <span data-ttu-id="6e9fd-121">urządzenia z systemem Android Hello kontaktuje się hello zaplecza żądania hello bezpiecznego ładunku.</span><span class="sxs-lookup"><span data-stu-id="6e9fd-121">hello Android device contacts hello back-end requesting hello secure payload.</span></span>
   * <span data-ttu-id="6e9fd-122">Aplikacja Hello można wyświetlić ładunku hello jako powiadomienie na urządzeniu hello.</span><span class="sxs-lookup"><span data-stu-id="6e9fd-122">hello app can show hello payload as a notification on hello device.</span></span>

<span data-ttu-id="6e9fd-123">Jest ważne toonote, że w hello poprzedzających przepływu (i w tym samouczku) przyjęto założenie, urządzenia hello po zalogowaniu użytkownika hello przechowuje token uwierzytelniania w magazynie lokalnym.</span><span class="sxs-lookup"><span data-stu-id="6e9fd-123">It is important toonote that in hello preceding flow (and in this tutorial), we assume that hello device stores an authentication token in local storage, after hello user logs in.</span></span> <span data-ttu-id="6e9fd-124">Gwarantuje to całkowicie sprawnie, jak urządzenia hello mogą pobierać ładunku bezpiecznego hello powiadomienia za pomocą tego tokenu.</span><span class="sxs-lookup"><span data-stu-id="6e9fd-124">This guarantees a completely seamless experience, as hello device can retrieve hello notification’s secure payload using this token.</span></span> <span data-ttu-id="6e9fd-125">Jeśli aplikacja nie przechowuje tokeny uwierzytelniania na urządzeniu hello lub tokeny te mogą wygasnąć, hello aplikacji urządzenia, po otrzymaniu powiadomienia wypychane hello powinien być wyświetlany ogólny powiadomienie aplikacji hello toolaunch użytkownika hello monitowania.</span><span class="sxs-lookup"><span data-stu-id="6e9fd-125">If your application does not store authentication tokens on hello device, or if these tokens can be expired, hello device app, upon receiving hello push notification should display a generic notification prompting hello user toolaunch hello app.</span></span> <span data-ttu-id="6e9fd-126">Aplikacja Hello następnie uwierzytelnia użytkownika hello i zawiera ładunek powiadomienia hello.</span><span class="sxs-lookup"><span data-stu-id="6e9fd-126">hello app then authenticates hello user and shows hello notification payload.</span></span>

<span data-ttu-id="6e9fd-127">Ten samouczek pokazuje, jak toosend bezpieczne powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="6e9fd-127">This tutorial shows how toosend secure push notifications.</span></span> <span data-ttu-id="6e9fd-128">Opiera się na powitania [Powiadom użytkowników](notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md) samouczku, dlatego należy wykonać kroki hello w tym samouczku najpierw Jeśli jeszcze.</span><span class="sxs-lookup"><span data-stu-id="6e9fd-128">It builds on hello [Notify Users](notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md) tutorial, so you should complete hello steps in that tutorial first if you haven't already.</span></span>

> [!NOTE]
> <span data-ttu-id="6e9fd-129">Ten samouczek zakłada, że utworzony i skonfigurowany Centrum powiadomień, zgodnie z opisem w [wprowadzenie do korzystania z usługi Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6e9fd-129">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-android-project"></a><span data-ttu-id="6e9fd-130">Modyfikowanie hello projekt systemu Android</span><span class="sxs-lookup"><span data-stu-id="6e9fd-130">Modify hello Android project</span></span>
<span data-ttu-id="6e9fd-131">Teraz, aby modyfikować tylko aplikacji hello w toosend zaplecza *identyfikator* powiadomienia wypychane, masz toochange Twojego toohandle aplikacji systemu Android, że powiadomienia i wywołania zwrotne Twojej hello tooretrieve zaplecza secure toobe komunikat wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="6e9fd-131">Now that you modified your app back-end toosend just hello *id* of a push notification, you have toochange your Android app toohandle that notification and call back your back-end tooretrieve hello secure message toobe displayed.</span></span>
<span data-ttu-id="6e9fd-132">tooachieve ten cel ma toomake się upewnić, że aplikacji systemu Android wie jak tooauthenticate się z poziomu zaplecza, gdy odbiera powiadomienia wypychane hello.</span><span class="sxs-lookup"><span data-stu-id="6e9fd-132">tooachieve this goal, you have toomake sure that your Android app knows how tooauthenticate itself with your back-end when it receives hello push notifications.</span></span>

<span data-ttu-id="6e9fd-133">Firma Microsoft będzie teraz zmodyfikować hello *logowania* przepływu w kolejności toosave hello wartości nagłówka uwierzytelniania w hello udostępnionych preferencji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6e9fd-133">We will now modify hello *login* flow in order toosave hello authentication header value in hello shared preferences of your app.</span></span> <span data-ttu-id="6e9fd-134">Mechanizmy analogiczne mogą być używane toostore żadnych token uwierzytelniania (np. tokenów OAuth), który aplikacja hello ma toouse bez konieczności wprowadzania poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6e9fd-134">Analogous mechanisms can be used toostore any authentication token (e.g. OAuth tokens) that hello app will have toouse without requiring user credentials.</span></span>

1. <span data-ttu-id="6e9fd-135">W projekcie aplikacji systemu Android, Dodaj powitania po stałe u góry hello hello **MainActivity** klasy:</span><span class="sxs-lookup"><span data-stu-id="6e9fd-135">In your Android app project, add hello following constants at hello top of hello **MainActivity** class:</span></span>
   
        public static final String NOTIFY_USERS_PROPERTIES = "NotifyUsersProperties";
        public static final String AUTHORIZATION_HEADER_PROPERTY = "AuthorizationHeader";
2. <span data-ttu-id="6e9fd-136">Nadal w hello **MainActivity** klasy, aktualizacja hello `getAuthorizationHeader()` hello toocontain metody następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="6e9fd-136">Still in hello **MainActivity** class, update hello `getAuthorizationHeader()` method toocontain hello following code:</span></span>
   
        private String getAuthorizationHeader() throws UnsupportedEncodingException {
            EditText username = (EditText) findViewById(R.id.usernameText);
            EditText password = (EditText) findViewById(R.id.passwordText);
            String basicAuthHeader = username.getText().toString()+":"+password.getText().toString();
            basicAuthHeader = Base64.encodeToString(basicAuthHeader.getBytes("UTF-8"), Base64.NO_WRAP);
   
            SharedPreferences sp = getSharedPreferences(NOTIFY_USERS_PROPERTIES, Context.MODE_PRIVATE);
            sp.edit().putString(AUTHORIZATION_HEADER_PROPERTY, basicAuthHeader).commit();
   
            return basicAuthHeader;
        }
3. <span data-ttu-id="6e9fd-137">Dodaj następujące hello `import` instrukcji u góry hello hello **MainActivity** pliku:</span><span class="sxs-lookup"><span data-stu-id="6e9fd-137">Add hello following `import` statements at hello top of hello **MainActivity** file:</span></span>
   
        import android.content.SharedPreferences;

<span data-ttu-id="6e9fd-138">Teraz zostanie zmieniona hello obsługi, która jest wywoływana po otrzymaniu powiadomienia hello.</span><span class="sxs-lookup"><span data-stu-id="6e9fd-138">Now we will change hello handler that is called when hello notification is received.</span></span>

1. <span data-ttu-id="6e9fd-139">W hello **MyHandler** klasy zmienić hello `OnReceive()` toocontain metody:</span><span class="sxs-lookup"><span data-stu-id="6e9fd-139">In hello **MyHandler** class change hello `OnReceive()` method toocontain:</span></span>
   
        public void onReceive(Context context, Bundle bundle) {
            ctx = context;
            String secureMessageId = bundle.getString("secureId");
            retrieveNotification(secureMessageId);
        }
2. <span data-ttu-id="6e9fd-140">Następnie dodaj hello `retrieveNotification()` metoda zastępuje symbol zastępczy hello `{back-end endpoint}` z punktem końcowym zaplecza hello uzyskane podczas wdrażania sieci wewnętrznej:</span><span class="sxs-lookup"><span data-stu-id="6e9fd-140">Then add hello `retrieveNotification()` method, replacing hello placeholder `{back-end endpoint}` with hello back-end endpoint obtained while deploying your back-end:</span></span>
   
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
                        Log.e("MainActivity", "Failed tooretrieve secure notification - " + e.getMessage());
                        return e;
                    }
                    return null;
                }
            }.execute(null, null, null);
        }

<span data-ttu-id="6e9fd-141">Ta metoda wywołuje zawartości przy użyciu poświadczeń hello przechowywanych w hello udostępnionych preferencji i wyświetla je jako normalne powiadomienie powiadomienia hello tooretrieve zaplecza aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6e9fd-141">This method calls your app back-end tooretrieve hello notification content using hello credentials stored in hello shared preferences and displays it as a normal notification.</span></span> <span data-ttu-id="6e9fd-142">powiadomienie Hello wygląda toohello użytkownika aplikacji, dokładnie tak samo jak inne powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="6e9fd-142">hello notification looks toohello app user exactly like any other push notification.</span></span>

<span data-ttu-id="6e9fd-143">Należy pamiętać, że preferowane toohandle hello przypadków brakujących właściwości nagłówka uwierzytelniania lub odrzucenia przez hello zaplecza.</span><span class="sxs-lookup"><span data-stu-id="6e9fd-143">Note that it is preferable toohandle hello cases of missing authentication header property or rejection by hello back-end.</span></span> <span data-ttu-id="6e9fd-144">Obsługa określonego Hello powyższych przypadkach zależą od przede wszystkim użytkowników docelowych.</span><span class="sxs-lookup"><span data-stu-id="6e9fd-144">hello specific handling of these cases depend mostly on your target user experience.</span></span> <span data-ttu-id="6e9fd-145">Jedną z opcji jest toodisplay powiadomienie z wierszem ogólnego hello użytkownika tooauthenticate tooretrieve hello rzeczywiste powiadomienia o.</span><span class="sxs-lookup"><span data-stu-id="6e9fd-145">One option is toodisplay a notification with a generic prompt for hello user tooauthenticate tooretrieve hello actual notification.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="6e9fd-146">Uruchom hello aplikacji</span><span class="sxs-lookup"><span data-stu-id="6e9fd-146">Run hello Application</span></span>
<span data-ttu-id="6e9fd-147">toorun hello aplikacji, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="6e9fd-147">toorun hello application, do hello following:</span></span>

1. <span data-ttu-id="6e9fd-148">Upewnij się, że **AppBackend** jest wdrożona na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="6e9fd-148">Make sure **AppBackend** is deployed in Azure.</span></span> <span data-ttu-id="6e9fd-149">Jeśli używasz programu Visual Studio, uruchom hello **AppBackend** aplikacji interfejsu API sieci Web.</span><span class="sxs-lookup"><span data-stu-id="6e9fd-149">If using Visual Studio, run hello **AppBackend** Web API application.</span></span> <span data-ttu-id="6e9fd-150">Zostanie wyświetlona strona sieci web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="6e9fd-150">An ASP.NET web page is displayed.</span></span>
2. <span data-ttu-id="6e9fd-151">W środowisku Eclipse uruchamianie aplikacji hello na fizyczne urządzenie lub hello emulator systemu Android.</span><span class="sxs-lookup"><span data-stu-id="6e9fd-151">In Eclipse, run hello app on a physical Android device or hello emulator.</span></span>
3. <span data-ttu-id="6e9fd-152">W aplikacji systemu Android hello interfejsu użytkownika wprowadź nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="6e9fd-152">In hello Android app UI, enter a username and password.</span></span> <span data-ttu-id="6e9fd-153">Mogą to być dowolny ciąg, ale muszą one być hello tę samą wartość.</span><span class="sxs-lookup"><span data-stu-id="6e9fd-153">These can be any string, but they must be hello same value.</span></span>
4. <span data-ttu-id="6e9fd-154">W aplikacji systemu Android hello interfejsu użytkownika, kliknij przycisk **Zaloguj**.</span><span class="sxs-lookup"><span data-stu-id="6e9fd-154">In hello Android app UI, click **Log in**.</span></span> <span data-ttu-id="6e9fd-155">Następnie kliknij przycisk **wysyłania wypychania**.</span><span class="sxs-lookup"><span data-stu-id="6e9fd-155">Then click **Send push**.</span></span>

