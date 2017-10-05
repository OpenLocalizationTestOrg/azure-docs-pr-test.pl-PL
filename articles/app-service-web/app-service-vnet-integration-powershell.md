---
title: "Łączenie aplikacji z siecią wirtualną za pomocą programu PowerShell"
description: "Instrukcje dotyczące sposobu nawiązać połączenie i pracować z sieci wirtualnych za pomocą programu PowerShell"
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
ms.openlocfilehash: 6fae6a6c162fa326161d2b47a259b3151d6e3dd0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-app-to-your-virtual-network-by-using-powershell"></a><span data-ttu-id="6aa1f-103">Łączenie aplikacji z siecią wirtualną za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="6aa1f-103">Connect your app to your virtual network by using PowerShell</span></span>
## <a name="overview"></a><span data-ttu-id="6aa1f-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="6aa1f-104">Overview</span></span>
<span data-ttu-id="6aa1f-105">W usłudze Azure App Service można połączyć aplikacji (sieć web, mobilnych lub interfejsu API) do sieci wirtualnej platformy Azure (VNet) w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-105">In Azure App Service, you can connect your app (web, mobile, or API) to an Azure virtual network (VNet) in your subscription.</span></span> <span data-ttu-id="6aa1f-106">Ta funkcja jest nazywana integracji sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-106">This feature is called VNet Integration.</span></span> <span data-ttu-id="6aa1f-107">Funkcja integracji sieci wirtualnej nie należy mylić z funkcji środowiska usługi aplikacji, która pozwala na uruchamianie wystąpienia usługi Azure App Service w Twojej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-107">The VNet Integration feature should not be confused with the App Service Environment feature, which allows you to run an instance of Azure App Service in your virtual network.</span></span>

<span data-ttu-id="6aa1f-108">Funkcja integracji sieci wirtualnej ma interfejs użytkownika (UI) w nowego portalu, który służy do integracji z sieciami wirtualnymi, które zostały wdrożone przy użyciu klasycznego modelu wdrażania lub modelu wdrażania usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-108">The VNet Integration feature has a user interface (UI) in the new portal that you can use to integrate with virtual networks that are deployed by using either the classic deployment model or the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="6aa1f-109">Jeśli chcesz dowiedzieć się więcej na temat funkcji, zobacz [integracji aplikacji z sieci wirtualnej platformy Azure](web-sites-integrate-with-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="6aa1f-109">If you want to learn more about the feature, see [Integrate your app with an Azure virtual network](web-sites-integrate-with-vnet.md).</span></span>

<span data-ttu-id="6aa1f-110">W tym artykule jest nie o sposobie używania interfejsu użytkownika, ale raczej o włączaniu integracji przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-110">This article is not about how to use the UI but rather about how to enable integration by using PowerShell.</span></span> <span data-ttu-id="6aa1f-111">Ponieważ polecenia dla każdego modelu wdrażania są różne, w tym artykule ma sekcji do każdego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-111">Because the commands for each deployment model are different, this article has a section for each deployment model.</span></span>  

<span data-ttu-id="6aa1f-112">Przed kontynuowaniem w tym artykule upewnij się, że masz:</span><span class="sxs-lookup"><span data-stu-id="6aa1f-112">Before you continue with this article, ensure that you have:</span></span>

* <span data-ttu-id="6aa1f-113">R zainstalowany zestaw SDK usługi Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-113">The latest Azure PowerShell SDK installed.</span></span> <span data-ttu-id="6aa1f-114">Można go zainstalować za pomocą Instalatora platformy sieci Web.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-114">You can install this with the Web Platform Installer.</span></span>
* <span data-ttu-id="6aa1f-115">Aplikacja w usłudze Azure App Service w Standard lub Premium jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-115">An app in Azure App Service running in a Standard or Premium SKU.</span></span>

## <a name="classic-virtual-networks"></a><span data-ttu-id="6aa1f-116">Klasycznych sieci wirtualnych</span><span class="sxs-lookup"><span data-stu-id="6aa1f-116">Classic virtual networks</span></span>
<span data-ttu-id="6aa1f-117">W tej sekcji opisano trzy zadania dla sieci wirtualnych, które używają klasycznym modelu wdrażania:</span><span class="sxs-lookup"><span data-stu-id="6aa1f-117">This section explains three tasks for virtual networks that use the classic deployment model:</span></span>

1. <span data-ttu-id="6aa1f-118">Łączenie aplikacji z istniejących sieci wirtualnej, i jest konfigurowane połączenie punkt lokacja z bramą.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-118">Connect your app to a preexisting virtual network that has a gateway and is configured for point-to-site connectivity.</span></span>
2. <span data-ttu-id="6aa1f-119">Aktualizowanie informacji o integracji sieci wirtualnej dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-119">Update your virtual network integration information for your app.</span></span>
3. <span data-ttu-id="6aa1f-120">Aplikację można rozłączyć sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-120">Disconnect your app from your virtual network.</span></span>

### <a name="connect-an-app-to-a-classic-vnet"></a><span data-ttu-id="6aa1f-121">Łączenie aplikacji klasycznej sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="6aa1f-121">Connect an app to a classic VNet</span></span>
<span data-ttu-id="6aa1f-122">Aby połączyć aplikację z sieci wirtualnej, wykonaj następujące trzy kroki:</span><span class="sxs-lookup"><span data-stu-id="6aa1f-122">To connect an app to a virtual network, follow these three steps:</span></span>

1. <span data-ttu-id="6aa1f-123">W aplikacji sieci web zadeklarować, że zostanie do niej dołączanie do określonej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-123">Declare to the web app that it will be joining a particular virtual network.</span></span> <span data-ttu-id="6aa1f-124">Aplikacja wygeneruje certyfikat, który będzie podane do sieci wirtualnej dla połączenia punkt lokacja.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-124">The app will generate a certificate that will be given to the virtual network for point-to-site connectivity.</span></span>
2. <span data-ttu-id="6aa1f-125">Przekaż certyfikat aplikacji sieci web do sieci wirtualnej, a następnie pobrać identyfikator URI pakietu sieci VPN punkt lokacja.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-125">Upload the web app certificate to the virtual network, and then retrieve the point-to-site VPN package URI.</span></span>
3. <span data-ttu-id="6aa1f-126">Zaktualizuj połączenie wirtualnej sieci aplikacji sieci web z pakietem punkt lokacja identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-126">Update the web app's virtual network connection with the point-to-site package URI.</span></span>

