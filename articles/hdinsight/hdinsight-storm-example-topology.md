---
title: "aaaExample topologii Apache Storm w usłudze HDInsight | Dokumentacja firmy Microsoft"
description: "Listę przykładowych topologii Storm utworzone i przetestowane z systemu Apache Storm w usłudze HDInsight tym podstawowe topologii C# i Java i pracy z usługą Event Hubs."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: f9b1bdff-5928-4705-a76d-52fd200917cb
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/07/2017
ms.author: larryfr
ms.openlocfilehash: b20299112f6489b7c99360f0a539fc732703c64a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="example-storm-topologies-and-components-for-apache-storm-on-hdinsight"></a>Przykładowych topologii Storm i składniki Apache STORM w usłudze HDInsight

Witaj poniżej znajduje się lista przykładów tworzone i obsługiwane przez firmę Microsoft do użycia z systemu Apache Storm w usłudze HDInsight. Te przykłady obejmują różne tematy tworzenia podstawowe języka C# i tooworking topologii Java z usługami Azure, takich jak usługi Event Hubs, rozwiązania Cosmos bazy danych, usługi Power BI, baza danych SQL, HBase HDInsight i usługi Azure Storage. Przykłady również pokazują, jak toowork z technologii innych niż Azure lub nawet innych niż Microsoft, takich jak SignalR i użyciu biblioteki Socket.IO.

