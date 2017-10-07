---
title: aaaWhat jest Apache Storm - Azure HDInsight | Dokumentacja firmy Microsoft
description: "Apache Storm umożliwia tooprocess strumieni danych w czasie rzeczywistym. Usługa Azure HDInsight pozwala tooeasily Tworzenie klastrów Storm na powitania chmury Azure. Z programem Visual Studio może utworzyć rozwiązanie Storm przy użyciu języka C# i wdrożyć tooyour, który klastrów HDInsight Storm."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: "przypadki użycia systemu apache storm,klaster storm,co to jest apache storm"
ms.assetid: 72d54080-1e48-4a5e-aa50-cce4ffc85077
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.openlocfilehash: 6c6b2925ef3e5666dfecc3fb3c835bb362902c51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-apache-storm-on-azure-hdinsight"></a>Co to jest Apache Storm w usłudze Azure HDInsight?

[Apache Storm](http://storm.apache.org/) to rozproszony, odporny na uszkodzenia system obliczeniowy typu open source. Używając Storm tooprocess strumieni danych w czasie rzeczywistym z platformą Hadoop. Rozwiązanie STORM oferuje również gwarantowane przetwarzanie danych, z tooreplay możliwości hello danych, które nie zostały pomyślnie przetworzone powitania po raz pierwszy.

STORM w usłudze HDInsight zapewnia hello następujące kluczowe korzyści:

* Działa jako usługa zarządzana przy dostępności 99,9 procent czasu według umowy SLA.

* Umożliwia łatwe dostosowywanie klastrów Storm dzięki uruchamianiu w nich skryptów podczas procesu tworzenia klastra lub po jego ukończeniu. Aby uzyskać więcej informacji, zobacz [Dostosowywanie klastrów usługi HDInsight za pomocą akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md).

* Korzysta z różnych języków. Można napisać składników systemu Storm w języku hello wybranych przez użytkownika, takie jak Java, C# i Python.

    * Integruje Visual Studio z usługą HDInsight hello tworzenia, zarządzania i monitorowania topologii C#. Aby uzyskać więcej informacji, zobacz [topologii opracowywania C# Storm z hello narzędzia HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

    * Obsługuje hello Trident Java interfejsu. Umożliwia on tworzenie topologii Storm obsługujących dokładnie jednokrotne przetwarzanie komunikatów, transakcyjną trwałość magazynu danych i zestaw typowych operacji analizy strumienia.

*  Klastry Storm można łatwo skalować w górę i w dół. Można dodawać i usuwać węzłów procesu roboczego o topologii Storm toorunning nie wpływu.

* Integruje się z hello następujących usług Azure:

    * Azure Event Hubs

    * Azure Virtual Network

    * Usługa Azure SQL Database

    * Azure Storage

    * Azure Cosmos DB

* Bezpieczny sposób łączy hello możliwości wielu klastrów usługi HDInsight przy użyciu sieci wirtualnej. Można tworzyć potoki analityczne, które korzystają z klastrów Storm, Kafka, Spark, HBase i Hadoop.

Lista firm, które używają systemu Apache Storm w rozwiązaniach analitycznych działających w czasie rzeczywistym, jest dostępna na stronie [Companies Using Apache Storm](https://storm.apache.org/documentation/Powered-By.html) (Firmy korzystające z systemu Apache Storm).

tooget uruchomić za pomocą Storm, zobacz [wprowadzenie Storm w usłudze HDInsight][gettingstarted].

## <a name="how-does-storm-work"></a>Jak działa system Storm

STORM uruchamia topologie zamiast hello zadań MapReduce, które mogą być doświadczenia w obsłudze. Topologie systemu Storm obejmują wiele składników rozmieszczonych w skierowanym grafie acyklicznym (DAG). Dane przepływają między składnikami hello hello wykresie. Każdy składnik używa przynajmniej jednego strumienia danych i może opcjonalnie emitować przynajmniej jeden strumień. powitania po diagram przedstawia, jak dane przepływają między składnikami w topologii podstawowe wyrazów:

![Przykładowy układ składników w topologii Storm](./media/hdinsight-storm-overview/example-apache-storm-topology-diagram.png)

* Składniki typu spout wprowadzają dane do topologii. Wysyłają jeden lub więcej strumieni w topologii hello.

* Składniki typu bolt wykorzystują strumienie emitowane przez elementy spout lub inne elementy bolt. Elementów bolt może opcjonalnie Emituj strumieni w topologii hello. Elementy bolt są również odpowiedzialne za zapisywanie danych tooexternal usług lub magazynu, na przykład system plików HDFS, Kafka lub HBase.

## <a name="ease-of-creation"></a>Łatwość tworzenia

Nowy klaster Storm można aprowizować w usłudze HDInsight w ciągu kilku minut. Aby uzyskać więcej informacji na temat tworzenia klastra Storm, zobacz [Wprowadzenie do usługi Storm w usłudze HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).

## <a name="ease-of-use"></a>Łatwość obsługi

* __Secure Shell (SSH) łączności__: hello głównymi węzłami klastra Storm mogą korzystać za pośrednictwem Internetu hello, za pomocą protokołu SSH. Polecenia można uruchamiać bezpośrednio w klastrze przy użyciu protokołu SSH.

  Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

* __Łączność w sieci Web__: klastry HDInsight wszystkie zapewniają hello Ambari web UI. Można łatwo monitorowanie, konfigurowanie i zarządzanie usługami w klastrze za pomocą hello Ambari web UI. Klastry STORM zapewniają także hello interfejsu użytkownika platformy Storm. Można monitorować i zarządzania uruchomionymi topologiami Storm w przeglądarce przy użyciu interfejsu użytkownika platformy Storm hello.

  Aby uzyskać więcej informacji, zobacz hello [Zarządzanie HDInsight przy użyciu hello Interfejsu sieci Web Ambari](hdinsight-hadoop-manage-ambari.md) i [monitora i zarządzać nimi przy użyciu interfejsu użytkownika platformy Storm hello](hdinsight-storm-deploy-monitor-topology-linux.md#monitor-and-manage-storm-ui) dokumentów.

* __Azure PowerShell i interfejsu wiersza polecenia Azure__: środowiska PowerShell i interfejsu wiersza polecenia zarówno zapewniają narzędzia wiersza polecenia, korzystających z Twojej toowork systemu klienta z usługi HDInsight i innymi usługami Azure.

* __Integracja z programem Visual Studio__: Azure Data Lake Tools dla programu Visual Studio obejmują szablony projektów do tworzenia topologii Storm C# przy użyciu hello SCP.Net framework. Narzędzia Data Lake Tools udostępniają toodeploy narzędzia, monitorowanie i zarządzanie rozwiązaniami Storm w usłudze HDInsight.

  Aby uzyskać więcej informacji, zobacz [topologii opracowywania C# Storm z hello narzędzia HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

## <a name="integration-with-other-azure-services"></a>Integracja z innymi usługami platformy Azure

* __Azure Data Lake Store__: przykład użycia usługi Data Lake Store w klastrze Storm można znaleźć w artykule [Use Azure Data Lake Store with Apache Storm on HDInsight](hdinsight-storm-write-data-lake-store.md) (Korzystanie z usługi Azure Data Lake Store razem z systemem Apache Storm w usłudze HDInsight).

* __Centra zdarzeń__: przykład za pomocą usługi Event Hubs z klastrem Storm, zobacz następujące dokumenty hello:

    * [Develop a Java-based topology for Storm on HDInsight](hdinsight-storm-develop-java-topology.md) (Opracowywanie topologii opartej na języku Java dla systemu Storm w usłudze HDInsight)

    * [Process events from Azure Event Hubs with Storm on HDInsight (C#)](hdinsight-storm-develop-csharp-event-hub-topology.md) (Przetwarzanie zdarzeń usługi Azure Event Hubs przy użyciu systemu Storm w usłudze HDInsight — C#)

* __Baza danych SQL__, __DB rozwiązania Cosmos__, __usługi Event Hubs__, i __HBase__: szablon przykłady znajdują się w hello narzędzi Data Lake Tools dla programu Visual Studio. Aby uzyskać więcej informacji, zobacz [Develop a C# topology for Storm on HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md) (Opracowywanie technologii języka C# dla usługi Storm w usłudze HDInsight).

## <a name="reliability"></a>Niezawodność

Apache Storm gwarantuje, że każdy przychodzący komunikat zawsze pełni jest przetwarzany, nawet wtedy, gdy analiza danych hello jest rozłożona na setki węzłów.

węzeł Nimbus Hello zapewnia funkcje podobne toohello Hadoop JobTracker i przypisuje zadania tooother węzłów w klastrze za pośrednictwem dozorcy. Węzły dozorcy zapewniają koordynację klastra i ułatwiają komunikację między Nimbus i hello proces przełożonego na powitania węzłów procesu roboczego. Jeśli jeden węzeł przetwarzania przestanie działać, zawiadomiony węzeł Nimbus hello i przypisuje zadania hello i skojarzone dane tooanother węzła.

Witaj konfigurację domyślną dla klastrów platformy Apache Storm jest tylko jeden węzeł Nimbus toohave. System Storm w usłudze HDInsight obejmuje dwa węzły Nimbus. W przypadku niepowodzenia hello węzła podstawowego klaster Storm hello zmienia węzła pomocniczego toohello podczas hello węzeł podstawowy jest przywracany. Witaj poniższym diagramie przedstawiono konfigurację przepływu zadań hello systemu STORM w usłudze HDInsight:

![Schemat węzłów Nimbus, dozorcy i nadzorcy](./media/hdinsight-storm-overview/nimbus.png)

## <a name="scale"></a>Skalowanie

Klastry usługi HDInsight mogą być skalowane dynamicznie przez dodawanie lub usuwanie węzłów procesu roboczego. Tę operację można wykonać podczas przetwarzania danych.

> [!IMPORTANT]
> tootake skorzystać z nowych węzłów dodanych do skalowania, należy uruchomić przed zwiększeniem rozmiaru klastra hello topologii Storm toorebalance.

## <a name="support"></a>Pomoc techniczna

System Storm w usłudze HDInsight jest dostarczany z pełną, stale dostępną pomocą techniczną na poziomie korporacyjnym. System Storm w usłudze HDInsight gwarantuje również dostępność na poziomie 99,9 procent zgodnie z umową SLA. Oznacza to, że gwarantujemy, że klaster Storm ma łączność zewnętrzną co najmniej 99,9% czasu hello.

Aby uzyskać więcej informacji, zobacz [Pomoc techniczna platformy Azure](https://azure.microsoft.com/support/options/).

## <a name="apache-storm-use-cases"></a>Przypadki użycia systemu Apache Storm

Witaj, poniżej przedstawiono kilka typowych scenariuszy, w których może używać systemu Storm w usłudze HDInsight:

* Internet rzeczy (IoT)
* Wykrywanie oszustw
* Analityka społecznościowa
* Wyodrębnianie, transformacja, ładowanie (ETL)
* Monitorowanie sieci
* Wyszukiwanie
* Marketing na urządzeniach przenośnych

Informacje o scenariuszach rzeczywistych, zobacz hello [firmy korzystania z systemu Storm](https://storm.apache.org/documentation/Powered-By.html) dokumentu.

## <a name="development"></a>Opracowywanie zawartości

Korzystając z narzędzi Data Lake Tools for Visual Studio programiści .NET mogą projektować i implementować topologie w języku C#. Można również tworzyć hybrydowe topologie, wykorzystujące składniki Java i C#.

Aby uzyskać więcej informacji na ten temat, zobacz [Develop C# topologies for Storm on HDInsight using Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md) (Tworzenie topologii C# dla Storm w usłudze HDInsight przy użyciu programu Visual Studio).

Można również tworzenie rozwiązań Java za pomocą hello IDE wybranych przez użytkownika. Aby uzyskać więcej informacji, zobacz [Develop Java topologies for Storm on HDInsight](hdinsight-storm-develop-java-topology.md) (Opracowywanie topologii języka Java dla usługi Storm w usłudze HDInsight).

Python może być również używane toodevelop składników systemu Storm. Aby uzyskać więcej informacji, zobacz [Develop Storm topologies using Python on HDInsight](hdinsight-storm-develop-python-topology.md) (Opracowywanie topologii systemu Storm przy użyciu języka Python w usłudze HDInsight).

## <a name="common-development-patterns"></a>Typowe wzorce programowania

### <a name="guaranteed-message-processing"></a>Gwarantowane przetwarzanie komunikatów

System Apache Storm zapewnia różne poziomy gwarantowanego przetwarzania komunikatów. Na przykład podstawowa aplikacja Storm może zagwarantować przetwarzanie co najmniej jednokrotne, a Trident może zagwarantować przetwarzanie dokładnie jednokrotne.

Aby uzyskać więcej informacji, zobacz [Guarantees on data processing](https://storm.apache.org/about/guarantees-data-processing.html) (Gwarancje przetwarzania danych) w serwisie apache.org.

### <a name="ibasicbolt"></a>IBasicBolt

Witaj wzorzec obejmujący odczytywanie krotki wejściowej emitowanie zero lub więcej krotek, a następnie krotki wejściowej hello ACK na krotce natychmiast na końcu hello hello wykonaj — metoda często. STORM zapewnia hello [IBasicBolt](https://storm.apache.org/releases/1.0.3/javadocs/org/apache/storm/topology/IBasicBolt.html) interfejsu tooautomate tego wzorca.

### <a name="joins"></a>Sprzężenia

Sposób łączenia strumieni danych różni się między aplikacjami. Na przykład można łączyć poszczególne krotki z wielu strumieni w jeden nowy strumień lub łączyć tylko partie krotek w określonym oknie. W obu przypadkach łączenie można przeprowadzić za pomocą metody [fieldsGrouping](http://storm.apache.org/releases/current/javadocs/org/apache/storm/topology/InputDeclarer.html#fieldsGrouping-java.lang.String-org.apache.storm.tuple.Fields-). Pole Grupowanie jest sposób definiowania sposobu routingiem toobolts spójnych kolekcji.

Poniższy przykład Java hello fieldsGrouping jest używane tooroute krotek, pochodzących ze składników "1", "2" i "3" toohello MyJoiner bolt:

    builder.setBolt("join", new MyJoiner(), parallelism) .fieldsGrouping("1", new Fields("joinfield1", "joinfield2")) .fieldsGrouping("2", new Fields("joinfield1", "joinfield2")) .fieldsGrouping("3", new Fields("joinfield1", "joinfield2"));

### <a name="batches"></a>Partie

System Apache Storm ma wewnętrzny mechanizm zegarowy nazywany „krotką znacznikową”. Można określić częstotliwość emitowania krotki znacznikowej w topologii.

Aby zapoznać się z przykładem korzystania z krotki znacznikowej z poziomu składnika języka C#, zobacz [PartialBoltCount.cs](https://github.com/hdinsight/hdinsight-storm-examples/blob/3b2c960549cac122e8874931df4801f0934fffa7/EventCountExample/EventCountTopology/src/main/java/com/microsoft/hdinsight/storm/examples/PartialCountBolt.java).

### <a name="caches"></a>Pamięci podręczne

Buforowanie w pamięci jest często używane jako mechanizm przyspieszania przetwarzania, ponieważ utrzymuje często używane zasoby w pamięci. Ponieważ topologia jest rozpowszechniana na wiele węzłów i wiele procesów w każdym węźle, należy rozważyć użycie metody [fieldsGrouping](http://storm.apache.org/releases/current/javadocs/org/apache/storm/topology/InputDeclarer.html#fieldsGrouping-java.lang.String-org.apache.storm.tuple.Fields-). Użyj `fieldsGrouping` tooensure krotki zawierające pola hello, które są używane do wyszukiwania w pamięci podręcznej są zawsze routingiem toohello tego samego procesu. Funkcja grupowania pozwala uniknąć duplikowania wpisów pamięci podręcznej między procesami.

### <a name="stream-top-n"></a>Strumień „pierwszych N”

Gdy topologia zależy od obliczenia wartości pierwszych N, należy obliczyć wartość pierwszych N hello równolegle. Następnie scalić dane wyjściowe z tych obliczeń do wartości globalnej hello. Ta operacja może odbywać się przy użyciu [fieldsGrouping](http://storm.apache.org/releases/current/javadocs/org/apache/storm/topology/InputDeclarer.html#fieldsGrouping-java.lang.String-org.apache.storm.tuple.Fields-) tooroute według pola w celu równoległego przetwarzania. Następnie może kierować tooa bolt, który globalnie określa wartość pierwszych N hello.

Na przykład obliczania wartości pierwszych N Zobacz hello [RollingTopWords](https://github.com/apache/storm/blob/master/examples/storm-starter/src/jvm/org/apache/storm/starter/RollingTopWords.java) przykład.

## <a name="logging"></a>Rejestrowanie

STORM używa Apache Log4j toolog informacji. Domyślnie jest rejestrowana dużej ilości danych, i może być trudne toosort za pośrednictwem hello informacje. Plik konfiguracji rejestrowania można dodać jako część programu zachowania podczas rejestrowania toocontrol topologii Storm.

Dla przykładową topologię, która przedstawia tooconfigure rejestrowania, zobacz temat [opartych na języku Java WordCount](hdinsight-storm-develop-java-topology.md) przykład Storm w usłudze HDInsight.

## <a name="next-steps"></a>Następne kroki

Dowiedz się więcej na temat rozwiązań analitycznych w czasie rzeczywistym z wykorzystaniem systemu Storm w usłudze HDInsight:

* [Wprowadzenie do systemu Apache Storm w usłudze HDInsight][gettingstarted]
* [Przykładowe topologie dla systemu Apache Storm w usłudze HDInsight](hdinsight-storm-example-topology.md)

[stormtrident]: https://storm.apache.org/documentation/Trident-API-Overview.html
[samoa]: http://yahooeng.tumblr.com/post/65453012905/introducing-samoa-an-open-source-platform-for-mining
[apachetutorial]: https://storm.apache.org/documentation/Tutorial.html
[gettingstarted]: hdinsight-apache-storm-tutorial-get-started-linux.md
