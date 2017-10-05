---
title: "Zarządzanie aplikacją sieci Web Azure przy użyciu automatyzacji Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat sposobu usługi Automatyzacja Azure może służyć do zarządzania aplikacji sieci Web platformy Azure."
services: app-service\web, automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: c960a44f-f941-401d-afba-a4bc0f0394eb
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: magoedte
ms.openlocfilehash: a96332346747114620ee6ebd2a2d0c4417d4a213
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="managing-azure-web-app-using-azure-automation"></a><span data-ttu-id="84c8c-103">Zarządzanie aplikacją sieci Web platformy Azure przy użyciu usługi Automatyzacja Azure</span><span class="sxs-lookup"><span data-stu-id="84c8c-103">Managing Azure Web App using Azure Automation</span></span>
<span data-ttu-id="84c8c-104">W tym przewodniku przedstawiono usługi Automatyzacja Azure i jak może służyć do uproszczenia zarządzania aplikacji sieci Web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="84c8c-104">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of Azure Web App.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="84c8c-105">Co to jest Azure Automation?</span><span class="sxs-lookup"><span data-stu-id="84c8c-105">What is Azure Automation?</span></span>
<span data-ttu-id="84c8c-106">[Automatyzacja Azure](../automation/automation-intro.md) jest usługą platformy Azure, dla uproszczenia zarządzania chmurą za pomocą automatyzacji procesu.</span><span class="sxs-lookup"><span data-stu-id="84c8c-106">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="84c8c-107">Przy użyciu automatyzacji Azure, ręczne, powtarzane, długotrwałe i podatne na błędy zadań można zautomatyzować, aby zwiększyć niezawodność, wydajność i wartość czasu dla Twojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="84c8c-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span></span>

<span data-ttu-id="84c8c-108">Automatyzacja Azure umożliwia aparatowi wykonywania przepływów pracy wysoce niezawodne, wysokiej dostępności, która może obsłużyć do własnych potrzeb.</span><span class="sxs-lookup"><span data-stu-id="84c8c-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales to meet your needs.</span></span> <span data-ttu-id="84c8c-109">W automatyzacji Azure procesów może być rozpoczęte ręcznie, przez systemy 3rd firmy lub w zaplanowanych odstępach czasu tak, aby zadania stanie dokładnie w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="84c8c-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="84c8c-110">Obniżenie kosztów operacyjnych i zwolnić IT i pracownicy DevOps skupić się na pracy dodającego wartość biznesową przez przeniesienie zadań zarządzania chmury do automatycznego uruchamiania przez usługi Automatyzacja Azure.</span><span class="sxs-lookup"><span data-stu-id="84c8c-110">Reduce operational overhead and free up IT and DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-web-app"></a><span data-ttu-id="84c8c-111">Jak usługi Automatyzacja Azure ułatwia zarządzanie aplikacją sieci Web Azure?</span><span class="sxs-lookup"><span data-stu-id="84c8c-111">How can Azure Automation help manage Azure Web App?</span></span>
<span data-ttu-id="84c8c-112">Aplikacja sieci Web można zarządzać w automatyzacji Azure za pomocą poleceń cmdlet programu PowerShell, które są dostępne w [modułów programu Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="84c8c-112">Web App can be managed in Azure Automation by using the PowerShell cmdlets that are available in the [Azure PowerShell modules](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="84c8c-113">Możesz [zainstalować te polecenia cmdlet programu PowerShell aplikacji sieci Web automatyzacji Azure](https://azure.microsoft.com/blog/announcing-azure-resource-manager-support-azure-automation-runbooks/), dzięki czemu można wykonywać wszystkie zadania zarządzania aplikacji sieci Web w ramach usługi.</span><span class="sxs-lookup"><span data-stu-id="84c8c-113">You can [install these Web App PowerShell cmdlets in Azure Automation](https://azure.microsoft.com/blog/announcing-azure-resource-manager-support-azure-automation-runbooks/), so that you can perform all of your Web App management tasks within the service.</span></span> <span data-ttu-id="84c8c-114">Można również skojarzyć te polecenia cmdlet usługi Automatyzacja Azure, za pomocą poleceń cmdlet dla innych usług platformy Azure do zautomatyzowania złożonych zadań 3 systemów firm i usług Azure.</span><span class="sxs-lookup"><span data-stu-id="84c8c-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services to automate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="84c8c-115">Oto kilka przykładów Zarządzanie usługami aplikacji przy użyciu automatyzacji:</span><span class="sxs-lookup"><span data-stu-id="84c8c-115">Here are some examples of managing App Services with Automation:</span></span>

* [<span data-ttu-id="84c8c-116">Skrypty do zarządzania aplikacjami sieci Web</span><span class="sxs-lookup"><span data-stu-id="84c8c-116">Scripts for managing Web Apps</span></span>](https://azure.microsoft.com/documentation/scripts/)

## <a name="next-steps"></a><span data-ttu-id="84c8c-117">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="84c8c-117">Next steps</span></span>
<span data-ttu-id="84c8c-118">Teraz, kiedy znasz już podstawy usługi Automatyzacja Azure i jak może służyć do zarządzania aplikacji sieci Web platformy Azure, skorzystaj z poniższych linków, aby dowiedzieć się więcej na temat automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="84c8c-118">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure Web App, follow these links to learn more about Azure Automation.</span></span>

* <span data-ttu-id="84c8c-119">Zobacz automatyzacji Azure [Wprowadzenie — samouczek](../automation/automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="84c8c-119">See the Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md)</span></span>

