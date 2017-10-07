---
title: "aaaMove tooand danych z magazynu obiektów Blob platformy Azure | Dokumentacja firmy Microsoft"
description: "Przenieś tooand danych z magazynu obiektów Blob platformy Azure"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d6681e30-ab45-45ea-a9fb-ac8acefe544d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;sachouks
ms.openlocfilehash: e12b8c157955195e826f8b108075afaf25ca7bd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage"></a><span data-ttu-id="d7667-103">Przenieś tooand danych z magazynu obiektów Blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d7667-103">Move data tooand from Azure Blob Storage</span></span>
[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<!-- just in case, adding this tooseparate these two include references -->

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

<span data-ttu-id="d7667-104">Która metoda jest najlepsze dla Ciebie zależy od danego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="d7667-104">Which method is best for you depends on your scenario.</span></span> <span data-ttu-id="d7667-105">Witaj [scenariusze zaawansowana analityka w usłudze Azure Machine Learning](machine-learning-data-science-plan-sample-scenarios.md) artykuł pomaga ustalić hello zasoby potrzebne dla różnych przepływów pracy nauki danych używany w hello zaawansowane analizy procesu.</span><span class="sxs-lookup"><span data-stu-id="d7667-105">hello [Scenarios for advanced analytics in Azure Machine Learning](machine-learning-data-science-plan-sample-scenarios.md) article helps you determine hello resources you need for a variety of data science workflows used in hello advanced analytics process.</span></span>

> [!NOTE]
> <span data-ttu-id="d7667-106">Magazyn obiektów blob tooAzure pełne wprowadzenie można znaleźć za[podstawy obiektów Blob Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) i zbyt[usługi obiektów Blob Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="d7667-106">For a complete introduction tooAzure blob storage, refer too[Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and too[Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

<span data-ttu-id="d7667-107">Alternatywnie, można użyć [fabryki danych Azure](https://azure.microsoft.com/services/data-factory/) do:</span><span class="sxs-lookup"><span data-stu-id="d7667-107">As an alternative, you can use [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) to:</span></span> 

* <span data-ttu-id="d7667-108">Tworzenie i planowanie potok, który pobiera dane z magazynu obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d7667-108">create and schedule a pipeline that downloads data from Azure blob storage,</span></span> 
* <span data-ttu-id="d7667-109">przekazywanie ich tooa opublikowane usługi sieci web Azure Machine Learning,</span><span class="sxs-lookup"><span data-stu-id="d7667-109">pass it tooa published Azure Machine Learning web service,</span></span> 
* <span data-ttu-id="d7667-110">otrzymywać wyniki analizy predykcyjnej hello, i</span><span class="sxs-lookup"><span data-stu-id="d7667-110">receive hello predictive analytics results, and</span></span> 
* <span data-ttu-id="d7667-111">Przekaż hello toostorage wyników.</span><span class="sxs-lookup"><span data-stu-id="d7667-111">upload hello results toostorage.</span></span> 

<span data-ttu-id="d7667-112">Aby uzyskać więcej informacji, zobacz [tworzenie potoków predykcyjnej przy użyciu fabryki danych Azure i usługi Azure Machine Learning](../data-factory/data-factory-azure-ml-batch-execution-activity.md).</span><span class="sxs-lookup"><span data-stu-id="d7667-112">For more information, see [Create predictive pipelines using Azure Data Factory and Azure Machine Learning](../data-factory/data-factory-azure-ml-batch-execution-activity.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d7667-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d7667-113">Prerequisites</span></span>
<span data-ttu-id="d7667-114">Tym dokumencie przyjęto założenie, że masz subskrypcję platformy Azure, konta magazynu i hello odpowiedniego klucza magazynu dla tego konta.</span><span class="sxs-lookup"><span data-stu-id="d7667-114">This document assumes that you have an Azure subscription, a storage account, and hello corresponding storage key for that account.</span></span> <span data-ttu-id="d7667-115">Przed przekazaniem/pobieranie danych, musisz znać Azure klucz konta magazynu nazwy i konta.</span><span class="sxs-lookup"><span data-stu-id="d7667-115">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="d7667-116">tooset zapasową subskrypcji platformy Azure, zobacz [bezpłatna miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d7667-116">tooset up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="d7667-117">Aby uzyskać instrukcje dotyczące tworzenia konta magazynu oraz uzyskiwanie konta i informacje o kluczu, zobacz [kont magazynu Azure o](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="d7667-117">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

