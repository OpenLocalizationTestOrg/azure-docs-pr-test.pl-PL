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
# <a name="use-notification-hubs-toosend-breaking-news"></a>Użyj usługi Notification Hubs toosend fundamentalne wiadomości
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a>Omówienie
W tym temacie opisano sposób toobroadcast usługi Azure Notification Hubs toouse fundamentalne aplikacji Windows Phone 8.1 (z systemem innym niż platformy Silverlight) lub Sklepu Windows tooa powiadomień dla wiadomości. Jeśli ma być przeznaczona dla systemu Windows Phone 8.1 Silverlight, zobacz toohello [Windows Phone](notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md) wersji. Po zakończeniu będzie być może tooregister zakłócenia w kategorii wiadomości i odbierać tylko powiadomienia wypychane dla tych kategorii. Ten scenariusz jest wspólnego wzorca dla wielu aplikacji, w której powiadomienia mają toogroups toobe wysyłane użytkowników, którzy wcześniej zadeklarowany jako zainteresowanie je, np. czytnik danych RSS, aplikacje dla wentylatory muzyka i tak dalej. 

Scenariusze emisji są włączone, umieszczając w niej co najmniej jeden *tagi* podczas tworzenia rejestracji w Centrum powiadomień hello. Gdy tooa tag wysyłane są powiadomienia, wszystkie urządzenia, które zostały zarejestrowane dla tagu hello będzie wysyłane powiadomienie hello. Ponieważ tagi są po prostu ciągów, nie mają toobe udostępnione wcześniej. Aby uzyskać więcej informacji na temat tagów, zobacz zbyt[routingu centra powiadomień i wyrażeń tagów](notification-hubs-tags-segment-push-message.md).

> [!NOTE]
> Sklep Windows i wersji projektów Windows Phone 8.1 i starsze nie są obsługiwane w programie Visual Studio 2017 r.  Aby uzyskać więcej informacji, zobacz [Obsługiwane platformy i zgodność programu Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs). 

## <a name="prerequisites"></a>Wymagania wstępne
W tym temacie opiera się na aplikacji hello utworzony w [Rozpoczynanie pracy z usługą Notification Hubs][get-started]. Przed rozpoczęciem tego samouczka należy zostały już wykonane [Rozpoczynanie pracy z usługą Notification Hubs][get-started].

## <a name="add-category-selection-toohello-app"></a>Dodaj aplikację toohello wybór kategorii
Witaj pierwszym krokiem jest tooadd hello interfejsu użytkownika elementy tooyour istniejącej strony głównej umożliwiające hello użytkownika tooselect kategorii tooregister. Witaj kategorie wybrane przez użytkownika są przechowywane na urządzeniu hello. Po uruchomieniu aplikacji hello rejestracji urządzenia jest tworzony w Centrum powiadomień z kategorii hello wybrany jako znaczniki.

1. Otwórz plik projektu MainPage.xaml hello, a następnie hello kopiowania następującego kodu w hello **siatki** elementu:
   
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
2. Powitania kliknij prawym przyciskiem myszy **Shared** projektu i dodać nową klasę o nazwie **powiadomienia**, Dodaj hello **publicznego** toohello modyfikator klasy definicji, a następnie dodaj następujące hello **przy użyciu** instrukcje toohello nowy plik kodu:
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.Storage;
        using System.Threading.Tasks;
3. Kopiuj hello poniższy kod do nowego hello **powiadomienia** klasy:
   
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
   
    Ta klasa korzysta z hello Magazyn lokalny toostore hello kategorii wiadomości, czy to urządzenie ma tooreceive. Należy pamiętać, że zamiast wywoływania hello *RegisterNativeAsync* metody nazywamy *RegisterTemplateAsync* tooregister dla kategorii hello przy użyciu rejestracji szablonu. 
   
    Firma Microsoft udostępnia również nazwę dla szablonu hello ("simpleWNSTemplateExample"), ponieważ firma Microsoft może być tooregister więcej niż jednego szablonu (na przykład po jednej dla wyskakujące powiadomienia) i jeden dla kafelków i potrzebujemy tooname kolejność ich w stanie tooupdate toobe lub usuń je.
   
    Należy pamiętać, że jeśli urządzenie rejestruje wiele szablonów z hello sam tagu wiadomości przychodzącej elementów docelowych, że tag spowoduje wielu dostarczyć powiadomień urządzenia toohello, (po jednej dla każdego szablonu). To zachowanie jest przydatne, gdy hello tej samej logicznej wiadomość ma tooresult w wielu powiadomienia wizualne, na przykład zawierający wskaźnika i użyciu powiadomienia wyskakującego w aplikacji Sklepu Windows.
   
    Aby uzyskać więcej informacji dotyczących szablonów, zobacz [szablony](notification-hubs-templates-cross-platform-push-messages.md).
