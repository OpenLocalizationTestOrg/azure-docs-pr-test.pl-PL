---
title: "Konserwacja aaaPredictive w aerospace z platformy Azure — podręcznik techniczny Cortana Intelligence rozwiązania | Dokumentacja firmy Microsoft"
description: "Podręcznik techniczny toohello szablon rozwiązania z Microsoft Cortana Intelligence do konserwacji predykcyjnej w aerospace, narzędzia i transportu."
services: cortana-analytics
documentationcenter: 
author: fboylu
manager: jhubbard
editor: cgronlun
ms.assetid: 2c4d2147-0f05-4705-8748-9527c2c1f033
ms.service: cortana-analytics
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: fboylu
ms.openlocfilehash: 30ddc1c101007546ae1b303bccebae3ecdacb442
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="technical-guide-toohello-cortana-intelligence-solution-template-for-predictive-maintenance-in-aerospace-and-other-businesses"></a>Podręcznik techniczny toohello szablon rozwiązania Cortana Intelligence do konserwacji predykcyjnej aerospace i innych firm

## <a name="important"></a>**Ważne**
W tym artykule jest przestarzała. informacje Hello jest problem toohello nadal obowiązują, tj. konserwacji predykcyjnej w Aerospace, ale hello najnowszy artykuł wiedzy hello najbardziej toodate parametrów można znaleźć [tutaj](https://github.com/Azure/cortana-intelligence-predictive-maintenance-aerospace). 

## <a name="acknowledgements"></a>**Potwierdzeń**
W tym artykule jest przypisany przez analityków danych Yan Zhang Gauher Shaheen, uż Boylu Fidan i odtwarzania oprogramowania Dan Grecoe firmy Microsoft.

## <a name="overview"></a>**Omówienie**
Szablony rozwiązań zostały zaprojektowane tooaccelerate hello proces tworzenia pokaz E2E u góry pakietu Cortana Intelligence Suite. Szablon wdrożonej będzie obsługi administracyjnej subskrypcji z niezbędne składniki Cortana Intelligence i kompilacji hello relacji między nimi. Z przykładowymi danymi wygenerowanych z aplikacji generator danych, co spowoduje pobrać i zainstalować na komputerze lokalnym po wdrożeniu szablon rozwiązania hello są również nasion hello danych potoku. wygenerowana przez hello generator danych Hello będzie hydrate hello potoku danych i rozpoczęcia generowania prognoz uczenia maszynowego, które mogą być następnie wizualizowane na pulpit nawigacyjny usługi Power BI hello. proces wdrażania Hello przeprowadzi Cię kilka kroków tooset zapasową poświadczeń rozwiązania. Upewnij się, że rekord tych poświadczeń, takich jak nazwa rozwiązania, nazwę użytkownika i hasło, które należy podać podczas wdrażania hello.  

Hello celem niniejszego dokumentu jest architektura referencyjna hello tooexplain i różnych składników udostępniane w ramach subskrypcji w ramach tego rozwiązania szablonu. dokument Hello komunikuje się również o tym, jak tooreplace dane przykładowe dane własne toobe stanie toosee insights i predykcje uzyskiwane z danych użytkownika. Ponadto hello dokumencie omówiono części hello szablon rozwiązania, wymagającym toobe modyfikacji, jeśli chce toocustomize hello rozwiązania z użyciem własnych danych. Na końcu hello znajdują się instrukcje dotyczące sposobu toobuild hello pulpit nawigacyjny usługi Power BI dla tego szablonu rozwiązania.

> [!TIP]
> Możesz pobrać i wydrukować [wersja tego dokumentu PDF](http://download.microsoft.com/download/F/4/D/F4D7D208-D080-42ED-8813-6030D23329E9/cortana-analytics-technical-guide-predictive-maintenance.pdf).
> 
> 

## <a name="big-picture"></a>**Duży obraz**
![Architektura konserwacji predykcyjnej](media/cortana-analytics-technical-guide-predictive-maintenance/predictive-maintenance-architecture.png)

Po wdrożeniu rozwiązania hello różne usługi platformy Azure w ramach Cortana Analytics Suite zostaną aktywowane (*tj.* Centrum zdarzeń, Stream Analytics, HDInsight, fabryki danych Machine Learning, *itp.*). diagram architektury Hello powyżej wskazuje na wysokim poziomie, jak hello konserwacji predykcyjnej dla lotniczego szablon rozwiązania jest tworzony z end-to-end. Będziesz w stanie tooinvestigate tych usług w portalu hello azure, klikając je na diagramie szablon rozwiązania hello utworzone za pomocą wdrażania hello hello rozwiązania z wyjątkiem hello usługi hdinsight, ponieważ ta usługa jest inicjowana na żądanie, gdy hello powiązane potok działania są wymagane toorun i później usunięte.
Możesz pobrać [pełnym rozmiarze wersji diagramu hello](http://download.microsoft.com/download/1/9/B/19B815F0-D1B0-4F67-AED3-A40544225FD1/ca-topologies-maintenance-prediction.png).

Witaj następujące sekcje opisują każdego z nich.

## <a name="data-source-and-ingestion"></a>**Źródło danych i wprowadzanie**
### <a name="synthetic-data-source"></a>Źródło danych syntetycznego
Dla tych danych hello szablonu źródło używane jest generowana z aplikacją, która będzie Pobierz i uruchom lokalnie, po pomyślnym wdrożeniu. Zostanie Znajdź hello instrukcje toodownload i zainstalować tę aplikację w pasku właściwości powitania po wybraniu hello pierwszego węzła o nazwie Generator danych konserwacji predykcyjnej na diagramie szablon rozwiązania hello. Ta aplikacja źródła hello [Azure Event Hub](#azure-event-hub) usługi z punktów danych lub zdarzeń, które będą używane w rest hello hello rozwiązania przepływu. To źródło danych jest obejmuje lub z dostępnych publicznie danych z [repozytorium danych NASA](http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/) przy użyciu hello [zestawu danych symulacji degradacji aparat turbowentylatorowe](http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/#turbofan).

Aplikacja generowania zdarzeń Hello spowoduje wypełnienie hello Azure Event Hub tylko wtedy, gdy jest wykonywane na tym komputerze.

### <a name="azure-event-hub"></a>Centrum zdarzeń platformy Azure
Witaj [Azure Event Hub](https://azure.microsoft.com/services/event-hubs/) usługi jest odbiorcą hello hello wejściowych przez hello syntetyczne źródło danych powyższy.

## <a name="data-preparation-and-analysis"></a>**Przygotowanie danych i analiza**
### <a name="azure-stream-analytics"></a>Usługa Azure Stream Analytics
Witaj [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) usługi jest używane tooprovide niemal w czasie rzeczywistym analizy hello strumienia wejściowego z hello [Azure Event Hub](#azure-event-hub) usługi i opublikować wyniki na [usługi Power BI](https://powerbi.microsoft.com) pulpitu nawigacyjnego, jak również archiwizowanie wszystkie nieprzetworzone toohello zdarzenia przychodzące [usługi Azure Storage](https://azure.microsoft.com/services/storage/) usługi do późniejszego przetwarzania przez hello [fabryki danych Azure](https://azure.microsoft.com/documentation/services/data-factory/) usługi.

### <a name="hd-insights-custom-aggregation"></a>Informacje na temat technologii HD niestandardowych agregacji
Hello usługi wglądu HD Azure jest używana toorun [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) agregacji tooprovide skryptów (zorkiestrowana przez fabryki danych Azure) na powitania nieprzetworzone zdarzenia, które zostały zarchiwizowane przy użyciu usługi Azure Stream Analytics hello.

### <a name="azure-machine-learning"></a>Azure Machine Learning
Witaj [usługi Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) (zorkiestrowana przez fabryki danych Azure), używana jest usługa prognoz toomake na powitania pozostałych użytkowania (RUL) aparatem określonego powietrznego podane dane wejściowe hello odebrane.

## <a name="data-publishing"></a>**Publikowanie danych**
### <a name="azure-sql-database-service"></a>Usługa bazy danych Azure SQL
Witaj [bazy danych SQL Azure](https://azure.microsoft.com/services/sql-database/) usługi jest używane toostore (zarządzane przez fabryki danych Azure) hello prognoz odebranych przez hello usługi usługi Azure Machine Learning, które zostaną użyte w hello [usługi Power BI](https://powerbi.microsoft.com) pulpitu nawigacyjnego.

## <a name="data-consumption"></a>**Użycie danych**
### <a name="power-bi"></a>Power BI
Hello [usługi Power BI](https://powerbi.microsoft.com) usługi jest używane tooshow pulpit nawigacyjny, który zawiera agregacji i alerty podał hello [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) usługi oraz prognoz RUL przechowywane w [Azure SQL Baza danych](https://azure.microsoft.com/services/sql-database/) które zostały utworzone przy użyciu hello [usługi Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) usługi. Aby uzyskać instrukcje dotyczące sposobu toobuild hello pulpit nawigacyjny usługi Power BI dla tego szablonu rozwiązania można znaleźć toohello poniżej.

## <a name="how-toobring-in-your-own-data"></a>**Jak toobring w swoich własnych danych**
W tej sekcji opisano, jak toobring tooAzure własnych danych i obszarów, jakie wymagałyby zmiany danych hello wprowadzenia w tej architekturze.

Jest mało prawdopodobne, że wszelkie dataset przełączeniem spowoduje dopasowanie hello zestawu danych używanego przez hello [zestawu danych symulacji degradacji aparat turbowentylatorowe](http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/#turbofan) używane dla tego szablonu rozwiązania. Opis danych i wymagania zostaną kluczową rolę w sposób modyfikowania toowork tego szablonu z użyciem własnych danych. Jeśli jest to pierwszy toohello narażenia usługi Azure Machine Learning, można uzyskać tooit wprowadzenie za pomocą przykład Witaj w [jak toocreate pierwszego eksperymentu](machine-learning-create-experiment.md).

następujące sekcje Hello przedstawimy sekcje hello hello szablonu, który będzie wymagać modyfikacji, jeśli wprowadzono nowy zestaw danych.

### <a name="azure-event-hub"></a>Centrum zdarzeń platformy Azure
Hello usługi Azure Event Hub jest bardzo ogólnych w taki sposób, że dane mogą być publikowane Centrum toohello w formacie CSV lub JSON. Brak specjalnego przetwarzania występuje w hello Azure Event Hub, ale jest ważne, aby zrozumieć hello dane, które są przekazywane do niego.

Ten dokument nie opisuje sposób tooingest danych, ale umożliwia łatwe wysyłanie zdarzeń lub danych tooan Centrum zdarzeń platformy Azure przy użyciu hello API Centrum zdarzeń.

### <a name="azure-stream-analytics"></a>Usługa Azure Stream Analytics
Hello usługi Azure Stream Analytics jest używane tooprovide niemal w czasie rzeczywistym analizy odczytywanie ze strumieni danych i wyprowadzania danych tooany liczbę źródeł.

Zapytanie usługi Azure Stream Analytics hello konserwacji predykcyjnej lotniczego szablonu rozwiązania składa się z czterech podzapytaniach, każdego zdarzenia korzystanie z hello usługi Azure Event Hub i konieczności dane wyjściowe cztery różne lokalizacje. Te dane wyjściowe składają się z trzech zbiorów danych usługi Power BI i jedną lokalizację magazynu Azure.

Hello Azure Stream Analytics query można znaleźć przez:

* Logowanie do hello portalu Azure
* Lokalizowanie zadania usługi analiza strumienia hello ![ikona Stream Analytics](media/cortana-analytics-technical-guide-predictive-maintenance/icon-stream-analytics.png) które zostały wygenerowane, gdy wdrożono rozwiązanie hello (*np.*, **maintenancesa02asapbi** i **maintenancesa02asablob** dla rozwiązania konserwacji predykcyjnej)
* Wybieranie
  
  * ***Dane wejściowe*** tooview hello zapytania w danych wejściowych
  * ***ZAPYTANIE*** samą kwerendę hello tooview
  * ***GENERUJE*** tooview hello różnych danych wyjściowych

Informacji na temat tworzenia zapytań usługi Azure Stream Analytics można znaleźć w hello [Stream Analytics kwerendy odwołania](https://msdn.microsoft.com/library/azure/dn834998.aspx) w witrynie MSDN.

W tym rozwiązaniu zapytania hello output trzy zestawy danych z niemal analiz w czasie rzeczywistym informacje o hello przychodzących danych strumienia tooa usługi Power BI pulpit nawigacyjny, który jest dostarczane jako część tego szablonu rozwiązania. Ponieważ nie istnieje niejawna wiedzą na temat formatu danych przychodzących hello, te zapytania musi toobe zmienione na podstawie Twojej formatu danych.

Zapytanie Hello w zadaniu Stream Analytics drugi hello **maintenancesa02asablob** po prostu wyświetla wszystkie [Centrum zdarzeń](https://azure.microsoft.com/services/event-hubs/) zdarzenia [usługi Azure Storage](https://azure.microsoft.com/services/storage/) i dlatego wymaga żadne zmiany niezależnie od formatu danych jako hello informacji o zdarzeniu pełne przesyłanej strumieniowo toostorage.

### <a name="azure-data-factory"></a>Azure Data Factory
Witaj [fabryki danych Azure](https://azure.microsoft.com/documentation/services/data-factory/) Usługa uruchamia przepływ hello i przetwarzania danych. W konserwacji predykcyjnej danych hello lotniczego szablon rozwiązania fabryki składa się z trzech [potoki](../data-factory/data-factory-create-pipelines.md) czy przenoszenia i przetwarzania danych hello z użyciem różnych technologii.  Dostępne fabrykę danych przez otwarcie hello hello fabryki danych węzła u dołu hello diagram szablon rozwiązania hello utworzone za pomocą wdrażania hello hello rozwiązania. Spowoduje to przejście możesz toohello fabryki danych portalu Azure. Jeśli błędy są wyświetlane w obszarze zestawów danych, możesz zignorować te są one powodu fabryki toodata wdrażany przed hello generator danych zostało uruchomione. Te błędy nie uniemożliwiają działanie fabryką danych.

![Błędy zbiorów danych fabryki danych](media/cortana-analytics-technical-guide-predictive-maintenance/data-factory-dataset-error.png)

W tej sekcji omówiono konieczne hello [potoki](../data-factory/data-factory-create-pipelines.md) i [działania](../data-factory/data-factory-create-pipelines.md) zawartych w hello [fabryki danych Azure](https://azure.microsoft.com/documentation/services/data-factory/). Poniżej znajdują się w widoku diagramu hello hello rozwiązania.

![Azure Data Factory](media/cortana-analytics-technical-guide-predictive-maintenance/azure-data-factory.png)

Zawiera dwa potoki hello tej fabryki [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) skrypty, które są używane toopartition i hello agregacji danych. Jeśli zaznaczono inaczej, skrypty hello będą znajdować się w hello [usługi Azure Storage](https://azure.microsoft.com/services/storage/) konto utworzone podczas instalacji. Ich lokalizacja będzie: maintenancesascript\\\\skryptu\\\\hive\\ \\ (lub https://[Your name].blob.core.windows.net/maintenancesascript rozwiązania).

Podobne toohello [Azure Stream Analytics](#azure-stream-analytics-1) zapytań, [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) skryptów ma niejawne informacji na temat hello przychodzące format danych, musi toobe zmienić te zapytania oparte na format danych i [Inżynieria](machine-learning-feature-selection-and-engineering.md) wymagania.

#### <a name="aggregateflightinfopipeline"></a>*AggregateFlightInfoPipeline*
To [potoku](../data-factory/data-factory-create-pipelines.md) zawiera pojedyncze działanie - [HDInsightHive](../data-factory/data-factory-hive-activity.md) działania przy użyciu [HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx) , na którym działa [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) Umieść skrypt toopartition hello danych w [usługi Azure Storage](https://azure.microsoft.com/services/storage/) podczas [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) zadania.

[Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) skryptów jest to zadanie partycjonowania ***AggregateFlightInfo.hql***

#### <a name="mlscoringpipeline"></a>*MLScoringPipeline*
To [potoku](../data-factory/data-factory-create-pipelines.md) zawiera kilka działań i którego wynik końcowy jest oceniane hello prognoz z hello [usługi Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) eksperymentu skojarzone z tym szablonem rozwiązania.

dostępne są następujące działania Hello zawarte w tym:

* [HDInsightHive](../data-factory/data-factory-hive-activity.md) działania przy użyciu [HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx) , na którym działa [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) skryptów tooperform agregacji i inżynieria niezbędne do hello [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) eksperymentu.
  [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) skryptów jest to zadanie partycjonowania ***PrepareMLInput.hql***.
* [Kopia](https://msdn.microsoft.com/library/azure/dn835035.aspx) działanie, które przenosi hello wyników z [HDInsightHive](../data-factory/data-factory-hive-activity.md) tooa działania pojedynczego [usługi Azure Storage](https://azure.microsoft.com/services/storage/) obiektu blob, które mogą być dostępu przez [AzureMLBatchScoring](https://msdn.microsoft.com/library/azure/dn894009.aspx) działania.
* [AzureMLBatchScoring](https://msdn.microsoft.com/library/azure/dn894009.aspx) działania, która wywołuje hello [usługi Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) eksperymentu, co powoduje wyniki hello dotyczy żądanie put w jednej [usługi Azure Storage](https://azure.microsoft.com/services/storage/) obiektu blob.

#### <a name="copyscoredresultpipeline"></a>*CopyScoredResultPipeline*
To [potoku](../data-factory/data-factory-create-pipelines.md) zawiera pojedyncze działanie - [kopiowania](https://msdn.microsoft.com/library/azure/dn835035.aspx) działanie, które przenosi hello wyniki hello [usługi Azure Machine Learning](#azure-machine-learning) Poeksperymentuj z *** MLScoringPipeline*** toohello [bazy danych SQL Azure](https://azure.microsoft.com/services/sql-database/) udostępniony jako część instalacji szablon rozwiązania.

### <a name="azure-machine-learning"></a>Azure Machine Learning
Hello [usługi Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) eksperymentu używane dla tego szablonu rozwiązanie zapewnia hello pozostałych przydatne w cyklu życia (RUL) powietrznego aparatu. eksperymentu Hello jest toohello określonego zestawu danych używane i dlatego wymaga modyfikacji lub wymiany danych toohello określonych w.

Aby uzyskać informacji na temat sposobu utworzenia hello eksperymentu uczenia maszynowego Azure, zobacz [konserwacji predykcyjnej: krok 1 z 3, przygotowanie danych i funkcji engineering](http://gallery.cortanaanalytics.com/Experiment/Predictive-Maintenance-Step-1-of-3-data-preparation-and-feature-engineering-2).

## <a name="monitor-progress"></a>**Monitoruj postęp**
 Po uruchomieniu hello Generator danych, hello potoku rozpoczyna się tooget uwodniony i hello różnych składników rozwiązania start zasób do akcji następujące polecenia hello wystawiony przez hello fabryki danych. Istnieją dwa sposoby monitorowania hello potoku.

1. Zapisuje jednego zadania usługi analiza strumienia hello hello raw przychodzące tooblob magazynu danych. Kliknij składnik magazynu obiektów Blob rozwiązania na ekranie powitania można pomyślnie wdrożono hello rozwiązania, następnie kliknij polecenie Otwórz w prawym panelu hello spowoduje przejście toohello [portalu zarządzania](https://portal.azure.com/). Wyświetlonym edytorze kliknij na obiekty BLOB. W panelu dalej hello zostanie wyświetlona lista kontenerów. Polecenie **maintenancesadata**. W panelu dalej hello, zobaczysz hello **rawdata** folderu. W folderze rawdata hello zobaczysz folderów przy użyciu nazwy, takie jak godzina = 17, godzina = 18 itp. Jeśli widzisz tych folderów wskazuje pomyślnie jest hello nieprzetworzone dane są generowane na komputerze i przechowywane w magazynie obiektów blob. Powinny pojawić się plików csv, które powinny mieć ograniczone rozmiary MB w tych folderach.
2. Ostatnim krokiem Hello potoku hello jest toowrite danych (np. predykcje uzyskiwane z uczenia maszynowego) do bazy danych SQL. Toowait może mieć maksymalnie trzech godzin, zanim hello tooappear danych w bazie danych SQL. Jednym ze sposobów toomonitor jak dużo danych jest dostępne w bazie danych SQL jest za pośrednictwem [portalu azure](https://manage.windowsazure.com/). Zlokalizuj BAZ danych na lewym panelu hello ![ikona SQL](media/cortana-analytics-technical-guide-predictive-maintenance/icon-SQL-databases.png) i kliknij ją. Zlokalizuj bazę danych **pmaintenancedb** i kliknij go. Na następnej stronie powitania u dołu hello kliknij przycisk ZARZĄDZAJ
   
    ![Ikona zarządzania](media/cortana-analytics-technical-guide-predictive-maintenance/icon-manage.png).
   
    W tym miejscu możesz kliknąć na nowe zapytanie i zapytanie hello liczbę wierszy (np. Wybierz count(*) z PMResult). Wraz z rozwojem bazy danych, należy zwiększyć hello liczbę wierszy w tabeli hello.

## <a name="power-bi-dashboard"></a>**Pulpit nawigacyjny programu Power BI**
### <a name="overview"></a>Omówienie
W tej sekcji opisano, jak tooset się toovisualize pulpit nawigacyjny usługi Power BI danych czasu rzeczywistego z usługi Azure Stream Analytics (ścieżka gorących), a także prognozowania partii wynikiem uczenie maszynowe Azure (zimny ścieżki).

### <a name="setup-cold-path-dashboard"></a>Pulpit nawigacyjny zimnych ścieżki Instalatora
Hello ścieżki zimnych danych potoku hello niezbędne celem jest tooget predykcyjnej RUL (pozostałe użytkowania) każdego powietrznego aparatu po zakończeniu transmitowane (cykle). wynik prognozowania Hello jest aktualizowany co 3 godziny przewidywania hello powietrznego aparatów, które zakończyły lot podczas hello ostatnich 3 godziny.

Usługa Power BI łączy tooan bazy danych Azure SQL jako źródła danych, w którym są przechowywane wyniki prognozowania. Uwaga: 1) podczas wdrażania rozwiązania, rzeczywista prognozowania będą widoczne w hello bazy danych w ciągu 3 godziny.
Plik pbix Hello dołączonej pobierania Generator hello zawiera niektóre dane inicjatora, dlatego możesz od razu utworzyć pulpit nawigacyjny usługi Power BI hello. 2) w tym kroku hello warunkiem wstępnym jest toodownload i zainstaluj oprogramowanie bezpłatne hello [Power BI desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/).

Witaj następujące kroki zawiera informacje pomocne w sposób plików tooconnect hello pbix na powitania bazy danych SQL, które zostało uruchomione w czasie hello zawierającego dane dotyczące wdrażania rozwiązania (*np.*. wyniki prognozowania) dla wizualizacji.

1. Pobierz hello poświadczenia bazy danych.
   
   Będziesz potrzebować **bazy danych, nazwę serwera, nazwa bazy danych, nazwę użytkownika i hasło** przed przeniesieniem toonext czynności. Poniżej przedstawiono hello tooguide kroki należy jak toofind je.
   
   * Raz **usługi Azure SQL Database** w szablonie rozwiązania włącza zielony diagramu, kliknij go, a następnie kliknij przycisk **"Open"**.
   * Zostanie wyświetlone nowe karty/okno przeglądarki wyświetlającego hello strony portalu Azure. Kliknij przycisk **"Grupy zasobów"** na powitania lewego panelu.
   * Wybierz subskrypcję hello używany w przypadku wdrażania rozwiązania hello, a następnie wybierz **"YourSolutionName\_ResourceGroup"**.
   * W hello pop nowy limit panelu kliknij hello ![ikona SQL](media/cortana-analytics-technical-guide-predictive-maintenance/icon-sql.png) tooaccess ikonę bazy danych. Nazwa bazy danych jest ta ikona dalej toohello (*np.*, **"pmaintenancedb"**), a hello **nazwę serwera bazy danych** znajduje się w obszarze hello właściwość nazwy serwera i sprawdzić Podobnie za**YourSoutionName.database.windows.net**.
   * Bazy danych **username** i **hasło** są hello tak samo jak hello nazwy użytkownika i hasła wcześniej zarejestrowane podczas wdrażania rozwiązania hello.
2. Aktualizowanie źródła danych hello hello zimnych Ścieżka raportu pliku Power BI Desktop.
   
   * W folderze hello na komputerze, którego pobrano i unzipped Generator plików, kliknij dwukrotnie **PowerBI\\PredictiveMaintenanceAerospace.pbix** pliku. Jeśli podczas otwierania pliku hello są wyświetlane wszystkie komunikaty ostrzegawcze, można je zignorować. U góry hello hello pliku, kliknij przycisk **"Edytuj zapytania"**.
     
     ![Edytowanie zapytań](media/cortana-analytics-technical-guide-predictive-maintenance/edit-queries.png)
   * Zobaczysz dwóch tabel, **RemainingUsefulLife** i **PMResult**. Wybierz hello pierwszej tabeli, a następnie kliknij przycisk ![ikonę ustawienia zapytania](media/cortana-analytics-technical-guide-predictive-maintenance/icon-query-settings.png) dalej zbyt**'Source'** w obszarze **"KROKI stosowane"** na powitania prawo **"Ustawienia zapytania"**panelu. Ignoruj wszystkie wyświetlone komunikaty ostrzegawcze.
   * W hello pop okna, Zastąp **'Server'** i **"Baza danych"** z własne nazwy serwera i bazy danych, a następnie kliknij przycisk **"OK"**. Dla nazwy serwera, upewnij się, że Określ hello portu 1433 (**YourSoutionName.database.windows.net, 1433**). Pole bazy danych hello jako **pmaintenancedb**. Ignoruj ostrzeżenia hello, które są wyświetlane na ekranie powitania.
   * W hello pop dalej w oknie, zobaczysz dwie opcje w okienku po lewej stronie powitania (**Windows** i **bazy danych**). Kliknij przycisk **"Baza danych"**, wypełnij Twojej **'Username'** i **"Password"** (jest to hello nazwy użytkownika i hasła podczas najpierw wdrożyć rozwiązanie hello i utworzyć Baza danych Azure SQL). W ***wybierz poziom które tooapply te ustawienia mają być***, zaznacz opcję poziomu bazy danych. Następnie kliknij przycisk **"Połącz"**.
   * Polecenie hello drugiej tabeli **PMResult** następnie kliknij przycisk ![ikona nawigacji](media/cortana-analytics-technical-guide-predictive-maintenance/icon-navigation.png) dalej zbyt**'Source'** w obszarze **"KROKI stosowane"** na powitania prawo **"Ustawienia zapytania"** panelu i zaktualizuj powitania serwera i nazwy bazy danych, tak jak hello powyżej kroki i kliknij przycisk OK.
   * Po nawiązaniu połączenia z przewodnikiem toohello wstecz na poprzedniej stronie, zamknij okno hello. Wiadomość zostanie pop out — kliknij przycisk **Zastosuj**. Na koniec kliknij hello **zapisać** przycisk toosave hello zmiany. Plik usługi Power BI ma ustanowione połączenie toohello serwera. Jeśli Twoje wizualizacje są puste, upewnij się, że wyczyścić wszystkie dane hello wybór hello na powitania wizualizacje toovisualize klikając ikonę Gumka hello na powitania prawym górnym rogu hello legendy. Użyj hello odświeżania przycisk tooreflect nowe dane na powitania wizualizacji. Początkowo wyświetlany tylko hello inicjatora danych w sieci wizualizacji fabryki danych hello jest zaplanowane toorefresh co 3 godziny. Po 3 godziny zostanie wyświetlony nowy prognoz, które zostaną uwzględnione w sieci wizualizacji podczas odświeżania danych hello.
3. (Opcjonalnie) Publikowanie pulpitu nawigacyjnego zimnych ścieżki hello zbyt[online usługi Power BI](http://www.powerbi.com/). Należy pamiętać, że ten krok wymaga konta usługi Power BI (lub konta usługi Office 365).
   
   * Kliknij przycisk **"Publikuj"** i później kilku sekund zostanie wyświetlone okno wyświetlania "Publikowania tooPower BI sukcesu!" z zielonym znacznikiem wyboru. Kliknij łącze hello poniżej "Otwórz PredictiveMaintenanceAerospace.pbix w usłudze Power BI". toofind szczegółowe instrukcje, zobacz [publikowania z Power BI Desktop](https://support.powerbi.com/knowledgebase/articles/461278-publish-from-power-bi-desktop).
   * toocreate nowego pulpitu nawigacyjnego: kliknij hello  **+**  zarejestrować dalej toothe **pulpity nawigacyjne** sekcji w okienku po lewej stronie powitania. Wprowadź nazwę hello "Demo konserwacji predykcyjnej" dla tego nowego pulpitu nawigacyjnego.
   * Po otwarciu raportu powitania kliknij ![ikonę PINEZKI](media/cortana-analytics-technical-guide-predictive-maintenance/icon-pin.png) toopin wszystkich na pulpicie nawigacyjnym tooyour wizualizacji. toofind szczegółowe instrukcje, zobacz [Przypnij do pulpitu nawigacyjnego usługi Power BI tooa kafelka z raportu](https://support.powerbi.com/knowledgebase/articles/430323-pin-a-tile-to-a-power-bi-dashboard-from-a-report).
     Przejdź do strony pulpitu nawigacyjnego toohello i dostosować hello rozmiar i położenie sieci wizualizacji i Edytuj ich tytułów. toofind szczegółowe instrukcje na tooedit Twojego Kafelki, zobacz temat [edycji kafelka — zmiany rozmiaru, Przenieś, Zmień nazwę, numer pin, usuwanie, Dodawanie hiperłącza](https://powerbi.microsoft.com/documentation/powerbi-service-edit-a-tile-in-a-dashboard/#rename). Oto pulpitu nawigacyjnego przykład z niektórych tooit wizualizacje przypięty zimnych ścieżki.  W zależności od tego, jak długo zostanie uruchomione z generator danych numery na powitania wizualizacje mogą się różnić.
     <br/>
     ![Widok końcowy](media/cortana-analytics-technical-guide-predictive-maintenance/final-view.png)
     <br/>
   * tooschedule odświeżania danych hello, umieść kursor nad hello **PredictiveMaintenanceAerospace** zestawu danych, kliknij przycisk ![ikoną wielokropka](media/cortana-analytics-technical-guide-predictive-maintenance/icon-elipsis.png) , a następnie wybierz **planowanie odświeżania**.
     <br/>
     **Uwaga:** Jeśli widzisz Masaż ostrzeżenie, kliknij przycisk **edytowanie poświadczeń** i upewnij się, że poświadczenia bazy danych są hello takie same jak te opisane w kroku 1.
     <br/>
     ![Harmonogram odświeżania](media/cortana-analytics-technical-guide-predictive-maintenance/schedule-refresh.png)
     <br/>
   * Rozwiń węzeł hello **planowanie odświeżania** sekcji. Włącz funkcję "zachować aktualność danych".
     <br/>
   * Harmonogram odświeżania hello na podstawie Twoich potrzeb. toofind więcej informacji, zobacz [odświeżania danych w usłudze Power BI](https://support.powerbi.com/knowledgebase/articles/474669-data-refresh-in-power-bi).

### <a name="setup-hot-path-dashboard"></a>Pulpit nawigacyjny aktywnej ścieżki Instalatora
następujące kroki Hello przeprowadzi Cię jak danych czasu rzeczywistego toovisualize dane wyjściowe z usługi analiza strumienia zadania, które zostały wygenerowane w czasie hello wdrożenia rozwiązania. A [online usługi Power BI](http://www.powerbi.com/) konto jest wymagane tooperform hello następujące kroki. Jeśli nie masz konta, możesz [utworzyć](https://powerbi.microsoft.com/pricing).

1. Dodawanie danych wyjściowych usługi Power BI w Azure Stream Analytics (ASA).
   
   * Konieczne będzie instrukcjami hello toofollow [Azure Stream Analytics & usługi Power BI: pulpitu nawigacyjnego analytics w czasie rzeczywistym uzyskać wgląd w czasie rzeczywistym przesyłać strumieniowo danych](../stream-analytics/stream-analytics-power-bi-dashboard.md) tooset się hello wyjściowego zadania usługi analiza strumienia Azure jako zasilania Pulpit nawigacyjny analizy BIZNESOWEJ.
   * Witaj ASA zapytanie ma trzy dane wyjściowe, które są **aircraftmonitor**, **aircraftalert**, i **flightsbyhour**. Hello zapytania można wyświetlić, klikając na karcie zapytania. Tooeach odpowiednich z tych tabel, konieczne będzie tooadd tooASA danych wyjściowych. Po dodaniu hello pierwszy danych wyjściowych (*np.* **aircraftmonitor**) upewnij się, że hello **Alias wyjściowy**, **nazwę zestawu danych** i  **Nazwa tabeli** są takie same hello (**aircraftmonitor**). Dla danych wyjściowych hello Powtórz kroki tooadd **aircraftalert**, i **flightsbyhour**. Po dodaniu wszystkich trzech output tabel i uruchomił zadanie ASA hello, należy pobrać potwierdzenia (*np.*, "Uruchamianie usługi analiza strumienia zadania maintenancesa02asapbi powiodło się.").
2. Zaloguj się za[online usługi Power BI](http://www.powerbi.com)
   
   * Na powitania po lewej sekcji zestawów danych panelu w obszarze Mój obszar roboczy ***DATASET*** nazwy **aircraftmonitor**, **aircraftalert**, i **flightsbyhour**powinna zostać wyświetlona. To hello przesyłanie strumieniowe danych wypychana z usługi Azure Stream Analytics w zestawie danych hello poprzedniej step.hello **flightsbyhour** mogą nie występować w hello czasu takie same, jak hello innych dwóch zestawów danych powodu toohello rodzaj zapytania SQL hello za go. Jednak go powinny być widoczne po upływie godziny.
   * Upewnij się, że hello ***wizualizacje*** okienko jest otwarty i jest wyświetlany na ekranie powitania po prawej stronie.
3. Po utworzeniu hello danych otrzymywanych przez usługę Power BI, można uruchomić wizualizacja hello strumienia danych. Poniżej znajduje się, że pulpit nawigacyjny przykład z niektórych wizualizacjami aktywnej ścieżki przypięty tooit. Można utworzyć innych kafelka pulpitu nawigacyjnego oparte na odpowiednich zestawów danych. W zależności od tego, jak długo zostanie uruchomione z generator danych numery na powitania wizualizacje mogą się różnić.

    ![Widok pulpitu nawigacyjnego](media\cortana-analytics-technical-guide-predictive-maintenance\dashboard-view.png)

1. Poniżej przedstawiono niektóre czynności toocreate jednej kafelków hello powyżej — Witaj "floty widok vs czujnik 11. Próg 48,26" kafelka:
   
   * Kliknij zestaw danych **aircraftmonitor** na powitania po lewej sekcji zestawów danych panelu.
   * Kliknij przycisk hello **wykres liniowy** ikony.
   * Kliknij przycisk **przetwarzanych** w hello **pola** okienku, tak że przedstawia w obszarze "Osi" hello **wizualizacje** okienka.
   * Kliknij przycisk "s11" i "s11\_alert" obydwie będą wyświetlane w obszarze "Wartości". Kliknij strzałkę małych hello obok zbyt**s11** i **s11\_alert**, zmień "Sum" za "średnia".
   * Kliknij przycisk **ZAPISAĆ** hello górnej i nazwa raportu hello "aircraftmonitor". Raport o nazwie "aircraftmonitor" jest wyświetlany w hello **raporty** części hello **Nawigator** w okienku po lewej stronie powitania.
   * Kliknij przycisk hello **numeru Pin Visual** ikonę na powitania prawym górnym rogu ten wykres liniowy. Można wybrać pulpit nawigacyjny może wyświetlane okno "TooDashboard numeru Pin". Wybierz "Demo konserwacji predykcyjnej", a następnie kliknij przycisk "Numer Pin".
   * Umieść kursor myszy hello za pośrednictwem tego kafelka na pulpicie nawigacyjnym hello, kliknij ikonę "edit" hello na powitania toochange prawym górnym rogu jego tytuł zbyt "vs floty widoku czujnik 11. Próg 48,26" i pomocniczą zbyt"średni między floty w czasie".

## <a name="how-toodelete-your-solution"></a>**Jak toodelete rozwiązania**
Sprawdź, czy Zatrzymaj hello generator danych, gdy nie są aktywnie przy użyciu rozwiązania hello uruchamiania generatora danych hello będą naliczane wyższe koszty. Usuń hello rozwiązanie, jeśli nie są używane. Usunięcie rozwiązania spowoduje usunięcie wszystkich składników hello aprowizowane w Twojej subskrypcji po wdrożeniu rozwiązania hello. rozwiązanie hello toodelete kliknij swoją nazwę rozwiązania, w lewym panelu hello hello rozwiązania szablonu i kliknij delete.

## <a name="cost-estimation-tools"></a>**Narzędzia oszacowanie kosztów**
Witaj następujące dwa narzędzia są dostępne toohelp lepiej zrozumieć całkowity koszt objętego uruchomiona hello konserwacji predykcyjnej lotniczego szablon rozwiązania w ramach subskrypcji:

* [Microsoft Azure koszt narzędzia do szacowania Tool (online)](https://azure.microsoft.com/pricing/calculator/)
* [Microsoft Azure koszt narzędzia do szacowania Tool (desktop)](http://www.microsoft.com/download/details.aspx?id=43376)

