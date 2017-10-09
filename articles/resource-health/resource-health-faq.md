---
title: "aaaAzure kondycja zasobów — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Przegląd kondycji zasobów platformy Azure"
services: Resource health
documentationcenter: dev-center-name
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: resource-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 06/01/2016
ms.author: BernardoAMunoz
ms.openlocfilehash: 5c5cfa116340094ffb1d6d5b206a11d389a0305a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-health-faq"></a>Kondycja zasobów platformy Azure — często zadawane pytania
Dowiedz się, że hello toocommon pytania dotyczące kondycji zasobów platformy Azure.

## <a name="frequently-asked-questions"></a>Często zadawane pytania
* [Co to jest usługa Azure Resource Health?](#what-is-azure-resource-health)
* [Kondycja zasobów hello przeznaczenie?](#what-is-the-resource-health-intended-for)
* [Sprawdza, jakie kondycji są wykonywane przez kondycja zasobów?](#what-health-checks-are-performed-by-resource-health)
* [Co każdy stan kondycji hello oznacza?](#what-does-each-of-the-health-status-mean)
* [Co to hello oznacza nieznany stan? Coś jest problem z mojej zasobów?](#what-does-the-unknown-status-mean-is-something-wrong-with-my-resource)
* [Jak uzyskać pomoc dla zasobu, która jest niedostępna](#how-can-i-get-help-for-a-resource-that-is-unavailable)
* [Kondycja zasobów odróżnienie niedostępności z uwzględnieniem wielkości liter problemami platformy i coś jak?](#does-resource-health-differentiate-between-unavailability-cased-by-platform-problems-versus-something-i-did)
* [Czy można zintegrować z narzędzi do monitorowania kondycji zasobów?](#can-i-integrate-resource-health-with-my-monitoring-tools)
* [Gdzie znaleźć kondycja zasobów?](#where-do-i-find-resource-health)
* [Kondycja zasobu jest dostępna dla wszystkich typów zasobów?](#is-resource-health-available-for-all-resource-types)
* [Co należy zrobić, jeśli mojego zasobów jest wyświetlany dostępny, ale I uważają, że nie jest?](#what-should-i-do-if-my-resource-is-showing-available-but-i-believe-it-is-not)
* [Kondycja zasobu jest dostępna dla wszystkich regionów platformy Azure?](#is-resource-health-available-for-all-azure-regions)
* [Jak kondycja zasobu jest inna niż hello pulpit nawigacyjny kondycji usługi lub hello portalu usługi Azure powiadomień?](#how-is-resource-health-different-from-the-service-health-dashboard-or-the-azure-portal-service-notifications)
* [Należy tooactivate kondycja zasobów dla każdego zasobu?](#do-i-need-to-activate-resource-health-for-each-resource)
* [Potrzebujemy tooenable kondycja zasobów dla mojej organizacji?](#do-we-need-to-enable-resource-health-for-my-organization)
* [Jest kondycja zasobu jest dostępny bezpłatnie?](#is-resource-health-available-free-of-charge)
* [Jakie są zalecenia hello, które udostępnia kondycja zasobów?](#what-are-the-recommendations-that-resource-health-provides)


## <a name="what-is-azure-resource-health"></a>Co to jest kondycji zasobów platformy Azure?
Usługa Resource Health ułatwia diagnozowanie i uzyskanie pomocy technicznej, gdy problem z platformą Azure ma wpływ na zasoby. Informuje o hello kondycji do bieżących i starszych zasobów, a pomaga ograniczać problemy. Usługa Resource Health oferuje pomoc techniczną w przypadku problemów z usługą platformy Azure.  

## <a name="what-is-hello-resource-health-intended-for"></a>Kondycja zasobów hello przeznaczenie?
Po wykryto problem z zasobem, kondycja zasobu może pomóc w diagnozowaniu hello główną przyczynę. Zapewnia pomoc toomitigate hello problem i pomocy technicznej, gdy potrzebujesz więcej pomocy dotyczącej problemów dotyczących usługi Azure.

## <a name="what-health-checks-are-performed-by-resource-health"></a>Sprawdza, jakie kondycji są wykonywane przez kondycja zasobów?
Kondycja zasobów sprawdza różnych oparte na powitania [typu zasobu](resource-health-checks-resource-types.md). Kontrole są zaprojektowane tooimplement trzy rodzaje problemów: 
1. Nieplanowane zdarzenia, na przykład host nieoczekiwane ponowne uruchomienie komputera
2. Planowane zdarzeń, takich jak aktualizacje zaplanowane systemu operacyjnego hosta
3. Zdarzenia wyzwolone przez akcje użytkownika, na przykład użytkownik ponowny rozruch maszyny wirtualnej

## <a name="what-does-each-of-hello-health-status-mean"></a>Co każdy stan kondycji hello oznacza?
Istnieją trzy stany kondycji różne:
1. Niedostępne: Nie ma żadnych znanych problemów w hello platformy Azure, które mogą mieć wpływ na tego zasobu
2. Niedostępne: Kondycja zasobów wykrył problemy, które wpływają na powitania zasobów
3. Nieznany: Kondycja zasobu nie można określić hello kondycji zasobu, ponieważ została zatrzymana, odbieranie informacji ich dotyczących. 

## <a name="what-does-hello-unknown-status-mean-is-something-wrong-with-my-resource"></a>Co to hello oznacza nieznany stan? Coś jest problem z mojej zasobów?
stan kondycji Hello ustawiono toounknown po zatrzymaniu kondycja zasobów odbieranie informacji na temat określonego zasobu. Gdy ten stan nie jest ostatecznym wskazanie hello stan zasobu hello, w przypadkach, w których występują problemy, może to oznaczać, że występuje problem z platformy Azure.

## <a name="how-can-i-get-help-for-a-resource-that-is-unavailable"></a>Jak uzyskać pomoc dla zasobu, która jest niedostępna
Można przesłać żądanie obsługi z bloku kondycji zasobów hello. Nie ma potrzeby obsługi zgodą tooopen Microsoft żądanie po hello zasób jest niedostępny ponieważ zdarzenia platformy.

## <a name="does-resource-health-differentiate-between-unavailability-cased-by-platform-problems-versus-something-i-did"></a>Kondycja zasobów odróżnienie niedostępności z uwzględnieniem wielkości liter problemami platformy i coś jak?
Tak, gdy zasób jest niedostępny, kondycja zasobu identyfikuje hello główną przyczynę w jednej z tych kategorii: 
1.  Akcji zainicjowanej przez użytkownika
2.  Zdarzenie planowane 
3.  Nieplanowane zdarzenia

W portalu hello akcji zainicjowanej przez użytkownika są wyświetlane przy użyciu ikony powiadomień niebieski, podczas planowanych lub nieplanowanych zdarzenia są wyświetlane przy użyciu czerwona ikona ostrzeżenia. Bardziej szczegółowe informacje znajdują się w hello [Przegląd kondycji zasobów](Resource-health-overview.md).  

## <a name="can-i-integrate-resource-health-with-my-monitoring-tools"></a>Czy można zintegrować z narzędzi do monitorowania kondycji zasobów?
Kondycja zasobu jest toohelp zaprojektowanej zdiagnozować i rozwiązać problemy dotyczące usługi Azure, które mają wpływ na zasoby. Za pomocą tooprogrammatically interfejsu API kondycji zasobów hello uzyskać hello stan kondycji, firma Microsoft zaleca się, że używasz toomonitor metryki zasobów. Gdy zostanie wykryty problem, kondycja zasobu pomaga ustalić przyczynę hello i przeprowadza Cię przez akcje tooaddress je. Odwiedź stronę [Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/) toolearn więcej informacji na temat używania metryki toocheck zasobów.

## <a name="where-do-i-find-resource-health"></a>Gdzie znaleźć kondycja zasobów?
Po zalogowaniu się toohello portalu Azure, istnieje wiele sposobów, kondycja zasobu można uzyskać dostęp:
1. Przejdź tooyour zasobów. W nawigacji po lewej stronie powitania, kliknij przycisk **kondycja zasobów**.
2. Przejdź toohello Azure Monitor bloku.  W nawigacji po lewej stronie powitania, kliknij przycisk **kondycja zasobów**.
3. Otwórz hello **Pomoc i obsługa techniczna** bloku, klikając znak zapytania hello w hello prawym górnym rogu portalu hello, a następnie wybierając **Pomoc i obsługa techniczna**. Gdy zostanie otwarty blok hello, kliknij przycisk **kondycja zasobów**

Umożliwia także kondycja zasobów hello interfejsu API tooobtain informacje o kondycji hello zasobów.

## <a name="is-resource-health-available-for-all-resource-types"></a>Kondycja zasobu jest dostępna dla wszystkich typów zasobów?
Witaj listy kontroli kondycji i typów zasobów, które są obsługiwane w ramach kondycji zasobów można znaleźć [tutaj](resource-health-checks-resource-types.md)

## <a name="what-should-i-do-if-my-resource-is-showing-available-but-i-believe-it-is-not"></a>Co należy zrobić, jeśli mojego zasobów jest wyświetlany dostępny, ale I uważają, że nie jest?"
Sprawdzanie kondycji hello zasobu, bezpośrednio w stan kondycji hello można kliknąć **zgłoszenia stanu kondycji niepoprawne**. Przed przesłaniem hello raportu, można skorzystać z opcji hello udostępnia dodatkowe szczegóły na dlaczego uważasz, że bieżący stan kondycji hello jest niepoprawny.

## <a name="is-resource-health-available-for-all-azure-regions"></a>Kondycja zasobu jest dostępna dla wszystkich regionów platformy Azure? 
Kondycja zasobu jest dostępna w we wszystkich obszarach geograficznych Azure, z wyjątkiem następujących regionach hello:
* Administracja USA — Wirginia
* Administracja USA — Iowa
* US DoD — wschodnie stany
* US DoD — środkowe stany
* Niemcy Środkowe
* Niemcy Północno-Wschodnie
* Chiny Wschodnie
* Chiny Północne

## <a name="how-is-resource-health-different-from-hello-service-health-dashboard-or-hello-azure-portal-service-notifications"></a>Jak kondycja zasobu jest inna niż hello pulpit nawigacyjny kondycji usługi lub hello portalu usługi Azure powiadomień?
Witaj informacje o kondycji zasobu jest bardziej szczegółowy niż dostarczanych przez hello pulpit nawigacyjny kondycji usługi platformy Azure.

Podczas gdy [stan Azure](https://status.azure.com) i powiadomień usługi portalu hello informuje o problemach usługi, które mają wpływ na szerokiego zakresu klientów (na przykład region platformy Azure), kondycja zasobów przedstawia bardziej szczegółowego zdarzenia, które mają zastosowanie tylko toohello określonego zasobu. Na przykład jeśli host nieoczekiwanie uruchamiany ponownie, kondycja zasobu alerty tylko tych klientów, w której maszyny wirtualne zostały uruchomione na tym hoście.

Jest ważne toonotice tego tooprovide ukończyć widoczność zdarzeń wpływu na zasoby, kondycja zasobów udostępnia również zdarzenia opublikowane w powiadomieniach usługi i hello pulpit nawigacyjny kondycji usługi.

## <a name="do-i-need-tooactivate-resource-health-for-each-resource"></a>Należy tooactivate kondycja zasobów dla każdego zasobu?
Nie, informacje o kondycji są dostępne dla wszystkich typów zasobów dostępne za pośrednictwem kondycja zasobów. 

## <a name="do-we-need-tooenable-resource-health-for-my-organization"></a>Potrzebujemy tooenable kondycja zasobów dla mojej organizacji?
Nie.  Kondycja zasobów platformy Azure jest dostępny w ramach hello portalu Azure, bez żadnych wymagań dotyczących instalacji.

## <a name="is-resource-health-available-free-of-charge"></a>Jest kondycja zasobu jest dostępny bezpłatnie?
Tak.  Kondycja zasobów platformy Azure jest bezpłatne.

## <a name="what-are-hello-recommendations-that-resource-health-provides"></a>Jakie są zalecenia hello, które udostępnia kondycja zasobów?
Oparte na stanie kondycji hello, kondycja zasobów zapewnia zalecenia hello celu skrócenia czasu hello spędzony rozwiązywania problemów. Na dostępne zasoby zalecenia hello skupić się na jak wystąpić toosolve hello najbardziej typowe problemy z klientów. Jeśli hello zasób jest niedostępny z powodu tooan Azure nieplanowanego zdarzenia hello skupić się na wspieranie możesz podczas i po zakończeniu procesu odzyskiwania hello. 

## <a name="next-steps"></a>Następne kroki

Wyewidencjonuj toolearn tych zasobów, więcej informacji na temat kondycji zasobów:
-  [Przegląd kondycji zasobów platformy Azure](Resource-health-overview.md)
-  [Typy zasobów i kontrole kondycji dostępne w usłudze Azure Resource Health](resource-health-checks-resource-types.md)
