---
title: aaaGetting wprowadzenie do synchronizacji danych SQL Azure (wersja zapoznawcza) | Dokumentacja firmy Microsoft
description: "Ten samouczek ułatwia szybkie wprowadzenie do synchronizacji danych SQL Azure (wersja zapoznawcza)."
services: sql-database
documentationcenter: 
author: douglaslms
manager: craigg
editor: 
ms.assetid: a295a768-7ff2-4a86-a253-0090281c8efa
ms.service: sql-database
ms.custom: load & move data
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: douglasl
ms.openlocfilehash: 666d09237e42acc23ae3c8c81e60734a413f5949
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-sql-data-sync-preview"></a>Wprowadzenie do synchronizacji danych Azure SQL (wersja zapoznawcza)
Z tego samouczka dowiesz się, jak tooset się synchronizacja danych SQL Azure, tworząc grupy synchronizacji hybrydowych, który zawiera zarówno usługi Azure SQL Database i programu SQL Server wystąpienia. Nowa grupa synchronizacji Hello jest w pełni skonfigurowane i synchronizuje zgodnie z harmonogramem hello, które można ustawić.

W tym samouczku założono, że co najmniej pewne doświadczenie z bazy danych SQL i programu SQL Server. 

Omówienie synchronizacji danych SQL, zobacz [synchronizowanie danych](sql-database-sync-data.md).

Aby uzyskać pełną przykłady z programu PowerShell, które zawierają tooconfigure synchronizacji danych SQL, zobacz temat hello następujące artykuły:
-   [Użyj programu PowerShell toosync między wiele baz danych Azure SQL](scripts/sql-database-sync-data-between-sql-databases.md)
-   [Użyj programu PowerShell toosync między bazą danych SQL Azure i lokalnej bazy danych programu SQL Server](scripts/sql-database-sync-data-between-azure-onprem.md)

> [!NOTE]
> Hello pełną dokumentację techniczną dla synchronizacji danych SQL Azure, wcześniej znajdowały się w witrynie MSDN, jest dostępna jako. Dokument PDF. Pobierz go [tutaj](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true).

## <a name="step-1---create-sync-group"></a>Krok 1 — Tworzenie grupy synchronizacji

### <a name="locate-hello-data-sync-settings"></a>Zlokalizuj hello ustawienia synchronizacji danych

1.  W przeglądarce Przejdź toohello portalu Azure.

2.  W portalu hello zlokalizować bazy danych SQL z pulpitu nawigacyjnego lub ikonę bazy danych SQL hello na powitania narzędzi.

    ![Lista baz danych Azure SQL](media/sql-database-get-started-sql-data-sync/datasync-preview-sqldbs.png)

3.  Na powitania **baz danych SQL** bloku, wybierz hello istniejącej bazy danych SQL, które mają toouse jako otwiera hello Centrum bazy danych synchronizacji danych. blok bazy danych SQL o hello.

4.  W bloku bazy danych SQL hello hello wybranej bazy danych, wybierz **synchronizować bazy danych tooother**. zostanie otwarty blok synchronizacji danych Hello.

    ![Opcja bazy danych tooother synchronizacji](media/sql-database-get-started-sql-data-sync/datasync-preview-newsyncgroup.png)

### <a name="create-a-new-sync-group"></a>Utwórz nową grupę synchronizacji

1.  W bloku synchronizacji danych hello, wybierz **nowej grupy synchronizacji**. Witaj **nowej grupy synchronizacji** z kroku 1, zostanie otwarty blok **Utwórz grupę synchronizacji**, zaznaczony. Witaj **Tworzenie grupy synchronizacji danych** również zostanie otwarty blok.

