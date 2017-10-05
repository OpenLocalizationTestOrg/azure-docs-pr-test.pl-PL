---
title: "Przykładowe dane w tabelach platformy Azure HDInsight Hive | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: d46297dfaf85976114fbf610803e5f1a997041e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="sample-data-in-azure-hdinsight-hive-tables"></a><span data-ttu-id="145d9-103">Przykładowe dane w tabelach usługi Azure HDInsight Hive</span><span class="sxs-lookup"><span data-stu-id="145d9-103">Sample data in Azure HDInsight Hive tables</span></span>
<span data-ttu-id="145d9-104">W tym artykule firma Microsoft opisują sposób dół przykładowe dane przechowywane w tabelach platformy Azure HDInsight Hive za pomocą zapytań Hive.</span><span class="sxs-lookup"><span data-stu-id="145d9-104">In this article, we describe how to down-sample data stored in Azure HDInsight Hive tables using Hive queries.</span></span> <span data-ttu-id="145d9-105">Firma Microsoft obejmuje trzy metody pobierania próbek popularly używany:</span><span class="sxs-lookup"><span data-stu-id="145d9-105">We cover three popularly used sampling methods:</span></span>

* <span data-ttu-id="145d9-106">Jednolite losowego pobierania próbek</span><span class="sxs-lookup"><span data-stu-id="145d9-106">Uniform random sampling</span></span>
* <span data-ttu-id="145d9-107">Losowe próbkowania według grup</span><span class="sxs-lookup"><span data-stu-id="145d9-107">Random sampling by groups</span></span>
* <span data-ttu-id="145d9-108">Stratyfikowana pobierania próbek</span><span class="sxs-lookup"><span data-stu-id="145d9-108">Stratified sampling</span></span>

<span data-ttu-id="145d9-109">Następujące **menu** linki do tematów opisujących sposób przykładowe dane z różnych środowiskach magazynu.</span><span class="sxs-lookup"><span data-stu-id="145d9-109">The following **menu** links to topics that describe how to sample data from various storage environments.</span></span>

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="145d9-110">**Dlaczego przykładowe dane?**</span><span class="sxs-lookup"><span data-stu-id="145d9-110">**Why sample your data?**</span></span>
<span data-ttu-id="145d9-111">Jeśli zestaw danych, które mają być analizowanie jest duży, zazwyczaj jest dobrym rozwiązaniem w dół przykładowych danych, aby zmniejszyć jego rozmiar mniejsze, ale reprezentatywny i łatwiejsze w zarządzaniu.</span><span class="sxs-lookup"><span data-stu-id="145d9-111">If the dataset you plan to analyze is large, it's usually a good idea to down-sample the data to reduce it to a smaller but representative and more manageable size.</span></span> <span data-ttu-id="145d9-112">To ułatwia zrozumienie danych, badanie i inżynieria funkcji.</span><span class="sxs-lookup"><span data-stu-id="145d9-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="145d9-113">Swoją rolę w procesie nauki danych zespołu jest umożliwienie szybkiego prototypy funkcji przetwarzania danych i modeli uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="145d9-113">Its role in the Team Data Science Process is to enable fast prototyping of the data processing functions and machine learning models.</span></span>

