---
title: "tooCreate szablonów usługi Azure Resource Manager aaaUse i konfigurowanie obszaru roboczego analizy dzienników | Dokumentacja firmy Microsoft"
description: "Można użyć toocreate szablonów usługi Azure Resource Manager i skonfigurować analizy dzienników obszarów roboczych."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: jochan
editor: 
ms.assetid: d21ca1b0-847d-4716-bb30-2a8c02a606aa
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: json
ms.topic: article
ms.date: 06/01/2017
ms.author: richrund
ms.openlocfilehash: c8f413e982f5eeed73f463524ff6f239f26c9127
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-log-analytics-using-azure-resource-manager-templates"></a><span data-ttu-id="e911c-103">Zarządzanie za pomocą szablonów usługi Azure Resource Manager analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="e911c-103">Manage Log Analytics using Azure Resource Manager templates</span></span>
<span data-ttu-id="e911c-104">Można użyć [szablonów usługi Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) toocreate i konfigurowanie analizy dzienników obszarów roboczych.</span><span class="sxs-lookup"><span data-stu-id="e911c-104">You can use [Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) toocreate and configure Log Analytics workspaces.</span></span> <span data-ttu-id="e911c-105">Przykłady hello zadań, które można wykonywać za pomocą szablonów:</span><span class="sxs-lookup"><span data-stu-id="e911c-105">Examples of hello tasks you can perform with templates include:</span></span>

* <span data-ttu-id="e911c-106">Tworzenie obszaru roboczego</span><span class="sxs-lookup"><span data-stu-id="e911c-106">Create a workspace</span></span>
* <span data-ttu-id="e911c-107">Dodaj rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="e911c-107">Add a solution</span></span>
* <span data-ttu-id="e911c-108">Tworzenie zapisanych wyszukiwań</span><span class="sxs-lookup"><span data-stu-id="e911c-108">Create saved searches</span></span>
* <span data-ttu-id="e911c-109">Tworzenie grupy komputerów</span><span class="sxs-lookup"><span data-stu-id="e911c-109">Create a computer group</span></span>
* <span data-ttu-id="e911c-110">Włącz zbieranie dzienników usług IIS z komputerów z zainstalowanym agentem systemu Windows hello</span><span class="sxs-lookup"><span data-stu-id="e911c-110">Enable collection of IIS logs from computers with hello Windows agent installed</span></span>
* <span data-ttu-id="e911c-111">Zebrać liczników wydajności z komputerów z systemami Linux i Windows</span><span class="sxs-lookup"><span data-stu-id="e911c-111">Collect performance counters from Linux and Windows computers</span></span>
* <span data-ttu-id="e911c-112">Zbierać zdarzenia z dziennika systemowego na komputerach z systemem Linux</span><span class="sxs-lookup"><span data-stu-id="e911c-112">Collect events from syslog on Linux computers</span></span> 
* <span data-ttu-id="e911c-113">Zbieranie zdarzeń z dzienników zdarzeń systemu Windows</span><span class="sxs-lookup"><span data-stu-id="e911c-113">Collect events from Windows event logs</span></span>
* <span data-ttu-id="e911c-114">Zbieranie dzienników zdarzeń niestandardowych</span><span class="sxs-lookup"><span data-stu-id="e911c-114">Collect custom event logs</span></span>
* <span data-ttu-id="e911c-115">Dodaj hello dziennika analizy agenta tooan maszyny wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e911c-115">Add hello log analytics agent tooan Azure virtual machine</span></span>
* <span data-ttu-id="e911c-116">Skonfiguruj tooindex dane analizy dziennika, zebrane przy użyciu diagnostyki Azure</span><span class="sxs-lookup"><span data-stu-id="e911c-116">Configure log analytics tooindex data collected using Azure diagnostics</span></span>

<span data-ttu-id="e911c-117">Ten artykuł zawiera szablon przykłady ilustrujące niektóre hello konfiguracji, który można wykonać za pomocą szablonów.</span><span class="sxs-lookup"><span data-stu-id="e911c-117">This article provides a template samples that illustrate some of hello configuration that you can perform from templates.</span></span>

