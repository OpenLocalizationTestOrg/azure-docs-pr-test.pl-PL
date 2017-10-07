---
title: "aaaAzure danych Lake Spark wydajności dostrajanie wytyczne sklepu | Dokumentacja firmy Microsoft"
description: "Dostosowywanie wskazówki dotyczące wydajności Spark usługi Azure Data Lake Store"
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
ms.openlocfilehash: da1d172e9cb1199ad95605ea1718e78559f79650
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tuning-guidance-for-spark-on-hdinsight-and-azure-data-lake-store"></a>Wskazówki dotyczące platforma Spark w usłudze HDInsight i usługi Azure Data Lake Store dostrajania wydajności

Dostrajanie wydajności na Spark, konieczne jest tooconsider hello liczba aplikacje działające w klastrze.  Domyślnie program można uruchomić 4 aplikacji równocześnie na klaster HDI (Uwaga: hello domyślne ustawienie to toochange podmiotu).  Użytkownik może zdecydować toouse mniej aplikacji może zastąpić ustawienia domyślne hello i użyć więcej hello klastra dla tych aplikacji.  

## <a name="prerequisites"></a>Wymagania wstępne

* **Subskrypcja platformy Azure**. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Konto usługi Azure Data Lake Store**. Aby uzyskać instrukcje dotyczące jednego, zobacz toocreate [wprowadzenie do usługi Azure Data Lake Store](data-lake-store-get-started-portal.md)
* **Klaster HDInsight Azure** z tooa dostępu do konta usługi Data Lake Store. Zobacz [tworzenia klastra usługi HDInsight z usługą Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md). Upewnij się, że włączenie pulpitu zdalnego dla klastra hello.
* **Uruchomiona klastra Spark w usłudze Azure Data Lake Store**.  Aby uzyskać więcej informacji, zobacz [dane tooanalyze klastra HDInsight korzystanie z platformy Spark w usłudze Data Lake Store](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-use-with-data-lake-store)
* **Wytyczne dotyczące ADLS dostrajania wydajności**.  Pojęcia dotyczące ogólnej wydajności, aby zapoznać [Data Lake magazynu dostrajanie wytyczne dotyczące wydajności](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance) 

## <a name="parameters"></a>Parametry

Podczas uruchamiania zadań Spark, Oto hello najważniejszych ustawień, które mogą być wydajności tooincrease Zaczekaj na ADLS:

* **Liczba modułów** — Witaj liczba równoczesnych zadań, które mogą być wykonywane.

* **Moduł wykonujący pamięci** -hello ilość pamięci przydzielonej tooeach Moduł wykonujący.

* **Moduł wykonujący rdzeni** -hello liczba rdzeni przydzielone tooeach Moduł wykonujący.                     

**Liczba modułów** modułów Num ustawi hello maksymalna liczba zadań, które można uruchomić równolegle.  Rzeczywista liczba zadań, które można uruchomić równolegle Hello jest ograniczone przez hello pamięć i zasoby Procesora dostępne w klastrze.

**Moduł wykonujący pamięci** to hello ilość pamięci, która jest przydzielane tooeach Moduł wykonujący.  wymagane dla każdego modułu wykonującego pamięci Hello jest zależna od hello zadania.  W przypadku złożonych operacji hello pamięci musi toobe wyższy.  Proste operacje, takie jak odczytu i zapisu wymagania dotyczące pamięci będzie niższa.  ilość pamięci dla każdego modułu wykonującego Hello można wyświetlić w narzędzia Ambari.  W Ambari Przejdź tooSpark i wyświetl kartę Configs hello.  

**Moduł wykonujący rdzeni** to ustawia hello liczbę rdzeni na moduł wykonujący określającą hello liczba równoległych wątków, które mogą być uruchamiane na moduł wykonujący.  Na przykład jeśli moduł wykonujący rdzeni = 2, a następnie każdy moduł wykonujący można uruchamiać zadania równoległych 2 hello Moduł wykonujący.  Program Hello — rdzenie potrzebne będzie zależało od hello zadania.  Duże zadania We/Wy nie wymaga dużej ilości pamięci poszczególnych zadań, dzięki czemu można każdy moduł wykonujący może obsługiwać więcej zadań równoległych.

