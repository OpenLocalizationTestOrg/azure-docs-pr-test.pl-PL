---
title: format pliku manifestu importu/eksportu aaaAzure | Dokumentacja firmy Microsoft
description: "Informacje o hello format pliku manifestu hello dysku, który opisuje hello mapowanie między obiekty BLOB w magazynie obiektów Blob platformy Azure i plików na dysku w ramach zadania importu lub eksportu w usłudze Import/Eksport hello."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: f3119e1c-2c25-48ad-8752-a6ed4adadbb0
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: d7e5e1990482916f7ff5f891c97343b52e82b2f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-importexport-service-manifest-file-format"></a>Azure format pliku manifestu usługi Import/Eksport
Plik manifestu dysku Hello opisuje hello mapowanie między obiekty BLOB w magazynie obiektów Blob platformy Azure i plików na dysku obejmujące zadania importu lub eksportu. Dla operacji importowania pliku manifestu hello jest tworzony jako część procesu przygotowywania dysku hello i jest przechowywana na dysku hello, przed wysłaniem dysku hello toohello centrum danych Azure. Podczas operacji eksportowania hello manifest jest tworzony i zapisywany na dysku hello w przez hello usługi Import/Eksport Azure.  
  
Dla importu i zadań eksportu, plik manifestu dysku hello jest przechowywana na powitania importowania lub eksportowania dysku; nie jest przesyłane toohello usługi za pośrednictwem każdej operacji interfejsu API.  
  
Witaj poniżej opisano ogólny format pliku manifestu dysku hello:  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveManifest Version="2014-11-01">  
  <Drive>  
    <DriveId>drive-id</DriveId>  
    import-export-credential  
  
    <!-- First Blob List -->  
    <BlobList>  
      <!-- Global properties and metadata that applies tooall blobs -->  
      [<MetadataPath Hash="md5-hash">global-metadata-file-path</MetadataPath>]  
      [<PropertiesPath   
        Hash="md5-hash">global-properties-file-path</PropertiesPath>]  
  
      <!-- First Blob -->  
      <Blob>  
        <BlobPath>blob-path-relative-to-account</BlobPath>  
        <FilePath>file-path-relative-to-transfer-disk</FilePath>  
        [<ClientData>client-data</ClientData>]  
        [<Snapshot>snapshot</Snapshot>]  
        <Length>content-length</Length>  
        [<ImportDisposition>import-disposition</ImportDisposition>]  
        page-range-list-or-block-list          
        [<MetadataPath Hash="md5-hash">metadata-file-path</MetadataPath>]  
        [<PropertiesPath Hash="md5-hash">properties-file-path</PropertiesPath>]  
      </Blob>  
  
      <!-- Second Blob -->  
      <Blob>  
      . . .  
      </Blob>  
    </BlobList>  
  
    <!-- Second Blob List -->  
    <BlobList>  
    . . .  
    </BlobList>  
  </Drive>  
</DriveManifest>  
  
import-export-credential ::=   
  <StorageAccountKey>storage-account-key</StorageAccountKey> | <ContainerSas>container-sas</ContainerSas>  
  
page-range-list-or-block-list ::=   
  page-range-list | block-list  
  
page-range-list ::=   
    <PageRangeList>  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       Hash="md5-hash"/>]  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       Hash="md5-hash"/>]  
    </PageRangeList>  
  
block-list ::=  
    <BlockList>  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]  
       Hash="md5-hash"/>]  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]   
       Hash="md5-hash"/>]  
    </BlockList>  

```

## <a name="manifest-xml-elements-and-attributes"></a>Manifest elementów XML oraz atrybuty

Witaj danych elementów i atrybutów formatu XML manifestu dysku hello są określone w hello w poniższej tabeli.  
  
|XML Element|Typ|Opis|  
|-----------------|----------|-----------------|  
|`DriveManifest`|Element główny|element główny Hello hello pliku manifestu. Wszystkie elementy w pliku hello się poniżej tego elementu.|  
|`Version`|Atrybut ciągu|Wersja Hello hello pliku manifestu.|  
|`Drive`|Zagnieżdżone — element XML|Zawiera manifest powitania dla każdego dysku.|  
|`DriveId`|Ciąg|identyfikator unikatowy dysku Hello hello dysku. Identyfikator dysku Hello znaleziono badając dysku hello jego numeru seryjnego. numer seryjny dysku Hello jest zazwyczaj wydrukowany hello poza również hello dysku. Witaj `DriveID` elementu musi występować przed każdą `BlobList` elementu w pliku manifestu hello.|  
|`StorageAccountKey`|Ciąg|Wymagany dla zadania importu, jeśli, a tylko wtedy, gdy `ContainerSas` nie jest określona. klucz konta Hello hello kontem magazynu platformy Azure skojarzone z zadaniem hello.<br /><br /> Ten element został pominięty hello manifestu dla operacji eksportowania.|  
|`ContainerSas`|Ciąg|Wymagany dla zadania importu, jeśli, a tylko wtedy, gdy `StorageAccountKey` nie jest określona. kontener Hello SAS do uzyskiwania dostępu do obiektów blob hello skojarzone z zadaniem hello. Zobacz [zawiesić zadanie](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) dla jego format. Ten element został pominięty hello manifestu dla operacji eksportowania.|  
|`ClientCreator`|Ciąg|Określa powitania klienta, który utworzył hello plik XML. Ta wartość nie jest interpretowany przez hello usługi Import/Eksport.|  
|`BlobList`|Zagnieżdżone — element XML|Zawiera listę obiektów blob, które są częścią hello importu lub eksportu zadania. Każdy obiekt blob w postaci listy obiektów blob udziałów hello tych samych metadanych i właściwości.|  
|`BlobList/MetadataPath`|Ciąg|Opcjonalny. Określa ścieżkę względną hello pliku na dysku hello, który zawiera hello metadane domyślnej zostanie ustawiona na obiekty BLOB na liście hello obiektu blob dla operacji importowania. Te metadane można opcjonalnie zastąpić na podstawie obiektu blob przez obiekt blob.<br /><br /> Ten element został pominięty hello manifestu dla operacji eksportowania.|  
|`BlobList/MetadataPath/@Hash`|Atrybut ciągu|Określa wartość skrótu MD5 kodowany w formacie Base16 hello hello pliku metadanych.|  
|`BlobList/PropertiesPath`|Ciąg|Opcjonalny. Określa ścieżkę względną hello pliku na dysku hello, który zawiera właściwości domyślne hello, które zostaną ustawione na obiekty BLOB na liście hello obiektu blob dla operacji importowania. Te właściwości można opcjonalnie zastąpić na podstawie obiektu blob przez obiekt blob.<br /><br /> Ten element został pominięty hello manifestu dla operacji eksportowania.|  
|`BlobList/PropertiesPath/@Hash`|Atrybut ciągu|Określa wartość skrótu MD5 kodowany w formacie Base16 hello hello właściwości pliku.|  
|`Blob`|Zagnieżdżone — element XML|Zawiera informacje dotyczące każdego obiektu blob na wszystkich listach obiektów blob.|  
|`Blob/BlobPath`|Ciąg|Hello względny identyfikator URI toohello obiektów blob, rozpoczynające się od nazwy kontenera hello. W przypadku hello obiektów blob w kontenerze głównego, musi zaczynać się od `$root`.|  
|`Blob/FilePath`|Ciąg|Określa plik toohello ścieżki względnej hello na powitania dysku. Dla zadań eksportowania ścieżka obiektu blob hello będzie służyć do hello ścieżka pliku, jeśli jest to możliwe. *np.*, `pictures/bob/wild/desert.jpg` zostaną wyeksportowane zbyt`\pictures\bob\wild\desert.jpg`. Jednak ze względu na ograniczenia toohello nazw systemu plików NTFS, obiektu blob może być tooa wyeksportowany plik ze ścieżką nie przypominać hello ścieżka obiektu blob.|  
|`Blob/ClientData`|Ciąg|Opcjonalny. Zawiera komentarz powitania klienta. Ta wartość nie jest interpretowany przez hello usługi Import/Eksport.|  
|`Blob/Snapshot`|Data i godzina|Opcjonalny w przypadku zadań eksportu. Określa identyfikator migawki hello migawki wyeksportowany obiekt blob.|  
|`Blob/Length`|Liczba całkowita|Określa hello całkowita długość obiektu hello blob w bajtach. wartość Hello może być too200 GB dla blokowych obiektów blob i zapasowej too1 TB dla stronicowych obiektów blob. Dla stronicowych obiektów blob ta wartość musi być wielokrotnością 512.|  
|`Blob/ImportDisposition`|Ciąg|Opcjonalne dla zadania importu, pominąć w przypadku zadań eksportu. To ustawienie określa, jak hello usługi Import/Eksport powinna obsługiwać hello przypadku dla zadania importu gdzie obiektu blob z hello sam o tej nazwie już istnieje. W przypadku pominięcia tej wartości z hello importu manifestu hello wartość domyślna to `rename`.<br /><br /> Witaj wartości dla tego elementu:<br /><br /> -   `no-overwrite`: Jeśli docelowego obiektu blob jest już obecny razem z hello samą nazwę operacji importowania hello pominie importowania tego pliku.<br />-   `overwrite`: Wszystkie istniejące docelowego obiektu blob jest całkowicie zastąpiona hello nowo zaimportowany plik.<br />-   `rename`: hello nowego obiektu blob zostanie przekazany z nazwą zmodyfikowane.<br /><br /> Zmiana nazwy reguły Hello jest następujący:<br /><br /> — Jeśli hello nazwa obiektu blob nie zawiera kropkę, Nowa nazwa jest generowany przez dołączenie `(2)` toohello oryginalna nazwa obiektu blob; Jeśli ta nowa nazwa również powoduje konflikt z istniejącą nazwą obiektu blob, następnie `(3)` jest dołączany zamiast `(2)`; i tak dalej.<br />— Jeśli nazwa obiektu blob hello zawiera kropkę, część powitania po ostatniej kropka hello jest uważany za hello Nazwa rozszerzenia. Podobne toohello powyżej procedury `(2)` dodaje się przed hello ostatniego toogenerate kropka nową nazwę; Jeśli nadal hello Nowa nazwa powoduje konflikt z istniejącą nazwą obiektu blob, hello usługa próbuje `(3)`, `(4)`i tak dalej do niekolidujących znaleziono nazwy.<br /><br /> Kilka przykładów:<br /><br /> Obiekt blob Hello `BlobNameWithoutDot` zostanie zmieniona na:<br /><br /> `BlobNameWithoutDot (2)  // if BlobNameWithoutDot exists`<br /><br /> `BlobNameWithoutDot (3)  // if both BlobNameWithoutDot and BlobNameWithoutDot (2) exist`<br /><br /> Obiekt blob Hello `Seattle.jpg` zostanie zmieniona na:<br /><br /> `Seattle (2).jpg  // if Seattle.jpg exists`<br /><br /> `Seattle (3).jpg  // if both Seattle.jpg and Seattle (2).jpg exist`|  
|`PageRangeList`|Zagnieżdżone — element XML|Wymagany dla stronicowych obiektów blob.<br /><br /> Do zaimportowania operacji określa listę zakresów bajtów toobe pliku, zaimportowane. Każdy zakres stron jest opisany przez przesunięcie i długość w pliku źródłowym hello opisujący hello zakres stron, wraz z wyznaczania wartości skrótu MD5 hello regionu. Witaj `Hash` wymagany jest atrybut zakresu stron. Usługa Hello zostanie przeprowadzona Weryfikacja hello skrót danych hello w obiekcie blob hello zgodność skrótu MD5 hello obliczana z zakresu stron hello. Dowolna liczba zakresów stron może być używane toodescribe plik do zaimportowania z hello całkowity rozmiar się too1 TB. Wszystkie zakresy strony musi zostać określona przez przesunięcie, a nie nakłada się jest niedozwolone.<br /><br /> W przypadku operacji eksportowania, określa zestaw zakresów bajtów obiektu blob, które zostały wyeksportowane toohello dysku.<br /><br /> razem zakresów stron Hello może obejmować tylko zakresy podrzędne obiektów blob lub pliku.  Oczekiwano Hello pozostałej części pliku hello nie pasuje do żadnego zakresu żadnych stron i jego zawartość może być niezdefiniowana.|  
|`PageRange`|XML element|Reprezentuje zakres stron.|  
|`PageRange/@Offset`|Atrybut, liczba całkowita|Określa, że rozpoczyna przesunięcie hello w hello transferu plików i obiektów blob hello gdzie hello określony zakres stron. Ta wartość musi być wielokrotnością 512.|  
|`PageRange/@Length`|Atrybut, liczba całkowita|Określa długość hello hello strony zakresu. Ta wartość musi być wielokrotnością 512 i nie więcej niż 4 MB.|  
|`PageRange/@Hash`|Atrybut ciągu|Określa wartość skrótu MD5 kodowany w formacie Base16 hello hello zakres stron.|  
|`BlockList`|Zagnieżdżone — element XML|Wymagany w przypadku blokowego obiektu blob z nazwanym bloków.<br /><br /> Dla operacji importowania listy zablokowanych hello określa zestaw bloków, które zostaną zaimportowane do magazynu Azure. Dla operacji eksportowania listy zablokowanych hello Określa, gdzie każdy blok przechowywanych w pliku hello na powitania eksportu dysku. Każdy blok jest opisane przez przesunięcie w pliku hello i długość bloku; Każdy blok jest ponadto o nazwie atrybutu ID bloku i zawiera wyznaczania wartości skrótu MD5 hello bloku. Zapasowej too50 000 bloków mogą być używane toodescribe obiektu blob.  Wszystkie bloki muszą być uporządkowane przez przesunięcie, a jednocześnie powinno obejmować hello pełną gamę pliku hello *tj*, musi istnieć bez przerw między bloków. Jeśli obiekt blob hello jest nie więcej niż 64 MB, identyfikatory bloków hello każdy blok musi być wszystkie nieobecny lub przedstawia wszystkie. Identyfikatory bloku są wymagane toobe ciągów algorytmem Base64. Zobacz [Put bloku](/rest/api/storageservices/put-block) dodatkowe wymagania dotyczące identyfikatory bloków.|  
|`Block`|XML element|Reprezentuje blok.|  
|`Block/@Offset`|Atrybut, liczba całkowita|Określa przesunięcie hello, w którym rozpoczyna się hello określony blok.|  
|`Block/@Length`|Atrybut, liczba całkowita|Określa hello liczbę bajtów w bloku hello; Ta wartość musi być nie więcej niż 4MB.|  
|`Block/@Id`|Atrybut ciągu|Określa ciąg reprezentujący identyfikator bloku hello hello bloku.|  
|`Block/@Hash`|Atrybut ciągu|Określa Skrót MD5 kodowany w formacie Base16 hello hello bloku.|  
|`Blob/MetadataPath`|Ciąg|Opcjonalny. Określa ścieżkę względną hello pliku metadanych. Podczas importowania metadanych hello jest ustawiona na powitania docelowego obiektu blob. Podczas operacji eksportowania hello obiektów blob metadane są przechowywane w pliku metadanych hello na powitania dysku.|  
|`Blob/MetadataPath/@Hash`|Atrybut ciągu|Określa Skrót MD5 kodowany w formacie Base16 hello hello obiektów blob metadane pliku.|  
|`Blob/PropertiesPath`|Ciąg|Opcjonalny. Określa ścieżkę względną hello właściwości pliku. Podczas importowania hello właściwości są ustawione na powitania docelowego obiektu blob. Podczas operacji eksportowania hello właściwości obiektów blob są przechowywane w pliku właściwości hello na powitania dysku.|  
|`Blob/PropertiesPath/@Hash`|Atrybut ciągu|Określa Skrót MD5 kodowany w formacie Base16 hello hello blob właściwości pliku.|  
  
## <a name="next-steps"></a>Następne kroki
 
* [Interfejs API REST importu/eksportu magazynu](/rest/api/storageimportexport/)
