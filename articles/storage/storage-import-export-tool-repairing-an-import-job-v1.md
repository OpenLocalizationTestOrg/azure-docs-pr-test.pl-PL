---
title: Import/Eksport Azure zadania importu - v1 aaaRepairing | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toorepair został utworzony i uruchamiany za pomocą zadania importu hello Import/Eksport Azure usługi."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 38cc16bd-ad55-4625-9a85-e1726c35fd1b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: a9ed81f50cffd8ae6e0cb21b25a04815c2b51ee5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="repairing-an-import-job"></a>Naprawianie zadania importu
Witaj usługi Import/Eksport Microsoft Azure może się nie powieść toocopy niektórych plików lub części pliku toohello usługi Windows Azure Blob. Niektóre błędy przyczyny:  
  
-   Uszkodzone pliki  
  
-   Uszkodzone dyski  
  
-   Witaj zmienione podczas transferowania plików hello klucz konta magazynu.  
  
Można uruchamiać hello narzędzia importu/eksportu pakietu Microsoft Azure hello importowania plików dziennika zadanie kopiowania, i narzędzie hello przekaże hello brakujących plików (lub części pliku) zadania importu toocomplete konta magazynu tooyour systemu Windows Azure.  
  
## <a name="repairimport-parameters"></a>Parametry RepairImport

Witaj następujące parametry można określić z **RepairImport**: 
  
|||  
|-|-|  
|**/ r:**< RepairFile\>|**Wymagane.** Plik naprawy toohello ścieżki, który śledzi postęp hello naprawy hello i pozwala tooresume naprawę przerwania. Każdy dysk musi mieć jeden i tylko jeden plik naprawy. Po uruchomieniu naprawy dla danego dysku przechodzą w hello ścieżki tooa naprawy pliku, które jeszcze nie istnieje. tooresume naprawę przerwania, należy przekazać w nazwie hello istniejącego pliku naprawy. zawsze należy określać Hello naprawy pliku odpowiedniego toohello dysk docelowy.|  
|**/ logdir:**< LogDirectory\>|**Opcjonalne.** Katalog dziennika Hello. Pełne pliki dziennika zostaną zapisane toothis katalogu. Jeśli katalog dziennika nie jest określony, bieżący katalog hello będzie używany jako katalog dziennika hello.|  
|**/ d:**< TargetDirectories\>|**Wymagane.** Co najmniej jeden oddzielonych średnikami katalogi, które zawierają hello oryginalnych plików, które zostały zaimportowane. Hello importowania dysku może być używany, ale nie jest wymagane, jeśli alternatywnych lokalizacji oryginalnych plików są dostępne.|  
|**/BK:**< BitLockerKey\>|**Opcjonalne.** Należy określić hello klucza funkcji BitLocker, jeśli chcesz toounlock narzędzie hello zaszyfrowanego dysku, której hello oryginalnych plików są dostępne.|  
|**/SN:**< StorageAccountName\>|**Wymagane.** Witaj nazwę konta magazynu hello hello Importuj zadanie.|  
|**/SK:**< StorageAccountKey\>|**Wymagane** tylko wtedy, gdy nie określono kontenera sygnatury dostępu Współdzielonego. Witaj klucz konta usługi dla konta magazynu hello hello Importuj zadanie.|  
|**/csas:**< ContainerSas\>|**Wymagane** tylko wtedy, gdy nie określono klucza konta magazynu hello. kontener Hello SAS do uzyskiwania dostępu do obiektów blob hello skojarzone z zadaniem importu hello.|  
|**/ CopyLogFile:**< DriveCopyLogFile\>|**Wymagane.** Ścieżka toohello dysku kopii pliku dziennika (pełnego dziennika lub dziennik błędów). Plik Hello jest generowany przez hello usługi Import/Eksport systemu Windows Azure i można pobrać z magazynu obiektów blob hello skojarzone z zadaniem hello. Witaj Kopiuj plik dziennika zawiera informacje dotyczące obiektów blob nie powiodło się lub pliki, które są toobe naprawić.|  
|**/ PathMapFile:**< DrivePathMapFile\>|**Opcjonalne.** Ścieżka pliku tekstowego tooa, który może służyć niejednoznaczności tooresolve, jeśli masz wiele plików z hello takie same nazwy, czy zostały importowania w hello samo zadanie. Witaj pierwszego czasu hello narzędzie jest uruchamiane, można wypełnić ten plik ze wszystkimi hello niejednoznaczne nazwy. Kolejnych uruchomieniach hello narzędzie będzie używać tego pliku tooresolve hello niejednoznaczności.|  
  
## <a name="using-hello-repairimport-command"></a>Za pomocą polecenia RepairImport hello  
toorepair importu danych przez przesyłania strumieniowego hello danych za pośrednictwem sieci hello, musisz określić hello hello katalogi, które zawierają hello oryginalnych plików zostały importowanie przy użyciu `/d` parametru. Należy również określić hello kopii dziennika pobranego pliku z konta magazynu. Toorepair wiersza polecenia typowe zadania importu z częściowa błędami wygląda następująco:  
  
