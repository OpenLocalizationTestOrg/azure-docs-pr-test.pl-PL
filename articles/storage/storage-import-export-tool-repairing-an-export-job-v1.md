---
title: Naprawianie zadania eksportu Import/Eksport Azure - v1 | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak naprawić zadanie eksportu, który został utworzony i uruchamiany za pomocą usługi Import/Eksport Azure."
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
ms.openlocfilehash: 30ca0f8d06cb1927c19e66035ff485db0fc09e5a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="repairing-an-export-job"></a><span data-ttu-id="0556f-103">Naprawianie zadania eksportu</span><span class="sxs-lookup"><span data-stu-id="0556f-103">Repairing an export job</span></span>
<span data-ttu-id="0556f-104">Po zakończeniu zadania eksportu, możesz uruchomić narzędzie importu/eksportu pakietu Microsoft Azure lokalnej do:</span><span class="sxs-lookup"><span data-stu-id="0556f-104">After an export job has completed, you can run the Microsoft Azure Import/Export Tool on-premises to:</span></span>  
  
1.  <span data-ttu-id="0556f-105">Pobierz wszystkie pliki, które usługi Import/Eksport Azure nie mógł wyeksportować.</span><span class="sxs-lookup"><span data-stu-id="0556f-105">Download any files that the Azure Import/Export service was unable to export.</span></span>  
  
2.  <span data-ttu-id="0556f-106">Sprawdź, czy zostały poprawnie wyeksportowane pliki na dysku.</span><span class="sxs-lookup"><span data-stu-id="0556f-106">Validate that the files on the drive were correctly exported.</span></span>  
  
<span data-ttu-id="0556f-107">Musisz mieć połączenie z magazynem Azure, aby używać tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="0556f-107">You must have connectivity to Azure Storage to use this functionality.</span></span>  
  
<span data-ttu-id="0556f-108">Polecenie naprawy zadania importu jest **RepairExport**.</span><span class="sxs-lookup"><span data-stu-id="0556f-108">The command for repairing an import job is **RepairExport**.</span></span>

## <a name="repairexport-parameters"></a><span data-ttu-id="0556f-109">Parametry RepairExport</span><span class="sxs-lookup"><span data-stu-id="0556f-109">RepairExport parameters</span></span>

<span data-ttu-id="0556f-110">Można określić następujące parametry z **RepairExport**:</span><span class="sxs-lookup"><span data-stu-id="0556f-110">The following parameters can be specified with **RepairExport**:</span></span>  
  
