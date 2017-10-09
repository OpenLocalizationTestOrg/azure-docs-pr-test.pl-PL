---
title: "aaaAzure Powiadom użytkowników centra powiadomień z zaplecza programu .NET"
description: "Dowiedz się, jak bezpieczne toosend powiadomień wypychanych na platformie Azure. Przykłady kodu napisane w języku C# za pomocą hello interfejsu API platformy .NET."
documentationcenter: windows
author: ysxu
manager: erikre
services: notification-hubs
editor: 
ms.assetid: 012529f2-fdbc-43c4-8634-2698164b5880
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: a366181faa81e78adf4de61435ef2790c3aa29d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-notify-users-with-net-backend"></a><span data-ttu-id="0b5f8-104">Azure Notification Hubs Powiadom użytkowników z zaplecza programu .NET</span><span class="sxs-lookup"><span data-stu-id="0b5f8-104">Azure Notification Hubs Notify Users with .NET backend</span></span>
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a><span data-ttu-id="0b5f8-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="0b5f8-105">Overview</span></span>
<span data-ttu-id="0b5f8-106">Obsługa powiadomień wypychanych na platformie Azure umożliwia tooaccess łatwy w użyciu, multiplatform i wypychanych skalowanej infrastruktury, co znacznie upraszcza hello stosowania powiadomienia wypychane zarówno konsumenckie i korporacyjne aplikacji dla urządzeń przenośnych platform.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-106">Push notification support in Azure enables you tooaccess an easy-to-use, multiplatform, and scaled-out push infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span> <span data-ttu-id="0b5f8-107">Ten samouczek pokazuje, jak toosend usługi Azure Notification Hubs toouse wypychanie powiadomień tooa specyficzne dla aplikacji użytkownika na określonym urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-107">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa specific app user on a specific device.</span></span> <span data-ttu-id="0b5f8-108">Zaplecza ASP.NET WebAPI jest używane tooauthenticate klientów.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-108">An ASP.NET WebAPI backend is used tooauthenticate clients.</span></span> <span data-ttu-id="0b5f8-109">Przy użyciu hello uwierzytelniony użytkownik komputera klienckiego, a tag zostaną automatycznie dodane przez hello zaplecza toonotification rejestracji.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-109">Using hello authenticated client user, and tag will be automatically added by hello backend toonotification registration.</span></span> <span data-ttu-id="0b5f8-110">Ten tag będzie toosend używanych przez hello zaplecza toogenerate powiadomienia dla określonego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-110">This tag will be used toosend by hello backend toogenerate notifications for a specific user.</span></span> <span data-ttu-id="0b5f8-111">Aby uzyskać więcej informacji o rejestrowaniu powiadomień przy użyciu zaplecza aplikacji, zobacz temat wskazówki hello [rejestrowanie z zaplecza aplikacji](http://msdn.microsoft.com/library/dn743807.aspx).</span><span class="sxs-lookup"><span data-stu-id="0b5f8-111">For more information on registering for notifications using an app backend, see hello guidance topic [Registering from your app backend](http://msdn.microsoft.com/library/dn743807.aspx).</span></span> <span data-ttu-id="0b5f8-112">W tym samouczku, bazując na powitania Centrum powiadomień i projektu, który został utworzony w hello [Rozpoczynanie pracy z usługą Notification Hubs] samouczka.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-112">This tutorial builds on hello notification hub and project that you created in hello [Get started with Notification Hubs] tutorial.</span></span>

<span data-ttu-id="0b5f8-113">W tym samouczku jest również hello wymagań wstępnych toohello [Secure Push] samouczka.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-113">This tutorial is also hello prerequisite toohello [Secure Push] tutorial.</span></span> <span data-ttu-id="0b5f8-114">Po wykonaniu kroków hello w tym samouczku, można przejść toohello [Secure Push] samouczku przedstawiono sposób toomodify hello kodu w tym samouczku toosend powiadomienie wypychane bezpiecznie.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-114">After you have completed hello steps in this tutorial, you can proceed toohello [Secure Push] tutorial, which shows how toomodify hello code in this tutorial toosend a push notification securely.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0b5f8-115">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="0b5f8-115">Before you begin</span></span>
<span data-ttu-id="0b5f8-116">Traktujemy opinie naszych użytkowników bardzo poważnie.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-116">We do take your feedback seriously.</span></span> <span data-ttu-id="0b5f8-117">Jeśli masz trudności z wykonaniem instrukcji w tym temacie lub zalecenia dotyczące poprawy tej zawartości, prosimy o wyrażenie opinii u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-117">If you have any difficulties completing this topic, or recommendations for improving this content, we would appreciate your feedback at hello bottom of hello page.</span></span>

