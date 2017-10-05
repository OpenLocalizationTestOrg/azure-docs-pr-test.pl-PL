---
title: "Utwórz bramę aplikacji Azure — szablony | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera instrukcje dotyczące tworzenia bramy aplikacji platformy Azure za pomocą szablonu usługi Azure Resource Manager"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 46cca89ccb5bd77d57fabc3e9027fcebd38da8e7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-application-gateway-by-using-the-azure-resource-manager-template"></a><span data-ttu-id="e4896-103">Tworzenie bramy aplikacji przy użyciu szablonu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e4896-103">Create an application gateway by using the Azure Resource Manager template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e4896-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e4896-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="e4896-105">Azure Resource Manager — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="e4896-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="e4896-106">Klasyczny portal Azure — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="e4896-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="e4896-107">Szablon usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e4896-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="e4896-108">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e4896-108">Azure CLI</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="e4896-109">Usługa Azure Application Gateway to moduł równoważenia obciążenia warstwy 7.</span><span class="sxs-lookup"><span data-stu-id="e4896-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="e4896-110">Udostępnia tryb failover oraz oparty na wydajności routing żądań HTTP między różnymi serwerami — w chmurze i lokalnymi.</span><span class="sxs-lookup"><span data-stu-id="e4896-110">It provides failover and performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span> <span data-ttu-id="e4896-111">Usługa Application Gateway zapewnia wiele funkcji kontrolera dostarczania aplikacji (ADC, Application Delivery Controller), w tym między innymi równoważenie obciążenia HTTP, koligację sesji na podstawie plików cookie, odciążanie protokołu Secure Sockets Layer (SSL), niestandardowe sondy kondycji i obsługę wielu witryn.</span><span class="sxs-lookup"><span data-stu-id="e4896-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="e4896-112">Pełną listę obsługiwanych funkcji można znaleźć [omówienie bramy aplikacji](application-gateway-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="e4896-112">To find a complete list of supported features, visit [Application Gateway overview](application-gateway-introduction.md)</span></span>

<span data-ttu-id="e4896-113">W tym artykule przedstawiono sposób pobierania i modyfikacji istniejącego szablonu usługi Azure Resource Manager z usługi GitHub i wdrażania szablonu z serwisu GitHub, programu PowerShell i interfejsu wiersza polecenia Azure.</span><span class="sxs-lookup"><span data-stu-id="e4896-113">This article walks you through downloading and modifying an existing Azure Resource Manager template from GitHub and deploying the template from GitHub, PowerShell, and the Azure CLI.</span></span>

<span data-ttu-id="e4896-114">Jeśli po prostu wdrażasz szablon usługi Azure Resource Manager bezpośrednio z serwisu GitHub bez wprowadzania żadnych zmian, przejdź do wdrażania szablonu z serwisu GitHub.</span><span class="sxs-lookup"><span data-stu-id="e4896-114">If you are simply deploying the Azure Resource Manager template directly from GitHub without any changes, skip to deploy a template from GitHub.</span></span>

## <a name="scenario"></a><span data-ttu-id="e4896-115">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="e4896-115">Scenario</span></span>

<span data-ttu-id="e4896-116">W ramach tego scenariusza wykonasz następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="e4896-116">In this scenario you will:</span></span>

* <span data-ttu-id="e4896-117">Utwórz bramę aplikacji z zapory aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="e4896-117">Create an application gateway with web application firewall.</span></span>
* <span data-ttu-id="e4896-118">Tworzenie sieci wirtualnej o nazwie VirtualNetwork1 przy użyciu zarezerwowanego bloku CIDR 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="e4896-118">Create a virtual network named VirtualNetwork1 with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="e4896-119">Tworzenie podsieci o nazwie Appgatewaysubnet używającej bloku 10.0.0.0/28 jako bloku CIDR.</span><span class="sxs-lookup"><span data-stu-id="e4896-119">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span></span>
* <span data-ttu-id="e4896-120">Ustawianie dwóch wcześniej skonfigurowanych adresów IP zaplecza dla serwerów sieci Web, w przypadku których chcesz równoważyć obciążenie ruchem.</span><span class="sxs-lookup"><span data-stu-id="e4896-120">Set up two previously configured back-end IPs for the web servers you want to load balance the traffic.</span></span> <span data-ttu-id="e4896-121">W tym przykładzie szablonu adresy IP zaplecza to 10.0.1.10 i 10.0.1.11.</span><span class="sxs-lookup"><span data-stu-id="e4896-121">In this template example, the back-end IPs are 10.0.1.10 and 10.0.1.11.</span></span>

