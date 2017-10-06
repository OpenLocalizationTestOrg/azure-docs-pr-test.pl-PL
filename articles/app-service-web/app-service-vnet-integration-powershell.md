---
title: "aaaConnect Twojej sieci wirtualnej tooyour aplikacji przy użyciu programu PowerShell"
description: "Instrukcje dotyczące działania tooconnect tooand z sieci wirtualnych za pomocą programu PowerShell"
services: app-service
documentationcenter: 
author: ccompy
manager: erikre
editor: cephalin
ms.assetid: a5c76e77-972a-431c-b14b-3611dae1631b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/29/2016
ms.author: ccompy
ms.openlocfilehash: c9d0fa99d02cab7b2c7211a1b2f7b7d0cd27ee8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-app-tooyour-virtual-network-by-using-powershell"></a><span data-ttu-id="2c77e-103">Połączenie sieci wirtualnej tooyour aplikacji przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="2c77e-103">Connect your app tooyour virtual network by using PowerShell</span></span>
## <a name="overview"></a><span data-ttu-id="2c77e-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="2c77e-104">Overview</span></span>
<span data-ttu-id="2c77e-105">W usłudze Azure App Service można połączyć aplikacji (sieć web, mobilnych lub interfejsu API) tooan sieci wirtualnej platformy Azure (VNet) w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="2c77e-105">In Azure App Service, you can connect your app (web, mobile, or API) tooan Azure virtual network (VNet) in your subscription.</span></span> <span data-ttu-id="2c77e-106">Ta funkcja jest nazywana integracji sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2c77e-106">This feature is called VNet Integration.</span></span> <span data-ttu-id="2c77e-107">Funkcja integracji z sieciami wirtualnymi Hello nie należy mylić z funkcją środowiska usługi aplikacji hello, dzięki czemu można toorun wystąpienia usługi Azure App Service w Twojej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2c77e-107">hello VNet Integration feature should not be confused with hello App Service Environment feature, which allows you toorun an instance of Azure App Service in your virtual network.</span></span>

