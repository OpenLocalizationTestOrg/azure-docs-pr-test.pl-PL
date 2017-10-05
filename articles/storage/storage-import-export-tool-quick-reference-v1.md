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
ms.openlocfilehash: 47f450ee87dac3db2ccf7659928d52a6330a5697
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a><span data-ttu-id="d5bd4-104">Krótki przewodnik dotyczący często używanych poleceń zadań importu</span><span class="sxs-lookup"><span data-stu-id="d5bd4-104">Quick reference for frequently used commands for import jobs</span></span>
<span data-ttu-id="d5bd4-105">Ta sekcja zawiera szybkie odwołań dla niektórych często używanych poleceń.</span><span class="sxs-lookup"><span data-stu-id="d5bd4-105">This section provides a quick references for some frequently used commands.</span></span> <span data-ttu-id="d5bd4-106">Aby uzyskać szczegółowe dane użycia, zobacz [przygotowywanie dyski twarde dla zadania importu](storage-import-export-tool-preparing-hard-drives-import-v1.md).</span><span class="sxs-lookup"><span data-stu-id="d5bd4-106">For detailed usage, see [Preparing Hard Drives for an Import Job](storage-import-export-tool-preparing-hard-drives-import-v1.md).</span></span>  

## <a name="prepare-the-disks-when-data-already-copied-to-the-disks"></a><span data-ttu-id="d5bd4-107">Przygotowanie dysków, gdy dane są już skopiowane na dyskach</span><span class="sxs-lookup"><span data-stu-id="d5bd4-107">Prepare the disks when data already copied to the disks</span></span>
 <span data-ttu-id="d5bd4-108">Oto przykład polecenia do przygotowania dysków, gdy danych jeszcze skopiowany na dysk twardy, który nie został jeszcze zaszyfrowanych za pomocą funkcji BitLocker:</span><span class="sxs-lookup"><span data-stu-id="d5bd4-108">Here is a sample command to prepare a disks when data already copied to the hard drive that hasn't been yet been encrypted with BitLocker:</span></span>  
  
```  
  WAImportExport.exe PrepImport /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /t:d /encrypt /srcdir:d:\movies\drama /dstdir:movies/drama/ /skipwrite
```    

## <a name="copy-a-single-directory-to-a-hard-drive"></a><span data-ttu-id="d5bd4-109">Skopiuj jednego katalogu na dysku twardym</span><span class="sxs-lookup"><span data-stu-id="d5bd4-109">Copy a single directory to a hard drive</span></span>  
 <span data-ttu-id="d5bd4-110">Oto przykład polecenia można skopiować katalogu źródłowego pojedynczy dysk twardy, który nie został jeszcze zaszyfrowanych za pomocą funkcji BitLocker:</span><span class="sxs-lookup"><span data-stu-id="d5bd4-110">Here is a sample command to copy a single source directory to a hard drive that hasn't been yet been encrypted with BitLocker:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
## <a name="copy-wwo-directories-to-a-hard-drive"></a><span data-ttu-id="d5bd4-111">Kopiowanie katalogów wwo na dysk twardy</span><span class="sxs-lookup"><span data-stu-id="d5bd4-111">Copy wwo directories to a hard drive</span></span>  
 <span data-ttu-id="d5bd4-112">Aby skopiować dwa katalogi źródłowe na dysku, konieczne będzie dwa polecenia.</span><span class="sxs-lookup"><span data-stu-id="d5bd4-112">To copy two source directories to a drive, you will need two commands.</span></span>  
  
 <span data-ttu-id="d5bd4-113">Pierwsze polecenie Określa katalog dziennika, klucz konta magazynu, literę dysku docelowym i `format/encrypt` wymagania, oprócz typowych parametrów:</span><span class="sxs-lookup"><span data-stu-id="d5bd4-113">The first command specifies the log directory, storage account key, target drive letter and `format/encrypt` requirements, in addition to the common parameters:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
 <span data-ttu-id="d5bd4-114">Drugie polecenie Określa plik dziennika, nowy identyfikator sesji i lokalizacje źródłowa i docelowa:</span><span class="sxs-lookup"><span data-stu-id="d5bd4-114">The second command specifies the journal file, a new session ID, and the source and destination locations:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:music /srcdir:d:\Music /dstdir:entertainment/music/  
```  
  
## <a name="copy-a-large-file-to-a-hard-drive-in-a-second-copy-session"></a><span data-ttu-id="d5bd4-115">Kopiowanie dużych plików na dysk twardy w drugiej sesji kopiowania</span><span class="sxs-lookup"><span data-stu-id="d5bd4-115">Copy a large file to a hard drive in a second copy session</span></span>  
 <span data-ttu-id="d5bd4-116">Oto przykład polecenia, który kopiuje jednego dużego pliku na dysku, który został przygotowany w poprzednim sesji kopiowania:</span><span class="sxs-lookup"><span data-stu-id="d5bd4-116">Here is a sample command that copies a single large file to a drive that has been prepared in a previous copy session:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:dvd /srcfile:d:\dvd\favoritemovie.vhd /dstblob:dvd/favoritemovie.vhd  
```  
  
## <a name="next-steps"></a><span data-ttu-id="d5bd4-117">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d5bd4-117">Next steps</span></span>

* [<span data-ttu-id="d5bd4-118">Przykładowy przepływ pracy przygotowywania dysków twardych do zadania importu</span><span class="sxs-lookup"><span data-stu-id="d5bd4-118">Sample workflow to prepare hard drives for an import job</span></span>](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)
