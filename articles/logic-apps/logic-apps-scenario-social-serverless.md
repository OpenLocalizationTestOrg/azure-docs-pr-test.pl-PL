---
title: "aaaScenario — Utwórz pulpit nawigacyjny szczegółowych informacji klienta z Azure Niekorzystającą | Dokumentacja firmy Microsoft"
description: "Przykład można utworzyć klienta toomanage pulpitu nawigacyjnego opinii, dane społecznościowe i inne aplikacje logiki platformy Azure i usługi Azure Functions."
keywords: 
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: d565873c-6b1b-4057-9250-cf81a96180ae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/29/2017
ms.author: jehollan
ms.openlocfilehash: db175e895e37aa795a9c34bf4d65566bf68f8c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-real-time-customer-insights-dashboard-with-azure-logic-apps-and-azure-functions"></a>Utwórz pulpit nawigacyjny szczegółowych informacji w czasie rzeczywistym klienta z usługi Azure Logic Apps i usługi Azure Functions

Narzędzia Niekorzystającą Azure zapewniają tooquickly wydajnego kompilacji i aplikacji hosta w chmurze hello bez konieczności toothink dotyczące infrastruktury.  W tym scenariuszu firma Microsoft będzie tworzenie tootrigger pulpitu nawigacyjnego na opinie klientów, analizowanie opinii z usługi machine learning i publikowanie insights źródła, takich jak usługi Power BI lub usługi Azure Data Lake.

## <a name="overview-of-hello-scenario-and-tools-used"></a>Omówienie scenariusza hello i narzędzia

