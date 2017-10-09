---
title: "aaaTroubleshoot zadania usługi Azure Data Lake Analytics przy użyciu portalu Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello zadania usługi Data Lake Analytics tootroubleshoot portalu Azure. "
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
ms.openlocfilehash: e810d56bab8f1a8254721ec9906bb6a4508dc22a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-data-lake-analytics-jobs-using-azure-portal"></a><span data-ttu-id="b704e-103">Rozwiązywanie problemów z zadania usługi Azure Data Lake Analytics przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="b704e-103">Troubleshoot Azure Data Lake Analytics jobs using Azure Portal</span></span>
<span data-ttu-id="b704e-104">Dowiedz się, jak toouse hello zadania usługi Data Lake Analytics tootroubleshoot portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b704e-104">Learn how toouse hello Azure Portal tootroubleshoot Data Lake Analytics jobs.</span></span>

<span data-ttu-id="b704e-105">W tym samouczku będzie skonfigurować Brak problem plik źródłowy i stosować problem hello tootroubleshoot hello w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b704e-105">In this tutorial, you will setup a missing source file problem, and use hello Azure Portal tootroubleshoot hello problem.</span></span>

## <a name="submit-a-data-lake-analytics-job"></a><span data-ttu-id="b704e-106">Przesyłanie zadania usługi Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="b704e-106">Submit a Data Lake Analytics job</span></span>

<span data-ttu-id="b704e-107">Prześlij hello następujące zadania skryptu U-SQL:</span><span class="sxs-lookup"><span data-stu-id="b704e-107">Submit hello following U-SQL job:</span></span>

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
   too"/output/SearchLog-from-adls.csv"
   USING Outputters.Csv();
```
    
<span data-ttu-id="b704e-108">Witaj plik źródłowy zdefiniowana w skrypcie hello jest **/Samples/Data/SearchLog.tsv1**, gdzie powinien być **/Samples/Data/SearchLog.tsv**.</span><span class="sxs-lookup"><span data-stu-id="b704e-108">hello source file defined in hello script is **/Samples/Data/SearchLog.tsv1**, where it should be **/Samples/Data/SearchLog.tsv**.</span></span>


## <a name="troubleshoot-hello-job"></a><span data-ttu-id="b704e-109">Rozwiązywanie problemów z hello zadania</span><span class="sxs-lookup"><span data-stu-id="b704e-109">Troubleshoot hello job</span></span>

<span data-ttu-id="b704e-110">**toosee hello wszystkich zadań**</span><span class="sxs-lookup"><span data-stu-id="b704e-110">**toosee all hello jobs**</span></span>

1. <span data-ttu-id="b704e-111">Witaj portalu Azure kliknij **Microsoft Azure** w lewym górnym rogu hello.</span><span class="sxs-lookup"><span data-stu-id="b704e-111">From hello Azure portal, click **Microsoft Azure** in hello upper left corner.</span></span>
2. <span data-ttu-id="b704e-112">Kliknij Kafelek hello nazwą konta usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="b704e-112">Click hello tile with your Data Lake Analytics account name.</span></span>  <span data-ttu-id="b704e-113">Witaj zadania podsumowania jest wyświetlany na powitania **zadania zarządzania** kafelka.</span><span class="sxs-lookup"><span data-stu-id="b704e-113">hello job summary is shown on hello **Job Management** tile.</span></span>

    ![Zarządzanie zadaniami usługi Azure Data Lake Analytics](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-job-management.png)

    <span data-ttu-id="b704e-115">Hello zadania zarządzania zapewnia podstawowe informacje o stanie zadania hello.</span><span class="sxs-lookup"><span data-stu-id="b704e-115">hello job Management gives you a glance of hello job status.</span></span> <span data-ttu-id="b704e-116">Należy zauważyć, że zadania nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="b704e-116">Notice there is a failed job.</span></span>
3. <span data-ttu-id="b704e-117">Kliknij przycisk hello **zadania zarządzania** kafelka toosee hello zadania.</span><span class="sxs-lookup"><span data-stu-id="b704e-117">Click hello **Job Management** tile toosee hello jobs.</span></span> <span data-ttu-id="b704e-118">Witaj zadania są podzielone na **systemem**, **w kolejce**, i **zakończone**.</span><span class="sxs-lookup"><span data-stu-id="b704e-118">hello jobs are categorized in **Running**, **Queued**, and **Ended**.</span></span> <span data-ttu-id="b704e-119">Zostanie wyświetlona nieudane zadania hello **zakończone** sekcji.</span><span class="sxs-lookup"><span data-stu-id="b704e-119">You shall see your failed job in hello **Ended** section.</span></span> <span data-ttu-id="b704e-120">Jest ona pierwszego hello na liście.</span><span class="sxs-lookup"><span data-stu-id="b704e-120">It shall be first one in hello list.</span></span> <span data-ttu-id="b704e-121">Jeśli masz wiele zadań, można kliknąć **filtru** toohelp można toolocate zadania.</span><span class="sxs-lookup"><span data-stu-id="b704e-121">When you have a lot of jobs, you can click **Filter** toohelp you toolocate jobs.</span></span>

    ![Usługa Azure Data Lake Analytics filtrowania zadań](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-filter-jobs.png)
4. <span data-ttu-id="b704e-123">Kliknij zadanie zakończone niepowodzeniem hello z hello listy tooopen hello szczegóły zadania w nowym bloku:</span><span class="sxs-lookup"><span data-stu-id="b704e-123">Click hello failed job from hello list tooopen hello job details in a new blade:</span></span>

    ![Azure Data Lake Analytics zadania nie powiodło się](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job.png)

    <span data-ttu-id="b704e-125">Powiadomienie hello **ponownie prześlij** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b704e-125">Notice hello **Resubmit** button.</span></span> <span data-ttu-id="b704e-126">Po rozwiązaniu problemu hello można przesłać ponownie hello zadania.</span><span class="sxs-lookup"><span data-stu-id="b704e-126">After you fix hello problem, you can resubmit hello job.</span></span>
5. <span data-ttu-id="b704e-127">Kliknij przycisk wyróżnione części z hello poprzedniej zrzut ekranu tooopen hello szczegóły błędu.</span><span class="sxs-lookup"><span data-stu-id="b704e-127">Click highlighted part from hello previous screenshot tooopen hello error details.</span></span>  <span data-ttu-id="b704e-128">Zostanie wyświetlona wyglądać mniej więcej tak:</span><span class="sxs-lookup"><span data-stu-id="b704e-128">You shall see something like:</span></span>

    ![Azure Data Lake Analytics szczegóły zadania nie powiodło się](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job-details.png)

    <span data-ttu-id="b704e-130">Określa się, że nie można odnaleźć folderu źródłowego hello.</span><span class="sxs-lookup"><span data-stu-id="b704e-130">It tells you hello source folder is not found.</span></span>
6. <span data-ttu-id="b704e-131">Kliknij przycisk **zduplikowane skryptu**.</span><span class="sxs-lookup"><span data-stu-id="b704e-131">Click **Duplicate Script**.</span></span>
7. <span data-ttu-id="b704e-132">Aktualizacja hello **FROM** ścieżka toohello poniżej:</span><span class="sxs-lookup"><span data-stu-id="b704e-132">Update hello **FROM** path toohello following:</span></span>

    <span data-ttu-id="b704e-133">"/ Samples/Data/SearchLog.tsv"</span><span class="sxs-lookup"><span data-stu-id="b704e-133">"/Samples/Data/SearchLog.tsv"</span></span>
8. <span data-ttu-id="b704e-134">Kliknij przycisk **Prześlij zadanie**.</span><span class="sxs-lookup"><span data-stu-id="b704e-134">Click **Submit Job**.</span></span>

## <a name="see-also"></a><span data-ttu-id="b704e-135">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="b704e-135">See also</span></span>
* [<span data-ttu-id="b704e-136">Omówienie programu Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="b704e-136">Azure Data Lake Analytics overview</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="b704e-137">Wprowadzenie do usługi Azure Data Lake Analytics przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b704e-137">Get started with Azure Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="b704e-138">Rozpoczynanie pracy z usługą Azure Data Lake Analytics i języka U-SQL przy użyciu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b704e-138">Get started with Azure Data Lake Analytics and U-SQL using Visual Studio</span></span>](data-lake-analytics-u-sql-get-started.md)
* [<span data-ttu-id="b704e-139">Zarządzanie usługą Azure Data Lake Analytics przy użyciu witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b704e-139">Manage Azure Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-manage-use-portal.md)
