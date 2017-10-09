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
# <a name="how-toouse-automatic-scaling-and-virtual-machine-scale-sets"></a>Jak toouse automatyczne skalowanie i zestawy skalowania maszyny wirtualnej
Automatyczne skalowanie maszyn wirtualnych w zestawie skalowania jest tworzenie hello lub usunięcia maszyn w hello Ustaw jako potrzebne toomatch wymagania dotyczące wydajności. Wraz z rozwojem hello ilość pracy, aplikacja może wymagać dodatkowych zasobów tooenable on tooeffectively wykonywania zadań.

Automatyczne skalowanie jest zautomatyzowany proces czy pomaga upraszczają zarządzanie. Przez zmniejszenie nakładów pracy, nie należy monitorować wydajność systemu toocontinually lub zdecydować, jak toomanage zasobów. Skalowanie jest procesem elastycznej. Więcej zasobów do dodania jako hello wzrostu obciążenia. I jako spadku żądanie zasoby mogą zostać usunięte toominimize kosztów i Obsługa poziomów wydajności.

Skonfiguruj automatyczne skalowanie w skali skonfigurowane przy użyciu usługi Azure Resource Manager szablonu programu Azure PowerShell, interfejsu wiersza polecenia Azure albo hello portalu Azure.

## <a name="set-up-scaling-by-using-resource-manager-templates"></a>Ustawianie skalowania przy użyciu szablonów usługi Resource Manager
Zamiast wdrażania i zarządzania nimi każdego zasobu aplikacji oddzielnie, należy użyć szablonu, który wdraża wszystkie zasoby w jednej, skoordynowanej operacji. W szablonie hello są zdefiniowane zasoby aplikacji i parametrów wdrożenia są określone dla różnych środowisk. Szablon Hello składa się z kodu JSON i wyrażeń, że możesz użyć wartości tooconstruct dla danego wdrożenia. toolearn, obejrzyj [szablonów Authoring Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

W szablonie hello należy określić element pojemności hello:

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 3
},
```

Pojemność identyfikuje hello liczbę maszyn wirtualnych w zestawie hello. Możesz ręcznie zmienić hello pojemności poprzez wdrożenie szablonu, podając inną wartość. Jeśli wdrażasz szablon tooonly zmiany hello pojemności może zawierać tylko element SKU hello o pojemności hello zaktualizowane.

Witaj pojemność zestawu skalowania można automatycznie dostosować przy użyciu kombinacji hello **autoscaleSettings** zasobów i hello rozszerzenie diagnostyki.

### <a name="configure-hello-azure-diagnostics-extension"></a>Skonfiguruj rozszerzenie Azure Diagnostics hello
Automatyczne skalowanie jest możliwe tylko w przypadku pomyślnego nawiązania na każdej maszynie wirtualnej w zestawie skalowania hello kolekcji metryki. Witaj rozszerzenia diagnostyki Azure udostępnia możliwości monitorowania i diagnostyki hello, które zaspokoi potrzeby zbierania miar hello hello automatycznego skalowania zasobu. Rozszerzenie hello można zainstalować jako część hello szablonu usługi Resource Manager.

Ten przykład przedstawia hello zmienne, które są używane w hello szablonu tooconfigure hello diagnostyki rozszerzenia:

```json
"diagnosticsStorageAccountName": "[concat(parameters('resourcePrefix'), 'saa')]",
"accountid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/', 'Microsoft.Storage/storageAccounts/', variables('diagnosticsStorageAccountName'))]",
"wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
"wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Thread Count\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
"wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
"wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
"wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
```

Parametry są udostępniane po wdrożeniu hello szablonu. W tym przykładzie, nazwa hello hello konta magazynu (w którym są przechowywane dane) i hello podano nazwę zestawu skali hello (w którym dane są zbierane). Również w tym przykładzie systemu Windows Server, zbierane są tylko hello licznika wydajności liczba wątków. Witaj wszystkich dostępnych liczników wydajności w systemie Windows lub Linux mogą być używane toocollect informacje diagnostyczne i może być uwzględniony w konfiguracji rozszerzenia hello.

W tym przykładzie przedstawiono definicję hello rozszerzenia hello w szablonie hello:

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

Po uruchomieniu rozszerzenia diagnostyki hello hello danych są przechowywane i zebrane w tabeli, hello konta magazynu, który określisz. W hello **WADPerformanceCounters** tabeli, możesz znaleźć hello zebranych danych:

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountBefore2.png)

### <a name="configure-hello-autoscalesettings-resource"></a>Konfigurowanie zasobów autoScaleSettings hello
Witaj autoscaleSettings zasobów używane są informacje hello z hello diagnostyki rozszerzenia toodecide czy tooincrease lub zmniejszenia hello liczba maszyn wirtualnych w skali hello zestawu.

W tym przykładzie przedstawiono konfigurację hello hello zasobu w szablonie hello:

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

W powyższym przykładzie hello dwie reguły są tworzone dla Definiowanie hello automatycznych akcji skalowania. Pierwsza reguła Hello definiuje hello akcji skalowania w poziomie i hello drugą regułę definiuje hello skali w akcji. Te wartości są dostępne w zasadach hello:

| Reguła | Opis |
| ---- | ----------- |
| metricName        | Ta wartość jest hello taki sam jak licznika wydajności hello zdefiniowaną w zmiennej wadperfcounter hello hello diagnostyki rozszerzenia. W powyższym przykładzie hello licznik liczby wątków hello jest używany.    |
| metricResourceUri | Ta wartość jest identyfikator zasobu hello zestaw skali maszyny wirtualnej hello. Ten identyfikator zawiera hello nazwę grupy zasobów hello, hello Nazwa dostawcy zasobów hello i nazwę hello tooscale zestaw skalowania hello. |
| Ziarnem czasu         | Ta wartość jest szczegółowości hello hello metryk, które są zbierane. W hello poprzedzających przykładzie dane są zbierane w odstępach jednej minuty. Ta wartość jest używana z timeWindow. |
| Statystyka         | Ta wartość określa, jak metryki hello są połączone tooaccommodate hello automatyczne skalowanie akcji. Witaj możliwe wartości to: średnia, Min, Max. |
| timeWindow        | Ta wartość jest hello zakres czasu, w którym są zbierane dane wystąpienia. Musi być od 5 minut do 12 godzin. |
| timeAggregation   | Ta wartość określa, jak powinny być połączone hello dane, które są zbierane wraz z upływem czasu. Witaj domyślna wartość to średnia. Witaj możliwe wartości to: średnia, co najmniej, maksimum, ostatnich, łączna liczba, liczba. |
| Operator          | Ta wartość jest hello operator, który jest używany toocompare hello metryki danych i hello próg. Witaj możliwe wartości to: równa, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual. |
| Próg         | Ta wartość jest wartość hello wyzwala hello akcji skalowania. Można tooprovide się wystarczające różnicę wartości progowe hello hello **skalowalnego w poziomie** i **w skali** akcje. Jeśli ustawisz hello takie same wartości dla obu akcje systemu hello oszacowano stałej zmiany, które uniemożliwiają wdrożenie akcji skalowania. Na przykład ustawienie obu wątków too600 w hello poprzedzających przykład nie działa. |
| Kierunek         | Ta wartość określa akcji hello, wykonywaną, gdy uzyskuje się hello wartość progową. Witaj możliwe wartości to zwiększyć lub zmniejszyć. |
| type              | Ta wartość jest typu hello akcji, która powinna się odbyć i musi być ustawione tooChangeCount. |
| wartość             | Ta wartość jest liczbą hello maszyn wirtualnych, które są dodawane tooor usunięte z hello zestaw skali. Ta wartość musi wynosić 1 lub większą. |
| cooldown          | Ta wartość jest hello ilość czasu toowait od momentu ostatniej akcji skalowania hello, zanim nastąpi hello następnej akcji. Ta wartość musi należeć do zakresu od minutę i jeden tydzień. |

W zależności od hello licznika wydajności używasz, niektóre elementy hello w konfiguracji szablonu hello są używane inaczej. W hello poprzedzających przykład licznika wydajności hello to liczba wątków, wartość progowa hello jest 650 dla akcji skalowania w poziomie oraz wartości progowej hello jest 550 hello skali w akcji. Jeśli używasz licznika, takie jak czas procesora (%), wartość progowa hello jest ustawiona toohello wartości procentowej użycia Procesora, która określa akcji skalowania.

Po wyzwoleniu akcji skalowania, takich jak wysokie obciążenie, zwiększa się na podstawie wartości hello w szablonie hello pojemności hello hello zestawu. Na przykład w skali ustawić gdzie pojemności hello jest ustawiony too3, a wartość akcji skalowania hello jest ustawiony too1:

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerBefore.png)

Gdy hello bieżącego obciążenia przyczyny hello wątku średnia liczba toogo powyżej progu hello 650:

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountAfter.png)

A **skalowalnego w poziomie** akcji zostanie wywołany, że przyczyny hello pojemności toobe zestaw hello zwiększonego o jeden:

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 4
},
```

