---
title: "Wybór między przepływu, Logic Apps, funkcje i zadań Webjob | Dokumentacja firmy Microsoft"
description: "Porównywanie i kontrastu chmury integracji usług firmy Microsoft i zdecydować, które usługi, należy użyć."
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
ms.openlocfilehash: da2ff16b5bdd7a0c171451930ce10427fe5bbda7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="choose-between-flow-logic-apps-functions-and-webjobs"></a>Wybieranie między przepływem, aplikacjami logiki, funkcjami a zadaniami WebJob
W tym artykule porównuje i zachowanie różni się od następujących usług w chmurze firmy Microsoft, które można rozwiązać wszystkie problemy integracji i automatyzacji procesów biznesowych:

* [Przepływ firmy Microsoft](https://flow.microsoft.com/)
* [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/)
* [Azure Functions](https://azure.microsoft.com/services/functions/)
* [Usługa aplikacji Azure Webjob](../app-service-web/web-sites-create-web-jobs.md)

Wszystkie te usługi są przydatne, gdy "przyklejanie" ze sobą różnych systemów. Można wszystkie definiują dane wejściowe, akcje, warunki i danych wyjściowych. Każdy z nich można uruchomić na harmonogram lub wyzwalacza. Jednak każdej usługi dodaje unikatowy zestaw wartości i ich porównanie nie jest kwestia "usługi, która jest najbardziej?" oprócz jednego "usługi, która najlepiej nadaje się do tej sytuacji?" Często kombinacji tych usług jest najlepszy sposób, aby szybko tworzyć rozwiązania skalowalne, Pełna integracja polecanych.

<a name="flow"></a>

## <a name="flow-vs-logic-apps"></a>Przepływ programu vs. Logic Apps
Można omówimy Flow firmy Microsoft i usługi Azure Logic Apps razem ponieważ są one zarówno *pierwszej konfiguracji* usług integracji, które ułatwia tworzenie procesów i przepływów pracy oraz integrują się z różnych SaaS i enterprise aplikacje. 

* Przepływ bazuje na Logic Apps
* Mają one z tej samej projektanta przepływów pracy
* [Łączniki](../connectors/apis-list.md) czy pracy w jednym mogą również działać w innym

Office roboczych do wykonywania prostych integracji upoważnia przepływów (np. uzyskać SMS ważne wiadomości e-mail) bez przechodzenia przez deweloperów lub IT. Z drugiej strony aplikacje logiki można włączyć integracji zaawansowane lub krytycznym (np. B2B procesów), których praktyki dotyczące opracowywania oprogramowania i zabezpieczeń przedsiębiorstw są wymagane. Jest typowa dla zwiększa się złożoność nadgodzinach biznesowego przepływu pracy. W związku z tym można uruchomić z przepływem na początku, a następnie przekonwertować go do aplikacji logiki, zgodnie z potrzebami.

Poniższa tabela ułatwia określenie, czy przepływ lub Logic Apps jest najlepsze dla danego integracji.

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
Można omówiono usługi Azure Functions i zadań Webjob Azure App Service razem ponieważ są one zarówno *pierwszy kod* integracji usług i przeznaczone dla deweloperów. Pozwalają użytkownikom na uruchamianie skryptu lub fragment kodu w odpowiedzi na różnych zdarzeń, takich jak [nowego magazynu obiektów blob](functions-bindings-storage.md) lub [żądania elementu WebHook](functions-bindings-http-webhook.md). Oto ich podobieństwa: 

* Zarówno są tworzone [usłudze Azure App Service](../app-service/app-service-value-prop-what-is.md) i korzystać z funkcji takich jak [kontroli źródła](../app-service-web/app-service-continuous-deployment.md), [uwierzytelniania](../app-service/app-service-authentication-overview.md), i [monitorowania](../app-service-web/web-sites-monitor.md).
* Oba są ukierunkowane dewelopera usługi.
* Koszty pomocy technicznej standard skryptów i języków programowania.
* Mają NuGet i NPM obsługuje.

Funkcje powstał fizycznych zadań Webjob przyjmuje najlepszych rzeczy informacji o zadaniach Webjob, i zwiększa się na nich. Ulepszenia obejmują: 

* Prostsze deweloperów, testowania i uruchom kodu bezpośrednio w przeglądarce.
* Wbudowane integrację z usługami 3rd firm i Azure więcej usług, takich jak [elementów Webhook GitHub](https://developer.github.com/webhooks/creating/).
* Płatności użycia, nie trzeba płacić za [planu usługi aplikacji](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
* Automatyczne, [dynamiczne skalowanie](functions-scale.md).
* Dla istniejących klientów usługi App Service, systemem planu usługi aplikacji nadal możliwe (wykorzystać stopniu wykorzystania zasobów).
* Integracja z usługą Logic Apps.

W poniższej tabeli przedstawiono różnice w funkcjach i zadań Webjob:

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

Czy używać funkcji lub zadań Webjob jest ostatecznie uzależniona od wykonywanych już czynności z usługi aplikacji. Jeśli masz aplikację usługi aplikacji, dla którego chcesz uruchomić wstawki kodu, i chcesz zarządzać nimi w tym samym środowisku DevOps, należy użyć zadania Webjob. Jeśli chcesz uruchomić wstawki kodu dla innych usług platformy Azure lub nawet 3rd firm aplikacji lub jeśli chcesz zarządzać wstawki kodu programu integration oddzielnie z aplikacji usługi aplikacji lub jeśli chcesz się połączyć z fragmentów kodu z aplikacji logiki, należy korzystać ze wszystkich i mprovements w funkcjach.  

<a name="together"></a>

## <a name="flow-logic-apps-and-functions-together"></a>Są zgrupowane, Logic Apps i funkcje
Jak wcześniej wspomniano usługi, która najlepiej nadaje się do Ciebie w zależności od sytuacji. 

* Optymalizacja biznesowa prostego następnie użyć przepływu.
* Jeśli danego scenariusza integracji jest zbyt zaawansowane dla przepływu lub potrzebujesz możliwości DevOps i compliances zabezpieczeń, użyj Logic Apps.
* Jeśli krok w danym scenariuszu integracji wymaga dużej niestandardowych transformacji lub wyspecjalizowany kod, następnie należy napisać aplikację funkcji i wyzwolić funkcji jako akcja w aplikacji logiki.

Możesz wywołać aplikacji logiki w strumieniu. Można również wywołać funkcję w aplikacji logiki i aplikacji logiki w funkcji. Integracja przepływu, Logic Apps i funkcje kontynuować proces ulepszania nadgodzinach. Możesz skompilować coś w jedną usługę i używać go w innych usług. W związku z tym inwestycji, wszelkie wprowadzone w tych trzech technologii jest rozważyć.

## <a name="next-steps"></a>Następne kroki
Wprowadzenie do wszystkich usług, tworząc Twojego pierwszego przepływu, aplikację logiki, aplikacji funkcji lub zadania WebJob. Kliknij dowolny z następujących łączy:

* [Rozpoczynanie pracy z Flow firmy Microsoft](https://flow.microsoft.com/en-us/documentation/getting-started/)
* [Tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md)
* [Tworzenie pierwszej funkcji platformy Azure](functions-create-first-azure-function.md)
* [Wdrażanie zadań WebJob za pomocą programu Visual Studio](../app-service-web/websites-dotnet-deploy-webjobs.md)

Można też uzyskać więcej informacji na temat tych usług integracji z następujących łączy:

* [Korzystanie z usług Azure Functions & Azure App Service dla scenariuszy integracji przez Christopher Anderson](http://www.biztalk360.com/integrate-2016-resources/leveraging-azure-functions-azure-app-service-integration-scenarios/)
* [Uproszczona Lamanna Charlesa integracji](http://www.biztalk360.com/integrate-2016-resources/integrations-made-simple/)
* [Emisja na żywo Logic Apps](http://aka.ms/logicappslive)
* [Microsoft przepływu często zadawane pytania](https://flow.microsoft.com/documentation/frequently-asked-questions/)
* [Zasoby dokumentacji zadań Webjob Azure](../app-service-web/websites-webjobs-resources.md)

