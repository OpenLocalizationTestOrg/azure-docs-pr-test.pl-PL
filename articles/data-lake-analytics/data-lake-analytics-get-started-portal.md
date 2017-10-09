---
title: "aaaGet Started with Azure Data Lake Analytics przy użyciu portalu Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć zadanie usługi Data Lake Analytics przy użyciu języka U-SQL toouse hello Azure toocreate portalu konta usługi Data Lake Analytics i przesłać zadanie hello. "
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: b1584d16-e0d2-4019-ad1f-f04be8c5b430
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/21/2017
ms.author: edmaca
ms.openlocfilehash: 6bb54404fa42cfed25b18bc2bfb7c72e6c361149
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-portal"></a><span data-ttu-id="1f0bd-103">Rozpoczynanie pracy z usługą Azure Data Lake Analytics przy użyciu witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="1f0bd-103">Get started with Azure Data Lake Analytics using Azure portal</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="1f0bd-104">Dowiedz się, jak toouse hello Azure toocreate portalu konta usługi Azure Data Lake Analytics, definiowania zadań w [U-SQL](data-lake-analytics-u-sql-get-started.md)i przesyłanie usługi Data Lake Analytics toohello zadania.</span><span class="sxs-lookup"><span data-stu-id="1f0bd-104">Learn how toouse hello Azure portal toocreate Azure Data Lake Analytics accounts, define jobs in [U-SQL](data-lake-analytics-u-sql-get-started.md), and submit jobs toohello Data Lake Analytics service.</span></span> <span data-ttu-id="1f0bd-105">Więcej informacji na temat usługi Data Lake Analytics można znaleźć w artykule [Omówienie usługi Azure Data Lake Analytics](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1f0bd-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1f0bd-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1f0bd-106">Prerequisites</span></span>

<span data-ttu-id="1f0bd-107">Przed rozpoczęciem tego samouczka musisz dysponować **subskrypcją platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="1f0bd-107">Before you begin this tutorial, you must have an **Azure subscription**.</span></span> <span data-ttu-id="1f0bd-108">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1f0bd-108">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="1f0bd-109">Tworzenie konta Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="1f0bd-109">Create a Data Lake Analytics account</span></span>

<span data-ttu-id="1f0bd-110">Teraz utworzysz usługi Data Lake Analytics i Data Lake Store konta na powitania sam czas.</span><span class="sxs-lookup"><span data-stu-id="1f0bd-110">Now, you will create a Data Lake Analytics and a Data Lake Store account at hello same time.</span></span>  <span data-ttu-id="1f0bd-111">Ten krok jest proste i trwa tylko około toofinish 60 sekund.</span><span class="sxs-lookup"><span data-stu-id="1f0bd-111">This step is simple and only takes about 60 seconds toofinish.</span></span>

1. <span data-ttu-id="1f0bd-112">Zaloguj się na toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1f0bd-112">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1f0bd-113">Kliknij pozycję **Nowy** >  **Dane + analiza** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="1f0bd-113">Click **New** >  **Data + Analytics** > **Data Lake Analytics**.</span></span>
3. <span data-ttu-id="1f0bd-114">Wybierz wartości hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="1f0bd-114">Select values for hello following items:</span></span>
   * <span data-ttu-id="1f0bd-115">**Nazwa**: nazwa konta usługi Data Lake Analytics (dozwolone są tylko małe litery i cyfry).</span><span class="sxs-lookup"><span data-stu-id="1f0bd-115">**Name**: Name your Data Lake Analytics account (Only lower case letters and numbers allowed).</span></span>
   * <span data-ttu-id="1f0bd-116">**Subskrypcja**: Wybierz hello subskrypcja platformy Azure używana na potrzeby hello konta usługi Analytics.</span><span class="sxs-lookup"><span data-stu-id="1f0bd-116">**Subscription**: Choose hello Azure subscription used for hello Analytics account.</span></span>
   * <span data-ttu-id="1f0bd-117">**Grupa zasobów**.</span><span class="sxs-lookup"><span data-stu-id="1f0bd-117">**Resource Group**.</span></span> <span data-ttu-id="1f0bd-118">Wybierz istniejącą grupę zasobów platformy Azure lub utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="1f0bd-118">Select an existing Azure Resource Group or create a new one.</span></span>
   * <span data-ttu-id="1f0bd-119">**Lokalizacja**.</span><span class="sxs-lookup"><span data-stu-id="1f0bd-119">**Location**.</span></span> <span data-ttu-id="1f0bd-120">Wybierz centrum danych platformy Azure dla konta usługi Data Lake Analytics hello.</span><span class="sxs-lookup"><span data-stu-id="1f0bd-120">Select an Azure data center for hello Data Lake Analytics account.</span></span>
   * <span data-ttu-id="1f0bd-121">**Data Lake Store**: wykonaj hello instrukcji toocreate nowe konto usługi Data Lake Store lub wybierz istniejący.</span><span class="sxs-lookup"><span data-stu-id="1f0bd-121">**Data Lake Store**: Follow hello instruction toocreate a new Data Lake Store account, or select an existing one.</span></span> 
4. <span data-ttu-id="1f0bd-122">Opcjonalnie wybierz warstwę cenową dla konta usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="1f0bd-122">Optionally, select a pricing tier for your Data Lake Analytics account.</span></span>
5. <span data-ttu-id="1f0bd-123">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="1f0bd-123">Click **Create**.</span></span> 


## <a name="your-first-u-sql-script"></a><span data-ttu-id="1f0bd-124">Pierwszy skrypt U-SQL</span><span class="sxs-lookup"><span data-stu-id="1f0bd-124">Your first U-SQL script</span></span>

<span data-ttu-id="1f0bd-125">Witaj następującego tekstu jest bardzo prosty skrypt U-SQL.</span><span class="sxs-lookup"><span data-stu-id="1f0bd-125">hello following text is a very simple U-SQL script.</span></span> <span data-ttu-id="1f0bd-126">Wszystko robi to zdefiniować małym zestawie danych skryptu hello, a następnie wpisz tego zestawu danych wychodzących toohello domyślne Data Lake Store jako plik o nazwie `/data.csv`.</span><span class="sxs-lookup"><span data-stu-id="1f0bd-126">All it does is define a small dataset within hello script and then write that dataset out toohello default Data Lake Store as a file called `/data.csv`.</span></span>

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
```

## <a name="submit-a-u-sql-job"></a><span data-ttu-id="1f0bd-127">Przesyłanie zadania U-SQL</span><span class="sxs-lookup"><span data-stu-id="1f0bd-127">Submit a U-SQL job</span></span>

1. <span data-ttu-id="1f0bd-128">Hello konta usługi Data Lake Analytics kliknij **nowe zadanie**.</span><span class="sxs-lookup"><span data-stu-id="1f0bd-128">From hello Data Lake Analytics account, click **New Job**.</span></span>
2. <span data-ttu-id="1f0bd-129">Wklej tekst hello hello powyższy skrypt U-SQL.</span><span class="sxs-lookup"><span data-stu-id="1f0bd-129">Paste in hello text of hello U-SQL script shown above.</span></span> 
3. <span data-ttu-id="1f0bd-130">Kliknij przycisk **Prześlij zadanie**.</span><span class="sxs-lookup"><span data-stu-id="1f0bd-130">Click **Submit Job**.</span></span>   
4. <span data-ttu-id="1f0bd-131">Czekać do momentu zmiany stanu zadania hello zbyt**zakończyło się pomyślnie**.</span><span class="sxs-lookup"><span data-stu-id="1f0bd-131">Wait until hello job status changes too**Succeeded**.</span></span>
5. <span data-ttu-id="1f0bd-132">Jeśli zadanie hello nie powiodło się, zobacz [monitorowanie zadań usługi Data Lake Analytics i rozwiązywanie problemów](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="1f0bd-132">If hello job failed, see [Monitor and troubleshoot Data Lake Analytics jobs](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span></span>
6. <span data-ttu-id="1f0bd-133">Kliknij przycisk hello **dane wyjściowe** , a następnie kliknij pozycję `data.csv`.</span><span class="sxs-lookup"><span data-stu-id="1f0bd-133">Click hello **Output** tab, and then click `data.csv`.</span></span> 

## <a name="see-also"></a><span data-ttu-id="1f0bd-134">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="1f0bd-134">See also</span></span>

* <span data-ttu-id="1f0bd-135">tooget Rozpoczęto tworzenie aplikacji U-SQL, zobacz [skryptów U-SQL opracowanie przy użyciu narzędzi Data Lake Tools dla programu Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="1f0bd-135">tooget started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="1f0bd-136">toolearn U-SQL, zobacz [wprowadzenie do języka Azure Data Lake Analytics U-SQL](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="1f0bd-136">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="1f0bd-137">Informacje o zadaniach zarządzania znajdziesz w artykule [Zarządzanie usługą Azure Data Lake Analytics przy użyciu witryny Azure Portal](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1f0bd-137">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
