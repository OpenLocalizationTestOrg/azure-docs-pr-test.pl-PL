---
title: "aaaNotification koncentratory zlokalizowane fundamentalne wiadomości samouczka"
description: "Dowiedz się, jak toosend usługi Azure Notification Hubs toouse zlokalizowane powiadomienia o najważniejszych wiadomościach."
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
ms.openlocfilehash: d273a6b384df311dea7b76ca83ccd94d9a989c4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-localized-breaking-news"></a><span data-ttu-id="e3121-103">Użyj usługi Notification Hubs toosend zlokalizowane najważniejszych wiadomości</span><span class="sxs-lookup"><span data-stu-id="e3121-103">Use Notification Hubs toosend localized breaking news</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e3121-104">Sklep Windows C#</span><span class="sxs-lookup"><span data-stu-id="e3121-104">Windows Store C#</span></span>](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [<span data-ttu-id="e3121-105">iOS</span><span class="sxs-lookup"><span data-stu-id="e3121-105">iOS</span></span>](notification-hubs-ios-xplat-localized-apns-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="e3121-106">Omówienie</span><span class="sxs-lookup"><span data-stu-id="e3121-106">Overview</span></span>
<span data-ttu-id="e3121-107">W tym temacie opisano sposób toouse hello **szablonu** funkcji usługi Azure Notification Hubs toobroadcast fundamentalne powiadomień wiadomości, które zostały zlokalizowane według języka i urządzenia.</span><span class="sxs-lookup"><span data-stu-id="e3121-107">This topic shows you how toouse hello **template** feature of Azure Notification Hubs toobroadcast breaking news notifications that have been localized by language and device.</span></span> <span data-ttu-id="e3121-108">W tym samouczku początkowo utworzony w aplikacji ze Sklepu Windows hello [toosend użyciu usługi Notification Hubs fundamentalne wiadomości].</span><span class="sxs-lookup"><span data-stu-id="e3121-108">In this tutorial you start with hello Windows Store app created in [Use Notification Hubs toosend breaking news].</span></span> <span data-ttu-id="e3121-109">Po zakończeniu będziesz w stanie tooregister dla kategorii, które planuje się, określ język w powiadomienia, które hello tooreceive i otrzymywać tylko powiadomienia wypychane dla kategorii hello wybrany w tym języku.</span><span class="sxs-lookup"><span data-stu-id="e3121-109">When complete, you will be able tooregister for categories you are interested in, specify a language in which tooreceive hello notifications, and receive only push notifications for hello selected categories in that language.</span></span>

<span data-ttu-id="e3121-110">Istnieją dwie części toothis scenariusza:</span><span class="sxs-lookup"><span data-stu-id="e3121-110">There are two parts toothis scenario:</span></span>

* <span data-ttu-id="e3121-111">Aplikacja ze Sklepu Windows Hello umożliwia klienta urządzenia toospecify język i toodifferent toosubscribe fundamentalne kategorie nowości;</span><span class="sxs-lookup"><span data-stu-id="e3121-111">hello Windows Store app allows client devices toospecify a language, and toosubscribe toodifferent breaking news categories;</span></span>
* <span data-ttu-id="e3121-112">Witaj zaplecza emituje hello powiadomień, przy użyciu hello **tag** i **szablonu** feautres usługi Azure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="e3121-112">hello back-end broadcasts hello notifications, using hello **tag** and **template** feautres of Azure Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e3121-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e3121-113">Prerequisites</span></span>
<span data-ttu-id="e3121-114">Należy zostały już wykonane hello [toosend użyciu usługi Notification Hubs fundamentalne wiadomości] samouczka i mieć kod hello jest dostępne, ponieważ w tym samouczku bezpośrednio oparta na kod.</span><span class="sxs-lookup"><span data-stu-id="e3121-114">You must have already completed hello [Use Notification Hubs toosend breaking news] tutorial and have hello code available, because this tutorial builds directly upon that code.</span></span>

<span data-ttu-id="e3121-115">Należy również Visual Studio 2012 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="e3121-115">You also need Visual Studio 2012 or later.</span></span>

