---
title: "Omówienie usługi Azure CDN | Microsoft Docs"
description: "Dowiedz się, co to jest usługa Azure Content Delivery Network (CDN) i jak z niej korzystać w celu dostarczania zawartości wysokiej przepustowości przez buforowanie obiektów blob i zawartości statycznej."
services: cdn
documentationcenter: 
author: dksimpson
manager: akucer
editor: 
ms.assetid: 866e0c30-1f33-43a5-91f0-d22f033b16c6
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 11/10/2017
ms.author: v-semcev
ms.openlocfilehash: cdcf07b6af2bd915345361c0bda2dcd9abe5486e
ms.sourcegitcommit: 5d3e99478a5f26e92d1e7f3cec6b0ff5fbd7cedf
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/06/2017
---
# <a name="overview-of-the-azure-content-delivery-network"></a>Omówienie usługi Azure Content Delivery Network

Usługa Azure Content Delivery Network (CDN) buforuje statyczną zawartość internetową w strategicznie rozmieszczonych lokalizacjach w celu zapewnienia maksymalnej przepływności umożliwiającej bezpieczne dostarczanie zawartości dla użytkowników. Usługa CDN oferuje deweloperom globalne rozwiązanie umożliwiające szybkie dostarczanie zawartości o wysokiej przepustowości przez zapisywanie zawartości w pamięci podręcznej w węzłach fizycznych na całym świecie. 

> [!NOTE]
> W tym artykule opisano usługę Azure CDN — jej działanie oraz funkcje poszczególnych produktów Azure CDN. Aby pominąć te informacje i wyświetlić samouczek dotyczący tworzenia punktu końcowego usługi CDN, zobacz [Wprowadzenie do usługi Azure CDN](cdn-create-new-endpoint.md). Aby wyświetlić listę bieżących lokalizacji węzłów CDN, zobacz [Lokalizacje POP usługi Azure CDN](cdn-pop-locations.md).

Zalety używania usługi CDN do buforowania zasobów witryn internetowych obejmują:

* Lepszą wydajność i ulepszone środowisko użytkowników końcowych, zwłaszcza w przypadku korzystania z aplikacji, które wymagają wielu rund do załadowania zawartości.
* Duże skalowanie, aby lepiej obsługiwać natychmiastowe wysokie obciążenie, na przykład na początku zdarzenia uruchamiania produktu.
* Dystrybucję żądań użytkowników i obsługę zawartości bezpośrednio z serwerów brzegowych, dzięki czemu do punktu początkowego jest wysyłanych mniej danych.

## <a name="how-it-works"></a>Jak to działa
![Omówienie usługi CDN](./media/cdn-overview/cdn-overview.png)

1. Użytkownik (Anna) żąda pliku (nazywanego również zasobem) przy użyciu adresu URL ze specjalną nazwą domeny, taką jak `<endpointname>.azureedge.net`. System DNS kieruje żądanie do najlepiej działającej lokalizacji punktu obecności (POP, Point of Presence) — zwykle jest to punkt obecności znajdujący się geograficznie najbliżej użytkownika.
2. Jeśli serwery krawędzi w lokalizacji POP nie mają pliku w swojej pamięci podręcznej, serwer krawędzi żąda pliku z punktu początkowego.  Punktem początkowym może być aplikacja sieci Web platformy Azure, usługa Azure Cloud Service, konto usługi Azure Storage lub dowolny publicznie dostępny serwer sieci Web.
3. Punkt początkowy zwraca plik do serwera krawędzi, dołączając opcjonalne nagłówki HTTP opisujące czas wygaśnięcia (TTL, Time-to-Live) pliku.
4. Serwer krawędzi zapisuje plik w pamięci podręcznej i zwraca go do oryginalnego obiektu żądającego (Anna).  Plik pozostaje w pamięci podręcznej na serwerze krawędzi do momentu upłynięcia czasu wygaśnięcia.  Jeśli punkt początkowy nie określił czasu wygaśnięcia, domyślnie wynosi on siedem dni.
5. Dodatkowi użytkownicy mogą następnie zażądać tego samego pliku przy użyciu tego samego adresu URL, a także mogą być kierowani do tego samego punktu obecności.
6. Jeśli czas wygaśnięcia pliku nie upłynął, serwer krawędzi zwraca plik z pamięci podręcznej. Ten proces prowadzi do krótszego czasu reakcji w środowisku użytkownika.

## <a name="azure-cdn-features"></a>Funkcje usługi Azure CDN
Istnieją trzy produkty Azure CDN: **Azure CDN Standard from Akamai**, **Azure CDN Standard from Verizon** i **Azure CDN Premium from Verizon**.  W tabeli poniżej wymieniono funkcje dostępne w poszczególnych produktach.

