---
title: "aaaUse toodeploy portalu Azure zasobów platformy Azure | Dokumentacja firmy Microsoft"
description: "Użyj portalu Azure i usługi Azure Resource Manager toodeploy zasobów."
services: azure-resource-manager,azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 2c98a4aa-8d9f-4a0a-b764-214dbe8ed009
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: 5a5217f94c8dfc0c1ebd613903ea3dcbe1197bfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-portal"></a><span data-ttu-id="963cb-103">Deploy resources with Resource Manager templates and Azure portal (Wdrażanie zasobów za pomocą szablonów usługi Resource Manager i witryny Azure Portal)</span><span class="sxs-lookup"><span data-stu-id="963cb-103">Deploy resources with Resource Manager templates and Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="963cb-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="963cb-104">PowerShell</span></span>](resource-group-template-deploy.md)
> * [<span data-ttu-id="963cb-105">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="963cb-105">Azure CLI</span></span>](resource-group-template-deploy-cli.md)
> * [<span data-ttu-id="963cb-106">Portal</span><span class="sxs-lookup"><span data-stu-id="963cb-106">Portal</span></span>](resource-group-template-deploy-portal.md)
> * [<span data-ttu-id="963cb-107">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="963cb-107">REST API</span></span>](resource-group-template-deploy-rest.md)
> 
> 

