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
# <a name="send-cross-platform-notifications-to-users-with-notification-hubs"></a><span data-ttu-id="ab988-103">Wyślij powiadomienia i platform do użytkowników z usługą Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="ab988-103">Send cross-platform notifications to users with Notification Hubs</span></span>
<span data-ttu-id="ab988-104">W poprzednich instrukcji [powiadomić użytkowników z usługą Notification Hubs], przedstawiono sposób powiadomienia wypychane do wszystkich urządzeń zarejestrowanych przez określonego użytkownika uwierzytelnionego.</span><span class="sxs-lookup"><span data-stu-id="ab988-104">In the previous tutorial [Notify users with Notification Hubs], you learned how to push notifications to all devices registered by a specific authenticated user.</span></span> <span data-ttu-id="ab988-105">W tym samouczku wiele żądań były wymagane do wysyłania powiadomień do każdego obsługiwana platforma kliencka.</span><span class="sxs-lookup"><span data-stu-id="ab988-105">In that tutorial, multiple requests were required to send a notification to each supported client platform.</span></span> <span data-ttu-id="ab988-106">Notification Hubs obsługuje szablonów, które pozwalają określić, jak chce otrzymywać powiadomienia o określonym urządzeniem.</span><span class="sxs-lookup"><span data-stu-id="ab988-106">Notification Hubs supports templates, which let you specify how a specific device wants to receive notifications.</span></span> <span data-ttu-id="ab988-107">Upraszcza to wysyłanie powiadomień i platform.</span><span class="sxs-lookup"><span data-stu-id="ab988-107">This simplifies sending cross-platform notifications.</span></span> <span data-ttu-id="ab988-108">W tym temacie pokazano, jak korzystać z szablonów, aby wysłać pojedyncze żądanie powiadomienia niezależny od platformy, przeznaczonego dla wszystkich platform.</span><span class="sxs-lookup"><span data-stu-id="ab988-108">This topic demonstrates how to take advantage of templates to send, in a single request, a platform-agnostic notification that targets all platforms.</span></span> <span data-ttu-id="ab988-109">Aby uzyskać szczegółowe informacje o szablonach, zobacz [Przegląd centra powiadomień Azure][Templates].</span><span class="sxs-lookup"><span data-stu-id="ab988-109">For more detailed information about templates, see [Azure Notification Hubs Overview][Templates].</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ab988-110">Projektów Windows Phone 8.1 i starsze nie są obsługiwane przy użyciu programu Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="ab988-110">Windows Phone projects 8.1 and earlier are not supported using Visual Studio 2017.</span></span> <span data-ttu-id="ab988-111">Aby uzyskać więcej informacji, zobacz [Obsługiwane platformy i zgodność programu Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="ab988-111">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

> [!NOTE]
> <span data-ttu-id="ab988-112">Usługa Notification Hubs umożliwia urządzenia w celu rejestrowania wielu szablonów z tym samym tagiem.</span><span class="sxs-lookup"><span data-stu-id="ab988-112">Notification Hubs allows a device to register multiple templates with the same tag.</span></span> <span data-ttu-id="ab988-113">W takim przypadku komunikat przychodzący przeznaczonych dla tagu powoduje wiele powiadomień dostarczony do urządzenia, po jednej dla każdego szablonu.</span><span class="sxs-lookup"><span data-stu-id="ab988-113">In this case, an incoming message targeting that tag results in multiple notifications delivered to the device, one for each template.</span></span> <span data-ttu-id="ab988-114">Dzięki temu można wyświetlić tę samą wiadomość w wielu visual powiadomień, takie jak zarówno jako wskaźnika, a wyskakujące powiadomienie w aplikacji ze Sklepu Windows.</span><span class="sxs-lookup"><span data-stu-id="ab988-114">This enables you to display the same message in multiple visual notifications, such as both as a badge and as a toast notification in a Windows Store app.</span></span>
> 
> 

<span data-ttu-id="ab988-115">Wykonaj poniższe kroki, aby wysyłać powiadomienia i platform, za pomocą szablonów:</span><span class="sxs-lookup"><span data-stu-id="ab988-115">Complete the following steps to send cross-platform notifications using templates:</span></span>

1. <span data-ttu-id="ab988-116">W Eksploratorze rozwiązań w programie Visual Studio, rozwiń węzeł **kontrolerów** folder, a następnie otwórz plik RegisterController.cs.</span><span class="sxs-lookup"><span data-stu-id="ab988-116">In the Solution Explorer in Visual Studio, expand the **Controllers** folder, then open the RegisterController.cs file.</span></span>
2. <span data-ttu-id="ab988-117">Znajdź blok kodu w **Put** metodę, która tworzy nowy Zamień rejestracji `switch` zawartość następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="ab988-117">Locate the block of code in the **Put** method that creates a new registration replace the `switch` content with the following code:</span></span>
   
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
   
    <span data-ttu-id="ab988-118">Ten kod wywołuje metodę specyficzne dla platformy do utworzenia rejestracji szablonu zamiast rejestracji macierzystego.</span><span class="sxs-lookup"><span data-stu-id="ab988-118">This code calls the platform-specific method to create a template registration instead of a native registration.</span></span> <span data-ttu-id="ab988-119">Istniejące rejestracje nie należy modyfikować, ponieważ szablon rejestracji pochodzi z natywnego rejestracji.</span><span class="sxs-lookup"><span data-stu-id="ab988-119">Existing registrations need not be modified because template registrations derive from native registrations.</span></span>
