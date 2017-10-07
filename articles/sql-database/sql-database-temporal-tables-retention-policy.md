---
title: dane historyczne aaaManage w tabelach danych czasowych z zasadami przechowywania | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toouse przechowywania danych tymczasowych zasad tookeep danych historycznych pod kontrolą."
services: sql-database
documentationcenter: 
author: bonova
manager: drasumic
editor: 
ms.assetid: 76cfa06a-e758-453e-942c-9f1ed6a38c2a
ms.service: sql-database
ms.custom: develop databases
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: sql-database
ms.date: 10/12/2016
ms.author: bonova
ms.openlocfilehash: a72a6111a6cd7322d734d08bf3852e95f5ffea8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-historical-data-in-temporal-tables-with-retention-policy"></a>Zarządzanie danych historycznych w tabelach danych czasowych z zasady przechowywania
Tabele danych czasowych może zwiększyć baz danych o rozmiarze ponad zwykłych tabelach, zwłaszcza jeśli przechowywanie danych historycznych przez dłuższy okres. W związku z tym zasady przechowywania danych historycznych jest istotnym elementem planowania i zarządzanie cyklem życia hello każdej tabeli danych czasowych. Tabele danych czasowych w bazie danych SQL Azure pochodzą z mechanizmem przechowywania łatwy w użyciu, który ułatwia wykonywanie tego zadania.

Przechowywania historii danych czasowych można skonfigurować na poziomie pojedynczej tabeli hello, dzięki czemu użytkownicy, który toocreate przedawnienia elastyczne zasady. Stosowanie przechowywania danych czasowych jest prosty: wymaga tylko jednego toobe parametru ustawiona podczas zmiany schematu lub tworzenia tabeli.

Po zdefiniowaniu zasad przechowywania bazy danych SQL Azure rozpoczyna regularnie sprawdzanie, czy istnieją historyczne wierszy, które kwalifikują się do czyszczenia danych. Identyfikacja zgodnych wierszy i ich usunięcia z tabeli historii hello występować w sposób niewidoczny dla użytkownika, w zadania w tle hello zaplanowane i uruchamiane przez hello system. Warunek wieku wiersze tabeli historii hello jest sprawdzany zależności w kolumnie hello reprezentujący koniec okresu SYSTEM_TIME. Jeśli okres przechowywania, na przykład ustawiono toosix miesiące, kwalifikuje się do oczyszczania wiersze tabeli spełniają hello następującego warunku:

````
ValidTo < DATEADD (MONTH, -6, SYSUTCDATETIME())
````

W hello poprzedzających przykład, możemy przyjąć, że **ValidTo** kolumna odpowiada toohello koniec okresu SYSTEM_TIME.

## <a name="how-tooconfigure-retention-policy"></a>Jak tooconfigure zasady przechowywania?
Przed skonfigurowaniem zasad przechowywania dla tabeli danych czasowych należy sprawdzić w pierwszej kolejności czy włączone jest przechowywanie historycznych danych czasowych *na poziomie bazy danych hello*.

````
SELECT is_temporal_history_retention_enabled, name
FROM sys.databases
````

Baza danych flagi **is_temporal_history_retention_enabled** jest zestaw tooON domyślnie, ale użytkownicy można go zmienić za pomocą instrukcji ALTER DATABASE. Jest również automatycznie tooOFF zestaw po [punktu w czasie przywracania](sql-database-recovery-using-backups.md) operacji. Oczyszczanie przechowywania historii danych czasowych tooenable dla bazy danych, wykonaj hello następującej instrukcji:

````
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
````

> [!IMPORTANT]
> Możesz skonfigurować czas przechowywania w przypadku tabel czasowych, nawet jeśli **is_temporal_history_retention_enabled** jest wyłączona, ale automatycznego oczyszczania przestarzałych wierszy jest nie są uruchamiane w takiej sytuacji.
> 
> 

Zasady przechowywania jest skonfigurowane podczas tworzenia tabeli, określając wartość parametru HISTORY_RETENTION_PERIOD hello:

