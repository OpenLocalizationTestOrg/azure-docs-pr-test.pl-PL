---
title: "aaaRespond toosecurity zdarzenia z Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "W tym dokumencie opisano, jak toouse, Centrum zabezpieczeń Azure, scenariusz odpowiedzi na zdarzenia."
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 8af12f1c-4dce-4212-8ac4-170d4313492d
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: aaf50c0c7e774d03d517c3fd11686dbae48dd29b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-security-center-for-an-incident-response"></a>Używanie usługi Azure Security Center do reagowania na zdarzenia
W wielu organizacjach Dowiedz się jak incydenty toosecurity toorespond tylko po niewystarczający atak. koszty tooreduce i uszkodzenia, jest ważne toohave odpowiedzi na zdarzenia planu przed dokonaniem atak. Usługi Azure Security Center można używać na różnych etapach reagowania na zdarzenia.

## <a name="incident-response-planning"></a>Planowanie reagowania na zdarzenia
Efektywny plan zależy od trzech podstawowych możliwości: Trwa stanie tooprotect, wykrywania i reagowania toothreats. Ochrona dotyczy uniemożliwia zdarzenia, wykrywania jest temat wczesne identyfikowania zagrożeń i odpowiedź jest o wykluczania atakująca hello i przywracaniu systemów toomitigate hello wpływu jego naruszenia.

