---
title: "Zaktualizuj Azure modułów w automatyzacji Azure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: ed8c97b642d406a05817ec6c67f31a1b4bce93b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-update-azure-powershell-modules-in-azure-automation"></a><span data-ttu-id="d6faa-103">Jak zaktualizować modułów programu Azure PowerShell w usłudze Automatyzacja Azure</span><span class="sxs-lookup"><span data-stu-id="d6faa-103">How to update Azure PowerShell modules in Azure Automation</span></span>

<span data-ttu-id="d6faa-104">Najbardziej typowe moduły programu PowerShell systemu Azure znajdują się domyślnie każdego konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="d6faa-104">The most common Azure PowerShell modules are provided by default in each Automation account.</span></span>  <span data-ttu-id="d6faa-105">Zespół Azure aktualizuje Azure modułów regularnie, więc w ramach konta automatyzacji udostępniamy sposób aktualizowania modułów w ramach konta, gdy nowe wersje są dostępne w portalu.</span><span class="sxs-lookup"><span data-stu-id="d6faa-105">The Azure team updates the Azure modules regularly, so in the Automation account we provide a way for you to update the modules in the account when new versions are available from the portal.</span></span>  

<span data-ttu-id="d6faa-106">Ponieważ moduły są regularnie aktualizowane przez grupę, zmiany mogą być uwzględnione polecenia cmdlet, które może niekorzystnie wpłynąć na elementach runbook, w zależności od rodzaju zmiany, takie jak zmiana nazwy parametru lub całkowicie wycofano polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d6faa-106">Because modules are updated regularly by the product group, changes can occur with the  included cmdlets, which may negatively impact your runbooks depending on the type of change, such as renaming a parameter or deprecating a cmdlet entirely.</span></span> <span data-ttu-id="d6faa-107">Aby uniknąć wpływu na elementy runbook i ich automatyzacji procesów, zdecydowanie zaleca się testowanie i zweryfikować przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="d6faa-107">To avoid impacting your runbooks and the processes they automate, it is strongly recommended that you test and validate before proceeding.</span></span>  <span data-ttu-id="d6faa-108">Jeśli nie masz dedykowane konto automatyzacji przeznaczone do tego celu, należy rozważyć utworzenie jednego, dzięki czemu można przetestować wiele różnych scenariuszy i permutacji podczas tworzenia elementów runbook, oprócz do iteracji zmian, takich jak aktualizowanie Moduły programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d6faa-108">If you do not have a dedicated Automation account intended for this purpose, consider creating one so that you can test many different scenarios and permutations during the development of your runbooks, in addition to iterative changes such as updating the PowerShell modules.</span></span>  <span data-ttu-id="d6faa-109">Po zweryfikowaniu wyniki i wszelkie wymagane zmiany zostały zastosowane, kontynuować koordynowanie migracji wszystkie elementy runbook, który wymagany modyfikacji i wykonać aktualizację, zgodnie z poniższym opisem w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="d6faa-109">After the results are validated and you have applied any changes required, proceed with coordinating the migration of any runbooks that required modification and perform the update as described below in production.</span></span>     

## <a name="updating-azure-modules"></a><span data-ttu-id="d6faa-110">Aktualizowanie Azure modułów</span><span class="sxs-lookup"><span data-stu-id="d6faa-110">Updating Azure Modules</span></span>

1. <span data-ttu-id="d6faa-111">W modułach bloku Twoje konto usługi Automatyzacja jest opcję o nazwie **modułów Azure aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="d6faa-111">In the Modules blade of your Automation account there is an option called **Update Azure Modules**.</span></span>  <span data-ttu-id="d6faa-112">Jest zawsze włączone.</span><span class="sxs-lookup"><span data-stu-id="d6faa-112">It is always enabled.</span></span><br><br> <span data-ttu-id="d6faa-113">![Aktualizowanie opcji Azure modułów w bloku modułów](media/automation-update-azure-modules/automation-update-azure-modules-option.png)</span><span class="sxs-lookup"><span data-stu-id="d6faa-113">![Update Azure Modules option in Modules blade](media/automation-update-azure-modules/automation-update-azure-modules-option.png)</span></span>

2. <span data-ttu-id="d6faa-114">Kliknij przycisk **modułów Azure aktualizacji** i użytkownik zostanie wyświetlone powiadomienie z potwierdzeniem z pytaniem, czy chcesz kontynuować.</span><span class="sxs-lookup"><span data-stu-id="d6faa-114">Click **Update Azure Modules** and you will be presented with a confirmation notification that asks you if you want to continue.</span></span><br><br> <span data-ttu-id="d6faa-115">![Zaktualizuj powiadomień Azure modułów](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)</span><span class="sxs-lookup"><span data-stu-id="d6faa-115">![Update Azure Modules notification](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)</span></span>