> [!NOTE]
> <span data-ttu-id="e4896-122">Te ustawienia to parametry tego szablonu.</span><span class="sxs-lookup"><span data-stu-id="e4896-122">Those settings are the parameters for this template.</span></span> <span data-ttu-id="e4896-123">Aby dostosować szablon, można zmienić zasady, odbiornika protokołu SSL i inne opcje w plik azuredeploy.json.</span><span class="sxs-lookup"><span data-stu-id="e4896-123">To customize the template, you can change rules, the listener, SSL, and other options in the azuredeploy.json file.</span></span>

![Scenariusz](./media/application-gateway-create-gateway-arm-template/scenario.png)

## <a name="download-and-understand-the-azure-resource-manager-template"></a><span data-ttu-id="e4896-125">Pobieranie szablonu usługi Azure Resource Manager i zapoznawanie się z nim</span><span class="sxs-lookup"><span data-stu-id="e4896-125">Download and understand the Azure Resource Manager template</span></span>

<span data-ttu-id="e4896-126">Z witryny GitHub można pobrać istniejący szablon usługi Azure Resource Manager umożliwiający utworzenie sieci wirtualnej z dwoma podsieciami, wprowadzić wybrane zmiany, a następnie ponownie go użyć.</span><span class="sxs-lookup"><span data-stu-id="e4896-126">You can download the existing Azure Resource Manager template to create a virtual network and two subnets from GitHub, make any changes you might want, and reuse it.</span></span> <span data-ttu-id="e4896-127">Aby to zrobić, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="e4896-127">To do so, use the following steps:</span></span>