<span data-ttu-id="963cb-108">W tym temacie przedstawiono sposób toouse hello [portalu Azure](https://portal.azure.com) z [usługi Azure Resource Manager](resource-group-overview.md) toodeploy zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="963cb-108">This topic shows how toouse hello [Azure portal](https://portal.azure.com) with [Azure Resource Manager](resource-group-overview.md) toodeploy your Azure resources.</span></span> <span data-ttu-id="963cb-109">toolearn dotyczące zarządzania zasobami, zobacz [zasobów Azure zarządzania za pośrednictwem portalu](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="963cb-109">toolearn about managing your resources, see [Manage Azure resources through portal](resource-group-portal.md).</span></span>

<span data-ttu-id="963cb-110">Obecnie nie wszystkie usługi obsługuje portalu hello lub Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="963cb-110">Currently, not every service supports hello portal or Resource Manager.</span></span> <span data-ttu-id="963cb-111">W przypadku tych usług należy toouse hello [klasyczny portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="963cb-111">For those services, you need toouse hello [classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="963cb-112">Witaj stan każdej usługi, zobacz [wykresu dostępności portalu Azure](https://azure.microsoft.com/features/azure-portal/availability/).</span><span class="sxs-lookup"><span data-stu-id="963cb-112">For hello status of each service, see [Azure portal availability chart](https://azure.microsoft.com/features/azure-portal/availability/).</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="963cb-113">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="963cb-113">Create resource group</span></span>
1. <span data-ttu-id="963cb-114">Wybierz toocreate pustej grupy zasobów, **nowy** > **zarządzania** > **grupy zasobów**.</span><span class="sxs-lookup"><span data-stu-id="963cb-114">toocreate an empty resource group, select **New** > **Management** > **Resource Group**.</span></span>
   
    ![Tworzenie pustej grupy zasobów](./media/resource-group-template-deploy-portal/create-empty-group.png)
2. <span data-ttu-id="963cb-116">Nadaj nazwę i lokalizację, a w razie potrzeby wybierz subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="963cb-116">Give it a name and location, and, if necessary, select a subscription.</span></span> <span data-ttu-id="963cb-117">Należy tooprovide lokalizację dla grupy zasobów hello, ponieważ hello grupy zasobów są przechowywane metadane dotyczące hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="963cb-117">You need tooprovide a location for hello resource group because hello resource group stores metadata about hello resources.</span></span> <span data-ttu-id="963cb-118">Ze względu na zgodność można toospecify przechowywania tych metadanych.</span><span class="sxs-lookup"><span data-stu-id="963cb-118">For compliance reasons, you may want toospecify where that metadata is stored.</span></span> <span data-ttu-id="963cb-119">Ogólnie rzecz biorąc firma Microsoft zaleca, aby określić lokalizację, w której będą znajdować się większość zasobów.</span><span class="sxs-lookup"><span data-stu-id="963cb-119">In general, we recommend that you specify a location where most of your resources will reside.</span></span> <span data-ttu-id="963cb-120">Przy użyciu hello sam lokalizacji może uprościć szablonu.</span><span class="sxs-lookup"><span data-stu-id="963cb-120">Using hello same location can simplify your template.</span></span>
   
    ![zestaw wartości grupy](./media/resource-group-template-deploy-portal/set-group-properties.png)

## <a name="deploy-resources-from-marketplace"></a><span data-ttu-id="963cb-122">Wdrażanie zasobów z witryny Marketplace</span><span class="sxs-lookup"><span data-stu-id="963cb-122">Deploy resources from Marketplace</span></span>
<span data-ttu-id="963cb-123">Po utworzeniu grupy zasobów, można wdrożyć tooit zasoby z hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="963cb-123">After you create a resource group, you can deploy resources tooit from hello Marketplace.</span></span> <span data-ttu-id="963cb-124">Hello Marketplace udostępnia wstępnie zdefiniowane rozwiązań dla typowych scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="963cb-124">hello Marketplace provides pre-defined solutions for common scenarios.</span></span>

1. <span data-ttu-id="963cb-125">toostart wdrożenia, wybierz **nowy** i hello typ zasobu ma toodeploy.</span><span class="sxs-lookup"><span data-stu-id="963cb-125">toostart a deployment, select **New** and hello type of resource you would like toodeploy.</span></span> <span data-ttu-id="963cb-126">Następnie, poszukaj dla określonej wersji hello zasobu hello chcesz toodeploy.</span><span class="sxs-lookup"><span data-stu-id="963cb-126">Then, look for hello particular version of hello resource you would like toodeploy.</span></span>
   
    ![Wdrażanie zasobów](./media/resource-group-template-deploy-portal/deploy-resource.png)
2. <span data-ttu-id="963cb-128">Jeśli nie ma hello danego rozwiązania, które chcesz toodeploy, możesz wyszukać hello Marketplace go.</span><span class="sxs-lookup"><span data-stu-id="963cb-128">If you do not see hello particular solution you would like toodeploy, you can search hello Marketplace for it.</span></span>
   
    ![Wyszukiwanie w witrynie marketplace](./media/resource-group-template-deploy-portal/search-resource.png)
3. <span data-ttu-id="963cb-130">W zależności od typu wybranego zasobu hello masz kolekcję tooset odpowiednie właściwości przed przystąpieniem do wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="963cb-130">Depending on hello type of selected resource, you have a collection of relevant properties tooset before deployment.</span></span> <span data-ttu-id="963cb-131">Te opcje nie są wyświetlane w tym miejscu, zgodnie z ich różnić w zależności od typu zasobu.</span><span class="sxs-lookup"><span data-stu-id="963cb-131">Those options are not shown here, as they vary based on resource type.</span></span> <span data-ttu-id="963cb-132">Dla wszystkich typów należy wybrać grupę zasobu docelowego.</span><span class="sxs-lookup"><span data-stu-id="963cb-132">For all types, you must select a destination resource group.</span></span> <span data-ttu-id="963cb-133">następujące Hello obraz przedstawia sposób toocreate aplikacji sieci web i wdróż je utworzoną grupę zasobów toohello.</span><span class="sxs-lookup"><span data-stu-id="963cb-133">hello following image shows how toocreate a web app and deploy it toohello resource group you created.</span></span>
   
    ![Utwórz grupę zasobów](./media/resource-group-template-deploy-portal/select-existing-group.png)
   
    <span data-ttu-id="963cb-135">Alternatywnie można określić toocreate grupę zasobów, w przypadku wdrażania zasobów.</span><span class="sxs-lookup"><span data-stu-id="963cb-135">Alternatively, you can decide toocreate a resource group when deploying your resources.</span></span> <span data-ttu-id="963cb-136">Wybierz **Utwórz nowy** i nadaj nazwę grupy zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="963cb-136">Select **Create new** and give hello resource group a name.</span></span>
   
    ![Utwórz nową grupę zasobów](./media/resource-group-template-deploy-portal/select-new-group.png)
4. <span data-ttu-id="963cb-138">Rozpoczyna się wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="963cb-138">Your deployment begins.</span></span> <span data-ttu-id="963cb-139">Witaj wdrażania może potrwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="963cb-139">hello deployment could take a few minutes.</span></span> <span data-ttu-id="963cb-140">Po zakończeniu wdrażania hello zostanie wyświetlone powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="963cb-140">When hello deployment has finished, you see a notification.</span></span>
   
    ![Wyświetl powiadomienie](./media/resource-group-template-deploy-portal/view-notification.png)
5. <span data-ttu-id="963cb-142">Po wdrożeniu zasobów, można dodać więcej grupy zasobów toohello zasobów za pomocą hello **Dodaj** polecenia w bloku grupy zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="963cb-142">After deploying your resources, you can add more resources toohello resource group by using hello **Add** command on hello resource group blade.</span></span>
   
    ![dodawanie zasobu](./media/resource-group-template-deploy-portal/add-resource.png)

## <a name="deploy-resources-from-custom-template"></a><span data-ttu-id="963cb-144">Wdrażanie zasobów z szablonu niestandardowego</span><span class="sxs-lookup"><span data-stu-id="963cb-144">Deploy resources from custom template</span></span>
<span data-ttu-id="963cb-145">Tooexecute wdrożenia, ale nie używane szablony hello w hello Marketplace, można utworzyć szablon niestandardowy, który definiuje infrastrukturę Twojego rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="963cb-145">If you want tooexecute a deployment but not use any of hello templates in hello Marketplace, you can create a customized template that defines hello infrastructure for your solution.</span></span> <span data-ttu-id="963cb-146">toolearn o tworzeniu szablonów, zobacz [szablonów Authoring Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="963cb-146">toolearn about creating templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

1. <span data-ttu-id="963cb-147">Wybierz szablon niestandardowy za pośrednictwem portalu hello toodeploy **nowy**i rozpocząć wyszukiwanie **wdrażania szablonu** dopóki nie zostanie ona wybrana, korzystając z opcji hello.</span><span class="sxs-lookup"><span data-stu-id="963cb-147">toodeploy a customized template through hello portal, select **New**, and start searching for **Template Deployment** until you can select it from hello options.</span></span>
   
    ![Wdrażanie szablonu wyszukiwania](./media/resource-group-template-deploy-portal/search-template.png)
2. <span data-ttu-id="963cb-149">Wybierz **wdrażania szablonu** z hello dostępnych zasobów.</span><span class="sxs-lookup"><span data-stu-id="963cb-149">Select **Template Deployment** from hello available resources.</span></span>
   
    ![Wybierz szablon wdrażania](./media/resource-group-template-deploy-portal/select-template.png)
3. <span data-ttu-id="963cb-151">Po uruchomieniu hello szablonu wdrażania, otwórz hello pustego szablonu, dostępnej dostosowywania.</span><span class="sxs-lookup"><span data-stu-id="963cb-151">After launching hello template deployment, open hello blank template that is available for customizing.</span></span>
   
    ![Tworzenie szablonu](./media/resource-group-template-deploy-portal/show-custom-template.png)
   
    <span data-ttu-id="963cb-153">W edytorze hello Dodaj składni JSON hello definiujący hello zasoby, które chcesz toodeploy.</span><span class="sxs-lookup"><span data-stu-id="963cb-153">In hello editor, add hello JSON syntax that defines hello resources you want toodeploy.</span></span> <span data-ttu-id="963cb-154">Wybierz **zapisać** po zakończeniu.</span><span class="sxs-lookup"><span data-stu-id="963cb-154">Select **Save** when done.</span></span> <span data-ttu-id="963cb-155">Aby uzyskać wskazówki dotyczące pisania hello składni JSON, zobacz [Przewodnik po szablonie usługi Resource Manager](resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="963cb-155">For guidance on writing hello JSON syntax, see [Resource Manager template walkthrough](resource-manager-template-walkthrough.md).</span></span>
   
    ![edytowanie szablonu](./media/resource-group-template-deploy-portal/edit-template.png)
4. <span data-ttu-id="963cb-157">Umożliwia wybranie istniejącego szablonu z hello [szablonów Szybki Start Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="963cb-157">Or, you can select a pre-existing template from hello [Azure quickstart templates](https://azure.microsoft.com/documentation/templates/).</span></span> <span data-ttu-id="963cb-158">Te szablony są tworzone przez społeczność hello.</span><span class="sxs-lookup"><span data-stu-id="963cb-158">These templates are contributed by hello community.</span></span> <span data-ttu-id="963cb-159">Obejmują one wielu typowych scenariuszy, a ktoś dodany szablon, który jest podobne toowhat próbujesz toodeploy.</span><span class="sxs-lookup"><span data-stu-id="963cb-159">They cover many common scenarios, and someone may have added a template that is similar toowhat you are trying toodeploy.</span></span> <span data-ttu-id="963cb-160">Można wyszukiwać toofind szablony hello odpowiadającego danego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="963cb-160">You can search hello templates toofind something that matches your scenario.</span></span>
   
    ![Wybierz szablon szybkiego startu](./media/resource-group-template-deploy-portal/select-quickstart-template.png)
   
    <span data-ttu-id="963cb-162">W edytorze hello można wyświetlić hello wybranego szablonu.</span><span class="sxs-lookup"><span data-stu-id="963cb-162">You can view hello selected template in hello editor.</span></span>
5. <span data-ttu-id="963cb-163">Po podaniu hello wszystkie inne wartości, wybierz **Utwórz** toodeploy hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="963cb-163">After providing all hello other values, select **Create** toodeploy hello template.</span></span> 
   
    ![wdrażanie szablonu](./media/resource-group-template-deploy-portal/create-custom-deploy.png)

## <a name="deploy-resources-from-a-template-saved-tooyour-account"></a><span data-ttu-id="963cb-165">Wdrażanie zasobów z szablonu zapisane tooyour konta</span><span class="sxs-lookup"><span data-stu-id="963cb-165">Deploy resources from a template saved tooyour account</span></span>
<span data-ttu-id="963cb-166">Hello portal umożliwia toosave tooyour szablonu konto platformy Azure i wdróż go ponownie później.</span><span class="sxs-lookup"><span data-stu-id="963cb-166">hello portal enables you toosave a template tooyour Azure account, and redeploy it later.</span></span> <span data-ttu-id="963cb-167">Aby uzyskać więcej informacji na temat pracy z tych szablonów, zapisanych [Rozpoczynanie pracy z szablonami prywatnymi w portalu Azure hello](../marketplace-consumer/mytemplates-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="963cb-167">For more information about working with these saved templates, [Get started with private templates on hello Azure portal](../marketplace-consumer/mytemplates-getstarted.md).</span></span>

1. <span data-ttu-id="963cb-168">Wybierz zapisane szablony toofind **Przeglądaj** > **szablony**.</span><span class="sxs-lookup"><span data-stu-id="963cb-168">toofind your saved templates, select **Browse** > **Templates**.</span></span>
   
    ![Przeglądaj szablony](./media/resource-group-template-deploy-portal/browse-templates.png)
2. <span data-ttu-id="963cb-170">Z listy hello zapisane konto tooyour szablony wybierz hello co chcesz toowork na.</span><span class="sxs-lookup"><span data-stu-id="963cb-170">From hello list of templates saved tooyour account, select hello one you wish toowork on.</span></span>
   
    ![zapisane szablony](./media/resource-group-template-deploy-portal/saved-templates.png)
3. <span data-ttu-id="963cb-172">Wybierz **Wdróż** tooredeploy zapisany szablon.</span><span class="sxs-lookup"><span data-stu-id="963cb-172">Select **Deploy** tooredeploy this saved template.</span></span>
   
    ![zapisany szablon wdrażania](./media/resource-group-template-deploy-portal/deploy-saved-template.png)

## <a name="next-steps"></a><span data-ttu-id="963cb-174">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="963cb-174">Next steps</span></span>
* <span data-ttu-id="963cb-175">Dzienniki inspekcji tooview, zobacz [inspekcji operacji za pomocą Menedżera zasobów](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="963cb-175">tooview audit logs, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="963cb-176">błędy wdrożenia tootroubleshoot, zobacz [wyświetlić operacje wdrażania](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="963cb-176">tootroubleshoot deployment errors, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="963cb-177">tooretrieve szablonu z wdrożenia lub grupy zasobów, zobacz [szablonu eksportu usługi Azure Resource Manager z istniejących zasobów](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="963cb-177">tooretrieve a template from a deployment or resource group, see [Export Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="963cb-178">Aby uzyskać wskazówki dotyczące użycia tooeffectively Menedżera zasobów przedsiębiorstwa Zarządzaj subskrypcjami, zobacz [szkieletu Azure enterprise — ładu przetestowanego subskrypcji](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="963cb-178">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

