---
title: "Wysyłanie najważniejszych wiadomości (Windows Phone) przy użyciu usługi Notification Hubs"
description: "Za pomocą usługi Azure Notification Hubs do tagu w rejestracji wysyłanie najważniejszych wiadomości do aplikacji Windows Phone."
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: 
ms.assetid: 42726bf5-cc82-438d-9eaa-238da3322d80
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 3a6a69bf555c7267d3fbeb03ff6c03054991960f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-notification-hubs-to-send-breaking-news"></a><span data-ttu-id="c506c-103">Wysyłanie najważniejszych wiadomości przy użyciu usługi Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="c506c-103">Use Notification Hubs to send breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="c506c-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="c506c-104">Overview</span></span>
<span data-ttu-id="c506c-105">W tym temacie przedstawiono sposób użycia usługi Azure Notification Hubs wysyłać powiadomienia o najważniejszych wiadomościach do aplikacji Windows Phone 8.0/8.1 Silverlight.</span><span class="sxs-lookup"><span data-stu-id="c506c-105">This topic shows you how to use Azure Notification Hubs to broadcast breaking news notifications to a Windows Phone 8.0/8.1 Silverlight app.</span></span> <span data-ttu-id="c506c-106">Jeśli ma być przeznaczona dla aplikacji Windows Phone 8.1 lub Sklepu Windows, zapoznaj się do [uniwersalnych systemu Windows](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md) wersji.</span><span class="sxs-lookup"><span data-stu-id="c506c-106">If you are targeting Windows Store or Windows Phone 8.1 app, please refer to to the [Windows Universal](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md) version.</span></span> <span data-ttu-id="c506c-107">Po zakończeniu będzie można rejestrować zakłócenia w kategorii wiadomości i odbierać tylko powiadomienia wypychane dla tych kategorii.</span><span class="sxs-lookup"><span data-stu-id="c506c-107">When complete, you will be able to register for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="c506c-108">Ten scenariusz jest wspólnego wzorca dla wielu aplikacji, gdzie powiadomienia muszą być wysłane do grup użytkowników, które wcześniej zostały zadeklarowane zainteresowanie je, np. czytnik danych RSS, aplikacje wentylatory utworów muzycznych itp.</span><span class="sxs-lookup"><span data-stu-id="c506c-108">This scenario is a common pattern for many apps where notifications have to be sent to groups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="c506c-109">Scenariusze emisji są włączone, umieszczając w niej co najmniej jeden *tagi* podczas tworzenia rejestracji w Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="c506c-109">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in the notification hub.</span></span> <span data-ttu-id="c506c-110">Gdy powiadomienia są wysyłane do tagu, wszystkie urządzenia, które zostały zarejestrowane dla tagu będą otrzymywać powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="c506c-110">When notifications are sent to a tag, all devices that have registered for the tag will receive the notification.</span></span> <span data-ttu-id="c506c-111">Ponieważ tagi są po prostu ciągów, nie mają być przygotowana z wyprzedzeniem.</span><span class="sxs-lookup"><span data-stu-id="c506c-111">Because tags are simply strings, they do not have to be provisioned in advance.</span></span> <span data-ttu-id="c506c-112">Aby uzyskać więcej informacji na temat tagów, zapoznaj się [routingu centra powiadomień i wyrażeń tagów](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="c506c-112">For more information about tags, refer to [Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c506c-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c506c-113">Prerequisites</span></span>
<span data-ttu-id="c506c-114">W tym temacie opiera się na aplikacji utworzony w [Rozpoczynanie pracy z usługą Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="c506c-114">This topic builds on the app you created in [Get started with Notification Hubs].</span></span> <span data-ttu-id="c506c-115">Przed rozpoczęciem tego samouczka należy zostały już wykonane [Rozpoczynanie pracy z usługą Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="c506c-115">Before starting this tutorial, you must have already completed [Get started with Notification Hubs].</span></span>

## <a name="add-category-selection-to-the-app"></a><span data-ttu-id="c506c-116">Dodaj wybrane kategorii do aplikacji</span><span class="sxs-lookup"><span data-stu-id="c506c-116">Add category selection to the app</span></span>
<span data-ttu-id="c506c-117">Pierwszym krokiem jest dodać elementy interfejsu użytkownika do strony głównej istniejących umożliwiają użytkownikowi wybierz kategorie, aby zarejestrować.</span><span class="sxs-lookup"><span data-stu-id="c506c-117">The first step is to add the UI elements to your existing main page that enable the user to select categories to register.</span></span> <span data-ttu-id="c506c-118">Kategorie wybrane przez użytkownika są przechowywane na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="c506c-118">The categories selected by a user are stored on the device.</span></span> <span data-ttu-id="c506c-119">Po uruchomieniu aplikacji, rejestracji urządzenia jest tworzony w Centrum powiadomień z wybranych kategorii jako znaczniki.</span><span class="sxs-lookup"><span data-stu-id="c506c-119">When the app starts, a device registration is created in your notification hub with the selected categories as tags.</span></span>

1. <span data-ttu-id="c506c-120">Otwórz plik projektu MainPage.xaml, a następnie zastąp **siatki** elementy o nazwie `TitlePanel` i `ContentPanel` z następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="c506c-120">Open the MainPage.xaml project file, then replace the **Grid** elements named `TitlePanel` and `ContentPanel` with the following code:</span></span>
   
        <StackPanel x:Name="TitlePanel" Grid.Row="0" Margin="12,17,0,28">
            <TextBlock Text="Breaking News" Style="{StaticResource PhoneTextNormalStyle}" Margin="12,0"/>
            <TextBlock Text="Categories" Margin="9,-7,0,0" Style="{StaticResource PhoneTextTitle1Style}"/>
        </StackPanel>
   
        <Grid Name="ContentPanel" Grid.Row="1" Margin="12,0,12,0">
            <Grid.RowDefinitions>
                <RowDefinition Height="auto"/>
                <RowDefinition Height="auto" />
                <RowDefinition Height="auto" />
                <RowDefinition Height="auto" />
            </Grid.RowDefinitions>
            <Grid.ColumnDefinitions>
                <ColumnDefinition />
                <ColumnDefinition />
            </Grid.ColumnDefinitions>
            <CheckBox Name="WorldCheckBox" Grid.Row="0" Grid.Column="0">World</CheckBox>
            <CheckBox Name="PoliticsCheckBox" Grid.Row="1" Grid.Column="0">Politics</CheckBox>
            <CheckBox Name="BusinessCheckBox" Grid.Row="2" Grid.Column="0">Business</CheckBox>
            <CheckBox Name="TechnologyCheckBox" Grid.Row="0" Grid.Column="1">Technology</CheckBox>
            <CheckBox Name="ScienceCheckBox" Grid.Row="1" Grid.Column="1">Science</CheckBox>
            <CheckBox Name="SportsCheckBox" Grid.Row="2" Grid.Column="1">Sports</CheckBox>
            <Button Name="SubscribeButton" Content="Subscribe" HorizontalAlignment="Center" Grid.Row="3" Grid.Column="0" Grid.ColumnSpan="2" Click="SubscribeButton_Click" />
        </Grid>
2. <span data-ttu-id="c506c-121">W projekcie, Utwórz nową klasę o nazwie **powiadomienia**, Dodaj **publicznego** modyfikator do definicji klasy, a następnie dodaj następujące **przy użyciu** instrukcje do nowego pliku kodu:</span><span class="sxs-lookup"><span data-stu-id="c506c-121">In the project, create a new class named **Notifications**, add the **public** modifier to the class definition, then add the following **using** statements to the new code file:</span></span>
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
        using System.IO.IsolatedStorage;
        using System.Windows;
3. <span data-ttu-id="c506c-122">Skopiuj następujący kod do nowej **powiadomienia** klasy:</span><span class="sxs-lookup"><span data-stu-id="c506c-122">Copy the following code into the new **Notifications** class:</span></span>
   
        private NotificationHub hub;
   
        // Registration task to complete registration in the ChannelUriUpdated event handler
        private TaskCompletionSource<Registration> registrationTask;
   
        public Notifications(string hubName, string listenConnectionString)
        {
            hub = new NotificationHub(hubName, listenConnectionString);
        }
   
        public IEnumerable<string> RetrieveCategories()
        {
            var categories = (string)IsolatedStorageSettings.ApplicationSettings["categories"];
            return categories != null ? categories.Split(',') : new string[0];
        }
   
        public async Task<Registration> StoreCategoriesAndSubscribe(IEnumerable<string> categories)
        {
            var categoriesAsString = string.Join(",", categories);
            var settings = IsolatedStorageSettings.ApplicationSettings;
            if (!settings.Contains("categories"))
            {
                settings.Add("categories", categoriesAsString);
            }
            else
            {
                settings["categories"] = categoriesAsString;
            }
            settings.Save();
   
            return await SubscribeToCategories();
        }
   
        public async Task<Registration> SubscribeToCategories()
        {
            registrationTask = new TaskCompletionSource<Registration>();
   
            var channel = HttpNotificationChannel.Find("MyPushChannel");
   
            if (channel == null)
            {
                channel = new HttpNotificationChannel("MyPushChannel");
                channel.Open();
                channel.BindToShellToast();
                channel.ChannelUriUpdated += channel_ChannelUriUpdated;
   
                // This is optional, used to receive notifications while the app is running.
                channel.ShellToastNotificationReceived += channel_ShellToastNotificationReceived;
            }
   
            // If channel.ChannelUri is not null, we will complete the registrationTask here.  
            // If it is null, the registrationTask will be completed in the ChannelUriUpdated event handler.
            if (channel.ChannelUri != null)
            {
                await RegisterTemplate(channel.ChannelUri);
            }
   
            return await registrationTask.Task;
        }
   
        async void channel_ChannelUriUpdated(object sender, NotificationChannelUriEventArgs e)
        {
            await RegisterTemplate(e.ChannelUri);
        }
   
        async Task<Registration> RegisterTemplate(Uri channelUri)
        {
            // Using a template registration to support notifications across platforms.
            // Any template notifications that contain messageParam and a corresponding tag expression
            // will be delivered for this registration.
   
            const string templateBodyMPNS = "<wp:Notification xmlns:wp=\"WPNotification\">" +
                                                "<wp:Toast>" +
                                                    "<wp:Text1>$(messageParam)</wp:Text1>" +
                                                "</wp:Toast>" +
                                            "</wp:Notification>";
   
            // The stored categories tags are passed with the template registration.
   
            registrationTask.SetResult(await hub.RegisterTemplateAsync(channelUri.ToString(), 
                templateBodyMPNS, "simpleMPNSTemplateExample", this.RetrieveCategories()));
   
            return await registrationTask.Task;
        }
   
        // This is optional. It is used to receive notifications while the app is running.
        void channel_ShellToastNotificationReceived(object sender, NotificationEventArgs e)
        {
            StringBuilder message = new StringBuilder();
            string relativeUri = string.Empty;
   
            message.AppendFormat("Received Toast {0}:\n", DateTime.Now.ToShortTimeString());
   
            // Parse out the information that was part of the message.
            foreach (string key in e.Collection.Keys)
            {
                message.AppendFormat("{0}: {1}\n", key, e.Collection[key]);
   
                if (string.Compare(
                    key,
                    "wp:Param",
                    System.Globalization.CultureInfo.InvariantCulture,
                    System.Globalization.CompareOptions.IgnoreCase) == 0)
                {
                    relativeUri = e.Collection[key];
                }
            }
   
            // Display a dialog of all the fields in the toast.
            System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() => 
            { 
                MessageBox.Show(message.ToString()); 
            });
        }

    <span data-ttu-id="c506c-123">Ta klasa używa izolowanego magazynu do przechowywania kategorii wiadomości, który ma otrzymać tego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="c506c-123">This class uses the isolated storage to store the categories of news that this device is to receive.</span></span> <span data-ttu-id="c506c-124">Zawiera również metody do rejestrowania dla tych kategorii przy użyciu [szablonu](notification-hubs-templates-cross-platform-push-messages.md) rejestracji powiadomień.</span><span class="sxs-lookup"><span data-stu-id="c506c-124">It also contains methods to register for these categories using a [template](notification-hubs-templates-cross-platform-push-messages.md) notification registration.</span></span>


1. <span data-ttu-id="c506c-125">W pliku projektu App.xaml.cs Dodaj następującą właściwość, aby **aplikacji** klasy.</span><span class="sxs-lookup"><span data-stu-id="c506c-125">In the App.xaml.cs project file, add the following property to the **App** class.</span></span> <span data-ttu-id="c506c-126">Zastąp `<hub name>` i `<connection string with listen access>` symbole zastępcze nazwą Centrum powiadomień i parametry połączenia dla *DefaultListenSharedAccessSignature* uzyskany wcześniej.</span><span class="sxs-lookup"><span data-stu-id="c506c-126">Replace the `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and the connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
   > [!NOTE]
   > <span data-ttu-id="c506c-127">Ponieważ poświadczenia, które są dystrybuowane wraz z aplikacji przez klienta nie są zazwyczaj bezpieczna, klucz dostępu do nasłuchiwania należy dystrybuować tylko z aplikacji klienta.</span><span class="sxs-lookup"><span data-stu-id="c506c-127">Because credentials that are distributed with a client app are not generally secure, you should only distribute the key for listen access with your client app.</span></span> <span data-ttu-id="c506c-128">Nasłuchiwanie umożliwia dostęp, nie można zmodyfikować aplikację, aby zarejestrować dla powiadomień, ale istniejące rejestracje i nie mogą być wysyłane powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="c506c-128">Listen access enables your app to register for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="c506c-129">Klucz pełny dostęp jest używany w usłudze zabezpieczonych wewnętrznej bazy danych do wysyłania powiadomień i zmianę istniejącego rejestracji.</span><span class="sxs-lookup"><span data-stu-id="c506c-129">The full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
2. <span data-ttu-id="c506c-130">W Twojej MainPage.xaml.cs Dodaj następujący wiersz:</span><span class="sxs-lookup"><span data-stu-id="c506c-130">In your MainPage.xaml.cs, add the following line:</span></span>
   
        using Windows.UI.Popups;
3. <span data-ttu-id="c506c-131">W pliku MainPage.xaml.cs projekt Dodaj następującą metodę:</span><span class="sxs-lookup"><span data-stu-id="c506c-131">In the MainPage.xaml.cs project file, add the following method:</span></span>
   
        private async void SubscribeButton_Click(object sender, RoutedEventArgs e)
        {
          var categories = new HashSet<string>();
          if (WorldCheckBox.IsChecked == true) categories.Add("World");
          if (PoliticsCheckBox.IsChecked == true) categories.Add("Politics");
          if (BusinessCheckBox.IsChecked == true) categories.Add("Business");
          if (TechnologyCheckBox.IsChecked == true) categories.Add("Technology");
          if (ScienceCheckBox.IsChecked == true) categories.Add("Science");
          if (SportsCheckBox.IsChecked == true) categories.Add("Sports");
   
          var result = await ((App)Application.Current).notifications.StoreCategoriesAndSubscribe(categories);
   
          MessageBox.Show("Subscribed to: " + string.Join(",", categories) + " on registration id : " +
             result.RegistrationId);
        }
   
    <span data-ttu-id="c506c-132">Ta metoda tworzy listę kategorii i używa **powiadomienia** klasy przechowywania listy w magazynie lokalnym i rejestracji, odpowiednie znaczniki w Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="c506c-132">This method creates a list of categories and uses the **Notifications** class to store the list in the local storage and register the corresponding tags with your notification hub.</span></span> <span data-ttu-id="c506c-133">Zmiana kategorii rejestracji zostaje odtworzone w nowej kategorii.</span><span class="sxs-lookup"><span data-stu-id="c506c-133">When categories are changed, the registration is recreated with the new categories.</span></span>

<span data-ttu-id="c506c-134">Aplikacja jest teraz możliwość przechowywania zestawu kategorii w lokalnej pamięci masowej na urządzeniu i Zarejestruj w Centrum powiadomień, zawsze, gdy użytkownik zmieni się zaznaczenie kategorii.</span><span class="sxs-lookup"><span data-stu-id="c506c-134">Your app is now able to store a set of categories in local storage on the device and register with the notification hub whenever the user changes the selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="c506c-135">Rejestrowanie się w celu powiadomienia</span><span class="sxs-lookup"><span data-stu-id="c506c-135">Register for notifications</span></span>
<span data-ttu-id="c506c-136">Następujące kroki, zarejestruj się w Centrum powiadomień przy uruchamianiu przy użyciu kategorii, które były przechowywane w magazynie lokalnym.</span><span class="sxs-lookup"><span data-stu-id="c506c-136">These steps register with the notification hub on startup using the categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="c506c-137">Ponieważ identyfikator URI przypisane przez Microsoft Push Notification Service (MPNS) kanału można zmienić w dowolnym momencie, należy zarejestrować powiadomień często uniknąć niepowodzeń powiadomień.</span><span class="sxs-lookup"><span data-stu-id="c506c-137">Because the channel URI assigned by the Microsoft Push Notification Service (MPNS) can change at any time, you should register for notifications frequently to avoid notification failures.</span></span> <span data-ttu-id="c506c-138">W tym przykładzie rejestruje powiadomienia o każdym uruchomieniu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c506c-138">This example registers for notifications every time that the app starts.</span></span> <span data-ttu-id="c506c-139">Dla aplikacji, które są uruchamiane często więcej niż raz dziennie, można prawdopodobnie pominąć rejestrację, aby zachować przepustowość, jeśli krótszy niż doba upłynął od czasu poprzedniej rejestracji.</span><span class="sxs-lookup"><span data-stu-id="c506c-139">For apps that are run frequently, more than once a day, you can probably skip registration to preserve bandwidth if less than a day has passed since the previous registration.</span></span>
> 
> 

1. <span data-ttu-id="c506c-140">Otwórz plik App.xaml.cs i Dodaj **async** modyfikator do **Application_Launching** metodę i Zastąp rejestracji usługi Notification Hubs kodu tego zostanie dodany do [Rozpoczynanie pracy z usługą Notification Hubs] następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="c506c-140">Open the App.xaml.cs file and add the **async** modifier to **Application_Launching** method and replace the Notification Hubs registration code that you added in [Get started with Notification Hubs] with the following code:</span></span>
   
        private async void Application_Launching(object sender, LaunchingEventArgs e)
        {
            var result = await notifications.SubscribeToCategories();
   
            if (result != null)
                System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() =>
                {
                    MessageBox.Show("Registration Id :" + result.RegistrationId, "Registered", MessageBoxButton.OK);
                });
        }
   
    <span data-ttu-id="c506c-141">Dzięki temu przy każdym uruchomieniu aplikacji it pobiera kategorie z magazynu lokalnego i żądań rejestracji dla tych kategorii.</span><span class="sxs-lookup"><span data-stu-id="c506c-141">This makes sure that every time the app starts it retrieves the categories from local storage and requests a registration for these categories.</span></span>
2. <span data-ttu-id="c506c-142">W pliku MainPage.xaml.cs projekt, Dodaj następujący kod, który implementuje **OnNavigatedTo** metody:</span><span class="sxs-lookup"><span data-stu-id="c506c-142">In the MainPage.xaml.cs project file, add the following code that implements the **OnNavigatedTo** method:</span></span>
   
        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
            var categories = ((App)Application.Current).notifications.RetrieveCategories();
   
            if (categories.Contains("World")) WorldCheckBox.IsChecked = true;
            if (categories.Contains("Politics")) PoliticsCheckBox.IsChecked = true;
            if (categories.Contains("Business")) BusinessCheckBox.IsChecked = true;
            if (categories.Contains("Technology")) TechnologyCheckBox.IsChecked = true;
            if (categories.Contains("Science")) ScienceCheckBox.IsChecked = true;
            if (categories.Contains("Sports")) SportsCheckBox.IsChecked = true;
        }
   
    <span data-ttu-id="c506c-143">Spowoduje to zaktualizowanie strony głównej na podstawie kategorii uprzednio zapisanego stanu.</span><span class="sxs-lookup"><span data-stu-id="c506c-143">This updates the main page based on the status of previously saved categories.</span></span>

<span data-ttu-id="c506c-144">Aplikacja jest teraz ukończona i może przechowywać zestawu kategorii w magazynie lokalnym urządzenia używane do rejestrowania w Centrum powiadomień, zawsze, gdy użytkownik zmieni się zaznaczenie kategorii.</span><span class="sxs-lookup"><span data-stu-id="c506c-144">The app is now complete and can store a set of categories in the device local storage used to register with the notification hub whenever the user changes the selection of categories.</span></span> <span data-ttu-id="c506c-145">Następnie zdefiniujemy wewnętrznej bazy danych, który może wysyłać powiadomienia kategorii do tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c506c-145">Next, we will define a backend that can send category notifications to this app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="c506c-146">Wysyłanie powiadomień oznakowany</span><span class="sxs-lookup"><span data-stu-id="c506c-146">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-the-app-and-generate-notifications"></a><span data-ttu-id="c506c-147">Uruchom aplikację i generować powiadomienia</span><span class="sxs-lookup"><span data-stu-id="c506c-147">Run the app and generate notifications</span></span>
1. <span data-ttu-id="c506c-148">W programie Visual Studio naciśnij klawisz F5, aby skompilować i uruchomić aplikację.</span><span class="sxs-lookup"><span data-stu-id="c506c-148">In Visual Studio, press F5 to compile and start the app.</span></span>
   
    ![][1]
   
    <span data-ttu-id="c506c-149">Należy pamiętać, że aplikacja interfejsu użytkownika zawiera zestaw przełącza umożliwiające wybierz kategorie, aby subskrybować.</span><span class="sxs-lookup"><span data-stu-id="c506c-149">Note that the app UI provides a set of toggles that lets you choose the categories to subscribe to.</span></span>
2. <span data-ttu-id="c506c-150">Włącz co najmniej jeden przełącza kategorie, a następnie kliknij przycisk **Subskrybuj**.</span><span class="sxs-lookup"><span data-stu-id="c506c-150">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="c506c-151">Konwertuje wybranych kategorii do tagów i żąda nowej rejestracji urządzeń dla wybranych tagów z Centrum powiadomień aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c506c-151">The app converts the selected categories into tags and requests a new device registration for the selected tags from the notification hub.</span></span> <span data-ttu-id="c506c-152">Zarejestrowany kategorie są zwracane i wyświetlane w oknie dialogowym.</span><span class="sxs-lookup"><span data-stu-id="c506c-152">The registered categories are returned and displayed in a dialog.</span></span>
   
    ![][2]
3. <span data-ttu-id="c506c-153">Po otrzymaniu potwierdzenia, że kategorie zostały ukończone subskrypcji, uruchom aplikację konsoli do wysyłania powiadomień dla każdej kategorii.</span><span class="sxs-lookup"><span data-stu-id="c506c-153">After receiving a confirmation that your categories were subscription completed, run the console app to send notifications for each categories.</span></span> <span data-ttu-id="c506c-154">Sprawdź, czy tylko otrzymasz powiadomienie dla kategorii, które subskrybujesz.</span><span class="sxs-lookup"><span data-stu-id="c506c-154">Verify you only receive a notification for the categories you have subscribed to.</span></span>
   
    ![][3]

<span data-ttu-id="c506c-155">W tym temacie została ukończona.</span><span class="sxs-lookup"><span data-stu-id="c506c-155">You have completed this topic.</span></span>

<!--##Next steps

In this tutorial we learned how to broadcast breaking news by category. Consider completing one of the following tutorials that highlight other advanced Notification Hubs scenarios:

+ [Use Notification Hubs to broadcast localized breaking news]

    Learn how to expand the breaking news app to enable sending localized notifications.

+ [Notify users with Notification Hubs]

    Learn how to push notifications to specific authenticated users. This is a good solution for sending notifications only to specific users.
-->

<!-- Anchors. -->
[Add category selection to the app]: #adding-categories
[Register for notifications]: #register
[Send notifications from your back-end]: #send
[Run the app and generate notifications]: #test-app
[Next Steps]: #next-steps

<!-- Images. -->
[1]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-breakingnews.png
[2]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-registration.png
[3]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-toast.png



<!-- URLs.-->
<span data-ttu-id="c506c-156">[Rozpoczynanie pracy z usługą Notification Hubs]: /manage/services/notification-hubs/get-started-notification-hubs-wp8/</span><span class="sxs-lookup"><span data-stu-id="c506c-156">[Get started with Notification Hubs]: /manage/services/notification-hubs/get-started-notification-hubs-wp8/</span></span>
[Use Notification Hubs to broadcast localized breaking news]: ../breakingnews-localized-wp8.md
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users/
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-To for Windows Phone]: ??

