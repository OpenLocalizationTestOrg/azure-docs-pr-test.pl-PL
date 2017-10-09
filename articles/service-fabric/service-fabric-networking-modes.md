---
title: "aaaConfigure sieci tryby usługi kontenera platformy Azure Service Fabric | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toosetup hello różne tryby sieciowych tej sieci szkieletowej usług Azure obsługuje."
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
ms.openlocfilehash: 5c5dd4c590c7698a947503cbe8ef66ff7d6b503a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-container-networking-modes"></a><span data-ttu-id="41872-103">Tryby sieci kontenera sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="41872-103">Service Fabric container networking modes</span></span>

<span data-ttu-id="41872-104">Witaj domyślny tryb sieci oferowany hello sieci szkieletowej usług hello jest klaster usługi kontenera `nat` trybu sieci.</span><span class="sxs-lookup"><span data-stu-id="41872-104">hello default networking mode offered in hello Service Fabric cluster for container services is hello `nat` networking mode.</span></span> <span data-ttu-id="41872-105">Z hello `nat` sieci trybu mających więcej niż jeden toohello nasłuchiwania usługi kontenerów sam portu powoduje błędy wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="41872-105">With hello `nat` networking mode, having more than one containers service listening toohello same port results in deployment errors.</span></span> <span data-ttu-id="41872-106">Do uruchamiania kilka usług, które nasłuchują na powitania tego samego portu, Service Fabric obsługuje hello `open` trybu sieciowego (w wersji 5.7 lub nowszej).</span><span class="sxs-lookup"><span data-stu-id="41872-106">For running several services that listen on hello same port, Service Fabric supports hello `open` networking mode (version 5.7 or higher).</span></span> <span data-ttu-id="41872-107">Z hello `open` sieci trybu każdej usługi kontenera pobiera przypisywany dynamicznie adres IP wewnętrznie stosowanie wielu usług toolisten toohello tego samego portu.</span><span class="sxs-lookup"><span data-stu-id="41872-107">With hello `open` networking mode, each container service gets a dynamically assigned IP address internally allowing multiple services toolisten toohello same port.</span></span>   

<span data-ttu-id="41872-108">W związku z tym z pojedynczego typu usługi z punktem końcowym statyczne zdefiniowane w manifeście usługi hello, nowych usług mogą być tworzone i usunąć bez błędów wdrażania przy użyciu hello `open` trybu sieci.</span><span class="sxs-lookup"><span data-stu-id="41872-108">Thus, with a single service type with a static endpoint defined in hello service manifest, new services may be created and deleted without deployment errors using hello `open` networking mode.</span></span> <span data-ttu-id="41872-109">Podobnie, można użyć jednego hello sam `docker-compose.yml` plik z portu statycznego mapowania do tworzenia wielu usług.</span><span class="sxs-lookup"><span data-stu-id="41872-109">Similarly, one can use hello same `docker-compose.yml` file with static port mappings for creating multiple services.</span></span>

<span data-ttu-id="41872-110">Przy użyciu hello przypisywane dynamicznie usług toodiscover IP nie jest zalecane od czasu zmiany adresu IP powitania po usługi hello ponownie uruchamia lub przenosi tooanother węzła.</span><span class="sxs-lookup"><span data-stu-id="41872-110">Using hello dynamically assigned IP toodiscover services is not advisable since hello IP address changes when hello service restarts or moves tooanother node.</span></span> <span data-ttu-id="41872-111">Używaj tylko hello **Usługa nazewnictwa sieci szkieletowej** lub hello **usługi DNS** dla potrzeb odnajdywania usług.</span><span class="sxs-lookup"><span data-stu-id="41872-111">Only use hello **Service Fabric Naming Service**  or hello **DNS Service** for service discovery.</span></span> 


