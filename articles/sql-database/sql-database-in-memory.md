---
title: "technologie SQL bazy danych w pamięci aaaAzure | Dokumentacja firmy Microsoft"
description: "Technologie usługi Azure SQL bazy danych w pamięci znacząco poprawić wydajność hello transakcyjne i obciążeń analizy. Dowiedz się, jak tootake korzystać z tych technologii."
services: sql-database
documentationCenter: 
author: jodebrui
manager: jhubbard
editor: 
ms.assetid: 250ef341-90e5-492f-b075-b4750d237c05
ms.service: sql-database
ms.custom: develop databases
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jodebrui
ms.openlocfilehash: 1bacd7297b2f9b018853088eabf2a2ee66a9cb43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-performance-by-using-in-memory-technologies-in-sql-database"></a>Optymalizacja wydajności za pomocą technologii w pamięci w bazie danych SQL

Dzięki użyciu technologii w pamięci w bazie danych SQL Azure, można osiągnąć ulepszenia wydajności z różnych obciążeń: transakcyjna (transakcyjnego przetwarzania online (OLTP)), analytics (online analytical processing (OLAP)) i mieszanego (hybrydowe przetwarzanie analityczne/transakcji (HTAP)). Z powodu hello większą wydajność zapytań i przetwarzania transakcji, technologie w pamięci też pomóc Ci tooreduce kosztów. Zwykle nie trzeba hello tooupgrade cenowym wzrost wydajności tooachieve hello w bazie danych. W niektórych przypadkach, nawet można zmniejszyć hello cenowym podczas nadal występuje ulepszenia wydajności z technologiami w pamięci.

Poniżej przedstawiono dwa przykłady sposobu OLTP w pamięci pomogła toosignificantly poprawić wydajność:

- Za pomocą OLTP w pamięci [rozwiązań biznesowych kworum został toodouble stanie ich obciążenie poprawienie Dtu 70%](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database).
    - Oznacza jednostek dtu w warstwie *jednostki przepływności bazy danych*, a także mesurement zużycia zasobów.
- Witaj poniżej film wideo przedstawia znaczne ulepszenia w zużycie zasobów z przykładowe obciążenie: [OLTP w pamięci wideo bazy danych SQL Azure](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB).
    - Aby uzyskać więcej informacji, zobacz hello wpisie w blogu: [OLTP w pamięci w blogu blogu bazy danych SQL Azure](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)

Technologie w pamięci są dostępne wszystkie bazy danych w warstwie Premium hello, w tym baz danych w puli elastycznej Premium.

Witaj poniższego klipu wideo wyjaśniono, potencjalne zwiększenie wydajności w przypadku technologii w pamięci w bazie danych SQL Azure. Należy pamiętać, że hello są bardziej wydajne zawsze wyświetlany zależy od wielu czynników, takich jak rodzaj hello hello obciążenia i dane, wzorca dostępu hello bazy danych i tak dalej.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-In-Memory-Technologies/player]
>
>

Baza danych SQL Azure ma hello następujące technologie w pamięci:

- *OLTP w pamięci* zwiększa przepustowość i zmniejsza opóźnienia przetwarzania transakcji. Scenariusze, w których warto skorzystać z OLTP w pamięci są: przetwarzanie takich jak handlowych i gier, wprowadzanie danych z urządzeń IoT, buforowanie ładowania danych i tabeli tymczasowej i scenariusze zmiennej tabeli lub zdarzenia transakcji wysokiej przepustowości.
- *Klastrowane indeksy magazynu kolumn* ograniczyć wpływ sieci magazynowania (w górę too10 razy) i zwiększyć wydajność dla raportowania i zapytań analiz. Można używać go z tabel faktów w Twojej toofit składnice danych większej ilości danych w bazie danych i zwiększyć wydajność. Ponadto można jej używać z danych historycznych w Twojej tooarchive operacyjnej bazy danych i być tooquery stanie się too10 razy więcej danych.
- *Klastrowanych indeksów magazynu kolumn* HTAP pomocy można toogain wgląd w czasie rzeczywistym w firmie za pomocą zapytań hello operacyjnej bazy danych bezpośrednio, bez toorun potrzeby hello kosztowne wyodrębniania, transformacji i proces ładowania (ETL) i poczekaj dla hello wypełnione toobe magazynu danych. Klastrowanych indeksów magazynu kolumn Zezwalaj bardzo szybkie wykonywanie zapytania analityczne na powitania bazy danych OLTP, przy jednoczesnym zmniejszeniu hello wpływ na obciążenie operacyjne hello.
- Może także zawierać kombinację hello tabeli zoptymalizowanej pod kątem pamięci z indeksem magazynu kolumn. To połączenie umożliwia tooperform transakcji bardzo szybkie przetwarzanie i zbyt*jednocześnie* wykonywania analizy zapytanie bardzo szybko na powitania takie same dane.

