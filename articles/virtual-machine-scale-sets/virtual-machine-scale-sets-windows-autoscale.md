---
title: aaaAutoscale zestawy skalowania maszyny wirtualnej z systemem Windows | Dokumentacja firmy Microsoft
description: "Ustawienia skalowania automatycznego dla systemu Windows zestawu skalowania maszyn wirtualnych przy użyciu programu Azure PowerShell"
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 88886cad-a2f0-46bc-8b58-32ac2189fc93
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adegeo
ms.openlocfilehash: 67cf1c5063ceba4fc076dc270090defdbddbcfe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-scale-machines-in-a-virtual-machine-scale-set"></a>Automatycznie skalować maszyny w zestawie skalowania maszyn wirtualnych
Zestawy skalowania maszyn wirtualnych ułatwiają możesz toodeploy i zarządzaj nimi wiele identycznych maszyn wirtualnych jako zestaw. Zestawy skalowania w przypadku aplikacji o dużej skali zapewnić warstwy obliczeniowej wysoce skalowalnemu i dostosowania i obsługują obrazów platformy systemu Windows, Linux platformy obrazów niestandardowych obrazów i rozszerzenia. Aby uzyskać więcej informacji na temat zestawów skalowania, zobacz [zestawach skali maszyny wirtualnej](virtual-machine-scale-sets-overview.md).

Ten samouczek pokazuje, jak ustawić toocreate zestaw skalowania maszyn wirtualnych Windows i automatycznie skali hello maszyn w hello. Możesz utworzyć hello skalowalnego definiować skalowania przez utworzenie szablonu usługi Azure Resource Manager i wdrażania go przy użyciu programu Azure PowerShell a. Aby uzyskać więcej informacji na temat szablonów, zobacz [Tworzenie szablonów usługi Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md). toolearn więcej informacji na temat skalowania automatycznego zestawy skalowania, zobacz [automatyczne skalowanie i zestawach skali maszyny wirtualnej](virtual-machine-scale-sets-autoscale-overview.md).

W tym artykule wdrożeniem hello następujących zasobów i rozszerzeń:

* Microsoft.Storage/storageAccounts
* Microsoft.Network/virtualNetworks
* Microsoft.Network/publicIPAddresses
* Microsoft.Network/loadBalancers
* Microsoft.Network/networkInterfaces
* Microsoft.Compute/virtualMachines
* Microsoft.Compute/virtualMachineScaleSets
* Microsoft.Insights.VMDiagnosticsSettings
* Microsoft.Insights/autoscaleSettings

Aby uzyskać więcej informacji na temat zasoby usługi Resource Manager, zobacz [usługi Azure Resource Manager, a wdrożenie klasyczne](../azure-resource-manager/resource-manager-deployment-model.md).

## <a name="step-1-install-azure-powershell"></a>Krok 1. Instalowanie programu Azure PowerShell
Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) uzyskać informacji na temat instalowania najnowszej wersji programu Azure PowerShell hello, wybierając subskrypcję i logowanie tooAzure.

## <a name="step-2-create-a-resource-group-and-a-storage-account"></a>Krok 2: Tworzenie grupy zasobów i konto magazynu
1. **Utwórz grupę zasobów** — wszystkie zasoby musi być wdrożone tooa grupy zasobów. Użyj [New-AzureRmResourceGroup](https://msdn.microsoft.com/library/mt603739.aspx) toocreate grupę zasobów o nazwie **vmsstestrg1**.
2. **Utwórz konto magazynu** — to konto magazynu jest przechowywania hello szablonu. Użyj [New-AzureRmStorageAccount](https://msdn.microsoft.com/library/mt607148.aspx) toocreate konto magazynu o nazwie **vmsstestsa**.

## <a name="step-3-create-hello-template"></a>Krok 3: Tworzenie szablonu hello
Szablonu usługi Azure Resource Manager umożliwia możesz toodeploy i zarządzania zasobami Azure ze sobą przy użyciu opisu JSON zasobów hello i parametry skojarzonego wdrożenia.

1. W edytorze Ulubione Utwórz plik hello C:\VMSSTemplate.json i Dodaj hello początkowej JSON struktury toosupport hello szablonu.

    ```json
    {
      "$schema":"http://schema.management.azure.com/schemas/2014-04-01-preview/VM.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
      },
      "variables": {
      },
      "resources": [
      ]
    }
    ```

2. Parametry nie są zawsze wymagana, ale ich tooinput sposób wartości po wdrożeniu hello szablonu. Dodaj tych parametrów w obszarze hello elementu nadrzędnego dla parametrów czy dodany szablon toohello.

    ```json   
    "vmName": { "type": "string" },
    "vmSSName": { "type": "string" },
    "instanceCount": { "type": "string" },
    "adminUsername": { "type": "string" },
    "adminPassword": { "type": "securestring" },
    "resourcePrefix": { "type": "string" }
    ```
   
    * Nazwa dla hello oddzielne maszyny wirtualnej, która jest używana tooaccess hello maszyny w zestawie skalowania hello.
    * Hello nazwa konta magazynu hello przechowywania hello szablonu.
    * Utwórz Hello liczba tooinitially maszyn wirtualnych w zestawie skalowania hello.
    * Witaj nazwę i hasło konta administratora hello na maszynach wirtualnych hello.
    * Ustaw prefiksu nazwy hello zasobów, które są tworzone toosupport hello skali.

3. Zmienne mogą być używane w wartości toospecify szablonów, które mogą ulec zmianie często lub wartości, które wymagają toobe utworzone na podstawie kombinację wartości parametrów. Dodaj te zmienne w obszarze elementu nadrzędnego zmienne hello czy dodany szablon toohello.

    ```json
    "dnsName1": "[concat(parameters('resourcePrefix'),'dn1')]",
    "dnsName2": "[concat(parameters('resourcePrefix'),'dn2')]",
    "publicIP1": "[concat(parameters('resourcePrefix'),'ip1')]",
    "publicIP2": "[concat(parameters('resourcePrefix'),'ip2')]",
    "loadBalancerName": "[concat(parameters('resourcePrefix'),'lb1')]",
    "virtualNetworkName": "[concat(parameters('resourcePrefix'),'vn1')]",
    "nicName": "[concat(parameters('resourcePrefix'),'nc1')]",
    "lbID": "[resourceId('Microsoft.Network/loadBalancers',variables('loadBalancerName'))]",
    "frontEndIPConfigID": "[concat(variables('lbID'),'/frontendIPConfigurations/loadBalancerFrontEnd')]",
    "storageAccountSuffix": [ "a", "g", "m", "s", "y" ],
    "diagnosticsStorageAccountName": "[concat(parameters('resourcePrefix'), 'a')]",
    "accountid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/','Microsoft.Storage/storageAccounts/', variables('diagnosticsStorageAccountName'))]",
      "wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
    "wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% Processor Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU utilization\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
    "wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
    "wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
    "wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
    ```
   
    * Nazwy DNS, które są używane przez hello interfejsów sieciowych.

        * Witaj nazwy adresów IP i prefiksy hello sieci wirtualnej i podsieci.
        * Witaj nazwy i identyfikatory hello sieci wirtualnej, obciążenia równoważenia i interfejsów sieciowych.
        * Nazwy konta magazynu dla konta hello skojarzone z hello maszyny w zestawie skalowania hello.
        * Ustawienia dla hello diagnostyki rozszerzenia, które jest zainstalowane na maszynie wirtualnej hello. Aby uzyskać więcej informacji na temat hello rozszerzenia diagnostyki, zobacz [Utwórz maszynę wirtualną systemu Windows z monitorowania i diagnostyki za pomocą szablonu usługi Resource Manager Azure](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

4. Dodaj zasób konta magazynu hello pod elementem nadrzędnym zasobów hello czy dodany szablon toohello. Ten szablon używa hello toocreate pętli, zalecane konta magazynu przechowywania hello dysków systemu operacyjnego i danych diagnostycznych. Ten zestaw kont może obsługiwać zapasowych too100 maszyn wirtualnych w zestawie skalowania jest bieżąca maksymalna hello. Z określeniem litera, która została zdefiniowana w połączeniu z hello prefiks hello parametrów szablonu hello zmiennych hello nosi nazwę każdego konta magazynu.

    ```json
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat(parameters('resourcePrefix'), variables('storageAccountSuffix')[copyIndex()])]",
      "apiVersion": "2015-06-15",
      "copy": {
        "name": "storageLoop",
        "count": 5
      },
      "location": "[resourceGroup().location]",
      "properties": { "accountType": "Standard_LRS" }
    },
    ```

5. Dodaj hello zasobów sieci wirtualnej. Aby uzyskać więcej informacji, zobacz [dostawcy zasobów sieciowych](../virtual-network/resource-groups-networking.md).

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Network/virtualNetworks",
      "name": "[variables('virtualNetworkName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "addressSpace": { "addressPrefixes": [ "10.0.0.0/16" ] },
        "subnets": [
          {
            "name": "subnet1",
            "properties": { "addressPrefix": "10.0.0.0/24" }
          }
        ]
      }
    },
    ```

6. Dodaj hello publicznego zasoby adresów IP używanych przez hello obciążenia równoważenia i interfejsu sieciowego.

    ```json
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIP1')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "Dynamic",
        "dnsSettings": {
          "domainNameLabel": "[variables('dnsName1')]"
        }
      }
    },
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIP2')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "Dynamic",
        "dnsSettings": {
          "domainNameLabel": "[variables('dnsName2')]"
        }
      }
    },
    ```

7. Dodaj zasób usługi równoważenia obciążenia hello, który jest używany przez zestaw skali hello. Aby uzyskać więcej informacji, zobacz [Obsługa Menedżera zasobów Azure dla usługi równoważenia obciążenia](../load-balancer/load-balancer-arm.md).

    ```json   
    {
      "apiVersion": "2015-06-15",
      "name": "[variables('loadBalancerName')]",
      "type": "Microsoft.Network/loadBalancers",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
      ],
      "properties": {
        "frontendIPConfigurations": [
          {
            "name": "loadBalancerFrontEnd",
            "properties": {
              "publicIPAddress": {
                "id": "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
              }
            }
          }
        ],
        "backendAddressPools": [ { "name": "bepool1" } ],
        "inboundNatPools": [
          {
            "name": "natpool1",
            "properties": {
              "frontendIPConfiguration": {
                "id": "[variables('frontEndIPConfigID')]"
              },
              "protocol": "tcp",
              "frontendPortRangeStart": 50000,
              "frontendPortRangeEnd": 50500,
              "backendPort": 3389
            }
          }
        ]
      }
    },
    ```

8. Dodaj hello sieci interfejsu zasób, który jest używany przez maszynę wirtualną z oddzielnych hello. Ponieważ maszyny w zestawie skalowania nie są dostępne za pośrednictwem publicznego adresu IP, oddzielnej maszynie wirtualnej jest tworzony w hello sam wirtualnych sieci tooremotely dostępu hello maszyny.

    ```json  
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[variables('nicName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP2'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
      ],
      "properties": {
        "ipConfigurations": [
          {
            "name": "ipconfig1",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicIP2'))]"
              },
              "subnet": {
                "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/virtualNetworks/',variables('virtualNetworkName'),'/subnets/subnet1')]"
              }
            }
          }
        ]
      }
    },
    ```

9. Dodaj hello oddzielnej maszynie wirtualnej w hello sam sieci jako zestaw skali hello.

    ```json
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Compute/virtualMachines",
      "name": "[parameters('vmName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "storageLoop",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
      ],
      "properties": {
        "hardwareProfile": { "vmSize": "Standard_A1" },
        "osProfile": {
          "computername": "[parameters('vmName')]",
          "adminUsername": "[parameters('adminUsername')]",
          "adminPassword": "[parameters('adminPassword')]"
        },
        "storageProfile": {
          "imageReference": {
            "publisher": "MicrosoftWindowsServer",
            "offer": "WindowsServer",
            "sku": "2012-R2-Datacenter",
            "version": "latest"
          },
          "osDisk": {
            "name": "[concat(parameters('resourcePrefix'), 'os1')]",
            "vhd": {
              "uri":  "[concat('https://',parameters('resourcePrefix'),'a.blob.core.windows.net/vhds/',parameters('resourcePrefix'),'os1.vhd')]"
            },
            "caching": "ReadWrite",
            "createOption": "FromImage"        
          }
        },
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]"
            }
          ]
        }
      }
    },
    ```

10. Dodaj zasób zestawu skalowania maszyny wirtualnej hello i określ hello diagnostyki rozszerzenia, które jest zainstalowany na wszystkich maszynach wirtualnych w zestawie skalowania hello. Wiele ustawień powitania dla tego zasobu przypominają z hello zasobu maszyny wirtualnej. główne różnice Hello są hello pojemność elementu, który określa hello liczbę maszyn wirtualnych w zestawie skalowania hello i upgradePolicy określający, jak zaktualizowane toovirtual maszyny. Witaj zestaw skalowania jest tworzone dopiero po wszystkich kont magazynu hello są tworzone z elementem dependsOn hello określonej.

    ```json
    {
      "type": "Microsoft.Compute/virtualMachineScaleSets",
      "apiVersion": "2016-03-30",
      "name": "[parameters('vmSSName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "storageLoop",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
        "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]"
      ],
      "sku": {
        "name": "Standard_A1",
        "tier": "Standard",
        "capacity": "[parameters('instanceCount')]"
      },
      "properties": {
        "upgradePolicy": {
          "mode": "Manual"
        },
        "virtualMachineProfile": {
          "storageProfile": {
            "osDisk": {
              "vhdContainers": [
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[0], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[1], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[2], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[3], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[4], '.blob.core.windows.net/vhds')]"
              ],
              "name": "vmssosdisk",
              "caching": "ReadOnly",
              "createOption": "FromImage"
            },
            "imageReference": {
              "publisher": "MicrosoftWindowsServer",
              "offer": "WindowsServer",
              "sku": "2012-R2-Datacenter",
              "version": "latest"
            }
          },
          "osProfile": {
            "computerNamePrefix": "[parameters('vmSSName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
          },
          "networkProfile": {
            "networkInterfaceConfigurations": [
              {
                "name": "networkconfig1",
                "properties": {
                  "primary": "true",
                  "ipConfigurations": [
                    {
                      "name": "ip1",
                      "properties": {
                        "subnet": {
                          "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/virtualNetworks/',variables('virtualNetworkName'),'/subnets/subnet1')]"
                        },
                        "loadBalancerBackendAddressPools": [
                          {
                            "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/loadBalancers/',variables('loadBalancerName'),'/backendAddressPools/bepool1')]"
                          }
                        ],
                        "loadBalancerInboundNatPools": [
                          {
                            "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/loadBalancers/',variables('loadBalancerName'),'/inboundNatPools/natpool1')]"
                          }
                        ]
                      }
                    }
                  ]
                }
              }
            ]
          },
          "extensionProfile": {
            "extensions": [
              {
                "name": "Microsoft.Insights.VMDiagnosticsSettings",
                "properties": {
                  "publisher": "Microsoft.Azure.Diagnostics",
                  "type": "IaaSDiagnostics",
                  "typeHandlerVersion": "1.5",
                  "autoUpgradeMinorVersion": true,
                  "settings": {
                    "xmlCfg": "[base64(concat(variables('wadcfgxstart'),variables('wadmetricsresourceid'),variables('wadcfgxend')))]",
                    "storageAccount": "[variables('diagnosticsStorageAccountName')]"
                  },
                  "protectedSettings": {
                    "storageAccountName": "[variables('diagnosticsStorageAccountName')]",
                    "storageAccountKey": "[listkeys(variables('accountid'), '2015-06-15').key1]",
                    "storageAccountEndPoint": "https://core.windows.net"
                  }
                }
              }
            ]
          }
        }
      }
    },
    ```

11. Dodaj hello autoscaleSettings zasób, który definiuje sposób oparte na powitania wykorzystanie procesora na komputerach hello w zestawie skalowania hello dopasowuje zestaw skali hello.

    ```json
    {
      "type": "Microsoft.Insights/autoscaleSettings",
      "apiVersion": "2015-04-01",
      "name": "[concat(parameters('resourcePrefix'),'as1')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
      ],
      "properties": {
        "enabled": true,
        "name": "[concat(parameters('resourcePrefix'),'as1')]",
        "profiles": [
          {
            "name": "Profile1",
            "capacity": {
              "minimum": "1",
              "maximum": "10",
              "default": "1"
            },
            "rules": [
              {
                "metricTrigger": {
                  "metricName": "\\Processor(_Total)\\% Processor Time",
                  "metricNamespace": "",
                  "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]",
                  "timeGrain": "PT1M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 50.0
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              }
            ]
          }
        ],
        "targetResourceUri": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
      }
    }
    ```

    W tym samouczku te wartości są ważne:
    
    * **metricName**  
    Ta wartość jest hello taki sam jak hello licznika wydajności, zdefiniowanego w zmiennej wadperfcounter hello. Za pomocą tej zmiennej, hello rozszerzenia diagnostycznych zbiera hello **procesor(_Total)\% czasu procesora** licznika.
    
    * **metricResourceUri**  
    Ta wartość jest identyfikator zasobu hello zestaw skali maszyny wirtualnej hello.
    
    * **ziarnem czasu**  
    Ta wartość jest szczegółowości hello hello metryk, które są zbierane. W tym szablonie ustawiono tooone minutę.
    
    * **Statystyka**  
    Ta wartość określa, jak metryki hello są połączone tooaccommodate hello automatyczne skalowanie akcji. Witaj możliwe wartości to: średnia, Min, Max. W tym szablonie są zbierane hello średni całkowite użycie Procesora hello maszyn wirtualnych.
    
    * **timeWindow**  
    Ta wartość jest hello zakres czasu, w którym są zbierane dane wystąpienia. Musi być od 5 minut do 12 godzin.
    
    * **timeAggregation**  
    jego wartość określa, jak powinny być połączone hello dane, które są zbierane wraz z upływem czasu. Witaj domyślna wartość to średnia. Witaj możliwe wartości to: średnia, co najmniej, maksimum, ostatnich, łączna liczba, liczba.
    
    * **operator**  
    Ta wartość jest hello operator, który jest używany toocompare hello metryki danych i hello próg. Witaj możliwe wartości to: równa, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.
    
    * **Próg**  
    Ta wartość jest wartość hello wyzwala hello akcji skalowania. W tym szablonie maszyn dodanych skali toohello ustawić, gdy hello średniego użycia procesora CPU między maszynami w zestawie hello jest ponad 50%.
    
    * **Kierunek**  
    Ta wartość określa akcji hello, wykonywaną, gdy uzyskuje się hello wartość progową. Witaj możliwe wartości to zwiększyć lub zmniejszyć. W tym szablonie hello liczbę maszyn wirtualnych w zestawie skalowania hello jest zwiększane, gdy próg hello jest ponad 50% hello określone okno czasu.
    
    * **Typ**  
    Ta wartość jest typu hello akcji, która powinna się odbyć i musi być ustawione tooChangeCount.
    
    * **wartość**  
    Ta wartość jest liczbą hello maszyn wirtualnych, które zostały dodane lub usunięte z hello zestaw skali. Ta wartość musi wynosić 1 lub większą. Witaj, wartość domyślna to 1. W tym szablonie hello liczba maszyn w skali hello ustawić zwiększa 1, gdy zostały spełnione warunki progowe hello.
    
    * **cooldown**  
    Ta wartość jest hello ilość czasu toowait od momentu ostatniej akcji skalowania hello, zanim nastąpi hello następnej akcji. Ta wartość musi należeć do zakresu od minutę i jeden tydzień.

12. Zapisz plik szablonu hello.    

## <a name="step-4-upload-hello-template-toostorage"></a>Krok 4: Przekaż hello toostorage szablonu
można przekazać szablon Hello tak długo, jak znana nazwa hello i klucz podstawowy hello konta magazynu, który został utworzony w kroku 1.

1. W oknie programu PowerShell Azure Microsoft hello wartość zmiennej, która określa nazwę hello hello konta magazynu, który został utworzony w kroku 1.
   
    ```powershell
    $storageAccountName = "vmstestsa"
    ```

2. Wartość zmiennej, która określa klucz podstawowy hello hello konta magazynu.
   
    ```powershell
    $storageAccountKey = "<primary-account-key>"
    ```
   
   Ten klucz można uzyskać, klikając ikonę klucza hello podczas wyświetlania zasobów konta magazynu hello w hello portalu Azure.
3. Utworzyć obiekt kontekstu konta magazynu hello, będącą operacji toovalidate używanych z kontem magazynu hello.
   
    ```powershell
    $ctx = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
    ```

4. Tworzenie kontenera hello do przechowywania szablonu hello.

    ```powershell
    $containerName = "templates"
    New-AzureStorageContainer -Name $containerName -Context $ctx  -Permission Blob
    ```

5. Przekaż hello szablon pliku toohello nowego kontenera.

    ```powershell   
    $blobName = "VMSSTemplate.json"
    $fileName = "C:\" + $BlobName
    Set-AzureStorageBlobContent -File $fileName -Container $containerName -Blob  $blobName -Context $ctx
    ```

## <a name="step-5-deploy-hello-template"></a>Krok 5: Wdrożenie hello szablonu
Teraz, gdy utworzono szablon hello, możesz przystąpić do wdrażania hello zasobów. Użyj tego polecenia toostart hello procesu:

```powershell
New-AzureRmResourceGroupDeployment -Name "vmsstestdp1" -ResourceGroupName "vmsstestrg1" -TemplateUri "https://vmsstestsa.blob.core.windows.net/templates/VMSSTemplate.json"
```

Po naciśnięciu wprowadź, zostanie wyświetlony monit o tooprovide wartości zmiennych hello, przypisana. Podaj następujące wartości:

```powershell
vmName: vmsstestvm1
  vmSSName: vmsstest1
  instanceCount: 5
  adminUserName: vmadmin1
  adminPassword: VMpass1
  resourcePrefix: vmsstest
```

Dla wszystkich toosuccessfully zasobów hello można wdrożyć powinien trwa około 15 minut.

> [!NOTE]
> Umożliwia także hello portal możliwości toodeploy hello zasobów. Użyj tego linku: "https://portal.azure.com/#create/Microsoft.Template/uri/<link tooVM Scale Set JSON template>"
> 
> 

## <a name="step-6-monitor-resources"></a>Krok 6: Monitor zasobów
Można uzyskać informacji o zestawy skalowania maszyny wirtualnej za pomocą następujących metod:

* Witaj Azure portal — można obecnie uzyskać ograniczoną ilość informacji za pomocą portalu hello.
* Witaj [Eksploratora zasobów Azure](https://resources.azure.com/) — narzędzie to jest hello najlepsze do eksplorowania hello bieżącego stanu sieci zestawu skali. Tej ścieżki i powinna zostać wyświetlona zestawu widok wystąpienia hello skali hello utworzony:
  
    Subskrypcje > {subskrypcji} > resourceGroups > vmsstestrg1 > dostawców > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > maszyn wirtualnych

* Program Azure PowerShell — Użyj tego polecenia tooget niektóre informacje:

  ```powershell
  Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"
  ```
  
  Lub
  
  ```powershell
  Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceView
  ```

* Połącz toohello oddzielnej maszynie wirtualnej, podobnie jak inne maszyny, a następnie można zdalnie przejść hello maszyn wirtualnych w hello skali zestaw toomonitor poszczególnych procesów.

> [!NOTE]
> Zakończenie interfejsu API REST do uzyskiwania informacji na temat zestawów skalowania można znaleźć w [zestawach skali maszyny wirtualnej](https://msdn.microsoft.com/library/mt589023.aspx)

## <a name="step-7-remove-hello-resources"></a>Krok 7: Usuwanie hello zasobów
Naliczane są opłaty za zasoby używane na platformie Azure, dlatego jest zawsze zasobów toodelete dobrym rozwiązaniem, które nie są już potrzebne. Nie trzeba toodelete każdego zasobu niezależnie od grupy zasobów. Można usunąć grupy zasobów hello i wszystkie jej zasoby są automatycznie usuwane.

  ```powershell
  Remove-AzureRmResourceGroup -Name vmsstestrg1
  ```

Jeśli chcesz tookeep w grupie zasobów, można usunąć tylko zestaw skalowania hello.

  ```powershell
  Remove-AzureRmVmss -ResourceGroupName "resource group name" –VMScaleSetName "scale set name"
  ```

## <a name="next-steps"></a>Następne kroki
* Zarządzanie hello zestaw skali, który został właśnie utworzony przy użyciu informacji hello w [zarządzania maszynami wirtualnymi w zestawie skalowania maszyn wirtualnych](virtual-machine-scale-sets-windows-manage.md).
* Więcej informacji o skalowaniu w pionie zawiera artykuł [Vertical autoscale with Virtual Machine Scale sets](virtual-machine-scale-sets-vertical-scale-reprovision.md) (Automatyczne skalowanie w pionie za pomocą zestawów skalowania maszyn wirtualnych)
* Znajdź przykłady Azure Monitor funkcje w [Azure PowerShell Monitor szybki start — przykłady](../monitoring-and-diagnostics/insights-powershell-samples.md)
* Dowiedz się więcej o funkcji powiadomień w [Użyj skalowania automatycznego akcje toosend poczty e-mail i elementu webhook powiadomień o alertach w monitorze Azure](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)
* Dowiedz się, jak za[dzienniki inspekcji użycia w monitorze Azure, toosend poczty e-mail i elementu webhook powiadomień o alertach](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)