<span data-ttu-id="6aa1f-127">Pierwszy i trzeci kroki są w pełni skryptowe, a drugi etap wymaga jednorazowe, ręczna Akcja za pośrednictwem portalu lub dostępu do wykonywania **PUT** lub **poprawka** akcje na wirtualnej sieci zasobów Azure Punkt końcowy menedżera.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-127">The first and third steps are fully scriptable, but the second step requires a one-time, manual action through the portal, or access to perform **PUT** or **PATCH** actions on the virtual network Azure Resource Manager endpoint.</span></span> <span data-ttu-id="6aa1f-128">Skontaktuj się z pomocą techniczną platformy Azure ma to włączone.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-128">Contact Azure Support to have this enabled.</span></span> <span data-ttu-id="6aa1f-129">Przed rozpoczęciem upewnij się, czy masz klasycznego siecią wirtualną, która ma już włączone połączenie punkt lokacja i wdrożone bramę.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-129">Before you start, make sure that you have a classic virtual network that has point-to-site connectivity already enabled and a deployed gateway.</span></span> <span data-ttu-id="6aa1f-130">Aby utworzyć bramę i Włącz połączenie punkt lokacja, należy korzystać z portalu zgodnie z opisem w [Tworzenie bramy sieci VPN][createvpngateway].</span><span class="sxs-lookup"><span data-stu-id="6aa1f-130">To create the gateway and enable point-to-site connectivity, you need to use the portal as described at [Creating a VPN gateway][createvpngateway].</span></span>

<span data-ttu-id="6aa1f-131">Klasyczne sieci wirtualnej musi być w tej samej subskrypcji co planu usługi aplikacji zawierający aplikację, która jest integrowany z.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-131">The classic virtual network needs to be in the same subscription as your App Service plan that holds the app that you are integrating with.</span></span>

##### <a name="set-up-azure-powershell-sdk"></a><span data-ttu-id="6aa1f-132">Konfigurowanie programu Azure PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="6aa1f-132">Set up Azure PowerShell SDK</span></span>
<span data-ttu-id="6aa1f-133">Otwórz okno programu PowerShell i skonfigurować konto platformy Azure i subskrypcji przy użyciu:</span><span class="sxs-lookup"><span data-stu-id="6aa1f-133">Open a PowerShell window and set up your Azure account and subscription by using:</span></span>

    Login-AzureRmAccount

<span data-ttu-id="6aa1f-134">To polecenie spowoduje otwarcie wiersza, aby uzyskać poświadczenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-134">That command will open a prompt to get your Azure credentials.</span></span> <span data-ttu-id="6aa1f-135">Po zalogowaniu w użyj jednej z następujących poleceń, aby wybrać subskrypcję, która ma być używany.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-135">After you sign in, use either of the following commands to select the subscription that you want to use.</span></span> <span data-ttu-id="6aa1f-136">Upewnij się, że używasz subskrypcji, że sieć wirtualna i plan usługi aplikacji znajdują się w.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-136">Make sure that you are using the subscription that your virtual network and App Service plan are in.</span></span>

    Select-AzureRmSubscription –SubscriptionName [WebAppSubscriptionName]

<span data-ttu-id="6aa1f-137">lub</span><span class="sxs-lookup"><span data-stu-id="6aa1f-137">or</span></span>

    Select-AzureRmSubscription –SubscriptionId [WebAppSubscriptionId]

##### <a name="variables-used-in-this-article"></a><span data-ttu-id="6aa1f-138">Zmienne używane w tym artykule</span><span class="sxs-lookup"><span data-stu-id="6aa1f-138">Variables used in this article</span></span>
<span data-ttu-id="6aa1f-139">Aby uprościć poleceń, możemy ustawi **$Configuration** PowerShell zmienna o określonej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-139">To simplify commands, we will set a **$Configuration** PowerShell variable with the specific configuration.</span></span>

<span data-ttu-id="6aa1f-140">Ustaw zmienną w następujący sposób w programie PowerShell z następującymi parametrami:</span><span class="sxs-lookup"><span data-stu-id="6aa1f-140">Set a variable as follows in PowerShell with the following parameters:</span></span>

    $Configuration = @{}
    $Configuration.WebAppResourceGroup = "[Your web app resource group]"
    $Configuration.WebAppName = "[Your web app name]"
    $Configuration.VnetSubscriptionId = "[Your vnet subscription id]"
    $Configuration.VnetResourceGroup = "[Your vnet resource group]"
    $Configuration.VnetName = "[Your vnet name]"

<span data-ttu-id="6aa1f-141">Lokalizacja aplikacji powinna być lokalizacji bez spacji.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-141">The app location should be the location without any spaces.</span></span> <span data-ttu-id="6aa1f-142">Zachodnie stany USA jest na przykład westus.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-142">For example, West US is westus.</span></span>

    $Configuration.WebAppLocation = "[Your web app Location]"

<span data-ttu-id="6aa1f-143">Następny element jest, którym zapisany certyfikat.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-143">The next item is where the certificate should be written.</span></span> <span data-ttu-id="6aa1f-144">Należy ścieżką zapisu na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-144">It should be a writable path on your local computer.</span></span> <span data-ttu-id="6aa1f-145">Upewnij się uwzględnić .cer na końcu.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-145">Make sure to include .cer at the end.</span></span>

    $Configuration.GeneratedCertificatePath = "[C:\Path\To\Certificate.cer]"

<span data-ttu-id="6aa1f-146">Aby zobaczyć, jakie ustawiasz, wpisz **$Configuration**.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-146">To see what you set, type **$Configuration**.</span></span>

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

<span data-ttu-id="6aa1f-147">Pozostałej części tej sekcji założono, że utworzony zgodnie z opisem właśnie zmiennej.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-147">The rest of this section assumes that you have a variable created as just described.</span></span>

##### <a name="declare-the-virtual-network-to-the-app"></a><span data-ttu-id="6aa1f-148">Deklarowanie sieci wirtualnej do aplikacji</span><span class="sxs-lookup"><span data-stu-id="6aa1f-148">Declare the virtual network to the app</span></span>
<span data-ttu-id="6aa1f-149">Użyj następującego polecenia aplikacji stwierdzić, że zostanie do niej używa tej określonej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-149">Use the following command to tell the app that it will be using this particular virtual network.</span></span> <span data-ttu-id="6aa1f-150">Spowoduje to aplikacji do wygenerowania niezbędnych certyfikatów:</span><span class="sxs-lookup"><span data-stu-id="6aa1f-150">This will cause the app to generate necessary certificates:</span></span>

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -PropertyObject @{"VnetResourceId" = "/subscriptions/$($Configuration.VnetSubscriptionId)/resourceGroups/$($Configuration.VnetResourceGroup)/providers/Microsoft.ClassicNetwork/virtualNetworks/$($Configuration.VnetName)"} -Location $Configuration.WebAppLocation -ApiVersion 2015-07-01

