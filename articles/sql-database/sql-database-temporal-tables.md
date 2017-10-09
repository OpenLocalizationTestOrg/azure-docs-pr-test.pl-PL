---
title: "aaaGetting rozpoczęte w tabelach danych czasowych w bazie danych SQL Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooget pracę z przy użyciu tabel danych czasowych w bazie danych SQL Azure."
services: sql-database
documentationcenter: 
author: bonova
manager: jhubbard
editor: 
ms.assetid: c8c0f232-0751-4a7f-a36e-67a0b29fa1b8
ms.service: sql-database
ms.custom: develop databases
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: sql-database
ms.date: 01/10/2017
ms.author: bonova
ms.openlocfilehash: 54f394b51df07aa2f9bb299f207e692171d23479
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-temporal-tables-in-azure-sql-database"></a>Wprowadzenie do tabel danych czasowych w bazie danych Azure SQL
Tabele danych czasowych są nową funkcją programowalności bazy danych SQL Azure, która pozwala tootrack i analizować hello pełną historię zmian danych, bez potrzeby hello programowania. Tabele danych czasowych zachować kontekstu tootime ściśle powiązanych danych, aby przechowywane dane mogą być interpretowane jako prawidłowy tylko w określonym okresie hello. Ta właściwość tabel danych czasowych umożliwia wydajne analizy na podstawie czasu i pobierania wgląd w dane dotyczące zmiany danych.

## <a name="temporal-scenario"></a>Scenariusz danych czasowych
W tym artykule przedstawiono hello kroki tooutilize tabel danych czasowych w scenariuszu aplikacji. Załóżmy, że chcesz tootrack aktywność użytkownika na nowej witryny sieci Web, który jest obecnie opracowywane od początku lub na istniejącej witryny sieci Web, które mają tooextend z analizowanie aktywności użytkowników. W tym przykładzie uproszczony przyjęto założenie, że hello liczbę odwiedzonych stron sieci web w okresie czasu jest wskaźnik musi toobe przechwycony i monitorowane w bazie danych witryny sieci Web hello, który znajduje się w bazie danych SQL Azure. Celem Hello hello historycznej analizy aktywności użytkownika tooget dane wejściowe tooredesign witryny sieci Web i zapewnia lepsze środowisko dla użytkowników zewnętrznych hello.

Witaj modelu bazy danych dla tego scenariusza jest bardzo prosty — pomiar aktywności użytkownika odpowiada za pomocą pola jeden **PageVisited**i są przechwytywane oraz podstawowe informacje na temat hello profilu użytkownika. Ponadto do analizy na podstawie czasu można zachowa serii wierszy dla każdego użytkownika, której każdy wiersz reprezentuje hello liczbę stron, dany użytkownik odwiedzi w określonym okresie czasu.

![Schemat](./media/sql-database-temporal-tables/AzureTemporal1.png)

Na szczęście, nie trzeba tooput wszelkich starań w Twojej aplikacji toomaintain informacje te działania. W tabelach danych czasowych ten proces jest automatyczne — umożliwiając pełną elastyczność podczas projektowania witryny sieci Web i więcej toofocus czas na powitania analizy danych, sama. Witaj, co ma toodo jest tooensure tylko który **WebSiteInfo** tabeli jest skonfigurowany jako [danych czasowych systemową kontrolą wersji](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_0). Witaj kolejnych kroków tooutilize tabel danych czasowych w tym scenariuszu opisano poniżej.

## <a name="step-1-configure-tables-as-temporal"></a>Krok 1: Konfigurowanie tabel jako danych czasowych
W zależności od tego, czy są uruchamianie nowych aplikacji lub uaktualnienia istniejącej aplikacji zostanie Tworzenie tabel danych czasowych lub modyfikować istniejące przez dodanie atrybutów danych czasowych. Ogólnie rzecz biorąc przypadku danego scenariusza można kombinacja tych dwóch opcji. Wykonaj te za pomocą akcji [programu SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) (SSMS), [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) (SSDT) lub inne narzędzie do projektowania języka Transact-SQL.

> [!IMPORTANT]
> Zalecane jest, aby zawsze używała hello najnowszej wersji programu Management Studio tooremain synchronizowane z tooMicrosoft aktualizacje, Azure i bazy danych SQL. [Zaktualizuj program SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).
> 
> 

### <a name="create-new-table"></a>Utwórz nową tabelę
W menu kontekstowym "Nową tabelę systemową kontrolą wersji" w edytorze zapytań hello tooopen Eksplorator obiektów programu SSMS za pomocą skryptu szablonu tabeli danych czasowych, a następnie użyć szablonu hello toopopulate "Określ wartości dla parametrów szablonu" (Ctrl + Shift + M):

![SSMSNewTable](./media/sql-database-temporal-tables/AzureTemporal2.png)

Programu SSDT wybierz szablon "(systemową) tabeli danych czasowych" podczas dodawania nowych elementów toohello bazy danych projektu. Czy będzie designer Otwórz tabelę i Włącz tooeasily możesz określić hello układu tabeli:

![SSDTNewTable](./media/sql-database-temporal-tables/AzureTemporal3.png)

