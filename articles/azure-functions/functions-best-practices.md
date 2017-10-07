---
title: "aaaBest wskazówki dotyczące usługi Azure Functions | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: bd3d826b75267a740e355b008943a48f71ebd339
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-hello-performance-and-reliability-of-azure-functions"></a><span data-ttu-id="77b54-104">Optymalizacja hello wydajności i niezawodności usługi Azure Functions</span><span class="sxs-lookup"><span data-stu-id="77b54-104">Optimize hello performance and reliability of Azure Functions</span></span>

<span data-ttu-id="77b54-105">Ten artykuł zawiera wskazówki dotyczące tooimprove hello wydajności i niezawodności aplikacji funkcji.</span><span class="sxs-lookup"><span data-stu-id="77b54-105">This article provides guidance tooimprove hello performance and reliability of your function apps.</span></span> 


## <a name="avoid-long-running-functions"></a><span data-ttu-id="77b54-106">Unikaj długotrwałe funkcji</span><span class="sxs-lookup"><span data-stu-id="77b54-106">Avoid long running functions</span></span>

<span data-ttu-id="77b54-107">Funkcje dużych, długotrwałą mogą powodować problemy nieoczekiwany limitu czasu.</span><span class="sxs-lookup"><span data-stu-id="77b54-107">Large, long-running functions can cause unexpected timeout issues.</span></span> <span data-ttu-id="77b54-108">Funkcja może stać się duża powodu toomany Node.js zależności.</span><span class="sxs-lookup"><span data-stu-id="77b54-108">A function can become large due toomany Node.js dependencies.</span></span> <span data-ttu-id="77b54-109">Importowanie zależności mogą powodować zwiększone obciążenie uruchomień spowodować nieoczekiwane przekroczeń limitu czasu.</span><span class="sxs-lookup"><span data-stu-id="77b54-109">Importing dependencies can also cause increased load times that result in unexpected timeouts.</span></span> <span data-ttu-id="77b54-110">Zależności są ładowane zarówno jawnie i niejawnie.</span><span class="sxs-lookup"><span data-stu-id="77b54-110">Dependencies are loaded both explicitly and implicitly.</span></span> <span data-ttu-id="77b54-111">Moduł pojedynczego załadowane przez kod może załadować własną dodatkowych modułów.</span><span class="sxs-lookup"><span data-stu-id="77b54-111">A single module loaded by your code may load its own additional modules.</span></span>  

<span data-ttu-id="77b54-112">Jeśli to możliwe, zrefaktoryzuj długie funkcje na mniejsze funkcja ustawia które współpracują ze sobą i szybko powrócić odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="77b54-112">Whenever possible, refactor large functions into smaller function sets that work together and return responses fast.</span></span> <span data-ttu-id="77b54-113">Na przykład elementu webhook lub funkcja wyzwalacza HTTP może wymagać potwierdzenia odpowiedzi w określonym terminie. bardzo często toorequire elementów webhook natychmiastowej reakcji.</span><span class="sxs-lookup"><span data-stu-id="77b54-113">For example, a webhook or HTTP trigger function might require an acknowledgment response within a certain time limit; it is common for webhooks toorequire an immediate response.</span></span> <span data-ttu-id="77b54-114">Ładunek wyzwalacza HTTP hello można przekazać do toobe kolejki, przetwarzane przez funkcję wyzwalacza kolejki.</span><span class="sxs-lookup"><span data-stu-id="77b54-114">You can pass hello HTTP trigger payload into a queue toobe processed by a queue trigger function.</span></span> <span data-ttu-id="77b54-115">Takie podejście pozwala toodefer hello rzeczywistą pracę i zwracać natychmiastowej reakcji.</span><span class="sxs-lookup"><span data-stu-id="77b54-115">This approach allows you toodefer hello actual work and return an immediate response.</span></span>


## <a name="cross-function-communication"></a><span data-ttu-id="77b54-116">Funkcja komunikacji między</span><span class="sxs-lookup"><span data-stu-id="77b54-116">Cross function communication</span></span>

<span data-ttu-id="77b54-117">Integrowanie wiele funkcji, jest zazwyczaj najlepsze praktyki toouse kolejek magazynu dla wielu funkcji komunikacji.</span><span class="sxs-lookup"><span data-stu-id="77b54-117">When integrating multiple functions, it is generally a best practice toouse storage queues for cross function communication.</span></span>  <span data-ttu-id="77b54-118">Witaj główną przyczyną jest kolejki magazynu są tańsze i znacznie łatwiejsze tooprovision.</span><span class="sxs-lookup"><span data-stu-id="77b54-118">hello main reason is storage queues are cheaper and much easier tooprovision.</span></span> 

