---
title: aaaAzure powiadomienia Push Secure koncentratory
description: "Dowiedz się, jak bezpieczne toosend powiadomień wypychanych na platformie Azure. Przykłady kodu napisane w języku C# za pomocą hello interfejsu API platformy .NET."
documentationcenter: windows
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: 5aef50f4-80b3-460e-a9a7-7435001273bd
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: b6fe16c96d28d75ff698278409fb012472ba6396
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-secure-push"></a><span data-ttu-id="3e218-104">Azure Notification Hubs bezpiecznego Push</span><span class="sxs-lookup"><span data-stu-id="3e218-104">Azure Notification Hubs Secure Push</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3e218-105">Aplikacje uniwersalne systemu Windows</span><span class="sxs-lookup"><span data-stu-id="3e218-105">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="3e218-106">iOS</span><span class="sxs-lookup"><span data-stu-id="3e218-106">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="3e218-107">Android</span><span class="sxs-lookup"><span data-stu-id="3e218-107">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="3e218-108">Omówienie</span><span class="sxs-lookup"><span data-stu-id="3e218-108">Overview</span></span>
<span data-ttu-id="3e218-109">Obsługa powiadomień wypychanych w Microsoft Azure umożliwia tooaccess infrastruktury wypychania łatwy w użyciu, wieloplatformową skalowalnych w poziomie, który jest znacznie ułatwione hello stosowania powiadomienia wypychane zarówno konsumenckie i korporacyjne aplikacji dla urządzeń przenośnych platform.</span><span class="sxs-lookup"><span data-stu-id="3e218-109">Push notification support in Microsoft Azure enables you tooaccess an easy-to-use, multiplatform, scaled-out push infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="3e218-110">Czasami ze względu na ograniczenia tooregulatory lub zabezpieczeń, aplikacja może być tooinclude coś w hello powiadomienie, które nie są przesyłane za pośrednictwem infrastruktury powiadomień wypychanych standardowe hello.</span><span class="sxs-lookup"><span data-stu-id="3e218-110">Due tooregulatory or security constraints, sometimes an application might want tooinclude something in hello notification that cannot be transmitted through hello standard push notification infrastructure.</span></span> <span data-ttu-id="3e218-111">W tym samouczku opisano, jak tooachieve hello tego samego środowiska poprzez wysłanie poufnych informacji za pośrednictwem bezpiecznego połączenia uwierzytelnionego między powitania klienta urządzenia i aplikacji hello wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="3e218-111">This tutorial describes how tooachieve hello same experience by sending sensitive information through a secure, authenticated connection between hello client device and hello app backend.</span></span>

<span data-ttu-id="3e218-112">Na wysokim poziomie przepływu hello jest następujący:</span><span class="sxs-lookup"><span data-stu-id="3e218-112">At a high level, hello flow is as follows:</span></span>

1. <span data-ttu-id="3e218-113">Witaj zaplecze aplikacji:</span><span class="sxs-lookup"><span data-stu-id="3e218-113">hello app back-end:</span></span>
   * <span data-ttu-id="3e218-114">Magazyny bezpiecznego ładunku w wewnętrznej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="3e218-114">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="3e218-115">Wysyła identyfikator hello tego urządzenia toohello powiadomienie (nie bezpiecznego informacje są wysyłane).</span><span class="sxs-lookup"><span data-stu-id="3e218-115">Sends hello ID of this notification toohello device (no secure information is sent).</span></span>
2. <span data-ttu-id="3e218-116">Aplikacja Hello na urządzeniu hello podczas odbierania powiadomień hello:</span><span class="sxs-lookup"><span data-stu-id="3e218-116">hello app on hello device, when receiving hello notification:</span></span>
   * <span data-ttu-id="3e218-117">urządzenie Hello kontaktuje się hello zaplecza żądania hello bezpiecznego ładunku.</span><span class="sxs-lookup"><span data-stu-id="3e218-117">hello device contacts hello back-end requesting hello secure payload.</span></span>
   * <span data-ttu-id="3e218-118">Aplikacja Hello można wyświetlić ładunku hello jako powiadomienie na urządzeniu hello.</span><span class="sxs-lookup"><span data-stu-id="3e218-118">hello app can show hello payload as a notification on hello device.</span></span>

