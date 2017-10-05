---
title: "Opcje kontekstu platformy R Server w usłudze HDInsight - Azure obliczania | Dokumentacja firmy Microsoft"
description: "Informacje na temat opcji kontekstu obliczeń różne dostępne dla użytkowników z serwerem R w usłudze HDInsight"
services: HDInsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 0deb0b1c-4094-459b-94fc-ec9b774c1f8a
ms.service: HDInsight
ms.custom: hdinsightactive
ms.devlang: R
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: 47f4441612be4f363ba82cc22b09786a6f3bfdc3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="compute-context-options-for-r-server-on-hdinsight"></a>Obliczenia bazy danych kontekstu opcje serwera R w usłudze HDInsight

Microsoft R Server w usłudze Azure HDInsight kontroluje sposób wywołania są wykonywane przez ustawienie kontekstu obliczeń. W tym artykule opisano opcje, które są dostępne określić, czy i jak wykonanie jest zarządzana z przetwarzaniem na rdzeni węzła krawędzi lub klastra usługi HDInsight.

Węzeł krawędzi klastra umożliwia wygodne Połącz się z klastrem i uruchamiania skryptów R. Z węzłem krawędzi istnieje możliwość uruchomionych zrównoleglone funkcje rozproszonej ScaleR na rdzeni serwera węzła krawędzi. Można również uruchomić je w węzłach klastra przy użyciu jego ScaleR Hadoop mapy zmniejszyć lub Spark obliczeniowe kontekstach.

## <a name="microsoft-r-server-on-azure-hdinsight"></a>Serwer Microsoft R w usłudze Azure HDInsight
[Microsoft R Server w usłudze Azure HDInsight](hdinsight-hadoop-r-server-overview.md) zawiera najnowsze funkcje analizy na podstawie R. Można użyć danych przechowywanych w kontenerze systemu plików HDFS w Twojej [obiektów Blob platformy Azure](../storage/common/storage-introduction.md "magazynu obiektów Blob Azure") konta magazynu, Data Lake store lub lokalny system plików w systemie Linux. Ponieważ R Server jest zbudowany na typu open source R, można zastosować R aplikacji tworzonych żadnych pakietów 8000 + R typu open source. Można też procedury w [RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler), pakiet analizy danych big data firmy Microsoft jest dołączony serwer R.  

## <a name="compute-contexts-for-an-edge-node"></a>Obliczenia bazy danych kontekstów dla węzła krawędzi
Ogólnie rzecz biorąc skrypt języka R, uruchamiany w R Server dla węzła krawędzi jest uruchamiany w ramach interpreter języka R w tym węźle. Wyjątki są te kroki, które wywołują funkcję ScaleR. Wywołania ScaleR uruchomione w środowisku obliczeniowe, które określają sposób ustawiania kontekstu obliczeń ScaleR.  Po uruchomieniu skryptu języka R z węzłem krawędzi, możliwe wartości kontekstu obliczeń to:

- lokalny sekwencyjnych (*"local"*)
- równoległe lokalnego (*"localpar"*)
- Zmniejsz mapy
- platforma Spark

*"Local"* i *"localpar"* opcje różnią się tylko w sposób **rxExec** wywołania są wykonywane. Oba wykonać inne wywołania funkcji odbierania w sposób równoległy między wszystkie dostępne rdzenie chyba że określono inaczej, za pomocą ScaleR **numCoresToUse** opcji, na przykład `rxOptions(numCoresToUse=6)`. Opcje przetwarzania równoległego oferują optymalną wydajność.

W poniższej tabeli przedstawiono różne opcje kontekstu obliczeń ustalenie sposobu wykonywania wywołań:

| Obliczenia bazy danych kontekstu  | Jak ustawić                      | Kontekst wykonywania                        |
| ---------------- | ------------------------------- | ---------------------------------------- |
| Lokalny sekwencyjne | rxSetComputeContext('local')    | Wykonanie zrównoleglone między rdzenie serwera węzła krawędzi, z wyjątkiem rxExec wywołań, które są wykonywane szeregowo |
| Równoległe lokalnego   | rxSetComputeContext('localpar') | Wykonanie zrównoleglone między rdzenie serwera granicznego węzła |
| platforma Spark            | RxSpark()                       | Zrównoleglone rozproszonego wykonywania za pośrednictwem platformy Spark w węzłach klastra HDI |
| Zmniejsz mapy       | RxHadoopMR()                    | Zrównoleglone rozproszonego wykonywania przy użyciu mapy zmniejszyć w węzłach klastra HDI |

