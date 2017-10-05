---
title: "Niestandardowy kod dla usługi Azure Logic Apps w środowisku Azure Functions | Dokumentacja firmy Microsoft"
description: "Tworzenie i uruchamianie niestandardowych kodów dla usługi Azure Logic Apps w środowisku Azure Functions"
services: logic-apps,functions
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 9fab1050-cfbc-4a8b-b1b3-5531bee92856
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 18442c87b049200fac5ed41cc7034ba7a848b8d3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="add-and-run-custom-code-for-logic-apps-through-azure-functions"></a><span data-ttu-id="50e48-103">Dodaj i uruchomienia niestandardowego kodu dla usługi logic apps za pomocą usługi Azure Functions</span><span class="sxs-lookup"><span data-stu-id="50e48-103">Add and run custom code for logic apps through Azure Functions</span></span>

<span data-ttu-id="50e48-104">Aby uruchomić niestandardowe fragmenty kodu języka C# lub node.js w aplikacji logiki, można utworzyć funkcji niestandardowych za pomocą usługi Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="50e48-104">To run custom snippets of C# or node.js in logic apps, you can create custom functions through Azure Functions.</span></span> 
<span data-ttu-id="50e48-105">[Środowisko Azure Functions](../azure-functions/functions-overview.md) oferuje wolny od serwera przetwarzania danych w Microsoft Azure i są użyteczne do wykonywania tych zadań:</span><span class="sxs-lookup"><span data-stu-id="50e48-105">[Azure Functions](../azure-functions/functions-overview.md) offers server-free computing in Microsoft Azure and are useful for performing these tasks:</span></span>

* <span data-ttu-id="50e48-106">Zaawansowane, formatowanie lub obliczeniowych pól w aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="50e48-106">Advanced formatting or compute of fields in logic apps</span></span>
* <span data-ttu-id="50e48-107">Wykonywanie obliczeń w przepływie pracy.</span><span class="sxs-lookup"><span data-stu-id="50e48-107">Perform calculations in a workflow.</span></span>
* <span data-ttu-id="50e48-108">Rozszerzanie funkcjonalności aplikacji logiki z funkcjami, które są obsługiwane w języku C# lub node.js</span><span class="sxs-lookup"><span data-stu-id="50e48-108">Extend the logic app functionality with functions that are supported in C# or node.js</span></span>

## <a name="create-custom-functions-for-your-logic-apps"></a><span data-ttu-id="50e48-109">Tworzenie funkcji niestandardowych dla aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="50e48-109">Create custom functions for your logic apps</span></span>

<span data-ttu-id="50e48-110">Zaleca się utworzenie funkcji w portalu Azure Functions z **ogólny element Webhook - węzła** lub **ogólny element Webhook - C#** szablonów.</span><span class="sxs-lookup"><span data-stu-id="50e48-110">We recommend that you create a function in the Azure Functions portal, from the **Generic Webhook - Node** or **Generic Webhook - C#** templates.</span></span> <span data-ttu-id="50e48-111">Wynik tworzy wypełniana automatycznie szablon, który akceptuje `application/json` z aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="50e48-111">The result creates an auto-populated a template that accepts `application/json` from a logic app.</span></span> <span data-ttu-id="50e48-112">Funkcje, które utworzono z tych szablonów są wykrywane automatycznie i są wyświetlane w Projektancie aplikacji logiki w obszarze **usługi Azure Functions w moim regionie.**</span><span class="sxs-lookup"><span data-stu-id="50e48-112">Functions that you create from these templates are automatically detected and appear in the Logic App Designer under **Azure Functions in my region.**</span></span>

<span data-ttu-id="50e48-113">W portalu Azure na **integracji** okienku dla funkcji szablon powinien pokazują, że **tryb** ustawioną **Webhook** i **typu elementu Webhook**ma ustawioną wartość **ogólnego JSON**.</span><span class="sxs-lookup"><span data-stu-id="50e48-113">In the Azure portal, on the **Integrate** pane for your function, your template should show that **Mode** set to **Webhook** and **Webhook type** is set to **Generic JSON**.</span></span> 

