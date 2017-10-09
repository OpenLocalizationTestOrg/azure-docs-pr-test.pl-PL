## <a name="application-gateway"></a><span data-ttu-id="28644-101">Application Gateway</span><span class="sxs-lookup"><span data-stu-id="28644-101">Application Gateway</span></span>
<span data-ttu-id="28644-102">Brama aplikacji w udostępnia równoważenie rozwiązania opartego na temat funkcji równoważenia obciążenia warstwy 7 obciążenia zarządzany Azure HTTP.</span><span class="sxs-lookup"><span data-stu-id="28644-102">Application Gateway provides an Azure-managed HTTP load balancing solution based on layer 7 load balancing.</span></span> <span data-ttu-id="28644-103">Równoważenie obciążenia aplikacji umożliwia wykorzystanie hello reguły routingu ruchu sieciowego oparte na HTTP.</span><span class="sxs-lookup"><span data-stu-id="28644-103">Application load balancing allows hello use of routing rules for network traffic based on HTTP.</span></span> 
<BR>

| <span data-ttu-id="28644-104">Właściwość</span><span class="sxs-lookup"><span data-stu-id="28644-104">Property</span></span> | <span data-ttu-id="28644-105">Opis</span><span class="sxs-lookup"><span data-stu-id="28644-105">Description</span></span> |
| --- | --- |
| <span data-ttu-id="28644-106">**backendAddressPools**</span><span class="sxs-lookup"><span data-stu-id="28644-106">**backendAddressPools**</span></span> |<span data-ttu-id="28644-107">Lista Hello adresy IP serwerów zaplecza hello.</span><span class="sxs-lookup"><span data-stu-id="28644-107">hello list of IP addresses of hello back end servers.</span></span> <span data-ttu-id="28644-108">wymienionych na liście adresów IP Hello albo powinny należeć toohello podsieć sieci wirtualnej lub powinny być publicznego adresu IP/VIP lub prywatnego adresu IP</span><span class="sxs-lookup"><span data-stu-id="28644-108">hello IP addresses listed should either belong toohello virtual network subnet, or should be a public IP/VIP or private IP</span></span> |
| <span data-ttu-id="28644-109">**backendHttpSettingsCollection**</span><span class="sxs-lookup"><span data-stu-id="28644-109">**backendHttpSettingsCollection**</span></span> |<span data-ttu-id="28644-110">Co Pula ma ustawienia, takie jak koligacja opartego na plikach cookie, protokołu i portu.</span><span class="sxs-lookup"><span data-stu-id="28644-110">Every pool has settings like port, protocol, and cookie based affinity.</span></span> <span data-ttu-id="28644-111">Te ustawienia są wiązanej tooa puli i są stosowane tooall serwery w puli hello</span><span class="sxs-lookup"><span data-stu-id="28644-111">These settings are tied tooa pool and are applied tooall servers within hello pool</span></span> |
| <span data-ttu-id="28644-112">**frontendPorts**</span><span class="sxs-lookup"><span data-stu-id="28644-112">**frontendPorts**</span></span> |<span data-ttu-id="28644-113">Ten port jest port publiczny hello otwarte na powitania bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="28644-113">This port is hello public port opened on hello application gateway.</span></span> <span data-ttu-id="28644-114">Ruch trafienia tego portu, a następnie pobiera przekierowanie tooone hello serwerów wewnętrznej bazy</span><span class="sxs-lookup"><span data-stu-id="28644-114">Traffic hits this port, and then gets redirected tooone of hello back end servers</span></span> |
| <span data-ttu-id="28644-115">**httpListeners**</span><span class="sxs-lookup"><span data-stu-id="28644-115">**httpListeners**</span></span> |<span data-ttu-id="28644-116">Odbiornik ma port serwera sieci Web, protokół (Http lub Https, te jest rozróżniana wielkość liter), a hello nazwa certyfikatu SSL (jeśli odciążania Konfigurowanie protokołu SSL)</span><span class="sxs-lookup"><span data-stu-id="28644-116">Listener has a frontend port, a protocol (Http or Https, these are case-sensitive), and hello SSL certificate name (if configuring SSL offload)</span></span> |
| <span data-ttu-id="28644-117">**elementów Requestroutingrule**</span><span class="sxs-lookup"><span data-stu-id="28644-117">**requestRoutingRules**</span></span> |<span data-ttu-id="28644-118">Reguła Hello wiąże hello hello i odbiornika zaplecza puli serwerów i określa, jaki ruch hello puli serwera zaplecza powinny być kierowane.</span><span class="sxs-lookup"><span data-stu-id="28644-118">hello rule binds hello listener and hello back end server pool and defines which back end server pool hello traffic should be directed.</span></span> <span data-ttu-id="28644-119">Obecnie działa tylko jako okrężnego</span><span class="sxs-lookup"><span data-stu-id="28644-119">Currently works only as Round-robin</span></span> |

