---
title: "aaaMonitor stan replikacji usługi Active Directory z Azure Log Analytics | Dokumentacja firmy Microsoft"
description: "Witaj pakiet rozwiązania stan replikacji usługi Active Directory regularnie monitoruje środowiska usługi Active Directory dla wszelkie błędy replikacji i wyświetla wyniki hello na pulpicie nawigacyjnym OMS."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 1b988972-8e01-4f83-a7f4-87f62778f91d
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 235e4f7a066ea50b79f681398182b22c91fb6d31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-active-directory-replication-status-with-log-analytics"></a>Monitoruje stan replikacji usługi Active Directory z analizy dzienników

![Symbol stan replikacji usługi AD](./media/log-analytics-ad-replication-status/ad-replication-status-symbol.png)

Usługa Active Directory jest kluczowym elementem w środowisku INFORMATYCZNYM przedsiębiorstwa. tooensure wysoką dostępność i wysoką wydajność, każdy kontroler domeny ma własną kopię bazy danych usługi Active Directory hello. Kontrolery domeny replikowanie ze sobą w kolejności toopropagate zmiany w przedsiębiorstwie hello. W tym procesie replikacji mogą powodować różne problemy dla hello przedsiębiorstwa.

Hello pakiet rozwiązania stan replikacji AD regularnie monitoruje środowiska usługi Active Directory dla wszelkie błędy replikacji i wyświetla wyniki hello na pulpicie nawigacyjnym OMS.

## <a name="installing-and-configuring-hello-solution"></a>Instalowanie i konfigurowanie hello rozwiązania
Użyj powitania po tooinstall informacji i skonfiguruj hello rozwiązania.

* Należy zainstalować agentów na kontrolery domeny, które są członkami toobe domeny hello obliczone. Lub, należy zainstalować agentów na serwerach członkowskich i skonfigurować hello agentów toosend AD replikacji danych tooOMS. toounderstand tooconnect tooOMS komputerów z systemem Windows, zobacz temat [tooLog komputerów Windows połączyć Analytics](log-analytics-windows-agents.md). Jeśli kontroler domeny jest już częścią istniejącego środowiska System Center Operations Manager, które mają tooconnect tooOMS, zobacz [tooLog połączenie programu Operations Manager Analytics](log-analytics-om-agents.md).
* Dodaj tooyour rozwiązania hello stan replikacji usługi Active Directory z obszarem roboczym pakietu OMS za pomocą hello procesu opisanego w [rozwiązań analizy dzienników dodać hello galerii rozwiązań](log-analytics-add-solutions.md).  Nie są wymagane żadne dalsze czynności konfiguracyjne.

## <a name="ad-replication-status-data-collection-details"></a>Szczegóły kolekcji danych stanu replikacji usługi AD
Witaj poniższej tabeli przedstawiono metody zbierania danych i inne szczegółowe informacje o jak zbierane są dane, stan replikacji usługi AD.

| Platformy | Bezpośrednie agenta | Agenta programu SCOM | Azure Storage | SCOM wymagane? | Dane agenta programu SCOM wysyłane za pośrednictwem grupy zarządzania | Częstotliwość kolekcji |
| --- | --- | --- | --- | --- | --- | --- |
| Windows |&#8226; |&#8226; |  |  |&#8226; |co pięć dni |

## <a name="optionally-enable-a-non-domain-controller-toosend-ad-data-toooms"></a>Opcjonalnie możesz włączyć tooOMS danych toosend AD nie jest kontrolerem domeny
Jeśli nie chcesz tooconnect poszczególnych kontrolerów domeny bezpośrednio tooOMS, można użyć dowolnego innego komputera podłączony OMS w Twojej toocollect domeny dane hello rozwiązania stan replikacji AD pakiet i jego wysyłania danych hello.