## <a name="create-and-configure-a-log-analytics-workspace"></a><span data-ttu-id="e911c-118">Tworzenie i konfigurowanie obszaru roboczego analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="e911c-118">Create and configure a Log Analytics Workspace</span></span>
<span data-ttu-id="e911c-119">Hello Poniższy przykładowy szablon ilustruje sposób:</span><span class="sxs-lookup"><span data-stu-id="e911c-119">hello following template sample illustrates how to:</span></span>

1. <span data-ttu-id="e911c-120">Tworzenie obszaru roboczego, w tym ustawienia przechowywania danych</span><span class="sxs-lookup"><span data-stu-id="e911c-120">Create a workspace, including setting data retention</span></span>
2. <span data-ttu-id="e911c-121">Dodaj obszar roboczy toohello rozwiązań</span><span class="sxs-lookup"><span data-stu-id="e911c-121">Add solutions toohello workspace</span></span>
3. <span data-ttu-id="e911c-122">Tworzenie zapisanych wyszukiwań</span><span class="sxs-lookup"><span data-stu-id="e911c-122">Create saved searches</span></span>
4. <span data-ttu-id="e911c-123">Tworzenie grupy komputerów</span><span class="sxs-lookup"><span data-stu-id="e911c-123">Create a computer group</span></span>
5. <span data-ttu-id="e911c-124">Włącz zbieranie dzienników usług IIS z komputerów z zainstalowanym agentem systemu Windows hello</span><span class="sxs-lookup"><span data-stu-id="e911c-124">Enable collection of IIS logs from computers with hello Windows agent installed</span></span>
6. <span data-ttu-id="e911c-125">Zbierania z komputerów z systemem Linux liczników wydajności dysku logicznego (% użytych węzłów i; Wolne megabajty; % Używane miejsce; Transfery dyskowe/s; Odczyty dysku/s; Zapisy dysku/s)</span><span class="sxs-lookup"><span data-stu-id="e911c-125">Collect Logical Disk perf counters from Linux computers (% Used Inodes; Free Megabytes; % Used Space; Disk Transfers/sec; Disk Reads/sec; Disk Writes/sec)</span></span>
7. <span data-ttu-id="e911c-126">Zbieraj zdarzenia dziennika systemowego z komputerów z systemem Linux</span><span class="sxs-lookup"><span data-stu-id="e911c-126">Collect syslog events from Linux computers</span></span>
8. <span data-ttu-id="e911c-127">Zbieranie zdarzeń błędu i ostrzeżenia z hello dziennik zdarzeń aplikacji z komputerów z systemem Windows</span><span class="sxs-lookup"><span data-stu-id="e911c-127">Collect Error and Warning events from hello Application Event Log from Windows computers</span></span>
9. <span data-ttu-id="e911c-128">Zbieraj dane licznika wydajności dostępna pamięć (MB) z komputerów z systemem Windows</span><span class="sxs-lookup"><span data-stu-id="e911c-128">Collect Memory Available Mbytes performance counter from Windows computers</span></span>
10. <span data-ttu-id="e911c-129">Zbieranie dzienników niestandardowych</span><span class="sxs-lookup"><span data-stu-id="e911c-129">Collect a custom log</span></span> 
11. <span data-ttu-id="e911c-130">Zbieranie dzienników usług IIS i napisane przez konto magazynu diagnostyki Azure tooa dzienniki zdarzeń systemu Windows</span><span class="sxs-lookup"><span data-stu-id="e911c-130">Collect IIS logs and Windows Event logs written by Azure diagnostics tooa storage account</span></span>

