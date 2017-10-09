---
title: "toosend usługi Notification Hubs aaaUse fundamentalne wiadomości (uniwersalnych systemu Windows)"
description: "Azure Notification Hubs za pomocą tagów w toosend rejestracji hello fundamentalne wiadomości tooa uniwersalnej aplikacji systemu Windows."
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
ms.openlocfilehash: f102d286d2c7bd387fcfa2c7eab2ba31a0298517
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-breaking-news"></a><span data-ttu-id="109e0-103">Użyj usługi Notification Hubs toosend fundamentalne wiadomości</span><span class="sxs-lookup"><span data-stu-id="109e0-103">Use Notification Hubs toosend breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="109e0-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="109e0-104">Overview</span></span>
<span data-ttu-id="109e0-105">W tym temacie opisano sposób toobroadcast usługi Azure Notification Hubs toouse fundamentalne aplikacji Windows Phone 8.1 (z systemem innym niż platformy Silverlight) lub Sklepu Windows tooa powiadomień dla wiadomości.</span><span class="sxs-lookup"><span data-stu-id="109e0-105">This topic shows you how toouse Azure Notification Hubs toobroadcast breaking news notifications tooa Windows Store or Windows Phone 8.1 (non-Silverlight) app.</span></span> <span data-ttu-id="109e0-106">Jeśli ma być przeznaczona dla systemu Windows Phone 8.1 Silverlight, zobacz toohello [Windows Phone](notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md) wersji.</span><span class="sxs-lookup"><span data-stu-id="109e0-106">If you are targeting Windows Phone 8.1 Silverlight, please refer toohello [Windows Phone](notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md) version.</span></span> <span data-ttu-id="109e0-107">Po zakończeniu będzie być może tooregister zakłócenia w kategorii wiadomości i odbierać tylko powiadomienia wypychane dla tych kategorii.</span><span class="sxs-lookup"><span data-stu-id="109e0-107">When complete, you will be able tooregister for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="109e0-108">Ten scenariusz jest wspólnego wzorca dla wielu aplikacji, w której powiadomienia mają toogroups toobe wysyłane użytkowników, którzy wcześniej zadeklarowany jako zainteresowanie je, np. czytnik danych RSS, aplikacje dla wentylatory muzyka i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="109e0-108">This scenario is a common pattern for many apps where notifications have toobe sent toogroups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, and so on.</span></span> 

