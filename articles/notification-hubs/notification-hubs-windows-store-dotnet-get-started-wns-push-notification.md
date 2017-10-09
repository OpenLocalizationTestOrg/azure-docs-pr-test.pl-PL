---
title: "wprowadzenie do usługi Azure Notification Hubs dla systemu Windows Universal platformy aplikacji aaaGet | Dokumentacja firmy Microsoft"
description: "Z tego samouczka, dowiesz się, jak toouse usługi Azure Notification Hubs toopush powiadomienia tooa aplikacji platformy uniwersalnej systemu Windows."
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: erikre
ms.assetid: cf307cf3-8c58-4628-9c63-8751e6a0ef43
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 11056842d205522ed493dc61c76ecf78ebb5a363
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-notification-hubs-for-windows-universal-platform-apps"></a><span data-ttu-id="19fca-103">Rozpoczynanie pracy z usługą Azure Notification Hubs dla aplikacji platformy uniwersalnej systemu Windows</span><span class="sxs-lookup"><span data-stu-id="19fca-103">Getting started with Notification Hubs for Windows Universal Platform Apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="19fca-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="19fca-104">Overview</span></span>
<span data-ttu-id="19fca-105">Ten samouczek pokazuje, jak toosend usługi Azure Notification Hubs toouse wypychanie powiadomień tooa Windows platformy Uniwersalnej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="19fca-105">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa Universal Windows Platform (UWP) app.</span></span>

<span data-ttu-id="19fca-106">W tym samouczku utworzysz pustą aplikację Sklepu Windows, która odbiera powiadomienia wypychane przy użyciu hello wypychania powiadomienia usługi WNS (Windows).</span><span class="sxs-lookup"><span data-stu-id="19fca-106">In this tutorial, you create a blank Windows Store app that receives push notifications by using hello Windows Push Notification Service (WNS).</span></span> <span data-ttu-id="19fca-107">Po zakończeniu będziesz w stanie toouse Twojego toobroadcast Centrum powiadomień wypychanych powiadomienia tooall hello urządzeń z tą aplikacją.</span><span class="sxs-lookup"><span data-stu-id="19fca-107">When you're finished, you'll be able toouse your notification hub toobroadcast push notifications tooall hello devices running your app.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="19fca-108">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="19fca-108">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="19fca-109">Kod ukończyć powitalnych dla tego samouczka można znaleźć w witrynie GitHub [tutaj](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal).</span><span class="sxs-lookup"><span data-stu-id="19fca-109">hello completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="19fca-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="19fca-110">Prerequisites</span></span>
<span data-ttu-id="19fca-111">Ten samouczek wymaga następujących hello:</span><span class="sxs-lookup"><span data-stu-id="19fca-111">This tutorial requires hello following:</span></span>

* <span data-ttu-id="19fca-112">Program [Microsoft Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs) lub nowszy</span><span class="sxs-lookup"><span data-stu-id="19fca-112">[Microsoft Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs) or later</span></span>
* [<span data-ttu-id="19fca-113">Zainstalowane narzędzia do programowania aplikacji uniwersalnych systemu Windows</span><span class="sxs-lookup"><span data-stu-id="19fca-113">Universal Windows App Development Tools installed</span></span>](https://msdn.microsoft.com/windows/uwp/get-started/get-set-up)
* <span data-ttu-id="19fca-114">Aktywne konto platformy Azure</span><span class="sxs-lookup"><span data-stu-id="19fca-114">An active Azure account</span></span> <br/><span data-ttu-id="19fca-115">Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="19fca-115">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="19fca-116">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-store-dotnet-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="19fca-116">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-store-dotnet-get-started%2F).</span></span>
* <span data-ttu-id="19fca-117">Aktywne konto Sklepu Windows</span><span class="sxs-lookup"><span data-stu-id="19fca-117">An active Windows Store account</span></span>

<span data-ttu-id="19fca-118">Wykonanie czynności opisanych w tym samouczku jest wymaganiem wstępnym dla wszystkich innych samouczków usługi Notification Hubs dotyczących aplikacji platformy uniwersalnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="19fca-118">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Windows Universal Platform apps.</span></span>

