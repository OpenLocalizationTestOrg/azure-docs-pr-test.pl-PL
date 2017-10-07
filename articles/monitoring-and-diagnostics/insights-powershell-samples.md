---
title: "aaaAzure próbki szybki start Monitor programu PowerShell. | Microsoft Docs"
description: "Za pomocą programu PowerShell tooaccess Azure Monitor funkcje, takie jak skalowania automatycznego, alertów, elementów webhook i wyszukiwanie Dzienniki aktywności."
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
ms.openlocfilehash: 6eece0b0227e0bbf08225bd330d0601169911f55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitor-powershell-quick-start-samples"></a><span data-ttu-id="09a16-104">Przykładów dla platformy Azure Monitor PowerShell szybki start</span><span class="sxs-lookup"><span data-stu-id="09a16-104">Azure Monitor PowerShell quick start samples</span></span>
<span data-ttu-id="09a16-105">Ten artykuł przedstawia przykładowe toohelp poleceń programu PowerShell możesz uzyskiwać dostęp do funkcji monitorowania Azure.</span><span class="sxs-lookup"><span data-stu-id="09a16-105">This article shows you sample PowerShell commands toohelp you access Azure Monitor features.</span></span> <span data-ttu-id="09a16-106">Azure Monitor umożliwia tooAutoScale usługi w chmurze, maszyn wirtualnych i aplikacji sieci Web i toosend powiadomień o alertach lub na podstawie wartości dane telemetryczne skonfigurowanych adresów URL sieci web wywołania.</span><span class="sxs-lookup"><span data-stu-id="09a16-106">Azure Monitor allows you tooAutoScale Cloud Services, Virtual Machines, and Web Apps and toosend alert notifications or call web URLs based on values of configured telemetry data.</span></span>

> [!NOTE]
> <span data-ttu-id="09a16-107">Azure Monitor jest nową nazwę hello proponowaną "Azure Insights" do 25 września 2016 r.</span><span class="sxs-lookup"><span data-stu-id="09a16-107">Azure Monitor is hello new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="09a16-108">Jednak hello przestrzeni nazw, dlatego hello następujące polecenia nadal zawierać hello "insights".</span><span class="sxs-lookup"><span data-stu-id="09a16-108">However, hello namespaces and thus hello following commands still contain hello "insights".</span></span>
> 
> 

## <a name="set-up-powershell"></a><span data-ttu-id="09a16-109">Konfigurowanie środowiska PowerShell</span><span class="sxs-lookup"><span data-stu-id="09a16-109">Set up PowerShell</span></span>
<span data-ttu-id="09a16-110">Jeśli nie jest jeszcze zdefiniować toorun programu PowerShell na komputerze.</span><span class="sxs-lookup"><span data-stu-id="09a16-110">If you haven't already, set up PowerShell toorun on your computer.</span></span> <span data-ttu-id="09a16-111">Aby uzyskać więcej informacji, zobacz [jak tooInstall i konfigurowanie programu PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="09a16-111">For more information, see [How tooInstall and Configure PowerShell](/powershell/azure/overview).</span></span>

## <a name="examples-in-this-article"></a><span data-ttu-id="09a16-112">Przykłady w tym artykule</span><span class="sxs-lookup"><span data-stu-id="09a16-112">Examples in this article</span></span>
<span data-ttu-id="09a16-113">Przykłady Hello w artykule hello pokazują, jak można użyć poleceń cmdlet Azure monitora.</span><span class="sxs-lookup"><span data-stu-id="09a16-113">hello examples in hello article illustrate how you can use Azure Monitor cmdlets.</span></span> <span data-ttu-id="09a16-114">Można również przejrzeć całą listę poleceń cmdlet programu PowerShell usługi Azure monitora na powitania [poleceń cmdlet Azure monitora (Insights)](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx).</span><span class="sxs-lookup"><span data-stu-id="09a16-114">You can also review hello entire list of Azure Monitor PowerShell cmdlets at [Azure Monitor (Insights) Cmdlets](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx).</span></span>

## <a name="sign-in-and-use-subscriptions"></a><span data-ttu-id="09a16-115">Zaloguj się i korzystać z subskrypcji</span><span class="sxs-lookup"><span data-stu-id="09a16-115">Sign in and use subscriptions</span></span>
<span data-ttu-id="09a16-116">Po pierwsze Zaloguj tooyour subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="09a16-116">First, log in tooyour Azure subscription.</span></span>

```PowerShell
Login-AzureRmAccount
```

<span data-ttu-id="09a16-117">Wymaga to toosign w.</span><span class="sxs-lookup"><span data-stu-id="09a16-117">This requires you toosign in.</span></span> <span data-ttu-id="09a16-118">Gdy to zrobisz, Twoje konto dla identyfikatora dzierżawcy i domyślnego Identyfikatora subskrypcji są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="09a16-118">Once you do, your Account, TenantID and default Subscription ID are displayed.</span></span> <span data-ttu-id="09a16-119">Witaj wszystkie polecenia cmdlet systemu Azure pracy w kontekście hello subskrypcji domyślne.</span><span class="sxs-lookup"><span data-stu-id="09a16-119">All hello Azure cmdlets work in hello context of your default subscription.</span></span> <span data-ttu-id="09a16-120">tooview hello Lista subskrypcji, do których masz dostęp, użyj następującego polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="09a16-120">tooview hello list of subscriptions you have access to, use hello following command.</span></span>