|<span data-ttu-id="0556f-111">Parametr</span><span class="sxs-lookup"><span data-stu-id="0556f-111">Parameter</span></span>|<span data-ttu-id="0556f-112">Opis</span><span class="sxs-lookup"><span data-stu-id="0556f-112">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="0556f-113">**/ r: < RepairFile\>**</span><span class="sxs-lookup"><span data-stu-id="0556f-113">**/r:<RepairFile\>**</span></span>|<span data-ttu-id="0556f-114">Wymagane.</span><span class="sxs-lookup"><span data-stu-id="0556f-114">Required.</span></span> <span data-ttu-id="0556f-115">Ścieżka do pliku naprawy, który śledzi postęp naprawy i umożliwia wznowienie naprawę przerwania.</span><span class="sxs-lookup"><span data-stu-id="0556f-115">Path to the repair file, which tracks the progress of the repair, and allows you to resume an interrupted repair.</span></span> <span data-ttu-id="0556f-116">Każdy dysk musi mieć jeden i tylko jeden plik naprawy.</span><span class="sxs-lookup"><span data-stu-id="0556f-116">Each drive must have one and only one repair file.</span></span> <span data-ttu-id="0556f-117">Po uruchomieniu naprawy dla danego dysku zostaną spełnione w ścieżce do pliku naprawy, które jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="0556f-117">When you start a repair for a given drive, you will pass in the path to a repair file which does not yet exist.</span></span> <span data-ttu-id="0556f-118">Aby wznowić naprawę przerwania, należy przekazać nazwę istniejącego pliku naprawy.</span><span class="sxs-lookup"><span data-stu-id="0556f-118">To resume an interrupted repair, you should pass in the name of an existing repair file.</span></span> <span data-ttu-id="0556f-119">Zawsze należy określać plik naprawy odpowiadający dysk docelowy.</span><span class="sxs-lookup"><span data-stu-id="0556f-119">The repair file corresponding to the target drive must always be specified.</span></span>|  
|<span data-ttu-id="0556f-120">**/ logdir: < LogDirectory\>**</span><span class="sxs-lookup"><span data-stu-id="0556f-120">**/logdir:<LogDirectory\>**</span></span>|<span data-ttu-id="0556f-121">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="0556f-121">Optional.</span></span> <span data-ttu-id="0556f-122">Katalog dziennika.</span><span class="sxs-lookup"><span data-stu-id="0556f-122">The log directory.</span></span> <span data-ttu-id="0556f-123">Plików pełnego dziennika zostanie zapisany do tego katalogu.</span><span class="sxs-lookup"><span data-stu-id="0556f-123">Verbose log files will be written to this directory.</span></span> <span data-ttu-id="0556f-124">Jeśli katalog dziennika nie jest określony, bieżący katalog będzie używany jako katalog dziennika.</span><span class="sxs-lookup"><span data-stu-id="0556f-124">If no log directory is specified, the current directory will be used as the log directory.</span></span>|  
|<span data-ttu-id="0556f-125">**/ d: < TargetDirectory\>**</span><span class="sxs-lookup"><span data-stu-id="0556f-125">**/d:<TargetDirectory\>**</span></span>|<span data-ttu-id="0556f-126">Wymagane.</span><span class="sxs-lookup"><span data-stu-id="0556f-126">Required.</span></span> <span data-ttu-id="0556f-127">Katalog do sprawdzania poprawności i napraw.</span><span class="sxs-lookup"><span data-stu-id="0556f-127">The directory to validate and repair.</span></span> <span data-ttu-id="0556f-128">Zazwyczaj jest to katalog główny dysku eksportu, ale może też być sieciowego udziału plików zawierający kopię wyeksportowane pliki.</span><span class="sxs-lookup"><span data-stu-id="0556f-128">This is usually the root directory of the export drive, but could also be a network file share containing a copy of the exported files.</span></span>|  
|<span data-ttu-id="0556f-129">**/BK: < BitLockerKey\>**</span><span class="sxs-lookup"><span data-stu-id="0556f-129">**/bk:<BitLockerKey\>**</span></span>|<span data-ttu-id="0556f-130">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="0556f-130">Optional.</span></span> <span data-ttu-id="0556f-131">Należy określić klucza funkcji BitLocker, jeśli chcesz użyć narzędzia, aby odblokować zaszyfrowany, gdzie znajdują się wyeksportowane pliki.</span><span class="sxs-lookup"><span data-stu-id="0556f-131">You should specify the BitLocker key if you want the tool to unlock an encrypted where the exported files are stored.</span></span>|  
|<span data-ttu-id="0556f-132">**/SN: < StorageAccountName\>**</span><span class="sxs-lookup"><span data-stu-id="0556f-132">**/sn:<StorageAccountName\>**</span></span>|<span data-ttu-id="0556f-133">Wymagane.</span><span class="sxs-lookup"><span data-stu-id="0556f-133">Required.</span></span> <span data-ttu-id="0556f-134">Nazwa konta magazynu dla zadania eksportu.</span><span class="sxs-lookup"><span data-stu-id="0556f-134">The name of the storage account for the export job.</span></span>|  
|<span data-ttu-id="0556f-135">**/SK: < StorageAccountKey\>**</span><span class="sxs-lookup"><span data-stu-id="0556f-135">**/sk:<StorageAccountKey\>**</span></span>|<span data-ttu-id="0556f-136">**Wymagane** tylko wtedy, gdy nie określono kontenera sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="0556f-136">**Required** if and only if a container SAS is not specified.</span></span> <span data-ttu-id="0556f-137">Klucz konta dla konta magazynu dla zadania eksportu.</span><span class="sxs-lookup"><span data-stu-id="0556f-137">The account key for the storage account for the export job.</span></span>|  
|<span data-ttu-id="0556f-138">**/csas: < ContainerSas\>**</span><span class="sxs-lookup"><span data-stu-id="0556f-138">**/csas:<ContainerSas\>**</span></span>|<span data-ttu-id="0556f-139">**Wymagane** tylko wtedy, gdy nie określono klucza konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="0556f-139">**Required** if and only if the storage account key is not specified.</span></span> <span data-ttu-id="0556f-140">Kontener SAS do uzyskiwania dostępu do obiektów blob skojarzony z zadaniem eksportu.</span><span class="sxs-lookup"><span data-stu-id="0556f-140">The container SAS for accessing the blobs associated with the export job.</span></span>|  
|<span data-ttu-id="0556f-141">**/ CopyLogFile: < DriveCopyLogFile\>**</span><span class="sxs-lookup"><span data-stu-id="0556f-141">**/CopyLogFile:<DriveCopyLogFile\>**</span></span>|<span data-ttu-id="0556f-142">Wymagane.</span><span class="sxs-lookup"><span data-stu-id="0556f-142">Required.</span></span> <span data-ttu-id="0556f-143">Ścieżka do pliku dziennika kopii dysku.</span><span class="sxs-lookup"><span data-stu-id="0556f-143">The path to the drive copy log file.</span></span> <span data-ttu-id="0556f-144">Plik jest generowany przez usługę Windows Azure importu/eksportu i można pobrać z magazynu obiektów blob, skojarzone z zadaniem.</span><span class="sxs-lookup"><span data-stu-id="0556f-144">The file is generated by the Windows Azure Import/Export service and can be downloaded from the blob storage associated with the job.</span></span> <span data-ttu-id="0556f-145">Kopiuj plik dziennika zawiera informacje dotyczące obiektów blob nie powiodło się lub pliki, które mają zostać naprawione.</span><span class="sxs-lookup"><span data-stu-id="0556f-145">The copy log file contains information about failed blobs or files which are to be repaired.</span></span>|  
|<span data-ttu-id="0556f-146">**/ ManifestFile: < DriveManifestFile\>**</span><span class="sxs-lookup"><span data-stu-id="0556f-146">**/ManifestFile:<DriveManifestFile\>**</span></span>|<span data-ttu-id="0556f-147">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="0556f-147">Optional.</span></span> <span data-ttu-id="0556f-148">Ścieżka do pliku manifestu dysku eksportu.</span><span class="sxs-lookup"><span data-stu-id="0556f-148">The path to the export drive's manifest file.</span></span> <span data-ttu-id="0556f-149">Ten plik jest generowany przez usługę Windows Azure importu/eksportu i przechowywane na dysku eksportu, a opcjonalnie w obiekcie blob na koncie magazynu skojarzone z zadaniem.</span><span class="sxs-lookup"><span data-stu-id="0556f-149">This file is generated by the Windows Azure Import/Export service and stored on the export drive, and optionally in a blob in the storage account associated with the job.</span></span><br /><br /> <span data-ttu-id="0556f-150">Zawartość plików na dysku eksportu zostaną zweryfikowane wartości skrótu MD5 zawarte w tym pliku.</span><span class="sxs-lookup"><span data-stu-id="0556f-150">The content of the files on the export drive will be verified with the MD5 hashes contained in this file.</span></span> <span data-ttu-id="0556f-151">Wszystkie pliki, które są określane uszkodzone zostanie pobrany i ulegną do katalogów docelowych.</span><span class="sxs-lookup"><span data-stu-id="0556f-151">Any files that are determined to be corrupted will be downloaded and rewritten to the target directories.</span></span>|  
  
