## <a name="load-balancer"></a>Moduł równoważenia obciążenia
Moduł równoważenia obciążenia jest używany, gdy chcesz tooscale aplikacji. Typowe wdrożenie scenariusze obejmują aplikacje działające na wielu wystąpień maszyny Wirtualnej. Witaj wystąpień maszyn wirtualnych są fronted przez równoważenia obciążenia, który pomaga toohello ruchu sieciowego toodistribute różne wystąpienia. 

![Karty Sieciowej na jednej maszynie Wirtualnej](./media/resource-groups-networking/figure8.png)

| Właściwość | Opis |
| --- | --- |
| *konfiguracji IP frontonu* |Moduł równoważenia obciążenia może zawierać co najmniej jeden adres IP frontonu, znanej także jako wirtualnych adresów IP (VIP). Te adresy IP stanowią wejściowych hello ruchu i może być publiczny adres IP lub prywatnego adresu IP |
| *backendAddressPools* |są to adresy IP skojarzone z hello będą dystrybuowane obciążenia toowhich kart sieciowych maszyny Wirtualnej |
| *dodatkowe elementy Ipconfiguration* |Właściwości reguły mapowania IP frontonu danego portu kombinacja tooa zbiór adresów IP zaplecza i portu kombinacji. Z jednej definicji zasobu usługi równoważenia obciążenia można zdefiniować wiele reguł równoważenia obciążenia, każda reguła w czasie wykonywania odbicia kombinację przodu kończyć adresu IP i portu i wykonać ich kopię końcowemu adresowi IP i port skojarzony z maszynami wirtualnymi. Reguła Hello jest jeden port hello frontonu puli toomany maszyn wirtualnych w puli zaplecza hello |
| *Sondy* |sondy włączyć śledzenie tookeep hello kondycji wystąpień maszyny Wirtualnej. W przypadku niepowodzenia sondy kondycji hello wystąpienie maszyny wirtualnej zostaną wykonane poza obrotu automatycznie |
| *inboundNatRules* |Definiowanie hello reguł NAT przepływających przez IP frontonu hello ruchu przychodzącego i rozproszonych toohello zaplecza IP tooa określonej maszyny wirtualnej wystąpienia. Reguła NAT jest jeden port na maszynie wirtualnej tooone puli frontonu hello w puli zaplecza hello |

Przykład szablon usługi równoważenia obciążenia w formacie Json:

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "dnsNameforLBIP": {
          "type": "string",
          "metadata": {
            "description": "Unique DNS name"
          }
        },
        "location": {
          "type": "string",
          "allowedValues": [
            "East US",
            "West US",
            "West Europe",
            "East Asia",
            "Southeast Asia"
          ],
          "metadata": {
            "description": "Location toodeploy"
          }
        },
        "addressPrefix": {
          "type": "string",
          "defaultValue": "10.0.0.0/16",
          "metadata": {
            "description": "Address Prefix"
          }
        },
        "subnetPrefix": {
          "type": "string",
          "defaultValue": "10.0.0.0/24",
          "metadata": {
            "description": "Subnet Prefix"
          }
        },
        "publicIPAddressType": {
          "type": "string",
          "defaultValue": "Dynamic",
          "allowedValues": [
            "Dynamic",
            "Static"
          ],
          "metadata": {
            "description": "Public IP type"
          }
        }
      },
      "variables": {
        "virtualNetworkName": "virtualNetwork1",
        "publicIPAddressName": "publicIp1",
        "subnetName": "subnet1",
        "loadBalancerName": "loadBalancer1",
        "nicName": "networkInterface1",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
        "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]",
        "publicIPAddressID": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]",
        "lbID": "[resourceId('Microsoft.Network/loadBalancers',variables('loadBalancerName'))]",
        "nicId": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]",
        "frontEndIPConfigID": "[concat(variables('lbID'),'/frontendIPConfigurations/loadBalancerFrontEnd')]",
        "backEndIPConfigID": "[concat(variables('nicId'),'/ipConfigurations/ipconfig1')]"
      },
      "resources": [
    {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIPAddressName')]",
      "location": "[parameters('location')]",
      "properties": {
        "publicIPAllocationMethod": "[parameters('publicIPAddressType')]",
        "dnsSettings": {
          "domainNameLabel": "[parameters('dnsNameforLBIP')]"
        }
      }
    },
    {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Network/virtualNetworks",
      "name": "[variables('virtualNetworkName')]",
      "location": "[parameters('location')]",
      "properties": {
        "addressSpace": {
          "addressPrefixes": [
            "[parameters('addressPrefix')]"
          ]
        },
        "subnets": [
          {
            "name": "[variables('subnetName')]",
            "properties": {
              "addressPrefix": "[parameters('subnetPrefix')]"
            }
          }
        ]
      }
    },
    {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[variables('nicName')]",
      "location": "[parameters('location')]",
      "dependsOn": [
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
        "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]"
      ],
      "properties": {
        "ipConfigurations": [
          {
            "name": "ipconfig1",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "subnet": {
                "id": "[variables('subnetRef')]"
              },
              "loadBalancerBackendAddressPools": [
                {
                  "id": "[concat(variables('lbID'), '/backendAddressPools/LoadBalancerBackend')]"
                }
              ],
              "loadBalancerInboundNatRules": [
                {
                  "id": "[concat(variables('lbID'),'/inboundNatRules/RDP')]"
                }
              ]
            }
          }
        ]
      }
    },
    {
      "apiVersion": "2015-05-01-preview",
      "name": "[variables('loadBalancerName')]",
      "type": "Microsoft.Network/loadBalancers",
      "location": "[parameters('location')]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'))]"
      ],
      "properties": {
        "frontendIPConfigurations": [
          {
            "name": "loadBalancerFrontEnd",
            "properties": {
              "publicIPAddress": {
                "id": "[variables('publicIPAddressID')]"
              }
            }
          }
        ],
        "backendAddressPools": [
          {
            "name": "loadBalancerBackEnd"
          }
        ],
        "inboundNatRules": [
          {
            "name": "RDP",
            "properties": {
              "frontendIPConfiguration": {
                "id": "[variables('frontEndIPConfigID')]"
              },
              "protocol": "tcp",
              "frontendPort": 3389,
              "backendPort": 3389,
              "enableFloatingIP": false
            }
          }
        ]
      }
    }
      ]
    }

### <a name="additional-resources"></a>Dodatkowe zasoby
Odczyt [interfejsu API REST usługi równoważenia obciążenia](https://msdn.microsoft.com/library/azure/mt163651.aspx) Aby uzyskać więcej informacji.

