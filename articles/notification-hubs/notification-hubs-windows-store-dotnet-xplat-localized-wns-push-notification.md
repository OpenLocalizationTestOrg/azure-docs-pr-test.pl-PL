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
# <a name="use-notification-hubs-toosend-localized-breaking-news"></a>Użyj usługi Notification Hubs toosend zlokalizowane najważniejszych wiadomości
> [!div class="op_single_selector"]
> * [Sklep Windows C#](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [iOS](notification-hubs-ios-xplat-localized-apns-push-notification.md)
> 
> 

## <a name="overview"></a>Omówienie
W tym temacie opisano sposób toouse hello **szablonu** funkcji usługi Azure Notification Hubs toobroadcast fundamentalne powiadomień wiadomości, które zostały zlokalizowane według języka i urządzenia. W tym samouczku początkowo utworzony w aplikacji ze Sklepu Windows hello [toosend użyciu usługi Notification Hubs fundamentalne wiadomości]. Po zakończeniu będziesz w stanie tooregister dla kategorii, które planuje się, określ język w powiadomienia, które hello tooreceive i otrzymywać tylko powiadomienia wypychane dla kategorii hello wybrany w tym języku.

Istnieją dwie części toothis scenariusza:

* Aplikacja ze Sklepu Windows Hello umożliwia klienta urządzenia toospecify język i toodifferent toosubscribe fundamentalne kategorie nowości;
* Witaj zaplecza emituje hello powiadomień, przy użyciu hello **tag** i **szablonu** feautres usługi Azure Notification Hubs.

## <a name="prerequisites"></a>Wymagania wstępne
Należy zostały już wykonane hello [toosend użyciu usługi Notification Hubs fundamentalne wiadomości] samouczka i mieć kod hello jest dostępne, ponieważ w tym samouczku bezpośrednio oparta na kod.

Należy również Visual Studio 2012 lub nowszym.

## <a name="template-concepts"></a>Pojęcia dotyczące szablonów
W [toosend użyciu usługi Notification Hubs fundamentalne wiadomości] utworzono aplikację, która jest używana **tagi** toonotifications toosubscribe dla różnych grup dyskusyjnych kategorii.
Wiele aplikacji, jednak docelowy kilku rynkach i wymagają lokalizacji. Oznacza to, czy zawartość hello hello powiadomień, się toobe zlokalizowane i dostarczonego toohello Popraw zbiór urządzeń.
W tym temacie pokazano, jak toouse hello **szablonu** funkcji tooeasily świadczenia usługi Notification Hubs zlokalizowane powiadomienia o najważniejszych wiadomościach.

Uwaga: jednokierunkowej toosend zlokalizowane powiadomień jest toocreate wiele wersji każdego znacznika. Na przykład toosupport angielskim, francuskim i mandaryński, potrzebujemy czy trzy różne znaczniki dla wiadomości world: "world_en", "world_fr" i "world_ch". Firma Microsoft będzie zmuszony toosend zlokalizowanej wersji hello world wiadomości tooeach tych tagów. W tym temacie używamy szablony tooavoid hello mnożenie tagów i wymagania hello wielu operacji wysyłania wiadomości.

Na wysokim poziomie, szablony są toospecify sposób jak określonym urządzeniu powinno zostać odebrane powiadomienie. Szablon Hello Określa format ładunku dokładne hello odwołując tooproperties, które są częścią hello wiadomość wysłana przez zaplecze Twojej aplikacji. W tym przypadku firma Microsoft wyśle komunikat niezależny od ustawień regionalnych zawierający wszystkie obsługiwane języki:

    {
        "News_English": "...",
        "News_French": "...",
        "News_Mandarin": "..."
    }

Następnie firma Microsoft zapewnia Zarejestruj szablon, który odwołuje się właściwość poprawne toohello przez urządzenia. Na przykład aplikacji Sklepu Windows, który chce tooreceive komunikat proste wyskakujące zarejestruje dla następującego szablonu z wszystkimi tagami odpowiedniego hello:

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">$(News_English)</text>
        </binding>
      </visual>
    </toast>



Szablony są bardzo przydatna funkcja, możesz dowiedzieć się więcej w naszym [szablony](notification-hubs-templates-cross-platform-push-messages.md) artykułu. 

## <a name="hello-app-user-interface"></a>Interfejs użytkownika aplikacji Hello
Firma Microsoft będzie teraz zmodyfikować aplikacji fundamentalne wiadomości powitania, utworzonego w temacie hello [toosend użyciu usługi Notification Hubs fundamentalne wiadomości] toosend zlokalizowane najważniejszych wiadomości przy użyciu szablonów.

W aplikacji ze Sklepu Windows:

Zmień tooinclude Twojego MainPage.xaml combobox ustawień regionalnych:

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

## <a name="building-hello-windows-store-client-app"></a>Tworzenie powitania klienta w Sklepie Windows
1. W klasie powiadomień, dodać tooyour parametr ustawień regionalnych *StoreCategoriesAndSubscribe* i *SubscribeToCateories* metody.
   
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
   
    Należy pamiętać, że zamiast wywoływania hello *RegisterNativeAsync* metody nazywamy *RegisterTemplateAsync*: format określonych powiadomień, w którym hello szablonu zależy od ustawień regionalnych hello możemy rejestracji. Firma Microsoft udostępnia również nazwę dla szablonu hello ("localizedWNSTemplateExample"), ponieważ firma Microsoft może być tooregister więcej niż jednego szablonu (na przykład po jednej dla wyskakujące powiadomienia) i jeden dla kafelków i potrzebujemy tooname kolejność ich w stanie tooupdate toobe lub usuń je.
   
    Należy pamiętać, że jeśli urządzenie rejestruje wiele szablonów z hello sam tagu wiadomości przychodzącej elementów docelowych, że tag spowoduje wielu dostarczyć powiadomień urządzenia toohello, (po jednej dla każdego szablonu). To zachowanie jest przydatne, gdy hello tej samej logicznej wiadomość ma tooresult w wielu powiadomienia wizualne, na przykład zawierający wskaźnika i użyciu powiadomienia wyskakującego w aplikacji Sklepu Windows.
2. Dodaj hello następujące metody tooretrieve hello przechowywane ustawienia regionalne:
   
        public string RetrieveLocale()
        {
            var locale = (string) ApplicationData.Current.LocalSettings.Values["locale"];
            return locale != null ? locale : "English";
        }
3. W Twojej MainPage.xaml.cs aktualizacji przycisk kliknij programu obsługi pobierania hello bieżącą wartość pola kombi ustawień regionalnych hello i podając go klasy toohello wywołania toohello powiadomień, jak pokazano:
   
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
4. Na koniec w pliku App.xaml.cs, upewnij się, że tooupdate Twojego `InitNotificationsAsync` tooretrieve — metoda hello ustawień regionalnych i użyć go subskrypcji:
   
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

## <a name="send-localized-notifications-from-your-back-end"></a>Wysyłanie powiadomień zlokalizowanych z poziomu zaplecza
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
