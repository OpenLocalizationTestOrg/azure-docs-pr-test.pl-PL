---
title: "aaaReport dla baz danych chmury skalowalnych w poziomie (poziomy podziału) | Dokumentacja firmy Microsoft"
description: "jak toouse cross zapytań bazy danych dla bazy danych"
services: sql-database
documentationcenter: 
manager: jhubbard
author: MladjoA
ms.assetid: c81ef5e3-41e9-4fd2-8631-868f2e168147
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: mlandzic
ms.openlocfilehash: e34f398f8d408cffd91a70fc2cfbda73daec3550
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="report-across-scaled-out-cloud-databases-preview"></a>Raport w chmurze skalowalnych w poziomie bazy danych (wersja zapoznawcza)
Możesz utworzyć raporty z wielu baz danych Azure SQL z punktu pojedynczego połączenia przy użyciu [elastycznej zapytania](sql-database-elastic-query-overview.md). Hello bazy danych musi być podzielony w poziomie, (określane również jako "podzielonej").

Jeśli masz istniejącą bazę danych, zobacz [Migrowanie istniejącej bazy danych bazy danych poza tooscaled](sql-database-elastic-convert-to-use-elastic-tools.md).

obiekty SQL hello toounderstand potrzebne tooquery, zobacz [zapytanie na poziomie partycjonowanej baz danych](sql-database-elastic-query-horizontal-partitioning.md).

## <a name="prerequisites"></a>Wymagania wstępne
Pobierz i uruchom hello [wprowadzenie próbki narzędzi elastycznej bazy danych](sql-database-elastic-scale-get-started.md).

## <a name="create-a-shard-map-manager-using-hello-sample-app"></a>Tworzenie mapy niezależnego fragmentu manager za pomocą hello przykładowej aplikacji
W tym miejscu spowoduje utworzenie mapy niezależnego fragmentu manager oraz kilka fragmentów, następuje wstawiania danych do odłamków hello. W przypadku tooalready skonfigurowano fragmentów danych podzielonej w nich, można pominąć hello następujące kroki i przenieść toohello następnej sekcji.

1. Tworzenie i uruchamianie hello **wprowadzenie do korzystania z narzędzi elastycznej bazy danych** przykładowej aplikacji. Wykonaj kroki hello aż do kroku 7 w sekcji hello [pobieranie i uruchamianie aplikacji przykładowej hello](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app). Na końcu hello kroku 7 zostanie wyświetlony hello następującego wiersza polecenia:

    ![Wiersz polecenia][1]
