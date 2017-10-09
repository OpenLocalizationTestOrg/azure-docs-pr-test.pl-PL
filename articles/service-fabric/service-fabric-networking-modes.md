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
# <a name="service-fabric-container-networking-modes"></a>Tryby sieci kontenera sieci szkieletowej usług

Witaj domyślny tryb sieci oferowany hello sieci szkieletowej usług hello jest klaster usługi kontenera `nat` trybu sieci. Z hello `nat` sieci trybu mających więcej niż jeden toohello nasłuchiwania usługi kontenerów sam portu powoduje błędy wdrożenia. Do uruchamiania kilka usług, które nasłuchują na powitania tego samego portu, Service Fabric obsługuje hello `open` trybu sieciowego (w wersji 5.7 lub nowszej). Z hello `open` sieci trybu każdej usługi kontenera pobiera przypisywany dynamicznie adres IP wewnętrznie stosowanie wielu usług toolisten toohello tego samego portu.   

W związku z tym z pojedynczego typu usługi z punktem końcowym statyczne zdefiniowane w manifeście usługi hello, nowych usług mogą być tworzone i usunąć bez błędów wdrażania przy użyciu hello `open` trybu sieci. Podobnie, można użyć jednego hello sam `docker-compose.yml` plik z portu statycznego mapowania do tworzenia wielu usług.

Przy użyciu hello przypisywane dynamicznie usług toodiscover IP nie jest zalecane od czasu zmiany adresu IP powitania po usługi hello ponownie uruchamia lub przenosi tooanother węzła. Używaj tylko hello **Usługa nazewnictwa sieci szkieletowej** lub hello **usługi DNS** dla potrzeb odnajdywania usług. 


> [!WARNING]
> Tylko łącznie 4096 adresy IP są dozwolone dla sieci wirtualnej na platformie Azure. W związku z tym hello Suma hello liczbę węzłów i hello liczbę wystąpień usługi kontenera (z `open` sieci) nie może przekroczyć 4096 w ramach sieci wirtualnej. W przypadku takich scenariuszy wysokiej gęstości hello `nat` zalecany jest tryb sieci.
>

## <a name="setting-up-open-networking-mode"></a>Konfigurowanie trybu otwartego sieci

1. Konfigurowanie szablonów usługi Azure Resource Manager hello przez włączenie usługi DNS i hello dostawca IP w obszarze `fabricSettings`. 

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

2. Skonfiguruj adresy IP wielu toobe skonfigurowany w każdym węźle klastra hello hello sieci profilu sekcji tooallow. Witaj poniższy przykład konfiguruje pięć adresów IP na węzeł (w związku z tym program może nasłuchiwać portu toohello w każdym węźle pięciu wystąpień usługi) dla klastra usługi sieć szkieletowa usług systemu Windows.

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

    W przypadku klastrów systemu Linux dodatkową konfigurację publicznego adresu IP jest dodawana tooallow łączność wychodząca. Witaj poniższy fragment konfiguruje pięć adresów IP w każdym węźle klastra z systemem Linux:

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

3. Dla systemu Windows, klastry, skonfigurowane grupy NSG zasada otwierania portu UDP i 53 hello sieci wirtualnej z hello następujące wartości:

   | Priorytet |    Nazwa    |    Element źródłowy      |  Element docelowy   |   Usługa    | Akcja |
   |:--------:|:----------:|:--------------:|:--------------:|:------------:|:------:|
   |     2000 | Custom_Dns | VirtualNetwork | VirtualNetwork | DNS (UDP/53) | Zezwalaj  |


4. Określ tryb sieci hello w manifeście aplikacji hello dla każdej usługi `<NetworkConfig NetworkType="open">`.  Tryb Hello `open` powoduje usługi hello pobierania dedykowany adres IP. Jeśli tryb nie jest określony, domyślnie przyjmowana toohello podstawowe `nat` tryb. W związku z tym w hello poniższy przykład manifestu `NodeContainerServicePackage1` i `NodeContainerServicePackage2` można każdego toohello nasłuchiwania tego samego portu (obie te usługi są nasłuchiwanie `Endpoint1`).

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
Można mieszać i dopasowywać różne tryby sieciowych w usługach w ramach aplikacji w klastrze systemu Windows. W związku z tym niektóre usługi mogą mieć na `open` tryb i niektóre na `nat` trybu sieci. Gdy usługa jest skonfigurowana z `nat`, port hello jest nasłuchiwania toomust być unikatowe. Mieszanie tryby sieci dla różnych usług nie jest obsługiwana w systemie Linux klastrów. 


## <a name="next-steps"></a>Następne kroki
W tym artykule przedstawiono dotyczące tryby oferowane przez sieć szkieletowa usług sieciowych.  

* [Model aplikacji sieci szkieletowej usług](service-fabric-application-model.md)
* [Zasoby manifestu usługi sieci szkieletowej usług](service-fabric-application-model.md)
* [Wdrażanie systemu Windows tooService kontenera sieci szkieletowej w systemie Windows Server 2016](service-fabric-get-started-containers.md)
* [Wdrażanie tooService kontenera Docker sieci szkieletowej w systemie Linux](service-fabric-get-started-containers-linux.md)
