---
title: "aaaOverview nauki danych przy użyciu platformy Spark w usłudze Azure HDInsight | Dokumentacja firmy Microsoft"
description: "zestaw narzędzi platformy Spark MLlib Hello łączy uczenia maszynowego znaczne modelowania możliwości toohello rozproszonych HDInsight środowiska."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: a4e1de99-a554-4240-9647-2c6d669593c8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: 515705684a46917c2741bf063d439b1cda016abb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-data-science-using-spark-on-azure-hdinsight"></a>Omówienie nauki danych przy użyciu platformy Spark w usłudze Azure HDInsight
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

Ten pakiet tematy pokazuje, jak toouse HDInsight Spark toocomplete typowych danych nauki zadań takich jak wprowadzanie danych, funkcja engineering modelowania i oceny modelu. dane Hello używane jest przykładowe hello 2013 NYC taksówki podróży i taryfy zestawu danych. modele Hello wbudowane obejmują Regresja logistyczna i liniowych, losowe lasów i gradientu boosted drzewa. Witaj tematy przedstawiają także sposób toostore tych modeli w usłudze Azure blob magazynu (WASB) i w jaki sposób tooscore i ocena wydajności predykcyjnej. Bardziej zaawansowanych tematów dotyczących opisano, jak można modeli uczenia przy użyciu kominów krzyżowego sprawdzania poprawności i parametru funkcji hyper. Ten temat odwołujący się hello tematach opisano, jak tooset się hello klastra Spark, potrzebne kroki hello toocomplete hello wskazówki podane. 

## <a name="spark-and-mllib"></a>Platforma Spark i MLlib
[Platforma Spark](http://spark.apache.org/) platforma przetwarzania równoległego open source, który obsługuje w pamięci przetwarza tooboost hello wydajności aplikacji do analizy danych big data. aparat przetwarzania Spark Hello zaprojektowano pod kątem szybkości, łatwości użycia i zaawansowanych możliwości analitycznych. Możliwości rozproszone obliczenia w pamięci platforma Spark stanowić dobry wybór w przypadku hello algorytmów iteracyjnych używanych w machine learning i obliczeniach na grafach. [MLlib](http://spark.apache.org/mllib/) jest platforma Spark skalowalne maszyny learning biblioteki wprowadzający hello algorytmicznego modelowania możliwości toothis się środowisku rozproszonym. 

## <a name="hdinsight-spark"></a>Spark w usłudze HDInsight
[HDInsight Spark](../hdinsight/hdinsight-apache-spark-overview.md) hello Azure znajduje się oferty open source platformy Spark. Obejmuje również obsługę **notesów Jupyter PySpark** w klastrze Spark hello, które można uruchomić interakcyjnych zapytań Spark SQL Przekształcanie, filtrowania i wizualizacja danych przechowywanych w obiektach blob Azure (WASB). PySpark jest hello interfejsu API języka Python dla platformy Spark. wstawki kodu Hello dostarczające rozwiązań hello i Pokaż hello odpowiednich powierzchni toovisualize hello dane tutaj uruchomione w systemie klastry Spark hello notesów Jupyter. kroki modelowania Hello w tych tematach zawiera kod, który pokazuje, jak tootrain, ocenić, zapisywania i korzystać z każdego typu modelu. 

## <a name="setup-spark-clusters-and-jupyter-notebooks"></a>Instalatora: Klastry Spark i notesów Jupyter
Kroki instalacji i kodu są dostępne w tym przewodniku dla przy użyciu wersji 1.6 HDInsight Spark. Ale notesów Jupyter znajdują się w przypadku klastrów HDInsight Spark 1.6 jak Spark 2.0. Opis hello toothem notesów i linki znajdują się w hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) hello repozytorium GitHub zawierające je. Ponadto hello kodu w tym miejscu w notesach hello połączony jest rodzajowy i powinny działać na dowolnym klastra Spark. Jeśli nie używasz Spark w usłudze HDInsight, konfiguracja klastra hello i czynności administracyjne mogą być nieco inne niż to, co przedstawiono w tym miejscu. Dla wygody Oto łącza hello notesów Jupyter toohello 1.6 Spark (Uruchom jądra pySpark hello z powitania serwera notesu Jupyter toobe) i 2.0 Spark (Uruchom jądra pySpark3 hello z powitania serwera notesu Jupyter toobe):

### <a name="spark-16-notebooks"></a>Notesów Spark w wersji 1.6
Te komputery przenośne są toobe Uruchom jądra pySpark powitania serwera notesu Jupyter.

