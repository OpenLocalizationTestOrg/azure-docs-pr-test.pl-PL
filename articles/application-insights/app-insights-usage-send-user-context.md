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
#  <a name="sending-user-context-tooenable-usage-experiences-in-azure-application-insights"></a>Napotyka wysyłania użycie tooenable kontekstu użytkownika w usłudze Azure Application Insights

## <a name="tracking-users"></a>Śledzenie użytkowników

Usługi Application Insights umożliwia możesz toomonitor i śledzenie użytkowników za pomocą zestawu narzędzi użycia produktu: 
* [Użytkownicy, sesje, zdarzenia](https://docs.microsoft.com/azure/application-insights/app-insights-usage-segmentation)
* [Lejki](https://docs.microsoft.com/azure/application-insights/usage-funnels)
* [Przechowywanie](https://docs.microsoft.com/azure/application-insights/app-insights-usage-retention)
* Stado
* [Skoroszyty](https://docs.microsoft.com/azure/application-insights/app-insights-usage-workbooks)

W kolejności tootrack, jakie użytkownik wykona wraz z upływem czasu usługi Application Insights wymaga Identyfikatora dla każdego użytkownika lub sesję. Dołącz te identyfikatory każdy widok niestandardowy zdarzeń lub strony.
- Użytkownicy, Lejki, przechowywania i stado: zawiera identyfikatora użytkownika.
- Sesje: Zawiera identyfikatora sesji.

Jeśli aplikacja jest zintegrowana z hello [JavaScript SDK](https://docs.microsoft.com/azure/application-insights/app-insights-javascript#set-up-application-insights-for-your-web-page), automatycznie śledzenia identyfikator użytkownika.

## <a name="choosing-user-ids"></a>Wybieranie nazwy użytkowników

Identyfikatory powinny zachowany po tootrack sesji użytkownika, zachowania użytkowników w czasie. Istnieją różne metody utrwalanie hello identyfikatora.
- Definicja użytkownika, która już istnieje w usłudze.
- W przypadku usługi hello dostępu tooa przeglądarki, jego można przekazać przeglądarki hello pliku cookie z Identyfikatorem w nim. Identyfikator Hello będzie utrzymywać tak długo, jak plik cookie hello pozostaje w przeglądarce hello użytkownika.
- W razie potrzeby nowego Identyfikatora można użyć w każdej sesji, ale wyniki hello o użytkownikach będą ograniczone. Na przykład nie będzie możliwe toosee jak zachowanie użytkownika zmienia się wraz z upływem czasu.

Identyfikator Hello powinien być identyfikatorem Guid lub innego string dostatecznie złożone tooidentify każdego użytkownika unikatowo. Na przykład może to być liczba długo.

Jeśli identyfikator hello zawiera identyfikujących informacje o użytkowniku hello, nie jest odpowiednią wartość toosend tooApplication Insights jako identyfikator użytkownika. Możesz wysłać identyfikator jako [uwierzytelniony identyfikator użytkownika](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#authenticated-users), ale nie spełnia wymagań identyfikator użytkownika powitania dla scenariuszy użycia.

## <a name="aspnet-apps-set-user-context-in-an-itelemetryinitializer"></a>Aplikacje ASP.NET: Ustaw kontekst użytkownika w ITelemetryInitializer

Utwórz inicjator telemetrii w sposób opisany szczegółowo [tutaj](https://docs.microsoft.com/azure/application-insights/app-insights-api-filtering-sampling#add-properties-itelemetryinitializer)i ustaw hello Context.User.Id i hello Context.Session.Id.

W tym przykładzie hello użytkownika identyfikator tooan identyfikator, który wygasa po hello sesji. Jeśli to możliwe Użyj Identyfikatora użytkownika, który będzie się powtarzał między sesjami.

*C#*

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

## <a name="next-steps"></a>Następne kroki
- Użycie tooenable napotyka, Rozpocznij wysyłanie [zdarzeń niestandardowych](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) lub [wyświetlenia strony](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).
- Jeśli już wysyłania zdarzeń niestandardowych lub wyświetleń strony Eksploruj hello użycia narzędzia toolearn użytkowników wykorzystania usługi.
    * [Przegląd wykorzystania](app-insights-usage-overview.md)
    * [Użytkownikami, sesjami i zdarzenia](app-insights-usage-segmentation.md)
    * [Lejki](usage-funnels.md)
    * [Przechowywanie](app-insights-usage-retention.md)
    * [Skoroszyty](app-insights-usage-workbooks.md)
