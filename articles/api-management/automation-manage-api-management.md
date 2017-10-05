---
title: "Zarządzanie Azure API Management przy użyciu usługi Automatyzacja Azure"
description: "Więcej informacji na temat sposobu usługi Automatyzacja Azure może służyć do zarządzania usługi Azure API Management."
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
ms.openlocfilehash: 73a1135482b88ea7c228bc8b228d47c57b2e70a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-api-management-using-azure-automation"></a><span data-ttu-id="307b8-103">Zarządzanie Azure API Management przy użyciu usługi Automatyzacja Azure</span><span class="sxs-lookup"><span data-stu-id="307b8-103">Managing Azure API Management using Azure Automation</span></span>
<span data-ttu-id="307b8-104">W tym przewodniku przedstawiono usługi Automatyzacja Azure oraz jak on używany w celu uproszczenia zarządzania usługi Azure API Management.</span><span class="sxs-lookup"><span data-stu-id="307b8-104">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of Azure API Management.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="307b8-105">Co to jest Azure Automation?</span><span class="sxs-lookup"><span data-stu-id="307b8-105">What is Azure Automation?</span></span>
<span data-ttu-id="307b8-106">[Automatyzacja Azure](https://azure.microsoft.com/services/automation/) jest usługą platformy Azure, dla uproszczenia zarządzania chmurą za pomocą automatyzacji procesu.</span><span class="sxs-lookup"><span data-stu-id="307b8-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="307b8-107">Przy użyciu automatyzacji Azure, ręczne, powtarzane, długotrwałe i podatne na błędy zadań można zautomatyzować, aby zwiększyć niezawodność, wydajność i wartość czasu dla Twojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="307b8-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span></span>

<span data-ttu-id="307b8-108">Automatyzacja Azure umożliwia aparatowi wykonywania przepływów pracy wysoce niezawodne, wysokiej dostępności, która może obsłużyć do własnych potrzeb.</span><span class="sxs-lookup"><span data-stu-id="307b8-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales to meet your needs.</span></span> <span data-ttu-id="307b8-109">W automatyzacji Azure procesów może być rozpoczęte ręcznie, przez systemy 3rd firmy lub w zaplanowanych odstępach czasu tak, aby zadania stanie dokładnie w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="307b8-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="307b8-110">Obniżenie kosztów operacyjnych i zwolnić IT i pracownicy DevOps skupić się na pracy dodającego wartość biznesową przez przeniesienie zadań zarządzania chmury do automatycznego uruchamiania przez usługi Automatyzacja Azure.</span><span class="sxs-lookup"><span data-stu-id="307b8-110">Reduce operational overhead and free up IT and DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-api-management"></a><span data-ttu-id="307b8-111">Jak usługi Automatyzacja Azure ułatwia zarządzanie Azure API Management?</span><span class="sxs-lookup"><span data-stu-id="307b8-111">How can Azure Automation help manage Azure API Management?</span></span>
<span data-ttu-id="307b8-112">Zarządzanie interfejsami API można zarządzać w automatyzacji Azure za pomocą [polecenia cmdlet programu Windows PowerShell dla interfejsu API usługi Azure API Management](https://azure.microsoft.com/updates/full-set-of-windows-powershell-cmdlets-for-azure-api-management-api/).</span><span class="sxs-lookup"><span data-stu-id="307b8-112">API Management can be managed in Azure Automation by using the [Windows PowerShell cmdlets for Azure API Management API](https://azure.microsoft.com/updates/full-set-of-windows-powershell-cmdlets-for-azure-api-management-api/).</span></span> <span data-ttu-id="307b8-113">W automatyzacji Azure można napisać skrypty przepływu pracy programu PowerShell do wykonywania wielu zadań interfejsu API zarządzania przy użyciu polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="307b8-113">Within Azure Automation you can write PowerShell workflow scripts to perform many of your API Management tasks using the cmdlets.</span></span> <span data-ttu-id="307b8-114">Można również skojarzyć te polecenia cmdlet usługi Automatyzacja Azure, za pomocą poleceń cmdlet dla innych usług Azure, aby zautomatyzować złożone zadania 3 systemów firm i usług Azure.</span><span class="sxs-lookup"><span data-stu-id="307b8-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="307b8-115">Oto kilka przykładów użycia interfejsu API zarządzania przy użyciu automatyzacji:</span><span class="sxs-lookup"><span data-stu-id="307b8-115">Here are some examples of using API Management with Automation:</span></span>

* [<span data-ttu-id="307b8-116">Zarządzanie interfejsami API Azure — używanie programu PowerShell na potrzeby tworzenia kopii zapasowych i przywracania</span><span class="sxs-lookup"><span data-stu-id="307b8-116">Azure API Management – Using PowerShell for backup and restore</span></span>](https://blogs.msdn.microsoft.com/katriend/2015/10/02/azure-api-management-using-powershell-for-backup-and-restore/)

## <a name="next-steps"></a><span data-ttu-id="307b8-117">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="307b8-117">Next Steps</span></span>
<span data-ttu-id="307b8-118">Teraz, kiedy znasz już podstawy usługi Automatyzacja Azure i jak może służyć do zarządzania usługi Azure API Management, skorzystaj z poniższych linków, aby dowiedzieć się więcej.</span><span class="sxs-lookup"><span data-stu-id="307b8-118">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure API Management, follow these links to learn more.</span></span>

* <span data-ttu-id="307b8-119">Zobacz automatyzacji Azure [Wprowadzenie — samouczek](../automation/automation-first-runbook-graphical.md).</span><span class="sxs-lookup"><span data-stu-id="307b8-119">See the Azure Automation [getting started tutorial](../automation/automation-first-runbook-graphical.md).</span></span>