```
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "workspaceName": {
      "type": "string",
      "metadata": {
        "description": "workspaceName"
      }
    },
    "serviceTier": {
      "type": "string",
      "allowedValues": [
        "Free",
        "Standalone",
        "PerNode"
      ],
      "metadata": {
        "description": "Service Tier: Free, Standalone, or PerNode"
    }
      },
    "dataRetention": {
      "type": "int",
      "defaultValue": 30,
      "minValue": 7,
      "maxValue": 730,
      "metadata": {
        "description": "Number of days of retention. Free plans can only have 7 days, Standalone and OMS plans include 30 days for free"
      }
    },
    "location": {
      "type": "string",
      "allowedValues": [
        "East US",
        "West Europe",
        "Southeast Asia",
        "Australia Southeast"
      ]
    },
    "applicationDiagnosticsStorageAccountName": {
        "type": "string",
        "metadata": {
          "description": "Name of hello storage account with Azure diagnostics output"
        }
    },
    "applicationDiagnosticsStorageAccountResourceGroup": {
        "type": "string",
        "metadata": {
          "description": "hello resource group name containing hello storage account with Azure diagnostics output"
        }
    }
  },
  "variables": {
    "Updates": {
      "Name": "[Concat('Updates', '(', parameters('workspaceName'), ')')]",
      "GalleryName": "Updates"
    },
    "AntiMalware": {
      "Name": "[concat('AntiMalware', '(', parameters('workspaceName'), ')')]",
      "GalleryName": "AntiMalware"
    },
    "SQLAssessment": {
      "Name": "[Concat('SQLAssessment', '(', parameters('workspaceName'), ')')]",
      "GalleryName": "SQLAssessment"
    },
    "diagnosticsStorageAccount": "[resourceId(parameters('applicationDiagnosticsStorageAccountResourceGroup'), 'Microsoft.Storage/storageAccounts', parameters('applicationDiagnosticsStorageAccountName'))]"
  },
  "resources": [
    {
      "apiVersion": "2015-11-01-preview",
      "type": "Microsoft.OperationalInsights/workspaces",
      "name": "[parameters('workspaceName')]",
      "location": "[parameters('location')]",
      "properties": {
        "sku": {
          "Name": "[parameters('serviceTier')]"
        },
    "retention": "[parameters('dataRetention')]"
      },
      "resources": [
        {
          "apiVersion": "2015-11-01-preview",
          "name": "VMSS Queries2",
          "type": "savedSearches",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "properties": {
            "Category": "VMSS",
            "ETag": "*",
            "DisplayName": "VMSS Instance Count",
            "Query": "Type:Event Source=ServiceFabricNodeBootstrapAgent | dedup Computer | measure count () by Computer",
            "Version": 1
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleWindowsEvent1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "WindowsEvent",
          "properties": {
            "eventLogName": "Application",
            "eventTypes": [
              {
                "eventType": "Error"
              },
              {
                "eventType": "Warning"
              }
            ]
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleWindowsPerfCounter1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "WindowsPerformanceCounter",
          "properties": {
            "objectName": "Memory",
            "instanceName": "*",
            "intervalSeconds": 10,
            "counterName": "Available MBytes"
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleIISLog1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "IISLogs",
          "properties": {
            "state": "OnPremiseEnabled"
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleSyslog1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "LinuxSyslog",
          "properties": {
            "syslogName": "kern",
            "syslogSeverities": [
              {
                "severity": "emerg"
              },
              {
                "severity": "alert"
              },
              {
                "severity": "crit"
              },
              {
                "severity": "err"
              },
              {
                "severity": "warning"
              }
            ]
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleSyslogCollection1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "LinuxSyslogCollection",
          "properties": {
            "state": "Enabled"
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleLinuxPerf1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "LinuxPerformanceObject",
          "properties": {
            "performanceCounters": [
              {
                "counterName": "% Used Inodes"
              },
              {
                "counterName": "Free Megabytes"
              },
              {
                "counterName": "% Used Space"
              },
              {
                "counterName": "Disk Transfers/sec"
              },
              {
                "counterName": "Disk Reads/sec"
              },
              {
                "counterName": "Disk Writes/sec"
              }
            ],
            "objectName": "Logical Disk",
            "instanceName": "*",
            "intervalSeconds": 10
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleLinuxPerfCollection1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "LinuxPerformanceCollection",
          "properties": {
            "state": "Enabled"
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleCustomLog1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "CustomLog",
          "properties": {
            "customLogName": "sampleCustomLog1",
            "description": "test custom log datasources",
            "inputs": [
              {
                "location": {
                  "fileSystemLocations": {
                    "windowsFileTypeLogPaths": [ "e:\\iis5\\*.log" ],
                    "linuxFileTypeLogPaths": [ "/var/logs" ]
                  }
                },
                "recordDelimiter": {
                  "regexDelimiter": {
                    "pattern": "\\n",
                    "matchIndex": 0,
                    "matchIndexSpecified": true,
                    "numberedGroup": null
                  }
                }
              }
            ],
            "extractions": [
              {
                "extractionName": "TimeGenerated",
                "extractionType": "DateTime",
                "extractionProperties": {
                  "dateTimeExtraction": {
                    "regex": null,
                    "joinStringRegex": null
                  }
                }
              }
            ]
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleCustomLogCollection1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "CustomLogCollection",
          "properties": {
            "state": "LinuxLogsEnabled"
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "name": "[concat(parameters('applicationDiagnosticsStorageAccountName'),parameters('workspaceName'))]",
          "type": "storageinsightconfigs",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "properties": {
            "containers": [ 
              "wad-iis-logfiles" 
            ],
            "tables": [
              "WADWindowsEventLogsTable"
            ],
            "storageAccount": {
              "id": "[variables('diagnosticsStorageAccount')]",
              "key": "[listKeys(variables('diagnosticsStorageAccount'),'2015-06-15').key1]"
            }
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "location": "[parameters('location')]",
          "name": "[variables('Updates').Name]",
          "type": "Microsoft.OperationsManagement/solutions",
          "id": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationsManagement/solutions/', variables('Updates').Name)]",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "properties": {
            "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          },
          "plan": {
            "name": "[variables('Updates').Name]",
            "publisher": "Microsoft",
            "product": "[Concat('OMSGallery/', variables('Updates').GalleryName)]",
            "promotionCode": ""
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "location": "[parameters('location')]",
          "name": "[variables('AntiMalware').Name]",
          "type": "Microsoft.OperationsManagement/solutions",
          "id": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationsManagement/solutions/', variables('AntiMalware').Name)]",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "properties": {
            "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          },
          "plan": {
            "name": "[variables('AntiMalware').Name]",
            "publisher": "Microsoft",
            "product": "[Concat('OMSGallery/', variables('AntiMalware').GalleryName)]",
            "promotionCode": ""
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "location": "[parameters('location')]",
          "name": "[variables('SQLAssessment').Name]",
          "type": "Microsoft.OperationsManagement/solutions",
          "id": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationsManagement/solutions/', variables('SQLAssessment').Name)]",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "properties": {
            "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          },
          "plan": {
            "name": "[variables('SQLAssessment').Name]",
            "publisher": "Microsoft",
            "product": "[Concat('OMSGallery/', variables('SQLAssessment').GalleryName)]",
            "promotionCode": ""
          }
        }
      ]
    }
  ],
  "outputs": {
    "workspaceOutput": {
      "value": "[reference(concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName')), '2015-11-01-preview')]",
      "type": "object"
    }
  }
}

```
### <a name="deploying-hello-sample-template"></a><span data-ttu-id="e911c-131">Wdrażanie hello przykładowy szablon</span><span class="sxs-lookup"><span data-stu-id="e911c-131">Deploying hello sample template</span></span>
<span data-ttu-id="e911c-132">toodeploy hello przykładowy szablon:</span><span class="sxs-lookup"><span data-stu-id="e911c-132">toodeploy hello sample template:</span></span>

