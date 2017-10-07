---
title: "aaaAzure danych Lake Hive wydajności dostrajanie wytyczne sklepu | Dokumentacja firmy Microsoft"
description: "Dostosowywanie wskazówki dotyczące wydajności Hive usługi Azure Data Lake Store"
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
ms.openlocfilehash: e44daeb6ad3b64e893c709df63b56444a330729f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tuning-guidance-for-hive-on-hdinsight-and-azure-data-lake-store"></a>Wskazówki dotyczące Hive w usłudze HDInsight i usługi Azure Data Lake Store dostrajania wydajności

ustawienia domyślne Hello ustawiono tooprovide dobrą wydajność w wielu innych przypadków użycia.  Dla zapytań intensywne operacje We/Wy gałąź może być Zaczekaj tooget lepszą wydajność ADLS.  

## <a name="prerequisites"></a>Wymagania wstępne

* **Subskrypcja platformy Azure**. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Konto usługi Azure Data Lake Store**. Aby uzyskać instrukcje dotyczące jednego, zobacz toocreate [wprowadzenie do usługi Azure Data Lake Store](data-lake-store-get-started-portal.md)
* **Klaster HDInsight Azure** z tooa dostępu do konta usługi Data Lake Store. Zobacz [tworzenia klastra usługi HDInsight z usługą Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md). Upewnij się, że włączenie pulpitu zdalnego dla klastra hello.
* **Uruchomiona Hive w usłudze HDInsight**.  toolearn o uruchamianiu zadań Hive w usłudze HDInsight, zobacz [używanie Hive w usłudze HDInsight] (https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-use-hive)
* **Wytyczne dotyczące ADLS dostrajania wydajności**.  Pojęcia dotyczące ogólnej wydajności, aby zapoznać [Data Lake magazynu dostrajanie wytyczne dotyczące wydajności](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance)

## <a name="parameters"></a>Parametry

Poniżej przedstawiono najważniejsze tootune ustawienia hello zwiększonej wydajności ADLS:

* **hive.tez.container.SIZE** — Witaj ilość pamięci użytej przez każdego zadania

* **rozmiar tez.GROUPING.min** — minimalny rozmiar każdego mapowania

* **rozmiar tez.GROUPING.max** — maksymalny rozmiar każdego mapowania

* **hive.EXEC.reducer.Bytes.per.reducer** — rozmiar każdego reduktor

**hive.tez.container.SIZE** — rozmiar kontenera hello Określa, ile pamięci dostępnej dla każdego zadania.  Jest to hello głównego wejściowe kontrolowanie współbieżności hello w gałęzi.  

**rozmiar tez.GROUPING.min** — ten parametr umożliwia tooset hello minimalny rozmiar każdego mapowania.  Jeśli liczba hello mapowań, które wybierze Tez jest mniejsza niż hello wartość tego parametru, Tez użyje wartości hello określonego w tym miejscu.  

**rozmiar tez.GROUPING.max** — parametr hello umożliwia tooset hello maksymalny rozmiar każdego mapowania.  Jeśli liczba hello mapowań, które wybierze Tez jest większy niż hello wartość tego parametru, Tez użyje wartości hello określonego w tym miejscu.  

**hive.EXEC.reducer.Bytes.per.reducer** — ten parametr określa rozmiar każdego reduktor hello.  Domyślnie każdy reduktor to 256MB.  

## <a name="guidance"></a>Wskazówki

**Ustaw hive.exec.reducer.bytes.per.reducer** — wartość domyślna hello działa dobrze przypadku nieskompresowanych danych hello.  Dane są kompresowane należy zmniejszyć rozmiar hello reduktor hello.  

**Ustaw hive.tez.container.size** — w każdym węźle jest określona przez yarn.nodemanager.resource.memory mb pamięci i powinien zostać poprawnie określony HDI klastra domyślnie.  Aby uzyskać dodatkowe informacje na temat ustawiania hello odpowiedniej ilości pamięci w YARN, zobacz [post](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-hive-out-of-memory-error-oom).

