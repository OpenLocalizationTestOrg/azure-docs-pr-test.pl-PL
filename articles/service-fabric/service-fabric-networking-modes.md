---
title: "Konfigurowanie sieci tryby usługi kontenera platformy Azure Service Fabric | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak można skonfigurować różne tryby sieci, które obsługuje sieć szkieletowa usług Azure."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: d552c8cd-67d1-45e8-91dc-871853f44fc6
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: f792f9604a5d6e62551ed92c1049d6e2b4216417
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="service-fabric-container-networking-modes"></a><span data-ttu-id="967b9-103">Tryby sieci kontenera sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="967b9-103">Service Fabric container networking modes</span></span>

<span data-ttu-id="967b9-104">Domyślny tryb sieci oferowanych w klastrze usługi sieć szkieletowa usług dla usługi kontenera jest `nat` trybu sieci.</span><span class="sxs-lookup"><span data-stu-id="967b9-104">The default networking mode offered in the Service Fabric cluster for container services is the `nat` networking mode.</span></span> <span data-ttu-id="967b9-105">Z `nat` sieci trybie mających więcej niż jedna usługa kontenery nasłuchiwanie wyniki do tego samego portu błędy wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="967b9-105">With the `nat` networking mode, having more than one containers service listening to the same port results in deployment errors.</span></span> <span data-ttu-id="967b9-106">Uruchomione kilka usług tego nasłuchiwania na tym samym porcie, obsługuje sieci szkieletowej usług `open` trybu sieciowego (w wersji 5.7 lub nowszej).</span><span class="sxs-lookup"><span data-stu-id="967b9-106">For running several services that listen on the same port, Service Fabric supports the `open` networking mode (version 5.7 or higher).</span></span> <span data-ttu-id="967b9-107">Z `open` sieci trybu każdej usługi kontenera pobiera przypisywany dynamicznie adres IP wewnętrznie stosowanie wielu usług do nasłuchiwania do tego samego portu.</span><span class="sxs-lookup"><span data-stu-id="967b9-107">With the `open` networking mode, each container service gets a dynamically assigned IP address internally allowing multiple services to listen to the same port.</span></span>   

<span data-ttu-id="967b9-108">W związku z tym z pojedynczego typu usługi z punktem końcowym statyczne zdefiniowane w manifeście usługi, nowych usług mogą być tworzone i usunąć bez błędów wdrażania przy użyciu `open` trybu sieci.</span><span class="sxs-lookup"><span data-stu-id="967b9-108">Thus, with a single service type with a static endpoint defined in the service manifest, new services may be created and deleted without deployment errors using the `open` networking mode.</span></span> <span data-ttu-id="967b9-109">Podobnie, co może używać tego samego `docker-compose.yml` plik z portu statycznego mapowania do tworzenia wielu usług.</span><span class="sxs-lookup"><span data-stu-id="967b9-109">Similarly, one can use the same `docker-compose.yml` file with static port mappings for creating multiple services.</span></span>

<span data-ttu-id="967b9-110">Za pomocą IP dynamicznie przypisywanych do odnajdywania usługi nie jest zalecane od czasu zmiany adresu IP, gdy Usługa uruchamia się ponownie lub przenoszone do innego węzła.</span><span class="sxs-lookup"><span data-stu-id="967b9-110">Using the dynamically assigned IP to discover services is not advisable since the IP address changes when the service restarts or moves to another node.</span></span> <span data-ttu-id="967b9-111">Należy używać tylko **Usługa nazewnictwa sieci szkieletowej** lub **usługi DNS** dla potrzeb odnajdywania usług.</span><span class="sxs-lookup"><span data-stu-id="967b9-111">Only use the **Service Fabric Naming Service**  or the **DNS Service** for service discovery.</span></span> 


> [!WARNING]
> <span data-ttu-id="967b9-112">Tylko łącznie 4096 adresy IP są dozwolone dla sieci wirtualnej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="967b9-112">Only a total of 4096 IPs are allowed per vNET in Azure.</span></span> <span data-ttu-id="967b9-113">W związku z tym sumę liczby węzłów i numer wystąpienia usługi kontenera (z `open` sieci) nie może przekroczyć 4096 w ramach sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="967b9-113">Thus, the sum of the number of nodes and the number of container service instances (with `open` networking) cannot exceed 4096 within a vNET.</span></span> <span data-ttu-id="967b9-114">W przypadku takich scenariuszy wysokiej gęstości `nat` zalecany jest tryb sieci.</span><span class="sxs-lookup"><span data-stu-id="967b9-114">For such high-density scenarios, the `nat` networking mode is recommended.</span></span>
>

