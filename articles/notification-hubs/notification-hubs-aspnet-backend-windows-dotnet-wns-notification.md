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
# <a name="azure-notification-hubs-notify-users-with-net-backend"></a>Azure Notification Hubs Powiadom użytkowników z zaplecza programu .NET
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a>Omówienie
Obsługa powiadomień wypychanych na platformie Azure umożliwia tooaccess łatwy w użyciu, multiplatform i wypychanych skalowanej infrastruktury, co znacznie upraszcza hello stosowania powiadomienia wypychane zarówno konsumenckie i korporacyjne aplikacji dla urządzeń przenośnych platform. Ten samouczek pokazuje, jak toosend usługi Azure Notification Hubs toouse wypychanie powiadomień tooa specyficzne dla aplikacji użytkownika na określonym urządzeniu. Zaplecza ASP.NET WebAPI jest używane tooauthenticate klientów. Przy użyciu hello uwierzytelniony użytkownik komputera klienckiego, a tag zostaną automatycznie dodane przez hello zaplecza toonotification rejestracji. Ten tag będzie toosend używanych przez hello zaplecza toogenerate powiadomienia dla określonego użytkownika. Aby uzyskać więcej informacji o rejestrowaniu powiadomień przy użyciu zaplecza aplikacji, zobacz temat wskazówki hello [rejestrowanie z zaplecza aplikacji](http://msdn.microsoft.com/library/dn743807.aspx). W tym samouczku, bazując na powitania Centrum powiadomień i projektu, który został utworzony w hello [Rozpoczynanie pracy z usługą Notification Hubs] samouczka.

W tym samouczku jest również hello wymagań wstępnych toohello [Secure Push] samouczka. Po wykonaniu kroków hello w tym samouczku, można przejść toohello [Secure Push] samouczku przedstawiono sposób toomodify hello kodu w tym samouczku toosend powiadomienie wypychane bezpiecznie.

## <a name="before-you-begin"></a>Przed rozpoczęciem
Traktujemy opinie naszych użytkowników bardzo poważnie. Jeśli masz trudności z wykonaniem instrukcji w tym temacie lub zalecenia dotyczące poprawy tej zawartości, prosimy o wyrażenie opinii u dołu hello hello strony.

Kod ukończyć powitalnych dla tego samouczka można znaleźć w witrynie GitHub [tutaj](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers). 

## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem tego samouczka należy wykonano już tych samouczków usług Mobile Services:

* [Rozpoczynanie pracy z usługą Notification Hubs]<br/>Tworzenie Centrum powiadomień i zarezerwowania nazwy aplikacji hello oraz zarejestrować tooreceive powiadomienia w tym samouczku. W tym samouczku założono, że zostały już wykonane następujące kroki. Jeśli nie, należy wykonać czynności hello w [wprowadzenie do korzystania z usługi Notification Hubs (w Sklepie Windows)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md); w szczególności hello sekcje [rejestrowanie aplikacji dla Sklepu Windows hello](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#register-your-app-for-the-windows-store) i [Konfiguruj Centrum powiadomień](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub). W szczególności, upewnij się, że wprowadzono hello **identyfikatora SID pakietu** i **klucz tajny klienta** wartości w portalu hello w hello **Konfiguruj** karty dla Centrum powiadomień. Ta procedura konfiguracja jest opisana w sekcji hello [Konfigurowanie Centrum powiadomień](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub). Jest to ważny krok: Jeśli hello poświadczeń w portalu hello odpowiadają wartościom określonym dla nazwy aplikacji hello wybierzesz, powiadomień wypychanych hello nie powiedzie się.

> [!NOTE]
> Jeśli używasz Mobile Apps w usłudze Azure App Service jako usługi wewnętrznej bazy danych, zobacz hello [wersją funkcji Mobile Apps](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md) tego samouczka.
> 
> 

&nbsp;

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="update-hello-code-for-hello-client-project"></a>Zaktualizuj kod hello powitania klienta projektu
W tej sekcji, zaktualizuj kod hello w projekcie hello zakończone dla hello [Rozpoczynanie pracy z usługą Notification Hubs] samouczka. Hello powinna już skojarzona z magazynem hello i skonfigurowany dla Centrum powiadomień. W tej sekcji możesz dodać kod toocall hello WebAPI zaplecza nowej i używać go do rejestracji i wysyłania powiadomień.

1. W programie Visual Studio Otwórz rozwiązanie hello hello utworzone dla hello [Rozpoczynanie pracy z usługą Notification Hubs] samouczka.
2. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **(Windows 8.1)** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet**.
3. Na powitania po lewej stronie, kliknij przycisk **Online**.
4. W hello **wyszukiwania** wpisz **klienta Http**.
5. Kliknij na liście wyników hello **bibliotek klienta HTTP Microsoft**, a następnie kliknij przycisk **zainstalować**. Ukończenie instalacji hello.
6. Po powrocie do hello NuGet **wyszukiwania** wpisz **Json.net**. Zainstaluj hello **Json.NET** pakietu i hello następnie zamknij okno Menedżera pakietów NuGet.
7. Powtórz powyższe kroki powitania dla hello **(Windows Phone 8.1)** hello tooinstall projektu **JSON.NET** pakietu NuGet dla projektu Windows Phone hello.
8. W Eksploratorze rozwiązań w hello **(Windows 8.1)** projektu, kliknij dwukrotnie **MainPage.xaml** tooopen go w edytorze programu Visual Studio hello.
9. W hello **MainPage.xaml** kod XML, Zastąp hello `<Grid>` sekcji o hello następującego kodu. Ten kod dodaje pole tekstowe nazwy użytkownika i hasła, który hello użytkownika będzie uwierzytelniania w usłudze. Dodano również pól tekstowych dla komunikatu powiadomienia hello i hello tag nazwy użytkownika, który powinny być przesyłane powiadomienia hello:
   
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
10. W Eksploratorze rozwiązań w hello **(Windows Phone 8.1)** otwarciu projektu **MainPage.xaml** i Zastąp hello Windows Phone 8.1 `<Grid>` sekcji o tym samym kodzie powyżej. Interfejs Hello powinien wyglądać podobnie toowhats pokazano poniżej.
    
    ![][13]
11. W Eksploratorze rozwiązań Otwórz hello **MainPage.xaml.cs** pliku hello **(Windows 8.1)** i **(Windows Phone 8.1)** projektów. Dodaj następujące hello `using` instrukcji u góry hello oba pliki:
    
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Windows.Networking.PushNotifications;
        using Windows.UI.Popups;
        using System.Threading.Tasks;
12. W **MainPage.xaml.cs** dla hello **(Windows 8.1)** i **(Windows Phone 8.1)** projektów, Dodaj hello następującego elementu członkowskiego toohello `MainPage` klasy. Należy się tooreplace `<Enter Your Backend Endpoint>` z hello punktu końcowego rzeczywiste wewnętrznej bazy danych uzyskany wcześniej. Na przykład `http://mybackend.azurewebsites.net`.
    
        private static string BACKEND_ENDPOINT = "<Enter Your Backend Endpoint>";
13. Dodaj kod hello poniżej klasy MainPage toohello w **MainPage.xaml.cs** dla hello **(Windows 8.1)** i **(Windows Phone 8.1)** projektów.
    
    Hello `PushClick` hello jest metoda obsługi powitania kliknij **wysyłania Push** przycisku. Wywołuje hello zaplecza tootrigger tooall powiadamiania urządzeń przy użyciu tagu nazwę użytkownika odpowiadającą hello `to_tag` parametru. wiadomości powitania powiadomienia są wysyłane jako zawartość JSON w treści żądania hello.
    
    Hello `LoginAndRegisterClick` hello jest metoda obsługi powitania kliknij **zalogować się i Zarejestruj** przycisku. Przechowuje hello basic token uwierzytelniania w magazynie lokalnym (Zauważ, że jest to dowolny token używa schematem uwierzytelniania), następnie używa `RegisterClient` tooregister dla powiadomień przy użyciu hello wewnętrznej bazy danych.

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



1. W Eksploratorze rozwiązań, w obszarze hello **Shared** projektu, otwórz hello **App.xaml.cs** pliku. Znajdowanie hello rozmowy za`InitNotificationsAsync()` w hello `OnLaunched()` obsługi zdarzeń. Komentarz lub Usuń wywołanie hello zbyt`InitNotificationsAsync()`. Obsługa przycisku Hello dodanych wcześniej zainicjuje rejestracji powiadomień.

        protected override void OnLaunched(LaunchActivatedEventArgs e)
        {
            //InitNotificationsAsync();


1. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **Shared** projektu, a następnie kliknij przycisk **Dodaj**, a następnie kliknij przycisk **klasy**. Nazwa klasy hello **RegisterClient.cs**, następnie kliknij przycisk **OK** toogenerate hello klasy.
   
   Ta klasa będzie zawijany hello REST wywołania wymagane toocontact hello zaplecza aplikacji, w kolejności tooregister dla powiadomień wypychanych. Przechowuje także lokalnie hello *registrationIds* utworzone przez hello Centrum powiadomień zgodnie z opisem w [rejestrowanie z zaplecza aplikacji](http://msdn.microsoft.com/library/dn743807.aspx). Uwaga używa tokenu autoryzacji przechowywanych w magazynie lokalnym po kliknięciu hello **zalogować się i Zarejestruj** przycisku.
2. Dodaj następujące hello `using` instrukcji u góry pliku RegisterClient.cs hello hello:
   
       using Windows.Storage;
       using System.Net;
       using System.Net.Http;
       using System.Net.Http.Headers;
       using Newtonsoft.Json;
       using System.Threading.Tasks;
       using System.Linq;
3. Dodaj następujące kodu wewnątrz hello hello `RegisterClient` definicji klasy.
   
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
4. Zapisz wszystkie zmiany.

## <a name="testing-hello-application"></a>Testowanie aplikacji hello
1. Uruchamianie aplikacji hello na Windows 8.1 i Windows Phone 8.1. Dla systemu Windows Phone 8.1 można uruchomić wystąpienie hello hello emulatora lub rzeczywistego urządzenia.
2. W wystąpieniu hello Windows 8.1 aplikacji hello, wprowadź **Username** i **hasło** jak pokazano na poniższym zrzucie ekranu hello. Powinny różnić się od hello nazwy użytkownika i hasła, która została wprowadzona Windows Phone.
3. Kliknij przycisk **zalogować się i Zarejestruj** i sprawdź okno dialogowe pokazuje, że użytkownik zalogował się. Umożliwi to również hello **wysyłania Push** przycisku.
   
    ![][14]
4. W wystąpieniu hello Windows Phone 8.1, wprowadź ciąg nazwy użytkownika w obu hello **Username** i **hasło** kliknięcie pola **logowania i rejestrowanie**.
5. Następnie w hello **Username Tag odbiorcy** wprowadź nazwę użytkownika hello zarejestrowany na Windows 8.1. Wprowadź komunikat powiadomienia, a następnie kliknij przycisk **wysyłania Push**.
   
    ![][16]
6. Witaj tylko te urządzenia, które zarejestrowanego hello pasującego tagu username wyświetlony komunikat powiadomienia hello.
   
    ![][15]

## <a name="next-steps"></a>Następne kroki
* Jeśli chcesz toosegment użytkowników na grupy zainteresowań, zobacz [toosend użyciu usługi Notification Hubs fundamentalne wiadomości].
* więcej informacji na temat toolearn toouse Notification Hubs, zobacz [wskazówki dotyczące usługi Notification Hubs].

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
