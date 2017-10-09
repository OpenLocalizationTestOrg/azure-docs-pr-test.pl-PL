---
title: "aaaAutomatic skalowania maszyn wirtualnych i skalowanie zestawów | Dokumentacja firmy Microsoft"
description: "Informacje o używaniu diagnostyki i maszyny wirtualne skalowania automatycznego skalowania zasobów tooautomatically w zestawie skalowania."
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
ms.openlocfilehash: 25f54b693e3c991577238242008c262023ed479c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-automatic-scaling-and-virtual-machine-scale-sets"></a><span data-ttu-id="b160a-103">Jak toouse automatyczne skalowanie i zestawy skalowania maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="b160a-103">How toouse automatic scaling and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="b160a-104">Automatyczne skalowanie maszyn wirtualnych w zestawie skalowania jest tworzenie hello lub usunięcia maszyn w hello Ustaw jako potrzebne toomatch wymagania dotyczące wydajności.</span><span class="sxs-lookup"><span data-stu-id="b160a-104">Automatic scaling of virtual machines in a scale set is hello creation or deletion of machines in hello set as needed toomatch performance requirements.</span></span> <span data-ttu-id="b160a-105">Wraz z rozwojem hello ilość pracy, aplikacja może wymagać dodatkowych zasobów tooenable on tooeffectively wykonywania zadań.</span><span class="sxs-lookup"><span data-stu-id="b160a-105">As hello volume of work grows, an application may require additional resources tooenable it tooeffectively perform tasks.</span></span>

<span data-ttu-id="b160a-106">Automatyczne skalowanie jest zautomatyzowany proces czy pomaga upraszczają zarządzanie.</span><span class="sxs-lookup"><span data-stu-id="b160a-106">Automatic scaling is an automated process that helps ease management overhead.</span></span> <span data-ttu-id="b160a-107">Przez zmniejszenie nakładów pracy, nie należy monitorować wydajność systemu toocontinually lub zdecydować, jak toomanage zasobów.</span><span class="sxs-lookup"><span data-stu-id="b160a-107">By reducing overhead, you don't need toocontinually monitor system performance or decide how toomanage resources.</span></span> <span data-ttu-id="b160a-108">Skalowanie jest procesem elastycznej.</span><span class="sxs-lookup"><span data-stu-id="b160a-108">Scaling is an elastic process.</span></span> <span data-ttu-id="b160a-109">Więcej zasobów do dodania jako hello wzrostu obciążenia.</span><span class="sxs-lookup"><span data-stu-id="b160a-109">More resources can be added as hello load increases.</span></span> <span data-ttu-id="b160a-110">I jako spadku żądanie zasoby mogą zostać usunięte toominimize kosztów i Obsługa poziomów wydajności.</span><span class="sxs-lookup"><span data-stu-id="b160a-110">And as demand decreases, resources can be removed toominimize costs and maintain performance levels.</span></span>

<span data-ttu-id="b160a-111">Skonfiguruj automatyczne skalowanie w skali skonfigurowane przy użyciu usługi Azure Resource Manager szablonu programu Azure PowerShell, interfejsu wiersza polecenia Azure albo hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b160a-111">Set up automatic scaling on a scale set by using an Azure Resource Manager template, Azure PowerShell, Azure CLI, or hello Azure portal.</span></span>

