---
title: "Statystyka aaaReal czasu w usłudze Azure CDN | Dokumentacja firmy Microsoft"
description: "Statystyki w czasie rzeczywistym udostępnia w czasie rzeczywistym danych dotyczących wydajności hello Azure CDN podczas dostarczania zawartości tooyour klientów."
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
ms.openlocfilehash: 68900a5092b767e45c1fdf9cef2cd03f55f38a6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-stats-in-microsoft-azure-cdn"></a><span data-ttu-id="f9b73-103">Statystyki w czasie rzeczywistym w usłudze Microsoft Azure CDN</span><span class="sxs-lookup"><span data-stu-id="f9b73-103">Real-time stats in Microsoft Azure CDN</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="f9b73-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="f9b73-104">Overview</span></span>
<span data-ttu-id="f9b73-105">W tym dokumencie opisano statystyki w czasie rzeczywistym w usłudze Microsoft Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="f9b73-105">This document explains real-time stats in Microsoft Azure CDN.</span></span>  <span data-ttu-id="f9b73-106">Ta funkcja udostępnia w czasie rzeczywistym danych, takie jak przepustowości, pamięci podręcznej stanów i tooyour równoczesnych połączeń CDN profilu podczas dostarczania zawartości tooyour klientów.</span><span class="sxs-lookup"><span data-stu-id="f9b73-106">This functionality provides real-time data, such as bandwidth, cache statuses, and concurrent connections tooyour CDN profile when delivering content tooyour clients.</span></span> <span data-ttu-id="f9b73-107">Dzięki temu ciągłego monitorowania kondycji hello usługi w dowolnym momencie, w tym zdarzenia dotyczące przejdź na żywo.</span><span class="sxs-lookup"><span data-stu-id="f9b73-107">This enables continuous monitoring of hello health of your service at any time, including go-live events.</span></span>

<span data-ttu-id="f9b73-108">dostępne są następujące wykresy Hello:</span><span class="sxs-lookup"><span data-stu-id="f9b73-108">hello following graphs are available:</span></span>