<span data-ttu-id="6aa1f-151">Jeśli to polecenie zakończy się powodzeniem, **$vnet** powinien mieć **właściwości** zmiennej w nim.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-151">If this command succeeds, **$vnet** should have a **Properties** variable in it.</span></span> <span data-ttu-id="6aa1f-152">**Właściwości** zmienna powinna zawierać zarówno odcisku palca certyfikatu, jak i dane certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-152">The **Properties** variable should contain both a certificate thumbprint and the certificate data.</span></span>

##### <a name="upload-the-web-app-certificate-to-the-virtual-network"></a><span data-ttu-id="6aa1f-153">Przekaż certyfikat aplikacji sieci web do sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="6aa1f-153">Upload the web app certificate to the virtual network</span></span>
<span data-ttu-id="6aa1f-154">Ręczne, jednorazowe krok jest wymagany dla każdej kombinacji sieci wirtualnej i subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-154">A manual, one-time step is required for each subscription and virtual network combination.</span></span> <span data-ttu-id="6aa1f-155">Oznacza to, że łączysz aplikacji w ramach subskrypcji A A sieci wirtualnej, należy wykonać ten krok tylko wtedy, gdy niezależnie od tego, jak wiele aplikacji można skonfigurować.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-155">That is, if you are connecting apps in Subscription A to Virtual Network A, you will need to do this step only once regardless of how many apps you configure.</span></span> <span data-ttu-id="6aa1f-156">Jeśli dodajesz nową aplikację do innej sieci wirtualnej, należy ponownie.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-156">If you are adding a new app to another virtual network, you'll need to do this again.</span></span> <span data-ttu-id="6aa1f-157">Przyczyną tego jest zestaw certyfikatów jest generowany na poziomie subskrypcji w usłudze Azure App Service, czy zestaw jest generowany raz dla każdej sieci wirtualnej, które aplikacje będą się łączyć.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-157">The reason for this is that a set of certificates is generated at a subscription level in Azure App Service, and the set is generated once for each virtual network that the apps will connect to.</span></span>

<span data-ttu-id="6aa1f-158">Certyfikaty zostaną już zostały ustawione po wykonaniu tych kroków lub zintegrowana z tej samej sieci wirtualnej przy użyciu portalu.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-158">The certificates will have already been set if you followed these steps or if you integrated with the same virtual network by using the portal.</span></span>

<span data-ttu-id="6aa1f-159">Pierwszym krokiem jest generowanie pliku .cer.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-159">The first step is to generate the .cer file.</span></span> <span data-ttu-id="6aa1f-160">Drugim krokiem jest można przekazać pliku .cer do sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-160">The second step is to upload the .cer file to your virtual network.</span></span> <span data-ttu-id="6aa1f-161">Aby wygenerować plik .cer w wywołaniu interfejsu API w poprzednim kroku, uruchom następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-161">To generate the .cer file from the API call in the earlier step, run the following commands.</span></span>

    $certBytes = [System.Convert]::FromBase64String($vnet.Properties.certBlob)
    [System.IO.File]::WriteAllBytes("$($Configuration.GeneratedCertificatePath)", $certBytes)

<span data-ttu-id="6aa1f-162">Będzie można znaleźć certyfikatu w lokalizacji który **$Configuration.GeneratedCertificatePath** określa.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-162">The certificate will be found in the location that **$Configuration.GeneratedCertificatePath** specifies.</span></span>

<span data-ttu-id="6aa1f-163">Aby przekazać certyfikat ręcznie, należy użyć [portalu Azure] [ azureportal] i **Przeglądaj sieć wirtualna (klasyczna)** > **połączeń sieci VPN**  >  **Punkt lokacja** > **zarządzanie certyfikatami**.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-163">To upload the certificate manually, use the [Azure portal][azureportal] and **Browse Virtual Network (classic)** > **VPN connections** > **Point-to-site** > **Manage certificates**.</span></span> <span data-ttu-id="6aa1f-164">W tym miejscu przekazanie certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-164">From here, upload your certificate.</span></span>

##### <a name="get-the-point-to-site-package"></a><span data-ttu-id="6aa1f-165">Pobierz pakiet punkt lokacja</span><span class="sxs-lookup"><span data-stu-id="6aa1f-165">Get the point-to-site package</span></span>
<span data-ttu-id="6aa1f-166">Następnym krokiem w procesie konfigurowania połączenia z wirtualną siecią w aplikacji sieci web jest pobrania pakietu punkt lokacja i przekazywanie ich do aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-166">The next step in setting up a virtual network connection on a web app is to get the point-to-site package and provide it to your web app.</span></span>

<span data-ttu-id="6aa1f-167">Zapisz następującego szablonu w pliku o nazwie GetNetworkPackageUri.json gdzieś na komputerze, na przykład C:\Azure\Templates\GetNetworkPackageUri.json.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-167">Save the following template to a file called GetNetworkPackageUri.json somewhere on your computer, for example, C:\Azure\Templates\GetNetworkPackageUri.json.</span></span>

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


<span data-ttu-id="6aa1f-168">Ustaw parametry wejściowe:</span><span class="sxs-lookup"><span data-stu-id="6aa1f-168">Set input parameters:</span></span>

    $parameters = @{"certData" = $vnet.Properties.certBlob ;
    certThumbprint = $vnet.Properties.certThumbprint ;
    "networkName" = $Configuration.VnetName }

<span data-ttu-id="6aa1f-169">Wywołanie skryptu:</span><span class="sxs-lookup"><span data-stu-id="6aa1f-169">Call the script:</span></span>

    $output = New-AzureRmResourceGroupDeployment -Name unused -ResourceGroupName $Configuration.VnetResourceGroup -TemplateParameterObject $parameters -TemplateFile C:\PATH\TO\GetNetworkPackageUri.json


