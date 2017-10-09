---
title: Stan zadania Import/Eksport Azure - v1 aaaReviewing | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak pliki dziennika hello toouse utworzony podczas hello importu lub eksportu zadania był uruchamiany toosee hello stan zadania importu/eksportu hello."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: c69d1d69-6403-4eee-9949-0185faeecfa1
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: muralikk
ms.openlocfilehash: 378bc9a7ef6bfe65209413c8c4134f313a2c0d79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="reviewing-azure-importexport-job-status-with-copy-log-files"></a><span data-ttu-id="baa82-103">Przeglądanie Import/Eksport Azure stan zadania kopiowania plików dzienników</span><span class="sxs-lookup"><span data-stu-id="baa82-103">Reviewing Azure Import/Export job status with copy log files</span></span>
<span data-ttu-id="baa82-104">Kiedy hello usługi Import/Eksport Microsoft Azure przetwarza dyski skojarzone z zadaniem importu lub eksportu, zapisuje kopii dziennika pliki toohello magazynu konta tooor z którego są importowania lub eksportowania obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="baa82-104">When hello Microsoft Azure Import/Export service processes drives associated with an import or export job, it writes copy log files toohello storage account tooor from which you are importing or exporting blobs.</span></span> <span data-ttu-id="baa82-105">plik dziennika Hello zawiera szczegółowe informacje dotyczące każdego pliku, który został zaimportowany ani eksportowane.</span><span class="sxs-lookup"><span data-stu-id="baa82-105">hello log file contains detailed status about each file that was imported or exported.</span></span> <span data-ttu-id="baa82-106">plik dziennika kopii tooeach adres URL Hello jest zwracany, jeśli można zbadać stanu hello zadanie zostało ukończone; zobacz [pobrania zadania](/rest/api/storageservices/Get-Job3) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="baa82-106">hello URL tooeach copy log file is returned when you query hello status of a completed job; see [Get Job](/rest/api/storageservices/Get-Job3) for more information.</span></span>  

## <a name="example-urls"></a><span data-ttu-id="baa82-107">Adresy URL</span><span class="sxs-lookup"><span data-stu-id="baa82-107">Example URLs</span></span>

<span data-ttu-id="baa82-108">adresy URL do kopiowania plików dziennika dla zadania importu z dwóch dysków są następujące Hello:</span><span class="sxs-lookup"><span data-stu-id="baa82-108">hello following are example URLs for copy log files for an import job with two drives:</span></span>  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM35C2V_20130921-034307-902_error.xml`  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM45A6Q_20130921-042122-021_error.xml`  
  
 <span data-ttu-id="baa82-109">Zobacz [usługi Import/Eksport Format pliku dziennika](storage-import-export-file-format-log.md) formatu hello kopiowaniu dzienników i hello pełną listę kodów stanu.</span><span class="sxs-lookup"><span data-stu-id="baa82-109">See [Import/Export service Log File Format](storage-import-export-file-format-log.md) for hello format of copy logs and hello full list of status codes.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="baa82-110">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="baa82-110">Next steps</span></span>
 
 * [<span data-ttu-id="baa82-111">Definiowanie hello Azure narzędzie importu/eksportu</span><span class="sxs-lookup"><span data-stu-id="baa82-111">Setting Up hello Azure Import/Export Tool</span></span>](storage-import-export-tool-setup-v1.md)   
 * [<span data-ttu-id="baa82-112">Przygotowywanie dysków twardych do zadania importu</span><span class="sxs-lookup"><span data-stu-id="baa82-112">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
 * [<span data-ttu-id="baa82-113">Naprawianie zadania importu</span><span class="sxs-lookup"><span data-stu-id="baa82-113">Repairing an import job</span></span>](storage-import-export-tool-repairing-an-import-job-v1.md)   
 * [<span data-ttu-id="baa82-114">Naprawianie zadania eksportu</span><span class="sxs-lookup"><span data-stu-id="baa82-114">Repairing an export job</span></span>](storage-import-export-tool-repairing-an-export-job-v1.md)   
 * [<span data-ttu-id="baa82-115">Rozwiązywanie problemów z hello Azure narzędzie importu/eksportu</span><span class="sxs-lookup"><span data-stu-id="baa82-115">Troubleshooting hello Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
