---
title: "Konto usługi Automatyzacja Azure z analizy dzienników aaaUnlink | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera omówienie sposobu toounlink Twojego automatyzacji Azure konta z obszarem roboczym pakietu OMS."
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
ms.openlocfilehash: 3ec0745673f6a872538d33023a7a1d2bb1d18ec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toounlink-your-automation-account-from-a-log-analytics-workspace"></a>Jak toounlink Twojego automatyzacji konta z obszaru roboczego analizy dzienników

Automatyzacja Azure umożliwia integrację z analizy dzienników toonot tylko obsługę aktywnego monitorowania zadań elementu runbook dla wszystkich kont automatyzacji, ale jest również wymagany podczas importowania hello następujące rozwiązania, które są zależne od analizy dzienników:

* [Zarządzanie aktualizacjami](../operations-management-suite/oms-solution-update-management.md)
* [Śledzenie zmian](../log-analytics/log-analytics-change-tracking.md)
* [Uruchamiania/zatrzymywania maszyn wirtualnych w godzinach](automation-solution-vm-management.md)
 
Jeśli zdecydujesz się, że nie chcesz już toointegrate Twojego konta automatyzacji z analizy dzienników można odłączyć konta bezpośrednio z hello portalu Azure.  Zanim będziesz kontynuować, należy najpierw rozwiązań hello tooremove wspomniano wcześniej, w przeciwnym razie ten proces nie będzie mógł kontynuować.  Przejrzyj temat powitania dla danego rozwiązania hello zaimportowano toounderstand hello kroki wymagane tooremove go.  

Po usunięciu tych rozwiązań można wykonywać następujące czynności toounlink hello Twoje konto usługi Automatyzacja.

## <a name="unlink-workspace"></a>Rozłącz obszaru roboczego

1. Hello portalu Azure, otwórz Twoje konto usługi Automatyzacja i w bloku konta usługi Automatyzacja hello, w bloku konta hello, wybierz **odłączyć obszaru roboczego**.<br><br> ![Odłącz obszar roboczy](media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)<br><br>  
2. W bloku obszaru roboczego Rozłącz hello, kliknij **odłączyć worksapce**.<br><br> ![Rozłącz bloku obszaru roboczego](media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png).<br><br>  Zostanie wyświetlony monit zweryfikowaniu, że chcesz tooproceed.<br><br>
3. Podczas automatyzacji Azure próbuje konta hello toounlink obszaru roboczego analizy dzienników, możesz śledzić postępy hello w obszarze **powiadomienia** hello menu.

Użycie rozwiązania zarządzania aktualizacjami hello Opcjonalnie możesz hello tooremove następujące elementy, które nie są już potrzebne po usunięciu hello rozwiązania.

* Harmonogramy aktualizacji.  Będzie mieć nazwy są zgodne z wdrożenia aktualizacji hello utworzone)

* Hybrydowe utworzone dla rozwiązania hello grupy procesu roboczego.  Każda będzie miała nazwę podobnie zbyt machine1.contoso.com_9ceb8108 - 26 c 9-4051-b6b3-227600d715c8).

Jeśli maszyn wirtualnych uruchamiania i zatrzymywania hello jest używany podczas rozwiązania poza godzinami szczytu, opcjonalnie można hello tooremove następujące elementy, które nie są już potrzebne po usunięciu hello rozwiązania.

* Uruchamianie i zatrzymywanie harmonogramy runbook maszyny Wirtualnej 
* Uruchamianie i zatrzymywanie elementów runbook maszyny Wirtualnej
* Zmienne   

## <a name="next-steps"></a>Następne kroki

tooreconfigure Twojego toointegrate konta automatyzacji o OMS Log Analytics, zobacz [przekazuj strumienie zadania i stan zadania z automatyzacji tooLog Analytics (OMS)](automation-manage-send-joblogs-log-analytics.md). 
