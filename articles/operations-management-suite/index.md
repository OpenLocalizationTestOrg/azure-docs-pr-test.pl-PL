---
title: "aaaAzure dokumentacji Operations Management Suite (OMS) — samouczki | Dokumentacja firmy Microsoft"
description: "Pakiet Microsoft Operations Management Suite (OMS) to oparte na chmurze rozwiązanie firmy Microsoft do zarządzania systemami IT, które ułatwia zarządzanie infrastrukturą lokalną i chmurową oraz jej ochronę. W tym artykule identyfikuje hello różnych usług objęte OMS i linki tootheir szczegółowe zawartości."
services: operations-management-suite
author: carolz
manager: carolz
layout: LandingPage
ms.assetid: 
ms.service: operations-management-suite
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: landing-page
ms.date: 01/23/2017
ms.author: carolz
ms.openlocfilehash: 11a8f5ecb3d84aed90554510fc1bb43320fdebb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-operations-management-suite-oms"></a>Co to jest pakiet Operations Management Suite (OMS)?
Pakiet Microsoft Operations Management Suite (OMS) to oparte na chmurze rozwiązanie firmy Microsoft do zarządzania systemami IT, które ułatwia zarządzanie infrastrukturą lokalną i chmurową oraz jej ochronę.  Ponieważ oprogramowanie OMS jest zaimplementowane jako usługa w chmurze, może być dostępne szybko przy minimalnym poziomie inwestycji w usługi infrastruktury.  Nowe funkcje są dostarczane automatycznie, co eliminuje koszty konserwacji i uaktualniania.

Ponadto tooproviding cenne usług na własną, OMS można zintegrować ze składnikami programu System Center, takich jak System Center Operations Manager tooextend istniejące inwestycje w technologie zarządzania hello chmury.  System Center i OMS mogą współdziałać ze sobą tooprovide zarządzania pełne hybrydowego.

następujące sekcje Hello Podaj opis wysokiego poziomu obszarów inną wartość hello OMS i hello usług, które ich wdrażania.  Przed hello Przeglądanie szczegółowe dokumentacji dla każdego mogą odwoływać się architektura tooOMS omówienie hello różne składniki pakietu OMS.

## <a name="insight-and-analyticsmediaoperations-management-suite-overviewicon-insight-analyticspng-insight-and-analytics"></a>![Wgląd w dane i analizy](media/operations-management-suite-overview/icon-insight-analytics.png) Wgląd w dane i analizy
[Usługa Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics) pomaga w zbieraniu, korelowaniu i wyszukiwaniu danych dziennika i danych wydajnościowych wygenerowanych przez systemy operacyjne i aplikacje, a także podejmowaniu odpowiednich działań na podstawie tych danych. Udostępnia w czasie rzeczywistym operational insights przy użyciu zintegrowanego wyszukiwania i tooreadily niestandardowe pulpity nawigacyjne analizowanie miliony rekordów dla wszystkich obciążeń i serwerów, niezależnie od ich lokalizacji fizycznej.

Możesz łatwo dodać tooLog rozwiązań analitycznych zdefiniuj toobe danych zebranych i hello logikę jego analizy.  Rozwiązania może zawierać dodatkowe funkcje, które automatycznie jest dostarczany tooagents z minimalnym lub żadna konfiguracja.  Ponadto narzędzia analizy toousing udostępniane przez poszczególne rozwiązania niestandardowe wyszukiwania można wykonywać w hello cały zestaw danych w kolejności toocorrelate danych między systemami i aplikacjami.  

## <a name="automation--controlmediaoperations-management-suite-overviewicon-automation-controlpng-automation--control"></a>![Automatyzacja i kontrola](media/operations-management-suite-overview/icon-automation-control.png) Automatyzacja i kontrola
Automatyzacja Azure pozwala zautomatyzować procesów administracyjnych z [elementów runbook](../automation/automation-runbook-types.md) które są oparte na programie PowerShell i uruchom w hello chmury Azure.  Elementy Runbook mają dostęp do dowolnego produktu lub usługi, którymi można zarządzać za pomocą programu PowerShell, w tym do zasobów znajdujących się w innych chmurach, jak Amazon Web Services (AWS).  Elementy Runbook mogą być również wykonywane na serwerze w danych lokalnych zasobów lokalnych toomanage Centrum.