<span data-ttu-id="6aa1f-170">Zmienna **$output. Outputs.packageUri** teraz będzie zawierać pakiet identyfikator URI do aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-170">The variable **$output.Outputs.packageUri** will now contain the package URI to be given to your web app.</span></span>

##### <a name="upload-the-point-to-site-package-to-your-app"></a><span data-ttu-id="6aa1f-171">Przekaż pakiet punkt lokacja, do aplikacji</span><span class="sxs-lookup"><span data-stu-id="6aa1f-171">Upload the point-to-site package to your app</span></span>
<span data-ttu-id="6aa1f-172">Ostatnim krokiem jest zapewnienie aplikacji z tym pakietem.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-172">The final step is to provide the app with this package.</span></span> <span data-ttu-id="6aa1f-173">Po prostu uruchom następne polecenie:</span><span class="sxs-lookup"><span data-stu-id="6aa1f-173">Simply run the next command:</span></span>

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)/primary" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-07-01 -PropertyObject @{"VnetName" = $Configuration.VnetName ; "VpnPackageUri" = $($output.Outputs.packageUri).Value } -Location $Configuration.WebAppLocation

<span data-ttu-id="6aa1f-174">Jeśli wiadomość prośba o potwierdzenie, że są zastępowania istniejącego zasobu, upewnij się umożliwić jego.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-174">If a message asks you to confirm that you are overwriting an existing resource, make sure to allow it.</span></span>

<span data-ttu-id="6aa1f-175">Po pomyślnym zainicjowaniu tego polecenia, aplikacji powinno być teraz połączone siecią wirtualną.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-175">After this command succeeds, your app should now be connected to the virtual network.</span></span> <span data-ttu-id="6aa1f-176">Aby sprawdzić, powodzenia, przejdź do aplikacji konsoli, a następnie wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="6aa1f-176">To confirm success, go to your app console, and type the following:</span></span>

    SET WEBSITE_

<span data-ttu-id="6aa1f-177">W przypadku zmienną środowiskową o nazwie WEBSITE_VNETNAME, który ma wartość, która jest zgodna z nazwą docelowej sieci wirtualnej, wszystkie konfiguracje mają zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-177">If there is an environment variable called WEBSITE_VNETNAME that has a value that matches the name of the target virtual network, all configurations have succeeded.</span></span>

### <a name="update-classic-vnet-integration-information"></a><span data-ttu-id="6aa1f-178">Aktualizowanie klasycznych informacji integracji sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="6aa1f-178">Update classic VNet integration information</span></span>
<span data-ttu-id="6aa1f-179">Aby zaktualizować lub ponownej synchronizacji danych, po prostu Powtórz kroki, które należy przestrzegać podczas integracji został utworzony w pierwszej kolejności.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-179">To update or resync your information, simply repeat the steps that you followed when you created the integration in the first place.</span></span> <span data-ttu-id="6aa1f-180">Te kroki są:</span><span class="sxs-lookup"><span data-stu-id="6aa1f-180">Those steps are:</span></span>

1. <span data-ttu-id="6aa1f-181">Zdefiniuj informacje o konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-181">Define your configuration information.</span></span>
2. <span data-ttu-id="6aa1f-182">Deklarowanie sieci wirtualnej do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-182">Declare the virtual network to the app.</span></span>
3. <span data-ttu-id="6aa1f-183">Pobierz pakiet punkt lokacja.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-183">Get the point-to-site package.</span></span>
4. <span data-ttu-id="6aa1f-184">Przekaż pakiet punkt lokacja, do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-184">Upload the point-to-site package to your app.</span></span>

### <a name="disconnect-your-app-from-a-classic-vnet"></a><span data-ttu-id="6aa1f-185">Rozłączyć aplikacji klasycznej sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="6aa1f-185">Disconnect your app from a classic VNet</span></span>
<span data-ttu-id="6aa1f-186">Aby odłączyć aplikacji, potrzebne są informacje o konfiguracji, która została ustawiona podczas integracji sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-186">To disconnect the app, you need the configuration information that was set during virtual network integration.</span></span> <span data-ttu-id="6aa1f-187">Za pomocą tych informacji, jest następnie jednego polecenia można rozłączyć aplikacji z sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-187">Using that information, there is then one command to disconnect your app from your virtual network.</span></span>

    $vnet = Remove-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-07-01

## <a name="resource-manager-virtual-networks"></a><span data-ttu-id="6aa1f-188">Sieci wirtualne usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6aa1f-188">Resource Manager virtual networks</span></span>
<span data-ttu-id="6aa1f-189">Sieci wirtualne usługi Resource Manager ma interfejsów API usługi Azure Resource Manager, który uprościć niektóre procesy w porównaniu z klasycznych sieci wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-189">Resource Manager virtual networks have Azure Resource Manager APIs, which simplify some processes when compared with classic virtual networks.</span></span> <span data-ttu-id="6aa1f-190">Mamy skrypt, który pomoże wykonać następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="6aa1f-190">We have a script that will help you complete the following tasks:</span></span>

* <span data-ttu-id="6aa1f-191">Tworzenie sieci wirtualnej Resource Manager i integracji aplikacji z nim.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-191">Create a Resource Manager virtual network and integrate your app with it.</span></span>
* <span data-ttu-id="6aa1f-192">Utwórz bramę, skonfiguruj połączenie punkt lokacja w istniejących sieci wirtualnych Menedżera zasobów, a następnie Integrowanie aplikacji z nim.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-192">Create a gateway, configure point-to-site connectivity in a preexisting Resource Manager virtual network, and then integrate your app with it.</span></span>
* <span data-ttu-id="6aa1f-193">Integracja aplikacji z istniejących Menedżera zasobów sieci wirtualnej bramy i włączyć łączność punkt do lokacji.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-193">Integrate your app with a preexisting Resource Manager virtual network that has a gateway and point-to-site connectivity enabled.</span></span>
* <span data-ttu-id="6aa1f-194">Aplikację można rozłączyć sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-194">Disconnect your app from your virtual network.</span></span>

