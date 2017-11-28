---
title: "aaaDeploy aplikacji sieci web przy użyciu narzędzia MSDeploy z certyfikatów ssl i nazwy hosta"
description: "Użycie toodeploy szablonu usługi Azure Resource Manager aplikacji sieci web przy użyciu MSDeploy i konfigurowanie niestandardowej nazwy hosta i certyfikatem SSL"
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
ms.openlocfilehash: ac13f4a7d14ae182e8e7ced5adff30491422d1e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-web-app-with-msdeploy-custom-hostname-and-ssl-certificate"></a><span data-ttu-id="fa278-103">Wdrażanie aplikacji sieci web z MSDeploy, niestandardową nazwę hosta i certyfikat protokołu SSL</span><span class="sxs-lookup"><span data-stu-id="fa278-103">Deploy a web app with MSDeploy, custom hostname and SSL certificate</span></span>
<span data-ttu-id="fa278-104">Ten przewodnik przeprowadzi Cię przez tworzenie end-to-end wdrożenia dla aplikacji sieci Web platformy Azure, wykorzystaniu MSDeploy, a także Dodawanie niestandardowej nazwy hosta i szablon ARM toohello certyfikatu SSL.</span><span class="sxs-lookup"><span data-stu-id="fa278-104">This guide walks through creating an end-to-end deployment for an Azure Web App, leveraging MSDeploy as well as adding a custom hostname and an SSL certificate toohello ARM template.</span></span>