<span data-ttu-id="77b54-119">Poszczególne wiadomości w kolejce magazynu jest ograniczona too64 rozmiar KB.</span><span class="sxs-lookup"><span data-stu-id="77b54-119">Individual messages in a storage queue are limited in size too64 KB.</span></span> <span data-ttu-id="77b54-120">Toopass większych wiadomości między funkcji, należy kolejki usługi Azure Service Bus można rozmiary wiadomości używanych toosupport się too256 KB.</span><span class="sxs-lookup"><span data-stu-id="77b54-120">If you need toopass larger messages between functions, an Azure Service Bus queue could be used toosupport message sizes up too256 KB.</span></span>

<span data-ttu-id="77b54-121">Tematy usługi Service Bus są przydatne, jeśli potrzebujesz filtrowania przed rozpoczęciem przetwarzania komunikatu.</span><span class="sxs-lookup"><span data-stu-id="77b54-121">Service Bus topics are useful if you require message filtering before processing.</span></span>

<span data-ttu-id="77b54-122">Centra zdarzeń są przydatne toosupport dużą komunikacji.</span><span class="sxs-lookup"><span data-stu-id="77b54-122">Event hubs are useful toosupport high volume communications.</span></span>


## <a name="write-functions-toobe-stateless"></a><span data-ttu-id="77b54-123">Pisanie funkcji toobe bezstanowych</span><span class="sxs-lookup"><span data-stu-id="77b54-123">Write functions toobe stateless</span></span> 

<span data-ttu-id="77b54-124">Funkcje powinny być bezstanowych i idempotentności, jeśli to możliwe.</span><span class="sxs-lookup"><span data-stu-id="77b54-124">Functions should be stateless and idempotent if possible.</span></span> <span data-ttu-id="77b54-125">Kojarzenie żadnych informacji o stanie wymagane z danymi.</span><span class="sxs-lookup"><span data-stu-id="77b54-125">Associate any required state information with your data.</span></span> <span data-ttu-id="77b54-126">Na przykład kolejność przetwarzania prawdopodobnie byłyby skojarzony `state` elementu członkowskiego.</span><span class="sxs-lookup"><span data-stu-id="77b54-126">For example, an order being processed would likely have an associated `state` member.</span></span> <span data-ttu-id="77b54-127">Funkcja może przetworzyć zamówienia na podstawie tego stanu funkcja hello pozostaje bezstanowe.</span><span class="sxs-lookup"><span data-stu-id="77b54-127">A function could process an order based on that state while hello function itself remains stateless.</span></span> 

<span data-ttu-id="77b54-128">Funkcje idempotentności są szczególnie zalecane z wyzwalaczy czasomierza.</span><span class="sxs-lookup"><span data-stu-id="77b54-128">Idempotent functions are especially recommended with timer triggers.</span></span> <span data-ttu-id="77b54-129">Na przykład jeśli coś, co należy bezwzględnie uruchom raz dziennie, Zapisz, można je uruchomić czasie hello dnia z hello takie same wyniki.</span><span class="sxs-lookup"><span data-stu-id="77b54-129">For example, if you have something that absolutely must run once a day, write it so it can run any time during hello day with hello same results.</span></span> <span data-ttu-id="77b54-130">Funkcja Hello można zamknąć po żadnej pracy dla danego dnia.</span><span class="sxs-lookup"><span data-stu-id="77b54-130">hello function can exit when there is no work for a particular day.</span></span> <span data-ttu-id="77b54-131">Także jeśli poprzedniego uruchomienia nie powiodła się toocomplete, hello kolejnego uruchomienia powinien wybierz miejsca, w którym.</span><span class="sxs-lookup"><span data-stu-id="77b54-131">Also if a previous run failed toocomplete, hello next run should pick up where it left off.</span></span>


## <a name="write-defensive-functions"></a><span data-ttu-id="77b54-132">Pisanie funkcji obrony</span><span class="sxs-lookup"><span data-stu-id="77b54-132">Write defensive functions</span></span>

