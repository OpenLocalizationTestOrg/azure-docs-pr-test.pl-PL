---
ms.assetid: 
title: "aaaAzure wskazówki dotyczące ograniczania przepustowości usługi Key Vault | Dokumentacja firmy Microsoft"
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 06/21/2017
ms.openlocfilehash: a75cf96bc6503e51f14378bee598bad57e85be82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-throttling-guidance"></a><span data-ttu-id="df661-102">Usługa Azure Key Vault ograniczania wskazówki</span><span class="sxs-lookup"><span data-stu-id="df661-102">Azure Key Vault throttling guidance</span></span>

<span data-ttu-id="df661-103">Ograniczanie jest procesem zainicjowanych przez ogranicza liczbę hello nadmierne zużycie tooprevent usługi Azure toohello równoczesnych wywołań zasobów.</span><span class="sxs-lookup"><span data-stu-id="df661-103">Throttling is a process you initiate that limits hello number of concurrent calls toohello Azure service tooprevent overuse of resources.</span></span> <span data-ttu-id="df661-104">Magazyn kluczy Azure (AKV) jest zaprojektowana toohandle dużą liczbę żądań.</span><span class="sxs-lookup"><span data-stu-id="df661-104">Azure Key Vault (AKV) is designed toohandle a high volume of requests.</span></span> <span data-ttu-id="df661-105">W przypadku utrudnione liczba żądań ograniczanie żądań klienta pomaga utrzymać optymalną wydajność i niezawodność hello AKV usługi.</span><span class="sxs-lookup"><span data-stu-id="df661-105">If an overwhelming number of requests occurs, throttling your client's requests helps maintain optimal performance and reliability of hello AKV service.</span></span>

<span data-ttu-id="df661-106">Limity ograniczania przepustowości różnić w zależności od scenariusza hello.</span><span class="sxs-lookup"><span data-stu-id="df661-106">Throttling limits vary based on hello scenario.</span></span> <span data-ttu-id="df661-107">Na przykład jeśli przeprowadzasz dużą liczbę operacji zapisu, ograniczanie możliwości hello jest wyższa niż jeśli tylko wykonywana odczyty.</span><span class="sxs-lookup"><span data-stu-id="df661-107">For example, if you are performing a large volume of writes, hello possibility for throttling is higher than if you are only performing reads.</span></span>

## <a name="how-does-key-vault-handle-its-limits"></a><span data-ttu-id="df661-108">Jak usługi Key Vault obsługuje limit?</span><span class="sxs-lookup"><span data-stu-id="df661-108">How does Key Vault handle its limits?</span></span>

<span data-ttu-id="df661-109">Ograniczenia usługi Key Vault istnieją tooprevent nieprawidłowe użycie zasobów i zapewnienia jakości usług dla wszystkich klientów usługi Key Vault.</span><span class="sxs-lookup"><span data-stu-id="df661-109">Service limits in Key Vault are there tooprevent misuse of resources and ensure quality of service for all of Key Vault’s clients.</span></span> <span data-ttu-id="df661-110">Po przekroczeniu progu usługi Key Vault ogranicza żadnych dalszych żądań z tego klienta w danym okresie czasu.</span><span class="sxs-lookup"><span data-stu-id="df661-110">When a service threshold is exceeded, Key Vault limits any further requests from that client for a period of time.</span></span> <span data-ttu-id="df661-111">W takim przypadku magazyn kluczy zwraca kod stanu HTTP 429 (zbyt wiele żądań), oraz hello żądania kończyć się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="df661-111">When this happens, Key Vault returns HTTP status code 429 (Too many requests), and hello requests fail.</span></span> <span data-ttu-id="df661-112">Ponadto nie żądań zwracających 429 liczba kierunku limity przepustowości hello śledzone przez magazyn kluczy.</span><span class="sxs-lookup"><span data-stu-id="df661-112">Also, failed requests that return a 429 count towards hello throttle limits tracked by Key Vault.</span></span> 

<span data-ttu-id="df661-113">Jeśli masz prawidłowe firm przypadku wyższe limity przepustowości, skontaktuj się z nami.</span><span class="sxs-lookup"><span data-stu-id="df661-113">If you have a valid business case for higher throttle limits, please contact us.</span></span>


## <a name="how-toothrottle-your-app-in-response-tooservice-limits"></a><span data-ttu-id="df661-114">Jak toothrottle aplikacji w odpowiedzi tooservice ogranicza</span><span class="sxs-lookup"><span data-stu-id="df661-114">How toothrottle your app in response tooservice limits</span></span>

