---
title: "Hybrydowy proces roboczy elementu Runbook: Zadanie elementu runbook kończy o stanie Suspended | Dokumentacja firmy Microsoft"
description: "Objawy przyczyny i rozwiązania dla błędu zakończenia zadania hybrydowy proces roboczy elementu Runbook."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 02c6606e-8924-4328-a196-45630c2255e9
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/17/2016
ms.author: magoedte
ms.openlocfilehash: 513a90d144e7ade9c21cd7f3b718578989702c25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-runbook-worker-a-runbook-job-terminates-with-a-status-of-suspended"></a>Hybrydowy proces roboczy elementu Runbook: zadanie elementu Runbook zostaje zakończone ze stanem Zawieszone
## <a name="summary"></a>Podsumowanie
Element runbook jest wstrzymana krótko po próby tooexecute on trzy razy. Istnieją warunki, które mogą przerwać runbook hello pomyślne zakończenie działania i hello pokrewne komunikat nie ma żadnych dodatkowych informacji i wskazujący przyczynę. Ten artykuł zawiera kroki rozwiązywania problemów powiązanych toohello hybrydowy proces roboczy elementu Runbook runbook wykonywania błędów.

Jeśli problem Azure nie jest opisany w tym artykule, odwiedź hello na forach platformy Azure [MSDN i hello przepełnienie stosu](https://azure.microsoft.com/support/forums/). Problem można umieścić na tych fora lub zbyt[ @AzureSupport w serwisie Twitter](https://twitter.com/AzureSupport). Ponadto można pliku żądania pomocy technicznej platformy Azure, wybierając **uzyskać pomoc techniczną** na powitania [pomocy technicznej platformy Azure](https://azure.microsoft.com/support/options/) lokacji.

## <a name="symptom"></a>Objaw
Wykonanie elementu Runbook nie powiedzie się i jest zwracany błąd powitania "hello akcji zadania"Uaktywnij"nie można uruchomić, ponieważ hello proces został nieoczekiwanie zatrzymany. Akcja zadania Hello podjęto próbę 3 razy".

## <a name="cause"></a>Przyczyna
Istnieje kilka możliwych przyczyn tego błędu hello: 

1. Witaj hybrydowy proces roboczy jest używany serwer proxy lub Zapora
2. Witaj komputera hello hybrydowy proces roboczy jest uruchomiona na ma mniejszą niż minimalne wymagania dotyczące sprzętu hello [wymagania](automation-hybrid-runbook-worker.md#hybrid-runbook-worker-requirements) 
3. elementy runbook Hello nie można uwierzytelnić z zasobów lokalnych

## <a name="cause-1-hybrid-runbook-worker-is-behind-proxy-or-firewall"></a>Przyczyna 1: Hybrydowy proces roboczy elementu Runbook jest używany serwer proxy lub Zapora
powitalne komputera Hello hybrydowy proces roboczy elementu Runbook jest uruchomiony na się za serwerem zapory lub serwera proxy i dostępu sieciowego ruchu wychodzącego nie mogą być dozwolone lub prawidłowo skonfigurowane.

### <a name="solution"></a>Rozwiązanie
Sprawdź komputer hello ma too*.cloudapp wychodzący dostęp .net na porty 443, 9354 i 30000 30199. 

## <a name="cause-2-computer-has-less-than-minimum-hardware-requirements"></a>2 Przyczyna: Komputer ma mniej niż minimalne wymagania sprzętowe
Komputery z systemem hello hybrydowy proces roboczy elementu Runbook powinna spełniać hello minimalne wymagania sprzętowe przed oznaczeniem go toohost tej funkcji. W przeciwnym razie w zależności od wykorzystania zasobów hello innych procesów w tle i rywalizacji spowodowane przez elementy runbook podczas wykonywania, hello komputera będzie stają się nadmiernie wykorzystywany i spowodować opóźnienia zadania elementu runbook i przekroczeń limitu czasu. 

### <a name="solution"></a>Rozwiązanie
Najpierw upewnij się, komputer hello wyznaczonych funkcji hybrydowego procesu roboczego elementu Runbook hello toorun spełnia hello minimalne wymagania sprzętowe.  Jeśli tak, monitorować toodetermine wykorzystanie procesora CPU i pamięci korelacja hello wydajności procesów hybrydowy proces roboczy elementu Runbook i systemu Windows.  Jeśli brak pamięci lub dużego wykorzystania procesora CPU, może to wskazywać tooupgrade potrzeby hello lub dodać dodatkowych procesorów lub zwiększenie pamięci tooaddress hello zasobu "wąskie gardło" i usunąć błąd hello. Można również wybrać zasób różnych obliczeń obsługiwanych hello minimalne wymagania i skalowane, gdy wymaganego obciążenia wskazywać wzrost jest konieczne.         

## <a name="cause-3-runbooks-cannot-authenticate-with-local-resources"></a>Przyczyny 3: Elementy Runbook nie można uwierzytelnić z zasobów lokalnych
### <a name="solution"></a>Rozwiązanie
Sprawdź hello **Microsoft SMA** odpowiednie zdarzenie z opisem w dzienniku zdarzeń *Win32 proces został zakończony z kodem [4294967295]*.  Witaj przyczynę tego błędu jest nie jeszcze skonfigurowane uwierzytelnianie w elementach runbook lub określony hello poświadczeń Uruchom jako dla grupy hello hybrydowych procesów roboczych.  Zapoznaj się z tematem [uprawnienia elementów Runbook](automation-hybrid-runbook-worker.md#runbook-permissions) tooconfirm zostały prawidłowo skonfigurowane uwierzytelnianie na elementach runbook.  

