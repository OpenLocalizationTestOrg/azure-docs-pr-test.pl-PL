---
title: "aaaAlert zarządzania w programie Microsoft monitoring produktów | Dokumentacja firmy Microsoft"
description: "Alert wskazuje niektórych problem, który wymaga uwagi ze strony administratora.  W tym artykule opisano różnice hello w sposób alerty są tworzone i zarządzane w System Center Operations Manager (SCOM) i analizy dzienników oraz podano najlepszych rozwiązań dzięki wykorzystaniu hello dwóch produktów w strategii zarządzania alertami hybrydowego."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 6572c3f8-78ca-4fa9-8fe1-d0b488590788
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: bwren
ms.openlocfilehash: 526a3d92f3b6a5d6dec2f3979a934cc94c13f2e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-alerts-with-microsoft-monitoring"></a>Zarządzanie alertami z monitorowania firmy Microsoft
Alert wskazuje niektórych problem, który wymaga uwagi ze strony administratora.  Istnieją różne różnice między programu System Center Operations Manager (SCOM) i analizy dzienników w Operations Management Suite (OMS) pod względem sposobu tworzenia alertów, jak są zarządzane i analizowane i jak otrzymasz powiadomienie, że krytyczne problem został Wykryto.

## <a name="alerts-in-operations-manager"></a>Alerty w programie Operations Manager
Alerty w SCOM są generowane przez poszczególne reguły i monitory tooindicate konkretnego problemu.  Monitor mogą generować alert po przechodzi do stanu błędu, gdy reguła może generować alert tooindicate niektórych krytyczny problem, który nie jest bezpośrednio powiązane toohello kondycji zarządzanego obiektu.  Pakiety administracyjne obejmują wiele przepływów pracy, które tworzą alertów dla aplikacji hello lub usługi, które zarządzają.  Część hello proces konfigurowania nowego pakietu administracyjnego dostrajania go tooensure, że nie otrzyma nadmiernego alerty dotyczące problemów, które nie zostały uznane za krytyczne.

![Widok alertów programu SCOM](media/operations-management-suite-monitoring-alerts/scom-alert-view.png)

SCOM zapewnia pełną zarządzania alertami alerty o stanie, który może zostać zmieniona przez Administratorzy pracują tooresolve hello problem.  Po rozwiązaniu problemu hello hello administrator ustawi hello tooclosed alertów po tym czasie będzie już wyświetlane w widokach Wyświetlanie aktywnych alertów.  Alerty generowane przez monitory mogą automatycznie rozwiązana po hello monitor zwraca tooa dobrej kondycji.

![Stan alertu](media/operations-management-suite-monitoring-alerts/scom-alert-status.png)

## <a name="alerts-in-log-analytics"></a>Alerty w analizy dzienników
Alert w analizy dzienników jest tworzona na podstawie zapytania dziennika, który jest automatycznie uruchamiany w regularnych odstępach czasu.  Wszelkie zapytania dziennika można utworzyć zasady alertu.  Jeśli hello zapytanie zwraca wyników spełniających kryteria hello, tworzona jest alert.  Może to być określonej kwerendy, która tworzy alert po wykryciu określonego zdarzenia lub można użyć zapytania bardziej ogólne czy szuka dowolnego zdarzenia błędu powiązane tooa określonej aplikacji.

Alerty analizy dziennika są zapisywane repozytorium OMS toohello jako zdarzenie i może zostać pobrany z zapytania dziennika.  Nie mają stanu, takich jak zdarzenia programu SCOM, dzięki czemu można wskazać, kiedy hello problem został rozwiązany.

![OMS alert](media/operations-management-suite-monitoring-alerts/oms-alert.png)

Gdy SCOM jest używany jako źródło danych analizy dzienników, SCOM alerty są zapisywane toohello OMS repozytorium, ponieważ są one tworzone i modyfikowane.  

![Alert programu SCOM](media/operations-management-suite-monitoring-alerts/scom-alert.png)