<span data-ttu-id="3e218-119">Jest ważne toonote, że w hello poprzedzających przepływu (i w tym samouczku) przyjęto założenie, urządzenia hello po zalogowaniu użytkownika hello przechowuje token uwierzytelniania w magazynie lokalnym.</span><span class="sxs-lookup"><span data-stu-id="3e218-119">It is important toonote that in hello preceding flow (and in this tutorial), we assume that hello device stores an authentication token in local storage, after hello user logs in.</span></span> <span data-ttu-id="3e218-120">Gwarantuje to całkowicie sprawnie, jak urządzenia hello mogą pobierać ładunku bezpiecznego hello powiadomienia za pomocą tego tokenu.</span><span class="sxs-lookup"><span data-stu-id="3e218-120">This guarantees a completely seamless experience, as hello device can retrieve hello notification’s secure payload using this token.</span></span> <span data-ttu-id="3e218-121">Jeśli aplikacja nie przechowuje tokeny uwierzytelniania na urządzeniu hello lub tokeny te mogą wygasnąć, hello aplikacji urządzenia po otrzymaniu powiadomienia hello powinien być wyświetlany ogólny powiadomienie aplikacji hello toolaunch użytkownika hello monitowania.</span><span class="sxs-lookup"><span data-stu-id="3e218-121">If your application does not store authentication tokens on hello device, or if these tokens can be expired, hello device app, upon receiving hello notification should display a generic notification prompting hello user toolaunch hello app.</span></span> <span data-ttu-id="3e218-122">Aplikacja Hello następnie uwierzytelnia użytkownika hello i zawiera ładunek powiadomienia hello.</span><span class="sxs-lookup"><span data-stu-id="3e218-122">hello app then authenticates hello user and shows hello notification payload.</span></span>

<span data-ttu-id="3e218-123">W tym samouczku Secure wypychania przedstawiono sposób toosend powiadomienie wypychane bezpieczny sposób.</span><span class="sxs-lookup"><span data-stu-id="3e218-123">This Secure Push tutorial shows how toosend a push notification securely.</span></span> <span data-ttu-id="3e218-124">Samouczek Hello opiera się na powitania [Powiadom użytkowników](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) samouczku, dlatego należy wykonać kroki hello w tym samouczku najpierw.</span><span class="sxs-lookup"><span data-stu-id="3e218-124">hello tutorial builds on hello [Notify Users](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) tutorial, so you should complete hello steps in that tutorial first.</span></span>