<span data-ttu-id="fa278-105">Aby uzyskać więcej informacji na temat tworzenia szablonów, zobacz [Authoring Azure Resource Manager szablony](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="fa278-105">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

### <a name="create-sample-application"></a><span data-ttu-id="fa278-106">Tworzenie przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="fa278-106">Create Sample Application</span></span>
<span data-ttu-id="fa278-107">Wdrażania aplikacji sieci web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="fa278-107">You will be deploying an ASP.NET web application.</span></span> <span data-ttu-id="fa278-108">pierwszym krokiem Hello toocreate prostą aplikację sieci web (lub toouse można wybrać istniejący — w takim przypadku możesz pominąć ten krok).</span><span class="sxs-lookup"><span data-stu-id="fa278-108">hello first step is toocreate a simple web application (or you could choose toouse an existing one - in which case you can skip this step).</span></span>

<span data-ttu-id="fa278-109">Otwórz program Visual Studio 2015 i wybrać plik > Nowy projekt.</span><span class="sxs-lookup"><span data-stu-id="fa278-109">Open Visual Studio 2015 and choose File > New Project.</span></span> <span data-ttu-id="fa278-110">W oknie dialogowym hello, który pojawia się wybrać sieci Web > Aplikacja sieci Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="fa278-110">On hello dialog that appears choose Web > ASP.NET Web Application.</span></span> <span data-ttu-id="fa278-111">W obszarze szablonów wybierz sieci Web, a następnie wybierz szablon MVC hello.</span><span class="sxs-lookup"><span data-stu-id="fa278-111">Under Templates choose Web and choose hello MVC template.</span></span> <span data-ttu-id="fa278-112">Wybierz *Zmień typ uwierzytelniania* za*bez uwierzytelniania*.</span><span class="sxs-lookup"><span data-stu-id="fa278-112">Select *Change authentication type* too*No Authentication*.</span></span> <span data-ttu-id="fa278-113">Jest to po prostu toomake hello przykładowej aplikacji, wystarczy.</span><span class="sxs-lookup"><span data-stu-id="fa278-113">This is just toomake hello sample application as simple as possible.</span></span>

<span data-ttu-id="fa278-114">W tym momencie będziesz mieć podstawowe ASP.Net web app gotowe toouse w ramach procesu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="fa278-114">At this point you will have a basic ASP.Net web app ready toouse as part of your deployment process.</span></span>

### <a name="create-msdeploy-package"></a><span data-ttu-id="fa278-115">Utwórz pakiet MSDeploy</span><span class="sxs-lookup"><span data-stu-id="fa278-115">Create MSDeploy package</span></span>
<span data-ttu-id="fa278-116">Następnym krokiem jest tooAzure aplikacji sieci web hello toodeploy toocreate hello pakietu.</span><span class="sxs-lookup"><span data-stu-id="fa278-116">Next step is toocreate hello package toodeploy hello web app tooAzure.</span></span> <span data-ttu-id="fa278-117">toodo, Zapisz projekt, a następnie uruchom następujące hello z wiersza polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="fa278-117">toodo this, save your project and then run hello following from hello command line:</span></span>

    msbuild yourwebapp.csproj /t:Package /p:PackageLocation="path\to\package.zip"

<span data-ttu-id="fa278-118">Spowoduje to utworzenie pakietu ZIP w folderze tabelę PackageLocation hello.</span><span class="sxs-lookup"><span data-stu-id="fa278-118">This will create a zipped package under hello PackageLocation folder.</span></span> <span data-ttu-id="fa278-119">Witaj aplikacji jest teraz gotowa toobe wdrożeniu, które można teraz utworzyć limit toodo szablonu usługi Azure Resource Manager który.</span><span class="sxs-lookup"><span data-stu-id="fa278-119">hello application is now ready toobe deployed, which you can now build out an Azure Resource Manager template toodo that.</span></span>

### <a name="create-arm-template"></a><span data-ttu-id="fa278-120">Utwórz szablon ARM</span><span class="sxs-lookup"><span data-stu-id="fa278-120">Create ARM Template</span></span>
<span data-ttu-id="fa278-121">Po pierwsze Zacznijmy podstawowy szablon ARM, który spowoduje utworzenie aplikacji sieci web i plan hostingu (należy pamiętać, że parametry i zmienne nie są pokazywane w celu jego skrócenia).</span><span class="sxs-lookup"><span data-stu-id="fa278-121">First, let's start with a basic ARM template that will create a web application and a hosting plan (note that parameters and variables are not shown for brevity).</span></span>

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

<span data-ttu-id="fa278-122">Następnie należy toomodify hello sieci web aplikacji zasobów tootake zagnieżdżonych zasobów MSDeploy.</span><span class="sxs-lookup"><span data-stu-id="fa278-122">Next, you will need toomodify hello web app resource tootake a nested MSDeploy resource.</span></span> <span data-ttu-id="fa278-123">To spowoduje Zezwól możesz tooreference hello pakietu utworzonego wcześniej i poinformuj usługi Azure Resource Manager toouse MSDeploy toodeploy hello pakietu toohello aplikacji sieci Web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fa278-123">This will allow you tooreference hello package created earlier and tell Azure Resource Manager toouse MSDeploy toodeploy hello package toohello Azure WebApp.</span></span> <span data-ttu-id="fa278-124">Oto Hello hello Microsoft.Web/sites zasobów z zasobem MSDeploy hello zagnieżdżone:</span><span class="sxs-lookup"><span data-stu-id="fa278-124">hello following shows hello Microsoft.Web/sites resource with hello nested MSDeploy resource:</span></span>

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

<span data-ttu-id="fa278-125">Teraz można zauważyć przyjmuje tego hello zasobów MSDeploy **packageUri** właściwość, która jest zdefiniowana w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="fa278-125">Now you will notice that hello MSDeploy resource takes a **packageUri** property which is defined as follows:</span></span>

    "packageUri": "[concat(parameters('_artifactsLocation'), '/', parameters('webDeployPackageFolder'), '/', parameters('webDeployPackageFileName'), parameters('_artifactsLocationSasToken'))]"

<span data-ttu-id="fa278-126">To **packageUri** przyjmuje hello identyfikator uri konta magazynu, którego konto magazynu toohello, gdzie możesz przekazać pocztowy pakietu do punktu.</span><span class="sxs-lookup"><span data-stu-id="fa278-126">This **packageUri** takes hello storage account uri which points toohello storage account where you will upload your package zip to.</span></span> <span data-ttu-id="fa278-127">Witaj usługi Azure Resource Manager będzie korzystać z [sygnatury dostępu współdzielonego](../storage/common/storage-dotnet-shared-access-signature-part-1.md) pakietu hello toopull dół lokalnie z konta magazynu hello podczas wdrażania szablonu hello.</span><span class="sxs-lookup"><span data-stu-id="fa278-127">hello Azure Resource Manager will leverage [Shared Access Signatures](../storage/common/storage-dotnet-shared-access-signature-part-1.md) toopull hello package down locally from hello storage account when you deploy hello template.</span></span> <span data-ttu-id="fa278-128">Ten proces będzie można zautomatyzować za pomocą skryptu programu PowerShell, przekaż pakiet hello i wywołać hello Azure Management API toocreate hello klucze są wymagane i przekazania ich na powitania szablonu jako parametry (*_artifactsLocation* i *_artifactsLocationSasToken*).</span><span class="sxs-lookup"><span data-stu-id="fa278-128">This process will be automated via a PowerShell script that will upload hello package and call hello Azure Management API toocreate hello keys required and pass those into hello template as parameters (*_artifactsLocation* and *_artifactsLocationSasToken*).</span></span> <span data-ttu-id="fa278-129">Musisz mieć parametry toodefine folderu hello oraz filename hello pakiet jest kontenera magazynu hello toounder przekazane.</span><span class="sxs-lookup"><span data-stu-id="fa278-129">You will need toodefine parameters for hello folder and filename hello package is uploaded toounder hello storage container.</span></span>

<span data-ttu-id="fa278-130">Następnie należy tooadd w innym zagnieżdżonych zasobów toosetup hello hostname powiązania tooleverage domeny niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="fa278-130">Next you need tooadd in another nested resource toosetup hello hostname bindings tooleverage a custom domain.</span></span> <span data-ttu-id="fa278-131">Będzie pierwszy tooensure potrzeby właścicielem hello nazwy hosta, a następnie skonfigurować toobe zweryfikowane przez usługę Azure jego właścicielem — zobacz [Konfigurowanie niestandardowej nazwy domeny w usłudze Azure App Service](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="fa278-131">You will first need tooensure that you own hello hostname and set it up toobe verified by Azure that you own it - see [Configure a custom domain name in Azure App Service](app-service-web-tutorial-custom-domain.md).</span></span> <span data-ttu-id="fa278-132">Po zakończeniu tej operacji można dodać następującego szablonu tooyour w sekcji zasobów Microsoft.Web/sites hello hello:</span><span class="sxs-lookup"><span data-stu-id="fa278-132">Once that is done you can add hello following tooyour template under hello Microsoft.Web/sites resource section:</span></span>

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

<span data-ttu-id="fa278-133">Na koniec należy tooadd inny zasób najwyższego poziomu, Microsoft.Web/certificates.</span><span class="sxs-lookup"><span data-stu-id="fa278-133">Finally you need tooadd another top level resource, Microsoft.Web/certificates.</span></span> <span data-ttu-id="fa278-134">Ten zasób będzie zawierać certyfikatu SSL i będzie istniał w momencie powitalne sam poziom jako aplikacji sieci web i hostingu plan.</span><span class="sxs-lookup"><span data-stu-id="fa278-134">This resource will contain your SSL certificate and will exist at hello same level as your web app and hosting plan.</span></span>

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

<span data-ttu-id="fa278-135">Konieczne będzie toohave ważnego certyfikatu SSL w kolejności tooset się tego zasobu.</span><span class="sxs-lookup"><span data-stu-id="fa278-135">You will need toohave a valid SSL certificate in order tooset up this resource.</span></span> <span data-ttu-id="fa278-136">Po określeniu, że prawidłowy certyfikat należy tooextract hello pfx bajtów jako ciąg base64.</span><span class="sxs-lookup"><span data-stu-id="fa278-136">Once you have that valid certificate then you need tooextract hello pfx bytes as a base64 string.</span></span> <span data-ttu-id="fa278-137">Jedną z opcji tooextract to hello toouse następującego polecenia programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="fa278-137">One option tooextract this is toouse hello following PowerShell command:</span></span>

    $fileContentBytes = get-content 'C:\path\to\cert.pfx' -Encoding Byte

    [System.Convert]::ToBase64String($fileContentBytes) | Out-File 'pfx-bytes.txt'

<span data-ttu-id="fa278-138">Można następnie przekazać to jako parametr tooyour ARM wdrażania szablonu.</span><span class="sxs-lookup"><span data-stu-id="fa278-138">You could then pass this as a parameter tooyour ARM deployment template.</span></span>

<span data-ttu-id="fa278-139">Na tym etapie szablon ARM hello jest gotowy.</span><span class="sxs-lookup"><span data-stu-id="fa278-139">At this point hello ARM template is ready.</span></span>

### <a name="deploy-template"></a><span data-ttu-id="fa278-140">Wdrażanie szablonu</span><span class="sxs-lookup"><span data-stu-id="fa278-140">Deploy Template</span></span>
<span data-ttu-id="fa278-141">Witaj ostatnie kroki są toopiece to wszystkich elementów do wdrażania pełnej end-to-end.</span><span class="sxs-lookup"><span data-stu-id="fa278-141">hello final steps are toopiece this all together into a full end-to-end deployment.</span></span> <span data-ttu-id="fa278-142">łatwiejsze, można wykorzystać hello wdrożenia toomake **AzureResourceGroup.ps1 Wdróż** skrypt PowerShell, który jest dodawany po utworzeniu projektu grupy zasobów platformy Azure w Visual Studio toohelp z przekazywanie wszelkie artefakty wymagane w Szablon Hello.</span><span class="sxs-lookup"><span data-stu-id="fa278-142">toomake deployment easier you can leverage hello **Deploy-AzureResourceGroup.ps1** PowerShell script that is added when you create an Azure Resource Group project in Visual Studio toohelp with uploading of any artifacts required in hello template.</span></span> <span data-ttu-id="fa278-143">Wymaga to toohave utworzone konto magazynu, które chcesz toouse wcześniejsze.</span><span class="sxs-lookup"><span data-stu-id="fa278-143">It requires you toohave created a storage account you want toouse ahead of time.</span></span> <span data-ttu-id="fa278-144">Na przykład utworzono konto magazynu udostępnionego dla toobe pakiet.zip hello przekazany.</span><span class="sxs-lookup"><span data-stu-id="fa278-144">For this example, I created a shared storage account for hello package.zip toobe uploaded.</span></span> <span data-ttu-id="fa278-145">skrypt Hello będzie korzystać z konta magazynu toohello AzCopy tooupload hello pakietu.</span><span class="sxs-lookup"><span data-stu-id="fa278-145">hello script will leverage AzCopy tooupload hello package toohello storage account.</span></span> <span data-ttu-id="fa278-146">Przekaż w lokalizacji folderu artefaktów i hello skryptu spowoduje automatyczne przekazywanie wszystkich plików w tym toohello katalog o nazwie kontenera magazynu.</span><span class="sxs-lookup"><span data-stu-id="fa278-146">You pass in your artifact folder location and hello script will automatically upload all files within that directory toohello named storage container.</span></span> <span data-ttu-id="fa278-147">Po wywołaniu metody wdrażania AzureResourceGroup.ps1 masz toothen aktualizacji hello SSL powiązania toomap hello niestandardową nazwę hosta przy użyciu certyfikatu SSL.</span><span class="sxs-lookup"><span data-stu-id="fa278-147">After calling Deploy-AzureResourceGroup.ps1 you have toothen update hello SSL bindings toomap hello custom hostname with your SSL certificate.</span></span>

<span data-ttu-id="fa278-148">powitania po programu PowerShell pokazuje hello hello wywoływania ukończenia wdrożenia Wdróż-AzureResourceGroup.ps1:</span><span class="sxs-lookup"><span data-stu-id="fa278-148">hello following PowerShell shows hello complete deployment calling hello Deploy-AzureResourceGroup.ps1:</span></span>

    #Set resource group name
    $rgName = "Name-of-resource-group"

    #call deploy-azureresourcegroup script toodeploy web app

    .\Deploy-AzureResourceGroup.ps1 -ResourceGroupLocation "East US" `
                                    -ResourceGroupName $rgName `
                                    -UploadArtifacts `
                                    -StorageAccountName "name-of-storage-acct-for-package" `
                                    -StorageAccountResourceGroupName "resource-group-name-storage-acct" `
                                    -TemplateFile "web-app-deploy.json" `
                                    -TemplateParametersFile "web-app-deploy-parameters.json" `
                                    -ArtifactStagingDirectory "C:\path\to\packagefolder\"

    #update web app toobind ssl certificate toohostname. This has toobe done after creation above.

    $cert = Get-PfxCertificate -FilePath C:\path\to\certificate.pfx

    $ar = Get-AzureRmResource -Name nameofwebsite -ResourceGroupName $rgName -ResourceType Microsoft.Web/sites -ApiVersion 2014-11-01

    $props = $ar.Properties

    $props.HostNameSslStates[2].'SslState' = 1
    $props.HostNameSslStates[2].'thumbprint' = $cert.Thumbprint
    $props.hostNameSslStates[2].'toUpdate' = $true

    Set-AzureRmResource -ApiVersion 2014-11-01 -Name nameofwebsite -ResourceGroupName $rgName -ResourceType Microsoft.Web/sites -PropertyObject $props

<span data-ttu-id="fa278-149">W tym momencie aplikacja powinna zostały wdrożone, oraz powinno być możliwe toobrowse tooit za pośrednictwem https://www.yourcustomdomain.com</span><span class="sxs-lookup"><span data-stu-id="fa278-149">At this point your application should have been deployed and you should be able toobrowse tooit via https://www.yourcustomdomain.com</span></span>

