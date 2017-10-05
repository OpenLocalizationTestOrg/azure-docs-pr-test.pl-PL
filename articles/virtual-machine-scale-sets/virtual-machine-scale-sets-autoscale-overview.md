---
title: "Automatyczne skalowanie i maszyny wirtualnej skalowanie zestawów | Dokumentacja firmy Microsoft"
description: "Informacje o używaniu diagnostyki i skalowania automatycznego zasobów do automatycznego skalowania maszyn wirtualnych w zestawie skalowania."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d29a3385-179e-4331-a315-daa7ea5701df
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: adegeo
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 06ff9d9ae1dd8256f0d22c1a60ed6a85554f1f17
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-automatic-scaling-and-virtual-machine-scale-sets"></a><span data-ttu-id="20628-103">Jak używać automatyczne skalowanie i zestawy skalowania maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="20628-103">How to use automatic scaling and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="20628-104">Automatyczne skalowanie maszyn wirtualnych w zestawie skalowania jest utworzenia lub usunięcia maszyn w zestawie, zgodnie z potrzebami, aby dopasować wymagania dotyczące wydajności.</span><span class="sxs-lookup"><span data-stu-id="20628-104">Automatic scaling of virtual machines in a scale set is the creation or deletion of machines in the set as needed to match performance requirements.</span></span> <span data-ttu-id="20628-105">Wraz z rozwojem działalności, aplikacja może wymagać dodatkowych zasobów, aby umożliwić skutecznie wykonywania zadań.</span><span class="sxs-lookup"><span data-stu-id="20628-105">As the volume of work grows, an application may require additional resources to enable it to effectively perform tasks.</span></span>

<span data-ttu-id="20628-106">Automatyczne skalowanie jest zautomatyzowany proces czy pomaga upraszczają zarządzanie.</span><span class="sxs-lookup"><span data-stu-id="20628-106">Automatic scaling is an automated process that helps ease management overhead.</span></span> <span data-ttu-id="20628-107">Przez zmniejszenie nakładów pracy, nie trzeba było stale monitorowania wydajności systemu lub zdecydować, jak zarządzać zasobami.</span><span class="sxs-lookup"><span data-stu-id="20628-107">By reducing overhead, you don't need to continually monitor system performance or decide how to manage resources.</span></span> <span data-ttu-id="20628-108">Skalowanie jest procesem elastycznej.</span><span class="sxs-lookup"><span data-stu-id="20628-108">Scaling is an elastic process.</span></span> <span data-ttu-id="20628-109">Miarę wzrostu obciążenia można dodać więcej zasobów.</span><span class="sxs-lookup"><span data-stu-id="20628-109">More resources can be added as the load increases.</span></span> <span data-ttu-id="20628-110">I jak żądanie zmniejsza, można usunąć zasoby, aby zminimalizować koszty i Obsługa poziomów wydajności.</span><span class="sxs-lookup"><span data-stu-id="20628-110">And as demand decreases, resources can be removed to minimize costs and maintain performance levels.</span></span>

<span data-ttu-id="20628-111">Skonfiguruj automatyczne skalowanie w skali skonfigurowane przy użyciu szablonu usługi Azure Resource Manager, programu Azure PowerShell, interfejsu wiersza polecenia Azure lub portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="20628-111">Set up automatic scaling on a scale set by using an Azure Resource Manager template, Azure PowerShell, Azure CLI, or the Azure portal.</span></span>