<span data-ttu-id="50e48-114">Funkcje elementu Webhook zaakceptować żądania i przekaż go do metody za pomocą `data` zmiennej.</span><span class="sxs-lookup"><span data-stu-id="50e48-114">Webhook functions accept a request and pass it into the method via a `data` variable.</span></span> <span data-ttu-id="50e48-115">Uzyskać dostęp do właściwości z ładunku, używając zapisu kropkowego jak `data.function-name`.</span><span class="sxs-lookup"><span data-stu-id="50e48-115">You can access the properties of your payload by using dot notation like `data.function-name`.</span></span> <span data-ttu-id="50e48-116">Na przykład prostych funkcji JavaScript, który konwertuje wartości daty i godziny do ciągu daty wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="50e48-116">For example, a simple JavaScript function that converts a DateTime value into a date string looks like the following example:</span></span>

```
function start(req, res){
    var data = req.body;
    res = {
        body: data.date.ToDateString();
    }
}
```

## <a name="call-azure-functions-from-logic-apps"></a><span data-ttu-id="50e48-117">Wywołanie usługi Azure Functions w aplikacjach logic apps</span><span class="sxs-lookup"><span data-stu-id="50e48-117">Call Azure Functions from logic apps</span></span>

<span data-ttu-id="50e48-118">Aby wyświetlić kontenery w ramach subskrypcji i wybierz funkcję, która ma zostać wywołana w Projektancie aplikacji logiki, kliknij przycisk **akcje** menu, a następnie wybierz z **usługi Azure Functions w moim regionie**.</span><span class="sxs-lookup"><span data-stu-id="50e48-118">To list the containers in your subscription and select the function that you want to call, in Logic App Designer, click the **Actions** menu, and select from **Azure Functions in my Region**.</span></span>

<span data-ttu-id="50e48-119">Po wybraniu funkcji, należy określić obiekt wprowadzony ładunek.</span><span class="sxs-lookup"><span data-stu-id="50e48-119">After you select the function, you are asked to specify an input payload object.</span></span> <span data-ttu-id="50e48-120">Ten obiekt jest komunikatów wysyła do funkcji i musi być obiektem JSON aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="50e48-120">This object is the message that the logic app sends to the function and must be a JSON object.</span></span> <span data-ttu-id="50e48-121">Na przykład, jeśli mają być przekazywane **ostatniej modyfikacji** daty z wyzwalacza Salesforce ładunku funkcja wygląda w tym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="50e48-121">For example, if you want to pass in the **Last Modified** date from a Salesforce trigger, the function payload might look like this example:</span></span>

![Data ostatniej modyfikacji][1]

## <a name="trigger-logic-apps-from-a-function"></a><span data-ttu-id="50e48-123">Aplikacje logiki wyzwalacza w funkcji</span><span class="sxs-lookup"><span data-stu-id="50e48-123">Trigger logic apps from a function</span></span>

