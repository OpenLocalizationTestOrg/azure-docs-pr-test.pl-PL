---
title: "aaaSample przepływu pracy tooprep dyski twarde dla Import/Eksport Azure Importuj zadanie | Dokumentacja firmy Microsoft"
description: "Zobacz wskazówki dla hello Zakończ proces przygotowywania dysków dla zadania importu w hello usługi Import/Eksport Azure."
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
ms.date: 04/07/2017
ms.author: muralikk
ms.openlocfilehash: fa7f36300b35b81757523de4960fd583bd4bf305
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sample-workflow-tooprepare-hard-drives-for-an-import-job"></a>Przykładowy przepływ pracy tooprepare dysków dla zadania importu

W tym artykule przedstawiono hello Zakończ proces przygotowywania dysków dla zadania importu.

## <a name="sample-data"></a>Dane przykładowe

W tym przykładzie importuje powitania po danych do konta magazynu platformy Azure o nazwie `mystorageaccount`:

|Lokalizacja|Opis|Rozmiar danych|
|--------------|-----------------|-----|
|H:\Video\ |Kolekcja filmów wideo|12 TB|
|H:\Photo\ |Kolekcja zdjęć|30 GB|
|K:\Temp\FavoriteMovie.ISO|Obraz dysku A Blu-ray™|25 GB|
|\\\bigshare\john\music\|Kolekcja plików muzycznych w udziale sieciowym|10 GB|

## <a name="storage-account-destinations"></a>Miejsca docelowe konto magazynu

zadania importu Hello zostaną zaimportowane hello danych do następujących miejsc docelowych na koncie magazynu hello hello:

|Element źródłowy|Katalog wirtualny docelowego lub obiektu blob|
|------------|-------------------------------------------|
|H:\Video\ |wideo /|
|H:\Photo\ |zdjęcie /|
|K:\Temp\FavoriteMovie.ISO|favorite/FavoriteMovies.ISO|
|\\\bigshare\john\music\ |Muzyka|

Do tego mapowania hello pliku `H:\Video\Drama\GreatMovie.mov` będzie toohello importowanych obiektów blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.

## <a name="determine-hard-drive-requirements"></a>Określenie wymagań dotyczących dysku twardego

Następnie toodetermine liczbę dysków twardych są potrzebne, obliczeń hello rozmiar danych hello:

`12TB + 30GB + 25GB + 10GB = 12TB + 65GB`

Na przykład dwa 8TB dyski twarde powinny być wystarczające. Jednak ponieważ katalog źródłowy hello `H:\Video` ma 12TB danych i pojemności pojedynczego dysku twardego w tylko 8TB, będziesz w stanie toospecify to w hello w następujący sposób w hello **driveset.csv** pliku:

```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
X,Format,SilentMode,Encrypt,
Y,Format,SilentMode,Encrypt,
```
Narzędzie Hello będzie rozpowszechniają danych dwóch dysków twardych w sposób zoptymalizowane.

## <a name="attach-drives-and-configure-hello-job"></a>Dołącz dysków i skonfigurować zadanie hello
Zostanie Dołącz zarówno maszyny toohello dysków i tworzyć woluminów. Następnie tworzyć **dataset.csv** pliku:
```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

Ponadto można ustawić hello następujące metadane dla wszystkich plików:

* **UploadMethod:** usługi Import/Eksport systemu Windows Azure
* **DataSetName:** SampleData
* **CreationDate:** 10/1/2013

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

* **Content-Type:** application/octet-stream
* **Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ ==
* **Cache-Control:** no-cache

tooset te właściwości, Utwórz plik tekstowy `c:\WAImportExport\SampleProperties.txt`:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

## <a name="run-hello-azure-importexport-tool-waimportexportexe"></a>Uruchom hello Azure narzędzie importu/eksportu (WAImportExport.exe)

Teraz wszystko jest gotowe toorun hello Azure narzędzie importu/eksportu tooprepare hello dwóch dysków twardych.

**Dla hello pierwszej sesji:**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

Jeśli więcej danych wymaga toobe dodany, należy utworzyć inny plik zestawu danych (tego samego formatu co Initialdataset).

**Dla hello drugiej sesji:**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

Po hello kopiowania sesji została ukończona, można odłączyć Witaj dwie stacje z komputera kopiowania hello i wysłać je toohello centrum danych Azure. Będzie przekazać hello dwa pliki dziennika, `<FirstDriveSerialNumber>.xml` i `<SecondDriveSerialNumber>.xml`, podczas tworzenia zadania importu hello w hello portalu Azure.

## <a name="next-steps"></a>Następne kroki

* [Przygotowywanie dysków twardych do zadania importu](../storage-import-export-tool-preparing-hard-drives-import.md)
* [Krótki przewodnik dla często używanych poleceń](../storage-import-export-tool-quick-reference.md)
