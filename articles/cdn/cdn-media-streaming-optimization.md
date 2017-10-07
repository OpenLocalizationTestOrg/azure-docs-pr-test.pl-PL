---
title: "aaaMedia przesyłania strumieniowego optymalizacji za pośrednictwem hello Azure Content Delivery Network"
description: "Optymalizacja strumieniowego przesyłania plików multimedialnych w celu dostarczania smooth"
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: v-semcev
ms.openlocfilehash: a05a86204708c7ea7ef1f9be04323cdda6a2d403
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="media-streaming-optimization-via-hello-azure-content-delivery-network"></a>Multimediów strumieniowych optymalizacji za pośrednictwem hello Azure Content Delivery Network 
 
Użyj wideo wysokiej rozdzielczości zwiększa się na powitania Internet, który tworzy trudności dla dostarczania dużych plików. Klienci oczekują smooth odtwarzania wideo na żądanie lub live wideo zasobów na różnych klientów i sieci na całym świecie hello. Mechanizm dostarczania szybkich i wydajnych multimediów strumieniowych plików jest krytyczne tooensure środowisko płynne i jest przyjemne konsumenta.  

Z powodu hello duże rozmiary i liczba równoczesnych przeglądarki multimediów strumieniowych na żywo jest toodeliver szczególnie trudne. Długie opóźnienia spowodować tooleave użytkowników. Strumienie na żywo nie można buforować wcześniejsze i duże opóźnienia nie są akceptowane tooviewers, dlatego należy dostarczyć fragmenty wideo w odpowiednim czasie. 

wzorce Hello przesyłania strumieniowego zapewniają również pewne wyzwania. Po zwolnieniu popularnych strumień na żywo lub utworzenie nowej serii wideo na żądanie, tysięcy toomillions przeglądarki mogą żądać hello strumienia hello tym samym czasie. W takim przypadku żądanie inteligentnych konsolidacji jest ważna toonot przeciąży hello pochodzenia serwery, kiedy hello zasoby nie są jeszcze buforowane.
 
Hello Azure Content Delivery Network from Akamai oferuje teraz funkcja, która dostarcza przesyłania strumieniowego multimediów zasoby wydajnie toousers między Witaj świecie na dużą skalę. Funkcja Hello zmniejsza opóźnienia, ponieważ redukuje hello obciążenia hello pochodzenia serwerów. Ta funkcja jest dostępna z warstwy cenowej standardowa Akamai hello. 

Hello Azure Content Delivery Network from Verizon zapewnia multimediów strumieniowych bezpośrednio w hello ogólne web dostarczania optymalizacji typu.
 
## <a name="configure-an-endpoint-toooptimize-media-streaming-in-hello-azure-content-delivery-network-from-akamai"></a>Konfigurowanie media toooptimize punktu końcowego przesyłania strumieniowego w hello Azure Content Delivery Network from Akamai
 
Można skonfigurować sieci dostarczania zawartości sieci (CDN) punktu końcowego toooptimize dostarczania dla dużych plików za pomocą hello portalu Azure. Można również użyć naszych interfejsów API REST lub dowolną z hello klienta toodo zestawów SDK to. Witaj poniższe kroki przedstawiają hello za pośrednictwem portalu Azure hello:

1. nowy punkt końcowy na powitania tooadd **profilu CDN** wybierz pozycję **punktu końcowego**.
  
    ![Nowy punkt końcowy](./media/cdn-media-streaming-optimization/01_Adding.png)

2. W hello **zoptymalizowane pod kątem** listy rozwijanej wybierz **wideo na żądanie przesyłania strumieniowego multimediów** zasobów wideo na żądanie. Jeśli to zrobisz, kombinację na żywo i przesyłania strumieniowego wideo na żądanie, wybierz **przesyłania strumieniowego multimediów ogólne**.

    ![Wybrane przesyłania strumieniowego](./media/cdn-media-streaming-optimization/02_Creating.png) 
 
Po utworzeniu punktu końcowego hello stosuje hello optymalizacji dla wszystkich plików spełniających określone kryteria. powitania po sekcji opisano tego procesu. 
 
## <a name="media-streaming-optimizations-for-hello-azure-content-delivery-network-from-akamai"></a>Przesyłanie strumieniowe optymalizacji dla hello Azure Content Delivery Network from Akamai multimediów
 
Nośnika, który optymalizacji transmisji strumieniowej from Akamai ma zastosowanie w przypadku na żywo lub wideo multimediów strumieniowych używa nośnika poszczególne fragmenty dla dostawy. Ten proces różni się od pojedynczego zasobu dużych przesyłane przy użyciu pobierania progresywnego lub za pomocą żądania zakresu bajtów. Dla informacji o stylu dostarczania multimediów, zobacz [optymalizacji plików o dużym](cdn-large-file-optimization.md).


Hello ogólne nośnika dostarczania lub wideo na żądanie dostarczania optymalizacji typów multimediów za pomocą CDN optymalizacje zaplecza toodeliver nośnika zasoby szybciej. Konfiguracje korzysta również trwałych nośnika, na podstawie najlepszych rozwiązań rozpoznane w czasie.

### <a name="caching"></a>Buforowanie

