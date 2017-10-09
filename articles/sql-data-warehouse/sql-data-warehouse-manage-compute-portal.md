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
# <a name="manage-compute-power-in-azure-sql-data-warehouse-azure-portal"></a>Zarządzanie moc obliczeniową w usłudze Azure SQL Data Warehouse (Azure portal)
> [!div class="op_single_selector"]
> * [Omówienie](sql-data-warehouse-manage-compute-overview.md)
> * [Portal](sql-data-warehouse-manage-compute-portal.md)
> * [PowerShell](sql-data-warehouse-manage-compute-powershell.md)
> * [REST](sql-data-warehouse-manage-compute-rest-api.md)
> * [TSQL](sql-data-warehouse-manage-compute-tsql.md)
>
>


## <a name="scale-compute-power"></a>Moc obliczeniową skali
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

zasoby obliczeniowe toochange:

1. Otwórz hello [portalu Azure][Azure portal], otwórz bazę danych i kliknij przycisk **skali**.

    ![Kliknij polecenie Skaluj][1]
2. W bloku skali hello hello suwak w lewo lub w prawo toochange hello wartości DWU ustawienia.

    ![Przesuń suwak][2]
3. Kliknij pozycję **Zapisz**. Zostanie wyświetlony komunikat potwierdzenia. Kliknij przycisk **tak** tooconfirm lub **nie** toocancel.

    ![Klikanie pozycji Zapisz.][3]

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a>Wstrzymaj obliczeń
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

toopause bazy danych:

1. Otwórz hello [portalu Azure] [ Azure portal] i otworzyć bazy danych. Zwróć uwagę, że hello jest w stanie **Online**.

    ![Stan online][6]
2. toosuspend zasobów obliczeniowych i pamięć, kliknij przycisk **Wstrzymaj**, a następnie zostanie wyświetlony komunikat potwierdzenia. Kliknij przycisk **tak** tooconfirm lub **nie** toocancel.

    ![Upewnij się, Wstrzymaj][7]
3. Podczas uruchamiania hello bazy danych SQL Data Warehouse, stan hello jest **wstrzymywanie**.
4. Gdy stan hello jest **wstrzymana**, odbywa się hello operację wstrzymywania i nie zawierają dla jednostek dwu.

    ![Stan wstrzymania][4]

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a>Wznów obliczeń
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

tooresume bazy danych:

1. Otwórz hello [portalu Azure] [ Azure portal] i otworzyć bazy danych. Zwróć uwagę, że hello jest w stanie **Paused**.

    ![Wstrzymaj bazy danych][4]
2. tooresume hello bazy danych kliknij **Start**, a następnie zostanie wyświetlony komunikat potwierdzenia. Kliknij przycisk **tak** tooconfirm lub **nie** toocancel.

    ![Upewnij się, Wznów][5]
3. Podczas uruchamiania hello bazy danych SQL Data Warehouse, hello stanu jest "Wznawianie".
4. Gdy stan hello jest **online**, hello bazy danych jest gotowy.

    ![Stan online][6]

<a name="next-steps-bk"></a>

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji, zobacz [omówienie zarządzania][Management overview].

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