## <a name="set-up-scaling-by-using-resource-manager-templates"></a><span data-ttu-id="20628-112">Ustawianie skalowania przy użyciu szablonów usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="20628-112">Set up scaling by using Resource Manager templates</span></span>
<span data-ttu-id="20628-113">Zamiast wdrażania i zarządzania nimi każdego zasobu aplikacji oddzielnie, należy użyć szablonu, który wdraża wszystkie zasoby w jednej, skoordynowanej operacji.</span><span class="sxs-lookup"><span data-stu-id="20628-113">Rather than deploying and managing each resource of your application separately, use a template that deploys all resources in a single, coordinated operation.</span></span> <span data-ttu-id="20628-114">W szablonie są zdefiniowane zasoby aplikacji i parametrów wdrożenia są określone dla różnych środowisk.</span><span class="sxs-lookup"><span data-stu-id="20628-114">In the template, application resources are defined and deployment parameters are specified for different environments.</span></span> <span data-ttu-id="20628-115">Szablon składa się z kodu JSON i wyrażeń, które służy do tworzenia wartości na potrzeby wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="20628-115">The template consists of JSON and expressions that you can use to construct values for your deployment.</span></span> <span data-ttu-id="20628-116">Aby dowiedzieć się więcej, zobacz [szablonów Authoring Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="20628-116">To learn more, look at [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="20628-117">W szablonie należy określić pojemność elementu:</span><span class="sxs-lookup"><span data-stu-id="20628-117">In the template, you specify the capacity element:</span></span>

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 3
},
```

<span data-ttu-id="20628-118">Pojemność określa liczbę maszyn wirtualnych w zestawie.</span><span class="sxs-lookup"><span data-stu-id="20628-118">Capacity identifies the number of virtual machines in the set.</span></span> <span data-ttu-id="20628-119">Wydajność można zmienić ręcznie przez wdrożenie szablonu, podając inną wartość.</span><span class="sxs-lookup"><span data-stu-id="20628-119">You can manually change the capacity by deploying a template with a different value.</span></span> <span data-ttu-id="20628-120">Jeśli wdrażasz szablon można zmienić tylko pojemność może zawierać tylko element SKU o pojemności zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="20628-120">If you are deploying a template to only change the capacity, you can include only the SKU element with the updated capacity.</span></span>

<span data-ttu-id="20628-121">Pojemność zestawu skalowania można automatycznie dostosowywany przy użyciu kombinacji **autoscaleSettings** zasobu i rozszerzenia diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="20628-121">The capacity of your scale set can be automatically adjusted by using a combination of the **autoscaleSettings** resource and the diagnostics extension.</span></span>

### <a name="configure-the-azure-diagnostics-extension"></a><span data-ttu-id="20628-122">Skonfiguruj rozszerzenie diagnostyki Azure</span><span class="sxs-lookup"><span data-stu-id="20628-122">Configure the Azure Diagnostics extension</span></span>
<span data-ttu-id="20628-123">Automatyczne skalowanie jest możliwe tylko jeśli kolekcji metryki zakończy się pomyślnie na każdej maszynie wirtualnej w zestawie skalowania.</span><span class="sxs-lookup"><span data-stu-id="20628-123">Automatic scaling can only be done if metrics collection is successful on each virtual machine in the scale set.</span></span> <span data-ttu-id="20628-124">Rozszerzenia diagnostyki Azure oferuje możliwości monitorowania i diagnostyki, które zaspokoi potrzeby kolekcji metryki automatycznego skalowania zasobu.</span><span class="sxs-lookup"><span data-stu-id="20628-124">The Azure Diagnostics Extension provides the monitoring and diagnostics capabilities that meets the metrics collection needs of the autoscale resource.</span></span> <span data-ttu-id="20628-125">W ramach szablonu usługi Resource Manager można zainstalować rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="20628-125">You can install the extension as part of the Resource Manager template.</span></span>

<span data-ttu-id="20628-126">W tym przykładzie przedstawiono zmienne, które są używane w szablonie, aby skonfigurować rozszerzenie diagnostyki:</span><span class="sxs-lookup"><span data-stu-id="20628-126">This example shows the variables that are used in the template to configure the diagnostics extension:</span></span>

```json
"diagnosticsStorageAccountName": "[concat(parameters('resourcePrefix'), 'saa')]",
"accountid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/', 'Microsoft.Storage/storageAccounts/', variables('diagnosticsStorageAccountName'))]",
"wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
"wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Thread Count\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
"wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
"wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
"wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
```

<span data-ttu-id="20628-127">Parametry są podane podczas wdrażania szablonu.</span><span class="sxs-lookup"><span data-stu-id="20628-127">Parameters are provided when the template is deployed.</span></span> <span data-ttu-id="20628-128">W tym przykładzie podano nazwę konta magazynu (w którym są przechowywane dane) i nazwy zestawu skali (w którym dane są zbierane).</span><span class="sxs-lookup"><span data-stu-id="20628-128">In this example, the name of the storage account (where data is stored) and the name of the scale set (where data is collected) are provided.</span></span> <span data-ttu-id="20628-129">Również w tym przykładzie systemu Windows Server zbieranych licznika wydajności liczba wątków.</span><span class="sxs-lookup"><span data-stu-id="20628-129">Also in this Windows Server example, only the Thread Count performance counter is collected.</span></span> <span data-ttu-id="20628-130">Wszystkie liczniki wydajności dostępne w systemie Windows lub Linux może służyć do zbierania informacji diagnostycznych i może być uwzględniony w konfiguracji rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="20628-130">All the available performance counters in Windows or Linux can be used to collect diagnostics information and can be included in the extension configuration.</span></span>

<span data-ttu-id="20628-131">W tym przykładzie przedstawiono definicję rozszerzenia w szablonie:</span><span class="sxs-lookup"><span data-stu-id="20628-131">This example shows the definition of the extension in the template:</span></span>

```json
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
          "storageAccountKey": "[listkeys(variables('accountid'), variables('apiVersion')).key1]",
          "storageAccountEndPoint": "https://core.windows.net"
        }
      }
    }
  ]
}
```

<span data-ttu-id="20628-132">Po uruchomieniu rozszerzenia diagnostyki, dane są przechowywane i zbierane w tabeli, w ramach konta magazynu, który określisz.</span><span class="sxs-lookup"><span data-stu-id="20628-132">When the diagnostics extension runs, the data is stored and collected in a table, in the storage account that you specify.</span></span> <span data-ttu-id="20628-133">W **WADPerformanceCounters** tabeli, możesz znaleźć zebranych danych:</span><span class="sxs-lookup"><span data-stu-id="20628-133">In the **WADPerformanceCounters** table, you can find the collected data:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountBefore2.png)

### <a name="configure-the-autoscalesettings-resource"></a><span data-ttu-id="20628-134">Konfigurowanie zasobów autoScaleSettings</span><span class="sxs-lookup"><span data-stu-id="20628-134">Configure the autoScaleSettings resource</span></span>
<span data-ttu-id="20628-135">Zasób autoscaleSettings używa tych informacji z rozszerzenia diagnostyki umożliwia określenie, czy można zwiększyć lub zmniejszyć liczbę maszyn wirtualnych w zestawie skalowania.</span><span class="sxs-lookup"><span data-stu-id="20628-135">The autoscaleSettings resource uses the information from the diagnostics extension to decide whether to increase or decrease the number of virtual machines in the scale set.</span></span>

<span data-ttu-id="20628-136">W tym przykładzie pokazano konfigurację zasobu w szablonie:</span><span class="sxs-lookup"><span data-stu-id="20628-136">This example shows the configuration of the resource in the template:</span></span>

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
              "metricName": "\\Processor(_Total)\\Thread Count",
              "metricNamespace": "",
              "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
              "timeGrain": "PT1M",
              "statistic": "Average",
              "timeWindow": "PT5M",
              "timeAggregation": "Average",
              "operator": "GreaterThan",
              "threshold": 650
            },
            "scaleAction": {
              "direction": "Increase",
              "type": "ChangeCount",
              "value": "1",
              "cooldown": "PT5M"
            }
          },
          {
            "metricTrigger": {
              "metricName": "\\Processor(_Total)\\Thread Count",
              "metricNamespace": "",
              "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
              "timeGrain": "PT1M",
              "statistic": "Average",
              "timeWindow": "PT5M",
              "timeAggregation": "Average",
              "operator": "LessThan",
              "threshold": 550
            },
            "scaleAction": {
              "direction": "Decrease",
              "type": "ChangeCount",
              "value": "1",
              "cooldown": "PT5M"
            }
          }
        ]
      }
    ],
    "targetResourceUri": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]"
  }
}
```

