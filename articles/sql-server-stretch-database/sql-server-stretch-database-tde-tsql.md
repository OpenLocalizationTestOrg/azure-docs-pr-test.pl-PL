---
title: aaaEnable przezroczystego szyfrowania danych dla bazy danych Stretch, TSQL - Azure | Dokumentacja firmy Microsoft
description: "Włącz przezroczystego szyfrowania danych (funkcji TDE) dla danych programu SQL Server Stretch na Azure TSQL"
services: sql-server-stretch-database
documentationcenter: 
author: douglaslMS
manager: jhubbard
editor: 
ms.assetid: 27753d91-9ca2-4d47-b34d-b5e2c2f029bb
ms.service: sql-server-stretch-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: anvang
ms.openlocfilehash: a9ba23649656fb344480d79438a1115f0eb353bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure-transact-sql"></a>Włącz przezroczystego szyfrowania danych (funkcji TDE) dla baza danych Stretch na platformie Azure (Transact-SQL)
> [!div class="op_single_selector"]
> * [Witryna Azure Portal](sql-server-stretch-database-encryption-tde.md)
> * [TSQL](sql-server-stretch-database-tde-tsql.md)
>
>

Funkcji przezroczystego szyfrowania danych (TDE) ułatwia ochronę przed zagrożeniem hello złośliwych działań, wykonując w czasie rzeczywistym szyfrowania i odszyfrowywania hello bazy danych, skojarzonych kopii zapasowych i plików dziennika transakcji w stanie spoczynku bez konieczności zmiany toohello aplikacja.

Funkcji TDE szyfruje magazyn hello całej bazy danych przy użyciu klucza szyfrowania symetrycznego klucza o nazwie hello bazy danych. klucz szyfrowania bazy danych Hello jest chroniony za pomocą certyfikatu wbudowanego serwera. certyfikat serwera wbudowanych Hello jest unikatowy dla każdego serwera Azure. Microsoft automatycznie przełącza tych certyfikatów, co najmniej co 90 dni. Ogólny opis funkcji TDE, zobacz [funkcji przezroczystego szyfrowania danych (TDE)].

## <a name="enabling-encryption"></a>Włączenie szyfrowania
tooenable funkcji TDE Azure bazy danych, która jest przechowywana hello migracji danych z bazy danych programu SQL Server z obsługą odcinek, hello następujące czynności:

1. Połącz toohello *wzorca* bazy danych na powitania serwera Azure hostingu hello bazy danych przy użyciu nazwy logowania, która jest administrator lub członek hello **dbmanager:** roli w bazie danych master hello
2. Wykonanie powitania po instrukcji tooencrypt hello w bazie danych.

```sql
ALTER DATABASE [database_name] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a>Wyłączenie szyfrowania
toodisable funkcji TDE Azure bazy danych, która jest przechowywana hello migracji danych z bazy danych programu SQL Server z obsługą odcinek, hello następujące czynności:

1. Połącz toohello *wzorca* bazy danych przy użyciu nazwy logowania, która jest administrator lub członek hello **dbmanager:** roli w bazie danych master hello
2. Wykonanie powitania po instrukcji tooencrypt hello w bazie danych.

```sql
ALTER DATABASE [database_name] SET ENCRYPTION OFF;
```

## <a name="verifying-encryption"></a>Weryfikowanie szyfrowania
Stan szyfrowania tooverify Azure bazy danych, która jest przechowywana hello migracji danych z bazy danych programu SQL Server z obsługą odcinek, hello następujące czynności:

1. Połącz toohello *wzorca* lub wystąpienie bazy danych przy użyciu nazwy logowania, która jest administrator lub członek hello **dbmanager:** roli w bazie danych master hello
2. Wykonanie powitania po instrukcji tooencrypt hello w bazie danych.

```sql
SELECT
    [name],
    [is_encrypted]
FROM
    sys.databases;
```

W wyniku ```1``` wskazuje zaszyfrowanej bazy danych, ```0``` wskazuje niezaszyfrowane bazy danych.

<!--Anchors-->
[funkcji przezroczystego szyfrowania danych (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx


<!--Image references-->

<!--Link references-->