### <a name="resource-manager-vnet-app-service-integration-script"></a><span data-ttu-id="6aa1f-195">Skrypt integracji usługi aplikacji — Menedżer zasobów sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="6aa1f-195">Resource Manager VNet App Service integration script</span></span>
<span data-ttu-id="6aa1f-196">Skopiuj poniższy skrypt i zapisz go w pliku.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-196">Copy the following script and save it to a file.</span></span> <span data-ttu-id="6aa1f-197">Jeśli nie chcesz użyć skryptu, możesz także dowiedzieć się od niego na temat sposobu konfigurowania elementów sieci wirtualnych Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-197">If you don’t want to use the script, feel free to learn from it to see how to set things up with a Resource Manager virtual network.</span></span>

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

        Write-Host "Adding a root certificate to this VNET"
        $root = New-AzureRmVpnClientRootCertificate -Name "AppServiceCertificate.cer" -PublicCertData $certificateData

        Write-Host "Creating Azure VNET Gateway. This may take up to an hour."
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
            Write-Host "Currently, I will create a VNET with the following settings:"
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
            $changeRequested = PromptYesNo "" "Do you wish to change these settings?" 1

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

        # We create the virtual network and add it here. The way this works is:
        # 1) Add the VNET association to the App. This allows the App to generate certificates, etc. for the VNET.
        # 2) Create the VNET and VNET gateway, add the certificates, create the public IP, etc., required for the gateway
        # 3) Get the VPN package from the gateway and pass it back to the App.

        $webApp = Get-AzureRmResource -ResourceName $webAppName -ResourceType "Microsoft.Web/sites" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup
        $location = $webApp.Location

        Write-Host "Creating App association to VNET"
        $propertiesObject = @{
         "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($resourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnetName)"
        }
        $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnetName)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup -Force

        CreateVnet $resourceGroupName $vnetName $vnetAddressSpace $vnetGatewayAddressSpace $location

        CreateVnetGateway $resourceGroupName $vnetName $vnetIpName $location $vnetIpConfigName $vnetGatewayName $virtualNetwork.Properties.CertBlob $vnetPointToSiteAddressSpace

        Write-Host "Retrieving VPN Package and supplying to App"
        $packageUri = Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName -VirtualNetworkGatewayName $vnetGatewayName -ProcessorArchitecture Amd64
        
        # $packageUri may contain literal double-quotes at the start and the end of the URL
        if($packageUri.Length -gt 0 -and $packageUri.Substring(0, 1) -eq '"' -and $packageUri.Substring($packageUri.Length - 1, 1) -eq '"')
        {
            $packageUri = $packageUri.Substring(1, $packageUri.Length - 2)
        }

        # Put the VPN client configuration package onto the App
        $PropertiesObject = @{
        "vnetName" = $VirtualNetworkName; "vpnPackageUri" = $packageUri
        }

        New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnetName)/primary" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup -Force

        Write-Host "Finished!"
    }

    function AddExistingVnet($subscriptionId, $resourceGroupName, $webAppName)
    {
        $ErrorActionPreference = "Stop";

        # At this point, the gateway should be able to be joined to an App, but may require some minor tweaking. We will declare to the App now to use this VNET
        Write-Host "Getting App information"
        $webApp = Get-AzureRmResource -ResourceName $webAppName -ResourceType "Microsoft.Web/sites" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $location = $webApp.Location

        $webAppConfig = Get-AzureRmResource -ResourceName "$($webAppName)/web" -ResourceType "Microsoft.Web/sites/config" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $currentVnet = $webAppConfig.Properties.VnetName
        if($currentVnet -ne $null -and $currentVnet -ne "")
        {
            Write-Host "Currently connected to VNET $currentVnet"
        }

        # Display existing vnets
        $vnets = Get-AzureRmVirtualNetwork
        $vnetNames = @()
        foreach($vnet in $vnets)
        {
            $vnetNames += $vnet.Name
        }

        Write-Host
        $vnet = PromptCustom "Select a VNET to integrate with" $vnets $vnetNames

        # We need to check if this VNET is able to be joined to a App, based on following criteria
            # If there is no gateway, we can create one.
            # If there is a gateway:
                # It must be of type Vpn
                # It must be of VpnType RouteBased
                # If it doesn't have the right certificate, we will need to add it.
                # If it doesn't have a point-to-site range, we will need to add it.

        $gatewaySubnet = $vnet.Subnets | Where-Object { $_.Name -eq "GatewaySubnet" }

        if($gatewaySubnet -eq $null -or $gatewaySubnet.IpConfigurations -eq $null -or $gatewaySubnet.IpConfigurations.Count -eq 0)
        {
            $ErrorActionPreference = "Continue";
            # There is no gateway. We need to create one.
            Write-Host "This Virtual Network has no gateway. I will need to create one."

            $vnetName = $vnet.Name
            $vnetGatewayName="$($vnetName)-gateway"
            $vnetIpName="$($vnetName)-ip"
            $vnetIpConfigName="$($vnetName)-ipconf"

            # Virtual Network settings
            $vnetAddressSpace="10.0.0.0/8"
            $vnetGatewayAddressSpace="10.5.0.0/16"
            $vnetPointToSiteAddressSpace="172.16.0.0/16"

            $changeRequested = 0

            Write-Host "Your VNET is in the address space $($vnet.AddressSpace.AddressPrefixes), with the following Subnets:"
            foreach($subnet in $vnet.Subnets)
            {
                Write-Host "$($subnet.Name): $($subnet.AddressPrefix)"
            }

            $vnetGatewayAddressSpace = Read-Host "Please choose a GatewaySubnet address space"

            while($changeRequested -eq 0)
            {
                Write-Host
                Write-Host "Currently, I will create a VNET gateway with the following settings:"
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
                $changeRequested = PromptYesNo "" "Do you wish to change these settings?" 1

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

            Write-Host "Creating App association to VNET"
            $propertiesObject = @{
             "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($vnet.ResourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnetName)"
            }

            $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

            # If there is no gateway subnet, we need to create one.
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
                Write-Error "This gateway is not of the Vpn type. It cannot be joined to an App."
                return
            }

            if($gateway.VpnType -ne "RouteBased")
            {
                Write-Error "This gateways Vpn type is not RouteBased. It cannot be joined to an App."
                return
            }

            if($gateway.VpnClientConfiguration -eq $null -or $gateway.VpnClientConfiguration.VpnClientAddressPool -eq $null)
            {
                Write-Host "This gateway does not have a Point-to-site Address Range. Please specify one in CIDR notation, e.g. 10.0.0.0/8"
                $pointToSiteAddress = Read-Host "Point-To-Site Address Space"
                Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $gateway.Name -VpnClientAddressPool $pointToSiteAddress
            }

            Write-Host "Creating App association to VNET"
            $propertiesObject = @{
             "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($vnet.ResourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnet.Name)"
            }

            $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

            # We need to check if the certificate here exists in the gateway.
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

        # Now finish joining by getting the VPN package and giving it to the App
        Write-Host "Retrieving VPN Package and supplying to App"
        $packageUri = Get-AzureRmVpnClientPackage -ResourceGroupName $vnet.ResourceGroupName -VirtualNetworkGatewayName $gateway.Name -ProcessorArchitecture Amd64
        
        # $packageUri may contain literal double-quotes at the start and the end of the URL
        if($packageUri.Length -gt 0 -and $packageUri.Substring(0, 1) -eq '"' -and $packageUri.Substring($packageUri.Length - 1, 1) -eq '"')
        {
            $packageUri = $packageUri.Substring(1, $packageUri.Length - 2)
        }

        # Put the VPN client configuration package onto the App
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
            Write-Host "Currently connected to VNET $currentVnet"

            Remove-AzureRmResource -ResourceName "$($webAppName)/$($currentVnet)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        }
            else
        {
            Write-Host "Not connected to a VNET."
        }
    }

    Write-Host "Please Login"
    Login-AzureRmAccount

    # Choose subscription. If there's only one we will choose automatically

    $subs = Get-AzureRmSubscription
    $subscriptionId = ""

    if($subs.Length -eq 0)
    {
        Write-Error "No subscriptions bound to this account."
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

    $resourceGroup = Read-Host "Please enter the Resource Group of your App"

    $appName = Read-Host "Please enter the Name of your App"

    $options = @("Add a NEW Virtual Network to an App", "Add an EXISTING Virtual Network to an App", "Remove a Virtual Network from an App");
    $optionValues = @(0, 1, 2)
    $option = PromptCustom "What do you want to do?" $optionValues $options

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

<span data-ttu-id="6aa1f-198">Zapisz kopię skryptu.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-198">Save a copy of the script.</span></span> <span data-ttu-id="6aa1f-199">W tym artykule jest nazywany V2VnetAllinOne.ps1, ale możesz użyć innej nazwy.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-199">In this article, it is called V2VnetAllinOne.ps1, but you can use another name.</span></span> <span data-ttu-id="6aa1f-200">Nie ma żadnych argumentów w ramach tego skryptu.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-200">There are no arguments for this script.</span></span> <span data-ttu-id="6aa1f-201">Wystarczy uruchomić go.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-201">You simply run it.</span></span> <span data-ttu-id="6aa1f-202">W pierwszej kolejności skrypt będzie wykonywać jest wyświetlenie monitu zaloguj się.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-202">The first thing the script will do is prompt you to sign in.</span></span> <span data-ttu-id="6aa1f-203">Po zalogowaniu, skrypt pobiera szczegółowe informacje o Twoim koncie i zwraca listę subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-203">After you sign in, the script gets details about your account and returns a list of subscriptions.</span></span> <span data-ttu-id="6aa1f-204">Nie, licząc w żądanie o podanie poświadczeń, wykonywanie skryptu początkowej wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="6aa1f-204">Not counting the request for your credentials, the initial script execution looks like this:</span></span>

    PS C:\Users\ccompy\Documents\VNET> .\V2VnetAllInOne.ps1
    Please Login

    Environment           : AzureCloud
    Account               : ccompy@microsoft.com
    TenantId              : 722278f-fef1-499f-91ab-2323d011db47
    SubscriptionId        : af5358e1-acac-2c90-a9eb-722190abf47a
    CurrentStorageAccount :

    Choose a subscription

    1) <span data-ttu-id="6aa1f-205">Wersja demonstracyjna dla subskrypcji (af5358e1-acac-2c90-a9eb-722190abf47a)</span><span class="sxs-lookup"><span data-stu-id="6aa1f-205">Demo Subscription (af5358e1-acac-2c90-a9eb-722190abf47a)</span></span>
    2) <span data-ttu-id="6aa1f-206">Test MS (a5350f55-dd5a-41ec-2ddb-ff7b911bb2ef)</span><span class="sxs-lookup"><span data-stu-id="6aa1f-206">MS Test (a5350f55-dd5a-41ec-2ddb-ff7b911bb2ef)</span></span>
    3) <span data-ttu-id="6aa1f-207">Pokaz purpurowa subskrypcji (2d4c99a4-57f9-4d5e-a0a1-0034c52db59d)</span><span class="sxs-lookup"><span data-stu-id="6aa1f-207">Purple Demo Subscription (2d4c99a4-57f9-4d5e-a0a1-0034c52db59d)</span></span>

    <span data-ttu-id="6aa1f-208">Wybierz jedną z opcji: 3</span><span class="sxs-lookup"><span data-stu-id="6aa1f-208">Choose an option: 3</span></span>

    <span data-ttu-id="6aa1f-209">Konto: ccompy@microsoft.com środowiska: subskrypcji AzureCloud: 2d4c99a4-57f9-4d5e-a0a1-0034c52db59d dzierżawy: 722278f-fef1-499f-91ab-2323d011db47</span><span class="sxs-lookup"><span data-stu-id="6aa1f-209">Account      : ccompy@microsoft.com Environment  : AzureCloud Subscription : 2d4c99a4-57f9-4d5e-a0a1-0034c52db59d Tenant       : 722278f-fef1-499f-91ab-2323d011db47</span></span>

    <span data-ttu-id="6aa1f-210">Wprowadź grupę zasobów aplikacji: zarządcy zasobów hcdemo wprowadź nazwę aplikacji: v2vnetpowershell co chcesz zrobić?</span><span class="sxs-lookup"><span data-stu-id="6aa1f-210">Please enter the Resource Group of your App: hcdemo-rg Please enter the Name of your App: v2vnetpowershell What do you want to do?</span></span>

    1) <span data-ttu-id="6aa1f-211">Dodawanie nowej sieci wirtualnej do aplikacji</span><span class="sxs-lookup"><span data-stu-id="6aa1f-211">Add a NEW Virtual Network to an App</span></span>
    2) <span data-ttu-id="6aa1f-212">Dodaj istniejące sieci wirtualnej do aplikacji</span><span class="sxs-lookup"><span data-stu-id="6aa1f-212">Add an EXISTING Virtual Network to an App</span></span>
    3) <span data-ttu-id="6aa1f-213">Usuń sieć wirtualną z aplikacji</span><span class="sxs-lookup"><span data-stu-id="6aa1f-213">Remove a Virtual Network from an App</span></span>