1. <span data-ttu-id="e911c-133">Na przykład zapisać przykładowe dołączone hello w pliku,`azuredeploy.json`</span><span class="sxs-lookup"><span data-stu-id="e911c-133">Save hello attached sample in a file, for example `azuredeploy.json`</span></span> 
2. <span data-ttu-id="e911c-134">Edytuj hello szablonu toohave hello konfiguracji, który ma</span><span class="sxs-lookup"><span data-stu-id="e911c-134">Edit hello template toohave hello configuration you want</span></span>
3. <span data-ttu-id="e911c-135">Użyj szablonu hello toodeploy wiersza polecenia programu PowerShell lub hello</span><span class="sxs-lookup"><span data-stu-id="e911c-135">Use PowerShell or hello command line toodeploy hello template</span></span>

#### <a name="powershell"></a><span data-ttu-id="e911c-136">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e911c-136">PowerShell</span></span>
`New-AzureRmResourceGroupDeployment -Name <deployment-name> -ResourceGroupName <resource-group-name> -TemplateFile azuredeploy.json`

#### <a name="command-line"></a><span data-ttu-id="e911c-137">Wiersz polecenia</span><span class="sxs-lookup"><span data-stu-id="e911c-137">Command line</span></span>
```
azure config mode arm
azure group deployment create <my-resource-group> <my-deployment-name> --TemplateFile azuredeploy.json
```


