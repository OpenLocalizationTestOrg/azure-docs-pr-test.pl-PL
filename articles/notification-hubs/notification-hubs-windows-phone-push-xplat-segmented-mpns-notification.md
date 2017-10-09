---
title: "toosend usługi Notification Hubs aaaUse fundamentalne wiadomości (Windows Phone)"
description: "Użyj usługi Azure Notification Hubs toouse tag w toosend rejestracje fundamentalne aplikacji Windows Phone tooa wiadomości."
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
ms.openlocfilehash: 3519a8701105f88198afe288e59e9204420234db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-breaking-news"></a>Użyj usługi Notification Hubs toosend fundamentalne wiadomości
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a>Omówienie
W tym temacie opisano sposób toouse usługi Azure Notification Hubs toobroadcast najważniejszych wiadomości powiadomienia tooa Windows Phone 8.0/8.1 Silverlight aplikacji. Jeśli ma być przeznaczona dla aplikacji Windows Phone 8.1 lub Sklepu Windows, zobacz tootoohello [uniwersalnych systemu Windows](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md) wersji. Po zakończeniu będzie być może tooregister zakłócenia w kategorii wiadomości i odbierać tylko powiadomienia wypychane dla tych kategorii. Ten scenariusz jest wspólnego wzorca dla wielu aplikacji, w której powiadomienia mają toogroups toobe wysyłane użytkowników, które wcześniej zostały zadeklarowane zainteresowanie je, np. czytnik danych RSS, aplikacje wentylatory utworów muzycznych itp.

Scenariusze emisji są włączone, umieszczając w niej co najmniej jeden *tagi* podczas tworzenia rejestracji w Centrum powiadomień hello. Gdy tooa tag wysyłane są powiadomienia, wszystkie urządzenia, które zostały zarejestrowane dla tagu hello będzie wysyłane powiadomienie hello. Ponieważ tagi są po prostu ciągów, nie mają toobe udostępnione wcześniej. Aby uzyskać więcej informacji na temat tagów, zobacz zbyt[routingu centra powiadomień i wyrażeń tagów](notification-hubs-tags-segment-push-message.md).

## <a name="prerequisites"></a>Wymagania wstępne
W tym temacie opiera się na aplikacji hello utworzony w [Rozpoczynanie pracy z usługą Notification Hubs]. Przed rozpoczęciem tego samouczka należy zostały już wykonane [Rozpoczynanie pracy z usługą Notification Hubs].

## <a name="add-category-selection-toohello-app"></a>Dodaj aplikację toohello wybór kategorii
Witaj pierwszym krokiem jest tooadd hello interfejsu użytkownika elementy tooyour istniejącej strony głównej umożliwiające hello użytkownika tooselect kategorii tooregister. Witaj kategorie wybrane przez użytkownika są przechowywane na urządzeniu hello. Po uruchomieniu aplikacji hello rejestracji urządzenia jest tworzony w Centrum powiadomień z kategorii hello wybrany jako znaczniki.

1. Otwórz plik projektu MainPage.xaml hello, a następnie zastąp hello **siatki** elementy o nazwie `TitlePanel` i `ContentPanel` z hello następującego kodu:
   
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
2. W projekcie hello, Utwórz nową klasę o nazwie **powiadomienia**, Dodaj hello **publicznego** toohello modyfikator klasy definicji, a następnie dodaj poniższe hello **przy użyciu** — instrukcje toohello nowy plik kodu:
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
        using System.IO.IsolatedStorage;
        using System.Windows;