> [!WARNING]
> <span data-ttu-id="41872-112">Tylko łącznie 4096 adresy IP są dozwolone dla sieci wirtualnej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="41872-112">Only a total of 4096 IPs are allowed per vNET in Azure.</span></span> <span data-ttu-id="41872-113">W związku z tym hello Suma hello liczbę węzłów i hello liczbę wystąpień usługi kontenera (z `open` sieci) nie może przekroczyć 4096 w ramach sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="41872-113">Thus, hello sum of hello number of nodes and hello number of container service instances (with `open` networking) cannot exceed 4096 within a vNET.</span></span> <span data-ttu-id="41872-114">W przypadku takich scenariuszy wysokiej gęstości hello `nat` zalecany jest tryb sieci.</span><span class="sxs-lookup"><span data-stu-id="41872-114">For such high-density scenarios, hello `nat` networking mode is recommended.</span></span>
>

## <a name="setting-up-open-networking-mode"></a><span data-ttu-id="41872-115">Konfigurowanie trybu otwartego sieci</span><span class="sxs-lookup"><span data-stu-id="41872-115">Setting up open networking mode</span></span>

1. <span data-ttu-id="41872-116">Konfigurowanie szablonów usługi Azure Resource Manager hello przez włączenie usługi DNS i hello dostawca IP w obszarze `fabricSettings`.</span><span class="sxs-lookup"><span data-stu-id="41872-116">Set up hello Azure Resource Manager template by enabling DNS Service and hello IP Provider under `fabricSettings`.</span></span> 

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

2. <span data-ttu-id="41872-117">Skonfiguruj adresy IP wielu toobe skonfigurowany w każdym węźle klastra hello hello sieci profilu sekcji tooallow.</span><span class="sxs-lookup"><span data-stu-id="41872-117">Set up hello network profile section tooallow multiple IP addresses toobe configured on each node of hello cluster.</span></span> <span data-ttu-id="41872-118">Witaj poniższy przykład konfiguruje pięć adresów IP na węzeł (w związku z tym program może nasłuchiwać portu toohello w każdym węźle pięciu wystąpień usługi) dla klastra usługi sieć szkieletowa usług systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="41872-118">hello following example sets up five IP addresses per node (thus you can have five service instances listening toohello port on each node) for a Windows Service Fabric cluster.</span></span>

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

    <span data-ttu-id="41872-119">W przypadku klastrów systemu Linux dodatkową konfigurację publicznego adresu IP jest dodawana tooallow łączność wychodząca.</span><span class="sxs-lookup"><span data-stu-id="41872-119">For Linux clusters, an additional public IP configuration is added tooallow outbound connectivity.</span></span> <span data-ttu-id="41872-120">Witaj poniższy fragment konfiguruje pięć adresów IP w każdym węźle klastra z systemem Linux:</span><span class="sxs-lookup"><span data-stu-id="41872-120">hello following snippet sets up five IP addresses per node for a Linux cluster:</span></span>

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

3. <span data-ttu-id="41872-121">Dla systemu Windows, klastry, skonfigurowane grupy NSG zasada otwierania portu UDP i 53 hello sieci wirtualnej z hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="41872-121">For Windows clusters only, set up an NSG rule opening up port UDP/53 for hello vNET with hello following values:</span></span>

   | <span data-ttu-id="41872-122">Priorytet</span><span class="sxs-lookup"><span data-stu-id="41872-122">Priority</span></span> |    <span data-ttu-id="41872-123">Nazwa</span><span class="sxs-lookup"><span data-stu-id="41872-123">Name</span></span>    |    <span data-ttu-id="41872-124">Element źródłowy</span><span class="sxs-lookup"><span data-stu-id="41872-124">Source</span></span>      |  <span data-ttu-id="41872-125">Element docelowy</span><span class="sxs-lookup"><span data-stu-id="41872-125">Destination</span></span>   |   <span data-ttu-id="41872-126">Usługa</span><span class="sxs-lookup"><span data-stu-id="41872-126">Service</span></span>    | <span data-ttu-id="41872-127">Akcja</span><span class="sxs-lookup"><span data-stu-id="41872-127">Action</span></span> |
   |:--------:|:----------:|:--------------:|:--------------:|:------------:|:------:|
   |     <span data-ttu-id="41872-128">2000</span><span class="sxs-lookup"><span data-stu-id="41872-128">2000</span></span> | <span data-ttu-id="41872-129">Custom_Dns</span><span class="sxs-lookup"><span data-stu-id="41872-129">Custom_Dns</span></span> | <span data-ttu-id="41872-130">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="41872-130">VirtualNetwork</span></span> | <span data-ttu-id="41872-131">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="41872-131">VirtualNetwork</span></span> | <span data-ttu-id="41872-132">DNS (UDP/53)</span><span class="sxs-lookup"><span data-stu-id="41872-132">DNS (UDP/53)</span></span> | <span data-ttu-id="41872-133">Zezwalaj</span><span class="sxs-lookup"><span data-stu-id="41872-133">Allow</span></span>  |