## <a name="set-up-scaling-by-using-resource-manager-templates"></a><span data-ttu-id="b160a-112">Ustawianie skalowania przy użyciu szablonów usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b160a-112">Set up scaling by using Resource Manager templates</span></span>
<span data-ttu-id="b160a-113">Zamiast wdrażania i zarządzania nimi każdego zasobu aplikacji oddzielnie, należy użyć szablonu, który wdraża wszystkie zasoby w jednej, skoordynowanej operacji.</span><span class="sxs-lookup"><span data-stu-id="b160a-113">Rather than deploying and managing each resource of your application separately, use a template that deploys all resources in a single, coordinated operation.</span></span> <span data-ttu-id="b160a-114">W szablonie hello są zdefiniowane zasoby aplikacji i parametrów wdrożenia są określone dla różnych środowisk.</span><span class="sxs-lookup"><span data-stu-id="b160a-114">In hello template, application resources are defined and deployment parameters are specified for different environments.</span></span> <span data-ttu-id="b160a-115">Szablon Hello składa się z kodu JSON i wyrażeń, że możesz użyć wartości tooconstruct dla danego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="b160a-115">hello template consists of JSON and expressions that you can use tooconstruct values for your deployment.</span></span> <span data-ttu-id="b160a-116">toolearn, obejrzyj [szablonów Authoring Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="b160a-116">toolearn more, look at [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="b160a-117">W szablonie hello należy określić element pojemności hello:</span><span class="sxs-lookup"><span data-stu-id="b160a-117">In hello template, you specify hello capacity element:</span></span>

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 3
},
```

<span data-ttu-id="b160a-118">Pojemność identyfikuje hello liczbę maszyn wirtualnych w zestawie hello.</span><span class="sxs-lookup"><span data-stu-id="b160a-118">Capacity identifies hello number of virtual machines in hello set.</span></span> <span data-ttu-id="b160a-119">Możesz ręcznie zmienić hello pojemności poprzez wdrożenie szablonu, podając inną wartość.</span><span class="sxs-lookup"><span data-stu-id="b160a-119">You can manually change hello capacity by deploying a template with a different value.</span></span> <span data-ttu-id="b160a-120">Jeśli wdrażasz szablon tooonly zmiany hello pojemności może zawierać tylko element SKU hello o pojemności hello zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="b160a-120">If you are deploying a template tooonly change hello capacity, you can include only hello SKU element with hello updated capacity.</span></span>

<span data-ttu-id="b160a-121">Witaj pojemność zestawu skalowania można automatycznie dostosować przy użyciu kombinacji hello **autoscaleSettings** zasobów i hello rozszerzenie diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="b160a-121">hello capacity of your scale set can be automatically adjusted by using a combination of hello **autoscaleSettings** resource and hello diagnostics extension.</span></span>

### <a name="configure-hello-azure-diagnostics-extension"></a><span data-ttu-id="b160a-122">Skonfiguruj rozszerzenie Azure Diagnostics hello</span><span class="sxs-lookup"><span data-stu-id="b160a-122">Configure hello Azure Diagnostics extension</span></span>
<span data-ttu-id="b160a-123">Automatyczne skalowanie jest możliwe tylko w przypadku pomyślnego nawiązania na każdej maszynie wirtualnej w zestawie skalowania hello kolekcji metryki.</span><span class="sxs-lookup"><span data-stu-id="b160a-123">Automatic scaling can only be done if metrics collection is successful on each virtual machine in hello scale set.</span></span> <span data-ttu-id="b160a-124">Witaj rozszerzenia diagnostyki Azure udostępnia możliwości monitorowania i diagnostyki hello, które zaspokoi potrzeby zbierania miar hello hello automatycznego skalowania zasobu.</span><span class="sxs-lookup"><span data-stu-id="b160a-124">hello Azure Diagnostics Extension provides hello monitoring and diagnostics capabilities that meets hello metrics collection needs of hello autoscale resource.</span></span> <span data-ttu-id="b160a-125">Rozszerzenie hello można zainstalować jako część hello szablonu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b160a-125">You can install hello extension as part of hello Resource Manager template.</span></span>

<span data-ttu-id="b160a-126">Ten przykład przedstawia hello zmienne, które są używane w hello szablonu tooconfigure hello diagnostyki rozszerzenia:</span><span class="sxs-lookup"><span data-stu-id="b160a-126">This example shows hello variables that are used in hello template tooconfigure hello diagnostics extension:</span></span>

```json
"diagnosticsStorageAccountName": "[concat(parameters('resourcePrefix'), 'saa')]",
"accountid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/', 'Microsoft.Storage/storageAccounts/', variables('diagnosticsStorageAccountName'))]",
"wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
"wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Thread Count\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
"wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
"wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
"wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
```

<span data-ttu-id="b160a-127">Parametry są udostępniane po wdrożeniu hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="b160a-127">Parameters are provided when hello template is deployed.</span></span> <span data-ttu-id="b160a-128">W tym przykładzie, nazwa hello hello konta magazynu (w którym są przechowywane dane) i hello podano nazwę zestawu skali hello (w którym dane są zbierane).</span><span class="sxs-lookup"><span data-stu-id="b160a-128">In this example, hello name of hello storage account (where data is stored) and hello name of hello scale set (where data is collected) are provided.</span></span> <span data-ttu-id="b160a-129">Również w tym przykładzie systemu Windows Server, zbierane są tylko hello licznika wydajności liczba wątków.</span><span class="sxs-lookup"><span data-stu-id="b160a-129">Also in this Windows Server example, only hello Thread Count performance counter is collected.</span></span> <span data-ttu-id="b160a-130">Witaj wszystkich dostępnych liczników wydajności w systemie Windows lub Linux mogą być używane toocollect informacje diagnostyczne i może być uwzględniony w konfiguracji rozszerzenia hello.</span><span class="sxs-lookup"><span data-stu-id="b160a-130">All hello available performance counters in Windows or Linux can be used toocollect diagnostics information and can be included in hello extension configuration.</span></span>

<span data-ttu-id="b160a-131">W tym przykładzie przedstawiono definicję hello rozszerzenia hello w szablonie hello:</span><span class="sxs-lookup"><span data-stu-id="b160a-131">This example shows hello definition of hello extension in hello template:</span></span>

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

<span data-ttu-id="b160a-132">Po uruchomieniu rozszerzenia diagnostyki hello hello danych są przechowywane i zebrane w tabeli, hello konta magazynu, który określisz.</span><span class="sxs-lookup"><span data-stu-id="b160a-132">When hello diagnostics extension runs, hello data is stored and collected in a table, in hello storage account that you specify.</span></span> <span data-ttu-id="b160a-133">W hello **WADPerformanceCounters** tabeli, możesz znaleźć hello zebranych danych:</span><span class="sxs-lookup"><span data-stu-id="b160a-133">In hello **WADPerformanceCounters** table, you can find hello collected data:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountBefore2.png)

### <a name="configure-hello-autoscalesettings-resource"></a><span data-ttu-id="b160a-134">Konfigurowanie zasobów autoScaleSettings hello</span><span class="sxs-lookup"><span data-stu-id="b160a-134">Configure hello autoScaleSettings resource</span></span>
<span data-ttu-id="b160a-135">Witaj autoscaleSettings zasobów używane są informacje hello z hello diagnostyki rozszerzenia toodecide czy tooincrease lub zmniejszenia hello liczba maszyn wirtualnych w skali hello zestawu.</span><span class="sxs-lookup"><span data-stu-id="b160a-135">hello autoscaleSettings resource uses hello information from hello diagnostics extension toodecide whether tooincrease or decrease hello number of virtual machines in hello scale set.</span></span>

<span data-ttu-id="b160a-136">W tym przykładzie przedstawiono konfigurację hello hello zasobu w szablonie hello:</span><span class="sxs-lookup"><span data-stu-id="b160a-136">This example shows hello configuration of hello resource in hello template:</span></span>

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

<span data-ttu-id="b160a-137">W powyższym przykładzie hello dwie reguły są tworzone dla Definiowanie hello automatycznych akcji skalowania.</span><span class="sxs-lookup"><span data-stu-id="b160a-137">In hello example above, two rules are created for defining hello automatic scaling actions.</span></span> <span data-ttu-id="b160a-138">Pierwsza reguła Hello definiuje hello akcji skalowania w poziomie i hello drugą regułę definiuje hello skali w akcji.</span><span class="sxs-lookup"><span data-stu-id="b160a-138">hello first rule defines hello scale-out action and hello second rule defines hello scale-in action.</span></span> <span data-ttu-id="b160a-139">Te wartości są dostępne w zasadach hello:</span><span class="sxs-lookup"><span data-stu-id="b160a-139">These values are provided in hello rules:</span></span>

| <span data-ttu-id="b160a-140">Reguła</span><span class="sxs-lookup"><span data-stu-id="b160a-140">Rule</span></span> | <span data-ttu-id="b160a-141">Opis</span><span class="sxs-lookup"><span data-stu-id="b160a-141">Description</span></span> |
| ---- | ----------- |
| <span data-ttu-id="b160a-142">metricName</span><span class="sxs-lookup"><span data-stu-id="b160a-142">metricName</span></span>        | <span data-ttu-id="b160a-143">Ta wartość jest hello taki sam jak licznika wydajności hello zdefiniowaną w zmiennej wadperfcounter hello hello diagnostyki rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="b160a-143">This value is hello same as hello performance counter that you defined in hello wadperfcounter variable for hello diagnostics extension.</span></span> <span data-ttu-id="b160a-144">W powyższym przykładzie hello licznik liczby wątków hello jest używany.</span><span class="sxs-lookup"><span data-stu-id="b160a-144">In hello example above, hello Thread Count counter is used.</span></span>    |
| <span data-ttu-id="b160a-145">metricResourceUri</span><span class="sxs-lookup"><span data-stu-id="b160a-145">metricResourceUri</span></span> | <span data-ttu-id="b160a-146">Ta wartość jest identyfikator zasobu hello zestaw skali maszyny wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="b160a-146">This value is hello resource identifier of hello virtual machine scale set.</span></span> <span data-ttu-id="b160a-147">Ten identyfikator zawiera hello nazwę grupy zasobów hello, hello Nazwa dostawcy zasobów hello i nazwę hello tooscale zestaw skalowania hello.</span><span class="sxs-lookup"><span data-stu-id="b160a-147">This identifier contains hello name of hello resource group, hello name of hello resource provider, and hello name of hello scale set tooscale.</span></span> |
| <span data-ttu-id="b160a-148">Ziarnem czasu</span><span class="sxs-lookup"><span data-stu-id="b160a-148">timeGrain</span></span>         | <span data-ttu-id="b160a-149">Ta wartość jest szczegółowości hello hello metryk, które są zbierane.</span><span class="sxs-lookup"><span data-stu-id="b160a-149">This value is hello granularity of hello metrics that are collected.</span></span> <span data-ttu-id="b160a-150">W hello poprzedzających przykładzie dane są zbierane w odstępach jednej minuty.</span><span class="sxs-lookup"><span data-stu-id="b160a-150">In hello preceding example, data is collected on an interval of one minute.</span></span> <span data-ttu-id="b160a-151">Ta wartość jest używana z timeWindow.</span><span class="sxs-lookup"><span data-stu-id="b160a-151">This value is used with timeWindow.</span></span> |
| <span data-ttu-id="b160a-152">Statystyka</span><span class="sxs-lookup"><span data-stu-id="b160a-152">statistic</span></span>         | <span data-ttu-id="b160a-153">Ta wartość określa, jak metryki hello są połączone tooaccommodate hello automatyczne skalowanie akcji.</span><span class="sxs-lookup"><span data-stu-id="b160a-153">This value determines how hello metrics are combined tooaccommodate hello automatic scaling action.</span></span> <span data-ttu-id="b160a-154">Witaj możliwe wartości to: średnia, Min, Max.</span><span class="sxs-lookup"><span data-stu-id="b160a-154">hello possible values are: Average, Min, Max.</span></span> |
| <span data-ttu-id="b160a-155">timeWindow</span><span class="sxs-lookup"><span data-stu-id="b160a-155">timeWindow</span></span>        | <span data-ttu-id="b160a-156">Ta wartość jest hello zakres czasu, w którym są zbierane dane wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="b160a-156">This value is hello range of time in which instance data is collected.</span></span> <span data-ttu-id="b160a-157">Musi być od 5 minut do 12 godzin.</span><span class="sxs-lookup"><span data-stu-id="b160a-157">It must be between 5 minutes and 12 hours.</span></span> |
| <span data-ttu-id="b160a-158">timeAggregation</span><span class="sxs-lookup"><span data-stu-id="b160a-158">timeAggregation</span></span>   | <span data-ttu-id="b160a-159">Ta wartość określa, jak powinny być połączone hello dane, które są zbierane wraz z upływem czasu.</span><span class="sxs-lookup"><span data-stu-id="b160a-159">This value determines how hello data that is collected should be combined over time.</span></span> <span data-ttu-id="b160a-160">Witaj domyślna wartość to średnia.</span><span class="sxs-lookup"><span data-stu-id="b160a-160">hello default value is Average.</span></span> <span data-ttu-id="b160a-161">Witaj możliwe wartości to: średnia, co najmniej, maksimum, ostatnich, łączna liczba, liczba.</span><span class="sxs-lookup"><span data-stu-id="b160a-161">hello possible values are: Average, Minimum, Maximum, Last, Total, Count.</span></span> |
| <span data-ttu-id="b160a-162">Operator</span><span class="sxs-lookup"><span data-stu-id="b160a-162">operator</span></span>          | <span data-ttu-id="b160a-163">Ta wartość jest hello operator, który jest używany toocompare hello metryki danych i hello próg.</span><span class="sxs-lookup"><span data-stu-id="b160a-163">This value is hello operator that is used toocompare hello metric data and hello threshold.</span></span> <span data-ttu-id="b160a-164">Witaj możliwe wartości to: równa, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span><span class="sxs-lookup"><span data-stu-id="b160a-164">hello possible values are: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span></span> |
| <span data-ttu-id="b160a-165">Próg</span><span class="sxs-lookup"><span data-stu-id="b160a-165">threshold</span></span>         | <span data-ttu-id="b160a-166">Ta wartość jest wartość hello wyzwala hello akcji skalowania.</span><span class="sxs-lookup"><span data-stu-id="b160a-166">This value is hello value that triggers hello scale action.</span></span> <span data-ttu-id="b160a-167">Można tooprovide się wystarczające różnicę wartości progowe hello hello **skalowalnego w poziomie** i **w skali** akcje.</span><span class="sxs-lookup"><span data-stu-id="b160a-167">Be sure tooprovide a sufficient difference between hello threshold values for hello **scale-out** and **scale-in** actions.</span></span> <span data-ttu-id="b160a-168">Jeśli ustawisz hello takie same wartości dla obu akcje systemu hello oszacowano stałej zmiany, które uniemożliwiają wdrożenie akcji skalowania.</span><span class="sxs-lookup"><span data-stu-id="b160a-168">If you set hello same values for both actions, hello system anticipates constant change, which prevents it from implementing a scaling action.</span></span> <span data-ttu-id="b160a-169">Na przykład ustawienie obu wątków too600 w hello poprzedzających przykład nie działa.</span><span class="sxs-lookup"><span data-stu-id="b160a-169">For example, setting both too600 threads in hello preceding example doesn't work.</span></span> |
| <span data-ttu-id="b160a-170">Kierunek</span><span class="sxs-lookup"><span data-stu-id="b160a-170">direction</span></span>         | <span data-ttu-id="b160a-171">Ta wartość określa akcji hello, wykonywaną, gdy uzyskuje się hello wartość progową.</span><span class="sxs-lookup"><span data-stu-id="b160a-171">This value determines hello action that is taken when hello threshold value is achieved.</span></span> <span data-ttu-id="b160a-172">Witaj możliwe wartości to zwiększyć lub zmniejszyć.</span><span class="sxs-lookup"><span data-stu-id="b160a-172">hello possible values are Increase or Decrease.</span></span> |
| <span data-ttu-id="b160a-173">type</span><span class="sxs-lookup"><span data-stu-id="b160a-173">type</span></span>              | <span data-ttu-id="b160a-174">Ta wartość jest typu hello akcji, która powinna się odbyć i musi być ustawione tooChangeCount.</span><span class="sxs-lookup"><span data-stu-id="b160a-174">This value is hello type of action that should occur and must be set tooChangeCount.</span></span> |
| <span data-ttu-id="b160a-175">wartość</span><span class="sxs-lookup"><span data-stu-id="b160a-175">value</span></span>             | <span data-ttu-id="b160a-176">Ta wartość jest liczbą hello maszyn wirtualnych, które są dodawane tooor usunięte z hello zestaw skali.</span><span class="sxs-lookup"><span data-stu-id="b160a-176">This value is hello number of virtual machines that are added tooor removed from hello scale set.</span></span> <span data-ttu-id="b160a-177">Ta wartość musi wynosić 1 lub większą.</span><span class="sxs-lookup"><span data-stu-id="b160a-177">This value must be 1 or greater.</span></span> |
| <span data-ttu-id="b160a-178">cooldown</span><span class="sxs-lookup"><span data-stu-id="b160a-178">cooldown</span></span>          | <span data-ttu-id="b160a-179">Ta wartość jest hello ilość czasu toowait od momentu ostatniej akcji skalowania hello, zanim nastąpi hello następnej akcji.</span><span class="sxs-lookup"><span data-stu-id="b160a-179">This value is hello amount of time toowait since hello last scaling action before hello next action occurs.</span></span> <span data-ttu-id="b160a-180">Ta wartość musi należeć do zakresu od minutę i jeden tydzień.</span><span class="sxs-lookup"><span data-stu-id="b160a-180">This value must be between one minute and one week.</span></span> |

<span data-ttu-id="b160a-181">W zależności od hello licznika wydajności używasz, niektóre elementy hello w konfiguracji szablonu hello są używane inaczej.</span><span class="sxs-lookup"><span data-stu-id="b160a-181">Depending on hello performance counter, you are using, some of hello elements in hello template configuration are used differently.</span></span> <span data-ttu-id="b160a-182">W hello poprzedzających przykład licznika wydajności hello to liczba wątków, wartość progowa hello jest 650 dla akcji skalowania w poziomie oraz wartości progowej hello jest 550 hello skali w akcji.</span><span class="sxs-lookup"><span data-stu-id="b160a-182">In hello preceding example, hello performance counter is Thread Count, hello threshold value is 650 for a scale-out action, and hello threshold value is 550 for hello scale-in action.</span></span> <span data-ttu-id="b160a-183">Jeśli używasz licznika, takie jak czas procesora (%), wartość progowa hello jest ustawiona toohello wartości procentowej użycia Procesora, która określa akcji skalowania.</span><span class="sxs-lookup"><span data-stu-id="b160a-183">If you use a counter such as %Processor Time, hello threshold value is set toohello percentage of CPU usage that determines a scaling action.</span></span>

<span data-ttu-id="b160a-184">Po wyzwoleniu akcji skalowania, takich jak wysokie obciążenie, zwiększa się na podstawie wartości hello w szablonie hello pojemności hello hello zestawu.</span><span class="sxs-lookup"><span data-stu-id="b160a-184">When a scaling action is triggered, such as a high load, hello capacity of hello set is increased based on hello value in hello template.</span></span> <span data-ttu-id="b160a-185">Na przykład w skali ustawić gdzie pojemności hello jest ustawiony too3, a wartość akcji skalowania hello jest ustawiony too1:</span><span class="sxs-lookup"><span data-stu-id="b160a-185">For example, in a scale set where hello capacity is set too3 and hello scale action value is set too1:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerBefore.png)

<span data-ttu-id="b160a-186">Gdy hello bieżącego obciążenia przyczyny hello wątku średnia liczba toogo powyżej progu hello 650:</span><span class="sxs-lookup"><span data-stu-id="b160a-186">When hello current load causes hello average thread count toogo above hello threshold of 650:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountAfter.png)

<span data-ttu-id="b160a-187">A **skalowalnego w poziomie** akcji zostanie wywołany, że przyczyny hello pojemności toobe zestaw hello zwiększonego o jeden:</span><span class="sxs-lookup"><span data-stu-id="b160a-187">A **scale-out** action is triggered that causes hello capacity of hello set toobe increased by one:</span></span>

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 4
},
```

<span data-ttu-id="b160a-188">wynik Hello jest jest dodać toohello zestaw skali maszyny wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="b160a-188">hello result is a virtual machine is added toohello scale set:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerAfter.png)