<span data-ttu-id="2c77e-108">Funkcja integracji z sieciami wirtualnymi Hello ma interfejsu użytkownika (UI) w hello nowego portalu służącego toointegrate z sieciami wirtualnymi, które zostały wdrożone przy użyciu modelu wdrażania usługi Azure Resource Manager hello albo hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="2c77e-108">hello VNet Integration feature has a user interface (UI) in hello new portal that you can use toointegrate with virtual networks that are deployed by using either hello classic deployment model or hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="2c77e-109">Aby uzyskać dodatkowe informacje o funkcji hello toolearn zobacz [integracji aplikacji z sieci wirtualnej platformy Azure](web-sites-integrate-with-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="2c77e-109">If you want toolearn more about hello feature, see [Integrate your app with an Azure virtual network](web-sites-integrate-with-vnet.md).</span></span>

<span data-ttu-id="2c77e-110">Ten artykuł zawiera nie na temat sposobu toouse hello interfejsu użytkownika, ale raczej dotyczące integracji tooenable przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2c77e-110">This article is not about how toouse hello UI but rather about how tooenable integration by using PowerShell.</span></span> <span data-ttu-id="2c77e-111">Ponieważ hello poleceń dla każdego modelu wdrażania są różne, w tym artykule ma sekcji do każdego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="2c77e-111">Because hello commands for each deployment model are different, this article has a section for each deployment model.</span></span>  

<span data-ttu-id="2c77e-112">Przed kontynuowaniem w tym artykule upewnij się, że masz:</span><span class="sxs-lookup"><span data-stu-id="2c77e-112">Before you continue with this article, ensure that you have:</span></span>

* <span data-ttu-id="2c77e-113">Witaj, zainstalowany najnowszy zestaw SDK usługi Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2c77e-113">hello latest Azure PowerShell SDK installed.</span></span> <span data-ttu-id="2c77e-114">Można go zainstalować z hello Instalatora platformy sieci Web.</span><span class="sxs-lookup"><span data-stu-id="2c77e-114">You can install this with hello Web Platform Installer.</span></span>
* <span data-ttu-id="2c77e-115">Aplikacja w usłudze Azure App Service w Standard lub Premium jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="2c77e-115">An app in Azure App Service running in a Standard or Premium SKU.</span></span>

## <a name="classic-virtual-networks"></a><span data-ttu-id="2c77e-116">Klasycznych sieci wirtualnych</span><span class="sxs-lookup"><span data-stu-id="2c77e-116">Classic virtual networks</span></span>
<span data-ttu-id="2c77e-117">W tej sekcji opisano trzy zadania dla sieci wirtualnych korzystających z hello klasycznego modelu wdrażania:</span><span class="sxs-lookup"><span data-stu-id="2c77e-117">This section explains three tasks for virtual networks that use hello classic deployment model:</span></span>

1. <span data-ttu-id="2c77e-118">Łączenie aplikacji tooa istniejących sieci wirtualnej i jest konfigurowane połączenie punkt lokacja z bramą.</span><span class="sxs-lookup"><span data-stu-id="2c77e-118">Connect your app tooa preexisting virtual network that has a gateway and is configured for point-to-site connectivity.</span></span>
2. <span data-ttu-id="2c77e-119">Aktualizowanie informacji o integracji sieci wirtualnej dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2c77e-119">Update your virtual network integration information for your app.</span></span>
3. <span data-ttu-id="2c77e-120">Aplikację można rozłączyć sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2c77e-120">Disconnect your app from your virtual network.</span></span>

### <a name="connect-an-app-tooa-classic-vnet"></a><span data-ttu-id="2c77e-121">Połącz tooa aplikacji klasycznej sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="2c77e-121">Connect an app tooa classic VNet</span></span>
<span data-ttu-id="2c77e-122">tooconnect aplikacji tooa sieci wirtualnej, wykonaj następujące trzy kroki:</span><span class="sxs-lookup"><span data-stu-id="2c77e-122">tooconnect an app tooa virtual network, follow these three steps:</span></span>

1. <span data-ttu-id="2c77e-123">Deklarowanie toohello aplikacji sieci web, że zostanie do niej dołączanie do określonej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2c77e-123">Declare toohello web app that it will be joining a particular virtual network.</span></span> <span data-ttu-id="2c77e-124">Aplikacja Hello wygeneruje certyfikat, który będzie mógł skorzystać z sieci wirtualnej toohello połączenia punkt lokacja.</span><span class="sxs-lookup"><span data-stu-id="2c77e-124">hello app will generate a certificate that will be given toohello virtual network for point-to-site connectivity.</span></span>
2. <span data-ttu-id="2c77e-125">Przekaż hello web app certyfikatu toohello wirtualnej sieci, a następnie pobrać hello identyfikator URI pakietu sieci VPN punkt lokacja.</span><span class="sxs-lookup"><span data-stu-id="2c77e-125">Upload hello web app certificate toohello virtual network, and then retrieve hello point-to-site VPN package URI.</span></span>
3. <span data-ttu-id="2c77e-126">Zaktualizuj połączenie sieci wirtualnej aplikacji sieci web hello z pakietem punkt lokacja hello identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="2c77e-126">Update hello web app's virtual network connection with hello point-to-site package URI.</span></span>

<span data-ttu-id="2c77e-127">Witaj pierwszy i trzeci kroki są w pełni skryptowe, ale drugi etap hello wymaga jednorazowe, ręczna Akcja za pośrednictwem portalu hello lub tooperform dostępu **PUT** lub **poprawka** akcje na powitania sieci wirtualnej Usługa Azure Resource Manager punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="2c77e-127">hello first and third steps are fully scriptable, but hello second step requires a one-time, manual action through hello portal, or access tooperform **PUT** or **PATCH** actions on hello virtual network Azure Resource Manager endpoint.</span></span> <span data-ttu-id="2c77e-128">Skontaktuj się z pomocą techniczną platformy Azure toohave to włączone.</span><span class="sxs-lookup"><span data-stu-id="2c77e-128">Contact Azure Support toohave this enabled.</span></span> <span data-ttu-id="2c77e-129">Przed rozpoczęciem upewnij się, czy masz klasycznego siecią wirtualną, która ma już włączone połączenie punkt lokacja i wdrożone bramę.</span><span class="sxs-lookup"><span data-stu-id="2c77e-129">Before you start, make sure that you have a classic virtual network that has point-to-site connectivity already enabled and a deployed gateway.</span></span> <span data-ttu-id="2c77e-130">toocreate hello bramy i Włącz lokacji punktu połączenia, należy toouse hello portalu zgodnie z opisem w [Tworzenie bramy sieci VPN][createvpngateway].</span><span class="sxs-lookup"><span data-stu-id="2c77e-130">toocreate hello gateway and enable point-to-site connectivity, you need toouse hello portal as described at [Creating a VPN gateway][createvpngateway].</span></span>

<span data-ttu-id="2c77e-131">Witaj klasycznej sieci wirtualnej musi toobe w hello tej samej subskrypcji co w usłudze App Service plan, który jest integrowany z aplikacja hello blokad.</span><span class="sxs-lookup"><span data-stu-id="2c77e-131">hello classic virtual network needs toobe in hello same subscription as your App Service plan that holds hello app that you are integrating with.</span></span>

##### <a name="set-up-azure-powershell-sdk"></a><span data-ttu-id="2c77e-132">Konfigurowanie programu Azure PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="2c77e-132">Set up Azure PowerShell SDK</span></span>
<span data-ttu-id="2c77e-133">Otwórz okno programu PowerShell i skonfigurować konto platformy Azure i subskrypcji przy użyciu:</span><span class="sxs-lookup"><span data-stu-id="2c77e-133">Open a PowerShell window and set up your Azure account and subscription by using:</span></span>

    Login-AzureRmAccount

<span data-ttu-id="2c77e-134">To polecenie spowoduje otwarcie tooget monitu o poświadczenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2c77e-134">That command will open a prompt tooget your Azure credentials.</span></span> <span data-ttu-id="2c77e-135">Po zalogowaniu, użyj jednej z powitania po subskrypcji hello tooselect poleceń, które mają toouse.</span><span class="sxs-lookup"><span data-stu-id="2c77e-135">After you sign in, use either of hello following commands tooselect hello subscription that you want toouse.</span></span> <span data-ttu-id="2c77e-136">Upewnij się, że używasz hello subskrypcji, że sieć wirtualna i plan usługi aplikacji znajdują się w.</span><span class="sxs-lookup"><span data-stu-id="2c77e-136">Make sure that you are using hello subscription that your virtual network and App Service plan are in.</span></span>

    Select-AzureRmSubscription –SubscriptionName [WebAppSubscriptionName]

<span data-ttu-id="2c77e-137">lub</span><span class="sxs-lookup"><span data-stu-id="2c77e-137">or</span></span>

    Select-AzureRmSubscription –SubscriptionId [WebAppSubscriptionId]

##### <a name="variables-used-in-this-article"></a><span data-ttu-id="2c77e-138">Zmienne używane w tym artykule</span><span class="sxs-lookup"><span data-stu-id="2c77e-138">Variables used in this article</span></span>
<span data-ttu-id="2c77e-139">polecenia toosimplify, możemy ustawi **$Configuration** PowerShell zmienna o określonej konfiguracji hello.</span><span class="sxs-lookup"><span data-stu-id="2c77e-139">toosimplify commands, we will set a **$Configuration** PowerShell variable with hello specific configuration.</span></span>

<span data-ttu-id="2c77e-140">Ustaw zmienną w następujący sposób w programie PowerShell z hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="2c77e-140">Set a variable as follows in PowerShell with hello following parameters:</span></span>

    $Configuration = @{}
    $Configuration.WebAppResourceGroup = "[Your web app resource group]"
    $Configuration.WebAppName = "[Your web app name]"
    $Configuration.VnetSubscriptionId = "[Your vnet subscription id]"
    $Configuration.VnetResourceGroup = "[Your vnet resource group]"
    $Configuration.VnetName = "[Your vnet name]"

<span data-ttu-id="2c77e-141">Lokalizacja aplikacji Hello powinna być hello lokalizacji bez spacji.</span><span class="sxs-lookup"><span data-stu-id="2c77e-141">hello app location should be hello location without any spaces.</span></span> <span data-ttu-id="2c77e-142">Zachodnie stany USA jest na przykład westus.</span><span class="sxs-lookup"><span data-stu-id="2c77e-142">For example, West US is westus.</span></span>

    $Configuration.WebAppLocation = "[Your web app Location]"

<span data-ttu-id="2c77e-143">Następny element Hello jest miejsca zapisu hello certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="2c77e-143">hello next item is where hello certificate should be written.</span></span> <span data-ttu-id="2c77e-144">Należy ścieżką zapisu na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="2c77e-144">It should be a writable path on your local computer.</span></span> <span data-ttu-id="2c77e-145">Upewnij się, że .cer tooinclude na końcu hello.</span><span class="sxs-lookup"><span data-stu-id="2c77e-145">Make sure tooinclude .cer at hello end.</span></span>

    $Configuration.GeneratedCertificatePath = "[C:\Path\To\Certificate.cer]"

<span data-ttu-id="2c77e-146">toosee zostanie ustawiona, typ **$Configuration**.</span><span class="sxs-lookup"><span data-stu-id="2c77e-146">toosee what you set, type **$Configuration**.</span></span>

    > $Configuration

    Name                           Value
    ----                           -----
    GeneratedCertificatePath       C:\vnetcert.cer
    VnetSubscriptionId             efc239a4-88f9-2c5e-a9a1-3034c21ad496
    WebAppResourceGroup            vnetdemo-rg
    VnetResourceGroup              testase1-rg
    VnetName                       TestNetwork
    WebAppName                     vnetintdemoapp
    WebAppLocation                 centralus

<span data-ttu-id="2c77e-147">Witaj pozostałej części tej sekcji założono, że utworzony zgodnie z opisem właśnie zmiennej.</span><span class="sxs-lookup"><span data-stu-id="2c77e-147">hello rest of this section assumes that you have a variable created as just described.</span></span>

##### <a name="declare-hello-virtual-network-toohello-app"></a><span data-ttu-id="2c77e-148">Deklarowanie hello sieci wirtualnej toohello aplikacji</span><span class="sxs-lookup"><span data-stu-id="2c77e-148">Declare hello virtual network toohello app</span></span>
<span data-ttu-id="2c77e-149">Użyj hello następujące polecenie aplikacji hello tootell, że zostanie do niej używa tej określonej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2c77e-149">Use hello following command tootell hello app that it will be using this particular virtual network.</span></span> <span data-ttu-id="2c77e-150">Spowoduje to toogenerate aplikacji hello niezbędnych certyfikatów:</span><span class="sxs-lookup"><span data-stu-id="2c77e-150">This will cause hello app toogenerate necessary certificates:</span></span>

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -PropertyObject @{"VnetResourceId" = "/subscriptions/$($Configuration.VnetSubscriptionId)/resourceGroups/$($Configuration.VnetResourceGroup)/providers/Microsoft.ClassicNetwork/virtualNetworks/$($Configuration.VnetName)"} -Location $Configuration.WebAppLocation -ApiVersion 2015-07-01

<span data-ttu-id="2c77e-151">Jeśli to polecenie zakończy się powodzeniem, **$vnet** powinien mieć **właściwości** zmiennej w nim.</span><span class="sxs-lookup"><span data-stu-id="2c77e-151">If this command succeeds, **$vnet** should have a **Properties** variable in it.</span></span> <span data-ttu-id="2c77e-152">Witaj **właściwości** zmienna powinna zawierać zarówno certyfikat odcisk palca i hello danych certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="2c77e-152">hello **Properties** variable should contain both a certificate thumbprint and hello certificate data.</span></span>

##### <a name="upload-hello-web-app-certificate-toohello-virtual-network"></a><span data-ttu-id="2c77e-153">Przekaż hello web app certyfikatu toohello wirtualnej sieci</span><span class="sxs-lookup"><span data-stu-id="2c77e-153">Upload hello web app certificate toohello virtual network</span></span>
<span data-ttu-id="2c77e-154">Ręczne, jednorazowe krok jest wymagany dla każdej kombinacji sieci wirtualnej i subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="2c77e-154">A manual, one-time step is required for each subscription and virtual network combination.</span></span> <span data-ttu-id="2c77e-155">Oznacza to jeśli łączysz się z aplikacji w subskrypcji A tooVirtual sieci A, konieczne będzie toodo ten krok tylko raz, niezależnie od tego, jak wiele aplikacji można skonfigurować.</span><span class="sxs-lookup"><span data-stu-id="2c77e-155">That is, if you are connecting apps in Subscription A tooVirtual Network A, you will need toodo this step only once regardless of how many apps you configure.</span></span> <span data-ttu-id="2c77e-156">W przypadku dodawania nowej sieci wirtualnej tooanother aplikacji, musisz toodo ponownie.</span><span class="sxs-lookup"><span data-stu-id="2c77e-156">If you are adding a new app tooanother virtual network, you'll need toodo this again.</span></span> <span data-ttu-id="2c77e-157">Witaj przyczyną tego błędu jest zestaw certyfikatów jest generowany na poziomie subskrypcji w usłudze Azure App Service, czy zestaw hello jest generowany raz dla każdej sieci wirtualnej, którą aplikacji hello połączy się.</span><span class="sxs-lookup"><span data-stu-id="2c77e-157">hello reason for this is that a set of certificates is generated at a subscription level in Azure App Service, and hello set is generated once for each virtual network that hello apps will connect to.</span></span>

<span data-ttu-id="2c77e-158">Hello certyfikaty będą już zostały ustawione po wykonaniu tych kroków lub zintegrowana z hello sam sieci wirtualnej przy użyciu portalu hello.</span><span class="sxs-lookup"><span data-stu-id="2c77e-158">hello certificates will have already been set if you followed these steps or if you integrated with hello same virtual network by using hello portal.</span></span>

<span data-ttu-id="2c77e-159">pierwszym krokiem Hello jest plik cer hello toogenerate.</span><span class="sxs-lookup"><span data-stu-id="2c77e-159">hello first step is toogenerate hello .cer file.</span></span> <span data-ttu-id="2c77e-160">drugim krokiem Hello jest tooupload hello .cer pliku tooyour wirtualnej sieci.</span><span class="sxs-lookup"><span data-stu-id="2c77e-160">hello second step is tooupload hello .cer file tooyour virtual network.</span></span> <span data-ttu-id="2c77e-161">plik .cer hello toogenerate z wywołania interfejsu API hello w hello wcześniejszym kroku, uruchom następujące polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="2c77e-161">toogenerate hello .cer file from hello API call in hello earlier step, run hello following commands.</span></span>

    $certBytes = [System.Convert]::FromBase64String($vnet.Properties.certBlob)
    [System.IO.File]::WriteAllBytes("$($Configuration.GeneratedCertificatePath)", $certBytes)

<span data-ttu-id="2c77e-162">certyfikat Hello zostaną znalezione w lokalizacji hello który **$Configuration.GeneratedCertificatePath** określa.</span><span class="sxs-lookup"><span data-stu-id="2c77e-162">hello certificate will be found in hello location that **$Configuration.GeneratedCertificatePath** specifies.</span></span>

<span data-ttu-id="2c77e-163">tooupload hello certyfikat ręcznie, użyj hello [portalu Azure] [ azureportal] i **Przeglądaj sieć wirtualna (klasyczna)** > **połączeń sieci VPN**  >  **Punkt lokacja** > **zarządzanie certyfikatami**.</span><span class="sxs-lookup"><span data-stu-id="2c77e-163">tooupload hello certificate manually, use hello [Azure portal][azureportal] and **Browse Virtual Network (classic)** > **VPN connections** > **Point-to-site** > **Manage certificates**.</span></span> <span data-ttu-id="2c77e-164">W tym miejscu przekazanie certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="2c77e-164">From here, upload your certificate.</span></span>

##### <a name="get-hello-point-to-site-package"></a><span data-ttu-id="2c77e-165">Pobierz pakiet punkt lokacja hello</span><span class="sxs-lookup"><span data-stu-id="2c77e-165">Get hello point-to-site package</span></span>
<span data-ttu-id="2c77e-166">Hello następnego kroku w procesie konfigurowania połączenia z wirtualną siecią w aplikacji sieci web jest tooget hello punkt lokacja pakietu i podaj go tooyour aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="2c77e-166">hello next step in setting up a virtual network connection on a web app is tooget hello point-to-site package and provide it tooyour web app.</span></span>

<span data-ttu-id="2c77e-167">Zapisz hello następującego szablonu tooa pliku o nazwie GetNetworkPackageUri.json gdzieś na komputerze, na przykład C:\Azure\Templates\GetNetworkPackageUri.json.</span><span class="sxs-lookup"><span data-stu-id="2c77e-167">Save hello following template tooa file called GetNetworkPackageUri.json somewhere on your computer, for example, C:\Azure\Templates\GetNetworkPackageUri.json.</span></span>

    {
        "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "certData": {
                "type": "string"
            },
            "certThumbprint": {
                "type": "string"
            },
            "networkName": {
                "type": "string"
            }
        },
        "variables": {
            "legacyVnetName": "[concat('Group ', resourceGroup().name, ' ', parameters('networkName'))]"
            },
            "resources": [
            ],
        "outputs" : {
            "PackageUri" :
            {
            "value" : "[listPackage(resourceId('Microsoft.ClassicNetwork/virtualNetworks/gateways/clientRootCertificates', parameters('networkName'), 'primary', parameters('certThumbprint')), '2014-06-01').packageUri]", "type" : "string"
            }
        }
    }


