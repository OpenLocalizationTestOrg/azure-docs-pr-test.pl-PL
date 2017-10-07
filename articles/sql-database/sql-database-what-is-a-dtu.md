---
title: "Usługa SQL Database: Co to jest jednostka DTU? | Microsoft Docs"
description: "Opis jednostki transakcji usługi Azure SQL Database."
keywords: "opcje bazy danych, wydajność bazy danych"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: CarlRabeler
ms.assetid: 89e3e9ce-2eeb-4949-b40f-6fc3bf520538
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: NA
ms.date: 04/13/2017
ms.author: carlrab
ms.openlocfilehash: ba1fe580b32826259edaf6c8dc124faaf5b3d234
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="explaining-database-transaction-units-dtus-and-elastic-database-transaction-units-edtus"></a>Wyjaśnienie jednostek DTU (Database Transaction Units) i eDTU (elastic Database Transaction Units)
W tym artykule opisano, że jednostki transakcji bazy danych (Dtu) i jednostek transakcji elastycznej bazy danych (Edtu) i co się stanie po naciśnięciu przycisku hello maksymalna liczba jednostek Dtu lub Edtu.  

## <a name="what-are-database-transaction-units-dtus"></a>Co to są jednostki DTU (Database Transaction Unit)
Dla jednej bazy danych Azure SQL w konkretnego poziomu wydajności w ramach [warstwy usług](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels), Microsoft gwarantuje pewnego poziomu zasobów dla tej bazy danych (niezależnie od innych bazy danych w hello chmury Azure) i przewidywalna poziom wydajności. Ta ilość zasobów jest obliczany jako liczba jednostek transakcji bazy danych lub Dtu i jest mieszanych pomiarach Procesora, pamięci, we/wy (danych i dziennika transakcji we/wy). współczynnik Hello spośród tych zasobów pierwotnie został określony poprzez [obciążenia OLTP testu porównawczego](sql-database-benchmark-overview.md) zaprojektowane toobe typowe dla obciążeń OLTP rzeczywistych. Gdy obciążenie przekracza wielkość hello któregokolwiek z tych zasobów, przepustowość sieci jest ograniczeniem przepustowości — wynikowe w niska wydajność i przekroczeń limitu czasu. Hello zasoby używane przez obciążenie będzie mieć wpływu na powitania zasoby dostępne tooother baz danych w hello chmury Azure i zasobów hello używany przez inne obciążenia nie wpływają na hello zasoby dostępne tooyour SQL w bazie danych.

![obwiedni](./media/sql-database-what-is-a-dtu/bounding-box.png)

Liczba jednostek Dtu są najbardziej przydatne dla zrozumienia hello względną ilość zasobów między bazami danych SQL Azure na różne poziomy wydajności i warstwy usług. Na przykład podwojenie Dtu powitania po podniesieniu poziomu wydajności hello bazy danych oznacza zestaw hello toodoubling toothat dostępnych zasobów w bazie danych. Na przykład baza danych Premium P11 z 1750 jednostkami DTU zapewnia 350 razy więcej mocy obliczeniowej DTU niż podstawowa baza danych z 5 jednostkami DTU.  

toogain lepszy wgląd w zużycie zasobów (bazy danych DTU) hello obciążenia, użyj [szczegółowe informacje o usłudze Azure SQL bazy danych zapytań wydajności](sql-database-query-performance.md) do:

- Identyfikowanie najważniejszych zapytań hello według liczby wykonywania-Procesor/czas trwania, który może potencjalnie dostroić zwiększonej wydajności. Na przykład kwerendę intensywne operacje We/Wy mogą korzystać z użycia hello [techniki optymalizacji w pamięci](sql-database-in-memory.md) toomake lepsze wykorzystanie pamięci hello w niektórych warstwę i poziom wydajności usługi.
- Przechodzenie do szczegółów hello zapytania, Wyświetl tekst i historii wykorzystania zasobów.
- Dostosowywanie zaleceń, które zawierają akcje wykonywane przez wydajności dostępu [doradcy bazy danych SQL](sql-database-advisor.md).

