---
title: "aaaOperations zabezpieczeń pakietu administracyjnego i inspekcji rozwiązanie sieci Web bazową | Dokumentacja firmy Microsoft"
description: "W tym dokumencie opisano sposób toouse OMS zabezpieczeń i inspekcji rozwiązania tooperform oceny linii bazowej sieci web, wszystkich serwerów sieci web monitorowane w celu zgodności i zabezpieczeń."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ROBOTS: NOINDEX
redirect_url: https://www.microsoft.com/cloud-platform/security-and-compliance
ms.assetid: 17837c8b-3e79-47c0-9b83-a51c6ca44ca6
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: yurid
ms.openlocfilehash: 8aa87fa404ff97ab549dda3f9bebb75766055963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="web-baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a>Ocena linii bazowej sieci Web w rozwiązaniu Zabezpieczenia i inspekcja w pakiecie Operations Management Suite
Ten dokument ułatwia toouse [zabezpieczeń Operations Management Suite (OMS) i rozwiązania inspekcji](operations-management-suite-overview.md) oceny linii bazowej tooaccess możliwości hello bezpieczny stan monitorowanych zasobów w sieci web.

## <a name="what-is-web-baseline-assessment"></a>Co to jest ocena linii bazowej sieci Web?
Obecnie rozwiązanie Zabezpieczenia w pakiecie OMS umożliwia ocenę podstawy linii bazowej zabezpieczeń systemów operacyjnych. Skanuje hello ustawień systemu operacyjnego serwerów co 24 godziny i zapewnia wgląd do ustawienia potencjalnie narażone. Przeczytaj artykuł [Ocena linii bazowej w rozwiązaniu Zabezpieczenia i inspekcja w pakiecie Operations Management Suite](oms-security-baseline.md), aby uzyskać więcej informacji na ten temat.

Celem Hello oceny linii bazowej sieci web hello jest ustawień serwera sieci web potencjalnie narażone toofind. Witaj trzech źródeł podstawowy to hello web linii bazowej konfiguracji: konfiguracji platformy .NET, ASP.NET oraz usług IIS.  Podobnie jak hello ocenę linii bazowej systemu operacyjnego, OMS zabezpieczeń będzie tooscan Twojego serwery sieci web co 24hrs i podaj zapewnia wgląd w ich stanie zabezpieczeń.  W konsoli Internet Information Service (IIS) konfiguracje są dużym stopniu dostosowywane umożliwiającą różnych witryny i aplikacji toobe poziomy zastąpiona. Skaner Hello sprawdza ustawienia hello na każdym poziomie witryny/aplikacji dodanie toohello domyślnego katalogu głównego poziomu. To ułatwia tooidentify potencjalnych luk w zabezpieczeniach ustawienia lokalizacji i szybko skorygować.


## <a name="web-security-baseline-assessment"></a>Ocena linii bazowej zabezpieczeń sieci Web
Dla tej wersji zapoznawczej tej funkcji będzie toobe dostęp za pomocą opcji wyszukiwania OMS hello. Wykonaj kroki hello poniżej tooperform hello przeznaczona zapytania:

1. W hello **programu Microsoft Operations Management Suite** głównym pulpicie nawigacyjnym kliknij **zabezpieczeń i inspekcji** kafelka.
2. W hello **zabezpieczeń i inspekcji** pulpitu nawigacyjnego, kliknij przycisk **wyszukiwania dziennika** przycisku.
3. Hello pierwszego zapytania, którego można używać jest hello **podsumowanie oceny linii bazowej sieci Web**. W hello **tutaj wyszukiwania Begin** wpisz tego zapytania: typ*= SecurityBaselineSummary BaselineType = sieci web*. po ekranie powitania zawiera przykładowe dane wyjściowe:

![Podsumowanie oceny linii bazowej sieci Web](./media/oms-security-web-baseline/oms-security-web-baseline-fig1-new.png)

> [!NOTE]
> W tym zapytaniu każdy rekord wskazuje podsumowanie oceny na jednym serwerze.

Po przejściu do hello **wyszukiwania dziennika**, można wpisać tooobtain różne zapytania więcej informacji na temat oceny linii bazowej sieci web hello. Ponadto toohello poprzednie zapytanie, umożliwia także powitania od tych w tej wersji zapoznawczej.

**Ocena reguły linii bazowej sieci Web**: każdy rekord reprezentuje jedną ocenę reguły linii bazowej sieci Web na jednym serwerze. Zawiera wszystkie dane dla reguły hello, lokalizacji hello oczekiwano wyników i hello rzeczywisty wynik.

**Zapytanie**: Type*=SecurityBaseline BaselineType=web*

![Ocena reguły linii bazowej sieci Web](./media/oms-security-web-baseline/oms-security-web-baseline-fig2.png)

**Pokaż wszystkie wyniki dla określonego serwera**: to zapytanie pokazuje, jak toosee wyniki z określonego serwera.

**Zapytanie**: *Type=SecurityBaseline BaselineType=web Computer=BaselineTestVM1*

![Wszystkie wyniki](./media/oms-security-web-baseline/oms-security-web-baseline-fig3.png)

Umożliwia także te rekordy/kwerendy toocreate własne pulpity nawigacyjne, raporty lub alerty. Witaj ekranu poniżej zawiera formant interfejsu użytkownika próbki dodać tooyour pulpitu nawigacyjnego. Aby dowiedzieć się jak toovisualize dane przy użyciu projektanta widoków OMS [tutaj](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/). poniższym zrzucie ekranu Hello jest przykładem sposobu hello kafelka będzie wyglądać po wprowadzeniu takie dostosowanie.

![Przykładowy interfejs użytkownika](./media/oms-security-web-baseline/oms-security-web-baseline-fig4.png)

> [!NOTE]
> Jeśli chcesz tooknow hello ustawień, które są sprawdzane pod kątem oceny linii bazowej hello, możesz pobrać [ten arkusz kalkulacyjny programu Excel](https://gallery.technet.microsoft.com/OMS-Web-Baseline-1e811690) zawiera tych ustawień.

## <a name="see-also"></a>Zobacz też
Ten dokument przedstawia informacje na temat oceny linii bazowej sieci Web w rozwiązaniu Zabezpieczenia i inspekcja w pakiecie OMS. toolearn więcej informacji na temat zabezpieczeń OMS, zobacz następujące artykuły hello:

* [Omówienie pakietu Operations Management Suite (OMS)](operations-management-suite-overview.md)
* [Monitorowanie i alerty tooSecurity odpowiada Operations Management Suite zabezpieczeń i rozwiązanie inspekcji](oms-security-responding-alerts.md)
* [Monitorowanie zasobów w rozwiązaniu Zabezpieczenia i inspekcja w pakiecie Operations Management Suite](oms-security-monitoring-resources.md)