<span data-ttu-id="2c77e-168">Ustaw parametry wejściowe:</span><span class="sxs-lookup"><span data-stu-id="2c77e-168">Set input parameters:</span></span>

    $parameters = @{"certData" = $vnet.Properties.certBlob ;
    certThumbprint = $vnet.Properties.certThumbprint ;
    "networkName" = $Configuration.VnetName }

<span data-ttu-id="2c77e-169">Wywołanie skryptu hello:</span><span class="sxs-lookup"><span data-stu-id="2c77e-169">Call hello script:</span></span>

    $output = New-AzureRmResourceGroupDeployment -Name unused -ResourceGroupName $Configuration.VnetResourceGroup -TemplateParameterObject $parameters -TemplateFile C:\PATH\TO\GetNetworkPackageUri.json


<span data-ttu-id="2c77e-170">Zmienna Hello **$output. Outputs.packageUri** teraz będzie zawierać toobe identyfikator URI pakietu hello podane tooyour aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="2c77e-170">hello variable **$output.Outputs.packageUri** will now contain hello package URI toobe given tooyour web app.</span></span>

##### <a name="upload-hello-point-to-site-package-tooyour-app"></a><span data-ttu-id="2c77e-171">Przekaż aplikację tooyour pakietu punkt lokacja hello</span><span class="sxs-lookup"><span data-stu-id="2c77e-171">Upload hello point-to-site package tooyour app</span></span>
<span data-ttu-id="2c77e-172">Ostatnim krokiem Hello jest aplikacja hello tooprovide z tym pakietem.</span><span class="sxs-lookup"><span data-stu-id="2c77e-172">hello final step is tooprovide hello app with this package.</span></span> <span data-ttu-id="2c77e-173">Po prostu uruchom następne polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="2c77e-173">Simply run hello next command:</span></span>

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)/primary" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-07-01 -PropertyObject @{"VnetName" = $Configuration.VnetName ; "VpnPackageUri" = $($output.Outputs.packageUri).Value } -Location $Configuration.WebAppLocation

<span data-ttu-id="2c77e-174">Jeśli wiadomość zostanie wyświetlona prośba tooconfirm, że są zastępowania istniejącego zasobu, upewnij się, że tooallow go.</span><span class="sxs-lookup"><span data-stu-id="2c77e-174">If a message asks you tooconfirm that you are overwriting an existing resource, make sure tooallow it.</span></span>

<span data-ttu-id="2c77e-175">Po pomyślnym zainicjowaniu tego polecenia, aplikacji powinno być teraz toohello połączonych sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2c77e-175">After this command succeeds, your app should now be connected toohello virtual network.</span></span> <span data-ttu-id="2c77e-176">Powodzenie tooconfirm Przejdź tooyour aplikacji konsoli, a następnie wpisz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="2c77e-176">tooconfirm success, go tooyour app console, and type hello following:</span></span>

    SET WEBSITE_

