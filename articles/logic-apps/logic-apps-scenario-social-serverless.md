---
title: "Scenariusz — Utwórz pulpit nawigacyjny szczegółowych informacji klienta z Azure Niekorzystającą | Dokumentacja firmy Microsoft"
description: "Przykład sposobu można tworzyć pulpit nawigacyjny do zarządzania opinie klientów, dane społecznościowe i inne aplikacje logiki platformy Azure i usługi Azure Functions."
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
ms.openlocfilehash: 0b6e118cb13ab8185d8eeb42bec6147155967967
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-real-time-customer-insights-dashboard-with-azure-logic-apps-and-azure-functions"></a><span data-ttu-id="74d5f-103">Utwórz pulpit nawigacyjny szczegółowych informacji w czasie rzeczywistym klienta z usługi Azure Logic Apps i usługi Azure Functions</span><span class="sxs-lookup"><span data-stu-id="74d5f-103">Create a real-time customer insights dashboard with Azure Logic Apps and Azure Functions</span></span>

<span data-ttu-id="74d5f-104">Narzędzia Niekorzystającą Azure zapewniają wydajnego szybkie tworzenie i hostowanie aplikacji w chmurze, bez konieczności pomyśleć o infrastruktury.</span><span class="sxs-lookup"><span data-stu-id="74d5f-104">Azure Serverless tools provide powerful capabilities to quickly build and host applications in the cloud, without having to think about infrastructure.</span></span>  <span data-ttu-id="74d5f-105">W tym scenariuszu zostanie utworzony pulpit nawigacyjny do wyzwolenia na opinie klientów, analizowanie opinii z uczenia maszynowego i insights Opublikuj źródła, takich jak usługi Power BI lub usługi Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="74d5f-105">In this scenario, we will create a dashboard to trigger on customer feedback, analyze feedback with machine learning, and publish insights a source like Power BI or Azure Data Lake.</span></span>

## <a name="overview-of-the-scenario-and-tools-used"></a><span data-ttu-id="74d5f-106">Omówienie scenariusza i narzędzia</span><span class="sxs-lookup"><span data-stu-id="74d5f-106">Overview of the scenario and tools used</span></span>

