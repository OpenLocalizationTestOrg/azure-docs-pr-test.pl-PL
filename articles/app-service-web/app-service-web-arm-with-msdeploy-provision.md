---
title: "Wdrażanie aplikacji sieci web, przy użyciu MSDeploy z certyfikatów ssl i nazwy hosta"
description: "Szablon usługi Azure Resource Manager umożliwia wdrażanie aplikacji sieci web, przy użyciu MSDeploy i konfigurowanie niestandardowej nazwy hosta i certyfikatem SSL"
services: app-service\web
manager: erikre
documentationcenter: 
author: jodehavi
ms.assetid: 66366a72-cef7-4d75-8779-f4d32ed33cf7
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2016
ms.author: jodehavi
ms.openlocfilehash: a0e944d0d74ecb72a919538d54db330cbbdeef64
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-a-web-app-with-msdeploy-custom-hostname-and-ssl-certificate"></a><span data-ttu-id="6aaca-103">Wdrażanie aplikacji sieci web z MSDeploy, niestandardową nazwę hosta i certyfikat protokołu SSL</span><span class="sxs-lookup"><span data-stu-id="6aaca-103">Deploy a web app with MSDeploy, custom hostname and SSL certificate</span></span>
<span data-ttu-id="6aaca-104">Ten przewodnik przeprowadzi Cię przez tworzenie end-to-end wdrożenia dla aplikacji sieci Web platformy Azure, wykorzystując MSDeploy, a także Dodawanie niestandardowej nazwy hosta i certyfikat SSL do szablonu ARM.</span><span class="sxs-lookup"><span data-stu-id="6aaca-104">This guide walks through creating an end-to-end deployment for an Azure Web App, leveraging MSDeploy as well as adding a custom hostname and an SSL certificate to the ARM template.</span></span>

