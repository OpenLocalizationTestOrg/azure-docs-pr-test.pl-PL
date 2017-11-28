---
title: "aaaCreate laboratorium w usłudze Azure DevTest Labs | Dokumentacja firmy Microsoft"
description: "Tworzenie laboratorium w usłudze Azure DevTest Labs na potrzeby maszyn wirtualnych"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 8b6d3e70-6528-42a4-a2ef-449575d0f928
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/30/2017
ms.author: tarcher
ms.openlocfilehash: 2ec5498f10e0cc06a196a71e319e340937abb1a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="478dc-103">Tworzenie laboratorium w usłudze Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="478dc-103">Create a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="478dc-104">Laboratorium w usłudze Azure DevTest Labs jest hello infrastruktury, który obejmuje grupy zasobów, takich jak maszyn wirtualnych (VM), które umożliwiają lepsze zarządzanie tych zasobów, określając ograniczenia i limity przydziału.</span><span class="sxs-lookup"><span data-stu-id="478dc-104">A lab in Azure DevTest Labs is hello infrastructure that encompasses a group of resources, such as Virtual Machines (VMs), that lets you better manage those resources by specifying limits and quotas.</span></span> <span data-ttu-id="478dc-105">Ten artykuł przeprowadzi Cię przez proces tworzenia laboratorium przy użyciu portalu Azure hello hello.</span><span class="sxs-lookup"><span data-stu-id="478dc-105">This article walks you through hello process of creating a lab using hello Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="478dc-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="478dc-106">Prerequisites</span></span>
<span data-ttu-id="478dc-107">toocreate laboratorium, potrzebne są:</span><span class="sxs-lookup"><span data-stu-id="478dc-107">toocreate a lab, you need:</span></span>