Domyślnie dwa rdzenie YARN wirtualnych są definiowane dla każdego rdzeni fizycznych uruchomionej w usłudze HDInsight Spark.  Liczba ta zapewnia kompromis concurrecy oraz ilości wiele wątków do przełączania kontekstu.  

## <a name="guidance"></a>Wskazówki

Podczas uruchamiania Spark toowork analityczne obciążeń z danymi w usłudze Data Lake Store, zalecane jest użycie hello najnowszych HDInsight wersji tooget hello najlepszą wydajność z usługą Data Lake Store. Gdy zadanie jest bardziej intensywne operacje We/Wy, niektóre parametry mogą być skonfigurowany tooimprove wydajności.  Azure Data Lake Store jest platformy wysokiej skalowalności magazynu, który może obsługiwać wysokiej przepływności.  Jeśli zadanie hello zawiera głównie odczytu lub zapisu, następnie zwiększenie współbieżności dla operacji We/Wy tooand z usługi Azure Data Lake Store może zwiększyć wydajność.

Istnieje kilka sposobów ogólne tooincrease współbieżności zadań intensywne operacje We/Wy.

**Krok 1: Określanie, jak wiele aplikacji uruchomionych w klastrze** — należy wiedzieć, jak wiele aplikacji są uruchomione w klastrze hello hello bieżącym włącznie.  wartości domyślne powitania dla każdego Spark ustawienia obowiązuje założenie, które istnieją 4 równoczesne działanie aplikacji.  W związku z tym będzie mieć tylko 25% klastra hello dostępne dla każdej aplikacji.  tooget lepszą wydajność, można zastąpić wartości domyślne hello zmieniając hello liczba modułów.  

**Krok 2: Ustawić modułu wykonującego pamięci** — Witaj po pierwsze tooset jest moduł wykonujący hello pamięci.  pamięć Hello będzie zależna od zadania hello czy toorun będzie.  Można zwiększyć współbieżność przydzielając mniejszą ilość pamięci na moduł wykonujący.  Jeśli widzisz poza wyjątkami pamięci podczas uruchamiania zadania, należy zwiększyć wartość tego parametru hello.  Jeden alternatywą jest tooget większej ilości pamięci za pomocą klastra, który ma większych ilości pamięci lub zwiększyć rozmiar hello klastra.  Więcej pamięci umożliwi więcej toobe modułów używane, co oznacza więcej współbieżności.

**Krok 3: Ustawianie rdzeni Moduł wykonujący** — we/wy intensywnych obciążeń, które nie mają złożonych operacji, jest dobrym toostart z dużej liczby rdzeni Moduł wykonujący tooincrease hello liczbę równoległych zadań na moduł wykonujący.  Ustawienie too4 rdzeni Moduł wykonujący stanowi dobry początek.   

    executor-cores = 4
Zwiększenie liczby hello rdzeni Moduł wykonujący zapewni więcej równoległości, możesz eksperymentować z różnych rdzeni Moduł wykonujący.  Dla zadania, których bardziej złożonych operacji należy zmniejszyć hello liczba rdzeni w moduł wykonujący.  Jeśli moduł wykonujący rdzeni jest wyższa niż 4, następnie wyrzucanie elementów bezużytecznych mogą się nieefektywne i obniżyć wydajność.

**Krok 4: Określanie ilości pamięci YARN w klastrze** — te informacje są dostępne w narzędzia Ambari.  Przejdź tooYARN, a następnie Wyświetl kartę Configs hello.  Witaj YARN pamięci jest wyświetlany w tym oknie.  
Uwaga: podczas pracy w oknie hello jest również widoczna hello domyślny YARN kontenera rozmiar.  rozmiar kontenera YARN Hello jest hello taki sam jak ilość pamięci na parametru Moduł wykonujący.

    Total YARN memory = nodes * YARN memory per node
**Krok 5: Oblicz num modułów**