<span data-ttu-id="77b54-133">Załóżmy, że funkcja może wystąpić wyjątek w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="77b54-133">Assume your function could encounter an exception at any time.</span></span> <span data-ttu-id="77b54-134">Projektowanie funkcje za pomocą toocontinue możliwości powitania od poprzedniego punktu kończyć się niepowodzeniem podczas wykonywania dalej hello.</span><span class="sxs-lookup"><span data-stu-id="77b54-134">Design your functions with hello ability toocontinue from a previous fail point during hello next execution.</span></span> <span data-ttu-id="77b54-135">Rozważ scenariusz, który wymaga hello następujące akcje:</span><span class="sxs-lookup"><span data-stu-id="77b54-135">Consider a scenario that requires hello following actions:</span></span>

1. <span data-ttu-id="77b54-136">Zapytanie o 10 000 wierszy w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="77b54-136">Query for 10,000 rows in a db.</span></span>
2. <span data-ttu-id="77b54-137">Tworzenie komunikatu w kolejce dla każdego tooprocess tych wierszy do dalszego w hello wiersz w dół.</span><span class="sxs-lookup"><span data-stu-id="77b54-137">Create a queue message for each of those rows tooprocess further down hello line.</span></span>
 
<span data-ttu-id="77b54-138">W zależności od tego, jak złożoność system jest, może być: zachowuje nieprawidłowo zaangażowany usługami podrzędnymi, awarii sieci lub limit przydziału ogranicza osiągnęło itp. Wszystkie te mogą wpływać na funkcji w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="77b54-138">Depending on how complex your system is, you may have: involved downstream services behaving badly, networking outages, or quota limits reached, etc. All of these can affect your function at any time.</span></span> <span data-ttu-id="77b54-139">Należy toodesign Twojego toobe funkcje przygotowany dla niego.</span><span class="sxs-lookup"><span data-stu-id="77b54-139">You need toodesign your functions toobe prepared for it.</span></span>

<span data-ttu-id="77b54-140">Jak kodu reagować, jeśli wystąpi błąd po wstawieniu 5000 tych elementów w kolejce do przetworzenia?</span><span class="sxs-lookup"><span data-stu-id="77b54-140">How does your code react if a failure occurs after inserting 5,000 of those items into a queue for processing?</span></span> <span data-ttu-id="77b54-141">Śledzenie elementów w zestawie, które zostały zakończone.</span><span class="sxs-lookup"><span data-stu-id="77b54-141">Track items in a set that you’ve completed.</span></span> <span data-ttu-id="77b54-142">W przeciwnym razie możesz wstawić je ponownie po następnym.</span><span class="sxs-lookup"><span data-stu-id="77b54-142">Otherwise, you might insert them again next time.</span></span> <span data-ttu-id="77b54-143">Może to mieć poważny wpływ na Twoje przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="77b54-143">This can have a serious impact on your work flow.</span></span> 

<span data-ttu-id="77b54-144">Jeśli element kolejki został już przetworzony, Zezwalaj toobe Twojego funkcja zerowa.</span><span class="sxs-lookup"><span data-stu-id="77b54-144">If a queue item was already processed, allow your function toobe a no-op.</span></span>