## <a name="example-resource-manager-templates"></a><span data-ttu-id="e911c-138">Szablony przykład Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e911c-138">Example Resource Manager templates</span></span>
<span data-ttu-id="e911c-139">Galeria szablonów Szybki Start Azure Hello zawiera kilka szablonów dla analizy dziennika, w tym:</span><span class="sxs-lookup"><span data-stu-id="e911c-139">hello Azure quickstart template gallery includes several templates for Log Analytics, including:</span></span>

* [<span data-ttu-id="e911c-140">Wdróż maszynę wirtualną z systemem Windows z hello rozszerzenia maszyny Wirtualnej analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="e911c-140">Deploy a virtual machine running Windows with hello Log Analytics VM extension</span></span>](https://azure.microsoft.com/documentation/templates/201-oms-extension-windows-vm/)
* [<span data-ttu-id="e911c-141">Wdróż maszynę wirtualną z systemem Linux z hello rozszerzenia maszyny Wirtualnej analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="e911c-141">Deploy a virtual machine running Linux with hello Log Analytics VM extension</span></span>](https://azure.microsoft.com/documentation/templates/201-oms-extension-ubuntu-vm/)
* [<span data-ttu-id="e911c-142">Monitor usługi Azure Site Recovery przy użyciu istniejący obszar roboczy analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="e911c-142">Monitor Azure Site Recovery using an existing Log Analytics workspace</span></span>](https://azure.microsoft.com/documentation/templates/asr-oms-monitoring/)
* [<span data-ttu-id="e911c-143">Monitorowanie aplikacji sieci Web platformy Azure przy użyciu istniejący obszar roboczy analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="e911c-143">Monitor Azure Web Apps using an existing Log Analytics workspace</span></span>](https://azure.microsoft.com/documentation/templates/101-webappazure-oms-monitoring/)
* [<span data-ttu-id="e911c-144">Monitor SQL Azure za pomocą istniejący obszar roboczy analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="e911c-144">Monitor SQL Azure using an existing Log Analytics workspace</span></span>](https://azure.microsoft.com/documentation/templates/101-sqlazure-oms-monitoring/)
* [<span data-ttu-id="e911c-145">Wdrażanie klastra usługi sieć szkieletowa usług i monitorować je z istniejącym obszarem roboczym analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="e911c-145">Deploy a Service Fabric cluster and monitor it with an existing Log Analytics workspace</span></span>](https://azure.microsoft.com/documentation/templates/service-fabric-oms/)
* [<span data-ttu-id="e911c-146">Wdrażanie klastra usługi sieć szkieletowa usług i Utwórz toomonitor obszaru roboczego analizy dzienników go</span><span class="sxs-lookup"><span data-stu-id="e911c-146">Deploy a Service Fabric cluster and create a Log Analytics workspace toomonitor it</span></span>](https://azure.microsoft.com/documentation/templates/service-fabric-vmss-oms/)

## <a name="next-steps"></a><span data-ttu-id="e911c-147">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e911c-147">Next steps</span></span>
* [<span data-ttu-id="e911c-148">Wdrażanie agentów w maszynach wirtualnych platformy Azure przy użyciu szablonów usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e911c-148">Deploy agents into Azure VMs using Resource Manager templates</span></span>](log-analytics-azure-vm-extension.md)

