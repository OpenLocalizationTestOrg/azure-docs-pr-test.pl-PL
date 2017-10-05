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
# <a name="use-notification-hubs-to-send-breaking-news"></a>Wysyłanie najważniejszych wiadomości przy użyciu usługi Notification Hubs
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a>Omówienie
W tym temacie przedstawiono sposób użycia usługi Azure Notification Hubs wysyłać powiadomienia o najważniejszych wiadomościach do Sklepu Windows lub Windows Phone 8.1 (z systemem innym niż platformy Silverlight) aplikacji. Jeśli aplikacja ma być przeznaczona dla systemu Windows Phone 8.1 z platformą Silverlight, zapoznaj się z wersją dla systemu [Windows Phone](notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md). Po zakończeniu będzie można rejestrować zakłócenia w kategorii wiadomości i odbierać tylko powiadomienia wypychane dla tych kategorii. Ten scenariusz jest wspólnego wzorca dla wielu aplikacji, w której powiadomienia muszą być wysłane do grup użytkowników, którzy wcześniej zadeklarowany jako zainteresowanie je, np. czytnik danych RSS, aplikacje dla wentylatory muzyka i tak dalej. 

Scenariusze emisji są włączone, umieszczając w niej co najmniej jeden *tagi* podczas tworzenia rejestracji w Centrum powiadomień. Gdy powiadomienia są wysyłane do tagu, wszystkie urządzenia, które zostały zarejestrowane dla tagu będą otrzymywać powiadomienia. Ponieważ tagi są po prostu ciągów, nie mają być przygotowana z wyprzedzeniem. Aby uzyskać więcej informacji na temat tagów, zapoznaj się [routingu centra powiadomień i wyrażeń tagów](notification-hubs-tags-segment-push-message.md).

> [!NOTE]
> Sklep Windows i wersji projektów Windows Phone 8.1 i starsze nie są obsługiwane w programie Visual Studio 2017 r.  Aby uzyskać więcej informacji, zobacz [Obsługiwane platformy i zgodność programu Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs). 

## <a name="prerequisites"></a>Wymagania wstępne
W tym temacie opiera się na aplikacji utworzony w [Rozpoczynanie pracy z usługą Notification Hubs][get-started]. Przed rozpoczęciem tego samouczka należy zostały już wykonane [Rozpoczynanie pracy z usługą Notification Hubs][get-started].

## <a name="add-category-selection-to-the-app"></a>Dodaj wybrane kategorii do aplikacji
Pierwszym krokiem jest dodać elementy interfejsu użytkownika do strony głównej istniejących umożliwiają użytkownikowi wybierz kategorie, aby zarejestrować. Kategorie wybrane przez użytkownika są przechowywane na urządzeniu. Po uruchomieniu aplikacji, rejestracji urządzenia jest tworzony w Centrum powiadomień z wybranych kategorii jako znaczniki.

1. Otwórz plik projektu MainPage.xaml, a następnie skopiuj następujący kod w **siatki** elementu:
   
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
2. Kliknij prawym przyciskiem myszy **Shared** projektu i dodać nową klasę o nazwie **powiadomienia**, Dodaj **publicznego** modyfikator do definicji klasy, a następnie dodaj następujące  **przy użyciu** instrukcje do nowego pliku kodu:
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.Storage;
        using System.Threading.Tasks;
3. Skopiuj następujący kod do nowej **powiadomienia** klasy:
   
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
   
    Ta klasa używa lokalnego magazynu do przechowywania kategorii wiadomości, który to urządzenie musi odebrać. Należy pamiętać, że zamiast wywoływać metodę *RegisterNativeAsync* metody nazywamy *RegisterTemplateAsync* do zarejestrowania dla kategorii przy użyciu rejestracji szablonu. 
   
    Również udostępniamy nazwę dla szablonu ("simpleWNSTemplateExample"), ponieważ chcemy zarejestrować więcej niż jednego szablonu (na przykład jeden dla wyskakujące powiadomienia) i drugi dla kafelków i musimy ich nazw, aby można było zaktualizować lub usunąć je.
   
    Należy pamiętać, że jeśli urządzenie rejestruje wiele szablonów z tym samym tagiem, przychodzących wiadomości przeznaczonych dla który tag spowoduje wiele powiadomień dostarczony do urządzenia, (po jednej dla każdego szablonu). To zachowanie jest przydatne, gdy ten sam komunikat logiczne ma zastosowanie w wielu powiadomienia wizualne, na przykład zawierający wskaźnika i użyciu powiadomienia wyskakującego w aplikacji Sklepu Windows.
   
    Aby uzyskać więcej informacji dotyczących szablonów, zobacz [szablony](notification-hubs-templates-cross-platform-push-messages.md).
4. W pliku projektu App.xaml.cs Dodaj następującą właściwość, aby **aplikacji** klasy:
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
    Ta właściwość jest używana do tworzenia i dostępu **powiadomienia** wystąpienia.
   
    W powyższym kodzie Zamień `<hub name>` i `<connection string with listen access>` symbole zastępcze nazwą Centrum powiadomień i parametry połączenia dla *DefaultListenSharedAccessSignature* uzyskany wcześniej.
   
   > [!NOTE]
   > Ponieważ poświadczenia, które są dystrybuowane wraz z aplikacji przez klienta nie są zazwyczaj bezpieczna, klucz dostępu do nasłuchiwania należy dystrybuować tylko z aplikacji klienta. Nasłuchiwanie umożliwia dostęp, nie można zmodyfikować aplikację, aby zarejestrować dla powiadomień, ale istniejące rejestracje i nie mogą być wysyłane powiadomienia. Klucz pełny dostęp jest używany w usłudze zabezpieczonych wewnętrznej bazy danych do wysyłania powiadomień i zmianę istniejącego rejestracji.
   > 
   > 