<span data-ttu-id="77b54-145">Skorzystaj z środków obrony już dostarczona dla składników, używanych na platformie Azure Functions hello.</span><span class="sxs-lookup"><span data-stu-id="77b54-145">Take advantage of defensive measures already provided for components you use in hello Azure Functions platform.</span></span> <span data-ttu-id="77b54-146">Na przykład, zobacz **obsługi wiadomości w kolejce skażone** w dokumentacji hello [wyzwala kolejki magazynu Azure](functions-bindings-storage-queue.md#trigger).</span><span class="sxs-lookup"><span data-stu-id="77b54-146">For example, see **Handling poison queue messages** in hello documentation for [Azure Storage Queue triggers](functions-bindings-storage-queue.md#trigger).</span></span>
 

## <a name="dont-mix-test-and-production-code-in-hello-same-function-app"></a><span data-ttu-id="77b54-147">Nie testu mieszanego i produkcji kod hello sama aplikacja — funkcja</span><span class="sxs-lookup"><span data-stu-id="77b54-147">Don't mix test and production code in hello same function app</span></span>

<span data-ttu-id="77b54-148">Funkcje w obrębie aplikacji funkcji udostępniania zasobów.</span><span class="sxs-lookup"><span data-stu-id="77b54-148">Functions within a function app share resources.</span></span> <span data-ttu-id="77b54-149">Na przykład pamięci jest udostępniony.</span><span class="sxs-lookup"><span data-stu-id="77b54-149">For example, memory is shared.</span></span> <span data-ttu-id="77b54-150">Jeśli używasz aplikacji funkcji w środowisku produkcyjnym, nie dodawaj funkcji związanych z testu i tooit zasobów.</span><span class="sxs-lookup"><span data-stu-id="77b54-150">If you're using a function app in production, don't add test-related functions and resources tooit.</span></span> <span data-ttu-id="77b54-151">Może spowodować nieoczekiwane obciążenie podczas wykonywania kodu produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="77b54-151">It can cause unexpected overhead during production code execution.</span></span>

<span data-ttu-id="77b54-152">Należy zachować ostrożność ładowanie w aplikacjach funkcji produkcji.</span><span class="sxs-lookup"><span data-stu-id="77b54-152">Be careful what you load in your production function apps.</span></span> <span data-ttu-id="77b54-153">Pamięć jest uśredniana dla każdej funkcji aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="77b54-153">Memory is averaged across each function in hello app.</span></span>

<span data-ttu-id="77b54-154">Jeśli masz współużytkowanego zespołu, do którego odwołuje się wiele funkcji .net, umieść ją w typowych folderu udostępnionego.</span><span class="sxs-lookup"><span data-stu-id="77b54-154">If you have a shared assembly referenced in multiple .Net functions, put it in a common shared folder.</span></span> <span data-ttu-id="77b54-155">Odwołanie do zestawu hello z instrukcji toohello podobne, poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="77b54-155">Reference hello assembly with a statement similar toohello following example:</span></span> 

    #r "..\Shared\MyAssembly.dll". 

<span data-ttu-id="77b54-156">W przeciwnym razie jest łatwe tooaccidentally wdrażania wielu wersji testu hello tego samego pliku binarnego, które zachowują się inaczej między funkcji.</span><span class="sxs-lookup"><span data-stu-id="77b54-156">Otherwise, it is easy tooaccidentally deploy multiple test versions of hello same binary that behave differently between functions.</span></span>

<span data-ttu-id="77b54-157">Nie używaj pełnego rejestrowania w kodzie produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="77b54-157">Don't use verbose logging in production code.</span></span> <span data-ttu-id="77b54-158">Ma ona negatywny wpływ na wydajność.</span><span class="sxs-lookup"><span data-stu-id="77b54-158">It has a negative performance impact.</span></span>



## <a name="use-async-code-but-avoid-blocking-calls"></a><span data-ttu-id="77b54-159">Użyj kodu asynchroniczne, ale unikania blokowania połączeń</span><span class="sxs-lookup"><span data-stu-id="77b54-159">Use async code but avoid blocking calls</span></span>

<span data-ttu-id="77b54-160">Programowanie asynchroniczne jest zalecanym najlepszym rozwiązaniem.</span><span class="sxs-lookup"><span data-stu-id="77b54-160">Asynchronous programming is a recommended best practice.</span></span> <span data-ttu-id="77b54-161">Jednak zawsze uniknąć odwołujące się do hello `Result` właściwość lub wywołanie `Wait` metoda `Task` wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="77b54-161">However, always avoid referencing hello `Result` property or calling `Wait` method on a `Task` instance.</span></span> <span data-ttu-id="77b54-162">Takie podejście może spowodować wyczerpanie toothread.</span><span class="sxs-lookup"><span data-stu-id="77b54-162">This approach can lead toothread exhaustion.</span></span>


[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

## <a name="next-steps"></a><span data-ttu-id="77b54-163">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="77b54-163">Next steps</span></span>
<span data-ttu-id="77b54-164">Aby uzyskać więcej informacji zobacz następujące zasoby hello:</span><span class="sxs-lookup"><span data-stu-id="77b54-164">For more information, see hello following resources:</span></span>

<span data-ttu-id="77b54-165">Ponieważ usługi Azure Functions używa usługi Azure App Service, należy wziąć pod uwagę wskazówki dotyczące usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="77b54-165">Because Azure Functions uses Azure App Service, you should also be aware of  App Service guidelines.</span></span>
* [<span data-ttu-id="77b54-166">Wzorce i praktyki optymalizacji wydajności HTTP</span><span class="sxs-lookup"><span data-stu-id="77b54-166">Patterns and Practices HTTP Performance Optimizations</span></span>](https://docs.microsoft.com/azure/architecture/antipatterns/improper-instantiation/)

