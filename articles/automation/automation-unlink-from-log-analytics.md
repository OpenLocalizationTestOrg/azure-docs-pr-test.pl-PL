---
title: "Konto usługi Automatyzacja Azure z analizy dzienników aaaUnlink | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera omówienie sposobu toounlink Twojego automatyzacji Azure konta z obszarem roboczym pakietu OMS."
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
ms.openlocfilehash: 3ec0745673f6a872538d33023a7a1d2bb1d18ec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toounlink-your-automation-account-from-a-log-analytics-workspace"></a><span data-ttu-id="fa4a9-103">Jak toounlink Twojego automatyzacji konta z obszaru roboczego analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="fa4a9-103">How toounlink your Automation account from a Log Analytics workspace</span></span>

<span data-ttu-id="fa4a9-104">Automatyzacja Azure umożliwia integrację z analizy dzienników toonot tylko obsługę aktywnego monitorowania zadań elementu runbook dla wszystkich kont automatyzacji, ale jest również wymagany podczas importowania hello następujące rozwiązania, które są zależne od analizy dzienników:</span><span class="sxs-lookup"><span data-stu-id="fa4a9-104">Azure Automation integrates with Log Analytics toonot only support proactive monitoring of your runbook jobs across all of your Automation accounts, but is also required when you import hello following solutions that are dependent on Log Analytics:</span></span>

* [<span data-ttu-id="fa4a9-105">Zarządzanie aktualizacjami</span><span class="sxs-lookup"><span data-stu-id="fa4a9-105">Update Management</span></span>](../operations-management-suite/oms-solution-update-management.md)
* [<span data-ttu-id="fa4a9-106">Śledzenie zmian</span><span class="sxs-lookup"><span data-stu-id="fa4a9-106">Change Tracking</span></span>](../log-analytics/log-analytics-change-tracking.md)
* [<span data-ttu-id="fa4a9-107">Uruchamiania/zatrzymywania maszyn wirtualnych w godzinach</span><span class="sxs-lookup"><span data-stu-id="fa4a9-107">Start/Stop VMs during off-hours</span></span>](automation-solution-vm-management.md)
 
<span data-ttu-id="fa4a9-108">Jeśli zdecydujesz się, że nie chcesz już toointegrate Twojego konta automatyzacji z analizy dzienników można odłączyć konta bezpośrednio z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="fa4a9-108">If you decide you no longer wish toointegrate your Automation account with Log Analytics, you can unlink your account directly from hello Azure portal.</span></span>  <span data-ttu-id="fa4a9-109">Zanim będziesz kontynuować, należy najpierw rozwiązań hello tooremove wspomniano wcześniej, w przeciwnym razie ten proces nie będzie mógł kontynuować.</span><span class="sxs-lookup"><span data-stu-id="fa4a9-109">Before you proceed, you will first need tooremove hello solutions mentioned earlier, otherwise this process will be prevented from proceeding.</span></span>  <span data-ttu-id="fa4a9-110">Przejrzyj temat powitania dla danego rozwiązania hello zaimportowano toounderstand hello kroki wymagane tooremove go.</span><span class="sxs-lookup"><span data-stu-id="fa4a9-110">Review hello topic for hello particular solution you have imported toounderstand hello steps required tooremove it.</span></span>  

<span data-ttu-id="fa4a9-111">Po usunięciu tych rozwiązań można wykonywać następujące czynności toounlink hello Twoje konto usługi Automatyzacja.</span><span class="sxs-lookup"><span data-stu-id="fa4a9-111">After you remove these solutions you can perform hello following steps toounlink your Automation account.</span></span>

## <a name="unlink-workspace"></a><span data-ttu-id="fa4a9-112">Rozłącz obszaru roboczego</span><span class="sxs-lookup"><span data-stu-id="fa4a9-112">Unlink workspace</span></span>

