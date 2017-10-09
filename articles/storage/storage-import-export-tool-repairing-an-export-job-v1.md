---
title: zadanie eksportu Import/Eksport Azure - v1 aaaRepairing | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toorepair zadanie eksportu, która została utworzona, a następnie uruchomić przy użyciu hello Import/Eksport Azure usługi."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 728e2a42-04ce-4be8-9375-e9e2bc6827a5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 96c674fc7c697c37882fb2980c340303896ac6c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="repairing-an-export-job"></a>Naprawianie zadania eksportu
Po zakończeniu zadania eksportu, możesz uruchomić narzędzie importu/eksportu pakietu Microsoft Azure lokalne powitania:  
  
1.  Pobierz wszystkie pliki, że usługa Import/Eksport Azure hello nie tooexport.  
  
2.  Sprawdź, czy hello plików na dysku hello zostały poprawnie wyeksportowane.  
  
Musi mieć łączność tooAzure magazynu toouse tej funkcji.  
  
polecenie Hello naprawy zadania importu jest **RepairExport**.

## <a name="repairexport-parameters"></a>Parametry RepairExport

Witaj następujące parametry można określić z **RepairExport**:  
  
|Parametr|Opis|  
|---------------|-----------------|  
|**/ r: < RepairFile\>**|Wymagany. Plik naprawy toohello ścieżki, który śledzi postęp hello naprawy hello i pozwala tooresume naprawę przerwania. Każdy dysk musi mieć jeden i tylko jeden plik naprawy. Po uruchomieniu naprawy dla danego dysku przechodzą w hello ścieżki tooa naprawy pliku, które jeszcze nie istnieje. tooresume naprawę przerwania, należy przekazać w nazwie hello istniejącego pliku naprawy. zawsze należy określać Hello naprawy pliku odpowiedniego toohello dysk docelowy.|  
|**/ logdir: < LogDirectory\>**|Opcjonalny. Katalog dziennika Hello. Pełne pliki dziennika zostaną zapisane toothis katalogu. Jeśli katalog dziennika nie jest określony, bieżący katalog hello będzie używany jako katalog dziennika hello.|  
|**/ d: < TargetDirectory\>**|Wymagany. Witaj toovalidate katalogu i naprawy. Zazwyczaj jest to katalog główny hello hello eksportu dysku, ale może też być sieciowego udziału plików zawierający kopię hello wyeksportowane pliki.|  
|**/BK: < BitLockerKey\>**|Opcjonalny. Należy określić hello klucza funkcji BitLocker, jeśli chcesz, aby toounlock narzędzie hello są szyfrowane, gdy hello wyeksportowane pliki przechowywane.|  
|**/SN: < StorageAccountName\>**|Wymagany. zadanie eksportowania Hello nazwę konta magazynu hello hello.|  
|**/SK: < StorageAccountKey\>**|**Wymagane** tylko wtedy, gdy nie określono kontenera sygnatury dostępu Współdzielonego. zadanie eksportowania Hello klucz konta usługi dla konta magazynu hello hello.|  
|**/csas: < ContainerSas\>**|**Wymagane** tylko wtedy, gdy nie określono klucza konta magazynu hello. kontener Hello SAS do uzyskiwania dostępu do obiektów blob hello skojarzone z zadaniem eksportu hello.|  
|**/ CopyLogFile: < DriveCopyLogFile\>**|Wymagany. Witaj ścieżki toohello dysku kopii pliku dziennika. Plik Hello jest generowany przez hello usługi Import/Eksport systemu Windows Azure i można pobrać z magazynu obiektów blob hello skojarzone z zadaniem hello. Witaj Kopiuj plik dziennika zawiera informacje dotyczące obiektów blob nie powiodło się lub pliki, które są toobe naprawić.|  
|**/ ManifestFile: < DriveManifestFile\>**|Opcjonalny. Witaj dysk ścieżki toohello eksportu pliku manifestu. Ten plik jest generowany przez usługę Windows Azure importu/eksportu hello i przechowywane na dysku eksportu hello i opcjonalnie w obiekcie blob na koncie magazynu hello skojarzone z zadaniem hello.<br /><br /> Witaj zawartości hello plików na dysku eksportu hello zostaną zweryfikowane wartości skrótu MD5 hello zawarte w tym pliku. Wszystkie pliki, które są określone toobe uszkodzony będzie toohello pobrane i ponownie zapisane docelowy katalogów.|  
  
