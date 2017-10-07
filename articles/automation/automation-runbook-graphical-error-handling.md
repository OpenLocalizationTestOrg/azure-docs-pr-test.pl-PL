---
title: "Obsługa w graficznych elementów runbook usługi Automatyzacja Azure aaaError | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób obsługi logiki w graficznych elementów runbook usługi Automatyzacja Azure tooimplement błędów."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/26/2016
ms.author: magoedte
ms.openlocfilehash: b9ff01361d2ebd9c0174b074a7a290b1cc2fd1c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="error-handling-in-azure-automation-graphical-runbooks"></a>Obsługa błędów w graficznych elementach Runbook w usłudze Azure Automation

Tooconsider główny projekt klucza runbook identyfikuje różnych problemów, które mogą wystąpić elementu runbook. Przykładowe problemy to powodzenie, oczekiwane stany błędu i nieoczekiwane warunki błędu.

Elementy runbook powinny zawierać obsługę błędów. toovalidate hello dane wyjściowe działania lub obsługi błędu z graficznych elementów runbook, można użyć działania kodu programu Windows PowerShell, zdefiniuj logikę warunkową hello łącze dane wyjściowe działania hello lub zastosowania innej metody.          

Często w przypadku błąd niepowodujący, która występuje podczas działania elementu runbook, niezależnie od błędu hello są przetwarzane działalności, która jest zgodna. Błąd Hello jest prawdopodobnie toogenerate wyjątek, ale toorun nadal uzyskuje zezwolenie na powitania następnego działania. Jest to hello sposób, że programu PowerShell jest zaprojektowana toohandle błędy.    

Przerywanie Hello typów błędów środowiska PowerShell, które mogą wystąpić podczas wykonywania lub niepowodujący. Hello różnice między Trwa przerywanie działania i niepowodujący błędy są następujące:

* **Trwa przerywanie wykonywania błąd**: poważny błąd podczas wykonywania, która całkowicie zatrzymuje hello polecenia (lub wykonywanie skryptu). Do przykładów należą nieistniejące polecenia cmdlet, błędy składniowe, które uniemożliwiają wykonanie polecenia cmdlet, lub inne błędy krytyczne.

* **Przerywanie bez błędu**: z systemem innym niż poważny błąd, który umożliwia wykonanie toocontinue pomimo awarii hello. Do przykładów należą błędy operacyjne, takie jak niemożność odnalezienia pliku i problemy z uprawnieniami.

Graficzne elementy runbook automatyzacji Azure ulepszono z obsługi błędów tooinclude możliwości hello. Teraz możesz przekształcać wyjątki w błędy niepowodujące zakończenia oraz tworzyć linki błędów między działaniami. Ten proces umożliwia twórcy elementu runbook toocatch błędy i Zarządzaj warunkami rzeczywista lub nieoczekiwany.  

## <a name="when-toouse-error-handling"></a>Podczas obsługi błędów toouse

Zawsze, gdy jest krytyczny działania, która zgłasza błąd lub wyjątek, jest ważne tooprevent hello następne działanie w elemencie runbook toohandle i przetwarzania błędu hello odpowiednio. Jest to bardzo ważne zwłaszcza wtedy, gdy Twoje elementy runbook obsługują proces operacji usługi lub biznesowy.

Dla każdego działania, które mogą wytwarzać błąd hello Autor elementów runbook można dodać Błąd łącza tooany innych działań.  działanie docelowe Hello mogą być dowolnego typu, łącznie z czynności kodu wywoływanie polecenia cmdlet, wywoływania innego elementu runbook i tak dalej.

Ponadto działania docelowego hello również może mieć linki wychodzące. Mogą to być zwykłe linki lub linki błędów. Oznacza to, że autor elementów runbook hello można zaimplementować złożonej logiki obsługi błędów bez ponowne sortowanie tooa działania kodu. Witaj zalecane rozwiązaniem jest toocreate dedykowanych runbook obsługi błędów z typowych funkcji, ale nie jest obowiązkowe. Logika obsługi błędów w działaniu kodu programu PowerShell, który nie jest hello tylko opcja.  