### <a name="tooenable-a-non-domain-controller-toosend-ad-data-toooms"></a>tooenable tooOMS danych toosend AD nie jest kontrolerem domeny
1. Sprawdź, czy tego komputera hello jest członkiem domeny hello, że chcesz toomonitor za pomocą rozwiązania stan replikacji hello AD.
2. [Połącz tooOMS komputera z systemem Windows hello](log-analytics-windows-agents.md) lub [połączyć za pomocą programu istniejących tooOMS środowiska programu Operations Manager](log-analytics-om-agents.md), jeśli nie jest już połączony.
3. Na tym komputerze należy ustawić powitania po klucz rejestru:

   * Klucz: **grup wartość HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\HealthService\Parameters\Management\<ManagementGroupName > \Solutions\ADReplication**
   * Wartość: **IsTarget**
   * Dane wartości: **wartość true**

   > [!NOTE]
   > Te zmiany nie będą obowiązywać do Twojej hello ponowne uruchomienie usługi Microsoft Monitoring Agent (HealthService.exe).
   >
   >

## <a name="understanding-replication-errors"></a>Opis błędów replikacji
Po utworzeniu dane stanu replikacji AD przesyłane tooOMS, zobaczysz kafelka toohello podobne, po obraz na pulpicie nawigacyjnym OMS hello wskazującą liczbę błędów replikacji aktualnie.  
![Stan replikacji AD kafelka](./media/log-analytics-ad-replication-status/oms-ad-replication-tile.png)

