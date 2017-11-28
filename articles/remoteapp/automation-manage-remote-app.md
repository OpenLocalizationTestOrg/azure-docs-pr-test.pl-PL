---
title: "aaaManage usługi Azure RemoteApp przy użyciu automatyzacji Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat sposobu hello usługi Automatyzacja Azure może być używane toomanage usługi Azure RemoteApp."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 589f01ef-f9c1-4e7b-a040-1b46862d3544
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: magoedte;csand
ms.openlocfilehash: a4cb23e292c797256e971acb3b363b025f140f16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-remoteapp-using-azure-automation"></a><span data-ttu-id="f2ea8-103">Zarządzanie usługą Azure RemoteApp przy użyciu usługi Automatyzacja Azure</span><span class="sxs-lookup"><span data-stu-id="f2ea8-103">Managing Azure RemoteApp using Azure Automation</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f2ea8-104">Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="f2ea8-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="f2ea8-105">Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="f2ea8-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="f2ea8-106">W tym przewodniku przedstawiono usługi Automatyzacja Azure toohello i jak mogą być używane toosimplify zarządzania usługi Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="f2ea8-106">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of Azure RemoteApp.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="f2ea8-107">Co to jest Azure Automation?</span><span class="sxs-lookup"><span data-stu-id="f2ea8-107">What is Azure Automation?</span></span>
<span data-ttu-id="f2ea8-108">[Automatyzacja Azure](../automation/automation-intro.md) jest usługą platformy Azure, dla uproszczenia zarządzania chmurą za pomocą automatyzacji procesu.</span><span class="sxs-lookup"><span data-stu-id="f2ea8-108">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="f2ea8-109">Zadania ręczne, często powtarzanych długotrwałe i podatne na błędy przy użyciu usługi Automatyzacja Azure, może być automatycznych tooincrease niezawodności, wydajności i toovalue czasu dla Twojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="f2ea8-109">Using Azure Automation, manual, frequently-repeated, long-running, and error-prone tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="f2ea8-110">Automatyzacja Azure umożliwia aparatowi wykonywania przepływów pracy wysoce niezawodne, wysokiej dostępności, która może obsłużyć toomeet potrzeb.</span><span class="sxs-lookup"><span data-stu-id="f2ea8-110">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales toomeet your needs.</span></span> <span data-ttu-id="f2ea8-111">W automatyzacji Azure procesów może być rozpoczęte ręcznie, przez systemy 3rd firmy lub w zaplanowanych odstępach czasu tak, aby zadania stanie dokładnie w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="f2ea8-111">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="f2ea8-112">Obniżenie kosztów operacyjnych i zwolnić IT i toofocus personelu DevOps pracy dodającego wartość biznesową, przenosząc toobe zadań zarządzania z chmury uruchamiane automatycznie przez usługi Automatyzacja Azure.</span><span class="sxs-lookup"><span data-stu-id="f2ea8-112">Reduce operational overhead and free up IT and DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-remoteapp"></a><span data-ttu-id="f2ea8-113">Jak usługi Automatyzacja Azure ułatwia zarządzanie usługą Azure RemoteApp?</span><span class="sxs-lookup"><span data-stu-id="f2ea8-113">How can Azure Automation help manage Azure RemoteApp?</span></span>
<span data-ttu-id="f2ea8-114">Usługi RemoteApp można zarządzać w automatyzacji Azure za pomocą poleceń cmdlet programu PowerShell hello, które są dostępne w hello [narzędzia programu Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="f2ea8-114">RemoteApp can be managed in Azure Automation by using hello PowerShell cmdlets that are available in hello [Azure PowerShell tools](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="f2ea8-115">Automatyzacja Azure ma tych poleceń cmdlet środowiska PowerShell usługi RemoteApp fabrycznej hello tak, aby można było wykonać wszystkie zadania zarządzania w ramach usługi hello programów RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="f2ea8-115">Azure Automation has these RemoteApp PowerShell cmdlets available out of hello box, so that you can perform all of your RemoteApp management tasks within hello service.</span></span> <span data-ttu-id="f2ea8-116">Tych poleceń cmdlet usługi Automatyzacja Azure, za pomocą poleceń cmdlet powitania dla innych usług platformy Azure, tooautomate złożone zadania może również łączyć 3 systemów firm i usług Azure.</span><span class="sxs-lookup"><span data-stu-id="f2ea8-116">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2ea8-117">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f2ea8-117">Next steps</span></span>
<span data-ttu-id="f2ea8-118">Teraz, kiedy znasz już podstawy hello usługi Automatyzacja Azure i jak mogą być używane toomanage usługi Azure RemoteApp, wykonaj te toolearn łącza więcej informacji na temat automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="f2ea8-118">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure RemoteApp, follow these links toolearn more about Azure Automation.</span></span>

* <span data-ttu-id="f2ea8-119">Zobacz hello usługi Automatyzacja Azure [Wprowadzenie — samouczek](../automation/automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="f2ea8-119">See hello Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md)</span></span>