<span data-ttu-id="20628-137">W powyższym przykładzie dwie reguły są tworzone dla Definiowanie automatycznych akcji skalowania.</span><span class="sxs-lookup"><span data-stu-id="20628-137">In the example above, two rules are created for defining the automatic scaling actions.</span></span> <span data-ttu-id="20628-138">Pierwsza reguła definiuje akcji skalowania w poziomie, a drugą regułę definiuje akcji skalowania w.</span><span class="sxs-lookup"><span data-stu-id="20628-138">The first rule defines the scale-out action and the second rule defines the scale-in action.</span></span> <span data-ttu-id="20628-139">Te wartości są dostępne w zasadach:</span><span class="sxs-lookup"><span data-stu-id="20628-139">These values are provided in the rules:</span></span>

| <span data-ttu-id="20628-140">Reguła</span><span class="sxs-lookup"><span data-stu-id="20628-140">Rule</span></span> | <span data-ttu-id="20628-141">Opis</span><span class="sxs-lookup"><span data-stu-id="20628-141">Description</span></span> |
| ---- | ----------- |
| <span data-ttu-id="20628-142">metricName</span><span class="sxs-lookup"><span data-stu-id="20628-142">metricName</span></span>        | <span data-ttu-id="20628-143">Ta wartość jest taka sama jak licznika wydajności, które zdefiniowano w zmiennej wadperfcounter rozszerzenia diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="20628-143">This value is the same as the performance counter that you defined in the wadperfcounter variable for the diagnostics extension.</span></span> <span data-ttu-id="20628-144">W powyższym przykładzie wątku licznik jest używany.</span><span class="sxs-lookup"><span data-stu-id="20628-144">In the example above, the Thread Count counter is used.</span></span>    |
| <span data-ttu-id="20628-145">metricResourceUri</span><span class="sxs-lookup"><span data-stu-id="20628-145">metricResourceUri</span></span> | <span data-ttu-id="20628-146">Ta wartość jest identyfikator zasobu zestawu skali maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="20628-146">This value is the resource identifier of the virtual machine scale set.</span></span> <span data-ttu-id="20628-147">Ten identyfikator zawiera nazwę grupy zasobów, nazwę dostawcy zasobów i nazwę zestaw skalowania skalowania.</span><span class="sxs-lookup"><span data-stu-id="20628-147">This identifier contains the name of the resource group, the name of the resource provider, and the name of the scale set to scale.</span></span> |
| <span data-ttu-id="20628-148">Ziarnem czasu</span><span class="sxs-lookup"><span data-stu-id="20628-148">timeGrain</span></span>         | <span data-ttu-id="20628-149">Ta wartość jest stopień szczegółowości metryki, które są zbierane.</span><span class="sxs-lookup"><span data-stu-id="20628-149">This value is the granularity of the metrics that are collected.</span></span> <span data-ttu-id="20628-150">W powyższym przykładzie dane są zbierane w odstępach jednej minuty.</span><span class="sxs-lookup"><span data-stu-id="20628-150">In the preceding example, data is collected on an interval of one minute.</span></span> <span data-ttu-id="20628-151">Ta wartość jest używana z timeWindow.</span><span class="sxs-lookup"><span data-stu-id="20628-151">This value is used with timeWindow.</span></span> |
| <span data-ttu-id="20628-152">Statystyka</span><span class="sxs-lookup"><span data-stu-id="20628-152">statistic</span></span>         | <span data-ttu-id="20628-153">Ta wartość określa, jak metryki połączone pomieścić automatycznych akcji skalowania.</span><span class="sxs-lookup"><span data-stu-id="20628-153">This value determines how the metrics are combined to accommodate the automatic scaling action.</span></span> <span data-ttu-id="20628-154">Możliwe wartości to: średnia, Min, Max.</span><span class="sxs-lookup"><span data-stu-id="20628-154">The possible values are: Average, Min, Max.</span></span> |
| <span data-ttu-id="20628-155">timeWindow</span><span class="sxs-lookup"><span data-stu-id="20628-155">timeWindow</span></span>        | <span data-ttu-id="20628-156">Ta wartość jest przedział czasu, w którym są zbierane dane wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="20628-156">This value is the range of time in which instance data is collected.</span></span> <span data-ttu-id="20628-157">Musi być od 5 minut do 12 godzin.</span><span class="sxs-lookup"><span data-stu-id="20628-157">It must be between 5 minutes and 12 hours.</span></span> |
| <span data-ttu-id="20628-158">timeAggregation</span><span class="sxs-lookup"><span data-stu-id="20628-158">timeAggregation</span></span>   | <span data-ttu-id="20628-159">Ta wartość określa, jak powinny być połączone dane, które są zbierane wraz z upływem czasu.</span><span class="sxs-lookup"><span data-stu-id="20628-159">This value determines how the data that is collected should be combined over time.</span></span> <span data-ttu-id="20628-160">Wartość domyślna to średnia.</span><span class="sxs-lookup"><span data-stu-id="20628-160">The default value is Average.</span></span> <span data-ttu-id="20628-161">Możliwe wartości to: średnia, co najmniej, maksimum, ostatnich, łączna liczba, liczba.</span><span class="sxs-lookup"><span data-stu-id="20628-161">The possible values are: Average, Minimum, Maximum, Last, Total, Count.</span></span> |
| <span data-ttu-id="20628-162">Operator</span><span class="sxs-lookup"><span data-stu-id="20628-162">operator</span></span>          | <span data-ttu-id="20628-163">Ta wartość jest operator, który służy do porównywania danych metryki i wartość progową.</span><span class="sxs-lookup"><span data-stu-id="20628-163">This value is the operator that is used to compare the metric data and the threshold.</span></span> <span data-ttu-id="20628-164">Możliwe wartości to: równa, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span><span class="sxs-lookup"><span data-stu-id="20628-164">The possible values are: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span></span> |
| <span data-ttu-id="20628-165">Próg</span><span class="sxs-lookup"><span data-stu-id="20628-165">threshold</span></span>         | <span data-ttu-id="20628-166">Ta wartość jest wartością wyzwala akcji skalowania.</span><span class="sxs-lookup"><span data-stu-id="20628-166">This value is the value that triggers the scale action.</span></span> <span data-ttu-id="20628-167">Pamiętaj zapewnić wystarczającą różnicę wartości progowych dla **skalowalnego w poziomie** i **w skali** akcje.</span><span class="sxs-lookup"><span data-stu-id="20628-167">Be sure to provide a sufficient difference between the threshold values for the **scale-out** and **scale-in** actions.</span></span> <span data-ttu-id="20628-168">Jeśli ustawisz takie same wartości dla obu akcje systemu oszacowano stałej zmiany, które uniemożliwiają wdrożenie akcji skalowania.</span><span class="sxs-lookup"><span data-stu-id="20628-168">If you set the same values for both actions, the system anticipates constant change, which prevents it from implementing a scaling action.</span></span> <span data-ttu-id="20628-169">Na przykład ustawienie zarówno do 600 wątków w poprzednim przykładzie nie działa.</span><span class="sxs-lookup"><span data-stu-id="20628-169">For example, setting both to 600 threads in the preceding example doesn't work.</span></span> |
| <span data-ttu-id="20628-170">Kierunek</span><span class="sxs-lookup"><span data-stu-id="20628-170">direction</span></span>         | <span data-ttu-id="20628-171">Ta wartość Określa akcję wykonywaną, gdy uzyskuje się wartość progową.</span><span class="sxs-lookup"><span data-stu-id="20628-171">This value determines the action that is taken when the threshold value is achieved.</span></span> <span data-ttu-id="20628-172">Możliwe wartości to zwiększyć lub zmniejszyć.</span><span class="sxs-lookup"><span data-stu-id="20628-172">The possible values are Increase or Decrease.</span></span> |
| <span data-ttu-id="20628-173">type</span><span class="sxs-lookup"><span data-stu-id="20628-173">type</span></span>              | <span data-ttu-id="20628-174">Ta wartość jest typu akcji, która powinna się odbyć i musi mieć ustawioną ChangeCount.</span><span class="sxs-lookup"><span data-stu-id="20628-174">This value is the type of action that should occur and must be set to ChangeCount.</span></span> |
| <span data-ttu-id="20628-175">wartość</span><span class="sxs-lookup"><span data-stu-id="20628-175">value</span></span>             | <span data-ttu-id="20628-176">Ta wartość jest liczba maszyn wirtualnych, które zostały dodane do lub usunięte z zestawu skalowania.</span><span class="sxs-lookup"><span data-stu-id="20628-176">This value is the number of virtual machines that are added to or removed from the scale set.</span></span> <span data-ttu-id="20628-177">Ta wartość musi wynosić 1 lub większą.</span><span class="sxs-lookup"><span data-stu-id="20628-177">This value must be 1 or greater.</span></span> |
| <span data-ttu-id="20628-178">cooldown</span><span class="sxs-lookup"><span data-stu-id="20628-178">cooldown</span></span>          | <span data-ttu-id="20628-179">Ta wartość jest czas oczekiwania od momentu ostatniej akcji skalowania, zanim nastąpi następnej akcji.</span><span class="sxs-lookup"><span data-stu-id="20628-179">This value is the amount of time to wait since the last scaling action before the next action occurs.</span></span> <span data-ttu-id="20628-180">Ta wartość musi należeć do zakresu od minutę i jeden tydzień.</span><span class="sxs-lookup"><span data-stu-id="20628-180">This value must be between one minute and one week.</span></span> |