> [!NOTE]
> <span data-ttu-id="3e218-125">Ten samouczek zakłada, że utworzony i skonfigurowany Centrum powiadomień, zgodnie z opisem w [wprowadzenie do korzystania z usługi Notification Hubs (w Sklepie Windows)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).</span><span class="sxs-lookup"><span data-stu-id="3e218-125">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).</span></span>
> <span data-ttu-id="3e218-126">Należy również zauważyć, że program Windows Phone 8.1 wymaga poświadczeń systemu Windows (nie Windows Phone) i czy zadania w tle nie działają na Windows Phone 8.0 lub Silverlight 8.1.</span><span class="sxs-lookup"><span data-stu-id="3e218-126">Also, note that Windows Phone 8.1 requires Windows (not Windows Phone) credentials, and that background tasks do not work on Windows Phone 8.0 or Silverlight 8.1.</span></span> <span data-ttu-id="3e218-127">Dla aplikacji ze Sklepu Windows można otrzymywać powiadomienia za pośrednictwem zadania w tle, tylko wtedy, gdy aplikacja hello jest włączona na ekranie blokady (kliknij pole wyboru hello w hello Appmanifest).</span><span class="sxs-lookup"><span data-stu-id="3e218-127">For Windows Store applications, you can receive notifications via a background task only if hello app is lock-screen enabled (click hello checkbox in hello Appmanifest).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-windows-phone-project"></a><span data-ttu-id="3e218-128">Modyfikowanie hello projektu Windows Phone</span><span class="sxs-lookup"><span data-stu-id="3e218-128">Modify hello Windows Phone Project</span></span>
1. <span data-ttu-id="3e218-129">W hello **NotifyUserWindowsPhone** projekt, Dodaj hello następującego kodu tooApp.xaml.cs tooregister hello wypychania zadanie wykonywane w tle.</span><span class="sxs-lookup"><span data-stu-id="3e218-129">In hello **NotifyUserWindowsPhone** project, add hello following code tooApp.xaml.cs tooregister hello push background task.</span></span> <span data-ttu-id="3e218-130">Dodaj następujące wiersz kodu na końcu hello hello hello `OnLaunched()` metody:</span><span class="sxs-lookup"><span data-stu-id="3e218-130">Add hello following line of code at hello end of hello `OnLaunched()` method:</span></span>
   
        RegisterBackgroundTask();
2. <span data-ttu-id="3e218-131">Nadal w pliku App.xaml.cs Dodaj następujące kod bezpośrednio po hello hello `OnLaunched()` metody:</span><span class="sxs-lookup"><span data-stu-id="3e218-131">Still in App.xaml.cs, add hello following code immediately after hello `OnLaunched()` method:</span></span>
   
        private async void RegisterBackgroundTask()
        {
            if (!Windows.ApplicationModel.Background.BackgroundTaskRegistration.AllTasks.Any(i => i.Value.Name == "PushBackgroundTask"))
            {
                var result = await BackgroundExecutionManager.RequestAccessAsync();
                var builder = new BackgroundTaskBuilder();
   
                builder.Name = "PushBackgroundTask";
                builder.TaskEntryPoint = typeof(PushBackgroundComponent.PushBackgroundTask).FullName;
                builder.SetTrigger(new Windows.ApplicationModel.Background.PushNotificationTrigger());
                BackgroundTaskRegistration task = builder.Register();
            }
        }
3. <span data-ttu-id="3e218-132">Dodaj następujące hello `using` instrukcji u góry hello plik App.xaml.cs hello:</span><span class="sxs-lookup"><span data-stu-id="3e218-132">Add hello following `using` statements at hello top of hello App.xaml.cs file:</span></span>
   
        using Windows.Networking.PushNotifications;
        using Windows.ApplicationModel.Background;
4. <span data-ttu-id="3e218-133">Z hello **pliku** menu programu Visual Studio kliknij **Zapisz wszystko**.</span><span class="sxs-lookup"><span data-stu-id="3e218-133">From hello **File** menu in Visual Studio, click **Save All**.</span></span>

## <a name="create-hello-push-background-component"></a><span data-ttu-id="3e218-134">Utwórz hello Push składnika tła</span><span class="sxs-lookup"><span data-stu-id="3e218-134">Create hello Push Background Component</span></span>
<span data-ttu-id="3e218-135">Witaj następnym krokiem jest toocreate hello wypychania tła składnika.</span><span class="sxs-lookup"><span data-stu-id="3e218-135">hello next step is toocreate hello push background component.</span></span>

