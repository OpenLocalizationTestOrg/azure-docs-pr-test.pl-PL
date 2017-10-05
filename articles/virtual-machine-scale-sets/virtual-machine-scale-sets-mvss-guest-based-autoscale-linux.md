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
# <a name="autoscale-using-guest-metrics-in-a-linux-scale-set-template"></a><span data-ttu-id="231d3-103">Przy użyciu metryk gościa w szablonie Linux zestaw skalowania automatycznego skalowania</span><span class="sxs-lookup"><span data-stu-id="231d3-103">Autoscale using guest metrics in a Linux scale set template</span></span>

<span data-ttu-id="231d3-104">Istnieją dwa typy metryki na platformie Azure, które są zbierane z maszyn wirtualnych i skalowanie zestawów: niektóre pochodzą z hosta maszyny Wirtualnej i innych pochodzi z gościa maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="231d3-104">There are two types of metrics in Azure that are gathered from VMs and scale sets: some come from the host VM and others come from the guest VM.</span></span> <span data-ttu-id="231d3-105">Metryki hosta nie wymagają dodatkowej konfiguracji, ponieważ są one zbierane przez hosta maszyny Wirtualnej, metryki gościa wymagają firmie Microsoft w celu zainstalowania [rozszerzenie systemu Windows Azure Diagnostics](../virtual-machines/windows/extensions-diagnostics-template.md) lub [rozszerzenia diagnostyki Azure systemu Linux ](../virtual-machines/linux/diagnostic-extension.md) na maszynie Wirtualnej gościa.</span><span class="sxs-lookup"><span data-stu-id="231d3-105">Host metrics do not require additional setup because they are collected by the host VM, whereas guest metrics require us to install the [Windows Azure Diagnostics extension](../virtual-machines/windows/extensions-diagnostics-template.md) or the [Linux Azure Diagnostics extension](../virtual-machines/linux/diagnostic-extension.md) in the guest VM.</span></span> <span data-ttu-id="231d3-106">Typową przyczyną metryki gościa zamiast metryki hosta jest, że metryki gościa zapewniają większy wybór metryk niż metryki hosta.</span><span class="sxs-lookup"><span data-stu-id="231d3-106">One common reason to use guest metrics instead of host metrics is that guest metrics provide a larger selection of metrics than host metrics.</span></span> <span data-ttu-id="231d3-107">Przykładem takiego jest metryki zużycie pamięci, które są dostępne za pośrednictwem metryki gościa tylko.</span><span class="sxs-lookup"><span data-stu-id="231d3-107">One such example is memory-consumption metrics, which are only available via guest metrics.</span></span> <span data-ttu-id="231d3-108">Metryki hosta obsługiwane są wyświetlane [tutaj](../monitoring-and-diagnostics/monitoring-supported-metrics.md), i znajduje się gościa często używane metryki [tutaj](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="231d3-108">The supported host metrics are listed [here](../monitoring-and-diagnostics/monitoring-supported-metrics.md), and commonly used guest metrics are listed [here](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span></span> <span data-ttu-id="231d3-109">W tym artykule przedstawiono sposób modyfikowania [minimalnej wielkości Ustaw szablon](./virtual-machine-scale-sets-mvss-start.md) używać reguł skalowania automatycznego oparciu metryki gościa dla zestawów skalowania systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="231d3-109">This article shows how to modify the [minimum viable scale set template](./virtual-machine-scale-sets-mvss-start.md) to use autoscale rules based on guest metrics for Linux scale sets.</span></span>

## <a name="change-the-template-definition"></a><span data-ttu-id="231d3-110">Zmiany definicji szablonu</span><span class="sxs-lookup"><span data-stu-id="231d3-110">Change the template definition</span></span>

<span data-ttu-id="231d3-111">Nasze minimalnej wielkości Ustaw szablon może być widoczny [tutaj](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), i naszych szablonu dla wdrażania skalowania Linux zestawu z gości skalowania automatycznego widoczne [tutaj](https://raw.githubusercontent.com/gatneil/mvss/guest-based-autoscale-linux/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="231d3-111">Our minimum viable scale set template can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), and our template for deploying the Linux scale set with guest-based autoscale can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/guest-based-autoscale-linux/azuredeploy.json).</span></span> <span data-ttu-id="231d3-112">Przeanalizujmy różnicowego używany do tworzenia tego szablonu (`git diff minimum-viable-scale-set existing-vnet`) element przez element:</span><span class="sxs-lookup"><span data-stu-id="231d3-112">Let's examine the diff used to create this template (`git diff minimum-viable-scale-set existing-vnet`) piece by piece:</span></span>

<span data-ttu-id="231d3-113">Najpierw dodamy parametrów `storageAccountName` i `storageAccountSasToken`.</span><span class="sxs-lookup"><span data-stu-id="231d3-113">First, we add parameters for `storageAccountName` and `storageAccountSasToken`.</span></span> <span data-ttu-id="231d3-114">Diagnostyka agenta będą przechowywać dane w [tabeli](../cosmos-db/table-storage-how-to-use-dotnet.md) na tym koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="231d3-114">The diagnostics agent will store metric data in a [table](../cosmos-db/table-storage-how-to-use-dotnet.md) in this storage account.</span></span> <span data-ttu-id="231d3-115">Począwszy od agenta w wersji 3.0 Diagnostyka systemu Linux przy użyciu klucz dostępu do magazynu nie jest już obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="231d3-115">As of the Linux Diagnostics Agent version 3.0, using a storage access key is no longer supported.</span></span> <span data-ttu-id="231d3-116">Możemy użyć [tokenu sygnatury dostępu Współdzielonego](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="231d3-116">We must use a [SAS Token](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span></span>

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

<span data-ttu-id="231d3-117">Następnie możemy zmodyfikować zestaw skalowania `extensionProfile` do rozszerzenie diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="231d3-117">Next, we modify the scale set `extensionProfile` to include the diagnostics extension.</span></span> <span data-ttu-id="231d3-118">W tej konfiguracji możemy Określ identyfikator ID zasobu skali ustawioną zbieranie metryk, a także konta magazynu i tokenu sygnatury dostępu Współdzielonego do przechowywania metryki.</span><span class="sxs-lookup"><span data-stu-id="231d3-118">In this configuration, we specify the resource ID of the scale set to collect metrics from, as well as the storage account and SAS token to use to store the metrics.</span></span> <span data-ttu-id="231d3-119">Możemy również określić, jak często są agregowane metryki (w tym przypadku co minutę) i które metryk do śledzenia (w tym przypadku procent używanej pamięci).</span><span class="sxs-lookup"><span data-stu-id="231d3-119">We also specify how frequently the metrics are aggregated (in this case every minute) and which metrics to track (in this case percent used memory).</span></span> <span data-ttu-id="231d3-120">Aby uzyskać bardziej szczegółowe informacje dotyczące tej konfiguracji i metryki innego niż % wykorzystanie pamięci, zobacz [tej dokumentacji](../virtual-machines/linux/diagnostic-extension.md).</span><span class="sxs-lookup"><span data-stu-id="231d3-120">For more detailed information on this configuration and metrics other than percent used memory, see [this documentation](../virtual-machines/linux/diagnostic-extension.md).</span></span>

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

<span data-ttu-id="231d3-121">Na koniec dodamy `autoscaleSettings` zasobów, aby skonfigurować skalowania automatycznego oparte na tych metryk.</span><span class="sxs-lookup"><span data-stu-id="231d3-121">Finally, we add an `autoscaleSettings` resource to configure autoscale based on these metrics.</span></span> <span data-ttu-id="231d3-122">Ten zasób ma `dependsOn` klauzuli, który odwołuje się do skali ustawioną upewnij się, że zestaw skalowania istnieje przed podjęciem próby automatycznego skalowania go.</span><span class="sxs-lookup"><span data-stu-id="231d3-122">This resource has a `dependsOn` clause that references the scale set to ensure that the scale set exists before attempting to autoscale it.</span></span> <span data-ttu-id="231d3-123">Jeśli wybrany na różne metryki automatycznego skalowania, firma Microsoft użyje `counterSpecifier` z konfiguracji rozszerzenia diagnostyki jako `metricName` w konfiguracji automatycznego skalowania.</span><span class="sxs-lookup"><span data-stu-id="231d3-123">If we choose a different metric to autoscale on, we would use the `counterSpecifier` from the diagnostics extension configuration as the `metricName` in the autoscale configuration.</span></span> <span data-ttu-id="231d3-124">Aby uzyskać więcej informacji dotyczących konfiguracji automatycznego skalowania, zobacz [najlepsze rozwiązania w zakresie skalowania automatycznego](..//monitoring-and-diagnostics/insights-autoscale-best-practices.md) i [dokumentacji interfejsu API REST Monitor Azure](https://msdn.microsoft.com/library/azure/dn931928.aspx).</span><span class="sxs-lookup"><span data-stu-id="231d3-124">For more information on autoscale configuration, see the [autoscale best practices](..//monitoring-and-diagnostics/insights-autoscale-best-practices.md) and the [Azure Monitor REST API reference documentation](https://msdn.microsoft.com/library/azure/dn931928.aspx).</span></span>

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





## <a name="next-steps"></a><span data-ttu-id="231d3-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="231d3-125">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