Można również tworzenie tabeli danych czasowych, określając instrukcji języka Transact-SQL hello bezpośrednio, jak pokazano w poniższym przykładzie hello. Należy zauważyć, że elementy obowiązkowe hello każda tabela danych czasowych klauzuli SYSTEM_VERSIONING hello z tabelą użytkownika tooanother odwołania, który będzie przechowywać wersje wierszy historycznych i definicji okresu hello:

````
CREATE TABLE WebsiteUserInfo 
(  
    [UserID] int NOT NULL PRIMARY KEY CLUSTERED 
  , [UserName] nvarchar(100) NOT NULL
  , [PagesVisited] int NOT NULL 
  , [ValidFrom] datetime2 (0) GENERATED ALWAYS AS ROW START
  , [ValidTo] datetime2 (0) GENERATED ALWAYS AS ROW END
  , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)
 )  
 WITH (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.WebsiteUserInfoHistory));
````

Hello towarzyszące tabeli historii z konfiguracji domyślnej hello jest tworzony automatycznie podczas tworzenia tabeli danych czasowych z systemową kontrolą wersji. Tabela historii domyślne Hello zawiera B-drzewa indeksu klastrowanego na kolumny okresu hello (koniec, start) z włączoną kompresją strony. Ta konfiguracja jest optymalna dla hello większość scenariuszy, w których są używane tabele danych czasowych, szczególnie w przypadku [inspekcja danych](https://msdn.microsoft.com/library/mt631669.aspx#Anchor_0). 

W tym przypadku firma Microsoft osiągnięcia analizy trendów na podstawie czasu tooperform za pośrednictwem dłużej historii danych i większych zestawów danych, więc hello wybór magazynu dla tabeli historii hello jest klastrowany indeks magazynu kolumn. Klastrowanego magazynu kolumn zawiera bardzo dobre kompresji i wydajności dla zapytań analitycznych. Całkowicie niezależnie hello elastyczność tooconfigure indeksów w tabelach bieżących i danych czasowych hello podać tabel danych czasowych. 

> [!NOTE]
> Indeksy magazynu kolumn są dostępne tylko w warstwie usług premium hello.
>

Witaj następującego skryptu pokazuje, jak domyślny indeks w tabeli historii może być zmienione toohello klastrowanego magazynu kolumn:

````
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory
ON dbo.WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON); 
````

Tabele danych czasowych są reprezentowane w hello Eksplorator obiektów z określonych ikonę hello ułatwiają identyfikację podczas jego tabeli historii jest wyświetlany jako węzeł podrzędny.

![AlterTable](./media/sql-database-temporal-tables/AzureTemporal4.png)

### <a name="alter-existing-table-tootemporal"></a>Zmienia istniejące tootemporal tabeli
Teraz obejmuje hello alternatywnych scenariusz, w których hello WebsiteUserInfo tabeli już istnieje, ale nie zostało zaprojektowane tookeep historię zmian. W takim przypadku można po prostu rozszerzyć hello istniejącej tabeli toobecome danych czasowych, jak pokazano na powitania poniższy przykład:

````
ALTER TABLE WebsiteUserInfo 
ADD 
    ValidFrom datetime2 (0) GENERATED ALWAYS AS ROW START HIDDEN  
        constraint DF_ValidFrom DEFAULT DATEADD(SECOND, -1, SYSUTCDATETIME())
    , ValidTo datetime2 (0)  GENERATED ALWAYS AS ROW END HIDDEN   
        constraint DF_ValidTo DEFAULT '9999.12.31 23:59:59.99'
    , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo); 

ALTER TABLE WebsiteUserInfo  
SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.WebsiteUserInfoHistory));
GO

CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory
ON dbo.WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON); 
````

## <a name="step-2-run-your-workload-regularly"></a>Krok 2: Regularnego uruchamiania obciążenia
główną zaletą tabel danych czasowych w Hello jest możesz nie wymagają toochange lub Dostosuj witryny sieci Web w sposób zmiany tooperform śledzenia. Po utworzeniu tabel danych czasowych niewidocznie utrwalić poprzednie wersje wiersza za każdym razem, gdy wykonywania modyfikacji danych w. 

W kolejności tooleverage śledzenie zmian automatycznego dla tego scenariusza, umożliwia tylko zaktualizować kolumny **PagesVisited** za każdym razem, gdy użytkownik kończy się jego sesji w witrynie sieci Web hello:

````
UPDATE WebsiteUserInfo  SET [PagesVisited] = 5 
WHERE [UserID] = 1;
````

Jest ważne toonotice, który hello zapytanie update nie musi tooknow hello dokładny czas, gdy podczas bieżącej operacji hello ani w jaki sposób dane historyczne zostaną zachowane dla przyszłych analizy. Zarówno aspekty automatycznie są obsługiwane przez hello bazy danych SQL Azure. Witaj poniższym diagramie przedstawiono sposób dane historii jest generowany na każdej aktualizacji.

![TemporalArchitecture](./media/sql-database-temporal-tables/AzureTemporal5.png)

