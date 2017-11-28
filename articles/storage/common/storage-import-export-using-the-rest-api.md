---
title: "Przy użyciu interfejsu API REST usługi Import/Eksport Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, gdzie można znaleźć zasobów dla za pomocą usługi Import/Eksport Azure interfejsu API REST, w tym zarówno instrukcje, jak i odwołanie do materiałów."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 233f80e9-2e7f-48e0-9639-5c7785e7d743
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: b780385ad0af34bcb15639683d1aa5d689b38b50
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="using-the-azure-importexport-service-rest-api"></a><span data-ttu-id="814b4-103">Korzystanie z interfejsu API REST usługi Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="814b4-103">Using the Azure Import/Export service REST API</span></span>

<span data-ttu-id="814b4-104">Usługa Import/Eksport Microsoft Azure udostępnia interfejs API REST umożliwiające sterowanie programowe zadań importu i eksportu.</span><span class="sxs-lookup"><span data-stu-id="814b4-104">The Microsoft Azure Import/Export service exposes a REST API to enable programmatic control of import/export jobs.</span></span> <span data-ttu-id="814b4-105">Służy do wykonywania operacji importu/eksportu, które można wykonać za pomocą interfejsu API REST [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="814b4-105">You can use the REST API to perform all of the import/export operations that you can perform with the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="814b4-106">Ponadto można użyć interfejsu API REST wykonywania pewnych operacji szczegółowych, takich jak badania procent zakończenia zadania, która nie jest obecnie dostępna w klasycznym portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="814b4-106">Additionally, you can use the REST API to perform certain granular operations, such as querying the percentage completion of a job, which is not currently available in the Azure classic portal.</span></span>

<span data-ttu-id="814b4-107">Zobacz [za pomocą usługi Import/Eksport Microsoft Azure przesyłanie danych do magazynu obiektów Blob](../storage-import-export-service.md) Omówienie usługi Import/Eksport i samouczek, który demonstruje sposób tworzenia i zarządzania importowanie i eksportowanie zadań za pomocą portalu klasycznego.</span><span class="sxs-lookup"><span data-stu-id="814b4-107">See [Using the Microsoft Azure Import/Export service to Transfer Data to Blob Storage](../storage-import-export-service.md) for an overview of the Import/Export service and a tutorial that demonstrates how to use the classic portal to create and manage import and export jobs.</span></span>

## <a name="service-endpoints"></a><span data-ttu-id="814b4-108">Punkty końcowe usługi</span><span class="sxs-lookup"><span data-stu-id="814b4-108">Service endpoints</span></span>

<span data-ttu-id="814b4-109">Import/Eksport Azure dostawcy zasobów usługi Azure Resource Manager i usługi zawiera zestaw interfejsów API REST na następujący punkt końcowy HTTPS zarządzania zadania importu/eksportu:</span><span class="sxs-lookup"><span data-stu-id="814b4-109">The Azure Import/Export service is a resource provider for Azure Resource Manager and provides a set of REST APIs at the following HTTPS endpoint for managing import/export jobs:</span></span>

```
https://management.azure.com/subscriptions/<subscription-id>/resourceGroups/<resource-group>/providers/Microsoft.ImportExport/jobs/<job-name>
```

## <a name="versioning"></a><span data-ttu-id="814b4-110">Przechowywanie wersji</span><span class="sxs-lookup"><span data-stu-id="814b4-110">Versioning</span></span>

<span data-ttu-id="814b4-111">Należy określić żądań do usługi Import/Eksport `api-version` parametru i ustaw dla niego wartość `2016-11-01`.</span><span class="sxs-lookup"><span data-stu-id="814b4-111">Requests to the Import/Export service must specify the `api-version` parameter and set its value to `2016-11-01`.</span></span>

## <a name="importexport-service-operations"></a><span data-ttu-id="814b4-112">Import/Eksport operacji usługi</span><span class="sxs-lookup"><span data-stu-id="814b4-112">Import/Export service operations</span></span>

[<span data-ttu-id="814b4-113">Tworzenie zadania importu</span><span class="sxs-lookup"><span data-stu-id="814b4-113">Creating an import job</span></span>](../storage-import-export-creating-an-import-job.md)

[<span data-ttu-id="814b4-114">Tworzenie zadania eksportu</span><span class="sxs-lookup"><span data-stu-id="814b4-114">Creating an export job</span></span>](../storage-import-export-creating-an-export-job.md)

[<span data-ttu-id="814b4-115">Pobieranie informacji o stanie zadania</span><span class="sxs-lookup"><span data-stu-id="814b4-115">Retrieving state information for a job</span></span>](storage-import-export-retrieving-state-info-for-a-job.md)

[<span data-ttu-id="814b4-116">Wyliczanie zadań</span><span class="sxs-lookup"><span data-stu-id="814b4-116">Enumerating jobs</span></span>](../storage-import-export-enumerating-jobs.md)

[<span data-ttu-id="814b4-117">Anulowanie i usuwanie zadań</span><span class="sxs-lookup"><span data-stu-id="814b4-117">Cancelling and deleting jobs</span></span>](storage-import-export-cancelling-and-deleting-jobs.md)

[<span data-ttu-id="814b4-118">Manifesty wykonywanie kopii zapasowych dysków</span><span class="sxs-lookup"><span data-stu-id="814b4-118">Backing Up drive manifests</span></span>](../storage-import-export-backing-up-drive-manifests.md)

[<span data-ttu-id="814b4-119">Diagnostyka i odzyskiwanie po błędach zadań usługi Import/Export</span><span class="sxs-lookup"><span data-stu-id="814b4-119">Diagnostics and error recovery for Import/Export jobs</span></span>](../storage-import-export-diagnostics-and-error-recovery.md)

## <a name="next-steps"></a><span data-ttu-id="814b4-120">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="814b4-120">Next steps</span></span>

* [<span data-ttu-id="814b4-121">Magazyn importu/eksportu REST</span><span class="sxs-lookup"><span data-stu-id="814b4-121">Storage Import/Export REST</span></span>](/rest/api/storageimportexport)
