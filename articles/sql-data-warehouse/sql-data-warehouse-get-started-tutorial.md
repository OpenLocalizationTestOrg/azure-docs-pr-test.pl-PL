---
title: "Rozpoczynanie pracy aaaAzure SQL Data Warehouse — samouczek | Dokumentacja firmy Microsoft"
description: "W tym samouczku jest przedstawienie sposobu tooprovision i ładowanie danych do usługi Azure SQL Data Warehouse. Dowiesz się hello podstawy dotyczące skalowania, wstrzymywanie i dostrajania."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: barbkess
ms.assetid: 52DFC191-E094-4B04-893F-B64D5828A900
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: quickstart
ms.date: 01/26/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: edd2a21b0fe49ca8e9792c7c512310339a822c55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-data-warehouse"></a>Rozpoczynanie pracy z usługą SQL Data Warehouse

Ten samouczek pokazuje, jak tooprovision i ładowanie danych do usługi Azure SQL Data Warehouse. Dowiesz się hello podstawy dotyczące skalowania, wstrzymywanie i dostrajania. Po zakończeniu, należy być gotowe tooquery i Eksploruj magazynu danych.

**Szacowany czas toocomplete:** jest na trasie samouczek z przykładowy kod, który toocomplete około 30 minut po hello wymagania wstępne zostały spełnione. 

## <a name="prerequisites"></a>Wymagania wstępne

Hello samouczka przyjęto założenie, że czytelnik zna podstawowe pojęcia dotyczące usługi SQL Data Warehouse. Wprowadzenie można znaleźć na stronie [Co to jest usługa SQL Data Warehouse?](sql-data-warehouse-overview-what-is.md) 

### <a name="sign-up-for-microsoft-azure"></a>Utwórz konto na platformie Microsoft Azure
Jeśli nie masz już konto Microsoft Azure, należy toosign dla jednego toouse tej usługi. Jeśli masz już konto platformy Azure, pomiń ten krok. 