**Błędy krytyczne replikacji** błędów, które są co najmniej 75% hello [okresu istnienia reliktu](https://technet.microsoft.com/library/cc784932%28v=ws.10%29.aspx) dla lasu usługi Active Directory.

Po kliknięciu kafelka hello można wyświetlić więcej informacji na temat błędów hello.
![Pulpit nawigacyjny stan replikacji usługi AD](./media/log-analytics-ad-replication-status/oms-ad-replication-dash.png)

### <a name="destination-server-status-and-source-server-status"></a>Stan serwera docelowego i stan serwera źródłowego
Te kolumny zawierają hello stan serwerów docelowych i serwerów źródłowych, których wystąpiły błędy replikacji. Liczba powitania po nazwie kontrolera domeny wskazuje hello liczbę błędów replikacji na tym kontrolerze domeny.

błędy powitania dla serwerów docelowych i serwerów źródłowych są wyświetlane, ponieważ niektóre problemy są łatwiejsze tootroubleshoot z perspektywy serwera źródłowego hello i inne osoby z perspektywy serwera docelowego hello.

W tym przykładzie widać, około ma wiele serwerów docelowych hello samą liczbę błędów, ale istnieje jeden serwer źródłowy (ADDC35), który ma wiele błędów więcej niż hello wszystkich innych użytkowników. Istnieje prawdopodobieństwo, że jest jakiś problem na ADDC35, która powoduje partnerami replikacji tooits toofail toosend danych. Rozwiązywanie problemów z hello na ADDC35 może rozwiązać wiele błędów hello, które są wyświetlane w obszarze serwera docelowego hello.

### <a name="replication-error-types"></a>Typy błędów replikacji
Ten obszar zawiera informacje o typach hello błędy wykryte w całym przedsiębiorstwie. Każdy z błędów ma unikatowy kod numeryczne i komunikat, który może pomóc w określeniu hello głównej przyczyny błędu hello.

pierścień Hello u góry hello daje pomysł, w których występują błędy więcej i mniej często w danym środowisku.

Przedstawia on po wielu kontrolerów domeny wystąpić hello sam błąd replikacji. W takim przypadku należy może toodiscover może być lub identyfikowania rozwiązania na jeden kontroler domeny, a następnie powtórz ją na innych kontrolerach domeny dotyczy hello sam błąd.

### <a name="tombstone-lifetime"></a>Okresu istnienia reliktu
okresu istnienia reliktu Hello, określa, jak długo usuniętego obiektu określonego tooas reliktów, są przechowywane w bazie danych usługi Active Directory hello. Gdy usuniętego obiektu przekazuje hello okresu istnienia reliktu, proces zbierania odzyskiwanie automatycznie spowoduje usunięcie jej z bazy danych usługi Active Directory hello.

okresu istnienia reliktu domyślne Hello jest 180 dni do najnowszej wersji systemu Windows, ale był 60 dni w starszych wersjach, a można go zmienić jawnie przez administratora usługi Active Directory.

Jeśli występują błędy replikacji, które zbliża się lub upłynął okres istnienia reliktu hello jest ważne tooknow. Jeśli dwa kontrolery domeny wystąpi błąd replikacji, który będzie się powtarzać, poza okresu istnienia reliktu hello, wyłączyć replikacji między te dwa kontrolery domeny, nawet wtedy, gdy podstawowy błąd replikacji hello jest stała.

Witaj obszaru okresu istnienia reliktu pomaga zidentyfikować miejsca, w którym wyłączone replikacji jest w toku. Każdy z błędów hello **ponad 100% TSL** kategorii reprezentuje partycji, która nie została zreplikowana między jego źródłowy i docelowy serwer w co najmniej okresu istnienia reliktu hello hello lasu.

W takim przypadku po prostu ustalania hello błąd replikacji nie będzie wystarczającej ilości. Co najmniej należy toomanually zbadać tooidentify i wyczyścić pokutujące obiekty przed ponownym uruchomieniem replikacji. Może być konieczne nawet toodecommission kontrolera domeny.

W dodatku tooidentifying wszystkie błędy replikacji, które trwają poza okresu istnienia reliktu hello, również ma błędy tooany uwagi toopay należących do hello **TSL 50 75%** lub **TSL 75 100%** kategorie.

Są to błędy, które są wyraźnie pokutujących, nie jest przejściowe, więc prawdopodobnie potrzebują tooresolve Twojego interwencji. Dobra wiadomość Hello jest, że ich nie osiągnęły jeszcze okresu istnienia reliktu hello. Jeśli szybko rozwiązać te problemy i *przed* osiągną okresu istnienia reliktu hello, replikacji można ponownie uruchomić z minimalnym ręcznej interwencji.

Jak wspomniano wcześniej, hello kafelka pulpitu nawigacyjnego rozwiązania stan replikacji hello AD pokazuje liczbę hello *krytyczne* błędy replikacji w danym środowisku, który jest zdefiniowany jako błędy, które są ponad 75% okresu istnienia reliktu (w tym błędy, które są ponad 100% TSL). Dokładamy wszelkich starań, tookeep tego numeru w lokalizacji 0.

> [!NOTE]
> Wszystkich obliczeń wartość procentowa okresu istnienia reliktu hello są oparte na powitania rzeczywiste reliktu lasu usługi Active Directory, więc ufasz, że te wartości procentowe są poprawne, nawet jeśli ma wartość okresu istnienia reliktu niestandardowych, ustaw.
>
>

### <a name="ad-replication-status-details"></a>Szczegóły stanu replikacji usługi AD
Kliknij dowolny element w jednej z list hello, pojawić się dodatkowe szczegóły dotyczące za pomocą wyszukiwania dziennika. Witaj wyniki są filtrowane tooshow tylko hello błędów pokrewnych toothat elementu. Na przykład po kliknięciu hello pierwszego kontrolera domeny są wyświetlane w obszarze **stan serwera docelowego (ADDC02)**, zobaczysz, że wyniki wyszukiwania filtrowane tooshow błędy z tego kontrolera domeny na liście jako serwer docelowy hello:

![Błędy stanu replikacji usługi AD w wynikach wyszukiwania](./media/log-analytics-ad-replication-status/oms-ad-replication-search-details.png)

W tym miejscu można filtrować dalsze, zmodyfikować zapytanie wyszukiwania hello i tak dalej. Aby uzyskać więcej informacji o używaniu hello wyszukiwania dziennika, zobacz [dziennika wyszukiwania](log-analytics-log-searches.md).

Witaj **HelpLink** pole zawiera hello adres URL strony TechNet dodatkowe informacje dotyczące tego błędu. Można skopiować i wkleić to łącze do informacji toosee okna przeglądarki o Rozwiązywanie problemów i naprawienie błędów hello.

Możesz również kliknąć **wyeksportować** tooexport hello powoduje tooExcel. Eksportowanie danych hello może pomóc wizualizacji danych błąd replikacji w żaden sposób, który chcesz.

![błędy stanu replikacji AD wyeksportowanego w programie Excel](./media/log-analytics-ad-replication-status/oms-ad-replication-export.png)

## <a name="ad-replication-status-faq"></a>Stan replikacji AD — często zadawane pytania
**Pytanie: jak często jest zaktualizowane dane o stanie replikacji AD?**
Odpowiedź: hello informacje są aktualizowane co pięć dni.

**Pytanie: czy istnieje tooconfigure sposób, jak często są aktualizowane dane?**
Odpowiedź: nie w tej chwili.

**Pytanie: należy tooadd wszystkie moje domeny kontrolery toomy obszarem roboczym pakietu OMS w stan replikacji toosee kolejności?**
Odpowiedź: nie można dodać tylko jednego kontrolera domeny. Jeśli masz wiele kontrolerów domeny w obszarze roboczym pakietu OMS tooOMS wysłaniu danych z wszystkich z nich.

**Pytanie: nie chcę tooadd wszystkie domeny kontrolery toomy obszarem roboczym pakietu OMS. Można nadal korzystać z hello rozwiązania stan replikacji usługi AD?**
Odpowiedź: tak. Można ustawić wartości hello tooenable klucza rejestru go. Zobacz [tooenable tooOMS danych toosend AD kontrolera domeny z systemem innym niż](#to-enable-a-non-domain-controller-to-send-ad-data-to-oms).

**Pytanie: co to jest nazwa hello procesu hello hello zbierania danych?**
A: AdvisorAssessment.exe

**Pytanie: jak długo trwa dla toobe dane zbierane?**
A: czas zbierania danych zależy od rozmiaru hello hello środowiska usługi Active Directory, ale zazwyczaj trwa mniej niż 15 minut.

**Pytanie: typ danych zbieranych?**
A: informacje o replikacji zbieranych za pośrednictwem protokołu LDAP.

**Pytanie: czy istnieje tooconfigure sposób podczas zbierania danych?**
Odpowiedź: nie w tej chwili.

**Pytanie: co zrobić uprawnienia potrzebne toocollect danych?**
A: zwykłego użytkownika uprawnień tooActive katalogu są wystarczające.

## <a name="troubleshoot-data-collection-problems"></a>Rozwiązywanie problemów zbierania danych
W danych toocollect pakiet rozwiązania stan replikacji hello AD wymaga co najmniej jednej domeny kontrolera toobe połączone tooyour obszarem roboczym pakietu OMS. Dopiero po nawiązaniu połączenia kontrolera domeny, pojawi się komunikat wskazujący, że **nadal są zbierane dane**.

Jeśli potrzebujesz pomocy przy podłączaniu jeden z kontrolerów domeny, można wyświetlić dokumentację w [tooLog komputerów Windows połączyć Analytics](log-analytics-windows-agents.md). Alternatywnie, jeśli kontroler domeny jest już połączony tooan istniejącego środowiska System Center Operations Manager, można wyświetlić dokumentację w [tooLog połączyć System Center Operations Manager Analytics](log-analytics-om-agents.md).

Jeśli nie chcesz tooconnect poszczególnych kontrolerów domeny bezpośrednio tooOMS lub tooSCOM, zobacz [tooenable tooOMS danych toosend AD kontrolera domeny z systemem innym niż](#to-enable-a-non-domain-controller-to-send-ad-data-to-oms).

## <a name="next-steps"></a>Następne kroki
* Użyj [Zaloguj wyszukiwania analizy dzienników](log-analytics-log-searches.md) tooview szczegółowe dane stanu replikacja usługi Active Directory.
