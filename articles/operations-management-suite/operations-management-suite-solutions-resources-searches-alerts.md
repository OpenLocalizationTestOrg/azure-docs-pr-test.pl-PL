---
title: "aaaSaved wyszukiwania i alertów w rozwiązaniach pakietu OMS | Dokumentacja firmy Microsoft"
description: "W analizy dzienników tooanalyze danych zbieranych przez rozwiązanie hello rozwiązań w OMS zazwyczaj uwzględnia zapisane wyszukiwania.  Mogą również definiować alerty toonotify hello użytkownika lub automatyczne wykonywanie akcji w problem krytyczny tooa odpowiedzi.  W tym artykule opisano, jak toodefine analizy dzienników zapisane wyszukiwania i alertów w szablonu usługi ARM, aby mogły one zostać uwzględnione w rozwiązaniach do zarządzania."
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
ms.openlocfilehash: 93d7c5bbf061473833ca6c0a8e4d8e10d923f3ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="adding-log-analytics-saved-searches-and-alerts-toooms-management-solution-preview"></a><span data-ttu-id="f9eba-105">Dodawanie analizy dzienników zapisane wyszukiwania i alerty tooOMS rozwiązania do zarządzania (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="f9eba-105">Adding Log Analytics saved searches and alerts tooOMS management solution (Preview)</span></span>

> [!NOTE]
> <span data-ttu-id="f9eba-106">To jest wstępna dokumentacji do tworzenia rozwiązań do zarządzania w OMS, które są obecnie w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="f9eba-106">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="f9eba-107">Żadnego schematu opisanych poniżej jest toochange podmiotu.</span><span class="sxs-lookup"><span data-stu-id="f9eba-107">Any schema described below is subject toochange.</span></span>   


<span data-ttu-id="f9eba-108">[Rozwiązania do zarządzania w OMS](operations-management-suite-solutions.md) zazwyczaj uwzględnia [zapisane wyszukiwania](../log-analytics/log-analytics-log-searches.md) analizy dzienników tooanalyze danych zbieranych przez hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f9eba-108">[Management solutions in OMS](operations-management-suite-solutions.md) will typically include [saved searches](../log-analytics/log-analytics-log-searches.md) in Log Analytics tooanalyze data collected by hello solution.</span></span>  <span data-ttu-id="f9eba-109">Mogą również określić [alerty](../log-analytics/log-analytics-alerts.md) toonotify hello użytkownika lub automatyczne wykonywanie akcji w problem krytyczny tooa odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="f9eba-109">They may also define [alerts](../log-analytics/log-analytics-alerts.md) toonotify hello user or automatically take action in response tooa critical issue.</span></span>  <span data-ttu-id="f9eba-110">W tym artykule opisano, jak toodefine analizy dzienników zapisane wyszukiwania i alertach w [szablonu zarządzanie zasobami](../resource-manager-template-walkthrough.md) aby mogły one zostać uwzględnione w [rozwiązań do zarządzania](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="f9eba-110">This article describes how toodefine Log Analytics saved searches and alerts in a [Resource Management template](../resource-manager-template-walkthrough.md) so they can be included in [management solutions](operations-management-suite-solutions-creating.md).</span></span>

> [!NOTE]
> <span data-ttu-id="f9eba-111">cześć przykłady w tym artykule Użyj parametry i zmienne, które są albo toomanagement wymagane lub typowych rozwiązań i opisane w [tworzenia rozwiązań do zarządzania w Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span><span class="sxs-lookup"><span data-stu-id="f9eba-111">hello samples in this article use parameters and variables that are either required or common toomanagement solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="f9eba-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f9eba-112">Prerequisites</span></span>
<span data-ttu-id="f9eba-113">W tym artykule przyjęto założenie, że znasz już jak zbyt[tworzenie rozwiązania do zarządzania](operations-management-suite-solutions-creating.md) i struktura hello [szablon ARM](../resource-group-authoring-templates.md) i plik rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f9eba-113">This article assumes that you're already familiar with how too[create a management solution](operations-management-suite-solutions-creating.md) and hello structure of an [ARM template](../resource-group-authoring-templates.md) and solution file.</span></span>


## <a name="log-analytics-workspace"></a><span data-ttu-id="f9eba-114">Obszar roboczy analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="f9eba-114">Log Analytics Workspace</span></span>
<span data-ttu-id="f9eba-115">Wszystkie zasoby w analizy dzienników znajdują się w [obszaru roboczego](../log-analytics/log-analytics-manage-access.md).</span><span class="sxs-lookup"><span data-stu-id="f9eba-115">All resources in Log Analytics are contained in a [workspace](../log-analytics/log-analytics-manage-access.md).</span></span>  <span data-ttu-id="f9eba-116">Zgodnie z opisem w [OMS obszaru roboczego i konto automatyzacji](operations-management-suite-solutions.md#oms-workspace-and-automation-account) hello obszaru roboczego nie jest zawarty w rozwiązaniu do zarządzania hello, ale musi istnieć przed zainstalowaniem hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f9eba-116">As described in [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) hello workspace isn't included in hello management solution but must exist before hello solution is installed.</span></span>  <span data-ttu-id="f9eba-117">Jeśli nie jest dostępna, następnie hello rozwiązania instalacja zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="f9eba-117">If it isn't available, then hello solution install will fail.</span></span>

<span data-ttu-id="f9eba-118">Nazwa Hello obszaru roboczego hello jest nazwa hello każdego zasobu analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="f9eba-118">hello name of hello workspace is in hello name of each Log Analytics resource.</span></span>  <span data-ttu-id="f9eba-119">Odbywa się w rozwiązaniu hello hello **obszaru roboczego** parametru jak hello poniższy przykład savedsearch zasobu.</span><span class="sxs-lookup"><span data-stu-id="f9eba-119">This is done in hello solution with hello **workspace** parameter as in hello following example of a savedsearch resource.</span></span>

    "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearchId'))]"


## <a name="saved-searches"></a><span data-ttu-id="f9eba-120">Zapisane wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="f9eba-120">Saved Searches</span></span>
<span data-ttu-id="f9eba-121">Obejmują [zapisane wyszukiwania](../log-analytics/log-analytics-log-searches.md) rozwiązania tooallow użytkowników tooquery danych zbieranych przez rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f9eba-121">Include [saved searches](../log-analytics/log-analytics-log-searches.md) in a solution tooallow users tooquery data collected by your solution.</span></span>  <span data-ttu-id="f9eba-122">Zapisane wyszukiwania zostanie wyświetlony w obszarze **ulubione** w portalu OMS hello i **zapisane wyszukiwania** w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f9eba-122">Saved searches will appear under **Favorites** in hello OMS portal and **Saved Searches** in hello Azure portal .</span></span>  <span data-ttu-id="f9eba-123">Zapisane wyszukiwanie jest również wymagany dla każdego alertu.</span><span class="sxs-lookup"><span data-stu-id="f9eba-123">A saved search is also required for each alert.</span></span>   

<span data-ttu-id="f9eba-124">[Analiza dzienników zapisanego wyszukiwania](../log-analytics/log-analytics-log-searches.md) zasobów mieć typu `Microsoft.OperationalInsights/workspaces/savedSearches` i mieć hello następujące struktury.</span><span class="sxs-lookup"><span data-stu-id="f9eba-124">[Log Analytics saved search](../log-analytics/log-analytics-log-searches.md) resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches` and have hello following structure.</span></span>  <span data-ttu-id="f9eba-125">W tym wspólnych zmiennych i parametrów, aby mogli skopiuj i wklej następujący fragment kodu w pliku rozwiązania i Zmień nazwy parametrów hello.</span><span class="sxs-lookup"><span data-stu-id="f9eba-125">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

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



<span data-ttu-id="f9eba-126">Każdej z właściwości hello zapisanego kryterium wyszukiwania są opisane w hello w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="f9eba-126">Each of hello properties of a saved search are described in hello following table.</span></span> 

| <span data-ttu-id="f9eba-127">Właściwość</span><span class="sxs-lookup"><span data-stu-id="f9eba-127">Property</span></span> | <span data-ttu-id="f9eba-128">Opis</span><span class="sxs-lookup"><span data-stu-id="f9eba-128">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="f9eba-129">category</span><span class="sxs-lookup"><span data-stu-id="f9eba-129">category</span></span> | <span data-ttu-id="f9eba-130">Kategoria Hello hello zapisanego kryterium wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="f9eba-130">hello category for hello saved search.</span></span>  <span data-ttu-id="f9eba-131">Dowolne zapisane wyszukiwania w powitalne tego samego rozwiązania często muszą współdzielić jednej kategorii, są pogrupowane w hello konsoli.</span><span class="sxs-lookup"><span data-stu-id="f9eba-131">Any saved searches in hello same solution will often share a single category so they are grouped together in hello console.</span></span> |
| <span data-ttu-id="f9eba-132">Nazwa wyświetlana</span><span class="sxs-lookup"><span data-stu-id="f9eba-132">displayname</span></span> | <span data-ttu-id="f9eba-133">Nazwa toodisplay dla hello zapisane wyszukiwanie w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="f9eba-133">Name toodisplay for hello saved search in hello portal.</span></span> |
| <span data-ttu-id="f9eba-134">query</span><span class="sxs-lookup"><span data-stu-id="f9eba-134">query</span></span> | <span data-ttu-id="f9eba-135">Toorun zapytania.</span><span class="sxs-lookup"><span data-stu-id="f9eba-135">Query toorun.</span></span> |

> [!NOTE]
> <span data-ttu-id="f9eba-136">Znaki specjalne toouse w zapytaniu hello może być konieczne, jeśli zawiera znaki, które mogą być interpretowane jako JSON.</span><span class="sxs-lookup"><span data-stu-id="f9eba-136">You may need toouse escape characters in hello query if it includes characters that could be interpreted as JSON.</span></span>  <span data-ttu-id="f9eba-137">Na przykład, jeśli zapytanie zostało **OperationName:"Microsoft.Compute/virtualMachines/write typu: AzureActivity"**, mają być zapisywane w pliku rozwiązania hello jako **OperationName typu: AzureActivity:\" Microsoft.Compute/virtualMachines/write\"**.</span><span class="sxs-lookup"><span data-stu-id="f9eba-137">For example, if your query was **Type:AzureActivity OperationName:"Microsoft.Compute/virtualMachines/write"**, it should be written in hello solution file as **Type:AzureActivity OperationName:\"Microsoft.Compute/virtualMachines/write\"**.</span></span>

## <a name="alerts"></a><span data-ttu-id="f9eba-138">Alerty</span><span class="sxs-lookup"><span data-stu-id="f9eba-138">Alerts</span></span>
<span data-ttu-id="f9eba-139">[Rejestrowania alertów Analytics](../log-analytics/log-analytics-alerts.md) są tworzone przez reguły alertów, które uruchomić zapisane wyszukiwanie w regularnych odstępach czasu.</span><span class="sxs-lookup"><span data-stu-id="f9eba-139">[Log Analytics alerts](../log-analytics/log-analytics-alerts.md) are created by alert rules that run a saved search on a regular interval.</span></span>  <span data-ttu-id="f9eba-140">Jeśli hello wyników zapytania hello spełniających określone kryteria, tworzony jest rekord alertów i są uruchamiane co najmniej jednej akcji.</span><span class="sxs-lookup"><span data-stu-id="f9eba-140">If hello results of hello query match specified criteria, an alert record is created and one or more actions are run.</span></span>  

<span data-ttu-id="f9eba-141">Reguły alertów w rozwiązaniu do zarządzania składają się z hello następujące trzy różne zasoby.</span><span class="sxs-lookup"><span data-stu-id="f9eba-141">Alert rules in a management solution are made up of hello following three different resources.</span></span>

- <span data-ttu-id="f9eba-142">**Zapisane wyszukiwanie.**</span><span class="sxs-lookup"><span data-stu-id="f9eba-142">**Saved search.**</span></span>  <span data-ttu-id="f9eba-143">Definiuje hello dziennik wyszukiwania, które będą uruchamiane.</span><span class="sxs-lookup"><span data-stu-id="f9eba-143">Defines hello log search that will be run.</span></span>  <span data-ttu-id="f9eba-144">Wiele reguł alertów można udostępniać pojedynczy zapisanego kryterium wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="f9eba-144">Multiple alert rules can share a single saved search.</span></span>
- <span data-ttu-id="f9eba-145">**Harmonogram.**</span><span class="sxs-lookup"><span data-stu-id="f9eba-145">**Schedule.**</span></span>  <span data-ttu-id="f9eba-146">Określa, jak często hello wyszukiwania dziennika zostanie uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="f9eba-146">Defines how often hello log search will be run.</span></span>  <span data-ttu-id="f9eba-147">Każdej reguły alertu będzie mieć tylko jeden harmonogram.</span><span class="sxs-lookup"><span data-stu-id="f9eba-147">Each alert rule will have one and only one schedule.</span></span>
- <span data-ttu-id="f9eba-148">**Akcja alertu.**</span><span class="sxs-lookup"><span data-stu-id="f9eba-148">**Alert action.**</span></span>  <span data-ttu-id="f9eba-149">Każdej reguły alertu będzie mieć jeden zasób akcji z typem **Alert** definiuje hello szczegóły alertu hello, takich jak kryteria hello rekord alertu zostanie utworzony po hello ważność alertu.</span><span class="sxs-lookup"><span data-stu-id="f9eba-149">Each alert rule will have one action resource with a type of **Alert** that defines hello details of hello alert such as hello criteria for when an alert record will be created and hello alert's severity.</span></span>  <span data-ttu-id="f9eba-150">zasób akcji Hello opcjonalnie definiują odpowiedzi poczty i elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="f9eba-150">hello action resource will optionally define a mail and runbook response.</span></span>
- <span data-ttu-id="f9eba-151">**Akcja elementu Webhook (opcjonalnie).**</span><span class="sxs-lookup"><span data-stu-id="f9eba-151">**Webhook action (optional).**</span></span>  <span data-ttu-id="f9eba-152">Reguła alertu hello wywoła elementu webhook, a następnie go wymaga dodatkowych czynności zasobu o typie **Webhook**.</span><span class="sxs-lookup"><span data-stu-id="f9eba-152">If hello alert rule will call a webhook, then it requires an additional action resource with a type of **Webhook**.</span></span>    

<span data-ttu-id="f9eba-153">Zapisane wyszukiwania zasobów opisanych powyżej.</span><span class="sxs-lookup"><span data-stu-id="f9eba-153">Saved search resources are described above.</span></span>  <span data-ttu-id="f9eba-154">Witaj inne zasoby są opisane poniżej.</span><span class="sxs-lookup"><span data-stu-id="f9eba-154">hello other resources are described below.</span></span>


### <a name="schedule-resource"></a><span data-ttu-id="f9eba-155">Zasób harmonogramu</span><span class="sxs-lookup"><span data-stu-id="f9eba-155">Schedule resource</span></span>

<span data-ttu-id="f9eba-156">Zapisane wyszukiwanie może mieć co najmniej jeden harmonogram z każdym harmonogramem reprezentujący oddzielne reguły alertu.</span><span class="sxs-lookup"><span data-stu-id="f9eba-156">A saved search can have one or more schedules with each schedule representing a separate alert rule.</span></span> <span data-ttu-id="f9eba-157">Hello harmonogram Określa częstotliwość hello wyszukiwania jest uruchamiany i hello interwał czasu, przez które hello dane są pobierane.</span><span class="sxs-lookup"><span data-stu-id="f9eba-157">hello schedule defines how often hello search is run and hello time interval over which hello data is retrieved.</span></span>  <span data-ttu-id="f9eba-158">Planowanie zasobów mieć typu `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/` i mieć hello następujące struktury.</span><span class="sxs-lookup"><span data-stu-id="f9eba-158">Schedule resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/` and have hello following structure.</span></span> <span data-ttu-id="f9eba-159">W tym wspólnych zmiennych i parametrów, aby mogli skopiuj i wklej następujący fragment kodu w pliku rozwiązania i Zmień nazwy parametrów hello.</span><span class="sxs-lookup"><span data-stu-id="f9eba-159">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 


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



<span data-ttu-id="f9eba-160">w hello w poniższej tabeli opisano Hello właściwości harmonogramu zasobów.</span><span class="sxs-lookup"><span data-stu-id="f9eba-160">hello properties for schedule resources are described in hello following table.</span></span>

| <span data-ttu-id="f9eba-161">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="f9eba-161">Element name</span></span> | <span data-ttu-id="f9eba-162">Wymagane</span><span class="sxs-lookup"><span data-stu-id="f9eba-162">Required</span></span> | <span data-ttu-id="f9eba-163">Opis</span><span class="sxs-lookup"><span data-stu-id="f9eba-163">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="f9eba-164">włączone</span><span class="sxs-lookup"><span data-stu-id="f9eba-164">enabled</span></span>       | <span data-ttu-id="f9eba-165">Tak</span><span class="sxs-lookup"><span data-stu-id="f9eba-165">Yes</span></span> | <span data-ttu-id="f9eba-166">Określa, czy hello alert jest włączony podczas jego tworzenia.</span><span class="sxs-lookup"><span data-stu-id="f9eba-166">Specifies whether hello alert is enabled when it's created.</span></span> |
| <span data-ttu-id="f9eba-167">interval</span><span class="sxs-lookup"><span data-stu-id="f9eba-167">interval</span></span>      | <span data-ttu-id="f9eba-168">Tak</span><span class="sxs-lookup"><span data-stu-id="f9eba-168">Yes</span></span> | <span data-ttu-id="f9eba-169">Jak często hello zapytania jest uruchamiany w minutach.</span><span class="sxs-lookup"><span data-stu-id="f9eba-169">How often hello query runs in minutes.</span></span> |
| <span data-ttu-id="f9eba-170">QueryTimeSpan</span><span class="sxs-lookup"><span data-stu-id="f9eba-170">queryTimeSpan</span></span> | <span data-ttu-id="f9eba-171">Tak</span><span class="sxs-lookup"><span data-stu-id="f9eba-171">Yes</span></span> | <span data-ttu-id="f9eba-172">Długość czasu w minutach, przez które wyniki tooevaluate.</span><span class="sxs-lookup"><span data-stu-id="f9eba-172">Length of time in minutes over which tooevaluate results.</span></span> |

<span data-ttu-id="f9eba-173">zasób harmonogramu Hello powinien zależą od hello zapisanego wyszukiwania, dzięki czemu jest tworzona przed hello harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="f9eba-173">hello schedule resource should depend on hello saved search so that it's created before hello schedule.</span></span>


### <a name="actions"></a><span data-ttu-id="f9eba-174">Akcje</span><span class="sxs-lookup"><span data-stu-id="f9eba-174">Actions</span></span>
<span data-ttu-id="f9eba-175">Istnieją dwa typy akcji zasobu określonego przez hello **typu** właściwości.</span><span class="sxs-lookup"><span data-stu-id="f9eba-175">There are two types of action resource specified by hello **Type** property.</span></span>  <span data-ttu-id="f9eba-176">Harmonogram wymaga jednego **Alert** akcji, który definiuje szczegóły hello hello reguły alertów i jakie akcje są pobierane, gdy alert jest tworzony.</span><span class="sxs-lookup"><span data-stu-id="f9eba-176">A schedule requires one **Alert** action which defines hello details of hello alert rule and what actions are taken when an alert is created.</span></span>  <span data-ttu-id="f9eba-177">Mogą również obejmować **Webhook** akcji, o ile elementu webhook powinna być wywoływana z hello alertu.</span><span class="sxs-lookup"><span data-stu-id="f9eba-177">It may also include a **Webhook** action if a webhook should be called from hello alert.</span></span>  

<span data-ttu-id="f9eba-178">Zasoby akcji mieć typu `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions`.</span><span class="sxs-lookup"><span data-stu-id="f9eba-178">Action resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions`.</span></span>  

#### <a name="alert-actions"></a><span data-ttu-id="f9eba-179">Akcje alertów</span><span class="sxs-lookup"><span data-stu-id="f9eba-179">Alert actions</span></span>

<span data-ttu-id="f9eba-180">Każdy harmonogram będzie mieć jeden **alertu** akcji.</span><span class="sxs-lookup"><span data-stu-id="f9eba-180">Every schedule will have one **Alert** action.</span></span>  <span data-ttu-id="f9eba-181">Określa szczegóły hello hello alert, oraz opcjonalnie powiadomień i korygowania akcji.</span><span class="sxs-lookup"><span data-stu-id="f9eba-181">This defines hello details of hello alert and optionally notification and remediation actions.</span></span>  <span data-ttu-id="f9eba-182">Powiadomienie o wysyła tooone poczty e-mail lub więcej adresów.</span><span class="sxs-lookup"><span data-stu-id="f9eba-182">A notification sends an email tooone or more addresses.</span></span>  <span data-ttu-id="f9eba-183">Korygowanie uruchamia element runbook w automatyzacji Azure tooattempt tooremediate hello wykrył problem.</span><span class="sxs-lookup"><span data-stu-id="f9eba-183">A remediation starts a runbook in Azure Automation tooattempt tooremediate hello detected issue.</span></span>

<span data-ttu-id="f9eba-184">Akcje alertu ma hello następujące struktury.</span><span class="sxs-lookup"><span data-stu-id="f9eba-184">Alert actions have hello following structure.</span></span>  <span data-ttu-id="f9eba-185">W tym wspólnych zmiennych i parametrów, aby mogli skopiuj i wklej następujący fragment kodu w pliku rozwiązania i Zmień nazwy parametrów hello.</span><span class="sxs-lookup"><span data-stu-id="f9eba-185">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 



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

<span data-ttu-id="f9eba-186">Hello właściwości zasobów akcji alertu są opisane w następujących tabel hello.</span><span class="sxs-lookup"><span data-stu-id="f9eba-186">hello properties for Alert action resources are described in hello following tables.</span></span>

| <span data-ttu-id="f9eba-187">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="f9eba-187">Element name</span></span> | <span data-ttu-id="f9eba-188">Wymagane</span><span class="sxs-lookup"><span data-stu-id="f9eba-188">Required</span></span> | <span data-ttu-id="f9eba-189">Opis</span><span class="sxs-lookup"><span data-stu-id="f9eba-189">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="f9eba-190">Typ</span><span class="sxs-lookup"><span data-stu-id="f9eba-190">Type</span></span> | <span data-ttu-id="f9eba-191">Tak</span><span class="sxs-lookup"><span data-stu-id="f9eba-191">Yes</span></span> | <span data-ttu-id="f9eba-192">Typ akcji hello.</span><span class="sxs-lookup"><span data-stu-id="f9eba-192">Type of hello action.</span></span>  <span data-ttu-id="f9eba-193">Są to **Alert** dla akcje alertu.</span><span class="sxs-lookup"><span data-stu-id="f9eba-193">This will be **Alert** for alert actions.</span></span> |
| <span data-ttu-id="f9eba-194">Nazwa</span><span class="sxs-lookup"><span data-stu-id="f9eba-194">Name</span></span> | <span data-ttu-id="f9eba-195">Tak</span><span class="sxs-lookup"><span data-stu-id="f9eba-195">Yes</span></span> | <span data-ttu-id="f9eba-196">Nazwa wyświetlana hello alertu.</span><span class="sxs-lookup"><span data-stu-id="f9eba-196">Display name for hello alert.</span></span>  <span data-ttu-id="f9eba-197">Jest to nazwa hello, która jest wyświetlana w konsoli hello hello reguły alertów.</span><span class="sxs-lookup"><span data-stu-id="f9eba-197">This is hello name that's displayed in hello console for hello alert rule.</span></span> |
| <span data-ttu-id="f9eba-198">Opis</span><span class="sxs-lookup"><span data-stu-id="f9eba-198">Description</span></span> | <span data-ttu-id="f9eba-199">Nie</span><span class="sxs-lookup"><span data-stu-id="f9eba-199">No</span></span> | <span data-ttu-id="f9eba-200">Opcjonalny opis hello alertu.</span><span class="sxs-lookup"><span data-stu-id="f9eba-200">Optional description of hello alert.</span></span> |
| <span data-ttu-id="f9eba-201">Ważność</span><span class="sxs-lookup"><span data-stu-id="f9eba-201">Severity</span></span> | <span data-ttu-id="f9eba-202">Tak</span><span class="sxs-lookup"><span data-stu-id="f9eba-202">Yes</span></span> | <span data-ttu-id="f9eba-203">Ważność alertu rekordu hello z hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="f9eba-203">Severity of hello alert record from hello following values:</span></span><br><br> <span data-ttu-id="f9eba-204">**Krytyczne**</span><span class="sxs-lookup"><span data-stu-id="f9eba-204">**Critical**</span></span><br><span data-ttu-id="f9eba-205">**Ostrzeżenie**</span><span class="sxs-lookup"><span data-stu-id="f9eba-205">**Warning**</span></span><br><span data-ttu-id="f9eba-206">**Informacyjny**</span><span class="sxs-lookup"><span data-stu-id="f9eba-206">**Informational**</span></span> |


##### <a name="threshold"></a><span data-ttu-id="f9eba-207">Próg</span><span class="sxs-lookup"><span data-stu-id="f9eba-207">Threshold</span></span>
<span data-ttu-id="f9eba-208">Ta sekcja jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="f9eba-208">This section is required.</span></span>  <span data-ttu-id="f9eba-209">Definiuje właściwości hello hello próg alertu.</span><span class="sxs-lookup"><span data-stu-id="f9eba-209">It defines hello properties for hello alert threshold.</span></span>

| <span data-ttu-id="f9eba-210">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="f9eba-210">Element name</span></span> | <span data-ttu-id="f9eba-211">Wymagane</span><span class="sxs-lookup"><span data-stu-id="f9eba-211">Required</span></span> | <span data-ttu-id="f9eba-212">Opis</span><span class="sxs-lookup"><span data-stu-id="f9eba-212">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="f9eba-213">Operator</span><span class="sxs-lookup"><span data-stu-id="f9eba-213">Operator</span></span> | <span data-ttu-id="f9eba-214">Tak</span><span class="sxs-lookup"><span data-stu-id="f9eba-214">Yes</span></span> | <span data-ttu-id="f9eba-215">Operator porównania hello z hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="f9eba-215">Operator for hello comparison from hello following values:</span></span><br><br><span data-ttu-id="f9eba-216">**gt = większe<br>lt = mniej niż**</span><span class="sxs-lookup"><span data-stu-id="f9eba-216">**gt = greater than<br>lt = less than**</span></span> |
| <span data-ttu-id="f9eba-217">Wartość</span><span class="sxs-lookup"><span data-stu-id="f9eba-217">Value</span></span> | <span data-ttu-id="f9eba-218">Tak</span><span class="sxs-lookup"><span data-stu-id="f9eba-218">Yes</span></span> | <span data-ttu-id="f9eba-219">Witaj wartość toocompare hello wyniki.</span><span class="sxs-lookup"><span data-stu-id="f9eba-219">hello value toocompare hello results.</span></span> |


##### <a name="metricstrigger"></a><span data-ttu-id="f9eba-220">MetricsTrigger</span><span class="sxs-lookup"><span data-stu-id="f9eba-220">MetricsTrigger</span></span>
<span data-ttu-id="f9eba-221">Ta sekcja jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="f9eba-221">This section is optional.</span></span>  <span data-ttu-id="f9eba-222">Uwzględnij czynnik dla alertu metryki pomiaru.</span><span class="sxs-lookup"><span data-stu-id="f9eba-222">Include it for a metric measurement alert.</span></span>

> [!NOTE]
> <span data-ttu-id="f9eba-223">Metryki pomiaru alerty są obecnie w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="f9eba-223">Metric measurement alerts are currently in public preview.</span></span> 

| <span data-ttu-id="f9eba-224">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="f9eba-224">Element name</span></span> | <span data-ttu-id="f9eba-225">Wymagane</span><span class="sxs-lookup"><span data-stu-id="f9eba-225">Required</span></span> | <span data-ttu-id="f9eba-226">Opis</span><span class="sxs-lookup"><span data-stu-id="f9eba-226">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="f9eba-227">TriggerCondition</span><span class="sxs-lookup"><span data-stu-id="f9eba-227">TriggerCondition</span></span> | <span data-ttu-id="f9eba-228">Tak</span><span class="sxs-lookup"><span data-stu-id="f9eba-228">Yes</span></span> | <span data-ttu-id="f9eba-229">Określa, czy próg hello całkowitą liczbę naruszeń lub kolejnych naruszenia z hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="f9eba-229">Specifies whether hello threshold is for total number of breaches or consecutive breaches from hello following values:</span></span><br><br><span data-ttu-id="f9eba-230">**Całkowita liczba<br>kolejnych**</span><span class="sxs-lookup"><span data-stu-id="f9eba-230">**Total<br>Consecutive**</span></span> |
| <span data-ttu-id="f9eba-231">Operator</span><span class="sxs-lookup"><span data-stu-id="f9eba-231">Operator</span></span> | <span data-ttu-id="f9eba-232">Tak</span><span class="sxs-lookup"><span data-stu-id="f9eba-232">Yes</span></span> | <span data-ttu-id="f9eba-233">Operator porównania hello z hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="f9eba-233">Operator for hello comparison from hello following values:</span></span><br><br><span data-ttu-id="f9eba-234">**gt = większe<br>lt = mniej niż**</span><span class="sxs-lookup"><span data-stu-id="f9eba-234">**gt = greater than<br>lt = less than**</span></span> |
| <span data-ttu-id="f9eba-235">Wartość</span><span class="sxs-lookup"><span data-stu-id="f9eba-235">Value</span></span> | <span data-ttu-id="f9eba-236">Tak</span><span class="sxs-lookup"><span data-stu-id="f9eba-236">Yes</span></span> | <span data-ttu-id="f9eba-237">Liczba hello razy kryteria hello musi być niespełnienia tootrigger hello alertu.</span><span class="sxs-lookup"><span data-stu-id="f9eba-237">Number of hello times hello criteria must be met tootrigger hello alert.</span></span> |

##### <a name="throttling"></a><span data-ttu-id="f9eba-238">Ograniczanie przepływności</span><span class="sxs-lookup"><span data-stu-id="f9eba-238">Throttling</span></span>
<span data-ttu-id="f9eba-239">Ta sekcja jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="f9eba-239">This section is optional.</span></span>  <span data-ttu-id="f9eba-240">W tej sekcji należy uwzględnić, jeśli chcesz otrzymywać alerty toosuppress z hello same reguły dla niektórych ilość czasu, po utworzeniu alertu.</span><span class="sxs-lookup"><span data-stu-id="f9eba-240">Include this section if you want toosuppress alerts from hello same rule for some amount of time after an alert is created.</span></span>

| <span data-ttu-id="f9eba-241">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="f9eba-241">Element name</span></span> | <span data-ttu-id="f9eba-242">Wymagane</span><span class="sxs-lookup"><span data-stu-id="f9eba-242">Required</span></span> | <span data-ttu-id="f9eba-243">Opis</span><span class="sxs-lookup"><span data-stu-id="f9eba-243">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="f9eba-244">DurationInMinutes</span><span class="sxs-lookup"><span data-stu-id="f9eba-244">DurationInMinutes</span></span> | <span data-ttu-id="f9eba-245">Tak, jeśli ograniczanie dołączony — element</span><span class="sxs-lookup"><span data-stu-id="f9eba-245">Yes if Throttling element included</span></span> | <span data-ttu-id="f9eba-246">Liczba minut toosuppress alertów po jednej z hello tworzone tego samego alertu.</span><span class="sxs-lookup"><span data-stu-id="f9eba-246">Number of minutes toosuppress alerts after one from hello same alert rule is created.</span></span> |

##### <a name="emailnotification"></a><span data-ttu-id="f9eba-247">EmailNotification</span><span class="sxs-lookup"><span data-stu-id="f9eba-247">EmailNotification</span></span>
 <span data-ttu-id="f9eba-248">Ta sekcja jest opcjonalny Dołącz go, jeśli chcesz hello tooone poczty toosend alertu lub więcej adresatów.</span><span class="sxs-lookup"><span data-stu-id="f9eba-248">This section is optional  Include it if you want hello alert toosend mail tooone or more recipients.</span></span>

| <span data-ttu-id="f9eba-249">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="f9eba-249">Element name</span></span> | <span data-ttu-id="f9eba-250">Wymagane</span><span class="sxs-lookup"><span data-stu-id="f9eba-250">Required</span></span> | <span data-ttu-id="f9eba-251">Opis</span><span class="sxs-lookup"><span data-stu-id="f9eba-251">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="f9eba-252">Adresaci</span><span class="sxs-lookup"><span data-stu-id="f9eba-252">Recipients</span></span> | <span data-ttu-id="f9eba-253">Tak</span><span class="sxs-lookup"><span data-stu-id="f9eba-253">Yes</span></span> | <span data-ttu-id="f9eba-254">Rozdzielany przecinkami lista e-mail adresów toosend powiadomień, podczas tworzenia alertu takich jak w hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="f9eba-254">Comma delimited list of email addresses toosend notification when an alert is created such as in hello following example.</span></span><br><br><span data-ttu-id="f9eba-255">**[ "recipient1@contoso.com", "recipient2@contoso.com" ]**</span><span class="sxs-lookup"><span data-stu-id="f9eba-255">**[ "recipient1@contoso.com", "recipient2@contoso.com" ]**</span></span> |
| <span data-ttu-id="f9eba-256">Temat</span><span class="sxs-lookup"><span data-stu-id="f9eba-256">Subject</span></span> | <span data-ttu-id="f9eba-257">Tak</span><span class="sxs-lookup"><span data-stu-id="f9eba-257">Yes</span></span> | <span data-ttu-id="f9eba-258">Wiersz tematu wiadomości powitania.</span><span class="sxs-lookup"><span data-stu-id="f9eba-258">Subject line of hello mail.</span></span> |
| <span data-ttu-id="f9eba-259">Załącznika</span><span class="sxs-lookup"><span data-stu-id="f9eba-259">Attachment</span></span> | <span data-ttu-id="f9eba-260">Nie</span><span class="sxs-lookup"><span data-stu-id="f9eba-260">No</span></span> | <span data-ttu-id="f9eba-261">Załączniki nie są obecnie obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="f9eba-261">Attachments are not currently supported.</span></span>  <span data-ttu-id="f9eba-262">Jeśli ten element jest włączone, należy go **Brak**.</span><span class="sxs-lookup"><span data-stu-id="f9eba-262">If this element is included, it should be **None**.</span></span> |


##### <a name="remediation"></a><span data-ttu-id="f9eba-263">Korygowania</span><span class="sxs-lookup"><span data-stu-id="f9eba-263">Remediation</span></span>
<span data-ttu-id="f9eba-264">Ta sekcja jest opcjonalna Dołącz ją, jeśli chcesz, aby toostart elementu runbook, w odpowiedzi toohello alertu.</span><span class="sxs-lookup"><span data-stu-id="f9eba-264">This section is optional  Include it if you want a runbook toostart in response toohello alert.</span></span> |

| <span data-ttu-id="f9eba-265">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="f9eba-265">Element name</span></span> | <span data-ttu-id="f9eba-266">Wymagane</span><span class="sxs-lookup"><span data-stu-id="f9eba-266">Required</span></span> | <span data-ttu-id="f9eba-267">Opis</span><span class="sxs-lookup"><span data-stu-id="f9eba-267">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="f9eba-268">RunbookName</span><span class="sxs-lookup"><span data-stu-id="f9eba-268">RunbookName</span></span> | <span data-ttu-id="f9eba-269">Tak</span><span class="sxs-lookup"><span data-stu-id="f9eba-269">Yes</span></span> | <span data-ttu-id="f9eba-270">Nazwa hello toostart elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="f9eba-270">Name of hello runbook toostart.</span></span> |
| <span data-ttu-id="f9eba-271">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="f9eba-271">WebhookUri</span></span> | <span data-ttu-id="f9eba-272">Tak</span><span class="sxs-lookup"><span data-stu-id="f9eba-272">Yes</span></span> | <span data-ttu-id="f9eba-273">Identyfikator URI elementu webhook hello hello elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="f9eba-273">Uri of hello webhook for hello runbook.</span></span> |
| <span data-ttu-id="f9eba-274">Wygaśnięcia</span><span class="sxs-lookup"><span data-stu-id="f9eba-274">Expiry</span></span> | <span data-ttu-id="f9eba-275">Nie</span><span class="sxs-lookup"><span data-stu-id="f9eba-275">No</span></span> | <span data-ttu-id="f9eba-276">Data i godzina hello korygowania wygasa.</span><span class="sxs-lookup"><span data-stu-id="f9eba-276">Date and time that hello remediation expires.</span></span> |

#### <a name="webhook-actions"></a><span data-ttu-id="f9eba-277">Akcje elementu Webhook</span><span class="sxs-lookup"><span data-stu-id="f9eba-277">Webhook actions</span></span>

<span data-ttu-id="f9eba-278">Akcje elementu Webhook uruchomienia procesu podczas wywoływania adresu URL i opcjonalnie podając toobe ładunku, wysyłane.</span><span class="sxs-lookup"><span data-stu-id="f9eba-278">Webhook actions start a process by calling a URL and optionally providing a payload toobe sent.</span></span> <span data-ttu-id="f9eba-279">Są one podobne akcje tooRemediation, z wyjątkiem są przeznaczone dla elementów webhook, które może wywołać procesów innych niż element runbook usługi Automatyzacja Azure.</span><span class="sxs-lookup"><span data-stu-id="f9eba-279">They are similar tooRemediation actions except they are meant for webhooks that may invoke processes other than Azure Automation runbooks.</span></span> <span data-ttu-id="f9eba-280">Zapewniają także hello dodatkowa opcja udostępniania procesu zdalnego toohello toobe dostarczyć ładunku.</span><span class="sxs-lookup"><span data-stu-id="f9eba-280">They also provide hello additional option of providing a payload toobe delivered toohello remote process.</span></span>

<span data-ttu-id="f9eba-281">Jeśli alert będzie wywoływać elementu webhook, a następnie konieczne będzie zasób akcji z typem **Webhook** w toohello dodanie **Alert** zasób akcji.</span><span class="sxs-lookup"><span data-stu-id="f9eba-281">If your alert will call a webhook, then it will need an action resource with a type of **Webhook** in addition toohello **Alert** action resource.</span></span>  

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

<span data-ttu-id="f9eba-282">Hello właściwości elementu Webhook akcji zasobów są opisane w następujących tabel hello.</span><span class="sxs-lookup"><span data-stu-id="f9eba-282">hello properties for Webhook action resources are described in hello following tables.</span></span>

| <span data-ttu-id="f9eba-283">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="f9eba-283">Element name</span></span> | <span data-ttu-id="f9eba-284">Wymagane</span><span class="sxs-lookup"><span data-stu-id="f9eba-284">Required</span></span> | <span data-ttu-id="f9eba-285">Opis</span><span class="sxs-lookup"><span data-stu-id="f9eba-285">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="f9eba-286">type</span><span class="sxs-lookup"><span data-stu-id="f9eba-286">type</span></span> | <span data-ttu-id="f9eba-287">Tak</span><span class="sxs-lookup"><span data-stu-id="f9eba-287">Yes</span></span> | <span data-ttu-id="f9eba-288">Typ akcji hello.</span><span class="sxs-lookup"><span data-stu-id="f9eba-288">Type of hello action.</span></span>  <span data-ttu-id="f9eba-289">Są to **Webhook** dla Akcje elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="f9eba-289">This will be **Webhook** for webhook actions.</span></span> |
| <span data-ttu-id="f9eba-290">name</span><span class="sxs-lookup"><span data-stu-id="f9eba-290">name</span></span> | <span data-ttu-id="f9eba-291">Tak</span><span class="sxs-lookup"><span data-stu-id="f9eba-291">Yes</span></span> | <span data-ttu-id="f9eba-292">Nazwa wyświetlana hello akcji.</span><span class="sxs-lookup"><span data-stu-id="f9eba-292">Display name for hello action.</span></span>  <span data-ttu-id="f9eba-293">Nie jest on wyświetlany w konsoli hello.</span><span class="sxs-lookup"><span data-stu-id="f9eba-293">This is not displayed in hello console.</span></span> |
| <span data-ttu-id="f9eba-294">wehookUri</span><span class="sxs-lookup"><span data-stu-id="f9eba-294">wehookUri</span></span> | <span data-ttu-id="f9eba-295">Tak</span><span class="sxs-lookup"><span data-stu-id="f9eba-295">Yes</span></span> | <span data-ttu-id="f9eba-296">Identyfikator URI dla elementu webhook hello.</span><span class="sxs-lookup"><span data-stu-id="f9eba-296">Uri for hello webhook.</span></span> |
| <span data-ttu-id="f9eba-297">CustomPayload</span><span class="sxs-lookup"><span data-stu-id="f9eba-297">customPayload</span></span> | <span data-ttu-id="f9eba-298">Nie</span><span class="sxs-lookup"><span data-stu-id="f9eba-298">No</span></span> | <span data-ttu-id="f9eba-299">Niestandardowy ładunek toobe wysyłane toohello elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="f9eba-299">Custom payload toobe sent toohello webhook.</span></span> <span data-ttu-id="f9eba-300">Hello format będzie zależeć od elementu webhook jakie hello jest oczekiwany.</span><span class="sxs-lookup"><span data-stu-id="f9eba-300">hello format will depend on what hello webhook is expecting.</span></span> |




## <a name="sample"></a><span data-ttu-id="f9eba-301">Przykład</span><span class="sxs-lookup"><span data-stu-id="f9eba-301">Sample</span></span>

<span data-ttu-id="f9eba-302">Poniżej przedstawiono przykładowe rozwiązanie obejmujące obejmuje hello następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="f9eba-302">Following is a sample of a solution that include that includes hello following resources:</span></span>

- <span data-ttu-id="f9eba-303">Zapisane wyszukiwanie</span><span class="sxs-lookup"><span data-stu-id="f9eba-303">Saved search</span></span>
- <span data-ttu-id="f9eba-304">Harmonogram</span><span class="sxs-lookup"><span data-stu-id="f9eba-304">Schedule</span></span>
- <span data-ttu-id="f9eba-305">Akcji alertu</span><span class="sxs-lookup"><span data-stu-id="f9eba-305">Alert action</span></span>
- <span data-ttu-id="f9eba-306">Akcja elementu Webhook</span><span class="sxs-lookup"><span data-stu-id="f9eba-306">Webhook action</span></span>

<span data-ttu-id="f9eba-307">Witaj używa próbki [parametry standardowego rozwiązania](operations-management-suite-solutions-solution-file.md#parameters) zmiennych, które służy zwykle do rozwiązania jako przeciwieństwie wartości toohardcoding w definicjach zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="f9eba-307">hello sample uses [standard solution parameters](operations-management-suite-solutions-solution-file.md#parameters) variables that would commonly be used in a solution as opposed toohardcoding values in hello resource definitions.</span></span>

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
              "Description": "List of recipients for hello email alert separated by semicolon"
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


<span data-ttu-id="f9eba-308">Hello następującego pliku parametrów zawiera przykłady wartości dla tego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f9eba-308">hello following parameter file provides samples values for this solution.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="f9eba-309">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f9eba-309">Next steps</span></span>
* <span data-ttu-id="f9eba-310">[Dodawanie widoków](operations-management-suite-solutions-resources-views.md) tooyour rozwiązania do zarządzania.</span><span class="sxs-lookup"><span data-stu-id="f9eba-310">[Add views](operations-management-suite-solutions-resources-views.md) tooyour management solution.</span></span>
* <span data-ttu-id="f9eba-311">[Dodaj element runbook usługi Automatyzacja i innych zasobów](operations-management-suite-solutions-resources-automation.md) tooyour rozwiązania do zarządzania.</span><span class="sxs-lookup"><span data-stu-id="f9eba-311">[Add Automation runbooks and other resources](operations-management-suite-solutions-resources-automation.md) tooyour management solution.</span></span>