2.  Na powitania **Tworzenie grupy synchronizacji danych** bloku hello następujących czynności:

    1.  W hello **nazwy grupy synchronizacji** wprowadź nazwę nowej grupy synchronizacji hello.

    2.  W hello **bazy danych usługi synchronizacji metadanych** wybierz, czy toocreate nową bazę danych (zalecane) lub toouse istniejącej bazy danych.

        > [!NOTE]
        > Firma Microsoft zaleca utworzenie toouse nową, pustą bazę danych, jak hello synchronizacji bazy danych metadanych. Synchronizacja danych tworzy tabele w tej bazie danych i uruchamia częste obciążenia. Ta baza danych jest automatycznie udostępniony jako hello synchronizacji bazy danych metadanych dla wszystkich grup synchronizacji w wybranym regionie hello. Nie można zmienić hello bazy danych usługi synchronizacji metadanych, jego nazwa lub jego poziom usługi bez usuwania go.

        Jeśli została wybrana opcja **nową bazę danych**, wybierz pozycję **Utwórz nową bazę danych.** Witaj **bazy danych SQL** zostanie otwarty blok. Na powitania **bazy danych SQL** bloku, nazwy i skonfigurować hello nowej bazy danych. Następnie wybierz **OK**.

        Jeśli została wybrana opcja **Użyj istniejącej bazy danych**, wybierz pozycję hello bazy danych, z listy hello.

    3.  W hello **synchronizacji automatycznej** najpierw wybierz **na** lub **poza**.

        Jeśli została wybrana opcja **na**, w hello **częstotliwości synchronizacji** , wprowadź liczbę z zakresu a następnie wybierz opcję sekundy, minuty, godziny lub dni.

        ![Określ częstotliwość synchronizacji](media/sql-database-get-started-sql-data-sync/datasync-preview-syncfreq.png)

    4.  W hello **rozwiązywania konfliktów** wybierz "Centrum wins" lub "Elementu członkowskiego wins".

        ![Określ, jak są rozwiązywane konflikty](media/sql-database-get-started-sql-data-sync/datasync-preview-conflictres.png)

    5.  Wybierz **OK** i poczekaj, aż hello nowe synchronizacji grupy toobe utworzeniu i wdrożeniu.

## <a name="step-2---add-sync-members"></a>Krok 2 — Dodawanie członków synchronizacji

Po utworzeniu i wdrożeniu, krok 2 hello nowej grupy synchronizacji **dodawać członków synchronizacji**, zostało wyróżnione hello **nowej grupy synchronizacji** bloku.

W hello **bazy danych Centrum** wprowadź hello istniejących poświadczeń dla hello serwera bazy danych SQL, na którym hello znajduje się baza danych Centrum. Nie wprowadzaj *nowe* poświadczeń w tej sekcji.

![Koncentrator bazy danych został dodany toosync grupy](media/sql-database-get-started-sql-data-sync/datasync-preview-hubadded.png)

## <a name="add-an-azure-sql-database"></a>Dodaj bazę danych Azure SQL

W hello **bazy danych elementów członkowskich** sekcji i opcjonalnie Dodaj grupy synchronizacji toohello bazy danych SQL Azure, wybierając **dodać bazy danych Azure**. Witaj **Konfigurowanie bazy danych Azure** zostanie otwarty blok.

Na powitania **Konfigurowanie bazy danych Azure** bloku hello następujących czynności:

1.  W hello **nazwa elementu członkowskiego synchronizacji** Podaj nazwę nowego członka synchronizacji hello. Ta nazwa różni się od nazwy hello hello bazy danych.

2.  W hello **subskrypcji** hello wybierz opcję skojarzona subskrypcja platformy Azure na potrzeby rozliczeń.

3.  W hello **Azure SQL Server** hello wybierz opcję istniejącego serwera baz danych SQL.

4.  W hello **bazy danych SQL Azure** hello wybierz opcję istniejąca baza danych SQL.

5.  W hello **kierunki synchronizacji** wybierz synchronizacji dwukierunkowe, toohello koncentratora, lub z hello koncentratora.

    ![Dodawanie nowego elementu członkowskiego synchronizacji bazy danych SQL](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadding.png)

6.  W hello **Username** i **hasło** wprowadź hello istniejących poświadczeń dla hello serwera bazy danych SQL, na które hello znajduje się bazy danych elementów członkowskich. Nie wprowadzaj *nowe* poświadczeń w tej sekcji.

7.  Wybierz **OK** i poczekaj, aż hello nowe synchronizacji członek toobe utworzeniu i wdrożeniu.

    ![Dodano nowy element członkowski synchronizacji bazy danych SQL](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadded.png)