<span data-ttu-id="6aa1f-214">Pozostałej części tej sekcji opisano każdy z tych trzech opcji.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-214">The rest of this section explains each of those three options.</span></span>

### <a name="create-a-resource-manager-vnet-and-integrate-with-it"></a><span data-ttu-id="6aa1f-215">Tworzenie sieci wirtualnej Resource Manager oraz integrują się z jej</span><span class="sxs-lookup"><span data-stu-id="6aa1f-215">Create a Resource Manager VNet and integrate with it</span></span>
<span data-ttu-id="6aa1f-216">Aby utworzyć nową sieć wirtualną, która używa modelu wdrażania usługi Resource Manager i zintegrować ją z aplikacji, wybierz **1) Dodawanie nowej sieci wirtualnej do aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-216">To create a new virtual network that uses the Resource Manager deployment model and integrate it with your app, select **1) Add a NEW Virtual Network to an App**.</span></span> <span data-ttu-id="6aa1f-217">To spowoduje wyświetlenie monitu o nazwę sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-217">This will prompt you for the name of the virtual network.</span></span> <span data-ttu-id="6aa1f-218">W przypadku mojej jak widać w następujących ustawieniach I użyta nazwa v2pshell.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-218">In my case, as you can see in the following settings, I used the name, v2pshell.</span></span>