## <a name="guidelines-for-deciding-on-a-compute-context"></a>Wytyczne dotyczące podejmowania decyzji o w kontekście obliczeń

Z trzech opcji wybierzesz umożliwiających wykonanie zrównoleglone zależnej od charakteru pracy analytics, rozmiar i lokalizację danych. Nie ma żadnych prostej formuły, informujący o którym obliczeniowe kontekst do użycia. Istnieją jednak niektóre wytyczne, które mogą pomóc Ci wybrać odpowiednie opcje lub co najmniej pomóc zawęzić wybór przed uruchomieniem testu porównawczego. Obejmują one wytyczne:

- Lokalny system plików systemu Linux jest szybsza niż system plików HDFS.
- Jeśli dane są lokalne, a jeśli XDF, szybsze są powtarzane analizy.
- Zaleca się do przesyłania strumieniowego niewielkich ilości danych ze źródła danych tekstowych. W przypadku większych ilości danych, przekonwertować go na XDF przed analizą.
- Koszty kopiowania lub strumieniowe przesyłanie danych z węzłem krawędzi do analizy staje się bezproblemowego zarządzania dla bardzo dużych ilości danych.
- Platforma Spark jest szybsza niż mapa zmniejszyć do analizy w Hadoop.

Podana tych zasad, poniższe sekcje zapewniają pewne ogólne reguły przyjąć wybierania kontekstu obliczeń.

### <a name="local"></a>Lokalna
* Jeśli ilość danych w celu przeanalizowania jest mała i nie wymaga oczekiwanego, następnie strumienia go bezpośrednio do analizy rutynowych użyciu *"local"* lub *"localpar"*.
* Jeśli ilość danych w celu przeanalizowania jest małych i średnich i wymaga oczekiwanego, następnie skopiować go do lokalnego systemu plików, zaimportuj go do XDF i analizować go za pomocą *"local"* lub *"localpar"*.

### <a name="hadoop-spark"></a>Hadoop, Spark
* W przypadku dużych ilości danych do analizy, następnie zaimportować go do Spark DataFrame przy użyciu **RxHiveData** lub **RxParquetData**, lub XDF w systemie plików HDFS (chyba, że magazyn jest problemu) i przeanalizuj go przy użyciu obliczeniowych Spark kontekst.

### <a name="hadoop-map-reduce"></a>Zmniejsz mapy usługi Hadoop
* Tylko wtedy, gdy wystąpią porównania problem z kontekstem obliczeń Spark, ponieważ jest ono zazwyczaj wolniej, należy używać kontekstu obliczeń zmniejszyć mapy.  

## <a name="inline-help-on-rxsetcomputecontext"></a>Wbudowany pomoc na temat rxSetComputeContext
Dodatkowe informacje i przykłady ScaleR kontekstów obliczeń dla wbudowanego pomoc w R w metodzie rxSetComputeContext, na przykład:

    > ?rxSetComputeContext

Można także odwoływać się do "[przewodnik rozproszonego przetwarzania danych ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-distributed-computing)" nie jest dostępna z [R Server w witrynie MSDN](https://msdn.microsoft.com/library/mt674634.aspx "R Server w witrynie MSDN") biblioteki.

## <a name="next-steps"></a>Następne kroki
W tym artykule przedstawiono o opcjach, które są dostępne określić, czy i jak wykonanie jest zarządzana z przetwarzaniem na rdzeni węzła krawędzi lub klastra usługi HDInsight. Aby dowiedzieć się więcej o sposobie używania R Server z klastrami usługi HDInsight, zobacz następujące tematy:

* [Omówienie R Server dla usługi Hadoop](hdinsight-hadoop-r-server-overview.md)
* [Rozpoczynanie pracy z R Server dla platformy Hadoop](hdinsight-hadoop-r-server-get-started.md)
* [Dodaj serwer programu RStudio do HDInsight (Jeśli nie dodano podczas tworzenia klastra)](hdinsight-hadoop-r-server-install-r-studio.md)
* [Azure Storage options for R Server on HDInsight](hdinsight-hadoop-r-server-storage.md) (Opcje usługi Azure Storage dla oprogramowania R Server w usłudze HDInsight)

