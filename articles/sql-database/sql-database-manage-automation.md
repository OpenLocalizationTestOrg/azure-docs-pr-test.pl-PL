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
# <a name="managing-azure-sql-databases-using-azure-automation"></a><span data-ttu-id="b7a3d-103">Zarządzanie bazami danych SQL Azure przy użyciu usługi Automatyzacja Azure</span><span class="sxs-lookup"><span data-stu-id="b7a3d-103">Managing Azure SQL Databases using Azure Automation</span></span>
<span data-ttu-id="b7a3d-104">W tym przewodniku przedstawiono usługi Automatyzacja Azure toohello i jak mogą być używane toosimplify zarządzania baz danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="b7a3d-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of your Azure SQL databases.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="b7a3d-105">Co to jest Azure Automation?</span><span class="sxs-lookup"><span data-stu-id="b7a3d-105">What is Azure Automation?</span></span>
<span data-ttu-id="b7a3d-106">[Automatyzacja Azure](https://azure.microsoft.com/services/automation/) jest usługą platformy Azure, dla uproszczenia zarządzania chmurą za pomocą automatyzacji procesu.</span><span class="sxs-lookup"><span data-stu-id="b7a3d-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="b7a3d-107">Przy użyciu usługi Automatyzacja Azure, długotrwałe, ręcznych, podatnych i często powtarzanych zadań można automatycznych tooincrease niezawodności, wydajności i toovalue czasu dla Twojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="b7a3d-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="b7a3d-108">Automatyzacja Azure umożliwia aparatowi wykonywania przepływów pracy wysoce niezawodne i wysokiej dostępności, która może obsłużyć toomeet potrzeb miarę rozwoju organizacji.</span><span class="sxs-lookup"><span data-stu-id="b7a3d-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales toomeet your needs as your organization grows.</span></span> <span data-ttu-id="b7a3d-109">W automatyzacji Azure procesów może być rozpoczęte ręcznie, przez systemy 3rd firmy lub w zaplanowanych odstępach czasu tak, aby zadania stanie dokładnie w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="b7a3d-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="b7a3d-110">Obniżyć koszty operacyjne i zwolnić IT / toofocus personelu DevOps pracy dodającego wartość biznesową, przenosząc toobe zadań zarządzania z chmury uruchamiane automatycznie przez usługi Automatyzacja Azure.</span><span class="sxs-lookup"><span data-stu-id="b7a3d-110">Lower operational overhead and free up IT / DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-sql-databases"></a><span data-ttu-id="b7a3d-111">Jak usługi Automatyzacja Azure ułatwia zarządzanie bazami danych Azure SQL?</span><span class="sxs-lookup"><span data-stu-id="b7a3d-111">How can Azure Automation help manage Azure SQL databases?</span></span>
<span data-ttu-id="b7a3d-112">Baza danych SQL Azure można zarządzać w automatyzacji Azure za pomocą hello [poleceń cmdlet programu PowerShell bazy danych SQL Azure](https://docs.microsoft.com/powershell/servicemanagement/azure.sqldatabase/v1.6.1/azure.sqldatabase/) dostępnych w hello [narzędzia programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b7a3d-112">Azure SQL Database can be managed in Azure Automation by using hello [Azure SQL Database PowerShell cmdlets](https://docs.microsoft.com/powershell/servicemanagement/azure.sqldatabase/v1.6.1/azure.sqldatabase/) that are available in hello [Azure PowerShell tools](/powershell/azure/overview).</span></span> <span data-ttu-id="b7a3d-113">Usługi Automatyzacja Azure ma tych poleceń cmdlet programu PowerShell bazy danych SQL Azure fabrycznej hello, dzięki czemu można wykonywać wszystkie zadania zarządzania bazy danych SQL w ramach usługi hello.</span><span class="sxs-lookup"><span data-stu-id="b7a3d-113">Azure Automation has these Azure SQL Database PowerShell cmdlets available out of hello box, so that you can perform all of your SQL DB management tasks within hello service.</span></span> <span data-ttu-id="b7a3d-114">Tych poleceń cmdlet usługi Automatyzacja Azure, za pomocą poleceń cmdlet powitania dla innych usług platformy Azure, tooautomate złożone zadania może również łączyć 3 systemów firm i usług Azure.</span><span class="sxs-lookup"><span data-stu-id="b7a3d-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="b7a3d-115">Automatyzacja Azure jest również toocommunicate możliwości hello z serwerami SQL bezpośrednio, wysyłając poleceń SQL przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b7a3d-115">Azure Automation also has hello ability toocommunicate with SQL servers directly, by issuing SQL commands using PowerShell.</span></span>

<span data-ttu-id="b7a3d-116">Witaj [galerię elementów runbook usługi Automatyzacja Azure](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) zawiera szereg produktu zespołu i społeczność elementów runbook tooget pracy automatyzacji zarządzania bazami danych SQL Azure, innych usług platformy Azure i 3 systemów firm.</span><span class="sxs-lookup"><span data-stu-id="b7a3d-116">hello [Azure Automation runbook gallery](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contains a variety of product team and community runbooks tooget started automating management of Azure SQL Databases, other Azure services, and 3rd party systems.</span></span> <span data-ttu-id="b7a3d-117">Galeria elementów runbook obejmują:</span><span class="sxs-lookup"><span data-stu-id="b7a3d-117">Gallery runbooks include:</span></span>

* [<span data-ttu-id="b7a3d-118">Uruchamianie zapytań SQL na bazie danych programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="b7a3d-118">Run SQL queries against a SQL Server database</span></span>](https://gallery.technet.microsoft.com/scriptcenter/How-to-use-a-SQL-Command-be77f9d2)
* [<span data-ttu-id="b7a3d-119">Skalowanie w pionie (w górę lub w dół) bazy danych SQL Azure zgodnie z harmonogramem</span><span class="sxs-lookup"><span data-stu-id="b7a3d-119">Vertically scale (up or down) an Azure SQL Database on a schedule</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-e957354f)
* [<span data-ttu-id="b7a3d-120">Obciąć tabeli SQL, jeśli zbliża się do maksymalnego rozmiaru bazy danych</span><span class="sxs-lookup"><span data-stu-id="b7a3d-120">Truncate a SQL table if its database approaches its maximum size</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Azure-Automation-Your-SQL-30f8736b)
* [<span data-ttu-id="b7a3d-121">Indeks tabel w bazie danych SQL Azure, jeśli są one bardzo pofragmentowane</span><span class="sxs-lookup"><span data-stu-id="b7a3d-121">Index tables in an Azure SQL Database if they are highly fragmented</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Indexes-tables-in-an-Azure-73a2a8ea)

## <a name="next-steps"></a><span data-ttu-id="b7a3d-122">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b7a3d-122">Next steps</span></span>
<span data-ttu-id="b7a3d-123">Teraz, kiedy znasz już podstawy hello usługi Automatyzacja Azure i jak można baz danych Azure SQL toomanage używane, należy wykonać te toolearn łącza więcej informacji na temat automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="b7a3d-123">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure SQL databases, follow these links toolearn more about Azure Automation.</span></span>

* [<span data-ttu-id="b7a3d-124">Omówienie usługi Automatyzacja Azure</span><span class="sxs-lookup"><span data-stu-id="b7a3d-124">Azure Automation Overview</span></span>](../automation/automation-intro.md)
* [<span data-ttu-id="b7a3d-125">Mój pierwszy element Runbook</span><span class="sxs-lookup"><span data-stu-id="b7a3d-125">My first runbook</span></span>](../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="b7a3d-126">Mapa uczenia usługi Automatyzacja Azure</span><span class="sxs-lookup"><span data-stu-id="b7a3d-126">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)
* [<span data-ttu-id="b7a3d-127">Automatyzacja Azure: Agenta programu SQL w chmurze hello</span><span class="sxs-lookup"><span data-stu-id="b7a3d-127">Azure Automation: Your SQL Agent in hello Cloud</span></span>](https://azure.microsoft.com/blog/2014/06/26/azure-automation-your-sql-agent-in-the-cloud/) 

