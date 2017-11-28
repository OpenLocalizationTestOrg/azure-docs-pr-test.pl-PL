---
title: "Centra powiadomień w zlokalizowanych samouczek wiadomości podziału"
description: "Dowiedz się, jak używać usługi Azure Notification Hubs wysłać powiadomienia o zlokalizowanych najważniejszych wiadomościach."
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: 
ms.assetid: c454f5a3-a06b-45ac-91c7-f91210889b25
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: e864e832b4c50644bf4062dee29d34ff9fe2774e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-notification-hubs-to-send-localized-breaking-news"></a><span data-ttu-id="2f479-103">Wysyłanie zlokalizowanych najważniejszych wiadomości przy użyciu usługi Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="2f479-103">Use Notification Hubs to send localized breaking news</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2f479-104">Sklep Windows C#</span><span class="sxs-lookup"><span data-stu-id="2f479-104">Windows Store C#</span></span>](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [<span data-ttu-id="2f479-105">iOS</span><span class="sxs-lookup"><span data-stu-id="2f479-105">iOS</span></span>](notification-hubs-ios-xplat-localized-apns-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="2f479-106">Omówienie</span><span class="sxs-lookup"><span data-stu-id="2f479-106">Overview</span></span>
<span data-ttu-id="2f479-107">W tym temacie przedstawiono sposób użycia **szablonu** funkcji usługi Azure Notification Hubs wysyłać powiadomienia o najważniejszych wiadomościach które zostały zlokalizowane według języka i urządzenia.</span><span class="sxs-lookup"><span data-stu-id="2f479-107">This topic shows you how to use the **template** feature of Azure Notification Hubs to broadcast breaking news notifications that have been localized by language and device.</span></span> <span data-ttu-id="2f479-108">W tym samouczku początkowo utworzony w aplikacji ze Sklepu Windows [użyciu usługi Notification Hubs wysyłanie najważniejszych wiadomości].</span><span class="sxs-lookup"><span data-stu-id="2f479-108">In this tutorial you start with the Windows Store app created in [Use Notification Hubs to send breaking news].</span></span> <span data-ttu-id="2f479-109">Po zakończeniu będzie można zarejestrować dla kategorii, które planuje się, określ język, w których chcesz otrzymywać powiadomienia, a otrzymywać tylko powiadomień wypychanych do wybranych kategorii w tym języku.</span><span class="sxs-lookup"><span data-stu-id="2f479-109">When complete, you will be able to register for categories you are interested in, specify a language in which to receive the notifications, and receive only push notifications for the selected categories in that language.</span></span>

<span data-ttu-id="2f479-110">Istnieją dwie części tego scenariusza:</span><span class="sxs-lookup"><span data-stu-id="2f479-110">There are two parts to this scenario:</span></span>

* <span data-ttu-id="2f479-111">aplikacji ze Sklepu Windows pozwala klientów urządzeń do określania języka i subskrybować podziału różne kategorie nowości;</span><span class="sxs-lookup"><span data-stu-id="2f479-111">the Windows Store app allows client devices to specify a language, and to subscribe to different breaking news categories;</span></span>
* <span data-ttu-id="2f479-112">zaplecza emituje powiadomień, przy użyciu **tag** i **szablonu** feautres usługi Azure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="2f479-112">the back-end broadcasts the notifications, using the **tag** and **template** feautres of Azure Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f479-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2f479-113">Prerequisites</span></span>
<span data-ttu-id="2f479-114">Należy zostały już wykonane [użyciu usługi Notification Hubs wysyłanie najważniejszych wiadomości] samouczka i mieć kod dostępne, ponieważ w tym samouczku bezpośrednio oparta na kod.</span><span class="sxs-lookup"><span data-stu-id="2f479-114">You must have already completed the [Use Notification Hubs to send breaking news] tutorial and have the code available, because this tutorial builds directly upon that code.</span></span>

<span data-ttu-id="2f479-115">Należy również Visual Studio 2012 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="2f479-115">You also need Visual Studio 2012 or later.</span></span>

