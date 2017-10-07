---
title: aaaCopy bazy danych Azure SQL | Dokumentacja firmy Microsoft
description: "Utwórz kopię bazy danych Azure SQL"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 5aaf6bcd-3839-49b5-8c77-cbdf786e359b
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.date: 06/15/2017
ms.author: carlrab
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 64a297d819d6da89600fda60abe8394ae405abfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="copy-an-azure-sql-database"></a>Kopiowanie bazy danych Azure SQL

Baza danych SQL Azure zapewnia kilka metod tworzenia spójna transakcyjnie kopię istniejącej SQL Azure bazy danych na obu hello sam serwer lub inny serwer. Możesz skopiować bazę danych SQL za pomocą hello portalu Azure, programu PowerShell lub T-SQL. 

## <a name="overview"></a>Omówienie

Kopia bazy danych jest migawką hello źródłowej bazy danych od czasu hello hello kopia żądania. Możesz wybrać hello na tym samym serwerze lub inny serwer, jego warstwę i poziom wydajności usługi lub poziomu wydajności różnych w hello tej samej warstwie usług (wydanie). Po zakończeniu kopiowania hello staje się funkcjonalnej, niezależnie od bazy danych. W tym momencie możesz uaktualnić lub obniżyć go tooany edition. Witaj logowania, użytkowników i uprawnienia można zarządzać niezależnie.  

## <a name="logins-in-hello-database-copy"></a>Nazwy logowania w hello kopii bazy danych

Po skopiowaniu toohello baza danych sam serwer logiczny, hello tej samej nazwy logowania może być używany z obiema bazami danych. podmiot, użyj bazy danych hello toocopy zabezpieczeń Hello staje się właścicielem bazy danych hello na powitania nowej bazy danych. Wszyscy użytkownicy bazy danych, ich uprawnienia i ich zabezpieczeń identyfikatorów (SID) są kopiowane toohello kopii bazy danych.  

Podczas kopiowania bazy danych tooa inny serwer logiczny podmiotu na nowym serwerze hello zabezpieczeń hello staje się hello właściciela bazy danych na powitania nowej bazy danych. Jeśli używasz [zawarte bazy danych użytkowników](sql-database-manage-logins.md) dla dostępu do danych, upewnij się, że oba hello głównej i pomocniczej bazy danych zawsze mieć hello tych samych poświadczeń użytkownika, który po kopiowania hello zakończeniu natychmiast mogą uzyskiwać dostęp do za pomocą hello takie same poświadczenia. 

Jeśli używasz [usługi Azure Active Directory](../active-directory/active-directory-whatis.md), można całkowicie wyeliminować potrzebę hello zarządzania poświadczeniami hello kopii w. Jednak podczas kopiowania bazy danych hello tooa nowy serwer hello dostępu opartego na nazwie logowania mogą nie działać, ponieważ hello logowania nie istnieje na nowym serwerze hello. toolearn o zarządzaniu nazwy logowania podczas kopiowania tooa innego serwera logicznego bazy danych, zobacz [jak toomanage Azure SQL bazy zabezpieczeń danych po awarii](sql-database-geo-replication-security-config.md). 

