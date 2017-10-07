---
title: "Omówienie grup dostępności serwera — maszyny wirtualne Azure - aaaSQL | Dokumentacja firmy Microsoft"
description: "W tym artykule przedstawiono grup dostępności programu SQL Server na maszynach wirtualnych Azure."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 601eebb1-fc2c-4f5b-9c05-0e6ffd0e5334
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/13/2017
ms.author: mikeray
ms.openlocfilehash: ecac8b8c5073021af2aa22a05490bb8c4c20ed17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-sql-server-always-on-availability-groups-on-azure-virtual-machines"></a>Wprowadzenie do programu SQL Server zawsze włączonych grup dostępności na maszynach wirtualnych Azure #

W tym artykule przedstawiono grup dostępności programu SQL Server na maszynach wirtualnych platformy Azure. 

Zawsze włączone grupy dostępności na maszynach wirtualnych platformy Azure są podobne tooAlways dotyczących grup dostępności lokalnie. Aby uzyskać więcej informacji, zobacz [zawsze włączonych grup dostępności (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx). 

Witaj diagram przedstawia hello części pełną grupy dostępności serwera SQL w maszynach wirtualnych platformy Azure.

![Grupy dostępności](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

Witaj Najważniejsza różnica dla grupy dostępności w maszynach wirtualnych platformy Azure jest, który hello maszyn wirtualnych platformy Azure, wymagają [modułu równoważenia obciążenia](../../../load-balancer/load-balancer-overview.md). Moduł równoważenia obciążenia Hello przechowuje hello adresów IP dla odbiornika grupy dostępności hello. Jeśli masz więcej niż jednej grupy dostępności w każdej grupie wymaga odbiornik. Jeden moduł równoważenia obciążenia może obsługiwać wiele odbiorników.

Gdy wszystko jest gotowe toobuild aroup dostępności programu SQL Server na maszynach wirtualnych platformy Azure, można znaleźć samouczki toothese.

## <a name="automatically-create-an-availability-group-from-a-template"></a>Automatycznie utworzyć grupy dostępności na podstawie szablonu

[Konfigurowanie zawsze włączonej grupy dostępności w maszynie Wirtualnej platformy Azure automatycznie - Resource Manager](virtual-machines-windows-portal-sql-alwayson-availability-groups.md)

## <a name="manually-create-an-availability-group-in-azure-portal"></a>Ręcznie utwórz grupę dostępności w portalu Azure

Można również utworzyć maszyny wirtualne hello samodzielnie bez hello szablonu. Najpierw należy ukończyć powitalnych wymagania wstępne, a następnie utworzyć grupy dostępności hello. Zobacz hello następujące tematy: 

- [Konfigurowanie wymagań wstępnych dla programu SQL Server zawsze włączonych grup dostępności na maszynach wirtualnych platformy Azure](virtual-machines-windows-portal-sql-availability-group-prereq.md)

- [Utwórz zawsze włączonej grupy dostępności tooimprove dostępności i odzyskiwania po awarii](virtual-machines-windows-portal-sql-availability-group-tutorial.md)

## <a name="next-steps"></a>Następne kroki

[Konfigurowanie programu SQL Server, zawsze w grupie dostępności na maszynach wirtualnych Azure w różnych regionach](virtual-machines-windows-portal-sql-availability-group-dr.md).
