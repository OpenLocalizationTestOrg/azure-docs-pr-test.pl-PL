---
title: "aaaMonitoring i alerty tooSecurity odpowiada Operations Management Suite zabezpieczeń i inspekcji rozwiązania | Dokumentacja firmy Microsoft"
description: "Ten dokument pomaga możesz toouse hello zagrożeń analizy opcja dostępna w OMS zabezpieczeń i toomonitor inspekcji i Odpowiedz toosecurity alertów."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 7d45a32b-1341-4bb5-a436-1f42a8a2590a
ms.service: operations-management-suite
ms.custom: oms-security
ms.topic: article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/13/2017
ms.author: yurid
ms.openlocfilehash: 3d92b6809b7bd934c889afc119e5e34ff2b85f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-and-responding-toosecurity-alerts-in-operations-management-suite-security-and-audit-solution"></a>Monitorowanie i odpowiada alerty toosecurity Operations Management Suite zabezpieczeń i rozwiązanie inspekcji
Ten dokument ułatwia użyj opcji analizy zagrożeń hello dostępne w OMS zabezpieczeń i toomonitor inspekcji i reagowania na alerty toosecurity.

## <a name="what-is-oms"></a>Co to jest pakiet OMS?
Microsoft Operations Management Suite (OMS) to rozwiązanie do zarządzania IT, które pomaga zarządzać i chronić lokalnej i w chmurze infrastruktury opartej na chmurze firmy Microsoft. Aby uzyskać więcej informacji na temat pakietu OMS, przeczytaj artykuł hello [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx).

## <a name="threat-intelligence"></a>Analiza zagrożeń
W środowisku firmowym, których użytkownicy mają szeroki dostęp toohello sieci i korzystają z różnych urządzeń tooconnect toocorporate danych konieczne jest można aktywne monitorowanie zasobów i szybkie odpowiadanie toosecurity zdarzenia. Jest to szczególnie istotne z perspektywy cyklu życia zabezpieczeń hello, ponieważ niektóre bezpieczeństwa, które nie mogą zgłaszać zagrożenia alerty lub podejrzanych działań, które mogą zostać zidentyfikowane przez kontrolę techniczną tradycyjne zabezpieczenia. 

