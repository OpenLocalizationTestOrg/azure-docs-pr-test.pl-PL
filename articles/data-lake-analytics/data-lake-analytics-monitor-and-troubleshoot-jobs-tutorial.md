---
title: "Rozwiązywanie problemów z zadania usługi Azure Data Lake Analytics przy użyciu portalu Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak rozwiązywać problemy z zadań usługi Data Lake Analytics przy użyciu portalu Azure. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: b7066d81-3142-474f-8a34-32b0b39656dc
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: b9c7453cc0a94f70d0098ed83e5f127832065a62
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-azure-data-lake-analytics-jobs-using-azure-portal"></a><span data-ttu-id="abd5e-103">Rozwiązywanie problemów z zadania usługi Azure Data Lake Analytics przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="abd5e-103">Troubleshoot Azure Data Lake Analytics jobs using Azure Portal</span></span>
<span data-ttu-id="abd5e-104">Dowiedz się, jak rozwiązywać problemy z zadań usługi Data Lake Analytics przy użyciu portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="abd5e-104">Learn how to use the Azure Portal to troubleshoot Data Lake Analytics jobs.</span></span>

<span data-ttu-id="abd5e-105">W tym samouczku będzie brak problem pliku źródłowego instalacji i za pomocą portalu Azure do rozwiązania problemu.</span><span class="sxs-lookup"><span data-stu-id="abd5e-105">In this tutorial, you will setup a missing source file problem, and use the Azure Portal to troubleshoot the problem.</span></span>

## <a name="submit-a-data-lake-analytics-job"></a><span data-ttu-id="abd5e-106">Przesyłanie zadania usługi Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="abd5e-106">Submit a Data Lake Analytics job</span></span>

<span data-ttu-id="abd5e-107">Prześlij zadanie U-SQL:</span><span class="sxs-lookup"><span data-stu-id="abd5e-107">Submit the following U-SQL job:</span></span>

```
@searchlog =
   EXTRACT UserId          int,
           Start           DateTime,
           Region          string,
           Query           string,
           Duration        int?,
           Urls            string,
           ClickedUrls     string
   FROM "/Samples/Data/SearchLog.tsv1"
   USING Extractors.Tsv();

OUTPUT @searchlog   
   TO "/output/SearchLog-from-adls.csv"
   USING Outputters.Csv();
```
    
<span data-ttu-id="abd5e-108">Plik źródłowy zdefiniowane w skrypcie jest **/Samples/Data/SearchLog.tsv1**, gdzie powinien być **/Samples/Data/SearchLog.tsv**.</span><span class="sxs-lookup"><span data-stu-id="abd5e-108">The source file defined in the script is **/Samples/Data/SearchLog.tsv1**, where it should be **/Samples/Data/SearchLog.tsv**.</span></span>


## <a name="troubleshoot-the-job"></a><span data-ttu-id="abd5e-109">Rozwiązywanie problemów z zadania</span><span class="sxs-lookup"><span data-stu-id="abd5e-109">Troubleshoot the job</span></span>

<span data-ttu-id="abd5e-110">**Aby wyświetlić wszystkie zadania**</span><span class="sxs-lookup"><span data-stu-id="abd5e-110">**To see all the jobs**</span></span>

1. <span data-ttu-id="abd5e-111">W portalu Azure kliknij **Microsoft Azure** w lewym górnym rogu.</span><span class="sxs-lookup"><span data-stu-id="abd5e-111">From the Azure portal, click **Microsoft Azure** in the upper left corner.</span></span>
2. <span data-ttu-id="abd5e-112">Kliknij kafelek z nazwą konta usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="abd5e-112">Click the tile with your Data Lake Analytics account name.</span></span>  <span data-ttu-id="abd5e-113">Zadanie podsumowania jest wyświetlany na **zadania zarządzania** kafelka.</span><span class="sxs-lookup"><span data-stu-id="abd5e-113">The job summary is shown on the **Job Management** tile.</span></span>

    ![Zarządzanie zadaniami usługi Azure Data Lake Analytics](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-job-management.png)

    <span data-ttu-id="abd5e-115">Zadania zarządzania zapewnia podstawowe informacje o stanie zadania.</span><span class="sxs-lookup"><span data-stu-id="abd5e-115">The job Management gives you a glance of the job status.</span></span> <span data-ttu-id="abd5e-116">Należy zauważyć, że zadania nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="abd5e-116">Notice there is a failed job.</span></span>
3. <span data-ttu-id="abd5e-117">Kliknij przycisk **zadania zarządzania** Kafelek, aby wyświetlić zadania.</span><span class="sxs-lookup"><span data-stu-id="abd5e-117">Click the **Job Management** tile to see the jobs.</span></span> <span data-ttu-id="abd5e-118">Zadania są podzielone na **systemem**, **w kolejce**, i **zakończone**.</span><span class="sxs-lookup"><span data-stu-id="abd5e-118">The jobs are categorized in **Running**, **Queued**, and **Ended**.</span></span> <span data-ttu-id="abd5e-119">Zostanie wyświetlona zadania nie powiodło się **zakończone** sekcji.</span><span class="sxs-lookup"><span data-stu-id="abd5e-119">You shall see your failed job in the **Ended** section.</span></span> <span data-ttu-id="abd5e-120">Jest ona pierwsza z nich na liście.</span><span class="sxs-lookup"><span data-stu-id="abd5e-120">It shall be first one in the list.</span></span> <span data-ttu-id="abd5e-121">Jeśli masz wiele zadań, można kliknąć **filtru** ułatwiające można znaleźć zadania.</span><span class="sxs-lookup"><span data-stu-id="abd5e-121">When you have a lot of jobs, you can click **Filter** to help you to locate jobs.</span></span>

    ![Usługa Azure Data Lake Analytics filtrowania zadań](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-filter-jobs.png)
4. <span data-ttu-id="abd5e-123">Kliknij zadanie zakończone niepowodzeniem z listy, aby otworzyć w nowym bloku szczegóły zadania:</span><span class="sxs-lookup"><span data-stu-id="abd5e-123">Click the failed job from the list to open the job details in a new blade:</span></span>

    ![Azure Data Lake Analytics zadania nie powiodło się](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job.png)

    <span data-ttu-id="abd5e-125">Powiadomienie **ponownie prześlij** przycisku.</span><span class="sxs-lookup"><span data-stu-id="abd5e-125">Notice the **Resubmit** button.</span></span> <span data-ttu-id="abd5e-126">Po rozwiązaniu problemu należy ponownie przesłać zadania.</span><span class="sxs-lookup"><span data-stu-id="abd5e-126">After you fix the problem, you can resubmit the job.</span></span>
5. <span data-ttu-id="abd5e-127">Kliknij część wyróżnione na poprzednim zrzucie ekranu, aby otworzyć szczegóły błędu.</span><span class="sxs-lookup"><span data-stu-id="abd5e-127">Click highlighted part from the previous screenshot to open the error details.</span></span>  <span data-ttu-id="abd5e-128">Zostanie wyświetlona wyglądać mniej więcej tak:</span><span class="sxs-lookup"><span data-stu-id="abd5e-128">You shall see something like:</span></span>

    ![Azure Data Lake Analytics szczegóły zadania nie powiodło się](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job-details.png)

    <span data-ttu-id="abd5e-130">Określa, że nie znaleziono folderu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="abd5e-130">It tells you the source folder is not found.</span></span>
6. <span data-ttu-id="abd5e-131">Kliknij przycisk **zduplikowane skryptu**.</span><span class="sxs-lookup"><span data-stu-id="abd5e-131">Click **Duplicate Script**.</span></span>
7. <span data-ttu-id="abd5e-132">Aktualizacja **FROM** ścieżka do następujących:</span><span class="sxs-lookup"><span data-stu-id="abd5e-132">Update the **FROM** path to the following:</span></span>

    <span data-ttu-id="abd5e-133">"/ Samples/Data/SearchLog.tsv"</span><span class="sxs-lookup"><span data-stu-id="abd5e-133">"/Samples/Data/SearchLog.tsv"</span></span>
8. <span data-ttu-id="abd5e-134">Kliknij przycisk **Prześlij zadanie**.</span><span class="sxs-lookup"><span data-stu-id="abd5e-134">Click **Submit Job**.</span></span>

## <a name="see-also"></a><span data-ttu-id="abd5e-135">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="abd5e-135">See also</span></span>
* [<span data-ttu-id="abd5e-136">Omówienie programu Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="abd5e-136">Azure Data Lake Analytics overview</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="abd5e-137">Wprowadzenie do usługi Azure Data Lake Analytics przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="abd5e-137">Get started with Azure Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="abd5e-138">Rozpoczynanie pracy z usługą Azure Data Lake Analytics i języka U-SQL przy użyciu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="abd5e-138">Get started with Azure Data Lake Analytics and U-SQL using Visual Studio</span></span>](data-lake-analytics-u-sql-get-started.md)
* [<span data-ttu-id="abd5e-139">Zarządzanie usługą Azure Data Lake Analytics przy użyciu witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="abd5e-139">Manage Azure Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-manage-use-portal.md)
