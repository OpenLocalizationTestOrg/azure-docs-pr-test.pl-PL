---
title: "Zapisane wyszukiwania i alertów w rozwiązaniach pakietu OMS | Dokumentacja firmy Microsoft"
description: "Rozwiązania w OMS zazwyczaj uwzględnia zapisane wyszukiwania w analizy dzienników do analizowania danych zebranych przez rozwiązanie.  Mogą również definiować alertów umożliwiających powiadamianie użytkownika lub automatyczne wykonywanie akcji w odpowiedzi na problem krytyczny.  W tym artykule opisano sposób definiowania analizy dzienników zapisane wyszukiwania i alertów w szablonu usługi ARM, aby mogły one zostać uwzględnione w rozwiązaniach do zarządzania."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 21c42a747a08c5386c65d10190baf0054a7adef8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="adding-log-analytics-saved-searches-and-alerts-to-oms-management-solution-preview"></a><span data-ttu-id="6ba17-105">Dodawanie analizy dzienników zapisane wyszukiwania i alerty OMS rozwiązania do zarządzania (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="6ba17-105">Adding Log Analytics saved searches and alerts to OMS management solution (Preview)</span></span>

> [!NOTE]
> <span data-ttu-id="6ba17-106">To jest wstępna dokumentacji do tworzenia rozwiązań do zarządzania w OMS, które są obecnie w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="6ba17-106">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="6ba17-107">Żadnego schematu opisanych poniżej może ulec zmianie.</span><span class="sxs-lookup"><span data-stu-id="6ba17-107">Any schema described below is subject to change.</span></span>   


<span data-ttu-id="6ba17-108">[Rozwiązania do zarządzania w OMS](operations-management-suite-solutions.md) zazwyczaj uwzględnia [zapisane wyszukiwania](../log-analytics/log-analytics-log-searches.md) w analizy dzienników do analizowania danych zebranych przez rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="6ba17-108">[Management solutions in OMS](operations-management-suite-solutions.md) will typically include [saved searches](../log-analytics/log-analytics-log-searches.md) in Log Analytics to analyze data collected by the solution.</span></span>  <span data-ttu-id="6ba17-109">Mogą również określić [alerty](../log-analytics/log-analytics-alerts.md) powiadamia użytkownika lub automatyczne wykonywanie akcji w odpowiedzi na problem krytyczny.</span><span class="sxs-lookup"><span data-stu-id="6ba17-109">They may also define [alerts](../log-analytics/log-analytics-alerts.md) to notify the user or automatically take action in response to a critical issue.</span></span>  <span data-ttu-id="6ba17-110">W tym artykule opisano sposób definiowania analizy dzienników zapisane wyszukiwania i alertów w [szablonu zarządzanie zasobami](../resource-manager-template-walkthrough.md) aby mogły one zostać uwzględnione w [rozwiązań do zarządzania](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="6ba17-110">This article describes how to define Log Analytics saved searches and alerts in a [Resource Management template](../resource-manager-template-walkthrough.md) so they can be included in [management solutions](operations-management-suite-solutions-creating.md).</span></span>

> [!NOTE]
> <span data-ttu-id="6ba17-111">Przykłady w tym artykule, użyj parametrów i zmiennych, które są wymagane ani wspólne dla rozwiązań do zarządzania i opisano w [tworzenia rozwiązań do zarządzania w Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span><span class="sxs-lookup"><span data-stu-id="6ba17-111">The samples in this article use parameters and variables that are either required or common to management solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="6ba17-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6ba17-112">Prerequisites</span></span>
<span data-ttu-id="6ba17-113">W tym artykule przyjęto założenie, że znasz już jak [tworzenie rozwiązania do zarządzania](operations-management-suite-solutions-creating.md) i struktura [szablon ARM](../resource-group-authoring-templates.md) i plik rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="6ba17-113">This article assumes that you're already familiar with how to [create a management solution](operations-management-suite-solutions-creating.md) and the structure of an [ARM template](../resource-group-authoring-templates.md) and solution file.</span></span>


## <a name="log-analytics-workspace"></a><span data-ttu-id="6ba17-114">Obszar roboczy analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="6ba17-114">Log Analytics Workspace</span></span>
<span data-ttu-id="6ba17-115">Wszystkie zasoby w analizy dzienników znajdują się w [obszaru roboczego](../log-analytics/log-analytics-manage-access.md).</span><span class="sxs-lookup"><span data-stu-id="6ba17-115">All resources in Log Analytics are contained in a [workspace](../log-analytics/log-analytics-manage-access.md).</span></span>  <span data-ttu-id="6ba17-116">Zgodnie z opisem w [OMS obszaru roboczego i konto automatyzacji](operations-management-suite-solutions.md#oms-workspace-and-automation-account) obszaru roboczego nie jest zawarty w rozwiązaniu do zarządzania, ale musi istnieć przed zainstalowaniem rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="6ba17-116">As described in [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) the workspace isn't included in the management solution but must exist before the solution is installed.</span></span>  <span data-ttu-id="6ba17-117">Jeśli nie jest dostępny, nie będą instalacji rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="6ba17-117">If it isn't available, then the solution install will fail.</span></span>

<span data-ttu-id="6ba17-118">Nazwa obszaru roboczego jest nazwy każdego zasobu analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="6ba17-118">The name of the workspace is in the name of each Log Analytics resource.</span></span>  <span data-ttu-id="6ba17-119">Ma to rozwiązanie z **obszaru roboczego** parametru, jak w poniższym przykładzie savedsearch zasobu.</span><span class="sxs-lookup"><span data-stu-id="6ba17-119">This is done in the solution with the **workspace** parameter as in the following example of a savedsearch resource.</span></span>

    "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearchId'))]"


## <a name="saved-searches"></a><span data-ttu-id="6ba17-120">Zapisane wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="6ba17-120">Saved Searches</span></span>
<span data-ttu-id="6ba17-121">Obejmują [zapisane wyszukiwania](../log-analytics/log-analytics-log-searches.md) w rozwiązaniu, aby umożliwić użytkownikom zapytania danych zbieranych przez rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="6ba17-121">Include [saved searches](../log-analytics/log-analytics-log-searches.md) in a solution to allow users to query data collected by your solution.</span></span>  <span data-ttu-id="6ba17-122">Zapisane wyszukiwania zostanie wyświetlony w obszarze **ulubione** w portalu OMS i **zapisane wyszukiwania** w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6ba17-122">Saved searches will appear under **Favorites** in the OMS portal and **Saved Searches** in the Azure portal .</span></span>  <span data-ttu-id="6ba17-123">Zapisane wyszukiwanie jest również wymagany dla każdego alertu.</span><span class="sxs-lookup"><span data-stu-id="6ba17-123">A saved search is also required for each alert.</span></span>   

<span data-ttu-id="6ba17-124">[Analiza dzienników zapisane wyszukiwanie](../log-analytics/log-analytics-log-searches.md) zasobów mieć typu `Microsoft.OperationalInsights/workspaces/savedSearches` i ma następującą strukturę.</span><span class="sxs-lookup"><span data-stu-id="6ba17-124">[Log Analytics saved search](../log-analytics/log-analytics-log-searches.md) resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches` and have the following structure.</span></span>  <span data-ttu-id="6ba17-125">W tym wspólnych zmiennych i parametrów, aby mogli skopiuj i wklej następujący fragment kodu w pliku rozwiązania i Zmień nazwy parametrów.</span><span class="sxs-lookup"><span data-stu-id="6ba17-125">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
        ],
        "tags": { },
        "properties": {
            "etag": "*",
            "query": "[variables('SavedSearch').Query]",
            "displayName": "[variables('SavedSearch').DisplayName]",
            "category": "[variables('SavedSearch').Category]"
        }
    }



<span data-ttu-id="6ba17-126">Każdej z właściwości zapisanego kryterium wyszukiwania są opisane w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="6ba17-126">Each of the properties of a saved search are described in the following table.</span></span> 

| <span data-ttu-id="6ba17-127">Właściwość</span><span class="sxs-lookup"><span data-stu-id="6ba17-127">Property</span></span> | <span data-ttu-id="6ba17-128">Opis</span><span class="sxs-lookup"><span data-stu-id="6ba17-128">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="6ba17-129">category</span><span class="sxs-lookup"><span data-stu-id="6ba17-129">category</span></span> | <span data-ttu-id="6ba17-130">Kategoria dla zapisanego wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="6ba17-130">The category for the saved search.</span></span>  <span data-ttu-id="6ba17-131">Żadnych zapisanych wyszukiwań, w tym samym rozwiązaniu często muszą współdzielić jednej kategorii, więc są pogrupowane w konsoli.</span><span class="sxs-lookup"><span data-stu-id="6ba17-131">Any saved searches in the same solution will often share a single category so they are grouped together in the console.</span></span> |
| <span data-ttu-id="6ba17-132">Nazwa wyświetlana</span><span class="sxs-lookup"><span data-stu-id="6ba17-132">displayname</span></span> | <span data-ttu-id="6ba17-133">Nazwa do wyświetlenia dla zapisanego wyszukiwania w portalu.</span><span class="sxs-lookup"><span data-stu-id="6ba17-133">Name to display for the saved search in the portal.</span></span> |
| <span data-ttu-id="6ba17-134">query</span><span class="sxs-lookup"><span data-stu-id="6ba17-134">query</span></span> | <span data-ttu-id="6ba17-135">Zapytanie do uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="6ba17-135">Query to run.</span></span> |

> [!NOTE]
> <span data-ttu-id="6ba17-136">Może być konieczne użycie znaki specjalne w zapytaniu, jeśli zawiera znaki, które mogą być interpretowane jako JSON.</span><span class="sxs-lookup"><span data-stu-id="6ba17-136">You may need to use escape characters in the query if it includes characters that could be interpreted as JSON.</span></span>  <span data-ttu-id="6ba17-137">Na przykład, jeśli zapytanie zostało **OperationName:"Microsoft.Compute/virtualMachines/write typu: AzureActivity"**, mają być zapisywane w pliku rozwiązania jako **OperationName typu: AzureActivity:\"Microsoft.Compute/virtualMachines/write\"**.</span><span class="sxs-lookup"><span data-stu-id="6ba17-137">For example, if your query was **Type:AzureActivity OperationName:"Microsoft.Compute/virtualMachines/write"**, it should be written in the solution file as **Type:AzureActivity OperationName:\"Microsoft.Compute/virtualMachines/write\"**.</span></span>

## <a name="alerts"></a><span data-ttu-id="6ba17-138">Alerty</span><span class="sxs-lookup"><span data-stu-id="6ba17-138">Alerts</span></span>
<span data-ttu-id="6ba17-139">[Rejestrowania alertów Analytics](../log-analytics/log-analytics-alerts.md) są tworzone przez reguły alertów, które uruchomić zapisane wyszukiwanie w regularnych odstępach czasu.</span><span class="sxs-lookup"><span data-stu-id="6ba17-139">[Log Analytics alerts](../log-analytics/log-analytics-alerts.md) are created by alert rules that run a saved search on a regular interval.</span></span>  <span data-ttu-id="6ba17-140">Jeśli wyniki zapytania dopasowania określone kryteria, tworzony jest rekord alertów i są uruchamiane co najmniej jednej akcji.</span><span class="sxs-lookup"><span data-stu-id="6ba17-140">If the results of the query match specified criteria, an alert record is created and one or more actions are run.</span></span>  

<span data-ttu-id="6ba17-141">Reguły alertów w rozwiązaniu do zarządzania składają się z następujących trzech różnych zasobów.</span><span class="sxs-lookup"><span data-stu-id="6ba17-141">Alert rules in a management solution are made up of the following three different resources.</span></span>

- <span data-ttu-id="6ba17-142">**Zapisane wyszukiwanie.**</span><span class="sxs-lookup"><span data-stu-id="6ba17-142">**Saved search.**</span></span>  <span data-ttu-id="6ba17-143">Definiuje wyszukiwania dziennika, które będą uruchamiane.</span><span class="sxs-lookup"><span data-stu-id="6ba17-143">Defines the log search that will be run.</span></span>  <span data-ttu-id="6ba17-144">Wiele reguł alertów można udostępniać pojedynczy zapisanego kryterium wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="6ba17-144">Multiple alert rules can share a single saved search.</span></span>
- <span data-ttu-id="6ba17-145">**Harmonogram.**</span><span class="sxs-lookup"><span data-stu-id="6ba17-145">**Schedule.**</span></span>  <span data-ttu-id="6ba17-146">Określa, jak często wyszukiwania dziennika zostanie uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="6ba17-146">Defines how often the log search will be run.</span></span>  <span data-ttu-id="6ba17-147">Każdej reguły alertu będzie mieć tylko jeden harmonogram.</span><span class="sxs-lookup"><span data-stu-id="6ba17-147">Each alert rule will have one and only one schedule.</span></span>
- <span data-ttu-id="6ba17-148">**Akcja alertu.**</span><span class="sxs-lookup"><span data-stu-id="6ba17-148">**Alert action.**</span></span>  <span data-ttu-id="6ba17-149">Każdej reguły alertu będzie mieć jeden zasób akcji z typem **Alert** definiuje szczegóły alertu, takie jak kryteria utworzenia rekordu alertów i ważność alertu.</span><span class="sxs-lookup"><span data-stu-id="6ba17-149">Each alert rule will have one action resource with a type of **Alert** that defines the details of the alert such as the criteria for when an alert record will be created and the alert's severity.</span></span>  <span data-ttu-id="6ba17-150">Zasób akcji zostanie opcjonalnie określić odpowiedź poczty i elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="6ba17-150">The action resource will optionally define a mail and runbook response.</span></span>
- <span data-ttu-id="6ba17-151">**Akcja elementu Webhook (opcjonalnie).**</span><span class="sxs-lookup"><span data-stu-id="6ba17-151">**Webhook action (optional).**</span></span>  <span data-ttu-id="6ba17-152">Reguła alertu wywoła elementu webhook, a następnie go wymaga dodatkowych czynności zasobu o typie **Webhook**.</span><span class="sxs-lookup"><span data-stu-id="6ba17-152">If the alert rule will call a webhook, then it requires an additional action resource with a type of **Webhook**.</span></span>    

<span data-ttu-id="6ba17-153">Zapisane wyszukiwania zasobów opisanych powyżej.</span><span class="sxs-lookup"><span data-stu-id="6ba17-153">Saved search resources are described above.</span></span>  <span data-ttu-id="6ba17-154">Inne zasoby są opisane poniżej.</span><span class="sxs-lookup"><span data-stu-id="6ba17-154">The other resources are described below.</span></span>


### <a name="schedule-resource"></a><span data-ttu-id="6ba17-155">Zasób harmonogramu</span><span class="sxs-lookup"><span data-stu-id="6ba17-155">Schedule resource</span></span>

<span data-ttu-id="6ba17-156">Zapisane wyszukiwanie może mieć co najmniej jeden harmonogram z każdym harmonogramem reprezentujący oddzielne reguły alertu.</span><span class="sxs-lookup"><span data-stu-id="6ba17-156">A saved search can have one or more schedules with each schedule representing a separate alert rule.</span></span> <span data-ttu-id="6ba17-157">Harmonogram Określa, jak często wyszukiwanie jest uruchamiania i przedział czasu, przez który dane są pobierane.</span><span class="sxs-lookup"><span data-stu-id="6ba17-157">The schedule defines how often the search is run and the time interval over which the data is retrieved.</span></span>  <span data-ttu-id="6ba17-158">Planowanie zasobów mieć typu `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/` i ma następującą strukturę.</span><span class="sxs-lookup"><span data-stu-id="6ba17-158">Schedule resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/` and have the following structure.</span></span> <span data-ttu-id="6ba17-159">W tym wspólnych zmiennych i parametrów, aby mogli skopiuj i wklej następujący fragment kodu w pliku rozwiązania i Zmień nazwy parametrów.</span><span class="sxs-lookup"><span data-stu-id="6ba17-159">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 


    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name)]"
        ],
        "properties": {
            "etag": "*",
            "interval": "[variables('Schedule').Interval]",
            "queryTimeSpan": "[variables('Schedule').TimeSpan]",
            "enabled": "[variables('Schedule').Enabled]"
        }
    }



