---
title: "aaaCalling element Runbook usługi Automatyzacja Azure z dziennika alertu Analytics | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera omówienie sposobu tooinvoke element runbook usługi Automatyzacja z alertu Analiza dzienników Microsoft OMS."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/31/2017
ms.author: magoedte
ms.openlocfilehash: 8b745d6e6c2b0294d676e010f52855cd51741cf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="calling-an-azure-automation-runbook-from-an-oms-log-analytics-alert"></a>Wywoływanie elementu runbook usługi Azure Automation z alertu usługi OMS Log Analytics

Gdy alert jest skonfigurowany w toocreate analizy dzienników rekord alertu, jeżeli wyników spełniających kryteria określonego, takich jak długimi kolekcji w określonej aplikacji proces krytyczne toohello funkcji aplikacji biznesowej lub użycie procesora nie powiedzie się i zapisuje odpowiednie zdarzenie w dzienniku zdarzeń systemu Windows hello, że alert automatycznie można uruchomić element runbook usługi Automatyzacja w tooauto próba-skorygować hello problem.  

Istnieją dwie opcje toocall elementu runbook podczas konfigurowania hello alertu.  Są to:

1. Skorzystanie z elementu webhook.
   * Jest to hello jedyną dostępną opcją, jeśli obszar roboczy OMS nie jest połączony tooan konta automatyzacji.
   * Jeśli masz już obszar roboczy OMS tooan konta automatyzacji, ta opcja jest nadal dostępny.  

2. Bezpośrednie wybranie elementu runbook.
   * Ta opcja jest dostępna tylko wtedy, gdy obszar roboczy OMS hello tooan połączonego konta automatyzacji.  

## <a name="calling-a-runbook-using-a-webhook"></a>Wywoływanie elementu runbook przy użyciu elementu webhook

