---
title: "Automatycznie włączaj ustawień diagnostycznych przy użyciu szablonu usługi Resource Manager | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak szablon Menedżera zasobów do tworzenia ustawień diagnostycznych, które umożliwi strumienia dzienników diagnostycznych do usługi Event Hubs lub przechowywać je na koncie magazynu."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: a8a88a8c-4a48-4df6-8f7e-d90634d39c57
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/14/2017
ms.author: johnkem
ms.openlocfilehash: dde2435e976bbd14ca35cccc714ea21dcc5817b7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="automatically-enable-diagnostic-settings-at-resource-creation-using-a-resource-manager-template"></a><span data-ttu-id="76177-103">Automatycznie włączaj ustawień diagnostycznych na tworzenie zasobów przy użyciu szablonu usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="76177-103">Automatically enable Diagnostic Settings at resource creation using a Resource Manager template</span></span>
<span data-ttu-id="76177-104">W tym artykule zostanie przedstawiony sposób korzystania [szablonu usługi Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) do konfigurowania ustawień diagnostycznych zasobu podczas jego tworzenia.</span><span class="sxs-lookup"><span data-stu-id="76177-104">In this article we show how you can use an [Azure Resource Manager template](../azure-resource-manager/resource-group-authoring-templates.md) to configure Diagnostic Settings on a resource when it is created.</span></span> <span data-ttu-id="76177-105">Umożliwia to automatyczne uruchamianie przesyłanych strumieniowo z dzienników diagnostycznych i metryk do usługi Event Hubs, archiwizacji je na koncie magazynu lub wysyłania ich do analizy dzienników po utworzeniu zasobu.</span><span class="sxs-lookup"><span data-stu-id="76177-105">This enables you to automatically start streaming your Diagnostic Logs and metrics to Event Hubs, archiving them in a Storage Account, or sending them to Log Analytics when a resource is created.</span></span>

<span data-ttu-id="76177-106">Metoda Włączanie dzienników diagnostycznych przy użyciu szablonu usługi Resource Manager zależy od typu zasobu.</span><span class="sxs-lookup"><span data-stu-id="76177-106">The method for enabling Diagnostic Logs using a Resource Manager template depends on the resource type.</span></span>