<span data-ttu-id="109e0-109">Scenariusze emisji są włączone, umieszczając w niej co najmniej jeden *tagi* podczas tworzenia rejestracji w Centrum powiadomień hello.</span><span class="sxs-lookup"><span data-stu-id="109e0-109">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in hello notification hub.</span></span> <span data-ttu-id="109e0-110">Gdy tooa tag wysyłane są powiadomienia, wszystkie urządzenia, które zostały zarejestrowane dla tagu hello będzie wysyłane powiadomienie hello.</span><span class="sxs-lookup"><span data-stu-id="109e0-110">When notifications are sent tooa tag, all devices that have registered for hello tag will receive hello notification.</span></span> <span data-ttu-id="109e0-111">Ponieważ tagi są po prostu ciągów, nie mają toobe udostępnione wcześniej.</span><span class="sxs-lookup"><span data-stu-id="109e0-111">Because tags are simply strings, they do not have toobe provisioned in advance.</span></span> <span data-ttu-id="109e0-112">Aby uzyskać więcej informacji na temat tagów, zobacz zbyt[routingu centra powiadomień i wyrażeń tagów](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="109e0-112">For more information about tags, refer too[Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

> [!NOTE]
> <span data-ttu-id="109e0-113">Sklep Windows i wersji projektów Windows Phone 8.1 i starsze nie są obsługiwane w programie Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="109e0-113">Windows Store and Windows Phone projects version 8.1 and earlier are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="109e0-114">Aby uzyskać więcej informacji, zobacz [Obsługiwane platformy i zgodność programu Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="109e0-114">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="109e0-115">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="109e0-115">Prerequisites</span></span>
<span data-ttu-id="109e0-116">W tym temacie opiera się na aplikacji hello utworzony w [Rozpoczynanie pracy z usługą Notification Hubs][get-started].</span><span class="sxs-lookup"><span data-stu-id="109e0-116">This topic builds on hello app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="109e0-117">Przed rozpoczęciem tego samouczka należy zostały już wykonane [Rozpoczynanie pracy z usługą Notification Hubs][get-started].</span><span class="sxs-lookup"><span data-stu-id="109e0-117">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-toohello-app"></a><span data-ttu-id="109e0-118">Dodaj aplikację toohello wybór kategorii</span><span class="sxs-lookup"><span data-stu-id="109e0-118">Add category selection toohello app</span></span>
<span data-ttu-id="109e0-119">Witaj pierwszym krokiem jest tooadd hello interfejsu użytkownika elementy tooyour istniejącej strony głównej umożliwiające hello użytkownika tooselect kategorii tooregister.</span><span class="sxs-lookup"><span data-stu-id="109e0-119">hello first step is tooadd hello UI elements tooyour existing main page that enable hello user tooselect categories tooregister.</span></span> <span data-ttu-id="109e0-120">Witaj kategorie wybrane przez użytkownika są przechowywane na urządzeniu hello.</span><span class="sxs-lookup"><span data-stu-id="109e0-120">hello categories selected by a user are stored on hello device.</span></span> <span data-ttu-id="109e0-121">Po uruchomieniu aplikacji hello rejestracji urządzenia jest tworzony w Centrum powiadomień z kategorii hello wybrany jako znaczniki.</span><span class="sxs-lookup"><span data-stu-id="109e0-121">When hello app starts, a device registration is created in your notification hub with hello selected categories as tags.</span></span>

1. <span data-ttu-id="109e0-122">Otwórz plik projektu MainPage.xaml hello, a następnie hello kopiowania następującego kodu w hello **siatki** elementu:</span><span class="sxs-lookup"><span data-stu-id="109e0-122">Open hello MainPage.xaml project file, then copy hello following code in hello **Grid** element:</span></span>
   
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
2. <span data-ttu-id="109e0-123">Powitania kliknij prawym przyciskiem myszy **Shared** projektu i dodać nową klasę o nazwie **powiadomienia**, Dodaj hello **publicznego** toohello modyfikator klasy definicji, a następnie dodaj następujące hello **przy użyciu** instrukcje toohello nowy plik kodu:</span><span class="sxs-lookup"><span data-stu-id="109e0-123">Right click hello **Shared** project and add a new class named **Notifications**, add hello **public** modifier toohello class definition, then add hello following **using** statements toohello new code file:</span></span>
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.Storage;
        using System.Threading.Tasks;
3. <span data-ttu-id="109e0-124">Kopiuj hello poniższy kod do nowego hello **powiadomienia** klasy:</span><span class="sxs-lookup"><span data-stu-id="109e0-124">Copy hello following code into hello new **Notifications** class:</span></span>
   
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
   
            // Using a template registration toosupport notifications across platforms.
            // Any template notifications that contain messageParam and a corresponding tag expression
            // will be delivered for this registration.
   
            const string templateBodyWNS = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(messageParam)</text></binding></visual></toast>";
   
            return await hub.RegisterTemplateAsync(channel.Uri, templateBodyWNS, "simpleWNSTemplateExample",
                    categories);
        }
   
    <span data-ttu-id="109e0-125">Ta klasa korzysta z hello Magazyn lokalny toostore hello kategorii wiadomości, czy to urządzenie ma tooreceive.</span><span class="sxs-lookup"><span data-stu-id="109e0-125">This class uses hello local storage toostore hello categories of news that this device has tooreceive.</span></span> <span data-ttu-id="109e0-126">Należy pamiętać, że zamiast wywoływania hello *RegisterNativeAsync* metody nazywamy *RegisterTemplateAsync* tooregister dla kategorii hello przy użyciu rejestracji szablonu.</span><span class="sxs-lookup"><span data-stu-id="109e0-126">Note that instead of calling hello *RegisterNativeAsync* method we call *RegisterTemplateAsync* tooregister for hello categories using a template registration.</span></span> 
   
    <span data-ttu-id="109e0-127">Firma Microsoft udostępnia również nazwę dla szablonu hello ("simpleWNSTemplateExample"), ponieważ firma Microsoft może być tooregister więcej niż jednego szablonu (na przykład po jednej dla wyskakujące powiadomienia) i jeden dla kafelków i potrzebujemy tooname kolejność ich w stanie tooupdate toobe lub usuń je.</span><span class="sxs-lookup"><span data-stu-id="109e0-127">We also provide a name for hello template ("simpleWNSTemplateExample"), because we might want tooregister more than one template (for instance one for toast notifications and one for tiles) and we need tooname them in order toobe able tooupdate or delete them.</span></span>
   
    <span data-ttu-id="109e0-128">Należy pamiętać, że jeśli urządzenie rejestruje wiele szablonów z hello sam tagu wiadomości przychodzącej elementów docelowych, że tag spowoduje wielu dostarczyć powiadomień urządzenia toohello, (po jednej dla każdego szablonu).</span><span class="sxs-lookup"><span data-stu-id="109e0-128">Note that if a device registers multiple templates with hello same tag, an incoming message targeting that tag will result in multiple notifications delivered toohello device (one for each template).</span></span> <span data-ttu-id="109e0-129">To zachowanie jest przydatne, gdy hello tej samej logicznej wiadomość ma tooresult w wielu powiadomienia wizualne, na przykład zawierający wskaźnika i użyciu powiadomienia wyskakującego w aplikacji Sklepu Windows.</span><span class="sxs-lookup"><span data-stu-id="109e0-129">This behavior is useful when hello same logical message has tooresult in multiple visual notifications, for instance showing both a badge and a toast in a Windows Store application.</span></span>
   
    <span data-ttu-id="109e0-130">Aby uzyskać więcej informacji dotyczących szablonów, zobacz [szablony](notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="109e0-130">For more information on templates, see [Templates](notification-hubs-templates-cross-platform-push-messages.md).</span></span>
4. <span data-ttu-id="109e0-131">W pliku projektu App.xaml.cs hello, Dodaj następujące właściwości toohello hello **aplikacji** klasy:</span><span class="sxs-lookup"><span data-stu-id="109e0-131">In hello App.xaml.cs project file, add hello following property toohello **App** class:</span></span>
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
    <span data-ttu-id="109e0-132">Ta właściwość jest używana toocreate i dostęp **powiadomienia** wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="109e0-132">This property is used toocreate and access a **Notifications** instance.</span></span>
   
    <span data-ttu-id="109e0-133">W hello powyżej kodu, Zastąp hello `<hub name>` i `<connection string with listen access>` symbole zastępcze z powiadomienia Centrum nazwy i hello parametrów połączenia dla *DefaultListenSharedAccessSignature* uzyskany wcześniej.</span><span class="sxs-lookup"><span data-stu-id="109e0-133">In hello above code, replace hello `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and hello connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="109e0-134">Ponieważ poświadczenia, które są dystrybuowane wraz z aplikacji przez klienta nie są zazwyczaj bezpieczna, hello klucz dostępu do nasłuchiwania należy dystrybuować tylko z aplikacji klienta.</span><span class="sxs-lookup"><span data-stu-id="109e0-134">Because credentials that are distributed with a client app are not generally secure, you should only distribute hello key for listen access with your client app.</span></span> <span data-ttu-id="109e0-135">Nasłuchiwanie umożliwia dostęp, nie można zmodyfikować tooregister Twojej aplikacji dla powiadomień, ale istniejące rejestracje i nie mogą być wysyłane powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="109e0-135">Listen access enables your app tooregister for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="109e0-136">klucz pełny dostęp Hello jest używany w usłudze zabezpieczonych wewnętrznej bazy danych do wysyłania powiadomień i zmianę istniejącego rejestracji.</span><span class="sxs-lookup"><span data-stu-id="109e0-136">hello full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
5. <span data-ttu-id="109e0-137">W Twojej MainPage.xaml.cs Dodaj powitania po wierszu:</span><span class="sxs-lookup"><span data-stu-id="109e0-137">In your MainPage.xaml.cs, add hello following line:</span></span>
   
        using Windows.UI.Popups;
6. <span data-ttu-id="109e0-138">W pliku projektu hello MainPage.xaml.cs Dodaj hello następujące metody:</span><span class="sxs-lookup"><span data-stu-id="109e0-138">In hello MainPage.xaml.cs project file, add hello following method:</span></span>
   
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
   
    <span data-ttu-id="109e0-139">Ta metoda tworzy listę kategorii i używa hello **powiadomienia** klasy toostore hello listy w magazynie lokalnym hello i zarejestruj hello odpowiednie tagi w Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="109e0-139">This method creates a list of categories and uses hello **Notifications** class toostore hello list in hello local storage and register hello corresponding tags with your notification hub.</span></span> <span data-ttu-id="109e0-140">Zmiana kategorii rejestracji hello zostaje odtworzone w hello nowych kategorii.</span><span class="sxs-lookup"><span data-stu-id="109e0-140">When categories are changed, hello registration is recreated with hello new categories.</span></span>

<span data-ttu-id="109e0-141">Aplikacji jest teraz możliwe toostore zestaw kategorii w lokalnej pamięci masowej na powitania urządzenia i rejestruje hello Centrum powiadomień, gdy wybór kategorii hello hello zmiany wprowadzane przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="109e0-141">Your app is now able toostore a set of categories in local storage on hello device and register with hello notification hub whenever hello user changes hello selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="109e0-142">Rejestrowanie się w celu powiadomienia</span><span class="sxs-lookup"><span data-stu-id="109e0-142">Register for notifications</span></span>
<span data-ttu-id="109e0-143">Następujące kroki, zarejestruj się w Centrum powiadomień hello podczas uruchamiania przy użyciu hello kategorie, które były przechowywane w magazynie lokalnym.</span><span class="sxs-lookup"><span data-stu-id="109e0-143">These steps register with hello notification hub on startup using hello categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="109e0-144">Ponieważ kanał hello URI przypisał hello powiadomienia usługi WNS (Windows), można zmienić w dowolnym momencie, należy zarejestrować powiadomienia o często tooavoid powiadomień błędów.</span><span class="sxs-lookup"><span data-stu-id="109e0-144">Because hello channel URI assigned by hello Windows Notification Service (WNS) can change at any time, you should register for notifications frequently tooavoid notification failures.</span></span> <span data-ttu-id="109e0-145">W tym przykładzie rejestruje powiadomienia o każdym uruchomieniu danej aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="109e0-145">This example registers for notification every time that hello app starts.</span></span> <span data-ttu-id="109e0-146">Dla aplikacji, które są uruchamiane często więcej niż raz dziennie, prawdopodobnie Jeśli możesz pominąć rejestrację toopreserve przepustowości od poprzedniej rejestracji hello upłynął krótszy niż doba.</span><span class="sxs-lookup"><span data-stu-id="109e0-146">For apps that are run frequently, more than once a day, you can probably skip registration toopreserve bandwidth if less than a day has passed since hello previous registration.</span></span>
> 
> 

1. <span data-ttu-id="109e0-147">Otwórz hello App.xaml.cs plików i aktualizacji hello **InitNotificationsAsync** hello toouse — metoda `notifications` klasy toosubscribe na podstawie kategorii.</span><span class="sxs-lookup"><span data-stu-id="109e0-147">Open hello App.xaml.cs file and update hello **InitNotificationsAsync** method toouse hello `notifications` class toosubscribe based on categories.</span></span>
   
        // *** Remove or comment out these lines *** 
        //var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
        //var hub = new NotificationHub("your hub name", "your listen connection string");
        //var result = await hub.RegisterNativeAsync(channel.Uri);
   
        var result = await notifications.SubscribeToCategories();
   
    <span data-ttu-id="109e0-148">Dzięki temu że każdym uruchomieniu aplikacji hello pobiera kategorie hello z magazynu lokalnego i żąda rejestracja dla tych kategorii.</span><span class="sxs-lookup"><span data-stu-id="109e0-148">This makes sure that every time hello app starts it retrieves hello categories from local storage and requests a registeration for these categories.</span></span> <span data-ttu-id="109e0-149">Witaj **InitNotificationsAsync** metody został utworzony jako część hello [Rozpoczynanie pracy z usługą Notification Hubs] [ get-started] samouczka.</span><span class="sxs-lookup"><span data-stu-id="109e0-149">hello **InitNotificationsAsync** method was created as part of hello [Get started with Notification Hubs][get-started] tutorial.</span></span>
2. <span data-ttu-id="109e0-150">W pliku projektu hello MainPage.xaml.cs Dodaj hello następującego kodu toohello *OnNavigatedTo* metody:</span><span class="sxs-lookup"><span data-stu-id="109e0-150">In hello MainPage.xaml.cs project file, add hello following code toohello *OnNavigatedTo* method:</span></span>
   
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
   
    <span data-ttu-id="109e0-151">Tej aktualizacji hello głównej strony na podstawie stanu hello wcześniej zapisane kategorii.</span><span class="sxs-lookup"><span data-stu-id="109e0-151">This updates hello main page based on hello status of previously saved categories.</span></span>

<span data-ttu-id="109e0-152">Aplikacja Hello jest teraz ukończona i może przechowywać zestawu kategorii hello urządzenia magazynu lokalnego używane tooregister hello Centrum powiadomień przy każdym zmiany użytkowników hello hello wybór kategorii.</span><span class="sxs-lookup"><span data-stu-id="109e0-152">hello app is now complete and can store a set of categories in hello device local storage used tooregister with hello notification hub whenever hello user changes hello selection of categories.</span></span> <span data-ttu-id="109e0-153">Następnie zdefiniujemy wewnętrznej bazy danych, który może wysyłać kategorii powiadomienia toothis aplikacji.</span><span class="sxs-lookup"><span data-stu-id="109e0-153">Next, we will define a backend that can send category notifications toothis app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="109e0-154">Wysyłanie powiadomień oznakowany</span><span class="sxs-lookup"><span data-stu-id="109e0-154">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-hello-app-and-generate-notifications"></a><span data-ttu-id="109e0-155">Uruchamianie aplikacji hello i generować powiadomienia</span><span class="sxs-lookup"><span data-stu-id="109e0-155">Run hello app and generate notifications</span></span>
1. <span data-ttu-id="109e0-156">W programie Visual Studio naciśnij klawisz F5 toocompile i uruchomić aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="109e0-156">In Visual Studio, press F5 toocompile and start hello app.</span></span>
   
    ![][1]
   
    <span data-ttu-id="109e0-157">Należy pamiętać, że przełącza, aplikacja hello, które interfejs użytkownika zawiera zestaw, który umożliwia wybranie hello toosubscribe kategorii do.</span><span class="sxs-lookup"><span data-stu-id="109e0-157">Note that hello app UI provides a set of toggles that lets you choose hello categories toosubscribe to.</span></span>
2. <span data-ttu-id="109e0-158">Włącz co najmniej jeden przełącza kategorie, a następnie kliknij przycisk **Subskrybuj**.</span><span class="sxs-lookup"><span data-stu-id="109e0-158">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="109e0-159">Aplikacja Hello konwertuje kategorii hello wybrane tagi i żąda nowej rejestracji urządzenia hello wybrane tagów z Centrum powiadomień hello.</span><span class="sxs-lookup"><span data-stu-id="109e0-159">hello app converts hello selected categories into tags and requests a new device registration for hello selected tags from hello notification hub.</span></span> <span data-ttu-id="109e0-160">Witaj zarejestrowanych kategorie są zwracane i wyświetlane w oknie dialogowym.</span><span class="sxs-lookup"><span data-stu-id="109e0-160">hello registered categories are returned and displayed in a dialog.</span></span>
   
    ![][19]
3. <span data-ttu-id="109e0-161">Wysyłanie nowych powiadomień z zaplecza hello w jednym z hello następujące sposoby:</span><span class="sxs-lookup"><span data-stu-id="109e0-161">Send a new notification from hello backend in one of hello following ways:</span></span>
   
   * <span data-ttu-id="109e0-162">**Aplikacja konsoli:** start hello aplikacji konsoli.</span><span class="sxs-lookup"><span data-stu-id="109e0-162">**Console app:** start hello console app.</span></span>
   * <span data-ttu-id="109e0-163">**Java/PHP:** uruchamiania aplikacji lub skryptu.</span><span class="sxs-lookup"><span data-stu-id="109e0-163">**Java/PHP:** run your app/script.</span></span>
     
     <span data-ttu-id="109e0-164">Powiadomienia o kategoriach hello wybrane są wyświetlane jako wyskakujące powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="109e0-164">Notifications for hello selected categories appear as toast notifications.</span></span>
     
     ![][14]

## <a name="next-steps"></a><span data-ttu-id="109e0-165">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="109e0-165">Next steps</span></span>
<span data-ttu-id="109e0-166">W tym samouczku opisano sposób toobroadcast krytyczne według kategorii wiadomości.</span><span class="sxs-lookup"><span data-stu-id="109e0-166">In this tutorial we learned how toobroadcast breaking news by category.</span></span> <span data-ttu-id="109e0-167">Należy rozważyć wykonanie jednej hello następujące samouczki dotyczące innych zaawansowanych scenariuszy centra powiadomień:</span><span class="sxs-lookup"><span data-stu-id="109e0-167">Consider completing one of hello following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="109e0-168">[Użyj usługi Notification Hubs toobroadcast zlokalizowane najważniejszych wiadomości]</span><span class="sxs-lookup"><span data-stu-id="109e0-168">[Use Notification Hubs toobroadcast localized breaking news]</span></span>
  
    <span data-ttu-id="109e0-169">Dowiedz się, jak fundamentalne wysyłania tooenable aplikacji wiadomości powitania tooexpand zlokalizowane powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="109e0-169">Learn how tooexpand hello breaking news app tooenable sending localized notifications.</span></span>

<!-- Anchors. -->
[Add category selection toohello app]: #adding-categories
[Register for notifications]: #register
[Send notifications from your back-end]: #send
[Run hello app and generate notifications]: #test-app
[Next Steps]: #next-steps

<!-- Images. -->
[1]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-breakingnews-win1.png

[14]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-windows-toast-2.png


[19]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-windows-reg-2.png

<!-- URLs.-->
[get-started]: /manage/services/notification-hubs/getting-started-windows-dotnet/
[Użyj usługi Notification Hubs toobroadcast zlokalizowane najważniejszych wiadomości]: /manage/services/notification-hubs/breaking-news-localized-dotnet/
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users
[Mobile Service]: /develop/mobile/tutorials/get-started/
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