## <a name="using-repairexport-mode-to-correct-failed-exports"></a><span data-ttu-id="0556f-152">Aby rozwiązać eksportowanie nie powiodło się w trybie RepairExport</span><span class="sxs-lookup"><span data-stu-id="0556f-152">Using RepairExport mode to correct failed exports</span></span>  
<span data-ttu-id="0556f-153">Narzędzie importu/eksportu Azure służy do pobierania plików, których nie można wyeksportować.</span><span class="sxs-lookup"><span data-stu-id="0556f-153">You can use the Azure Import/Export Tool to download files that failed to export.</span></span> <span data-ttu-id="0556f-154">Kopiuj plik dziennika będzie zawierać listę plików, których nie można wyeksportować.</span><span class="sxs-lookup"><span data-stu-id="0556f-154">The copy log file will contain a list of files that failed to export.</span></span>  
  
<span data-ttu-id="0556f-155">Przyczyny niepowodzeń eksportu obejmują następujące możliwości:</span><span class="sxs-lookup"><span data-stu-id="0556f-155">The causes of export failures include the following possibilities:</span></span>  
  
-   <span data-ttu-id="0556f-156">Uszkodzone dyski</span><span class="sxs-lookup"><span data-stu-id="0556f-156">Damaged drives</span></span>  
  
