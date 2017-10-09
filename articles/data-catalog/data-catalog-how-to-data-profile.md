---
title: "źródła danych profilu tooData aaaHow"
description: "Tooarticle jak wyróżnianie jak danych na poziomie tabeli i kolumny tooinclude profile podczas rejestrowania źródła danych w usłudze Azure Data Catalog i jak danych toouse profile toounderstand źródeł danych."
services: data-catalog
documentationcenter: 
author: spelluru
manager: NA
editor: 
tags: 
ms.assetid: 94a8274b-5c9c-4962-a4b1-2fed38a3d919
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: 12c9f38501cdaee903d0dcbbdd0b82395f35a187
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="data-profile-data-sources"></a>Źródła danych profilu danych
## <a name="introduction"></a>Wprowadzenie
**Microsoft Azure Data Catalog** to usługa w chmurze pełni zarządzana, która służy jako system rejestracji i system odnajdowania źródeł danych przedsiębiorstwa. Innymi słowy **Azure Data Catalog** wszystkie o osobach myśl odnajdywania, zrozumienia i używania źródeł danych, a także pomaga organizacjom tooget więcej wartość z ich istniejących danych. Jeśli źródło danych jest zarejestrowana w usłudze **Azure Data Catalog**, jego metadanych jest kopiowany i indeksowane przez usługę hello, ale hello wątku nie istnieje zakończyć.

Witaj **danych profilowania** funkcji **Azure Data Catalog** sprawdza hello danych z obsługiwanych źródeł danych w katalogu i zbiera dane statystyczne i informacje o tych danych. Jest łatwy tooinclude profil zasobów danych. Podczas rejestrowania zasobów danych, wybierz **obejmują dane profilu** w narzędzia rejestracji źródła danych hello.

## <a name="what-is-data-profiling"></a>Co to jest danych profilowania
Dane profilowania sprawdza hello danych w źródle danych hello jest zarejestrowany i zbiera dane statystyczne i informacje o tych danych. Podczas odnajdowania źródła danych statystyki te mogą ułatwić określenie przydatności hello toosolve danych hello problemy biznesowe.

<!-- In [How toodiscover data sources](data-catalog-how-to-discover.md), you learn about **Azure Data Catalog's** extensive search capabilities including searching for data assets that have a profile. See [How tooinclude a data profile when registering a data source](#howto). -->

Witaj następujące źródła danych obsługuje dane profilowania:

* SQL Server (łącznie z bazy danych SQL Azure i usługi Azure SQL Data Warehouse) tabel i widoków
* Oracle tabele i widoki
* Teradata tabele i widoki
* Tabele programu hive

Takie jak profile danych podczas rejestrowania zasobów danych ułatwia użytkownikom odpowiedzi na pytania dotyczące źródeł danych, takich jak:

* Może ona być używane toosolve Mój problem biznesowy?
* Dane hello jest zgodny, standardów tooparticular lub wzorce?
* Jakie są anomalii hello hello źródła danych?
* Co to są potencjalnych problemów o włączenie tych danych do mojej aplikacji?

> [!NOTE]
> Można również dodać toodescribe zasobów tooan dokumentacji jak danych może być zintegrowane z aplikacji. Zobacz [jak źródeł danych toodocument](data-catalog-how-to-documentation.md).
>
>

<a name="howto"/>

## <a name="how-tooinclude-a-data-profile-when-registering-a-data-source"></a>Jak tooinclude danych profilu podczas rejestrowania źródła danych
Jest łatwy tooinclude profilu źródła danych. Podczas rejestrowania źródła danych w hello **toobe obiektów w zarejestrowany** panelu rejestracji źródła danych hello narzędzie, wybierz **obejmują dane profilu**.

![](media/data-catalog-data-profile/data-catalog-register-profile.png)

więcej informacji o toolearn, tooregister źródeł danych, zobacz temat [jak źródeł danych tooregister](data-catalog-how-to-register.md) i [Rozpoczynanie pracy z usługą Azure Data Catalog](data-catalog-get-started.md).

## <a name="filtering-on-data-assets-that-include-data-profiles"></a>Filtrowanie zasobów danych, które dotyczą profili danych
toodiscover zasobów danych, które obejmują profilu danych, mogą obejmować `has:tableDataProfiles` lub `has:columnsDataProfiles` jako jeden z warunkami wyszukiwania.

> [!NOTE]
> Wybieranie **obejmują dane profilu** danych hello narzędzia rejestracji źródła zawiera tabelę i informacje o profilu na poziomie kolumny. Jednak hello interfejsu API usługi Data Catalog pozwala toobe zasoby danych zarejestrowany tylko jeden zestaw uwzględnione informacje o profilu.
>
>

## <a name="viewing-data-profile-information"></a>Wyświetlanie informacji o profilu danych
Po znalezieniu źródła danych odpowiednie za pomocą profilu można wyświetlić szczegółów profilu hello danych. tooview hello danych profilu, zaznacz zasobu danych i wybierz polecenie **profilu danych** w oknie portalu wykazu danych hello.

![](media/data-catalog-data-profile/data-catalog-view.png)

Dane profilu w **Azure Data Catalog** zawiera tabela i kolumna profilu informacje w tym:

### <a name="object-data-profile"></a>Obiekt danych profilu
* Liczba wierszy
* Rozmiar tabeli
* Gdy obiekt hello ostatniej aktualizacji

### <a name="column-data-profile"></a>Kolumny danych profilu
* Typ danych kolumny
* Liczba wartości odrębnych
* Liczba wierszy z wartości NULL
* Minimalna, maksymalna, średnia i odchylenie standardowe dla wartości w kolumnie

## <a name="summary"></a>Podsumowanie
Dane profilowania zawiera dane statystyczne i informacje o zarejestrowane ustalić hello przydatności problemów biznesowych toosolve danych hello toohelp zasobów danych. Wraz z adnotacji i dokumentowanie źródeł danych, danych profilów można umożliwić użytkownikom lepiej zrozumieć dane.

## <a name="see-also"></a>Zobacz też
* [Jak tooregister źródeł danych](data-catalog-how-to-register.md)
* [Rozpoczynanie pracy z usługą Azure Data Catalog](data-catalog-get-started.md)
