---
title: "Przetwarzanie wsadowe wydajność aplikacji bazy danych SQL Azure tooimprove toouse aaaHow"
description: "Witaj temat zawiera dowód, że przetwarzanie wsadowe bazy danych operacji znacznie imroves hello szybkość i skalowalność aplikacji bazy danych SQL Azure. Mimo że te techniki przetwarzanie wsadowe działać dla dowolnej bazy danych programu SQL Server, hello hello artykuł koncentruje się na platformie Azure."
services: sql-database
documentationcenter: na
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 563862ca-c65a-46f6-975d-10df7ff6aa9c
ms.service: sql-database
ms.custom: develop apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/12/2016
ms.author: sstein
ms.openlocfilehash: 124b203ee69c595f0813852ff09ef9ec6841233a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-batching-tooimprove-sql-database-application-performance"></a>Jak toouse przetwarzanie wsadowe wydajność aplikacji tooimprove bazy danych SQL
Przetwarzanie wsadowe operacji tooAzure bazy danych SQL znacznie poprawia hello wydajność i skalowalność aplikacji. W kolejności toounderstand hello korzyści hello pierwsza część w tym artykule omówiono niektóre przykładowe wyniki testów, pozwalające porównać tooa żądań wsadowych i sekwencyjny bazy danych SQL. Witaj dalszej części artykułu hello pokazuje hello technik, scenariusze i zagadnienia dotyczące toohelp toouse pomyślnie przetwarzanie wsadowe w aplikacjach platformy Azure.

## <a name="why-is-batching-important-for-sql-database"></a>Dlaczego jest przetwarzanie wsadowe ważne dla bazy danych SQL?
Przetwarzanie wsadowe wywołania tooa zdalny jest dobrze znane strategię zwiększenie wydajności i skalowalności. Usunięto przetwarzania kosztów tooany interakcji z usługi zdalnej, takich jak serializacji, transferu sieciowego i deserializacji. Pakowanie wiele oddzielnych transakcji do pojedynczej partii minimalizuje tych kosztów.

W tym dokumencie chcemy tooexamine różne strategie przetwarzanie wsadowe bazy danych SQL i scenariuszy. Mimo że strategie również są ważne dla aplikacji lokalnych, które używają programu SQL Server, istnieje kilka przyczyn wyróżnianie hello stosowania przetwarzania wsadowego dla bazy danych SQL:

* Brak potencjalnie większe opóźnienia sieci podczas uzyskiwania dostępu do bazy danych SQL, zwłaszcza, jeśli uzyskują dostęp do bazy danych SQL z hello poza tym samym centrum danych Microsoft Azure.
* toohello odpowiada warstwy dostępu Hello wielodostępnym właściwości bazy danych SQL oznacza, że hello wydajności danych hello ogólnej skalowalności hello bazy danych. Baza danych SQL musi uniemożliwić przejęcie kontroli nad bazy danych zasobów toohello szkody innych dzierżawców dowolnego pojedynczego dzierżawcy/użytkownika. W odpowiedzi toousage poza przydziały wstępnie zdefiniowane bazy danych SQL można zmniejszyć przepływności lub odpowiadać, podając ograniczania wyjątków. Korzyści, takich jak przetwarzanie wsadowe, Włącz toodo możesz więcej pracy w bazie danych SQL przed osiągnięciem tych ograniczeń. 
* Tworzenie plików wsadowych jest również dla architektury, które używają wielu baz danych (dzielenia na fragmenty). wydajność Hello współpracy z każdej jednostki bazy danych nadal jest kluczowym czynnikiem Twojej ogólnej skalowalności. 

Jedną z zalet hello przy użyciu bazy danych SQL jest, że nie masz serwerów hello toomanage hello hosta bazy danych. Jednak ta infrastruktura zarządzanych również oznacza, że toothink inaczej o optymalizacji bazy danych. Nie można sprawdzić tooimprove hello bazy danych sprzętu lub siecią infrastruktury. Microsoft Azure określa tych środowisk. Hello obszaru głównego, który można kontrolować jest współdziałania aplikacji z bazy danych SQL. Tworzenie plików wsadowych jest jednym z tych optymalizacji. 

Pierwsza część papieru hello Hello sprawdza różnych technik przetwarzanie wsadowe aplikacji .NET, które używają bazy danych SQL. sekcje ostatnich dwóch Hello obejmują scenariusze i wskazówki dotyczące przetwarzanie wsadowe.

## <a name="batching-strategies"></a>Przetwarzanie wsadowe strategie
### <a name="note-about-timing-results-in-this-topic"></a>Należy pamiętać o wynikach czasu, w tym temacie
> [!NOTE]
> Wyniki nie są testów porównawczych, ale mają tooshow **względną wydajność**. Czasy są oparte na średnio co najmniej 10 uruchomień testów. Operacje są wstawia do pustej tabeli. Te testy zostały zmierzone pre-V12, a ich nie muszą odpowiadać toothroughput, które mogą pojawić się w bazie danych w wersji 12 przy użyciu nowego hello [warstw usług](sql-database-service-tiers.md). Hello względną zaletą hello przetwarzanie wsadowe technika powinny być podobne.
> 
> 

### <a name="transactions"></a>Transakcje
Wydaje się dziwne toobegin Przegląd przetwarzania wsadowego przez dyskutować transakcji. Ale użyj hello transakcji po stronie klienta ma Delikatny efekt przetwarzanie wsadowe po stronie serwera, który zapewnia lepszą wydajność. I transakcji można dodać przy tylko kilku wierszy kodu, więc zapewniają szybki sposób wydajności tooimprove sekwencyjnych operacji.

Należy wziąć pod uwagę hello następującego kodu C#, który zawiera sekwencję INSERT i aktualizowanie operacji na prostej tabeli.

    List<string> dbOperations = new List<string>();
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 1");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 2");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 3");
    dbOperations.Add("insert MyTable values ('new value',1)");
    dbOperations.Add("insert MyTable values ('new value',2)");
    dbOperations.Add("insert MyTable values ('new value',3)");

Hello następującego kodu ADO.NET sekwencyjnie wykonuje te operacje.

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        conn.Open();

        foreach(string commandString in dbOperations)
        {
            SqlCommand cmd = new SqlCommand(commandString, conn);
            cmd.ExecuteNonQuery();                   
        }
    }

