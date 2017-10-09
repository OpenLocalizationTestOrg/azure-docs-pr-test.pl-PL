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
ms.openlocfilehash: 945eb4f9eff28c92ec963585d27cba73a7eb59bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a>Krótki przewodnik dotyczący często używanych poleceń zadań importu
Ta sekcja zawiera szybki przegląd niektóre często używanych poleceń. Aby uzyskać szczegółowe dane użycia, zobacz [przygotowywanie dyski twarde dla zadania importu](../storage-import-export-tool-preparing-hard-drives-import-v1.md).  

## <a name="prepare-a-hard-drive-when-data-has-already-been-copied-toohello-hard-drive"></a>Przygotowywanie dysku twardego, jeśli dane zostały już skopiowane toohello dysk twardy
 Hello następujące polecenia przygotowuje dysk twardy, gdy danych został już skopiowane tooit, ale nie ma jeszcze zaszyfrowany za pomocą funkcji BitLocker:  
  
```  
  WAImportExport.exe PrepImport /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /t:d /encrypt /srcdir:d:\movies\drama /dstdir:movies/drama/ /skipwrite
```    

## <a name="copy-a-single-directory-tooa-hard-drive"></a>Kopiowanie dysku twardego tooa jednego katalogu  
 następujące polecenie Hello kopiuje jednego źródła katalogu tooa dysku twardego, który nie ma jeszcze zaszyfrowany za pomocą funkcji BitLocker:  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
## <a name="copy-two-directories-tooa-hard-drive"></a>Skopiuj dwa katalogi tooa dysku  
 toocopy dwa katalogi tooa dysk źródłowy, hello Użyj następującego polecenia:  
  
 Witaj pierwsze polecenie Określa katalog dziennika hello, klucz konta magazynu, literę dysku docelowym, `format/encrypt` wymagania oraz typowe parametry:  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
 drugie polecenie Hello określa hello pliku dziennika, nowy identyfikator sesji i lokalizacje źródłowa i docelowa hello:  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:music /srcdir:d:\Music /dstdir:entertainment/music/  
```  
  
## <a name="copy-a-large-file-tooa-hard-drive-in-a-second-copy-session"></a>Kopiowanie dużych plików dysku twardego tooa w drugiej sesji kopiowania  
 następujące polecenie Hello kopiuje dysku twardego tooa jednego dużego pliku, który został przygotowany w poprzedniej sesji kopiowania:  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:dvd /srcfile:d:\dvd\favoritemovie.vhd /dstblob:dvd/favoritemovie.vhd  
```  
  
## <a name="next-steps"></a>Następne kroki

* [Przykładowy przepływ pracy tooprepare dysków dla zadania importu](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)