<span data-ttu-id="6ba17-160">W poniższej tabeli opisano właściwości planowania zasobów.</span><span class="sxs-lookup"><span data-stu-id="6ba17-160">The properties for schedule resources are described in the following table.</span></span>

| <span data-ttu-id="6ba17-161">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="6ba17-161">Element name</span></span> | <span data-ttu-id="6ba17-162">Wymagane</span><span class="sxs-lookup"><span data-stu-id="6ba17-162">Required</span></span> | <span data-ttu-id="6ba17-163">Opis</span><span class="sxs-lookup"><span data-stu-id="6ba17-163">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="6ba17-164">włączone</span><span class="sxs-lookup"><span data-stu-id="6ba17-164">enabled</span></span>       | <span data-ttu-id="6ba17-165">Tak</span><span class="sxs-lookup"><span data-stu-id="6ba17-165">Yes</span></span> | <span data-ttu-id="6ba17-166">Określa, czy alert jest włączony podczas jego tworzenia.</span><span class="sxs-lookup"><span data-stu-id="6ba17-166">Specifies whether the alert is enabled when it's created.</span></span> |
| <span data-ttu-id="6ba17-167">Interwał</span><span class="sxs-lookup"><span data-stu-id="6ba17-167">interval</span></span>      | <span data-ttu-id="6ba17-168">Tak</span><span class="sxs-lookup"><span data-stu-id="6ba17-168">Yes</span></span> | <span data-ttu-id="6ba17-169">Częstotliwość wykonywania kwerendy w minutach.</span><span class="sxs-lookup"><span data-stu-id="6ba17-169">How often the query runs in minutes.</span></span> |
| <span data-ttu-id="6ba17-170">QueryTimeSpan</span><span class="sxs-lookup"><span data-stu-id="6ba17-170">queryTimeSpan</span></span> | <span data-ttu-id="6ba17-171">Tak</span><span class="sxs-lookup"><span data-stu-id="6ba17-171">Yes</span></span> | <span data-ttu-id="6ba17-172">Długość czasu w minutach, przez który ocena wyników.</span><span class="sxs-lookup"><span data-stu-id="6ba17-172">Length of time in minutes over which to evaluate results.</span></span> |

