---
title: "Wdrażanie aplikacji sieci web, która jest połączona z repozytorium GitHub | Dokumentacja firmy Microsoft"
description: "Szablon usługi Azure Resource Manager umożliwia wdrażanie aplikacji sieci web, który zawiera projekt z repozytorium GitHub."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 32739607-85fe-43c8-a4dc-1feb46d93a4d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2016
ms.author: cephalin
ms.openlocfilehash: 77064802814296d0c21f004534e4264d2f97252e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-web-app-linked-to-a-github-repository"></a><span data-ttu-id="f8bcc-103">Wdrażanie aplikacji sieci web, połączony z repozytorium GitHub</span><span class="sxs-lookup"><span data-stu-id="f8bcc-103">Deploy a web app linked to a GitHub repository</span></span>
<span data-ttu-id="f8bcc-104">W tym temacie dowiesz się, jak utworzyć szablon usługi Azure Resource Manager, która wdraża aplikację sieci web, która jest połączona z projektem w repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="f8bcc-104">In this topic, you will learn how to create an Azure Resource Manager template that deploys a web app that is linked to a project in a GitHub repository.</span></span> <span data-ttu-id="f8bcc-105">Dowiesz się, jak do definiowania zasobów, do których są wdrażane i sposób definiowania parametrów, które są określone, gdy wdrożenie jest wykonywane.</span><span class="sxs-lookup"><span data-stu-id="f8bcc-105">You will learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="f8bcc-106">Można użyć tego szablonu na potrzeby własnych wdrożeń lub dostosować go do konkretnych potrzeb.</span><span class="sxs-lookup"><span data-stu-id="f8bcc-106">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="f8bcc-107">Aby uzyskać więcej informacji na temat tworzenia szablonów, zobacz [Authoring Azure Resource Manager szablony](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="f8bcc-107">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="f8bcc-108">Zakończenie szablonu, zobacz [sieci Web aplikacji połączonych do szablonu usługi GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="f8bcc-108">For the complete template, see [Web App Linked to GitHub template](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-deploy"></a><span data-ttu-id="f8bcc-109">Zostanie wdrożona</span><span class="sxs-lookup"><span data-stu-id="f8bcc-109">What you will deploy</span></span>
<span data-ttu-id="f8bcc-110">W przypadku tego szablonu zostanie wdrożona aplikacja sieci web, która zawiera kod z projektem w usłudze GitHub.</span><span class="sxs-lookup"><span data-stu-id="f8bcc-110">With this template, you will deploy a web app that contains the code from a project in GitHub.</span></span>

<span data-ttu-id="f8bcc-111">Aby automatycznie uruchomić wdrożenie, kliknij poniższy przycisk:</span><span class="sxs-lookup"><span data-stu-id="f8bcc-111">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="f8bcc-112">[![Wdrażanie na platformie Azure](./media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="f8bcc-112">[![Deploy to Azure](./media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="f8bcc-113">Parametry</span><span class="sxs-lookup"><span data-stu-id="f8bcc-113">Parameters</span></span>
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

### <a name="repourl"></a><span data-ttu-id="f8bcc-114">repoURL</span><span class="sxs-lookup"><span data-stu-id="f8bcc-114">repoURL</span></span>
<span data-ttu-id="f8bcc-115">Adres URL repozytorium GitHub, zawierający projekt do wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="f8bcc-115">The URL for GitHub repository that contains the project to deploy.</span></span> <span data-ttu-id="f8bcc-116">Ten parametr zawiera wartość domyślną, ale ta wartość jest przeznaczona tylko do opisano, jak wprowadzić adres URL repozytorium.</span><span class="sxs-lookup"><span data-stu-id="f8bcc-116">This parameter contains a default value but this value is only intended to show you how to provide the URL for repository.</span></span> <span data-ttu-id="f8bcc-117">Tej wartości można użyć podczas testowania szablonu, ale można podać adres URL własnych repozytorium podczas pracy z szablonem.</span><span class="sxs-lookup"><span data-stu-id="f8bcc-117">You can use this value when testing the template but you will want to provide the URL your own repository when working with the template.</span></span>

    "repoURL": {
        "type": "string",
        "defaultValue": "https://github.com/davidebbo-test/Mvc52Application.git"
    }

### <a name="branch"></a><span data-ttu-id="f8bcc-118">Gałęzi</span><span class="sxs-lookup"><span data-stu-id="f8bcc-118">branch</span></span>
<span data-ttu-id="f8bcc-119">Rozgałęzienie repozytorium do użycia podczas wdrażania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f8bcc-119">The branch of the repository to use when deploying the application.</span></span> <span data-ttu-id="f8bcc-120">Wartością domyślną jest baza danych master, ale można podać nazwę dowolnego gałęzi w repozytorium, który chcesz wdrożyć.</span><span class="sxs-lookup"><span data-stu-id="f8bcc-120">The default value is master, but you can provide the name of any branch in the repository that you wish to deploy.</span></span>

    "branch": {
        "type": "string",
        "defaultValue": "master"
    }

## <a name="resources-to-deploy"></a><span data-ttu-id="f8bcc-121">Zasoby wymagające wdrożenia</span><span class="sxs-lookup"><span data-stu-id="f8bcc-121">Resources to deploy</span></span>
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="web-app"></a><span data-ttu-id="f8bcc-122">Aplikacja internetowa</span><span class="sxs-lookup"><span data-stu-id="f8bcc-122">Web app</span></span>
<span data-ttu-id="f8bcc-123">Tworzy aplikacji sieci web, z którym powiązany jest projekt w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="f8bcc-123">Creates the web app that is linked to the project in GitHub.</span></span> 

<span data-ttu-id="f8bcc-124">Należy określić nazwę aplikacji sieci web za pośrednictwem **siteName** parametr i lokalizacja aplikacji sieci web za pomocą **siteLocation** parametru.</span><span class="sxs-lookup"><span data-stu-id="f8bcc-124">You specify the name of the web app through the **siteName** parameter, and the location of the web app through the **siteLocation** parameter.</span></span> <span data-ttu-id="f8bcc-125">W **dependsOn** element, szablon definiuje aplikacji sieci web jako zależne od usługi plan hostingu.</span><span class="sxs-lookup"><span data-stu-id="f8bcc-125">In the **dependsOn** element, the template defines the web app as dependent on the service hosting plan.</span></span> <span data-ttu-id="f8bcc-126">Ponieważ jest on zależny od plan hostingu, aplikacji sieci web nie zostanie utworzony, do momentu zakończenia plan hostingu tworzona.</span><span class="sxs-lookup"><span data-stu-id="f8bcc-126">Because it is dependent on the hosting plan, the web app is not created until the hosting plan has finished being created.</span></span> <span data-ttu-id="f8bcc-127">**DependsOn** elementu tylko służy do określania kolejności wdrażania.</span><span class="sxs-lookup"><span data-stu-id="f8bcc-127">The **dependsOn** element is only used to specify deployment order.</span></span> <span data-ttu-id="f8bcc-128">Jeśli aplikacja sieci web jako zależne plan hostingu nie jest zaznaczone, Mananger zasobów Azure podejmie próbę utworzenia oba zasoby w tym samym czasie i może wystąpić błąd, jeśli aplikacja sieci web został utworzony przed plan hostingu.</span><span class="sxs-lookup"><span data-stu-id="f8bcc-128">If you do not mark the web app as dependent on the hosting plan, Azure Resource Mananger will attempt to create both resources at the same time and you may receive an error if the web app is created before the hosting plan.</span></span>

<span data-ttu-id="f8bcc-129">Aplikacja sieci web ma również zasobu podrzędnego, który jest zdefiniowany w **zasobów** poniższej sekcji.</span><span class="sxs-lookup"><span data-stu-id="f8bcc-129">The web app also has a child resource which is defined in **resources** section below.</span></span> <span data-ttu-id="f8bcc-130">Ten zasób podrzędnych definiuje kontroli źródła dla projektu z aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="f8bcc-130">This child resource defines source control for the project deployed with the web app.</span></span> <span data-ttu-id="f8bcc-131">W tym szablonie kontroli źródła jest połączony z konkretnym repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="f8bcc-131">In this template, the source control is linked to a particular GitHub repository.</span></span> <span data-ttu-id="f8bcc-132">Repozytorium GitHub jest zdefiniowany kod **"RepoUrl": "https://github.com/davidebbo-test/Mvc52Application.git"** możesz kodowane adres URL repozytorium, gdy chcesz utworzyć szablon, który wdraża wielokrotnie pojedynczy Projekt podczas wymagające minimalną liczbę parametrów.</span><span class="sxs-lookup"><span data-stu-id="f8bcc-132">The GitHub repository is defined with the code **"RepoUrl":"https://github.com/davidebbo-test/Mvc52Application.git"** You might hard-code the repository URL when you want to create a template that repeatedly deploys a single project while requiring the minimum number of parameters.</span></span>
<span data-ttu-id="f8bcc-133">Zamiast kodować adres URL repozytorium, możesz dodać parametr adresu URL repozytorium i użycie tej wartości dla **RepoUrl** właściwości.</span><span class="sxs-lookup"><span data-stu-id="f8bcc-133">Instead of hard-coding the repository URL, you can add a parameter for the repository URL and use that value for the **RepoUrl** property.</span></span>

    {
      "apiVersion": "2015-08-01",
      "name": "[parameters('siteName')]",
      "type": "Microsoft.Web/sites",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', parameters('hostingPlanName'))]"
      ],
      "properties": {
        "serverFarmId": "[parameters('hostingPlanName')]"
      },
      "resources": [
        {
          "apiVersion": "2015-08-01",
          "name": "web",
          "type": "sourcecontrols",
          "dependsOn": [
            "[resourceId('Microsoft.Web/Sites', parameters('siteName'))]"
          ],
          "properties": {
            "RepoUrl": "[parameters('repoURL')]",
            "branch": "[parameters('branch')]",
            "IsManualIntegration": true
          }
        }
      ]
    }

## <a name="commands-to-run-deployment"></a><span data-ttu-id="f8bcc-134">Polecenia umożliwiające uruchomienie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="f8bcc-134">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="f8bcc-135">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f8bcc-135">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json -siteName ExampleSite -hostingPlanName ExamplePlan -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="f8bcc-136">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="f8bcc-136">Azure CLI</span></span>

    azure group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json

### <a name="azure-cli-20"></a><span data-ttu-id="f8bcc-137">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="f8bcc-137">Azure CLI 2.0</span></span>

    az group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json --parameters '@azuredeploy.parameters.json'

> [!NOTE] 
> <span data-ttu-id="f8bcc-138">Dla zawartości pliku JSON parametrów, zobacz [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json).</span><span class="sxs-lookup"><span data-stu-id="f8bcc-138">For content of the parameters JSON file, see [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json).</span></span>
>
>

