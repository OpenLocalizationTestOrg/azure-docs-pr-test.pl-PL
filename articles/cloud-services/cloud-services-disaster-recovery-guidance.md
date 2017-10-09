---
title: "toodo aaaWhat w przypadku hello Azure zakłócenia, który ma wpływ na usługi w chmurze Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jakie toodo w przypadku hello Azure zakłócenia, który ma wpływ na usługi w chmurze Azure."
services: cloud-services
documentationcenter: 
author: mmccrory
manager: timlt
editor: 
ms.assetid: e52634ab-003d-4f1e-85fa-794f6cd12ce4
ms.service: cloud-services
ms.workload: cloud-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: mmccrory
ms.openlocfilehash: bb1f1835fc91a23772f81801b67d5786c190ba19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-toodo-in-hello-event-of-an-azure-service-disruption-that-impacts-azure-cloud-services"></a>Jakie toodo w przypadku hello Azure zakłócenia, który ma wpływ na usługi w chmurze Azure
Firma Microsoft pracujemy twardych toomake się, że naszych usług są zawsze dostępne tooyou najodpowiedniejszym czasie. Wymusza naszych niezależnych czasami wpływ nam w sposób, aby spowodować zakłócenia w świadczeniu usług nieplanowane.

Firma Microsoft udostępnia Umowa dotycząca poziomu usług (SLA) dla swoich usług jako zobowiązanie czas pracy i łączności. Witaj umowy SLA dla poszczególnych usług Azure można znaleźć w folderze [umowy dotyczące poziomu usług Azure](https://azure.microsoft.com/support/legal/sla/).

Platforma Azure ma już wiele wbudowanych funkcji obsługujących aplikacje o wysokiej dostępności. Aby uzyskać więcej informacji o tych usług, przeczytaj [odzyskiwania po awarii i wysoką dostępność aplikacji Azure](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md).

W tym artykule omówiono scenariusza odzyskiwania awaryjnego wartość true, gdy całego regionu ulegnie awarii toomajor klęski żywiołowej lub powszechnie przerw w obsłudze. Są to rzadkie wystąpienia, ale należy przygotować możliwości hello jest awarii całego regionu. Całego regionu napotyka przerw w działaniu usługi, hello magazyn lokalnie nadmiarowy kopie danych tymczasowo będą niedostępne. Jeśli włączono replikację geograficzną, trzy dodatkowe kopie obiektów blob magazynu Azure i tabele są przechowywane w innym regionie. W przypadku hello pełną regionalnej awarii lub awarii, w których hello regionu podstawowego nie jest możliwe do odzyskania Azure ponownie mapuje wszystkie hello DNS wpisy toohello replikacją geograficzną regionu.

> [!NOTE]
> Należy pamiętać, że nie masz żadnych kontrolę nad ten proces i nastąpią dla zakłócenia w świadczeniu usług centrum danych na poziomie. W związku z tym należy również polegać na innych strategii tworzenia kopii zapasowych specyficzne dla aplikacji tooachieve hello najwyższy poziom dostępności. Aby uzyskać więcej informacji, zobacz [odzyskiwania po awarii i wysokiej dostępności dla aplikacji tworzonych w systemie Microsoft Azure](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md). Jeśli chcesz, aby mogli tooaffect toobe własne przejścia w tryb failover może być użycie hello tooconsider [dostęp do odczytu magazynu geograficznie nadmiarowego (RA-GRS)](../storage/common/storage-redundancy.md#read-access-geo-redundant-storage), który tworzy kopię danych tylko do odczytu w innym regionie.
>
>


## <a name="option-1-use-a-backup-deployment-through-azure-traffic-manager"></a>Opcja 1: Użycie kopii zapasowej wdrożenia za pośrednictwem usługi Azure Traffic Manager
Witaj najbardziej niezawodne rozwiązanie odzyskiwania po awarii wymaga obsługi wielu wdrożeń aplikacji w różnych regionach, a następnie za pomocą [usługi Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md) toodirect ruch między nimi. Usługi Azure Traffic Manager zawiera wiele [metody routingu](../traffic-manager/traffic-manager-routing-methods.md), więc możesz wybrać, czy toomanage wdrożeń za pomocą modelu podstawowej lub tworzenia kopii zapasowej lub toosplit ruch między nimi.

![Równoważenie usług Azure Cloud Services w regionach z usługi Azure Traffic Manager](./media/cloud-services-disaster-recovery-guidance/using-azure-traffic-manager.png)

Hello najszybszym odpowiedzi toohello utraty regionu, ważne jest, aby skonfigurować Menedżera ruchu [monitorowania punktów końcowych](../traffic-manager/traffic-manager-monitoring.md).

## <a name="option-2-deploy-your-application-tooa-new-region"></a>Opcja 2: Wdróż nowy obszar tooa aplikacji
Obsługa wielu aktywnych wdrożeń, zgodnie z opisem w poprzedniej opcji hello wiąże się dodatkowe bieżących kosztów. Jeśli masz hello oryginalnego kodu lub skompilowanych pakietu usługi w chmurze celu czasu odzyskiwania (RTO) jest wystarczająco elastyczny, można Utwórz nowe wystąpienie aplikacji w innym regionie i aktualizacji wdrożenia DNS rekordów toopoint toohello nowe.

Aby uzyskać więcej szczegółów na temat toocreate i wdrażania aplikacji usługi w chmurze, zobacz [jak toocreate i wdrażania usługi w chmurze](cloud-services-how-to-create-deploy-portal.md).

W zależności od źródła danych aplikacji może być konieczne procedury odzyskiwania hello toocheck dla źródła danych aplikacji.

* Dla źródeł danych usługi Azure Storage, zobacz [replikacja usługi Azure Storage](../storage/common/storage-redundancy.md#read-access-geo-redundant-storage) toocheck na powitania dostępne opcje oparte na powitania wybrany model replikacji dla aplikacji.
* Dla źródeł bazy danych SQL, przeczytaj [omówienie: firm odzyskiwania po awarii ciągłości i bazy danych z bazy danych SQL w chmurze](../sql-database/sql-database-business-continuity.md) toocheck na dostępne opcje hello oparte na modelu replikacji hello wybrany dla aplikacji.


## <a name="option-3-wait-for-recovery"></a>Opcja 3: Poczekaj, aż odzyskiwanie
W takim przypadku nie jest wymagana żadna akcja ze strony użytkownika, ale usługi będą niedostępne do momentu przywrócenia hello regionu. Możesz wyświetlać bieżący stan usługi hello na powitania [pulpit nawigacyjny kondycji usługi Azure](https://azure.microsoft.com/status/).

## <a name="next-steps"></a>Następne kroki
więcej informacji na temat sposobu tooimplement odzyskiwania po awarii i strategii wysokiej dostępności, zobacz toolearn [odzyskiwania po awarii i wysoką dostępność aplikacji Azure](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md).

Zobacz toodevelop techniczne szczegółowy opis możliwości platformy chmury [wskazówki techniczne Azure odporności](../resiliency/resiliency-technical-guidance.md).