**Oblicz ograniczenie pamięci** — parametr num modułów hello jest ograniczony przez pamięci lub procesora CPU.  Ograniczenie pamięci Hello jest określana przez hello ilość dostępnej pamięci YARN dla aplikacji.  Należy podjąć YARN pamięć i przez moduł wykonujący pamięci.  ograniczenie Hello musi toobe cofnąć skalowania dla wielu aplikacji hello, możemy podzielić przez hello liczba aplikacji.

    Memory constraint = (total YARN memory / executor memory) / # of apps   
**Obliczanie Procesora ograniczenia** -hello ograniczenie procesora CPU jest obliczany jako hello całkowita liczba rdzeni wirtualnego rozdzielonych hello liczba rdzeni w moduł wykonujący.  Istnieją 2 rdzenie wirtualnych dla poszczególnych rdzeni fizycznych.  Ograniczenie pamięci toohello podobne, mamy dzielenia przez hello liczba aplikacji.

    virtual cores = (nodes in cluster * # of physical cores in node * 2)
    CPU constraint = (total virtual cores / # of cores per executor) / # of apps
**Ustaw modułów num** — parametr num modułów hello jest określana przez pobranie hello minimum hello pamięci ograniczenia i ograniczenia hello procesora CPU. 

    num-executors = Min (total virtual Cores / # of cores per executor, available YARN memory / executor-memory)   
Ustawienie większej liczby modułów num nie zawsze poprawia wydajność.  Należy rozważyć dodanie więcej modułów spowoduje dodanie czy bardzo ogólnych, dla każdego dodatkowego Moduł wykonujący, które potencjalnie może zmniejszyć wydajność.  Liczba modułów jest ograniczone przez hello zasobów klastra.    

## <a name="example-calculation"></a>Przykład obliczeń

Załóżmy, że masz obecnie klaster składa się z 8 węzłów D4v2 2 uruchomionej aplikacji hello w tym co ma toorun.  

**Krok 1: Określanie, jak wiele aplikacji uruchomionych w klastrze** — wiesz, że masz 2 aplikacji w klastrze, w tym hello, co ma toorun.  

**Krok 2: Ustawić modułu wykonującego pamięci** — na przykład możemy ustalić, czy 6 GB pamięci Moduł wykonujący są wystarczające dla zadania intensywne operacje We/Wy.  

    executor-memory = 6GB
**Krok 3: Ustawianie rdzeni Moduł wykonujący** — ponieważ jest to zadanie intensywne operacje We/Wy, możemy ustawić hello liczba rdzeni dla każdego too4 Moduł wykonujący.  Ustawienie rdzeni w jednym toolarger Moduł wykonujący niż 4 może spowodować problemy z kolekcji pamięci.  

    executor-cores = 4
**Krok 4: Określanie ilości pamięci YARN w klastrze** — możemy przejść toofind tooAmbari się, że każdy D4v2 ma 25 GB pamięci YARN.  Ponieważ 8 węzłów, dostępnej pamięci YARN hello jest mnożona przez 8.

    Total YARN memory = nodes * YARN memory* per node
    Total YARN memory = 8 nodes * 25GB = 200GB
**Krok 5: Oblicz modułów num** — parametr num modułów hello jest określana przez pobranie hello minimalna hello pamięci ograniczenia i ograniczenie Procesora hello rozdzielonych hello # aplikacje działające na Spark.    

**Oblicz ograniczenie pamięci** — ograniczenie pamięci hello jest obliczany jako hello całkowita pamięć YARN podzielona przez ilość pamięci hello na moduł wykonujący.

    Memory constraint = (total YARN memory / executor memory) / # of apps   
    Memory constraint = (200GB / 6GB) / 2   
    Memory constraint = 16 (rounded)
**Obliczanie Procesora ograniczenia** -hello ograniczenie procesora CPU jest liczony jako hello yarn całkowita liczba rdzeni rozdzielonych hello liczba rdzeni w moduł wykonujący.
    
    YARN cores = nodes in cluster * # of cores per node * 2   
    YARN cores = 8 nodes * 8 cores per D14 * 2 = 128
    CPU constraint = (total YARN cores / # of cores per executor) / # of apps
    CPU constraint = (128 / 4) / 2
    CPU constraint = 16
**Zestaw num modułów**

    num-executors = Min (memory constraint, CPU constraint)
    num-executors = Min (16, 16)
    num-executors = 16    

