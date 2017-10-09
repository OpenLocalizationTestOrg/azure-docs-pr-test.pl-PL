---
title: "aaaManage obliczeniowe zasilania w usłudze Azure SQL Data Warehouse (Azure portal) | Dokumentacja firmy Microsoft"
description: "Mocy obliczeniowej toomanage zadania portalu Azure. Zasoby obliczeniowe skali przez dostosowanie wartości dwu. Lub wstrzymywanie i wznawianie koszty toosave zasoby obliczeniowe."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 233b0da5-4abd-4d1d-9586-4ccc5f50b071
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: b2e84b3763e97ce88c190eecfb64b2d06f727229
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-azure-portal"></a><span data-ttu-id="334e5-105">Zarządzanie moc obliczeniową w usłudze Azure SQL Data Warehouse (Azure portal)</span><span class="sxs-lookup"><span data-stu-id="334e5-105">Manage compute power in Azure SQL Data Warehouse (Azure portal)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="334e5-106">Omówienie</span><span class="sxs-lookup"><span data-stu-id="334e5-106">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="334e5-107">Portal</span><span class="sxs-lookup"><span data-stu-id="334e5-107">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="334e5-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="334e5-108">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="334e5-109">REST</span><span class="sxs-lookup"><span data-stu-id="334e5-109">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="334e5-110">TSQL</span><span class="sxs-lookup"><span data-stu-id="334e5-110">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>


## <a name="scale-compute-power"></a><span data-ttu-id="334e5-111">Moc obliczeniową skali</span><span class="sxs-lookup"><span data-stu-id="334e5-111">Scale compute power</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="334e5-112">zasoby obliczeniowe toochange:</span><span class="sxs-lookup"><span data-stu-id="334e5-112">toochange compute resources:</span></span>

1. <span data-ttu-id="334e5-113">Otwórz hello [portalu Azure][Azure portal], otwórz bazę danych i kliknij przycisk **skali**.</span><span class="sxs-lookup"><span data-stu-id="334e5-113">Open hello [Azure portal][Azure portal], open your database, and click **Scale**.</span></span>

    ![Kliknij polecenie Skaluj][1]
2. <span data-ttu-id="334e5-115">W bloku skali hello hello suwak w lewo lub w prawo toochange hello wartości DWU ustawienia.</span><span class="sxs-lookup"><span data-stu-id="334e5-115">In hello Scale blade, move hello slider left or right toochange hello DWU setting.</span></span>

    ![Przesuń suwak][2]
3. <span data-ttu-id="334e5-117">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="334e5-117">Click **Save**.</span></span> <span data-ttu-id="334e5-118">Zostanie wyświetlony komunikat potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="334e5-118">A confirmation message appears.</span></span> <span data-ttu-id="334e5-119">Kliknij przycisk **tak** tooconfirm lub **nie** toocancel.</span><span class="sxs-lookup"><span data-stu-id="334e5-119">Click **yes** tooconfirm or **no** toocancel.</span></span>

    ![Klikanie pozycji Zapisz.][3]

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="334e5-121">Wstrzymaj obliczeń</span><span class="sxs-lookup"><span data-stu-id="334e5-121">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="334e5-122">toopause bazy danych:</span><span class="sxs-lookup"><span data-stu-id="334e5-122">toopause a database:</span></span>

1. <span data-ttu-id="334e5-123">Otwórz hello [portalu Azure] [ Azure portal] i otworzyć bazy danych.</span><span class="sxs-lookup"><span data-stu-id="334e5-123">Open hello [Azure portal][Azure portal] and open your database.</span></span> <span data-ttu-id="334e5-124">Zwróć uwagę, że hello jest w stanie **Online**.</span><span class="sxs-lookup"><span data-stu-id="334e5-124">Notice that hello Status is **Online**.</span></span>

    ![Stan online][6]
