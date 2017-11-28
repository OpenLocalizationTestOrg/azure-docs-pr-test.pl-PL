---
title: "Obsługa aaaHTTP/2 w usłudze Azure CDN | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 2e5e5345e8cf5c40e080ebf18b4f13a239a5aac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="http2-support-in-azure-cdn"></a><span data-ttu-id="d6349-103">Obsługa protokołu HTTP/2 w usługi Azure CDN</span><span class="sxs-lookup"><span data-stu-id="d6349-103">HTTP/2 Support in Azure CDN</span></span>

<span data-ttu-id="d6349-104">HTTP/2 jest tooHTTP/1.1\ znaczne zmiany.</span><span class="sxs-lookup"><span data-stu-id="d6349-104">HTTP/2 is a major revision tooHTTP/1.1\.</span></span> <span data-ttu-id="d6349-105">Zapewnia szybszy wydajności sieci web, czas odpowiedzi obniżona i lepsze środowisko, przy zachowaniu semantyki hello znanych metod HTTP i kodów stanu.</span><span class="sxs-lookup"><span data-stu-id="d6349-105">It provides faster web performance, reduced response time, and improved user experience, while maintaining hello familiar HTTP methods, status codes, and semantics.</span></span> <span data-ttu-id="d6349-106">Chociaż HTTP/2 jest zaprojektowana toowork z protokołów HTTP i HTTPS, wiele przeglądarek sieci web klienta obsługują tylko HTTP/2 za pośrednictwem protokołu TLS.</span><span class="sxs-lookup"><span data-stu-id="d6349-106">Though HTTP/2 is designed toowork with HTTP and HTTPS, many client web browsers only support HTTP/2 over TLS.</span></span>

###<a name="http2-benefits"></a><span data-ttu-id="d6349-107">Korzyści HTTP/2</span><span class="sxs-lookup"><span data-stu-id="d6349-107">HTTP/2 Benefits</span></span>

<span data-ttu-id="d6349-108">Witaj HTTP/2 zalety:</span><span class="sxs-lookup"><span data-stu-id="d6349-108">hello benefits of HTTP/2 include:</span></span>

*   <span data-ttu-id="d6349-109">**Multipleksowanie i współbieżność**</span><span class="sxs-lookup"><span data-stu-id="d6349-109">**Multiplexing and concurrency**</span></span>

    <span data-ttu-id="d6349-110">Przy użyciu protokołu HTTP 1.1, wielu wprowadzania wielu żądań zasobów wymaga wielu połączeń TCP, a każde połączenie ma zmniejszenie wydajności związane z nią.</span><span class="sxs-lookup"><span data-stu-id="d6349-110">Using HTTP 1.1, multiple making multiple resource requests requires multiple TCP connections, and each connection has performance overhead associated with it.</span></span> <span data-ttu-id="d6349-111">HTTP/2 umożliwia wielu toobe zasobów żądana pojedynczego połączenia TCP.</span><span class="sxs-lookup"><span data-stu-id="d6349-111">HTTP/2 allows multiple resources toobe requested on a single TCP connection.</span></span>

*   <span data-ttu-id="d6349-112">**Kompresja nagłówka**</span><span class="sxs-lookup"><span data-stu-id="d6349-112">**Header compression**</span></span>

    <span data-ttu-id="d6349-113">Przez kompresowanie nagłówki hello HTTP obsługiwane zasobów, czas umieszczonego hello jest znacznie ograniczony.</span><span class="sxs-lookup"><span data-stu-id="d6349-113">By compressing hello HTTP headers for served resources, time on hello wire is reduced significantly.</span></span>

*   <span data-ttu-id="d6349-114">**Zależności strumienia**</span><span class="sxs-lookup"><span data-stu-id="d6349-114">**Stream dependencies**</span></span>

    <span data-ttu-id="d6349-115">Zależności strumienia Zezwalaj powitania klienta serwer toohello tooindicate, którego zasoby mają priorytet.</span><span class="sxs-lookup"><span data-stu-id="d6349-115">Stream dependencies allow hello client tooindicate toohello server which of resources have priority.</span></span>


##<a name="http2-browser-support"></a><span data-ttu-id="d6349-116">Obsługa przeglądarek HTTP/2</span><span class="sxs-lookup"><span data-stu-id="d6349-116">HTTP/2 Browser Support</span></span>

<span data-ttu-id="d6349-117">Wszystkie główne przeglądarki hello wdrożono Obsługa HTTP/2 w ich bieżącej wersji.</span><span class="sxs-lookup"><span data-stu-id="d6349-117">All of hello major browsers have implemented HTTP/2 support in their current versions.</span></span> <span data-ttu-id="d6349-118">Nieobsługiwany przeglądarki zostanie automatycznie rezerwowy tooHTTP/1.1.</span><span class="sxs-lookup"><span data-stu-id="d6349-118">Non-supported browsers will automatically fallback tooHTTP/1.1.</span></span>

