---
title: "aaaDeploy zestawu skalowania maszyn wirtualnych za pomocą programu Visual Studio | Dokumentacja firmy Microsoft"
description: "Wdrażanie zestawów skali maszyny wirtualnej za pomocą szablonu usługi Resource Manager i Visual Studio"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ed0786b8-34b2-49a8-85b5-2a628128ead6
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: guybo
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c89a9f2478ccc3d22989aea604a4273bcc46df82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-virtual-machine-scale-set-with-visual-studio"></a><span data-ttu-id="d1507-103">Jak toocreate, zestawu skalowania maszyn wirtualnych, z programem Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d1507-103">How toocreate a Virtual Machine Scale Set with Visual Studio</span></span>
<span data-ttu-id="d1507-104">W tym artykule opisano, jak toodeploy Azure zestawu skalowania maszyn wirtualnych za pomocą programu Visual Studio wdrożenie grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="d1507-104">This article shows you how toodeploy an Azure Virtual Machine Scale Set using a Visual Studio Resource Group Deployment.</span></span>

<span data-ttu-id="d1507-105">[Zestawy skalowania maszyny wirtualnej Azure](https://azure.microsoft.com/blog/azure-vm-scale-sets-public-preview/) jest toodeploy rozwiązań usługi obliczenia Azure zasobów i zarządzanie kolekcją podobnych maszyn wirtualnych z automatycznego skalowania i równoważenie obciążenia.</span><span class="sxs-lookup"><span data-stu-id="d1507-105">[Azure Virtual Machine Scale Sets](https://azure.microsoft.com/blog/azure-vm-scale-sets-public-preview/) is an Azure Compute resource toodeploy and manage a collection of similar virtual machines with auto-scale and load balancing.</span></span> <span data-ttu-id="d1507-106">Można udostępnić i wdrożyć zestawy skalowania maszyny wirtualnej przy użyciu [szablony Menedżera zasobów Azure](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="d1507-106">You can provision and deploy Virtual Machine Scale Sets using [Azure Resource Manager Templates](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="d1507-107">Szablony usługi Azure Resource Manager można wdrożyć przy użyciu interfejsu wiersza polecenia Azure, programu PowerShell, REST, a także bezpośrednio z programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d1507-107">Azure Resource Manager Templates can be deployed using Azure CLI, PowerShell, REST and also directly from Visual Studio.</span></span> <span data-ttu-id="d1507-108">Program Visual Studio oferuje zestaw przykład szablonów, które można wdrożyć w ramach projektu wdrożenia grupy zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d1507-108">Visual Studio provides a set of example templates, which can be deployed as part of an Azure Resource Group Deployment project.</span></span>

<span data-ttu-id="d1507-109">Wdrożenia grupy zasobów platformy Azure są toogroup sposób i opublikować zestawu powiązanych zasobów systemu Azure w ramach operacji pojedynczego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="d1507-109">Azure Resource Group deployments are a way toogroup and publish a set of related Azure resources in a single deployment operation.</span></span> <span data-ttu-id="d1507-110">Więcej informacji o nich w tym miejscu: [tworzenie i wdrażanie grup zasobów platformy Azure za pomocą programu Visual Studio](../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="d1507-110">You can learn more about them here: [Creating and deploying Azure resource groups through Visual Studio](../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span></span>

## <a name="pre-requisites"></a><span data-ttu-id="d1507-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d1507-111">Pre-requisites</span></span>
<span data-ttu-id="d1507-112">tooget rozpoczęto wdrażanie zestawy skalowania maszyny wirtualnej w programie Visual Studio, potrzebne są następujące hello:</span><span class="sxs-lookup"><span data-stu-id="d1507-112">tooget started deploying Virtual Machine Scale Sets in Visual Studio, you need hello following:</span></span>

* <span data-ttu-id="d1507-113">Visual Studio 2013 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="d1507-113">Visual Studio 2013 or later</span></span>
* <span data-ttu-id="d1507-114">Zestaw Azure SDK 2.8 2.7 i 2.9</span><span class="sxs-lookup"><span data-stu-id="d1507-114">Azure SDK 2.7, 2.8 or 2.9</span></span>

>[!NOTE]
><span data-ttu-id="d1507-115">W poniższych instrukcjach przyjęto w przypadku korzystania z programu Visual Studio z [Azure SDK 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).</span><span class="sxs-lookup"><span data-stu-id="d1507-115">These instructions assume you are using Visual Studio with [Azure SDK 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).</span></span>

## <a name="creating-a-project"></a><span data-ttu-id="d1507-116">Tworzenie projektu</span><span class="sxs-lookup"><span data-stu-id="d1507-116">Creating a Project</span></span>
1. <span data-ttu-id="d1507-117">Utwórz nowy projekt w programie Visual Studio, wybierając **pliku | Nowy | Projekt**.</span><span class="sxs-lookup"><span data-stu-id="d1507-117">Create a new project in Visual Studio by choosing **File | New | Project**.</span></span>
   
    ![Nowy plik][file_new]

2. <span data-ttu-id="d1507-119">W obszarze **Visual C# | Chmura**, wybierz **usługi Azure Resource Manager** toocreate projektu wdrażania szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d1507-119">Under **Visual C# | Cloud**, choose **Azure Resource Manager** toocreate a project for deploying an Azure Resource Manager Template.</span></span>
   
    ![Tworzenie projektu][create_project]

3. <span data-ttu-id="d1507-121">Z listy hello szablony wybierz hello Linux lub szablon ustawić skali maszyny wirtualnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="d1507-121">From hello list of Templates, select either hello Linux or Windows Virtual Machine Scale Set Template.</span></span>
   
   ![Wybierz szablon][select_Template]

4. <span data-ttu-id="d1507-123">Po utworzeniu projektu Zobacz skryptów wdrażania środowiska PowerShell szablonu usługi Azure Resource Manager i pliku parametrów dla hello zestawu skalowania maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="d1507-123">Once your project is created you see PowerShell deployment scripts, an Azure Resource Manager Template, and a parameter file for hello Virtual Machine Scale Set.</span></span>
   
    ![Eksplorator rozwiązań][solution_explorer]

## <a name="customize-your-project"></a><span data-ttu-id="d1507-125">Dostosowywanie projektu</span><span class="sxs-lookup"><span data-stu-id="d1507-125">Customize your project</span></span>
<span data-ttu-id="d1507-126">Teraz możesz edytować hello toocustomize szablonu reguły równoważenia go na potrzeby aplikacji, takich jak dodawanie właściwości rozszerzenia maszyny Wirtualnej lub edytowanie obciążenia.</span><span class="sxs-lookup"><span data-stu-id="d1507-126">Now you can edit hello Template toocustomize it for your application's needs, such as adding VM extension properties or editing load balancing rules.</span></span> <span data-ttu-id="d1507-127">Domyślnie hello szablony zestawu skali maszyny wirtualnej są skonfigurowane toodeploy hello AzureDiagnostics rozszerzenia, co pozwala na łatwe tooadd reguł skalowania automatycznego.</span><span class="sxs-lookup"><span data-stu-id="d1507-127">By default hello Virtual Machine Scale Set Templates are configured toodeploy hello AzureDiagnostics extension, which makes it easy tooadd autoscale rules.</span></span> <span data-ttu-id="d1507-128">Ponadto wdraża z publicznym adresem IP skonfigurowano reguły NAT ruchu przychodzącego modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="d1507-128">It also deploys a load balancer with a public IP address, configured with inbound NAT rules.</span></span> 

<span data-ttu-id="d1507-129">Moduł równoważenia obciążenia Hello umożliwia nawiązanie połączenia toohello wystąpień maszyn wirtualnych z protokołu SSH (Linux) lub protokołu RDP (system Windows).</span><span class="sxs-lookup"><span data-stu-id="d1507-129">hello load balancer lets you connect toohello VM instances with SSH (Linux) or RDP (Windows).</span></span> <span data-ttu-id="d1507-130">zakres portów frontonu Hello rozpoczyna się od 50000.</span><span class="sxs-lookup"><span data-stu-id="d1507-130">hello front-end port range starts at 50000.</span></span> <span data-ttu-id="d1507-131">Dla systemu linux oznacza to, że jeśli użytkownik SSH tooport 50000, są routingiem tooport 22 z hello pierwsza maszyna wirtualna w hello zestawu skalowania maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d1507-131">For linux this means that if you SSH tooport 50000, you are routed tooport 22 of hello first VM in hello Scale Set.</span></span> <span data-ttu-id="d1507-132">Łączenie tooport 50001 jest kierowany tooport 22 z hello drugie maszyny Wirtualnej i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="d1507-132">Connecting tooport 50001 is routed tooport 22 of hello second VM and so on.</span></span>

 <span data-ttu-id="d1507-133">Tooedit dobrze szablonów z programem Visual Studio jest toouse hello konspekt pliku JSON tooorganize hello parametrów, zmienne i zasobów.</span><span class="sxs-lookup"><span data-stu-id="d1507-133">A good way tooedit your Templates with Visual Studio is toouse hello JSON Outline tooorganize hello parameters, variables, and resources.</span></span> <span data-ttu-id="d1507-134">Po zrozumieniu hello schematu programu Visual Studio może wskazywać błędy w szablonie przed przystąpieniem do wdrażania.</span><span class="sxs-lookup"><span data-stu-id="d1507-134">With an understanding of hello schema Visual Studio can point out errors in your Template before you deploy it.</span></span>

![Eksplorator JSON][json_explorer]

## <a name="deploy-hello-project"></a><span data-ttu-id="d1507-136">Wdrażanie projektu hello</span><span class="sxs-lookup"><span data-stu-id="d1507-136">Deploy hello project</span></span>
1. <span data-ttu-id="d1507-137">Wdrażanie zasobów hello szablon Menedżera zasobów Azure toocreate hello zestawu skalowania maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="d1507-137">Deploy hello Azure Resource Manager Template toocreate hello Virtual Machine Scale Set resource.</span></span> <span data-ttu-id="d1507-138">Kliknij prawym przyciskiem myszy węzeł projektu hello i wybierz polecenie **Wdróż | Nowe wdrożenie**.</span><span class="sxs-lookup"><span data-stu-id="d1507-138">Right-click on hello project node and choose **Deploy | New Deployment**.</span></span>
   
    ![Wdrażanie szablonu][5deploy_Template]
    
2. <span data-ttu-id="d1507-140">W oknie dialogowym "Wdróż tooResource grupy" hello, wybierz subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="d1507-140">Select your subscription in hello “Deploy tooResource Group” dialog.</span></span>
   
    ![Wdrażanie szablonu][6deploy_Template]

3. <span data-ttu-id="d1507-142">W tym miejscu można utworzyć grupy zasobów platformy Azure toodeploy szablon.</span><span class="sxs-lookup"><span data-stu-id="d1507-142">From here, you can create an Azure Resource Group toodeploy your Template to.</span></span>
   
    ![Nową grupę zasobów][new_resource]

4. <span data-ttu-id="d1507-144">Następnie kliknij przycisk **Edytuj parametry** tooenter parametry przekazywane tooyour szablonu.</span><span class="sxs-lookup"><span data-stu-id="d1507-144">Next, click **Edit Parameters** tooenter parameters that are passed tooyour Template.</span></span> <span data-ttu-id="d1507-145">Podaj hello nazwy użytkownika i hasła dla hello systemu operacyjnego, który jest wymagany toocreate hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="d1507-145">Provide hello username and password for hello OS, which is required toocreate hello deployment.</span></span> <span data-ttu-id="d1507-146">Jeśli nie masz narzędzia programu PowerShell dla programu Visual Studio, zainstalowane, zalecane jest toocheck **zapisywanie haseł** tooavoid ukryte wiersza polecenia programu PowerShell monit, lub użyj [Obsługa keyvault](https://azure.microsoft.com/blog/keyvault-support-for-arm-templates/).</span><span class="sxs-lookup"><span data-stu-id="d1507-146">If you don't have PowerShell Tools for Visual Studio installed, it is recommended toocheck **Save passwords** tooavoid a hidden PowerShell command-line prompt, or use [keyvault support](https://azure.microsoft.com/blog/keyvault-support-for-arm-templates/).</span></span>
   
    ![Edytowanie parametrów][edit_parameters]

5. <span data-ttu-id="d1507-148">Teraz kliknij **Wdróż**.</span><span class="sxs-lookup"><span data-stu-id="d1507-148">Now click **Deploy**.</span></span> <span data-ttu-id="d1507-149">Witaj **dane wyjściowe** okno zawiera hello postępu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="d1507-149">hello **Output** window shows hello deployment progress.</span></span> <span data-ttu-id="d1507-150">Należy pamiętać, że akcja hello jest wykonywany hello **AzureResourceGroup.ps1 Wdróż** skryptu.</span><span class="sxs-lookup"><span data-stu-id="d1507-150">Note that hello action is executing hello **Deploy-AzureResourceGroup.ps1** script.</span></span>
   
   ![Okno danych wyjściowych][output_window]

## <a name="exploring-your-virtual-machine-scale-set"></a><span data-ttu-id="d1507-152">Eksplorowanie sieci zestawu skali maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="d1507-152">Exploring your Virtual Machine Scale Set</span></span>
<span data-ttu-id="d1507-153">Po zakończeniu wdrażania hello, można wyświetlić hello nowego zestawu skalowania maszyn wirtualnych w Visual Studio hello **Eksplorator chmury** (Lista hello odświeżania).</span><span class="sxs-lookup"><span data-stu-id="d1507-153">Once hello deployment completes, you can view hello new Virtual Machine Scale Set in hello Visual Studio **Cloud Explorer** (refresh hello list).</span></span> <span data-ttu-id="d1507-154">Eksplorator chmury umożliwia zarządzanie zasobami Azure w programie Visual Studio podczas tworzenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d1507-154">Cloud Explorer lets you manage Azure resources in Visual Studio while developing applications.</span></span> <span data-ttu-id="d1507-155">Można również wyświetlić zestawu skalowania maszyn wirtualnych w hello [portalu Azure](https://portal.azure.com) i [Eksploratora zasobów Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d1507-155">You can also view your Virtual Machine Scale Set in hello [Azure portal](https://portal.azure.com) and [Azure Resource Explorer](https://resources.azure.com/).</span></span>

![Eksplorator chmury][cloud_explorer]

 <span data-ttu-id="d1507-157">Hello portal udostępnia najlepszy sposób hello toovisually zarządzać infrastruktury platformy Azure przy użyciu przeglądarki sieci web, gdy Eksploratora zasobów Azure zapewnia prosty sposób tooexplore i debugowania zasobów platformy Azure, nadanie okna do Witaj, "Wyświetl wystąpienia" i również przedstawiający programu PowerShell polecenia hello zasoby, które jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="d1507-157">hello portal provides hello best way toovisually manage your Azure infrastructure with a web browser, while Azure Resource Explorer provides an easy way tooexplore and debug Azure resources, giving a window into hello "instance view" and also showing PowerShell commands for hello resources you are looking at.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d1507-158">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d1507-158">Next steps</span></span>
<span data-ttu-id="d1507-159">Po pomyślnym wdrożeniu zestawy skalowania maszyny wirtualnej za pomocą programu Visual Studio, można dostosować toosuit Twojego projektu wymagań aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d1507-159">Once you’ve successfully deployed Virtual Machine Scale Sets through Visual Studio, you can further customize your project toosuit your application requirements.</span></span> <span data-ttu-id="d1507-160">Na przykład skonfigurować automatyczne skalowanie, dodając **Insights** zasobów, dodając infrastruktury tooyour szablonu (na przykład autonomicznych maszyn wirtualnych) lub wdrażanie aplikacji przy użyciu hello niestandardowego rozszerzenia skryptu.</span><span class="sxs-lookup"><span data-stu-id="d1507-160">For example, configure auto-scale by adding an **Insights** resource, adding infrastructure tooyour Template (like standalone VMs), or deploying applications using hello custom script extension.</span></span> <span data-ttu-id="d1507-161">Dobrym przykładem szablonów można znaleźć w hello [szablonów Szybki Start Azure](https://github.com/Azure/azure-quickstart-templates) repozytorium GitHub (Wyszukaj "vmss").</span><span class="sxs-lookup"><span data-stu-id="d1507-161">Good example templates can be found in hello [Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates) GitHub repository (search for "vmss").</span></span>

[file_new]: ./media/virtual-machine-scale-sets-vs-create/1-FileNew.png
[create_project]: ./media/virtual-machine-scale-sets-vs-create/2-CreateProject.png
[select_Template]: ./media/virtual-machine-scale-sets-vs-create/3b-SelectTemplateLin.png
[solution_explorer]: ./media/virtual-machine-scale-sets-vs-create/4-SolutionExplorer.png
[json_explorer]: ./media/virtual-machine-scale-sets-vs-create/10-JsonExplorer.png
[5deploy_Template]: ./media/virtual-machine-scale-sets-vs-create/5-DeployTemplate.png
[6deploy_Template]: ./media/virtual-machine-scale-sets-vs-create/6-DeployTemplate.png
[new_resource]: ./media/virtual-machine-scale-sets-vs-create/7-NewResourceGroup.png
[edit_parameters]: ./media/virtual-machine-scale-sets-vs-create/8-EditParameter.png
[output_window]: ./media/virtual-machine-scale-sets-vs-create/9-Output.png
[cloud_explorer]: ./media/virtual-machine-scale-sets-vs-create/12-CloudExplorer.png
