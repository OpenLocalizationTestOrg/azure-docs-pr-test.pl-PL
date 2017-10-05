---
title: "Najlepsze rozwiązania dotyczące funkcji platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się najlepsze rozwiązania i wzorce dla usługi Azure Functions."
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "środowisko Azure functions, wzorce, najlepszym rozwiązaniem, funkcji, przetwarzania elementów webhook, dynamiczne obliczeń, architektura niekorzystającą zdarzeń"
ms.assetid: 9058fb2f-8a93-4036-a921-97a0772f503c
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/13/2017
ms.author: glenga
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 645a5dd16e72619e7c2470ab8f03098f0fa6c7f8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="optimize-the-performance-and-reliability-of-azure-functions"></a><span data-ttu-id="860ba-104">Optymalizuj wydajność i niezawodność usługi Azure Functions</span><span class="sxs-lookup"><span data-stu-id="860ba-104">Optimize the performance and reliability of Azure Functions</span></span>

<span data-ttu-id="860ba-105">Ten artykuł zawiera wskazówki dotyczące poprawy wydajności i niezawodności aplikacji funkcji.</span><span class="sxs-lookup"><span data-stu-id="860ba-105">This article provides guidance to improve the performance and reliability of your function apps.</span></span> 


## <a name="avoid-long-running-functions"></a><span data-ttu-id="860ba-106">Unikaj długotrwałe funkcji</span><span class="sxs-lookup"><span data-stu-id="860ba-106">Avoid long running functions</span></span>

<span data-ttu-id="860ba-107">Funkcje dużych, długotrwałą mogą powodować problemy nieoczekiwany limitu czasu.</span><span class="sxs-lookup"><span data-stu-id="860ba-107">Large, long-running functions can cause unexpected timeout issues.</span></span> <span data-ttu-id="860ba-108">Funkcja może stać się duża ze względu na wiele zależności Node.js.</span><span class="sxs-lookup"><span data-stu-id="860ba-108">A function can become large due to many Node.js dependencies.</span></span> <span data-ttu-id="860ba-109">Importowanie zależności mogą powodować zwiększone obciążenie uruchomień spowodować nieoczekiwane przekroczeń limitu czasu.</span><span class="sxs-lookup"><span data-stu-id="860ba-109">Importing dependencies can also cause increased load times that result in unexpected timeouts.</span></span> <span data-ttu-id="860ba-110">Zależności są ładowane zarówno jawnie i niejawnie.</span><span class="sxs-lookup"><span data-stu-id="860ba-110">Dependencies are loaded both explicitly and implicitly.</span></span> <span data-ttu-id="860ba-111">Moduł pojedynczego załadowane przez kod może załadować własną dodatkowych modułów.</span><span class="sxs-lookup"><span data-stu-id="860ba-111">A single module loaded by your code may load its own additional modules.</span></span>  

<span data-ttu-id="860ba-112">Jeśli to możliwe, zrefaktoryzuj długie funkcje na mniejsze funkcja ustawia które współpracują ze sobą i szybko powrócić odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="860ba-112">Whenever possible, refactor large functions into smaller function sets that work together and return responses fast.</span></span> <span data-ttu-id="860ba-113">Na przykład elementu webhook lub funkcja wyzwalacza HTTP może wymagać potwierdzenia odpowiedzi w określonym terminie. jest typowe dla elementów webhook wymagają natychmiastowej reakcji.</span><span class="sxs-lookup"><span data-stu-id="860ba-113">For example, a webhook or HTTP trigger function might require an acknowledgment response within a certain time limit; it is common for webhooks to require an immediate response.</span></span> <span data-ttu-id="860ba-114">Ładunek wyzwalacza HTTP można przekazać w kolejce do przetworzenia przez funkcję wyzwalacza kolejki.</span><span class="sxs-lookup"><span data-stu-id="860ba-114">You can pass the HTTP trigger payload into a queue to be processed by a queue trigger function.</span></span> <span data-ttu-id="860ba-115">Takie podejście umożliwia odroczenie rzeczywistą pracę i zwracać natychmiastowej reakcji.</span><span class="sxs-lookup"><span data-stu-id="860ba-115">This approach allows you to defer the actual work and return an immediate response.</span></span>


## <a name="cross-function-communication"></a><span data-ttu-id="860ba-116">Funkcja komunikacji między</span><span class="sxs-lookup"><span data-stu-id="860ba-116">Cross function communication</span></span>