1. <span data-ttu-id="e4896-128">Przejdź do [Utwórz bramę aplikacji włączona jest Zapora aplikacji sieci web](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf).</span><span class="sxs-lookup"><span data-stu-id="e4896-128">Navigate to [Create Application Gateway with web application firewall enabled](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf).</span></span>
1. <span data-ttu-id="e4896-129">Kliknij opcję **azuredeploy.json**, a następnie kliknij opcję **RAW**.</span><span class="sxs-lookup"><span data-stu-id="e4896-129">Click **azuredeploy.json**, and then click **RAW**.</span></span>
1. <span data-ttu-id="e4896-130">Zapisz plik w folderze lokalnym na komputerze.</span><span class="sxs-lookup"><span data-stu-id="e4896-130">Save the file to a local folder on your computer.</span></span>
1. <span data-ttu-id="e4896-131">Jeśli znasz szablony usługi Azure Resource Manager, przejdź do kroku 7.</span><span class="sxs-lookup"><span data-stu-id="e4896-131">If you are familiar with Azure Resource Manager templates, skip to step 7.</span></span>
1. <span data-ttu-id="e4896-132">Otwórz zapisany plik i przyjrzyj się zawartości sekcji **parametry** w wierszu</span><span class="sxs-lookup"><span data-stu-id="e4896-132">Open the file that you saved and look at the contents under **parameters** in line</span></span>
1. <span data-ttu-id="e4896-133">Parametry szablonu usługi Azure Resource Manager zawierają symbole zastępcze wartości, które można wypełnić podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="e4896-133">Azure Resource Manager template parameters provide a placeholder for values that can be filled out during deployment.</span></span>

  | <span data-ttu-id="e4896-134">Parametr</span><span class="sxs-lookup"><span data-stu-id="e4896-134">Parameter</span></span> | <span data-ttu-id="e4896-135">Opis</span><span class="sxs-lookup"><span data-stu-id="e4896-135">Description</span></span> |
  | --- | --- |
  | <span data-ttu-id="e4896-136">**subnetPrefix**</span><span class="sxs-lookup"><span data-stu-id="e4896-136">**subnetPrefix**</span></span> |<span data-ttu-id="e4896-137">Blok CIDR podsieci bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e4896-137">CIDR block for the application gateway subnet.</span></span> |
  | <span data-ttu-id="e4896-138">**applicationGatewaySize**</span><span class="sxs-lookup"><span data-stu-id="e4896-138">**applicationGatewaySize**</span></span> | <span data-ttu-id="e4896-139">Rozmiar bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e4896-139">Size of the application gateway.</span></span>  <span data-ttu-id="e4896-140">Zapory aplikacji sieci Web udostępnia tylko dla średnich i dużych.</span><span class="sxs-lookup"><span data-stu-id="e4896-140">WAF only allows medium and large.</span></span> |
  | <span data-ttu-id="e4896-141">**backendIpaddress1**</span><span class="sxs-lookup"><span data-stu-id="e4896-141">**backendIpaddress1**</span></span> |<span data-ttu-id="e4896-142">Adres IP pierwszego serwera sieci web.</span><span class="sxs-lookup"><span data-stu-id="e4896-142">IP address of the first web server.</span></span> |
  | <span data-ttu-id="e4896-143">**backendIpaddress2**</span><span class="sxs-lookup"><span data-stu-id="e4896-143">**backendIpaddress2**</span></span> |<span data-ttu-id="e4896-144">Adres IP drugiego serwera sieci web.</span><span class="sxs-lookup"><span data-stu-id="e4896-144">IP address of the second web server.</span></span> |
  | <span data-ttu-id="e4896-145">**wafEnabled**</span><span class="sxs-lookup"><span data-stu-id="e4896-145">**wafEnabled**</span></span> | <span data-ttu-id="e4896-146">Ustawienie, aby określić, czy zapory aplikacji sieci Web jest włączony.</span><span class="sxs-lookup"><span data-stu-id="e4896-146">Setting to determine if WAF is enabled.</span></span>|
  | <span data-ttu-id="e4896-147">**wafMode**</span><span class="sxs-lookup"><span data-stu-id="e4896-147">**wafMode**</span></span> | <span data-ttu-id="e4896-148">Tryb zapory aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="e4896-148">Mode of the web application firewall.</span></span>  <span data-ttu-id="e4896-149">Dostępne są następujące opcje **zapobiegania** lub **wykrywania**.</span><span class="sxs-lookup"><span data-stu-id="e4896-149">Available options are **prevention** or **detection**.</span></span>|
  | <span data-ttu-id="e4896-150">**wafRuleSetType**</span><span class="sxs-lookup"><span data-stu-id="e4896-150">**wafRuleSetType**</span></span> | <span data-ttu-id="e4896-151">Typ zestaw reguł zapory aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="e4896-151">Ruleset type for WAF.</span></span>  <span data-ttu-id="e4896-152">OWASP jest obecnie jedyną obsługiwaną opcją.</span><span class="sxs-lookup"><span data-stu-id="e4896-152">Currently OWASP is the only supported option.</span></span> |
  | <span data-ttu-id="e4896-153">**wafRuleSetVersion**</span><span class="sxs-lookup"><span data-stu-id="e4896-153">**wafRuleSetVersion**</span></span> |<span data-ttu-id="e4896-154">Wersja zestaw reguł.</span><span class="sxs-lookup"><span data-stu-id="e4896-154">Ruleset version.</span></span> <span data-ttu-id="e4896-155">CRS OWASP 2.2.9 i 3.0 są obecnie obsługiwane opcje.</span><span class="sxs-lookup"><span data-stu-id="e4896-155">OWASP CRS 2.2.9 and 3.0 are currently the supported options.</span></span> |

