---
title: scenariusze odzyskiwania aaaDisaster dla maszyn wirtualnych platformy Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jakie toodo w zdarzeniu hello czy przerw w działaniu usługi Azure ma wpływ na maszynach wirtualnych platformy Azure."
services: virtual-machines
documentationcenter: 
author: kmouss
manager: timlt
editor: 
ms.assetid: 65272148-ff06-4bce-91f1-851d706d4d40
ms.service: virtual-machines
ms.workload: virtual-machines
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: kmouss;aglick
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 839c6f9c51a7f35b48ef3636bc346eef332bb06d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-toodo-in-hello-event-that-an-azure-service-disruption-impacts-azure-vms"></a>Jakie toodo w zdarzeniu hello czy przerw w działaniu usługi Azure ma wpływ na maszynach wirtualnych platformy Azure
Firma Microsoft pracujemy twardych toomake się, że naszych usług są zawsze dostępne tooyou najodpowiedniejszym czasie. Wymusza naszych niezależnych czasami wpływ nam w sposób, aby spowodować zakłócenia w świadczeniu usług nieplanowane.

Firma Microsoft udostępnia Umowa dotycząca poziomu usług (SLA) dla swoich usług jako zobowiązanie czas pracy i łączności. Witaj umowy SLA dla poszczególnych usług Azure można znaleźć w folderze [umowy dotyczące poziomu usług Azure](https://azure.microsoft.com/support/legal/sla/).

Platforma Azure ma już wiele wbudowanych funkcji obsługujących aplikacje o wysokiej dostępności. Aby uzyskać więcej informacji o tych usług, przeczytaj [odzyskiwania po awarii i wysoką dostępność aplikacji Azure](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md).

W tym artykule omówiono scenariusza odzyskiwania awaryjnego wartość true, gdy całego regionu ulegnie awarii toomajor klęski żywiołowej lub powszechnie przerw w obsłudze. Są to rzadkie wystąpienia, ale należy przygotować możliwości hello jest awarii całego regionu. Całego regionu napotyka przerw w działaniu usługi, hello magazyn lokalnie nadmiarowy kopie danych tymczasowo będą niedostępne. Jeśli włączono replikację geograficzną, trzy dodatkowe kopie obiektów blob magazynu Azure i tabele są przechowywane w innym regionie. W przypadku hello pełną regionalnej awarii lub awarii, w których hello regionu podstawowego nie jest możliwe do odzyskania Azure ponownie mapuje wszystkie hello DNS wpisy toohello replikacją geograficzną regionu.

toohelp obsługi tych zdarzeń w rzadkich, udostępniamy hello następujące wskazówki dotyczące maszyn wirtualnych platformy Azure w przypadku hello przerw w działaniu usługi hello regionu całego wdrożonym aplikacji maszyny wirtualnej platformy Azure.

## <a name="option-1-initiate-a-failover-by-using-azure-site-recovery"></a>Opcja 1: Zainicjuj tryb failover przy użyciu usługi Azure Site Recovery
Można skonfigurować usługi Azure Site Recovery dla maszyn wirtualnych, dzięki czemu będzie można odzyskać aplikacji za pomocą jednego kliknięcia w kilku minut. Można replikować regionu tooAzure wybranym i regiony toopaired bez ograniczeń. Możesz rozpocząć pracę przez [replikowanie maszyn wirtualnych](https://aka.ms/a2a-getting-started). Możesz [Tworzenie planu odzyskiwania](../site-recovery/site-recovery-create-recovery-plans.md) , dzięki czemu można zautomatyzować proces całej pracy awaryjnej hello aplikacji. Możesz [testy z trybu failover](../site-recovery/site-recovery-test-failover-to-azure.md) uprzednio bez wpływu na aplikacji lub hello trwającej replikacji w środowisku produkcyjnym. W przypadku hello zakłóceń regionu podstawowego, wystarczy [Zainicjuj tryb failover](../site-recovery/site-recovery-failover.md) i aplikacji w docelowym regionie.


## <a name="option-2-wait-for-recovery"></a>Opcja 2: Poczekaj, aż odzyskiwanie
W takim przypadku jest wymagana żadna akcja ze strony użytkownika. Wiedzieć, że firma Microsoft pracuje dokładnie toorestore dostępności usługi. Możesz wyświetlać bieżący stan usługi hello na naszych [pulpit nawigacyjny kondycji usługi Azure](https://azure.microsoft.com/status/).

Jest to hello najlepszym rozwiązaniem, jeśli nie skonfigurowano usługi Azure Site Recovery, dostęp do odczytu z magazynu geograficznie nadmiarowego magazynu lub przerw w działaniu wcześniejsze toohello magazynu geograficznie nadmiarowego. Jeśli zdefiniowano magazynu geograficznie nadmiarowego lub magazynu geograficznie nadmiarowego dostęp do odczytu dla konta magazynu hello przechowywania maszyny Wirtualnej wirtualnego dysku twardego (VHD), może wyglądać toorecover hello podstawowy obraz wirtualnego dysku twardego i spróbuj tooprovision nowej maszyny Wirtualnej z niego. To nie jest preferowaną opcję, ponieważ nie ma żadnych gwarancji synchronizacji danych. W związku z tym ta opcja nie jest gwarantowana toowork.


> [!NOTE]
> Należy pamiętać, że nie masz żadnych kontrolę nad ten proces i będą występować tylko dla zakłócenia w świadczeniu usług całej regionu. W związku z tym należy również polegać na innych strategii tworzenia kopii zapasowych specyficzne dla aplikacji tooachieve hello najwyższy poziom dostępności. Aby uzyskać więcej informacji, zobacz sekcję hello na [danych strategii odzyskiwania po awarii](https://docs.microsoft.com/azure/architecture/resiliency/disaster-recovery-azure-applications#data-strategies-for-disaster-recovery).
>
>

## <a name="next-steps"></a>Następne kroki

- Uruchom [ochrona aplikacji uruchomionych na maszynach wirtualnych Azure](https://aka.ms/a2a-getting-started) przy użyciu usługi Azure Site Recovery

- więcej informacji na temat sposobu tooimplement odzyskiwania po awarii i strategii wysokiej dostępności, zobacz toolearn [odzyskiwania po awarii i wysoką dostępność aplikacji Azure](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md).

- Zobacz toodevelop techniczne szczegółowy opis możliwości platformy chmury [wskazówki techniczne Azure odporności](../resiliency/resiliency-technical-guidance.md).


- Jeśli instrukcje hello nie jest jasne lub jeśli chcesz Microsoft toodo hello działań w Twoim imieniu, skontaktuj się z [techniczną](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).
