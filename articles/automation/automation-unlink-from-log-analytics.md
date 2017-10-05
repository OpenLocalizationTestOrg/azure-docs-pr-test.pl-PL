---
title: "Odłączanie konta usługi Automatyzacja Azure Log Analytics | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera omówienie sposobu odłączania Twoje konto usługi Automatyzacja Azure z obszarem roboczym pakietu OMS."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: how-to-article
ms.date: 02/07/2017
ms.author: magoedte
ms.openlocfilehash: 56b09c2cfc14813b5efcb364c580787fec1bf639
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-unlink-your-automation-account-from-a-log-analytics-workspace"></a><span data-ttu-id="d060a-103">Sposobu odłączania Twoje konto usługi Automatyzacja z obszaru roboczego analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="d060a-103">How to unlink your Automation account from a Log Analytics workspace</span></span>

<span data-ttu-id="d060a-104">Automatyzacja Azure umożliwia integrację z analizy dzienników umożliwia nie tylko aktywnego monitorowania zadań elementu runbook dla wszystkich kont automatyzacji, ale jest również wymagany podczas importowania następujące rozwiązania, które są zależne od analizy dzienników:</span><span class="sxs-lookup"><span data-stu-id="d060a-104">Azure Automation integrates with Log Analytics to not only support proactive monitoring of your runbook jobs across all of your Automation accounts, but is also required when you import the following solutions that are dependent on Log Analytics:</span></span>

* [<span data-ttu-id="d060a-105">Zarządzanie aktualizacjami</span><span class="sxs-lookup"><span data-stu-id="d060a-105">Update Management</span></span>](../operations-management-suite/oms-solution-update-management.md)
* [<span data-ttu-id="d060a-106">Śledzenie zmian</span><span class="sxs-lookup"><span data-stu-id="d060a-106">Change Tracking</span></span>](../log-analytics/log-analytics-change-tracking.md)
* [<span data-ttu-id="d060a-107">Uruchamiania/zatrzymywania maszyn wirtualnych w godzinach</span><span class="sxs-lookup"><span data-stu-id="d060a-107">Start/Stop VMs during off-hours</span></span>](automation-solution-vm-management.md)
 
<span data-ttu-id="d060a-108">Jeśli zdecydujesz się, że chcesz zintegrować Twoje konto usługi Automatyzacja z analizy dzienników nie będzie można odłączyć konta bezpośrednio z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d060a-108">If you decide you no longer wish to integrate your Automation account with Log Analytics, you can unlink your account directly from the Azure portal.</span></span>  <span data-ttu-id="d060a-109">Zanim będziesz kontynuować, musisz najpierw usunąć rozwiązania wspomniano wcześniej, w przeciwnym razie ten proces nie będzie mógł kontynuować.</span><span class="sxs-lookup"><span data-stu-id="d060a-109">Before you proceed, you will first need to remove the solutions mentioned earlier, otherwise this process will be prevented from proceeding.</span></span>  <span data-ttu-id="d060a-110">Przejrzyj temat dla określonego rozwiązania, które zostały zaimportowane, aby zrozumieć kroki wymagane w celu usunięcia go.</span><span class="sxs-lookup"><span data-stu-id="d060a-110">Review the topic for the particular solution you have imported to understand the steps required to remove it.</span></span>  

<span data-ttu-id="d060a-111">Po usunięciu tych rozwiązań, które można wykonać następujące kroki, aby odłączyć Twoje konto usługi Automatyzacja.</span><span class="sxs-lookup"><span data-stu-id="d060a-111">After you remove these solutions you can perform the following steps to unlink your Automation account.</span></span>

## <a name="unlink-workspace"></a><span data-ttu-id="d060a-112">Rozłącz obszaru roboczego</span><span class="sxs-lookup"><span data-stu-id="d060a-112">Unlink workspace</span></span>

1. <span data-ttu-id="d060a-113">W portalu Azure, otwórz Twoje konto usługi Automatyzacja, a w bloku konta usługi Automatyzacja w bloku konta wybierz **odłączyć obszaru roboczego**.</span><span class="sxs-lookup"><span data-stu-id="d060a-113">From the Azure portal, open your Automation account, and in the Automation account blade, in the account blade, select **Unlink workspace**.</span></span><br><br> <span data-ttu-id="d060a-114">![Odłącz obszar roboczy](media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)</span><span class="sxs-lookup"><span data-stu-id="d060a-114">![Unlink workspace option](media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)</span></span><br><br>  
2. <span data-ttu-id="d060a-115">W bloku Rozłącz obszaru roboczego kliknij **odłączyć worksapce**.</span><span class="sxs-lookup"><span data-stu-id="d060a-115">On the Unlink workspace blade, click **Unlink worksapce**.</span></span><br><br> <span data-ttu-id="d060a-116">![Rozłącz bloku obszaru roboczego](media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png).</span><span class="sxs-lookup"><span data-stu-id="d060a-116">![Unlink workspace blade](media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png).</span></span><br><br>  <span data-ttu-id="d060a-117">Zostanie wyświetlony monit sprawdzający, czy chcesz kontynuować.</span><span class="sxs-lookup"><span data-stu-id="d060a-117">You will receive a prompt verifying you wish to proceed.</span></span><br><br>
3. <span data-ttu-id="d060a-118">Gdy usługi Automatyzacja Azure usiłuje odłączyć konto obszaru roboczego analizy dzienników, możesz śledzić postępy w obszarze **powiadomienia** z menu.</span><span class="sxs-lookup"><span data-stu-id="d060a-118">While Azure Automation attempts to unlink the account your Log Analytics workspace, you can track the progress under **Notifications** from the menu.</span></span>

<span data-ttu-id="d060a-119">Użycie rozwiązania zarządzania aktualizacjami, opcjonalnie możesz usunąć następujące elementy, które nie są już potrzebne po usunięciu rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="d060a-119">If you used the Update Management solution, optionally you may want to remove the following items that are no longer needed after you remove the solution.</span></span>

* <span data-ttu-id="d060a-120">Harmonogramy aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="d060a-120">Update schedules.</span></span>  <span data-ttu-id="d060a-121">Będzie mieć nazwy są zgodne z wdrożenia aktualizacji, który utworzono)</span><span class="sxs-lookup"><span data-stu-id="d060a-121">Each will have names that match the update deployments you created)</span></span>

* <span data-ttu-id="d060a-122">Hybrydowe utworzone dla rozwiązania grupy procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="d060a-122">Hybrid worker groups created for the solution.</span></span>  <span data-ttu-id="d060a-123">Każda będzie miała nazwę podobnie do machine1.contoso.com_9ceb8108 - 26 c 9-4051-b6b3-227600d715c8).</span><span class="sxs-lookup"><span data-stu-id="d060a-123">Each will be named similarly to  machine1.contoso.com_9ceb8108-26c9-4051-b6b3-227600d715c8).</span></span>

<span data-ttu-id="d060a-124">Jeśli używasz uruchamiania/zatrzymywania maszyn wirtualnych podczas rozwiązania poza godzinami szczytu, opcjonalnie może chcesz usunąć następujące elementy, które nie są już potrzebne po usunięciu rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="d060a-124">If you used the Start/Stop VMs during off-hours solution, optionally you may want to remove the following items that are no longer needed after you remove the solution.</span></span>

* <span data-ttu-id="d060a-125">Uruchamianie i zatrzymywanie harmonogramy runbook maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="d060a-125">Start and stop VM runbook schedules</span></span> 
* <span data-ttu-id="d060a-126">Uruchamianie i zatrzymywanie elementów runbook maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="d060a-126">Start and stop VM runbooks</span></span>
* <span data-ttu-id="d060a-127">Zmienne</span><span class="sxs-lookup"><span data-stu-id="d060a-127">Variables</span></span>   

## <a name="next-steps"></a><span data-ttu-id="d060a-128">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d060a-128">Next steps</span></span>

<span data-ttu-id="d060a-129">Aby zmienić konfigurację konta automatyzacji do integracji z analizy dzienników OMS, zobacz [przekazuj strumienie zadania i stan zadania z automatyzacji analizy dzienników (OMS)](automation-manage-send-joblogs-log-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="d060a-129">To reconfigure your Automation account to integrate with OMS Log Analytics, see [Forward job status and job streams from Automation to Log Analytics (OMS)](automation-manage-send-joblogs-log-analytics.md).</span></span> 