3. Kopiuj hello poniższy kod do nowego hello **powiadomienia** klasy:
   
        private NotificationHub hub;
   
        // Registration task toocomplete registration in hello ChannelUriUpdated event handler
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
   
                // This is optional, used tooreceive notifications while hello app is running.
                channel.ShellToastNotificationReceived += channel_ShellToastNotificationReceived;
            }
   
            // If channel.ChannelUri is not null, we will complete hello registrationTask here.  
            // If it is null, hello registrationTask will be completed in hello ChannelUriUpdated event handler.
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
            // Using a template registration toosupport notifications across platforms.
            // Any template notifications that contain messageParam and a corresponding tag expression
            // will be delivered for this registration.
   
            const string templateBodyMPNS = "<wp:Notification xmlns:wp=\"WPNotification\">" +
                                                "<wp:Toast>" +
                                                    "<wp:Text1>$(messageParam)</wp:Text1>" +
                                                "</wp:Toast>" +
                                            "</wp:Notification>";
   
            // hello stored categories tags are passed with hello template registration.
   
            registrationTask.SetResult(await hub.RegisterTemplateAsync(channelUri.ToString(), 
                templateBodyMPNS, "simpleMPNSTemplateExample", this.RetrieveCategories()));
   
            return await registrationTask.Task;
        }
   
        // This is optional. It is used tooreceive notifications while hello app is running.
        void channel_ShellToastNotificationReceived(object sender, NotificationEventArgs e)
        {
            StringBuilder message = new StringBuilder();
            string relativeUri = string.Empty;
   
            message.AppendFormat("Received Toast {0}:\n", DateTime.Now.ToShortTimeString());
   
            // Parse out hello information that was part of hello message.
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
   
            // Display a dialog of all hello fields in hello toast.
            System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() => 
            { 
                MessageBox.Show(message.ToString()); 
            });
        }

    Ta klasa korzysta z kategorii hello toostore magazynowania hello izolowane wiadomości, czy to urządzenie jest tooreceive. Zawiera również metody tooregister dla tych kategorii przy użyciu [szablonu](notification-hubs-templates-cross-platform-push-messages.md) rejestracji powiadomień.


1. W pliku projektu App.xaml.cs hello, Dodaj następujące właściwości toohello hello **aplikacji** klasy. Zastąp hello `<hub name>` i `<connection string with listen access>` symbole zastępcze z powiadomienia Centrum nazwy i hello parametrów połączenia dla *DefaultListenSharedAccessSignature* uzyskany wcześniej.
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
   > [!NOTE]
   > Ponieważ poświadczenia, które są dystrybuowane wraz z aplikacji przez klienta nie są zazwyczaj bezpieczna, hello klucz dostępu do nasłuchiwania należy dystrybuować tylko z aplikacji klienta. Nasłuchiwanie umożliwia dostęp, nie można zmodyfikować tooregister Twojej aplikacji dla powiadomień, ale istniejące rejestracje i nie mogą być wysyłane powiadomienia. klucz pełny dostęp Hello jest używany w usłudze zabezpieczonych wewnętrznej bazy danych do wysyłania powiadomień i zmianę istniejącego rejestracji.
   > 
   > 
2. W Twojej MainPage.xaml.cs Dodaj powitania po wierszu:
   
        using Windows.UI.Popups;
3. W pliku projektu hello MainPage.xaml.cs Dodaj hello następujące metody:
   
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
   
    Ta metoda tworzy listę kategorii i używa hello **powiadomienia** klasy toostore hello listy w magazynie lokalnym hello i zarejestruj hello odpowiednie tagi w Centrum powiadomień. Zmiana kategorii rejestracji hello zostaje odtworzone w hello nowych kategorii.

Aplikacji jest teraz możliwe toostore zestaw kategorii w lokalnej pamięci masowej na powitania urządzenia i rejestruje hello Centrum powiadomień, gdy wybór kategorii hello hello zmiany wprowadzane przez użytkownika.

## <a name="register-for-notifications"></a>Rejestrowanie się w celu powiadomienia
Następujące kroki, zarejestruj się w Centrum powiadomień hello podczas uruchamiania przy użyciu hello kategorie, które były przechowywane w magazynie lokalnym.

> [!NOTE]
> Ponieważ kanał hello URI przypisał hello usługi powiadomień wypychanych firmy Microsoft (MPNS) można zmienić w dowolnym momencie, należy zarejestrować powiadomienia o często tooavoid powiadomień błędów. W tym przykładzie rejestruje powiadomienia o każdym uruchomieniu danej aplikacji hello. Dla aplikacji, które są uruchamiane często więcej niż raz dziennie, prawdopodobnie Jeśli możesz pominąć rejestrację toopreserve przepustowości od poprzedniej rejestracji hello upłynął krótszy niż doba.
> 
> 

