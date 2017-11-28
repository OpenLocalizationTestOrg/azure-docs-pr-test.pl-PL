---
title: "aaaSending powiadomień wypychanych przy użyciu usługi Azure Notification Hubs na Windows Phone | Dokumentacja firmy Microsoft"
description: "Z tego samouczka, dowiesz się, jak powiadomienia toopush usługi Azure Notification Hubs toouse tooa Windows Phone 8 lub Windows Phone 8.1 Silverlight aplikacji."
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
ms.openlocfilehash: 1a0ad238fe7788ae2e4f47f02d113391af03dd1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-on-windows-phone"></a><span data-ttu-id="7e801-104">Wysyłanie powiadomień wypychanych do urządzeń z systemem Windows Phone przy użyciu usługi Azure Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="7e801-104">Sending push notifications with Azure Notification Hubs on Windows Phone</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="7e801-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="7e801-105">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="7e801-106">toocomplete tego samouczka, musi mieć aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7e801-106">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="7e801-107">Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="7e801-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="7e801-108">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-phone-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="7e801-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-phone-get-started%2F).</span></span>
> 
> 

<span data-ttu-id="7e801-109">Ten samouczek pokazuje, jak toosend usługi Azure Notification Hubs toouse push aplikacji Windows Phone 8 lub Windows Phone 8.1 Silverlight tooa powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="7e801-109">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa Windows Phone 8 or Windows Phone 8.1 Silverlight application.</span></span> <span data-ttu-id="7e801-110">Jeśli ma być przeznaczona dla Windows Phone 8.1 (z systemem innym niż platformy Silverlight), zapoznaj się toohello [uniwersalnych systemu Windows](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) wersji.</span><span class="sxs-lookup"><span data-stu-id="7e801-110">If you are targeting Windows Phone 8.1 (non-Silverlight), then refer toohello [Windows Universal](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) version.</span></span>
<span data-ttu-id="7e801-111">W tym samouczku utworzysz pustą aplikację systemu Windows Phone 8, która odbiera powiadomienia wypychane przy użyciu hello usługi powiadomień wypychanych firmy Microsoft (MPNS).</span><span class="sxs-lookup"><span data-stu-id="7e801-111">In this tutorial, you create a blank Windows Phone 8 app that receives push notifications by using hello Microsoft Push Notification Service (MPNS).</span></span> <span data-ttu-id="7e801-112">Po zakończeniu będziesz w stanie toouse Twojego toobroadcast Centrum powiadomień wypychanych powiadomienia tooall hello urządzeń z tą aplikacją.</span><span class="sxs-lookup"><span data-stu-id="7e801-112">When you're finished, you'll be able toouse your notification hub toobroadcast push notifications tooall hello devices running your app.</span></span>

> [!NOTE]
> <span data-ttu-id="7e801-113">Hello zestaw SDK usługi Notification Hubs Windows Phone nie obsługuje używania hello Push powiadomienia usługi WNS (Windows) dla aplikacji Windows Phone 8.1 Silverlight.</span><span class="sxs-lookup"><span data-stu-id="7e801-113">hello Notification Hubs Windows Phone SDK does not support using hello Windows Push Notification Service (WNS) with Windows Phone 8.1 Silverlight apps.</span></span> <span data-ttu-id="7e801-114">toouse WNS (zamiast usługi MPNS) z aplikacjami systemu Windows Phone 8.1 Silverlight, należy wykonać hello [Notification Hubs — Samouczek Windows Phone Silverlight], który używa interfejsów API REST.</span><span class="sxs-lookup"><span data-stu-id="7e801-114">toouse WNS (instead of MPNS) with Windows Phone 8.1 Silverlight apps, follow hello [Notification Hubs - Windows Phone Silverlight tutorial], which uses REST APIs.</span></span>
> 
> 

<span data-ttu-id="7e801-115">Hello samouczku został omówiony Prosty scenariusz emisji hello przy użyciu usługi Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="7e801-115">hello tutorial demonstrates hello simple broadcast scenario in using Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7e801-116">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7e801-116">Prerequisites</span></span>
<span data-ttu-id="7e801-117">Ten samouczek wymaga następujących hello:</span><span class="sxs-lookup"><span data-stu-id="7e801-117">This tutorial requires hello following:</span></span>

