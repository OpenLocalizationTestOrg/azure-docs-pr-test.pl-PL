---
title: "aaaSample przepływu pracy tooprep dyski twarde dla Import/Eksport Azure Importuj zadanie - v1 | Dokumentacja firmy Microsoft"
description: "Zobacz wskazówki dla hello Zakończ proces przygotowywania dysków dla zadania importu w hello usługi Import/Eksport Azure."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 6eb1b1b7-c69f-4365-b5ef-3cd5e05eb72a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: f836fc6104d8b4ad5660cb110a62f61b40b0b7ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sample-workflow-tooprepare-hard-drives-for-an-import-job"></a>Przykładowy przepływ pracy tooprepare dysków dla zadania importu
W tym temacie przedstawiono hello Zakończ proces przygotowywania dysków dla zadania importu.  
  
W tym przykładzie importuje powitania po danych na konto magazynu Azure okna o nazwie `mystorageaccount`:  
  
|Lokalizacja|Opis|  
|--------------|-----------------|  
|H:\Video|Kolekcja filmów wideo, 5 TB w sumie.|  
|H:\Photo|Kolekcja zdjęć, 30 GB w sumie.|  
|K:\Temp\FavoriteMovie.ISO|Obraz dysku A Blu-ray™, 25 GB.|  
|\\\bigshare\john\music|Kolekcja plików muzycznych w udziale sieciowym, 10 GB w sumie.|  
  
zadania importu Hello zostaną zaimportowane te dane do następujących miejsc docelowych na koncie magazynu hello hello:  
  
|Element źródłowy|Katalog wirtualny docelowego lub obiektu blob|  
|------------|-------------------------------------------|  
|H:\Video|https://mystorageaccount.blob.Core.Windows.NET/Video|  
|H:\Photo|https://mystorageaccount.blob.Core.Windows.NET/Photo|  
|K:\Temp\FavoriteMovie.ISO|https://mystorageaccount.blob.Core.Windows.NET/favorite/FavoriteMovies.ISO|  
|\\\bigshare\john\music|https://mystorageaccount.blob.Core.Windows.NET/Music|  
  
Do tego mapowania hello pliku `H:\Video\Drama\GreatMovie.mov` będzie toohello importowanych obiektów blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.  
  
Następnie toodetermine liczbę dysków twardych są potrzebne, obliczeń hello rozmiar danych hello:  
  
`5TB + 30GB + 25GB + 10GB = 5TB + 65GB`  
  
Na przykład dwa 3TB dyski twarde powinny być wystarczające. Jednak ponieważ katalog źródłowy hello `H:\Video` ma 5TB danych i pojemności pojedynczego dysku twardego w tylko 3TB jest konieczne toobreak `H:\Video` na dwa katalogi mniejszych przed uruchomieniem hello narzędzia importu/eksportu pakietu Microsoft Azure: `H:\Video1` i `H:\Video2`. Ten krok powoduje hello następujące katalogi źródłowe:  
  
|Lokalizacja|Rozmiar|Katalog wirtualny docelowego lub obiektu blob|  
|--------------|----------|-------------------------------------------|  
|H:\Video1|2.5 TB|https://mystorageaccount.blob.Core.Windows.NET/Video|  
|H:\Video2|2.5 TB|https://mystorageaccount.blob.Core.Windows.NET/Video|  
|H:\Photo|30 GB|https://mystorageaccount.blob.Core.Windows.NET/Photo|  
|K:\Temp\FavoriteMovies.ISO|25 GB|https://mystorageaccount.blob.Core.Windows.NET/favorite/FavoriteMovies.ISO|  
|\\\bigshare\john\music|10GB|https://mystorageaccount.blob.Core.Windows.NET/Music|  
  
 Należy pamiętać, że nawet jeśli hello `H:\Video`katalogu podzielonego tootwo katalogów, wskazywały toohello sam docelowy katalog wirtualny na koncie magazynu hello. Dzięki temu wszystkie pliki wideo są obsługiwane pod jedną `video` kontenera na koncie magazynu hello.  
  
 Następnie hello powyżej źródło katalogi są równomiernie przekazany toohello dwóch dysków twardych:  
  
||||  
|-|-|-|  
|Dysk twardy|Katalogi źródłowe|Całkowity rozmiar|  
|Pierwszy dysku|H:\Video1|2,5 TB + 30 GB|  
||H:\Photo||  
|Dysku na sekundę|H:\Video2|2,5 TB + 35 GB|  
||K:\Temp\BlueRay.ISO||  
||\\\bigshare\john\music||  
  
