---
title: "Usługi w chmurze Azure przy użyciu automatyzacji Azure aaaManage | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat jak hello usługi Automatyzacja Azure mogą być używane toomanage usług w chmurze Azure na dużą skalę."
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
ms.openlocfilehash: 8e920fb94955466bfec71cc332444f5f0ee497a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-cloud-services-using-azure-automation"></a><span data-ttu-id="4af4a-103">Zarządzania usługami w chmurze Azure przy użyciu usługi Automatyzacja Azure</span><span class="sxs-lookup"><span data-stu-id="4af4a-103">Managing Azure Cloud Services using Azure Automation</span></span>
<span data-ttu-id="4af4a-104">W tym przewodniku przedstawiono usługi Automatyzacja Azure toohello i jak mogą być używane toosimplify zarządzania usług w chmurze Azure.</span><span class="sxs-lookup"><span data-stu-id="4af4a-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of your Azure cloud services.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="4af4a-105">Co to jest Azure Automation?</span><span class="sxs-lookup"><span data-stu-id="4af4a-105">What is Azure Automation?</span></span>
<span data-ttu-id="4af4a-106">[Automatyzacja Azure](https://azure.microsoft.com/services/automation/) jest usługą platformy Azure, dla uproszczenia zarządzania chmurą za pomocą automatyzacji procesu.</span><span class="sxs-lookup"><span data-stu-id="4af4a-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="4af4a-107">Przy użyciu usługi Automatyzacja Azure, długotrwałe, ręcznych, podatnych i często powtarzanych zadań można automatycznych tooincrease niezawodności, wydajności i toovalue czasu dla Twojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="4af4a-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="4af4a-108">Automatyzacja Azure umożliwia aparatowi wykonywania przepływów pracy wysoce niezawodne i wysokiej dostępności, która może obsłużyć toomeet potrzeb miarę rozwoju organizacji.</span><span class="sxs-lookup"><span data-stu-id="4af4a-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales toomeet your needs as your organization grows.</span></span> <span data-ttu-id="4af4a-109">W automatyzacji Azure procesów może być rozpoczęte ręcznie, przez systemy 3rd firmy lub w zaplanowanych odstępach czasu tak, aby zadania stanie dokładnie w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="4af4a-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="4af4a-110">Obniżyć koszty operacyjne i zwolnić IT / toofocus personelu DevOps pracy dodającego wartość biznesową, przenosząc toobe zadań zarządzania z chmury uruchamiane automatycznie przez usługi Automatyzacja Azure.</span><span class="sxs-lookup"><span data-stu-id="4af4a-110">Lower operational overhead and free up IT / DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-cloud-services"></a><span data-ttu-id="4af4a-111">Jak usługi Automatyzacja Azure ułatwia zarządzanie usług w chmurze Azure?</span><span class="sxs-lookup"><span data-stu-id="4af4a-111">How can Azure Automation help manage Azure cloud services?</span></span>
<span data-ttu-id="4af4a-112">Usługi w chmurze platformy Azure można zarządzać w automatyzacji Azure za pomocą poleceń cmdlet programu PowerShell hello, które są dostępne w hello [narzędzia programu Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="4af4a-112">Azure cloud services can be managed in Azure Automation by using hello PowerShell cmdlets that are available in hello [Azure PowerShell tools](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="4af4a-113">Automatyzacja Azure ma te chmury usługi poleceń cmdlet programu PowerShell dostępne fabrycznej hello tak, aby można było wykonać wszystkie zadania zarządzania usługi chmury w ramach usługi hello.</span><span class="sxs-lookup"><span data-stu-id="4af4a-113">Azure Automation has these cloud service PowerShell cmdlets available out of hello box, so that you can perform all of your cloud service management tasks within hello service.</span></span> <span data-ttu-id="4af4a-114">Tych poleceń cmdlet usługi Automatyzacja Azure, za pomocą poleceń cmdlet powitania dla innych usług platformy Azure, tooautomate złożone zadania może również łączyć 3 systemów firm i usług Azure.</span><span class="sxs-lookup"><span data-stu-id="4af4a-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="4af4a-115">Przykładowe zastosowania toomanage usługi Automatyzacja Azure, które obejmują usługi w chmurze Azure:</span><span class="sxs-lookup"><span data-stu-id="4af4a-115">Some example uses of Azure Automation toomanage Azure Cloud Services include:</span></span>

* [<span data-ttu-id="4af4a-116">Ciągłej wdrożenia usługi w chmurze przy każdej aktualizacji cscfg lub cspkg w magazynie obiektów Blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="4af4a-116">Continous deployment of a Cloud Service whenever cscfg or cspkg is updated in Azure Blob storage</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Continuous-Deployment-of-A-eeebf3a6)
* [<span data-ttu-id="4af4a-117">Ponowne uruchomienie wystąpienia usługi w chmurze równolegle domeny uaktualnienia pojedynczo</span><span class="sxs-lookup"><span data-stu-id="4af4a-117">Rebooting Cloud Service instances in parallel, one upgrade domain at a time</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Reboot-Cloud-Service-PaaS-b337a06d)

## <a name="next-steps"></a><span data-ttu-id="4af4a-118">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4af4a-118">Next Steps</span></span>
<span data-ttu-id="4af4a-119">Teraz, kiedy znasz już podstawy hello usługi Automatyzacja Azure i jak mogą być używane toomanage usług w chmurze Azure, wykonaj te toolearn łącza więcej informacji na temat automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="4af4a-119">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure cloud services, follow these links toolearn more about Azure Automation.</span></span>

* [<span data-ttu-id="4af4a-120">Omówienie usługi Automatyzacja Azure</span><span class="sxs-lookup"><span data-stu-id="4af4a-120">Azure Automation Overview</span></span>](../automation/automation-intro.md)
* [<span data-ttu-id="4af4a-121">Mój pierwszy element Runbook</span><span class="sxs-lookup"><span data-stu-id="4af4a-121">My first runbook</span></span>](../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="4af4a-122">Mapa uczenia usługi Automatyzacja Azure</span><span class="sxs-lookup"><span data-stu-id="4af4a-122">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)
