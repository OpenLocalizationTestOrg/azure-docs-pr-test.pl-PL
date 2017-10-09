---
title: aaaWhat jest Apache Hive i HiveQL - Azure HDInsight | Dokumentacja firmy Microsoft
description: "Apache Hive jest platforma Hadoop w systemie magazynu danych. Można badać danych przechowywanych w gałęzi przy użyciu HiveQL, które podobne tooTransact-SQL. W tym dokumencie przedstawiono sposób toouse Hive i HiveQL z usługą Azure HDInsight."
keywords: "hiveql, co to jest hive i hadoop hiveql, jak toouse hive, Dowiedz się, hive, co to jest gałąź"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2c10f989-7636-41bf-b7f7-c4b67ec0814f
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.openlocfilehash: a2772312263895ff99b499898264c2e6d5e816e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-apache-hive-and-hiveql-on-azure-hdinsight"></a><span data-ttu-id="6f504-106">Co to jest Apache Hive i HiveQL w usłudze Azure HDInsight?</span><span class="sxs-lookup"><span data-stu-id="6f504-106">What is Apache Hive and HiveQL on Azure HDInsight?</span></span>

<span data-ttu-id="6f504-107">[Apache Hive](http://hive.apache.org/) jest systemem magazynu danych dla platformy Hadoop.</span><span class="sxs-lookup"><span data-stu-id="6f504-107">[Apache Hive](http://hive.apache.org/) is a data warehouse system for Hadoop.</span></span> <span data-ttu-id="6f504-108">Gałąź umożliwia podsumowania danych, wyszukiwanie i analizy danych.</span><span class="sxs-lookup"><span data-stu-id="6f504-108">Hive enables data summarization, querying, and analysis of data.</span></span> <span data-ttu-id="6f504-109">Zapytań programu hive są zapisywane w HiveQL, czyli tooSQL podobne języka zapytań.</span><span class="sxs-lookup"><span data-stu-id="6f504-109">Hive queries are written in HiveQL, which is a query language similar tooSQL.</span></span>

<span data-ttu-id="6f504-110">Gałąź umożliwia tooproject struktury danych niestrukturalnych w dużej mierze.</span><span class="sxs-lookup"><span data-stu-id="6f504-110">Hive allows you tooproject structure on largely unstructured data.</span></span> <span data-ttu-id="6f504-111">Po zdefiniowaniu struktury hello służy HiveQL tooquery hello danych bez znajomości języka Java lub MapReduce.</span><span class="sxs-lookup"><span data-stu-id="6f504-111">After you define hello structure, you can use HiveQL tooquery hello data without knowledge of Java or MapReduce.</span></span>

<span data-ttu-id="6f504-112">Usługa HDInsight zapewnia kilka typów klastra, które są dopasowane do konkretnych obciążeń.</span><span class="sxs-lookup"><span data-stu-id="6f504-112">HDInsight provides several cluster types, which are tuned for specific workloads.</span></span> <span data-ttu-id="6f504-113">następujące typy klastrów Hello są najczęściej używane dla zapytań programu Hive:</span><span class="sxs-lookup"><span data-stu-id="6f504-113">hello following cluster types are most often used for Hive queries:</span></span>

* <span data-ttu-id="6f504-114">__Interakcyjne Hive__: klastra usługi Hadoop A, która zapewnia [niskim opóźnieniu analitycznego przetwarzania (LLAP)](https://cwiki.apache.org/confluence/display/Hive/LLAP) czas odpowiedzi tooimprove funkcje dla interakcyjnych zapytań.</span><span class="sxs-lookup"><span data-stu-id="6f504-114">__Interactive Hive__: A Hadoop cluster that provides [Low Latency Analytical Processing (LLAP)](https://cwiki.apache.org/confluence/display/Hive/LLAP) functionality tooimprove response times for interactive queries.</span></span> <span data-ttu-id="6f504-115">Aby uzyskać więcej informacji, zobacz hello [rozpoczynać interakcyjne Hive w usłudze HDInsight](hdinsight-hadoop-use-interactive-hive.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="6f504-115">For more information, see hello [Start with Interactive Hive in HDInsight](hdinsight-hadoop-use-interactive-hive.md) document.</span></span>

* <span data-ttu-id="6f504-116">__Hadoop__: klaster A Hadoop dostosowana pod kątem obciążeń przetwarzania wsadowego.</span><span class="sxs-lookup"><span data-stu-id="6f504-116">__Hadoop__: A Hadoop cluster that is tuned for batch processing workloads.</span></span> <span data-ttu-id="6f504-117">Aby uzyskać więcej informacji, zobacz hello [Start z usługą Hadoop w usłudze HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="6f504-117">For more information, see hello [Start with Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md) document.</span></span>

* <span data-ttu-id="6f504-118">__Platforma Spark__: platforma Apache Spark ma wbudowaną funkcję do pracy z gałęzi.</span><span class="sxs-lookup"><span data-stu-id="6f504-118">__Spark__: Apache Spark has built-in functionality for working with Hive.</span></span> <span data-ttu-id="6f504-119">Aby uzyskać więcej informacji, zobacz hello [rozpoczynać Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="6f504-119">For more information, see hello [Start with Spark on HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md) document.</span></span>

* <span data-ttu-id="6f504-120">__HBase__: HiveQL mogą być używane tooquery danych przechowywanych w bazie danych HBase.</span><span class="sxs-lookup"><span data-stu-id="6f504-120">__HBase__: HiveQL can be used tooquery data stored in HBase.</span></span> <span data-ttu-id="6f504-121">Aby uzyskać więcej informacji, zobacz hello [rozpoczynać się od bazy danych HBase w usłudze HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="6f504-121">For more information, see hello [Start with HBase on HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) document.</span></span>

## <a name="how-toouse-hive"></a><span data-ttu-id="6f504-122">Jak Hive toouse</span><span class="sxs-lookup"><span data-stu-id="6f504-122">How toouse Hive</span></span>

<span data-ttu-id="6f504-123">Użyj poniższej hello tabeli toodiscover jak toouse Hive z usługą HDInsight:</span><span class="sxs-lookup"><span data-stu-id="6f504-123">Use hello following table toodiscover how toouse Hive with HDInsight:</span></span>

| <span data-ttu-id="6f504-124">**Ta metoda** Jeśli chcesz...</span><span class="sxs-lookup"><span data-stu-id="6f504-124">**Use this method** if you want...</span></span> | <span data-ttu-id="6f504-125">.. .an **interakcyjne** powłoki</span><span class="sxs-lookup"><span data-stu-id="6f504-125">...an **interactive** shell</span></span> | <span data-ttu-id="6f504-126">... **partii** przetwarzania</span><span class="sxs-lookup"><span data-stu-id="6f504-126">...**batch** processing</span></span> | <span data-ttu-id="6f504-127">.. zwykle to **systemu operacyjnego klastra**</span><span class="sxs-lookup"><span data-stu-id="6f504-127">...with this **cluster operating system**</span></span> | <span data-ttu-id="6f504-128">.. .from to **system operacyjny klienta**</span><span class="sxs-lookup"><span data-stu-id="6f504-128">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="6f504-129">Widok gałęzi</span><span class="sxs-lookup"><span data-stu-id="6f504-129">Hive View</span></span>](hdinsight-hadoop-use-hive-ambari-view.md) |<span data-ttu-id="6f504-130">✔</span><span class="sxs-lookup"><span data-stu-id="6f504-130">✔</span></span> |<span data-ttu-id="6f504-131">✔</span><span class="sxs-lookup"><span data-stu-id="6f504-131">✔</span></span> |<span data-ttu-id="6f504-132">Linux</span><span class="sxs-lookup"><span data-stu-id="6f504-132">Linux</span></span> |<span data-ttu-id="6f504-133">Wszelkie (opartych na przeglądarce)</span><span class="sxs-lookup"><span data-stu-id="6f504-133">Any (browser based)</span></span> |
| [<span data-ttu-id="6f504-134">Beeline klienta</span><span class="sxs-lookup"><span data-stu-id="6f504-134">Beeline client</span></span>](hdinsight-hadoop-use-hive-beeline.md) |<span data-ttu-id="6f504-135">✔</span><span class="sxs-lookup"><span data-stu-id="6f504-135">✔</span></span> |<span data-ttu-id="6f504-136">✔</span><span class="sxs-lookup"><span data-stu-id="6f504-136">✔</span></span> |<span data-ttu-id="6f504-137">Linux</span><span class="sxs-lookup"><span data-stu-id="6f504-137">Linux</span></span> |<span data-ttu-id="6f504-138">Linux, Unix, Mac OS X lub systemu Windows</span><span class="sxs-lookup"><span data-stu-id="6f504-138">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="6f504-139">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="6f504-139">REST API</span></span>](hdinsight-hadoop-use-hive-curl.md) |&nbsp; |<span data-ttu-id="6f504-140">✔</span><span class="sxs-lookup"><span data-stu-id="6f504-140">✔</span></span> |<span data-ttu-id="6f504-141">Linux lub Windows *</span><span class="sxs-lookup"><span data-stu-id="6f504-141">Linux or Windows*</span></span> |<span data-ttu-id="6f504-142">Linux, Unix, Mac OS X lub systemu Windows</span><span class="sxs-lookup"><span data-stu-id="6f504-142">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="6f504-143">Narzędzia HDInsight tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6f504-143">HDInsight tools for Visual Studio</span></span>](hdinsight-hadoop-use-hive-visual-studio.md) |&nbsp; |<span data-ttu-id="6f504-144">✔</span><span class="sxs-lookup"><span data-stu-id="6f504-144">✔</span></span> |<span data-ttu-id="6f504-145">Linux lub Windows *</span><span class="sxs-lookup"><span data-stu-id="6f504-145">Linux or Windows*</span></span> |<span data-ttu-id="6f504-146">Windows</span><span class="sxs-lookup"><span data-stu-id="6f504-146">Windows</span></span> |
| [<span data-ttu-id="6f504-147">Środowisko Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="6f504-147">Windows PowerShell</span></span>](hdinsight-hadoop-use-hive-powershell.md) |&nbsp; |<span data-ttu-id="6f504-148">✔</span><span class="sxs-lookup"><span data-stu-id="6f504-148">✔</span></span> |<span data-ttu-id="6f504-149">Linux lub Windows *</span><span class="sxs-lookup"><span data-stu-id="6f504-149">Linux or Windows*</span></span> |<span data-ttu-id="6f504-150">Windows</span><span class="sxs-lookup"><span data-stu-id="6f504-150">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="6f504-151">\*Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="6f504-151">\* Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="6f504-152">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="6f504-152">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="6f504-153">Jeśli korzystasz z klastra usługi HDInsight opartej na systemie Windows, możesz użyć hello [konsoli zapytania](hdinsight-hadoop-use-hive-query-console.md) z przeglądarki lub [pulpitu zdalnego](hdinsight-hadoop-use-hive-remote-desktop.md) toorun zapytań programu Hive.</span><span class="sxs-lookup"><span data-stu-id="6f504-153">If you are using a Windows-based HDInsight cluster, you can use hello [Query console](hdinsight-hadoop-use-hive-query-console.md) from your browser or [Remote Desktop](hdinsight-hadoop-use-hive-remote-desktop.md) toorun Hive queries.</span></span>

## <a name="hiveql-language-reference"></a><span data-ttu-id="6f504-154">Dokumentacja języka HiveQL</span><span class="sxs-lookup"><span data-stu-id="6f504-154">HiveQL language reference</span></span>

<span data-ttu-id="6f504-155">Dokumentacja języka HiveQL jest dostępna w hello [ręcznego języka (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual).</span><span class="sxs-lookup"><span data-stu-id="6f504-155">HiveQL language reference is available in hello [language manual (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual).</span></span>

## <a name="hive-and-data-structure"></a><span data-ttu-id="6f504-156">Struktura danych i hive</span><span class="sxs-lookup"><span data-stu-id="6f504-156">Hive and data structure</span></span>

<span data-ttu-id="6f504-157">Gałąź rozumie struktury toowork z i częściowo ustrukturyzowanych danych.</span><span class="sxs-lookup"><span data-stu-id="6f504-157">Hive understands how toowork with structured and semi-structured data.</span></span> <span data-ttu-id="6f504-158">Na przykład pliki tekstowe gdzie hello pola są rozdzielone określonych znaków.</span><span class="sxs-lookup"><span data-stu-id="6f504-158">For example, text files where hello fields are delimited by specific characters.</span></span> <span data-ttu-id="6f504-159">Po instrukcji HiveQL Hello tworzy tabelę danych rozdzielonych spacjami:</span><span class="sxs-lookup"><span data-stu-id="6f504-159">hello following HiveQL statement creates a table over space-delimited data:</span></span>

```hiveql
CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
STORED AS TEXTFILE LOCATION '/example/data/';
```

<span data-ttu-id="6f504-160">Hive obsługuje również niestandardowe **serializator/deserializers (SerDe)** złożonego lub nieregularnych strukturalnych danych.</span><span class="sxs-lookup"><span data-stu-id="6f504-160">Hive also supports custom **serializer/deserializers (SerDe)** for complex or irregularly structured data.</span></span> <span data-ttu-id="6f504-161">Aby uzyskać więcej informacji, zobacz hello [jak toouse niestandardowych SerDe JSON z usługą HDInsight](http://blogs.msdn.com/b/bigdatasupport/archive/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight.aspx) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="6f504-161">For more information, see hello [How toouse a custom JSON SerDe with HDInsight](http://blogs.msdn.com/b/bigdatasupport/archive/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight.aspx) document.</span></span>

<span data-ttu-id="6f504-162">Aby uzyskać więcej informacji na formaty plików obsługiwane przez Hive, zobacz hello [ręcznego języka (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)</span><span class="sxs-lookup"><span data-stu-id="6f504-162">For more information on file formats supported by Hive, see hello [Language manual (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)</span></span>

## <a name="hive-internal-tables-vs-external-tables"></a><span data-ttu-id="6f504-163">Hive tabel zewnętrznych vs wewnętrzny tabel</span><span class="sxs-lookup"><span data-stu-id="6f504-163">Hive internal tables vs external tables</span></span>

<span data-ttu-id="6f504-164">Istnieją dwa typy tabel, które można utworzyć przy użyciu Hive:</span><span class="sxs-lookup"><span data-stu-id="6f504-164">There are two types of tables that you can create with Hive:</span></span>

* <span data-ttu-id="6f504-165">__Wewnętrzny__: dane są przechowywane w magazynie danych hello Hive.</span><span class="sxs-lookup"><span data-stu-id="6f504-165">__Internal__: Data is stored in hello Hive data warehouse.</span></span> <span data-ttu-id="6f504-166">Witaj hurtowni danych znajduje się pod adresem `/hive/warehouse/` na powitania domyślny magazyn dla klastra hello.</span><span class="sxs-lookup"><span data-stu-id="6f504-166">hello data warehouse is located at `/hive/warehouse/` on hello default storage for hello cluster.</span></span>

    <span data-ttu-id="6f504-167">Użyj wewnętrznego tabel, gdy:</span><span class="sxs-lookup"><span data-stu-id="6f504-167">Use internal tables when:</span></span>

    * <span data-ttu-id="6f504-168">Dane są tymczasowe.</span><span class="sxs-lookup"><span data-stu-id="6f504-168">Data is temporary.</span></span>
    * <span data-ttu-id="6f504-169">Mają cykl życia hello toomanage Hive hello tabeli i danych.</span><span class="sxs-lookup"><span data-stu-id="6f504-169">You want Hive toomanage hello lifecycle of hello table and data.</span></span>

* <span data-ttu-id="6f504-170">__Zewnętrzne__: dane są przechowywane poza hello hurtowni danych.</span><span class="sxs-lookup"><span data-stu-id="6f504-170">__External__: Data is stored outside hello data warehouse.</span></span> <span data-ttu-id="6f504-171">Witaj danych mogą być przechowywane na każdy Magazyn dostępny przez klaster hello.</span><span class="sxs-lookup"><span data-stu-id="6f504-171">hello data can be stored on any storage accessible by hello cluster.</span></span>

    <span data-ttu-id="6f504-172">Użyj tabel zewnętrznych, gdy:</span><span class="sxs-lookup"><span data-stu-id="6f504-172">Use external tables when:</span></span>

    * <span data-ttu-id="6f504-173">dane Hello jest również używany poza Hive.</span><span class="sxs-lookup"><span data-stu-id="6f504-173">hello data is also used outside of Hive.</span></span> <span data-ttu-id="6f504-174">Na przykład pliki danych hello są aktualizowane przez inny proces (co oznacza, że nie blokuje pliki hello.)</span><span class="sxs-lookup"><span data-stu-id="6f504-174">For example, hello data files are updated by another process (that does not lock hello files.)</span></span>
    * <span data-ttu-id="6f504-175">Dane muszą tooremain w hello bazowy lokalizacji, nawet po porzucenie hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="6f504-175">Data needs tooremain in hello underlying location, even after dropping hello table.</span></span>
    * <span data-ttu-id="6f504-176">Należy lokalizacjach niestandardowych, takich jak konta magazynu z systemem innym niż domyślny.</span><span class="sxs-lookup"><span data-stu-id="6f504-176">You need a custom location, such as a non-default storage account.</span></span>
    * <span data-ttu-id="6f504-177">Z programem innym niż hive zarządza hello format danych, lokalizacji itp.</span><span class="sxs-lookup"><span data-stu-id="6f504-177">A program other than hive manages hello data format, location, etc.</span></span>

<span data-ttu-id="6f504-178">Aby uzyskać więcej informacji, zobacz hello [Hive wewnętrznych i zewnętrznych wprowadzenie tabel] [ cindygross-hive-tables] wpis w blogu.</span><span class="sxs-lookup"><span data-stu-id="6f504-178">For more information, see hello [Hive Internal and External Tables Intro][cindygross-hive-tables] blog post.</span></span>

## <a name="user-defined-functions-udf"></a><span data-ttu-id="6f504-179">Funkcje zdefiniowane przez użytkownika (UDF)</span><span class="sxs-lookup"><span data-stu-id="6f504-179">User-defined functions (UDF)</span></span>

<span data-ttu-id="6f504-180">Można również rozszerzać hive za pośrednictwem **funkcje zdefiniowane przez użytkownika (UDF)**.</span><span class="sxs-lookup"><span data-stu-id="6f504-180">Hive can also be extended through **user-defined functions (UDF)**.</span></span> <span data-ttu-id="6f504-181">UDF umożliwia funkcjonalności tooimplement lub logikę, która nie jest łatwo uformowana w HiveQL.</span><span class="sxs-lookup"><span data-stu-id="6f504-181">A UDF allows you tooimplement functionality or logic that isn't easily modeled in HiveQL.</span></span> <span data-ttu-id="6f504-182">Przykład przy użyciu Hive za pomocą funkcji UDF Zobacz hello w następujących dokumentach:</span><span class="sxs-lookup"><span data-stu-id="6f504-182">For an example of using UDFs with Hive, see hello following documents:</span></span>

* [<span data-ttu-id="6f504-183">Użyj funkcji zdefiniowanej przez użytkownika języka Java przy użyciu Hive</span><span class="sxs-lookup"><span data-stu-id="6f504-183">Use a Java user-defined function with Hive</span></span>](hdinsight-hadoop-hive-java-udf.md)

* [<span data-ttu-id="6f504-184">Użyj funkcji zdefiniowanej przez użytkownika Python z Hive i Pig</span><span class="sxs-lookup"><span data-stu-id="6f504-184">Use a Python user-defined function with Hive and Pig</span></span>](hdinsight-python.md)

* [<span data-ttu-id="6f504-185">C# — funkcja zdefiniowana przez użytkownika za pomocą technologii Hive i Pig</span><span class="sxs-lookup"><span data-stu-id="6f504-185">Use a C# user-defined function with Hive and Pig</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [<span data-ttu-id="6f504-186">Jak tooadd gałąź niestandardowe zdefiniowane przez użytkownika funkcji tooHDInsight</span><span class="sxs-lookup"><span data-stu-id="6f504-186">How tooadd a custom Hive user-defined function tooHDInsight</span></span>](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

* [<span data-ttu-id="6f504-187">Przykład Hive funkcja zdefiniowana przez użytkownika tooconvert formaty daty i godziny tooHive sygnatury czasowej</span><span class="sxs-lookup"><span data-stu-id="6f504-187">An example Hive user-defined function tooconvert date/time formats tooHive timestamp</span></span>](https://github.com/Azure-Samples/hdinsight-java-hive-udf)

## <span data-ttu-id="6f504-188"><a id="data"></a>Przykładowe dane</span><span class="sxs-lookup"><span data-stu-id="6f504-188"><a id="data"></a>Example data</span></span>

<span data-ttu-id="6f504-189">Hive w usłudze HDInsight jest dostarczany wstępnie załadowane z wewnętrznej tabeli o nazwie `hivesampletable`.</span><span class="sxs-lookup"><span data-stu-id="6f504-189">Hive on HDInsight comes pre-loaded with an internal table named `hivesampletable`.</span></span> <span data-ttu-id="6f504-190">Usługa HDInsight zapewnia również przykład zestawów danych, które mogą być używane z gałęzi.</span><span class="sxs-lookup"><span data-stu-id="6f504-190">HDInsight also provides example data sets that can be used with Hive.</span></span> <span data-ttu-id="6f504-191">Te zestawy danych są przechowywane w hello `/example/data` i `/HdiSamples` katalogów.</span><span class="sxs-lookup"><span data-stu-id="6f504-191">These data sets are stored in hello `/example/data` and `/HdiSamples` directories.</span></span> <span data-ttu-id="6f504-192">Te katalogi istnieją w hello domyślny magazyn dla klastra.</span><span class="sxs-lookup"><span data-stu-id="6f504-192">These directories exist in hello default storage for your cluster.</span></span>

## <span data-ttu-id="6f504-193"><a id="job"></a>Przykładowe zapytanie Hive</span><span class="sxs-lookup"><span data-stu-id="6f504-193"><a id="job"></a>Example Hive query</span></span>

<span data-ttu-id="6f504-194">Witaj, następujące kolumny projektu instrukcje HiveQL na powitania `/example/data/sample.log` pliku:</span><span class="sxs-lookup"><span data-stu-id="6f504-194">hello following HiveQL statements project columns onto hello `/example/data/sample.log` file:</span></span>

    set hive.execution.engine=tez;
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

<span data-ttu-id="6f504-195">W poprzednim przykładzie hello instrukcje HiveQL hello wykonaj hello następujące akcje:</span><span class="sxs-lookup"><span data-stu-id="6f504-195">In hello previous example, hello HiveQL statements perform hello following actions:</span></span>

* <span data-ttu-id="6f504-196">`set hive.execution.engine=tez;`: Ustawia hello wykonywania aparatu toouse Tez.</span><span class="sxs-lookup"><span data-stu-id="6f504-196">`set hive.execution.engine=tez;`: Sets hello execution engine toouse Tez.</span></span> <span data-ttu-id="6f504-197">Przy użyciu aplikacji Tez zamiast MapReduce zapewnić wzrost wydajności zapytań.</span><span class="sxs-lookup"><span data-stu-id="6f504-197">Using Tez instead of MapReduce can provide an increase in query performance.</span></span> <span data-ttu-id="6f504-198">Aby uzyskać więcej informacji o aplikacji Tez, zobacz hello [Użyj Apache Tez zwiększonej wydajności](#usetez) sekcji.</span><span class="sxs-lookup"><span data-stu-id="6f504-198">For more information on Tez, see hello [Use Apache Tez for improved performance](#usetez) section.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6f504-199">Ta instrukcja jest tylko wymagane w przypadku korzystania z klastra usługi HDInsight opartej na systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="6f504-199">This statement is only required when using a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="6f504-200">Tez jest hello domyślnego wykonywania aparatu dla usługi HDInsight opartej na systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="6f504-200">Tez is hello default execution engine for Linux-based HDInsight.</span></span>

* <span data-ttu-id="6f504-201">`DROP TABLE`: Jeśli hello tabela już istnieje, usuń go.</span><span class="sxs-lookup"><span data-stu-id="6f504-201">`DROP TABLE`: If hello table already exists, delete it.</span></span>

* <span data-ttu-id="6f504-202">`CREATE EXTERNAL TABLE`: Tworzy nowy **zewnętrznych** tabeli w gałęzi rejestru.</span><span class="sxs-lookup"><span data-stu-id="6f504-202">`CREATE EXTERNAL TABLE`: Creates a new **external** table in Hive.</span></span> <span data-ttu-id="6f504-203">Tabele zewnętrzne przechowywać tylko hello definicji tabeli w gałęzi.</span><span class="sxs-lookup"><span data-stu-id="6f504-203">External tables only store hello table definition in Hive.</span></span> <span data-ttu-id="6f504-204">Hello danych pozostaje w oryginalnej lokalizacji hello i hello oryginalnym formacie.</span><span class="sxs-lookup"><span data-stu-id="6f504-204">hello data is left in hello original location and in hello original format.</span></span>

* <span data-ttu-id="6f504-205">`ROW FORMAT`: Określa, że sposób formatowania danych hello Hive.</span><span class="sxs-lookup"><span data-stu-id="6f504-205">`ROW FORMAT`: Tells Hive how hello data is formatted.</span></span> <span data-ttu-id="6f504-206">W takim przypadku hello pól w każdym dzienniku są oddzielone spacją.</span><span class="sxs-lookup"><span data-stu-id="6f504-206">In this case, hello fields in each log are separated by a space.</span></span>

* <span data-ttu-id="6f504-207">`STORED AS TEXTFILE LOCATION`: Nakazuje Hive gdzie hello są przechowywane dane (hello `example/data` katalogu) i które są przechowywane jako tekst.</span><span class="sxs-lookup"><span data-stu-id="6f504-207">`STORED AS TEXTFILE LOCATION`: Tells Hive where hello data is stored (hello `example/data` directory) and that it is stored as text.</span></span> <span data-ttu-id="6f504-208">można w jednym pliku lub rozłożyć na wiele plików w katalogu hello Hello danych.</span><span class="sxs-lookup"><span data-stu-id="6f504-208">hello data can be in one file or spread across multiple files within hello directory.</span></span>

* <span data-ttu-id="6f504-209">`SELECT`: Wybiera liczbę wszystkich wierszy w przypadku gdy hello kolumny **t4** zawiera wartość hello **[Błąd]**.</span><span class="sxs-lookup"><span data-stu-id="6f504-209">`SELECT`: Selects a count of all rows where hello column **t4** contains hello value **[ERROR]**.</span></span> <span data-ttu-id="6f504-210">Ta instrukcja zwraca wartość **3** ponieważ istnieją trzy wiersze, które zawierają tę wartość.</span><span class="sxs-lookup"><span data-stu-id="6f504-210">This statement returns a value of **3** because there are three rows that contain this value.</span></span>

* <span data-ttu-id="6f504-211">`INPUT__FILE__NAME LIKE '%.log'`-Hive prób tooapply hello schematu tooall pliki w katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="6f504-211">`INPUT__FILE__NAME LIKE '%.log'` - Hive attempts tooapply hello schema tooall files in hello directory.</span></span> <span data-ttu-id="6f504-212">W takim przypadku hello katalog zawiera pliki, które nie są zgodne hello schematu.</span><span class="sxs-lookup"><span data-stu-id="6f504-212">In this case, hello directory contains files that do not match hello schema.</span></span> <span data-ttu-id="6f504-213">tooprevent odzyskiwanie danych w wynikach hello, niniejszych informuje Hive czy firma Microsoft powinno zwrócić dane tylko z plików w. dziennika.</span><span class="sxs-lookup"><span data-stu-id="6f504-213">tooprevent garbage data in hello results, this statement tells Hive that we should only return data from files ending in .log.</span></span>

> [!NOTE]
> <span data-ttu-id="6f504-214">Jeśli oczekujesz hello zaktualizowane przez źródło zewnętrzne podstawowej toobe danych należy użyć tabel zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="6f504-214">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="6f504-215">Na przykład procesu przekazywania danych lub operacja MapReduce.</span><span class="sxs-lookup"><span data-stu-id="6f504-215">For example, an automated data upload process, or MapReduce operation.</span></span>
>
> <span data-ttu-id="6f504-216">Usunięcie tabeli zewnętrznej jest **nie** usuwania danych hello usuwa tylko hello definicji tabeli.</span><span class="sxs-lookup"><span data-stu-id="6f504-216">Dropping an external table does **not** delete hello data, it only deletes hello table definition.</span></span>

<span data-ttu-id="6f504-217">toocreate **wewnętrzny** tabeli zamiast zewnętrznego, użyj następującego HiveQL hello:</span><span class="sxs-lookup"><span data-stu-id="6f504-217">toocreate an **internal** table instead of external, use hello following HiveQL:</span></span>

    set hive.execution.engine=tez;
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs
    SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';

<span data-ttu-id="6f504-218">Instrukcje te należy wykonać hello następujące akcje:</span><span class="sxs-lookup"><span data-stu-id="6f504-218">These statements perform hello following actions:</span></span>

* <span data-ttu-id="6f504-219">`CREATE TABLE IF NOT EXISTS`: Jeśli hello tabela nie istnieje, należy go utworzyć.</span><span class="sxs-lookup"><span data-stu-id="6f504-219">`CREATE TABLE IF NOT EXISTS`: If hello table does not exist, create it.</span></span> <span data-ttu-id="6f504-220">Ponieważ hello **zewnętrznych** — słowo kluczowe nie jest używany, ta instrukcja tworzy wewnętrznej tabeli.</span><span class="sxs-lookup"><span data-stu-id="6f504-220">Because hello **EXTERNAL** keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="6f504-221">Tabela Hello są przechowywane w magazynie danych Hive hello i zarządza całkowicie Hive.</span><span class="sxs-lookup"><span data-stu-id="6f504-221">hello table is stored in hello Hive data warehouse and is managed completely by Hive.</span></span>

* <span data-ttu-id="6f504-222">`STORED AS ORC`: Przechowuje dane hello w formacie zoptymalizowanych pod kątem wiersza kolumnowy (ORC).</span><span class="sxs-lookup"><span data-stu-id="6f504-222">`STORED AS ORC`: Stores hello data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="6f504-223">ORC jest wysoce zoptymalizowane i wydajne formatu do przechowywania danych gałęzi.</span><span class="sxs-lookup"><span data-stu-id="6f504-223">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

* <span data-ttu-id="6f504-224">`INSERT OVERWRITE ... SELECT`: Wybiera wiersze z hello **log4jLogs** tabeli, która zawiera **[Błąd]**, a następnie hello wstawia dane do hello **errorLogs** tabeli.</span><span class="sxs-lookup"><span data-stu-id="6f504-224">`INSERT OVERWRITE ... SELECT`: Selects rows from hello **log4jLogs** table that contains **[ERROR]**, and then inserts hello data into hello **errorLogs** table.</span></span>

> [!NOTE]
> <span data-ttu-id="6f504-225">W przeciwieństwie do tabel zewnętrznych porzucenie wewnętrznej tabeli spowoduje również usunięcie hello danych.</span><span class="sxs-lookup"><span data-stu-id="6f504-225">Unlike external tables, dropping an internal table also deletes hello underlying data.</span></span>

## <a name="improve-hive-query-performance"></a><span data-ttu-id="6f504-226">Poprawiać wydajność zapytań Hive</span><span class="sxs-lookup"><span data-stu-id="6f504-226">Improve Hive query performance</span></span>

### <span data-ttu-id="6f504-227"><a id="usetez"></a>Apache Tez</span><span class="sxs-lookup"><span data-stu-id="6f504-227"><a id="usetez"></a>Apache Tez</span></span>

<span data-ttu-id="6f504-228">[Apache Tez](http://tez.apache.org) to platforma, która umożliwia aplikacjom znacznym danych, takich jak Hive, toorun wydajniej na dużą skalę.</span><span class="sxs-lookup"><span data-stu-id="6f504-228">[Apache Tez](http://tez.apache.org) is a framework that allows data intensive applications, such as Hive, toorun much more efficiently at scale.</span></span> <span data-ttu-id="6f504-229">Tez jest domyślnie włączona dla klastrów usługi HDInsight opartych na systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="6f504-229">Tez is enabled by default for Linux-based HDInsight clusters.</span></span>

> [!NOTE]
> <span data-ttu-id="6f504-230">Tez jest obecnie domyślnie wyłączona w przypadku klastrów usługi HDInsight opartej na systemie Windows, a musi być włączona.</span><span class="sxs-lookup"><span data-stu-id="6f504-230">Tez is currently off by default for Windows-based HDInsight clusters and it must be enabled.</span></span> <span data-ttu-id="6f504-231">dla zapytania programu Hive, musi być ustawiona tootake zaletą aplikacji Tez, hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="6f504-231">tootake advantage of Tez, hello following value must be set for a Hive query:</span></span>
>
> `set hive.execution.engine=tez;`
>
> <span data-ttu-id="6f504-232">Tez jest hello domyślny aparat dla klastrów usługi HDInsight opartych na systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="6f504-232">Tez is hello default engine for Linux-based HDInsight clusters.</span></span>

<span data-ttu-id="6f504-233">Witaj [Hive w aplikacji Tez dokumentów projektowych](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez) zawiera szczegółowe informacje dotyczące opcji wdrażania hello i dostrajania konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="6f504-233">hello [Hive on Tez design documents](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez) contains details about hello implementation choices and tuning configurations.</span></span>

<span data-ttu-id="6f504-234">tooaid w debugowaniu zadań została uruchomiona przy użyciu aplikacji Tez, usługa HDInsight zapewnia powitania po web UI, umożliwiających tooview szczegóły Tez zadań:</span><span class="sxs-lookup"><span data-stu-id="6f504-234">tooaid in debugging jobs ran using Tez, HDInsight provides hello following web UIs that allow you tooview details of Tez jobs:</span></span>

* [<span data-ttu-id="6f504-235">Użyj hello widoku Ambari Tez w HDInsight opartych na systemie Linux</span><span class="sxs-lookup"><span data-stu-id="6f504-235">Use hello Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

* [<span data-ttu-id="6f504-236">Użyj hello Tez interfejsu użytkownika w usłudze HDInsight z systemu Windows</span><span class="sxs-lookup"><span data-stu-id="6f504-236">Use hello Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)

### <a name="low-latency-analytical-processing-llap"></a><span data-ttu-id="6f504-237">Małe opóźnienia przetwarzania analitycznego (LLAP)</span><span class="sxs-lookup"><span data-stu-id="6f504-237">Low Latency Analytical Processing (LLAP)</span></span>

<span data-ttu-id="6f504-238">[LLAP](https://cwiki.apache.org/confluence/display/Hive/LLAP) (czasami znana jako funkcja Live długich i procesów) to nowa funkcja w gałęzi 2.0, umożliwiającą buforowanie w pamięci zapytań.</span><span class="sxs-lookup"><span data-stu-id="6f504-238">[LLAP](https://cwiki.apache.org/confluence/display/Hive/LLAP) (sometimes known as Live Long and Process) is a new feature in Hive 2.0 that allows in-memory caching of queries.</span></span> <span data-ttu-id="6f504-239">LLAP sprawia, że zapytań programu Hive szybciej się zbyt[26 x szybciej niż Hive 1.x w niektórych przypadkach](https://hortonworks.com/blog/announcing-apache-hive-2-1-25x-faster-queries-much/).</span><span class="sxs-lookup"><span data-stu-id="6f504-239">LLAP makes Hive queries much faster, up too[26x faster than Hive 1.x in some cases](https://hortonworks.com/blog/announcing-apache-hive-2-1-25x-faster-queries-much/).</span></span>

<span data-ttu-id="6f504-240">Usługa HDInsight zapewnia LLAP w hello interakcyjne Hive typ klastra.</span><span class="sxs-lookup"><span data-stu-id="6f504-240">HDInsight provides LLAP in hello Interactive Hive cluster type.</span></span> <span data-ttu-id="6f504-241">Aby uzyskać więcej informacji, zobacz hello [rozpoczynać interakcyjne Hive](hdinsight-hadoop-use-interactive-hive.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="6f504-241">For more information, see hello [Start with Interactive Hive](hdinsight-hadoop-use-interactive-hive.md) document.</span></span>

## <a name="hive-jobs-and-sql-server-integration-services"></a><span data-ttu-id="6f504-242">Zadania hive i SQL Server Integration Services</span><span class="sxs-lookup"><span data-stu-id="6f504-242">Hive jobs and SQL Server Integration Services</span></span>

<span data-ttu-id="6f504-243">Możesz użyć programu SQL Server Integration Services (SSIS) toorun zadania Hive.</span><span class="sxs-lookup"><span data-stu-id="6f504-243">You can use SQL Server Integration Services (SSIS) toorun a Hive job.</span></span> <span data-ttu-id="6f504-244">Hello Azure Feature Pack do SSIS zapewnia hello następujące składniki, które współpracują z zadań Hive w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6f504-244">hello Azure Feature Pack for SSIS provides hello following components that work with Hive jobs on HDInsight.</span></span>

* <span data-ttu-id="6f504-245">[Zadania Azure HDInsight Hive][hivetask]</span><span class="sxs-lookup"><span data-stu-id="6f504-245">[Azure HDInsight Hive Task][hivetask]</span></span>

* <span data-ttu-id="6f504-246">[Menedżer połączeń subskrypcji platformy Azure][connectionmanager]</span><span class="sxs-lookup"><span data-stu-id="6f504-246">[Azure Subscription Connection Manager][connectionmanager]</span></span>

<span data-ttu-id="6f504-247">Dowiedz się więcej o hello Azure Feature Pack SSIS [tutaj][ssispack].</span><span class="sxs-lookup"><span data-stu-id="6f504-247">Learn more about hello Azure Feature Pack for SSIS [here][ssispack].</span></span>

## <span data-ttu-id="6f504-248"><a id="nextsteps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6f504-248"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="6f504-249">Teraz, kiedy znasz już gałąź jest i jak toouse go z platformą Hadoop w usłudze HDInsight, hello Użyj następujących łączy tooexplore toowork inne sposoby z usługą Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6f504-249">Now that you've learned what Hive is and how toouse it with Hadoop in HDInsight, use hello following links tooexplore other ways toowork with Azure HDInsight.</span></span>

* <span data-ttu-id="6f504-250">[Przekazywanie danych tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="6f504-250">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="6f504-251">[Korzystanie z języka Pig z usługą HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="6f504-251">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="6f504-252">[Korzystanie z zadań MapReduce z usługą HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="6f504-252">[Use MapReduce jobs with HDInsight][hdinsight-use-mapreduce]</span></span>

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/
[hivetask]: http://msdn.microsoft.com/library/mt146771(v=sql.120).aspx
[connectionmanager]: http://msdn.microsoft.com/library/mt146773(v=sql.120).aspx
[ssispack]: http://msdn.microsoft.com/library/mt146770(v=sql.120).aspx

[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md


[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx
