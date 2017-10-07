---
title: aaaSample dane w tabelach platformy Azure HDInsight Hive | Dokumentacja firmy Microsoft
description: "Dół próbkowania dane w tabelach Hive w usłudze Azure HDInsight (Hadopop)"
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: f31e8d01-0fd4-4a10-b1a7-35de3c327521
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: 5f86df9b5a18facc875f437abfb004dbe3a06ea4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sample-data-in-azure-hdinsight-hive-tables"></a>Przykładowe dane w tabelach usługi Azure HDInsight Hive
W tym artykule opisano sposób toodown przykładowe dane przechowywane w tabelach platformy Azure HDInsight Hive za pomocą zapytań Hive. Firma Microsoft obejmuje trzy metody pobierania próbek popularly używany:

* Jednolite losowego pobierania próbek
* Losowe próbkowania według grup
* Stratyfikowana pobierania próbek

następujące Hello **menu** łączy tootopics, które opisują sposób toosample danych z różnych środowiskach magazynu.

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

**Dlaczego przykładowe dane?**
Jeśli planujesz tooanalyze dataset hello jest duży, zazwyczaj jest to dobrze hello toodown przykładowych danych tooreduce jego rozmiar tooa mniejsze, ale reprezentatywny i łatwiejsze w zarządzaniu. To ułatwia zrozumienie danych, badanie i inżynieria funkcji. Swoją rolę w hello proces nauki danych zespołu jest szybkie tworzenie prototypów tooenable hello przetwarzania danych funkcji i modeli uczenia maszynowego.

To zadanie próbkowania jest etapem hello [zespołu danych nauki procesu (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

## <a name="how-toosubmit-hive-queries"></a>Jak toosubmit zapytań programu Hive
W konsoli usługi Hadoop wiersza polecenia hello na powitania węzła głównego klastra usługi Hadoop hello można przesłać zapytań programu hive. toodo to Zaloguj się do hello węzła głównego klastra usługi Hadoop hello, otwórz hello konsoli wiersza polecenia platformy Hadoop i wysyłanie zapytań programu Hive hello stamtąd. Aby uzyskać instrukcje dotyczące przesyłania zapytań programu Hive w konsoli usługi Hadoop wiersza polecenia hello, zobacz [jak tooSubmit zapytań Hive](machine-learning-data-science-move-hive-tables.md#submit).

## <a name="uniform"></a>Jednolite losowego pobierania próbek
Jednolite próbkowania losowe oznacza, że każdego wiersza w zestawie danych hello ma taki sam sposób przez cały czas jest próbkowany. Może być zaimplementowany przez dodanie zestawu danych toohello rand() dodatkowe pola w wewnętrznym zapytania "select" hello, a w hello zewnętrzne zapytania "select" tego warunku w polu losowych.

Poniżej przedstawiono przykładowe zapytanie:

    SET sampleRate=<sample rate, 0-1>;
    select
        field1, field2, …, fieldN
    from
        (
        select
            field1, field2, …, fieldN, rand() as samplekey
        from <hive table name>
        )a
    where samplekey<='${hiveconf:sampleRate}'

W tym miejscu `<sample rate, 0-1>` określa hello część rekordów, które hello użytkownicy będą toosample.

## <a name="group"></a>Losowe próbkowania według grup
Podczas próbkowania danych podzielone na kategorie, może być tooeither dołączyć lub wykluczyć wszystkich wystąpień hello pewnej określonej wartości zmiennej podzielone na kategorie. Jest to, co oznacza "próbkowania przez grupę".
Na przykład jeśli zmienna kategorii "Stan", która zawiera wartości NY MA, urząd certyfikacji, NJ, PA, itp, rekordy z hello takim samym stanie zawsze być ze sobą, czy są pobierane, czy nie.

Poniżej przedstawiono przykładowe zapytanie tej próbki przez grupę:

    SET sampleRate=<sample rate, 0-1>;
    select
        b.field1, b.field2, …, b.catfield, …, b.fieldN
    from
        (
        select
            field1, field2, …, catfield, …, fieldN
        from <table name>
        )b
    join
        (
        select
            catfield
        from
            (
            select
                catfield, rand() as samplekey
            from <table name>
            group by catfield
            )a
        where samplekey<='${hiveconf:sampleRate}'
        )c
    on b.catfield=c.catfield

## <a name="stratified"></a>Stratyfikowana pobierania próbek
Losowe próbkowania jest uporządkować względem tooa podzielone na kategorie zmienną gdy próbki hello otrzymane wartości to podzielone na kategorie w hello zachowaniem jak hello nadrzędnego wypełniania, z których hello przykłady zostały uzyskane. Przy użyciu hello tym samym przykładzie, jako powyżej, załóżmy, że dane ma grupy przez Państwa, powiedz NJ ma 100 uwagi, NY ma 60 uwag, a WA ma 300 uwagi. Jeśli określisz szybkość hello uporządkować toobe próbkowania 0,5, a następnie hello próbki uzyskane powinny mieć około 50, 30 i 150 obserwacji NJ, NY i WA odpowiednio.

Poniżej przedstawiono przykładowe zapytanie:

    SET sampleRate=<sample rate, 0-1>;
    select
        field1, field2, field3, ..., fieldN, state
    from
        (
        select
            field1, field2, field3, ..., fieldN, state,
            count(*) over (partition by state) as state_cnt,
              rank() over (partition by state order by rand()) as state_rank
          from <table name>
        ) a
    where state_rank <= state_cnt*'${hiveconf:sampleRate}'


Aby uzyskać informacje na bardziej zaawansowane metody pobierania próbek, które są dostępne w gałęzi, zobacz [LanguageManual próbkowania](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Sampling).