Intensywnych obciążeń We/Wy mogą korzystać z równoległości więcej przez zmniejszenie rozmiaru kontenera Tez hello. Dzięki temu użytkownik hello więcej kontenerów, co zwiększa współbieżności.  Jednak niektóre zapytania Hive wymagają znaczną ilość pamięci (np. MapJoin).  Jeśli zadanie hello nie ma wystarczającej ilości pamięci, wystąpi wyjątek braku pamięci podczas wykonywania.  Jeśli zostanie wyświetlony poza wyjątkami pamięci, należy zwiększyć hello pamięci.   

liczby równoczesnych Hello jest uruchomione zadanie lub równoległości zostaną ograniczone przez hello całkowitej ilości pamięci YARN.  Witaj liczbę kontenerów YARN wyznaczają liczbę równoczesnych zadań można uruchamiać.  toofind hello YARN pamięć przypadająca na węzeł, możesz przejść tooAmbari.  Przejdź tooYARN, a następnie Wyświetl kartę Configs hello.  Witaj YARN pamięci jest wyświetlany w tym oknie.  

        Total YARN memory = nodes * YARN memory per node
        # of YARN containers = Total YARN memory / Tez container size
Hello klucza tooimproving wydajności przy użyciu ADLS jest możliwie współbieżności hello tooincrease.  Tez automatycznie oblicza hello liczba zadań, które ma zostać utworzona, więc nie trzeba tooset go.   

## <a name="example-calculation"></a>Przykład obliczeń

Załóżmy, że klaster D14 8 węzłów.  

    Total YARN memory = nodes * YARN memory per node
    Total YARN memory = 8 nodes * 96GB = 768GB
    # of YARN containers = 768GB / 3072MB = 256

## <a name="limitations"></a>Ograniczenia
**ADLS ograniczania przepustowości** 

UIf trafień hello limity przepustowości, pod warunkiem za pomocą ADLS, czy uruchomić toosee niepowodzeń zadań. Może to być identyfikowany przez obserwowania błędy ograniczania przepustowości w dziennikach zadań.  Możesz zmniejszyć równoległości hello przez zwiększenie rozmiaru kontenera aplikacji Tez.  Jeśli potrzebujesz więcej współbieżności dla zadania, skontaktuj się z nami.   

toocheck, jeśli są możesz pobierania ograniczane, należy debugowania hello tooenable rejestrowanie na powitania po stronie klienta. Oto, jak można to zrobić:

1. Umieść hello następujące właściwości we właściwościach log4j hello w pliku konfiguracyjnym Hive. Można to zrobić z widoku Ambari: log4j.logger.com.microsoft.azure.datalake.store=DEBUG ponownie uruchomić usługę wszystkich hello węzłów/hello config tootake efekt.

2. Jeśli możesz są pobierania ograniczane, zobaczysz kod błędu HTTP 429 hello w pliku dziennika gałęzi hello. plik dziennika hive Hello jest /tmp/&lt;użytkownika&gt;/hive.log

## <a name="further-information-on-hive-tuning"></a>Więcej informacji na temat dostrajania gałęzi

Poniżej przedstawiono kilka blogi, pomagających dostroić zapytań Hive:
* [Optymalizacja zapytań programu Hive dla platformy Hadoop w usłudze HDInsight](https://azure.microsoft.com/en-us/documentation/articles/hdinsight-hadoop-optimize-hive-query/)
* [Rozwiązywanie problemów z wydajność zapytań Hive](https://blogs.msdn.microsoft.com/bigdatasupport/2015/08/13/troubleshooting-hive-query-performance-in-hdinsight-hadoop-cluster/)
* [Rozmawiać z konferencji Ignite na optymalizowanie Hive w usłudze HDInsight](https://channel9.msdn.com/events/Machine-Learning-and-Data-Sciences-Conference/Data-Science-Summit-2016/MSDSS25)