-   <span data-ttu-id="0556f-157">Klucz konta magazynu została zmieniona w trakcie procesu transferu</span><span class="sxs-lookup"><span data-stu-id="0556f-157">The storage account key changed during the transfer process</span></span>  
  
<span data-ttu-id="0556f-158">Aby uruchomić narzędzie **RepairExport** trybie, należy najpierw połączyć dysk zawierający wyeksportowane pliki na komputerze.</span><span class="sxs-lookup"><span data-stu-id="0556f-158">To run the tool in **RepairExport** mode, you first need to connect the drive containing the exported files to your computer.</span></span> <span data-ttu-id="0556f-159">Następnie uruchom narzędzie importu/eksportu Azure, podając ścieżkę do tego dysku z `/d` parametru.</span><span class="sxs-lookup"><span data-stu-id="0556f-159">Next, run the Azure Import/Export Tool, specifying the path to that drive with the `/d` parameter.</span></span> <span data-ttu-id="0556f-160">Należy również określić ścieżkę do pliku dziennika kopii dysku pobranego.</span><span class="sxs-lookup"><span data-stu-id="0556f-160">You also need to specify the path to the drive's copy log file that you downloaded.</span></span> <span data-ttu-id="0556f-161">W poniższym przykładzie wiersza polecenia, poniżej uruchamiane narzędzie, aby naprawić wszystkie pliki, które nie można wyeksportować:</span><span class="sxs-lookup"><span data-stu-id="0556f-161">The following command line example below runs the tool to repair any files that failed to export:</span></span>  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log  
```  
  
<span data-ttu-id="0556f-162">Poniżej znajduje się przykład kopii pliku dziennika, który zawiera ten jeden blok w obiekcie blob nie można wyeksportować:</span><span class="sxs-lookup"><span data-stu-id="0556f-162">The following is an example of a copy log file that shows that one block in the blob failed to export:</span></span>  
  
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
  
<span data-ttu-id="0556f-163">Kopiuj plik dziennika wskazuje, że wystąpił błąd podczas usługi Import/Eksport systemu Windows Azure została pobierania jedną bloków blob do pliku na dysku eksportu.</span><span class="sxs-lookup"><span data-stu-id="0556f-163">The copy log file indicates that a failure occurred while the Windows Azure Import/Export service was downloading one of the blob's blocks to the file on the export drive.</span></span> <span data-ttu-id="0556f-164">Inne składniki pliku pobrane pomyślnie, a długość pliku została poprawnie ustawiona.</span><span class="sxs-lookup"><span data-stu-id="0556f-164">The other components of the file downloaded successfully, and the file length was correctly set.</span></span> <span data-ttu-id="0556f-165">W takim przypadku narzędzie będzie Otwórz plik na dysku, Pobierz bloku z konta magazynu i zapisz je w zakresie pliku, zaczynając od przesunięcia 65536 o długości 65536.</span><span class="sxs-lookup"><span data-stu-id="0556f-165">In this case, the tool will open the file on the drive, download the block from the storage account, and write it to the file range starting from offset 65536 with length 65536.</span></span>  
  
## <a name="using-repairexport-to-validate-drive-contents"></a><span data-ttu-id="0556f-166">Aby sprawdzić poprawność zawartości dysku przy użyciu RepairExport</span><span class="sxs-lookup"><span data-stu-id="0556f-166">Using RepairExport to validate drive contents</span></span>  
<span data-ttu-id="0556f-167">Można również użyć Import/Eksport Azure z **RepairExport** opcję, aby sprawdzić poprawność zawartości na dysku są poprawne.</span><span class="sxs-lookup"><span data-stu-id="0556f-167">You can also use Azure Import/Export with the **RepairExport** option to validate the contents on the drive are correct.</span></span> <span data-ttu-id="0556f-168">Plik manifestu na każdym dysku eksportu zawiera MD5s zawartość dysku.</span><span class="sxs-lookup"><span data-stu-id="0556f-168">The manifest file on each export drive contains MD5s for the contents of the drive.</span></span>  
  
<span data-ttu-id="0556f-169">Usługa Import/Eksport Azure można także zapisać pliki manifestu do konta magazynu podczas procesu eksportowania.</span><span class="sxs-lookup"><span data-stu-id="0556f-169">The Azure Import/Export service can also save the manifest files to a storage account during the export process.</span></span> <span data-ttu-id="0556f-170">Lokalizacja pliku manifestu jest dostępna za pośrednictwem [pobrania zadania](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operacji po ukończeniu zadania.</span><span class="sxs-lookup"><span data-stu-id="0556f-170">The location of the manifest files is available via the [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation when the job has completed.</span></span> <span data-ttu-id="0556f-171">Zobacz [usługi Import/Eksport Format pliku manifestu](storage-import-export-file-format-metadata-and-properties.md) Aby uzyskać więcej informacji o formacie pliku manifestu dysku.</span><span class="sxs-lookup"><span data-stu-id="0556f-171">See [Import/Export service Manifest File Format](storage-import-export-file-format-metadata-and-properties.md) for more information about the format of a drive manifest file.</span></span>  
  
<span data-ttu-id="0556f-172">Poniższy przykład pokazuje, jak uruchomić narzędzie importu/eksportu Azure z **/ManifestFile** i **/CopyLogFile** parametry:</span><span class="sxs-lookup"><span data-stu-id="0556f-172">The following example shows how to run the Azure Import/Export Tool with the **/ManifestFile** and **/CopyLogFile** parameters:</span></span>  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log /ManifestFile:G:\9WM35C3U.manifest  
```  
  
