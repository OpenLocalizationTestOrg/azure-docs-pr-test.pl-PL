---
title: "Podręczna karta informacyjna dotycząca polecenia zadania importu narzędzia importu/eksportu Azure | Dokumentacja firmy Microsoft"
description: "Dokumentacja poleceń Azure narzędzie importu/eksportu importu często używanych poleceń zadania."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: e9377e0c5001cf5be220e19e06ff96c1e058e853
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a><span data-ttu-id="83878-103">Krótki przewodnik dotyczący często używanych poleceń zadań importu</span><span class="sxs-lookup"><span data-stu-id="83878-103">Quick reference for frequently used commands for import jobs</span></span>

<span data-ttu-id="83878-104">W tym artykule przedstawiono szybki przegląd niektóre często używanych poleceń.</span><span class="sxs-lookup"><span data-stu-id="83878-104">This article provides a quick reference for some frequently used commands.</span></span> <span data-ttu-id="83878-105">Aby uzyskać szczegółowe dane użycia, zobacz [przygotowywanie dyski twarde dla zadania importu](storage-import-export-tool-preparing-hard-drives-import.md).</span><span class="sxs-lookup"><span data-stu-id="83878-105">For detailed usage, see [Preparing Hard Drives for an Import Job](storage-import-export-tool-preparing-hard-drives-import.md).</span></span>

## <a name="first-session"></a><span data-ttu-id="83878-106">Pierwsza sesja</span><span class="sxs-lookup"><span data-stu-id="83878-106">First session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1 /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

## <a name="second-session"></a><span data-ttu-id="83878-107">Drugi sesji</span><span class="sxs-lookup"><span data-stu-id="83878-107">Second session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2 /DataSet:dataset-2.csv
```

## <a name="abort-latest-session"></a><span data-ttu-id="83878-108">Przerwij najnowszych sesji</span><span class="sxs-lookup"><span data-stu-id="83878-108">Abort latest session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2 /AbortSession
```

## <a name="resume-latest-interrupted-session"></a><span data-ttu-id="83878-109">Wznów najnowszych przerwania sesji</span><span class="sxs-lookup"><span data-stu-id="83878-109">Resume latest interrupted session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#3 /ResumeSession
```

## <a name="add-drives-to-latest-session"></a><span data-ttu-id="83878-110">Dodawanie dysków do najnowszych sesji</span><span class="sxs-lookup"><span data-stu-id="83878-110">Add drives to latest session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#3 /AdditionalDriveSet:driveset-2.csv
```

## <a name="next-steps"></a><span data-ttu-id="83878-111">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="83878-111">Next steps</span></span>

* [<span data-ttu-id="83878-112">Przykładowy przepływ pracy przygotowywania dysków twardych do zadania importu</span><span class="sxs-lookup"><span data-stu-id="83878-112">Sample workflow to prepare hard drives for an import job</span></span>](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow.md)
