---
title: "Dokumentacja aaaQuick dla polecenia zadania importu narzędzia importu/eksportu Azure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 0a615aed938e5e1b52d55a340aa6b48fa0744367
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a><span data-ttu-id="71980-103">Krótki przewodnik dotyczący często używanych poleceń zadań importu</span><span class="sxs-lookup"><span data-stu-id="71980-103">Quick reference for frequently used commands for import jobs</span></span>

<span data-ttu-id="71980-104">W tym artykule przedstawiono szybki przegląd niektóre często używanych poleceń.</span><span class="sxs-lookup"><span data-stu-id="71980-104">This article provides a quick reference for some frequently used commands.</span></span> <span data-ttu-id="71980-105">Aby uzyskać szczegółowe dane użycia, zobacz [przygotowywanie dyski twarde dla zadania importu](storage-import-export-tool-preparing-hard-drives-import.md).</span><span class="sxs-lookup"><span data-stu-id="71980-105">For detailed usage, see [Preparing Hard Drives for an Import Job](storage-import-export-tool-preparing-hard-drives-import.md).</span></span>

## <a name="first-session"></a><span data-ttu-id="71980-106">Pierwsza sesja</span><span class="sxs-lookup"><span data-stu-id="71980-106">First session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1 /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

## <a name="second-session"></a><span data-ttu-id="71980-107">Drugi sesji</span><span class="sxs-lookup"><span data-stu-id="71980-107">Second session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2 /DataSet:dataset-2.csv
```

## <a name="abort-latest-session"></a><span data-ttu-id="71980-108">Przerwij najnowszych sesji</span><span class="sxs-lookup"><span data-stu-id="71980-108">Abort latest session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2 /AbortSession
```

## <a name="resume-latest-interrupted-session"></a><span data-ttu-id="71980-109">Wznów najnowszych przerwania sesji</span><span class="sxs-lookup"><span data-stu-id="71980-109">Resume latest interrupted session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#3 /ResumeSession
```

## <a name="add-drives-toolatest-session"></a><span data-ttu-id="71980-110">Dodawanie dysków toolatest sesji</span><span class="sxs-lookup"><span data-stu-id="71980-110">Add drives toolatest session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#3 /AdditionalDriveSet:driveset-2.csv
```

## <a name="next-steps"></a><span data-ttu-id="71980-111">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="71980-111">Next steps</span></span>

* [<span data-ttu-id="71980-112">Przykładowy przepływ pracy tooprepare dysków dla zadania importu</span><span class="sxs-lookup"><span data-stu-id="71980-112">Sample workflow tooprepare hard drives for an import job</span></span>](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow.md)
