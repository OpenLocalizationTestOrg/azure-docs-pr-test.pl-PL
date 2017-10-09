---
title: "aaaAutomatically Włącz ustawienia diagnostyki za pomocą szablonu usługi Resource Manager | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse Menedżera zasobów szablonu toocreate diagnostycznych ustawień, które umożliwią toostream Twojego diagnostykę rejestruje koncentratory tooEvent lub przechowywać je na koncie magazynu."
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
ms.openlocfilehash: 8f38731107029928029c6d940da7bd076fea5d49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-enable-diagnostic-settings-at-resource-creation-using-a-resource-manager-template"></a><span data-ttu-id="a275a-103">Automatycznie włączaj ustawień diagnostycznych na tworzenie zasobów przy użyciu szablonu usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a275a-103">Automatically enable Diagnostic Settings at resource creation using a Resource Manager template</span></span>
<span data-ttu-id="a275a-104">W tym artykule zostanie przedstawiony sposób korzystania [szablonu usługi Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) tooconfigure ustawień diagnostycznych dla zasobu podczas jego tworzenia.</span><span class="sxs-lookup"><span data-stu-id="a275a-104">In this article we show how you can use an [Azure Resource Manager template](../azure-resource-manager/resource-group-authoring-templates.md) tooconfigure Diagnostic Settings on a resource when it is created.</span></span> <span data-ttu-id="a275a-105">Dzięki temu tooautomatically rozpoczęcia przesyłania strumieniowego dzienników diagnostycznych i metryki tooEvent koncentratory, archiwizacji je na koncie magazynu lub wysyłania ich tooLog Analytics podczas tworzenia zasobu.</span><span class="sxs-lookup"><span data-stu-id="a275a-105">This enables you tooautomatically start streaming your Diagnostic Logs and metrics tooEvent Hubs, archiving them in a Storage Account, or sending them tooLog Analytics when a resource is created.</span></span>

<span data-ttu-id="a275a-106">Metoda Hello Włączanie dzienników diagnostycznych przy użyciu szablonu usługi Resource Manager zależy od typu zasobu hello.</span><span class="sxs-lookup"><span data-stu-id="a275a-106">hello method for enabling Diagnostic Logs using a Resource Manager template depends on hello resource type.</span></span>