1. <span data-ttu-id="3e218-136">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy węzeł najwyższego poziomu hello hello rozwiązania (**SecurePush rozwiązania** w tym przypadku), następnie kliknij przycisk **Dodaj**, następnie kliknij przycisk **nowy projekt**.</span><span class="sxs-lookup"><span data-stu-id="3e218-136">In Solution Explorer, right-click hello top-level node of hello solution (**Solution SecurePush** in this case), then click **Add**, then click **New Project**.</span></span>
2. <span data-ttu-id="3e218-137">Rozwiń węzeł **aplikacji ze sklepu**, następnie kliknij przycisk **aplikacji Windows Phone**, następnie kliknij przycisk **składnika środowiska wykonawczego systemu Windows (Windows Phone)**.</span><span class="sxs-lookup"><span data-stu-id="3e218-137">Expand **Store Apps**, then click **Windows Phone Apps**, then click **Windows Runtime Component (Windows Phone)**.</span></span> <span data-ttu-id="3e218-138">Nazwa projektu hello **PushBackgroundComponent**, a następnie kliknij przycisk **OK** toocreate hello projektu.</span><span class="sxs-lookup"><span data-stu-id="3e218-138">Name hello project **PushBackgroundComponent**, and then click **OK** toocreate hello project.</span></span>
   
    ![][12]
3. <span data-ttu-id="3e218-139">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **PushBackgroundComponent (Windows Phone 8.1)** projektu, a następnie kliknij przycisk **Dodaj**, następnie kliknij przycisk **klasy**.</span><span class="sxs-lookup"><span data-stu-id="3e218-139">In Solution Explorer, right-click hello **PushBackgroundComponent (Windows Phone 8.1)** project, then click **Add**, then click **Class**.</span></span> <span data-ttu-id="3e218-140">Nazwa nowej klasy hello **PushBackgroundTask.cs**.</span><span class="sxs-lookup"><span data-stu-id="3e218-140">Name hello new class **PushBackgroundTask.cs**.</span></span> <span data-ttu-id="3e218-141">Kliknij przycisk **Dodaj** toogenerate hello klasy.</span><span class="sxs-lookup"><span data-stu-id="3e218-141">Click **Add** toogenerate hello class.</span></span>
4. <span data-ttu-id="3e218-142">Zastąp całą zawartość hello hello **PushBackgroundComponent** definicję przestrzeni nazw z powitania po kod, zastępując symbolu zastępczego hello `{back-end endpoint}` z punktem końcowym zaplecza hello uzyskane podczas wdrażania programu zaplecza:</span><span class="sxs-lookup"><span data-stu-id="3e218-142">Replace hello entire contents of hello **PushBackgroundComponent** namespace definition with hello following code, substituting hello placeholder `{back-end endpoint}` with hello back-end endpoint obtained while deploying your back-end:</span></span>
   
        public sealed class Notification
            {
                public int Id { get; set; }
                public string Payload { get; set; }
                public bool Read { get; set; }
            }
   
            public sealed class PushBackgroundTask : IBackgroundTask
            {
                private string GET_URL = "{back-end endpoint}/api/notifications/";
   
                async void IBackgroundTask.Run(IBackgroundTaskInstance taskInstance)
                {
                    // Store hello content received from hello notification so it can be retrieved from hello UI.
                    RawNotification raw = (RawNotification)taskInstance.TriggerDetails;
                    var notificationId = raw.Content;
   
                    // retrieve content
                    BackgroundTaskDeferral deferral = taskInstance.GetDeferral();
                    var httpClient = new HttpClient();
                    var settings = ApplicationData.Current.LocalSettings.Values;
                    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string)settings["AuthenticationToken"]);
   
                    var notificationString = await httpClient.GetStringAsync(GET_URL + notificationId);
   
                    var notification = JsonConvert.DeserializeObject<Notification>(notificationString);
   
                    ShowToast(notification);
   
                    deferral.Complete();
                }
   
                private void ShowToast(Notification notification)
                {
                    ToastTemplateType toastTemplate = ToastTemplateType.ToastText01;
                    XmlDocument toastXml = ToastNotificationManager.GetTemplateContent(toastTemplate);
                    XmlNodeList toastTextElements = toastXml.GetElementsByTagName("text");
                    toastTextElements[0].AppendChild(toastXml.CreateTextNode(notification.Payload));
                    ToastNotification toast = new ToastNotification(toastXml);
                    ToastNotificationManager.CreateToastNotifier().Show(toast);
                }
            }
