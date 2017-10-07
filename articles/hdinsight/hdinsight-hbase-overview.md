---
title: "aaaWhat jest baza danych HBase w usłudze Azure HDInsight? | Microsoft Docs"
description: "TooApache wprowadzenie bazy danych HBase w usłudze HDInsight, bazę danych NoSQL kompilacji na platformie Hadoop. Dowiedz się więcej o przypadkach użycia i porównaj klastrów platformy Hadoop tooother HBase."
keywords: bigtable,nosql,what is hbase,apache hbase,hbase,habase overview,
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: d2a76d53-133a-4849-a30c-88d9c794391c
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: 0d28378d07b1a168e38748548578be11310d2228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hbase-in-hdinsight-a-nosql-database-that-provides-bigtable-like-capabilities-for-hadoop"></a>Czym jest baza danych HBase w usłudze HDInsight: jest to baza danych NoSQL o możliwościach analogicznych do bazy danych BigTable dla platformy Hadoop
Apache HBase jest bazą danych NoSQL typu open source opartą na platformie Hadoop i wzorowaną na bazie danych Google BigTable. Baza danych HBase zapewnia dostęp losowy i wysoki poziom spójności w przypadku dużych ilości danych z częściową strukturą i bez struktury w bezschematowej bazie danych zorganizowanej według rodzin kolumn.

Dane są przechowywane w hello wiersze tabeli, a dane w obrębie wiersza są grupowane według rodziny kolumn. HBase jest bezschematową bazą danych ani hello kolumn ani hello typu danych przechowywanych w nich znaczeniu hello muszą toobe zdefiniowane przed ich użyciem. Witaj kodu open source zapewnia Skalowanie liniowe toohandle petabajtów danych na tysiącach węzłów. Baza może wykorzystywać nadmiarowość danych, przetwarzanie wsadowe i inne funkcje, które są dostarczane przez aplikacje rozproszone w ekosystemie Hadoop hello.

## <a name="how-is-hbase-implemented-in-azure-hdinsight"></a>W jaki sposób baza danych HBase jest zaimplementowana w systemie Azure HDInsight?
HDInsight HBase jest oferowana jako zarządzany klaster zintegrowany hello środowiska platformy Azure. klastry Hello są skonfigurowane toostore danych bezpośrednio w [usługi Azure Storage](./hdinsight-hadoop-use-blob-storage.md) lub [Azure Data Lake Store](./hdinsight-hadoop-use-data-lake-store.md), który zapewnia małe opóźnienia i zwiększoną elastyczność w zakresie wydajności i kosztów. Dzięki temu klienci toobuild interaktywne witryny sieci Web pracować z dużymi zestawami danych, usługi toobuild przechowywania danych czujników i danych telemetrycznych z milionów punktów końcowych i tooanalyze te dane przy użyciu zadań platformy Hadoop. HBase i Hadoop są dobrymi punktami startowymi dla projektów danych big data w środowisku Azure. w szczególności może udostępnić toowork aplikacji w czasie rzeczywistym z dużymi zestawami danych.

Implementacja usługi HDInsight Hello wykorzystuje hello skalowalnego w poziomie architektury HBase tooprovide automatyczne dzielenie tabel na fragmenty, wysoki poziom spójności operacji odczytu i zapisu oraz automatycznej pracy awaryjnej. Wydajność jest zwiększona dzięki buforowaniu w pamięci operacji odczytu i przesyłaniu strumieniowemu o wysokiej przepustowości obejmującemu operacje zapisu. Klaster bazy danych HBase można utworzyć w sieci wirtualnej. Aby uzyskać szczegółowe informacje, zobacz temat [Create HDInsight clusters on Azure Virtual Network][hbase-provision-vnet] (Tworzenie klastrów usługi HDInsight w usłudze Azure Virtual Network).

## <a name="how-is-data-managed-in-hdinsight-hbase"></a>W jaki sposób zarządzane są dane w bazie danych HBase w usłudze HDInsight?
Dane można zarządzać w bazie danych HBase przy użyciu hello `create`, `get`, `put`, i `scan` poleceń z hello powłoki HBase. Dane są zapisywane toohello bazy danych przy użyciu `put` i odczytywane za pomocą `get`. Witaj `scan` polecenia jest używane tooobtain danych z wielu wierszy w tabeli. Dane można też zarządzać za pomocą hello HBase C# interfejsu API, który udostępnia bibliotekę klienta ponad hello interfejsu API REST HBase. Korzystając z programu Hive, można wykonywać zapytania w bazie danych HBase. Dla toothese wprowadzenie modele programowania, zobacz [rozpocząć korzystanie z platformy Hadoop w usłudze HDInsight HBase][hbase-get-started]. Dostępne są również dostępne, co umożliwia przetwarzanie danych w węzłach hello hello bazy danych hosta.