<span data-ttu-id="860ba-117">Podczas integracji wiele funkcji, zazwyczaj jest najlepszym rozwiązaniem jest użycie kolejek magazynu dla wielu funkcji komunikacji.</span><span class="sxs-lookup"><span data-stu-id="860ba-117">When integrating multiple functions, it is generally a best practice to use storage queues for cross function communication.</span></span>  <span data-ttu-id="860ba-118">Głównym celem jest kolejki magazynu to tańsze i znacznie łatwiejsze do udostępniania.</span><span class="sxs-lookup"><span data-stu-id="860ba-118">The main reason is storage queues are cheaper and much easier to provision.</span></span> 

<span data-ttu-id="860ba-119">Poszczególne wiadomości w kolejce magazynu są ograniczone w rozmiarze 64 KB.</span><span class="sxs-lookup"><span data-stu-id="860ba-119">Individual messages in a storage queue are limited in size to 64 KB.</span></span> <span data-ttu-id="860ba-120">Jeśli chcesz przekazać większych wiadomości pomiędzy funkcjami usługi Azure Service Bus kolejka może służyć do obsługi wiadomości rozmiarów do 256 KB.</span><span class="sxs-lookup"><span data-stu-id="860ba-120">If you need to pass larger messages between functions, an Azure Service Bus queue could be used to support message sizes up to 256 KB.</span></span>

<span data-ttu-id="860ba-121">Tematy usługi Service Bus są przydatne, jeśli potrzebujesz filtrowania przed rozpoczęciem przetwarzania komunikatu.</span><span class="sxs-lookup"><span data-stu-id="860ba-121">Service Bus topics are useful if you require message filtering before processing.</span></span>

<span data-ttu-id="860ba-122">Centra zdarzeń są przydatne do obsługi dużych obciążeń komunikacji.</span><span class="sxs-lookup"><span data-stu-id="860ba-122">Event hubs are useful to support high volume communications.</span></span>


## <a name="write-functions-to-be-stateless"></a><span data-ttu-id="860ba-123">Pisanie funkcji jako bezstanowy</span><span class="sxs-lookup"><span data-stu-id="860ba-123">Write functions to be stateless</span></span> 

<span data-ttu-id="860ba-124">Funkcje powinny być bezstanowych i idempotentności, jeśli to możliwe.</span><span class="sxs-lookup"><span data-stu-id="860ba-124">Functions should be stateless and idempotent if possible.</span></span> <span data-ttu-id="860ba-125">Kojarzenie żadnych informacji o stanie wymagane z danymi.</span><span class="sxs-lookup"><span data-stu-id="860ba-125">Associate any required state information with your data.</span></span> <span data-ttu-id="860ba-126">Na przykład kolejność przetwarzania prawdopodobnie byłyby skojarzony `state` elementu członkowskiego.</span><span class="sxs-lookup"><span data-stu-id="860ba-126">For example, an order being processed would likely have an associated `state` member.</span></span> <span data-ttu-id="860ba-127">Funkcja może przetworzyć zamówienia na podstawie w tym stanie, gdy ta funkcja jest bezstanowych.</span><span class="sxs-lookup"><span data-stu-id="860ba-127">A function could process an order based on that state while the function itself remains stateless.</span></span> 

<span data-ttu-id="860ba-128">Funkcje idempotentności są szczególnie zalecane z wyzwalaczy czasomierza.</span><span class="sxs-lookup"><span data-stu-id="860ba-128">Idempotent functions are especially recommended with timer triggers.</span></span> <span data-ttu-id="860ba-129">Na przykład jeśli coś, co należy bezwzględnie uruchom raz dziennie, Zapisz, można je uruchomić czasie dnia z takie same wyniki.</span><span class="sxs-lookup"><span data-stu-id="860ba-129">For example, if you have something that absolutely must run once a day, write it so it can run any time during the day with the same results.</span></span> <span data-ttu-id="860ba-130">Funkcja można zamknąć po żadnej pracy dla danego dnia.</span><span class="sxs-lookup"><span data-stu-id="860ba-130">The function can exit when there is no work for a particular day.</span></span> <span data-ttu-id="860ba-131">Także jeśli poprzedniej uruchamianie nie powiodło się, aby zakończyć, przy następnym uruchomieniu należy wybierz miejsca, w którym.</span><span class="sxs-lookup"><span data-stu-id="860ba-131">Also if a previous run failed to complete, the next run should pick up where it left off.</span></span>