Zarówno indeksy magazynu kolumn i OLTP w pamięci zostały część produktu SQL Server powitania od 2012 i 2014 r. odpowiednio. Azure SQL Database i programu SQL Server hello udostępnianie tego samego implementacją technologii w pamięci. Idąc dalej, nowych funkcji do tych technologii są wydawane w bazie danych SQL Azure, przed wprowadzeniem w programie SQL Server.

W tym temacie opisano aspekty indeksy OLTP w pamięci i magazynu kolumn, które są określone tooAzure bazy danych SQL i przykłady zawiera również:
- Zostanie wyświetlony hello wpływ tych technologii limity rozmiaru magazynu i danych.
- Zobaczysz, jak toomanage hello przenoszenia baz danych używających tych technologii między hello różnym warstwom cenowym.
- Zostanie wyświetlone dwa — przykłady ilustrujące stosowania hello OLTP w pamięci, a także indeksy magazynu kolumn w bazie danych SQL Azure.

Zobacz hello następujące zasoby, aby uzyskać więcej informacji.

Szczegółowe informacje na temat technologii hello:

- [Omówienie OLTP w pamięci i scenariusze użycia](https://msdn.microsoft.com/library/mt774593.aspx) (obejmuje odwołania toocustomer wdrożeń i tooget informacji uruchomiona)
- [Dokumentacja OLTP w pamięci](http://msdn.microsoft.com/library/dn133186.aspx)
- [Przewodnik indeksy magazynu kolumn](https://msdn.microsoft.com/library/gg492088.aspx)
- Hybrydowe transakcyjnej/przetwarzanie analityczne (HTAP), nazywany także [operacyjne analiz w czasie rzeczywistym](https://msdn.microsoft.com/library/dn817827.aspx)

Szybkie Elementarz na OLTP w pamięci: [Szybki Start 1: technologii OLTP w pamięci szybciej T-SQL wydajności](http://msdn.microsoft.com/library/mt694156.aspx) (inny toohelp artykułu Rozpoczynanie pracy)

Szczegółowe wideo na temat technologii hello:

- [OLTP w pamięci w usłudze Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB) (zawierającą pokaz wydajności przynosi korzyści i kroki tooreproduce te wyniki samodzielnie)
- [Wideo OLTP w pamięci: Co to jest i kiedy/jak toouse go](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/03/in-memory-oltp-video-what-it-is-and-whenhow-to-use-it/)
- [Indeks magazynu kolumn: Analiza w pamięci wideo z konferencji Ignite 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/04/columnstore-index-in-memory-analytics-i-e-columnstore-index-videos-from-ignite-2016/)

## <a name="storage-and-data-size"></a>Rozmiar magazynu i danych

### <a name="data-size-and-storage-cap-for-in-memory-oltp"></a>Limit rozmiaru i magazynu danych dla OLTP w pamięci

OLTP w pamięci zawiera tabele zoptymalizowane pod kątem pamięci, które są używane do przechowywania danych użytkownika. Następujące tabele są wymagane toofit w pamięci. Ponieważ zarządzanie pamięci bezpośrednio w hello usługi baza danych SQL, mamy koncepcji hello przydziału dla danych użytkownika. Tę koncepcję jest określony tooas *magazynu OLTP w pamięci*.

Każda baza danych z obsługiwanych autonomiczny warstwa cenowa i każda pula elastyczna warstwa cenowa zawiera pewne magazynu OLTP w pamięci. W czasie hello zapisu otrzymasz gigabajta przestrzeni dyskowej dla każdego 125 jednostki transakcji bazy danych (Dtu) lub elastycznej bazy danych jednostek transakcji (Edtu).

Witaj [warstw usługi SQL Database](sql-database-service-tiers.md) artykuł ma listę oficjalnego hello hello magazynu OLTP w pamięci, która jest dostępna dla poszczególnych obsługiwanych autonomiczna baza danych i warstwy cenowej puli elastycznej.

Witaj następującej liczby elementów kierunku z magazynu OLTP w pamięci, centralnych zasad dostępu:

- Wiersze danych aktywnego użytkownika w tabelach zoptymalizowanych pod kątem pamięci i zmiennych tabel. Należy pamiętać, że stare wersje wiersza nie są wliczane do zakończenia hello.
- Indeksów tabel zoptymalizowanych pod kątem pamięci.
- Nakłady operacyjne operacji ALTER TABLE.

Jeśli naciśniesz zakończenia hello komunikat o błędzie "limit przydziału" i nie jesteś już stanie tooinsert lub aktualizacji danych. toomitigate tego błędu, Usuń dane, lub zwiększ hello cenowym hello bazy danych lub puli.

Aby uzyskać więcej informacji dotyczących monitorowania użycia magazynu OLTP w pamięci i konfigurowania alertów, gdy prawie osiągnęła limit hello, zobacz [Monitor w pamięci magazynu](sql-database-in-memory-oltp-monitoring.md).

#### <a name="about-elastic-pools"></a>Temat pul elastycznych

Używając puli elastycznej hello magazynu OLTP w pamięci jest współużytkowana przez wszystkie bazy danych w puli hello. W związku z tym użycia hello w jednej bazie danych może wpłynąć na innych baz danych. Są dwa środki zaradcze dla tego:

- Skonfiguruj Max-liczbę jednostek eDTU dla baz danych jest niższa niż liczba jednostek eDTU hello hello pulę jako całość. Maksymalna caps hello wykorzystanie magazynu OLTP w pamięci, w dowolnej bazy danych w puli hello, rozmiar toohello, który odpowiada toohello liczby jednostek eDTU.
- Skonfiguruj Min-eDTU, która jest większa niż 0. Tego minimalna gwarancji, że każda baza danych w puli hello ma hello ilość dostępnego magazynu OLTP w pamięci, która odpowiada toohello skonfigurowany Min eDTU.

### <a name="data-size-and-storage-for-columnstore-indexes"></a>Rozmiar danych i magazynu dla indeksów magazynu kolumn

Indeksy magazynu kolumn nie są wymagane toofit w pamięci. W związku z tym hello tylko limit na rozmiar hello indeksów hello jest hello maksymalny ogólny rozmiar bazy danych, które opisano w hello [warstw usługi SQL Database](sql-database-service-tiers.md) artykułu.

Gdy używasz klastrowane indeksy magazynu kolumn, kolumnowy kompresji jest używane do przechowywania tabeli podstawowej hello. Kompresja ta może znacznie zmniejszyć rozmiaru magazynu hello dane użytkowników, co oznacza, że można umieścić więcej danych w bazie danych hello. I kompresji hello można go zwiększyć z [kolumnowy kompresji archiwizacji](https://msdn.microsoft.com/library/cc280449.aspx#Using Columnstore and Columnstore Archive Compression). Hello kompresji, które pozwalają osiągnąć zależy od charakteru hello hello danych, ale 10 razy hello kompresji nie jest nietypowa sytuacja.

Na przykład jeśli baza danych o maksymalnym rozmiarze 1 terabajtów (TB) i osiągnąć kompresji hello 10 razy przy użyciu indeksów magazynu kolumn, można umieścić łącznie 10 TB danych użytkownika w bazie danych hello.

Gdy używasz klastrowanych indeksów magazynu kolumn tabeli podstawowej hello jest nadal przechowywane w formacie tradycyjnego magazynu wierszy hello. W związku z tym hello oszczędności pojemności magazynu nie są big z klastrowane indeksy magazynu kolumn. Jednak jeśli liczba indeksów nieklastrowanych tradycyjnych z indeksem magazynu kolumn w jednym, również widzieć ogólną oszczędności rozmiaru magazynu hello hello tabeli.

## <a name="moving-databases-that-use-in-memory-technologies-between-pricing-tiers"></a>Przenoszenie baz danych korzystających z technologii w pamięci między warstw cenowych

Brak Nigdy nie wszelkie niezgodności lub innych problemów po uaktualnieniu tooa wyższe cenowym, takich jak z tooPremium standardowa. Funkcje dostępne Hello i zasoby tylko zwiększyć.

Ale starszą wersję hello warstwy cenowej może niekorzystnie wpłynąć na bazie danych. wpływ Hello jest szczególnie widoczne, gdy obniżyć z Premium tooStandard lub podstawowa, gdy baza danych zawiera obiekty OLTP w pamięci. Tabele zoptymalizowane pod kątem pamięci i indeksy magazynu kolumn są niedostępne po obniżenia poziomu hello (nawet jeśli są one widoczne). powitalne te same kwestie należy w przypadku obniżenia hello cenowym puli elastycznej lub przenoszenia bazy danych z technologiami w pamięci w standardowej lub podstawowa puli elastycznej.

### <a name="in-memory-oltp"></a>Przetwarzanie OLTP w pamięci

*Zmiana wersji na starszą tooBasic/Standard*: OLTP w pamięci nie jest obsługiwane w bazach danych w hello warstwy standardowa lub Basic. Ponadto nie jest możliwe toomove bazy danych zawierającej wszystkie OLTP w pamięci obiektów toohello warstwy standardowa lub Basic.

Przed obniżyć hello bazy danych tooStandard/Basic, Usuń wszystkie tabele zoptymalizowane pod kątem pamięci i typy tabel, a także wszystkich modułów skompilowanych w sposób macierzysty T-SQL.

Brak toounderstand sposób programowy czy danego bazy danych obsługuje OLTP w pamięci. Możesz wykonać hello następującego zapytania języka Transact-SQL:

```
SELECT DatabasePropertyEx(DB_NAME(), 'IsXTPSupported');
```

Jeśli hello zapytanie zwraca **1**, OLTP w pamięci jest obsługiwana w tej bazie danych.


*Zmiana wersji na starszą dolnej warstwy Premium tooa*: dane w tabelach zoptymalizowanych pod kątem pamięci musi mieścić się w hello magazynu OLTP w pamięci, który jest skojarzony z hello cenowym hello bazy danych lub w puli elastycznej hello jest dostępny. Spróbuj hello toolower warstwy cenowej lub przenieść bazę danych hello w puli, który nie ma za mało dostępnej pamięci OLTP w pamięci, operacja hello kończy się niepowodzeniem.

### <a name="columnstore-indexes"></a>Indeksy magazynu kolumn

*Zmiana wersji na starszą tooBasic lub Standard*: warstwy standardowa lub Basic hello indeksy są obsługiwane tylko dla warstwy cenowej Premium hello, a nie w systemie magazynu kolumn. Można obniżyć z tooStandard bazy danych lub Basic, indeksu magazynu kolumn staje się niedostępna. Hello system obsługuje indeksu magazynu kolumn, ale nigdy nie wykorzystuje hello indeksu. Uaktualnienie później wstecz tooPremium indeksu magazynu kolumn jest od razu gotowy toobe ponownie wykorzystać.

Jeśli masz **klastrowanych** indeksu magazynu kolumn po obniżania poziomu niedostępny hello całej tabeli. Dlatego zaleca się usunąć wszystkich *klastrowanych* indeksy magazynu kolumn przed obniżyć poniżej warstwy Premium hello bazy danych.

*Zmiana wersji na starszą dolnej warstwy Premium tooa*: ten obniżenia poziomu zakończy się pomyślnie, jeśli hello całej bazy danych mieści się w hello maksymalny rozmiar bazy danych dla obiektu docelowego hello warstwy cenowej lub do dostępnego magazynu hello w puli elastycznej hello. Nie ma żadnego określonego wpływu z hello indeksy magazynu kolumn.


<a id="install_oltp_manuallink" name="install_oltp_manuallink"></a>

&nbsp;

## <a name="1-install-hello-in-memory-oltp-sample"></a>1. Zainstaluj hello próbki OLTP w pamięci

Witaj AdventureWorksLT przykładowej bazy danych można utworzyć za pomocą kilku kliknięć w hello [portalu Azure](https://portal.azure.com/). Następnie hello w tej sekcji opisano sposób można wzbogacić bazy danych AdventureWorksLT z obiektami OLTP w pamięci i Wykaż zwiększenia wydajności.

Aby uzyskać więcej simplistic, ale atrakcyjność wizualną demonstrację wydajności OLTP w pamięci Zobacz:

- Wersja: [w pamięci — oltp pokaz-wersja 1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)
- Kod źródłowy: [in-memory-oltp-demo-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/in-memory/ticket-reservations)

#### <a name="installation-steps"></a>Kroki instalacji

1. W hello [portalu Azure](https://portal.azure.com/), utworzyć bazy danych Premium na serwerze. Zestaw hello **źródła** toohello AdventureWorksLT przykładowej bazy danych. Aby uzyskać szczegółowe instrukcje, zobacz [utworzyć pierwszą bazę danych Azure SQL](sql-database-get-started-portal.md).

2. Uzyskuj toohello bazy danych programu SQL Server Management Studio [(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx).

3. Kopiuj hello [skryptu OLTP w pamięci języka Transact-SQL](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_oltp_sample.sql) tooyour Schowka. Witaj skryptu T-SQL tworzy hello obiekty niezbędne w pamięci w hello AdventureWorksLT przykładową bazę danych utworzoną w kroku 1.

4. Wklej hello skryptu T-SQL w programie SSMS, a następnie uruchom skrypt hello. Witaj `MEMORY_OPTIMIZED = ON` instrukcji CREATE TABLE klauzuli są niezwykle istotne. Na przykład:


```
CREATE TABLE [SalesLT].[SalesOrderHeader_inmem](
    [SalesOrderID] int IDENTITY NOT NULL PRIMARY KEY NONCLUSTERED ...,
    ...
) WITH (MEMORY_OPTIMIZED = ON);
```


#### <a name="error-40536"></a>Błąd 40536


Jeśli zostanie wyświetlony błąd 40536 po uruchomieniu skryptu hello T-SQL, uruchom powitania po tooverify skryptu T-SQL, czy w pamięci obsługuje hello bazy danych:


```
SELECT DatabasePropertyEx(DB_Name(), 'IsXTPSupported');
```


W wyniku **0** oznacza, że w pamięci nie jest obsługiwany, i **1** oznacza, że jest obsługiwana. toodiagnose hello problem, upewnij się, że hello baza danych jest w warstwie usług Premium hello.


#### <a name="about-hello-created-memory-optimized-items"></a>O hello utworzone elementy zoptymalizowanych pod kątem pamięci

**Tabele**: hello przykład zawiera następujące tabele zoptymalizowane pod kątem pamięci hello:

- SalesLT.Product_inmem
- SalesLT.SalesOrderHeader_inmem
- SalesLT.SalesOrderDetail_inmem
- Demo.DemoSalesOrderHeaderSeed
- Demo.DemoSalesOrderDetailSeed


Możesz sprawdzić tabel zoptymalizowanych pod kątem pamięci przy użyciu hello **Eksplorator obiektów** w programie SSMS. Kliknij prawym przyciskiem myszy **tabel** > **filtru** > **ustawienia filtrowania** > **jest zoptymalizowana pod kątem pamięci**. Witaj, wartość jest równa 1.


Lub możesz zbadać hello widokach katalogów, takich jak:


```
SELECT is_memory_optimized, name, type_desc, durability_desc
    FROM sys.tables
    WHERE is_memory_optimized = 1;
```


**Procedura składowana skompilowanych w sposób macierzysty**: SalesLT.usp_InsertSalesOrder_inmem można sprawdzić za pomocą widoku wykazu kwerendy:


```
SELECT uses_native_compilation, OBJECT_NAME(object_id), definition
    FROM sys.sql_modules
    WHERE uses_native_compilation = 1;
```


&nbsp;

### <a name="run-hello-sample-oltp-workload"></a>Uruchom hello przykładowe obciążenie OLTP

Witaj jedyna różnica między hello następujące dwa *procedur składowanych* hello Pierwsza procedura używa wersji hello tabel zoptymalizowanych pod kątem pamięci, podczas hello Druga procedura używa hello zwykłych tabelach na dysku:

- SalesLT**.** usp_InsertSalesOrder**_inmem**
- SalesLT**.** usp_InsertSalesOrder**_ondisk**


W tej sekcji, zobaczysz, jak toouse hello przydatną **ostress.exe** tooexecute narzędzie Witaj dwie procedury przechowywanej na poziomach stressful. Możesz porównać, jak długo toofinish uruchamia akcent hello dwa.


Po uruchomieniu ostress.exe zaleca się, że przekazujesz przeznaczony dla obu hello następujące wartości parametrów:

- Uruchamianie dużej liczby równoczesnych połączeń przy użyciu - n100.
- Ma przy każdej pętli połączenia setki razy, za pomocą parametru-r500.


Jednak może być toostart wartościami znacznie mniejszy, takich jak - n10 i - r50 tooensure, czy wszystko działa.


### <a name="script-for-ostressexe"></a>Skrypt dla ostress.exe


Ta sekcja wyświetla hello skryptu T-SQL, osadzonego w naszym ostress.exe wiersza polecenia. skrypt Hello używa elementów, które zostały utworzone przez hello skryptu T-SQL, który został wcześniej zainstalowany.


Hello poniższy skrypt wstawia przykładowe zamówienia sprzedaży z pięciu pozycji do następujących hello zoptymalizowanych pod kątem pamięci *tabel*:

- SalesLT.SalesOrderHeader_inmem
- SalesLT.SalesOrderDetail_inmem


```
DECLARE
    @i int = 0,
    @od SalesLT.SalesOrderDetailType_inmem,
    @SalesOrderID int,
    @DueDate datetime2 = sysdatetime(),
    @CustomerID int = rand() * 8000,
    @BillToAddressID int = rand() * 10000,
    @ShipToAddressID int = rand() * 10000;

INSERT INTO @od
    SELECT OrderQty, ProductID
    FROM Demo.DemoSalesOrderDetailSeed
    WHERE OrderID= cast((rand()*60) as int);

WHILE (@i < 20)
begin;
    EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT,
        @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od;
    SET @i = @i + 1;
end
```


Witaj toomake *_ondisk* wersji hello ostress.exe poprzedniego skryptu T-SQL, należy zastąpić zarówno wystąpień hello *_inmem* podciąg z *_ondisk*. Te elementy zastępcze wpływa na powitania nazwy tabel i procedur składowanych.


### <a name="install-rml-utilities-and-ostress"></a>Zainstaluj narzędzia RML i ostress


W idealnym przypadku będzie zaplanować toorun ostress.exe na maszynie wirtualnej platformy Azure (VM). Należy utworzyć [maszyny Wirtualnej Azure](https://azure.microsoft.com/documentation/services/virtual-machines/) w hello tego samego Azure region geograficzny, w którym znajduje się baza danych AdventureWorksLT. Ale może uruchamiać ostress.exe na laptopie zamiast tego.


Hello maszyny Wirtualnej lub niezależnie od hosta, możesz wybrać, zainstaluj narzędzia powtarzania Markup Language (RML) hello. programy narzędziowe Hello ostress.exe.

Aby uzyskać więcej informacji, zobacz:
- Witaj dyskusji ostress.exe [przykładowej bazy danych OLTP w pamięci](http://msdn.microsoft.com/library/mt465764.aspx).
- [Przykładowe bazy danych do OLTP w pamięci](http://msdn.microsoft.com/library/mt465764.aspx).
- Witaj [blogu instalowania ostress.exe](http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx).



<!--
dn511655.aspx is for SQL 2014,
[Extensions tooAdventureWorks tooDemonstrate In-Memory OLTP]
(http://msdn.microsoft.com/library/dn511655&#x28;v=sql.120&#x29;.aspx)

whereas for SQL 2016+
[Sample Database for In-Memory OLTP]
(http://msdn.microsoft.com/library/mt465764.aspx)
-->



### <a name="run-hello-inmem-stress-workload-first"></a>Uruchom hello *_inmem* najpierw podkreślają obciążenia


Można użyć *RML Cmd monitu* toorun okno wiersza polecenia naszych ostress.exe. Parametry wiersza polecenia Hello bezpośrednie ostress do:

- Równoczesne uruchamianie połączenia o szybkości 100 (-n100).
- Każdy połączenia uruchomienia skryptu T-SQL hello 50 razy (-r50).


```
ostress.exe -n100 -r50 -S<servername>.database.windows.net -U<login> -P<password> -d<database> -q -Q"DECLARE @i int = 0, @od SalesLT.SalesOrderDetailType_inmem, @SalesOrderID int, @DueDate datetime2 = sysdatetime(), @CustomerID int = rand() * 8000, @BillToAddressID int = rand() * 10000, @ShipToAddressID int = rand()* 10000; INSERT INTO @od SELECT OrderQty, ProductID FROM Demo.DemoSalesOrderDetailSeed WHERE OrderID= cast((rand()*60) as int); WHILE (@i < 20) begin; EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od; set @i += 1; end"
```


Witaj toorun poprzedzających ostress.exe wiersza polecenia:


1. Resetuj zawartości danych bazy danych hello, uruchamiając następujące polecenie w programie SSMS, toodelete hello wszystkie dane hello został wstawiony przez wszystkie poprzednie działa:

    ``` tsql
    EXECUTE Demo.usp_DemoReset;
    ```

2. Skopiuj tekst hello hello poprzedzających ostress.exe wiersza polecenia tooyour Schowka.

3. Zastąp hello `<placeholders>` hello parametrów -S - U -P - d z hello Popraw wartości rzeczywistych.

4. Edytowany linii polecenia są uruchamiane w oknie RML Cmd.


#### <a name="result-is-a-duration"></a>Wynik jest czas trwania


Po zakończeniu pracy ostress.exe zapisuje hello czas trwania jako jego końcowego wiersza danych wyjściowych w oknie RML Cmd hello. Na przykład krótszą uruchomienia testu trwała około 1,5 minuty:

`11/12/15 00:35:00.873 [0x000030A8] OSTRESS exiting normally, elapsed time: 00:01:31.867`


#### <a name="reset-edit-for-ondisk-then-rerun"></a>Resetuj, edytowanie *_ondisk*, uruchom ponownie


Po uzyskaniu wyniku hello hello *_inmem* uruchomić, wykonaj następujące kroki dla hello hello *_ondisk* Uruchom:


1. Resetowanie hello bazy danych, uruchamiając następujące polecenie w programie SSMS toodelete hello wszystkie dane hello wstawione przez hello poprzedniego uruchomienia:
```
EXECUTE Demo.usp_DemoReset;
```

2. Edytuj hello ostress.exe wiersza polecenia tooreplace wszystkie *_inmem* z *_ondisk*.

3. Uruchom ponownie ostress.exe na powitania po raz drugi i przechwytywania hello czas trwania wynik.

4. Ponownie resetowania hello bazy danych (w przypadku usuwania odpowiedzialne, które mogą być duże ilości danych testowych).


#### <a name="expected-comparison-results"></a>Porównanie oczekiwanego wyników

Nasze testy w pamięci wykazały, że wydajność poprawia **dziewięciokrotnie** dla tego simplistic obciążenia z ostress uruchomione na maszynie Wirtualnej platformy Azure w hello sam region platformy Azure jako hello bazy danych.

<a id="install_analytics_manuallink" name="install_analytics_manuallink"></a>

&nbsp;

## <a name="2-install-hello-in-memory-analytics-sample"></a>2. Zainstaluj hello próbki analityka w pamięci


W tej sekcji można porównywać hello We/Wy i wyniki statystyk podczas korzystania z indeksu magazynu kolumn lub indeksu b drzewa tradycyjnych.


Analiz w czasie rzeczywistym na obciążenia OLTP jest często najlepszym toouse nieklastrowany indeks magazynu kolumn. Aby uzyskać więcej informacji, zobacz [opisane indeksy magazynu kolumn](http://msdn.microsoft.com/library/gg492088.aspx).



### <a name="prepare-hello-columnstore-analytics-test"></a>Przygotowanie hello magazynu kolumn analytics testu


1. Użyj hello Azure toocreate portalu nową bazę danych AdventureWorksLT z hello próbki.
 - Użyj takiej samej nazwie.
 - Wybierz wszystkie warstwy usług Premium.

2. Kopiuj hello [sql_in memory_analytics_sample](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_analytics_sample.sql) tooyour Schowka.
 - Witaj skryptu T-SQL tworzy hello obiekty niezbędne w pamięci w hello AdventureWorksLT przykładową bazę danych utworzoną w kroku 1.
 - Witaj skrypt tworzy hello tabeli wymiarów i tabel faktów. tabele faktów Hello są wypełniane przy użyciu 3.5 milion wierszy.
 - skrypt Hello może potrwać toocomplete 15 minut.

3. Wklej hello skryptu T-SQL w programie SSMS, a następnie uruchom skrypt hello. Witaj **magazynu kolumn** — słowo kluczowe w hello **CREATE INDEX** instrukcja jest niezwykle ważny, jak w programie:<br/>`CREATE NONCLUSTERED COLUMNSTORE INDEX ...;`

4. Ustaw poziom toocompatibility AdventureWorksLT 130:<br/>`ALTER DATABASE AdventureworksLT SET compatibility_level = 130;`

    Poziom 130 nie jest z nią bezpośrednio powiązane pamięci tooIn funkcji. Jednak poziom 130 zwykle zapewnia lepszą wydajność zapytań, niż 120.


#### <a name="key-tables-and-columnstore-indexes"></a>Tabele klucza i indeksy magazynu kolumn


- dbo. Tabela mająca klastrowany indeks magazynu kolumn, który udostępnia zaawansowane kompresji w hello jest FactResellerSalesXL_CCI *danych* poziom.

- dbo. Tabela mająca równoważne regularne indeks klastrowany, które są kompresowane tylko w hello jest FactResellerSalesXL_PageCompressed *strony* poziom.


#### <a name="key-queries-toocompare-hello-columnstore-index"></a>Indeks magazynu kolumn hello toocompare klucza zapytania


Brak [kilka typów zapytania T-SQL, które można uruchomić](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/clustered_columnstore_sample_queries.sql) toosee ulepszenia wydajności. W kroku 2 hello skryptu T-SQL należy zwrócić uwagę toothis pary zapytań. Różnią się tylko w jednym wierszu:


- `FROM FactResellerSalesXL_PageCompressed a`
- `FROM FactResellerSalesXL_CCI a`


Klastrowany indeks magazynu kolumn jest hello FactResellerSalesXL\_WIK tabeli.

Hello poniższy fragment skryptu T-SQL wyświetla statystyki dla We/Wy i godziny dla zapytania hello każdej tabeli.


```
/*********************************************************************
Step 2 -- Overview
-- Page Compressed BTree table v/s Columnstore table performance differences
-- Enable actual Query Plan in order toosee Plan differences when Executing
*/
-- Ensure Database is in 130 compatibility mode
ALTER DATABASE AdventureworksLT SET compatibility_level = 130
GO

-- Execute a typical query that joins hello Fact Table with dimension tables
-- Note this query will run on hello Page Compressed table, Note down hello time
SET STATISTICS IO ON
SET STATISTICS TIME ON
GO

SELECT c.Year
    ,e.ProductCategoryKey
    ,FirstName + ' ' + LastName AS FullName
    ,count(SalesOrderNumber) AS NumSales
    ,sum(SalesAmount) AS TotalSalesAmt
    ,Avg(SalesAmount) AS AvgSalesAmt
    ,count(DISTINCT SalesOrderNumber) AS NumOrders
    ,count(DISTINCT a.CustomerKey) AS CountCustomers
FROM FactResellerSalesXL_PageCompressed a
INNER JOIN DimProduct b ON b.ProductKey = a.ProductKey
INNER JOIN DimCustomer d ON d.CustomerKey = a.CustomerKey
Inner JOIN DimProductSubCategory e on e.ProductSubcategoryKey = b.ProductSubcategoryKey
INNER JOIN DimDate c ON c.DateKey = a.OrderDateKey
GROUP BY e.ProductCategoryKey,c.Year,d.CustomerKey,d.FirstName,d.LastName
GO
SET STATISTICS IO OFF
SET STATISTICS TIME OFF
GO


-- This is hello same Prior query on a table with a clustered columnstore index CCI
-- hello comparison numbers are even more dramatic hello larger hello table is (this is an 11 million row table only)
SET STATISTICS IO ON
SET STATISTICS TIME ON
GO
SELECT c.Year
    ,e.ProductCategoryKey
    ,FirstName + ' ' + LastName AS FullName
    ,count(SalesOrderNumber) AS NumSales
    ,sum(SalesAmount) AS TotalSalesAmt
    ,Avg(SalesAmount) AS AvgSalesAmt
    ,count(DISTINCT SalesOrderNumber) AS NumOrders
    ,count(DISTINCT a.CustomerKey) AS CountCustomers
FROM FactResellerSalesXL_CCI a
INNER JOIN DimProduct b ON b.ProductKey = a.ProductKey
INNER JOIN DimCustomer d ON d.CustomerKey = a.CustomerKey
Inner JOIN DimProductSubCategory e on e.ProductSubcategoryKey = b.ProductSubcategoryKey
INNER JOIN DimDate c ON c.DateKey = a.OrderDateKey
GROUP BY e.ProductCategoryKey,c.Year,d.CustomerKey,d.FirstName,d.LastName
GO

SET STATISTICS IO OFF
SET STATISTICS TIME OFF
GO
```

W bazie danych z warstwy cenowej P2 hello może spodziewać się bardziej wydajne hello około dziewięciokrotnie dla tego zapytania przy użyciu hello klastrowany indeks magazynu kolumn w porównaniu z hello tradycyjnych indeksu. Z P15 z replikacją może spodziewać się bardziej wydajne hello około 57 razy przy użyciu hello indeksu magazynu kolumn.



## <a name="next-steps"></a>Następne kroki

- [Szybki Start 1: Technologii OLTP w pamięci, aby zwiększyć wydajność T-SQL](http://msdn.microsoft.com/library/mt694156.aspx)

- [Użyj OLTP w pamięci w istniejącej aplikacji usługi Azure SQL](sql-database-in-memory-oltp-migration.md)

- [Monitor OLTP w pamięci magazynu](sql-database-in-memory-oltp-monitoring.md) dla OLTP w pamięci


## <a name="additional-resources"></a>Dodatkowe zasoby

#### <a name="deeper-information"></a>Więcej informacji

- [Dowiedz się, jak kworum podwaja obciążenia klucza bazy danych podczas opuszczania jednostek dtu w warstwie 70% z OLTP w pamięci w bazie danych SQL](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)

- [OLTP w pamięci w bazie danych Azure SQL wpis w blogu](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)

- [Dowiedz się więcej o OLTP w pamięci](http://msdn.microsoft.com/library/dn133186.aspx)

- [Dowiedz się więcej o indeksy magazynu kolumn](https://msdn.microsoft.com/library/gg492088.aspx)

- [Dowiedz się więcej o operacyjne analiz w czasie rzeczywistym](http://msdn.microsoft.com/library/dn817827.aspx)

- Zobacz [typowe wzorce obciążeń i zagadnienia dotyczące migracji](http://msdn.microsoft.com/library/dn673538.aspx) (w którym opisano wzorców obciążenia, gdzie OLTP w pamięci zapewnia często znaczący wzrost wydajności)

#### <a name="application-design"></a>Aplikacja — projekt

- [(Optymalizacja w pamięci) OLTP w pamięci](http://msdn.microsoft.com/library/dn133186.aspx)

- [Użyj OLTP w pamięci w istniejącej aplikacji usługi Azure SQL](sql-database-in-memory-oltp-migration.md)

#### <a name="tools"></a>Narzędzia

- [Witryna Azure Portal](https://portal.azure.com/)

- [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx)

- [SQL Server Data Tools (SSDT)](http://msdn.microsoft.com/library/mt204009.aspx)
