---
title: "Wdrażanie zestawu skalowania maszyn wirtualnych za pomocą programu Visual Studio | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 78a4b0c8d305f57f495402cecb92d18425ff6bff
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-create-a-virtual-machine-scale-set-with-visual-studio"></a><span data-ttu-id="3e9d4-103">Tworzenie zestawu skalowania maszyn wirtualnych z programem Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3e9d4-103">How to create a Virtual Machine Scale Set with Visual Studio</span></span>
<span data-ttu-id="3e9d4-104">W tym artykule przedstawiono sposób wdrażania usługi Azure zestawu skalowania maszyn wirtualnych za pomocą programu Visual Studio wdrożenie grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="3e9d4-104">This article shows you how to deploy an Azure Virtual Machine Scale Set using a Visual Studio Resource Group Deployment.</span></span>

<span data-ttu-id="3e9d4-105">[Zestawy skalowania maszyny wirtualnej Azure](https://azure.microsoft.com/blog/azure-vm-scale-sets-public-preview/) jest zasobem rozwiązań usługi obliczenia Azure, aby wdrożyć i zarządzanie kolekcją podobnych maszyn wirtualnych z automatycznego skalowania i równoważenie obciążenia.</span><span class="sxs-lookup"><span data-stu-id="3e9d4-105">[Azure Virtual Machine Scale Sets](https://azure.microsoft.com/blog/azure-vm-scale-sets-public-preview/) is an Azure Compute resource to deploy and manage a collection of similar virtual machines with auto-scale and load balancing.</span></span> <span data-ttu-id="3e9d4-106">Można udostępnić i wdrożyć zestawy skalowania maszyny wirtualnej przy użyciu [szablony Menedżera zasobów Azure](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="3e9d4-106">You can provision and deploy Virtual Machine Scale Sets using [Azure Resource Manager Templates](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="3e9d4-107">Szablony usługi Azure Resource Manager można wdrożyć przy użyciu interfejsu wiersza polecenia Azure, programu PowerShell, REST, a także bezpośrednio z programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3e9d4-107">Azure Resource Manager Templates can be deployed using Azure CLI, PowerShell, REST and also directly from Visual Studio.</span></span> <span data-ttu-id="3e9d4-108">Program Visual Studio oferuje zestaw przykład szablonów, które można wdrożyć w ramach projektu wdrożenia grupy zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3e9d4-108">Visual Studio provides a set of example templates, which can be deployed as part of an Azure Resource Group Deployment project.</span></span>

<span data-ttu-id="3e9d4-109">Wdrożenia grupy zasobów platformy Azure służą do grupowania i opublikować zestawu powiązanych zasobów systemu Azure w ramach operacji pojedynczego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="3e9d4-109">Azure Resource Group deployments are a way to group and publish a set of related Azure resources in a single deployment operation.</span></span> <span data-ttu-id="3e9d4-110">Więcej informacji o nich w tym miejscu: [tworzenie i wdrażanie grup zasobów platformy Azure za pomocą programu Visual Studio](../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="3e9d4-110">You can learn more about them here: [Creating and deploying Azure resource groups through Visual Studio](../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span></span>

## <a name="pre-requisites"></a><span data-ttu-id="3e9d4-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3e9d4-111">Pre-requisites</span></span>
<span data-ttu-id="3e9d4-112">Aby rozpocząć wdrażanie zestawy skalowania maszyny wirtualnej w programie Visual Studio, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="3e9d4-112">To get started deploying Virtual Machine Scale Sets in Visual Studio, you need the following:</span></span>

* <span data-ttu-id="3e9d4-113">Visual Studio 2013 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="3e9d4-113">Visual Studio 2013 or later</span></span>
* <span data-ttu-id="3e9d4-114">Zestaw Azure SDK 2.8 2.7 i 2.9</span><span class="sxs-lookup"><span data-stu-id="3e9d4-114">Azure SDK 2.7, 2.8 or 2.9</span></span>

>[!NOTE]
><span data-ttu-id="3e9d4-115">W poniższych instrukcjach przyjęto w przypadku korzystania z programu Visual Studio z [Azure SDK 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).</span><span class="sxs-lookup"><span data-stu-id="3e9d4-115">These instructions assume you are using Visual Studio with [Azure SDK 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).</span></span>

## <a name="creating-a-project"></a><span data-ttu-id="3e9d4-116">Tworzenie projektu</span><span class="sxs-lookup"><span data-stu-id="3e9d4-116">Creating a Project</span></span>
1. <span data-ttu-id="3e9d4-117">Utwórz nowy projekt w programie Visual Studio, wybierając **pliku | Nowy | Projekt**.</span><span class="sxs-lookup"><span data-stu-id="3e9d4-117">Create a new project in Visual Studio by choosing **File | New | Project**.</span></span>
   
    ![Nowy plik][file_new]

2. <span data-ttu-id="3e9d4-119">W obszarze **Visual C# | Chmura**, wybierz **usługi Azure Resource Manager** do utworzenia projektu wdrażania szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3e9d4-119">Under **Visual C# | Cloud**, choose **Azure Resource Manager** to create a project for deploying an Azure Resource Manager Template.</span></span>
   
    ![Tworzenie projektu][create_project]

3. <span data-ttu-id="3e9d4-121">Z listy szablonów wybierz Linux albo szablon ustawić skali maszyny wirtualnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="3e9d4-121">From the list of Templates, select either the Linux or Windows Virtual Machine Scale Set Template.</span></span>
   
   ![Wybierz szablon][select_Template]

4. <span data-ttu-id="3e9d4-123">Po utworzeniu projektu Zobacz skryptów programu PowerShell wdrażania szablonu usługi Azure Resource Manager i pliku parametrów dla zestawu skalowania maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="3e9d4-123">Once your project is created you see PowerShell deployment scripts, an Azure Resource Manager Template, and a parameter file for the Virtual Machine Scale Set.</span></span>
   
    ![Eksplorator rozwiązań][solution_explorer]

## <a name="customize-your-project"></a><span data-ttu-id="3e9d4-125">Dostosowywanie projektu</span><span class="sxs-lookup"><span data-stu-id="3e9d4-125">Customize your project</span></span>
<span data-ttu-id="3e9d4-126">Można teraz edytować szablonu, aby dostosować go na potrzeby aplikacji, takich jak dodawanie właściwości rozszerzenia maszyny Wirtualnej lub edytowanie reguły równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="3e9d4-126">Now you can edit the Template to customize it for your application's needs, such as adding VM extension properties or editing load balancing rules.</span></span> <span data-ttu-id="3e9d4-127">Domyślnie szablony zestawu skali maszyny wirtualnej są skonfigurowane do rozszerzenia AzureDiagnostics, co ułatwia dodawanie reguł skalowania automatycznego wdrażania.</span><span class="sxs-lookup"><span data-stu-id="3e9d4-127">By default the Virtual Machine Scale Set Templates are configured to deploy the AzureDiagnostics extension, which makes it easy to add autoscale rules.</span></span> <span data-ttu-id="3e9d4-128">Ponadto wdraża z publicznym adresem IP skonfigurowano reguły NAT ruchu przychodzącego modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="3e9d4-128">It also deploys a load balancer with a public IP address, configured with inbound NAT rules.</span></span> 

<span data-ttu-id="3e9d4-129">Moduł równoważenia obciążenia umożliwia połączenie z wystąpień maszyn wirtualnych z protokołu SSH (Linux) lub protokołu RDP (system Windows).</span><span class="sxs-lookup"><span data-stu-id="3e9d4-129">The load balancer lets you connect to the VM instances with SSH (Linux) or RDP (Windows).</span></span> <span data-ttu-id="3e9d4-130">Zakres portów frontonu rozpoczyna się od 50000.</span><span class="sxs-lookup"><span data-stu-id="3e9d4-130">The front-end port range starts at 50000.</span></span> <span data-ttu-id="3e9d4-131">Dla systemu linux, oznacza to, że jeśli użytkownik SSH do portu 50000, możesz są kierowane do portu 22 pierwsza maszyna wirtualna w zestawie skalowania.</span><span class="sxs-lookup"><span data-stu-id="3e9d4-131">For linux this means that if you SSH to port 50000, you are routed to port 22 of the first VM in the Scale Set.</span></span> <span data-ttu-id="3e9d4-132">Łączenie z porcie 50001 jest kierowany do portu 22 drugiej maszyny wirtualnej i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="3e9d4-132">Connecting to port 50001 is routed to port 22 of the second VM and so on.</span></span>

 <span data-ttu-id="3e9d4-133">Dobrym sposobem Edytuj szablony z programem Visual Studio jest konspekt pliku JSON umożliwia organizowanie parametrów, zmienne i zasobów.</span><span class="sxs-lookup"><span data-stu-id="3e9d4-133">A good way to edit your Templates with Visual Studio is to use the JSON Outline to organize the parameters, variables, and resources.</span></span> <span data-ttu-id="3e9d4-134">Po zrozumieniu schematu programu Visual Studio może wskazywać błędy w szablonie przed przystąpieniem do wdrażania.</span><span class="sxs-lookup"><span data-stu-id="3e9d4-134">With an understanding of the schema Visual Studio can point out errors in your Template before you deploy it.</span></span>

![Eksplorator JSON][json_explorer]

## <a name="deploy-the-project"></a><span data-ttu-id="3e9d4-136">Wdrażanie projektu</span><span class="sxs-lookup"><span data-stu-id="3e9d4-136">Deploy the project</span></span>
1. <span data-ttu-id="3e9d4-137">Wdróż szablon Menedżera zasobów Azure, aby utworzyć zasób zestawu skalowania maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="3e9d4-137">Deploy the Azure Resource Manager Template to create the Virtual Machine Scale Set resource.</span></span> <span data-ttu-id="3e9d4-138">Kliknij prawym przyciskiem myszy węzeł projektu i wybierz polecenie **Wdróż | Nowe wdrożenie**.</span><span class="sxs-lookup"><span data-stu-id="3e9d4-138">Right-click on the project node and choose **Deploy | New Deployment**.</span></span>
   
    ![Wdrażanie szablonu][5deploy_Template]
    
2. <span data-ttu-id="3e9d4-140">Wybierz subskrypcję, w oknie dialogowym "Wdrożyć do grupy zasobów".</span><span class="sxs-lookup"><span data-stu-id="3e9d4-140">Select your subscription in the “Deploy to Resource Group” dialog.</span></span>
   
    ![Wdrażanie szablonu][6deploy_Template]

3. <span data-ttu-id="3e9d4-142">W tym miejscu można utworzyć grupy zasobów platformy Azure, aby wdrożyć szablon.</span><span class="sxs-lookup"><span data-stu-id="3e9d4-142">From here, you can create an Azure Resource Group to deploy your Template to.</span></span>
   
    ![Nową grupę zasobów][new_resource]

4. <span data-ttu-id="3e9d4-144">Następnie kliknij przycisk **Edytuj parametry** o wprowadzenie parametrów, które są przekazywane do szablonu.</span><span class="sxs-lookup"><span data-stu-id="3e9d4-144">Next, click **Edit Parameters** to enter parameters that are passed to your Template.</span></span> <span data-ttu-id="3e9d4-145">Podaj nazwę użytkownika i hasło dla systemu operacyjnego, który jest wymagany do tworzenia wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="3e9d4-145">Provide the username and password for the OS, which is required to create the deployment.</span></span> <span data-ttu-id="3e9d4-146">Jeśli nie masz narzędzia programu PowerShell dla programu Visual Studio, zainstalowane, zalecane jest Sprawdź **zapisywanie haseł** w celu uniknięcia ukryte wierszu polecenia programu PowerShell lub użyj [Obsługa keyvault](https://azure.microsoft.com/blog/keyvault-support-for-arm-templates/).</span><span class="sxs-lookup"><span data-stu-id="3e9d4-146">If you don't have PowerShell Tools for Visual Studio installed, it is recommended to check **Save passwords** to avoid a hidden PowerShell command-line prompt, or use [keyvault support](https://azure.microsoft.com/blog/keyvault-support-for-arm-templates/).</span></span>
   
    ![Edytowanie parametrów][edit_parameters]

5. <span data-ttu-id="3e9d4-148">Teraz kliknij **Wdróż**.</span><span class="sxs-lookup"><span data-stu-id="3e9d4-148">Now click **Deploy**.</span></span> <span data-ttu-id="3e9d4-149">**Dane wyjściowe** okno będzie wyświetlany postęp wdrażania.</span><span class="sxs-lookup"><span data-stu-id="3e9d4-149">The **Output** window shows the deployment progress.</span></span> <span data-ttu-id="3e9d4-150">Należy pamiętać, że akcja jest wykonywana **AzureResourceGroup.ps1 Wdróż** skryptu.</span><span class="sxs-lookup"><span data-stu-id="3e9d4-150">Note that the action is executing the **Deploy-AzureResourceGroup.ps1** script.</span></span>
   
   ![Okno danych wyjściowych][output_window]

## <a name="exploring-your-virtual-machine-scale-set"></a><span data-ttu-id="3e9d4-152">Eksplorowanie sieci zestawu skali maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="3e9d4-152">Exploring your Virtual Machine Scale Set</span></span>
<span data-ttu-id="3e9d4-153">Po zakończeniu wdrożenia, można wyświetlić zestawu skali maszyny wirtualnej w programie Visual Studio **Eksplorator chmury** (odświeżenie listy).</span><span class="sxs-lookup"><span data-stu-id="3e9d4-153">Once the deployment completes, you can view the new Virtual Machine Scale Set in the Visual Studio **Cloud Explorer** (refresh the list).</span></span> <span data-ttu-id="3e9d4-154">Eksplorator chmury umożliwia zarządzanie zasobami Azure w programie Visual Studio podczas tworzenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3e9d4-154">Cloud Explorer lets you manage Azure resources in Visual Studio while developing applications.</span></span> <span data-ttu-id="3e9d4-155">Można również wyświetlić z uprawnieniami w zestawie skalowania maszyn wirtualnych [portalu Azure](https://portal.azure.com) i [Eksploratora zasobów Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3e9d4-155">You can also view your Virtual Machine Scale Set in the [Azure portal](https://portal.azure.com) and [Azure Resource Explorer](https://resources.azure.com/).</span></span>

![Eksplorator chmury][cloud_explorer]

 <span data-ttu-id="3e9d4-157">Portal zawiera najlepszy sposób, aby wizualnie zarządzać infrastruktury platformy Azure przy użyciu przeglądarki sieci web, gdy Eksploratora zasobów Azure pozwala łatwo eksplorować i debugowania zasobów platformy Azure, nadanie okna w widoku"wystąpienia", a także wyświetlanie poleceń programu PowerShell dla zasobów jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="3e9d4-157">The portal provides the best way to visually manage your Azure infrastructure with a web browser, while Azure Resource Explorer provides an easy way to explore and debug Azure resources, giving a window into the "instance view" and also showing PowerShell commands for the resources you are looking at.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e9d4-158">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3e9d4-158">Next steps</span></span>
<span data-ttu-id="3e9d4-159">Po pomyślnym wdrożeniu zestawy skalowania maszyny wirtualnej za pomocą programu Visual Studio, można dostosować projekt do własnych wymagań aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3e9d4-159">Once you’ve successfully deployed Virtual Machine Scale Sets through Visual Studio, you can further customize your project to suit your application requirements.</span></span> <span data-ttu-id="3e9d4-160">Na przykład skonfigurować automatyczne skalowanie, dodając **Insights** zasobów, dodawania infrastruktury do szablonu (na przykład autonomicznych maszyn wirtualnych), lub wdrażania aplikacji za pomocą niestandardowego rozszerzenia skryptu.</span><span class="sxs-lookup"><span data-stu-id="3e9d4-160">For example, configure auto-scale by adding an **Insights** resource, adding infrastructure to your Template (like standalone VMs), or deploying applications using the custom script extension.</span></span> <span data-ttu-id="3e9d4-161">Dobrym przykładem szablonów można znaleźć w [szablonów Szybki Start Azure](https://github.com/Azure/azure-quickstart-templates) repozytorium GitHub (Wyszukaj "vmss").</span><span class="sxs-lookup"><span data-stu-id="3e9d4-161">Good example templates can be found in the [Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates) GitHub repository (search for "vmss").</span></span>

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
