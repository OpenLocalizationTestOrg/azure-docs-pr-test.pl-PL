---
title: "dane czujników aaaAnalyze przy użyciu Hive i Hadoop - Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak dane czujników tooanalyze przy użyciu hello Hive konsoli zapytania z usługą HDInsight (Hadoop), a następnie wizualizacji danych hello w programie Microsoft Excel z PowerView."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: a8ac160c-1cef-45d9-bf36-7beb5a439105
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/14/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 70e595705c33d9835dc9809161f79c3ac5ece870
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-sensor-data-using-hello-hive-query-console-on-hadoop-in-hdinsight"></a>Analizowanie danych czujnika przy użyciu konsoli zapytania Hive hello na platformie Hadoop w usłudze HDInsight

Dowiedz się, jak dane czujników tooanalyze przy użyciu hello Hive konsoli zapytania z usługą HDInsight (Hadoop), a następnie wizualizacji danych hello w programie Microsoft Excel za pomocą Power View.

> [!IMPORTANT]
> Witaj czynnościach w ramach tego dokumentu działać tylko w przypadku klastrów usługi HDInsight opartych na systemie Windows. HDInsight jest dostępna tylko w systemie Windows dla wersji starszej niż HDInsight 3.4. Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).


W tym przykładzie używamy danych historycznych tooprocess Hive i zidentyfikować problemy z systemami grzejników i klimatyzacja. W szczególności zidentyfikować systemy są tooreliably nie jest w stanie utrzymać stałej temperatury, wykonując następujące zadania hello:

* Utwórz gałąź Tabele tooquery dane przechowywane w plikach plik wartości rozdzielanych przecinkami (CSV).
* Tworzenie zapytań programu HIVE tooanalyze hello danych.
* tooretrieve hello analizy danych, użyj tooHDInsight tooconnect programu Microsoft Excel.
* toovisualize hello danych, użyj Power View.

![Diagram architektury rozwiązania hello](./media/hdinsight-hive-analyze-sensor-data/hvac-architecture.png)

## <a name="prerequisites"></a>Wymagania wstępne

* Klaster usługi HDInsight (Hadoop): zobacz [klastrów utworzyć Hadoop w usłudze HDInsight](hdinsight-hadoop-provision-linux-clusters.md) informacji o tworzeniu klastra.
* Programu Microsoft Excel 2013

  > [!NOTE]
  > Program Microsoft Excel jest używana do wizualizacji danych z [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US).

* [Sterownik ODBC firmy Microsoft Hive](http://www.microsoft.com/download/details.aspx?id=40886)

## <a name="toorun-hello-sample"></a>przykład Witaj toorun

1. W przeglądarce sieci web przejdź toohello następującego adresu URL: 

         https://<clustername>.azurehdinsight.net

    Zastąp `<clustername>` o nazwie hello klastra usługi HDInsight.

    Po wyświetleniu monitu uwierzytelniania przy użyciu nazwy użytkownika administratora hello i hasło użyte podczas inicjowania obsługi administracyjnej tego klastra.

2. Z hello strony sieci web, który zostanie otwarty, kliknij przycisk hello **Getting Started galerii** kartę, a następnie w obszarze hello **rozwiązań z przykładowymi danymi** kategorii, kliknij hello **analizy danych czujnika** przykład.

    ![Pobieranie rozpoczęte galerii](./media/hdinsight-hive-analyze-sensor-data/getting-started-gallery.png)

3. Postępuj zgodnie z instrukcjami hello hello strony sieci web toofinish hello próbki.