## <a name="using-repairexport-mode-toocorrect-failed-exports"></a>Przy użyciu RepairExport toocorrect trybu nie powiodło się eksportowanie  
Można użyć hello Azure narzędzie importu/eksportu toodownload pliki, których nie powiodła się tooexport. plik dziennika kopii Hello będzie zawierać listę plików, których nie powiodła się tooexport.  
  
Hello przyczyny niepowodzeń eksportu: hello następujące możliwości:  
  
-   Uszkodzone dyski  
  
-   klucz konta magazynu Hello została zmieniona w trakcie procesu transferu hello  
  
Narzędzie hello toorun w **RepairExport** trybie, należy najpierw tooconnect hello dysku zawierającego hello wyeksportowane pliki tooyour komputera. Następnie należy uruchomić narzędzie importu/eksportu Azure, określenie hello ścieżki toothat dysku z hello hello `/d` parametru. Należy również toospecify hello ścieżki toohello dysku kopii dziennika pobranego pliku. Hello poniżej poniższy przykład wiersz polecenia uruchamia hello narzędzia toorepair wszystkie pliki, których nie powiodła się tooexport:  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log  
```  
  
Witaj poniżej znajduje się przykład kopii pliku dziennika, który zawiera ten jeden blok w hello tooexport obiektu blob nie powiodło się:  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog>  
  <DriveId>9WM35C2V</DriveId>  
  <Blob Status="CompletedWithErrors">  
    <BlobPath>pictures/wild/desert.jpg</BlobPath>  
    <FilePath>\pictures\wild\desert.jpg</FilePath>  
    <LastModified>2012-09-18T23:47:08Z</LastModified>  
    <Length>163840</Length>  
    <BlockList>  
      <Block Offset="65536" Length="65536" Id="AQAAAA==" Status="Failed" />  
    </BlockList>  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```  
  
plik dziennika kopii Hello wskazuje, wystąpił błąd podczas pobierania został hello usługi Import/Eksport systemu Windows Azure, jednego pliku toohello bloków hello blob na powitania eksportu dysku. Witaj inne składniki pliku hello pobrana pomyślnie, a długość pliku hello została poprawnie ustawiona. W takim przypadku narzędzie hello będzie Otwórz plik hello na powitania dysku, Pobierz bloku hello z konta magazynu hello i Zapisz toohello pliku zakresu, zaczynając od przesunięcia 65536 o długości 65536.  
  
## <a name="using-repairexport-toovalidate-drive-contents"></a>Przy użyciu zawartości dysku toovalidate RepairExport  
Import/Eksport Azure można również używać z hello **RepairExport** opcji toovalidate hello zawartości na dysku hello są poprawne. Plik manifestu Hello na każdym dysku eksportu zawiera MD5s hello zawartość hello dysku.  
  
