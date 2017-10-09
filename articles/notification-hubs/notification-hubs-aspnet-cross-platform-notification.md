---
title: "aaaSend powiadomienia na różnych platformach toousers z koncentratorami powiadomień (ASP.NET)"
description: "Dowiedz się, jak toouse toosend szablony usługi Notification Hubs, pojedyncze żądanie powiadomienia niezależny od platformy, przeznaczonego dla wszystkich platform."
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
ms.openlocfilehash: f105b871b809e739dd5c05ea819ad135e842ebb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="send-cross-platform-notifications-toousers-with-notification-hubs"></a>Wyślij powiadomienia na różnych platformach toousers z usługą Notification Hubs
W samouczku poprzedniej hello [powiadomić użytkowników z usługą Notification Hubs], wiesz, jak toopush powiadomienia tooall urządzeń zarejestrowanych przez określonego użytkownika uwierzytelnionego. W tym samouczku wiele żądań były wymagane toosend platformie klienta tooeach obsługiwane powiadomień. Notification Hubs obsługuje szablonów, które pozwalają określić, jak określonego urządzenia chce tooreceive powiadomienia. Upraszcza to wysyłanie powiadomień i platform. W tym temacie przedstawiono sposób tootake zaletą toosend szablony, w ramach pojedynczego żądania powiadomienie niezależny od platformy, które dotyczy wszystkich platform. Aby uzyskać szczegółowe informacje o szablonach, zobacz [Przegląd centra powiadomień Azure][Templates].
> [!IMPORTANT]
> Projektów Windows Phone 8.1 i starsze nie są obsługiwane przy użyciu programu Visual Studio 2017 r. Aby uzyskać więcej informacji, zobacz [Obsługiwane platformy i zgodność programu Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).

> [!NOTE]
> Centra powiadomień umożliwia tooregister urządzenia wiele szablonów z hello tym samym tagiem. W takim przypadku komunikat przychodzący elementów docelowych, że tag powoduje wiele powiadomień dostarczyć toohello urządzenie, dla każdego szablonu. Ta umożliwia toodisplay możesz hello tę samą wiadomość w wielu visual powiadomień, takie jak zarówno jako wskaźnika, a wyskakujące powiadomienie w aplikacji ze Sklepu Windows.
> 
> 

Wykonaj następujące kroki wieloplatformowych toosend powiadomienia za pomocą szablonów hello:

1. W Eksploratorze rozwiązań w programie Visual Studio hello, rozwiń węzeł hello **kontrolerów** folder, a następnie otwórz hello RegisterController.cs pliku.
2. Znajdź hello blok kodu w hello **Put** hello zastąpić metodę umożliwiającą utworzenie nowej rejestracji `switch` zawartości z hello następującego kodu:
   
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
   
    Ten kod wywołuje toocreate metody specyficzne dla platformy hello rejestracji szablonu zamiast rejestracji macierzystego. Istniejące rejestracje nie należy modyfikować, ponieważ szablon rejestracji pochodzi z natywnego rejestracji.
3. W hello **powiadomienia** kontrolera, Zastąp hello **sendNotification** metody z hello następującego kodu:
   
        public async Task<HttpResponseMessage> Post()
        {
            var user = HttpContext.Current.User.Identity.Name;
            var userTag = "username:" + user;
   
            var notification = new Dictionary<string, string> { { "message", "Hello, " + user } };
            await Notifications.Instance.Hub.SendTemplateNotificationAsync(notification, userTag);
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
    Ten kod platformy tooall wysyła powiadomienie na hello sam czasu i bez konieczności toospecify natywnego ładunku. Tworzy usługi Notification Hubs i dostarcza hello urządzenia tooevery poprawne ładunku z hello podane *tag* wartość określoną w szablonach hello zarejestrowany.
4. Ponownie opublikować WebApi projektu zaplecza.
5. Ponownie uruchom aplikację klienta hello i sprawdź, czy rejestracja zakończy się pomyślnie.
6. (Opcjonalnie) Wdrażanie urządzenia drugi tooa powitania klienta aplikacji, a następnie uruchom aplikacji hello.
   
    Należy pamiętać, że na każdym urządzeniu zostanie wyświetlone powiadomienie.

## <a name="next-steps"></a>Następne kroki
Teraz, gdy została ukończona w tym samouczku, Dowiedz się więcej o usłudze Notification Hubs i szablonów w tych tematach:

* **[Użyj usługi Notification Hubs toosend fundamentalne wiadomości]** <br/>Demonstracja innego scenariusza za pomocą szablonów
* **[Omówienie usługi Azure Notification Hubs][Templates]**<br/>Temat szczegółowymi informacjami na szablony.

<!-- Anchors. -->

<!-- Images. -->




<!-- URLs. -->
[Push toousers ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Push toousers Mobile Services]: /manage/services/notification-hubs/notify-users/
[Visual Studio 2012 Express for Windows 8]: http://go.microsoft.com/fwlink/?LinkId=257546

[Użyj usługi Notification Hubs toosend fundamentalne wiadomości]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md
[Azure Notification Hubs]: http://go.microsoft.com/fwlink/p/?LinkId=314257
[powiadomić użytkowników z usługą Notification Hubs]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[Templates]: http://go.microsoft.com/fwlink/p/?LinkId=317339
[Notification Hub How toofor Windows Store]: http://msdn.microsoft.com/library/windowsazure/jj927172.aspx