4. <span data-ttu-id="41872-134">Określ tryb sieci hello w manifeście aplikacji hello dla każdej usługi `<NetworkConfig NetworkType="open">`.</span><span class="sxs-lookup"><span data-stu-id="41872-134">Specify hello networking mode in hello app manifest for each service `<NetworkConfig NetworkType="open">`.</span></span>  <span data-ttu-id="41872-135">Tryb Hello `open` powoduje usługi hello pobierania dedykowany adres IP.</span><span class="sxs-lookup"><span data-stu-id="41872-135">hello mode `open` results in hello service getting a dedicated IP address.</span></span> <span data-ttu-id="41872-136">Jeśli tryb nie jest określony, domyślnie przyjmowana toohello podstawowe `nat` tryb.</span><span class="sxs-lookup"><span data-stu-id="41872-136">If a mode isn't specified, it defaults toohello basic `nat` mode.</span></span> <span data-ttu-id="41872-137">W związku z tym w hello poniższy przykład manifestu `NodeContainerServicePackage1` i `NodeContainerServicePackage2` można każdego toohello nasłuchiwania tego samego portu (obie te usługi są nasłuchiwanie `Endpoint1`).</span><span class="sxs-lookup"><span data-stu-id="41872-137">Thus, in hello following manifest example, `NodeContainerServicePackage1` and `NodeContainerServicePackage2` can each listen toohello same port (both services are listening on `Endpoint1`).</span></span>

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
<span data-ttu-id="41872-138">Można mieszać i dopasowywać różne tryby sieciowych w usługach w ramach aplikacji w klastrze systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="41872-138">You can mix and match different networking modes across services within an application for a Windows cluster.</span></span> <span data-ttu-id="41872-139">W związku z tym niektóre usługi mogą mieć na `open` tryb i niektóre na `nat` trybu sieci.</span><span class="sxs-lookup"><span data-stu-id="41872-139">Thus, you can have some services on `open` mode and some on `nat` networking mode.</span></span> <span data-ttu-id="41872-140">Gdy usługa jest skonfigurowana z `nat`, port hello jest nasłuchiwania toomust być unikatowe.</span><span class="sxs-lookup"><span data-stu-id="41872-140">When a service is configured with `nat`, hello port it is listening toomust be unique.</span></span> <span data-ttu-id="41872-141">Mieszanie tryby sieci dla różnych usług nie jest obsługiwana w systemie Linux klastrów.</span><span class="sxs-lookup"><span data-stu-id="41872-141">Mixing networking modes for different services isn't supported on Linux clusters.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="41872-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="41872-142">Next steps</span></span>
<span data-ttu-id="41872-143">W tym artykule przedstawiono dotyczące tryby oferowane przez sieć szkieletowa usług sieciowych.</span><span class="sxs-lookup"><span data-stu-id="41872-143">In this article, you learned about networking modes offered by Service Fabric.</span></span>  

* [<span data-ttu-id="41872-144">Model aplikacji sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="41872-144">Service Fabric application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="41872-145">Zasoby manifestu usługi sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="41872-145">Service Fabric service manifest resources</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="41872-146">Wdrażanie systemu Windows tooService kontenera sieci szkieletowej w systemie Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="41872-146">Deploy a Windows container tooService Fabric on Windows Server 2016</span></span>](service-fabric-get-started-containers.md)
* [<span data-ttu-id="41872-147">Wdrażanie tooService kontenera Docker sieci szkieletowej w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="41872-147">Deploy a Docker container tooService Fabric on Linux</span></span>](service-fabric-get-started-containers-linux.md)
