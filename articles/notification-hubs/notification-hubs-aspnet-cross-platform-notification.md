---
title: "Wyślij powiadomienia i platform do użytkowników z koncentratorami powiadomień (ASP.NET)"
description: "Dowiedz się, jak używać usługi Notification Hubs szablonów wysłać pojedyncze żądanie powiadomienia niezależny od platformy, przeznaczonego dla wszystkich platform."
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 11d2131b-f683-47fd-a691-4cdfc696f62b
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: multiple
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: ef971fcfe68978ea9ce0810c69efbe134bb15f8a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="send-cross-platform-notifications-to-users-with-notification-hubs"></a>Wyślij powiadomienia i platform do użytkowników z usługą Notification Hubs
W poprzednich instrukcji [powiadomić użytkowników z usługą Notification Hubs], przedstawiono sposób powiadomienia wypychane do wszystkich urządzeń zarejestrowanych przez określonego użytkownika uwierzytelnionego. W tym samouczku wiele żądań były wymagane do wysyłania powiadomień do każdego obsługiwana platforma kliencka. Notification Hubs obsługuje szablonów, które pozwalają określić, jak chce otrzymywać powiadomienia o określonym urządzeniem. Upraszcza to wysyłanie powiadomień i platform. W tym temacie pokazano, jak korzystać z szablonów, aby wysłać pojedyncze żądanie powiadomienia niezależny od platformy, przeznaczonego dla wszystkich platform. Aby uzyskać szczegółowe informacje o szablonach, zobacz [Przegląd centra powiadomień Azure][Templates].
> [!IMPORTANT]
> Projektów Windows Phone 8.1 i starsze nie są obsługiwane przy użyciu programu Visual Studio 2017 r. Aby uzyskać więcej informacji, zobacz [Obsługiwane platformy i zgodność programu Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).

> [!NOTE]
> Usługa Notification Hubs umożliwia urządzenia w celu rejestrowania wielu szablonów z tym samym tagiem. W takim przypadku komunikat przychodzący przeznaczonych dla tagu powoduje wiele powiadomień dostarczony do urządzenia, po jednej dla każdego szablonu. Dzięki temu można wyświetlić tę samą wiadomość w wielu visual powiadomień, takie jak zarówno jako wskaźnika, a wyskakujące powiadomienie w aplikacji ze Sklepu Windows.
> 
> 

Wykonaj poniższe kroki, aby wysyłać powiadomienia i platform, za pomocą szablonów:

1. W Eksploratorze rozwiązań w programie Visual Studio, rozwiń węzeł **kontrolerów** folder, a następnie otwórz plik RegisterController.cs.
2. Znajdź blok kodu w **Put** metodę, która tworzy nowy Zamień rejestracji `switch` zawartość następującym kodem:
   
        switch (deviceUpdate.Platform)
        {
            case "mpns":
                var toastTemplate = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                    "<wp:Notification xmlns:wp=\"WPNotification\">" +
                       "<wp:Toast>" +
                            "<wp:Text1>$(message)</wp:Text1>" +
                       "</wp:Toast> " +
                    "</wp:Notification>";
                registration = new MpnsTemplateRegistrationDescription(deviceUpdate.Handle, toastTemplate);
                break;
            case "wns":
                toastTemplate = @"<toast><visual><binding template=""ToastText01""><text id=""1"">$(message)</text></binding></visual></toast>";
                registration = new WindowsTemplateRegistrationDescription(deviceUpdate.Handle, toastTemplate);
                break;
            case "apns":
                var alertTemplate = "{\"aps\":{\"alert\":\"$(message)\"}}";
                registration = new AppleTemplateRegistrationDescription(deviceUpdate.Handle, alertTemplate);
                break;
            case "gcm":
                var messageTemplate = "{\"data\":{\"message\":\"$(message)\"}}";
                registration = new GcmTemplateRegistrationDescription(deviceUpdate.Handle, messageTemplate);
                break;
            default:
                throw new HttpResponseException(HttpStatusCode.BadRequest);
        }
   
    Ten kod wywołuje metodę specyficzne dla platformy do utworzenia rejestracji szablonu zamiast rejestracji macierzystego. Istniejące rejestracje nie należy modyfikować, ponieważ szablon rejestracji pochodzi z natywnego rejestracji.
3. W **powiadomienia** kontrolera, Zastąp **sendNotification** metodę z następującym kodem:
   
        public async Task<HttpResponseMessage> Post()
        {
            var user = HttpContext.Current.User.Identity.Name;
            var userTag = "username:" + user;
   
            var notification = new Dictionary<string, string> { { "message", "Hello, " + user } };
            await Notifications.Instance.Hub.SendTemplateNotificationAsync(notification, userTag);
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
    Ten kod wysyła powiadomienie do wszystkich platform, w tym samym czasie i bez konieczności określania natywnego ładunku. Powiadomienie koncentratory kompilacje i dostarcza poprawne ładunku do wszystkich urządzeń z dostarczonych *tag* wartość określoną w szablonie w zarejestrowany.
4. Ponownie opublikować WebApi projektu zaplecza.
5. Ponownie uruchom aplikację klienta i sprawdź, czy rejestracja zakończy się pomyślnie.
6. (Opcjonalnie) Wdrażanie aplikacji klienta do drugiego urządzenia, a następnie uruchom aplikację.
   
    Należy pamiętać, że na każdym urządzeniu zostanie wyświetlone powiadomienie.

## <a name="next-steps"></a>Następne kroki
Teraz, gdy została ukończona w tym samouczku, Dowiedz się więcej o usłudze Notification Hubs i szablonów w tych tematach:

* **[Wysyłanie najważniejszych wiadomości przy użyciu usługi Notification Hubs]** <br/>Demonstracja innego scenariusza za pomocą szablonów
* **[Omówienie usługi Azure Notification Hubs][Templates]**<br/>Temat szczegółowymi informacjami na szablony.

<!-- Anchors. -->

<!-- Images. -->




<!-- URLs. -->
[Push to users ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Push to users Mobile Services]: /manage/services/notification-hubs/notify-users/
[Visual Studio 2012 Express for Windows 8]: http://go.microsoft.com/fwlink/?LinkId=257546

[Wysyłanie najważniejszych wiadomości przy użyciu usługi Notification Hubs]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md
[Azure Notification Hubs]: http://go.microsoft.com/fwlink/p/?LinkId=314257
[powiadomić użytkowników z usługą Notification Hubs]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[Templates]: http://go.microsoft.com/fwlink/p/?LinkId=317339
[Notification Hub How to for Windows Store]: http://msdn.microsoft.com/library/windowsazure/jj927172.aspx