3. <span data-ttu-id="d6faa-116">Kliknij przycisk **tak** i rozpocznie się proces aktualizacji modułu.</span><span class="sxs-lookup"><span data-stu-id="d6faa-116">Click **Yes** and the module update process will begin.</span></span>  <span data-ttu-id="d6faa-117">Proces aktualizacji trwa około 15-20 minut, można zaktualizować następujących modułów:</span><span class="sxs-lookup"><span data-stu-id="d6faa-117">The update process takes about 15-20 minutes to update the following modules:</span></span>

  * <span data-ttu-id="d6faa-118">Azure</span><span class="sxs-lookup"><span data-stu-id="d6faa-118">Azure</span></span>
  * <span data-ttu-id="d6faa-119">Azure.Storage</span><span class="sxs-lookup"><span data-stu-id="d6faa-119">Azure.Storage</span></span>
  * <span data-ttu-id="d6faa-120">AzureRm.Automation</span><span class="sxs-lookup"><span data-stu-id="d6faa-120">AzureRm.Automation</span></span>
  * <span data-ttu-id="d6faa-121">AzureRm.Compute</span><span class="sxs-lookup"><span data-stu-id="d6faa-121">AzureRm.Compute</span></span>
  * <span data-ttu-id="d6faa-122">AzureRm.Profile</span><span class="sxs-lookup"><span data-stu-id="d6faa-122">AzureRm.Profile</span></span>
  * <span data-ttu-id="d6faa-123">AzureRm.Resources</span><span class="sxs-lookup"><span data-stu-id="d6faa-123">AzureRm.Resources</span></span>
  * <span data-ttu-id="d6faa-124">AzureRm.Sql</span><span class="sxs-lookup"><span data-stu-id="d6faa-124">AzureRm.Sql</span></span>
  * <span data-ttu-id="d6faa-125">AzureRm.Storage</span><span class="sxs-lookup"><span data-stu-id="d6faa-125">AzureRm.Storage</span></span>

    <span data-ttu-id="d6faa-126">Jeśli moduły są już aktualne, proces zostanie zakończony w ciągu kilku sekund.</span><span class="sxs-lookup"><span data-stu-id="d6faa-126">If the modules are already up to date, then the process will complete in a few seconds.</span></span>  <span data-ttu-id="d6faa-127">Po zakończeniu procesu aktualizacji otrzymasz powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="d6faa-127">When the update process completes you will be notified.</span></span><br><br> ![Zaktualizuj stan aktualizacji modułów Azure](media/automation-update-azure-modules/automation-update-azure-modules-updatestatus.png)

> [!NOTE]
> <span data-ttu-id="d6faa-129">Automatyzacja Azure użyje najnowszej modułów na Twoim koncie automatyzacji po uruchomieniu nowego zaplanowanego zadania.</span><span class="sxs-lookup"><span data-stu-id="d6faa-129">Azure Automation will use the latest modules in your Automation account when a new scheduled job is run.</span></span>    

<span data-ttu-id="d6faa-130">Jeśli używasz poleceń cmdlet z tych modułów programu Azure PowerShell w elementach runbook do zarządzania zasobami Azure, następnie należy przeprowadzić proces aktualizacji co miesiąc lub tak, aby mieć pewność, że masz najnowszą modułów.</span><span class="sxs-lookup"><span data-stu-id="d6faa-130">If you use cmdlets from these Azure PowerShell modules in your runbooks to manage Azure resources, then you will want to perform this update process every month or so to assure that you have the latest modules.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6faa-131">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d6faa-131">Next steps</span></span>

* <span data-ttu-id="d6faa-132">Aby dowiedzieć się więcej o moduły integracji oraz sposobu tworzenia niestandardowych modułów do dalszej integracji z innymi systemami, usług lub rozwiązań automatyzacji, zobacz [moduły integracji](automation-integration-modules.md).</span><span class="sxs-lookup"><span data-stu-id="d6faa-132">To learn more about Integration Modules and how to create custom modules to further integrate Automation with other systems, services, or solutions, see [Integration Modules](automation-integration-modules.md).</span></span>

* <span data-ttu-id="d6faa-133">Należy rozważyć użycie integracji kontroli źródła [GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md) lub [Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md) centralne zarządzanie i sterowanie wersjach portfela automatyzacji elementu runbook i konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d6faa-133">Consider source control integration using [GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md) or [Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md) to centrally manage and control releases of your Automation runbook and configuration portfolio.</span></span>  