5. <span data-ttu-id="3e218-143">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **PushBackgroundComponent (Windows Phone 8.1)** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="3e218-143">In Solution Explorer, right-click hello **PushBackgroundComponent (Windows Phone 8.1)** project and then click **Manage NuGet Packages**.</span></span>
6. <span data-ttu-id="3e218-144">Na powitania po lewej stronie, kliknij przycisk **Online**.</span><span class="sxs-lookup"><span data-stu-id="3e218-144">On hello left-hand side, click **Online**.</span></span>
7. <span data-ttu-id="3e218-145">W hello **wyszukiwania** wpisz **klienta Http**.</span><span class="sxs-lookup"><span data-stu-id="3e218-145">In hello **Search** box, type **Http Client**.</span></span>
8. <span data-ttu-id="3e218-146">Kliknij na liście wyników hello **bibliotek klienta HTTP Microsoft**, a następnie kliknij przycisk **zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="3e218-146">In hello results list, click **Microsoft HTTP Client Libraries**, and then click **Install**.</span></span> <span data-ttu-id="3e218-147">Ukończenie instalacji hello.</span><span class="sxs-lookup"><span data-stu-id="3e218-147">Complete hello installation.</span></span>
9. <span data-ttu-id="3e218-148">Po powrocie do hello NuGet **wyszukiwania** wpisz **Json.net**.</span><span class="sxs-lookup"><span data-stu-id="3e218-148">Back in hello NuGet **Search** box, type **Json.net**.</span></span> <span data-ttu-id="3e218-149">Zainstaluj hello **Json.NET** pakietu, a następnie zamknij hello okna Menedżera pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="3e218-149">Install hello **Json.NET** package, then close hello NuGet Package Manager window.</span></span>
10. <span data-ttu-id="3e218-150">Dodaj następujące hello `using` instrukcji u góry hello hello **PushBackgroundTask.cs** pliku:</span><span class="sxs-lookup"><span data-stu-id="3e218-150">Add hello following `using` statements at hello top of hello **PushBackgroundTask.cs** file:</span></span>
    
        using Windows.ApplicationModel.Background;
        using Windows.Networking.PushNotifications;
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Newtonsoft.Json;
        using Windows.UI.Notifications;
        using Windows.Data.Xml.Dom;
11. <span data-ttu-id="3e218-151">W Eksploratorze rozwiązań w hello **NotifyUserWindowsPhone (Windows Phone 8.1)** projektu, kliknij prawym przyciskiem myszy **odwołania**, następnie kliknij przycisk **Dodawanie odwołania...** . W oknie dialogowym Menedżera odwołań hello hello pole wyboru obok zbyt**PushBackgroundComponent**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="3e218-151">In Solution Explorer, in hello **NotifyUserWindowsPhone (Windows Phone 8.1)** project, right-click **References**, then click **Add Reference...**. In hello Reference Manager dialog, check hello box next too**PushBackgroundComponent**, and then click **OK**.</span></span>
12. <span data-ttu-id="3e218-152">W Eksploratorze rozwiązań kliknij dwukrotnie **Package.appxmanifest** w hello **NotifyUserWindowsPhone (Windows Phone 8.1)** projektu.</span><span class="sxs-lookup"><span data-stu-id="3e218-152">In Solution Explorer, double-click **Package.appxmanifest** in hello **NotifyUserWindowsPhone (Windows Phone 8.1)** project.</span></span> <span data-ttu-id="3e218-153">W obszarze **powiadomienia**ustaw **wyskakujące funkcją** za**tak**.</span><span class="sxs-lookup"><span data-stu-id="3e218-153">Under **Notifications**, set **Toast Capable** too**Yes**.</span></span>
    
    ![][3]