Witaj najlepsze sposób toooptimize ten kod jest tooimplement jakiegoś typu po stronie klienta przetwarzanie wsadowe tych wywołań. Występuje wydajność hello tooincrease prosty sposób ten kod po prostu zawijania hello sekwencję wywołań w transakcji. Oto hello tego samego kodu, który używa transakcji.

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        conn.Open();
        SqlTransaction transaction = conn.BeginTransaction();

        foreach (string commandString in dbOperations)
        {
            SqlCommand cmd = new SqlCommand(commandString, conn, transaction);
            cmd.ExecuteNonQuery();
        }

        transaction.Commit();
    }

Transakcje są rzeczywiście używane w obu tych przykładów. W pierwszym przykładzie hello każdego wywołania poszczególnych jest transakcji niejawnej. W drugim przykładzie hello transakcji jawnej opakowuje wszystkich połączeń hello. Na powitania dokumentacji hello [dziennika transakcji zapisu z wyprzedzeniem](https://msdn.microsoft.com/library/ms186259.aspx), rekordów dziennika są wyczyszczone toohello dysku po zatwierdzeniu hello transakcji. Dlatego przy tym kolejnych wywołań w transakcji, hello dziennika transakcji toohello zapisu można opóźnienie do momentu hello transakcja została przekazana. W efekcie włączasz, przetwarzanie wsadowe dla dziennika transakcji serwera hello zapisy toohello.

Hello w poniższej tabeli przedstawiono niektóre wyniki testowania ad hoc. Witaj testy wykonywane hello, które same sekwencyjnych wstawia z włączonymi i wyłączonymi transakcji. Więcej perspektywy hello pierwszy zestaw testów został uruchomiony zdalnie z komputera przenośnego toohello bazy danych w systemie Microsoft Azure. Witaj drugi zestaw testów został uruchomiony z usługi w chmurze i że oba znajdowały się w obrębie hello sama baza danych Microsoft Azure datacenter (zachodnie stany USA). Witaj poniższej tabeli przedstawiono czas trwania hello w milisekundach sekwencyjnego wstawiania z włączonymi i wyłączonymi transakcji.

**TooAzure lokalnymi**:

| Operacje | Brak transakcji (ms) | W transakcji (ms) |
| --- | --- | --- |
| 1 |130 |402 |
| 10 |1208 |1226 |
| 100 |12662 |10395 |
| 1000 |128852 |102917 |

**Azure tooAzure (tym samym centrum danych)**:

| Operacje | Brak transakcji (ms) | W transakcji (ms) |
| --- | --- | --- |
| 1 |21 |26 |
| 10 |220 |56 |
| 100 |2145 |341 |
| 1000 |21479 |2756 |

> [!NOTE]
> Wyniki nie są testy. Zobacz hello [należy pamiętać o wynikach czasu, w tym temacie](#note-about-timing-results-in-this-topic).
> 
> 

Oparte na powitania poprzednie wyniki testu, zawijania jednej operacji w transakcji obniża wydajność. Ale zwiększania hello liczba operacji w ramach jednej transakcji zwiększenie wydajności hello staje się bardziej oznaczone. poprawę wydajności Hello jest bardziej widoczne również w przypadku, gdy wszystkie operacje są wykonywane w ramach centrum danych Microsoft Azure hello. Witaj większe opóźnienia korzystania z bazy danych SQL z centrum danych Microsoft Azure poza hello overshadows hello przyrost wydajności przy użyciu transakcji.

Mimo że hello użycie transakcji można zwiększyć wydajność, nadal zbyt[obserwować najlepsze rozwiązania dotyczące połączenia i transakcje](https://msdn.microsoft.com/library/ms187484.aspx). Zachowanie transakcji hello tak krótka jak to możliwe i zamknij hello połączenia z bazą danych, po zakończeniu pracy hello. przy użyciu instrukcji w poprzednim przykładzie hello Hello gwarantuje, że połączenie hello jest zamknięte po zakończeniu blok kodu kolejnych hello.

Hello w poprzednim przykładzie pokazano, dodać kod ADO.NET tooany transakcji lokalnej z dwóch wierszy. Transakcje oferują szybki sposób tooimprove hello wydajności kodu, który sprawia, że kolejne wstawiania, aktualizowania i usuwania operacji. Jednak dla hello największą wydajność, należy rozważyć zmianę hello kodu dalsze tootake zaletą po stronie klienta przetwarzanie wsadowe, takie jak parametry przechowywanymi w tabeli.

Aby uzyskać więcej informacji o transakcji w ADO.NET, zobacz [lokalne transakcje w ADO.NET](https://docs.microsoft.com/dotnet/framework/data/adonet/local-transactions).

### <a name="table-valued-parameters"></a>Parametry przechowywanymi w tabeli
Parametry przechowywanymi w tabeli obsługuje typach tabel zdefiniowanych przez użytkownika jako parametry w instrukcji języka Transact-SQL, procedury składowane i funkcje. Ta technika przetwarzanie wsadowe po stronie klienta umożliwia toosend wiele wierszy danych w ramach hello parametru przechowywanymi w tabeli. Parametry toouse przechowywanymi w tabeli, najpierw zdefiniować typu tabeli. Witaj następującej instrukcji języka Transact-SQL tworzy typ tabeli o nazwie **MyTableType**.

    CREATE TYPE MyTableType AS TABLE 
    ( mytext TEXT,
      num INT );


W kodzie, możesz utworzyć **DataTable** z hello dokładnie tej samej nazwy i typy hello typ tabeli. Przekazany **DataTable** w parametrze tekstu zapytania lub procedury składowanej wywołania. Witaj poniższy przykład przedstawia tej techniki:

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        DataTable table = new DataTable();
        // Add columns and rows. hello following is a simple example.
        table.Columns.Add("mytext", typeof(string));
        table.Columns.Add("num", typeof(int));    
        for (var i = 0; i < 10; i++)
        {
            table.Rows.Add(DateTime.Now.ToString(), DateTime.Now.Millisecond);
        }

        SqlCommand cmd = new SqlCommand(
            "INSERT INTO MyTable(mytext, num) SELECT mytext, num FROM @TestTvp",
            connection);

        cmd.Parameters.Add(
            new SqlParameter()
            {
                ParameterName = "@TestTvp",
                SqlDbType = SqlDbType.Structured,
                TypeName = "MyTableType",
                Value = table,
            });

        cmd.ExecuteNonQuery();
    }

W poprzednim przykładzie hello hello **SqlCommand** obiektu wstawia wiersze z parametrem przechowywanymi w tabeli  **@TestTvp** . Hello wcześniej utworzony **DataTable** obiektu przypisano parametru toothis o hello **SqlCommand.Parameters.Add** metody. Przetwarzanie wsadowe wstawia hello w jednym wywołać znacznie zwiększa wydajność hello za pośrednictwem sekwencyjnego wstawiania.

tooimprove hello poprzedni przykład, użyj procedury składowanej zamiast polecenia opartego na tekście. następujące polecenie języka Transact-SQL Hello tworzy procedury przechowywanej, która przyjmuje hello **SimpleTestTableType** parametru przechowywanymi w tabeli.

    CREATE PROCEDURE [dbo].[sp_InsertRows] 
    @TestTvp as MyTableType READONLY
    AS
    BEGIN
    INSERT INTO MyTable(mytext, num) 
    SELECT mytext, num FROM @TestTvp
    END
    GO

Następnie zmienić hello **SqlCommand** obiekt deklaracji w poniższych toohello przykładów kodu hello poprzedniej.

    SqlCommand cmd = new SqlCommand("sp_InsertRows", connection);
    cmd.CommandType = CommandType.StoredProcedure;

W większości przypadków przechowywanymi w tabeli Parametry mają równoważną lub lepszą wydajność niż innych technik, przetwarzanie wsadowe. Parametry przechowywanymi w tabeli są często zalecane, ponieważ są one bardziej elastyczne niż inne opcje. Na przykład innych technik, takich jak kopiowania zbiorczego SQL, tylko umożliwienia hello wstawiania nowych wierszy. Ale z parametrami przechowywanymi w tabeli, możesz użyć logikę w hello przechowywane procedury toodetermine wiersze, które są aktualizacje i które są wstawia. Typ tabeli Hello można także toocontain zmodyfikował kolumnę "Operacji", która wskazuje, czy hello określony wiersz powinien można wstawiać, zaktualizować lub usunąć.

Witaj w poniższej tabeli przedstawiono ad hoc wyników testu do użytku hello parametrów przechowywanymi w tabeli w milisekundach.

| Operacje | TooAzure lokalnymi (ms) | Tym samym centrum danych Azure (ms) |
| --- | --- | --- |
| 1 |124 |32 |
| 10 |131 |25 |
| 100 |338 |51 |
| 1000 |2615 |382 |
| 10 000 |23830 |3586 |

> [!NOTE]
> Wyniki nie są testy. Zobacz hello [należy pamiętać o wynikach czasu, w tym temacie](#note-about-timing-results-in-this-topic).
> 
> 

Hello są bardziej wydajne z tworzenie plików wsadowych jest oczywista. Poprzedni test sekwencyjnych hello 1000 operacji trwało 129 sekund hello poza centrum danych i 21 sekund od w ramach hello centrum danych. Jednak z parametrami przechowywanymi w tabeli, operacje 1000 wykorzystania tylko 2.6 sekund poza centrum danych hello i 0,4 sekund w obrębie centrum danych hello.

Aby uzyskać więcej informacji o parametrach przechowywanymi w tabeli, zobacz [zwracającej tabelę parametrów](https://msdn.microsoft.com/library/bb510489.aspx).

### <a name="sql-bulk-copy"></a>Kopiowania zbiorczego SQL
Kopiowania zbiorczego SQL jest w inny sposób tooinsert dużych ilości danych do docelowej bazy danych. Aplikacje .NET mogą używać hello **SqlBulkCopy** klasy tooperform zbiorczego wstawiania operacji. **SqlBulkCopy** przypomina w funkcji toohello narzędzie wiersza polecenia, **Bcp.exe**, lub hello instrukcji języka Transact-SQL **BULK INSERT**. Witaj Poniższy przykładowy kod przedstawia sposób hello kopiowania toobulk wierszy w źródle hello **DataTable**, tabeli, w tabeli docelowej toohello w programie SQL Server, MyTable.

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        using (SqlBulkCopy bulkCopy = new SqlBulkCopy(connection))
        {
            bulkCopy.DestinationTableName = "MyTable";
            bulkCopy.ColumnMappings.Add("mytext", "mytext");
            bulkCopy.ColumnMappings.Add("num", "num");
            bulkCopy.WriteToServer(table);
        }
    }

Istnieją przypadki, gdzie kopiowania zbiorczego jest preferowana przez parametry przechowywanymi w tabeli. Zobacz Tabela porównawcza hello przechowywanymi w tabeli parametrów lub w temacie hello BULK INSERT [zwracającej tabelę parametrów](https://msdn.microsoft.com/library/bb510489.aspx).

Witaj następujące wyniki testu ad hoc Pokaż hello wydajność przetwarzania wsadowego z **SqlBulkCopy** w milisekundach.

| Operacje | TooAzure lokalnymi (ms) | Tym samym centrum danych Azure (ms) |
| --- | --- | --- |
| 1 |433 |57 |
| 10 |441 |32 |
| 100 |636 |53 |
| 1000 |2535 |341 |
| 10 000 |21605 |2737 |

> [!NOTE]
> Wyniki nie są testy. Zobacz hello [należy pamiętać o wynikach czasu, w tym temacie](#note-about-timing-results-in-this-topic).
> 
> 

W mniejszych partii hello korzystanie z przechowywanymi w tabeli parametrów outperformed hello **SqlBulkCopy** klasy. Jednak **SqlBulkCopy** wykonano % 12-31 szybciej niż przechowywanymi w tabeli parametrów dla testów hello 1000 i 10 000 wierszy. Przechowywanymi w tabeli parametrów, takich jak **SqlBulkCopy** jest dobra opcja w przypadku operacji wsadowej operacji wstawienia, szczególnie w porównaniu toohello wydajność operacji niewsadowego.

Aby uzyskać więcej informacji dotyczących kopiowania zbiorczego w ADO.NET, zobacz [operacje kopiowania masowego w programie SQL Server](https://msdn.microsoft.com/library/7ek5da1a.aspx).

### <a name="multiple-row-parameterized-insert-statements"></a>Instrukcje sparametryzowana WSTAWIĆ wiele wierszy
Jeden alternatywą dla małych partii jest tooconstruct dużej sparametryzowanych instrukcji INSERT, która wstawia wiele wierszy. Witaj poniższy przykład kodu pokazuje tej metody.

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        string insertCommand = "INSERT INTO [MyTable] ( mytext, num ) " +
            "VALUES (@p1, @p2), (@p3, @p4), (@p5, @p6), (@p7, @p8), (@p9, @p10)";

        SqlCommand cmd = new SqlCommand(insertCommand, connection);

        for (int i = 1; i <= 10; i += 2)
        {
            cmd.Parameters.Add(new SqlParameter("@p" + i.ToString(), "test"));
            cmd.Parameters.Add(new SqlParameter("@p" + (i+1).ToString(), i));
        }

        cmd.ExecuteNonQuery();
    }


W tym przykładzie oznacza tooshow hello podstawowe pojęcia. Scenariusz bardziej realistyczne czy pętli ciąg hello wymagane jednostek tooconstruct hello zapytania i parametry polecenia hello jednocześnie. Istnieje ograniczenie tooa całkowitej liczby parametrów zapytania 2100, co ogranicza hello całkowitą liczbę wierszy, które mogą być przetwarzane w ten sposób.

powitania po ad hoc wydajności hello Pokaż wyniki testu tego typu instrukcji insert w milisekundach.

| Operacje | Parametry z wartościami przechowywanymi w tabeli (ms) | Wstaw jednej instrukcji (ms) |
| --- | --- | --- |
| 1 |32 |20 |
| 10 |30 |25 |
| 100 |33 |51 |

> [!NOTE]
> Wyniki nie są testy. Zobacz hello [należy pamiętać o wynikach czasu, w tym temacie](#note-about-timing-results-in-this-topic).
> 
> 

Ta metoda może być nieco większą partii, które są mniej niż 100 wierszy. Mimo że ulepszenie hello jest mały, ta metoda jest inną opcją, która może działać również w danym scenariuszu określonej aplikacji.

### <a name="dataadapter"></a>Element DataAdapter
Witaj **element DataAdapter** klasa umożliwia toomodify **DataSet** obiekt i spróbuj przesłać zmiany hello operacji INSERT, UPDATE i DELETE. Jeśli używasz hello **element DataAdapter** w ten sposób jest ważne, toonote, który upłynąć wywołania są wykonywane dla każdej operacji distinct. wydajność tooimprove, użyj hello **UpdateBatchSize** właściwości toohello liczba operacji, które należy umieścić w zadaniu wsadowym, w czasie. Aby uzyskać więcej informacji, zobacz [wykonywania wsadowego operacje przy użyciu obiektów DataAdapter](https://msdn.microsoft.com/library/aadf8fk2.aspx).

### <a name="entity-framework"></a>Programu Entity framework
Entity Framework nie obsługuje obecnie przetwarzanie wsadowe. Deweloperzy różne społeczności hello podjęto toodemonstrate rozwiązania, takie jak zastąpienie hello **SaveChanges** metody. Ale zazwyczaj są rozwiązania hello aplikacji złożonych i dostosowane toohello i modelu danych. Hello Entity Framework w witrynie codeplex projektu jest obecnie strona dyskusji na żądanie tej funkcji. tooview te informacje, zobacz [spotkania uwagami - 2 sierpień 2012](http://entityframework.codeplex.com/wikipage?title=Design%20Meeting%20Notes%20-%20August%202%2c%202012).

### <a name="xml"></a>XML
Aby informacje były kompletne uważamy, jest ważne tootalk o XML jako strategii przetwarzanie wsadowe. Jednak użycie hello XML ma nie zalet w porównaniu z innych metod i kilka wady. podejście Hello jest podobnych tootable o wartościach parametrów, ale plik XML lub ciąg jest przekazywany tooa przechowywane procedury zamiast tabeli zdefiniowane przez użytkownika. procedury przechowywane Hello analizuje polecenia hello hello przechowywane procedury.

Istnieje kilka wady toothis podejścia:

* Praca z danymi XML może być skomplikowane i błąd podatnych na błędy.
* Podczas analizowania hello XML na powitania bazy danych może być użycie Procesora CPU.
* W większości przypadków ta metoda jest mniejsza niż parametry przechowywanymi w tabeli.

Z tego względu nie jest zalecane użycie hello XML dla partii zapytań.

## <a name="batching-considerations"></a>Przetwarzanie wsadowe uwagi
Witaj następujące sekcje zawierają więcej wskazówki dotyczące stosowania hello przetwarzanie wsadowe w aplikacjach baz danych SQL.

### <a name="tradeoffs"></a>Wady i zalety
W zależności od architektury przetwarzanie wsadowe może obejmować zależności między wydajność i odporność. Na przykład Rozważmy scenariusz hello, których rola użytkownika nieoczekiwanie ulegnie awarii. W przypadku utraty jednego wiersza danych, wpływ hello jest mniejszy niż wpływ hello utraty duży wsadu nieprzesłane wierszy. Istnieje większe ryzyko, gdy bufor wierszy przed ich wysłaniem toohello bazy danych w oknie określonego czasu.

Ze względu na to zależnościami ocenić hello typ operacji tego wsadowej. Bardziej agresywnie partii (większe partie i dłuższy czas systemu windows) przy użyciu danych jest mniej istotny.

### <a name="batch-size"></a>Rozmiar partii
Nasze testy nie było zwykle nie partie dużych toobreaking korzystać na mniejsze fragmenty. W rzeczywistości często tej części pola spowodowała wolniej niż przesyłanie dużych pojedyncza partia. Na przykład Rozważmy scenariusz, w którym ma być tooinsert 1000 wierszy. Witaj poniższej tabeli przedstawiono czas potrzebny toouse przechowywanymi w tabeli parametrów tooinsert 1000 wierszy, gdy podzielona na mniejsze partie.

| Rozmiar partii | Liczba iteracji | Parametry z wartościami przechowywanymi w tabeli (ms) |
| --- | --- | --- |
| 1000 |1 |347 |
| 500 |2 |355 |
| 100 |10 |465 |
| 50 |20 |630 |

> [!NOTE]
> Wyniki nie są testy. Zobacz hello [należy pamiętać o wynikach czasu, w tym temacie](#note-about-timing-results-in-this-topic).
> 
> 

Widać, że hello najlepszą wydajność 1000 wierszy jest toosubmit ich wszystkich naraz. W innych testach (nie jest tutaj widoczny) wystąpił toobreak przyrost wydajności małych partii 10000 wiersza w dwóch partie 5000. Ale schemat tabeli hello tych testów jest stosunkowo proste, należy wykonać testy na określonych danych i tooverify rozmiary partii tych wyników.

Innym czynnikiem tooconsider jest Jeśli całkowita liczba partii hello stanie się zbyt duży, bazy danych SQL może ograniczenie przepustowości i odmówić toocommit hello partii. Dla uzyskania najlepszych wyników hello testu toodetermine Twojego danego scenariusza Jeśli rozmiar partii idealne. Rozmiar partii hello można skonfigurować w wprowadzanie korekt szybkie tooenable środowiska uruchomieniowego na podstawie wydajności lub błędy.

Ponadto równoważenie hello rozmiar wsadu hello ryzyka hello skojarzone z przetwarzanie wsadowe. Jeśli ma błędów przejściowych lub roli hello nie powiedzie się, należy wziąć pod uwagę konsekwencje hello ponowną próbą wykonania operacji hello lub utraty danych hello w partii hello.

### <a name="parallel-processing"></a>Przetwarzanie równoległe
Co zrobić, jeśli trwało podejście hello zmniejsza rozmiar partii hello, ale używana wiele wątków tooexecute hello pracy? Ponownie Nasze testy wykazały, czy partie mniejszych wielowątkowe najczęściej wykonywane gorsza niż pojedyncza partia większy. Witaj następującego testu prób tooinsert 1000 wierszy w partii równoległych co najmniej jeden. Ten test pokazuje, jak więcej jednoczesnych partie faktycznie obniżenie wydajności.

| Rozmiar partii [iteracji] | Dwoma wątkami (ms) | Cztery wątków (ms) | Sześć wątków (ms) |
| --- | --- | --- | --- |
| 1000 [1] |277 |315 |266 |
| 500 [2] |548 |278 |256 |
| 250 [4] |405 |329 |265 |
| 100 [10] |488 |439 |391 |

> [!NOTE]
> Wyniki nie są testy. Zobacz hello [należy pamiętać o wynikach czasu, w tym temacie](#note-about-timing-results-in-this-topic).
> 
> 

Istnieje kilka potencjalnych przyczyn hello spadek wydajności z powodu tooparallelism:

* Istnieje wiele wywołań awarią sieci, zamiast jednego.
* Wiele operacji na jednej tabeli może spowodować rywalizację i blokowania.
* Występują ogólne koszty związane z wielowątkowości.
* wydatków Hello otwarcia wielu połączeń przeważa nad hello zaletą przetwarzania równoległego.

W przypadku skierowania różnych tabelach lub baz danych, jest możliwe toosee wydajności uzyskania z tej strategii. Dzielenia na fragmenty bazy danych lub federacje byłoby scenariusz dla tej metody. Dzielenia na fragmenty używa wielu baz danych i bazy danych tooeach różnych danych trasy. Jeżeli każdej partii małych będzie tooa innej bazy danych, może być skuteczniejsza następnie operacji hello równolegle. Jednak hello są bardziej wydajne nie jest wystarczająco znaczące toouse jako podstawy hello decyzji toouse bazy danych dzielenia na fragmenty w rozwiązaniu.

W niektórych projektach wykonywanie równoległe partii mniejszych może spowodować lepszą przepustowość żądań w systemie pod obciążeniem. W takim przypadku mimo że jest to szybsza tooprocess pojedyncza partia większy, wiele instancji równoległego przetwarzania może być bardziej wydajne.

Jeśli używasz wykonywanie równoległe, należy wziąć pod uwagę kontrolowanie hello maksymalną liczbę wątków roboczych. Mniejsza liczba może spowodować mniej rywalizacji i skrócić czas wykonywania. Należy również rozważyć hello dodatkowego obciążenia, które ten zostaje umieszczony na powitania docelowa baza danych połączenia i transakcji.

### <a name="related-performance-factors"></a>Czynniki wydajności związanych z
Typowe wskazówki dotyczące wydajności bazy danych ma wpływ również na przetwarzanie wsadowe. Na przykład, Wstaw wydajność jest ograniczona do tabel, które mają duże kluczem podstawowym lub wiele nieklastrowanych indeksów.

Jeśli parametry przechowywanymi w tabeli, użyj procedury składowanej, możesz użyć polecenia hello **SET NOCOUNT ON** na początku hello hello procedury. Ta instrukcja pomija hello powrotu hello liczbę wierszy hello wpływ hello procedury. Jednak w naszym testy hello użycie **SET NOCOUNT ON** nie miała wpływu albo obniżenie wydajności. Witaj procedury przechowywane testu został proste za pomocą jednej **Wstaw** polecenie hello parametru przechowywanymi w tabeli. Istnieje możliwość, że bardziej złożonych procedur składowanych będzie korzystać z tej instrukcji. Ale nie zakłada się, że dodawanie **SET NOCOUNT ON** tooyour przechowywane procedury automatycznie poprawia wydajność. toounderstand hello efekt, przetestować procedurę składowaną z włączonymi i wyłączonymi hello **SET NOCOUNT ON** instrukcji.

## <a name="batching-scenarios"></a>Przetwarzanie wsadowe scenariuszy
Witaj poniższych sekcjach opisano sposób toouse przechowywanymi w tabeli parametrów w trzech scenariuszy aplikacji. pierwszy scenariusz Hello pokazuje, jak buforowanie i przetwarzanie wsadowe mogą współdziałać ze sobą. drugi scenariusz Hello zwiększa wydajność, wykonując operacje główny szczegółowy w wywołaniu jednej procedury składowanej. Witaj końcowego scenariuszu przedstawiono sposób toouse przechowywanymi w tabeli parametrów w operacji "UPSERT".

### <a name="buffering"></a>Buforowanie
Istnieje kilka scenariuszy, które są oczywiste candidate dla przetwarzania wsadowego, istnieje wiele scenariuszy, które można wykorzystać przetwarzania wsadowego przez przetwarzanie opóźnione. Jednak również opóźnione przetwarzanie niesie większe ryzyko, że hello dane zostaną utracone w przypadku hello wystąpił nieoczekiwany błąd. Jest to zagrożenie toounderstand ważne i należy wziąć pod uwagę konsekwencje hello.

Rozważmy na przykład aplikacji sieci web służący do śledzenia historii nawigacji hello każdego użytkownika. Na każdym żądaniu strony aplikacji hello można utworzyć widok strony użytkownika hello toorecord wywołania bazy danych. Jednak buforowanie użytkowników hello nawigacji działania, a następnie wysyła tę bazę danych toohello danych w partiach można osiągnąć wyższą wydajność i skalowalność. Możesz wyzwolić hello aktualizacji bazy danych przez czas, który upłynął i/lub rozmiaru buforu. Na przykład reguła można określić tej partii hello powinna zostać przetworzona po 20 sekund lub gdy bufor hello osiągnie 1000 elementów.

następujące Hello przykład kodu wykorzystuje [rozszerzenia reaktywne - Rx](https://msdn.microsoft.com/data/gg577609) tooprocess buforowane zdarzenia wywoływane przez klasę monitorowania. Gdy hello wypełnienia buforu lub osiągnięto limit czasu, hello partii danych użytkownika jest wysyłana bazy danych toohello z parametrem przechowywanymi w tabeli.

Witaj poniższe NavHistoryData klasy modeli hello użytkownika nawigacji informacje. Zawiera podstawowe informacje, takie jak identyfikator użytkownika hello, adres URL hello dostęp i hello czas dostępu.

    public class NavHistoryData
    {
        public NavHistoryData(int userId, string url, DateTime accessTime)
        { UserId = userId; URL = url; AccessTime = accessTime; }
        public int UserId { get; set; }
        public string URL { get; set; }
        public DateTime AccessTime { get; set; }
    }

Witaj NavHistoryDataMonitor klasy jest odpowiedzialny za buforowanie bazy danych toohello danych hello użytkownika nawigacji. Zawiera metodę RecordUserNavigationEntry, która odpowiada za wywoływanie **OnAdded** zdarzeń. Witaj poniższy kod przedstawia hello logikę konstruktora, który używa Rx toocreate zauważalne kolekcji na podstawie hello zdarzenia. Subskrybuje następnie toothis zauważalne kolekcji z metodą buforu hello. przeciążenie Hello Określa, że ten bufor hello mają być wysyłane co 20 sekund lub 1000 wpisów.

    public NavHistoryDataMonitor()
    {
        var observableData =
            Observable.FromEventPattern<NavHistoryDataEventArgs>(this, "OnAdded");

        observableData.Buffer(TimeSpan.FromSeconds(20), 1000).Subscribe(Handler);           
    }

obsługi Hello konwertuje wszystkie elementy hello buforowane na typ przechowywanymi w tabeli i następnie przekazuje tej procedury przechowywane tooa typu tej partii hello procesów. Witaj poniższy kod przedstawia hello pełnej definicji hello NavHistoryDataEventArgs i hello NavHistoryDataMonitor klasy.

    public class NavHistoryDataEventArgs : System.EventArgs
    {
        public NavHistoryDataEventArgs(NavHistoryData data) { Data = data; }
        public NavHistoryData Data { get; set; }
    }

    public class NavHistoryDataMonitor
    {
        public event EventHandler<NavHistoryDataEventArgs> OnAdded;

        public NavHistoryDataMonitor()
        {
            var observableData =
                Observable.FromEventPattern<NavHistoryDataEventArgs>(this, "OnAdded");

            observableData.Buffer(TimeSpan.FromSeconds(20), 1000).Subscribe(Handler);           
        }

        public void RecordUserNavigationEntry(NavHistoryData data)
        {    
            if (OnAdded != null)
                OnAdded(this, new NavHistoryDataEventArgs(data));
        }

        protected void Handler(IList<EventPattern<NavHistoryDataEventArgs>> items)
        {
            DataTable navHistoryBatch = new DataTable("NavigationHistoryBatch");
            navHistoryBatch.Columns.Add("UserId", typeof(int));
            navHistoryBatch.Columns.Add("URL", typeof(string));
            navHistoryBatch.Columns.Add("AccessTime", typeof(DateTime));
            foreach (EventPattern<NavHistoryDataEventArgs> item in items)
            {
                NavHistoryData data = item.EventArgs.Data;
                navHistoryBatch.Rows.Add(data.UserId, data.URL, data.AccessTime);
            }

            using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
            {
                connection.Open();

                SqlCommand cmd = new SqlCommand("sp_RecordUserNavigation", connection);
                cmd.CommandType = CommandType.StoredProcedure;

                cmd.Parameters.Add(
                    new SqlParameter()
                    {
                        ParameterName = "@NavHistoryBatch",
                        SqlDbType = SqlDbType.Structured,
                        TypeName = "NavigationHistoryTableType",
                        Value = navHistoryBatch,
                    });

                cmd.ExecuteNonQuery();
            }
        }
    }

toouse tej klasy buforowania aplikacji hello tworzy obiektu NavHistoryDataMonitor statycznego. Każdym razem, użytkownik uzyskuje dostęp do strony, aplikacji hello wywołuje metodę NavHistoryDataMonitor.RecordUserNavigationEntry hello. Hello buforowanie logiki przebieg tootake nad wysyła te bazy danych toohello wpisów w partiach.

### <a name="master-detail"></a>Wzorzec szczegół
Parametry przechowywanymi w tabeli są przydatne w scenariuszach INSERT proste. Jednak może być trudniejsza wstawia toobatch obejmujące więcej niż jedna tabela. scenariusz "wzorzec/szczegół" Hello jest dobrym przykładem. główny tabeli Hello identyfikuje hello podstawowej jednostki. Co najmniej jedna tabela szczegółów przechowywać więcej danych dotyczących hello jednostki. W tym scenariuszu relacje klucza obcego wymusić relacji hello szczegóły tooa unikatowe jednostki wzorca. Należy wziąć pod uwagę uproszczonej wersji tabeli PurchaseOrder i jego skojarzonej tabeli OrderDetail. Hello następującego języka Transact-SQL tworzy hello PurchaseOrder tabeli z czterech kolumn: OrderID, OrderDate CustomerID i stanu.

    CREATE TABLE [dbo].[PurchaseOrder](
    [OrderID] [int] IDENTITY(1,1) NOT NULL,
    [OrderDate] [datetime] NOT NULL,
    [CustomerID] [int] NOT NULL,
    [Status] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrder] 
    PRIMARY KEY CLUSTERED ( [OrderID] ASC ))

Każdej kolejności zawiera co najmniej jeden produkt. Te informacje są przechwytywane hello PurchaseOrderDetail tabeli. Hello następującego języka Transact-SQL tworzy hello PurchaseOrderDetail tabeli z kolumnami pięć: OrderID, OrderDetailID ProductID, UnitPrice i OrderQty.

    CREATE TABLE [dbo].[PurchaseOrderDetail](
    [OrderID] [int] NOT NULL,
    [OrderDetailID] [int] IDENTITY(1,1) NOT NULL,
    [ProductID] [int] NOT NULL,
    [UnitPrice] [money] NULL,
    [OrderQty] [smallint] NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrderDetail] PRIMARY KEY CLUSTERED 
    ( [OrderID] ASC, [OrderDetailID] ASC ))

z tabeli PurchaseOrder hello Hello OrderID kolumny w tabeli PurchaseOrderDetail hello musi odwoływać się zamówienia. po definicji klucza obcego Hello wymusza to ograniczenie.

    ALTER TABLE [dbo].[PurchaseOrderDetail]  WITH CHECK ADD 
    CONSTRAINT [FK_OrderID_PurchaseOrder] FOREIGN KEY([OrderID])
    REFERENCES [dbo].[PurchaseOrder] ([OrderID])

W parametrach przechowywanymi w tabeli toouse kolejności musi mieć jeden typ tabeli zdefiniowany przez użytkownika dla każdej tabeli docelowej.

    CREATE TYPE PurchaseOrderTableType AS TABLE 
    ( OrderID INT,
      OrderDate DATETIME,
      CustomerID INT,
      Status NVARCHAR(50) );
    GO

    CREATE TYPE PurchaseOrderDetailTableType AS TABLE 
    ( OrderID INT,
      ProductID INT,
      UnitPrice MONEY,
      OrderQty SMALLINT );
    GO

Następnie zdefiniuj procedury przechowywanej, która akceptuje tabele tych typów. Ta procedura umożliwia partii toolocally aplikacji zestaw zleceń i szczegółów zamówienia w pojedynczym wywołaniu. Witaj następującego języka Transact-SQL zawiera hello deklaracji całą procedurę składowaną w ramach tego przykładu zamówienia zakupu.

    CREATE PROCEDURE sp_InsertOrdersBatch (
    @orders as PurchaseOrderTableType READONLY,
    @details as PurchaseOrderDetailTableType READONLY )
    AS
    SET NOCOUNT ON;

    -- Table that connects hello order identifiers in hello @orders
    -- table with hello actual order identifiers in hello PurchaseOrder table
    DECLARE @IdentityLink AS TABLE ( 
    SubmittedKey int, 
    ActualKey int, 
    RowNumber int identity(1,1)
    );

          -- Add new orders toohello PurchaseOrder table, storing hello actual
    -- order identifiers in hello @IdentityLink table   
    INSERT INTO PurchaseOrder ([OrderDate], [CustomerID], [Status])
    OUTPUT inserted.OrderID INTO @IdentityLink (ActualKey)
    SELECT [OrderDate], [CustomerID], [Status] FROM @orders ORDER BY OrderID;

    -- Match hello passed-in order identifiers with hello actual identifiers
    -- and complete hello @IdentityLink table for use with inserting hello details
    WITH OrderedRows As (
    SELECT OrderID, ROW_NUMBER () OVER (ORDER BY OrderID) As RowNumber 
    FROM @orders
    )
    UPDATE @IdentityLink SET SubmittedKey = M.OrderID
    FROM @IdentityLink L JOIN OrderedRows M ON L.RowNumber = M.RowNumber;

    -- Insert hello order details into hello PurchaseOrderDetail table, 
          -- using hello actual order identifiers of hello master table, PurchaseOrder
    INSERT INTO PurchaseOrderDetail (
    [OrderID],
    [ProductID],
    [UnitPrice],
    [OrderQty] )
    SELECT L.ActualKey, D.ProductID, D.UnitPrice, D.OrderQty
    FROM @details D
    JOIN @IdentityLink L ON L.SubmittedKey = D.OrderID;
    GO

W tym przykładzie hello zdefiniowany lokalnie @IdentityLink w tabeli są przechowywane wartości rzeczywistych OrderID hello hello nowo wstawić wierszy. Te identyfikatory kolejności różnią się od wartości tymczasowe OrderID hello w hello @orders i @details parametry przechowywanymi w tabeli. Z tego powodu hello @IdentityLink tabeli następnie łączy w wartości OrderID hello hello @orders toohello rzeczywistych OrderID wartości parametrów dla hello nowych wierszy w tabeli PurchaseOrder hello. Po wykonaniu tego kroku hello @IdentityLink tabela ułatwia wstawianie szczegółów zamówienia hello z hello rzeczywiste OrderID, spełniająca hello ograniczenie klucza obcego.

Tę procedurę składowaną można z kodu lub inne wywołania języka Transact-SQL. W sekcji hello przechowywanymi w tabeli parametrów tego dokumentu, na przykład kodu. Witaj następującego języka Transact-SQL pokazuje, jak toocall hello sp_InsertOrdersBatch.

    declare @orders as PurchaseOrderTableType
    declare @details as PurchaseOrderDetailTableType

    INSERT @orders 
    ([OrderID], [OrderDate], [CustomerID], [Status])
    VALUES(1, '1/1/2013', 1125, 'Complete'),
    (2, '1/13/2013', 348, 'Processing'),
    (3, '1/12/2013', 2504, 'Shipped')

    INSERT @details
    ([OrderID], [ProductID], [UnitPrice], [OrderQty])
    VALUES(1, 10, $11.50, 1),
    (1, 12, $1.58, 1),
    (2, 23, $2.57, 2),
    (3, 4, $10.00, 1)

    exec sp_InsertOrdersBatch @orders, @details

To rozwiązanie umożliwia toouse każdej partii zestaw wartości OrderID, które rozpoczynają się do 1. Te wartości tymczasowe OrderID opisano relacje hello w partii hello, ale hello rzeczywiste OrderID wartości są określane w czasie hello hello operacji insert. Można uruchomić hello tych samych instrukcji w poprzednim przykładzie hello wielokrotnie i wygenerować unikatowy zamówienia hello bazy danych. Z tego powodu należy rozważyć dodanie więcej logiki kodu lub bazy danych, która zapobiega zduplikowane zleceń za pomocą tej techniki partie.

W tym przykładzie pokazano, że można zebrać bardziej złożone operacje bazy danych, takimi jak operacje wzorzec szczegół za pomocą parametrów przechowywanymi w tabeli.

### <a name="upsert"></a>UPSERT
Inny przetwarzanie wsadowe scenariusz obejmuje jednoczesne aktualizowanie istniejących wierszy i wstawianie nowych wierszy. Ta operacja jest czasami tooas określonej operacji "UPSERT" (aktualizacja + insert). Zamiast wprowadzania tooINSERT wywołań i aktualizacji, instrukcji MERGE hello jest najlepiej nadaje się toothis zadań. Hello instrukcji MERGE można wykonywać zarówno wstawiania i aktualizowania operacji w pojedynczym wywołaniu.

Parametry przechowywanymi w tabeli mogą być używane z aktualizacji tooperform instrukcji MERGE hello i wstawia. Rozważmy na przykład uproszczony tabeli pracowników, która zawiera następujące kolumny hello: identyfikator pracownika, FirstName, LastName, SocialSecurityNumber:

    CREATE TABLE [dbo].[Employee](
    [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
    [FirstName] [nvarchar](50) NOT NULL,
    [LastName] [nvarchar](50) NOT NULL,
    [SocialSecurityNumber] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_Employee] PRIMARY KEY CLUSTERED 
    ([EmployeeID] ASC ))

W tym przykładzie można użyć hello fakt, że ten hello SocialSecurityNumber jest unikatowy tooperform scalania wielu pracowników. Najpierw utwórz hello typu tabeli zdefiniowanego przez użytkownika:

    CREATE TYPE EmployeeTableType AS TABLE 
    ( Employee_ID INT,
      FirstName NVARCHAR(50),
      LastName NVARCHAR(50),
      SocialSecurityNumber NVARCHAR(50) );
    GO

Następnie utwórz procedurę składowaną lub napisać kod, że używa hello aktualizacji hello tooperform instrukcji MERGE i wstawiania. Witaj poniższym przykładzie użyto hello instrukcji MERGE dla parametru przechowywanymi w tabeli, @employees, typu EmployeeTableType. Witaj zawartość hello @employees tabeli nie są wyświetlane tutaj.

    MERGE Employee AS target
    USING (SELECT [FirstName], [LastName], [SocialSecurityNumber] FROM @employees) 
    AS source ([FirstName], [LastName], [SocialSecurityNumber])
    ON (target.[SocialSecurityNumber] = source.[SocialSecurityNumber])
    WHEN MATCHED THEN 
    UPDATE SET
    target.FirstName = source.FirstName, 
    target.LastName = source.LastName
    WHEN NOT MATCHED THEN
       INSERT ([FirstName], [LastName], [SocialSecurityNumber])
       VALUES (source.[FirstName], source.[LastName], source.[SocialSecurityNumber]);

Aby uzyskać więcej informacji zobacz hello dokumentacja i przykłady dotyczące hello instrukcji MERGE. Mimo że powitalne służbowe może być wykonana w kroku wielu przechowywane wywołania procedury z oddzielnych operacji INSERT i UPDATE, hello instrukcji MERGE jest bardziej wydajny. Kod bazy danych można także konstruować wywołania języka Transact-SQL, które użyj instrukcji MERGE hello bezpośrednio, bez konieczności dwóch wywołania bazy danych dla INSERT i UPDATE.

## <a name="recommendation-summary"></a>Zalecenie podsumowania
Witaj Poniższa lista zawiera podsumowanie hello przetwarzanie wsadowe zalecenia omówione w tym temacie:

* Użycie buforowania i przetwarzanie wsadowe tooincrease hello wydajność i skalowalność aplikacji bazy danych SQL.
* Zrozumienie wady i zalety hello między przetwarzanie wsadowe buforowania i odporność. Podczas awarii roli hello ryzyko utraty nieprzetworzone partii strategicznych danych biznesowych mogą przeważają korzyści hello wydajności przetwarzania wsadowego.
* Próba tookeep wszystkie bazy danych toohello wywołań w opóźnienia tooreduce jednego centrum danych.
* Jeśli wybierzesz pojedyncza technika przetwarzanie wsadowe parametry przechowywanymi w tabeli oferują hello najlepszą wydajność i elastyczność.
* Dla hello najszybszym Wstaw wydajności, wykonaj następujące ogólne wytyczne, ale test danego scenariusza:
  * < 100 wierszy użyj jednego sparametryzowane polecenia INSERT.
  * < 1000 wierszy użyj parametrów przechowywanymi w tabeli.
  * Aby uzyskać > = 1000 wierszy, użyj SqlBulkCopy.
* Dla aktualizacji i operacji usunięcia, parametry przechowywanymi w tabeli za pomocą procedury składowanej logikę, która określa hello poprawne działanie w każdym wierszu w parametrze tabeli hello.
* Informacje dotyczące rozmiaru partii:
  * Użyj hello największy rozmiarów partii odpowiednich dla aplikacji i wymaganiami biznesowymi.
  * Wydajności hello równoważenia uzyskać dużych partii z ryzykiem hello tymczasowe lub poważnej awarii. Co to jest konsekwencją hello ponownych prób i utraty danych hello w partii hello? 
  * Przetestuj hello największy partii rozmiar tooverify bazy danych SQL go nie odrzucić.
  * Utwórz ustawienia konfiguracji tej partii kontroli, takich jak rozmiar partii hello lub hello buforowania przedział czasu. Te ustawienia zapewniają elastyczność. Przetwarzanie wsadowe zachowanie w środowisku produkcyjnym bez ponownego wdrożenia usługi w chmurze hello hello, można zmienić.
* Unikaj wykonywanie równoległe w partii, które pracują na pojedynczej tabeli w jednej bazie danych. Jeśli wybierzesz toodivide pojedyncza partia przez wiele wątków roboczych, uruchom testy toodetermine hello idealne liczba wątków. Po nieokreślone wartości progowej więcej wątków będzie obniżyć wydajność, a nie powinna ona być.
* Należy wziąć pod uwagę buforowanie włączone rozmiaru i czasu sposób stosowania przetwarzania wsadowego dla scenariuszy.

## <a name="next-steps"></a>Następne kroki
Ten artykuł skupia się na sposób projektowania baz danych i techniki tworzenia kodu powiązane toobatching może zwiększyć Twojej aplikacji wydajności i skalowalności. Ale tylko jeden składnik w ogólnej strategii. Więcej sposobów tooimprove wydajności i skalowalności, zobacz [wytyczne dotyczące wydajności bazy danych SQL Azure dla pojedynczej bazy danych](sql-database-performance-guidance.md) i [zagadnienia dotyczące cen i wydajności dla elastycznej puli](sql-database-elastic-pool-guidance.md).

