---
title: "aaaManage zarządzanie interfejsami API Azure przy użyciu usługi Automatyzacja Azure"
description: "Więcej informacji na temat sposobu hello usługi Automatyzacja Azure może być używane toomanage Azure API Management."
services: api-management, automation
documentationcenter: 
author: csand-msft
manager: eamono
editor: 
ms.assetid: 2e53c9af-f738-47f8-b1b6-593050a7c51b
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 05b8e3cad786fa701feb88f7b6d9629f16686d15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-api-management-using-azure-automation"></a><span data-ttu-id="20ca9-103">Zarządzanie Azure API Management przy użyciu usługi Automatyzacja Azure</span><span class="sxs-lookup"><span data-stu-id="20ca9-103">Managing Azure API Management using Azure Automation</span></span>
<span data-ttu-id="20ca9-104">W tym przewodniku przedstawiono usługi Automatyzacja Azure toohello i jak mogą być używane toosimplify zarządzania usługi Azure API Management.</span><span class="sxs-lookup"><span data-stu-id="20ca9-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of Azure API Management.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="20ca9-105">Co to jest Azure Automation?</span><span class="sxs-lookup"><span data-stu-id="20ca9-105">What is Azure Automation?</span></span>
<span data-ttu-id="20ca9-106">[Automatyzacja Azure](https://azure.microsoft.com/services/automation/) jest usługą platformy Azure, dla uproszczenia zarządzania chmurą za pomocą automatyzacji procesu.</span><span class="sxs-lookup"><span data-stu-id="20ca9-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="20ca9-107">Zadania ręczne, powtarzane długotrwałe i podatne na błędy przy użyciu usługi Automatyzacja Azure, może być automatycznych tooincrease niezawodności, wydajności i toovalue czasu dla Twojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="20ca9-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="20ca9-108">Automatyzacja Azure umożliwia aparatowi wykonywania przepływów pracy wysoce niezawodne, wysokiej dostępności, która może obsłużyć toomeet potrzeb.</span><span class="sxs-lookup"><span data-stu-id="20ca9-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales toomeet your needs.</span></span> <span data-ttu-id="20ca9-109">W automatyzacji Azure procesów może być rozpoczęte ręcznie, przez systemy 3rd firmy lub w zaplanowanych odstępach czasu tak, aby zadania stanie dokładnie w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="20ca9-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="20ca9-110">Obniżenie kosztów operacyjnych i zwolnić IT i toofocus personelu DevOps pracy dodającego wartość biznesową, przenosząc toobe zadań zarządzania z chmury uruchamiane automatycznie przez usługi Automatyzacja Azure.</span><span class="sxs-lookup"><span data-stu-id="20ca9-110">Reduce operational overhead and free up IT and DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-api-management"></a><span data-ttu-id="20ca9-111">Jak usługi Automatyzacja Azure ułatwia zarządzanie Azure API Management?</span><span class="sxs-lookup"><span data-stu-id="20ca9-111">How can Azure Automation help manage Azure API Management?</span></span>
<span data-ttu-id="20ca9-112">Zarządzanie interfejsami API można zarządzać w automatyzacji Azure za pomocą hello [polecenia cmdlet programu Windows PowerShell dla interfejsu API usługi Azure API Management](https://azure.microsoft.com/updates/full-set-of-windows-powershell-cmdlets-for-azure-api-management-api/).</span><span class="sxs-lookup"><span data-stu-id="20ca9-112">API Management can be managed in Azure Automation by using hello [Windows PowerShell cmdlets for Azure API Management API](https://azure.microsoft.com/updates/full-set-of-windows-powershell-cmdlets-for-azure-api-management-api/).</span></span> <span data-ttu-id="20ca9-113">W automatyzacji Azure można napisać tooperform skrypty przepływu pracy programu PowerShell wiele zadań zarządzania interfejsu API za pomocą poleceń cmdlet hello.</span><span class="sxs-lookup"><span data-stu-id="20ca9-113">Within Azure Automation you can write PowerShell workflow scripts tooperform many of your API Management tasks using hello cmdlets.</span></span> <span data-ttu-id="20ca9-114">Tych poleceń cmdlet usługi Automatyzacja Azure, za pomocą poleceń cmdlet powitania dla innych usług platformy Azure, tooautomate złożone zadania może również łączyć 3 systemów firm i usług Azure.</span><span class="sxs-lookup"><span data-stu-id="20ca9-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="20ca9-115">Oto kilka przykładów użycia interfejsu API zarządzania przy użyciu automatyzacji:</span><span class="sxs-lookup"><span data-stu-id="20ca9-115">Here are some examples of using API Management with Automation:</span></span>

* [<span data-ttu-id="20ca9-116">Zarządzanie interfejsami API Azure — używanie programu PowerShell na potrzeby tworzenia kopii zapasowych i przywracania</span><span class="sxs-lookup"><span data-stu-id="20ca9-116">Azure API Management – Using PowerShell for backup and restore</span></span>](https://blogs.msdn.microsoft.com/katriend/2015/10/02/azure-api-management-using-powershell-for-backup-and-restore/)

## <a name="next-steps"></a><span data-ttu-id="20ca9-117">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="20ca9-117">Next Steps</span></span>
<span data-ttu-id="20ca9-118">Teraz, kiedy znasz już podstawy hello usługi Automatyzacja Azure i jak mogą być używane toomanage Azure API Management, wykonaj te więcej toolearn łącza.</span><span class="sxs-lookup"><span data-stu-id="20ca9-118">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure API Management, follow these links toolearn more.</span></span>

* <span data-ttu-id="20ca9-119">Zobacz hello usługi Automatyzacja Azure [Wprowadzenie — samouczek](../automation/automation-first-runbook-graphical.md).</span><span class="sxs-lookup"><span data-stu-id="20ca9-119">See hello Azure Automation [getting started tutorial](../automation/automation-first-runbook-graphical.md).</span></span>

