---
title: "Poznaj aaaDeep prognozowania vehicle kondycji i wspierającym zwyczaje - Azure | Dokumentacja firmy Microsoft"
description: "Korzystanie z możliwości hello wgląd w czasie rzeczywistym oraz predykcyjnej toogain Cortana Intelligence na kondycji vehicle i wspierającym zwyczaje."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d8866fa6-aba6-40e5-b3b3-33057393c1a8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: ba1448a5081762292561f904d9ec54617c9a5330
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook-deep-dive-into-hello-solution"></a>Vehicle telemetrii analizy rozwiązania podręcznikowym: nowości w hello rozwiązania
To **menu** toohello części tego podręcznika dotyczącego łączy: 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

Ta sekcja rozwija na każdym z etapów hello pokazana na powitania architektury rozwiązania wraz z instrukcjami i wskaźniki do dostosowania. 

## <a name="data-sources"></a>Źródła danych
rozwiązanie Hello używa dwóch różnych źródeł danych:

* **Symulowane sygnały vehicle i danych diagnostycznych** i 
* **vehicle katalogu**

Symulator telematyki vehicle wchodzi w skład tego rozwiązania. Emituje informacje diagnostyczne, a sygnały odpowiadający mu stan toohello hello vehicle i toohello zwiększają wzorca w danym punkcie w czasie. Kliknij przycisk [symulatora telematyki Vehicle](http://go.microsoft.com/fwlink/?LinkId=717075) toodownload hello **Vehicle telematyki symulatora rozwiązania Visual Studio** dostosowań, w zależności od wymagań. katalog vehicle Hello zawiera odwołanie do zestawu danych z mapowaniem toomodel VIN.

![Symulator telematyki vehicle](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig1-vehicle-telematics-simulator.png)

*Rysunek 1 — Vehicle telematyki symulatora*

Jest to formacie JSON zestawu danych zawierającego powitania po schematu.

| Kolumna | Opis | Wartości |
| --- | --- | --- |
| VIN |Losowo generowany numer identyfikacyjny |To są uzyskiwane ze wzorca listę 10 000 numery identyfikacyjne losowo generowany pojazdów. |
| Poza temperatury |Witaj poza temperatury gdzie sterujące hello vehicle |Losowo generowany numer od 0 do 100 |
| Aparat temperatury |Witaj aparat temperatury pojazdów hello |Losowo generowany numer od 0-500 |
| Szybkość |szybkość aparat Hello na które hello sterujące vehicle |Losowo generowany numer od 0 do 100 |
| Paliwa |poziom paliwa Hello pojazdów hello |Losowo generowany numer od 0 do 100 (procent poziomu paliwa wskazuje) |
| EngineOil |Witaj aparatu wydobycie ropy naftowej pojazdów hello |Losowo generowany numer od 0 do 100 (procent poziomu wydobycie ropy naftowej aparat oznacza) |
| Opona wykorzystania |Witaj opona wykorzystania pojazdów hello |Losowo generowany numer 50 0 (wskazuje procent poziomu wykorzystania opona) |
| Licznika |Odczytywanie licznika Hello hello vehicle |Losowo generowany numer od 0 200000 |
| Accelerator_pedal_position |Pozycja szkła akceleratora Hello pojazdów hello |Losowo generowany numer od 0 do 100 (procent poziomu akceleratora wskazuje) |
| Parking_brake_status |Wskazuje, czy hello vehicle jest stoi lub nie |Wartość PRAWDA lub FAŁSZ |
| Headlamp_status |Wskazuje, gdzie reflektor hello jest na lub nie |Wartość PRAWDA lub FAŁSZ |
| Brake_pedal_status |Wskazuje, czy pedał hamulca hello zostanie naciśnięty, czy nie |Wartość PRAWDA lub FAŁSZ |
| Transmission_gear_position |Pozycja koło zębate transmisji Hello pojazdów hello |Stan: najpierw drugie, trzecie czwarty, piąte, szóstego, siódme, kolejnego, ósmego |
| Ignition_status |Wskazuje, czy hello vehicle jest uruchomiona lub zatrzymana |Wartość PRAWDA lub FAŁSZ |
| Windshield_wiper_status |Wskazuje, czy Wycieraczka szyby hello jest wyłączone lub nie |Wartość PRAWDA lub FAŁSZ |
| ABS |Wskazuje, czy ABS prowadzi lub nie |Wartość PRAWDA lub FAŁSZ |
| Znacznik czasu |Witaj sygnatury czasowej po utworzeniu hello punktu danych. |Date |
| Miasto |Lokalizacja Hello pojazdów hello |4 miejscowości, w tym rozwiązaniu: Bellevue, Redmond, Sammamish, Seattle |

Hello vehicle modelu odwołanie dataset zawiera mapowania modelu toohello VIN. 

| VIN | Model |
| --- | --- |
| FHL3O1SA4IEHB4WU1 |Limuzyna |
| 8J0U8XCPRGW4Z3NQE |Połączenie hybrydowe |
| WORG68Z2PLTNZDBI7 |Rodziny zamknięte |
| JTHMYHQTEPP4WBMRN |Limuzyna |
| W9FTHG27LZN1YWO0Y |Połączenie hybrydowe |
| MHTP9N792PHK08WJM |Rodziny zamknięte |
| EI4QXI2AXVQQING4I |Limuzyna |
| 5KKR2VB4WHQH97PF8 |Połączenie hybrydowe |
| W9NSZ423XZHAONYXB |Rodziny zamknięte |
| 26WJSGHX4MA5ROHNL |Możliwe do przekonwertowania |
| GHLUB6ONKMOSI7E77 |Kombi |
| 9C2RHVRVLMEJDBXLP |Samochód kompaktowy |
| BRNHVMZOUJ6EOCP32 |Mała SUV |
| VCYVW0WUZNBTM594J |Samochodu sportowych |
| HNVCE6YFZSA5M82NY |Średnia SUV |
| 4R30FOR7NUOBL05GJ |Kombi |
| WYNIIY42VKV6OQS1J |Duże SUV |
| 8Y5QKG27QET1RBK7I |Duże SUV |
| DF6OX2WSRA6511BVG |Coupe |
| Z2EOZWZBXAEW3E60T |Limuzyna |
| M4TV6IEALD5QDS3IR |Połączenie hybrydowe |
| VHRA1Y2TGTA84F00H |Rodziny zamknięte |
| R0JAUHT1L1R3BIKI0 |Limuzyna |
| 9230C202Z60XX84AU |Połączenie hybrydowe |
| T8DNDN5UDCWL7M72H |Rodziny zamknięte |
| 4WPYRUZII5YV7YA42 |Limuzyna |
| D1ZVY26UV2BFGHZNO |Połączenie hybrydowe |
| XUF99EW9OIQOMV7Q7 |Rodziny zamknięte |
| 8OMCL3LGI7XNCC21U |Możliwe do przekonwertowania |
| ……. | |

### <a name="references"></a>Dokumentacja
[Rozwiązanie programu Visual Studio symulatora telematyki vehicle](http://go.microsoft.com/fwlink/?LinkId=717075) 

[Centrum zdarzeń platformy Azure](https://azure.microsoft.com/services/event-hubs/)

[Azure Data Factory](https://azure.microsoft.com/documentation/learning-paths/data-factory/)

## <a name="ingestion"></a>Wprowadzanie
Kombinacje Azure Event Hubs, Stream Analytics i fabryki danych są wykorzystywane tooingest hello vehicle sygnałów, hello zdarzeń diagnostycznych, w czasie rzeczywistym i partii analytics. Wszystkie te składniki są tworzone i skonfigurowany jako część hello wdrażania rozwiązania. 

### <a name="real-time-analysis"></a>Analiza w czasie rzeczywistym
Witaj zdarzenia generowane przez hello Vehicle telematyki symulatora są publikowane za pomocą Centrum zdarzeń toohello hello SDK Centrum zdarzeń. Zadanie usługi Stream Analytics Hello wysyła strumień te zdarzenia z hello Centrum zdarzeń i danych w czasie rzeczywistym tooanalyze hello vehicle kondycji hello procesów. 

![Pulpit nawigacyjny Centrum zdarzeń](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig4-vehicle-telematics-event-hub-dashboard.png) 

*Rysunek 4 - pulpit nawigacyjny Centrum zdarzeń*

![Dane przetwarzania zadania usługi analiza strumienia](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig5-vehicle-telematics-stream-analytics-job-processing-data.png) 

*Rysunek 5. zadania usługi analiza strumienia przetwarzania danych*

zadanie Stream Analytics Hello;

* wysyła strumień danych z hello Centrum zdarzeń 
* wykonuje sprzężenie z hello odwołanie toomap hello vehicle VIN toohello odpowiedni model danych 
* są utrwalane w magazynie obiektów blob platformy Azure dla analizach wsadowych sformatowanego. 

powitania po zapytań usługi Stream Analytics jest używane toopersist hello dane do magazynu obiektów blob platformy Azure. 

![Zapytanie dotyczące zadań analizy strumienia dla wprowadzanie danych](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig6-vehicle-telematics-stream-analytics-job-query-for-data-ingestion.png) 

*Rysunek 6 - analiza strumienia zadania zapytania na wprowadzanie danych*

### <a name="batch-analysis"></a>Analiza partii
Możemy również generowania woluminów sygnały symulowane vehicle i diagnostycznych zestawu danych dla bardziej zaawansowane funkcje analizy partii. Jest to wymagane tooensure wolumin danych reprezentatywnych dla przetwarzania wsadowego. W tym celu używamy potoku o nazwie "PrepareSampleDataPipeline" w toogenerate przepływu pracy fabryki danych Azure hello wartość jednego roku sygnały symulowane vehicle i zestawu danych diagnostycznych. Kliknij przycisk [działania niestandardowego fabryki danych](http://go.microsoft.com/fwlink/?LinkId=717077) toodownload hello niestandardowego działania DotNet rozwiązania Visual Studio dla dostosowania fabryki danych zgodnie z wymaganiami. 

![Przygotowanie przykładowych danych do przepływu pracy przetwarzania wsadowego](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig7-vehicle-telematics-prepare-sample-data-for-batch-processing.png) 

*Rysunek 7 — przygotowanie przykładowych danych do przepływu pracy przetwarzania wsadowego*

potok Hello składa się z niestandardowych .net ADF działania, Pokaż tutaj:

![Działanie PrepareSampleDataPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig8-vehicle-telematics-prepare-sample-data-pipeline.png) 

*Rysunek 8 - PrepareSampleDataPipeline*

Po potoku hello wykonuje pomyślnie i zestawu danych "RawCarEventsTable" jest oznaczona jako "Gotowe", jednego roku warto symulowane vehicle sygnałów oraz diagnostyki danych są tworzone. Zobacz następujące hello utworzone na Twoim koncie magazynu w kontenerze "connectedcar" hello plików i folderów:

![Dane wyjściowe PrepareSampleDataPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig9-vehicle-telematics-prepare-sample-data-pipeline-output.png) 

*Rysunek 9 - PrepareSampleDataPipeline danych wyjściowych*

### <a name="references"></a>Dokumentacja
[Azure SDK Centrum zdarzeń pozyskiwania strumieni](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

[Możliwości przenoszenia danych fabryki danych platformy Azure](../data-factory/data-factory-data-movement-activities.md)
[działania DotNet fabryki danych Azure](../data-factory/data-factory-use-custom-activities.md)

[Rozwiązanie programu visual studio działania DotNet fabryki danych Azure przygotowania przykładowe dane](http://go.microsoft.com/fwlink/?LinkId=717077) 

## <a name="partition-hello-dataset"></a>Zestaw danych hello partycji
sygnały raw vehicle częściowo ustrukturyzowanych Hello i zestawu danych diagnostycznych są dzielone w kroku przygotowania danych hello na format rok i miesiąc. Tym partycjonowanie wspiera efektywniejsze wykonywanie zapytania i skalowalności magazynu długoterminowego przez włączenie błędów w tryb failover z jednego obiektu blob konta toohello obok jako pierwsze konto hello wypełnia. 

>[!NOTE] 
>Ten krok w rozwiązaniu hello jest stosowane tylko toobatch przetwarzania.

Wejście i wyjście danych zarządzania danymi:

* Witaj **dane wyjściowe** (etykietą *PartitionedCarEventsTable*) toobe pozostaje długi okres czasu jako formularz podstawowych / "rawest" hello danych w powitania klienta "Data Lake". 
* Witaj **dane wejściowe** potoku toothis zwykle będą usunięte, ponieważ dane wyjściowe hello ma toohello pełnej rozdzielczości danych wejściowych — wystarczy znajduje (podzielona na partycje) lepiej dla dalszego wykorzystania.

![Przepływ pracy zdarzenia samochodu partycji](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig10-vehicle-telematics-partition-car-events-workflow.png)

*Rysunek 10 — przepływ pracy zdarzenia samochodu partycji*

dane pierwotne Hello jest podzielona na partycje przy użyciu działania Hive HDInsight w "PartitionCarEventsPipeline". ROK i miesiąc partycjonowanego Hello przykładowych danych wygenerowanych w kroku 1 rok. partycje Hello są używane toogenerate vehicle sygnały i danych diagnostycznych dla każdego miesiąca roku (całkowita liczba partycji 12). 

![Działanie PartitionCarEventsPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig11-vehicle-telematics-partition-car-events-pipeline.png)

*Rysunek 11 — PartitionCarEventsPipeline*

***Skryptu PartitionConnectedCarEvents Hive***

Witaj poniższy skrypt Hive, o nazwie "partitioncarevents.hql" służy do partycjonowania i znajduje się w folderze "\demo\src\connectedcar\scripts" hello zip hello pobrane. 
    
    SET hive.exec.dynamic.partition=true;
    SET hive.exec.dynamic.partition.mode = nonstrict;
    set hive.cli.print.header=true;

    DROP TABLE IF EXISTS RawCarEvents; 
    CREATE EXTERNAL TABLE RawCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:RAWINPUT}'; 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string
    ) partitioned by (YearNo int, MonthNo int) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDOUTPUT}';

    DROP TABLE IF EXISTS Stage_RawCarEvents; 
    CREATE TABLE IF NOT EXISTS Stage_RawCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string,
                YearNo                             int,
                MonthNo                         int) 
    ROW FORMAT delimited fields terminated by ',' LINES TERMINATED BY '10';

    INSERT OVERWRITE TABLE Stage_RawCarEvents
    SELECT
        vin,            
        model,
        timestamp,
        outsidetemperature,
        enginetemperature,
        speed,
        fuel,
        engineoil,
        tirepressure,
        odometer,
        city,
        accelerator_pedal_position,
        parking_brake_status,
        headlamp_status,
        brake_pedal_status,
        transmission_gear_position,
        ignition_status,
        windshield_wiper_status,
        abs,
        gendate,
        Year(gendate),
        Month(gendate)

    FROM RawCarEvents WHERE Year(gendate) = ${hiveconf:Year} AND Month(gendate) = ${hiveconf:Month}; 

    INSERT OVERWRITE TABLE PartitionedCarEvents PARTITION(YearNo, MonthNo) 
    SELECT
        vin,            
        model,
        timestamp,
        outsidetemperature,
        enginetemperature,
        speed,
        fuel,
        engineoil,
        tirepressure,
        odometer,
        city,
        accelerator_pedal_position,
        parking_brake_status,
        headlamp_status,
        brake_pedal_status,
        transmission_gear_position,
        ignition_status,
        windshield_wiper_status,
        abs,
        gendate,
        YearNo,
        MonthNo
    FROM Stage_RawCarEvents WHERE YearNo = ${hiveconf:Year} AND MonthNo = ${hiveconf:Month};

Po pomyślnym wykonaniu potoku hello zapoznaj się hello następujące partycje generowane na koncie magazynu w kontenerze "connectedcar" hello.

![Dane wyjściowe podzielonym na partycje](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig12-vehicle-telematics-partitioned-output.png)

*Rysunek 12 — partycjonowanej danych wyjściowych*

dane Hello jest zoptymalizowane, jest bardziej łatwe w zarządzaniu i gotowa do dalszego przetwarzania toogain partii bogate informacje na temat technologii. 

## <a name="data-analysis"></a>Analiza danych
W tej sekcji, zobaczysz, jak zaawansowane toocombine Azure Stream Analytics, usługi Azure Machine Learning fabryki danych Azure i usłudze Azure HDInsight dla zaawansowanej analizy kondycji vehicle i wspierającym zwyczaje. Istnieją trzy podpunkty tutaj:

1. **Machine Learning**: ta podsekcja zawiera informacje na temat hello eksperymentu wykrywania anomalii, użytymi w tym pojazdów toopredict rozwiązania wymagające obsługi konserwacji i pojazdów odwołania powodu toosafety problemy wymagające.
2. **W czasie rzeczywistym analizy**: ta podsekcja zawiera informacje dotyczące analiz w czasie rzeczywistym hello przy użyciu hello język zapytań usługi analiza strumienia i operacyjnych uczenia maszynowego hello eksperymentu w czasie rzeczywistym za pomocą aplikacji niestandardowej.
3. **Partii analizy**: ta podsekcja zawiera informacje dotyczące hello, przekształcanie i przetwarzania danych partii hello przy użyciu usługi Azure HDInsight i usługi Azure Machine Learning operationalized przez fabryki danych Azure.

### <a name="machine-learning"></a>Usługa Machine Learning
Naszym celem jest pojazdów hello toopredict, które wymagają konserwacji lub wycofania oparte na niektórych statystyki kondycji. Wykonujemy powitania po założenia

* Jeśli jeden z hello następujące trzy warunki są spełnione, wymagają pojazdów hello **obsługi konserwacji**:
  
  * Brakuje opona wykorzystania
  * Brakuje wydobycie ropy naftowej aparatu
  * Aparat temperatury jest wysoka
* Jeśli jeden z hello następujące warunki są spełnione, może być pojazdów hello **problem bezpieczeństwa** i wymagają **odwołania**:
  
  * Aparat temperatury jest wysoka, ale brakuje poza temperatury
  * Aparat temperatury jest niska, ale poza temperatury jest wysoka

Na podstawie hello poprzedniej wymagań, został utworzony dwóch osobnych modeli toodetect anomalii: jeden vehicle obsługi wykrywania i jeden do wykrywania odwołania pojazdów. W obu tych modeli hello wbudowanych algorytm analizy składnik główny (PCA) służy do wykrywania anomalii. 

**Model wykrywania konserwacji**

Jeśli jeden z trzech wskaźniki opona wykorzystania, aparat wydobycie ropy naftowej lub temperatury aparat — spełniał stanu odpowiednich, model wykrywania konserwacji hello raporty anomalii. W związku z tym tylko potrzebujemy tooconsider te trzy zmienne w budynku hello modelu. W naszym eksperymentu w usłudze Azure Machine Learning, najpierw używamy **Select Columns in Dataset** tooextract modułu tych trzech zmiennych. Następnie użyć hello anomalii oparte na PCA wykrywania modułu toobuild hello anomalii wykrywania modelu. 

Podmiot zabezpieczeń składnika analiza (PCA) to technikę ustalonych w uczeniu maszynowym, które mogą być zastosowane toofeature zaznaczenia, klasyfikacji i anomalii wykrywania. PCA Konwertuje zestaw przypadku zawierającego prawdopodobnie skorelowane zmienne, do wartości o nazwie główne składniki. Hello klucza informacje o tym, na podstawie PCA modelowania jest tooproject danych na małe wymiarowej miejsca, aby funkcje i anomalie, można łatwiej zidentyfikować.

Dla każdego nowego wprowadzania hello zbyt model wykrywania, wykrywanie anomalii hello najpierw oblicza swojej projekcji na powitania eigenvectors, a następnie oblicza hello znormalizowany błąd odbudowy. Ten błąd znormalizowane jest hello anomalii wynik. Hello wyższej hello błąd hello więcej nietypowe wystąpienia hello jest. 

Hello obsługi wykrywania problem każdy rekord jest uznawana za ustalony punktu 3-wymiarową przestrzeni opona wykorzystania, aparat wydobycie ropy naftowej i temperatury aparat współrzędnych. toocapture tych nieprawidłowości możemy projektu hello oryginalne dane przestrzeni 3-wymiarową hello na 2-wymiarową miejsca, przy użyciu PCA. W związku z tym możemy ustawić parametr hello liczby składników toouse w PCA toobe 2. Ten parametr odgrywa ważną rolę w stosowaniu wykrywania anomalii oparte na PCA. Po zakończeniu operacji przewidywania danych przy użyciu PCA możemy łatwiej ustalić tych nieprawidłowości.

**Model wykrywania anomalii odwołania** w model wykrywania anomalii odwołania hello używamy hello Select Columns in Dataset i anomalii oparte na PCA modułów wykrywania w podobny sposób. W szczególności firma Microsoft najpierw wyodrębnić trzy zmienne - temperatury aparatu, poza temperatury i szybkość — przy użyciu hello **Select Columns in Dataset** modułu. Przeprowadzamy szybkości hello zmiennej, ponieważ temperatury aparat hello jest zwykle skorelowane toohello szybkości. Następnie używamy anomalii oparte na PCA wykrywania modułu tooproject hello danych z 3-wymiarową obszaru hello do 2-wymiarowej. Hello odwołania kryteriami i hello vehicle wymaga odwołania gdy aparat temperatury i poza temperatury wysokiej negatywnie skorelowane. Za pomocą algorytmu wykrywania anomalii oparte na PCA, firma Microsoft przechwytywać anomalie hello po wykonaniu PCA. 

Podczas uczenia modelu albo, potrzebujemy danych normalne toouse, które nie wymagają konserwacji lub wycofania jako model wykrywania anomalii oparte na PCA hello tootrain hello danych wejściowych. W hello oceniania eksperymentu używamy toodetect model wykrywania anomalii hello uczony czy hello vehicle wymaga konserwacji lub wycofania. 

### <a name="real-time-analysis"></a>Analiza w czasie rzeczywistym
następujące zapytanie SQL Stream Analytics Hello jest używany tooget średnią hello wszystkich hello ważny parametry, takie jak prędkość, poziom paliwa temperatury aparatu, odczytu licznika, opona wykorzystania, aparatu wydobycie ropy naftowej i inne. Witaj średnie są używane toodetect anomalii, wydawania alertów i określić hello ogólnej kondycji warunki pojazdów obsługiwane w określonym regionie i skorelowania go po toodemographics. 

![Stream Analytics zapytania do przetworzenia w czasie rzeczywistym](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig13-vehicle-telematics-stream-analytics-query-for-real-time-processing.png)

*Rysunek 13 — zapytań usługi Stream Analytics do przetworzenia w czasie rzeczywistym*

Wszystkie średnie hello są obliczane przez TumblingWindow 3 sekundy. Użyto TubmlingWindow w takim przypadku ponieważ wymagamy przedziały czasu nienakładający, jak i ciągłe. 

Kliknij toolearn więcej informacji na temat wszystkie funkcje "Okien" hello, w systemie Azure Stream Analytics [okien (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835019.aspx).

**Prognozowanie w czasie rzeczywistym**

Aplikacja jest częścią modelu uczenia maszynowego hello toooperationalize rozwiązania hello w czasie rzeczywistym. Ta aplikacja o nazwie "RealTimeDashboardApp" zostało utworzone i skonfigurowane jako część wdrożenia rozwiązania hello. Aplikacja Hello wykonuje następujące hello:

1. Wykrywa tooan Centrum zdarzeń wystąpienia których Stream Analytics jest publikowania hello zdarzeń we wzorcu stale. ![Stream Analytics zapytania do publikowania danych hello](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig14-vehicle-telematics-stream-analytics-query-for-publishing.png) *rysunek 14 — zapytań usługi Stream Analytics publikowania hello tooan danych wyjściowych Centrum zdarzeń wystąpienia* 
2. Dla każdego zdarzenia, które otrzymuje tej aplikacji: 
   
   * Procesy hello danych przy użyciu punktu końcowego Machine Learning żądań i odpowiedzi oceniania (RR). punkt końcowy RR Hello jest automatycznie publikowany jako część wdrożenia hello.
   * dane wyjściowe RR Hello jest wypychania hello interfejsów API usługi Power BI tooa opublikowanych w zestawie danych.

Ten wzorzec jest również tooscenarios dotyczy mają toointegrate aplikacji biznesowych (LoB), z przepływem analiz w czasie rzeczywistym hello, dla scenariuszy, takich jak alerty, powiadomienia i wiadomości.

Kliknij przycisk [pobierania RealtimeDashboardApp](http://go.microsoft.com/fwlink/?LinkId=717078) hello toodownload RealtimeDashboardApp rozwiązania Visual Studio dostosowań. 

**Witaj tooexecute w czasie rzeczywistym pulpitu nawigacyjnego aplikacji**
1. Wyodrębnij i Zapisz lokalnie ![folderu RealtimeDashboardApp](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig16-vehicle-telematics-realtimedashboardapp-folder.png) *rysunek 16 – RealtimeDashboardApp folderu*  
2. Uruchom aplikację hello RealtimeDashboardApp.exe
3. Podaj prawidłowe poświadczenia usługi Power BI, zaloguj się i kliknij przycisk Akceptuj ![W czasie rzeczywistym pulpit nawigacyjny aplikacji logowania tooPower analizy Biznesowej](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17a-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) ![Logowania tooPower BI Zakończ w czasie rzeczywistym pulpitu nawigacyjnego aplikacji](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17b-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) 

*Rysunek 17 — RealtimeDashboardApp: Logowania tooPower analizy Biznesowej*

>[!NOTE] 
>Zestaw danych usługi Power BI hello tooflush należy wykonać hello RealtimeDashboardApp z parametrem "flushdata" hello: 

    RealtimeDashboardApp.exe -flushdata


### <a name="batch-analysis"></a>Analiza partii
Celem Hello jest tooshow jak Motors Contoso używa hello obliczeń platformy Azure możliwości tooharness danych big data toogain szczegółowe, bogate informacje na wzorzec, zachowanie użycia i kondycji pojazdów. Dzięki temu możliwe:

* Udoskonalanie powitania klienta i zapewnić ich tańsze zapewniając wgląd na zwyczaje i wydajne zachowania pobudzenie paliwa
* Dowiedz się więcej o klientów i ich pobudzenie decyzje biznesowe toogovern patters aktywnego i podaj hello najlepiej w klasie produktów i usług

W tym rozwiązaniu możemy przeznaczonych hello następujące metryki:

1. **Agresywna zwiększają zachowanie**: identyfikuje trend hello hello modeli, lokalizacje pobudzenie warunki i czas hello roku toogain wgląd w bliskiej schematy. Silniki contoso można używać tych insights kampanii marketingowych, nowe funkcje spersonalizowane i ubezpieczenia opartej na użyciu.
2. **Paliwa wydajne działanie pobudzenie**: identyfikuje trend hello hello modeli, lokalizacje pobudzenie warunki i czas hello roku toogain rozeznanie wydajne schematy paliwa. Silniki contoso można używać tych insights kampanii, zwiększają nowe funkcje i aktywne raportowania toohello sterowniki kosztów obowiązującej oraz środowisko przyjazne zwyczaje jazdy. 
3. **Odwołaj modele**: identyfikuje modele wymagających odwołań przez operacyjnych hello eksperymentu uczenia maszynowego wykrywania anomalii

Oto do hello szczegóły każdego z tych metryk

**Agresywne pobudzenie wzorca**

Hello sygnały vehicle podzielona na partycje i danych diagnostycznych są przetwarzane w potoku hello o nazwie "AggresiveDrivingPatternPipeline" przy użyciu modeli hello toodetermine Hive, lokalizacji, vehicle, zwiększają warunki oraz innych parametrów, które wykazuje aktywnego wzorzec jazdy.

![Agresywne pobudzenie przepływu pracy wzorzec](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig18-vehicle-telematics-aggressive-driving-pattern.png) 
*rysunek 18 — agresywne pobudzenie przepływu pracy wzorca*


***Agresywne kierowania zapytań Hive wzorca***

Hello skryptu Hive o nazwie "aggresivedriving.hql" używany do analizowania aktywnego wzorca warunku jazdy znajduje się w folderze "\demo\src\connectedcar\scripts" hello pobrane zip. 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDINPUT}';

    DROP TABLE IF EXISTS CarEventsAggresive; 
    CREATE EXTERNAL TABLE CarEventsAggresive
    (
                   vin                         string, 
                model                        string,
                timestamp                    string,
                city                        string,
                speed                          string,
                transmission_gear_position    string,
                brake_pedal_status            string,
                Year                        string,
                Month                        string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:AGGRESIVEOUTPUT}';



    INSERT OVERWRITE TABLE CarEventsAggresive
    select
    vin,
    model,
    timestamp,
    city,
    speed,
    transmission_gear_position,
    brake_pedal_status,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from PartitionedCarEvents
    where transmission_gear_position IN ('fourth', 'fifth', 'sixth', 'seventh', 'eight') AND brake_pedal_status = '1' AND speed >= '50'


Używa kombinacji hello vehicle w pozycji koło zębate transmisji, hamulca szkła stanu i szybkość toodetect reckless/agresywne zwiększają działanie hamowania wzorzec dużą prędkością. 

Po pomyślnym wykonaniu potoku hello zapoznaj się hello następujące partycje generowane na koncie magazynu w kontenerze "connectedcar" hello.

![Dane wyjściowe AggressiveDrivingPatternPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-aggressive-driving-pattern-output.png) 

*Rysunek 19 — AggressiveDrivingPatternPipeline danych wyjściowych*

**Efektywne wzorzec pobudzenie paliwa**

Hello sygnały vehicle podzielona na partycje i danych diagnostycznych są przetwarzane w potoku hello o nazwie "FuelEfficientDrivingPatternPipeline". Gałąź jest używane toodetermine hello modeli, lokalizacji vehicle, pobudzenie warunki i inne właściwości, które wykazują paliwa wydajne pobudzenie wzorca.

![Wzorzec pobudzenie obniżające zużycie paliwa](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-fuel-efficient-driving-pattern.png) 

*Rysunek 20 – obniżające zużycie paliwa pobudzenie przepływu pracy wzorca*

***Paliwa wydajne pobudzenie wzorzec zapytań Hive***

Hello skryptu Hive o nazwie "fuelefficientdriving.hql" używany do analizowania aktywnego wzorca warunku jazdy znajduje się w folderze "\demo\src\connectedcar\scripts" hello pobrane zip. 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDINPUT}';

    DROP TABLE IF EXISTS FuelEfficientDriving; 
    CREATE EXTERNAL TABLE FuelEfficientDriving
    (
                   vin                         string, 
                model                        string,
                   city                        string,
                speed                          string,
                transmission_gear_position    string,                
                brake_pedal_status            string,            
                accelerator_pedal_position    string,                             
                Year                        string,
                Month                        string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:FUELEFFICIENTOUTPUT}';



    INSERT OVERWRITE TABLE FuelEfficientDriving
    select
    vin,
    model,
    city,
    speed,
    transmission_gear_position,
    brake_pedal_status,
    accelerator_pedal_position,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from PartitionedCarEvents
    where transmission_gear_position IN ('fourth', 'fifth', 'sixth', 'seventh', 'eight') AND parking_brake_status = '0' AND brake_pedal_status = '0' AND speed <= '60' AND accelerator_pedal_position >= '50'


Wykorzystuje kombinację hello vehicle w pozycji koło zębate transmisji, stan szkła hamulca szybkość i paliwa toodetect szkła pozycji akceleratora wydajne działanie pobudzenie oparte na przyspieszenie hamowania, oraz przyspieszyć wzorce. 

Po pomyślnym wykonaniu potoku hello zapoznaj się hello następujące partycje generowane na koncie magazynu w kontenerze "connectedcar" hello.

![Dane wyjściowe FuelEfficientDrivingPatternPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig20-vehicle-telematics-fuel-efficient-driving-pattern-output.png) 

*Rysunek 21 — FuelEfficientDrivingPatternPipeline danych wyjściowych*

**Operacje przewidywania dla odwołania**

eksperymentu uczenia maszynowego Hello jest udostępniane i opublikowane jako usługi sieci web jako część wdrożenia rozwiązania hello. Witaj wsadowego oceniania punkt końcowy jest wykorzystywana w tym przepływie pracy, zarejestrowany jako usługa połączone fabryki danych i operationalized przy użyciu danych fabryki działanie wsadowego oceniania.

![Punkt końcowy Machine Learning](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig21-vehicle-telematics-machine-learning-endpoint.png) 

*Rysunek 22 — punktu końcowego uczenia maszynowego zarejestrowany jako połączonej usługi z fabryki danych*

Witaj zarejestrowanej połączonej usługi jest używany w hello DetectAnomalyPipeline tooscore hello danych przy użyciu modelu wykrywania anomalii hello. 

![Learning działanie wsadowego oceniania w fabryce danych komputera](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig22-vehicle-telematics-aml-batch-scoring.png) 

*Rysunek 23 — działanie usługi Azure Machine Learning wsadowego oceniania z fabryki danych* 

Istnieje kilka czynności wykonywanych w tym potoku w celu przygotowania danych, dzięki czemu mogą być operationalized z hello wsadowego oceniania usługi sieci web. 

![DetectAnomalyPipeline do prognozowania pojazdów wymagających odwołań](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig23-vehicle-telematics-pipeline-predicting-recalls.png) 

*Rysunek 24 — DetectAnomalyPipeline do prognozowania pojazdów wymagających odwołań* 

***Zapytanie Hive wykrywania anomalii***

Po zakończeniu oceniania hello działanie HDInsight jest używane tooprocess i hello agregacji danych, które są sklasyfikowane jako anomalii przez model hello wynik prawdopodobieństwa: 0,60 lub nowszego.

    DROP TABLE IF EXISTS CarEventsAnomaly; 
    CREATE EXTERNAL TABLE CarEventsAnomaly 
    (
                vin                            string,
                model                        string,
                gendate                        string,
                outsidetemperature            string,
                enginetemperature            string,
                speed                        string,
                fuel                        string,
                engineoil                    string,
                tirepressure                string,
                odometer                    string,
                city                        string,
                accelerator_pedal_position    string,
                parking_brake_status        string,
                headlamp_status                string,
                brake_pedal_status            string,
                transmission_gear_position    string,
                ignition_status                string,
                windshield_wiper_status        string,
                abs                          string,
                maintenanceLabel            string,
                maintenanceProbability        string,
                RecallLabel                    string,
                RecallProbability            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:ANOMALYOUTPUT}';

    DROP TABLE IF EXISTS RecallModel; 
    CREATE EXTERNAL TABLE RecallModel 
    (

                vin                            string,
                model                        string,
                city                        string,
                outsidetemperature            string,
                enginetemperature            string,
                speed                        string,
                Year                        string,
                Month                        string                

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:RECALLMODELOUTPUT}';

    INSERT OVERWRITE TABLE RecallModel
    select
    vin,
    model,
    city,
    outsidetemperature,
    enginetemperature,
    speed,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from CarEventsAnomaly
    where RecallLabel = '1' AND RecallProbability >= '0.60'


Po pomyślnym wykonaniu potoku hello zapoznaj się hello następujące partycje generowane na koncie magazynu w kontenerze "connectedcar" hello.

![Dane wyjściowe DetectAnomalyPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig24-vehicle-telematics-detect-anamoly-pipeline-output.png) 

*Rysunek 25 — DetectAnomalyPipeline danych wyjściowych*

## <a name="publish"></a>Publikowanie

### <a name="real-time-analysis"></a>Analiza w czasie rzeczywistym
Jedną z hello kwerend w zadaniu Stream Analytics hello publikuje dane wyjściowe tooan zdarzenia hello wystąpienia Centrum zdarzeń. 

![Zadania usługi analiza strumienia publikuje dane wyjściowe tooan wystąpienia Centrum zdarzeń](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig25-vehicle-telematics-stream-analytics-job-publishes-output-event-hub.png)

*Rysunek 26 — zadanie usługi Stream Analytics publikuje dane wyjściowe tooan wystąpienia Centrum zdarzeń*

![Stream Analytics query toopublish toohello output wystąpień Centrum zdarzeń](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig26-vehicle-telematics-stream-analytics-query-publish-output-event-hub.png)

*Rysunek 27 — toohello toopublish zapytań usługi Stream Analytics output wystąpień Centrum zdarzeń*

Ten strumień zdarzeń jest używany przez powitalne RealTimeDashboardApp zawartych w rozwiązaniu hello. Ta aplikacja korzysta z usługi sieci web Machine Learning żądań i odpowiedzi hello wyników w czasie rzeczywistym i publikuje zestawu danych usługi Power BI tooa dane wynikowe hello zużycia. 

### <a name="batch-analysis"></a>Analiza partii
wyniki Hello hello partii i przetwarzanie w czasie rzeczywistym są tabele bazy danych SQL Azure opublikowanych toohello zużycia. Hello Azure SQL Server, bazy danych i tabele hello są tworzone automatycznie w ramach hello w skrypcie Instalatora. 

![Przepływ pracy składnicy toodata skopiować wyniki przetwarzania wsadowego](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig27-vehicle-telematics-batch-processing-results-copy-to-data-mart.png)

*Rysunek 28 — przetwarzania przepływu składnicy toodata kopiowania wyników wsadowego*

![Zadania usługi analiza strumienia publikuje składnicy toodata](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig28-vehicle-telematics-stream-analytics-job-publishes-to-data-mart.png)

*Rysunek 29 — zadanie usługi Stream Analytics publikuje składnicy toodata*

![Ustawienie składnicy danych w zadaniu Stream Analytics](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig29-vehicle-telematics-data-mart-setting-in-stream-analytics-job.png)

*Rysunek 30 – składnicy danych ustawienie w zadaniu Stream Analytics*

## <a name="consume"></a>Używanie
Usługi Power BI pozwala to rozwiązanie sformatowanego pulpitu nawigacyjnego i analizy predykcyjnej wizualizacji danych w czasie rzeczywistym. 

Kliknij tutaj, aby uzyskać szczegółowe instrukcje dotyczące konfigurowania raportów usługi Power BI hello i hello pulpitu nawigacyjnego. pulpit nawigacyjny końcowego Hello wygląda następująco:

![Pulpit nawigacyjny programu Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig30-vehicle-telematics-powerbi-dashboard.png)

*Rysunek 31 - pulpitu nawigacyjnego programu Power BI*

## <a name="summary"></a>Podsumowanie
Ten dokument zawiera szczegółowe przechodzenia z hello rozwiązania analizy Telemetrii pojazdów. Ten wzorzec architektury lambda, dla których są wyświetlane w czasie rzeczywistym i partii analizy w usłudze prognoz i akcji. Ten wzorzec stosuje tooa szeroką gamę przypadków użycia, które wymagają aktywnej ścieżki (w czasie rzeczywistym) i analiza zimnych ścieżki (partii). 

