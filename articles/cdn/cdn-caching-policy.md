---
title: "aaaManage Azure CDN zasad buforowania w usłudze Azure Media Services | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomanage Azure CDN zasad buforowania w usłudze Azure Media Services."
services: media-services,cdn
documentationcenter: .NET
author: juliako
manager: erikre
editor: 
ms.assetid: be33aecc-6dbe-43d7-a056-10ba911e0e94
ms.service: media-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/04/2017
ms.author: juliako
ms.openlocfilehash: 4c7ee2922fcbb5727e10fbe44fc6e61b79f6917c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-cdn-caching-policy-in-azure-media-services"></a>Zarządzanie Azure CDN buforowanie zasad w usłudze Azure Media Services
Usługa Azure Media Services zapewnia HTTP adaptacyjnego przesyłania strumieniowego i pobierania progresywnego. Oparty na protokole HTTP przesyłania strumieniowego jest wysoce skalowalna z zalet buforowanie w serwera proxy i warstwy CDN, jak również buforowanie po stronie klienta. Punkty końcowe przesyłania strumieniowego zawiera ogólne możliwości przesyłania strumieniowego, a także konfiguracji nagłówków HTTP pamięci podręcznej. Punkty końcowe przesyłania strumieniowego ustawia HTTP Cache-Control: maksymalny wiek i Expires headers. Można uzyskać dodatkowe informacje dotyczące nagłówków HTTP pamięci podręcznej z [adresem W3.org](http://www.w3.org/Protocols/rfc2616/rfc2616-sec13.html).

## <a name="default-caching-headers"></a>Domyślne nagłówki buforowanie
Domyślnie — punkty końcowe przesyłania strumieniowego zastosować 3 dni nagłówków pamięci podręcznej danych przesyłania strumieniowego na żądanie (multimedialna fragmenty/fragmentów) i manifest(playlist). Transmisja strumieniowa na żywo punktów końcowych przesyłania strumieniowego zastosować 3 dni nagłówków pamięci podręcznej danych (multimedialna fragmenty/fragmentów) i nagłówek żądania manifest(playlist) pamięci podręcznej 2 sekundy. Podczas program na żywo włącza tooon żądanie (archiwum na żywo) mają zastosowanie nagłówków pamięci podręcznej z przesyłania strumieniowego na żądanie.

## <a name="azure-cdn-integration"></a>Integracja z usługą Azure CDN
Azure Media Services udostępnia [zintegrowane CDN](https://azure.microsoft.com/updates/azure-media-services-now-fully-integrated-with-azure-cdn/) dla — punkty końcowe przesyłania strumieniowego. Nagłówki kontroli pamięci podręcznej działa w hello sam sposób jak tooCDN punkty końcowe przesyłania strumieniowego włączone punktów końcowych przesyłania strumieniowego. Azure używa CDN przesyłania strumieniowego punkt końcowy skonfigurowany pamięci podręcznej wartości toodefine hello okres istnienia hello wewnętrznie obiektów w pamięci podręcznej i używa również nagłówków tej wartości tooset hello dostarczania pamięci podręcznej. Przy użyciu usługi CDN włączone punktów końcowych przesyłania strumieniowego nie jest zalecane tooset wartości małych pamięci podręcznej. Ustawianie wartości małych obniżyć wydajność hello i zmniejszyć hello zaletą sieci CDN. Nie można z obsługą tooset nagłówków pamięci podręcznej jest mniejszy niż 600 sekund dla sieci CDN punktów końcowych przesyłania strumieniowego.

> [!IMPORTANT]
>Usługa Azure Media Services zawiera pełną integrację z usługą Azure CDN. Za pomocą jednego kliknięcia można zintegrować wszystkich hello dostępne usługi Azure CDN dostawców (Akamai i Verizon) tooyour przesyłania strumieniowego punktu końcowego, włącznie z produktami w sieci CDN w warstwie standardowa i Premium. Aby uzyskać więcej informacji, zobacz [anonsu](https://azure.microsoft.com/blog/standardstreamingendpoint/).
> 
> Opłatami za przesyłanie danych z przesyłania strumieniowego punktu końcowego tooCDN pobiera tylko wyłączonych włączenie hello CDN za pośrednictwem interfejsów API punktu końcowego przesyłania strumieniowego lub przy użyciu sekcji punktu końcowego przesyłania strumieniowego portalu zarządzania Azure. Integracja ręczna lub bezpośrednio tworzenia punktu końcowego usługi CDN przy użyciu interfejsów API usługi CDN lub portalu sekcji nie spowoduje wyłączenie hello danych opłat.

## <a name="configuring-cache-headers-with-azure-media-services"></a>Konfigurowanie nagłówków pamięci podręcznej w usłudze Azure Media Services
Możesz użyć portalu zarządzania Azure lub wartości nagłówka w pamięci podręcznej tooconfigure interfejsów API usługi Azure Media Services.

1. tooconfigure nagłówków pamięci podręcznej za pomocą zarządzania portalu można znaleźć zbyt[jak punkty końcowe przesyłania strumieniowego tooManage](../media-services/media-services-portal-manage-streaming-endpoints.md) sekcji Konfigurowanie hello punktu końcowego przesyłania strumieniowego.
2. W przypadku interfejsu API REST usługi Azure Media Services [StreamingEndpoint](https://msdn.microsoft.com/library/azure/dn783468.aspx#StreamingEndpointCacheControl).
3. Zestaw .NET SDK usługi Azure Media Services [StreamingEndpointCacheControl właściwości](http://go.microsoft.com/fwlink/?LinkId=615302).

## <a name="cache-configuration-precedence-order"></a>Kolejność pierwszeństwa konfiguracji pamięci podręcznej
1. Azure Media Services skonfigurowany pamięci podręcznej wartość zastępuje wartości domyślne.
2. Jeśli nie istnieje konfiguracja ręczna, zastosowanie wartości domyślnych.
3. Domyślnie 2 sekundy nagłówków pamięci podręcznej stosuje toolive przesyłania strumieniowego manifest(playlist) niezależnie od konfiguracji multimediów Azure lub usługi Azure Storage i zastępowanie tej wartości nie jest dostępna.