## <a name="write-defensive-functions"></a><span data-ttu-id="860ba-132">Pisanie funkcji obrony</span><span class="sxs-lookup"><span data-stu-id="860ba-132">Write defensive functions</span></span>

<span data-ttu-id="860ba-133">Załóżmy, że funkcja może wystąpić wyjątek w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="860ba-133">Assume your function could encounter an exception at any time.</span></span> <span data-ttu-id="860ba-134">Projektowanie funkcji z możliwością kontynuować od poprzedniego punktu kończyć się niepowodzeniem podczas wykonywania dalej.</span><span class="sxs-lookup"><span data-stu-id="860ba-134">Design your functions with the ability to continue from a previous fail point during the next execution.</span></span> <span data-ttu-id="860ba-135">Rozważmy scenariusz, który wymaga następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="860ba-135">Consider a scenario that requires the following actions:</span></span>

1. <span data-ttu-id="860ba-136">Zapytanie o 10 000 wierszy w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="860ba-136">Query for 10,000 rows in a db.</span></span>
2. <span data-ttu-id="860ba-137">Tworzenie komunikatu w kolejce dla każdego z tych wierszy do dalszego przetwarzania wiersz w dół.</span><span class="sxs-lookup"><span data-stu-id="860ba-137">Create a queue message for each of those rows to process further down the line.</span></span>
 
<span data-ttu-id="860ba-138">W zależności od tego, jak złożoność system jest, może być: zachowuje nieprawidłowo zaangażowany usługami podrzędnymi, awarii sieci lub limit przydziału ogranicza osiągnęło itp. Wszystkie te mogą wpływać na funkcji w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="860ba-138">Depending on how complex your system is, you may have: involved downstream services behaving badly, networking outages, or quota limits reached, etc. All of these can affect your function at any time.</span></span> <span data-ttu-id="860ba-139">Należy projektować funkcji, aby móc przywrócić go.</span><span class="sxs-lookup"><span data-stu-id="860ba-139">You need to design your functions to be prepared for it.</span></span>

<span data-ttu-id="860ba-140">Jak kodu reagować, jeśli wystąpi błąd po wstawieniu 5000 tych elementów w kolejce do przetworzenia?</span><span class="sxs-lookup"><span data-stu-id="860ba-140">How does your code react if a failure occurs after inserting 5,000 of those items into a queue for processing?</span></span> <span data-ttu-id="860ba-141">Śledzenie elementów w zestawie, które zostały zakończone.</span><span class="sxs-lookup"><span data-stu-id="860ba-141">Track items in a set that you’ve completed.</span></span> <span data-ttu-id="860ba-142">W przeciwnym razie możesz wstawić je ponownie po następnym.</span><span class="sxs-lookup"><span data-stu-id="860ba-142">Otherwise, you might insert them again next time.</span></span> <span data-ttu-id="860ba-143">Może to mieć poważny wpływ na Twoje przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="860ba-143">This can have a serious impact on your work flow.</span></span> 

<span data-ttu-id="860ba-144">Jeśli element kolejki został już przetworzony, Zezwalaj funkcja ma być pusta.</span><span class="sxs-lookup"><span data-stu-id="860ba-144">If a queue item was already processed, allow your function to be a no-op.</span></span>

