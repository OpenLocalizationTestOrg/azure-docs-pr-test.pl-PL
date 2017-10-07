---
title: "Przegląd interfejsu API REST operacji usług aaaMedia | Dokumentacja firmy Microsoft"
description: "Przegląd interfejsu API REST usługi multimediów"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: a5f1c5e7-ec52-4e26-9a44-d9ea699f68d9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: b54f4d9123486d6cae832c9817688b0f3da5b401
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="media-services-operations-rest-api-overview"></a>Przegląd interfejsu API REST operacji usługi Media Services
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

Witaj **Media Services operacji REST** interfejsu API jest używany do tworzenia zadań, zasobów, zasady dostępu i inne operacje na obiektach w ramach konta usługi Media. Aby uzyskać więcej informacji, zobacz [nośnika usług operacji REST API reference](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference).

Microsoft Azure Media Services to usługa, która akceptuje żądania HTTP na podstawie OData i na pełne JSON lub atom + pub może odpowiedzieć. Ponieważ usługi Media Services spełnia zaleceń dotyczących projektowania tooAzure, występuje zbiór wymagane nagłówki HTTP, które każdy komputer kliencki musi używać podczas łączenia tooMedia usług, a także zestaw opcjonalne nagłówki, które mogą być używane. Witaj poniższych sekcjach opisano hello nagłówki i zleceń HTTP, można użyć podczas tworzenia żądania odbierania odpowiedzi z usługi Media Services.

Ten temat zawiera omówienie sposobu toouse REST v2 z usługi Media Services.

## <a name="considerations"></a>Zagadnienia do rozważenia

Witaj następujące zagadnienia dotyczące stosowane, gdy za pomocą usługi REST.

