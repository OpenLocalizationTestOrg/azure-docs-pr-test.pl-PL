---
title: "aaaUse toomanage portalu Azure zasobów platformy Azure | Dokumentacja firmy Microsoft"
description: "Użyj portalu Azure i usługi Azure Resource Manager toomanage zasobów. Pokazuje sposób toowork z zasobami toomonitor pulpitów nawigacyjnych."
services: azure-resource-manager,azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 0725bbf2-5913-4c07-af6e-24e11d957fbc
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: 0c89a197a31c5b6dd03ba457cb4d1fdf9f6d00f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-resources-through-portal"></a><span data-ttu-id="122de-104">Zarządzania zasobami Azure za pośrednictwem portalu</span><span class="sxs-lookup"><span data-stu-id="122de-104">Manage Azure resources through portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="122de-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="122de-105">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="122de-106">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="122de-106">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="122de-107">Portal</span><span class="sxs-lookup"><span data-stu-id="122de-107">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="122de-108">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="122de-108">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="122de-109">W tym temacie przedstawiono sposób toouse hello [portalu Azure](https://portal.azure.com) z [usługi Azure Resource Manager](resource-group-overview.md) toomanage zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="122de-109">This topic shows how toouse hello [Azure portal](https://portal.azure.com) with [Azure Resource Manager](resource-group-overview.md) toomanage your Azure resources.</span></span> <span data-ttu-id="122de-110">Zobacz toolearn dotyczących wdrażania zasobów za pośrednictwem portalu hello [wdrożenie zasobów z szablonami usługi Resource Manager i portalu Azure](resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="122de-110">toolearn about deploying resources through hello portal, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>

<span data-ttu-id="122de-111">Obecnie nie wszystkie usługi obsługuje portalu hello lub Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="122de-111">Currently, not every service supports hello portal or Resource Manager.</span></span> <span data-ttu-id="122de-112">W przypadku tych usług należy toouse hello [klasyczny portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="122de-112">For those services, you need toouse hello [classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="122de-113">Witaj stan każdej usługi, zobacz [wykresu dostępności portalu Azure](https://azure.microsoft.com/features/azure-portal/availability/).</span><span class="sxs-lookup"><span data-stu-id="122de-113">For hello status of each service, see [Azure portal availability chart](https://azure.microsoft.com/features/azure-portal/availability/).</span></span>

## <a name="manage-resource-groups"></a><span data-ttu-id="122de-114">Zarządzanie grupami zasobów</span><span class="sxs-lookup"><span data-stu-id="122de-114">Manage resource groups</span></span>

<span data-ttu-id="122de-115">Grupa zasobów jest kontenerem, który zawiera powiązane zasoby Azure rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="122de-115">A resource group is a container that holds related resources for an Azure solution.</span></span> <span data-ttu-id="122de-116">Grupa zasobów Hello mogą obejmować wszystkie zasoby hello hello rozwiązania lub tylko tych zasobów, które mają toomanage jako grupa.</span><span class="sxs-lookup"><span data-stu-id="122de-116">hello resource group can include all hello resources for hello solution, or only those resources that you want toomanage as a group.</span></span> <span data-ttu-id="122de-117">Możesz zdecydować, jak zasoby tooallocate tooresource grupy oparte na to, co sprawia, że hello najbardziej odpowiednie dla Twojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="122de-117">You decide how you want tooallocate resources tooresource groups based on what makes hello most sense for your organization.</span></span> <span data-ttu-id="122de-118">Ogólnie rzecz biorąc, Dodaj zasoby, które współużytkują hello tego samego toohello cyklu życia zasobów w tej samej grupy tak łatwe wdrażanie, aktualizować i usuwać je jako grupę.</span><span class="sxs-lookup"><span data-stu-id="122de-118">Generally, add resources that share hello same lifecycle toohello same resource group so you can easily deploy, update, and delete them as a group.</span></span> 

<span data-ttu-id="122de-119">Grupa zasobów Hello są przechowywane metadane dotyczące hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="122de-119">hello resource group stores metadata about hello resources.</span></span> <span data-ttu-id="122de-120">W związku z tym po określeniu lokalizacji dla grupy zasobów hello określisz przechowywania tych metadanych.</span><span class="sxs-lookup"><span data-stu-id="122de-120">Therefore, when you specify a location for hello resource group, you are specifying where that metadata is stored.</span></span> <span data-ttu-id="122de-121">Ze względu na zgodność może być konieczne tooensure danych przechowywanych w określonym regionie.</span><span class="sxs-lookup"><span data-stu-id="122de-121">For compliance reasons, you may need tooensure that your data is stored in a particular region.</span></span>

1. <span data-ttu-id="122de-122">Wybierz wszystkie grupy zasobów hello w ramach subskrypcji, toosee **grup zasobów**.</span><span class="sxs-lookup"><span data-stu-id="122de-122">toosee all hello resource groups in your subscription, select **Resource groups**.</span></span>
   
    ![Przeglądaj grup zasobów](./media/resource-group-portal/browse-groups.png)
2. <span data-ttu-id="122de-124">Wybierz toocreate pustej grupy zasobów, **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="122de-124">toocreate an empty resource group, select **Add**.</span></span>
   
    ![Dodaj grupę zasobów](./media/resource-group-portal/add-resource-group.png)
3. <span data-ttu-id="122de-126">Podaj nazwę i lokalizację hello nową grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="122de-126">Provide a name and location for hello new resource group.</span></span> <span data-ttu-id="122de-127">Wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="122de-127">Select **Create**.</span></span>
   
    ![Utwórz grupę zasobów](./media/resource-group-portal/create-empty-group.png)
4. <span data-ttu-id="122de-129">Może być konieczne tooselect **Odśwież** grupy zasobów toosee hello niedawno utworzona.</span><span class="sxs-lookup"><span data-stu-id="122de-129">You may need tooselect **Refresh** toosee hello recently created resource group.</span></span>
   
    ![Odśwież grupę zasobów](./media/resource-group-portal/refresh-resource-groups.png)
5. <span data-ttu-id="122de-131">Wybierz toocustomize hello informacje wyświetlane dla grupy zasobów, **kolumn**.</span><span class="sxs-lookup"><span data-stu-id="122de-131">toocustomize hello information displayed for your resource groups, select **Columns**.</span></span>
   
    ![Dostosowywanie kolumn](./media/resource-group-portal/select-columns.png)
6. <span data-ttu-id="122de-133">Wybierz hello tooadd kolumny, a następnie wybierz **aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="122de-133">Select hello columns tooadd, and then select **Update**.</span></span>
   
    ![Dodawanie kolumn](./media/resource-group-portal/add-columns.png)
7. <span data-ttu-id="122de-135">toolearn dotyczących wdrażania zasobów tooyour nową grupę zasobów, zobacz [wdrożenie zasobów z szablonami usługi Resource Manager i portalu Azure](resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="122de-135">toolearn about deploying resources tooyour new resource group, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>
8. <span data-ttu-id="122de-136">Szybki dostęp tooa grupy zasobów można przypiąć hello bloku tooyour w pulpicie nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="122de-136">For quick access tooa resource group, you can pin hello blade tooyour dashboard.</span></span>
   
    ![Grupa zasobów numeru PIN](./media/resource-group-portal/pin-group.png)
9. <span data-ttu-id="122de-138">pulpit nawigacyjny Hello Wyświetla hello grupy zasobów i jego zasoby.</span><span class="sxs-lookup"><span data-stu-id="122de-138">hello dashboard displays hello resource group and its resources.</span></span> <span data-ttu-id="122de-139">Można wybrać grupy zasobów hello lub dowolną z jego element toohello toonavigate zasobów.</span><span class="sxs-lookup"><span data-stu-id="122de-139">You can select either hello resource groups or any of its resources toonavigate toohello item.</span></span>
   
    ![Grupa zasobów numeru PIN](./media/resource-group-portal/show-resource-group-dashboard.png)

## <a name="tag-resources"></a><span data-ttu-id="122de-141">Tag zasobów</span><span class="sxs-lookup"><span data-stu-id="122de-141">Tag resources</span></span>
<span data-ttu-id="122de-142">Można stosować grup tooresource tagów i toologically zasobów organizowania zasobów.</span><span class="sxs-lookup"><span data-stu-id="122de-142">You can apply tags tooresource groups and resources toologically organize your assets.</span></span> <span data-ttu-id="122de-143">Informacje o pracy z tagami, zobacz [używanie tagów tooorganize zasobów platformy Azure](resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="122de-143">For information about working with tags, see [Using tags tooorganize your Azure resources](resource-group-using-tags.md).</span></span>

[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]

## <a name="monitor-resources"></a><span data-ttu-id="122de-144">Monitorowanie zasobów</span><span class="sxs-lookup"><span data-stu-id="122de-144">Monitor resources</span></span>
<span data-ttu-id="122de-145">Po wybraniu zasobu bloku zasobów hello przedstawia domyślne wykresów i tabel do monitorowania tego typu zasobu.</span><span class="sxs-lookup"><span data-stu-id="122de-145">When you select a resource, hello resource blade presents default graphs and tables for monitoring that resource type.</span></span>

1. <span data-ttu-id="122de-146">Wybierz hello zasobów i zwróć uwagę, **monitorowanie** sekcji.</span><span class="sxs-lookup"><span data-stu-id="122de-146">Select a resource and notice hello **Monitoring** section.</span></span> <span data-ttu-id="122de-147">Zawiera wykresy toohello odpowiedniego typu zasobu.</span><span class="sxs-lookup"><span data-stu-id="122de-147">It includes graphs that are relevant toohello resource type.</span></span> <span data-ttu-id="122de-148">Witaj poniższej ilustracji przedstawiono domyślne hello monitorowania danych dla konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="122de-148">hello following image shows hello default monitoring data for a storage account.</span></span>
   
    ![Pokaż monitorowania](./media/resource-group-portal/show-monitoring.png)
2. <span data-ttu-id="122de-150">Części pulpitu nawigacyjnego tooyour bloku hello można przypiąć, wybierając hello wielokropek (...) powyżej hello sekcji.</span><span class="sxs-lookup"><span data-stu-id="122de-150">You can pin a section of hello blade tooyour dashboard by selecting hello ellipsis (...) above hello section.</span></span> <span data-ttu-id="122de-151">Można również dostosować hello rozmiar hello części bloku hello lub całkowicie usunąć.</span><span class="sxs-lookup"><span data-stu-id="122de-151">You can also customize hello size hello section in hello blade or remove it completely.</span></span> <span data-ttu-id="122de-152">Witaj Poniższa ilustracja przedstawia przykładowy sposób dostosować toopin, lub usuń hello procesora CPU i pamięci sekcji.</span><span class="sxs-lookup"><span data-stu-id="122de-152">hello following image shows how toopin, customize, or remove hello CPU and Memory section.</span></span>
   
    ![sekcja numeru PIN](./media/resource-group-portal/pin-cpu-section.png)
3. <span data-ttu-id="122de-154">Po przypięciu pulpitu nawigacyjnego toohello sekcji hello, zobaczysz hello podsumowania na powitania pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="122de-154">After pinning hello section toohello dashboard, you will see hello summary on hello dashboard.</span></span> <span data-ttu-id="122de-155">I wybierając ją od razu przejście toomore szczegóły hello danych.</span><span class="sxs-lookup"><span data-stu-id="122de-155">And, selecting it immediately takes you toomore details about hello data.</span></span>
   
    ![widok pulpitu nawigacyjnego](./media/resource-group-portal/view-startboard.png)
4. <span data-ttu-id="122de-157">toocompletely dostosować hello danych monitorowania za pośrednictwem portalu hello, przejdź tooyour domyślnego pulpitu nawigacyjnego i wybierz **nowego pulpitu nawigacyjnego**.</span><span class="sxs-lookup"><span data-stu-id="122de-157">toocompletely customize hello data you monitor through hello portal, navigate tooyour default dashboard, and select **New dashboard**.</span></span>
   
    ![pulpit nawigacyjny](./media/resource-group-portal/dashboard.png)
5. <span data-ttu-id="122de-159">Nadaj nazwę nowego pulpitu nawigacyjnego i przeciągnij Kafelki na pulpicie nawigacyjnym hello.</span><span class="sxs-lookup"><span data-stu-id="122de-159">Give your new dashboard a name and drag tiles onto hello dashboard.</span></span> <span data-ttu-id="122de-160">Kafelki Hello są filtrowane według różnych opcji.</span><span class="sxs-lookup"><span data-stu-id="122de-160">hello tiles are filtered by different options.</span></span>
   
    ![pulpit nawigacyjny](./media/resource-group-portal/create-dashboard.png)
   
     <span data-ttu-id="122de-162">toolearn o pracy z pulpitów nawigacyjnych, zobacz [tworzenie i udostępnianie pulpitów nawigacyjnych w portalu Azure hello](../azure-portal/azure-portal-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="122de-162">toolearn about working with dashboards, see [Creating and sharing dashboards in hello Azure portal](../azure-portal/azure-portal-dashboards.md).</span></span>

## <a name="manage-resources"></a><span data-ttu-id="122de-163">Zarządzanie zasobami</span><span class="sxs-lookup"><span data-stu-id="122de-163">Manage resources</span></span>
<span data-ttu-id="122de-164">W bloku hello zasobu widać hello opcje zarządzania hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="122de-164">In hello blade for a resource, you see hello options for managing hello resource.</span></span> <span data-ttu-id="122de-165">Hello portal przedstawia opcje zarządzania dla tego typu zasobu.</span><span class="sxs-lookup"><span data-stu-id="122de-165">hello portal presents management options for that particular resource type.</span></span> <span data-ttu-id="122de-166">Widzisz polecenia zarządzania hello hello górze bloku zasobów hello i po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="122de-166">You see hello management commands across hello top of hello resource blade and on hello left side.</span></span>

![Zarządzanie zasobami](./media/resource-group-portal/manage-resources.png)

<span data-ttu-id="122de-168">Z tych opcji można wykonywać operacje, takie jak uruchamianie i zatrzymywanie maszyny wirtualnej lub ponownej konfiguracji właściwości hello hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="122de-168">From these options, you can perform operations such as starting and stopping a virtual machine, or reconfiguring hello properties of hello virtual machine.</span></span>

## <a name="move-resources"></a><span data-ttu-id="122de-169">Przenoszenie zasobów</span><span class="sxs-lookup"><span data-stu-id="122de-169">Move resources</span></span>
<span data-ttu-id="122de-170">Aby uzyskać grupy zasobów tooanother zasobów toomove lub inną subskrypcję, zobacz [przenieść grupy zasobów toonew zasobów lub subskrypcji](resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="122de-170">If you need toomove resources tooanother resource group or another subscription, see [Move resources toonew resource group or subscription](resource-group-move-resources.md).</span></span>

## <a name="lock-resources"></a><span data-ttu-id="122de-171">Blokowanie zasobów</span><span class="sxs-lookup"><span data-stu-id="122de-171">Lock resources</span></span>
<span data-ttu-id="122de-172">Można zablokować subskrypcji, grupy zasobów lub tooprevent zasobów innym użytkownikom w organizacji przypadkowo usuwanie i modyfikowanie kluczowych zasobów.</span><span class="sxs-lookup"><span data-stu-id="122de-172">You can lock a subscription, resource group, or resource tooprevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="122de-173">Aby uzyskać więcej informacji, zobacz [Lock resources with Azure Resource Manager](resource-group-lock-resources.md) (Blokowanie zasobów w usłudze Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="122de-173">For more information, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="view-your-subscription-and-costs"></a><span data-ttu-id="122de-174">Wyświetlanie Twoich subskrypcji i kosztów</span><span class="sxs-lookup"><span data-stu-id="122de-174">View your subscription and costs</span></span>
<span data-ttu-id="122de-175">Można wyświetlić informacji o subskrypcji i hello zestawienia kosztów dla wszystkich zasobów.</span><span class="sxs-lookup"><span data-stu-id="122de-175">You can view information about your subscription and hello rolled-up costs for all your resources.</span></span> <span data-ttu-id="122de-176">Wybierz **subskrypcje** i subskrypcji hello ma toosee.</span><span class="sxs-lookup"><span data-stu-id="122de-176">Select **Subscriptions** and hello subscription you want toosee.</span></span> <span data-ttu-id="122de-177">Może mieć tylko jeden tooselect subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="122de-177">You might only have one subscription tooselect.</span></span>

![subskrypcja](./media/resource-group-portal/select-subscription.png)

<span data-ttu-id="122de-179">W bloku subskrypcji hello zobacz temat ocena wydajności.</span><span class="sxs-lookup"><span data-stu-id="122de-179">Within hello subscription blade, you see a burn rate.</span></span>

![współczynnik spalania](./media/resource-group-portal/burn-rate.png)

<span data-ttu-id="122de-181">I podziału kosztów według typów zasobów.</span><span class="sxs-lookup"><span data-stu-id="122de-181">And, a breakdown of costs by resource type.</span></span>

![koszt zasobów](./media/resource-group-portal/cost-by-resource.png)

## <a name="export-template"></a><span data-ttu-id="122de-183">Eksportowanie szablonu</span><span class="sxs-lookup"><span data-stu-id="122de-183">Export template</span></span>
<span data-ttu-id="122de-184">Po skonfigurowaniu grupy zasobów, można szablonu usługi Resource Manager hello tooview hello grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="122de-184">After setting up your resource group, you may want tooview hello Resource Manager template for hello resource group.</span></span> <span data-ttu-id="122de-185">Eksportowanie szablonu hello oferuje dwie korzyści:</span><span class="sxs-lookup"><span data-stu-id="122de-185">Exporting hello template offers two benefits:</span></span>

1. <span data-ttu-id="122de-186">Można łatwo automatyzować przyszłych wdrożeń hello rozwiązania, ponieważ szablon hello zawiera wszystkie hello całej infrastruktury.</span><span class="sxs-lookup"><span data-stu-id="122de-186">You can easily automate future deployments of hello solution because hello template contains all hello complete infrastructure.</span></span>
2. <span data-ttu-id="122de-187">Należy zaznajomić o składni szablonu analizując hello JavaScript Object Notation (JSON) reprezentujący rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="122de-187">You can become familiar with template syntax by looking at hello JavaScript Object Notation (JSON) that represents your solution.</span></span>

<span data-ttu-id="122de-188">Aby uzyskać instrukcje, zobacz [szablonu eksportu usługi Azure Resource Manager z istniejących zasobów](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="122de-188">For step-by-step guidance, see [Export Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>

## <a name="delete-resource-group-or-resources"></a><span data-ttu-id="122de-189">Usuń grupę zasobów lub zasobów</span><span class="sxs-lookup"><span data-stu-id="122de-189">Delete resource group or resources</span></span>
<span data-ttu-id="122de-190">Usunięcie grupy zasobów powoduje usunięcie wszystkich zasobów hello w nim zawarte.</span><span class="sxs-lookup"><span data-stu-id="122de-190">Deleting a resource group deletes all hello resources contained within it.</span></span> <span data-ttu-id="122de-191">Można również usunąć pojedynczych zasobów w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="122de-191">You can also delete individual resources within a resource group.</span></span> <span data-ttu-id="122de-192">Ma tooexercise ostrożność podczas usuwania grupy zasobów, ponieważ innych grup zasobów, które są połączone tooit może być zasobów.</span><span class="sxs-lookup"><span data-stu-id="122de-192">You want tooexercise caution when you delete a resource group because there might be resources in other resource groups that are linked tooit.</span></span> <span data-ttu-id="122de-193">Menedżer zasobów nie powoduje usunięcia połączonych zasobów, ale ich nie może działać poprawnie bez hello oczekiwano zasobów.</span><span class="sxs-lookup"><span data-stu-id="122de-193">Resource Manager does not delete linked resources, but they may not operate correctly without hello expected resources.</span></span>

![Usuwanie grupy](./media/resource-group-portal/delete-group.png)

## <a name="next-steps"></a><span data-ttu-id="122de-195">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="122de-195">Next steps</span></span>
* <span data-ttu-id="122de-196">Zobacz dzienniki aktywności tooview, [inspekcji operacji za pomocą Menedżera zasobów](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="122de-196">tooview activity logs, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="122de-197">tooview szczegóły dotyczące wdrożenia, zobacz [wyświetlić operacje wdrażania](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="122de-197">tooview details about a deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="122de-198">Zobacz zasoby toodeploy za pośrednictwem portalu hello [wdrożenie zasobów z szablonami usługi Resource Manager i portalu Azure](resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="122de-198">toodeploy resources through hello portal, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>
* <span data-ttu-id="122de-199">toomanage tooresources dostępu, zobacz [Użyj roli przypisania toomanage dostępu tooyour subskrypcji platformy Azure zasobów](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="122de-199">toomanage access tooresources, see [Use role assignments toomanage access tooyour Azure subscription resources](../active-directory/role-based-access-control-configure.md).</span></span>
* <span data-ttu-id="122de-200">Aby uzyskać wskazówki dotyczące użycia tooeffectively Menedżera zasobów przedsiębiorstwa Zarządzaj subskrypcjami, zobacz [szkieletu Azure enterprise — ładu przetestowanego subskrypcji](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="122de-200">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