1. <span data-ttu-id="e4896-156">Sprawdź zawartość w obszarze **zasobów** i zwróć uwagę, następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="e4896-156">Check the content under **resources** and notice the following properties:</span></span>

   * <span data-ttu-id="e4896-157">**type**.</span><span class="sxs-lookup"><span data-stu-id="e4896-157">**type**.</span></span> <span data-ttu-id="e4896-158">Typ zasobu tworzonego przez szablon.</span><span class="sxs-lookup"><span data-stu-id="e4896-158">Type of resource being created by the template.</span></span> <span data-ttu-id="e4896-159">W tym przypadku jest typ `Microsoft.Network/applicationGateways`, który reprezentuje bramę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e4896-159">In this case, the type is `Microsoft.Network/applicationGateways`, which represents an application gateway.</span></span>
   * <span data-ttu-id="e4896-160">**name**.</span><span class="sxs-lookup"><span data-stu-id="e4896-160">**name**.</span></span> <span data-ttu-id="e4896-161">Nazwa zasobu.</span><span class="sxs-lookup"><span data-stu-id="e4896-161">Name for the resource.</span></span> <span data-ttu-id="e4896-162">Zwróć uwagę na `[parameters('applicationGatewayName')]`, co oznacza, że nazwa jest podana jako dane wejściowe przez Ciebie lub pliku parametrów podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="e4896-162">Notice the use of `[parameters('applicationGatewayName')]`, which means that the name is provided as input by you or by a parameter file during deployment.</span></span>
   * <span data-ttu-id="e4896-163">**properties**.</span><span class="sxs-lookup"><span data-stu-id="e4896-163">**properties**.</span></span> <span data-ttu-id="e4896-164">Lista właściwości zasobu.</span><span class="sxs-lookup"><span data-stu-id="e4896-164">List of properties for the resource.</span></span> <span data-ttu-id="e4896-165">Ten szablon korzysta z sieci wirtualnej i publicznego adresu IP podczas tworzenia aplikacji bramy.</span><span class="sxs-lookup"><span data-stu-id="e4896-165">This template uses the virtual network and public IP address during application gateway creation.</span></span>

   > [!NOTE]
   > <span data-ttu-id="e4896-166">Aby uzyskać więcej informacji na temat szablonów odwiedź: [dokumentacja szablonów usługi Resource Manager](/templates/)</span><span class="sxs-lookup"><span data-stu-id="e4896-166">For more information on templates visit: [Resource Manager templates reference](/templates/)</span></span>

1. <span data-ttu-id="e4896-167">Przejdź z powrotem do [https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf).</span><span class="sxs-lookup"><span data-stu-id="e4896-167">Navigate back to [https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf).</span></span>
1. <span data-ttu-id="e4896-168">Kliknij przycisk **parameters.JSON następującym kodem azuredeploy**, a następnie kliknij przycisk **RAW**.</span><span class="sxs-lookup"><span data-stu-id="e4896-168">Click **azuredeploy-parameters.json**, and then click **RAW**.</span></span>
1. <span data-ttu-id="e4896-169">Zapisz plik w folderze lokalnym na komputerze.</span><span class="sxs-lookup"><span data-stu-id="e4896-169">Save the file to a local folder on your computer.</span></span>
1. <span data-ttu-id="e4896-170">Otwórz zapisany plik i edytuj wartości parametrów.</span><span class="sxs-lookup"><span data-stu-id="e4896-170">Open the file that you saved and edit the values for the parameters.</span></span> <span data-ttu-id="e4896-171">Do wdrożenia opisanej w scenariuszu bramy aplikacji użyj poniższych wartości.</span><span class="sxs-lookup"><span data-stu-id="e4896-171">Use the following values to deploy the application gateway described in our scenario.</span></span>

    ```json
    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "addressPrefix": {
            "value": "10.0.0.0/16"
            },
            "subnetPrefix": {
            "value": "10.0.0.0/28"
            },
            "applicationGatewaySize": {
            "value": "WAF_Medium"
            },
            "capacity": {
            "value": 2
            },
            "backendIpAddress1": {
            "value": "10.0.1.10"
            },
            "backendIpAddress2": {
            "value": "10.0.1.11"
            },
            "wafEnabled": {
            "value": true
            },
            "wafMode": {
            "value": "Detection"
            },
            "wafRuleSetType": {
            "value": "OWASP"
            },
            "wafRuleSetVersion": {
            "value": "3.0"
            }
        }
    }
    ```