Elementu webhook umożliwia toostart określonego elementu runbook automatyzacji Azure za pomocą pojedynczego żądania HTTP.  Przed skonfigurowaniem hello [alert analizy dzienników](../log-analytics/log-analytics-alerts.md#alert-rules) toocall hello runbook przy użyciu elementu webhook jako Akcja alertu, konieczne będzie toofirst tworzenia elementu webhook dla elementu runbook hello, która zostanie wywołana za pomocą tej metody.  Przejrzyj i wykonaj kroki hello hello [tworzenia elementu webhook](automation-webhooks.md#creating-a-webhook) artykułu i zapamiętać adresu URL elementu webhook hello toorecord odwołania podczas konfigurowania reguły alertu hello.   

## <a name="calling-a-runbook-directly"></a>Bezpośrednie uruchamianie elementu runbook

Jeśli masz hello automatyzacji & oferty kontroli zainstalowany i skonfigurowany w obszarze roboczym pakietu OMS, podczas konfigurowania opcji działania elementu Runbook hello hello alertu, można wyświetlić wszystkich elementów runbook z hello **wybrać element runbook** listy rozwijanej i wybierz hello element runbook ma toorun w odpowiedzi toohello alertu.  w obszarze roboczym hello chmury Azure lub hybrydowy proces roboczy elementu runbook można uruchomić elementu runbook Hello wybrane.  Podczas tworzenia alertu hello przy użyciu opcji elementu runbook hello elementu webhook zostaną utworzone dla hello elementu runbook.  Można wyświetlić elementu webhook hello Przejdź toohello konta automatyzacji i przejdź do bloku webhook toohello hello wybrany element runbook.  Jeśli usuniesz hello alert hello elementu webhook nie zostanie usunięta, ale hello użytkownika można usunąć elementu webhook hello ręcznie.  Nie jest problem Jeśli hello elementu webhook nie zostanie usunięta, jest ona tylko oddzielone elementu, który po pewnym czasie będzie konieczne toobe usunięte w kolejności toomaintain organizowane konta automatyzacji.  

## <a name="characteristics-of-a-runbook-for-both-options"></a>Właściwości elementu runbook (w przypadku obu opcji)

Obu metod wywoływania elementu runbook hello z hello analizy dzienników alert ma właściwości inaczej, wymagające toobe zrozumiał przed skonfigurowaniem reguł alertów.  

* Musisz mieć parametr wejściowy elementu runbook o nazwie **WebhookData**, którego typ to **Obiekt**.  Może on być wymagany lub opcjonalny.  Hello alert przekazuje hello wyszukiwania wyniki toohello elementu runbook za pomocą tego parametru wejściowego.

        param  
         (  
          [Parameter (Mandatory=$true)]  
          [object] $WebhookData  
         )

*  Musi mieć kod tooconvert hello WebhookData tooa środowiska PowerShell obiektu.

    `$SearchResults = (ConvertFrom-Json $WebhookData.RequestBody).SearchResults.value`

    *$SearchResults* będzie tablicę obiektów; każdego obiektu zawiera pola hello z wyników wyszukiwania co

### <a name="webhookdata-inconsistencies-between-hello-webhook-option-and-runbook-option"></a>WebhookData niespójności między opcję elementu webhook hello i elementu runbook

* Podczas konfigurowania alertów toocall elementu Webhook, wprowadź adres URL elementu webhook został utworzony dla elementu runbook i kliknij przycisk hello **Webhook testu** przycisku.  Hello wynikowy WebhookData wysyłane toohello elementu runbook nie zawiera albo *. Właściwości SearchResult* lub *. Wynikówwyszukiwania*.

*  Zapisanie tego alertu hello alert wyzwolenia i wywołuje element webhook hello hello WebhookData wysyłane toohello runbook zawiera *. Właściwości SearchResult*.
* Utwórz alert i należy skonfigurować ją toocall elementu runbook (która także tworzy elementu webhook), gdy hello alertu wyzwalaczy wysyła WebhookData toohello runbook, który zawiera *. Wynikówwyszukiwania*.

W związku z tym w powyższym przykładzie kodu hello, konieczne będzie tooget *. Właściwości SearchResult* Jeśli hello alert wywołania elementu webhook i będzie konieczne tooget *. Wynikówwyszukiwania* hello alert bezpośrednio wywołuje element runbook.

## <a name="example-walkthrough"></a>Przykładowy przewodnik

Firma Microsoft pokazują, jak to działa przy użyciu następującego przykładu graficznym elementem runbook, który uruchamia usługę Windows hello.<br><br> ![Graficzny element runbook uruchamiający usługę systemu Windows](media/automation-invoke-runbook-from-omsla-alert/automation-runbook-restartservice.png)<br>

Element runbook Hello ma jeden parametr wejściowy typu **obiektu** jest to **WebhookData** i obejmuje przekazywane z hello alertów zawierający dane elementu webhook hello *. Wynikówwyszukiwania*.<br><br> ![Parametry wejściowe elementu runbook](media/automation-invoke-runbook-from-omsla-alert/automation-runbook-restartservice-inputparameter.png)<br>

Na przykład w analizy dzienników utworzyliśmy dwa pola niestandardowe, *SvcDisplayName_CF* i *SvcState_CF*, tooextract hello wyświetlaną nazwę i hello stan usługi hello usługi (np. uruchomiona lub zatrzymana) od hello zdarzenia zapisywane w dzienniku zdarzeń systemowych toohello.  Następnie utworzymy regułę alertu z następującego zapytania wyszukiwania hello: `Type=Event SvcDisplayName_CF="Print Spooler" SvcState_CF="stopped"` tak, aby firma Microsoft może wykryć po zatrzymaniu hello usługi buforu wydruku na powitania systemu Windows.  Może być dowolnej usługi zainteresowań, ale w tym przykładzie mamy odwołują się do jednego z hello już istniejących usług, które są dołączone do systemu operacyjnego Windows hello.  Hello akcji alertu jest skonfigurowany tooexecute naszych elementu runbook w tym przykładzie i uruchom na powitania hybrydowy proces roboczy elementu Runbook, które są włączone na systemów docelowych hello.   

Witaj działanie elementu runbook kodu **pobieranie nazwy usługi z LA** przekonwertuje hello ciąg w formacie JSON na obiekt typu i filtr w elemencie hello *SvcDisplayName_CF* nazwę wyświetlaną hello tooextract hello Usługi systemu Windows i przekazany na powitania następnego działania, który sprawdzi hello zostanie zatrzymana przed podjęciem próby wykonania toorestart go.  *SvcDisplayName_CF* jest [niestandardowego pola](../log-analytics/log-analytics-custom-fields.md) utworzone w toodemonstrate analizy dzienników w tym przykładzie.

    $SearchResults = (ConvertFrom-Json $WebhookData.RequestBody).SearchResults.value
    $SearchResults.SvcDisplayName_CF  

Po zatrzymaniu usługi hello hello reguły alertów w analizy dzienników wykryje dopasowanie i wyzwolić elementu runbook hello i wysłać hello kontekst alertu toohello runbook. Hello runbook podejmie akcji tooverify hello usługa zostanie zatrzymana, i jeśli tak toorestart próba hello usługi i sprawdź jej prawidłowo uruchomić i powoduje hello danych wyjściowych.     

Można również nie masz obszar roboczy OMS automatyzacji konto połączone tooyour przypadku czy skonfigurować regułę alertu hello element webhook akcji tootrigger hello i skonfigurowania hello runbook tooconvert hello ciąg w formacie JSON i filtr na *. Właściwości SearchResult* następujące wskazówki hello wymienionych poniżej.    

## <a name="next-steps"></a>Następne kroki

* więcej informacji na temat alertów w analizy dzienników toolearn i toocreate, zobacz temat [alertów w analizy dzienników](../log-analytics/log-analytics-alerts.md).

* toounderstand tootrigger elementów runbook przy użyciu elementu webhook, zobacz temat [elementów webhook usługi Automatyzacja Azure](automation-webhooks.md).