<span data-ttu-id="2c77e-177">Jeśli zmienna środowiskowa o nazwie WEBSITE_VNETNAME wartości, który odpowiada nazwie hello hello docelowy wirtualnej sieci pomyślnie wszystkie konfiguracje.</span><span class="sxs-lookup"><span data-stu-id="2c77e-177">If there is an environment variable called WEBSITE_VNETNAME that has a value that matches hello name of hello target virtual network, all configurations have succeeded.</span></span>

### <a name="update-classic-vnet-integration-information"></a><span data-ttu-id="2c77e-178">Aktualizowanie klasycznych informacji integracji sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="2c77e-178">Update classic VNet integration information</span></span>
<span data-ttu-id="2c77e-179">tooupdate lub ponownej synchronizacji danych, po prostu Powtórz kroki hello, których należy przestrzegać podczas tworzenia integracji hello w miejscu pierwszego hello.</span><span class="sxs-lookup"><span data-stu-id="2c77e-179">tooupdate or resync your information, simply repeat hello steps that you followed when you created hello integration in hello first place.</span></span> <span data-ttu-id="2c77e-180">Te kroki są:</span><span class="sxs-lookup"><span data-stu-id="2c77e-180">Those steps are:</span></span>

1. <span data-ttu-id="2c77e-181">Zdefiniuj informacje o konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="2c77e-181">Define your configuration information.</span></span>
2. <span data-ttu-id="2c77e-182">Deklarowanie hello sieci wirtualnej toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2c77e-182">Declare hello virtual network toohello app.</span></span>
3. <span data-ttu-id="2c77e-183">Pobierz pakiet punkt lokacja hello.</span><span class="sxs-lookup"><span data-stu-id="2c77e-183">Get hello point-to-site package.</span></span>
4. <span data-ttu-id="2c77e-184">Przekaż hello pakietu punkt lokacja tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2c77e-184">Upload hello point-to-site package tooyour app.</span></span>

### <a name="disconnect-your-app-from-a-classic-vnet"></a><span data-ttu-id="2c77e-185">Rozłączyć aplikacji klasycznej sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="2c77e-185">Disconnect your app from a classic VNet</span></span>
<span data-ttu-id="2c77e-186">Aplikacja hello toodisconnect, należy hello informacje o konfiguracji, która została ustawiona podczas integracji sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2c77e-186">toodisconnect hello app, you need hello configuration information that was set during virtual network integration.</span></span> <span data-ttu-id="2c77e-187">Za pomocą tych informacji, istnieje jeden toodisconnect polecenia aplikacji z sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2c77e-187">Using that information, there is then one command toodisconnect your app from your virtual network.</span></span>

    $vnet = Remove-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-07-01

## <a name="resource-manager-virtual-networks"></a><span data-ttu-id="2c77e-188">Sieci wirtualne usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2c77e-188">Resource Manager virtual networks</span></span>
<span data-ttu-id="2c77e-189">Sieci wirtualne usługi Resource Manager ma interfejsów API usługi Azure Resource Manager, który uprościć niektóre procesy w porównaniu z klasycznych sieci wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="2c77e-189">Resource Manager virtual networks have Azure Resource Manager APIs, which simplify some processes when compared with classic virtual networks.</span></span> <span data-ttu-id="2c77e-190">Mamy skrypt, który pomoże Ci się ukończyć powitalnych następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="2c77e-190">We have a script that will help you complete hello following tasks:</span></span>

* <span data-ttu-id="2c77e-191">Tworzenie sieci wirtualnej Resource Manager i integracji aplikacji z nim.</span><span class="sxs-lookup"><span data-stu-id="2c77e-191">Create a Resource Manager virtual network and integrate your app with it.</span></span>
* <span data-ttu-id="2c77e-192">Utwórz bramę, skonfiguruj połączenie punkt lokacja w istniejących sieci wirtualnych Menedżera zasobów, a następnie Integrowanie aplikacji z nim.</span><span class="sxs-lookup"><span data-stu-id="2c77e-192">Create a gateway, configure point-to-site connectivity in a preexisting Resource Manager virtual network, and then integrate your app with it.</span></span>
* <span data-ttu-id="2c77e-193">Integracja aplikacji z istniejących Menedżera zasobów sieci wirtualnej bramy i włączyć łączność punkt do lokacji.</span><span class="sxs-lookup"><span data-stu-id="2c77e-193">Integrate your app with a preexisting Resource Manager virtual network that has a gateway and point-to-site connectivity enabled.</span></span>
* <span data-ttu-id="2c77e-194">Aplikację można rozłączyć sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2c77e-194">Disconnect your app from your virtual network.</span></span>

