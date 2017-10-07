---
title: "aaaUpdate Azure modułów w automatyzacji Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak można teraz zaktualizować typowymi modułami programu Azure PowerShell domyślne automatyzacji Azure."
services: automation
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/13/2017
ms.author: magoedte
ms.openlocfilehash: afa404a643349f044e55be2280e435b575049dec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupdate-azure-powershell-modules-in-azure-automation"></a><span data-ttu-id="d70fd-103">Jak tooupdate programu Azure PowerShell modułów w automatyzacji Azure</span><span class="sxs-lookup"><span data-stu-id="d70fd-103">How tooupdate Azure PowerShell modules in Azure Automation</span></span>

<span data-ttu-id="d70fd-104">najbardziej typowe modułów programu Azure PowerShell Hello znajdują się domyślnie każdego konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="d70fd-104">hello most common Azure PowerShell modules are provided by default in each Automation account.</span></span>  <span data-ttu-id="d70fd-105">Hello Azure zespołu aktualizacje hello Azure modułów regularnie, więc w hello konta automatyzacji zapewniamy, sposób dla Ciebie tooupdate hello modułów na koncie hello gdy są dostępne w portalu hello nowe wersje.</span><span class="sxs-lookup"><span data-stu-id="d70fd-105">hello Azure team updates hello Azure modules regularly, so in hello Automation account we provide a way for you tooupdate hello modules in hello account when new versions are available from hello portal.</span></span>  

<span data-ttu-id="d70fd-106">Ponieważ moduły są regularnie aktualizowane przez grupę produktu hello, zmiany mogą wystąpić z poleceniami cmdlet hello uwzględnione, które może niekorzystnie wpłynąć na elementach runbook, w zależności od typu hello zmiany, takie jak zmiana nazwy parametru lub całkowicie wycofano polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d70fd-106">Because modules are updated regularly by hello product group, changes can occur with hello  included cmdlets, which may negatively impact your runbooks depending on hello type of change, such as renaming a parameter or deprecating a cmdlet entirely.</span></span> <span data-ttu-id="d70fd-107">tooavoid wpływu na Twoje elementy runbook i hello procesów one zautomatyzować, zdecydowanie zaleca się testowanie i zweryfikować przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="d70fd-107">tooavoid impacting your runbooks and hello processes they automate, it is strongly recommended that you test and validate before proceeding.</span></span>  <span data-ttu-id="d70fd-108">Jeśli nie masz dedykowane konto automatyzacji przeznaczone do tego celu, należy rozważyć utworzenie tak, aby można było testować wiele różnych scenariuszy i permutacji podczas tworzenia hello elementów runbook, w dodanie tooiterative zmian, takich jak aktualizowanie hello Moduły programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d70fd-108">If you do not have a dedicated Automation account intended for this purpose, consider creating one so that you can test many different scenarios and permutations during hello development of your runbooks, in addition tooiterative changes such as updating hello PowerShell modules.</span></span>  <span data-ttu-id="d70fd-109">Po hello wyniki są weryfikowane i wszelkie wymagane zmiany zostały zastosowane, kontynuować koordynowanie migracji hello elementów runbook, wszelkie wymagane zmiany i zaktualizować hello zgodnie z poniższym opisem w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="d70fd-109">After hello results are validated and you have applied any changes required, proceed with coordinating hello migration of any runbooks that required modification and perform hello update as described below in production.</span></span>     

## <a name="updating-azure-modules"></a><span data-ttu-id="d70fd-110">Aktualizowanie Azure modułów</span><span class="sxs-lookup"><span data-stu-id="d70fd-110">Updating Azure Modules</span></span>

1. <span data-ttu-id="d70fd-111">W modułach hello bloku Twoje konto usługi Automatyzacja jest opcję o nazwie **modułów Azure aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="d70fd-111">In hello Modules blade of your Automation account there is an option called **Update Azure Modules**.</span></span>  <span data-ttu-id="d70fd-112">Jest zawsze włączone.</span><span class="sxs-lookup"><span data-stu-id="d70fd-112">It is always enabled.</span></span><br><br> <span data-ttu-id="d70fd-113">![Aktualizowanie opcji Azure modułów w bloku modułów](media/automation-update-azure-modules/automation-update-azure-modules-option.png)</span><span class="sxs-lookup"><span data-stu-id="d70fd-113">![Update Azure Modules option in Modules blade](media/automation-update-azure-modules/automation-update-azure-modules-option.png)</span></span>

2. <span data-ttu-id="d70fd-114">Kliknij przycisk **modułów Azure aktualizacji** i wyświetlone zostanie okno z pytaniem, czy ma toocontinue powiadomienie z potwierdzeniem.</span><span class="sxs-lookup"><span data-stu-id="d70fd-114">Click **Update Azure Modules** and you will be presented with a confirmation notification that asks you if you want toocontinue.</span></span><br><br> <span data-ttu-id="d70fd-115">![Zaktualizuj powiadomień Azure modułów](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)</span><span class="sxs-lookup"><span data-stu-id="d70fd-115">![Update Azure Modules notification](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)</span></span>

