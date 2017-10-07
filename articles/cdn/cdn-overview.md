---
title: "Omówienie usługi CDN aaaAzure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jakie hello jest usługa Azure Content Delivery Network (CDN) i w jaki sposób toouse on toodeliver zawartości wysokiej przepustowości przez buforowanie obiektów blob i zawartości statycznej."
services: cdn
documentationcenter: 
author: smcevoy
manager: akucer
editor: 
ms.assetid: 866e0c30-1f33-43a5-91f0-d22f033b16c6
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 02/08/2017
ms.author: v-semcev
ms.openlocfilehash: e0230a6e107969b845985f2f4d357bf93cd40d42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-hello-azure-content-delivery-network-cdn"></a>Omówienie hello Azure sieci dostarczania zawartości (CDN)
> [!NOTE]
> Tym dokumencie opisano, jakie hello jest Azure sieci dostarczania zawartości (CDN), jak działa i hello funkcje każdego produktu Azure CDN.  Jeśli mają tooskip te informacje i przejść proste tooa samouczek na temat toocreate punktu końcowego usługi CDN, zobacz [przy użyciu usługi Azure CDN](cdn-create-new-endpoint.md).  Jeśli chcesz toosee listę bieżące lokalizacje węzłów CDN, zobacz [lokalizacje POP usługi Azure CDN](cdn-pop-locations.md).
> 
> 

Hello Azure Content Delivery Network (CDN) buforuje zawartość statyczną sieci web w strategicznie rozmieszczonych lokalizacjach tooprovide maksymalnej przepływności dostarczania zawartości toousers.  Witaj CDN oferuje deweloperom globalne rozwiązanie umożliwiające dostarczanie zawartości wysokiej przepustowości przez buforowanie zawartości hello w węzłach fizycznych między hello world. 

Witaj przy użyciu zasobów witryny sieci web toocache CDN hello zalety:

* Lepszą wydajność i środowisko dla użytkowników końcowych, zwłaszcza w przypadku, gdy za pomocą aplikacji, w którym jest wiele rund wymagane tooload zawartości.
* Duże skalowanie toobetter obsługiwać natychmiastowe wysokie obciążenie, np. na początku hello produktu uruchamianie zdarzeń.
* Dystrybucję żądań użytkowników i obsługę zawartości z serwerów krawędzi, mniej ruchu jest wysyłane toohello pochodzenia.

## <a name="how-it-works"></a>Jak to działa
![Omówienie usługi CDN](./media/cdn-overview/cdn-overview.png)

1. Użytkownik (Anna) żąda pliku (nazywanego również zasobem) przy użyciu adresu URL ze specjalną nazwą domeny, taką jak `<endpointname>.azureedge.net`.  System DNS kieruje hello żądania toohello najlepiej wykonywania punktu z obecności (POP) lokalizacji.  Zazwyczaj jest to punkt obecności znajdujący się geograficznie najbliżej użytkownika toohello hello.
2. Jeśli serwery krawędzi hello w hello POP nie ma pliku hello w swojej pamięci podręcznej, hello serwer krawędzi żąda pliku hello hello pochodzenia.  Witaj źródła można aplikacji sieci Web platformy Azure, usługa w chmurze Azure, konta magazynu Azure lub dowolnego publicznie dostępny serwer sieci web.
3. Witaj punkt początkowy zwraca hello pliku toohello krawędzi serwera, w tym opcjonalne nagłówki HTTP opisujące pliku hello Time-to-Live (TTL).
4. serwer graniczny Hello buforuje plik hello i zwraca hello pliku toohello oryginalnego obiektu żądającego (Anna).  Plik Hello pozostaje buforowane na serwerze granicznym hello, do momentu wygaśnięcia hello TTL.  Jeśli hello punkt początkowy nie określił wartości TTL, domyślny hello czas wygaśnięcia wynosi siedem dni.
5. Dodatkowych użytkowników może hello żądania sam plik za pomocą tego samego adresu URL i może również być ukierunkowanej toothat tego samego punktu obecności.
6. Jeśli hello czas wygaśnięcia pliku hello nie wygasł, serwer graniczny hello zwraca hello pliku z pamięci podręcznej hello.  Skutkuje to szybszymi czasami reakcji w środowisku użytkownika.

## <a name="azure-cdn-features"></a>Funkcje usługi Azure CDN
Istnieją trzy produkty Azure CDN: **Azure CDN Standard from Akamai**, **Azure CDN Standard from Verizon** i **Azure CDN Premium from Verizon**.  Witaj poniższej tabeli wymieniono hello funkcje dostępne w poszczególnych produktach.

