---
title: "aaaSetting się hello Azure narzędzie importu/eksportu | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooset się hello dysków przygotowania i narzędzia do naprawy hello usługi Import/Eksport Azure."
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
ms.date: 06/29/2017
ms.author: muralikk
ms.openlocfilehash: ee5bb99bd84ea5ee2f6b6e99c5a375b215e94ea8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-hello-azure-importexport-tool"></a>Konfigurowanie hello Azure narzędzie importu/eksportu

Witaj narzędzia importu/eksportu pakietu Microsoft Azure jest przygotowanie stacji hello i narzędzia do naprawy używanej w hello usługi Import/Eksport Microsoft Azure. Narzędzie hello na powitania następujące funkcje:

* Przed utworzeniem zadania importu, można użyć tego narzędzia toocopy danych toohello dyski twarde ma centrum danych Azure tooan tooship.
* Po zakończeniu zadania importu można toorepair to narzędzie żadnych obiektów blob, które zostały uszkodzone, brakuje lub konflikt z innymi obiektami blob.
* Po otrzymaniu hello dysków z zadania eksportu ukończone, można użyć toorepair tego narzędzia, wszystkie pliki, które zostały uszkodzone lub brakujące na dyskach hello.

## <a name="prerequisites"></a>Wymagania wstępne

Jeśli jesteś **przygotowywania dysków** dla zadania importu, muszą być spełnione następujące wymagania wstępne hello:

* Musi mieć aktywną subskrypcją platformy Azure.
* Subskrypcja musi zawierać konto magazynu z plikami hello toostore za mało dostępnego miejsca ma tooimport.
* Należy co najmniej jeden z kluczy dostępu do konta magazynu hello.
* Potrzebny jest komputer (hello "urządzenie") z systemu Windows 7, Windows Server 2008 R2 lub nowszego systemu operacyjnego Windows zainstalowana.
* Witaj .NET Framework 4 musi być zainstalowany na maszynie kopiowania hello.
* Na powitania kopiowania maszyny musi być włączona funkcja BitLocker.
* Potrzebna jest jedna lub więcej pusty 3.5 cala dysków twardych SATA połączone toohello kopiowania maszyny.
* Planowanie tooimport pliki Hello musi być dostępny z maszyny kopiowania hello, czy znajdują się w udziale sieciowym lub na lokalnym dysku twardym.

Jeśli próbujesz zbyt**napraw importowanie** który częściowo nie powiodła się, należy:

* Witaj kopiowania plików dziennika
* klucz konta magazynu Hello

Jeśli próbujesz zbyt**naprawy export** który częściowo nie powiodła się, należy:

* Witaj kopiowania plików dziennika
* pliki manifestu Hello (opcjonalnie)
* klucz konta magazynu Hello

## <a name="installing-hello-azure-importexport-tool"></a>Instalowanie hello Azure narzędzie importu/eksportu