* <span data-ttu-id="a275a-107">**Inne niż obliczeń** używany przez zasoby (na przykład automatyzacji grup zabezpieczeń sieci, Logic Apps) [ustawień diagnostycznych opisane w tym artykule](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).</span><span class="sxs-lookup"><span data-stu-id="a275a-107">**Non-Compute** resources (for example, Network Security Groups, Logic Apps, Automation) use [Diagnostic Settings described in this article](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).</span></span>
* <span data-ttu-id="a275a-108">**Obliczenia bazy danych** (WAD/LAD-zasobów opartych na plikach) Użyj hello [WAD/LAD pliku konfiguracji opisanych w tym artykule](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span><span class="sxs-lookup"><span data-stu-id="a275a-108">**Compute** (WAD/LAD-based) resources use hello [WAD/LAD configuration file described in this article](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span></span>

<span data-ttu-id="a275a-109">W tym artykule opisano sposób diagnostyki tooconfigure za pomocą jednej z metod.</span><span class="sxs-lookup"><span data-stu-id="a275a-109">In this article we describe how tooconfigure diagnostics using either method.</span></span>

<span data-ttu-id="a275a-110">podstawowe kroki Hello są następujące:</span><span class="sxs-lookup"><span data-stu-id="a275a-110">hello basic steps are as follows:</span></span>

1. <span data-ttu-id="a275a-111">Tworzenie szablonu w formacie JSON, który opisuje sposób toocreate hello zasobów i Włącz diagnostykę.</span><span class="sxs-lookup"><span data-stu-id="a275a-111">Create a template as a JSON file that describes how toocreate hello resource and enable diagnostics.</span></span>
2. <span data-ttu-id="a275a-112">[Wdrażanie szablonu hello przy użyciu dowolnej metody wdrażania](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="a275a-112">[Deploy hello template using any deployment method](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

<span data-ttu-id="a275a-113">Poniżej możemy podać przykład hello szablon pliku JSON należy toogenerate z systemem innym niż obliczeniowych i zasobów obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="a275a-113">Below we give an example of hello template JSON file you need toogenerate for non-Compute and Compute resources.</span></span>

## <a name="non-compute-resource-template"></a><span data-ttu-id="a275a-114">Zasób obliczeniowy bez szablonu</span><span class="sxs-lookup"><span data-stu-id="a275a-114">Non-Compute resource template</span></span>
<span data-ttu-id="a275a-115">Dla zasobów obliczeniowych nie są potrzebne toodo dwie czynności:</span><span class="sxs-lookup"><span data-stu-id="a275a-115">For non-Compute resources, you will need toodo two things:</span></span>

1. <span data-ttu-id="a275a-116">Dodaj obiekt blob parametry toohello parametry dla nazwy konta magazynu hello, identyfikator reguły magistrali usługi i/lub identyfikator obszaru roboczego analizy dzienników OMS (Włączanie archiwizacji dzienników diagnostycznych na koncie magazynu, przesyłanie strumieniowe tooEvent dzienniki koncentratorów i/lub wysyłania dzienników tooLog Analytics).</span><span class="sxs-lookup"><span data-stu-id="a275a-116">Add parameters toohello parameters blob for hello storage account name, service bus rule ID, and/or OMS Log Analytics workspace ID (enabling archival of Diagnostic Logs in a storage account, streaming of logs tooEvent Hubs, and/or sending logs tooLog Analytics).</span></span>
   
    ```json
    "storageAccountName": {
      "type": "string",
      "metadata": {
        "description": "Name of hello Storage Account in which Diagnostic Logs should be saved."
      }
    },
    "serviceBusRuleId": {
      "type": "string",
      "metadata": {
        "description": "Service Bus Rule Id for hello Service Bus Namespace in which hello Event Hub should be created or streamed to."
      }
    },
    "workspaceId":{
      "type": "string",
      "metadata": {
        "description": "Log Analytics workspace ID for hello Log Analytics workspace toowhich logs will be sent."
      }
    }
    ```
2. <span data-ttu-id="a275a-117">W tablicy zasobów hello hello zasobu, dla której ma zostać tooenable dzienników diagnostycznych, Dodaj zasób typu `[resource namespace]/providers/diagnosticSettings`.</span><span class="sxs-lookup"><span data-stu-id="a275a-117">In hello resources array of hello resource for which you want tooenable Diagnostic Logs, add a resource of type `[resource namespace]/providers/diagnosticSettings`.</span></span>
   
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

<span data-ttu-id="a275a-118">Hello obiektu blob właściwości dla hello ustawienie diagnostyczne następuje [format hello opisane w tym artykule](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span><span class="sxs-lookup"><span data-stu-id="a275a-118">hello properties blob for hello Diagnostic Setting follows [hello format described in this article](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span> <span data-ttu-id="a275a-119">Dodawanie hello `metrics` właściwość spowoduje włączenie wysyłania tooalso zasobu metryki toothese sam danych wyjściowych, pod warunkiem, że [zasób hello obsługuje metryki Azure Monitor](monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="a275a-119">Adding hello `metrics` property will enable you tooalso send resource metrics toothese same outputs, provided that [hello resource supports Azure Monitor metrics](monitoring-supported-metrics.md).</span></span>

<span data-ttu-id="a275a-120">W tym miejscu jest pełny przykład, która tworzy aplikację logiki i włącza opcję przesyłania strumieniowego tooEvent koncentratorów i magazynu w ramach konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="a275a-120">Here is a full example that creates a Logic App and turns on streaming tooEvent Hubs and storage in a storage account.</span></span>

```json

{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "logicAppName": {
      "type": "string",
      "metadata": {
        "description": "Name of hello Logic App that will be created."
      }
    },
    "testUri": {
      "type": "string",
      "defaultValue": "http://azure.microsoft.com/en-us/status/feed/"
    },
    "storageAccountName": {
      "type": "string",
      "metadata": {
        "description": "Name of hello Storage Account in which Diagnostic Logs should be saved."
      }
    },
    "serviceBusRuleId": {
      "type": "string",
      "metadata": {
        "description": "Service Bus Rule Id for hello Service Bus Namespace in which hello Event Hub should be created or streamed to."
      }
    },
    "workspaceId": {
      "type": "string",
      "metadata": {
        "description": "Log Analytics workspace ID for hello Log Analytics workspace toowhich logs will be sent."
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

## <a name="compute-resource-template"></a><span data-ttu-id="a275a-121">Obliczenia bazy danych zasobów szablonu</span><span class="sxs-lookup"><span data-stu-id="a275a-121">Compute resource template</span></span>
<span data-ttu-id="a275a-122">Diagnostyka tooenable w zasobie obliczeń, na przykład maszynę wirtualną lub klastra sieci szkieletowej usług, musisz:</span><span class="sxs-lookup"><span data-stu-id="a275a-122">tooenable diagnostics on a Compute resource, for example a Virtual Machine or Service Fabric cluster, you need to:</span></span>

1. <span data-ttu-id="a275a-123">Dodawanie definicji zasobu hello Azure Diagnostics rozszerzenia toohello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a275a-123">Add hello Azure Diagnostics extension toohello VM resource definition.</span></span>
2. <span data-ttu-id="a275a-124">Określ konta i/lub zdarzenia koncentratora magazynu jako parametr.</span><span class="sxs-lookup"><span data-stu-id="a275a-124">Specify a storage account and/or event hub as a parameter.</span></span>
3. <span data-ttu-id="a275a-125">Dodaj hello zawartość pliku WADCfg XML do właściwości XMLCfg hello, prawidłowo anulowanie wszystkich znaków XML.</span><span class="sxs-lookup"><span data-stu-id="a275a-125">Add hello contents of your WADCfg XML file into hello XMLCfg property, escaping all XML characters properly.</span></span>

> [!WARNING]
> <span data-ttu-id="a275a-126">Ten ostatni krok można trudnych tooget prawo.</span><span class="sxs-lookup"><span data-stu-id="a275a-126">This last step can be tricky tooget right.</span></span> <span data-ttu-id="a275a-127">[Znajduje się w artykule](../virtual-machines/windows/extensions-diagnostics-template.md#diagnostics-configuration-variables) na przykład, że podziałów hello schemat konfiguracji diagnostyki do zmiennych, które są anulowane i poprawnie sformatowany.</span><span class="sxs-lookup"><span data-stu-id="a275a-127">[See this article](../virtual-machines/windows/extensions-diagnostics-template.md#diagnostics-configuration-variables) for an example that splits hello Diagnostics Configuration Schema into variables that are escaped and formatted correctly.</span></span>
> 
> 

<span data-ttu-id="a275a-128">Witaj cały proces, w tym przykłady, jest opisany [w tym dokumencie](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a275a-128">hello entire process, including samples, is described [in this document](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a275a-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a275a-129">Next Steps</span></span>
* [<span data-ttu-id="a275a-130">Więcej informacji na temat dzienników diagnostycznych platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a275a-130">Read more about Azure Diagnostic Logs</span></span>](monitoring-overview-of-diagnostic-logs.md)
* [<span data-ttu-id="a275a-131">Strumień dzienników diagnostycznych platformy Azure tooEvent koncentratory</span><span class="sxs-lookup"><span data-stu-id="a275a-131">Stream Azure Diagnostic Logs tooEvent Hubs</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)

