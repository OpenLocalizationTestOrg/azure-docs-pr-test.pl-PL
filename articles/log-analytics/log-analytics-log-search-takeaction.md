---
title: aaaUser akcji zainicjowanej przez Azure automatyzacji elementu Runbook w Log Analytics | Dokumentacja firmy Microsoft
description: "W tym artykule opisano, jak toorun element runbook usługi Automatyzacja z analizy dzienników wyszukiwanie wyników na żądanie."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/04/2017
ms.author: magoedte
ms.openlocfilehash: 53c25431572babd5fd54bf964e4683077e2a4c2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="take-action-with-an-automation-runbook-from-a-log-analytics-log-search-result"></a>Podjąć działania z element Runbook usługi Automatyzacja w wynikach wyszukiwania dziennika analizy dzienników

Wynik wyszukiwania dziennika w Azure Log Analytics można teraz wybrać **reakcję** toorun element runbook usługi Automatyzacja.  Witaj element runbook może służyć tooremediate hello problem lub wykonać niektóre akcje, takie jak zbieranie informacji dotyczących rozwiązywania problemów, Wyślij wiadomość e-mail lub Utwórz żądanie obsługi. 

## <a name="components-and-features-used"></a>Używane składniki i funkcje
* [Konto usługi Automatyzacja Azure](../automation/automation-offering-get-started.md)
* [Obszar roboczy analizy dzienników](../log-analytics/log-analytics-overview.md)

## <a name="tooinitiate-runbook-from-log-search"></a>Element runbook tooinitiate z dziennika wyszukiwania

Akcja tootake na zdarzenie oraz inicjowanie elementu runbook z wyników wyszukiwania dziennika, rozpoczyna się od utworzenia wyszukiwania dziennika i z wyników hello można wywołać elementu runbook na żądanie.  Można to osiągnąć z funkcji Wyszukaj dziennika hello w hello Azure lub [portalu OMS](../log-analytics/log-analytics-log-searches.md).  W tym przykładzie mamy wyszukiwaniu dziennika z hello portalu Azure z podstawowych pokaz tej funkcji.

1. W portalu Azure hello, w menu Centrum powitania kliknij **więcej usług** i wybierz **analizy dzienników**.  
2. W bloku analizy dzienników hello, wybierz obszar roboczy analizy dzienników oraz na powitania bloku obszaru roboczego wybierz **wyszukiwania dziennika**.  
3. W bloku dziennika wyszukiwania hello wyszukiwaniu dziennika.  
4. Wyniki wyszukiwania dziennika hello, kliknij hello elipsy toohello lewej strony pól hello i z menu podręczne hello, wybierz **zająć się**.<br><br> ![Wybierz podjąć akcję z wyników wyszukiwania](./media/log-analytics-log-search-takeaction/log-search-takeaction-menuoption.png) 
5. Hello podjęcia działania bloku, zaznacz **uruchomienia elementu runbook**, a na powitania **uruchomienia elementu runbook** bloku możesz wybrać toorun elementu runbook.  Można wybrać dowolnego elementu runbook w hello konta automatyzacji, które jest połączone toohello obszaru roboczego analizy dzienników.  Należy uwzględnić następujące hello:

    * Elementy Runbook są zorganizowane według znaczników
    * Wartości parametru wejściowego elementu Runbook można wybrać bezpośrednio z pola hello hello wyników wyszukiwania.  Wyświetlanie wszystkich hello dostępne pola z hello tooselect wynik z zostanie wyświetlona lista listy rozwijanej.  
    * Możesz wybrać element runbook hello toorun na [hybrydowy proces roboczy elementu runbook](../automation/automation-hybrid-runbook-worker.md) czy zostały zainstalowane na maszynie hello, która ma problem hello ma odpowiedniej grupy hybrydowego procesu roboczego elementu Runbook, zawiera tylko ten komputer jako członka.  Jeśli nazwa hello hello grupy hybrydowego procesu roboczego odpowiada nazwie hello hello komputera, który znajduje się w wyniku wyszukiwania dziennika hello, grupy hello jest wybierana automatycznie.    

6. Po kliknięciu **Uruchom**, bloku zadania elementu runbook hello spowoduje otwarcie tooallow możesz tooreview hello stan hello zadania.   

W przypadku wybrania elementu runbook, który został skonfigurowany toobe [wywoływane z alertu analizy dzienników](../automation/automation-invoke-runbook-from-omsla-alert.md), ma parametr wejściowy o nazwie **WebhookData** czyli **obiektu** typu.  Parametr wejściowy hello jest obowiązkowy, należy najpierw toopass hello wyszukiwania wyniki toohello runbook, umożliwia on konwertowanie ciągu w formacie JSON hello do typu obiektu, umożliwiając toofilter na określone elementy, które będzie odwoływać się w działania elementu runbook.  Aby to zrobić, wybierając **(obiekt) wynik wyszukiwania** z listy rozwijanej hello.<br><br> ![Wybierz obiekt danych elementu Webhook dla parametru elementu runbook](media/log-analytics-log-search-takeaction/select-runbook-and-properties.png)   
    
## <a name="next-steps"></a>Następne kroki

* Przejrzyj hello [analizy dzienników dziennika odwołanie wyszukiwania](log-analytics-search-reference.md) tooview wszystkie hello wyszukiwania pól i aspektów, które są dostępne w analizy dzienników.
* jak tooinvoke element runbook usługi Automatyzacja automatycznie, przejrzyj toolearn [wywołanie elementu runbook usługi Automatyzacja Azure z poziomu alertu analizy dzienników OMS](../automation/automation-invoke-runbook-from-omsla-alert.md).  