13. <span data-ttu-id="3e218-154">Nadal **Package.appxmanifest**, kliknij przycisk hello **deklaracje** menu u góry hello.</span><span class="sxs-lookup"><span data-stu-id="3e218-154">Still in **Package.appxmanifest**, click hello **Declarations** menu near hello top.</span></span> <span data-ttu-id="3e218-155">W hello **dostępne deklaracje** listy rozwijanej, kliknij przycisk **zadania w tle**, a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="3e218-155">In hello **Available Declarations** dropdown, click **Background Tasks**, and then click **Add**.</span></span>
14. <span data-ttu-id="3e218-156">W **Package.appxmanifest**w obszarze **właściwości**, sprawdź **powiadomienie wypychane**.</span><span class="sxs-lookup"><span data-stu-id="3e218-156">In **Package.appxmanifest**, under **Properties**, check **Push notification**.</span></span>
15. <span data-ttu-id="3e218-157">W **Package.appxmanifest**w obszarze **ustawień aplikacji**, typ **PushBackgroundComponent.PushBackgroundTask** w hello **punktu wejścia** pole.</span><span class="sxs-lookup"><span data-stu-id="3e218-157">In **Package.appxmanifest**, under **App Settings**, type **PushBackgroundComponent.PushBackgroundTask** in hello **Entry Point** field.</span></span>
    
    ![][13]
16. <span data-ttu-id="3e218-158">Z hello **pliku** menu, kliknij przycisk **Zapisz wszystko**.</span><span class="sxs-lookup"><span data-stu-id="3e218-158">From hello **File** menu, click **Save All**.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="3e218-159">Uruchom hello aplikacji</span><span class="sxs-lookup"><span data-stu-id="3e218-159">Run hello Application</span></span>
<span data-ttu-id="3e218-160">toorun hello aplikacji, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="3e218-160">toorun hello application, do hello following:</span></span>

1. <span data-ttu-id="3e218-161">W programie Visual Studio, uruchom hello **AppBackend** aplikacji interfejsu API sieci Web.</span><span class="sxs-lookup"><span data-stu-id="3e218-161">In Visual Studio, run hello **AppBackend** Web API application.</span></span> <span data-ttu-id="3e218-162">Zostanie wyświetlona strona sieci web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="3e218-162">An ASP.NET web page is displayed.</span></span>
2. <span data-ttu-id="3e218-163">W programie Visual Studio, uruchom hello **NotifyUserWindowsPhone (Windows Phone 8.1)** aplikacji Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="3e218-163">In Visual Studio, run hello **NotifyUserWindowsPhone (Windows Phone 8.1)** Windows Phone app.</span></span> <span data-ttu-id="3e218-164">Witaj Windows Phone emulator działa i aplikacji hello jest ładowana automatycznie.</span><span class="sxs-lookup"><span data-stu-id="3e218-164">hello Windows Phone emulator runs and loads hello app automatically.</span></span>
3. <span data-ttu-id="3e218-165">W hello **NotifyUserWindowsPhone** aplikacji interfejsu użytkownika, wprowadź nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="3e218-165">In hello **NotifyUserWindowsPhone** app UI, enter a username and password.</span></span> <span data-ttu-id="3e218-166">Mogą to być dowolny ciąg, ale muszą one być hello tę samą wartość.</span><span class="sxs-lookup"><span data-stu-id="3e218-166">These can be any string, but they must be hello same value.</span></span>
4. <span data-ttu-id="3e218-167">W hello **NotifyUserWindowsPhone** aplikacji interfejsu użytkownika, kliknij przycisk **zalogować się i Zarejestruj**.</span><span class="sxs-lookup"><span data-stu-id="3e218-167">In hello **NotifyUserWindowsPhone** app UI, click **Log in and register**.</span></span> <span data-ttu-id="3e218-168">Następnie kliknij przycisk **wysyłania wypychania**.</span><span class="sxs-lookup"><span data-stu-id="3e218-168">Then click **Send push**.</span></span>

[3]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push3.png
[12]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push12.png
[13]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push13.png
