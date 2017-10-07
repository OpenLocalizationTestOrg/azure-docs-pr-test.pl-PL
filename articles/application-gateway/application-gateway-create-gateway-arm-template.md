---
title: "aaaCreate bramę aplikacji Azure — szablony | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera instrukcje toocreate bramę aplikacji platformy Azure przy użyciu szablonu usługi Azure Resource Manager hello"
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
ms.openlocfilehash: fc18e553852551326d6a302abe2c7f8a08c2eb6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-resource-manager-template"></a><span data-ttu-id="5409b-103">Tworzenie za pomocą szablonu usługi Azure Resource Manager hello bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="5409b-103">Create an application gateway by using hello Azure Resource Manager template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5409b-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5409b-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="5409b-105">Azure Resource Manager — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="5409b-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="5409b-106">Klasyczny portal Azure — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="5409b-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="5409b-107">Szablon usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5409b-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="5409b-108">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="5409b-108">Azure CLI</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="5409b-109">Usługa Azure Application Gateway to moduł równoważenia obciążenia warstwy 7.</span><span class="sxs-lookup"><span data-stu-id="5409b-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="5409b-110">Udostępnia trybu failover i wydajności routingu żądań HTTP między różnymi serwerami, czy znajdują się w chmurze hello lub lokalnie.</span><span class="sxs-lookup"><span data-stu-id="5409b-110">It provides failover and performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="5409b-111">Usługa Application Gateway zapewnia wiele funkcji kontrolera dostarczania aplikacji (ADC, Application Delivery Controller), w tym między innymi równoważenie obciążenia HTTP, koligację sesji na podstawie plików cookie, odciążanie protokołu Secure Sockets Layer (SSL), niestandardowe sondy kondycji i obsługę wielu witryn.</span><span class="sxs-lookup"><span data-stu-id="5409b-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="5409b-112">odwiedź toofind pełną listę obsługiwanych funkcji [omówienie bramy aplikacji](application-gateway-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="5409b-112">toofind a complete list of supported features, visit [Application Gateway overview](application-gateway-introduction.md)</span></span>

<span data-ttu-id="5409b-113">W tym artykule przedstawiono sposób pobierania i modyfikacji istniejącego szablonu usługi Azure Resource Manager z usługi GitHub i wdrażanie hello szablonu z serwisu GitHub, programu PowerShell i hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5409b-113">This article walks you through downloading and modifying an existing Azure Resource Manager template from GitHub and deploying hello template from GitHub, PowerShell, and hello Azure CLI.</span></span>

<span data-ttu-id="5409b-114">Jeśli po prostu wdrażasz szablon usługi Azure Resource Manager hello bezpośrednio z serwisu GitHub, bez wprowadzania żadnych zmian, Pomiń toodeploy szablonu z serwisu GitHub.</span><span class="sxs-lookup"><span data-stu-id="5409b-114">If you are simply deploying hello Azure Resource Manager template directly from GitHub without any changes, skip toodeploy a template from GitHub.</span></span>

## <a name="scenario"></a><span data-ttu-id="5409b-115">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="5409b-115">Scenario</span></span>

<span data-ttu-id="5409b-116">W ramach tego scenariusza wykonasz następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5409b-116">In this scenario you will:</span></span>

* <span data-ttu-id="5409b-117">Utwórz bramę aplikacji z zapory aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="5409b-117">Create an application gateway with web application firewall.</span></span>
* <span data-ttu-id="5409b-118">Tworzenie sieci wirtualnej o nazwie VirtualNetwork1 przy użyciu zarezerwowanego bloku CIDR 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="5409b-118">Create a virtual network named VirtualNetwork1 with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="5409b-119">Tworzenie podsieci o nazwie Appgatewaysubnet używającej bloku 10.0.0.0/28 jako bloku CIDR.</span><span class="sxs-lookup"><span data-stu-id="5409b-119">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span></span>
* <span data-ttu-id="5409b-120">Konfigurowanie dwóch wcześniej skonfigurowane adresy IP zaplecza dla serwerów sieci web hello bilans tooload hello ruchu.</span><span class="sxs-lookup"><span data-stu-id="5409b-120">Set up two previously configured back-end IPs for hello web servers you want tooload balance hello traffic.</span></span> <span data-ttu-id="5409b-121">W tym przykładzie szablon hello zaplecza adresy IP są 10.0.1.10 i 10.0.1.11.</span><span class="sxs-lookup"><span data-stu-id="5409b-121">In this template example, hello back-end IPs are 10.0.1.10 and 10.0.1.11.</span></span>

