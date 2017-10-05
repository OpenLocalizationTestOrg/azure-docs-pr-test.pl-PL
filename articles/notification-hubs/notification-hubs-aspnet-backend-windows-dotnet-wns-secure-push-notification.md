---
title: Azure Notification Hubs bezpiecznego Push
description: "Dowiedz się, jak wysyłać powiadomienia wypychane bezpiecznej platformie Azure. Przykłady kodu napisane w języku C# z użyciem interfejsu API programu .NET."
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
ms.openlocfilehash: 9c626ec1534c4899588150a58c0da57b9d963f6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-notification-hubs-secure-push"></a><span data-ttu-id="b145d-104">Azure Notification Hubs bezpiecznego Push</span><span class="sxs-lookup"><span data-stu-id="b145d-104">Azure Notification Hubs Secure Push</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b145d-105">Aplikacje uniwersalne systemu Windows</span><span class="sxs-lookup"><span data-stu-id="b145d-105">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="b145d-106">iOS</span><span class="sxs-lookup"><span data-stu-id="b145d-106">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="b145d-107">Android</span><span class="sxs-lookup"><span data-stu-id="b145d-107">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="b145d-108">Omówienie</span><span class="sxs-lookup"><span data-stu-id="b145d-108">Overview</span></span>
<span data-ttu-id="b145d-109">Obsługa powiadomień wypychanych w Microsoft Azure pozwala uzyskiwać dostęp do infrastruktury wypychania łatwy w użyciu, wieloplatformową skalowalnych w poziomie, co znacznie upraszcza implementacji powiadomienia wypychane dla aplikacji zarówno konsumenckie i korporacyjne dla platform urządzeń przenośnych.</span><span class="sxs-lookup"><span data-stu-id="b145d-109">Push notification support in Microsoft Azure enables you to access an easy-to-use, multiplatform, scaled-out push infrastructure, which greatly simplifies the implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="b145d-110">Z powodu przepisami ograniczeń dotyczących zabezpieczeń, czasami aplikacji może mają zostać uwzględnione coś w powiadomienie, które nie są przesyłane za pośrednictwem infrastruktury powiadomień wypychanych standardowa.</span><span class="sxs-lookup"><span data-stu-id="b145d-110">Due to regulatory or security constraints, sometimes an application might want to include something in the notification that cannot be transmitted through the standard push notification infrastructure.</span></span> <span data-ttu-id="b145d-111">Ten przewodnik opisuje sposób do osiągnięcia w tym samym środowisku, wysyłając informacje poufne za pośrednictwem bezpiecznego uwierzytelnionego połączenia od urządzeń klienckich i zaplecza aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b145d-111">This tutorial describes how to achieve the same experience by sending sensitive information through a secure, authenticated connection between the client device and the app backend.</span></span>

<span data-ttu-id="b145d-112">Na wysokim poziomie przepływ wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="b145d-112">At a high level, the flow is as follows:</span></span>

1. <span data-ttu-id="b145d-113">Zaplecza aplikacji:</span><span class="sxs-lookup"><span data-stu-id="b145d-113">The app back-end:</span></span>
   * <span data-ttu-id="b145d-114">Magazyny bezpiecznego ładunku w wewnętrznej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="b145d-114">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="b145d-115">Wysyła identyfikator tego powiadomienia do urządzenia (nie informacji o są wysyłane).</span><span class="sxs-lookup"><span data-stu-id="b145d-115">Sends the ID of this notification to the device (no secure information is sent).</span></span>
2. <span data-ttu-id="b145d-116">Aplikacją na urządzeniu, podczas odbierania powiadomienia:</span><span class="sxs-lookup"><span data-stu-id="b145d-116">The app on the device, when receiving the notification:</span></span>
   * <span data-ttu-id="b145d-117">Urządzenie kontaktuje się z zaplecza żąda bezpiecznego ładunku.</span><span class="sxs-lookup"><span data-stu-id="b145d-117">The device contacts the back-end requesting the secure payload.</span></span>
   * <span data-ttu-id="b145d-118">Aplikację można wyświetlić ładunku jako powiadomienie na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="b145d-118">The app can show the payload as a notification on the device.</span></span>

