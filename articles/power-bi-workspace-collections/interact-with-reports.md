---
title: "Interakcja z raportami za pomocą interfejsu API języka JavaScript | Microsoft Docs"
description: "Interfejs API języka JavaScript usługi Power BI umożliwia łatwe osadzanie raportów usługi Power BI w aplikacjach."
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ROBOTS: NOINDEX
ms.assetid: bdd885d3-1b00-4dcf-bdff-531eb1f97bfb
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 09/20/2017
ms.author: asaxton
ms.openlocfilehash: 62a95807c35fcba15a8e5ffdf340a307dd22a642
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="interact-with-power-bi-reports-using-the-javascript-api"></a>Interakcja z raportami usługi Power BI za pomocą interfejsu API języka JavaScript

Interfejs API języka JavaScript usługi Power BI umożliwia łatwe osadzanie raportów usługi Power BI w aplikacjach. Dzięki interfejsowi API Twoje aplikacje mogą programowo współdziałać z różnymi elementami raportów, takimi jak strony i filtry. W sposób interaktywny sprawia to, że raporty usługi Power BI są bardziej zintegrowaną częścią aplikacji.

> [!IMPORTANT]
> Kolekcje obszarów roboczych usługi Power BI są przestarzałe i będą dostępne do czerwca 2018 roku lub do daty podanej w kontrakcie. Zachęcamy do zaplanowania migracji do usługi Power BI Embedded, aby uniknąć przerw w działaniu aplikacji. Aby uzyskać informacje dotyczące sposobu przeprowadzenia migracji danych do usługi Power BI Embedded, zobacz [How to migrate Power BI Workspace Collections content to Power BI Embedded (Migrowanie zawartości kolekcji obszarów roboczych usługi Power BI do usługi Power BI Embedded)](https://powerbi.microsoft.com/documentation/powerbi-developer-migrate-from-powerbi-embedded/).

Raport usługi Power BI osadza się w aplikacji przy użyciu elementu iframe, który jest obsługiwany w ramach aplikacji. Element iframe działa jak granica między aplikacją i raportem, co widać na poniższej ilustracji:

![Element iframe kolekcji obszarów roboczych usługi Power BI bez interfejsu API języka Javascript](media/interact-with-reports/iframe-without-javacript.png)

Element iframe znacznie ułatwia proces osadzania, ale bez interfejsu API języka JavaScript raport i aplikacja nie mogą ze sobą współdziałać. Ten brak interakcji może tworzyć wrażenie, że raport nie jest tak naprawdę częścią aplikacji. Raport i aplikacja muszą dwukierunkowo komunikować się ze sobą, jak na poniższej ilustracji:

![Element iframe kolekcji obszarów roboczych usługi Power BI z interfejsem API języka Javascript](media/interact-with-reports/iframe-with-javascript.png)

Interfejs API języka JavaScript usługi Power BI pozwala napisać kod, który może bezpiecznie przechodzić przez granicę elementu iframe. Dzięki temu aplikacja może programowo wykonywać akcje w raporcie oraz nasłuchiwać zdarzeń z akcji wykonywanych w raporcie przez użytkowników.

## <a name="what-can-you-do-with-the-power-bi-javascript-api"></a>Co możesz zrobić z interfejsem API języka JavaScript usługi Power BI?

Używając interfejsu API języka JavaScript, możesz zarządzać raportami, przechodzić do stron w raporcie, filtrować raport oraz obsługiwać zdarzenia osadzania. Poniższy diagram przedstawia strukturę interfejsu API.

![Diagram interfejsu API języka JavaScript usługi Power BI](media/interact-with-reports/javascript-api-diagram.png)

### <a name="manage-reports"></a>Zarządzanie raportami
Interfejs API języka Javascript pozwala na zarządzanie zachowaniem na poziomie raportu i strony:

* Bezpieczne osadzanie określonego raportu usługi Power BI w aplikacji — spróbuj [osadzić aplikację pokazową](http://azure-samples.github.io/powerbi-angular-client/#/scenario1)
  * Określanie tokenu dostępu
* Konfigurowanie raportu
  * Włączanie i wyłączanie okienka filtru i okienka nawigacji strony — spróbuj [zaktualizować ustawienia aplikacji pokazowej](http://azure-samples.github.io/powerbi-angular-client/#/scenario6)
  * Ustawianie wartości domyślnych dla stron i filtrów — spróbuj [określić pokazowe ustawienia domyślne](http://azure-samples.github.io/powerbi-angular-client/#/scenario5)
* Włączanie i zamykanie trybu pełnoekranowego

[Więcej informacji na temat osadzania raportu](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embedding-Basics)

### <a name="navigate-to-pages-in-a-report"></a>Przechodzenie do stron w raporcie
Interfejs API języka JavaScript umożliwia odnalezienie wszystkich stron w raporcie i ustawienie bieżącej strony. Wypróbuj [nawigowanie w aplikacji pokazowej](http://azure-samples.github.io/powerbi-angular-client/#/scenario3).

[Więcej informacji o nawigacji na stronie](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Page-Navigation)

### <a name="filter-a-report"></a>Filtrowanie raportu
Interfejs API języka JavaScript zawiera podstawowe i zaawansowane funkcje filtrowania osadzonych raportów i stron raportu. Wypróbuj [filtrowanie aplikacji pokazowej](http://azure-samples.github.io/powerbi-angular-client/#/scenario4) i przejrzyj w tym miejscu niektóre kody wprowadzenia.

#### <a name="basic-filters"></a>Filtry podstawowe
Filtr podstawowy znajduje się na poziomie kolumny lub hierarchii i zawiera listę wartości do dołączenia lub wykluczenia.

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
Filtry zaawansowane używają operatora logicznego ORAZ lub LUB i akceptują jeden lub dwa warunki, z których każdy ma własny operator i wartość. Obsługiwane warunki to:

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

Oprócz wysyłania informacji do elementu iframe, aplikacja może również odbierać informacje na temat następujących zdarzeń przychodzących z elementu iframe:

* Embed
  * loaded
  * error
* Reports
  * pageChanged
  * dataSelected (wkrótce)

[Więcej informacji na temat obsługi zdarzeń](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Handling-Events)

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji o interfejsie API języka JavaScript usługi Power BI kliknij następujące linki:

* [Strona typu Wiki interfejsu API języka JavaScript](https://github.com/Microsoft/PowerBI-JavaScript/wiki)
* [Dokumentacja modelu obiektów](https://microsoft.github.io/powerbi-models/modules/_models_.html)
* [Pokaz na żywo](https://microsoft.github.io/PowerBI-JavaScript/demo/)