<span data-ttu-id="6ba17-173">Zasób harmonogramu powinien są zależne od zapisanego wyszukiwania, aby przed harmonogram jest tworzona.</span><span class="sxs-lookup"><span data-stu-id="6ba17-173">The schedule resource should depend on the saved search so that it's created before the schedule.</span></span>


### <a name="actions"></a><span data-ttu-id="6ba17-174">Akcje</span><span class="sxs-lookup"><span data-stu-id="6ba17-174">Actions</span></span>
<span data-ttu-id="6ba17-175">Istnieją dwa typy akcji zasobu określonego przez **typu** właściwości.</span><span class="sxs-lookup"><span data-stu-id="6ba17-175">There are two types of action resource specified by the **Type** property.</span></span>  <span data-ttu-id="6ba17-176">Harmonogram wymaga jednego **Alert** akcji, który definiuje szczegóły reguły alertów i jakie akcje są pobierane, gdy tworzony jest alert.</span><span class="sxs-lookup"><span data-stu-id="6ba17-176">A schedule requires one **Alert** action which defines the details of the alert rule and what actions are taken when an alert is created.</span></span>  <span data-ttu-id="6ba17-177">Mogą również obejmować **Webhook** akcji, o ile elementu webhook powinna być wywoływana w alercie.</span><span class="sxs-lookup"><span data-stu-id="6ba17-177">It may also include a **Webhook** action if a webhook should be called from the alert.</span></span>  