<span data-ttu-id="b145d-119">Należy pamiętać, że w poprzednim przepływu (i w tym samouczku) przyjęto założenie, że urządzenia są przechowywane token uwierzytelniania w magazynie lokalnym, po zalogowaniu się użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b145d-119">It is important to note that in the preceding flow (and in this tutorial), we assume that the device stores an authentication token in local storage, after the user logs in.</span></span> <span data-ttu-id="b145d-120">Gwarantuje to całkowicie nie zakłóca pracy, jak urządzenia mogą pobierać ładunku bezpiecznego powiadomienia za pomocą tego tokenu.</span><span class="sxs-lookup"><span data-stu-id="b145d-120">This guarantees a completely seamless experience, as the device can retrieve the notification’s secure payload using this token.</span></span> <span data-ttu-id="b145d-121">Jeśli aplikacja nie przechowuje tokeny uwierzytelniania na urządzeniu lub tokeny te mogą wygasnąć, aplikacji urządzenia, po otrzymaniu powiadomienia powinien być wyświetlany ogólny powiadomienie monitowania użytkownika do uruchomienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b145d-121">If your application does not store authentication tokens on the device, or if these tokens can be expired, the device app, upon receiving the notification should display a generic notification prompting the user to launch the app.</span></span> <span data-ttu-id="b145d-122">Następnie aplikacja uwierzytelnia użytkownika i zawiera ładunek powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="b145d-122">The app then authenticates the user and shows the notification payload.</span></span>

<span data-ttu-id="b145d-123">W tym samouczku Secure wypychania pokazano, jak bezpiecznie wysyłać powiadomienia wypychane.</span><span class="sxs-lookup"><span data-stu-id="b145d-123">This Secure Push tutorial shows how to send a push notification securely.</span></span> <span data-ttu-id="b145d-124">Samouczek opiera się na [Powiadom użytkowników](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) samouczku, dlatego należy wykonać kroki tego samouczka najpierw.</span><span class="sxs-lookup"><span data-stu-id="b145d-124">The tutorial builds on the [Notify Users](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) tutorial, so you should complete the steps in that tutorial first.</span></span>

> [!NOTE]
> <span data-ttu-id="b145d-125">Ten samouczek zakłada, że utworzony i skonfigurowany Centrum powiadomień, zgodnie z opisem w [wprowadzenie do korzystania z usługi Notification Hubs (w Sklepie Windows)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).</span><span class="sxs-lookup"><span data-stu-id="b145d-125">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).</span></span>
> <span data-ttu-id="b145d-126">Należy również zauważyć, że program Windows Phone 8.1 wymaga poświadczeń systemu Windows (nie Windows Phone) i czy zadania w tle nie działają na Windows Phone 8.0 lub Silverlight 8.1.</span><span class="sxs-lookup"><span data-stu-id="b145d-126">Also, note that Windows Phone 8.1 requires Windows (not Windows Phone) credentials, and that background tasks do not work on Windows Phone 8.0 or Silverlight 8.1.</span></span> <span data-ttu-id="b145d-127">Dla aplikacji ze Sklepu Windows można otrzymywać powiadomienia za pośrednictwem zadania w tle, tylko wtedy, gdy aplikacja jest włączona na ekranie blokady (kliknij pole wyboru w Appmanifest).</span><span class="sxs-lookup"><span data-stu-id="b145d-127">For Windows Store applications, you can receive notifications via a background task only if the app is lock-screen enabled (click the checkbox in the Appmanifest).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-the-windows-phone-project"></a><span data-ttu-id="b145d-128">Modyfikowanie projektu Windows Phone</span><span class="sxs-lookup"><span data-stu-id="b145d-128">Modify the Windows Phone Project</span></span>
1. <span data-ttu-id="b145d-129">W **NotifyUserWindowsPhone** projekt, Dodaj następujący kod do pliku App.xaml.cs zarejestrować zadania w tle wypychania.</span><span class="sxs-lookup"><span data-stu-id="b145d-129">In the **NotifyUserWindowsPhone** project, add the following code to App.xaml.cs to register the push background task.</span></span> <span data-ttu-id="b145d-130">Dodaj następujący wiersz kodu na końcu `OnLaunched()` metody:</span><span class="sxs-lookup"><span data-stu-id="b145d-130">Add the following line of code at the end of the `OnLaunched()` method:</span></span>
   
        RegisterBackgroundTask();
