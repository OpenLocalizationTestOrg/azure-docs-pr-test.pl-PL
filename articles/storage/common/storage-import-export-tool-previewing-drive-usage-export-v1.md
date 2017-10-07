---
title: "aaaPreviewing użycia dysków dla zadania eksportu Import/Eksport Azure - v1 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toopreview hello listę obiektów blob wybrany dla zadania eksportu w usłudze Import/Eksport Azure hello."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 7707d744-7ec7-4de8-ac9b-93a18608dc9a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 7378c159f6d11702cda9ae7654e84d85f9b671b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="previewing-drive-usage-for-an-export-job"></a>Wyświetlanie podglądu użycia dysków przez zadanie eksportu
Przed utworzeniem zadania eksportu należy toochoose wyeksportowane przez zestaw toobe obiektów blob. Hello usługi Import/Eksport Microsoft Azure umożliwia toouse listę obiektów blob ścieżki lub obiektu blob prefiksy toorepresent obiekty BLOB hello zaznaczony.  
  
Następnie należy toodetermine liczbę dysków należy toosend. Witaj narzędzie importu/eksportu umożliwia hello `PreviewExport` użycia dysków toopreview polecenia dla obiektów blob hello wybrane, na podstawie rozmiaru hello dysków hello ma toouse.

## <a name="command-line-parameters"></a>Parametry wiersza polecenia

Można użyć hello następujące parametry, używając hello `PreviewExport` polecenie z hello narzędzie importu/eksportu.

|Parametr wiersza polecenia|Opis|  
|--------------------------|-----------------|  
|**/ logdir:**< LogDirectory\>|Opcjonalny. Katalog dziennika Hello. Pełne pliki dziennika zostaną zapisane toothis katalogu. Jeśli katalog dziennika nie jest określony, bieżący katalog hello będzie używany jako katalog dziennika hello.|  
|**/SN:**< StorageAccountName\>|Wymagany. zadanie eksportowania Hello nazwę konta magazynu hello hello.|  
|**/SK:**< StorageAccountKey\>|Wymagany tylko wtedy, gdy nie określono kontenera sygnatury dostępu Współdzielonego. zadanie eksportowania Hello klucz konta usługi dla konta magazynu hello hello.|  
|**/csas:**< ContainerSas\>|Wymagany tylko wtedy, gdy nie określono klucza konta magazynu. kontener Hello sygnatury dostępu Współdzielonego dla listy hello obiekty BLOB toobe eksportowane w hello zadanie eksportu.|  
|**/ ExportBlobListFile:**< ExportBlobListFile\>|Wymagany. Ścieżka toohello XML pliku zawierającego listę obiektów blob ścieżek lub obiektu blob prefiksy ścieżki dla toobe obiekty BLOB hello wyeksportowane. format pliku Hello używany w hello `BlobListBlobPath` element hello [zawiesić zadanie](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operacji hello interfejsu API REST usługi Import/Eksport.|  
|**/ DriveSize:**< DriveSize\>|Wymagany. Witaj rozmiar toouse dysków dla zadania eksportu *np.*, 500 GB, 1,5 TB.|  

## <a name="command-line-example"></a>Przykład wiersza polecenia

Witaj poniższym przykładzie pokazano hello `PreviewExport` polecenia:  
  
```  
WAImportExport.exe PreviewExport /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /ExportBlobListFile:C:\WAImportExport\mybloblist.xml /DriveSize:500GB    
```  
  
Hello eksportu obiektów blob listy plik może zawierać nazwy obiektów blob i obiektów blob prefiksy, jak pokazano poniżej:  
  
```xml 
<?xml version="1.0" encoding="utf-8"?>  
<BlobList>  
<BlobPath>pictures/animals/koala.jpg</BlobPath>  
<BlobPathPrefix>/vhds/</BlobPathPrefix>  
<BlobPathPrefix>/movies/</BlobPathPrefix>  
</BlobList>  
```

Hello Azure narzędzie importu/eksportu zawiera listę wszystkich toobe obiekty BLOB wyeksportowany i oblicza jak toopack ich na dyski hello określony rozmiar, biorąc pod uwagę wszystkie niezbędne koszty następnie szacuje hello liczba dysków potrzebne obiekty BLOB hello toohold i użycie dysku informacje.  
  
Oto przykład danych wyjściowych hello, z dziennikami informacyjną pominięte:  
  
```  
Number of unique blob paths/prefixes:   3  
Number of duplicate blob paths/prefixes:        0  
Number of nonexistent blob paths/prefixes:      1  
  
Drive size:     500.00 GB  
Number of blobs that can be exported:   6  
Number of blobs that cannot be exported:        2  
Number of drives needed:        3  
        Drive #1:       blobs = 1, occupied space = 454.74 GB  
        Drive #2:       blobs = 3, occupied space = 441.37 GB  
        Drive #3:       blobs = 2, occupied space = 131.28 GB    
```  
  
## <a name="next-steps"></a>Następne kroki

* [Odwołanie do usługi Azure narzędzie importu/eksportu](../storage-import-export-tool-how-to-v1.md)
