---
title: "Przegląd kondycji usługi aaaAzure | Dokumentacja firmy Microsoft"
description: "Spersonalizowane informacje o aplikacji Azure wpływu problemów aktualnych i przyszłych usługi Azure i konserwacji."
services: Resource health
documentationcenter: 
author: rboucher
manager: 
editor: 
ms.assetid: 
ms.service: service-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 07/07/2017
ms.author: robb
ms.openlocfilehash: 2b536ee2f19757d4f2baf5529866c3d159a4670c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-health"></a>Azure Service Health
Kondycja usługi Azure zawiera informacje o odpowiednim i spersonalizowane, gdy problemy w usługach Azure mieć wpływ na usługi.  Można go również przygotować do najbliższej planowanej konserwacji.

## <a name="service-health-events"></a>Zdarzenia kondycji usługi
Kondycja usługi śledzi trzy typy zdarzeń kondycji, które mogą mieć wpływ na zasoby:
1. **Usługa problemów** -problemów w hello usług Azure wpływających od razu. 
2. **Zaplanowanej konserwacji** -najbliższej konserwacji, które mogą mieć wpływ na dostępność hello usług w przyszłości hello.  
3. **Klasyfikatory kondycji** -zmiany w usługach Azure, które wymagają Twojej uwagi. Przykłady obejmują funkcje platformy Azure są przestarzałe lub przekracza przydział użycia.

    ![Zdarzenia kondycji usługi](./media/service-health-overview/azure-service-health-overview-7.png)

## <a name="get-started-with-service-health"></a>Wprowadzenie do usługi kondycji
toolaunch pulpit nawigacyjny kondycji usługi, wybierz hello kondycja usługi kafelka na pulpicie nawigacyjnym portalu. Jeśli wcześniej zostały usunięte kafelka hello lub jest używany niestandardowy pulpit nawigacyjny, wyszukaj usługi usługi kondycji w "Więcej usługi" (dołu w lewo na pulpicie nawigacyjnym).
![Wprowadzenie do usługi kondycji](./media/service-health-overview/azure-service-health-overview-1.png)

## <a name="see-current-issues-which-impact-your-services"></a>Zobacz bieżących problemach mogących mieć wpływ na usługi
Witaj **usługi problemów** widok zawiera wszystkie bieżące problemy w usług Azure, które wpływają na Twoich zasobów. Można zrozumieć, kiedy rozpoczął się problem hello i jakie usługi i regiony ma wpływ. Można również znaleźć hello najnowszych aktualizacji toounderstand co Azure wykonuje tooresolve hello problem. 
![Problem dotyczący usługi zarządzania](./media/service-health-overview/azure-service-health-overview-2.png)

Wybierz hello **potencjalny wpływ** kartę toosee hello określonej listy zasobów własnej, które mogą mieć wpływ hello problem. Lista CSV tooshare tych zasobów można pobrać z zespołem.
![Zarządzanie problem dotyczący usługi — wpływ](./media/service-health-overview/azure-service-health-overview-4.png)

## <a name="get-links-and-downloadable-explanations"></a>Korzystać z linków i wyjaśnienia do pobrania 
Możesz też uzyskać łącze hello toouse problemu w systemie zarządzania problem. Plików PDF i czasami tooshare pliki CSV można pobrać osobom, które nie mają toohello dostęp do portalu Azure.   
![Zarządzanie problem dotyczący usługi — Zarządzanie problemami](./media/service-health-overview/azure-service-health-overview-3.png)

## <a name="get-support-from-microsoft"></a>Uzyskiwanie pomocy technicznej firmy Microsoft
Jeśli zasób jest w złym stanie nawet po hello problem zostanie rozwiązany, skontaktuj się z pomocy technicznej.  Użyj łącza pomocy technicznej hello na powitania po prawej strony hello.  

## <a name="pin-a-personalized-health-map-tooyour-dashboard"></a>Pulpit nawigacyjny kondycji spersonalizowane mapy tooyour numeru PIN
Filtrowanie tooshow usługi kondycji Twojej subskrypcji biznesowych o znaczeniu krytycznym, regiony i typów zasobów. Zapisz hello filtru i numer pin spersonalizowane world mapy tooyour portalu pulpit nawigacyjny kondycji. 
![Mapa spersonalizowane kondycji filtru](./media/service-health-overview/azure-service-health-overview-6a.png)
![Przypnij mapę spersonalizowane kondycji](./media/service-health-overview/azure-service-health-overview-6b.png)

## <a name="configure-service-health-alerts"></a>Skonfiguruj alerty dotyczące kondycji usługi
Kondycja usługi Azure integruje się z tooalert Azure Monitor można za pośrednictwem wiadomości e-mail, wiadomości SMS i powiadomień elementu webhook po wpływ na zasoby biznesowych o znaczeniu krytycznym. Konfigurowanie alertu dziennika aktywności hello odpowiednie zdarzenia kondycji usługi. Trasa alertów toohello odpowiednich osób w organizacji za pomocą grup akcji. Aby uzyskać więcej informacji, zobacz [skonfigurować alerty dotyczące kondycji usługi](../monitoring-and-diagnostics/monitoring-activity-log-alerts-on-service-notifications.md)

# <a name="next-steps"></a>Następne kroki
Konfigurowanie alertów, więc użytkownik jest powiadamiany o kondycji problemy. Aby uzyskać więcej informacji, zobacz [skonfigurować alerty dotyczące kondycji usługi](../monitoring-and-diagnostics/monitoring-activity-log-alerts-on-service-notifications.md). 