Ponadto można ustawić hello następujące metadane dla wszystkich plików:  
  
-   **UploadMethod:** usługi Import/Eksport systemu Windows Azure  
  
-   **DataSetName:** SampleData  
  
-   **CreationDate:** 10/1/2013  
  
metadane tooset plików hello zaimportowane, Utwórz plik tekstowy `c:\WAImportExport\SampleMetadata.txt`, z hello następującej zawartości:  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>  
    <DataSetName>SampleData</DataSetName>  
    <CreationDate>10/1/2013</CreationDate>  
</Metadata>  
```
  
Można również ustawić niektórych właściwości hello `FavoriteMovie.ISO` obiektu blob:  
  
-   **Content-Type:** application/octet-stream  
  
-   **Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ ==  
  
-   **Cache-Control:** no-cache  
  
tooset te właściwości, Utwórz plik tekstowy `c:\WAImportExport\SampleProperties.txt`:  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
Teraz wszystko jest gotowe toorun hello Azure narzędzie importu/eksportu tooprepare hello dwóch dysków twardych. Należy pamiętać, że:  
  
-   Witaj pierwszego dysku jest zainstalowany jako dysku X.  
  
-   drugi dysk Hello jest zainstalowany jako dysk Y.  
  
-   Witaj klucza dla konta magazynu hello `mystorageaccount` jest `8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`.  

## <a name="preparing-disk-for-import-when-data-is-pre-loaded"></a>Przygotowywanie dysku do zaimportowania podczas wstępnego ładowania danych
 
 Jeśli zaimportowane toobe danych hello jest już obecny na powitania dysku, użyj /skipwrite flagi hello. Wartość /t i /srcdir powinny wskazywać dysku toohello przygotowanym do importu. Jeśli nie wszystkie hello danych na dysku hello musi toogo toohello tego samego katalogu wirtualnego w docelowym lub głównego konta magazynu hello, hello wykonywania polecenia takie same dla każdego katalogu oddzielnie zachowuje wartość hello/identyfikator tej samej przez wszystkie elementy.

>[!NOTE] 
>Nie określaj/format, jak go spowoduje wyczyszczenie danych hello na powitania dysku. Można określić / szyfrowania lub /bk w zależności od tego, czy dysk hello jest już zaszyfrowane lub nie. 
>

```
    When data is already present on hello disk for each drive run hello following command.
    WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:x:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt /skipwrite
```

## <a name="copy-sessions---first-drive"></a>Skopiuj sesje — najpierw dysków

Dla pierwszego dysku hello Uruchom hello Azure narzędzie importu/eksportu źródła dwukrotnie hello toocopy dwa katalogi:  

**Najpierw skopiować sesji**
  
```
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:H:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```

**Druga kopia sesji**

```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Photo /srcdir:H:\Photo /dstdir:photo/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt
```

## <a name="copy-sessions---second-drive"></a>Skopiuj sesji — w drugim dysku
 
Dla hello drugiego dysku, uruchom hello Azure narzędzie importu/eksportu trzy razy, po wszystkich hello źródła katalogów i raz dla autonomicznej hello Blu-Ray™ pliku obrazu):  
  
**Najpierw skopiować sesji** 

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Video2 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:y /format /encrypt /srcdir:H:\Video2 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```
  
**Druga kopia sesji**

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Music /srcdir:\\bigshare\john\music /dstdir:music/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```  
  
**Trzeci sesji kopiowania**  

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```

## <a name="copy-session-completion"></a>Skopiuj zakończenia sesji

Po hello kopiowania sesji została ukończona, można odłączyć Witaj dwie stacje z komputera kopiowania hello i wysłać je toohello odpowiednie centrum danych systemu Windows Azure. Będzie przekazać hello dwa pliki dziennika, `FirstDrive.jrn` i `SecondDrive.jrn`, podczas tworzenia zadania importu hello w hello [portalu zarządzania pakietu Windows Azure](https://manage.windowsazure.com/).  
  
## <a name="next-steps"></a>Następne kroki

* [Przygotowywanie dysków twardych do zadania importu](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [Krótki przewodnik dla często używanych poleceń](storage-import-export-tool-quick-reference-v1.md) 
