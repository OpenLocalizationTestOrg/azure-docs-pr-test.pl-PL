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
# <a name="autoscale-using-guest-metrics-in-a-linux-scale-set-template"></a><span data-ttu-id="0ad38-103">Przy użyciu metryk gościa w szablonie Linux zestaw skalowania automatycznego skalowania</span><span class="sxs-lookup"><span data-stu-id="0ad38-103">Autoscale using guest metrics in a Linux scale set template</span></span>

<span data-ttu-id="0ad38-104">Istnieją dwa typy metryki na platformie Azure, które są zbierane z maszyn wirtualnych i skalowanie zestawów: niektóre dostarczanych z hello hosta maszyny Wirtualnej i innych pochodzi z hello gościa maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0ad38-104">There are two types of metrics in Azure that are gathered from VMs and scale sets: some come from hello host VM and others come from hello guest VM.</span></span> <span data-ttu-id="0ad38-105">Metryki hosta nie wymagają dodatkowej konfiguracji ponieważ są one zbierane przez hello hosta maszyny Wirtualnej, metryki gościa wymagają nam tooinstall hello [rozszerzenie systemu Windows Azure Diagnostics](../virtual-machines/windows/extensions-diagnostics-template.md) lub hello [diagnostyki Azure systemu Linux rozszerzenie](../virtual-machines/linux/diagnostic-extension.md) w hello gościa maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0ad38-105">Host metrics do not require additional setup because they are collected by hello host VM, whereas guest metrics require us tooinstall hello [Windows Azure Diagnostics extension](../virtual-machines/windows/extensions-diagnostics-template.md) or hello [Linux Azure Diagnostics extension](../virtual-machines/linux/diagnostic-extension.md) in hello guest VM.</span></span> <span data-ttu-id="0ad38-106">Co typowe przyczyny toouse gościa metryki zamiast metryki hosta jest, że metryki gościa zapewniają większy wybór metryk niż metryki hosta.</span><span class="sxs-lookup"><span data-stu-id="0ad38-106">One common reason toouse guest metrics instead of host metrics is that guest metrics provide a larger selection of metrics than host metrics.</span></span> <span data-ttu-id="0ad38-107">Przykładem takiego jest metryki zużycie pamięci, które są dostępne za pośrednictwem metryki gościa tylko.</span><span class="sxs-lookup"><span data-stu-id="0ad38-107">One such example is memory-consumption metrics, which are only available via guest metrics.</span></span> <span data-ttu-id="0ad38-108">metryki hosta Hello obsługiwane są wyświetlane [tutaj](../monitoring-and-diagnostics/monitoring-supported-metrics.md), i znajduje się gościa często używane metryki [tutaj](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="0ad38-108">hello supported host metrics are listed [here](../monitoring-and-diagnostics/monitoring-supported-metrics.md), and commonly used guest metrics are listed [here](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span></span> <span data-ttu-id="0ad38-109">W tym artykule przedstawiono sposób toomodify hello [minimalnej wielkości Ustaw szablon](./virtual-machine-scale-sets-mvss-start.md) reguł skalowania automatycznego toouse oparciu metryki gościa dla zestawów skalowania systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="0ad38-109">This article shows how toomodify hello [minimum viable scale set template](./virtual-machine-scale-sets-mvss-start.md) toouse autoscale rules based on guest metrics for Linux scale sets.</span></span>

## <a name="change-hello-template-definition"></a><span data-ttu-id="0ad38-110">Zmień hello definicji szablonu</span><span class="sxs-lookup"><span data-stu-id="0ad38-110">Change hello template definition</span></span>

<span data-ttu-id="0ad38-111">Nasze minimalnej wielkości Ustaw szablon może być widoczny [tutaj](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), i widoczne naszych szablon do wdrażania zestaw z gości skalowania automatycznego skalowania Linux hello [tutaj](https://raw.githubusercontent.com/gatneil/mvss/guest-based-autoscale-linux/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="0ad38-111">Our minimum viable scale set template can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), and our template for deploying hello Linux scale set with guest-based autoscale can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/guest-based-autoscale-linux/azuredeploy.json).</span></span> <span data-ttu-id="0ad38-112">Przeanalizujmy hello toocreate różnicowego używany ten szablon (`git diff minimum-viable-scale-set existing-vnet`) element przez element:</span><span class="sxs-lookup"><span data-stu-id="0ad38-112">Let's examine hello diff used toocreate this template (`git diff minimum-viable-scale-set existing-vnet`) piece by piece:</span></span>

<span data-ttu-id="0ad38-113">Najpierw dodamy parametrów `storageAccountName` i `storageAccountSasToken`.</span><span class="sxs-lookup"><span data-stu-id="0ad38-113">First, we add parameters for `storageAccountName` and `storageAccountSasToken`.</span></span> <span data-ttu-id="0ad38-114">agent diagnostyki Hello będą przechowywać dane w [tabeli](../cosmos-db/table-storage-how-to-use-dotnet.md) na tym koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="0ad38-114">hello diagnostics agent will store metric data in a [table](../cosmos-db/table-storage-how-to-use-dotnet.md) in this storage account.</span></span> <span data-ttu-id="0ad38-115">Począwszy od hello Linux diagnostyki agenta w wersji 3.0 lub nowszej za pomocą klucz dostępu do magazynu nie jest już obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="0ad38-115">As of hello Linux Diagnostics Agent version 3.0, using a storage access key is no longer supported.</span></span> <span data-ttu-id="0ad38-116">Możemy użyć [tokenu sygnatury dostępu Współdzielonego](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="0ad38-116">We must use a [SAS Token](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span></span>

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

<span data-ttu-id="0ad38-117">Następnie możemy zmodyfikować zestaw skali hello `extensionProfile` tooinclude hello diagnostyki rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="0ad38-117">Next, we modify hello scale set `extensionProfile` tooinclude hello diagnostics extension.</span></span> <span data-ttu-id="0ad38-118">W tej konfiguracji możemy określić zasób hello ustawiony identyfikator skali hello toocollect metryki z, a także hello konto magazynu i metryki hello toostore toouse tokenu sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="0ad38-118">In this configuration, we specify hello resource ID of hello scale set toocollect metrics from, as well as hello storage account and SAS token toouse toostore hello metrics.</span></span> <span data-ttu-id="0ad38-119">Możemy również określić, jak często metryki hello są agregowane (w tym przypadku co minutę) i które tootrack metryki (w tym przypadku procent używanej pamięci).</span><span class="sxs-lookup"><span data-stu-id="0ad38-119">We also specify how frequently hello metrics are aggregated (in this case every minute) and which metrics tootrack (in this case percent used memory).</span></span> <span data-ttu-id="0ad38-120">Aby uzyskać bardziej szczegółowe informacje dotyczące tej konfiguracji i metryki innego niż % wykorzystanie pamięci, zobacz [tej dokumentacji](../virtual-machines/linux/diagnostic-extension.md).</span><span class="sxs-lookup"><span data-stu-id="0ad38-120">For more detailed information on this configuration and metrics other than percent used memory, see [this documentation](../virtual-machines/linux/diagnostic-extension.md).</span></span>

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

<span data-ttu-id="0ad38-121">Na koniec dodamy `autoscaleSettings` funkcja automatycznego skalowania zasobu tooconfigure oparte na tych metryk.</span><span class="sxs-lookup"><span data-stu-id="0ad38-121">Finally, we add an `autoscaleSettings` resource tooconfigure autoscale based on these metrics.</span></span> <span data-ttu-id="0ad38-122">Ten zasób ma `dependsOn` klauzuli, który odwołuje się do skalowania hello ustawić tooensure, czy istnieje zestaw skali hello przed podjęciem próby wykonania tooautoscale go.</span><span class="sxs-lookup"><span data-stu-id="0ad38-122">This resource has a `dependsOn` clause that references hello scale set tooensure that hello scale set exists before attempting tooautoscale it.</span></span> <span data-ttu-id="0ad38-123">Jeśli wybrany inny tooautoscale metryki na, firma Microsoft użyje hello `counterSpecifier` z konfiguracji rozszerzenia diagnostyki hello jako hello `metricName` hello automatycznego skalowania konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="0ad38-123">If we choose a different metric tooautoscale on, we would use hello `counterSpecifier` from hello diagnostics extension configuration as hello `metricName` in hello autoscale configuration.</span></span> <span data-ttu-id="0ad38-124">Aby uzyskać więcej informacji dotyczących konfiguracji automatycznego skalowania, zobacz hello [najlepsze rozwiązania w zakresie skalowania automatycznego](..//monitoring-and-diagnostics/insights-autoscale-best-practices.md) i hello [dokumentacji interfejsu API REST Monitor Azure](https://msdn.microsoft.com/library/azure/dn931928.aspx).</span><span class="sxs-lookup"><span data-stu-id="0ad38-124">For more information on autoscale configuration, see hello [autoscale best practices](..//monitoring-and-diagnostics/insights-autoscale-best-practices.md) and hello [Azure Monitor REST API reference documentation](https://msdn.microsoft.com/library/azure/dn931928.aspx).</span></span>

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





## <a name="next-steps"></a><span data-ttu-id="0ad38-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0ad38-125">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