1. Przejdź do strony konta toohello [https://azure.microsoft.com/account/](https://azure.microsoft.com/account/)
2. Utwórz bezpłatne konto platformy Azure lub zakup konto.
3. Postępuj zgodnie z instrukcjami hello

### <a name="install-appropriate-sql-client-drivers-and-tools"></a>Instalowanie odpowiednich sterowników i narzędzi klienta SQL

Większość narzędzi klienta SQL mogą łączyć się z tooSQL hurtowni danych przy użyciu JDBC, ODBC lub ADO.NET. Powodu toohello dużej liczby funkcje T-SQL, które obsługuje magazyn danych SQL niektóre aplikacje klienckie nie są całkowicie zgodne z usługą Magazyn danych SQL.

Jeśli używasz systemu operacyjnego Windows, zalecamy użycie programu [Visual Studio] lub [SQL Server Management Studio].

[!INCLUDE [Create a new logical server](../../includes/sql-data-warehouse-create-logical-server.md)] 

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="create-a-sql-data-warehouse"></a>Tworzenie bazy danych w usłudze SQL Data Warehouse

Magazyn danych SQL Data Warehouse to specjalny typ bazy danych zaprojektowany z myślą o masowym przetwarzaniu równoległym. Baza danych Hello są rozproszone na wielu węzłach i przetwarza zapytania równolegle. Magazyn danych SQL ma węzeł kontrolny, będąca aranżacją hello działania wszystkich węzłów hello. Witaj w poszczególnych węzłach dane wykorzystywane toomanage bazy danych SQL.  

> [!NOTE]
> Utworzenie bazy danych w usłudze SQL Data Warehouse może skutkować powstaniem nowej usługi płatnej.  Aby uzyskać więcej informacji, zobacz [Cennik usługi SQL Data Warehouse](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).
>

### <a name="create-a-data-warehouse"></a>Tworzenie magazynu danych

1. Zaloguj się na powitania [portalu Azure](https://portal.azure.com).
2. Kliknij pozycję **Nowy** > **Bazy danych** > **SQL Data Warehouse**.

    ![NewBlade](../../includes/media/sql-data-warehouse-create-dw/blade-click-new.png) ![SelectDW](../../includes/media/sql-data-warehouse-create-dw/blade-select-dw.png)

3. Wypełnij szczegóły dotyczące wdrożenia

    **Nazwa bazy danych**: wybierz dowolną. Jeśli masz wiele magazynów danych, zaleca się nazwy zawierają szczegółowe informacje, takie jak hello regionu, środowisko, na przykład *mydw westus-1-test*.

    **Subskrypcja**: Twoja subskrypcja platformy Azure

    **Grupa zasobów**: utwórz grupę zasobów lub użyj istniejącej grupy zasobów.
    > [!NOTE]
    > Grupy zasobów są przydatne w przypadku administrowania zasobami, co obejmuje na przykład wyznaczanie zakresu kontroli dostępu i wdrażanie oparte na szablonach. Więcej o grupach zasobów platformy Azure i najlepszych praktykach możesz dowiedzieć się [tutaj](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups)

    **Źródło**: pusta baza danych

    **Serwer**: serwer hello wybierz utworzony w [wymagania wstępne].

    **Sortowanie**: pozostaw hello domyślnego sortowania SQL_Latin1_General_CP1_CI_AS.

    **Wybierz wydajności**: zalecamy Rozpoczynanie od hello 400DWU standardowa.

4. Wybierz **toodashboard numeru Pin** ![tooDashboard numeru Pin](./media/sql-data-warehouse-get-started-tutorial/pin-to-dashboard.png)

5. Zaczekaj i poczekaj, aż Twoje toodeploy magazynu danych! Jest zjawiskiem tootake tego procesu kilka minut. Hello portal powiadamia użytkownika, gdy magazyn danych jest gotowy toouse. 

## <a name="connect-toosql-data-warehouse"></a>Połącz tooSQL magazynu danych

W tym samouczku korzysta z magazynu danych programu SQL Server Management Studio (SSMS) tooconnect toohello. Możesz połączyć tooSQL hurtowni danych za pośrednictwem obsługiwanych łączników: ADO.NET, JDBC ODBC i PHP. W przypadku narzędzi nieobsługiwanych przez firmę Microsoft funkcjonalność może być ograniczona.


### <a name="get-connection-information"></a>Pobieranie informacji o połączeniu

Magazyn danych tooyour tooconnect, należy tooconnect za pośrednictwem powitania serwera logicznego SQL utworzony w [wymagania wstępne].

1. Wybierz magazyn danych z pulpitu nawigacyjnego hello lub wyszukaj go w Twoich zasobów.

    ![Pulpit nawigacyjny usługi SQL Data Warehouse](./media/sql-data-warehouse-get-started-tutorial/sql-dw-dashboard.png)

2. Znajdź pełną nazwę serwera logicznego SQL hello hello.

    ![Wybieranie nazwy serwera](./media/sql-data-warehouse-get-started-tutorial/select-server.png)

3. Otwórz SSMS i użyj obiektu explorer tooconnect toothis serwera przy użyciu poświadczeń administratora serwera na powitania utworzony w [wymagania wstępne]

    ![Nawiązywanie połączenia z programem SSMS](./media/sql-data-warehouse-get-started-tutorial/ssms-connect.png)

Jeśli wszystko przebiegnie poprawnie, powinno być teraz połączonych tooyour logicznego programu SQL server. Ponieważ użytkownik zalogowany jako administrator serwera Witaj, możesz połączyć tooany bazy danych obsługiwanych przez serwer hello, w tym hello bazy danych master. 

Istnieje tylko jeden serwer, konto administratora i ma hello większość uprawnień przez dowolnego użytkownika. Należy zachować ostrożność nie tooallow zbyt wiele osób w organizacji hasło administratora hello tooknow. 

Możesz również mieć konto administratora usługi Azure Active Directory. Firma Microsoft nie udostępniają hello tutaj. Jeśli chcesz toolearn więcej informacji na temat przy użyciu uwierzytelniania usługi Azure Active Directory, zobacz [uwierzytelniania usługi Azure AD](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).

Następnym tematem jest tworzenie dodatkowych kont logowania i użytkowników.


## <a name="create-a-database-user"></a>Tworzenie użytkownika bazy danych

W tym kroku utworzysz tooaccess konta użytkownika magazynu danych. Możemy również przedstawiają sposób toogive tego użytkownika hello możliwości toorun zapytania dużą ilość pamięci i zasobów Procesora.

### <a name="notes-about-resource-classes-for-allocating-resources-tooqueries"></a>Uwagi dotyczące klasy zasobu przydzielania zasobów tooqueries

- tookeep danych bezpieczne, nie używaj powitania serwera admin toorun zapytania na produkcyjnych baz danych. Ma hello większości uprawnienia każdego użytkownika i przy jego użyciu tooperform operacji na danych użytkownika umieszcza dane na ryzyko. Ponadto ponieważ Witaj, Administratorze server jest przeznaczona tooperform operacji zarządzania, uruchamia operacje, przy użyciu tylko małych alokacji pamięci i zasobów procesora CPU. 

- Usługi SQL Data Warehouse używa ról wstępnie zdefiniowanych bazy danych, o nazwie klasy zasobu, tooallocate różnych ilości pamięci, zasobów Procesora i toousers miejsc współbieżności. Każdy użytkownik może należeć tooa klasy mały, Średni, duża lub bardzo duży zasób. Witaj klasy zasobów użytkownika określa hello zasobów hello użytkownik ma toorun zapytań i załaduj operacji.

- Kompresja danych optymalną hello użytkownika może być wymagane tooload duże lub alokacji zasobów bardzo duża. Więcej o klasach zasobów może dowiedzieć się [tutaj](./sql-data-warehouse-develop-concurrency.md#resource-classes):

### <a name="create-an-account-that-can-control-a-database"></a>Tworzenie konta z możliwością sterowania bazą danych

Ponieważ użytkownik jest zalogowany w hello administratora serwera ma uprawnienia logowania toocreate i użytkowników.

1. Za pomocą programu SSMS lub innego klienta zapytań otwórz nowe zapytanie dotyczące bazy danych **master**.

    ![Nowe zapytanie w bazie danych master Master](./media/sql-data-warehouse-get-started-tutorial/query-on-server.png)

    ![Nowe zapytanie w bazie danych master Master1](./media/sql-data-warehouse-get-started-tutorial/query-on-master.png)

2. W oknie zapytania hello Uruchom to toocreate polecenia T-SQL o nazwie MedRCLogin logowania i użytkownika o nazwie LoadingUser. Tę nazwę logowania można połączyć toohello logicznego programu SQL server.

    ```sql
    CREATE LOGIN MedRCLogin WITH PASSWORD = 'a123reallySTRONGpassword!';
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

3. Teraz zapytanie hello *bazy danych magazynu danych SQL*, utworzyć użytkownika bazy danych na podstawie hello utworzony tooaccess logowania i wykonywania operacji na powitania bazy danych.

    ```sql
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

4. Nadaj hello użytkownika kontroli uprawnień toohello baza danych o nazwie NYT. 

    ```sql
    GRANT CONTROL ON DATABASE::[NYT] tooLoadingUser;
    ```
    > [!NOTE]
    > Jeśli nazwa bazy danych ma łączników, należy się toowrap go w nawiasach! 
    >

### <a name="give-hello-user-medium-resource-allocations"></a>Nadaj alokacji zasobów średnia użytkownika hello

1. Uruchom ten toomake polecenia T-SQL it, a element członkowski klasy hello średnia zasobu, która jest wywoływana mediumrc. 

    ```sql
    EXEC sp_addrolemember 'mediumrc', 'LoadingUser';
    ```
    > [!NOTE]
    > Kliknij przycisk [tutaj](sql-data-warehouse-develop-concurrency.md#resource-classes) toolearn więcej informacji na temat klas współbieżności i zasobów! 
    >

2. Połącz z nowymi poświadczeniami hello toohello serwera logicznego

    ![Zaloguj się za pomocą nowego identyfikatora logowania](./media/sql-data-warehouse-get-started-tutorial/new-login.png)


## <a name="load-data-from-azure-blob-storage"></a>Ładowanie danych usługi Azure Blob Storage

Wszystko jest teraz gotowy tooload danych w magazynie danych. W tym kroku przedstawiono sposób obiektu blob tooload nowego Jorku taksówki cab danych z publicznej usługi Azure storage. 

- Typowa tooload danych do usługi SQL Data Warehouse jest toofirst przenieść magazyn obiektów blob tooAzure danych hello, a następnie załadować go do magazynu danych. toomake on toounderstand łatwiejszy sposób tooload, mamy danych pliku cab taksówki Nowy Jork już hostowana w obiekcie blob magazynu Azure publicznego. 

- Do użytku w przyszłości, toolearn jak tooget Twojego tooAzure danych obiektu blob magazynu lub tooload go bezpośrednio ze źródła do usługi SQL Data Warehouse, zobacz hello [omówienie ładowania](sql-data-warehouse-overview-load.md).


### <a name="define-external-data"></a>Definiowanie danych zewnętrznych

1. Utwórz klucz główny. Wystarczy toocreate klucz główny raz na bazie danych. 

    ```sql
    CREATE MASTER KEY;
    ```

2. Zdefiniuj lokalizację hello hello obiektów blob platformy Azure, zawierający dane pliku cab taksówki hello.  

    ```sql
    CREATE EXTERNAL DATA SOURCE NYTPublic
    WITH
    (
        TYPE = Hadoop,
        LOCATION = 'wasbs://2013@nytpublic.blob.core.windows.net/'
    );
    ```

3. Zdefiniuj hello formatów plików zewnętrznych

    Witaj ```CREATE EXTERNAL FILE FORMAT``` polecenie jest toospecify używany format plików, które zawierają hello danych zewnętrznych. Zawierają one tekst rozdzielony znakami nazywanymi ogranicznikami. Dla celów demonstracyjnych hello taksówki cab dane są przechowywane, zarówno jako nieskompresowanych danych, jak i jako dane skompresowane gzip.

    Uruchom te polecenia T-SQL toodefine dwóch różnych formatach: nieskompresowane i skompresowane.

    ```sql
    CREATE EXTERNAL FILE FORMAT uncompressedcsv
    WITH (
        FORMAT_TYPE = DELIMITEDTEXT,
        FORMAT_OPTIONS ( 
            FIELD_TERMINATOR = ',',
            STRING_DELIMITER = '',
            DATE_FORMAT = '',
            USE_TYPE_DEFAULT = False
        )
    );

    CREATE EXTERNAL FILE FORMAT compressedcsv
    WITH ( 
        FORMAT_TYPE = DELIMITEDTEXT,
        FORMAT_OPTIONS ( FIELD_TERMINATOR = '|',
            STRING_DELIMITER = '',
        DATE_FORMAT = '',
            USE_TYPE_DEFAULT = False
        ),
        DATA_COMPRESSION = 'org.apache.hadoop.io.compress.GzipCodec'
    );
    ```

4.  Utwórz schemat dla formatu plików zewnętrznych. 

    ```sql
    CREATE SCHEMA ext;
    ```
5. Utwórz hello tabel zewnętrznych. Te tabele odwołują się do danych przechowywanych w usłudze Azure Blob Storage. Uruchom następujące toocreate polecenia T-SQL hello kilku tabel zewnętrznych, że wszystkie punktu toohello obiektów blob platformy Azure zdefiniowanego wcześniej w naszym zewnętrznego źródła danych.

```sql
    CREATE EXTERNAL TABLE [ext].[Date] 
    (
        [DateID] int NOT NULL,
        [Date] datetime NULL,
        [DateBKey] char(10) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfMonth] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DaySuffix] varchar(4) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeek] char(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeekInMonth] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeekInYear] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfQuarter] varchar(3) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfYear] varchar(3) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfMonth] varchar(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfQuarter] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfYear] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Month] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthOfQuarter] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Quarter] char(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [QuarterName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Year] char(4) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [YearName] char(7) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthYear] char(10) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MMYYYY] char(6) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [FirstDayOfMonth] date NULL,
        [LastDayOfMonth] date NULL,
        [FirstDayOfQuarter] date NULL,
        [LastDayOfQuarter] date NULL,
        [FirstDayOfYear] date NULL,
        [LastDayOfYear] date NULL,
        [IsHolidayUSA] bit NULL,
        [IsWeekday] bit NULL,
        [HolidayUSA] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Date',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    );
    
    CREATE EXTERNAL TABLE [ext].[Geography]
    (
        [GeographyID] int NOT NULL,
        [ZipCodeBKey] varchar(10) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [County] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [City] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [State] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Country] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [ZipCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Geography',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0 
    );
        
    
    CREATE EXTERNAL TABLE [ext].[HackneyLicense]
    (
        [HackneyLicenseID] int NOT NULL,
        [HackneyLicenseBKey] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [HackneyLicenseCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'HackneyLicense',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
        
    
    CREATE EXTERNAL TABLE [ext].[Medallion]
    (
        [MedallionID] int NOT NULL,
        [MedallionBKey] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [MedallionCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Medallion',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
        
    CREATE EXTERNAL TABLE [ext].[Time]
    (
        [TimeID] int NOT NULL,
        [TimeBKey] varchar(8) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [HourNumber] tinyint NOT NULL,
        [MinuteNumber] tinyint NOT NULL,
        [SecondNumber] tinyint NOT NULL,
        [TimeInSecond] int NOT NULL,
        [HourlyBucket] varchar(15) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [DayTimeBucketGroupKey] int NOT NULL,
        [DayTimeBucket] varchar(100) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL
    )
    WITH
    (
        LOCATION = 'Time',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
    
    
    CREATE EXTERNAL TABLE [ext].[Trip]
    (
        [DateID] int NOT NULL,
        [MedallionID] int NOT NULL,
        [HackneyLicenseID] int NOT NULL,
        [PickupTimeID] int NOT NULL,
        [DropoffTimeID] int NOT NULL,
        [PickupGeographyID] int NULL,
        [DropoffGeographyID] int NULL,
        [PickupLatitude] float NULL,
        [PickupLongitude] float NULL,
        [PickupLatLong] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DropoffLatitude] float NULL,
        [DropoffLongitude] float NULL,
        [DropoffLatLong] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [PassengerCount] int NULL,
        [TripDurationSeconds] int NULL,
        [TripDistanceMiles] float NULL,
        [PaymentType] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [FareAmount] money NULL,
        [SurchargeAmount] money NULL,
        [TaxAmount] money NULL,
        [TipAmount] money NULL,
        [TollsAmount] money NULL,
        [TotalAmount] money NULL
    )
    WITH
    (
        LOCATION = 'Trip2013',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = compressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
    
    CREATE EXTERNAL TABLE [ext].[Weather]
    (
        [DateID] int NOT NULL,
        [GeographyID] int NOT NULL,
        [PrecipitationInches] float NOT NULL,
        [AvgTemperatureFahrenheit] float NOT NULL
    )
    WITH
    (
        LOCATION = 'Weather2013',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
```

### <a name="import-hello-data-from-azure-blob-storage"></a>Importuj dane hello z magazynu obiektów blob platformy Azure.

Usługa SQL Data Warehouse obsługuje kluczową instrukcję o nazwie CREATE TABLE AS SELECT (CTAS). Ta instrukcja tworzy nową tabelę na podstawie wyników hello instrukcji select. Witaj nowa tabela zawiera hello tej samej kolumny i typy danych jak wyniki hello hello wybierz instrukcji.  To są dane tooimport elegancki sposób z magazynu obiektów blob platformy Azure do usługi SQL Data Warehouse.

1. Uruchom ten skrypt tooimport danych.

    ```sql
    CREATE TABLE [dbo].[Date]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Date]
    OPTION (LABEL = 'CTAS : Load [dbo].[Date]')
    ;
    
    CREATE TABLE [dbo].[Geography]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS
    SELECT * FROM [ext].[Geography]
    OPTION (LABEL = 'CTAS : Load [dbo].[Geography]')
    ;
    
    CREATE TABLE [dbo].[HackneyLicense]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[HackneyLicense]
    OPTION (LABEL = 'CTAS : Load [dbo].[HackneyLicense]')
    ;
    
    CREATE TABLE [dbo].[Medallion]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Medallion]
    OPTION (LABEL = 'CTAS : Load [dbo].[Medallion]')
    ;
    
    CREATE TABLE [dbo].[Time]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Time]
    OPTION (LABEL = 'CTAS : Load [dbo].[Time]')
    ;
    
    CREATE TABLE [dbo].[Weather]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Weather]
    OPTION (LABEL = 'CTAS : Load [dbo].[Weather]')
    ;
    
    CREATE TABLE [dbo].[Trip]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Trip]
    OPTION (LABEL = 'CTAS : Load [dbo].[Trip]')
    ;
    ```

2. Wyświetlaj dane podczas ładowania.

   Ładowane jest kilka gigabajtów danych, które są kompresowane do wysoce wydajnych indeksów magazynu kolumn klastra. Uruchom następujące zapytanie, które korzysta z dynamicznego zarządzania widoków (widoków DMV) tooshow hello stan obciążenia hello hello. Po uruchomieniu kwerendy hello, wystarczy pobrać kawy i popcorn podczas SQL Data Warehouse nie niektórych lifting ciężki.
    
    ```sql
    SELECT
        r.command,
        s.request_id,
        r.status,
        count(distinct input_name) as nbr_files,
        sum(s.bytes_processed)/1024/1024/1024 as gb_processed
    FROM 
        sys.dm_pdw_exec_requests r
        INNER JOIN sys.dm_pdw_dms_external_work s
        ON r.request_id = s.request_id
    WHERE
        r.[label] = 'CTAS : Load [dbo].[Date]' OR
        r.[label] = 'CTAS : Load [dbo].[Geography]' OR
        r.[label] = 'CTAS : Load [dbo].[HackneyLicense]' OR
        r.[label] = 'CTAS : Load [dbo].[Medallion]' OR
        r.[label] = 'CTAS : Load [dbo].[Time]' OR
        r.[label] = 'CTAS : Load [dbo].[Weather]' OR
        r.[label] = 'CTAS : Load [dbo].[Trip]'
    GROUP BY
        r.command,
        s.request_id,
        r.status
    ORDER BY
        nbr_files desc, 
        gb_processed desc;
    ```

3. Wyświetl wszystkie zapytania systemowe.

    ```sql
    SELECT * FROM sys.dm_pdw_exec_requests;
    ```

4. Korzystaj z danych poprawnie załadowanych do usługi Azure SQL Data Warehouse.

    ![Wyświetl załadowane dane](./media/sql-data-warehouse-get-started-tutorial/see-data-loaded.png)


## <a name="improve-query-performance"></a>Zwiększanie wydajności zapytań

Istnieje kilka sposobów tooimprove kwerendy wydajności i tooachieve hello szybkich wydajność usługi SQL Data Warehouse jest zaprojektowany tooprovide.  

### <a name="see-hello-effect-of-scaling-on-query-performance"></a>Zobacz efekt hello skalowanie na wydajność zapytań 

Wydajność zapytania jednokierunkowej tooimprove jest tooscale zasobów, zmieniając poziom usług DWU hello magazynu danych. Poszczególne poziomy usług są coraz droższe, ale w dowolnej chwili można przeprowadzić skalowanie w dół lub wstrzymać zasoby. 

W tym kroku wykonywane jest porównanie wydajności dla dwóch różnych ustawień jednostek DWU.

Najpierw Przeprowadź skalowanie hello zmiany rozmiaru w dół too100 DWU, więc można pobrać informacje o tym, jak jeden węzeł obliczeń może wykonywać samodzielnie.

1. Przejdź toohello portalu i wybierz polecenie SQL Data Warehouse.

2. W bloku usługi SQL Data Warehouse hello wybierz skali. 

    ![Skalowanie usługi SQL Data Warehouse z poziomu portalu](./media/sql-data-warehouse-get-started-tutorial/scale-dw.png)

3. Dół wydajności hello paska too100 DWU i kliknij przycisk Zapisz.

    ![Skaluj i zapisz](./media/sql-data-warehouse-get-started-tutorial/scale-and-save.png)

4. Poczekaj, aż Twoje toofinish operacji skalowania.

    > [!NOTE]
    > Zapytania nie można uruchomić podczas zmiany hello skali. Skalowanie powoduje **skasowanie** aktualnie uruchomionych zapytań. Można uruchomić je ponownie, po zakończeniu operacji hello.
    >
    
5. Wykonaj operację skanowania na powitania podróży danych, wybierając hello top milionów wpisy dla wszystkich kolumn hello. Jeśli używasz wczesny toomove szybko, możesz tooselect wolnego mniej wierszy. Zwróć uwagę na powitania czas toorun tej operacji.

    ```sql
    SELECT TOP(1000000) * FROM dbo.[Trip]
    ```
6. Skalować dane kopii too400 DWU. Należy pamiętać, że w każdym 100 DWU polega na dodaniu innego tooyour węzła obliczeń magazyn danych SQL Azure.

7. Ponownie uruchom zapytanie Witaj! Powinna być zauważalna istotna różnica. 

    > [!NOTE]
    > Ponieważ hello zapytanie zwraca dużą ilość danych, dostępnej przepustowości hello maszyny hello uruchomionej SSMS może być wąskie gardło. Może to spowodować, że użytkownik nie odczuje jakiegokolwiek zwiększenia wydajności.

> [!NOTE]
> Usługa SQL Data Warehouse korzysta bowiem z masowego przetwarzania równoległego. Zapytania, które skanowania ani wykonywać funkcje analityczne na miliony wierszy wystąpić hello true możliwości usługi Azure SQL Data Warehouse.
>

### <a name="see-hello-effect-of-statistics-on-query-performance"></a>Zobaczyć efekt hello statystyk na wydajność zapytań

1. Uruchom zapytanie, że sprzężenia hello tabeli danych z tabeli podróży hello

    ```sql
    SELECT TOP (1000000) 
        dt.[DayOfWeek],
        tr.[MedallionID],
        tr.[HackneyLicenseID],
        tr.[PickupTimeID],
        tr.[DropoffTimeID],
        tr.[PickupGeographyID],
        tr.[DropoffGeographyID],
        tr.[PickupLatitude],
        tr.[PickupLongitude],
        tr.[PickupLatLong],
        tr.[DropoffLatitude],
        tr.[DropoffLongitude],
        tr.[DropoffLatLong],
        tr.[PassengerCount],
        tr.[TripDurationSeconds],
        tr.[TripDistanceMiles],
        tr.[PaymentType],
        tr.[FareAmount],
        tr.[SurchargeAmount],
        tr.[TaxAmount],
        tr.[TipAmount],
        tr.[TollsAmount],
        tr.[TotalAmount]
    FROM [dbo].[Trip] as tr
        JOIN dbo.[Date] as dt
        ON  tr.DateID = dt.DateID
    ```

    To zapytanie zajmie trochę czasu, ponieważ Magazyn danych SQL ma tooshuffle danych, zanim można wykonywać hello sprzężenia. Sprzężenia nie ma danych tooshuffle, jeśli są one zaprojektowane toojoin danych hello jest rozpowszechniana tak samo. Jest to nieco skomplikowane. 

2. Przychodzi tu z pomocą statystyka. 
3. Uruchom statystyki toocreate tej instrukcji na powitania kolumn sprzężenia.

    ```sql
    CREATE STATISTICS [dbo.Date DateID stats] ON dbo.Date (DateID);
    CREATE STATISTICS [dbo.Trip DateID stats] ON dbo.Trip (DateID);
    ```

    > [!NOTE]
    > Usługa SQL Data Warehouse nie zarządza statystykami automatycznie. Statystyki są istotne w przypadku wydajności zapytań i zdecydowanie zalecane jest ich tworzenie i aktualizowanie.
    > 
    > **Możesz uzyskać hello największe korzyści uzyskanie statystyki do kolumn uczestniczących w sprzężeniu, kolumn używanych w hello klauzuli i kolumny wykrytych GROUP BY.**
    >

3. Ponownie uruchom zapytanie hello z wymagań wstępnych i sprawdź wszystkie problemy dotyczące różnic wydajności. Podczas hello różnic w wydajności zapytania nie zostanie jako radykalne jako skalowanie, można zauważyć, przyspieszyć. 

## <a name="next-steps"></a>Następne kroki

Jest teraz gotowy tooquery i eksplorowanie. Zapoznaj się z naszymi najlepszymi praktykami i poradami.

Gdy wszystko będzie gotowe poszukiwania dzień hello, upewnij się, że toopause wystąpienia! W środowisku produkcyjnym, może występować znaczne oszczędności wstrzymywania i skalowanie toomeet potrzeb biznesowych.

![Wstrzymaj](./media/sql-data-warehouse-get-started-tutorial/pause.png)

## <a name="useful-readings"></a>Przydatne zasoby

[Współbieżność i zarządzanie obciążeniami][]

[Najlepsze praktyki dotyczące korzystania z usługi Azure SQL Data Warehouse][]

[Monitorowanie zapytań][]

[10 najlepszych praktyk dotyczących tworzenia relacyjnego magazynu danych w dużej skali][]

[Migrowanie danych tooAzure SQL Data Warehouse][]

[Współbieżność i zarządzanie obciążeniami]: sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example
[Najlepsze praktyki dotyczące korzystania z usługi Azure SQL Data Warehouse]: sql-data-warehouse-best-practices.md#hash-distribute-large-tables
[Monitorowanie zapytań]: sql-data-warehouse-manage-monitor.md
[10 najlepszych praktyk dotyczących tworzenia relacyjnego magazynu danych w dużej skali]: https://blogs.msdn.microsoft.com/sqlcat/2013/09/16/top-10-best-practices-for-building-a-large-scale-relational-data-warehouse/
[Migrowanie danych tooAzure SQL Data Warehouse]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/



[!INCLUDE [Additional Resources](../../includes/sql-data-warehouse-article-footer.md)]

<!-- Internal Links -->
[wymagania wstępne]: sql-data-warehouse-get-started-tutorial.md#prerequisites

<!--Other Web references-->
[Visual Studio]: https://www.visualstudio.com/
[SQL Server Management Studio]: https://msdn.microsoft.com/en-us/library/mt238290.aspx
