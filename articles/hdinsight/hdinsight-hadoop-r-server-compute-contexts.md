---
title: "Opcje kontekstu aaaCompute R Server w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o hello różnych obliczeń kontekstu opcje dostępne toousers z serwerem R w usłudze HDInsight"
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
ms.openlocfilehash: b3b0d0cc3caa390797dcff8c73d66cd3ad78bcaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="compute-context-options-for-r-server-on-hdinsight"></a>Obliczenia bazy danych kontekstu opcje serwera R w usłudze HDInsight

Microsoft R Server w usłudze Azure HDInsight kontroluje sposób wywołania są wykonywane przez ustawienie hello kontekstu obliczeń. W tym artykule opisano opcje hello, które są dostępne toospecify czy i jak wykonanie jest zarządzana z przetwarzaniem na rdzeni węzła krawędzi hello lub klastra usługi HDInsight.

Witaj krawędzi węzła klastra zawiera wygodne miejsce tooconnect toohello klastra i toorun skrypty języka R. Z węzłem krawędzi masz hello opcja uruchomionych hello zarządzana z przetwarzaniem rozproszonych funkcji ScaleR na powitania rdzeni hello krawędzi węzeł serwera. Można również uruchomić je w węzłach hello hello klastra przy użyciu Zmniejsz mapy platformy Hadoop w ScaleR lub Spark kontekstów obliczeń.

## <a name="microsoft-r-server-on-azure-hdinsight"></a>Serwer Microsoft R w usłudze Azure HDInsight
[Microsoft R Server w usłudze Azure HDInsight](hdinsight-hadoop-r-server-overview.md) zapewnia hello najnowsze możliwości analizy na podstawie R. Można użyć danych przechowywanych w kontenerze systemu plików HDFS w Twojej [obiektów Blob platformy Azure](../storage/common/storage-introduction.md "magazynu obiektów Blob Azure") konta magazynu, Data Lake store lub hello lokalny system plików systemu Linux. Ponieważ serwer R jest oparty na typu open source R, można zastosować hello R aplikacji tworzonych żadnych pakietów hello 8000 + R typu open source. Można też procedury hello w [RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler), pakiet analizy danych big data firmy Microsoft jest dołączony serwer R.  

## <a name="compute-contexts-for-an-edge-node"></a>Obliczenia bazy danych kontekstów dla węzła krawędzi
Ogólnie rzecz biorąc skrypt języka R, uruchamiany w R Server w węźle krawędzi hello jest uruchamiany w ramach interpreter hello R w tym węźle. Wyjątki Hello są te kroki, które wywołują funkcję ScaleR. Uruchom Hello ScaleR wywołania w środowisku obliczeniowe, które określają sposób ustawiania kontekstu obliczeń ScaleR hello.  Po uruchomieniu skryptu języka R z węzłem krawędzi hello możliwe wartości hello obliczeniowe są kontekstu:

- lokalny sekwencyjnych (*"local"*)
- równoległe lokalnego (*"localpar"*)
- Zmniejsz mapy
- platforma Spark

Witaj *"local"* i *"localpar"* opcje różnią się tylko w sposób **rxExec** wywołania są wykonywane. Oba wykonać inne wywołania funkcji odbierania w sposób równoległy między wszystkie dostępne rdzenie chyba że określono inaczej, za pomocą hello ScaleR **numCoresToUse** opcji, na przykład `rxOptions(numCoresToUse=6)`. Opcje przetwarzania równoległego oferują optymalną wydajność.

Witaj w poniższej tabeli znajduje się podsumowanie hello różnych obliczeniowe tooset opcje kontekstu sposobu wykonywania wywołań:

| Obliczenia bazy danych kontekstu  | Jak tooset                      | Kontekst wykonywania                        |
| ---------------- | ------------------------------- | ---------------------------------------- |
| Lokalny sekwencyjne | rxSetComputeContext('local')    | Wykonanie zrównoleglone na powitania rdzeni powitania serwera węzła krawędzi, z wyjątkiem rxExec wywołań, które są wykonywane szeregowo |
| Równoległe lokalnego   | rxSetComputeContext('localpar') | Wykonanie zrównoleglone na powitania rdzeni hello krawędzi węzła serwera |
| platforma Spark            | RxSpark()                       | Zrównoleglone rozproszonego wykonywania za pośrednictwem platformy Spark w węzłach hello hello klastra HDI |
| Zmniejsz mapy       | RxHadoopMR()                    | Zrównoleglone rozproszonego wykonywania przy użyciu mapy zmniejszyć w węzłach hello hello klastra HDI |