<span data-ttu-id="28644-120">Przykład szablonu Json bramy aplikacji:</span><span class="sxs-lookup"><span data-stu-id="28644-120">Example of an application gateway Json template:</span></span>

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "location": {
          "type": "string",
          "metadata": {
            "description": "Location toodeploy to"
          }
        },
        "addressPrefix": {
          "type": "string",
          "defaultValue": "10.0.0.0/16",
          "metadata": {
            "description": "Address prefix for hello Virtual Network"
          }
        },
        "subnetPrefix": {
          "type": "string",
          "defaultValue": "10.0.0.0/28",
          "metadata": {
            "description": "Subnet prefix"
          }
        },
        "skuName": {
          "type": "string",
          "allowedValues": [
            "Standard_Small",
            "Standard_Medium",
            "Standard_Large"
          ],
          "defaultValue": "Standard_Medium",
          "metadata": {
            "description": "Sku Name"
          }
        },
        "capacity": {
          "type": "int",
          "defaultValue": 2,
          "metadata": {
            "description": "Number of instances"
          }
        },
        "backendIpAddress1": {
          "type": "string",
          "metadata": {
            "description": "IP Address for Backend Server 1"
          }
        },
        "backendIpAddress2": {
          "type": "string",
          "metadata": {
            "description": "IP Address for Backend Server 2"
          }
        }
      },
      "variables": {
        "applicationGatewayName": "applicationGateway1",
        "publicIPAddressName": "publicIp1",
        "virtualNetworkName": "virtualNetwork1",
        "subnetName": "appGatewaySubnet",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
        "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]",
        "publicIPRef": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]",
        "applicationGatewayID": "[resourceId('Microsoft.Network/applicationGateways',variables('applicationGatewayName'))]",
        "apiVersion": "2015-05-01-preview"
      },
      "resources": [
        {
          "apiVersion": "[variables('apiVersion')]",
          "type": "Microsoft.Network/publicIPAddresses",
          "name": "[variables('publicIPAddressName')]",
          "location": "[parameters('location')]",
          "properties": {
            "publicIPAllocationMethod": "Dynamic"
          }
        },
        {
          "apiVersion": "[variables('apiVersion')]",
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
          "apiVersion": "[variables('apiVersion')]",
          "name": "[variables('applicationGatewayName')]",
          "type": "Microsoft.Network/applicationGateways",
          "location": "[parameters('location')]",
          "dependsOn": [
            "[concat('Microsoft.Network/virtualNetworks/', variables    ('virtualNetworkName'))]",
            "[concat('Microsoft.Network/publicIPAddresses/', variables    ('publicIPAddressName'))]"
          ],
          "properties": {
            "sku": {
              "name": "[parameters('skuName')]",
              "tier": "Standard",
              "capacity": "[parameters('capacity')]"
            },
            "gatewayIPConfigurations": [
              {
                "name": "appGatewayIpConfig",
                "properties": {
                  "subnet": {
                    "id": "[variables('subnetRef')]"
                  }
                }
              }
            ],
            "frontendIPConfigurations": [
              {
                "name": "appGatewayFrontendIP",
                "properties": {
                  "PublicIPAddress": {
                    "id": "[variables('publicIPRef')]"
                  }
                }
              }
            ],
            "frontendPorts": [
              {
                "name": "appGatewayFrontendPort",
                "properties": {
                  "Port": 80
                }
              }
            ],
            "backendAddressPools": [
              {
                "name": "appGatewayBackendPool",
                "properties": {
                  "BackendAddresses": [
                    {
                      "IpAddress": "[parameters('backendIpAddress1')]"
                    },
                    {
                      "IpAddress": "[parameters('backendIpAddress2')]"
                    }
                  ]
                }
              }
            ],
            "backendHttpSettingsCollection": [
              {
                "name": "appGatewayBackendHttpSettings",
                "properties": {
                  "Port": 80,
                  "Protocol": "Http",
                  "CookieBasedAffinity": "Disabled"
                }
              }
            ],
            "httpListeners": [
              {
                "name": "appGatewayHttpListener",
                "properties": {
                  "FrontendIPConfiguration": {
                    "Id": "[concat(variables('applicationGatewayID'), '/    frontendIPConfigurations/appGatewayFrontendIP')]"
                  },
                  "FrontendPort": {
                    "Id": "[concat(variables('applicationGatewayID'), '/    frontendPorts/appGatewayFrontendPort')]"
                  },
                  "Protocol": "Http",
                  "SslCertificate": null
                }
              }
            ],
            "requestRoutingRules": [
              {
                "Name": "rule1",
                "properties": {
                  "RuleType": "Basic",
                  "httpListener": {
                    "id": "[concat(variables('applicationGatewayID'), '/    httpListeners/appGatewayHttpListener')]"
                  },
                  "backendAddressPool": {
                    "id": "[concat(variables('applicationGatewayID'), '/    backendAddressPools/appGatewayBackendPool')]"
                  },
                  "backendHttpSettings": {
                    "id": "[concat(variables('applicationGatewayID'), '/    backendHttpSettingsCollection/    appGatewayBackendHttpSettings')]"
                  }
                }
              }
            ]
          }
        }
      ]    
    }


### <a name="additional-resources"></a><span data-ttu-id="28644-121">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="28644-121">Additional resources</span></span>
<span data-ttu-id="28644-122">Odczyt [ bramy aplikacji interfejsu API REST](https://msdn.microsoft.com/library/azure/mt299388.aspx) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="28644-122">Read [ application gateway REST API](https://msdn.microsoft.com/library/azure/mt299388.aspx) for more information.</span></span>

