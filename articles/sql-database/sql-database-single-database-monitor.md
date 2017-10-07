---
title: "aaaMonitoring wydajność bazy danych w usłudze Azure SQL Database | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat hello opcje monitorowania bazy danych za pomocą narzędzi Azure i dynamicznych widoków zarządzania."
keywords: "monitorowanie bazy danych, wydajność bazy danych w chmurze"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: a2e47475-c955-4a8d-a65c-cbef9a6d9b9f
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: b13771183d4ccf37f58e2fc518b9b14de38212dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-database-performance-in-azure-sql-database"></a>Monitorowanie wydajności bazy danych w usłudze Azure SQL Database
Monitorowanie wydajności hello bazy danych SQL na platformie Azure rozpoczyna się od monitorowania hello zasobów wykorzystania względną toohello poziomu wydajności bazy danych, wybranych. Monitorowanie pomaga ustalić, czy baza danych ma nadmiarowej pojemności lub czy nie występują problemy, ponieważ limit maksymalnego wykorzystania zasobów, a następnie zdecydować, czy poziom wydajności hello tooadjust czasu i [warstwy usług](sql-database-service-tiers.md) bazy danych. Można monitorować bazy danych za pomocą narzędzi graficznych w hello [portalu Azure](https://portal.azure.com) lub przy użyciu programu SQL [dynamicznych widoków zarządzania](https://msdn.microsoft.com/library/ms188754.aspx).

## <a name="monitor-databases-using-hello-azure-portal"></a>Monitorowanie baz danych przy użyciu hello portalu Azure
W hello [portalu Azure](https://portal.azure.com/), można monitorować wykorzystanie pojedynczej bazy danych wybrać bazę danych, a następnie klikając polecenie hello **monitorowanie** wykresu. Spowoduje to wyświetlenie **Metryka** oknie, w którym można zmienić, klikając hello **Edytuj wykres** przycisku. Dodaj następujące metryki hello:

* Procent użycia procesora CPU
* Procent użycia jednostek DTU
* Procent użycia operacji we/wy na danych
* Procent użycia rozmiaru bazy danych

Po dodaniu tych metryk możesz nadal tooview je hello **monitorowanie** wykres z bardziej szczegółowymi informacjami na powitania **Metryka** okna. Wszystkie cztery metryki pokazują hello średnie wykorzystanie procent względną toohello **jednostek dtu w warstwie** bazy danych. Zobacz hello [warstw usług](sql-database-service-tiers.md) artykułu, aby uzyskać szczegółowe informacje o Dtu.

![Monitorowanie warstw usług pod względem wydajności bazy danych.](./media/sql-database-service-tiers/sqldb_service_tier_monitoring.png)

Można również skonfigurować alerty dotyczące metryk wydajności hello. Kliknij przycisk hello **Dodaj alert** przycisku na powitania **Metryka** okna. Wykonaj tooconfigure kreatora hello alertu. Masz hello tooalert opcji, jeśli hello metryki przekroczą określony próg lub hello spadną poniżej określonego progu.

Na przykład jeśli obciążenie hello na toogrow Twojej bazy danych, możesz tooconfigure alerty w wiadomościach e-mail zawsze, gdy baza danych osiągnie 80% na żadnym z hello metryki wydajności. Możesz użyć tego jako wczesne ostrzeżenie toofigure się, gdy masz tooswitch toohello dalej wyższego poziomu wydajności.

metryki wydajności Hello pomaga ustalić, czy jest możliwe toodowngrade tooa niższego poziomu wydajności. Załóżmy, w przypadku korzystania z bazy danych standardowa S2 i wszystkie Pokaż metryki wydajności średnio hello bazy danych nie używa więcej niż 10% w danym momencie. Prawdopodobnie hello bazy danych będzie działać poprawnie w standardowa S1. Należy jednak pamiętać o obciążeń, które chwilowo wzrastają lub zmieniają się przed dokonaniem hello decyzji toomove tooa niższego poziomu wydajności.

## <a name="monitor-databases-using-dmvs"></a>Monitorowanie baz danych przy użyciu widoków DMV
Witaj same metryki, które są widoczne w portalu hello są również dostępne za pośrednictwem widoków systemowych: [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx) w hello logicznej **wzorca** bazy danych serwera, i [sys.dm_db_ resource_stats](https://msdn.microsoft.com/library/dn800981.aspx) hello bazy danych użytkowników. Użyj **sys.resource_stats** Jeśli potrzebujesz toomonitor mniej szczegółowe dane przez dłuższy okres czasu. Użyj **sys.dm_db_resource_stats** Jeśli potrzebujesz toomonitor bardziej szczegółowe dane w mniejszych odcinkach czasu. Aby uzyskać więcej informacji, zobacz [wytyczne dotyczące wydajności usługi Azure SQL Database](sql-database-single-database-monitor.md#monitor-resource-use)

> [!NOTE]
> Widok **sys.dm_db_resource_stats** zwraca pusty zestaw wyników w przypadku używania baz danych w wersjach Web i Business, które zostały wycofane.
>
>

### <a name="monitor-resource-use"></a>Monitorowanie użycia zasobów

Można monitorować przy użyciu użycia zasobów [Insight wydajności kwerendy bazy danych SQL](sql-database-query-performance.md) i [magazyn zapytań](https://msdn.microsoft.com/library/dn817826.aspx).

Można również monitorować za pomocą tych dwóch widoków użycia:

* [sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx)
* [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx)

#### <a name="sysdmdbresourcestats"></a>sys.dm_db_resource_stats
Można użyć hello [sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx) widoku w każdej bazie danych SQL. Witaj **sys.dm_db_resource_stats** widok pokazuje ostatnie warstwy usług względną toohello danych zasobów użycia. Średni procent dla procesora CPU, dane We/Wy zapisu dziennika i pamięci są rejestrowane co 15 sekund i mają być przechowywane przez godzinę.

Ponieważ ten widok udostępnia szczegółowe przyjrzeć się wykorzystania zasobów, użyj **sys.dm_db_resource_stats** pierwszego dla analizy bieżący stan lub rozwiązywania problemów. Na przykład to zapytanie zawiera hello średnia i maksymalna zasobów przy użyciu hello bieżącej bazy danych za pośrednictwem hello ostatniej godziny:

    SELECT  
        AVG(avg_cpu_percent) AS 'Average CPU use in percent',
        MAX(avg_cpu_percent) AS 'Maximum CPU use in percent',
        AVG(avg_data_io_percent) AS 'Average data I/O in percent',
        MAX(avg_data_io_percent) AS 'Maximum data I/O in percent',
        AVG(avg_log_write_percent) AS 'Average log write use in percent',
        MAX(avg_log_write_percent) AS 'Maximum log write use in percent',
        AVG(avg_memory_usage_percent) AS 'Average memory use in percent',
        MAX(avg_memory_usage_percent) AS 'Maximum memory use in percent'
    FROM sys.dm_db_resource_stats;  

Dla innych zapytań, zobacz przykłady hello w [sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx).

#### <a name="sysresourcestats"></a>sys.resource_stats
Witaj [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx) widoku w hello **wzorca** bazy danych zawiera dodatkowe informacje, które pomaga monitorować wydajność hello na jego określonej usługi warstwę i poziom wydajności bazy danych SQL . Hello dane są zbierane, co 5 minut, a także jest obsługiwany przez około 35 dni. Ten widok jest przydatna do długoterminowego historycznej analizy używaniu zasobów bazy danych SQL.

Witaj Wykres ukazuje hello użycia zasobów procesora CPU dla bazy danych — warstwa Premium z hello P2 poziom wydajności dla każdej godziny w tygodniu. Ten wykres rozpoczyna się w poniedziałek, pokazuje 5 dni roboczych i następnie przedstawiono weekendy, w przypadku znacznie mniej w aplikacji hello.

![Wykorzystanie zasobów bazy danych SQL](./media/sql-database-performance-guidance/sql_db_resource_utilization.png)

Z danych hello ta baza danych ma obecnie szczytowego obciążenia procesora CPU około 50 procent względną toohello P2 poziom wydajności (południe wtorek) użycie procesora CPU. Jeśli procesora CPU jest czynnikiem dominującą hello profilu zasobów aplikacji hello, następnie można zdecydować, czy P2 jest hello prawo dopasowanie tooguarantee poziomu wydajności, która zawsze hello obciążenia. Jeśli toogrow aplikacji w czasie, jest dobrym rozwiązaniem toohave buforu dodatkowym zasobem tak, aby aplikacja hello nigdy nie osiągnięto limitu hello poziom wydajności liczby. Jeśli zwiększysz hello poziom wydajności, może pomóc uniknąć błędów widoczne klienta, które mogą wystąpić, gdy baza danych nie ma wystarczającej liczby żądań tooprocess power skutecznie, szczególnie w środowiskach wrażliwy na opóźnienia. Przykładem jest bazy danych, która obsługuje aplikację, która umożliwia malowanie stron sieci Web na podstawie wyników hello wywołań bazy danych.

Inne typy aplikacji może zinterpretować hello sam wykres inaczej. Na przykład jeśli aplikacja próbuje danych Lista płac tooprocess każdego dnia i ma hello tego samego wykresu, tego rodzaju modelu "zadania wsadowego" może poradzić na poziom wydajności P1. Hello poziom wydajności P1 ma 100 Dtu too200 Dtu porównaniu hello P2 poziom wydajności. Witaj poziom wydajności P1 zapewnia połowa wydajność hello hello P2 poziom wydajności. Tak 50 procent użycia procesora CPU w P2 jest równy 100 procent użycia procesora CPU w P1. Jeśli aplikacja hello nie ma przekroczeń limitu czasu, jego może niezależnie od tego, jeśli zadanie ma 2 godziny lub toofinish 2,5 godziny, jeżeli pobiera dzisiaj. Prawdopodobnie aplikacji w tej kategorii można użyć poziomu wydajności P1. Można korzystać z hello fakt, że są okresach, podczas gdy wykorzystanie zasobów jest starsza, tak, aby wszelkie "big szczytu" może być zostaną przeniesione za pośrednictwem do jednego z koryta hello później w ciągu dnia hello dzień hello. Witaj poziom wydajności P1 może być dobrym dla tego typu aplikacji (i Zapisz pieniędzy), tak długo, jak zakończyć zadania hello na czas każdego dnia.

Informacje o zasobie dla każdej bazy danych dla aktywnej w hello używane ujawnia bazy danych SQL Azure **sys.resource_stats** widoku hello **wzorca** bazy danych w każdym serwerze. Witaj w tabeli hello są agregowane dla 5-minutowy. Z hello podstawowa, standardowa i Premium warstwy usług, hello danych może być więcej niż 5 minut tooappear tabeli hello, tak aby bardziej użyteczna w przypadku historycznej analizy, a nie w pobliżu czasie rzeczywistym analizy danych. Zapytanie hello **sys.resource_stats** widoku toosee hello niedawną historię bazy danych i toovalidate czy hello rezerwacji została wybrana opcja dostarczyć wydajności hello ma w razie potrzeby.

> [!NOTE]
> Musi być połączony toohello **wzorca** bazy danych logicznych tooquery serwera bazy danych SQL **sys.resource_stats** w hello następujące przykłady.
> 
> 

Ten przykład przedstawia, jak jest uwidaczniany hello danych w tym widoku:

    SELECT TOP 10 *
    FROM sys.resource_stats
    WHERE database_name = 'resource1'
    ORDER BY start_time DESC

![widoku wykazu sys.resource_stats Hello](./media/sql-database-performance-guidance/sys_resource_stats.png)

Witaj dalej przykładzie przedstawiono różne sposoby, w których można używać hello **sys.resource_stats** widoku tooget informacji o używaniu zasobów w bazie danych SQL w katalogu:

1. toolook na powitania po tygodniu zasobów dla hello userdb1 bazy danych, można uruchomić tego zapytania:
   
        SELECT *
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND
              start_time > DATEADD(day, -7, GETDATE())
        ORDER BY start_time DESC;
2. jak dobrze obciążenie pasuje do poziomu wydajności hello tooevaluate, należy toodrill w dół do każdego aspektu hello zasobu metryki: procesora CPU, odczyty zapisy, liczbę procesów roboczych i liczba sesji. Oto poprawione zapytań przy użyciu **sys.resource_stats** tooreport hello średniego i maksymalnego wartości tych metryk zasobów:
   
        SELECT
            avg(avg_cpu_percent) AS 'Average CPU use in percent',
            max(avg_cpu_percent) AS 'Maximum CPU use in percent',
            avg(avg_data_io_percent) AS 'Average physical data I/O use in percent',
            max(avg_data_io_percent) AS 'Maximum physical data I/O use in percent',
            avg(avg_log_write_percent) AS 'Average log write use in percent',
            max(avg_log_write_percent) AS 'Maximum log write use in percent',
            avg(max_session_percent) AS 'Average % of sessions',
            max(max_session_percent) AS 'Maximum % of sessions',
            avg(max_worker_percent) AS 'Average % of workers',
            max(max_worker_percent) AS 'Maximum % of workers'
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND start_time > DATEADD(day, -7, GETDATE());
3. Dzięki tym informacjom o wartości średnia i maksymalna hello każdego zasobu metryki można ocenić, jak obciążenie pasuje do poziomu wydajności hello wybrana. Zazwyczaj średnie wartości z **sys.resource_stats** zapewniają toouse dobrej linii bazowej, przed hello rozmiar docelowy. Należy go z dysku podstawowego miary. Na przykład być może używasz hello warstwie usług standardowa S2 poziom wydajności. Średnia Hello Użyj wartości procentowe dla procesora CPU i we/wy odczyty i zapisy są poniżej 40 procent, hello średnia liczba procesów roboczych jest poniżej 50 i hello średnią liczbę sesji jest poniżej 200. Obciążenie może pasuje do hello poziomie wydajności S1. Jest łatwy toosee czy bazy danych mieści się w hello procesu roboczego i limity sesji. czy bazy danych jest dopasowywana do niższej wydajności o zakresie tooCPU, odczyty i zapisy, toosee Podziel hello niższego poziomu wydajności liczba jednostek dtu w warstwie hello hello liczbę jednostek dtu w warstwie aktualny poziom wydajności i następnie pomnożenia wyniku hello 100:
   
    **S1 DTU / S2 JEDNOSTEK DTU W WARSTWIE * 100 = 20 / 50 * 100 = 40**
   
    wynik Hello jest hello względną wydajność różnica między hello dwa poziomy wydajności w procentach. Jeśli Twoje użycie zasobów nie przekracza tę wartość, obciążenie może pasuje do hello niższego poziomu wydajności. Jednak muszą toolook na wszystkie zakresy wartości użycia zasobów, a określenia wartości procentowej, jak często obciążenie bazy danych mieści się w hello niższego poziomu wydajności. Witaj następujące zapytanie wyświetla się, że hello Dopasuj procent na wymiarze zasobów na powitania progu 40 procent, możemy obliczona w tym przykładzie:
   
        SELECT
            (COUNT(database_name) - SUM(CASE WHEN avg_cpu_percent >= 40 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'CPU Fit Percent'
            ,(COUNT(database_name) - SUM(CASE WHEN avg_log_write_percent >= 40 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Log Write Fit Percent'
            ,(COUNT(database_name) - SUM(CASE WHEN avg_data_io_percent >= 40 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Physical Data IO Fit Percent'
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND start_time > DATEADD(day, -7, GETDATE());
   
    Oparty na celu poziomu usługi (SLO) bazy danych, można zdecydować, czy obciążenie jest dopasowywana do hello niższego poziomu wydajności. Jeśli SLO obciążenie bazy danych jest 99,9 procent hello poprzedniego zapytanie zwraca wartości większe niż 99,9% dla wszystkich wymiarów zasobów, obciążenie może pasuje do hello niższego poziomu wydajności.
   
    Spojrzenie na powitania Dopasuj procent daje również wgląd w Określa, czy należy przenieść toohello dalej wyższej wydajności poziomu toomeet Twojego SLO. Na przykład userdb1 przedstawia powitania po użycia procesora CPU dla hello zeszłym tygodniu:
   
   | Średni procent procesora CPU | Maksymalny procent procesora CPU |
   | --- | --- |
   | 24.5 |100.00 |
   
    średnie wykorzystanie Procesora Hello jest o kwartału hello limit hello poziom wydajności, który będzie pasują do poziomu wydajności hello hello bazy danych. Jednak wartość maksymalna hello pokazuje hello bazy danych osiągnie limit hello hello poziomu wydajności. Potrzebujesz toomove toohello dalej wyższego poziomu wydajności? Zobacz, jak wiele razy z osiągnie obciążenia 100 procent, a następnie porównaj jej obciążenie bazy danych tooyour SLO.
   
        SELECT
        (COUNT(database_name) - SUM(CASE WHEN avg_cpu_percent >= 100 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'CPU fit percent'
        ,(COUNT(database_name) - SUM(CASE WHEN avg_log_write_percent >= 100 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Log write fit percent'
        ,(COUNT(database_name) - SUM(CASE WHEN avg_data_io_percent >= 100 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Physical data I/O fit percent'
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND start_time > DATEADD(day, -7, GETDATE());
   
    Jeśli ta kwerenda zwraca wartość mniej niż 99,9% dla każdego hello trzech wymiarów zasobu, należy wziąć pod uwagę albo przenoszenie toohello dalej wyższego poziomu wydajności lub użyj Dostrajanie aplikacji techniki tooreduce hello obciążenia na powitania bazy danych SQL.
4. Tego ćwiczenia również uwzględnia Twojej planowane obciążenie wzrost hello przyszłych.

Dla pul elastycznych można monitorować pojedyncze bazy danych w puli hello hello techniki opisane w tej sekcji. Ale można również monitorować pulę hello jako całość. Informacje na ten temat znajdziesz w artykule [Monitor and manage an elastic pool](sql-database-elastic-pool-manage-portal.md) (Monitorowanie puli elastycznej i zarządzanie nią).


### <a name="maximum-concurrent-requests"></a>Maksymalna liczba równoczesnych żądań
toosee hello liczbę jednoczesnych żądań, uruchom to zapytanie języka Transact-SQL w bazie danych SQL:

    SELECT COUNT(*) AS [Concurrent_Requests]
    FROM sys.dm_exec_requests R

tooanalyze hello obciążenia lokalnej bazy danych SQL Server, zmodyfikuj ten toofilter zapytania na powitania określonej bazy danych ma tooanalyze. Na przykład jeśli masz lokalną bazą danych o nazwie mojabazadanych tego zapytania języka Transact-SQL zwraca hello liczbę jednoczesnych żądań w tej bazie danych:

    SELECT COUNT(*) AS [Concurrent_Requests]
    FROM sys.dm_exec_requests R
    INNER JOIN sys.databases D ON D.database_id = R.database_id
    AND D.name = 'MyDatabase'

To właśnie migawki w jednym punkcie w czasie. tooget lepiej zrozumieć obciążenia i wymagania równoczesnych żądań, będziesz potrzebować toocollect wiele próbek w czasie.

### <a name="maximum-concurrent-logins"></a>Maksymalna równoczesnych logowania
Można analizować sieci użytkownika i aplikacji wzorce tooget wyobrażenie o częstotliwości hello logowania. Można również uruchomić rzeczywistych obciążeń w toomake środowiska testowego się upewnić, że użytkownik jest nie naciśnięcie to lub inne ograniczenia, które omówiono w tym artykule. Nie ma jednego zapytania lub widoku dynamicznego zarządzania (DMV), który można wyświetlić równoczesnych się, że liczba logowania lub historii.

Użycie wielu klientom Witaj tych samych parametrach połączenia hello usługa uwierzytelnia każdego logowania. Jeśli 10 użytkowników jednocześnie połączyć hello tooa bazy danych, przy użyciu tej samej nazwy użytkownika i hasła, będzie 10 równoczesnych logowania. Ten limit dotyczy tylko toohello czas trwania hello logowania i uwierzytelniania. Hello tego samego 10 użytkowników połączyć toohello bazy danych po kolei, hello liczba równoczesnych logowań nigdy nie będzie większa niż 1.

> [!NOTE]
> Obecnie ten limit nie ma zastosowania toodatabases w pule elastyczne.
> 
> 

### <a name="maximum-sessions"></a>Maksymalna liczba sesji
Bieżące aktywne sesje, liczba hello toosee wykonania tego zapytania języka Transact-SQL w bazie danych SQL:

    SELECT COUNT(*) AS [Sessions]
    FROM sys.dm_exec_connections

Jeśli czasie analizowania lokalnymi obciążenie serwera SQL, zmodyfikuj toofocus zapytania hello na określonej bazy danych. To zapytanie ułatwia określenie sesji możliwych potrzeb hello bazy danych, planując przeniesieniem tooAzure bazy danych SQL.

    SELECT COUNT(*)  AS [Sessions]
    FROM sys.dm_exec_connections C
    INNER JOIN sys.dm_exec_sessions S ON (S.session_id = C.session_id)
    INNER JOIN sys.databases D ON (D.database_id = S.database_id)
    WHERE D.name = 'MyDatabase'

Ponownie tych zapytań Zwróć liczba punktu w czasie. W przypadku zebrania wielu próbkach wraz z upływem czasu, będziesz mieć hello jest opis najlepszych sesji, użyj.

Analizy bazy danych SQL można uzyskać statystyki historycznych na sesji badając hello [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx) widoku i przeglądanie hello **active_session_count** kolumny. 
