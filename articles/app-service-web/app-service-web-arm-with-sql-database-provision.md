---
title: "Udostępniać aplikacji sieci web, który korzysta z bazy danych SQL"
description: "Wdrażanie aplikacji sieci web, który zawiera bazę danych SQL za pomocą szablonu usługi Azure Resource Manager."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: fb9648e1-9bf2-4537-bc4a-ab8d4953168c
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2016
ms.author: cephalin
ms.openlocfilehash: cc34f684f8c50e95a62cb7b04fd2ddce5deb68d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="provision-a-web-app-with-a-sql-database"></a><span data-ttu-id="d8823-103">Udostępniać aplikacji sieci web z bazą danych SQL</span><span class="sxs-lookup"><span data-stu-id="d8823-103">Provision a web app with a SQL Database</span></span>
<span data-ttu-id="d8823-104">W tym temacie dowiesz się, jak utworzyć szablon usługi Azure Resource Manager, która wdraża aplikację sieci web i bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="d8823-104">In this topic, you will learn how to create an Azure Resource Manager template that deploys a web app and SQL Database.</span></span> <span data-ttu-id="d8823-105">Dowiesz się, jak do definiowania zasobów, do których są wdrażane i sposób definiowania parametrów, które są określone, gdy wdrożenie jest wykonywane.</span><span class="sxs-lookup"><span data-stu-id="d8823-105">You will learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="d8823-106">Można użyć tego szablonu na potrzeby własnych wdrożeń lub dostosować go do konkretnych potrzeb.</span><span class="sxs-lookup"><span data-stu-id="d8823-106">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="d8823-107">Aby uzyskać więcej informacji na temat tworzenia szablonów, zobacz [Authoring Azure Resource Manager szablony](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="d8823-107">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="d8823-108">Aby uzyskać więcej informacji na temat wdrażania aplikacji, zobacz [wdrażanie złożonych aplikacji przewidywalnego na platformie Azure](app-service-deploy-complex-application-predictably.md).</span><span class="sxs-lookup"><span data-stu-id="d8823-108">For more information about deploying apps, see [Deploy a complex application predictably in Azure](app-service-deploy-complex-application-predictably.md).</span></span>

<span data-ttu-id="d8823-109">Zakończenie szablonu, zobacz [szablonu aplikacji sieci Web z SQL Database](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-sql-database/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="d8823-109">For the complete template, see [Web App With SQL Database template](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-sql-database/azuredeploy.json).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-deploy"></a><span data-ttu-id="d8823-110">Zostanie wdrożona</span><span class="sxs-lookup"><span data-stu-id="d8823-110">What you will deploy</span></span>
<span data-ttu-id="d8823-111">W tym szablonie zostanie wdrożona:</span><span class="sxs-lookup"><span data-stu-id="d8823-111">In this template, you will deploy:</span></span>

* <span data-ttu-id="d8823-112">Aplikacja sieci web</span><span class="sxs-lookup"><span data-stu-id="d8823-112">a web app</span></span>
* <span data-ttu-id="d8823-113">Serwer bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="d8823-113">SQL Database server</span></span>
* <span data-ttu-id="d8823-114">SQL Database</span><span class="sxs-lookup"><span data-stu-id="d8823-114">SQL Database</span></span>
* <span data-ttu-id="d8823-115">Ustawienia skalowania automatycznego</span><span class="sxs-lookup"><span data-stu-id="d8823-115">AutoScale settings</span></span>
* <span data-ttu-id="d8823-116">Reguły alertów</span><span class="sxs-lookup"><span data-stu-id="d8823-116">Alert rules</span></span>
* <span data-ttu-id="d8823-117">Szczegółowe informacje w aplikacji</span><span class="sxs-lookup"><span data-stu-id="d8823-117">App Insights</span></span>

<span data-ttu-id="d8823-118">Aby automatycznie uruchomić wdrożenie, kliknij poniższy przycisk:</span><span class="sxs-lookup"><span data-stu-id="d8823-118">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="d8823-119">[![Wdrażanie na platformie Azure](./media/app-service-web-arm-with-sql-database-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-sql-database%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="d8823-119">[![Deploy to Azure](./media/app-service-web-arm-with-sql-database-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-sql-database%2Fazuredeploy.json)</span></span>

## <a name="parameters-to-specify"></a><span data-ttu-id="d8823-120">W celu określenia</span><span class="sxs-lookup"><span data-stu-id="d8823-120">Parameters to specify</span></span>
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

### <a name="administratorlogin"></a><span data-ttu-id="d8823-121">administratorLogin</span><span class="sxs-lookup"><span data-stu-id="d8823-121">administratorLogin</span></span>
<span data-ttu-id="d8823-122">Nazwa konta do użycia dla administratora serwera bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d8823-122">The account name to use for the database server administrator.</span></span>

    "administratorLogin": {
      "type": "string"
    }

### <a name="administratorloginpassword"></a><span data-ttu-id="d8823-123">administratorLoginPassword</span><span class="sxs-lookup"><span data-stu-id="d8823-123">administratorLoginPassword</span></span>
<span data-ttu-id="d8823-124">Hasło do użycia dla administratora serwera bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d8823-124">The password to use for the database server administrator.</span></span>

    "administratorLoginPassword": {
      "type": "securestring"
    }

### <a name="databasename"></a><span data-ttu-id="d8823-125">DatabaseName</span><span class="sxs-lookup"><span data-stu-id="d8823-125">databaseName</span></span>
<span data-ttu-id="d8823-126">Nazwa nowej bazy danych do utworzenia.</span><span class="sxs-lookup"><span data-stu-id="d8823-126">The name of the new database to create.</span></span>

    "databaseName": {
      "type": "string",
      "defaultValue": "sampledb"
    }

### <a name="collation"></a><span data-ttu-id="d8823-127">Sortowanie</span><span class="sxs-lookup"><span data-stu-id="d8823-127">collation</span></span>
<span data-ttu-id="d8823-128">Sortowanie bazy danych do użycia na potrzeby użycia prawidłowego znaków.</span><span class="sxs-lookup"><span data-stu-id="d8823-128">The database collation to use for governing the proper use of characters.</span></span>

    "collation": {
      "type": "string",
      "defaultValue": "SQL_Latin1_General_CP1_CI_AS"
    }

### <a name="edition"></a><span data-ttu-id="d8823-129">Edition</span><span class="sxs-lookup"><span data-stu-id="d8823-129">edition</span></span>
<span data-ttu-id="d8823-130">Typ bazy danych do utworzenia.</span><span class="sxs-lookup"><span data-stu-id="d8823-130">The type of database to create.</span></span>

    "edition": {
      "type": "string",
      "defaultValue": "Basic",
      "allowedValues": [
        "Basic",
        "Standard",
        "Premium"
      ],
      "metadata": {
        "description": "The type of database to create."
      }
    }

### <a name="maxsizebytes"></a><span data-ttu-id="d8823-131">maxSizeBytes</span><span class="sxs-lookup"><span data-stu-id="d8823-131">maxSizeBytes</span></span>
<span data-ttu-id="d8823-132">Maksymalny rozmiar w bajtach dla bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d8823-132">The maximum size, in bytes, for the database.</span></span>

    "maxSizeBytes": {
      "type": "string",
      "defaultValue": "1073741824"
    }

### <a name="requestedserviceobjectivename"></a><span data-ttu-id="d8823-133">requestedServiceObjectiveName</span><span class="sxs-lookup"><span data-stu-id="d8823-133">requestedServiceObjectiveName</span></span>
<span data-ttu-id="d8823-134">Nazwa odpowiadającego poziom wydajności dla wersji.</span><span class="sxs-lookup"><span data-stu-id="d8823-134">The name corresponding to the performance level for edition.</span></span> 

    "requestedServiceObjectiveName": {
      "type": "string",
      "defaultValue": "Basic",
      "allowedValues": [
        "Basic",
        "S0",
        "S1",
        "S2",
        "P1",
        "P2",
        "P3"
      ],
      "metadata": {
        "description": "Describes the performance level for Edition"
      }
    }

## <a name="variables-for-names"></a><span data-ttu-id="d8823-135">Zmienne dla nazwy</span><span class="sxs-lookup"><span data-stu-id="d8823-135">Variables for names</span></span>
<span data-ttu-id="d8823-136">Ten szablon obejmuje zmiennych, które konstruowania nazwy używane w szablonie.</span><span class="sxs-lookup"><span data-stu-id="d8823-136">This template includes variables that construct names used in the template.</span></span> <span data-ttu-id="d8823-137">Użyj wartości zmiennej **uniqueString** funkcji, aby wygenerować nazwę na podstawie identyfikatora grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="d8823-137">The variable values use the **uniqueString** function to generate a name from the resource group id.</span></span>

    "variables": {
        "hostingPlanName": "[concat('hostingplan', uniqueString(resourceGroup().id))]",
        "webSiteName": "[concat('webSite', uniqueString(resourceGroup().id))]",
        "sqlserverName": "[concat('sqlserver', uniqueString(resourceGroup().id))]"
    },


## <a name="resources-to-deploy"></a><span data-ttu-id="d8823-138">Zasoby wymagające wdrożenia</span><span class="sxs-lookup"><span data-stu-id="d8823-138">Resources to deploy</span></span>
### <a name="sql-server-and-database"></a><span data-ttu-id="d8823-139">SQL Server i bazy danych</span><span class="sxs-lookup"><span data-stu-id="d8823-139">SQL Server and Database</span></span>
<span data-ttu-id="d8823-140">Tworzy nowy program SQL Server i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d8823-140">Creates a new SQL Server and database.</span></span> <span data-ttu-id="d8823-141">Nazwa serwera jest określona w **serverName** parametr i lokalizacji określonej w **serverLocation** parametru.</span><span class="sxs-lookup"><span data-stu-id="d8823-141">The name of the server is specified in the **serverName** parameter and the location specified in the **serverLocation** parameter.</span></span> <span data-ttu-id="d8823-142">Podczas tworzenia nowego serwera, podaj nazwę logowania i hasło administratora serwera bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d8823-142">When creating the new server, you must provide a login name and password for the database server administrator.</span></span> 

    {
      "name": "[variables('sqlserverName')]",
      "type": "Microsoft.Sql/servers",
      "location": "[resourceGroup().location]",
      "tags": {
        "displayName": "SqlServer"
      },
      "apiVersion": "2014-04-01-preview",
      "properties": {
        "administratorLogin": "[parameters('administratorLogin')]",
        "administratorLoginPassword": "[parameters('administratorLoginPassword')]"
      },
      "resources": [
        {
          "name": "[parameters('databaseName')]",
          "type": "databases",
          "location": "[resourceGroup().location]",
          "tags": {
            "displayName": "Database"
          },
          "apiVersion": "2014-04-01-preview",
          "dependsOn": [
            "[variables('sqlserverName')]"
          ],
          "properties": {
            "edition": "[parameters('edition')]",
            "collation": "[parameters('collation')]",
            "maxSizeBytes": "[parameters('maxSizeBytes')]",
            "requestedServiceObjectiveName": "[parameters('requestedServiceObjectiveName')]"
          }
        },
        {
          "type": "firewallrules",
          "apiVersion": "2014-04-01-preview",
          "dependsOn": [
            "[variables('sqlserverName')]"
          ],
          "location": "[resourceGroup().location]",
          "name": "AllowAllAzureIps",
          "properties": {
            "endIpAddress": "0.0.0.0",
            "startIpAddress": "0.0.0.0"
          }
        }
      ]
    },

[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="web-app"></a><span data-ttu-id="d8823-143">Aplikacja internetowa</span><span class="sxs-lookup"><span data-stu-id="d8823-143">Web app</span></span>
    {
      "apiVersion": "2015-08-01",
      "name": "[variables('webSiteName')]",
      "type": "Microsoft.Web/sites",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[variables('hostingPlanName')]"
      ],
      "tags": {
        "[concat('hidden-related:', resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName')))]": "empty",
        "displayName": "Website"
      },
      "properties": {
        "name": "[variables('webSiteName')]",
        "serverFarmId": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]"
      },
      "resources": [
        {
          "apiVersion": "2015-08-01",
          "type": "config",
          "name": "connectionstrings",
          "dependsOn": [
            "[variables('webSiteName')]"
          ],
          "properties": {
            "DefaultConnection": {
              "value": "[concat('Data Source=tcp:', reference(concat('Microsoft.Sql/servers/', variables('sqlserverName'))).fullyQualifiedDomainName, ',1433;Initial Catalog=', parameters('databaseName'), ';User Id=', parameters('administratorLogin'), '@', variables('sqlserverName'), ';Password=', parameters('administratorLoginPassword'), ';')]",
              "type": "SQLServer"
            }
          }
        }
      ]
    },


### <a name="autoscale"></a><span data-ttu-id="d8823-144">Automatyczne skalowanie</span><span class="sxs-lookup"><span data-stu-id="d8823-144">AutoScale</span></span>
    {
      "apiVersion": "2014-04-01",
      "name": "[concat(variables('hostingPlanName'), '-', resourceGroup().name)]",
      "type": "Microsoft.Insights/autoscalesettings",
      "location": "[resourceGroup().location]",
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName')))]": "Resource",
        "displayName": "AutoScaleSettings"
      },
      "dependsOn": [
        "[variables('hostingPlanName')]"
      ],
      "properties": {
        "profiles": [
          {
            "name": "Default",
            "capacity": {
              "minimum": 1,
              "maximum": 2,
              "default": 1
            },
            "rules": [
              {
                "metricTrigger": {
                  "metricName": "CpuPercentage",
                  "metricResourceUri": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
                  "timeGrain": "PT1M",
                  "statistic": "Average",
                  "timeWindow": "PT10M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 80.0
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": 1,
                  "cooldown": "PT10M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "CpuPercentage",
                  "metricResourceUri": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
                  "timeGrain": "PT1M",
                  "statistic": "Average",
                  "timeWindow": "PT1H",
                  "timeAggregation": "Average",
                  "operator": "LessThan",
                  "threshold": 60.0
                },
                "scaleAction": {
                  "direction": "Decrease",
                  "type": "ChangeCount",
                  "value": 1,
                  "cooldown": "PT1H"
                }
              }
            ]
          }
        ],
        "enabled": false,
        "name": "[concat(variables('hostingPlanName'), '-', resourceGroup().name)]",
        "targetResourceUri": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]"
      }
    },


### <a name="alert-rules-for-status-codes-403-and-500s-high-cpu-and-http-queue-length"></a><span data-ttu-id="d8823-145">Zasady alertów i kodów stanu 403 500's, wysokiej Procesora, a długość kolejki HTTP</span><span class="sxs-lookup"><span data-stu-id="d8823-145">Alert rules for status codes 403 and 500's, High CPU, and HTTP Queue Length</span></span>
    {
      "apiVersion": "2014-04-01",
      "name": "[concat('ServerErrors ', variables('webSiteName'))]",
      "type": "Microsoft.Insights/alertrules",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[variables('webSiteName')]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Web/sites', variables('webSiteName')))]": "Resource",
        "displayName": "ServerErrorsAlertRule"
      },
      "properties": {
        "name": "[concat('ServerErrors ', variables('webSiteName'))]",
        "description": "[concat(variables('webSiteName'), ' has some server errors, status code 5xx.')]",
        "isEnabled": false,
        "condition": {
          "odata.type": "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
          "dataSource": {
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
            "resourceUri": "[resourceId('Microsoft.Web/sites', variables('webSiteName'))]",
            "metricName": "Http5xx"
          },
          "operator": "GreaterThan",
          "threshold": 0.0,
          "windowSize": "PT5M"
        },
        "action": {
          "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
          "sendToServiceOwners": true,
          "customEmails": [ ]
        }
      }
    },
    {
      "apiVersion": "2014-04-01",
      "name": "[concat('ForbiddenRequests ', variables('webSiteName'))]",
      "type": "Microsoft.Insights/alertrules",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[variables('webSiteName')]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Web/sites', variables('webSiteName')))]": "Resource",
        "displayName": "ForbiddenRequestsAlertRule"
      },
      "properties": {
        "name": "[concat('ForbiddenRequests ', variables('webSiteName'))]",
        "description": "[concat(variables('webSiteName'), ' has some requests that are forbidden, status code 403.')]",
        "isEnabled": false,
        "condition": {
          "odata.type": "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
          "dataSource": {
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
            "resourceUri": "[resourceId('Microsoft.Web/sites', variables('webSiteName'))]",
            "metricName": "Http403"
          },
          "operator": "GreaterThan",
          "threshold": 0,
          "windowSize": "PT5M"
        },
        "action": {
          "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
          "sendToServiceOwners": true,
          "customEmails": [ ]
        }
      }
    },
    {
      "apiVersion": "2014-04-01",
      "name": "[concat('CPUHigh ', variables('hostingPlanName'))]",
      "type": "Microsoft.Insights/alertrules",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[variables('hostingPlanName')]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName')))]": "Resource",
        "displayName": "CPUHighAlertRule"
      },
      "properties": {
        "name": "[concat('CPUHigh ', variables('hostingPlanName'))]",
        "description": "[concat('The average CPU is high across all the instances of ', variables('hostingPlanName'))]",
        "isEnabled": false,
        "condition": {
          "odata.type": "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
          "dataSource": {
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
            "resourceUri": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
            "metricName": "CpuPercentage"
          },
          "operator": "GreaterThan",
          "threshold": 90,
          "windowSize": "PT15M"
        },
        "action": {
          "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
          "sendToServiceOwners": true,
          "customEmails": [ ]
        }
      }
    },
    {
      "apiVersion": "2014-04-01",
      "name": "[concat('LongHttpQueue ', variables('hostingPlanName'))]",
      "type": "Microsoft.Insights/alertrules",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[variables('hostingPlanName')]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName')))]": "Resource",
        "displayName": "AutoScaleSettings"
      },
      "properties": {
        "name": "[concat('LongHttpQueue ', variables('hostingPlanName'))]",
        "description": "[concat('The HTTP queue for the instances of ', variables('hostingPlanName'), ' has a large number of pending requests.')]",
        "isEnabled": false,
        "condition": {
          "odata.type": "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
          "dataSource": {
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
            "resourceUri": "[concat(resourceGroup().id, '/providers/Microsoft.Web/serverfarms/', variables('hostingPlanName'))]",
            "metricName": "HttpQueueLength"
          },
          "operator": "GreaterThan",
          "threshold": 100.0,
          "windowSize": "PT5M"
        },
        "action": {
          "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
          "sendToServiceOwners": true,
          "customEmails": [ ]
        }
      }
    },

