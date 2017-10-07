---
title: "aaaInteract z raportów za pomocą hello JavaScript API | Dokumentacja firmy Microsoft"
description: "Power BI Embedded, interakcji z raportów za pomocą hello JavaScript API"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: bdd885d3-1b00-4dcf-bdff-531eb1f97bfb
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: 657e4d5cee031bdda173ab3f451cc19b93ddb17b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="interact-with-power-bi-reports-using-hello-javascript-api"></a>Interakcje z raportów usługi Power BI za pomocą hello JavaScript API
Umożliwia Power BI JavaScript API Hello tooeasily możesz osadzić raportów usługi Power BI w aplikacji. Z hello interfejsu API aplikacji programowo zakłócają elementów raportów, takich jak strony i filtry. W sposób interaktywny sprawia to, że raporty usługi Power BI są bardziej zintegrowaną częścią aplikacji.

Osadzanie raportu usługi Power BI w aplikacji odbywa się przy użyciu elementu iframe, która jest obsługiwana w ramach aplikacji hello. Hello iframe pełni funkcję granicy między aplikacji i hello raport, jak widać w powitania po obrazu. 

![Element iframe usługi Power BI Embedded bez interfejsu API języka Javascript](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-1.png)

Hello iframe powoduje osadzanie procesu znacznie łatwiejsze hello, ale bez hello JavaScript API hello raportu i aplikacji nie mogą oddziaływać na siebie. Ten brak interakcji można tworzyć wrażenie hello raportu nie jest częścią aplikacji hello. Raport Hello i aplikacji są naprawdę potrzebne toocommunicate i z powrotem, tak jak powitania po obrazu.

![Element iframe usługi Power BI Embedded z interfejsem API języka Javascript](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-2.png)

Witaj Power BI JavaScript API umożliwia toowrite kod, który można bezpiecznie przekazywane hello iframe granic. Ta umożliwia tooprogrammatically Twojej aplikacji wykonywania akcji w raporcie i toolisten zdarzeń z akcji, które użytkownicy wykonują w raporcie hello.

## <a name="what-can-you-do-with-hello-power-bi-javascript-api"></a>Co należy zrobić z hello Power BI JavaScript API?
Z hello JavaScript API można Zarządzanie raportami, przejdź toopages w raporcie, filtrowanie raportu i obsługi osadzanie zdarzenia. Witaj Poniższy diagram przedstawia hello struktury hello interfejsu API.

![Diagram interfejsu API języka JavaScript usługi Power BI](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-3.png)

### <a name="manage-reports"></a>Zarządzanie raportami
Witaj Javascript API umożliwia zachowanie toomanage na poziomie raportu i strony hello:

* Bezpieczne osadzanie określonego raportu Power BI w aplikacji - spróbuj hello [osadzić pokaz aplikacji](http://azure-samples.github.io/powerbi-angular-client/#/scenario1)
  * Określanie tokenu dostępu
* Skonfiguruj raport hello
  * Włącz i Wyłącz okienko filtru hello i okienko nawigacji strony - spróbuj hello [aktualizowanie ustawień aplikacji demonstracyjnej](http://azure-samples.github.io/powerbi-angular-client/#/scenario6)
  * Określ ustawienia domyślne dla stron i filtry - spróbuj hello [zestaw wartości domyślnych pokaz](http://azure-samples.github.io/powerbi-angular-client/#/scenario5)
* Włączanie i zamykanie trybu pełnoekranowego

[Więcej informacji na temat osadzania raportu](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embedding-Basics)

### <a name="navigate-toopages-in-a-report"></a>Przejdź toopages w raporcie
enbales JavaScript API Hello możesz toodiscover wszystkie strony raportu i tooset hello bieżącej strony. Spróbuj hello [aplikacji demonstracyjnej nawigacji](http://azure-samples.github.io/powerbi-angular-client/#/scenario3).

[Więcej informacji o nawigacji na stronie](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Page-Navigation)

### <a name="filter-a-report"></a>Filtrowanie raportu
Witaj JavaScript API udostępnia podstawowe i zaawansowane filtrowanie możliwości dla osadzonych raporty i strony raportu. Spróbuj hello [filtrowania aplikacji demonstracyjnej](http://azure-samples.github.io/powerbi-angular-client/#/scenario4)i przejrzyj niektórych wprowadzenia kodu.  

#### <a name="basic-filters"></a>Filtry podstawowe
Filtr podstawowe znajduje się na poziomie kolumny lub hierarchii i zawiera listę wartości tooinclude lub wykluczania.

```
const basicFilter: pbi.models.IBasicFilter = {
  $schema: "http://powerbi.com/product/schema#basic",
  target: {
    table: "Store",
    column: "Count"
  },
  operator: "In",
  values: [1,2,3,4]
}
```


#### <a name="advanced-filters"></a>Filtry zaawansowane
Filtry zaawansowane użycie operatora logicznego hello i lub OR i zaakceptuj warunki jeden lub dwa, każdy z własnych operator i wartość. Obsługiwane warunki to:

* None
* LessThan
* LessThanOrEqual
* GreaterThan
* GreaterThanOrEqual
* Contains
* DoesNotContain
* StartsWith
* DoesNotStartWith
* Is
* IsNot
* IsBlank
* IsNotBlank

```
const advancedFilter: pbi.models.IAdvancedFilter = {
  $schema: "http://powerbi.com/product/schema#advanced",
  target: {
    table: "Store",
    column: "Name"
  },
  logicalOperator: "Or",
  conditions: [
    {
      operator: "Contains",
      value: "Wash"
    },
    {
      operator: "Contains",
      value: "Park"
    }
  ]
}
```
[Więcej informacji na temat filtrowania](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Filters)

### <a name="handling-events"></a>Obsługa zdarzeń
Ponadto toosending informacji do hello iframe, aplikację można również odbierać informacji na temat hello następujące zdarzenia pochodzące z elementu iframe hello:

* Embed
  * loaded
  * error
* Reports
  * pageChanged
  * dataSelected (wkrótce)

[Więcej informacji na temat obsługi zdarzeń](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Handling-Events)

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji na temat hello Power BI JavaScript API wyewidencjonować hello następującego łącza:

* [Strona typu Wiki interfejsu API języka JavaScript](https://github.com/Microsoft/PowerBI-JavaScript/wiki)
* [Dokumentacja modelu obiektów](https://microsoft.github.io/powerbi-models/modules/_models_.html)
* Przykłady
  * [Angular](http://azure-samples.github.io/powerbi-angular-client)
  * [Ember](https://github.com/Microsoft/powerbi-ember)
* [Pokaz na żywo](https://microsoft.github.io/PowerBI-JavaScript/demo/)

