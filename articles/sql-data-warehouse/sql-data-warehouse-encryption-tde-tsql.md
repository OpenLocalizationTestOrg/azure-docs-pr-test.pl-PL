---
title: aaaTransparent szyfrowanie danych w magazynie danych SQL (T-SQL) | Dokumentacja firmy Microsoft
description: Przezroczystego szyfrowania danych (funkcji TDE) w magazynie danych SQL (T-SQL)
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: barbkess
editor: 
ms.assetid: 8ccefef3-1308-41ee-b336-5e491d1098ae
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: 3894431c76f14b217f3a6b9a42dbf2f4d216bad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-transparent-data-encryption-tde"></a>Rozpoczynanie pracy z przezroczystym danych szyfrowania (funkcji TDE)
> [!div class="op_single_selector"]
> * [Przegląd zabezpieczeń](sql-data-warehouse-overview-manage-security.md)
> * [Uwierzytelnianie](sql-data-warehouse-authentication.md)
> * [Szyfrowanie (Portal)](sql-data-warehouse-encryption-tde.md)
> * [Szyfrowanie (T-SQL)](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a>Wymagane uprawnienia
tooenable przezroczystego danych szyfrowania (funkcji TDE), musisz być administratorem lub członkiem roli dbmanager: hello.

## <a name="enabling-encryption"></a>Włączenie szyfrowania
Wykonaj te kroki tooenable funkcji TDE dla magazynu danych SQL:

1. Połącz toohello *wzorca* bazy danych na powitania serwera obsługującego hello bazy danych przy użyciu nazwy logowania, która jest administrator lub członek hello **dbmanager:** roli w bazie danych master hello
2. Wykonanie powitania po instrukcji tooencrypt hello w bazie danych.

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a>Wyłączenie szyfrowania
Wykonaj te kroki toodisable funkcji TDE dla magazynu danych SQL:

1. Połącz toohello *wzorca* bazy danych przy użyciu nazwy logowania, która jest administrator lub członek hello **dbmanager:** roli w bazie danych master hello
2. Wykonanie powitania po instrukcji tooencrypt hello w bazie danych.

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION OFF;
```

> [!NOTE]
> Przed wprowadzeniem zmian ustawień funkcji TDE toohello musi zostać wznowiony wstrzymanej SQL Data Warehouse.
> 
> 

## <a name="verifying-encryption"></a>Weryfikowanie szyfrowania
tooverify stanu szyfrowania dla usługi SQL Data Warehouse, wykonaj poniższe kroki hello:

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

## <a name="encryption-dmvs"></a>Szyfrowanie widoków DMV
* [sys.Databases][sys.databases] 
* [sys.dm_pdw_nodes_database_encryption_keys][sys.dm_pdw_nodes_database_encryption_keys]

<!--Anchors-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx  
[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx  

<!--Image references-->

<!--Link references-->