4. W pliku projektu App.xaml.cs hello, Dodaj następujące właściwości toohello hello **aplikacji** klasy:
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
    Ta właściwość jest używana toocreate i dostęp **powiadomienia** wystąpienia.
   
    W hello powyżej kodu, Zastąp hello `<hub name>` i `<connection string with listen access>` symbole zastępcze z powiadomienia Centrum nazwy i hello parametrów połączenia dla *DefaultListenSharedAccessSignature* uzyskany wcześniej.
   
   > [!NOTE]
   > Ponieważ poświadczenia, które są dystrybuowane wraz z aplikacji przez klienta nie są zazwyczaj bezpieczna, hello klucz dostępu do nasłuchiwania należy dystrybuować tylko z aplikacji klienta. Nasłuchiwanie umożliwia dostęp, nie można zmodyfikować tooregister Twojej aplikacji dla powiadomień, ale istniejące rejestracje i nie mogą być wysyłane powiadomienia. klucz pełny dostęp Hello jest używany w usłudze zabezpieczonych wewnętrznej bazy danych do wysyłania powiadomień i zmianę istniejącego rejestracji.
   > 
   > 
5. W Twojej MainPage.xaml.cs Dodaj powitania po wierszu:
   
        using Windows.UI.Popups;
6. W pliku projektu hello MainPage.xaml.cs Dodaj hello następujące metody:
   
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
   
    Ta metoda tworzy listę kategorii i używa hello **powiadomienia** klasy toostore hello listy w magazynie lokalnym hello i zarejestruj hello odpowiednie tagi w Centrum powiadomień. Zmiana kategorii rejestracji hello zostaje odtworzone w hello nowych kategorii.

Aplikacji jest teraz możliwe toostore zestaw kategorii w lokalnej pamięci masowej na powitania urządzenia i rejestruje hello Centrum powiadomień, gdy wybór kategorii hello hello zmiany wprowadzane przez użytkownika.

## <a name="register-for-notifications"></a>Rejestrowanie się w celu powiadomienia
Następujące kroki, zarejestruj się w Centrum powiadomień hello podczas uruchamiania przy użyciu hello kategorie, które były przechowywane w magazynie lokalnym.

> [!NOTE]
> Ponieważ kanał hello URI przypisał hello powiadomienia usługi WNS (Windows), można zmienić w dowolnym momencie, należy zarejestrować powiadomienia o często tooavoid powiadomień błędów. W tym przykładzie rejestruje powiadomienia o każdym uruchomieniu danej aplikacji hello. Dla aplikacji, które są uruchamiane często więcej niż raz dziennie, prawdopodobnie Jeśli możesz pominąć rejestrację toopreserve przepustowości od poprzedniej rejestracji hello upłynął krótszy niż doba.
> 
> 

1. Otwórz hello App.xaml.cs plików i aktualizacji hello **InitNotificationsAsync** hello toouse — metoda `notifications` klasy toosubscribe na podstawie kategorii.
   
        // *** Remove or comment out these lines *** 
        //var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
        //var hub = new NotificationHub("your hub name", "your listen connection string");
        //var result = await hub.RegisterNativeAsync(channel.Uri);
   
        var result = await notifications.SubscribeToCategories();
   
    Dzięki temu że każdym uruchomieniu aplikacji hello pobiera kategorie hello z magazynu lokalnego i żąda rejestracja dla tych kategorii. Witaj **InitNotificationsAsync** metody został utworzony jako część hello [Rozpoczynanie pracy z usługą Notification Hubs] [ get-started] samouczka.
2. W pliku projektu hello MainPage.xaml.cs Dodaj hello następującego kodu toohello *OnNavigatedTo* metody:
   
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
   
    ![][19]
3. Wysyłanie nowych powiadomień z zaplecza hello w jednym z hello następujące sposoby:
   
   * **Aplikacja konsoli:** start hello aplikacji konsoli.
   * **Java/PHP:** uruchamiania aplikacji lub skryptu.
     
     Powiadomienia o kategoriach hello wybrane są wyświetlane jako wyskakujące powiadomienia.
     
     ![][14]

## <a name="next-steps"></a>Następne kroki
W tym samouczku opisano sposób toobroadcast krytyczne według kategorii wiadomości. Należy rozważyć wykonanie jednej hello następujące samouczki dotyczące innych zaawansowanych scenariuszy centra powiadomień:

* [Użyj usługi Notification Hubs toobroadcast zlokalizowane najważniejszych wiadomości]
  
    Dowiedz się, jak fundamentalne wysyłania tooenable aplikacji wiadomości powitania tooexpand zlokalizowane powiadomienia.

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
