---
title: "monitorowanie porównanie produktów aaaMicrosoft | Dokumentacja firmy Microsoft"
description: "Microsoft Operations Management Suite (OMS) to rozwiązanie do zarządzania IT, które pomaga zarządzać i chronić lokalnej i w chmurze infrastruktury opartej na chmurze firmy Microsoft.  W tym artykule identyfikuje hello różnych usług objęte OMS i linki tootheir szczegółowe zawartości."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: a63ca0ad-61f8-425d-a48c-d87ba518c104
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/27/2016
ms.author: bwren
ms.openlocfilehash: 61144a298fe73c35181070d552c41b96fc445097
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-monitoring-product-comparison"></a>Monitorowania porównanie produktów firmy Microsoft
W tym artykule przedstawiono porównanie programu System Center Operations Manager (SCOM) i analizy dzienników w Operations Management Suite (OMS) pod względem ich architektury, logiki hello jak monitorować ich zasobów i sposób ich analiza danych hello one Zbieraj.  Jest to toogive możesz podstawowych zrozumienie ich różnice i siły względnej.  

## <a name="basic-architecture"></a>Podstawowa architektura
### <a name="system-center-operations-manager"></a>System Center Operations Manager
Wszystkie składniki programu SCOM są zainstalowane w centrum danych.  [Agenci są zainstalowani](http://technet.microsoft.com/library/hh551142.aspx) na maszynach z systemem Windows i Linux, które są zarządzane przez SCOM.  Agenci połączyć za[serwerów zarządzania](https://technet.microsoft.com/library/hh301922.aspx) który komunikacji z magazynem danych i bazy danych SCOM hello.  Agenci są zależne od serwerów toomanagement tooconnect uwierzytelniania domeny.  Poza zaufanej domeny można uwierzytelniania certyfikatów lub połączyć tooa [serwera bramy](https://technet.microsoft.com/library/hh212823.aspx).

SCOM wymaga dwóch baz danych, dla danych operacyjnych i innym danych magazynu toosupport raportowanie i analiza danych.  A [Reporting Server](https://technet.microsoft.com/library/hh298611.aspx) uruchamia tooreport usług SQL Reporting Services na danych z magazynu danych hello. 

SCOM można monitorować zasobów w chmurze przy użyciu pakietów administracyjnych dla produktów takich jak [Azure](https://www.microsoft.com/download/details.aspx?id=38414), [usługi Office 365](https://www.microsoft.com/download/details.aspx?id=43708), i [usług AWS](http://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/AWSManagementPack.html).  Te pakiety administracyjne, użyj jednej lub więcej agentów lokalnych jako serwery proxy do odnajdywania w chmurze zasobów i uruchomione przepływy pracy toomeasure ich wydajności i dostępności.  Agenci proxy są używane również zbyt[monitorować urządzenia sieciowe](https://technet.microsoft.com/library/hh212935.aspx) i innych zasobów zewnętrznych.

Witaj konsoli operacje jest aplikacji systemu Windows, który jest podłączany tooone hello serwerów zarządzania i umożliwia tooview administratora hello i analizować dane zbierane i konfigurowania środowiska SCOM hello.  Konsola sieci web może znajdować się na dowolnym serwerze usług IIS i zapewnia analizy danych za pośrednictwem przeglądarki.

![Architektura programu SCOM](media/operations-management-suite-monitoring-product-comparison/scom-architecture.png)

### <a name="log-analytics"></a>Log Analytics
Większość składników pakietu OMS znajdują się w hello chmury Azure, aby można było wdrożyć i zarządzania nim za pomocą minimalne kosztów i prac administracyjnych związanych.  Wszystkie dane zebrane przez analizy dzienników są przechowywane w hello OMS repozytorium.

Analiza dzienników może zbierać dane z jednego z trzech źródeł:

* Fizycznych i maszyn wirtualnych z systemem Windows hello [Microsoft Monitoring Agent (MMA)](https://technet.microsoft.com/library/mt484108.aspx) lub Linux, jak i hello [Operations Management Suite agenta dla systemu Linux](https://technet.microsoft.com/library/mt622052.aspx).  Te maszyny można lokalnymi lub maszyn wirtualnych w Azure lub innej chmurze.
* Konto magazynu Azure z [diagnostyki Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) dane zebrane przez roli procesu roboczego platformy Azure, roli sieci web lub maszyny wirtualnej.
* [Grupy zarządzania SCOM tooa połączenia](https://technet.microsoft.com/library/mt484104.aspx).  W tej konfiguracji agentów hello komunikują się z serwerami zarządzania programu SCOM, które dostarczają hello danych toohello SCOM w bazie danych, gdzie następnie jest dostarczany toohello OMS danych magazynu.
  Administratorzy analizowanie zebranych danych i konfigurowanie analizy dzienników przy użyciu portalu OMS hello, która jest hostowana na platformie Azure i są dostępne z dowolnej przeglądarki.  Aplikacje mobilne tooaccess te dane są dostępne dla platform standardowe hello.

![Architektura analizy dzienników](media/operations-management-suite-monitoring-product-comparison/log-analytics-architecture.png)

### <a name="integrating-scom-and-log-analytics"></a>Integrowanie programu SCOM i analizy dzienników
Kiedy SCOM jest używany jako źródło danych do analizy dzienników można korzystać z funkcji hello obu produktów w hybrydowego monitorowania środowiska.  Można skonfigurować istniejącą agentów SCOM za pośrednictwem toobe konsoli operacje hello zarządza OMS, ponadto pakiety administracyjne toorun toocontinuing z programu SCOM.  
Dane z podłączonej grupy zarządzania SCOM są dostarczane tooLog Analytics przy użyciu jednej z czterech metod:

* Zdarzenia i dane wydajności są zbierane przez agenta hello i dostarczyć tooSCOM.  Serwery zarządzania w SCOM dostarcza hello danych tooLog Analytics.
* Niektóre zdarzenia, takie jak dzienniki programu IIS i zdarzenia zabezpieczeń kontynuować toobe dostarczone bezpośrednio tooLog Analytics z hello agenta.
* Rozwiązania będzie dostarczać dodatkowe oprogramowanie agenta toohello lub wymagają oprogramowania zainstalowanych toocollect dodatkowe dane.  Te dane będą zwykle wysyłane bezpośrednio tooLog Analytics.
* Niektóre rozwiązania będzie zbierać dane bezpośrednio z serwerów zarządzania programu SCOM, które nie pochodzą z agenta hello.  Na przykład Witaj [rozwiązania zarządzania alertami](https://technet.microsoft.com/library/mt484092.aspx) gromadzi alerty z programu SCOM, po ich utworzeniu.

## <a name="monitoring-logic"></a>Logika monitorowania
SCOM i analizy dzienników współpracować z podobne dane zbierane przez agentów, ale mają podstawowe różnice w sposób definiowania i wdrożyć ich logikę zbierania danych i sposobu ich analizowania hello zbieranych danych.

### <a name="operations-manager"></a>Operations Manager
Logika monitorowania dla programu SCOM jest zaimplementowana w [pakietów administracyjnych](https://technet.microsoft.com/library/hh457558.aspx) zawierających logikę wykrywania toomonitor składników, pomiaru kondycji hello tych składników i zbierania danych tooanalyze.  Dane monitorowania może być prosty jak zbieranie licznik zdarzeń lub wydajności lub można użyć złożonej logiki zaimplementowana w skrypcie.  Pakiety administracyjne, które obejmują pełne monitorowania są dostępne dla różnych [aplikacji firmy Microsoft i innych firm](http://go.microsoft.com/fwlink/?LinkId=82105) dodanie urządzenia toohardware i sieci.  Możesz [tworzenie własnych pakietów administracyjnych](http://aka.ms/mpauthor) dla niestandardowych aplikacji.

Pakiety administracyjne zawierają wiele przepływów pracy pełniących niektórych odrębne funkcje monitorowania takich jak próbkowania licznika wydajności, sprawdzanie stanu usługi hello lub uruchamianie skryptu.  Każdy przepływ pracy działa niezależnie i definiuje własną wyników, takie jak bazy danych będą zapisywane tooand czy wygeneruje alert. 

Szczegółowe informacje o przepływie pracy, takich jak hello częstotliwości działają, próg hello których uznają błąd oraz hello ważność alertu hello, które generują można zastąpić.  Można też podać dodatkowe funkcje, dodając własne przepływów pracy.

![Zastąpienia](media/operations-management-suite-monitoring-product-comparison/scom-overrides.png)

Pakiety administracyjne są zainstalowane w bazie danych programu Operations Manager hello i automatycznie dystrybuowana tooagents serwerów zarządzania.  Każdy agent zostanie automatycznie pobrać pakietów administracyjnych i obciążenia aplikacji toohello odpowiednich przepływy pracy, zainstalowanych.  Dane zebrane przez agenta hello jest dostarczane toohello zapasowego serwera zarządzania do wstawienia do hello SCOM bazy danych i magazynu danych.  Hello konsoli operacje można tooview i analizować te dane przy użyciu niestandardowych widoków, pulpity nawigacyjne i raporty zawarte w pakiecie administracyjnym hello.

powitania po diagram przedstawia Hello dystrybucji pakietów administracyjnych.

![Przepływ pakiet zarządzania](media/operations-management-suite-monitoring-product-comparison/scom-mpflow.png)

### <a name="log-analytics"></a>Log Analytics
#### <a name="event-and-performance-collection"></a>Zdarzenia i zbieranie danych wydajności
Analiza dzienników gromadzi zdarzenia i liczniki wydajności z systemów agenta przy użyciu źródeł, takich jak dziennika zdarzeń systemu Windows, dzienniki programu IIS i Syslog.  Można określić kryteria, dla których dane są zbierane za pomocą portalu usługi Analiza dzienników hello, a następnie utwórz dziennika zapytań tooanalyze hello zebranych danych.  Standardowe kryteria określone jest definiowany podczas tworzenia obszaru roboczego OMS i można zdefiniować dodatkowe dane dla określonej aplikacji. 

![Definiowanie dzienników zdarzeń w analizy dzienników](media/operations-management-suite-monitoring-product-comparison/log-analytics-definedata.png)

Kiedy SCOM ma wiele szczegółowe przepływów pracy, które zazwyczaj określić kryteria dla danych i hello akcji, która powinna być wykonywana w odpowiedzi, Log Analytics ma bardziej ogólne kryteria zbierania danych.  Dziennika zapytań i rozwiązań zapewnia bardziej docelowe kryteria do analizowania i działające na określonych danych w chmurze powitania po zostały zebrane.

#### <a name="solutions"></a>Rozwiązania
Rozwiązań zapewnia dodatkową logikę do zbierania danych i analiz.  Można wybrać rozwiązań tooadd tooyour OMS subskrypcji z hello galerii rozwiązań.

![Galeria rozwiązań](media/operations-management-suite-monitoring-product-comparison/log-analytics-solutiongallery.png)

Rozwiązania głównie uruchomienia w chmurze hello, umożliwiając analizę zdarzenia i liczniki wydajności zebrane w repozytorium OMS hello.  Mogą również określić toobe dodatkowe dane zbierane z zapytaniami dziennika lub przy użyciu interfejsu użytkownika dodatkowe podane przez rozwiązanie hello na pulpicie nawigacyjnym OMS hello umożliwia analizowanie. 

Na przykład Witaj [śledzenia zmian rozwiązania](https://technet.microsoft.com/library/mt484099.aspx) wykrywa konfiguracji zmiany w systemach agenta i zapisuje zdarzenia toohello OMS repozytorium, które mogą być analizowane za pomocą kilku graficznego widoki, które zawierają podsumowanie wykrył zmiany.  Możesz można przejść z widoku podsumowania hello do dziennika zapytań tego hello wyświetlania szczegółowych danych zbieranych przez hello rozwiązania.

Podczas zaznaczania rozwiązania Dodaj subskrypcję tooyour, nie masz aktualnie toocreate możliwości hello własnych rozwiązań.  Można wybrać hello zdarzenia i toocollect liczniki wydajności i tworzenie niestandardowych widoków opartych na kwerendach dziennika.

Logika monitorowania dla analizy dzienników Hello znajduje się w powitania po diagramu.

![Przepływ rozwiązania analizy dzienników](media/operations-management-suite-monitoring-product-comparison/log-analytics-solution-flow.png)

## <a name="health-monitoring"></a>Monitorowanie kondycji
### <a name="operations-manager"></a>Operations Manager
SCOM można modelu hello różne składniki aplikacji i zapewniają kondycji w czasie rzeczywistym dla każdego.  Dzięki temu można toonot tylko wyświetlić wykryto błędów i wydajności w czasie, ale również toovalidate hello rzeczywiste kondycji aplikacji lub systemu i wszystkich jego składników w danym momencie.  Ponieważ sam hello okresów, które aplikacja jest dostępna, aparat kondycji hello w SCOM obsługuje również poziomu usług umów (SLA), którego analiza i raport o dostępności hello aplikacji wraz z upływem czasu.

Na przykład hello ilustracja przedstawia kondycję w czasie rzeczywistym hello monitorowane przez SCOM aparatów bazy danych SQL.  Witaj kondycję wszystkich baz danych powitania dla jednej z baz danych hello przedstawiono na dole hello połowy hello widoku.

![Widok stanu](media/operations-management-suite-monitoring-product-comparison/scom-state-view.png)

Witaj Eksploratora kondycji dla jednej z baz danych hello poniżej przedstawiono hello monitory, które są używane toodetermine jego ogólna kondycja.  Te monitory są zdefiniowane w hello pakiet administracyjny SQL i uruchomienia aparatów bazy danych SQL wszystkie odnalezione przez SCOM.

![Eksplorator kondycji](media/operations-management-suite-monitoring-product-comparison/scom-health-explorer.png)

Składników w wielu systemach mogą być połączone toomeasure hello kondycji aplikacji rozproszonej.  Może to być szczególnie przydatne w przypadku aplikacji LOB, obejmujących wiele składników rozproszonych.  Można utworzyć modelu, który mierzy kondycję każdego składnika hello czy pakiet zbiorczy aktualizacji do dostępności dla aplikacji hello.

Usługa Active Directory jest przykładem jeden pakiet administracyjny, który udostępnia tooanalyze modelu jego składników rozproszonych.  Witaj przykładowy diagram poniżej przedstawia kondycję hello hello ogólnej środowiska i hello relacji między lasami, domenami i kontrolerów domeny.  Każdy z tych składników zawiera podskładniki i wiele monitorów podobny przykład SQL toohello powyżej.

![Widok diagramu programu SCOM](media/operations-management-suite-monitoring-product-comparison/scom-diagram-view.png)

### <a name="log-analytics"></a>Log Analytics
OMS nie zawiera typowe aplikacje toomodel aparat lub miary, ich kondycję w czasie rzeczywistym.  Poszczególne rozwiązania może ocenić hello ogólnej kondycji określonej usługi na podstawie zebranych danych i może instalacji niestandardowej logiki na powitania agenta tooperform w czasie rzeczywistym analizy.  Ponieważ uruchamiania rozwiązań w chmurze hello z repozytorium OMS toohello dostępu, często zapewniają dokładniejszej analizy nie jest zazwyczaj wykonywane przez pakiety administracyjne. 

Na przykład Witaj [oceny usługi AD i oceny SQL rozwiązania](https://technet.microsoft.com/library/mt484102.aspx) analizowanie zebranych danych i podaj klasyfikacji dla różnych aspektów hello środowiska.  Zawiera zalecenia dotyczące ulepszeń, które można podjąć tooimprove hello dostępności i wydajności środowiska hello.

![Rozwiązanie do oceny usługi AD](media/operations-management-suite-monitoring-product-comparison/log-analytics-ad-assessment.png)

## <a name="data-analysis"></a>Analiza danych
SCOM, jak i analizy dzienników zapewniają różne funkcje tooanalyze zebrane dane.  Widoki i pulpity nawigacyjne w konsoli operacje hello SCOM ma do analizowania ostatnich danych w różnych formatach i raportów, prezentacji danych z magazynu danych hello w formie tabelarycznej.  Analiza dzienników zapewnia pełny dziennik język zapytań i interfejsu analizowania danych w repozytorium OMS hello.  Gdy SCOM jest używany jako źródło danych analizy dzienników, hello repozytorium zawiera dane zebrane przez SCOM tak narzędzia analizy dzienników hello mogą być używane tooanalyze dane z tymi dwoma systemami.

### <a name="operations-manager"></a>Operations Manager
#### <a name="views"></a>Widoki
Widoki w konsoli operacje hello Zezwalaj tooview różne typy danych zebranych przez SCOM w różnych formatach, zwykle tabelarycznych dla zdarzeń, alertów, dane o stanie i wykresy wiersza danych wydajności.  Widoki wykonywania analizy minimalnego lub konsolidacji danych hello, ale pozwala toofilter zgodnie z kryteriami tooparticular. 

![Widoki](media/operations-management-suite-monitoring-product-comparison/scom-views.png)

Pakiety administracyjne zwykle zawierają wiele widoków obsługi aplikacji hello lub systemu, którą monitoruje.  To może obejmować widoki stanu dla hello różnych obiektów, które hello pakiet administracyjny umożliwia odnajdywanie, alertów, widoków wykrytych problemów i widokach wydajności dla liczników.

Widoki są szczególnie przydatny w przypadku analizowania hello bieżący stan środowiska hello, w tym otwartych alertów i stan kondycji hello monitorowanych systemów i obiektów.  Można przeprowadzić drążenie danych zdarzeń lub wydajności toodetailed obsługi danego alertu w kolejności toodiagnose jego główną przyczynę. Podobnie można wyświetlić hello wydajności i kondycji poszczególnych składników aplikacji tooassess jego bieżącą kondycję.

#### <a name="dashboards"></a>Pulpity nawigacyjne
Pulpity nawigacyjne w hello konsoli operacje głównie pracować z hello tych samych danych, zgodnie z widoków, ale więcej można dostosowywać i może zawierać wizualizacje bardziej zaawansowane funkcje.  Zbiór standardowych pulpity nawigacyjne są dostępne, że można łatwo dostosować do własnych celów.  Umożliwia także widget programu PowerShell, który można wyświetlić dane zwrócone w wyniku zapytania programu PowerShell.

![Pulpit nawigacyjny](media/operations-management-suite-monitoring-product-comparison/scom-dashboard.png)

Deweloperzy mają hello możliwości tooadd niestandardowych składników toodashboards, które są umieszczane w pakietach administracyjnych, ich.  Mogą to być specjalistyczny tooa określonej aplikacji, takich jak pulpit nawigacyjny hello w hello pakiet administracyjny SQL pokazano poniżej.  Ten pulpit nawigacyjny mogą służyć jako szablon dla wersji niestandardowych.

![Pulpit nawigacyjny SQL](media/operations-management-suite-monitoring-product-comparison/scom-sql-dashboard.png)

#### <a name="reports"></a>Raporty
Raportów w programie SCOM analizowania danych z magazynu danych hello w formie tabelarycznej.  Mogą być drukowane i zaplanowane w celu automatycznego dostarczania w różnych formatach plików tym PDF, CSV i Word.  Raporty pracować z danymi z magazynu danych hello, tak, aby były szczególnie odpowiednie do analizy trendów w perspektywie długoterminowej.

Pakiety administracyjne zwykle zapewni niestandardowych raportów dla określonej aplikacji.  Możesz również wybrać z biblioteki raportów ogólnych, które można dostosować do własnych aplikacji lub do wykonywania analizy ad hoc.

Poniżej przedstawiono przykładowy raport wydajności, dane zebrane przez hello pakietu administracyjnego usługi Active Directory są wyświetlane.

![Raport](media/operations-management-suite-monitoring-product-comparison/scom-report.png)

### <a name="log-analytics"></a>Log Analytics
Analiza dzienników ma [języka zapytań](https://technet.microsoft.com/library/mt484120.aspx) służącego analizy tooperform przez dane z wielu aplikacji bez toocreate potrzeby hello widok niestandardowy lub raportu.  Ponieważ OMS jest wdrażane w chmurze hello, wydajność zapytań i analizy danych nie są ograniczenia sprzętowe tooany podmiotu i może szybko analizować kwerend w tym miliony rekordów. 

Zapytania w analizy dzienników są również hello podstawę innych funkcji.  Możesz zapisać kwerendę, wyeksportować jego tooExcel wyników lub go uruchomić w regularnych odstępach czasu i automatycznie Wygeneruj alerty, gdy jego wyników spełniających kryteria określonego.  

![Dziennik zapytań przepływu](media/operations-management-suite-monitoring-product-comparison/log-analytics-query-flow.png)

Poniżej znajduje się przykład kwerendy analizy dzienników.  W tym przykładzie wszystkie zdarzenia z "uruchomiona" w nazwie hello są zwracane i grupować zdarzenia identyfikatora.  Hello użytkownika zawiera po prostu hello zapytania i analizy dzienników dynamicznie generuje hello użytkowników interface tooperform hello analizy.  Wybranie dowolnego elementu na liście hello zwróci hello szczegółowe dane zdarzenia.

![Dziennik zapytań](media/operations-management-suite-monitoring-product-comparison/log-analytics-query.png)

Ponadto tooproviding analizy ad hoc, zapytania w analizy dzienników można zapisać do użytku w przyszłości, a także dodano tooyour [pulpitu nawigacyjnego OMS](http://technet.microsoft.com/library/mt484090.aspx) pokazane na powitania poniższy przykład.

![Pulpit nawigacyjny OMS](media/operations-management-suite-monitoring-product-comparison/log-analytics-dashboard.png)

## <a name="next-steps"></a>Następne kroki
* Wdrażanie [programu System Center Operations Manager (SCOM)](https://technet.microsoft.com/library/hh205987.aspx).
* Zaloguj się do [analizy dzienników](https://azure.microsoft.com/documentation/services/log-analytics).  