## <a name="template-concepts"></a><span data-ttu-id="e3121-116">Pojęcia dotyczące szablonów</span><span class="sxs-lookup"><span data-stu-id="e3121-116">Template concepts</span></span>
<span data-ttu-id="e3121-117">W [toosend użyciu usługi Notification Hubs fundamentalne wiadomości] utworzono aplikację, która jest używana **tagi** toonotifications toosubscribe dla różnych grup dyskusyjnych kategorii.</span><span class="sxs-lookup"><span data-stu-id="e3121-117">In [Use Notification Hubs toosend breaking news] you built an app that used **tags** toosubscribe toonotifications for different news categories.</span></span>
<span data-ttu-id="e3121-118">Wiele aplikacji, jednak docelowy kilku rynkach i wymagają lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="e3121-118">Many apps, however, target multiple markets and require localization.</span></span> <span data-ttu-id="e3121-119">Oznacza to, czy zawartość hello hello powiadomień, się toobe zlokalizowane i dostarczonego toohello Popraw zbiór urządzeń.</span><span class="sxs-lookup"><span data-stu-id="e3121-119">This means that hello content of hello notifications themselves have toobe localized and delivered toohello correct set of devices.</span></span>
<span data-ttu-id="e3121-120">W tym temacie pokazano, jak toouse hello **szablonu** funkcji tooeasily świadczenia usługi Notification Hubs zlokalizowane powiadomienia o najważniejszych wiadomościach.</span><span class="sxs-lookup"><span data-stu-id="e3121-120">In this topic we will show how toouse hello **template** feature of Notification Hubs tooeasily deliver localized breaking news notifications.</span></span>

<span data-ttu-id="e3121-121">Uwaga: jednokierunkowej toosend zlokalizowane powiadomień jest toocreate wiele wersji każdego znacznika.</span><span class="sxs-lookup"><span data-stu-id="e3121-121">Note: one way toosend localized notifications is toocreate multiple versions of each tag.</span></span> <span data-ttu-id="e3121-122">Na przykład toosupport angielskim, francuskim i mandaryński, potrzebujemy czy trzy różne znaczniki dla wiadomości world: "world_en", "world_fr" i "world_ch".</span><span class="sxs-lookup"><span data-stu-id="e3121-122">For instance, toosupport English, French, and Mandarin, we would need three different tags for world news: "world_en", "world_fr", and "world_ch".</span></span> <span data-ttu-id="e3121-123">Firma Microsoft będzie zmuszony toosend zlokalizowanej wersji hello world wiadomości tooeach tych tagów.</span><span class="sxs-lookup"><span data-stu-id="e3121-123">We would then have toosend a localized version of hello world news tooeach of these tags.</span></span> <span data-ttu-id="e3121-124">W tym temacie używamy szablony tooavoid hello mnożenie tagów i wymagania hello wielu operacji wysyłania wiadomości.</span><span class="sxs-lookup"><span data-stu-id="e3121-124">In this topic we use templates tooavoid hello proliferation of tags and hello requirement of sending multiple messages.</span></span>

<span data-ttu-id="e3121-125">Na wysokim poziomie, szablony są toospecify sposób jak określonym urządzeniu powinno zostać odebrane powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="e3121-125">At a high level, templates are a way toospecify how a specific device should receive a notification.</span></span> <span data-ttu-id="e3121-126">Szablon Hello Określa format ładunku dokładne hello odwołując tooproperties, które są częścią hello wiadomość wysłana przez zaplecze Twojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e3121-126">hello template specifies hello exact payload format by referring tooproperties that are part of hello message sent by your app back-end.</span></span> <span data-ttu-id="e3121-127">W tym przypadku firma Microsoft wyśle komunikat niezależny od ustawień regionalnych zawierający wszystkie obsługiwane języki:</span><span class="sxs-lookup"><span data-stu-id="e3121-127">In our case, we will send a locale-agnostic message containing all supported languages:</span></span>

    {
        "News_English": "...",
        "News_French": "...",
        "News_Mandarin": "..."
    }

<span data-ttu-id="e3121-128">Następnie firma Microsoft zapewnia Zarejestruj szablon, który odwołuje się właściwość poprawne toohello przez urządzenia.</span><span class="sxs-lookup"><span data-stu-id="e3121-128">Then we will ensure that devices register with a template that refers toohello correct property.</span></span> <span data-ttu-id="e3121-129">Na przykład aplikacji Sklepu Windows, który chce tooreceive komunikat proste wyskakujące zarejestruje dla następującego szablonu z wszystkimi tagami odpowiedniego hello:</span><span class="sxs-lookup"><span data-stu-id="e3121-129">For instance, a Windows Store app that wants tooreceive a simple toast message will register for hello following template with any corresponding tags:</span></span>

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">$(News_English)</text>
        </binding>
      </visual>
    </toast>



