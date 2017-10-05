---
title: "Włącz przezroczystego szyfrowania danych dla bazy danych Stretch - Azure | Dokumentacja firmy Microsoft"
description: "Włącz przezroczystego szyfrowania danych (funkcji TDE) dla danych programu SQL Server Stretch na platformie Azure"
services: sql-server-stretch-database
documentationcenter: 
author: douglaslMS
manager: barbkess
editor: 
ms.assetid: a44ed8f5-b416-4c41-9b1e-b7271f10bdc3
ms.service: sql-server-stretch-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2016
ms.author: douglasl
ms.openlocfilehash: ceb355d2ba872ed5d3886c6dc82ca75b1854db0a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure"></a><span data-ttu-id="b8f7b-103">Włącz przezroczystego szyfrowania danych (funkcji TDE) dla baza danych Stretch na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="b8f7b-103">Enable Transparent Data Encryption (TDE) for Stretch Database on Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b8f7b-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b8f7b-104">Azure portal</span></span>](sql-server-stretch-database-encryption-tde.md)
> * [<span data-ttu-id="b8f7b-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="b8f7b-105">TSQL</span></span>](sql-server-stretch-database-tde-tsql.md)
>
>

<span data-ttu-id="b8f7b-106">Funkcji przezroczystego szyfrowania danych (TDE) pomaga w ochronie przed zagrożeniem złośliwych działań, wykonując w czasie rzeczywistym szyfrowanie i odszyfrowywanie bazy danych, skojarzonych kopii zapasowych i plików dziennika transakcji w stanie spoczynku bez konieczności wprowadzania zmian w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b8f7b-106">Transparent Data Encryption (TDE) helps protect against the threat of malicious activity by performing real-time encryption and decryption of the database, associated backups, and transaction log files at rest without requiring changes to the application.</span></span>

<span data-ttu-id="b8f7b-107">Funkcji TDE szyfruje magazyn całej bazy danych przy użyciu klucza symetrycznego o nazwie klucza szyfrowania bazy danych.</span><span class="sxs-lookup"><span data-stu-id="b8f7b-107">TDE encrypts the storage of an entire database by using a symmetric key called the database encryption key.</span></span> <span data-ttu-id="b8f7b-108">Klucz szyfrowania bazy danych jest chroniony za pomocą certyfikatu wbudowanego serwera.</span><span class="sxs-lookup"><span data-stu-id="b8f7b-108">The database encryption key is protected by a built-in server certificate.</span></span> <span data-ttu-id="b8f7b-109">Certyfikat serwera wbudowanych jest unikatowy dla każdego serwera usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="b8f7b-109">The built-in server certificate is unique for each Azure server.</span></span> <span data-ttu-id="b8f7b-110">Microsoft automatycznie przełącza tych certyfikatów, co najmniej co 90 dni.</span><span class="sxs-lookup"><span data-stu-id="b8f7b-110">Microsoft automatically rotates these certificates at least every 90 days.</span></span> <span data-ttu-id="b8f7b-111">Ogólny opis funkcji TDE, zobacz [funkcji przezroczystego szyfrowania danych (TDE)].</span><span class="sxs-lookup"><span data-stu-id="b8f7b-111">For a general description of TDE, see [Transparent Data Encryption (TDE)].</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="b8f7b-112">Włączenie szyfrowania</span><span class="sxs-lookup"><span data-stu-id="b8f7b-112">Enabling Encryption</span></span>
<span data-ttu-id="b8f7b-113">Aby włączyć funkcji TDE platformy Azure bazy danych, które są przechowywane dane migracji z bazy danych programu SQL Server z obsługą odcinek, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b8f7b-113">To enable TDE for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:</span></span>

1. <span data-ttu-id="b8f7b-114">Otworzyć bazy danych w [portalu Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="b8f7b-114">Open the database in the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="b8f7b-115">W bloku bazy danych, kliknij przycisk **ustawienia** przycisku</span><span class="sxs-lookup"><span data-stu-id="b8f7b-115">In the database blade, click the **Settings** button</span></span>
3. <span data-ttu-id="b8f7b-116">Wybierz **przezroczystego szyfrowania danych** opcji![][1]</span><span class="sxs-lookup"><span data-stu-id="b8f7b-116">Select the **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="b8f7b-117">Wybierz **na** ustawienia, a następnie wybierz **Zapisz**
   ![][2]</span><span class="sxs-lookup"><span data-stu-id="b8f7b-117">Select the **On** setting, and then select **Save**
![][2]</span></span>

## <a name="disabling-encryption"></a><span data-ttu-id="b8f7b-118">Wyłączenie szyfrowania</span><span class="sxs-lookup"><span data-stu-id="b8f7b-118">Disabling Encryption</span></span>
<span data-ttu-id="b8f7b-119">Wyłączenie funkcji TDE platformy Azure bazy danych, które są przechowywane dane migracji z bazy danych programu SQL Server z obsługą odcinek, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b8f7b-119">To disable TDE for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:</span></span>

1. <span data-ttu-id="b8f7b-120">Otworzyć bazy danych w [portalu Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="b8f7b-120">Open the database in the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="b8f7b-121">W bloku bazy danych, kliknij przycisk **ustawienia** przycisku</span><span class="sxs-lookup"><span data-stu-id="b8f7b-121">In the database blade, click the **Settings** button</span></span>
3. <span data-ttu-id="b8f7b-122">Wybierz **przezroczystego szyfrowania danych** opcji</span><span class="sxs-lookup"><span data-stu-id="b8f7b-122">Select the **Transparent data encryption** option</span></span>
4. <span data-ttu-id="b8f7b-123">Wybierz **poza** ustawienia, a następnie wybierz **Zapisz**</span><span class="sxs-lookup"><span data-stu-id="b8f7b-123">Select the **Off** setting, and then select **Save**</span></span>

<!--Anchors-->
<span data-ttu-id="b8f7b-124">[funkcji przezroczystego szyfrowania danych (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx</span><span class="sxs-lookup"><span data-stu-id="b8f7b-124">[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx</span></span>


<!--Image references-->
[1]: ./media/sql-server-stretch-database-encryption-tde/stretchtde1.png
[2]: ./media/sql-server-stretch-database-encryption-tde/stretchtde2.png


<!--Link references-->
