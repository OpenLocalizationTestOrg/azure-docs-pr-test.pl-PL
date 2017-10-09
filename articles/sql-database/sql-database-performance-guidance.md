---
title: "wskazówki dotyczące dostrajania wydajności bazy danych SQL aaaAzure | Dokumentacja firmy Microsoft"
description: "W tym artykule może pomóc w określeniu które toochoose warstwy usługi dla aplikacji. Zaleca także sposoby tootune Twojej aplikacji hello tooget najbardziej z bazy danych SQL Azure."
services: sql-database
documentationcenter: na
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: dd8d95fa-24b2-4233-b3f1-8e8952a7a22b
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 02/09/2017
ms.author: carlrab
ms.openlocfilehash: 2699f755391e94ab488ac1e6acedd30f8aec4488
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tuning-performance-in-azure-sql-database"></a>Dostrajanie wydajności w bazie danych SQL Azure

Baza danych SQL Azure udostępnia [zalecenia](sql-database-advisor.md) czy można użyć tooimprove wydajność bazy danych, lub możesz pozwolić, aby baza danych SQL Azure [automatycznie dostosowania aplikacji tooyour](sql-database-automatic-tuning.md) i zastosować zmiany która poprawi wydajność obciążenia.

W przypadku nie ma żadnych odpowiednich zaleceń i nadal masz problemy z wydajnością, można użyć hello następujące metody tooimprove parametrów:
1. Zwiększ [warstw usług](sql-database-service-tiers.md) i podaj więcej zasobów tooyour w bazie danych.
2. Dostrajanie aplikacji i stosować najlepsze rozwiązania, które może poprawić wydajność. 
3. Dostosuj hello bazy danych, zmieniając indeksów i zapytań toomore efektywną pracę z danymi.

Te są metod ręcznych, ponieważ należy toodecide co [warstw usług](sql-database-service-tiers.md) należy wybrać lub będzie wymagane toorewrite aplikacji lub kodu bazy danych i deply hello zmiany.

## <a name="increasing-performance-tier-of-your-database"></a>Zwiększenie poziomu wydajności bazy danych

