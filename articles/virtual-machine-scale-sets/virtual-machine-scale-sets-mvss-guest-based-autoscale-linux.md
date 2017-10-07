---
title: "Azure automatycznego skalowania za pomocą metryki gościa w szablonie zestaw skalowania systemu Linux | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooautoscale przy użyciu metryk gościa w szablonie zestawu skalowania maszyn wirtualnych systemu Linux"
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
ms.openlocfilehash: 7afbef943a5f15c7a72dcf7114f46d521c504424
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="autoscale-using-guest-metrics-in-a-linux-scale-set-template"></a>Przy użyciu metryk gościa w szablonie Linux zestaw skalowania automatycznego skalowania

Istnieją dwa typy metryki na platformie Azure, które są zbierane z maszyn wirtualnych i skalowanie zestawów: niektóre dostarczanych z hello hosta maszyny Wirtualnej i innych pochodzi z hello gościa maszyny Wirtualnej. Metryki hosta nie wymagają dodatkowej konfiguracji ponieważ są one zbierane przez hello hosta maszyny Wirtualnej, metryki gościa wymagają nam tooinstall hello [rozszerzenie systemu Windows Azure Diagnostics](../virtual-machines/windows/extensions-diagnostics-template.md) lub hello [diagnostyki Azure systemu Linux rozszerzenie](../virtual-machines/linux/diagnostic-extension.md) w hello gościa maszyny Wirtualnej. Co typowe przyczyny toouse gościa metryki zamiast metryki hosta jest, że metryki gościa zapewniają większy wybór metryk niż metryki hosta. Przykładem takiego jest metryki zużycie pamięci, które są dostępne za pośrednictwem metryki gościa tylko. metryki hosta Hello obsługiwane są wyświetlane [tutaj](../monitoring-and-diagnostics/monitoring-supported-metrics.md), i znajduje się gościa często używane metryki [tutaj](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md). W tym artykule przedstawiono sposób toomodify hello [minimalnej wielkości Ustaw szablon](./virtual-machine-scale-sets-mvss-start.md) reguł skalowania automatycznego toouse oparciu metryki gościa dla zestawów skalowania systemu Linux.

## <a name="change-hello-template-definition"></a>Zmień hello definicji szablonu

Nasze minimalnej wielkości Ustaw szablon może być widoczny [tutaj](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), i widoczne naszych szablon do wdrażania zestaw z gości skalowania automatycznego skalowania Linux hello [tutaj](https://raw.githubusercontent.com/gatneil/mvss/guest-based-autoscale-linux/azuredeploy.json). Przeanalizujmy hello toocreate różnicowego używany ten szablon (`git diff minimum-viable-scale-set existing-vnet`) element przez element:

Najpierw dodamy parametrów `storageAccountName` i `storageAccountSasToken`. agent diagnostyki Hello będą przechowywać dane w [tabeli](../cosmos-db/table-storage-how-to-use-dotnet.md) na tym koncie magazynu. Począwszy od hello Linux diagnostyki agenta w wersji 3.0 lub nowszej za pomocą klucz dostępu do magazynu nie jest już obsługiwana. Możemy użyć [tokenu sygnatury dostępu Współdzielonego](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

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

Następnie możemy zmodyfikować zestaw skali hello `extensionProfile` tooinclude hello diagnostyki rozszerzenia. W tej konfiguracji możemy określić zasób hello ustawiony identyfikator skali hello toocollect metryki z, a także hello konto magazynu i metryki hello toostore toouse tokenu sygnatury dostępu Współdzielonego. Możemy również określić, jak często metryki hello są agregowane (w tym przypadku co minutę) i które tootrack metryki (w tym przypadku procent używanej pamięci). Aby uzyskać bardziej szczegółowe informacje dotyczące tej konfiguracji i metryki innego niż % wykorzystanie pamięci, zobacz [tej dokumentacji](../virtual-machines/linux/diagnostic-extension.md).

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

Na koniec dodamy `autoscaleSettings` funkcja automatycznego skalowania zasobu tooconfigure oparte na tych metryk. Ten zasób ma `dependsOn` klauzuli, który odwołuje się do skalowania hello ustawić tooensure, czy istnieje zestaw skali hello przed podjęciem próby wykonania tooautoscale go. Jeśli wybrany inny tooautoscale metryki na, firma Microsoft użyje hello `counterSpecifier` z konfiguracji rozszerzenia diagnostyki hello jako hello `metricName` hello automatycznego skalowania konfiguracji. Aby uzyskać więcej informacji dotyczących konfiguracji automatycznego skalowania, zobacz hello [najlepsze rozwiązania w zakresie skalowania automatycznego](..//monitoring-and-diagnostics/insights-autoscale-best-practices.md) i hello [dokumentacji interfejsu API REST Monitor Azure](https://msdn.microsoft.com/library/azure/dn931928.aspx).

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
