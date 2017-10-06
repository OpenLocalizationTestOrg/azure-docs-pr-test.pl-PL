---
title: "Przegląd usługi Konfiguracja DSC automatyzacji aaaAzure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 5b8e5104c7b5bed848c015ac26a8b7d1f5b24de9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-dsc-overview"></a><span data-ttu-id="bb245-104">Przegląd usługi Konfiguracja DSC automatyzacji Azure</span><span class="sxs-lookup"><span data-stu-id="bb245-104">Azure Automation DSC Overview</span></span>

<span data-ttu-id="bb245-105">Konfiguracja DSC usługi Automatyzacja Azure jest usługą platformy Azure, która pozwala toowrite, zarządzanie i skompilować konfiguracji żądanego stanu środowiska PowerShell (DSC) [konfiguracje](https://msdn.microsoft.com/powershell/dsc/configurations), zaimportuj [zasobów DSC](https://msdn.microsoft.com/powershell/dsc/resources)i przypisz węzły tootarget konfiguracje w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="bb245-105">Azure Automation DSC is an Azure service that allows you toowrite, manage, and compile PowerShell Desired State Configuration (DSC) [configurations](https://msdn.microsoft.com/powershell/dsc/configurations), import [DSC Resources](https://msdn.microsoft.com/powershell/dsc/resources), and assign configurations tootarget nodes, all in hello cloud.</span></span>

## <a name="why-use-azure-automation-dsc"></a><span data-ttu-id="bb245-106">Dlaczego warto korzystać z usługi Konfiguracja DSC automatyzacji Azure</span><span class="sxs-lookup"><span data-stu-id="bb245-106">Why use Azure Automation DSC</span></span>

<span data-ttu-id="bb245-107">Konfiguracja DSC automatyzacji Azure zapewnia kilka zalet w porównaniu z używaniem konfiguracji DSC poza platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="bb245-107">Azure Automation DSC provides several advantages over using DSC outside of Azure.</span></span>

### <a name="built-in-pull-server"></a><span data-ttu-id="bb245-108">Serwerem ściągania wbudowane</span><span class="sxs-lookup"><span data-stu-id="bb245-108">Built-in pull server</span></span>

<span data-ttu-id="bb245-109">Udostępnia usługi Automatyzacja Azure [serwera ściągania usługi Konfiguracja DSC](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver) tak, aby węzły docelowe automatycznie otrzymują konfiguracje, jest zgodna z toohello żądany stan i raportować o swojej zgodności.</span><span class="sxs-lookup"><span data-stu-id="bb245-109">Azure Automation provides a [DSC pull server](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver) so that target nodes automatically receive configurations, conform toohello desired state, and report back on their compliance.</span></span>
<span data-ttu-id="bb245-110">powitania serwera ściągania wbudowanych w automatyzacji Azure eliminuje hello tooset muszą się i obsługa serwera ściągania.</span><span class="sxs-lookup"><span data-stu-id="bb245-110">hello built-in pull server in Azure Automation eliminates hello need tooset up and maintain your own pull server.</span></span>
<span data-ttu-id="bb245-111">Automatyzacja Azure można kierować wirtualnych lub fizycznych systemu Windows lub Linux maszyny, w chmurze hello lub lokalnie.</span><span class="sxs-lookup"><span data-stu-id="bb245-111">Azure Automation can target virtual or physical Windows or Linux machines, in hello cloud or on-premises.</span></span>

### <a name="management-of-all-your-dsc-artifacts"></a><span data-ttu-id="bb245-112">Zarządzanie artefaktów DSC</span><span class="sxs-lookup"><span data-stu-id="bb245-112">Management of all your DSC artifacts</span></span>

<span data-ttu-id="bb245-113">Konfiguracja DSC automatyzacji Azure oferuje zbyt hello tego samego warstwa zarządzania[konfiguracji żądanego stanu programu PowerShell](https://msdn.microsoft.com/powershell/dsc/overview) jako usługi Automatyzacja Azure oferuje dla skryptów środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bb245-113">Azure Automation DSC brings hello same management layer too[PowerShell Desired State Configuration](https://msdn.microsoft.com/powershell/dsc/overview) as Azure Automation offers for PowerShell scripting.</span></span>

<span data-ttu-id="bb245-114">Z hello portalu Azure lub programu PowerShell można zarządzać wszystkie Twoje DSC konfiguracje, zasobów i węzły docelowe.</span><span class="sxs-lookup"><span data-stu-id="bb245-114">From hello Azure portal, or from PowerShell, you can manage all your DSC configurations, resources, and target nodes.</span></span>

![Zrzut ekranu przedstawiający blok usługi Automatyzacja Azure hello](./media/automation-dsc-overview/azure-automation-blade.png)

### <a name="import-reporting-data-into-log-analytics"></a><span data-ttu-id="bb245-116">Importowanie danych raportowania do analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="bb245-116">Import reporting data into Log Analytics</span></span>

<span data-ttu-id="bb245-117">Węzły, które są zarządzane w usłudze Konfiguracja DSC automatyzacji Azure Wyślij szczegółowy stan danych toohello ściągania wbudowanego serwera raportowania.</span><span class="sxs-lookup"><span data-stu-id="bb245-117">Nodes that are managed with Azure Automation DSC send detailed reporting status data toohello built-in pull server.</span></span>
<span data-ttu-id="bb245-118">Konfiguracja DSC automatyzacji Azure toosend można skonfigurować tego obszaru roboczego analizy dzienników programu Microsoft Operations Management Suite (OMS) tooyour danych.</span><span class="sxs-lookup"><span data-stu-id="bb245-118">You can configure Azure Automation DSC toosend this data tooyour Microsoft Operations Management Suite (OMS) Log Analytics workspace.</span></span>
<span data-ttu-id="bb245-119">toolearn toosend DSC stan danych tooyour obszaru roboczego analizy dzienników, zobacz temat [do przodu Konfiguracja DSC automatyzacji Azure raportowania tooOMS danych analizy dzienników](automation-dsc-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="bb245-119">toolearn how toosend DSC status data tooyour Log Analytics workspace, see [Forward Azure Automation DSC reporting data tooOMS Log Analytics](automation-dsc-diagnostics.md).</span></span>

## <a name="introduction-video"></a><span data-ttu-id="bb245-120">Wideo z wprowadzeniem</span><span class="sxs-lookup"><span data-stu-id="bb245-120">Introduction video</span></span>

<span data-ttu-id="bb245-121">Preferowane jest obserwowanie tooreading?</span><span class="sxs-lookup"><span data-stu-id="bb245-121">Prefer watching tooreading?</span></span> <span data-ttu-id="bb245-122">Ma wygląd na powitania po wideo z maja 2015 roku, po raz pierwszy ogłoszono Konfiguracja DSC automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="bb245-122">Have a look at hello following video from May 2015, when Azure Automation DSC was first announced.</span></span>

>[!NOTE]
><span data-ttu-id="bb245-123">Pojęcia hello i cyklem życia omówione w tym wideo są poprawne, konfiguracja DSC automatyzacji Azure zanotowano znacznie, ponieważ ten film został zapisany.</span><span class="sxs-lookup"><span data-stu-id="bb245-123">While hello concepts and life cycle discussed in this video are correct, Azure Automation DSC has progressed a lot since this video was recorded.</span></span>
><span data-ttu-id="bb245-124">Teraz jest ogólnie dostępna, ma znacznie bardziej rozległych interfejsu użytkownika w portalu Azure hello i obsługuje wiele dodatkowych funkcji.</span><span class="sxs-lookup"><span data-stu-id="bb245-124">It is now generally available, has a much more extensive UI in hello Azure portal, and supports many additional capabilities.</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3467/player]

## <a name="next-steps"></a><span data-ttu-id="bb245-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bb245-125">Next steps</span></span>

* <span data-ttu-id="bb245-126">toolearn tooonboard toobe węzłów zarządzanych za pomocą usługi Konfiguracja DSC automatyzacji Azure, zobacz [dołączania komputerów do zarządzania przez Konfiguracja DSC automatyzacji Azure](automation-dsc-onboarding.md)</span><span class="sxs-lookup"><span data-stu-id="bb245-126">toolearn how tooonboard nodes toobe managed with Azure Automation DSC, see [Onboarding machines for management by Azure Automation DSC](automation-dsc-onboarding.md)</span></span>
* <span data-ttu-id="bb245-127">tooget uruchomiony przy użyciu usługi Konfiguracja DSC automatyzacji Azure, zobacz [wprowadzenie do korzystania z usługi Konfiguracja DSC automatyzacji Azure](automation-dsc-getting-started.md)</span><span class="sxs-lookup"><span data-stu-id="bb245-127">tooget started using Azure Automation DSC, see [Getting started with Azure Automation DSC](automation-dsc-getting-started.md)</span></span>
* <span data-ttu-id="bb245-128">Zobacz toolearn o kompilowania konfiguracji DSC, dzięki czemu można je przypisać węzłów tootarget [kompilowania konfiguracji DSC automatyzacji Azure](automation-dsc-compile.md)</span><span class="sxs-lookup"><span data-stu-id="bb245-128">toolearn about compiling DSC configurations so that you can assign them tootarget nodes, see [Compiling configurations in Azure Automation DSC](automation-dsc-compile.md)</span></span>
* <span data-ttu-id="bb245-129">Dokumentacja poleceń cmdlet programu PowerShell dla usługi Konfiguracja DSC automatyzacji Azure, aby zapoznać [poleceń cmdlet usługi Konfiguracja DSC automatyzacji Azure](/powershell/module/azurerm.automation/#automation)</span><span class="sxs-lookup"><span data-stu-id="bb245-129">For PowerShell cmdlet reference for Azure Automation DSC, see [Azure Automation DSC cmdlets](/powershell/module/azurerm.automation/#automation)</span></span>
* <span data-ttu-id="bb245-130">Aby uzyskać informacje o cenach, zobacz [cennik usługi Konfiguracja DSC automatyzacji Azure](https://azure.microsoft.com/pricing/details/automation/)</span><span class="sxs-lookup"><span data-stu-id="bb245-130">For pricing information, see [Azure Automation DSC pricing](https://azure.microsoft.com/pricing/details/automation/)</span></span>
* <span data-ttu-id="bb245-131">Zobacz toosee przykładem w potoku ciągłe wdrażanie przy użyciu usługi Konfiguracja DSC automatyzacji Azure [tooIaaS ciągłe wdrażanie maszyn wirtualnych przy użyciu usługi Azure Automation DSC i Chocolatey](automation-dsc-cd-chocolatey.md)</span><span class="sxs-lookup"><span data-stu-id="bb245-131">toosee an example of using Azure Automation DSC in a continuous deployment pipeline, see  [Continuous Deployment tooIaaS VMs Using Azure Automation DSC and Chocolatey](automation-dsc-cd-chocolatey.md)</span></span>