> [!NOTE]
> <span data-ttu-id="5409b-122">Te ustawienia są hello parametrów dla tego szablonu.</span><span class="sxs-lookup"><span data-stu-id="5409b-122">Those settings are hello parameters for this template.</span></span> <span data-ttu-id="5409b-123">Szablon hello toocustomize, można zmienić zasady, hello odbiornika protokołu SSL i inne opcje w plik azuredeploy.json hello.</span><span class="sxs-lookup"><span data-stu-id="5409b-123">toocustomize hello template, you can change rules, hello listener, SSL, and other options in hello azuredeploy.json file.</span></span>

![Scenariusz](./media/application-gateway-create-gateway-arm-template/scenario.png)

## <a name="download-and-understand-hello-azure-resource-manager-template"></a><span data-ttu-id="5409b-125">Pobierz i zrozumieć hello szablonu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5409b-125">Download and understand hello Azure Resource Manager template</span></span>

<span data-ttu-id="5409b-126">Możesz pobrać z witryny GitHub hello istniejącej usługi Azure Resource Manager szablonu toocreate sieci wirtualnej z dwoma podsieciami, zmiany mogą, a następnie użyć go ponownie.</span><span class="sxs-lookup"><span data-stu-id="5409b-126">You can download hello existing Azure Resource Manager template toocreate a virtual network and two subnets from GitHub, make any changes you might want, and reuse it.</span></span> <span data-ttu-id="5409b-127">toodo tak, użycie hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="5409b-127">toodo so, use hello following steps:</span></span>