2. <span data-ttu-id="b145d-131">W pliku App.xaml.cs Dodaj następujący kod bezpośrednio po `OnLaunched()` metody:</span><span class="sxs-lookup"><span data-stu-id="b145d-131">Still in App.xaml.cs, add the following code immediately after the `OnLaunched()` method:</span></span>
   
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
3. <span data-ttu-id="b145d-132">Dodaj następujące `using` instrukcje w górnej części pliku App.xaml.cs:</span><span class="sxs-lookup"><span data-stu-id="b145d-132">Add the following `using` statements at the top of the App.xaml.cs file:</span></span>
   
        using Windows.Networking.PushNotifications;
        using Windows.ApplicationModel.Background;
4. <span data-ttu-id="b145d-133">W menu **Plik** programu Visual Studio kliknij polecenie **Zapisz wszystko**.</span><span class="sxs-lookup"><span data-stu-id="b145d-133">From the **File** menu in Visual Studio, click **Save All**.</span></span>

## <a name="create-the-push-background-component"></a><span data-ttu-id="b145d-134">Tworzenie składnika tła wypychania</span><span class="sxs-lookup"><span data-stu-id="b145d-134">Create the Push Background Component</span></span>
<span data-ttu-id="b145d-135">Następnym krokiem jest utworzyć składnika tła wypychania.</span><span class="sxs-lookup"><span data-stu-id="b145d-135">The next step is to create the push background component.</span></span>

1. <span data-ttu-id="b145d-136">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy węzeł najwyższego poziomu rozwiązania (**SecurePush rozwiązania** w tym przypadku), następnie kliknij przycisk **Dodaj**, następnie kliknij przycisk **nowy projekt**.</span><span class="sxs-lookup"><span data-stu-id="b145d-136">In Solution Explorer, right-click the top-level node of the solution (**Solution SecurePush** in this case), then click **Add**, then click **New Project**.</span></span>
2. <span data-ttu-id="b145d-137">Rozwiń węzeł **aplikacji ze sklepu**, następnie kliknij przycisk **aplikacji Windows Phone**, następnie kliknij przycisk **składnika środowiska wykonawczego systemu Windows (Windows Phone)**.</span><span class="sxs-lookup"><span data-stu-id="b145d-137">Expand **Store Apps**, then click **Windows Phone Apps**, then click **Windows Runtime Component (Windows Phone)**.</span></span> <span data-ttu-id="b145d-138">Nazwij projekt **PushBackgroundComponent**, a następnie kliknij przycisk **OK** Aby utworzyć projekt.</span><span class="sxs-lookup"><span data-stu-id="b145d-138">Name the project **PushBackgroundComponent**, and then click **OK** to create the project.</span></span>
   
    ![][12]