Usługa Azure Automation udostępnia funkcję zarządzania konfiguracją za pomocą programu [PowerShell DSC](../automation/automation-dsc-overview.md).  Można tworzyć i zarządzanie zasobami DSC hostowana na platformie Azure i zastosować je toocloud i lokalnymi toodefine systemów i automatycznie wymuszać ich konfiguracji.

## <a name="protection-and-recoverymediaoperations-management-suite-overviewicon-protection-recoverypng-protection-and-disaster-recovery"></a>![Ochrona i odzyskiwanie](media/operations-management-suite-overview/icon-protection-recovery.png) Ochrona i odzyskiwanie po awarii
Usługa [Azure Backup](http://azure.microsoft.com/documentation/services/backup) chroni dane aplikacji i przechowuje je przez wiele lat bez konieczności ponoszenia jakichkolwiek inwestycji kapitałowych i przy minimalnych kosztach operacyjnych.  Dane z systemów Windows Server fizycznymi i wirtualnymi w dodanie tooapplication obciążeń, takich jak SQL Server i SharePoint jej kopii zapasowej.  Może również służyć przez System Center Data Protection Manager (DPM) tooreplicate chronionych danych tooAzure nadmiarowości i długoterminowego przechowywania.

[Usługa Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery) wspiera tooyour ciągłość i strategii odzyskiwania (BCDR) po awarii poprzez organizowanie replikacji, trybu failover i odzyskiwania na lokalne maszyny wirtualne funkcji Hyper-V, maszyny wirtualne VMware i fizyczne systemu Windows / Serwery systemu Linux. Można replikować maszyny tooa pomocniczego Centrum lub rozszerzyć poprzez replikację ich tooAzure centrum danych. Usługa Site Recovery udostępnia także prosty tryb failover oraz odzyskiwanie dla obciążeń. Integruje się z mechanizmami odzyskiwania po awarii, takimi jak SQL Server AlwaysOn, i udostępnia plany odzyskiwania w celu zapewnienia łatwego trybu failover dla obciążeń, które są rozmieszczone warstwowo na różnych maszynach.

## <a name="oms-security-and-compliancemediaoperations-management-suite-overviewicon-security-compliancepng-security-and-compliance"></a>![Zabezpieczenia i zgodność w ramach pakietu OMS](media/operations-management-suite-overview/icon-security-compliance.png) Zabezpieczenia i zgodność
Zabezpieczeń i zgodności pomaga zidentyfikować, oceny i ograniczyć zagrożenie bezpieczeństwa tooyour infrastruktury.  Te funkcje OMS są implementowane za pośrednictwem wielu rozwiązań w analizy dzienników, która analizowanie danych dziennika i konfiguracji na podstawie agent systemów tooassist przy równoczesnym zapewnieniu bezpieczeństwa trwającą hello środowiska.

* Witaj [rozwiązania zabezpieczeń i inspekcji](oms-security-getting-started.md) zbiera i analizuje zdarzenia zabezpieczeń w zarządzanych systemach tooidentify podejrzanych działań.
* Witaj [rozwiązania chroniące przed złośliwym kodem](../log-analytics/log-analytics-malware.md) raportów dotyczących stanu hello ochronę przed złośliwym oprogramowaniem w zarządzanych systemach.  
* Hello rozwiązania aktualizacji systemu przeprowadza analizę hello aktualizacje zabezpieczeń i innych aktualizacji na zarządzanych systemach, aby łatwo zidentyfikować systemy wymagające stosowanie poprawek.

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o usłudze [Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics).
* Dowiedz się więcej o usłudze [Azure Automation](../automation/automation-intro.md).
* Dowiedz się więcej o usłudze [Azure Backup](http://azure.microsoft.com/documentation/services/backup).
* Dowiedz się więcej o usłudze [Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery).