Możesz [zmiana warstw usług](sql-database-service-tiers.md) w dowolnym momencie z minimalnym czasem przestojów tooyour aplikacji (zwykle uśrednianie poniżej cztery sekund). Dla wielu firm i aplikacji jest w stanie toocreate baz danych i wybrać wydajności w górę lub w dół na żądanie jest wystarczająca, zwłaszcza jeśli wzorce użycia są względnie przewidywalne. Ale jeśli masz nieprzewidywalnych wzorców, może być twarde toomanage kosztów i modelem biznesowym. W tym scenariuszu używany z określonej liczby jednostek Edtu, które są współużytkowane przez wiele bazy danych w puli hello puli elastycznej.

![Wprowadzenie do tooSQL bazy danych: pojedynczy Dtu bazy danych według warstwy i poziomu](./media/sql-database-what-is-a-dtu/single_db_dtus.png)

## <a name="what-are-elastic-database-transaction-units-edtus"></a>Co to są jednostki eDTU (elastic Database Transaction Unit)
Raczej nie udostępniają dedykowany zestaw zasobów (Dtu) tooa bazy danych SQL, która jest zawsze dostępna niezależnie od tego, czy potrzebne nie, możesz umieścić baz danych do [puli elastycznej](sql-database-elastic-pool.md) na serwerze bazy danych SQL, który współużytkuje puli zasobów wśród tych bazy danych. Hello udostępnionych zasobów w puli elastycznej, mierząc elastycznych jednostkach transakcji bazy danych lub Edtu. Pule elastyczne Podaj prostym rozwiązaniem ekonomiczne cele wydajności hello toomanage dla wielu baz danych, które mają różnymi i nieprzewidywalnych wzorców. W puli elastycznej może zagwarantować nie jedna baza danych używa wszystkich zasobów hello w puli hello oraz czy minimalna ilość zasobów jest zawsze bazy danych tooa dostępne w puli elastycznej. Zobacz [pule elastyczne](sql-database-elastic-pool.md) Aby uzyskać więcej informacji.

![Wprowadzenie do tooSQL bazy danych: Edtu według warstwy i poziomu](./media/sql-database-what-is-a-dtu/sqldb_elastic_pools.png)

Puli jest przydzielana określona liczba jednostek eDTU za określoną cenę. W puli elastycznej hello pojedynczych baz danych są podane hello elastyczność tooauto skali w granicach hello skonfigurowane. Duże obciążenie bazy danych mogą zużywać więcej jednostek Edtu toomeet żądanie podczas baz danych w ramach lekkie ładunki zużywają mniej się punkt toohello, że bazy danych w ramach obciążenia korzystać z nie jednostek Edtu. Inicjowanie obsługi zasobów dla całej puli hello, zamiast na bazę danych, zadania zarządzania są uproszczone i mają przewidywalna budżetu hello puli.

Dodatkowe Edtu można dodać istniejącej puli tooan bez przestojów bazy danych i bez wpływu na hello hello puli baz danych. Podobnie jeśli dodatkowe jednostki eDTU nie są już potrzebne, można je usunąć z istniejącej puli w dowolnej chwili. Można dodawać lub odjęcia puli toohello baz danych lub kwota hello limitu liczby jednostek Edtu bazy danych można użyć w obszarze obciążony tooreserve Edtu dla innych baz danych. Jeśli bazy danych jest jednoznacznie w obszarze wykorzystaniem zasobów, można wychodzenia hello puli i skonfigurować go jako pojedynczej bazy danych z przewidywalną ilość zasobów wymaga.