### <a name="resource-manager-vnet-app-service-integration-script"></a><span data-ttu-id="2c77e-195">Skrypt integracji usługi aplikacji — Menedżer zasobów sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="2c77e-195">Resource Manager VNet App Service integration script</span></span>
<span data-ttu-id="2c77e-196">Skopiuj hello następujący skrypt i zapisać go w pliku tooa.</span><span class="sxs-lookup"><span data-stu-id="2c77e-196">Copy hello following script and save it tooa file.</span></span> <span data-ttu-id="2c77e-197">Jeśli nie chcesz toouse hello skryptu, możesz toolearn wolne od niego toosee jak rzeczy tooset się z siecią wirtualną Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="2c77e-197">If you don’t want toouse hello script, feel free toolearn from it toosee how tooset things up with a Resource Manager virtual network.</span></span>

    function ReadHostWithDefault($message, $default)
    {
        $result = Read-Host "$message [$default]"
        if($result -eq "")
        {
            $result = $default
        }
            return $result
        }

    function PromptCustom($title, $optionValues, $optionDescriptions)
    {
        Write-Host $title
        Write-Host
        $a = @()
        for($i = 0; $i -lt $optionValues.Length; $i++){
            Write-Host "$($i+1))" $optionDescriptions[$i]
        }
        Write-Host

        while($true)
        {
            Write-Host "Choose an option: "
            $option = Read-Host
            $option = $option -as [int]

            if($option -ge 1 -and $option -le $optionValues.Length)
            {
                return $optionValues[$option-1]
            }
        }
    }

    function PromptYesNo($title, $message, $default = 0)
    {
        $yes = New-Object System.Management.Automation.Host.ChoiceDescription "&Yes", ""
        $no = New-Object System.Management.Automation.Host.ChoiceDescription "&No", ""
        $options = [System.Management.Automation.Host.ChoiceDescription[]]($yes, $no)
        $result = $host.ui.PromptForChoice($title, $message, $options, $default)
        return $result
    }

    function CreateVnet($resourceGroupName, $vnetName, $vnetAddressSpace, $vnetGatewayAddressSpace, $location)
    {
        Write-Host "Creating a new VNET"
        $gatewaySubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix $vnetGatewayAddressSpace
        New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroupName -Location $location -AddressPrefix $vnetAddressSpace -Subnet $gatewaySubnet
    }

    function CreateVnetGateway($resourceGroupName, $vnetName, $vnetIpName, $location, $vnetIpConfigName, $vnetGatewayName, $certificateData, $vnetPointToSiteAddressSpace)
    {
        $vnet = Get-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroupName
        $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet

        Write-Host "Creating a public IP address for this VNET"
        $pip = New-AzureRmPublicIpAddress -Name $vnetIpName -ResourceGroupName $resourceGroupName -Location $location -AllocationMethod Dynamic
        $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $vnetIpConfigName -Subnet $subnet -PublicIpAddress $pip

        Write-Host "Adding a root certificate toothis VNET"
        $root = New-AzureRmVpnClientRootCertificate -Name "AppServiceCertificate.cer" -PublicCertData $certificateData

        Write-Host "Creating Azure VNET Gateway. This may take up tooan hour."
        New-AzureRmVirtualNetworkGateway -Name $vnetGatewayName -ResourceGroupName $resourceGroupName -Location $location -IpConfigurations $ipconf -GatewayType Vpn -VpnType RouteBased -EnableBgp $false -GatewaySku Basic -VpnClientAddressPool $vnetPointToSiteAddressSpace -VpnClientRootCertificates $root
    }

    function AddNewVnet($subscriptionId, $webAppResourceGroup, $webAppName)
    {
        Write-Host "Adding a new Vnet"
        Write-Host
        $vnetName = Read-Host "Specify a name for this Virtual Network"

        $vnetGatewayName="$($vnetName)-gateway"
        $vnetIpName="$($vnetName)-ip"
        $vnetIpConfigName="$($vnetName)-ipconf"

        # Virtual Network settings
        $vnetAddressSpace="10.0.0.0/8"
        $vnetGatewayAddressSpace="10.5.0.0/16"
        $vnetPointToSiteAddressSpace="172.16.0.0/16"

        $changeRequested = 0
        $resourceGroupName = $webAppResourceGroup

        while($changeRequested -eq 0)
        {
            Write-Host
            Write-Host "Currently, I will create a VNET with hello following settings:"
            Write-Host
            Write-Host "Virtual Network Name: $vnetName"
            Write-Host "Resource Group Name:  $resourceGroupName"
            Write-Host "Gateway Name: $vnetGatewayName"
            Write-Host "Vnet IP name: $vnetIpName"
            Write-Host "Vnet IP config name:  $vnetIpConfigName"
            Write-Host "Address Space:$vnetAddressSpace"
            Write-Host "Gateway Address Space:$vnetGatewayAddressSpace"
            Write-Host "Point-To-Site Address Space:  $vnetPointToSiteAddressSpace"
            Write-Host
            $changeRequested = PromptYesNo "" "Do you wish toochange these settings?" 1

            if($changeRequested -eq 0)
            {
                $vnetName = ReadHostWithDefault "Virtual Network Name" $vnetName
                $resourceGroupName = ReadHostWithDefault "Resource Group Name" $resourceGroupName
                $vnetGatewayName = ReadHostWithDefault "Vnet Gateway Name" $vnetGatewayName
                $vnetIpName = ReadHostWithDefault "Vnet IP name" $vnetIpName
                $vnetIpConfigName = ReadHostWithDefault "Vnet IP configuration name" $vnetIpConfigName
                $vnetAddressSpace = ReadHostWithDefault "Vnet Address Space" $vnetAddressSpace
                $vnetGatewayAddressSpace = ReadHostWithDefault "Vnet Gateway Address Space" $vnetGatewayAddressSpace
                $vnetPointToSiteAddressSpace = ReadHostWithDefault "Vnet Point-to-site Address Space" $vnetPointToSiteAddressSpace
            }
        }

        $ErrorActionPreference = "Stop";

        # We create hello virtual network and add it here. hello way this works is:
        # 1) Add hello VNET association toohello App. This allows hello App toogenerate certificates, etc. for hello VNET.
        # 2) Create hello VNET and VNET gateway, add hello certificates, create hello public IP, etc., required for hello gateway
        # 3) Get hello VPN package from hello gateway and pass it back toohello App.

        $webApp = Get-AzureRmResource -ResourceName $webAppName -ResourceType "Microsoft.Web/sites" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup
        $location = $webApp.Location

        Write-Host "Creating App association tooVNET"
        $propertiesObject = @{
         "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($resourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnetName)"
        }
        $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnetName)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup -Force

        CreateVnet $resourceGroupName $vnetName $vnetAddressSpace $vnetGatewayAddressSpace $location

        CreateVnetGateway $resourceGroupName $vnetName $vnetIpName $location $vnetIpConfigName $vnetGatewayName $virtualNetwork.Properties.CertBlob $vnetPointToSiteAddressSpace

        Write-Host "Retrieving VPN Package and supplying tooApp"
        $packageUri = Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName -VirtualNetworkGatewayName $vnetGatewayName -ProcessorArchitecture Amd64
        
        # $packageUri may contain literal double-quotes at hello start and hello end of hello URL
        if($packageUri.Length -gt 0 -and $packageUri.Substring(0, 1) -eq '"' -and $packageUri.Substring($packageUri.Length - 1, 1) -eq '"')
        {
            $packageUri = $packageUri.Substring(1, $packageUri.Length - 2)
        }

        # Put hello VPN client configuration package onto hello App
        $PropertiesObject = @{
        "vnetName" = $VirtualNetworkName; "vpnPackageUri" = $packageUri
        }

        New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnetName)/primary" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup -Force

        Write-Host "Finished!"
    }

    function AddExistingVnet($subscriptionId, $resourceGroupName, $webAppName)
    {
        $ErrorActionPreference = "Stop";

        # At this point, hello gateway should be able toobe joined tooan App, but may require some minor tweaking. We will declare toohello App now toouse this VNET
        Write-Host "Getting App information"
        $webApp = Get-AzureRmResource -ResourceName $webAppName -ResourceType "Microsoft.Web/sites" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $location = $webApp.Location

        $webAppConfig = Get-AzureRmResource -ResourceName "$($webAppName)/web" -ResourceType "Microsoft.Web/sites/config" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $currentVnet = $webAppConfig.Properties.VnetName
        if($currentVnet -ne $null -and $currentVnet -ne "")
        {
            Write-Host "Currently connected tooVNET $currentVnet"
        }

        # Display existing vnets
        $vnets = Get-AzureRmVirtualNetwork
        $vnetNames = @()
        foreach($vnet in $vnets)
        {
            $vnetNames += $vnet.Name
        }

        Write-Host
        $vnet = PromptCustom "Select a VNET toointegrate with" $vnets $vnetNames

        # We need toocheck if this VNET is able toobe joined tooa App, based on following criteria
            # If there is no gateway, we can create one.
            # If there is a gateway:
                # It must be of type Vpn
                # It must be of VpnType RouteBased
                # If it doesn't have hello right certificate, we will need tooadd it.
                # If it doesn't have a point-to-site range, we will need tooadd it.

        $gatewaySubnet = $vnet.Subnets | Where-Object { $_.Name -eq "GatewaySubnet" }

        if($gatewaySubnet -eq $null -or $gatewaySubnet.IpConfigurations -eq $null -or $gatewaySubnet.IpConfigurations.Count -eq 0)
        {
            $ErrorActionPreference = "Continue";
            # There is no gateway. We need toocreate one.
            Write-Host "This Virtual Network has no gateway. I will need toocreate one."

            $vnetName = $vnet.Name
            $vnetGatewayName="$($vnetName)-gateway"
            $vnetIpName="$($vnetName)-ip"
            $vnetIpConfigName="$($vnetName)-ipconf"

            # Virtual Network settings
            $vnetAddressSpace="10.0.0.0/8"
            $vnetGatewayAddressSpace="10.5.0.0/16"
            $vnetPointToSiteAddressSpace="172.16.0.0/16"

            $changeRequested = 0

            Write-Host "Your VNET is in hello address space $($vnet.AddressSpace.AddressPrefixes), with hello following Subnets:"
            foreach($subnet in $vnet.Subnets)
            {
                Write-Host "$($subnet.Name): $($subnet.AddressPrefix)"
            }

            $vnetGatewayAddressSpace = Read-Host "Please choose a GatewaySubnet address space"

            while($changeRequested -eq 0)
            {
                Write-Host
                Write-Host "Currently, I will create a VNET gateway with hello following settings:"
                Write-Host
                Write-Host "Virtual Network Name: $vnetName"
                Write-Host "Resource Group Name:  $($vnet.ResourceGroupName)"
                Write-Host "Gateway Name: $vnetGatewayName"
                Write-Host "Vnet IP name: $vnetIpName"
                Write-Host "Vnet IP config name:  $vnetIpConfigName"
                Write-Host "Address Space:$($vnet.AddressSpace.AddressPrefixes)"
                Write-Host "Gateway Address Space:$vnetGatewayAddressSpace"
                Write-Host "Point-To-Site Address Space:  $vnetPointToSiteAddressSpace"
                Write-Host
                $changeRequested = PromptYesNo "" "Do you wish toochange these settings?" 1

                if($changeRequested -eq 0)
                {
                    $vnetGatewayName = ReadHostWithDefault "Vnet Gateway Name" $vnetGatewayName
                    $vnetIpName = ReadHostWithDefault "Vnet IP name" $vnetIpName
                    $vnetIpConfigName = ReadHostWithDefault "Vnet IP configuration name" $vnetIpConfigName
                    $vnetGatewayAddressSpace = ReadHostWithDefault "Vnet Gateway Address Space" $vnetGatewayAddressSpace
                    $vnetPointToSiteAddressSpace = ReadHostWithDefault "Vnet Point-to-site Address Space" $vnetPointToSiteAddressSpace
                }
            }

            $ErrorActionPreference = "Stop";

            Write-Host "Creating App association tooVNET"
            $propertiesObject = @{
             "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($vnet.ResourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnetName)"
            }

            $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

            # If there is no gateway subnet, we need toocreate one.
            if($gatewaySubnet -eq $null)
            {
                $gatewaySubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix $vnetGatewayAddressSpace
                $vnet.Subnets.Add($gatewaySubnet);
                Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
            }

            CreateVnetGateway $vnet.ResourceGroupName $vnetName $vnetIpName $location $vnetIpConfigName $vnetGatewayName $virtualNetwork.Properties.CertBlob $vnetPointToSiteAddressSpace

            $gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $vnet.ResourceGroupName -Name $vnetGatewayName
        }
        else
        {
            $uriParts = $gatewaySubnet.IpConfigurations[0].Id.Split('/')
            $gatewayResourceGroup = $uriParts[4]
            $gatewayName = $uriParts[8]

            $gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $vnet.ResourceGroupName -Name $gatewayName

            # validate gateway types, etc.
            if($gateway.GatewayType -ne "Vpn")
            {
                Write-Error "This gateway is not of hello Vpn type. It cannot be joined tooan App."
                return
            }

            if($gateway.VpnType -ne "RouteBased")
            {
                Write-Error "This gateways Vpn type is not RouteBased. It cannot be joined tooan App."
                return
            }

            if($gateway.VpnClientConfiguration -eq $null -or $gateway.VpnClientConfiguration.VpnClientAddressPool -eq $null)
            {
                Write-Host "This gateway does not have a Point-to-site Address Range. Please specify one in CIDR notation, e.g. 10.0.0.0/8"
                $pointToSiteAddress = Read-Host "Point-To-Site Address Space"
                Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $gateway.Name -VpnClientAddressPool $pointToSiteAddress
            }

            Write-Host "Creating App association tooVNET"
            $propertiesObject = @{
             "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($vnet.ResourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnet.Name)"
            }

            $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

            # We need toocheck if hello certificate here exists in hello gateway.
            $certificates = $gateway.VpnClientConfiguration.VpnClientRootCertificates

            $certFound = $false
            foreach($certificate in $certificates)
            {
                if($certificate.PublicCertData -eq $virtualNetwork.Properties.CertBlob)
                {
                    $certFound = $true
                    break
                }
            }

            if(-not $certFound)
            {
                Write-Host "Adding certificate"
                Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName "AppServiceCertificate.cer" -PublicCertData $virtualNetwork.Properties.CertBlob -VirtualNetworkGatewayName $gateway.Name
            }
        }

        # Now finish joining by getting hello VPN package and giving it toohello App
        Write-Host "Retrieving VPN Package and supplying tooApp"
        $packageUri = Get-AzureRmVpnClientPackage -ResourceGroupName $vnet.ResourceGroupName -VirtualNetworkGatewayName $gateway.Name -ProcessorArchitecture Amd64
        
        # $packageUri may contain literal double-quotes at hello start and hello end of hello URL
        if($packageUri.Length -gt 0 -and $packageUri.Substring(0, 1) -eq '"' -and $packageUri.Substring($packageUri.Length - 1, 1) -eq '"')
        {
            $packageUri = $packageUri.Substring(1, $packageUri.Length - 2)
        }

        # Put hello VPN client configuration package onto hello App
        $PropertiesObject = @{
        "vnetName" = $vnet.Name; "vpnPackageUri" = $packageUri
        }

        New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)/primary" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

        Write-Host "Finished!"
    }

    function RemoveVnet($subscriptionId, $resourceGroupName, $webAppName)
    {
        $webAppConfig = Get-AzureRmResource -ResourceName "$($webAppName)/web" -ResourceType "Microsoft.Web/sites/config" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $currentVnet = $webAppConfig.Properties.VnetName
        if($currentVnet -ne $null -and $currentVnet -ne "")
        {
            Write-Host "Currently connected tooVNET $currentVnet"

            Remove-AzureRmResource -ResourceName "$($webAppName)/$($currentVnet)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        }
            else
        {
            Write-Host "Not connected tooa VNET."
        }
    }

    Write-Host "Please Login"
    Login-AzureRmAccount

    # Choose subscription. If there's only one we will choose automatically

    $subs = Get-AzureRmSubscription
    $subscriptionId = ""

    if($subs.Length -eq 0)
    {
        Write-Error "No subscriptions bound toothis account."
        return
    }

    if($subs.Length -eq 1)
    {
        $subscriptionId = $subs[0].SubscriptionId
    }
    else
    {
        $subscriptionChoices = @()
        $subscriptionValues = @()

        foreach($subscription in $subs){
        $subscriptionChoices += "$($subscription.SubscriptionName) ($($subscription.SubscriptionId))";
        $subscriptionValues += ($subscription.SubscriptionId);
        }

        $subscriptionId = PromptCustom "Choose a subscription" $subscriptionValues $subscriptionChoices
    }

    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    $resourceGroup = Read-Host "Please enter hello Resource Group of your App"

    $appName = Read-Host "Please enter hello Name of your App"

    $options = @("Add a NEW Virtual Network tooan App", "Add an EXISTING Virtual Network tooan App", "Remove a Virtual Network from an App");
    $optionValues = @(0, 1, 2)
    $option = PromptCustom "What do you want toodo?" $optionValues $options

    if($option -eq 0)
    {
        AddNewVnet $subscriptionId $resourceGroup $appName
    }
    if($option -eq 1)
    {
        AddExistingVnet $subscriptionId $resourceGroup $appName
    }
    if($option -eq 2)
    {
        RemoveVnet $subscriptionId $resourceGroup $appName
    }

<span data-ttu-id="2c77e-198">Zapisz kopię hello skryptu.</span><span class="sxs-lookup"><span data-stu-id="2c77e-198">Save a copy of hello script.</span></span> <span data-ttu-id="2c77e-199">W tym artykule jest nazywany V2VnetAllinOne.ps1, ale możesz użyć innej nazwy.</span><span class="sxs-lookup"><span data-stu-id="2c77e-199">In this article, it is called V2VnetAllinOne.ps1, but you can use another name.</span></span> <span data-ttu-id="2c77e-200">Nie ma żadnych argumentów w ramach tego skryptu.</span><span class="sxs-lookup"><span data-stu-id="2c77e-200">There are no arguments for this script.</span></span> <span data-ttu-id="2c77e-201">Wystarczy uruchomić go.</span><span class="sxs-lookup"><span data-stu-id="2c77e-201">You simply run it.</span></span> <span data-ttu-id="2c77e-202">Witaj po pierwsze hello skrypt będzie wykonywać jest monit toosign w.</span><span class="sxs-lookup"><span data-stu-id="2c77e-202">hello first thing hello script will do is prompt you toosign in.</span></span> <span data-ttu-id="2c77e-203">Po zalogowaniu, skrypt hello pobiera szczegółowe informacje o Twoim koncie i zwraca listę subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="2c77e-203">After you sign in, hello script gets details about your account and returns a list of subscriptions.</span></span> <span data-ttu-id="2c77e-204">Nie, licząc w żądania hello o podanie poświadczeń, wykonywanie skryptu początkowej hello wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="2c77e-204">Not counting hello request for your credentials, hello initial script execution looks like this:</span></span>

    PS C:\Users\ccompy\Documents\VNET> .\V2VnetAllInOne.ps1
    Please Login

    Environment           : AzureCloud
    Account               : ccompy@microsoft.com
    TenantId              : 722278f-fef1-499f-91ab-2323d011db47
    SubscriptionId        : af5358e1-acac-2c90-a9eb-722190abf47a
    CurrentStorageAccount :

    Choose a subscription

    1) <span data-ttu-id="2c77e-205">Wersja demonstracyjna dla subskrypcji (af5358e1-acac-2c90-a9eb-722190abf47a)</span><span class="sxs-lookup"><span data-stu-id="2c77e-205">Demo Subscription (af5358e1-acac-2c90-a9eb-722190abf47a)</span></span>
    2) <span data-ttu-id="2c77e-206">Test MS (a5350f55-dd5a-41ec-2ddb-ff7b911bb2ef)</span><span class="sxs-lookup"><span data-stu-id="2c77e-206">MS Test (a5350f55-dd5a-41ec-2ddb-ff7b911bb2ef)</span></span>
    3) <span data-ttu-id="2c77e-207">Pokaz purpurowa subskrypcji (2d4c99a4-57f9-4d5e-a0a1-0034c52db59d)</span><span class="sxs-lookup"><span data-stu-id="2c77e-207">Purple Demo Subscription (2d4c99a4-57f9-4d5e-a0a1-0034c52db59d)</span></span>

    <span data-ttu-id="2c77e-208">Wybierz jedną z opcji: 3</span><span class="sxs-lookup"><span data-stu-id="2c77e-208">Choose an option: 3</span></span>

    <span data-ttu-id="2c77e-209">Konto: ccompy@microsoft.com środowiska: subskrypcji AzureCloud: 2d4c99a4-57f9-4d5e-a0a1-0034c52db59d dzierżawy: 722278f-fef1-499f-91ab-2323d011db47</span><span class="sxs-lookup"><span data-stu-id="2c77e-209">Account      : ccompy@microsoft.com Environment  : AzureCloud Subscription : 2d4c99a4-57f9-4d5e-a0a1-0034c52db59d Tenant       : 722278f-fef1-499f-91ab-2323d011db47</span></span>

    <span data-ttu-id="2c77e-210">Podaj nazwę grupy zasobów aplikacji hello: zarządcy zasobów hcdemo wprowadź nazwę aplikacji hello: v2vnetpowershell czego użytkownik ma toodo?</span><span class="sxs-lookup"><span data-stu-id="2c77e-210">Please enter hello Resource Group of your App: hcdemo-rg Please enter hello Name of your App: v2vnetpowershell What do you want toodo?</span></span>

    1) <span data-ttu-id="2c77e-211">Dodaj nową sieć wirtualną tooan aplikacji</span><span class="sxs-lookup"><span data-stu-id="2c77e-211">Add a NEW Virtual Network tooan App</span></span>
    2) <span data-ttu-id="2c77e-212">Dodawanie istniejącej sieci wirtualnej tooan aplikacji</span><span class="sxs-lookup"><span data-stu-id="2c77e-212">Add an EXISTING Virtual Network tooan App</span></span>
    3) <span data-ttu-id="2c77e-213">Usuń sieć wirtualną z aplikacji</span><span class="sxs-lookup"><span data-stu-id="2c77e-213">Remove a Virtual Network from an App</span></span>

