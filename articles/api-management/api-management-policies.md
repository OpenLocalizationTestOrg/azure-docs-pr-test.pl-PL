---
title: "zasady usługi API Management aaaAzure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat zasad hello dostępne do użycia w usłudze Azure API Management."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 1cc460cb-8e67-41aa-bc76-bbafc1892798
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 1c468ff37d73359f1dd694b91e20c2ca04f8934e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-policies"></a>API Management policies
W tej sekcji znajdują się informacje na następujące zasady usługi API Management hello. Aby uzyskać informacje dotyczące dodawania i konfigurowania zasad, zobacz [zasad w usłudze API Management](api-management-howto-policies.md).  
  
 Zasady są zaawansowanych możliwości hello system, który umożliwia zachowanie hello toochange hello interfejsu API za pomocą konfiguracji hello wydawcy. Zasady są zbiór instrukcji, które są wykonywane sekwencyjnie na powitania żądania lub odpowiedzi interfejsu API. Popularne instrukcje obejmują Konwersja formatu XML tooJSON i Wywołaj tempa ograniczania toorestrict hello ilość przychodzących od dewelopera. Wiele zasad są dostępne fabrycznej hello.  
  
 Wyrażenie zasad może służyć jako wartości atrybutu lub tekst w żadnym z zasad interfejsu API zarządzania hello, chyba że zasady hello Określa, w przeciwnym razie wartość. Niektóre zasady, takie jak hello [sterowania przepływem](api-management-advanced-policies.md#choose) i [zmiennej zestaw](api-management-advanced-policies.md#set-variable) zasady są oparte na wyrażeniach zasad. Aby uzyskać więcej informacji, zobacz [zaawansowane zasady](api-management-advanced-policies.md#AdvancedPolicies) i [wyrażenie zasad](api-management-policy-expressions.md).  
  
##  <a name="ProxyPolicies"></a>Zasady  
  
-   [Zasady ograniczeń dostępu](api-management-access-restriction-policies.md#AccessRestrictionPolicies)  
  
    -   [Nagłówek HTTP wyboru](api-management-access-restriction-policies.md#CheckHTTPHeader) — wymusza istnienia i/lub wartość nagłówka HTTP.  
  
    -   [Limit szybkości wywołanie przez subskrypcji](api-management-access-restriction-policies.md#LimitCallRate) — użycie uniemożliwia API wzrósł poprzez ograniczenie wywołań szybkości, na podstawie subskrypcji na.  
  
    -   [Limit szybkości wywołanie przez klucz](api-management-access-restriction-policies.md#LimitCallRateByKey) — użycie uniemożliwia API wzrósł ograniczając szybkość połączenia, na podstawie na klucz.  
  
    -   [Ograniczenia adresów IP wywołującego](api-management-access-restriction-policies.md#RestrictCallerIPs) -wywołania filtrów (umożliwia/nie zezwala na) z określonych adresów IP i/lub zakresów adresów.  
  
    -   [Przydział użycia zestawu subskrypcji](api-management-access-restriction-policies.md#SetUsageQuota) — umożliwia tooenforce odnawialnymi lub okres istnienia połączenia woluminu i/lub przepustowości przydziału na podstawie na subskrypcję.  
  
    -   [Przydział użycia zestawu przez klucz](api-management-access-restriction-policies.md#SetUsageQuotaByKey) — umożliwia tooenforce odnawialnymi lub okres istnienia połączenia woluminu i/lub przepustowości przydziału na podstawie według klucza.  
  
    -   [Sprawdź poprawność JWT](api-management-access-restriction-policies.md#ValidateJWT) — wymusza istnienia i ważności wyodrębniony z określonego nagłówka HTTP lub parametr zapytania określony token JWT.  
  
-   [Zasady zaawansowane](api-management-advanced-policies.md#AdvancedPolicies)  
  
    -   [Przepływ kontroli](api-management-advanced-policies.md#choose) — warunkowo stosuje deklaracji zasad oparte na ocenie hello wyrażeń logicznych.  
  
    -   [Przekazanie żądania](api-management-advanced-policies.md#ForwardRequest) -przekazuje hello żądania toohello wewnętrznej bazy danych usługi.  
  
    -   [Zaloguj się tooEvent Centrum](api-management-advanced-policies.md#log-to-eventhub) — wysyła komunikaty w hello określonego formatu tooa obiektu docelowego komunikatu zdefiniowanych przez podmiot rejestratora.  
  
    -   [Spróbuj ponownie](api-management-advanced-policies.md#Retry) -ponownych prób wykonania hello ujęta deklaracji zasad, jeśli i dopóki nie zostanie spełniony warunek hello. Wykonanie jest powtarzany w hello w określonych odstępach czasu i zapasowej toohello określona liczba ponownych prób.  
  
    -   [Odpowiedź zwrócona](api-management-advanced-policies.md#ReturnResponse) -przerwań potoku wykonywania i zwraca hello określona odpowiedź bezpośrednio toohello wywołującego.  
  
    -   [Wyślij żądanie jednokierunkowej](api-management-advanced-policies.md#SendOneWayRequest) — wysyła toohello żądania określony adres URL bez oczekiwania na odpowiedź.  
  
    -   [Wyślij żądanie](api-management-advanced-policies.md#SendRequest) — wysyła toohello żądania określonego adresu URL.  
  
    -   [Ustaw zmienną](api-management-advanced-policies.md#set-variable) -utrwalić wartość w zmiennej o nazwie kontekstu nowsze dostępu.  
  
    -   [Ustawia metodę żądania](api-management-advanced-policies.md#SetRequestMethod) — pozwala toochange metody hello HTTP dla żądania.  
  
    -   [Ustaw kod stanu](api-management-advanced-policies.md#SetStatus) -toohello kod stanu hello HTTP zmiany określona wartość.  
  
    -   [Śledzenia](api-management-advanced-policies.md#Trace) -dodaje ciąg do hello [inspektora interfejsu API](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) danych wyjściowych.  
  
    -   [Poczekaj](api-management-advanced-policies.md#Wait) -oczekuje dla ujęta [żądanie wysłania](api-management-advanced-policies.md#SendRequest), [pobrać wartości z pamięci podręcznej](api-management-caching-policies.md#GetFromCacheByKey), lub [sterowania przepływem](api-management-advanced-policies.md#choose) toocomplete zasad przed kontynuowaniem.  
  
-   [Zasady uwierzytelniania](api-management-authentication-policies.md#AuthenticationPolicies)  
  
    -   [Uwierzytelnianie za pomocą Basic](api-management-authentication-policies.md#Basic) -uwierzytelniania za pomocą usługi wewnętrznej bazy danych przy użyciu uwierzytelniania podstawowego.  
  
    -   [Uwierzytelniania za pomocą certyfikatu klienta](api-management-authentication-policies.md#ClientCertificate) -uwierzytelniania za pomocą usługi wewnętrznej bazy danych przy użyciu certyfikatów klienta.  
  
-   [Caching policies](api-management-caching-policies.md#CachingPolicies)  
  
    -   [Pobierz z pamięci podręcznej](api-management-caching-policies.md#GetFromCache) — wykonaj pamięci podręcznej wyszukiwania i zwracać prawidłową odpowiedź buforowana, jeśli jest dostępna.  
  
    -   [Przechowywanie toocache](api-management-caching-policies.md#StoreToCache) -pamięci podręcznych odpowiedzi zgodnie z toohello określonej konfiguracji kontroli pamięci podręcznej.  
  
    -   [Pobiera wartość z pamięci podręcznej](api-management-caching-policies.md#GetFromCacheByKey) -pobrania elementu pamięci podręcznej według klucza.  
  
    -   [Przechowywana wartość w pamięci podręcznej](api-management-caching-policies.md#StoreToCacheByKey) -przechowywania elementu w pamięci podręcznej hello według klucza.  
  
    -   [Usuń wartość z pamięci podręcznej](api-management-caching-policies.md#RemoveCacheByKey) -usunięcie elementu w pamięci podręcznej hello według klucza.  
  
-   [Zasady międzydomenowe](api-management-cross-domain-policies.md#CrossDomainPolicies)  
  
    -   [Zezwalaj na połączenia między domenami](api-management-cross-domain-policies.md#AllowCrossDomainCalls) — sprawia, że interfejs API hello dostępne od klientów programu Adobe Flash i Microsoft Silverlight bazujące na przeglądarce.  
  
    -   [CORS](api-management-cross-domain-policies.md#CORS) -dodaje współużytkowanie zasobów między źródłami (CORS) obsługuje tooan operacji lub międzydomenowego interfejsu API tooallow wymaga od klientów przeglądarki.  
  
    -   [JSONP](api-management-cross-domain-policies.md#JSONP) — dodaje JSON dopełnienie (JSONP) operacji tooan pomocy technicznej lub międzydomenowego interfejsu API tooallow wymaga od klientów przeglądarki JavaScript.  
  
-   [Zasady transformacji](api-management-transformation-policies.md#TransformationPolicies)  
  
    -   [Konwertuj JSON tooXML](api-management-transformation-policies.md#ConvertJSONtoXML) — konwertuje żądania lub odpowiedzi body z JSON tooXML.  
  
    -   [Konwertuj XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) — konwertuje żądania lub odpowiedzi body z XML tooJSON.  
  
    -   [Znajdowanie i zamienianie ciągów w treści](api-management-transformation-policies.md#Findandreplacestringinbody) — znajduje podciąg żądania lub odpowiedzi i zastępuje go inny podciąg.  
  
    -   [Maski adresów URL w zawartości](api-management-transformation-policies.md#MaskURLSContent) -ponownie zapisuje (maski) łącza w odpowiedzi hello body tak, aby wskazywały toohello równoważne połączenie za pośrednictwem bramy hello.  
  
    -   [Ustaw usługę zaplecza](api-management-transformation-policies.md#SetBackendService) — zmienia hello usługi wewnętrznej bazy danych dla żądania przychodzącego.  
  
    -   [Ustaw treści](api-management-transformation-policies.md#SetBody) -ustawia treść wiadomości powitania żądań przychodzących i wychodzących.  
  
    -   [Set — nagłówek HTTP](api-management-transformation-policies.md#SetHTTPheader) — przypisuje wartość tooan istniejących odpowiedzi i/lub nagłówek żądania lub dodaje nowy nagłówek odpowiedzi i/lub żądania.  
  
    -   [Wartość parametru ciągu zapytania](api-management-transformation-policies.md#SetQueryStringParameter) — dodaje, zastępuje wartość lub usuwa parametru ciągu zapytania żądania.  
  
    -   [Ponowne zapisywanie adresów URL](api-management-transformation-policies.md#RewriteURL) — konwertuje adres URL żądania w postaci toohello publicznego formularza oczekiwane przez usługę sieci web hello.  
  
    -   [Przekształcanie XML za pomocą XSLT](api-management-transformation-policies.md#XSLTransform) — ma zastosowanie tooXML transformacji XSL w treści żądania lub odpowiedzi hello.  
  
## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji, Praca z zasad, zobacz [zasad w usłudze API Management](api-management-howto-policies.md).  
