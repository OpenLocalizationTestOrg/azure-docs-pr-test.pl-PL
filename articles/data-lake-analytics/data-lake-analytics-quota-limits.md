---
title: "Limity przydziału usługi Azure Data Lake Analytics | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak dostosować i zwiększyć limity przydziału na kontach usługi Azure Data Lake Analytics (ADLA)."
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
ms.openlocfilehash: 957f306ea0e80b5830ad64e5ef06c6d122d9eccc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-data-lake-analytics-quota-limits"></a><span data-ttu-id="976ce-104">Limity przydziału usługi Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="976ce-104">Azure Data Lake Analytics Quota Limits</span></span>

<span data-ttu-id="976ce-105">Dowiedz się, jak dostosować i zwiększyć limity przydziału na kontach usługi Azure Data Lake Analytics (ADLA).</span><span class="sxs-lookup"><span data-stu-id="976ce-105">Learn how to adjust and increase quota limits in Azure Data Lake Analytics (ADLA) accounts.</span></span> <span data-ttu-id="976ce-106">Znajomość tych limitów mogą ułatwić zrozumienie zachowania zadania z języka U-SQL.</span><span class="sxs-lookup"><span data-stu-id="976ce-106">Knowing these limits may help you understand your U-SQL job behavior.</span></span> <span data-ttu-id="976ce-107">Wszystkie limity przydziału są miękkie, więc może zwiększyć maksymalną wartością dotarcie z nami.</span><span class="sxs-lookup"><span data-stu-id="976ce-107">All quota limits are soft, so you can increase the maximum limits by reaching out to us.</span></span>

## <a name="azure-subscriptions-limits"></a><span data-ttu-id="976ce-108">Limity subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="976ce-108">Azure subscriptions limits</span></span>

<span data-ttu-id="976ce-109">**Maksymalna liczba ADLA konta dla subskrypcji:** 5</span><span class="sxs-lookup"><span data-stu-id="976ce-109">**Maximum number of ADLA accounts per subscription:**  5</span></span>

 <span data-ttu-id="976ce-110">Jest to maksymalna liczba kont ADLA, które można utworzyć na subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="976ce-110">This is the maximum number of ADLA accounts you can create per subscription.</span></span> <span data-ttu-id="976ce-111">Jeśli próbujesz utworzyć konto ADLA szóstego, wystąpi błąd "Osiągnięto maksymalną liczbę kont usługi Data Lake Analytics może (5) w regionie, w obszarze Nazwa subskrypcji".</span><span class="sxs-lookup"><span data-stu-id="976ce-111">If you try to create a sixth ADLA account, you will get an error "You have reached the maximum number of Data Lake Analytics accounts allowed (5) in region under subscription name".</span></span> <span data-ttu-id="976ce-112">W takim przypadku Usuń wszystkie nieużywane konta ADLA albo dotrzeć do nas przez [otwarcie biletu pomocy technicznej](#increase-maximum-quota-limits).</span><span class="sxs-lookup"><span data-stu-id="976ce-112">In this case, either delete any unused ADLA accounts, or reach out to us by [opening a support ticket](#increase-maximum-quota-limits).</span></span>

## <a name="adla-account-limits"></a><span data-ttu-id="976ce-113">Limity konta ADLA</span><span class="sxs-lookup"><span data-stu-id="976ce-113">ADLA account limits</span></span>

<span data-ttu-id="976ce-114">**Maksymalna liczba jednostek Analytics (AUs) dla konta:** 250</span><span class="sxs-lookup"><span data-stu-id="976ce-114">**Maximum number of Analytics Units (AUs) per account:** 250</span></span>

<span data-ttu-id="976ce-115">Jest to maksymalna liczba AUs, które można uruchomić jednocześnie w ramach Twojego konta.</span><span class="sxs-lookup"><span data-stu-id="976ce-115">This is the maximum number of AUs that can run concurrently in your account.</span></span> <span data-ttu-id="976ce-116">Jeśli Twoja Suma uruchamianie AUs we wszystkich zadań przekracza ten limit, automatycznie są kolejkowane zadania nowsza.</span><span class="sxs-lookup"><span data-stu-id="976ce-116">If your total running AUs across all jobs exceeds this limit, newer jobs are queued automatically.</span></span> <span data-ttu-id="976ce-117">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="976ce-117">For example:</span></span>

* <span data-ttu-id="976ce-118">Jeśli masz tylko jedno zadanie uruchomione z 250 AUs, podczas przesyłania drugiej zadania go będzie czekać w kolejce zadań dopiero po zakończeniu pierwszego zadania.</span><span class="sxs-lookup"><span data-stu-id="976ce-118">If you have only one job running with 250 AUs, when you submit a second job it will wait in the job queue until the first job completes.</span></span>
* <span data-ttu-id="976ce-119">Jeśli masz pięć zadania uruchomione i każdego używa 50 AUs, podczas przesyłania szóstego zadanie, które wymaga 20 AUs oczekuje w kolejce zadań, dopóki istnieją 20 AUs dostępne.</span><span class="sxs-lookup"><span data-stu-id="976ce-119">If you already have five jobs running and each is using 50 AUs, when you submit a sixth job that needs 20 AUs it waits in the job queue until there are 20 AUs available.</span></span>

<span data-ttu-id="976ce-120">**Maksymalna liczba jednoczesnych zadań U-SQL dla danego konta:** 20</span><span class="sxs-lookup"><span data-stu-id="976ce-120">**Maximum number of concurrent U-SQL jobs per account:** 20</span></span>

<span data-ttu-id="976ce-121">Jest to maksymalna liczba zadań, które można uruchomić jednocześnie w ramach Twojego konta.</span><span class="sxs-lookup"><span data-stu-id="976ce-121">This is the maximum number of jobs that can run concurrently in your account.</span></span> <span data-ttu-id="976ce-122">Powyżej tej wartości automatycznie są kolejkowane zadania nowsza.</span><span class="sxs-lookup"><span data-stu-id="976ce-122">Above this value, newer jobs are queued automatically.</span></span>

## <a name="adjust-adla-quota-limits-per-account"></a><span data-ttu-id="976ce-123">Dostosuj ADLA limity przydziału dla konta</span><span class="sxs-lookup"><span data-stu-id="976ce-123">Adjust ADLA quota limits per account</span></span>

1. <span data-ttu-id="976ce-124">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="976ce-124">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="976ce-125">Wybierz istniejące konto ADLA.</span><span class="sxs-lookup"><span data-stu-id="976ce-125">Choose an existing ADLA account.</span></span>
3. <span data-ttu-id="976ce-126">Kliknij pozycję **Właściwości**.</span><span class="sxs-lookup"><span data-stu-id="976ce-126">Click **Properties**.</span></span>
4. <span data-ttu-id="976ce-127">Dostosuj **równoległości** i **równoczesnych zadań** w zależności od potrzeb.</span><span class="sxs-lookup"><span data-stu-id="976ce-127">Adjust **Parallelism** and **Concurrent Jobs** to suit your needs.</span></span>

    ![Blok portalu usługi Azure Data Lake Analytics](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-properties.png)

## <a name="increase-maximum-quota-limits"></a><span data-ttu-id="976ce-129">Zwiększ limit przydziału maksymalnej</span><span class="sxs-lookup"><span data-stu-id="976ce-129">Increase maximum quota limits</span></span>

1. <span data-ttu-id="976ce-130">W portalu Azure, otwórz żądanie pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="976ce-130">Open a support request in Azure Portal.</span></span>

    ![Blok portalu usługi Azure Data Lake Analytics](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-help-support.png)

    ![Blok portalu usługi Azure Data Lake Analytics](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request.png)
2. <span data-ttu-id="976ce-133">Wybierz typ problemu **przydziału**.</span><span class="sxs-lookup"><span data-stu-id="976ce-133">Select the issue type **Quota**.</span></span>
3. <span data-ttu-id="976ce-134">Wybierz użytkownika **subskrypcji** (Upewnij się, nie jest "wersję próbną").</span><span class="sxs-lookup"><span data-stu-id="976ce-134">Select your **Subscription** (make sure it is not a "trial" subscription).</span></span>
4. <span data-ttu-id="976ce-135">Wybierz typ przydziału **usługi Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="976ce-135">Select quota type **Data Lake Analytics**.</span></span>

    ![Blok portalu usługi Azure Data Lake Analytics](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-basics.png)

5. <span data-ttu-id="976ce-137">W bloku problem opisano żądanego Zwiększ limit z **szczegóły** z czego potrzebujesz tej dodatkowej pojemności.</span><span class="sxs-lookup"><span data-stu-id="976ce-137">In the problem blade, explain your requested increase limit with **Details** of why you need this extra capacity.</span></span>

    ![Blok portalu usługi Azure Data Lake Analytics](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-details.png)

6. <span data-ttu-id="976ce-139">Sprawdź informacje kontaktowe i Utwórz żądanie obsługi.</span><span class="sxs-lookup"><span data-stu-id="976ce-139">Verify your contact information and create the support request.</span></span>

<span data-ttu-id="976ce-140">Firma Microsoft sprawdzenia żądania przez i próbuje jak najszybciej dostosowania potrzeb biznesowych.</span><span class="sxs-lookup"><span data-stu-id="976ce-140">Microsoft reviews your request and tries to accommodate your business needs as soon as possible.</span></span>

## <a name="next-steps"></a><span data-ttu-id="976ce-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="976ce-141">Next steps</span></span>

* [<span data-ttu-id="976ce-142">Omówienie usługi Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="976ce-142">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="976ce-143">Zarządzanie usługą Azure Data Lake Analytics przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="976ce-143">Manage Azure Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-manage-use-powershell.md)
* [<span data-ttu-id="976ce-144">Monitorowanie zadań usługi Azure Data Lake Analytics i rozwiązywanie problemów przy użyciu witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="976ce-144">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
