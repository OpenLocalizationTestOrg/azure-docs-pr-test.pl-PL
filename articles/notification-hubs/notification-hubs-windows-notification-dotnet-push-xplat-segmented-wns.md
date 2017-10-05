---
title: "Usługi Notification Hubs umożliwia wysyłanie najważniejszych wiadomości (uniwersalnych systemu Windows)"
description: "Za pomocą usługi Azure Notification Hubs tagów w rejestracji wysyłanie najważniejszych wiadomości do uniwersalnych aplikacji systemu Windows."
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: 
ms.assetid: 994d2eed-f62e-433c-bf65-4afebf1c0561
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 0e945b5626a08fcb428131f2abb465c2c141011a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="use-notification-hubs-to-send-breaking-news"></a><span data-ttu-id="5a375-103">Wysyłanie najważniejszych wiadomości przy użyciu usługi Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="5a375-103">Use Notification Hubs to send breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="5a375-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="5a375-104">Overview</span></span>
<span data-ttu-id="5a375-105">W tym temacie przedstawiono sposób użycia usługi Azure Notification Hubs wysyłać powiadomienia o najważniejszych wiadomościach do Sklepu Windows lub Windows Phone 8.1 (z systemem innym niż platformy Silverlight) aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5a375-105">This topic shows you how to use Azure Notification Hubs to broadcast breaking news notifications to a Windows Store or Windows Phone 8.1 (non-Silverlight) app.</span></span> <span data-ttu-id="5a375-106">Jeśli aplikacja ma być przeznaczona dla systemu Windows Phone 8.1 z platformą Silverlight, zapoznaj się z wersją dla systemu [Windows Phone](notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md).</span><span class="sxs-lookup"><span data-stu-id="5a375-106">If you are targeting Windows Phone 8.1 Silverlight, please refer to the [Windows Phone](notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md) version.</span></span> <span data-ttu-id="5a375-107">Po zakończeniu będzie można rejestrować zakłócenia w kategorii wiadomości i odbierać tylko powiadomienia wypychane dla tych kategorii.</span><span class="sxs-lookup"><span data-stu-id="5a375-107">When complete, you will be able to register for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="5a375-108">Ten scenariusz jest wspólnego wzorca dla wielu aplikacji, w której powiadomienia muszą być wysłane do grup użytkowników, którzy wcześniej zadeklarowany jako zainteresowanie je, np. czytnik danych RSS, aplikacje dla wentylatory muzyka i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="5a375-108">This scenario is a common pattern for many apps where notifications have to be sent to groups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, and so on.</span></span> 