## <a name="add-an-on-premises-sql-server-database"></a>Dodaj lokalną bazą danych programu SQL Server

W hello **bazy danych elementów członkowskich** sekcji i opcjonalnie Dodaj grupy synchronizacji toohello lokalnego programu SQL Server, wybierając **Dodaj bazę danych z lokalnego**. Witaj **Konfigurowanie lokalnego** zostanie otwarty blok.

Na powitania **Konfigurowanie lokalnego** bloku hello następujących czynności:

1.  Wybierz **hello wybierz bramy agenta synchronizacji**. Witaj **Agent synchronizacji wybierz** zostanie otwarty blok.

    ![Wybierz bramę agent synchronizacji hello](media/sql-database-get-started-sql-data-sync/datasync-preview-choosegateway.png)

2.  Na powitania **hello wybierz bramy agenta synchronizacji** bloku, wybierz czy toouse istniejącego agenta lub Utwórz nowy agent.

    Jeśli została wybrana opcja **agentów istniejące**, wybierz hello istniejącego agenta z listy hello.

    Jeśli została wybrana opcja **Utwórz nowy agent**, hello następujących czynności:

    1.  Pobierz oprogramowanie agenta do powitania klienta synchronizacji z łączem hello i zainstaluj go na komputerze hello, w którym znajduje się hello programu SQL Server.
 
        > [!IMPORTANT]
        > Masz tooopen wychodzący port TCP 1433 w agenta hello zapory toolet powitania klienta komunikacji z serwerem hello.


    2.  Wprowadź nazwę dla agenta hello.

    3.  Wybierz **tworzenie i generowanie klucza**.

    4.  Kopiuj hello agenta klucza toohello Schowka.
        
        ![Tworzenie nowego agenta synchronizacji](media/sql-database-get-started-sql-data-sync/datasync-preview-selectsyncagent.png)

    5.  Wybierz **OK** tooclose hello **Agent synchronizacji wybierz** bloku.

    6.  Na komputerze serwera SQL hello Znajdź i uruchom aplikację klienta synchronizacji agenta hello.

        ![dane Hello synchronizacji aplikacji agenta klienta](media/sql-database-get-started-sql-data-sync/datasync-preview-clientagent.png)

    7.  W aplikacji agenta synchronizacji hello, wybierz **przesłać klucz agenta**. Witaj **synchronizacji metadanych bazy danych konfiguracji** zostanie otwarte okno dialogowe.

    8.  W hello **synchronizacji metadanych bazy danych konfiguracji** okno dialogowe, Wklej hello agenta klucza skopiowany z hello portalu Azure. Udostępniają hello istniejących poświadczeń dla serwera bazy danych SQL Azure hello, na które hello znajduje się bazy danych metadanych. (Jeśli została utworzona nowa baza danych metadanych, ta baza danych znajduje się na powitania tym samym serwerze co baza danych Centrum hello.) Wybierz **OK** i poczekaj, aż hello toofinish konfiguracji.

        ![Wprowadź poświadczenia agenta hello klucza i serwera](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-enterkey.png)

        >   [!NOTE] 
        >   Jeśli w tym momencie zostanie wyświetlony błąd zapory, należy toocreate reguły zapory na ruch przychodzący Azure tooallow z komputera z programem SQL Server hello. Witaj regułę można utworzyć ręcznie w portalu hello, ale może być łatwiejsze toocreate go w programu SQL Server Management Studio (SSMS). W programie SSMS spróbuj tooconnect toohello centrum danych na platformie Azure. Wpisz jej nazwę jako \<hub_database_name\>. database.windows.net. Wykonaj kroki hello hello okna dialogowego pole tooconfigure hello Azure reguła. Następnie wróć toohello aplikacji agenta klienta synchronizacji.

    9.  W aplikacji agenta klienta synchronizacji powitania kliknij **zarejestrować** tooregister bazy danych programu SQL Server z agentem hello. Witaj **konfiguracji serwera SQL** zostanie otwarte okno dialogowe.

        ![Dodaj i skonfiguruj bazę danych programu SQL Server](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-adddb.png)

    10. W hello **konfiguracji serwera SQL** oknie dialogowym wybierz czy tooconnect przy użyciu uwierzytelniania programu SQL Server lub uwierzytelniania systemu Windows. Jeśli wybrano opcję uwierzytelniania programu SQL Server, wprowadź hello istniejących poświadczeń. Podaj nazwę programu SQL Server hello oraz nazwę hello hello bazy danych o tym, że chcesz toosync. Wybierz **połączenie testowe** tootest ustawień. Następnie wybierz **zapisać**. liście hello pojawi się Hello zarejestrowany w bazie danych.

        ![Baza danych SQL Server zostanie zarejestrowany](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-dbadded.png)

    11. Można teraz zamknąć hello aplikacji agenta klienta synchronizacji.

    12. W portalu hello na powitania **Konfigurowanie lokalnego** bloku, wybierz opcję **wybierz hello bazy danych.** Witaj **wybierz bazę danych** zostanie otwarty blok.

    13. Na powitania **wybierz bazę danych** bloku w hello **nazwa elementu członkowskiego synchronizacji** Podaj nazwę nowego członka synchronizacji hello. Ta nazwa różni się od nazwy hello hello bazy danych. Wybierz bazę danych hello z listy hello. W hello **kierunki synchronizacji** wybierz synchronizacji dwukierunkowe, toohello koncentratora, lub z hello koncentratora.

        ![Wybierz hello w lokalnej bazie danych](media/sql-database-get-started-sql-data-sync/datasync-preview-selectdb.png)

    14. Wybierz **OK** tooclose hello **wybierz bazę danych** bloku. Następnie wybierz **OK** tooclose hello **Konfigurowanie lokalnego** bloku i poczekaj hello synchronizacji nowego elementu członkowskiego toobe utworzeniu i wdrożeniu. Na koniec kliknij **OK** tooclose hello **Wybierz członków synchronizacji** bloku.

        ![W lokalnej bazie danych dodano grupę toosync](media/sql-database-get-started-sql-data-sync/datasync-preview-onpremadded.png)

