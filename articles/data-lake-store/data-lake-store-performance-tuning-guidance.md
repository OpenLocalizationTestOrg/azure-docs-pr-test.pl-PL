---
title: "aaaAzure wytyczne dostrajania wydajności sklepu Lake danych | Dokumentacja firmy Microsoft"
description: "Dostosowywanie wskazówki dotyczące wydajności usługi Azure Data Lake Store"
services: data-lake-store
documentationcenter: 
author: stewu
manager: amitkul
editor: cgronlun
ms.assetid: ebde7b9f-2e51-4d43-b7ab-566417221335
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/30/2017
ms.author: stewu
ms.openlocfilehash: 939faa068c0f81d18d9533956f4d336bc4d0cbe3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tuning-azure-data-lake-store-for-performance"></a>Dostrajanie wydajności usługi Azure Data Lake Store

Data Lake Store obsługuje wysokiej przepustowości dla analizy intensywne operacje We/Wy i przenoszenia danych.  W usłudze Azure Data Lake Store przy użyciu wszystkich dostępnych przepływności — Witaj ilość danych, które mogły być odczytywane i zapisywane na sekundę — jest ważna tooget hello najlepszą wydajność.  To jest osiągane, wykonując dowolną liczbę operacji odczytu i zapisu równoległe, jak to możliwe.

![Wydajność usługi Data Lake Store](./media/data-lake-store-performance-tuning-guidance/throughput.png)

Azure Data Lake Store można skalować przepływność tooprovide hello niezbędne dla wszystkich scenariuszy analizy. Domyślnie konto usługi Azure Data Lake Store zapewnia automatycznie za mało przepływności toomeet hello potrzebom szerokiego kategorii przypadków użycia. W przypadkach hello gdzie klienci funkcjonowaniem hello domyślny limit hello koncie ADLS może być skonfigurowany tooprovide więcej przepustowości kontaktując się z pomocą techniczną firmy Microsoft.

## <a name="data-ingestion"></a>Wprowadzanie danych

Podczas pobierania danych z tooADLS systemu źródłowego, ważne jest tooconsider, który hello sprzętu źródłowego, sprzęt sieciowy źródła i tooADLS łączności sieciowej może być "wąskim gardłem" hello.  

![Wydajność usługi Data Lake Store](./media/data-lake-store-performance-tuning-guidance/bottleneck.png)

Jest ważne tooensure, który hello przenoszenia danych nie ma wpływu na te czynniki.

### <a name="source-hardware"></a>Źródło sprzętu

Czy korzystasz z maszyny lokalnej lub maszyn wirtualnych na platformie Azure, należy wybrać uważnie hello jest odpowiedni sprzęt. Sprzętu z dysku źródłowego preferowane tooHDDs dyski SSD i wybierz sprzętu dysku z jednostkami szybsze. Dla źródła sprzętu sieciowego należy używać hello najszybsze karty sieciowe.  Na platformie Azure firma Microsoft zaleca D14 maszynach wirtualnych platformy Azure, którym hello odpowiedniego zaawansowanym dysku i sprzęt sieciowy.

### <a name="network-connectivity-tooazure-data-lake-store"></a>Sieciowe połączenie tooAzure Data Lake Store