3. <span data-ttu-id="b145d-139">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **PushBackgroundComponent (Windows Phone 8.1)** projektu, a następnie kliknij przycisk **Dodaj**, następnie kliknij przycisk **klasy**.</span><span class="sxs-lookup"><span data-stu-id="b145d-139">In Solution Explorer, right-click the **PushBackgroundComponent (Windows Phone 8.1)** project, then click **Add**, then click **Class**.</span></span> <span data-ttu-id="b145d-140">Nazwa nowej klasy **PushBackgroundTask.cs**.</span><span class="sxs-lookup"><span data-stu-id="b145d-140">Name the new class **PushBackgroundTask.cs**.</span></span> <span data-ttu-id="b145d-141">Kliknij przycisk **Dodaj** do generowania klasy.</span><span class="sxs-lookup"><span data-stu-id="b145d-141">Click **Add** to generate the class.</span></span>
4. <span data-ttu-id="b145d-142">Zastąp całą zawartość **PushBackgroundComponent** definicję przestrzeni nazw następującym kodem, zastępując symbol zastępczy `{back-end endpoint}` z punktem końcowym zaplecza uzyskane podczas wdrażania sieci wewnętrznej:</span><span class="sxs-lookup"><span data-stu-id="b145d-142">Replace the entire contents of the **PushBackgroundComponent** namespace definition with the following code, substituting the placeholder `{back-end endpoint}` with the back-end endpoint obtained while deploying your back-end:</span></span>
   
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
                    // Store the content received from the notification so it can be retrieved from the UI.
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
5. <span data-ttu-id="b145d-143">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **PushBackgroundComponent (Windows Phone 8.1)** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="b145d-143">In Solution Explorer, right-click the **PushBackgroundComponent (Windows Phone 8.1)** project and then click **Manage NuGet Packages**.</span></span>
6. <span data-ttu-id="b145d-144">Po lewej stronie kliknij **Online**.</span><span class="sxs-lookup"><span data-stu-id="b145d-144">On the left-hand side, click **Online**.</span></span>
7. <span data-ttu-id="b145d-145">W **wyszukiwania** wpisz **klienta Http**.</span><span class="sxs-lookup"><span data-stu-id="b145d-145">In the **Search** box, type **Http Client**.</span></span>
8. <span data-ttu-id="b145d-146">Na liście wyników kliknij **bibliotek klienta HTTP Microsoft**, a następnie kliknij przycisk **zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="b145d-146">In the results list, click **Microsoft HTTP Client Libraries**, and then click **Install**.</span></span> <span data-ttu-id="b145d-147">Ukończ instalację.</span><span class="sxs-lookup"><span data-stu-id="b145d-147">Complete the installation.</span></span>
9. <span data-ttu-id="b145d-148">W polu **wyszukiwania** wpisz **Json.net**.</span><span class="sxs-lookup"><span data-stu-id="b145d-148">Back in the NuGet **Search** box, type **Json.net**.</span></span> <span data-ttu-id="b145d-149">Zainstaluj **Json.NET** pakietu, a następnie zamknij okno Menedżera pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="b145d-149">Install the **Json.NET** package, then close the NuGet Package Manager window.</span></span>
10. <span data-ttu-id="b145d-150">Dodaj następujące `using` instrukcje w górnej części **PushBackgroundTask.cs** pliku:</span><span class="sxs-lookup"><span data-stu-id="b145d-150">Add the following `using` statements at the top of the **PushBackgroundTask.cs** file:</span></span>
    
        using Windows.ApplicationModel.Background;
        using Windows.Networking.PushNotifications;
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Newtonsoft.Json;
        using Windows.UI.Notifications;
        using Windows.Data.Xml.Dom;
11. <span data-ttu-id="b145d-151">W Eksploratorze rozwiązań w **NotifyUserWindowsPhone (Windows Phone 8.1)** projektu, kliknij prawym przyciskiem myszy **odwołania**, następnie kliknij przycisk **Dodawanie odwołania...** .</span><span class="sxs-lookup"><span data-stu-id="b145d-151">In Solution Explorer, in the **NotifyUserWindowsPhone (Windows Phone 8.1)** project, right-click **References**, then click **Add Reference...**.</span></span> <span data-ttu-id="b145d-152">W oknie dialogowym Menedżer odwołania, zaznacz pole wyboru obok pozycji **PushBackgroundComponent**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="b145d-152">In the Reference Manager dialog, check the box next to **PushBackgroundComponent**, and then click **OK**.</span></span>
12. <span data-ttu-id="b145d-153">W Eksploratorze rozwiązań kliknij dwukrotnie **Package.appxmanifest** w **NotifyUserWindowsPhone (Windows Phone 8.1)** projektu.</span><span class="sxs-lookup"><span data-stu-id="b145d-153">In Solution Explorer, double-click **Package.appxmanifest** in the **NotifyUserWindowsPhone (Windows Phone 8.1)** project.</span></span> <span data-ttu-id="b145d-154">W obszarze **powiadomienia**ustaw **wyskakujące funkcją** do **tak**.</span><span class="sxs-lookup"><span data-stu-id="b145d-154">Under **Notifications**, set **Toast Capable** to **Yes**.</span></span>
    
    ![][3]