3.  tooSQL tooconnect synchronizacji danych i hello lokalnego agenta, Dodaj toohello nazwa rola `DataSync_Executor`. Synchronizacja danych tworzy tę rolę w wystąpieniu programu SQL Server hello.

## <a name="step-3---configure-sync-group"></a>Krok 3 — Konfigurowanie synchronizacji grupy

Po hello nowych członków grupy synchronizacji są tworzone i wdrażane, krok 3 **Konfigurowanie synchronizacji grupy**, zostało wyróżnione hello **nowej grupy synchronizacji** bloku.

1.  Na powitania **tabel** bloku, wybierz bazę danych z listy hello synchronizacji członków grupy, a następnie wybierz **schematu odświeżania**.

2.  Zaznacz hello tabel, które mają toosync hello listę dostępnych tabel.

    ![Wybierz tabele toosync](media/sql-database-get-started-sql-data-sync/datasync-preview-tables.png)

3.  Domyślnie wybrane są wszystkie kolumny w tabeli hello. Jeśli nie chcesz toosync wszystkie kolumny hello, wyłącz wyboru hello hello kolumn, że nie chcesz toosync. Upewnij się kolumna klucza podstawowego hello tooleave zaznaczone.

    ![Wybierz pola toosync](media/sql-database-get-started-sql-data-sync/datasync-preview-tables2.png)

4.  Na koniec wybierz **zapisać**.

## <a name="next-steps"></a>Następne kroki
Gratulacje. Utworzono grupę synchronizacji, która zawiera zarówno wystąpienie bazy danych SQL, jak i bazy danych programu SQL Server.

Aby uzyskać więcej informacji na temat bazy danych SQL i synchronizacji danych SQL zobacz:

-   [Pobierz pełną dokumentację techniczną hello synchronizacji danych SQL](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true)
-   [Pobierz hello dokumentacji interfejsu API REST synchronizacji danych SQL](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_REST_API.pdf?raw=true)
-   [Omówienie bazy danych SQL](sql-database-technical-overview.md)
-   [Zarządzanie cyklem życia bazy danych](https://msdn.microsoft.com/library/jj907294.aspx)