<span data-ttu-id="b160a-189">Po upływie cooldown pięć minut Jeśli hello średnią liczbę wątków na maszynach hello pozostaje ponad 600 inną maszynę jest dodawana toohello zestawu.</span><span class="sxs-lookup"><span data-stu-id="b160a-189">After a cooldown period of five minutes, if hello average number of threads on hello machines stays over 600, another machine is added toohello set.</span></span> <span data-ttu-id="b160a-190">Jeśli liczba wątków średni hello pozostaje poniżej 550, hello pojemność zestawu skalowania hello zostanie zmniejszona o jeden, a maszyna zostanie usunięta z hello zestawu.</span><span class="sxs-lookup"><span data-stu-id="b160a-190">If hello average thread count stays below 550, hello capacity of hello scale set is reduced by one and a machine is removed from hello set.</span></span>

## <a name="set-up-scaling-using-azure-powershell"></a><span data-ttu-id="b160a-191">Ustawianie skalowania przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b160a-191">Set up scaling using Azure PowerShell</span></span>

<span data-ttu-id="b160a-192">Przyjrzyj się przy użyciu programu PowerShell tooset się Skalowanie automatyczne, przykłady toosee [Azure PowerShell Monitor szybki start przykłady](../monitoring-and-diagnostics/insights-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b160a-192">toosee examples of using PowerShell tooset up autoscaling, look at [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md).</span></span>

## <a name="set-up-scaling-using-azure-cli"></a><span data-ttu-id="b160a-193">Ustawianie skalowania przy użyciu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b160a-193">Set up scaling using Azure CLI</span></span>

<span data-ttu-id="b160a-194">Przyjrzyj się przy użyciu interfejsu wiersza polecenia Azure tooset się Skalowanie automatyczne, przykłady toosee [Azure Monitor i platform interfejsu wiersza polecenia Szybki start przykłady](../monitoring-and-diagnostics/insights-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b160a-194">toosee examples of using Azure CLI tooset up autoscaling, look at [Azure Monitor Cross-platform CLI quick start samples](../monitoring-and-diagnostics/insights-cli-samples.md).</span></span>

## <a name="set-up-scaling-using-hello-azure-portal"></a><span data-ttu-id="b160a-195">Ustawianie skalowania za pomocą hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="b160a-195">Set up scaling using hello Azure portal</span></span>

<span data-ttu-id="b160a-196">przykład użycia toosee hello Azure portalu tooset się Skalowanie automatyczne, poszukać w [tworzenia zestawu skalowania maszyn wirtualnych przy użyciu portalu Azure hello](virtual-machine-scale-sets-portal-create.md).</span><span class="sxs-lookup"><span data-stu-id="b160a-196">toosee an example of using hello Azure portal tooset up autoscaling, look at [Create a Virtual Machine Scale Set using hello Azure portal](virtual-machine-scale-sets-portal-create.md).</span></span>

## <a name="investigate-scaling-actions"></a><span data-ttu-id="b160a-197">Zbadaj akcji skalowania</span><span class="sxs-lookup"><span data-stu-id="b160a-197">Investigate scaling actions</span></span>

* <span data-ttu-id="b160a-198">**Witryna Azure Portal**</span><span class="sxs-lookup"><span data-stu-id="b160a-198">**Azure portal**</span></span>  
<span data-ttu-id="b160a-199">Obecnie można uzyskać ograniczone informacje przy użyciu portalu hello.</span><span class="sxs-lookup"><span data-stu-id="b160a-199">You can currently get a limited amount of information using hello portal.</span></span>

* <span data-ttu-id="b160a-200">**Eksplorator zasobów Azure**</span><span class="sxs-lookup"><span data-stu-id="b160a-200">**Azure Resource Explorer**</span></span>  
<span data-ttu-id="b160a-201">To narzędzie jest hello najlepsze do eksplorowania hello bieżącego stanu sieci zestawu skali.</span><span class="sxs-lookup"><span data-stu-id="b160a-201">This tool is hello best for exploring hello current state of your scale set.</span></span> <span data-ttu-id="b160a-202">Tej ścieżki i powinna zostać wyświetlona zestawu widok wystąpienia hello skali hello utworzony:</span><span class="sxs-lookup"><span data-stu-id="b160a-202">Follow this path and you should see hello instance view of hello scale set that you created:</span></span>  
<span data-ttu-id="b160a-203">**Subskrypcje > {subskrypcji} > resourceGroups > {grupie zasobów} > dostawców > Microsoft.Compute > virtualMachineScaleSets > {zestawie skali} > maszyn wirtualnych**</span><span class="sxs-lookup"><span data-stu-id="b160a-203">**Subscriptions > {your subscription} > resourceGroups > {your resource group} > providers > Microsoft.Compute > virtualMachineScaleSets > {your scale set} > virtualMachines**</span></span>

* <span data-ttu-id="b160a-204">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="b160a-204">**Azure PowerShell**</span></span>  
<span data-ttu-id="b160a-205">Użyj tego polecenia tooget niektóre informacje:</span><span class="sxs-lookup"><span data-stu-id="b160a-205">Use this command tooget some information:</span></span>

  ```powershell
  Get-AzureRmResource -name vmsstest1 -ResourceGroupName vmsstestrg1 -ResourceType Microsoft.Compute/virtualMachineScaleSets -ApiVersion 2015-06-15
  Get-Autoscalesetting -ResourceGroup rainvmss -DetailedOutput
  ```

* <span data-ttu-id="b160a-206">Łączenie maszyny wirtualnej jumpbox toohello, podobnie jak inne maszyny, a następnie można zdalnie przejść hello maszyn wirtualnych w hello skali zestaw toomonitor poszczególnych procesów.</span><span class="sxs-lookup"><span data-stu-id="b160a-206">Connect toohello jumpbox virtual machine just like you would any other machine and then you can remotely access hello virtual machines in hello scale set toomonitor individual processes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b160a-207">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b160a-207">Next Steps</span></span>
* <span data-ttu-id="b160a-208">Przyjrzyj się [automatycznie skalować maszyny w zestawie skalowania maszyn wirtualnych](virtual-machine-scale-sets-windows-autoscale.md) toosee przykładem toocreate skali konfiguracji przy użyciu automatycznego skalowania skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="b160a-208">Look at [Automatically scale machines in a Virtual Machine Scale Set](virtual-machine-scale-sets-windows-autoscale.md) toosee an example of how toocreate a scale set with automatic scaling configured.</span></span>

* <span data-ttu-id="b160a-209">Znajdź przykłady Azure Monitor funkcje w [Azure PowerShell Monitor szybki start — przykłady](../monitoring-and-diagnostics/insights-powershell-samples.md)</span><span class="sxs-lookup"><span data-stu-id="b160a-209">Find examples of Azure Monitor monitoring features in [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md)</span></span>

* <span data-ttu-id="b160a-210">Dowiedz się więcej o funkcji powiadomień w [Użyj skalowania automatycznego akcje toosend poczty e-mail i elementu webhook powiadomień o alertach w monitorze Azure](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md).</span><span class="sxs-lookup"><span data-stu-id="b160a-210">Learn about notification features in [Use autoscale actions toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md).</span></span>

* <span data-ttu-id="b160a-211">Dowiedz się więcej o zbyt[dzienniki inspekcji użycia w monitorze Azure, toosend poczty e-mail i elementu webhook powiadomień o alertach](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="b160a-211">Learn about how too[Use audit logs toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span></span>

* <span data-ttu-id="b160a-212">Dowiedz się więcej o [zaawansowanych scenariuszy skalowania automatycznego](virtual-machine-scale-sets-advanced-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="b160a-212">Learn about [advanced autoscale scenarios](virtual-machine-scale-sets-advanced-autoscale.md).</span></span>