|<span data-ttu-id="d6349-119">Przeglądarka</span><span class="sxs-lookup"><span data-stu-id="d6349-119">Browser</span></span>|<span data-ttu-id="d6349-120">Minimalna wersja</span><span class="sxs-lookup"><span data-stu-id="d6349-120">Minimum Version</span></span>|
|-------------|------------|
|<span data-ttu-id="d6349-121">Przeglądarka Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="d6349-121">Microsoft Edge</span></span>| <span data-ttu-id="d6349-122">12</span><span class="sxs-lookup"><span data-stu-id="d6349-122">12</span></span>|
|<span data-ttu-id="d6349-123">Google Chrome</span><span class="sxs-lookup"><span data-stu-id="d6349-123">Google Chrome</span></span>| <span data-ttu-id="d6349-124">43</span><span class="sxs-lookup"><span data-stu-id="d6349-124">43</span></span>|
|<span data-ttu-id="d6349-125">Mozilla Firefox</span><span class="sxs-lookup"><span data-stu-id="d6349-125">Mozilla Firefox</span></span>| <span data-ttu-id="d6349-126">38</span><span class="sxs-lookup"><span data-stu-id="d6349-126">38</span></span>|
|<span data-ttu-id="d6349-127">Opera</span><span class="sxs-lookup"><span data-stu-id="d6349-127">Opera</span></span>| <span data-ttu-id="d6349-128">32</span><span class="sxs-lookup"><span data-stu-id="d6349-128">32</span></span>|
|<span data-ttu-id="d6349-129">Safari</span><span class="sxs-lookup"><span data-stu-id="d6349-129">Safari</span></span>| <span data-ttu-id="d6349-130">9</span><span class="sxs-lookup"><span data-stu-id="d6349-130">9</span></span>|

##<a name="enabling-http2-support-in-azure-cdn"></a><span data-ttu-id="d6349-131">Włączanie obsługi protokołu HTTP/2 w Azure CDN</span><span class="sxs-lookup"><span data-stu-id="d6349-131">Enabling HTTP/2 Support in Azure CDN</span></span>

<span data-ttu-id="d6349-132">Obsługa protokołu HTTP/2 jest obecnie aktywny dla **Azure CDN from Akamai** i **Azure CDN from Verizon** profilów.</span><span class="sxs-lookup"><span data-stu-id="d6349-132">Currently HTTP/2 support is active for **Azure CDN from Akamai** and **Azure CDN from Verizon** profiles.</span></span> <span data-ttu-id="d6349-133">Żadne dalsze akcje nie jest wymagana od klientów.</span><span class="sxs-lookup"><span data-stu-id="d6349-133">No further action is required from customers.</span></span>

##<a name="next-steps"></a><span data-ttu-id="d6349-134">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d6349-134">Next Steps</span></span>

<span data-ttu-id="d6349-135">Zalety hello toosee HTTP/2 akcji, zobacz [ten pokaz from Akamai](https://http2.akamai.com/demo).</span><span class="sxs-lookup"><span data-stu-id="d6349-135">toosee hello benefits of HTTP/2 in action, see [this demo from Akamai](https://http2.akamai.com/demo).</span></span>

<span data-ttu-id="d6349-136">toolearn więcej informacji na temat protokołu HTTP/2, odwiedź hello następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="d6349-136">toolearn more about HTTP/2, visit hello following resources:</span></span>

*   [<span data-ttu-id="d6349-137">Strona główna specyfikacji HTTP/2</span><span class="sxs-lookup"><span data-stu-id="d6349-137">HTTP/2 specification homepage</span></span>](https://http2.github.io/)
*   [<span data-ttu-id="d6349-138">Oficjalna HTTP/2 — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="d6349-138">Official HTTP/2 FAQ</span></span>](https://http2.github.io/faq/)
*   [<span data-ttu-id="d6349-139">Informacje o Akamai HTTP/2</span><span class="sxs-lookup"><span data-stu-id="d6349-139">Akamai HTTP/2 information</span></span>](https://http2.akamai.com/)

<span data-ttu-id="d6349-140">toolearn więcej informacji na temat dostępnych funkcji usługi Azure CDN, zobacz hello [Omówienie usługi Azure CDN](https://azure.microsoft.com/documentation/articles/cdn-overview/).</span><span class="sxs-lookup"><span data-stu-id="d6349-140">toolearn more about Azure CDN's available features, see hello [Azure CDN Overview](https://azure.microsoft.com/documentation/articles/cdn-overview/).</span></span>