## <a name="setting-up-open-networking-mode"></a><span data-ttu-id="967b9-115">Konfigurowanie trybu otwartego sieci</span><span class="sxs-lookup"><span data-stu-id="967b9-115">Setting up open networking mode</span></span>

1. <span data-ttu-id="967b9-116">Konfigurowanie szablonów usługi Azure Resource Manager przez włączenie usługi DNS i dostawca IP w obszarze `fabricSettings`.</span><span class="sxs-lookup"><span data-stu-id="967b9-116">Set up the Azure Resource Manager template by enabling DNS Service and the IP Provider under `fabricSettings`.</span></span> 

    ```json
    "fabricSettings": [
                {
                    "name": "DnsService",
                    "parameters": [
                       {
                            "name": "IsEnabled",
                            "value": "true"
                      }
                    ]
                },
                {
                    "name": "Hosting",
                    "parameters": [
                      { 
                            "name": "IPProviderEnabled",
                            "value": "true"
                      }
                    ]
                },
                {
                    "name":  "Trace/Etw", 
                    "parameters": [
                    {
                            "name": "Level",
                            "value": "5"
                    }
                    ]
                },
                {
                    "name": "Setup",
                    "parameters": [
                    {
                            "name": "ContainerNetworkSetup",
                            "value": "true"
                    }
                    ]
                }
            ],
    ```

2. <span data-ttu-id="967b9-117">Konfigurowanie sekcji profilu sieciowego umożliwiają wielu adresów IP, które mają być skonfigurowane na każdym węźle klastra.</span><span class="sxs-lookup"><span data-stu-id="967b9-117">Set up the network profile section to allow multiple IP addresses to be configured on each node of the cluster.</span></span> <span data-ttu-id="967b9-118">Poniższy przykład powoduje ustawienie pięć adresów IP na węzeł (w związku z tym można masz pięć wystąpień usługi nasłuchiwanie portów w każdym węźle) dla klastra usługi sieć szkieletowa usług systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="967b9-118">The following example sets up five IP addresses per node (thus you can have five service instances listening to the port on each node) for a Windows Service Fabric cluster.</span></span>

    ```json
    "variables": {
        "nicName": "NIC",
        "vmName": "vm",
        "virtualNetworkName": "VNet",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
        "vmNodeType0Name": "[toLower(concat('NT1', variables('vmName')))]",
        "subnet0Name": "Subnet-0",
        "subnet0Prefix": "10.0.0.0/24",
        "subnet0Ref": "[concat(variables('vnetID'),'/subnets/',variables('subnet0Name'))]",
        "lbID0": "[resourceId('Microsoft.Network/loadBalancers',concat('LB','-', parameters('clusterName'),'-',variables('vmNodeType0Name')))]",
        "lbIPConfig0": "[concat(variables('lbID0'),'/frontendIPConfigurations/LoadBalancerIPConfig')]",
        "lbPoolID0": "[concat(variables('lbID0'),'/backendAddressPools/LoadBalancerBEAddressPool')]",
        "lbProbeID0": "[concat(variables('lbID0'),'/probes/FabricGatewayProbe')]",
        "lbHttpProbeID0": "[concat(variables('lbID0'),'/probes/FabricHttpGatewayProbe')]",
        "lbNatPoolID0": "[concat(variables('lbID0'),'/inboundNatPools/LoadBalancerBEAddressNatPool')]"
    }
    "networkProfile": {
                "networkInterfaceConfigurations": [
                  {
                    "name": "[concat(parameters('nicName'), '-0')]",
                    "properties": {
                      "ipConfigurations": [
                        {
                          "name": "[concat(parameters('nicName'),'-',0)]",
                          "properties": {
                            "primary": "true",
                            "loadBalancerBackendAddressPools": [
                              {
                                "id": "[variables('lbPoolID0')]"
                              }
                            ],
                            "loadBalancerInboundNatPools": [
                              {
                                "id": "[variables('lbNatPoolID0')]"
                              }
                            ],
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 1)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 2)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 3)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 4)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 5)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        }
                      ],
                      "primary": true
                    }
                  }
                ]
              }
    ```

    <span data-ttu-id="967b9-119">W przypadku klastrów systemu Linux dodatkową konfigurację publicznego adresu IP jest dodawany do umożliwiają nawiązywanie połączeń wychodzących.</span><span class="sxs-lookup"><span data-stu-id="967b9-119">For Linux clusters, an additional public IP configuration is added to allow outbound connectivity.</span></span> <span data-ttu-id="967b9-120">Poniższy fragment konfiguruje pięć adresów IP w każdym węźle klastra z systemem Linux:</span><span class="sxs-lookup"><span data-stu-id="967b9-120">The following snippet sets up five IP addresses per node for a Linux cluster:</span></span>

    ```json
    "networkProfile": {
                "networkInterfaceConfigurations": [
                  {
                    "name": "[concat(parameters('nicName'), '-0')]",
                    "properties": {
                      "ipConfigurations": [
                        {
                          "name": "[concat(parameters('nicName'),'-',0)]",
                          "properties": {
                            "primary": "true",
                            "publicipaddressconfiguration": {
                              "name": "devpub",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "loadBalancerBackendAddressPools": [
                              {
                                "id": "[variables('lbPoolID0')]"
                              }
                            ],
                            "loadBalancerInboundNatPools": [
                              {
                                "id": "[variables('lbNatPoolID0')]"
                              }
                            ],
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 1)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 1)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 2)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 2)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 3)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 3)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 4)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 4)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 5)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 5)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        }
                      ],
                      "primary": true
                    }
                  }
                ]
              }
    ```