### <a name="app-insights"></a><span data-ttu-id="d8823-146">Szczegółowe informacje w aplikacji</span><span class="sxs-lookup"><span data-stu-id="d8823-146">App Insights</span></span>
    {
      "apiVersion": "2014-04-01",
      "name": "[concat('AppInsights', variables('webSiteName'))]",
      "type": "Microsoft.Insights/components",
      "location": "Central US",
      "dependsOn": [
        "[variables('webSiteName')]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Web/sites', variables('webSiteName')))]": "Resource",
        "displayName": "AppInsightsComponent"
      },
      "properties": {
        "ApplicationId": "[variables('webSiteName')]"
      }
    }

## <a name="commands-to-run-deployment"></a><span data-ttu-id="d8823-147">Polecenia umożliwiające uruchomienie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="d8823-147">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="d8823-148">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d8823-148">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-sql-database/azuredeploy.json

### <a name="azure-cli"></a><span data-ttu-id="d8823-149">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d8823-149">Azure CLI</span></span>

    azure config mode arm
    azure group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-sql-database/azuredeploy.json

### <a name="azure-cli-20"></a><span data-ttu-id="d8823-150">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="d8823-150">Azure CLI 2.0</span></span>

    az resource deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-sql-database/azuredeploy.json --parameters '@azuredeploy.parameters.json'

> [!NOTE]
> <span data-ttu-id="d8823-151">Dla zawartości pliku JSON parametrów, zobacz [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-sql-database/azuredeploy.parameters.json).</span><span class="sxs-lookup"><span data-stu-id="d8823-151">For content of the parameters JSON file, see [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-sql-database/azuredeploy.parameters.json).</span></span>
>
>
