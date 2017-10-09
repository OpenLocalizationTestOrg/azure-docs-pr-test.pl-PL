---
title: aaaExamples & Typowe scenariusze - Azure Logic Apps | Dokumentacja firmy Microsoft
description: "Dowiedz się więcej o aplikacjach logiki z przykładami, scenariusze i samouczki"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: e06311bc-29eb-49df-9273-1f05bbb2395c
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/9/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 17caa8539ec6a57726b9c6c07a71fb74caa07ccb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="examples-and-common-scenarios-for-azure-logic-apps"></a>Przykłady i typowe scenariusze dotyczące usługi Azure Logic Apps

Witaj toohelp, który Dowiedz się więcej o wielu wzorców i możliwości w aplikacjach logiki platformy Azure, poniżej przedstawiono typowe przykłady i scenariusze.

## <a name="key-scenarios-for-logic-apps"></a>Najważniejsze scenariusze dla usługi logic apps

Aplikacje logiki platformy Azure zapewnia odporność aranżacji i integracji w przypadku różnych usług. Hello usługi Logic Apps jest "bez serwera", dlatego nie masz tooworry o skali lub wystąpień — wszystkie masz toodo zdefiniuj przepływu hello (wyzwalacza i akcje). platforma podstawowa Hello obsługuje skali, dostępności i wydajności. Sytuacja, których należy toocoordinate wiele akcji, szczególnie w wielu systemach, jest doskonałym przypadek użycia dla usługi Azure Logic Apps. Poniżej przedstawiono niektóre wzorców i przykłady.

## <a name="respond-tootriggers-and-extend-actions"></a>Odpowiadanie tootriggers i rozszerzanie akcje

Każda aplikacja logiki rozpoczyna się od wyzwalacza. Na przykład przepływu pracy można uruchomić z zdarzenia harmonogramu, ręczne wywołania lub zdarzenia z zewnętrznego systemu, takich jak hello wyzwalacza "po dodaniu pliku serwera tooan FTP". Aplikacje logiki platformy Azure obsługuje obecnie ponad 100 łączniki gotowe do użycia, od tooMicrosoft SAP lokalnych usług kognitywnych. Dla systemów i usług, które mogą nie mieć opublikowane łączników można rozszerzać aplikacji logiki.