## <a name="step-3-perform-historical-data-analysis"></a>Krok 3: Wykonanie analizy danych historycznych
Teraz po włączeniu danych czasowych system-versioning analizy danych historycznych jest tylko jedno zapytanie od użytkownika. W tym artykule, firma Microsoft będzie zawierają kilka przykładów, które rozwiązują typowe scenariusze analizy - toolearn wszystkie szczegółowe informacje, zapoznaj się różne opcje wprowadzone w systemie hello [FOR SYSTEM_TIME](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_3) klauzuli.

toosee hello 10 użytkownicy z największą uporządkowanych według liczby hello odwiedzane strony sieci web na godzinę temu, uruchom to zapytanie:

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
SELECT TOP 10 * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME AS OF @hourAgo
ORDER BY PagesVisited DESC
````

To zapytanie może dopasowywać tooanalyze hello wizyty dzień temu miesiąc temu lub w dowolnym momencie w przeszłości hello ma.

dla hello podstawowych celów analizy statystycznej tooperform poprzedniego dnia, użyj hello poniższy przykład:

````
DECLARE @twoDaysAgo datetime2 = DATEADD(DAY, -2, SYSUTCDATETIME());
DECLARE @aDayAgo datetime2 = DATEADD(DAY, -1, SYSUTCDATETIME());

SELECT UserID, SUM (PagesVisited) as TotalVisitedPages, AVG (PagesVisited) as AverageVisitedPages,
MAX (PagesVisited) AS MaxVisitedPages, MIN (PagesVisited) AS MinVisitedPages,
STDEV (PagesVisited) as StDevViistedPages
FROM dbo.WebsiteUserInfo 
FOR SYSTEM_TIME BETWEEN @twoDaysAgo AND @aDayAgo
GROUP BY UserId
````

toosearch działań określonego użytkownika, w określonym przedziale czasu, użyj hello ZAWARTEJ w klauzuli:

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
DECLARE @twoHoursAgo datetime2 = DATEADD(HOUR, -2, SYSUTCDATETIME());
SELECT * FROM dbo.WebsiteUserInfo 
FOR SYSTEM_TIME CONTAINED IN (@twoHoursAgo, @hourAgo)
WHERE [UserID] = 1;
````

Graficzne wizualizacji jest szczególnie wygodne czasowych zapytań, jak można wyświetlić trendów i wzorców użytkowania w intuicyjny sposób bardzo łatwo:

![TemporalGraph](./media/sql-database-temporal-tables/AzureTemporal6.png)

## <a name="evolving-table-schema"></a>Schemat tabeli zmieniające się
Zazwyczaj należy schemat tabeli danych czasowych hello toochange podczas operacji tworzenia aplikacji. W tym wystarczy uruchomić regularne instrukcji ALTER TABLE i bazy danych SQL Azure odpowiednio rozpropaguje zmiany toohello historii tabeli. Witaj poniższy skrypt pokazuje, jak dodać dodatkowe atrybut śledzenia:

````
/*Add new column for tracking source IP address*/
ALTER TABLE dbo.WebsiteUserInfo 
ADD  [IPAddress] varchar(128) NOT NULL CONSTRAINT DF_Address DEFAULT 'N/A';
````

Podobnie można zmienić definicji kolumny, gdy obciążenie jest aktywna:

````
/*Increase hello length of name column*/
ALTER TABLE dbo.WebsiteUserInfo 
    ALTER COLUMN  UserName nvarchar(256) NOT NULL;
````

Na koniec można usunąć kolumny, które nie są już potrzebne.

````
/*Drop unnecessary column */
ALTER TABLE dbo.WebsiteUserInfo 
    DROP COLUMN TemporaryColumn; 
````

Można również użyć najnowszej [SSDT](https://msdn.microsoft.com/library/mt204009.aspx) toochange danych czasowych tabeli schematu, gdy są połączone toohello bazy danych (w trybie online) lub jako część hello projekt bazy danych (w trybie offline).

## <a name="controlling-retention-of-historical-data"></a>Kontrolowanie przechowywania danych historycznych
Tabela historii hello może zwiększyć tabelach danych czasowych z systemową kontrolą wersji hello baz danych o rozmiarze ponad zwykłych tabelach. Tabel historii duży i coraz dłuższej może stać się problemem w obu toopure kosztów magazynowania, a także nakładające wydajności podatek danych czasowych zapytań. W związku z tym tworzenie zasad przechowywania danych zarządzania danymi w tabeli historii hello jest istotnym elementem planowania i zarządzanie cyklem życia hello każdej tabeli danych czasowych. Z bazy danych SQL Azure masz następujące podejścia do zarządzania danych historycznych w tabeli danych czasowych hello hello:

* [Partycjonowanie tabel](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_2)
* [Skrypt czyszczący niestandardowych](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_3)

## <a name="next-steps"></a>Następne kroki
Aby uzyskać szczegółowe informacje w tabelach danych czasowych, zapoznaj się z [dokumentacji MSDN](https://msdn.microsoft.com/library/dn935015.aspx).
Toohear odwiedziny Channel 9 [klienta rzeczywistych danych czasowych implementacji Powodzenie wątku](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) i obejrzyj [live danych czasowych pokaz](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).

