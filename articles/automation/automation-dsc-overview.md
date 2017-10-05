---
title: "Przegląd usługi Konfiguracja DSC automatyzacji Azure | Dokumentacja firmy Microsoft"
description: "Omówienie programu żądanego stanu konfiguracji (Konfiguracja DSC automatyzacji Azure), jego warunki i znane problemy"
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
keywords: "PowerShell dsc, konfiguracji żądanego stanu, azure dsc środowiska powershell"
ms.assetid: fd40cb68-c1a6-48c3-bba2-710b607d1555
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 06/15/2017
ms.author: eslesar
ms.openlocfilehash: 468321fa6863d78bc0d179fbe5c2ed6195040d50
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-dsc-overview"></a><span data-ttu-id="04fbc-104">Przegląd usługi Konfiguracja DSC automatyzacji Azure</span><span class="sxs-lookup"><span data-stu-id="04fbc-104">Azure Automation DSC Overview</span></span>

<span data-ttu-id="04fbc-105">Konfiguracja DSC usługi Automatyzacja Azure jest usługą platformy Azure, która umożliwia zapis, zarządzanie i skompilować konfiguracji żądanego stanu środowiska PowerShell (DSC) [konfiguracje](https://msdn.microsoft.com/powershell/dsc/configurations), zaimportuj [zasobów DSC](https://msdn.microsoft.com/powershell/dsc/resources)i przypisz konfiguracje do węzły docelowe w chmurze.</span><span class="sxs-lookup"><span data-stu-id="04fbc-105">Azure Automation DSC is an Azure service that allows you to write, manage, and compile PowerShell Desired State Configuration (DSC) [configurations](https://msdn.microsoft.com/powershell/dsc/configurations), import [DSC Resources](https://msdn.microsoft.com/powershell/dsc/resources), and assign configurations to target nodes, all in the cloud.</span></span>

## <a name="why-use-azure-automation-dsc"></a><span data-ttu-id="04fbc-106">Dlaczego warto korzystać z usługi Konfiguracja DSC automatyzacji Azure</span><span class="sxs-lookup"><span data-stu-id="04fbc-106">Why use Azure Automation DSC</span></span>

<span data-ttu-id="04fbc-107">Konfiguracja DSC automatyzacji Azure zapewnia kilka zalet w porównaniu z używaniem konfiguracji DSC poza platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="04fbc-107">Azure Automation DSC provides several advantages over using DSC outside of Azure.</span></span>

### <a name="built-in-pull-server"></a><span data-ttu-id="04fbc-108">Serwerem ściągania wbudowane</span><span class="sxs-lookup"><span data-stu-id="04fbc-108">Built-in pull server</span></span>

<span data-ttu-id="04fbc-109">Udostępnia usługi Automatyzacja Azure [serwera ściągania usługi Konfiguracja DSC](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver) tak, aby węzły docelowe automatycznie otrzymują konfiguracje, dostosowywać się do żądanego stanu i raportować o swojej zgodności.</span><span class="sxs-lookup"><span data-stu-id="04fbc-109">Azure Automation provides a [DSC pull server](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver) so that target nodes automatically receive configurations, conform to the desired state, and report back on their compliance.</span></span>
<span data-ttu-id="04fbc-110">Z serwerem ściągania wbudowanych w automatyzacji Azure eliminuje konieczność Konfigurowanie i konserwacja serwera ściągania.</span><span class="sxs-lookup"><span data-stu-id="04fbc-110">The built-in pull server in Azure Automation eliminates the need to set up and maintain your own pull server.</span></span>
<span data-ttu-id="04fbc-111">Automatyzacja Azure można kierować wirtualnych lub fizycznych systemu Windows lub Linux maszyny, w chmurze lub lokalnie.</span><span class="sxs-lookup"><span data-stu-id="04fbc-111">Azure Automation can target virtual or physical Windows or Linux machines, in the cloud or on-premises.</span></span>

### <a name="management-of-all-your-dsc-artifacts"></a><span data-ttu-id="04fbc-112">Zarządzanie artefaktów DSC</span><span class="sxs-lookup"><span data-stu-id="04fbc-112">Management of all your DSC artifacts</span></span>

<span data-ttu-id="04fbc-113">Konfiguracja DSC automatyzacji Azure oferuje tej samej warstwie zarządzania [konfiguracji żądanego stanu środowiska PowerShell](https://msdn.microsoft.com/powershell/dsc/overview) jako usługi Automatyzacja Azure oferuje dla skryptów środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="04fbc-113">Azure Automation DSC brings the same management layer to [PowerShell Desired State Configuration](https://msdn.microsoft.com/powershell/dsc/overview) as Azure Automation offers for PowerShell scripting.</span></span>

<span data-ttu-id="04fbc-114">Z portalu Azure lub programu PowerShell można zarządzać wszystkie Twoje DSC konfiguracje, zasobów i węzły docelowe.</span><span class="sxs-lookup"><span data-stu-id="04fbc-114">From the Azure portal, or from PowerShell, you can manage all your DSC configurations, resources, and target nodes.</span></span>

![Zrzut ekranu przedstawiający blok usługi Automatyzacja Azure](./media/automation-dsc-overview/azure-automation-blade.png)

### <a name="import-reporting-data-into-log-analytics"></a><span data-ttu-id="04fbc-116">Importowanie danych raportowania do analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="04fbc-116">Import reporting data into Log Analytics</span></span>

<span data-ttu-id="04fbc-117">Węzły, które są zarządzane w usłudze Konfiguracja DSC automatyzacji Azure wysyłać szczegółowe dane raportów o stanie do serwera ściągania wbudowanych.</span><span class="sxs-lookup"><span data-stu-id="04fbc-117">Nodes that are managed with Azure Automation DSC send detailed reporting status data to the built-in pull server.</span></span>
<span data-ttu-id="04fbc-118">Można skonfigurować do wysyłania tych danych do swojego obszaru roboczego analizy dzienników programu Microsoft Operations Management Suite (OMS), konfiguracja DSC automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="04fbc-118">You can configure Azure Automation DSC to send this data to your Microsoft Operations Management Suite (OMS) Log Analytics workspace.</span></span>
<span data-ttu-id="04fbc-119">Aby dowiedzieć się, jak wysyłać dane o stanie DSC do obszaru roboczego analizy dzienników, zobacz [do przodu Konfiguracja DSC automatyzacji Azure raportowania danych do analizy dzienników OMS](automation-dsc-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="04fbc-119">To learn how to send DSC status data to your Log Analytics workspace, see [Forward Azure Automation DSC reporting data to OMS Log Analytics](automation-dsc-diagnostics.md).</span></span>

## <a name="introduction-video"></a><span data-ttu-id="04fbc-120">Wideo z wprowadzeniem</span><span class="sxs-lookup"><span data-stu-id="04fbc-120">Introduction video</span></span>

<span data-ttu-id="04fbc-121">Wolisz obejrzeć film niż przeczytać artykuł?</span><span class="sxs-lookup"><span data-stu-id="04fbc-121">Prefer watching to reading?</span></span> <span data-ttu-id="04fbc-122">Ma wygląd w poniższym klipie wideo z maja 2015 roku, po raz pierwszy ogłoszono Konfiguracja DSC automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="04fbc-122">Have a look at the following video from May 2015, when Azure Automation DSC was first announced.</span></span>

>[!NOTE]
><span data-ttu-id="04fbc-123">Koncepcje i cyklu życia omówione w tym wideo są poprawne, konfiguracja DSC automatyzacji Azure zanotowano znacznie, ponieważ ten film został zapisany.</span><span class="sxs-lookup"><span data-stu-id="04fbc-123">While the concepts and life cycle discussed in this video are correct, Azure Automation DSC has progressed a lot since this video was recorded.</span></span>
><span data-ttu-id="04fbc-124">Teraz jest ogólnie dostępna, ma znacznie bardziej rozległych interfejsu użytkownika w portalu Azure i obsługuje wiele dodatkowych funkcji.</span><span class="sxs-lookup"><span data-stu-id="04fbc-124">It is now generally available, has a much more extensive UI in the Azure portal, and supports many additional capabilities.</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3467/player]

## <a name="next-steps"></a><span data-ttu-id="04fbc-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="04fbc-125">Next steps</span></span>

* <span data-ttu-id="04fbc-126">Aby dowiedzieć się, aby dodać węzły mają być zarządzane w usłudze Konfiguracja DSC automatyzacji Azure, zobacz temat [dołączania komputerów do zarządzania przez Konfiguracja DSC automatyzacji Azure](automation-dsc-onboarding.md)</span><span class="sxs-lookup"><span data-stu-id="04fbc-126">To learn how to onboard nodes to be managed with Azure Automation DSC, see [Onboarding machines for management by Azure Automation DSC](automation-dsc-onboarding.md)</span></span>
* <span data-ttu-id="04fbc-127">Aby rozpocząć korzystanie z usługi Konfiguracja DSC automatyzacji Azure, zobacz [wprowadzenie do korzystania z usługi Konfiguracja DSC automatyzacji Azure](automation-dsc-getting-started.md)</span><span class="sxs-lookup"><span data-stu-id="04fbc-127">To get started using Azure Automation DSC, see [Getting started with Azure Automation DSC](automation-dsc-getting-started.md)</span></span>
* <span data-ttu-id="04fbc-128">Aby uzyskać informacje dotyczące kompilowania konfiguracji DSC, dzięki czemu można je przypisać do węzły docelowe, zobacz [kompilowania konfiguracji DSC automatyzacji Azure](automation-dsc-compile.md)</span><span class="sxs-lookup"><span data-stu-id="04fbc-128">To learn about compiling DSC configurations so that you can assign them to target nodes, see [Compiling configurations in Azure Automation DSC](automation-dsc-compile.md)</span></span>
* <span data-ttu-id="04fbc-129">Dokumentacja poleceń cmdlet programu PowerShell dla usługi Konfiguracja DSC automatyzacji Azure, aby zapoznać [poleceń cmdlet usługi Konfiguracja DSC automatyzacji Azure](/powershell/module/azurerm.automation/#automation)</span><span class="sxs-lookup"><span data-stu-id="04fbc-129">For PowerShell cmdlet reference for Azure Automation DSC, see [Azure Automation DSC cmdlets](/powershell/module/azurerm.automation/#automation)</span></span>
* <span data-ttu-id="04fbc-130">Aby uzyskać informacje o cenach, zobacz [cennik usługi Konfiguracja DSC automatyzacji Azure](https://azure.microsoft.com/pricing/details/automation/)</span><span class="sxs-lookup"><span data-stu-id="04fbc-130">For pricing information, see [Azure Automation DSC pricing](https://azure.microsoft.com/pricing/details/automation/)</span></span>
* <span data-ttu-id="04fbc-131">Aby zapoznać się z przykładem w potoku ciągłe wdrażanie przy użyciu usługi Konfiguracja DSC automatyzacji Azure, zobacz [ciągłe wdrażanie DSC automatyzacji Azure przy użyciu maszyn wirtualnych IaaS i Chocolatey](automation-dsc-cd-chocolatey.md)</span><span class="sxs-lookup"><span data-stu-id="04fbc-131">To see an example of using Azure Automation DSC in a continuous deployment pipeline, see  [Continuous Deployment to IaaS VMs Using Azure Automation DSC and Chocolatey](automation-dsc-cd-chocolatey.md)</span></span>