- [pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb): zawiera informacje na temat Eksploracja danych tooperform, modelowania i oceniania z kilku różnych algorytmów.
- [pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): zawiera tematy w notesie #1 i tworzenia modelu przy użyciu hyperparameter dostrajanie i krzyżowego sprawdzania poprawności.
- [pySpark-machine-learning-data-science-spark-model-consumption.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb): Pokazuje, jak toooperationalize zapisany model przy użyciu języka Python w usłudze HDInsight clusters.

### <a name="spark-20-notebooks"></a>Notesów Spark 2.0
Te komputery przenośne są toobe Uruchom hello pySpark3 jądra serwera notesu Jupyter.

- [Spark2.0-pySpark3-Machine-Learning-Data-Science-Spark-Advanced-Data-exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): ten plik zawiera informacje dotyczące sposobu tooperform Eksploracja danych, modelowania i oceniania w Spark 2.0 klastrów za pomocą hello taksówki NYC podróży i zestaw danych taryfy opisane [tutaj](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data). Ten notes może być dobry punkt wyjścia do eksplorowania szybko hello kodu, który firma Microsoft umieściła 2.0 Spark. Dla bardziej szczegółowe notesu analizuje hello taksówki NYC danych, zobacz hello notesu dalej na tej liście. Zobacz uwagi hello końcu tej listy, pozwalające porównać te komputery przenośne. 
- [Spark2.0 pySpark3_NYC_Taxi_Tip_Regression.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_NYC_Taxi_Tip_Regression.ipynb): ten plik pokazuje, jak tooperform danych wrangling (operacje Spark SQL i dataframe) eksploracji, modelowania i oceniania przy użyciu hello taksówki NYC podróży i taryfy zestawu danych opisane [ w tym miejscu](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).
- [Spark2.0 pySpark3_Airline_Departure_Delay_Classification.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_Airline_Departure_Delay_Classification.ipynb): ten plik pokazuje, jak tooperform danych wrangling (operacje Spark SQL i dataframe) eksploracji, modelowania i oceniania przy użyciu hello dobrze znanego linii lotniczych na czas wyjścia zestaw danych z 2011 i 2012. Dataset linii lotniczych hello firma Microsoft zintegrowane z hello lotnisku pogody danych (np. prędkość wiatru, temperatury, wysokość itp.) przed toomodeling, więc te funkcje pogody można dołączyć do modelu hello.

<!-- -->

> [!NOTE]
> zestaw danych linii lotniczych Hello dodano notesów toohello Spark 2.0 toobetter ilustrują hello użyciem algorytmów klasyfikacji. Zobacz następujące linki do informacji na temat zestawu danych na czas wyjścia linii lotniczych i dataset pogody hello:

>- Dane na czas wyjścia linii lotniczych: [http://www.transtats.bts.gov/ONTIME/](http://www.transtats.bts.gov/ONTIME/)

>- Dane pogody lotnisku: [https://www.ncdc.noaa.gov/](https://www.ncdc.noaa.gov/) 
> 
> 

<!-- -->

<!-- -->

> [!NOTE]
Notesy Spark 2.0 Hello na powitania taksówki NYC i linii lotniczych transmitowane opóźnienie-zestawów danych może potrwać 10 minut lub więcej toorun (w zależności od wielkości hello klastra HDI). Witaj pierwszego notesu w hello powyżej listy zawiera wiele aspektów hello Eksploracja danych, wizualizacji i ML modelu szkolenia w notesie pobierającej toorun mniej czasu z próbkowany dół NYC zestaw danych, w których hello taksówkami i taryfy pliki zostały wstępnie przyłączone do: [ Spark2.0-pySpark3-Machine-Learning-Data-Science-Spark-Advanced-Data-exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb) tego notesu zajmuje dużo krótszy czas toofinish (2 – 3 min) i może być bardzo punkt początkowy dla szybko Eksploracja kodu hello mamy podany dla Spark 2.0. 

<!-- -->

Aby uzyskać wskazówki dotyczące operationalization hello model Spark 2.0 i zużycia modelu do oceniania, zobacz hello [Spark 1.6 dokumentu o zużyciu](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb) przykład zwijania hello kroki wymagane. toouse to 2.0 Spark, Zastąp plik kodu Python hello z [ten plik](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Python/Spark2.0_ConsumeRFCV_NYCReg.py).

### <a name="prerequisites"></a>Wymagania wstępne
zgodnie z procedurami Hello są powiązane tooSpark 1.6. W wersji Spark 2.0 hello notesów hello Użyj opisane i połączone toopreviously. 

1 użytkownik musi mieć subskrypcję platformy Azure. Jeśli nie masz już jeden, zobacz [Azure Pobierz bezpłatną wersję próbną](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

2. należy toocomplete klastra Spark w wersji 1.6 tego przewodnika. toocreate, zobacz hello instrukcje podane w [wprowadzenie: tworzenie Apache Spark w usłudze Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md). Typ klastra Hello i wersji określonego z hello **wybierz typ klastra** menu. 

![Konfigurowanie klastra](./media/machine-learning-data-science-spark-overview/spark-cluster-on-portal.png)

<!-- -->

> [!NOTE]
> Dla tematu, który pokazuje, jak toouse Scala zamiast Python toocomplete zadań w procesie nauki danych na całej trasie, zobacz hello [nauki danych przy użyciu języka Scala z łącznikiem Spark on Azure](machine-learning-data-science-process-scala-walkthrough.md).
> 
> 

<!-- -->

> [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]
> 
> 

## <a name="hello-nyc-2013-taxi-data"></a>Witaj taksówki 2013 NYC danych
Hello danych podróży taksówki NYC około 20 GB skompresowanego wartości rozdzielanych przecinkami (CSV) plików (~ 48 GB nieskompresowane), składającej się z więcej niż 173 milionów poszczególnych podróży i hello cen w klasie ekonomicznej płatnej w odniesieniu do każdej podróży. Każdy rekord podróży obejmuje hello odbioru i przyjmowania lokalizacji i czasu, hack anonimowe (sterownik) numer licencji i numer Medalionu (taksówki jego unikatowy identyfikator). Hello danych obejmuje wszystkie rund w roku hello 2013 i jest dostępne w powitania po dwóch zestawów danych dla każdego miesiąca:

1. pliki CSV "trip_data" Hello zawierają szczegóły podróży, takie jak liczba pasażerów, podnieś i dropoff punktów, rzeczy przed wyjazdem czas trwania i długości podróży. Poniżej przedstawiono kilka przykładowych rekordów:
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. pliki CSV "trip_fare" Hello zawierają szczegółowe informacje o klasie hello za każdym razem, takie jak typ płatności, kwota taryfy przeciążenia i podatków, porady i przejazd i Suma hello płatnej. Poniżej przedstawiono kilka przykładowych rekordów:
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

Przekierowaliśmy próbkę 0,1% tych plików i połączone hello podróży\_danych i podróży\_taryfy CVS plików do toouse jednego zestawu danych jako hello wejściowy zestaw danych w ramach tego przewodnika. Hello unikatowy kluczy toojoin podróży\_danych i podróży\_taryfy składa się z pola hello: Medalionu, hack\_licencji i pobrania\_daty/godziny. Każdy rekord hello dataset zawiera następujące atrybuty reprezentujący podróży taksówki NYC hello:

| Pole | Krótki opis |
| --- | --- |
| Medalionu |Anonimowe taksówki Medalionu (taksówki Unikatowy identyfikator) |
| hack_license |Numer licencji karetki Hackney anonimowe |
| vendor_id |Identyfikator dostawcy taksówki |
| rate_code |Szybkość taksówki NYC Taryfy |
| store_and_fwd_flag |Magazyn i flagi do przodu |
| pickup_datetime |Wybierz datę i godzinę |
| dropoff_datetime |Dropoff wartość daty i godziny |
| pickup_hour |Wybierz godzinę |
| pickup_week |Wybierz tydzień roku hello |
| dzień tygodnia |Dzień tygodnia (zakresu 1-7) |
| passenger_count |Liczba osób w podróży taksówki |
| trip_time_in_secs |Podróży czas w sekundach |
| trip_distance |Dystans podróży w milach |
| pickup_longitude |Wybierz długość geograficzna |
| pickup_latitude |Podnieś współrzędnych |
| dropoff_longitude |Długość geograficzna Dropoff |
| dropoff_latitude |Współrzędne Dropoff |
| direct_distance |Bezpośrednie odległość między pobrania w górę i lokalizacje dropoff |
| payment_type |Typ płatności (urzędów certyfikacji, karta kredytowa itp.) |
| fare_amount |Kwota taryfy w |
| Przeciążenia |Przeciążenia |
| mta_tax |Podatek MTA |
| tip_amount |Porada kwota |
| tolls_amount |Kwota przejazd |
| total_amount |Suma |
| Przechylony |Przechylony (0/1 dla nie lub tak) |
| tip_class |Porada klasy (0: $0, 1: $0-5, 2: $6-10, 3: $11-20, 4: > $20) |

## <a name="execute-code-from-a-jupyter-notebook-on-hello-spark-cluster"></a>Wykonanie kodu z notesu Jupyter w klastrze Spark hello
Można uruchomić hello notesu Jupyter z hello portalu Azure. Znajdź klastra Spark na pulpicie nawigacyjnym i kliknij ją tooenter strony zarządzania dla klastra. Kliknij notesu hello tooopen skojarzony z klastrem Spark hello, **pulpitów nawigacyjnych klastrów** -> **notesu Jupyter** .

![Pulpitów nawigacyjnych klastrów](./media/machine-learning-data-science-spark-overview/spark-jupyter-on-portal.png)

Można również przeglądać zbyt***https://CLUSTERNAME.azurehdinsight.net/jupyter*** tooaccess hello notesów Jupyter. Zastąp nazwą hello własnego klastra hello NAZWAKLASTRA częścią tego adresu URL. Potrzebne hasło hello notesów hello tooaccess konta administratora.

![Przeglądaj notesów Jupyter](./media/machine-learning-data-science-spark-overview/spark-jupyter-notebook.png)

Wybierz toosee PySpark katalog, który zawiera kilka przykładów opakowanych notesów, korzystających z hello notesy PySpark API.hello, które zawierają hello przykłady kodu dla tego zestawu Spark tematu są dostępne pod adresem [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/pySpark)

Możesz przekazać notesów hello bezpośrednio z [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/pySpark) toohello Jupyter notebook serwera w klastrze Spark. Na stronie głównej hello Jupyter użytkownika, kliknij przycisk hello **przekazać** przycisk w prawej części ekranu hello hello. Spowoduje to otwarcie Eksploratora plików. W tym miejscu można Wklej adres URL usługi GitHub (nieprzetworzonej zawartości) hello hello notesu i kliknij przycisk **Otwórz**. 

Nazwa pliku hello zostanie wyświetlony na liście plików Jupyter z **przekazać** przycisk ponownie. Kliknij tutaj, **przekazać** przycisku. Teraz zaimportowano hello notesu. Powtórz te kroki tooupload hello innych notesów z tego przewodnika.

> [!TIP]
> Możesz kliknąć prawym przyciskiem myszy hello łącza przeglądarki i wybierz **Kopiuj Link** tooget hello github — nieprzetworzony adres URL zawartości. Ten adres URL można wkleić do hello Jupyter przekazać plik explorer — okno dialogowe.
> 
> 

Teraz możesz:

* Zobacz kod hello klikając hello notesu.
* Wykonanie każdej komórki naciskając **wprowadź SHIFT**.
* Uruchom hello cały notes klikając **komórki** -> **Uruchom**.
* Użyj automatycznego wizualizacji hello zapytań.

> [!TIP]
> Jądro PySpark Hello wizualizuje automatycznie hello wynik zapytania SQL (HiveQL). Podano tooselect opcji hello między kilka różnych typów wizualizacji (tabeli, kołowego, wiersz, obszar lub pasek) przy użyciu hello **typu** przycisków menu w notesie hello:
> 
> 

![Regresja logistyczna krzywą ROC dla metody ogólne](./media/machine-learning-data-science-spark-overview/pyspark-jupyter-autovisualization.png)

## <a name="whats-next"></a>Co dalej?
Teraz, gdy są skonfigurowane z klastra Spark w usłudze HDInsight i zostały przekazane notesów Jupyter hello jesteś gotowy toowork za pośrednictwem hello tematów, które odpowiadają toohello trzy PySpark notesów. Przedstawiają sposób tooexplore danych i jak następnie toocreate i korzystanie z modeli. Hello zaawansowane Eksploracja danych i modelowanie notesu pokazuje sposób tooinclude kominów krzyżowego sprawdzania poprawności, funkcji hyper parametr i oceny modelu. 

**Eksploracja danych i modelowanie z Spark:** Eksploruj hello zestawu danych i tworzenie, wynik i oceny hello machine learning modeli pracy nad hello [utworzyć binarne klasyfikacji i regresji modeli danych z hello Spark Zestaw narzędzi MLlib](machine-learning-data-science-spark-data-exploration-modeling.md) tematu.

**Model zużycia:** toolearn modele klasyfikacji i regresji hello tooscore utworzone w tym temacie, zobacz [wynik i ocena modele uczenia wbudowane Spark maszyny](machine-learning-data-science-spark-model-consumption.md).

**Krzyżowe sprawdzanie poprawności i kominów hyperparameter**: zobacz [zaawansowane Eksploracja danych i modelowania z Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) na jak modeli można uczony przy użyciu kominów krzyżowego sprawdzania poprawności i parametru funkcji hyper