<span data-ttu-id="145d9-114">To zadanie próbkowania jest krokiem w [zespołu danych nauki procesu (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="145d9-114">This sampling task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="how-to-submit-hive-queries"></a><span data-ttu-id="145d9-115">Temat dotyczący przesyłania zapytań programu Hive</span><span class="sxs-lookup"><span data-stu-id="145d9-115">How to submit Hive queries</span></span>
<span data-ttu-id="145d9-116">W konsoli usługi Hadoop wiersza polecenia na węzła głównego klastra usługi Hadoop można przesłać zapytań programu hive.</span><span class="sxs-lookup"><span data-stu-id="145d9-116">Hive queries can be submitted from the Hadoop Command Line console on the head node of the Hadoop cluster.</span></span> <span data-ttu-id="145d9-117">Aby to zrobić, zaloguj się do węzła głównego klastra usługi Hadoop, otwórz konsolę wiersza polecenia platformy Hadoop i wysyłanie zapytań programu Hive z tego miejsca.</span><span class="sxs-lookup"><span data-stu-id="145d9-117">To do this, log into the head node of the Hadoop cluster, open the Hadoop Command Line console, and submit the Hive queries from there.</span></span> <span data-ttu-id="145d9-118">Aby uzyskać instrukcje dotyczące przesyłania zapytań programu Hive w konsoli usługi Hadoop wiersza polecenia, zobacz [sposobu przesyłania zapytań Hive](machine-learning-data-science-move-hive-tables.md#submit).</span><span class="sxs-lookup"><span data-stu-id="145d9-118">For instructions on submitting Hive queries in the Hadoop Command Line console, see [How to Submit Hive Queries](machine-learning-data-science-move-hive-tables.md#submit).</span></span>

## <span data-ttu-id="145d9-119"><a name="uniform"></a>Jednolite losowego pobierania próbek</span><span class="sxs-lookup"><span data-stu-id="145d9-119"><a name="uniform"></a> Uniform random sampling</span></span>
<span data-ttu-id="145d9-120">Jednolite próbkowania losowe oznacza, że każdego wiersza w zestawie danych ma taki sam sposób przez cały czas jest próbkowany.</span><span class="sxs-lookup"><span data-stu-id="145d9-120">Uniform random sampling means that each row in the data set has an equal chance of being sampled.</span></span> <span data-ttu-id="145d9-121">To może być zaimplementowany przez dodanie rand() dodatkowe pola zestawu danych w wewnętrznym zapytania "select" i w zapytaniu "Wybierz" zewnętrzne tego warunku na losowe pola.</span><span class="sxs-lookup"><span data-stu-id="145d9-121">This can be implemented by adding an extra field rand() to the data set in the inner "select" query, and in the outer "select" query that condition on that random field.</span></span>

<span data-ttu-id="145d9-122">Poniżej przedstawiono przykładowe zapytanie:</span><span class="sxs-lookup"><span data-stu-id="145d9-122">Here is an example query:</span></span>

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

<span data-ttu-id="145d9-123">W tym miejscu `<sample rate, 0-1>` określa część rekordów, które użytkownicy mają do próbkowania.</span><span class="sxs-lookup"><span data-stu-id="145d9-123">Here, `<sample rate, 0-1>` specifies the proportion of records that the users want to sample.</span></span>

## <span data-ttu-id="145d9-124"><a name="group"></a>Losowe próbkowania według grup</span><span class="sxs-lookup"><span data-stu-id="145d9-124"><a name="group"></a> Random sampling by groups</span></span>
<span data-ttu-id="145d9-125">Podczas pobierania próbek danych podzielone na kategorie, warto uwzględnić lub wykluczyć wszystkie wystąpienia niektórych określonej wartości zmiennej podzielone na kategorie.</span><span class="sxs-lookup"><span data-stu-id="145d9-125">When sampling categorical data, you may want to either include or exclude all of the instances of some particular value of a categorical variable.</span></span> <span data-ttu-id="145d9-126">Jest to, co oznacza "próbkowania przez grupę".</span><span class="sxs-lookup"><span data-stu-id="145d9-126">This is what is meant by "sampling by group".</span></span>
<span data-ttu-id="145d9-127">Na przykład jeśli zmienna kategorii "Stan", która zawiera wartości NY MA, urząd certyfikacji, NJ, PA, itp, mają rekordy z takim samym stanie zawsze być ze sobą, czy są próbkowane lub nie.</span><span class="sxs-lookup"><span data-stu-id="145d9-127">For example, if you have a categorical variable "State", which has values NY, MA, CA, NJ, PA, etc, you want records of the same state be always together, whether they are sampled or not.</span></span>

<span data-ttu-id="145d9-128">Poniżej przedstawiono przykładowe zapytanie tej próbki przez grupę:</span><span class="sxs-lookup"><span data-stu-id="145d9-128">Here is an example query that samples by group:</span></span>

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

## <span data-ttu-id="145d9-129"><a name="stratified"></a>Stratyfikowana pobierania próbek</span><span class="sxs-lookup"><span data-stu-id="145d9-129"><a name="stratified"></a>Stratified sampling</span></span>
<span data-ttu-id="145d9-130">Losowe próbkowania jest uporządkować względem zmienną podzielone na kategorie gdy próbki otrzymane wartości czy podzielone na kategorie które znajdują się w tej samej stosunek jak populacji nadrzędnej, z którego uzyskano próbek.</span><span class="sxs-lookup"><span data-stu-id="145d9-130">Random sampling is stratified with respect to a categorical variable when the samples obtained have values of that categorical that are in the same ratio as in the parent population from which the samples were obtained.</span></span> <span data-ttu-id="145d9-131">W tym samym przykładzie jako powyżej, załóżmy, że dane mają grupy przez Państwa, co oznacza NJ ma 100 uwagi, NY ma 60 uwag, a WA ma 300 uwag.</span><span class="sxs-lookup"><span data-stu-id="145d9-131">Using the same example as above, suppose your data has sub-populations by states, say NJ has 100 observations, NY has 60 observations, and WA has 300 observations.</span></span> <span data-ttu-id="145d9-132">Jeśli określisz częstotliwość próbkowania stratyfikowana jako 0,5, następnie otrzymaną próbkę ma około 50, 30 i 150 obserwacji NJ, NY i WA odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="145d9-132">If you specify the rate of stratified sampling to be 0.5, then the sample obtained should have approximately 50, 30, and 150 observations of NJ, NY, and WA respectively.</span></span>

<span data-ttu-id="145d9-133">Poniżej przedstawiono przykładowe zapytanie:</span><span class="sxs-lookup"><span data-stu-id="145d9-133">Here is an example query:</span></span>

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


<span data-ttu-id="145d9-134">Aby uzyskać informacje na bardziej zaawansowane metody pobierania próbek, które są dostępne w gałęzi, zobacz [LanguageManual próbkowania](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Sampling).</span><span class="sxs-lookup"><span data-stu-id="145d9-134">For information on more advanced sampling methods that are available in Hive, see [LanguageManual Sampling](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Sampling).</span></span>