```PowerShell
Get-AzureRmSubscription
```

<span data-ttu-id="09a16-121">toochange pracy kontekstu tooa inną subskrypcję, hello Użyj następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="09a16-121">toochange your working context tooa different subscription, use hello following command.</span></span>

```PowerShell
Set-AzureRmContext -SubscriptionId <subscriptionid>
```


## <a name="retrieve-activity-log-for-a-subscription"></a><span data-ttu-id="09a16-122">Pobrać dziennik aktywności dla subskrypcji</span><span class="sxs-lookup"><span data-stu-id="09a16-122">Retrieve Activity log for a subscription</span></span>
<span data-ttu-id="09a16-123">Użyj hello `Get-AzureRmLog` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="09a16-123">Use hello `Get-AzureRmLog` cmdlet.</span></span>  <span data-ttu-id="09a16-124">Witaj poniżej przedstawiono niektóre typowe przykłady.</span><span class="sxs-lookup"><span data-stu-id="09a16-124">hello following are some common examples.</span></span>

<span data-ttu-id="09a16-125">Pobierz wpisy dziennika z tym toopresent daty/godziny:</span><span class="sxs-lookup"><span data-stu-id="09a16-125">Get log entries from this time/date toopresent:</span></span>

```PowerShell
Get-AzureRmLog -StartTime 2016-03-01T10:30
```

<span data-ttu-id="09a16-126">Pobierz wpisy dziennika z zakresu daty/godziny:</span><span class="sxs-lookup"><span data-stu-id="09a16-126">Get log entries between a time/date range:</span></span>

```PowerShell
Get-AzureRmLog -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

<span data-ttu-id="09a16-127">Pobierz wpisy dziennika z danej grupy zasobów:</span><span class="sxs-lookup"><span data-stu-id="09a16-127">Get log entries from a specific resource group:</span></span>

```PowerShell
Get-AzureRmLog -ResourceGroup 'myrg1'
```

<span data-ttu-id="09a16-128">Wpisy dziennika należy uzyskać od dostawcy zasobów określonego zakresu daty/godziny:</span><span class="sxs-lookup"><span data-stu-id="09a16-128">Get log entries from a specific resource provider between a time/date range:</span></span>

```PowerShell
Get-AzureRmLog -ResourceProvider 'Microsoft.Web' -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

<span data-ttu-id="09a16-129">Pobierz wszystkie wpisy dziennika z określonym obiektem wywołującym:</span><span class="sxs-lookup"><span data-stu-id="09a16-129">Get all log entries with a specific caller:</span></span>

```PowerShell
Get-AzureRmLog -Caller 'myname@company.com'
```

<span data-ttu-id="09a16-130">następujące polecenie pobiera Hello hello ostatnich 1000 zdarzenia z dziennika aktywności hello:</span><span class="sxs-lookup"><span data-stu-id="09a16-130">hello following command retrieves hello last 1000 events from hello activity log:</span></span>

```PowerShell
Get-AzureRmLog -MaxEvents 1000
```

<span data-ttu-id="09a16-131">`Get-AzureRmLog`obsługuje wiele innych parametrów.</span><span class="sxs-lookup"><span data-stu-id="09a16-131">`Get-AzureRmLog` supports many other parameters.</span></span> <span data-ttu-id="09a16-132">Zobacz hello `Get-AzureRmLog` odwołania, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="09a16-132">See hello `Get-AzureRmLog` reference for more information.</span></span>

