---
title: "Statystyki w czasie rzeczywistym w usłudze Azure CDN | Dokumentacja firmy Microsoft"
description: "Statystyki w czasie rzeczywistym udostępnia w czasie rzeczywistym danych dotyczących wydajności usługi Azure CDN podczas dostarczania zawartości do klientów."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: c7989340-1172-4315-acbb-186ba34dd52a
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: e9b9522de6b2c54dc794b00100ffe358296ecfdd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="real-time-stats-in-microsoft-azure-cdn"></a><span data-ttu-id="926b5-103">Statystyki w czasie rzeczywistym w usłudze Microsoft Azure CDN</span><span class="sxs-lookup"><span data-stu-id="926b5-103">Real-time stats in Microsoft Azure CDN</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="926b5-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="926b5-104">Overview</span></span>
<span data-ttu-id="926b5-105">W tym dokumencie opisano statystyki w czasie rzeczywistym w usłudze Microsoft Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="926b5-105">This document explains real-time stats in Microsoft Azure CDN.</span></span>  <span data-ttu-id="926b5-106">Ta funkcja udostępnia w czasie rzeczywistym danych, takich jak przepustowości, pamięci podręcznej stanów i jednoczesnych połączeń z profilu CDN podczas dostarczania zawartości do klientów.</span><span class="sxs-lookup"><span data-stu-id="926b5-106">This functionality provides real-time data, such as bandwidth, cache statuses, and concurrent connections to your CDN profile when delivering content to your clients.</span></span> <span data-ttu-id="926b5-107">Dzięki temu ciągłego monitorowania kondycji usługi, w dowolnym momencie, w tym zdarzenia dotyczące przejdź na żywo.</span><span class="sxs-lookup"><span data-stu-id="926b5-107">This enables continuous monitoring of the health of your service at any time, including go-live events.</span></span>

<span data-ttu-id="926b5-108">Dostępne są następujące wykresy:</span><span class="sxs-lookup"><span data-stu-id="926b5-108">The following graphs are available:</span></span>

