---
title: "aaaView działanie Azure dzienniki zasobów toomonitor | Dokumentacja firmy Microsoft"
description: "Użyj hello działania dzienniki tooreview użytkownika akcje i błędy. Pokazuje portalu Azure w programie PowerShell, interfejsu wiersza polecenia platformy Azure i REST."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: fcdb3125-13ce-4c3b-9087-f514c5e41e73
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: tomfitz
ms.openlocfilehash: 8430ed2a9c1dfe5f13423a55d358e590b0facb22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="view-activity-logs-tooaudit-actions-on-resources"></a><span data-ttu-id="96bbb-104">Wyświetl działanie rejestruje akcje tooaudit zasobów</span><span class="sxs-lookup"><span data-stu-id="96bbb-104">View activity logs tooaudit actions on resources</span></span>
<span data-ttu-id="96bbb-105">Za pomocą działania dzienniki można określić:</span><span class="sxs-lookup"><span data-stu-id="96bbb-105">Through activity logs, you can determine:</span></span>

* <span data-ttu-id="96bbb-106">jakie operacje zostały pobrane na powitania zasobów w ramach subskrypcji</span><span class="sxs-lookup"><span data-stu-id="96bbb-106">what operations were taken on hello resources in your subscription</span></span>
* <span data-ttu-id="96bbb-107">kto zainicjował operację hello (chociaż operacje inicjowane przez usługi wewnętrznej bazy danych nie mają użytkownika jako wywołującego hello)</span><span class="sxs-lookup"><span data-stu-id="96bbb-107">who initiated hello operation (although operations initiated by a backend service do not return a user as hello caller)</span></span>
* <span data-ttu-id="96bbb-108">wystąpienia hello operacji</span><span class="sxs-lookup"><span data-stu-id="96bbb-108">when hello operation occurred</span></span>
* <span data-ttu-id="96bbb-109">Stan Hello hello operacji</span><span class="sxs-lookup"><span data-stu-id="96bbb-109">hello status of hello operation</span></span>
* <span data-ttu-id="96bbb-110">Hello wartości innych właściwości, które mogą ułatwić badania hello operacji</span><span class="sxs-lookup"><span data-stu-id="96bbb-110">hello values of other properties that might help you research hello operation</span></span>

[!INCLUDE [resource-manager-audit-limitations](../../includes/resource-manager-audit-limitations.md)]

<span data-ttu-id="96bbb-111">Mogą pobierać informacje z Dzienniki aktywności hello za pośrednictwem portalu hello, programu PowerShell, interfejsu wiersza polecenia Azure, interfejsu API REST szczegółowych informacji, lub [biblioteki .NET Insights](https://www.nuget.org/packages/Microsoft.Azure.Insights/).</span><span class="sxs-lookup"><span data-stu-id="96bbb-111">You can retrieve information from hello activity logs through hello portal, PowerShell, Azure CLI, Insights REST API, or [Insights .NET Library](https://www.nuget.org/packages/Microsoft.Azure.Insights/).</span></span>

## <a name="portal"></a><span data-ttu-id="96bbb-112">Portal</span><span class="sxs-lookup"><span data-stu-id="96bbb-112">Portal</span></span>
1. <span data-ttu-id="96bbb-113">Wybierz Dzienniki aktywności hello tooview za pośrednictwem portalu hello **Monitor**.</span><span class="sxs-lookup"><span data-stu-id="96bbb-113">tooview hello activity logs through hello portal, select **Monitor**.</span></span>
   
    ![Wybierz Dzienniki aktywności](./media/resource-group-audit/select-monitor.png)

   <span data-ttu-id="96bbb-115">Lub dziennik aktywności hello tooautomatically filtru dla określonego zasobu lub grupy zasobów, wybierz opcję **dziennik aktywności** z tego bloku zasobów.</span><span class="sxs-lookup"><span data-stu-id="96bbb-115">Or, tooautomatically filter hello activity log for a particular resource or resource group, select **Activity log** from that resource blade.</span></span> <span data-ttu-id="96bbb-116">Należy zauważyć, że ten dziennik aktywności hello automatycznie są filtrowane według zasobu hello wybrane.</span><span class="sxs-lookup"><span data-stu-id="96bbb-116">Notice that hello activity log is automatically filtered by hello selected resource.</span></span>
   
    ![Filtruj według zasobu](./media/resource-group-audit/filtered-by-resource.png)
2. <span data-ttu-id="96bbb-118">W hello **dziennik aktywności** bloku, wyświetlane jest podsumowanie ostatnich operacji.</span><span class="sxs-lookup"><span data-stu-id="96bbb-118">In hello **Activity Log** blade, you see a summary of recent operations.</span></span>
   
    ![Pokaż akcje](./media/resource-group-audit/audit-summary.png)
3. <span data-ttu-id="96bbb-120">toorestrict hello liczbę operacji wyświetlane, wybierz inne warunki.</span><span class="sxs-lookup"><span data-stu-id="96bbb-120">toorestrict hello number of operations displayed, select different conditions.</span></span> <span data-ttu-id="96bbb-121">Na przykład hello poniższy obraz przedstawia hello **Timespan** i **zdarzenie inicjowane przez** pola zmienione tooview hello akcje wykonywane przez określonego użytkownika lub aplikacji hello ostatnim miesiącu.</span><span class="sxs-lookup"><span data-stu-id="96bbb-121">For example, hello following image shows hello **Timespan** and **Event initiated by** fields changed tooview hello actions taken by a particular user or application for hello past month.</span></span> <span data-ttu-id="96bbb-122">Wybierz **Zastosuj** tooview hello wyniki zapytania.</span><span class="sxs-lookup"><span data-stu-id="96bbb-122">Select **Apply** tooview hello results of your query.</span></span>
   
    ![Ustaw opcje filtru](./media/resource-group-audit/set-filter.png)

4. <span data-ttu-id="96bbb-124">Zapytanie hello toorun ponownie później, należy wybrać **zapisać** i nadaj nazwę hello zapytania.</span><span class="sxs-lookup"><span data-stu-id="96bbb-124">If you need toorun hello query again later, select **Save** and give hello query a name.</span></span>
   
    ![Zapisz zapytanie](./media/resource-group-audit/save-query.png)
5. <span data-ttu-id="96bbb-126">tooquickly uruchomić kwerendę, można wybrać jedną z wbudowanych kwerend hello, takich jak wdrożenia nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="96bbb-126">tooquickly run a query, you can select one of hello built-in queries, such as failed deployments.</span></span>

    ![Wybierz zapytanie](./media/resource-group-audit/select-quick-query.png)

   <span data-ttu-id="96bbb-128">Wybrane zapytanie Hello automatycznie ustawia hello wymagane wartości filtru.</span><span class="sxs-lookup"><span data-stu-id="96bbb-128">hello selected query automatically sets hello required filter values.</span></span>

    ![Wyświetl błędy wdrażania](./media/resource-group-audit/view-failed-deployment.png)   

6. <span data-ttu-id="96bbb-130">Wybierz jedną z toosee operacji hello podsumowanie hello zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="96bbb-130">Select one of hello operations toosee a summary of hello event.</span></span>

    ![operacji dotyczącej widoku](./media/resource-group-audit/view-operation.png)  

## <a name="powershell"></a><span data-ttu-id="96bbb-132">PowerShell</span><span class="sxs-lookup"><span data-stu-id="96bbb-132">PowerShell</span></span>
1. <span data-ttu-id="96bbb-133">wpisy dziennika tooretrieve, uruchom hello **Get-AzureRmLog** polecenia.</span><span class="sxs-lookup"><span data-stu-id="96bbb-133">tooretrieve log entries, run hello **Get-AzureRmLog** command.</span></span> <span data-ttu-id="96bbb-134">Możesz podać dodatkowe parametry toofilter hello listy wpisów.</span><span class="sxs-lookup"><span data-stu-id="96bbb-134">You provide additional parameters toofilter hello list of entries.</span></span> <span data-ttu-id="96bbb-135">Jeśli nie określisz godzina rozpoczęcia i zakończenia, wpisy dla hello ostatniej godziny są zwracane.</span><span class="sxs-lookup"><span data-stu-id="96bbb-135">If you do not specify a start and end time, entries for hello last hour are returned.</span></span> <span data-ttu-id="96bbb-136">Na przykład uruchom tooretrieve hello operacji dla grupy zasobów podczas hello ostatniej godziny:</span><span class="sxs-lookup"><span data-stu-id="96bbb-136">For example, tooretrieve hello operations for a resource group during hello past hour run:</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup
  ```
   
    <span data-ttu-id="96bbb-137">Witaj poniższy przykład przedstawia sposób działania hello toouse dziennika operacji tooresearch podjąć w określonym czasie.</span><span class="sxs-lookup"><span data-stu-id="96bbb-137">hello following example shows how toouse hello activity log tooresearch operations taken during a specified time.</span></span> <span data-ttu-id="96bbb-138">Witaj daty rozpoczęcia i zakończenia są określone w formacie daty.</span><span class="sxs-lookup"><span data-stu-id="96bbb-138">hello start and end dates are specified in a date format.</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime 2015-08-28T06:00 -EndTime 2015-09-10T06:00
  ```

    <span data-ttu-id="96bbb-139">Alternatywnie można użyć funkcji toospecify hello Data zakres dat, takich jak hello ostatnie 14 dni.</span><span class="sxs-lookup"><span data-stu-id="96bbb-139">Or, you can use date functions toospecify hello date range, such as hello last 14 days.</span></span>
   
  ```powershell 
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14)
  ```

2. <span data-ttu-id="96bbb-140">W zależności od hello czasem rozpoczęcia, które określisz poprzednie polecenia hello może zwrócić długą listę operacji dla grupy zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="96bbb-140">Depending on hello start time you specify, hello previous commands can return a long list of operations for hello resource group.</span></span> <span data-ttu-id="96bbb-141">Można filtrować wyniki hello są odpowiednie podając kryteria wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="96bbb-141">You can filter hello results for what you are looking for by providing search criteria.</span></span> <span data-ttu-id="96bbb-142">Na przykład jeśli próbujesz tooresearch jak aplikacji sieci web została zatrzymana, można uruchomić hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="96bbb-142">For example, if you are trying tooresearch how a web app was stopped, you could run hello following command:</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14) | Where-Object OperationName -eq Microsoft.Web/sites/stop/action
  ```

    <span data-ttu-id="96bbb-143">Który w tym przykładzie wskazuje, że Akcja zatrzymania została wykonana przez użytkownika someone@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="96bbb-143">Which for this example shows that a stop action was performed by someone@contoso.com.</span></span> 

  ```powershell 
  Authorization     :
  Scope     : /subscriptions/xxxxx/resourcegroups/ExampleGroup/providers/Microsoft.Web/sites/ExampleSite
  Action    : Microsoft.Web/sites/stop/action
  Role      : Subscription Admin
  Condition :
  Caller            : someone@contoso.com
  CorrelationId     : 84beae59-92aa-4662-a6fc-b6fecc0ff8da
  EventSource       : Administrative
  EventTimestamp    : 8/28/2015 4:08:18 PM
  OperationName     : Microsoft.Web/sites/stop/action
  ResourceGroupName : ExampleGroup
  ResourceId        : /subscriptions/xxxxx/resourcegroups/ExampleGroup/providers/Microsoft.Web/sites/ExampleSite
  Status            : Succeeded
  SubscriptionId    : xxxxx
  SubStatus         : OK
  ```

3. <span data-ttu-id="96bbb-144">Można wyszukiwać hello akcje wykonywane przez określonego użytkownika, nawet w przypadku grupy zasobów, która już nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="96bbb-144">You can look up hello actions taken by a particular user, even for a resource group that no longer exists.</span></span>

  ```powershell 
  Get-AzureRmLog -ResourceGroup deletedgroup -StartTime (Get-Date).AddDays(-14) -Caller someone@contoso.com
  ```

4. <span data-ttu-id="96bbb-145">Można filtrować zakończone niepowodzeniem operacje.</span><span class="sxs-lookup"><span data-stu-id="96bbb-145">You can filter for failed operations.</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -Status Failed
  ```

5. <span data-ttu-id="96bbb-146">Można skupić się na jeden błąd analizując hello komunikatu o stanie dla tego wpisu.</span><span class="sxs-lookup"><span data-stu-id="96bbb-146">You can focus on one error by looking at hello status message for that entry.</span></span>
   
        ((Get-AzureRmLog -Status Failed -ResourceGroup ExampleGroup -DetailedOutput).Properties[1].Content["statusMessage"] | ConvertFrom-Json).error
   
    <span data-ttu-id="96bbb-147">Polecenie to zwraca:</span><span class="sxs-lookup"><span data-stu-id="96bbb-147">Which returns:</span></span>
   
        code           message                                                                        
        ----           -------                                                                        
        DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. 


## <a name="azure-cli"></a><span data-ttu-id="96bbb-148">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="96bbb-148">Azure CLI</span></span>
* <span data-ttu-id="96bbb-149">wpisy dziennika tooretrieve, uruchom hello **Pokaż dziennik grupy azure** polecenia.</span><span class="sxs-lookup"><span data-stu-id="96bbb-149">tooretrieve log entries, you run hello **azure group log show** command.</span></span>

  ```azurecli
  azure group log show ExampleGroup --json
  ```


## <a name="rest-api"></a><span data-ttu-id="96bbb-150">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="96bbb-150">REST API</span></span>
<span data-ttu-id="96bbb-151">Witaj operacje REST do pracy z dziennika aktywności hello są częścią hello [interfejsu API REST usługi Insights](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="96bbb-151">hello REST operations for working with hello activity log are part of hello [Insights REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span> <span data-ttu-id="96bbb-152">zdarzenia dziennika aktywności tooretrieve, zobacz [listy zdarzeń zarządzania hello w ramach subskrypcji](https://msdn.microsoft.com/library/azure/dn931934.aspx).</span><span class="sxs-lookup"><span data-stu-id="96bbb-152">tooretrieve activity log events, see [List hello management events in a subscription](https://msdn.microsoft.com/library/azure/dn931934.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="96bbb-153">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="96bbb-153">Next steps</span></span>
* <span data-ttu-id="96bbb-154">Azure dzienniki działania mogą być używane z usługi Power BI toogain bardziej szczegółowe analizy o akcjach hello w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="96bbb-154">Azure Activity logs can be used with Power BI toogain greater insights about hello actions in your subscription.</span></span> <span data-ttu-id="96bbb-155">Zobacz [widoku i analizować Dzienniki aktywności platformy Azure w usłudze Power BI i nie tylko](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/).</span><span class="sxs-lookup"><span data-stu-id="96bbb-155">See [View and analyze Azure Activity Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/).</span></span>
* <span data-ttu-id="96bbb-156">toolearn o Ustawianie zasad zabezpieczeń, zobacz [kontroli dostępu opartej na roli Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="96bbb-156">toolearn about setting security policies, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>
* <span data-ttu-id="96bbb-157">Zobacz toolearn dotyczących operacji wdrażania, wyświetlanie poleceń hello [wyświetlić operacje wdrażania](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="96bbb-157">toolearn about hello commands for viewing deployment operations, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="96bbb-158">toolearn tooprevent usunięcia zasobu dla wszystkich użytkowników, zobacz temat [blokowania zasobów z usługi Azure Resource Manager](resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="96bbb-158">toolearn how tooprevent deletions on a resource for all users, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

