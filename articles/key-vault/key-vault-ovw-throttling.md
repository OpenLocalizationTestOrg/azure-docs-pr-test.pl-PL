---
ms.assetid: 
title: "Usługa Azure Key Vault ograniczania wskazówki | Dokumentacja firmy Microsoft"
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 06/21/2017
ms.openlocfilehash: fe700e22c5323c2a0bdc315e349cd119798bcf40
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-key-vault-throttling-guidance"></a><span data-ttu-id="04fcc-102">Usługa Azure Key Vault ograniczania wskazówki</span><span class="sxs-lookup"><span data-stu-id="04fcc-102">Azure Key Vault throttling guidance</span></span>

<span data-ttu-id="04fcc-103">Ograniczanie jest procesem zainicjowanych przez ograniczenie liczby równoczesnych wywołań do usługi Azure, aby uniemożliwić nadużycia zasobów.</span><span class="sxs-lookup"><span data-stu-id="04fcc-103">Throttling is a process you initiate that limits the number of concurrent calls to the Azure service to prevent overuse of resources.</span></span> <span data-ttu-id="04fcc-104">Magazyn kluczy Azure (AKV) jest przeznaczona do obsługi dużej liczby żądań.</span><span class="sxs-lookup"><span data-stu-id="04fcc-104">Azure Key Vault (AKV) is designed to handle a high volume of requests.</span></span> <span data-ttu-id="04fcc-105">W przypadku utrudnione liczba żądań ograniczanie żądań klienta pomaga utrzymać optymalną wydajność i niezawodność AKV usługi.</span><span class="sxs-lookup"><span data-stu-id="04fcc-105">If an overwhelming number of requests occurs, throttling your client's requests helps maintain optimal performance and reliability of the AKV service.</span></span>

<span data-ttu-id="04fcc-106">Limity ograniczania przepustowości różnić w zależności od scenariusza.</span><span class="sxs-lookup"><span data-stu-id="04fcc-106">Throttling limits vary based on the scenario.</span></span> <span data-ttu-id="04fcc-107">Na przykład jeśli przeprowadzasz dużą liczbę operacji zapisu, możliwość ograniczania jest wyższa niż jeśli tylko wykonywana odczytów.</span><span class="sxs-lookup"><span data-stu-id="04fcc-107">For example, if you are performing a large volume of writes, the possibility for throttling is higher than if you are only performing reads.</span></span>

## <a name="how-does-key-vault-handle-its-limits"></a><span data-ttu-id="04fcc-108">Jak usługi Key Vault obsługuje limit?</span><span class="sxs-lookup"><span data-stu-id="04fcc-108">How does Key Vault handle its limits?</span></span>

<span data-ttu-id="04fcc-109">Ograniczenia usługi Key Vault istnieją uniemożliwić nadużycia zasobów i zapewnienia jakości usług dla wszystkich klientów usługi Key Vault.</span><span class="sxs-lookup"><span data-stu-id="04fcc-109">Service limits in Key Vault are there to prevent misuse of resources and ensure quality of service for all of Key Vault’s clients.</span></span> <span data-ttu-id="04fcc-110">Po przekroczeniu progu usługi Key Vault ogranicza żadnych dalszych żądań z tego klienta w danym okresie czasu.</span><span class="sxs-lookup"><span data-stu-id="04fcc-110">When a service threshold is exceeded, Key Vault limits any further requests from that client for a period of time.</span></span> <span data-ttu-id="04fcc-111">W takim przypadku magazyn kluczy zwraca kod stanu HTTP 429 (zbyt wiele żądań), i Niepowodzenie żądania.</span><span class="sxs-lookup"><span data-stu-id="04fcc-111">When this happens, Key Vault returns HTTP status code 429 (Too many requests), and the requests fail.</span></span> <span data-ttu-id="04fcc-112">Ponadto nie żądań zwracających 429 liczba kierunku limity przepustowości śledzone przez magazyn kluczy.</span><span class="sxs-lookup"><span data-stu-id="04fcc-112">Also, failed requests that return a 429 count towards the throttle limits tracked by Key Vault.</span></span> 

<span data-ttu-id="04fcc-113">Jeśli masz prawidłowe firm przypadku wyższe limity przepustowości, skontaktuj się z nami.</span><span class="sxs-lookup"><span data-stu-id="04fcc-113">If you have a valid business case for higher throttle limits, please contact us.</span></span>


## <a name="how-to-throttle-your-app-in-response-to-service-limits"></a><span data-ttu-id="04fcc-114">Ograniczania aplikacji w odpowiedzi na ograniczenia usługi</span><span class="sxs-lookup"><span data-stu-id="04fcc-114">How to throttle your app in response to service limits</span></span>