<span data-ttu-id="5a375-109">Scenariusze emisji są włączone, umieszczając w niej co najmniej jeden *tagi* podczas tworzenia rejestracji w Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="5a375-109">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in the notification hub.</span></span> <span data-ttu-id="5a375-110">Gdy powiadomienia są wysyłane do tagu, wszystkie urządzenia, które zostały zarejestrowane dla tagu będą otrzymywać powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="5a375-110">When notifications are sent to a tag, all devices that have registered for the tag will receive the notification.</span></span> <span data-ttu-id="5a375-111">Ponieważ tagi są po prostu ciągów, nie mają być przygotowana z wyprzedzeniem.</span><span class="sxs-lookup"><span data-stu-id="5a375-111">Because tags are simply strings, they do not have to be provisioned in advance.</span></span> <span data-ttu-id="5a375-112">Aby uzyskać więcej informacji na temat tagów, zapoznaj się [routingu centra powiadomień i wyrażeń tagów](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="5a375-112">For more information about tags, refer to [Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

> [!NOTE]
> <span data-ttu-id="5a375-113">Sklep Windows i wersji projektów Windows Phone 8.1 i starsze nie są obsługiwane w programie Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="5a375-113">Windows Store and Windows Phone projects version 8.1 and earlier are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="5a375-114">Aby uzyskać więcej informacji, zobacz [Obsługiwane platformy i zgodność programu Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="5a375-114">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="5a375-115">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5a375-115">Prerequisites</span></span>
<span data-ttu-id="5a375-116">W tym temacie opiera się na aplikacji utworzony w [Rozpoczynanie pracy z usługą Notification Hubs][get-started].</span><span class="sxs-lookup"><span data-stu-id="5a375-116">This topic builds on the app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="5a375-117">Przed rozpoczęciem tego samouczka należy zostały już wykonane [Rozpoczynanie pracy z usługą Notification Hubs][get-started].</span><span class="sxs-lookup"><span data-stu-id="5a375-117">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-to-the-app"></a><span data-ttu-id="5a375-118">Dodaj wybrane kategorii do aplikacji</span><span class="sxs-lookup"><span data-stu-id="5a375-118">Add category selection to the app</span></span>
<span data-ttu-id="5a375-119">Pierwszym krokiem jest dodać elementy interfejsu użytkownika do strony głównej istniejących umożliwiają użytkownikowi wybierz kategorie, aby zarejestrować.</span><span class="sxs-lookup"><span data-stu-id="5a375-119">The first step is to add the UI elements to your existing main page that enable the user to select categories to register.</span></span> <span data-ttu-id="5a375-120">Kategorie wybrane przez użytkownika są przechowywane na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="5a375-120">The categories selected by a user are stored on the device.</span></span> <span data-ttu-id="5a375-121">Po uruchomieniu aplikacji, rejestracji urządzenia jest tworzony w Centrum powiadomień z wybranych kategorii jako znaczniki.</span><span class="sxs-lookup"><span data-stu-id="5a375-121">When the app starts, a device registration is created in your notification hub with the selected categories as tags.</span></span>

1. <span data-ttu-id="5a375-122">Otwórz plik projektu MainPage.xaml, a następnie skopiuj następujący kod w **siatki** elementu:</span><span class="sxs-lookup"><span data-stu-id="5a375-122">Open the MainPage.xaml project file, then copy the following code in the **Grid** element:</span></span>
   
        <Grid>
            <Grid.RowDefinitions>
                <RowDefinition/>
                <RowDefinition/>
                <RowDefinition/>
                <RowDefinition/>
                <RowDefinition/>
            </Grid.RowDefinitions>
            <Grid.ColumnDefinitions>
                <ColumnDefinition/>
                <ColumnDefinition/>
            </Grid.ColumnDefinitions>
            <TextBlock Grid.Row="0" Grid.Column="0" Grid.ColumnSpan="2"  TextWrapping="Wrap" Text="Breaking News" FontSize="42" VerticalAlignment="Top" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="World" Name="WorldToggle" Grid.Row="1" Grid.Column="0" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Politics" Name="PoliticsToggle" Grid.Row="2" Grid.Column="0" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Business" Name="BusinessToggle" Grid.Row="3" Grid.Column="0" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Technology" Name="TechnologyToggle" Grid.Row="1" Grid.Column="1" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Science" Name="ScienceToggle" Grid.Row="2" Grid.Column="1" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Sports" Name="SportsToggle" Grid.Row="3" Grid.Column="1" HorizontalAlignment="Center"/>
            <Button Name="SubscribeButton" Content="Subscribe" HorizontalAlignment="Center" Grid.Row="4" Grid.Column="0" Grid.ColumnSpan="2" Click="SubscribeButton_Click"/>
        </Grid>
2. <span data-ttu-id="5a375-123">Kliknij prawym przyciskiem myszy **Shared** projektu i dodać nową klasę o nazwie **powiadomienia**, Dodaj **publicznego** modyfikator do definicji klasy, a następnie dodaj następujące  **przy użyciu** instrukcje do nowego pliku kodu:</span><span class="sxs-lookup"><span data-stu-id="5a375-123">Right click the **Shared** project and add a new class named **Notifications**, add the **public** modifier to the class definition, then add the following **using** statements to the new code file:</span></span>
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.Storage;
        using System.Threading.Tasks;
3. <span data-ttu-id="5a375-124">Skopiuj następujący kod do nowej **powiadomienia** klasy:</span><span class="sxs-lookup"><span data-stu-id="5a375-124">Copy the following code into the new **Notifications** class:</span></span>
   
        private NotificationHub hub;
   
        public Notifications(string hubName, string listenConnectionString)
        {
            hub = new NotificationHub(hubName, listenConnectionString);
        }
   
        public async Task<Registration> StoreCategoriesAndSubscribe(IEnumerable<string> categories)
        {
            ApplicationData.Current.LocalSettings.Values["categories"] = string.Join(",", categories);
            return await SubscribeToCategories(categories);
        }
   
        public IEnumerable<string> RetrieveCategories()
        {
            var categories = (string) ApplicationData.Current.LocalSettings.Values["categories"];
            return categories != null ? categories.Split(','): new string[0];
        }
   
        public async Task<Registration> SubscribeToCategories(IEnumerable<string> categories = null)
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            if (categories == null)
            {
                categories = RetrieveCategories();
            }
   
            // Using a template registration to support notifications across platforms.
            // Any template notifications that contain messageParam and a corresponding tag expression
            // will be delivered for this registration.
   
            const string templateBodyWNS = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(messageParam)</text></binding></visual></toast>";
   
            return await hub.RegisterTemplateAsync(channel.Uri, templateBodyWNS, "simpleWNSTemplateExample",
                    categories);
        }
   
    <span data-ttu-id="5a375-125">Ta klasa używa lokalnego magazynu do przechowywania kategorii wiadomości, który to urządzenie musi odebrać.</span><span class="sxs-lookup"><span data-stu-id="5a375-125">This class uses the local storage to store the categories of news that this device has to receive.</span></span> <span data-ttu-id="5a375-126">Należy pamiętać, że zamiast wywoływać metodę *RegisterNativeAsync* metody nazywamy *RegisterTemplateAsync* do zarejestrowania dla kategorii przy użyciu rejestracji szablonu.</span><span class="sxs-lookup"><span data-stu-id="5a375-126">Note that instead of calling the *RegisterNativeAsync* method we call *RegisterTemplateAsync* to register for the categories using a template registration.</span></span> 
   
    <span data-ttu-id="5a375-127">Również udostępniamy nazwę dla szablonu ("simpleWNSTemplateExample"), ponieważ chcemy zarejestrować więcej niż jednego szablonu (na przykład jeden dla wyskakujące powiadomienia) i drugi dla kafelków i musimy ich nazw, aby można było zaktualizować lub usunąć je.</span><span class="sxs-lookup"><span data-stu-id="5a375-127">We also provide a name for the template ("simpleWNSTemplateExample"), because we might want to register more than one template (for instance one for toast notifications and one for tiles) and we need to name them in order to be able to update or delete them.</span></span>
   
    <span data-ttu-id="5a375-128">Należy pamiętać, że jeśli urządzenie rejestruje wiele szablonów z tym samym tagiem, przychodzących wiadomości przeznaczonych dla który tag spowoduje wiele powiadomień dostarczony do urządzenia, (po jednej dla każdego szablonu).</span><span class="sxs-lookup"><span data-stu-id="5a375-128">Note that if a device registers multiple templates with the same tag, an incoming message targeting that tag will result in multiple notifications delivered to the device (one for each template).</span></span> <span data-ttu-id="5a375-129">To zachowanie jest przydatne, gdy ten sam komunikat logiczne ma zastosowanie w wielu powiadomienia wizualne, na przykład zawierający wskaźnika i użyciu powiadomienia wyskakującego w aplikacji Sklepu Windows.</span><span class="sxs-lookup"><span data-stu-id="5a375-129">This behavior is useful when the same logical message has to result in multiple visual notifications, for instance showing both a badge and a toast in a Windows Store application.</span></span>
   
    <span data-ttu-id="5a375-130">Aby uzyskać więcej informacji dotyczących szablonów, zobacz [szablony](notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="5a375-130">For more information on templates, see [Templates](notification-hubs-templates-cross-platform-push-messages.md).</span></span>
4. <span data-ttu-id="5a375-131">W pliku projektu App.xaml.cs Dodaj następującą właściwość, aby **aplikacji** klasy:</span><span class="sxs-lookup"><span data-stu-id="5a375-131">In the App.xaml.cs project file, add the following property to the **App** class:</span></span>
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
    <span data-ttu-id="5a375-132">Ta właściwość jest używana do tworzenia i dostępu **powiadomienia** wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="5a375-132">This property is used to create and access a **Notifications** instance.</span></span>
   
    <span data-ttu-id="5a375-133">W powyższym kodzie Zamień `<hub name>` i `<connection string with listen access>` symbole zastępcze nazwą Centrum powiadomień i parametry połączenia dla *DefaultListenSharedAccessSignature* uzyskany wcześniej.</span><span class="sxs-lookup"><span data-stu-id="5a375-133">In the above code, replace the `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and the connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5a375-134">Ponieważ poświadczenia, które są dystrybuowane wraz z aplikacji przez klienta nie są zazwyczaj bezpieczna, klucz dostępu do nasłuchiwania należy dystrybuować tylko z aplikacji klienta.</span><span class="sxs-lookup"><span data-stu-id="5a375-134">Because credentials that are distributed with a client app are not generally secure, you should only distribute the key for listen access with your client app.</span></span> <span data-ttu-id="5a375-135">Nasłuchiwanie umożliwia dostęp, nie można zmodyfikować aplikację, aby zarejestrować dla powiadomień, ale istniejące rejestracje i nie mogą być wysyłane powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="5a375-135">Listen access enables your app to register for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="5a375-136">Klucz pełny dostęp jest używany w usłudze zabezpieczonych wewnętrznej bazy danych do wysyłania powiadomień i zmianę istniejącego rejestracji.</span><span class="sxs-lookup"><span data-stu-id="5a375-136">The full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
5. <span data-ttu-id="5a375-137">W Twojej MainPage.xaml.cs Dodaj następujący wiersz:</span><span class="sxs-lookup"><span data-stu-id="5a375-137">In your MainPage.xaml.cs, add the following line:</span></span>
   
        using Windows.UI.Popups;
6. <span data-ttu-id="5a375-138">W pliku MainPage.xaml.cs projekt Dodaj następującą metodę:</span><span class="sxs-lookup"><span data-stu-id="5a375-138">In the MainPage.xaml.cs project file, add the following method:</span></span>
   
        private async void SubscribeButton_Click(object sender, RoutedEventArgs e)
        {
            var categories = new HashSet<string>();
            if (WorldToggle.IsOn) categories.Add("World");
            if (PoliticsToggle.IsOn) categories.Add("Politics");
            if (BusinessToggle.IsOn) categories.Add("Business");
            if (TechnologyToggle.IsOn) categories.Add("Technology");
            if (ScienceToggle.IsOn) categories.Add("Science");
            if (SportsToggle.IsOn) categories.Add("Sports");
   
            var result = await ((App)Application.Current).notifications.StoreCategoriesAndSubscribe(categories);
   
            var dialog = new MessageDialog("Subscribed to: " + string.Join(",", categories) + " on registration Id: " + result.RegistrationId);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
   
    <span data-ttu-id="5a375-139">Ta metoda tworzy listę kategorii i używa **powiadomienia** klasy przechowywania listy w magazynie lokalnym i rejestracji, odpowiednie znaczniki w Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="5a375-139">This method creates a list of categories and uses the **Notifications** class to store the list in the local storage and register the corresponding tags with your notification hub.</span></span> <span data-ttu-id="5a375-140">Zmiana kategorii rejestracji zostaje odtworzone w nowej kategorii.</span><span class="sxs-lookup"><span data-stu-id="5a375-140">When categories are changed, the registration is recreated with the new categories.</span></span>

<span data-ttu-id="5a375-141">Aplikacja jest teraz możliwość przechowywania zestawu kategorii w lokalnej pamięci masowej na urządzeniu i Zarejestruj w Centrum powiadomień, zawsze, gdy użytkownik zmieni się zaznaczenie kategorii.</span><span class="sxs-lookup"><span data-stu-id="5a375-141">Your app is now able to store a set of categories in local storage on the device and register with the notification hub whenever the user changes the selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="5a375-142">Rejestrowanie się w celu powiadomienia</span><span class="sxs-lookup"><span data-stu-id="5a375-142">Register for notifications</span></span>
<span data-ttu-id="5a375-143">Następujące kroki, zarejestruj się w Centrum powiadomień przy uruchamianiu przy użyciu kategorii, które były przechowywane w magazynie lokalnym.</span><span class="sxs-lookup"><span data-stu-id="5a375-143">These steps register with the notification hub on startup using the categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="5a375-144">Ponieważ identyfikator URI przypisany przez usługę powiadomień systemu Windows (WNS) kanału można zmienić w dowolnym momencie, należy zarejestrować powiadomień często uniknąć niepowodzeń powiadomień.</span><span class="sxs-lookup"><span data-stu-id="5a375-144">Because the channel URI assigned by the Windows Notification Service (WNS) can change at any time, you should register for notifications frequently to avoid notification failures.</span></span> <span data-ttu-id="5a375-145">W tym przykładzie rejestruje powiadomienia każdym uruchomieniu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5a375-145">This example registers for notification every time that the app starts.</span></span> <span data-ttu-id="5a375-146">Dla aplikacji, które są uruchamiane często więcej niż raz dziennie, można prawdopodobnie pominąć rejestrację, aby zachować przepustowość, jeśli krótszy niż doba upłynął od czasu poprzedniej rejestracji.</span><span class="sxs-lookup"><span data-stu-id="5a375-146">For apps that are run frequently, more than once a day, you can probably skip registration to preserve bandwidth if less than a day has passed since the previous registration.</span></span>
> 
> 

1. <span data-ttu-id="5a375-147">Otwórz plik App.xaml.cs i aktualizacji **InitNotificationsAsync** metodę `notifications` klasy do subskrybowania na podstawie kategorii.</span><span class="sxs-lookup"><span data-stu-id="5a375-147">Open the App.xaml.cs file and update the **InitNotificationsAsync** method to use the `notifications` class to subscribe based on categories.</span></span>
   
        // *** Remove or comment out these lines *** 
        //var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
        //var hub = new NotificationHub("your hub name", "your listen connection string");
        //var result = await hub.RegisterNativeAsync(channel.Uri);
   
        var result = await notifications.SubscribeToCategories();
   
    <span data-ttu-id="5a375-148">Dzięki temu przy każdym uruchomieniu aplikacji it pobiera kategorie z magazynu lokalnego i żąda rejestracja dla tych kategorii.</span><span class="sxs-lookup"><span data-stu-id="5a375-148">This makes sure that every time the app starts it retrieves the categories from local storage and requests a registeration for these categories.</span></span> <span data-ttu-id="5a375-149">**InitNotificationsAsync** metody został utworzony jako część [Rozpoczynanie pracy z usługą Notification Hubs] [ get-started] samouczka.</span><span class="sxs-lookup"><span data-stu-id="5a375-149">The **InitNotificationsAsync** method was created as part of the [Get started with Notification Hubs][get-started] tutorial.</span></span>
2. <span data-ttu-id="5a375-150">W pliku MainPage.xaml.cs projekt, Dodaj następujący kod do *OnNavigatedTo* metody:</span><span class="sxs-lookup"><span data-stu-id="5a375-150">In the MainPage.xaml.cs project file, add the following code to the *OnNavigatedTo* method:</span></span>
   
        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
            var categories = ((App)Application.Current).notifications.RetrieveCategories();
   
            if (categories.Contains("World")) WorldToggle.IsOn = true;
            if (categories.Contains("Politics")) PoliticsToggle.IsOn = true;
            if (categories.Contains("Business")) BusinessToggle.IsOn = true;
            if (categories.Contains("Technology")) TechnologyToggle.IsOn = true;
            if (categories.Contains("Science")) ScienceToggle.IsOn = true;
            if (categories.Contains("Sports")) SportsToggle.IsOn = true;
        }
   
    <span data-ttu-id="5a375-151">Spowoduje to zaktualizowanie strony głównej na podstawie kategorii uprzednio zapisanego stanu.</span><span class="sxs-lookup"><span data-stu-id="5a375-151">This updates the main page based on the status of previously saved categories.</span></span>

<span data-ttu-id="5a375-152">Aplikacja jest teraz ukończona i może przechowywać zestawu kategorii w magazynie lokalnym urządzenia używane do rejestrowania w Centrum powiadomień, zawsze, gdy użytkownik zmieni się zaznaczenie kategorii.</span><span class="sxs-lookup"><span data-stu-id="5a375-152">The app is now complete and can store a set of categories in the device local storage used to register with the notification hub whenever the user changes the selection of categories.</span></span> <span data-ttu-id="5a375-153">Następnie zdefiniujemy wewnętrznej bazy danych, który może wysyłać powiadomienia kategorii do tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5a375-153">Next, we will define a backend that can send category notifications to this app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="5a375-154">Wysyłanie powiadomień oznakowany</span><span class="sxs-lookup"><span data-stu-id="5a375-154">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-the-app-and-generate-notifications"></a><span data-ttu-id="5a375-155">Uruchom aplikację i generować powiadomienia</span><span class="sxs-lookup"><span data-stu-id="5a375-155">Run the app and generate notifications</span></span>
1. <span data-ttu-id="5a375-156">W programie Visual Studio naciśnij klawisz F5, aby skompilować i uruchomić aplikację.</span><span class="sxs-lookup"><span data-stu-id="5a375-156">In Visual Studio, press F5 to compile and start the app.</span></span>
   
    ![][1]
   
    <span data-ttu-id="5a375-157">Należy pamiętać, że aplikacja interfejsu użytkownika zawiera zestaw przełącza umożliwiające wybierz kategorie, aby subskrybować.</span><span class="sxs-lookup"><span data-stu-id="5a375-157">Note that the app UI provides a set of toggles that lets you choose the categories to subscribe to.</span></span>
2. <span data-ttu-id="5a375-158">Włącz co najmniej jeden przełącza kategorie, a następnie kliknij przycisk **Subskrybuj**.</span><span class="sxs-lookup"><span data-stu-id="5a375-158">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="5a375-159">Konwertuje wybranych kategorii do tagów i żąda nowej rejestracji urządzeń dla wybranych tagów z Centrum powiadomień aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5a375-159">The app converts the selected categories into tags and requests a new device registration for the selected tags from the notification hub.</span></span> <span data-ttu-id="5a375-160">Zarejestrowany kategorie są zwracane i wyświetlane w oknie dialogowym.</span><span class="sxs-lookup"><span data-stu-id="5a375-160">The registered categories are returned and displayed in a dialog.</span></span>
   
    ![][19]
3. <span data-ttu-id="5a375-161">Wyślij nowe powiadomienie z wewnętrznej bazy danych w jednym z następujących sposobów:</span><span class="sxs-lookup"><span data-stu-id="5a375-161">Send a new notification from the backend in one of the following ways:</span></span>
   
   * <span data-ttu-id="5a375-162">**Aplikacja konsoli:** uruchomić aplikację konsoli.</span><span class="sxs-lookup"><span data-stu-id="5a375-162">**Console app:** start the console app.</span></span>
   * <span data-ttu-id="5a375-163">**Java/PHP:** uruchamiania aplikacji lub skryptu.</span><span class="sxs-lookup"><span data-stu-id="5a375-163">**Java/PHP:** run your app/script.</span></span>
     
     <span data-ttu-id="5a375-164">Powiadomienia dotyczące wybranych kategorii są wyświetlane jako wyskakujące powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="5a375-164">Notifications for the selected categories appear as toast notifications.</span></span>
     
     ![][14]

## <a name="next-steps"></a><span data-ttu-id="5a375-165">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5a375-165">Next steps</span></span>
<span data-ttu-id="5a375-166">W tym samouczku opisano sposób emisji najważniejszych wiadomości według kategorii.</span><span class="sxs-lookup"><span data-stu-id="5a375-166">In this tutorial we learned how to broadcast breaking news by category.</span></span> <span data-ttu-id="5a375-167">Należy rozważyć wykonanie jednej z następujących samouczków, w których są wyróżniane innych zaawansowanych scenariuszy centra powiadomień:</span><span class="sxs-lookup"><span data-stu-id="5a375-167">Consider completing one of the following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="5a375-168">[Emisji zlokalizowanych najważniejszych wiadomości przy użyciu usługi Notification Hubs]</span><span class="sxs-lookup"><span data-stu-id="5a375-168">[Use Notification Hubs to broadcast localized breaking news]</span></span>
  
    <span data-ttu-id="5a375-169">Dowiedz się, jak rozszerzyć aplikację wiadomości podziału, aby umożliwić wysyłanie powiadomień zlokalizowane.</span><span class="sxs-lookup"><span data-stu-id="5a375-169">Learn how to expand the breaking news app to enable sending localized notifications.</span></span>

<!-- Anchors. -->
[Add category selection to the app]: #adding-categories
[Register for notifications]: #register
[Send notifications from your back-end]: #send
[Run the app and generate notifications]: #test-app
[Next Steps]: #next-steps

<!-- Images. -->
[1]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-breakingnews-win1.png

[14]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-windows-toast-2.png


[19]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-windows-reg-2.png

<!-- URLs.-->
[get-started]: /manage/services/notification-hubs/getting-started-windows-dotnet/
<span data-ttu-id="5a375-170">[Emisji zlokalizowanych najważniejszych wiadomości przy użyciu usługi Notification Hubs]: /manage/services/notification-hubs/breaking-news-localized-dotnet/</span><span class="sxs-lookup"><span data-stu-id="5a375-170">[Use Notification Hubs to broadcast localized breaking news]: /manage/services/notification-hubs/breaking-news-localized-dotnet/</span></span>
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users
[Mobile Service]: /develop/mobile/tutorials/get-started/
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-To for Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
