---
title: "Co to jest system Apache Storm w usłudze Azure HDInsight? | Microsoft Docs"
description: "System Apache Storm służy do przetwarzania strumieni danych w czasie rzeczywistym. Usługa Azure HDInsight umożliwia łatwe tworzenie klastrów Storm w chmurze Azure. Przy użyciu programu Visual Studio można tworzyć rozwiązania Storm przy użyciu języka C#, a następnie wdrażać je do klastrów usługi HDInsight Storm."
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
ms.openlocfilehash: 073672f1223313938baedee027072cb96062294b
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="what-is-apache-storm-on-azure-hdinsight"></a>Co to jest Apache Storm w usłudze Azure HDInsight?

[Apache Storm](http://storm.apache.org/) to rozproszony, odporny na uszkodzenia system obliczeniowy typu open source. Przy użyciu systemu Storm można przetwarzać strumienie danych w czasie rzeczywistym za pomocą usługi Hadoop. Rozwiązanie Storm oferuje również gwarantowane przetwarzanie danych z możliwością powtarzania danych, które nie zostały pomyślnie przetworzone po raz pierwszy.

System Storm w usłudze HDInsight oferuje następujące kluczowe korzyści:

* Działa jako usługa zarządzana przy dostępności 99,9 procent czasu według umowy SLA.

* Umożliwia łatwe dostosowywanie klastrów Storm dzięki uruchamianiu w nich skryptów podczas procesu tworzenia klastra lub po jego ukończeniu. Aby uzyskać więcej informacji, zobacz [Dostosowywanie klastrów usługi HDInsight za pomocą akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md).

* Korzysta z różnych języków. Składniki systemu Storm można pisać w wybranym języku, takim jak Java, C# i Python.

    * Integruje program Visual Studio z usługą HDInsight na potrzeby tworzenia i monitorowania topologii języka C# oraz zarządzania nimi. Aby uzyskać więcej informacji, zobacz [Develop C# Storm topologies with the HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md) (Tworzenie topologii języka C# przy użyciu narzędzi HDInsight Tools dla programu Visual Studio).

    * Obsługuje interfejs języka Java Trident. Umożliwia on tworzenie topologii Storm obsługujących dokładnie jednokrotne przetwarzanie komunikatów, transakcyjną trwałość magazynu danych i zestaw typowych operacji analizy strumienia.

*  Klastry Storm można łatwo skalować w górę i w dół. Można dodawać lub usuwać węzły procesu roboczego bez wpływu na działające topologie Storm.

* Integruje z następującymi usługami platformy Azure:

    * Azure Event Hubs

    * Azure Virtual Network

    * Usługa Azure SQL Database

    * Azure Storage

    * Azure Cosmos DB

* Bezpiecznie łączy możliwości wielu klastrów usługi HDInsight przy użyciu sieci wirtualnej. Można tworzyć potoki analityczne, które korzystają z klastrów Storm, Kafka, Spark, HBase i Hadoop.

Lista firm, które używają systemu Apache Storm w rozwiązaniach analitycznych działających w czasie rzeczywistym, jest dostępna na stronie [Companies Using Apache Storm](https://storm.apache.org/documentation/Powered-By.html) (Firmy korzystające z systemu Apache Storm).

Aby rozpocząć korzystanie z systemu Storm, zobacz [Rozpoczynanie pracy z systemem Storm w usłudze HDInsight][gettingstarted].

## <a name="how-does-storm-work"></a>Jak działa system Storm

System Storm uruchamia topologie zamiast zadań MapReduce, które być może już znasz. Topologie systemu Storm obejmują wiele składników rozmieszczonych w skierowanym grafie acyklicznym (DAG). Dane przepływają między składnikami tego grafu. Każdy składnik używa przynajmniej jednego strumienia danych i może opcjonalnie emitować przynajmniej jeden strumień. Na poniższym diagramie przedstawiono sposób przepływu danych między składnikami w podstawowej topologii zliczania wyrazów:

![Przykładowy układ składników w topologii Storm](./media/hdinsight-storm-overview/example-apache-storm-topology-diagram.png)

* Składniki typu spout wprowadzają dane do topologii. Wysyłają one co najmniej jeden strumień danych do topologii.

* Składniki typu bolt wykorzystują strumienie emitowane przez elementy spout lub inne elementy bolt. Składniki typu bolt mogą opcjonalnie emitować strumienie do topologii. Odpowiadają również za zapisywanie danych w usługach zewnętrznych lub magazynie — takim jak system plików HDFS, platforma Kafka lub usługa HBase.

## <a name="ease-of-creation"></a>Łatwość tworzenia

Nowy klaster Storm można aprowizować w usłudze HDInsight w ciągu kilku minut. Aby uzyskać więcej informacji na temat tworzenia klastra Storm, zobacz [Wprowadzenie do usługi Storm w usłudze HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).

## <a name="ease-of-use"></a>Łatwość obsługi

* __Łączność z protokołem Secure Shell (SSH)__: dostęp do węzłów głównych klastra Storm w Internecie przy użyciu protokołu SSH. Polecenia można uruchamiać bezpośrednio w klastrze przy użyciu protokołu SSH.

  Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

* __Łączność w sieci Web__: wszystkie klastry HDInsight udostępniają interfejs webowy Ambari. Pozwala on łatwo monitorować i konfigurować usługi oraz zarządzać nimi w klastrze. Klastry Storm udostępniają też interfejs Storm. Interfejs ten pozwala na monitorowanie działających topologii systemu Storm oraz zarządzanie nimi z poziomu przeglądarki przy użyciu interfejsu użytkownika Storm.

  Aby uzyskać więcej informacji, zobacz następujące artykuły: [Manage HDInsight using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md) (Zarządzanie usługą HDInsight przy użyciu interfejsu webowego Ambari) i [Monitor and manage using the Storm UI](hdinsight-storm-deploy-monitor-topology-linux.md#monitor-and-manage-storm-ui) (Monitorowanie i zarządzanie przy użyciu interfejsu Storm).

* __Program Azure PowerShell i interfejs wiersza polecenia platformy Azure__: program Azure PowerShell i interfejs wiersza polecenia platformy Azure udostępniają narzędzia wiersza polecenia, których można używać w systemie klienta do pracy z usługą HDInsight i innymi usługami platformy Azure.

* __Integracja z programem Visual Studio__: narzędzia Azure Data Lake Tools for Visual Studio obejmują szablony projektów umożliwiające tworzenie topologii Storm języka C# przy użyciu platformy SCP.Net. Narzędzia Data Lake Tools oferują również umożliwiające wdrażanie i monitorowanie rozwiązań systemu Storm w usłudze HDInsight oraz zarządzanie nimi.

  Aby uzyskać więcej informacji, zobacz [Develop C# Storm topologies with the HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md) (Tworzenie topologii języka C# przy użyciu narzędzi HDInsight Tools dla programu Visual Studio).

## <a name="integration-with-other-azure-services"></a>Integracja z innymi usługami platformy Azure

* __Azure Data Lake Store__: przykład użycia usługi Data Lake Store w klastrze Storm można znaleźć w artykule [Use Azure Data Lake Store with Apache Storm on HDInsight](hdinsight-storm-write-data-lake-store.md) (Korzystanie z usługi Azure Data Lake Store razem z systemem Apache Storm w usłudze HDInsight).

* __Event Hubs__: przykład użycia usługi Event Hubs w klastrze Storm można znaleźć w następujących artykułach:

    * [Develop a Java-based topology for Storm on HDInsight](hdinsight-storm-develop-java-topology.md) (Opracowywanie topologii opartej na języku Java dla systemu Storm w usłudze HDInsight)

    * [Process events from Azure Event Hubs with Storm on HDInsight (C#)](hdinsight-storm-develop-csharp-event-hub-topology.md) (Przetwarzanie zdarzeń usługi Azure Event Hubs przy użyciu systemu Storm w usłudze HDInsight — C#)

* __SQL Database__, __Cosmos DB__, __Event Hubs__ i __HBase__: przykłady szablonów są dostępne w narzędziach Data Lake Tools for Visual Studio. Aby uzyskać więcej informacji, zobacz [Develop a C# topology for Storm on HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md) (Opracowywanie technologii języka C# dla usługi Storm w usłudze HDInsight).

## <a name="reliability"></a>Niezawodność

System Apache Storm gwarantuje, że każdy przychodzący komunikat jest zawsze w pełni przetwarzany — nawet wtedy, gdy analiza danych jest rozłożona na setki węzłów.

Węzeł Nimbus oferuje funkcje podobne do Hadoop JobTracker i przypisuje zadania do innych węzłów w klastrze za pośrednictwem dozorcy. Węzły dozorcy zapewniają koordynację klastra i ułatwiają komunikację między węzłem Nimbus i procesem nadzorczym procesów roboczych. Jeśli jeden węzeł przetwarzania przestanie działać, zostanie zawiadomiony węzeł Nimbus, który przypisze zadanie i związane z nim dane do innego węzła.

W domyślnej konfiguracji klastrów Apache Storm występuje tylko jeden węzeł Nimbus. System Storm w usłudze HDInsight obejmuje dwa węzły Nimbus. W przypadku awarii węzła podstawowego klaster Storm przechodzi do węzła pomocniczego, a węzeł podstawowy jest przywracany. Na poniższym diagramie przedstawiono konfigurację przepływu zadań systemu Storm w usłudze HDInsight:

![Schemat węzłów Nimbus, dozorcy i nadzorcy](./media/hdinsight-storm-overview/nimbus.png)

## <a name="scale"></a>Skalowanie

Klastry usługi HDInsight mogą być skalowane dynamicznie przez dodawanie lub usuwanie węzłów procesu roboczego. Tę operację można wykonać podczas przetwarzania danych.

> [!IMPORTANT]
> Aby móc skorzystać z nowych węzłów dodanych do skalowania, konieczne jest ponowne zrównoważenie topologii systemu Storm uruchomionych przed zwiększeniem rozmiaru klastra.

## <a name="support"></a>Pomoc techniczna

System Storm w usłudze HDInsight jest dostarczany z pełną, stale dostępną pomocą techniczną na poziomie korporacyjnym. System Storm w usłudze HDInsight gwarantuje również dostępność na poziomie 99,9 procent zgodnie z umową SLA. Gwarantujemy więc, że klaster Storm utrzymuje łączność zewnętrzną przez nie mniej niż 99,9% czasu.

Aby uzyskać więcej informacji, zobacz [Pomoc techniczna platformy Azure](https://azure.microsoft.com/support/options/).

## <a name="apache-storm-use-cases"></a>Przypadki użycia systemu Apache Storm

Poniżej przedstawiono kilka typowych scenariuszy, w których można skorzystać z systemu Storm w usłudze HDInsight:

* Internet rzeczy (IoT)
* Wykrywanie oszustw
* Analityka społecznościowa
* Wyodrębnianie, transformacja, ładowanie (ETL)
* Monitorowanie sieci
* Wyszukiwanie
* Marketing na urządzeniach przenośnych

Aby uzyskać informacje o praktycznych scenariuszach, zobacz dokument [How companies are using Storm](https://storm.apache.org/documentation/Powered-By.html) (Zastosowania systemu Storm w firmach).

## <a name="development"></a>Opracowywanie zawartości

Korzystając z narzędzi Data Lake Tools for Visual Studio programiści .NET mogą projektować i implementować topologie w języku C#. Można również tworzyć hybrydowe topologie, wykorzystujące składniki Java i C#.

Aby uzyskać więcej informacji na ten temat, zobacz [Develop C# topologies for Storm on HDInsight using Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md) (Tworzenie topologii C# dla Storm w usłudze HDInsight przy użyciu programu Visual Studio).

Możesz również tworzyć rozwiązania w języku Java przy użyciu wybranego środowiska IDE. Aby uzyskać więcej informacji, zobacz [Develop Java topologies for Storm on HDInsight](hdinsight-storm-develop-java-topology.md) (Opracowywanie topologii języka Java dla usługi Storm w usłudze HDInsight).

Składniki systemu Storm można również opracowywać w języku Python. Aby uzyskać więcej informacji, zobacz [Develop Storm topologies using Python on HDInsight](hdinsight-storm-develop-python-topology.md) (Opracowywanie topologii systemu Storm przy użyciu języka Python w usłudze HDInsight).

## <a name="common-development-patterns"></a>Typowe wzorce programowania

### <a name="guaranteed-message-processing"></a>Gwarantowane przetwarzanie komunikatów

System Apache Storm zapewnia różne poziomy gwarantowanego przetwarzania komunikatów. Na przykład podstawowa aplikacja Storm może zagwarantować przetwarzanie co najmniej jednokrotne, a Trident może zagwarantować przetwarzanie dokładnie jednokrotne.

Aby uzyskać więcej informacji, zobacz [Guarantees on data processing](https://storm.apache.org/about/guarantees-data-processing.html) (Gwarancje przetwarzania danych) w serwisie apache.org.

### <a name="ibasicbolt"></a>IBasicBolt

Wzorzec obejmujący odczytywanie krotki wejściowej, emitującej zero lub więcej krotek, a następnie potwierdzanie krotki wejściowej natychmiast po zakończeniu przetwarzania jest typowy. System Storm udostępnia interfejs [IBasicBolt](https://storm.apache.org/releases/1.0.3/javadocs/org/apache/storm/topology/IBasicBolt.html) w celu automatyzacji tego wzorca.

### <a name="joins"></a>Sprzężenia

Sposób łączenia strumieni danych różni się między aplikacjami. Na przykład można łączyć poszczególne krotki z wielu strumieni w jeden nowy strumień lub łączyć tylko partie krotek w określonym oknie. W obu przypadkach łączenie można przeprowadzić za pomocą metody [fieldsGrouping](http://storm.apache.org/releases/current/javadocs/org/apache/storm/topology/InputDeclarer.html#fieldsGrouping-java.lang.String-org.apache.storm.tuple.Fields-). Grupowanie pól polega na określeniu, jak krotki są kierowane do składników bolt.

W poniższym przykładzie w języku Java metoda fieldsGrouping służy do kierowana krotek pochodzących ze składników „1”, „2” i „3” do elementu bolt o nazwie MyJoiner:

    builder.setBolt("join", new MyJoiner(), parallelism) .fieldsGrouping("1", new Fields("joinfield1", "joinfield2")) .fieldsGrouping("2", new Fields("joinfield1", "joinfield2")) .fieldsGrouping("3", new Fields("joinfield1", "joinfield2"));

### <a name="batches"></a>Partie

System Apache Storm ma wewnętrzny mechanizm zegarowy nazywany „krotką znacznikową”. Można określić częstotliwość emitowania krotki znacznikowej w topologii.

Aby zapoznać się z przykładem korzystania z krotki znacznikowej z poziomu składnika języka C#, zobacz [PartialBoltCount.cs](https://github.com/hdinsight/hdinsight-storm-examples/blob/3b2c960549cac122e8874931df4801f0934fffa7/EventCountExample/EventCountTopology/src/main/java/com/microsoft/hdinsight/storm/examples/PartialCountBolt.java).

### <a name="caches"></a>Pamięci podręczne

Buforowanie w pamięci jest często używane jako mechanizm przyspieszania przetwarzania, ponieważ utrzymuje często używane zasoby w pamięci. Ponieważ topologia jest rozpowszechniana na wiele węzłów i wiele procesów w każdym węźle, należy rozważyć użycie metody [fieldsGrouping](http://storm.apache.org/releases/current/javadocs/org/apache/storm/topology/InputDeclarer.html#fieldsGrouping-java.lang.String-org.apache.storm.tuple.Fields-). Użyj metody `fieldsGrouping`, aby zagwarantować, że krotki z polami używanymi do przeszukiwania pamięci podręcznej są zawsze kierowane do tego samego procesu. Funkcja grupowania pozwala uniknąć duplikowania wpisów pamięci podręcznej między procesami.

### <a name="stream-top-n"></a>Strumień „pierwszych N”

Jeśli topologia zależy od obliczenia wartości „pierwszych N”, oblicz wartość pierwszych N równolegle. Następnie należy scalić dane wyjściowe z tych obliczeń w obrębie wartości globalnej. Tę operację można wykonać przy użyciu metody [fieldsGrouping](http://storm.apache.org/releases/current/javadocs/org/apache/storm/topology/InputDeclarer.html#fieldsGrouping-java.lang.String-org.apache.storm.tuple.Fields-), aby przeprowadzić kierowanie według pola na potrzeby przetwarzania równoległego. Następnie można kierować do składnika bolt, który określa globalnie największą wartość N.

Aby zapoznać się z przykładem obliczania wartości pierwszych N, zobacz przykład [RollingTopWords](https://github.com/apache/storm/blob/master/examples/storm-starter/src/jvm/org/apache/storm/starter/RollingTopWords.java).

## <a name="logging"></a>Rejestrowanie

System Storm używa mechanizmu Apache Log4j do rejestrowania informacji. Domyślnie rejestrowana jest duża ilość danych i sortowanie informacji może być trudne. W topologii systemu Storm można uwzględnić plik konfiguracji rejestrowania, aby sterować zachowaniem rejestrowania.

Przykładową topologię pokazującą metodę konfigurowania logowania można znaleźć w przykładzie [aplikacji WordCount opartej na języku Java](hdinsight-storm-develop-java-topology.md) dla systemu Storm w usłudze HDInsight.

## <a name="next-steps"></a>Następne kroki

Dowiedz się więcej na temat rozwiązań analitycznych w czasie rzeczywistym z wykorzystaniem systemu Storm w usłudze HDInsight:

* [Wprowadzenie do systemu Apache Storm w usłudze HDInsight][gettingstarted]
* [Przykładowe topologie dla systemu Apache Storm w usłudze HDInsight](hdinsight-storm-example-topology.md)

[stormtrident]: https://storm.apache.org/documentation/Trident-API-Overview.html
[samoa]: http://yahooeng.tumblr.com/post/65453012905/introducing-samoa-an-open-source-platform-for-mining
[apachetutorial]: https://storm.apache.org/documentation/Tutorial.html
[gettingstarted]: hdinsight-apache-storm-tutorial-get-started-linux.md