<span data-ttu-id="2c77e-214">Hello pozostałej części tej sekcji opisano każdy z tych trzech opcji.</span><span class="sxs-lookup"><span data-stu-id="2c77e-214">hello rest of this section explains each of those three options.</span></span>

### <a name="create-a-resource-manager-vnet-and-integrate-with-it"></a><span data-ttu-id="2c77e-215">Tworzenie sieci wirtualnej Resource Manager oraz integrują się z jej</span><span class="sxs-lookup"><span data-stu-id="2c77e-215">Create a Resource Manager VNet and integrate with it</span></span>
<span data-ttu-id="2c77e-216">Wybierz nową sieć wirtualną, że używa hello modelu wdrażania usługi Resource Manager i zintegrować ją z aplikacją, toocreate **1) Dodaj nową sieć wirtualną tooan aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="2c77e-216">toocreate a new virtual network that uses hello Resource Manager deployment model and integrate it with your app, select **1) Add a NEW Virtual Network tooan App**.</span></span> <span data-ttu-id="2c77e-217">To wyświetli monit o nazwę hello hello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2c77e-217">This will prompt you for hello name of hello virtual network.</span></span> <span data-ttu-id="2c77e-218">W przypadku mojej jak widać w hello następujące ustawienia, I użyto nazwy hello, v2pshell.</span><span class="sxs-lookup"><span data-stu-id="2c77e-218">In my case, as you can see in hello following settings, I used hello name, v2pshell.</span></span>