<span data-ttu-id="0b5f8-118">Kod ukończyć powitalnych dla tego samouczka można znaleźć w witrynie GitHub [tutaj](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span><span class="sxs-lookup"><span data-stu-id="0b5f8-118">hello completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="0b5f8-119">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="0b5f8-119">Prerequisites</span></span>
<span data-ttu-id="0b5f8-120">Przed rozpoczęciem tego samouczka należy wykonano już tych samouczków usług Mobile Services:</span><span class="sxs-lookup"><span data-stu-id="0b5f8-120">Before you start this tutorial, you must have already completed these Mobile Services tutorials:</span></span>

* <span data-ttu-id="0b5f8-121">[Rozpoczynanie pracy z usługą Notification Hubs]</span><span class="sxs-lookup"><span data-stu-id="0b5f8-121">[Get started with Notification Hubs]</span></span><br/><span data-ttu-id="0b5f8-122">Tworzenie Centrum powiadomień i zarezerwowania nazwy aplikacji hello oraz zarejestrować tooreceive powiadomienia w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-122">You create your notification hub and reserve hello app name and register tooreceive notifications in this tutorial.</span></span> <span data-ttu-id="0b5f8-123">W tym samouczku założono, że zostały już wykonane następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-123">This tutorial assumes you have already completed these steps.</span></span> <span data-ttu-id="0b5f8-124">Jeśli nie, należy wykonać czynności hello w [wprowadzenie do korzystania z usługi Notification Hubs (w Sklepie Windows)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md); w szczególności hello sekcje [rejestrowanie aplikacji dla Sklepu Windows hello](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#register-your-app-for-the-windows-store) i [Konfiguruj Centrum powiadomień](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span><span class="sxs-lookup"><span data-stu-id="0b5f8-124">If not, please follow hello steps in [Getting Started with Notification Hubs (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md); specifically, hello sections [Register your app for hello Windows Store](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#register-your-app-for-the-windows-store) and [Configure your Notification Hub](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span></span> <span data-ttu-id="0b5f8-125">W szczególności, upewnij się, że wprowadzono hello **identyfikatora SID pakietu** i **klucz tajny klienta** wartości w portalu hello w hello **Konfiguruj** karty dla Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-125">In particular, make sure that you have entered hello **Package SID** and **Client Secret** values in hello portal, in hello **Configure** tab for your notification hub.</span></span> <span data-ttu-id="0b5f8-126">Ta procedura konfiguracja jest opisana w sekcji hello [Konfigurowanie Centrum powiadomień](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span><span class="sxs-lookup"><span data-stu-id="0b5f8-126">This configuration procedure is described in hello section [Configure your Notification Hub](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span></span> <span data-ttu-id="0b5f8-127">Jest to ważny krok: Jeśli hello poświadczeń w portalu hello odpowiadają wartościom określonym dla nazwy aplikacji hello wybierzesz, powiadomień wypychanych hello nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-127">This is an important step: if hello credentials on hello portal do not match those specified for hello app name you choose, hello push notification will not succeed.</span></span>

> [!NOTE]
> <span data-ttu-id="0b5f8-128">Jeśli używasz Mobile Apps w usłudze Azure App Service jako usługi wewnętrznej bazy danych, zobacz hello [wersją funkcji Mobile Apps](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md) tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-128">If you are using Mobile Apps in Azure App Service as your backend service, see hello [Mobile Apps version](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md) of this tutorial.</span></span>
> 
> 

&nbsp;

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="update-hello-code-for-hello-client-project"></a><span data-ttu-id="0b5f8-129">Zaktualizuj kod hello powitania klienta projektu</span><span class="sxs-lookup"><span data-stu-id="0b5f8-129">Update hello code for hello client project</span></span>
<span data-ttu-id="0b5f8-130">W tej sekcji, zaktualizuj kod hello w projekcie hello zakończone dla hello [Rozpoczynanie pracy z usługą Notification Hubs] samouczka.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-130">In this section, you update hello code in hello project you completed for hello [Get started with Notification Hubs] tutorial.</span></span> <span data-ttu-id="0b5f8-131">Hello powinna już skojarzona z magazynem hello i skonfigurowany dla Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-131">hello should already be associated with hello store and configured for your notification hub.</span></span> <span data-ttu-id="0b5f8-132">W tej sekcji możesz dodać kod toocall hello WebAPI zaplecza nowej i używać go do rejestracji i wysyłania powiadomień.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-132">In this section, you will add code toocall hello new WebAPI backend and use it for registering and sending notifications.</span></span>

1. <span data-ttu-id="0b5f8-133">W programie Visual Studio Otwórz rozwiązanie hello hello utworzone dla hello [Rozpoczynanie pracy z usługą Notification Hubs] samouczka.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-133">In Visual Studio, open hello hello solution you created for hello [Get started with Notification Hubs] tutorial.</span></span>
2. <span data-ttu-id="0b5f8-134">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **(Windows 8.1)** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-134">In Solution Explorer, right-click hello **(Windows 8.1)** project and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="0b5f8-135">Na powitania po lewej stronie, kliknij przycisk **Online**.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-135">On hello left-hand side, click **Online**.</span></span>
4. <span data-ttu-id="0b5f8-136">W hello **wyszukiwania** wpisz **klienta Http**.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-136">In hello **Search** box, type **Http Client**.</span></span>
5. <span data-ttu-id="0b5f8-137">Kliknij na liście wyników hello **bibliotek klienta HTTP Microsoft**, a następnie kliknij przycisk **zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-137">In hello results list, click **Microsoft HTTP Client Libraries**, and then click **Install**.</span></span> <span data-ttu-id="0b5f8-138">Ukończenie instalacji hello.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-138">Complete hello installation.</span></span>
6. <span data-ttu-id="0b5f8-139">Po powrocie do hello NuGet **wyszukiwania** wpisz **Json.net**.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-139">Back in hello NuGet **Search** box, type **Json.net**.</span></span> <span data-ttu-id="0b5f8-140">Zainstaluj hello **Json.NET** pakietu i hello następnie zamknij okno Menedżera pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-140">Install hello **Json.NET** package, and then close hello NuGet Package Manager window.</span></span>
7. <span data-ttu-id="0b5f8-141">Powtórz powyższe kroki powitania dla hello **(Windows Phone 8.1)** hello tooinstall projektu **JSON.NET** pakietu NuGet dla projektu Windows Phone hello.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-141">Repeat hello steps above for hello **(Windows Phone 8.1)** project tooinstall hello **JSON.NET** NuGet package for hello Windows Phone project.</span></span>
8. <span data-ttu-id="0b5f8-142">W Eksploratorze rozwiązań w hello **(Windows 8.1)** projektu, kliknij dwukrotnie **MainPage.xaml** tooopen go w edytorze programu Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-142">In Solution Explorer, in hello **(Windows 8.1)** project, double-click **MainPage.xaml** tooopen it in hello Visual Studio editor.</span></span>
9. <span data-ttu-id="0b5f8-143">W hello **MainPage.xaml** kod XML, Zastąp hello `<Grid>` sekcji o hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-143">In hello **MainPage.xaml** XML code, replace hello `<Grid>` section with hello following code.</span></span> <span data-ttu-id="0b5f8-144">Ten kod dodaje pole tekstowe nazwy użytkownika i hasła, który hello użytkownika będzie uwierzytelniania w usłudze.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-144">This code adds a username and password textbox that hello user will authenticate with.</span></span> <span data-ttu-id="0b5f8-145">Dodano również pól tekstowych dla komunikatu powiadomienia hello i hello tag nazwy użytkownika, który powinny być przesyłane powiadomienia hello:</span><span class="sxs-lookup"><span data-stu-id="0b5f8-145">It also adds textboxes for hello notification message and hello username tag that should receive hello notification:</span></span>
   
        <Grid>
            <Grid.RowDefinitions>
                <RowDefinition Height="Auto"/>
                <RowDefinition Height="*"/>
            </Grid.RowDefinitions>
   
            <TextBlock Grid.Row="0" Text="Notify Users" HorizontalAlignment="Center" FontSize="48"/>
   
            <StackPanel Grid.Row="1" VerticalAlignment="Center">
                <Grid>
                    <Grid.RowDefinitions>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                    </Grid.RowDefinitions>
                    <Grid.ColumnDefinitions>
                        <ColumnDefinition></ColumnDefinition>
                        <ColumnDefinition></ColumnDefinition>
                        <ColumnDefinition></ColumnDefinition>
                    </Grid.ColumnDefinitions>
                    <TextBlock Grid.Row="0" Grid.ColumnSpan="3" Text="Username" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="UsernameTextBox" Grid.Row="1" Grid.ColumnSpan="3" Margin="20,0,20,0"/>
                    <TextBlock Grid.Row="2" Grid.ColumnSpan="3" Text="Password" FontSize="24" Margin="20,0,20,0" />
                    <PasswordBox Name="PasswordTextBox" Grid.Row="3" Grid.ColumnSpan="3" Margin="20,0,20,0"/>
   
                    <Button Grid.Row="4" Grid.ColumnSpan="3" HorizontalAlignment="Center" VerticalAlignment="Center"
                                Content="1. Login and register" Click="LoginAndRegisterClick" Margin="0,0,0,20"/>
   
                    <ToggleButton Name="toggleWNS" Grid.Row="5" Grid.Column="0" HorizontalAlignment="Right" Content="WNS" IsChecked="True" />
                    <ToggleButton Name="toggleGCM" Grid.Row="5" Grid.Column="1" HorizontalAlignment="Center" Content="GCM" />
                    <ToggleButton Name="toggleAPNS" Grid.Row="5" Grid.Column="2" HorizontalAlignment="Left" Content="APNS" />
   
                    <TextBlock Grid.Row="6" Grid.ColumnSpan="3" Text="Username Tag tooSend To" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="ToUserTagTextBox" Grid.Row="7" Grid.ColumnSpan="3" Margin="20,0,20,0" TextWrapping="Wrap" />
                    <TextBlock Grid.Row="8" Grid.ColumnSpan="3" Text="Enter Notification Message" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="NotificationMessageTextBox" Grid.Row="9" Grid.ColumnSpan="3" Margin="20,0,20,0" TextWrapping="Wrap" />
                    <Button Grid.Row="10" Grid.ColumnSpan="3" HorizontalAlignment="Center" Content="2. Send push" Click="PushClick" Name="SendPushButton" />
                </Grid>
            </StackPanel>
        </Grid>
10. <span data-ttu-id="0b5f8-146">W Eksploratorze rozwiązań w hello **(Windows Phone 8.1)** otwarciu projektu **MainPage.xaml** i Zastąp hello Windows Phone 8.1 `<Grid>` sekcji o tym samym kodzie powyżej.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-146">In Solution Explorer, in hello **(Windows Phone 8.1)** project, open **MainPage.xaml** and replace hello Windows Phone 8.1 `<Grid>` section with that same code above.</span></span> <span data-ttu-id="0b5f8-147">Interfejs Hello powinien wyglądać podobnie toowhats pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-147">hello interface should look similar toowhats shown below.</span></span>
    
    ![][13]
11. <span data-ttu-id="0b5f8-148">W Eksploratorze rozwiązań Otwórz hello **MainPage.xaml.cs** pliku hello **(Windows 8.1)** i **(Windows Phone 8.1)** projektów.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-148">In Solution Explorer, open hello **MainPage.xaml.cs** file for hello **(Windows 8.1)** and **(Windows Phone 8.1)** projects.</span></span> <span data-ttu-id="0b5f8-149">Dodaj następujące hello `using` instrukcji u góry hello oba pliki:</span><span class="sxs-lookup"><span data-stu-id="0b5f8-149">Add hello following `using` statements at hello top of both files:</span></span>
    
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Windows.Networking.PushNotifications;
        using Windows.UI.Popups;
        using System.Threading.Tasks;
12. <span data-ttu-id="0b5f8-150">W **MainPage.xaml.cs** dla hello **(Windows 8.1)** i **(Windows Phone 8.1)** projektów, Dodaj hello następującego elementu członkowskiego toohello `MainPage` klasy.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-150">In **MainPage.xaml.cs** for hello **(Windows 8.1)** and **(Windows Phone 8.1)** projects, add hello following member toohello `MainPage` class.</span></span> <span data-ttu-id="0b5f8-151">Należy się tooreplace `<Enter Your Backend Endpoint>` z hello punktu końcowego rzeczywiste wewnętrznej bazy danych uzyskany wcześniej.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-151">Be sure tooreplace `<Enter Your Backend Endpoint>` with hello your actual backend endpoint obtained previously.</span></span> <span data-ttu-id="0b5f8-152">Na przykład `http://mybackend.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-152">For example, `http://mybackend.azurewebsites.net`.</span></span>
    
        private static string BACKEND_ENDPOINT = "<Enter Your Backend Endpoint>";
13. <span data-ttu-id="0b5f8-153">Dodaj kod hello poniżej klasy MainPage toohello w **MainPage.xaml.cs** dla hello **(Windows 8.1)** i **(Windows Phone 8.1)** projektów.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-153">Add hello code below toohello MainPage class in **MainPage.xaml.cs** for hello **(Windows 8.1)** and **(Windows Phone 8.1)** projects.</span></span>
    
    <span data-ttu-id="0b5f8-154">Hello `PushClick` hello jest metoda obsługi powitania kliknij **wysyłania Push** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-154">hello `PushClick` method is hello click handler for hello **Send Push** button.</span></span> <span data-ttu-id="0b5f8-155">Wywołuje hello zaplecza tootrigger tooall powiadamiania urządzeń przy użyciu tagu nazwę użytkownika odpowiadającą hello `to_tag` parametru.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-155">It calls hello backend tootrigger a notification tooall devices with a username tag that matches hello `to_tag` parameter.</span></span> <span data-ttu-id="0b5f8-156">wiadomości powitania powiadomienia są wysyłane jako zawartość JSON w treści żądania hello.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-156">hello notification message is sent as JSON content in hello request body.</span></span>
    
    <span data-ttu-id="0b5f8-157">Hello `LoginAndRegisterClick` hello jest metoda obsługi powitania kliknij **zalogować się i Zarejestruj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-157">hello `LoginAndRegisterClick` method is hello click handler for hello **Log in and register** button.</span></span> <span data-ttu-id="0b5f8-158">Przechowuje hello basic token uwierzytelniania w magazynie lokalnym (Zauważ, że jest to dowolny token używa schematem uwierzytelniania), następnie używa `RegisterClient` tooregister dla powiadomień przy użyciu hello wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-158">It stores hello basic authentication token in local storage (note that this represents any token your authentication scheme uses), then uses `RegisterClient` tooregister for notifications using hello backend.</span></span>

        private async void PushClick(object sender, RoutedEventArgs e)
        {
            if (toggleWNS.IsChecked.Value)
            {
                await sendPush("wns", ToUserTagTextBox.Text, this.NotificationMessageTextBox.Text);
            }
            if (toggleGCM.IsChecked.Value)
            {
                await sendPush("gcm", ToUserTagTextBox.Text, this.NotificationMessageTextBox.Text);
            }
            if (toggleAPNS.IsChecked.Value)
            {
                await sendPush("apns", ToUserTagTextBox.Text, this.NotificationMessageTextBox.Text);

            }
        }

        private async Task sendPush(string pns, string userTag, string message)
        {
            var POST_URL = BACKEND_ENDPOINT + "/api/notifications?pns=" +
                pns + "&to_tag=" + userTag;

            using (var httpClient = new HttpClient())
            {
                var settings = ApplicationData.Current.LocalSettings.Values;
                httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string)settings["AuthenticationToken"]);

                try
                {
                    await httpClient.PostAsync(POST_URL, new StringContent("\"" + message + "\"",
                        System.Text.Encoding.UTF8, "application/json"));
                }
                catch (Exception ex)
                {
                    MessageDialog alert = new MessageDialog(ex.Message, "Failed toosend " + pns + " message");
                    alert.ShowAsync();
                }
            }
        }

        private async void LoginAndRegisterClick(object sender, RoutedEventArgs e)
        {
            SetAuthenticationTokenInLocalStorage();

            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

            // hello "username:<user name>" tag gets automatically added by hello message handler in hello backend.
            // hello tag passed here can be whatever other tags you may want toouse.
            try
            {
                // hello device handle used will be different depending on hello device and PNS. 
                // Windows devices use hello channel uri as hello PNS handle.
                await new RegisterClient(BACKEND_ENDPOINT).RegisterAsync(channel.Uri, new string[] { "myTag" });

                var dialog = new MessageDialog("Registered as: " + UsernameTextBox.Text);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
                SendPushButton.IsEnabled = true;
            }
            catch (Exception ex)
            {
                MessageDialog alert = new MessageDialog(ex.Message, "Failed tooregister with RegisterClient");
                alert.ShowAsync();
            }
        }

        private void SetAuthenticationTokenInLocalStorage()
        {
            string username = UsernameTextBox.Text;
            string password = PasswordTextBox.Password;

            var token = Convert.ToBase64String(System.Text.Encoding.UTF8.GetBytes(username + ":" + password));
            ApplicationData.Current.LocalSettings.Values["AuthenticationToken"] = token;
        }



