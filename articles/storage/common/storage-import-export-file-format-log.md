---
title: format pliku dziennika importu/eksportu aaaAzure | Dokumentacja firmy Microsoft
description: "Więcej informacji na temat formatu hello hello pliki dziennika utworzone podczas czynności są wykonywane zadania usługi Import/Eksport."
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
ms.openlocfilehash: 15a652455aa947922af0aa39ccefe68811a3db19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-importexport-service-log-file-format"></a>Format pliku dziennika usług Azure Import/Eksport
Gdy hello usługi Import/Eksport Microsoft Azure wykonuje akcję na dysku jako część zadania importu lub eksportu, dziennikach tooblock obiekty BLOB na koncie magazynu hello skojarzonego z tym zadaniem.  
  
Istnieją dwa dzienniki, które mogą zostać zapisane przez hello importu/eksportu usług:  
  
-   Dziennik błędów Hello był zawsze generowany w przypadku hello błędu.  
  
-   Witaj pełnego dziennika nie jest domyślnie włączona, ale może zostać włączona przez ustawienie hello `EnableVerboseLog` właściwość [zawiesić zadanie](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) lub [właściwości zadania aktualizacji](/rest/api/storageimportexport/jobs#Jobs_Update) operacji.  
  
## <a name="log-file-location"></a>Lokalizacja pliku dziennika  
Witaj dziennikach tooblock obiekty BLOB w kontenerze hello lub określony przez hello katalog wirtualny `ImportExportStatesPath` ustawienie, które można ustawić na `Put Job` operacji. Witaj lokalizacji toowhich hello dziennikach zależy od sposobu uwierzytelniania jest określona dla zadania hello, wraz z hello wartość określona dla `ImportExportStatesPath`. Uwierzytelnianie hello zadania można określić za pomocą klucza konta magazynu lub kontener SAS (sygnatury dostępu współdzielonego).  
  
Nazwa Hello kontenera hello lub katalog wirtualny może być hello domyślną nazwę `waimportexport`, lub innego kontenera ani nazwy katalogu wirtualnego, który określisz.  
  
Witaj w poniższej tabeli przedstawiono hello możliwe opcje:  
  
|Metoda uwierzytelniania|Wartość `ImportExportStatesPath`elementu|Lokalizacja dziennika obiektów blob|  
|---------------------------|----------------------------------------------|---------------------------|  
|Klucz konta magazynu|Wartość domyślna|Kontener o nazwie `waimportexport`, która jest hello domyślnego kontenera. Na przykład:<br /><br /> `https://myaccount.blob.core.windows.net/waimportexport`|  
|Klucz konta magazynu|Wartość określona przez użytkownika|Kontener o nazwie przez użytkownika hello. Na przykład:<br /><br /> `https://myaccount.blob.core.windows.net/mylogcontainer`|  
|Kontener SAS|Wartość domyślna|Katalog wirtualny o nazwie `waimportexport`, czyli hello domyślną nazwę poniżej kontenera hello określone w hello sygnatury dostępu Współdzielonego.<br /><br /> Na przykład jeśli hello SAS określone dla zadania hello jest `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, następnie będzie hello lokalizacja dziennika`https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport`|  
|Kontener SAS|Wartość określona przez użytkownika|Katalog wirtualny o nazwie użytkownika hello, poniżej kontenera hello określone w hello sygnatury dostępu Współdzielonego.<br /><br /> Na przykład jeśli hello SAS określone dla zadania hello jest `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, i hello określony katalog wirtualny nosi nazwę `mylogblobs`, następnie będzie lokalizacja dziennika hello `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport/mylogblobs`.|  
  
Można pobrać adresu URL hello hello błąd i pełne dzienniki hello wywoływania [pobrania zadania](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operacji. Dzienniki Hello są dostępne po zakończeniu przetwarzania hello dysku.  
  
## <a name="log-file-format"></a>Format pliku dziennika  
Witaj formatu dla obu dzienników jest hello takie same: obiektu blob zawierające opisy XML hello zdarzeń, które wystąpiły podczas kopiowania obiektów blob między hello dysk twardy i konta powitania klienta.  
  
Pełny dziennik Hello zawiera pełne informacje na temat stanu hello hello operacji kopiowania dla każdego obiektu blob (w przypadku zadania importu) lub pliku (dla zadania eksportu), tylko hello informacje dotyczące obiektów blob lub plików, które napotkały błędy podczas hello zawiera dziennik błędów hello Importowanie lub eksportowanie zadania.  
  
format pełny dziennik Hello jest pokazany poniżej. Dziennik błędów Hello ma hello takie same struktury, ale odfiltrowuje pomyślnych operacji.  

```xml
<DriveLog Version="2014-11-01">  
  <DriveId>drive-id</DriveId>  
  [<Blob Status="blob-status">  
   <BlobPath>blob-path</BlobPath>  
   <FilePath>file-path</FilePath>  
   [<Snapshot>snapshot</Snapshot>]  
   <Length>length</Length>  
   [<LastModified>last-modified</LastModified>]  
   [<ImportDisposition Status="import-disposition-status">import-disposition</ImportDisposition>]  
   [page-range-list-or-block-list]  
   [metadata-status]  
   [properties-status]  
  </Blob>]  
  [<Blob>  
    . . .  
  </Blob>]  
  <Status>drive-status</Status>  
</DriveLog>  
  
page-range-list-or-block-list ::= 
  page-range-list | block-list  
  
page-range-list ::=   
<PageRangeList>  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       [Hash="md5-hash"] Status="page-range-status"/>]  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       [Hash="md5-hash"] Status="page-range-status"/>]  
</PageRangeList>  
  
block-list ::=  
<BlockList>  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]  
       [Hash="md5-hash"] Status="block-status"/>]  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]   
       [Hash="md5-hash"] Status="block-status"/>]  
</BlockList>  
  
metadata-status ::=  
<Metadata Status="metadata-status">  
   [<GlobalPath Hash="md5-hash">global-metadata-file-path</GlobalPath>]  
   [<Path Hash="md5-hash">metadata-file-path</Path>]  
</Metadata>  
  
properties-status ::=  
<Properties Status="properties-status">  
   [<GlobalPath Hash="md5-hash">global-properties-file-path</GlobalPath>]  
   [<Path Hash="md5-hash">properties-file-path</Path>]  
</Properties>  
```

Witaj poniższej tabeli opisano elementy hello hello pliku dziennika.  
  
|XML Element|Typ|Opis|  
|-----------------|----------|-----------------|  
|`DriveLog`|XML Element|Reprezentuje dziennika dysku.|  
|`Version`|Atrybut ciągu|Wersja Hello hello format dziennika.|  
|`DriveId`|Ciąg|Witaj numer seryjny sprzętu stacji.|  
|`Status`|Ciąg|Stan przetwarzania dysku hello. Zobacz hello `Drive Status Codes` tabela poniżej, aby uzyskać więcej informacji.|  
|`Blob`|Zagnieżdżone — element XML|Reprezentuje obiektu blob.|  
|`Blob/BlobPath`|Ciąg|Identyfikator URI obiektu hello blob Hello.|  
|`Blob/FilePath`|Ciąg|Witaj ścieżki względnej toohello pliku na dysku hello.|  
|`Blob/Snapshot`|Data i godzina|Wersja migawki Hello hello obiektów blob, tylko zadania eksportu.|  
|`Blob/Length`|Liczba całkowita|Witaj całkowita długość obiektu blob hello w bajtach.|  
|`Blob/LastModified`|Data i godzina|Witaj daty/godziny tego obiektu blob hello ostatniej modyfikacji, tylko zadania eksportu.|  
|`Blob/ImportDisposition`|Ciąg|Hello zaimportować dyspozycji hello obiektów blob, tylko zadania importu.|  
|`Blob/ImportDisposition/@Status`|Atrybut ciągu|Stan Hello hello zaimportować dyspozycji.|  
|`PageRangeList`|Zagnieżdżone — element XML|Reprezentuje listę zakresów stron dla stronicowych obiektów blob.|  
|`PageRange`|XML element|Reprezentuje zakres stron.|  
|`PageRange/@Offset`|Atrybut, liczba całkowita|Początkowe przesunięcie zakresu strony hello w obiekcie blob hello.|  
|`PageRange/@Length`|Atrybut, liczba całkowita|Długość w bajtach hello zakres stron.|  
|`PageRange/@Hash`|Atrybut ciągu|Kodowany w formacie Base16 Skrót MD5 hello strony zakresu.|  
|`PageRange/@Status`|Atrybut ciągu|Stan przetwarzania hello zakres stron.|  
|`BlockList`|Zagnieżdżone — element XML|Reprezentuje listę bloków dla blokowego obiektu blob.|  
|`Block`|XML element|Reprezentuje blok.|  
|`Block/@Offset`|Atrybut, liczba całkowita|Przesunięcie początkowe bloku hello w obiekcie blob hello.|  
|`Block/@Length`|Atrybut, liczba całkowita|Długość w bajtach hello bloku.|  
|`Block/@Id`|Atrybut ciągu|Identyfikator bloku Hello.|  
|`Block/@Hash`|Atrybut ciągu|Kodowany w formacie Base16 Skrót MD5 hello bloku.|  
|`Block/@Status`|Atrybut ciągu|Stan przetwarzania hello bloku.|  
|`Metadata`|Zagnieżdżone — element XML|Reprezentuje metadane hello obiektu blob.|  
|`Metadata/@Status`|Atrybut ciągu|Stan przetwarzania hello metadane obiektu blob.|  
|`Metadata/GlobalPath`|Ciąg|Ścieżka względna toohello globalnych metadanych pliku.|  
|`Metadata/GlobalPath/@Hash`|Atrybut ciągu|Kodowany w formacie Base16 Skrót MD5 hello globalnych metadanych pliku.|  
|`Metadata/Path`|Ciąg|Ścieżka względna toohello pliku metadanych.|  
|`Metadata/Path/@Hash`|Atrybut ciągu|Kodowany w formacie Base16 Skrót MD5 hello pliku metadanych.|  
|`Properties`|Zagnieżdżone — element XML|Reprezentuje hello właściwości obiektu blob.|  
|`Properties/@Status`|Atrybut ciągu|Stan przetwarzania hello właściwości obiektu blob, np. nie można odnaleźć pliku, ukończone.|  
|`Properties/GlobalPath`|Ciąg|Ścieżka względna toohello globalnych właściwości pliku.|  
|`Properties/GlobalPath/@Hash`|Atrybut ciągu|Kodowany w formacie Base16 Skrót MD5 hello globalnych właściwości pliku.|  
|`Properties/Path`|Ciąg|Ścieżka względna toohello właściwości pliku.|  
|`Properties/Path/@Hash`|Atrybut ciągu|Kodowany w formacie Base16 Skrót MD5 hello właściwości pliku.|  
|`Blob/Status`|Ciąg|Stan przetwarzania obiektu blob hello.|  
  
# <a name="drive-status-codes"></a>Kody stanu dysku  
Witaj Poniższa tabela zawiera listę kodów stanu hello przetwarzania dysku.  
  
|Kod stanu|Opis|  
|-----------------|-----------------|  
|`Completed`|dysk Hello zakończył przetwarzanie bez żadnych błędów.|  
|`CompletedWithWarnings`|dysk Hello zakończył przetwarzanie z ostrzeżeniami w jeden lub więcej obiektów blob na powitania importu przepisy określone dla obiektów blob hello.|  
|`CompletedWithErrors`|dysk Hello zostało zakończone z błędami obiektów blob lub fragmentów.|  
|`DiskNotFound`|Dysk nie znajduje się na dysku hello.|  
|`VolumeNotNtfs`|Hello pierwszy wolumin danych na dysku hello nie jest w formacie NTFS.|  
|`DiskOperationFailed`|Wystąpił nieznany błąd podczas wykonywania operacji na powitania dysku.|  
|`BitLockerVolumeNotFound`|Znaleziono encryptable woluminu funkcji BitLocker.|  
|`BitLockerNotActivated`|Nie włączono funkcji BitLocker w woluminie hello.|  
|`BitLockerProtectorNotFound`|Ochrona klucza Hello numerycznym hasłem nie istnieje na woluminie hello.|  
|`BitLockerKeyInvalid`|podane hasło numeryczne Hello nie można odblokować hello woluminu.|  
|`BitLockerUnlockVolumeFailed`|Nieznany błąd wystąpił podczas próby toounlock hello woluminu.|  
|`BitLockerFailed`|Wystąpił nieznany błąd podczas wykonywania operacji funkcji BitLocker.|  
|`ManifestNameInvalid`|Nazwa pliku manifestu Hello jest nieprawidłowa.|  
|`ManifestNameTooLong`|Nazwa pliku manifestu Hello jest zbyt długa.|  
|`ManifestNotFound`|Nie znaleziono pliku manifestu Hello.|  
|`ManifestAccessDenied`|Odmowa pliku manifestu toohello dostępu.|  
|`ManifestCorrupted`|Witaj pliku manifestu jest uszkodzony (zawartość hello nie odpowiada jego skrót).|  
|`ManifestFormatInvalid`|zawartość manifestu Hello jest niezgodny z wymaganym formatem toohello.|  
|`ManifestDriveIdMismatch`|Witaj Identyfikatora w pliku manifestu hello jest niezgodna z jedną odczytu z dysku hello hello dysku.|  
|`ReadManifestFailed`|Wystąpił błąd We/Wy dysku podczas odczytu z hello manifestu.|  
|`BlobListFormatInvalid`|blob listę obiektów blob eksportu Hello jest niezgodny z wymaganym formatem toohello.|  
|`BlobRequestForbidden`|Dostęp do obiektów blob toohello na koncie magazynu hello jest zabronione. Może to być klucz konta magazynu tooinvalid lub kontener sygnatury dostępu Współdzielonego.|  
|`InternalError`|I wystąpił błąd wewnętrzny podczas przetwarzania hello dysku.|  
  
## <a name="blob-status-codes"></a>Kody stanu obiektu blob  
Witaj Poniższa tabela zawiera listę kodów stanu hello do przetwarzania obiektu blob.  
  
|Kod stanu|Opis|  
|-----------------|-----------------|  
|`Completed`|Obiekt blob Hello zakończył przetwarzanie bez błędów.|  
|`CompletedWithErrors`|Obiekt blob Hello zakończył przetwarzanie z błędami w jednej lub więcej zakresów stron lub bloków metadanych i właściwości.|  
|`FileNameInvalid`|Nazwa pliku Hello jest nieprawidłowa.|  
|`FileNameTooLong`|Nazwa pliku Hello jest zbyt długa.|  
|`FileNotFound`|Nie znaleziono pliku Hello.|  
|`FileAccessDenied`|Odmowa dostępu do pliku toohello.|  
|`BlobRequestFailed`|żądanie usługi Blob Hello się, że tooaccess hello obiektów blob nie powiodło się.|  
|`BlobRequestForbidden`|żądanie usługi Blob Hello się, że tooaccess hello obiektu blob jest zabronione. Może to być klucz konta magazynu tooinvalid lub kontener sygnatury dostępu Współdzielonego.|  
|`RenameFailed`|Nie można obiektu blob hello toorename (dla zadania importu) lub pliku hello (dla zadania eksportu).|  
|`BlobUnexpectedChange`|Nieoczekiwana zmiana wystąpił błąd związany z obiektu blob hello (dla zadania eksportu).|  
|`LeasePresent`|Brak dzierżawę na powitania obiektu blob.|  
|`IOFailed`|Podczas przetwarzania obiektu blob hello wystąpił dysku lub w sieci, błąd We/Wy.|  
|`Failed`|Wystąpił nieznany błąd podczas przetwarzania hello obiektu blob.|  
  
## <a name="import-disposition-status-codes"></a>Kody stanu dyspozycji importu  
Witaj Poniższa tabela zawiera listę kodów stanu hello w celu rozwiązania dyspozycji importu.  
  
|Kod stanu|Opis|  
|-----------------|-----------------|  
|`Created`|Utworzono Hello obiektu blob.|  
|`Renamed`|Obiekt blob Hello została zmieniona na dyspozycji importu zmiany nazwy. Witaj `Blob/BlobPath` element zawiera hello identyfikator URI obiektu blob hello zmieniono jego nazwę.|  
|`Skipped`|Obiekt blob Hello zostało pominięte na `no-overwrite` zaimportować dyspozycji.|  
|`Overwritten`|Obiekt blob Hello zastąpiły istniejącym obiektem blob na `overwrite` zaimportować dyspozycji.|  
|`Cancelled`|Niepowodzenia wcześniejszego została zatrzymana, dalsze przetwarzanie hello dyspozycji importu.|  
  
## <a name="page-rangeblock-status-codes"></a>Kody stanu zakres/blok strony  
Witaj Poniższa tabela zawiera listę kodów stanu hello przetwarzania strony zakres lub blok.  
  
|Kod stanu|Opis|  
|-----------------|-----------------|  
|`Completed`|Witaj strony zakres lub blok zakończył przetwarzanie bez żadnych błędów.|  
|`Committed`|Blok Hello został przekazany, ale nie w hello pełne zablokowanych ponieważ inne bloki mają nie powiodło się lub umieść samej listy pełny blok nie powiodło się.|  
|`Uncommitted`|Blok Hello jest przekazany, ale nie zostało zatwierdzone.|  
|`Corrupted`|Witaj strony zakres lub blok jest uszkodzony (zawartość hello nie odpowiada jego skrót).|  
|`FileUnexpectedEnd`|Napotkano nieoczekiwany koniec pliku.|  
|`BlobUnexpectedEnd`|Napotkano nieoczekiwany koniec obiektu blob.|  
|`BlobRequestFailed`|Witaj obiektu Blob usługi żądania tooaccess hello zakres stron lub blok nie powiodło się.|  
|`IOFailed`|Podczas przetwarzania hello strony zakres lub blok wystąpił dysku lub w sieci, błąd We/Wy.|  
|`Failed`|Wystąpił nieznany błąd podczas przetwarzania hello strony zakres lub blok.|  
|`Cancelled`|Błąd przed została zatrzymana, dalsze przetwarzanie hello strony zakres lub blok.|  
  
## <a name="metadata-status-codes"></a>Kody stanu metadanych  
Witaj Poniższa tabela zawiera listę kodów stanu powitania dla przetwarzania metadane obiektu blob.  
  
|Kod stanu|Opis|  
|-----------------|-----------------|  
|`Completed`|metadane Hello zakończył przetwarzanie bez błędów.|  
|`FileNameInvalid`|Nazwa pliku metadanych Hello jest nieprawidłowa.|  
|`FileNameTooLong`|Nazwa pliku metadanych Hello jest zbyt długa.|  
|`FileNotFound`|Nie znaleziono pliku metadanych Hello.|  
|`FileAccessDenied`|Odmowa dostępu toohello metadane pliku.|  
|`Corrupted`|Plik metadanych Hello jest uszkodzony (zawartość hello nie odpowiada jego skrót).|  
|`XmlReadFailed`|Hello metadane zawartości jest niezgodny z wymaganym formatem toohello.|  
|`XmlWriteFailed`|Zapisywanie metadanych hello XML nie powiodło się.|  
|`BlobRequestFailed`|żądanie usługi Blob Hello się, że tooaccess hello metadanych nie powiodła się.|  
|`IOFailed`|Podczas przetwarzania metadanych hello wystąpił błąd We/Wy dysku lub w sieci.|  
|`Failed`|Wystąpił nieznany błąd podczas przetwarzania hello metadanych.|  
|`Cancelled`|Błąd przed została zatrzymana, dalsze przetwarzanie hello metadanych.|  
  
## <a name="properties-status-codes"></a>Kody stanu właściwości  
Witaj Poniższa tabela zawiera listę kodów stanu hello przetwarzania właściwości obiektu blob.  
  
|Kod stanu|Opis|  
|-----------------|-----------------|  
|`Completed`|właściwości Hello Zakończono przetwarzanie bez żadnych błędów.|  
|`FileNameInvalid`|Nazwa pliku właściwości Hello jest nieprawidłowa.|  
|`FileNameTooLong`|Nazwa pliku właściwości Hello jest zbyt długa.|  
|`FileNotFound`|Nie znaleziono Hello właściwości pliku.|  
|`FileAccessDenied`|Odmowa dostępu toohello właściwości pliku.|  
|`Corrupted`|Plik właściwości Hello jest uszkodzony (zawartość hello nie odpowiada jego skrót).|  
|`XmlReadFailed`|Hello właściwości zawartości jest niezgodny z wymaganym formatem toohello.|  
|`XmlWriteFailed`|Zapisywanie właściwości hello XML nie powiodło się.|  
|`BlobRequestFailed`|żądanie usługi Blob Hello się, że tooaccess hello właściwości nie powiodła się.|  
|`IOFailed`|Wystąpił błąd We/Wy dysku lub w sieci podczas przetwarzania hello właściwości.|  
|`Failed`|Wystąpił nieznany błąd podczas przetwarzania hello właściwości.|  
|`Cancelled`|Błąd przed została zatrzymana, dalsze przetwarzanie hello właściwości.|  
  
## <a name="sample-logs"></a>Dzienniki próbki  
Hello Oto przykład pełnego dziennika.  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveLog Version="2014-11-01">  
    <DriveId>WD-WMATV123456</DriveId>  
    <Blob Status="Completed">  
       <BlobPath>pictures/bob/wild/desert.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\wild\desert.jpg</FilePath>  
       <Length>98304</Length>  
       <ImportDisposition Status="Created">overwrite</ImportDisposition>  
       <BlockList>  
          <Block Offset="0" Length="65536" Id="AAAAAA==" Hash=" 9C8AE14A55241F98533C4D80D85CDC68" Status="Completed"/>  
          <Block Offset="65536" Length="32768" Id="AQAAAA==" Hash=" DF54C531C9B3CA2570FDDDB3BCD0E27D" Status="Completed"/>  
       </BlockList>  
       <Metadata Status="Completed">  
          <GlobalPath Hash=" E34F54B7086BCF4EC1601D056F4C7E37">\Users\bob\Pictures\wild\metadata.xml</GlobalPath>  
       </Metadata>  
    </Blob>  
    <Blob Status="CompletedWithErrors">  
       <BlobPath>pictures/bob/animals/koala.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\animals\koala.jpg</FilePath>  
       <Length>163840</Length>  
       <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
       <PageRangeList>  
          <PageRange Offset="0" Length="65536" Hash="19701B8877418393CB3CB567F53EE225" Status="Completed"/>  
          <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted"/>  
          <PageRange Offset="131072" Length="4096" Hash="9BA552E1C3EEAFFC91B42B979900A996" Status="Completed"/>  
       </PageRangeList>  
       <Properties Status="Completed">  
          <Path Hash="38D7AE80653F47F63C0222FEE90EC4E7">\Users\bob\Pictures\animals\koala.jpg.properties</Path>  
       </Properties>  
    </Blob>  
    <Status>CompletedWithErrors</Status>  
</DriveLog>  
```  
  
Poniżej przedstawiono Hello odpowiedni dziennik błędów.  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveLog Version="2014-11-01">  
    <DriveId>WD-WMATV6965824</DriveId>  
    <Blob Status="CompletedWithErrors">  
       <BlobPath>pictures/bob/animals/koala.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\animals\koala.jpg</FilePath>  
       <Length>163840</Length>  
       <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
       <PageRangeList>  
          <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted"/>  
       </PageRangeList>  
    </Blob>  
    <Status>CompletedWithErrors</Status>  
</DriveLog>  
```

 Dziennik błędów wykonaj powitania dla zadania importu zawiera błąd o pliku nie można odnaleźć na powitania importowania dysku. Należy pamiętać, że stan hello kolejnych składników `Cancelled`.  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog Version="2014-11-01">  
  <DriveId>9WM35C2V</DriveId>  
  <Blob Status="FileNotFound">  
    <BlobPath>pictures/animals/koala.jpg</BlobPath>  
    <FilePath>\animals\koala.jpg</FilePath>  
    <Length>30310</Length>  
    <ImportDisposition Status="Cancelled">rename</ImportDisposition>  
    <BlockList>  
      <Block Offset="0" Length="6062" Id="MD5/cAzn4h7VVSWXf696qp5Uaw==" Hash="700CE7E21ED55525977FAF7AAA9E546B" Status="Cancelled" />  
      <Block Offset="6062" Length="6062" Id="MD5/PEnGwYOI8LPLNYdfKr7kAg==" Hash="3C49C6C18388F0B3CB35875F2ABEE402" Status="Cancelled" />  
      <Block Offset="12124" Length="6062" Id="MD5/FG4WxqfZKuUWZ2nGTU2qVA==" Hash="146E16C6A7D92AE5166769C64D4DAA54" Status="Cancelled" />  
      <Block Offset="18186" Length="6062" Id="MD5/ZzibNDzr3IRBQENRyegeXQ==" Hash="67389B343CEBDC8441404351C9E81E5D" Status="Cancelled" />  
      <Block Offset="24248" Length="6062" Id="MD5/ZzibNDzr3IRBQENRyegeXQ==" Hash="67389B343CEBDC8441404351C9E81E5D" Status="Cancelled" />  
    </BlockList>  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```

Hello następujące dziennik błędów dla zadania eksportu wskazuje, czy zawartość obiektu blob hello został zapisany pomyślnie toohello dysku, ale że wystąpił błąd podczas eksportowania właściwości hello obiektu blob.  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog Version="2014-11-01">  
  <DriveId>9WM35C3U</DriveId>  
  <Blob Status="CompletedWithErrors">  
    <BlobPath>pictures/wild/canyon.jpg</BlobPath>  
    <FilePath>\pictures\wild\canyon.jpg</FilePath>  
    <LastModified>2012-09-18T23:47:08Z</LastModified>  
    <Length>163840</Length>  
    <BlockList />  
    <Properties Status="Failed" />  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```
  
## <a name="next-steps"></a>Następne kroki
 
* [Interfejs API REST importu/eksportu magazynu](/rest/api/storageimportexport/)
