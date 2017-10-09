---
title: "aaaManage baz danych SQL Azure przy użyciu automatyzacji Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat jak hello usługi Automatyzacja Azure można baz danych Azure SQL toomanage używanych na dużą skalę."
services: sql-database, automation
documentationcenter: 
author: jodoglevy
manager: jhubbard
editor: monicar
ms.assetid: 77c262a1-9b93-456d-b3c7-b2f23bdfcd61
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: jhubbard
ms.openlocfilehash: d613cca32ba86e27b9c1b952c4e723ea7f07beb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-sql-databases-using-azure-automation"></a>Zarządzanie bazami danych SQL Azure przy użyciu usługi Automatyzacja Azure
W tym przewodniku przedstawiono usługi Automatyzacja Azure toohello i jak mogą być używane toosimplify zarządzania baz danych Azure SQL.

## <a name="what-is-azure-automation"></a>Co to jest Azure Automation?
[Automatyzacja Azure](https://azure.microsoft.com/services/automation/) jest usługą platformy Azure, dla uproszczenia zarządzania chmurą za pomocą automatyzacji procesu. Przy użyciu usługi Automatyzacja Azure, długotrwałe, ręcznych, podatnych i często powtarzanych zadań można automatycznych tooincrease niezawodności, wydajności i toovalue czasu dla Twojej organizacji.

Automatyzacja Azure umożliwia aparatowi wykonywania przepływów pracy wysoce niezawodne i wysokiej dostępności, która może obsłużyć toomeet potrzeb miarę rozwoju organizacji. W automatyzacji Azure procesów może być rozpoczęte ręcznie, przez systemy 3rd firmy lub w zaplanowanych odstępach czasu tak, aby zadania stanie dokładnie w razie potrzeby.

Obniżyć koszty operacyjne i zwolnić IT / toofocus personelu DevOps pracy dodającego wartość biznesową, przenosząc toobe zadań zarządzania z chmury uruchamiane automatycznie przez usługi Automatyzacja Azure.

## <a name="how-can-azure-automation-help-manage-azure-sql-databases"></a>Jak usługi Automatyzacja Azure ułatwia zarządzanie bazami danych Azure SQL?
Baza danych SQL Azure można zarządzać w automatyzacji Azure za pomocą hello [poleceń cmdlet programu PowerShell bazy danych SQL Azure](https://docs.microsoft.com/powershell/servicemanagement/azure.sqldatabase/v1.6.1/azure.sqldatabase/) dostępnych w hello [narzędzia programu Azure PowerShell](/powershell/azure/overview). Usługi Automatyzacja Azure ma tych poleceń cmdlet programu PowerShell bazy danych SQL Azure fabrycznej hello, dzięki czemu można wykonywać wszystkie zadania zarządzania bazy danych SQL w ramach usługi hello. Tych poleceń cmdlet usługi Automatyzacja Azure, za pomocą poleceń cmdlet powitania dla innych usług platformy Azure, tooautomate złożone zadania może również łączyć 3 systemów firm i usług Azure.

Automatyzacja Azure jest również toocommunicate możliwości hello z serwerami SQL bezpośrednio, wysyłając poleceń SQL przy użyciu programu PowerShell.

Witaj [galerię elementów runbook usługi Automatyzacja Azure](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) zawiera szereg produktu zespołu i społeczność elementów runbook tooget pracy automatyzacji zarządzania bazami danych SQL Azure, innych usług platformy Azure i 3 systemów firm. Galeria elementów runbook obejmują:

* [Uruchamianie zapytań SQL na bazie danych programu SQL Server](https://gallery.technet.microsoft.com/scriptcenter/How-to-use-a-SQL-Command-be77f9d2)
* [Skalowanie w pionie (w górę lub w dół) bazy danych SQL Azure zgodnie z harmonogramem](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-e957354f)
* [Obciąć tabeli SQL, jeśli zbliża się do maksymalnego rozmiaru bazy danych](https://gallery.technet.microsoft.com/scriptcenter/Azure-Automation-Your-SQL-30f8736b)
* [Indeks tabel w bazie danych SQL Azure, jeśli są one bardzo pofragmentowane](https://gallery.technet.microsoft.com/scriptcenter/Indexes-tables-in-an-Azure-73a2a8ea)

## <a name="next-steps"></a>Następne kroki
Teraz, kiedy znasz już podstawy hello usługi Automatyzacja Azure i jak można baz danych Azure SQL toomanage używane, należy wykonać te toolearn łącza więcej informacji na temat automatyzacji Azure.

* [Omówienie usługi Automatyzacja Azure](../automation/automation-intro.md)
* [Mój pierwszy element Runbook](../automation/automation-first-runbook-graphical.md)
* [Mapa uczenia usługi Automatyzacja Azure](https://azure.microsoft.com/documentation/learning-paths/automation/)
* [Automatyzacja Azure: Agenta programu SQL w chmurze hello](https://azure.microsoft.com/blog/2014/06/26/azure-automation-your-sql-agent-in-the-cloud/) 