13. <span data-ttu-id="b145d-155">Nadal **Package.appxmanifest**, kliknij przycisk **deklaracje** menu u góry.</span><span class="sxs-lookup"><span data-stu-id="b145d-155">Still in **Package.appxmanifest**, click the **Declarations** menu near the top.</span></span> <span data-ttu-id="b145d-156">W **dostępne deklaracje** listy rozwijanej, kliknij przycisk **zadania w tle**, a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="b145d-156">In the **Available Declarations** dropdown, click **Background Tasks**, and then click **Add**.</span></span>
14. <span data-ttu-id="b145d-157">W **Package.appxmanifest**w obszarze **właściwości**, sprawdź **powiadomienie wypychane**.</span><span class="sxs-lookup"><span data-stu-id="b145d-157">In **Package.appxmanifest**, under **Properties**, check **Push notification**.</span></span>
15. <span data-ttu-id="b145d-158">W **Package.appxmanifest**w obszarze **ustawień aplikacji**, typ **PushBackgroundComponent.PushBackgroundTask** w **punktu wejścia** pola.</span><span class="sxs-lookup"><span data-stu-id="b145d-158">In **Package.appxmanifest**, under **App Settings**, type **PushBackgroundComponent.PushBackgroundTask** in the **Entry Point** field.</span></span>
    
    ![][13]
16. <span data-ttu-id="b145d-159">W menu **Plik** kliknij polecenie **Zapisz wszystko**.</span><span class="sxs-lookup"><span data-stu-id="b145d-159">From the **File** menu, click **Save All**.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="b145d-160">Uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="b145d-160">Run the Application</span></span>
<span data-ttu-id="b145d-161">Aby uruchomić aplikację, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b145d-161">To run the application, do the following:</span></span>

1. <span data-ttu-id="b145d-162">W programie Visual Studio, uruchom **AppBackend** aplikacji interfejsu API sieci Web.</span><span class="sxs-lookup"><span data-stu-id="b145d-162">In Visual Studio, run the **AppBackend** Web API application.</span></span> <span data-ttu-id="b145d-163">Zostanie wyświetlona strona sieci web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="b145d-163">An ASP.NET web page is displayed.</span></span>
2. <span data-ttu-id="b145d-164">W programie Visual Studio, uruchom **NotifyUserWindowsPhone (Windows Phone 8.1)** aplikacji Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="b145d-164">In Visual Studio, run the **NotifyUserWindowsPhone (Windows Phone 8.1)** Windows Phone app.</span></span> <span data-ttu-id="b145d-165">Windows Phone emulator działa i automatycznie załadowanie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b145d-165">The Windows Phone emulator runs and loads the app automatically.</span></span>
3. <span data-ttu-id="b145d-166">W **NotifyUserWindowsPhone** aplikacji interfejsu użytkownika, wprowadź nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="b145d-166">In the **NotifyUserWindowsPhone** app UI, enter a username and password.</span></span> <span data-ttu-id="b145d-167">Mogą to być dowolny ciąg, ale muszą one mieć taką samą wartość.</span><span class="sxs-lookup"><span data-stu-id="b145d-167">These can be any string, but they must be the same value.</span></span>
4. <span data-ttu-id="b145d-168">W **NotifyUserWindowsPhone** aplikacji interfejsu użytkownika, kliknij przycisk **zalogować się i Zarejestruj**.</span><span class="sxs-lookup"><span data-stu-id="b145d-168">In the **NotifyUserWindowsPhone** app UI, click **Log in and register**.</span></span> <span data-ttu-id="b145d-169">Następnie kliknij przycisk **wysyłania wypychania**.</span><span class="sxs-lookup"><span data-stu-id="b145d-169">Then click **Send push**.</span></span>

[3]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push3.png
[12]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push12.png
[13]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push13.png
