---
title: "źródła danych tooannotate aaaHow | Dokumentacja firmy Microsoft"
description: "Wyróżnianie jak tooarticle jak tooannotate zasobów danych w wykazie danych Azure, w tym przyjaznych nazw, tagów, opisów i ekspertów."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 5a7e6bb2-863c-4eca-b614-1c814920d9ed
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 1d1ef34e3f1ef73cdc65129209d938abe1e36c01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooannotate-data-sources"></a>Jak tooannotate źródeł danych
## <a name="introduction"></a>Wprowadzenie
**Microsoft Azure Data Catalog** to usługa w chmurze pełni zarządzana, która służy jako system rejestracji i system odnajdowania źródeł danych przedsiębiorstwa. Innymi słowy Data Catalog jest pomaga osób odnajdywania, zrozumienia i używania źródeł danych oraz tooget organizacje większych zysków z ich istniejących danych. Po zarejestrowaniu źródła danych z wykazu danych metadanych jest kopiowany i indeksowane przez usługę hello, ale hello wątku nie zakończyć. Data Catalog pozwala użytkownikom tooprovide własnych metadane opisowe — takie jak opisy i tagi — toosupplement hello metadanych wyodrębnionych ze źródła danych hello i źródła danych hello toomake więcej toomore zrozumiały dla osób.

## <a name="annotation-and-crowdsourcing"></a>Adnotacja i crowdsourcing
Każdy ma opinii. I to jest to przydatne.
Wykaz danych rozpoznaje, że różni użytkownicy mają różnych perspektyw w źródłach danych przedsiębiorstwa i czy każdy z tych perspektywy może być przydatna. Należy wziąć pod uwagę hello następujących scenariuszy:

* administrator systemu Hello wie hello umowy dotyczącej poziomu usług hello serwerów lub usług tego źródła danych hello hosta.
* administrator bazy danych Hello wie hello kopii zapasowych, harmonogram dla każdej bazy danych i przetwarzania ETL dozwolonych windows hello.
* właściciela systemu Hello wie hello procesu dla źródła danych toohello dostępu toorequest użytkowników.
* steward danych Hello wie, sposób mapowania modelu danych przedsiębiorstwa toohello zasoby hello i atrybuty hello źródła danych.
* Analityk Hello wie, jak dane hello jest używane w kontekście hello hello procesów biznesowych, które obsługuje on.

Każdy z tych perspektywy jest przydatna, a Data Catalog używa crowdsourcing toometadata podejście, umożliwiający każdego jeden toobe przechwycony i używać tooprovide pełnego obrazu zarejestrowanych źródeł danych. Za pomocą portalu wykazu danych hello, każdy użytkownik można dodawać i edytować własne adnotacje, będąc adnotacje stanie tooview udostępnione przez innych użytkowników.

## <a name="different-types-of-annotations"></a>Różne typy adnotacji
Następujące typy adnotacje hello obsługuje wykazu danych:

| Adnotacja | Uwagi |
| --- | --- |
| Przyjazna nazwa |Przyjazne nazwy mogą być dostarczane na poziomie hello danych zasobów, zasobów danych hello toomake bardziej zrozumiały. Przyjazne nazwy są najbardziej przydatne, gdy nazwa obiektu źródłowego hello jest toousers one niezrozumiałe, skróconej lub w przeciwnym razie nie ma istotnego znaczenia. |
| Opis |Opisy mogą być dostarczane na powitania zasobu danych i atrybutu / poziomy kolumny. Opisy są adnotacje dowolnych krótki tekst opisu użytkownika hello perspektywą zasobu danych hello lub jego użyciem. |
| Znaczników (tagów użytkownika) |Tagi mogą być dostarczane na powitania zasobu danych i atrybutu / poziomy kolumny. Tagi użytkownika są zdefiniowane przez użytkownika etykiet, które mogą być używane toocategorize zasobów danych lub atrybutów. |
| Tagi (Słownik znaczniki) |Tagi mogą być dostarczane na powitania zasobu danych i atrybutu / poziomy kolumny. Słownik tagi są centralnego definiowania terminów, które mogą być używane toocategorize zasobów danych lub atrybutów przy użyciu wspólnej taksonomii biznesowej. Aby uzyskać więcej informacji, zobacz [jak tooset się hello słownik biznesowy dla postanowieniom znakowanie](data-catalog-how-to-business-glossary.md) |
| Ekspertów |Eksperci mogą być dostarczane na poziomie hello danych zasobów. Eksperci zidentyfikować użytkowników lub grup z perspektywy ekspertów hello danych i może służyć jako punkty kontaktu dla użytkowników, którzy odnajdywanie hello zarejestrowanego źródła danych i masz pytania, które nie są odbierane przez hello istniejących adnotacji. |
| Żądania dostępu |Informacje o żądaniu dostępu mogą być dostarczane na poziomie hello danych zasobów. Te informacje są dla użytkowników, którzy odnajdywanie źródła danych, że ich nie ma jeszcze tooaccess uprawnienia. Użytkownicy mogą wprowadzać adresu e-mail hello hello użytkownika lub grupę, która udziela dostępu, hello adresu URL procesu hello narzędzia udostępniane użytkownikom toogain potrzeby lub wprowadzić sam proces hello jako tekst. |
| Dokumentacja |Dokumentacja mogą być dostarczane na poziomie hello danych zasobów. Dokumentacja zasobów jest informacji tekstu sformatowanego zawierające łącza i obrazki, a które zapewniają informacje nie są przekazywane za pośrednictwem opisy i tagów. |

## <a name="annotating-multiple-assets"></a>Dodawanie adnotacji do wielu zasobów
Podczas wybierania wielu zasobów danych w portalu wykazu danych hello, użytkowników może dodawać adnotacje do wszystkich wybranych środków w ramach jednej operacji. Adnotacje zastosuje tooall wybrane zasoby, dzięki czemu można łatwo tooselect i podaj opis spójne i zestawy tagów i ekspertów zasobów powiązanych danych w.

> [!NOTE]
> Znaczniki i ekspertów można również podać przy rejestracji zasoby danych przy użyciu danych Data Catalog hello źródła narzędzia rejestracji.
>
>

Po wybraniu wielu tabel i widoków, tylko kolumny, czy wszystkie wybrane dane, które są wspólne dla zasobów będą wyświetlane w portalu wykazu danych hello. Dzięki temu użytkownicy tooprovide tagów i opisy dla wszystkich kolumn z hello takie same nazwy dla wszystkich wybranych zasobów.

## <a name="annotations-and-discovery"></a>Adnotacje i odnajdywania
Podobnie jak hello metadanych wyodrębnionych ze źródła danych hello podczas rejestracji zostanie dodany indeksu wyszukiwania toohello Data Catalog, dostarczone przez użytkownika metadane są również indeksowane. Oznacza to, że nie tylko czy adnotacje ułatwiają użytkownikom toounderstand hello dane, które stwierdzonych, adnotacje również ułatwić użytkownikom toodiscover hello adnotacji danych trwałych wyszukiwanie przy użyciu hello warunkach, które powodują toothem znaczeniu.

## <a name="summary"></a>Podsumowanie
Rejestrowanie źródła danych z wykazu danych sprawia, że wykrywalny danych przez skopiowanie metadanych strukturalnych i opisowy ze źródła danych hello na powitania usługi katalogu. Po zarejestrowaniu źródła danych użytkowników może udostępniać toodiscover łatwiejsze toomake adnotacje i zrozumieć z wewnątrz hello portalu wykazu danych.

## <a name="see-also"></a>Zobacz też
* [Rozpoczynanie pracy z usługą Azure Data Catalog](data-catalog-get-started.md) samouczek krok po kroku szczegółowe informacje dotyczące tooannotate źródeł danych.
