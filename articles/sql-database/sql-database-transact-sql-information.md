---
title: "aaaResolving T-SQL różnice migracji Azure SQL Database | Dokumentacja firmy Microsoft"
description: "Instrukcje języka Transact-SQL, które nie są w pełni obsługiwane w usłudze Azure SQL Database"
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: c05abd9e-28a7-4c97-9bdf-bc60d08fc92e
ms.service: sql-database
ms.custom: load & move data
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 03/17/2017
ms.author: rickbyh
ms.openlocfilehash: 3852013338bfdc6c7da9d1d879c54781682bc635
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="resolving-transact-sql-differences-during-migration-toosql-database"></a>Rozstrzyganie różnic języka Transact-SQL podczas migracji tooSQL bazy danych   
Gdy [Migrowanie bazy danych](sql-database-cloud-migrate.md) z tooAzure programu SQL Server SQL Server, użytkownik może stwierdzić, że baza danych wymaga niektórych reorganizacji przed hello programu SQL Server, które można poddać migracji. W tym temacie omówiono tooassist wskazówki, które możesz zarówno wykonywania ponownego projektowania i zrozumienie podstawowych powodów dlaczego hello hello reorganizacji niezbędne. niezgodności toodetect Użyj hello [Asystenta migracji danych (DMA)](https://www.microsoft.com/download/details.aspx?id=53595).

## <a name="overview"></a>Omówienie
Większość funkcji języka Transact-SQL, które używają aplikacji są w pełni obsługiwane zarówno w przypadku programu Microsoft SQL Server, jak i bazy danych SQL Azure. Na przykład Witaj podstawowe składniki programu SQL, takich jak typy danych, operatory, ciąg, operacje arytmetyczne, logiczna i funkcje kursora, tak samo pracy w programie SQL Server i bazy danych SQL. Istnieją, jednak niewielkie różnice T-SQL w pliku DDL (języka definicji danych) i elementy DML (język edycji danych), co zapewnia instrukcje T-SQL i zapytań, które są obsługiwane tylko częściowo (co omówiono w dalszej części tego tematu).

Ponadto niektóre funkcje i składnię, która nie jest obsługiwana w ogóle, ponieważ baza danych SQL Azure jest zaprojektowany funkcji tooisolate z na powitania bazy danych master i hello systemu operacyjnego. W efekcie większości działań na poziomie serwera nie mają zastosowania do bazy danych SQL. Instrukcje T-SQL i opcje nie są dostępne, jeśli skonfiguruj opcje na poziomie serwera, składników systemu operacyjnego, lub określ plik konfiguracji systemu. Jeśli takie możliwości są wymagane, właściwym rozwiązaniem często jest dostępny w inny sposób funkcji z bazy danych SQL lub innej platformy Azure lub usługi. 

Na przykład wysokiej dostępności jest oparty na platformie Azure, dlatego nie jest konieczne konfigurowanie zawsze włączone, (mimo że może być aktywna replikacja geograficzna tooconfigure szybsze odzyskiwania w razie awarii hello). Tak instrukcje T-SQL dotyczące tooavailability grupy nie są obsługiwane przez usługę SQL Database i powiązane tooAlways widoki dynamiczne zarządzanie hello na nie również są obsługiwane.

Aby uzyskać listę hello funkcje, które są obsługiwane i nieobsługiwane przez bazę danych SQL, zobacz [porównanie funkcji bazy danych SQL Azure](sql-database-features.md). Lista Hello na tej stronie stanowi uzupełnienie tego tematu wskazówki i funkcje i koncentruje się na instrukcji języka Transact-SQL.

## <a name="transact-sql-syntax-statements-with-partial-differences"></a>Instrukcje składni języka Transact-SQL z częściowa różnic
instrukcji DDL (języka definicji danych) core Hello są dostępne, ale niektóre instrukcji DDL mają rozszerzenia powiązane toodisk umieszczania i nieobsługiwane funkcje. 

- Instrukcje CREATE i ALTER DATABASE ma ponad dwanaście trzy opcje. instrukcje Hello zawierają umieszczania plików FILESTREAM i opcje brokera usługi, które mają zastosowanie tylko tooSQL serwera. To może niezależnie od tego, czy tworzenie baz danych, przed przeprowadzeniem migracji, ale w przypadku migracji kod T-SQL, który tworzy bazy danych należy porównać [CREATE DATABASE (baza danych SQL Azure)](https://msdn.microsoft.com/library/dn268335.aspx) o składni SQL Server hello na [Utwórz Bazy danych (SQL Server Transact-SQL)](https://msdn.microsoft.com/library/ms176061.aspx) toomake się, że wszystkie opcje hello używane są obsługiwane. Tworzenie bazy danych dla bazy danych SQL Azure ma również cel usługi i opcje elastycznego skalowania, które są stosowane tylko tooSQL bazy danych.
- instrukcje CREATE i ALTER TABLE Hello ma FileTable opcje, których nie można używać w bazie danych SQL, ponieważ FILESTREAM nie jest obsługiwany.
- Tworzenie i ALTER login instrukcje są obsługiwane, ale baza danych SQL nie oferuje wszystkie opcje hello. toomake zachęca bazy danych przenośną, baza danych SQL przy użyciu zawarte bazy danych użytkowników zamiast nazwy logowania, jeśli to możliwe. Aby uzyskać więcej informacji, zobacz [CREATE/ALTER LOGIN](https://msdn.microsoft.com/library/ms189828.aspx) i [kontrolowanie i udzielanie dostępu do bazy danych](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins).

## <a name="transact-sql-syntax-not-supported-in-sql-database"></a>Składnia języka Transact-SQL nieobsługiwana w bazie danych SQL Database   
Ponadto toohello powiązane instrukcje tooTransact SQL nieobsługiwane funkcje opisane w [porównanie funkcji bazy danych SQL Azure](sql-database-features.md), hello następujące instrukcje i grup instrukcji, nie są obsługiwane. Tak, czy toobe Twojej bazy danych migracji korzysta z następujących hello funkcji, ponownie opracowywać tooeliminate Twojego T-SQL te funkcje T-SQL i instrukcje.

- Sortowanie obiektów systemu
- Dotyczące połączeń: instrukcje Endpoint, `ORIGINAL_DB_NAME`. Baza danych SQL nie obsługuje uwierzytelniania systemu Windows, ale obsługuje hello podobne uwierzytelniania usługi Azure Active Directory. Niektóre typy uwierzytelniania wymagają hello najnowszą wersję programu SSMS. Aby uzyskać więcej informacji, zobacz [tooSQL łączenie bazy danych lub danych magazynu przez przy użyciu Azure Active Directory uwierzytelniania SQL](sql-database-aad-authentication.md).
- Zapytania obejmujące wiele baz danych, korzystające z nazw trój- i czteroczęściowych. (Zapytania tylko do odczytu obejmujące wiele baz danych są obsługiwane za pomocą [zapytania elastycznej bazy danych](sql-database-elastic-query-overview.md)).
- Tworzenie łańcucha własności między wieloma bazami danych, ustawienie `TRUSTWORTHY`
- `DATABASEPROPERTY` Zamiast tego użyj instrukcji `DATABASEPROPERTYEX`.
- `EXECUTE AS LOGIN` Zamiast tego użyj instrukcji „EXECUTE AS USER”.
- Szyfrowanie jest obsługiwane z wyjątkiem rozszerzonego zarządzania kluczami
- Obsługi zdarzeń: Zdarzeń, powiadomień o zdarzeniach, powiadomienia kwerendy
- Położenie pliku: Składnia powiązane toodatabase położenie pliku, rozmiar i pliki bazy danych, które są automatycznie zarządzane przez Microsoft Azure.
- Wysoka dostępność: Składnia powiązane toohigh dostępności, która jest zarządzana za pomocą konta Microsoft Azure. Obejmuje to składnię kopii zapasowych, przywracania, funkcji Always On, dublowania bazy danych, wysyłania dziennika oraz trybów odzyskiwania.
- Czytnik dziennika: składnię, która opiera się na powitania czytnik dziennika, który nie jest dostępny w bazie danych SQL: Push replikacji, przechwytywania zmian danych. Baza danych SQL Database może być subskrybentem artykułu replikacji wypychanej.
- Funkcje: `fn_get_sql`, `fn_virtualfilestats`, `fn_virtualservernodes`
- Globalne tabele tymczasowe
- Sprzęt: Składni powiązane ustawienia serwera dotyczące toohardware: takich jak pamięć wątków roboczych, koligacji procesora CPU, flagi śledzenia. Zamiast tego użyj poziomów usług.
- `HAS_DBACCESS`
- `KILL STATS JOB`
- `OPENQUERY`, `OPENROWSET`, `OPENDATASOURCE`i czteroczęściową nazwy
- .NET framework: CLR integracji z programem SQL Server
- Wyszukiwanie semantyczne
- Poświadczenia serwera: Użyj [poświadczeń o zakresie bazy danych](https://msdn.microsoft.com/library/mt270260.aspx) zamiast tego.
- Elementy na poziomie serwera: role serwera, `IS_SRVROLEMEMBER`, `sys.login_token`. Instrukcje `GRANT`, `REVOKE` i `DENY` w odniesieniu do uprawnień na poziomie serwera nie są dostępne, chociaż niektóre zostały zastąpione przez uprawnienia na poziomie bazy danych. Niektóre przydatne dynamiczne widoki zarządzania na poziomie serwera mają swoje odpowiedniki na poziomie bazy danych.
- `SET REMOTE_PROC_TRANSACTIONS`
- `SHUTDOWN`
- `sp_addmessage`
- Opcje polecenia `sp_configure` i instrukcja `RECONFIGURE`. Niektóre opcje są dostępne po użyciu instrukcji [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx).
- `sp_helpuser`
- `sp_migrate_user_to_contained`
- SQL Server Agent: Składnię, która opiera się na powitania agenta programu SQL Server lub hello bazy danych MSDB: alerty, operatory, centralnego zarządzania serwerami. Zamiast tego używaj skryptów, takich jak Azure PowerShell.
- SQL Server audit: Użyj bazy danych SQL zamiast inspekcji.
- Śledzenie programu SQL Server
- Flagi śledzenia: Flaga śledzenia, niektóre elementy zostały przeniesione toocompatibility trybów.
- Debugowanie języka Transact-SQL
- Wyzwalacze: wyzwalacze zakresu serwera lub wyzwalacze logowania
- `USE`Instrukcja: toochange hello kontekstu tooa różnych baza danych, należy wykonać nowe połączenie toohello nową bazę danych.

## <a name="full-transact-sql-reference"></a>Pełna dokumentacja języka Transact-SQL
Aby uzyskać więcej informacji dotyczących gramatyki języka Transact-SQL oraz przykłady jego użycia, zobacz artykuł [Transact-SQL Reference (Database Engine)](https://msdn.microsoft.com/library/bb510741.aspx) (Dokumentacja języka Transact-SQL (aparat bazy danych)) w dokumentacji SQL Server — książki online. 

### <a name="about-hello-applies-to-tags"></a>Tagi "Dotyczy" hello — informacje
Witaj języka Transact-SQL zawiera tematy pokrewne tooSQL obecny toohello 2008 wersji serwera. Poniżej tytuł tematu hello jest pasek ikon, listę hello cztery programu SQL Server platform i wskazujące możliwość zastosowania. Na przykład grupy dostępności zostały wprowadzone w programie SQL Server 2012. [Utwórz GRUPĘ AVAILABILTY](https://msdn.microsoft.com/library/ff878399.aspx) tematu wskazuje, że instrukcja hello dotyczy **programu SQL Server (począwszy od 2012)**. Instrukcja Hello nie ma zastosowania, tooSQL Server 2008, SQL Server 2008 R2, baza danych SQL Azure, Magazyn danych SQL Azure lub Parallel Data Warehouse.

W niektórych przypadkach temat hello tematu mogą być używane w produktu, ale występują niewielkie różnice między produktów. różnice Hello są oznaczone w punkty środkowe w temacie hello zależnie od potrzeb. W niektórych przypadkach temat hello tematu mogą być używane w produktu, ale występują niewielkie różnice między produktów. różnice Hello są oznaczone w punkty środkowe w temacie hello zależnie od potrzeb. Na przykład temat CREATE TRIGGER hello jest dostępny w bazie danych SQL. Ale hello **wszystkie SERVER** opcji wyzwalaczy na poziomie serwera, wskazuje, że wyzwalaczy poziomu serwera nie może być używane w bazie danych SQL. Zamiast tego Użyj wyzwalaczy na poziomie bazy danych.

## <a name="next-steps"></a>Następne kroki

Aby uzyskać listę hello funkcje, które są obsługiwane i nieobsługiwane przez bazę danych SQL, zobacz [porównanie funkcji bazy danych SQL Azure](sql-database-features.md). Lista Hello na tej stronie stanowi uzupełnienie tego tematu wskazówki i funkcje i koncentruje się na instrukcji języka Transact-SQL.

