---
title: "Przykłady szybki start Azure PowerShell monitora. | Microsoft Docs"
description: "Dostęp do funkcji Azure Monitor, takich jak skalowania automatycznego, alertów, elementów webhook i wyszukiwanie Dzienniki aktywności za pomocą programu PowerShell."
author: kamathashwin
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: c0761814-7148-4ab5-8c27-a2c9fa4cfef5
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: ashwink
ms.openlocfilehash: 48f064884c2a6d0a55cc58a44169ed03c62de46d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-monitor-powershell-quick-start-samples"></a><span data-ttu-id="c623b-104">Przykładów dla platformy Azure Monitor PowerShell szybki start</span><span class="sxs-lookup"><span data-stu-id="c623b-104">Azure Monitor PowerShell quick start samples</span></span>
<span data-ttu-id="c623b-105">Ten artykuł przedstawia przykładowe polecenia programu PowerShell, aby ułatwić dostęp do funkcji Azure monitora.</span><span class="sxs-lookup"><span data-stu-id="c623b-105">This article shows you sample PowerShell commands to help you access Azure Monitor features.</span></span> <span data-ttu-id="c623b-106">Azure Monitor pozwala automatycznego skalowania usługi w chmurze, maszyn wirtualnych i aplikacji sieci Web, jak i do wysyłania powiadomień o alertach lub zadzwoń na podstawie wartości dane telemetryczne skonfigurowanych adresów URL sieci web.</span><span class="sxs-lookup"><span data-stu-id="c623b-106">Azure Monitor allows you to AutoScale Cloud Services, Virtual Machines, and Web Apps and to send alert notifications or call web URLs based on values of configured telemetry data.</span></span>

> [!NOTE]
> <span data-ttu-id="c623b-107">Azure Monitor to nowa nazwa dla proponowaną "Azure Insights" do 25 września 2016 r.</span><span class="sxs-lookup"><span data-stu-id="c623b-107">Azure Monitor is the new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="c623b-108">Jednak przestrzenie nazw i w związku z tym następujące polecenia nadal zawierają "insights".</span><span class="sxs-lookup"><span data-stu-id="c623b-108">However, the namespaces and thus the following commands still contain the "insights".</span></span>
> 
> 

## <a name="set-up-powershell"></a><span data-ttu-id="c623b-109">Konfigurowanie środowiska PowerShell</span><span class="sxs-lookup"><span data-stu-id="c623b-109">Set up PowerShell</span></span>
<span data-ttu-id="c623b-110">Jeśli nie jest jeszcze zdefiniować programu PowerShell do uruchamiania na komputerze.</span><span class="sxs-lookup"><span data-stu-id="c623b-110">If you haven't already, set up PowerShell to run on your computer.</span></span> <span data-ttu-id="c623b-111">Aby uzyskać więcej informacji, zobacz [Instalowanie i konfigurowanie programu PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c623b-111">For more information, see [How to Install and Configure PowerShell](/powershell/azure/overview).</span></span>

## <a name="examples-in-this-article"></a><span data-ttu-id="c623b-112">Przykłady w tym artykule</span><span class="sxs-lookup"><span data-stu-id="c623b-112">Examples in this article</span></span>
<span data-ttu-id="c623b-113">Przykłady w artykule pokazują, jak można użyć poleceń cmdlet Azure monitora.</span><span class="sxs-lookup"><span data-stu-id="c623b-113">The examples in the article illustrate how you can use Azure Monitor cmdlets.</span></span> <span data-ttu-id="c623b-114">Można również przejrzeć całą listę poleceń cmdlet programu PowerShell usługi Azure monitora na [poleceń cmdlet Azure monitora (Insights)](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx).</span><span class="sxs-lookup"><span data-stu-id="c623b-114">You can also review the entire list of Azure Monitor PowerShell cmdlets at [Azure Monitor (Insights) Cmdlets](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx).</span></span>

## <a name="sign-in-and-use-subscriptions"></a><span data-ttu-id="c623b-115">Zaloguj się i korzystać z subskrypcji</span><span class="sxs-lookup"><span data-stu-id="c623b-115">Sign in and use subscriptions</span></span>
<span data-ttu-id="c623b-116">Po pierwsze Zaloguj się do subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c623b-116">First, log in to your Azure subscription.</span></span>

```PowerShell
Login-AzureRmAccount
```

<span data-ttu-id="c623b-117">Wymaga zalogowania się.</span><span class="sxs-lookup"><span data-stu-id="c623b-117">This requires you to sign in.</span></span> <span data-ttu-id="c623b-118">Gdy to zrobisz, Twoje konto dla identyfikatora dzierżawcy i domyślnego Identyfikatora subskrypcji są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="c623b-118">Once you do, your Account, TenantID and default Subscription ID are displayed.</span></span> <span data-ttu-id="c623b-119">Wszystkie polecenia cmdlet systemu Azure działają w kontekście subskrypcji domyślne.</span><span class="sxs-lookup"><span data-stu-id="c623b-119">All the Azure cmdlets work in the context of your default subscription.</span></span> <span data-ttu-id="c623b-120">Aby wyświetlić subskrypcje, do których masz dostęp do listy, użyj następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="c623b-120">To view the list of subscriptions you have access to, use the following command.</span></span>

