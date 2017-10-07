---
title: "zalecenia dotyczące aaaPerformance — baza danych SQL Azure | Dokumentacja firmy Microsoft"
description: "Witaj bazy danych SQL Azure zawiera zalecenia dotyczące bazy danych SQL, które może poprawić wydajność kwerend bieżącej."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: 1db441ff-58f5-45da-8d38-b54dc2aa6145
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: sstein
ms.openlocfilehash: 77db338a0a395aec78c9e02849ae5ba4f2d01680
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="performance-recommendations"></a>Zalecenia dotyczące wydajności

Baza danych SQL Azure uzyskuje informacje o dostosowuje się z aplikacją i zawiera zalecenia dostosowane, umożliwiając toomaximize hello wydajności baz danych SQL. Wydajność jest ciągle oceniane analizując Twojej historii użycia bazy danych SQL. zalecenia Hello, które są dostarczane są oparte na wzorzec obciążenia unikatowy bazy danych i zwiększyć jej wydajność.

> [!NOTE]
> Zalecanym sposobem stosowania zaleceń jest przez włączenie "Automatycznego dostrajania" w bazie danych. Aby uzyskać więcej informacji, zobacz [automatycznego dostrajania](sql-database-automatic-tuning.md).
>

## <a name="create-index-recommendations"></a>Utwórz zalecenia dotyczące indeksu
Baza danych SQL Azure stale monitoruje zapytania hello wykonywana i identyfikuje hello indeksów, które może poprawić wydajność hello. Po utworzeniu za mało pewność, że indeks niektórych brakuje, nowy **Utwórz indeks** zalecenie zostanie utworzony. Azure zaufania kompilacji bazy danych SQL przez określenie indeksu hello przyrost wydajności doprowadzi do czasu. W zależności od hello szacowany są bardziej wydajne zalecenia są sklasyfikowane jako wysoki, średni lub niski. 

Utworzone za pomocą zalecenia dotyczące indeksów są zawsze oznaczonej jako auto_created indeksów. Można sprawdzić, które indeksy są auto_created analizując sys.indexes widoku. Automatycznie utworzone indeksy nie blokować polecenia ALTER/Zmień nazwę. Jeśli spróbujesz toodrop hello kolumny, która ma automatycznie utworzony indeks nad nim polecenia hello przekazuje i hello automatycznie utworzone indeksu zostało porzucone z poleceniem hello również. Zwykłych indeksów uniemożliwiają hello polecenie ALTER/Zmień nazwę kolumny, które są indeksowane.

Po utworzenia hello zastosowano zalecenie dotyczące indeksu, bazy danych SQL Azure zostanie porównany wydajność kwerend hello hello linię bazową wydajności. Jeśli nowy indeks ulepszenia wydajności hello, zalecenie zostanie oznaczone jako pomyślnie i wpływ raport będzie dostępny. W przypadku, gdy indeks hello nie Przełącz hello korzyści, zostanie automatycznie przywrócony. W ten sposób baza danych SQL Azure zapewnia, że za pomocą zalecenia tylko zwiększy wydajność bazy danych hello.

Wszelkie **Utwórz indeks** zalecenie ma wycofywania zasad, które nie pozwalają na stosowanie hello zalecenie, jeśli użycie jednostek dtu w warstwie bazy danych lub puli hello przekracza 80% w ostatnich 20 minut lub jeśli magazyn hello jest ponad 90% użycia. W takim przypadku zostanie przełożone zalecenie hello.

## <a name="drop-index-recommendations"></a>Zalecenia dotyczące usuwania indeksów
Ponadto toodetecting brakuje indeksu, bazy danych SQL Azure stale analizuje wydajność hello istniejące indeksy. Jeśli indeks nie jest używany, baza danych SQL Azure zaleci usunięcie go. W obu przypadkach zaleca się porzucenie indeksu:
* Indeks jest duplikat nazwy innego indeksu (sama indeksowane i zawiera kolumny, schemat partycji i filtrów)
* Indeks nie jest używana przez dłuższy okres (93 dni)

Zalecenia dotyczące usuwania indeksów również przejść przez weryfikacji powitania po implementacji. Jeśli lepsza wydajność hello hello wpływ raport będzie dostępny. W przypadku wykrycia obniżenia wydajności zalecenie zostaną cofnięte.


## <a name="parameterize-queries-recommendations"></a>Parametryzacja zapytań zalecenia
**Parametryzacja zapytań** zalecenia są wyświetlane po mieć jeden lub więcej zapytań, które są stale zwrócenie, ale na końcu hello tego samego planu wykonania zapytania. Ten warunek otwiera tooapply możliwości wymuszone parametryzacja, co pozwoli plany zapytań toobe w pamięci podręcznej i użyć ponownie w hello przyszłych poprawy wydajności i zmniejszenia użycia zasobów. 

Każdej kwerendy początkowo wystawiony na podstawie programu SQL Server musi mieć toogenerate toobe skompilowany plan wykonania. Każdy plan wygenerowany zostanie dodany pamięci podręcznej planu toohello oraz podczas kolejnych wykonań kodu z hello tego samego zapytania można ponownie użyć tego planu z pamięci podręcznej hello, eliminując konieczność hello dodatkowe kompilacji. 

