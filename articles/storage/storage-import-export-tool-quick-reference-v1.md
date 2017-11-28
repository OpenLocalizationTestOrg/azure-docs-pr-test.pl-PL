---
title: "Dokumentacja aaaQuick dla polecenia zadania importu narzędzia importu/eksportu Azure - v1 | Dokumentacja firmy Microsoft"
description: "Dokumentacja poleceń Azure narzędzie importu/eksportu importu często używanych poleceń zadania. Odnosi się toov1 hello narzędzie importu/eksportu."
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
ms.openlocfilehash: e36f065e5d23268758cf6b6db9428fe8a8e1056d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a><span data-ttu-id="e6fd2-104">Krótki przewodnik dotyczący często używanych poleceń zadań importu</span><span class="sxs-lookup"><span data-stu-id="e6fd2-104">Quick reference for frequently used commands for import jobs</span></span>
<span data-ttu-id="e6fd2-105">Ta sekcja zawiera szybkie odwołań dla niektórych często używanych poleceń.</span><span class="sxs-lookup"><span data-stu-id="e6fd2-105">This section provides a quick references for some frequently used commands.</span></span> <span data-ttu-id="e6fd2-106">Aby uzyskać szczegółowe dane użycia, zobacz [przygotowywanie dyski twarde dla zadania importu](storage-import-export-tool-preparing-hard-drives-import-v1.md).</span><span class="sxs-lookup"><span data-stu-id="e6fd2-106">For detailed usage, see [Preparing Hard Drives for an Import Job](storage-import-export-tool-preparing-hard-drives-import-v1.md).</span></span>  

## <a name="prepare-hello-disks-when-data-already-copied-toohello-disks"></a><span data-ttu-id="e6fd2-107">Przygotowując dyski hello, gdy dane już skopiowane toohello dysków</span><span class="sxs-lookup"><span data-stu-id="e6fd2-107">Prepare hello disks when data already copied toohello disks</span></span>
 <span data-ttu-id="e6fd2-108">W tym miejscu jest tooprepare polecenia przykładowe dysków, gdy dane już skopiowane toohello dysk twardy, który nie został jeszcze zaszyfrowanych za pomocą funkcji BitLocker:</span><span class="sxs-lookup"><span data-stu-id="e6fd2-108">Here is a sample command tooprepare a disks when data already copied toohello hard drive that hasn't been yet been encrypted with BitLocker:</span></span>  
  
```  
  WAImportExport.exe PrepImport /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /t:d /encrypt /srcdir:d:\movies\drama /dstdir:movies/drama/ /skipwrite
```    

## <a name="copy-a-single-directory-tooa-hard-drive"></a><span data-ttu-id="e6fd2-109">Kopiowanie dysku twardego tooa jednego katalogu</span><span class="sxs-lookup"><span data-stu-id="e6fd2-109">Copy a single directory tooa hard drive</span></span>  
 <span data-ttu-id="e6fd2-110">Oto toocopy polecenia przykładowe, pojedynczego źródła katalogu tooa dysku twardym, który nie został jeszcze został zaszyfrowany za pomocą funkcji BitLocker:</span><span class="sxs-lookup"><span data-stu-id="e6fd2-110">Here is a sample command toocopy a single source directory tooa hard drive that hasn't been yet been encrypted with BitLocker:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
## <a name="copy-wwo-directories-tooa-hard-drive"></a><span data-ttu-id="e6fd2-111">Kopiowanie dysku twardego tooa wwo katalogów</span><span class="sxs-lookup"><span data-stu-id="e6fd2-111">Copy wwo directories tooa hard drive</span></span>  
 <span data-ttu-id="e6fd2-112">toocopy dwa katalogi tooa dysk źródłowy, konieczne będzie dwa polecenia.</span><span class="sxs-lookup"><span data-stu-id="e6fd2-112">toocopy two source directories tooa drive, you will need two commands.</span></span>  
  
 <span data-ttu-id="e6fd2-113">Witaj pierwsze polecenie Określa katalog dziennika hello, klucz konta magazynu, literę dysku docelowym i `format/encrypt` wymagania w dodanie toohello typowe parametry:</span><span class="sxs-lookup"><span data-stu-id="e6fd2-113">hello first command specifies hello log directory, storage account key, target drive letter and `format/encrypt` requirements, in addition toohello common parameters:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
 <span data-ttu-id="e6fd2-114">drugie polecenie Hello określa hello pliku dziennika, nowy identyfikator sesji i lokalizacje źródłowa i docelowa hello:</span><span class="sxs-lookup"><span data-stu-id="e6fd2-114">hello second command specifies hello journal file, a new session ID, and hello source and destination locations:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:music /srcdir:d:\Music /dstdir:entertainment/music/  
```  
  
## <a name="copy-a-large-file-tooa-hard-drive-in-a-second-copy-session"></a><span data-ttu-id="e6fd2-115">Kopiowanie dużych plików dysku twardego tooa w drugiej sesji kopiowania</span><span class="sxs-lookup"><span data-stu-id="e6fd2-115">Copy a large file tooa hard drive in a second copy session</span></span>  
 <span data-ttu-id="e6fd2-116">Poniżej przedstawiono przykładowe polecenia, które kopiuje dysk tooa jednego dużego pliku, który został przygotowany w poprzednim sesji kopiowania:</span><span class="sxs-lookup"><span data-stu-id="e6fd2-116">Here is a sample command that copies a single large file tooa drive that has been prepared in a previous copy session:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:dvd /srcfile:d:\dvd\favoritemovie.vhd /dstblob:dvd/favoritemovie.vhd  
```  
  
## <a name="next-steps"></a><span data-ttu-id="e6fd2-117">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e6fd2-117">Next steps</span></span>

* [<span data-ttu-id="e6fd2-118">Przykładowy przepływ pracy tooprepare dysków dla zadania importu</span><span class="sxs-lookup"><span data-stu-id="e6fd2-118">Sample workflow tooprepare hard drives for an import job</span></span>](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)