## <a name="template-concepts"></a><span data-ttu-id="2f479-116">Pojęcia dotyczące szablonów</span><span class="sxs-lookup"><span data-stu-id="2f479-116">Template concepts</span></span>
<span data-ttu-id="2f479-117">W [użyciu usługi Notification Hubs wysyłanie najważniejszych wiadomości] utworzono aplikację, która jest używana **tagi** do subskrybowania powiadomień dla wiadomości różnych kategorii.</span><span class="sxs-lookup"><span data-stu-id="2f479-117">In [Use Notification Hubs to send breaking news] you built an app that used **tags** to subscribe to notifications for different news categories.</span></span>
<span data-ttu-id="2f479-118">Wiele aplikacji, jednak docelowy kilku rynkach i wymagają lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="2f479-118">Many apps, however, target multiple markets and require localization.</span></span> <span data-ttu-id="2f479-119">Oznacza to, że zawartość powiadomień, się muszą być lokalizowany i dostarczane do odpowiednich zestawów urządzeń.</span><span class="sxs-lookup"><span data-stu-id="2f479-119">This means that the content of the notifications themselves have to be localized and delivered to the correct set of devices.</span></span>
<span data-ttu-id="2f479-120">W tym temacie pokazano, jak używać **szablonu** funkcji usługi Notification Hubs łatwe udostępnianie powiadomienia o zlokalizowanych najważniejszych wiadomościach.</span><span class="sxs-lookup"><span data-stu-id="2f479-120">In this topic we will show how to use the **template** feature of Notification Hubs to easily deliver localized breaking news notifications.</span></span>

<span data-ttu-id="2f479-121">Uwaga: jeden sposób wysyłania powiadomień zlokalizowanych jest utworzenie wielu wersji każdego znacznika.</span><span class="sxs-lookup"><span data-stu-id="2f479-121">Note: one way to send localized notifications is to create multiple versions of each tag.</span></span> <span data-ttu-id="2f479-122">Na przykład do obsługi w języku angielskim, francuskim i mandaryński, czy potrzebujemy trzy różne znaczniki dla wiadomości world: "world_en", "world_fr" i "world_ch".</span><span class="sxs-lookup"><span data-stu-id="2f479-122">For instance, to support English, French, and Mandarin, we would need three different tags for world news: "world_en", "world_fr", and "world_ch".</span></span> <span data-ttu-id="2f479-123">Firma Microsoft następnie musi wysłać zlokalizowanej wersji wiadomości world do każdego z tych tagów.</span><span class="sxs-lookup"><span data-stu-id="2f479-123">We would then have to send a localized version of the world news to each of these tags.</span></span> <span data-ttu-id="2f479-124">W tym temacie używamy szablonów w celu uniknięcia mnożenie tagów i wymaganie wysyła wiele komunikatów.</span><span class="sxs-lookup"><span data-stu-id="2f479-124">In this topic we use templates to avoid the proliferation of tags and the requirement of sending multiple messages.</span></span>

<span data-ttu-id="2f479-125">Na wysokim poziomie szablony są sposób, aby określić, jak powinno zostać odebrane powiadomienie określonego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="2f479-125">At a high level, templates are a way to specify how a specific device should receive a notification.</span></span> <span data-ttu-id="2f479-126">Szablon określa format ładunku dokładne odwołując się do właściwości, które są częścią komunikat wysłany przez zaplecze Twojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2f479-126">The template specifies the exact payload format by referring to properties that are part of the message sent by your app back-end.</span></span> <span data-ttu-id="2f479-127">W tym przypadku firma Microsoft wyśle komunikat niezależny od ustawień regionalnych zawierający wszystkie obsługiwane języki:</span><span class="sxs-lookup"><span data-stu-id="2f479-127">In our case, we will send a locale-agnostic message containing all supported languages:</span></span>

    {
        "News_English": "...",
        "News_French": "...",
        "News_Mandarin": "..."
    }