Jeśli hello Azure Content Delivery Network from Akamai wykrywa, że tej zawartości hello jest manifest przesyłania strumieniowego lub fragment, używa innej buforowania czas wygaśnięcia od dostarczania ogólne sieci web. (Zobacz pełną listę hello w hello w poniższej tabeli). Jak zawsze honorowane cache-control lub Expires nagłówki wysyłane z hello źródła. Jeśli hello zasobów nie jest trwały nośnika, buforuje go za pomocą czas wygaśnięcia hello w celu dostarczania ogólne sieci web.

Hello krótki czas buforowania ujemna jest przydatna do odciążania źródła, gdy wielu użytkowników żądają fragmentu, która jeszcze nie istnieje. Przykładem jest strumień na żywo, w którym pakietów hello nie są dostępne z hello źródła tego drugiego. Interwał buforowania już powitania pomaga również w odciążania żądań z hello źródła, ponieważ zawartość wideo zwykle nie jest zmodyfikowany.
 

|    | Ogólne<br> sieci Web<br>dostarczania | Ogólne<br> nośnik<br> przesyłanie strumieniowe | Wideo na żądanie <br>nośnik<br> przesyłanie strumieniowe  
--- | --- | --- | ---
Buforowanie: dodatnią <br> HTTP 200, 203, 300, <br> 301, 302 i 410 | 7 dni |365 dni | 365 dni   
Buforowanie: ujemna <br> HTTP 204, 305, 404, <br> i 405 | Brak | 1 sekunda | 1 sekunda
 
### <a name="deal-with-origin-failure"></a>Postępowania w przypadku niepowodzenia źródła  

Dostarczanie multimediów ogólne i dostarczanie multimediów wideo na żądanie mieć również limit czasu źródła i dziennika ponownych prób, na podstawie najlepszych rozwiązań dla żądania typowe wzorce. Na przykład, ponieważ dostarczania ogólne nośnika jest dla na żywo i dostarczania multimediów wideo na żądanie, używa krótszy limit czasu połączenia powodu toohello harmonogramów rodzaj transmisja strumieniowa na żywo.

Jeśli upłynie limit czasu połączenia, hello CDN ponowi próbę wiele razy przed wysłaniem klienta toohello błąd "504 — Limit czasu bramy". 

Gdy plik jest zgodny hello typ i rozmiar warunki lista plików, hello CDN używa hello zachowania przesyłania strumieniowego multimediów. W przeciwnym razie używa dostarczania ogólne sieci web.
   
### <a name="conditions-for-media-streaming-optimization"></a>Warunki dotyczące multimediów strumieniowych optymalizacji 

Witaj w poniższej tabeli wymieniono hello zbiór toobe kryteria dotyczące multimediów strumieniowych optymalizacji: 
 
Obsługiwane typy przesyłania strumieniowego | Rozszerzenia plików  
--- | ---  
Apple HLS | m3u8, m3u, m3ub, klucza usług terminalowych, aac
Adobe obr. / min | f4m, f4x, drmmeta, bootstrap, f4f,<br>Adres URL seg Frag — struktura <br> (dopasowanie wyrażenia regularnego: ^(/.*)Seq(\d+)-Frag(\d+)
KRESKA | mpd, kreska, divx, ismv, m4s, m4v, mp4, mp4v, <br> sidx, webm, mp4a, m4a, isma
Funkcji Smooth streaming | / manifest/fragmenty/QualityLevels / /
  

 
## <a name="media-streaming-optimizations-for-hello-azure-content-delivery-network-from-verizon"></a>Przesyłanie strumieniowe optymalizacji dla hello Azure Content Delivery Network from Verizon multimediów

Hello Azure Content Delivery Network from Verizon zapewnia przesyłania strumieniowego multimediów zasoby bezpośrednio, za pomocą hello ogólne web dostarczania optymalizacji typu. Kilka funkcji na powitania CDN bezpośrednio pomoc w dostarczaniu zasoby nośnika domyślnie.

### <a name="partial-cache-sharing"></a>Udostępnianie częściowe pamięci podręcznej

Udostępnianie częściowe pamięci podręcznej umożliwia hello CDN tooserve częściowo buforowane zawartości toonew żądań. Na przykład, jeśli hello pierwszego żądania toohello CDN powoduje Chybienie pamięci podręcznej, hello zostaje wysłane żądanie toohello pochodzenia. Chociaż ten niekompletną zawartość jest ładowany do hello CDN pamięci podręcznej, inne żądania toohello CDN można uruchomić pobierania tych danych. 

### <a name="cache-fill-wait-time"></a>Czas oczekiwania wypełnienie pamięci podręcznej

 funkcji czasu oczekiwania wypełnienie pamięci podręcznej Hello wymusza toohold serwer krawędzi hello wszystkie kolejne żądania hello tego samego zasobu do odpowiedzi HTTP, które nagłówki są odbierane z serwera źródłowego hello. Jeśli nagłówki odpowiedzi HTTP z hello źródła napływają przed wygaśnięciem hello, wszystkie żądania, które zostały wstrzymane są udostępniane poza hello rośnie pamięci podręcznej. Na powitania sam czas, hello pamięci podręcznej jest wypełniana przez dane z hello pochodzenia. Czas oczekiwania wypełnienie pamięci podręcznej hello jest domyślnie too3, 000 milisekund. 