* Podczas wykonywania zapytania jednostek, istnieje limit 1000 jednostek zwracane w tym samym czasie, ponieważ publiczny v2 REST ogranicza wyniki too1000 wyników zapytania. Należy toouse **Pomiń** i **zająć** (.NET) / **górnej** (REST) zgodnie z opisem w [w tym przykładzie .NET](media-services-dotnet-manage-entities.md#enumerating-through-large-collections-of-entities) i [tego interfejsu API REST przykład](media-services-rest-manage-entities.md#enumerating-through-large-collections-of-entities). 
* Gdy przy użyciu formatu JSON i określając toouse hello **__metadata** — słowo kluczowe w żądaniu hello (na przykład tooreferences obiektu połączonego), należy ustawić hello **Zaakceptuj** nagłówka zbyt[format trybu informacji pełnej JSON ](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/) (zobacz poniższy przykład hello). OData nie rozpoznaje hello **__metadata** właściwości w hello żądania, chyba że jest on ustawiany tooverbose.  
  
        POST https://media.windows.net/API/Jobs HTTP/1.1
        Content-Type: application/json;odata=verbose
        Accept: application/json;odata=verbose
        DataServiceVersion: 3.0
        MaxDataServiceVersion: 3.0
        x-ms-version: 2.11
        Authorization: Bearer <token> 
        Host: media.windows.net
  
        {
            "Name" : "NewTestJob", 
            "InputMediaAssets" : 
                [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3Aba5356eb-30ff-4dc6-9e5a-41e4223540e7')"}}]
        . . . 

## <a name="standard-http-request-headers-supported-by-media-services"></a>Standardowych nagłówków żądania HTTP obsługiwane przez usługę Media Services
Dla każdego wywołania wprowadzone do usługi Media Services to zestaw wymagane nagłówki, które należy uwzględnić w żądaniu, a także zestaw opcjonalne nagłówki można tooinclude. powitania po hello list tabeli wymagane nagłówki:

| Nagłówek | Typ | Wartość |
| --- | --- | --- |
| Autoryzacja |Elementu nośnego |Elementu nośnego jest hello akceptowany tylko mechanizmu autoryzacji. wartość Hello musi także obejmować hello token dostępu udostępniony przez usługę ACS. |
| x-ms-version |Decimal |2.11 |
| DataServiceVersion |Decimal |3.0 |
| MaxDataServiceVersion |Decimal |3.0 |

> [!NOTE]
> Ponieważ usługi Media Services używa OData tooexpose podstawowej repozytorium metadanych zasobów za pośrednictwem interfejsów API REST, hello DataServiceVersion i nagłówki MaxDataServiceVersion powinny być uwzględnione w żadnym żądaniem; Jednak jeśli nie są one następnie obecnie Media Services przyjęto założenie, że wartość DataServiceVersion hello jest 3.0.
> 
> 

następujące Hello jest zestawem opcjonalne nagłówki:

| Nagłówek | Typ | Wartość |
| --- | --- | --- |
| Date |RFC 1123 daty |Sygnatura czasowa żądania hello |
| Zaakceptuj |Typ zawartości |Witaj zażądano typ zawartości odpowiedzi hello takie jak następujące hello:<p> -application/json; odata = verbose<p> -application/atom + xml<p> Odpowiedzi może być innego typu zawartości, takich jak pobieranie obiektu blob, gdy odpowiedź oznaczająca Powodzenie będzie zawierać hello strumienia obiektu blob jako ładunek hello. |
| Zaakceptuj kodowania |Gzip, deflate |GZIP i DEFLATE kodowania, jeśli jest to wymagane. Uwaga: W przypadku dużych zasobów usługi Media Services może zignorować ten nagłówek i zwrócić nieskompresowanych danych. |
| Zaakceptuj języka |"en", "es" i tak dalej. |Określa hello preferowany język hello odpowiedzi. |
| Accept-Charset |Typ zestawu znaków, takich jak "UTF-8" |Domyślne to UTF-8. |
| X-HTTP-Method |Metoda HTTP |Umożliwia klientom lub zapory, które nie obsługują metody HTTP, takie jak toouse PUT i DELETE tych metod, tunneled za pośrednictwem wywołania GET. |
| Typ zawartości |Typ zawartości |Typ zawartości hello treści żądania PUT lub POST żądań. |
| Client-request-id |Ciąg |Wartość zdefiniowane przez obiekt wywołujący, która identyfikuje hello danego żądania. Jeśli jest określony, ta wartość będą uwzględniane w komunikacie odpowiedzi hello jako żądania hello toomap sposób. <p><p>**Ważne**<p>Wartości powinny być ograniczone do 2096b (2 KB). |

## <a name="standard-http-response-headers-supported-by-media-services"></a>Standardowych nagłówków odpowiedzi HTTP obsługiwane przez usługę Media Services
następujące Hello to zestaw nagłówków, które mogą być zwrócone tooyou w zależności od zasobów hello zostały żądania i hello przeznaczone tooperform akcji.

| Nagłówek | Typ | Wartość |
| --- | --- | --- |
| Identyfikator żądania |Ciąg |Unikatowy identyfikator hello bieżącą operację usługi wygenerowany. |
| Client-request-id |Ciąg |Identyfikator określony przez obiekt wywołujący hello w hello oryginalnego żądania, jeśli jest obecny. |
| Date |RFC 1123 daty |Data Hello tego hello żądanie zostało przetworzone. |
| Typ zawartości |Zmienia się |Typ zawartości Hello hello treści odpowiedzi. |
| Kodowanie zawartości |Zmienia się |Gzip i deflate, gdzie to właściwe. |

## <a name="standard-http-verbs-supported-by-media-services"></a>Standardowa zleceń HTTP obsługiwane przez usługę Media Services
Oto Hello pełną listę zleceń HTTP, które mogą być używane podczas wprowadzania HTTP żądania:

| Zlecenie | Opis |
| --- | --- |
| POBIERZ |Zwraca hello bieżącą wartość obiektu. |
| POST |Tworzy obiekt na podstawie danych hello podane lub przesyła polecenia. |
| UMIEŚĆ |Zastępuje obiekt lub tworzy nazwanego obiektu (jeśli jest to wymagane). |
| USUŃ |Usuwa obiekt. |
| SCALANIA |Aktualizuje istniejący obiekt nazwane właściwości zostanie zmieniona. |
| HEAD |Zwraca metadane obiektu dla odpowiedzi GET. |

## <a name="discover-media-services-model"></a>Odnajdywanie modelu usługi Media Services
można toomake Media Services jednostek mogą szybciej odnajdywać, hello $metadata operacji. Umożliwia tooretrieve wszystkie typy jednostek prawidłowe, właściwości jednostki, skojarzenia, funkcji, działania i tak dalej. Witaj poniższy przykład przedstawia sposób tooconstruct hello identyfikatora URI: https://media.windows.net/API/$ metadanych.

Należy dołączyć "? api version=2.x" toohello koniec hello URI tooview hello metadanych w przeglądarce, lub nie ma nagłówka x-ms-version hello w żądaniu.

## <a name="connect-toomedia-services"></a>Połączenie usług tooMedia

Aby uzyskać informacje dotyczące tooconnect toohello AMS interfejsu API, zobacz temat [hello dostępu do interfejsu API usługi Azure Media Services przy użyciu uwierzytelniania usługi Azure AD](media-services-use-aad-auth-to-access-ams-api.md). Po pomyślnym połączeniu toohttps://media.windows.net, otrzymasz 301 przekierowanie, określając inny identyfikator URI usługi multimediów. Należy wykonać kolejne wywołania toohello nowy identyfikator URI.

## <a name="next-steps"></a>Następne kroki

tooaccess interfejsów API usług AMS z REST, zobacz [użycia usługi Azure AD authentication tooaccess hello Azure Media Services API z POZOSTAŁĄ](media-services-rest-connect-with-aad.md).

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