<span data-ttu-id="20628-181">W zależności od licznika wydajności są używane, niektórych elementów w konfiguracji szablonu są używane w inny sposób.</span><span class="sxs-lookup"><span data-stu-id="20628-181">Depending on the performance counter, you are using, some of the elements in the template configuration are used differently.</span></span> <span data-ttu-id="20628-182">W powyższym przykładzie licznika wydajności to liczba wątków, wartość progowa jest 650 dla akcji skalowania w poziomie, a wartość progowa jest 550 dla akcji skalowania w.</span><span class="sxs-lookup"><span data-stu-id="20628-182">In the preceding example, the performance counter is Thread Count, the threshold value is 650 for a scale-out action, and the threshold value is 550 for the scale-in action.</span></span> <span data-ttu-id="20628-183">Użycie licznika, takie jak czas procesora (%), wartość progowa jest równa wartości procentowej użycia procesora CPU, która określa akcji skalowania.</span><span class="sxs-lookup"><span data-stu-id="20628-183">If you use a counter such as %Processor Time, the threshold value is set to the percentage of CPU usage that determines a scaling action.</span></span>

<span data-ttu-id="20628-184">Po wyzwoleniu akcji skalowania, takich jak wysokie obciążenie, zwiększa się na podstawie wartości w szablonie pojemność zestawu.</span><span class="sxs-lookup"><span data-stu-id="20628-184">When a scaling action is triggered, such as a high load, the capacity of the set is increased based on the value in the template.</span></span> <span data-ttu-id="20628-185">Na przykład w skali zestawu, którego pojemność ustawiono 3 i wartość akcji skalowania jest równa 1:</span><span class="sxs-lookup"><span data-stu-id="20628-185">For example, in a scale set where the capacity is set to 3 and the scale action value is set to 1:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerBefore.png)