2. <span data-ttu-id="334e5-126">toosuspend zasobów obliczeniowych i pamięć, kliknij przycisk **Wstrzymaj**, a następnie zostanie wyświetlony komunikat potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="334e5-126">toosuspend compute and memory resources, click **Pause**, and then a confirmation message appears.</span></span> <span data-ttu-id="334e5-127">Kliknij przycisk **tak** tooconfirm lub **nie** toocancel.</span><span class="sxs-lookup"><span data-stu-id="334e5-127">Click **yes** tooconfirm or **no** toocancel.</span></span>

    ![Upewnij się, Wstrzymaj][7]
3. <span data-ttu-id="334e5-129">Podczas uruchamiania hello bazy danych SQL Data Warehouse, stan hello jest **wstrzymywanie**.</span><span class="sxs-lookup"><span data-stu-id="334e5-129">While SQL Data Warehouse is starting hello database, hello status is **Pausing**.</span></span>
4. <span data-ttu-id="334e5-130">Gdy stan hello jest **wstrzymana**, odbywa się hello operację wstrzymywania i nie zawierają dla jednostek dwu.</span><span class="sxs-lookup"><span data-stu-id="334e5-130">When hello status is **Paused**, hello pause operation is done and you are no longer being charged for DWUs.</span></span>

    ![Stan wstrzymania][4]

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="334e5-132">Wznów obliczeń</span><span class="sxs-lookup"><span data-stu-id="334e5-132">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="334e5-133">tooresume bazy danych:</span><span class="sxs-lookup"><span data-stu-id="334e5-133">tooresume a database:</span></span>

1. <span data-ttu-id="334e5-134">Otwórz hello [portalu Azure] [ Azure portal] i otworzyć bazy danych.</span><span class="sxs-lookup"><span data-stu-id="334e5-134">Open hello [Azure portal][Azure portal] and open your database.</span></span> <span data-ttu-id="334e5-135">Zwróć uwagę, że hello jest w stanie **Paused**.</span><span class="sxs-lookup"><span data-stu-id="334e5-135">Notice that hello Status is **Paused**.</span></span>

    ![Wstrzymaj bazy danych][4]
2. <span data-ttu-id="334e5-137">tooresume hello bazy danych kliknij **Start**, a następnie zostanie wyświetlony komunikat potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="334e5-137">tooresume hello database click **Start**, and then a confirmation message appears.</span></span> <span data-ttu-id="334e5-138">Kliknij przycisk **tak** tooconfirm lub **nie** toocancel.</span><span class="sxs-lookup"><span data-stu-id="334e5-138">Click **yes** tooconfirm or **no** toocancel.</span></span>

    ![Upewnij się, Wznów][5]
3. <span data-ttu-id="334e5-140">Podczas uruchamiania hello bazy danych SQL Data Warehouse, hello stanu jest "Wznawianie".</span><span class="sxs-lookup"><span data-stu-id="334e5-140">While SQL Data Warehouse is starting hello database, hello status is "Resuming".</span></span>
4. <span data-ttu-id="334e5-141">Gdy stan hello jest **online**, hello bazy danych jest gotowy.</span><span class="sxs-lookup"><span data-stu-id="334e5-141">When hello status is **online**, hello database is ready.</span></span>

    ![Stan online][6]

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="334e5-143">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="334e5-143">Next steps</span></span>
<span data-ttu-id="334e5-144">Aby uzyskać więcej informacji, zobacz [omówienie zarządzania][Management overview].</span><span class="sxs-lookup"><span data-stu-id="334e5-144">For more information, see [Management overview][Management overview].</span></span>

<!--Image references-->
[1]: ./media/sql-data-warehouse-manage-compute-portal/click-scale.png
[2]: ./media/sql-data-warehouse-manage-compute-portal/move-slider.png
[3]: ./media/sql-data-warehouse-manage-compute-portal/click-save.png
[4]: ./media/sql-data-warehouse-manage-compute-portal/resume-database.png
[5]: ./media/sql-data-warehouse-manage-compute-portal/resume-confirm.png
[6]: ./media/sql-data-warehouse-manage-compute-portal/pause-database.png
[7]: ./media/sql-data-warehouse-manage-compute-portal/pause-confirm.png

<!--Article references-->
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->


<!--Other Web references-->

[Azure portal]: http://portal.azure.com/