````
CREATE TABLE dbo.WebsiteUserInfo
(  
    [UserID] int NOT NULL PRIMARY KEY CLUSTERED
  , [UserName] nvarchar(100) NOT NULL
  , [PagesVisited] int NOT NULL
  , [ValidFrom] datetime2 (0) GENERATED ALWAYS AS ROW START
  , [ValidTo] datetime2 (0) GENERATED ALWAYS AS ROW END
  , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)
 )  
 WITH
 (
     SYSTEM_VERSIONING = ON
     (
        HISTORY_TABLE = dbo.WebsiteUserInfoHistory,
        HISTORY_RETENTION_PERIOD = 6 MONTHS
     )
 );
````

Bazy danych SQL Azure umożliwia przechowywanie toospecify przy użyciu różne jednostki: dni, tygodnie, MIESIĄCE i lata. W przypadku pominięcia HISTORY_RETENTION_PERIOD przyjęto NIESKOŃCZONE przechowywania. Umożliwia także NIESKOŃCZONE — słowo kluczowe jawnie.

W niektórych scenariuszach może być tooconfigure przechowywania po utworzeniu tabeli lub toochange wcześniej skonfigurowane wartości. W takim przypadku należy użyć instrukcji ALTER TABLE:

````
ALTER TABLE dbo.WebsiteUserInfo
SET (SYSTEM_VERSIONING = ON (HISTORY_RETENTION_PERIOD = 9 MONTHS));
````

> [!IMPORTANT]
> Ustawienie SYSTEM_VERSIONING tooOFF *nie zachowa* wartość okresu przechowywania. Ustawienie tooON SYSTEM_VERSIONING bez HISTORY_RETENTION_PERIOD określone jawnie wyniki w hello NIEOGRANICZONY okres przechowywania.
> 
> 

tooreview bieżący stan hello zasady przechowywania, użyj następujących hello kwerendy tę flagę aktywacji przechowywania danych czasowych sprzężenia na poziomie bazy danych hello z okresów przechowywania dla poszczególnych tabel:

````
SELECT DB.is_temporal_history_retention_enabled,
SCHEMA_NAME(T1.schema_id) AS TemporalTableSchema,
T1.name as TemporalTableName,  SCHEMA_NAME(T2.schema_id) AS HistoryTableSchema,
T2.name as HistoryTableName,T1.history_retention_period,
T1.history_retention_period_unit_desc
FROM sys.tables T1  
OUTER APPLY (select is_temporal_history_retention_enabled from sys.databases
where name = DB_NAME()) AS DB
LEFT JOIN sys.tables T2   
ON T1.history_table_id = T2.object_id WHERE T1.temporal_type = 2
````


## <a name="how-sql-database-deletes-aged-rows"></a>Jak baza danych SQL usuwa przestarzałe wierszy?
procesu oczyszczania Hello zależy od hello układ indeksu tabeli historii hello. Jest ważne toonotice który *tylko do tabel historii z indeksem klastrowanym, (B-drzewa lub magazynu kolumn) może mieć skonfigurowanych zasad przechowywania skończoną*. Zadanie w tle jest tworzony tooperform oczyszczania przestarzałych danych dla wszystkich tabel danych czasowych z okresu przechowywania ograniczone.
Oczyścić logikę klastrowanego indeksu magazynu wierszy (B-drzewa) hello usuwa wiersz przestarzałe w mniejsze fragmenty (up too10K) minimalizując nacisk na dziennika bazy danych i podsystem We/Wy. Mimo że używa logiki oczyszczania wymagane indeksu B-drzewa, kolejność usunięcia wierszy hello starsze niż okres przechowywania nie może zagwarantować mocno. W związku z tym *nie przyjmują wszelkie zależności na powitania oczyszczania kolejności w aplikacjach*.

