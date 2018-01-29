---
title: "Wywoływanie elementu runbook usługi Azure Automation z alertu usługi Log Analytics | Microsoft Docs"
description: "Ten artykuł zawiera omówienie sposobu wywoływania elementu runbook usługi Automation z alertu usługi Log Analytics w pakiecie Operations Management Suite."
services: automation
documentationcenter: 
author: georgewallace
manager: jwhit
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/31/2017
ms.author: magoedte
ms.openlocfilehash: a10be867965eef9746a0f4cc9b14c4fc429f6e35
ms.sourcegitcommit: 9292e15fc80cc9df3e62731bafdcb0bb98c256e1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/10/2018
---
# <a name="call-an-azure-automation-runbook-from-a-log-analytics-alert"></a>Wywoływanie elementu runbook usługi Azure Automation z alertu usługi Log Analytics

W usłudze Azure Log Analytics można skonfigurować alert do tworzenia rekordu alertu, gdy wyniki spełniają określone kryteria. Alert ten może automatycznie uruchamiać element runbook usługi Automation w celu podjęcia próby automatycznego rozwiązania problemu. 

Alert może na przykład wskazywać długotrwały wzrost użycia procesora. Może też wskazywać, kiedy proces aplikacji o znaczeniu krytycznym dla funkcjonalności aplikacji biznesowej zakończy się niepowodzeniem. Element runbook może następnie zapisywać odpowiadające zdarzenie w dzienniku zdarzeń systemu Windows.  

Podczas konfigurowania alertu dostępne są dwie opcje wywołania elementu runbook:

* Skorzystanie z elementu webhook.
   * To jedyna dostępna opcja w przypadku, gdy obszar roboczy pakietu Operations Management Suite nie jest połączony z kontem usługi Automation.
   * Jeśli masz już konto usługi Automation połączone z obszarem roboczym pakietu Operations Management Suite, ta opcja będzie nadal dostępna.  

* Bezpośrednie wybranie elementu runbook.
   * Ta opcja jest dostępna tylko po połączeniu obszaru roboczego pakietu Operations Management Suite z kontem usługi Automation.

## <a name="calling-a-runbook-by-using-a-webhook"></a>Wywoływanie elementu runbook przy użyciu elementu webhook

