---
title: "Użycie tooenable kontekstu użytkownika aaaSending napotka w usłudze Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Śledzenie, jak przenieść użytkowników za pośrednictwem usługi, po przypisaniu do każdego z nich unikatowe, trwałe ciąg Identyfikatora w usłudze Application Insights."
services: application-insights
documentationcenter: 
author: abgreg
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: csharp
ms.topic: article
ms.date: 08/02/2017
ms.author: bwren
ms.openlocfilehash: 0e6c2348f53a3ea970060334179b0dd070925e82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
#  <a name="sending-user-context-tooenable-usage-experiences-in-azure-application-insights"></a><span data-ttu-id="5314a-103">Napotyka wysyłania użycie tooenable kontekstu użytkownika w usłudze Azure Application Insights</span><span class="sxs-lookup"><span data-stu-id="5314a-103">Sending user context tooenable usage experiences in Azure Application Insights</span></span>

## <a name="tracking-users"></a><span data-ttu-id="5314a-104">Śledzenie użytkowników</span><span class="sxs-lookup"><span data-stu-id="5314a-104">Tracking users</span></span>

<span data-ttu-id="5314a-105">Usługi Application Insights umożliwia możesz toomonitor i śledzenie użytkowników za pomocą zestawu narzędzi użycia produktu:</span><span class="sxs-lookup"><span data-stu-id="5314a-105">Application Insights enables you toomonitor and track your users through a set of product usage tools:</span></span> 
* [<span data-ttu-id="5314a-106">Użytkownicy, sesje, zdarzenia</span><span class="sxs-lookup"><span data-stu-id="5314a-106">Users, Sessions, Events</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-usage-segmentation)
* [<span data-ttu-id="5314a-107">Lejki</span><span class="sxs-lookup"><span data-stu-id="5314a-107">Funnels</span></span>](https://docs.microsoft.com/azure/application-insights/usage-funnels)
* [<span data-ttu-id="5314a-108">Przechowywanie</span><span class="sxs-lookup"><span data-stu-id="5314a-108">Retention</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-usage-retention)
* <span data-ttu-id="5314a-109">Stado</span><span class="sxs-lookup"><span data-stu-id="5314a-109">Cohorts</span></span>
* [<span data-ttu-id="5314a-110">Skoroszyty</span><span class="sxs-lookup"><span data-stu-id="5314a-110">Workbooks</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-usage-workbooks)

<span data-ttu-id="5314a-111">W kolejności tootrack, jakie użytkownik wykona wraz z upływem czasu usługi Application Insights wymaga Identyfikatora dla każdego użytkownika lub sesję.</span><span class="sxs-lookup"><span data-stu-id="5314a-111">In order tootrack what a user does over time, Application Insights needs an ID for each user or session.</span></span> <span data-ttu-id="5314a-112">Dołącz te identyfikatory każdy widok niestandardowy zdarzeń lub strony.</span><span class="sxs-lookup"><span data-stu-id="5314a-112">Include these IDs in every custom event or page view.</span></span>
- <span data-ttu-id="5314a-113">Użytkownicy, Lejki, przechowywania i stado: zawiera identyfikatora użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5314a-113">Users, Funnels, Retention, and Cohorts: Include user ID.</span></span>
- <span data-ttu-id="5314a-114">Sesje: Zawiera identyfikatora sesji.</span><span class="sxs-lookup"><span data-stu-id="5314a-114">Sessions: Include session ID.</span></span>

<span data-ttu-id="5314a-115">Jeśli aplikacja jest zintegrowana z hello [JavaScript SDK](https://docs.microsoft.com/azure/application-insights/app-insights-javascript#set-up-application-insights-for-your-web-page), automatycznie śledzenia identyfikator użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5314a-115">If your app is integrated with hello [JavaScript SDK](https://docs.microsoft.com/azure/application-insights/app-insights-javascript#set-up-application-insights-for-your-web-page), user ID is tracked automatically.</span></span>

## <a name="choosing-user-ids"></a><span data-ttu-id="5314a-116">Wybieranie nazwy użytkowników</span><span class="sxs-lookup"><span data-stu-id="5314a-116">Choosing user IDs</span></span>

<span data-ttu-id="5314a-117">Identyfikatory powinny zachowany po tootrack sesji użytkownika, zachowania użytkowników w czasie.</span><span class="sxs-lookup"><span data-stu-id="5314a-117">User IDs should persist across user sessions tootrack how users behave over time.</span></span> <span data-ttu-id="5314a-118">Istnieją różne metody utrwalanie hello identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="5314a-118">There are various approaches for persisting hello ID.</span></span>
- <span data-ttu-id="5314a-119">Definicja użytkownika, która już istnieje w usłudze.</span><span class="sxs-lookup"><span data-stu-id="5314a-119">A definition of a user that you already have in your service.</span></span>
- <span data-ttu-id="5314a-120">W przypadku usługi hello dostępu tooa przeglądarki, jego można przekazać przeglądarki hello pliku cookie z Identyfikatorem w nim.</span><span class="sxs-lookup"><span data-stu-id="5314a-120">If hello service has access tooa browser, it can pass hello browser a cookie with an ID in it.</span></span> <span data-ttu-id="5314a-121">Identyfikator Hello będzie utrzymywać tak długo, jak plik cookie hello pozostaje w przeglądarce hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5314a-121">hello ID will persist for as long as hello cookie remains in hello user's browser.</span></span>
- <span data-ttu-id="5314a-122">W razie potrzeby nowego Identyfikatora można użyć w każdej sesji, ale wyniki hello o użytkownikach będą ograniczone.</span><span class="sxs-lookup"><span data-stu-id="5314a-122">If necessary, you can use a new ID each session, but hello results about users will be limited.</span></span> <span data-ttu-id="5314a-123">Na przykład nie będzie możliwe toosee jak zachowanie użytkownika zmienia się wraz z upływem czasu.</span><span class="sxs-lookup"><span data-stu-id="5314a-123">For example, you won't be able toosee how a user's behavior changes over time.</span></span>

<span data-ttu-id="5314a-124">Identyfikator Hello powinien być identyfikatorem Guid lub innego string dostatecznie złożone tooidentify każdego użytkownika unikatowo.</span><span class="sxs-lookup"><span data-stu-id="5314a-124">hello ID should be a Guid or another string complex enough tooidentify each user uniquely.</span></span> <span data-ttu-id="5314a-125">Na przykład może to być liczba długo.</span><span class="sxs-lookup"><span data-stu-id="5314a-125">For example, it could be a long random number.</span></span>

<span data-ttu-id="5314a-126">Jeśli identyfikator hello zawiera identyfikujących informacje o użytkowniku hello, nie jest odpowiednią wartość toosend tooApplication Insights jako identyfikator użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5314a-126">If hello ID contains personally identifying information about hello user, it is not an appropriate value toosend tooApplication Insights as a user ID.</span></span> <span data-ttu-id="5314a-127">Możesz wysłać identyfikator jako [uwierzytelniony identyfikator użytkownika](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#authenticated-users), ale nie spełnia wymagań identyfikator użytkownika powitania dla scenariuszy użycia.</span><span class="sxs-lookup"><span data-stu-id="5314a-127">You can send such an ID as an [authenticated user ID](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#authenticated-users), but it does not fulfill hello user ID requirement for usage scenarios.</span></span>

## <a name="aspnet-apps-set-user-context-in-an-itelemetryinitializer"></a><span data-ttu-id="5314a-128">Aplikacje ASP.NET: Ustaw kontekst użytkownika w ITelemetryInitializer</span><span class="sxs-lookup"><span data-stu-id="5314a-128">ASP.NET Apps: Set user context in an ITelemetryInitializer</span></span>

<span data-ttu-id="5314a-129">Utwórz inicjator telemetrii w sposób opisany szczegółowo [tutaj](https://docs.microsoft.com/azure/application-insights/app-insights-api-filtering-sampling#add-properties-itelemetryinitializer)i ustaw hello Context.User.Id i hello Context.Session.Id.</span><span class="sxs-lookup"><span data-stu-id="5314a-129">Create a telemetry initializer, as described in detail [here](https://docs.microsoft.com/azure/application-insights/app-insights-api-filtering-sampling#add-properties-itelemetryinitializer), and set hello Context.User.Id and hello Context.Session.Id.</span></span>

<span data-ttu-id="5314a-130">W tym przykładzie hello użytkownika identyfikator tooan identyfikator, który wygasa po hello sesji.</span><span class="sxs-lookup"><span data-stu-id="5314a-130">This example sets hello user ID tooan identifier that expires after hello session.</span></span> <span data-ttu-id="5314a-131">Jeśli to możliwe Użyj Identyfikatora użytkownika, który będzie się powtarzał między sesjami.</span><span class="sxs-lookup"><span data-stu-id="5314a-131">If possible, use a user ID that persists across sessions.</span></span>

<span data-ttu-id="5314a-132">*C#*</span><span class="sxs-lookup"><span data-stu-id="5314a-132">*C#*</span></span>

```C#

    using System;
    using System.Web;
    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.Extensibility;

    namespace MvcWebRole.Telemetry
    {
      /*
       * Custom TelemetryInitializer that sets hello user ID.
       *
       */
      public class MyTelemetryInitializer : ITelemetryInitializer
      {
        public void Initialize(ITelemetry telemetry)
        {
            // For a full experience, track each user across sessions. For an incomplete view of user 
            // behavior within a session, store user ID on hello HttpContext Session.
            // Set hello user ID if we haven't done so yet.
            if (HttpContext.Current.Session["UserId"] == null)
            {
                HttpContext.Current.Session["UserId"] = Guid.NewGuid();
            }

            // Set hello user id on hello Application Insights telemetry item.
            telemetry.Context.User.Id = (string)HttpContext.Current.Session["UserId"];

            // Set hello session id on hello Application Insights telemetry item.
            telemetry.Context.Session.Id = HttpContext.Current.Session.SessionID;
        }
      }
    }
```

## <a name="next-steps"></a><span data-ttu-id="5314a-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5314a-133">Next steps</span></span>
- <span data-ttu-id="5314a-134">Użycie tooenable napotyka, Rozpocznij wysyłanie [zdarzeń niestandardowych](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) lub [wyświetlenia strony](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="5314a-134">tooenable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="5314a-135">Jeśli już wysyłania zdarzeń niestandardowych lub wyświetleń strony Eksploruj hello użycia narzędzia toolearn użytkowników wykorzystania usługi.</span><span class="sxs-lookup"><span data-stu-id="5314a-135">If you already send custom events or page views, explore hello Usage tools toolearn how users use your service.</span></span>
    * [<span data-ttu-id="5314a-136">Przegląd wykorzystania</span><span class="sxs-lookup"><span data-stu-id="5314a-136">Usage overview</span></span>](app-insights-usage-overview.md)
    * [<span data-ttu-id="5314a-137">Użytkownikami, sesjami i zdarzenia</span><span class="sxs-lookup"><span data-stu-id="5314a-137">Users, Sessions, and Events</span></span>](app-insights-usage-segmentation.md)
    * [<span data-ttu-id="5314a-138">Lejki</span><span class="sxs-lookup"><span data-stu-id="5314a-138">Funnels</span></span>](usage-funnels.md)
    * [<span data-ttu-id="5314a-139">Przechowywanie</span><span class="sxs-lookup"><span data-stu-id="5314a-139">Retention</span></span>](app-insights-usage-retention.md)
    * [<span data-ttu-id="5314a-140">Skoroszyty</span><span class="sxs-lookup"><span data-stu-id="5314a-140">Workbooks</span></span>](app-insights-usage-workbooks.md)
