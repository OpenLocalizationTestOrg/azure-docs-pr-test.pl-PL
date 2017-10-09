---
title: "aaaFrequently zadawane pytania dotyczące usługi Azure Search | Dokumentacja firmy Microsoft"
description: "Uzyskaj odpowiedzi toocommon pytania dotyczące usługi Microsoft Azure Search"
services: search
author: HeidiSteen
manager: jhubbard
ms.service: search
ms.technology: search
ms.topic: article
ms.date: 08/03/2017
ms.author: heidist
ms.openlocfilehash: 2c573750600d80585b746bfce20d6c0f8df5a262
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-search---frequently-asked-questions-faq"></a>Usługa wyszukiwanie Azure — często zadawane pytania (FAQ)
 
 Znajdź odpowiedzi toocommonly zadawane pytania dotyczące pojęć, kodu i scenariusze związane z tooAzure wyszukiwania.

## <a name="platform"></a>Platforma

### <a name="how-is-azure-search-different-from-full-text-search-in-my-dbms"></a>Jak usługi Azure Search jest inny niż wyszukiwanie pełnotekstowe w mojej DBMS?

Wyszukiwanie Azure obsługuje wiele źródeł danych, [językową analiza wielu języków](https://docs.microsoft.com/rest/api/searchservice/language-support), [analizy niestandardowego dla danych wejściowych danych interesujące i nietypowych](https://docs.microsoft.com/rest/api/searchservice/custom-analyzers-in-azure-search), wyszukaj rangi formantów za pomocą [oceniania Profile](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index)oraz funkcji środowiska użytkownika, takich jak typeahead wyróżnianie trafień i nawigacji aspektowej. Zawiera również inne funkcje, takie jak synonimy i składnia kwerendy sformatowanej, ale te są zwykle nie rozróżnianie funkcji.

### <a name="what-is-hello-difference-between-azure-search-and-elasticsearch"></a>Jaka jest różnica hello Azure Search i Elasticsearch?

Porównując technologii wyszukiwania, klienci często uzyskać charakterystykę na jak usługi Azure Search porównuje Elasticsearch. Klienci, którzy wybierz usługi Azure Search za pośrednictwem Elasticsearch wyszukiwania projektów aplikacji zwykle zrobić ponieważ wprowadziliśmy klucza zadań łatwiejsze lub potrzebują hello wbudowanej integracji z innymi technologiami firmy Microsoft:

+ Wyszukiwanie Azure jest usługą w chmurze pełni zarządzany z wartością 99,9% umów dotyczących poziomu usług (SLA) podczas obsługi administracyjnej z nadmiarowością wystarczające (2 repliki do odczytu, 3 repliki do odczytu i zapisu).
+ Firmy Microsoft [procesorów języka naturalnego](https://docs.microsoft.com/rest/api/searchservice/language-support) oferują analizy inguistic krawędzi.  
+ [Usługa Azure Search indeksatory](search-indexer-overview.md) może przeszukiwać różnych źródeł danych Azure początkowa i przyrostowa indeksowania.
+ Jeśli potrzebne są odpowiedzi szybkie toofluctuations zapytania lub indeksowania woluminów, możesz użyć [suwaków](search-manage.md#scale-up-or-down) w hello Azure portalu lub wykonywania [skrypt programu PowerShell](search-manage-powershell.md), pomijanie zarządzania niezależnego fragmentu bezpośrednio.  
+ [Ocenianie i dostrajania funkcji](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index) Podaj hello oznacza wpływające na wyszukiwania randze poza zapewniają jakie wyszukiwarki hello samodzielnie. 

### <a name="can-i-pause-azure-search-service-and-stop-billing"></a>Można wstrzymać usługi Azure Search i Zatrzymaj rozliczeń?

Nie można wstrzymać usługi hello. Po utworzeniu usługi hello, zasobów obliczeniowych i przestrzeni dyskowej są przydzielone do wyłącznego użytku. Nie jest możliwe toorelease i odzyskania tych zasobów na żądanie. 

## <a name="indexing-operations"></a>Operacje indeksowania

### <a name="backup-and-restore-or-download-and-move-indexes-or-index-snapshots"></a>Indeksy kopii zapasowej i przywracania (lub pobierania i przenieś) lub indeks migawki?

Mimo że można [pobrać definicji indeksu](https://docs.microsoft.com/rest/api/searchservice/get-index) w dowolnym momencie, nie jest dostępna wyodrębniania indeksu, migawki ani funkcja przywracania kopii zapasowej pobierania *wypełnione* indeksu działa w chmurze hello tooa systemu lokalnego, lub Przenoszenie tooanother usługi Azure Search. 

Indeksy są wbudowane i wypełnione z kodu, który zapisu i uruchomić tylko na usłudze Azure Search w chmurze hello. Zazwyczaj klientów, którzy mają toomove usługi tooanother indeksu zrobić, edytując ich toouse kod nowy punkt końcowy i spróbować ponownie indeksowania. Tootake możliwości hello migawki lub utworzyć kopię zapasową indeksu, rzutowanie głos na [User Voice](https://feedback.azure.com/forums/263029-azure-search/suggestions/8021610-backup-snapshot-of-index).

### <a name="can-i-index-from-sql-database-replicas-applies-tooazure-sql-database-indexershttpsdocsmicrosoftcomazuresearchsearch-howto-connecting-azure-sql-database-to-azure-search-using-indexers"></a>Może indeksować z repliki bazy danych SQL (dotyczy zbyt[indeksatory bazy danych SQL Azure](https://docs.microsoft.com/azure/search/search-howto-connecting-azure-sql-database-to-azure-search-using-indexers))

 Nie ma żadnych ograniczeń na powitania Użyj repliki podstawowej lub pomocniczej jako źródła danych, podczas tworzenia indeksu od początku. Odświeżanie indeksu z aktualizacji przyrostowych (uwzględnieniem zmienionych rekordów) wymaga jednak hello repliki podstawowej. To wymaganie jest dostarczany z bazy danych SQL, które gwarantuje Zmień śledzenie na tylko podstawowy replik. Jeśli spróbujesz się przy użyciu repliki pomocniczej dla obciążenia odświeżania indeksu, nie ma żadnej gwarancji, wszystkie dane hello Ci.

## <a name="search-operations"></a>Operacji wyszukiwania

### <a name="can-i-search-across-multiple-indexes"></a>Umożliwia wyszukiwanie w wielu indeksów?

Nie, ta operacja nie jest obsługiwana. Wyszukiwanie jest zawsze tooa zakresie jednego indeksu.

### <a name="can-i-restrict-search-corpus-access-by-user-identity"></a>Czy można ograniczyć dostęp Boże wyszukiwania przez tożsamość użytkownika

Usługa Azure Search nie ma modelu zabezpieczeń opartego na rolach dla dostępu do danych użytkownika. Uwierzytelnianie jest albo pełne prawa lub na poziomie usługi hello jest tylko do odczytu. Niektórzy klienci zostały zaimplementowane rozwiązań opartych na [ `$filter` parametru wyszukiwania](https://docs.microsoft.com/rest/api/searchservice/search-documents), ale co najlepiej jest obejście tego problemu. Jeśli chcesz, aby ta funkcja, rzutowanie głos na [User Voice](https://feedback.azure.com/forums/263029-azure-search/category/86074-security).

### <a name="why-are-there-zero-matches-on-terms-i-know-toobe-valid"></a>Dlaczego są zero odpowiada na warunkach wiem toobe prawidłowy?

najbardziej typowych przypadkach Hello jest nie wiedząc, że każdego typu zapytania obsługuje różne zachowania i poziomy językowe analiz. Wyszukiwanie pełnotekstowe, co hello dominujący obciążenie, obejmuje faza analizy języka, który dzieli warunki dół tooroot formularzy. Ten aspekt analizowania zapytania rzutuje szerszych net za pośrednictwem dopasowania, ponieważ hello tokenami termin jest zgodna z większą liczbą elementów typu Variant.

Jeśli należy wywołać [inne typy zapytań](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) (symbol wieloznaczny wyszukiwania, Wyszukiwanie rozmyte, wyszukiwanie w sąsiedztwie, masz sugestie, między innymi), nie językowe analizą. Warunki są dodawane toohello zapytania drzewa jako — jest. 

### <a name="why-is-hello-search-rank-a-constant-or-equal-score-of-10-for-every-hit"></a>Dlaczego jest hello wyszukiwarkach wynikiem stałej lub równa 1.0 dla każdego trafień?

Domyślnie wyniki wyszukiwania są oceniane na podstawie na powitania [statystyczne właściwości pasujących warunki](search-lucene-query-architecture.md#stage-4-scoring)i uporządkowanych wysokiej toolow w zestawie wyników hello. Jednak niektóre typy (symbol wieloznaczny, prefiksu, wyrażenie regularne) zapytań zawsze współtworzenia stałej wynik toohello ogólną dokumentu wynik. To zachowanie jest celowe. Wyszukiwanie Azure nakłada stałą wynik tooallow dopasowań za pośrednictwem uwzględnione w wynikach hello, bez wywierania wpływu na powitania klasyfikacji toobe rozszerzenia zapytania. 

Na przykład załóżmy, że danych wejściowych "samouczek *" w wyszukiwaniu symboli wieloznacznych tworzy dopasowania "przewodniki", "tourettes" i "tourmaline". Biorąc pod uwagę rodzaj hello tych wyników, nie istnieje sposób wnioskować tooreasonably terminów są większej wartości niż inne. Z tego powodu możemy Ignoruj określenie częstotliwości podczas oceniania wyników w kwerendach typów symboli wieloznacznych, prefiksu i wyrażenia regularnego. Wyniki wyszukiwania na podstawie częściowe danych wprowadzonych podano stałą tooavoid odchylenia do dopasowania potencjalnie nieoczekiwany wynik.

## <a name="design-patterns"></a>Wzorce projektowe

### <a name="what-is-hello-best-approach-for-implementing-localized-search"></a>Co to jest najlepszym rozwiązaniem hello wykonywania wyszukiwania zlokalizowanych?

Większość klientów wybierz pola dedykowanych przez kolekcję po przejściu do toosupporting różnych ustawień regionalnych (języki) w hello sam indeks. Pola ustawień regionalnych była możliwe tooassign odpowiednie analizatora. Na przykład przypisywanie pola tooa analizator francuski Microsoft hello zawierającego ciągi francuskim. Ułatwia także filtrowania. Jeśli wiesz, że zapytanie jest inicjowana na stronie fr-fr, można ograniczyć pola toothis wyników wyszukiwania. Lub Utwórz [profilu oceniania](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index) toogive hello pola więcej względną wagę.

## <a name="next-steps"></a>Następne kroki

To pytanie dotyczące funkcji lub funkcjonalności? Żądania funkcji hello na powitania [witryny User Voice](https://feedback.azure.com/forums/263029-azure-search).

## <a name="see-also"></a>Zobacz też

 [StackOverflow: Usługa Azure Search](https://stackoverflow.com/questions/tagged/azure-search)   
 [Ile wyszukiwanie pełnotekstowe działa w usłudze Azure Search](search-lucene-query-architecture.md)  
 [Co to jest usługa Azure Search?](search-what-is-azure-search.md)

 