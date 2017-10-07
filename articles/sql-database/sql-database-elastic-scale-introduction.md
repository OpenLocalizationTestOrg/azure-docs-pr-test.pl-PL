---
title: "aaaScaling się z bazą danych SQL Azure | Dokumentacja firmy Microsoft"
description: "Oprogramowanie jako usługa (SaaS) deweloperzy mogą łatwo tworzyć elastyczne, skalowalne baz danych w hello chmury, za pomocą tych narzędzi"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: d15a2e3f-5adf-41f0-95fa-4b945448e184
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: ddove
ms.openlocfilehash: 82a561e07389d8619727a540fa9424248c087eda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-out-with-azure-sql-database"></a>Scaling out with Azure SQL Database (Skalowanie w poziomie za pomocą usługi Azure SQL Database)
Możesz łatwo skalować w poziomie bazy danych Azure SQL przy użyciu hello **elastycznej bazy danych** narzędzia. Te narzędzia i funkcje umożliwiają używanie hello nieograniczoną bazy danych zasobów **bazy danych SQL Azure** toocreate rozwiązania obciążeń transakcyjnych i szczególnie oprogramowania jako aplikacje usługi (SaaS). Elastyczne funkcje bazy danych składają się z następujących hello:

* [Biblioteka klienta usługi elastycznej bazy danych](sql-database-elastic-database-client-library.md): Biblioteka klienta hello jest funkcją, która pozwala toocreate i obsługa podzielonej baz danych.  Zobacz [wprowadzenie do narzędzi elastycznej bazy danych](sql-database-elastic-scale-get-started.md).
* [Elastyczne narzędzia scalania podziału bazy danych](sql-database-elastic-scale-overview-split-and-merge.md): przenosi dane między podzielonej baz danych. Jest to przydatna do przenoszenia danych z wieloma dzierżawcami bazy danych tooa pojedynczej dzierżawy bazy danych (lub odwrotnie). Zobacz [samouczek narzędzi elastycznej bazy danych scalania podziału](sql-database-elastic-scale-configure-deploy-split-and-merge.md).
* [Zadania elastyczne bazy danych](sql-database-elastic-jobs-overview.md) (wersja zapoznawcza): użyj zadania toomanage dużej liczby baz danych Azure SQL. Łatwe wykonywanie operacji administracyjnych, takie jak zmiany schematu, Zarządzanie poświadczeniami, aktualizacje danych odwołania, zbierania danych o wydajności lub przy użyciu zadań gromadzenia danych telemetrii dzierżawy (klienta).
* [Zapytanie elastycznej bazy danych](sql-database-elastic-query-overview.md) (wersja zapoznawcza): umożliwia zapytania toorun języka Transact-SQL, obejmującej wiele baz danych. Dzięki temu połączenia tooreporting narzędzi, takich jak program Excel, usługa Power BI, Tableau itp.
* [Transakcje elastycznej](sql-database-elastic-transactions-overview.md): Ta funkcja umożliwia transakcje toorun, obejmujące wiele baz danych w bazie danych SQL Azure. Transakcji elastycznej bazy danych są dostępne dla aplikacji .NET przy użyciu ADO .NET oraz integrują się z hello znanych środowisko programowania przy użyciu hello [System.Transaction klasy](https://msdn.microsoft.com/library/system.transactions.aspx).

Hello rysunku poniżej przedstawiono architekturę, która obejmuje hello **elastycznej bazy danych funkcji** w kolekcji tooa relacji baz danych.

Na rysunku kolory hello bazy danych reprezentują schematów. Bazy danych z hello samego udziału kolor hello tego samego schematu.

1. Zestaw **baz danych Azure SQL** są hostowane na platformie Azure przy użyciu architektury dzielenia na fragmenty.
2. Witaj **biblioteki klienta elastycznej bazy danych** ustawiono używane toomanage niezależnego fragmentu.
3. Podzbiór hello baz danych są umieszczane w **puli elastycznej**. (Zobacz [co to jest pula?](sql-database-elastic-pool.md)).
4. **Zadania elastycznej bazy danych** działa według harmonogramu lub ad hoc skryptów T-SQL dla wszystkich baz danych.
5. Witaj **narzędzia do scalania podziału** toomove używane dane z jednego niezależnego fragmentu tooanother.
6. Witaj **elastycznej bazy danych zapytania** pozwala toowrite kwerendę, która obejmuje wszystkie bazy danych w zestawie niezależnego fragmentu hello.
7. **Transakcje elastycznej** pozwala transakcje toorun, obejmujące wiele baz danych. 

![Narzędzia elastycznych baz danych][1]

## <a name="why-use-hello-tools"></a>Dlaczego warto używać narzędzia hello?
Elastyczność obsługiwanie i skalowanie dla aplikacji w chmurze nastąpiło proste dla maszyn wirtualnych i magazynu obiektów blob — po prostu dodania lub odjęcia jednostki lub zwiększ zasilania. Lecz pozostają wyzwanie dla stanowych przetwarzania danych w relacyjnych baz danych. Wyzwania pojawiło się w następujących scenariuszach:

* Powiększania i zmniejszania pojemności hello relacyjnej bazy danych części obciążenie.
* Zarządzanie punktami HotSpot, które mogą wystąpić podczas wpływających na konkretnego podzestawu dane — takie jak szczególnie zajęty end klienta (dzierżawcy).

Tradycyjnie scenariuszy, takich jak te dotyczą zainwestować w aplikacji hello toosupport serwerów bazy danych z dużą skalę. Jednak ta opcja jest ograniczona w chmurze hello gdzie przetwarzania się dzieje na sprzęcie masowym wstępnie zdefiniowane. Zamiast tego przesyłanie danych i przetwarzania przez wiele baz danych strukturalnych tak samo (nazywane "dzielenia na fragmenty" wzorzec skalowalnego w poziomie) oferuje alternatywne tootraditional podejścia skalowanie w pionie zarówno pod względem kosztów i elastyczność.

## <a name="horizontal-and-vertical-scaling"></a>Skalowanie w poziomie i w pionie
na poniższym rysunku Hello przedstawiono hello poziome i pionowe wymiarów, skalowania, które są hello podstawowe sposoby, które mogą być skalowane hello elastycznych baz danych.

![Poziome i pionowe skalowania][2]

Skalowanie w poziomie odnosi się tooadding lub usuwania bazy danych w kolejności tooadjust pojemności lub ogólną wydajność. To jest również nazywany "skalowanie" out. Dzielenia na fragmenty, w którym danych jest podzielonym na partycje w kolekcji identycznie strukturalnych baz danych, jest poziomy wspólnej tooimplement sposób skalowania.  

Skalowanie w pionie odwołuje się tooincreasing lub Zmniejsz poziom wydajności hello poszczególne bazy danych — jest to również nazywane "skalowaniu."

Większość aplikacji baz danych w skali chmury użyje kombinacji tych dwóch strategii. Aplikacja oprogramowania jako usługi może na przykład użyć poziome skalowania tooprovision nowych end klientów i pionowego, skalowania tooallow każdego odbiorcy końcowego zasobów bazy danych toogrow lub zmniejszania odpowiednio do potrzeb hello obciążenia.

* Skalowanie w poziomie jest zarządzany przy użyciu hello [biblioteki klienta elastycznej bazy danych](sql-database-elastic-database-client-library.md).
* Skalowanie w pionie odbywa się przy użyciu warstwy usług Azure PowerShell polecenia cmdlet toochange hello, lub poprzez umieszczenie bazy danych w puli elastycznej.

## <a name="sharding"></a>Dzielenia na fragmenty
*Dzielenia na fragmenty* jest toodistribute technika dużych ilości danych strukturalnych tak samo dla pewnej liczby niezależnych baz danych. Jest to szczególnie popularnych z deweloperami chmury tworzenie oprogramowania jako ofert usługi (SAAS) dla klientów końcowych lub firmy. Ci klienci zakończenia są często określonego tooas "dzierżawcy". Dzielenia na fragmenty mogą być wymagane dla wielu sytuacjach:  

* Witaj całkowitej ilości danych jest zbyt duży toofit w ramach ograniczenia hello pojedynczej bazy danych
* przepustowość transakcji Hello hello ogólną obciążenie przekracza możliwości hello pojedynczej bazy danych
* Dzierżawcy mogą wymagać fizycznego izolacji od siebie, więc oddzielne bazy danych są wymagane dla każdego dzierżawcy
* Różne sekcje bazy danych może być konieczne tooreside w różnych lokalizacjach geograficznych dla zgodności, wydajność lub geograficznymi powodów.

W innych sytuacjach, takich jak wprowadzanie danych z urządzeń rozproszonych dzielenia na fragmenty może być używane toofill zestaw baz danych, które są zorganizowane tymczasowe. Na przykład oddzielnej bazy danych może być dedykowany tooeach dnia lub tygodnia. W takim przypadku hello dzielenia na fragmenty klucz może być liczba całkowita reprezentująca hello datę (istnieje we wszystkich wierszach tabel podzielonej hello) i zapytania podczas pobierania informacji dotyczących zakresu dat muszą być kierowane przez podzestawu toohello aplikacji hello obejmujących zakres hello w bazach danych pytanie.

Dzielenia na fragmenty działa najlepiej, gdy każda transakcja w aplikacji może być ograniczony tooa pojedyncza wartość klucza dzielenia na fragmenty. Dzięki temu konieczności wszystkich transakcji lokalnej tooa określonej bazy danych.

## <a name="multi-tenant-and-single-tenant"></a>Wielodostępne i pojedynczej dzierżawy
Niektóre aplikacje używają hello najprostsza metoda tworzenia oddzielnej bazy danych dla każdego dzierżawcy. Jest to hello **wzorca dzielenia na fragmenty pojedynczej dzierżawy** zapewnia izolację, możliwość wykonywania kopii zapasowej i przywracania i zasobów skalowania o hello hello dzierżawcy. Z pojedynczej dzierżawy dzielenia na fragmenty każda baza danych jest skojarzona z wartość Identyfikatora dzierżawy określonego (lub wartość klucza klienta), ale tego klucza nie muszą zawsze być obecne w samych danych hello. Jest hello tooroute odpowiedzialność aplikacji każdego żądania toohello odpowiednie bazy danych — i uprościć to powitania klienta biblioteki.

![Pojedynczej dzierżawy w porównaniu z wieloma dzierżawcami][4]

Inne scenariusze pakietu wielu dzierżawców ze sobą do bazy danych zamiast izolowanie je do oddzielnego baz danych. To jest typowe **wzorca dzielenia na fragmenty wielodostępne** - i może być prowadzony hello fakt, że aplikacja zarządza dużej liczby dzierżawców bardzo małe. W wielodostępnym dzielenia na fragmenty hello wierszy w tabelach bazy danych hello są wszystkie są zaprojektowane toocarry klucz identyfikujący klucza dzierżawy hello Identyfikatora lub dzielenia na fragmenty. Ponownie warstwy aplikacji hello jest odpowiedzialny za routingu dzierżawcy żądania toohello odpowiednią bazę danych, a to może być obsługiwana przez biblioteki klienta elastycznej bazy danych hello. Ponadto zabezpieczenia na poziomie wiersza mogą być używane toofilter wiersze, które każdego dzierżawcy można uzyskać dostępu do — Aby uzyskać więcej informacji, zobacz [wielodostępnych aplikacji za pomocą narzędzi elastycznej bazy danych i zabezpieczenia na poziomie wiersza](sql-database-elastic-tools-multi-tenant-row-level-security.md). Redystrybuowanie danych między bazami danych mogą być wymagane ze wzorcem dzielenia na fragmenty wielodostępne hello i umożliwiają to narzędzie do scalania podziału elastycznej bazy danych hello. toolearn więcej informacji na temat wzorców projektowych dla aplikacji SaaS wykorzystujących pule elastyczne, zobacz [wzorce projektowe dla wielodostępnych aplikacji SaaS przy użyciu usługi Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md).

### <a name="move-data-from-multiple-toosingle-tenancy-databases"></a>Przenoszenie danych z wielu dzierżawców toosingle baz danych
Podczas tworzenia aplikacji SaaS, jest typowy toooffer potencjalnych odbiorców wersję próbną programu hello oprogramowania. W takim przypadku jest ekonomiczna toouse wielodostępne bazy danych dla danych hello. Jednak gdy dot, dzierżawy pojedynczej bazy danych jest lepszym rozwiązaniem, ponieważ zapewnia lepszą wydajność. Jeśli powitania klienta były tworzone danych podczas okresu próbnego hello, użyj hello [narzędzia do scalania podziału](sql-database-elastic-scale-overview-split-and-merge.md) toomove hello danych z hello toohello wielodostępne nową bazę danych pojedynczej dzierżawy.

## <a name="next-steps"></a>Następne kroki
Aby przykładową aplikację prezentującą powitania klienta biblioteki, zobacz [rozpocząć pracę z narzędziami elastycznej Datababase](sql-database-elastic-scale-get-started.md).

tooconvert istniejących baz danych toouse hello narzędzia, zobacz [migracji istniejącej bazy danych poza tooscale](sql-database-elastic-convert-to-use-elastic-tools.md).

Zobacz szczegóły hello toosee hello elastycznej puli [zagadnienia dotyczące cen i wydajności dla elastycznej puli](sql-database-elastic-pool.md), lub Utwórz nową pulę z [pule elastyczne](sql-database-elastic-pool-manage-portal.md).  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->
[1]:./media/sql-database-elastic-scale-introduction/tools.png
[2]:./media/sql-database-elastic-scale-introduction/h_versus_vert.png
[3]:./media/sql-database-elastic-scale-introduction/overview.png
[4]:./media/sql-database-elastic-scale-introduction/single_v_multi_tenant.png

