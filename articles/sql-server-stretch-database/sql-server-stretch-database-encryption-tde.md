---
title: aaaEnable przezroczystego szyfrowania danych dla bazy danych Stretch - Azure | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: 1d6bff455030ac8851b2184c1e8097afd61361d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure"></a><span data-ttu-id="1c485-103">Włącz przezroczystego szyfrowania danych (funkcji TDE) dla baza danych Stretch na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="1c485-103">Enable Transparent Data Encryption (TDE) for Stretch Database on Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1c485-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="1c485-104">Azure portal</span></span>](sql-server-stretch-database-encryption-tde.md)
> * [<span data-ttu-id="1c485-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="1c485-105">TSQL</span></span>](sql-server-stretch-database-tde-tsql.md)
>
>

<span data-ttu-id="1c485-106">Funkcji przezroczystego szyfrowania danych (TDE) ułatwia ochronę przed zagrożeniem hello złośliwych działań, wykonując w czasie rzeczywistym szyfrowania i odszyfrowywania hello bazy danych, skojarzonych kopii zapasowych i plików dziennika transakcji w stanie spoczynku bez konieczności zmiany toohello aplikacja.</span><span class="sxs-lookup"><span data-stu-id="1c485-106">Transparent Data Encryption (TDE) helps protect against hello threat of malicious activity by performing real-time encryption and decryption of hello database, associated backups, and transaction log files at rest without requiring changes toohello application.</span></span>

<span data-ttu-id="1c485-107">Funkcji TDE szyfruje magazyn hello całej bazy danych przy użyciu klucza szyfrowania symetrycznego klucza o nazwie hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="1c485-107">TDE encrypts hello storage of an entire database by using a symmetric key called hello database encryption key.</span></span> <span data-ttu-id="1c485-108">klucz szyfrowania bazy danych Hello jest chroniony za pomocą certyfikatu wbudowanego serwera.</span><span class="sxs-lookup"><span data-stu-id="1c485-108">hello database encryption key is protected by a built-in server certificate.</span></span> <span data-ttu-id="1c485-109">certyfikat serwera wbudowanych Hello jest unikatowy dla każdego serwera Azure.</span><span class="sxs-lookup"><span data-stu-id="1c485-109">hello built-in server certificate is unique for each Azure server.</span></span> <span data-ttu-id="1c485-110">Microsoft automatycznie przełącza tych certyfikatów, co najmniej co 90 dni.</span><span class="sxs-lookup"><span data-stu-id="1c485-110">Microsoft automatically rotates these certificates at least every 90 days.</span></span> <span data-ttu-id="1c485-111">Ogólny opis funkcji TDE, zobacz [funkcji przezroczystego szyfrowania danych (TDE)].</span><span class="sxs-lookup"><span data-stu-id="1c485-111">For a general description of TDE, see [Transparent Data Encryption (TDE)].</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="1c485-112">Włączenie szyfrowania</span><span class="sxs-lookup"><span data-stu-id="1c485-112">Enabling Encryption</span></span>
<span data-ttu-id="1c485-113">tooenable funkcji TDE Azure bazy danych, która jest przechowywana hello migracji danych z bazy danych programu SQL Server z obsługą odcinek, hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="1c485-113">tooenable TDE for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="1c485-114">Bazy danych otwórz hello w hello [portalu Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="1c485-114">Open hello database in hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="1c485-115">W bloku bazy danych powitania kliknij hello **ustawienia** przycisku</span><span class="sxs-lookup"><span data-stu-id="1c485-115">In hello database blade, click hello **Settings** button</span></span>
3. <span data-ttu-id="1c485-116">Wybierz hello **przezroczystego szyfrowania danych** opcji![][1]</span><span class="sxs-lookup"><span data-stu-id="1c485-116">Select hello **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="1c485-117">Wybierz hello **na** ustawienia, a następnie wybierz **Zapisz**
   ![][2]</span><span class="sxs-lookup"><span data-stu-id="1c485-117">Select hello **On** setting, and then select **Save**
![][2]</span></span>

## <a name="disabling-encryption"></a><span data-ttu-id="1c485-118">Wyłączenie szyfrowania</span><span class="sxs-lookup"><span data-stu-id="1c485-118">Disabling Encryption</span></span>
<span data-ttu-id="1c485-119">toodisable funkcji TDE Azure bazy danych, która jest przechowywana hello migracji danych z bazy danych programu SQL Server z obsługą odcinek, hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="1c485-119">toodisable TDE for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="1c485-120">Bazy danych otwórz hello w hello [portalu Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="1c485-120">Open hello database in hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="1c485-121">W bloku bazy danych powitania kliknij hello **ustawienia** przycisku</span><span class="sxs-lookup"><span data-stu-id="1c485-121">In hello database blade, click hello **Settings** button</span></span>
3. <span data-ttu-id="1c485-122">Wybierz hello **przezroczystego szyfrowania danych** opcji</span><span class="sxs-lookup"><span data-stu-id="1c485-122">Select hello **Transparent data encryption** option</span></span>
4. <span data-ttu-id="1c485-123">Wybierz hello **poza** ustawienia, a następnie wybierz **Zapisz**</span><span class="sxs-lookup"><span data-stu-id="1c485-123">Select hello **Off** setting, and then select **Save**</span></span>

<!--Anchors-->
[funkcji przezroczystego szyfrowania danych (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx


<!--Image references-->
[1]: ./media/sql-server-stretch-database-encryption-tde/stretchtde1.png
[2]: ./media/sql-server-stretch-database-encryption-tde/stretchtde2.png


<!--Link references-->
