---
title: "aaaTroubleshooting i monitorowania programu SAP HANA na platformie Azure (wystąpienia duże) | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów i monitorowanie SAP HANA na platformie Azure (wystąpienia duże)."
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1f1cd35820e227fd99af495431cd4b826aa53600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootroubleshoot-and-monitor-sap-hana-large-instances-on-azure"></a>Jak tootroubleshoot i monitor SAP HANA (duże wystąpień) w systemie Azure


## <a name="monitoring-in-sap-hana-on-azure-large-instances"></a>Monitorowanie SAP HANA na platformie Azure (wystąpienia duże)

SAP HANA na platformie Azure (wystąpienia duże) nie różni się od innych wdrożeń IaaS — muszą toomonitor co hello systemu operacyjnego, a aplikacja hello jest to, jak korzystać z tych hello następujące zasoby:

- Procesor CPU
- Memory (Pamięć)
- Przepustowość sieci
- Miejsce na dysku

Zgodnie z maszyn wirtualnych Azure należy toofigure czy hello klasy zasobów o nazwie powyżej są wystarczające, lub czy pobrać te wyczerpany. Poniżej przedstawiono więcej szczegółów na każdym z różnych klas hello:

**Zużycie zasobów procesora CPU:** hello zdefiniowanego dla niektórych obciążeń przed HANA SAP jest wymuszone toomake się upewnić, że powinien być za mało toowork dostępne zasoby procesora CPU przez hello dane są przechowywane w pamięci. Niemniej jednak może być przypadki, w którym HANA zużywa wiele zasobów procesora, wykonywanie kwerend indeksów toomissing lub podobne problemy. Oznacza to, że należy monitorować zużycia zasobów procesora CPU hello HANA dużych wystąpienia jednostki, a także zasobów Procesora używanych przez hello określonych usług HANA.

**Zużycie pamięci:** jest ważne toomonitor z wewnątrz HANA, a także poza HANA na powitania jednostki. W ramach HANA monitorować jak hello danych zajmuje przydzielonej pamięci w kolejności toostay w hello wymagane zmiany rozmiaru wytyczne SAP HANA. Należy zawsze toomonitor zużycie pamięci na powitania dużych wystąpienia poziomu toomake się, że dodatkowe zainstalowanych z systemem innym niż — HANA oprogramowania nie zużywa zbyt dużej ilości pamięci i w związku z tym konkurują ze HANA pamięci.

**Przepustowość sieci:** hello bramy sieci wirtualnej Azure ma ograniczoną przepustowość danych do hello sieci wirtualnej Azure, dlatego warto odebrane przez wszystkie dane hello toomonitor hello maszyn wirtualnych Azure w ramach toofigure sieci wirtualnej, jak blisko jest toohello limitów hello Azure wybrano jednostki SKU bramy. W jednostce wystąpienia dużych HANA hello sprawia, że znaczeniu toomonitor przychodzący i wychodzący ruch sieciowy również i Śledź tookeep hello woluminów, które są obsługiwane w czasie.

**Miejsce na dysku:** użycie miejsca na dysku zwykle zwiększa się wraz z upływem czasu. Istnieje wiele powodów, ale większość wszystkich: wzrasta ilość danych, wykonywania kopii zapasowej dziennika transakcji, przechowywanie plików śledzenia i wykonywania migawek magazynu. Dlatego jest ważne toomonitor użycie miejsca na dysku i zarządzać miejscem na dysku hello skojarzonego z jednostką wystąpienia dużych HANA hello.

## <a name="monitoring-and-troubleshooting-from-hana-side"></a>Monitorowanie i rozwiązywanie problemów z HANA strony

W kolejności tooeffectively analizować problemy pokrewne tooSAP HANA na platformie Azure (wystąpienia duże), jest przydatne toonarrow dół hello główną przyczynę problemu. SAP został opublikowany dużą ilość toohelp dokumentacji użytkownik.

Zastosowanie wydajności HANA pokrewne tooSAP — często zadawane pytania można znaleźć w powitania po SAP uwagi:

- [Uwaga SAP #2222200 — często zadawane pytania: SAP HANA sieci](https://launchpad.support.sap.com/#/notes/2222200)
- [Uwaga SAP #2100040 — często zadawane pytania: SAP HANA Procesora](https://launchpad.support.sap.com/#/notes/0002100040)
- [Uwaga SAP #199997 — często zadawane pytania: SAP HANA pamięci](https://launchpad.support.sap.com/#/notes/2177064)
- [SAP Uwaga #200000 — często zadawane pytania: Optymalizacja wydajności HANA SAP](https://launchpad.support.sap.com/#/notes/2000000)
- [Uwaga SAP #199930 — często zadawane pytania: SAP HANA we/wy analizy](https://launchpad.support.sap.com/#/notes/1999930)
- [Uwaga SAP #2177064 — często zadawane pytania: Uruchom ponownie SAP HANA usługi i awarii](https://launchpad.support.sap.com/#/notes/2177064)

**SAP HANA alertów**

Pierwszym krokiem w dzienniku hello bieżącego SAP HANA alertu. W systemie SAP HANA Studio Przejdź zbyt**konsoli administracyjnej: alerty: Pokaż: wszystkie alerty**. Na tej karcie zostaną wyświetlone wszystkie alerty SAP HANA określone wartości (wolnej pamięci fizycznej, użycie procesora CPU, itp.), które dzielą się poza hello ustawić minimalną i maksymalną progów. Domyślnie sprawdza są odświeżane automatycznie co 15 minut.

![W systemie SAP HANA Studio Przejdź tooAdministration konsoli: alerty: Pokaż: wszystkie alerty](./media/troubleshooting-monitoring/image1-show-alerts.png)

**PROCESOR CPU**

Alert wyzwolony powodu ustawienie progu tooimproper rozwiązanie jest wartość domyślną toohello tooreset lub bardziej przystępne wartość progową.

![Zresetuj wartość domyślną toohello lub bardziej przystępne wartość progowa](./media/troubleshooting-monitoring/image2-cpu-utilization.png)

powitania po alertów może wskazywać problemy zasobów Procesora:

- Użycie procesora CPU hosta (alertu 5)
- Operacja punktu zapisu najnowszych (28 alertów)
- Czas trwania punktu zapisu (54 alertów)

Można zauważyć wysokie użycie procesora CPU w Twojej bazie danych SAP HANA z jednego z następujących hello:

- Alert 5 (użycie procesora CPU hosta) jest wywoływane bieżące lub wcześniejsze użycia procesora CPU
- Hello wyświetlane użycie procesora CPU na powitania ekran Przegląd

![Wyświetlane użycie procesora CPU na powitania ekran Przegląd](./media/troubleshooting-monitoring/image3-cpu-usage.png)

w przeszłości hello Hello wykres obciążenia mogą być wyświetlane wysokie użycie procesora CPU lub wysokie zużycie:

![Wykres obciążenia Hello mogą być wyświetlane w przeszłości hello wysokie użycie procesora CPU lub wysokie zużycie](./media/troubleshooting-monitoring/image4-load-graph.png)

Alert wyzwolony powodu wykorzystania procesora CPU toohigh może być spowodowane przez kilka przyczyn, w tym między innymi: wykonanie pewnych transakcji, ładowanie danych, wysunięć zadania, długotrwałą instrukcji SQL i wydajności zapytania (na przykład z BW na HANA moduły).

Można znaleźć toohello [SAP HANA rozwiązywania problemów: pokrewne powoduje procesora CPU i rozwiązań](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4f/bc915462db406aa2fe92b708b95189/content.htm?frameset=/en/db/6ca50424714af8b370960c04ce667b/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=46&amp;show_children=false) lokacji szczegółowe kroki rozwiązywania problemów.

**System operacyjny**

Jedną z najważniejszych hello sprawdza, czy SAP HANA w systemie Linux jest toomake się upewnić, że wyłączono przezroczysty dużych stron, zobacz [&#2131662; Uwaga SAP — przezroczysty dużych stron (THP) na serwerach z SAP HANA](https://launchpad.support.sap.com/#/notes/2131662).

- Możesz sprawdzić, czy przezroczyste dużych stron są włączone za pośrednictwem hello następujące polecenia Linux: **cat /sys/kernel/mm/transparent\_hugepage lub nie włączono**
- Jeśli _zawsze_ jest ujęta w nawiasy kwadratowe zgodnie z poniższymi instrukcjami, oznacza to, czy przezroczyste dużych stron hello są włączone: [zawsze] madvise nigdy nie; Jeśli _nigdy nie_ jest ujęta w nawiasy kwadratowe zgodnie z poniższymi instrukcjami, oznacza to, że hello przezroczysty Wyłączono dużych stron: zawsze madvise [nigdy nie]

Hello następujące polecenia Linux powinien zwrócić nic: **obr. / min — odpowiedzi na pytania | grep ulimit.** Jeśli zostanie wyświetlona _ulimit_ jest zainstalowane, odinstaluj go bezpośrednio.

**Pamięci**

Można zaobserwować hello wielkość pamięci przydzielonej przez hello SAP HANA bazy danych jest większa niż oczekiwano. Witaj następujące alerty wskazują na problemy z wysokie użycie pamięci:

- Użycie pamięci fizycznej hosta (alertu 1)
- Użycie pamięci serwera nazw (12 alertów)
- Łączne użycie pamięci magazynu kolumn w tabelach (40 alertów)
- Użycie pamięci usług (43 alertów)
- Użycie pamięci magazynu głównego magazynu kolumn tabel (45 alertów)
- Pliki zrzutu środowiska uruchomieniowego (46 alertów)

Zobacz toohello [SAP HANA rozwiązywania problemów: problemy z pamięcią](http://help.sap.com/saphelp_hanaplatform/helpdata/en/db/6ca50424714af8b370960c04ce667b/content.htm?frameset=/en/59/5eaa513dde43758b51378ab3315ebb/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=26&amp;show_children=false) lokacji szczegółowe kroki rozwiązywania problemów.

**Sieć**

Odwołuje się zbyt[SAP Uwaga #2081065 — Rozwiązywanie problemów z programem SAP HANA sieci](https://launchpad.support.sap.com/#/notes/2081065) i wykonywać rozwiązywania problemów w tej uwagi SAP hello sieciowych.

1. Analizowanie czasu Rundy między serwerem a klientem.
  A. Uruchom skrypt SQL hello [ _HANA\_sieci\_klientów_](https://launchpad.support.sap.com/#/notes/1969700)_._
  
2. Przeanalizuj komunikacji między węzłami.
  A. Uruchom skrypt SQL [ _HANA\_sieci\_usług_](https://launchpad.support.sap.com/#/notes/1969700)_._

3. Uruchom polecenie Linux **ifconfig** (hello dane wyjściowe zawierają, jeśli występują strat pakietów).
4. Uruchom polecenie Linux **tcpdump**.

Należy także użyć typu open source hello [dotyczące programu Iperf;](https://iperf.fr/) narzędzia (lub podobny) wydajność sieci toomeasure rzeczywistej aplikacji.

Zobacz toohello [SAP HANA rozwiązywania problemów: wydajność sieci i występują problemy z łącznością](http://help.sap.com/saphelp_hanaplatform/helpdata/en/a3/ccdff1aedc4720acb24ed8826938b6/content.htm?frameset=/en/dc/6ff98fa36541e997e4c719a632cbd8/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=142&amp;show_children=false) lokacji szczegółowe kroki rozwiązywania problemów.

**Storage**

Z perspektywy użytkownika końcowego aplikacji (lub hello system jako całość) działa wolno, nie odpowiada lub nawet może wydawać toohang, jeśli występują problemy z wydajnością we/wy. W hello **woluminów** kartę SAP HANA Studio zawiera hello dołączone woluminy i woluminy są używane przez każdej usługi.

![Na karcie woluminów hello w SAP HANA Studio można zauważyć, że hello dołączone woluminy i woluminy są używane przez każdego usługi](./media/troubleshooting-monitoring/image5-volumes-tab-a.png)

Dołączone woluminy w dolnej części ekranu hello, które można wyświetlić szczegóły hello hello woluminów, takie jak pliki i statystyki we/wy.

![Dołączone woluminy w dolnej części ekranu hello, które można wyświetlić szczegóły hello hello woluminów, takie jak pliki i statystyki we/wy](./media/troubleshooting-monitoring/image6-volumes-tab-b.png)

Można znaleźć toohello [SAP HANA rozwiązywania problemów: We/Wy pokrewne główne przyczyny i rozwiązania](http://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/6ff98fa36541e997e4c719a632cbd8/content.htm?frameset=/en/47/4cb08a715c42fe9f7cc5efdc599959/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=55&amp;show_children=false) i [SAP HANA Rozwiązywanie problemów z: dysku pokrewne główne przyczyny i rozwiązania](http://help.sap.com/saphelp_hanaplatform/helpdata/en/47/4cb08a715c42fe9f7cc5efdc599959/content.htm?frameset=/en/44/3e1db4f73d42da859008df4f69e37a/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=53&amp;show_children=false) lokacji szczegółowe kroki rozwiązywania problemów.

**Narzędzia diagnostyczne**

Wykonaj sprawdzenie kondycji programu SAP HANA za pośrednictwem HANA\_konfiguracji\_Minichecks. To narzędzie zwraca potencjalnie krytycznych problemów technicznych, które powinny już mieć został zgłoszony jako ostrzeżenia w SAP HANA Studio.

Odwołuje się zbyt[&#1969700; Uwaga SAP — kolekcja instrukcji SQL dla SAP HANA](https://launchpad.support.sap.com/#/notes/1969700) i Pobierz hello SQL Statements.zip pliku dołączonego toothat Uwaga. Należy zapisać ten plik zip na lokalnym dysku twardym powitania.

W SAP HANA Studio na powitania **informacje o systemie** karcie, kliknij prawym przyciskiem myszy hello **nazwa** kolumny i wybierz **instrukcje SQL importu**.

![W SAP HANA Studio, na karcie informacji o systemie hello kliknij prawym przyciskiem myszy hello kolumny z nazwami, a następnie wybierz importu instrukcje SQL](./media/troubleshooting-monitoring/image7-import-statements-a.png)

Plik SQL Statements.zip SELECT hello przechowywany lokalnie, a folder z odpowiedniej instrukcji SQL hello zostaną zaimportowane. W tym momencie powitalne szereg różnych testów diagnostycznych mogą być uruchamiane z tych instrukcji SQL.

Na przykład wymagania dotyczące przepustowości replikacji systemu SAP HANA tootest, kliknij prawym przyciskiem myszy hello **przepustowości** instrukcji w obszarze **replikacji: przepustowości** i wybierz **Otwórz** w konsoli programu SQL.

pełną instrukcję SQL Hello otwiera zezwalanie toobe parametrów wejściowych (modyfikacji sekcja) zmienione, a następnie wykonać.

![zezwolenie na obecność toobe parametrów wejściowych (modyfikacji sekcja) zmienione, a następnie wykonać otwiera Hello pełną instrukcję SQL](./media/troubleshooting-monitoring/image8-import-statements-b.png)

Innym przykładem jest kliknięcie prawym przyciskiem myszy w instrukcjach hello w obszarze **replikacji: omówienie**. Wybierz **Execute** z menu kontekstowego hello:

![Innym przykładem jest kliknięcie prawym przyciskiem myszy w instrukcjach hello w ramach replikacji: omówienie. Wybierz z menu kontekstowego hello Execute](./media/troubleshooting-monitoring/image9-import-statements-c.png)

Powoduje to informacje pomocne przy rozwiązywaniu problemów:

![Spowoduje to informacje, które ułatwią rozwiązywanie problemów](./media/troubleshooting-monitoring/image10-import-statements-d.png)

Witaj takie same dla HANA\_konfiguracji\_Minichecks i zaznacz pole wyboru dla dowolnej _X_ znaczników hello _C_ kolumny (krytyczne).

Przykładowe wyniki:

**HANA\_konfiguracji\_MiniChecks\_Rev102.01 + 1** kontroli ogólne SAP HANA.

![HANA\_konfiguracji\_MiniChecks\_Rev102.01 + 1 dla ogólnych kontroli SAP HANA](./media/troubleshooting-monitoring/image11-configuration-minichecks.png)

**HANA\_usług\_omówienie** omówienie co SAP HANA usługi są aktualnie uruchomione.

![HANA\_usług\_omówienie omówienie co SAP HANA usługi są aktualnie uruchomione](./media/troubleshooting-monitoring/image12-services-overview.png)

**HANA\_usług\_statystyki** dla SAP HANA usługi informacji (CPU, pamięci, itd.).

![HANA\_usług\_statystyki dla SAP HANA informacje o usługach ](./media/troubleshooting-monitoring/image13-services-statistics.png)

**HANA\_konfiguracji\_omówienie\_Rev110 +** ogólne informacje na temat hello wystąpieniem SAP HANA.

![HANA\_konfiguracji\_omówienie\_Rev110 + ogólne informacje na temat hello SAP HANA wystąpienia](./media/troubleshooting-monitoring/image14-configuration-overview.png)

**HANA\_konfiguracji\_parametry\_Rev70 +** toocheck parametrów SAP HANA.

![HANA\_konfiguracji\_parametry\_Rev70 + toocheck SAP HANA parametrów](./media/troubleshooting-monitoring/image15-configuration-parameters.png)