Hello połączenie sieciowe między źródła danych i usługi Azure Data Lake store może być czasem hello "wąskie gardło". Jeśli źródło danych działa lokalnie, należy rozważyć użycie dedykowanego łącza z [Azure ExpressRoute](https://azure.microsoft.com/en-us/services/expressroute/) . Jeśli źródło danych jest na platformie Azure, wydajność hello jest najlepsza, gdy dane hello są hello tego samego regionu Azure hello usługi Data Lake Store.

### <a name="configure-data-ingestion-tools-for-maximum-parallelization"></a>Konfigurowanie narzędzia wprowadzanie danych do maksymalnego paralelizacja

Po usunąć hello źródła sprzętu i wąskich gardeł łączności powyżej sieci są gotowe tooconfigure narzędziami wprowadzanie. Hello poniższej tabeli zestawiono hello ustawień klucza dla kilku popularnych wprowadzanie narzędzi i zapewnia szczegółowe wydajność dostrajanie artykułów dla nich.  odwiedź witrynę toolearn więcej na temat narzędzia toouse dla danego scenariusza [artykułu](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-data-scenarios).

| Narzędzie               | Ustawienia     | Więcej informacji                                                                 |
|--------------------|------------------------------------------------------|------------------------------|
| PowerShell       | PerFileThreadCount, ConcurrentFileCount |  [Link](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-get-started-powershell#performance-guidance-while-using-powershell)   |
| AdlCopy    | Usługa Azure Data Lake Analytics jednostki  |   [Link](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-copy-data-azure-storage-blob#performance-considerations-for-using-adlcopy)         |
| Narzędzia DistCp            | -m (mapowanie)   | [Link](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-copy-data-wasb-distcp#performance-considerations-while-using-distcp)                             |
| Azure Data Factory| parallelCopies    | [Link](../data-factory/data-factory-copy-activity-performance.md)                          |
| Sqoop           | FS.Azure.Block.size, -m (mapowanie)    |   [Link](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/)        |

## <a name="structure-your-data-set"></a>Struktury zestawu danych

Gdy dane są przechowywane w usłudze Data Lake Store, rozmiar pliku hello, liczbę plików i struktury folderów będzie mieć wpływ na wydajność.  Witaj poniższej sekcji opisano najlepsze rozwiązania w następujących obszarach.  

### <a name="file-size"></a>Rozmiar pliku

Aparaty analizy, takie jak usługi HDInsight i usługą Azure Data Lake Analytics ma zwykle, obciążenie dla plików.  Jeśli dane są przechowywane jako wiele małych plików, może to negatywnie wpłynąć na wydajność.  

Ogólnie rzecz biorąc organizowania danych w większe pliki o rozmiarze w celu poprawy wydajności.  Jako zasadą organizowanie zestawów danych w plikach 256MB lub większy. W niektórych przypadkach, takich jak obrazy i danych binarnych nie jest możliwe tooprocess ich równolegle.  W takich przypadkach zaleca tookeep poszczególnych plików mniej niż 2GB.

Czasami potoki danych mają ograniczoną kontrolę nad hello nieprzetworzone dane, które zawiera wiele małych plików.  Zalecane jest toohave "gotowania" procesu, który generuje większe pliki toouse do podrzędnych aplikacji.  

### <a name="organizing-time-series-data-in-folders"></a>Organizowanie danych szeregów czasowych w folderach

W przypadku obciążeń Hive i ADLA partycji oczyszczania danych szeregu czasowego może pomóc niektórych kwerend odczytać tylko podzestaw danych hello, co zwiększa wydajność.    

Potoki, które pozyskiwania danych szeregu czasowego, często umieść ich pliki z bardzo strukturalnych nazewnictwa plików i folderów. Poniżej znajdują się bardzo typowym przykładem, który widzimy dla danych, które mają strukturę według daty:

    \DataSet\YYYY\MM\DD\datafile_YYYY_MM_DD.tsv

Należy zauważyć, że są wyświetlane informacje datetime hello folderów oraz w nazwie pliku hello.

Daty i godziny hello Oto wspólnego wzorca

    \DataSet\YYYY\MM\DD\HH\mm\datafile_YYYY_MM_DD_HH_mm.tsv

Ponownie hello wybrane z organizacją folderu i pliku hello powinien optymalizować hello większych plików i uzasadnione liczba plików w każdym folderze.

## <a name="optimizing-io-intensive-jobs-on-hadoop-and-spark-workloads-on-hdinsight"></a>Optymalizacja znacznym zadania we/wy na obciążenie Hadoop i Spark w usłudze HDInsight

Zadania dzielą się na powitania następujące trzy kategorie:

* **Procesora CPU.**  Te zadania mają obliczeń długie czasy wraz z minimalnym czasem we/wy.  Przykładami uczenie maszynowe i przetwarzania zadań języka naturalnego.  
* **Pamięci.**  Te zadania korzystają z dużej ilości pamięci.  Przykładami PageRank i zadania usługi analiza w czasie rzeczywistym.  
* **Operacji We/Wy.**  Te zadania spędzają większość czasu wykonywania operacji We/Wy.  Typowym przykładem jest zadanie kopiowania, które tylko do odczytu i zapisu.  Inne przykłady zadania przygotowywania danych, które odczyt dużą ilość danych, wykonuje pewne przekształcania danych, a następnie zapisuje hello magazynu zapasowego toohello danych.  

następujące wskazówki Hello jest tylko odpowiednie tooI/O znacznym zadania.

### <a name="general-considerations-for-an-hdinsight-cluster"></a>Ogólne zagadnienia dotyczące klastra usługi HDInsight

* **Wersje usługi HDInsight.** Aby uzyskać najlepszą wydajność Użyj hello najnowszej wersji usługi hdinsight.
* **Regiony.** Umieść hello Data Lake Store w hello tego samego regionu hello klastra usługi HDInsight.  

Klaster usługi HDInsight składa się z dwóch węzłów głównych i niektóre węzły procesów roboczych. Każdego węzła procesu roboczego zawiera określonej liczby rdzeni i ilości pamięci, który jest określany przez hello typu maszyny Wirtualnej.  Podczas wykonywania zadania, YARN jest moduł negocjowania zasobów hello przydzielanej hello dostępnej pamięci i kontenery toocreate rdzeni.  Każdy kontener uruchamia hello zadania wymagane toocomplete hello zadania.  Kontenery szybko uruchomić tooprocess równoległych zadań. W związku z tym lepsza wydajność, uruchamiając dowolną liczbę kontenerów równoległych, jak to możliwe.

Istnieją trzy warstwy w ramach klastra usługi HDInsight, które mogą być tooincrease Zaczekaj hello liczbę kontenerów i korzystać wszystkie dostępne przepływności.  

* **W warstwie fizycznej**
* **YARN warstwy**
* **Obciążenie warstwy**

### <a name="physical-layer"></a>W warstwie fizycznej

**Uruchomienie klastra z więcej węzłów i/lub większy rozmiar maszyn wirtualnych.**  Większego klastra spowoduje włączenie możesz toorun więcej kontenerów YARN pokazane na poniższej ilustracji hello.

![Wydajność usługi Data Lake Store](./media/data-lake-store-performance-tuning-guidance/VM.png)

**Użyj maszyn wirtualnych z większej przepustowości sieci.**  Hello ilość przepustowości sieci może być wąskiego gardła, jeśli istnieje mniej przepustowości sieci niż przepływności usługi Data Lake Store.  Różnych maszyn wirtualnych będą mieć różne rozmiary przepustowości sieci.  Wybierz maszyny Wirtualnej — typ, który ma hello największa możliwa przepustowości.

### <a name="yarn-layer"></a>YARN warstwy

**Używanie mniejszych kontenerów YARN.**  Zmniejszenie rozmiaru hello każdego toocreate kontenera YARN więcej kontenerów z hello tego samego ilość zasobów.

![Wydajność usługi Data Lake Store](./media/data-lake-store-performance-tuning-guidance/small-containers.png)

W zależności od obciążenia będą zawsze miały minimalny rozmiar kontenera YARN, który jest wymagany. W przypadku wybrania za mały kontener Twoje zadania będą uruchamiane w problemów braku pamięci. Zazwyczaj kontenerów YARN nie powinien być mniejszy niż 1GB. Jest typowe toosee 3GB YARN kontenerów. Dla niektórych zadań może być konieczne większe kontenery YARN.  

**Zwiększ rdzeni w jednym YARN kontenera.**  Zwiększ liczbę hello rdzeni przydzielone tooeach kontenera tooincrease hello liczby zadań wykonywanych w każdego kontenera.  Działa to w przypadku aplikacji, takich jak Spark, których uruchamianie wielu zadań na kontenera.  Dla aplikacji jak Hive, których uruchamianie pojedynczego wątku każdego kontenera jest lepsze toohave więcej kontenerów, a nie rdzeni na kontenera.   

### <a name="workload-layer"></a>Obciążenie warstwy

**Użyj wszystkich dostępnych kontenerów.**  Ustaw hello liczbę zadań toobe równa lub większa niż liczba hello dostępne kontenery, tak, aby wszystkie zasoby są wykorzystywane.

![Wydajność usługi Data Lake Store](./media/data-lake-store-performance-tuning-guidance/use-containers.png)

**Zadania zakończone niepowodzeniem są kosztowne.** Jeśli każde zadanie ma dużą ilość danych tooprocess, następnie niepowodzenia zadania powoduje kosztowne ponów próbę.  Dlatego jest lepsze toocreate więcej zadań, z których każdy przetwarza niewielką ilość danych.

W przypadku dodawania toohello ogólne wytyczne powyżej każda aplikacja ma różne parametry tootune dostępne dla tej konkretnej aplikacji. Witaj w poniższej tabeli przedstawiono niektóre z hello parametrów i linki tooget wprowadzenie dostrajania wydajności dla każdej aplikacji.

| Obciążenie               | Parametr tooset zadań                                                         |
|--------------------|-------------------------------------------------------------------------------------|
| [Platforma Spark w HDInisight](data-lake-store-performance-tuning-spark.md)       | <ul><li>Liczba modułów</li><li>Moduł wykonujący pamięci</li><li>Moduł wykonujący rdzeni</li></ul> |
| [Hive w usłudze HDInsight](data-lake-store-performance-tuning-hive.md)    | <ul><li>hive.tez.container.size</li></ul>         |
| [MapReduce w usłudze HDInsight](data-lake-store-performance-tuning-mapreduce.md)            | <ul><li>mapreduce.map.Memory</li><li>Mapreduce.job.Maps</li><li>mapreduce.Reduce.Memory</li><li>Mapreduce.job.reduces</li></ul> |
| [STORM w usłudze HDInsight](data-lake-store-performance-tuning-storm.md)| <ul><li>Liczba procesów roboczych</li><li>Liczba wystąpień Moduł wykonujący spout</li><li>Liczba wystąpień Moduł wykonujący bolt </li><li>Liczba zadań spout</li><li>Liczba zadań bolt</li></ul>|

## <a name="see-also"></a>Zobacz też
* [Omówienie usługi Azure Data Lake Store](data-lake-store-overview.md)
* [Rozpoczynanie pracy z usługą Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
