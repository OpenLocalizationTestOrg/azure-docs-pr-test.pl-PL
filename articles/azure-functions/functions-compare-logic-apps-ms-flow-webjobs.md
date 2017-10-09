---
title: "aaaChoose między przepływu, Logic Apps, funkcje i zadań Webjob | Dokumentacja firmy Microsoft"
description: "Porównaj kontrastu Witaj dla usług integracji w chmurze firmy Microsoft i zdecydować, które usługi, należy użyć."
services: functions,app-service\logic
documentationcenter: na
author: cephalin
manager: wpickett
tags: 
keywords: "Microsoft przepływu, przepływ, aplikacje logiki, funkcje platformy azure, funkcje platformy azure webjobs zadań webjob, przetwarzania, dynamiczne obliczeń niekorzystającą architektura zdarzeń"
ms.assetid: e9ccf7ad-efc4-41af-b9d3-584957b1515d
ms.service: functions
ms.devlang: multiple
ms.topic: overview
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/03/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 6becc1e389698e517924b18295dac4375542d524
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="choose-between-flow-logic-apps-functions-and-webjobs"></a>Wybieranie między przepływem, aplikacjami logiki, funkcjami a zadaniami WebJob
W tym artykule porównuje i różni się znacząco hello następujących usług w chmurze firmy Microsoft hello, który można rozwiązać wszystkie problemy integracji i automatyzacji procesów biznesowych:

* [Przepływ firmy Microsoft](https://flow.microsoft.com/)
* [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/)
* [Azure Functions](https://azure.microsoft.com/services/functions/)
* [Usługa aplikacji Azure Webjob](../app-service-web/web-sites-create-web-jobs.md)

Wszystkie te usługi są przydatne, gdy "przyklejanie" ze sobą różnych systemów. Można wszystkie definiują dane wejściowe, akcje, warunki i danych wyjściowych. Każdy z nich można uruchomić na harmonogram lub wyzwalacza. Jednak każdej usługi dodaje unikatowy zestaw wartości, i ich porównanie nie jest kwestia "usługi, która jest najlepszym hello?" oprócz jednego "usługi, która najlepiej nadaje się do tej sytuacji?" Często kombinacji tych usług jest najlepszym sposobem hello toorapidly zbudować rozwiązanie skalowalne, Pełna integracja polecanych.

<a name="flow"></a>

## <a name="flow-vs-logic-apps"></a>Przepływ programu vs. Logic Apps
Można omówimy Flow firmy Microsoft i usługi Azure Logic Apps razem ponieważ są one zarówno *pierwszej konfiguracji* usług integracji, które umożliwia łatwe toobuild procesy i przepływów pracy oraz integrują się z różnych SaaS i enterprise aplikacje. 

* Przepływ bazuje na Logic Apps
* Mają one hello tego samego projektanta przepływów pracy
* [Łączniki](../connectors/apis-list.md) czy pracy w jednym może również współpracować w hello innych

Wszelkie office worker tooperform proste integracji upoważnia przepływów (np. uzyskać SMS ważne wiadomości e-mail) bez przechodzenia przez deweloperów lub IT. Na hello drugiej strony, Logic Apps można włączyć integracji zaawansowane lub krytycznym (np. B2B procesów), których praktyki dotyczące opracowywania oprogramowania i zabezpieczeń przedsiębiorstw są wymagane. Jest typowa dla toogrow przepływu pracy firm nadgodzinach złożoności. W związku z tym można uruchomić z przepływem na początku, a następnie przekonwertować go aplikacji logiki tooa zgodnie z potrzebami.

Hello Poniższa tabela ułatwia określenie, czy przepływ lub Logic Apps jest najlepsze dla danego integracji.

|  | Ruch | Logic Apps |
| --- | --- | --- |
| Grupy odbiorców |Pracownicy biura, użytkownicy biznesowi |Informatycy i deweloperzy |
| Scenariusze |Samoobsługi |Krytycznym |
| Narzędzie do projektowania |W przeglądarce i przenośnych, aplikacja, tylko interfejsu użytkownika |W przeglądarce i [programu Visual Studio](../logic-apps/logic-apps-deploy-from-vs.md), [widok Kod](../logic-apps/logic-apps-author-definitions.md) dostępne |
| DevOps |Ad-hoc, tworzenie w środowisku produkcyjnym |Źródło kontroli, testowania, obsługi i automatyzacji oraz możliwości zarządzania w [zarządzania zasobami Azure](../logic-apps/logic-apps-arm-provision.md) |
| Środowisko pracy administratora |[https://Flow.microsoft.com](https://flow.microsoft.com) |[https://Portal.Azure.com](https://portal.azure.com) |
| Bezpieczeństwo |Standardowe rozwiązania: [suwerenności danych](https://wikipedia.org/wiki/Technological_Sovereignty), [szyfrowanie magazynowanych](https://wikipedia.org/wiki/Data_at_rest#Encryption) dla poufnych danych, itp. |Zapewnienie bezpieczeństwa systemu Azure: [zabezpieczeń Azure](https://www.microsoft.com/trustcenter/Security/AzureSecurity), [Centrum zabezpieczeń](https://azure.microsoft.com/services/security-center/), [dzienniki inspekcji](https://azure.microsoft.com/blog/azure-audit-logs-ux-refresh/)itd. |

<a name="function"></a>

## <a name="functions-vs-webjobs"></a>Funkcje programu vs. Zadania WebJob
Można omówiono usługi Azure Functions i zadań Webjob Azure App Service razem ponieważ są one zarówno *pierwszy kod* integracji usług i przeznaczone dla deweloperów. Pozwalają użytkownikom toorun skryptu lub fragmentu kodu w odpowiedzi toovarious zdarzenia, takie jak [nowego magazynu obiektów blob](functions-bindings-storage.md) lub [żądania elementu WebHook](functions-bindings-http-webhook.md). Oto ich podobieństwa: 

* Zarówno są tworzone [usłudze Azure App Service](../app-service/app-service-value-prop-what-is.md) i korzystać z funkcji takich jak [kontroli źródła](../app-service-web/app-service-continuous-deployment.md), [uwierzytelniania](../app-service/app-service-authentication-overview.md), i [monitorowania](../app-service-web/web-sites-monitor.md).
* Oba są ukierunkowane dewelopera usługi.
* Koszty pomocy technicznej standard skryptów i języków programowania.
* Mają NuGet i NPM obsługuje.

Funkcje jest hello fizycznych ewolucji zadań Webjob przyjmuje hello najlepszych rzeczy informacji o zadaniach Webjob i zwiększa się na nich. Witaj ulepszenia obejmują: 

* Prostsze deweloperów, testowania i uruchom kodu bezpośrednio w przeglądarce hello.
* Wbudowane integrację z usługami 3rd firm i Azure więcej usług, takich jak [elementów Webhook GitHub](https://developer.github.com/webhooks/creating/).
* Płatności użycia, nie konieczności toopay dla [planu usługi aplikacji](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
* Automatyczne, [dynamiczne skalowanie](functions-scale.md).
* Dla istniejących klientów usługi App Service, systemem planu usługi aplikacji nadal możliwe (tootake zaletą stopniu wykorzystania zasobów).
* Integracja z usługą Logic Apps.

Witaj w poniższej tabeli znajduje się podsumowanie hello różnic pomiędzy funkcjami i zadań Webjob:

|  | Funkcje | Zadania WebJob |
| --- | --- | --- |
| Skalowanie |Skalowanie configurationless |Skalowanie planu usługi aplikacji |
| Cennik |Płatności użycia lub w ramach planu usługi aplikacji |Część planu usługi aplikacji |
| Typ uruchomienia |wyzwalane, zaplanowane (za pomocą czasomierza wyzwalacz) |wyzwalane, ciągłego, zaplanowane |
| Wyzwalacz zdarzenia |[czasomierz](functions-bindings-timer.md), [bazy danych Azure rozwiązania Cosmos](functions-bindings-documentdb.md), [Azure Event Hubs](functions-bindings-event-hubs.md), [HTTP/WebHook (GitHub, zapas czasu)](functions-bindings-http-webhook.md), [Azure App Service Mobile Apps](functions-bindings-mobile-apps.md), [Azure Notification Hubs](functions-bindings-notification-hubs.md), [usługi Azure Service Bus](functions-bindings-service-bus.md), [magazynu Azure](functions-bindings-storage.md) |[Usługa Azure Storage](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), [usługi Azure Service Bus](../app-service-web/websites-dotnet-webjobs-sdk-service-bus.md) |
| Programowanie w przeglądarce |Obsługiwane | Nieobsługiwane |
| Okno obsługi skryptów |Eksperymentalne |Obsługiwane |
| PowerShell |Eksperymentalne |Obsługiwane |
| C# |Obsługiwane |Obsługiwane |
| F# |Obsługiwane |Nieobsługiwane |
| Bash |Eksperymentalne |Obsługiwane |
| PHP |Eksperymentalne |Obsługiwane |
| Python |Eksperymentalne |Obsługiwane |
| JavaScript |Obsługiwane |Obsługiwane |

Określa, czy funkcje toouse lub zadań Webjob ostatecznie zależy od wykonywanych już czynności z usługi aplikacji. Jeśli masz aplikację usługi aplikacji, dla której ma zostać toorun wstawki kodu, i chcesz toomanage hello je razem w tym samym środowisku DevOps, należy użyć zadania Webjob. Jeśli mają toorun wstawki kodu dla innych usług platformy Azure lub aplikacji nawet 3rd firm lub zbyt zarządzania wstawki kodu programu integration oddzielnie od aplikacji usługi aplikacji, lub jeśli chcesz toocall Twojego fragmentów kodu z aplikacji logiki, należy korzystać ze wszystkich ulepszenia Hello w funkcjach.  

<a name="together"></a>

## <a name="flow-logic-apps-and-functions-together"></a>Są zgrupowane, Logic Apps i funkcje
Jak wcześniej wspomniano usługi, która najlepiej nadaje się tooyou zależy od konkretnej sytuacji. 

* Optymalizacja biznesowa prostego następnie użyć przepływu.
* Jeśli danego scenariusza integracji jest zbyt zaawansowane dla przepływu lub potrzebujesz możliwości DevOps i compliances zabezpieczeń, użyj Logic Apps.
* Jeśli krok w danym scenariuszu integracji wymaga dużej niestandardowych transformacji lub wyspecjalizowany kod, następnie należy napisać aplikację funkcji i wyzwolić funkcji jako akcja w aplikacji logiki.

Możesz wywołać aplikacji logiki w strumieniu. Można również wywołać funkcję w aplikacji logiki i aplikacji logiki w funkcji. Integracja Hello przepływu, Logic Apps i funkcje nadal nadgodzinach tooimprove. Możesz skompilować coś w jedną usługę i użyć go w hello innych usług. W związku z tym inwestycji, wszelkie wprowadzone w tych trzech technologii jest rozważyć.

## <a name="next-steps"></a>Następne kroki
Wprowadzenie do poszczególnych usług hello tworząc Twojego pierwszego przepływu, aplikację logiki, aplikacji funkcji lub zadania WebJob. Kliknij dowolną hello następującego łącza:

* [Rozpoczynanie pracy z Flow firmy Microsoft](https://flow.microsoft.com/en-us/documentation/getting-started/)
* [Tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md)
* [Tworzenie pierwszej funkcji platformy Azure](functions-create-first-azure-function.md)
* [Wdrażanie zadań WebJob za pomocą programu Visual Studio](../app-service-web/websites-dotnet-deploy-webjobs.md)

Można też uzyskać więcej informacji na temat tych usług integracji z hello następującego łącza:

* [Korzystanie z usług Azure Functions & Azure App Service dla scenariuszy integracji przez Christopher Anderson](http://www.biztalk360.com/integrate-2016-resources/leveraging-azure-functions-azure-app-service-integration-scenarios/)
* [Uproszczona Lamanna Charlesa integracji](http://www.biztalk360.com/integrate-2016-resources/integrations-made-simple/)
* [Emisja na żywo Logic Apps](http://aka.ms/logicappslive)
* [Microsoft przepływu często zadawane pytania](https://flow.microsoft.com/documentation/frequently-asked-questions/)
* [Zasoby dokumentacji zadań Webjob Azure](../app-service-web/websites-webjobs-resources.md)

