---
title: "Kod aaaCustom dla usługi Azure Logic Apps w środowisku Azure Functions | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 18b3821ed7e434feb568b9b96e9a5a2189dba3bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-and-run-custom-code-for-logic-apps-through-azure-functions"></a><span data-ttu-id="1a9fa-103">Dodaj i uruchomienia niestandardowego kodu dla usługi logic apps za pomocą usługi Azure Functions</span><span class="sxs-lookup"><span data-stu-id="1a9fa-103">Add and run custom code for logic apps through Azure Functions</span></span>

<span data-ttu-id="1a9fa-104">toorun niestandardowych fragmenty kodu języka C# lub node.js w aplikacji logiki, można utworzyć funkcji niestandardowych za pomocą usługi Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="1a9fa-104">toorun custom snippets of C# or node.js in logic apps, you can create custom functions through Azure Functions.</span></span> 
<span data-ttu-id="1a9fa-105">[Środowisko Azure Functions](../azure-functions/functions-overview.md) oferuje wolny od serwera przetwarzania danych w Microsoft Azure i są użyteczne do wykonywania tych zadań:</span><span class="sxs-lookup"><span data-stu-id="1a9fa-105">[Azure Functions](../azure-functions/functions-overview.md) offers server-free computing in Microsoft Azure and are useful for performing these tasks:</span></span>

* <span data-ttu-id="1a9fa-106">Zaawansowane, formatowanie lub obliczeniowych pól w aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="1a9fa-106">Advanced formatting or compute of fields in logic apps</span></span>
* <span data-ttu-id="1a9fa-107">Wykonywanie obliczeń w przepływie pracy.</span><span class="sxs-lookup"><span data-stu-id="1a9fa-107">Perform calculations in a workflow.</span></span>
* <span data-ttu-id="1a9fa-108">Rozszerzenia funkcji aplikacji logiki hello z funkcjami, które są obsługiwane w języku C# lub node.js</span><span class="sxs-lookup"><span data-stu-id="1a9fa-108">Extend hello logic app functionality with functions that are supported in C# or node.js</span></span>

## <a name="create-custom-functions-for-your-logic-apps"></a><span data-ttu-id="1a9fa-109">Tworzenie funkcji niestandardowych dla aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="1a9fa-109">Create custom functions for your logic apps</span></span>

<span data-ttu-id="1a9fa-110">Zaleca się utworzenie funkcji w portalu usługi Azure Functions hello z hello **ogólny element Webhook - węzła** lub **ogólny element Webhook - C#** szablonów.</span><span class="sxs-lookup"><span data-stu-id="1a9fa-110">We recommend that you create a function in hello Azure Functions portal, from hello **Generic Webhook - Node** or **Generic Webhook - C#** templates.</span></span> <span data-ttu-id="1a9fa-111">wynik Hello tworzy wypełniana automatycznie szablon, który akceptuje `application/json` z aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="1a9fa-111">hello result creates an auto-populated a template that accepts `application/json` from a logic app.</span></span> <span data-ttu-id="1a9fa-112">Funkcje, które utworzono z tych szablonów są automatycznie wykrywane i są wyświetlane w hello projektanta aplikacji logiki w obszarze **usługi Azure Functions w moim regionie.**</span><span class="sxs-lookup"><span data-stu-id="1a9fa-112">Functions that you create from these templates are automatically detected and appear in hello Logic App Designer under **Azure Functions in my region.**</span></span>

<span data-ttu-id="1a9fa-113">W portalu Azure na powitania hello **integracji** okienku dla funkcji szablon powinien pokazują, że **tryb** ustawić także**Webhook** i **typu elementu Webhook** ustawiono zbyt**ogólnego JSON**.</span><span class="sxs-lookup"><span data-stu-id="1a9fa-113">In hello Azure portal, on hello **Integrate** pane for your function, your template should show that **Mode** set too**Webhook** and **Webhook type** is set too**Generic JSON**.</span></span> 

