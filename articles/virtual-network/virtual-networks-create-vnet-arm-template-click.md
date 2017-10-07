---
title: "aaaCreate sieci wirtualnej | Szablonu usługi Azure Resource Manager | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate a wirtualnych sieci za pomocą szablonu usługi Azure Resource Manager."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 69530861-2f97-4a6e-b336-a7baf2690044
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b9c289433ff2a84bec19eac25fa28ab40d131c7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-an-azure-resource-manager-template"></a><span data-ttu-id="89eb7-103">Utwórz sieć wirtualną przy użyciu szablonu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="89eb7-103">Create a virtual network using an Azure Resource Manager template</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="89eb7-104">Platforma Azure ma dwa modele wdrażania: usługa Azure Resource Manager i wersja klasyczna.</span><span class="sxs-lookup"><span data-stu-id="89eb7-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="89eb7-105">Firma Microsoft zaleca utworzenie zasobów za pośrednictwem modelu wdrażania usługi Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="89eb7-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="89eb7-106">więcej informacji o toolearn hello różnice między modelami hello dwa odczytu hello [modele wdrażania zrozumieć Azure](../azure-resource-manager/resource-manager-deployment-model.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="89eb7-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>
 
<span data-ttu-id="89eb7-107">W tym artykule opisano, jak toocreate sieci wirtualnej przez wdrożenie usługi Resource Manager hello modelu przy użyciu szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="89eb7-107">This article explains how toocreate a VNet through hello Resource Manager deployment model using an Azure Resource Manager template.</span></span> <span data-ttu-id="89eb7-108">Możesz również utworzyć sieć wirtualną za pomocą Menedżera zasobów przy użyciu innych narzędzi lub utworzyć sieć wirtualną przy użyciu hello klasycznego modelu wdrażania, wybierając inną opcję z hello następującej listy:</span><span class="sxs-lookup"><span data-stu-id="89eb7-108">You can also create a VNet through Resource Manager using other tools or create a VNet through hello classic deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
- [<span data-ttu-id="89eb7-109">Portal</span><span class="sxs-lookup"><span data-stu-id="89eb7-109">Portal</span></span>](virtual-networks-create-vnet-arm-pportal.md)
- [<span data-ttu-id="89eb7-110">Program PowerShell</span><span class="sxs-lookup"><span data-stu-id="89eb7-110">PowerShell</span></span>](virtual-networks-create-vnet-arm-ps.md)
- [<span data-ttu-id="89eb7-111">Interfejs wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="89eb7-111">CLI</span></span>](virtual-networks-create-vnet-arm-cli.md)
- [<span data-ttu-id="89eb7-112">Szablon</span><span class="sxs-lookup"><span data-stu-id="89eb7-112">Template</span></span>](virtual-networks-create-vnet-arm-template-click.md)
- [<span data-ttu-id="89eb7-113">Portal (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="89eb7-113">Portal (Classic)</span></span>](virtual-networks-create-vnet-classic-pportal.md)
- [<span data-ttu-id="89eb7-114">PowerShell (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="89eb7-114">PowerShell (Classic)</span></span>](virtual-networks-create-vnet-classic-netcfg-ps.md)
- [<span data-ttu-id="89eb7-115">Interfejs wiersza polecenia (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="89eb7-115">CLI (Classic)</span></span>](virtual-networks-create-vnet-classic-cli.md)

<span data-ttu-id="89eb7-116">Dowiesz się jak toodownload i zmodyfikować istniejący szablon ARM z serwisu GitHub i wdrażanie hello szablonu z serwisu GitHub, programu PowerShell i hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="89eb7-116">You will learn how toodownload and modify and existing ARM template from GitHub, and deploy hello template from GitHub, PowerShell, and hello Azure CLI.</span></span>

<span data-ttu-id="89eb7-117">Jeśli po prostu wdrażasz szablon ARM hello bezpośrednio z serwisu GitHub, bez wprowadzania żadnych zmian, Pomiń zbyt[wdrażania szablonu z serwisu github](#deploy-the-arm-template-by-using-click-to-deploy).</span><span class="sxs-lookup"><span data-stu-id="89eb7-117">If you are simply deploying hello ARM template directly from GitHub, without any changes, skip too[deploy a template from github](#deploy-the-arm-template-by-using-click-to-deploy).</span></span>

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="download-and-understand-hello-azure-resource-manager-template"></a><span data-ttu-id="89eb7-118">Pobierz i zrozumieć hello szablonu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="89eb7-118">Download and understand hello Azure Resource Manager template</span></span>
<span data-ttu-id="89eb7-119">Można pobrać hello istniejący szablon do tworzenia sieci wirtualnej z dwoma podsieciami z serwisu GitHub, zmiany mogą, a następnie użyć go ponownie.</span><span class="sxs-lookup"><span data-stu-id="89eb7-119">You can download hello existing template for creating a VNet and two subnets from GitHub, make any changes you might want, and reuse it.</span></span> <span data-ttu-id="89eb7-120">toodo tak, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="89eb7-120">toodo so, complete hello following steps:</span></span>

1. <span data-ttu-id="89eb7-121">Przejdź za[hello przykładowy szablon strony](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span><span class="sxs-lookup"><span data-stu-id="89eb7-121">Navigate too[hello sample template page](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span></span>
2. <span data-ttu-id="89eb7-122">Kliknij opcję **azuredeploy.json**, a następnie kliknij opcję **RAW**.</span><span class="sxs-lookup"><span data-stu-id="89eb7-122">Click **azuredeploy.json**, and then click **RAW**.</span></span>
3. <span data-ttu-id="89eb7-123">Zapisz hello tooa pliku lokalnego folderu na komputerze.</span><span class="sxs-lookup"><span data-stu-id="89eb7-123">Save hello file tooa a local folder on your computer.</span></span>
4. <span data-ttu-id="89eb7-124">Jeśli znasz szablony, Pomiń toostep 7.</span><span class="sxs-lookup"><span data-stu-id="89eb7-124">If you are familiar with templates, skip toostep 7.</span></span>
5. <span data-ttu-id="89eb7-125">Otwórz zapisany plik hello i przyjrzyj się zawartości hello w obszarze **parametry** w wierszu 5.</span><span class="sxs-lookup"><span data-stu-id="89eb7-125">Open hello file you just saved and look at hello contents under **parameters** in line 5.</span></span> <span data-ttu-id="89eb7-126">Parametry szablonu ARM zawierają symbole zastępcze wartości, które mogą zostać wypełnione podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="89eb7-126">ARM template parameters provide a placeholder for values that can be filled out during deployment.</span></span>
   
   | <span data-ttu-id="89eb7-127">Parametr</span><span class="sxs-lookup"><span data-stu-id="89eb7-127">Parameter</span></span> | <span data-ttu-id="89eb7-128">Opis</span><span class="sxs-lookup"><span data-stu-id="89eb7-128">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="89eb7-129">**location**</span><span class="sxs-lookup"><span data-stu-id="89eb7-129">**location**</span></span> |<span data-ttu-id="89eb7-130">Region platformy Azure, w której zostanie utworzona hello sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="89eb7-130">Azure region where hello VNet will be created</span></span> |
   | <span data-ttu-id="89eb7-131">**vnetName**</span><span class="sxs-lookup"><span data-stu-id="89eb7-131">**vnetName**</span></span> |<span data-ttu-id="89eb7-132">Nazwa hello nowej sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="89eb7-132">Name for hello new VNet</span></span> |
   | <span data-ttu-id="89eb7-133">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="89eb7-133">**addressPrefix**</span></span> |<span data-ttu-id="89eb7-134">Przestrzeń adresowa hello sieci wirtualnej, w formacie CIDR</span><span class="sxs-lookup"><span data-stu-id="89eb7-134">Address space for hello VNet, in CIDR format</span></span> |
   | <span data-ttu-id="89eb7-135">**subnet1Name**</span><span class="sxs-lookup"><span data-stu-id="89eb7-135">**subnet1Name**</span></span> |<span data-ttu-id="89eb7-136">Nazwa hello pierwszej sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="89eb7-136">Name for hello first VNet</span></span> |
   | <span data-ttu-id="89eb7-137">**subnet1Prefix**</span><span class="sxs-lookup"><span data-stu-id="89eb7-137">**subnet1Prefix**</span></span> |<span data-ttu-id="89eb7-138">Blok CIDR pierwszej podsieci hello</span><span class="sxs-lookup"><span data-stu-id="89eb7-138">CIDR block for hello first subnet</span></span> |
   | <span data-ttu-id="89eb7-139">**subnet2Name**</span><span class="sxs-lookup"><span data-stu-id="89eb7-139">**subnet2Name**</span></span> |<span data-ttu-id="89eb7-140">Nazwa hello drugiej sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="89eb7-140">Name for hello second VNet</span></span> |
   | <span data-ttu-id="89eb7-141">**subnet2Prefix**</span><span class="sxs-lookup"><span data-stu-id="89eb7-141">**subnet2Prefix**</span></span> |<span data-ttu-id="89eb7-142">Blok CIDR drugiej podsieci hello</span><span class="sxs-lookup"><span data-stu-id="89eb7-142">CIDR block for hello second subnet</span></span> |
   
   > [!IMPORTANT]
   > <span data-ttu-id="89eb7-143">Szablony usługi Azure Resource Manger utrzymywane w usłudze GitHub mogą z upływem czasu ulec zmianie.</span><span class="sxs-lookup"><span data-stu-id="89eb7-143">Azure Resource Manager templates maintained in GitHub can change over time.</span></span> <span data-ttu-id="89eb7-144">Upewnij się, że sprawdzanie hello szablon przed jego użyciem.</span><span class="sxs-lookup"><span data-stu-id="89eb7-144">Make sure you check hello template before using it.</span></span>
   > 
   > 
6. <span data-ttu-id="89eb7-145">Sprawdź zawartość hello w obszarze **zasobów** i zwróć uwagę, hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="89eb7-145">Check hello content under **resources** and notice hello following:</span></span>
   
   * <span data-ttu-id="89eb7-146">**type**.</span><span class="sxs-lookup"><span data-stu-id="89eb7-146">**type**.</span></span> <span data-ttu-id="89eb7-147">Typ zasobu tworzonego przez szablon hello.</span><span class="sxs-lookup"><span data-stu-id="89eb7-147">Type of resource being created by hello template.</span></span> <span data-ttu-id="89eb7-148">W tym przypadku jest to **Microsoft.Network/virtualNetworks** reprezentujący sieć wirtualną.</span><span class="sxs-lookup"><span data-stu-id="89eb7-148">In this case, **Microsoft.Network/virtualNetworks**, which represent a VNet.</span></span>
   * <span data-ttu-id="89eb7-149">**name**.</span><span class="sxs-lookup"><span data-stu-id="89eb7-149">**name**.</span></span> <span data-ttu-id="89eb7-150">Nazwa zasobu hello.</span><span class="sxs-lookup"><span data-stu-id="89eb7-150">Name for hello resource.</span></span> <span data-ttu-id="89eb7-151">Użycie hello powiadomienia **[parameters('vnetName')]**, która oznacza hello nazwa zostanie podana jako dane wejściowe użytkownika hello lub pliku parametrów podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="89eb7-151">Notice hello use of **[parameters('vnetName')]**, which means hello name will provided as input by hello user or a parameter file during deployment.</span></span>
   * <span data-ttu-id="89eb7-152">**properties**.</span><span class="sxs-lookup"><span data-stu-id="89eb7-152">**properties**.</span></span> <span data-ttu-id="89eb7-153">Lista właściwości zasobu hello.</span><span class="sxs-lookup"><span data-stu-id="89eb7-153">List of properties for hello resource.</span></span> <span data-ttu-id="89eb7-154">Ten szablon używa właściwości adresu hello miejsca i podsieci podczas tworzenia sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="89eb7-154">This template uses hello address space and subnet properties during VNet creation.</span></span>
7. <span data-ttu-id="89eb7-155">Przejdź wstecz zbyt[hello przykładowy szablon strony](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span><span class="sxs-lookup"><span data-stu-id="89eb7-155">Navigate back too[hello sample template page](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span></span>
8. <span data-ttu-id="89eb7-156">Kliknij opcję **azuredeploy-paremeters.json**, a następnie kliknij opcję **RAW**.</span><span class="sxs-lookup"><span data-stu-id="89eb7-156">Click **azuredeploy-paremeters.json**, and then click **RAW**.</span></span>
9. <span data-ttu-id="89eb7-157">Zapisz hello tooa pliku lokalnego folderu na komputerze.</span><span class="sxs-lookup"><span data-stu-id="89eb7-157">Save hello file tooa a local folder on your computer.</span></span>
10. <span data-ttu-id="89eb7-158">Otwórz plik hello, zapisany i edytować hello wartości parametrów hello.</span><span class="sxs-lookup"><span data-stu-id="89eb7-158">Open hello file you just saved and edit hello values for hello parameters.</span></span> <span data-ttu-id="89eb7-159">Użyj hello następujące wartości poniżej hello toodeploy opisany w scenariuszu hello sieci wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="89eb7-159">Use hello following values below toodeploy hello VNet described in hello scenario:</span></span>

    ```json
        {
          "location": {
            "value": "Central US"
          },
          "vnetName": {
              "value": "TestVNet"
          },
          "addressPrefix": {
              "value": "192.168.0.0/16"
          },
          "subnet1Name": {
              "value": "FrontEnd"
          },
          "subnet1Prefix": {
            "value": "192.168.1.0/24"
          },
          "subnet2Name": {
              "value": "BackEnd"
          },
          "subnet2Prefix": {
              "value": "192.168.2.0/24"
          }
        }
    ```

11. <span data-ttu-id="89eb7-160">Zapisz plik hello.</span><span class="sxs-lookup"><span data-stu-id="89eb7-160">Save hello file.</span></span>


## <a name="deploy-hello-template-using-powershell"></a><span data-ttu-id="89eb7-161">Wdrażanie szablonu hello przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="89eb7-161">Deploy hello template using PowerShell</span></span>

<span data-ttu-id="89eb7-162">Wykonaj następujące kroki toodeploy hello szablon, który został pobrany przy użyciu programu PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="89eb7-162">Complete hello following steps toodeploy hello template you downloaded by using PowerShell:</span></span>

1. <span data-ttu-id="89eb7-163">Instalowanie i konfigurowanie programu Azure PowerShell, wykonując kroki hello hello [jak tooInstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) artykułu.</span><span class="sxs-lookup"><span data-stu-id="89eb7-163">Install and configure Azure PowerShell by completing hello steps in hello [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="89eb7-164">Uruchom następujące polecenie toocreate hello nową grupę zasobów:</span><span class="sxs-lookup"><span data-stu-id="89eb7-164">Run hello following command toocreate a new resource group:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    <span data-ttu-id="89eb7-165">polecenie Hello tworzy grupę zasobów o nazwie *TestRG* w hello *środkowe stany USA* region platformy azure.</span><span class="sxs-lookup"><span data-stu-id="89eb7-165">hello command creates a resource group named *TestRG* in hello *Central US* azure region.</span></span> <span data-ttu-id="89eb7-166">Aby uzyskać więcej informacji na temat grup zasobów, zobacz temat [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="89eb7-166">For more information about resource groups, visit [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    <span data-ttu-id="89eb7-167">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="89eb7-167">Expected output:</span></span>

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/[Id]/resourceGroups/TestRG

3. <span data-ttu-id="89eb7-168">Uruchom następujące polecenie toodeploy hello nowej sieci wirtualnej przy użyciu hello szablon i parametr plików pobranego i zmodyfikowanego hello:</span><span class="sxs-lookup"><span data-stu-id="89eb7-168">Run hello following command toodeploy hello new VNet using hello template and parameter files you downloaded and modified above:</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestVNetDeployment -ResourceGroupName TestRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

    <span data-ttu-id="89eb7-169">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="89eb7-169">Expected output:</span></span>
   
        DeploymentName    : TestVNetDeployment
        ResourceGroupName : TestRG
        ProvisioningState : Succeeded
        Timestamp         : [Date and time]
        Mode              : Incremental
        TemplateLink      :
        Parameters        :
                            Name             Type                       Value
                            ===============  =========================  ==========
                            location         String                     Central US
                            vnetName         String                     TestVNet
                            addressPrefix    String                     192.168.0.0/16
                            subnet1Prefix    String                     192.168.1.0/24
                            subnet1Name      String                     FrontEnd
                            subnet2Prefix    String                     192.168.2.0/24
                            subnet2Name      String                     BackEnd
   
        Outputs           :
4. <span data-ttu-id="89eb7-170">Witaj uruchom następujące polecenie Właściwości hello tooview hello nowej sieci wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="89eb7-170">Run hello following command tooview hello properties of hello new VNet:</span></span>

    ```powershell
    Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

    <span data-ttu-id="89eb7-171">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="89eb7-171">Expected output:</span></span>

        Name              : TestVNet
        ResourceGroupName : TestRG
        Location          : centralus
        Id                : /subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag              : W/"[Id]"
        ProvisioningState : Succeeded
        Tags              :
        AddressSpace      : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptions       : {
                              "DnsServers": null
                            }
        NetworkInterfaces : null
        Subnets           : [
                              {
                                "Name": "FrontEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                "AddressPrefix": "192.168.1.0/24",
                                "IpConfigurations": [],
                                "NetworkSecurityGroup": null,
                                "RouteTable": null,
                                "ProvisioningState": "Succeeded"
                              },
                              {
                                "Name": "BackEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                                "AddressPrefix": "192.168.2.0/24",
                                "IpConfigurations": [],
                                "NetworkSecurityGroup": null,
                                "RouteTable": null,
                                "ProvisioningState": "Succeeded"
                              }
                            ]

## <a name="deploy-hello-template-using-click-to-deploy"></a><span data-ttu-id="89eb7-172">Wdrażanie szablonu hello przy użyciu kliknij wdrażania</span><span class="sxs-lookup"><span data-stu-id="89eb7-172">Deploy hello template using click-to-deploy</span></span>

<span data-ttu-id="89eb7-173">Można ponownie użyć wstępnie zdefiniowanych usługi Azure Resource Manager szablony przekazane tooa repozytorium GitHub obsługiwane przez firmę Microsoft i otwórz toohello społeczności.</span><span class="sxs-lookup"><span data-stu-id="89eb7-173">You can reuse pre-defined Azure Resource Manager templates uploaded tooa GitHub repository maintained by Microsoft and open toohello community.</span></span> <span data-ttu-id="89eb7-174">Te szablony można wdrożyć bezpośrednio z witryny GitHub, lub pobrać i zmodyfikować toofit potrzeb.</span><span class="sxs-lookup"><span data-stu-id="89eb7-174">These templates can be deployed straight out of GitHub, or downloaded and modified toofit your needs.</span></span> <span data-ttu-id="89eb7-175">toodeploy szablon, który pozwala utworzyć sieć wirtualną z dwiema podsieciami, pełną hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="89eb7-175">toodeploy a template that creates a VNet with two subnets, complete hello following steps:</span></span>

1. <span data-ttu-id="89eb7-176">W przeglądarce Przejdź zbyt[https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="89eb7-176">From a browser, navigate too[https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span>
2. <span data-ttu-id="89eb7-177">Przewiń w dół listę szablonów hello, a następnie kliknij przycisk **101-vnet-two-subnets**.</span><span class="sxs-lookup"><span data-stu-id="89eb7-177">Scroll down hello list of templates, and click **101-vnet-two-subnets**.</span></span> <span data-ttu-id="89eb7-178">Sprawdź hello **README.md** plików, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="89eb7-178">Check hello **README.md** file, as shown below.</span></span>

    ![Plik READEME.md w witrynie github](./media/virtual-networks-create-vnet-arm-template-click-include/figure1.png)

3. <span data-ttu-id="89eb7-180">Kliknij przycisk **wdrażanie tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="89eb7-180">Click **Deploy tooAzure**.</span></span> <span data-ttu-id="89eb7-181">W razie potrzeby wprowadź poświadczenia logowania do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="89eb7-181">If necessary, enter your Azure login credentials.</span></span> 
4. <span data-ttu-id="89eb7-182">W hello **parametry** bloku, wprowadź wartości hello mają toouse toocreate nowej sieci wirtualnej, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="89eb7-182">In hello **Parameters** blade, enter hello values you want toouse toocreate your new VNet, and then click **OK**.</span></span> <span data-ttu-id="89eb7-183">Witaj poniższej ilustracji przedstawiono hello wartości dla scenariusza hello:</span><span class="sxs-lookup"><span data-stu-id="89eb7-183">hello following figure shows hello values for hello scenario:</span></span>
   
    ![Parametry szablonu ARM](./media/virtual-networks-create-vnet-arm-template-click-include/figure2.png)

5. <span data-ttu-id="89eb7-185">Kliknij przycisk **grupy zasobów** i wybrać hello sieci wirtualnej do tooadd grupy zasobów, lub kliknij przycisk **Utwórz nowy** tooadd hello sieci wirtualnej tooa nową grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="89eb7-185">Click **Resource group** and select a resource group tooadd hello VNet to, or click **Create new** tooadd hello VNet tooa new resource group.</span></span> <span data-ttu-id="89eb7-186">Witaj przedstawiony na poniższym rysunku zasobów hello ustawienia grupy dla nowej grupy zasobów o nazwie **TestRG**:</span><span class="sxs-lookup"><span data-stu-id="89eb7-186">hello following figure shows hello resource group settings for a new resource group called **TestRG**:</span></span>

    ![Grupa zasobów](./media/virtual-networks-create-vnet-arm-template-click-include/figure3.png)

6. <span data-ttu-id="89eb7-188">W razie potrzeby zmień hello **subskrypcji** i **lokalizacji** ustawienia sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="89eb7-188">If necessary, change hello **Subscription** and **Location** settings for your VNet.</span></span>
7. <span data-ttu-id="89eb7-189">Jeśli nie chcesz hello toosee sieci wirtualnej jako Kafelek hello **tablicy startowej**, wyłącz **tooStartboard numeru Pin**.</span><span class="sxs-lookup"><span data-stu-id="89eb7-189">If you do not want toosee hello VNet as a tile in hello **Startboard**, disable **Pin tooStartboard**.</span></span>
8. <span data-ttu-id="89eb7-190">Kliknij przycisk **postanowienia prawne**, przeczytaj warunki hello i kliknij przycisk **kupić** tooagree.</span><span class="sxs-lookup"><span data-stu-id="89eb7-190">Click **Legal terms**, read hello terms, and click **Buy** tooagree.</span></span> 
9. <span data-ttu-id="89eb7-191">Kliknij przycisk **Utwórz** hello toocreate sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="89eb7-191">Click **Create** toocreate hello VNet.</span></span>
   
    ![Przesyłanie kafelka wdrażania w portalu w wersji zapoznawczej](./media/virtual-networks-create-vnet-arm-template-click-include/figure4.png)

10. <span data-ttu-id="89eb7-193">Po zakończeniu wdrażania hello w hello portalu Azure kliknij **więcej usług**, typ *sieci wirtualnych* hello filtru pojawi się okno, następnie kliknij przycisk wirtualnej sieci toosee hello wirtualnej sieci bloku.</span><span class="sxs-lookup"><span data-stu-id="89eb7-193">Once hello deployment is complete, in hello Azure portal click **More services**, type *virtual networks* in hello filter box that appears, then click Virtual networks toosee hello Virtual networks blade.</span></span> <span data-ttu-id="89eb7-194">W bloku powitania kliknij *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="89eb7-194">In hello blade, click *TestVNet*.</span></span> <span data-ttu-id="89eb7-195">W hello *TestVNet* bloku, kliknij przycisk **podsieci** toosee hello tworzone podsieci, jak pokazano na poniższej ilustracji hello:</span><span class="sxs-lookup"><span data-stu-id="89eb7-195">In hello *TestVNet* blade, click **Subnets** toosee hello created subnets, as shown in hello following picture:</span></span>
    
     ![Tworzenie sieci wirtualnej w portalu w wersji zapoznawczej](./media/virtual-networks-create-vnet-arm-template-click-include/figure5.png)

## <a name="next-steps"></a><span data-ttu-id="89eb7-197">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="89eb7-197">Next steps</span></span>

<span data-ttu-id="89eb7-198">Dowiedz się, jak tooconnect:</span><span class="sxs-lookup"><span data-stu-id="89eb7-198">Learn how tooconnect:</span></span>

- <span data-ttu-id="89eb7-199">Sieć wirtualną maszyny wirtualnej (VM) tooa za odczytywanie hello [utworzyć Maszynę wirtualną systemu Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md) lub [Utwórz Maszynę wirtualną systemu Linux](../virtual-machines/linux/quick-create-portal.md) artykułów.</span><span class="sxs-lookup"><span data-stu-id="89eb7-199">A virtual machine (VM) tooa virtual network by reading hello [Create a Windows VM](../virtual-machines/virtual-machines-windows-hero-tutorial.md) or [Create a Linux VM](../virtual-machines/linux/quick-create-portal.md) articles.</span></span> <span data-ttu-id="89eb7-200">Zamiast tworzenia sieci wirtualnej i podsieci w krokach hello hello artykułów, możesz wybrać istniejącej sieci wirtualnej i tooconnect podsieci maszyny Wirtualnej, aby.</span><span class="sxs-lookup"><span data-stu-id="89eb7-200">Instead of creating a VNet and subnet in hello steps of hello articles, you can select an existing VNet and subnet tooconnect a VM to.</span></span>
- <span data-ttu-id="89eb7-201">Witaj sieci wirtualne sieci wirtualnej tooother odczytując hello [połączyć sieci wirtualnych](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="89eb7-201">hello virtual network tooother virtual networks by reading hello [Connect VNets](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) article.</span></span>
- <span data-ttu-id="89eb7-202">Witaj sieci wirtualnej tooan sieci lokalnej za pomocą wirtualnej sieci prywatnej (VPN) do lokacji lub obwodu usługi expressroute.</span><span class="sxs-lookup"><span data-stu-id="89eb7-202">hello virtual network tooan on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="89eb7-203">Dowiedz się, jak odczytując hello [połączyć sieć lokalną tooan sieci wirtualnej przy użyciu sieci VPN lokacja lokacja](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) i [połączyć sieć wirtualną tooan obwodu ExpressRoute](../expressroute/expressroute-howto-linkvnet-arm.md) artykułów.</span><span class="sxs-lookup"><span data-stu-id="89eb7-203">Learn how by reading hello [Connect a VNet tooan on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet tooan ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-arm.md) articles.</span></span>