|  | Standard Akamai | Standard Verizon | Premium Verizon |
| --- | --- | --- | --- |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;__Funkcje wydajności i optymalizacje__ |
| [Przyspieszanie witryn dynamicznych](https://docs.microsoft.com/azure/cdn/cdn-dynamic-site-acceleration) | **&#x2713;**  | **&#x2713;** | **&#x2713;** |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Przyspieszanie witryn dynamicznych — Adaptive Image Compression (Adaptacyjna kompresja obrazu)](https://docs.microsoft.com/azure/cdn/cdn-dynamic-site-acceleration#adaptive-image-compression-akamai-only) | **&#x2713;**  |  |  |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Przyspieszanie witryn dynamicznych — Object Prefetch (Pobieranie obiektów z wyprzedzeniem)](https://docs.microsoft.com/azure/cdn/cdn-dynamic-site-acceleration#object-prefetch-akamai-only) | **&#x2713;**  |  |  |
| [Optymalizacja przesyłania strumieniowego wideo](https://docs.microsoft.com/azure/cdn/cdn-media-streaming-optimization) | **&#x2713;**  | \* |  \* |
| [Optymalizacja dużych plików](https://docs.microsoft.com/azure/cdn/cdn-large-file-optimization) | **&#x2713;**  | \* |  \* |
| [Globalne równoważenia obciążenia serwera (usługa GSLB)](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-load-balancing-azure) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Szybkie przeczyszczanie](cdn-purge-endpoint.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Wstępne ładowanie zasobów](cdn-preload-endpoint.md) | |**&#x2713;** |**&#x2713;** |
| [Buforowanie ciągu zapytania](cdn-query-string.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| Podwójny stos protokołów IPv4/IPv6 |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Obsługa protokołu HTTP/2](cdn-http2.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;__Zabezpieczenia__ |
| Obsługa protokołu HTTPS z punktem końcowym usługi CDN |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Protokół HTTPS domen niestandardowych](cdn-custom-ssl.md) | |**&#x2713;** |**&#x2713;** |
| [Obsługa niestandardowych nazw domen](cdn-map-content-to-custom-domain.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Filtrowanie geograficzne](cdn-restrict-access-by-country.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Uwierzytelnianie przy użyciu tokenów](cdn-token-auth.md)|  |  |**&#x2713;**| 
| [Ochrona przed atakami DDOS](https://www.us-cert.gov/ncas/tips/ST04-015) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;__Analiza i raportowanie__ |
| [Podstawowa analiza](cdn-analyze-usage-patterns.md) | **&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Zaawansowane raporty HTTP](cdn-advanced-http-reports.md) | | |**&#x2713;** |
| [Statystyki w czasie rzeczywistym](cdn-real-time-stats.md) | | |**&#x2713;** |
| [Alerty w czasie rzeczywistym](cdn-real-time-alerts.md) | | |**&#x2713;** |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; __Łatwość obsługi__ |
| Łatwa integracja z usługami platformy Azure, takimi jak [Storage](cdn-create-a-storage-account-with-cdn.md), [Cloud Services](cdn-cloud-service-with-cdn.md), [Web Apps](../app-service-web/app-service-web-tutorial-content-delivery-network.md) i [Media Services](../media-services/media-services-portal-manage-streaming-endpoints.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| Zarządzanie za pomocą [interfejsu API REST](https://msdn.microsoft.com/library/mt634456.aspx), [platformy .NET](cdn-app-dev-net.md), [środowiska Node.js](cdn-app-dev-node.md) lub [programu PowerShell](cdn-manage-powershell.md). |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Dostosowywalny, oparty na regułach aparat dostarczania zawartości](cdn-rules-engine.md) | | |**&#x2713;** |
| Ustawienia pamięci podręcznej/nagłówka (przy użyciu [aparatu reguł](cdn-rules-engine.md)) | | |**&#x2713;** |
| Adres URL przekierowania/ponownego napisania (przy użyciu [aparatu reguł](cdn-rules-engine.md)) | | |**&#x2713;** |
| Zasady urządzeń przenośnych (przy użyciu [aparatu reguł](cdn-rules-engine.md)) | | |**&#x2713;** |

\* Firma Verizon obsługuje bezpośrednie dostarczanie dużych plików i multimediów za pomocą usługi ogólnego dostarczania w sieci Web.


> [!TIP]
> Czy jest jakaś funkcja chcesz toosee w usłudze Azure CDN?  [Prześlij nam swoją opinię](https://feedback.azure.com/forums/169397-cdn)! 
> 
> 

## <a name="next-steps"></a>Następne kroki
tooget pracę z usługą CDN, zobacz [przy użyciu usługi Azure CDN](cdn-create-new-endpoint.md).

Jeśli jesteś istniejącym klientem usługi CDN, teraz można zarządzać punktami końcowymi CDN przy użyciu hello [portalu Microsoft Azure](https://portal.azure.com) lub [PowerShell](cdn-manage-powershell.md).

toosee hello sieci CDN w akcji, zapoznaj się z hello [wideo z sesji Konferencji Build 2016](https://azure.microsoft.com/documentation/videos/build-2016-leveraging-the-new-azure-cdn-apis-to-build-wicked-fast-applications/).

Dowiedz się, jak tooautomate Azure CDN z [.NET](cdn-app-dev-net.md) lub [Node.js](cdn-app-dev-node.md).

Aby uzyskać informacje o cenach, zobacz [cennik usługi CDN](https://azure.microsoft.com/pricing/details/cdn/).

