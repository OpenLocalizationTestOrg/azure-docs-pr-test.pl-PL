---
title: "Przegląd kondycji zasobów aaaAzure | Dokumentacja firmy Microsoft"
description: "Przegląd kondycji zasobów platformy Azure"
services: Resource health
documentationcenter: 
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: service-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 07/01/2017
ms.author: BernardoAMunoz
ms.openlocfilehash: f06153864090487829f717dc3e8972c78a4a58af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-health-overview"></a>Przegląd kondycji zasobów platformy Azure
 
Usługa Resource Health ułatwia diagnozowanie i uzyskanie pomocy technicznej, gdy problem z platformą Azure ma wpływ na zasoby. Informuje o hello kondycji do bieżących i starszych zasobów, a pomaga ograniczać problemy. Usługa Resource Health oferuje pomoc techniczną w przypadku problemów z usługą platformy Azure.

Podczas gdy [stan Azure](https://status.azure.com) informuje o problemów dotyczących usługi, które mają wpływ na szerokiego zakresu klientów platformy Azure, kondycja zasobu zawiera spersonalizowane pulpit nawigacyjny kondycji hello zasobów. Kondycja zasobów zawiera zawsze hello zasoby były niedostępne w hello minął termin płatności tooAzure problemów dotyczących usługi. Dzięki temu proste dla toounderstand możesz Jeśli umowa SLA zostało naruszone. 

## <a name="what-is-considered-a-resource-and-how-does-resource-health-decides-if-a-resource-is-healthy-or-not"></a>Co to jest uznawany za zasobu i jak kondycja zasobów decyduje o tym, jeśli zasób jest uszkodzony lub nie?
Zasób jest wystąpieniem typu zasobu oferowane przez usługę Azure za pomocą usługi Azure Resource Manager, na przykład: maszynę wirtualną, aplikacji sieci web lub bazy danych SQL.

Kondycja zasobów polega na sygnały emitowane przez hello tooassess różnych usług platformy Azure, jeśli zasób jest uszkodzony lub nie. Jeśli zasób jest zła, kondycja zasobu analizuje dodatkowe informacje toodetermine hello źródłem problemu hello. Identyfikuje również akcje, które Microsoft trwa toofix hello problem lub akcji może zająć tooaddress hello spowodować hello problemu. 

Przejrzyj hello pełną listę typów zasobów i kondycji sprawdza [kondycji zasobów platformy Azure](resource-health-checks-resource-types.md) dodatkowe szczegóły dotyczące sposób jest oceny kondycji.

## <a name="health-status-provided-by-resource-health"></a>Dostarczone przez kondycji zasobów stan kondycji
Witaj kondycji zasobu jest jednym z hello następujące stany:

### <a name="available"></a>Dostępna
Usługa Hello nie wykrył wszelkie zdarzenia wpływające na kondycję hello hello zasobów. W przypadkach, gdzie zasobów hello odzyskał sprawność po nieplanowane przestoje podczas hello ostatnie 24 godziny, zobaczysz hello **ostatnio odzyskana** powiadomień.

![Maszyna wirtualna zasobów kondycji dostępności](./media/resource-health-overview/Available.png)

### <a name="unavailable"></a>Niedostępne
usługi Hello wykrył trwającą platformy lub zdarzenia-platforma wpływające na kondycję hello hello zasobów.

#### <a name="platform-events"></a>Zdarzenia platformy
Te zdarzenia są wyzwalane przez kilka składników hello infrastruktury platformy Azure i obejmują zarówno zaplanowanych akcji, takich jak planowanej konserwacji i nieoczekiwane zdarzenia, takie jak ponowne uruchomienie komputera hosta nieplanowane.

Kondycja zasobów zawiera dodatkowe szczegóły dotyczące zdarzeń hello, proces odzyskiwania hello i umożliwia obsługę toocontact nawet, jeśli nie masz aktywnych pomocy technicznej umowy firmy Microsoft.

![Zasób kondycji niedostępny maszyny wirtualnej powodu tooplatform zdarzeń](./media/resource-health-overview/Unavailable.png)

#### <a name="non-platform-events"></a>Zdarzenia non-platformy
Te zdarzenia są wyzwalane przez akcje wykonywane przez użytkowników, na przykład zatrzymanie maszyny wirtualnej lub osiągnięcia hello maksymalną liczbę połączeń tooa pamięci podręcznej Redis.

![Zasób kondycji niedostępny maszyny wirtualnej powodu zdarzenia toonon platformy](./media/resource-health-overview/Unavailable_NonPlatform.png)

### <a name="unknown"></a>Nieznany
Ten stan kondycji wskazuje, że kondycja zasobu nie otrzymano informacji na temat tego zasobu na więcej niż 10 minut. Gdy ten stan nie jest oznaczenie ostateczne hello stanu zasobu hello, jest ważne dane w hello proces rozwiązywania problemów:
* Jeśli zasobów hello jest uruchomiona jako oczekiwanego hello stan zasobu hello zaktualizuje tooAvailable po kilku minutach.
* Jeśli występują problemy z zasobem hello, hello stan kondycji nieznany może sugerują, że zasób hello jest wpływ zdarzenie platformy hello.

![Nieznany maszyny wirtualnej kondycji zasobów](./media/resource-health-overview/Unknown.png)

## <a name="report-an-incorrect-status"></a>Niepoprawny stan raportu
Jeśli w dowolnym momencie uważasz hello bieżący stan kondycji jest niepoprawny, możesz można Daj nam znać, klikając **zgłoszenia stanu kondycji niepoprawne**. W przypadkach, w których ma wpływ Azure problem, firma Microsoft zachęca obsługę toocontact za pomocą bloku kondycji zasobów hello. 

![Kondycja zasobu raportu niepoprawny stan.](./media/resource-health-overview/incorrect-status.png)

## <a name="historical-information"></a>Informacje historyczne
Można uzyskać się dane historyczne kondycji too14 dni, klikając **wyświetlanie historii** w bloku kondycji zasobów hello. 

![Kondycja zasobów historii raportu](./media/resource-health-overview/history-blade.png)

## <a name="getting-started"></a>Wprowadzenie
tooopen kondycja zasobów dla jednego zasobu
1.  Zaloguj się do hello portalu Azure.
2.  Przejdź tooyour zasobów.
3.  W menu zasobów hello znajduje się w lewej hello, kliknij przycisk **kondycja zasobów**.

![Otwórz kondycja zasobów z bloku zasobów](./media/resource-health-overview/from-resource-blade.png)

Kondycja zasobów można również uzyskać, klikając **więcej usług**i wpisując **kondycja zasobów** w hello tooopen pole tekstowe filtru **Pomoc i obsługa techniczna** bloku. Na koniec kliknij [ **kondycja zasobów**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth).

![Otwórz z usługi więcej kondycja zasobów](./media/resource-health-overview/FromOtherServices.png)

## <a name="next-steps"></a>Następne kroki

Wyewidencjonuj toolearn tych zasobów, więcej informacji na temat kondycji zasobów:
-  [Typy zasobów i kondycji sprawdza w kondycji zasobów platformy Azure](resource-health-checks-resource-types.md)
-  [Często zadawane pytania dotyczące kondycji zasobów platformy Azure](resource-health-faq.md)




