---
title: "Odłączanie konta usługi Automatyzacja Azure Log Analytics | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera omówienie sposobu odłączania Twoje konto usługi Automatyzacja Azure z obszarem roboczym pakietu OMS."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: how-to-article
ms.date: 02/07/2017
ms.author: magoedte
ms.openlocfilehash: 56b09c2cfc14813b5efcb364c580787fec1bf639
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-unlink-your-automation-account-from-a-log-analytics-workspace"></a>Sposobu odłączania Twoje konto usługi Automatyzacja z obszaru roboczego analizy dzienników

Automatyzacja Azure umożliwia integrację z analizy dzienników umożliwia nie tylko aktywnego monitorowania zadań elementu runbook dla wszystkich kont automatyzacji, ale jest również wymagany podczas importowania następujące rozwiązania, które są zależne od analizy dzienników:

* [Zarządzanie aktualizacjami](../operations-management-suite/oms-solution-update-management.md)
* [Śledzenie zmian](../log-analytics/log-analytics-change-tracking.md)
* [Uruchamiania/zatrzymywania maszyn wirtualnych w godzinach](automation-solution-vm-management.md)
 
Jeśli zdecydujesz się, że chcesz zintegrować Twoje konto usługi Automatyzacja z analizy dzienników nie będzie można odłączyć konta bezpośrednio z portalu Azure.  Zanim będziesz kontynuować, musisz najpierw usunąć rozwiązania wspomniano wcześniej, w przeciwnym razie ten proces nie będzie mógł kontynuować.  Przejrzyj temat dla określonego rozwiązania, które zostały zaimportowane, aby zrozumieć kroki wymagane w celu usunięcia go.  

Po usunięciu tych rozwiązań, które można wykonać następujące kroki, aby odłączyć Twoje konto usługi Automatyzacja.

## <a name="unlink-workspace"></a>Rozłącz obszaru roboczego

1. W portalu Azure, otwórz Twoje konto usługi Automatyzacja, a w bloku konta usługi Automatyzacja w bloku konta wybierz **odłączyć obszaru roboczego**.<br><br> ![Odłącz obszar roboczy](media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)<br><br>  
2. W bloku Rozłącz obszaru roboczego kliknij **odłączyć worksapce**.<br><br> ![Rozłącz bloku obszaru roboczego](media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png).<br><br>  Zostanie wyświetlony monit sprawdzający, czy chcesz kontynuować.<br><br>
3. Gdy usługi Automatyzacja Azure usiłuje odłączyć konto obszaru roboczego analizy dzienników, możesz śledzić postępy w obszarze **powiadomienia** z menu.

Użycie rozwiązania zarządzania aktualizacjami, opcjonalnie możesz usunąć następujące elementy, które nie są już potrzebne po usunięciu rozwiązania.

* Harmonogramy aktualizacji.  Będzie mieć nazwy są zgodne z wdrożenia aktualizacji, który utworzono)

* Hybrydowe utworzone dla rozwiązania grupy procesu roboczego.  Każda będzie miała nazwę podobnie do machine1.contoso.com_9ceb8108 - 26 c 9-4051-b6b3-227600d715c8).

Jeśli używasz uruchamiania/zatrzymywania maszyn wirtualnych podczas rozwiązania poza godzinami szczytu, opcjonalnie może chcesz usunąć następujące elementy, które nie są już potrzebne po usunięciu rozwiązania.

* Uruchamianie i zatrzymywanie harmonogramy runbook maszyny Wirtualnej 
* Uruchamianie i zatrzymywanie elementów runbook maszyny Wirtualnej
* Zmienne   

## <a name="next-steps"></a>Następne kroki

Aby zmienić konfigurację konta automatyzacji do integracji z analizy dzienników OMS, zobacz [przekazuj strumienie zadania i stan zadania z automatyzacji analizy dzienników (OMS)](automation-manage-send-joblogs-log-analytics.md). 