1. <span data-ttu-id="5409b-128">Przejdź za[Utwórz bramę aplikacji włączona jest Zapora aplikacji sieci web](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf).</span><span class="sxs-lookup"><span data-stu-id="5409b-128">Navigate too[Create Application Gateway with web application firewall enabled](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf).</span></span>
1. <span data-ttu-id="5409b-129">Kliknij opcję **azuredeploy.json**, a następnie kliknij opcję **RAW**.</span><span class="sxs-lookup"><span data-stu-id="5409b-129">Click **azuredeploy.json**, and then click **RAW**.</span></span>
1. <span data-ttu-id="5409b-130">Zapisz hello pliku tooa lokalnego folderu na komputerze.</span><span class="sxs-lookup"><span data-stu-id="5409b-130">Save hello file tooa local folder on your computer.</span></span>
1. <span data-ttu-id="5409b-131">Jeśli znasz szablony Menedżera zasobów Azure, Pomiń toostep 7.</span><span class="sxs-lookup"><span data-stu-id="5409b-131">If you are familiar with Azure Resource Manager templates, skip toostep 7.</span></span>
1. <span data-ttu-id="5409b-132">Otwórz zapisany plik hello i przyjrzyj się zawartości hello w obszarze **parametry** w wierszu</span><span class="sxs-lookup"><span data-stu-id="5409b-132">Open hello file that you saved and look at hello contents under **parameters** in line</span></span>
1. <span data-ttu-id="5409b-133">Parametry szablonu usługi Azure Resource Manager zawierają symbole zastępcze wartości, które można wypełnić podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="5409b-133">Azure Resource Manager template parameters provide a placeholder for values that can be filled out during deployment.</span></span>

  | <span data-ttu-id="5409b-134">Parametr</span><span class="sxs-lookup"><span data-stu-id="5409b-134">Parameter</span></span> | <span data-ttu-id="5409b-135">Opis</span><span class="sxs-lookup"><span data-stu-id="5409b-135">Description</span></span> |
  | --- | --- |
  | <span data-ttu-id="5409b-136">**subnetPrefix**</span><span class="sxs-lookup"><span data-stu-id="5409b-136">**subnetPrefix**</span></span> |<span data-ttu-id="5409b-137">Blok CIDR podsieci bramy aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="5409b-137">CIDR block for hello application gateway subnet.</span></span> |
  | <span data-ttu-id="5409b-138">**applicationGatewaySize**</span><span class="sxs-lookup"><span data-stu-id="5409b-138">**applicationGatewaySize**</span></span> | <span data-ttu-id="5409b-139">Rozmiar hello bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5409b-139">Size of hello application gateway.</span></span>  <span data-ttu-id="5409b-140">Zapory aplikacji sieci Web udostępnia tylko dla średnich i dużych.</span><span class="sxs-lookup"><span data-stu-id="5409b-140">WAF only allows medium and large.</span></span> |
  | <span data-ttu-id="5409b-141">**backendIpaddress1**</span><span class="sxs-lookup"><span data-stu-id="5409b-141">**backendIpaddress1**</span></span> |<span data-ttu-id="5409b-142">Adres IP hello na pierwszym serwerze sieci web.</span><span class="sxs-lookup"><span data-stu-id="5409b-142">IP address of hello first web server.</span></span> |
  | <span data-ttu-id="5409b-143">**backendIpaddress2**</span><span class="sxs-lookup"><span data-stu-id="5409b-143">**backendIpaddress2**</span></span> |<span data-ttu-id="5409b-144">Adres IP hello drugi serwer sieci web.</span><span class="sxs-lookup"><span data-stu-id="5409b-144">IP address of hello second web server.</span></span> |
  | <span data-ttu-id="5409b-145">**wafEnabled**</span><span class="sxs-lookup"><span data-stu-id="5409b-145">**wafEnabled**</span></span> | <span data-ttu-id="5409b-146">Ustawienie toodetermine zapory aplikacji sieci Web jest włączona.</span><span class="sxs-lookup"><span data-stu-id="5409b-146">Setting toodetermine if WAF is enabled.</span></span>|
  | <span data-ttu-id="5409b-147">**wafMode**</span><span class="sxs-lookup"><span data-stu-id="5409b-147">**wafMode**</span></span> | <span data-ttu-id="5409b-148">Tryb zapory aplikacji sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="5409b-148">Mode of hello web application firewall.</span></span>  <span data-ttu-id="5409b-149">Dostępne są następujące opcje **zapobiegania** lub **wykrywania**.</span><span class="sxs-lookup"><span data-stu-id="5409b-149">Available options are **prevention** or **detection**.</span></span>|
  | <span data-ttu-id="5409b-150">**wafRuleSetType**</span><span class="sxs-lookup"><span data-stu-id="5409b-150">**wafRuleSetType**</span></span> | <span data-ttu-id="5409b-151">Typ zestaw reguł zapory aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="5409b-151">Ruleset type for WAF.</span></span>  <span data-ttu-id="5409b-152">Obecnie OWASP jest hello obsługiwane tylko opcja.</span><span class="sxs-lookup"><span data-stu-id="5409b-152">Currently OWASP is hello only supported option.</span></span> |
  | <span data-ttu-id="5409b-153">**wafRuleSetVersion**</span><span class="sxs-lookup"><span data-stu-id="5409b-153">**wafRuleSetVersion**</span></span> |<span data-ttu-id="5409b-154">Wersja zestaw reguł.</span><span class="sxs-lookup"><span data-stu-id="5409b-154">Ruleset version.</span></span> <span data-ttu-id="5409b-155">CRS OWASP 2.2.9 i 3.0 są obecnie obsługiwane hello opcje.</span><span class="sxs-lookup"><span data-stu-id="5409b-155">OWASP CRS 2.2.9 and 3.0 are currently hello supported options.</span></span> |

