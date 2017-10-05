---
title: "Przeglądanie stanu zadania Import/Eksport Azure - v1 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak pliki dziennika utworzone po sprzed uruchomienia zadania importu lub eksportu, aby wyświetlić stan zadania importu/eksportu."
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
ms.openlocfilehash: 621e41df127fded6ec6fe1f71e86cb8630965a70
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="reviewing-azure-importexport-job-status-with-copy-log-files"></a><span data-ttu-id="f6354-103">Przeglądanie Import/Eksport Azure stan zadania kopiowania plików dzienników</span><span class="sxs-lookup"><span data-stu-id="f6354-103">Reviewing Azure Import/Export job status with copy log files</span></span>
<span data-ttu-id="f6354-104">Kiedy usługa Import/Eksport Microsoft Azure przetwarza dyski skojarzone z zadaniem importu lub eksportu, zapisuje kopiowania plików dziennika do konta magazynu do lub z którego są importowania lub eksportowania obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="f6354-104">When the Microsoft Azure Import/Export service processes drives associated with an import or export job, it writes copy log files to the storage account to or from which you are importing or exporting blobs.</span></span> <span data-ttu-id="f6354-105">Plik dziennika zawiera szczegółowe informacje dotyczące każdego pliku, który został zaimportowany ani eksportowane.</span><span class="sxs-lookup"><span data-stu-id="f6354-105">The log file contains detailed status about each file that was imported or exported.</span></span> <span data-ttu-id="f6354-106">Zwracany jest adres URL do każdego pliku dziennika kopii po wykonaniu kwerendy stanu zadanie zostało ukończone; zobacz [pobrania zadania](/rest/api/storageservices/Get-Job3) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="f6354-106">The URL to each copy log file is returned when you query the status of a completed job; see [Get Job](/rest/api/storageservices/Get-Job3) for more information.</span></span>  

## <a name="example-urls"></a><span data-ttu-id="f6354-107">Adresy URL</span><span class="sxs-lookup"><span data-stu-id="f6354-107">Example URLs</span></span>

<span data-ttu-id="f6354-108">Adresy URL do kopiowania plików dziennika dla zadania importu z dwóch dysków są następujące:</span><span class="sxs-lookup"><span data-stu-id="f6354-108">The following are example URLs for copy log files for an import job with two drives:</span></span>  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM35C2V_20130921-034307-902_error.xml`  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM45A6Q_20130921-042122-021_error.xml`  
  
 <span data-ttu-id="f6354-109">Zobacz [usługi Import/Eksport Format pliku dziennika](storage-import-export-file-format-log.md) formatu kopiowaniu dzienników i z pełną listą kodów stanu.</span><span class="sxs-lookup"><span data-stu-id="f6354-109">See [Import/Export service Log File Format](storage-import-export-file-format-log.md) for the format of copy logs and the full list of status codes.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="f6354-110">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f6354-110">Next steps</span></span>
 
 * [<span data-ttu-id="f6354-111">Trwa konfigurowanie narzędzia Azure Import/Eksport</span><span class="sxs-lookup"><span data-stu-id="f6354-111">Setting Up the Azure Import/Export Tool</span></span>](storage-import-export-tool-setup-v1.md)   
 * [<span data-ttu-id="f6354-112">Przygotowywanie dysków twardych do zadania importu</span><span class="sxs-lookup"><span data-stu-id="f6354-112">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
 * [<span data-ttu-id="f6354-113">Naprawianie zadania importu</span><span class="sxs-lookup"><span data-stu-id="f6354-113">Repairing an import job</span></span>](storage-import-export-tool-repairing-an-import-job-v1.md)   
 * [<span data-ttu-id="f6354-114">Naprawianie zadania eksportu</span><span class="sxs-lookup"><span data-stu-id="f6354-114">Repairing an export job</span></span>](storage-import-export-tool-repairing-an-export-job-v1.md)   
 * [<span data-ttu-id="f6354-115">Rozwiązywanie problemów z narzędziem Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="f6354-115">Troubleshooting the Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
