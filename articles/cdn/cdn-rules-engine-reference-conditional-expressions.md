---
title: "wyrażenia warunkowe aparatu reguł aaaAzure CDN | Dokumentacja firmy Microsoft"
description: "Dokumentacja referencyjna dla usługi Azure CDN zasady warunków dopasowania aparatu i funkcje."
services: cdn
documentationcenter: 
author: Lichard
manager: akucer
editor: 
ms.assetid: 669ef140-a6dd-4b62-9b9d-3f375a14215e
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: 39d0754c34a577f77ca87b6fd92e2b6a9e4ff8fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cdn-rules-engine-conditional-expressions"></a>Zasady usługi Azure CDN aparat wyrażeń warunkowych
Ten temat zawiera szczegółowe opisy hello wyrażenia warunkowego dla usługi Azure sieci dostarczania zawartości (CDN) [aparatu reguł](cdn-rules-engine.md).

Pierwsza część reguły Hello jest hello wyrażenia warunkowego.

Wyrażenie warunkowe | Opis
-----------------------|-------------
JEŚLI | Jeśli wyrażenie jest zawsze część hello pierwszą instrukcją w regule. Podobnie jak wszystkie inne wyrażenia warunkowego tej instrukcji IF musi być skojarzony z dopasowania. Jeśli są zdefiniowane nie dodatkowe wyrażenia warunkowego, tego dopasowania określa hello kryterium, które muszą zostać spełnione przed zestawem funkcji mogą być zastosowane tooa żądania.
A JEŚLI | Wyrażenie IF i mogą być dodane tylko po hello następujące typy wyrażenia warunkowe: IF, i jeśli. Go wskazuje, że istnieje inny warunek, które należy spełnić, aby hello początkowego instrukcji IF.
ELSE IF| Wyrażenia ELSE IF określa warunek alternatywną, na którym muszą zostać spełnione przed dokonaniem zestaw funkcji określonych toothis instrukcji ELSE IF. obecność Hello instrukcji ELSE IF wskazuje koniec hello hello poprzednią instrukcję. Witaj wyrażenia warunkowego tylko może być umieszczany po instrukcji ELSE IF innej instrukcji ELSE IF. Oznacza to, że instrukcji ELSE IF mogą być tylko używana toospecify pojedynczy warunek dodatkowe ma toobe spełnione.

**Przykład**: ![CDN zgodne z warunkiem](./media/cdn-rules-engine-reference/cdn-rules-engine-conditional-expression.png)

 > [!TIP]
   > Kolejne reguły mogą zastąpić akcje hello określone przez poprzednie reguły. Przykład: Reguła wychwytywania chroni wszystkie żądania przy użyciu uwierzytelniania opartego na tokenie. Można tworzyć bezpośrednio pod inną regułę toomake wyjątków dla określonych typów żądań.

### <a name="next-steps"></a>Następne kroki
* [Omówienie usługi Azure CDN](cdn-overview.md)
* [Odwołanie do aparatu reguł](cdn-rules-engine-reference.md)
* [Warunki uzgadniania aparatu reguł](cdn-rules-engine-reference-match-conditions.md)
* [Funkcje aparatu reguł](cdn-rules-engine-reference-features.md)
* [Zastępowanie domyślnego zachowania HTTP przy użyciu aparatu reguł hello](cdn-rules-engine.md)