<span data-ttu-id="df661-115">Witaj poniżej przedstawiono **najlepsze rozwiązania** dla ograniczania aplikacji:</span><span class="sxs-lookup"><span data-stu-id="df661-115">hello following are **best practices** for throttling your app:</span></span>
- <span data-ttu-id="df661-116">Ogranicz liczbę hello operacji na żądanie.</span><span class="sxs-lookup"><span data-stu-id="df661-116">Reduce hello number of operations per request.</span></span>
- <span data-ttu-id="df661-117">Zmniejsz częstotliwość hello żądań.</span><span class="sxs-lookup"><span data-stu-id="df661-117">Reduce hello frequency of requests.</span></span>
- <span data-ttu-id="df661-118">Należy unikać bezpośredniego ponownych prób.</span><span class="sxs-lookup"><span data-stu-id="df661-118">Avoid immediate retries.</span></span> 
    - <span data-ttu-id="df661-119">Wszystkie żądania są naliczane względem limitów do użycia.</span><span class="sxs-lookup"><span data-stu-id="df661-119">All requests accrue against your usage limits.</span></span>

<span data-ttu-id="df661-120">Podczas implementowania obsługi błędów aplikacji, użyj hello HTTP Błąd kodu 429 toodetect hello potrzebę ograniczania po stronie klienta.</span><span class="sxs-lookup"><span data-stu-id="df661-120">When you implement your app's error handling, use hello HTTP error code 429 toodetect hello need for client-side throttling.</span></span> <span data-ttu-id="df661-121">Jeśli Żądanie hello nie powiedzie się ponownie z kodem błędu HTTP 429, pojawiły się nadal limit usług Azure.</span><span class="sxs-lookup"><span data-stu-id="df661-121">If hello request fails again with an HTTP 429 error code, you are still encountering an Azure service limit.</span></span> <span data-ttu-id="df661-122">Kontynuować toouse hello zalecana metoda ograniczania przepustowości po stronie klienta, ponawianie próby hello żądania do skutku.</span><span class="sxs-lookup"><span data-stu-id="df661-122">Continue toouse hello recommended client-side throttling method, retrying hello request until it succeeds.</span></span>

### <a name="recommended-client-side-throttling-method"></a><span data-ttu-id="df661-123">Zalecana metoda ograniczania przepustowości po stronie klienta</span><span class="sxs-lookup"><span data-stu-id="df661-123">Recommended client-side throttling method</span></span>

<span data-ttu-id="df661-124">Na kod błędu HTTP 429 Rozpocznij ograniczanie klienta przy użyciu podejścia wykładniczego wycofywania:</span><span class="sxs-lookup"><span data-stu-id="df661-124">On HTTP error code 429, begin throttling your client using an exponential backoff approach:</span></span>

1. <span data-ttu-id="df661-125">Poczekaj 1 sekundę, ponów próbę wykonania żądania</span><span class="sxs-lookup"><span data-stu-id="df661-125">Wait 1 second, retry request</span></span>
2. <span data-ttu-id="df661-126">Jeśli nadal ograniczany poczekaj 2 sekundy, ponów próbę wykonania żądania</span><span class="sxs-lookup"><span data-stu-id="df661-126">If still throttled wait 2 seconds, retry request</span></span>
3. <span data-ttu-id="df661-127">Jeśli nadal ograniczany oczekiwania 4 sekundy, ponów próbę wykonania żądania</span><span class="sxs-lookup"><span data-stu-id="df661-127">If still throttled wait 4 seconds, retry request</span></span>
4. <span data-ttu-id="df661-128">Jeśli nadal ograniczany oczekiwania 8 sekund, ponów próbę wykonania żądania</span><span class="sxs-lookup"><span data-stu-id="df661-128">If still throttled wait 8 seconds, retry request</span></span>
5. <span data-ttu-id="df661-129">Jeśli nadal ograniczany oczekiwania w sekundach 16, ponów próbę wykonania żądania</span><span class="sxs-lookup"><span data-stu-id="df661-129">If still throttled wait 16 seconds, retry request</span></span>

<span data-ttu-id="df661-130">W tym momencie możesz powinien nie uzyskać kody odpowiedzi HTTP 429.</span><span class="sxs-lookup"><span data-stu-id="df661-130">At this point, you should not be getting HTTP 429 response codes.</span></span>

## <a name="see-also"></a><span data-ttu-id="df661-131">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="df661-131">See also</span></span>

<span data-ttu-id="df661-132">Uzyskać lepszy orientacji ograniczania przepustowości na powitania Microsoft Cloud, zobacz [ograniczania wzorzec](https://docs.microsoft.com/azure/architecture/patterns/throttling).</span><span class="sxs-lookup"><span data-stu-id="df661-132">For a deeper orientation of throttling on hello Microsoft Cloud, see [Throttling Pattern](https://docs.microsoft.com/azure/architecture/patterns/throttling).</span></span>