1. <span data-ttu-id="5409b-156">Sprawdź zawartość hello w obszarze **zasobów** i hello powiadomienia następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="5409b-156">Check hello content under **resources** and notice hello following properties:</span></span>

   * <span data-ttu-id="5409b-157">**type**.</span><span class="sxs-lookup"><span data-stu-id="5409b-157">**type**.</span></span> <span data-ttu-id="5409b-158">Typ zasobu tworzonego przez szablon hello.</span><span class="sxs-lookup"><span data-stu-id="5409b-158">Type of resource being created by hello template.</span></span> <span data-ttu-id="5409b-159">W takim przypadku typ hello jest `Microsoft.Network/applicationGateways`, który reprezentuje bramę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5409b-159">In this case, hello type is `Microsoft.Network/applicationGateways`, which represents an application gateway.</span></span>
   * <span data-ttu-id="5409b-160">**name**.</span><span class="sxs-lookup"><span data-stu-id="5409b-160">**name**.</span></span> <span data-ttu-id="5409b-161">Nazwa zasobu hello.</span><span class="sxs-lookup"><span data-stu-id="5409b-161">Name for hello resource.</span></span> <span data-ttu-id="5409b-162">Użycie hello powiadomienia `[parameters('applicationGatewayName')]`, co oznacza, że ta nazwa hello jest podana jako dane wejściowe przez Ciebie lub pliku parametrów podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="5409b-162">Notice hello use of `[parameters('applicationGatewayName')]`, which means that hello name is provided as input by you or by a parameter file during deployment.</span></span>
   * <span data-ttu-id="5409b-163">**properties**.</span><span class="sxs-lookup"><span data-stu-id="5409b-163">**properties**.</span></span> <span data-ttu-id="5409b-164">Lista właściwości zasobu hello.</span><span class="sxs-lookup"><span data-stu-id="5409b-164">List of properties for hello resource.</span></span> <span data-ttu-id="5409b-165">Ten szablon używa hello sieć wirtualna i publiczny adres IP podczas tworzenia bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5409b-165">This template uses hello virtual network and public IP address during application gateway creation.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5409b-166">Aby uzyskać więcej informacji na temat szablonów odwiedź: [dokumentacja szablonów usługi Resource Manager](/templates/)</span><span class="sxs-lookup"><span data-stu-id="5409b-166">For more information on templates visit: [Resource Manager templates reference](/templates/)</span></span>

1. <span data-ttu-id="5409b-167">Przejdź wstecz zbyt[https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf).</span><span class="sxs-lookup"><span data-stu-id="5409b-167">Navigate back too[https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf).</span></span>
1. <span data-ttu-id="5409b-168">Kliknij przycisk **parameters.JSON następującym kodem azuredeploy**, a następnie kliknij przycisk **RAW**.</span><span class="sxs-lookup"><span data-stu-id="5409b-168">Click **azuredeploy-parameters.json**, and then click **RAW**.</span></span>
1. <span data-ttu-id="5409b-169">Zapisz hello pliku tooa lokalnego folderu na komputerze.</span><span class="sxs-lookup"><span data-stu-id="5409b-169">Save hello file tooa local folder on your computer.</span></span>
1. <span data-ttu-id="5409b-170">Otwórz zapisany plik hello i edytowania wartości hello hello parametrów.</span><span class="sxs-lookup"><span data-stu-id="5409b-170">Open hello file that you saved and edit hello values for hello parameters.</span></span> <span data-ttu-id="5409b-171">Użyj hello następujące wartości toodeploy hello brama aplikacji w opisanej w scenariuszu.</span><span class="sxs-lookup"><span data-stu-id="5409b-171">Use hello following values toodeploy hello application gateway described in our scenario.</span></span>

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

