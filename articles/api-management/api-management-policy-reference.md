---
title: "aaaAzure API Reference zasad zarządzania"
description: "Więcej informacji na temat tooconfigure dostępne hello zasad interfejsu API zarządzania."
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.assetid: 9d4ac609-b221-4032-93ae-e27a1254d43d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 7ee194f4d6f172bf836c789cbe8ab732e18a7e0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-policy-reference"></a>Informacje o zasadach usługi Azure API Management
Ta sekcja zawiera indeks dla zasad hello w hello [informacje o zasadach usługi API Management][API Management policy reference]. Aby uzyskać informacje dotyczące dodawania i konfigurowania zasad, zobacz [zasad w usłudze API Management][Policies in API Management].

Wyrażenie zasad może służyć jako wartości atrybutu lub tekst w żadnym z zasad interfejsu API zarządzania hello, chyba że zasady hello Określa, w przeciwnym razie wartość. Niektóre zasady, takie jak hello [sterowania przepływem] [ Control flow] i [zmiennej zestaw] [ Set variable] zasady są oparte na wyrażeniach zasad. Aby uzyskać więcej informacji, zobacz [zaawansowane zasady] [ Advanced policies] i [wyrażenie zasad][Policy expressions]

## <a name="policy-reference-index"></a>Informacje ogólne o zasadach — indeks
* [Zasady ograniczeń dostępu][Access restriction policies]
  * [Nagłówek HTTP wyboru] [ Check HTTP header] — wymusza istnienia i/lub wartość nagłówka HTTP.
  * [Limit szybkości wywołanie przez subskrypcji] [ Limit call rate by subscription] -API uniemożliwia użycie wzrósł poprzez ograniczenie wywołań szybkości, na podstawie subskrypcji na.
  * [Limit szybkości wywołanie przez klucz](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) — użycie uniemożliwia API wzrósł ograniczając szybkość połączenia, na podstawie na klucz.
  * [Ograniczenia adresów IP wywołującego] [ Restrict caller IPs] -wywołania filtrów (umożliwia/nie zezwala na) z określonych adresów IP i/lub zakresów adresów.
  * [Przydział użycia zestawu subskrypcji] [ Set usage quota by subscription] — umożliwia tooenforce odnawialnymi lub okres istnienia połączenia woluminu i/lub przepustowości przydziału na podstawie na subskrypcję.
  * [Przydział użycia zestawu przez klucz](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) — umożliwia tooenforce odnawialnymi lub okres istnienia połączenia woluminu i/lub przepustowości przydziału na podstawie według klucza.
  * [Sprawdź poprawność JWT] [ Validate JWT] — wymusza istnienia i ważności wyodrębniony z określonego nagłówka HTTP lub parametr zapytania określony token JWT.