> [!NOTE]
> <span data-ttu-id="09a16-133">`Get-AzureRmLog`zapewnia tylko 15 dni historii.</span><span class="sxs-lookup"><span data-stu-id="09a16-133">`Get-AzureRmLog` only provides 15 days of history.</span></span> <span data-ttu-id="09a16-134">Przy użyciu hello **- MaxEvents** parametr umożliwia tooquery hello ostatniego N zdarzeń, ponad 15 dni.</span><span class="sxs-lookup"><span data-stu-id="09a16-134">Using hello **-MaxEvents** parameter allows you tooquery hello last N events, beyond 15 days.</span></span> <span data-ttu-id="09a16-135">tooaccess zdarzenia starsze niż 15 dni, użyj hello interfejsu API REST lub zestawu SDK (C# przykład przy użyciu hello zestawu SDK).</span><span class="sxs-lookup"><span data-stu-id="09a16-135">tooaccess events older than 15 days, use hello REST API or SDK (C# sample using hello SDK).</span></span> <span data-ttu-id="09a16-136">Jeśli nie zostanie uwzględniony **StartTime**, a następnie hello wartość domyślna to **EndTime** minus godzinę.</span><span class="sxs-lookup"><span data-stu-id="09a16-136">If you do not include **StartTime**, then hello default value is **EndTime** minus one hour.</span></span> <span data-ttu-id="09a16-137">Jeśli nie zostanie uwzględniony **EndTime**, to wartość domyślna hello jest bieżący czas.</span><span class="sxs-lookup"><span data-stu-id="09a16-137">If you do not include **EndTime**, then hello default value is current time.</span></span> <span data-ttu-id="09a16-138">Wszystkie godziny są w formacie UTC.</span><span class="sxs-lookup"><span data-stu-id="09a16-138">All times are in UTC.</span></span>
> 
> 

## <a name="retrieve-alerts-history"></a><span data-ttu-id="09a16-139">Pobrać historii alertów</span><span class="sxs-lookup"><span data-stu-id="09a16-139">Retrieve alerts history</span></span>
<span data-ttu-id="09a16-140">tooview wszystkich alertów zdarzeń, można zbadać hello dzienników usługi Azure Resource Manager przy użyciu hello następujące przykłady.</span><span class="sxs-lookup"><span data-stu-id="09a16-140">tooview all alert events, you can query hello Azure Resource Manager logs using hello following examples.</span></span>

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/alertRules" -DetailedOutput -StartTime 2015-03-01
```

<span data-ttu-id="09a16-141">reguły tooview hello historii dla określonego alertu, można użyć hello `Get-AzureRmAlertHistory` polecenia cmdlet, przekazując identyfikator zasobu hello hello reguły alertu.</span><span class="sxs-lookup"><span data-stu-id="09a16-141">tooview hello history for a specific alert rule, you can use hello `Get-AzureRmAlertHistory` cmdlet, passing in hello resource ID of hello alert rule.</span></span>

```PowerShell
Get-AzureRmAlertHistory -ResourceId /subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/myalert -StartTime 2016-03-1 -Status Activated
```

<span data-ttu-id="09a16-142">Witaj `Get-AzureRmAlertHistory` polecenie cmdlet obsługuje różne parametry.</span><span class="sxs-lookup"><span data-stu-id="09a16-142">hello `Get-AzureRmAlertHistory` cmdlet supports various parameters.</span></span> <span data-ttu-id="09a16-143">Więcej informacji, zobacz [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).</span><span class="sxs-lookup"><span data-stu-id="09a16-143">More information, see [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).</span></span>

## <a name="retrieve-information-on-alert-rules"></a><span data-ttu-id="09a16-144">Pobieranie informacji na temat reguł alertów</span><span class="sxs-lookup"><span data-stu-id="09a16-144">Retrieve information on alert rules</span></span>
<span data-ttu-id="09a16-145">Wszystkie następujące polecenia hello działają na grupy zasobów o nazwie "montest".</span><span class="sxs-lookup"><span data-stu-id="09a16-145">All of hello following commands act on a Resource Group named "montest".</span></span>

<span data-ttu-id="09a16-146">Wyświetl wszystkie właściwości hello hello reguły alertu:</span><span class="sxs-lookup"><span data-stu-id="09a16-146">View all hello properties of hello alert rule:</span></span>

```PowerShell
Get-AzureRmAlertRule -Name simpletestCPU -ResourceGroup montest -DetailedOutput
```

<span data-ttu-id="09a16-147">Pobieranie wszystkich alertów w grupie zasobów:</span><span class="sxs-lookup"><span data-stu-id="09a16-147">Retrieve all alerts on a resource group:</span></span>

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest
```

<span data-ttu-id="09a16-148">Pobierz wszystkie reguły alertu dla zasobu docelowego.</span><span class="sxs-lookup"><span data-stu-id="09a16-148">Retrieve all alert rules set for a target resource.</span></span> <span data-ttu-id="09a16-149">Na przykład wszystkie reguły alertu ustawione na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="09a16-149">For example, all alert rules set on a VM.</span></span>

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest -TargetResourceId /subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig
```

<span data-ttu-id="09a16-150">`Get-AzureRmAlertRule`obsługuje inne parametry.</span><span class="sxs-lookup"><span data-stu-id="09a16-150">`Get-AzureRmAlertRule` supports other parameters.</span></span> <span data-ttu-id="09a16-151">Zobacz [Get AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="09a16-151">See [Get-AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) for more information.</span></span>

## <a name="create-metric-alerts"></a><span data-ttu-id="09a16-152">Tworzenie metryk alertów</span><span class="sxs-lookup"><span data-stu-id="09a16-152">Create metric alerts</span></span>
<span data-ttu-id="09a16-153">Można użyć hello `Add-AlertRule` toocreate polecenia cmdlet, zaktualizować lub wyłączyć regułę alertu.</span><span class="sxs-lookup"><span data-stu-id="09a16-153">You can use hello `Add-AlertRule` cmdlet toocreate, update or disable an alert rule.</span></span>

<span data-ttu-id="09a16-154">Można utworzyć właściwości poczty e-mail i elementu webhook za pomocą `New-AzureRmAlertRuleEmail` i `New-AzureRmAlertRuleWebhook`odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="09a16-154">You can create email and webhook properties using  `New-AzureRmAlertRuleEmail` and `New-AzureRmAlertRuleWebhook`, respectively.</span></span> <span data-ttu-id="09a16-155">W poleceniu cmdlet reguły alertu hello, przypisz je jako akcje toohello **akcje** właściwości hello reguły alertów.</span><span class="sxs-lookup"><span data-stu-id="09a16-155">In hello Alert rule cmdlet, assign these as actions toohello **Actions** property of hello Alert Rule.</span></span>

<span data-ttu-id="09a16-156">Witaj w poniższej tabeli opisano parametry hello i wartości używane toocreate alert przy użyciu metryki.</span><span class="sxs-lookup"><span data-stu-id="09a16-156">hello following table describes hello parameters and values used toocreate an alert using a metric.</span></span>

| <span data-ttu-id="09a16-157">Parametr</span><span class="sxs-lookup"><span data-stu-id="09a16-157">parameter</span></span> | <span data-ttu-id="09a16-158">wartość</span><span class="sxs-lookup"><span data-stu-id="09a16-158">value</span></span> |
| --- | --- |
| <span data-ttu-id="09a16-159">Nazwa</span><span class="sxs-lookup"><span data-stu-id="09a16-159">Name</span></span> |<span data-ttu-id="09a16-160">simpletestdiskwrite</span><span class="sxs-lookup"><span data-stu-id="09a16-160">simpletestdiskwrite</span></span> |
| <span data-ttu-id="09a16-161">Lokalizacja tę regułę alertów</span><span class="sxs-lookup"><span data-stu-id="09a16-161">Location of this alert rule</span></span> |<span data-ttu-id="09a16-162">Wschodnie stany USA</span><span class="sxs-lookup"><span data-stu-id="09a16-162">East US</span></span> |
| <span data-ttu-id="09a16-163">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="09a16-163">ResourceGroup</span></span> |<span data-ttu-id="09a16-164">montest</span><span class="sxs-lookup"><span data-stu-id="09a16-164">montest</span></span> |
| <span data-ttu-id="09a16-165">Element TargetResourceId</span><span class="sxs-lookup"><span data-stu-id="09a16-165">TargetResourceId</span></span> |<span data-ttu-id="09a16-166">/Subscriptions/S1/resourceGroups/montest/Providers/Microsoft.COMPUTE/virtualMachines/testconfig</span><span class="sxs-lookup"><span data-stu-id="09a16-166">/subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig</span></span> |
| <span data-ttu-id="09a16-167">MetricName hello alertu, który jest tworzony</span><span class="sxs-lookup"><span data-stu-id="09a16-167">MetricName of hello alert that is created</span></span> |<span data-ttu-id="09a16-168">\Disk \PhysicalDisk (_Total) / s. Zobacz hello `Get-MetricDefinitions` polecenia cmdlet dotyczące sposobu tooretrieve hello dokładnej nazwy metryki</span><span class="sxs-lookup"><span data-stu-id="09a16-168">\PhysicalDisk(_Total)\Disk Writes/sec. See hello `Get-MetricDefinitions` cmdlet about how tooretrieve hello exact metric names</span></span> |
| <span data-ttu-id="09a16-169">Operator</span><span class="sxs-lookup"><span data-stu-id="09a16-169">operator</span></span> |<span data-ttu-id="09a16-170">GreaterThan</span><span class="sxs-lookup"><span data-stu-id="09a16-170">GreaterThan</span></span> |
| <span data-ttu-id="09a16-171">Wartość progowa (liczba/s w tym metryki)</span><span class="sxs-lookup"><span data-stu-id="09a16-171">Threshold value (count/sec in for this metric)</span></span> |<span data-ttu-id="09a16-172">1</span><span class="sxs-lookup"><span data-stu-id="09a16-172">1</span></span> |
| <span data-ttu-id="09a16-173">Rozmiar_okna (w formacie hh: mm:)</span><span class="sxs-lookup"><span data-stu-id="09a16-173">WindowSize (hh:mm:ss format)</span></span> |<span data-ttu-id="09a16-174">00:05:00</span><span class="sxs-lookup"><span data-stu-id="09a16-174">00:05:00</span></span> |
| <span data-ttu-id="09a16-175">agregatora (Statystyka hello metryki, który używa w tym przypadku średnia liczba)</span><span class="sxs-lookup"><span data-stu-id="09a16-175">aggregator (statistic of hello metric, which uses Average count, in this case)</span></span> |<span data-ttu-id="09a16-176">Średnia</span><span class="sxs-lookup"><span data-stu-id="09a16-176">Average</span></span> |
| <span data-ttu-id="09a16-177">niestandardowe wiadomości e-mail (tablicy ciągów)</span><span class="sxs-lookup"><span data-stu-id="09a16-177">custom emails (string array)</span></span> |<span data-ttu-id="09a16-178">'foo@example.com','bar@example.com'</span><span class="sxs-lookup"><span data-stu-id="09a16-178">'foo@example.com','bar@example.com'</span></span> |
| <span data-ttu-id="09a16-179">Wyślij wiadomość e-mail tooowners, współautorzy i czytelnicy</span><span class="sxs-lookup"><span data-stu-id="09a16-179">send email tooowners, contributors and readers</span></span> |<span data-ttu-id="09a16-180">-SendToServiceOwners</span><span class="sxs-lookup"><span data-stu-id="09a16-180">-SendToServiceOwners</span></span> |

<span data-ttu-id="09a16-181">Tworzy akcję, poczty E-mail</span><span class="sxs-lookup"><span data-stu-id="09a16-181">Create an Email action</span></span>

```PowerShell
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
```

<span data-ttu-id="09a16-182">Utworzenie elementu Webhook</span><span class="sxs-lookup"><span data-stu-id="09a16-182">Create a Webhook action</span></span>

```PowerShell
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://example.com?token=mytoken
```

<span data-ttu-id="09a16-183">Utwórz regułę alertu hello na powitania Procesora % metryki klasyczne maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="09a16-183">Create hello alert rule on hello CPU% metric on a classic VM</span></span>

```PowerShell
Add-AzureRmMetricAlertRule -Name vmcpu_gt_1 -Location "East US" -ResourceGroup myrg1 -TargetResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.ClassicCompute/virtualMachines/my_vm1 -MetricName "Percentage CPU" -Operator GreaterThan -Threshold 1 -WindowSize 00:05:00 -TimeAggregationOperator Average -Actions $actionEmail, $actionWebhook -Description "alert on CPU > 1%"
```

<span data-ttu-id="09a16-184">Pobrać hello reguły alertu</span><span class="sxs-lookup"><span data-stu-id="09a16-184">Retrieve hello alert rule</span></span>

```PowerShell
Get-AzureRmAlertRule -Name vmcpu_gt_1 -ResourceGroup myrg1 -DetailedOutput
```

<span data-ttu-id="09a16-185">alertu polecenia cmdlet Add Hello aktualizuje również hello reguły, jeśli reguły alertu już istnieje dla hello podanej właściwości.</span><span class="sxs-lookup"><span data-stu-id="09a16-185">hello Add alert cmdlet also updates hello rule if an alert rule already exists for hello given properties.</span></span> <span data-ttu-id="09a16-186">Parametr hello uwzględniony toodisable regułę alertu **- DisableRule**.</span><span class="sxs-lookup"><span data-stu-id="09a16-186">toodisable an alert rule, include hello parameter **-DisableRule**.</span></span>

## <a name="get-a-list-of-available-metrics-for-alerts"></a><span data-ttu-id="09a16-187">Pobierz listę dostępnych metryk dla alertów</span><span class="sxs-lookup"><span data-stu-id="09a16-187">Get a list of available metrics for alerts</span></span>
<span data-ttu-id="09a16-188">Można użyć hello `Get-AzureRmMetricDefinition` polecenia cmdlet tooview hello lista wszystkie metryki dla określonego zasobu.</span><span class="sxs-lookup"><span data-stu-id="09a16-188">You can use hello `Get-AzureRmMetricDefinition` cmdlet tooview hello list of all metrics for a specific resource.</span></span>

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id>
```

<span data-ttu-id="09a16-189">Witaj poniższy przykład generuje tabeli z metryką hello nazwy i hello jednostki dla niego.</span><span class="sxs-lookup"><span data-stu-id="09a16-189">hello following example generates a table with hello metric Name and hello Unit for it.</span></span>

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

<span data-ttu-id="09a16-190">Pełną listę dostępnych opcji `Get-AzureRmMetricDefinition` znajduje się w temacie [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).</span><span class="sxs-lookup"><span data-stu-id="09a16-190">A full list of available options for `Get-AzureRmMetricDefinition` is available at [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).</span></span>

## <a name="create-and-manage-autoscale-settings"></a><span data-ttu-id="09a16-191">Utwórz i Zarządzaj ustawieniami automatycznego skalowania</span><span class="sxs-lookup"><span data-stu-id="09a16-191">Create and manage AutoScale settings</span></span>
<span data-ttu-id="09a16-192">Zasób, takie jak aplikacja sieci Web, maszyn wirtualnych, usługa w chmurze lub zestawu skalowania maszyn wirtualnych może mieć tylko jedno ustawienie skalowania automatycznego skonfigurowane pod jego kątem.</span><span class="sxs-lookup"><span data-stu-id="09a16-192">A resource, such as a Web app, VM, Cloud Service or Virtual Machine Scale Set can have only one autoscale setting configured for it.</span></span>
<span data-ttu-id="09a16-193">Jednak każdego ustawienia automatycznego skalowania może mieć wiele profilów.</span><span class="sxs-lookup"><span data-stu-id="09a16-193">However, each autoscale setting can have multiple profiles.</span></span> <span data-ttu-id="09a16-194">Na przykład jeden profil na podstawie wydajności skali i drugi dla profilu oparte na harmonogramie.</span><span class="sxs-lookup"><span data-stu-id="09a16-194">For example, one for a performance-based scale profile and a second one for a schedule-based profile.</span></span> <span data-ttu-id="09a16-195">Każdy profil może mieć wiele reguł skonfigurowane na nim.</span><span class="sxs-lookup"><span data-stu-id="09a16-195">Each profile can have multiple rules configured on it.</span></span> <span data-ttu-id="09a16-196">Aby uzyskać więcej informacji na temat skalowania automatycznego, zobacz [jak tooAutoscale aplikacji](../cloud-services/cloud-services-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="09a16-196">For more information about Autoscale, see [How tooAutoscale an Application](../cloud-services/cloud-services-how-to-scale.md).</span></span>

<span data-ttu-id="09a16-197">Poniżej przedstawiono kroki hello, które będą używane:</span><span class="sxs-lookup"><span data-stu-id="09a16-197">Here are hello steps we will use:</span></span>

1. <span data-ttu-id="09a16-198">Tworzenie reguł.</span><span class="sxs-lookup"><span data-stu-id="09a16-198">Create rule(s).</span></span>
2. <span data-ttu-id="09a16-199">Tworzenie profilów reguły mapowania hello utworzony wcześniej toohello profilów.</span><span class="sxs-lookup"><span data-stu-id="09a16-199">Create profile(s) mapping hello rules that you created previously toohello profiles.</span></span>
3. <span data-ttu-id="09a16-200">Opcjonalnie: Utworzyć powiadomienia na potrzeby skalowania automatycznego konfigurowania właściwości elementu webhook i poczty e-mail.</span><span class="sxs-lookup"><span data-stu-id="09a16-200">Optional: Create notifications for autoscale by configuring webhook and email properties.</span></span>
4. <span data-ttu-id="09a16-201">Utwórz ustawienie skalowania automatycznego o nazwie na zasób docelowy hello przez mapowanie hello profilów i powiadomień, które zostały utworzone w poprzednich krokach hello.</span><span class="sxs-lookup"><span data-stu-id="09a16-201">Create an autoscale setting with a name on hello target resource by mapping hello profiles and notifications that you created in hello previous steps.</span></span>

<span data-ttu-id="09a16-202">Hello poniższych przykładach przedstawiono tworzenia ustawieniu skalowania automatycznego dla zestawu skalowania maszyn wirtualnych systemu operacyjnego Windows za pomocą metryki użycia hello procesora CPU.</span><span class="sxs-lookup"><span data-stu-id="09a16-202">hello following examples show you how you can create an Autoscale setting for a Virtual Machine Scale Set for a Windows operating system based by using hello CPU utilization metric.</span></span>

<span data-ttu-id="09a16-203">Najpierw należy utworzyć regułę tooscale-out, o zwiększenie liczby wystąpień.</span><span class="sxs-lookup"><span data-stu-id="09a16-203">First, create a rule tooscale-out, with an instance count increase.</span></span>

```PowerShell
$rule1 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 60 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Increase -ScaleActionValue 1
```        

<span data-ttu-id="09a16-204">Następnie należy utworzyć regułę tooscale w, z zmniejszenie liczby wystąpień.</span><span class="sxs-lookup"><span data-stu-id="09a16-204">Next, create a rule tooscale-in, with an instance count decrease.</span></span>

```PowerShell
$rule2 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 30 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Decrease -ScaleActionValue 1
```

<span data-ttu-id="09a16-205">Następnie utwórz profil dla hello reguły.</span><span class="sxs-lookup"><span data-stu-id="09a16-205">Then, create a profile for hello rules.</span></span>

```PowerShell
$profile1 = New-AzureRmAutoscaleProfile -DefaultCapacity 2 -MaximumCapacity 10 -MinimumCapacity 2 -Rules $rule1,$rule2 -Name "My_Profile"
```

<span data-ttu-id="09a16-206">Utwórz właściwość elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="09a16-206">Create a webhook property.</span></span>

```PowerShell
$webhook_scale = New-AzureRmAutoscaleWebhook -ServiceUri "https://example.com?mytoken=mytokenvalue"
```

<span data-ttu-id="09a16-207">Utwórz właściwość powiadomień hello Ustawienia skalowania automatycznego hello, w tym wiadomości e-mail i hello webhook utworzonego wcześniej.</span><span class="sxs-lookup"><span data-stu-id="09a16-207">Create hello notification property for hello autoscale setting, including email and hello webhook that you created previously.</span></span>

```PowerShell
$notification1= New-AzureRmAutoscaleNotification -CustomEmails ashwink@microsoft.com -SendEmailToSubscriptionAdministrators SendEmailToSubscriptionCoAdministrators -Webhooks $webhook_scale
```

<span data-ttu-id="09a16-208">Na koniec Utwórz hello skalowania automatycznego ustawienie tooadd hello profil utworzone powyżej.</span><span class="sxs-lookup"><span data-stu-id="09a16-208">Finally, create hello autoscale setting tooadd hello profile that you created above.</span></span>

```PowerShell
Add-AzureRmAutoscaleSetting -Location "East US" -Name "MyScaleVMSSSetting" -ResourceGroup big2 -TargetResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -AutoscaleProfiles $profile1 -Notifications $notification1
```

<span data-ttu-id="09a16-209">Aby uzyskać więcej informacji o zarządzaniu Ustawienia skalowania automatycznego, zobacz [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).</span><span class="sxs-lookup"><span data-stu-id="09a16-209">For more information about managing Autoscale settings, see [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).</span></span>

## <a name="autoscale-history"></a><span data-ttu-id="09a16-210">Historia skalowania automatycznego</span><span class="sxs-lookup"><span data-stu-id="09a16-210">Autoscale history</span></span>
<span data-ttu-id="09a16-211">Witaj poniższym przykładzie pokazano, jak można wyświetlić ostatnie zdarzenia skalowania automatycznego i alertów.</span><span class="sxs-lookup"><span data-stu-id="09a16-211">hello following example shows you how you can view recent autoscale and alert events.</span></span> <span data-ttu-id="09a16-212">Za pomocą hello działania dziennik wyszukiwania tooview hello skalowania automatycznego historii.</span><span class="sxs-lookup"><span data-stu-id="09a16-212">Use hello activity log search tooview hello autoscale history.</span></span>

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/autoscaleSettings" -DetailedOutput -StartTime 2015-03-01
```

<span data-ttu-id="09a16-213">Można użyć hello `Get-AzureRmAutoScaleHistory` tooretrieve polecenia cmdlet historii automatycznego skalowania.</span><span class="sxs-lookup"><span data-stu-id="09a16-213">You can use hello `Get-AzureRmAutoScaleHistory` cmdlet tooretrieve AutoScale history.</span></span>

```PowerShell
Get-AzureRmAutoScaleHistory -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/microsoft.insights/autoscalesettings/myScaleSetting -StartTime 2016-03-15 -DetailedOutput
```

<span data-ttu-id="09a16-214">Aby uzyskać więcej informacji, zobacz [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).</span><span class="sxs-lookup"><span data-stu-id="09a16-214">For more information, see [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).</span></span>

### <a name="view-details-for-an-autoscale-setting"></a><span data-ttu-id="09a16-215">Wyświetlanie szczegółów dla ustawienie automatycznego skalowania</span><span class="sxs-lookup"><span data-stu-id="09a16-215">View details for an autoscale setting</span></span>
<span data-ttu-id="09a16-216">Można użyć hello `Get-Autoscalesetting` tooretrieve polecenia cmdlet więcej informacji o ustawieniu skalowania automatycznego hello.</span><span class="sxs-lookup"><span data-stu-id="09a16-216">You can use hello `Get-Autoscalesetting` cmdlet tooretrieve more information about hello autoscale setting.</span></span>

<span data-ttu-id="09a16-217">Witaj poniższy przykład przedstawia szczegółowe informacje o wszystkich ustawień automatycznego skalowania w hello grupy zasobów "myrg1".</span><span class="sxs-lookup"><span data-stu-id="09a16-217">hello following example shows details about all autoscale settings in hello resource group 'myrg1'.</span></span>

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -DetailedOutput
```

<span data-ttu-id="09a16-218">Witaj poniższy przykład przedstawia szczegółowe informacje dotyczące wszystkich ustawień automatycznego skalowania w hello grupy zasobów "myrg1" i w szczególności hello ustawieniu skalowania automatycznego o nazwie "MyScaleVMSSSetting".</span><span class="sxs-lookup"><span data-stu-id="09a16-218">hello following example shows details about all autoscale settings in hello resource group 'myrg1' and specifically hello autoscale setting named 'MyScaleVMSSSetting'.</span></span>

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting -DetailedOutput
```

### <a name="remove-an-autoscale-setting"></a><span data-ttu-id="09a16-219">Usuń ustawienie skalowania automatycznego</span><span class="sxs-lookup"><span data-stu-id="09a16-219">Remove an autoscale setting</span></span>
<span data-ttu-id="09a16-220">Można użyć hello `Remove-Autoscalesetting` toodelete polecenia cmdlet ustawieniu skalowania automatycznego.</span><span class="sxs-lookup"><span data-stu-id="09a16-220">You can use hello `Remove-Autoscalesetting` cmdlet toodelete an autoscale setting.</span></span>

```PowerShell
Remove-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting
```

## <a name="manage-log-profiles-for-activity-log"></a><span data-ttu-id="09a16-221">Zarządzanie profilami dziennika dla dziennika aktywności</span><span class="sxs-lookup"><span data-stu-id="09a16-221">Manage log profiles for activity log</span></span>
<span data-ttu-id="09a16-222">Można utworzyć *dziennika profilu* i eksportowanie danych z konta magazynu tooa dziennika aktywności i można skonfigurować przechowywania danych dla niego.</span><span class="sxs-lookup"><span data-stu-id="09a16-222">You can create a *log profile* and export data from your activity log tooa storage account and you can configure data retention for it.</span></span> <span data-ttu-id="09a16-223">Opcjonalnie można również strumienia tooyour danych hello Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="09a16-223">Optionally, you can also stream hello data tooyour Event Hub.</span></span> <span data-ttu-id="09a16-224">Należy pamiętać, że ta funkcja jest obecnie w wersji zapoznawczej i można tworzyć tylko jeden profil dziennika na subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="09a16-224">Note that this feature is currently in Preview and you can only create one log profile per subscription.</span></span> <span data-ttu-id="09a16-225">Można użyć następującego polecenia cmdlet z Twojej bieżącej subskrypcji toocreate hello i Zarządzaj profilami dziennika.</span><span class="sxs-lookup"><span data-stu-id="09a16-225">You can use hello following cmdlets with your current subscription toocreate and manage log profiles.</span></span> <span data-ttu-id="09a16-226">Możesz również określonej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="09a16-226">You can also choose a particular subscription.</span></span> <span data-ttu-id="09a16-227">Mimo że PowerShell domyślne toohello bieżącej subskrypcji, zawsze można zmienić tego za pomocą `Set-AzureRmContext`.</span><span class="sxs-lookup"><span data-stu-id="09a16-227">Although PowerShell defaults toohello current subscription, you can always change that using `Set-AzureRmContext`.</span></span> <span data-ttu-id="09a16-228">Konto magazynu tooany danych tooroute dziennik aktywności lub Centrum zdarzeń można skonfigurować w ramach danej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="09a16-228">You can configure activity log tooroute data tooany storage account or Event Hub within that subscription.</span></span> <span data-ttu-id="09a16-229">Dane są zapisywane jako pliki obiektu blob w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="09a16-229">Data is written as blob files in JSON format.</span></span>

### <a name="get-a-log-profile"></a><span data-ttu-id="09a16-230">Pobierz profil dziennika</span><span class="sxs-lookup"><span data-stu-id="09a16-230">Get a log profile</span></span>
<span data-ttu-id="09a16-231">toofetch istniejące profile dziennika, użyj hello `Get-AzureRmLogProfile` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="09a16-231">toofetch your existing log profiles, use hello `Get-AzureRmLogProfile` cmdlet.</span></span>

### <a name="add-a-log-profile-without-data-retention"></a><span data-ttu-id="09a16-232">Dodawanie profilu dziennika bez przechowywania danych</span><span class="sxs-lookup"><span data-stu-id="09a16-232">Add a log profile without data retention</span></span>
```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a><span data-ttu-id="09a16-233">Usuń profil dziennika</span><span class="sxs-lookup"><span data-stu-id="09a16-233">Remove a log profile</span></span>
```PowerShell
Remove-AzureRmLogProfile -name my_log_profile_s1
```

### <a name="add-a-log-profile-with-data-retention"></a><span data-ttu-id="09a16-234">Dodawanie profilu dziennika z przechowywaniem danych</span><span class="sxs-lookup"><span data-stu-id="09a16-234">Add a log profile with data retention</span></span>
<span data-ttu-id="09a16-235">Można określić hello **- RetentionInDays** właściwość o hello liczbę dni, jako dodatnią liczbą całkowitą, gdzie są przechowywane dane hello.</span><span class="sxs-lookup"><span data-stu-id="09a16-235">You can specify hello **-RetentionInDays** property with hello number of days, as a positive integer, where hello data is retained.</span></span>

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

### <a name="add-log-profile-with-retention-and-eventhub"></a><span data-ttu-id="09a16-236">Dodawanie profilu dziennika z przechowywania i EventHub</span><span class="sxs-lookup"><span data-stu-id="09a16-236">Add log profile with retention and EventHub</span></span>
<span data-ttu-id="09a16-237">W dodatku toorouting Twojego konta toostorage danych, można również przesyłania strumieniowego go tooan Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="09a16-237">In addition toorouting your data toostorage account, you can also stream it tooan Event Hub.</span></span> <span data-ttu-id="09a16-238">Należy pamiętać, że w tej wersji zapoznawczej wersji i hello konfiguracji konta magazynu jest wymagane, ale konfiguracja Centrum zdarzeń jest opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="09a16-238">Note that in this preview release and hello storage account configuration is mandatory but Event Hub configuration is optional.</span></span>

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

## <a name="configure-diagnostics-logs"></a><span data-ttu-id="09a16-239">Konfigurowanie dzienników diagnostycznych</span><span class="sxs-lookup"><span data-stu-id="09a16-239">Configure diagnostics logs</span></span>
<span data-ttu-id="09a16-240">Wiele usług platformy Azure zapewniają dodatkowe dzienniki i dane telemetryczne, które mogą być skonfigurowane toosave danych na koncie magazynu Azure wysyłania tooEvent koncentratorów i/lub wysyłane obszaru roboczego analizy dzienników OMS tooan.</span><span class="sxs-lookup"><span data-stu-id="09a16-240">Many Azure services provide additional logs and telemetry that can be configured toosave data in your Azure Storage account, send tooEvent Hubs, and/or sent tooan OMS Log Analytics workspace.</span></span> <span data-ttu-id="09a16-241">Tę operację można wykonać tylko na poziomie zasobów i hello magazynu konta lub zdarzenia koncentratora powinny znajdować się w hello tym samym regionie co zasób docelowy hello konfigurowana hello ustawienia diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="09a16-241">That operation can only be performed at a resource level and hello storage account or event hub should be present in hello same region as hello target resource where hello diagnostics setting is configured.</span></span>

### <a name="get-diagnostic-setting"></a><span data-ttu-id="09a16-242">Pobierz ustawienia diagnostyki</span><span class="sxs-lookup"><span data-stu-id="09a16-242">Get diagnostic setting</span></span>
```PowerShell
Get-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp
```

<span data-ttu-id="09a16-243">Wyłącz ustawienie diagnostyczne</span><span class="sxs-lookup"><span data-stu-id="09a16-243">Disable diagnostic setting</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $false
```

<span data-ttu-id="09a16-244">Włącz ustawienie diagnostyczne bez przechowywania</span><span class="sxs-lookup"><span data-stu-id="09a16-244">Enable diagnostic setting without retention</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true
```

<span data-ttu-id="09a16-245">Włącz ustawienie diagnostyczne z przechowywaniem</span><span class="sxs-lookup"><span data-stu-id="09a16-245">Enable diagnostic setting with retention</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

<span data-ttu-id="09a16-246">Włącz ustawienie diagnostyczne z przechowywania dla kategorii określonego dziennika</span><span class="sxs-lookup"><span data-stu-id="09a16-246">Enable diagnostic setting with retention for a specific log category</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/sakteststorage -Categories NetworkSecurityGroupEvent -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

<span data-ttu-id="09a16-247">Włącz ustawienie diagnostyczne dla usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="09a16-247">Enable diagnostic setting for Event Hubs</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Enable $true
```

<span data-ttu-id="09a16-248">Włącz ustawienie diagnostyczne dla OMS</span><span class="sxs-lookup"><span data-stu-id="09a16-248">Enable diagnostic setting for OMS</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -WorkspaceId 76d785fd-d1ce-4f50-8ca3-858fc819ca0f -Enabled $true

```
