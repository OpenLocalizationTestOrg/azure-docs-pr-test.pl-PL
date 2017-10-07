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
# <a name="sample-data-in-azure-hdinsight-hive-tables"></a><span data-ttu-id="01a77-103">Przykładowe dane w tabelach usługi Azure HDInsight Hive</span><span class="sxs-lookup"><span data-stu-id="01a77-103">Sample data in Azure HDInsight Hive tables</span></span>
<span data-ttu-id="01a77-104">W tym artykule opisano sposób toodown przykładowe dane przechowywane w tabelach platformy Azure HDInsight Hive za pomocą zapytań Hive.</span><span class="sxs-lookup"><span data-stu-id="01a77-104">In this article, we describe how toodown-sample data stored in Azure HDInsight Hive tables using Hive queries.</span></span> <span data-ttu-id="01a77-105">Firma Microsoft obejmuje trzy metody pobierania próbek popularly używany:</span><span class="sxs-lookup"><span data-stu-id="01a77-105">We cover three popularly used sampling methods:</span></span>

* <span data-ttu-id="01a77-106">Jednolite losowego pobierania próbek</span><span class="sxs-lookup"><span data-stu-id="01a77-106">Uniform random sampling</span></span>
* <span data-ttu-id="01a77-107">Losowe próbkowania według grup</span><span class="sxs-lookup"><span data-stu-id="01a77-107">Random sampling by groups</span></span>
* <span data-ttu-id="01a77-108">Stratyfikowana pobierania próbek</span><span class="sxs-lookup"><span data-stu-id="01a77-108">Stratified sampling</span></span>

<span data-ttu-id="01a77-109">następujące Hello **menu** łączy tootopics, które opisują sposób toosample danych z różnych środowiskach magazynu.</span><span class="sxs-lookup"><span data-stu-id="01a77-109">hello following **menu** links tootopics that describe how toosample data from various storage environments.</span></span>

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="01a77-110">**Dlaczego przykładowe dane?**</span><span class="sxs-lookup"><span data-stu-id="01a77-110">**Why sample your data?**</span></span>
<span data-ttu-id="01a77-111">Jeśli planujesz tooanalyze dataset hello jest duży, zazwyczaj jest to dobrze hello toodown przykładowych danych tooreduce jego rozmiar tooa mniejsze, ale reprezentatywny i łatwiejsze w zarządzaniu.</span><span class="sxs-lookup"><span data-stu-id="01a77-111">If hello dataset you plan tooanalyze is large, it's usually a good idea toodown-sample hello data tooreduce it tooa smaller but representative and more manageable size.</span></span> <span data-ttu-id="01a77-112">To ułatwia zrozumienie danych, badanie i inżynieria funkcji.</span><span class="sxs-lookup"><span data-stu-id="01a77-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="01a77-113">Swoją rolę w hello proces nauki danych zespołu jest szybkie tworzenie prototypów tooenable hello przetwarzania danych funkcji i modeli uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="01a77-113">Its role in hello Team Data Science Process is tooenable fast prototyping of hello data processing functions and machine learning models.</span></span>

