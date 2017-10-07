---
title: "aaaAzure rozliczeń interfejsów API Enterprise | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat hello interfejsów API raportowania programowo włączyć dane dotyczące zużycia toopull klientów Enterprise Azure."
services: 
documentationcenter: 
author: aedwin
manager: aedwin
editor: 
tags: billing
ms.assetid: 3e817b43-0696-400c-a02e-47b7817f9b77
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 04/25/2017
ms.author: aedwin
ms.openlocfilehash: 017cecc57ad6bdeb402b5d9d57fc95df9b033a42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-reporting-apis-for-enterprise-customers"></a>Omówienie API raportowania dla przedsiębiorstw
Witaj raportowania interfejsy API umożliwia Enterprise Azure klienci tooprogrammatically ściągania konsumenckich i danych dotyczących rozliczeń do narzędzia do analizy danych preferowany. 

## <a name="enabling-data-access-toohello-api"></a>Włączanie interfejsu API toohello dostępu do danych
* **Generowanie lub pobrać klucza interfejsu API hello** — dziennik toohello Enterprise portal i wykonaj hello samouczka w pomocy - API raportowania. Hello w pierwszej sekcji tego artykułu Pomocy opisano, jak toogenerate lub pobrać klucz hello interfejsu API dla hello określony rejestracji.
* **Przekazując klucze interfejsu API hello** — klucz interfejsu API hello musi toobe przekazany dla każdego wywołania do uwierzytelniania i autoryzacji. Witaj następującej właściwości musi nagłówki toohello HTTP toobe

|Klucz nagłówka żądania | Wartość|
|-|-|
|Autoryzacja| Określ wartość hello w następującym formacie: **elementu nośnego {API_KEY}** <br/> Przykład: eyr elementu nośnego... 09|

## <a name="consumption-apis"></a>Interfejsy API zużycie
Punktu końcowego struktury Swagger jest dostępna [tutaj](https://consumption.azure.com/swagger/ui/index) dla hello interfejsów API opisane poniżej którego powinien Włącz introspection łatwe hello interfejsu API i zestawów SDK klienta toogenerate możliwości hello [AutoRest](https://github.com/Azure/AutoRest) lub [ Swagger CodeGen](http://swagger.io/swagger-codegen/). Począwszy od 1 maja 2014 danych jest dostępna za pośrednictwem tego interfejsu API. 

* **Saldo i Podsumowanie** — Witaj [saldo oraz podsumowanie interfejsu API](billing-enterprise-api-balance-summary.md) oferuje miesięczne podsumowanie informacji na temat salda, nowych zakupów, opłaty za usługę Azure Marketplace, zmiany i nadwyżkowe opłat.

* **Szczegóły użycia** — Witaj [API szczegółów użycia](billing-enterprise-api-usage-detail.md) oferuje zestawienie ilości wykorzystanego i opłat szacowany przy rejestracji. wynik Hello zawiera również informacje dotyczące wystąpień, mierniki i działów. Witaj interfejsu API mogą być przeszukiwane przez okres rozliczeń lub określona data rozpoczęcia i zakończenia. 

* **Opłata magazynu Marketplace** — Witaj [Marketplace magazynu opłat API](billing-enterprise-api-marketplace-storecharge.md) zwraca hello opartej na użyciu marketplace opłat podział według dnia dla hello określonego okresu rozliczeniowego lub daty rozpoczęcia i zakończenia (jeden raz opłaty nie są uwzględniane) .

* **Arkusz cen** — Witaj [API arkusza cen](billing-enterprise-api-pricesheet.md) udostępnia hello stawkę dla każdego licznika dla hello rejestracji i okresu rozliczeniowego. 

## <a name="helper-apis"></a>Interfejsy API pomocy
 **Lista rozliczeń okresów** — Witaj [rozliczeń API okresów](billing-enterprise-api-billing-periods.md) zwraca listę rozliczeń okresów, które mają dane dotyczące zużycia dla hello określonych rejestracji w odwrotnej kolejności chronologicznej. Każdego okresu zawiera właściwość wskazujący trasę interfejsu API toohello dla hello cztery zestawy danych - BalanceSummary, UsageDetails opłat w witrynie Marketplace i arkusza cen.


## <a name="api-response-codes"></a>Kody odpowiedzi interfejsu API  
|Kod stanu odpowiedzi|Komunikat|Opis|
|-|-|-|
|200| OK|Błąd braku|
|401| Brak autoryzacji| Klucz interfejsu API nie został znaleziony, nieprawidłowy, ważność itp.|
|404| Niedostępne| Nie znaleziono punktu końcowego raportu|
|400| Nieprawidłowe żądanie| Nieprawidłowe parametry — zakresy dat, liczb EA itp.|
|500| Błąd serwera| Unexoected błąd podczas przetwarzania żądania| 