* <span data-ttu-id="7e801-118">Program [Visual Studio 2012 Express for Windows Phone] lub nowsza wersja.</span><span class="sxs-lookup"><span data-stu-id="7e801-118">[Visual Studio 2012 Express for Windows Phone], or a later version.</span></span>

<span data-ttu-id="7e801-119">Wykonanie czynności opisanych w tym samouczku jest wymaganiem wstępnym dla wszystkich innych samouczków usługi Notification Hubs dotyczących aplikacji dla systemu Windows Phone 8.</span><span class="sxs-lookup"><span data-stu-id="7e801-119">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Windows Phone 8 apps.</span></span>

## <a name="create-your-notification-hub"></a><span data-ttu-id="7e801-120">Tworzenie centrum powiadomień</span><span class="sxs-lookup"><span data-stu-id="7e801-120">Create your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p><span data-ttu-id="7e801-121">Kliknij przycisk hello <b>usługi powiadomień</b> sekcji (w ramach <i>ustawienia</i>), kliknij <b>Windows Phone (MPNS)</b> , a następnie kliknij przycisk hello <b>Włącz nieuwierzytelnione wypychanie </b> pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="7e801-121">Click hello <b>Notification Services</b> section (within <i>Settings</i>), click on <b>Windows Phone (MPNS)</b> and then click hello <b>Enable unauthenticated push</b> check box.</span></span></p>
</li>
</ol>

&emsp;&emsp;![Portal Azure — włączanie nieuwierzytelnionych powiadomień wypychanych](./media/notification-hubs-windows-phone-get-started/azure-portal-unauth.png)

<span data-ttu-id="7e801-123">Koncentrator jest teraz utworzony i skonfigurowany toosend nieuwierzytelnionych powiadomień dla Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="7e801-123">Your hub is now created and configured toosend unauthenticated notification for Windows Phone.</span></span>