1. Otwórz plik App.xaml.cs hello i Dodaj hello **async** modyfikator zbyt**Application_Launching** metodę i Zastąp kod rejestracji usługi Notification Hubs hello, dodanego w [Rozpoczynanie pracy z usługą Notification Hubs] z hello następującego kodu:
   
        private async void Application_Launching(object sender, LaunchingEventArgs e)
        {
            var result = await notifications.SubscribeToCategories();
   
            if (result != null)
                System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() =>
                {
                    MessageBox.Show("Registration Id :" + result.RegistrationId, "Registered", MessageBoxButton.OK);
                });
        }
   
    Dzięki temu że każdym uruchomieniu aplikacji hello pobiera kategorie hello z magazynu lokalnego i żądań rejestracji dla tych kategorii.
2. W pliku projektu hello MainPage.xaml.cs Dodaj hello następującego kodu, który implementuje hello **OnNavigatedTo** metody:
   
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
   
    Tej aktualizacji hello głównej strony na podstawie stanu hello wcześniej zapisane kategorii.

Aplikacja Hello jest teraz ukończona i może przechowywać zestawu kategorii hello urządzenia magazynu lokalnego używane tooregister hello Centrum powiadomień przy każdym zmiany użytkowników hello hello wybór kategorii. Następnie zdefiniujemy wewnętrznej bazy danych, który może wysyłać kategorii powiadomienia toothis aplikacji.

## <a name="sending-tagged-notifications"></a>Wysyłanie powiadomień oznakowany
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-hello-app-and-generate-notifications"></a>Uruchamianie aplikacji hello i generować powiadomienia
1. W programie Visual Studio naciśnij klawisz F5 toocompile i uruchomić aplikacji hello.
   
    ![][1]
   
    Należy pamiętać, że przełącza, aplikacja hello, które interfejs użytkownika zawiera zestaw, który umożliwia wybranie hello toosubscribe kategorii do.
2. Włącz co najmniej jeden przełącza kategorie, a następnie kliknij przycisk **Subskrybuj**.
   
    Aplikacja Hello konwertuje kategorii hello wybrane tagi i żąda nowej rejestracji urządzenia hello wybrane tagów z Centrum powiadomień hello. Witaj zarejestrowanych kategorie są zwracane i wyświetlane w oknie dialogowym.
   
    ![][2]
3. Po otrzymaniu potwierdzenia, że kategorie zostały ukończone subskrypcji, uruchom program toosend aplikacji hello konsoli powiadomień dla każdej kategorii. Sprawdź, czy tylko otrzymasz powiadomienie o kategoriach hello, które subskrybujesz.
   
    ![][3]

W tym temacie została ukończona.

<!--##Next steps

In this tutorial we learned how toobroadcast breaking news by category. Consider completing one of hello following tutorials that highlight other advanced Notification Hubs scenarios:

+ [Use Notification Hubs toobroadcast localized breaking news]

    Learn how tooexpand hello breaking news app tooenable sending localized notifications.

+ [Notify users with Notification Hubs]

    Learn how toopush notifications toospecific authenticated users. This is a good solution for sending notifications only toospecific users.
-->

<!-- Anchors. -->
[Add category selection toohello app]: #adding-categories
[Register for notifications]: #register
[Send notifications from your back-end]: #send
[Run hello app and generate notifications]: #test-app
[Next Steps]: #next-steps

<!-- Images. -->
[1]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-breakingnews.png
[2]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-registration.png
[3]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-toast.png



<!-- URLs.-->
[Rozpoczynanie pracy z usługą Notification Hubs]: /manage/services/notification-hubs/get-started-notification-hubs-wp8/
[Use Notification Hubs toobroadcast localized breaking news]: ../breakingnews-localized-wp8.md
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users/
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor Windows Phone]: ??