* <span data-ttu-id="76177-107">**Inne niż obliczeń** używany przez zasoby (na przykład automatyzacji grup zabezpieczeń sieci, Logic Apps) [ustawień diagnostycznych opisane w tym artykule](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).</span><span class="sxs-lookup"><span data-stu-id="76177-107">**Non-Compute** resources (for example, Network Security Groups, Logic Apps, Automation) use [Diagnostic Settings described in this article](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).</span></span>
* <span data-ttu-id="76177-108">**Obliczenia bazy danych** zasobów (WAD/LAD w oparciu o), użyj [WAD/LAD pliku konfiguracji opisanych w tym artykule](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span><span class="sxs-lookup"><span data-stu-id="76177-108">**Compute** (WAD/LAD-based) resources use the [WAD/LAD configuration file described in this article](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span></span>

<span data-ttu-id="76177-109">W tym artykule możemy opisano sposób konfigurowania diagnostyki za pomocą jednej z metod.</span><span class="sxs-lookup"><span data-stu-id="76177-109">In this article we describe how to configure diagnostics using either method.</span></span>

<span data-ttu-id="76177-110">Podstawowe kroki są następujące:</span><span class="sxs-lookup"><span data-stu-id="76177-110">The basic steps are as follows:</span></span>

1. <span data-ttu-id="76177-111">Tworzenie szablonu w formacie JSON, który opisuje sposób utworzenia zasobu i Włącz diagnostykę.</span><span class="sxs-lookup"><span data-stu-id="76177-111">Create a template as a JSON file that describes how to create the resource and enable diagnostics.</span></span>
2. <span data-ttu-id="76177-112">[Wdrażanie szablonu przy użyciu dowolnej metody wdrażania](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="76177-112">[Deploy the template using any deployment method](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

<span data-ttu-id="76177-113">Poniżej możemy podać przykład pliku JSON szablonu, który chcesz wygenerować z systemem innym niż obliczeniowych i zasobów obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="76177-113">Below we give an example of the template JSON file you need to generate for non-Compute and Compute resources.</span></span>

## <a name="non-compute-resource-template"></a><span data-ttu-id="76177-114">Zasób obliczeniowy bez szablonu</span><span class="sxs-lookup"><span data-stu-id="76177-114">Non-Compute resource template</span></span>
<span data-ttu-id="76177-115">Dla zasobów obliczeniowych nie należy wykonać dwie czynności:</span><span class="sxs-lookup"><span data-stu-id="76177-115">For non-Compute resources, you will need to do two things:</span></span>

1. <span data-ttu-id="76177-116">Dodawanie parametrów do obiektu blob parametry dla nazwy konta magazynu, identyfikator reguły magistrali usługi i/lub identyfikator obszaru roboczego analizy dzienników OMS (Włączanie archiwizacji dzienników diagnostycznych na konto magazynu, przesyłania strumieniowego dzienników do usługi Event Hubs i/lub wysyłania dzienników do analizy dzienników).</span><span class="sxs-lookup"><span data-stu-id="76177-116">Add parameters to the parameters blob for the storage account name, service bus rule ID, and/or OMS Log Analytics workspace ID (enabling archival of Diagnostic Logs in a storage account, streaming of logs to Event Hubs, and/or sending logs to Log Analytics).</span></span>
   
    ```json
    "storageAccountName": {
      "type": "string",
      "metadata": {
        "description": "Name of the Storage Account in which Diagnostic Logs should be saved."
      }
    },
    "serviceBusRuleId": {
      "type": "string",
      "metadata": {
        "description": "Service Bus Rule Id for the Service Bus Namespace in which the Event Hub should be created or streamed to."
      }
    },
    "workspaceId":{
      "type": "string",
      "metadata": {
        "description": "Log Analytics workspace ID for the Log Analytics workspace to which logs will be sent."
      }
    }
    ```
2. <span data-ttu-id="76177-117">W tablicy zasobów zasobu, dla którego chcesz włączyć dzienniki diagnostyczne, Dodaj zasób typu `[resource namespace]/providers/diagnosticSettings`.</span><span class="sxs-lookup"><span data-stu-id="76177-117">In the resources array of the resource for which you want to enable Diagnostic Logs, add a resource of type `[resource namespace]/providers/diagnosticSettings`.</span></span>
   
    ```json
    "resources": [
      {
        "type": "providers/diagnosticSettings",
        "name": "Microsoft.Insights/service",
        "dependsOn": [
          "[/*resource Id for which Diagnostic Logs will be enabled>*/]"
        ],
        "apiVersion": "2015-07-01",
        "properties": {
          "storageAccountId": "[resourceId('Microsoft.Storage/storageAccounts', parameters('storageAccountName'))]",
          "serviceBusRuleId": "[parameters('serviceBusRuleId')]",
          "workspaceId": "[parameters('workspaceId')]",
          "logs": [ 
            {
              "category": "/* log category name */",
              "enabled": true,
              "retentionPolicy": {
                "days": 0,
                "enabled": false
              }
            }
          ],
          "metrics": [
            {
              "timeGrain": "PT1M",
              "enabled": true,
              "retentionPolicy": {
                "enabled": false,
                "days": 0
              }
            }
          ]
        }
      }
    ]
    ```

<span data-ttu-id="76177-118">Właściwości obiektu blob dla ustawienie diagnostyczne następuje [opisany w tym artykule](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span><span class="sxs-lookup"><span data-stu-id="76177-118">The properties blob for the Diagnostic Setting follows [the format described in this article](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span> <span data-ttu-id="76177-119">Dodawanie `metrics` właściwości umożliwi to również wysłać metryki zasobów do tych samym dane wyjściowe, pod warunkiem, że [zasób obsługuje metryki Azure Monitor](monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="76177-119">Adding the `metrics` property will enable you to also send resource metrics to these same outputs, provided that [the resource supports Azure Monitor metrics](monitoring-supported-metrics.md).</span></span>

<span data-ttu-id="76177-120">W tym miejscu jest pełny przykład, która tworzy aplikację logiki i włącza opcję przesyłania strumieniowego centra zdarzeń i magazynu w ramach konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="76177-120">Here is a full example that creates a Logic App and turns on streaming to Event Hubs and storage in a storage account.</span></span>

```json

{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "logicAppName": {
      "type": "string",
      "metadata": {
        "description": "Name of the Logic App that will be created."
      }
    },
    "testUri": {
      "type": "string",
      "defaultValue": "http://azure.microsoft.com/en-us/status/feed/"
    },
    "storageAccountName": {
      "type": "string",
      "metadata": {
        "description": "Name of the Storage Account in which Diagnostic Logs should be saved."
      }
    },
    "serviceBusRuleId": {
      "type": "string",
      "metadata": {
        "description": "Service Bus Rule Id for the Service Bus Namespace in which the Event Hub should be created or streamed to."
      }
    },
    "workspaceId": {
      "type": "string",
      "metadata": {
        "description": "Log Analytics workspace ID for the Log Analytics workspace to which logs will be sent."
      }
    }
  },
  "variables": {},
  "resources": [
    {
      "type": "Microsoft.Logic/workflows",
      "name": "[parameters('logicAppName')]",
      "apiVersion": "2016-06-01",
      "location": "[resourceGroup().location]",
      "properties": {
        "definition": {
          "$schema": "http://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
          "contentVersion": "1.0.0.0",
          "parameters": {
            "testURI": {
              "type": "string",
              "defaultValue": "[parameters('testUri')]"
            }
          },
          "triggers": {
            "recurrence": {
              "type": "recurrence",
              "recurrence": {
                "frequency": "Hour",
                "interval": 1
              }
            }
          },
          "actions": {
            "http": {
              "type": "Http",
              "inputs": {
                "method": "GET",
                "uri": "@parameters('testUri')"
              },
              "runAfter": {}
            }
          },
          "outputs": {}
        },
        "parameters": {}
      },
      "resources": [
        {
          "type": "providers/diagnosticSettings",
          "name": "Microsoft.Insights/service",
          "dependsOn": [
            "[resourceId('Microsoft.Logic/workflows', parameters('logicAppName'))]"
          ],
          "apiVersion": "2015-07-01",
          "properties": {
            "storageAccountId": "[resourceId('Microsoft.Storage/storageAccounts', parameters('storageAccountName'))]",
            "serviceBusRuleId": "[parameters('serviceBusRuleId')]",
            "workspaceId": "[parameters('workspaceId')]",
            "logs": [
              {
                "category": "WorkflowRuntime",
                "enabled": true,
                "retentionPolicy": {
                  "days": 0,
                  "enabled": false
                }
              }
            ],
            "metrics": [
              {
                "timeGrain": "PT1M",
                "enabled": true,
                "retentionPolicy": {
                  "enabled": false,
                  "days": 0
                }
              }
            ]
          }
        }
      ],
      "dependsOn": []
    }
  ]
}

```

## <a name="compute-resource-template"></a><span data-ttu-id="76177-121">Obliczenia bazy danych zasobów szablonu</span><span class="sxs-lookup"><span data-stu-id="76177-121">Compute resource template</span></span>
<span data-ttu-id="76177-122">Aby włączyć diagnostykę na zasobów obliczeniowych, na przykład klaster maszyny wirtualnej lub usługi Service Fabric należy:</span><span class="sxs-lookup"><span data-stu-id="76177-122">To enable diagnostics on a Compute resource, for example a Virtual Machine or Service Fabric cluster, you need to:</span></span>

1. <span data-ttu-id="76177-123">Dodaj rozszerzenie diagnostyki Azure w definicji zasobu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="76177-123">Add the Azure Diagnostics extension to the VM resource definition.</span></span>
2. <span data-ttu-id="76177-124">Określ konta i/lub zdarzenia koncentratora magazynu jako parametr.</span><span class="sxs-lookup"><span data-stu-id="76177-124">Specify a storage account and/or event hub as a parameter.</span></span>
3. <span data-ttu-id="76177-125">Dodaj zawartość pliku WADCfg XML do właściwości XMLCfg, prawidłowo anulowanie wszystkich znaków XML.</span><span class="sxs-lookup"><span data-stu-id="76177-125">Add the contents of your WADCfg XML file into the XMLCfg property, escaping all XML characters properly.</span></span>

> [!WARNING]
> <span data-ttu-id="76177-126">Ten ostatni krok mogą być nieco kłopotliwe prawo.</span><span class="sxs-lookup"><span data-stu-id="76177-126">This last step can be tricky to get right.</span></span> <span data-ttu-id="76177-127">[Znajduje się w artykule](../virtual-machines/windows/extensions-diagnostics-template.md#diagnostics-configuration-variables) przykład dzielącą schemat konfiguracji diagnostyki na zmiennych, które są anulowane i prawidłowo sformatowane.</span><span class="sxs-lookup"><span data-stu-id="76177-127">[See this article](../virtual-machines/windows/extensions-diagnostics-template.md#diagnostics-configuration-variables) for an example that splits the Diagnostics Configuration Schema into variables that are escaped and formatted correctly.</span></span>
> 
> 

<span data-ttu-id="76177-128">Cały proces, w tym przykłady, jest opisany [w tym dokumencie](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="76177-128">The entire process, including samples, is described [in this document](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="76177-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="76177-129">Next Steps</span></span>
* [<span data-ttu-id="76177-130">Więcej informacji na temat dzienników diagnostycznych platformy Azure</span><span class="sxs-lookup"><span data-stu-id="76177-130">Read more about Azure Diagnostic Logs</span></span>](monitoring-overview-of-diagnostic-logs.md)
* [<span data-ttu-id="76177-131">Strumienia Azure dzienników diagnostycznych do usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="76177-131">Stream Azure Diagnostic Logs to Event Hubs</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)

