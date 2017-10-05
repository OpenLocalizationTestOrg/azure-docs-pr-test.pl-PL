---
title: "Obsługa protokołu HTTP/2 w usłudze Azure CDN | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat obsługi protokołu HTTP/2 i CDN."
services: cdn
documentationcenter: 
author: lichard
manager: erikre
editor: 
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 5/04/2017
ms.author: rli
ms.openlocfilehash: 4f8dd685c3ae89535217d7a17a01c5129ca7e6e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="http2-support-in-azure-cdn"></a><span data-ttu-id="d4ec6-103">Obsługa protokołu HTTP/2 w usługi Azure CDN</span><span class="sxs-lookup"><span data-stu-id="d4ec6-103">HTTP/2 Support in Azure CDN</span></span>

<span data-ttu-id="d4ec6-104">HTTP/2 jest znaczne zmiany do HTTP/1.1\.</span><span class="sxs-lookup"><span data-stu-id="d4ec6-104">HTTP/2 is a major revision to HTTP/1.1\.</span></span> <span data-ttu-id="d4ec6-105">Zapewnia szybszy wydajności sieci web, czas odpowiedzi obniżona i lepsze środowisko, przy zachowaniu znanych metod HTTP, kodów stanu i semantyki.</span><span class="sxs-lookup"><span data-stu-id="d4ec6-105">It provides faster web performance, reduced response time, and improved user experience, while maintaining the familiar HTTP methods, status codes, and semantics.</span></span> <span data-ttu-id="d4ec6-106">Chociaż HTTP/2 jest przeznaczony do pracy z protokołów HTTP i HTTPS, wiele przeglądarek sieci web klienta obsługują tylko HTTP/2 za pośrednictwem protokołu TLS.</span><span class="sxs-lookup"><span data-stu-id="d4ec6-106">Though HTTP/2 is designed to work with HTTP and HTTPS, many client web browsers only support HTTP/2 over TLS.</span></span>

###<a name="http2-benefits"></a><span data-ttu-id="d4ec6-107">Korzyści HTTP/2</span><span class="sxs-lookup"><span data-stu-id="d4ec6-107">HTTP/2 Benefits</span></span>

<span data-ttu-id="d4ec6-108">Zalety HTTP/2:</span><span class="sxs-lookup"><span data-stu-id="d4ec6-108">The benefits of HTTP/2 include:</span></span>

*   <span data-ttu-id="d4ec6-109">**Multipleksowanie i współbieżność**</span><span class="sxs-lookup"><span data-stu-id="d4ec6-109">**Multiplexing and concurrency**</span></span>

    <span data-ttu-id="d4ec6-110">Przy użyciu protokołu HTTP 1.1, wielu wprowadzania wielu żądań zasobów wymaga wielu połączeń TCP, a każde połączenie ma zmniejszenie wydajności związane z nią.</span><span class="sxs-lookup"><span data-stu-id="d4ec6-110">Using HTTP 1.1, multiple making multiple resource requests requires multiple TCP connections, and each connection has performance overhead associated with it.</span></span> <span data-ttu-id="d4ec6-111">HTTP/2 umożliwia wielu zasobów wymagane dla pojedynczego połączenia TCP.</span><span class="sxs-lookup"><span data-stu-id="d4ec6-111">HTTP/2 allows multiple resources to be requested on a single TCP connection.</span></span>

*   <span data-ttu-id="d4ec6-112">**Kompresja nagłówka**</span><span class="sxs-lookup"><span data-stu-id="d4ec6-112">**Header compression**</span></span>

    <span data-ttu-id="d4ec6-113">Przez kompresowanie nagłówków HTTP obsługiwane zasobów, czas przesyłania jest znacznie ograniczony.</span><span class="sxs-lookup"><span data-stu-id="d4ec6-113">By compressing the HTTP headers for served resources, time on the wire is reduced significantly.</span></span>

*   <span data-ttu-id="d4ec6-114">**Zależności strumienia**</span><span class="sxs-lookup"><span data-stu-id="d4ec6-114">**Stream dependencies**</span></span>

    <span data-ttu-id="d4ec6-115">Zależności strumienia pozwalają klientowi wskazują na serwer, którego zasoby mają priorytet.</span><span class="sxs-lookup"><span data-stu-id="d4ec6-115">Stream dependencies allow the client to indicate to the server which of resources have priority.</span></span>


##<a name="http2-browser-support"></a><span data-ttu-id="d4ec6-116">Obsługa przeglądarek HTTP/2</span><span class="sxs-lookup"><span data-stu-id="d4ec6-116">HTTP/2 Browser Support</span></span>

<span data-ttu-id="d4ec6-117">Wszystkie główne przeglądarki wdrożono Obsługa HTTP/2 w ich bieżącej wersji.</span><span class="sxs-lookup"><span data-stu-id="d4ec6-117">All of the major browsers have implemented HTTP/2 support in their current versions.</span></span> <span data-ttu-id="d4ec6-118">Nieobsługiwany przeglądarki zostanie automatycznie powrotu do HTTP/1.1.</span><span class="sxs-lookup"><span data-stu-id="d4ec6-118">Non-supported browsers will automatically fallback to HTTP/1.1.</span></span>

