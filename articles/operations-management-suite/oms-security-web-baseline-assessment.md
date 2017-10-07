---
title: "aaaWeb oceny linii bazowej w Operations Management Suite zabezpieczeń i inspekcji rozwiązania bazową | Dokumentacja firmy Microsoft"
description: "W tym dokumencie opisano, jak toouse sieci web oceny linii bazowej w OMS zabezpieczeń i inspekcji tooperform rozwiązania na podstawie oceny linii bazowej wszystkich serwerów sieci web monitorowane w celu zgodności i zabezpieczeń."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 17837c8b-3e79-47c0-9b83-a51c6ca44ca6
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: yurid
ms.openlocfilehash: dafa9d3d93fae31748306b60ee40b285dd59c802
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="web-baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a>Ocena linii bazowej sieci Web w rozwiązaniu Zabezpieczenia i inspekcja w pakiecie Operations Management Suite
Ten dokument ułatwia korzystanie z zabezpieczeń OMS i inspekcji sieci web linii bazowej oceny możliwości tooaccess hello bezpieczny stan monitorowanych zasobów.

## <a name="what-is-web-baseline-assessment"></a>Co to jest ocena internetowej linii bazowej?
Obecnie rozwiązanie Zabezpieczenia w pakiecie OMS umożliwia ocenę podstawy linii bazowej zabezpieczeń systemów operacyjnych. Skanuje hello ustawień systemu operacyjnego serwerów co 24 godziny i zapewnia wgląd do ustawienia potencjalnie narażone. Przeczytaj artykuł [Ocena linii bazowej w rozwiązaniu Zabezpieczenia i inspekcja w pakiecie Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/oms-security-baseline), aby uzyskać więcej informacji na ten temat.

Celem Hello hello oceny linii bazowej sieci Web jest ustawień serwera sieci web potencjalnie narażone toofind. Witaj trzech źródeł podstawowy to hello web linii bazowej konfiguracji: konfiguracji platformy .NET, ASP.NET oraz usług IIS.  Podobnie jak hello ocenę linii bazowej systemu operacyjnego, OMS zabezpieczeń będzie tooscan Twojego serwery sieci web co 24hrs i podaj zapewnia wgląd w ich stanie zabezpieczeń.  W konsoli Internet Information Service (IIS) konfiguracje są dużym stopniu dostosowywane umożliwiającą różnych witryny i aplikacji toobe poziomy zastąpiona. Skaner Hello sprawdza ustawienia hello na każdym poziomie witryny/aplikacji dodanie toohello domyślnego katalogu głównego poziomu. To ułatwia tooidentify potencjalnie narażone ustawienia i szybko skorygować wraz z Nasze zalecenia dotyczące tych ustawień.

>[!NOTE] 
>Możesz pobrać hello typowych konfiguracji identyfikatorów i używane przez OMS zabezpieczeń w tym reguły linii bazowej [strony](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335?redir=0).


## <a name="web-security-baseline-assessment"></a>Ocena internetowej linii bazowej zabezpieczeń

Dla tej wersji zapoznawczej funkcji hello są dostępne za pośrednictwem hello opcję wyszukiwania OMS i hello OMS zabezpieczeń i inspekcji pulpitu nawigacyjnego. Wykonaj kroki hello poniżej tooperform hello przeznaczona zapytania:

1. W hello **programu Microsoft Operations Management Suite** głównym pulpicie nawigacyjnym, kliknij przycisk **zabezpieczeń i inspekcji** kafelka.
2. W hello **zabezpieczeń i inspekcji** pulpitu nawigacyjnego, zostanie wyświetlony hello linii bazowej sieci Web perspektywy dalej toohello OS linii bazowej perspektywy.
   
    ![Ocena internetowej linii bazowej w rozwiązaniu Security and Audit w pakiecie OMS](./media/oms-security-web-baseline/oms-security-web-baseline-fig5.png)