```PowerShell
Get-AzureRmSubscription
```

<span data-ttu-id="c623b-121">Aby zmienić kontekst pracy do innej subskrypcji, użyj następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="c623b-121">To change your working context to a different subscription, use the following command.</span></span>

```PowerShell
Set-AzureRmContext -SubscriptionId <subscriptionid>
```


## <a name="retrieve-activity-log-for-a-subscription"></a><span data-ttu-id="c623b-122">Pobrać dziennik aktywności dla subskrypcji</span><span class="sxs-lookup"><span data-stu-id="c623b-122">Retrieve Activity log for a subscription</span></span>
<span data-ttu-id="c623b-123">Użyj `Get-AzureRmLog` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c623b-123">Use the `Get-AzureRmLog` cmdlet.</span></span>  <span data-ttu-id="c623b-124">Poniżej przedstawiono niektóre typowe przykłady.</span><span class="sxs-lookup"><span data-stu-id="c623b-124">The following are some common examples.</span></span>

<span data-ttu-id="c623b-125">Pobierz wpisy dziennika z tym datę i godzinę do prezentowania:</span><span class="sxs-lookup"><span data-stu-id="c623b-125">Get log entries from this time/date to present:</span></span>

```PowerShell
Get-AzureRmLog -StartTime 2016-03-01T10:30
```

<span data-ttu-id="c623b-126">Pobierz wpisy dziennika z zakresu daty/godziny:</span><span class="sxs-lookup"><span data-stu-id="c623b-126">Get log entries between a time/date range:</span></span>

```PowerShell
Get-AzureRmLog -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

<span data-ttu-id="c623b-127">Pobierz wpisy dziennika z danej grupy zasobów:</span><span class="sxs-lookup"><span data-stu-id="c623b-127">Get log entries from a specific resource group:</span></span>

```PowerShell
Get-AzureRmLog -ResourceGroup 'myrg1'
```

<span data-ttu-id="c623b-128">Wpisy dziennika należy uzyskać od dostawcy zasobów określonego zakresu daty/godziny:</span><span class="sxs-lookup"><span data-stu-id="c623b-128">Get log entries from a specific resource provider between a time/date range:</span></span>

```PowerShell
Get-AzureRmLog -ResourceProvider 'Microsoft.Web' -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

<span data-ttu-id="c623b-129">Pobierz wszystkie wpisy dziennika z określonym obiektem wywołującym:</span><span class="sxs-lookup"><span data-stu-id="c623b-129">Get all log entries with a specific caller:</span></span>

```PowerShell
Get-AzureRmLog -Caller 'myname@company.com'
```

<span data-ttu-id="c623b-130">Polecenie pobiera ostatnich 1000 zdarzenia z dziennika aktywności:</span><span class="sxs-lookup"><span data-stu-id="c623b-130">The following command retrieves the last 1000 events from the activity log:</span></span>

```PowerShell
Get-AzureRmLog -MaxEvents 1000
```

<span data-ttu-id="c623b-131">`Get-AzureRmLog`obsługuje wiele innych parametrów.</span><span class="sxs-lookup"><span data-stu-id="c623b-131">`Get-AzureRmLog` supports many other parameters.</span></span> <span data-ttu-id="c623b-132">Zobacz `Get-AzureRmLog` odwołania, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="c623b-132">See the `Get-AzureRmLog` reference for more information.</span></span>

