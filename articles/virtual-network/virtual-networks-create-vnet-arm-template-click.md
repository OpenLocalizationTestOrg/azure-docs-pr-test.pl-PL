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
# <a name="create-a-virtual-network-using-an-azure-resource-manager-template"></a>Utwórz sieć wirtualną przy użyciu szablonu usługi Azure Resource Manager

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

Platforma Azure ma dwa modele wdrażania: usługa Azure Resource Manager i wersja klasyczna. Firma Microsoft zaleca utworzenie zasobów za pośrednictwem modelu wdrażania usługi Resource Manager hello. więcej informacji o toolearn hello różnice między modelami hello dwa odczytu hello [modele wdrażania zrozumieć Azure](../azure-resource-manager/resource-manager-deployment-model.md) artykułu.
 
W tym artykule opisano, jak toocreate sieci wirtualnej przez wdrożenie usługi Resource Manager hello modelu przy użyciu szablonu usługi Azure Resource Manager. Możesz również utworzyć sieć wirtualną za pomocą Menedżera zasobów przy użyciu innych narzędzi lub utworzyć sieć wirtualną przy użyciu hello klasycznego modelu wdrażania, wybierając inną opcję z hello następującej listy:

> [!div class="op_single_selector"]
- [Portal](virtual-networks-create-vnet-arm-pportal.md)
- [Program PowerShell](virtual-networks-create-vnet-arm-ps.md)
- [Interfejs wiersza polecenia](virtual-networks-create-vnet-arm-cli.md)
- [Szablon](virtual-networks-create-vnet-arm-template-click.md)
- [Portal (klasyczny)](virtual-networks-create-vnet-classic-pportal.md)
- [PowerShell (klasyczny)](virtual-networks-create-vnet-classic-netcfg-ps.md)
- [Interfejs wiersza polecenia (klasyczny)](virtual-networks-create-vnet-classic-cli.md)

Dowiesz się jak toodownload i zmodyfikować istniejący szablon ARM z serwisu GitHub i wdrażanie hello szablonu z serwisu GitHub, programu PowerShell i hello wiersza polecenia platformy Azure.