<span data-ttu-id="6aa1f-219">Skrypt podaje szczegółowe informacje o sieci wirtualnej, która jest tworzona.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-219">The script gives the details about the virtual network that's being created.</span></span> <span data-ttu-id="6aa1f-220">Jeśli ma, można zmienić wartości.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-220">If I want, I can change any of the values.</span></span> <span data-ttu-id="6aa1f-221">Podczas wykonywania tego przykładu I utworzyć sieci wirtualnej, który ma następujące ustawienia:</span><span class="sxs-lookup"><span data-stu-id="6aa1f-221">In this example execution, I created a virtual network that has the following settings:</span></span>

    Virtual Network Name:         v2pshell
    Resource Group Name:          hcdemo-rg
    Gateway Name:                 v2pshell-gateway
    Vnet IP name:                 v2pshell-ip
    Vnet IP config name:          v2pshell-ipconf
    Address Space:                10.0.0.0/8
    Gateway Address Space:        10.5.0.0/16
    Point-To-Site Address Space:  172.16.0.0/12

    Do you wish to change these settings?
    [Y] Yes  [N] No  [?] Help (default is "N"):

<span data-ttu-id="6aa1f-222">Jeśli chcesz zmienić wartości, wpisz **Y** i wprowadź zmiany.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-222">If you want to change any of the values, type **Y** and make the changes.</span></span> <span data-ttu-id="6aa1f-223">W przypadku modyfikowania ustawień sieci wirtualnej wpisz **N** lub po prostu naciśnij klawisz Enter po wyświetleniu monitu o zmianę ustawień.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-223">When you are happy with the virtual network settings, type **N** or simply press Enter when prompted about changing the settings.</span></span> <span data-ttu-id="6aa1f-224">Z tego miejsca na aż do zakończenia skryptu informuje o niektórych jakie "być czynności do chwili jego uruchomienia utworzyć bramę sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-224">From there on until completion, the script will tell you some of what it' i's doing until it starts to create the virtual network gateway.</span></span> <span data-ttu-id="6aa1f-225">Ten krok może potrwać do godziny.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-225">That step can take up to an hour.</span></span> <span data-ttu-id="6aa1f-226">Nie jest wskaźnik postępu, nie w tej fazie, ale skrypt poinformuje użytkownika po utworzeniu bramy.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-226">There is no progress indicator during this phase, but the script will let you know when the gateway has been created.</span></span>

<span data-ttu-id="6aa1f-227">Po zakończeniu działania skryptu jest wyświetlany tekst **Zakończono**.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-227">When the script finishes, it will say **Finished**.</span></span> <span data-ttu-id="6aa1f-228">W tym momencie będzie mieć Resource Manager sieć wirtualna, która ma nazwę i ustawienia, które zostały wybrane.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-228">At this point, you will have a Resource Manager virtual network that has the name and settings that you selected.</span></span> <span data-ttu-id="6aa1f-229">Ta nowa sieć wirtualna będzie również być zintegrowane z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-229">This new virtual network will also be integrated with your app.</span></span>

### <a name="integrate-your-app-with-a-preexisting-resource-manager-vnet"></a><span data-ttu-id="6aa1f-230">Integracja aplikacji z istniejących zasobów Menedżera sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="6aa1f-230">Integrate your app with a preexisting Resource Manager VNet</span></span>
<span data-ttu-id="6aa1f-231">Gdy w przypadku integracji z istniejących sieci wirtualnej, jeśli podasz Menedżera zasobów sieci wirtualnej, która nie ma bramy lub połączenie punkt lokacja, skrypt zostanie skonfigurowany który.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-231">When you're integrating with a preexisting virtual network, if you provide a Resource Manager virtual network that doesn’t have a gateway or point-to-site connectivity, the script will set that up.</span></span> <span data-ttu-id="6aa1f-232">Jeśli sieć wirtualna ma już tych problemów, konfigurowanie, skrypt trafia bezpośrednio do integracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-232">If the VNET already has those things set up, the script goes straight to the app integration.</span></span> <span data-ttu-id="6aa1f-233">Aby uruchomić ten proces, po prostu zaznacz **2) Dodaj istniejącej sieci wirtualnej do aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-233">To start this process, simply select **2) Add an EXISTING Virtual Network to an App**.</span></span>

<span data-ttu-id="6aa1f-234">Ta opcja działa tylko wtedy, gdy masz istniejących Resource Manager siecią wirtualną, która znajduje się w tej samej subskrypcji co aplikacja.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-234">This option works only if you have a preexisting Resource Manager virtual network that is in the same subscription as your app.</span></span> <span data-ttu-id="6aa1f-235">Po wybraniu opcji, zostanie wyświetlona lista sieci wirtualne usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-235">After you select the option, you will be presented with a list of your Resource Manager virtual networks.</span></span>   

    Select a VNET to integrate with

    1) <span data-ttu-id="6aa1f-236">v2demonetwork</span><span class="sxs-lookup"><span data-stu-id="6aa1f-236">v2demonetwork</span></span>
    2) <span data-ttu-id="6aa1f-237">v2pshell</span><span class="sxs-lookup"><span data-stu-id="6aa1f-237">v2pshell</span></span>
    3) <span data-ttu-id="6aa1f-238">v2vnetintdemo</span><span class="sxs-lookup"><span data-stu-id="6aa1f-238">v2vnetintdemo</span></span>
    4) <span data-ttu-id="6aa1f-239">v2asenetwork</span><span class="sxs-lookup"><span data-stu-id="6aa1f-239">v2asenetwork</span></span>
    5) <span data-ttu-id="6aa1f-240">v2pshell2</span><span class="sxs-lookup"><span data-stu-id="6aa1f-240">v2pshell2</span></span>

    <span data-ttu-id="6aa1f-241">Wybierz jedną z opcji: 5</span><span class="sxs-lookup"><span data-stu-id="6aa1f-241">Choose an option: 5</span></span>

