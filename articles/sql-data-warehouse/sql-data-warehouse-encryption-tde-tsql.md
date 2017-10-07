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
# <a name="get-started-with-transparent-data-encryption-tde"></a><span data-ttu-id="f062b-103">Rozpoczynanie pracy z przezroczystym danych szyfrowania (funkcji TDE)</span><span class="sxs-lookup"><span data-stu-id="f062b-103">Get started with Transparent Data Encryption (TDE)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f062b-104">Przegląd zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="f062b-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="f062b-105">Uwierzytelnianie</span><span class="sxs-lookup"><span data-stu-id="f062b-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="f062b-106">Szyfrowanie (Portal)</span><span class="sxs-lookup"><span data-stu-id="f062b-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="f062b-107">Szyfrowanie (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="f062b-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a><span data-ttu-id="f062b-108">Wymagane uprawnienia</span><span class="sxs-lookup"><span data-stu-id="f062b-108">Required Permssions</span></span>
<span data-ttu-id="f062b-109">tooenable przezroczystego danych szyfrowania (funkcji TDE), musisz być administratorem lub członkiem roli dbmanager: hello.</span><span class="sxs-lookup"><span data-stu-id="f062b-109">tooenable Transparent Data Encryption (TDE), you must be an administrator or a member of hello dbmanager role.</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="f062b-110">Włączenie szyfrowania</span><span class="sxs-lookup"><span data-stu-id="f062b-110">Enabling Encryption</span></span>
<span data-ttu-id="f062b-111">Wykonaj te kroki tooenable funkcji TDE dla magazynu danych SQL:</span><span class="sxs-lookup"><span data-stu-id="f062b-111">Follow these steps tooenable TDE for a SQL Data Warehouse:</span></span>

1. <span data-ttu-id="f062b-112">Połącz toohello *wzorca* bazy danych na powitania serwera obsługującego hello bazy danych przy użyciu nazwy logowania, która jest administrator lub członek hello **dbmanager:** roli w bazie danych master hello</span><span class="sxs-lookup"><span data-stu-id="f062b-112">Connect toohello *master* database on hello server hosting hello database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="f062b-113">Wykonanie powitania po instrukcji tooencrypt hello w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="f062b-113">Execute hello following statement tooencrypt hello database.</span></span>

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a><span data-ttu-id="f062b-114">Wyłączenie szyfrowania</span><span class="sxs-lookup"><span data-stu-id="f062b-114">Disabling Encryption</span></span>
<span data-ttu-id="f062b-115">Wykonaj te kroki toodisable funkcji TDE dla magazynu danych SQL:</span><span class="sxs-lookup"><span data-stu-id="f062b-115">Follow these steps toodisable TDE for a SQL Data Warehouse:</span></span>

1. <span data-ttu-id="f062b-116">Połącz toohello *wzorca* bazy danych przy użyciu nazwy logowania, która jest administrator lub członek hello **dbmanager:** roli w bazie danych master hello</span><span class="sxs-lookup"><span data-stu-id="f062b-116">Connect toohello *master* database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="f062b-117">Wykonanie powitania po instrukcji tooencrypt hello w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="f062b-117">Execute hello following statement tooencrypt hello database.</span></span>

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION OFF;
```

> [!NOTE]
> <span data-ttu-id="f062b-118">Przed wprowadzeniem zmian ustawień funkcji TDE toohello musi zostać wznowiony wstrzymanej SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f062b-118">A paused SQL Data Warehouse must be resumed before making changes toohello TDE settings.</span></span>
> 
> 

## <a name="verifying-encryption"></a><span data-ttu-id="f062b-119">Weryfikowanie szyfrowania</span><span class="sxs-lookup"><span data-stu-id="f062b-119">Verifying Encryption</span></span>
<span data-ttu-id="f062b-120">tooverify stanu szyfrowania dla usługi SQL Data Warehouse, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="f062b-120">tooverify encryption status for a SQL Data Warehouse, follow hello steps below:</span></span>

1. <span data-ttu-id="f062b-121">Połącz toohello *wzorca* lub wystąpienie bazy danych przy użyciu nazwy logowania, która jest administrator lub członek hello **dbmanager:** roli w bazie danych master hello</span><span class="sxs-lookup"><span data-stu-id="f062b-121">Connect toohello *master* or instance database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="f062b-122">Wykonanie powitania po instrukcji tooencrypt hello w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="f062b-122">Execute hello following statement tooencrypt hello database.</span></span>

```sql
SELECT
    [name],
    [is_encrypted]
FROM
    sys.databases;
```

<span data-ttu-id="f062b-123">W wyniku ```1``` wskazuje zaszyfrowanej bazy danych, ```0``` wskazuje niezaszyfrowane bazy danych.</span><span class="sxs-lookup"><span data-stu-id="f062b-123">A result of ```1``` indicates an encrypted database, ```0``` indicates a non-encrypted database.</span></span>

## <a name="encryption-dmvs"></a><span data-ttu-id="f062b-124">Szyfrowanie widoków DMV</span><span class="sxs-lookup"><span data-stu-id="f062b-124">Encryption DMVs</span></span>
* <span data-ttu-id="f062b-125">[sys.Databases][sys.databases]</span><span class="sxs-lookup"><span data-stu-id="f062b-125">[sys.databases][sys.databases]</span></span> 
* <span data-ttu-id="f062b-126">[sys.dm_pdw_nodes_database_encryption_keys][sys.dm_pdw_nodes_database_encryption_keys]</span><span class="sxs-lookup"><span data-stu-id="f062b-126">[sys.dm_pdw_nodes_database_encryption_keys][sys.dm_pdw_nodes_database_encryption_keys]</span></span>

<!--Anchors-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx  
[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx  

<!--Image references-->

<!--Link references-->