3. <span data-ttu-id="d70fd-116">Kliknij przycisk **tak** i rozpocznie się proces aktualizacji hello modułu.</span><span class="sxs-lookup"><span data-stu-id="d70fd-116">Click **Yes** and hello module update process will begin.</span></span>  <span data-ttu-id="d70fd-117">proces aktualizacji Hello trwa około 15-20 minut tooupdate hello następujących modułów:</span><span class="sxs-lookup"><span data-stu-id="d70fd-117">hello update process takes about 15-20 minutes tooupdate hello following modules:</span></span>

  * <span data-ttu-id="d70fd-118">Azure</span><span class="sxs-lookup"><span data-stu-id="d70fd-118">Azure</span></span>
  * <span data-ttu-id="d70fd-119">Azure.Storage</span><span class="sxs-lookup"><span data-stu-id="d70fd-119">Azure.Storage</span></span>
  * <span data-ttu-id="d70fd-120">AzureRm.Automation</span><span class="sxs-lookup"><span data-stu-id="d70fd-120">AzureRm.Automation</span></span>
  * <span data-ttu-id="d70fd-121">AzureRm.Compute</span><span class="sxs-lookup"><span data-stu-id="d70fd-121">AzureRm.Compute</span></span>
  * <span data-ttu-id="d70fd-122">AzureRm.Profile</span><span class="sxs-lookup"><span data-stu-id="d70fd-122">AzureRm.Profile</span></span>
  * <span data-ttu-id="d70fd-123">AzureRm.Resources</span><span class="sxs-lookup"><span data-stu-id="d70fd-123">AzureRm.Resources</span></span>
  * <span data-ttu-id="d70fd-124">AzureRm.Sql</span><span class="sxs-lookup"><span data-stu-id="d70fd-124">AzureRm.Sql</span></span>
  * <span data-ttu-id="d70fd-125">AzureRm.Storage</span><span class="sxs-lookup"><span data-stu-id="d70fd-125">AzureRm.Storage</span></span>

    <span data-ttu-id="d70fd-126">Jeśli moduły hello są już włączone toodate, hello proces zostanie zakończony w ciągu kilku sekund.</span><span class="sxs-lookup"><span data-stu-id="d70fd-126">If hello modules are already up toodate, then hello process will complete in a few seconds.</span></span>  <span data-ttu-id="d70fd-127">Po zakończeniu procesu aktualizacji hello otrzymasz powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="d70fd-127">When hello update process completes you will be notified.</span></span><br><br> ![Zaktualizuj stan aktualizacji modułów Azure](media/automation-update-azure-modules/automation-update-azure-modules-updatestatus.png)

> [!NOTE]
> <span data-ttu-id="d70fd-129">Automatyzacja Azure użyje modułów najnowszego hello na Twoim koncie automatyzacji po uruchomieniu nowego zaplanowanego zadania.</span><span class="sxs-lookup"><span data-stu-id="d70fd-129">Azure Automation will use hello latest modules in your Automation account when a new scheduled job is run.</span></span>    

<span data-ttu-id="d70fd-130">Jeśli używasz poleceń cmdlet z tych modułów programu Azure PowerShell w Twojej toomanage elementów runbook Azure zasobów, możesz dokonać tooperform proces aktualizacji co miesiąc lub tak tooassure, czy masz hello najnowsze modułów.</span><span class="sxs-lookup"><span data-stu-id="d70fd-130">If you use cmdlets from these Azure PowerShell modules in your runbooks toomanage Azure resources, then you will want tooperform this update process every month or so tooassure that you have hello latest modules.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d70fd-131">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d70fd-131">Next steps</span></span>

* <span data-ttu-id="d70fd-132">toolearn więcej informacji na temat moduły integracji i jak toocreate toofurther niestandardowe moduły integracji automatyzacji z innych systemów, usługi lub rozwiązania, zobacz [moduły integracji](automation-integration-modules.md).</span><span class="sxs-lookup"><span data-stu-id="d70fd-132">toolearn more about Integration Modules and how toocreate custom modules toofurther integrate Automation with other systems, services, or solutions, see [Integration Modules](automation-integration-modules.md).</span></span>

* <span data-ttu-id="d70fd-133">Należy rozważyć użycie integracji kontroli źródła [GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md) lub [Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md) toocentrally zarządzanie i sterowanie wersjach portfela automatyzacji elementu runbook i konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d70fd-133">Consider source control integration using [GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md) or [Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md) toocentrally manage and control releases of your Automation runbook and configuration portfolio.</span></span>  