<span data-ttu-id="e3121-130">Szablony są bardzo przydatna funkcja, możesz dowiedzieć się więcej w naszym [szablony](notification-hubs-templates-cross-platform-push-messages.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="e3121-130">Templates are a very powerful feature you can learn more about in our [Templates](notification-hubs-templates-cross-platform-push-messages.md) article.</span></span> 

## <a name="hello-app-user-interface"></a><span data-ttu-id="e3121-131">Interfejs użytkownika aplikacji Hello</span><span class="sxs-lookup"><span data-stu-id="e3121-131">hello app user interface</span></span>
<span data-ttu-id="e3121-132">Firma Microsoft będzie teraz zmodyfikować aplikacji fundamentalne wiadomości powitania, utworzonego w temacie hello [toosend użyciu usługi Notification Hubs fundamentalne wiadomości] toosend zlokalizowane najważniejszych wiadomości przy użyciu szablonów.</span><span class="sxs-lookup"><span data-stu-id="e3121-132">We will now modify hello Breaking News app that you created in hello topic [Use Notification Hubs toosend breaking news] toosend localized breaking news using templates.</span></span>

<span data-ttu-id="e3121-133">W aplikacji ze Sklepu Windows:</span><span class="sxs-lookup"><span data-stu-id="e3121-133">In your Windows Store app:</span></span>

<span data-ttu-id="e3121-134">Zmień tooinclude Twojego MainPage.xaml combobox ustawień regionalnych:</span><span class="sxs-lookup"><span data-stu-id="e3121-134">Change your MainPage.xaml tooinclude a locale combobox:</span></span>

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

## <a name="building-hello-windows-store-client-app"></a><span data-ttu-id="e3121-135">Tworzenie powitania klienta w Sklepie Windows</span><span class="sxs-lookup"><span data-stu-id="e3121-135">Building hello Windows Store client app</span></span>
1. <span data-ttu-id="e3121-136">W klasie powiadomień, dodać tooyour parametr ustawień regionalnych *StoreCategoriesAndSubscribe* i *SubscribeToCateories* metody.</span><span class="sxs-lookup"><span data-stu-id="e3121-136">In your Notifications class, add a locale parameter tooyour  *StoreCategoriesAndSubscribe* and *SubscribeToCateories* methods.</span></span>
   
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
            // Using hello localized tags based on locale selected.
            string templateBodyWNS = String.Format("<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(News_{0})</text></binding></visual></toast>", locale);
   
            return await hub.RegisterTemplateAsync(channel.Uri, templateBodyWNS, "localizedWNSTemplateExample", categories);
        }
   
    <span data-ttu-id="e3121-137">Należy pamiętać, że zamiast wywoływania hello *RegisterNativeAsync* metody nazywamy *RegisterTemplateAsync*: format określonych powiadomień, w którym hello szablonu zależy od ustawień regionalnych hello możemy rejestracji.</span><span class="sxs-lookup"><span data-stu-id="e3121-137">Note that instead of calling hello *RegisterNativeAsync* method we call *RegisterTemplateAsync*: we are registering a specific notification format in which hello template depends on hello locale.</span></span> <span data-ttu-id="e3121-138">Firma Microsoft udostępnia również nazwę dla szablonu hello ("localizedWNSTemplateExample"), ponieważ firma Microsoft może być tooregister więcej niż jednego szablonu (na przykład po jednej dla wyskakujące powiadomienia) i jeden dla kafelków i potrzebujemy tooname kolejność ich w stanie tooupdate toobe lub usuń je.</span><span class="sxs-lookup"><span data-stu-id="e3121-138">We also provide a name for hello template ("localizedWNSTemplateExample"), because we might want tooregister more than one template (for instance one for toast notifications and one for tiles) and we need tooname them in order toobe able tooupdate or delete them.</span></span>
   
    <span data-ttu-id="e3121-139">Należy pamiętać, że jeśli urządzenie rejestruje wiele szablonów z hello sam tagu wiadomości przychodzącej elementów docelowych, że tag spowoduje wielu dostarczyć powiadomień urządzenia toohello, (po jednej dla każdego szablonu).</span><span class="sxs-lookup"><span data-stu-id="e3121-139">Note that if a device registers multiple templates with hello same tag, an incoming message targeting that tag will result in multiple notifications delivered toohello device (one for each template).</span></span> <span data-ttu-id="e3121-140">To zachowanie jest przydatne, gdy hello tej samej logicznej wiadomość ma tooresult w wielu powiadomienia wizualne, na przykład zawierający wskaźnika i użyciu powiadomienia wyskakującego w aplikacji Sklepu Windows.</span><span class="sxs-lookup"><span data-stu-id="e3121-140">This behavior is useful when hello same logical message has tooresult in multiple visual notifications, for instance showing both a badge and a toast in a Windows Store application.</span></span>
