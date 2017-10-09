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
# <a name="send-cross-platform-notifications-toousers-with-notification-hubs"></a><span data-ttu-id="5385a-103">Wyślij powiadomienia na różnych platformach toousers z usługą Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="5385a-103">Send cross-platform notifications toousers with Notification Hubs</span></span>
<span data-ttu-id="5385a-104">W samouczku poprzedniej hello [powiadomić użytkowników z usługą Notification Hubs], wiesz, jak toopush powiadomienia tooall urządzeń zarejestrowanych przez określonego użytkownika uwierzytelnionego.</span><span class="sxs-lookup"><span data-stu-id="5385a-104">In hello previous tutorial [Notify users with Notification Hubs], you learned how toopush notifications tooall devices registered by a specific authenticated user.</span></span> <span data-ttu-id="5385a-105">W tym samouczku wiele żądań były wymagane toosend platformie klienta tooeach obsługiwane powiadomień.</span><span class="sxs-lookup"><span data-stu-id="5385a-105">In that tutorial, multiple requests were required toosend a notification tooeach supported client platform.</span></span> <span data-ttu-id="5385a-106">Notification Hubs obsługuje szablonów, które pozwalają określić, jak określonego urządzenia chce tooreceive powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="5385a-106">Notification Hubs supports templates, which let you specify how a specific device wants tooreceive notifications.</span></span> <span data-ttu-id="5385a-107">Upraszcza to wysyłanie powiadomień i platform.</span><span class="sxs-lookup"><span data-stu-id="5385a-107">This simplifies sending cross-platform notifications.</span></span> <span data-ttu-id="5385a-108">W tym temacie przedstawiono sposób tootake zaletą toosend szablony, w ramach pojedynczego żądania powiadomienie niezależny od platformy, które dotyczy wszystkich platform.</span><span class="sxs-lookup"><span data-stu-id="5385a-108">This topic demonstrates how tootake advantage of templates toosend, in a single request, a platform-agnostic notification that targets all platforms.</span></span> <span data-ttu-id="5385a-109">Aby uzyskać szczegółowe informacje o szablonach, zobacz [Przegląd centra powiadomień Azure][Templates].</span><span class="sxs-lookup"><span data-stu-id="5385a-109">For more detailed information about templates, see [Azure Notification Hubs Overview][Templates].</span></span>
> [!IMPORTANT]
> <span data-ttu-id="5385a-110">Projektów Windows Phone 8.1 i starsze nie są obsługiwane przy użyciu programu Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="5385a-110">Windows Phone projects 8.1 and earlier are not supported using Visual Studio 2017.</span></span> <span data-ttu-id="5385a-111">Aby uzyskać więcej informacji, zobacz [Obsługiwane platformy i zgodność programu Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="5385a-111">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

> [!NOTE]
> <span data-ttu-id="5385a-112">Centra powiadomień umożliwia tooregister urządzenia wiele szablonów z hello tym samym tagiem.</span><span class="sxs-lookup"><span data-stu-id="5385a-112">Notification Hubs allows a device tooregister multiple templates with hello same tag.</span></span> <span data-ttu-id="5385a-113">W takim przypadku komunikat przychodzący elementów docelowych, że tag powoduje wiele powiadomień dostarczyć toohello urządzenie, dla każdego szablonu.</span><span class="sxs-lookup"><span data-stu-id="5385a-113">In this case, an incoming message targeting that tag results in multiple notifications delivered toohello device, one for each template.</span></span> <span data-ttu-id="5385a-114">Ta umożliwia toodisplay możesz hello tę samą wiadomość w wielu visual powiadomień, takie jak zarówno jako wskaźnika, a wyskakujące powiadomienie w aplikacji ze Sklepu Windows.</span><span class="sxs-lookup"><span data-stu-id="5385a-114">This enables you toodisplay hello same message in multiple visual notifications, such as both as a badge and as a toast notification in a Windows Store app.</span></span>
> 
> 

<span data-ttu-id="5385a-115">Wykonaj następujące kroki wieloplatformowych toosend powiadomienia za pomocą szablonów hello:</span><span class="sxs-lookup"><span data-stu-id="5385a-115">Complete hello following steps toosend cross-platform notifications using templates:</span></span>

1. <span data-ttu-id="5385a-116">W Eksploratorze rozwiązań w programie Visual Studio hello, rozwiń węzeł hello **kontrolerów** folder, a następnie otwórz hello RegisterController.cs pliku.</span><span class="sxs-lookup"><span data-stu-id="5385a-116">In hello Solution Explorer in Visual Studio, expand hello **Controllers** folder, then open hello RegisterController.cs file.</span></span>
2. <span data-ttu-id="5385a-117">Znajdź hello blok kodu w hello **Put** hello zastąpić metodę umożliwiającą utworzenie nowej rejestracji `switch` zawartości z hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="5385a-117">Locate hello block of code in hello **Put** method that creates a new registration replace hello `switch` content with hello following code:</span></span>
   
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
   
    <span data-ttu-id="5385a-118">Ten kod wywołuje toocreate metody specyficzne dla platformy hello rejestracji szablonu zamiast rejestracji macierzystego.</span><span class="sxs-lookup"><span data-stu-id="5385a-118">This code calls hello platform-specific method toocreate a template registration instead of a native registration.</span></span> <span data-ttu-id="5385a-119">Istniejące rejestracje nie należy modyfikować, ponieważ szablon rejestracji pochodzi z natywnego rejestracji.</span><span class="sxs-lookup"><span data-stu-id="5385a-119">Existing registrations need not be modified because template registrations derive from native registrations.</span></span>
3. <span data-ttu-id="5385a-120">W hello **powiadomienia** kontrolera, Zastąp hello **sendNotification** metody z hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="5385a-120">In hello **Notifications** controller, replace hello **sendNotification** method with hello following code:</span></span>
   
        public async Task<HttpResponseMessage> Post()
        {
            var user = HttpContext.Current.User.Identity.Name;
            var userTag = "username:" + user;
   
            var notification = new Dictionary<string, string> { { "message", "Hello, " + user } };
            await Notifications.Instance.Hub.SendTemplateNotificationAsync(notification, userTag);
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
    <span data-ttu-id="5385a-121">Ten kod platformy tooall wysyła powiadomienie na hello sam czasu i bez konieczności toospecify natywnego ładunku.</span><span class="sxs-lookup"><span data-stu-id="5385a-121">This code sends a notification tooall platforms at hello same time and without having toospecify a native payload.</span></span> <span data-ttu-id="5385a-122">Tworzy usługi Notification Hubs i dostarcza hello urządzenia tooevery poprawne ładunku z hello podane *tag* wartość określoną w szablonach hello zarejestrowany.</span><span class="sxs-lookup"><span data-stu-id="5385a-122">Notification Hubs builds and delivers hello correct payload tooevery device with hello provided *tag* value, as specified in hello registered templates.</span></span>
4. <span data-ttu-id="5385a-123">Ponownie opublikować WebApi projektu zaplecza.</span><span class="sxs-lookup"><span data-stu-id="5385a-123">Re-publish your WebApi back-end project.</span></span>
5. <span data-ttu-id="5385a-124">Ponownie uruchom aplikację klienta hello i sprawdź, czy rejestracja zakończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="5385a-124">Run hello client app again and verify that registration succeeds.</span></span>
6. <span data-ttu-id="5385a-125">(Opcjonalnie) Wdrażanie urządzenia drugi tooa powitania klienta aplikacji, a następnie uruchom aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="5385a-125">(Optional) Deploy hello client app tooa second device, then run hello app.</span></span>
   
    <span data-ttu-id="5385a-126">Należy pamiętać, że na każdym urządzeniu zostanie wyświetlone powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="5385a-126">Note that a notification is displayed on each device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5385a-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5385a-127">Next Steps</span></span>
<span data-ttu-id="5385a-128">Teraz, gdy została ukończona w tym samouczku, Dowiedz się więcej o usłudze Notification Hubs i szablonów w tych tematach:</span><span class="sxs-lookup"><span data-stu-id="5385a-128">Now that you have completed this tutorial, find out more about Notification Hubs and templates in these topics:</span></span>

* <span data-ttu-id="5385a-129">**[Użyj usługi Notification Hubs toosend fundamentalne wiadomości]**</span><span class="sxs-lookup"><span data-stu-id="5385a-129">**[Use Notification Hubs toosend breaking news]**</span></span> <br/><span data-ttu-id="5385a-130">Demonstracja innego scenariusza za pomocą szablonów</span><span class="sxs-lookup"><span data-stu-id="5385a-130">Demonstrates another scenario for using templates</span></span>
* <span data-ttu-id="5385a-131">**[Omówienie usługi Azure Notification Hubs][Templates]**</span><span class="sxs-lookup"><span data-stu-id="5385a-131">**[Azure Notification Hubs Overview][Templates]**</span></span><br/><span data-ttu-id="5385a-132">Temat szczegółowymi informacjami na szablony.</span><span class="sxs-lookup"><span data-stu-id="5385a-132">Overview topic has more detailed information on templates.</span></span>

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