<span data-ttu-id="01a77-114">To zadanie próbkowania jest etapem hello [zespołu danych nauki procesu (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="01a77-114">This sampling task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="how-toosubmit-hive-queries"></a><span data-ttu-id="01a77-115">Jak toosubmit zapytań programu Hive</span><span class="sxs-lookup"><span data-stu-id="01a77-115">How toosubmit Hive queries</span></span>
<span data-ttu-id="01a77-116">W konsoli usługi Hadoop wiersza polecenia hello na powitania węzła głównego klastra usługi Hadoop hello można przesłać zapytań programu hive.</span><span class="sxs-lookup"><span data-stu-id="01a77-116">Hive queries can be submitted from hello Hadoop Command Line console on hello head node of hello Hadoop cluster.</span></span> <span data-ttu-id="01a77-117">toodo to Zaloguj się do hello węzła głównego klastra usługi Hadoop hello, otwórz hello konsoli wiersza polecenia platformy Hadoop i wysyłanie zapytań programu Hive hello stamtąd.</span><span class="sxs-lookup"><span data-stu-id="01a77-117">toodo this, log into hello head node of hello Hadoop cluster, open hello Hadoop Command Line console, and submit hello Hive queries from there.</span></span> <span data-ttu-id="01a77-118">Aby uzyskać instrukcje dotyczące przesyłania zapytań programu Hive w konsoli usługi Hadoop wiersza polecenia hello, zobacz [jak tooSubmit zapytań Hive](machine-learning-data-science-move-hive-tables.md#submit).</span><span class="sxs-lookup"><span data-stu-id="01a77-118">For instructions on submitting Hive queries in hello Hadoop Command Line console, see [How tooSubmit Hive Queries](machine-learning-data-science-move-hive-tables.md#submit).</span></span>

## <span data-ttu-id="01a77-119"><a name="uniform"></a>Jednolite losowego pobierania próbek</span><span class="sxs-lookup"><span data-stu-id="01a77-119"><a name="uniform"></a> Uniform random sampling</span></span>
<span data-ttu-id="01a77-120">Jednolite próbkowania losowe oznacza, że każdego wiersza w zestawie danych hello ma taki sam sposób przez cały czas jest próbkowany.</span><span class="sxs-lookup"><span data-stu-id="01a77-120">Uniform random sampling means that each row in hello data set has an equal chance of being sampled.</span></span> <span data-ttu-id="01a77-121">Może być zaimplementowany przez dodanie zestawu danych toohello rand() dodatkowe pola w wewnętrznym zapytania "select" hello, a w hello zewnętrzne zapytania "select" tego warunku w polu losowych.</span><span class="sxs-lookup"><span data-stu-id="01a77-121">This can be implemented by adding an extra field rand() toohello data set in hello inner "select" query, and in hello outer "select" query that condition on that random field.</span></span>

<span data-ttu-id="01a77-122">Poniżej przedstawiono przykładowe zapytanie:</span><span class="sxs-lookup"><span data-stu-id="01a77-122">Here is an example query:</span></span>

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

<span data-ttu-id="01a77-123">W tym miejscu `<sample rate, 0-1>` określa hello część rekordów, które hello użytkownicy będą toosample.</span><span class="sxs-lookup"><span data-stu-id="01a77-123">Here, `<sample rate, 0-1>` specifies hello proportion of records that hello users want toosample.</span></span>

## <span data-ttu-id="01a77-124"><a name="group"></a>Losowe próbkowania według grup</span><span class="sxs-lookup"><span data-stu-id="01a77-124"><a name="group"></a> Random sampling by groups</span></span>
<span data-ttu-id="01a77-125">Podczas próbkowania danych podzielone na kategorie, może być tooeither dołączyć lub wykluczyć wszystkich wystąpień hello pewnej określonej wartości zmiennej podzielone na kategorie.</span><span class="sxs-lookup"><span data-stu-id="01a77-125">When sampling categorical data, you may want tooeither include or exclude all of hello instances of some particular value of a categorical variable.</span></span> <span data-ttu-id="01a77-126">Jest to, co oznacza "próbkowania przez grupę".</span><span class="sxs-lookup"><span data-stu-id="01a77-126">This is what is meant by "sampling by group".</span></span>
<span data-ttu-id="01a77-127">Na przykład jeśli zmienna kategorii "Stan", która zawiera wartości NY MA, urząd certyfikacji, NJ, PA, itp, rekordy z hello takim samym stanie zawsze być ze sobą, czy są pobierane, czy nie.</span><span class="sxs-lookup"><span data-stu-id="01a77-127">For example, if you have a categorical variable "State", which has values NY, MA, CA, NJ, PA, etc, you want records of hello same state be always together, whether they are sampled or not.</span></span>

<span data-ttu-id="01a77-128">Poniżej przedstawiono przykładowe zapytanie tej próbki przez grupę:</span><span class="sxs-lookup"><span data-stu-id="01a77-128">Here is an example query that samples by group:</span></span>

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

## <span data-ttu-id="01a77-129"><a name="stratified"></a>Stratyfikowana pobierania próbek</span><span class="sxs-lookup"><span data-stu-id="01a77-129"><a name="stratified"></a>Stratified sampling</span></span>
<span data-ttu-id="01a77-130">Losowe próbkowania jest uporządkować względem tooa podzielone na kategorie zmienną gdy próbki hello otrzymane wartości to podzielone na kategorie w hello zachowaniem jak hello nadrzędnego wypełniania, z których hello przykłady zostały uzyskane.</span><span class="sxs-lookup"><span data-stu-id="01a77-130">Random sampling is stratified with respect tooa categorical variable when hello samples obtained have values of that categorical that are in hello same ratio as in hello parent population from which hello samples were obtained.</span></span> <span data-ttu-id="01a77-131">Przy użyciu hello tym samym przykładzie, jako powyżej, załóżmy, że dane ma grupy przez Państwa, powiedz NJ ma 100 uwagi, NY ma 60 uwag, a WA ma 300 uwagi.</span><span class="sxs-lookup"><span data-stu-id="01a77-131">Using hello same example as above, suppose your data has sub-populations by states, say NJ has 100 observations, NY has 60 observations, and WA has 300 observations.</span></span> <span data-ttu-id="01a77-132">Jeśli określisz szybkość hello uporządkować toobe próbkowania 0,5, a następnie hello próbki uzyskane powinny mieć około 50, 30 i 150 obserwacji NJ, NY i WA odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="01a77-132">If you specify hello rate of stratified sampling toobe 0.5, then hello sample obtained should have approximately 50, 30, and 150 observations of NJ, NY, and WA respectively.</span></span>

<span data-ttu-id="01a77-133">Poniżej przedstawiono przykładowe zapytanie:</span><span class="sxs-lookup"><span data-stu-id="01a77-133">Here is an example query:</span></span>

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


<span data-ttu-id="01a77-134">Aby uzyskać informacje na bardziej zaawansowane metody pobierania próbek, które są dostępne w gałęzi, zobacz [LanguageManual próbkowania](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Sampling).</span><span class="sxs-lookup"><span data-stu-id="01a77-134">For information on more advanced sampling methods that are available in Hive, see [LanguageManual Sampling](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Sampling).</span></span>