1. <span data-ttu-id="0b5f8-159">W Eksploratorze rozwiązań, w obszarze hello **Shared** projektu, otwórz hello **App.xaml.cs** pliku.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-159">In Solution Explorer, under hello **Shared** project, open hello **App.xaml.cs** file.</span></span> <span data-ttu-id="0b5f8-160">Znajdowanie hello rozmowy za`InitNotificationsAsync()` w hello `OnLaunched()` obsługi zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-160">Find hello call too`InitNotificationsAsync()` in hello `OnLaunched()` event handler.</span></span> <span data-ttu-id="0b5f8-161">Komentarz lub Usuń wywołanie hello zbyt`InitNotificationsAsync()`.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-161">Comment out or delete hello call too`InitNotificationsAsync()`.</span></span> <span data-ttu-id="0b5f8-162">Obsługa przycisku Hello dodanych wcześniej zainicjuje rejestracji powiadomień.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-162">hello button handler added above will initialize notification registrations.</span></span>

        protected override void OnLaunched(LaunchActivatedEventArgs e)
        {
            //InitNotificationsAsync();


1. <span data-ttu-id="0b5f8-163">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **Shared** projektu, a następnie kliknij przycisk **Dodaj**, a następnie kliknij przycisk **klasy**.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-163">In Solution Explorer, right-click hello **Shared** project, then click **Add**, and then click **Class**.</span></span> <span data-ttu-id="0b5f8-164">Nazwa klasy hello **RegisterClient.cs**, następnie kliknij przycisk **OK** toogenerate hello klasy.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-164">Name hello class **RegisterClient.cs**, then click **OK** toogenerate hello class.</span></span>
   
   <span data-ttu-id="0b5f8-165">Ta klasa będzie zawijany hello REST wywołania wymagane toocontact hello zaplecza aplikacji, w kolejności tooregister dla powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-165">This class will wrap hello REST calls required toocontact hello app backend, in order tooregister for push notifications.</span></span> <span data-ttu-id="0b5f8-166">Przechowuje także lokalnie hello *registrationIds* utworzone przez hello Centrum powiadomień zgodnie z opisem w [rejestrowanie z zaplecza aplikacji](http://msdn.microsoft.com/library/dn743807.aspx).</span><span class="sxs-lookup"><span data-stu-id="0b5f8-166">It also locally stores hello *registrationIds* created by hello Notification Hub as detailed in [Registering from your app backend](http://msdn.microsoft.com/library/dn743807.aspx).</span></span> <span data-ttu-id="0b5f8-167">Uwaga używa tokenu autoryzacji przechowywanych w magazynie lokalnym po kliknięciu hello **zalogować się i Zarejestruj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-167">Note that it uses an authorization token stored in local storage when you click hello **Log in and register** button.</span></span>
2. <span data-ttu-id="0b5f8-168">Dodaj następujące hello `using` instrukcji u góry pliku RegisterClient.cs hello hello:</span><span class="sxs-lookup"><span data-stu-id="0b5f8-168">Add hello following `using` statements at hello top of hello RegisterClient.cs file:</span></span>
   
       using Windows.Storage;
       using System.Net;
       using System.Net.Http;
       using System.Net.Http.Headers;
       using Newtonsoft.Json;
       using System.Threading.Tasks;
       using System.Linq;
3. <span data-ttu-id="0b5f8-169">Dodaj następujące kodu wewnątrz hello hello `RegisterClient` definicji klasy.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-169">Add hello following code inside hello `RegisterClient` class definition.</span></span>
   
       private string POST_URL;
   
       private class DeviceRegistration
       {
           public string Platform { get; set; }
           public string Handle { get; set; }
           public string[] Tags { get; set; }
       }
   
       public RegisterClient(string backendEndpoint)
       {
           POST_URL = backendEndpoint + "/api/register";
       }
   
       public async Task RegisterAsync(string handle, IEnumerable<string> tags)
       {
           var regId = await RetrieveRegistrationIdOrRequestNewOneAsync();
   
           var deviceRegistration = new DeviceRegistration
           {
               Platform = "wns",
               Handle = handle,
               Tags = tags.ToArray<string>()
           };
   
           var statusCode = await UpdateRegistrationAsync(regId, deviceRegistration);
   
           if (statusCode == HttpStatusCode.Gone)
           {
               // regId is expired, deleting from local storage & recreating
               var settings = ApplicationData.Current.LocalSettings.Values;
               settings.Remove("__NHRegistrationId");
               regId = await RetrieveRegistrationIdOrRequestNewOneAsync();
               statusCode = await UpdateRegistrationAsync(regId, deviceRegistration);
           }
   
           if (statusCode != HttpStatusCode.Accepted)
           {
               // log or throw
               throw new System.Net.WebException(statusCode.ToString());
           }
       }
   
       private async Task<HttpStatusCode> UpdateRegistrationAsync(string regId, DeviceRegistration deviceRegistration)
       {
           using (var httpClient = new HttpClient())
           {
               var settings = ApplicationData.Current.LocalSettings.Values;
               httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string) settings["AuthenticationToken"]);
   
               var putUri = POST_URL + "/" + regId;
   
               string json = JsonConvert.SerializeObject(deviceRegistration);
                               var response = await httpClient.PutAsync(putUri, new StringContent(json, Encoding.UTF8, "application/json"));
               return response.StatusCode;
           }
       }
   
       private async Task<string> RetrieveRegistrationIdOrRequestNewOneAsync()
       {
           var settings = ApplicationData.Current.LocalSettings.Values;
           if (!settings.ContainsKey("__NHRegistrationId"))
           {
               using (var httpClient = new HttpClient())
               {
                   httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string)settings["AuthenticationToken"]);
   
                   var response = await httpClient.PostAsync(POST_URL, new StringContent(""));
                   if (response.IsSuccessStatusCode)
                   {
                       string regId = await response.Content.ReadAsStringAsync();
                       regId = regId.Substring(1, regId.Length - 2);
                       settings.Add("__NHRegistrationId", regId);
                   }
                   else
                   {
                       throw new System.Net.WebException(response.StatusCode.ToString());
                   }
               }
           }
           return (string)settings["__NHRegistrationId"];
   
       }