5. W Twojej MainPage.xaml.cs Dodaj następujący wiersz:
   
        using Windows.UI.Popups;
6. W pliku MainPage.xaml.cs projekt Dodaj następującą metodę:
   
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
   
    Ta metoda tworzy listę kategorii i używa **powiadomienia** klasy przechowywania listy w magazynie lokalnym i rejestracji, odpowiednie znaczniki w Centrum powiadomień. Zmiana kategorii rejestracji zostaje odtworzone w nowej kategorii.

Aplikacja jest teraz możliwość przechowywania zestawu kategorii w lokalnej pamięci masowej na urządzeniu i Zarejestruj w Centrum powiadomień, zawsze, gdy użytkownik zmieni się zaznaczenie kategorii.

## <a name="register-for-notifications"></a>Rejestrowanie się w celu powiadomienia
Następujące kroki, zarejestruj się w Centrum powiadomień przy uruchamianiu przy użyciu kategorii, które były przechowywane w magazynie lokalnym.

> [!NOTE]
> Ponieważ identyfikator URI przypisany przez usługę powiadomień systemu Windows (WNS) kanału można zmienić w dowolnym momencie, należy zarejestrować powiadomień często uniknąć niepowodzeń powiadomień. W tym przykładzie rejestruje powiadomienia każdym uruchomieniu aplikacji. Dla aplikacji, które są uruchamiane często więcej niż raz dziennie, można prawdopodobnie pominąć rejestrację, aby zachować przepustowość, jeśli krótszy niż doba upłynął od czasu poprzedniej rejestracji.
> 
> 

1. Otwórz plik App.xaml.cs i aktualizacji **InitNotificationsAsync** metodę `notifications` klasy do subskrybowania na podstawie kategorii.
   
        // *** Remove or comment out these lines *** 
        //var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
        //var hub = new NotificationHub("your hub name", "your listen connection string");
        //var result = await hub.RegisterNativeAsync(channel.Uri);
   
        var result = await notifications.SubscribeToCategories();
   
    Dzięki temu przy każdym uruchomieniu aplikacji it pobiera kategorie z magazynu lokalnego i żąda rejestracja dla tych kategorii. **InitNotificationsAsync** metody został utworzony jako część [Rozpoczynanie pracy z usługą Notification Hubs] [ get-started] samouczka.
2. W pliku MainPage.xaml.cs projekt, Dodaj następujący kod do *OnNavigatedTo* metody:
   
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
   
    Spowoduje to zaktualizowanie strony głównej na podstawie kategorii uprzednio zapisanego stanu.

Aplikacja jest teraz ukończona i może przechowywać zestawu kategorii w magazynie lokalnym urządzenia używane do rejestrowania w Centrum powiadomień, zawsze, gdy użytkownik zmieni się zaznaczenie kategorii. Następnie zdefiniujemy wewnętrznej bazy danych, który może wysyłać powiadomienia kategorii do tej aplikacji.

## <a name="sending-tagged-notifications"></a>Wysyłanie powiadomień oznakowany
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-the-app-and-generate-notifications"></a>Uruchom aplikację i generować powiadomienia
1. W programie Visual Studio naciśnij klawisz F5, aby skompilować i uruchomić aplikację.
   
    ![][1]
   
    Należy pamiętać, że aplikacja interfejsu użytkownika zawiera zestaw przełącza umożliwiające wybierz kategorie, aby subskrybować.
2. Włącz co najmniej jeden przełącza kategorie, a następnie kliknij przycisk **Subskrybuj**.
   
    Konwertuje wybranych kategorii do tagów i żąda nowej rejestracji urządzeń dla wybranych tagów z Centrum powiadomień aplikacji. Zarejestrowany kategorie są zwracane i wyświetlane w oknie dialogowym.
   
    ![][19]
3. Wyślij nowe powiadomienie z wewnętrznej bazy danych w jednym z następujących sposobów:
   
   * **Aplikacja konsoli:** uruchomić aplikację konsoli.
   * **Java/PHP:** uruchamiania aplikacji lub skryptu.
     
     Powiadomienia dotyczące wybranych kategorii są wyświetlane jako wyskakujące powiadomienia.
     
     ![][14]

## <a name="next-steps"></a>Następne kroki
W tym samouczku opisano sposób emisji najważniejszych wiadomości według kategorii. Należy rozważyć wykonanie jednej z następujących samouczków, w których są wyróżniane innych zaawansowanych scenariuszy centra powiadomień:

* [Emisji zlokalizowanych najważniejszych wiadomości przy użyciu usługi Notification Hubs]
  
    Dowiedz się, jak rozszerzyć aplikację wiadomości podziału, aby umożliwić wysyłanie powiadomień zlokalizowane.

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
[Emisji zlokalizowanych najważniejszych wiadomości przy użyciu usługi Notification Hubs]: /manage/services/notification-hubs/breaking-news-localized-dotnet/
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users
[Mobile Service]: /develop/mobile/tutorials/get-started/
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-To for Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