Witaj zadanie oczyszczania dla hello klastrowanego magazynu kolumn spowoduje usunięcie całego [wiersz grup](https://msdn.microsoft.com/library/gg492088.aspx) jednocześnie (zwykle zawierają 1 milion wierszy każdego), który jest bardzo wydajny, szczególnie w przypadku, gdy dane historyczne zostanie wygenerowany w szybkim tempie.

![Przechowywania klastrowanego magazynu kolumn](./media/sql-database-temporal-tables-retention-policy/cciretention.png)

Kompresji danych doskonała i wydajne przechowywania oczyszczania sprawia, że klastrowany indeks magazynu kolumn doskonałym rozwiązaniem dla scenariuszy jeśli obciążenie generuje szybko dużej ilości danych historycznych. Ten wzorzec jest typowa dla intensywnego [obciążenia przetwarzania transakcyjnego, które tabele danych czasowych](https://msdn.microsoft.com/library/mt631669.aspx) śledzenie zmian i inspekcji, analiza trendu lub wprowadzanie danych IoT.

## <a name="index-considerations"></a>Zagadnienia dotyczące indeksu
Zadanie oczyszczania Hello tabel klastrowanego indeksu magazynu wierszy wymaga toostart indeksu z hello kolumny odpowiedniego hello końca okresu SYSTEM_TIME. Jeśli takie indeks nie istnieje, nie można skonfigurować okres przechowywania ograniczone:

*Msg 13765, poziom 16, stan 1 <br> </br> ustawienie okresu przechowywania ograniczone nie można w tabeli danych czasowych z systemową kontrolą wersji "temporalstagetestdb.dbo.WebsiteUserInfo", ponieważ tabela historii hello " temporalstagetestdb.dbo.WebsiteUserInfoHistory "nie zawiera wymaganego indeksu klastrowanego. Należy rozważyć utworzenie klastrowanego magazynu kolumn lub indeksu B-drzewa, począwszy od hello kolumny, która odpowiada koniec SYSTEM_TIME period w tabeli historii hello.*

Jest ważne toonotice, który hello tabeli historii domyślny utworzony przez bazę danych SQL Azure już ma klastrowany indeks, który jest zgodny z zasady przechowywania. Jeśli spróbujesz tooremove tego indeksu dla tabeli z okresu przechowywania ograniczone, operacja nie powiedzie się z hello następujący błąd:

*Msg 13766, poziom 16, stan 1 <br> </br> nie można porzucić indeksu klastrowanego hello "WebsiteUserInfoHistory.IX_WebsiteUserInfoHistory", ponieważ jest on używany do automatycznego usuwania przestarzałych danych. Jeśli potrzebujesz toodrop tego indeksu, należy wziąć pod uwagę tooINFINITE HISTORY_RETENTION_PERIOD ustawienie na powitania odpowiedniej tabeli danych czasowych systemową kontrolą wersji.*

Oczyszczanie na powitania klastrowany indeks magazynu kolumn działa optymalnie, jeśli umieszczanych historycznych wierszy w kolejności rosnącej (uporządkowane według hello koniec okresu kolumny), co jest zawsze hello sytuacją, gdy tabela historii hello jest wypełniana wyłącznie hello SYSTEM_ hello Mechanizm VERSIONIOING. Wiersze w tabeli historii hello nie są uporządkowane według koniec kolumnie okresu (które mogą być przypadku powitania po migracji istniejących danych historycznych), należy ponownie utworzyć klastrowanego indeksu magazynu kolumn na górze indeksu magazynu wierszy B-drzewa, który jest poprawnie określona, tooachieve optymalną wydajność.

Należy unikać odbudowywania klastrowany indeks magazynu kolumn w tabeli historii hello hello okres przechowywania ograniczone, ponieważ mogą ulec zmianie, kolejność w naturalnie narzucone przez operację system-versioning hello grupy wierszy hello. Jeśli potrzebujesz toorebuild klastrowany indeks magazynu kolumn w tabeli historii hello zrobić, ponowne utworzenie u góry zgodne indeksu B-drzewa, zachowując kolejnością rowgroups hello niezbędne oczyszczania regularnych danych. Witaj, które same podejście należy podjąć w przypadku utworzenia tabeli danych czasowych z istniejącą tabelę historii, która ma klastrowany indeks kolumny bez kolejność gwarantowane danych:

````
/*Create B-tree ordered by hello end of period column*/
CREATE CLUSTERED INDEX IX_WebsiteUserInfoHistory ON WebsiteUserInfoHistory (ValidTo)
WITH (DROP_EXISTING = ON);
GO
/*Re-create clustered columnstore index*/
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory ON WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON);
````

Po skonfigurowaniu ograniczone przechowywanie hello tabeli historii z hello klastrowany indeks magazynu kolumn nie można utworzyć dodatkowe nieklastrowanych indeksów B-drzewa w tej tabeli:

````
CREATE NONCLUSTERED INDEX IX_WebHistNCI ON WebsiteUserInfoHistory ([UserName])
````

Próba tooexecute powyżej instrukcji kończy się niepowodzeniem z hello następujący błąd:

*Msg 13772, poziom 16, stan 1 <br> </br> nie można utworzyć indeksu nieklastrowanego dla tabeli historii danych czasowych "WebsiteUserInfoHistory" ponieważ ma ona okres przechowywania skończona i klastrowany indeks magazynu kolumn zdefiniowane.*

## <a name="querying-tables-with-retention-policy"></a>Tworzenie zapytań o tabele z zasady przechowywania
Wszystkie zapytania w tabeli danych czasowych hello automatycznie odfiltrowywania historycznych wierszy pasujących zasad przechowywania ograniczone, tooavoid nieprzewidywalne i niespójne wyniki, ponieważ przestarzałych wierszy może zostać usunięta przez zadanie oczyszczania hello, *w dowolnym momencie w czasie, a w kolejność dowolnego*.

Witaj poniższej ilustracji przedstawiono hello planu zapytania dla prostego zapytania:

````
SELECT * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME ALL;
````

Zapytanie Hello plan zawiera dodatkowy filtr stosowane tooend (ValidTo) w kolumnie okresu w operatorze hello skanowania indeksu klastrowanego w tabeli historii hello (wyróżniony). W tym przykładzie przyjęto założenie, w tabeli WebsiteUserInfo ustawiono tego okresu przechowywania jeden miesiąc.

![Filtr kwerendy przechowywania](./media/sql-database-temporal-tables-retention-policy/queryexecplanwithretention.png)

Jednak w tabeli historii są zapytania bezpośrednio, może wystąpić wierszy, które są starsze niż przechowywania określony okres, ale bez żadnych gwarancji dla powtarzalne wyniki. Witaj poniższej ilustracji przedstawiono planu wykonania zapytania dla zapytania hello w tabeli historii hello bez dodatkowych filtrów:

![Trwa badanie historii bez filtru przechowywania](./media/sql-database-temporal-tables-retention-policy/queryexecplanhistorytable.png)

Nie należy polegać logiki biznesowej na odczytywania tabeli historii poza okresem przechowywania, jak możesz uzyskać niespójne lub nieoczekiwane wyniki. Zalecane jest użycie czasowych zapytań z klauzulą FOR SYSTEM_TIME do analizowania danych w tabelach danych czasowych.

## <a name="point-in-time-restore-considerations"></a>Punktu w czasie przywracania uwagi
Podczas tworzenia nowej bazy danych przez [Przywracanie istniejącej bazy danych tooa określonego punktu w czasie](sql-database-recovery-using-backups.md), ma przechowywania danych czasowych wyłączona na poziomie bazy danych hello. (**is_temporal_history_retention_enabled** tooOFF ustawiona flaga). Ta funkcja umożliwia tooexamine zostaną usunięte wszystkie wiersze historycznych podczas przywracania, nie martwiąc, które przestarzałe wierszy, zanim będzie można pobrać tooquery je. Służy on zbyt*sprawdzić historycznych danych poza okresem przechowywania skonfigurowanych*.

Załóżmy, że tabela danych czasowych ma podanego okresu przechowywania jeden miesiąc. Jeśli baza danych została utworzona w warstwie Premium usługi, będzie możliwe toocreate kopii bazy danych z hello stan bazy danych w górę too35 dni w przeszłości hello. Które skutecznie pozwoli tooanalyze historycznych wierszy, które są uruchomione too65 dni przez bezpośrednie wysyłanie zapytań hello tabeli historii.

Oczyszczanie przechowywania danych tymczasowych tooactivate, uruchomić hello następującej instrukcji języka Transact-SQL po punkcie w czasie przywracania:

````
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
````

## <a name="next-steps"></a>Następne kroki
jak toouse tabel danych czasowych w aplikacji, zapoznaj się z toolearn [wprowadzenie do tabel danych czasowych w bazie danych SQL Azure](sql-database-temporal-tables.md).

Toohear odwiedziny Channel 9 [klienta rzeczywistych danych czasowych implementacji Powodzenie wątku](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) i obejrzyj [live danych czasowych pokaz](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).

Aby uzyskać szczegółowe informacje o tabelach danych czasowych, przejrzyj [dokumentacji MSDN](https://msdn.microsoft.com/library/dn935015.aspx).

