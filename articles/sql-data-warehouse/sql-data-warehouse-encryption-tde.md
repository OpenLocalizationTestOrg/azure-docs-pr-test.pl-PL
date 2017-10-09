---
title: "aaaTransparent szyfrowanie danych w usłudze SQL Data Warehouse (Portal) | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 8233886ecf170844104e0d1459e2a829cafa9b8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-transparent-data-encryption-tde-in-sql-data-warehouse"></a><span data-ttu-id="8fe27-103">Rozpoczynanie pracy z przezroczystym danych szyfrowania (funkcji TDE) w magazynie danych SQL</span><span class="sxs-lookup"><span data-stu-id="8fe27-103">Get started with Transparent Data Encryption (TDE) in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8fe27-104">Przegląd zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="8fe27-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="8fe27-105">Uwierzytelnianie</span><span class="sxs-lookup"><span data-stu-id="8fe27-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="8fe27-106">Szyfrowanie (Portal)</span><span class="sxs-lookup"><span data-stu-id="8fe27-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="8fe27-107">Szyfrowanie (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="8fe27-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a><span data-ttu-id="8fe27-108">Wymagane uprawnienia</span><span class="sxs-lookup"><span data-stu-id="8fe27-108">Required Permssions</span></span>
<span data-ttu-id="8fe27-109">tooenable przezroczystego danych szyfrowania (funkcji TDE), musisz być administratorem lub członkiem roli dbmanager: hello.</span><span class="sxs-lookup"><span data-stu-id="8fe27-109">tooenable Transparent Data Encryption (TDE), you must be an administrator or a member of hello dbmanager role.</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="8fe27-110">Włączenie szyfrowania</span><span class="sxs-lookup"><span data-stu-id="8fe27-110">Enabling Encryption</span></span>
<span data-ttu-id="8fe27-111">tooenable funkcji TDE dla magazynu danych SQL, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="8fe27-111">tooenable TDE for a SQL Data Warehouse, follow hello steps below:</span></span>

1. <span data-ttu-id="8fe27-112">Bazy danych otwórz hello w hello [portalu Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="8fe27-112">Open hello database in hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="8fe27-113">W bloku bazy danych powitania kliknij hello **ustawienia** przycisku</span><span class="sxs-lookup"><span data-stu-id="8fe27-113">In hello database blade, click hello **Settings** button</span></span>
3. <span data-ttu-id="8fe27-114">Wybierz hello **przezroczystego szyfrowania danych** opcji![][1]</span><span class="sxs-lookup"><span data-stu-id="8fe27-114">Select hello **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="8fe27-115">Wybierz hello **na** ustawienie![][2]</span><span class="sxs-lookup"><span data-stu-id="8fe27-115">Select hello **On** setting ![][2]</span></span>
5. <span data-ttu-id="8fe27-116">Wybierz **Zapisz**
   ![][3]</span><span class="sxs-lookup"><span data-stu-id="8fe27-116">Select **Save**
![][3]</span></span>  

## <a name="disabling-encryption"></a><span data-ttu-id="8fe27-117">Wyłączenie szyfrowania</span><span class="sxs-lookup"><span data-stu-id="8fe27-117">Disabling Encryption</span></span>
<span data-ttu-id="8fe27-118">toodisable funkcji TDE dla magazynu danych SQL, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="8fe27-118">toodisable TDE for a SQL Data Warehouse, follow hello steps below:</span></span>

1. <span data-ttu-id="8fe27-119">Bazy danych otwórz hello w hello [portalu Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="8fe27-119">Open hello database in hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="8fe27-120">W bloku bazy danych powitania kliknij hello **ustawienia** przycisku</span><span class="sxs-lookup"><span data-stu-id="8fe27-120">In hello database blade, click hello **Settings** button</span></span>
3. <span data-ttu-id="8fe27-121">Wybierz hello **przezroczystego szyfrowania danych** opcji![][1]</span><span class="sxs-lookup"><span data-stu-id="8fe27-121">Select hello **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="8fe27-122">Wybierz hello **poza** ustawienie![][4]</span><span class="sxs-lookup"><span data-stu-id="8fe27-122">Select hello **Off** setting ![][4]</span></span>
5. <span data-ttu-id="8fe27-123">Wybierz **Zapisz**
   ![][5]</span><span class="sxs-lookup"><span data-stu-id="8fe27-123">Select **Save**
![][5]</span></span>  

## <a name="encryption-dmvs"></a><span data-ttu-id="8fe27-124">Szyfrowanie widoków DMV</span><span class="sxs-lookup"><span data-stu-id="8fe27-124">Encryption DMVs</span></span>
<span data-ttu-id="8fe27-125">Szyfrowanie może zostać potwierdzony z następujących widoków DMV hello:</span><span class="sxs-lookup"><span data-stu-id="8fe27-125">Encryption can be confirmed with hello following DMVs:</span></span>

* <span data-ttu-id="8fe27-126">[sys.Databases]</span><span class="sxs-lookup"><span data-stu-id="8fe27-126">[sys.databases]</span></span>
* <span data-ttu-id="8fe27-127">[sys.dm_pdw_nodes_database_encryption_keys]</span><span class="sxs-lookup"><span data-stu-id="8fe27-127">[sys.dm_pdw_nodes_database_encryption_keys]</span></span>

<!--MSDN references-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
[sys.Databases]: http://msdn.microsoft.com/library/ms178534.aspx
[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx

<!--Image references-->
[1]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings.png
[2]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-on.png
[3]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save.png
[4]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-off.png
[5]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save2.png

<!--Link references-->
