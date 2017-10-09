---
title: aaaAzure powiadomienia Push Secure koncentratory
description: "Dowiedz się, jak bezpieczne toosend powiadomień wypychanych na platformie Azure. Przykłady kodu napisane w języku C# za pomocą hello interfejsu API platformy .NET."
documentationcenter: windows
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: 5aef50f4-80b3-460e-a9a7-7435001273bd
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: b6fe16c96d28d75ff698278409fb012472ba6396
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-secure-push"></a>Azure Notification Hubs bezpiecznego Push
> [!div class="op_single_selector"]
> * [Aplikacje uniwersalne systemu Windows](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [iOS](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [Android](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a>Omówienie
Obsługa powiadomień wypychanych w Microsoft Azure umożliwia tooaccess infrastruktury wypychania łatwy w użyciu, wieloplatformową skalowalnych w poziomie, który jest znacznie ułatwione hello stosowania powiadomienia wypychane zarówno konsumenckie i korporacyjne aplikacji dla urządzeń przenośnych platform.

Czasami ze względu na ograniczenia tooregulatory lub zabezpieczeń, aplikacja może być tooinclude coś w hello powiadomienie, które nie są przesyłane za pośrednictwem infrastruktury powiadomień wypychanych standardowe hello. W tym samouczku opisano, jak tooachieve hello tego samego środowiska poprzez wysłanie poufnych informacji za pośrednictwem bezpiecznego połączenia uwierzytelnionego między powitania klienta urządzenia i aplikacji hello wewnętrznej bazy danych.

Na wysokim poziomie przepływu hello jest następujący:

1. Witaj zaplecze aplikacji:
   * Magazyny bezpiecznego ładunku w wewnętrznej bazie danych.
   * Wysyła identyfikator hello tego urządzenia toohello powiadomienie (nie bezpiecznego informacje są wysyłane).
2. Aplikacja Hello na urządzeniu hello podczas odbierania powiadomień hello:
   * urządzenie Hello kontaktuje się hello zaplecza żądania hello bezpiecznego ładunku.
   * Aplikacja Hello można wyświetlić ładunku hello jako powiadomienie na urządzeniu hello.

Jest ważne toonote, że w hello poprzedzających przepływu (i w tym samouczku) przyjęto założenie, urządzenia hello po zalogowaniu użytkownika hello przechowuje token uwierzytelniania w magazynie lokalnym. Gwarantuje to całkowicie sprawnie, jak urządzenia hello mogą pobierać ładunku bezpiecznego hello powiadomienia za pomocą tego tokenu. Jeśli aplikacja nie przechowuje tokeny uwierzytelniania na urządzeniu hello lub tokeny te mogą wygasnąć, hello aplikacji urządzenia po otrzymaniu powiadomienia hello powinien być wyświetlany ogólny powiadomienie aplikacji hello toolaunch użytkownika hello monitowania. Aplikacja Hello następnie uwierzytelnia użytkownika hello i zawiera ładunek powiadomienia hello.

W tym samouczku Secure wypychania przedstawiono sposób toosend powiadomienie wypychane bezpieczny sposób. Samouczek Hello opiera się na powitania [Powiadom użytkowników](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) samouczku, dlatego należy wykonać kroki hello w tym samouczku najpierw.

> [!NOTE]
> Ten samouczek zakłada, że utworzony i skonfigurowany Centrum powiadomień, zgodnie z opisem w [wprowadzenie do korzystania z usługi Notification Hubs (w Sklepie Windows)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).
> Należy również zauważyć, że program Windows Phone 8.1 wymaga poświadczeń systemu Windows (nie Windows Phone) i czy zadania w tle nie działają na Windows Phone 8.0 lub Silverlight 8.1. Dla aplikacji ze Sklepu Windows można otrzymywać powiadomienia za pośrednictwem zadania w tle, tylko wtedy, gdy aplikacja hello jest włączona na ekranie blokady (kliknij pole wyboru hello w hello Appmanifest).
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-windows-phone-project"></a>Modyfikowanie hello projektu Windows Phone
1. W hello **NotifyUserWindowsPhone** projekt, Dodaj hello następującego kodu tooApp.xaml.cs tooregister hello wypychania zadanie wykonywane w tle. Dodaj następujące wiersz kodu na końcu hello hello hello `OnLaunched()` metody:
   
        RegisterBackgroundTask();
2. Nadal w pliku App.xaml.cs Dodaj następujące kod bezpośrednio po hello hello `OnLaunched()` metody:
   
        private async void RegisterBackgroundTask()
        {
            if (!Windows.ApplicationModel.Background.BackgroundTaskRegistration.AllTasks.Any(i => i.Value.Name == "PushBackgroundTask"))
            {
                var result = await BackgroundExecutionManager.RequestAccessAsync();
                var builder = new BackgroundTaskBuilder();
   
                builder.Name = "PushBackgroundTask";
                builder.TaskEntryPoint = typeof(PushBackgroundComponent.PushBackgroundTask).FullName;
                builder.SetTrigger(new Windows.ApplicationModel.Background.PushNotificationTrigger());
                BackgroundTaskRegistration task = builder.Register();
            }
        }
3. Dodaj następujące hello `using` instrukcji u góry hello plik App.xaml.cs hello:
   
        using Windows.Networking.PushNotifications;
        using Windows.ApplicationModel.Background;
4. Z hello **pliku** menu programu Visual Studio kliknij **Zapisz wszystko**.

## <a name="create-hello-push-background-component"></a>Utwórz hello Push składnika tła
Witaj następnym krokiem jest toocreate hello wypychania tła składnika.

1. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy węzeł najwyższego poziomu hello hello rozwiązania (**SecurePush rozwiązania** w tym przypadku), następnie kliknij przycisk **Dodaj**, następnie kliknij przycisk **nowy projekt**.
2. Rozwiń węzeł **aplikacji ze sklepu**, następnie kliknij przycisk **aplikacji Windows Phone**, następnie kliknij przycisk **składnika środowiska wykonawczego systemu Windows (Windows Phone)**. Nazwa projektu hello **PushBackgroundComponent**, a następnie kliknij przycisk **OK** toocreate hello projektu.
   
    ![][12]
3. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **PushBackgroundComponent (Windows Phone 8.1)** projektu, a następnie kliknij przycisk **Dodaj**, następnie kliknij przycisk **klasy**. Nazwa nowej klasy hello **PushBackgroundTask.cs**. Kliknij przycisk **Dodaj** toogenerate hello klasy.
4. Zastąp całą zawartość hello hello **PushBackgroundComponent** definicję przestrzeni nazw z powitania po kod, zastępując symbolu zastępczego hello `{back-end endpoint}` z punktem końcowym zaplecza hello uzyskane podczas wdrażania programu zaplecza:
   
        public sealed class Notification
            {
                public int Id { get; set; }
                public string Payload { get; set; }
                public bool Read { get; set; }
            }
   
            public sealed class PushBackgroundTask : IBackgroundTask
            {
                private string GET_URL = "{back-end endpoint}/api/notifications/";
   
                async void IBackgroundTask.Run(IBackgroundTaskInstance taskInstance)
                {
                    // Store hello content received from hello notification so it can be retrieved from hello UI.
                    RawNotification raw = (RawNotification)taskInstance.TriggerDetails;
                    var notificationId = raw.Content;
   
                    // retrieve content
                    BackgroundTaskDeferral deferral = taskInstance.GetDeferral();
                    var httpClient = new HttpClient();
                    var settings = ApplicationData.Current.LocalSettings.Values;
                    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string)settings["AuthenticationToken"]);
   
                    var notificationString = await httpClient.GetStringAsync(GET_URL + notificationId);
   
                    var notification = JsonConvert.DeserializeObject<Notification>(notificationString);
   
                    ShowToast(notification);
   
                    deferral.Complete();
                }
   
                private void ShowToast(Notification notification)
                {
                    ToastTemplateType toastTemplate = ToastTemplateType.ToastText01;
                    XmlDocument toastXml = ToastNotificationManager.GetTemplateContent(toastTemplate);
                    XmlNodeList toastTextElements = toastXml.GetElementsByTagName("text");
                    toastTextElements[0].AppendChild(toastXml.CreateTextNode(notification.Payload));
                    ToastNotification toast = new ToastNotification(toastXml);
                    ToastNotificationManager.CreateToastNotifier().Show(toast);
                }
            }
5. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **PushBackgroundComponent (Windows Phone 8.1)** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet**.
6. Na powitania po lewej stronie, kliknij przycisk **Online**.
7. W hello **wyszukiwania** wpisz **klienta Http**.
8. Kliknij na liście wyników hello **bibliotek klienta HTTP Microsoft**, a następnie kliknij przycisk **zainstalować**. Ukończenie instalacji hello.
9. Po powrocie do hello NuGet **wyszukiwania** wpisz **Json.net**. Zainstaluj hello **Json.NET** pakietu, a następnie zamknij hello okna Menedżera pakietów NuGet.
10. Dodaj następujące hello `using` instrukcji u góry hello hello **PushBackgroundTask.cs** pliku:
    
        using Windows.ApplicationModel.Background;
        using Windows.Networking.PushNotifications;
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Newtonsoft.Json;
        using Windows.UI.Notifications;
        using Windows.Data.Xml.Dom;
11. W Eksploratorze rozwiązań w hello **NotifyUserWindowsPhone (Windows Phone 8.1)** projektu, kliknij prawym przyciskiem myszy **odwołania**, następnie kliknij przycisk **Dodawanie odwołania...** . W oknie dialogowym Menedżera odwołań hello hello pole wyboru obok zbyt**PushBackgroundComponent**, a następnie kliknij przycisk **OK**.
12. W Eksploratorze rozwiązań kliknij dwukrotnie **Package.appxmanifest** w hello **NotifyUserWindowsPhone (Windows Phone 8.1)** projektu. W obszarze **powiadomienia**ustaw **wyskakujące funkcją** za**tak**.
    
    ![][3]
13. Nadal **Package.appxmanifest**, kliknij przycisk hello **deklaracje** menu u góry hello. W hello **dostępne deklaracje** listy rozwijanej, kliknij przycisk **zadania w tle**, a następnie kliknij przycisk **Dodaj**.
14. W **Package.appxmanifest**w obszarze **właściwości**, sprawdź **powiadomienie wypychane**.
15. W **Package.appxmanifest**w obszarze **ustawień aplikacji**, typ **PushBackgroundComponent.PushBackgroundTask** w hello **punktu wejścia** pole.
    
    ![][13]
16. Z hello **pliku** menu, kliknij przycisk **Zapisz wszystko**.

## <a name="run-hello-application"></a>Uruchom hello aplikacji
toorun hello aplikacji, hello następujące:

1. W programie Visual Studio, uruchom hello **AppBackend** aplikacji interfejsu API sieci Web. Zostanie wyświetlona strona sieci web ASP.NET.
2. W programie Visual Studio, uruchom hello **NotifyUserWindowsPhone (Windows Phone 8.1)** aplikacji Windows Phone. Witaj Windows Phone emulator działa i aplikacji hello jest ładowana automatycznie.
3. W hello **NotifyUserWindowsPhone** aplikacji interfejsu użytkownika, wprowadź nazwę użytkownika i hasło. Mogą to być dowolny ciąg, ale muszą one być hello tę samą wartość.
4. W hello **NotifyUserWindowsPhone** aplikacji interfejsu użytkownika, kliknij przycisk **zalogować się i Zarejestruj**. Następnie kliknij przycisk **wysyłania wypychania**.

[3]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push3.png
[12]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push12.png
[13]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push13.png