wynik Hello jest jest dodać toohello zestaw skali maszyny wirtualnej:

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerAfter.png)

Po upływie cooldown pięć minut Jeśli hello średnią liczbę wątków na maszynach hello pozostaje ponad 600 inną maszynę jest dodawana toohello zestawu. Jeśli liczba wątków średni hello pozostaje poniżej 550, hello pojemność zestawu skalowania hello zostanie zmniejszona o jeden, a maszyna zostanie usunięta z hello zestawu.

## <a name="set-up-scaling-using-azure-powershell"></a>Ustawianie skalowania przy użyciu programu Azure PowerShell

Przyjrzyj się przy użyciu programu PowerShell tooset się Skalowanie automatyczne, przykłady toosee [Azure PowerShell Monitor szybki start przykłady](../monitoring-and-diagnostics/insights-powershell-samples.md).

## <a name="set-up-scaling-using-azure-cli"></a>Ustawianie skalowania przy użyciu wiersza polecenia platformy Azure

Przyjrzyj się przy użyciu interfejsu wiersza polecenia Azure tooset się Skalowanie automatyczne, przykłady toosee [Azure Monitor i platform interfejsu wiersza polecenia Szybki start przykłady](../monitoring-and-diagnostics/insights-cli-samples.md).

## <a name="set-up-scaling-using-hello-azure-portal"></a>Ustawianie skalowania za pomocą hello portalu Azure

