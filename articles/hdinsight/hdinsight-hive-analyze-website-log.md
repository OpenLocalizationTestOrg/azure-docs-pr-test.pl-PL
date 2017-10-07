---
title: "aaaUse Hive z usługą Hadoop do analizy dziennika witryny sieci Web - Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak dzienniki toouse Hive z HDInsight tooanalyze witryny sieci Web. Zostanie użyć pliku dziennika jako dane wejściowe do tabeli HDInsight oraz użyć danych hello tooquery HiveQL."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 6fb7b5c2-8df4-40b1-a9e2-6815080004f9
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/17/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 9cbce3cc8cf8bc3ad104dc4ca6a5628802c8fe89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hive-with-windows-based-hdinsight-tooanalyze-logs-from-websites"></a>Korzystanie z programu Hive z HDInsight opartych na systemie Windows tooanalyze dzienników witryn sieci Web
Dowiedz się, jak rejestruje toouse HiveQL z HDInsight tooanalyze z witryny sieci Web. Analiza dziennika witryny sieci Web może być używane toosegment odbiorców w oparciu podobne działania, kategoryzowanie odwiedzający demograficznymi i toofind hello zawartość, którą mogą wyświetlać, hello witryn sieci Web, które pochodzą z i tak dalej.

> [!IMPORTANT]
> Witaj czynnościach w ramach tego dokumentu działać tylko w przypadku klastrów usługi HDInsight opartych na systemie Windows. HDInsight jest dostępna tylko w systemie Windows dla wersji starszej niż HDInsight 3.4. Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

W tym przykładzie użyjesz HDInsight klastra tooanalyze witryny sieci Web dziennika pliki tooget wgląd częstotliwość hello wizyt toohello witryny sieci Web z zewnętrznymi witrynami sieci Web w ciągu jednego dnia. Zostanie również wygenerowany podsumowanie błędów witryny sieci Web, które użytkownicy hello napotkać. Dowiesz się jak:

* Połącz tooa magazynu obiektów Blob platformy Azure, który zawiera pliki dziennika witryny sieci Web.
* Utwórz gałąź Tabele tooquery tych dzienników.
* Tworzenie zapytań programu HIVE tooanalyze hello danych.
* Użyj programu Microsoft Excel tooconnect tooHDInsight (przy użyciu bazy danych otwórz łączności (ODBC) tooretrieve hello analizy danych.

![HDI. Samples.Website.Log.Analysis][img-hdi-weblogs-sample]

## <a name="prerequisites"></a>Wymagania wstępne
* Musi mieć zainicjowana klastra usługi Hadoop w usłudze Azure HDInsight. Aby uzyskać instrukcje, zobacz [klastrów usługi HDInsight udostępniania][hdinsight-provision].
* Musi mieć programu Microsoft Excel 2013 lub zainstalowany program Excel 2010.
* Musi mieć [sterownik Microsoft Hive ODBC](http://www.microsoft.com/download/details.aspx?id=40886) tooimport danych z gałęzi do programu Excel.

## <a name="toorun-hello-sample"></a>przykład Witaj toorun
1. Z hello [Azure Portal](https://portal.azure.com/), hello tablicy startowej (jeśli został przypięty klastra hello istnieje), kliknij hello kafelka klastra, na którym ma zostać toorun hello próbki.
2. Z hello klastra bloku, w obszarze **szybkie linki**, kliknij przycisk **pulpit nawigacyjny klastra**, a następnie z hello **pulpit nawigacyjny klastra** bloku, kliknij przycisk **klastra usługi HDInsight Pulpit nawigacyjny**. Pulpit nawigacyjny hello można również otworzyć bezpośrednio za pomocą hello następującego adresu URL:

         https://<clustername>.azurehdinsight.net

    Po wyświetleniu monitu uwierzytelniania przy użyciu nazwy użytkownika administratora hello i hasło, które zostały użyte podczas inicjowania obsługi klastra hello.
3. Z hello strony sieci web, który zostanie otwarty, kliknij przycisk hello **Getting Started galerii** kartę, a następnie w obszarze hello **rozwiązań z przykładowymi danymi** kategorii, kliknij hello **analiza dziennika witryny sieci Web** przykład.
4. Postępuj zgodnie z instrukcjami hello hello strony sieci web toofinish hello próbki.

## <a name="next-steps"></a>Następne kroki
Spróbuj hello następujące przykładowe: [analizowanie danych czujnika przy użyciu Hive z usługą HDInsight](hdinsight-hive-analyze-sensor-data.md).

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-sensor-data-sample]: ../hdinsight-use-hive-sensor-data-analysis.md

[img-hdi-weblogs-sample]: ./media/hdinsight-hive-analyze-website-log/hdinsight-weblogs-sample.png