<span data-ttu-id="74d5f-107">Aby zaimplementować to rozwiązanie, firma Microsoft będzie korzystać dwie najważniejsze składniki niekorzystającą aplikacji na platformie Azure: [usługi Azure Functions](https://azure.microsoft.com/services/functions/) i [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span><span class="sxs-lookup"><span data-stu-id="74d5f-107">In order to implement this solution, we will leverage the two key components of serverless apps in Azure: [Azure Functions](https://azure.microsoft.com/services/functions/) and [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span></span>

<span data-ttu-id="74d5f-108">Logic Apps jest aparatem niekorzystającą przepływu pracy w chmurze.</span><span class="sxs-lookup"><span data-stu-id="74d5f-108">Logic Apps is a serverless workflow engine in the cloud.</span></span>  <span data-ttu-id="74d5f-109">Udostępnia aranżacji między składnikami niekorzystającą, a także łączy się przez ponad 100 usług i interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="74d5f-109">It provides orchestration across serverless components, and also connects to over 100 services and APIs.</span></span>  <span data-ttu-id="74d5f-110">W tym scenariuszu utworzymy aplikację logiki, aby wyzwolić na opinie klientów.</span><span class="sxs-lookup"><span data-stu-id="74d5f-110">For this scenario, we will create a logic app to trigger on feedback from customers.</span></span>  <span data-ttu-id="74d5f-111">Łączniki, które mogą pomóc w reakcji na opinie klientów między innymi Outlook.com, usługi Office 365 małp ankiety, Twitter i żądania HTTP [za pomocą formularza sieci web](https://blogs.msdn.microsoft.com/logicapps/2017/01/30/calling-a-logic-app-from-an-html-form/).</span><span class="sxs-lookup"><span data-stu-id="74d5f-111">Some of the connectors that can assist in reacting to customer feedback include Outlook.com, Office 365, Survey Monkey, Twitter, and an HTTP Request [from a web form](https://blogs.msdn.microsoft.com/logicapps/2017/01/30/calling-a-logic-app-from-an-html-form/).</span></span>  <span data-ttu-id="74d5f-112">Poniżej przepływu pracy firma Microsoft będzie monitorował hasztagiem w serwisie Twitter.</span><span class="sxs-lookup"><span data-stu-id="74d5f-112">For the workflow below, we will monitor a hashtag on Twitter.</span></span>

<span data-ttu-id="74d5f-113">Funkcje umożliwiać niekorzystającą obliczeniowych w chmurze.</span><span class="sxs-lookup"><span data-stu-id="74d5f-113">Functions provide serverless compute in the cloud.</span></span>  <span data-ttu-id="74d5f-114">W tym scenariuszu użyjemy usługi Azure Functions do flagi tweetów z klientów w oparciu o szereg wstępnie zdefiniowanych słów kluczowych.</span><span class="sxs-lookup"><span data-stu-id="74d5f-114">In this scenario, we will use Azure Functions to flag tweets from customers based on a series of pre-defined key words.</span></span>

<span data-ttu-id="74d5f-115">Całe rozwiązanie może być [kompilacji w programie Visual Studio](logic-apps-deploy-from-vs.md) i [wdrożenia w ramach szablonu zasobów](logic-apps-create-deploy-template.md).</span><span class="sxs-lookup"><span data-stu-id="74d5f-115">The entire solution can be [build in Visual Studio](logic-apps-deploy-from-vs.md) and [deployed as part of a resource template](logic-apps-create-deploy-template.md).</span></span>  <span data-ttu-id="74d5f-116">Istnieje również przewodnik wideo scenariusza [witrynie Channel 9](http://aka.ms/logicappsdemo).</span><span class="sxs-lookup"><span data-stu-id="74d5f-116">There is also video walkthrough of the scenario [on Channel 9](http://aka.ms/logicappsdemo).</span></span>

## <a name="build-the-logic-app-to-trigger-on-customer-data"></a><span data-ttu-id="74d5f-117">Tworzenie aplikacji logiki, aby wyzwolić na dane klienta</span><span class="sxs-lookup"><span data-stu-id="74d5f-117">Build the logic app to trigger on customer data</span></span>

<span data-ttu-id="74d5f-118">Po [tworzenie aplikacji logiki](logic-apps-create-a-logic-app.md) w programie Visual Studio lub w portalu Azure:</span><span class="sxs-lookup"><span data-stu-id="74d5f-118">After [creating a logic app](logic-apps-create-a-logic-app.md) in Visual Studio or the Azure portal:</span></span>

1. <span data-ttu-id="74d5f-119">Dodaj wyzwalacz **na nowych Tweetów** z serwisem Twitter</span><span class="sxs-lookup"><span data-stu-id="74d5f-119">Add a trigger for **On New Tweets** from Twitter</span></span>
2. <span data-ttu-id="74d5f-120">Skonfiguruj wyzwalacza słuchać tweetów — słowo kluczowe lub hasztagiem.</span><span class="sxs-lookup"><span data-stu-id="74d5f-120">Configure the trigger to listen to tweets on a keyword or hashtag.</span></span>

   > [!NOTE]
   > <span data-ttu-id="74d5f-121">Właściwość cyklu w wyzwalaczu określają częstotliwość aplikacji logiki sprawdza dostępność nowych elementów na podstawie sondowania wyzwalacze</span><span class="sxs-lookup"><span data-stu-id="74d5f-121">The recurrence property on the trigger will determine how frequently the logic app checks for new items on polling-based triggers</span></span>

   ![Przykład wyzwalacza Twitter][1]

<span data-ttu-id="74d5f-123">Ta aplikacja będzie teraz Wyzwól na wszystkich nowych tweetów.</span><span class="sxs-lookup"><span data-stu-id="74d5f-123">This app will now fire on all new tweets.</span></span>  <span data-ttu-id="74d5f-124">Następnie możemy pobrania tych danych tweet i dowiedzieć się więcej o wskaźniki nastrojów klientów wyrażone.</span><span class="sxs-lookup"><span data-stu-id="74d5f-124">We can then take that tweet data and understand more of the sentiment expressed.</span></span>  <span data-ttu-id="74d5f-125">W tym używamy [kognitywnych usługę Azure](https://azure.microsoft.com/services/cognitive-services/) wykryć wskaźniki nastrojów klientów tekstu.</span><span class="sxs-lookup"><span data-stu-id="74d5f-125">For this we use the [Azure Cognitive Service](https://azure.microsoft.com/services/cognitive-services/) to detect sentiment of text.</span></span>

1. <span data-ttu-id="74d5f-126">Kliknij przycisk **nowy krok**</span><span class="sxs-lookup"><span data-stu-id="74d5f-126">Click **New Step**</span></span>
1. <span data-ttu-id="74d5f-127">Wybierz lub Wyszukaj **Analiza tekstu** łącznika</span><span class="sxs-lookup"><span data-stu-id="74d5f-127">Select or search for the **Text Analytics** connector</span></span>
1. <span data-ttu-id="74d5f-128">Wybierz **wykrywa wskaźniki nastrojów klientów** operacji</span><span class="sxs-lookup"><span data-stu-id="74d5f-128">Select the **Detect Sentiment** operation</span></span>
1. <span data-ttu-id="74d5f-129">Po wyświetleniu monitu podaj prawidłowy klucz kognitywnych usług dla usługi Analiza tekstu</span><span class="sxs-lookup"><span data-stu-id="74d5f-129">If prompted, provide a valid Cognitive Services key for the Text Analytics service</span></span>
1. <span data-ttu-id="74d5f-130">Dodaj **tekst Tweet** jako tekst do analizy.</span><span class="sxs-lookup"><span data-stu-id="74d5f-130">Add the **Tweet Text** as the text to analyze.</span></span>

<span data-ttu-id="74d5f-131">Teraz, gdy mamy tweet dane i informacje na tweet wiele innych łączników mogą być istotne:</span><span class="sxs-lookup"><span data-stu-id="74d5f-131">Now that we have the tweet data, and insights on the tweet, a number of other connectors may be relevant:</span></span>
* <span data-ttu-id="74d5f-132">Power BI — Dodawanie wierszy do przesyłania strumieniowego zestawu danych: Wyświetl tweetów w czasie rzeczywistym na pulpicie nawigacyjnym usługi Power BI.</span><span class="sxs-lookup"><span data-stu-id="74d5f-132">Power BI - Add Rows to Streaming Dataset: View tweets real time on a Power BI dashboard.</span></span>
* <span data-ttu-id="74d5f-133">Azure Data Lake — Dołącz plik: Dodaj do zestawu danych usługi Azure Data Lake do uwzględnienia w zadania usługi analiza danych klienta.</span><span class="sxs-lookup"><span data-stu-id="74d5f-133">Azure Data Lake - Append file: Add customer data to an Azure Data Lake dataset to include in analytics jobs.</span></span>
* <span data-ttu-id="74d5f-134">SQL — Dodawanie wierszy: przechowywanie danych w bazie danych do nowszej pobierania.</span><span class="sxs-lookup"><span data-stu-id="74d5f-134">SQL - Add rows: Store data in a database for later retrieval.</span></span>
* <span data-ttu-id="74d5f-135">Slack — wysyłanie wiadomości: Alert kanału slack na negatywnej opinii, która wymaga działania.</span><span class="sxs-lookup"><span data-stu-id="74d5f-135">Slack - Send message: Alert a slack channel on negative feedback that requires actions.</span></span>

<span data-ttu-id="74d5f-136">Funkcję platformy Azure można również wykonać więcej niestandardowego obliczenia na podstawie danych.</span><span class="sxs-lookup"><span data-stu-id="74d5f-136">An Azure Function can also be used to do more custom compute on top of the data.</span></span>

## <a name="enriching-the-data-with-an-azure-function"></a><span data-ttu-id="74d5f-137">Wzbogacenie danych przy użyciu funkcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="74d5f-137">Enriching the data with an Azure Function</span></span>

<span data-ttu-id="74d5f-138">Zanim można utworzyć funkcji, musimy mieć aplikacji funkcji w naszym subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="74d5f-138">Before we can create a function, we need to have a function app in our Azure subscription.</span></span>  <span data-ttu-id="74d5f-139">Szczegółowe informacje na temat tworzenia funkcji platformy Azure w portalu można [można znaleźć tutaj](../azure-functions/functions-create-first-azure-function-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="74d5f-139">Details on creating an Azure Function in the portal can [be found here](../azure-functions/functions-create-first-azure-function-azure-portal.md)</span></span>

<span data-ttu-id="74d5f-140">Dla funkcję, która ma być wywoływana bezpośrednio z aplikacji logiki, musi mieć HTTP wyzwolenia powiązania.</span><span class="sxs-lookup"><span data-stu-id="74d5f-140">For a function to be called directly from a logic app, it needs to have an HTTP trigger binding.</span></span>  <span data-ttu-id="74d5f-141">Firma Microsoft zaleca używanie **HttpTrigger** szablonu.</span><span class="sxs-lookup"><span data-stu-id="74d5f-141">We recommend using the **HttpTrigger** template.</span></span>

<span data-ttu-id="74d5f-142">W tym scenariuszu treść żądania funkcji platformy Azure będzie tweet tekstu.</span><span class="sxs-lookup"><span data-stu-id="74d5f-142">In this scenario, the request body of the Azure Function would be the tweet text.</span></span>  <span data-ttu-id="74d5f-143">Kod funkcji wystarczy zdefiniować logiki Jeśli tekst tweet zawiera słowo kluczowe lub frazę.</span><span class="sxs-lookup"><span data-stu-id="74d5f-143">In the function code, simply define logic on if the tweet text contains a key word or phrase.</span></span>  <span data-ttu-id="74d5f-144">Ta funkcja może znajdować się proste lub złożone, zgodnie z potrzebami dla tego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="74d5f-144">The function itself could be kept as simple or complex as needed for the scenario.</span></span>

<span data-ttu-id="74d5f-145">Na końcu funkcję po prostu zwraca odpowiedź do aplikacji logiki z niektórych danych.</span><span class="sxs-lookup"><span data-stu-id="74d5f-145">At the end of the function, simply return a response to the logic app with some data.</span></span>  <span data-ttu-id="74d5f-146">Może to być wartość logiczną proste (np. `containsKeyword`), lub obiekt złożony.</span><span class="sxs-lookup"><span data-stu-id="74d5f-146">This could be a simple boolean value (e.g. `containsKeyword`), or a complex object.</span></span>

![Skonfigurowany krok funkcji platformy Azure][2]

> [!TIP]
> <span data-ttu-id="74d5f-148">Podczas uzyskiwania dostępu do złożonych odpowiedzi przez funkcję aplikacji logiki, użyj akcji przeanalizować JSON.</span><span class="sxs-lookup"><span data-stu-id="74d5f-148">When accessing a complex response from a function in a logic app, use the Parse JSON action.</span></span>

<span data-ttu-id="74d5f-149">Po zapisaniu funkcji, można dodać do aplikacji logiki utworzone powyżej.</span><span class="sxs-lookup"><span data-stu-id="74d5f-149">Once the function is saved, it can be added into the logic app created above.</span></span>  <span data-ttu-id="74d5f-150">W aplikacji logiki:</span><span class="sxs-lookup"><span data-stu-id="74d5f-150">In the logic app:</span></span>

1. <span data-ttu-id="74d5f-151">Kliknij, aby dodać **nowy krok**</span><span class="sxs-lookup"><span data-stu-id="74d5f-151">Click to add a **New Step**</span></span>
1. <span data-ttu-id="74d5f-152">Wybierz **usługi Azure Functions** łącznika</span><span class="sxs-lookup"><span data-stu-id="74d5f-152">Select the **Azure Functions** connector</span></span>
1. <span data-ttu-id="74d5f-153">Zaznacz, aby wybrać istniejące funkcję i przejdź do funkcji utworzone</span><span class="sxs-lookup"><span data-stu-id="74d5f-153">Select to choose an existing function, and browse to the function created</span></span>
1. <span data-ttu-id="74d5f-154">Wysyłanie w **Tweetować tekst** dla **treść żądania**</span><span class="sxs-lookup"><span data-stu-id="74d5f-154">Send in the **Tweet Text** for the **Request Body**</span></span>

## <a name="running-and-monitoring-the-solution"></a><span data-ttu-id="74d5f-155">Uruchamiania i monitorowania rozwiązania</span><span class="sxs-lookup"><span data-stu-id="74d5f-155">Running and monitoring the solution</span></span>

<span data-ttu-id="74d5f-156">Jedną z zalet tworzenia niekorzystającą orchestrations w aplikacjach logiki jest sformatowany debugowania i możliwości monitorowania.</span><span class="sxs-lookup"><span data-stu-id="74d5f-156">One of the benefits of authoring serverless orchestrations in Logic Apps is the rich debug and monitoring capabilities.</span></span>  <span data-ttu-id="74d5f-157">Wszelkie Uruchom (bieżącą lub historyczny) mogą być wyświetlane z poziomu programu Visual Studio, portalu Azure lub za pośrednictwem interfejsu API REST i zestawy SDK.</span><span class="sxs-lookup"><span data-stu-id="74d5f-157">Any run (current or historic) can be viewed from within Visual Studio, the Azure portal, or via the REST API and SDKs.</span></span>

<span data-ttu-id="74d5f-158">Jednym ze sposobów najłatwiejsza do testowania aplikacji logiki przy użyciu **Uruchom** przycisk w projektancie.</span><span class="sxs-lookup"><span data-stu-id="74d5f-158">One of the easiest ways to test a logic app is using the **Run** button in the designer.</span></span>  <span data-ttu-id="74d5f-159">Kliknięcie przycisku **Uruchom** będzie sondować wyzwalacza co 5 sekund, dopóki nie zostanie wykryte zdarzenie i nadaj widoku aktywnego w trakcie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="74d5f-159">Clicking **Run** will continue to poll the trigger every 5 seconds until an event is detected, and give a live view as the run progresses.</span></span>

<span data-ttu-id="74d5f-160">Poprzednie historii wykonywania można wyświetlić w bloku omówienie w portalu Azure lub za pomocą programu Visual Studio Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="74d5f-160">Previous run histories can be viewed on the Overview blade in the Azure portal, or using the Visual Studio Cloud Explorer.</span></span>

## <a name="creating-a-deployment-template-for-automated-deployments"></a><span data-ttu-id="74d5f-161">Tworzenie szablonu wdrożenia dla zautomatyzowanych wdrożeń</span><span class="sxs-lookup"><span data-stu-id="74d5f-161">Creating a deployment template for automated deployments</span></span>

<span data-ttu-id="74d5f-162">Po rozwiązaniu został opracowany, można przechwycić i wdrażane za pomocą szablonu wdrożenia usługi Azure do dowolnego regionu Azure na świecie.</span><span class="sxs-lookup"><span data-stu-id="74d5f-162">Once a solution has been developed, it can be captured and deployed via an Azure deployment template to any Azure region in the world.</span></span>  <span data-ttu-id="74d5f-163">Jest to przydatne w przypadku obu parametrów modyfikujących dla różnych wersji tego przepływu pracy, ale również do integracji to rozwiązanie w potoku kompilacji i wydania.</span><span class="sxs-lookup"><span data-stu-id="74d5f-163">This is useful for both modifying parameters for different versions of this workflow, but also for integrating this solution in a build and release pipeline.</span></span>  <span data-ttu-id="74d5f-164">Szczegóły dotyczące tworzenia szablonu wdrożenia można znaleźć [w tym artykule](logic-apps-create-deploy-template.md).</span><span class="sxs-lookup"><span data-stu-id="74d5f-164">Details on creating a deployment template can be found [in this article](logic-apps-create-deploy-template.md).</span></span>

<span data-ttu-id="74d5f-165">Środowisko Azure Functions można również włączona Szablon wdrożenia — tak całego rozwiązania z wszystkie zależności mogą być zarządzane jako jednego szablonu.</span><span class="sxs-lookup"><span data-stu-id="74d5f-165">Azure Functions can also be incorporated in the deployment template - so the entire solution with all dependencies can be managed as a single template.</span></span>  <span data-ttu-id="74d5f-166">Przykład wdrożenia szablonu funkcji można znaleźć w [repozytorium szablonów Szybki Start Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/101-function-app-create-dynamic).</span><span class="sxs-lookup"><span data-stu-id="74d5f-166">An example of a function deployment template can be found in the [Azure quickstart template repository](https://github.com/Azure/azure-quickstart-templates/tree/master/101-function-app-create-dynamic).</span></span>

## <a name="next-steps"></a><span data-ttu-id="74d5f-167">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="74d5f-167">Next steps</span></span>

* [<span data-ttu-id="74d5f-168">Zobacz inne przykłady i scenariusze dla usługi Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="74d5f-168">See other examples and scenarios for Azure Logic Apps</span></span>](logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="74d5f-169">Obejrzyj wideo wskazówki na temat tworzenia tego rozwiązania end-to-end</span><span class="sxs-lookup"><span data-stu-id="74d5f-169">Watch a video walkthrough on creating this solution end-to-end</span></span>](http://aka.ms/logicappsdemo)
* [<span data-ttu-id="74d5f-170">Informacje o sposobie obsługi i przechwytywanie wyjątków w aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="74d5f-170">Learn how to handle and catch exceptions within a logic app</span></span>](logic-apps-exception-handling.md)

<!-- Image References -->
[1]: ./media/logic-apps-scenario-social-serverless/twitter.png
[2]: ./media/logic-apps-scenario-social-serverless/function.png