Witaj [rozwiązania zarządzania alertami](http://technet.microsoft.com/library/mt484092.aspx) zawiera podsumowanie aktywne alerty i kilka typowych kwerend tooretrieve różne zestawy alertów.  Zapewnia bardziej efektywną analizy alertów niż raportu w SCOM.  Można przechodzenie z hello podsumowania toodetailed danych i tworzenie zapytań ad hoc tooretrieve różne zestawy alertów.

![Rozwiązanie do zarządzania alertu](media/operations-management-suite-monitoring-alerts/alert-management.png)

## <a name="notifications"></a>Powiadomienia
Powiadomienia w SCOM wysłać poczty lub tekstu w odpowiedzi tooalerts, odpowiadających określonym kryteriom.  Można utworzyć subskrypcje powiadomień różnych, które mają różne osoby powiadomienie w zależności od takich kryteriów, jak obiekt hello monitorowana, hello ważności alertu hello, hello rodzaju problem, którego wykryć lub hello czasu dnia.

Kilka subskrypcje mogą być używane tooimplement strategię pełną powiadomień dla dużej liczby pakietów administracyjnych.

![Alerty programu SCOM](media/operations-management-suite-monitoring-alerts/alerts-overview-scom.png)

Analiza dzienników mogą wyświetlać powiadomienia pocztą utworzony alert przez ustawienie akcji powiadomienia e-mail dla każdego [reguły alertu](http://technet.microsoft.com/library/mt614775.aspx).  Nie ma możliwości hello programu SCOM hello subskrybować alerty toomultiple przy użyciu jednej reguły.  Należy również toocreate własne reguły alertu ponieważ OMS nie zapewnia żadnych wstępnie skonfigurowane.

![Alerty usługi Log Analytics](media/operations-management-suite-monitoring-alerts/alerts-overview-oms.png)

Nie można całkowicie zarządzać SCOM alertów w analizy dzienników jednak ponieważ można modyfikować tylko je w konsoli operacje hello.  Analiza dzienników jest przydatna jako część zarządzania alertami jednak przetwarzania dla zapewnienie tego samego SCOM narzędzi analizy nie ma.

## <a name="alert-remediation"></a>Korygowanie alertu
[Korygowanie](http://technet.microsoft.com/library/mt614775.aspx) odwołuje się tooan próba tooautomatically poprawne hello problem identyfikowana na podstawie alertu.

SCOM pozwala toorun diagnostyki i odzyskiwania w monitorze tooa odpowiedzi wprowadzania złej kondycji.  Dzieje się to monitor toohello jednoczesne tworzenie hello alertu.  Elementy diagnostyki i przywracania zwykle są zaimplementowane jako skryptu uruchamianego na powitania agenta.  Toogather prób diagnostycznych więcej informacji na temat hello wykrył problem podczas odzyskiwania prób toocorrect hello problem.

Analiza dzienników umożliwia toostart [runbook usługi Automatyzacja Azure](https://azure.microsoft.com/documentation/services/automation/) lub wywołanie elementu webhook w odpowiedzi tooa analizy dzienników alertu.  Elementy Runbook mogą zawierać złożonej logiki zaimplementowany w programie PowerShell.  Witaj skrypt jest uruchamiany na platformie Azure i można uzyskać dostępu do żadnych zasobów platformy Azure lub dostępnych zasobów zewnętrznych z chmury hello.  Automatyzacja Azure ma elementy runbook tooexecute możliwości hello na serwerze w lokalnym centrum danych, ale ta funkcja nie jest obecnie dostępna podczas uruchamiania elementu runbook hello w odpowiedzi tooLog Analytics alerty.

Zarówno odzyskiwania w SCOM i elementów runbook w pakiecie OMS może zawierać skryptów programu PowerShell, ale odzyskiwania są trudniejsze toocreate i zarządzać nimi, ponieważ musi być zawarty w pakiecie administracyjnym.  Elementy Runbook są przechowywane w automatyzacji Azure, która dostarcza funkcje do tworzenia, testowania i zarządzanie elementów runbook.

Jeśli używasz programu SCOM jako źródła danych do analizy dzienników można utworzyć analizy dzienników alertów za pomocą tooretrieve zapytania dziennika SCOM alertów przechowywanych w hello repozytorium OMS.  Dzięki temu możesz toorun runbook usługi Automatyzacja Azure w odpowiedzi tooa SCOM alertu.  Oczywiście ponieważ hello runbook będzie uruchamiany na platformie Azure, nie będzie działało strategię odzyskiwania problemy z lokalnymi.

## <a name="next-steps"></a>Następne kroki
* Szczegóły dotyczące hello [alertów w System Center Operations Manager (SCOM)](https://technet.microsoft.com/library/hh212913.aspx).