* [Zaawansowane zasady][Advanced policies]
  * [Przepływ kontroli] [ Control flow] — warunkowo stosuje deklaracji zasad, na podstawie wyników hello oceny hello Boolean [wyrażenia][expressions].
  * [Przekazanie żądania] [ Forward request] -przekazuje hello żądania toohello wewnętrznej bazy danych usługi.
  * [Zaloguj się tooEvent Centrum] [ Log tooEvent Hub] — wysyła komunikaty w hello określonego formatu tooa obiektu docelowego komunikatu zdefiniowane przez [rejestratora](https://msdn.microsoft.com/library/azure/mt592020.aspx#Logger) jednostki.
  * [Spróbuj ponownie](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Retry) -ponownych prób wykonania hello ujęta deklaracji zasad, jeśli i dopóki nie zostanie spełniony warunek hello. Wykonanie jest powtarzany w hello w określonych odstępach czasu i zapasowej toohello określona liczba ponownych prób.
  * [Odpowiedź zwrócona](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) -przerwań potoku wykonywania i zwraca hello określona odpowiedź bezpośrednio toohello wywołującego.
  * [Wyślij żądanie jednokierunkowej](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) — wysyła toohello żądania określony adres URL bez oczekiwania na odpowiedź.
  * [Wyślij żądanie](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) — wysyła toohello żądania określonego adresu URL.
  * [Ustawia metodę żądania](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetRequestMethod) — pozwala toochange metody hello HTTP dla żądania.
  * [Ustaw stan](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetStatus) -toohello kod stanu hello HTTP zmiany określona wartość.
  * [Ustaw zmienną] [ Set variable] -utrwalić wartości w nazwanym [kontekstu] [ context] zmiennej nowsze dostępu.
  * [Śledzenia](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Trace) -dodaje ciąg do hello [inspektora interfejsu API](api-management-howto-api-inspector.md) danych wyjściowych.
  * [Poczekaj](https://msdn.microsoft.com/library/azure/dn894085.aspx#Wait) — czeka na wysyłanie zamkniętych żądań, pobrać wartości z pamięci podręcznej, lub Sterowanie przepływem toocomplete zasad przed kontynuowaniem.
* [Zasady uwierzytelniania][Authentication policies]
  * [Uwierzytelnianie za pomocą Basic] [ Authenticate with Basic] -uwierzytelniania za pomocą usługi wewnętrznej bazy danych przy użyciu uwierzytelniania podstawowego.
  * [Uwierzytelniania za pomocą certyfikatu klienta] [ Authenticate with client certificate] -uwierzytelniania za pomocą usługi wewnętrznej bazy danych przy użyciu certyfikatów klienta.
* [Buforowanie zasad][Caching policies] 
  * [Pobierz z pamięci podręcznej] [ Get from cache] -wykonaj pamięci podręcznej wyszukiwania i zwracać prawidłową odpowiedź buforowana, jeśli jest dostępna.
  * [Przechowywanie toocache] [ Store toocache] -pamięci podręcznych odpowiedzi zgodnie z toohello określonej konfiguracji kontroli pamięci podręcznej.
  * [Pobiera wartość z pamięci podręcznej](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) -pobrania elementu pamięci podręcznej według klucza.
  * [Przechowywana wartość w pamięci podręcznej](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) -przechowywania elementu w pamięci podręcznej hello według klucza.
  * [Usuń wartość z pamięci podręcznej](https://msdn.microsoft.com/en-us/library/dn894086.aspx#RemoveCacheByKey) -usunięcie elementu w pamięci podręcznej hello według klucza.
* [Krzyżowe zasady domeny][Cross domain policies] 
  * [Zezwalaj na połączenia między domenami] [ Allow cross-domain calls] — sprawia, że interfejs API hello dostępne od klientów programu Adobe Flash i Microsoft Silverlight bazujące na przeglądarce.
  * [CORS] [ CORS] -dodaje współużytkowanie zasobów między źródłami (CORS) obsługuje tooan operacji lub międzydomenowego interfejsu API tooallow wymaga od klientów przeglądarki.
  * [JSONP] [ JSONP] — dodaje JSON dopełnienie (JSONP) operacji tooan pomocy technicznej lub międzydomenowego interfejsu API tooallow wymaga od klientów przeglądarki JavaScript.
* [Zasad przekształcania][Transformation policies] 
  * [Konwertuj JSON tooXML] [ Convert JSON tooXML] — konwertuje żądania lub odpowiedzi body z JSON tooXML.
  * [Konwertuj XML tooJSON] [ Convert XML tooJSON] — konwertuje żądania lub odpowiedzi body z XML tooJSON.
  * [Znajdowanie i zamienianie ciągów w treści] [ Find and replace string in body] — znajduje podciąg żądania lub odpowiedzi i zastępuje go inny podciąg.
  * [Maski adresów URL w zawartości] [ Mask URLs in content] -ponownie zapisuje (maski) łącza w odpowiedzi hello body tak, aby wskazywały toohello równoważne połączenie za pośrednictwem bramy hello.
  * [Ustaw usługę zaplecza] [ Set backend service] — zmienia hello usługi wewnętrznej bazy danych dla żądania przychodzącego.
  * [Ustaw treści] [ Set body] -ustawia treść wiadomości powitania żądań przychodzących i wychodzących.
  * [Set — nagłówek HTTP] [ Set HTTP header] — przypisuje wartość tooan istniejących odpowiedzi i/lub nagłówek żądania lub dodaje nowy nagłówek odpowiedzi i/lub żądania.
  * [Wartość parametru ciągu zapytania] [ Set query string parameter] — dodaje, zastępuje wartość lub usuwa parametru ciągu zapytania żądania.
  * [Ponowne zapisywanie adresów URL] [ Rewrite URL] — konwertuje adres URL żądania w postaci toohello publicznego formularza oczekiwane przez usługę sieci web hello.

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji na wyrażenia zasad Zobacz powitania po wideo.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Policy-Expressions-in-Azure-API-Management/player]
> 
> 

[Access restriction policies]: https://msdn.microsoft.com/library/azure/dn894078.aspx
[Check HTTP header]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#CheckHTTPHeader
[Limit call rate by subscription]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#LimitCallRate
[Restrict caller IPs]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#RestrictCallerIPs
[Set usage quota by subscription]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#SetUsageQuota
[Validate JWT]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT

[Advanced policies]: https://msdn.microsoft.com/library/azure/dn894085.aspx
[Control flow]: https://msdn.microsoft.com/library/azure/dn894085.aspx#choose
[Set variable]: https://msdn.microsoft.com/library/azure/dn894085.aspx#set_variable
[expressions]: https://msdn.microsoft.com/library/azure/dn910913.aspx
[context]: https://msdn.microsoft.com/library/azure/ea160028-fc04-4782-aa26-4b8329df3448#ContextVariables
[Forward request]: https://msdn.microsoft.com/library/azure/dn894085.aspx#ForwardRequest
[Log tooEvent Hub]: https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub

[Authentication policies]: https://msdn.microsoft.com/library/azure/dn894079.aspx
[Authenticate with Basic]: https://msdn.microsoft.com/library/azure/061702a7-3a78-472b-a54a-f3b1e332490d#Basic
[Authenticate with client certificate]: https://msdn.microsoft.com/library/azure/061702a7-3a78-472b-a54a-f3b1e332490d#ClientCertificate
[Caching policies]: https://msdn.microsoft.com/library/azure/dn894086.aspx
[Get from cache]: https://msdn.microsoft.com/library/azure/8147199c-24d8-439f-b2a9-da28a70a890c#GetFromCache
[Store toocache]: https://msdn.microsoft.com/library/azure/8147199c-24d8-439f-b2a9-da28a70a890c#StoreToCache

[Cross domain policies]: https://msdn.microsoft.com/library/azure/dn894084.aspx
[Allow cross-domain calls]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#AllowCrossDomainCalls
[CORS]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#CORS
[JSONP]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#JSONP

[Transformation policies]: https://msdn.microsoft.com/library/azure/dn894083.aspx
[Convert JSON tooXML]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#ConvertJSONtoXML
[Convert XML tooJSON]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#ConvertXMLtoJSON
[Find and replace string in body]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#Findandreplacestringinbody
[Mask URLs in content]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#MaskURLSContent
[Set backend service]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#SetBackendService
[Set body]: https://msdn.microsoft.com/library/azure/dn894083.aspx#SetBody
[Set HTTP header]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#SetHTTPheader
[Set query string parameter]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#SetQueryStringParameter
[Rewrite URL]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#RewriteURL



[Policies in API Management]: api-management-howto-policies.md
[API Management policy reference]: https://msdn.microsoft.com/library/azure/dn894081.aspx

[Policy expressions]: https://msdn.microsoft.com/library/azure/dn910913.aspx