<span data-ttu-id="6aaca-105">Aby uzyskać więcej informacji na temat tworzenia szablonów, zobacz [Authoring Azure Resource Manager szablony](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="6aaca-105">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

### <a name="create-sample-application"></a><span data-ttu-id="6aaca-106">Tworzenie przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="6aaca-106">Create Sample Application</span></span>
<span data-ttu-id="6aaca-107">Wdrażania aplikacji sieci web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="6aaca-107">You will be deploying an ASP.NET web application.</span></span> <span data-ttu-id="6aaca-108">Pierwszym krokiem jest utworzenie prostą aplikację sieci web (lub można użyć istniejącego — w takim przypadku możesz pominąć ten krok).</span><span class="sxs-lookup"><span data-stu-id="6aaca-108">The first step is to create a simple web application (or you could choose to use an existing one - in which case you can skip this step).</span></span>

<span data-ttu-id="6aaca-109">Otwórz program Visual Studio 2015 i wybrać plik > Nowy projekt.</span><span class="sxs-lookup"><span data-stu-id="6aaca-109">Open Visual Studio 2015 and choose File > New Project.</span></span> <span data-ttu-id="6aaca-110">W wyświetlonym oknie dialogowym Wybierz sieci Web > Aplikacja sieci Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="6aaca-110">On the dialog that appears choose Web > ASP.NET Web Application.</span></span> <span data-ttu-id="6aaca-111">W obszarze szablonów wybierz sieci Web, a następnie wybierz szablon MVC.</span><span class="sxs-lookup"><span data-stu-id="6aaca-111">Under Templates choose Web and choose the MVC template.</span></span> <span data-ttu-id="6aaca-112">Wybierz *Zmień typ uwierzytelniania* do *bez uwierzytelniania*.</span><span class="sxs-lookup"><span data-stu-id="6aaca-112">Select *Change authentication type* to *No Authentication*.</span></span> <span data-ttu-id="6aaca-113">To jest tylko tworzenie przykładowej aplikacji, wystarczy.</span><span class="sxs-lookup"><span data-stu-id="6aaca-113">This is just to make the sample application as simple as possible.</span></span>

<span data-ttu-id="6aaca-114">W tym momencie będziesz mieć podstawowe aplikacji sieci web ASP.Net gotowe do użycia w ramach procesu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="6aaca-114">At this point you will have a basic ASP.Net web app ready to use as part of your deployment process.</span></span>

### <a name="create-msdeploy-package"></a><span data-ttu-id="6aaca-115">Utwórz pakiet MSDeploy</span><span class="sxs-lookup"><span data-stu-id="6aaca-115">Create MSDeploy package</span></span>
<span data-ttu-id="6aaca-116">Następnym krokiem jest, aby utworzyć pakiet do wdrożenia aplikacji sieci web na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="6aaca-116">Next step is to create the package to deploy the web app to Azure.</span></span> <span data-ttu-id="6aaca-117">W tym celu należy zapisać projekt, a następnie uruchom następujące polecenie w wierszu polecenia:</span><span class="sxs-lookup"><span data-stu-id="6aaca-117">To do this, save your project and then run the following from the command line:</span></span>

    msbuild yourwebapp.csproj /t:Package /p:PackageLocation="path\to\package.zip"

<span data-ttu-id="6aaca-118">Spowoduje to utworzenie pakietu ZIP w folderze tabelę PackageLocation.</span><span class="sxs-lookup"><span data-stu-id="6aaca-118">This will create a zipped package under the PackageLocation folder.</span></span> <span data-ttu-id="6aaca-119">Aplikacja jest teraz gotowa do wdrożenia, które można teraz utworzyć limit szablonu usługi Azure Resource Manager w tym.</span><span class="sxs-lookup"><span data-stu-id="6aaca-119">The application is now ready to be deployed, which you can now build out an Azure Resource Manager template to do that.</span></span>

### <a name="create-arm-template"></a><span data-ttu-id="6aaca-120">Utwórz szablon ARM</span><span class="sxs-lookup"><span data-stu-id="6aaca-120">Create ARM Template</span></span>
<span data-ttu-id="6aaca-121">Po pierwsze Zacznijmy podstawowy szablon ARM, który spowoduje utworzenie aplikacji sieci web i plan hostingu (należy pamiętać, że parametry i zmienne nie są pokazywane w celu jego skrócenia).</span><span class="sxs-lookup"><span data-stu-id="6aaca-121">First, let's start with a basic ARM template that will create a web application and a hosting plan (note that parameters and variables are not shown for brevity).</span></span>

    {
        "name": "[parameters('appServicePlanName')]",
        "type": "Microsoft.Web/serverfarms",
        "location": "[resourceGroup().location]",
        "apiVersion": "2014-06-01",
        "dependsOn": [ ],
        "tags": {
            "displayName": "appServicePlan"
        },
        "properties": {
            "name": "[parameters('appServicePlanName')]",
            "sku": "[parameters('appServicePlanSKU')]",
            "workerSize": "[parameters('appServicePlanWorkerSize')]",
            "numberOfWorkers": 1
        }
    },
    {
        "name": "[variables('webAppName')]",
        "type": "Microsoft.Web/sites",
        "location": "[resourceGroup().location]",
        "apiVersion": "2015-08-01",
        "dependsOn": [
            "[concat('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        ],
        "tags": {
            "[concat('hidden-related:', resourceGroup().id, '/providers/Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]": "Resource",
            "displayName": "webApp"
        },
        "properties": {
            "name": "[variables('webAppName')]",
            "serverFarmId": "[resourceId('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        }
    }

<span data-ttu-id="6aaca-122">Następnie należy zmodyfikować zasobów aplikacji sieci web do podjęcia zagnieżdżonych zasobów MSDeploy.</span><span class="sxs-lookup"><span data-stu-id="6aaca-122">Next, you will need to modify the web app resource to take a nested MSDeploy resource.</span></span> <span data-ttu-id="6aaca-123">Dzięki temu będzie można odwołania do pakietu utworzonego wcześniej i poinformuj usługi Azure Resource Manager umożliwia MSDeploy można wdrożyć pakietu dla aplikacji sieci Web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6aaca-123">This will allow you to reference the package created earlier and tell Azure Resource Manager to use MSDeploy to deploy the package to the Azure WebApp.</span></span> <span data-ttu-id="6aaca-124">Poniżej przedstawiono zasób Microsoft.Web/sites o zagnieżdżonych zasobów MSDeploy:</span><span class="sxs-lookup"><span data-stu-id="6aaca-124">The following shows the Microsoft.Web/sites resource with the nested MSDeploy resource:</span></span>

    {
        "name": "[variables('webAppName')]",
        "type": "Microsoft.Web/sites",
        "location": "[resourceGroup().location]",
        "apiVersion": "2015-08-01",
        "dependsOn": [
            "[concat('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        ],
        "tags": {
            "[concat('hidden-related:', resourceGroup().id, '/providers/Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]": "Resource",
            "displayName": "webApp"
        },
        "properties": {
            "name": "[variables('webAppName')]",
            "serverFarmId": "[resourceId('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        },
        "resources": [
            {
                "name": "MSDeploy",
                "type": "extensions",
                "location": "[resourceGroup().location]",
                "apiVersion": "2015-08-01",
                "dependsOn": [
                    "[concat('Microsoft.Web/sites/', variables('webAppName'))]"
                ],
                "tags": {
                    "displayName": "webDeploy"
                },
                "properties": {
                    "packageUri": "[concat(parameters('_artifactsLocation'), '/', parameters('webDeployPackageFolder'), '/', parameters('webDeployPackageFileName'), parameters('_artifactsLocationSasToken'))]",
                    "dbType": "None",
                    "connectionString": "",
                    "setParameters": {
                        "IIS Web Application Name": "[variables('webAppName')]"
                    }
                }
            }
        ]
    }

<span data-ttu-id="6aaca-125">Teraz można zauważyć, że zasób MSDeploy przyjmuje **packageUri** właściwość, która jest zdefiniowana w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="6aaca-125">Now you will notice that the MSDeploy resource takes a **packageUri** property which is defined as follows:</span></span>

    "packageUri": "[concat(parameters('_artifactsLocation'), '/', parameters('webDeployPackageFolder'), '/', parameters('webDeployPackageFileName'), parameters('_artifactsLocationSasToken'))]"

<span data-ttu-id="6aaca-126">To **packageUri** pobiera identyfikator uri konta magazynu, która wskazuje na konto magazynu, gdzie możesz przekazać pocztowy do pakietu.</span><span class="sxs-lookup"><span data-stu-id="6aaca-126">This **packageUri** takes the storage account uri which points to the storage account where you will upload your package zip to.</span></span> <span data-ttu-id="6aaca-127">Będzie korzystać z usługi Azure Resource Manager [sygnatury dostępu współdzielonego](../storage/common/storage-dotnet-shared-access-signature-part-1.md) do Rozwiń pakiet lokalnie z konta magazynu podczas wdrażania szablonu.</span><span class="sxs-lookup"><span data-stu-id="6aaca-127">The Azure Resource Manager will leverage [Shared Access Signatures](../storage/common/storage-dotnet-shared-access-signature-part-1.md) to pull the package down locally from the storage account when you deploy the template.</span></span> <span data-ttu-id="6aaca-128">Ten proces będzie można zautomatyzować za pomocą skryptu programu PowerShell, przekaż pakiet i wywołania interfejsu API zarządzania platformy Azure do tworzenia kluczy, wymaganych i przekazania ich na szablon jako parametry (*_artifactsLocation* i *_artifactsLocationSasToken*).</span><span class="sxs-lookup"><span data-stu-id="6aaca-128">This process will be automated via a PowerShell script that will upload the package and call the Azure Management API to create the keys required and pass those into the template as parameters (*_artifactsLocation* and *_artifactsLocationSasToken*).</span></span> <span data-ttu-id="6aaca-129">Należy określić parametry w folderze i nazwa pliku pakietu zostanie przesłany w ramach kontenera magazynu.</span><span class="sxs-lookup"><span data-stu-id="6aaca-129">You will need to define parameters for the folder and filename the package is uploaded to under the storage container.</span></span>

<span data-ttu-id="6aaca-130">Następnie należy dodać w inny zasób zagnieżdżonych konfiguracja powiązań z nazwami hostów wykorzystać domeny niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="6aaca-130">Next you need to add in another nested resource to setup the hostname bindings to leverage a custom domain.</span></span> <span data-ttu-id="6aaca-131">Najpierw należy zapewnić własnej nazwy hosta i ustaw go do weryfikacji przez platformę Azure własne jej — zobacz [Konfigurowanie niestandardowej nazwy domeny w usłudze Azure App Service](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="6aaca-131">You will first need to ensure that you own the hostname and set it up to be verified by Azure that you own it - see [Configure a custom domain name in Azure App Service](app-service-web-tutorial-custom-domain.md).</span></span> <span data-ttu-id="6aaca-132">Po zakończeniu tej operacji można dodać do szablonu w sekcji zasobów Microsoft.Web/sites następujące:</span><span class="sxs-lookup"><span data-stu-id="6aaca-132">Once that is done you can add the following to your template under the Microsoft.Web/sites resource section:</span></span>

    {
        "apiVersion": "2015-08-01",
        "type": "hostNameBindings",
        "name": "www.yourcustomdomain.com",
        "dependsOn": [
            "[concat('Microsoft.Web/sites/', variables('webAppName'))]"
        ],
        "properties": {
            "domainId": null,
            "hostNameType": "Verified",
            "siteName": "variables('webAppName')"
        }
    }

<span data-ttu-id="6aaca-133">Na koniec należy dodać najwyższego poziomu zasób Microsoft.Web/certificates.</span><span class="sxs-lookup"><span data-stu-id="6aaca-133">Finally you need to add another top level resource, Microsoft.Web/certificates.</span></span> <span data-ttu-id="6aaca-134">Ten zasób będzie zawierać certyfikatu SSL i będzie istnieć na tym samym poziomie jako aplikacji sieci web i plan hostingu.</span><span class="sxs-lookup"><span data-stu-id="6aaca-134">This resource will contain your SSL certificate and will exist at the same level as your web app and hosting plan.</span></span>

    {
        "name": "[parameters('certificateName')]",
        "apiVersion": "2014-04-01",
        "type": "Microsoft.Web/certificates",
        "location": "[resourceGroup().location]",
        "properties": {
            "pfxBlob": "pfx base64 blob",
            "password": "some pass"
        }
    }

<span data-ttu-id="6aaca-135">Musisz mieć ważny certyfikat SSL w celu skonfigurowania tego zasobu.</span><span class="sxs-lookup"><span data-stu-id="6aaca-135">You will need to have a valid SSL certificate in order to set up this resource.</span></span> <span data-ttu-id="6aaca-136">Po określeniu, że prawidłowy certyfikat należy wyodrębnić bajtów pfx jako ciąg base64.</span><span class="sxs-lookup"><span data-stu-id="6aaca-136">Once you have that valid certificate then you need to extract the pfx bytes as a base64 string.</span></span> <span data-ttu-id="6aaca-137">Użyj następującego polecenia programu PowerShell jest jedną opcję, aby wyodrębnić to:</span><span class="sxs-lookup"><span data-stu-id="6aaca-137">One option to extract this is to use the following PowerShell command:</span></span>

    $fileContentBytes = get-content 'C:\path\to\cert.pfx' -Encoding Byte

    [System.Convert]::ToBase64String($fileContentBytes) | Out-File 'pfx-bytes.txt'

<span data-ttu-id="6aaca-138">Użytkownik może następnie przekazać jako parametru, do wdrożenia szablonu ARM.</span><span class="sxs-lookup"><span data-stu-id="6aaca-138">You could then pass this as a parameter to your ARM deployment template.</span></span>

<span data-ttu-id="6aaca-139">Na tym etapie szablon ARM jest gotowy.</span><span class="sxs-lookup"><span data-stu-id="6aaca-139">At this point the ARM template is ready.</span></span>

### <a name="deploy-template"></a><span data-ttu-id="6aaca-140">Wdrażanie szablonu</span><span class="sxs-lookup"><span data-stu-id="6aaca-140">Deploy Template</span></span>
<span data-ttu-id="6aaca-141">Końcowe czynności mają element to wszystkich elementów do wdrażania pełnej end-to-end.</span><span class="sxs-lookup"><span data-stu-id="6aaca-141">The final steps are to piece this all together into a full end-to-end deployment.</span></span> <span data-ttu-id="6aaca-142">Aby wdrożenie łatwiej można wykorzystać **AzureResourceGroup.ps1 Wdróż** skrypt PowerShell, który jest dodawany po utworzeniu projektu grupy zasobów platformy Azure w Visual Studio, aby ułatwić przekazywanie wszelkie artefakty wymagane w szablonie.</span><span class="sxs-lookup"><span data-stu-id="6aaca-142">To make deployment easier you can leverage the **Deploy-AzureResourceGroup.ps1** PowerShell script that is added when you create an Azure Resource Group project in Visual Studio to help with uploading of any artifacts required in the template.</span></span> <span data-ttu-id="6aaca-143">Wymaga utworzono konto magazynu, którego chcesz użyć wcześniejsze.</span><span class="sxs-lookup"><span data-stu-id="6aaca-143">It requires you to have created a storage account you want to use ahead of time.</span></span> <span data-ttu-id="6aaca-144">Na przykład utworzono konto magazynu udostępnionego dla pakiet.zip do załadowania.</span><span class="sxs-lookup"><span data-stu-id="6aaca-144">For this example, I created a shared storage account for the package.zip to be uploaded.</span></span> <span data-ttu-id="6aaca-145">Skrypt będzie korzystać z narzędzia AzCopy, aby przekazać pakiet do konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="6aaca-145">The script will leverage AzCopy to upload the package to the storage account.</span></span> <span data-ttu-id="6aaca-146">Przekazać w lokalizacji folderu artefaktów i skrypt automatycznie przekazać do kontenera magazynu o nazwie wszystkie pliki w tym katalogu.</span><span class="sxs-lookup"><span data-stu-id="6aaca-146">You pass in your artifact folder location and the script will automatically upload all files within that directory to the named storage container.</span></span> <span data-ttu-id="6aaca-147">Po wywołaniu metody wdrażania AzureResourceGroup.ps1 należy zaktualizować powiązania SSL, aby zamapować niestandardową nazwę hosta przy użyciu certyfikatu SSL.</span><span class="sxs-lookup"><span data-stu-id="6aaca-147">After calling Deploy-AzureResourceGroup.ps1 you have to then update the SSL bindings to map the custom hostname with your SSL certificate.</span></span>

<span data-ttu-id="6aaca-148">Następujące PowerShell Wyświetla pełne wdrożenie wywoływania Wdróż-AzureResourceGroup.ps1:</span><span class="sxs-lookup"><span data-stu-id="6aaca-148">The following PowerShell shows the complete deployment calling the Deploy-AzureResourceGroup.ps1:</span></span>

    #Set resource group name
    $rgName = "Name-of-resource-group"

    #call deploy-azureresourcegroup script to deploy web app

    .\Deploy-AzureResourceGroup.ps1 -ResourceGroupLocation "East US" `
                                    -ResourceGroupName $rgName `
                                    -UploadArtifacts `
                                    -StorageAccountName "name-of-storage-acct-for-package" `
                                    -StorageAccountResourceGroupName "resource-group-name-storage-acct" `
                                    -TemplateFile "web-app-deploy.json" `
                                    -TemplateParametersFile "web-app-deploy-parameters.json" `
                                    -ArtifactStagingDirectory "C:\path\to\packagefolder\"

    #update web app to bind ssl certificate to hostname. This has to be done after creation above.

    $cert = Get-PfxCertificate -FilePath C:\path\to\certificate.pfx

    $ar = Get-AzureRmResource -Name nameofwebsite -ResourceGroupName $rgName -ResourceType Microsoft.Web/sites -ApiVersion 2014-11-01

    $props = $ar.Properties

    $props.HostNameSslStates[2].'SslState' = 1
    $props.HostNameSslStates[2].'thumbprint' = $cert.Thumbprint
    $props.hostNameSslStates[2].'toUpdate' = $true

    Set-AzureRmResource -ApiVersion 2014-11-01 -Name nameofwebsite -ResourceGroupName $rgName -ResourceType Microsoft.Web/sites -PropertyObject $props

<span data-ttu-id="6aaca-149">W tym momencie aplikacja powinna zostały wdrożone, oraz powinny być możliwe przeglądanie za pomocą https://www.yourcustomdomain.com</span><span class="sxs-lookup"><span data-stu-id="6aaca-149">At this point your application should have been deployed and you should be able to browse to it via https://www.yourcustomdomain.com</span></span>

