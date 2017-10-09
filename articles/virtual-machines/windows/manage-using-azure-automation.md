---
title: "aaaManage maszyn wirtualnych przy użyciu automatyzacji Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o jak hello usługi Automatyzacja Azure można toomanage używanych maszyn wirtualnych platformy Azure na dużą skalę."
services: virtual-machines-windows, automation
documentationcenter: 
author: jodoglevy
manager: timlt
editor: 
ms.assetid: ce49f83a-f409-42ee-af74-a8ea2caa9ae8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2016
ms.author: timlt
ms.openlocfilehash: bfe7b3a51b6e82bd7cd5b0a83df7226476ed4f36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-virtual-machines-using-azure-automation"></a><span data-ttu-id="4cc08-103">Zarządzanie usługą Azure Virtual Machines przy użyciu usługi Azure Automation</span><span class="sxs-lookup"><span data-stu-id="4cc08-103">Managing Azure Virtual Machines using Azure Automation</span></span>
<span data-ttu-id="4cc08-104">W tym przewodniku przedstawiono usługi Automatyzacja Azure toohello i jak mogą być używane toosimplify Zarządzanie maszynach wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4cc08-104">This guide introduces you toohello Azure Automation service and how it can be used toosimplify managing your Azure virtual machines.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="4cc08-105">Co to jest Azure Automation?</span><span class="sxs-lookup"><span data-stu-id="4cc08-105">What is Azure Automation?</span></span>
<span data-ttu-id="4cc08-106">[Automatyzacja Azure](https://azure.microsoft.com/services/automation/) jest usługą platformy Azure, dla uproszczenia zarządzania chmurą za pomocą automatyzacji procesu.</span><span class="sxs-lookup"><span data-stu-id="4cc08-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="4cc08-107">Za pomocą usługi Automatyzacja Azure, długotrwałe, ręcznych, podatnych i często powtarzanych zadań może być automatycznych tooincrease niezawodności, wydajności i czasu na wartość dla organizacji.</span><span class="sxs-lookup"><span data-stu-id="4cc08-107">By using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated tooincrease reliability, efficiency, and time-to-value for your organization.</span></span>

<span data-ttu-id="4cc08-108">Automatyzacja Azure umożliwia aparatowi wykonywania przepływów pracy wysoce niezawodne i wysokiej dostępności, która może obsłużyć toomeet potrzeb miarę rozwoju organizacji.</span><span class="sxs-lookup"><span data-stu-id="4cc08-108">Azure Automation provides a highly reliable and highly available workflow execution engine that scales toomeet your needs as your organization grows.</span></span> <span data-ttu-id="4cc08-109">W automatyzacji Azure procesów może być rozpoczęte ręcznie, przez systemy innych firm lub w zaplanowanych odstępach czasu tak, aby zadania się tak zdarzyć, dokładnie tak, gdy jest to wymagane.</span><span class="sxs-lookup"><span data-stu-id="4cc08-109">In Azure Automation, processes can be kicked off manually, by third-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="4cc08-110">Można zmniejszyć nakłady operacyjne i zwolnić IT oraz DevOps toofocus pracy dodającego wartość biznesową, uruchamiając chmury zadań zarządzania automatycznie przy użyciu automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="4cc08-110">You can lower operational overhead and free up IT and DevOps staff toofocus on work that adds business value by running your cloud management tasks automatically with Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-virtual-machines"></a><span data-ttu-id="4cc08-111">Jak usługi Automatyzacja Azure ułatwia zarządzanie maszyn wirtualnych platformy Azure?</span><span class="sxs-lookup"><span data-stu-id="4cc08-111">How can Azure Automation help manage Azure virtual machines?</span></span>
<span data-ttu-id="4cc08-112">Maszyny wirtualne można zarządzać w automatyzacji Azure za pomocą [programu Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="4cc08-112">Virtual machines can be managed in Azure Automation by using [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="4cc08-113">Automatyzacja Azure obejmuje hello poleceń cmdlet programu Azure PowerShell, więc można wykonywać wszystkie zadania zarządzania maszyny wirtualnej w ramach usługi hello.</span><span class="sxs-lookup"><span data-stu-id="4cc08-113">Azure Automation includes hello Azure PowerShell cmdlets, so you can perform all of your virtual machine management tasks within hello service.</span></span> <span data-ttu-id="4cc08-114">Między usługami platformy Azure i systemów innych firm może łączyć się również polecenia cmdlet hello w automatyzacji Azure za pomocą poleceń cmdlet powitania dla innych usług platformy Azure, tooautomate złożone zadania.</span><span class="sxs-lookup"><span data-stu-id="4cc08-114">You can also pair hello cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and third-party systems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4cc08-115">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4cc08-115">Next steps</span></span>
<span data-ttu-id="4cc08-116">Teraz, kiedy znasz już podstawy hello usługi Automatyzacja Azure i jak mogą być używane toomanage maszyn wirtualnych platformy Azure, Dowiedz się więcej:</span><span class="sxs-lookup"><span data-stu-id="4cc08-116">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure virtual machines, learn more:</span></span>

* [<span data-ttu-id="4cc08-117">Omówienie usługi Automatyzacja Azure</span><span class="sxs-lookup"><span data-stu-id="4cc08-117">Azure Automation Overview</span></span>](../../automation/automation-intro.md)
* [<span data-ttu-id="4cc08-118">Mój pierwszy element Runbook</span><span class="sxs-lookup"><span data-stu-id="4cc08-118">My first runbook</span></span>](../../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="4cc08-119">Mapa uczenia usługi Automatyzacja Azure</span><span class="sxs-lookup"><span data-stu-id="4cc08-119">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)