## <a name="guidelines-for-deciding-on-a-compute-context"></a>Wytyczne dotyczące podejmowania decyzji o w kontekście obliczeń

Hello trzech opcji wybierzesz umożliwiających wykonanie zrównoleglone zależnej od charakteru hello pracy analytics, rozmiar hello i hello lokalizację danych. Nie ma żadnych prostej formuły, informujący o którym obliczeniowe toouse kontekstu. Istnieją jednak niektóre wytyczne, które mogą pomóc Ci wybrać opcje hello lub co najmniej pomóc zawęzić wybór przed uruchomieniem testu porównawczego. Obejmują one wytyczne:

- lokalny system plików Linux Hello jest szybsza niż system plików HDFS.
- Powtórzony analizy są szybsze danych hello jest lokalny, a jest XDF.
- Jest preferowana toostream niewielkich ilości danych ze źródła danych tekstowych. Jeśli hello ilości danych jest większy, przekonwertuj go tooXDF przed analizą.
- koszty Hello kopiowania lub przesyłania strumieniowego węzła krawędzi toohello hello danych do analizy staje się bezproblemowego zarządzania dla bardzo dużych ilości danych.
- Platforma Spark jest szybsza niż mapa zmniejszyć do analizy w Hadoop.

Podana tych zasad, hello poniższe sekcje zapewniają pewne ogólne reguły przyjąć wybierania kontekstu obliczeń.

### <a name="local"></a>Lokalna
* Jeśli hello ilość danych tooanalyze jest mała i nie wymaga oczekiwanego, następnie strumienia go bezpośrednio w użyciu rutynowych analizy hello *"local"* lub *"localpar"*.
* Jeśli hello ilość danych tooanalyze jest małych i średnich i wymaga oczekiwanego, następnie skopiuj go toohello lokalnego systemu plików, zaimportuj go tooXDF i przeanalizuj go za pomocą *"local"* lub *"localpar"*.

### <a name="hadoop-spark"></a>Hadoop, Spark
* Jeśli ilość hello tooanalyze danych jest duży, następnie zaimportuj go tooa Spark DataFrame przy użyciu **RxHiveData** lub **RxParquetData**, lub tooXDF w systemie plików HDFS (chyba, że magazyn jest problemu) i przeanalizuj go przy użyciu hello Spark obliczenia bazy danych kontekstu.

### <a name="hadoop-map-reduce"></a>Zmniejsz mapy usługi Hadoop
* Użyj kontekstu obliczeń zmniejszyć mapy hello tylko wtedy, gdy wystąpią porównania problem z kontekstem obliczeń Spark hello, ponieważ jest ono zazwyczaj wolniej.  

## <a name="inline-help-on-rxsetcomputecontext"></a>Wbudowany pomoc na temat rxSetComputeContext
Aby uzyskać dodatkowe informacje i przykłady ScaleR obliczeniowe kontekstów, zobacz wbudowanego hello pomoc w R na powitania rxSetComputeContext metody, na przykład:

    > ?rxSetComputeContext

Można także odwoływać się toohello "[przewodnik rozproszonego przetwarzania danych ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-distributed-computing)" nie jest dostępna z hello [R Server w witrynie MSDN](https://msdn.microsoft.com/library/mt674634.aspx "R Server w witrynie MSDN") biblioteki.

## <a name="next-steps"></a>Następne kroki
W tym artykule przedstawiono o opcjach hello, które są dostępne toospecify czy i jak wykonanie jest zarządzana z przetwarzaniem na rdzeni węzła krawędzi hello lub klastra usługi HDInsight. toolearn więcej informacji na temat sposobu klastrów toouse R Server z usługą HDInsight, zobacz następujące tematy hello:

* [Omówienie R Server dla usługi Hadoop](hdinsight-hadoop-r-server-overview.md)
* [Rozpoczynanie pracy z R Server dla platformy Hadoop](hdinsight-hadoop-r-server-get-started.md)
* [Dodaj serwer programu RStudio tooHDInsight (Jeśli nie dodano podczas tworzenia klastra)](hdinsight-hadoop-r-server-install-r-studio.md)
* [Azure Storage options for R Server on HDInsight](hdinsight-hadoop-r-server-storage.md) (Opcje usługi Azure Storage dla oprogramowania R Server w usłudze HDInsight)