<span data-ttu-id="6aa1f-242">Po prostu wybierz sieć wirtualną, który chcesz zintegrować z.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-242">Simply select the virtual network that you want to integrate with.</span></span> <span data-ttu-id="6aa1f-243">Jeśli masz już bramy, która ma włączone połączenie punkt lokacja, skrypt po prostu integracji aplikacji z sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-243">If you already have a gateway that has point-to-site connectivity enabled, the script will simply integrate your app with your virtual network.</span></span> <span data-ttu-id="6aa1f-244">Jeśli nie masz bramy, należy określić podsieć bramy.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-244">If you do not have a gateway, you will need to specify the gateway subnet.</span></span> <span data-ttu-id="6aa1f-245">Podsieć bramy musi być w przestrzeni adresowej sieci wirtualnej, a nie może być w innej podsieci.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-245">Your gateway subnet must be in your virtual network address space, and it cannot be in any other subnet.</span></span> <span data-ttu-id="6aa1f-246">Jeśli masz bez bramy sieci wirtualnej, a następnie uruchom ten krok, rzeczy wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="6aa1f-246">If you have a virtual network without a gateway and run this step, things look like this:</span></span>

    This Virtual Network has no gateway. I will need to create one.
    Your VNET is in the address space 172.16.0.0/16, with the following Subnets:
    default: 172.16.0.0/24
    Please choose a GatewaySubnet address space: 172.16.1.0/26

<span data-ttu-id="6aa1f-247">W tym przykładzie można utworzyć bramy sieci wirtualnej, która ma następujące ustawienia:</span><span class="sxs-lookup"><span data-stu-id="6aa1f-247">In this example, I created a virtual network gateway that has the following settings:</span></span>

    Virtual Network Name:         v2pshell2
    Resource Group Name:          vnetdemo-rg
    Gateway Name:                 v2pshell2-gateway
    Vnet IP name:                 v2pshell2-ip
    Vnet IP config name:          v2pshell2-ipconf
    Address Space:                172.16.0.0/16
    Gateway Address Space:        172.16.1.0/26
    Point-To-Site Address Space:  172.16.0.0/12

    Do you wish to change these settings?
    [Y] Yes  [N] No  [?] Help (default is "N"):
    Creating App association to VNET

<span data-ttu-id="6aa1f-248">Jeśli chcesz zmienić te ustawienia, możesz to zrobić.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-248">If you want to change any of those settings, you can do so.</span></span> <span data-ttu-id="6aa1f-249">W przeciwnym razie naciśnij klawisz Enter, a skrypt utworzy bramy i dołączyć aplikacji do sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-249">Otherwise, press Enter and the script will create your gateway and attach your app to your virtual network.</span></span> <span data-ttu-id="6aa1f-250">Czas utworzenia bramy jest nadal godzinę, mimo że, upewnij się, że należy pamiętać, że.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-250">The gateway creation time is still an hour, though, so make sure you keep that in mind.</span></span> <span data-ttu-id="6aa1f-251">Gdy wszystko jest gotowe, będzie napisane skrypt **Zakończono**.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-251">When everything is finished, the script will say **Finished**.</span></span>

### <a name="disconnect-your-app-from-a-resource-manager-vnet"></a><span data-ttu-id="6aa1f-252">Rozłączyć aplikacji z Menedżera zasobów sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="6aa1f-252">Disconnect your app from a Resource Manager VNet</span></span>
<span data-ttu-id="6aa1f-253">Odłączanie aplikacji od sieci wirtualnej nie wyłączyć bramy lub Wyłącz połączenie punkt lokacja.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-253">Disconnecting your app from your virtual network does not take down the gateway or disable point-to-site connectivity.</span></span> <span data-ttu-id="6aa1f-254">Być może używasz go do czegoś innego.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-254">You might, after all, be using it for something else.</span></span> <span data-ttu-id="6aa1f-255">On również nie odłączenie go od innych aplikacji, innego niż podany.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-255">It also does not disconnect it from any other apps other than the one you provided.</span></span> <span data-ttu-id="6aa1f-256">Aby wykonać tę akcję, wybierz **3) Usuń sieć wirtualną z aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-256">To perform this action, select **3) Remove a Virtual Network from an App**.</span></span> <span data-ttu-id="6aa1f-257">Jeśli tak zrobisz, zostanie wyświetlony podobny do następującego:</span><span class="sxs-lookup"><span data-stu-id="6aa1f-257">When you do so, you will see something like this:</span></span>

    Currently connected to VNET v2pshell

    Confirm
    Are you sure you want to delete the following resource:
    /subscriptions/edcc99a4-b7f9-4b5e-a9a1-3034c51db496/resourceGroups/hcdemo-rg/providers/Microsoft.Web/sites/v2vnetpowers
    hell/virtualNetworkConnections/v2pshell
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):

<span data-ttu-id="6aa1f-258">Mimo że skrypt jest wyświetlany komunikat delete nie powoduje usunięcia sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-258">Although the script says delete, it does not delete the virtual network.</span></span> <span data-ttu-id="6aa1f-259">Jest on tylko usuwanie integracji.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-259">It’s just removing the integration.</span></span> <span data-ttu-id="6aa1f-260">Po upewnieniu się, że jest to, co chcesz zrobić, polecenie jest bardzo szybko przetwarzane i pozwalają określić **True** po jej zakończeniu.</span><span class="sxs-lookup"><span data-stu-id="6aa1f-260">After you confirm that this is what you want to do, the command is processed quite quickly and tells you **True** when it is done.</span></span>

<!--Links-->
[createvpngateway]: http://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/
[azureportal]: http://portal.azure.com