Najpierw [Pobierz hello Azure narzędzie importu/eksportu](https://www.microsoft.com/download/details.aspx?id=55280) i wyodrębnij go tooa katalogu na komputerze, na przykład `c:\WAImportExport`.

Narzędzie importu/eksportu Azure Hello składa się z hello następujące pliki:

* DataSet.csv
* driveset.csv
* hddid.dll
* Microsoft.Data.Services.Client.dll
* Microsoft.WindowsAzure.Storage.dll
* Microsoft.WindowsAzure.Storage.pdb
* Microsoft.WindowsAzure.Storage.xml
* WAImportExport.exe
* WAImportExport.exe.config
* WAImportExport.pdb
* WAImportExportCore.dll
* WAImportExportCore.pdb
* WAImportExportRepair.dll
* WAImportExportRepair.pdb

Następnie otwórz okno wiersza polecenia w **trybu administratora**, i zmian w katalogu hello zawierającego hello wyodrębnione pliki.

toooutput pomocy dla polecenia hello, uruchom narzędzie hello (`WAImportExport.exe`) bez parametrów:

```
WAImportExport, a client tool for Windows Azure Import/Export Service. Microsoft (c) 2013


Copy directories and/or files with a new copy session:
    WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> [/logdir:<LogDirectory>]
        [/sk:<StorageAccountKey>] [/silentmode] [/InitialDriveSet:<driveset.csv>]
        DataSet:<dataset.csv>

Add more drives:
    WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /AdditionalDriveSet:<driveset.csv>

Abort an interrupted copy session:
    WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /AbortSession

Resume an interrupted copy session:
    WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /ResumeSession

List drives:
    WAImportExport.exe PrepImport /j:<JournalFile> /ListDrives

List copy sessions:
    WAImportExport.exe PrepImport /j:<JournalFile> /ListCopySessions

Repair a Drive:
    WAImportExport.exe RepairImport | RepairExport
        /r:<RepairFile> [/logdir:<LogDirectory>]
        [/d:<TargetDirectories>] [/bk:<BitLockerKey>]
        /sn:<StorageAccountName> /sk:<StorageAccountKey>
        [/CopyLogFile:<DriveCopyLogFile>] [/ManifestFile:<DriveManifestFile>]
        [/PathMapFile:<DrivePathMapFile>]

Preview an Export Job:
    WAImportExport.exe PreviewExport
        [/logdir:<LogDirectory>]
        /sn:<StorageAccountName> /sk:<StorageAccountKey>
        /ExportBlobListFile:<ExportBlobListFile> /DriveSize:<DriveSize>

Parameters:

    /j:<JournalFile>
        - Required. Path toohello journal file. A journal file tracks a set of drives and
          records hello progress in preparing these drives. hello journal file must always
          be specified.
    /logdir:<LogDirectory>
        - Optional. hello log directory. Verbose log files as well as some temporary
          files will be written toothis directory. If not specified, current directory
          will be used as hello log directory. hello log directory can be specified only
          once for hello same journal file.
    /id:<SessionId>
        - Optional. hello session Id is used tooidentify a copy session. It is used to
          ensure accurate recovery of an interrupted copy session.
    /ResumeSession
        - Optional. If hello last copy session was terminated abnormally, this parameter
          can be specified tooresume hello session.
    /AbortSession
        - Optional. If hello last copy session was terminated abnormally, this parameter
          can be specified tooabort hello session.
    /sn:<StorageAccountName>
        - Required. Only applicable for RepairImport and RepairExport. hello name of
          hello storage account.
    /sk:<StorageAccountKey>
        - Required. hello key of hello storage account.
    /InitialDriveSet:<driveset.csv>
        - Required. A .csv file that contains a list of drives tooprepare.
    /AdditionalDriveSet:<driveset.csv>
        - Required. A .csv file that contains a list of additional drives toobe added.
    /r:<RepairFile>
        - Required. Only applicable for RepairImport and RepairExport.
          Path toohello file for tracking repair progress. Each drive must have one
          and only one repair file.
    /d:<TargetDirectories>
        - Required. Only applicable for RepairImport and RepairExport.
          For RepairImport, one or more semicolon-separated directories toorepair;
          For RepairExport, one directory toorepair, e.g. root directory of hello drive.
    /CopyLogFile:<DriveCopyLogFile>
        - Required. Only applicable for RepairImport and RepairExport. Path toothe
          drive copy log file (verbose or error).
    /ManifestFile:<DriveManifestFile>
        - Required. Only applicable for RepairExport. Path toohello drive manifest file.
    /PathMapFile:<DrivePathMapFile>
        - Optional. Only applicable for RepairImport. Path toohello file containing
          mappings of file paths relative toohello drive root toolocations of actual files
          (tab-delimited). When first specified, it will be populated with file paths
          with empty targets, which means either they are not found in TargetDirectories,
          access denied, with invalid name, or they exist in multiple directories. The
          path map file can be manually edited tooinclude hello correct target paths and
          specified again for hello tool tooresolve hello file paths correctly.
    /ExportBlobListFile:<ExportBlobListFile>
        - Required. Path toohello XML file containing list of blob paths or blob path
          prefixes for hello blobs toobe exported. hello file format is hello same as the
          blob list blob format in hello Put Job operation of hello Import/Export Service
          REST API.
    /DriveSize:<DriveSize>
        - Required. Size of drives toobe used for export. For example, 500GB, 1.5TB.
          Note: 1 GB = 1,000,000,000 bytes
                1 TB = 1,000,000,000,000 bytes
    /DataSet:<dataset.csv>
        - Required. A .csv file that contains a list of directories and/or a list files
          toobe copied tootarget drives.

    /silentmode
        - Optional. If not specified, it will remind you hello requirement of drives and
          need your confirmation toocontinue.

Examples:

    Copy a data set tooa drive:
    WAImportExport.exe PrepImport
        /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GEL
        xmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /InitialDriveSet:driveset1.csv
        /DataSet:data.csv

    Copy another dataset toohello same drive following hello above command:
    WAImportExport.exe PrepImport /j:9WM35C2V.jrn /id:session#2 /DataSet:dataset2.csv

    Preview how many 1.5 TB drives are needed for an export job:
    WAImportExport.exe PreviewExport
        /sn:mytestaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7K
        ysbbeKLDksg7VoN1W/a5UuM2zNgQ== /ExportBlobListFile:C:\temp\myexportbloblist.xml
        /DriveSize:1.5TB

    Repair an finished import job:
    WAImportExport.exe RepairImport
        /r:9WM35C2V.rep /d:X:\ /bk:442926-020713-108086-436744-137335-435358-242242-2795
        98 /sn:mytestaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94
        f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\temp\9WM35C2V_error.log
```

## <a name="next-steps"></a>Następne kroki

* [Przygotowywanie dysków twardych do zadania importu](storage-import-export-tool-preparing-hard-drives-import.md)
* [Wyświetlanie podglądu użycia dysków przez zadanie eksportu](storage-import-export-tool-previewing-drive-usage-export-v1.md)
* [Sprawdzanie stanu zadania za pomocą plików dziennika kopiowania](storage-import-export-tool-reviewing-job-status-v1.md)
* [Naprawianie zadania importu](storage-import-export-tool-repairing-an-import-job-v1.md)
* [Naprawianie zadania eksportu](storage-import-export-tool-repairing-an-export-job-v1.md)
* [Rozwiązywanie problemów z hello Azure narzędzie importu/eksportu](storage-import-export-tool-troubleshooting-v1.md)
