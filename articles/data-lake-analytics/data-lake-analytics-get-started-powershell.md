---
title: "wprowadzenie do usługi Azure Data Lake Analytics przy użyciu programu Azure PowerShell aaaGet | Dokumentacja firmy Microsoft"
description: "Użyj programu Azure PowerShell toocreate konto usługi Data Lake Analytics, Utwórz zadanie usługi Data Lake Analytics przy użyciu języka U-SQL i przesłać zadanie hello. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 8a4e901e-9656-4a60-90d0-d78ff2f00656
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/04/2017
ms.author: edmaca
ms.openlocfilehash: cb9b35352d1cc9a78337448b1d6835875a212e08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-powershell"></a><span data-ttu-id="3b668-103">Wprowadzenie do pracy z usługą Azure Data Lake Analytics przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3b668-103">Get started with Azure Data Lake Analytics using Azure PowerShell</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="3b668-104">Dowiedz się, jak toouse toocreate programu Azure PowerShell usługi Azure Data Lake Analytics kont, a następnie przesłać i uruchamianie zadań U-SQL.</span><span class="sxs-lookup"><span data-stu-id="3b668-104">Learn how toouse Azure PowerShell toocreate Azure Data Lake Analytics accounts and then submit and run U-SQL jobs.</span></span> <span data-ttu-id="3b668-105">Więcej informacji na temat usługi Data Lake Analytics można znaleźć w artykule [Omówienie usługi Azure Data Lake Analytics](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3b668-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3b668-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3b668-106">Prerequisites</span></span>

<span data-ttu-id="3b668-107">Przed rozpoczęciem tego samouczka, musi mieć hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="3b668-107">Before you begin this tutorial, you must have hello following information:</span></span>

* <span data-ttu-id="3b668-108">**Konto usługi Azure Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="3b668-108">**An Azure Data Lake Analytics account**.</span></span> <span data-ttu-id="3b668-109">Zobacz [Wprowadzenie do usługi Data Lake Analytics](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-get-started-portal).</span><span class="sxs-lookup"><span data-stu-id="3b668-109">See [Get started with Data Lake Analytics](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-get-started-portal).</span></span>
* <span data-ttu-id="3b668-110">**Stacja robocza z programem Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="3b668-110">**A workstation with Azure PowerShell**.</span></span> <span data-ttu-id="3b668-111">Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3b668-111">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="3b668-112">Zaloguj się za tooAzure</span><span class="sxs-lookup"><span data-stu-id="3b668-112">Log in tooAzure</span></span>

<span data-ttu-id="3b668-113">W tym samouczku założono, że użytkownik wie już, jak korzystać z programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3b668-113">This tutorial assumes you are already familiar with using Azure PowerShell.</span></span> <span data-ttu-id="3b668-114">W szczególności należy tooknow jak toolog w tooAzure.</span><span class="sxs-lookup"><span data-stu-id="3b668-114">In particular, you need tooknow how toolog in tooAzure.</span></span> <span data-ttu-id="3b668-115">Zobacz hello [wprowadzenie do programu Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps) Jeśli potrzebujesz pomocy.</span><span class="sxs-lookup"><span data-stu-id="3b668-115">See hello [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps) if you need help.</span></span>

<span data-ttu-id="3b668-116">toolog się przy użyciu nazwy subskrypcji:</span><span class="sxs-lookup"><span data-stu-id="3b668-116">toolog in with a subscription name:</span></span>

```
Login-AzureRmAccount -SubscriptionName "ContosoSubscription"
```

<span data-ttu-id="3b668-117">Zamiast nazwy subskrypcji hello można także użyć toolog identyfikator subskrypcji w:</span><span class="sxs-lookup"><span data-stu-id="3b668-117">Instead of hello subscription name, you can also use a subscription id toolog in:</span></span>

```
Login-AzureRmAccount -SubscriptionId "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
```

<span data-ttu-id="3b668-118">W przypadku powodzenia hello dane wyjściowe tego polecenia wygląda hello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="3b668-118">If  successful, hello output of this command looks like hello following text:</span></span>

```
Environment           : AzureCloud
Account               : joe@contoso.com
TenantId              : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionId        : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionName      : ContosoSubscription
CurrentStorageAccount :
```

## <a name="preparing-for-hello-tutorial"></a><span data-ttu-id="3b668-119">Przygotowywanie do samouczka hello</span><span class="sxs-lookup"><span data-stu-id="3b668-119">Preparing for hello tutorial</span></span>

<span data-ttu-id="3b668-120">Witaj wstawki programu PowerShell w tym samouczku te informacje służą toostore następujące zmienne:</span><span class="sxs-lookup"><span data-stu-id="3b668-120">hello PowerShell snippets in this tutorial use these variables toostore this information:</span></span>

```
$rg = "<ResourceGroupName>"
$adls = "<DataLakeStoreAccountName>"
$adla = "<DataLakeAnalyticsAccountName>"
$location = "East US 2"
```

## <a name="get-information-about-a-data-lake-analytics-account"></a><span data-ttu-id="3b668-121">Uzyskiwanie informacji o koncie usługi Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="3b668-121">Get information about a Data Lake Analytics account</span></span>

```
Get-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla  
```

## <a name="submit-a-u-sql-job"></a><span data-ttu-id="3b668-122">Przesyłanie zadania U-SQL</span><span class="sxs-lookup"><span data-stu-id="3b668-122">Submit a U-SQL job</span></span>

<span data-ttu-id="3b668-123">Utwórz skrypt programu PowerShell zmiennej toohold hello U-SQL.</span><span class="sxs-lookup"><span data-stu-id="3b668-123">Create a PowerShell variable toohold hello U-SQL script.</span></span>

```
$script = @"
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

"@
```

<span data-ttu-id="3b668-124">Przedstawia hello skryptu.</span><span class="sxs-lookup"><span data-stu-id="3b668-124">Submit hello script.</span></span>

```
$job = Submit-AdlJob -AccountName $adla –Script $script
```

<span data-ttu-id="3b668-125">Alternatywnie można zapisać jako plik skryptu hello i przesłać o hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="3b668-125">Alternatively, you could save hello script as a file and submit with hello following command:</span></span>

```
$filename = "d:\test.usql"
$script | out-File $filename
$job = Submit-AdlJob -AccountName $adla –ScriptPath $filename
```


<span data-ttu-id="3b668-126">Pobierz stan hello danego zadania.</span><span class="sxs-lookup"><span data-stu-id="3b668-126">Get hello status of a specific job.</span></span> <span data-ttu-id="3b668-127">Nadal używać tego polecenia cmdlet, aż zobaczysz, że hello pracę.</span><span class="sxs-lookup"><span data-stu-id="3b668-127">Keep using this cmdlet until you see hello job is done.</span></span>

```
$job = Get-AdlJob -AccountName $adla -JobId $job.JobId
```

<span data-ttu-id="3b668-128">Zamiast samodzielnego wywołanie Get-AdlAnalyticsJob zakończenie zadania, możesz użyć polecenia cmdlet AdlJob oczekiwania hello.</span><span class="sxs-lookup"><span data-stu-id="3b668-128">Instead of calling Get-AdlAnalyticsJob over and over until a job finishes, you can use hello Wait-AdlJob cmdlet.</span></span>

```
Wait-AdlJob -Account $adla -JobId $job.JobId
```

<span data-ttu-id="3b668-129">Pobierz plik wyjściowy hello.</span><span class="sxs-lookup"><span data-stu-id="3b668-129">Download hello output file.</span></span>

```
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "C:\data.csv"
```

## <a name="see-also"></a><span data-ttu-id="3b668-130">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="3b668-130">See also</span></span>
* <span data-ttu-id="3b668-131">toosee hello sam samouczek przy użyciu innych narzędzi, kliknij przycisk hello selektor karty w górnej części hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="3b668-131">toosee hello same tutorial using other tools, click hello tab selectors on hello top of hello page.</span></span>
* <span data-ttu-id="3b668-132">toolearn U-SQL, zobacz [wprowadzenie do języka Azure Data Lake Analytics U-SQL](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3b668-132">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="3b668-133">Informacje o zadaniach zarządzania znajdziesz w artykule [Zarządzanie usługą Azure Data Lake Analytics przy użyciu witryny Azure Portal](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3b668-133">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
