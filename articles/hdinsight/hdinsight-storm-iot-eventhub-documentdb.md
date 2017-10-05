---
title: "Przetwarzania danych czujnika vehicle z systemu Apache Storm w usłudze HDInsight | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie przetwarzania danych czujnika vehicle z usługi Event Hubs przy użyciu platformy Apache Storm w usłudze HDInsight. Dodawanie modelu danych z bazy danych usługi Azure rozwiązania Cosmos i przechowywać dane wyjściowe do magazynu."
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
ms.openlocfilehash: 8e8ebc724e1c70e8fcd56312adef5da2342373ea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="process-vehicle-sensor-data-from-azure-event-hubs-using-apache-storm-on-hdinsight"></a>Przetwarzania danych czujnika vehicle z usługi Azure Event Hubs przy użyciu platformy Apache Storm w usłudze HDInsight

Informacje o sposobie przetwarzania danych czujnika vehicle z usługi Azure Event Hubs przy użyciu platformy Apache Storm w usłudze HDInsight. Ten przykład odczytuje danych czujnika z usługi Azure Event Hubs, poszerza danych odwołuje się do danych przechowywanych w usłudze Azure DB rozwiązania Cosmos. Dane są przechowywane w magazynie Azure za pomocą systemu plików Hadoop (HDFS).

![HDInsight i diagram architektury Internetu rzeczy (IoT)](./media/hdinsight-storm-iot-eventhub-documentdb/iot.png)

## <a name="overview"></a>Omówienie

Dodawanie czujników pojazdów służy do prognozowania na podstawie danych historycznych trendów problemów urządzeń. Można też udoskonalamy przyszłych wersji oparte na analizie wzorca użycia. Musi być w stanie szybkie i skuteczne ładowanie danych z wszystkich pojazdów do Hadoop zanim nastąpi przetwarzanie MapReduce. Ponadto można wykonać analizy ścieżek błąd krytyczny (aparat temperatury, hamulców itp.) w czasie rzeczywistym.

Usługa Azure Event Hubs korzysta z wbudowanej obsługi bardzo dużej ilości danych wygenerowanych przez czujniki. Apache Storm może służyć do ładowania i przetwarzania danych przed przekazaniem jej do systemu plików HDFS.

## <a name="solution"></a>Rozwiązanie

Dane telemetryczne temperatury aparatu, temperatury otoczenia i prędkość są rejestrowane przez czujniki. Dane są następnie wysyłane do usługi Event Hubs, oraz numer identyfikacji Vehicle samochodu (VIN) i sygnaturę czasową. Z tego miejsca topologii Storm systemem Apache Storm w klastrze usługi HDInsight odczytuje dane, procesy i zapisze go w systemie plików HDFS.

Podczas przetwarzania VIN służy do pobierania informacji o modelu z bazy danych rozwiązania Cosmos. Te dane jest dodawana do strumienia danych, zanim zostanie zachowana.

Składniki używane w topologii Storm są:

* **EventHubSpout** -odczytuje dane z usługi Azure Event Hubs
* **TypeConversionBolt** — konwertuje ciągu JSON z centrów zdarzeń spójnych kolekcji zawierający dane czujników w następujących:
    * Aparat temperatury
    * Temperatury otoczenia
    * Szybkość
    * VIN
    * Znacznik czasu
* **DataReferencBolt** -wyszukuje modelu vehicle z rozwiązania Cosmos bazy danych przy użyciu VIN
* **WasbStoreBolt** -przechowuje dane do systemu plików HDFS (magazyn Azure)

Poniższa ilustracja jest diagram tego rozwiązania:

![Topologii STORM](./media/hdinsight-storm-iot-eventhub-documentdb/iottopology.png)

## <a name="implementation"></a>Wdrażanie

Pełnego, automatycznego rozwiązania dla tego scenariusza są dostępne jako część [HDInsight-Storm-przykłady](https://github.com/hdinsight/hdinsight-storm-examples) repozytorium w witrynie GitHub. Aby użyć tego przykładu, postępuj zgodnie z instrukcjami [IoTExample Plik README. MD](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/IotExample/README.md).

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej przykładowych topologii Storm, zobacz [przykładowe topologie dla systemu Storm w usłudze HDInsight](hdinsight-storm-example-topology.md).

