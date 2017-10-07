---
title: "aaaMonitor aplikacji w usłudze Azure App Service | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomonitor aplikacji w usłudze Azure App Service przy użyciu hello portalu Azure."
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
ms.openlocfilehash: 80d5a466102a894a49d04ae35aa54cc1d05a58df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-monitor-apps-in-azure-app-service"></a><span data-ttu-id="467c8-103">Porady: monitorować aplikacje w usłudze aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="467c8-103">How to: Monitor Apps in Azure App Service</span></span>
<span data-ttu-id="467c8-104">[Usługi aplikacji](http://go.microsoft.com/fwlink/?LinkId=529714) oferuje wbudowane funkcje monitorowania w hello [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="467c8-104">[App Service](http://go.microsoft.com/fwlink/?LinkId=529714) provides built in monitoring functionality in hello [Azure Portal](https://portal.azure.com).</span></span>
<span data-ttu-id="467c8-105">Dotyczy to również hello możliwości tooreview **przydziały** i **metryki** dla aplikacji, a także hello planu usługi aplikacji, ustawianie **alerty** i nawet **skalowanie** automatycznie w oparciu o te metryki.</span><span class="sxs-lookup"><span data-stu-id="467c8-105">This includes hello ability tooreview **quotas** and **metrics** for an app as well as hello App Service plan, setting up **alerts** and even **scaling** automatically based on these metrics.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="understanding-quotas-and-metrics"></a><span data-ttu-id="467c8-106">Opis przydziałów i metryki</span><span class="sxs-lookup"><span data-stu-id="467c8-106">Understanding Quotas and Metrics</span></span>
### <a name="quotas"></a><span data-ttu-id="467c8-107">Przydziały</span><span class="sxs-lookup"><span data-stu-id="467c8-107">Quotas</span></span>
<span data-ttu-id="467c8-108">Aplikacje hostowane w usłudze App Service są podmiotu toocertain *limity* z użyciem zasobów.</span><span class="sxs-lookup"><span data-stu-id="467c8-108">Applications hosted in App Service are subject toocertain *limits* on the resources they can use.</span></span> <span data-ttu-id="467c8-109">Witaj limity są definiowane przez hello **planu usługi aplikacji** skojarzone z aplikacją hello.</span><span class="sxs-lookup"><span data-stu-id="467c8-109">hello limits are defined by hello **App Service plan** associated with hello app.</span></span>

<span data-ttu-id="467c8-110">Jeśli aplikacja hello jest obsługiwana w **wolne** lub **Shared** planowanie, a następnie wynika z limitów hello hello zasobów można używać aplikacji hello **przydziały**.</span><span class="sxs-lookup"><span data-stu-id="467c8-110">If hello application is hosted in a **Free** or **Shared** plan, then hello limits on hello resources hello app can use are defined by **Quotas**.</span></span>

<span data-ttu-id="467c8-111">Jeśli aplikacja hello jest obsługiwana w **podstawowe**, **standardowe** lub **Premium** planowanie, a następnie limity hello mogą używać zasobów hello są ustawiane przez hello **rozmiar** (Mały, Średni, duża) i **wystąpienia licznika** (1, 2, 3,...) z hello **planu usługi aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="467c8-111">If hello application is hosted in a **Basic**, **Standard** or **Premium** plan, then hello limits on hello resources they can use are set by hello **size** (Small, Medium, Large) and **instance count** (1, 2, 3, ...) of hello **App Service plan**.</span></span>

<span data-ttu-id="467c8-112">**Przydziały** dla **wolne** lub **Shared** aplikacje są:</span><span class="sxs-lookup"><span data-stu-id="467c8-112">**Quotas** for **Free** or **Shared** apps are:</span></span>

* <span data-ttu-id="467c8-113">**CPU(Short)**</span><span class="sxs-lookup"><span data-stu-id="467c8-113">**CPU(Short)**</span></span>
  * <span data-ttu-id="467c8-114">Ilość Procesora dozwolone dla tej aplikacji w 5 minut.</span><span class="sxs-lookup"><span data-stu-id="467c8-114">Amount of CPU allowed for this application in a 5-minute interval.</span></span> <span data-ttu-id="467c8-115">Ten limit przydziału ustawia ponownie co 5 minut.</span><span class="sxs-lookup"><span data-stu-id="467c8-115">This quota re-sets every 5 minutes.</span></span>
* <span data-ttu-id="467c8-116">**CPU(Day)**</span><span class="sxs-lookup"><span data-stu-id="467c8-116">**CPU(Day)**</span></span>
  * <span data-ttu-id="467c8-117">Całkowita ilość Procesora dozwolone dla tej aplikacji w ciągu jednego dnia.</span><span class="sxs-lookup"><span data-stu-id="467c8-117">Total amount of CPU allowed for this application in a day.</span></span> <span data-ttu-id="467c8-118">Ten limit przydziału ustawia ponownie co 24 godziny, o północy czasu UTC.</span><span class="sxs-lookup"><span data-stu-id="467c8-118">This quota re-sets every 24 hours at midnight UTC.</span></span>
* <span data-ttu-id="467c8-119">**Pamięci**</span><span class="sxs-lookup"><span data-stu-id="467c8-119">**Memory**</span></span>
  * <span data-ttu-id="467c8-120">Całkowita ilość pamięci dozwolone dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="467c8-120">Total amount of memory allowed for this application.</span></span>
* <span data-ttu-id="467c8-121">**Przepustowość**</span><span class="sxs-lookup"><span data-stu-id="467c8-121">**Bandwidth**</span></span>
  * <span data-ttu-id="467c8-122">Całkowita ilość przepustowości wychodzącej dozwolone dla tej aplikacji w ciągu jednego dnia.</span><span class="sxs-lookup"><span data-stu-id="467c8-122">Total amount of outgoing bandwidth allowed for this application in a day.</span></span>
    <span data-ttu-id="467c8-123">Ten limit przydziału ustawia ponownie co 24 godziny, o północy czasu UTC.</span><span class="sxs-lookup"><span data-stu-id="467c8-123">This quota re-sets every 24 hours at midnight UTC.</span></span>
* <span data-ttu-id="467c8-124">**System plików**</span><span class="sxs-lookup"><span data-stu-id="467c8-124">**Filesystem**</span></span>
  * <span data-ttu-id="467c8-125">Całkowita liczba dozwoloną ilość pamięci masowej.</span><span class="sxs-lookup"><span data-stu-id="467c8-125">Total amount of storage allowed.</span></span>

<span data-ttu-id="467c8-126">Witaj tylko przydział dotyczy tooapps hostowanych na **podstawowe**, **standardowe** i **Premium** jest planów **systemu plików**.</span><span class="sxs-lookup"><span data-stu-id="467c8-126">hello only quota applicable tooapps hosted on **Basic**, **Standard** and **Premium** plans is **Filesystem**.</span></span>

<span data-ttu-id="467c8-127">Więcej informacji na temat określonych przydziały hello, ograniczenia i funkcje dostępne dla hello różne jednostki magazynowe usługi aplikacji można znaleźć tutaj: [ograniczenia usługi subskrypcji platformy Azure](../azure-subscription-service-limits.md#app-service-limits)</span><span class="sxs-lookup"><span data-stu-id="467c8-127">More information about hello specific quotas, limits and features available to hello different App Service SKUs can be found here: [Azure Subscription Service Limits](../azure-subscription-service-limits.md#app-service-limits)</span></span>

#### <a name="quota-enforcement"></a><span data-ttu-id="467c8-128">Wymuszanie przydziałów</span><span class="sxs-lookup"><span data-stu-id="467c8-128">Quota Enforcement</span></span>
<span data-ttu-id="467c8-129">Jeśli aplikacja w jej użycie przekracza hello **procesora CPU (short)**, **procesora CPU (dzień)**, lub **przepustowości** przydziału, a następnie hello aplikacji zostanie zatrzymana, aż do ponownego ustawia limit przydziału hello.</span><span class="sxs-lookup"><span data-stu-id="467c8-129">If an application in its usage exceeds hello **CPU (short)**, **CPU (Day)**, or **bandwidth** quota then hello application will be stopped until hello quota re-sets.</span></span> <span data-ttu-id="467c8-130">W tym czasie wszystkie żądania przychodzące spowoduje **HTTP 403**.</span><span class="sxs-lookup"><span data-stu-id="467c8-130">During this time, all incoming requests will result in an **HTTP 403**.</span></span>
![][http403]

<span data-ttu-id="467c8-131">Jeśli aplikacja hello **pamięci** przekroczony przydział, a następnie aplikacja hello zostanie ponownie uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="467c8-131">If hello application **memory** quota is exceeded, then hello application will be re-started.</span></span>

<span data-ttu-id="467c8-132">Jeśli hello **Filesystem** przekroczony przydział, a następnie żadnego zapisu, operacja zakończy się niepowodzeniem, w tym zapisywania toologs.</span><span class="sxs-lookup"><span data-stu-id="467c8-132">If hello **Filesystem** quota is exceeded, then any write operation will fail, this includes writing toologs.</span></span>

<span data-ttu-id="467c8-133">Przydziały można zwiększyć lub usunięte z aplikacji, uaktualniając plan usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="467c8-133">Quotas can be increased or removed from your app by upgrading your App Service plan.</span></span>

### <a name="metrics"></a><span data-ttu-id="467c8-134">Metryki</span><span class="sxs-lookup"><span data-stu-id="467c8-134">Metrics</span></span>
<span data-ttu-id="467c8-135">**Metryki** zawierają informacje o aplikacji hello lub zachowanie planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="467c8-135">**Metrics** provide information about hello app, or App Service plan's behavior.</span></span>

<span data-ttu-id="467c8-136">Aby uzyskać **aplikacji**, są dostępne metryki hello:</span><span class="sxs-lookup"><span data-stu-id="467c8-136">For an **Application**, hello available metrics are:</span></span>

* <span data-ttu-id="467c8-137">**Średni czas odpowiedzi**</span><span class="sxs-lookup"><span data-stu-id="467c8-137">**Average Response Time**</span></span>
  * <span data-ttu-id="467c8-138">Witaj Średni czas żądania tooserve aplikacji hello w ms.</span><span class="sxs-lookup"><span data-stu-id="467c8-138">hello average time taken for hello app tooserve requests in ms.</span></span>
* <span data-ttu-id="467c8-139">**Pamięć średni zestaw roboczy**</span><span class="sxs-lookup"><span data-stu-id="467c8-139">**Average memory working set**</span></span>
  * <span data-ttu-id="467c8-140">Hello średnia ilość pamięci w bazach MIB używany przez aplikację hello.</span><span class="sxs-lookup"><span data-stu-id="467c8-140">hello average amount of memory in MiBs used by hello app.</span></span>
* <span data-ttu-id="467c8-141">**Czas procesora CPU**</span><span class="sxs-lookup"><span data-stu-id="467c8-141">**CPU Time**</span></span>
  * <span data-ttu-id="467c8-142">Witaj ilość Procesora w sekundach wykorzystanych w ramach aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="467c8-142">hello amount of CPU in seconds consumed by hello app.</span></span> <span data-ttu-id="467c8-143">Aby uzyskać więcej informacji o tym, zobacz metryki: [procent vs Procesora czas procesora CPU](#cpu-time-vs-cpu-percentage)</span><span class="sxs-lookup"><span data-stu-id="467c8-143">For more information about this metric see: [CPU time vs CPU percentage](#cpu-time-vs-cpu-percentage)</span></span>
* <span data-ttu-id="467c8-144">**Dane w**</span><span class="sxs-lookup"><span data-stu-id="467c8-144">**Data In**</span></span>
  * <span data-ttu-id="467c8-145">Witaj ilość przychodzącego przepustowości aplikacji hello w bazach MIB.</span><span class="sxs-lookup"><span data-stu-id="467c8-145">hello amount of incoming bandwidth consumed by hello app in MiBs.</span></span>
* <span data-ttu-id="467c8-146">**Dla danych wychodzących**</span><span class="sxs-lookup"><span data-stu-id="467c8-146">**Data Out**</span></span>
  * <span data-ttu-id="467c8-147">Witaj ilość przepustowości wychodzącej dla aplikacji hello w bazach MIB.</span><span class="sxs-lookup"><span data-stu-id="467c8-147">hello amount of outgoing bandwidth consumed by hello app in MiBs.</span></span>
* <span data-ttu-id="467c8-148">**Http 2xx**</span><span class="sxs-lookup"><span data-stu-id="467c8-148">**Http 2xx**</span></span>
  * <span data-ttu-id="467c8-149">Liczba żądań, co powoduje kod stanu http > = 200, ale < 300.</span><span class="sxs-lookup"><span data-stu-id="467c8-149">Count of requests resulting in a http status code >= 200 but < 300.</span></span>
* <span data-ttu-id="467c8-150">**Http 3xx**</span><span class="sxs-lookup"><span data-stu-id="467c8-150">**Http 3xx**</span></span>
  * <span data-ttu-id="467c8-151">Liczba żądań, co powoduje kod stanu http > = 300, ale < 400.</span><span class="sxs-lookup"><span data-stu-id="467c8-151">Count of requests resulting in a http status code >= 300 but < 400.</span></span>
* <span data-ttu-id="467c8-152">**HTTP 401**</span><span class="sxs-lookup"><span data-stu-id="467c8-152">**Http 401**</span></span>
  * <span data-ttu-id="467c8-153">Liczba żądań, co powoduje kod stanu HTTP 401.</span><span class="sxs-lookup"><span data-stu-id="467c8-153">Count of requests resulting in HTTP 401 status code.</span></span>
* <span data-ttu-id="467c8-154">**HTTP 403**</span><span class="sxs-lookup"><span data-stu-id="467c8-154">**Http 403**</span></span>
  * <span data-ttu-id="467c8-155">Liczba żądań, co powoduje kod stanu HTTP 403.</span><span class="sxs-lookup"><span data-stu-id="467c8-155">Count of requests resulting in HTTP 403 status code.</span></span>
* <span data-ttu-id="467c8-156">**HTTP 404**</span><span class="sxs-lookup"><span data-stu-id="467c8-156">**Http 404**</span></span>
  * <span data-ttu-id="467c8-157">Liczba żądań, co powoduje kod stanu HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="467c8-157">Count of requests resulting in HTTP 404 status code.</span></span>
* <span data-ttu-id="467c8-158">**HTTP 406**</span><span class="sxs-lookup"><span data-stu-id="467c8-158">**Http 406**</span></span>
  * <span data-ttu-id="467c8-159">Liczba żądań, co powoduje kod stanu HTTP 406.</span><span class="sxs-lookup"><span data-stu-id="467c8-159">Count of requests resulting in HTTP 406 status code.</span></span>
* <span data-ttu-id="467c8-160">**Http 4xx**</span><span class="sxs-lookup"><span data-stu-id="467c8-160">**Http 4xx**</span></span>
  * <span data-ttu-id="467c8-161">Liczba żądań, co powoduje kod stanu http > = 400, ale < 500.</span><span class="sxs-lookup"><span data-stu-id="467c8-161">Count of requests resulting in a http status code >= 400 but < 500.</span></span>
* <span data-ttu-id="467c8-162">**Błędy HTTP serwera**</span><span class="sxs-lookup"><span data-stu-id="467c8-162">**Http Server Errors**</span></span>
  * <span data-ttu-id="467c8-163">Liczba żądań, co powoduje kod stanu http > = 500, ale < 600.</span><span class="sxs-lookup"><span data-stu-id="467c8-163">Count of requests resulting in a http status code >= 500 but < 600.</span></span>
* <span data-ttu-id="467c8-164">**Zestaw roboczy pamięci**</span><span class="sxs-lookup"><span data-stu-id="467c8-164">**Memory working set**</span></span>
  * <span data-ttu-id="467c8-165">Bieżąca ilość pamięci użytej przez aplikację hello w bazach MIB.</span><span class="sxs-lookup"><span data-stu-id="467c8-165">Current amount of memory used by hello app in MiBs.</span></span>
* <span data-ttu-id="467c8-166">**Żądania**</span><span class="sxs-lookup"><span data-stu-id="467c8-166">**Requests**</span></span>
  * <span data-ttu-id="467c8-167">Całkowita liczba żądań, niezależnie od ich wynikowy kod stanu HTTP.</span><span class="sxs-lookup"><span data-stu-id="467c8-167">Total number of requests regardless of their resulting HTTP status code.</span></span>

<span data-ttu-id="467c8-168">Aby uzyskać **planu usługi aplikacji**, są dostępne metryki hello:</span><span class="sxs-lookup"><span data-stu-id="467c8-168">For an **App Service plan**, hello available metrics are:</span></span>

> [!NOTE]
> <span data-ttu-id="467c8-169">Metryki planu usługi aplikacji są dostępne tylko dla planów w **podstawowe**, **standardowe** i **Premium** jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="467c8-169">App Service plan metrics are only available for plans in **Basic**, **Standard** and **Premium** SKU.</span></span>
> 
> 

* <span data-ttu-id="467c8-170">**Procent użycia procesora CPU**</span><span class="sxs-lookup"><span data-stu-id="467c8-170">**CPU Percentage**</span></span>
  * <span data-ttu-id="467c8-171">Witaj średnie użycie procesora CPU we wszystkich wystąpieniach planu hello.</span><span class="sxs-lookup"><span data-stu-id="467c8-171">hello average CPU used across all instances of hello plan.</span></span>
* <span data-ttu-id="467c8-172">**Procent pamięci**</span><span class="sxs-lookup"><span data-stu-id="467c8-172">**Memory Percentage**</span></span>
  * <span data-ttu-id="467c8-173">Witaj średni pamięć używana we wszystkich wystąpieniach planu hello.</span><span class="sxs-lookup"><span data-stu-id="467c8-173">hello average memory used across all instances of hello plan.</span></span>
* <span data-ttu-id="467c8-174">**Dane w**</span><span class="sxs-lookup"><span data-stu-id="467c8-174">**Data In**</span></span>
  * <span data-ttu-id="467c8-175">Witaj Średnia przepustowość przychodzące używane we wszystkich wystąpieniach planu hello.</span><span class="sxs-lookup"><span data-stu-id="467c8-175">hello average incoming bandwidth used across all instances of hello plan.</span></span>
* <span data-ttu-id="467c8-176">**Dla danych wychodzących**</span><span class="sxs-lookup"><span data-stu-id="467c8-176">**Data Out**</span></span>
  * <span data-ttu-id="467c8-177">Średnia Hello przepustowość we wszystkich wystąpieniach planu hello wychodzące.</span><span class="sxs-lookup"><span data-stu-id="467c8-177">hello average outgoing bandwidth used across all instances of hello plan.</span></span>
* <span data-ttu-id="467c8-178">**Długość kolejki dysku**</span><span class="sxs-lookup"><span data-stu-id="467c8-178">**Disk Queue Length**</span></span>
  * <span data-ttu-id="467c8-179">Witaj średnią liczbę zarówno żądania odczytu i zapisu umieszczonych w kolejce w magazynie.</span><span class="sxs-lookup"><span data-stu-id="467c8-179">hello average number of both read and write requests that were queued on storage.</span></span> <span data-ttu-id="467c8-180">Długość kolejki dysku będzie wskazywać aplikacji, która może zmniejszają należne we/wy dysku tooexcessive.</span><span class="sxs-lookup"><span data-stu-id="467c8-180">A high disk queue length is an indication of an application that might be slowing down due tooexcessive disk I/O.</span></span>
* <span data-ttu-id="467c8-181">**Długość kolejki http**</span><span class="sxs-lookup"><span data-stu-id="467c8-181">**Http Queue Length**</span></span>
  * <span data-ttu-id="467c8-182">Witaj średnia liczba żądań HTTP, które ma toosit w kolejce hello przed są spełnione.</span><span class="sxs-lookup"><span data-stu-id="467c8-182">hello average number of HTTP requests that had toosit on hello queue before being fulfilled.</span></span> <span data-ttu-id="467c8-183">Wysoki lub zwiększa długość kolejki HTTP jest symptomem planu obciążona.</span><span class="sxs-lookup"><span data-stu-id="467c8-183">A high or increasing HTTP Queue length is a symptom of a plan under heavy load.</span></span>

### <a name="cpu-time-vs-cpu-percentage"></a><span data-ttu-id="467c8-184">Wartość procentowa vs Procesora czas Procesora</span><span class="sxs-lookup"><span data-stu-id="467c8-184">CPU time vs CPU percentage</span></span>
<!-- toodo: Fix Anchor (#CPU-time-vs.-CPU-percentage) -->

<span data-ttu-id="467c8-185">Istnieją 2 metryk, które odzwierciedlają użycie procesora CPU.</span><span class="sxs-lookup"><span data-stu-id="467c8-185">There are 2 metrics that reflect CPU usage.</span></span> <span data-ttu-id="467c8-186">**Czas procesora CPU** i **procent użycia procesora CPU**</span><span class="sxs-lookup"><span data-stu-id="467c8-186">**CPU time** and **CPU percentage**</span></span>

<span data-ttu-id="467c8-187">**Czas procesora CPU** jest przydatne dla aplikacji hostowanej w **wolne** lub **Shared** plany, ponieważ jeden z ich przydziały jest określana w minutach procesora CPU, używany przez aplikację hello.</span><span class="sxs-lookup"><span data-stu-id="467c8-187">**CPU Time** is useful for apps hosted in **Free** or **Shared** plans since one of their quotas is defined in CPU minutes used by hello app.</span></span>

<span data-ttu-id="467c8-188">**Procent użycia procesora CPU** na powitania drugiej jest przydatne dla aplikacji hostowanej w **podstawowe**, **standardowe** i **premium** plany, ponieważ mogą one być skalowana w poziomie i ta metryka jest dobrym wskaźnikiem hello ogólne wykorzystanie we wszystkich wystąpieniach.</span><span class="sxs-lookup"><span data-stu-id="467c8-188">**CPU percentage** on hello other hand is useful for apps hosted in **basic**, **standard** and **premium** plans since they can be scaled out and this metric is a good indication of hello overall usage across all instances.</span></span>

## <a name="metrics-granularity-and-retention-policy"></a><span data-ttu-id="467c8-189">Poziom szczegółowości metryki i zasady przechowywania</span><span class="sxs-lookup"><span data-stu-id="467c8-189">Metrics Granularity and Retention Policy</span></span>
<span data-ttu-id="467c8-190">Metryki planu usługi aplikacji i aplikacji są rejestrowane i agregowane przez usługę hello z hello następujące zasady przechowywania i szczegółowości:</span><span class="sxs-lookup"><span data-stu-id="467c8-190">Metrics for an application and app service plan are logged and aggregated by hello service with hello following granularities and retention policies:</span></span>

* <span data-ttu-id="467c8-191">**Minuta** metryki szczegółowości są zachowywane dla **48 godzin**</span><span class="sxs-lookup"><span data-stu-id="467c8-191">**Minute** granularity metrics are retained for **48 hours**</span></span>
* <span data-ttu-id="467c8-192">**Godzina** metryki szczegółowości są zachowywane dla **30 dni**</span><span class="sxs-lookup"><span data-stu-id="467c8-192">**Hour** granularity metrics are retained for **30 days**</span></span>
* <span data-ttu-id="467c8-193">**Dzień** metryki szczegółowości są zachowywane dla **90 dni**</span><span class="sxs-lookup"><span data-stu-id="467c8-193">**Day** granularity metrics are retained for **90 days**</span></span>

## <a name="monitoring-quotas-and-metrics-in-hello-azure-portal"></a><span data-ttu-id="467c8-194">Monitorowanie przydziałów i metryki hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="467c8-194">Monitoring Quotas and Metrics in hello Azure Portal.</span></span>
<span data-ttu-id="467c8-195">Możesz przejrzeć stan hello hello różnych **przydziały** i **metryki** mające wpływ na aplikację w hello [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="467c8-195">You can review hello status of hello different **quotas** and **metrics** affecting an application in hello [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="467c8-196">![][quotas]
**Przydziały** znajduje się w obszarze Ustawienia >**przydziały**.</span><span class="sxs-lookup"><span data-stu-id="467c8-196">![][quotas]
**Quotas** can be found under Settings>**Quotas**.</span></span> <span data-ttu-id="467c8-197">Witaj UX umożliwia zapoznanie się z: Nazwa przydziały hello (1), (2) jego interwał resetowania, (3) jego bieżący limit i (4) bieżącą wartość.</span><span class="sxs-lookup"><span data-stu-id="467c8-197">hello UX allows you to review: (1) hello quotas name, (2) its reset interval, (3) its current limit and (4) current value.</span></span>

<span data-ttu-id="467c8-198">![][metrics]
**Metryki** może być dostępu bezpośrednio z bloku zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="467c8-198">![][metrics]
**Metrics** can be access directly from hello resource blade.</span></span> <span data-ttu-id="467c8-199">Można również dostosować wykres hello przez: (1) **kliknij** i wybierz (2) **Edytuj wykres**.</span><span class="sxs-lookup"><span data-stu-id="467c8-199">You can also customize hello chart by: (1) **click** on it, and select (2) **edit chart**.</span></span>
<span data-ttu-id="467c8-200">W tym miejscu można zmienić hello (3) **zakres czasu**4 **typ wykresu**i 5 **metryki** toodisplay.</span><span class="sxs-lookup"><span data-stu-id="467c8-200">From here you can change hello (3) **time range**, (4) **chart type**, and (5) **metrics** toodisplay.</span></span>  

<span data-ttu-id="467c8-201">Dowiedz się więcej o metryki tutaj: [monitorować metryki usługi](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="467c8-201">You can learn more about metrics here: [Monitor service metrics](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span></span>

## <a name="alerts-and-autoscale"></a><span data-ttu-id="467c8-202">Alerty i skalowania automatycznego</span><span class="sxs-lookup"><span data-stu-id="467c8-202">Alerts and Autoscale</span></span>
<span data-ttu-id="467c8-203">Metryki planu aplikacji lub usługi aplikacji może podłączonymi tooalerts, toolearn więcej na ten temat, zobacz [otrzymywać powiadomienia o alertach](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)</span><span class="sxs-lookup"><span data-stu-id="467c8-203">Metrics for an App or App Service plan can be hooked up tooalerts, toolearn more about this, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)</span></span>

<span data-ttu-id="467c8-204">Aplikacje usługi aplikacji hostowanej w basic, standard lub premium plany usługi App Service obsługuje **skalowania automatycznego**.</span><span class="sxs-lookup"><span data-stu-id="467c8-204">App Service apps hosted in basic, standard or premium App Service Plans support **autoscale**.</span></span> <span data-ttu-id="467c8-205">Dzięki temu można tooconfigure reguł, które monitorować metryki planu usługi aplikacji i można zwiększyć lub zmniejszyć liczbę wystąpień hello, zapewniając dodatkowe zasoby, zgodnie z potrzebami lub zapisywanie oszczędność pieniędzy w przypadku aplikacji hello nadmiernego udostępniania.</span><span class="sxs-lookup"><span data-stu-id="467c8-205">This allows you tooconfigure rules that monitor the App Service plan metrics and can increase or decrease hello instance count providing additional resources as needed, or saving money when hello application is over-provision.</span></span> <span data-ttu-id="467c8-206">Dowiedz się więcej o automatyczne skalowanie: [jak tooScale](../monitoring-and-diagnostics/insights-how-to-scale.md) i tutaj [najlepszych rozwiązań dotyczących skalowania automatycznego Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-best-practices.md)</span><span class="sxs-lookup"><span data-stu-id="467c8-206">You can learn more about auto scale here: [How tooScale](../monitoring-and-diagnostics/insights-how-to-scale.md) and here [Best practices for Azure Monitor autoscaling](../monitoring-and-diagnostics/insights-autoscale-best-practices.md)</span></span>

> [!NOTE]
> <span data-ttu-id="467c8-207">Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="467c8-207">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="467c8-208">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="467c8-208">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="467c8-209">Co zostało zmienione</span><span class="sxs-lookup"><span data-stu-id="467c8-209">What's changed</span></span>
* <span data-ttu-id="467c8-210">Toohello przewodnik zmiany z tooApp witryn sieci Web usługi dla: [usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="467c8-210">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[fzilla]:http://go.microsoft.com/fwlink/?LinkId=247914
[vmsizes]:http://go.microsoft.com/fwlink/?LinkID=309169



<!-- Images. -->
[http403]: ./media/web-sites-monitor/http403.png
[quotas]: ./media/web-sites-monitor/quotas.png
[metrics]: ./media/web-sites-monitor/metrics.png