## <a name="register-your-app-for-hello-windows-store"></a><span data-ttu-id="19fca-119">Rejestrowanie aplikacji dla Sklepu Windows hello</span><span class="sxs-lookup"><span data-stu-id="19fca-119">Register your app for hello Windows Store</span></span>
<span data-ttu-id="19fca-120">toosend aplikacji tooUWP powiadomienia wypychane, należy skojarzyć z toohello aplikacji Sklepu Windows.</span><span class="sxs-lookup"><span data-stu-id="19fca-120">toosend push notifications tooUWP apps, you must associate your app toohello Windows Store.</span></span> <span data-ttu-id="19fca-121">Następnie należy skonfigurować Twoje toointegrate Centrum powiadomień z usługą WNS.</span><span class="sxs-lookup"><span data-stu-id="19fca-121">You must then configure your notification hub toointegrate with WNS.</span></span>

1. <span data-ttu-id="19fca-122">Jeśli nie zarejestrowano jeszcze aplikacji, przejdź toohello [Centrum deweloperów systemu Windows](https://dev.windows.com/overview), zaloguj się przy użyciu konta Microsoft, a następnie kliknij przycisk **Utwórz nową aplikację**.</span><span class="sxs-lookup"><span data-stu-id="19fca-122">If you have not already registered your app, navigate toohello [Windows Dev Center](https://dev.windows.com/overview), sign in with your Microsoft account, and then click **Create a new app**.</span></span>

2. <span data-ttu-id="19fca-123">Wpisz nazwę aplikacji i kliknij pozycję **Rezerwuj nazwę aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="19fca-123">Type a name for your app and click **Reserve app name**.</span></span> <span data-ttu-id="19fca-124">Spowoduje to utworzenie nowej rejestracji aplikacji w Sklepie Windows.</span><span class="sxs-lookup"><span data-stu-id="19fca-124">This creates a new Windows Store registration for your app.</span></span>

3. <span data-ttu-id="19fca-125">W programie Visual Studio Utwórz nowy projekt Visual C# aplikacji ze sklepu za pomocą uniwersalnych systemu Windows hello **pusta aplikacja** szablon i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="19fca-125">In Visual Studio, create a new Visual C# Store Apps project by using hello Windows Universal **Blank App** template and click **OK**.</span></span>

4. <span data-ttu-id="19fca-126">Zaakceptuj ustawienia domyślne powitania dla docelowej hello i minimalną platformy wersji.</span><span class="sxs-lookup"><span data-stu-id="19fca-126">Accept hello defaults for hello target and minimum platform versions.</span></span>

5. <span data-ttu-id="19fca-127">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy projekt aplikacji Sklepu Windows hello, kliknij przycisk **magazynu**, a następnie kliknij przycisk **Skojarz aplikację ze sklepu hello...** . hello **kojarzenie aplikacji ze Sklepu Windows hello** zostanie wyświetlony Kreator.</span><span class="sxs-lookup"><span data-stu-id="19fca-127">In Solution Explorer, right-click hello Windows Store app project, click **Store**, and then click **Associate App with hello Store...**. hello **Associate Your App with hello Windows Store** wizard appears.</span></span>

6. <span data-ttu-id="19fca-128">W Kreatorze hello Zaloguj się przy użyciu konta Microsoft.</span><span class="sxs-lookup"><span data-stu-id="19fca-128">In hello wizard, sign in with your Microsoft account.</span></span>

7. <span data-ttu-id="19fca-129">Kliknij aplikację hello zarejestrowaną w kroku 2, kliknij przycisk **dalej**, a następnie kliknij przycisk **skojarzyć**.</span><span class="sxs-lookup"><span data-stu-id="19fca-129">Click hello app that you registered in step 2, click **Next**, and then click **Associate**.</span></span> <span data-ttu-id="19fca-130">Spowoduje to dodanie manifest aplikacji toohello informacji o rejestracji Sklepu Windows hello wymagane.</span><span class="sxs-lookup"><span data-stu-id="19fca-130">This adds hello required Windows Store registration information toohello application manifest.</span></span>

8. <span data-ttu-id="19fca-131">Wstecz na powitania [Centrum deweloperów systemu Windows](http://dev.windows.com/overview) dla nowej aplikacji kliknij pozycję **usług**, kliknij przycisk **powiadomienia wypychane**, a następnie kliknij przycisk **WNS/MPNS**.</span><span class="sxs-lookup"><span data-stu-id="19fca-131">Back on hello [Windows Dev Center](http://dev.windows.com/overview) page for your new app, click **Services**, click **Push notifications**, and then click **WNS/MPNS**.</span></span>

9. <span data-ttu-id="19fca-132">Kliknij pozycję **Nowe powiadomienie**.</span><span class="sxs-lookup"><span data-stu-id="19fca-132">Click **New Notification**.</span></span>

10. <span data-ttu-id="19fca-133">Kliknij szablon **Puste (wyskakujące)**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="19fca-133">Click **Blank (Toast)** template and then click **OK**.</span></span>

11. <span data-ttu-id="19fca-134">Wprowadź **Nazwę** powiadomienia i komunikat **Kontekst** wizualizacji.</span><span class="sxs-lookup"><span data-stu-id="19fca-134">Enter a notification **Name** and Visual **Context** message.</span></span> <span data-ttu-id="19fca-135">Następnie kliknij pozycję **Zapisz jako wersję roboczą**.</span><span class="sxs-lookup"><span data-stu-id="19fca-135">Then click **Save as draft**.</span></span>

12. <span data-ttu-id="19fca-136">Przejdź toohello [portalu rejestracji aplikacji](http://apps.dev.microsoft.com) i zaloguj się.</span><span class="sxs-lookup"><span data-stu-id="19fca-136">Navigate toohello [Application Registration Portal](http://apps.dev.microsoft.com) and log in.</span></span>

13. <span data-ttu-id="19fca-137">Kliknij nazwę swojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="19fca-137">Click on your application name.</span></span> <span data-ttu-id="19fca-138">Zanotuj hello **klucz tajny aplikacji** hasło i hello **identyfikator zabezpieczeń (SID) pakietu** znajduje się w hello **Sklepu Windows** ustawienia platformy.</span><span class="sxs-lookup"><span data-stu-id="19fca-138">Make a note of hello **Application Secret** password and hello **Package security identifier (SID)** located in hello **Windows Store** platform settings.</span></span>

     > [AZURE.WARNING]
    <span data-ttu-id="19fca-139">klucz tajny aplikacji Hello i identyfikatora SID pakietu są ważnymi poświadczeniami zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="19fca-139">hello application secret and package SID are important security credentials.</span></span> <span data-ttu-id="19fca-140">Nie udostępniaj nikomu tych wartości ani nie rozpowszechniaj ich razem z aplikacją.</span><span class="sxs-lookup"><span data-stu-id="19fca-140">Do not share these values with anyone or distribute them with your app.</span></span>

## <a name="configure-your-notification-hub"></a><span data-ttu-id="19fca-141">Konfigurowanie centrum powiadomień</span><span class="sxs-lookup"><span data-stu-id="19fca-141">Configure your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p><span data-ttu-id="19fca-142">Wybierz hello <b>usługi powiadomień</b> opcja i hello <b>systemu Windows (WNS)</b> opcji.</span><span class="sxs-lookup"><span data-stu-id="19fca-142">Select hello <b>Notification Services</b> option and hello <b>Windows (WNS)</b> option.</span></span> <span data-ttu-id="19fca-143">Następnie wprowadź hello <b>klucz tajny aplikacji</b> hasło w hello <b>klucz zabezpieczeń</b> pola.</span><span class="sxs-lookup"><span data-stu-id="19fca-143">Then enter hello <b>Application secret</b> password in hello <b>Security Key</b> field.</span></span> <span data-ttu-id="19fca-144">Wprowadź użytkownika <b>identyfikatora SID pakietu</b> wartość uzyskane z usługi WNS w poprzedniej sekcji hello, a następnie kliknij przycisk <b>zapisać</b>.</span><span class="sxs-lookup"><span data-stu-id="19fca-144">Enter your <b>Package SID</b> value that you obtained from WNS in hello previous section, and then click <b>Save</b>.</span></span></p>
</li>
</ol>

&emsp;&emsp;![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-configure-wns.png)

<span data-ttu-id="19fca-145">Centrum powiadomień jest teraz skonfigurowany toowork z usługą WNS i mieć tooregister ciągów połączenia hello aplikacji oraz wysyłać powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="19fca-145">Your notification hub is now configured toowork with WNS, and you have hello connection strings tooregister your app and send notifications.</span></span>

## <a name="connect-your-app-toohello-notification-hub"></a><span data-ttu-id="19fca-146">Łączenie aplikacji toohello Centrum powiadomień</span><span class="sxs-lookup"><span data-stu-id="19fca-146">Connect your app toohello notification hub</span></span>
1. <span data-ttu-id="19fca-147">W programie Visual Studio, kliknij prawym przyciskiem myszy rozwiązanie hello, a następnie kliknij przycisk **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="19fca-147">In Visual Studio, right-click hello solution, and then click **Manage NuGet Packages**.</span></span>
   
    <span data-ttu-id="19fca-148">Spowoduje to wyświetlenie hello **Zarządzaj pakietami NuGet** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="19fca-148">This displays hello **Manage NuGet Packages** dialog box.</span></span>
2. <span data-ttu-id="19fca-149">Wyszukaj `WindowsAzure.Messaging.Managed` i kliknij przycisk **zainstalować**i zaakceptuj warunki użytkowania hello.</span><span class="sxs-lookup"><span data-stu-id="19fca-149">Search for `WindowsAzure.Messaging.Managed` and click **Install**, and accept hello terms of use.</span></span>
   
    ![][20]
   
    <span data-ttu-id="19fca-150">To spowoduje pobranie, instaluje i dodaje odwołanie do biblioteki Azure Messaging toohello dla systemu Windows za pomocą hello <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">pakietu WindowsAzure.Messaging.Managed NuGet</a>.</span><span class="sxs-lookup"><span data-stu-id="19fca-150">This downloads, installs, and adds a reference toohello Azure Messaging library for Windows by using hello <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet package</a>.</span></span>
3. <span data-ttu-id="19fca-151">Otwórz plik projektu App.xaml.cs hello i dodaj następujące hello `using` instrukcje.</span><span class="sxs-lookup"><span data-stu-id="19fca-151">Open hello App.xaml.cs project file and add hello following `using` statements.</span></span> 
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.UI.Popups;
4. <span data-ttu-id="19fca-152">Również w pliku App.xaml.cs Dodaj następujące hello **InitNotificationsAsync** toohello definicję metody **aplikacji** klasy:</span><span class="sxs-lookup"><span data-stu-id="19fca-152">Also in App.xaml.cs, add hello following **InitNotificationsAsync** method definition toohello **App** class:</span></span>
   
        private async void InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            var hub = new NotificationHub("< your hub name>", "<Your DefaultListenSharedAccessSignature connection string>");
            var result = await hub.RegisterNativeAsync(channel.Uri);
   
            // Displays hello registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
   
        }
   
    <span data-ttu-id="19fca-153">Ten kod pobiera identyfikator URI kanału hello aplikacji hello z usługi WNS, a następnie rejestruje ten identyfikator URI kanału w Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="19fca-153">This code retrieves hello channel URI for hello app from WNS, and then registers that channel URI with your notification hub.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="19fca-154">Upewnij się, że tooreplace hello symbolu zastępczego "Twoje hub name" nazwą hello hello Centrum powiadomień wyświetlaną w portalu Azure hello.</span><span class="sxs-lookup"><span data-stu-id="19fca-154">Make sure tooreplace hello "your hub name" placeholder with hello name of hello notification hub that appears in hello Azure Portal.</span></span> <span data-ttu-id="19fca-155">Również Zastąp symbol zastępczy parametrów połączenia hello hello **DefaultListenSharedAccessSignature** ciąg połączenia, który został uzyskany z hello **zasady dostępu** strony w Centrum powiadomień poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="19fca-155">Also replace hello connection string placeholder with hello **DefaultListenSharedAccessSignature** connection string that you obtained from hello **Access Polices** page of your Notification Hub in a previous section.</span></span>
   > 
   > 
5. <span data-ttu-id="19fca-156">U góry hello hello **OnLaunched** obsługi zdarzeń w pliku App.xaml.cs Dodaj hello następujące nowe toohello wywołania **InitNotificationsAsync** metody:</span><span class="sxs-lookup"><span data-stu-id="19fca-156">At hello top of hello **OnLaunched** event handler in App.xaml.cs, add hello following call toohello new **InitNotificationsAsync** method:</span></span>
   
        InitNotificationsAsync();
   
    <span data-ttu-id="19fca-157">Gwarantuje to tego kanału hello. identyfikator URI jest rejestrowany w Centrum powiadomień, które każda aplikacja hello czasu jest uruchamiana.</span><span class="sxs-lookup"><span data-stu-id="19fca-157">This guarantees that hello channel URI is registered in your notification hub each time hello application is launched.</span></span>
6. <span data-ttu-id="19fca-158">Naciśnij klawisz hello **F5** aplikacji hello toorun klucza.</span><span class="sxs-lookup"><span data-stu-id="19fca-158">Press hello **F5** key toorun hello app.</span></span> <span data-ttu-id="19fca-159">Podręczne okno dialogowe, który zawiera klucz rejestracji hello jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="19fca-159">A pop-up dialog that contains hello registration key is displayed.</span></span>

<span data-ttu-id="19fca-160">Aplikacja jest teraz gotowy tooreceive wyskakujące powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="19fca-160">Your app is now ready tooreceive toast notifications.</span></span>

## <a name="send-notifications"></a><span data-ttu-id="19fca-161">Wysyłanie powiadomień</span><span class="sxs-lookup"><span data-stu-id="19fca-161">Send notifications</span></span>
<span data-ttu-id="19fca-162">Możesz szybko przetestować odbieranie powiadomień w aplikacji, wysyłając powiadomienia w hello [Azure Portal](https://portal.azure.com/) przy użyciu hello **wysyłanie testowe** znajdującego się na powitania Centrum powiadomień, jak pokazano na poniższym zrzucie ekranu hello.</span><span class="sxs-lookup"><span data-stu-id="19fca-162">You can quickly test receiving notifications in your app by sending notifications in hello [Azure Portal](https://portal.azure.com/) using hello **Test Send** button on hello notification hub, as shown in hello screen below.</span></span>

![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-test-send-wns.png)

<span data-ttu-id="19fca-163">Powiadomienia wypychane są zwykle wysyłane za pośrednictwem usługi zaplecza, takiej jak Mobile Services czy ASP.NET, z użyciem zgodnej biblioteki.</span><span class="sxs-lookup"><span data-stu-id="19fca-163">Push notifications are normally sent in a back-end service like Mobile Services or ASP.NET using a compatible library.</span></span> <span data-ttu-id="19fca-164">Umożliwia także hello interfejsu API REST bezpośrednio toosend powiadomień wiadomości, jeśli biblioteka nie jest dostępna dla sieci wewnętrznej.</span><span class="sxs-lookup"><span data-stu-id="19fca-164">You can also use hello REST API directly toosend notification messages if a library is not available for your back-end.</span></span> 

<span data-ttu-id="19fca-165">W tym samouczku będziemy Zachowaj prostotę i przedstawiono testowanie aplikacji klienckiej przez wysyłanie powiadomień dotyczących usługi notification hubs w aplikacji konsoli usługi zaplecza przy użyciu hello zestawu .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="19fca-165">In this tutorial, we will keep it simple and just demonstrate testing your client app by sending notifications using hello .NET SDK for notification hubs in a console application instead of a backend service.</span></span> <span data-ttu-id="19fca-166">Firma Microsoft zaleca hello [toousers powiadomienia toopush użyciu usługi Notification Hubs] samouczka jako hello następnego kroku do wysyłania powiadomień z zaplecza ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="19fca-166">We recommend hello [Use Notification Hubs toopush notifications toousers] tutorial as hello next step for sending notifications from an ASP.NET backend.</span></span> <span data-ttu-id="19fca-167">Jednak po podejścia hello może służyć do wysyłania powiadomień:</span><span class="sxs-lookup"><span data-stu-id="19fca-167">However, hello following approaches can be used for sending notifications:</span></span>

* <span data-ttu-id="19fca-168">**Interfejs REST**: powiadomienia mogą być obsługiwane na dowolnej platformie zaplecza za pomocą hello [interfejsu REST](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="19fca-168">**REST Interface**:  You can support notification on any backend platform using  hello [REST interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span></span>
* <span data-ttu-id="19fca-169">**Microsoft Azure powiadomień koncentratory .NET SDK**: W hello Menedżera pakietów Nuget dla programu Visual Studio, uruchom [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="19fca-169">**Microsoft Azure Notification Hubs .NET SDK**: In hello Nuget Package Manager for Visual Studio, run [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>
* <span data-ttu-id="19fca-170">**Node.js** : [jak toouse centra powiadomień w oprogramowaniu Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="19fca-170">**Node.js** : [How toouse Notification Hubs from Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span></span>
* <span data-ttu-id="19fca-171">**Aplikacje mobilne platformy Azure**: na przykład jak toosend powiadomienia z aplikacji mobilnej Azure, który jest zintegrowany z usługą Notification Hubs, zobacz [Dodawanie powiadomień wypychanych do aplikacji mobilnej](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="19fca-171">**Azure Mobile Apps**: For an example of how toosend notifications from an Azure Mobile App that's integrated with Notification Hubs, see [Add push notifications for Mobile Apps](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span></span>
* <span data-ttu-id="19fca-172">**Java / PHP**: przykład sposobu toosend powiadomienia za pomocą hello interfejsów API REST, zobacz "jak toouse usługi Notification Hubs za pomocą języka Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span><span class="sxs-lookup"><span data-stu-id="19fca-172">**Java / PHP**: For an example of how toosend notifications by using hello REST APIs, see "How toouse Notification Hubs from Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span></span>

## <a name="optional-send-notifications-from-a-console-app"></a><span data-ttu-id="19fca-173">(Opcjonalnie) Wysyłanie powiadomień z poziomu aplikacji konsolowej</span><span class="sxs-lookup"><span data-stu-id="19fca-173">(Optional) Send notifications from a console app</span></span>
<span data-ttu-id="19fca-174">toosend powiadomienia za pomocą aplikacji konsoli .NET, wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="19fca-174">toosend notifications by using a .NET console application follow these steps.</span></span> 

1. <span data-ttu-id="19fca-175">Rozwiązanie powitania kliknij prawym przyciskiem myszy, wybierz opcję **Dodaj** i **nowy projekt...** , a następnie w obszarze **Visual C#**, kliknij przycisk **Windows** i **aplikacji konsoli**i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="19fca-175">Right-click hello solution, select **Add** and **New Project...**, and then under **Visual C#**, click **Windows** and **Console Application**, and click **OK**.</span></span>
   
    <span data-ttu-id="19fca-176">Spowoduje to dodanie nowego Visual C# console application toohello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="19fca-176">This adds a new Visual C# console application toohello solution.</span></span> <span data-ttu-id="19fca-177">Można to również zrobić w oddzielnym rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="19fca-177">You can also do this in a separate solution.</span></span>

2. <span data-ttu-id="19fca-178">W programie Visual Studio kliknij kolejno pozycje **Narzędzia**, **Menedżer pakietów NuGet**, **Konsola menedżera pakietów**.</span><span class="sxs-lookup"><span data-stu-id="19fca-178">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="19fca-179">Spowoduje to wyświetlenie konsoli Menedżera pakietów hello w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="19fca-179">This displays hello Package Manager Console in Visual Studio.</span></span>
3. <span data-ttu-id="19fca-180">W oknie konsoli Menedżera pakietów hello, ustaw hello **domyślny projekt** tooyour nowy projekt aplikacji konsoli, a następnie w oknie konsoli hello, wykonaj następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="19fca-180">In hello Package Manager Console window, set hello **Default project** tooyour new console application project, and then in hello console window, execute hello following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="19fca-181">Spowoduje to dodanie toohello odwołanie do zestawu SDK usługi Azure Notification Hubs za pomocą hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pakietu Microsoft.Azure.Notification Hubs NuGet</a>.</span><span class="sxs-lookup"><span data-stu-id="19fca-181">This adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. <span data-ttu-id="19fca-182">Otwórz plik Program.cs hello i dodaj następujące hello `using` instrukcji:</span><span class="sxs-lookup"><span data-stu-id="19fca-182">Open hello Program.cs file and add hello following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="19fca-183">W hello **Program** klasy, Dodaj hello następujące metody:</span><span class="sxs-lookup"><span data-stu-id="19fca-183">In hello **Program** class, add hello following method:</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient
                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">Hello from a .NET App!</text></binding></visual></toast>";
            await hub.SendWindowsNativeNotificationAsync(toast);
        }
   
       Make sure tooreplace hello "hub name" placeholder with hello name of hello notification hub that as it appears in hello Azure Portal. Also, replace hello connection string placeholder with hello **DefaultFullSharedAccessSignature** connection string that you obtained from hello **Access Policies** page of your Notification Hub in hello section called "Configure your notification hub."
   
   > [!NOTE]
   > <span data-ttu-id="19fca-184">Upewnij się, że używasz hello parametry połączenia, które ma **pełne** dostępu nie **nasłuchiwania** dostępu.</span><span class="sxs-lookup"><span data-stu-id="19fca-184">Make sure that you use hello connection string that has **Full** access, not **Listen** access.</span></span> <span data-ttu-id="19fca-185">Parametry połączenia Hello dostępu do nasłuchiwania nie mają uprawnień toosend powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="19fca-185">hello listen-access string does not have permissions toosend notifications.</span></span>
   > 
   > 
6. <span data-ttu-id="19fca-186">Dodaj następujące wiersze w hello hello **Main** metody:</span><span class="sxs-lookup"><span data-stu-id="19fca-186">Add hello following lines in hello **Main** method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="19fca-187">Kliknij prawym przyciskiem myszy projekt aplikacji hello konsoli w programie Visual Studio, a następnie kliknij przycisk **Ustaw jako projekt startowy** tooset go jako projekt startowy hello.</span><span class="sxs-lookup"><span data-stu-id="19fca-187">Right-click hello console application project in Visual Studio, and click **Set as StartUp Project** tooset it as hello startup project.</span></span> <span data-ttu-id="19fca-188">Następnie naciśnij klawisz hello **F5** aplikacji hello toorun klucza.</span><span class="sxs-lookup"><span data-stu-id="19fca-188">Then press hello **F5** key toorun hello application.</span></span>
   
    <span data-ttu-id="19fca-189">Otrzymasz wyskakujące powiadomienie na wszystkich zarejestrowanych urządzeniach.</span><span class="sxs-lookup"><span data-stu-id="19fca-189">You will receive a toast notification on all registered devices.</span></span> <span data-ttu-id="19fca-190">Kliknięcie lub naciśnięcie hello baneru wyskakującego powiadomienia spowoduje załadowanie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="19fca-190">Clicking or tapping hello toast banner loads hello app.</span></span>

<span data-ttu-id="19fca-191">Wszystkie hello obsługiwane ładunki można znaleźć w hello [wykazu powiadomień wyskakujących], [wykazu kafelków], i [omówienia znaczków] tematów w witrynie MSDN.</span><span class="sxs-lookup"><span data-stu-id="19fca-191">You can find all hello supported payloads in hello [toast catalog], [tile catalog], and [badge overview] topics on MSDN.</span></span>

## <a name="next-steps"></a><span data-ttu-id="19fca-192">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="19fca-192">Next steps</span></span>
<span data-ttu-id="19fca-193">W tym prostym przykładzie wysłano wyemitowane powiadomienia tooall urządzeń z systemem Windows za pomocą portalu hello lub aplikacji konsoli.</span><span class="sxs-lookup"><span data-stu-id="19fca-193">In this simple example, you sent broadcast notifications tooall your Windows devices using hello portal or a console app.</span></span> <span data-ttu-id="19fca-194">Firma Microsoft zaleca hello [toousers powiadomienia toopush użyciu usługi Notification Hubs] samouczka jako hello następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="19fca-194">We recommend hello [Use Notification Hubs toopush notifications toousers] tutorial as hello next step.</span></span> <span data-ttu-id="19fca-195">Przedstawiono w nim sposób toosend powiadomień z zaplecza ASP.NET za pomocą tagów tootarget określonych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="19fca-195">It will show you how toosend notifications from an ASP.NET backend using tags tootarget specific users.</span></span>

<span data-ttu-id="19fca-196">Jeśli chcesz toosegment użytkowników na grupy zainteresowań, zobacz [toosend użyciu usługi Notification Hubs fundamentalne wiadomości].</span><span class="sxs-lookup"><span data-stu-id="19fca-196">If you want toosegment your users by interest groups, see [Use Notification Hubs toosend breaking news].</span></span> 

<span data-ttu-id="19fca-197">toolearn więcej ogólnych informacji o usłudze Notification Hubs, zobacz [wskazówki dotyczące usługi Notification Hubs](notification-hubs-push-notification-overview.md).</span><span class="sxs-lookup"><span data-stu-id="19fca-197">toolearn more general information about Notification Hubs, see [Notification Hubs Guidance](notification-hubs-push-notification-overview.md).</span></span>

<!-- Images. -->
[13]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-create-console-app.png
[14]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-toast.png
[19]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-reg.png
[20]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-universal-app-install-package.png

<!-- URLs. -->

[toousers powiadomienia toopush użyciu usługi Notification Hubs]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[toosend użyciu usługi Notification Hubs fundamentalne wiadomości]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md

[wykazu powiadomień wyskakujących]: http://msdn.microsoft.com/library/windows/apps/hh761494.aspx
[wykazu kafelków]: http://msdn.microsoft.com/library/windows/apps/hh761491.aspx
[omówienia znaczków]: http://msdn.microsoft.com/library/windows/apps/hh779719.aspx