<span data-ttu-id="2c77e-219">skrypt Hello szczegółowo hello hello sieci wirtualnej, która jest tworzona.</span><span class="sxs-lookup"><span data-stu-id="2c77e-219">hello script gives hello details about hello virtual network that's being created.</span></span> <span data-ttu-id="2c77e-220">Jeśli ma, można zmienić wartości hello.</span><span class="sxs-lookup"><span data-stu-id="2c77e-220">If I want, I can change any of hello values.</span></span> <span data-ttu-id="2c77e-221">Podczas wykonywania tego przykładu I utworzyć sieć wirtualną mającą hello następujące ustawienia:</span><span class="sxs-lookup"><span data-stu-id="2c77e-221">In this example execution, I created a virtual network that has hello following settings:</span></span>

    Virtual Network Name:         v2pshell
    Resource Group Name:          hcdemo-rg
    Gateway Name:                 v2pshell-gateway
    Vnet IP name:                 v2pshell-ip
    Vnet IP config name:          v2pshell-ipconf
    Address Space:                10.0.0.0/8
    Gateway Address Space:        10.5.0.0/16
    Point-To-Site Address Space:  172.16.0.0/12

    Do you wish toochange these settings?
    [Y] Yes  [N] No  [?] Help (default is "N"):

<span data-ttu-id="2c77e-222">Toochange hello wartości, należy wpisać **Y** i wprowadź zmiany hello.</span><span class="sxs-lookup"><span data-stu-id="2c77e-222">If you want toochange any of hello values, type **Y** and make hello changes.</span></span> <span data-ttu-id="2c77e-223">W przypadku modyfikowania ustawień sieci wirtualnej hello wpisz **N** lub po prostu naciśnij klawisz Enter po wyświetleniu monitu o zmianę ustawień hello.</span><span class="sxs-lookup"><span data-stu-id="2c77e-223">When you are happy with hello virtual network settings, type **N** or simply press Enter when prompted about changing hello settings.</span></span> <span data-ttu-id="2c77e-224">Z tego miejsca na aż do zakończenia skryptu hello informuje o niektórych jakie "być wykonanie do momentu rozpoczęcia bramy sieci wirtualnej hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="2c77e-224">From there on until completion, hello script will tell you some of what it' i's doing until it starts toocreate hello virtual network gateway.</span></span> <span data-ttu-id="2c77e-225">Ten krok może potrwać godzinę tooan.</span><span class="sxs-lookup"><span data-stu-id="2c77e-225">That step can take up tooan hour.</span></span> <span data-ttu-id="2c77e-226">Nie jest wskaźnik postępu, nie w tej fazie, ale skryptu hello poinformuje użytkownika po utworzeniu bramy hello.</span><span class="sxs-lookup"><span data-stu-id="2c77e-226">There is no progress indicator during this phase, but hello script will let you know when hello gateway has been created.</span></span>

<span data-ttu-id="2c77e-227">Po zakończeniu działania skryptu hello jest wyświetlany tekst **Zakończono**.</span><span class="sxs-lookup"><span data-stu-id="2c77e-227">When hello script finishes, it will say **Finished**.</span></span> <span data-ttu-id="2c77e-228">W tym momencie będzie mieć Menedżera zasobów sieci wirtualnej o nazwie hello i wybrane ustawienia.</span><span class="sxs-lookup"><span data-stu-id="2c77e-228">At this point, you will have a Resource Manager virtual network that has hello name and settings that you selected.</span></span> <span data-ttu-id="2c77e-229">Ta nowa sieć wirtualna będzie również być zintegrowane z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2c77e-229">This new virtual network will also be integrated with your app.</span></span>

### <a name="integrate-your-app-with-a-preexisting-resource-manager-vnet"></a><span data-ttu-id="2c77e-230">Integracja aplikacji z istniejących zasobów Menedżera sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="2c77e-230">Integrate your app with a preexisting Resource Manager VNet</span></span>
<span data-ttu-id="2c77e-231">Gdy w przypadku integracji z istniejących sieci wirtualnej, jeśli podasz Menedżera zasobów sieci wirtualnej, która nie ma bramy lub połączenie punkt lokacja, skrypt hello skonfiguruje który.</span><span class="sxs-lookup"><span data-stu-id="2c77e-231">When you're integrating with a preexisting virtual network, if you provide a Resource Manager virtual network that doesn’t have a gateway or point-to-site connectivity, hello script will set that up.</span></span> <span data-ttu-id="2c77e-232">Jeśli hello sieci Wirtualnej ma już tych problemów, konfigurowanie, skrypt hello przechodzi toohello prostej aplikacji integracji.</span><span class="sxs-lookup"><span data-stu-id="2c77e-232">If hello VNET already has those things set up, hello script goes straight toohello app integration.</span></span> <span data-ttu-id="2c77e-233">toostart ten proces, po prostu zaznacz **2) Dodaj tooan istniejącej sieci wirtualnej aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="2c77e-233">toostart this process, simply select **2) Add an EXISTING Virtual Network tooan App**.</span></span>