<span data-ttu-id="04fcc-115">Poniżej przedstawiono **najlepsze rozwiązania** dla ograniczania aplikacji:</span><span class="sxs-lookup"><span data-stu-id="04fcc-115">The following are **best practices** for throttling your app:</span></span>
- <span data-ttu-id="04fcc-116">Zmniejsz liczbę operacji na żądanie.</span><span class="sxs-lookup"><span data-stu-id="04fcc-116">Reduce the number of operations per request.</span></span>
- <span data-ttu-id="04fcc-117">Zmniejsz częstotliwość żądań.</span><span class="sxs-lookup"><span data-stu-id="04fcc-117">Reduce the frequency of requests.</span></span>
- <span data-ttu-id="04fcc-118">Należy unikać bezpośredniego ponownych prób.</span><span class="sxs-lookup"><span data-stu-id="04fcc-118">Avoid immediate retries.</span></span> 
    - <span data-ttu-id="04fcc-119">Wszystkie żądania są naliczane względem limitów do użycia.</span><span class="sxs-lookup"><span data-stu-id="04fcc-119">All requests accrue against your usage limits.</span></span>

<span data-ttu-id="04fcc-120">Podczas implementowania obsługi błędów aplikacji umożliwia kod błędu HTTP 429 wykrywać ograniczania po stronie klienta.</span><span class="sxs-lookup"><span data-stu-id="04fcc-120">When you implement your app's error handling, use the HTTP error code 429 to detect the need for client-side throttling.</span></span> <span data-ttu-id="04fcc-121">Jeśli żądanie nie powiedzie się ponownie z kodem błędu HTTP 429, pojawiły się nadal limit usług Azure.</span><span class="sxs-lookup"><span data-stu-id="04fcc-121">If the request fails again with an HTTP 429 error code, you are still encountering an Azure service limit.</span></span> <span data-ttu-id="04fcc-122">Nadal używać zalecane po stronie klienta ograniczania metody, ponowienie do skutku.</span><span class="sxs-lookup"><span data-stu-id="04fcc-122">Continue to use the recommended client-side throttling method, retrying the request until it succeeds.</span></span>

### <a name="recommended-client-side-throttling-method"></a><span data-ttu-id="04fcc-123">Zalecana metoda ograniczania przepustowości po stronie klienta</span><span class="sxs-lookup"><span data-stu-id="04fcc-123">Recommended client-side throttling method</span></span>

<span data-ttu-id="04fcc-124">Na kod błędu HTTP 429 Rozpocznij ograniczanie klienta przy użyciu podejścia wykładniczego wycofywania:</span><span class="sxs-lookup"><span data-stu-id="04fcc-124">On HTTP error code 429, begin throttling your client using an exponential backoff approach:</span></span>

1. <span data-ttu-id="04fcc-125">Poczekaj 1 sekundę, ponów próbę wykonania żądania</span><span class="sxs-lookup"><span data-stu-id="04fcc-125">Wait 1 second, retry request</span></span>
2. <span data-ttu-id="04fcc-126">Jeśli nadal ograniczany poczekaj 2 sekundy, ponów próbę wykonania żądania</span><span class="sxs-lookup"><span data-stu-id="04fcc-126">If still throttled wait 2 seconds, retry request</span></span>
3. <span data-ttu-id="04fcc-127">Jeśli nadal ograniczany oczekiwania 4 sekundy, ponów próbę wykonania żądania</span><span class="sxs-lookup"><span data-stu-id="04fcc-127">If still throttled wait 4 seconds, retry request</span></span>
4. <span data-ttu-id="04fcc-128">Jeśli nadal ograniczany oczekiwania 8 sekund, ponów próbę wykonania żądania</span><span class="sxs-lookup"><span data-stu-id="04fcc-128">If still throttled wait 8 seconds, retry request</span></span>
5. <span data-ttu-id="04fcc-129">Jeśli nadal ograniczany oczekiwania w sekundach 16, ponów próbę wykonania żądania</span><span class="sxs-lookup"><span data-stu-id="04fcc-129">If still throttled wait 16 seconds, retry request</span></span>

<span data-ttu-id="04fcc-130">W tym momencie możesz powinien nie uzyskać kody odpowiedzi HTTP 429.</span><span class="sxs-lookup"><span data-stu-id="04fcc-130">At this point, you should not be getting HTTP 429 response codes.</span></span>

## <a name="see-also"></a><span data-ttu-id="04fcc-131">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="04fcc-131">See also</span></span>

<span data-ttu-id="04fcc-132">Uzyskać lepszy orientacji ograniczania przepustowości w Microsoft Cloud, zobacz [ograniczania wzorzec](https://docs.microsoft.com/azure/architecture/patterns/throttling).</span><span class="sxs-lookup"><span data-stu-id="04fcc-132">For a deeper orientation of throttling on the Microsoft Cloud, see [Throttling Pattern](https://docs.microsoft.com/azure/architecture/patterns/throttling).</span></span>

