---
title: "Użytkownik zainicjował akcję elementu Runbook usługi Automatyzacja Azure w Log Analytics | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób uruchamiania elementu runbook automatyzacji z analizy dzienników wyszukiwania wyników na żądanie."
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
ms.openlocfilehash: ff938697add98f3d21b4971175432335ee2e39ba
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="take-action-with-an-automation-runbook-from-a-log-analytics-log-search-result"></a>Podjąć działania z element Runbook usługi Automatyzacja w wynikach wyszukiwania dziennika analizy dzienników

Wynik wyszukiwania dziennika w Azure Log Analytics można teraz wybrać **reakcję** uruchomić element runbook usługi Automatyzacja.  Element runbook może służyć do rozwiązania problemu lub niektóre akcje, takie jak zbierać informacje dotyczące rozwiązywania problemów, Wyślij wiadomość e-mail lub Utwórz żądanie obsługi. 

## <a name="components-and-features-used"></a>Używane składniki i funkcje
* [Konto usługi Automatyzacja Azure](../automation/automation-offering-get-started.md)
* [Obszar roboczy analizy dzienników](../log-analytics/log-analytics-overview.md)

## <a name="to-initiate-runbook-from-log-search"></a>Aby zainicjować element runbook z dziennika wyszukiwania

Do wykonania akcji na zdarzenia i inicjowania elementu runbook z wyników wyszukiwania dziennika, rozpoczyna się od utworzenia wyszukiwania dziennika i z wyników można wywołać elementu runbook na żądanie.  Można to osiągnąć przez funkcję wyszukiwania dziennika w platformy Azure lub [portalu OMS](../log-analytics/log-analytics-log-searches.md).  W tym przykładzie mamy wyszukiwaniu dziennika z portalu Azure z podstawowych pokaz tej funkcji.

1. W portalu Azure, w menu centralnym kliknij **więcej usług** i wybierz **analizy dzienników**.  
2. W bloku analizy dzienników wybierz obszaru roboczego analizy dzienników, a następnie w bloku obszaru roboczego wybierz **wyszukiwania dziennika**.  
3. W bloku dziennika wyszukiwania wyszukiwaniu dziennika.  
4. Z dziennika wyniki wyszukiwania, kliknij przycisk wielokropka z lewej strony pól i z menu podręcznego wybierz **zająć się**.<br><br> ![Wybierz podjąć akcję z wyników wyszukiwania](./media/log-analytics-log-search-takeaction/log-search-takeaction-menuoption.png) 
5. W bloku podjęcia akcji wybierz **uruchomienia elementu runbook**i na **uruchomienia elementu runbook** bloku możesz wybrać uruchomienia elementu runbook.  Można wybrać dowolnego elementu runbook w ramach konta automatyzacji, który jest połączony z obszaru roboczego analizy dzienników.  Pamiętaj o następujących kwestiach:

    * Elementy Runbook są zorganizowane według znaczników
    * Można wybrać wartości parametru wejściowego Runbook bezpośrednio w polu wyników wyszukiwania.  Wyświetlanie wszystkich dostępnych pól z wyników, aby dokonać wyboru spośród zostanie wyświetlona lista listy rozwijanej.  
    * Można uruchomić elementu runbook na [hybrydowy proces roboczy elementu runbook](../automation/automation-hybrid-runbook-worker.md) zainstalowanego na komputerze, który ma problem ma odpowiedniej grupy hybrydowego procesu roboczego elementu Runbook, zawiera tylko ten komputer jako członka.  Jeśli nazwa grupy hybrydowego procesu roboczego odpowiada nazwie komputera, który znajduje się w wynikach wyszukiwania dziennika, grupa jest wybierana automatycznie.    

6. Po kliknięciu **Uruchom**, pozwala sprawdzać stan zadania zostanie otwarty blok zadania elementu runbook.   

Wybranie elementu runbook, który został skonfigurowany tak, aby [wywoływane z alertu analizy dzienników](../automation/automation-invoke-runbook-from-omsla-alert.md), ma parametr wejściowy o nazwie **WebhookData** czyli **obiektu** typu.  Parametr wejściowy jest obowiązkowy, należy najpierw przekazać wyniki wyszukiwania do elementu runbook, więc można go przekonwertować ciąg w formacie JSON na typu obiektu, dzięki czemu można filtrować na określone elementy, które będzie odwoływać się w działania elementu runbook.  Aby to zrobić, wybierając **(obiekt) wynik wyszukiwania** z listy rozwijanej.<br><br> ![Wybierz obiekt danych elementu Webhook dla parametru elementu runbook](media/log-analytics-log-search-takeaction/select-runbook-and-properties.png)   
    
## <a name="next-steps"></a>Następne kroki

* Przegląd [analizy dzienników dziennika odwołanie wyszukiwania](log-analytics-search-reference.md) do wyświetlenia wszystkich pól wyszukiwania i aspektów, które są dostępne w analizy dzienników.
* Aby dowiedzieć się, jak automatycznie Wywołaj element runbook usługi Automatyzacja, przejrzyj [wywołanie elementu runbook usługi Automatyzacja Azure z poziomu alertu analizy dzienników OMS](../automation/automation-invoke-runbook-from-omsla-alert.md).  