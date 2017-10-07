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
ms.openlocfilehash: 363731ede4751124a714b4ce96852e0b8c4dbca4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="reviewing-azure-importexport-job-status-with-copy-log-files"></a>Przeglądanie Import/Eksport Azure stan zadania kopiowania plików dzienników
Kiedy hello usługi Import/Eksport Microsoft Azure przetwarza dyski skojarzone z zadaniem importu lub eksportu, zapisuje kopii dziennika pliki toohello magazynu konta tooor z którego są importowania lub eksportowania obiektów blob. plik dziennika Hello zawiera szczegółowe informacje dotyczące każdego pliku, który został zaimportowany ani eksportowane. plik dziennika kopii tooeach adres URL Hello jest zwracany, jeśli można zbadać stanu hello zadanie zostało ukończone; zobacz [pobrania zadania](/rest/api/storageservices/Get-Job3) Aby uzyskać więcej informacji.  

## <a name="example-urls"></a>Adresy URL

adresy URL do kopiowania plików dziennika dla zadania importu z dwóch dysków są następujące Hello:  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM35C2V_20130921-034307-902_error.xml`  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM45A6Q_20130921-042122-021_error.xml`  
  
 Zobacz [usługi Import/Eksport Format pliku dziennika](../storage-import-export-file-format-log.md) formatu hello kopiowaniu dzienników i hello pełną listę kodów stanu.  
  
## <a name="next-steps"></a>Następne kroki
 
 * [Definiowanie hello Azure narzędzie importu/eksportu](storage-import-export-tool-setup-v1.md)   
 * [Przygotowywanie dysków twardych do zadania importu](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
 * [Naprawianie zadania importu](../storage-import-export-tool-repairing-an-import-job-v1.md)   
 * [Naprawianie zadania eksportu](../storage-import-export-tool-repairing-an-export-job-v1.md)   
 * [Rozwiązywanie problemów z hello Azure narzędzie importu/eksportu](storage-import-export-tool-troubleshooting-v1.md)
