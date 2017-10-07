---
title: "Omówienie funkcji aaaAzure | Dokumentacja firmy Microsoft"
description: "Zrozumienie sposobu obciążeń asynchronicznych toooptimize usługi Azure Functions toouse w minutach."
services: functions
documentationcenter: na
author: mattchenderson
manager: erikre
editor: 
tags: 
keywords: "usługa Azure Functions, funkcje, przetwarzanie zdarzeń, elementy webhook, obliczanie dynamiczne, architektura bez serwera"
ms.assetid: 01d6ca9f-ca3f-44fa-b0b9-7ffee115acd4
ms.service: functions
ms.devlang: multiple
ms.topic: overview
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 02/27/2017
ms.author: glenga
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 668f9055a007fee662a4c7ec774d3c0a1d847800
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="an-introduction-tooazure-functions"></a>Funkcje tooAzure wprowadzenie  
Azure Functions to rozwiązanie umożliwiające łatwe uruchamianie małych fragmentów kodu lub "funkcji" w chmurze hello. Można napisać tylko kod hello potrzebne hello problemu, nie martwiąc się o całą aplikację lub hello toorun infrastruktury go. Dzięki usłudze Functions programowanie może być jeszcze wydajniejsze i można korzystać z wybranego języka programowania, takiego jak C#, F#, Node.js, Python lub PHP. Płać tylko za czas działania kodu hello i zaufać Azure tooscale, zgodnie z potrzebami. Usługa Azure Functions pozwala tworzyć na platformie Microsoft Azure aplikacje niewymagające użycia serwera.

W tym temacie przedstawiono ogólne omówienie usługi Azure Functions. Jeśli mają prawo toojump i wprowadzenie do usługi Azure Functions, Rozpocznij od [tworzenie pierwszej funkcji platformy Azure](functions-create-first-azure-function.md). Jeśli chcesz uzyskać więcej informacji technicznych dotyczących funkcji, zobacz hello [dokumentacja dla deweloperów](functions-reference.md).

## <a name="features"></a>Funkcje
Oto główne funkcje usługi Azure Functions:

* **Wybór języka** — tworzenie funkcji przy użyciu języka C#, F#, Node.js, Python, PHP, batch, bash lub użycie dowolnych plików wykonywalnych.
* **Model cenowy płatności za użycie** — płać tylko w przypadku hello czas działania kodu. Zobacz planowanie opcję hello hosting zużycie hello [sekcji dotyczącej cen](#pricing).  
* **Korzystaj z własnych zależności** — środowisko Functions obsługuje rozwiązania NuGet i NPM, dzięki czemu można używać ulubionych bibliotek.  
* **Zintegrowane zabezpieczenia** — ochrona funkcji wyzwalanych przez protokół HTTP za pośrednictwem dostawców uwierzytelniania OAuth, takich jak Azure Active Directory, Facebook, Google, Twitter i konto Microsoft.  
* **Uproszczona integracja** — łatwe korzystanie z usług platformy Azure i ofert oprogramowania jako usługi (SaaS). Zobacz hello [sekcji dotyczącej integracji](#integrations) kilka przykładów.  
* **Elastyczne programowanie** — kodowanie funkcji bezpośrednio w portalu hello lub konfigurowanie ciągłej integracji i wdrażanie kodu za pomocą usług GitHub, Visual Studio Team Services i innych [obsługiwanych narzędzi deweloperskich](../app-service-web/web-sites-deploy.md#deploy-using-an-ide).  
* **Open source** — środowisko uruchomieniowe Functions hello jest open source i [dostępne w witrynie GitHub](https://github.com/azure/azure-webjobs-sdk-script).  

## <a name="what-can-i-do-with-functions"></a>Co można zrobić w środowisku Functions?
Azure Functions to doskonałe rozwiązanie do przetwarzania danych, integrowania systemów, pracy z hello internet z rzeczy (IoT) oraz tworzenia prostych interfejsów API i mikrousług. Należy wziąć pod uwagę funkcje dla zadań, takich jak obraz lub kolejność przetwarzania, plików obsługi lub wszelkie zadania, które mają toorun zgodnie z harmonogramem. 

Środowisko usługi Functions zawiera tooget szablony, pracę z kluczowymi scenariuszami, w tym następujące hello:

* **BlobTrigger** -procesu usługi Azure Storage obiektów blob, gdy są one dodawane toocontainers. Tej funkcji można użyć do zmiany rozmiaru obrazu.
* **EventHubTrigger** -odpowiadać tooevents dostarczyć tooan Azure Event Hub. Opcja szczególnie przydatna podczas instrumentacji aplikacji, przetwarzania środowiska użytkownika lub przepływu pracy oraz pracy ze scenariuszami Internetu rzeczy (IoT).
* **Ogólny element webhook** — przetwarzanie żądań HTTP elementu webhook z dowolnej usługi obsługującej takie elementy.
* **Element webhook GitHub** -tooevents odpowiedź, który występuje w repozytoriach usługi GitHub. Przykład można znaleźć w temacie [Create a webhook or API function](functions-create-a-web-hook-or-api-function.md) (Tworzenie funkcji interfejsu API lub elementu webhook).
* **HTTPTrigger** — wyzwalanie wykonywania kodu hello za pomocą żądania HTTP.
* **QueueTrigger** -odpowiadać toomessages pojawiających się w kolejce usługi Azure Storage. Na przykład zobacz [Tworzenie funkcji platformy Azure, który wiąże tooan usługi Azure](functions-create-an-azure-connected-function.md).
* **ServiceBusQueueTrigger** -Połącz z tooother kod usług Azure lub lokalnie usług przez nasłuchiwania toomessage kolejek. 
* **ServiceBusTopicTrigger** -Połącz z tooother kod usług Azure lub lokalnej usługi Subskrybuj tootopics. 
* **TimerTrigger** — wykonywanie oczyszczania lub innych zadań wsadowych zgodnie ze wstępnie zdefiniowanym harmonogramem. Przykład można znaleźć w temacie [Tworzenie funkcji przetwarzania zdarzeń](functions-create-an-event-processing-function.md).

Azure Functions obsługuje *wyzwalaczy*, która metodami toostart wykonywania kodu, i *powiązania*, które są toosimplify sposoby kodowanie danych wejściowych i wyjściowych. Aby uzyskać szczegółowy opis wyzwalaczy hello i powiązań oferowanych w środowisku Azure functions, zobacz [dokumentacja dla deweloperów usługi Azure Functions wyzwalaczy i powiązań](functions-triggers-bindings.md).

## <a name="integrations"></a>Integracje
Usługę Azure Functions można integrować z różnymi usługami platformy Azure i firm zewnętrznych. Te usługi umożliwiają wyzwalanie funkcji i uruchamianie wykonywania. Mogą również służyć jako dane wejściowe i wyjściowe dla kodu. Witaj następujące usługi integracji są obsługiwane przez usługi Azure Functions. 

* Azure Cosmos DB
* Azure Event Hubs 
* Azure Mobile Apps (tabele)
* Azure Notification Hubs
* Azure Service Bus (kolejki i tematy)
* Azure Storage (obiekty blob, kolejki i tabele) 
* GitHub (elementy webhook)
* Lokalne (za pomocą usługi Service Bus)
* Twilio (wiadomości SMS)

## <a name="pricing"></a>Ile kosztuje usługa Azure Functions?
Usługa Azure Functions oferuje dwa rodzaje planów cenowych, wybierz polecenie hello, który najlepiej zaspokaja Twoje potrzeby: 

* **Użycie planu** — po uruchomieniu funkcji, platforma Azure udostępnia wszystkie niezbędne zasoby obliczeniowe hello. Nie masz tooworry dotyczących zarządzania zasobami i płacisz tylko za czas działania kodu hello. 
* **Plan usługi App Service** — uruchamianie funkcji tak samo jak aplikacji sieci Web, mobilnych i interfejsu API. Jeśli korzystasz już z usługi aplikacji — dla innych aplikacji, można uruchomić funkcji na powitania sam plan bez ponoszenia dodatkowych kosztów. 

Szczegółowe informacje są dostępne na powitania [stronie cennika usługi Functions](https://azure.microsoft.com/pricing/details/functions/). Aby uzyskać więcej informacji na temat skalowania funkcji, zobacz [jak tooscale usługi Azure Functions](functions-scale.md).

## <a name="next-steps"></a>Następne kroki
* [Tworzenie pierwszej funkcji platformy Azure](functions-create-first-azure-function.md)  
  Od razu i utworzyć swoją pierwszą funkcję przy użyciu usługi Azure Functions hello — Szybki Start. 
* [Dokumentacja usługi Azure Functions dla deweloperów](functions-reference.md)  
  Zawiera więcej informacji technicznych dotyczących środowiska uruchomieniowego usługi Azure Functions hello i odwołanie dotycząca kodowania funkcji oraz definiowania wyzwalaczy i powiązań.
* [Testowanie usługi Azure Functions](functions-test-a-function.md)  
  Opis różnych narzędzi i technik testowania funkcji.
* [Jak tooscale usługi Azure Functions](functions-scale.md)  
  Omówienie planów usług dostępnych w środowisku Azure Functions: plan hostingu zużycie hello i jak toochoose hello właściwego planu. 
* [Dowiedz się więcej o usłudze Azure App Service](../app-service/app-service-value-prop-what-is.md)  
  Środowisko Azure Functions używa platformy Azure App Service hello do podstawowych funkcji, takich jak wdrożenia, zmienne środowiskowe i Diagnostyka. 