2. W oknie polecenia hello, wpisz "1", a następnie naciśnij klawisz **Enter**. Tworzy menedżera map niezależnego fragmentu hello i dodaje dwa niezależne toohello serwera. Następnie wpisz "3" i naciśnij klawisz **Enter**; powtórzenie akcji hello cztery razy. Wstawia Przykładowe wiersze danych z fragmentów.
3. Witaj [portalu Azure](https://portal.azure.com) powinny być widoczne trzech nowych baz danych na serwerze:

   ![Visual Studio potwierdzenia][2]

   W tym momencie między bazami danych zapytania są obsługiwane za pomocą biblioteki klienta elastycznej bazy danych hello. Na przykład opcja 4 w oknie polecenia hello. wyniki zapytania wielu niezależnych Hello są zawsze **UNION ALL** hello wyniki wszystkich fragmentów.

   W następnej sekcji hello możemy utworzyć obsługującego bardziej zaawansowane funkcje zapytań hello danych między odłamków punkt końcowy bazy danych przykładowych.

## <a name="create-an-elastic-query-database"></a>Tworzenie elastycznej kwerendy bazy danych
1. Otwórz hello [portalu Azure](https://portal.azure.com) i zaloguj się.
2. Utwórz nową bazę danych Azure SQL w hello tym samym serwerze co konfigurację niezależnego fragmentu. Nazwa bazy danych hello "ElasticDBQuery."

    ![Portalu Azure i warstwę cenową][3]

    > [!NOTE]
    > można użyć istniejącej bazy danych. Jeśli możesz to zrobić, nie może być jeden z fragmentów hello chcieliby tooexecute zapytań na. Ta baza danych będzie służyć do tworzenia hello obiektów metadanych dla zapytania elastycznej bazy danych.
    >

## <a name="create-database-objects"></a>Tworzenie obiektów bazy danych
### <a name="database-scoped-master-key-and-credentials"></a>Klucz główny o zakresie bazy danych i poświadczeń
Są używane tooconnect toohello niezależnego fragmentu mapy manager i odłamków hello:

1. Otwórz program SQL Server Management Studio lub SQL Server Data Tools w programie Visual Studio.
2. Połącz tooElasticDBQuery bazy danych i wykonaj następujące polecenia T-SQL hello:

        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';

        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred
        WITH IDENTITY = '<username>',
        SECRET = '<password>';

    "username" i "password" powinien być hello sam jako informacje logowania używane w kroku 6 [pobieranie i uruchamianie aplikacji przykładowej hello](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app) w [wprowadzenie do korzystania z narzędzi elastycznej bazy danych](sql-database-elastic-scale-get-started.md).

### <a name="external-data-sources"></a>Zewnętrzne źródła danych
toocreate zewnętrznego źródła danych, wykonaj następujące polecenia w bazie danych ElasticDBQuery hello hello:

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH
      (TYPE = SHARD_MAP_MANAGER,
      LOCATION = '<server_name>.database.windows.net',
      DATABASE_NAME = 'ElasticScaleStarterKit_ShardMapManagerDb',
      CREDENTIAL = ElasticDBQueryCred,
       SHARD_MAP_NAME = 'CustomerIDShardMap'
    ) ;

 "CustomerIDShardMap" jest nazwa hello hello niezależnego fragmentu mapy, jeśli utworzono hello niezależnego fragmentu mapy, a następnie mapować niezależnego fragmentu Menedżera przy użyciu hello — przykład narzędzi elastycznej bazy danych. Jednak jeśli używasz niestandardowych ustawień dla tego przykładu, następnie należy hello niezależnego fragmentu mapy wybrana nazwa aplikacji.

### <a name="external-tables"></a>Tabele zewnętrzne
Tworzenie tabeli zewnętrznej zgodny hello tabeli klientów na powitania odłamków, wykonując następujące polecenia w bazie danych ElasticDBQuery hello:

    CREATE EXTERNAL TABLE [dbo].[Customers]
    ( [CustomerId] [int] NOT NULL,
      [Name] [nvarchar](256) NOT NULL,
      [RegionId] [int] NOT NULL)
    WITH
    ( DATA_SOURCE = MyElasticDBQueryDataSrc,
      DISTRIBUTION = SHARDED([CustomerId])
    ) ;

## <a name="execute-a-sample-elastic-database-t-sql-query"></a>Wykonywanie przykładowego zapytania T-SQL elastycznej bazy danych
Po zdefiniowaniu zewnętrznym źródle danych i tabele zewnętrzne mogą teraz używać pełnej T-SQL w tabelach zewnętrznych.

Wykonaj tę kwerendę w bazie danych ElasticDBQuery hello:

    select count(CustomerId) from [dbo].[Customers]

Można zauważyć zapytania hello agreguje wyniki wszystkich odłamków hello i zapewnia hello następujące dane wyjściowe:

![Szczegóły danych wyjściowych][4]

## <a name="import-elastic-database-query-results-tooexcel"></a>Importuj tooExcel wyników zapytania elastycznej bazy danych
 Możesz zaimportować hello wyników z pliku programu Excel tooan zapytania.

1. Uruchom program Excel 2013.
2. Przejdź toohello **danych** wstążki.
3. Kliknij przycisk **z innych źródeł** i kliknij przycisk **z programu SQL Server**.

   ![Importowania z programu Excel z innych źródeł][5]
4. W hello **Kreator połączenia danych** wpisz powitania serwera nazwę i poświadczenia logowania. Następnie kliknij przycisk **Next** (Dalej).
5. W oknie dialogowym hello **hello wybierz bazy danych, która zawiera dane hello**, wybierz pozycję hello **ElasticDBQuery** bazy danych.
6. Wybierz hello **klientów** tabeli w widoku listy hello, a następnie kliknij przycisk **dalej**. Następnie kliknij przycisk **Zakończ**.
7. W hello **i zaimportuj dane** formularza, w obszarze **wybierz sposób tooview tych danych w skoroszycie**, wybierz pozycję **tabeli** i kliknij przycisk **OK**.

Witaj wszystkie wiersze z **klientów** tabeli, przechowywane w różnych odłamków wypełnić hello arkuszu programu Excel.

Możesz teraz użyć funkcji wizualizacji zaawansowanych danych programu Excel. Można użyć ciągu połączenia hello nazwę serwera, nazwa bazy danych i poświadczeń tooconnect BI i dane integracji narzędzia toohello zapytania elastycznej bazy danych. Upewnij się, czy program SQL Server jest obsługiwana jako źródło danych dla własnych narzędzi. Może się odwoływać toohello elastycznej zapytanie do bazy danych i tabel zewnętrznych, podobnie jak wszystkie inne bazy danych programu SQL Server i czy można połączyć toowith własnych narzędzi tabel programu SQL Server.

### <a name="cost"></a>Koszty
Brak bez dodatkowych opłat dla funkcji hello elastycznej kwerendy bazy danych.

Aby uzyskać informacje o cenach zobacz [szczegóły cennika bazy danych SQL](https://azure.microsoft.com/pricing/details/sql-database/).

## <a name="next-steps"></a>Następne kroki

* Omówienie elastycznej zapytania, zobacz [elastycznej zapytań — omówienie](sql-database-elastic-query-overview.md).
* Samouczek partycjonowania pionowego, zobacz [wprowadzenie do korzystania z bazy danych między kwerendy (partycjonowanie pionowe)](sql-database-elastic-query-getting-started-vertical.md).
* Dla zapytań dotyczących danych pionowo podzielonym na partycje i składnię i przykład, zobacz [zapytań w pionie na partycje danych)](sql-database-elastic-query-vertical-partitioning.md)
* Dla zapytań dotyczących danych poziomie podzielonym na partycje i składnię i przykład, zobacz [zapytań w poziomie na partycje danych)](sql-database-elastic-query-horizontal-partitioning.md)
* Zobacz [sp\_wykonania \_zdalnego](https://msdn.microsoft.com/library/mt703714) dla procedury składowanej, która wykonuje instrukcję Transact-SQL w jednym zdalnej bazy danych SQL Azure lub zestaw baz danych, służąc jako odłamków w poziomie schemat partycjonowania.


<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