|  | Standard Akamai | Standard Verizon | Premium Verizon |
| --- | --- | --- | --- |
| __Funkcje wydajności i optymalizacje__ |
| [Przyspieszanie witryn dynamicznych](https://docs.microsoft.com/azure/cdn/cdn-dynamic-site-acceleration) | **&#x2713;**  | **&#x2713;** | **&#x2713;** |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Przyspieszanie witryn dynamicznych — Adaptive Image Compression (Adaptacyjna kompresja obrazu)](https://docs.microsoft.com/azure/cdn/cdn-dynamic-site-acceleration#adaptive-image-compression-akamai-only) | **&#x2713;**  |  |  |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Przyspieszanie witryn dynamicznych — Object Prefetch (Pobieranie obiektów z wyprzedzeniem)](https://docs.microsoft.com/azure/cdn/cdn-dynamic-site-acceleration#object-prefetch-akamai-only) | **&#x2713;**  |  |  |
| [Optymalizacja przesyłania strumieniowego wideo](https://docs.microsoft.com/azure/cdn/cdn-media-streaming-optimization) | **&#x2713;**  | \* |  \* |
| [Optymalizacja dużych plików](https://docs.microsoft.com/azure/cdn/cdn-large-file-optimization) | **&#x2713;**  | \* |  \* |
| [Globalne równoważenia obciążenia serwera (usługa GSLB)](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-load-balancing-azure) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Szybkie przeczyszczanie](cdn-purge-endpoint.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Wstępne ładowanie zasobów](cdn-preload-endpoint.md) | |**&#x2713;** |**&#x2713;** |
| Ustawienia pamięci podręcznej/nagłówka (przy użyciu [reguł buforowania](cdn-caching-rules.md)) |**&#x2713;** |**&#x2713;** | |
| Ustawienia pamięci podręcznej/nagłówka (przy użyciu [aparatu reguł](cdn-rules-engine.md)) | | |**&#x2713;** |
| [Buforowanie ciągu zapytania](cdn-query-string.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| Podwójny stos protokołów IPv4/IPv6 |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Obsługa protokołu HTTP/2](cdn-http2.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| __Bezpieczeństwo__ |
| Obsługa protokołu HTTPS z punktem końcowym usługi CDN |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Protokół HTTPS domen niestandardowych](cdn-custom-ssl.md) | |**&#x2713;** |**&#x2713;** |
| [Obsługa niestandardowych nazw domen](cdn-map-content-to-custom-domain.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Filtrowanie geograficzne](cdn-restrict-access-by-country.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Uwierzytelnianie przy użyciu tokenów](cdn-token-auth.md)|  |  |**&#x2713;**| 
| [Ochrona przed atakami DDOS](https://www.us-cert.gov/ncas/tips/ST04-015) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| __Analiza i raportowanie__ |
| [Dzienniki diagnostyczne platformy Azure](cdn-azure-diagnostic-logs.md) | **&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Raporty podstawowe z usługi Verizon](cdn-analyze-usage-patterns.md) | |**&#x2713;** |**&#x2713;** |
| [Raporty niestandardowe z usługi Verizon](cdn-verizon-custom-reports.md) | |**&#x2713;** |**&#x2713;** |
| [Zaawansowane raporty HTTP](cdn-advanced-http-reports.md) | | |**&#x2713;** |
| [Statystyki w czasie rzeczywistym](cdn-real-time-stats.md) | | |**&#x2713;** |
| [Wydajność węzła brzegowego](cdn-edge-performance.md) | | |**&#x2713;** |
| [Alerty w czasie rzeczywistym](cdn-real-time-alerts.md) | | |**&#x2713;** |
| __Łatwość obsługi__ |
| Łatwa integracja z usługami platformy Azure, takimi jak [Storage](cdn-create-a-storage-account-with-cdn.md), [Cloud Services](cdn-cloud-service-with-cdn.md), [Web Apps](../app-service/app-service-web-tutorial-content-delivery-network.md) i [Media Services](../media-services/media-services-portal-manage-streaming-endpoints.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| Zarządzanie za pomocą [interfejsu API REST](https://msdn.microsoft.com/library/mt634456.aspx), [platformy .NET](cdn-app-dev-net.md), [środowiska Node.js](cdn-app-dev-node.md) lub [programu PowerShell](cdn-manage-powershell.md). |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Dostosowywalny, oparty na regułach aparat dostarczania zawartości](cdn-rules-engine.md) | | |**&#x2713;** |
| Adres URL przekierowania/ponownego napisania (przy użyciu [aparatu reguł](cdn-rules-engine.md)) | | |**&#x2713;** |
| Zasady urządzeń przenośnych (przy użyciu [aparatu reguł](cdn-rules-engine.md)) | | |**&#x2713;** |

\* Firma Verizon obsługuje bezpośrednie dostarczanie dużych plików i multimediów za pomocą usługi ogólnego dostarczania w sieci Web.


> [!TIP]
> Czy jest jakaś funkcja, z której chcesz korzystać w usłudze Azure CDN?  [Prześlij nam swoją opinię](https://feedback.azure.com/forums/169397-cdn)! 
> 
> 

## <a name="next-steps"></a>Następne kroki
Aby zacząć korzystać z usługi CDN, zobacz [Wprowadzenie do usługi Azure CDN](cdn-create-new-endpoint.md).

Jeśli jesteś istniejącym klientem usługi CDN, możesz teraz zarządzać punktami końcowymi usługi CDN za pomocą witryny [Microsoft Azure Portal](https://portal.azure.com) lub programu [PowerShell](cdn-manage-powershell.md).

Aby zobaczyć usługę CDN w akcji, obejrzyj [film wideo z sesji konferencji Build 2016](https://azure.microsoft.com/documentation/videos/build-2016-leveraging-the-new-azure-cdn-apis-to-build-wicked-fast-applications/).

Dowiedz się, jak zautomatyzować usługę Azure CDN przy użyciu platformy [.NET](cdn-app-dev-net.md) lub [Node.js](cdn-app-dev-node.md).

Aby uzyskać informacje o cenach, zobacz [Cennik usługi Content Delivery Network](https://azure.microsoft.com/pricing/details/cdn/).