1. <span data-ttu-id="e4896-172">Zapisz plik.</span><span class="sxs-lookup"><span data-stu-id="e4896-172">Save the file.</span></span> <span data-ttu-id="e4896-173">Szablon JSON i szablon parametrów można przetestować za pomocą narzędzi weryfikacji danych JSON w trybie online, takich jak [JSlint.com](http://www.jslint.com/).</span><span class="sxs-lookup"><span data-stu-id="e4896-173">You can test the JSON template and parameter template by using online JSON validation tools like [JSlint.com](http://www.jslint.com/).</span></span>

## <a name="deploy-the-azure-resource-manager-template-by-using-powershell"></a><span data-ttu-id="e4896-174">Wdrażanie szablonu usługi Azure Resource Manager przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="e4896-174">Deploy the Azure Resource Manager template by using PowerShell</span></span>

<span data-ttu-id="e4896-175">Jeśli nie znasz programu Azure PowerShell, odwiedź stronę: [jak instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) i postępuj zgodnie z instrukcjami, aby zalogować się do platformy Azure i wyboru subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="e4896-175">If you have never used Azure PowerShell, visit: [How to install and configure Azure PowerShell](/powershell/azure/overview) and follow the instructions to sign into Azure and select your subscription.</span></span>

1. <span data-ttu-id="e4896-176">Logowanie do programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="e4896-176">Login to PowerShell</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="e4896-177">Sprawdź subskrypcje dostępne na koncie.</span><span class="sxs-lookup"><span data-stu-id="e4896-177">Check the subscriptions for the account.</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

    <span data-ttu-id="e4896-178">Zostanie wyświetlony monit o uwierzytelnienie przy użyciu własnych poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="e4896-178">You are prompted to authenticate with your credentials.</span></span>

1. <span data-ttu-id="e4896-179">Wybierz subskrypcję platformy Azure do użycia.</span><span class="sxs-lookup"><span data-stu-id="e4896-179">Choose which of your Azure subscriptions to use.</span></span>

    ```powershell
    Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
    ```

1. <span data-ttu-id="e4896-180">W razie potrzeby utwórz grupę zasobów za pomocą polecenia cmdlet **New-AzureResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="e4896-180">If needed, create a resource group by using the **New-AzureResourceGroup** cmdlet.</span></span> <span data-ttu-id="e4896-181">W poniższym przykładzie należy utworzyć grupę zasobów o nazwie AppgatewayRG w lokalizacji wschodnie stany USA.</span><span class="sxs-lookup"><span data-stu-id="e4896-181">In the following example, you create a resource group called AppgatewayRG in East US location.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name AppgatewayRG -Location "West US"
    ```

1. <span data-ttu-id="e4896-182">Uruchom polecenie cmdlet **New-AzureRmResourceGroupDeployment**, aby wdrożyć nową sieć wirtualną przy użyciu uprzednio pobranych i zmodyfikowanych plików szablonu oraz parametrów.</span><span class="sxs-lookup"><span data-stu-id="e4896-182">Run the **New-AzureRmResourceGroupDeployment** cmdlet to deploy the new virtual network by using the preceding template and parameter files you downloaded and modified.</span></span>
    
    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestAppgatewayDeployment -ResourceGroupName AppgatewayRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

## <a name="deploy-the-azure-resource-manager-template-by-using-the-azure-cli"></a><span data-ttu-id="e4896-183">Wdrażanie szablonu usługi Azure Resource Manager przy użyciu interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e4896-183">Deploy the Azure Resource Manager template by using the Azure CLI</span></span>

<span data-ttu-id="e4896-184">Aby wdrożyć szablon usługi Azure Resource Manager, który został pobrany przy użyciu wiersza polecenia platformy Azure, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="e4896-184">To deploy the Azure Resource Manager template you downloaded by using Azure CLI, follow the following steps:</span></span>

1. <span data-ttu-id="e4896-185">Jeśli po raz pierwszy używasz interfejsu wiersza polecenia platformy Azure, zobacz artykuł [Install and configure the Azure CLI](/cli/azure/install-azure-cli) (Instalowanie i konfigurowanie interfejsu wiersza polecenia Azure) i postępuj zgodnie z instrukcjami aż do momentu wybrania konta i subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e4896-185">If you have never used Azure CLI, see [Install and configure the Azure CLI](/cli/azure/install-azure-cli) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>

1. <span data-ttu-id="e4896-186">W razie potrzeby uruchom `az group create` polecenie, aby utworzyć grupę zasobów, jak pokazano w poniższy fragment kodu.</span><span class="sxs-lookup"><span data-stu-id="e4896-186">If necessary, run the `az group create` command to create a resource group, as shown in the following code snippet.</span></span> <span data-ttu-id="e4896-187">Zwróć uwagę na dane wyjściowe polecenia.</span><span class="sxs-lookup"><span data-stu-id="e4896-187">Notice the output of the command.</span></span> <span data-ttu-id="e4896-188">Lista wyświetlana po danych wyjściowych zawiera opis używanych parametrów.</span><span class="sxs-lookup"><span data-stu-id="e4896-188">The list shown after the output explains the parameters used.</span></span> <span data-ttu-id="e4896-189">Aby uzyskać więcej informacji na temat grup zasobów, zobacz temat [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e4896-189">For more information about resource groups, visit [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    ```azurecli
    az group create --location westus --name appgatewayRG
    ```
    
    <span data-ttu-id="e4896-190">**-n (lub --name)**.</span><span class="sxs-lookup"><span data-stu-id="e4896-190">**-n (or --name)**.</span></span> <span data-ttu-id="e4896-191">Nazwa nowej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="e4896-191">Name for the new resource group.</span></span> <span data-ttu-id="e4896-192">W naszym scenariuszu jest to *appgatewayRG*.</span><span class="sxs-lookup"><span data-stu-id="e4896-192">For our scenario, it's *appgatewayRG*.</span></span>
    
    <span data-ttu-id="e4896-193">**-l (lub --location)**.</span><span class="sxs-lookup"><span data-stu-id="e4896-193">**-l (or --location)**.</span></span> <span data-ttu-id="e4896-194">Region świadczenia usługi Azure, w którym zostanie utworzona nowa grupa zasobów.</span><span class="sxs-lookup"><span data-stu-id="e4896-194">Azure region where the new resource group is created.</span></span> <span data-ttu-id="e4896-195">W naszym scenariuszu ma *westus*.</span><span class="sxs-lookup"><span data-stu-id="e4896-195">For our scenario, it's *westus*.</span></span>

1. <span data-ttu-id="e4896-196">Uruchom `az group deployment create` polecenia cmdlet, aby wdrożyć nową sieć wirtualną przy użyciu szablonu i parametr pliki, możesz pobrać i zmodyfikować w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="e4896-196">Run the `az group deployment create` cmdlet to deploy the new virtual network by using the template and parameter files you downloaded and modified in the preceding step.</span></span> <span data-ttu-id="e4896-197">Lista wyświetlana po danych wyjściowych zawiera opis używanych parametrów.</span><span class="sxs-lookup"><span data-stu-id="e4896-197">The list shown after the output explains the parameters used.</span></span>

    ```azurecli
    az group deployment create --resource-group appgatewayRG --name TestAppgatewayDeployment --template-file azuredeploy.json --parameters @azuredeploy-parameters.json
    ```

## <a name="deploy-the-azure-resource-manager-template-by-using-click-to-deploy"></a><span data-ttu-id="e4896-198">Wdrażanie szablonu usługi Azure Resource Manager przy użyciu funkcji szybkiego wdrażania</span><span class="sxs-lookup"><span data-stu-id="e4896-198">Deploy the Azure Resource Manager template by using click-to-deploy</span></span>

<span data-ttu-id="e4896-199">Użycie funkcji szybkiego wdrażania to kolejny sposób korzystania z szablonów usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e4896-199">Click-to-deploy is another way to use Azure Resource Manager templates.</span></span> <span data-ttu-id="e4896-200">Jest to prosty sposób używania szablonów w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e4896-200">It's an easy way to use templates with the Azure portal.</span></span>

1. <span data-ttu-id="e4896-201">Przejdź do [Utwórz bramę aplikacji z zapory aplikacji sieci web](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/).</span><span class="sxs-lookup"><span data-stu-id="e4896-201">Go to [Create an application gateway with web application firewall](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/).</span></span>

1. <span data-ttu-id="e4896-202">Kliknij przycisk **Wdrażaj na platformie Azure**.</span><span class="sxs-lookup"><span data-stu-id="e4896-202">Click **Deploy to Azure**.</span></span>

    ![Wdrażanie na platformie Azure](./media/application-gateway-create-gateway-arm-template/deploytoazure.png)
    
1. <span data-ttu-id="e4896-204">Wprowadź parametry szablonu wdrożenia w portalu i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="e4896-204">Fill out the parameters for the deployment template on the portal and click **OK**.</span></span>

    ![Parametry](./media/application-gateway-create-gateway-arm-template/ibiza1.png)
    
1. <span data-ttu-id="e4896-206">Wybierz **akceptuję warunki i postanowienia, o których wspomniano** i kliknij przycisk **zakupu**.</span><span class="sxs-lookup"><span data-stu-id="e4896-206">Select **I agree to the terms and conditions stated above** and click **Purchase**.</span></span>

1. <span data-ttu-id="e4896-207">W bloku wdrożenia niestandardowego kliknij pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="e4896-207">On the Custom deployment blade, click **Create**.</span></span>

## <a name="providing-certificate-data-to-resource-manager-templates"></a><span data-ttu-id="e4896-208">Dostarcza dane certyfikatu w szablonach usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e4896-208">Providing certificate data to Resource Manager templates</span></span>

<span data-ttu-id="e4896-209">Przy korzystaniu z protokołu SSL przy użyciu szablonu certyfikatu musi zostać zapewniony w zamiast przekazywanych ciąg w formacie base64.</span><span class="sxs-lookup"><span data-stu-id="e4896-209">When using SSL with a template, the certificate needs to be provided in a base64 string instead of being uploaded.</span></span> <span data-ttu-id="e4896-210">Aby przekonwertować pfx lub .cer ciąg base64 użyj jednej z następujących poleceń.</span><span class="sxs-lookup"><span data-stu-id="e4896-210">To convert a .pfx or .cer to a base64 string use one of the following commands.</span></span> <span data-ttu-id="e4896-211">Następujące polecenia przekonwertować ciąg base64, który może zostać dostarczona do szablonu certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="e4896-211">The following commands convert the certificate to a base64 string, which can be provided to the template.</span></span> <span data-ttu-id="e4896-212">Oczekiwane dane wyjściowe jest ciągiem, który może być przechowywana w zmiennej i wkleić w szablonie.</span><span class="sxs-lookup"><span data-stu-id="e4896-212">The expected output is a string that can be stored in a variable and pasted in the template.</span></span>

### <a name="macos"></a><span data-ttu-id="e4896-213">macOS</span><span class="sxs-lookup"><span data-stu-id="e4896-213">macOS</span></span>
```bash
cert=$( base64 <certificate path and name>.pfx )
echo $cert
```

### <a name="windows"></a><span data-ttu-id="e4896-214">Windows</span><span class="sxs-lookup"><span data-stu-id="e4896-214">Windows</span></span>
```powershell
[System.Convert]::ToBase64String([System.IO.File]::ReadAllBytes("<certificate path and name>.pfx"))
```

## <a name="delete-all-resources"></a><span data-ttu-id="e4896-215">Usuwanie wszystkich zasobów</span><span class="sxs-lookup"><span data-stu-id="e4896-215">Delete all resources</span></span>

<span data-ttu-id="e4896-216">Aby usunąć wszystkie zasoby utworzone w tym artykule, wykonaj jedną z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="e4896-216">To delete all resources created in this article, complete one of the following steps:</span></span>

### <a name="powershell"></a><span data-ttu-id="e4896-217">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e4896-217">PowerShell</span></span>

```powershell
Remove-AzureRmResourceGroup -Name appgatewayRG
```

### <a name="azure-cli"></a><span data-ttu-id="e4896-218">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e4896-218">Azure CLI</span></span>

```azurecli
az group delete --name appgatewayRG
```

## <a name="next-steps"></a><span data-ttu-id="e4896-219">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e4896-219">Next steps</span></span>

<span data-ttu-id="e4896-220">Jeśli chcesz skonfigurować odciążanie protokołu SSL, odwiedź: [Configure an application gateway for SSL offload](application-gateway-ssl.md) (Konfigurowanie bramy aplikacji na potrzeby odciążania protokołu SSL).</span><span class="sxs-lookup"><span data-stu-id="e4896-220">If you want to configure SSL offload, visit: [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="e4896-221">Jeśli chcesz skonfigurować bramę aplikacji do użycia z wewnętrznym modułem równoważenia obciążenia, odwiedź: [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md) (Tworzenie bramy aplikacji przy użyciu wewnętrznego modułu równoważenia obciążenia).</span><span class="sxs-lookup"><span data-stu-id="e4896-221">If you want to configure an application gateway to use with an internal load balancer, visit: [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="e4896-222">Więcej ogólnych informacji na temat opcji równoważenia obciążenia możesz znaleźć, odwiedzając:</span><span class="sxs-lookup"><span data-stu-id="e4896-222">If you want more information about load balancing options in general, visit:</span></span>

* [<span data-ttu-id="e4896-223">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="e4896-223">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="e4896-224">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="e4896-224">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

