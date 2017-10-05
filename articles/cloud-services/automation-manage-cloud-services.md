---
title: "Zarządzanie przy użyciu automatyzacji Azure usługi w chmurze Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat jak usługa Automatyzacja Azure może służyć do zarządzania usługami w chmurze platformy Azure na dużą skalę."
services: cloud-services, automation
documentationcenter: 
author: jodoglevy
manager: timlt
editor: 
ms.assetid: 3789810a-2892-4eef-bf29-c781c1b5af48
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2016
ms.author: timlt
ms.openlocfilehash: 6b5acac1b8647c324988c316cd5602b3dba98a1d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-cloud-services-using-azure-automation"></a><span data-ttu-id="9627e-103">Zarządzania usługami w chmurze Azure przy użyciu usługi Automatyzacja Azure</span><span class="sxs-lookup"><span data-stu-id="9627e-103">Managing Azure Cloud Services using Azure Automation</span></span>
<span data-ttu-id="9627e-104">W tym przewodniku przedstawiono usługi Automatyzacja Azure oraz jak on używany w celu uproszczenia zarządzania usług w chmurze Azure.</span><span class="sxs-lookup"><span data-stu-id="9627e-104">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of your Azure cloud services.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="9627e-105">Co to jest Azure Automation?</span><span class="sxs-lookup"><span data-stu-id="9627e-105">What is Azure Automation?</span></span>
<span data-ttu-id="9627e-106">[Automatyzacja Azure](https://azure.microsoft.com/services/automation/) jest usługą platformy Azure, dla uproszczenia zarządzania chmurą za pomocą automatyzacji procesu.</span><span class="sxs-lookup"><span data-stu-id="9627e-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="9627e-107">Przy użyciu usługi Automatyzacja Azure, można zautomatyzować długotrwałe, ręcznych, podatnych i często powtarzanych zadań, aby zwiększyć niezawodność, wydajność i wartość czasu dla Twojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="9627e-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span></span>

<span data-ttu-id="9627e-108">Automatyzacja Azure umożliwia aparatowi wykonywania przepływów pracy wysoce niezawodne i wysokiej dostępności, która może obsłużyć do własnych potrzeb miarę rozwoju organizacji.</span><span class="sxs-lookup"><span data-stu-id="9627e-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales to meet your needs as your organization grows.</span></span> <span data-ttu-id="9627e-109">W automatyzacji Azure procesów może być rozpoczęte ręcznie, przez systemy 3rd firmy lub w zaplanowanych odstępach czasu tak, aby zadania stanie dokładnie w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="9627e-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="9627e-110">Obniżyć koszty operacyjne i zwolnić IT / personel DevOps skupić się na pracy, który dodaje biznesowych wartość przez przeniesienie zadań zarządzania chmury do automatycznego uruchamiania przez usługi Automatyzacja Azure.</span><span class="sxs-lookup"><span data-stu-id="9627e-110">Lower operational overhead and free up IT / DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-cloud-services"></a><span data-ttu-id="9627e-111">Jak usługi Automatyzacja Azure ułatwia zarządzanie usług w chmurze Azure?</span><span class="sxs-lookup"><span data-stu-id="9627e-111">How can Azure Automation help manage Azure cloud services?</span></span>
<span data-ttu-id="9627e-112">Usługi w chmurze platformy Azure można zarządzać w automatyzacji Azure za pomocą poleceń cmdlet programu PowerShell, które są dostępne w [narzędzia programu Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="9627e-112">Azure cloud services can be managed in Azure Automation by using the PowerShell cmdlets that are available in the [Azure PowerShell tools](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="9627e-113">Usługi Automatyzacja Azure ma te chmury usługi poleceń cmdlet programu PowerShell dostępne fabrycznej, dzięki czemu można wykonywać wszystkie zadania zarządzania usługi chmury w ramach usługi.</span><span class="sxs-lookup"><span data-stu-id="9627e-113">Azure Automation has these cloud service PowerShell cmdlets available out of the box, so that you can perform all of your cloud service management tasks within the service.</span></span> <span data-ttu-id="9627e-114">Można również skojarzyć te polecenia cmdlet usługi Automatyzacja Azure, za pomocą poleceń cmdlet dla innych usług Azure, aby zautomatyzować złożone zadania 3 systemów firm i usług Azure.</span><span class="sxs-lookup"><span data-stu-id="9627e-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="9627e-115">Niektóre przykładowe zastosowania usługi Automatyzacja Azure do zarządzania usługami w chmurze Azure obejmują:</span><span class="sxs-lookup"><span data-stu-id="9627e-115">Some example uses of Azure Automation to manage Azure Cloud Services include:</span></span>

* [<span data-ttu-id="9627e-116">Ciągłej wdrożenia usługi w chmurze przy każdej aktualizacji cscfg lub cspkg w magazynie obiektów Blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9627e-116">Continous deployment of a Cloud Service whenever cscfg or cspkg is updated in Azure Blob storage</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Continuous-Deployment-of-A-eeebf3a6)
* [<span data-ttu-id="9627e-117">Ponowne uruchomienie wystąpienia usługi w chmurze równolegle domeny uaktualnienia pojedynczo</span><span class="sxs-lookup"><span data-stu-id="9627e-117">Rebooting Cloud Service instances in parallel, one upgrade domain at a time</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Reboot-Cloud-Service-PaaS-b337a06d)

## <a name="next-steps"></a><span data-ttu-id="9627e-118">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9627e-118">Next Steps</span></span>
<span data-ttu-id="9627e-119">Teraz, kiedy znasz już podstawy usługi Automatyzacja Azure i jak może służyć do zarządzania usługami w chmurze platformy Azure, skorzystaj z poniższych linków, aby dowiedzieć się więcej na temat automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="9627e-119">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure cloud services, follow these links to learn more about Azure Automation.</span></span>

* [<span data-ttu-id="9627e-120">Omówienie usługi Automatyzacja Azure</span><span class="sxs-lookup"><span data-stu-id="9627e-120">Azure Automation Overview</span></span>](../automation/automation-intro.md)
* [<span data-ttu-id="9627e-121">Mój pierwszy element Runbook</span><span class="sxs-lookup"><span data-stu-id="9627e-121">My first runbook</span></span>](../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="9627e-122">Mapa uczenia usługi Automatyzacja Azure</span><span class="sxs-lookup"><span data-stu-id="9627e-122">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)