3. <span data-ttu-id="967b9-121">Tylko klastrów systemu Windows należy skonfigurować reguły NSG otwierania portu UDP i 53 sieci wirtualnej z następującymi wartościami:</span><span class="sxs-lookup"><span data-stu-id="967b9-121">For Windows clusters only, set up an NSG rule opening up port UDP/53 for the vNET with the following values:</span></span>

   | <span data-ttu-id="967b9-122">Priorytet</span><span class="sxs-lookup"><span data-stu-id="967b9-122">Priority</span></span> |    <span data-ttu-id="967b9-123">Nazwa</span><span class="sxs-lookup"><span data-stu-id="967b9-123">Name</span></span>    |    <span data-ttu-id="967b9-124">Element źródłowy</span><span class="sxs-lookup"><span data-stu-id="967b9-124">Source</span></span>      |  <span data-ttu-id="967b9-125">Element docelowy</span><span class="sxs-lookup"><span data-stu-id="967b9-125">Destination</span></span>   |   <span data-ttu-id="967b9-126">Usługa</span><span class="sxs-lookup"><span data-stu-id="967b9-126">Service</span></span>    | <span data-ttu-id="967b9-127">Akcja</span><span class="sxs-lookup"><span data-stu-id="967b9-127">Action</span></span> |
   |:--------:|:----------:|:--------------:|:--------------:|:------------:|:------:|
   |     <span data-ttu-id="967b9-128">2000</span><span class="sxs-lookup"><span data-stu-id="967b9-128">2000</span></span> | <span data-ttu-id="967b9-129">Custom_Dns</span><span class="sxs-lookup"><span data-stu-id="967b9-129">Custom_Dns</span></span> | <span data-ttu-id="967b9-130">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="967b9-130">VirtualNetwork</span></span> | <span data-ttu-id="967b9-131">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="967b9-131">VirtualNetwork</span></span> | <span data-ttu-id="967b9-132">DNS (UDP/53)</span><span class="sxs-lookup"><span data-stu-id="967b9-132">DNS (UDP/53)</span></span> | <span data-ttu-id="967b9-133">Zezwalaj</span><span class="sxs-lookup"><span data-stu-id="967b9-133">Allow</span></span>  |


