---
title: "Skalowalna nauki danych z usługi Azure Data Lake: wskazówki end-to-end | Dokumentacja firmy Microsoft"
description: "Jak toouse usługi Azure Data Lake toodo binarnego i eksploracja klasyfikacji danych zadań w zestawie danych."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 91a8207f-1e57-4570-b7fc-7c5fa858ffeb
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: bradsev;weig
ms.openlocfilehash: 8b05457ae7045a7aaed350a7502469f2247161e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scalable-data-science-with-azure-data-lake-an-end-to-end-walkthrough"></a>Skalowalna nauki danych z usługi Azure Data Lake: wskazówki end-to-end
W tym przewodniku przedstawiono sposób toouse usługi Azure Data Lake toodo Eksplorowanie danych oraz zadania klasyfikacji binarnej na próbkę hello NYC taksówki podróży i taryfy toopredict zestawu danych czy Porada zostanie zwrócona w klasie. Przeprowadza użytkownika przez kroki hello hello [proces nauki danych zespołu](http://aka.ms/datascienceprocess)end-to- end, z szkolenia toomodel pozyskiwania danych, a następnie toohello wdrożenia usługi sieci web, która publikuje hello modelu.

### <a name="azure-data-lake-analytics"></a>Azure Data Lake Analytics
Witaj [Microsoft Azure Data Lake](https://azure.microsoft.com/solutions/data-lake/) ma wszystkie toomake wymagane możliwości hello go łatwo toostore służące danych dowolnego rozmiar, kształt i szybkość i tooconduct przetwarzania danych, zaawansowane analizy i machine learning modelowania o wysokiej skalowalności w ekonomiczny sposób.   Opłaty są naliczane za poszczególne zadania wykonywane tylko wtedy, gdy dane są rzeczywiście przetwarzane. Azure Data Lake Analytics obejmuje U-SQL, języka, że mieszanka hello deklaratywne rodzaj SQL z wszechstronnymi możliwościami hello C# tooprovide skalowalne rozproszone możliwości zapytania. Włącza tooprocess danych niestrukturalnych przy zastosowaniu schematu na odczyt, wstawianie niestandardowej logiki i zdefiniowanych przez użytkownika (UDF) działa i zawiera rozszerzalności tooenable przeprowadzać kontrolę nad jak tooexecute na dużą skalę. toolearn więcej informacji na temat zasady projektowania klas hello za U-SQL, zobacz [programu Visual Studio w blogu](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).

Usługa Data Lake Analytics to także kluczowa część pakietu Cortana Analytics współdziałająca z usługami Azure SQL Data Warehouse, Power BI i Data Factory. Zapewnia dane big data pełnej chmury i platformy zaawansowana analityka.

W tym przewodniku rozpoczyna się od opisu hello warunki wstępne i zasobów, które są potrzebne toocomplete hello zadania związane z usługi Data Lake Analytics tworzą hello w procesie nauki danych i w jaki sposób tooinstall je. Następnie przedstawiono hello etapy przetwarzania danych przy użyciu języka U-SQL i stwierdza, pokazując jak toouse Python i Hive z toobuild Azure Machine Learning Studio i wdrażanie modeli predykcyjnych hello. 

### <a name="u-sql-and-visual-studio"></a>U-SQL i programu Visual Studio
W tym przewodniku zaleca przy użyciu programu Visual Studio tooedit U-SQL skrypty tooprocess hello dataset. skryptów U-SQL Hello są opisane w tym miejscu i dostępne w oddzielnym pliku. proces Hello obejmuje wprowadzania, badać i hello dane próbkowania. Pokazuje też, jak toorun U-SQL inicjowanych przez skrypty zadania z hello portalu Azure. Tabele programu hive są tworzone dla danych hello w skojarzonych budynku hello toofacilitate klastra usługi HDInsight i wdrażania modelu klasyfikacji binarnej w usłudze Azure Machine Learning Studio.  

### <a name="python"></a>Python
Ten przewodnik zawiera również sekcja, która przedstawia sposób toobuild i wdrażanie modelu predykcyjnego przy użyciu języka Python w usłudze Azure Machine Learning Studio.  Udostępniamy notesu Jupyter z hello skrypty języka Python dla tych kroków w tym procesie. Witaj notesu zawiera kod niektóre procedury engineering dodatkowych funkcji i modeli konstrukcji, takie jak wieloklasowej klasyfikacji i regresji modelowania Ponadto model klasyfikacji binarnej toohello opisana w tym temacie. zadanie regresji Hello jest toopredict hello ilość Porada hello na podstawie innych funkcji poradę. 

### <a name="azure-machine-learning"></a>Azure Machine Learning
Azure Machine Learning Studio jest używane toobuild i wdrażanie modeli predykcyjnych hello. Jest to realizowane przy użyciu dwóch metod: najpierw ze skryptami języka Python, a następnie tabele programu Hive w klastrze usługi HDInsight (Hadoop).

### <a name="scripts"></a>Skrypty
Tylko hello główne kroki zostały opisane w tym przewodniku. Możesz pobrać pełną hello **skrypt U-SQL** i **notesu Jupyter** z [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).

## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem tych tematów, musi mieć następujące hello:

* Subskrypcja platformy Azure. Jeśli nie masz już jeden, zobacz [Azure Pobierz bezpłatną wersję próbną](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* [Zalecane] Program Visual Studio 2013 lub nowszy. Jeśli nie już masz jeden z tych wersji, możesz pobrać bezpłatną wersję społeczności z [Visual Studio Community](https://www.visualstudio.com/vs/community/).

> [!NOTE]
> Zamiast programu Visual Studio umożliwia także zapytań usługi Azure Data Lake toosubmit hello w portalu Azure. Firma Microsoft udostępni instrukcje dotyczące sposobu toodo tak zarówno z programem Visual Studio, jak i w portalu hello w sekcji hello zatytułowany **przetwarzania danych w języku U-SQL**. 
> 
> 


## <a name="prepare-data-science-environment-for-azure-data-lake"></a>Przygotowanie środowiska nauki danych dla usługi Azure Data Lake
środowisko nauki tooprepare hello danych w ramach tego przewodnika tworzenia hello następujące zasoby:

* Azure Data Lake — magazyn (ADLS) 
* Usługi Azure Data Lake Analytics (ADLA)
* Konto magazynu obiektów Blob platformy Azure
* Konto usługi Azure Machine Learning Studio
* Usługi Azure Data Lake Tools dla programu Visual Studio (zalecane)

Ta sekcja zawiera instrukcje na temat toocreate tych zasobów. Jeśli wybierzesz toouse tabele programu Hive z usługi Azure Machine Learning, zamiast Python, toobuild modelu, konieczne będzie również tooprovision klastra usługi HDInsight (Hadoop). Ta procedura alternatywne w opisanego w hello odpowiedniej sekcji poniżej.


> [!NOTE]
> Witaj **Azure Data Lake Store** można tworzyć zarówno oddzielnie lub po utworzeniu hello **Azure Data Lake Analytics** jako hello domyślny magazyn. Instrukcje odwołuje się do tworzenia tych zasobów oddzielnie poniżej, ale hello konta magazynu usługi Data Lake muszą nie można utworzyć oddzielnie.
>
> 

### <a name="create-an-azure-data-lake-store"></a>Tworzenie usługi Azure Data Lake Store


Tworzenie ADLS z hello [Azure Portal](http://portal.azure.com). Aby uzyskać więcej informacji, zobacz [tworzenia klastra usługi HDInsight z Data Lake Store przy użyciu portalu Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md). Należy się tooset się hello tożsamość usługi AAD klastra w hello **źródła danych** bloku hello **konfiguracji opcjonalnej** bloku opisane istnieje. 

 ![3](./media/machine-learning-data-science-process-data-lake-walkthrough/3-create-ADLS.PNG)

### <a name="create-an-azure-data-lake-analytics-account"></a>Tworzenie konta usługi Azure Data Lake Analytics
Tworzenie konta usługi ADLA z hello [Azure Portal](http://portal.azure.com). Aby uzyskać więcej informacji, zobacz [samouczek: wprowadzenie do usługi Azure Data Lake Analytics przy użyciu portalu Azure](../data-lake-analytics/data-lake-analytics-get-started-portal.md). 

 ![4](./media/machine-learning-data-science-process-data-lake-walkthrough/4-create-ADLA-new.PNG)

### <a name="create-an-azure-blob-storage-account"></a>Tworzenie konta magazynu obiektów Blob platformy Azure
Tworzenie konta magazynu obiektów Blob platformy Azure z hello [Azure Portal](http://portal.azure.com). Aby uzyskać więcej informacji, zobacz hello Utwórz konto magazynu w sekcji [kont magazynu Azure o](../storage/common/storage-create-storage-account.md).

 ![5](./media/machine-learning-data-science-process-data-lake-walkthrough/5-Create-Azure-Blob.PNG)

### <a name="set-up-an-azure-machine-learning-studio-account"></a>Konfigurowanie konta usługi Azure Machine Learning Studio
Zaloguj się w górę/w usłudze Azure Machine Learning Studio z hello [usługi Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) strony. Polecenie hello **Rozpocznij teraz** przycisk, a następnie wybierz pozycję "Wolnego obszaru roboczego" lub "Standardowe obszaru roboczego". Dzięki temu będzie stanie toocreate eksperymentów w Studio uczenia Maszynowego Azure.  

### <a name="install-azure-data-lake-tools-recommended"></a>Zainstaluj usługi Azure Data Lake Tools [zalecane]
Zainstaluj usługi Azure Data Lake Tools dla używanej wersji programu Visual Studio z [Azure Data Lake Tools dla programu Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).

 ![6](./media/machine-learning-data-science-process-data-lake-walkthrough/6-install-ADL-tools-VS.PNG)

Po pomyślnym zainstalowaniu hello otwarcia programu Visual Studio. Witaj usługi Data Lake kartę hello menu u góry hello powinna zostać wyświetlona. Zasobów platformy Azure powinny być wyświetlane w lewym panelu powitania po zalogowaniu do konta platformy Azure.

 ![7](./media/machine-learning-data-science-process-data-lake-walkthrough/7-install-ADL-tools-VS-done.PNG)

## <a name="hello-nyc-taxi-trips-dataset"></a>Witaj NYC taksówki rund w zestawie danych
Witaj zestaw danych użyliśmy tutaj jest publicznie dostępnych zestawu danych--hello [dataset rund taksówki NYC](http://www.andresmh.com/nyctaxitrips/). Hello podróży taksówki NYC danych składa się z około 20GB skompresowanego plików CSV (~ 48GB nieskompresowane), rejestrowanie ponad milion 173 poszczególnych podróży i hello cen w klasie ekonomicznej płatnej w odniesieniu do każdej podróży. Każdy rekord podróży zawiera hello odbiór i przyjmowania lokalizacje i godziny anonimowe hack numer licencji (sterownik) i hello numer Medalionu (taksówki jego unikatowy identyfikator). Hello danych obejmuje wszystkie rund w roku hello 2013 i jest dostępne w powitania po dwóch zestawów danych dla każdego miesiąca:

* Witaj "trip_data" CSV zawiera szczegóły podróży, takie jak liczba pasażerów, pobranie i punkty dropoff czas trwania podróży i długość podróży. Poniżej przedstawiono kilka przykładowych rekordów:
  
       medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count, trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
       89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
* Witaj "trip_fare" CSV zawiera szczegółowe informacje o klasie hello za każdym razem, takie jak typ płatności, kwota taryfy przeciążenia i podatków, porady i przejazd i Suma hello płatnej. Poniżej przedstawiono kilka przykładowych rekordów:
  
       medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
       89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

Hello unikatowy kluczy toojoin podróży\_danych i podróży\_taryfy składa się z następujących trzech pól hello: Medalionu, hack\_licencji i pobrania\_daty/godziny. pliki CSV raw Hello jest możliwy z obiektu blob magazynu Azure publicznego. Witaj skryptu U-SQL dla tego sprzężenia jest hello [łączenia tabel podróży i taryfy](#join) sekcji.

## <a name="process-data-with-u-sql"></a>Przetwarzaj dane w języku U-SQL
zadania przetwarzania danych Hello przedstawione w tej sekcji obejmują wprowadzania, sprawdzanie jakości eksploracji i hello dane próbkowania. Również zostanie przedstawiony sposób toojoin podróży i taryfy tabel. sekcja końcowego Hello zawiera wykonywania zadania przy użyciu skryptu U-SQL z hello portalu Azure. Oto łącza podsekcji tooeach:

* [Wprowadzanie danych: odczytać danych z obiektu blob publiczny](#ingest)
* [Kontrola jakości danych](#quality)
* [Eksploracja danych](#explore)
* [Dołącz do tabel podróży i taryfy](#join)
* [Próbkowanie danych](#sample)
* [Uruchamianie zadań U-SQL](#run)

skryptów U-SQL Hello są opisane w tym miejscu i dostępne w oddzielnym pliku. Możesz pobrać pełną hello **skryptów U-SQL** z [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).

tooexecute U-SQL, Otwórz program Visual Studio, kliknij przycisk **Plik--> Nowa--> Projekt**, wybierz **projektu U-SQL**, nazw i zapisz go w folderze tooa.

![8](./media/machine-learning-data-science-process-data-lake-walkthrough/8-create-USQL-project.PNG)

> [!NOTE]
> Jest możliwe toouse hello Azure Portal tooexecute U-SQL zamiast programu Visual Studio. Można znaleźć toohello zasobów usługi Azure Data Lake Analytics w portalu hello i przesyłania zapytań bezpośrednio jako ilustrowane w powitania po rysunku.
> 
> 

![9](./media/machine-learning-data-science-process-data-lake-walkthrough/9-portal-submit-job.PNG)

### <a name="ingest"></a>Wprowadzanie danych: Odczyt danych z obiektu blob publiczny
Witaj lokalizację danych hello w hello obiektów blob platformy Azure jest określany jako  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name**  i wyodrębniona przy użyciu **Extractors.Csv()**. Podstawić własną nazwę kontenera i nazwy konta magazynu w następujących skryptów dla container_name@blob_storage_account_name hello wasb adresu. Ponieważ nazwy plików hello znajdują się w tym samym formacie, możemy użyć **podróży\_data_ {\*\}CSV** tooread we wszystkich plikach 12 podróży. 

    ///Read in Trip data
    @trip0 =
        EXTRACT 
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count string,
        trip_time_in_secs string,
        trip_distance string,
        pickup_longitude string,
        pickup_latitude string,
        dropoff_longitude string,
        dropoff_latitude string
    // This is reading 12 trip data from blob
    FROM "wasb://container_name@blob_storage_account_name.blob.core.windows.net/nyctaxitrip/trip_data_{*}.csv"
    USING Extractors.Csv();

Ponieważ w pierwszym wierszu hello nagłówki, możemy muszą tooremove hello nagłówków, a następnie zmień typy kolumn do nich odpowiednie. Możemy zapisać hello przetworzonych danych tooAzure usługi Data Lake Storage przy użyciu **swebhdfs://data_lake_storage_name.azuredatalakestorage.net/folder_name/file_name**przy użyciu konta magazynu obiektów Blob _ lub tooAzure  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name** . 

    // change data types
    @trip =
        SELECT 
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        DateTime.Parse(pickup_datetime) AS pickup_datetime,
        DateTime.Parse(dropoff_datetime) AS dropoff_datetime,
        Int32.Parse(passenger_count) AS passenger_count,
        Double.Parse(trip_time_in_secs) AS trip_time_in_secs,
        Double.Parse(trip_distance) AS trip_distance,
        (pickup_longitude==string.Empty ? 0: float.Parse(pickup_longitude)) AS pickup_longitude,
        (pickup_latitude==string.Empty ? 0: float.Parse(pickup_latitude)) AS pickup_latitude,
        (dropoff_longitude==string.Empty ? 0: float.Parse(dropoff_longitude)) AS dropoff_longitude,
        (dropoff_latitude==string.Empty ? 0: float.Parse(dropoff_latitude)) AS dropoff_latitude
    FROM @trip0
    WHERE medallion != "medallion";

    ////output data tooADL
    OUTPUT @trip   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_trip.csv"
    USING Outputters.Csv(); 

    ////Output data tooblob
    OUTPUT @trip   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_trip.csv"
    USING Outputters.Csv();  

Firma Microsoft może odczytywać podobnie w zestawach danych taryfy hello. Azure Data Lake Store kliknij prawym przyciskiem myszy, wybierz polecenie toolook danych w **Azure Portal--> Eksploratora danych** lub **Eksploratora plików** w programie Visual Studio. 

 ![10](./media/machine-learning-data-science-process-data-lake-walkthrough/10-data-in-ADL-VS.PNG)

 ![11](./media/machine-learning-data-science-process-data-lake-walkthrough/11-data-in-ADL.PNG)

### <a name="quality"></a>Kontrola jakości danych
Po odczytano podróży i taryfy tabel w kontroli jakości danych może odbywać się w następujący sposób hello. Hello co pliki CSV można magazynu obiektów Blob tooAzure danych wyjściowych lub usługi Azure Data Lake Store. 

Znajdź liczbę hello medallions i unikatowy numer medallions:

    ///check hello number of medallions and unique number of medallions
    @trip2 =
        SELECT
        medallion,
        vendor_id,
        pickup_datetime.Month AS pickup_month
        FROM @trip;

    @ex_1 =
        SELECT
        pickup_month, 
        COUNT(medallion) AS cnt_medallion,
        COUNT(DISTINCT(medallion)) AS unique_medallion
        FROM @trip2
        GROUP BY pickup_month;
        OUTPUT @ex_1   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_1.csv"
    USING Outputters.Csv(); 

Znajdź te medallions, w których zastosowano więcej niż 100 rund:

    ///find those medallions that had more than 100 trips
    @ex_2 =
        SELECT medallion,
               COUNT(medallion) AS cnt_medallion
        FROM @trip2
        //where pickup_datetime >= "2013-01-01t00:00:00.0000000" and pickup_datetime <= "2013-04-01t00:00:00.0000000"
        GROUP BY medallion
        HAVING COUNT(medallion) > 100;
        OUTPUT @ex_2   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_2.csv"
    USING Outputters.Csv(); 

Znajdź te nieprawidłowe rekordy pod względem pickup_longitude:

    ///find those invalid records in terms of pickup_longitude
    @ex_3 =
        SELECT COUNT(medallion) AS cnt_invalid_pickup_longitude
        FROM @trip
        WHERE
        pickup_longitude <- 90 OR pickup_longitude > 90;
        OUTPUT @ex_3   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_3.csv"
    USING Outputters.Csv(); 

Znajdź brakujące wartości dla niektórych zmiennych:

    //check missing values
    @res =
        SELECT *,
               (medallion == null? 1 : 0) AS missing_medallion
        FROM @trip;

    @trip_summary6 =
        SELECT 
            vendor_id,
        SUM(missing_medallion) AS medallion_empty, 
        COUNT(medallion) AS medallion_total,
        COUNT(DISTINCT(medallion)) AS medallion_total_unique  
        FROM @res
        GROUP BY vendor_id;
    OUTPUT @trip_summary6
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_16.csv"
    USING Outputters.Csv();



### <a name="explore"></a>Eksploracja danych
Możemy niektórych tooget Eksploracja danych lepszego zrozumienia hello danych.

Znajdź hello dystrybucji rund Przechylony i Przechylony:

    ///tipped vs. not tipped distribution
    @tip_or_not =
        SELECT *,
               (tip_amount > 0 ? 1: 0) AS tipped
        FROM @fare;

    @ex_4 =
        SELECT tipped,
               COUNT(*) AS tip_freq
        FROM @tip_or_not
        GROUP BY tipped;
        OUTPUT @ex_4   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_4.csv"
    USING Outputters.Csv(); 

Znajdź dystrybucji hello kwoty Porada wartościami odcięty: 0,5,10 i 20 kwoty.

    //tip class/range distribution
    @tip_class =
        SELECT *,
               (tip_amount >20? 4: (tip_amount >10? 3:(tip_amount >5 ? 2:(tip_amount > 0 ? 1: 0)))) AS tip_class
        FROM @fare;
    @ex_5 =
        SELECT tip_class,
               COUNT(*) AS tip_freq
        FROM @tip_class
        GROUP BY tip_class;
        OUTPUT @ex_5   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_5.csv"
    USING Outputters.Csv(); 

Znajdź podstawowe dane statystyczne odległości podróży:

    // find basic statistics for trip_distance
    @trip_summary4 =
        SELECT 
            vendor_id,
            COUNT(*) AS cnt_row,
            MIN(trip_distance) AS min_trip_distance,
            MAX(trip_distance) AS max_trip_distance,
            AVG(trip_distance) AS avg_trip_distance 
        FROM @trip
        GROUP BY vendor_id;
    OUTPUT @trip_summary4
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_14.csv"
    USING Outputters.Csv();

Znajdź percentylu hello odległości podróży:

    // find percentiles of trip_distance
    @trip_summary3 =
        SELECT DISTINCT vendor_id AS vendor,
                        PERCENTILE_DISC(0.25) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc,
                        PERCENTILE_DISC(0.5) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc,
                        PERCENTILE_DISC(0.75) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc
        FROM @trip;
       // group by vendor_id;
    OUTPUT @trip_summary3
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_13.csv"
    USING Outputters.Csv(); 


### <a name="join"></a>Dołącz do tabel podróży i taryfy
Mogą zostać sprzężone tabele podróży i taryfy Medalionu, hack_license i pickup_time.

    //join trip and fare table

    @model_data_full =
    SELECT t.*, 
    f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,  f.total_amount, f.tip_amount,
    (f.tip_amount > 0 ? 1: 0) AS tipped,
    (f.tip_amount >20? 4: (f.tip_amount >10? 3:(f.tip_amount >5 ? 2:(f.tip_amount > 0 ? 1: 0)))) AS tip_class
    FROM @trip AS t JOIN  @fare AS f
    ON   (t.medallion == f.medallion AND t.hack_license == f.hack_license AND t.pickup_datetime == f.pickup_datetime)
    WHERE   (pickup_longitude != 0 AND dropoff_longitude != 0 );

    //// output tooblob
    OUTPUT @model_data_full   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_7_full_data.csv"
    USING Outputters.Csv(); 

    ////output data tooADL
    OUTPUT @model_data_full   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_ex_7_full_data.csv"
    USING Outputters.Csv(); 


Dla każdego poziomu liczby pasażerów obliczyć hello liczbę rekordów, porada średnia kwota, odchylenie kwoty Porada stopień podróży Przechylony.

    // contigency table
    @trip_summary8 =
        SELECT passenger_count,
               COUNT(*) AS cnt,
               AVG(tip_amount) AS avg_tip_amount,
               VAR(tip_amount) AS var_tip_amount,
               SUM(tipped) AS cnt_tipped,
               (float)SUM(tipped)/COUNT(*) AS pct_tipped
        FROM @model_data_full
        GROUP BY passenger_count;
        OUTPUT @trip_summary8
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_17.csv"
    USING Outputters.Csv();


### <a name="sample"></a>Próbkowanie danych
Najpierw możemy losowo wybierać 0,1% hello danych z tabeli sprzężonych hello:

    //random select 1/1000 data for modeling purpose
    @addrownumberres_randomsample =
    SELECT *,
            ROW_NUMBER() OVER() AS rownum
    FROM @model_data_full;

    @model_data_random_sample_1_1000 =
    SELECT *
    FROM @addrownumberres_randomsample
    WHERE rownum % 1000 == 0;

    OUTPUT @model_data_random_sample_1_1000   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_7_random_1_1000.csv"
    USING Outputters.Csv(); 

Następnie przejdziemy stratyfikowana próbkowania przez binarny tip_class zmiennych:

    //stratified random select 1/1000 data for modeling purpose
    @addrownumberres_stratifiedsample =
    SELECT *,
            ROW_NUMBER() OVER(PARTITION BY tip_class) AS rownum
    FROM @model_data_full;

    @model_data_stratified_sample_1_1000 =
    SELECT *
    FROM @addrownumberres_stratifiedsample
    WHERE rownum % 1000 == 0;
    //// output tooblob
    OUTPUT @model_data_stratified_sample_1_1000   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_9_stratified_1_1000.csv"
    USING Outputters.Csv(); 
    ////output data tooADL
    OUTPUT @model_data_stratified_sample_1_1000   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_ex_9_stratified_1_1000.csv"
    USING Outputters.Csv(); 


### <a name="run"></a>Uruchamianie zadań U-SQL
Po zakończeniu edycji skryptów U-SQL, możesz przesłać je toohello serwera przy użyciu konta usługi Azure Data Lake Analytics. Kliknij przycisk **usługi Data Lake**, **Prześlij zadanie**, wybierz użytkownika **konta usługi Analytics**, wybierz **równoległości**i kliknij przycisk **przesyłania**  przycisku.  

 ![12](./media/machine-learning-data-science-process-data-lake-walkthrough/12-submit-USQL.PNG)

Gdy zadanie hello jest pomyślnie spełnione, hello stan zadania będą wyświetlane w programie Visual Studio do monitorowania. Po zakończeniu zadania hello może nawet powtarzania hello zadania wykonywania procesu i sprawdź hello bottleneck tooimprove kroki wydajność zadania. Można także przejść tooAzure Portal toocheck hello stan zadań U-SQL.

 ![13](./media/machine-learning-data-science-process-data-lake-walkthrough/13-USQL-running-v2.PNG)

 ![14](./media/machine-learning-data-science-process-data-lake-walkthrough/14-USQL-jobs-portal.PNG)

Teraz można sprawdzić pliki wyjściowe hello w magazynie obiektów Blob Azure lub w portalu Azure. Dla naszych modelowania w następnym kroku hello użyjemy hello uporządkować przykładowych danych.

 ![15](./media/machine-learning-data-science-process-data-lake-walkthrough/15-U-SQL-output-csv.PNG)

 ![16](./media/machine-learning-data-science-process-data-lake-walkthrough/16-U-SQL-output-csv-portal.PNG)

## <a name="build-and-deploy-models-in-azure-machine-learning"></a>Tworzenie i wdrażanie modeli w usłudze Azure Machine Learning
Przedstawiony dwie opcje dostępne dla Ciebie toopull danych do usługi Azure Machine Learning toobuild i 

* W pierwszej opcji hello, możesz użyć danych hello próbkowany została zapisana tooan obiektów Blob platformy Azure (w hello **danych próbkowania** kroku powyżej) i Python toobuild i wdrażanie modeli z usługi Azure Machine Learning. 
* W drugiej opcji hello zapytaniu hello dotyczącym danych w usłudze Azure Data Lake bezpośrednio za pomocą zapytań programu Hive. Ta opcja wymaga utworzenia nowego klastra usługi HDInsight, lub użyj istniejącego klastra usługi HDInsight, gdzie hello gałąź Tabele toohello punktu taksówki NY danych w usłudze Azure Data Lake Storage.  Omówiono obie te opcje poniżej. 

## <a name="option-1-use-python-toobuild-and-deploy-machine-learning-models"></a>Opcja 1: Użyj Python toobuild i wdrażanie modeli uczenia maszyny
toobuild i wdrażanie modeli uczenia komputera przy użyciu języka Python, tworzenie notesu Jupyter na komputerze lokalnym lub w usłudze Azure Machine Learning Studio. Witaj notesu Jupyter podanego w [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough) zawiera hello tooexplore pełny kod, wizualizację danych, funkcja zespołu inżynieryjnego, modelowania i wdrożenia. W tym artykule zostanie przedstawiony tylko modelowania hello i wdrażania. 

### <a name="import-python-libraries"></a>Importuj biblioteki języka Python
W kolejności toorun hello przykładowe notesu Jupyter lub hello pliku skryptu języka Python, hello następujące pakiety Python niezbędne. Jeśli używasz usługi uczenie maszynowe Azure notesu hello te pakiety zostały wstępnie zainstalowane.

    import pandas as pd
    from pandas import Series, DataFrame
    import numpy as np
    import matplotlib.pyplot as plt
    from time import time
    import pyodbc
    import os
    from azure.storage.blob import BlobService
    import tables
    import time
    import zipfile
    import random
    import sklearn
    from sklearn.linear_model import LogisticRegression
    from sklearn.cross_validation import train_test_split
    from sklearn import metrics
    from __future__ import division
    from sklearn import linear_model
    from azureml import services


### <a name="read-in-hello-data-from-blob"></a>Przeczytaj hello danych z obiektu blob
* Parametry połączenia   
  
        CONTAINERNAME = 'test1'
        STORAGEACCOUNTNAME = 'XXXXXXXXX'
        STORAGEACCOUNTKEY = 'YYYYYYYYYYYYYYYYYYYYYYYYYYYY'
        BLOBNAME = 'demo_ex_9_stratified_1_1000_copy.csv'
        blob_service = BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
* Odczytu w postaci tekstu
  
        t1 = time.time()
        data = blob_service.get_blob_to_text(CONTAINERNAME,BLOBNAME).split("\n")
        t2 = time.time()
        print(("It takes %s seconds tooread in "+BLOBNAME) % (t2 - t1))
  
  ![17](./media/machine-learning-data-science-process-data-lake-walkthrough/17-python_readin_csv.PNG)    
* Dodaj nazwy kolumn i oddziel kolumn
  
        colnames = ['medallion','hack_license','vendor_id','rate_code','store_and_fwd_flag','pickup_datetime','dropoff_datetime',
        'passenger_count','trip_time_in_secs','trip_distance','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude',
        'payment_type', 'fare_amount', 'surcharge', 'mta_tax', 'tolls_amount',  'total_amount', 'tip_amount', 'tipped', 'tip_class', 'rownum']
        df1 = pd.DataFrame([sub.split(",") for sub in data], columns = colnames)
* Zmień toonumeric niektóre kolumny
  
        cols_2_float = ['trip_time_in_secs','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude',
        'fare_amount', 'surcharge','mta_tax','tolls_amount','total_amount','tip_amount', 'passenger_count','trip_distance'
        ,'tipped','tip_class','rownum']
        for col in cols_2_float:
            df1[col] = df1[col].astype(float)

### <a name="build-machine-learning-models"></a>Tworzenie modeli uczenia maszyny
W tym miejscu budujemy toopredict model klasyfikacji binarnej czy podróży jest Przechylony lub nie. W hello notesu Jupyter można znaleźć inne dwa modele: wieloklasowej klasyfikacji i regresji modeli.

* Najpierw musimy toocreate fikcyjny zmiennych, które mogą być używane w scikit — Dowiedz się modeli
  
        df1_payment_type_dummy = pd.get_dummies(df1['payment_type'], prefix='payment_type_dummy')
        df1_vendor_id_dummy = pd.get_dummies(df1['vendor_id'], prefix='vendor_id_dummy')
* Utwórz ramkę danych dla hello modelowania
  
        cols_to_keep = ['tipped', 'trip_distance', 'passenger_count']
        data = df1[cols_to_keep].join([df1_payment_type_dummy,df1_vendor_id_dummy])
  
        X = data.iloc[:,1:]
        Y = data.tipped
* Uczenie i testowanie 60 40 podziału
  
        X_train, X_test, Y_train, Y_test = train_test_split(X, Y, test_size=0.4, random_state=0)
* Regresja logistyczna w zestawie szkolenia
  
        model = LogisticRegression()
        logit_fit = model.fit(X_train, Y_train)
        print ('Coefficients: \n', logit_fit.coef_)
        Y_train_pred = logit_fit.predict(X_train)
  
       ![c1](./media/machine-learning-data-science-process-data-lake-walkthrough/c1-py-logit-coefficient.PNG)
* Wynik testowania zestawu danych
  
        Y_test_pred = logit_fit.predict(X_test)
* Oblicz metryki oceny
  
        fpr_train, tpr_train, thresholds_train = metrics.roc_curve(Y_train, Y_train_pred)
        print fpr_train, tpr_train, thresholds_train
  
        fpr_test, tpr_test, thresholds_test = metrics.roc_curve(Y_test, Y_test_pred) 
        print fpr_test, tpr_test, thresholds_test
  
        #AUC
        print metrics.auc(fpr_train,tpr_train)
        print metrics.auc(fpr_test,tpr_test)
  
        #Confusion Matrix
        print metrics.confusion_matrix(Y_train,Y_train_pred)
        print metrics.confusion_matrix(Y_test,Y_test_pred)
  
       ![c2](./media/machine-learning-data-science-process-data-lake-walkthrough/c2-py-logit-evaluation.PNG)

### <a name="build-web-service-api-and-consume-it-in-python"></a>Tworzenie interfejsu API usługi sieci Web i używać go w języku Python
Chcemy maszyny hello toooperationalize uczenie modelu po został skompilowany. W tym miejscu używamy modelu binarnego logistyczna hello jako przykład. Upewnij się, że scikit hello — Dowiedz się więcej wersji w komputerze lokalnym jest 0.15.1. Jeśli używasz usługi Azure ML studio usługi nie masz tooworry na ten temat.

* Znajdź poświadczenia obszar roboczy z usługi Azure ML studio ustawień. W usłudze Azure Machine Learning Studio, kliknij przycisk **ustawienia** --> **nazwa** --> **tokeny autoryzacji**. 
  
    ![C3](./media/machine-learning-data-science-process-data-lake-walkthrough/c3-workspace-id.PNG)

        workspaceid = 'xxxxxxxxxxxxxxxxxxxxxxxxxxx'
        auth_token = 'xxxxxxxxxxxxxxxxxxxxxxxxxxx'

* Tworzenie usługi sieci Web
  
        @services.publish(workspaceid, auth_token) 
        @services.types(trip_distance = float, passenger_count = float, payment_type_dummy_CRD = float, payment_type_dummy_CSH=float, payment_type_dummy_DIS = float, payment_type_dummy_NOC = float, payment_type_dummy_UNK = float, vendor_id_dummy_CMT = float, vendor_id_dummy_VTS = float)
        @services.returns(int) #0, or 1
        def predictNYCTAXI(trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH,payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS ):
            inputArray = [trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH, payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS]
            return logit_fit.predict(inputArray)
* Pobieranie poświadczeń usługi sieci web
  
        url = predictNYCTAXI.service.url
        api_key =  predictNYCTAXI.service.api_key
  
        print url
        print api_key
  
        @services.service(url, api_key)
        @services.types(trip_distance = float, passenger_count = float, payment_type_dummy_CRD = float, payment_type_dummy_CSH=float,payment_type_dummy_DIS = float, payment_type_dummy_NOC = float, payment_type_dummy_UNK = float, vendor_id_dummy_CMT = float, vendor_id_dummy_VTS = float)
        @services.returns(float)
        def NYCTAXIPredictor(trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH,payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS ):
            pass
* Wywołanie interfejsu API usługi sieci Web. Masz toowait 5 – 10 sekund po hello w poprzednim kroku.
  
        NYCTAXIPredictor(1,2,1,0,0,0,0,0,1)
  
       ![c4](./media/machine-learning-data-science-process-data-lake-walkthrough/c4-call-API.PNG)

## <a name="option-2-create-and-deploy-models-directly-in-azure-machine-learning"></a>Opcja 2: Tworzenie i wdrażanie modeli bezpośrednio w usłudze Azure Machine Learning
Azure Machine Learning Studio można odczytać dane bezpośrednio z usługi Azure Data Lake Store można toocreate używane i wdrażanie modeli. Ta metoda używa tabeli programu Hive, który wskazuje na hello Azure Data Lake Store. Wymaga to udostępniane oddzielny klaster Azure HDInsight, na które hello Hive tabela została utworzona. Witaj, jak następujące sekcje Pokaż toodo to. 

### <a name="create-an-hdinsight-linux-cluster"></a>Tworzenie klastra usługi HDInsight w systemie Linux
Tworzenie klastra usługi HDInsight (Linux) z hello [Azure Portal](http://portal.azure.com). Aby uzyskać więcej informacji, zobacz hello **tworzenia klastra usługi HDInsight z tooAzure dostępu do usługi Data Lake Store** sekcji [tworzenia klastra usługi HDInsight z Data Lake Store przy użyciu portalu Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

 ![18](./media/machine-learning-data-science-process-data-lake-walkthrough/18-create_HDI_cluster.PNG)

### <a name="create-hive-table-in-hdinsight"></a>Tworzenie tabeli Hive w usłudze HDInsight
Teraz utworzymy używana w usłudze Azure Machine Learning Studio w hello klastra usługi HDInsight przy użyciu hello danych przechowywanych w usłudze Azure Data Lake Store w poprzednim kroku hello toobe tabel Hive. Przejdź toohello właśnie utworzony klaster usługi HDInsight. Kliknij przycisk **ustawienia** --> **właściwości** --> **klastra tożsamości w usłudze AAD** --> **dostępem ADLS**, Upewnij się, że konto usługi Azure Data Lake Store zostanie dodane na liście hello z odczytu, zapisu i wykonywania praw. 

 ![19](./media/machine-learning-data-science-process-data-lake-walkthrough/19-HDI-cluster-add-ADLS.PNG)

Następnie kliknij przycisk **pulpitu nawigacyjnego** dalej toohello **ustawienia** przycisk i okno zostanie wyskakujące. Kliknij przycisk **Hive View** w hello prawym górnym rogu strony hello i zostanie wyświetlony hello **edytora zapytań**.

 ![20](./media/machine-learning-data-science-process-data-lake-walkthrough/20-HDI-dashboard.PNG)

 ![21](./media/machine-learning-data-science-process-data-lake-walkthrough/21-Hive-Query-Editor-v2.PNG)

Wklej powitania po toocreate skrypty Hive tabeli. Witaj lokalizację źródła danych jest w dokumentacji usługi Azure Data Lake Store w ten sposób: **adl://data_lake_store_name.azuredatalakestore.net:443/nazwa_folderu/nazwa_pliku**.

    CREATE EXTERNAL TABLE nyc_stratified_sample
    (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count string,
        trip_time_in_secs string,
        trip_distance string,
        pickup_longitude string,
        pickup_latitude string,
        dropoff_longitude string,
        dropoff_latitude string,
      payment_type string,
      fare_amount string,
      surcharge string,
      mta_tax string,
      tolls_amount string,
      total_amount string,
      tip_amount string,
      tipped string,
      tip_class string,
      rownum string
      )
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    LOCATION 'adl://data_lake_storage_name.azuredatalakestore.net:443/nyctaxi_folder/demo_ex_9_stratified_1_1000_copy.csv';


Po zakończeniu zapytania hello zobaczysz wyniki hello następująco:

 ![22](./media/machine-learning-data-science-process-data-lake-walkthrough/22-Hive-Query-results.PNG)

### <a name="build-and-deploy-models-in-azure-machine-learning-studio"></a>Tworzenie i wdrażanie modeli w usłudze Azure Machine Learning Studio
Firma Microsoft są teraz gotowe toobuild i wdrażanie modelu, który wskazuje, czy etykietki otrzymuje przy użyciu usługi Azure Machine Learning. Witaj stratyfikowana przykładowych danych jest gotowy toobe używane w tym klasyfikacji binarnej (Porada lub nie) problem. Witaj modeli predykcyjnych, przy użyciu wieloklasowej klasyfikacji (tip_class) i regresji (tip_amount) również może być skompilowany i wdrożony w usłudze Azure Machine Learning Studio, ale w tym miejscu możemy Pokaż tylko sposób toohandle hello wielkość użyciu hello model klasyfikacji binarnej.

1. Pobierz dane hello do uczenia Maszynowego Azure przy użyciu hello **importowanie danych** modułu dostępne w hello **danych wejściowych i wyjściowych** sekcji. Aby uzyskać więcej informacji, zobacz hello [modułu importu danych](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) strony odwołania.
2. Wybierz **zapytanie Hive** jako hello **źródła danych** w hello **właściwości** panelu.
3. Wklej hello następującego skryptu Hive w hello **zapytanie Hive bazy danych** edytora
   
        select * from nyc_stratified_sample;
4. Wprowadź hello URI HDInsight klastra (znajdują się w portalu Azure), poświadczenia usługi Hadoop, lokalizacja danych wyjściowych i nazwę kontenera nazwa/kluczy konta magazynu platformy Azure.
   
   ![23](./media/machine-learning-data-science-process-data-lake-walkthrough/23-reader-module-v3.PNG)  

Przykład eksperymentu klasyfikacji binarnej odczytywanie danych z tabeli Hive przedstawiono hello rysunku poniżej.

 ![24](./media/machine-learning-data-science-process-data-lake-walkthrough/24-AML-exp.PNG)

Po utworzeniu hello eksperyment, kliknij przycisk **ustawić usługę sieci Web** --> **predykcyjnej usługi sieci Web**

 ![25](./media/machine-learning-data-science-process-data-lake-walkthrough/25-AML-exp-deploy.PNG)

Oceniania eksperymentu, po zakończeniu kliknij przycisk Uruchom hello tworzone automatycznie **wdrażanie usługi sieci Web**

 ![26](./media/machine-learning-data-science-process-data-lake-walkthrough/26-AML-exp-deploy-web.PNG)

wkrótce zostanie wyświetlony pulpit nawigacyjny usługi sieci web Hello:

 ![27](./media/machine-learning-data-science-process-data-lake-walkthrough/27-AML-web-api.PNG)

## <a name="summary"></a>Podsumowanie
Kończenie pracy tego przewodnika utworzono środowisku nauki danych do tworzenia skalowalnych rozwiązań end-to-end w usłudze Azure Data Lake. To środowisko zostało tooanalyze używane duże publicznego zestawu danych, zabierz hello canonical kroki hello proces analizy danych, z pozyskiwania danych za pomocą uczenia modelu i następnie toohello wdrożenie hello model jako usługę sieci web. U-SQL została tooprocess używane i Eksploruj przykładowe dane hello. Python i Hive były używane z toobuild Azure Machine Learning Studio i wdrażanie modeli predykcyjnych.

## <a name="whats-next"></a>Co dalej?
Hello uczenia ścieżkę [zespołu danych nauki procesu (TDSP)](http://aka.ms/datascienceprocess) zapewnia tootopics łącza temat każdego kroku w hello zaawansowane analizy procesu. Istnieje szereg wskazówki wyszczególnione na powitania [wskazówki dotyczące procesu nauki danych zespołu](data-science-process-walkthroughs.md) jak strony tego pokazy toouse zasobów i usług w różnych scenariuszach analizy predykcyjnej:

* [Hello proces nauki danych zespołu w działaniu: przy użyciu magazynu danych SQL](machine-learning-data-science-process-sqldw-walkthrough.md)
* [Hello proces nauki danych zespołu w działaniu: z użyciem klastrów usługi HDInsight Hadoop](machine-learning-data-science-process-hive-walkthrough.md)
* [Hello proces nauki danych zespołu: przy użyciu programu SQL Server](machine-learning-data-science-process-sql-walkthrough.md)
* [Omówienie hello proces analizy danych za pomocą Spark w usłudze Azure HDInsight](machine-learning-data-science-spark-overview.md)