Jeśli po prostu wdrażasz szablon ARM hello bezpośrednio z serwisu GitHub, bez wprowadzania żadnych zmian, Pomiń zbyt[wdrażania szablonu z serwisu github](#deploy-the-arm-template-by-using-click-to-deploy).

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="download-and-understand-hello-azure-resource-manager-template"></a>Pobierz i zrozumieć hello szablonu usługi Azure Resource Manager
Można pobrać hello istniejący szablon do tworzenia sieci wirtualnej z dwoma podsieciami z serwisu GitHub, zmiany mogą, a następnie użyć go ponownie. toodo tak, wykonaj następujące kroki hello:

1. Przejdź za[hello przykładowy szablon strony](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).
2. Kliknij opcję **azuredeploy.json**, a następnie kliknij opcję **RAW**.
3. Zapisz hello tooa pliku lokalnego folderu na komputerze.
4. Jeśli znasz szablony, Pomiń toostep 7.
5. Otwórz zapisany plik hello i przyjrzyj się zawartości hello w obszarze **parametry** w wierszu 5. Parametry szablonu ARM zawierają symbole zastępcze wartości, które mogą zostać wypełnione podczas wdrażania.
   
   | Parametr | Opis |
   | --- | --- |
   | **location** |Region platformy Azure, w której zostanie utworzona hello sieci wirtualnej |
   | **vnetName** |Nazwa hello nowej sieci wirtualnej |
   | **addressPrefix** |Przestrzeń adresowa hello sieci wirtualnej, w formacie CIDR |
   | **subnet1Name** |Nazwa hello pierwszej sieci wirtualnej |
   | **subnet1Prefix** |Blok CIDR pierwszej podsieci hello |
   | **subnet2Name** |Nazwa hello drugiej sieci wirtualnej |
   | **subnet2Prefix** |Blok CIDR drugiej podsieci hello |
   
   > [!IMPORTANT]
   > Szablony usługi Azure Resource Manger utrzymywane w usłudze GitHub mogą z upływem czasu ulec zmianie. Upewnij się, że sprawdzanie hello szablon przed jego użyciem.
   > 
   > 
6. Sprawdź zawartość hello w obszarze **zasobów** i zwróć uwagę, hello poniżej:
   
   * **type**. Typ zasobu tworzonego przez szablon hello. W tym przypadku jest to **Microsoft.Network/virtualNetworks** reprezentujący sieć wirtualną.
   * **name**. Nazwa zasobu hello. Użycie hello powiadomienia **[parameters('vnetName')]**, która oznacza hello nazwa zostanie podana jako dane wejściowe użytkownika hello lub pliku parametrów podczas wdrażania.
   * **properties**. Lista właściwości zasobu hello. Ten szablon używa właściwości adresu hello miejsca i podsieci podczas tworzenia sieci wirtualnej.
7. Przejdź wstecz zbyt[hello przykładowy szablon strony](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).
8. Kliknij opcję **azuredeploy-paremeters.json**, a następnie kliknij opcję **RAW**.
9. Zapisz hello tooa pliku lokalnego folderu na komputerze.
10. Otwórz plik hello, zapisany i edytować hello wartości parametrów hello. Użyj hello następujące wartości poniżej hello toodeploy opisany w scenariuszu hello sieci wirtualnej:

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

11. Zapisz plik hello.


## <a name="deploy-hello-template-using-powershell"></a>Wdrażanie szablonu hello przy użyciu programu PowerShell

Wykonaj następujące kroki toodeploy hello szablon, który został pobrany przy użyciu programu PowerShell hello:

1. Instalowanie i konfigurowanie programu Azure PowerShell, wykonując kroki hello hello [jak tooInstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) artykułu.
2. Uruchom następujące polecenie toocreate hello nową grupę zasobów:

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    polecenie Hello tworzy grupę zasobów o nazwie *TestRG* w hello *środkowe stany USA* region platformy azure. Aby uzyskać więcej informacji na temat grup zasobów, zobacz temat [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).

    Oczekiwane dane wyjściowe:

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/[Id]/resourceGroups/TestRG

3. Uruchom następujące polecenie toodeploy hello nowej sieci wirtualnej przy użyciu hello szablon i parametr plików pobranego i zmodyfikowanego hello:

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestVNetDeployment -ResourceGroupName TestRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

    Oczekiwane dane wyjściowe:
   
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
4. Witaj uruchom następujące polecenie Właściwości hello tooview hello nowej sieci wirtualnej:

    ```powershell
    Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

    Oczekiwane dane wyjściowe:

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

## <a name="deploy-hello-template-using-click-to-deploy"></a>Wdrażanie szablonu hello przy użyciu kliknij wdrażania

Można ponownie użyć wstępnie zdefiniowanych usługi Azure Resource Manager szablony przekazane tooa repozytorium GitHub obsługiwane przez firmę Microsoft i otwórz toohello społeczności. Te szablony można wdrożyć bezpośrednio z witryny GitHub, lub pobrać i zmodyfikować toofit potrzeb. toodeploy szablon, który pozwala utworzyć sieć wirtualną z dwiema podsieciami, pełną hello następujące kroki:

1. W przeglądarce Przejdź zbyt[https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).
2. Przewiń w dół listę szablonów hello, a następnie kliknij przycisk **101-vnet-two-subnets**. Sprawdź hello **README.md** plików, jak pokazano poniżej.

    ![Plik READEME.md w witrynie github](./media/virtual-networks-create-vnet-arm-template-click-include/figure1.png)

3. Kliknij przycisk **wdrażanie tooAzure**. W razie potrzeby wprowadź poświadczenia logowania do platformy Azure. 
4. W hello **parametry** bloku, wprowadź wartości hello mają toouse toocreate nowej sieci wirtualnej, a następnie kliknij przycisk **OK**. Witaj poniższej ilustracji przedstawiono hello wartości dla scenariusza hello:
   
    ![Parametry szablonu ARM](./media/virtual-networks-create-vnet-arm-template-click-include/figure2.png)

5. Kliknij przycisk **grupy zasobów** i wybrać hello sieci wirtualnej do tooadd grupy zasobów, lub kliknij przycisk **Utwórz nowy** tooadd hello sieci wirtualnej tooa nową grupę zasobów. Witaj przedstawiony na poniższym rysunku zasobów hello ustawienia grupy dla nowej grupy zasobów o nazwie **TestRG**:

    ![Grupa zasobów](./media/virtual-networks-create-vnet-arm-template-click-include/figure3.png)

6. W razie potrzeby zmień hello **subskrypcji** i **lokalizacji** ustawienia sieci wirtualnej.
7. Jeśli nie chcesz hello toosee sieci wirtualnej jako Kafelek hello **tablicy startowej**, wyłącz **tooStartboard numeru Pin**.
8. Kliknij przycisk **postanowienia prawne**, przeczytaj warunki hello i kliknij przycisk **kupić** tooagree. 
9. Kliknij przycisk **Utwórz** hello toocreate sieci wirtualnej.
   
    ![Przesyłanie kafelka wdrażania w portalu w wersji zapoznawczej](./media/virtual-networks-create-vnet-arm-template-click-include/figure4.png)

10. Po zakończeniu wdrażania hello w hello portalu Azure kliknij **więcej usług**, typ *sieci wirtualnych* hello filtru pojawi się okno, następnie kliknij przycisk wirtualnej sieci toosee hello wirtualnej sieci bloku. W bloku powitania kliknij *TestVNet*. W hello *TestVNet* bloku, kliknij przycisk **podsieci** toosee hello tworzone podsieci, jak pokazano na poniższej ilustracji hello:
    
     ![Tworzenie sieci wirtualnej w portalu w wersji zapoznawczej](./media/virtual-networks-create-vnet-arm-template-click-include/figure5.png)

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak tooconnect:

- Sieć wirtualną maszyny wirtualnej (VM) tooa za odczytywanie hello [utworzyć Maszynę wirtualną systemu Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md) lub [Utwórz Maszynę wirtualną systemu Linux](../virtual-machines/linux/quick-create-portal.md) artykułów. Zamiast tworzenia sieci wirtualnej i podsieci w krokach hello hello artykułów, możesz wybrać istniejącej sieci wirtualnej i tooconnect podsieci maszyny Wirtualnej, aby.
- Witaj sieci wirtualne sieci wirtualnej tooother odczytując hello [połączyć sieci wirtualnych](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) artykułu.
- Witaj sieci wirtualnej tooan sieci lokalnej za pomocą wirtualnej sieci prywatnej (VPN) do lokacji lub obwodu usługi expressroute. Dowiedz się, jak odczytując hello [połączyć sieć lokalną tooan sieci wirtualnej przy użyciu sieci VPN lokacja lokacja](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) i [połączyć sieć wirtualną tooan obwodu ExpressRoute](../expressroute/expressroute-howto-linkvnet-arm.md) artykułów.