| Opis | Pokazuje | Język/Framework |
|:--- |:--- |:--- |
| [Zapis tooAzure Data Lake Store z systemu Apache Storm](hdinsight-storm-write-data-lake-store.md) |Zapisywanie tooAzure Data Lake Store |Java |
| [Elementów Spout Centrum zdarzeń i Bolt źródła](https://github.com/apache/storm/tree/master/external/storm-eventhubs) |Źródło hello elementów Spout Centrum zdarzeń i Bolt |Java |
| [Opracowywanie topologii opartych na języku Java Apache STORM w usłudze HDInsight][5797064f] |Maven |Java |
| [Tworzenie topologii C# dla Apache Storm w usłudze HDInsight przy użyciu programu Visual Studio][16fce2d1] |HDInsight Tools for Visual Studio |C#, Java |
| [Tworzenie wielu strumieni danych w topologii Storm C#][ec5a4064] |Wiele strumieni |C# |
| [Zdarzenia procesu z usługi Azure Event Hubs z systemu Storm w usłudze HDInsight (C#)][844d1d81] |Usługa Event Hubs |C# i Java |
| [Zdarzenia procesu z usługi Azure Event Hubs z systemu Storm w usłudze HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md) |Usługa Event Hubs |Java |
| [Użyj usługi Power Bi toovisualize danych od topologii Storm][94d15238] |Power BI |C# |
| [Analizowanie danych czujnika za pomocą Storm i bazy danych HBase w usłudze HDInsight][ab894747] |Event Hubs, HBase, użyciu biblioteki Socket.IO, pulpitu nawigacyjnego sieci Web |C#, Java, JavaScript, HTML |
| [Przetwarzania danych czujnika vehicle z usługi Event Hubs za pomocą Storm w usłudze HDInsight][246ee964] |Zdarzenie koncentratory, DB rozwiązania Cosmos obiektu Blob magazynu Azure (WASB) |C#, Java |
| [Wyodrębniania, przekształcania i ładowania (ETL) z usługi Azure Event Hubs tooHBase, korzystanie z systemu Storm w usłudze HDInsight][b4b68194] |Centra zdarzeń, HBase |C# |
| [Szablon projektu o topologii Storm C# do pracy z usługami Azure Storm w usłudze HDInsight][ce0c02a2] |Zdarzenie koncentratory, DB rozwiązania Cosmos SQL bazy danych, HBase, SignalR |C#, Java |
| [Wzorce skalowalność do odczytywania z usługi Azure Event Hubs za pomocą Storm w usłudze HDInsight][d6c540e3] |Komunikat przepływności usługi Event Hubs bazy danych SQL |C#, Java |
| [Korelowanie zdarzeń za pomocą Storm i bazy danych HBase w usłudze HDInsight](hdinsight-storm-correlation-topology.md) |HBase |C# |
| [Python za pomocą Storm w usłudze HDInsight](hdinsight-storm-develop-python-topology.md) |Składniki Python z topologią strumienia |Python |
| [Kafka za pomocą Storm w usłudze HDInsight](hdinsight-apache-storm-with-kafka.md) | Apache Storm odczytu i zapisu tooApache Kafka | Java |

### <a name="next-steps"></a>Następne kroki

* [Wprowadzenie do systemu Apache Storm w usłudze HDInsight][2b8c3488]
* [Dowiedz się, jak toodeploy i zarządzanie topologiami Storm z systemu Storm w usłudze HDInsight][6eb0d3b8]

[2b8c3488]: hdinsight-apache-storm-tutorial-get-started-linux.md "Dowiedz się, jak toocreate Storm w klastrze HDInsight i użyj hello pulpit nawigacyjny Storm toodeploy przykładowe topologie."
[6eb0d3b8]: hdinsight-storm-deploy-monitor-topology.md "Dowiedz się, jak toodeploy topologii użyciu hello opartych na sieci web pulpitu nawigacyjnego Storm i interfejsu użytkownika platformy Storm lub hello HDInsight Tools for Visual Studio oraz zarządzania nimi."
[16fce2d1]: hdinsight-storm-develop-csharp-visual-studio-topology.md "Dowiedz się, jak hello topologii Storm C# toocreate za pomocą narzędzi HDInsight Tools dla programu Visual Studio."
[5797064f]: hdinsight-storm-develop-java-topology.md "Dowiedz się, jak toocreate topologii Storm w języku Java, za pomocą programu Maven, tworząc topologii wordcount podstawowe."
[94d15238]: hdinsight-storm-power-bi-topology.md "Pokazuje, jak toowrite danych tooPower BI od C# topologii, następnie utworzyć wykres i pulpit nawigacyjny hello danych."
[ec5a4064]: https://github.com/Blackmist/csharp-storm-example "Przedstawia podstawowe topologii Storm, który wykonuje wordcount, zaimplementowana w języku C#. Oznacza to również, jak toocreate danych w wielu strumieni w topologii C#."
[844d1d81]: hdinsight-storm-develop-csharp-event-hub-topology.md "Dowiedz się, jak tooread i zapisu danych z usługi Azure Event Hubs z systemu Storm w usłudze HDInsight."
[ab894747]: hdinsight-storm-sensor-data-analysis.md "Dowiedz się, jak toouse Apache Storm na HDInsight tooprocess czujnik danych z usługi Azure Event Hubs przy użyciu D3.js wizualizacji i (opcjonalnie), zapisz go w tooHBase."
[246ee964]: https://github.com/hdinsight/hdinsight-storm-examples/blob/master/IotExample/README.md "Dowiedz się, jak toouse komunikaty tooread topologii Storm z usługi Azure Event Hubs odczytywać z bazy danych usługi Azure rozwiązania Cosmos odwołuje się do danych i zapisać tooAzure danych magazynu."
[d6c540e3]: https://github.com/hdinsight/hdinsight-storm-examples/blob/master/EventCountExample "Kilka topologii toodemonstrate przepustowość podczas odczytywania z usługi Azure Event Hubs i przechowywanie tooSQL bazy danych przy użyciu systemu Apache Storm w usłudze HDInsight."
[b4b68194]: https://github.com/hdinsight/hdinsight-storm-examples/blob/master/RealTimeETLExample "Dowiedz się, jak tooread dane z usługi Azure Event Hubs, agregacji i przekształcenie hello danych, a następnie zapisz go tooHBase w usłudze HDInsight."
[ce0c02a2]: https://github.com/hdinsight/hdinsight-storm-examples/tree/master/templates/HDInsightStormExamples "Ten projekt zawiera szablony toointeract elementach spout, elementów bolt i topologii z różnych usług Azure, takich jak usługi Event Hubs, rozwiązania Cosmos bazę danych i bazy danych SQL."

