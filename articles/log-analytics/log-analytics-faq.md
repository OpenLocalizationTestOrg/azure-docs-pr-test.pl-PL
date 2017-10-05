---
title: "Zaloguj się Analytics — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Odpowiedzi na często zadawane pytania dotyczące usługi Analiza dzienników Azure."
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
ms.openlocfilehash: 8ddea06b1a90e9b1599466ad4d1c3af7a6dc8ba9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="log-analytics-faq"></a>Log Analytics — często zadawane pytania
Ta FAQ firmy Microsoft znajduje się lista często zadawane pytania dotyczące usługi Analiza dzienników w Microsoft Operations Management Suite (OMS). Jeśli masz dodatkowe pytania dotyczące analizy dzienników, przejdź do [forum dyskusyjne](https://social.msdn.microsoft.com/Forums/azure/home?forum=opinsights) i opublikuj swoje pytania. Po zadawane pytania możemy dodać ją do tego artykułu, aby można je znaleźć szybkie i łatwe.

## <a name="general"></a>Ogólne

### <a name="q-does-log-analytics-use-the-same-agent-as-azure-security-center"></a>Q. Analiza dzienników używa tego samego agenta jako Centrum zabezpieczeń Azure?

A. W wczesne 2017 czerwca Centrum zabezpieczeń Azure rozpoczęło się przy użyciu programu Microsoft Monitoring Agent do gromadzenia i przechowywania danych. Aby dowiedzieć się więcej, zobacz [Azure Security Center platformy migracji — często zadawane pytania](../security-center/security-center-platform-migration-faq.md).

### <a name="q-what-checks-are-performed-by-the-ad-and-sql-assessment-solutions"></a>Q. Jakie są sprawdzane przez usługi AD i rozwiązań SQL do oceny?

A. Następujące zapytanie zawiera opis sprawdza wszystkie aktualnie wykonywane:

```
(Type=SQLAssessmentRecommendation OR Type=ADAssessmentRecommendation) | dedup RecommendationId | select FocusArea, ActionArea, Recommendation, Description | sort Type, FocusArea,ActionArea, Recommendation
```

Wyniki można wyeksportować do programu Excel dla dalszego przeglądu.

### <a name="q-why-do-i-see-something-different-than-oms-in-system-center-operations-manager-console"></a>Pytanie: Dlaczego coś innego niż zobacz *OMS* w konsoli programu System Center Operations Manager?

Odpowiedź: w zależności od jakiego Update Rollup programu Operations Manager znajdują się na, mogą pojawić się węzeł dla *System Center Advisor*, *usługi Operational Insights*, lub *analizy dzienników*.

Aktualizacja ciągu tekstowego *OMS* znajduje się w pakiecie administracyjnym, należy zaimportować ręcznie. Aby wyświetlić bieżący tekst i funkcje, postępuj zgodnie z instrukcjami w artykule najnowsze System Center Operations Manager aktualizacji pakiet zbiorczy KB i Odśwież konsolę.

### <a name="q-is-there-an-on-premises-version-of-log-analytics"></a>Pytanie: czy istnieje *lokalnymi* wersji Log Analytics?

Odpowiedź: nie. Analiza dzienników przetwarzania i przechowywania dużych ilości danych. Usługa w chmurze analizy dzienników jest możliwość skalowania w górę w razie potrzeby i uniknięcia wpływu wydajności dla danego środowiska.

Dodatkowe korzyści:
- Microsoft uruchamia infrastruktury analizy dzienników, co pozwala zaoszczędzić koszty
- Regularne wdrożenie funkcją Aktualizacje i poprawki.

### <a name="q-how-do-i-troubleshoot-that-log-analytics-is-no-longer-collecting-data"></a>Q. Jak rozwiązywać analizy dzienników nie zbiera danych?

A. Jeśli są na wolnych warstwy cenowej i zostały wysłane więcej niż 500 MB danych w ciągu dnia, gromadzenie danych zatrzymuje się do końca dnia. Osiągnięcia dziennego limitu jest typową przyczyną analizy dzienników zatrzymuje zbieranie danych lub dane są prawdopodobnie brakuje.

Analiza dzienników tworzy zdarzenie typu *operacji* podczas zbierania danych uruchamiania i zatrzymywania. 

W polu wyszukiwania, aby sprawdzić, czy osiągnięcia dziennego limitu i brakujące dane, należy uruchomić następujące zapytanie:`Type=Operation OperationCategory="Data Collection Status"`

Po zatrzymaniu zbierania danych *OperationStatus* jest **ostrzeżenie**. Podczas uruchamiania zbierania danych, *OperationStatus* jest **zakończyło się pomyślnie**. 

W poniższej tabeli opisano przyczyn, które zatrzymania zbierania danych i zalecaną akcję umożliwiającą wznowienie zbierania danych:

| Zatrzymuje zbieranie danych z powodu                       | Wznowienie zbierania danych |
| -------------------------------------------------- | ----------------  |
| Osiągnięty dzienny limit dane w warstwie bezpłatna<sup>1</sup>       | Zaczekaj do następnego dnia dla kolekcji do automatycznego ponownego uruchamiania lub<br> Zmień na płatną warstwy cenowej |
| Subskrypcja platformy Azure jest w stanie wstrzymania ze względu na: <br> Bezpłatna wersja próbna została zakończona <br> Ważność Azure — dostęp próbny <br> Osiągnięto limit wydatków co miesiąc (na przykład na subskrypcję MSDN lub Visual Studio)                          | Konwertuj na płatną subskrypcję <br> Konwertuj na płatną subskrypcję <br> Usuń limit lub poczekaj na zresetowanie limitu |

<sup>1</sup> czy obszaru roboczego znajduje się na warstwę cenową bezpłatna, jest ograniczona do wysyłania do usługi 500 MB danych na dzień. Po osiągnięciu dzienny limit gromadzenie danych zatrzymuje się do następnego dnia. Dane wysyłane podczas zatrzymania zbierania danych nie jest indeksowana i nie jest dostępny do wyszukiwania. Po wznowieniu pracy zbierania danych, przetwarzanie odbywa się tylko w przypadku nowych danych wysyłane. 

Analiza dzienników używa czas UTC i uruchamia każdego dnia o północy czasu UTC. Jeśli obszar roboczy osiągnie limit dzienny, przetwarzania wznawia podczas pierwszej godziny następnego dnia UTC.

### <a name="q-how-can-i-be-notified-when-data-collection-stops"></a>Q. Jak można zostanie wyświetlone powiadomienie po zatrzymaniu zbierania danych?

Odpowiedź: wykonaj kroki opisane w [Tworzenie reguły alertu](log-analytics-alerts-creating.md#create-an-alert-rule) zgłaszane po zatrzymaniu zbierania danych.

Podczas tworzenia alertu dla po zatrzymaniu zbierania danych należy skonfigurować:
- **Nazwa** do *zatrzymać zbieranie danych*
- **Ważność** na *Ostrzeżenie*
- **Zapytanie wyszukiwania** na `Type=Operation OperationCategory="Data Collection Status" OperationStatus=Warning`
- **Przedział czasu** do *2 godziny*.
- **Częstotliwość alertów** na jedną godzinę, ponieważ dane użycia są aktualizowane tylko raz na godzinę.
- **Generuj alert w oparciu o** na *Liczba wyników*
- **Liczba wyników** na *Większa niż 0*

Wykonaj kroki opisane w sekcji dotyczącej [dodawania akcji do reguł alertów](log-analytics-alerts-actions.md) i skonfiguruj wiadomość e-mail, element webhook lub akcję runbook dla reguły alertu.


## <a name="configuration"></a>Konfiguracja
### <a name="q-can-i-change-the-name-of-the-tableblob-container-used-to-read-from-azure-diagnostics-wad"></a>Q. Czy można zmienić nazwę tabeli/blobcontainer używany do odczytu z diagnostyki Azure (WAD)?

A. Nie, nie jest obecnie możliwa do odczytu z dowolnego tabel lub kontenerów w magazynie Azure.

### <a name="q-what-ip-addresses-does-the-log-analytics-service-use-how-do-i-ensure-that-my-firewall-only-allows-traffic-to-the-log-analytics-service"></a>Q. Adresy IP jest używana usługa Log Analytics? Jak zapewnić, że moje zapora zezwala na tylko ruch z usługą analizy dzienników

A. Usługi analizy dzienników jest oparty na platformie Azure. Adresy IP analizy dziennika znajdują się w [zakresów IP centrum danych Microsoft Azure](http://www.microsoft.com/download/details.aspx?id=41653).

Podczas wdrożenia usługi zostały wprowadzone, zmieniać rzeczywiste adresów IP usługi analizy dzienników. Nazwy DNS, aby zezwolić za pośrednictwem zapory są udokumentowane w [skonfigurować ustawienia serwera proxy i zapory w analizy dzienników](log-analytics-proxy-firewall.md).

### <a name="q-i-use-expressroute-for-connecting-to-azure-does-my-log-analytics-traffic-use-my-expressroute-connection"></a>Q. ExpressRoute można używać do nawiązywania połączenia z platformy Azure. Moje analizy dzienników ruchu używa połączenie ExpressRoute?

A. Opisano różne rodzaje ruchu usługi ExpressRoute w [dokumentacja usługi ExpressRoute](../expressroute/expressroute-faqs.md#supported-services).

Ruch do analizy dzienników korzysta z obwodem usługi ExpressRoute publicznej komunikacji równorzędnej.

### <a name="q-is-there-a-simple-and-easy-way-to-move-an-existing-log-analytics-workspace-to-another-log-analytics-workspaceazure-subscription"></a>Q. Czy istnieje prosty i łatwy sposób przenieść istniejący obszar roboczy analizy dzienników do innej subskrypcji Azure/obszaru roboczego analizy dzienników?

A. `Move-AzureRmResource` Polecenie cmdlet pozwala przenoszeniu obszaru roboczego analizy dzienników, a konto usługi Automatyzacja z jedną subskrypcją platformy Azure. Aby uzyskać więcej informacji, zobacz [Move AzureRmResource](http://msdn.microsoft.com/library/mt652516.aspx).

Ta zmiana może być również w portalu Azure.

Nie można przenieść dane z jednego obszaru roboczego analizy dzienników do innego lub zmień analizy dzienników danych przechowywanych w regionie.

### <a name="q-how-do-i-add-log-analytics-to-system-center-operations-manager"></a>Pytanie: jak dodać analizy dzienników do programu System Center Operations Manager?

A: aktualizowanie do najnowszego pakietu zbiorczego aktualizacji i importowanie pakietów administracyjnych umożliwia łączenie programu Operations Manager do analizy dzienników.

>[!NOTE]
>Połączenie programu Operations Manager do analizy dzienników jest dostępna tylko dla programu System Center Operations Manager 2012 z dodatkiem SP1 i nowszych.

### <a name="q-how-can-i-confirm-that-an-agent-is-able-to-communicate-with-log-analytics"></a>Pytanie: jak można potwierdzić, że agent jest w stanie nawiązać połączenia z analizy dzienników?

Odp.: aby upewnić się, że agent może komunikować się z usługą OMS, przejdź do: Panel sterowania, zabezpieczeń i ustawień, **programu Microsoft Monitoring Agent**.

W obszarze **Analiza dzienników Azure (OMS)** karcie, poszukaj zielony znacznik wyboru. Ikona zielony znacznik wyboru potwierdza, że agent jest w stanie komunikować się z usługą OMS.

Żółta ikona ostrzeżenia oznacza, że agent występują problemy dotyczące komunikacji z usługą OMS. Najczęściej zdarza się to usługa Microsoft Monitoring Agent została zatrzymana. Używają Menedżera kontroli usług, aby ponownie uruchomić usługę.

### <a name="q-how-do-i-stop-an-agent-from-communicating-with-log-analytics"></a>Pytanie: jak zatrzymać agenta komunikację z Log Analytics?

A: w programie System Center Operations Manager, Usuń komputer z listy komputerów zarządzanych Advisor. Operations Manager zaktualizuje konfigurację agenta już raportu analizy dzienników. Dla agentów podłączone bezpośrednio do analizy dzienników, można je zatrzymać komunikację za pośrednictwem: Panel sterowania, zabezpieczeń i ustawień, **programu Microsoft Monitoring Agent**.
W obszarze **Analiza dzienników Azure (OMS)**, Usuń wszystkie obszary robocze wymienione.

### <a name="q-why-am-i-getting-an-error-when-i-try-to-move-my-workspace-from-one-azure-subscription-to-another"></a>Pytanie: Dlaczego otrzymuję błąd przy próbie przenoszeniu mojego obszaru roboczego z jedną subskrypcją platformy Azure?

A. Jeśli używasz portalu Azure, upewnij się, że wybrano tylko obszaru roboczego do przeprowadzenia migracji. Nie wybieraj rozwiązania — zostanie automatycznie przełączona po przesunięciu obszaru roboczego. 

Upewnij się, że masz uprawnienia w obu subskrypcji platformy Azure.

## <a name="agent-data"></a>Dane agenta
### <a name="q-how-much-data-can-i-send-through-the-agent-to-log-analytics-is-there-a-maximum-amount-of-data-per-customer"></a>Q. Ilość danych można wysyłać agenta w celu analizy dzienników? Istnieje już maksymalna ilość danych klienta?
A. Planu free Ustawia dzienny limit 500 MB na obszar roboczy. Plany warstwy standardowa i premium ma żadnego limitu ilości danych, który jest przekazywany. Usługa w chmurze, analizy dzienników zaprojektowano w celu automatycznego skalowania do uchwytu woluminu pochodzące z klientem — nawet jeśli jest ona terabajtów na dzień.

Agent Log Analytics została zaprojektowana w celu upewnij się, że ma ona niewielkie rozmiary. Jednym z naszych klientów zapisano blog o testów, które są wykonane względem naszego agenta i jak wrażeniem były. Ilość danych w zależności od rozwiązania, które można włączyć. Możesz znaleźć szczegółowe informacje na temat ilość danych i rozpad przez rozwiązanie w [użycia](log-analytics-usage.md) strony.

Aby uzyskać więcej informacji można znaleźć [blogu klienta](http://thoughtsonopsmgr.blogspot.com/2015/09/one-small-footprint-for-server-one.html) o niewielki rozmiar agenta pakietu OMS.

### <a name="q-how-much-network-bandwidth-is-used-by-the-microsoft-management-agent-mma-when-sending-data-to-log-analytics"></a>Q. Jaka przepustowość sieci jest używany przez program Microsoft Management Agent (MMA) podczas wysyłania danych do analizy dzienników?

A. Przepustowość jest funkcja na ilość danych przesyłanych. Dane są kompresowane podczas ich przesyłania przez sieć.

### <a name="q-how-much-data-is-sent-per-agent"></a>Q. Ilość danych są wysyłane na agenta?

A. Zależy od ilości danych wysłanych w ciągu agenta:

* Rozwiązania, które aktywowano
* Liczba dzienników i liczniki wydajności są zbierane
* Ilość danych w dziennikach

Warstwa cenowa bezpłatna to dobry sposób na dołączyć kilka serwerów i ilość danych typowych miernika. Ogólne użycie jest wyświetlany na [użycia](log-analytics-usage.md) strony.

Dla komputerów, które można uruchomić agenta WireData Użyj następującego zapytania, aby zobaczyć, jak dużo danych jest wysyłane:

```
Type=WireData (ProcessName="C:\\Program Files\\Microsoft Monitoring Agent\\Agent\\MonitoringHost.exe") (Direction=Outbound) | measure Sum(TotalBytes) by Computer
```



## <a name="next-steps"></a>Następne kroki
* [Wprowadzenie do analizy dzienników](log-analytics-get-started.md) Dowiedz się więcej na temat analizy dzienników i rozpocząć pracę w minutach.