przykład użycia toosee hello Azure portalu tooset się Skalowanie automatyczne, poszukać w [tworzenia zestawu skalowania maszyn wirtualnych przy użyciu portalu Azure hello](virtual-machine-scale-sets-portal-create.md).

## <a name="investigate-scaling-actions"></a>Zbadaj akcji skalowania

* **Witryna Azure Portal**  
Obecnie można uzyskać ograniczone informacje przy użyciu portalu hello.

* **Eksplorator zasobów Azure**  
To narzędzie jest hello najlepsze do eksplorowania hello bieżącego stanu sieci zestawu skali. Tej ścieżki i powinna zostać wyświetlona zestawu widok wystąpienia hello skali hello utworzony:  
**Subskrypcje > {subskrypcji} > resourceGroups > {grupie zasobów} > dostawców > Microsoft.Compute > virtualMachineScaleSets > {zestawie skali} > maszyn wirtualnych**

* **Azure PowerShell**  
Użyj tego polecenia tooget niektóre informacje:

  ```powershell
  Get-AzureRmResource -name vmsstest1 -ResourceGroupName vmsstestrg1 -ResourceType Microsoft.Compute/virtualMachineScaleSets -ApiVersion 2015-06-15
  Get-Autoscalesetting -ResourceGroup rainvmss -DetailedOutput
  ```

* Łączenie maszyny wirtualnej jumpbox toohello, podobnie jak inne maszyny, a następnie można zdalnie przejść hello maszyn wirtualnych w hello skali zestaw toomonitor poszczególnych procesów.

## <a name="next-steps"></a>Następne kroki
* Przyjrzyj się [automatycznie skalować maszyny w zestawie skalowania maszyn wirtualnych](virtual-machine-scale-sets-windows-autoscale.md) toosee przykładem toocreate skali konfiguracji przy użyciu automatycznego skalowania skonfigurowane.

* Znajdź przykłady Azure Monitor funkcje w [Azure PowerShell Monitor szybki start — przykłady](../monitoring-and-diagnostics/insights-powershell-samples.md)

* Dowiedz się więcej o funkcji powiadomień w [Użyj skalowania automatycznego akcje toosend poczty e-mail i elementu webhook powiadomień o alertach w monitorze Azure](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md).

* Dowiedz się więcej o zbyt[dzienniki inspekcji użycia w monitorze Azure, toosend poczty e-mail i elementu webhook powiadomień o alertach](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)

* Dowiedz się więcej o [zaawansowanych scenariuszy skalowania automatycznego](virtual-machine-scale-sets-advanced-autoscale.md).