<span data-ttu-id="0556f-173">Poniżej przedstawiono przykładowy plik manifestu:</span><span class="sxs-lookup"><span data-stu-id="0556f-173">The following is an example of a manifest file:</span></span>  
  
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
  
<span data-ttu-id="0556f-174">Po zakończeniu procesu naprawy, narzędzie zapoznaj się z artykułem każdego pliku, do którego odwołuje się plik manifestu i zweryfikować integralność plików z wartości skrótu MD5.</span><span class="sxs-lookup"><span data-stu-id="0556f-174">After finishing the repair process, the tool will read through each file referenced in the manifest file and verify the file's integrity with the MD5 hashes.</span></span> <span data-ttu-id="0556f-175">Dla manifest powyżej przechodzą przez następujące składniki.</span><span class="sxs-lookup"><span data-stu-id="0556f-175">For the manifest above, it will go through the following components.</span></span>  

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

<span data-ttu-id="0556f-176">Dowolny składnik Niepowodzenie weryfikacji zostanie pobrana przez narzędzie i ponownie zapisać do tego samego pliku na dysku.</span><span class="sxs-lookup"><span data-stu-id="0556f-176">Any component failing the verification will be downloaded by the tool and rewritten to the same file on the drive.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="0556f-177">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0556f-177">Next steps</span></span>
 
* [<span data-ttu-id="0556f-178">Trwa konfigurowanie narzędzia Azure Import/Eksport</span><span class="sxs-lookup"><span data-stu-id="0556f-178">Setting Up the Azure Import/Export Tool</span></span>](storage-import-export-tool-setup-v1.md)   
* [<span data-ttu-id="0556f-179">Przygotowywanie dysków twardych do zadania importu</span><span class="sxs-lookup"><span data-stu-id="0556f-179">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="0556f-180">Sprawdzanie stanu zadania za pomocą plików dziennika kopiowania</span><span class="sxs-lookup"><span data-stu-id="0556f-180">Reviewing job status with copy log files</span></span>](storage-import-export-tool-reviewing-job-status-v1.md)   
* [<span data-ttu-id="0556f-181">Naprawianie zadania importu</span><span class="sxs-lookup"><span data-stu-id="0556f-181">Repairing an import job</span></span>](storage-import-export-tool-repairing-an-import-job-v1.md)   
* [<span data-ttu-id="0556f-182">Rozwiązywanie problemów z narzędziem Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="0556f-182">Troubleshooting the Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