1. <span data-ttu-id="fa4a9-113">Hello portalu Azure, otwórz Twoje konto usługi Automatyzacja i w bloku konta usługi Automatyzacja hello, w bloku konta hello, wybierz **odłączyć obszaru roboczego**.</span><span class="sxs-lookup"><span data-stu-id="fa4a9-113">From hello Azure portal, open your Automation account, and in hello Automation account blade, in hello account blade, select **Unlink workspace**.</span></span><br><br> <span data-ttu-id="fa4a9-114">![Odłącz obszar roboczy](media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)</span><span class="sxs-lookup"><span data-stu-id="fa4a9-114">![Unlink workspace option](media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)</span></span><br><br>  
2. <span data-ttu-id="fa4a9-115">W bloku obszaru roboczego Rozłącz hello, kliknij **odłączyć worksapce**.</span><span class="sxs-lookup"><span data-stu-id="fa4a9-115">On hello Unlink workspace blade, click **Unlink worksapce**.</span></span><br><br> <span data-ttu-id="fa4a9-116">![Rozłącz bloku obszaru roboczego](media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png).</span><span class="sxs-lookup"><span data-stu-id="fa4a9-116">![Unlink workspace blade](media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png).</span></span><br><br>  <span data-ttu-id="fa4a9-117">Zostanie wyświetlony monit zweryfikowaniu, że chcesz tooproceed.</span><span class="sxs-lookup"><span data-stu-id="fa4a9-117">You will receive a prompt verifying you wish tooproceed.</span></span><br><br>
3. <span data-ttu-id="fa4a9-118">Podczas automatyzacji Azure próbuje konta hello toounlink obszaru roboczego analizy dzienników, możesz śledzić postępy hello w obszarze **powiadomienia** hello menu.</span><span class="sxs-lookup"><span data-stu-id="fa4a9-118">While Azure Automation attempts toounlink hello account your Log Analytics workspace, you can track hello progress under **Notifications** from hello menu.</span></span>

<span data-ttu-id="fa4a9-119">Użycie rozwiązania zarządzania aktualizacjami hello Opcjonalnie możesz hello tooremove następujące elementy, które nie są już potrzebne po usunięciu hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="fa4a9-119">If you used hello Update Management solution, optionally you may want tooremove hello following items that are no longer needed after you remove hello solution.</span></span>

* <span data-ttu-id="fa4a9-120">Harmonogramy aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="fa4a9-120">Update schedules.</span></span>  <span data-ttu-id="fa4a9-121">Będzie mieć nazwy są zgodne z wdrożenia aktualizacji hello utworzone)</span><span class="sxs-lookup"><span data-stu-id="fa4a9-121">Each will have names that match hello update deployments you created)</span></span>

* <span data-ttu-id="fa4a9-122">Hybrydowe utworzone dla rozwiązania hello grupy procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="fa4a9-122">Hybrid worker groups created for hello solution.</span></span>  <span data-ttu-id="fa4a9-123">Każda będzie miała nazwę podobnie zbyt machine1.contoso.com_9ceb8108 - 26 c 9-4051-b6b3-227600d715c8).</span><span class="sxs-lookup"><span data-stu-id="fa4a9-123">Each will be named similarly too machine1.contoso.com_9ceb8108-26c9-4051-b6b3-227600d715c8).</span></span>

<span data-ttu-id="fa4a9-124">Jeśli maszyn wirtualnych uruchamiania i zatrzymywania hello jest używany podczas rozwiązania poza godzinami szczytu, opcjonalnie można hello tooremove następujące elementy, które nie są już potrzebne po usunięciu hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="fa4a9-124">If you used hello Start/Stop VMs during off-hours solution, optionally you may want tooremove hello following items that are no longer needed after you remove hello solution.</span></span>

* <span data-ttu-id="fa4a9-125">Uruchamianie i zatrzymywanie harmonogramy runbook maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="fa4a9-125">Start and stop VM runbook schedules</span></span> 
* <span data-ttu-id="fa4a9-126">Uruchamianie i zatrzymywanie elementów runbook maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="fa4a9-126">Start and stop VM runbooks</span></span>
* <span data-ttu-id="fa4a9-127">Zmienne</span><span class="sxs-lookup"><span data-stu-id="fa4a9-127">Variables</span></span>   

## <a name="next-steps"></a><span data-ttu-id="fa4a9-128">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fa4a9-128">Next steps</span></span>

<span data-ttu-id="fa4a9-129">tooreconfigure Twojego toointegrate konta automatyzacji o OMS Log Analytics, zobacz [przekazuj strumienie zadania i stan zadania z automatyzacji tooLog Analytics (OMS)](automation-manage-send-joblogs-log-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="fa4a9-129">tooreconfigure your Automation account toointegrate with OMS Log Analytics, see [Forward job status and job streams from Automation tooLog Analytics (OMS)](automation-manage-send-joblogs-log-analytics.md).</span></span> 