1. <span data-ttu-id="5409b-172">Zapisz plik hello.</span><span class="sxs-lookup"><span data-stu-id="5409b-172">Save hello file.</span></span> <span data-ttu-id="5409b-173">Należy przetestować hello JSON szablonu i parametr szablonu przy użyciu online narzędzia sprawdzania poprawności formatu JSON, takie jak [JSlint.com](http://www.jslint.com/).</span><span class="sxs-lookup"><span data-stu-id="5409b-173">You can test hello JSON template and parameter template by using online JSON validation tools like [JSlint.com](http://www.jslint.com/).</span></span>

## <a name="deploy-hello-azure-resource-manager-template-by-using-powershell"></a><span data-ttu-id="5409b-174">Wdrażanie szablonu usługi Azure Resource Manager hello przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="5409b-174">Deploy hello Azure Resource Manager template by using PowerShell</span></span>

<span data-ttu-id="5409b-175">Jeśli nie znasz programu Azure PowerShell, odwiedź stronę: [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) i wykonaj toosign instrukcje hello na platformie Azure i wyboru subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="5409b-175">If you have never used Azure PowerShell, visit: [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) and follow hello instructions toosign into Azure and select your subscription.</span></span>

1. <span data-ttu-id="5409b-176">TooPowerShell logowania</span><span class="sxs-lookup"><span data-stu-id="5409b-176">Login tooPowerShell</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="5409b-177">Sprawdź subskrypcje hello hello konta.</span><span class="sxs-lookup"><span data-stu-id="5409b-177">Check hello subscriptions for hello account.</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

    <span data-ttu-id="5409b-178">Jesteś zostanie wyświetlony monit o tooauthenticate przy użyciu poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="5409b-178">You are prompted tooauthenticate with your credentials.</span></span>

1. <span data-ttu-id="5409b-179">Wybierz z toouse Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5409b-179">Choose which of your Azure subscriptions toouse.</span></span>

    ```powershell
    Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
    ```

1. <span data-ttu-id="5409b-180">W razie potrzeby utwórz grupę zasobów za pomocą hello **New-AzureResourceGroup** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5409b-180">If needed, create a resource group by using hello **New-AzureResourceGroup** cmdlet.</span></span> <span data-ttu-id="5409b-181">Poniższy przykład hello służy do tworzenia grupy zasobów o nazwie AppgatewayRG w lokalizacji wschodnie stany USA.</span><span class="sxs-lookup"><span data-stu-id="5409b-181">In hello following example, you create a resource group called AppgatewayRG in East US location.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name AppgatewayRG -Location "West US"
    ```

1. <span data-ttu-id="5409b-182">Uruchom hello **AzureRmResourceGroupDeployment nowy** polecenia cmdlet toodeploy hello nową sieć wirtualną przy użyciu hello poprzedzających plików szablonu i parametr pobrane i modyfikować.</span><span class="sxs-lookup"><span data-stu-id="5409b-182">Run hello **New-AzureRmResourceGroupDeployment** cmdlet toodeploy hello new virtual network by using hello preceding template and parameter files you downloaded and modified.</span></span>
    
    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestAppgatewayDeployment -ResourceGroupName AppgatewayRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

## <a name="deploy-hello-azure-resource-manager-template-by-using-hello-azure-cli"></a><span data-ttu-id="5409b-183">Wdrażanie szablonu usługi Azure Resource Manager hello przy użyciu hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="5409b-183">Deploy hello Azure Resource Manager template by using hello Azure CLI</span></span>

<span data-ttu-id="5409b-184">toodeploy hello Azure Resource Manager szablon, który został pobrany przy użyciu wiersza polecenia platformy Azure, wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="5409b-184">toodeploy hello Azure Resource Manager template you downloaded by using Azure CLI, follow hello following steps:</span></span>

1. <span data-ttu-id="5409b-185">Jeśli po raz pierwszy używasz interfejsu wiersza polecenia Azure, zobacz [zainstalować i skonfigurować hello Azure CLI](/cli/azure/install-azure-cli) i wykonaj instrukcje hello zapasowej punktu toohello, gdzie należy wybrać konto platformy Azure i subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="5409b-185">If you have never used Azure CLI, see [Install and configure hello Azure CLI](/cli/azure/install-azure-cli) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>

1. <span data-ttu-id="5409b-186">Jeśli to konieczne, uruchom hello `az group create` toocreate polecenia grupę zasobów, jak pokazano w hello następującego fragmentu kodu.</span><span class="sxs-lookup"><span data-stu-id="5409b-186">If necessary, run hello `az group create` command toocreate a resource group, as shown in hello following code snippet.</span></span> <span data-ttu-id="5409b-187">Zwróć uwagę, hello dane wyjściowe polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="5409b-187">Notice hello output of hello command.</span></span> <span data-ttu-id="5409b-188">Lista Hello wyświetlana po danych wyjściowych hello wyjaśniono hello parametry używane.</span><span class="sxs-lookup"><span data-stu-id="5409b-188">hello list shown after hello output explains hello parameters used.</span></span> <span data-ttu-id="5409b-189">Aby uzyskać więcej informacji na temat grup zasobów, zobacz temat [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5409b-189">For more information about resource groups, visit [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    ```azurecli
    az group create --location westus --name appgatewayRG
    ```
    
    <span data-ttu-id="5409b-190">**-n (lub --name)**.</span><span class="sxs-lookup"><span data-stu-id="5409b-190">**-n (or --name)**.</span></span> <span data-ttu-id="5409b-191">Nazwa nowej grupy zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="5409b-191">Name for hello new resource group.</span></span> <span data-ttu-id="5409b-192">W naszym scenariuszu jest to *appgatewayRG*.</span><span class="sxs-lookup"><span data-stu-id="5409b-192">For our scenario, it's *appgatewayRG*.</span></span>
    
    <span data-ttu-id="5409b-193">**-l (lub --location)**.</span><span class="sxs-lookup"><span data-stu-id="5409b-193">**-l (or --location)**.</span></span> <span data-ttu-id="5409b-194">Region platformy Azure, w której jest tworzony hello nową grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="5409b-194">Azure region where hello new resource group is created.</span></span> <span data-ttu-id="5409b-195">W naszym scenariuszu ma *westus*.</span><span class="sxs-lookup"><span data-stu-id="5409b-195">For our scenario, it's *westus*.</span></span>

1. <span data-ttu-id="5409b-196">Uruchom hello `az group deployment create` polecenia cmdlet toodeploy hello nową sieć wirtualną przy użyciu szablonu hello i parametr pliki uprzednio pobranego i modyfikować w hello poprzedzających krok.</span><span class="sxs-lookup"><span data-stu-id="5409b-196">Run hello `az group deployment create` cmdlet toodeploy hello new virtual network by using hello template and parameter files you downloaded and modified in hello preceding step.</span></span> <span data-ttu-id="5409b-197">Lista Hello wyświetlana po danych wyjściowych hello wyjaśniono hello parametry używane.</span><span class="sxs-lookup"><span data-stu-id="5409b-197">hello list shown after hello output explains hello parameters used.</span></span>

    ```azurecli
    az group deployment create --resource-group appgatewayRG --name TestAppgatewayDeployment --template-file azuredeploy.json --parameters @azuredeploy-parameters.json
    ```

## <a name="deploy-hello-azure-resource-manager-template-by-using-click-to-deploy"></a><span data-ttu-id="5409b-198">Wdrażanie szablonu usługi Azure Resource Manager hello przy użyciu kliknij wdrażania</span><span class="sxs-lookup"><span data-stu-id="5409b-198">Deploy hello Azure Resource Manager template by using click-to-deploy</span></span>

<span data-ttu-id="5409b-199">Kliknij przycisk deploy jest inny sposób toouse szablonów usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5409b-199">Click-to-deploy is another way toouse Azure Resource Manager templates.</span></span> <span data-ttu-id="5409b-200">Jest łatwy sposób szablonów toouse hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="5409b-200">It's an easy way toouse templates with hello Azure portal.</span></span>

1. <span data-ttu-id="5409b-201">Przejdź za[Utwórz bramę aplikacji z zapory aplikacji sieci web](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/).</span><span class="sxs-lookup"><span data-stu-id="5409b-201">Go too[Create an application gateway with web application firewall](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/).</span></span>

1. <span data-ttu-id="5409b-202">Kliknij przycisk **wdrażanie tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="5409b-202">Click **Deploy tooAzure**.</span></span>

    ![Wdrażanie tooAzure](./media/application-gateway-create-gateway-arm-template/deploytoazure.png)
    
1. <span data-ttu-id="5409b-204">Wypełnianie hello parametrów hello Szablon wdrożenia na powitania portalu, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="5409b-204">Fill out hello parameters for hello deployment template on hello portal and click **OK**.</span></span>

    ![Parametry](./media/application-gateway-create-gateway-arm-template/ibiza1.png)
    
1. <span data-ttu-id="5409b-206">Wybierz **zgadzam się toohello warunki i postanowienia, o których wspomniano** i kliknij przycisk **zakupu**.</span><span class="sxs-lookup"><span data-stu-id="5409b-206">Select **I agree toohello terms and conditions stated above** and click **Purchase**.</span></span>

1. <span data-ttu-id="5409b-207">W bloku wdrożenia niestandardowe hello, kliknij polecenie **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="5409b-207">On hello Custom deployment blade, click **Create**.</span></span>

## <a name="providing-certificate-data-tooresource-manager-templates"></a><span data-ttu-id="5409b-208">Udostępnia szablony Menedżera tooResource dane certyfikatu</span><span class="sxs-lookup"><span data-stu-id="5409b-208">Providing certificate data tooResource Manager templates</span></span>

<span data-ttu-id="5409b-209">Przy korzystaniu z protokołu SSL przy użyciu szablonu certyfikatu hello musi toobe dostarczone w parametrach base64, zamiast przekazywanego.</span><span class="sxs-lookup"><span data-stu-id="5409b-209">When using SSL with a template, hello certificate needs toobe provided in a base64 string instead of being uploaded.</span></span> <span data-ttu-id="5409b-210">ciąg base64 tooa pfx lub .cer tooconvert użyj jednej z hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="5409b-210">tooconvert a .pfx or .cer tooa base64 string use one of hello following commands.</span></span> <span data-ttu-id="5409b-211">Witaj następujące polecenia przekonwertować ciąg base64 tooa certyfikatu hello, który można podać toohello szablonu.</span><span class="sxs-lookup"><span data-stu-id="5409b-211">hello following commands convert hello certificate tooa base64 string, which can be provided toohello template.</span></span> <span data-ttu-id="5409b-212">Witaj oczekiwanych danych wyjściowych jest ciągiem, który może być przechowywana w zmiennej i wkleić w szablonie hello.</span><span class="sxs-lookup"><span data-stu-id="5409b-212">hello expected output is a string that can be stored in a variable and pasted in hello template.</span></span>

### <a name="macos"></a><span data-ttu-id="5409b-213">macOS</span><span class="sxs-lookup"><span data-stu-id="5409b-213">macOS</span></span>
```bash
cert=$( base64 <certificate path and name>.pfx )
echo $cert
```

### <a name="windows"></a><span data-ttu-id="5409b-214">Windows</span><span class="sxs-lookup"><span data-stu-id="5409b-214">Windows</span></span>
```powershell
[System.Convert]::ToBase64String([System.IO.File]::ReadAllBytes("<certificate path and name>.pfx"))
```

## <a name="delete-all-resources"></a><span data-ttu-id="5409b-215">Usuwanie wszystkich zasobów</span><span class="sxs-lookup"><span data-stu-id="5409b-215">Delete all resources</span></span>

<span data-ttu-id="5409b-216">toodelete wszystkie zasoby są tworzone w tym artykule pełną spośród hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="5409b-216">toodelete all resources created in this article, complete one of hello following steps:</span></span>

### <a name="powershell"></a><span data-ttu-id="5409b-217">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5409b-217">PowerShell</span></span>

```powershell
Remove-AzureRmResourceGroup -Name appgatewayRG
```

### <a name="azure-cli"></a><span data-ttu-id="5409b-218">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="5409b-218">Azure CLI</span></span>

```azurecli
az group delete --name appgatewayRG
```

## <a name="next-steps"></a><span data-ttu-id="5409b-219">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5409b-219">Next steps</span></span>

<span data-ttu-id="5409b-220">Jeśli chcesz tooconfigure odciążanie protokołu SSL można znaleźć: [skonfigurować bramę aplikacji dla odciążania SSL](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="5409b-220">If you want tooconfigure SSL offload, visit: [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="5409b-221">Jeśli chcesz tooconfigure toouse bramy aplikacji z wewnętrznego modułu równoważenia obciążenia, odwiedź stronę: [Utwórz bramę aplikacji z wewnętrznego modułu równoważenia obciążenia (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="5409b-221">If you want tooconfigure an application gateway toouse with an internal load balancer, visit: [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="5409b-222">Więcej ogólnych informacji na temat opcji równoważenia obciążenia możesz znaleźć, odwiedzając:</span><span class="sxs-lookup"><span data-stu-id="5409b-222">If you want more information about load balancing options in general, visit:</span></span>

* [<span data-ttu-id="5409b-223">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="5409b-223">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="5409b-224">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="5409b-224">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