* <span data-ttu-id="478dc-108">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="478dc-108">An Azure subscription.</span></span> <span data-ttu-id="478dc-109">toolearn o opcjami zakupu platformy Azure, zobacz [jak toobuy Azure](https://azure.microsoft.com/pricing/purchase-options/) lub [bezpłatna miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="478dc-109">toolearn about Azure purchase options, see [How toobuy Azure](https://azure.microsoft.com/pricing/purchase-options/) or [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="478dc-110">Musi być właścicielem hello hello subskrypcji toocreate hello laboratorium.</span><span class="sxs-lookup"><span data-stu-id="478dc-110">You must be hello owner of hello subscription toocreate hello lab.</span></span>

## <a name="steps-toocreate-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="478dc-111">Kroki toocreate laboratorium w usłudze Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="478dc-111">Steps toocreate a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="478dc-112">Witaj następujące kroki pokazują, jak toouse hello Azure toocreate portalu laboratorium w usłudze Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="478dc-112">hello following steps illustrate how toouse hello Azure portal toocreate a lab in Azure DevTest Labs.</span></span> 

1. <span data-ttu-id="478dc-113">Zaloguj się toohello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="478dc-113">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="478dc-114">Wybierz z menu głównego powitania po lewej stronie powitania, **więcej usług** (u dołu hello hello listy).</span><span class="sxs-lookup"><span data-stu-id="478dc-114">From hello main menu on hello left side, select **More Services** (at hello bottom of hello list).</span></span>

    ![Opcja menu Więcej usług](./media/devtest-lab-create-lab/more-services-menu-option.png)

1. <span data-ttu-id="478dc-116">Z listy dostępnych usług, hello **DevTest Labs**.</span><span class="sxs-lookup"><span data-stu-id="478dc-116">From hello list of available services, **DevTest Labs**.</span></span>
1. <span data-ttu-id="478dc-117">Na powitania **DevTest Labs** bloku, wybierz opcję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="478dc-117">On hello **DevTest Labs** blade, select **Add**.</span></span>
   
    ![Dodawanie laboratorium](./media/devtest-lab-create-lab/add-lab-button.png)

1. <span data-ttu-id="478dc-119">Na powitania **Utwórz laboratorium DevTest Lab** bloku:</span><span class="sxs-lookup"><span data-stu-id="478dc-119">On hello **Create a DevTest Lab** blade:</span></span>
   
    1. <span data-ttu-id="478dc-120">Wprowadź **Nazwa laboratorium** dla nowego laboratorium hello.</span><span class="sxs-lookup"><span data-stu-id="478dc-120">Enter a **Lab Name** for hello new lab.</span></span>
    2. <span data-ttu-id="478dc-121">Wybierz hello **subskrypcji** tooassociate z hello laboratorium.</span><span class="sxs-lookup"><span data-stu-id="478dc-121">Select hello **Subscription** tooassociate with hello lab.</span></span>
    3. <span data-ttu-id="478dc-122">Wybierz **lokalizacji** w których toostore hello laboratorium.</span><span class="sxs-lookup"><span data-stu-id="478dc-122">Select a **Location** in which toostore hello lab.</span></span>
    4. <span data-ttu-id="478dc-123">Wybierz **automatyczne zamykanie** toospecify tooenable - i definiować parametry hello — Witaj, automatyczne zamykanie hello laboratorium wszystkich maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="478dc-123">Select **Auto-shutdown** toospecify if you want tooenable - and define hello parameters for - hello automatic shutting down of all hello lab's VMs.</span></span> <span data-ttu-id="478dc-124">Witaj automatyczne zamykanie funkcja jest głównie funkcji oszczędności zgodnie z którymi można określić, kiedy zechcesz hello wirtualna tooautomatically można zamknąć.</span><span class="sxs-lookup"><span data-stu-id="478dc-124">hello auto-shutdown feature is mainly a cost-saving feature whereby you can specify when you want hello VM tooautomatically be shut down.</span></span> <span data-ttu-id="478dc-125">Ustawienia automatycznego zamykania można zmienić po utworzeniu laboratorium hello hello wykonaj czynności opisane w artykule hello [zarządzanie wszystkimi zasadami dla laboratorium w usłudze Azure DevTest Labs](./devtest-lab-set-lab-policy.md#set-auto-shutdown).</span><span class="sxs-lookup"><span data-stu-id="478dc-125">You can change auto-shutdown settings after creating hello lab by following hello steps outlined in hello article, [Manage all policies for a lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md#set-auto-shutdown).</span></span>
    5. <span data-ttu-id="478dc-126">Wybierz **tooDashboard numeru Pin** Jeśli skrót tooappear laboratorium hello na powitania pulpitu nawigacyjnego portalu.</span><span class="sxs-lookup"><span data-stu-id="478dc-126">Select **Pin tooDashboard** if you want a shortcut of hello lab tooappear on hello portal dashboard.</span></span>
    6. <span data-ttu-id="478dc-127">Wybierz **opcje automatyzacji** tooget szablonów usługi Azure Resource Manager dla konfiguracji usługi Automatyzacja.</span><span class="sxs-lookup"><span data-stu-id="478dc-127">Select **Automation options** tooget Azure Resource Manager templates for configuration automation.</span></span> 
    7. <span data-ttu-id="478dc-128">Wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="478dc-128">Select **Create**.</span></span> <span data-ttu-id="478dc-129">Po wybraniu **Utwórz**, hello **DevTest Labs** wyświetla bloku.</span><span class="sxs-lookup"><span data-stu-id="478dc-129">After selecting **Create**, hello **DevTest Labs** blade displays.</span></span> <span data-ttu-id="478dc-130">Możesz monitorować stan hello procesu tworzenia laboratorium hello obserwując hello **powiadomienia** obszaru.</span><span class="sxs-lookup"><span data-stu-id="478dc-130">You can monitor hello status of hello lab creation process by watching hello **Notifications** area.</span></span> <span data-ttu-id="478dc-131">Po ukończeniu odświeżania hello strony toosee hello nowo utworzony w hello lista labs laboratorium.</span><span class="sxs-lookup"><span data-stu-id="478dc-131">Once completed, refresh hello page toosee hello newly created lab in hello list of labs.</span></span>  
    
    ![Blok tworzenia laboratorium](./media/devtest-lab-create-lab/create-devtestlab-blade.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="478dc-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="478dc-133">Next steps</span></span>
<span data-ttu-id="478dc-134">Po utworzeniu laboratorium, poniżej przedstawiono niektóre dalej tooconsider kroki:</span><span class="sxs-lookup"><span data-stu-id="478dc-134">Once you've created your lab, here are some next steps tooconsider:</span></span>

* <span data-ttu-id="478dc-135">[Bezpieczny dostęp tooa laboratorium](devtest-lab-add-devtest-user.md).</span><span class="sxs-lookup"><span data-stu-id="478dc-135">[Secure access tooa lab](devtest-lab-add-devtest-user.md).</span></span>
* <span data-ttu-id="478dc-136">[Set lab policies](devtest-lab-set-lab-policy.md) (Ustawianie zasad laboratorium).</span><span class="sxs-lookup"><span data-stu-id="478dc-136">[Set lab policies](devtest-lab-set-lab-policy.md).</span></span>
* <span data-ttu-id="478dc-137">[Create a lab template](devtest-lab-create-template.md) (Tworzenie szablonu laboratorium).</span><span class="sxs-lookup"><span data-stu-id="478dc-137">[Create a lab template](devtest-lab-create-template.md).</span></span>
* <span data-ttu-id="478dc-138">[Create custom artifacts for your VMs](devtest-lab-artifact-author.md) (Tworzenie niestandardowych artefaktów dla maszyn wirtualnych).</span><span class="sxs-lookup"><span data-stu-id="478dc-138">[Create custom artifacts for your VMs](devtest-lab-artifact-author.md).</span></span>
* <span data-ttu-id="478dc-139">[Dodawanie maszyny Wirtualnej z laboratorium tooa artefakty](https://azure.microsoft.com/resources/videos/how-to-create-vms-with-artifacts-in-a-devtest-lab/).</span><span class="sxs-lookup"><span data-stu-id="478dc-139">[Add a VM with artifacts tooa lab](https://azure.microsoft.com/resources/videos/how-to-create-vms-with-artifacts-in-a-devtest-lab/).</span></span>

