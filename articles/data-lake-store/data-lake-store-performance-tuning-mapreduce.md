---
title: "Data Lake MapReduce wydajności dostrajanie wytyczne sklepu aaaAzure | Dokumentacja firmy Microsoft"
description: "Dostosowywanie wskazówki dotyczące wydajności MapReduce usługi Azure Data Lake Store"
services: data-lake-store
documentationcenter: 
author: stewu
manager: amitkul
editor: stewu
ms.assetid: ebde7b9f-2e51-4d43-b7ab-566417221335
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/19/2016
ms.author: stewu
ms.openlocfilehash: e21414a23530e65613c85156af0209c88ec54d2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tuning-guidance-for-mapreduce-on-hdinsight-and-azure-data-lake-store"></a>Wskazówki dotyczące MapReduce na HDInsight i usługi Azure Data Lake Store dostrajania wydajności


## <a name="prerequisites"></a>Wymagania wstępne

* **Subskrypcja platformy Azure**. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Konto usługi Azure Data Lake Store**. Aby uzyskać instrukcje dotyczące jednego, zobacz toocreate [wprowadzenie do usługi Azure Data Lake Store](data-lake-store-get-started-portal.md)
* **Klaster HDInsight Azure** z tooa dostępu do konta usługi Data Lake Store. Zobacz [tworzenia klastra usługi HDInsight z usługą Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md). Upewnij się, że włączenie pulpitu zdalnego dla klastra hello.
* **W usłudze HDInsight przy użyciu MapReduce**.  Aby uzyskać więcej informacji, zobacz [MapReduce używany w Hadoop w usłudze HDInsight](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-use-mapreduce)  
* **Wytyczne dotyczące ADLS dostrajania wydajności**.  Pojęcia dotyczące ogólnej wydajności, aby zapoznać [Data Lake magazynu dostrajanie wytyczne dotyczące wydajności](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance)  

## <a name="parameters"></a>Parametry

Podczas uruchamiania zadań MapReduce, Oto hello Parametry najważniejszych tooincrease wydajności można skonfigurować na ADLS:

* **Mapreduce.map.Memory.MB** — Witaj ilość pamięci tooallocate tooeach mapowania
* **Mapreduce.job.Maps** — Witaj liczba zadań mapy na zadanie
* **Mapreduce.Reduce.Memory.MB** — Witaj ilość pamięci tooallocate tooeach reduktor
* **Mapreduce.job.reduces** — Witaj liczba zadań Zmniejsz na zadanie

**Mapreduce.map.Memory / Mapreduce.reduce.memory** liczba ta powinna dostosowywane w zależności od ilości pamięci jest wymagana dla mapy hello i/lub zmniejszyć zadań.  wartości domyślne Hello mapreduce.map.memory i mapreduce.reduce.memory można wyświetlić w Ambari za pośrednictwem hello Yarn konfiguracji.  W Ambari Przejdź tooYARN i wyświetl kartę Configs hello.  pojawi się Hello YARN pamięci.  

**Mapreduce.job.Maps / Mapreduce.job.reduces** umożliwi to określenie hello maksymalną liczbę toobe mapowań lub reduktory utworzony.  Określa Hello liczba podziałów dla zadania MapReduce hello zostanie utworzony ile mapowań.  W związku z tym może pobrać mapowań, mniejsze niż wymagane, jeśli istnieją podziałów mniejszą niż liczba hello mapowań żądanie.       

## <a name="guidance"></a>Wskazówki

**Krok 1: Określanie liczba zadań uruchomionych** — domyślnie MapReduce użyje hello całego klastra dla zadania.  Przy użyciu mapowań, mniejsze niż jest dostępne kontenery, można użyć klastra hello jest mniejsza.  wskazówki Hello w tym dokumencie zakłada, że aplikacja hello aplikacji tylko uruchomione w klastrze.      

**Krok 2: Ustaw mapreduce.map.memory/mapreduce.reduce.memory** — Witaj rozmiar pamięci hello mapy co pozwala zmniejszyć liczbę zadań będzie zależało od określonego zadania.  Można zmniejszyć rozmiar pamięci hello, jeśli chcesz tooincrease współbieżności.  Witaj liczbę jednocześnie uruchomionych zadań zależy od hello liczbę kontenerów.  Dzięki skróceniu hello ilość pamięci na mapowania lub reduktor, można utworzyć więcej kontenerów, umożliwiające więcej toorun mapowań lub reduktory jednocześnie.  Zbyt dużo malejącej hello ilość pamięci może spowodować toorun niektóre procesy za mało pamięci.  Jeśli zostanie wyświetlony błąd stosu podczas uruchamiania zadania, należy zwiększyć ilość pamięci hello na mapowania lub reduktor.  Należy rozważyć dodanie więcej kontenerów spowoduje dodanie czy bardzo ogólnych, dla każdego kontenera dodatkowe, które potencjalnie może zmniejszyć wydajność.  Inną możliwością jest tooget większej ilości pamięci za pomocą klastra, który ma większych ilości pamięci lub zwiększenie hello liczby węzłów w klastrze.  Więcej pamięci umożliwi więcej toobe kontenery używane, co oznacza więcej współbieżności.  

