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
ms.openlocfilehash: 7c6365b729d73f1c5b9bc57952b1723255d9e9f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="hybrid-runbook-worker-a-runbook-job-terminates-with-a-status-of-suspended"></a>Hybrydowy proces roboczy elementu Runbook: zadanie elementu Runbook zostaje zakończone ze stanem Zawieszone
## <a name="summary"></a>Podsumowanie
Element runbook został wstrzymany, wkrótce po próby wykonania jej trzy razy. Istnieją warunki, które mogą przerwać pomyślne zakończenie działania elementu runbook i powiązane komunikat nie ma żadnych dodatkowych informacji i wskazujący przyczynę. Ten artykuł zawiera kroki rozwiązywania problemów związanych z błędami wykonywania elementu runbook hybrydowy proces roboczy elementu Runbook.

Jeśli problem Azure nie jest opisany w tym artykule, odwiedź fora Azure na [MSDN i przepełnienie stosu](https://azure.microsoft.com/support/forums/). Możesz zamieścić problemu na tych fora lub do [ @AzureSupport w serwisie Twitter](https://twitter.com/AzureSupport). Ponadto można pliku żądania pomocy technicznej platformy Azure, wybierając **uzyskać pomoc techniczną** na [pomocy technicznej platformy Azure](https://azure.microsoft.com/support/options/) lokacji.

## <a name="symptom"></a>Objaw
Wykonanie elementu Runbook nie powiedzie się i zwrócony błąd to "akcji zadania, którego nie można uruchomić"Uaktywnij", ponieważ proces nieoczekiwanie zatrzymał się. Akcja zadania podjęto próbę 3 razy".

## <a name="cause"></a>Przyczyna
Istnieje kilka możliwych przyczyn tego błędu: 

1. Hybrydowy proces roboczy jest używany serwer proxy lub Zapora
2. Hybrydowy proces roboczy jest uruchomiona na komputerze są mniejsze niż minimalne wymagania dotyczące sprzętu [wymagania](automation-hybrid-runbook-worker.md#hybrid-runbook-worker-requirements) 
3. Elementy runbook nie mogą uwierzytelnić się przy użyciu lokalnych zasobów

## <a name="cause-1-hybrid-runbook-worker-is-behind-proxy-or-firewall"></a>Przyczyna 1: Hybrydowy proces roboczy elementu Runbook jest używany serwer proxy lub Zapora
Hybrydowy proces roboczy elementu Runbook na którym działa komputer znajduje się za serwerem zapory lub serwera proxy i dostępu sieciowego ruchu wychodzącego nie mogą być dozwolone lub prawidłowo skonfigurowane.

### <a name="solution"></a>Rozwiązanie
Sprawdź komputer ma dostęp ruchu wychodzącego do *. cloudapp.net na porty 443, 9354 i 30000 30199. 

## <a name="cause-2-computer-has-less-than-minimum-hardware-requirements"></a>2 Przyczyna: Komputer ma mniej niż minimalne wymagania sprzętowe
Komputery z systemem hybrydowy proces roboczy elementu Runbook powinna spełniać minimalne wymagania sprzętowe przed oznaczeniem go do obsługi tej funkcji. W przeciwnym razie w zależności od użycia zasobów innych procesów w tle i rywalizacji spowodowane przez elementy runbook podczas wykonywania, komputer będzie stają się nadmiernie wykorzystywany i spowodować opóźnienia zadania elementu runbook i przekroczeń limitu czasu. 

### <a name="solution"></a>Rozwiązanie
Najpierw upewnij się, że komputer wyznaczony do uruchomienia funkcji hybrydowego procesu roboczego elementu Runbook spełnia minimalne wymagania sprzętowe.  Jeśli tak, monitorowanie wykorzystania procesora CPU i pamięci, aby określić korelacja wydajności procesów hybrydowy proces roboczy elementu Runbook i Windows.  Brak pamięci lub dużego wykorzystania procesora CPU, może to oznaczać konieczność uaktualnienia lub dodać dodatkowych procesorów lub zwiększ ilość pamięci do adresów wąskie gardło zasobów i Usuń przyczynę błędu. Opcjonalnie zaznacz zasób różnych obliczeń, który może obsługiwać minimalne wymagania i skalowania, gdy wymaganego obciążenia wskazywać wzrost jest konieczne.         

## <a name="cause-3-runbooks-cannot-authenticate-with-local-resources"></a>Przyczyny 3: Elementy Runbook nie można uwierzytelnić z zasobów lokalnych
### <a name="solution"></a>Rozwiązanie
Sprawdź **Microsoft SMA** odpowiednie zdarzenie z opisem w dzienniku zdarzeń *Win32 proces został zakończony z kodem [4294967295]*.  Przyczyną tego błędu jest nie jeszcze skonfigurowane uwierzytelnianie w elementach runbook lub określony poświadczeń Uruchom jako grupy hybrydowych procesów roboczych.  Zapoznaj się z tematem [uprawnienia elementów Runbook](automation-hybrid-runbook-worker.md#runbook-permissions) o potwierdzenie zostały prawidłowo skonfigurowane uwierzytelnianie na elementach runbook.  

