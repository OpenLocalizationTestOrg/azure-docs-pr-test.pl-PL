---
title: "Włącz przezroczystego szyfrowania danych dla baza danych Stretch TSQL - Azure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: ed26c2b386e08b76f78b4a05e12c46d2b97c20f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure-transact-sql"></a><span data-ttu-id="ab19c-103">Włącz przezroczystego szyfrowania danych (funkcji TDE) dla baza danych Stretch na platformie Azure (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="ab19c-103">Enable Transparent Data Encryption (TDE) for Stretch Database on Azure (Transact-SQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ab19c-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ab19c-104">Azure portal</span></span>](sql-server-stretch-database-encryption-tde.md)
> * [<span data-ttu-id="ab19c-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="ab19c-105">TSQL</span></span>](sql-server-stretch-database-tde-tsql.md)
>
>

<span data-ttu-id="ab19c-106">Funkcji przezroczystego szyfrowania danych (TDE) pomaga w ochronie przed zagrożeniem złośliwych działań, wykonując w czasie rzeczywistym szyfrowanie i odszyfrowywanie bazy danych, skojarzonych kopii zapasowych i plików dziennika transakcji w stanie spoczynku bez konieczności wprowadzania zmian w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ab19c-106">Transparent Data Encryption (TDE) helps protect against the threat of malicious activity by performing real-time encryption and decryption of the database, associated backups, and transaction log files at rest without requiring changes to the application.</span></span>

<span data-ttu-id="ab19c-107">Funkcji TDE szyfruje magazyn całej bazy danych przy użyciu klucza symetrycznego o nazwie klucza szyfrowania bazy danych.</span><span class="sxs-lookup"><span data-stu-id="ab19c-107">TDE encrypts the storage of an entire database by using a symmetric key called the database encryption key.</span></span> <span data-ttu-id="ab19c-108">Klucz szyfrowania bazy danych jest chroniony za pomocą certyfikatu wbudowanego serwera.</span><span class="sxs-lookup"><span data-stu-id="ab19c-108">The database encryption key is protected by a built-in server certificate.</span></span> <span data-ttu-id="ab19c-109">Certyfikat serwera wbudowanych jest unikatowy dla każdego serwera usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="ab19c-109">The built-in server certificate is unique for each Azure server.</span></span> <span data-ttu-id="ab19c-110">Microsoft automatycznie przełącza tych certyfikatów, co najmniej co 90 dni.</span><span class="sxs-lookup"><span data-stu-id="ab19c-110">Microsoft automatically rotates these certificates at least every 90 days.</span></span> <span data-ttu-id="ab19c-111">Ogólny opis funkcji TDE, zobacz [funkcji przezroczystego szyfrowania danych (TDE)].</span><span class="sxs-lookup"><span data-stu-id="ab19c-111">For a general description of TDE, see [Transparent Data Encryption (TDE)].</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="ab19c-112">Włączenie szyfrowania</span><span class="sxs-lookup"><span data-stu-id="ab19c-112">Enabling Encryption</span></span>
<span data-ttu-id="ab19c-113">Aby włączyć funkcji TDE platformy Azure bazy danych, które są przechowywane dane migracji z bazy danych programu SQL Server z obsługą odcinek, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ab19c-113">To enable TDE for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:</span></span>

1. <span data-ttu-id="ab19c-114">Połączyć się z *wzorca* bazy danych na serwer platformy Azure obsługującym bazę danych przy użyciu nazwy logowania, która jest administrator lub członek **dbmanager:** roli w bazie danych master</span><span class="sxs-lookup"><span data-stu-id="ab19c-114">Connect to the *master* database on the Azure server hosting the database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="ab19c-115">Wykonaj następującą instrukcję do szyfrowania bazy danych.</span><span class="sxs-lookup"><span data-stu-id="ab19c-115">Execute the following statement to encrypt the database.</span></span>

```sql
ALTER DATABASE [database_name] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a><span data-ttu-id="ab19c-116">Wyłączenie szyfrowania</span><span class="sxs-lookup"><span data-stu-id="ab19c-116">Disabling Encryption</span></span>
<span data-ttu-id="ab19c-117">Wyłączenie funkcji TDE platformy Azure bazy danych, które są przechowywane dane migracji z bazy danych programu SQL Server z obsługą odcinek, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ab19c-117">To disable TDE for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:</span></span>

1. <span data-ttu-id="ab19c-118">Połączyć się z *wzorca* bazy danych przy użyciu nazwy logowania, która jest administrator lub członek **dbmanager:** roli w bazie danych master</span><span class="sxs-lookup"><span data-stu-id="ab19c-118">Connect to the *master* database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="ab19c-119">Wykonaj następującą instrukcję do szyfrowania bazy danych.</span><span class="sxs-lookup"><span data-stu-id="ab19c-119">Execute the following statement to encrypt the database.</span></span>

```sql
ALTER DATABASE [database_name] SET ENCRYPTION OFF;
```

## <a name="verifying-encryption"></a><span data-ttu-id="ab19c-120">Weryfikowanie szyfrowania</span><span class="sxs-lookup"><span data-stu-id="ab19c-120">Verifying Encryption</span></span>
<span data-ttu-id="ab19c-121">Aby sprawdzić, czy stan szyfrowania Azure bazy danych, które są przechowywane dane migracji z bazy danych programu SQL Server z obsługą odcinek, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ab19c-121">To verify encryption status for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:</span></span>

1. <span data-ttu-id="ab19c-122">Połączyć się z *wzorca* lub wystąpienie bazy danych przy użyciu nazwy logowania, która jest administrator lub członek **dbmanager:** roli w bazie danych master</span><span class="sxs-lookup"><span data-stu-id="ab19c-122">Connect to the *master* or instance database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="ab19c-123">Wykonaj następującą instrukcję do szyfrowania bazy danych.</span><span class="sxs-lookup"><span data-stu-id="ab19c-123">Execute the following statement to encrypt the database.</span></span>

```sql
SELECT
    [name],
    [is_encrypted]
FROM
    sys.databases;
```

<span data-ttu-id="ab19c-124">W wyniku ```1``` wskazuje zaszyfrowanej bazy danych, ```0``` wskazuje niezaszyfrowane bazy danych.</span><span class="sxs-lookup"><span data-stu-id="ab19c-124">A result of ```1``` indicates an encrypted database, ```0``` indicates a non-encrypted database.</span></span>

<!--Anchors-->
<span data-ttu-id="ab19c-125">[funkcji przezroczystego szyfrowania danych (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx</span><span class="sxs-lookup"><span data-stu-id="ab19c-125">[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx</span></span>


<!--Image references-->

<!--Link references-->
