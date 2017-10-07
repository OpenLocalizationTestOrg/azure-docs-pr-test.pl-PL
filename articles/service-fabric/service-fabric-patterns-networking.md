---
title: "wzorce aaaNetworking dla sieci szkieletowej usług Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano typowe wzorce sieciowych dla sieci szkieletowej usług i w jaki sposób toocreate klastra przy użyciu funkcji obsługi sieci platformy Azure."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/16/2017
ms.author: ryanwi
ms.openlocfilehash: 5973e3f9917076c6a36e71443ec256e0f414ff87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-networking-patterns"></a>Wzorce sieci sieci szkieletowej usług
Klaster sieci szkieletowej usług Azure można zintegrować z innymi funkcjami sieci platformy Azure. W tym artykule zostanie przedstawiony zostanie sposób toocreate klastrów tego hello Użyj następujących funkcji:

- [Istniejącej sieci wirtualnej lub podsieci](#existingvnet)
- [Statycznego publicznego adresu IP](#staticpublicip)
- [Moduł równoważenia obciążenia tylko do wewnętrznego](#internallb)
- [Moduł równoważenia obciążenia wewnętrznych i zewnętrznych](#internalexternallb)

Sieć szkieletowa usług jest uruchamiany w zestaw skali maszyny wirtualnej standardowego. Wszystkie funkcje są dostępne w zestawie skalowania maszyn wirtualnych, korzystania z klastra sieci szkieletowej usług. sekcje sieci Hello szablonów usługi Azure Resource Manager hello zestawy skalowania maszyny wirtualnej i sieci szkieletowej usług są identyczne. Po wdrożeniu tooan istniejącej sieci wirtualnej jest łatwe tooincorporate inne funkcje, takie jak usługa Azure ExpressRoute, Brama sieci VPN platformy Azure, sieciowej grupy zabezpieczeń i sieci wirtualnej komunikacji równorzędnej sieciowe.

Sieć szkieletowa usług to inaczej niż inne funkcje sieci w jednym aspekcie. Witaj [portalu Azure](https://portal.azure.com) wewnętrznie używa hello sieci szkieletowej usług zasobów dostawcy toocall tooa klastra tooget informacji o węzłach i aplikacji. Dostawca zasobów sieci szkieletowej usług Hello wymaga publicznie dostępu ruchu przychodzącego toohello HTTP bramy portu (domyślnie z portu 19080,) w punkcie końcowym zarządzania hello. [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) używa hello toomanage punkt końcowy zarządzania klastrem. Dostawca zasobów sieci szkieletowej usług Hello używa również port tooquery informacje o klastrze toodisplay w hello portalu Azure. 

Jeśli port 19080 nie jest dostępny od dostawcy zasobów usługi Service Fabric hello, takich jak wiadomość *węzłów nie można odnaleźć* jest wyświetlana w portalu hello i listy węzeł i aplikacja zostanie wyświetlona pusta. Jeśli chcesz toosee klastra w hello portalu Azure, moduł równoważenia obciążenia musi ujawniać publicznego adresu IP, a swojej grupy zabezpieczeń sieciowych muszą zezwalać na ruch przychodzący port 19080. Jeśli ustawienia nie spełnia te wymagania, hello portalu Azure nie wyświetla hello stan klastra.

## <a name="templates"></a>Szablony

Wszystkie szablony usługi sieć szkieletowa znajdują się w [jednego pobierania pliku](https://msdnshared.blob.core.windows.net/media/2016/10/SF_Networking_Templates.zip). Powinien być stanie toodeploy szablony hello jako — za pomocą następującego polecenia programu PowerShell hello. Jeśli wdrażasz hello istniejącego szablonu usługi Azure Virtual Network lub hello statycznego publicznego adresu IP szablonu, najpierw przeczytać artykuł hello [początkowej instalacji](#initialsetup) sekcji tego artykułu.

<a id="initialsetup"></a>
## <a name="initial-setup"></a>Początkowej konfiguracji

### <a name="existing-virtual-network"></a>Istniejącej sieci wirtualnej

W hello poniższy przykład, Rozpoczniemy z istniejącą siecią wirtualną o nazwie ExistingRG sieci wirtualnej, w hello **ExistingRG** grupy zasobów. podsieci Hello nosi nazwę domyślny. Tych domyślnych zasobów są tworzone, gdy używasz hello Azure toocreate portalu standardowe maszynę wirtualną (VM). Można utworzyć sieci wirtualnej hello i podsieć bez tworzenia hello maszyny Wirtualnej, ale hello głównym celem dodawania klastra tooan istniejącej sieci wirtualnej jest tooother łączności sieciowej tooprovide maszyn wirtualnych. Hello tworzenia maszyn wirtualnych zapewnia dobrym przykładem sposobu istniejącej sieci wirtualnej zwykle jest używana. Jeśli klaster sieci szkieletowej usług używa tylko do wewnętrznego modułu równoważenia obciążenia, bez publicznego adresu IP, możesz użyć hello maszyny Wirtualnej i jej publicznego adresu IP jako bezpieczny *skoku pole*.

### <a name="static-public-ip-address"></a>Statycznego publicznego adresu IP

Statycznego publicznego adresu IP jest zazwyczaj zasobów dedykowanych, zarządzanym oddzielnie z hello maszyny Wirtualnej lub jest przypisany do maszyn wirtualnych. Udostępniane w grupie zasobów sieciowych dedykowanych (jako tooin min. hello sieci szkieletowej usług grupa zasobów klastra sam). Tworzenie statycznego publicznego adresu IP o nazwie staticIP1 w hello tej samej grupie zasobów ExistingRG hello portalu Azure lub za pomocą programu PowerShell:

```powershell
PS C:\Users\user> New-AzureRmPublicIpAddress -Name staticIP1 -ResourceGroupName ExistingRG -Location westus -AllocationMethod Static -DomainNameLabel sfnetworking

Name                     : staticIP1
ResourceGroupName        : ExistingRG
Location                 : westus
Id                       : /subscriptions/1237f4d2-3dce-1236-ad95-123f764e7123/resourceGroups/ExistingRG/providers/Microsoft.Network/publicIPAddresses/staticIP1
Etag                     : W/"fc8b0c77-1f84-455d-9930-0404ebba1b64"
ResourceGuid             : 77c26c06-c0ae-496c-9231-b1a114e08824
ProvisioningState        : Succeeded
Tags                     :
PublicIpAllocationMethod : Static
IpAddress                : 40.83.182.110
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : null
DnsSettings              : {
                             "DomainNameLabel": "sfnetworking",
                             "Fqdn": "sfnetworking.westus.cloudapp.azure.com"
                           }
```

### <a name="service-fabric-template"></a>Szablon usługi sieć szkieletowa

W przykładach hello w tym artykule używamy hello template.json sieci szkieletowej usług. Można użyć hello standardowy kreator portalu toodownload hello szablonu z portalu hello, przed utworzeniem klastra. Można też użyć jednego z szablonów hello w hello [galerię szablonów](https://azure.microsoft.com/en-us/documentation/templates/?term=service+fabric), takich jak hello [pięcioma węzłami klastra sieci szkieletowej usług](https://azure.microsoft.com/en-us/documentation/templates/service-fabric-unsecure-cluster-5-node-1-nodetype/).

<a id="existingvnet"></a>
## <a name="existing-virtual-network-or-subnet"></a>Istniejącej sieci wirtualnej lub podsieci

1. Zmień nazwę toohello parametru podsieci hello hello istniejących podsieci, a następnie dodaj dwa nowe parametry tooreference hello istniejącej sieci wirtualnej:

    ```
        "subnet0Name": {
                "type": "string",
                "defaultValue": "default"
            },
            "existingVNetRGName": {
                "type": "string",
                "defaultValue": "ExistingRG"
            },

            "existingVNetName": {
                "type": "string",
                "defaultValue": "ExistingRG-vnet"
            },
            /*
            "subnet0Name": {
                "type": "string",
                "defaultValue": "Subnet-0"
            },
            "subnet0Prefix": {
                "type": "string",
                "defaultValue": "10.0.0.0/24"
            },*/
    ```


2. Zmień hello `vnetID` zmiennej toopoint toohello istniejącej sieci wirtualnej:

    ```
            /*old "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',parameters('virtualNetworkName'))]",*/
            "vnetID": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', parameters('existingVNetRGName'), '/providers/Microsoft.Network/virtualNetworks/', parameters('existingVNetName'))]",
    ```

3. Usuń `Microsoft.Network/virtualNetworks` z Twoich zasobów, dlatego Azure nie Utwórz nową sieć wirtualną:

    ```
    /*{
    "apiVersion": "[variables('vNetApiVersion')]",
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[parameters('virtualNetworkName')]",
    "location": "[parameters('computeLocation')]",
    "properities": {
        "addressSpace": {
            "addressPrefixes": [
                "[parameters('addressPrefix')]"
            ]
        },
        "subnets": [
            {
                "name": "[parameters('subnet0Name')]",
                "properties": {
                    "addressPrefix": "[parameters('subnet0Prefix')]"
                }
            }
        ]
    },
    "tags": {
        "resourceType": "Service Fabric",
        "clusterName": "[parameters('clusterName')]"
    }
    },*/
    ```

4. Komentarz hello sieci wirtualnej z hello `dependsOn` atrybutu `Microsoft.Compute/virtualMachineScaleSets`, więc nie zależą od tworzenia nowej sieci wirtualnej:

    ```
    "apiVersion": "[variables('vmssApiVersion')]",
    "type": "Microsoft.Computer/virtualMachineScaleSets",
    "name": "[parameters('vmNodeType0Name')]",
    "location": "[parameters('computeLocation')]",
    "dependsOn": [
        /*"[concat('Microsoft.Network/virtualNetworks/', parameters('virtualNetworkName'))]",
        */
        "[Concat('Microsoft.Storage/storageAccounts/', variables('uniqueStringArray0')[0])]",

    ```

5. Wdrażanie szablonu hello:

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkingexistingvnet -Location westus
    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkingexistingvnet -TemplateFile C:\SFSamples\Final\template\_existingvnet.json
    ```

    Po wdrożeniu sieci wirtualnej powinna zawierać hello nowego zestawu skalowania maszyny wirtualnej maszyny wirtualne. Typ węzła zestawu skali maszyny wirtualnej Hello powinny być widoczne hello istniejącej sieci wirtualnej i podsieci. Można również użyć protokołu RDP (Remote Desktop) tooaccess hello maszynę Wirtualną, która została już w sieci wirtualnej hello i tooping hello nowego zestawu skalowania maszyny wirtualnej maszyny wirtualne:

    ```
    C:>\Users\users>ping 10.0.0.5 -n 1
    C:>\Users\users>ping NOde1000000 -n 1
    ```

Na przykład innego, zobacz [, który nie jest określonym tooService sieci szkieletowej](https://github.com/gbowerman/azure-myriad/tree/master/existing-vnet).


<a id="staticpublicip"></a>
## <a name="static-public-ip-address"></a>Statycznego publicznego adresu IP

1. Dodaj parametry dla nazwy hello hello istniejące grupy zasobów w usłudze statycznego adresu IP, nazwa i Pełna nazwa domeny (FQDN):

    ```
    "existingStaticIPResourceGroup": {
                "type": "string"
            },
            "existingStaticIPName": {
                "type": "string"
            },
            "existingStaticIPDnsFQDN": {
                "type": "string"
    }
    ```

2. Usuń hello `dnsName` parametru. (hello statyczny adres IP już istnieje.)

    ```
    /*
    "dnsName": {
        "type": "string"
    },
    */
    ```

3. Dodawanie zmiennej tooreference hello istniejących statyczny adres IP:

    ```
    "existingStaticIP": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', parameters('existingStaticIPResourceGroup'), '/providers/Microsoft.Network/publicIPAddresses/', parameters('existingStaticIPName'))]",
    ```

4. Usuń `Microsoft.Network/publicIPAddresses` z Twoich zasobów, dlatego Azure nie Utwórz nowy adres IP:

    ```
    /*
    {
        "apiVersion": "[variables('publicIPApiVersion')]",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[concat(parameters('lbIPName'),)'-', '0')]",
        "location": "[parameters('computeLocation')]",
        "properties": {
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsName')]"
            },
            "publicIPAllocationMethod": "Dynamic"        
        },
        "tags": {
            "resourceType": "Service Fabric",
            "clusterName": "[parameters('clusterName')]"
        }
    }, */
    ```

5. Komentarz hello adresu IP z hello `dependsOn` atrybutu `Microsoft.Network/loadBalancers`, więc nie zależą od tworzenia nowego adresu IP:

    ```
    "apiVersion": "[variables('lbIPApiVersion')]",
    "type": "Microsoft.Network/loadBalancers",
    "name": "[concat('LB', '-', parameters('clusterName'), '-', parameters('vmNodeType0Name'))]",
    "location": "[parameters('computeLocation')]",
    /*
    "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', concat(parameters('lbIPName'), '-', '0'))]"
    ], */
    "properties": {
    ```

6. W hello `Microsoft.Network/loadBalancers` zasobów, zmień hello `publicIPAddress` elementu `frontendIPConfigurations` tooreference hello istniejących statyczny adres IP, zamiast nowo utworzone:

    ```
                "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                "publicIPAddress": {
                                    /*"id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"*/
                                    "id": "[variables('existingStaticIP')]"
                                }
                            }
                        }
                    ],
    ```

7. W hello `Microsoft.ServiceFabric/clusters` zasobów, zmień `managementEndpoint` toohello nazwy FQDN DNS hello statycznego adresu IP. Jeśli używane są bezpieczne klastra, upewnij się, możesz zmienić *http://* za*https://*. (Należy pamiętać, że ten krok ma zastosowanie tylko klastry tooService w sieci szkieletowej. Jeśli korzystasz z zestawu skalowania maszyn wirtualnych, Pomiń ten krok.)

    ```
                    "fabricSettings": [],
                    /*"managementEndpoint": "[concat('http://',reference(concat(parameters('lbIPName'),'-','0')).dnsSettings.fqdn,':',parameters('nt0fabricHttpGatewayPort'))]",*/
                    "managementEndpoint": "[concat('http://',parameters('existingStaticIPDnsFQDN'),':',parameters('nt0fabricHttpGatewayPort'))]",
    ```

8. Wdrażanie szablonu hello:

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkingstaticip -Location westus

    $staticip = Get-AzureRmPublicIpAddress -Name staticIP1 -ResourceGroupName ExistingRG

    $staticip

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkingstaticip -TemplateFile C:\SFSamples\Final\template\_staticip.json -existingStaticIPResourceGroup $staticip.ResourceGroupName -existingStaticIPName $staticip.Name -existingStaticIPDnsFQDN $staticip.DnsSettings.Fqdn
    ```

Po wdrożeniu widać, że moduł równoważenia obciążenia jest powiązane toohello publiczny statyczny adres IP z hello innej grupie zasobów. Witaj punktu końcowego połączenia klienta usługi Service Fabric i [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) toohello punktu końcowego nazwy FQDN DNS hello statycznego adresu IP.

<a id="internallb"></a>
## <a name="internal-only-load-balancer"></a>Moduł równoważenia obciążenia tylko do wewnętrznego

W tym scenariuszu zastępuje hello zewnętrznej usługi równoważenia obciążenia w szablonie usługi sieć szkieletowa domyślne hello usługi równoważenia obciążenia wewnętrznych. Aby uzyskać konsekwencje dla hello portalu Azure i dostawcy zasobów usługi Service Fabric hello Zobacz hello powyższej sekcji.

1. Usuń hello `dnsName` parametru. (Nie jest wymagana.)

    ```
    /*
    "dnsName": {
        "type": "string"
    },
    */
    ```

2. Opcjonalnie Jeśli używasz statyczną metodą przydziału, można dodać parametr statyczny adres IP. Jeśli używasz metody przydzielania, nie trzeba toodo ten krok.

    ```
            "internalLBAddress": {
                "type": "string",
                "defaultValue": "10.0.0.250"
            }
    ```

3. Usuń `Microsoft.Network/publicIPAddresses` z Twoich zasobów, dlatego Azure nie Utwórz nowy adres IP:

    ```
    /*
    {
        "apiVersion": "[variables('publicIPApiVersion')]",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[concat(parameters('lbIPName'),)'-', '0')]",
        "location": "[parameters('computeLocation')]",
        "properties": {
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsName')]"
            },
            "publicIPAllocationMethod": "Dynamic"        
        },
        "tags": {
            "resourceType": "Service Fabric",
            "clusterName": "[parameters('clusterName')]"
        }
    }, */
    ```

4. Usuń adres IP hello `dependsOn` atrybutu `Microsoft.Network/loadBalancers`, więc nie zależą od tworzenia nowego adresu IP. Dodawanie sieci wirtualnej hello `dependsOn` atrybutu, ponieważ moduł równoważenia obciążenia hello zależy od teraz hello podsieci z sieci wirtualnej hello:

    ```
                "apiVersion": "[variables('lbApiVersion')]",
                "type": "Microsoft.Network/loadBalancers",
                "name": "[concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'))]",
                "location": "[parameters('computeLocation')]",
                "dependsOn": [
                    /*"[concat('Microsoft.Network/publicIPAddresses/',concat(parameters('lbIPName'),'-','0'))]"*/
                    "[concat('Microsoft.Network/virtualNetworks/',parameters('virtualNetworkName'))]"
                ],
    ```

5. Zmień równoważenia obciążenia hello `frontendIPConfigurations` z przy użyciu `publicIPAddress`, toousing podsieci i `privateIPAddress`. `privateIPAddress`używa wstępnie zdefiniowanych statyczne wewnętrzne adresy IP. toouse dynamicznego adresu IP, Usuń hello `privateIPAddress` elementu, a następnie zmień `privateIPAllocationMethod` za**dynamiczne**.

    ```
                "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                /*
                                "publicIPAddress": {
                                    "id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"
                                } */
                                "subnet" :{
                                    "id": "[variables('subnet0Ref')]"
                                },
                                "privateIPAddress": "[parameters('internalLBAddress')]",
                                "privateIPAllocationMethod": "Static"
                            }
                        }
                    ],
    ```

6. W hello `Microsoft.ServiceFabric/clusters` zasobów, zmień `managementEndpoint` adres usługi równoważenia obciążenia wewnętrznego toohello toopoint. Jeśli używasz bezpiecznego klastra, upewnij się, można zmienić *http://* za*https://*. (Należy pamiętać, że ten krok ma zastosowanie tylko klastry tooService w sieci szkieletowej. Jeśli korzystasz z zestawu skalowania maszyn wirtualnych, Pomiń ten krok.)

    ```
                    "fabricSettings": [],
                    /*"managementEndpoint": "[concat('http://',reference(concat(parameters('lbIPName'),'-','0')).dnsSettings.fqdn,':',parameters('nt0fabricHttpGatewayPort'))]",*/
                    "managementEndpoint": "[concat('http://',reference(variables('lbID0')).frontEndIPConfigurations[0].properties.privateIPAddress,':',parameters('nt0fabricHttpGatewayPort'))]",
    ```

7. Wdrażanie szablonu hello:

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkinginternallb -Location westus

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkinginternallb -TemplateFile C:\SFSamples\Final\template\_internalonlyLB.json
    ```

Po wdrożeniu przez moduł równoważenia obciążenia używa hello 10.0.0.250 statycznego prywatnego adresu IP. Jeśli masz inną maszynę w tej samej sieci wirtualnej, można przejść toohello wewnętrzny [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) punktu końcowego. Uwaga łączy tooone węzłów hello za hello równoważenia obciążenia.

<a id="internalexternallb"></a>
## <a name="internal-and-external-load-balancer"></a>Moduł równoważenia obciążenia wewnętrznych i zewnętrznych

W tym scenariuszu zaczynać się hello istniejącego typu jednowęzłowej zewnętrznej usługi równoważenia obciążenia i dodać wewnętrznego modułu równoważenia obciążenia dla hello tego samego typu węzła. Pulę adresów zaplecza tooa portu zaplecza dołączony można przypisać tylko tooa jednego modułu równoważenia obciążenia. Wybierz, które usługa równoważenia obciążenia będzie miał porty Twojej aplikacji i które usługa równoważenia obciążenia mają zarządzania punktów końcowych (porty 19000 i 19080). Punkty końcowe zarządzania hello umieszczenie na powitania wewnętrznego modułu równoważenia obciążenia, należy przechowywać w uwadze hello zasobów sieci szkieletowej usług omówionych w artykule hello ograniczenia dostawcy. W przykładzie hello używanych punkty końcowe zarządzania hello pozostają na powitania zewnętrznej usługi równoważenia obciążenia. Możesz również dodać port 80 aplikacji portu i umieść ją na hello wewnętrznego modułu równoważenia obciążenia.

W klastrze typu węzła dwa jest jednego typu węzła na powitania zewnętrznej usługi równoważenia obciążenia. Witaj innego typu węzła znajduje się na powitania wewnętrznego modułu równoważenia obciążenia. toouse klastrze typu węzła dwa hello utworzonych przez portal dwóch węzłów typu szablonu (który pochodzi z dwóch usług równoważenia obciążenia), Przełącz hello drugi obciążenia równoważenia tooan wewnętrznego modułu równoważenia obciążenia. Aby uzyskać więcej informacji, zobacz hello [modułu równoważenia obciążenia tylko do wewnętrznego](#internallb) sekcji.

1. Dodaj parametr adres IP hello statyczna obciążenia wewnętrznego modułu równoważenia. (Aby uzyskać informacje o powiązanych toousing dynamicznego adresu IP, zobacz wcześniejszej części tego artykułu).

    ```
            "internalLBAddress": {
                "type": "string",
                "defaultValue": "10.0.0.250"
            }
    ```

2. Dodaj parametr port 80 aplikacji.

3. Wersje wewnętrzne tooadd hello istniejących sieci zmiennych, skopiuj i wklej je i Dodaj "-Int" Nazwa toohello:

    ```
    /* Add internal load balancer networking variables */
            "lbID0-Int": "[resourceId('Microsoft.Network/loadBalancers', concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'), '-Internal'))]",
            "lbIPConfig0-Int": "[concat(variables('lbID0-Int'),'/frontendIPConfigurations/LoadBalancerIPConfig')]",
            "lbPoolID0-Int": "[concat(variables('lbID0-Int'),'/backendAddressPools/LoadBalancerBEAddressPool')]",
            "lbProbeID0-Int": "[concat(variables('lbID0-Int'),'/probes/FabricGatewayProbe')]",
            "lbHttpProbeID0-Int": "[concat(variables('lbID0-Int'),'/probes/FabricHttpGatewayProbe')]",
            "lbNatPoolID0-Int": "[concat(variables('lbID0-Int'),'/inboundNatPools/LoadBalancerBEAddressNatPool')]",
            /* Internal load balancer networking variables end */
    ```

4. Jeśli na początku zasubskrybujesz generowanych przez portal szablonu hello, który korzysta z aplikacji portu 80, hello domyślnego szablonu portalu dodaje AppPort1 (port 80) na powitania zewnętrznej usługi równoważenia obciążenia. W takim przypadku usuń AppPort1 z hello zewnętrznej usługi równoważenia obciążenia `loadBalancingRules` i sond, dzięki czemu można je dodać toohello wewnętrznego modułu równoważenia obciążenia:

    ```
    "loadBalancingRules": [
        {
            "name": "LBHttpRule",
            "properties":{
                "backendAddressPool": {
                    "id": "[variables('lbPoolID0')]"
                },
                "backendPort": "[parameters('nt0fabricHttpGatewayPort')]",
                "enableFloatingIP": "false",
                "frontendIPConfiguration": {
                    "id": "[variables('lbIPConfig0')]"            
                },
                "frontendPort": "[parameters('nt0fabricHttpGatewayPort')]",
                "idleTimeoutInMinutes": "5",
                "probe": {
                    "id": "[variables('lbHttpProbeID0')]"
                },
                "protocol": "tcp"
            }
        } /* Remove AppPort1 from hello external load balancer.
        {
            "name": "AppPortLBRule1",
            "properties": {
                "backendAddressPool": {
                    "id": "[variables('lbPoolID0')]"
                },
                "backendPort": "[parameters('loadBalancedAppPort1')]",
                "enableFloatingIP": "false",
                "frontendIPConfiguration": {
                    "id": "[variables('lbIPConfig0')]"            
                },
                "frontendPort": "[parameters('loadBalancedAppPort1')]",
                "idleTimeoutInMinutes": "5",
                "probe": {
                    "id": "[concate(variables('lbID0'), '/probes/AppPortProbe1')]"
                },
                "protocol": "tcp"
            }
        }*/

    ],
    "probes": [
        {
            "name": "FabricGatewayProbe",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('nt0fabricTcpGatewayPort')]",
                "protocol": "tcp"
            }
        },
        {
            "name": "FabricHttpGatewayProbe",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('nt0fabricHttpGatewayPort')]",
                "protocol": "tcp"
            }
        } /* Remove AppPort1 from hello external load balancer.
        {
            "name": "AppPortProbe1",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('loadBalancedAppPort1')]",
                "protocol": "tcp"
            }
        } */

    ],
    "inboundNatPools": [
    ```

5. Dodaj drugi `Microsoft.Network/loadBalancers` zasobów. Wygląda podobnie toohello wewnętrznego modułu równoważenia obciążenia utworzony w hello [modułu równoważenia obciążenia tylko do wewnętrznego](#internallb) sekcji, ale używa powitania "-Int" obciążenia równoważenia zmienne i implementuje wyłącznie hello aplikacji port 80. Spowoduje to również usunięcie `inboundNatPools`, punkty końcowe protokołu RDP tookeep hello publiczny moduł równoważenia obciążenia. Jeśli chcesz RDP na powitania wewnętrznego modułu równoważenia obciążenia, Przenieś `inboundNatPools` toothis usługi równoważenia obciążenia zewnętrznych hello wewnętrznego modułu równoważenia obciążenia:

    ```
            /* Add a second load balancer, configured with a static privateIPAddress and hello "-Int" load balancer variables. */
            {
                "apiVersion": "[variables('lbApiVersion')]",
                "type": "Microsoft.Network/loadBalancers",
                /* Add "-Internal" toohello name. */
                "name": "[concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'), '-Internal')]",
                "location": "[parameters('computeLocation')]",
                "dependsOn": [
                    /* Remove public IP dependsOn, add vnet dependsOn
                    "[concat('Microsoft.Network/publicIPAddresses/',concat(parameters('lbIPName'),'-','0'))]"
                    */
                    "[concat('Microsoft.Network/virtualNetworks/',parameters('virtualNetworkName'))]"
                ],
                "properties": {
                    "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                /* Switch from Public tooPrivate IP address
                                */
                                "publicIPAddress": {
                                    "id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"
                                }
                                */
                                "subnet" :{
                                    "id": "[variables('subnet0Ref')]"
                                },
                                "privateIPAddress": "[parameters('internalLBAddress')]",
                                "privateIPAllocationMethod": "Static"
                            }
                        }
                    ],
                    "backendAddressPools": [
                        {
                            "name": "LoadBalancerBEAddressPool",
                            "properties": {}
                        }
                    ],
                    "loadBalancingRules": [
                        /* Add hello AppPort rule. Be sure tooreference hello "-Int" versions of backendAddressPool, frontendIPConfiguration, and hello probe variables. */
                        {
                            "name": "AppPortLBRule1",
                            "properties": {
                                "backendAddressPool": {
                                    "id": "[variables('lbPoolID0-Int')]"
                                },
                                "backendPort": "[parameters('loadBalancedAppPort1')]",
                                "enableFloatingIP": "false",
                                "frontendIPConfiguration": {
                                    "id": "[variables('lbIPConfig0-Int')]"
                                },
                                "frontendPort": "[parameters('loadBalancedAppPort1')]",
                                "idleTimeoutInMinutes": "5",
                                "probe": {
                                    "id": "[concat(variables('lbID0-Int'),'/probes/AppPortProbe1')]"
                                },
                                "protocol": "tcp"
                            }
                        }
                    ],
                    "probes": [
                    /* Add hello probe for hello app port. */
                    {
                            "name": "AppPortProbe1",
                            "properties": {
                                "intervalInSeconds": 5,
                                "numberOfProbes": 2,
                                "port": "[parameters('loadBalancedAppPort1')]",
                                "protocol": "tcp"
                            }
                        }
                    ],
                    "inboundNatPools": [
                    ]
                },
                "tags": {
                    "resourceType": "Service Fabric",
                    "clusterName": "[parameters('clusterName')]"
                }
            },
    ```

6. W `networkProfile` dla hello `Microsoft.Compute/virtualMachineScaleSets` zasobów, dodać puli adresów zaplecza wewnętrzny hello:

    ```
    "loadBalancerBackendAddressPools": [
                                                        {
                                                            "id": "[variables('lbPoolID0')]"
                                                        },
                                                        {
                                                            /* Add internal BE pool */
                                                            "id": "[variables('lbPoolID0-Int')]"
                                                        }
    ],
    ```

7. Wdrażanie szablonu hello:

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkinginternalexternallb -Location westus

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkinginternalexternallb -TemplateFile C:\SFSamples\Final\template\_internalexternalLB.json
    ```

Po wdrożeniu widać dwie usługi równoważenia obciążenia w grupie zasobów hello. Po przejściu usługi równoważenia obciążenia hello widoczne hello publicznego adresu IP i zarządzania przypisany punktów końcowych (porty 19000 i 19080) toohello publicznego adresu IP. Również widoczne hello statyczne wewnętrzne IP adres i aplikacji przypisany punkt końcowy (port 80) toohello wewnętrznego modułu równoważenia obciążenia. Zarówno załadować wykorzystania równoważenia hello tego samego zestawu skalowania maszyn wirtualnych puli zaplecza.

## <a name="next-steps"></a>Następne kroki
[Tworzenie klastra](service-fabric-cluster-creation-via-arm.md)