**Krok 3: Określanie YARN całkowitej pamięci** -tootune mapreduce.job.maps/mapreduce.job.reduces, należy rozważyć hello ilość całkowitej ilości pamięci YARN dostępne do użycia.  Te informacje są dostępne w narzędzia Ambari.  Przejdź tooYARN, a następnie Wyświetl kartę Configs hello.  Witaj YARN pamięci jest wyświetlany w tym oknie.  Należy pomnożyć pamięci YARN hello hello liczby węzłów w klastrze tooget hello całkowita YARN pamięci.

    Total YARN memory = nodes * YARN memory per node
Jeśli używane są puste klastra, pamięci może być YARN hello pamięć dla klastra.  Jeśli inne aplikacje są używane pamięci, można wybrać Użyj tooonly część klastra pamięci dzięki zmniejszeniu liczby hello mapowań lub reduktory toohello liczbę kontenerów ma toouse.  

**Krok 4: Obliczyć liczbę kontenerów YARN** — YARN kontenery dyktowania hello ilość dostępne dla zadania hello współbieżności.  Pobrać YARN pamięć i przez mapreduce.map.memory.  

    # of YARN containers = total YARN memory / mapreduce.map.memory

**Krok 5: Ustawianie mapreduce.job.maps/mapreduce.job.reduces** ustawić mapreduce.job.maps/mapreduce.job.reduces tooat najmniejsza liczba hello dostępnych kontenerów.  Możesz eksperymentować dalsze przez odpowiednie zwiększenie liczby hello mapowań i reduktory toosee, jeśli osiągnąć wyższą wydajność.  Należy pamiętać więcej mapowań ma dodatkowe obciążenie, o zbyt wiele mapowań może obniżyć wydajność.  

Planowanie procesora CPU i procesora CPU izolacji są domyślnie wyłączone tak hello liczbę kontenerów YARN jest ograniczane przez pamięci.

## <a name="example-calculation"></a>Przykład obliczeń

Załóżmy, że masz obecnie klaster składa się z 8 węzłów D14 ma toorun zadania intensywne operacje We/Wy.  Poniżej przedstawiono hello obliczeń, które należy wykonać:

**Krok 1: Określanie liczba zadań uruchomionych** — w naszym przykładzie przyjęto założenie, że nasze zadania jest hello uruchomiona tylko jedna.  

**Krok 2: Ustaw mapreduce.map.memory/mapreduce.reduce.memory** — w naszym przykładzie są uruchomione znacznym zadania we/wy i zdecydować, że 3 GB pamięci dla zadań mapy będą wystarczające.

    mapreduce.map.memory = 3GB
**Krok 3: Określanie YARN całkowitej pamięci**

    total memory from hello cluster is 8 nodes * 96GB of YARN memory for a D14 = 768GB
**Krok 4: Liczba kontenerów YARN obliczyć**

    # of YARN containers = 768GB of available memory / 3 GB of memory =   256

**Krok 5: Ustawianie mapreduce.job.maps/mapreduce.job.reduces**

    mapreduce.map.jobs = 256

## <a name="limitations"></a>Ograniczenia

**ADLS ograniczania przepustowości**

Jako usługę wielodostępną ADLS Ustawia limity przepustowości poziomu konta.  Jeśli naciśniesz te limity zostanie uruchomiona toosee niepowodzeń zadań. Może to zostać zidentyfikowane na podstawie obserwowania błędy ograniczania przepustowości w dziennikach zadań.  Jeśli potrzebujesz większej przepustowości dla zadania, skontaktuj się z nami.   

toocheck, jeśli są możesz pobierania ograniczane, należy debugowania hello tooenable rejestrowanie na powitania po stronie klienta. Oto, jak można to zrobić:

1. Umieść hello następujących właściwości w właściwości log4j hello w Ambari > YARN > Config > Zaawansowane narzędzia log4j yarn: log4j.logger.com.microsoft.azure.datalake.store=DEBUG

2. Ponownie uruchomić usługę wszystkich hello węzłów/hello config tootake efekt.

3. Jeśli możesz są pobierania ograniczane, zobaczysz kod błędu HTTP 429 hello w pliku dziennika YARN hello. plik dziennika YARN Hello jest /tmp/&lt;użytkownika&gt;/yarn.log

## <a name="examples-toorun"></a>Przykłady tooRun

toodemonstrate jak MapReduce działa na platformie Azure Data Lake Store, poniżej znajdują się niektóre przykładowy kod, które zostało uruchomione w klastrze z hello następujące ustawienia:

* węzeł 16 D14v2
* Uruchomiona 3,6 HDI klastra usługi Hadoop

Punkt początkowy poniżej przedstawiono niektóre przykładowe polecenia toorun MapReduce Teragen, Terasort i Teravalidate.  Można dostosować tych poleceń, w oparciu o Twoich zasobów.

**Teragen**

    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teragen -Dmapreduce.job.maps=2048 -Dmapreduce.map.memory.mb=3072 10000000000 adl://example/data/1TB-sort-input

**Terasort**

    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar terasort -Dmapreduce.job.maps=2048 -Dmapreduce.map.memory.mb=3072 -Dmapreduce.job.reduces=512 -Dmapreduce.reduce.memory.mb=3072 adl://example/data/1TB-sort-input adl://example/data/1TB-sort-output

**Teravalidate**

    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teravalidate -Dmapreduce.job.maps=512 -Dmapreduce.map.memory.mb=3072 adl://example/data/1TB-sort-output adl://example/data/1TB-sort-validate