* [<span data-ttu-id="f9b73-109">Przepustowość</span><span class="sxs-lookup"><span data-stu-id="f9b73-109">Bandwidth</span></span>](#bandwidth)
* [<span data-ttu-id="f9b73-110">Kody stanu</span><span class="sxs-lookup"><span data-stu-id="f9b73-110">Status Codes</span></span>](#status-codes)
* [<span data-ttu-id="f9b73-111">Stany pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="f9b73-111">Cache Statuses</span></span>](#cache-statuses)
* [<span data-ttu-id="f9b73-112">Połączenia</span><span class="sxs-lookup"><span data-stu-id="f9b73-112">Connections</span></span>](#connections)

## <a name="accessing-real-time-stats"></a><span data-ttu-id="f9b73-113">Uzyskiwanie dostępu do statystyki w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="f9b73-113">Accessing real-time stats</span></span>
1. <span data-ttu-id="f9b73-114">W hello [Azure Portal](https://portal.azure.com), Przeglądaj tooyour profilu CDN.</span><span class="sxs-lookup"><span data-stu-id="f9b73-114">In hello [Azure Portal](https://portal.azure.com), browse tooyour CDN profile.</span></span>
   
    ![Blok profilu CDN](./media/cdn-real-time-stats/cdn-profile-blade.png)
2. <span data-ttu-id="f9b73-116">Blok profilu CDN hello, kliknij hello **Zarządzaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f9b73-116">From hello CDN profile blade, click hello **Manage** button.</span></span>
   
    ![Przycisk Zarządzaj blok profilu CDN](./media/cdn-real-time-stats/cdn-manage-btn.png)
   
    <span data-ttu-id="f9b73-118">Otwiera portalu zarządzania Hello CDN.</span><span class="sxs-lookup"><span data-stu-id="f9b73-118">hello CDN management portal opens.</span></span>
3. <span data-ttu-id="f9b73-119">Przesuń kursor myszy hello **Analytics** kartę, a następnie przesuń kursor myszy hello **statystyki w czasie rzeczywistym** wysuwane okno.</span><span class="sxs-lookup"><span data-stu-id="f9b73-119">Hover over hello **Analytics** tab, then hover over hello **Real-Time Stats** flyout.</span></span>  <span data-ttu-id="f9b73-120">Polecenie **HTTP dużego obiektu**.</span><span class="sxs-lookup"><span data-stu-id="f9b73-120">Click on **HTTP Large Object**.</span></span>
   
    ![Portal zarządzania usługi CDN](./media/cdn-real-time-stats/cdn-premium-portal.png)
   
    <span data-ttu-id="f9b73-122">Wykresy statystyki w czasie rzeczywistym Hello są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="f9b73-122">hello real-time stats graphs are displayed.</span></span>

<span data-ttu-id="f9b73-123">Każda z wykresy hello Wyświetla statystyki w czasie rzeczywistym dla hello wybrany przedział czasu, uruchamianie podczas ładowania strony hello.</span><span class="sxs-lookup"><span data-stu-id="f9b73-123">Each of hello graphs displays real-time statistics for hello selected time span, starting when hello page loads.</span></span>  <span data-ttu-id="f9b73-124">Wykresy Hello automatycznie aktualizowane co kilka sekund.</span><span class="sxs-lookup"><span data-stu-id="f9b73-124">hello graphs update automatically every few seconds.</span></span>  <span data-ttu-id="f9b73-125">Witaj **Odśwież wykres** przycisku, jeśli jest obecny, spowoduje wyczyszczenie hello wykresu, po czym zostanie wyświetlona tylko wybrane hello danych.</span><span class="sxs-lookup"><span data-stu-id="f9b73-125">hello **Refresh Graph** button, if present, will clear hello graph, after which it will only display hello selected data.</span></span>

## <a name="bandwidth"></a><span data-ttu-id="f9b73-126">Przepustowość</span><span class="sxs-lookup"><span data-stu-id="f9b73-126">Bandwidth</span></span>
![Wykres przepustowości](./media/cdn-real-time-stats/cdn-bandwidth.png)

<span data-ttu-id="f9b73-128">Witaj **przepustowości** wykres przedstawia hello ilość przepustowości używanej w ramach bieżącej platformie hello za pośrednictwem hello wybrany okres.</span><span class="sxs-lookup"><span data-stu-id="f9b73-128">hello **Bandwidth** graph displays hello amount of bandwidth used for hello current platform over hello selected time span.</span></span> <span data-ttu-id="f9b73-129">Witaj przyciemnione część hello wykres wskazuje użycia przepustowości.</span><span class="sxs-lookup"><span data-stu-id="f9b73-129">hello shaded portion of hello graph indicates bandwidth usage.</span></span> <span data-ttu-id="f9b73-130">Hello dokładną ilość przepustowości aktualnie używane jest wyświetlana bezpośrednio pod hello wykres liniowy.</span><span class="sxs-lookup"><span data-stu-id="f9b73-130">hello exact amount of bandwidth currently being used is displayed directly below hello line graph.</span></span>

## <a name="status-codes"></a><span data-ttu-id="f9b73-131">Kody stanu</span><span class="sxs-lookup"><span data-stu-id="f9b73-131">Status Codes</span></span>
![Wykres kod stanu](./media/cdn-real-time-stats/cdn-status-codes.png)

<span data-ttu-id="f9b73-133">Witaj **kodów stanu** wykres wskazuje, jak często niektórych kody odpowiedzi HTTP dochodzi za pośrednictwem hello wybrany okres.</span><span class="sxs-lookup"><span data-stu-id="f9b73-133">hello **Status Codes** graph indicates how often certain HTTP response codes are occurring over hello selected time span.</span></span>

> [!TIP]
> <span data-ttu-id="f9b73-134">Opis każdej opcji Kod stanu HTTP, zobacz [kody stanu HTTP CDN Azure](https://msdn.microsoft.com/library/mt759238.aspx).</span><span class="sxs-lookup"><span data-stu-id="f9b73-134">For a description of each HTTP status code option, see [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx).</span></span>
> 
> 

<span data-ttu-id="f9b73-135">Bezpośrednio nad hello wykres zostanie wyświetlona lista kodów stanu HTTP.</span><span class="sxs-lookup"><span data-stu-id="f9b73-135">A list of HTTP status codes is displayed directly above hello graph.</span></span> <span data-ttu-id="f9b73-136">Ta lista wskazuje poszczególnych kodów stanu, który można umieścić w hello wykres liniowy i hello bieżąca liczba zdarzeń na sekundę dla tego kodu stanu.</span><span class="sxs-lookup"><span data-stu-id="f9b73-136">This list indicates each status code that can be included in hello line graph and hello current number of occurrences per second for that status code.</span></span> <span data-ttu-id="f9b73-137">Domyślnie wiersz jest wyświetlany dla każdej z tych kodów stanu hello wykresie.</span><span class="sxs-lookup"><span data-stu-id="f9b73-137">By default, a line is displayed for each of these status codes in hello graph.</span></span> <span data-ttu-id="f9b73-138">Jednak można wybrać tooonly kodów stanu hello monitor, które mają specjalne znaczenie dla danej konfiguracji sieci CDN.</span><span class="sxs-lookup"><span data-stu-id="f9b73-138">However, you can choose tooonly monitor hello status codes that have special significance for your CDN configuration.</span></span> <span data-ttu-id="f9b73-139">toodo, sprawdź hello potrzeby kodów stanu i wyczyść wszystkie inne opcje, a następnie kliknij **Odśwież wykres**.</span><span class="sxs-lookup"><span data-stu-id="f9b73-139">toodo this, check hello desired status codes and clear all other options, then click **Refresh Graph**.</span></span> 

<span data-ttu-id="f9b73-140">Można ukryć danych zarejestrowanych dla kodu określonego stanu.</span><span class="sxs-lookup"><span data-stu-id="f9b73-140">You can temporarily hide logged data for a particular status code.</span></span>  <span data-ttu-id="f9b73-141">Z legendy hello bezpośrednio pod hello wykresu kliknij przycisk Kod stanu hello ma toohide.</span><span class="sxs-lookup"><span data-stu-id="f9b73-141">From hello legend directly below hello graph, click hello status code you want toohide.</span></span> <span data-ttu-id="f9b73-142">Kod stanu Hello będą natychmiast ukryte hello wykresu.</span><span class="sxs-lookup"><span data-stu-id="f9b73-142">hello status code will be immediately hidden from hello graph.</span></span> <span data-ttu-id="f9b73-143">Ponowne kliknięcie tego kodu stanu spowoduje toobe tej opcji, ponownie wyświetlone.</span><span class="sxs-lookup"><span data-stu-id="f9b73-143">Clicking that status code again will cause that option toobe displayed again.</span></span>

## <a name="cache-statuses"></a><span data-ttu-id="f9b73-144">Stany pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="f9b73-144">Cache Statuses</span></span>
![Wykres stanów pamięci podręcznej](./media/cdn-real-time-stats/cdn-cache-status.png)

<span data-ttu-id="f9b73-146">Witaj **pamięci podręcznej stanów** wykres wskazuje, jak często niektóre rodzaje pamięci podręcznej stanów dochodzi za pośrednictwem hello wybrany okres.</span><span class="sxs-lookup"><span data-stu-id="f9b73-146">hello **Cache Statuses** graph indicates how often certain types of cache statuses are occurring over hello selected time span.</span></span> 

> [!TIP]
> <span data-ttu-id="f9b73-147">Opis opcji Kod stanu każdego pamięci podręcznej, zobacz [kodów stanu systemu Azure CDN pamięci podręcznej](https://msdn.microsoft.com/library/mt759237.aspx).</span><span class="sxs-lookup"><span data-stu-id="f9b73-147">For a description of each cache status code option, see [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx).</span></span>
> 
> 

<span data-ttu-id="f9b73-148">Zostanie wyświetlona lista kodów stanu pamięci podręcznej bezpośrednio nad hello wykresu.</span><span class="sxs-lookup"><span data-stu-id="f9b73-148">A list of cache status codes is displayed directly above hello graph.</span></span> <span data-ttu-id="f9b73-149">Ta lista wskazuje poszczególnych kodów stanu, który można umieścić w hello wykres liniowy i hello bieżąca liczba zdarzeń na sekundę dla tego kodu stanu.</span><span class="sxs-lookup"><span data-stu-id="f9b73-149">This list indicates each status code that can be included in hello line graph and hello current number of occurrences per second for that status code.</span></span> <span data-ttu-id="f9b73-150">Domyślnie wiersz jest wyświetlany dla każdej z tych kodów stanu hello wykresie.</span><span class="sxs-lookup"><span data-stu-id="f9b73-150">By default, a line is displayed for each of these status codes in hello graph.</span></span> <span data-ttu-id="f9b73-151">Jednak można wybrać tooonly kodów stanu hello monitor, które mają specjalne znaczenie dla danej konfiguracji sieci CDN.</span><span class="sxs-lookup"><span data-stu-id="f9b73-151">However, you can choose tooonly monitor hello status codes that have special significance for your CDN configuration.</span></span> <span data-ttu-id="f9b73-152">toodo, sprawdź hello potrzeby kodów stanu i wyczyść wszystkie inne opcje, a następnie kliknij **Odśwież wykres**.</span><span class="sxs-lookup"><span data-stu-id="f9b73-152">toodo this, check hello desired status codes and clear all other options, then click **Refresh Graph**.</span></span> 

<span data-ttu-id="f9b73-153">Można ukryć danych zarejestrowanych dla kodu określonego stanu.</span><span class="sxs-lookup"><span data-stu-id="f9b73-153">You can temporarily hide logged data for a particular status code.</span></span>  <span data-ttu-id="f9b73-154">Z legendy hello bezpośrednio pod hello wykresu kliknij przycisk Kod stanu hello ma toohide.</span><span class="sxs-lookup"><span data-stu-id="f9b73-154">From hello legend directly below hello graph, click hello status code you want toohide.</span></span> <span data-ttu-id="f9b73-155">Kod stanu Hello będą natychmiast ukryte hello wykresu.</span><span class="sxs-lookup"><span data-stu-id="f9b73-155">hello status code will be immediately hidden from hello graph.</span></span> <span data-ttu-id="f9b73-156">Ponowne kliknięcie tego kodu stanu spowoduje toobe tej opcji, ponownie wyświetlone.</span><span class="sxs-lookup"><span data-stu-id="f9b73-156">Clicking that status code again will cause that option toobe displayed again.</span></span>

## <a name="connections"></a><span data-ttu-id="f9b73-157">Połączenia</span><span class="sxs-lookup"><span data-stu-id="f9b73-157">Connections</span></span>
![Wykres połączeń](./media/cdn-real-time-stats/cdn-connections.png)

<span data-ttu-id="f9b73-159">Ten wykres wskazuje liczbę połączeń zostały ustalonych tooyour serwery krawędzi.</span><span class="sxs-lookup"><span data-stu-id="f9b73-159">This graph indicates how many connections have been established tooyour edge servers.</span></span> <span data-ttu-id="f9b73-160">Każde żądanie dla zasobu, który przechodzi przez naszych wyników sieci CDN w połączeniu.</span><span class="sxs-lookup"><span data-stu-id="f9b73-160">Each request for an asset that passes through our CDN results in a connection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f9b73-161">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f9b73-161">Next Steps</span></span>
* <span data-ttu-id="f9b73-162">Bądź na bieżąco z [alertów w czasie rzeczywistym w usłudze Azure CDN](cdn-real-time-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="f9b73-162">Get notified with [Real-time alerts in Azure CDN](cdn-real-time-alerts.md)</span></span>
* <span data-ttu-id="f9b73-163">Dig głębiej z [zaawansowane raporty HTTP](cdn-advanced-http-reports.md)</span><span class="sxs-lookup"><span data-stu-id="f9b73-163">Dig deeper with [advanced HTTP reports](cdn-advanced-http-reports.md)</span></span>
* <span data-ttu-id="f9b73-164">Analizowanie [wzorców użycia](cdn-analyze-usage-patterns.md)</span><span class="sxs-lookup"><span data-stu-id="f9b73-164">Analyze [usage patterns](cdn-analyze-usage-patterns.md)</span></span>

