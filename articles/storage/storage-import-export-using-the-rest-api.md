---
title: "Witaj aaaUsing interfejsu API REST usługi Import/Eksport Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, gdzie toofind zasoby przy użyciu hello Import/Eksport Azure usługi interfejsu API REST, w tym zarówno tooand jak materiałów referencyjnych."
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
ms.openlocfilehash: a01c170b1bc9c2b2ce9086d39de78a39fafb2c8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-importexport-service-rest-api"></a><span data-ttu-id="371e0-103">Przy użyciu interfejsu API REST usługi Import/Eksport Azure hello</span><span class="sxs-lookup"><span data-stu-id="371e0-103">Using hello Azure Import/Export service REST API</span></span>

<span data-ttu-id="371e0-104">Hello usługi Import/Eksport Microsoft Azure udostępnia interfejs API REST tooenable programowe kontrolę nad zadania importu/eksportu.</span><span class="sxs-lookup"><span data-stu-id="371e0-104">hello Microsoft Azure Import/Export service exposes a REST API tooenable programmatic control of import/export jobs.</span></span> <span data-ttu-id="371e0-105">Można użyć tooperform interfejsu API REST hello wszystkie hello importu/eksportu operacje, które można wykonywać za pomocą hello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="371e0-105">You can use hello REST API tooperform all of hello import/export operations that you can perform with hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="371e0-106">Ponadto można użyć tooperform interfejsu API REST hello niektóre szczegółowe operacji, takich jak badania hello procentu ukończenia zadania, które nie są obecnie dostępne w portalu klasycznym hello.</span><span class="sxs-lookup"><span data-stu-id="371e0-106">Additionally, you can use hello REST API tooperform certain granular operations, such as querying hello percentage completion of a job, which are not currently available in hello classic portal.</span></span>

<span data-ttu-id="371e0-107">Zobacz [przy użyciu hello Import/Eksport Microsoft Azure service tooTransfer danych tooBlob magazynu](storage-import-export-service.md) Omówienie usługi Import/Eksport hello i samouczek, który demonstruje sposób toouse hello toocreate portalu klasycznego i zarządzanie nimi importu i wyeksportować zadań.</span><span class="sxs-lookup"><span data-stu-id="371e0-107">See [Using hello Microsoft Azure Import/Export service tooTransfer Data tooBlob Storage](storage-import-export-service.md) for an overview of hello Import/Export service and a tutorial that demonstrates how toouse hello classic portal toocreate and manage import and export jobs.</span></span>

## <a name="service-endpoints"></a><span data-ttu-id="371e0-108">Punkty końcowe usługi</span><span class="sxs-lookup"><span data-stu-id="371e0-108">Service endpoints</span></span>

<span data-ttu-id="371e0-109">Hello usługi Import/Eksport Azure jest dostawcą zasobów dla usługi Azure Resource Manager i zawiera zestaw interfejsów API REST na powitania po końcowy HTTPS w celu zarządzania zadaniami importu/eksportu:</span><span class="sxs-lookup"><span data-stu-id="371e0-109">hello Azure Import/Export service is a resource provider for Azure Resource Manager and provides a set of REST APIs at hello following HTTPS endpoint for managing import/export jobs:</span></span>

```
https://management.azure.com/subscriptions/<subscription-id>/resourceGroups/<resource-group>/providers/Microsoft.ImportExport/jobs/<job-name>
```

## <a name="versioning"></a><span data-ttu-id="371e0-110">Przechowywanie wersji</span><span class="sxs-lookup"><span data-stu-id="371e0-110">Versioning</span></span>

<span data-ttu-id="371e0-111">Żądania toohello usługi Import/Eksport musi określać hello `api-version` parametru i ustaw jej wartość zbyt`2016-11-01`.</span><span class="sxs-lookup"><span data-stu-id="371e0-111">Requests toohello Import/Export service must specify hello `api-version` parameter and set its value too`2016-11-01`.</span></span>

## <a name="importexport-service-operations"></a><span data-ttu-id="371e0-112">Import/Eksport operacji usługi</span><span class="sxs-lookup"><span data-stu-id="371e0-112">Import/Export service operations</span></span>

[<span data-ttu-id="371e0-113">Tworzenie zadania importu</span><span class="sxs-lookup"><span data-stu-id="371e0-113">Creating an import job</span></span>](storage-import-export-creating-an-import-job.md)

[<span data-ttu-id="371e0-114">Tworzenie zadania eksportu</span><span class="sxs-lookup"><span data-stu-id="371e0-114">Creating an export job</span></span>](storage-import-export-creating-an-export-job.md)

[<span data-ttu-id="371e0-115">Pobieranie informacji o stanie zadania</span><span class="sxs-lookup"><span data-stu-id="371e0-115">Retrieving state information for a job</span></span>](storage-import-export-retrieving-state-info-for-a-job.md)

[<span data-ttu-id="371e0-116">Wyliczanie zadań</span><span class="sxs-lookup"><span data-stu-id="371e0-116">Enumerating jobs</span></span>](storage-import-export-enumerating-jobs.md)

[<span data-ttu-id="371e0-117">Anulowanie i usuwanie zadań</span><span class="sxs-lookup"><span data-stu-id="371e0-117">Cancelling and deleting jobs</span></span>](storage-import-export-cancelling-and-deleting-jobs.md)

[<span data-ttu-id="371e0-118">Manifesty wykonywanie kopii zapasowych dysków</span><span class="sxs-lookup"><span data-stu-id="371e0-118">Backing Up drive manifests</span></span>](storage-import-export-backing-up-drive-manifests.md)

[<span data-ttu-id="371e0-119">Diagnostyka i odzyskiwanie po błędach zadań usługi Import/Export</span><span class="sxs-lookup"><span data-stu-id="371e0-119">Diagnostics and error recovery for Import/Export jobs</span></span>](storage-import-export-diagnostics-and-error-recovery.md)

## <a name="next-steps"></a><span data-ttu-id="371e0-120">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="371e0-120">Next steps</span></span>

* [<span data-ttu-id="371e0-121">Magazyn importu/eksportu REST</span><span class="sxs-lookup"><span data-stu-id="371e0-121">Storage Import/Export REST</span></span>](/rest/api/storageimportexport)
