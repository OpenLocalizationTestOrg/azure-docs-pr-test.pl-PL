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
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a>Krótki przewodnik dotyczący często używanych poleceń zadań importu
Ta sekcja zawiera szybkie odwołań dla niektórych często używanych poleceń. Aby uzyskać szczegółowe dane użycia, zobacz [przygotowywanie dyski twarde dla zadania importu](storage-import-export-tool-preparing-hard-drives-import-v1.md).  

## <a name="prepare-the-disks-when-data-already-copied-to-the-disks"></a>Przygotowanie dysków, gdy dane są już skopiowane na dyskach
 Oto przykład polecenia do przygotowania dysków, gdy danych jeszcze skopiowany na dysk twardy, który nie został jeszcze zaszyfrowanych za pomocą funkcji BitLocker:  
  
```  
  WAImportExport.exe PrepImport /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /t:d /encrypt /srcdir:d:\movies\drama /dstdir:movies/drama/ /skipwrite
```    

## <a name="copy-a-single-directory-to-a-hard-drive"></a>Skopiuj jednego katalogu na dysku twardym  
 Oto przykład polecenia można skopiować katalogu źródłowego pojedynczy dysk twardy, który nie został jeszcze zaszyfrowanych za pomocą funkcji BitLocker:  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
## <a name="copy-wwo-directories-to-a-hard-drive"></a>Kopiowanie katalogów wwo na dysk twardy  
 Aby skopiować dwa katalogi źródłowe na dysku, konieczne będzie dwa polecenia.  
  
 Pierwsze polecenie Określa katalog dziennika, klucz konta magazynu, literę dysku docelowym i `format/encrypt` wymagania, oprócz typowych parametrów:  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
 Drugie polecenie Określa plik dziennika, nowy identyfikator sesji i lokalizacje źródłowa i docelowa:  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:music /srcdir:d:\Music /dstdir:entertainment/music/  
```  
  
## <a name="copy-a-large-file-to-a-hard-drive-in-a-second-copy-session"></a>Kopiowanie dużych plików na dysk twardy w drugiej sesji kopiowania  
 Oto przykład polecenia, który kopiuje jednego dużego pliku na dysku, który został przygotowany w poprzednim sesji kopiowania:  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:dvd /srcfile:d:\dvd\favoritemovie.vhd /dstblob:dvd/favoritemovie.vhd  
```  
  
## <a name="next-steps"></a>Następne kroki

* [Przykładowy przepływ pracy przygotowywania dysków twardych do zadania importu](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)