Po kopiowanie hello zakończy się pomyślnie i przed inni użytkownicy są mapowane ponownie hello logowania, który zainicjował hello kopiowania, hello właściciela bazy danych, można zalogować się wyłącznie w toohello nowej bazy danych. Zobacz tooresolve logowania po zakończeniu operacji kopiowania hello [rozwiązać logowania](#resolve-logins).

## <a name="copy-a-database-by-using-hello-azure-portal"></a>Kopiowanie bazy danych przy użyciu hello portalu Azure

toocopy bazy danych przy użyciu hello portalu Azure, otwórz hello strony bazy danych, a następnie kliknij przycisk **kopiowania**. 

   ![Kopiowanie bazy danych](./media/sql-database-copy/database-copy.png)

## <a name="copy-a-database-by-using-powershell"></a>Kopiowanie bazy danych przy użyciu programu PowerShell

toocopy bazy danych przy użyciu programu PowerShell, użyj hello [AzureRmSqlDatabaseCopy nowy](/powershell/module/azurerm.sql/new-azurermsqldatabasecopy) polecenia cmdlet. 

```PowerShell
New-AzureRmSqlDatabaseCopy -ResourceGroupName "myResourceGroup" `
    -ServerName $sourceserver `
    -DatabaseName "MySampleDatabase" `
    -CopyResourceGroupName "myResourceGroup" `
    -CopyServerName $targetserver `
    -CopyDatabaseName "CopyOfMySampleDatabase"
```

Kompletnego przykładowego skryptu, zobacz [skopiuj nowy serwer bazy danych tooa](scripts/sql-database-copy-database-to-new-server-powershell.md).

## <a name="copy-a-database-by-using-transact-sql"></a>Kopiowanie bazy danych przy użyciu języka Transact-SQL

Zaloguj się za toohello wzorca bazy danych z głównego identyfikatora logowania poziomu serwera hello lub logowania hello, utworzony hello bazy danych ma toocopy. Kopiowanie toosucceed bazy danych nazwy logowania, które nie są hello podmiotu zabezpieczeń z poziomu serwera muszą być członkami roli dbmanager: hello. Aby uzyskać więcej informacji na temat logowania i łączenia serwera toohello, zobacz [Zarządzanie logowania](sql-database-manage-logins.md).

Uruchom kopiowanie hello źródłowej bazy danych z hello [CREATE DATABASE](https://msdn.microsoft.com/library/ms176061.aspx) instrukcji. Wykonywanie tej instrukcji inicjuje hello bazy danych, proces kopiowania. Kopiowanie bazy danych jest proces asynchroniczny, przed ukończeniem kopiowania bazy danych hello powoduje zwrócenie hello instrukcji CREATE DATABASE.

### <a name="copy-a-sql-database-toohello-same-server"></a>Skopiuj toohello bazy danych programu SQL server tego samego
Zaloguj się za toohello wzorca bazy danych z głównego identyfikatora logowania poziomu serwera hello lub logowania hello, utworzony hello bazy danych ma toocopy. Kopiowanie toosucceed bazy danych nazwy logowania, które nie są hello podmiotu zabezpieczeń z poziomu serwera muszą być członkami roli dbmanager: hello.

To polecenie powoduje skopiowanie Database1 tooa nową bazę danych o nazwie Database2 na powitania tym samym serwerze. W zależności od wielkości hello bazy danych hello kopiowanie operacja może potrwać niektórych toocomplete czasu.

    -- Execute on hello master database.
    -- Start copying.
    CREATE DATABASE Database1_copy AS COPY OF Database1;

### <a name="copy-a-sql-database-tooa-different-server"></a>Skopiuj inny serwer tooa bazy danych SQL

Zaloguj się za toohello wzorca bazy danych na powitania serwera docelowego, serwer bazy danych SQL hello hello nowej bazy danych w przypadku toobe utworzony. Użyj nazwy logowania, która ma hello jako właściciel bazy danych hello hello źródłowej bazy danych na serwerze bazy danych SQL źródła hello tę samą nazwę i hasło. Witaj logowania na serwerze docelowym hello również musi być członkiem roli dbmanager: hello lub być głównego identyfikatora logowania poziomu serwera hello.

To polecenie powoduje skopiowanie na serwer1 tooa nową bazę danych o nazwie Database2 na serwerze2 Database1. W zależności od wielkości hello bazy danych hello kopiowanie operacja może potrwać niektórych toocomplete czasu.

    -- Execute on hello master database of hello target server (server2)
    -- Start copying from Server1 tooServer2
    CREATE DATABASE Database1_copy AS COPY OF server1.Database1;


### <a name="monitor-hello-progress-of-hello-copying-operation"></a>Monitorować postęp hello hello operacji kopiowania

Monitorowanie procesu kopiowania hello badając hello sys.databases i sys.dm_database_copies widoki. Podczas kopiowania hello jest w toku, hello **state_desc** kolumny widoku sys.databases hello hello nowej bazy danych ustawiono zbyt**kopiowanie**.

* W przypadku niepowodzenia kopiowanie hello hello **state_desc** kolumny widoku sys.databases hello hello nowej bazy danych ustawiono zbyt**PODEJRZEWAĆ**. Wykonaj hello instrukcja DROP na powitania nową bazę danych i spróbuj ponownie później.
* Jeśli kopiowanie hello zakończy się powodzeniem, hello **state_desc** kolumny widoku sys.databases hello hello nowej bazy danych ustawiono zbyt**ONLINE**. Kopiowanie Hello została zakończona i hello Nowa baza danych jest zwykłej bazy danych, które można zmienić niezależnie od hello źródłowej bazy danych.

> [!NOTE]
> Jeśli zdecydujesz się toocancel hello kopiowania, gdy jest w toku, wykonać hello [DROP DATABASE](https://msdn.microsoft.com/library/ms178613.aspx) instrukcji na powitania nowej bazy danych. Alternatywnie wykonywania instrukcji DROP DATABASE hello na powitania źródłowej bazy danych również anuluje hello proces kopiowania.
> 

## <a name="resolve-logins"></a>Rozwiąż logowania

Po hello nowej bazy danych jest w trybie online na serwerze docelowym hello, użyj hello [ALTER USER](https://msdn.microsoft.com/library/ms176060.aspx) instrukcji tooremap hello użytkownikom hello nowych toologins na serwerze docelowym hello bazy danych. tooresolve oddzielona użytkowników, zobacz [Rozwiązywanie problemów z osieroconych użytkowników](https://msdn.microsoft.com/library/ms175475.aspx). Zobacz też [jak toomanage Azure SQL bazy zabezpieczeń danych po awarii](sql-database-geo-replication-security-config.md).

Wszyscy użytkownicy w nowej bazy danych hello zachować uprawnienia hello, które miały w hello źródłowej bazy danych. Witaj użytkownik, który zainicjował hello kopii bazy danych staje się właścicielem bazy danych hello hello nową bazę danych i ma przypisany nowy identyfikator zabezpieczeń (SID). Po kopiowanie hello zakończy się pomyślnie i przed inni użytkownicy są mapowane ponownie hello logowania, który zainicjował hello kopiowania, hello właściciela bazy danych, można zalogować się wyłącznie w toohello nowej bazy danych.

toolearn dotyczące zarządzania użytkownikami i logowania do kopiowania tooa innego serwera logicznego bazy danych, zobacz [jak toomanage Azure SQL bazy zabezpieczeń danych po awarii](sql-database-geo-replication-security-config.md).

## <a name="next-steps"></a>Następne kroki

* Aby uzyskać informacje dotyczące logowania, zobacz [Zarządzanie logowania do](sql-database-manage-logins.md) i [jak toomanage Azure SQL bazy zabezpieczeń danych po awarii](sql-database-geo-replication-security-config.md).
* tooexport bazy danych, zobacz [wyeksportować hello bazy danych tooa pliku BACPAC](sql-database-export.md).