> [!NOTE]
> <span data-ttu-id="c623b-133">`Get-AzureRmLog`zapewnia tylko 15 dni historii.</span><span class="sxs-lookup"><span data-stu-id="c623b-133">`Get-AzureRmLog` only provides 15 days of history.</span></span> <span data-ttu-id="c623b-134">Przy użyciu **- MaxEvents** parametr umożliwia zapytania ostatniego N zdarzeń ponad 15 dni.</span><span class="sxs-lookup"><span data-stu-id="c623b-134">Using the **-MaxEvents** parameter allows you to query the last N events, beyond 15 days.</span></span> <span data-ttu-id="c623b-135">Aby dostępu zdarzenia starsze niż 15 dni należy użyć interfejsu API REST lub zestawu SDK (C# przykład przy użyciu zestawu SDK).</span><span class="sxs-lookup"><span data-stu-id="c623b-135">To access events older than 15 days, use the REST API or SDK (C# sample using the SDK).</span></span> <span data-ttu-id="c623b-136">Jeśli nie zostanie uwzględniony **StartTime**, to wartością domyślną jest **EndTime** minus jedną godzinę.</span><span class="sxs-lookup"><span data-stu-id="c623b-136">If you do not include **StartTime**, then the default value is **EndTime** minus one hour.</span></span> <span data-ttu-id="c623b-137">Jeśli nie zostanie uwzględniony **EndTime**, to wartością domyślną jest bieżący czas.</span><span class="sxs-lookup"><span data-stu-id="c623b-137">If you do not include **EndTime**, then the default value is current time.</span></span> <span data-ttu-id="c623b-138">Wszystkie godziny są w formacie UTC.</span><span class="sxs-lookup"><span data-stu-id="c623b-138">All times are in UTC.</span></span>
> 
> 

## <a name="retrieve-alerts-history"></a><span data-ttu-id="c623b-139">Pobrać historii alertów</span><span class="sxs-lookup"><span data-stu-id="c623b-139">Retrieve alerts history</span></span>
<span data-ttu-id="c623b-140">Aby wyświetlić wszystkie zdarzenia alertu, można zbadać dzienniki usługi Azure Resource Manager za pomocą poniższych przykładów.</span><span class="sxs-lookup"><span data-stu-id="c623b-140">To view all alert events, you can query the Azure Resource Manager logs using the following examples.</span></span>

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/alertRules" -DetailedOutput -StartTime 2015-03-01
```

<span data-ttu-id="c623b-141">Aby wyświetlić historię dla określonej reguły alertu, można użyć `Get-AzureRmAlertHistory` polecenia cmdlet, przekazując identyfikator zasobu reguły alertu.</span><span class="sxs-lookup"><span data-stu-id="c623b-141">To view the history for a specific alert rule, you can use the `Get-AzureRmAlertHistory` cmdlet, passing in the resource ID of the alert rule.</span></span>

```PowerShell
Get-AzureRmAlertHistory -ResourceId /subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/myalert -StartTime 2016-03-1 -Status Activated
```

<span data-ttu-id="c623b-142">`Get-AzureRmAlertHistory` Polecenie cmdlet obsługuje różne parametry.</span><span class="sxs-lookup"><span data-stu-id="c623b-142">The `Get-AzureRmAlertHistory` cmdlet supports various parameters.</span></span> <span data-ttu-id="c623b-143">Więcej informacji, zobacz [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).</span><span class="sxs-lookup"><span data-stu-id="c623b-143">More information, see [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).</span></span>

## <a name="retrieve-information-on-alert-rules"></a><span data-ttu-id="c623b-144">Pobieranie informacji na temat reguł alertów</span><span class="sxs-lookup"><span data-stu-id="c623b-144">Retrieve information on alert rules</span></span>
<span data-ttu-id="c623b-145">Wszystkie z poniższych poleceń, działają na grupy zasobów o nazwie "montest".</span><span class="sxs-lookup"><span data-stu-id="c623b-145">All of the following commands act on a Resource Group named "montest".</span></span>

<span data-ttu-id="c623b-146">Wyświetl wszystkie właściwości reguły alertu:</span><span class="sxs-lookup"><span data-stu-id="c623b-146">View all the properties of the alert rule:</span></span>

```PowerShell
Get-AzureRmAlertRule -Name simpletestCPU -ResourceGroup montest -DetailedOutput
```

<span data-ttu-id="c623b-147">Pobieranie wszystkich alertów w grupie zasobów:</span><span class="sxs-lookup"><span data-stu-id="c623b-147">Retrieve all alerts on a resource group:</span></span>

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest
```

<span data-ttu-id="c623b-148">Pobierz wszystkie reguły alertu dla zasobu docelowego.</span><span class="sxs-lookup"><span data-stu-id="c623b-148">Retrieve all alert rules set for a target resource.</span></span> <span data-ttu-id="c623b-149">Na przykład wszystkie reguły alertu ustawione na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c623b-149">For example, all alert rules set on a VM.</span></span>

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest -TargetResourceId /subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig
```

<span data-ttu-id="c623b-150">`Get-AzureRmAlertRule`obsługuje inne parametry.</span><span class="sxs-lookup"><span data-stu-id="c623b-150">`Get-AzureRmAlertRule` supports other parameters.</span></span> <span data-ttu-id="c623b-151">Zobacz [Get AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="c623b-151">See [Get-AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) for more information.</span></span>

## <a name="create-metric-alerts"></a><span data-ttu-id="c623b-152">Tworzenie metryk alertów</span><span class="sxs-lookup"><span data-stu-id="c623b-152">Create metric alerts</span></span>
<span data-ttu-id="c623b-153">Można użyć `Add-AlertRule` polecenia cmdlet, aby tworzyć, aktualizować lub wyłączyć regułę alertu.</span><span class="sxs-lookup"><span data-stu-id="c623b-153">You can use the `Add-AlertRule` cmdlet to create, update or disable an alert rule.</span></span>

<span data-ttu-id="c623b-154">Można utworzyć właściwości poczty e-mail i elementu webhook za pomocą `New-AzureRmAlertRuleEmail` i `New-AzureRmAlertRuleWebhook`odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="c623b-154">You can create email and webhook properties using  `New-AzureRmAlertRuleEmail` and `New-AzureRmAlertRuleWebhook`, respectively.</span></span> <span data-ttu-id="c623b-155">W poleceniu cmdlet reguły alertu, przypisz je jako akcje **akcje** właściwości reguły alertu.</span><span class="sxs-lookup"><span data-stu-id="c623b-155">In the Alert rule cmdlet, assign these as actions to the **Actions** property of the Alert Rule.</span></span>

<span data-ttu-id="c623b-156">W poniższej tabeli opisano parametry i wartości używane do utworzenia alertu za pomocą metryki.</span><span class="sxs-lookup"><span data-stu-id="c623b-156">The following table describes the parameters and values used to create an alert using a metric.</span></span>

| <span data-ttu-id="c623b-157">Parametr</span><span class="sxs-lookup"><span data-stu-id="c623b-157">parameter</span></span> | <span data-ttu-id="c623b-158">wartość</span><span class="sxs-lookup"><span data-stu-id="c623b-158">value</span></span> |
| --- | --- |
| <span data-ttu-id="c623b-159">Nazwa</span><span class="sxs-lookup"><span data-stu-id="c623b-159">Name</span></span> |<span data-ttu-id="c623b-160">simpletestdiskwrite</span><span class="sxs-lookup"><span data-stu-id="c623b-160">simpletestdiskwrite</span></span> |
| <span data-ttu-id="c623b-161">Lokalizacja tę regułę alertów</span><span class="sxs-lookup"><span data-stu-id="c623b-161">Location of this alert rule</span></span> |<span data-ttu-id="c623b-162">Wschodnie stany USA</span><span class="sxs-lookup"><span data-stu-id="c623b-162">East US</span></span> |
| <span data-ttu-id="c623b-163">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c623b-163">ResourceGroup</span></span> |<span data-ttu-id="c623b-164">montest</span><span class="sxs-lookup"><span data-stu-id="c623b-164">montest</span></span> |
| <span data-ttu-id="c623b-165">Element TargetResourceId</span><span class="sxs-lookup"><span data-stu-id="c623b-165">TargetResourceId</span></span> |<span data-ttu-id="c623b-166">/Subscriptions/S1/resourceGroups/montest/Providers/Microsoft.COMPUTE/virtualMachines/testconfig</span><span class="sxs-lookup"><span data-stu-id="c623b-166">/subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig</span></span> |
| <span data-ttu-id="c623b-167">MetricName alertu, który jest tworzony</span><span class="sxs-lookup"><span data-stu-id="c623b-167">MetricName of the alert that is created</span></span> |<span data-ttu-id="c623b-168">\Disk \PhysicalDisk (_Total) / s. Zobacz `Get-MetricDefinitions` polecenia cmdlet dotyczące pobrania dokładne metryki nazw</span><span class="sxs-lookup"><span data-stu-id="c623b-168">\PhysicalDisk(_Total)\Disk Writes/sec. See the `Get-MetricDefinitions` cmdlet about how to retrieve the exact metric names</span></span> |
| <span data-ttu-id="c623b-169">Operator</span><span class="sxs-lookup"><span data-stu-id="c623b-169">operator</span></span> |<span data-ttu-id="c623b-170">GreaterThan</span><span class="sxs-lookup"><span data-stu-id="c623b-170">GreaterThan</span></span> |
| <span data-ttu-id="c623b-171">Wartość progowa (liczba/s w tym metryki)</span><span class="sxs-lookup"><span data-stu-id="c623b-171">Threshold value (count/sec in for this metric)</span></span> |<span data-ttu-id="c623b-172">1</span><span class="sxs-lookup"><span data-stu-id="c623b-172">1</span></span> |
| <span data-ttu-id="c623b-173">Rozmiar_okna (w formacie hh: mm:)</span><span class="sxs-lookup"><span data-stu-id="c623b-173">WindowSize (hh:mm:ss format)</span></span> |<span data-ttu-id="c623b-174">00:05:00</span><span class="sxs-lookup"><span data-stu-id="c623b-174">00:05:00</span></span> |
| <span data-ttu-id="c623b-175">agregatora (Statystyka metryki, który używa w tym przypadku średnia liczba)</span><span class="sxs-lookup"><span data-stu-id="c623b-175">aggregator (statistic of the metric, which uses Average count, in this case)</span></span> |<span data-ttu-id="c623b-176">Średnia</span><span class="sxs-lookup"><span data-stu-id="c623b-176">Average</span></span> |
| <span data-ttu-id="c623b-177">niestandardowe wiadomości e-mail (tablicy ciągów)</span><span class="sxs-lookup"><span data-stu-id="c623b-177">custom emails (string array)</span></span> |<span data-ttu-id="c623b-178">'foo@example.com','bar@example.com'</span><span class="sxs-lookup"><span data-stu-id="c623b-178">'foo@example.com','bar@example.com'</span></span> |
| <span data-ttu-id="c623b-179">Wyślij wiadomość e-mail do właściciele, współautorzy i czytelnicy</span><span class="sxs-lookup"><span data-stu-id="c623b-179">send email to owners, contributors and readers</span></span> |<span data-ttu-id="c623b-180">-SendToServiceOwners</span><span class="sxs-lookup"><span data-stu-id="c623b-180">-SendToServiceOwners</span></span> |

<span data-ttu-id="c623b-181">Tworzy akcję, poczty E-mail</span><span class="sxs-lookup"><span data-stu-id="c623b-181">Create an Email action</span></span>

```PowerShell
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
```

<span data-ttu-id="c623b-182">Utworzenie elementu Webhook</span><span class="sxs-lookup"><span data-stu-id="c623b-182">Create a Webhook action</span></span>

```PowerShell
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://example.com?token=mytoken
```

<span data-ttu-id="c623b-183">Utwórz regułę alertu na metryki % procesora CPU na klasycznej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="c623b-183">Create the alert rule on the CPU% metric on a classic VM</span></span>

```PowerShell
Add-AzureRmMetricAlertRule -Name vmcpu_gt_1 -Location "East US" -ResourceGroup myrg1 -TargetResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.ClassicCompute/virtualMachines/my_vm1 -MetricName "Percentage CPU" -Operator GreaterThan -Threshold 1 -WindowSize 00:05:00 -TimeAggregationOperator Average -Actions $actionEmail, $actionWebhook -Description "alert on CPU > 1%"
```

<span data-ttu-id="c623b-184">Pobieranie reguły alertu</span><span class="sxs-lookup"><span data-stu-id="c623b-184">Retrieve the alert rule</span></span>

```PowerShell
Get-AzureRmAlertRule -Name vmcpu_gt_1 -ResourceGroup myrg1 -DetailedOutput
```

<span data-ttu-id="c623b-185">Alert polecenia cmdlet Add aktualizuje również reguły, jeśli reguły alertu już istnieje dla danej właściwości.</span><span class="sxs-lookup"><span data-stu-id="c623b-185">The Add alert cmdlet also updates the rule if an alert rule already exists for the given properties.</span></span> <span data-ttu-id="c623b-186">Aby wyłączyć regułę alertu, należy dodać parametr **- DisableRule**.</span><span class="sxs-lookup"><span data-stu-id="c623b-186">To disable an alert rule, include the parameter **-DisableRule**.</span></span>

## <a name="get-a-list-of-available-metrics-for-alerts"></a><span data-ttu-id="c623b-187">Pobierz listę dostępnych metryk dla alertów</span><span class="sxs-lookup"><span data-stu-id="c623b-187">Get a list of available metrics for alerts</span></span>
<span data-ttu-id="c623b-188">Można użyć `Get-AzureRmMetricDefinition` polecenia cmdlet, aby wyświetlić listę wszystkich metryki dla określonego zasobu.</span><span class="sxs-lookup"><span data-stu-id="c623b-188">You can use the `Get-AzureRmMetricDefinition` cmdlet to view the list of all metrics for a specific resource.</span></span>

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id>
```

<span data-ttu-id="c623b-189">Poniższy przykład generuje tabeli o nazwie metryki i jednostki dla niego.</span><span class="sxs-lookup"><span data-stu-id="c623b-189">The following example generates a table with the metric Name and the Unit for it.</span></span>

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

<span data-ttu-id="c623b-190">Pełną listę dostępnych opcji `Get-AzureRmMetricDefinition` znajduje się w temacie [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).</span><span class="sxs-lookup"><span data-stu-id="c623b-190">A full list of available options for `Get-AzureRmMetricDefinition` is available at [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).</span></span>

## <a name="create-and-manage-autoscale-settings"></a><span data-ttu-id="c623b-191">Utwórz i Zarządzaj ustawieniami automatycznego skalowania</span><span class="sxs-lookup"><span data-stu-id="c623b-191">Create and manage AutoScale settings</span></span>
<span data-ttu-id="c623b-192">Zasób, takie jak aplikacja sieci Web, maszyn wirtualnych, usługa w chmurze lub zestawu skalowania maszyn wirtualnych może mieć tylko jedno ustawienie skalowania automatycznego skonfigurowane pod jego kątem.</span><span class="sxs-lookup"><span data-stu-id="c623b-192">A resource, such as a Web app, VM, Cloud Service or Virtual Machine Scale Set can have only one autoscale setting configured for it.</span></span>
<span data-ttu-id="c623b-193">Jednak każdego ustawienia automatycznego skalowania może mieć wiele profilów.</span><span class="sxs-lookup"><span data-stu-id="c623b-193">However, each autoscale setting can have multiple profiles.</span></span> <span data-ttu-id="c623b-194">Na przykład jeden profil na podstawie wydajności skali i drugi dla profilu oparte na harmonogramie.</span><span class="sxs-lookup"><span data-stu-id="c623b-194">For example, one for a performance-based scale profile and a second one for a schedule-based profile.</span></span> <span data-ttu-id="c623b-195">Każdy profil może mieć wiele reguł skonfigurowane na nim.</span><span class="sxs-lookup"><span data-stu-id="c623b-195">Each profile can have multiple rules configured on it.</span></span> <span data-ttu-id="c623b-196">Aby uzyskać więcej informacji na temat skalowania automatycznego, zobacz [sposobu skalowania automatycznego aplikacji](../cloud-services/cloud-services-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="c623b-196">For more information about Autoscale, see [How to Autoscale an Application](../cloud-services/cloud-services-how-to-scale.md).</span></span>

<span data-ttu-id="c623b-197">Poniżej przedstawiono kroki, które będą używane:</span><span class="sxs-lookup"><span data-stu-id="c623b-197">Here are the steps we will use:</span></span>

1. <span data-ttu-id="c623b-198">Tworzenie reguł.</span><span class="sxs-lookup"><span data-stu-id="c623b-198">Create rule(s).</span></span>
2. <span data-ttu-id="c623b-199">Utwórz Profile mapowania reguł, które zostały utworzone wcześniej do profilów.</span><span class="sxs-lookup"><span data-stu-id="c623b-199">Create profile(s) mapping the rules that you created previously to the profiles.</span></span>
3. <span data-ttu-id="c623b-200">Opcjonalnie: Utworzyć powiadomienia na potrzeby skalowania automatycznego konfigurowania właściwości elementu webhook i poczty e-mail.</span><span class="sxs-lookup"><span data-stu-id="c623b-200">Optional: Create notifications for autoscale by configuring webhook and email properties.</span></span>
4. <span data-ttu-id="c623b-201">Utwórz ustawienie skalowania automatycznego o nazwie nad zasobem docelowym przez mapowanie profile i powiadomienia, które zostały utworzone w poprzednich krokach.</span><span class="sxs-lookup"><span data-stu-id="c623b-201">Create an autoscale setting with a name on the target resource by mapping the profiles and notifications that you created in the previous steps.</span></span>

<span data-ttu-id="c623b-202">Poniższe przykłady przedstawiają sposób tworzenia ustawieniu skalowania automatycznego dla zestawu skalowania maszyn wirtualnych systemu operacyjnego Windows za pomocą metryki użycia procesora CPU.</span><span class="sxs-lookup"><span data-stu-id="c623b-202">The following examples show you how you can create an Autoscale setting for a Virtual Machine Scale Set for a Windows operating system based by using the CPU utilization metric.</span></span>

<span data-ttu-id="c623b-203">Najpierw utwórz regułę w celu skalowania w poziomie, o zwiększenie liczby wystąpień.</span><span class="sxs-lookup"><span data-stu-id="c623b-203">First, create a rule to scale-out, with an instance count increase.</span></span>

```PowerShell
$rule1 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 60 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Increase -ScaleActionValue 1
```        

<span data-ttu-id="c623b-204">Następnie utwórz reguły do skali przy, zmniejszenie liczby wystąpień.</span><span class="sxs-lookup"><span data-stu-id="c623b-204">Next, create a rule to scale-in, with an instance count decrease.</span></span>

```PowerShell
$rule2 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 30 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Decrease -ScaleActionValue 1
```

<span data-ttu-id="c623b-205">Następnie utwórz profil dla reguły.</span><span class="sxs-lookup"><span data-stu-id="c623b-205">Then, create a profile for the rules.</span></span>

```PowerShell
$profile1 = New-AzureRmAutoscaleProfile -DefaultCapacity 2 -MaximumCapacity 10 -MinimumCapacity 2 -Rules $rule1,$rule2 -Name "My_Profile"
```

<span data-ttu-id="c623b-206">Utwórz właściwość elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="c623b-206">Create a webhook property.</span></span>

```PowerShell
$webhook_scale = New-AzureRmAutoscaleWebhook -ServiceUri "https://example.com?mytoken=mytokenvalue"
```

<span data-ttu-id="c623b-207">Utwórz właściwość powiadomień w ustawieniu skalowania automatycznego, w tym wiadomości e-mail i utworzonego wcześniej elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="c623b-207">Create the notification property for the autoscale setting, including email and the webhook that you created previously.</span></span>

```PowerShell
$notification1= New-AzureRmAutoscaleNotification -CustomEmails ashwink@microsoft.com -SendEmailToSubscriptionAdministrators SendEmailToSubscriptionCoAdministrators -Webhooks $webhook_scale
```

<span data-ttu-id="c623b-208">Na koniec Utwórz w ustawieniu skalowania automatycznego, aby dodać profil utworzoną wcześniej.</span><span class="sxs-lookup"><span data-stu-id="c623b-208">Finally, create the autoscale setting to add the profile that you created above.</span></span>

```PowerShell
Add-AzureRmAutoscaleSetting -Location "East US" -Name "MyScaleVMSSSetting" -ResourceGroup big2 -TargetResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -AutoscaleProfiles $profile1 -Notifications $notification1
```

<span data-ttu-id="c623b-209">Aby uzyskać więcej informacji o zarządzaniu Ustawienia skalowania automatycznego, zobacz [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).</span><span class="sxs-lookup"><span data-stu-id="c623b-209">For more information about managing Autoscale settings, see [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).</span></span>

## <a name="autoscale-history"></a><span data-ttu-id="c623b-210">Historia skalowania automatycznego</span><span class="sxs-lookup"><span data-stu-id="c623b-210">Autoscale history</span></span>
<span data-ttu-id="c623b-211">Poniższy przykład przedstawia, jak można wyświetlić ostatnie skalowania automatycznego i zdarzenia alertu.</span><span class="sxs-lookup"><span data-stu-id="c623b-211">The following example shows you how you can view recent autoscale and alert events.</span></span> <span data-ttu-id="c623b-212">Umożliwia wyświetlenie historii skalowania automatycznego wyszukiwania dziennika aktywności.</span><span class="sxs-lookup"><span data-stu-id="c623b-212">Use the activity log search to view the autoscale history.</span></span>

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/autoscaleSettings" -DetailedOutput -StartTime 2015-03-01
```

<span data-ttu-id="c623b-213">Można użyć `Get-AzureRmAutoScaleHistory` polecenia cmdlet można pobrać historii automatycznego skalowania.</span><span class="sxs-lookup"><span data-stu-id="c623b-213">You can use the `Get-AzureRmAutoScaleHistory` cmdlet to retrieve AutoScale history.</span></span>

```PowerShell
Get-AzureRmAutoScaleHistory -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/microsoft.insights/autoscalesettings/myScaleSetting -StartTime 2016-03-15 -DetailedOutput
```

<span data-ttu-id="c623b-214">Aby uzyskać więcej informacji, zobacz [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).</span><span class="sxs-lookup"><span data-stu-id="c623b-214">For more information, see [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).</span></span>

### <a name="view-details-for-an-autoscale-setting"></a><span data-ttu-id="c623b-215">Wyświetlanie szczegółów dla ustawienie automatycznego skalowania</span><span class="sxs-lookup"><span data-stu-id="c623b-215">View details for an autoscale setting</span></span>
<span data-ttu-id="c623b-216">Można użyć `Get-Autoscalesetting` polecenia cmdlet, aby pobrać więcej informacji o ustawieniu skalowania automatycznego.</span><span class="sxs-lookup"><span data-stu-id="c623b-216">You can use the `Get-Autoscalesetting` cmdlet to retrieve more information about the autoscale setting.</span></span>

<span data-ttu-id="c623b-217">Poniższy przykład przedstawia szczegółowe informacje o wszystkich ustawień automatycznego skalowania w grupie zasobów "myrg1".</span><span class="sxs-lookup"><span data-stu-id="c623b-217">The following example shows details about all autoscale settings in the resource group 'myrg1'.</span></span>

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -DetailedOutput
```

<span data-ttu-id="c623b-218">Poniższy przykład przedstawia szczegółowe informacje dotyczące wszystkie ustawienia skalowania automatycznego w grupie zasobów "myrg1", a w szczególności w ustawieniu skalowania automatycznego o nazwie "MyScaleVMSSSetting".</span><span class="sxs-lookup"><span data-stu-id="c623b-218">The following example shows details about all autoscale settings in the resource group 'myrg1' and specifically the autoscale setting named 'MyScaleVMSSSetting'.</span></span>

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting -DetailedOutput
```

### <a name="remove-an-autoscale-setting"></a><span data-ttu-id="c623b-219">Usuń ustawienie skalowania automatycznego</span><span class="sxs-lookup"><span data-stu-id="c623b-219">Remove an autoscale setting</span></span>
<span data-ttu-id="c623b-220">Można użyć `Remove-Autoscalesetting` polecenia cmdlet, aby usunąć ustawienia skalowania automatycznego.</span><span class="sxs-lookup"><span data-stu-id="c623b-220">You can use the `Remove-Autoscalesetting` cmdlet to delete an autoscale setting.</span></span>

```PowerShell
Remove-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting
```

## <a name="manage-log-profiles-for-activity-log"></a><span data-ttu-id="c623b-221">Zarządzanie profilami dziennika dla dziennika aktywności</span><span class="sxs-lookup"><span data-stu-id="c623b-221">Manage log profiles for activity log</span></span>
<span data-ttu-id="c623b-222">Można utworzyć *dziennika profilu* i eksportu danych z dziennika aktywności konta magazynu i należy skonfigurować przechowywania danych dla niego.</span><span class="sxs-lookup"><span data-stu-id="c623b-222">You can create a *log profile* and export data from your activity log to a storage account and you can configure data retention for it.</span></span> <span data-ttu-id="c623b-223">Opcjonalnie można również strumienia danych do Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="c623b-223">Optionally, you can also stream the data to your Event Hub.</span></span> <span data-ttu-id="c623b-224">Należy pamiętać, że ta funkcja jest obecnie w wersji zapoznawczej i można tworzyć tylko jeden profil dziennika na subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="c623b-224">Note that this feature is currently in Preview and you can only create one log profile per subscription.</span></span> <span data-ttu-id="c623b-225">Za pomocą następujących poleceń cmdlet i Twojej bieżącej subskrypcji do tworzenia i zarządzania profilami dziennika.</span><span class="sxs-lookup"><span data-stu-id="c623b-225">You can use the following cmdlets with your current subscription to create and manage log profiles.</span></span> <span data-ttu-id="c623b-226">Możesz również określonej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="c623b-226">You can also choose a particular subscription.</span></span> <span data-ttu-id="c623b-227">Mimo że domyślne programu PowerShell do bieżącej subskrypcji, zawsze można zmienić tego za pomocą `Set-AzureRmContext`.</span><span class="sxs-lookup"><span data-stu-id="c623b-227">Although PowerShell defaults to the current subscription, you can always change that using `Set-AzureRmContext`.</span></span> <span data-ttu-id="c623b-228">Można skonfigurować dziennik aktywności na przesyłanie danych do dowolnego konta magazynu lub Centrum zdarzeń, w ramach danej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="c623b-228">You can configure activity log to route data to any storage account or Event Hub within that subscription.</span></span> <span data-ttu-id="c623b-229">Dane są zapisywane jako pliki obiektu blob w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="c623b-229">Data is written as blob files in JSON format.</span></span>

### <a name="get-a-log-profile"></a><span data-ttu-id="c623b-230">Pobierz profil dziennika</span><span class="sxs-lookup"><span data-stu-id="c623b-230">Get a log profile</span></span>
<span data-ttu-id="c623b-231">Aby pobrać profili istniejącego dziennika, należy użyć `Get-AzureRmLogProfile` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c623b-231">To fetch your existing log profiles, use the `Get-AzureRmLogProfile` cmdlet.</span></span>

### <a name="add-a-log-profile-without-data-retention"></a><span data-ttu-id="c623b-232">Dodawanie profilu dziennika bez przechowywania danych</span><span class="sxs-lookup"><span data-stu-id="c623b-232">Add a log profile without data retention</span></span>
```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a><span data-ttu-id="c623b-233">Usuń profil dziennika</span><span class="sxs-lookup"><span data-stu-id="c623b-233">Remove a log profile</span></span>
```PowerShell
Remove-AzureRmLogProfile -name my_log_profile_s1
```

### <a name="add-a-log-profile-with-data-retention"></a><span data-ttu-id="c623b-234">Dodawanie profilu dziennika z przechowywaniem danych</span><span class="sxs-lookup"><span data-stu-id="c623b-234">Add a log profile with data retention</span></span>
<span data-ttu-id="c623b-235">Można określić **- RetentionInDays** właściwości z liczbą dni, jako dodatnią liczbą całkowitą, gdzie są przechowywane dane.</span><span class="sxs-lookup"><span data-stu-id="c623b-235">You can specify the **-RetentionInDays** property with the number of days, as a positive integer, where the data is retained.</span></span>

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

### <a name="add-log-profile-with-retention-and-eventhub"></a><span data-ttu-id="c623b-236">Dodawanie profilu dziennika z przechowywania i EventHub</span><span class="sxs-lookup"><span data-stu-id="c623b-236">Add log profile with retention and EventHub</span></span>
<span data-ttu-id="c623b-237">Oprócz routingu danych do konta magazynu, można również strumienia go do Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="c623b-237">In addition to routing your data to storage account, you can also stream it to an Event Hub.</span></span> <span data-ttu-id="c623b-238">Należy pamiętać, że w tej wersji zapoznawczej i Magazyn konfiguracji konta jest wymagane, ale konfiguracja Centrum zdarzeń jest opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="c623b-238">Note that in this preview release and the storage account configuration is mandatory but Event Hub configuration is optional.</span></span>

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

## <a name="configure-diagnostics-logs"></a><span data-ttu-id="c623b-239">Konfigurowanie dzienników diagnostycznych</span><span class="sxs-lookup"><span data-stu-id="c623b-239">Configure diagnostics logs</span></span>
<span data-ttu-id="c623b-240">Wiele usług platformy Azure zapewniają dodatkowe dzienniki i dane telemetryczne, które może być skonfigurowany tak, aby zapisać danych na koncie magazynu Azure, Wyślij do usługi Event Hubs i/lub wysyłane do obszaru roboczego analizy dzienników OMS.</span><span class="sxs-lookup"><span data-stu-id="c623b-240">Many Azure services provide additional logs and telemetry that can be configured to save data in your Azure Storage account, send to Event Hubs, and/or sent to an OMS Log Analytics workspace.</span></span> <span data-ttu-id="c623b-241">Tę operację można wykonać tylko na poziomie zasobów i Centrum konta lub zdarzenia magazynu powinien znajdować się w tym samym regionie co zasób docelowy, na którym skonfigurowano ustawienie diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="c623b-241">That operation can only be performed at a resource level and the storage account or event hub should be present in the same region as the target resource where the diagnostics setting is configured.</span></span>

### <a name="get-diagnostic-setting"></a><span data-ttu-id="c623b-242">Pobierz ustawienia diagnostyki</span><span class="sxs-lookup"><span data-stu-id="c623b-242">Get diagnostic setting</span></span>
```PowerShell
Get-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp
```

<span data-ttu-id="c623b-243">Wyłącz ustawienie diagnostyczne</span><span class="sxs-lookup"><span data-stu-id="c623b-243">Disable diagnostic setting</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $false
```

<span data-ttu-id="c623b-244">Włącz ustawienie diagnostyczne bez przechowywania</span><span class="sxs-lookup"><span data-stu-id="c623b-244">Enable diagnostic setting without retention</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true
```

<span data-ttu-id="c623b-245">Włącz ustawienie diagnostyczne z przechowywaniem</span><span class="sxs-lookup"><span data-stu-id="c623b-245">Enable diagnostic setting with retention</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

<span data-ttu-id="c623b-246">Włącz ustawienie diagnostyczne z przechowywania dla kategorii określonego dziennika</span><span class="sxs-lookup"><span data-stu-id="c623b-246">Enable diagnostic setting with retention for a specific log category</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/sakteststorage -Categories NetworkSecurityGroupEvent -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

<span data-ttu-id="c623b-247">Włącz ustawienie diagnostyczne dla usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="c623b-247">Enable diagnostic setting for Event Hubs</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Enable $true
```

<span data-ttu-id="c623b-248">Włącz ustawienie diagnostyczne dla OMS</span><span class="sxs-lookup"><span data-stu-id="c623b-248">Enable diagnostic setting for OMS</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -WorkspaceId 76d785fd-d1ce-4f50-8ca3-858fc819ca0f -Enabled $true

```