W tym artykule użyje etapach odpowiedzi na zdarzenia zabezpieczeń hello z hello [Response zabezpieczeń firmy Microsoft Azure w chmurze hello](https://gallery.technet.microsoft.com/Azure-Security-Response-in-dd18c678) artykułu, jak pokazano w powitania po diagramu:

![Cykl życia reakcji na zdarzenie](./media/security-center-incident-response/security-center-incident-response-fig1.png)

Centrum zabezpieczeń można użyć hello Wykryj, oceny i diagnozowanie etapach. Poniżej przedstawiono przykłady sposobu Centrum zabezpieczeń może być przydatne podczas hello trzech etapów początkowej odpowiedzi na zdarzenia:

* **Wykrywanie**: Przejrzyj hello pierwsze wskazanie dochodzenia zdarzeń.
  * Przykład: Przejrzyj hello wstępnej weryfikacji czy na pulpicie nawigacyjnym Centrum zabezpieczeń hello został zgłoszony alert zabezpieczeń o wysokim priorytecie.
* **Oceny**: wykonaj hello początkowej oceny tooobtain więcej informacji na temat hello podejrzanych działań.
  * Przykład: uzyskać więcej informacji na temat hello alertu zabezpieczeń.
* **Diagnozowanie**: przeprowadź badanie techniczne oraz określ strategię ograniczania ataku, łagodzenia jego skutków oraz możliwych obejść.
  * Przykład: wykonaj kroki korygowania hello opisanego przez Centrum zabezpieczeń w tym alert zabezpieczeń.

Hello scenariusz, w którym następuje pokazuje, jak tooleverage Centrum zabezpieczeń podczas hello Wykryj, oceny i diagnozowanie/odpowiedź etapu zdarzenia zabezpieczeń. W usłudze Security Center [zdarzenie zabezpieczeń](security-center-incident.md) to agregacja wszystkich alertów dotyczących zasobu, które są zgodne ze wzorcami ataku cybernetycznego typu [kill chain](https://blogs.technet.microsoft.com/office365security/addressing-your-cxos-top-five-cloud-security-concerns/). Zdarzenia są wyświetlane w hello [alerty zabezpieczeń](security-center-managing-and-responding-alerts.md) kafelków i bloku. Zdarzenie ujawnia hello listę powiązanych alertów, dzięki czemu możesz tooobtain więcej informacji na temat każdego wystąpienia. Centrum zabezpieczeń powoduje autonomiczny alerty zabezpieczeń, które mogą być również używane tootrack dół podejrzanych działań.

## <a name="scenario"></a>Scenariusz
Contoso niedawno migracji niektórych ich tooAzure zasobów lokalnych, w tym niektórych zadań biznesowych opartych na maszynach wirtualnych i baz danych. Obecnie zespół reagowania na zdarzenia zabezpieczeń firmy Contoso (CSIRT, Computer Security Incident Response Team) ma kłopot ze zbadaniem problemów dotyczących zabezpieczeń. Jest to spowodowane brakiem integracji funkcji analizy zabezpieczeń z ich obecnymi narzędziami do reagowania na zdarzenia. Ten brak integracji wprowadza problem podczas hello etap Wykryj (zbyt wiele fałszywych alarmów), a także podczas etapów Diagnozuj i hello oceny. W ramach tej migracji, zdecydowano, że tooopt w dla Centrum zabezpieczeń toohelp je rozwiązać ten problem.

Witaj tej migracji Zakończono pierwszą fazę po ich został załadowany wszystkich zasobów i rozwiązany, wszystkie hello zalecenia dotyczące zabezpieczeń w Centrum zabezpieczeń. Contoso CSIRT jest punkt centralny hello zajmujących się przypadki naruszenia zabezpieczeń komputera. zespół Hello składa się z grupy osób odpowiedzialnych za zajmowanie się wszystkie zdarzenia zabezpieczeń. Członkowie zespołu Hello wyraźnie zdefiniowanych tooensure obowiązków, że nie pozostaną bez obszaru odpowiedzi nie wykryte.

W celu hello tego scenariusza zamierzamy toofocus na powitania role powitania po osoby, które są częścią Contoso CSIRT:

![Cykl życia reakcji na zdarzenie](./media/security-center-incident-response/security-center-incident-response-fig2.png)

Magda zajmuje się operacjami zabezpieczeń. Jej obowiązki obejmują:

* Monitorowanie i odpowiada zagrożenia toosecurity wokół hello zegara.
* Coraz szybciej właściciel obciążenia chmury toohello lub analityk zabezpieczeń w razie potrzeby.

Szymon jest analitykiem zabezpieczeń i do jego obowiązków należą:

* Badanie ataków.
* Korygowanie działań na podstawie alertów.
* Praca z toodetermine właścicieli obciążeń i stosować środki zaradcze.

Jak widać, Jan i Sam mają różne obowiązki i muszą one współpracują ze sobą tooshare Centrum zabezpieczeń informacji.

## <a name="recommended-solution"></a>Zalecane rozwiązanie
Ponieważ Jan i Sam mają różne role, ich będziesz używać różnych obszarów Centrum zabezpieczeń tooobtain istotnych informacji dla ich codziennych działań. Magda używa **Alertów zabezpieczeń** w ramach codziennego monitorowania.

![Alerty zabezpieczeń](./media/security-center-incident-response/security-center-incident-response-fig3.png)

Jan użyje alerty zabezpieczeń podczas hello Wykryj i etapy oceny. Po zakończeniu początkowej oceny hello Jan użytkownik może przekazać tooSam problem hello Jeśli wymagane jest dodatkowe dochodzenia. W tym momencie Sam użyje hello informacji podanych przez Centrum zabezpieczeń, czasami w połączeniu z innymi źródłami danych toomove toohello Diagnozuj etapu.

## <a name="how-tooimplement-this-solution"></a>Jak tooimplement tego rozwiązania
toosee jak używasz Centrum zabezpieczeń Azure w scenariuszu odpowiedzi na zdarzenia, firma Microsoft będzie wykonaj kroki w Jan etapami hello Wykryj i oceny, a następnie zobacz, czego Sam toodiagnose hello problem.

### <a name="detect-and-assess-incident-response-stages"></a>Etapy wykrywania i oceniania w ramach reagowania na zdarzenie
Jan zalogowany toohello portalu Azure i działa w konsoli Centrum zabezpieczeń hello. W ramach swojej codziennie monitorowania działań klika pracy przeglądu zabezpieczeń o wysokim priorytecie, które hello alerty, wykonując następujące kroki:

1. Kliknij przycisk hello **alerty zabezpieczeń** hello kafelków i dostęp **alerty zabezpieczeń** bloku.
    ![Blok Alerty zabezpieczeń](./media/security-center-incident-response/security-center-incident-response-fig4.png)

   > [!NOTE]
   > W celu hello tego scenariusza Jan jest tooperform będzie ocenę na powitania SQL złośliwe działania alert, jak pokazano w powyższej ilustracji hello.
   >
   >
2. Kliknij przycisk hello **SQL złośliwe działania** alertów i przejrzyj hello zaatakowane zasoby w hello **SQL złośliwe działania** bloku: ![szczegóły zdarzenia](./media/security-center-incident-response/security-center-incident-response-fig5.png)

    W tym bloku Jan może zająć uwagi dotyczące atak powitania zasobów, jak wystąpiło wiele razy takiego ataku i jego wykrycia.
3. Kliknij przycisk hello **zaatakowany zasób** tooobtain więcej informacji na temat takiego ataku.

Po przeczytaniu opisu hello, Jan jest w przekonaniu, że nie jest to wynik fałszywie dodatni i że użytkownik podwyższania poziomu tej sprawy tooSam.

### <a name="diagnose-incident-response-stage"></a>Etap diagnozy w ramach reagowania na zdarzenie
Sam odbiera przypadku hello z Jan i uruchamia recenzowania hello korygowania kroki, które sugerowane w Centrum zabezpieczeń.

![Cykl życia reakcji na zdarzenie](./media/security-center-incident-response/security-center-incident-response-fig6.png)

### <a name="additional-resources"></a>Dodatkowe zasoby
Hello zespołu odpowiedzi na zdarzenia można również korzystać z hello [usługi Power BI Centrum zabezpieczeń](security-center-powerbi.md) możliwości toosee różnych typów raportów. Te raporty mogą pomóc w dalszych badań toovisualize, analizowanie i filtrowanie zaleceń oraz alertów zabezpieczeń. Dla firm, które używania ich informacji o zabezpieczeniach i rozwiązania do zarządzania (SIEM) zdarzenia w procesie dochodzenia hello, mogą one również [zintegrować z rozwiązaniem Centrum zabezpieczeń](security-center-integrating-alerts-with-log-integration.md). Można również zintegrować dzienników inspekcji platformy Azure i zdarzenia zabezpieczeń maszyny wirtualnej (VM) przy użyciu hello [narzędzia integracji dzienników Azure](https://blogs.msdn.microsoft.com/azuresecurity/2016/07/21/microsoft-azure-log-integration-preview/). tooinvestigate ataku, można użyć tych informacji w połączeniu z Centrum zabezpieczeń zawiera informacje hello.

## <a name="conclusion"></a>Podsumowanie
Składanie zespołu przed wystąpieniem zdarzenia jest bardzo ważne tooyour organizacji i wpływają pozytywnie obsługi zdarzeń. Witaj odpowiednich narzędzi toomonitor zasobów może pomóc tooremediate dokładne kroki tego zespołu tootake zdarzenia zabezpieczeń. Centrum zabezpieczeń [możliwości wykrywania](security-center-detection-capabilities.md) może pomóc toosecurity odpowiedź tooquickly informatycznego i Korygowanie problemów z zabezpieczeniami.