W kolejności tooimplement tego rozwiązania, firma Microsoft będzie korzystać z Witaj dwie najważniejsze składniki niekorzystającą aplikacji na platformie Azure: [usługi Azure Functions](https://azure.microsoft.com/services/functions/) i [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/).

Logic Apps jest aparatem niekorzystającą przepływu pracy w chmurze hello.  Udostępnia aranżacji między składnikami niekorzystającą, a także łączy tooover 100 usług i interfejsów API.  W tym scenariuszu utworzymy tootrigger aplikacji logiki informacji pochodzących od klientów.  Łączniki hello, które mogą pomóc w dające dodatnią reakcję opinii toocustomer między innymi Outlook.com, usługi Office 365 małp ankiety, Twitter i żądania HTTP [za pomocą formularza sieci web](https://blogs.msdn.microsoft.com/logicapps/2017/01/30/calling-a-logic-app-from-an-html-form/).  Dla przepływu pracy hello poniżej firma Microsoft będzie monitorował hasztagiem w serwisie Twitter.

Funkcje umożliwiać niekorzystającą obliczeniowych w chmurze hello.  W tym scenariuszu użyjemy usługi Azure Functions tooflag tweetów z klientów w oparciu o szereg wstępnie zdefiniowanych słów kluczowych.

Witaj całego rozwiązania może być [kompilacji w programie Visual Studio](logic-apps-deploy-from-vs.md) i [wdrożenia w ramach szablonu zasobów](logic-apps-create-deploy-template.md).  Dostępne są także przewodnik wideo dotyczący scenariusza hello [witrynie Channel 9](http://aka.ms/logicappsdemo).

## <a name="build-hello-logic-app-tootrigger-on-customer-data"></a>Tworzenie tootrigger aplikacji logiki hello na dane klienta

Po [tworzenie aplikacji logiki](logic-apps-create-a-logic-app.md) w programie Visual Studio lub hello portalu Azure:

1. Dodaj wyzwalacz **na nowych Tweetów** z serwisem Twitter
2. Konfigurowanie tootweets toolisten wyzwalacza hello na — słowo kluczowe lub hasztagiem.

   > [!NOTE]
   > Właściwość cyklu Hello na powitania wyzwalacza określają częstotliwość aplikacji logiki hello sprawdza dostępność nowych elementów na podstawie sondowania wyzwalacze

   ![Przykład wyzwalacza Twitter][1]

Ta aplikacja będzie teraz Wyzwól na wszystkich nowych tweetów.  Firma Microsoft następnie pobrania tych danych tweet i dowiedzieć się więcej hello wyrażone wskaźniki nastrojów klientów.  W tym używamy hello [kognitywnych usługę Azure](https://azure.microsoft.com/services/cognitive-services/) toodetect wskaźniki nastrojów klientów tekstu.

1. Kliknij przycisk **nowy krok**
1. Wybierz lub Wyszukaj hello **Analiza tekstu** łącznika
1. Wybierz hello **wykrywa wskaźniki nastrojów klientów** operacji
1. Jeśli zostanie wyświetlony monit, wprowadź prawidłowy klucz kognitywnych usług dla hello usługi Analiza tekstu
1. Dodaj hello **tekst Tweet** jako hello tooanalyze tekstu.

Teraz, gdy mamy hello tweet dane i informacje na powitania tweet wiele innych łączników mogą być istotne:
* Power BI — Dodawanie wierszy tooStreaming zestawu danych: Wyświetl tweetów w czasie rzeczywistym na pulpicie nawigacyjnym usługi Power BI.
* Usługa Azure Data Lake — dołączanie plików: dodatek odbiorcy danych tooan usługi Azure Data Lake dataset tooinclude zadania usługi analiza.
* SQL — Dodawanie wierszy: przechowywanie danych w bazie danych do nowszej pobierania.
* Slack — wysyłanie wiadomości: Alert kanału slack na negatywnej opinii, która wymaga działania.

Funkcja Azure mogą być również używane toodo więcej niestandardowe obliczeniowe na podstawie danych hello.

## <a name="enriching-hello-data-with-an-azure-function"></a>Wzbogacenie hello danych za pomocą funkcji platformy Azure

Zanim można utworzyć funkcji, potrzebujemy toohave aplikacji funkcji w naszym subskrypcji platformy Azure.  Szczegółowe informacje na temat tworzenia funkcji platformy Azure w portalu hello można [można znaleźć tutaj](../azure-functions/functions-create-first-azure-function-azure-portal.md)

Dla toobe funkcja wywoływana bezpośrednio z aplikacji logiki jednak wymaga toohave HTTP przyczyną powiązania.  Firma Microsoft zaleca używanie hello **HttpTrigger** szablonu.

W tym scenariuszu treści żądania hello hello funkcji platformy Azure będzie hello tweet tekstu.  Kod funkcji hello wystarczy zdefiniować logiki Jeśli hello tweet tekst zawiera słowo kluczowe lub frazę.  Funkcja Hello może znajdować się proste lub złożone, zgodnie z potrzebami dla scenariusza hello.

Na końcu hello hello funkcji wystarczy zwrócić aplikacji logiki toohello odpowiedzi z niektórych danych.  Może to być wartość logiczną proste (np. `containsKeyword`), lub obiekt złożony.

![Skonfigurowany krok funkcji platformy Azure][2]

> [!TIP]
> Podczas uzyskiwania dostępu do złożonych odpowiedzi przez funkcję aplikacji logiki, użyj akcji przeanalizować JSON hello.

Po zapisaniu hello funkcja może być dodana do aplikacji logiki hello utworzone powyżej.  W aplikacji logiki hello:

1. Kliknij przycisk tooadd **nowy krok**
1. Wybierz hello **usługi Azure Functions** łącznika
1. Wybierz toochoose istniejącej funkcji i Przeglądaj toohello utworzone — funkcja
1. Wysyłanie w hello **tekst Tweet** dla hello **treść żądania**

## <a name="running-and-monitoring-hello-solution"></a>Uruchamiania i monitorowania hello rozwiązania

Jedną z zalet hello tworzenia niekorzystającą orchestrations w aplikacjach logiki jest hello sformatowanego debugowania i możliwości monitorowania.  Wszelkie Uruchom (bieżącą lub historyczny) mogą być wyświetlane z poziomu programu Visual Studio, hello portalu Azure lub za pośrednictwem hello interfejsu API REST i zestawy SDK.

Jedna z hello najprostszy sposób tootest aplikacji logiki używa hello **Uruchom** przycisk w Projektancie hello.  Kliknięcie przycisku **Uruchom** będzie kontynuować wyzwalacza hello toopoll co 5 sekund, dopóki nie zostanie wykryte zdarzenie i przypisz widoku aktywnego w miarę postępów hello Uruchom.

Poprzednie historii wykonywania można wyświetlić w bloku omówienie hello hello portalu Azure lub za pomocą programu Visual Studio Cloud Explorer hello.

## <a name="creating-a-deployment-template-for-automated-deployments"></a>Tworzenie szablonu wdrożenia dla zautomatyzowanych wdrożeń

Po rozwiązaniu został opracowany, można przechwycić i wdrażane za pomocą tooany szablonu wdrożenia usługi Azure region platformy Azure w hello world.  Jest to przydatne w przypadku obu parametrów modyfikujących dla różnych wersji tego przepływu pracy, ale również do integracji to rozwiązanie w potoku kompilacji i wydania.  Szczegóły dotyczące tworzenia szablonu wdrożenia można znaleźć [w tym artykule](logic-apps-create-deploy-template.md).

Azure Functions można również włączona Szablon wdrożenia hello — tak hello całe rozwiązanie wszystkich zależności można zarządzać jako jednego szablonu.  Przykład szablonu wdrażania funkcji można znaleźć w hello [repozytorium szablonów Szybki Start Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/101-function-app-create-dynamic).

## <a name="next-steps"></a>Następne kroki

* [Zobacz inne przykłady i scenariusze dla usługi Azure Logic Apps](logic-apps-examples-and-scenarios.md)
* [Obejrzyj wideo wskazówki na temat tworzenia tego rozwiązania end-to-end](http://aka.ms/logicappsdemo)
* [Dowiedz się, jak toohandle i catch wyjątków w aplikacji logiki](logic-apps-exception-handling.md)

<!-- Image References -->
[1]: ./media/logic-apps-scenario-social-serverless/twitter.png
[2]: ./media/logic-apps-scenario-social-serverless/function.png