<span data-ttu-id="2f479-128">Następnie firma Microsoft zapewnia urządzenia Zarejestruj szablon, który odwołuje się do właściwości poprawne.</span><span class="sxs-lookup"><span data-stu-id="2f479-128">Then we will ensure that devices register with a template that refers to the correct property.</span></span> <span data-ttu-id="2f479-129">Na przykład aplikacji Sklepu Windows, która chce otrzymywać wiadomości proste wyskakujące zarejestruje dla następującego szablonu z żadnych odpowiednich tagów:</span><span class="sxs-lookup"><span data-stu-id="2f479-129">For instance, a Windows Store app that wants to receive a simple toast message will register for the following template with any corresponding tags:</span></span>

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">$(News_English)</text>
        </binding>
      </visual>
    </toast>



<span data-ttu-id="2f479-130">Szablony są bardzo przydatna funkcja, możesz dowiedzieć się więcej w naszym [szablony](notification-hubs-templates-cross-platform-push-messages.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="2f479-130">Templates are a very powerful feature you can learn more about in our [Templates](notification-hubs-templates-cross-platform-push-messages.md) article.</span></span> 

## <a name="the-app-user-interface"></a><span data-ttu-id="2f479-131">Interfejs użytkownika aplikacji</span><span class="sxs-lookup"><span data-stu-id="2f479-131">The app user interface</span></span>
<span data-ttu-id="2f479-132">Firma Microsoft będzie teraz zmodyfikować aplikację fundamentalne wiadomości utworzonego w temacie [użyciu usługi Notification Hubs wysyłanie najważniejszych wiadomości] wysłać zlokalizowane fundamentalne wiadomości za pomocą szablonów.</span><span class="sxs-lookup"><span data-stu-id="2f479-132">We will now modify the Breaking News app that you created in the topic [Use Notification Hubs to send breaking news] to send localized breaking news using templates.</span></span>

<span data-ttu-id="2f479-133">W aplikacji ze Sklepu Windows:</span><span class="sxs-lookup"><span data-stu-id="2f479-133">In your Windows Store app:</span></span>

<span data-ttu-id="2f479-134">Zmień Twoje MainPage.xaml, aby uwzględnić combobox ustawień regionalnych:</span><span class="sxs-lookup"><span data-stu-id="2f479-134">Change your MainPage.xaml to include a locale combobox:</span></span>

    <Grid Margin="120, 58, 120, 80"  
            Background="{StaticResource ApplicationPageBackgroundThemeBrush}">
        <Grid.RowDefinitions>
            <RowDefinition />
            <RowDefinition />
            <RowDefinition />
            <RowDefinition />
            <RowDefinition />
            <RowDefinition />
        </Grid.RowDefinitions>
        <Grid.ColumnDefinitions>
            <ColumnDefinition />
            <ColumnDefinition />
        </Grid.ColumnDefinitions>
        <TextBlock Grid.Row="0" Grid.Column="0" Grid.ColumnSpan="2"  TextWrapping="Wrap" Text="Breaking News" FontSize="42" VerticalAlignment="Top"/>
        <ComboBox Name="Locale" HorizontalAlignment="Left" VerticalAlignment="Center" Width="200" Grid.Row="1" Grid.Column="0">
            <x:String>English</x:String>
            <x:String>French</x:String>
            <x:String>Mandarin</x:String>
        </ComboBox>
        <ToggleSwitch Header="World" Name="WorldToggle" Grid.Row="2" Grid.Column="0"/>
        <ToggleSwitch Header="Politics" Name="PoliticsToggle" Grid.Row="3" Grid.Column="0"/>
        <ToggleSwitch Header="Business" Name="BusinessToggle" Grid.Row="4" Grid.Column="0"/>
        <ToggleSwitch Header="Technology" Name="TechnologyToggle" Grid.Row="2" Grid.Column="1"/>
        <ToggleSwitch Header="Science" Name="ScienceToggle" Grid.Row="3" Grid.Column="1"/>
        <ToggleSwitch Header="Sports" Name="SportsToggle" Grid.Row="4" Grid.Column="1"/>
        <Button Content="Subscribe" HorizontalAlignment="Center" Grid.Row="5" Grid.Column="0" Grid.ColumnSpan="2" Click="SubscribeButton_Click" />
    </Grid>

## <a name="building-the-windows-store-client-app"></a><span data-ttu-id="2f479-135">Tworzenie aplikacji ze Sklepu Windows klienta</span><span class="sxs-lookup"><span data-stu-id="2f479-135">Building the Windows Store client app</span></span>
1. <span data-ttu-id="2f479-136">W klasie powiadomień należy dodać parametr ustawień regionalnych użytkownika *StoreCategoriesAndSubscribe* i *SubscribeToCateories* metody.</span><span class="sxs-lookup"><span data-stu-id="2f479-136">In your Notifications class, add a locale parameter to your  *StoreCategoriesAndSubscribe* and *SubscribeToCateories* methods.</span></span>
   
        public async Task<Registration> StoreCategoriesAndSubscribe(string locale, IEnumerable<string> categories)
        {
            ApplicationData.Current.LocalSettings.Values["categories"] = string.Join(",", categories);
            ApplicationData.Current.LocalSettings.Values["locale"] = locale;
            return await SubscribeToCategories(categories);
        }
   
        public async Task<Registration> SubscribeToCategories(string locale, IEnumerable<string> categories = null)
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            if (categories == null)
            {
                categories = RetrieveCategories();
            }
   
            // Using a template registration. This makes supporting notifications across other platforms much easier.
            // Using the localized tags based on locale selected.
            string templateBodyWNS = String.Format("<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(News_{0})</text></binding></visual></toast>", locale);
   
            return await hub.RegisterTemplateAsync(channel.Uri, templateBodyWNS, "localizedWNSTemplateExample", categories);
        }
   
    <span data-ttu-id="2f479-137">Należy pamiętać, że zamiast wywoływać metodę *RegisterNativeAsync* metody nazywamy *RegisterTemplateAsync*: Firma Microsoft rejestracji format określonych powiadomień, w którym szablon jest zależny od ustawień regionalnych.</span><span class="sxs-lookup"><span data-stu-id="2f479-137">Note that instead of calling the *RegisterNativeAsync* method we call *RegisterTemplateAsync*: we are registering a specific notification format in which the template depends on the locale.</span></span> <span data-ttu-id="2f479-138">Również udostępniamy nazwę dla szablonu ("localizedWNSTemplateExample"), ponieważ chcemy zarejestrować więcej niż jednego szablonu (na przykład jeden dla wyskakujące powiadomienia) i drugi dla kafelków i musimy ich nazw, aby można było zaktualizować lub usunąć je.</span><span class="sxs-lookup"><span data-stu-id="2f479-138">We also provide a name for the template ("localizedWNSTemplateExample"), because we might want to register more than one template (for instance one for toast notifications and one for tiles) and we need to name them in order to be able to update or delete them.</span></span>
   
    <span data-ttu-id="2f479-139">Należy pamiętać, że jeśli urządzenie rejestruje wiele szablonów z tym samym tagiem, przychodzących wiadomości przeznaczonych dla który tag spowoduje wiele powiadomień dostarczony do urządzenia, (po jednej dla każdego szablonu).</span><span class="sxs-lookup"><span data-stu-id="2f479-139">Note that if a device registers multiple templates with the same tag, an incoming message targeting that tag will result in multiple notifications delivered to the device (one for each template).</span></span> <span data-ttu-id="2f479-140">To zachowanie jest przydatne, gdy ten sam komunikat logiczne ma zastosowanie w wielu powiadomienia wizualne, na przykład zawierający wskaźnika i użyciu powiadomienia wyskakującego w aplikacji Sklepu Windows.</span><span class="sxs-lookup"><span data-stu-id="2f479-140">This behavior is useful when the same logical message has to result in multiple visual notifications, for instance showing both a badge and a toast in a Windows Store application.</span></span>