Baza danych SQL Azure oferuje cztery [warstw usług](sql-database-service-tiers.md) wybraną z: Basic, Standard, Premium i Premium RS (mierzona jest wydajność w jednostek przepływności bazy danych, lub [Dtu](sql-database-what-is-a-dtu.md). Każdej warstwy usług izoluje ściśle hello zasobów można używać bazy danych SQL i zapewnia przewidywalną wydajność tego poziomu usług. W tym artykule firma Microsoft oferuje wskazówki, które mogą pomóc Ci wybrać hello warstwy usługi dla aplikacji. Omówiono także sposoby dostroić Twojej aplikacji hello tooget najbardziej z bazy danych SQL Azure.

> [!NOTE]
> Ten artykuł skupia się na wytyczne dotyczące wydajności dla pojedynczej bazy danych w bazie danych SQL Azure. Wskazówki wydajności powiązane tooelastic pule, zobacz [zagadnienia dotyczące cen i wydajności dla pul elastycznych](sql-database-elastic-pool-guidance.md). Należy pamiętać, jednak zastosować wiele hello dostrajanie zalecenia przedstawione w tym artykule toodatabases w puli elastycznej i uzyskać podobną wydajność korzyści.
> 

* **Podstawowe**: hello przewidywalności dobrą wydajność oferty warstwy podstawowej usługi dla każdej bazy danych, godzinę w ciągu godziny. W bazie danych podstawowych wystarczające zasoby obsługuje dobrą wydajność w małych baz danych, która nie ma wiele równoczesnych żądań. Typowe zastosowania, jeśli używasz warstwy podstawowej usługi są:
  * **Po prostu rozpoczniesz pracę z bazą danych SQL Azure**. Aplikacje, które są często rozwijany nie ma potrzeby poziomy wysokiej wydajności. Podstawowe bazy danych są idealne środowiska do tworzenia bazy danych i testowania, w momencie cen niski.
  * **Masz bazę danych z jednego użytkownika**. Aplikacje, które zwykle kojarzenie jednego użytkownika z bazy danych nie mają wysokie wymagania współbieżności i wydajności. Te aplikacje nadają się do warstwy usług podstawowa hello.
* **Standardowe**: warstwie usług standardowa na powitania oferuje lepszą wydajność przewidywalności i zapewnia dobrą wydajność dla baz danych, które mają wiele współbieżnych żądań, takich jak aplikacje sieci web i grupy roboczej. Po wybraniu warstwy standardowa usługa bazy danych można rozmiar bazy danych aplikacji w oparciu przewidywalną wydajność, minute w ciągu minuty.
  * **Baza danych zawiera wiele równoczesnych żądań**. Aplikacje, które usługi więcej niż jeden użytkownik naraz zwykle muszą wyższego poziomu wydajności. Na przykład grupy roboczej lub sieci web aplikacji, które mają wymagania ruch we/wy niskiego toomedium obsługi wielu równoczesnych zapytań nadaje się do warstwy standardowych usług hello.
* **Premium**: hello warstwę Premium oferuje przewidywalną wydajność, drugi na drugi, dla każdej bazy danych — warstwa Premium. Po wybraniu warstwy usług Premium hello można rozmiar bazy danych aplikacji oparte na powitania szczytowego obciążenia dla tej bazy danych. Hello plan usuwa przypadków, w których wariancję wydajności może spowodować tootake małych zapytania dłużej niż oczekiwano w operacjach wrażliwy na opóźnienia. Ten model może bardzo uprościć cykle hello rozwoju i produktu sprawdzania poprawności dla aplikacji, które muszą toomake silne oświadczenia dotyczące szczytowego zapotrzebowania na zasoby, odchylenie wydajności lub opóźnienia zapytania. Większość przypadków użycia warstwy Premium usługi ma co najmniej jeden z tych właściwości:
  * **Obciążenia szczytowego wysokiej**. Aplikacja, która wymaga znacznej procesora CPU, pamięć lub wejścia/wyjścia (We/Wy) toocomplete swoich operacji wymaga poziomu dedykowanego, wysokiej wydajności. Na przykład operacji bazy danych, znane tooconsume wiele rdzeni Procesora przez dłuższy czas jest kandydatem do hello warstwę Premium.
  * **Wiele równoczesnych żądań**. Niektóre aplikacje bazy danych usługi dużo współbieżnych żądań, na przykład gdy obsługująca witryny sieci Web, która ma duże natężenie ruchu. Podstawowa i standardowa warstwy usług Ogranicz hello liczbę równoczesnych żądań dla jednej bazy danych. Aplikacje, które wymagają więcej połączeń potrzebny toochoose rezerwacji odpowiedni rozmiar toohandle hello maksymalną liczbę potrzebnych żądań.
  * **Małe opóźnienia**. Niektóre aplikacje potrzebują tooguarantee odpowiedzi z hello bazy danych w minimalnym czasie. Określone procedury składowanej jest wywoływana w ramach szerszych operacji klienta, może być toohave wymaganie typ zwracany tego wywołania w milisekundach nie więcej niż 20 99 procent czasu hello. Ten typ aplikacji korzyści z warstwy usług Premium hello toomake upewnić się, że hello wymagane mocy obliczeniowej jest dostępna.
* **Premium RS**: hello warstwy Premium RS jest przeznaczony dla obciążeń intensywnie wykonujących operacje We/Wy, które nie wymagają hello najwyższy gwarancje dostępności. Przykłady obejmują testowanie obciążeń wysokiej wydajności lub obciążenia analitycznych, gdzie hello bazy danych nie jest systemem hello rekordu.

Hello poziom usług, który należy do bazy danych SQL jest zależna od hello szczytowego obciążenia wymagania dotyczące każdego wymiaru zasobów. Niektóre aplikacje używane trivial ilość pojedynczego zasobu, ale mieć znaczący wymagania dotyczące innych zasobów.

### <a name="service-tier-capabilities-and-limits"></a>Możliwości warstwy usług i limity

W poszczególnych warstwach usług można ustawić poziom wydajności hello, więc toopay elastyczność hello tylko w przypadku pojemności hello, które są potrzebne. Możesz [Dostosuj wydajność](sql-database-service-tiers.md), w górę lub w dół, jak zmiany obciążenia. Na przykład obciążenie bazy danych jest wysoka w sezonie zakupów hello wstecz do służbowych, może zwiększyć poziom wydajności hello hello bazy danych na określony czas, lipca za pośrednictwem września. Można zmniejszyć ją po zakończeniu Twojej sezonu godzinami szczytu. Można zminimalizować płacisz za optymalizacji sezonowości toohello środowiska chmury, tak firmy. Ten model jest również odpowiedni dla oprogramowania produktu cykle. Zespół może przydzielić pojemności, podczas jej uruchomień testów, a następnie zwolnij wydajność po zakończeniu testowania. W modelu żądania pojemności płacisz za pojemność potrzebny i uniknąć wydatków na dedykowany zasobów, które może być rzadko używane.

### <a name="why-service-tiers"></a>Dlaczego warstw do usług?
Mimo że poszczególnych obciążeń bazy danych może się różnić, hello warstwy usług ma tooprovide przewidywalność wydajności na różnych poziomach wydajności. Klientów z bazy danych na dużą skalę wymagań dotyczących zasobów można pracować w bardziej dedykowanego środowiska komputerowego.

## <a name="tune-your-application"></a>Dostrajanie aplikacji
W tradycyjnych, lokalnie programu SQL Server proces planowania pojemności początkowej hello jest często oddzielony od hello proces uruchomienia aplikacji w środowisku produkcyjnym. Najpierw zakupionych licencji sprzętu i produktu i dostrajania wydajności odbywają się później. Gdy używasz usługi Azure SQL Database jest procesem dobrze toointerweave hello uruchamianie aplikacji i dostrajania go. Model hello płatniczych pojemności na żądanie można dostosować w Twojej aplikacji toouse hello minimalna zasobów niezbędnych teraz, zamiast nadmiarowe Inicjowanie obsługi administracyjnej na sprzęcie oparte na prób planów przyszłego rozwoju aplikacji, które często są nieprawidłowe. Niektórzy klienci mogą nie tootune aplikacji lub zamiast tego wybrać toooverprovision zasobów sprzętowych. Takie podejście może być dobrym rozwiązaniem, jeśli nie chcesz toochange klucza aplikacji okresie zajęty. Jednak Dostrajanie aplikacji można zminimalizować wymagania dotyczące zasobów i niższe opłaty miesięczne użycie warstw usług hello w bazie danych SQL Azure.

### <a name="application-characteristics"></a>Właściwości aplikacji
Mimo że warstwach usług bazy danych SQL Azure są zaprojektowane tooimprove wydajność stabilność i przewidywalności dla aplikacji, najlepsze rozwiązania może pomóc dostroić Twojej aplikacji toobetter korzystanie z zalet hello zasobów na poziomie wydajności. Mimo że wiele aplikacji ma znaczący wzrost wydajności, po prostu przez przełączanie tooa wyższy poziom wydajności lub usługi warstwy, niektóre aplikacje muszą dodatkowe dostrojenia toobenefit z wyższego poziomu usługi. Aby zwiększyć wydajność należy wziąć pod uwagę dostrajania dodatkowych aplikacji dla aplikacji, które mają następujące cechy:

* **Aplikacje, które mają niską wydajność ze względu na zachowanie "chatty"**. Chatty aplikacji należy operacji dostępu nadmiernej ilości danych, które są toonetwork poufnych opóźnienia. Może być konieczne toomodify rodzaju aplikacje tooreduce hello liczba bazy danych SQL toohello operacji dostępu do danych. Na przykład może zwiększyć wydajność aplikacji przy użyciu technik, takich jak przetwarzanie wsadowe zapytań ad hoc lub przeniesienie hello odpytuje toostored procedury. Aby uzyskać więcej informacji, zobacz [partii zapytań](#batch-queries).
* **Bazy danych o znacznym obciążeniem, które nie może być obsługiwana przez cały jednej maszyny**. Bazy danych, które przekraczają zasobów hello hello najwyższego poziomu wydajności Premium mogą korzystać z skalowania obciążenia hello. Aby uzyskać więcej informacji, zobacz [dzielenia na fragmenty między bazami danych](#cross-database-sharding) i [funkcjonalności partycjonowania](#functional-partitioning).
* **Aplikacje, które mają zapytania nieoptymalne**. Aplikacje, zwłaszcza tych, które hello warstwie dostępu do danych, które zostały nieprawidłowo dopasowane zapytania rozwiązanie nie mogą korzystać z wyższego poziomu wydajności. W tym zapytań, które nie mają w klauzuli WHERE, brakuje indeksów lub mieć przestarzałe statystyki. Te aplikacje korzystają z techniki dostrajania wydajności standardowej kwerendy. Aby uzyskać więcej informacji, zobacz [brakujące indeksy](#identifying-and-adding-missing-indexes) i [zapytania dostrajanie i zalecanych](#query-tuning-and-hinting).
* **Projekt dostęp do aplikacji, które znajdują się dane nieoptymalne**. Aplikacje, które mają związanego z używaniem danych współbieżności problemy z dostępem, na przykład zakleszczenia, nie mogą korzystać z wyższego poziomu wydajności. Rozważ zmniejszenie rund przed hello bazy danych SQL Azure przez buforowanie danych na powitania po stronie klienta z hello usługi buforowania Azure lub innej technologii buforowania. Zobacz [buforowanie warstwy aplikacji](#application-tier-caching).

## <a name="tune-your-database"></a>Dostrajanie bazy danych
W tej sekcji opisano niektóre techniki, można użyć tootune bazy danych SQL Azure toogain hello najlepszej wydajności dla aplikacji i uruchom go na najniższym poziomie wydajność hello. Niektóre z tych metod odpowiada tradycyjnych dostrajania serwera SQL Server najlepsze rozwiązania, ale inne tooAzure określonej bazy danych SQL. W niektórych przypadkach można zbadać zasobów hello używane dla bazy danych toofind obszarów toofurther strojenia i rozszerzenia tradycyjnych toowork techniki serwera SQL w bazie danych SQL Azure.

### <a name="identify-performance-issues-using-azure-portal"></a>Identyfikowanie problemów z wydajnością przy użyciu portalu Azure
Hello następujących narzędzi w portalu Azure hello ułatwiają analizowanie i rozwiązywanie problemów z wydajnością z bazy danych SQL:

* [Szczegółowe informacje o wydajności zapytań](sql-database-query-performance.md)
* [SQL Database Advisor](sql-database-advisor.md)

Witaj portalu Azure ma więcej informacji na temat obu tych narzędzi i w jaki sposób toouse je. tooefficiently zdiagnozować i naprawić problemy, firma Microsoft zaleca najpierw spróbuj użyć narzędzia hello w hello portalu Azure. Firma Microsoft zaleca użycie ręcznego hello dostrajanie metod, które następnie omówimy brakujących indeksy i dostrajania zapytania, w szczególnych przypadkach.

Więcej informacji o identyfikowanie problemów w usłudze Azure SQL Database na [monitorowania wydajności](sql-database-single-database-monitor.md) artykułu.

### <a name="identifying-and-adding-missing-indexes"></a>Identyfikowanie i dodać brakujące indeksy
To powszechny problem, wydajność bazy danych OLTP odnosi się toohello fizyczna baza danych projektu. Często schematów bazy danych są zaprojektowane i wysłane bez testowania na dużą skalę (albo w obciążenia w woluminie danych). Niestety wydajność hello planu zapytania może być akceptowane na małą skalę, ale znacznie zmniejsza się w obszarze woluminów danych na poziomie produkcji. najbardziej typowe źródła Hello tego problemu jest brak hello odpowiednie indeksy toosatisfy filtry lub inne ograniczenia w zapytaniu. Często brakujące indeksy manifestów jako tabelę skanowania może wystarczyć wyszukiwanie indeksu.

W tym przykładzie hello planu wybrane zapytanie używa skanowania podczas wyszukiwania będzie wystarczająca:

    DROP TABLE dbo.missingindex;
    CREATE TABLE dbo.missingindex (col1 INT IDENTITY PRIMARY KEY, col2 INT);
    DECLARE @a int = 0;
    SET NOCOUNT ON;
    BEGIN TRANSACTION
    WHILE @a < 20000
    BEGIN
        INSERT INTO dbo.missingindex(col2) VALUES (@a);
        SET @a += 1;
    END
    COMMIT TRANSACTION;
    GO
    SELECT m1.col1
    FROM dbo.missingindex m1 INNER JOIN dbo.missingindex m2 ON(m1.col1=m2.col1)
    WHERE m1.col2 = 4;

![Planu zapytania z brakujące indeksy](./media/sql-database-performance-guidance/query_plan_missing_indexes.png)

Baza danych SQL Azure może pomóc Znajdź i napraw wspólnej brakujących indeksu warunków. Kompilacje zapytania, w których indeks może znacznie zmniejszyć hello szacowany koszt toorun kwerendy przyjrzeć się widoków DMV, które są wbudowane w bazie danych SQL Azure. Podczas wykonywania zapytania bazy danych SQL śledzi, jak często jest wykonywane każdego planu zapytania, a hello śledzi oszacowanego odstęp między hello wykonywania planu zapytania i hello sobie wyobrazić, co gdzie istniał tego indeksu. Możesz użyć tych wynik tooquickly widoków DMV projektowania fizyczna baza danych tooyour zmian można zwiększyć koszt obciążenia ogólną bazę danych i jego rzeczywistego obciążenia.

Możesz użyć tej możliwości tooevaluate zapytania brakujące indeksy:

    SELECT CONVERT (varchar, getdate(), 126) AS runtime,
        mig.index_group_handle, mid.index_handle,
        CONVERT (decimal (28,1), migs.avg_total_user_cost * migs.avg_user_impact *
                (migs.user_seeks + migs.user_scans)) AS improvement_measure,
        'CREATE INDEX missing_index_' + CONVERT (varchar, mig.index_group_handle) + '_' +
                  CONVERT (varchar, mid.index_handle) + ' ON ' + mid.statement + '
                  (' + ISNULL (mid.equality_columns,'')
                  + CASE WHEN mid.equality_columns IS NOT NULL
                              AND mid.inequality_columns IS NOT NULL
                         THEN ',' ELSE '' END + ISNULL (mid.inequality_columns, '')
                  + ')'
                  + ISNULL (' INCLUDE (' + mid.included_columns + ')', '') AS create_index_statement,
        migs.*,
        mid.database_id,
        mid.[object_id]
    FROM sys.dm_db_missing_index_groups AS mig
    INNER JOIN sys.dm_db_missing_index_group_stats AS migs
        ON migs.group_handle = mig.index_group_handle
    INNER JOIN sys.dm_db_missing_index_details AS mid
        ON mig.index_handle = mid.index_handle
    ORDER BY migs.avg_total_user_cost * migs.avg_user_impact * (migs.user_seeks + migs.user_scans) DESC

W tym przykładzie zapytanie hello dało w wyniku tego sugestii:

    CREATE INDEX missing_index_5006_5005 ON [dbo].[missingindex] ([col2])  

Po jego utworzeniu tej samej instrukcji SELECT wybiera innego planu, który używa wyszukiwania zamiast skanowania, a następnie wykonuje wydajniej hello plan:

![Planu zapytania z indeksami poprawiony](./media/sql-database-performance-guidance/query_plan_corrected_indexes.png)

szczegółowe informacje o klucza Hello jest tego hello wydajność We/Wy z udostępnionej, zwykłych system jest bardziej ograniczony niż maszyny dedykowanego serwera. Na minimalizując niepotrzebnych operacji We/Wy tootake maksymalną korzyści hello systemu hello jednostek dtu w warstwie poziomu wydajności poszczególnych warstwach usług bazy danych SQL Azure hello jest premium. Decyzji projektowych odpowiednie fizyczna baza danych może znacznie poprawić hello opóźnienie dla poszczególnych zapytań, zwiększyć przepustowość hello równoczesnych żądań obsługi na jednostkę skalowania, a zminimalizować hello koszty wymagane toosatisfy hello zapytania. Aby uzyskać więcej informacji na temat hello Brak widoków DMV indeksu, zobacz [sys.dm_db_missing_index_details](https://msdn.microsoft.com/library/ms345434.aspx).

### <a name="query-tuning-and-hinting"></a>Dostrajanie zapytania i zalecanych
Optymalizator zapytań Hello w bazie danych SQL Azure jest podobne Optymalizator zapytań programu SQL Server tradycyjnych toohello. Większość hello najlepsze rozwiązania dotyczące dostrajania zapytania i opis hello wnioskowania modelu ograniczenia dotyczące Optymalizator zapytań hello również zastosować tooAzure bazy danych SQL. Jeśli dostroić kwerendy w bazie danych SQL Azure, można otrzymać hello dodatkowych korzyści, zmniejszenie zapotrzebowania na zasoby agregacji. Aplikacja może być możliwe toorun na niższe koszty niż niewyregulowanym równoważną, ponieważ można uruchomić na niższym poziomie wydajności.

Przykładem jest typowe w programie SQL Server i który ma również zastosowanie tooAzure bazy danych SQL jest sposób hello Optymalizator "sniffs" Parametry zapytania. Podczas kompilacji Optymalizator zapytań hello ocenia hello bieżącą wartość toodetermine parametru, czy może generować bardziej optymalne planu zapytania. Mimo że ta strategia może często prowadzić tooa planu zapytania, który jest znacznie szybsze niż planu, który został skompilowany bez wartości parametrów znane, obecnie działa imperfectly zarówno w programie SQL Server i w bazie danych SQL Azure. Czasami parametru hello jest nie ten sposób i czasami ten parametr hello w sposób, ale wygenerowanego planu hello jest nieoptymalne dla hello pełny zestaw wartości parametrów obciążenia pracą. Firma Microsoft udostępnia wskazówki zapytania (dyrektywy), dzięki czemu można określić więcej celowo zamiar i zastąpić domyślne zachowanie hello wykrywanie parametrów. Często Jeśli używasz wskazówek, można naprawić przypadkach hello domyślne zachowanie serwera SQL lub bazy danych SQL Azure jest niedoskonała dla obciążenia określonego klienta.

Witaj w następnym przykładzie pokazano, jak procesor zapytań hello może wygenerować planu, który jest nieoptymalne, wydajności i wymagań dotyczących zasobów. W tym przykładzie przedstawiono również, że jeśli używasz wskazówki zapytania, można zmniejszyć wymagania dotyczące czasu i zasobów uruchomienie zapytania bazy danych SQL:

    DROP TABLE psptest1;
    CREATE TABLE psptest1(col1 int primary key identity, col2 int, col3 binary(200));

    DECLARE @a int = 0;
    SET NOCOUNT ON;
    BEGIN TRANSACTION
    WHILE @a < 20000
    BEGIN
        INSERT INTO psptest1(col2) values (1);
        INSERT INTO psptest1(col2) values (@a);
        SET @a += 1;
    END
    COMMIT TRANSACTION
    CREATE INDEX i1 on psptest1(col2);
    GO

    CREATE PROCEDURE psp1 (@param1 int)
    AS
    BEGIN
        INSERT INTO t1 SELECT * FROM psptest1
        WHERE col2 = @param1
        ORDER BY col2;
    END
    GO

    CREATE PROCEDURE psp2 (@param2 int)
    AS
    BEGIN
        INSERT INTO t1 SELECT * FROM psptest1 WHERE col2 = @param2
        ORDER BY col2
        OPTION (OPTIMIZE FOR (@param2 UNKNOWN))
    END
    GO

    CREATE TABLE t1 (col1 int primary key, col2 int, col3 binary(200));
    GO

Kod instalacji Hello tworzy tabelę, która ma niesymetryczna danych dystrybucji. Hello optymalne kwerenda planu różni się oparte na parametr, który jest zaznaczone. Niestety plan hello zachowanie buforowania nie zawsze ponowne skompilowanie zapytania hello na podstawie hello najbardziej typowe wartości parametru. Tak istnieje możliwość toobe planu panującymi w pamięci podręcznej i używany dla wielu wartości, nawet wtedy, gdy inny plan może być lepszym rozwiązaniem planu średnia. Następnie planu zapytania hello tworzy dwie procedury składowanej, które są identyczne, z wyjątkiem tego, że ma jedną wskazówkę zapytania specjalnych.

**Przykład, część 1**

    -- Prime Procedure Cache with scan plan
    EXEC psp1 @param1=1;
    TRUNCATE TABLE t1;

    -- Iterate multiple times tooshow hello performance difference
    DECLARE @i int = 0;
    WHILE @i < 1000
    BEGIN
        EXEC psp1 @param1=2;
        TRUNCATE TABLE t1;
        SET @i += 1;
    END

**Przykład część 2**

(Zaleca się poczekanie co najmniej 10 minut przed rozpoczęciem część 2 przykład Witaj tak, aby wyniki hello są unikatowe w hello co dane telemetryczne.)

    EXEC psp2 @param2=1;
    TRUNCATE TABLE t1;

    DECLARE @i int = 0;
    WHILE @i < 1000
    BEGIN
        EXEC psp2 @param2=2;
        TRUNCATE TABLE t1;
        SET @i += 1;
    END

W tym przykładzie każda część prób toorun sparametryzowane instrukcję 1000 razy (toogenerate wystarczające toouse obciążenia jako testowego zestawu danych). Podczas wykonywania procedur składowanych, procesor zapytań hello sprawdza, czy wartość parametru hello przekazywany procedury toohello podczas swojej pierwszej kompilacji ("wykrywanie parametrów"). Procesor Hello buforuje hello Wynikowy plan i używa go do nowszej wywołań, nawet jeśli wartość parametru hello jest inny. plan optymalne Hello nie mogą być używane we wszystkich przypadkach. Czasami trzeba tooguide hello Optymalizator toopick plan, który jest lepszym rozwiązaniem dla przypadku średni hello, a nie konkretnego przypadku hello z podczas zapytania hello najpierw został skompilowany. W tym przykładzie hello wstępny plan generuje planu "skanowanie", który odczytuje wszystkie wiersze toofind każda wartość odpowiadającą parametru hello:

![Zapytanie dostrajanie przy użyciu planu skanowania](./media/sql-database-performance-guidance/query_tuning_1.png)

Ponieważ firma Microsoft wykonywana procedura hello przy użyciu hello wartość 1, plan wynikowy hello został optymalne dla hello wartość 1, ale został nieoptymalne dla wszystkich wartości w tabeli hello. nie jest prawdopodobnie wynik Hello, co powinno, gdyby toopick każdego planu losowo, ponieważ hello plan wykonuje wolniej i wykorzystuje więcej zasobów.

Po uruchomieniu testu hello z `SET STATISTICS IO` ustawić także`ON`, praca logicznej skanowania hello w tym przykładzie jest wykonywana w tle hello. Aby sprawdzić, czy 1,148 odczyty programach planu hello, (która jest nieefektywne, jeśli średnia wielkość liter hello jest tylko jeden wiersz tooreturn):

![Zapytanie dostrajanie przy użyciu logicznej skanowania](./media/sql-database-performance-guidance/query_tuning_2.png)

Witaj drugiej części przykład Witaj używa zapytania wskazówka tootell hello Optymalizator toouse określonej wartości podczas procesu kompilacji hello. W takim przypadku wymusi hello zapytania procesora tooignore hello wartość, która została przekazana jako parametr hello i zamiast tego tooassume `UNKNOWN`. Odnosi się tooa wartość średnia częstotliwość hello w tabeli hello (Ignorowanie zegara). plan wynikowy Hello jest na podstawie wyszukiwania plan, który jest szybsze i średnio niż planu hello wykorzystuje mniej zasobów, w tym przykładzie części 1:

![Dostrajanie zapytania za pomocą wskazówki zapytania](./media/sql-database-performance-guidance/query_tuning_3.png)

Można zobaczyć efekt hello hello **sys.resource_stats** tabeli (jest wyświetlony z pewnym opóźnieniem od czasu hello wykonywania testu hello i kiedy danych hello wypełnienie hello tabeli). Dla tego przykładu, część 1 wykonywanego w oknie hello 22:25:00, a część 2 wykonywane 22:35:00. Witaj wcześniejszych przedział czasu używane więcej zasobów w danym przedziale czasu nie hello późniejszą (ze względu na ulepszenia wydajności plan).

    SELECT TOP 1000 *
    FROM sys.resource_stats
    WHERE database_name = 'resource1'
    ORDER BY start_time DESC

![Dostrajanie przykład wyniki zapytania](./media/sql-database-performance-guidance/query_tuning_4.png)

> [!NOTE]
> Chociaż wolumin hello w tym przykładzie jest celowo mały, efekt hello nieoptymalne parametrów mogą być istotne, szczególnie w przypadku większych baz danych. Różnica Hello, w ekstremalnych przypadkach mogą należeć do zakresu od sekund w przypadku szybkiego i godziny wolne przypadków.
> 
> 

Można sprawdzić **sys.resource_stats** toodetermine czy hello zasobów dla testu używa więcej lub mniej zasobów niż innego testu. Podczas porównywania danych oddzielenia czasu hello testów tak, aby nie były w hello tym samym oknie 5-minutowy w hello **sys.resource_stats** widoku. Witaj celem wykonywania hello jest toominimize hello łączną ilość zasobów używanych i nie toominimize hello szczytu zasobów. Ogólnie rzecz biorąc Optymalizacja fragment kodu dla opóźnienia zmniejsza zużycie zasobów. Upewnij się, że hello zmiany tooan aplikacji są niezbędne i nie mieć negatywny wpływ na wrażenia hello osobie, która może stosować wskazówki zapytania w aplikacji hello czy hello zmiany.

Jeśli obciążenie zawiera zestaw powtarzania zapytań, często go powoduje toocapture znaczeniu i zweryfikować optymalizacji hello z wybranych planu, ponieważ jego przebieg bazy danych hello zasobów minimalny rozmiar jednostki toohost wymagane hello. Po utworzeniu zweryfikować, czasami reexamine planów hello toohelp, należy upewnić się, że nie ma obniżoną. Użytkownik może dowiedzieć się więcej o [zapytania wskazówki (Transact-SQL)](https://msdn.microsoft.com/library/ms181714.aspx).

### <a name="cross-database-sharding"></a>Dzielenia na fragmenty między bazami danych
Ponieważ baza danych SQL Azure jest uruchamiana na standardowym sprzęcie, hello limity pojemności dla pojedynczej bazy danych są niższe niż w przypadku tradycyjnych, lokalnie instalacji programu SQL Server. Niektórzy klienci używają dzielenia na fragmenty techniki toospread bazy danych operacji over wielu baz danych podczas operacji hello nie mieści się w granicach hello pojedynczej bazy danych w bazie danych SQL Azure. Większość klientów korzystających z techniki dzielenia na fragmenty w bazie danych SQL Azure podzielone swoje dane na jednym wymiarze między wieloma bazami danych. Takie podejście należy toounderstand, że aplikacje OLTP często wykonywać transakcje tooonly jeden wiersz lub tooa niewielkiej liczby wierszy w schemacie hello.

> [!NOTE]
> Baza danych SQL oferuje teraz tooassist biblioteki z dzielenia na fragmenty. Aby uzyskać więcej informacji, zobacz [omówienie biblioteki klienta elastycznej bazy danych](sql-database-elastic-database-client-library.md).
> 
> 

Na przykład jeśli bazy danych ma nazwę odbiorcy, kolejność i szczegółów zamówienia (np. hello przykład tradycyjne bazy danych Northwind dostarczaną z programem SQL Server), to można podzielić tych danych do wielu baz danych przez grupowanie klientowi hello powiązane kolejności i szczegółami zamówienia informacje. Można zagwarantować powitania klienta danych pozostaje w pojedynczej bazy danych. Aplikacja Hello czy podziału różnych klientów dla baz danych, efektywnie rozłożenie obciążenia hello wielu baz danych. Z dzielenia na fragmenty, klienci nie tylko można uniknąć limitu rozmiaru hello maksymalna bazy danych, ale baza danych SQL Azure także można przetwarzać obciążeń, które są znacznie większe niż limity hello hello różne poziomy wydajności, jak długo każdy jedna baza danych jest dopasowywana do jego JEDNOSTEK DTU W WARSTWIE.

Dzielenia na fragmenty bazy danych nie zmniejszyć pojemność zagregowanych danych zasobu hello rozwiązania, ale jest wysoce efektywne Obsługa bardzo dużych rozwiązań, które rozprzestrzeniają się przez wiele baz danych. Każda baza danych można uruchomić na wydajność innego poziomu toosupport bardzo dużych "skuteczne" bazy danych o wysokich wymaganiach dotyczących zasobów.

### <a name="functional-partitioning"></a>Partycje funkcjonalne
Użytkownicy programu SQL Server często łączyć wiele funkcji w jednej bazie danych. Na przykład jeśli aplikacja ma spisu toomanage logiki magazynu, tej bazy danych może być logiki skojarzonej z magazynu śledzenia zakupów, procedury składowane i indeksowanych lub zmaterializowanych widoków, które Zarządzanie raportowaniem koniec miesiąca. Ta metoda umożliwia łatwiejsze tooadminister hello bazy danych operacje, takie jak Kopia zapasowa, ale również wymaga możesz toosize hello sprzętu toohandle hello obciążenia szczytowego we wszystkich funkcji aplikacji.

Jeśli używasz skalowalność architektury w bazie danych SQL Azure jest dobrym rozwiązaniem toosplit różne funkcje aplikacji do różnych baz danych. Korzystając z tej techniki, każda aplikacja skaluje niezależnie. Aplikacji staje się coraz bardziej zajęty (i hello obciążenie hello wzrostu bazy danych), hello administrator można poziomy wydajności niezależne dla każdej funkcji aplikacji hello. Limitu hello z tej architektury aplikacji może być większy niż maszyny pojedynczego towaru może obsłużyć obciążenia hello jest rozprzestrzeniają się na wielu komputerach.

### <a name="batch-queries"></a>Partii zapytań
Dla aplikacji, które uzyskują dostęp do danych przy użyciu dużych częste zapytań ad hoc, znacznej ilości czasu odpowiedzi odbywa się na komunikację sieciową między warstwą aplikacji hello i warstwy bazy danych SQL Azure hello. Nawet wtedy, gdy oba hello aplikacji i baz danych SQL Azure są w tym samym centrum danych, hello opóźnienie sieci między dwoma hello może być powiększony przez dużą liczbę operacji uzyskiwania dostępu do danych hello. round sieci hello tooreduce podróży hello danych operacji dostępu, rozważ użycie hello opcja tooeither partii hello ad hoc zapytania lub toocompile je jako procedury składowane. Jeśli partii zapytań ad hoc hello, możesz wysłać wiele zapytań jako jedna duża partia w podróży pojedynczego tooAzure bazy danych SQL. Jeśli kompilacja zapytań ad hoc w procedurze składowanej można osiągnąć hello spowodować takie same tak, jakby ich partii. Za pomocą procedury składowanej również zapewnia hello zaletą zwiększa prawdopodobieństwo hello buforowania hello plany zapytań w bazie danych SQL Azure, dzięki czemu można używać hello przechowywane procedury ponownie.

Niektóre aplikacje intensywnie zapisu. Czasami można zmniejszyć hello całkowitego obciążenia We/Wy na bazę danych, biorąc pod uwagę, jak toobatch zapisuje razem. Często jest tak proste, jak przy użyciu jawnych transakcji zamiast automatycznego zatwierdzania transakcji w procedur składowanych i partie ad hoc. Do oceny różnych technik można użyć, zobacz [przetwarzanie wsadowe techniki dla aplikacji bazy danych SQL na platformie Azure](https://msdn.microsoft.com/library/windowsazure/dn132615.aspx). Poeksperymentuj z własnych obciążenia toofind hello prawo modelu dla przetwarzania wsadowego. Nieznacznie się toounderstand się upewnić, że model może mieć różne spójności transakcyjnej gwarantuje. Znajdowanie hello obciążenie prawo minimalizuje wykorzystanie zasobów wymaga znajdowanie hello odpowiednie połączenie kompromisy wydajnością a spójnością.

### <a name="application-tier-caching"></a>Buforowanie warstwy aplikacji
Niektóre aplikacje bazy danych mają obciążeń intensywnie odczytu. Buforowanie warstwy może zmniejszyć obciążenie hello hello bazy danych i może zmniejszyć wydajność hello poziomu wirusowej toosupport wymagane bazy danych przy użyciu bazy danych SQL Azure. Z [pamięć podręczna Redis Azure](https://azure.microsoft.com/services/cache/), jeśli obciążenie intensywnie odczytu, możesz przeczytać danych hello raz (lub raz na maszynie warstwy aplikacji, w zależności od sposobu skonfigurowania) i następnie przechowywania tych danych spoza Twojej bazy danych SQL. Jest to sposób tooreduce obciążenia bazy danych (CPU i odczytu We/Wy), ale wpływa na spójności transakcyjnej ponieważ odczytywane z pamięci podręcznej hello dane hello może być zsynchronizowane z danymi hello hello bazy danych. Chociaż w wielu aplikacjach pewnego poziomu niespójności jest dopuszczalna, który nie jest spełniony dla wszystkich obciążeń. Wszelkie wymagania aplikacji należy zapoznać się przed zaimplementowaniem strategii buforowania warstwy aplikacji.

## <a name="next-steps"></a>Następne kroki
* Aby uzyskać więcej informacji na temat warstwy usług, zobacz [opcje bazy danych SQL i wydajność](sql-database-service-tiers.md)
* Aby uzyskać więcej informacji na temat pule elastyczne, zobacz [co to jest puli elastycznej platformy Azure?](sql-database-elastic-pool.md)
* Aby uzyskać informacje o wydajności i elastyczne pule, zobacz [podczas tooconsider puli elastycznej](sql-database-elastic-pool-guidance.md)