<span data-ttu-id="860ba-145">Skorzystaj z środków obrony już dostarczona dla składników używanych przez platformę Azure funkcji.</span><span class="sxs-lookup"><span data-stu-id="860ba-145">Take advantage of defensive measures already provided for components you use in the Azure Functions platform.</span></span> <span data-ttu-id="860ba-146">Na przykład, zobacz **obsługi wiadomości w kolejce skażone** w dokumentacji dotyczącej [wyzwala kolejki magazynu Azure](functions-bindings-storage-queue.md#trigger).</span><span class="sxs-lookup"><span data-stu-id="860ba-146">For example, see **Handling poison queue messages** in the documentation for [Azure Storage Queue triggers](functions-bindings-storage-queue.md#trigger).</span></span>
 

## <a name="dont-mix-test-and-production-code-in-the-same-function-app"></a><span data-ttu-id="860ba-147">Nie można mieszać testowych i produkcyjnych kodu w tej samej aplikacji — funkcja</span><span class="sxs-lookup"><span data-stu-id="860ba-147">Don't mix test and production code in the same function app</span></span>

<span data-ttu-id="860ba-148">Funkcje w obrębie aplikacji funkcji udostępniania zasobów.</span><span class="sxs-lookup"><span data-stu-id="860ba-148">Functions within a function app share resources.</span></span> <span data-ttu-id="860ba-149">Na przykład pamięci jest udostępniony.</span><span class="sxs-lookup"><span data-stu-id="860ba-149">For example, memory is shared.</span></span> <span data-ttu-id="860ba-150">Jeśli używasz aplikacji funkcji w środowisku produkcyjnym, nie dodawaj funkcji związanych z testu i zasoby do niego.</span><span class="sxs-lookup"><span data-stu-id="860ba-150">If you're using a function app in production, don't add test-related functions and resources to it.</span></span> <span data-ttu-id="860ba-151">Może spowodować nieoczekiwane obciążenie podczas wykonywania kodu produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="860ba-151">It can cause unexpected overhead during production code execution.</span></span>

<span data-ttu-id="860ba-152">Należy zachować ostrożność ładowanie w aplikacjach funkcji produkcji.</span><span class="sxs-lookup"><span data-stu-id="860ba-152">Be careful what you load in your production function apps.</span></span> <span data-ttu-id="860ba-153">Pamięć jest uśredniana dla poszczególnych funkcji w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="860ba-153">Memory is averaged across each function in the app.</span></span>

<span data-ttu-id="860ba-154">Jeśli masz współużytkowanego zespołu, do którego odwołuje się wiele funkcji .net, umieść ją w typowych folderu udostępnionego.</span><span class="sxs-lookup"><span data-stu-id="860ba-154">If you have a shared assembly referenced in multiple .Net functions, put it in a common shared folder.</span></span> <span data-ttu-id="860ba-155">Odwołanie zestawu z instrukcją podobny do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="860ba-155">Reference the assembly with a statement similar to the following example:</span></span> 

    #r "..\Shared\MyAssembly.dll". 

<span data-ttu-id="860ba-156">W przeciwnym razie jest łatwe przypadkowo wdrożono wiele wersji testu z tych samych danych binarnych, które zachowują się inaczej pomiędzy funkcjami.</span><span class="sxs-lookup"><span data-stu-id="860ba-156">Otherwise, it is easy to accidentally deploy multiple test versions of the same binary that behave differently between functions.</span></span>

<span data-ttu-id="860ba-157">Nie używaj pełnego rejestrowania w kodzie produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="860ba-157">Don't use verbose logging in production code.</span></span> <span data-ttu-id="860ba-158">Ma ona negatywny wpływ na wydajność.</span><span class="sxs-lookup"><span data-stu-id="860ba-158">It has a negative performance impact.</span></span>



## <a name="use-async-code-but-avoid-blocking-calls"></a><span data-ttu-id="860ba-159">Użyj kodu asynchroniczne, ale unikania blokowania połączeń</span><span class="sxs-lookup"><span data-stu-id="860ba-159">Use async code but avoid blocking calls</span></span>

<span data-ttu-id="860ba-160">Programowanie asynchroniczne jest zalecanym najlepszym rozwiązaniem.</span><span class="sxs-lookup"><span data-stu-id="860ba-160">Asynchronous programming is a recommended best practice.</span></span> <span data-ttu-id="860ba-161">Jednak zawsze uniknąć odwołujące się do `Result` właściwość lub wywołanie `Wait` metoda `Task` wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="860ba-161">However, always avoid referencing the `Result` property or calling `Wait` method on a `Task` instance.</span></span> <span data-ttu-id="860ba-162">Takie podejście może doprowadzić do wyczerpania wątku.</span><span class="sxs-lookup"><span data-stu-id="860ba-162">This approach can lead to thread exhaustion.</span></span>


[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

## <a name="next-steps"></a><span data-ttu-id="860ba-163">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="860ba-163">Next steps</span></span>
<span data-ttu-id="860ba-164">Więcej informacji zawierają następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="860ba-164">For more information, see the following resources:</span></span>

<span data-ttu-id="860ba-165">Ponieważ usługi Azure Functions używa usługi Azure App Service, należy wziąć pod uwagę wskazówki dotyczące usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="860ba-165">Because Azure Functions uses Azure App Service, you should also be aware of  App Service guidelines.</span></span>
* [<span data-ttu-id="860ba-166">Wzorce i praktyki optymalizacji wydajności HTTP</span><span class="sxs-lookup"><span data-stu-id="860ba-166">Patterns and Practices HTTP Performance Optimizations</span></span>](https://docs.microsoft.com/azure/architecture/antipatterns/improper-instantiation/)