2. <span data-ttu-id="2f479-141">Dodaj następującą metodę do pobrania przechowywane ustawienia regionalne:</span><span class="sxs-lookup"><span data-stu-id="2f479-141">Add the following method to retrieve the stored locale:</span></span>
   
        public string RetrieveLocale()
        {
            var locale = (string) ApplicationData.Current.LocalSettings.Values["locale"];
            return locale != null ? locale : "English";
        }
3. <span data-ttu-id="2f479-142">W Twojej MainPage.xaml.cs aktualizacji przycisk kliknij programu obsługi pobierania bieżącą wartość pola kombi ustawień regionalnych i zapewnienie wywołanie klasy powiadomień, jak pokazano:</span><span class="sxs-lookup"><span data-stu-id="2f479-142">In your MainPage.xaml.cs, update your button click handler by retrieving the current value of the Locale combo box and providing it to the call to the Notifications class, as shown:</span></span>
   
        private async void SubscribeButton_Click(object sender, RoutedEventArgs e)
        {
            var locale = (string)Locale.SelectedItem;
   
            var categories = new HashSet<string>();
            if (WorldToggle.IsOn) categories.Add("World");
            if (PoliticsToggle.IsOn) categories.Add("Politics");
            if (BusinessToggle.IsOn) categories.Add("Business");
            if (TechnologyToggle.IsOn) categories.Add("Technology");
            if (ScienceToggle.IsOn) categories.Add("Science");
            if (SportsToggle.IsOn) categories.Add("Sports");
   
            var result = await ((App)Application.Current).notifications.StoreCategoriesAndSubscribe(locale,
                 categories);
   
            var dialog = new MessageDialog("Locale: " + locale + " Subscribed to: " + 
                string.Join(",", categories) + " on registration Id: " + result.RegistrationId);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
4. <span data-ttu-id="2f479-143">Na koniec w pliku App.xaml.cs, upewnij się, że aktualizacja Twojego `InitNotificationsAsync` metody do pobierania ustawień regionalnych i użycia jej w przypadku subskrypcji:</span><span class="sxs-lookup"><span data-stu-id="2f479-143">Finally, in your App.xaml.cs file, make sure to update your `InitNotificationsAsync` method to retrieve the locale and use it when subscribing:</span></span>
   
        private async void InitNotificationsAsync()
        {
            var result = await notifications.SubscribeToCategories(notifications.RetrieveLocale());
   
            // Displays the registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
        }

## <a name="send-localized-notifications-from-your-back-end"></a><span data-ttu-id="2f479-144">Wysyłanie powiadomień zlokalizowanych z poziomu zaplecza</span><span class="sxs-lookup"><span data-stu-id="2f479-144">Send localized notifications from your back-end</span></span>
[!INCLUDE [notification-hubs-localized-back-end](../../includes/notification-hubs-localized-back-end.md)]

<!-- Anchors. -->
[Template concepts]: #concepts
[The app user interface]: #ui
[Building the Windows Store client app]: #building-client
[Send notifications from your back-end]: #send
[Next Steps]:#next-steps

<!-- Images. -->

<!-- URLs. -->
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notify users with Notification Hubs: ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Notify users with Notification Hubs: Mobile Services]: /manage/services/notification-hubs/notify-users
<span data-ttu-id="2f479-145">[użyciu usługi Notification Hubs wysyłanie najważniejszych wiadomości]: /manage/services/notification-hubs/breaking-news-dotnet</span><span class="sxs-lookup"><span data-stu-id="2f479-145">[Use Notification Hubs to send breaking news]: /manage/services/notification-hubs/breaking-news-dotnet</span></span>

[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started/#create-new-service
[Get started with data]: /develop/mobile/tutorials/get-started-with-data-dotnet
[Get started with authentication]: /develop/mobile/tutorials/get-started-with-users-dotnet
[Get started with push notifications]: /develop/mobile/tutorials/get-started-with-push-dotnet
[Push notifications to app users]: /develop/mobile/tutorials/push-notifications-to-app-users-dotnet
[Authorize users with scripts]: /develop/mobile/tutorials/authorize-users-in-scripts-dotnet
[JavaScript and HTML]: /develop/mobile/tutorials/get-started-with-push-js

[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-To for iOS]: http://msdn.microsoft.com/library/jj927168.aspx
[Notification Hubs How-To for Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