|<span data-ttu-id="d4ec6-119">Przeglądarka</span><span class="sxs-lookup"><span data-stu-id="d4ec6-119">Browser</span></span>|<span data-ttu-id="d4ec6-120">Minimalna wersja</span><span class="sxs-lookup"><span data-stu-id="d4ec6-120">Minimum Version</span></span>|
|-------------|------------|
|<span data-ttu-id="d4ec6-121">Przeglądarka Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="d4ec6-121">Microsoft Edge</span></span>| <span data-ttu-id="d4ec6-122">12</span><span class="sxs-lookup"><span data-stu-id="d4ec6-122">12</span></span>|
|<span data-ttu-id="d4ec6-123">Google Chrome</span><span class="sxs-lookup"><span data-stu-id="d4ec6-123">Google Chrome</span></span>| <span data-ttu-id="d4ec6-124">43</span><span class="sxs-lookup"><span data-stu-id="d4ec6-124">43</span></span>|
|<span data-ttu-id="d4ec6-125">Mozilla Firefox</span><span class="sxs-lookup"><span data-stu-id="d4ec6-125">Mozilla Firefox</span></span>| <span data-ttu-id="d4ec6-126">38</span><span class="sxs-lookup"><span data-stu-id="d4ec6-126">38</span></span>|
|<span data-ttu-id="d4ec6-127">Opera</span><span class="sxs-lookup"><span data-stu-id="d4ec6-127">Opera</span></span>| <span data-ttu-id="d4ec6-128">32</span><span class="sxs-lookup"><span data-stu-id="d4ec6-128">32</span></span>|
|<span data-ttu-id="d4ec6-129">Safari</span><span class="sxs-lookup"><span data-stu-id="d4ec6-129">Safari</span></span>| <span data-ttu-id="d4ec6-130">9</span><span class="sxs-lookup"><span data-stu-id="d4ec6-130">9</span></span>|

##<a name="enabling-http2-support-in-azure-cdn"></a><span data-ttu-id="d4ec6-131">Włączanie obsługi protokołu HTTP/2 w Azure CDN</span><span class="sxs-lookup"><span data-stu-id="d4ec6-131">Enabling HTTP/2 Support in Azure CDN</span></span>

<span data-ttu-id="d4ec6-132">Obsługa protokołu HTTP/2 jest obecnie aktywny dla **Azure CDN from Akamai** i **Azure CDN from Verizon** profilów.</span><span class="sxs-lookup"><span data-stu-id="d4ec6-132">Currently HTTP/2 support is active for **Azure CDN from Akamai** and **Azure CDN from Verizon** profiles.</span></span> <span data-ttu-id="d4ec6-133">Żadne dalsze akcje nie jest wymagana od klientów.</span><span class="sxs-lookup"><span data-stu-id="d4ec6-133">No further action is required from customers.</span></span>

##<a name="next-steps"></a><span data-ttu-id="d4ec6-134">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d4ec6-134">Next Steps</span></span>

<span data-ttu-id="d4ec6-135">Aby zapoznać się z zalet HTTP/2 w akcji, zobacz [ten pokaz from Akamai](https://http2.akamai.com/demo).</span><span class="sxs-lookup"><span data-stu-id="d4ec6-135">To see the benefits of HTTP/2 in action, see [this demo from Akamai](https://http2.akamai.com/demo).</span></span>

<span data-ttu-id="d4ec6-136">Aby dowiedzieć się więcej na temat protokołu HTTP/2, można znaleźć w następujących zasobach:</span><span class="sxs-lookup"><span data-stu-id="d4ec6-136">To learn more about HTTP/2, visit the following resources:</span></span>

*   [<span data-ttu-id="d4ec6-137">Strona główna specyfikacji HTTP/2</span><span class="sxs-lookup"><span data-stu-id="d4ec6-137">HTTP/2 specification homepage</span></span>](https://http2.github.io/)
*   [<span data-ttu-id="d4ec6-138">Oficjalna HTTP/2 — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="d4ec6-138">Official HTTP/2 FAQ</span></span>](https://http2.github.io/faq/)
*   [<span data-ttu-id="d4ec6-139">Informacje o Akamai HTTP/2</span><span class="sxs-lookup"><span data-stu-id="d4ec6-139">Akamai HTTP/2 information</span></span>](https://http2.akamai.com/)

<span data-ttu-id="d4ec6-140">Aby dowiedzieć się więcej na temat dostępnych funkcji usługi Azure CDN, zobacz [Omówienie usługi Azure CDN](https://azure.microsoft.com/documentation/articles/cdn-overview/).</span><span class="sxs-lookup"><span data-stu-id="d4ec6-140">To learn more about Azure CDN's available features, see the [Azure CDN Overview](https://azure.microsoft.com/documentation/articles/cdn-overview/).</span></span>