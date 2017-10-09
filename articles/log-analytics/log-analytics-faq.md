---
title: "aaaLog Analytics — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Zadawane pytania dotyczące usługi Azure Log Analytics hello toofrequently odpowiedzi."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: ad536ff7-2c60-4850-a46d-230bc9e1ab45
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: magoedte
ms.openlocfilehash: 25931f521cbb6ec840184221c6c1a5794b3445f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-faq"></a>Log Analytics — często zadawane pytania
Ta FAQ firmy Microsoft znajduje się lista często zadawane pytania dotyczące usługi Analiza dzienników w Microsoft Operations Management Suite (OMS). Jeśli masz dodatkowe pytania dotyczące analizy dzienników Przejdź toohello [forum dyskusyjne](https://social.msdn.microsoft.com/Forums/azure/home?forum=opinsights) i opublikuj swoje pytania. Po zadawane pytania możemy dodać ją toothis artykuł, aby można je znaleźć szybkie i łatwe.

## <a name="general"></a>Ogólne

### <a name="q-does-log-analytics-use-hello-same-agent-as-azure-security-center"></a>Q. Analiza dzienników używa hello samego agenta jako Centrum zabezpieczeń Azure?

A. W wczesne 2017 czerwca Centrum zabezpieczeń Azure rozpoczęło się przy użyciu programu Microsoft Monitoring Agent hello toocollect i magazynu danych. toolearn więcej, zobacz [Azure Security Center platformy migracji — często zadawane pytania](../security-center/security-center-platform-migration-faq.md).

### <a name="q-what-checks-are-performed-by-hello-ad-and-sql-assessment-solutions"></a>Q. Jakie są sprawdzane przez hello AD i rozwiązań SQL do oceny?

A. Witaj następujące zapytanie zawiera opis sprawdza wszystkie aktualnie wykonywane:

```
(Type=SQLAssessmentRecommendation OR Type=ADAssessmentRecommendation) | dedup RecommendationId | select FocusArea, ActionArea, Recommendation, Description | sort Type, FocusArea,ActionArea, Recommendation
```

Witaj wyniki następnie można wyeksportowanego tooExcel dla dalszego przeglądu.

### <a name="q-why-do-i-see-something-different-than-oms-in-system-center-operations-manager-console"></a>Pytanie: Dlaczego coś innego niż zobacz *OMS* w konsoli programu System Center Operations Manager?

Odpowiedź: w zależności od jakiego Update Rollup programu Operations Manager znajdują się na, mogą pojawić się węzeł dla *System Center Advisor*, *usługi Operational Insights*, lub *analizy dzienników*.

Witaj aktualizacji ciągu tekstowego zbyt*OMS* znajduje się w pakiecie administracyjnym, którą należy zaimportować ręcznie toobe. toosee hello bieżącego tekstu i funkcjonalność, wykonaj instrukcje hello na powitania najnowsze System Center Operations Manager aktualizacji pakiet zbiorczy KB artykułu i Odśwież hello konsoli.

### <a name="q-is-there-an-on-premises-version-of-log-analytics"></a>Pytanie: czy istnieje *lokalnymi* wersji Log Analytics?

Odpowiedź: nie. Analiza dzienników przetwarzania i przechowywania dużych ilości danych. Usługa w chmurze analizy dzienników jest możliwe tooscale w górę w razie potrzeby i uniknąć dowolnym środowisku tooyour wpływu na wydajność.

Dodatkowe korzyści:
- Microsoft uruchamia hello analizy dzienników infrastruktury, co pozwala zaoszczędzić koszty
- Regularne wdrożenie funkcją Aktualizacje i poprawki.

### <a name="q-how-do-i-troubleshoot-that-log-analytics-is-no-longer-collecting-data"></a>Q. Jak rozwiązywać analizy dzienników nie zbiera danych?

A. Jeśli znajdują się na powitania bezpłatnej warstwy cenowej i zostały wysłane więcej niż 500 MB danych w ciągu dnia, gromadzenie danych zatrzymuje hello końca dnia hello. Osiągnięcia dziennego limitu hello jest typową przyczyną, który analizy dzienników zatrzymuje zbieranie danych lub dane są wyświetlane toobe Brak.

Analiza dzienników tworzy zdarzenie typu *operacji* podczas zbierania danych uruchamiania i zatrzymywania. 

Uruchom hello następujące zapytanie w toocheck wyszukiwania osiągnięcia dziennego limitu hello, Brak danych:`Type=Operation OperationCategory="Data Collection Status"`

Kiedy gromadzenie danych zatrzymuje, hello *OperationStatus* jest **ostrzeżenie**. Podczas zbierania danych uruchamiania, hello *OperationStatus* jest **zakończyło się pomyślnie**. 

Witaj poniższej tabeli opisano przyczyn, które zatrzymania zbierania danych i kolekcji danych tooresume zalecane działanie:

| Zatrzymuje zbieranie danych z powodu                       | zbieranie danych tooresume |
| -------------------------------------------------- | ----------------  |
| Osiągnięty dzienny limit dane w warstwie bezpłatna<sup>1</sup>       | Zaczekaj na powitania dnia dla kolekcji tooautomatically ponownego uruchomienia komputera lub<br> Zmień tooa płatnej warstwy cenowej |
| Subskrypcja platformy Azure jest w stanie wstrzymania ze względu na: <br> Bezpłatna wersja próbna została zakończona <br> Ważność Azure — dostęp próbny <br> Osiągnięto limit wydatków co miesiąc (na przykład na subskrypcję MSDN lub Visual Studio)                          | Konwertuj tooa płatnej subskrypcji <br> Konwertuj tooa płatnej subskrypcji <br> Usuń limit lub poczekaj na zresetowanie limitu |

<sup>1</sup> Jeśli obszar roboczy znajduje się na powitania warstwy cenowej bezpłatna, użytkownik musi tylko toosending 500 MB danych na dzień toohello usługi. Po osiągnięciu hello dzienny limit zbierania danych zatrzymuje się dopiero hello następnego dnia. Dane wysyłane podczas zatrzymania zbierania danych nie jest indeksowana i nie jest dostępny do wyszukiwania. Po wznowieniu pracy zbierania danych, przetwarzanie odbywa się tylko w przypadku nowych danych wysyłane. 

Analiza dzienników używa czas UTC i uruchamia każdego dnia o północy czasu UTC. Jeśli roboczym hello osiągnie limit dzienny hello, przetwarzania wznawia podczas hello pierwszej godziny hello następnego dnia UTC.

### <a name="q-how-can-i-be-notified-when-data-collection-stops"></a>Q. Jak można zostanie wyświetlone powiadomienie po zatrzymaniu zbierania danych?

Odpowiedź: Użyj hello opisane w [Tworzenie reguły alertu](log-analytics-alerts-creating.md#create-an-alert-rule) toobe powiadomienie po zatrzymaniu zbierania danych.

Podczas tworzenia alertu hello momentu zatrzymania zbierania danych należy skonfigurować:
- **Nazwa** zbyt*zatrzymać zbieranie danych*
- **Ważność** zbyt*ostrzeżenie*
- **Zapytania wyszukiwania** zbyt`Type=Operation OperationCategory="Data Collection Status" OperationStatus=Warning`
- **Przedział czasu** za*2 godziny*.
- **Alert częstotliwości** toobe jedną godzinę, ponieważ dane użycia hello aktualizację tylko raz na godzinę.
- **Generuj alert, na podstawie** toobe *liczba wyników*
- **Liczba wyników** toobe *większa niż 0*

Użyj hello procedury opisanej w [dodać reguły tooalert akcje](log-analytics-alerts-actions.md) konfigurowanie poczty e-mail, webhook lub runbook akcji hello reguły alertów.


## <a name="configuration"></a>Konfiguracja
### <a name="q-can-i-change-hello-name-of-hello-tableblob-container-used-tooread-from-azure-diagnostics-wad"></a>Q. Można zmienić nazwę hello hello tabeli/obiektów blob kontenera używane tooread z diagnostyki Azure (WAD)?

A. Nie, nie jest obecnie możliwe tooread z dowolnego tabel lub kontenerów w magazynie Azure.

### <a name="q-what-ip-addresses-does-hello-log-analytics-service-use-how-do-i-ensure-that-my-firewall-only-allows-traffic-toohello-log-analytics-service"></a>Q. Adresy IP hello analizy dzienników użycia usługi? Jak zapewnić, że moje zapora zezwala na tylko ruch toohello analizy dzienników usługi?

A. Hello usługi analizy dzienników jest oparty na platformie Azure. Adresy IP analizy dziennika znajdują się w hello [zakresów IP centrum danych Microsoft Azure](http://www.microsoft.com/download/details.aspx?id=41653).

Wdrożenia usługi zostały wprowadzone, zmienić hello rzeczywiste adresy IP hello usługi analizy dzienników. tooallow nazwy DNS Hello za pośrednictwem zapory są udokumentowane w [skonfigurować ustawienia serwera proxy i zapory w analizy dzienników](log-analytics-proxy-firewall.md).

### <a name="q-i-use-expressroute-for-connecting-tooazure-does-my-log-analytics-traffic-use-my-expressroute-connection"></a>Q. ExpressRoute można używać do łączenia tooAzure. Moje analizy dzienników ruchu używa połączenie ExpressRoute?

A. różne rodzaje ruchu ExpressRoute Hello są opisane w hello [dokumentacja usługi ExpressRoute](../expressroute/expressroute-faqs.md#supported-services).

Ruch tooLog Analytics używa hello publicznej komunikacji równorzędnej ExpressRoute obwodu.

### <a name="q-is-there-a-simple-and-easy-way-toomove-an-existing-log-analytics-workspace-tooanother-log-analytics-workspaceazure-subscription"></a>Q. Istnieje już toomove prosty i łatwy sposób istniejący obszar roboczy analizy dzienników tooanother subskrypcji Azure/obszaru roboczego analizy dzienników?

A. Witaj `Move-AzureRmResource` polecenie cmdlet umożliwia przenoszenie obszaru roboczego analizy dzienników, a konto usługi Automatyzacja z jednego tooanother subskrypcji platformy Azure. Aby uzyskać więcej informacji, zobacz [Move AzureRmResource](http://msdn.microsoft.com/library/mt652516.aspx).

Ta zmiana może również w hello portalu Azure.

Nie można przenieść dane z jednego tooanother obszaru roboczego analizy dzienników, lub zmień region hello analizy dzienników dane są przechowywane w.

### <a name="q-how-do-i-add-log-analytics-toosystem-center-operations-manager"></a>Pytanie: jak dodać dziennika analizy tooSystem Center Operations Manager?

Odpowiedź: aktualizowanie toohello najnowszego pakietu zbiorczego aktualizacji i importowanie pakietów administracyjnych umożliwia tooconnect programu Operations Manager tooLog Analytics.

>[!NOTE]
>tooLog połączenie programu Operations Manager Hello Analytics jest dostępna tylko dla programu System Center Operations Manager 2012 z dodatkiem SP1 i nowszych.

### <a name="q-how-can-i-confirm-that-an-agent-is-able-toocommunicate-with-log-analytics"></a>Pytanie: jak można potwierdzić, że agent jest możliwe toocommunicate z analizy dzienników?

A: tooensure hello agent może komunikować się z OMS, przejdź do: Panel sterowania, zabezpieczeń i ustawień, **programu Microsoft Monitoring Agent**.

W obszarze hello **Analiza dzienników Azure (OMS)** karcie, poszukaj zielony znacznik wyboru. Ikona z zielonym znacznikiem wyboru potwierdza, że hello agent jest możliwe toocommunicate z hello usługę.

Żółta ikona ostrzeżenia oznacza, że hello agent występują problemy dotyczące komunikacji z usługą OMS. Najczęściej zdarza się to hello usługi Microsoft Monitoring Agent została zatrzymana. Korzystanie z usługi kontroli Menedżer toorestart hello usługi.

### <a name="q-how-do-i-stop-an-agent-from-communicating-with-log-analytics"></a>Pytanie: jak zatrzymać agenta komunikację z Log Analytics?

A: w programie System Center Operations Manager, Usuń komputer hello z listy komputerów zarządzanych Advisor hello. Aktualizacje programu Operations Manager hello konfiguracji hello agenta toono dłużej raport tooLog Analytics. Dla agentów bezpośrednio połączonych tooLog Analytics, można zatrzymać ich komunikację za pośrednictwem: Panel sterowania, zabezpieczeń i ustawień, **programu Microsoft Monitoring Agent**.
W obszarze **Analiza dzienników Azure (OMS)**, Usuń wszystkie obszary robocze wymienione.

### <a name="q-why-am-i-getting-an-error-when-i-try-toomove-my-workspace-from-one-azure-subscription-tooanother"></a>Pytanie: Dlaczego otrzymuję błąd przy próbie toomove Mój obszar roboczy z jedną subskrypcją platformy Azure tooanother?

A. Jeśli używasz hello portalu Azure, upewnij się, że tylko hello obszaru roboczego został wybrany do przeniesienia hello. Nie wybieraj rozwiązania hello — zostanie automatycznie przełączona po przesunięciu hello obszaru roboczego. 

Upewnij się, że masz uprawnienia w obu subskrypcji platformy Azure.

## <a name="agent-data"></a>Dane agenta
### <a name="q-how-much-data-can-i-send-through-hello-agent-toolog-analytics-is-there-a-maximum-amount-of-data-per-customer"></a>Q. Ilość danych może wysłać za pośrednictwem hello agenta tooLog Analytics? Istnieje już maksymalna ilość danych klienta?
A. planu free Hello Ustawia dzienny limit 500 MB na obszar roboczy. Hello standardowa i premium planów nie nie limity, na powitania ilość danych, który jest przekazany. Jako usługa w chmurze jest przeznaczony Analytics dziennika skali tooautomatically objętości hello toohandle pochodzące z klientem — nawet jeśli jest ona terabajtów na dzień.

Hello analizy dzienników agenta została zaprojektowana tooensure ma mało miejsca. Jednym z naszych klientów zapisano blog o hello testów, które są wykonane względem naszego agenta i jak wrażeniem były. ilość danych Hello w zależności od rozwiązania hello, które można włączyć. Możesz znaleźć szczegółowe informacje na temat hello ilość danych i rozpad hello przez rozwiązanie w hello [użycia](log-analytics-usage.md) strony.

Aby uzyskać więcej informacji można znaleźć [blogu klienta](http://thoughtsonopsmgr.blogspot.com/2015/09/one-small-footprint-for-server-one.html) o hello niewielki rozmiar hello agenta pakietu OMS.

### <a name="q-how-much-network-bandwidth-is-used-by-hello-microsoft-management-agent-mma-when-sending-data-toolog-analytics"></a>Q. Jaka przepustowość sieci jest używany przez hello Microsoft Management Agent (MMA) podczas wysyłania danych tooLog Analytics?

A. Przepustowość jest funkcja na powitania ilość danych przesyłanych. Dane są kompresowane podczas ich przesyłania przez sieć hello.

### <a name="q-how-much-data-is-sent-per-agent"></a>Q. Ilość danych są wysyłane na agenta?

A. Witaj ilość danych przesyłanych na agenta jest zależna od:

* Hello rozwiązania, które aktywowano
* Liczba Hello dzienniki i liczniki wydajności są zbierane
* Witaj ilość danych w dziennikach hello

Hello bezpłatnej warstwy cenowej jest tooonboard dobrze kilka serwerów i mierników hello typowych danych woluminu. Ogólne użycie jest wyświetlany na powitania [użycia](log-analytics-usage.md) strony.

Dla komputerów, które są możliwe toorun hello WireData agenta należy użyć hello toosee zapytania, ile dane są wysyłane następujące:

```
Type=WireData (ProcessName="C:\\Program Files\\Microsoft Monitoring Agent\\Agent\\MonitoringHost.exe") (Direction=Outbound) | measure Sum(TotalBytes) by Computer
```



## <a name="next-steps"></a>Następne kroki
* [Wprowadzenie do analizy dzienników](log-analytics-get-started.md) toolearn więcej informacji na temat analizy dzienników i get do pracy w minutach.