3. <span data-ttu-id="ab988-120">W **powiadomienia** kontrolera, Zastąp **sendNotification** metodę z następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="ab988-120">In the **Notifications** controller, replace the **sendNotification** method with the following code:</span></span>
   
        public async Task<HttpResponseMessage> Post()
        {
            var user = HttpContext.Current.User.Identity.Name;
            var userTag = "username:" + user;
   
            var notification = new Dictionary<string, string> { { "message", "Hello, " + user } };
            await Notifications.Instance.Hub.SendTemplateNotificationAsync(notification, userTag);
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
    <span data-ttu-id="ab988-121">Ten kod wysyła powiadomienie do wszystkich platform, w tym samym czasie i bez konieczności określania natywnego ładunku.</span><span class="sxs-lookup"><span data-stu-id="ab988-121">This code sends a notification to all platforms at the same time and without having to specify a native payload.</span></span> <span data-ttu-id="ab988-122">Powiadomienie koncentratory kompilacje i dostarcza poprawne ładunku do wszystkich urządzeń z dostarczonych *tag* wartość określoną w szablonie w zarejestrowany.</span><span class="sxs-lookup"><span data-stu-id="ab988-122">Notification Hubs builds and delivers the correct payload to every device with the provided *tag* value, as specified in the registered templates.</span></span>
4. <span data-ttu-id="ab988-123">Ponownie opublikować WebApi projektu zaplecza.</span><span class="sxs-lookup"><span data-stu-id="ab988-123">Re-publish your WebApi back-end project.</span></span>
5. <span data-ttu-id="ab988-124">Ponownie uruchom aplikację klienta i sprawdź, czy rejestracja zakończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="ab988-124">Run the client app again and verify that registration succeeds.</span></span>
6. <span data-ttu-id="ab988-125">(Opcjonalnie) Wdrażanie aplikacji klienta do drugiego urządzenia, a następnie uruchom aplikację.</span><span class="sxs-lookup"><span data-stu-id="ab988-125">(Optional) Deploy the client app to a second device, then run the app.</span></span>
   
    <span data-ttu-id="ab988-126">Należy pamiętać, że na każdym urządzeniu zostanie wyświetlone powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="ab988-126">Note that a notification is displayed on each device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab988-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ab988-127">Next Steps</span></span>
<span data-ttu-id="ab988-128">Teraz, gdy została ukończona w tym samouczku, Dowiedz się więcej o usłudze Notification Hubs i szablonów w tych tematach:</span><span class="sxs-lookup"><span data-stu-id="ab988-128">Now that you have completed this tutorial, find out more about Notification Hubs and templates in these topics:</span></span>

* <span data-ttu-id="ab988-129">**[Wysyłanie najważniejszych wiadomości przy użyciu usługi Notification Hubs]**</span><span class="sxs-lookup"><span data-stu-id="ab988-129">**[Use Notification Hubs to send breaking news]**</span></span> <br/><span data-ttu-id="ab988-130">Demonstracja innego scenariusza za pomocą szablonów</span><span class="sxs-lookup"><span data-stu-id="ab988-130">Demonstrates another scenario for using templates</span></span>
* <span data-ttu-id="ab988-131">**[Omówienie usługi Azure Notification Hubs][Templates]**</span><span class="sxs-lookup"><span data-stu-id="ab988-131">**[Azure Notification Hubs Overview][Templates]**</span></span><br/><span data-ttu-id="ab988-132">Temat szczegółowymi informacjami na szablony.</span><span class="sxs-lookup"><span data-stu-id="ab988-132">Overview topic has more detailed information on templates.</span></span>

<!-- Anchors. -->

<!-- Images. -->




<!-- URLs. -->
[Push to users ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Push to users Mobile Services]: /manage/services/notification-hubs/notify-users/
[Visual Studio 2012 Express for Windows 8]: http://go.microsoft.com/fwlink/?LinkId=257546

<span data-ttu-id="ab988-133">[Wysyłanie najważniejszych wiadomości przy użyciu usługi Notification Hubs]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md</span><span class="sxs-lookup"><span data-stu-id="ab988-133">[Use Notification Hubs to send breaking news]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md</span></span>
[Azure Notification Hubs]: http://go.microsoft.com/fwlink/p/?LinkId=314257
<span data-ttu-id="ab988-134">[powiadomić użytkowników z usługą Notification Hubs]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md</span><span class="sxs-lookup"><span data-stu-id="ab988-134">[Notify users with Notification Hubs]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md</span></span>
[Templates]: http://go.microsoft.com/fwlink/p/?LinkId=317339
[Notification Hub How to for Windows Store]: http://msdn.microsoft.com/library/windowsazure/jj927172.aspx