> [!NOTE]
> Platforma Thrift nie jest obsługiwana przez bazę danych HBase w usłudze HDInsight.
>

## <a name="scenarios-use-cases-for-hbase"></a>Scenariusze: przypadki użycia bazy danych HBase
Witaj klasycznym przypadkiem użycia których BigTable (i danych hbase) został utworzony został wyszukiwanie w sieci web. Aparaty wyszukiwania tworzą indeksy, które mapują terminy toohello web zawierające je strony. Istnieje jednak wiele innych przypadków użycia, w których baza danych HBase jest przydatna — niektóre z nich są wymienione w tej sekcji.

* Magazyn wartości klucza
  
    Baza danych HBase może być używana jako magazyn wartości klucza i nadaje się do zarządzania systemami obsługi wiadomości. Facebook używa bazy danych HBase na potrzeby systemu obsługi wiadomości, gdyż takie rozwiązanie idealnie nadaje się do przechowywania wiadomości i zarządzania komunikacją internetową. Usługa WebTable używa bazy danych HBase toosearch dla i zarządzaj nimi tabel wyodrębnianych ze stron sieci Web.
* Dane czujników
  
    Baza danych HBase może służyć do przechwytywania danych gromadzonych przyrostowo z różnych źródeł. Dotyczy to analiz społecznościowych, szeregów czasowych, aktualizowania interaktywnych pulpitów nawigacyjnych przy użyciu trendów i liczników oraz zarządzania systemami dzienników inspekcji. Przykładami mogą być terminale transakcyjne Bloomberg i hello Otwórz czasu serii baza danych OpenTSDB (), która przechowuje i udostępnia toometrics dostępu zebrane o hello kondycji systemów serwerowych.
* Zapytania w czasie rzeczywistym
  
    Baza danych Apache HBase korzysta z aparatu zapytań SQL [Phoenix](http://phoenix.apache.org/). Jest on dostępny jako sterownik JDBC i umożliwia wykonywanie zapytań i zarządzanie tabelami HBase przy użyciu języka SQL.
* HBase jako platforma
  
    Aplikacje mogą działać w bazie danych HBase, wykorzystując ją jako magazyn danych. Przykłady obejmują aplikacje Phoenix, OpenTSDB, Kiji i Titan. Aplikacje można również integrować z bazą danych HBase. Przykładami mogą być aplikacje Hive, Pig, Solr, Storm, Flume, Impala, Spark, Ganglia i Drill.

## <a name="next-steps"></a>Następne kroki
* [Rozpoczęcie korzystania z bazy danych HBase z użyciem usługi Hadoop w usłudze HDInsight][hbase-get-started]
* [Create HDInsight clusters on Azure Virtual Network][hbase-provision-vnet] (Tworzenie klastrów usługi HDInsight w usłudze Azure Virtual Network)
* [Konfigurowanie replikacji bazy danych HBase w usłudze HDInsight](hdinsight-hbase-replication.md)
* [Analizowanie opinii w serwisie Twitter przy użyciu bazy danych HBase w usłudze HDInsight][hbase-twitter-sentiment]
* [Korzystanie z aplikacji Java toobuild Maven, korzystających z bazy danych HBase w usłudze HDInsight (Hadoop)][hbase-build-java-maven]

## <a name="see-also"></a>Zobacz też
* [Apache HBase](https://hbase.apache.org/)
* [Bigtable: rozproszony system przechowywania danych strukturalnych](http://research.google.com/archive/bigtable.html)

[hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md

[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hbase-build-java-maven]: hdinsight-hbase-build-java-maven.md

[hdinsight-use-hive]: hdinsight-use-hive.md

[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md

[hbase-get-started]: http://azure.microsoft.com/documentation/articles/hdinsight-hbase-get-started/

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-management-portal]: https://portal.azure.com/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md

[apache-hadoop]: http://hadoop.apache.org/
