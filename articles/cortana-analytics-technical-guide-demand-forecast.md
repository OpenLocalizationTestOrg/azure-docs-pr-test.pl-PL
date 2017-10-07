---
title: "aaaDemand prognozy w podręczniku technicznym energii | Dokumentacja firmy Microsoft"
description: "Podręcznik techniczny toohello szablon rozwiązania z Microsoft Cortana Intelligence dla Prognoza energii."
services: cortana-analytics
documentationcenter: 
author: yijichen
manager: ilanr9
editor: yijichen
ms.assetid: 7f1a866b-79b7-4b97-ae3e-bc6bebe8c756
ms.service: cortana-analytics
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2016
ms.author: inqiu;yijichen;ilanr9
ms.openlocfilehash: c97b7c19c9e3a317aecc329e61a0692d2f1ec53e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="technical-guide-toohello-cortana-intelligence-solution-template-for-demand-forecast-in-energy"></a>Podręcznik techniczny toohello szablon rozwiązania Cortana Intelligence dla Prognoza energii
## <a name="overview"></a>**Omówienie**
Szablony rozwiązań zostały zaprojektowane tooaccelerate hello proces tworzenia pokaz E2E u góry pakietu Cortana Intelligence Suite. Szablon wdrożonej będzie obsługi administracyjnej subskrypcji z wymagany składnik Cortana Intelligence i kompilacji hello relacje między. Z przykładowymi danymi pobierania wygenerowanych z aplikacji symulacji danych są również nasion hello danych potoku. Pobrać hello symulatora danych z łączem hello i zainstaluj go na komputerze lokalnym, można znaleźć plik readme.txt toohello instrukcji przy użyciu symulatora hello. Dane generowane przez symulator hello będzie hydrate hello potoku danych, a następnie Rozpocznij generowanie machine learning prognozowania, które mogą być następnie wizualizowane na pulpit nawigacyjny usługi Power BI hello.

