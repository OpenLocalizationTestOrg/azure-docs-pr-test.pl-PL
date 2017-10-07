---
title: "aaaManage aplikacji sieci Web platformy Azure przy użyciu automatyzacji Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat sposobu hello usługi Automatyzacja Azure może być używane toomanage aplikacji sieci Web platformy Azure."
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
ms.openlocfilehash: 6d80351a2927f26753cfbaead6e1c0c3c94e86e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-web-app-using-azure-automation"></a><span data-ttu-id="48f65-103">Zarządzanie aplikacją sieci Web platformy Azure przy użyciu usługi Automatyzacja Azure</span><span class="sxs-lookup"><span data-stu-id="48f65-103">Managing Azure Web App using Azure Automation</span></span>
<span data-ttu-id="48f65-104">W tym przewodniku przedstawiono usługi Automatyzacja Azure toohello i jak mogą być używane toosimplify zarządzania aplikacji sieci Web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="48f65-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of Azure Web App.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="48f65-105">Co to jest Azure Automation?</span><span class="sxs-lookup"><span data-stu-id="48f65-105">What is Azure Automation?</span></span>
<span data-ttu-id="48f65-106">[Automatyzacja Azure](../automation/automation-intro.md) jest usługą platformy Azure, dla uproszczenia zarządzania chmurą za pomocą automatyzacji procesu.</span><span class="sxs-lookup"><span data-stu-id="48f65-106">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="48f65-107">Zadania ręczne, powtarzane długotrwałe i podatne na błędy przy użyciu usługi Automatyzacja Azure, może być automatycznych tooincrease niezawodności, wydajności i toovalue czasu dla Twojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="48f65-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="48f65-108">Automatyzacja Azure umożliwia aparatowi wykonywania przepływów pracy wysoce niezawodne, wysokiej dostępności, która może obsłużyć toomeet potrzeb.</span><span class="sxs-lookup"><span data-stu-id="48f65-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales toomeet your needs.</span></span> <span data-ttu-id="48f65-109">W automatyzacji Azure procesów może być rozpoczęte ręcznie, przez systemy 3rd firmy lub w zaplanowanych odstępach czasu tak, aby zadania stanie dokładnie w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="48f65-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="48f65-110">Obniżenie kosztów operacyjnych i zwolnić IT i toofocus personelu DevOps pracy dodającego wartość biznesową, przenosząc toobe zadań zarządzania z chmury uruchamiane automatycznie przez usługi Automatyzacja Azure.</span><span class="sxs-lookup"><span data-stu-id="48f65-110">Reduce operational overhead and free up IT and DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-web-app"></a><span data-ttu-id="48f65-111">Jak usługi Automatyzacja Azure ułatwia zarządzanie aplikacją sieci Web Azure?</span><span class="sxs-lookup"><span data-stu-id="48f65-111">How can Azure Automation help manage Azure Web App?</span></span>
<span data-ttu-id="48f65-112">Aplikacja sieci Web można zarządzać w automatyzacji Azure za pomocą poleceń cmdlet programu PowerShell hello, które są dostępne w hello [modułów programu Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="48f65-112">Web App can be managed in Azure Automation by using hello PowerShell cmdlets that are available in hello [Azure PowerShell modules](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="48f65-113">Możesz [zainstalować te polecenia cmdlet programu PowerShell aplikacji sieci Web automatyzacji Azure](https://azure.microsoft.com/blog/announcing-azure-resource-manager-support-azure-automation-runbooks/), dzięki czemu można wykonywać wszystkie zadania zarządzania w ramach usługi hello aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="48f65-113">You can [install these Web App PowerShell cmdlets in Azure Automation](https://azure.microsoft.com/blog/announcing-azure-resource-manager-support-azure-automation-runbooks/), so that you can perform all of your Web App management tasks within hello service.</span></span> <span data-ttu-id="48f65-114">Tych poleceń cmdlet usługi Automatyzacja Azure, za pomocą poleceń cmdlet hello innych usług Azure tooautomate złożonych zadań, może również łączyć 3 systemów firm i usług Azure.</span><span class="sxs-lookup"><span data-stu-id="48f65-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="48f65-115">Oto kilka przykładów Zarządzanie usługami aplikacji przy użyciu automatyzacji:</span><span class="sxs-lookup"><span data-stu-id="48f65-115">Here are some examples of managing App Services with Automation:</span></span>

* [<span data-ttu-id="48f65-116">Skrypty do zarządzania aplikacjami sieci Web</span><span class="sxs-lookup"><span data-stu-id="48f65-116">Scripts for managing Web Apps</span></span>](https://azure.microsoft.com/documentation/scripts/)

## <a name="next-steps"></a><span data-ttu-id="48f65-117">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="48f65-117">Next steps</span></span>
<span data-ttu-id="48f65-118">Teraz, kiedy znasz już podstawy hello usługi Automatyzacja Azure i jak mogą być używane toomanage aplikacji sieci Web platformy Azure, wykonaj te toolearn łącza więcej informacji na temat automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="48f65-118">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure Web App, follow these links toolearn more about Azure Automation.</span></span>

* <span data-ttu-id="48f65-119">Zobacz hello usługi Automatyzacja Azure [Wprowadzenie — samouczek](../automation/automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="48f65-119">See hello Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md)</span></span>

