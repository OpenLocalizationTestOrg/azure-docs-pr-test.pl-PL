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
# <a name="use-hive-with-windows-based-hdinsight-tooanalyze-logs-from-websites"></a><span data-ttu-id="d8f25-104">Korzystanie z programu Hive z HDInsight opartych na systemie Windows tooanalyze dzienników witryn sieci Web</span><span class="sxs-lookup"><span data-stu-id="d8f25-104">Use Hive with Windows-based HDInsight tooanalyze logs from websites</span></span>
<span data-ttu-id="d8f25-105">Dowiedz się, jak rejestruje toouse HiveQL z HDInsight tooanalyze z witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="d8f25-105">Learn how toouse HiveQL with HDInsight tooanalyze logs from a website.</span></span> <span data-ttu-id="d8f25-106">Analiza dziennika witryny sieci Web może być używane toosegment odbiorców w oparciu podobne działania, kategoryzowanie odwiedzający demograficznymi i toofind hello zawartość, którą mogą wyświetlać, hello witryn sieci Web, które pochodzą z i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="d8f25-106">Website log analysis can be used toosegment your audience based on similar activities, categorize site visitors by demographics, and toofind out hello content they view, hello websites they come from, and so on.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d8f25-107">Witaj czynnościach w ramach tego dokumentu działać tylko w przypadku klastrów usługi HDInsight opartych na systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="d8f25-107">hello steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="d8f25-108">HDInsight jest dostępna tylko w systemie Windows dla wersji starszej niż HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="d8f25-108">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="d8f25-109">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="d8f25-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d8f25-110">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="d8f25-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="d8f25-111">W tym przykładzie użyjesz HDInsight klastra tooanalyze witryny sieci Web dziennika pliki tooget wgląd częstotliwość hello wizyt toohello witryny sieci Web z zewnętrznymi witrynami sieci Web w ciągu jednego dnia.</span><span class="sxs-lookup"><span data-stu-id="d8f25-111">In this sample, you will use an HDInsight cluster tooanalyze website log files tooget insight into hello frequency of visits toohello website from external websites in a day.</span></span> <span data-ttu-id="d8f25-112">Zostanie również wygenerowany podsumowanie błędów witryny sieci Web, które użytkownicy hello napotkać.</span><span class="sxs-lookup"><span data-stu-id="d8f25-112">You'll also generate a summary of website errors that hello users experience.</span></span> <span data-ttu-id="d8f25-113">Dowiesz się jak:</span><span class="sxs-lookup"><span data-stu-id="d8f25-113">You will learn how to:</span></span>

* <span data-ttu-id="d8f25-114">Połącz tooa magazynu obiektów Blob platformy Azure, który zawiera pliki dziennika witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="d8f25-114">Connect tooa Azure Blob storage, which contains website log files.</span></span>
* <span data-ttu-id="d8f25-115">Utwórz gałąź Tabele tooquery tych dzienników.</span><span class="sxs-lookup"><span data-stu-id="d8f25-115">Create HIVE tables tooquery those logs.</span></span>
* <span data-ttu-id="d8f25-116">Tworzenie zapytań programu HIVE tooanalyze hello danych.</span><span class="sxs-lookup"><span data-stu-id="d8f25-116">Create HIVE queries tooanalyze hello data.</span></span>
* <span data-ttu-id="d8f25-117">Użyj programu Microsoft Excel tooconnect tooHDInsight (przy użyciu bazy danych otwórz łączności (ODBC) tooretrieve hello analizy danych.</span><span class="sxs-lookup"><span data-stu-id="d8f25-117">Use Microsoft Excel tooconnect tooHDInsight (by using open database connectivity (ODBC) tooretrieve hello analyzed data.</span></span>

![HDI. Samples.Website.Log.Analysis][img-hdi-weblogs-sample]

## <a name="prerequisites"></a><span data-ttu-id="d8f25-119">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d8f25-119">Prerequisites</span></span>
* <span data-ttu-id="d8f25-120">Musi mieć zainicjowana klastra usługi Hadoop w usłudze Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d8f25-120">You must have provisioned a Hadoop cluster on Azure HDInsight.</span></span> <span data-ttu-id="d8f25-121">Aby uzyskać instrukcje, zobacz [klastrów usługi HDInsight udostępniania][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="d8f25-121">For instructions, see [Provision HDInsight Clusters][hdinsight-provision].</span></span>
* <span data-ttu-id="d8f25-122">Musi mieć programu Microsoft Excel 2013 lub zainstalowany program Excel 2010.</span><span class="sxs-lookup"><span data-stu-id="d8f25-122">You must have Microsoft Excel 2013 or Excel 2010 installed.</span></span>
* <span data-ttu-id="d8f25-123">Musi mieć [sterownik Microsoft Hive ODBC](http://www.microsoft.com/download/details.aspx?id=40886) tooimport danych z gałęzi do programu Excel.</span><span class="sxs-lookup"><span data-stu-id="d8f25-123">You must have [Microsoft Hive ODBC Driver](http://www.microsoft.com/download/details.aspx?id=40886) tooimport data from Hive into Excel.</span></span>

## <a name="toorun-hello-sample"></a><span data-ttu-id="d8f25-124">przykład Witaj toorun</span><span class="sxs-lookup"><span data-stu-id="d8f25-124">toorun hello sample</span></span>
1. <span data-ttu-id="d8f25-125">Z hello [Azure Portal](https://portal.azure.com/), hello tablicy startowej (jeśli został przypięty klastra hello istnieje), kliknij hello kafelka klastra, na którym ma zostać toorun hello próbki.</span><span class="sxs-lookup"><span data-stu-id="d8f25-125">From hello [Azure Portal](https://portal.azure.com/), from hello Startboard (if you pinned hello cluster there), click hello cluster tile on which you want toorun hello sample.</span></span>
2. <span data-ttu-id="d8f25-126">Z hello klastra bloku, w obszarze **szybkie linki**, kliknij przycisk **pulpit nawigacyjny klastra**, a następnie z hello **pulpit nawigacyjny klastra** bloku, kliknij przycisk **klastra usługi HDInsight Pulpit nawigacyjny**.</span><span class="sxs-lookup"><span data-stu-id="d8f25-126">From hello cluster blade, under **Quick Links**, click **Cluster Dashboard**, and then from hello **Cluster Dashboard** blade, click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="d8f25-127">Pulpit nawigacyjny hello można również otworzyć bezpośrednio za pomocą hello następującego adresu URL:</span><span class="sxs-lookup"><span data-stu-id="d8f25-127">Alternatively, you can directly open hello dashboard by using hello following URL:</span></span>

         https://<clustername>.azurehdinsight.net

    <span data-ttu-id="d8f25-128">Po wyświetleniu monitu uwierzytelniania przy użyciu nazwy użytkownika administratora hello i hasło, które zostały użyte podczas inicjowania obsługi klastra hello.</span><span class="sxs-lookup"><span data-stu-id="d8f25-128">When prompted, authenticate by using hello administrator user name and password you used when provisioning hello cluster.</span></span>
3. <span data-ttu-id="d8f25-129">Z hello strony sieci web, który zostanie otwarty, kliknij przycisk hello **Getting Started galerii** kartę, a następnie w obszarze hello **rozwiązań z przykładowymi danymi** kategorii, kliknij hello **analiza dziennika witryny sieci Web** przykład.</span><span class="sxs-lookup"><span data-stu-id="d8f25-129">From hello web page that opens, click hello **Getting Started Gallery** tab, and then under hello **Solutions with Sample Data** category, click hello **Website Log Analysis** sample.</span></span>
4. <span data-ttu-id="d8f25-130">Postępuj zgodnie z instrukcjami hello hello strony sieci web toofinish hello próbki.</span><span class="sxs-lookup"><span data-stu-id="d8f25-130">Follow hello instructions provided on hello web page toofinish hello sample.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d8f25-131">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d8f25-131">Next steps</span></span>
<span data-ttu-id="d8f25-132">Spróbuj hello następujące przykładowe: [analizowanie danych czujnika przy użyciu Hive z usługą HDInsight](hdinsight-hive-analyze-sensor-data.md).</span><span class="sxs-lookup"><span data-stu-id="d8f25-132">Try hello following sample: [Analyzing sensor data using Hive with HDInsight](hdinsight-hive-analyze-sensor-data.md).</span></span>

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-sensor-data-sample]: ../hdinsight-use-hive-sensor-data-analysis.md

[img-hdi-weblogs-sample]: ./media/hdinsight-hive-analyze-website-log/hdinsight-weblogs-sample.png