Elementu webhook można użyć do uruchomienia określonego elementu runbook w usłudze Azure Automation za pośrednictwem pojedynczego żądania HTTP. Zanim skonfigurujesz [alert usługi Log Analytics](../log-analytics/log-analytics-alerts.md#alert-rules) do wywoływania elementu runbook za pomocą elementu webhook jako akcji alertu, musisz [utworzyć element webhook](automation-webhooks.md#creating-a-webhook) dla elementu runbook, który jest wywoływany za pośrednictwem tej metody. Pamiętaj o zapisaniu adresu URL elementu webhook, aby podać go podczas konfigurowania reguły alertu.   

## <a name="calling-a-runbook-directly"></a>Bezpośrednie uruchamianie elementu runbook

W obszarze roboczym usługi Operations Management Suite można zainstalować i skonfigurować usługę Automation and Control. Podczas konfigurowania opcji akcji elementu runbook dla alertu możesz wyświetlić wszystkie elementy runbook na liście rozwijanej **Wybierz element runbook** i wybrać konkretny element runbook, który ma być uruchamiany w odpowiedzi na alert. Wybrany element runbook można uruchomić w obszarze roboczym platformy Azure lub w hybrydowym procesie roboczym elementu runbook. 

Po utworzeniu alertu przy użyciu opcji elementu runbook dla elementu runbook jest tworzony element webhook. Element webhook można wyświetlić po przejściu do konta usługi Automation i otworzeniu okienka elementu webhook wybranego elementu runbook. 

Jeśli usuniesz alert, element webhook nie zostanie usunięty. To nie jest problem. Element webhook będzie po prostu elementem oddzielonym, który ostatecznie trzeba będzie usunąć ręcznie w celu utrzymania uporządkowanego konta usługi Automation.  

## <a name="characteristics-of-a-runbook"></a>Właściwości elementu runbook

Przed skonfigurowaniem reguł alertu należy zrozumieć cechy obu metod wywoływania elementu runbook z poziomu alertu usługi Log Analytics. 

Dane alertu są zapisane w formacie JSON w pojedynczej właściwości o nazwie **SearchResult**. Ten format jest używany w przypadku akcji elementów runbook i webhook ze standardowym ładunkiem. W przypadku akcji elementów webhook z niestandardowymi ładunkami (zawierających ciąg **IncludeSearchResults:True** w elemencie **RequestBody**) jest to właściwość **SearchResults**.

Musisz mieć parametr wejściowy elementu runbook o nazwie **WebhookData**, którego typ to **Obiekt**. Może on być wymagany lub opcjonalny. Przy użyciu tego parametru wejściowego alert przekazuje wyniki wyszukiwania do elementu runbook.

```powershell
param  
    (  
    [Parameter (Mandatory=$true)]  
    [object] $WebhookData  
    )
```
Musisz mieć również kod konwertujący parametr **WebhookData** na obiekt programu PowerShell.

```powershell
$SearchResult = (ConvertFrom-Json $WebhookData.RequestBody).SearchResult.value
```

Element **$SearchResult** jest tablicą obiektów. Każdy obiekt zawiera pola z wartościami z jednego wyniku wyszukiwania.


## <a name="example-walkthrough"></a>Przykładowy przewodnik

Poniższy przykład graficznego elementu runbook pokazuje, jak działa ten proces. Uruchamia on usługę systemu Windows.

![Graficzny element runbook do uruchamiania usługi systemu Windows](media/automation-invoke-runbook-from-omsla-alert/automation-runbook-restartservice.png)

Ten element runbook ma jeden parametr wejściowy typu **Obiekt** o nazwie **WebhookData**. Zawiera on dane elementu webhook przekazane z alertu zawierającego element **SearchResults**.

![Parametry wejściowe elementu Runbook](media/automation-invoke-runbook-from-omsla-alert/automation-runbook-restartservice-inputparameter.png)

Na potrzeby tego przykładu w usłudze Log Analytics utworzyliśmy dwa pola niestandardowe: **SvcDisplayName_CF** i **SvcState_CF**. Te pola wyodrębniają nazwę wyświetlaną usługi i stan usługi (uruchomiona lub zatrzymana) ze zdarzenia zapisanego w dzienniku zdarzeń systemu. Następnie utworzyliśmy regułę alertu z następującym zapytaniem wyszukiwania, dzięki czemu możemy wykryć, kiedy usługa Print Spooler zostanie zatrzymana w systemie Windows:

`Type=Event SvcDisplayName_CF="Print Spooler" SvcState_CF="stopped"` 

Może być to dowolna interesująca nas usługa. W tym przykładzie odwołujemy się do jednej ze wstępnie istniejących usług zawartych w systemie operacyjnym Windows. Akcja alertu jest skonfigurowana do wykonywania elementu runbook użytego w tym przykładzie i do działania w hybrydowym procesie roboczym elementu runbook, który jest włączany w systemie docelowym.   

Działanie kodu elementu runbook **Get Service Name from LA** przekonwertuje ciąg w formacie JSON na typ obiektu i zastosuje filtr do elementu **SvcDisplayName_CF**. Powoduje to wyodrębnienie nazwy wyświetlanej usługi systemu Windows, a następnie przekazuje ją do kolejnego działania, które przed podjęciem próby ponownego uruchomienia usługi sprawdzi, czy została ona zatrzymana. Element **SvcDisplayName_CF** to [pole niestandardowe](../log-analytics/log-analytics-custom-fields.md), które utworzyliśmy w usłudze Log Analytics na potrzeby tego przykładu.

```powershell
$SearchResult = (ConvertFrom-Json $WebhookData.RequestBody).SearchResult.value
$SearchResult.SvcDisplayName_CF  
```

Po zatrzymaniu usługi reguła alertu w usłudze Log Analytics wykrywa dopasowanie, wyzwala element runbook i wysyła kontekst alertu do tego elementu. Element runbook podejmuje próbę sprawdzenia, czy usługa została zatrzymana. Jeśli tak, element runbook próbuje ponownie uruchomić usługę, sprawdzić, czy usługa została uruchomiona prawidłowo, i wyświetlić wyniki.     

Alternatywnie, jeśli nie masz konta usługi Automation połączonego z przestrzenią roboczą pakietu Operations Management Suite, możesz skonfigurować regułę alertu z akcją elementu webhook. Ta akcja elementu webhook wyzwala element runbook. Konfiguruje również element runbook do konwertowania ciągu w formacie JSON oraz filtrowania elementu **SearchResult** zgodnie z podanymi wcześniej wskazówkami.    

>[!NOTE]
> Jeśli Twój obszar roboczy został uaktualniony do [nowego języka zapytań usługi Log Analytics](../log-analytics/log-analytics-log-search-upgrade.md), ładunek elementu webhook uległ zmianie. Szczegółowe informacje na temat tego formatu zawiera artykuł [Azure Log Analytics REST API](https://aka.ms/loganalyticsapiresponse) (Interfejs API REST usługi Azure Log Analytics).

## <a name="next-steps"></a>Kolejne kroki

* Aby dowiedzieć się więcej o alertach w usłudze Log Analytics i o sposobie ich tworzenia, zobacz temat [Alerts in Log Analytics](../log-analytics/log-analytics-alerts.md) (Alerty w usłudze Log Analytics).

* Aby dowiedzieć się, jak wyzwalać elementy runbook przy użyciu elementu webhook, zobacz [Elementy webhook w usłudze Azure Automation](automation-webhooks.md).