```  
WAImportExport.exe RepairImport /r:C:\WAImportExport\9WM35C2V.rep /d:C:\Users\bob\Pictures;X:\BobBackup\photos /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C2V.log  
```  
  
Witaj poniżej znajduje się przykład kopii pliku dziennika. W tym przypadku jeden 64 K część plik został uszkodzony na dysku hello, który został wysłany dla zadania importu hello. Ponieważ jest to błąd tylko hello wskazane, hello pozostałe obiekty BLOB hello hello zadania zostały pomyślnie zaimportowane.  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog>  
 <DriveId>9WM35C2V</DriveId>  
 <Blob Status="CompletedWithErrors">  
 <BlobPath>pictures/animals/koala.jpg</BlobPath>  
 <FilePath>\animals\koala.jpg</FilePath>  
 <Length>163840</Length>  
 <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
 <PageRangeList>  
  <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted" />  
 </PageRangeList>  
 </Blob>  
 <Status>CompletedWithErrors</Status>  
</DriveLog>  
```
  
Po upływie tego dziennika kopii toohello narzędzie importu/eksportu Azure narzędzia hello spróbuje toofinish hello importu dla tego pliku przez skopiowanie zawartości brakuje hello hello sieci. Następujący przykład hello powyżej, narzędzie hello będzie szukać hello oryginalnego pliku `\animals\koala.jpg` w katalogach hello dwa `C:\Users\bob\Pictures` i `X:\BobBackup\photos`. Jeśli hello plików `C:\Users\bob\Pictures\animals\koala.jpg` istnieje, hello Azure narzędzie importu/eksportu skopiuje hello zakresu brakuje odpowiedniego obiektu blob danych toohello `http://bobmediaaccount.blob.core.windows.net/pictures/animals/koala.jpg`.  
  
## <a name="resolving-conflicts-when-using-repairimport"></a>Rozwiązywanie konfliktów, korzystając z RepairImport  
W niektórych sytuacjach narzędzia hello nie może być możliwe toofind lub Otwórz hello niezbędnego pliku dla jednego z hello następujące przyczyny: nie można odnaleźć pliku hello, plik hello jest niedostępny, nazwa pliku hello jest niejednoznaczny lub hello zawartość pliku hello nie jest już prawidłowe.  
  
Niejednoznaczny błąd mógł wystąpić, jeśli narzędzie hello próbuje toolocate `\animals\koala.jpg` i istnieje plik o tej samej nazwie w obu `C:\Users\bob\pictures` i `X:\BobBackup\photos`. Oznacza to, że oba `C:\Users\bob\pictures\animals\koala.jpg` i `X:\BobBackup\photos\animals\koala.jpg` istnieje na dyskach zadania importu hello.  
  
Witaj `/PathMapFile` opcja umożliwi tooresolve te błędy. Można określić hello nazwę pliku hello, zawierającą hello lista plików, które hello narzędzie nie może zidentyfikować toocorrectly. Witaj poniżej przedstawiono przykład wiersz polecenia, który będzie wypełnić `9WM35C2V_pathmap.txt`:  
  
```
WAImportExport.exe RepairImport /r:C:\WAImportExport\9WM35C2V.rep /d:C:\Users\bob\Pictures;X:\BobBackup\photos /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C2V.log /PathMapFile:C:\WAImportExport\9WM35C2V_pathmap.txt  
```
  
Narzędzie Hello następnie zapisuje ścieżki plików problematycznych hello zbyt`9WM35C2V_pathmap.txt`, jeden w każdym wierszu. Na przykład plik hello może zawierać następujące wpisy po uruchomieniu polecenia hello hello:  
 
```
\animals\koala.jpg  
\animals\kangaroo.jpg  
```
  
 Dla każdego pliku na liście hello możesz spróbować toolocate i otworzyć tooensure pliku hello jest toohello dostępne narzędzia. Jeśli chcesz, aby narzędzie hello tootell jawnie w przypadku, gdy toofind plik, można zmodyfikować hello Ścieżka mapowania pliku i Dodaj hello ścieżki tooeach pliku na powitania tej samej linii, oddzielone znakiem karty:  
  
```
\animals\koala.jpg           C:\Users\bob\Pictures\animals\koala.jpg  
\animals\kangaroo.jpg        X:\BobBackup\photos\animals\kangaroo.jpg  
```
  
Po wprowadzania hello niezbędne pliki toohello dostępne narzędzia lub aktualizowania hello ścieżki mapy pliku należy ponownie uruchomić proces importowania hello hello narzędzia toocomplete.  
  
## <a name="next-steps"></a>Następne kroki
 
* [Definiowanie hello Azure narzędzie importu/eksportu](storage-import-export-tool-setup-v1.md)   
* [Przygotowywanie dysków twardych do zadania importu](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [Sprawdzanie stanu zadania za pomocą plików dziennika kopiowania](storage-import-export-tool-reviewing-job-status-v1.md)   
* [Naprawianie zadania eksportu](storage-import-export-tool-repairing-an-export-job-v1.md)   
* [Rozwiązywanie problemów z hello Azure narzędzie importu/eksportu](storage-import-export-tool-troubleshooting-v1.md)
