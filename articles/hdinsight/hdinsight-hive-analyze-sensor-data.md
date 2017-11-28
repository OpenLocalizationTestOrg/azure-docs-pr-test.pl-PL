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
# <a name="analyze-sensor-data-using-hello-hive-query-console-on-hadoop-in-hdinsight"></a><span data-ttu-id="1e1a3-103">Analizowanie danych czujnika przy użyciu konsoli zapytania Hive hello na platformie Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="1e1a3-103">Analyze sensor data using hello Hive Query Console on Hadoop in HDInsight</span></span>

<span data-ttu-id="1e1a3-104">Dowiedz się, jak dane czujników tooanalyze przy użyciu hello Hive konsoli zapytania z usługą HDInsight (Hadoop), a następnie wizualizacji danych hello w programie Microsoft Excel za pomocą Power View.</span><span class="sxs-lookup"><span data-stu-id="1e1a3-104">Learn how tooanalyze sensor data by using hello Hive Query Console with HDInsight (Hadoop), then visualize hello data in Microsoft Excel by using Power View.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1e1a3-105">Witaj czynnościach w ramach tego dokumentu działać tylko w przypadku klastrów usługi HDInsight opartych na systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="1e1a3-105">hello steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="1e1a3-106">HDInsight jest dostępna tylko w systemie Windows dla wersji starszej niż HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="1e1a3-106">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="1e1a3-107">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="1e1a3-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="1e1a3-108">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="1e1a3-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>


<span data-ttu-id="1e1a3-109">W tym przykładzie używamy danych historycznych tooprocess Hive i zidentyfikować problemy z systemami grzejników i klimatyzacja.</span><span class="sxs-lookup"><span data-stu-id="1e1a3-109">In this sample, you use Hive tooprocess historical data and identify problems with heating and air conditioning systems.</span></span> <span data-ttu-id="1e1a3-110">W szczególności zidentyfikować systemy są tooreliably nie jest w stanie utrzymać stałej temperatury, wykonując następujące zadania hello:</span><span class="sxs-lookup"><span data-stu-id="1e1a3-110">Specifically, you identify systems are not able tooreliably maintain a set temperature by performing hello following tasks:</span></span>

* <span data-ttu-id="1e1a3-111">Utwórz gałąź Tabele tooquery dane przechowywane w plikach plik wartości rozdzielanych przecinkami (CSV).</span><span class="sxs-lookup"><span data-stu-id="1e1a3-111">Create HIVE tables tooquery data stored in comma-separated value (CSV) files.</span></span>
* <span data-ttu-id="1e1a3-112">Tworzenie zapytań programu HIVE tooanalyze hello danych.</span><span class="sxs-lookup"><span data-stu-id="1e1a3-112">Create HIVE queries tooanalyze hello data.</span></span>
* <span data-ttu-id="1e1a3-113">tooretrieve hello analizy danych, użyj tooHDInsight tooconnect programu Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="1e1a3-113">tooretrieve hello analyzed data, use Microsoft Excel tooconnect tooHDInsight.</span></span>
* <span data-ttu-id="1e1a3-114">toovisualize hello danych, użyj Power View.</span><span class="sxs-lookup"><span data-stu-id="1e1a3-114">toovisualize hello data, use Power View.</span></span>

![Diagram architektury rozwiązania hello](./media/hdinsight-hive-analyze-sensor-data/hvac-architecture.png)

## <a name="prerequisites"></a><span data-ttu-id="1e1a3-116">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1e1a3-116">Prerequisites</span></span>

* <span data-ttu-id="1e1a3-117">Klaster usługi HDInsight (Hadoop): zobacz [klastrów utworzyć Hadoop w usłudze HDInsight](hdinsight-hadoop-provision-linux-clusters.md) informacji o tworzeniu klastra.</span><span class="sxs-lookup"><span data-stu-id="1e1a3-117">An HDInsight (Hadoop) cluster: See [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md) for information about creating a cluster.</span></span>
* <span data-ttu-id="1e1a3-118">Programu Microsoft Excel 2013</span><span class="sxs-lookup"><span data-stu-id="1e1a3-118">Microsoft Excel 2013</span></span>

  > [!NOTE]
  > <span data-ttu-id="1e1a3-119">Program Microsoft Excel jest używana do wizualizacji danych z [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US).</span><span class="sxs-lookup"><span data-stu-id="1e1a3-119">Microsoft Excel is used for data visualization with [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US).</span></span>

* [<span data-ttu-id="1e1a3-120">Sterownik ODBC firmy Microsoft Hive</span><span class="sxs-lookup"><span data-stu-id="1e1a3-120">Microsoft Hive ODBC Driver</span></span>](http://www.microsoft.com/download/details.aspx?id=40886)

## <a name="toorun-hello-sample"></a><span data-ttu-id="1e1a3-121">przykład Witaj toorun</span><span class="sxs-lookup"><span data-stu-id="1e1a3-121">toorun hello sample</span></span>

1. <span data-ttu-id="1e1a3-122">W przeglądarce sieci web przejdź toohello następującego adresu URL:</span><span class="sxs-lookup"><span data-stu-id="1e1a3-122">From your web browser, navigate toohello following URL:</span></span> 

         https://<clustername>.azurehdinsight.net

    <span data-ttu-id="1e1a3-123">Zastąp `<clustername>` o nazwie hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1e1a3-123">Replace `<clustername>` with hello name of your HDInsight cluster.</span></span>

    <span data-ttu-id="1e1a3-124">Po wyświetleniu monitu uwierzytelniania przy użyciu nazwy użytkownika administratora hello i hasło użyte podczas inicjowania obsługi administracyjnej tego klastra.</span><span class="sxs-lookup"><span data-stu-id="1e1a3-124">When prompted, authenticate by using hello administrator user name and password you used when provisioning this cluster.</span></span>

2. <span data-ttu-id="1e1a3-125">Z hello strony sieci web, który zostanie otwarty, kliknij przycisk hello **Getting Started galerii** kartę, a następnie w obszarze hello **rozwiązań z przykładowymi danymi** kategorii, kliknij hello **analizy danych czujnika** przykład.</span><span class="sxs-lookup"><span data-stu-id="1e1a3-125">From hello web page that opens, click hello **Getting Started Gallery** tab, and then under hello **Solutions with Sample Data** category, click hello **Sensor Data Analysis** sample.</span></span>

    ![Pobieranie rozpoczęte galerii](./media/hdinsight-hive-analyze-sensor-data/getting-started-gallery.png)

3. <span data-ttu-id="1e1a3-127">Postępuj zgodnie z instrukcjami hello hello strony sieci web toofinish hello próbki.</span><span class="sxs-lookup"><span data-stu-id="1e1a3-127">Follow hello instructions provided on hello web page toofinish hello sample.</span></span>
