---
title: "Monitorowanie aplikacji w usłudze Azure App Service | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak monitorować aplikacje w usłudze Azure App Service przy użyciu portalu Azure."
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: d273da4e-07de-48e0-b99d-4020d84a425e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/07/2016
ms.author: byvinyal
ms.openlocfilehash: 25d3776920d683fffedcd8ac6ed0e84dfe875974
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-monitor-apps-in-azure-app-service"></a><span data-ttu-id="2c27b-103">Porady: monitorować aplikacje w usłudze aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="2c27b-103">How to: Monitor Apps in Azure App Service</span></span>
<span data-ttu-id="2c27b-104">[Usługi aplikacji](http://go.microsoft.com/fwlink/?LinkId=529714) oferuje wbudowane funkcje monitorowania w [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2c27b-104">[App Service](http://go.microsoft.com/fwlink/?LinkId=529714) provides built in monitoring functionality in the [Azure Portal](https://portal.azure.com).</span></span>
<span data-ttu-id="2c27b-105">Obejmuje to możliwość Przejrzyj **przydziały** i **metryki** dla aplikacji, a także plan usługi aplikacji, ustawianie **alerty** i nawet **skalowanie**automatycznie w oparciu o te metryki.</span><span class="sxs-lookup"><span data-stu-id="2c27b-105">This includes the ability to review **quotas** and **metrics** for an app as well as the App Service plan, setting up **alerts** and even **scaling** automatically based on these metrics.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="understanding-quotas-and-metrics"></a><span data-ttu-id="2c27b-106">Opis przydziałów i metryki</span><span class="sxs-lookup"><span data-stu-id="2c27b-106">Understanding Quotas and Metrics</span></span>
### <a name="quotas"></a><span data-ttu-id="2c27b-107">Przydziały</span><span class="sxs-lookup"><span data-stu-id="2c27b-107">Quotas</span></span>
<span data-ttu-id="2c27b-108">Aplikacje hostowane w usłudze App Service podlegają niektórych *limity* z użyciem zasobów.</span><span class="sxs-lookup"><span data-stu-id="2c27b-108">Applications hosted in App Service are subject to certain *limits* on the resources they can use.</span></span> <span data-ttu-id="2c27b-109">Wynika z limitów **planu usługi aplikacji** skojarzone z aplikacją.</span><span class="sxs-lookup"><span data-stu-id="2c27b-109">The limits are defined by the **App Service plan** associated with the app.</span></span>

<span data-ttu-id="2c27b-110">Jeśli aplikacja jest hostowana w **wolne** lub **Shared** planowanie, a następnie wynika z ograniczenia zasobów, aplikacja może używać **przydziały**.</span><span class="sxs-lookup"><span data-stu-id="2c27b-110">If the application is hosted in a **Free** or **Shared** plan, then the limits on the resources the app can use are defined by **Quotas**.</span></span>

<span data-ttu-id="2c27b-111">Jeśli aplikacja jest hostowana w **podstawowe**, **standardowe** lub **Premium** planowanie, a następnie limity mogą używać zasoby są ustawiane przez **rozmiar**(Mały, Średni, duża) i **wystąpienia licznika** (1, 2, 3,...) z **planu usługi aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="2c27b-111">If the application is hosted in a **Basic**, **Standard** or **Premium** plan, then the limits on the resources they can use are set by the **size** (Small, Medium, Large) and **instance count** (1, 2, 3, ...) of the **App Service plan**.</span></span>

<span data-ttu-id="2c27b-112">**Przydziały** dla **wolne** lub **Shared** aplikacje są:</span><span class="sxs-lookup"><span data-stu-id="2c27b-112">**Quotas** for **Free** or **Shared** apps are:</span></span>

* <span data-ttu-id="2c27b-113">**CPU(Short)**</span><span class="sxs-lookup"><span data-stu-id="2c27b-113">**CPU(Short)**</span></span>
  * <span data-ttu-id="2c27b-114">Ilość Procesora dozwolone dla tej aplikacji w 5 minut.</span><span class="sxs-lookup"><span data-stu-id="2c27b-114">Amount of CPU allowed for this application in a 5-minute interval.</span></span> <span data-ttu-id="2c27b-115">Ten limit przydziału ustawia ponownie co 5 minut.</span><span class="sxs-lookup"><span data-stu-id="2c27b-115">This quota re-sets every 5 minutes.</span></span>
* <span data-ttu-id="2c27b-116">**CPU(Day)**</span><span class="sxs-lookup"><span data-stu-id="2c27b-116">**CPU(Day)**</span></span>
  * <span data-ttu-id="2c27b-117">Całkowita ilość Procesora dozwolone dla tej aplikacji w ciągu jednego dnia.</span><span class="sxs-lookup"><span data-stu-id="2c27b-117">Total amount of CPU allowed for this application in a day.</span></span> <span data-ttu-id="2c27b-118">Ten limit przydziału ustawia ponownie co 24 godziny, o północy czasu UTC.</span><span class="sxs-lookup"><span data-stu-id="2c27b-118">This quota re-sets every 24 hours at midnight UTC.</span></span>
* <span data-ttu-id="2c27b-119">**Pamięci**</span><span class="sxs-lookup"><span data-stu-id="2c27b-119">**Memory**</span></span>
  * <span data-ttu-id="2c27b-120">Całkowita ilość pamięci dozwolone dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2c27b-120">Total amount of memory allowed for this application.</span></span>
* <span data-ttu-id="2c27b-121">**Przepustowość**</span><span class="sxs-lookup"><span data-stu-id="2c27b-121">**Bandwidth**</span></span>
  * <span data-ttu-id="2c27b-122">Całkowita ilość przepustowości wychodzącej dozwolone dla tej aplikacji w ciągu jednego dnia.</span><span class="sxs-lookup"><span data-stu-id="2c27b-122">Total amount of outgoing bandwidth allowed for this application in a day.</span></span>
    <span data-ttu-id="2c27b-123">Ten limit przydziału ustawia ponownie co 24 godziny, o północy czasu UTC.</span><span class="sxs-lookup"><span data-stu-id="2c27b-123">This quota re-sets every 24 hours at midnight UTC.</span></span>
* <span data-ttu-id="2c27b-124">**System plików**</span><span class="sxs-lookup"><span data-stu-id="2c27b-124">**Filesystem**</span></span>
  * <span data-ttu-id="2c27b-125">Całkowita liczba dozwoloną ilość pamięci masowej.</span><span class="sxs-lookup"><span data-stu-id="2c27b-125">Total amount of storage allowed.</span></span>

<span data-ttu-id="2c27b-126">Tylko przydział stosowane w aplikacjach hostowanych na **podstawowe**, **standardowe** i **Premium** jest planów **Filesystem**.</span><span class="sxs-lookup"><span data-stu-id="2c27b-126">The only quota applicable to apps hosted on **Basic**, **Standard** and **Premium** plans is **Filesystem**.</span></span>

<span data-ttu-id="2c27b-127">Więcej informacji na temat określonych przydziałów, ograniczenia i funkcje dostępne dla różnych jednostki SKU usługi aplikacji można znaleźć tutaj: [ograniczenia usługi subskrypcji platformy Azure](../azure-subscription-service-limits.md#app-service-limits)</span><span class="sxs-lookup"><span data-stu-id="2c27b-127">More information about the specific quotas, limits and features available to the different App Service SKUs can be found here: [Azure Subscription Service Limits](../azure-subscription-service-limits.md#app-service-limits)</span></span>

#### <a name="quota-enforcement"></a><span data-ttu-id="2c27b-128">Wymuszanie przydziałów</span><span class="sxs-lookup"><span data-stu-id="2c27b-128">Quota Enforcement</span></span>
<span data-ttu-id="2c27b-129">Jeśli aplikacja w jej użycie przekracza **procesora CPU (short)**, **procesora CPU (dzień)**, lub **przepustowości** przydziału, a następnie aplikacji zostanie zatrzymana, aż do ponownego ustawia limit przydziału.</span><span class="sxs-lookup"><span data-stu-id="2c27b-129">If an application in its usage exceeds the **CPU (short)**, **CPU (Day)**, or **bandwidth** quota then the application will be stopped until the quota re-sets.</span></span> <span data-ttu-id="2c27b-130">W tym czasie wszystkie żądania przychodzące spowoduje **HTTP 403**.</span><span class="sxs-lookup"><span data-stu-id="2c27b-130">During this time, all incoming requests will result in an **HTTP 403**.</span></span>
![][http403]

<span data-ttu-id="2c27b-131">Jeśli aplikacja **pamięci** przekroczony przydział, a następnie aplikacja zostanie ponownie uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="2c27b-131">If the application **memory** quota is exceeded, then the application will be re-started.</span></span>

<span data-ttu-id="2c27b-132">Jeśli **Filesystem** przekroczony przydział, a następnie żadnego zapisu, operacja zakończy się niepowodzeniem, obejmuje to zapisywanie dzienników.</span><span class="sxs-lookup"><span data-stu-id="2c27b-132">If the **Filesystem** quota is exceeded, then any write operation will fail, this includes writing to logs.</span></span>

<span data-ttu-id="2c27b-133">Przydziały można zwiększyć lub usunięte z aplikacji, uaktualniając plan usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2c27b-133">Quotas can be increased or removed from your app by upgrading your App Service plan.</span></span>

### <a name="metrics"></a><span data-ttu-id="2c27b-134">Metryki</span><span class="sxs-lookup"><span data-stu-id="2c27b-134">Metrics</span></span>
<span data-ttu-id="2c27b-135">**Metryki** zawierają informacje o aplikacji, lub zachowanie planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2c27b-135">**Metrics** provide information about the app, or App Service plan's behavior.</span></span>

<span data-ttu-id="2c27b-136">Aby uzyskać **aplikacji**, są dostępne metryki:</span><span class="sxs-lookup"><span data-stu-id="2c27b-136">For an **Application**, the available metrics are:</span></span>

* <span data-ttu-id="2c27b-137">**Średni czas odpowiedzi**</span><span class="sxs-lookup"><span data-stu-id="2c27b-137">**Average Response Time**</span></span>
  * <span data-ttu-id="2c27b-138">Średni czas dla aplikacji do obsługi żądań w ms.</span><span class="sxs-lookup"><span data-stu-id="2c27b-138">The average time taken for the app to serve requests in ms.</span></span>
* <span data-ttu-id="2c27b-139">**Pamięć średni zestaw roboczy**</span><span class="sxs-lookup"><span data-stu-id="2c27b-139">**Average memory working set**</span></span>
  * <span data-ttu-id="2c27b-140">Średnia ilość pamięci w bazach MIB używany przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="2c27b-140">The average amount of memory in MiBs used by the app.</span></span>
* <span data-ttu-id="2c27b-141">**Czas procesora CPU**</span><span class="sxs-lookup"><span data-stu-id="2c27b-141">**CPU Time**</span></span>
  * <span data-ttu-id="2c27b-142">Ilość Procesora w sekundach używane przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="2c27b-142">The amount of CPU in seconds consumed by the app.</span></span> <span data-ttu-id="2c27b-143">Aby uzyskać więcej informacji o tym, zobacz metryki: [procent vs Procesora czas procesora CPU](#cpu-time-vs-cpu-percentage)</span><span class="sxs-lookup"><span data-stu-id="2c27b-143">For more information about this metric see: [CPU time vs CPU percentage](#cpu-time-vs-cpu-percentage)</span></span>
* <span data-ttu-id="2c27b-144">**Dane w**</span><span class="sxs-lookup"><span data-stu-id="2c27b-144">**Data In**</span></span>
  * <span data-ttu-id="2c27b-145">Ilość przychodzącego przepustowości przez aplikację w bazach MIB.</span><span class="sxs-lookup"><span data-stu-id="2c27b-145">The amount of incoming bandwidth consumed by the app in MiBs.</span></span>
* <span data-ttu-id="2c27b-146">**Dla danych wychodzących**</span><span class="sxs-lookup"><span data-stu-id="2c27b-146">**Data Out**</span></span>
  * <span data-ttu-id="2c27b-147">Liczba wychodzących przepustowości przez aplikację w bazach MIB.</span><span class="sxs-lookup"><span data-stu-id="2c27b-147">The amount of outgoing bandwidth consumed by the app in MiBs.</span></span>
* <span data-ttu-id="2c27b-148">**Http 2xx**</span><span class="sxs-lookup"><span data-stu-id="2c27b-148">**Http 2xx**</span></span>
  * <span data-ttu-id="2c27b-149">Liczba żądań, co powoduje kod stanu http > = 200, ale < 300.</span><span class="sxs-lookup"><span data-stu-id="2c27b-149">Count of requests resulting in a http status code >= 200 but < 300.</span></span>
* <span data-ttu-id="2c27b-150">**Http 3xx**</span><span class="sxs-lookup"><span data-stu-id="2c27b-150">**Http 3xx**</span></span>
  * <span data-ttu-id="2c27b-151">Liczba żądań, co powoduje kod stanu http > = 300, ale < 400.</span><span class="sxs-lookup"><span data-stu-id="2c27b-151">Count of requests resulting in a http status code >= 300 but < 400.</span></span>
* <span data-ttu-id="2c27b-152">**HTTP 401**</span><span class="sxs-lookup"><span data-stu-id="2c27b-152">**Http 401**</span></span>
  * <span data-ttu-id="2c27b-153">Liczba żądań, co powoduje kod stanu HTTP 401.</span><span class="sxs-lookup"><span data-stu-id="2c27b-153">Count of requests resulting in HTTP 401 status code.</span></span>
* <span data-ttu-id="2c27b-154">**HTTP 403**</span><span class="sxs-lookup"><span data-stu-id="2c27b-154">**Http 403**</span></span>
  * <span data-ttu-id="2c27b-155">Liczba żądań, co powoduje kod stanu HTTP 403.</span><span class="sxs-lookup"><span data-stu-id="2c27b-155">Count of requests resulting in HTTP 403 status code.</span></span>
* <span data-ttu-id="2c27b-156">**HTTP 404**</span><span class="sxs-lookup"><span data-stu-id="2c27b-156">**Http 404**</span></span>
  * <span data-ttu-id="2c27b-157">Liczba żądań, co powoduje kod stanu HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="2c27b-157">Count of requests resulting in HTTP 404 status code.</span></span>
* <span data-ttu-id="2c27b-158">**HTTP 406**</span><span class="sxs-lookup"><span data-stu-id="2c27b-158">**Http 406**</span></span>
  * <span data-ttu-id="2c27b-159">Liczba żądań, co powoduje kod stanu HTTP 406.</span><span class="sxs-lookup"><span data-stu-id="2c27b-159">Count of requests resulting in HTTP 406 status code.</span></span>
* <span data-ttu-id="2c27b-160">**Http 4xx**</span><span class="sxs-lookup"><span data-stu-id="2c27b-160">**Http 4xx**</span></span>
  * <span data-ttu-id="2c27b-161">Liczba żądań, co powoduje kod stanu http > = 400, ale < 500.</span><span class="sxs-lookup"><span data-stu-id="2c27b-161">Count of requests resulting in a http status code >= 400 but < 500.</span></span>
* <span data-ttu-id="2c27b-162">**Błędy HTTP serwera**</span><span class="sxs-lookup"><span data-stu-id="2c27b-162">**Http Server Errors**</span></span>
  * <span data-ttu-id="2c27b-163">Liczba żądań, co powoduje kod stanu http > = 500, ale < 600.</span><span class="sxs-lookup"><span data-stu-id="2c27b-163">Count of requests resulting in a http status code >= 500 but < 600.</span></span>
* <span data-ttu-id="2c27b-164">**Zestaw roboczy pamięci**</span><span class="sxs-lookup"><span data-stu-id="2c27b-164">**Memory working set**</span></span>
  * <span data-ttu-id="2c27b-165">Bieżąca ilość pamięci użytej przez aplikację w bazach MIB.</span><span class="sxs-lookup"><span data-stu-id="2c27b-165">Current amount of memory used by the app in MiBs.</span></span>
* <span data-ttu-id="2c27b-166">**Żądania**</span><span class="sxs-lookup"><span data-stu-id="2c27b-166">**Requests**</span></span>
  * <span data-ttu-id="2c27b-167">Całkowita liczba żądań, niezależnie od ich wynikowy kod stanu HTTP.</span><span class="sxs-lookup"><span data-stu-id="2c27b-167">Total number of requests regardless of their resulting HTTP status code.</span></span>

<span data-ttu-id="2c27b-168">Aby uzyskać **planu usługi aplikacji**, są dostępne metryki:</span><span class="sxs-lookup"><span data-stu-id="2c27b-168">For an **App Service plan**, the available metrics are:</span></span>

> [!NOTE]
> <span data-ttu-id="2c27b-169">Metryki planu usługi aplikacji są dostępne tylko dla planów w **podstawowe**, **standardowe** i **Premium** jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="2c27b-169">App Service plan metrics are only available for plans in **Basic**, **Standard** and **Premium** SKU.</span></span>
> 
> 

* <span data-ttu-id="2c27b-170">**Procent użycia procesora CPU**</span><span class="sxs-lookup"><span data-stu-id="2c27b-170">**CPU Percentage**</span></span>
  * <span data-ttu-id="2c27b-171">Średnie wykorzystanie Procesora, używana we wszystkich wystąpieniach planu.</span><span class="sxs-lookup"><span data-stu-id="2c27b-171">The average CPU used across all instances of the plan.</span></span>
* <span data-ttu-id="2c27b-172">**Procent pamięci**</span><span class="sxs-lookup"><span data-stu-id="2c27b-172">**Memory Percentage**</span></span>
  * <span data-ttu-id="2c27b-173">Średnia pamięć używana we wszystkich wystąpieniach planu.</span><span class="sxs-lookup"><span data-stu-id="2c27b-173">The average memory used across all instances of the plan.</span></span>
* <span data-ttu-id="2c27b-174">**Dane w**</span><span class="sxs-lookup"><span data-stu-id="2c27b-174">**Data In**</span></span>
  * <span data-ttu-id="2c27b-175">Średnia przepustowość przychodzące używane we wszystkich wystąpieniach planu.</span><span class="sxs-lookup"><span data-stu-id="2c27b-175">The average incoming bandwidth used across all instances of the plan.</span></span>
* <span data-ttu-id="2c27b-176">**Dla danych wychodzących**</span><span class="sxs-lookup"><span data-stu-id="2c27b-176">**Data Out**</span></span>
  * <span data-ttu-id="2c27b-177">Średnia przepustowość we wszystkich wystąpieniach planu wychodzące.</span><span class="sxs-lookup"><span data-stu-id="2c27b-177">The average outgoing bandwidth used across all instances of the plan.</span></span>
* <span data-ttu-id="2c27b-178">**Długość kolejki dysku**</span><span class="sxs-lookup"><span data-stu-id="2c27b-178">**Disk Queue Length**</span></span>
  * <span data-ttu-id="2c27b-179">Średnia liczba zarówno żądania odczytu i zapisu umieszczonych w kolejce w magazynie.</span><span class="sxs-lookup"><span data-stu-id="2c27b-179">The average number of both read and write requests that were queued on storage.</span></span> <span data-ttu-id="2c27b-180">Długość kolejki dysku będzie wskazywać aplikacji, która może być spowolnieniem z powodu nadmiernego We/Wy dysku.</span><span class="sxs-lookup"><span data-stu-id="2c27b-180">A high disk queue length is an indication of an application that might be slowing down due to excessive disk I/O.</span></span>
* <span data-ttu-id="2c27b-181">**Długość kolejki http**</span><span class="sxs-lookup"><span data-stu-id="2c27b-181">**Http Queue Length**</span></span>
  * <span data-ttu-id="2c27b-182">Średnia liczba żądań HTTP, które musiały znajdują się w kolejce przed są spełnione.</span><span class="sxs-lookup"><span data-stu-id="2c27b-182">The average number of HTTP requests that had to sit on the queue before being fulfilled.</span></span> <span data-ttu-id="2c27b-183">Wysoki lub zwiększa długość kolejki HTTP jest symptomem planu obciążona.</span><span class="sxs-lookup"><span data-stu-id="2c27b-183">A high or increasing HTTP Queue length is a symptom of a plan under heavy load.</span></span>

### <a name="cpu-time-vs-cpu-percentage"></a><span data-ttu-id="2c27b-184">Wartość procentowa vs Procesora czas Procesora</span><span class="sxs-lookup"><span data-stu-id="2c27b-184">CPU time vs CPU percentage</span></span>
<!-- To do: Fix Anchor (#CPU-time-vs.-CPU-percentage) -->

<span data-ttu-id="2c27b-185">Istnieją 2 metryk, które odzwierciedlają użycie procesora CPU.</span><span class="sxs-lookup"><span data-stu-id="2c27b-185">There are 2 metrics that reflect CPU usage.</span></span> <span data-ttu-id="2c27b-186">**Czas procesora CPU** i **procent użycia procesora CPU**</span><span class="sxs-lookup"><span data-stu-id="2c27b-186">**CPU time** and **CPU percentage**</span></span>

<span data-ttu-id="2c27b-187">**Czas procesora CPU** jest przydatne dla aplikacji hostowanej w **wolne** lub **Shared** plany, ponieważ ich przydziałów jest zdefiniowana w minutach procesora CPU używanych przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="2c27b-187">**CPU Time** is useful for apps hosted in **Free** or **Shared** plans since one of their quotas is defined in CPU minutes used by the app.</span></span>

<span data-ttu-id="2c27b-188">**Procent użycia procesora CPU** z drugiej strony jest przydatne dla aplikacji hostowanej w **podstawowe**, **standardowe** i **premium** plany, ponieważ mogą one być skalowana w poziomie, a ta metryka to wskazuje ogólną użycia we wszystkich wystąpieniach.</span><span class="sxs-lookup"><span data-stu-id="2c27b-188">**CPU percentage** on the other hand is useful for apps hosted in **basic**, **standard** and **premium** plans since they can be scaled out and this metric is a good indication of the overall usage across all instances.</span></span>

## <a name="metrics-granularity-and-retention-policy"></a><span data-ttu-id="2c27b-189">Poziom szczegółowości metryki i zasady przechowywania</span><span class="sxs-lookup"><span data-stu-id="2c27b-189">Metrics Granularity and Retention Policy</span></span>
<span data-ttu-id="2c27b-190">Metryki dla aplikacji i plan usługi aplikacji są rejestrowane i agregowane przez usługę za pomocą zasad przechowywania i szczegółowości następujące:</span><span class="sxs-lookup"><span data-stu-id="2c27b-190">Metrics for an application and app service plan are logged and aggregated by the service with the following granularities and retention policies:</span></span>

* <span data-ttu-id="2c27b-191">**Minuta** metryki szczegółowości są zachowywane dla **48 godzin**</span><span class="sxs-lookup"><span data-stu-id="2c27b-191">**Minute** granularity metrics are retained for **48 hours**</span></span>
* <span data-ttu-id="2c27b-192">**Godzina** metryki szczegółowości są zachowywane dla **30 dni**</span><span class="sxs-lookup"><span data-stu-id="2c27b-192">**Hour** granularity metrics are retained for **30 days**</span></span>
* <span data-ttu-id="2c27b-193">**Dzień** metryki szczegółowości są zachowywane dla **90 dni**</span><span class="sxs-lookup"><span data-stu-id="2c27b-193">**Day** granularity metrics are retained for **90 days**</span></span>

## <a name="monitoring-quotas-and-metrics-in-the-azure-portal"></a><span data-ttu-id="2c27b-194">Monitorowanie przydziałów i metryki w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="2c27b-194">Monitoring Quotas and Metrics in the Azure Portal.</span></span>
<span data-ttu-id="2c27b-195">Można sprawdzić stan różnych **przydziały** i **metryki** mające wpływ na aplikację w [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2c27b-195">You can review the status of the different **quotas** and **metrics** affecting an application in the [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="2c27b-196">![][quotas]
**Przydziały** znajduje się w obszarze Ustawienia >**przydziały**.</span><span class="sxs-lookup"><span data-stu-id="2c27b-196">![][quotas]
**Quotas** can be found under Settings>**Quotas**.</span></span> <span data-ttu-id="2c27b-197">Środowiska użytkownika umożliwia przeglądanie: (1) nazwa przydziałów, (2) jego interwał resetowania, (3) jego bieżący limit i (4) bieżącą wartość.</span><span class="sxs-lookup"><span data-stu-id="2c27b-197">The UX allows you to review: (1) the quotas name, (2) its reset interval, (3) its current limit and (4) current value.</span></span>

<span data-ttu-id="2c27b-198">![][metrics]
**Metryki** może być dostępu bezpośrednio z bloku zasobów.</span><span class="sxs-lookup"><span data-stu-id="2c27b-198">![][metrics]
**Metrics** can be access directly from the resource blade.</span></span> <span data-ttu-id="2c27b-199">Można również dostosować wykres przez: (1) **kliknij** i wybierz (2) **Edytuj wykres**.</span><span class="sxs-lookup"><span data-stu-id="2c27b-199">You can also customize the chart by: (1) **click** on it, and select (2) **edit chart**.</span></span>
<span data-ttu-id="2c27b-200">W tym miejscu można zmienić (3) **zakres czasu**4 **typ wykresu**i 5 **metryki** do wyświetlenia.</span><span class="sxs-lookup"><span data-stu-id="2c27b-200">From here you can change the (3) **time range**, (4) **chart type**, and (5) **metrics** to display.</span></span>  

<span data-ttu-id="2c27b-201">Dowiedz się więcej o metryki tutaj: [monitorować metryki usługi](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="2c27b-201">You can learn more about metrics here: [Monitor service metrics](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span></span>

## <a name="alerts-and-autoscale"></a><span data-ttu-id="2c27b-202">Alerty i skalowania automatycznego</span><span class="sxs-lookup"><span data-stu-id="2c27b-202">Alerts and Autoscale</span></span>
<span data-ttu-id="2c27b-203">Metryki dla planu aplikacji lub usługi aplikacji można podłączyć do alertów, aby dowiedzieć się więcej na ten temat, zobacz [otrzymywać powiadomienia o alertach](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)</span><span class="sxs-lookup"><span data-stu-id="2c27b-203">Metrics for an App or App Service plan can be hooked up to alerts, to learn more about this, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)</span></span>

<span data-ttu-id="2c27b-204">Aplikacje usługi aplikacji hostowanej w basic, standard lub premium plany usługi App Service obsługuje **skalowania automatycznego**.</span><span class="sxs-lookup"><span data-stu-id="2c27b-204">App Service apps hosted in basic, standard or premium App Service Plans support **autoscale**.</span></span> <span data-ttu-id="2c27b-205">Dzięki temu można skonfigurować reguły monitorować metryki planu usługi aplikacji i można zwiększyć lub zmniejszyć liczbę wystąpień, zapewniając dodatkowe zasoby, zgodnie z potrzebami lub zapisywanie pieniędzy, gdy aplikacja jest nadmiernego udostępniania.</span><span class="sxs-lookup"><span data-stu-id="2c27b-205">This allows you to configure rules that monitor the App Service plan metrics and can increase or decrease the instance count providing additional resources as needed, or saving money when the application is over-provision.</span></span> <span data-ttu-id="2c27b-206">Dowiedz się więcej o automatyczne skalowanie: [sposobu skalowania](../monitoring-and-diagnostics/insights-how-to-scale.md) i tutaj [najlepszych rozwiązań dotyczących skalowania automatycznego Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-best-practices.md)</span><span class="sxs-lookup"><span data-stu-id="2c27b-206">You can learn more about auto scale here: [How to Scale](../monitoring-and-diagnostics/insights-how-to-scale.md) and here [Best practices for Azure Monitor autoscaling](../monitoring-and-diagnostics/insights-autoscale-best-practices.md)</span></span>

> [!NOTE]
> <span data-ttu-id="2c27b-207">Jeśli chcesz zacząć korzystać z usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź do artykułu [Try App Service](https://azure.microsoft.com/try/app-service/) (Wypróbuj usługę App Service), w którym wyjaśniono, jak od razu utworzyć początkową aplikację sieci Web o krótkim okresie istnienia w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="2c27b-207">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="2c27b-208">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="2c27b-208">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="2c27b-209">Co zostało zmienione</span><span class="sxs-lookup"><span data-stu-id="2c27b-209">What's changed</span></span>
* <span data-ttu-id="2c27b-210">Przewodnik dotyczący przejścia od usługi Witryny sieci Web do usługi App Service można znaleźć w temacie [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714) (Usługa Azure App Service i jej wpływ na istniejące usługi platformy Azure).</span><span class="sxs-lookup"><span data-stu-id="2c27b-210">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[fzilla]:http://go.microsoft.com/fwlink/?LinkId=247914
[vmsizes]:http://go.microsoft.com/fwlink/?LinkID=309169



<!-- Images. -->
[http403]: ./media/web-sites-monitor/http403.png
[quotas]: ./media/web-sites-monitor/quotas.png
[metrics]: ./media/web-sites-monitor/metrics.png
