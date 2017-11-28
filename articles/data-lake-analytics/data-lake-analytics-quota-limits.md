---
title: "Limity przydziału Analytics Lake danych aaaAzure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak ogranicza tooadjust i zwiększ limit przydziału konta usługi Azure Data Lake Analytics (ADLA)."
services: data-lake-analytics
keywords: Azure Data Lake Analytics
documentationcenter: 
author: omidm1
editor: omidm1
ms.assetid: 49416f38-fcc7-476f-a55e-d67f3f9c1d34
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: omidm
ms.openlocfilehash: 875c4d00e0c57414031e50754495c02162bdca48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-lake-analytics-quota-limits"></a><span data-ttu-id="c86e3-104">Limity przydziału usługi Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="c86e3-104">Azure Data Lake Analytics Quota Limits</span></span>

<span data-ttu-id="c86e3-105">Dowiedz się, jak ogranicza tooadjust i zwiększ limit przydziału konta usługi Azure Data Lake Analytics (ADLA).</span><span class="sxs-lookup"><span data-stu-id="c86e3-105">Learn how tooadjust and increase quota limits in Azure Data Lake Analytics (ADLA) accounts.</span></span> <span data-ttu-id="c86e3-106">Znajomość tych limitów mogą ułatwić zrozumienie zachowania zadania z języka U-SQL.</span><span class="sxs-lookup"><span data-stu-id="c86e3-106">Knowing these limits may help you understand your U-SQL job behavior.</span></span> <span data-ttu-id="c86e3-107">Wszystkie limity przydziału są miękkie, więc może zwiększyć maksymalną wartością hello dotarcie do toous.</span><span class="sxs-lookup"><span data-stu-id="c86e3-107">All quota limits are soft, so you can increase hello maximum limits by reaching out toous.</span></span>

## <a name="azure-subscriptions-limits"></a><span data-ttu-id="c86e3-108">Limity subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c86e3-108">Azure subscriptions limits</span></span>

<span data-ttu-id="c86e3-109">**Maksymalna liczba ADLA konta dla subskrypcji:** 5</span><span class="sxs-lookup"><span data-stu-id="c86e3-109">**Maximum number of ADLA accounts per subscription:**  5</span></span>

 <span data-ttu-id="c86e3-110">Jest to hello maksymalną liczbę kont ADLA, które można utworzyć na subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="c86e3-110">This is hello maximum number of ADLA accounts you can create per subscription.</span></span> <span data-ttu-id="c86e3-111">Jeśli spróbujesz konta ADLA toocreate szóstego, wystąpi błąd "Osiągnięto maksymalną liczbę kont usługi Data Lake Analytics może (5) hello w regionie, w obszarze Nazwa subskrypcji".</span><span class="sxs-lookup"><span data-stu-id="c86e3-111">If you try toocreate a sixth ADLA account, you will get an error "You have reached hello maximum number of Data Lake Analytics accounts allowed (5) in region under subscription name".</span></span> <span data-ttu-id="c86e3-112">W takim przypadku Usuń wszystkie nieużywane konta ADLA albo dotrzeć toous przez [otwarcie biletu pomocy technicznej](#increase-maximum-quota-limits).</span><span class="sxs-lookup"><span data-stu-id="c86e3-112">In this case, either delete any unused ADLA accounts, or reach out toous by [opening a support ticket](#increase-maximum-quota-limits).</span></span>

## <a name="adla-account-limits"></a><span data-ttu-id="c86e3-113">Limity konta ADLA</span><span class="sxs-lookup"><span data-stu-id="c86e3-113">ADLA account limits</span></span>

<span data-ttu-id="c86e3-114">**Maksymalna liczba jednostek Analytics (AUs) dla konta:** 250</span><span class="sxs-lookup"><span data-stu-id="c86e3-114">**Maximum number of Analytics Units (AUs) per account:** 250</span></span>

<span data-ttu-id="c86e3-115">Jest to hello maksymalną liczbę AUs, które można uruchomić jednocześnie w ramach Twojego konta.</span><span class="sxs-lookup"><span data-stu-id="c86e3-115">This is hello maximum number of AUs that can run concurrently in your account.</span></span> <span data-ttu-id="c86e3-116">Jeśli Twoja Suma uruchamianie AUs we wszystkich zadań przekracza ten limit, automatycznie są kolejkowane zadania nowsza.</span><span class="sxs-lookup"><span data-stu-id="c86e3-116">If your total running AUs across all jobs exceeds this limit, newer jobs are queued automatically.</span></span> <span data-ttu-id="c86e3-117">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="c86e3-117">For example:</span></span>

* <span data-ttu-id="c86e3-118">Jeśli masz tylko jedno zadanie uruchomione z 250 AUs, podczas przesyłania drugiej zadania go będzie czekać w kolejce zadań hello przed zakończeniem hello pierwszego zadania.</span><span class="sxs-lookup"><span data-stu-id="c86e3-118">If you have only one job running with 250 AUs, when you submit a second job it will wait in hello job queue until hello first job completes.</span></span>
* <span data-ttu-id="c86e3-119">Jeśli masz pięć zadania uruchomione i każdego używa 50 AUs, podczas przesyłania szóstego zadanie, które wymaga 20 AUs oczekuje w kolejce zadań hello, dopóki istnieją 20 AUs dostępne.</span><span class="sxs-lookup"><span data-stu-id="c86e3-119">If you already have five jobs running and each is using 50 AUs, when you submit a sixth job that needs 20 AUs it waits in hello job queue until there are 20 AUs available.</span></span>

<span data-ttu-id="c86e3-120">**Maksymalna liczba jednoczesnych zadań U-SQL dla danego konta:** 20</span><span class="sxs-lookup"><span data-stu-id="c86e3-120">**Maximum number of concurrent U-SQL jobs per account:** 20</span></span>

<span data-ttu-id="c86e3-121">Jest to hello maksymalna liczba zadań, które można uruchomić jednocześnie w ramach Twojego konta.</span><span class="sxs-lookup"><span data-stu-id="c86e3-121">This is hello maximum number of jobs that can run concurrently in your account.</span></span> <span data-ttu-id="c86e3-122">Powyżej tej wartości automatycznie są kolejkowane zadania nowsza.</span><span class="sxs-lookup"><span data-stu-id="c86e3-122">Above this value, newer jobs are queued automatically.</span></span>

## <a name="adjust-adla-quota-limits-per-account"></a><span data-ttu-id="c86e3-123">Dostosuj ADLA limity przydziału dla konta</span><span class="sxs-lookup"><span data-stu-id="c86e3-123">Adjust ADLA quota limits per account</span></span>

1. <span data-ttu-id="c86e3-124">Zaloguj się na toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c86e3-124">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c86e3-125">Wybierz istniejące konto ADLA.</span><span class="sxs-lookup"><span data-stu-id="c86e3-125">Choose an existing ADLA account.</span></span>
3. <span data-ttu-id="c86e3-126">Kliknij pozycję **Właściwości**.</span><span class="sxs-lookup"><span data-stu-id="c86e3-126">Click **Properties**.</span></span>
4. <span data-ttu-id="c86e3-127">Dostosuj **równoległości** i **równoczesnych zadań** toosuit potrzeb.</span><span class="sxs-lookup"><span data-stu-id="c86e3-127">Adjust **Parallelism** and **Concurrent Jobs** toosuit your needs.</span></span>

    ![Blok portalu usługi Azure Data Lake Analytics](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-properties.png)

## <a name="increase-maximum-quota-limits"></a><span data-ttu-id="c86e3-129">Zwiększ limit przydziału maksymalnej</span><span class="sxs-lookup"><span data-stu-id="c86e3-129">Increase maximum quota limits</span></span>

1. <span data-ttu-id="c86e3-130">W portalu Azure, otwórz żądanie pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="c86e3-130">Open a support request in Azure Portal.</span></span>

    ![Blok portalu usługi Azure Data Lake Analytics](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-help-support.png)

    ![Blok portalu usługi Azure Data Lake Analytics](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request.png)
2. <span data-ttu-id="c86e3-133">Wybierz typ problemu hello **przydziału**.</span><span class="sxs-lookup"><span data-stu-id="c86e3-133">Select hello issue type **Quota**.</span></span>
3. <span data-ttu-id="c86e3-134">Wybierz użytkownika **subskrypcji** (Upewnij się, nie jest "wersję próbną").</span><span class="sxs-lookup"><span data-stu-id="c86e3-134">Select your **Subscription** (make sure it is not a "trial" subscription).</span></span>
4. <span data-ttu-id="c86e3-135">Wybierz typ przydziału **usługi Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="c86e3-135">Select quota type **Data Lake Analytics**.</span></span>

    ![Blok portalu usługi Azure Data Lake Analytics](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-basics.png)

5. <span data-ttu-id="c86e3-137">W bloku hello problem opisano żądanego Zwiększ limit z **szczegóły** z czego potrzebujesz tej dodatkowej pojemności.</span><span class="sxs-lookup"><span data-stu-id="c86e3-137">In hello problem blade, explain your requested increase limit with **Details** of why you need this extra capacity.</span></span>

    ![Blok portalu usługi Azure Data Lake Analytics](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-details.png)

6. <span data-ttu-id="c86e3-139">Sprawdź informacje kontaktowe i Utwórz żądanie obsługi hello.</span><span class="sxs-lookup"><span data-stu-id="c86e3-139">Verify your contact information and create hello support request.</span></span>

<span data-ttu-id="c86e3-140">Firma Microsoft sprawdza żądania i próbuje tooaccommodate jak najszybciej potrzeb firmy.</span><span class="sxs-lookup"><span data-stu-id="c86e3-140">Microsoft reviews your request and tries tooaccommodate your business needs as soon as possible.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c86e3-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c86e3-141">Next steps</span></span>

* [<span data-ttu-id="c86e3-142">Omówienie usługi Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="c86e3-142">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="c86e3-143">Zarządzanie usługą Azure Data Lake Analytics przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c86e3-143">Manage Azure Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-manage-use-powershell.md)
* [<span data-ttu-id="c86e3-144">Monitorowanie zadań usługi Azure Data Lake Analytics i rozwiązywanie problemów przy użyciu witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c86e3-144">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