<span data-ttu-id="50e48-124">Możesz wyzwolić aplikacji logiki z wewnątrz funkcji.</span><span class="sxs-lookup"><span data-stu-id="50e48-124">You can trigger a logic app from inside a function.</span></span> <span data-ttu-id="50e48-125">Zobacz [logiki aplikacji jako punkty końcowe można wywołać](logic-apps-http-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="50e48-125">See [Logic apps as callable endpoints](logic-apps-http-endpoint.md).</span></span> <span data-ttu-id="50e48-126">Tworzenie aplikacji logiki, która zawiera wyzwalacz ręcznego, a następnie z wewnątrz funkcji, generowanie HTTP POST do ręcznego wyzwalacza, adres URL z ładunku, który ma wysłany do aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="50e48-126">Create a logic app that has a manual trigger, then from inside your function, generate an HTTP POST to the manual trigger URL with the payload that you want sent to the logic app.</span></span>

### <a name="create-a-function-from-logic-app-designer"></a><span data-ttu-id="50e48-127">Tworzenie funkcji przy użyciu projektanta aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="50e48-127">Create a function from Logic App Designer</span></span>

<span data-ttu-id="50e48-128">Można również utworzyć funkcję webhook node.js przy użyciu projektanta.</span><span class="sxs-lookup"><span data-stu-id="50e48-128">You can also create a node.js webhook function from the designer.</span></span> <span data-ttu-id="50e48-129">Najpierw wybierz **usługi Azure Functions w moim regionie** , a następnie wybierz kontener dla funkcji.</span><span class="sxs-lookup"><span data-stu-id="50e48-129">First, select **Azure Functions in my Region,** and then choose a container for your function.</span></span> <span data-ttu-id="50e48-130">Jeśli jeszcze nie masz kontenera, należy utworzyć jeden z [portalu Azure Functions](https://functions.azure.com/signin).</span><span class="sxs-lookup"><span data-stu-id="50e48-130">If you don't yet have a container, you need to create one from the [Azure Functions portal](https://functions.azure.com/signin).</span></span> <span data-ttu-id="50e48-131">Następnie wybierz **Utwórz nowy**.</span><span class="sxs-lookup"><span data-stu-id="50e48-131">Then select **Create New**.</span></span>  

<span data-ttu-id="50e48-132">Aby wygenerować szablon na podstawie danych, który ma zostać obliczeniowe, należy określić obiekt kontekstu, który chcesz przekazać do funkcji.</span><span class="sxs-lookup"><span data-stu-id="50e48-132">To generate a template based on the data that you want to compute, specify the context object that you plan to pass into a function.</span></span> <span data-ttu-id="50e48-133">Ten obiekt musi być obiektem JSON.</span><span class="sxs-lookup"><span data-stu-id="50e48-133">This object must be a JSON object.</span></span> <span data-ttu-id="50e48-134">Na przykład jeśli przekazać zawartość pliku z akcji FTP, ładunku kontekstu wygląda w tym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="50e48-134">For example, if you pass in the file content from an FTP action, the context payload looks like this example:</span></span>

![Kontekst ładunku][2]

> [!NOTE]
> <span data-ttu-id="50e48-136">Ponieważ ten obiekt nie był rzutowany jako ciąg, zawartość jest dodawana bezpośrednio do ładunek JSON.</span><span class="sxs-lookup"><span data-stu-id="50e48-136">Because this object wasn't cast as a string, the content is added directly to the JSON payload.</span></span> <span data-ttu-id="50e48-137">Jednak występuje błąd, jeśli obiekt nie jest tokenem JSON (to znaczy, że ciąg lub JSON/Tablica obiektów).</span><span class="sxs-lookup"><span data-stu-id="50e48-137">However, an error occurs if the object is not a JSON token (that is, a string or a JSON object/array).</span></span> <span data-ttu-id="50e48-138">Można rzutować obiektu jako ciąg, Dodaj cudzysłowy, jak pokazano na pierwszym rysunku, w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="50e48-138">To cast the object as a string, add quotes as shown in the first illustration in this article.</span></span>
> 

<span data-ttu-id="50e48-139">Projektant następnie generuje szablonu funkcji, możesz utworzyć wbudowany.</span><span class="sxs-lookup"><span data-stu-id="50e48-139">The designer then generates a function template that you can create inline.</span></span> <span data-ttu-id="50e48-140">Zmienne wstępnie są tworzone na podstawie w kontekście, który chcesz przekazać do funkcji.</span><span class="sxs-lookup"><span data-stu-id="50e48-140">Variables are pre-created based on the context that you plan to pass into the function.</span></span>

<!--Image references-->
[1]: ./media/logic-apps-azure-functions/callfunction.png
[2]: ./media/logic-apps-azure-functions/createfunction.png
