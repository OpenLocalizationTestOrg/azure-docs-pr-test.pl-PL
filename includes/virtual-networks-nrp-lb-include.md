## <a name="load-balancer"></a><span data-ttu-id="87b47-101">Moduł równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="87b47-101">Load Balancer</span></span>
<span data-ttu-id="87b47-102">Moduł równoważenia obciążenia jest używany, gdy chcesz tooscale aplikacji.</span><span class="sxs-lookup"><span data-stu-id="87b47-102">A load balancer is used when you want tooscale your applications.</span></span> <span data-ttu-id="87b47-103">Typowe wdrożenie scenariusze obejmują aplikacje działające na wielu wystąpień maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="87b47-103">Typical deployment scenarios involve applications running on multiple VM instances.</span></span> <span data-ttu-id="87b47-104">Witaj wystąpień maszyn wirtualnych są fronted przez równoważenia obciążenia, który pomaga toohello ruchu sieciowego toodistribute różne wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="87b47-104">hello VM instances are fronted by a load balancer that helps toodistribute network traffic toohello various instances.</span></span> 

![Karty Sieciowej na jednej maszynie Wirtualnej](./media/resource-groups-networking/figure8.png)

| <span data-ttu-id="87b47-106">Właściwość</span><span class="sxs-lookup"><span data-stu-id="87b47-106">Property</span></span> | <span data-ttu-id="87b47-107">Opis</span><span class="sxs-lookup"><span data-stu-id="87b47-107">Description</span></span> |
| --- | --- |
| <span data-ttu-id="87b47-108">*konfiguracji IP frontonu*</span><span class="sxs-lookup"><span data-stu-id="87b47-108">*frontendIPConfigurations*</span></span> |<span data-ttu-id="87b47-109">Moduł równoważenia obciążenia może zawierać co najmniej jeden adres IP frontonu, znanej także jako wirtualnych adresów IP (VIP).</span><span class="sxs-lookup"><span data-stu-id="87b47-109">a Load balancer can include one or more front end IP addresses, otherwise known as a virtual IPs (VIPs).</span></span> <span data-ttu-id="87b47-110">Te adresy IP stanowią wejściowych hello ruchu i może być publiczny adres IP lub prywatnego adresu IP</span><span class="sxs-lookup"><span data-stu-id="87b47-110">These IP addresses serve as ingress for hello traffic and can be public IP or private IP</span></span> |
| <span data-ttu-id="87b47-111">*backendAddressPools*</span><span class="sxs-lookup"><span data-stu-id="87b47-111">*backendAddressPools*</span></span> |<span data-ttu-id="87b47-112">są to adresy IP skojarzone z hello będą dystrybuowane obciążenia toowhich kart sieciowych maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="87b47-112">these are IP addresses associated with hello VM NICs toowhich load will be distributed</span></span> |
| <span data-ttu-id="87b47-113">*dodatkowe elementy Ipconfiguration*</span><span class="sxs-lookup"><span data-stu-id="87b47-113">*loadBalancingRules*</span></span> |<span data-ttu-id="87b47-114">Właściwości reguły mapowania IP frontonu danego portu kombinacja tooa zbiór adresów IP zaplecza i portu kombinacji.</span><span class="sxs-lookup"><span data-stu-id="87b47-114">a rule property maps a given front end IP and port combination tooa set of back end IP addresses and port combination.</span></span> <span data-ttu-id="87b47-115">Z jednej definicji zasobu usługi równoważenia obciążenia można zdefiniować wiele reguł równoważenia obciążenia, każda reguła w czasie wykonywania odbicia kombinację przodu kończyć adresu IP i portu i wykonać ich kopię końcowemu adresowi IP i port skojarzony z maszynami wirtualnymi.</span><span class="sxs-lookup"><span data-stu-id="87b47-115">With a single definition of a load balancer resource, you can define multiple load balancing rules, each rule reflecting a combination of a front end IP and port and back end IP and port associated with virtual machines.</span></span> <span data-ttu-id="87b47-116">Reguła Hello jest jeden port hello frontonu puli toomany maszyn wirtualnych w puli zaplecza hello</span><span class="sxs-lookup"><span data-stu-id="87b47-116">hello rule is one port in hello front end pool toomany virtual machines in hello back end pool</span></span> |
| <span data-ttu-id="87b47-117">*Sondy*</span><span class="sxs-lookup"><span data-stu-id="87b47-117">*Probes*</span></span> |<span data-ttu-id="87b47-118">sondy włączyć śledzenie tookeep hello kondycji wystąpień maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="87b47-118">probes enable you tookeep track of hello health of VM instances.</span></span> <span data-ttu-id="87b47-119">W przypadku niepowodzenia sondy kondycji hello wystąpienie maszyny wirtualnej zostaną wykonane poza obrotu automatycznie</span><span class="sxs-lookup"><span data-stu-id="87b47-119">If a health probe fails, hello virtual machine instance will be taken out of rotation automatically</span></span> |
| <span data-ttu-id="87b47-120">*inboundNatRules*</span><span class="sxs-lookup"><span data-stu-id="87b47-120">*inboundNatRules*</span></span> |<span data-ttu-id="87b47-121">Definiowanie hello reguł NAT przepływających przez IP frontonu hello ruchu przychodzącego i rozproszonych toohello zaplecza IP tooa określonej maszyny wirtualnej wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="87b47-121">NAT rules defining hello inbound traffic flowing through hello front end IP and distributed toohello back end IP tooa specific virtual machine instance.</span></span> <span data-ttu-id="87b47-122">Reguła NAT jest jeden port na maszynie wirtualnej tooone puli frontonu hello w puli zaplecza hello</span><span class="sxs-lookup"><span data-stu-id="87b47-122">NAT rule is one port in hello front end pool tooone virtual machine in hello back end pool</span></span> |

<span data-ttu-id="87b47-123">Przykład szablon usługi równoważenia obciążenia w formacie Json:</span><span class="sxs-lookup"><span data-stu-id="87b47-123">Example of load balancer template in Json format:</span></span>

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

### <a name="additional-resources"></a><span data-ttu-id="87b47-124">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="87b47-124">Additional resources</span></span>
<span data-ttu-id="87b47-125">Odczyt [interfejsu API REST usługi równoważenia obciążenia](https://msdn.microsoft.com/library/azure/mt163651.aspx) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="87b47-125">Read [load balancer REST API](https://msdn.microsoft.com/library/azure/mt163651.aspx) for more information.</span></span>