## <a name="how-can-i-determine-hello-number-of-dtus-needed-by-my-workload"></a>Jak ustalić, hello liczba jednostek Dtu wymaganych przez obciążenie mojej?
Jeśli szukasz toomigrate istniejącym lokalnym lub tooAzure obciążenie maszyny wirtualnej programu SQL Server bazy danych SQL, można użyć hello [kalkulatora DTU](http://dtucalculator.azurewebsites.net/) tooapproximate hello liczbę jednostek Dtu potrzebne. Istniejące obciążenia pracą bazy danych SQL Azure, można użyć [Insight wydajności kwerendy bazy danych SQL](sql-database-query-performance.md) toounderstand Twojej bazy danych zasobów zużycie (Dtu) tooget lepszy wgląd w sposób toooptimize obciążenie. Można również użyć hello [sys.dm_db_ resource_stats](https://msdn.microsoft.com/library/dn800981.aspx) DMV tooget hello zasobów informacji dotyczących zużycia hello 1 godzinę. Alternatywnie hello widoku wykazu [sys.resource_stats](http://msdn.microsoft.com/library/dn269979.aspx) może również być tooget, którego dotyczy kwerenda hello te same dane dla hello ostatnie 14 dni, chociaż na dolnym wierności średnich 5 minutową.

## <a name="how-do-i-know-if-i-could-benefit-from-an-elastic-pool-of-resources"></a>Jak sprawdzić, czy elastyczna pula zasobów jest dla mnie korzystnym rozwiązaniem?
Pule są odpowiednie dla wielu baz danych o określonych wzorcach użycia. Dla danej bazy danych ten wzorzec charakteryzuje się niskim średnim wykorzystaniem oraz stosunkowo rzadkimi okresami zwiększonego użycia. Baza danych SQL automatycznie ocenia użycie zasobów historycznych hello baz danych na istniejącym serwerze bazy danych SQL i zaleca konfiguracji odpowiedniej puli hello w hello portalu Azure. Aby uzyskać więcej informacji, zobacz [Kiedy należy użyć puli elastycznej?](sql-database-elastic-pool.md)

## <a name="what-happens-when-i-hit-my-maximum-dtus"></a>Co się stanie po osiągnięciu limitu jednostek DTU?
Poziomy wydajności są kalibrować i której działalność tooprovide hello wymagane zasoby toorun obciążenie bazy danych się toohello limity maksymalny dozwolony poziom warstwy wydajności wybranej usługi. Jeżeli obciążenie jest naciśnięcie limity hello w jednym z ograniczeń we/wy procesora CPU/dane we/wy/Log, nadal tooreceive hello zasobów na powitania maksymalny dozwolony poziom, ale są prawdopodobnie toosee zwiększyć opóźnienia dla zapytań. Te limity nie spowoduje żadnych błędów, ale raczej spowolnienie obciążenia pracą hello, chyba że spowolnienie hello staje się tak poważne, że zapytania uruchamiane chronometrażu. W przypadku osiągnięcia limitów maksymalnej dozwolonej liczby równoczesnych sesji/żądań użytkowników (wątków roboczych) występują jawne błędy. Zobacz [Limity zasobów usługi Azure SQL Database](sql-database-resource-limits.md), aby uzyskać informacje na temat limitów zasobów innych niż procesor CPU, pamięć, operacje we/wy danych oraz operacje we/wy dziennika transakcji.

## <a name="next-steps"></a>Następne kroki
* Zobacz [warstwy usług](sql-database-service-tiers.md) informacji na temat jednostek Dtu hello i jednostek Edtu dostępnych dla pojedynczych baz danych i elastyczne pule.
* Zobacz [Limity zasobów usługi Azure SQL Database](sql-database-resource-limits.md), aby uzyskać informacje na temat limitów zasobów innych niż procesor CPU, pamięć, operacje we/wy danych oraz operacje we/wy dziennika transakcji.
* Zobacz [Insight wydajności kwerendy bazy danych SQL](sql-database-query-performance.md) toounderstand użycia (Dtu).
* Zobacz [omówienie testów porównawczych bazy danych SQL](sql-database-benchmark-overview.md) metodologii hello toounderstand za hello OLTP testu obciążenia używane hello toodetermine blend jednostek dtu w warstwie.