4. <span data-ttu-id="0b5f8-170">Zapisz wszystkie zmiany.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-170">Save all your changes.</span></span>

## <a name="testing-hello-application"></a><span data-ttu-id="0b5f8-171">Testowanie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="0b5f8-171">Testing hello Application</span></span>
1. <span data-ttu-id="0b5f8-172">Uruchamianie aplikacji hello na Windows 8.1 i Windows Phone 8.1.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-172">Launch hello application on both Windows 8.1 and Windows Phone 8.1.</span></span> <span data-ttu-id="0b5f8-173">Dla systemu Windows Phone 8.1 można uruchomić wystąpienie hello hello emulatora lub rzeczywistego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-173">For Windows Phone 8.1 you can run hello instance in hello emulator or an actual device.</span></span>
2. <span data-ttu-id="0b5f8-174">W wystąpieniu hello Windows 8.1 aplikacji hello, wprowadź **Username** i **hasło** jak pokazano na poniższym zrzucie ekranu hello.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-174">In hello Windows 8.1 instance of hello app, enter a **Username** and **Password** as shown in hello screen below.</span></span> <span data-ttu-id="0b5f8-175">Powinny różnić się od hello nazwy użytkownika i hasła, która została wprowadzona Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-175">It should differ from hello user name and password you enter on Windows Phone.</span></span>
3. <span data-ttu-id="0b5f8-176">Kliknij przycisk **zalogować się i Zarejestruj** i sprawdź okno dialogowe pokazuje, że użytkownik zalogował się.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-176">Click **Log in and register** and verify a dialog shows that you have logged in.</span></span> <span data-ttu-id="0b5f8-177">Umożliwi to również hello **wysyłania Push** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-177">This will also enable hello **Send Push** button.</span></span>
   
    ![][14]