> [!NOTE]
> <span data-ttu-id="7e801-124">W tym samouczku używana jest usługa MPNS w trybie nieuwierzytelnionym.</span><span class="sxs-lookup"><span data-stu-id="7e801-124">This tutorial uses MPNS in unauthenticated mode.</span></span> <span data-ttu-id="7e801-125">Trybie nieuwierzytelnionym usługi MPNS występują ograniczenia na wysłanie tooeach kanału powiadomień.</span><span class="sxs-lookup"><span data-stu-id="7e801-125">MPNS unauthenticated mode comes with restrictions on notifications that you can send tooeach channel.</span></span> <span data-ttu-id="7e801-126">Usługa Notification Hubs obsługuje [tryb uwierzytelniony usługi MPNS](http://msdn.microsoft.com/library/windowsphone/develop/ff941099.aspx) pozwala tooupload certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="7e801-126">Notification Hubs supports [MPNS authenticated mode](http://msdn.microsoft.com/library/windowsphone/develop/ff941099.aspx) by allowing you tooupload your certificate.</span></span>
> 
> 

## <a name="connecting-your-app-toohello-notification-hub"></a><span data-ttu-id="7e801-127">Łączenie aplikacji toohello Centrum powiadomień</span><span class="sxs-lookup"><span data-stu-id="7e801-127">Connecting your app toohello notification hub</span></span>
1. <span data-ttu-id="7e801-128">W programie Visual Studio utwórz nową aplikację dla systemu Windows Phone 8.</span><span class="sxs-lookup"><span data-stu-id="7e801-128">In Visual Studio, create a new Windows Phone 8 application.</span></span>
   
       ![Visual Studio - New Project - Windows Phone App][13]
   
    <span data-ttu-id="7e801-129">W programie Visual Studio 2013 Update 2 lub nowszym zamiast tego utwórz aplikację platformy Silverlight dla systemu Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="7e801-129">In Visual Studio 2013 Update 2 or later, you instead create a Windows Phone Silverlight application.</span></span>
   
    ![Visual Studio — Nowy projekt — Pusta aplikacja — Windows Phone Silverlight][11]
2. <span data-ttu-id="7e801-131">W programie Visual Studio, kliknij prawym przyciskiem myszy rozwiązanie hello, a następnie kliknij przycisk **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="7e801-131">In Visual Studio, right-click hello solution, and then click **Manage NuGet Packages**.</span></span>
   
    <span data-ttu-id="7e801-132">Spowoduje to wyświetlenie hello **Zarządzaj pakietami NuGet** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="7e801-132">This displays hello **Manage NuGet Packages** dialog box.</span></span>
3. <span data-ttu-id="7e801-133">Wyszukaj `WindowsAzure.Messaging.Managed` i kliknij przycisk **zainstalować**, a następnie zaakceptuj warunki użytkowania hello.</span><span class="sxs-lookup"><span data-stu-id="7e801-133">Search for `WindowsAzure.Messaging.Managed` and click **Install**, and then accept hello terms of use.</span></span>
   
    ![Visual Studio — menedżer pakietów NuGet][20]
   
    <span data-ttu-id="7e801-135">To spowoduje pobranie, instaluje i dodaje odwołanie do biblioteki Azure Messaging toohello dla systemu Windows za pomocą hello <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">pakietu WindowsAzure.Messaging.Managed NuGet</a>.</span><span class="sxs-lookup"><span data-stu-id="7e801-135">This downloads, installs, and adds a reference toohello Azure Messaging library for Windows by using hello <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet package</a>.</span></span>
4. <span data-ttu-id="7e801-136">Otwórz plik hello App.xaml.cs i dodaj następujące hello `using` instrukcji:</span><span class="sxs-lookup"><span data-stu-id="7e801-136">Open hello file App.xaml.cs and add hello following `using` statements:</span></span>
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
5. <span data-ttu-id="7e801-137">Dodaj następującego kodu u góry hello hello **Application_Launching** metody w pliku App.xaml.cs:</span><span class="sxs-lookup"><span data-stu-id="7e801-137">Add hello following code at hello top of **Application_Launching** method in App.xaml.cs:</span></span>
   
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
   > <span data-ttu-id="7e801-138">Witaj wartość **MyPushChannel** jest indeks, który jest używany toolookup istniejącego kanału w hello [HttpNotificationChannel](https://msdn.microsoft.com/library/windows/apps/microsoft.phone.notification.httpnotificationchannel.aspx) kolekcji.</span><span class="sxs-lookup"><span data-stu-id="7e801-138">hello value **MyPushChannel** is an index that is used toolookup an existing channel in hello [HttpNotificationChannel](https://msdn.microsoft.com/library/windows/apps/microsoft.phone.notification.httpnotificationchannel.aspx) collection.</span></span> <span data-ttu-id="7e801-139">Jeśli nie istnieje, utwórz nowy wpis o tej nazwie.</span><span class="sxs-lookup"><span data-stu-id="7e801-139">If there isn't one there, create a new entry with that name.</span></span>
   > 
   > 
   
    <span data-ttu-id="7e801-140">Upewnij się, że nazwa hello tooinsert parametrów połączenia koncentratora i hello wywoływana **DefaultListenSharedAccessSignature** uzyskane w poprzedniej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="7e801-140">Make sure tooinsert hello name of your hub and hello connection string called **DefaultListenSharedAccessSignature** that you obtained in hello previous section.</span></span>
    <span data-ttu-id="7e801-141">Ten kod pobiera identyfikator URI kanału hello aplikacji hello z usługi MPNS, a następnie rejestruje ten identyfikator URI kanału w Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="7e801-141">This code retrieves hello channel URI for hello app from MPNS, and then registers that channel URI with your notification hub.</span></span> <span data-ttu-id="7e801-142">Gwarantuje również tego kanału hello. identyfikator URI jest rejestrowany w Centrum powiadomień, które każda aplikacja hello czasu jest uruchamiana.</span><span class="sxs-lookup"><span data-stu-id="7e801-142">It also guarantees that hello channel URI is registered in your notification hub each time hello application is launched.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="7e801-143">W tym samouczku wysyła urządzenia toohello wyskakujące powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="7e801-143">This tutorial sends a toast notification toohello device.</span></span> <span data-ttu-id="7e801-144">W przypadku wysyłania powiadomienia na kafelku należy zamiast tego wywołać hello **BindToShellTile** metody w kanale hello.</span><span class="sxs-lookup"><span data-stu-id="7e801-144">When you send a tile notification, you must instead call hello **BindToShellTile** method on hello channel.</span></span> <span data-ttu-id="7e801-145">toosupport powiadomienia zarówno wyskakujące i kafelka, wywołać metodę **BindToShellTile** i **BindToShellToast**.</span><span class="sxs-lookup"><span data-stu-id="7e801-145">toosupport both toast and tile notifications, call both **BindToShellTile** and  **BindToShellToast**.</span></span>
   > 
   > 
6. <span data-ttu-id="7e801-146">W Eksploratorze rozwiązań rozwiń **właściwości**, otwórz hello `WMAppManifest.xml` plików, kliknij hello **możliwości** karcie i upewnij się, że hello **ID_CAP_PUSH_NOTIFICATION** jest zaznaczona.</span><span class="sxs-lookup"><span data-stu-id="7e801-146">In Solution Explorer, expand **Properties**, open hello `WMAppManifest.xml` file, click hello **Capabilities** tab, and make sure that hello **ID_CAP_PUSH_NOTIFICATION** capability is checked.</span></span>
   
       ![Visual Studio - Windows Phone App Capabilities][14]
   
       This ensures that your app can receive push notifications. Without it, any attempt toosend a push notification toohello app will fail.
7. <span data-ttu-id="7e801-147">Naciśnij klawisz hello `F5` aplikacji hello toorun klucza.</span><span class="sxs-lookup"><span data-stu-id="7e801-147">Press hello `F5` key toorun hello app.</span></span>
   
    <span data-ttu-id="7e801-148">W aplikacji hello zostanie wyświetlony komunikat rejestracji.</span><span class="sxs-lookup"><span data-stu-id="7e801-148">A registration message is displayed in hello app.</span></span>
8. <span data-ttu-id="7e801-149">Aplikacja hello Zamknij.</span><span class="sxs-lookup"><span data-stu-id="7e801-149">Close hello app.</span></span>  
   
   > [!NOTE]
   > <span data-ttu-id="7e801-150">tooreceive wyskakujące powiadomienia wypychane, aplikacja hello nie może być uruchomiona na pierwszym planie hello.</span><span class="sxs-lookup"><span data-stu-id="7e801-150">tooreceive a toast push notification, hello application must not be running in hello foreground.</span></span>
   > 
   > 

## <a name="send-push-notifications-from-your-backend"></a><span data-ttu-id="7e801-151">Wysyłanie powiadomień wypychanych z poziomu zaplecza</span><span class="sxs-lookup"><span data-stu-id="7e801-151">Send push notifications from your backend</span></span>
<span data-ttu-id="7e801-152">Można wysyłać powiadomienia wypychane przy użyciu usługi Notification Hubs z poziomu dowolnego zaplecza za pośrednictwem publicznego hello <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">interfejsu REST</a>.</span><span class="sxs-lookup"><span data-stu-id="7e801-152">You can send push notifications by using Notification Hubs from any backend via hello public <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST interface</a>.</span></span> <span data-ttu-id="7e801-153">W tym samouczku powiadomienia wypychane są wysyłane przy użyciu aplikacji konsolowej programu .NET.</span><span class="sxs-lookup"><span data-stu-id="7e801-153">In this tutorial, you send push notifications using a .NET console application.</span></span> 

<span data-ttu-id="7e801-154">Przykład sposobu toosend powiadomień wypychanych z zaplecza ASP.NET WebAPI zintegrowanego z usługą Notification Hubs, zobacz [Azure Notification Hubs Powiadom użytkowników z zaplecza programu .NET](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md).</span><span class="sxs-lookup"><span data-stu-id="7e801-154">For an example of how toosend push notifications from an ASP.NET WebAPI backend that's integrated with Notification Hubs, see [Azure Notification Hubs Notify Users with .NET backend](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md).</span></span>  

<span data-ttu-id="7e801-155">Przykład sposobu hello toosend powiadomień wypychanych przy użyciu [interfejsów API REST](https://msdn.microsoft.com/library/azure/dn223264.aspx), zapoznaj się z [jak toouse usługi Notification Hubs za pomocą języka Java](notification-hubs-java-push-notification-tutorial.md) i [jak toouse usługi Notification Hubs za pomocą języka PHP](notification-hubs-php-push-notification-tutorial.md) .</span><span class="sxs-lookup"><span data-stu-id="7e801-155">For an example of how toosend push notifications by using hello [REST APIs](https://msdn.microsoft.com/library/azure/dn223264.aspx), check out [How toouse Notification Hubs from Java](notification-hubs-java-push-notification-tutorial.md) and [How toouse Notification Hubs from PHP](notification-hubs-php-push-notification-tutorial.md).</span></span>

1. <span data-ttu-id="7e801-156">Rozwiązanie powitania kliknij prawym przyciskiem myszy, wybierz opcję **Dodaj** i **nowy projekt...** , a następnie w obszarze **Visual C#**, kliknij przycisk **Windows** i **aplikacji konsoli**i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="7e801-156">Right-click hello solution, select **Add** and **New Project...**, and then under **Visual C#**, click **Windows** and **Console Application**, and click **OK**.</span></span>
   
       ![Visual Studio - New Project - Console Application][6]
   
    <span data-ttu-id="7e801-157">Spowoduje to dodanie nowego Visual C# console application toohello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="7e801-157">This adds a new Visual C# console application toohello solution.</span></span> <span data-ttu-id="7e801-158">Można to również zrobić w oddzielnym rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="7e801-158">You can also do this in a separate solution.</span></span>
2. <span data-ttu-id="7e801-159">Kliknij pozycję **Narzędzia**, kliknij pozycję **Menedżer pakietów biblioteki**, a następnie kliknij pozycję **Konsola menedżera pakietów**.</span><span class="sxs-lookup"><span data-stu-id="7e801-159">Click **Tools**, click **Library Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="7e801-160">Spowoduje to wyświetlenie konsoli Menedżera pakietów hello.</span><span class="sxs-lookup"><span data-stu-id="7e801-160">This displays hello Package Manager Console.</span></span>
3. <span data-ttu-id="7e801-161">W hello **Konsola Menedżera pakietów** okna, zestaw hello **domyślny projekt** tooyour nowy projekt aplikacji konsoli, a następnie w oknie konsoli hello, wykonaj następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="7e801-161">In hello **Package Manager Console** window, set hello **Default project** tooyour new console application project, and then in hello console window, execute hello following command:</span></span>
   
       Install-Package Microsoft.Azure.NotificationHubs
   
   <span data-ttu-id="7e801-162">Spowoduje to dodanie toohello odwołanie do zestawu SDK usługi Azure Notification Hubs za pomocą hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pakietu Microsoft.Azure.Notification Hubs NuGet</a>.</span><span class="sxs-lookup"><span data-stu-id="7e801-162">This adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
4. <span data-ttu-id="7e801-163">Otwórz hello `Program.cs` i dodaj następujące hello `using` instrukcji:</span><span class="sxs-lookup"><span data-stu-id="7e801-163">Open hello `Program.cs` file and add hello following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="7e801-164">W hello `Program` klasy, Dodaj hello następujące metody:</span><span class="sxs-lookup"><span data-stu-id="7e801-164">In hello `Program` class, add hello following method:</span></span>
   
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
   
    <span data-ttu-id="7e801-165">Upewnij się, że hello tooreplace `<hub name>` symbol zastępczy nazwą hello hello Centrum powiadomień wyświetlaną w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="7e801-165">Make sure tooreplace hello `<hub name>` placeholder with hello name of hello notification hub that appears in hello portal.</span></span> <span data-ttu-id="7e801-166">Ponadto Zastąp symbol zastępczy parametrów połączenia hello hello parametry połączenia o nazwie **DefaultFullSharedAccessSignature** uzyskanymi w sekcji hello "Konfigurowanie Centrum powiadomień".</span><span class="sxs-lookup"><span data-stu-id="7e801-166">Also, replace hello connection string placeholder with hello connection string called **DefaultFullSharedAccessSignature** that you obtained in hello section "Configure your notification hub."</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="7e801-167">Upewnij się, że użyto parametrów połączenia hello z **pełne** dostępu nie **nasłuchiwania** dostępu.</span><span class="sxs-lookup"><span data-stu-id="7e801-167">Make sure that you use hello connection string with **Full** access, not **Listen** access.</span></span> <span data-ttu-id="7e801-168">Parametry połączenia Hello dostępu do nasłuchiwania nie mają powiadomień wypychanych toosend uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="7e801-168">hello listen-access string does not have permissions toosend push notifications.</span></span>
   > 
   > 
6. <span data-ttu-id="7e801-169">Dodaj powitania po wierszu w Twojej `Main` metody:</span><span class="sxs-lookup"><span data-stu-id="7e801-169">Add hello following line in your `Main` method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="7e801-170">Z programu Windows Phone uruchomionym emulatorem projekt aplikacji hello zamknięte, ustaw konsoli aplikacji jako hello domyślny projekt startowy, a następnie naciśnij klawisz hello `F5` aplikacji hello toorun klucza.</span><span class="sxs-lookup"><span data-stu-id="7e801-170">With your Windows Phone emulator running and your app closed, set hello console application project as hello default startup project, and then press hello `F5` key toorun hello app.</span></span>
   
    <span data-ttu-id="7e801-171">Otrzymasz wyskakujące powiadomienie wypychane.</span><span class="sxs-lookup"><span data-stu-id="7e801-171">You will receive a toast push notification.</span></span> <span data-ttu-id="7e801-172">Naciśnięcie baneru wyskakującego powiadomienia spowoduje hello ładuje aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="7e801-172">Tapping hello toast banner loads hello app.</span></span>

<span data-ttu-id="7e801-173">Wszystkie możliwe ładunki hello można znaleźć w hello [wykazu powiadomień wyskakujących] i [wykazu kafelków] tematów w witrynie MSDN.</span><span class="sxs-lookup"><span data-stu-id="7e801-173">You can find all hello possible payloads in hello [toast catalog] and [tile catalog] topics on MSDN.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7e801-174">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7e801-174">Next steps</span></span>
<span data-ttu-id="7e801-175">W tym prostym przykładzie wysłano tooall powiadomień wypychanych urządzenia Windows Phone 8.</span><span class="sxs-lookup"><span data-stu-id="7e801-175">In this simple example, you broadcasted push notifications tooall your Windows Phone 8 devices.</span></span> 

<span data-ttu-id="7e801-176">W kolejności tootarget określonych użytkowników, zapoznaj się toohello [toousers powiadomienia toopush użyciu usługi Notification Hubs] samouczka.</span><span class="sxs-lookup"><span data-stu-id="7e801-176">In order tootarget specific users, refer toohello [Use Notification Hubs toopush notifications toousers] tutorial.</span></span> 

<span data-ttu-id="7e801-177">Jeśli chcesz toosegment użytkowników na grupy zainteresowań, możesz przeczytać [toosend użyciu usługi Notification Hubs fundamentalne wiadomości].</span><span class="sxs-lookup"><span data-stu-id="7e801-177">If you want toosegment your users by interest groups, you can read [Use Notification Hubs toosend breaking news].</span></span> 

<span data-ttu-id="7e801-178">Dowiedz się więcej na temat toouse centra powiadomień w [wskazówki dotyczące usługi Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="7e801-178">Learn more about how toouse Notification Hubs in [Notification Hubs Guidance].</span></span>

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
[Visual Studio 2012 Express for Windows Phone]: https://go.microsoft.com/fwLink/p/?LinkID=268374
[wskazówki dotyczące usługi Notification Hubs]: http://msdn.microsoft.com/library/jj927170.aspx
[MPNS authenticated mode]: http://msdn.microsoft.com/library/windowsphone/develop/ff941099(v=vs.105).aspx
[toousers powiadomienia toopush użyciu usługi Notification Hubs]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[toosend użyciu usługi Notification Hubs fundamentalne wiadomości]: notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md
[wykazu powiadomień wyskakujących]: http://msdn.microsoft.com/library/windowsphone/develop/jj662938(v=vs.105).aspx
[wykazu kafelków]: http://msdn.microsoft.com/library/windowsphone/develop/hh202948(v=vs.105).aspx
[Notification Hubs — Samouczek Windows Phone Silverlight]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToSLPhoneApp

