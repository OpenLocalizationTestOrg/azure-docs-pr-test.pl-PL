---
title: "Azure automatycznego skalowania za pomocą metryki gościa w szablonie zestaw skalowania systemu Linux | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak w szablonie zestawu skalowania maszyn wirtualnych systemu Linux przy użyciu gościa metryki automatycznego skalowania"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: na
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: negat
ms.openlocfilehash: ac0bbb4dbfccca3f3fc31526aeff11afe55d44be
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="autoscale-using-guest-metrics-in-a-linux-scale-set-template"></a>Przy użyciu metryk gościa w szablonie Linux zestaw skalowania automatycznego skalowania

Istnieją dwa typy metryki na platformie Azure, które są zbierane z maszyn wirtualnych i skalowanie zestawów: niektóre pochodzą z hosta maszyny Wirtualnej i innych pochodzi z gościa maszyny Wirtualnej. Metryki hosta nie wymagają dodatkowej konfiguracji, ponieważ są one zbierane przez hosta maszyny Wirtualnej, metryki gościa wymagają firmie Microsoft w celu zainstalowania [rozszerzenie systemu Windows Azure Diagnostics](../virtual-machines/windows/extensions-diagnostics-template.md) lub [rozszerzenia diagnostyki Azure systemu Linux ](../virtual-machines/linux/diagnostic-extension.md) na maszynie Wirtualnej gościa. Typową przyczyną metryki gościa zamiast metryki hosta jest, że metryki gościa zapewniają większy wybór metryk niż metryki hosta. Przykładem takiego jest metryki zużycie pamięci, które są dostępne za pośrednictwem metryki gościa tylko. Metryki hosta obsługiwane są wyświetlane [tutaj](../monitoring-and-diagnostics/monitoring-supported-metrics.md), i znajduje się gościa często używane metryki [tutaj](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md). W tym artykule przedstawiono sposób modyfikowania [minimalnej wielkości Ustaw szablon](./virtual-machine-scale-sets-mvss-start.md) używać reguł skalowania automatycznego oparciu metryki gościa dla zestawów skalowania systemu Linux.

## <a name="change-the-template-definition"></a>Zmiany definicji szablonu

