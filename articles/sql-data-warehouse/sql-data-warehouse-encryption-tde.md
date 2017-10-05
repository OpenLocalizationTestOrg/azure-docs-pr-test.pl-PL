---
title: "Przezroczystego szyfrowania danych w usłudze SQL Data Warehouse (Portal) | Dokumentacja firmy Microsoft"
description: Przezroczystego szyfrowania danych (funkcji TDE) w magazynie danych SQL
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: fabf75d3-9bbf-4e0d-9b31-8b5a8713f08d
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: b1db3bdfdfb54bda325c9b971cfcb4dd5efa333a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-transparent-data-encryption-tde-in-sql-data-warehouse"></a><span data-ttu-id="0962a-103">Rozpoczynanie pracy z przezroczystym danych szyfrowania (funkcji TDE) w magazynie danych SQL</span><span class="sxs-lookup"><span data-stu-id="0962a-103">Get started with Transparent Data Encryption (TDE) in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0962a-104">Przegląd zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="0962a-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="0962a-105">Uwierzytelnianie</span><span class="sxs-lookup"><span data-stu-id="0962a-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="0962a-106">Szyfrowanie (Portal)</span><span class="sxs-lookup"><span data-stu-id="0962a-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="0962a-107">Szyfrowanie (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="0962a-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a><span data-ttu-id="0962a-108">Wymagane uprawnienia</span><span class="sxs-lookup"><span data-stu-id="0962a-108">Required Permssions</span></span>
<span data-ttu-id="0962a-109">Aby włączyć funkcji przezroczystego szyfrowania danych (TDE), musi być administrator lub członek roli dbmanager:.</span><span class="sxs-lookup"><span data-stu-id="0962a-109">To enable Transparent Data Encryption (TDE), you must be an administrator or a member of the dbmanager role.</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="0962a-110">Włączenie szyfrowania</span><span class="sxs-lookup"><span data-stu-id="0962a-110">Enabling Encryption</span></span>
<span data-ttu-id="0962a-111">Aby włączyć funkcji TDE dla magazynu danych SQL, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="0962a-111">To enable TDE for a SQL Data Warehouse, follow the steps below:</span></span>

1. <span data-ttu-id="0962a-112">Otworzyć bazy danych w [portalu Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="0962a-112">Open the database in the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="0962a-113">W bloku bazy danych, kliknij przycisk **ustawienia** przycisku</span><span class="sxs-lookup"><span data-stu-id="0962a-113">In the database blade, click the **Settings** button</span></span>
3. <span data-ttu-id="0962a-114">Wybierz **przezroczystego szyfrowania danych** opcji![][1]</span><span class="sxs-lookup"><span data-stu-id="0962a-114">Select the **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="0962a-115">Wybierz **na** ustawienie![][2]</span><span class="sxs-lookup"><span data-stu-id="0962a-115">Select the **On** setting ![][2]</span></span>
5. <span data-ttu-id="0962a-116">Wybierz **Zapisz**
   ![][3]</span><span class="sxs-lookup"><span data-stu-id="0962a-116">Select **Save**
![][3]</span></span>  

## <a name="disabling-encryption"></a><span data-ttu-id="0962a-117">Wyłączenie szyfrowania</span><span class="sxs-lookup"><span data-stu-id="0962a-117">Disabling Encryption</span></span>
<span data-ttu-id="0962a-118">Aby wyłączyć funkcji TDE dla magazynu danych SQL, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="0962a-118">To disable TDE for a SQL Data Warehouse, follow the steps below:</span></span>

1. <span data-ttu-id="0962a-119">Otworzyć bazy danych w [portalu Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="0962a-119">Open the database in the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="0962a-120">W bloku bazy danych, kliknij przycisk **ustawienia** przycisku</span><span class="sxs-lookup"><span data-stu-id="0962a-120">In the database blade, click the **Settings** button</span></span>
3. <span data-ttu-id="0962a-121">Wybierz **przezroczystego szyfrowania danych** opcji![][1]</span><span class="sxs-lookup"><span data-stu-id="0962a-121">Select the **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="0962a-122">Wybierz **poza** ustawienie![][4]</span><span class="sxs-lookup"><span data-stu-id="0962a-122">Select the **Off** setting ![][4]</span></span>
5. <span data-ttu-id="0962a-123">Wybierz **Zapisz**
   ![][5]</span><span class="sxs-lookup"><span data-stu-id="0962a-123">Select **Save**
![][5]</span></span>  

## <a name="encryption-dmvs"></a><span data-ttu-id="0962a-124">Szyfrowanie widoków DMV</span><span class="sxs-lookup"><span data-stu-id="0962a-124">Encryption DMVs</span></span>
<span data-ttu-id="0962a-125">Szyfrowanie może zostać potwierdzony z następujących widoków DMV:</span><span class="sxs-lookup"><span data-stu-id="0962a-125">Encryption can be confirmed with the following DMVs:</span></span>

* <span data-ttu-id="0962a-126">[sys.Databases]</span><span class="sxs-lookup"><span data-stu-id="0962a-126">[sys.databases]</span></span>
* <span data-ttu-id="0962a-127">[sys.dm_pdw_nodes_database_encryption_keys]</span><span class="sxs-lookup"><span data-stu-id="0962a-127">[sys.dm_pdw_nodes_database_encryption_keys]</span></span>

<!--MSDN references-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
<span data-ttu-id="0962a-128">[sys.Databases]: http://msdn.microsoft.com/library/ms178534.aspx</span><span class="sxs-lookup"><span data-stu-id="0962a-128">[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx</span></span>
<span data-ttu-id="0962a-129">[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx</span><span class="sxs-lookup"><span data-stu-id="0962a-129">[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx</span></span>

<!--Image references-->
[1]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings.png
[2]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-on.png
[3]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save.png
[4]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-off.png
[5]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save2.png

<!--Link references-->