Aplikacje wysyłające zapytania, które obejmują wartości bez parametrów, może spowodować zmniejszenie wydajności tooa, którym dla każdego takie zapytanie z innym parametrem wartości plan wykonania hello jest skompilowane ponownie. W wielu przypadkach hello tego samego zapytania z innym parametrem, który Generowanie wartości hello planów wykonania tego samego, ale te plany są nadal osobno dodać toohello pamięci podręcznej planu. Planów wykonania ponownej kompilacji korzystanie z zasobów bazy danych, zwiększyć hello czas trwania czasu i przepełnienie hello planu zapytania, powodując pamięci podręcznej planów toobe usunięty z pamięci podręcznej hello. Przez ustawienie hello wymuszone opcji parametryzacja na powitania bazy danych może się zmienić to zachowanie programu SQL Server. 

toohelp oszacować hello wpływu tego zalecenia, są dostarczane z porównanie hello rzeczywiste użycie procesora CPU użycia i hello przewidywane użycie Procesora (tak, jakby zalecenie hello została zastosowana). Ponadto oszczędności tooCPU czasu trwania kwerendy zmniejsza hello czas spędzony w kompilacji. Również będzie znacznie mniejszy narzut na pamięci podręcznej planu, dzięki czemu większość hello planów toostay w pamięci podręcznej i można użyć ponownie. Można zastosować zalecenie to szybkie i łatwe, klikając hello **Zastosuj** polecenia. 

Gdy zastosujesz zalecenie spowoduje włączenie parametryzacja wymuszone w ciągu minut bazy danych i rozpoczyna hello monitorowania procesu, który trwa około 24 godzin. Po tym okresie będzie można toosee stanie hello sprawdzania poprawności raportu, który pokazuje użycie procesora CPU bazy danych 24 godzin przed i po zastosowaniu hello zalecenia. Doradca bazy danych programu SQL ma mechanizm bezpieczeństwa, który automatycznie przywrócona hello zastosować zalecenie, w przypadku, gdy wykryto regresji wydajności.

## <a name="fix-schema-issues-recommendations"></a>Usuń zalecenia dotyczące problemów schematu
**Rozwiązywanie problemów schematu** zalecenia są wyświetlane po hello usługi baza danych SQL powiadomienia anomalii w hello liczba błędów SQL dotyczące schematu wykonywanych na bazie danych SQL Azure. To zalecenie jest zwykle wyświetlany, gdy bazy danych wystąpi wiele błędów związanych z schematu (Nieprawidłowa nazwa kolumny, nieprawidłowa nazwa obiektu itp.) w ciągu godziny.

"Problemy z schematu" jest klasą błędy składniowe w programie SQL Server, które się zdarzyć, gdy hello definicji zapytania SQL hello i definicji hello hello schematu bazy danych nie są wyrównane. Na przykład być jedna z kolumn hello oczekiwany przez zapytanie hello brakuje w tabeli docelowej hello, lub na odwrót. 

"Napraw problem schematu" zalecenie jest wyświetlany, gdy usługi baza danych SQL Azure powiadomienia anomalii w hello liczba błędów SQL dotyczące schematu wykonywanych na bazie danych SQL Azure. Witaj, w następującej tabeli przedstawiono hello błędów, które są powiązane tooschema problemy:

| Kod błędu SQL | Komunikat |
| --- | --- |
| 201 |Procedura lub funkcja "*"oczekuje parametru"*", który nie został dostarczony. |
| 207 |Nieprawidłowa nazwa kolumny ' *'. |
| 208 |Nieprawidłowa nazwa obiektu "*". |
| 213 |Nazwa kolumny lub liczba podanych wartości nie odpowiada definicji tabeli. |
| 2812 |Nie można odnaleźć procedury składowanej "*". |
| 8144 |Procedura lub funkcja * ma określono zbyt wiele argumentów. |

## <a name="next-steps"></a>Następne kroki
Monitorowanie zalecenia i kontynuować tooapply ich toorefine wydajności. Obciążeń bazy danych są dynamiczne i zmienianie w sposób ciągły. Doradca bazy danych SQL nadal toomonitor i podano zalecenia, które może potencjalnie podnieść wydajność bazy danych. 

* Zobacz [zalecenia dotyczące wydajności w portalu Azure hello](sql-database-advisor-portal.md) dotyczące czynności w sposób toouse zaleceń w hello portalu Azure.
* Zobacz [szczegółowe informacje o wydajności zapytań](sql-database-query-performance.md) toolearn o i widoku hello wpływ na wydajność kwerend top.

## <a name="additional-resources"></a>Dodatkowe zasoby
* [Magazyn zapytań](https://msdn.microsoft.com/library/dn817826.aspx)
* [TWORZENIE INDEKSU](https://msdn.microsoft.com/library/ms188783.aspx)
* [Kontrola dostępu oparta na rolach](../active-directory/role-based-access-control-what-is.md)

