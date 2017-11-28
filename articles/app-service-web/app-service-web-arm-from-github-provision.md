---
title: "aaaDeploy aplikacji sieci web, która jest połączona z repozytorium GitHub tooa | Dokumentacja firmy Microsoft"
description: "Za pomocą usługi Azure Resource Manager toodeploy szablonu aplikacji sieci web, który zawiera projekt z repozytorium GitHub."
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
ms.openlocfilehash: 8b23416c4c06a60991517e6ee4cd82bebc5a9d73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-web-app-linked-tooa-github-repository"></a><span data-ttu-id="a47ad-103">Wdrażanie repozytorium GitHub tooa połączonych aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="a47ad-103">Deploy a web app linked tooa GitHub repository</span></span>
<span data-ttu-id="a47ad-104">W tym temacie dowiesz się, jak toocreate szablonu usługi Azure Resource Manager, która wdraża aplikację sieci web, która jest połączona tooa projektu w repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="a47ad-104">In this topic, you will learn how toocreate an Azure Resource Manager template that deploys a web app that is linked tooa project in a GitHub repository.</span></span> <span data-ttu-id="a47ad-105">Dowiesz się jak toodefine zasobów, do których są wdrażane i jak parametry toodefine, które są określone, podczas wdrażania hello jest wykonywana.</span><span class="sxs-lookup"><span data-stu-id="a47ad-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="a47ad-106">Można użyć tego szablonu własnych wdrożeniach lub dostosować go toomeet wymagań.</span><span class="sxs-lookup"><span data-stu-id="a47ad-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="a47ad-107">Aby uzyskać więcej informacji na temat tworzenia szablonów, zobacz [Authoring Azure Resource Manager szablony](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a47ad-107">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="a47ad-108">Hello pełną szablonu, zobacz [połączonej aplikacji sieci Web szablonu tooGitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="a47ad-108">For hello complete template, see [Web App Linked tooGitHub template](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-deploy"></a><span data-ttu-id="a47ad-109">Zostanie wdrożona</span><span class="sxs-lookup"><span data-stu-id="a47ad-109">What you will deploy</span></span>
<span data-ttu-id="a47ad-110">W przypadku tego szablonu zostanie wdrożona w aplikacji sieci web zawierający kod hello z projektu w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="a47ad-110">With this template, you will deploy a web app that contains hello code from a project in GitHub.</span></span>

<span data-ttu-id="a47ad-111">toorun automatycznie hello wdrożenia, kliknij powitania po przycisku:</span><span class="sxs-lookup"><span data-stu-id="a47ad-111">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="a47ad-112">[![Wdrażanie tooAzure](./media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="a47ad-112">[![Deploy tooAzure](./media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="a47ad-113">Parametry</span><span class="sxs-lookup"><span data-stu-id="a47ad-113">Parameters</span></span>
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

### <a name="repourl"></a><span data-ttu-id="a47ad-114">repoURL</span><span class="sxs-lookup"><span data-stu-id="a47ad-114">repoURL</span></span>
<span data-ttu-id="a47ad-115">adres URL Hello repozytorium GitHub, zawierający hello toodeploy projektu.</span><span class="sxs-lookup"><span data-stu-id="a47ad-115">hello URL for GitHub repository that contains hello project toodeploy.</span></span> <span data-ttu-id="a47ad-116">Ten parametr zawiera wartość domyślną, ale ta wartość jest tylko zamierzonego tooshow należy jak tooprovide hello adres URL dla repozytorium.</span><span class="sxs-lookup"><span data-stu-id="a47ad-116">This parameter contains a default value but this value is only intended tooshow you how tooprovide hello URL for repository.</span></span> <span data-ttu-id="a47ad-117">Tej wartości można użyć podczas testowania hello szablonu, ale będzie tooprovide hello URL własnych repozytorium podczas pracy z hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="a47ad-117">You can use this value when testing hello template but you will want tooprovide hello URL your own repository when working with hello template.</span></span>

    "repoURL": {
        "type": "string",
        "defaultValue": "https://github.com/davidebbo-test/Mvc52Application.git"
    }

### <a name="branch"></a><span data-ttu-id="a47ad-118">Gałęzi</span><span class="sxs-lookup"><span data-stu-id="a47ad-118">branch</span></span>
<span data-ttu-id="a47ad-119">Rozgałęzienie Hello hello repozytorium toouse podczas wdrażania aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="a47ad-119">hello branch of hello repository toouse when deploying hello application.</span></span> <span data-ttu-id="a47ad-120">Wartość domyślna Hello jest baza danych master, ale można podać nazwę hello żadnych gałęzi w repozytorium hello że chcesz toodeploy.</span><span class="sxs-lookup"><span data-stu-id="a47ad-120">hello default value is master, but you can provide hello name of any branch in hello repository that you wish toodeploy.</span></span>

    "branch": {
        "type": "string",
        "defaultValue": "master"
    }

## <a name="resources-toodeploy"></a><span data-ttu-id="a47ad-121">Toodeploy zasobów</span><span class="sxs-lookup"><span data-stu-id="a47ad-121">Resources toodeploy</span></span>
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="web-app"></a><span data-ttu-id="a47ad-122">Aplikacja internetowa</span><span class="sxs-lookup"><span data-stu-id="a47ad-122">Web app</span></span>
<span data-ttu-id="a47ad-123">Tworzy hello aplikacji sieci web, który jest połączony toohello projektu w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="a47ad-123">Creates hello web app that is linked toohello project in GitHub.</span></span> 

<span data-ttu-id="a47ad-124">Należy określić nazwę hello hello aplikacji sieci web za pośrednictwem hello **siteName** parametru i lokalizację hello hello aplikacji sieci web za pośrednictwem hello **siteLocation** parametru.</span><span class="sxs-lookup"><span data-stu-id="a47ad-124">You specify hello name of hello web app through hello **siteName** parameter, and hello location of hello web app through hello **siteLocation** parameter.</span></span> <span data-ttu-id="a47ad-125">W hello **dependsOn** elementu hello szablon definiuje hello aplikacji sieci web jako zależne od usługi hello plan hostingu.</span><span class="sxs-lookup"><span data-stu-id="a47ad-125">In hello **dependsOn** element, hello template defines hello web app as dependent on hello service hosting plan.</span></span> <span data-ttu-id="a47ad-126">Ponieważ jest on zależny od hello plan hostingu, hello aplikacji sieci web nie zostanie utworzony, do momentu zakończenia hello plan hostingu tworzona.</span><span class="sxs-lookup"><span data-stu-id="a47ad-126">Because it is dependent on hello hosting plan, hello web app is not created until hello hosting plan has finished being created.</span></span> <span data-ttu-id="a47ad-127">Witaj **dependsOn** element jest tylko używane toospecify kolejności wdrażania.</span><span class="sxs-lookup"><span data-stu-id="a47ad-127">hello **dependsOn** element is only used toospecify deployment order.</span></span> <span data-ttu-id="a47ad-128">Jeśli nie zostanie zaznaczone hello aplikacji sieci web jako zależne hello plan hostingu, Mananger zasobów platformy Azure będzie podejmować toocreate oba zasoby na powitania tym samym czasie i może zostać wyświetlony błąd hello aplikacji sieci web zostanie utworzony przed hello plan hostingu.</span><span class="sxs-lookup"><span data-stu-id="a47ad-128">If you do not mark hello web app as dependent on hello hosting plan, Azure Resource Mananger will attempt toocreate both resources at hello same time and you may receive an error if hello web app is created before hello hosting plan.</span></span>

<span data-ttu-id="a47ad-129">Aplikacja sieci web Hello ma również zasobu podrzędnego, który jest zdefiniowany w **zasobów** poniższej sekcji.</span><span class="sxs-lookup"><span data-stu-id="a47ad-129">hello web app also has a child resource which is defined in **resources** section below.</span></span> <span data-ttu-id="a47ad-130">Ten zasób podrzędnych definiuje kontroli źródła dla projektu hello wdrażane hello aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="a47ad-130">This child resource defines source control for hello project deployed with hello web app.</span></span> <span data-ttu-id="a47ad-131">W tym szablonie hello kontroli źródła jest połączony tooa określonego repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="a47ad-131">In this template, hello source control is linked tooa particular GitHub repository.</span></span> <span data-ttu-id="a47ad-132">repozytorium GitHub Hello jest zdefiniowana z kodem hello **"RepoUrl": "https://github.com/davidebbo-test/Mvc52Application.git"** może adres URL repozytorium hello kodowane należy toocreate szablon, który wdraża wielokrotnie pojedynczego projektu podczas wymagające hello minimalną liczbę parametrów.</span><span class="sxs-lookup"><span data-stu-id="a47ad-132">hello GitHub repository is defined with hello code **"RepoUrl":"https://github.com/davidebbo-test/Mvc52Application.git"** You might hard-code hello repository URL when you want toocreate a template that repeatedly deploys a single project while requiring hello minimum number of parameters.</span></span>
<span data-ttu-id="a47ad-133">Zamiast kodować hello adres URL repozytorium, możesz dodać parametr adresu URL repozytorium hello i użycie tej wartości na powitania **RepoUrl** właściwości.</span><span class="sxs-lookup"><span data-stu-id="a47ad-133">Instead of hard-coding hello repository URL, you can add a parameter for hello repository URL and use that value for hello **RepoUrl** property.</span></span>

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

## <a name="commands-toorun-deployment"></a><span data-ttu-id="a47ad-134">Polecenia toorun wdrożenia</span><span class="sxs-lookup"><span data-stu-id="a47ad-134">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="a47ad-135">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a47ad-135">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json -siteName ExampleSite -hostingPlanName ExamplePlan -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="a47ad-136">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a47ad-136">Azure CLI</span></span>

    azure group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json

### <a name="azure-cli-20"></a><span data-ttu-id="a47ad-137">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="a47ad-137">Azure CLI 2.0</span></span>

    az group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json --parameters '@azuredeploy.parameters.json'

> [!NOTE] 
> <span data-ttu-id="a47ad-138">Dla zawartości pliku JSON hello parametrów, zobacz [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json).</span><span class="sxs-lookup"><span data-stu-id="a47ad-138">For content of hello parameters JSON file, see [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json).</span></span>
>
>