2. <span data-ttu-id="e3121-141">Dodaj hello następujące metody tooretrieve hello przechowywane ustawienia regionalne:</span><span class="sxs-lookup"><span data-stu-id="e3121-141">Add hello following method tooretrieve hello stored locale:</span></span>
   
        public string RetrieveLocale()
        {
            var locale = (string) ApplicationData.Current.LocalSettings.Values["locale"];
            return locale != null ? locale : "English";
        }
3. <span data-ttu-id="e3121-142">W Twojej MainPage.xaml.cs aktualizacji przycisk kliknij programu obsługi pobierania hello bieżącą wartość pola kombi ustawień regionalnych hello i podając go klasy toohello wywołania toohello powiadomień, jak pokazano:</span><span class="sxs-lookup"><span data-stu-id="e3121-142">In your MainPage.xaml.cs, update your button click handler by retrieving hello current value of hello Locale combo box and providing it toohello call toohello Notifications class, as shown:</span></span>
   
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
4. <span data-ttu-id="e3121-143">Na koniec w pliku App.xaml.cs, upewnij się, że tooupdate Twojego `InitNotificationsAsync` tooretrieve — metoda hello ustawień regionalnych i użyć go subskrypcji:</span><span class="sxs-lookup"><span data-stu-id="e3121-143">Finally, in your App.xaml.cs file, make sure tooupdate your `InitNotificationsAsync` method tooretrieve hello locale and use it when subscribing:</span></span>
   
        private async void InitNotificationsAsync()
        {
            var result = await notifications.SubscribeToCategories(notifications.RetrieveLocale());
   
            // Displays hello registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
        }

## <a name="send-localized-notifications-from-your-back-end"></a><span data-ttu-id="e3121-144">Wysyłanie powiadomień zlokalizowanych z poziomu zaplecza</span><span class="sxs-lookup"><span data-stu-id="e3121-144">Send localized notifications from your back-end</span></span>
[!INCLUDE [notification-hubs-localized-back-end](../../includes/notification-hubs-localized-back-end.md)]

<!-- Anchors. -->
[Template concepts]: #concepts
[hello app user interface]: #ui
[Building hello Windows Store client app]: #building-client
[Send notifications from your back-end]: #send
[Next Steps]:#next-steps

<!-- Images. -->

<!-- URLs. -->
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notify users with Notification Hubs: ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Notify users with Notification Hubs: Mobile Services]: /manage/services/notification-hubs/notify-users
[toosend użyciu usługi Notification Hubs fundamentalne wiadomości]: /manage/services/notification-hubs/breaking-news-dotnet

[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started/#create-new-service
[Get started with data]: /develop/mobile/tutorials/get-started-with-data-dotnet
[Get started with authentication]: /develop/mobile/tutorials/get-started-with-users-dotnet
[Get started with push notifications]: /develop/mobile/tutorials/get-started-with-push-dotnet
[Push notifications tooapp users]: /develop/mobile/tutorials/push-notifications-to-app-users-dotnet
[Authorize users with scripts]: /develop/mobile/tutorials/authorize-users-in-scripts-dotnet
[JavaScript and HTML]: /develop/mobile/tutorials/get-started-with-push-js

[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor iOS]: http://msdn.microsoft.com/library/jj927168.aspx
[Notification Hubs How-toofor Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
