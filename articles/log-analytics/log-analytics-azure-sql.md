---
title: "aaaAzure rozwiązania analizy SQL w Log Analytics | Dokumentacja firmy Microsoft"
description: "Hello rozwiązania analizy SQL Azure ułatwia zarządzanie bazami danych Azure SQL."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: b2712749-1ded-40c4-b211-abc51cc65171
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: banders
ms.openlocfilehash: fe228bb3cb3f9d578a84707c3917f02fbeb8a627
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-sql-database-using-azure-sql-analytics-preview-in-log-analytics"></a><span data-ttu-id="4a2fe-103">Monitorowanie bazy danych SQL Azure przy użyciu analiza SQL Azure (wersja zapoznawcza) w analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="4a2fe-103">Monitor Azure SQL Database using Azure SQL Analytics (Preview) in Log Analytics</span></span>

![Symbol SQL Analytics Azure](./media/log-analytics-azure-sql/azure-sql-symbol.png)

<span data-ttu-id="4a2fe-105">Witaj rozwiązania analizy SQL Azure w Azure Log Analytics zbiera i wizualizuje ważne metryki wydajności usługi SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-105">hello Azure SQL Analytics solution in Azure Log Analytics collects and visualizes important SQL Azure performance metrics.</span></span> <span data-ttu-id="4a2fe-106">Za pomocą hello metryki, które należy zebrać z rozwiązaniem hello, można utworzyć niestandardowe reguły monitorowania i alertów.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-106">By using hello metrics that you collect with hello solution, you can create custom monitoring rules and alerts.</span></span> <span data-ttu-id="4a2fe-107">Można monitorować bazy danych SQL Azure i metryki elastycznej puli w wielu subskrypcji platformy Azure i elastyczne pule i ich wizualizacji.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-107">And, you can monitor Azure SQL Database and elastic pool metrics across multiple Azure subscriptions and elastic pools and visualize them.</span></span> <span data-ttu-id="4a2fe-108">rozwiązanie Hello ułatwia również problemy tooidentify w każdej warstwie stosu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-108">hello solution also helps you tooidentify issues at each layer of your application stack.</span></span>  <span data-ttu-id="4a2fe-109">Używa [diagnostyki Azure metryki](log-analytics-azure-storage.md) wraz z analizy dzienników widoków toopresent dane dotyczące wszystkich baz danych Azure SQL i pul elastycznych w jednym obszarze roboczym analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-109">It uses [Azure Diagnostic metrics](log-analytics-azure-storage.md) together with Log Analytics views toopresent data about all your Azure SQL databases and elastic pools in a single Log Analytics workspace.</span></span>

<span data-ttu-id="4a2fe-110">Obecnie to rozwiązanie w wersji zapoznawczej obsługuje too150, 000 baz danych SQL Azure i 5000 SQL pule elastyczne według obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-110">Currently, this preview solution supports up too150,000 Azure SQL Databases and 5,000 SQL Elastic Pools per workspace.</span></span>

<span data-ttu-id="4a2fe-111">Witaj rozwiązania analizy SQL Azure, takich jak inne dostępne dla analizy dzienników pomaga monitorować i otrzymywanie powiadomień o kondycji hello zasobów platformy Azure — w takim przypadku baza danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-111">hello Azure SQL Analytics solution, like others available for Log Analytics, helps you monitor and receive notifications about hello health of your Azure resources—in this case, Azure SQL Database.</span></span> <span data-ttu-id="4a2fe-112">Baza danych SQL Azure Microsoft to usługa skalowalne relacyjnej bazy danych, która zapewnia znanych tooapplications możliwości programu SQL Server typu w hello chmury Azure.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-112">Microsoft Azure SQL Database is a scalable relational database service that provides familiar SQL-Server-like capabilities tooapplications running in hello Azure cloud.</span></span> <span data-ttu-id="4a2fe-113">Log Analytics pomaga toocollect skorelowania i wizualizacji danych strukturalnych i bez struktury.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-113">Log Analytics helps you toocollect, correlate, and visualize structured and unstructured data.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="4a2fe-114">Połączone źródła</span><span class="sxs-lookup"><span data-stu-id="4a2fe-114">Connected sources</span></span>

<span data-ttu-id="4a2fe-115">Witaj rozwiązania analizy SQL Azure nie używa agentów tooconnect toohello usługi analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-115">hello Azure SQL Analytics solution doesn't use agents tooconnect toohello Log Analytics service.</span></span>

<span data-ttu-id="4a2fe-116">Witaj w poniższej tabeli opisano hello połączone źródeł, które są obsługiwane przez to rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-116">hello following table describes hello connected sources that are supported by this solution.</span></span>

| <span data-ttu-id="4a2fe-117">Połączone źródło</span><span class="sxs-lookup"><span data-stu-id="4a2fe-117">Connected Source</span></span> | <span data-ttu-id="4a2fe-118">Pomoc techniczna</span><span class="sxs-lookup"><span data-stu-id="4a2fe-118">Support</span></span> | <span data-ttu-id="4a2fe-119">Opis</span><span class="sxs-lookup"><span data-stu-id="4a2fe-119">Description</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="4a2fe-120">Agenci dla systemu Windows</span><span class="sxs-lookup"><span data-stu-id="4a2fe-120">Windows agents</span></span>](log-analytics-windows-agents.md) | <span data-ttu-id="4a2fe-121">Nie</span><span class="sxs-lookup"><span data-stu-id="4a2fe-121">No</span></span> | <span data-ttu-id="4a2fe-122">Bezpośrednie agentów systemu Windows nie są używane przez rozwiązanie hello.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-122">Direct Windows agents are not used by hello solution.</span></span> |
| [<span data-ttu-id="4a2fe-123">Agenci dla systemu Linux</span><span class="sxs-lookup"><span data-stu-id="4a2fe-123">Linux agents</span></span>](log-analytics-linux-agents.md) | <span data-ttu-id="4a2fe-124">Nie</span><span class="sxs-lookup"><span data-stu-id="4a2fe-124">No</span></span> | <span data-ttu-id="4a2fe-125">Bezpośrednie agentów systemu Linux nie są używane przez rozwiązanie hello.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-125">Direct Linux agents are not used by hello solution.</span></span> |
| [<span data-ttu-id="4a2fe-126">Grupa zarządzania programu SCOM</span><span class="sxs-lookup"><span data-stu-id="4a2fe-126">SCOM management group</span></span>](log-analytics-om-agents.md) | <span data-ttu-id="4a2fe-127">Nie</span><span class="sxs-lookup"><span data-stu-id="4a2fe-127">No</span></span> | <span data-ttu-id="4a2fe-128">Połączenie bezpośrednie z tooLog agenta programu SCOM hello Analytics nie jest używany przez rozwiązanie hello.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-128">A direct connection from hello SCOM agent tooLog Analytics is not used by hello solution.</span></span> |
| [<span data-ttu-id="4a2fe-129">Konto usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="4a2fe-129">Azure storage account</span></span>](log-analytics-azure-storage.md) | <span data-ttu-id="4a2fe-130">Nie</span><span class="sxs-lookup"><span data-stu-id="4a2fe-130">No</span></span> | <span data-ttu-id="4a2fe-131">Analizy dzienników nie odczytuje danych hello z konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-131">Log Analytics does not read hello data from a storage account.</span></span> |
| [<span data-ttu-id="4a2fe-132">Diagnostyka Azure</span><span class="sxs-lookup"><span data-stu-id="4a2fe-132">Azure diagnostics</span></span>](log-analytics-azure-storage.md) | <span data-ttu-id="4a2fe-133">Tak</span><span class="sxs-lookup"><span data-stu-id="4a2fe-133">Yes</span></span> | <span data-ttu-id="4a2fe-134">Azure metryki dane są wysyłane tooLog Analytics bezpośrednio przez platformę Azure.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-134">Azure metric data is sent tooLog Analytics directly by Azure.</span></span> |

## <a name="prerequisites"></a><span data-ttu-id="4a2fe-135">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4a2fe-135">Prerequisites</span></span>

- <span data-ttu-id="4a2fe-136">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-136">An Azure Subscription.</span></span> <span data-ttu-id="4a2fe-137">Jeśli nie masz, możesz utworzyć jedną dla [wolnego](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="4a2fe-137">If you don't have one, you can create one for [free](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="4a2fe-138">Obszar roboczy analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-138">A Log Analytics workspace.</span></span> <span data-ttu-id="4a2fe-139">Można użyć istniejącego, lub możesz [Utwórz nową](log-analytics-get-started.md) przed rozpoczęciem korzystania z tego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-139">You can use an existing one, or you can [create a new one](log-analytics-get-started.md) before you start using this solution.</span></span>
- <span data-ttu-id="4a2fe-140">Włącz diagnostyki Azure dla baz danych Azure SQL i pule elastyczne i [je skonfigurować toosend ich tooLog danych Analytics](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span><span class="sxs-lookup"><span data-stu-id="4a2fe-140">Enable Azure Diagnostics for your Azure SQL databases and elastic pools and [configure them toosend their data tooLog Analytics](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span></span>

## <a name="configuration"></a><span data-ttu-id="4a2fe-141">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="4a2fe-141">Configuration</span></span>

<span data-ttu-id="4a2fe-142">Wykonaj następujące kroki tooadd hello analiza SQL Azure rozwiązania tooyour roboczym hello.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-142">Perform hello following steps tooadd hello Azure SQL Analytics solution tooyour workspace.</span></span>

1. <span data-ttu-id="4a2fe-143">Dodaj obszar roboczy tooyour rozwiązania analizy SQL Azure hello z [witrynę Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureSQLAnalyticsOMS?tab=Overview) lub za pomocą hello procesu opisanego w temacie [rozwiązań analizy dzienników dodać hello galerii rozwiązań](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="4a2fe-143">Add hello Azure SQL Analytics solution tooyour workspace from [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureSQLAnalyticsOMS?tab=Overview) or by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="4a2fe-144">W portalu Azure hello, kliknij przycisk **nowy** (hello + symbol), następnie hello listy zasobów, wybierz **monitorowanie i zarządzanie**.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-144">In hello Azure portal, click **New** (hello + symbol), then in hello list of resources, select **Monitoring + Management**.</span></span>  
    <span data-ttu-id="4a2fe-145">![Monitorowanie i zarządzanie](./media/log-analytics-azure-sql/monitoring-management.png)</span><span class="sxs-lookup"><span data-stu-id="4a2fe-145">![Monitoring + Management](./media/log-analytics-azure-sql/monitoring-management.png)</span></span>
3. <span data-ttu-id="4a2fe-146">W hello **monitorowanie i zarządzanie** listy kliknij **zobaczyć wszystkie**.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-146">In hello **Monitoring + Management** list click **See all**.</span></span>
4. <span data-ttu-id="4a2fe-147">W hello **zalecane** kliknij **więcej** , a następnie hello nowej listy, Znajdź **analiza SQL Azure (wersja zapoznawcza)** i wybierz go.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-147">In hello **Recommended** list, click **More** , and then in hello new list, find **Azure SQL Analytics (Preview)** and then select it.</span></span>  
    <span data-ttu-id="4a2fe-148">![Rozwiązania analizy SQL Azure](./media/log-analytics-azure-sql/azure-sql-solution-portal.png)</span><span class="sxs-lookup"><span data-stu-id="4a2fe-148">![Azure SQL Analytics solution](./media/log-analytics-azure-sql/azure-sql-solution-portal.png)</span></span>
5. <span data-ttu-id="4a2fe-149">W hello **analiza SQL Azure (wersja zapoznawcza)** bloku, kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-149">In hello **Azure SQL Analytics (Preview)** blade, click **Create**.</span></span>  
    <span data-ttu-id="4a2fe-150">![Tworzenie](./media/log-analytics-azure-sql/portal-create.png)</span><span class="sxs-lookup"><span data-stu-id="4a2fe-150">![Create](./media/log-analytics-azure-sql/portal-create.png)</span></span>
6. <span data-ttu-id="4a2fe-151">W hello **Utwórz nowe rozwiązanie** bloku, wybierz hello roboczym mają tooadd hello rozwiązania tooand, następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-151">In hello **Create new solution** blade, select hello workspace that you want tooadd hello solution tooand then click **Create**.</span></span>  
    <span data-ttu-id="4a2fe-152">![Dodaj tooworkspace](./media/log-analytics-azure-sql/add-to-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="4a2fe-152">![add tooworkspace](./media/log-analytics-azure-sql/add-to-workspace.png)</span></span>


### <a name="tooconfigure-multiple-azure-subscriptions"></a><span data-ttu-id="4a2fe-153">tooconfigure wiele subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="4a2fe-153">tooconfigure multiple Azure subscriptions</span></span>

<span data-ttu-id="4a2fe-154">toosupport wiele subskrypcji, użyj skryptu programu PowerShell hello z [rejestrowania metryki zasobów Azure włączyć przy użyciu programu PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span><span class="sxs-lookup"><span data-stu-id="4a2fe-154">toosupport multiple subscriptions, use hello PowerShell script from [Enable Azure resource metrics logging using PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span></span> <span data-ttu-id="4a2fe-155">Podaj identyfikator zasobu obszaru roboczego hello jako parametr podczas wykonywania hello danych diagnostycznych toosend skryptu z zasobów w obszarze roboczym tooa jedną subskrypcją platformy Azure w innej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-155">Provide hello workspace resource ID as a parameter when executing hello script toosend diagnostic data from resources in one Azure subscription tooa workspace in another Azure subscription.</span></span>

<span data-ttu-id="4a2fe-156">**Przykład**</span><span class="sxs-lookup"><span data-stu-id="4a2fe-156">**Example**</span></span>

```
PS C:\> $WSID = "/subscriptions/<subID>/resourcegroups/oms/providers/microsoft.operationalinsights/workspaces/omsws"
```

```
PS C:\> .\Enable-AzureRMDiagnostics.ps1 -WSID $WSID
```

## <a name="using-hello-solution"></a><span data-ttu-id="4a2fe-157">Za pomocą rozwiązania hello</span><span class="sxs-lookup"><span data-stu-id="4a2fe-157">Using hello solution</span></span>

<span data-ttu-id="4a2fe-158">Po dodaniu obszar roboczy tooyour rozwiązania hello powitalne kafelka analiza SQL Azure jest dodawany tooyour obszaru roboczego i wygląda na to, w obszarze Przegląd.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-158">When you add hello solution tooyour workspace, hello Azure SQL Analytics tile is added tooyour workspace, and it appears in Overview.</span></span> <span data-ttu-id="4a2fe-159">Kafelek Hello jest wyświetlana liczba hello baz danych Azure SQL i Azure SQL pule elastyczne, które rozwiązanie hello jest podłączony do.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-159">hello tile shows hello number of Azure SQL databases and Azure SQL elastic pools that hello solution is connected to.</span></span>

![Kafelek SQL Analytics Azure](./media/log-analytics-azure-sql/azure-sql-sol-tile.png)

### <a name="viewing-azure-sql-analytics-data"></a><span data-ttu-id="4a2fe-161">Wyświetlanie danych analiz SQL Azure</span><span class="sxs-lookup"><span data-stu-id="4a2fe-161">Viewing Azure SQL Analytics data</span></span>

<span data-ttu-id="4a2fe-162">Polecenie hello **analiza SQL Azure** nawigacyjnego Azure SQL Analytics hello tooopen kafelka.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-162">Click on hello **Azure SQL Analytics** tile tooopen hello Azure SQL Analytics dashboard.</span></span> <span data-ttu-id="4a2fe-163">pulpit nawigacyjny Hello zawiera bloki hello określonych poniżej.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-163">hello dashboard includes hello blades defined below.</span></span> <span data-ttu-id="4a2fe-164">Każdy blok zawiera listę zasobów too15 (subskrypcji, serwer puli elastycznej i bazy danych).</span><span class="sxs-lookup"><span data-stu-id="4a2fe-164">Each blade lists up too15 resources (subscription, server, elastic pool, and database).</span></span> <span data-ttu-id="4a2fe-165">Kliknij dowolny pulpit nawigacyjny hello tooopen zasobów powitania dla tego konkretnego zasobu.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-165">Click any of hello resources tooopen hello dashboard for that specific resource.</span></span> <span data-ttu-id="4a2fe-166">Elastycznej puli lub baza danych zawiera wykresy hello o metryki dla wybranego zasobu.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-166">Elastic Pool or Database contains hello charts with metrics for a selected resource.</span></span> <span data-ttu-id="4a2fe-167">Kliknij okno dialogowe wyszukiwania dziennika hello tooopen wykresu.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-167">Click a chart tooopen hello Log Search dialog.</span></span>

| <span data-ttu-id="4a2fe-168">Blok</span><span class="sxs-lookup"><span data-stu-id="4a2fe-168">Blade</span></span> | <span data-ttu-id="4a2fe-169">Opis</span><span class="sxs-lookup"><span data-stu-id="4a2fe-169">Description</span></span> |
|---|---|
| <span data-ttu-id="4a2fe-170">Subskrypcje</span><span class="sxs-lookup"><span data-stu-id="4a2fe-170">Subscriptions</span></span> | <span data-ttu-id="4a2fe-171">Lista subskrypcji z liczbą połączonych serwerów, pule adresów i baz danych.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-171">List of subscriptions with number of connected servers, pools, and databases.</span></span> |
| <span data-ttu-id="4a2fe-172">Serwery</span><span class="sxs-lookup"><span data-stu-id="4a2fe-172">Servers</span></span> | <span data-ttu-id="4a2fe-173">Lista serwerów z liczbą pul połączonych i baz danych.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-173">List of servers with number of connected pools and databases.</span></span> |
| <span data-ttu-id="4a2fe-174">Pule elastyczne</span><span class="sxs-lookup"><span data-stu-id="4a2fe-174">Elastic Pools</span></span> | <span data-ttu-id="4a2fe-175">Lista połączonych pul elastycznych z maksymalną GB i liczby jednostek eDTU w hello obserwowanych okresu.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-175">List of connected elastic pools with maximum GB and eDTU in hello observed period.</span></span> |
|<span data-ttu-id="4a2fe-176">Bazy danych</span><span class="sxs-lookup"><span data-stu-id="4a2fe-176">Databases</span></span> | <span data-ttu-id="4a2fe-177">Listy baz danych połączonych z maksymalną GB i jednostek dtu w warstwie w hello obserwowanych okresu.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-177">List of connected databases with maximum GB and DTU in hello observed period.</span></span>|


### <a name="analyze-data-and-create-alerts"></a><span data-ttu-id="4a2fe-178">Analizuj dane i tworzyć alerty</span><span class="sxs-lookup"><span data-stu-id="4a2fe-178">Analyze data and create alerts</span></span>

<span data-ttu-id="4a2fe-179">Można łatwo tworzyć alerty z danymi hello pochodzące z zasobów bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-179">You can easily create alerts with hello data coming from Azure SQL Database resources.</span></span> <span data-ttu-id="4a2fe-180">Poniżej przedstawiono kilka przydatne [wyszukiwania dziennika](log-analytics-log-searches.md) zapytań, które służy do tworzenia alertu:</span><span class="sxs-lookup"><span data-stu-id="4a2fe-180">Here are a couple of useful [log search](log-analytics-log-searches.md) queries that you can use for alerting:</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]


<span data-ttu-id="4a2fe-181">*Wysoka DTU na bazę danych Azure SQL*</span><span class="sxs-lookup"><span data-stu-id="4a2fe-181">*High DTU on Azure SQL Database*</span></span>

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/DATABASES/"* MetricName=dtu_consumption_percent | measure Avg(Average) by Resource interval 5minutes
```

<span data-ttu-id="4a2fe-182">*Wysoka jednostek DTU w puli elastycznej bazy danych Azure SQL*</span><span class="sxs-lookup"><span data-stu-id="4a2fe-182">*High DTU on Azure SQL Database Elastic Pool*</span></span>

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource interval 5minutes
```

<span data-ttu-id="4a2fe-183">Te tooalert zapytań na podstawie alertu można użyć na określone progi dla bazy danych SQL Azure i elastyczne pule.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-183">You can use these alert-based queries tooalert on specific thresholds for both Azure SQL Database and elastic pools.</span></span> <span data-ttu-id="4a2fe-184">alert dotyczący obszar roboczy OMS tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="4a2fe-184">tooconfigure an alert for your OMS workspace:</span></span>

#### <a name="tooconfigure-an-alert-for-your-workspace"></a><span data-ttu-id="4a2fe-185">tooconfigure alert dla obszaru roboczego</span><span class="sxs-lookup"><span data-stu-id="4a2fe-185">tooconfigure an alert for your workspace</span></span>

1. <span data-ttu-id="4a2fe-186">Przejdź toohello [portalu OMS](http://mms.microsoft.com/) i zaloguj się.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-186">Go toohello [OMS portal](http://mms.microsoft.com/) and sign in.</span></span>
2. <span data-ttu-id="4a2fe-187">Otwórz obszar roboczy hello, skonfigurowanego dla hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-187">Open hello workspace that you have configured for hello solution.</span></span>
3. <span data-ttu-id="4a2fe-188">Na stronie Przegląd powitania kliknij hello **analiza SQL Azure (wersja zapoznawcza)** kafelka.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-188">On hello Overview page, click hello **Azure SQL Analytics (Preview)** tile.</span></span>
4. <span data-ttu-id="4a2fe-189">Uruchom jedno z hello przykładowych zapytań.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-189">Run one of hello example queries.</span></span>
5. <span data-ttu-id="4a2fe-190">W wyszukiwaniu dziennik, kliknij przycisk **alertu**.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-190">In Log Search, click **Alert**.</span></span>  
<span data-ttu-id="4a2fe-191">![Utwórz alert podczas wyszukiwania.](./media/log-analytics-azure-sql/create-alert01.png)</span><span class="sxs-lookup"><span data-stu-id="4a2fe-191">![create alert in search](./media/log-analytics-azure-sql/create-alert01.png)</span></span>
6. <span data-ttu-id="4a2fe-192">Na powitania **Dodaj regułę alertu** Ustaw odpowiednie właściwości hello a hello określone progi, które mają, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-192">On hello **Add Alert Rule** page, configure hello appropriate properties and hello specific thresholds that you want and then click **Save**.</span></span>  
<span data-ttu-id="4a2fe-193">![Dodaj regułę alertów](./media/log-analytics-azure-sql/create-alert02.png)</span><span class="sxs-lookup"><span data-stu-id="4a2fe-193">![add alert rule](./media/log-analytics-azure-sql/create-alert02.png)</span></span>

### <a name="act-on-azure-sql-analytics-data"></a><span data-ttu-id="4a2fe-194">Wpływ na dane analityczne SQL Azure</span><span class="sxs-lookup"><span data-stu-id="4a2fe-194">Act on Azure SQL Analytics data</span></span>

<span data-ttu-id="4a2fe-195">Na przykład jeden hello najbardziej przydatne zapytań, które można wykonywać jest użycie jednostek dtu w warstwie hello toocompare dla wszystkich pul elastycznych SQL Azure wszystkich subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-195">As an example, one of hello most useful queries that you can perform is toocompare hello DTU utilization for all Azure SQL Elastic Pools across all your Azure subscriptions.</span></span> <span data-ttu-id="4a2fe-196">Jednostki przepływności bazy danych (DTU) zapewnia toodescribe sposób hello relatywną pojemność poziomu wydajności baz danych Basic, Standard i Premium i pul.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-196">Database Throughput Unit (DTU) provides a way toodescribe hello relative capacity of a performance level of Basic, Standard, and Premium databases and pools.</span></span> <span data-ttu-id="4a2fe-197">Liczba jednostek Dtu są oparte na mieszanych pomiarach procesora CPU, pamięci, odczytuje i zapisuje.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-197">DTUs are based on a blended measure of CPU, memory, reads, and writes.</span></span> <span data-ttu-id="4a2fe-198">Jak zwiększyć liczbę jednostek Dtu, hello oferowane przez zwiększa poziom wydajności hello zasilania.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-198">As DTUs increase, hello power offered by hello performance level increases.</span></span> <span data-ttu-id="4a2fe-199">Na przykład poziomu wydajności z 5 jednostkami Dtu ma pięć razy więcej mocy niż poziom wydajności z jednostek dtu w warstwie 1.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-199">For example, a performance level with 5 DTUs has five times more power than a performance level with 1 DTU.</span></span> <span data-ttu-id="4a2fe-200">Maksymalny limit przydziału jednostek DTU dotyczy tooeach serwerem i elastyczne puli.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-200">A maximum DTU quota applies tooeach server and elastic pool.</span></span>

<span data-ttu-id="4a2fe-201">Uruchamiając hello następującego zapytania wyszukiwania dziennika można łatwo stwierdzić, jeśli analizę lub ponad przy użyciu programu SQL Azure elastyczne pule.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-201">By running hello following Log Search query, you can easily tell if you are underutilizing or over utilizing your SQL Azure elastic pools.</span></span>

```
Type=AzureMetrics ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource | display LineChart
```

>[!NOTE]
> <span data-ttu-id="4a2fe-202">Jeśli obszaru roboczego został uaktualniony toohello [języka zapytań nowe analizy dzienników](log-analytics-log-search-upgrade.md), następnie hello powyżej zapytania spowoduje zmianę następujących toohello.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-202">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then hello above query would change toohello following.</span></span>
>
>`search in (AzureMetrics) isnotempty(ResourceId) and "/ELASTICPOOLS/" and MetricName == "dtu_consumption_percent" | summarize AggregatedValue = avg(Average) by bin(TimeGenerated, 1h), Resource | render timechart`

<span data-ttu-id="4a2fe-203">W hello poniższy przykład, widać, że jeden puli elastycznej ma wysokiego użycia bliskie 100% jednostek dtu w warstwie, podczas gdy inne mają bardzo mało użycia.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-203">In hello following example, you can see that one elastic pool has a high usage near 100% DTU while others have very little usage.</span></span> <span data-ttu-id="4a2fe-204">Możesz przejrzeć dalsze tootroubleshoot potencjalnych najnowszych zmian w środowisku przy użyciu dzienników działanie usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-204">You can investigate further tootroubleshoot potential recent changes in your environment using Azure Activity logs.</span></span>

![Wyniki wyszukiwania dziennika - wysokie użycie](./media/log-analytics-azure-sql/log-search-high-util.png)

## <a name="see-also"></a><span data-ttu-id="4a2fe-206">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="4a2fe-206">See also</span></span>

- <span data-ttu-id="4a2fe-207">Użyj [dziennik wyszukiwania](log-analytics-log-searches.md) w tooview analizy dzienników szczegółowe danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-207">Use [Log Searches](log-analytics-log-searches.md) in Log Analytics tooview detailed Azure SQL data.</span></span>
- <span data-ttu-id="4a2fe-208">[Tworzenie własnych pulpity nawigacyjne](log-analytics-dashboards.md) przedstawiający danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-208">[Create your own dashboards](log-analytics-dashboards.md) showing Azure SQL data.</span></span>
- <span data-ttu-id="4a2fe-209">[Tworzenie alertów](log-analytics-alerts.md) po wystąpieniu określonych zdarzeń Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="4a2fe-209">[Create alerts](log-analytics-alerts.md) when specific Azure SQL events occur.</span></span>