4. <span data-ttu-id="967b9-134">Określ tryb sieci w manifeście aplikacji dla każdej usługi `<NetworkConfig NetworkType="open">`.</span><span class="sxs-lookup"><span data-stu-id="967b9-134">Specify the networking mode in the app manifest for each service `<NetworkConfig NetworkType="open">`.</span></span>  <span data-ttu-id="967b9-135">Tryb `open` powoduje Usługa pobierania dedykowany adres IP.</span><span class="sxs-lookup"><span data-stu-id="967b9-135">The mode `open` results in the service getting a dedicated IP address.</span></span> <span data-ttu-id="967b9-136">Jeśli tryb nie jest określony, domyślnie przyjmowana do podstawowego `nat` tryb.</span><span class="sxs-lookup"><span data-stu-id="967b9-136">If a mode isn't specified, it defaults to the basic `nat` mode.</span></span> <span data-ttu-id="967b9-137">W związku z tym w poniższym przykładzie manifestu `NodeContainerServicePackage1` i `NodeContainerServicePackage2` można każdego nasłuchiwania do tego samego portu (obie te usługi są nasłuchiwanie `Endpoint1`).</span><span class="sxs-lookup"><span data-stu-id="967b9-137">Thus, in the following manifest example, `NodeContainerServicePackage1` and `NodeContainerServicePackage2` can each listen to the same port (both services are listening on `Endpoint1`).</span></span>

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <ApplicationManifest ApplicationTypeName="NodeJsApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
      <Description>Calculator Application</Description>
      <Parameters>
        <Parameter Name="ServiceInstanceCount" DefaultValue="3"></Parameter>
        <Parameter Name="MyCpuShares" DefaultValue="3"></Parameter>
      </Parameters>
      <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="NodeContainerServicePackage1" ServiceManifestVersion="1.0"/>
        <Policies>
          <ContainerHostPolicies CodePackageRef="NodeContainerService1.Code" Isolation="hyperv">
           <NetworkConfig NetworkType="open"/>
           <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
          </ContainerHostPolicies>
        </Policies>
      </ServiceManifestImport>
      <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="NodeContainerServicePackage2" ServiceManifestVersion="1.0"/>
        <Policies>
          <ContainerHostPolicies CodePackageRef="NodeContainerService2.Code" Isolation="default">
            <NetworkConfig NetworkType="open"/>
            <PortBinding ContainerPort="8910" EndpointRef="Endpoint1"/>
          </ContainerHostPolicies>
        </Policies>
      </ServiceManifestImport>
    </ApplicationManifest>
    ```
<span data-ttu-id="967b9-138">Można mieszać i dopasowywać różne tryby sieciowych w usługach w ramach aplikacji w klastrze systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="967b9-138">You can mix and match different networking modes across services within an application for a Windows cluster.</span></span> <span data-ttu-id="967b9-139">W związku z tym niektóre usługi mogą mieć na `open` tryb i niektóre na `nat` trybu sieci.</span><span class="sxs-lookup"><span data-stu-id="967b9-139">Thus, you can have some services on `open` mode and some on `nat` networking mode.</span></span> <span data-ttu-id="967b9-140">Gdy usługa jest skonfigurowana z `nat`, port jest nasłuchiwanie muszą być unikatowe.</span><span class="sxs-lookup"><span data-stu-id="967b9-140">When a service is configured with `nat`, the port it is listening to must be unique.</span></span> <span data-ttu-id="967b9-141">Mieszanie tryby sieci dla różnych usług nie jest obsługiwana w systemie Linux klastrów.</span><span class="sxs-lookup"><span data-stu-id="967b9-141">Mixing networking modes for different services isn't supported on Linux clusters.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="967b9-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="967b9-142">Next steps</span></span>
<span data-ttu-id="967b9-143">W tym artykule przedstawiono dotyczące tryby oferowane przez sieć szkieletowa usług sieciowych.</span><span class="sxs-lookup"><span data-stu-id="967b9-143">In this article, you learned about networking modes offered by Service Fabric.</span></span>  

* [<span data-ttu-id="967b9-144">Model aplikacji sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="967b9-144">Service Fabric application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="967b9-145">Zasoby manifestu usługi sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="967b9-145">Service Fabric service manifest resources</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="967b9-146">Wdrażanie kontenera systemu Windows w sieci szkieletowej usług w systemie Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="967b9-146">Deploy a Windows container to Service Fabric on Windows Server 2016</span></span>](service-fabric-get-started-containers.md)
* [<span data-ttu-id="967b9-147">Wdrażanie kontenera Docker sieci szkieletowej usług w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="967b9-147">Deploy a Docker container to Service Fabric on Linux</span></span>](service-fabric-get-started-containers-linux.md)