Witaj usługi Import/Eksport Azure można także zapisać pliki manifestu hello tooa konta magazynu podczas procesu eksportowania hello. Witaj lokalizację plików manifestu hello jest dostępny za pośrednictwem hello [pobrania zadania](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operacji po ukończeniu zadania hello. Zobacz [usługi Import/Eksport Format pliku manifestu](storage-import-export-file-format-metadata-and-properties.md) Aby uzyskać więcej informacji o formacie hello dysku pliku manifestu.  
  
Witaj poniższy przykład przedstawia sposób toorun hello Azure narzędzie importu/eksportu z hello **/ManifestFile** i **/CopyLogFile** parametry:  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log /ManifestFile:G:\9WM35C3U.manifest  
```  
  
Witaj poniżej znajduje się przykład pliku manifestu:  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveManifest Version="2011-10-01">  
  <Drive>  
    <DriveId>9WM35C3U</DriveId>  
    <ClientCreator>Windows Azure Import/Export service</ClientCreator>  
    <BlobList>
      <Blob>  
        <BlobPath>pictures/city/redmond.jpg</BlobPath>  
        <FilePath>\pictures\city\redmond.jpg</FilePath>  
        <Length>15360</Length>  
        <PageRangeList>  
          <PageRange Offset="0" Length="3584" Hash="72FC55ED9AFDD40A0C8D5C4193208416" />  
          <PageRange Offset="3584" Length="3584" Hash="68B28A561B73D1DA769D4C24AA427DB8" />  
          <PageRange Offset="7168" Length="512" Hash="F521DF2F50C46BC5F9EA9FB787A23EED" />  
        </PageRangeList>  
        <PropertiesPath Hash="E72A22EA959566066AD89E3B49020C0A">\pictures\city\redmond.jpg.properties</PropertiesPath>  
      </Blob>  
      <Blob>  
        <BlobPath>pictures/wild/canyon.jpg</BlobPath>  
        <FilePath>\pictures\wild\canyon.jpg</FilePath>  
        <Length>10884</Length>  
        <BlockList>  
          <Block Offset="0" Length="2721" Id="AAAAAA==" Hash="263DC9C4B99C2177769C5EBE04787037" />  
          <Block Offset="2721" Length="2721" Id="AQAAAA==" Hash="0C52BAE2CC20EFEC15CC1E3045517AA6" />  
          <Block Offset="5442" Length="2721" Id="AgAAAA==" Hash="73D1CB62CB426230C34C9F57B7148F10" />  
          <Block Offset="8163" Length="2721" Id="AwAAAA==" Hash="11210E665C5F8E7E4F136D053B243E6A" />  
        </BlockList>  
        <PropertiesPath Hash="81D7F81B2C29F10D6E123D386C3A4D5A">\pictures\wild\canyon.jpg.properties</PropertiesPath>  
      </Blob> 
    </BlobList>  
 </Drive>  
</DriveManifest>  
``` 
  
Po zakończenia procesu naprawy hello narzędzie hello zapoznaj się z artykułem każdego pliku, do którego odwołuje się plik manifestu hello i Sprawdź integralność pliku hello skrótów hello MD5. Dla manifest hello powyżej przechodzą przez hello następujące składniki.  

```  
G:\pictures\city\redmond.jpg, offset 0, length 3584  
  
G:\pictures\city\redmond.jpg, offset 3584, length 3584  
  
G:\pictures\city\redmond.jpg, offset 7168, length 3584  
  
G:\pictures\city\redmond.jpg.properties  
  
G:\pictures\wild\canyon.jpg, offset 0, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 2721, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 5442, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 8163, length 2721  
  
G:\pictures\wild\canyon.jpg.properties  
```

Dowolny składnik Niepowodzenie weryfikacji hello zostanie pobrana przez narzędzie hello i ulegną toohello tego samego pliku na dysku hello.  
  
## <a name="next-steps"></a>Następne kroki
 
* [Definiowanie hello Azure narzędzie importu/eksportu](storage-import-export-tool-setup-v1.md)   
* [Przygotowywanie dysków twardych do zadania importu](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [Sprawdzanie stanu zadania za pomocą plików dziennika kopiowania](storage-import-export-tool-reviewing-job-status-v1.md)   
* [Naprawianie zadania importu](storage-import-export-tool-repairing-an-import-job-v1.md)   
* [Rozwiązywanie problemów z hello Azure narzędzie importu/eksportu](storage-import-export-tool-troubleshooting-v1.md)