Za pomocą hello **analizy zagrożeń** opcja dostępna w OMS zabezpieczeń i inspekcji, Administratorzy IT można zidentyfikować zagrożenia bezpieczeństwa w środowisku hello, na przykład, ustalić, czy na określonym komputerze jest częścią [ botnet](https://www.microsoft.com/security/sir/story/default.aspx#!botnetsection). Komputery mogą stać się węzły w sieć botnet wykorzystywana osobom atakującym instalowania nielegalnemu złośliwego oprogramowania, które potajemnie łączy z tego polecenia toohello komputera i kontroli. Mogą też wskazać potencjalnych zagrożeń pochodzące z kanałów komunikacyjnych podziemnych, takich jak [darknet](https://www.microsoft.com/security/sir/story/default.aspx#!botnetsection_honeypots_darkents). 

W kolejności toobuild tej analizy zagrożeń bezpieczeństwa OMS i inspekcji użyć danych pochodzących z wielu źródeł w ramach firmy Microsoft. Zabezpieczenia OMS i inspekcji będzie korzystać z tego danych tooidentify potencjalnych zagrożeń dla środowiska.

Okienko analizy zagrożeń Hello składa się przez trzy główne sposoby:

* Serwery z wychodzącym ruchem złośliwego oprogramowania
* Typy wykrytych zagrożeń
* Mapa analizy zagrożeń

> [!NOTE]
> Omówienie tych opcji, należy przeczytać [wprowadzenie Operations Management Suite zabezpieczeń i rozwiązanie inspekcji](oms-security-getting-started.md).
> 
> 

### <a name="responding-toosecurity-alerts"></a>Odpowiada toosecurity alertów
Jeden z kroków hello [odpowiedzi na zdarzenia zabezpieczeń](https://technet.microsoft.com/library/cc512623.aspx) ważność hello tooidentify systemy naruszenia hello jest proces. Na tym etapie należy wykonać następujące zadania hello:

* Określić hello rodzaj atak powitania
* Określić atak powitania punkt początkowy
* Określ opcje hello atak powitania. Został atak powitania specjalnie skierowany w Twojej organizacji tooacquire określone informacje, czy został on losowe?
* Znalezienie hello komputerów, których bezpieczeństwo zostało naruszone
* Zidentyfikować hello pliki, które uzyskiwały zostały i określenie czułości hello tych plików

Można wykorzystać **analizy zagrożeń** informacji w OMS zabezpieczeń i inspekcji toohelp rozwiązania z tych zadań. Wykonaj kroki hello poniżej tooaccess, to **analizy zagrożeń** opcje:

1. W hello **programu Microsoft Operations Management Suite** głównym pulpicie nawigacyjnym kliknij **zabezpieczeń i inspekcji** kafelka.
   
    ![Bezpieczeństwo i inspekcji](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig1.png)
2. W hello **zabezpieczeń i inspekcji** pulpitu nawigacyjnego, zobaczysz hello **analizy zagrożeń** opcje w prawej hello, jak pokazano poniżej:
   
    ![Intel zagrożeń](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig2-ga.png)

Te trzy Kafelki zawiera przegląd hello bieżącego zagrożeń. W hello **serwera z wychodzącym ruchem złośliwego oprogramowania** Jeśli komputer, na którym są monitorowania (wewnątrz lub na zewnątrz sieci) będą mogli tooidentify czyli wysyłania ruchu złośliwego toohello Internet. 

Witaj **wykryto typy zagrożeń** kafelka zawiera podsumowanie informacji o hello zagrożenia, które są aktualne "w hello wild", po kliknięciu tego kafelka więcej informacji o tych zagrożeniach zostanie wyświetlone jako wyświetlane poniżej:

![Typy wykrytych zagrożeń](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig3.png)

Można wyodrębnić więcej informacji na temat każde zagrożenie, klikając go. przykład Witaj poniżej przedstawiono więcej informacji na temat Botnet:

![więcej informacji na temat zagrożenie](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig4.png)

Zgodnie z opisem w hello na początku tego tematu, informacja ta może być bardzo przydatne w przypadku odpowiedzi na zdarzenia. Go można też ważne podczas postępowania śledczego, której należy źródło hello toofind atak powitania, który system został naruszony i hello osi czasu. W tym raporcie można łatwo zidentyfikować niektóre najważniejsze szczegóły dotyczące atak powitania, takich jak: hello źródła atak powitania, hello lokalny adres IP, którego bezpieczeństwo zostało naruszone i hello stan połączenia hello bieżącej sesji. 

Witaj **mapy analizy zagrożeń** pomoże Ci tooidentify hello bieżące lokalizacje całym Witaj świecie mających szkodliwy ruch. Kolor pomarańczowy są (operacja przychodząca) i czerwone (wychodzące) strzałki na tej mapie identyfikujące hello kierunek ruchu, jeśli klikniesz przycisk w jednym z tych strzałki, zostanie wyświetlona hello rodzaju zagrożenia i hello kierunek ruchu, jak pokazano poniżej:

![Mapa analizy zagrożeń](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig5.png)

> [!NOTE]
> Można wyświetlić pokaz sposobu toouse tę możliwość w odpowiedzi na zdarzenia procesu obserwując prezentacji hello [ograniczenia zagrożeń zabezpieczeń w centrum danych z przewodnikiem postępowaniu przy użyciu usługi Operations Management Suite](https://myignite.microsoft.com/videos/5000) dostarczone w Ignite firmy Microsoft.
> 

### <a name="responding-toodistinct-malicious-ip-accessed"></a>Odpowiada toodistinct IP złośliwego dostęp
W niektórych scenariuszach możesz zauważyć potencjalnie złośliwy adres IP, do którego uzyskano dostęp z jednego z monitorowanych komputerów:

![Mapa analizy zagrożeń](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig6.png)

Ten alert i innych użytkowników w tej samej kategorii Witaj, są generowane przez OMS zabezpieczeń dzięki wykorzystaniu [analizy zagrożeń Microsoft](https://youtu.be/O4WtxgUrDc8). Hello danych analizy zagrożeń jest zbieranych przez firmę Microsoft a także zakupione z wiodącymi dostawcami analizy zagrożeń. Te dane jest często aktualizowana i dostosowywane przenoszenie toofast zagrożeń. Powodu charakter tooits powinny być połączone z innych źródeł informacji o zabezpieczeniach podczas [badanie](https://blogs.technet.microsoft.com/msoms/2016/12/08/investigating-suspicious-activity-in-a-hybrid-cloud-with-oms-security/) alert zabezpieczeń. 

## <a name="customize-alerts-received-via-e-mail"></a>Dostosowywanie alertów odebranych za pośrednictwem poczty e-mail

Można dostosować, którzy użytkownicy w organizacji zostanie powiadomiony, gdy alerty zabezpieczeń są wyzwalane przez zabezpieczenia OMS. Ta opcja jest dostępna w obszarze Przegląd / pulpit nawigacyjny OMS hello ustawienia na:

![Adres e-mail](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig7.png)

## <a name="see-also"></a>Zobacz też
W tym dokumencie możesz przedstawiono sposób toouse hello **analizy zagrożeń** opcji zabezpieczeń OMS i inspekcji alertów toosecurity toorespond rozwiązania. toolearn więcej informacji na temat zabezpieczeń OMS, zobacz następujące artykuły hello:

* [Omówienie pakietu Operations Management Suite (OMS)](operations-management-suite-overview.md)
* [Wprowadzenie do programu Operations Management Suite zabezpieczeń i rozwiązanie inspekcji](oms-security-getting-started.md)
* [Monitorowanie zasobów w rozwiązaniu Zabezpieczenia i inspekcja w pakiecie Operations Management Suite](oms-security-monitoring-resources.md)

