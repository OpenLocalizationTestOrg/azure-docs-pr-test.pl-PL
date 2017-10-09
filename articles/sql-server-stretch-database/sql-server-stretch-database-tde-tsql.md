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
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure-transact-sql"></a><span data-ttu-id="351fd-103">Włącz przezroczystego szyfrowania danych (funkcji TDE) dla baza danych Stretch na platformie Azure (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="351fd-103">Enable Transparent Data Encryption (TDE) for Stretch Database on Azure (Transact-SQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="351fd-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="351fd-104">Azure portal</span></span>](sql-server-stretch-database-encryption-tde.md)
> * [<span data-ttu-id="351fd-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="351fd-105">TSQL</span></span>](sql-server-stretch-database-tde-tsql.md)
>
>

<span data-ttu-id="351fd-106">Funkcji przezroczystego szyfrowania danych (TDE) ułatwia ochronę przed zagrożeniem hello złośliwych działań, wykonując w czasie rzeczywistym szyfrowania i odszyfrowywania hello bazy danych, skojarzonych kopii zapasowych i plików dziennika transakcji w stanie spoczynku bez konieczności zmiany toohello aplikacja.</span><span class="sxs-lookup"><span data-stu-id="351fd-106">Transparent Data Encryption (TDE) helps protect against hello threat of malicious activity by performing real-time encryption and decryption of hello database, associated backups, and transaction log files at rest without requiring changes toohello application.</span></span>

<span data-ttu-id="351fd-107">Funkcji TDE szyfruje magazyn hello całej bazy danych przy użyciu klucza szyfrowania symetrycznego klucza o nazwie hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="351fd-107">TDE encrypts hello storage of an entire database by using a symmetric key called hello database encryption key.</span></span> <span data-ttu-id="351fd-108">klucz szyfrowania bazy danych Hello jest chroniony za pomocą certyfikatu wbudowanego serwera.</span><span class="sxs-lookup"><span data-stu-id="351fd-108">hello database encryption key is protected by a built-in server certificate.</span></span> <span data-ttu-id="351fd-109">certyfikat serwera wbudowanych Hello jest unikatowy dla każdego serwera Azure.</span><span class="sxs-lookup"><span data-stu-id="351fd-109">hello built-in server certificate is unique for each Azure server.</span></span> <span data-ttu-id="351fd-110">Microsoft automatycznie przełącza tych certyfikatów, co najmniej co 90 dni.</span><span class="sxs-lookup"><span data-stu-id="351fd-110">Microsoft automatically rotates these certificates at least every 90 days.</span></span> <span data-ttu-id="351fd-111">Ogólny opis funkcji TDE, zobacz [funkcji przezroczystego szyfrowania danych (TDE)].</span><span class="sxs-lookup"><span data-stu-id="351fd-111">For a general description of TDE, see [Transparent Data Encryption (TDE)].</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="351fd-112">Włączenie szyfrowania</span><span class="sxs-lookup"><span data-stu-id="351fd-112">Enabling Encryption</span></span>
<span data-ttu-id="351fd-113">tooenable funkcji TDE Azure bazy danych, która jest przechowywana hello migracji danych z bazy danych programu SQL Server z obsługą odcinek, hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="351fd-113">tooenable TDE for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="351fd-114">Połącz toohello *wzorca* bazy danych na powitania serwera Azure hostingu hello bazy danych przy użyciu nazwy logowania, która jest administrator lub członek hello **dbmanager:** roli w bazie danych master hello</span><span class="sxs-lookup"><span data-stu-id="351fd-114">Connect toohello *master* database on hello Azure server hosting hello database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="351fd-115">Wykonanie powitania po instrukcji tooencrypt hello w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="351fd-115">Execute hello following statement tooencrypt hello database.</span></span>

```sql
ALTER DATABASE [database_name] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a><span data-ttu-id="351fd-116">Wyłączenie szyfrowania</span><span class="sxs-lookup"><span data-stu-id="351fd-116">Disabling Encryption</span></span>
<span data-ttu-id="351fd-117">toodisable funkcji TDE Azure bazy danych, która jest przechowywana hello migracji danych z bazy danych programu SQL Server z obsługą odcinek, hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="351fd-117">toodisable TDE for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="351fd-118">Połącz toohello *wzorca* bazy danych przy użyciu nazwy logowania, która jest administrator lub członek hello **dbmanager:** roli w bazie danych master hello</span><span class="sxs-lookup"><span data-stu-id="351fd-118">Connect toohello *master* database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="351fd-119">Wykonanie powitania po instrukcji tooencrypt hello w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="351fd-119">Execute hello following statement tooencrypt hello database.</span></span>

```sql
ALTER DATABASE [database_name] SET ENCRYPTION OFF;
```

## <a name="verifying-encryption"></a><span data-ttu-id="351fd-120">Weryfikowanie szyfrowania</span><span class="sxs-lookup"><span data-stu-id="351fd-120">Verifying Encryption</span></span>
<span data-ttu-id="351fd-121">Stan szyfrowania tooverify Azure bazy danych, która jest przechowywana hello migracji danych z bazy danych programu SQL Server z obsługą odcinek, hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="351fd-121">tooverify encryption status for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="351fd-122">Połącz toohello *wzorca* lub wystąpienie bazy danych przy użyciu nazwy logowania, która jest administrator lub członek hello **dbmanager:** roli w bazie danych master hello</span><span class="sxs-lookup"><span data-stu-id="351fd-122">Connect toohello *master* or instance database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="351fd-123">Wykonanie powitania po instrukcji tooencrypt hello w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="351fd-123">Execute hello following statement tooencrypt hello database.</span></span>

```sql
SELECT
    [name],
    [is_encrypted]
FROM
    sys.databases;
```

<span data-ttu-id="351fd-124">W wyniku ```1``` wskazuje zaszyfrowanej bazy danych, ```0``` wskazuje niezaszyfrowane bazy danych.</span><span class="sxs-lookup"><span data-stu-id="351fd-124">A result of ```1``` indicates an encrypted database, ```0``` indicates a non-encrypted database.</span></span>

<!--Anchors-->
[funkcji przezroczystego szyfrowania danych (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx


<!--Image references-->

<!--Link references-->
