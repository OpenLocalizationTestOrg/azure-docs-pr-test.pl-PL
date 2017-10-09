---
title: "aaaScheduler wysokiej dostępności i niezawodności"
description: "Harmonogram wysokiej dostępności i niezawodności"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 5ec78e60-a9b9-405a-91a8-f010f3872d50
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/16/2016
ms.author: deli
ms.openlocfilehash: 5c9efb333eb42b393adc5deea657ca99206d425e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-high-availability-and-reliability"></a>Harmonogram wysokiej dostępności i niezawodności
## <a name="azure-scheduler-high-availability"></a>Harmonogram systemu Azure wysokiej dostępności
Jako podstawowa usługi platformy Azure Harmonogram systemu Azure zapewnia wysoką dostępność i zawiera zarówno wdrożenia usługi geograficznie nadmiarowego i regionalnych geo zadania replikacji.

### <a name="geo-redundant-service-deployment"></a>Wdrożenie usługi geograficznie nadmiarowego
Harmonogram systemu Azure jest dostępna za pośrednictwem hello interfejsu użytkownika w niemal każdego regionu geograficznego, który jest obecnie na platformie Azure. Witaj lista regionów, które Harmonogram systemu Azure jest dostępna w [wymienione w tym miejscu](https://azure.microsoft.com/regions/#services). Jeśli centrum danych w regionie hostowanej staje się niedostępny, możliwości trybu failover hello Azure harmonogramu są tak, aby usługa hello jest dostępna z innej centrum danych.

### <a name="geo-regional-job-replication"></a>Replikacja geograficzna regionalne zadania
Witaj jest nie tylko frontonu, dostępne dla żądań zarządzania, ale własne stanowisko jest również replikacją geograficzną Harmonogram systemu Azure. Przypadku wystąpienia awarii w jeden region, harmonogram Azure awaryjnie i gwarantuje, że to zadanie hello jest uruchamiany z innym centrum danych w regionie geograficznym sparowanego hello.

Na przykład jeśli po utworzeniu zadania w południowo-środkowe stany Harmonogram systemu Azure automatycznie replikuje tego zadania w północno-środkowe Stany. Jeśli wystąpi awaria w południowo-środkowe stany, harmonogram systemu Azure zapewnia, że to zadanie hello jest uruchamiany z północno-środkowe Stany. 

![][1]

W związku z tym harmonogram systemu Azure zapewnia, że Twoje danych pozostaje w hello szerszych tym samym regionie geograficznym w razie awarii usługi Azure. W związku z tym nie należy zduplikowane Twoje zadania tylko tooadd wysokiej dostępności — Harmonogram systemu Azure automatycznie zapewnia funkcje wysokiej dostępności dla zadań.

## <a name="azure-scheduler-reliability"></a>Niezawodność Harmonogram systemu Azure
Harmonogram Azure gwarancje własne wysokiej dostępności i ma inny sposób utworzyć toouser zadania. Na przykład zadanie może wywoływać punktu końcowego HTTP, która jest niedostępna. Harmonogram systemu Azure niemniej próbuje tooexecute swoją pracę pomyślnie, zapewniając toodeal alternatywnych opcji z błędem. Harmonogram systemu Azure dzieje się tak na dwa sposoby:

### <a name="configurable-retry-policy-via-retrypolicy"></a>Można skonfigurować zasady spróbuj ponownie za pomocą "retryPolicy"
Harmonogram systemu Azure umożliwia tooconfigure zasady ponawiania. Domyślnie jeśli zadanie nie powiedzie się, harmonogram próbuje zadania hello ponownie cztery razy więcej, w odstępach 30 sekund. Można skonfigurować ponownie ten ponawiania zasad toobe skuteczniejsze (na przykład dziesięć razy, w odstępach 30 sekund) lub im (na przykład dwa razy codziennie.)

Jako przykład kiedy może to ułatwić może utworzyć zadania uruchamiane raz w tygodniu, który wywołuje punkt końcowy HTTP. Jeśli punkt końcowy hello HTTP działa przez kilka godzin po uruchomieniu zadania, nie możesz toowait jeden tydzień w przypadku toorun zadania hello ponownie ponieważ nawet hello domyślne zasady ponawiania z zakończy się niepowodzeniem. W takich przypadkach mogą skonfigurujesz tooretry zasady ponawiania standardowe hello co trzy godziny (na przykład) zamiast co 30 sekund.

toolearn jak tooconfigure zasady ponawiania odwoływać się za[retryPolicy](scheduler-concepts-terms.md#retrypolicy).

### <a name="alternate-endpoint-configurability-via-erroraction"></a>Alternatywne konfigurowalne punktu końcowego za pośrednictwem "errorAction"
Jeśli hello endpoint docelowego dla zadania Harmonogram systemu Azure jest nieosiągalny, harmonogram systemu Azure powraca punktu końcowego toohello alternatywny obsługi błędów po wykonaniu jej zasady ponawiania. Jeśli skonfigurowano punkcie końcowym alternate obsługi błędów, harmonogram systemu Azure wywołuje go. Z punktem końcowym alternatywne własne zadania są wysokiej dostępności jest w fazie hello awarii.

Na przykład w diagramie hello poniżej Harmonogram systemu Azure następuje jego toohit zasady ponawiania usługi sieci web w Nowym Jorku. Po hello ponawia próby kończyć się niepowodzeniem, sprawdza, czy jest alternatywny. Następnie przejdzie do przodu i uruchamia wysyłania żądań toohello alternatywny z hello takie same zasady ponawiania.

![][2]

Należy pamiętać, że hello zasady ponawiania z tym samym stosuje tooboth hello oryginalnego akcji i błędu alternatywny hello. Typ akcji jego również możliwe toohave hello alternatywny Błąd akcji się różnić od typu akcji hello działania głównego. Na przykład podczas działania głównego hello może wywołaniem punktu końcowego HTTP, akcja błędu hello zamiast tego można kolejki magazynu, kolejką usługi service bus lub Akcja temat magistrali usługi, który wykonuje rejestrowanie błędów.

jak tooconfigure alternatywny punkt końcowy, można znaleźć zbyt toolearn[errorAction](scheduler-concepts-terms.md#action-and-erroraction).

## <a name="see-also"></a>Zobacz też
 [Co to jest Scheduler?](scheduler-intro.md)

 [Pojęcia i terminologia dotyczące usługi Azure Scheduler oraz hierarchia jednostek](scheduler-concepts-terms.md)

 [Rozpoczynanie pracy przy użyciu harmonogramu w hello portalu Azure](scheduler-get-started-portal.md)

 [Plany i rozliczenia w usłudze Azure Scheduler](scheduler-plans-billing.md)

 [Jak planuje toobuild złożone i zaawansowane cyklu z Harmonogram systemu Azure](scheduler-advanced-complexity.md)

 [Dokumentacja interfejsu API REST usługi Azure Scheduler](https://msdn.microsoft.com/library/mt629143)

 [Dokumentacja poleceń cmdlet programu PowerShell dla usługi Azure Scheduler](scheduler-powershell-reference.md)

 [Limity, wartości domyślne i kody błędów usługi Azure Scheduler](scheduler-limits-defaults-errors.md)

 [Uwierzytelnianie połączeń wychodzących usługi Azure Scheduler](scheduler-outbound-authentication.md)

[1]: ./media/scheduler-high-availability-reliability/scheduler-high-availability-reliability-image1.png

[2]: ./media/scheduler-high-availability-reliability/scheduler-high-availability-reliability-image2.png