<span data-ttu-id="6ba17-178">Zasoby akcji mieć typu `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions`.</span><span class="sxs-lookup"><span data-stu-id="6ba17-178">Action resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions`.</span></span>  

#### <a name="alert-actions"></a><span data-ttu-id="6ba17-179">Akcje alertów</span><span class="sxs-lookup"><span data-stu-id="6ba17-179">Alert actions</span></span>

<span data-ttu-id="6ba17-180">Każdy harmonogram będzie mieć jeden **alertu** akcji.</span><span class="sxs-lookup"><span data-stu-id="6ba17-180">Every schedule will have one **Alert** action.</span></span>  <span data-ttu-id="6ba17-181">Określa szczegóły alertu, i opcjonalnie działań powiadomień i korygowania.</span><span class="sxs-lookup"><span data-stu-id="6ba17-181">This defines the details of the alert and optionally notification and remediation actions.</span></span>  <span data-ttu-id="6ba17-182">Powiadomienie o wysyła wiadomość e-mail do co najmniej jeden adres.</span><span class="sxs-lookup"><span data-stu-id="6ba17-182">A notification sends an email to one or more addresses.</span></span>  <span data-ttu-id="6ba17-183">Korygowanie uruchamia element runbook automatyzacji Azure, aby podjąć próbę rozwiązania problemu.</span><span class="sxs-lookup"><span data-stu-id="6ba17-183">A remediation starts a runbook in Azure Automation to attempt to remediate the detected issue.</span></span>

<span data-ttu-id="6ba17-184">Akcje alertu ma następującą strukturę.</span><span class="sxs-lookup"><span data-stu-id="6ba17-184">Alert actions have the following structure.</span></span>  <span data-ttu-id="6ba17-185">W tym wspólnych zmiennych i parametrów, aby mogli skopiuj i wklej następujący fragment kodu w pliku rozwiązania i Zmień nazwy parametrów.</span><span class="sxs-lookup"><span data-stu-id="6ba17-185">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 



    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name, '/', variables('Alert').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name, '/schedules/', variables('Schedule').Name)]"
        ],
        "properties": {
            "etag": "*",
            "type": "Alert",
            "name": "[variables('Alert').Name]",
            "description": "[variables('Alert').Description]",
            "severity": "[variables('Alert').Severity]",
            "threshold": {
                "operator": "[variables('Alert').Threshold.Operator]",
                "value": "[variables('Alert').Threshold.Value]",
                "metricsTrigger": {
                    "triggerCondition": "[variables('Alert').Threshold.Trigger.Condition]",
                    "operator": "[variables('Alert').Trigger.Operator]",
                    "value": "[variables('Alert').Trigger.Value]"
                },
            },
            "emailNotification": {
                "recipients": [
                    "[variables('Alert').Recipients]"
                ],
                "subject": "[variables('Alert').Subject]"
            },
            "remediation": {
                "runbookName": "[variables('Alert').Remedition.RunbookName]",
                "webhookUri": "[variables('Alert').Remedition.WebhookUri]"
            }
        }
    }

<span data-ttu-id="6ba17-186">W poniższych tabelach opisano właściwości zasobów akcji alertu.</span><span class="sxs-lookup"><span data-stu-id="6ba17-186">The properties for Alert action resources are described in the following tables.</span></span>

| <span data-ttu-id="6ba17-187">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="6ba17-187">Element name</span></span> | <span data-ttu-id="6ba17-188">Wymagane</span><span class="sxs-lookup"><span data-stu-id="6ba17-188">Required</span></span> | <span data-ttu-id="6ba17-189">Opis</span><span class="sxs-lookup"><span data-stu-id="6ba17-189">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="6ba17-190">Typ</span><span class="sxs-lookup"><span data-stu-id="6ba17-190">Type</span></span> | <span data-ttu-id="6ba17-191">Tak</span><span class="sxs-lookup"><span data-stu-id="6ba17-191">Yes</span></span> | <span data-ttu-id="6ba17-192">Typ akcji.</span><span class="sxs-lookup"><span data-stu-id="6ba17-192">Type of the action.</span></span>  <span data-ttu-id="6ba17-193">Są to **Alert** dla akcje alertu.</span><span class="sxs-lookup"><span data-stu-id="6ba17-193">This will be **Alert** for alert actions.</span></span> |
| <span data-ttu-id="6ba17-194">Nazwa</span><span class="sxs-lookup"><span data-stu-id="6ba17-194">Name</span></span> | <span data-ttu-id="6ba17-195">Tak</span><span class="sxs-lookup"><span data-stu-id="6ba17-195">Yes</span></span> | <span data-ttu-id="6ba17-196">Nazwa wyświetlana alertu.</span><span class="sxs-lookup"><span data-stu-id="6ba17-196">Display name for the alert.</span></span>  <span data-ttu-id="6ba17-197">Jest to nazwa, która jest wyświetlana w konsoli dla reguł alertów.</span><span class="sxs-lookup"><span data-stu-id="6ba17-197">This is the name that's displayed in the console for the alert rule.</span></span> |
| <span data-ttu-id="6ba17-198">Opis</span><span class="sxs-lookup"><span data-stu-id="6ba17-198">Description</span></span> | <span data-ttu-id="6ba17-199">Nie</span><span class="sxs-lookup"><span data-stu-id="6ba17-199">No</span></span> | <span data-ttu-id="6ba17-200">Opcjonalny opis alertu.</span><span class="sxs-lookup"><span data-stu-id="6ba17-200">Optional description of the alert.</span></span> |
| <span data-ttu-id="6ba17-201">Ważność</span><span class="sxs-lookup"><span data-stu-id="6ba17-201">Severity</span></span> | <span data-ttu-id="6ba17-202">Tak</span><span class="sxs-lookup"><span data-stu-id="6ba17-202">Yes</span></span> | <span data-ttu-id="6ba17-203">Ważność alertu rekordu z następujących wartości:</span><span class="sxs-lookup"><span data-stu-id="6ba17-203">Severity of the alert record from the following values:</span></span><br><br> <span data-ttu-id="6ba17-204">**Krytyczne**</span><span class="sxs-lookup"><span data-stu-id="6ba17-204">**Critical**</span></span><br><span data-ttu-id="6ba17-205">**Ostrzeżenie**</span><span class="sxs-lookup"><span data-stu-id="6ba17-205">**Warning**</span></span><br><span data-ttu-id="6ba17-206">**Informacyjny**</span><span class="sxs-lookup"><span data-stu-id="6ba17-206">**Informational**</span></span> |


##### <a name="threshold"></a><span data-ttu-id="6ba17-207">Próg</span><span class="sxs-lookup"><span data-stu-id="6ba17-207">Threshold</span></span>
<span data-ttu-id="6ba17-208">Ta sekcja jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="6ba17-208">This section is required.</span></span>  <span data-ttu-id="6ba17-209">Definiuje właściwości dla wartości progowej alertu.</span><span class="sxs-lookup"><span data-stu-id="6ba17-209">It defines the properties for the alert threshold.</span></span>

| <span data-ttu-id="6ba17-210">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="6ba17-210">Element name</span></span> | <span data-ttu-id="6ba17-211">Wymagane</span><span class="sxs-lookup"><span data-stu-id="6ba17-211">Required</span></span> | <span data-ttu-id="6ba17-212">Opis</span><span class="sxs-lookup"><span data-stu-id="6ba17-212">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="6ba17-213">Operator</span><span class="sxs-lookup"><span data-stu-id="6ba17-213">Operator</span></span> | <span data-ttu-id="6ba17-214">Tak</span><span class="sxs-lookup"><span data-stu-id="6ba17-214">Yes</span></span> | <span data-ttu-id="6ba17-215">Operator porównania z następujących wartości:</span><span class="sxs-lookup"><span data-stu-id="6ba17-215">Operator for the comparison from the following values:</span></span><br><br><span data-ttu-id="6ba17-216">**gt = większe<br>lt = mniej niż**</span><span class="sxs-lookup"><span data-stu-id="6ba17-216">**gt = greater than<br>lt = less than**</span></span> |
| <span data-ttu-id="6ba17-217">Wartość</span><span class="sxs-lookup"><span data-stu-id="6ba17-217">Value</span></span> | <span data-ttu-id="6ba17-218">Tak</span><span class="sxs-lookup"><span data-stu-id="6ba17-218">Yes</span></span> | <span data-ttu-id="6ba17-219">Wartość do porównywania wyników.</span><span class="sxs-lookup"><span data-stu-id="6ba17-219">The value to compare the results.</span></span> |


##### <a name="metricstrigger"></a><span data-ttu-id="6ba17-220">MetricsTrigger</span><span class="sxs-lookup"><span data-stu-id="6ba17-220">MetricsTrigger</span></span>
<span data-ttu-id="6ba17-221">Ta sekcja jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="6ba17-221">This section is optional.</span></span>  <span data-ttu-id="6ba17-222">Uwzględnij czynnik dla alertu metryki pomiaru.</span><span class="sxs-lookup"><span data-stu-id="6ba17-222">Include it for a metric measurement alert.</span></span>

> [!NOTE]
> <span data-ttu-id="6ba17-223">Metryki pomiaru alerty są obecnie w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="6ba17-223">Metric measurement alerts are currently in public preview.</span></span> 

| <span data-ttu-id="6ba17-224">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="6ba17-224">Element name</span></span> | <span data-ttu-id="6ba17-225">Wymagane</span><span class="sxs-lookup"><span data-stu-id="6ba17-225">Required</span></span> | <span data-ttu-id="6ba17-226">Opis</span><span class="sxs-lookup"><span data-stu-id="6ba17-226">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="6ba17-227">TriggerCondition</span><span class="sxs-lookup"><span data-stu-id="6ba17-227">TriggerCondition</span></span> | <span data-ttu-id="6ba17-228">Tak</span><span class="sxs-lookup"><span data-stu-id="6ba17-228">Yes</span></span> | <span data-ttu-id="6ba17-229">Określa, czy próg całkowitą liczbę naruszeń lub kolejnych naruszenia z następujących wartości:</span><span class="sxs-lookup"><span data-stu-id="6ba17-229">Specifies whether the threshold is for total number of breaches or consecutive breaches from the following values:</span></span><br><br><span data-ttu-id="6ba17-230">**Całkowita liczba<br>kolejnych**</span><span class="sxs-lookup"><span data-stu-id="6ba17-230">**Total<br>Consecutive**</span></span> |
| <span data-ttu-id="6ba17-231">Operator</span><span class="sxs-lookup"><span data-stu-id="6ba17-231">Operator</span></span> | <span data-ttu-id="6ba17-232">Tak</span><span class="sxs-lookup"><span data-stu-id="6ba17-232">Yes</span></span> | <span data-ttu-id="6ba17-233">Operator porównania z następujących wartości:</span><span class="sxs-lookup"><span data-stu-id="6ba17-233">Operator for the comparison from the following values:</span></span><br><br><span data-ttu-id="6ba17-234">**gt = większe<br>lt = mniej niż**</span><span class="sxs-lookup"><span data-stu-id="6ba17-234">**gt = greater than<br>lt = less than**</span></span> |
| <span data-ttu-id="6ba17-235">Wartość</span><span class="sxs-lookup"><span data-stu-id="6ba17-235">Value</span></span> | <span data-ttu-id="6ba17-236">Tak</span><span class="sxs-lookup"><span data-stu-id="6ba17-236">Yes</span></span> | <span data-ttu-id="6ba17-237">Liczba przypadków, które muszą zostać spełnione kryteria wyzwolenia alertu.</span><span class="sxs-lookup"><span data-stu-id="6ba17-237">Number of the times the criteria must be met to trigger the alert.</span></span> |

##### <a name="throttling"></a><span data-ttu-id="6ba17-238">Ograniczanie przepływności</span><span class="sxs-lookup"><span data-stu-id="6ba17-238">Throttling</span></span>
<span data-ttu-id="6ba17-239">Ta sekcja jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="6ba17-239">This section is optional.</span></span>  <span data-ttu-id="6ba17-240">W tej sekcji należy uwzględnić, jeśli chcesz pominąć alertów z tej samej reguły dla niektórych ilość czasu, po utworzeniu alertu.</span><span class="sxs-lookup"><span data-stu-id="6ba17-240">Include this section if you want to suppress alerts from the same rule for some amount of time after an alert is created.</span></span>

| <span data-ttu-id="6ba17-241">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="6ba17-241">Element name</span></span> | <span data-ttu-id="6ba17-242">Wymagane</span><span class="sxs-lookup"><span data-stu-id="6ba17-242">Required</span></span> | <span data-ttu-id="6ba17-243">Opis</span><span class="sxs-lookup"><span data-stu-id="6ba17-243">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="6ba17-244">DurationInMinutes</span><span class="sxs-lookup"><span data-stu-id="6ba17-244">DurationInMinutes</span></span> | <span data-ttu-id="6ba17-245">Tak, jeśli ograniczanie dołączony — element</span><span class="sxs-lookup"><span data-stu-id="6ba17-245">Yes if Throttling element included</span></span> | <span data-ttu-id="6ba17-246">Liczba minut do pomijania alertów po utworzeniu z tego samego alertu.</span><span class="sxs-lookup"><span data-stu-id="6ba17-246">Number of minutes to suppress alerts after one from the same alert rule is created.</span></span> |

##### <a name="emailnotification"></a><span data-ttu-id="6ba17-247">EmailNotification</span><span class="sxs-lookup"><span data-stu-id="6ba17-247">EmailNotification</span></span>
 <span data-ttu-id="6ba17-248">Ta sekcja jest opcjonalna Dołącz go, jeżeli alert do wysyłania wiadomości e-mail do co najmniej jednego adresata.</span><span class="sxs-lookup"><span data-stu-id="6ba17-248">This section is optional  Include it if you want the alert to send mail to one or more recipients.</span></span>

| <span data-ttu-id="6ba17-249">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="6ba17-249">Element name</span></span> | <span data-ttu-id="6ba17-250">Wymagane</span><span class="sxs-lookup"><span data-stu-id="6ba17-250">Required</span></span> | <span data-ttu-id="6ba17-251">Opis</span><span class="sxs-lookup"><span data-stu-id="6ba17-251">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="6ba17-252">Adresaci</span><span class="sxs-lookup"><span data-stu-id="6ba17-252">Recipients</span></span> | <span data-ttu-id="6ba17-253">Tak</span><span class="sxs-lookup"><span data-stu-id="6ba17-253">Yes</span></span> | <span data-ttu-id="6ba17-254">Rozdzielana przecinkami lista adresów e-mail, aby wysłać powiadomienie, gdy jest tworzony alert, takich jak w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="6ba17-254">Comma delimited list of email addresses to send notification when an alert is created such as in the following example.</span></span><br><br><span data-ttu-id="6ba17-255">**[ "recipient1@contoso.com", "recipient2@contoso.com" ]**</span><span class="sxs-lookup"><span data-stu-id="6ba17-255">**[ "recipient1@contoso.com", "recipient2@contoso.com" ]**</span></span> |
| <span data-ttu-id="6ba17-256">Temat</span><span class="sxs-lookup"><span data-stu-id="6ba17-256">Subject</span></span> | <span data-ttu-id="6ba17-257">Tak</span><span class="sxs-lookup"><span data-stu-id="6ba17-257">Yes</span></span> | <span data-ttu-id="6ba17-258">Wiersz tematu wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="6ba17-258">Subject line of the mail.</span></span> |
| <span data-ttu-id="6ba17-259">Załącznika</span><span class="sxs-lookup"><span data-stu-id="6ba17-259">Attachment</span></span> | <span data-ttu-id="6ba17-260">Nie</span><span class="sxs-lookup"><span data-stu-id="6ba17-260">No</span></span> | <span data-ttu-id="6ba17-261">Załączniki nie są obecnie obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="6ba17-261">Attachments are not currently supported.</span></span>  <span data-ttu-id="6ba17-262">Jeśli ten element jest włączone, należy go **Brak**.</span><span class="sxs-lookup"><span data-stu-id="6ba17-262">If this element is included, it should be **None**.</span></span> |


##### <a name="remediation"></a><span data-ttu-id="6ba17-263">Korygowania</span><span class="sxs-lookup"><span data-stu-id="6ba17-263">Remediation</span></span>
<span data-ttu-id="6ba17-264">Ta sekcja jest opcjonalna Dołącz ją, jeśli chcesz, aby element runbook można uruchomić w odpowiedzi na alert.</span><span class="sxs-lookup"><span data-stu-id="6ba17-264">This section is optional  Include it if you want a runbook to start in response to the alert.</span></span> |

| <span data-ttu-id="6ba17-265">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="6ba17-265">Element name</span></span> | <span data-ttu-id="6ba17-266">Wymagane</span><span class="sxs-lookup"><span data-stu-id="6ba17-266">Required</span></span> | <span data-ttu-id="6ba17-267">Opis</span><span class="sxs-lookup"><span data-stu-id="6ba17-267">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="6ba17-268">RunbookName</span><span class="sxs-lookup"><span data-stu-id="6ba17-268">RunbookName</span></span> | <span data-ttu-id="6ba17-269">Tak</span><span class="sxs-lookup"><span data-stu-id="6ba17-269">Yes</span></span> | <span data-ttu-id="6ba17-270">Nazwa elementu runbook, aby rozpocząć.</span><span class="sxs-lookup"><span data-stu-id="6ba17-270">Name of the runbook to start.</span></span> |
| <span data-ttu-id="6ba17-271">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="6ba17-271">WebhookUri</span></span> | <span data-ttu-id="6ba17-272">Tak</span><span class="sxs-lookup"><span data-stu-id="6ba17-272">Yes</span></span> | <span data-ttu-id="6ba17-273">Identyfikator URI elementu webhook dla elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="6ba17-273">Uri of the webhook for the runbook.</span></span> |
| <span data-ttu-id="6ba17-274">Wygaśnięcia</span><span class="sxs-lookup"><span data-stu-id="6ba17-274">Expiry</span></span> | <span data-ttu-id="6ba17-275">Nie</span><span class="sxs-lookup"><span data-stu-id="6ba17-275">No</span></span> | <span data-ttu-id="6ba17-276">Data i godzina wygaśnięcia korygowania.</span><span class="sxs-lookup"><span data-stu-id="6ba17-276">Date and time that the remediation expires.</span></span> |

#### <a name="webhook-actions"></a><span data-ttu-id="6ba17-277">Akcje elementu Webhook</span><span class="sxs-lookup"><span data-stu-id="6ba17-277">Webhook actions</span></span>

<span data-ttu-id="6ba17-278">Akcje elementu Webhook uruchomienia procesu podczas wywoływania adresu URL i opcjonalnie podając ładunku do wysłania.</span><span class="sxs-lookup"><span data-stu-id="6ba17-278">Webhook actions start a process by calling a URL and optionally providing a payload to be sent.</span></span> <span data-ttu-id="6ba17-279">Są one podobne do akcji korygowania, z wyjątkiem są przeznaczone dla elementów webhook, które może wywołać procesy inne niż elementy runbook automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="6ba17-279">They are similar to Remediation actions except they are meant for webhooks that may invoke processes other than Azure Automation runbooks.</span></span> <span data-ttu-id="6ba17-280">Zawierają także dodatkowe opcja podania ładunku mają zostać dostarczone do zdalnego procesu.</span><span class="sxs-lookup"><span data-stu-id="6ba17-280">They also provide the additional option of providing a payload to be delivered to the remote process.</span></span>

<span data-ttu-id="6ba17-281">Jeśli alert będzie wywoływać elementu webhook, a następnie konieczne będzie zasób akcji z typem **Webhook** oprócz **Alert** zasób akcji.</span><span class="sxs-lookup"><span data-stu-id="6ba17-281">If your alert will call a webhook, then it will need an action resource with a type of **Webhook** in addition to the **Alert** action resource.</span></span>  

    {
      "name": "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name, '/', variables('Webhook').Name)]",
      "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions/",
      "apiVersion": "[variables('LogAnalyticsApiVersion')]",
      "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name, '/schedules/', variables('Schedule').Name)]"
      ],
      "properties": {
        "etag": "*",
        "type": "[variables('Alert').Webhook.Type]",
        "name": "[variables('Alert').Webhook.Name]",
        "webhookUri": "[variables('Alert').Webhook.webhookUri]",
        "customPayload": "[variables('Alert').Webhook.CustomPayLoad]"
      }
    }

<span data-ttu-id="6ba17-282">Właściwości elementu Webhook akcji zasoby są opisane w poniższych tabelach.</span><span class="sxs-lookup"><span data-stu-id="6ba17-282">The properties for Webhook action resources are described in the following tables.</span></span>

| <span data-ttu-id="6ba17-283">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="6ba17-283">Element name</span></span> | <span data-ttu-id="6ba17-284">Wymagane</span><span class="sxs-lookup"><span data-stu-id="6ba17-284">Required</span></span> | <span data-ttu-id="6ba17-285">Opis</span><span class="sxs-lookup"><span data-stu-id="6ba17-285">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="6ba17-286">type</span><span class="sxs-lookup"><span data-stu-id="6ba17-286">type</span></span> | <span data-ttu-id="6ba17-287">Tak</span><span class="sxs-lookup"><span data-stu-id="6ba17-287">Yes</span></span> | <span data-ttu-id="6ba17-288">Typ akcji.</span><span class="sxs-lookup"><span data-stu-id="6ba17-288">Type of the action.</span></span>  <span data-ttu-id="6ba17-289">Są to **Webhook** dla Akcje elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="6ba17-289">This will be **Webhook** for webhook actions.</span></span> |
| <span data-ttu-id="6ba17-290">name</span><span class="sxs-lookup"><span data-stu-id="6ba17-290">name</span></span> | <span data-ttu-id="6ba17-291">Tak</span><span class="sxs-lookup"><span data-stu-id="6ba17-291">Yes</span></span> | <span data-ttu-id="6ba17-292">Nazwa wyświetlana dla akcji.</span><span class="sxs-lookup"><span data-stu-id="6ba17-292">Display name for the action.</span></span>  <span data-ttu-id="6ba17-293">Nie jest on wyświetlany w konsoli.</span><span class="sxs-lookup"><span data-stu-id="6ba17-293">This is not displayed in the console.</span></span> |
| <span data-ttu-id="6ba17-294">wehookUri</span><span class="sxs-lookup"><span data-stu-id="6ba17-294">wehookUri</span></span> | <span data-ttu-id="6ba17-295">Tak</span><span class="sxs-lookup"><span data-stu-id="6ba17-295">Yes</span></span> | <span data-ttu-id="6ba17-296">Identyfikator URI dla elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="6ba17-296">Uri for the webhook.</span></span> |
| <span data-ttu-id="6ba17-297">CustomPayload</span><span class="sxs-lookup"><span data-stu-id="6ba17-297">customPayload</span></span> | <span data-ttu-id="6ba17-298">Nie</span><span class="sxs-lookup"><span data-stu-id="6ba17-298">No</span></span> | <span data-ttu-id="6ba17-299">Niestandardowy ładunek do wysłania do elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="6ba17-299">Custom payload to be sent to the webhook.</span></span> <span data-ttu-id="6ba17-300">Format będzie zależeć od tego, czego oczekuje elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="6ba17-300">The format will depend on what the webhook is expecting.</span></span> |




## <a name="sample"></a><span data-ttu-id="6ba17-301">Przykład</span><span class="sxs-lookup"><span data-stu-id="6ba17-301">Sample</span></span>

<span data-ttu-id="6ba17-302">Poniżej przedstawiono przykładowe rozwiązanie obejmujące obejmuje następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="6ba17-302">Following is a sample of a solution that include that includes the following resources:</span></span>

- <span data-ttu-id="6ba17-303">Zapisane wyszukiwanie</span><span class="sxs-lookup"><span data-stu-id="6ba17-303">Saved search</span></span>
- <span data-ttu-id="6ba17-304">Harmonogram</span><span class="sxs-lookup"><span data-stu-id="6ba17-304">Schedule</span></span>
- <span data-ttu-id="6ba17-305">Akcji alertu</span><span class="sxs-lookup"><span data-stu-id="6ba17-305">Alert action</span></span>
- <span data-ttu-id="6ba17-306">Akcja elementu Webhook</span><span class="sxs-lookup"><span data-stu-id="6ba17-306">Webhook action</span></span>

<span data-ttu-id="6ba17-307">W przykładzie użyto [parametry standardowego rozwiązania](operations-management-suite-solutions-solution-file.md#parameters) zmiennych, które służy zwykle do rozwiązania, w przeciwieństwie do wartości hardcoding w definicji zasobu.</span><span class="sxs-lookup"><span data-stu-id="6ba17-307">The sample uses [standard solution parameters](operations-management-suite-solutions-solution-file.md#parameters) variables that would commonly be used in a solution as opposed to hardcoding values in the resource definitions.</span></span>

    {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0",
        "parameters": {
          "workspaceName": {
            "type": "string",
            "metadata": {
              "Description": "Name of Log Analytics workspace"
            }
          },
          "accountName": {
            "type": "string",
            "metadata": {
              "Description": "Name of Automation account"
            }
          },
          "workspaceregionId": {
            "type": "string",
            "metadata": {
              "Description": "Region of Log Analytics workspace"
            }
          },
          "regionId": {
            "type": "string",
            "metadata": {
              "Description": "Region of Automation account"
            }
          },
          "pricingTier": {
            "type": "string",
            "metadata": {
              "Description": "Pricing tier of both Log Analytics workspace and Azure Automation account"
            }
          },
          "recipients": {
            "type": "string",
            "metadata": {
              "Description": "List of recipients for the email alert separated by semicolon"
            }
          }
        },
        "variables": {
          "SolutionName": "MySolution",
          "SolutionVersion": "1.0",
          "SolutionPublisher": "Contoso",
          "ProductName": "SampleSolution",
    
          "LogAnalyticsApiVersion": "2015-11-01-preview",
    
          "MySearch": {
            "displayName": "Error records by hour",
            "query": "Type=MyRecord_CL | measure avg(Rating_d) by Instance_s interval 60minutes",
            "category": "Samples",
            "name": "Samples-Count of data"
          },
          "MyAlert": {
            "Name": "[toLower(concat('myalert-',uniqueString(resourceGroup().id, deployment().name)))]",
            "DisplayName": "My alert rule",
            "Description": "Sample alert.  Fires when 3 error records found over hour interval.",
            "Severity": "Critical",
            "ThresholdOperator": "gt",
            "ThresholdValue": 3,
            "Schedule": {
              "Name": "[toLower(concat('myschedule-',uniqueString(resourceGroup().id, deployment().name)))]",
              "Interval": 15,
              "TimeSpan": 60
            },
            "MetricsTrigger": {
              "TriggerCondition": "Consecutive",
              "Operator": "gt",
              "Value": 3
            },
            "ThrottleMinutes": 60,
            "Notification": {
              "Recipients": [
                "[parameters('recipients')]"
              ],
              "Subject": "Sample alert"
            },
            "Remediation": {
              "RunbookName": "MyRemediationRunbook",
              "WebhookUri": "https://s1events.azure-automation.net/webhooks?token=TluBFH3GpX4IEAnFoImoAWLTULkjD%2bTS0yscyrr7ogw%3d"
            },
            "Webhook": {
              "Name": "MyWebhook",
              "Uri": "https://MyService.com/webhook",
              "Payload": "{\"field1\":\"value1\",\"field2\":\"value2\"}"
            }
          }
        },
        "resources": [
          {
            "name": "[concat(variables('SolutionName'), '[' ,parameters('workspacename'), ']')]",
            "location": "[parameters('workspaceRegionId')]",
            "tags": { },
            "type": "Microsoft.OperationsManagement/solutions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches', parameters('workspacename'), variables('MySearch').Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Webhook.Name)]"
            ],
            "properties": {
              "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
              "referencedResources": [
              ],
              "containedResources": [
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches', parameters('workspacename'), variables('MySearch').Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Webhook.Name)]"
              ]
            },
            "plan": {
              "name": "[concat(variables('SolutionName'), '[' ,parameters('workspaceName'), ']')]",
              "Version": "[variables('SolutionVersion')]",
              "product": "[variables('ProductName')]",
              "publisher": "[variables('SolutionPublisher')]",
              "promotionCode": ""
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [ ],
            "tags": { },
            "properties": {
              "etag": "*",
              "query": "[variables('MySearch').query]",
              "displayName": "[variables('MySearch').displayName]",
              "category": "[variables('MySearch').category]"
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/', variables('MyAlert').Schedule.Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name)]"
            ],
            "properties": {
              "etag": "*",
              "interval": "[variables('MyAlert').Schedule.Interval]",
              "queryTimeSpan": "[variables('MyAlert').Schedule.TimeSpan]",
              "enabled": true
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/',  variables('MyAlert').Schedule.Name, '/',  variables('MyAlert').Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/',  variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name)]"
            ],
            "properties": {
              "etag": "*",
              "Type": "Alert",
              "Name": "[variables('MyAlert').DisplayName]",
              "Description": "[variables('MyAlert').Description]",
              "Severity": "[variables('MyAlert').Severity]",
              "Threshold": {
                "Operator": "[variables('MyAlert').ThresholdOperator]",
                "Value": "[variables('MyAlert').ThresholdValue]",
                "MetricsTrigger": {
                  "TriggerCondition": "[variables('MyAlert').MetricsTrigger.TriggerCondition]",
                  "Operator": "[variables('MyAlert').MetricsTrigger.Operator]",
                  "Value": "[variables('MyAlert').MetricsTrigger.Value]"
                }
              },
              "Throttling": {
                "DurationInMinutes": "[variables('MyAlert').ThrottleMinutes]"
              },
              "EmailNotification": {
                "Recipients": "[variables('MyAlert').Notification.Recipients]",
                "Subject": "[variables('MyAlert').Notification.Subject]",
                "Attachment": "None"
              },
              "Remediation": {
                "RunbookName": "[variables('MyAlert').Remediation.RunbookName]",
                "WebhookUri": "[variables('MyAlert').Remediation.WebhookUri]"
              }
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/', variables('MyAlert').Schedule.Name, '/', variables('MyAlert').Webhook.Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name)]",
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name, '/actions/',variables('MyAlert').Name)]"
            ],
            "properties": {
              "etag": "*",
              "Type": "Webhook",
              "Name": "[variables('MyAlert').Webhook.Name]",
              "WebhookUri": "[variables('MyAlert').Webhook.Uri]",
              "CustomPayload": "[variables('MyAlert').Webhook.Payload]"
            }
          }
        ]
    }


<span data-ttu-id="6ba17-308">Następujący plik parametrów zawiera przykłady wartości dla tego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="6ba17-308">The following parameter file provides samples values for this solution.</span></span>

    {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "workspacename": {
                "value": "myWorkspace"
            },
            "accountName": {
                "value": "myAccount"
            },
            "workspaceregionId": {
                "value": "East US"
            },
            "regionId": {
                "value": "East US 2"
            },
            "pricingTier": {
                "value": "Free"
            },
            "recipients": {
                "value": "recipient1@contoso.com;recipient2@contoso.com"
            }
        }
    }


## <a name="next-steps"></a><span data-ttu-id="6ba17-309">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6ba17-309">Next steps</span></span>
* <span data-ttu-id="6ba17-310">[Dodawanie widoków](operations-management-suite-solutions-resources-views.md) do rozwiązania do zarządzania.</span><span class="sxs-lookup"><span data-stu-id="6ba17-310">[Add views](operations-management-suite-solutions-resources-views.md) to your management solution.</span></span>
* <span data-ttu-id="6ba17-311">[Dodaj element runbook usługi Automatyzacja i innych zasobów](operations-management-suite-solutions-resources-automation.md) do rozwiązania do zarządzania.</span><span class="sxs-lookup"><span data-stu-id="6ba17-311">[Add Automation runbooks and other resources](operations-management-suite-solutions-resources-automation.md) to your management solution.</span></span>