3. w okienku po lewej stronie powitania pokazuje liczbę hello serwerów sieci Web w porównaniu toohello linii bazowej, hello średnią wartość procentową reguł, które są przekazywane na wszystkich serwerach hello obliczone i hello listę serwerów, które zostały ocenione.
4. Hello w prawym okienku wymieniono hello unikatowe zasady zakończonych niepowodzeniem przez *ważność*, i *typ*. Klikając na dowolnym zasad w okienku po prawej stronie powitania wyświetli szczegóły hello tej reguły. Przykładem jest wyświetlany w hello poniżej obrazu. Reguła Hello, której wartość jest szacowana znajduje się w obszarze *ustawienia reguł*. Witaj *AzId* pola, które jest unikatowym identyfikatorem dla każdej reguły używane przez firmę Microsoft do śledzenia hello reguły linii bazowej. Ponadto toothat użytkownicy będą mogli zobaczyć hello *oczekiwany wynik* (wartość zalecane przez firmę Microsoft), i inne szczegóły dotyczące wpływu zabezpieczeń hello hello reguły.
    
    ![Zapytanie](./media/oms-security-web-baseline/oms-security-web-baseline-fig6.png)

5. Można utworzyć własne zapytania tooreview hello wyniki. 

Hello pierwszego zapytania, którego można używać jest hello **podsumowanie oceny linii bazowej sieci Web**. W hello **tutaj wyszukiwania Begin** wpisz tego zapytania: *typu = SecurityBaselineSummary BaselineType = Web*. Witaj poniżej przedstawiono przykładowe dane wyjściowe:

![Wynik zapytania](./media/oms-security-web-baseline/oms-security-web-baseline-fig7.png)

>[!NOTE] 
>W tym zapytaniu każdy rekord wskazuje podsumowanie oceny na jednym serwerze.

Po przejściu do hello **wyszukiwania dziennika**, można wpisać tooobtain różne zapytania więcej informacji na temat oceny linii bazowej sieci web hello. Ponadto toohello poprzednie zapytanie, umożliwia także powitania od tych w tej wersji zapoznawczej:

**Ocena reguły linii bazowej sieci Web**: każdy rekord reprezentuje jedną ocenę reguły linii bazowej sieci Web na jednym serwerze. Zawiera wszystkie dane w przypadku niepowodzenia reguły hello *SitePath* na które hello reguły oszacowano, hello *oczekiwany wynik*i hello *rzeczywisty wynik*.

Zapytanie: *Type=SecurityBaseline BaselineType=Web AnalyzeResult=Failed*

![Wynik zapytania 2](./media/oms-security-web-baseline/oms-security-web-baseline-fig8.png)

**Pokaż wszystkie wyniki dla określonego serwera**: to zapytanie pokazuje, jak powoduje toosee określonego serwera: zapytania: *typu = SecurityBaseline BaselineType = sieci Web = BaselineTestVM1*

![Wynik zapytania 3](./media/oms-security-web-baseline/oms-security-web-baseline-fig3.png)

Te rekordy/kwerendy toocreate można użyć własnych pulpity nawigacyjne, raporty lub alerty. Oto przykładowe formantu interfejsu użytkownika, dodać tooyour pulpitu nawigacyjnego. Aby dowiedzieć się jak toovisualize dane przy użyciu projektanta widoków OMS [tutaj](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/). poniższym zrzucie ekranu Hello jest przykładem sposobu hello kafelka będzie wyglądać po wprowadzeniu takie dostosowanie.

![pulpit nawigacyjny](./media/oms-security-web-baseline/oms-security-web-baseline-fig4.png)

## <a name="see-also"></a>Zobacz też
W tym dokumencie przedstawiono informacje na temat oceny internetowej linii bazowej w rozwiązaniu Security and Audit w pakiecie OMS. toolearn więcej informacji na temat zabezpieczeń OMS, zobacz następujące artykuły hello:

* [Omówienie pakietu Operations Management Suite (OMS)](operations-management-suite-overview.md)
* [Monitorowanie i alerty tooSecurity odpowiada Operations Management Suite zabezpieczeń i rozwiązanie inspekcji](oms-security-responding-alerts.md)
* [Monitorowanie zasobów w rozwiązaniu Zabezpieczenia i inspekcja w pakiecie Operations Management Suite](oms-security-monitoring-resources.md)

