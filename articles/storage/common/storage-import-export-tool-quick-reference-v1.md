---
title: "Podręczna karta informacyjna dotycząca polecenia zadania importu narzędzia importu/eksportu Azure - v1 | Dokumentacja firmy Microsoft"
description: "Dokumentacja poleceń Azure narzędzie importu/eksportu importu często używanych poleceń zadania. Odnosi się do v1 narzędzia importu/eksportu."
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
ms.openlocfilehash: 370cf6fae7ae106e8341f65086c8b8187d335746
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a><span data-ttu-id="db0c4-104">Krótki przewodnik dotyczący często używanych poleceń zadań importu</span><span class="sxs-lookup"><span data-stu-id="db0c4-104">Quick reference for frequently used commands for import jobs</span></span>
<span data-ttu-id="db0c4-105">Ta sekcja zawiera szybki przegląd niektóre często używanych poleceń.</span><span class="sxs-lookup"><span data-stu-id="db0c4-105">This section provides a quick reference for some frequently used commands.</span></span> <span data-ttu-id="db0c4-106">Aby uzyskać szczegółowe dane użycia, zobacz [przygotowywanie dyski twarde dla zadania importu](../storage-import-export-tool-preparing-hard-drives-import-v1.md).</span><span class="sxs-lookup"><span data-stu-id="db0c4-106">For detailed usage, see [Preparing Hard Drives for an Import Job](../storage-import-export-tool-preparing-hard-drives-import-v1.md).</span></span>  

## <a name="prepare-a-hard-drive-when-data-has-already-been-copied-to-the-hard-drive"></a><span data-ttu-id="db0c4-107">Przygotowanie dysk twardy, jeśli dane zostały już skopiowane na dysku twardym</span><span class="sxs-lookup"><span data-stu-id="db0c4-107">Prepare a hard drive when data has already been copied to the hard drive</span></span>
 <span data-ttu-id="db0c4-108">Następujące polecenie przygotowuje dysk twardy, gdy dane już został skopiowany do niego, ale jeszcze nie został zaszyfrowany za pomocą funkcji BitLocker:</span><span class="sxs-lookup"><span data-stu-id="db0c4-108">The following command prepares a hard drive when data has already been copied to it, but has not yet been encrypted with BitLocker:</span></span>  
  
```  
  WAImportExport.exe PrepImport /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /t:d /encrypt /srcdir:d:\movies\drama /dstdir:movies/drama/ /skipwrite
```    

## <a name="copy-a-single-directory-to-a-hard-drive"></a><span data-ttu-id="db0c4-109">Skopiuj jednego katalogu na dysku twardym</span><span class="sxs-lookup"><span data-stu-id="db0c4-109">Copy a single directory to a hard drive</span></span>  
 <span data-ttu-id="db0c4-110">Następujące polecenie kopiuje katalog źródłowy pojedynczy dysk twardy, który nie ma jeszcze zaszyfrowany za pomocą funkcji BitLocker:</span><span class="sxs-lookup"><span data-stu-id="db0c4-110">The following command copies a single source directory to a hard drive that has not yet been encrypted with BitLocker:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
## <a name="copy-two-directories-to-a-hard-drive"></a><span data-ttu-id="db0c4-111">Skopiuj dwa katalogi na dysku twardym</span><span class="sxs-lookup"><span data-stu-id="db0c4-111">Copy two directories to a hard drive</span></span>  
 <span data-ttu-id="db0c4-112">Aby skopiować dwa katalogi źródłowe na dysku, użyj następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="db0c4-112">To copy two source directories to a drive, use the following commands:</span></span>  
  
 <span data-ttu-id="db0c4-113">Pierwsze polecenie Określa katalog dziennika, klucz konta magazynu, literę dysku docelowym, `format/encrypt` wymagania oraz typowe parametry:</span><span class="sxs-lookup"><span data-stu-id="db0c4-113">The first command specifies the log directory, storage account key, target drive letter, `format/encrypt` requirements, and common parameters:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
 <span data-ttu-id="db0c4-114">Drugie polecenie Określa plik dziennika, nowy identyfikator sesji i lokalizacje źródłowa i docelowa:</span><span class="sxs-lookup"><span data-stu-id="db0c4-114">The second command specifies the journal file, a new session ID, and the source and destination locations:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:music /srcdir:d:\Music /dstdir:entertainment/music/  
```  
  
## <a name="copy-a-large-file-to-a-hard-drive-in-a-second-copy-session"></a><span data-ttu-id="db0c4-115">Kopiowanie dużych plików na dysk twardy w drugiej sesji kopiowania</span><span class="sxs-lookup"><span data-stu-id="db0c4-115">Copy a large file to a hard drive in a second copy session</span></span>  
 <span data-ttu-id="db0c4-116">Polecenie kopiuje pojedynczy duży plik na dysk twardy, który został przygotowany w poprzedniej sesji kopiowania:</span><span class="sxs-lookup"><span data-stu-id="db0c4-116">The following command copies a single large file to a hard drive that was prepared in a previous copy session:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:dvd /srcfile:d:\dvd\favoritemovie.vhd /dstblob:dvd/favoritemovie.vhd  
```  
  
## <a name="next-steps"></a><span data-ttu-id="db0c4-117">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="db0c4-117">Next steps</span></span>

* [<span data-ttu-id="db0c4-118">Przykładowy przepływ pracy przygotowywania dysków twardych do zadania importu</span><span class="sxs-lookup"><span data-stu-id="db0c4-118">Sample workflow to prepare hard drives for an import job</span></span>](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)