* [Tworzenie niestandardowych wyzwalaczy lub akcji](../logic-apps/logic-apps-create-api-app.md)
* [Konfigurowanie akcji długotrwałe dla przebiegów przepływu pracy](../logic-apps/logic-apps-create-api-app.md)
* [Odpowiadanie na zdarzenia tooexternal i akcji z elementów webhook](../logic-apps/logic-apps-create-api-app.md)
* [Wywołaj wyzwalacz, lub zagnieżdżania przepływy pracy z żądaniami tooHTTP synchronicznej odpowiedzi](../logic-apps/logic-apps-http-endpoint.md)
* [Samouczek: Odpowiadają elementów webhook SMS tooTwilio i wysyłania odpowiedzi tekstu](https://channel9.msdn.com/Blogs/Windows-Azure/Azure-Logic-Apps-Walkthrough-Webhook-Functions-and-an-SMS-Bot)
* [Samouczek: Zasilane AI społecznościowych pulpit nawigacyjny kompilacji w minutach, z Logic Apps i usługi Power BI](http://aka.ms/logicappsdemo)

## <a name="error-handling-logging-and-control-flow-capabilities"></a>Obsługa błędów, rejestrowania i możliwości przepływu sterowania

Aplikacje logiki to rozbudowane możliwości przepływu sterowania zaawansowanych, takich jak warunki, przełączniki, pętli i zakresów. tooensure elastyczne rozwiązania, można też wdrożyć błąd i obsługa wyjątków w przepływów pracy. Dla powiadomień i dzienników diagnostycznych dla przepływu pracy stan uruchomienia Azure Logic Apps oferuje również monitorowanie i alerty.

* [Wykonaj różne akcje w instrukcjach przełącznika](../logic-apps/logic-apps-switch-case.md)
* [Proces elementów w kolekcji z pętli i partie w aplikacjach logiki i tablic](../logic-apps/logic-apps-loops-and-scopes.md)
* [Błąd tworzenie i obsługa wyjątków w przepływie pracy](../logic-apps/logic-apps-exception-handling.md)
* [Włącz monitorowanie, rejestrowanie i alerty dla istniejących aplikacji logiki](../logic-apps/logic-apps-monitor-your-logic-apps.md)
* [Włącz monitorowanie i rejestrowanie danych diagnostycznych podczas tworzenia aplikacji logiki](../logic-apps/logic-apps-monitor-your-logic-apps-oms.md)
* [Przypadek użycia: jak opieki zdrowotnej firma korzysta z obsługi dla przepływów pracy HL7 FHIR wyjątków aplikacji logiki](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)

## <a name="deploy-and-manage-logic-apps"></a>Wdrażanie i zarządzanie nimi aplikacje logiki

Pełni mogą tworzyć i wdrażać aplikacje logiki z programu Visual Studio, Visual Studio Team Services lub innymi kontroli źródła i narzędzi kompilacji automatycznych. toosupport wdrożenia dla przepływów pracy i zależne połączeń w szablonie zasobów aplikacji logiki korzystają z szablonów wdrażania zasobów platformy Azure. Narzędzia programu Visual Studio automatycznie generować tych szablonów, które można sprawdzić w formancie toosource dla wersji.

* [Tworzenie szablonu automatycznego wdrażania](../logic-apps/logic-apps-create-deploy-template.md)
* [Tworzenie i wdrażanie aplikacji logiki w programie Visual Studio](../logic-apps/logic-apps-deploy-from-vs.md)
* [Monitorowanie kondycji hello aplikacji logiki](../logic-apps/logic-apps-monitor-your-logic-apps.md)

## <a name="content-types-conversions-and-transformations-within-a-run"></a>Typy zawartości, konwersje i przekształcenia w Uruchom

Dostęp, konwersji i przekształcanie wiele typów zawartości za pomocą hello wiele funkcji w hello Azure Logic Apps [język definicji przepływu pracy](http://aka.ms/logicappsdocs). Na przykład można konwertować między ciągu, JSON i XML z hello `@json()` i `@xml()` wyrażeń przepływu pracy. Aparat Logic Apps Hello zachowuje transferu zawartości toosupport typów zawartości w sposób bezstratny między usługami.

* [Obsługi typów zawartości bez JSON](../logic-apps/logic-apps-content-type.md), takiej jak `application/xml`, `application/octet-stream`, i`multipart/formdata`
* [Sposób działania wyrażeń przepływu pracy w aplikacji logiki](../logic-apps/logic-apps-author-definitions.md)
* [Odwołanie: Język definicji przepływu pracy aplikacje logiki platformy Azure](http://aka.ms/logicappsdocs)

## <a name="other-integrations-and-capabilities"></a>Inne integracji i możliwości

Usługa Logic apps oferuje także integrację z wielu usług, takich jak usługi Azure Functions, zarządzanie interfejsami API Azure usługi aplikacji Azure i niestandardowych końcowych HTTP, na przykład REST i SOAP.

* [Tworzenie w czasie rzeczywistym społecznościowych pulpitu nawigacyjnego z Niekorzystającą Azure](../logic-apps/logic-apps-scenario-social-serverless.md)
* [Wywołanie usługi Azure Functions w aplikacjach logic apps](../logic-apps/logic-apps-azure-functions.md)
* [Scenariusz: Aplikacje logiki wyzwalacza w środowisku Azure Functions](../logic-apps/logic-apps-scenario-function-sb-trigger.md)
* [Blog: Wywołanie punktów końcowych SOAP z aplikacji logiki](https://blogs.msdn.microsoft.com/logicapps/2016/04/07/using-soap-services-with-logic-apps/)

## <a name="end-to-end-scenarios"></a>Kompleksowe scenariusze

* [Oficjalny dokument: Enterprise end-to-end wielkość zarządzanie integracją z usługami Azure, takich jak aplikacje logiki](https://aka.ms/enterprise-integration-e2e-case-management-utilities-logic-apps)

## <a name="next-steps"></a>Następne kroki

- [Obsługa błędów i wyjątków w aplikacji logiki](../logic-apps/logic-apps-exception-handling.md)
- [Tworzenie definicji przepływu pracy z języka definicji przepływu pracy hello](../logic-apps/logic-apps-author-definitions.md)
- [Przesyłanie komentarzy, pytania, opinie i sugestie dla jak możemy ulepszyć aplikacje logiki platformy Azure](https://feedback.azure.com/forums/287593-logic-apps)