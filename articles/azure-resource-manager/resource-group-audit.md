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
# <a name="view-activity-logs-tooaudit-actions-on-resources"></a>Wyświetl działanie rejestruje akcje tooaudit zasobów
Za pomocą działania dzienniki można określić:

* jakie operacje zostały pobrane na powitania zasobów w ramach subskrypcji
* kto zainicjował operację hello (chociaż operacje inicjowane przez usługi wewnętrznej bazy danych nie mają użytkownika jako wywołującego hello)
* wystąpienia hello operacji
* Stan Hello hello operacji
* Hello wartości innych właściwości, które mogą ułatwić badania hello operacji

[!INCLUDE [resource-manager-audit-limitations](../../includes/resource-manager-audit-limitations.md)]

Mogą pobierać informacje z Dzienniki aktywności hello za pośrednictwem portalu hello, programu PowerShell, interfejsu wiersza polecenia Azure, interfejsu API REST szczegółowych informacji, lub [biblioteki .NET Insights](https://www.nuget.org/packages/Microsoft.Azure.Insights/).

## <a name="portal"></a>Portal
1. Wybierz Dzienniki aktywności hello tooview za pośrednictwem portalu hello **Monitor**.
   
    ![Wybierz Dzienniki aktywności](./media/resource-group-audit/select-monitor.png)

   Lub dziennik aktywności hello tooautomatically filtru dla określonego zasobu lub grupy zasobów, wybierz opcję **dziennik aktywności** z tego bloku zasobów. Należy zauważyć, że ten dziennik aktywności hello automatycznie są filtrowane według zasobu hello wybrane.
   
    ![Filtruj według zasobu](./media/resource-group-audit/filtered-by-resource.png)
2. W hello **dziennik aktywności** bloku, wyświetlane jest podsumowanie ostatnich operacji.
   
    ![Pokaż akcje](./media/resource-group-audit/audit-summary.png)
3. toorestrict hello liczbę operacji wyświetlane, wybierz inne warunki. Na przykład hello poniższy obraz przedstawia hello **Timespan** i **zdarzenie inicjowane przez** pola zmienione tooview hello akcje wykonywane przez określonego użytkownika lub aplikacji hello ostatnim miesiącu. Wybierz **Zastosuj** tooview hello wyniki zapytania.
   
    ![Ustaw opcje filtru](./media/resource-group-audit/set-filter.png)

4. Zapytanie hello toorun ponownie później, należy wybrać **zapisać** i nadaj nazwę hello zapytania.
   
    ![Zapisz zapytanie](./media/resource-group-audit/save-query.png)
5. tooquickly uruchomić kwerendę, można wybrać jedną z wbudowanych kwerend hello, takich jak wdrożenia nie powiodło się.

    ![Wybierz zapytanie](./media/resource-group-audit/select-quick-query.png)

   Wybrane zapytanie Hello automatycznie ustawia hello wymagane wartości filtru.

    ![Wyświetl błędy wdrażania](./media/resource-group-audit/view-failed-deployment.png)   

6. Wybierz jedną z toosee operacji hello podsumowanie hello zdarzeń.

    ![operacji dotyczącej widoku](./media/resource-group-audit/view-operation.png)  

## <a name="powershell"></a>PowerShell
1. wpisy dziennika tooretrieve, uruchom hello **Get-AzureRmLog** polecenia. Możesz podać dodatkowe parametry toofilter hello listy wpisów. Jeśli nie określisz godzina rozpoczęcia i zakończenia, wpisy dla hello ostatniej godziny są zwracane. Na przykład uruchom tooretrieve hello operacji dla grupy zasobów podczas hello ostatniej godziny:

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup
  ```
   
    Witaj poniższy przykład przedstawia sposób działania hello toouse dziennika operacji tooresearch podjąć w określonym czasie. Witaj daty rozpoczęcia i zakończenia są określone w formacie daty.

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime 2015-08-28T06:00 -EndTime 2015-09-10T06:00
  ```

    Alternatywnie można użyć funkcji toospecify hello Data zakres dat, takich jak hello ostatnie 14 dni.
   
  ```powershell 
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14)
  ```

2. W zależności od hello czasem rozpoczęcia, które określisz poprzednie polecenia hello może zwrócić długą listę operacji dla grupy zasobów hello. Można filtrować wyniki hello są odpowiednie podając kryteria wyszukiwania. Na przykład jeśli próbujesz tooresearch jak aplikacji sieci web została zatrzymana, można uruchomić hello następujące polecenie:

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14) | Where-Object OperationName -eq Microsoft.Web/sites/stop/action
  ```

    Który w tym przykładzie wskazuje, że Akcja zatrzymania została wykonana przez użytkownika someone@contoso.com. 

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

3. Można wyszukiwać hello akcje wykonywane przez określonego użytkownika, nawet w przypadku grupy zasobów, która już nie istnieje.

  ```powershell 
  Get-AzureRmLog -ResourceGroup deletedgroup -StartTime (Get-Date).AddDays(-14) -Caller someone@contoso.com
  ```

4. Można filtrować zakończone niepowodzeniem operacje.

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -Status Failed
  ```

5. Można skupić się na jeden błąd analizując hello komunikatu o stanie dla tego wpisu.
   
        ((Get-AzureRmLog -Status Failed -ResourceGroup ExampleGroup -DetailedOutput).Properties[1].Content["statusMessage"] | ConvertFrom-Json).error
   
    Polecenie to zwraca:
   
        code           message                                                                        
        ----           -------                                                                        
        DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. 


## <a name="azure-cli"></a>Interfejs wiersza polecenia platformy Azure
* wpisy dziennika tooretrieve, uruchom hello **Pokaż dziennik grupy azure** polecenia.

  ```azurecli
  azure group log show ExampleGroup --json
  ```


## <a name="rest-api"></a>Interfejs API REST
Witaj operacje REST do pracy z dziennika aktywności hello są częścią hello [interfejsu API REST usługi Insights](https://msdn.microsoft.com/library/azure/dn931943.aspx). zdarzenia dziennika aktywności tooretrieve, zobacz [listy zdarzeń zarządzania hello w ramach subskrypcji](https://msdn.microsoft.com/library/azure/dn931934.aspx).

## <a name="next-steps"></a>Następne kroki
* Azure dzienniki działania mogą być używane z usługi Power BI toogain bardziej szczegółowe analizy o akcjach hello w ramach subskrypcji. Zobacz [widoku i analizować Dzienniki aktywności platformy Azure w usłudze Power BI i nie tylko](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/).
* toolearn o Ustawianie zasad zabezpieczeń, zobacz [kontroli dostępu opartej na roli Azure](../active-directory/role-based-access-control-configure.md).
* Zobacz toolearn dotyczących operacji wdrażania, wyświetlanie poleceń hello [wyświetlić operacje wdrażania](resource-manager-deployment-operations.md).
* toolearn tooprevent usunięcia zasobu dla wszystkich użytkowników, zobacz temat [blokowania zasobów z usługi Azure Resource Manager](resource-group-lock-resources.md).