<span data-ttu-id="20628-186">Gdy bieżącego obciążenia powoduje, że liczba wątków średni przejść powyżej wartości progowej 650:</span><span class="sxs-lookup"><span data-stu-id="20628-186">When the current load causes the average thread count to go above the threshold of 650:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountAfter.png)

<span data-ttu-id="20628-187">A **skalowalnego w poziomie** wyzwoleniu powodujący stanie można zwiększyć o jeden zestaw akcji:</span><span class="sxs-lookup"><span data-stu-id="20628-187">A **scale-out** action is triggered that causes the capacity of the set to be increased by one:</span></span>

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 4
},
```

<span data-ttu-id="20628-188">Wynik jest, że maszyna wirtualna została dodana do zestawu skalowania:</span><span class="sxs-lookup"><span data-stu-id="20628-188">The result is a virtual machine is added to the scale set:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerAfter.png)

<span data-ttu-id="20628-189">Po upływie cooldown pięć minut Jeśli średnia liczba wątków na maszynach pozostaje ponad 600 innej maszyny jest dodane do zestawu.</span><span class="sxs-lookup"><span data-stu-id="20628-189">After a cooldown period of five minutes, if the average number of threads on the machines stays over 600, another machine is added to the set.</span></span> <span data-ttu-id="20628-190">Jeśli liczba wątków średni pozostaje poniżej 550, pojemność zestawu skalowania, zostanie zmniejszona jedną i maszynie jest usuwane z zestawu.</span><span class="sxs-lookup"><span data-stu-id="20628-190">If the average thread count stays below 550, the capacity of the scale set is reduced by one and a machine is removed from the set.</span></span>

## <a name="set-up-scaling-using-azure-powershell"></a><span data-ttu-id="20628-191">Ustawianie skalowania przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="20628-191">Set up scaling using Azure PowerShell</span></span>

<span data-ttu-id="20628-192">Aby wyświetlić przykłady przy użyciu programu PowerShell, aby skonfigurować funkcję skalowania automatycznego, obejrzyj [Azure PowerShell Monitor szybki start przykłady](../monitoring-and-diagnostics/insights-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="20628-192">To see examples of using PowerShell to set up autoscaling, look at [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md).</span></span>

## <a name="set-up-scaling-using-azure-cli"></a><span data-ttu-id="20628-193">Ustawianie skalowania przy użyciu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="20628-193">Set up scaling using Azure CLI</span></span>

<span data-ttu-id="20628-194">Aby wyświetlić przykłady przy użyciu wiersza polecenia platformy Azure, aby skonfigurować funkcję skalowania automatycznego, obejrzyj [Azure Monitor i platform interfejsu wiersza polecenia Szybki start przykłady](../monitoring-and-diagnostics/insights-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="20628-194">To see examples of using Azure CLI to set up autoscaling, look at [Azure Monitor Cross-platform CLI quick start samples](../monitoring-and-diagnostics/insights-cli-samples.md).</span></span>

## <a name="set-up-scaling-using-the-azure-portal"></a><span data-ttu-id="20628-195">Ustawianie skalowania przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="20628-195">Set up scaling using the Azure portal</span></span>

<span data-ttu-id="20628-196">Aby zapoznać się z przykładem przy użyciu portalu Azure, aby skonfigurować funkcję skalowania automatycznego, obejrzyj [tworzenia zestawu skalowania maszyn wirtualnych przy użyciu portalu Azure](virtual-machine-scale-sets-portal-create.md).</span><span class="sxs-lookup"><span data-stu-id="20628-196">To see an example of using the Azure portal to set up autoscaling, look at [Create a Virtual Machine Scale Set using the Azure portal](virtual-machine-scale-sets-portal-create.md).</span></span>

## <a name="investigate-scaling-actions"></a><span data-ttu-id="20628-197">Zbadaj akcji skalowania</span><span class="sxs-lookup"><span data-stu-id="20628-197">Investigate scaling actions</span></span>

* <span data-ttu-id="20628-198">**Witryna Azure Portal**</span><span class="sxs-lookup"><span data-stu-id="20628-198">**Azure portal**</span></span>  
<span data-ttu-id="20628-199">Obecnie można uzyskać ograniczone informacje za pomocą portalu.</span><span class="sxs-lookup"><span data-stu-id="20628-199">You can currently get a limited amount of information using the portal.</span></span>

* <span data-ttu-id="20628-200">**Eksplorator zasobów Azure**</span><span class="sxs-lookup"><span data-stu-id="20628-200">**Azure Resource Explorer**</span></span>  
<span data-ttu-id="20628-201">To narzędzie jest najlepsze dla eksploracji bieżącego stanu sieci zestawu skali.</span><span class="sxs-lookup"><span data-stu-id="20628-201">This tool is the best for exploring the current state of your scale set.</span></span> <span data-ttu-id="20628-202">Tej ścieżki i powinien zostać wyświetlony widok wystąpienia zestawu skali utworzony:</span><span class="sxs-lookup"><span data-stu-id="20628-202">Follow this path and you should see the instance view of the scale set that you created:</span></span>  
<span data-ttu-id="20628-203">**Subskrypcje > {subskrypcji} > resourceGroups > {grupie zasobów} > dostawców > Microsoft.Compute > virtualMachineScaleSets > {zestawie skali} > maszyn wirtualnych**</span><span class="sxs-lookup"><span data-stu-id="20628-203">**Subscriptions > {your subscription} > resourceGroups > {your resource group} > providers > Microsoft.Compute > virtualMachineScaleSets > {your scale set} > virtualMachines**</span></span>

* <span data-ttu-id="20628-204">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="20628-204">**Azure PowerShell**</span></span>  
<span data-ttu-id="20628-205">Użyj tego polecenia, aby uzyskać pewne informacje:</span><span class="sxs-lookup"><span data-stu-id="20628-205">Use this command to get some information:</span></span>

  ```powershell
  Get-AzureRmResource -name vmsstest1 -ResourceGroupName vmsstestrg1 -ResourceType Microsoft.Compute/virtualMachineScaleSets -ApiVersion 2015-06-15
  Get-Autoscalesetting -ResourceGroup rainvmss -DetailedOutput
  ```

* <span data-ttu-id="20628-206">Połączenie z maszyną wirtualną jumpbox podobnie jak inne maszyny, a następnie zdalny dostęp maszyny wirtualne w skali ustawioną monitorowania poszczególnych procesów.</span><span class="sxs-lookup"><span data-stu-id="20628-206">Connect to the jumpbox virtual machine just like you would any other machine and then you can remotely access the virtual machines in the scale set to monitor individual processes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="20628-207">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="20628-207">Next Steps</span></span>
* <span data-ttu-id="20628-208">Przyjrzyj się [automatycznie skalować maszyny w zestawie skalowania maszyn wirtualnych](virtual-machine-scale-sets-windows-autoscale.md) Aby wyświetlić przykład sposobu tworzenia skali ustawiony za pomocą automatyczne skalowanie skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="20628-208">Look at [Automatically scale machines in a Virtual Machine Scale Set](virtual-machine-scale-sets-windows-autoscale.md) to see an example of how to create a scale set with automatic scaling configured.</span></span>

* <span data-ttu-id="20628-209">Znajdź przykłady Azure Monitor funkcje w [Azure PowerShell Monitor szybki start — przykłady](../monitoring-and-diagnostics/insights-powershell-samples.md)</span><span class="sxs-lookup"><span data-stu-id="20628-209">Find examples of Azure Monitor monitoring features in [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md)</span></span>

* <span data-ttu-id="20628-210">Dowiedz się więcej o funkcji powiadomień w [użyć akcji skalowania automatycznego do wysyłania wiadomości e-mail i elementu webhook powiadomień o alertach w monitorze Azure](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md).</span><span class="sxs-lookup"><span data-stu-id="20628-210">Learn about notification features in [Use autoscale actions to send email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md).</span></span>

* <span data-ttu-id="20628-211">Więcej informacji na temat sposobu [dzienników inspekcji używany do wysyłania wiadomości e-mail i elementu webhook powiadomień o alertach w monitorze Azure](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="20628-211">Learn about how to [Use audit logs to send email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span></span>

* <span data-ttu-id="20628-212">Dowiedz się więcej o [zaawansowanych scenariuszy skalowania automatycznego](virtual-machine-scale-sets-advanced-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="20628-212">Learn about [advanced autoscale scenarios](virtual-machine-scale-sets-advanced-autoscale.md).</span></span>