<span data-ttu-id="2c77e-234">Ta opcja działa tylko wtedy, gdy w przypadku istniejących sieci wirtualnych Menedżera zasobów, w hello tej samej subskrypcji co aplikacja.</span><span class="sxs-lookup"><span data-stu-id="2c77e-234">This option works only if you have a preexisting Resource Manager virtual network that is in hello same subscription as your app.</span></span> <span data-ttu-id="2c77e-235">Po wybraniu opcji hello, zostanie wyświetlona lista sieci wirtualne usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2c77e-235">After you select hello option, you will be presented with a list of your Resource Manager virtual networks.</span></span>   

    Select a VNET toointegrate with

    1) <span data-ttu-id="2c77e-236">v2demonetwork</span><span class="sxs-lookup"><span data-stu-id="2c77e-236">v2demonetwork</span></span>
    2) <span data-ttu-id="2c77e-237">v2pshell</span><span class="sxs-lookup"><span data-stu-id="2c77e-237">v2pshell</span></span>
    3) <span data-ttu-id="2c77e-238">v2vnetintdemo</span><span class="sxs-lookup"><span data-stu-id="2c77e-238">v2vnetintdemo</span></span>
    4) <span data-ttu-id="2c77e-239">v2asenetwork</span><span class="sxs-lookup"><span data-stu-id="2c77e-239">v2asenetwork</span></span>
    5) <span data-ttu-id="2c77e-240">v2pshell2</span><span class="sxs-lookup"><span data-stu-id="2c77e-240">v2pshell2</span></span>

    <span data-ttu-id="2c77e-241">Wybierz jedną z opcji: 5</span><span class="sxs-lookup"><span data-stu-id="2c77e-241">Choose an option: 5</span></span>

<span data-ttu-id="2c77e-242">Po prostu wybierz hello sieci wirtualnej, który ma toointegrate z.</span><span class="sxs-lookup"><span data-stu-id="2c77e-242">Simply select hello virtual network that you want toointegrate with.</span></span> <span data-ttu-id="2c77e-243">Jeśli masz już bramy, która ma włączone połączenie punkt lokacja, skrypt powitania po prostu integracji aplikacji z sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2c77e-243">If you already have a gateway that has point-to-site connectivity enabled, hello script will simply integrate your app with your virtual network.</span></span> <span data-ttu-id="2c77e-244">Jeśli nie ma bramę, konieczne będzie podsieci bramy hello toospecify.</span><span class="sxs-lookup"><span data-stu-id="2c77e-244">If you do not have a gateway, you will need toospecify hello gateway subnet.</span></span> <span data-ttu-id="2c77e-245">Podsieć bramy musi być w przestrzeni adresowej sieci wirtualnej, a nie może być w innej podsieci.</span><span class="sxs-lookup"><span data-stu-id="2c77e-245">Your gateway subnet must be in your virtual network address space, and it cannot be in any other subnet.</span></span> <span data-ttu-id="2c77e-246">Jeśli masz bez bramy sieci wirtualnej, a następnie uruchom ten krok, rzeczy wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="2c77e-246">If you have a virtual network without a gateway and run this step, things look like this:</span></span>

    This Virtual Network has no gateway. I will need toocreate one.
    Your VNET is in hello address space 172.16.0.0/16, with hello following Subnets:
    default: 172.16.0.0/24
    Please choose a GatewaySubnet address space: 172.16.1.0/26

<span data-ttu-id="2c77e-247">W tym przykładzie można utworzyć bramy sieci wirtualnej, która ma hello następujące ustawienia:</span><span class="sxs-lookup"><span data-stu-id="2c77e-247">In this example, I created a virtual network gateway that has hello following settings:</span></span>

    Virtual Network Name:         v2pshell2
    Resource Group Name:          vnetdemo-rg
    Gateway Name:                 v2pshell2-gateway
    Vnet IP name:                 v2pshell2-ip
    Vnet IP config name:          v2pshell2-ipconf
    Address Space:                172.16.0.0/16
    Gateway Address Space:        172.16.1.0/26
    Point-To-Site Address Space:  172.16.0.0/12

    Do you wish toochange these settings?
    [Y] Yes  [N] No  [?] Help (default is "N"):
    Creating App association tooVNET

<span data-ttu-id="2c77e-248">Jeśli chcesz toochange dowolne z tych ustawień, możesz to zrobić.</span><span class="sxs-lookup"><span data-stu-id="2c77e-248">If you want toochange any of those settings, you can do so.</span></span> <span data-ttu-id="2c77e-249">W przeciwnym razie naciśnij klawisz Enter, a skrypt hello Tworzenie bramy i Dołącz sieć wirtualna tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2c77e-249">Otherwise, press Enter and hello script will create your gateway and attach your app tooyour virtual network.</span></span> <span data-ttu-id="2c77e-250">Czas utworzenia bramy Hello jest nadal godzinę, mimo że, upewnij się, że należy pamiętać, że.</span><span class="sxs-lookup"><span data-stu-id="2c77e-250">hello gateway creation time is still an hour, though, so make sure you keep that in mind.</span></span> <span data-ttu-id="2c77e-251">Gdy wszystko jest gotowe, będzie napisane skryptu hello **Zakończono**.</span><span class="sxs-lookup"><span data-stu-id="2c77e-251">When everything is finished, hello script will say **Finished**.</span></span>

### <a name="disconnect-your-app-from-a-resource-manager-vnet"></a><span data-ttu-id="2c77e-252">Rozłączyć aplikacji z Menedżera zasobów sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="2c77e-252">Disconnect your app from a Resource Manager VNet</span></span>
<span data-ttu-id="2c77e-253">Odłączanie aplikacji od sieci wirtualnej nie wyłączyć hello bramy lub Wyłącz połączenie punkt lokacja.</span><span class="sxs-lookup"><span data-stu-id="2c77e-253">Disconnecting your app from your virtual network does not take down hello gateway or disable point-to-site connectivity.</span></span> <span data-ttu-id="2c77e-254">Być może używasz go do czegoś innego.</span><span class="sxs-lookup"><span data-stu-id="2c77e-254">You might, after all, be using it for something else.</span></span> <span data-ttu-id="2c77e-255">Go również nie odłączenie go od innych aplikacji innych niż hello co podane.</span><span class="sxs-lookup"><span data-stu-id="2c77e-255">It also does not disconnect it from any other apps other than hello one you provided.</span></span> <span data-ttu-id="2c77e-256">tooperform tę akcję, wybierz opcję **3) Usuń sieć wirtualną z aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="2c77e-256">tooperform this action, select **3) Remove a Virtual Network from an App**.</span></span> <span data-ttu-id="2c77e-257">Jeśli tak zrobisz, zostanie wyświetlony podobny do następującego:</span><span class="sxs-lookup"><span data-stu-id="2c77e-257">When you do so, you will see something like this:</span></span>

    Currently connected tooVNET v2pshell

    Confirm
    Are you sure you want toodelete hello following resource:
    /subscriptions/edcc99a4-b7f9-4b5e-a9a1-3034c51db496/resourceGroups/hcdemo-rg/providers/Microsoft.Web/sites/v2vnetpowers
    hell/virtualNetworkConnections/v2pshell
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):

<span data-ttu-id="2c77e-258">Mimo że skryptu hello mówi delete, nie powoduje usunięcia hello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2c77e-258">Although hello script says delete, it does not delete hello virtual network.</span></span> <span data-ttu-id="2c77e-259">Jest on tylko usuwanie hello integracji.</span><span class="sxs-lookup"><span data-stu-id="2c77e-259">It’s just removing hello integration.</span></span> <span data-ttu-id="2c77e-260">Po upewnieniu się, że jest to czego chcesz toodo, polecenie hello jest bardzo szybko przetwarzane i pozwalają określić **True** po jej zakończeniu.</span><span class="sxs-lookup"><span data-stu-id="2c77e-260">After you confirm that this is what you want toodo, hello command is processed quite quickly and tells you **True** when it is done.</span></span>

<!--Links-->
[createvpngateway]: http://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/
[azureportal]: http://portal.azure.com