* [<span data-ttu-id="926b5-109">Przepustowość</span><span class="sxs-lookup"><span data-stu-id="926b5-109">Bandwidth</span></span>](#bandwidth)
* [<span data-ttu-id="926b5-110">Kody stanu</span><span class="sxs-lookup"><span data-stu-id="926b5-110">Status Codes</span></span>](#status-codes)
* [<span data-ttu-id="926b5-111">Stany pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="926b5-111">Cache Statuses</span></span>](#cache-statuses)
* [<span data-ttu-id="926b5-112">Połączenia</span><span class="sxs-lookup"><span data-stu-id="926b5-112">Connections</span></span>](#connections)

## <a name="accessing-real-time-stats"></a><span data-ttu-id="926b5-113">Uzyskiwanie dostępu do statystyki w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="926b5-113">Accessing real-time stats</span></span>
1. <span data-ttu-id="926b5-114">W [Azure Portal](https://portal.azure.com), przejdź do swojego profilu CDN.</span><span class="sxs-lookup"><span data-stu-id="926b5-114">In the [Azure Portal](https://portal.azure.com), browse to your CDN profile.</span></span>
   
    ![Blok profilu CDN](./media/cdn-real-time-stats/cdn-profile-blade.png)
2. <span data-ttu-id="926b5-116">Blok profilu CDN, kliknij **Zarządzaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="926b5-116">From the CDN profile blade, click the **Manage** button.</span></span>
   
    ![Przycisk Zarządzaj blok profilu CDN](./media/cdn-real-time-stats/cdn-manage-btn.png)
   
    <span data-ttu-id="926b5-118">Zostanie otwarty w portalu zarządzania usługi CDN.</span><span class="sxs-lookup"><span data-stu-id="926b5-118">The CDN management portal opens.</span></span>
3. <span data-ttu-id="926b5-119">Umieść kursor nad **Analytics** , a następnie umieść kursor nad **statystyki w czasie rzeczywistym** wysuwane okno.</span><span class="sxs-lookup"><span data-stu-id="926b5-119">Hover over the **Analytics** tab, then hover over the **Real-Time Stats** flyout.</span></span>  <span data-ttu-id="926b5-120">Polecenie **HTTP dużego obiektu**.</span><span class="sxs-lookup"><span data-stu-id="926b5-120">Click on **HTTP Large Object**.</span></span>
   
    ![Portal zarządzania usługi CDN](./media/cdn-real-time-stats/cdn-premium-portal.png)
   
    <span data-ttu-id="926b5-122">Są wyświetlane na wykresach statystyki w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="926b5-122">The real-time stats graphs are displayed.</span></span>

<span data-ttu-id="926b5-123">Każda wykresów Wyświetla statystyki w czasie rzeczywistym dla zakresu wybrana wartość czasu, uruchamianie podczas ładowania strony.</span><span class="sxs-lookup"><span data-stu-id="926b5-123">Each of the graphs displays real-time statistics for the selected time span, starting when the page loads.</span></span>  <span data-ttu-id="926b5-124">Wykresy automatycznie aktualizowane co kilka sekund.</span><span class="sxs-lookup"><span data-stu-id="926b5-124">The graphs update automatically every few seconds.</span></span>  <span data-ttu-id="926b5-125">**Odśwież wykres** przycisku, jeśli jest obecny, spowoduje wyczyszczenie wykresu, po czym zostanie wyświetlona tylko wybranych danych.</span><span class="sxs-lookup"><span data-stu-id="926b5-125">The **Refresh Graph** button, if present, will clear the graph, after which it will only display the selected data.</span></span>

## <a name="bandwidth"></a><span data-ttu-id="926b5-126">Przepustowość</span><span class="sxs-lookup"><span data-stu-id="926b5-126">Bandwidth</span></span>
![Wykres przepustowości](./media/cdn-real-time-stats/cdn-bandwidth.png)

<span data-ttu-id="926b5-128">**Przepustowości** wykres przedstawia ilość przepustowości używanej w ramach bieżącej platformy w wybranym okresie.</span><span class="sxs-lookup"><span data-stu-id="926b5-128">The **Bandwidth** graph displays the amount of bandwidth used for the current platform over the selected time span.</span></span> <span data-ttu-id="926b5-129">Przyciemnione część wykres wskazuje użycia przepustowości.</span><span class="sxs-lookup"><span data-stu-id="926b5-129">The shaded portion of the graph indicates bandwidth usage.</span></span> <span data-ttu-id="926b5-130">Dokładne ilość przepustowości aktualnie używane jest wyświetlana bezpośrednio pod wykres liniowy.</span><span class="sxs-lookup"><span data-stu-id="926b5-130">The exact amount of bandwidth currently being used is displayed directly below the line graph.</span></span>

## <a name="status-codes"></a><span data-ttu-id="926b5-131">Kody stanu</span><span class="sxs-lookup"><span data-stu-id="926b5-131">Status Codes</span></span>
![Wykres kod stanu](./media/cdn-real-time-stats/cdn-status-codes.png)

<span data-ttu-id="926b5-133">**Kodów stanu** wykres wskazuje, jak często występuje niektórych kody odpowiedzi HTTP przez wybrany okres.</span><span class="sxs-lookup"><span data-stu-id="926b5-133">The **Status Codes** graph indicates how often certain HTTP response codes are occurring over the selected time span.</span></span>

> [!TIP]
> <span data-ttu-id="926b5-134">Opis każdej opcji Kod stanu HTTP, zobacz [kody stanu HTTP CDN Azure](https://msdn.microsoft.com/library/mt759238.aspx).</span><span class="sxs-lookup"><span data-stu-id="926b5-134">For a description of each HTTP status code option, see [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx).</span></span>
> 
> 

<span data-ttu-id="926b5-135">Bezpośrednio powyżej wykresu zostanie wyświetlona lista kodów stanu HTTP.</span><span class="sxs-lookup"><span data-stu-id="926b5-135">A list of HTTP status codes is displayed directly above the graph.</span></span> <span data-ttu-id="926b5-136">Ta lista wskazuje poszczególnych kodów stanu, który można umieścić w wykres liniowy i bieżącą liczbę wystąpień na sekundę dla tego kodu stanu.</span><span class="sxs-lookup"><span data-stu-id="926b5-136">This list indicates each status code that can be included in the line graph and the current number of occurrences per second for that status code.</span></span> <span data-ttu-id="926b5-137">Domyślnie dla każdego z tych kodów stanu na wykresie jest wyświetlany wiersza.</span><span class="sxs-lookup"><span data-stu-id="926b5-137">By default, a line is displayed for each of these status codes in the graph.</span></span> <span data-ttu-id="926b5-138">Można jednak tylko monitorowanie kodów stanu, które mają specjalne znaczenie dla danej konfiguracji sieci CDN.</span><span class="sxs-lookup"><span data-stu-id="926b5-138">However, you can choose to only monitor the status codes that have special significance for your CDN configuration.</span></span> <span data-ttu-id="926b5-139">Aby to zrobić, sprawdź kody żądany stan i wyczyść wszystkie inne opcje, a następnie kliknij **Odśwież wykres**.</span><span class="sxs-lookup"><span data-stu-id="926b5-139">To do this, check the desired status codes and clear all other options, then click **Refresh Graph**.</span></span> 

<span data-ttu-id="926b5-140">Można ukryć danych zarejestrowanych dla kodu określonego stanu.</span><span class="sxs-lookup"><span data-stu-id="926b5-140">You can temporarily hide logged data for a particular status code.</span></span>  <span data-ttu-id="926b5-141">W legendzie bezpośrednio pod wykresem kliknij kod stanu, który chcesz ukryć.</span><span class="sxs-lookup"><span data-stu-id="926b5-141">From the legend directly below the graph, click the status code you want to hide.</span></span> <span data-ttu-id="926b5-142">Kod stanu będą natychmiast ukryte wykresu.</span><span class="sxs-lookup"><span data-stu-id="926b5-142">The status code will be immediately hidden from the graph.</span></span> <span data-ttu-id="926b5-143">Ponowne kliknięcie tego kodu stanu spowoduje, że ta opcja będzie wyświetlana ponownie.</span><span class="sxs-lookup"><span data-stu-id="926b5-143">Clicking that status code again will cause that option to be displayed again.</span></span>

## <a name="cache-statuses"></a><span data-ttu-id="926b5-144">Stany pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="926b5-144">Cache Statuses</span></span>
![Wykres stanów pamięci podręcznej](./media/cdn-real-time-stats/cdn-cache-status.png)

<span data-ttu-id="926b5-146">**Pamięci podręcznej stanów** wykres wskazuje, jak często występują niektóre rodzaje pamięci podręcznej stanów w wybranym okresie.</span><span class="sxs-lookup"><span data-stu-id="926b5-146">The **Cache Statuses** graph indicates how often certain types of cache statuses are occurring over the selected time span.</span></span> 

> [!TIP]
> <span data-ttu-id="926b5-147">Opis opcji Kod stanu każdego pamięci podręcznej, zobacz [kodów stanu systemu Azure CDN pamięci podręcznej](https://msdn.microsoft.com/library/mt759237.aspx).</span><span class="sxs-lookup"><span data-stu-id="926b5-147">For a description of each cache status code option, see [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx).</span></span>
> 
> 

<span data-ttu-id="926b5-148">Zostanie wyświetlona lista kodów stanu pamięci podręcznej bezpośrednio powyżej wykresu.</span><span class="sxs-lookup"><span data-stu-id="926b5-148">A list of cache status codes is displayed directly above the graph.</span></span> <span data-ttu-id="926b5-149">Ta lista wskazuje poszczególnych kodów stanu, który można umieścić w wykres liniowy i bieżącą liczbę wystąpień na sekundę dla tego kodu stanu.</span><span class="sxs-lookup"><span data-stu-id="926b5-149">This list indicates each status code that can be included in the line graph and the current number of occurrences per second for that status code.</span></span> <span data-ttu-id="926b5-150">Domyślnie dla każdego z tych kodów stanu na wykresie jest wyświetlany wiersza.</span><span class="sxs-lookup"><span data-stu-id="926b5-150">By default, a line is displayed for each of these status codes in the graph.</span></span> <span data-ttu-id="926b5-151">Można jednak tylko monitorowanie kodów stanu, które mają specjalne znaczenie dla danej konfiguracji sieci CDN.</span><span class="sxs-lookup"><span data-stu-id="926b5-151">However, you can choose to only monitor the status codes that have special significance for your CDN configuration.</span></span> <span data-ttu-id="926b5-152">Aby to zrobić, sprawdź kody żądany stan i wyczyść wszystkie inne opcje, a następnie kliknij **Odśwież wykres**.</span><span class="sxs-lookup"><span data-stu-id="926b5-152">To do this, check the desired status codes and clear all other options, then click **Refresh Graph**.</span></span> 

<span data-ttu-id="926b5-153">Można ukryć danych zarejestrowanych dla kodu określonego stanu.</span><span class="sxs-lookup"><span data-stu-id="926b5-153">You can temporarily hide logged data for a particular status code.</span></span>  <span data-ttu-id="926b5-154">W legendzie bezpośrednio pod wykresem kliknij kod stanu, który chcesz ukryć.</span><span class="sxs-lookup"><span data-stu-id="926b5-154">From the legend directly below the graph, click the status code you want to hide.</span></span> <span data-ttu-id="926b5-155">Kod stanu będą natychmiast ukryte wykresu.</span><span class="sxs-lookup"><span data-stu-id="926b5-155">The status code will be immediately hidden from the graph.</span></span> <span data-ttu-id="926b5-156">Ponowne kliknięcie tego kodu stanu spowoduje, że ta opcja będzie wyświetlana ponownie.</span><span class="sxs-lookup"><span data-stu-id="926b5-156">Clicking that status code again will cause that option to be displayed again.</span></span>

## <a name="connections"></a><span data-ttu-id="926b5-157">Połączenia</span><span class="sxs-lookup"><span data-stu-id="926b5-157">Connections</span></span>
![Wykres połączeń](./media/cdn-real-time-stats/cdn-connections.png)

<span data-ttu-id="926b5-159">Ten wykres wskazuje liczbę połączeń ustanowionych do serwerów krawędzi.</span><span class="sxs-lookup"><span data-stu-id="926b5-159">This graph indicates how many connections have been established to your edge servers.</span></span> <span data-ttu-id="926b5-160">Każde żądanie dla zasobu, który przechodzi przez naszych wyników sieci CDN w połączeniu.</span><span class="sxs-lookup"><span data-stu-id="926b5-160">Each request for an asset that passes through our CDN results in a connection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="926b5-161">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="926b5-161">Next Steps</span></span>
* <span data-ttu-id="926b5-162">Bądź na bieżąco z [alertów w czasie rzeczywistym w usłudze Azure CDN](cdn-real-time-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="926b5-162">Get notified with [Real-time alerts in Azure CDN](cdn-real-time-alerts.md)</span></span>
* <span data-ttu-id="926b5-163">Dig głębiej z [zaawansowane raporty HTTP](cdn-advanced-http-reports.md)</span><span class="sxs-lookup"><span data-stu-id="926b5-163">Dig deeper with [advanced HTTP reports](cdn-advanced-http-reports.md)</span></span>
* <span data-ttu-id="926b5-164">Analizowanie [wzorców użycia](cdn-analyze-usage-patterns.md)</span><span class="sxs-lookup"><span data-stu-id="926b5-164">Analyze [usage patterns](cdn-analyze-usage-patterns.md)</span></span>

