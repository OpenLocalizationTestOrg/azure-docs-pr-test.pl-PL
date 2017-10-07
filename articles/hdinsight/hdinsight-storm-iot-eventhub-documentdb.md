---
title: "dane czujników vehicle aaaProcess z systemu Apache Storm w usłudze HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak dane czujników vehicle tooprocess z usługi Event Hubs przy użyciu platformy Apache Storm w usłudze HDInsight. Dodawanie modelu danych z bazy danych usługi Azure rozwiązania Cosmos i przechowywać toostorage danych wyjściowych."
services: hdinsight,documentdb,notification-hubs
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 78980635-8bef-4c33-96c3-fae50e932e31
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/03/2017
ms.author: larryfr
ms.openlocfilehash: 8f7b1dbb9072e095ea32160bb731bedd071288af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="process-vehicle-sensor-data-from-azure-event-hubs-using-apache-storm-on-hdinsight"></a>Przetwarzania danych czujnika vehicle z usługi Azure Event Hubs przy użyciu platformy Apache Storm w usłudze HDInsight

Dowiedz się, jak dane czujników vehicle tooprocess z usługi Azure Event Hubs przy użyciu platformy Apache Storm w usłudze HDInsight. Ten przykład odczytuje danych czujnika z usługi Azure Event Hubs, poszerza hello danych odwołuje się do danych przechowywanych w usłudze Azure DB rozwiązania Cosmos. Witaj dane są przechowywane w magazynie Azure za pomocą hello systemu plików Hadoop (HDFS).

![HDInsight i hello diagram architektury Internetu rzeczy (IoT)](./media/hdinsight-storm-iot-eventhub-documentdb/iot.png)

## <a name="overview"></a>Omówienie

Dodawanie czujników toovehicles umożliwia toopredict problemów urządzenia na podstawie danych historycznych trendów. Umożliwia także ulepszenia toomake wersje toofuture oparte na analizie wzorca użycia. Muszą być stanie tooquickly i efektywnie ładowanie hello danych z wszystkich pojazdów do Hadoop zanim nastąpi przetwarzanie MapReduce. Ponadto możesz analizy toodo ścieżek błąd krytyczny (aparat temperatury, hamulców itp.) w czasie rzeczywistym.

Usługa Azure Event Hubs jest wbudowana toohandle hello olbrzymich ilości danych wygenerowanych przez czujniki. Apache Storm może być używane tooload i przetwarzania hello danych przed przekazaniem jej do systemu plików HDFS.

## <a name="solution"></a>Rozwiązanie

Dane telemetryczne temperatury aparatu, temperatury otoczenia i prędkość są rejestrowane przez czujniki. Dane są następnie wysyłane koncentratory tooEvent oraz hello samochodu Vehicle identyfikacji numer (VIN) i sygnaturę czasową. Z tego miejsca topologii Storm systemem Apache Storm w klastrze usługi HDInsight odczytuje dane hello, procesy i zapisze go w systemie plików HDFS.

Podczas przetwarzania hello VIN jest używane tooretrieve modelu informacji z bazy danych rozwiązania Cosmos. Te dane jest dodawana toohello strumienia danych, zanim zostanie zachowana.

składniki Hello używana w topologii Storm hello są:

* **EventHubSpout** -odczytuje dane z usługi Azure Event Hubs
* **TypeConversionBolt** — konwertuje hello ciągu JSON z centrów zdarzeń do spójnych kolekcji zawierający hello następujące dane czujników:
    * Aparat temperatury
    * Temperatury otoczenia
    * Szybkość
    * VIN
    * Znacznik czasu
* **DataReferencBolt** -wyszukuje hello vehicle modelu z rozwiązania Cosmos bazy danych przy użyciu hello VIN
* **WasbStoreBolt** -magazynów hello tooHDFS danych (magazyn Azure)

powitania po obrazu jest diagram tego rozwiązania:

![Topologii STORM](./media/hdinsight-storm-iot-eventhub-documentdb/iottopology.png)

## <a name="implementation"></a>Wdrażanie

Pełnego, automatycznego rozwiązania dla tego scenariusza są dostępne jako część hello [HDInsight-Storm-przykłady](https://github.com/hdinsight/hdinsight-storm-examples) repozytorium w witrynie GitHub. toouse w tym przykładzie, wykonaj kroki hello hello [IoTExample Plik README. MD](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/IotExample/README.md).

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej przykładowych topologii Storm, zobacz [przykładowe topologie dla systemu Storm w usłudze HDInsight](hdinsight-storm-example-topology.md).