<span data-ttu-id="1a9fa-114">Funkcje elementu Webhook zaakceptować żądania i przekaż go do metody hello za pośrednictwem `data` zmiennej.</span><span class="sxs-lookup"><span data-stu-id="1a9fa-114">Webhook functions accept a request and pass it into hello method via a `data` variable.</span></span> <span data-ttu-id="1a9fa-115">Uzyskać dostęp do właściwości hello Twojej ładunku, używając zapisu kropkowego jak `data.function-name`.</span><span class="sxs-lookup"><span data-stu-id="1a9fa-115">You can access hello properties of your payload by using dot notation like `data.function-name`.</span></span> <span data-ttu-id="1a9fa-116">Na przykład prosty funkcji JavaScript, który konwertuje wartości daty i godziny do ciągu daty wygląda hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="1a9fa-116">For example, a simple JavaScript function that converts a DateTime value into a date string looks like hello following example:</span></span>

```
function start(req, res){
    var data = req.body;
    res = {
        body: data.date.ToDateString();
    }
}
```

## <a name="call-azure-functions-from-logic-apps"></a><span data-ttu-id="1a9fa-117">Wywołanie usługi Azure Functions w aplikacjach logic apps</span><span class="sxs-lookup"><span data-stu-id="1a9fa-117">Call Azure Functions from logic apps</span></span>

<span data-ttu-id="1a9fa-118">kontenery hello toolist w Twojej subskrypcji i wybierz hello funkcji, które mają toocall w Projektancie aplikacji logiki, kliknij przycisk hello **akcje** menu, a następnie wybierz z **usługi Azure Functions w moim regionie**.</span><span class="sxs-lookup"><span data-stu-id="1a9fa-118">toolist hello containers in your subscription and select hello function that you want toocall, in Logic App Designer, click hello **Actions** menu, and select from **Azure Functions in my Region**.</span></span>

<span data-ttu-id="1a9fa-119">Po wybraniu funkcji hello są zadawane toospecify obiektu wprowadzony ładunek.</span><span class="sxs-lookup"><span data-stu-id="1a9fa-119">After you select hello function, you are asked toospecify an input payload object.</span></span> <span data-ttu-id="1a9fa-120">Ten obiekt jest wiadomość hello hello logiki aplikacji wysyła toohello funkcji i musi być obiektem JSON.</span><span class="sxs-lookup"><span data-stu-id="1a9fa-120">This object is hello message that hello logic app sends toohello function and must be a JSON object.</span></span> <span data-ttu-id="1a9fa-121">Na przykład, jeśli chcesz, aby toopass w hello **ostatniej modyfikacji** daty z wyzwalacza Salesforce ładunku funkcja hello może wyglądać w tym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="1a9fa-121">For example, if you want toopass in hello **Last Modified** date from a Salesforce trigger, hello function payload might look like this example:</span></span>

![Data ostatniej modyfikacji][1]

## <a name="trigger-logic-apps-from-a-function"></a><span data-ttu-id="1a9fa-123">Aplikacje logiki wyzwalacza w funkcji</span><span class="sxs-lookup"><span data-stu-id="1a9fa-123">Trigger logic apps from a function</span></span>

