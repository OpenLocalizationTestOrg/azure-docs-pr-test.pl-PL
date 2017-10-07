---
title: "instruktaże Spark aaaHDInsight przy użyciu PySpark i Scala na platformie Azure | Dokumentacja firmy Microsoft"
description: "Przykłady hello zespołu w procesie nauki danych, których przeprowadzenie hello w systemie PySpark i Scala analizy predykcyjnej toodo Azure HDInsight Spark."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: bradsev
ms.openlocfilehash: f8b41a8cae414586570761ba4b4eb4c239cbb981
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="hdinsight-spark-data-science-walkthroughs-using-pyspark-and-scala-on-azure"></a>HDInsight Spark nauki wskazówki dotyczące danych przy użyciu PySpark i Scala na platformie Azure

Te wskazówki w systemie PySpark i Scala toodo klastra Azure Spark dla analizy predykcyjnej. One wykonaj kroki hello opisane w hello proces nauki danych zespołu. Omówienie hello zespołu w procesie nauki danych, zobacz [proces nauki danych](data-science-process-overview.md). Omówienie Spark w usłudze HDInsight, zobacz [tooSpark wprowadzenie w usłudze HDInsight](../hdinsight/hdinsight-apache-spark-overview.md).

Wskazówki dotyczące nauki dodatkowych danych, wykonujących hello proces nauki danych Team są pogrupowane według hello **platformy** obsługującego: 

[!INCLUDE [tdsp-walkthroughs-by-platform](../../includes/tdsp-walkthroughs-by-platform.md)]

## <a name="predict-taxi-tips-using-pyspark-on-azure-spark"></a>Przewidywanie taksówki porady na Azure Spark przy użyciu PySpark

Witaj [korzystanie z platformy Spark w usłudze Azure HDInsight](machine-learning-data-science-spark-overview.md) wskazówki korzysta z nowego Jorku taksówkach toopredict danych czy otrzymuje porady i zakres hello kwot oczekiwano toobe płatnej. Używa hello proces nauki danych zespołu w scenariuszu przy użyciu [klastra Spark w usłudze HDInsight Azure](https://azure.microsoft.com/services/hdinsight/) toostore, Eksploruj, funkcję odtwarzania danych z hello publicznie dostępnych NYC taksówki podróży i taryfy zestawu danych. Ten temat konfiguruje możesz z klastra Spark w usłudze HDInsight i hello Jupyter PySpark notesów używane w hello reszty hello wskazówki. Te komputery przenośne przedstawia sposób tooexplore danych i jak następnie toocreate i korzystanie z modeli. Hello zaawansowane Eksploracja danych i modelowanie notesu pokazuje sposób tooinclude kominów krzyżowego sprawdzania poprawności, funkcji hyper parametr i oceny modelu.

### <a name="data-exploration-and-modeling-with-spark"></a>Eksploracja danych i modelowanie z Spark 
Eksploruj hello zestawu danych i tworzenie, wynik i oceny hello machine learning modeli pracy nad hello [Tworzenie binarnego klasyfikacji i regresji modeli danych narzędzi Spark MLlib hello](machine-learning-data-science-spark-data-exploration-modeling.md) tematu.

### <a name="model-consumption"></a>Użycie modelu
toolearn modele klasyfikacji i regresji hello tooscore utworzone w tym temacie, zobacz [wynik i ocena modele uczenia wbudowane Spark maszyny](machine-learning-data-science-spark-model-consumption.md).

### <a name="cross-validation-and-hyperparameter-sweeping"></a>Krzyżowe sprawdzanie poprawności i kominów hyperparameter
Zobacz [zaawansowane Eksploracja danych i modelowania z platformy Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) na jak można modeli uczenia przy użyciu kominów krzyżowego sprawdzania poprawności i parametru funkcji hyper.


## <a name="predict-taxi-tips-using-scala-on-azure-spark"></a>Przewidywanie taksówki porady na Azure Spark przy użyciu języka Scala

Witaj [Scala użycia z łącznikiem Spark on Azure](machine-learning-data-science-process-scala-walkthrough.md) wskazówki korzysta z nowego Jorku taksówkach toopredict danych czy otrzymuje porady i zakres hello kwot oczekiwano toobe płatnej. Pokazuje, jak toouse Scala dla zadania uczenia nadzorowanego maszyny z hello Spark machine learning biblioteki (MLlib) i SparkML pakietów w klastrze usługi Azure HDInsight Spark. Przeprowadza użytkownika przez hello zadań, które stanowią hello [proces nauki danych](http://aka.ms/datascienceprocess): wprowadzanie danych i eksploracja, wizualizacji engineering funkcji, modelowania i zużycia modelu. modele Hello wbudowane obejmują Regresja logistyczna i liniowych, losowe lasów i gradientu boosted drzewa.


## <a name="next-steps"></a>Następne kroki

Omówienie hello najważniejsze składniki wchodzące w skład hello zespołu w procesie nauki danych, zobacz [Omówienie procesu nauki danych zespołu](data-science-process-overview.md).

Omówienie cyklu życia procesu nauki danych zespołu hello służy toostructure projektów analizy danych, zobacz [cyklu życia procesu nauki danych zespołu](data-science-process-lifecycle.md). cykl życia Hello opisano kroki hello, z toofinish start, która projektów wykonaj zazwyczaj, gdy są one wykonywane. 

