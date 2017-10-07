---
title: "aaaSet się hello słownik biznesowy, dla której działalność znakowanie w usłudze Azure Data Catalog | Dokumentacja firmy Microsoft"
description: "Jak tooarticle wyróżnienia hello firm słownik w wykazie danych Azure do definiowania i przy użyciu wspólnej tootag słownictwa biznesowych zarejestrowanych zasobów danych."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: b3d63dbe-1ae7-499f-bc46-42124e950cd6
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: c9adf663bd08ac3c0c7b5d3551e6af409fe69ebc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-business-glossary-for-governed-tagging"></a>Dla postanowieniom znakowanie zdefiniowanie hello słownik biznesowy
## <a name="introduction"></a>Wprowadzenie
Wykaz danych Azure umożliwia odnajdywanie źródła danych, więc można łatwo odnalezienia i zrozumienia hello źródeł danych muszą tooperform analizy i podejmowanie decyzji. Te możliwości utworzyć hello największy wpływ można odnaleźć i zrozumieć hello szerokiej gamy dostępnych źródeł danych.

Znakowanie jest jedną funkcję wykazu danych, które ułatwia lepsze zrozumienie zasobów danych. Za pomocą znakowania, słowa kluczowe można skojarzyć z zasobów lub kolumnę, co z kolei pozwala na łatwiejsze toodiscover hello zasobów za pomocą wyszukiwania i przeglądania. Znakowanie pomaga również więcej łatwo zrozumieć hello kontekstu i celem hello zasobów.

Jednak znakowanie czasami może spowodować problemy z własnych. Przykłady problemów, które mogą stać się znakowanie to:

* Użyj Hello skrótów w niektórych zasobów i rozszerzonej tekstu na innym. Ta niezgodność przeszkadza hello odnajdywania zasobów, nawet jeśli celem hello został tootag hello zasobów z hello tym samym tagiem.
* Potencjalne zmiany znaczenia, w zależności od kontekstu. Na przykład tag o nazwie *przychodu* na klienta zestawu danych może to oznaczać przychodu przez klienta, ale hello znacznik na kwartał sprzedaży zestawu danych może to oznaczać co kwartał przychodu firmy hello.  

te i inne podobne wyzwania adresów toohelp, Data Catalog zawiera słownik biznesowy.

Za pomocą słownik biznesowy Data Catalog hello, warunki biznesowe klucza i ich definicje toocreate wspólnego słownika biznesowe organizacji można dokumentów. Ta ładu umożliwia spójności danych użycia między hello organizacji. Po zdefiniowaniu termin w hello słownik biznesowy, można go przypisać tooa danych zasobów w katalogu hello. Takie podejście, *postanowieniom znakowanie*, jest hello same podejście jako znakowanie.

## <a name="glossary-availability-and-privileges"></a>Słownik dostępności i uprawnień
Słownik biznesowy Hello jest dostępna tylko w hello Standard Edition usługi Azure Data Catalog. Hello bezpłatnej wersji usługi Data Catalog zawiera słownik i nie ma możliwości dla której działalność znakowanie.

Dostęp można uzyskać słownik biznesowy hello za pośrednictwem hello **słownik** opcję w menu nawigacji portalu wykazu danych hello.  

![Uzyskiwanie dostępu do hello słownik biznesowy](./media/data-catalog-how-to-business-glossary/01-portal-menu.png)

Administratorzy katalogu danych i członkowie słownik hello, roli Administratorzy mogą tworzyć, edytowanie i usuwanie terminów w hello słownik biznesowy. Wszyscy użytkownicy usługi Data Catalog można wyświetlić hello definicje terminów i zasobów tagu z terminów.

![Dodawanie nowych słownik](./media/data-catalog-how-to-business-glossary/02-new-term.png)

## <a name="creating-glossary-terms"></a>Tworzenie terminów
Administratorzy katalogu danych i słownik można tworzyć terminów przez kliknięcie hello **nowy termin** przycisku. Każdy słownik zawiera hello następujące pola:

* Termin hello definicji biznesowa
* Opis, który przechwytuje reguły użyj lub biznesowych hello przeznaczone dla zasobów hello lub kolumny
* Lista uczestników znających hello najbardziej o hello termin
* termin nadrzędny Hello, który definiuje hello hierarchii, w których hello jest zorganizowana termin

## <a name="glossary-term-hierarchies"></a>Słownik terminów hierarchii
Za pomocą słownik biznesowy hello Data Catalog, organizacji można opisać jego słownictwa firm jako hierarchię warunków, a można utworzyć klasyfikację warunki lepiej reprezentuje jego taksonomii biznesowej.

Okres musi być unikatowa na danym poziomie hierarchii. Zduplikowane nazwy są niedozwolone. Nie jest brak toohello Ogranicz liczbę poziomów w hierarchii, ale hierarchii jest często bardziej zrozumiały gdy istnieją trzy poziomy lub mniej.

Użycie Hello hierarchii w słownik biznesowy hello jest opcjonalne. Zostawianie hello termin pola nadrzędnego pusty słownik terminów tworzy listę płaski (z systemem innym niż — hierarchiczna) terminów w hello słownik.  

## <a name="tagging-assets-with-glossary-terms"></a>Znakowanie zasobów z terminów
Po zdefiniowaniu terminów w katalogu hello, środowisko hello znakowania zasoby jest słownik hello toosearch zoptymalizowana, jako użytkownik wpisze tag. Witaj portalu wykazu danych zostanie wyświetlona lista zgodnych toochoose warunki słownik z. Jeśli hello użytkownik wybiera słownik z listy hello, termin hello jest dodawana zasobów toohello jako tag (nazywany także tag słownik). Witaj użytkownika można również toocreate nowy znacznik, wpisując termin, który nie znajduje się w hello słownik (nazywany także tag użytkownika).

![Oznakowanych zasobów danych z jednego użytkownika tagu i dwa tagi słownik](./media/data-catalog-how-to-business-glossary/03-tagged-asset.png)

> [!NOTE]
> Tagi użytkownika są hello tylko do typ tagu obsługiwane w hello bezpłatnej wersji wykazu danych.
>
>

### <a name="hover-behavior-on-tags"></a>Umieść kursor w tagi zachowanie
W portalu wykazu danych hello hello dwa rodzaje tagi są wizualnie distinct i znajdują się różne hover zachowania. Po ustawieniu kursora tag użytkownika widać hello tag tekstu i hello użytkownika lub użytkowników, którzy dodano hello tagu. Po ustawieniu kursora tag słownik można również sprawdzić hello definicja hello słownik i łącze tooopen hello firm słownik tooview hello pełnej definicji okresu hello.

### <a name="search-filters-for-tags"></a>Filtry wyszukiwania tagów
Słownik tagów i tagi użytkownika są można wyszukiwać i zastosować je jako filtrów w polu wyszukiwania.

## <a name="summary"></a>Podsumowanie
Za pomocą słownik biznesowy hello Azure Data Catalog i hello postanowieniom znakowanie go włącza, można zidentyfikować, zarządzanie i odnaleźć zasoby danych w sposób ciągły. Słownik biznesowy Hello podwyższyć poziom uczenie się ich słownictwa firm hello przez członków organizacji. Słownik Hello obsługuje również Przechwytywanie łatwy do rozpoznania metadanych, co ułatwia wykrywanie zasobów i zrozumienia.

## <a name="next-steps"></a>Następne kroki
* [Dokumentacja interfejsu API REST na operacje biznesowe słownik](https://msdn.microsoft.com/library/mt708855.aspx)
