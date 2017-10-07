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
# <a name="http2-support-in-azure-cdn"></a>Obsługa protokołu HTTP/2 w usługi Azure CDN

HTTP/2 jest tooHTTP/1.1\ znaczne zmiany. Zapewnia szybszy wydajności sieci web, czas odpowiedzi obniżona i lepsze środowisko, przy zachowaniu semantyki hello znanych metod HTTP i kodów stanu. Chociaż HTTP/2 jest zaprojektowana toowork z protokołów HTTP i HTTPS, wiele przeglądarek sieci web klienta obsługują tylko HTTP/2 za pośrednictwem protokołu TLS.

###<a name="http2-benefits"></a>Korzyści HTTP/2

Witaj HTTP/2 zalety:

*   **Multipleksowanie i współbieżność**

    Przy użyciu protokołu HTTP 1.1, wielu wprowadzania wielu żądań zasobów wymaga wielu połączeń TCP, a każde połączenie ma zmniejszenie wydajności związane z nią. HTTP/2 umożliwia wielu toobe zasobów żądana pojedynczego połączenia TCP.

*   **Kompresja nagłówka**

    Przez kompresowanie nagłówki hello HTTP obsługiwane zasobów, czas umieszczonego hello jest znacznie ograniczony.

*   **Zależności strumienia**

    Zależności strumienia Zezwalaj powitania klienta serwer toohello tooindicate, którego zasoby mają priorytet.


##<a name="http2-browser-support"></a>Obsługa przeglądarek HTTP/2

Wszystkie główne przeglądarki hello wdrożono Obsługa HTTP/2 w ich bieżącej wersji. Nieobsługiwany przeglądarki zostanie automatycznie rezerwowy tooHTTP/1.1.

|Przeglądarka|Minimalna wersja|
|-------------|------------|
|Przeglądarka Microsoft Edge| 12|
|Google Chrome| 43|
|Mozilla Firefox| 38|
|Opera| 32|
|Safari| 9|

##<a name="enabling-http2-support-in-azure-cdn"></a>Włączanie obsługi protokołu HTTP/2 w Azure CDN

Obsługa protokołu HTTP/2 jest obecnie aktywny dla **Azure CDN from Akamai** i **Azure CDN from Verizon** profilów. Żadne dalsze akcje nie jest wymagana od klientów.

##<a name="next-steps"></a>Następne kroki

Zalety hello toosee HTTP/2 akcji, zobacz [ten pokaz from Akamai](https://http2.akamai.com/demo).

toolearn więcej informacji na temat protokołu HTTP/2, odwiedź hello następujące zasoby:

*   [Strona główna specyfikacji HTTP/2](https://http2.github.io/)
*   [Oficjalna HTTP/2 — często zadawane pytania](https://http2.github.io/faq/)
*   [Informacje o Akamai HTTP/2](https://http2.akamai.com/)

toolearn więcej informacji na temat dostępnych funkcji usługi Azure CDN, zobacz hello [Omówienie usługi Azure CDN](https://azure.microsoft.com/documentation/articles/cdn-overview/).
