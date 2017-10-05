---
title: "Analizowanie danych czujnika przy użyciu Hive i Hadoop - Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak i analizowanie danych czujnika przy użyciu konsoli zapytania programu Hive z usługą HDInsight (Hadoop), a następnie wizualizacji danych w programie Microsoft Excel z PowerView."
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
ms.openlocfilehash: 3abb71c12b4769bebd808276f8bdd832aad22d7a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-sensor-data-using-the-hive-query-console-on-hadoop-in-hdinsight"></a><span data-ttu-id="af8b7-103">Analizowanie danych czujnika przy użyciu konsoli zapytania Hive na platformie Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="af8b7-103">Analyze sensor data using the Hive Query Console on Hadoop in HDInsight</span></span>

<span data-ttu-id="af8b7-104">Dowiedz się, jak i analizowanie danych czujnika przy użyciu konsoli zapytania programu Hive z usługą HDInsight (Hadoop), a następnie wizualizacji danych w programie Microsoft Excel za pomocą Power View.</span><span class="sxs-lookup"><span data-stu-id="af8b7-104">Learn how to analyze sensor data by using the Hive Query Console with HDInsight (Hadoop), then visualize the data in Microsoft Excel by using Power View.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="af8b7-105">Kroki opisane w tym dokumencie pracować tylko z klastrami HDInsight opartych na systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="af8b7-105">The steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="af8b7-106">HDInsight jest dostępna tylko w systemie Windows dla wersji starszej niż HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="af8b7-106">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="af8b7-107">Linux jest jedynym systemem operacyjnym używanym w połączeniu z usługą HDInsight w wersji 3.4 lub nowszą.</span><span class="sxs-lookup"><span data-stu-id="af8b7-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="af8b7-108">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="af8b7-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>


<span data-ttu-id="af8b7-109">W tym przykładzie służy do przetwarzania danych historycznych i zidentyfikować problemy z systemami grzejników i klimatyzacja Hive.</span><span class="sxs-lookup"><span data-stu-id="af8b7-109">In this sample, you use Hive to process historical data and identify problems with heating and air conditioning systems.</span></span> <span data-ttu-id="af8b7-110">W szczególności zidentyfikować systemy nie będą mogli w sposób niezawodny utrzymać stałej temperatury przy wykonywaniu następujących zadań:</span><span class="sxs-lookup"><span data-stu-id="af8b7-110">Specifically, you identify systems are not able to reliably maintain a set temperature by performing the following tasks:</span></span>

* <span data-ttu-id="af8b7-111">Tworzenie tabel programu HIVE wykonać zapytania o dane przechowywane w plikach plik wartości rozdzielanych przecinkami (CSV).</span><span class="sxs-lookup"><span data-stu-id="af8b7-111">Create HIVE tables to query data stored in comma-separated value (CSV) files.</span></span>
* <span data-ttu-id="af8b7-112">Tworzenie zapytań HIVE do analizowania danych.</span><span class="sxs-lookup"><span data-stu-id="af8b7-112">Create HIVE queries to analyze the data.</span></span>
* <span data-ttu-id="af8b7-113">Aby pobrać analizowanych danych, należy użyć programu Microsoft Excel do nawiązania połączenia usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="af8b7-113">To retrieve the analyzed data, use Microsoft Excel to connect to HDInsight.</span></span>
* <span data-ttu-id="af8b7-114">W celu wizualizacji danych, użyj Power View.</span><span class="sxs-lookup"><span data-stu-id="af8b7-114">To visualize the data, use Power View.</span></span>

![Diagram architektury rozwiązania](./media/hdinsight-hive-analyze-sensor-data/hvac-architecture.png)

## <a name="prerequisites"></a><span data-ttu-id="af8b7-116">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="af8b7-116">Prerequisites</span></span>

* <span data-ttu-id="af8b7-117">Klaster usługi HDInsight (Hadoop): zobacz [klastrów utworzyć Hadoop w usłudze HDInsight](hdinsight-hadoop-provision-linux-clusters.md) informacji o tworzeniu klastra.</span><span class="sxs-lookup"><span data-stu-id="af8b7-117">An HDInsight (Hadoop) cluster: See [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md) for information about creating a cluster.</span></span>
* <span data-ttu-id="af8b7-118">Programu Microsoft Excel 2013</span><span class="sxs-lookup"><span data-stu-id="af8b7-118">Microsoft Excel 2013</span></span>

  > [!NOTE]
  > <span data-ttu-id="af8b7-119">Program Microsoft Excel jest używana do wizualizacji danych z [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US).</span><span class="sxs-lookup"><span data-stu-id="af8b7-119">Microsoft Excel is used for data visualization with [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US).</span></span>

* [<span data-ttu-id="af8b7-120">Sterownik ODBC firmy Microsoft Hive</span><span class="sxs-lookup"><span data-stu-id="af8b7-120">Microsoft Hive ODBC Driver</span></span>](http://www.microsoft.com/download/details.aspx?id=40886)

## <a name="to-run-the-sample"></a><span data-ttu-id="af8b7-121">Aby uruchomić przykładowy</span><span class="sxs-lookup"><span data-stu-id="af8b7-121">To run the sample</span></span>

1. <span data-ttu-id="af8b7-122">W przeglądarce sieci web przejdź do następującego adresu URL:</span><span class="sxs-lookup"><span data-stu-id="af8b7-122">From your web browser, navigate to the following URL:</span></span> 

         https://<clustername>.azurehdinsight.net

    <span data-ttu-id="af8b7-123">Element `<clustername>` należy zastąpić nazwą klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="af8b7-123">Replace `<clustername>` with the name of your HDInsight cluster.</span></span>

    <span data-ttu-id="af8b7-124">Po wyświetleniu monitu uwierzytelniania przy użyciu nazwy użytkownika administratora i hasło użyte podczas inicjowania obsługi administracyjnej tego klastra.</span><span class="sxs-lookup"><span data-stu-id="af8b7-124">When prompted, authenticate by using the administrator user name and password you used when provisioning this cluster.</span></span>

2. <span data-ttu-id="af8b7-125">Na stronie sieci web, który zostanie otwarty, kliknij **Getting Started galerii** kartę, a następnie w obszarze **rozwiązań z przykładowymi danymi** kategorii, kliknij przycisk **analizy danych czujnika** próbki.</span><span class="sxs-lookup"><span data-stu-id="af8b7-125">From the web page that opens, click the **Getting Started Gallery** tab, and then under the **Solutions with Sample Data** category, click the **Sensor Data Analysis** sample.</span></span>

    ![Pobieranie rozpoczęte galerii](./media/hdinsight-hive-analyze-sensor-data/getting-started-gallery.png)

3. <span data-ttu-id="af8b7-127">Postępuj zgodnie z instrukcjami na stronie sieci web zakończenie próbki.</span><span class="sxs-lookup"><span data-stu-id="af8b7-127">Follow the instructions provided on the web page to finish the sample.</span></span>