Nasze minimalnej wielkości Ustaw szablon może być widoczny [tutaj](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), i naszych szablonu dla wdrażania skalowania Linux zestawu z gości skalowania automatycznego widoczne [tutaj](https://raw.githubusercontent.com/gatneil/mvss/guest-based-autoscale-linux/azuredeploy.json). Przeanalizujmy różnicowego używany do tworzenia tego szablonu (`git diff minimum-viable-scale-set existing-vnet`) element przez element:

Najpierw dodamy parametrów `storageAccountName` i `storageAccountSasToken`. Diagnostyka agenta będą przechowywać dane w [tabeli](../cosmos-db/table-storage-how-to-use-dotnet.md) na tym koncie magazynu. Począwszy od agenta w wersji 3.0 Diagnostyka systemu Linux przy użyciu klucz dostępu do magazynu nie jest już obsługiwana. Możemy użyć [tokenu sygnatury dostępu Współdzielonego](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

```diff
     },
     "adminPassword": {
       "type": "securestring"
+    },
+    "storageAccountName": {
+      "type": "string"
+    },
+    "storageAccountSasToken": {
+      "type": "securestring"
     }
   },
```

Następnie możemy zmodyfikować zestaw skalowania `extensionProfile` do rozszerzenie diagnostyki. W tej konfiguracji możemy Określ identyfikator ID zasobu skali ustawioną zbieranie metryk, a także konta magazynu i tokenu sygnatury dostępu Współdzielonego do przechowywania metryki. Możemy również określić, jak często są agregowane metryki (w tym przypadku co minutę) i które metryk do śledzenia (w tym przypadku procent używanej pamięci). Aby uzyskać bardziej szczegółowe informacje dotyczące tej konfiguracji i metryki innego niż % wykorzystanie pamięci, zobacz [tej dokumentacji](../virtual-machines/linux/diagnostic-extension.md).

```diff
                 }
               }
             ]
+          },
+          "extensionProfile": {
+            "extensions": [
+              {
+                "name": "LinuxDiagnosticExtension",
+                "properties": {
+                  "publisher": "Microsoft.Azure.Diagnostics",
+                  "type": "LinuxDiagnostic",
+                  "typeHandlerVersion": "3.0",
+                  "settings": {
+                    "StorageAccount": "[parameters('storageAccountName')]",
+                    "ladCfg": {
+                      "diagnosticMonitorConfiguration": {
+                        "performanceCounters": {
+                          "sinks": "WADMetricJsonBlob",
+                          "performanceCounterConfiguration": [
+                            {
+                              "unit": "percent",
+                              "type": "builtin",
+                              "class": "memory",
+                              "counter": "percentUsedMemory",
+                              "counterSpecifier": "/builtin/memory/percentUsedMemory",
+                              "condition": "IsAggregate=TRUE"
+                            }
+                          ]
+                        },
+                        "metrics": {
+                          "metricAggregation": [
+                            {
+                              "scheduledTransferPeriod": "PT1M"
+                            }
+                          ],
+                          "resourceId": "[resourceId('Microsoft.Compute/virtualMachineScaleSets', 'myScaleSet')]"
+                        }
+                      }
+                    }
+                  },
+                  "protectedSettings": {
+                    "storageAccountName": "[parameters('storageAccountName')]",
+                    "storageAccountSasToken": "[parameters('storageAccountSasToken')]",
+                    "sinksConfig": {
+                      "sink": [
+                        {
+                          "name": "WADMetricJsonBlob",
+                          "type": "JsonBlob"
+                        }
+                      ]
+                    }
+                  }
+                }
+              }
+            ]
           }
         }
       }
```

Na koniec dodamy `autoscaleSettings` zasobów, aby skonfigurować skalowania automatycznego oparte na tych metryk. Ten zasób ma `dependsOn` klauzuli, który odwołuje się do skali ustawioną upewnij się, że zestaw skalowania istnieje przed podjęciem próby automatycznego skalowania go. Jeśli wybrany na różne metryki automatycznego skalowania, firma Microsoft użyje `counterSpecifier` z konfiguracji rozszerzenia diagnostyki jako `metricName` w konfiguracji automatycznego skalowania. Aby uzyskać więcej informacji dotyczących konfiguracji automatycznego skalowania, zobacz [najlepsze rozwiązania w zakresie skalowania automatycznego](..//monitoring-and-diagnostics/insights-autoscale-best-practices.md) i [dokumentacji interfejsu API REST Monitor Azure](https://msdn.microsoft.com/library/azure/dn931928.aspx).

```diff
+    },
+    {
+      "type": "Microsoft.Insights/autoscaleSettings",
+      "apiVersion": "2015-04-01",
+      "name": "guestMetricsAutoscale",
+      "location": "[resourceGroup().location]",
+      "dependsOn": [
+        "Microsoft.Compute/virtualMachineScaleSets/myScaleSet"
+      ],
+      "properties": {
+        "name": "guestMetricsAutoscale",
+        "targetResourceUri": "[resourceId('Microsoft.Compute/virtualMachineScaleSets', 'myScaleSet')]",
+        "enabled": true,
+        "profiles": [
+          {
+            "name": "Profile1",
+            "capacity": {
+              "minimum": "1",
+              "maximum": "10",
+              "default": "3"
+            },
+            "rules": [
+              {
+                "metricTrigger": {
+                  "metricName": "/builtin/memory/percentUsedMemory",
+                  "metricNamespace": "",
+                  "metricResourceUri": "[resourceId('Microsoft.Compute/virtualMachineScaleSets', 'myScaleSet')]",
+                  "timeGrain": "PT1M",
+                  "statistic": "Average",
+                  "timeWindow": "PT5M",
+                  "timeAggregation": "Average",
+                  "operator": "GreaterThan",
+                  "threshold": 60
+                },
+                "scaleAction": {
+                  "direction": "Increase",
+                  "type": "ChangeCount",
+                  "value": "1",
+                  "cooldown": "PT1M"
+                }
+              },
+              {
+                "metricTrigger": {
+                  "metricName": "/builtin/memory/percentUsedMemory",
+                  "metricNamespace": "",
+                  "metricResourceUri": "[resourceId('Microsoft.Compute/virtualMachineScaleSets', 'myScaleSet')]",
+                  "timeGrain": "PT1M",
+                  "statistic": "Average",
+                  "timeWindow": "PT5M",
+                  "timeAggregation": "Average",
+                  "operator": "LessThan",
+                  "threshold": 30
+                },
+                "scaleAction": {
+                  "direction": "Decrease",
+                  "type": "ChangeCount",
+                  "value": "1",
+                  "cooldown": "PT1M"
+                }
+              }
+            ]
+          }
+        ]
+      }
     }
   ]
 }
```





## <a name="next-steps"></a>Następne kroki

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