Szablon rozwiązania Hello można znaleźć [tutaj](https://gallery.cortanaintelligence.com/SolutionTemplate/Demand-Forecasting-for-Energy-1)

proces wdrażania Hello przeprowadzi Cię kilka kroków tooset zapasową poświadczeń rozwiązania. Upewnij się, że rekord tych poświadczeń, takich jak nazwa rozwiązania, nazwę użytkownika i hasło, które należy podać podczas wdrażania hello.

Hello celem niniejszego dokumentu jest architektura referencyjna hello tooexplain i różnych składników udostępniane w ramach subskrypcji w ramach tego rozwiązania szablonu. dokument Hello zawiera również informacje o jak tooreplace hello przykładowych danych, dane z własnych toobe stanie toosee insights/prognoz w przypadku danych. Ponadto hello dokumencie omówiono hello części hello szablon rozwiązania, wymagającym toobe modyfikacji, jeśli chcesz toocustomize hello rozwiązania z użyciem własnych danych. Na końcu hello znajdują się instrukcje dotyczące sposobu toobuild hello pulpit nawigacyjny usługi Power BI dla tego szablonu rozwiązania.

## <a name="big-picture"></a>**Duży obraz**
![](media/cortana-analytics-technical-guide-demand-forecast/ca-topologies-energy-forecasting.png)

### <a name="architecture-explained"></a>Architektura wyjaśniono
Po wdrożeniu rozwiązania hello różne usługi platformy Azure w ramach Cortana Analytics Suite zostaną aktywowane (*tj.* Centrum zdarzeń, Stream Analytics, HDInsight, fabryki danych Machine Learning, *itp.*). diagram architektury Hello powyżej wskazuje na wysokim poziomie, jak żądanie Prognozowanie na szablon rozwiązania energii hello jest tworzony z end-to-end. Będzie możliwe tooinvestigate tych usług za pomocą kliknięcia na hello diagram szablon rozwiązania utworzone przy użyciu wdrażania hello hello rozwiązania. Witaj następujące sekcje opisują każdego z nich.

## <a name="data-source-and-ingestion"></a>**Źródło danych i wprowadzanie**
### <a name="synthetic-data-source"></a>Źródło danych syntetycznego
Dla tych danych hello szablonu źródło używane jest generowana z aplikacją, która będzie Pobierz i uruchom lokalnie, po pomyślnym wdrożeniu. Zostanie Znajdź hello instrukcje toodownload i zainstalować tę aplikację w pasku właściwości powitania po wybraniu hello pierwszego węzła o nazwie symulatora danych prognozowania energii na diagramie szablon rozwiązania hello. Ta aplikacja źródła hello [Azure Event Hub](#azure-event-hub) usługi z punktów danych lub zdarzeń, które będą używane w rest hello hello rozwiązania przepływu.

Aplikacja generowania zdarzeń Hello spowoduje wypełnienie hello Azure Event Hub tylko wtedy, gdy jest wykonywane na tym komputerze.

### <a name="azure-event-hub"></a>Centrum zdarzeń platformy Azure
Witaj [Azure Event Hub](https://azure.microsoft.com/services/event-hubs/) usługi jest odbiorcą hello hello wejściowych przez hello syntetyczne źródło danych powyższy.

## <a name="data-preparation-and-analysis"></a>**Przygotowanie danych i analiza**
### <a name="azure-stream-analytics"></a>Usługa Azure Stream Analytics
Witaj [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) usługi jest używane tooprovide niemal w czasie rzeczywistym analizy hello strumienia wejściowego z hello [Azure Event Hub](#azure-event-hub) usługi i opublikować wyniki na [usługi Power BI](https://powerbi.microsoft.com) pulpitu nawigacyjnego, jak również archiwizowanie wszystkie nieprzetworzone toohello zdarzenia przychodzące [usługi Azure Storage](https://azure.microsoft.com/services/storage/) usługi do późniejszego przetwarzania przez hello [fabryki danych Azure](https://azure.microsoft.com/documentation/services/data-factory/) usługi.

### <a name="hd-insights-custom-aggregation"></a>HD Insights niestandardowych agregacji
Hello usługi wglądu HD Azure jest używana toorun [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) agregacji tooprovide skryptów (zorkiestrowana przez fabryki danych Azure) na powitania nieprzetworzone zdarzenia, które zostały zarchiwizowane przy użyciu usługi Azure Stream Analytics hello.

### <a name="azure-machine-learning"></a>Azure Machine Learning
Witaj [usługi Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) (zorkiestrowana przez fabryki danych Azure), używana jest usługa toomake prognozy na zużycie energii przyszłych podane dane wejściowe hello Odebrano danego regionu.

## <a name="data-publishing"></a>**Publikowanie danych**
### <a name="azure-sql-database-service"></a>Usługa bazy danych Azure SQL
Witaj [bazy danych SQL Azure](https://azure.microsoft.com/services/sql-database/) usługi jest używane toostore (zarządzane przez fabryki danych Azure) hello prognoz odebranych przez hello usługi usługi Azure Machine Learning, które zostaną użyte w hello [usługi Power BI](https://powerbi.microsoft.com) pulpitu nawigacyjnego.

## <a name="data-consumption"></a>**Użycie danych**
### <a name="power-bi"></a>Power BI
Hello [usługi Power BI](https://powerbi.microsoft.com) usługi jest używane tooshow pulpit nawigacyjny, który zawiera agregacji podał hello [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) usługi, a także żądanie prognozy przechowywane w wynikach [Azure SQL Baza danych](https://azure.microsoft.com/services/sql-database/) które zostały utworzone przy użyciu hello [usługi Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) usługi. Aby uzyskać instrukcje dotyczące sposobu toobuild hello pulpit nawigacyjny usługi Power BI dla tego szablonu rozwiązania można znaleźć toohello poniżej.

## <a name="how-toobring-in-your-own-data"></a>**Jak toobring w swoich własnych danych**
W tej sekcji opisano, jak toobring tooAzure własnych danych i obszarów, jakie wymagałyby zmiany danych hello wprowadzenia w tej architekturze.

Jest mało prawdopodobne, że wszelkie zestawu danych, które można przenosić spowoduje dopasowanie dataset hello używane dla tego szablonu rozwiązania. Opis danych i wymagania zostaną kluczową rolę w sposób modyfikowania toowork tego szablonu z użyciem własnych danych. Jeśli jest to pierwszy toohello narażenia usługi Azure Machine Learning, można uzyskać tooit wprowadzenie za pomocą przykład Witaj w [jak toocreate pierwszego eksperymentu](machine-learning/machine-learning-create-experiment.md).

następujące sekcje Hello przedstawimy sekcje hello hello szablonu, który będzie wymagać modyfikacji, jeśli wprowadzono nowy zestaw danych.

### <a name="azure-event-hub"></a>Centrum zdarzeń platformy Azure
Witaj [Azure Event Hub](https://azure.microsoft.com/services/event-hubs/) usługi jest bardzo ogólnych w taki sposób, że dane mogą być publikowane Centrum toohello w formacie CSV lub JSON. Brak specjalnego przetwarzania występuje w hello Azure Event Hub, ale należy pamiętać, że rozumiesz hello dane, które są przekazywane do niego.

Ten dokument nie opisuje sposób tooingest danych, ale jeden umożliwia łatwe wysyłanie zdarzeń lub tooan danych Azure Event Hub przy użyciu hello [API Centrum zdarzeń](event-hubs/event-hubs-programming-guide.md).

### <a name="azure-stream-analytics"></a>Usługa Azure Stream Analytics
Witaj [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) usługi jest używane tooprovide niemal w czasie rzeczywistym analizy odczytywanie ze strumieni danych i wyprowadzania danych tooany liczbę źródeł.

Hello Azure Stream Analytics query hello żądanie Prognozowanie na szablon rozwiązania energii, składa się z dwóch podzapytaniach, każdy wykorzystywanie zdarzenia z usługi Azure Event Hub hello jako dane wejściowe i mających różne lokalizacje tootwo dane wyjściowe. Te dane wyjściowe zawierają zestawy danych usługi Power BI oraz jedną lokalizację magazynu Azure.

Witaj [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) można znaleźć zapytania według:

* Logowanie do hello [portalu zarządzania Azure](https://manage.windowsazure.com/)
* Lokalizowanie zadania usługi analiza strumienia hello ![](media/cortana-analytics-technical-guide-demand-forecast/icon-stream-analytics.png) które zostały wygenerowane podczas hello rozwiązanie zostało wdrożone. Jedna jest do wypychania tooblob pamięci masowej (np. mytest1streaming432822asablob) i hello innych, potrzebnych jest do wypychania danych tooPower analizy Biznesowej (np. mytest1streaming432822asapbi).
* Wybieranie

  * ***Dane wejściowe*** tooview hello zapytania w danych wejściowych
  * ***ZAPYTANIE*** samą kwerendę hello tooview
  * ***GENERUJE*** tooview hello różnych danych wyjściowych

Informacji na temat tworzenia zapytań usługi Azure Stream Analytics można znaleźć w hello [Stream Analytics kwerendy odwołania](https://msdn.microsoft.com/library/azure/dn834998.aspx) w witrynie MSDN.

W tym rozwiązaniu hello Azure Stream Analytics zadania, które generuje się, że zestaw danych o niemal analiz w czasie rzeczywistym informacje o hello przychodzących danych strumienia tooa nawigacyjny usługi Power BI jest dostarczane jako część tego szablonu rozwiązania. Ponieważ nie istnieje niejawna wiedzą na temat formatu danych przychodzących hello, te zapytania musi toobe zmienione na podstawie Twojej formatu danych.

Witaj inne zadanie usługi analiza strumienia Azure Wyświetla wszystkie [Centrum zdarzeń](https://azure.microsoft.com/services/event-hubs/) zdarzenia [usługi Azure Storage](https://azure.microsoft.com/services/storage/) i dlatego wymaga informacji o zdarzeniu pełne hello jest przesyłane strumieniowo nie zmian niezależnie od formatu danych toostorage.

### <a name="azure-data-factory"></a>Azure Data Factory
Witaj [fabryki danych Azure](https://azure.microsoft.com/documentation/services/data-factory/) Usługa uruchamia przepływ hello i przetwarzania danych. W hello prognozowania żądanie danych hello szablon rozwiązania energii fabryki składa się z dwanaście [potoki](data-factory/data-factory-create-pipelines.md) czy przenoszenia i przetwarzania danych hello z użyciem różnych technologii.

  Dostępne fabrykę danych przez otwarcie węzła fabryki danych hello u dołu hello diagram szablon rozwiązania hello utworzone za pomocą wdrażania hello hello rozwiązania. Spowoduje to przejście możesz toohello fabryki danych w portalu zarządzania platformy Azure. Jeśli błędy są wyświetlane w obszarze zestawów danych, możesz zignorować te są one powodu fabryki toodata wdrażany przed hello generator danych zostało uruchomione. Te błędy nie uniemożliwiają działanie fabryką danych.

W tej sekcji omówiono konieczne hello [potoki](data-factory/data-factory-create-pipelines.md) i [działania](data-factory/data-factory-create-pipelines.md) zawartych w hello [fabryki danych Azure](https://azure.microsoft.com/documentation/services/data-factory/). Poniżej znajdują się w widoku diagramu hello hello rozwiązania.

![](media/cortana-analytics-technical-guide-demand-forecast/ADF2.png)

Zawiera pięć potoki hello tej fabryki [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) skrypty, które są używane toopartition i hello agregacji danych. Jeśli zaznaczono inaczej, skrypty hello będą znajdować się w hello [usługi Azure Storage](https://azure.microsoft.com/services/storage/) konto utworzone podczas instalacji. Ich lokalizacja będzie: demandforecasting\\\\skryptu\\\\hive\\ \\ (lub https://[Your name].blob.core.windows.net/demandforecasting rozwiązania).

Podobne toohello [Azure Stream Analytics](#azure-stream-analytics-1) zapytań, [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) skryptów ma niejawne informacji na temat hello przychodzące format danych, musi toobe zmienić te zapytania oparte na format danych i [Inżynieria](machine-learning/machine-learning-feature-selection-and-engineering.md) wymagania.

#### <a name="aggregatedemanddatato1hrpipeline"></a>*AggregateDemandDataTo1HrPipeline*
To [potoku](data-factory/data-factory-create-pipelines.md) potoku zawiera pojedyncze działanie - [HDInsightHive](data-factory/data-factory-hive-activity.md) działania przy użyciu [HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx) , na którym działa [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx)hello tooaggregate skryptu co 10 sekund strumieniowo żądanie danych na poziomie region poziomu toohourly podstacji i umieść w [usługi Azure Storage](https://azure.microsoft.com/services/storage/) przez zadanie usługi analiza strumienia Azure hello.

[Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) skryptów jest to zadanie partycjonowania ***AggregateDemandRegion1Hr.hql***

#### <a name="loadhistorydemanddatapipeline"></a>*LoadHistoryDemandDataPipeline*
To [potoku](data-factory/data-factory-create-pipelines.md) zawiera dwa działania:

* [HDInsightHive](data-factory/data-factory-hive-activity.md) działania przy użyciu [HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx) czy działa gałąź skryptów tooaggregate hello co godzinę żądanie dane historii w poziom region poziomu toohourly podstacji i umieścić w magazynie Azure podczas hello Azure Zadania usługi analiza strumienia
* [Kopiuj](https://msdn.microsoft.com/library/azure/dn835035.aspx) działanie, które przenosi hello zagregowanych danych z magazynu Azure blob toohello bazy danych SQL Azure udostępniony jako część instalacji szablon rozwiązania hello.

Witaj [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) skryptów dla tego zadania jest ***AggregateDemandHistoryRegion.hql***.

#### <a name="mlscoringregionxpipeline"></a>*MLScoringRegionXPipeline*
Te [potoki](data-factory/data-factory-create-pipelines.md) zawiera kilka działań i którego wynik końcowy jest hello oceniane prognoz z hello eksperymentu uczenia maszynowego Azure skojarzone z tym szablonem rozwiązania. Są one niemal identyczne, z wyjątkiem każdego z nich obsługuje tylko hello inny region, która jest wykonywana przez inną RegionID przekazywany w potoku ADF hello i hello skryptu hive dla każdego regionu.  
dostępne są następujące działania Hello zawarte w tym:

* [HDInsightHive](data-factory/data-factory-hive-activity.md) działania przy użyciu [HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx) czy działa gałąź skryptów tooperform agregacji i inżynieria niezbędne do hello eksperymentu uczenia maszynowego Azure. Witaj gałęzi dla tego zadania są odpowiednie ***PrepareMLInputRegionX.hql***.
* [Kopiuj](https://msdn.microsoft.com/library/azure/dn835035.aspx) działanie, które przenosi hello wyników z hello [HDInsightHive](data-factory/data-factory-hive-activity.md) działania tooa pojedynczego blob magazynu Azure możliwy dostęp hello [AzureMLBatchScoring](https://msdn.microsoft.com/library/azure/dn894009.aspx) działania.
* [AzureMLBatchScoring](https://msdn.microsoft.com/library/azure/dn894009.aspx) wyniki działania, która wywołuje hello eksperymentu uczenia maszynowego Azure, co powoduje hello dotyczy żądanie put w pojedynczego obiektu blob magazynu Azure.

#### <a name="copyscoredresultregionxpipeline"></a>*CopyScoredResultRegionXPipeline*
Te [potoki](data-factory/data-factory-create-pipelines.md) zawierać pojedyncze działanie - [kopiowania](https://msdn.microsoft.com/library/azure/dn835035.aspx) działanie, które przenosi hello wyniki hello eksperymentu uczenia maszynowego Azure z odpowiednich hello ***MLScoringRegionXPipeline *** toohello bazy danych SQL Azure udostępniony jako część instalacji szablon rozwiązania hello.

#### <a name="copyaggdemandpipeline"></a>*CopyAggDemandPipeline*
To [potoki](data-factory/data-factory-create-pipelines.md) zawierać pojedyncze działanie - [kopiowania](https://msdn.microsoft.com/library/azure/dn835035.aspx) działanie, które przenosi hello zagregowanych danych bieżące żądanie z ***LoadHistoryDemandDataPipeline*** toohello Azure Baza danych SQL, udostępniony jako część instalacji szablon rozwiązania hello.

#### <a name="copyregiondatapipeline-copysubstationdatapipeline-copytopologydatapipeline"></a>*CopyTopologyDataPipeline CopyRegionDataPipeline, CopySubstationDataPipeline,*
Te [potoki](data-factory/data-factory-create-pipelines.md) zawierać pojedyncze działanie - [kopiowania](https://msdn.microsoft.com/library/azure/dn835035.aspx) działania, który przenosi dane odwołanie hello z regionu/podstacji/Topologygeo, które są przekazywane tooAzure obiektu blob magazynu w ramach rozwiązania hello toohello instalacja szablonu usługi Azure SQL Database udostępniony jako część instalacji szablon rozwiązania hello.

### <a name="azure-machine-learning"></a>Azure Machine Learning
Witaj [usługi Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) eksperymentu używane dla ten szablon rozwiązania umożliwia prognozowanie hello żądanie regionu. eksperymentu Hello jest toohello określonego zestawu danych używane i dlatego wymaga modyfikacji lub wymiany danych toohello określonych w.

## <a name="monitor-progress"></a>**Monitoruj postęp**
Po uruchomieniu hello Generator danych, hello potoku rozpoczyna się tooget uwodniony i hello różnych składników rozwiązania start zasób do akcji następujące polecenia hello wystawiony przez hello fabryki danych. Istnieją dwa sposoby monitorowania hello potoku.

1. Sprawdzenie, czy hello dane z magazynu obiektów Blob Azure.

    Zapisuje jednego zadania usługi analiza strumienia hello hello raw przychodzące tooblob magazynu danych. Po kliknięciu **magazyn obiektów Blob Azure** składnik rozwiązania z hello ekranu zostanie pomyślnie wdrożono hello rozwiązania, a następnie kliknij przycisk **Otwórz** hello prawym panelu, spowoduje przejście toohello [Portalu zarządzania azure](https://portal.azure.com). Wyświetlonym edytorze kliknij na **obiekty BLOB**. W panelu dalej hello zostanie wyświetlona lista kontenerów. Polecenie **"energysadata"**. W panelu dalej hello, zobaczysz hello **"demandongoing"** folderu. W folderze rawdata hello zobaczysz folderów przy użyciu nazwy, takie jak Data = 2016-01-28 itp. Jeśli widzisz tych folderów wskazuje pomyślnie jest hello nieprzetworzone dane są generowane na komputerze i przechowywane w magazynie obiektów blob. Powinny pojawić się pliki, które powinny mieć ograniczone rozmiary MB w tych folderach.
2. Sprawdzenie, czy hello dane z bazy danych SQL Azure.

    Ostatnim krokiem Hello potoku hello jest toowrite danych (np. predykcje uzyskiwane z uczenia maszynowego) do bazy danych SQL. Toowait może mieć maksymalnie 2 godziny dla hello tooappear danych w bazie danych SQL. Jednym ze sposobów toomonitor jak dużo danych jest dostępne w bazie danych SQL jest za pośrednictwem [portalu zarządzania Azure](https://manage.windowsazure.com/). Zlokalizuj BAZ danych na lewym panelu hello![](media/cortana-analytics-technical-guide-demand-forecast/SQLicon2.png) i kliknij ją. Następnie odszukaj bazy danych (tj. demo123456db) i kliknij go. Na następnej stronie powitania w obszarze **"Connect tooyour baza danych"** kliknij **"Uruchom języka Transact-SQL zapytań dotyczących bazy danych SQL"**.

    W tym miejscu możesz kliknąć opcję Nowa kwerenda i zapytanie hello liczbę wierszy (np. "select count(*) z DemandRealHourly)" wraz z rozwojem bazy danych, hello liczbę wierszy w tabeli hello zwiększyć.)
3. Sprawdzenie, czy dane hello z pulpitu nawigacyjnego usługi Power BI.

    Można skonfigurować usługi Power BI aktywnej ścieżki pulpitu nawigacyjnego toomonitor hello przychodzących danych pierwotnych. Wykonaj hello instrukcji w sekcji "Power BI pulpitu nawigacyjnego" hello.

## <a name="power-bi-dashboard"></a>**Pulpit nawigacyjny programu Power BI**
### <a name="overview"></a>Omówienie
W tej sekcji opisano, jak tooset się toovisualize pulpit nawigacyjny usługi Power BI danych czasu rzeczywistego z platformy Azure strumieniowo analytics (ścieżka gorących), oraz jak prognozy wyników z usługi Azure machine learning (zimny ścieżki).

### <a name="setup-hot-path-dashboard"></a>Pulpit nawigacyjny aktywnej ścieżki Instalatora
następujące kroki Hello przeprowadzi Cię jak danych czasu rzeczywistego toovisualize dane wyjściowe z usługi analiza strumienia zadania, które zostały wygenerowane w czasie hello wdrożenia rozwiązania. A [online usługi Power BI](http://www.powerbi.com/) konto jest wymagane tooperform hello następujące kroki. Jeśli nie masz konta, możesz [utworzyć](https://powerbi.microsoft.com/pricing).

1. Dodawanie danych wyjściowych usługi Power BI w Azure Stream Analytics (ASA).

   * Konieczne będzie instrukcjami hello toofollow [Azure Stream Analytics & usługi Power BI: pulpitu nawigacyjnego analytics w czasie rzeczywistym uzyskać wgląd w czasie rzeczywistym przesyłać strumieniowo danych](stream-analytics/stream-analytics-power-bi-dashboard.md) tooset się hello wyjściowego zadania usługi analiza strumienia Azure jako zasilania Pulpit nawigacyjny analizy BIZNESOWEJ.
   * Znajdź zadania usługi analiza strumienia hello w Twojej [portalu zarządzania Azure](https://manage.windowsazure.com). Nazwa zadania hello Hello powinna być: YourSolutionName + streamingjob"" + losowe numer + "asapbi" (tj. demostreamingjob123456asapbi).
   * Dodawanie danych wyjściowych zadania ASA hello usługi Power BI. Zestaw hello **Alias wyjściowy** jako **"PBIoutput"**. Ustaw użytkownika **nazwę zestawu danych** i **Nazwa tabeli** jako **"EnergyStreamData"**. Po dodaniu danych wyjściowych powitania kliknij **"Start"** u dołu hello zadanie usługi Stream Analytics hello hello strony toostart. Należy pobrać potwierdzenia (*np.*, "Uruchamianie usługi analiza strumienia zadania myteststreamingjob12345asablob powiodło się.").
2. Zaloguj się za[online usługi Power BI](http://www.powerbi.com)

   * W lewej sekcji zestawów danych panelu w obszarze Mój obszar roboczy hello powinien być stanie toosee nowe przedstawiający zestawu danych na lewym panelu hello usługi Power BI. Jest to hello przesyłanie strumieniowe danych wypychana z usługi Azure Stream Analytics hello poprzedniego kroku.
   * Upewnij się, że hello ***wizualizacje*** okienko jest otwarty i jest wyświetlany na ekranie powitania po prawej stronie.
3. Utwórz kafelka "Żądanie przez sygnatura czasowa" hello:

   * Kliknij zestaw danych **"EnergyStreamData"** na powitania po lewej sekcji zestawów danych panelu.
   * Kliknij przycisk **"Wykres liniowy"** ikona ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic8.png).
   * Kliknij przycisk "EnergyStreamData" w **pola** panelu.
   * Kliknij przycisk **"Timestamp"** i upewnij się, że będzie wyświetlana w obszarze "Osi". Kliknij przycisk **"Obciążenia"** i upewnij się, że będzie wyświetlana w obszarze "Wartości".
   * Kliknij przycisk **ZAPISAĆ** hello górnej i nazwa raportu hello jako "EnergyStreamDataReport". Witaj raportu o nazwie "EnergyStreamDataReport" będą wyświetlane w raportach hello Navigator okienka po lewej stronie.
   * Kliknij przycisk **"Numer Pin Visual"** ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic6.png) ikonę w prawym górnym rogu ten wykres liniowy, okno "Numer Pin tooDashboard" może wyświetlani dla toochoose użytkownik pulpitu nawigacyjnego. Wybierz opcję "EnergyStreamDataReport", a następnie kliknij przycisk "Numer Pin".
   * Umieść kursor myszy hello za pośrednictwem tego kafelka na pulpicie nawigacyjnym powitania kliknij "Edytuj" ikonę w prawym górnym rogu toochange jego tytuł jako "Żądanie przez sygnatury czasowej"
4. Utwórz innych kafelka pulpitu nawigacyjnego oparte na odpowiednich zestawów danych. widok pulpitu nawigacyjnego końcowego Hello przedstawiono poniżej.
     ![](media/cortana-analytics-technical-guide-demand-forecast/PBIFullScreen.png)

### <a name="setup-cold-path-dashboard"></a>Pulpit nawigacyjny zimnych ścieżki Instalatora
Ścieżka zimnych danych potoku hello niezbędne celem jest Żądanie hello tooget prognozy każdego regionu. Usługa Power BI łączy tooan bazy danych Azure SQL jako źródła danych, w którym przechowywane są wyniki prognozowania hello.

> [!NOTE]
> 1) Zajmuje kilka godzin toocollect wystarczająco prognozy wyniki dla hello pulpitu nawigacyjnego. Zaleca się rozpocząć ten proces 2 do 3 godzin po biedzie hello generator danych. 2) w tym kroku hello warunkiem wstępnym jest toodownload i zainstaluj oprogramowanie bezpłatne hello [Power BI desktop](https://powerbi.microsoft.com/desktop).
>
>

1. Pobierz hello poświadczenia bazy danych.

   Konieczne będzie **bazy danych, nazwę serwera, nazwa bazy danych, nazwę użytkownika i hasło** przed przeniesieniem toonext czynności. Poniżej przedstawiono hello tooguide kroki należy jak toofind je.

   * Raz **"Azure SQL Database"** w szablonie rozwiązania włącza zielony diagramu, kliknij go, a następnie kliknij przycisk **"Otwórz"**. Będzie tooAzure z przewodnikiem portalu zarządzania i zostaną otwarte także strona informacji bazy danych.
   * Na stronie powitania można znaleźć sekcji "Baza danych". Wyświetla listę limit hello bazy danych, które zostały utworzone. Nazwa Hello bazy danych powinna być **"Z nazwą rozwiązania liczbę losową +"db""** (np. "mytest12345db").
   * Kliknij przycisk bazy danych, w nowej pop limit panelu, można znaleźć nazwę serwera bazy danych na górze hello hello. Nazwa serwera bazy danych powinna być **"Z nazwą rozwiązania liczbę losową +"database.windows.net,1433""** (np. "mytest12345.database.windows.net,1433").
   * Bazy danych **username** i **hasło** są hello tak samo jak hello nazwy użytkownika i hasła wcześniej zarejestrowane podczas wdrażania rozwiązania hello.
2. Aktualizacja źródła danych hello hello zimnych ścieżki pliku usługi Power BI

   * Upewnij się, że zainstalowano hello najnowszą wersję [Power BI desktop](https://powerbi.microsoft.com/desktop).
   * W hello **"DemandForecastingDataGeneratorv1.0"** pobrać folder, kliknij dwukrotnie pozycję hello **"Power BI Template\DemandForecastPowerBI.pbix"** pliku. wizualizacje początkowej Hello są oparte na danych zastępczego. **Uwaga:** Jeśli zostanie wyświetlony błąd massage, upewnij się, że zainstalowano najnowszą wersję hello Power BI Desktop.

     Po otwarciu u góry hello hello pliku, kliknij przycisk **"Edytuj zapytania"**. W hello pop okna, kliknij dwukrotnie **'Source'** na powitania prawym panelu.
     ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic1.png)
   * W hello pop okna, Zastąp **"Server"** i **"Baza danych"** z własne nazwy serwera i bazy danych, a następnie kliknij przycisk **"OK"**. Dla nazwy serwera, upewnij się, że Określ hello portu 1433 (**YourSolutionName.database.windows.net, 1433**). Ignoruj ostrzeżenia hello, które są wyświetlane na ekranie powitania.
   * W hello pop dalej w oknie, zobaczysz dwie opcje w okienku po lewej stronie powitania (**Windows** i **bazy danych**). Kliknij przycisk **"Baza danych"**, wypełnij Twojej **"Nazwa_użytkownika"** i **"Password"** (jest to hello nazwy użytkownika i hasła podczas najpierw wdrożyć rozwiązanie hello i utworzyć Baza danych Azure SQL). W ***wybierz poziom które tooapply te ustawienia mają być***, zaznacz opcję poziomu bazy danych. Następnie kliknij przycisk **"Połącz"**.
   * Po nawiązaniu połączenia z przewodnikiem toohello wstecz na poprzedniej stronie, zamknij okno hello. Wiadomość zostanie pop out — kliknij przycisk **Zastosuj**. Na koniec kliknij hello **zapisać** przycisk toosave hello zmiany. Plik usługi Power BI ma ustanowione połączenie toohello serwera. Jeśli Twoje wizualizacje są puste, upewnij się, że wyczyścić wszystkie dane hello wybór hello na powitania wizualizacje toovisualize klikając ikonę Gumka hello na powitania prawym górnym rogu hello legendy. Użyj hello odświeżania przycisk tooreflect nowe dane na powitania wizualizacji. Początkowo wyświetlany tylko hello inicjatora danych w sieci wizualizacji fabryki danych hello jest zaplanowane toorefresh co 3 godziny. Po 3 godziny zostanie wyświetlony nowy prognoz, które zostaną uwzględnione w sieci wizualizacji podczas odświeżania danych hello.
3. (Opcjonalnie) Publikowanie pulpitu nawigacyjnego zimnych ścieżki hello zbyt[online usługi Power BI](http://www.powerbi.com/). Należy pamiętać, że ten krok wymaga konta usługi Power BI (lub konta usługi Office 365).

   * Kliknij przycisk **"Publikuj"** i później kilku sekund zostanie wyświetlone okno wyświetlania "Publikowania tooPower BI sukcesu!" z zielonym znacznikiem wyboru. Kliknij łącze hello poniżej "Demoprediction.pbix Otwórz w usłudze Power BI". toofind szczegółowe instrukcje, zobacz [publikowania z Power BI Desktop](https://support.powerbi.com/knowledgebase/articles/461278-publish-from-power-bi-desktop).
   * toocreate nowego pulpitu nawigacyjnego: kliknij hello  **+**  zarejestrować dalej toothe **pulpity nawigacyjne** sekcji w okienku po lewej stronie powitania. Wprowadź nazwę hello "Żądanie prognozowania pokaz" dla tego nowego pulpitu nawigacyjnego.
   * Po otwarciu raportu powitania kliknij ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic6.png) toopin wszystkich na pulpicie nawigacyjnym tooyour wizualizacji. toofind szczegółowe instrukcje, zobacz [Przypnij do pulpitu nawigacyjnego usługi Power BI tooa kafelka z raportu](https://support.powerbi.com/knowledgebase/articles/430323-pin-a-tile-to-a-power-bi-dashboard-from-a-report).
     Przejdź do strony pulpitu nawigacyjnego toohello i dostosować hello rozmiar i położenie sieci wizualizacji i Edytuj ich tytułów. toofind szczegółowe instrukcje na tooedit Twojego Kafelki, zobacz temat [edycji kafelka — zmiany rozmiaru, Przenieś, Zmień nazwę, numer pin, usuwanie, Dodawanie hiperłącza](https://powerbi.microsoft.com/documentation/powerbi-service-edit-a-tile-in-a-dashboard/#rename). Oto pulpitu nawigacyjnego przykład z niektórych tooit wizualizacje przypięty zimnych ścieżki.

     ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic7.png)
4. (Opcjonalnie) Harmonogram odświeżania hello źródła danych.

   * tooschedule odświeżania danych hello, umieść kursor nad hello **końcowa EnergyBPI** zestawu danych, kliknij przycisk ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic3.png) , a następnie wybierz **planowanie odświeżania**.
     **Uwaga:** Jeśli widzisz Masaż ostrzeżenie, kliknij przycisk **edytowanie poświadczeń** i upewnij się, że poświadczenia bazy danych są hello takie same jak te opisane w kroku 1.

     ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic4.png)
   * Rozwiń węzeł hello **planowanie odświeżania** sekcji. Włącz funkcję "zachować aktualność danych".
   * Harmonogram odświeżania hello na podstawie Twoich potrzeb. toofind więcej informacji, zobacz [odświeżania danych w usłudze Power BI](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/).

## <a name="how-toodelete-your-solution"></a>**Jak toodelete rozwiązania**
Sprawdź, czy Zatrzymaj hello generator danych, gdy nie są aktywnie przy użyciu rozwiązania hello uruchamiania generatora danych hello będą naliczane wyższe koszty. Usuń hello rozwiązanie, jeśli nie są używane. Usunięcie rozwiązania spowoduje usunięcie wszystkich składników hello aprowizowane w Twojej subskrypcji po wdrożeniu rozwiązania hello. rozwiązanie hello toodelete kliknij swoją nazwę rozwiązania, w lewym panelu hello hello rozwiązania szablonu i kliknij delete.

## <a name="cost-estimation-tools"></a>**Narzędzia do szacowania kosztów**
Witaj następujące dwa narzędzia są dostępne toohelp lepiej zrozumieć całkowity koszt objętego uruchomiona hello prognozowania żądanie szablon rozwiązania energii w ramach subskrypcji:

* [Microsoft Azure koszt narzędzia do szacowania Tool (online)](https://azure.microsoft.com/pricing/calculator/)
* [Microsoft Azure koszt narzędzia do szacowania Tool (desktop)](http://www.microsoft.com/download/details.aspx?id=43376)

## <a name="acknowledgements"></a>**Potwierdzeń**
W tym artykule jest przypisany przez naukowca danych Yijing Chen i oprogramowania inżyniera min. Qiu firmy Microsoft.