4. <span data-ttu-id="0b5f8-178">W wystąpieniu hello Windows Phone 8.1, wprowadź ciąg nazwy użytkownika w obu hello **Username** i **hasło** kliknięcie pola **logowania i rejestrowanie**.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-178">On hello Windows Phone 8.1 instance, enter a user name string in both hello **Username** and **Password** fields then click **Login and register**.</span></span>
5. <span data-ttu-id="0b5f8-179">Następnie w hello **Username Tag odbiorcy** wprowadź nazwę użytkownika hello zarejestrowany na Windows 8.1.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-179">Then in hello **Recipient Username Tag** field, enter hello user name registered on Windows 8.1.</span></span> <span data-ttu-id="0b5f8-180">Wprowadź komunikat powiadomienia, a następnie kliknij przycisk **wysyłania Push**.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-180">Enter a notification message and click **Send Push**.</span></span>
   
    ![][16]
6. <span data-ttu-id="0b5f8-181">Witaj tylko te urządzenia, które zarejestrowanego hello pasującego tagu username wyświetlony komunikat powiadomienia hello.</span><span class="sxs-lookup"><span data-stu-id="0b5f8-181">Only hello devices that have registered with hello matching username tag receive hello notification message.</span></span>
   
    ![][15]

## <a name="next-steps"></a><span data-ttu-id="0b5f8-182">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0b5f8-182">Next Steps</span></span>
* <span data-ttu-id="0b5f8-183">Jeśli chcesz toosegment użytkowników na grupy zainteresowań, zobacz [toosend użyciu usługi Notification Hubs fundamentalne wiadomości].</span><span class="sxs-lookup"><span data-stu-id="0b5f8-183">If you want toosegment your users by interest groups, see [Use Notification Hubs toosend breaking news].</span></span>
* <span data-ttu-id="0b5f8-184">więcej informacji na temat toolearn toouse Notification Hubs, zobacz [wskazówki dotyczące usługi Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="0b5f8-184">toolearn more about how toouse Notification Hubs, see [Notification Hubs Guidance].</span></span>

[9]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push9.png
[10]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push10.png
[11]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push11.png
[12]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push12.png
[13]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-wp-ui.png
[14]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-windows-instance-username.png
[15]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-notification-received.png
[16]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-wp-send-message.png



<!-- URLs. -->
[Rozpoczynanie pracy z usługą Notification Hubs]: notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[Secure Push]: notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md
[toosend użyciu usługi Notification Hubs fundamentalne wiadomości]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md
[wskazówki dotyczące usługi Notification Hubs]: http://msdn.microsoft.com/library/jj927170.aspx
