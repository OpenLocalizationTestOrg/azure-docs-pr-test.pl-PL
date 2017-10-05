---
title: "Wysyłanie powiadomień wypychanych do urządzeń z systemem Windows Phone przy użyciu usługi Azure Notification Hubs | Microsoft Docs"
description: "Korzystając z tego samouczka, dowiesz się, jak wysyłać powiadomienia wypychane do aplikacji platformy Silverlight dla systemu Windows Phone 8 lub Windows Phone 8.1 przy użyciu usługi Azure Notification Hubs."
services: notification-hubs
documentationcenter: windows
keywords: powiadomienie wypychane, powiadomienia wypychane, wypychanie w systemie windows phone
author: ysxu
manager: erikre
editor: erikre
ms.assetid: d872d8dc-4658-4d65-9e71-fa8e34fae96e
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: f0bfe81f849813d146d644b32490af657b1071b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-on-windows-phone"></a><span data-ttu-id="1102b-104">Wysyłanie powiadomień wypychanych do urządzeń z systemem Windows Phone przy użyciu usługi Azure Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="1102b-104">Sending push notifications with Azure Notification Hubs on Windows Phone</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="1102b-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="1102b-105">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="1102b-106">Do wykonania kroków tego samouczka potrzebne jest aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1102b-106">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="1102b-107">Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="1102b-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="1102b-108">Aby uzyskać szczegółowe informacje, zobacz [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-phone-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="1102b-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-phone-get-started%2F).</span></span>
> 
> 

<span data-ttu-id="1102b-109">Korzystając z tego samouczka, dowiesz się, jak wysyłać powiadomienia wypychane do aplikacji platformy Silverlight dla systemu Windows Phone 8 lub Windows Phone 8.1 przy użyciu usługi Azure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="1102b-109">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a Windows Phone 8 or Windows Phone 8.1 Silverlight application.</span></span> <span data-ttu-id="1102b-110">Jeśli aplikacja ma być przeznaczona dla systemu Windows Phone 8.1 (bez użycia platformy Silverlight), dodatkowe informacje zawiera wersja dotycząca [aplikacji uniwersalnych systemu Windows](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).</span><span class="sxs-lookup"><span data-stu-id="1102b-110">If you are targeting Windows Phone 8.1 (non-Silverlight), then refer to the [Windows Universal](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) version.</span></span>
<span data-ttu-id="1102b-111">Korzystając z tego samouczka, utworzysz pustą aplikację dla systemu Windows Phone 8, która odbiera powiadomienia wypychane przy użyciu usługi powiadomień wypychanych firmy Microsoft (MPNS, Microsoft Push Notification Service).</span><span class="sxs-lookup"><span data-stu-id="1102b-111">In this tutorial, you create a blank Windows Phone 8 app that receives push notifications by using the Microsoft Push Notification Service (MPNS).</span></span> <span data-ttu-id="1102b-112">Po zakończeniu będzie można za pomocą centrum powiadomień wysyłać powiadomienia wypychane do wszystkich urządzeń z tą aplikacją.</span><span class="sxs-lookup"><span data-stu-id="1102b-112">When you're finished, you'll be able to use your notification hub to broadcast push notifications to all the devices running your app.</span></span>

> [!NOTE]
> <span data-ttu-id="1102b-113">Zestaw SDK usługi Notification Hubs dla systemu Windows Phone nie obsługuje używania usługi WNS (Windows Push Notification Service) z aplikacjami platformy Silverlight dla systemu Windows Phone 8.1.</span><span class="sxs-lookup"><span data-stu-id="1102b-113">The Notification Hubs Windows Phone SDK does not support using the Windows Push Notification Service (WNS) with Windows Phone 8.1 Silverlight apps.</span></span> <span data-ttu-id="1102b-114">Aby używać usługi WNS (zamiast usługi MPNS) z aplikacjami platformy Silverlight dla systemu Windows Phone 8.1, postępuj zgodnie z instrukcjami w [samouczku dotyczącym usługi Notification Hubs dla aplikacji platformy Silverlight dla systemu Windows Phone], w którym zastosowano interfejsy API REST.</span><span class="sxs-lookup"><span data-stu-id="1102b-114">To use WNS (instead of MPNS) with Windows Phone 8.1 Silverlight apps, follow the [Notification Hubs - Windows Phone Silverlight tutorial], which uses REST APIs.</span></span>
> 
> 

<span data-ttu-id="1102b-115">W tym samouczku został omówiony prosty scenariusz wysyłania przy użyciu usługi Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="1102b-115">The tutorial demonstrates the simple broadcast scenario in using Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1102b-116">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1102b-116">Prerequisites</span></span>
<span data-ttu-id="1102b-117">Dla tego samouczka wymagane są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="1102b-117">This tutorial requires the following:</span></span>

* <span data-ttu-id="1102b-118">Program [Visual Studio 2012 Express for Windows Phone] lub nowsza wersja.</span><span class="sxs-lookup"><span data-stu-id="1102b-118">[Visual Studio 2012 Express for Windows Phone], or a later version.</span></span>

<span data-ttu-id="1102b-119">Wykonanie czynności opisanych w tym samouczku jest wymaganiem wstępnym dla wszystkich innych samouczków usługi Notification Hubs dotyczących aplikacji dla systemu Windows Phone 8.</span><span class="sxs-lookup"><span data-stu-id="1102b-119">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Windows Phone 8 apps.</span></span>

## <a name="create-your-notification-hub"></a><span data-ttu-id="1102b-120">Tworzenie centrum powiadomień</span><span class="sxs-lookup"><span data-stu-id="1102b-120">Create your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p><span data-ttu-id="1102b-121">Kliknij sekcję <b>Usługi powiadomień</b> (w obszarze <i>Ustawienia</i>), kliknij pozycję <b>Windows Phone (MPNS)</b>, a następnie kliknij pole wyboru <b>Włącz nieuwierzytelnione wypychanie</b>.</span><span class="sxs-lookup"><span data-stu-id="1102b-121">Click the <b>Notification Services</b> section (within <i>Settings</i>), click on <b>Windows Phone (MPNS)</b> and then click the <b>Enable unauthenticated push</b> check box.</span></span></p>
</li>
</ol>

&emsp;&emsp;![Portal Azure — włączanie nieuwierzytelnionych powiadomień wypychanych](./media/notification-hubs-windows-phone-get-started/azure-portal-unauth.png)

<span data-ttu-id="1102b-123">Centrum zostało utworzone i jest skonfigurowane do wysyłania nieuwierzytelnionych powiadomień do urządzeń z systemem Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="1102b-123">Your hub is now created and configured to send unauthenticated notification for Windows Phone.</span></span>

> [!NOTE]
> <span data-ttu-id="1102b-124">W tym samouczku używana jest usługa MPNS w trybie nieuwierzytelnionym.</span><span class="sxs-lookup"><span data-stu-id="1102b-124">This tutorial uses MPNS in unauthenticated mode.</span></span> <span data-ttu-id="1102b-125">W trybie nieuwierzytelnionym usługi MPNS występują ograniczenia dotyczące powiadomień, które można wysyłać do poszczególnych kanałów.</span><span class="sxs-lookup"><span data-stu-id="1102b-125">MPNS unauthenticated mode comes with restrictions on notifications that you can send to each channel.</span></span> <span data-ttu-id="1102b-126">Usługa Notification Hubs obsługuje [tryb uwierzytelniony usługi MPNS](http://msdn.microsoft.com/library/windowsphone/develop/ff941099.aspx), umożliwiając przekazanie certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="1102b-126">Notification Hubs supports [MPNS authenticated mode](http://msdn.microsoft.com/library/windowsphone/develop/ff941099.aspx) by allowing you to upload your certificate.</span></span>
> 
> 

## <a name="connecting-your-app-to-the-notification-hub"></a><span data-ttu-id="1102b-127">Łączenie aplikacji z centrum powiadomień</span><span class="sxs-lookup"><span data-stu-id="1102b-127">Connecting your app to the notification hub</span></span>
1. <span data-ttu-id="1102b-128">W programie Visual Studio utwórz nową aplikację dla systemu Windows Phone 8.</span><span class="sxs-lookup"><span data-stu-id="1102b-128">In Visual Studio, create a new Windows Phone 8 application.</span></span>
   
       ![Visual Studio - New Project - Windows Phone App][13]
   
    <span data-ttu-id="1102b-129">W programie Visual Studio 2013 Update 2 lub nowszym zamiast tego utwórz aplikację platformy Silverlight dla systemu Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="1102b-129">In Visual Studio 2013 Update 2 or later, you instead create a Windows Phone Silverlight application.</span></span>
   
    ![Visual Studio — Nowy projekt — Pusta aplikacja — Windows Phone Silverlight][11]
2. <span data-ttu-id="1102b-131">W programie Visual Studio kliknij rozwiązanie prawym przyciskiem myszy, a następnie kliknij pozycję **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="1102b-131">In Visual Studio, right-click the solution, and then click **Manage NuGet Packages**.</span></span>
   
    <span data-ttu-id="1102b-132">Zostanie wyświetlone okno dialogowe **Zarządzanie pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="1102b-132">This displays the **Manage NuGet Packages** dialog box.</span></span>
3. <span data-ttu-id="1102b-133">Wyszukaj pakiet `WindowsAzure.Messaging.Managed` i kliknij pozycję **Zainstaluj**, a następnie zaakceptuj warunki użytkowania.</span><span class="sxs-lookup"><span data-stu-id="1102b-133">Search for `WindowsAzure.Messaging.Managed` and click **Install**, and then accept the terms of use.</span></span>
   
    ![Visual Studio — menedżer pakietów NuGet][20]
   
    <span data-ttu-id="1102b-135">Spowoduje to pobranie i zainstalowanie biblioteki Azure Messaging dla systemu Windows oraz dodanie odwołania do niej przy użyciu <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">pakietu NuGet WindowsAzure.Messaging.Managed</a>.</span><span class="sxs-lookup"><span data-stu-id="1102b-135">This downloads, installs, and adds a reference to the Azure Messaging library for Windows by using the <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet package</a>.</span></span>
4. <span data-ttu-id="1102b-136">Otwórz plik App.xaml.cs i dodaj następujące instrukcje `using`:</span><span class="sxs-lookup"><span data-stu-id="1102b-136">Open the file App.xaml.cs and add the following `using` statements:</span></span>
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
5. <span data-ttu-id="1102b-137">Dodaj następujący kod w górnej części metody **Application_Launching** w pliku App.xaml.cs:</span><span class="sxs-lookup"><span data-stu-id="1102b-137">Add the following code at the top of **Application_Launching** method in App.xaml.cs:</span></span>
   
        var channel = HttpNotificationChannel.Find("MyPushChannel");
        if (channel == null)
        {
            channel = new HttpNotificationChannel("MyPushChannel");
            channel.Open();
            channel.BindToShellToast();
        }
   
        channel.ChannelUriUpdated += new EventHandler<NotificationChannelUriEventArgs>(async (o, args) =>
        {
            var hub = new NotificationHub("<hub name>", "<connection string>");
            var result = await hub.RegisterNativeAsync(args.ChannelUri.ToString());
   
            System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() =>
            {
                MessageBox.Show("Registration :" + result.RegistrationId, "Registered", MessageBoxButton.OK);
            });
        });
   
   > [!NOTE]
   > <span data-ttu-id="1102b-138">Wartość **MyPushChannel** jest indeksem służącym do wyszukiwania istniejącego kanału w kolekcji [HttpNotificationChannel](https://msdn.microsoft.com/library/windows/apps/microsoft.phone.notification.httpnotificationchannel.aspx).</span><span class="sxs-lookup"><span data-stu-id="1102b-138">The value **MyPushChannel** is an index that is used to lookup an existing channel in the [HttpNotificationChannel](https://msdn.microsoft.com/library/windows/apps/microsoft.phone.notification.httpnotificationchannel.aspx) collection.</span></span> <span data-ttu-id="1102b-139">Jeśli nie istnieje, utwórz nowy wpis o tej nazwie.</span><span class="sxs-lookup"><span data-stu-id="1102b-139">If there isn't one there, create a new entry with that name.</span></span>
   > 
   > 
   
    <span data-ttu-id="1102b-140">Wstaw nazwę centrum i parametry połączenia o nazwie **DefaultListenSharedAccessSignature** uzyskane w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="1102b-140">Make sure to insert the name of your hub and the connection string called **DefaultListenSharedAccessSignature** that you obtained in the previous section.</span></span>
    <span data-ttu-id="1102b-141">Ten kod pobiera identyfikator URI kanału dla aplikacji z usługi MPNS, a następnie rejestruje ten identyfikator URI kanału w centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="1102b-141">This code retrieves the channel URI for the app from MPNS, and then registers that channel URI with your notification hub.</span></span> <span data-ttu-id="1102b-142">Gwarantuje również to, że identyfikator URI kanału jest rejestrowany w centrum powiadomień przy każdym uruchomieniu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1102b-142">It also guarantees that the channel URI is registered in your notification hub each time the application is launched.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="1102b-143">W tym samouczku do urządzenia wysyłane jest wyskakujące powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="1102b-143">This tutorial sends a toast notification to the device.</span></span> <span data-ttu-id="1102b-144">W przypadku wysyłania powiadomienia na kafelku należy zamiast tego wywołać metodę **BindToShellTile** na kanale.</span><span class="sxs-lookup"><span data-stu-id="1102b-144">When you send a tile notification, you must instead call the **BindToShellTile** method on the channel.</span></span> <span data-ttu-id="1102b-145">W celu obsługi wyskakujących powiadomień oraz powiadomień na kafelku należy wywołać metodę **BindToShellTile** i **BindToShellToast**.</span><span class="sxs-lookup"><span data-stu-id="1102b-145">To support both toast and tile notifications, call both **BindToShellTile** and  **BindToShellToast**.</span></span>
   > 
   > 
6. <span data-ttu-id="1102b-146">W Eksploratorze rozwiązań rozwiń węzeł **Właściwości**, otwórz plik `WMAppManifest.xml`, kliknij kartę **Możliwości** i upewnij się, że możliwość **ID_CAP_PUSH_NOTIFICATION** jest zaznaczona.</span><span class="sxs-lookup"><span data-stu-id="1102b-146">In Solution Explorer, expand **Properties**, open the `WMAppManifest.xml` file, click the **Capabilities** tab, and make sure that the **ID_CAP_PUSH_NOTIFICATION** capability is checked.</span></span>
   
       ![Visual Studio - Windows Phone App Capabilities][14]
   
       This ensures that your app can receive push notifications. Without it, any attempt to send a push notification to the app will fail.
7. <span data-ttu-id="1102b-147">Naciśnij klawisz `F5`, aby uruchomić aplikację.</span><span class="sxs-lookup"><span data-stu-id="1102b-147">Press the `F5` key to run the app.</span></span>
   
    <span data-ttu-id="1102b-148">W aplikacji zostanie wyświetlony komunikat dotyczący rejestracji.</span><span class="sxs-lookup"><span data-stu-id="1102b-148">A registration message is displayed in the app.</span></span>
8. <span data-ttu-id="1102b-149">Zamknij aplikację.</span><span class="sxs-lookup"><span data-stu-id="1102b-149">Close the app.</span></span>  
   
   > [!NOTE]
   > <span data-ttu-id="1102b-150">Aby otrzymywać wyskakujące powiadomienia wypychane, aplikacja nie może być uruchomiona na pierwszym planie.</span><span class="sxs-lookup"><span data-stu-id="1102b-150">To receive a toast push notification, the application must not be running in the foreground.</span></span>
   > 
   > 

## <a name="send-push-notifications-from-your-backend"></a><span data-ttu-id="1102b-151">Wysyłanie powiadomień wypychanych z poziomu zaplecza</span><span class="sxs-lookup"><span data-stu-id="1102b-151">Send push notifications from your backend</span></span>
<span data-ttu-id="1102b-152">Powiadomienia wypychane przy użyciu usługi Notification Hubs można wysyłać z poziomu dowolnego zaplecza za pośrednictwem publicznego <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">interfejsu REST</a>.</span><span class="sxs-lookup"><span data-stu-id="1102b-152">You can send push notifications by using Notification Hubs from any backend via the public <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST interface</a>.</span></span> <span data-ttu-id="1102b-153">W tym samouczku powiadomienia wypychane są wysyłane przy użyciu aplikacji konsolowej programu .NET.</span><span class="sxs-lookup"><span data-stu-id="1102b-153">In this tutorial, you send push notifications using a .NET console application.</span></span> 

<span data-ttu-id="1102b-154">Aby uzyskać przykład sposobu wysyłania powiadomień wypychanych z zaplecza ASP.NET WebAPI zintegrowanego z usługą Notification Hubs, zobacz [Azure Notification Hubs Notify Users with .NET backend](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) (Powiadamianie użytkowników przy użyciu usługi Azure Notification Hubs z poziomu zaplecza programu .NET).</span><span class="sxs-lookup"><span data-stu-id="1102b-154">For an example of how to send push notifications from an ASP.NET WebAPI backend that's integrated with Notification Hubs, see [Azure Notification Hubs Notify Users with .NET backend](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md).</span></span>  

<span data-ttu-id="1102b-155">Aby zapoznać się z przykładem wysyłania powiadomień wypychanych przy użyciu interfejsów [API REST](https://msdn.microsoft.com/library/azure/dn223264.aspx), zobacz [How to use Notification Hubs from Java](notification-hubs-java-push-notification-tutorial.md) (Jak używać usługi Notification Hubs za pomocą języka Java) i [How to use Notification Hubs from PHP](notification-hubs-php-push-notification-tutorial.md) (Jak używać usługi Notification Hubs za pomocą języka PHP).</span><span class="sxs-lookup"><span data-stu-id="1102b-155">For an example of how to send push notifications by using the [REST APIs](https://msdn.microsoft.com/library/azure/dn223264.aspx), check out [How to use Notification Hubs from Java](notification-hubs-java-push-notification-tutorial.md) and [How to use Notification Hubs from PHP](notification-hubs-php-push-notification-tutorial.md).</span></span>

1. <span data-ttu-id="1102b-156">Kliknij prawym przyciskiem myszy rozwiązanie, wybierz polecenie **Dodaj** i pozycję **Nowy projekt...**, a następnie w obszarze **Visual C#** kliknij pozycję **Windows** i pozycję **Aplikacja konsolowa**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="1102b-156">Right-click the solution, select **Add** and **New Project...**, and then under **Visual C#**, click **Windows** and **Console Application**, and click **OK**.</span></span>
   
       ![Visual Studio - New Project - Console Application][6]
   
    <span data-ttu-id="1102b-157">Spowoduje to dodanie nowej aplikacji konsolowej w języku Visual C# do rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="1102b-157">This adds a new Visual C# console application to the solution.</span></span> <span data-ttu-id="1102b-158">Można to również zrobić w oddzielnym rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="1102b-158">You can also do this in a separate solution.</span></span>
2. <span data-ttu-id="1102b-159">Kliknij pozycję **Narzędzia**, kliknij pozycję **Menedżer pakietów biblioteki**, a następnie kliknij pozycję **Konsola menedżera pakietów**.</span><span class="sxs-lookup"><span data-stu-id="1102b-159">Click **Tools**, click **Library Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="1102b-160">Spowoduje to wyświetlenie konsoli menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="1102b-160">This displays the Package Manager Console.</span></span>
3. <span data-ttu-id="1102b-161">W oknie **Konsola menedżera pakietów** ustaw nowy projekt aplikacji konsoli jako **Projekt domyślny**, a następnie w oknie konsoli uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="1102b-161">In the **Package Manager Console** window, set the **Default project** to your new console application project, and then in the console window, execute the following command:</span></span>
   
       Install-Package Microsoft.Azure.NotificationHubs
   
   <span data-ttu-id="1102b-162">Spowoduje to dodanie odwołania do zestawu SDK usługi Azure Notification Hubs z użyciem <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pakietu NuGet Microsoft.Azure.Notification Hubs</a>.</span><span class="sxs-lookup"><span data-stu-id="1102b-162">This adds a reference to the Azure Notification Hubs SDK using the <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
4. <span data-ttu-id="1102b-163">Otwórz plik `Program.cs` i dodaj następującą instrukcję `using`:</span><span class="sxs-lookup"><span data-stu-id="1102b-163">Open the `Program.cs` file and add the following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="1102b-164">W klasie `Program` dodaj następującą metodę:</span><span class="sxs-lookup"><span data-stu-id="1102b-164">In the `Program` class, add the following method:</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient
                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            string toast = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                "<wp:Notification xmlns:wp=\"WPNotification\">" +
                   "<wp:Toast>" +
                        "<wp:Text1>Hello from a .NET App!</wp:Text1>" +
                   "</wp:Toast> " +
                "</wp:Notification>";
            await hub.SendMpnsNativeNotificationAsync(toast);
        }
   
    <span data-ttu-id="1102b-165">Zastąp symbol zastępczy `<hub name>` nazwą centrum powiadomień wyświetlaną w portalu.</span><span class="sxs-lookup"><span data-stu-id="1102b-165">Make sure to replace the `<hub name>` placeholder with the name of the notification hub that appears in the portal.</span></span> <span data-ttu-id="1102b-166">Ponadto zastąp symbol zastępczy parametrów połączenia parametrami połączenia o nazwie **DefaultFullSharedAccessSignature** uzyskanymi w sekcji „Konfigurowanie centrum powiadomień”.</span><span class="sxs-lookup"><span data-stu-id="1102b-166">Also, replace the connection string placeholder with the connection string called **DefaultFullSharedAccessSignature** that you obtained in the section "Configure your notification hub."</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="1102b-167">Upewnij się, że użyto parametrów połączenia z uprawnieniami dostępu **Pełne**, a nie **Nasłuchiwanie**.</span><span class="sxs-lookup"><span data-stu-id="1102b-167">Make sure that you use the connection string with **Full** access, not **Listen** access.</span></span> <span data-ttu-id="1102b-168">Parametry połączenia z uprawnieniami dostępu do nasłuchiwania nie mają uprawnień do wysyłania powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="1102b-168">The listen-access string does not have permissions to send push notifications.</span></span>
   > 
   > 
6. <span data-ttu-id="1102b-169">Dodaj następujący wiersz do metody `Main`:</span><span class="sxs-lookup"><span data-stu-id="1102b-169">Add the following line in your `Main` method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="1102b-170">Z uruchomionym emulatorem systemu Windows Phone i zamkniętą aplikacją ustaw projekt aplikacji konsolowej jako domyślny projekt startowy, a następnie naciśnij klawisz `F5`, aby uruchomić aplikację.</span><span class="sxs-lookup"><span data-stu-id="1102b-170">With your Windows Phone emulator running and your app closed, set the console application project as the default startup project, and then press the `F5` key to run the app.</span></span>
   
    <span data-ttu-id="1102b-171">Otrzymasz wyskakujące powiadomienie wypychane.</span><span class="sxs-lookup"><span data-stu-id="1102b-171">You will receive a toast push notification.</span></span> <span data-ttu-id="1102b-172">Naciśnięcie baneru wyskakującego powiadomienia spowoduje załadowanie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1102b-172">Tapping the toast banner loads the app.</span></span>

<span data-ttu-id="1102b-173">Wszystkie dozwolone ładunki można znaleźć w tematach dotyczących [wykazu powiadomień wyskakujących] i [wykazu kafelków] w witrynie MSDN.</span><span class="sxs-lookup"><span data-stu-id="1102b-173">You can find all the possible payloads in the [toast catalog] and [tile catalog] topics on MSDN.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1102b-174">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1102b-174">Next steps</span></span>
<span data-ttu-id="1102b-175">W tym prostym przykładzie wysłano powiadomienia wypychane do wszystkich urządzeń z systemem Windows Phone 8.</span><span class="sxs-lookup"><span data-stu-id="1102b-175">In this simple example, you broadcasted push notifications to all your Windows Phone 8 devices.</span></span> 

<span data-ttu-id="1102b-176">Aby skierować je do określonych użytkowników, zapoznaj się z samouczkiem [Wysyłanie powiadomień wypychanych do użytkowników przy użyciu usługi Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="1102b-176">In order to target specific users, refer to the [Use Notification Hubs to push notifications to users] tutorial.</span></span> 

<span data-ttu-id="1102b-177">Jeśli chcesz podzielić użytkowników na grupy zainteresowań, zobacz [Wysyłanie najważniejszych wiadomości przy użyciu usługi Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="1102b-177">If you want to segment your users by interest groups, you can read [Use Notification Hubs to send breaking news].</span></span> 

<span data-ttu-id="1102b-178">Dowiedz się więcej o sposobie użycia usługi Notification Hubs w temacie [Wskazówki dotyczące usługi Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="1102b-178">Learn more about how to use Notification Hubs in [Notification Hubs Guidance].</span></span>

<!-- Images. -->
[6]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-console-app.png
[7]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-from-portal.png
[8]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-from-portal2.png
[9]: ./media/notification-hubs-windows-phone-get-started/notification-hub-select-from-portal.png
[10]: ./media/notification-hubs-windows-phone-get-started/notification-hub-select-from-portal2.png
[11]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-wp-silverlight-app.png
[12]: ./media/notification-hubs-windows-phone-get-started/notification-hub-connection-strings.png

[13]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-wp-app.png
[14]: ./media/notification-hubs-windows-phone-get-started/mobile-app-enable-push-wp8.png
[15]: ./media/notification-hubs-windows-phone-get-started/notification-hub-pushauth.png
[20]: ./media/notification-hubs-windows-phone-get-started/notification-hub-windows-universal-app-install-package.png
[213]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-console-app.png





<!-- URLs. -->
<span data-ttu-id="1102b-179">[Visual Studio 2012 Express for Windows Phone]: https://go.microsoft.com/fwLink/p/?LinkID=268374</span><span class="sxs-lookup"><span data-stu-id="1102b-179">[Visual Studio 2012 Express for Windows Phone]: https://go.microsoft.com/fwLink/p/?LinkID=268374</span></span>
<span data-ttu-id="1102b-180">[Wskazówki dotyczące usługi Notification Hubs]: http://msdn.microsoft.com/library/jj927170.aspx</span><span class="sxs-lookup"><span data-stu-id="1102b-180">[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx</span></span>
[MPNS authenticated mode]: http://msdn.microsoft.com/library/windowsphone/develop/ff941099(v=vs.105).aspx
<span data-ttu-id="1102b-181">[Wysyłanie powiadomień wypychanych do użytkowników przy użyciu usługi Notification Hubs]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md</span><span class="sxs-lookup"><span data-stu-id="1102b-181">[Use Notification Hubs to push notifications to users]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md</span></span>
<span data-ttu-id="1102b-182">[Wysyłanie najważniejszych wiadomości przy użyciu usługi Notification Hubs]: notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md</span><span class="sxs-lookup"><span data-stu-id="1102b-182">[Use Notification Hubs to send breaking news]: notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md</span></span>
<span data-ttu-id="1102b-183">[wykazu powiadomień wyskakujących]: http://msdn.microsoft.com/library/windowsphone/develop/jj662938(v=vs.105).aspx</span><span class="sxs-lookup"><span data-stu-id="1102b-183">[toast catalog]: http://msdn.microsoft.com/library/windowsphone/develop/jj662938(v=vs.105).aspx</span></span>
<span data-ttu-id="1102b-184">[wykazu kafelków]: http://msdn.microsoft.com/library/windowsphone/develop/hh202948(v=vs.105).aspx</span><span class="sxs-lookup"><span data-stu-id="1102b-184">[tile catalog]: http://msdn.microsoft.com/library/windowsphone/develop/hh202948(v=vs.105).aspx</span></span>
<span data-ttu-id="1102b-185">[samouczku dotyczącym usługi Notification Hubs dla aplikacji platformy Silverlight dla systemu Windows Phone]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToSLPhoneApp</span><span class="sxs-lookup"><span data-stu-id="1102b-185">[Notification Hubs - Windows Phone Silverlight tutorial]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToSLPhoneApp</span></span>