<span data-ttu-id="1a9fa-124">Możesz wyzwolić aplikacji logiki z wewnątrz funkcji.</span><span class="sxs-lookup"><span data-stu-id="1a9fa-124">You can trigger a logic app from inside a function.</span></span> <span data-ttu-id="1a9fa-125">Zobacz [logiki aplikacji jako punkty końcowe można wywołać](logic-apps-http-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="1a9fa-125">See [Logic apps as callable endpoints](logic-apps-http-endpoint.md).</span></span> <span data-ttu-id="1a9fa-126">Tworzenie aplikacji logiki, która zawiera wyzwalacz ręcznego, a następnie z wewnątrz funkcji, wygeneruj adres URL ręczne wyzwalacza toohello HTTP POST z ładunku hello, który ma być wysyłane toohello aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="1a9fa-126">Create a logic app that has a manual trigger, then from inside your function, generate an HTTP POST toohello manual trigger URL with hello payload that you want sent toohello logic app.</span></span>

### <a name="create-a-function-from-logic-app-designer"></a><span data-ttu-id="1a9fa-127">Tworzenie funkcji przy użyciu projektanta aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="1a9fa-127">Create a function from Logic App Designer</span></span>

<span data-ttu-id="1a9fa-128">Można również utworzyć funkcję webhook node.js przy użyciu projektanta hello.</span><span class="sxs-lookup"><span data-stu-id="1a9fa-128">You can also create a node.js webhook function from hello designer.</span></span> <span data-ttu-id="1a9fa-129">Najpierw wybierz **usługi Azure Functions w moim regionie** , a następnie wybierz kontener dla funkcji.</span><span class="sxs-lookup"><span data-stu-id="1a9fa-129">First, select **Azure Functions in my Region,** and then choose a container for your function.</span></span> <span data-ttu-id="1a9fa-130">Jeśli jeszcze nie masz kontenera, należy toocreate jedną z hello [portalu Azure Functions](https://functions.azure.com/signin).</span><span class="sxs-lookup"><span data-stu-id="1a9fa-130">If you don't yet have a container, you need toocreate one from hello [Azure Functions portal](https://functions.azure.com/signin).</span></span> <span data-ttu-id="1a9fa-131">Następnie wybierz **Utwórz nowy**.</span><span class="sxs-lookup"><span data-stu-id="1a9fa-131">Then select **Create New**.</span></span>  

<span data-ttu-id="1a9fa-132">toogenerate szablon na podstawie danych hello, które mają toocompute, określić obiekt kontekstu hello planowanie toopass funkcji.</span><span class="sxs-lookup"><span data-stu-id="1a9fa-132">toogenerate a template based on hello data that you want toocompute, specify hello context object that you plan toopass into a function.</span></span> <span data-ttu-id="1a9fa-133">Ten obiekt musi być obiektem JSON.</span><span class="sxs-lookup"><span data-stu-id="1a9fa-133">This object must be a JSON object.</span></span> <span data-ttu-id="1a9fa-134">Na przykład jeśli przekazać zawartość pliku hello z akcji FTP, ładunku kontekstu hello wygląda w tym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="1a9fa-134">For example, if you pass in hello file content from an FTP action, hello context payload looks like this example:</span></span>

![Kontekst ładunku][2]

> [!NOTE]
> <span data-ttu-id="1a9fa-136">Ponieważ ten obiekt nie był rzutowany jako ciąg, hello zawartość jest dodawana bezpośrednio toohello ładunek JSON.</span><span class="sxs-lookup"><span data-stu-id="1a9fa-136">Because this object wasn't cast as a string, hello content is added directly toohello JSON payload.</span></span> <span data-ttu-id="1a9fa-137">Jednak występuje błąd, jeśli obiekt hello nie jest tokenem JSON (to znaczy, że ciąg lub JSON/Tablica obiektów).</span><span class="sxs-lookup"><span data-stu-id="1a9fa-137">However, an error occurs if hello object is not a JSON token (that is, a string or a JSON object/array).</span></span> <span data-ttu-id="1a9fa-138">toocast hello obiekt jako ciąg, Dodaj cudzysłowy, jak pokazano w pierwszym rysunku hello w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="1a9fa-138">toocast hello object as a string, add quotes as shown in hello first illustration in this article.</span></span>
> 

<span data-ttu-id="1a9fa-139">Projektant Hello następnie generuje szablonu funkcji, możesz utworzyć wbudowany.</span><span class="sxs-lookup"><span data-stu-id="1a9fa-139">hello designer then generates a function template that you can create inline.</span></span> <span data-ttu-id="1a9fa-140">Zmienne wstępnie są tworzone na podstawie kontekstu hello planowanie toopass do funkcji hello.</span><span class="sxs-lookup"><span data-stu-id="1a9fa-140">Variables are pre-created based on hello context that you plan toopass into hello function.</span></span>

<!--Image references-->
[1]: ./media/logic-apps-azure-functions/callfunction.png
[2]: ./media/logic-apps-azure-functions/createfunction.png