Na przykład rozważmy elementu runbook, który próbuje toostart maszynę Wirtualną i zainstalować aplikację na nim. Jeśli hello maszyny Wirtualnej nie uruchamia się poprawnie, wykonuje dwie czynności:

1. Wysyła powiadomienie o tym problemie.
2. Uruchamia inny element runbook, który automatycznie aprowizuje nową maszynę wirtualną.

Jedno rozwiązanie jest toohave łącza błąd działania tooan dojść do kroku 1. Na przykład można połączyć hello **Write-Warning** działania tooan polecenia cmdlet w kroku 2, takich jak hello **Start AzureRmAutomationRunbook** polecenia cmdlet.

To zachowanie do użycia w wielu elementów runbook można również generalize umieszczenie tych dwóch działań w oddzielnych błąd obsługi runbook i poniższe wskazówki hello sugerowane wcześniej. Przed wywołaniem elementu runbook to obsługa błędów, można utworzyć niestandardowe wiadomość hello danych w oryginalnej runbook hello, a następnie przekaż go jako element parametru toohello obsługi błędów.

## <a name="how-toouse-error-handling"></a>Sposób obsługi błędów toouse

Każde działanie ma ustawienie konfiguracji umożliwiające przekształcenie wyjątków w błędy niepowodujące zakończenia. To ustawienie jest domyślnie wyłączone. Zaleca się włączenie tego ustawienia na żadnej aktywności, w którym ma toohandle błędy.  

Przez włączenie tej konfiguracji, jest zapewnienie są traktowane jako błędy niepowodujący zakończenia i niepowodujący błędy w działaniu hello i mogą być obsługiwane z łączem błędu.  

Po skonfigurowaniu tego ustawienia, możesz utworzyć działanie, które obsługuje hello błędu. Jeśli działanie tworzy wszelkie błędy, następnie hello wychodzących błąd, który łączy zostaną wykonane, a hello regularnego połączenia nie są nawet wtedy, gdy działanie hello tworzy także regularne danych wyjściowych.<br><br> ![Przykład linka błędu elementu runbook usługi Automation](media/automation-runbook-graphical-error-handling/error-link-example.png)

W hello poniższy przykład element runbook pobiera zmienna, która zawiera nazwę komputera hello maszyny wirtualnej. Podejmuje maszyny wirtualnej hello toostart z hello następnego działania.<br><br> ![Przykład obsługi błędu elementu runbook usługi Automation](media/automation-runbook-graphical-error-handling/runbook-example-error-handling.png)<br><br>      

Witaj **Get-AutomationVariable** działania i **Start AzureRmVm** są tooerrors wyjątki tooconvert skonfigurowany.  Jeśli występują problemy z uzyskiwaniem hello zmiennej lub początkowy hello maszyny Wirtualnej, a następnie generowane są błędy.<br><br> ![Ustawienia działania obsługi błędu elementu runbook usługi Automation](media/automation-runbook-graphical-error-handling/activity-blade-convertexception-option.png)

Błąd łącza przepływać z tych działań tooa pojedynczego **błąd zarządzania** działania (działanie kodu). To działanie jest konfigurowana proste wyrażenie programu PowerShell, który używa hello *Throw* toostop — słowo kluczowe przetwarzania, wraz z *$Error.Exception.Message* tooget hello komunikat, który opisuje hello Bieżący wyjątek.<br><br> ![Przykład kodu obsługi błędu elementu runbook usługi Automation](media/automation-runbook-graphical-error-handling/runbook-example-error-handling-code.png)


## <a name="next-steps"></a>Następne kroki

* toolearn więcej informacji na temat łącza i typy łączy w graficznych elementów runbook, zobacz [tworzenia graficznego automatyzacji Azure](automation-graphical-authoring-intro.md#links-and-workflow).

* więcej informacji o wykonanie elementu runbook, w jaki sposób toomonitor zadań i inne szczegółowe informacje techniczne, zobacz toolearn [śledzić zadania elementu runbook](automation-runbook-execution.md).
