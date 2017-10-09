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
# <a name="repairing-an-export-job"></a><span data-ttu-id="13ebb-103">Naprawianie zadania eksportu</span><span class="sxs-lookup"><span data-stu-id="13ebb-103">Repairing an export job</span></span>
<span data-ttu-id="13ebb-104">Po zakończeniu zadania eksportu, możesz uruchomić narzędzie importu/eksportu pakietu Microsoft Azure lokalne powitania:</span><span class="sxs-lookup"><span data-stu-id="13ebb-104">After an export job has completed, you can run hello Microsoft Azure Import/Export Tool on-premises to:</span></span>  
  
1.  <span data-ttu-id="13ebb-105">Pobierz wszystkie pliki, że usługa Import/Eksport Azure hello nie tooexport.</span><span class="sxs-lookup"><span data-stu-id="13ebb-105">Download any files that hello Azure Import/Export service was unable tooexport.</span></span>  
  
2.  <span data-ttu-id="13ebb-106">Sprawdź, czy hello plików na dysku hello zostały poprawnie wyeksportowane.</span><span class="sxs-lookup"><span data-stu-id="13ebb-106">Validate that hello files on hello drive were correctly exported.</span></span>  
  
<span data-ttu-id="13ebb-107">Musi mieć łączność tooAzure magazynu toouse tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="13ebb-107">You must have connectivity tooAzure Storage toouse this functionality.</span></span>  
  
<span data-ttu-id="13ebb-108">polecenie Hello naprawy zadania importu jest **RepairExport**.</span><span class="sxs-lookup"><span data-stu-id="13ebb-108">hello command for repairing an import job is **RepairExport**.</span></span>

## <a name="repairexport-parameters"></a><span data-ttu-id="13ebb-109">Parametry RepairExport</span><span class="sxs-lookup"><span data-stu-id="13ebb-109">RepairExport parameters</span></span>

<span data-ttu-id="13ebb-110">Witaj następujące parametry można określić z **RepairExport**:</span><span class="sxs-lookup"><span data-stu-id="13ebb-110">hello following parameters can be specified with **RepairExport**:</span></span>  
  
|<span data-ttu-id="13ebb-111">Parametr</span><span class="sxs-lookup"><span data-stu-id="13ebb-111">Parameter</span></span>|<span data-ttu-id="13ebb-112">Opis</span><span class="sxs-lookup"><span data-stu-id="13ebb-112">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="13ebb-113">**/ r: < RepairFile\>**</span><span class="sxs-lookup"><span data-stu-id="13ebb-113">**/r:<RepairFile\>**</span></span>|<span data-ttu-id="13ebb-114">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="13ebb-114">Required.</span></span> <span data-ttu-id="13ebb-115">Plik naprawy toohello ścieżki, który śledzi postęp hello naprawy hello i pozwala tooresume naprawę przerwania.</span><span class="sxs-lookup"><span data-stu-id="13ebb-115">Path toohello repair file, which tracks hello progress of hello repair, and allows you tooresume an interrupted repair.</span></span> <span data-ttu-id="13ebb-116">Każdy dysk musi mieć jeden i tylko jeden plik naprawy.</span><span class="sxs-lookup"><span data-stu-id="13ebb-116">Each drive must have one and only one repair file.</span></span> <span data-ttu-id="13ebb-117">Po uruchomieniu naprawy dla danego dysku przechodzą w hello ścieżki tooa naprawy pliku, które jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="13ebb-117">When you start a repair for a given drive, you will pass in hello path tooa repair file which does not yet exist.</span></span> <span data-ttu-id="13ebb-118">tooresume naprawę przerwania, należy przekazać w nazwie hello istniejącego pliku naprawy.</span><span class="sxs-lookup"><span data-stu-id="13ebb-118">tooresume an interrupted repair, you should pass in hello name of an existing repair file.</span></span> <span data-ttu-id="13ebb-119">zawsze należy określać Hello naprawy pliku odpowiedniego toohello dysk docelowy.</span><span class="sxs-lookup"><span data-stu-id="13ebb-119">hello repair file corresponding toohello target drive must always be specified.</span></span>|  
|<span data-ttu-id="13ebb-120">**/ logdir: < LogDirectory\>**</span><span class="sxs-lookup"><span data-stu-id="13ebb-120">**/logdir:<LogDirectory\>**</span></span>|<span data-ttu-id="13ebb-121">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="13ebb-121">Optional.</span></span> <span data-ttu-id="13ebb-122">Katalog dziennika Hello.</span><span class="sxs-lookup"><span data-stu-id="13ebb-122">hello log directory.</span></span> <span data-ttu-id="13ebb-123">Pełne pliki dziennika zostaną zapisane toothis katalogu.</span><span class="sxs-lookup"><span data-stu-id="13ebb-123">Verbose log files will be written toothis directory.</span></span> <span data-ttu-id="13ebb-124">Jeśli katalog dziennika nie jest określony, bieżący katalog hello będzie używany jako katalog dziennika hello.</span><span class="sxs-lookup"><span data-stu-id="13ebb-124">If no log directory is specified, hello current directory will be used as hello log directory.</span></span>|  
|<span data-ttu-id="13ebb-125">**/ d: < TargetDirectory\>**</span><span class="sxs-lookup"><span data-stu-id="13ebb-125">**/d:<TargetDirectory\>**</span></span>|<span data-ttu-id="13ebb-126">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="13ebb-126">Required.</span></span> <span data-ttu-id="13ebb-127">Witaj toovalidate katalogu i naprawy.</span><span class="sxs-lookup"><span data-stu-id="13ebb-127">hello directory toovalidate and repair.</span></span> <span data-ttu-id="13ebb-128">Zazwyczaj jest to katalog główny hello hello eksportu dysku, ale może też być sieciowego udziału plików zawierający kopię hello wyeksportowane pliki.</span><span class="sxs-lookup"><span data-stu-id="13ebb-128">This is usually hello root directory of hello export drive, but could also be a network file share containing a copy of hello exported files.</span></span>|  
|<span data-ttu-id="13ebb-129">**/BK: < BitLockerKey\>**</span><span class="sxs-lookup"><span data-stu-id="13ebb-129">**/bk:<BitLockerKey\>**</span></span>|<span data-ttu-id="13ebb-130">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="13ebb-130">Optional.</span></span> <span data-ttu-id="13ebb-131">Należy określić hello klucza funkcji BitLocker, jeśli chcesz, aby toounlock narzędzie hello są szyfrowane, gdy hello wyeksportowane pliki przechowywane.</span><span class="sxs-lookup"><span data-stu-id="13ebb-131">You should specify hello BitLocker key if you want hello tool toounlock an encrypted where hello exported files are stored.</span></span>|  
|<span data-ttu-id="13ebb-132">**/SN: < StorageAccountName\>**</span><span class="sxs-lookup"><span data-stu-id="13ebb-132">**/sn:<StorageAccountName\>**</span></span>|<span data-ttu-id="13ebb-133">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="13ebb-133">Required.</span></span> <span data-ttu-id="13ebb-134">zadanie eksportowania Hello nazwę konta magazynu hello hello.</span><span class="sxs-lookup"><span data-stu-id="13ebb-134">hello name of hello storage account for hello export job.</span></span>|  
|<span data-ttu-id="13ebb-135">**/SK: < StorageAccountKey\>**</span><span class="sxs-lookup"><span data-stu-id="13ebb-135">**/sk:<StorageAccountKey\>**</span></span>|<span data-ttu-id="13ebb-136">**Wymagane** tylko wtedy, gdy nie określono kontenera sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="13ebb-136">**Required** if and only if a container SAS is not specified.</span></span> <span data-ttu-id="13ebb-137">zadanie eksportowania Hello klucz konta usługi dla konta magazynu hello hello.</span><span class="sxs-lookup"><span data-stu-id="13ebb-137">hello account key for hello storage account for hello export job.</span></span>|  
|<span data-ttu-id="13ebb-138">**/csas: < ContainerSas\>**</span><span class="sxs-lookup"><span data-stu-id="13ebb-138">**/csas:<ContainerSas\>**</span></span>|<span data-ttu-id="13ebb-139">**Wymagane** tylko wtedy, gdy nie określono klucza konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="13ebb-139">**Required** if and only if hello storage account key is not specified.</span></span> <span data-ttu-id="13ebb-140">kontener Hello SAS do uzyskiwania dostępu do obiektów blob hello skojarzone z zadaniem eksportu hello.</span><span class="sxs-lookup"><span data-stu-id="13ebb-140">hello container SAS for accessing hello blobs associated with hello export job.</span></span>|  
|<span data-ttu-id="13ebb-141">**/ CopyLogFile: < DriveCopyLogFile\>**</span><span class="sxs-lookup"><span data-stu-id="13ebb-141">**/CopyLogFile:<DriveCopyLogFile\>**</span></span>|<span data-ttu-id="13ebb-142">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="13ebb-142">Required.</span></span> <span data-ttu-id="13ebb-143">Witaj ścieżki toohello dysku kopii pliku dziennika.</span><span class="sxs-lookup"><span data-stu-id="13ebb-143">hello path toohello drive copy log file.</span></span> <span data-ttu-id="13ebb-144">Plik Hello jest generowany przez hello usługi Import/Eksport systemu Windows Azure i można pobrać z magazynu obiektów blob hello skojarzone z zadaniem hello.</span><span class="sxs-lookup"><span data-stu-id="13ebb-144">hello file is generated by hello Windows Azure Import/Export service and can be downloaded from hello blob storage associated with hello job.</span></span> <span data-ttu-id="13ebb-145">Witaj Kopiuj plik dziennika zawiera informacje dotyczące obiektów blob nie powiodło się lub pliki, które są toobe naprawić.</span><span class="sxs-lookup"><span data-stu-id="13ebb-145">hello copy log file contains information about failed blobs or files which are toobe repaired.</span></span>|  
|<span data-ttu-id="13ebb-146">**/ ManifestFile: < DriveManifestFile\>**</span><span class="sxs-lookup"><span data-stu-id="13ebb-146">**/ManifestFile:<DriveManifestFile\>**</span></span>|<span data-ttu-id="13ebb-147">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="13ebb-147">Optional.</span></span> <span data-ttu-id="13ebb-148">Witaj dysk ścieżki toohello eksportu pliku manifestu.</span><span class="sxs-lookup"><span data-stu-id="13ebb-148">hello path toohello export drive's manifest file.</span></span> <span data-ttu-id="13ebb-149">Ten plik jest generowany przez usługę Windows Azure importu/eksportu hello i przechowywane na dysku eksportu hello i opcjonalnie w obiekcie blob na koncie magazynu hello skojarzone z zadaniem hello.</span><span class="sxs-lookup"><span data-stu-id="13ebb-149">This file is generated by hello Windows Azure Import/Export service and stored on hello export drive, and optionally in a blob in hello storage account associated with hello job.</span></span><br /><br /> <span data-ttu-id="13ebb-150">Witaj zawartości hello plików na dysku eksportu hello zostaną zweryfikowane wartości skrótu MD5 hello zawarte w tym pliku.</span><span class="sxs-lookup"><span data-stu-id="13ebb-150">hello content of hello files on hello export drive will be verified with hello MD5 hashes contained in this file.</span></span> <span data-ttu-id="13ebb-151">Wszystkie pliki, które są określone toobe uszkodzony będzie toohello pobrane i ponownie zapisane docelowy katalogów.</span><span class="sxs-lookup"><span data-stu-id="13ebb-151">Any files that are determined toobe corrupted will be downloaded and rewritten toohello target directories.</span></span>|  
  
## <a name="using-repairexport-mode-toocorrect-failed-exports"></a><span data-ttu-id="13ebb-152">Przy użyciu RepairExport toocorrect trybu nie powiodło się eksportowanie</span><span class="sxs-lookup"><span data-stu-id="13ebb-152">Using RepairExport mode toocorrect failed exports</span></span>  
<span data-ttu-id="13ebb-153">Można użyć hello Azure narzędzie importu/eksportu toodownload pliki, których nie powiodła się tooexport.</span><span class="sxs-lookup"><span data-stu-id="13ebb-153">You can use hello Azure Import/Export Tool toodownload files that failed tooexport.</span></span> <span data-ttu-id="13ebb-154">plik dziennika kopii Hello będzie zawierać listę plików, których nie powiodła się tooexport.</span><span class="sxs-lookup"><span data-stu-id="13ebb-154">hello copy log file will contain a list of files that failed tooexport.</span></span>  
  
<span data-ttu-id="13ebb-155">Hello przyczyny niepowodzeń eksportu: hello następujące możliwości:</span><span class="sxs-lookup"><span data-stu-id="13ebb-155">hello causes of export failures include hello following possibilities:</span></span>  
  
-   <span data-ttu-id="13ebb-156">Uszkodzone dyski</span><span class="sxs-lookup"><span data-stu-id="13ebb-156">Damaged drives</span></span>  
  
-   <span data-ttu-id="13ebb-157">klucz konta magazynu Hello została zmieniona w trakcie procesu transferu hello</span><span class="sxs-lookup"><span data-stu-id="13ebb-157">hello storage account key changed during hello transfer process</span></span>  
  
<span data-ttu-id="13ebb-158">Narzędzie hello toorun w **RepairExport** trybie, należy najpierw tooconnect hello dysku zawierającego hello wyeksportowane pliki tooyour komputera.</span><span class="sxs-lookup"><span data-stu-id="13ebb-158">toorun hello tool in **RepairExport** mode, you first need tooconnect hello drive containing hello exported files tooyour computer.</span></span> <span data-ttu-id="13ebb-159">Następnie należy uruchomić narzędzie importu/eksportu Azure, określenie hello ścieżki toothat dysku z hello hello `/d` parametru.</span><span class="sxs-lookup"><span data-stu-id="13ebb-159">Next, run hello Azure Import/Export Tool, specifying hello path toothat drive with hello `/d` parameter.</span></span> <span data-ttu-id="13ebb-160">Należy również toospecify hello ścieżki toohello dysku kopii dziennika pobranego pliku.</span><span class="sxs-lookup"><span data-stu-id="13ebb-160">You also need toospecify hello path toohello drive's copy log file that you downloaded.</span></span> <span data-ttu-id="13ebb-161">Hello poniżej poniższy przykład wiersz polecenia uruchamia hello narzędzia toorepair wszystkie pliki, których nie powiodła się tooexport:</span><span class="sxs-lookup"><span data-stu-id="13ebb-161">hello following command line example below runs hello tool toorepair any files that failed tooexport:</span></span>  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log  
```  
  
<span data-ttu-id="13ebb-162">Witaj poniżej znajduje się przykład kopii pliku dziennika, który zawiera ten jeden blok w hello tooexport obiektu blob nie powiodło się:</span><span class="sxs-lookup"><span data-stu-id="13ebb-162">hello following is an example of a copy log file that shows that one block in hello blob failed tooexport:</span></span>  
  
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
  
<span data-ttu-id="13ebb-163">plik dziennika kopii Hello wskazuje, wystąpił błąd podczas pobierania został hello usługi Import/Eksport systemu Windows Azure, jednego pliku toohello bloków hello blob na powitania eksportu dysku.</span><span class="sxs-lookup"><span data-stu-id="13ebb-163">hello copy log file indicates that a failure occurred while hello Windows Azure Import/Export service was downloading one of hello blob's blocks toohello file on hello export drive.</span></span> <span data-ttu-id="13ebb-164">Witaj inne składniki pliku hello pobrana pomyślnie, a długość pliku hello została poprawnie ustawiona.</span><span class="sxs-lookup"><span data-stu-id="13ebb-164">hello other components of hello file downloaded successfully, and hello file length was correctly set.</span></span> <span data-ttu-id="13ebb-165">W takim przypadku narzędzie hello będzie Otwórz plik hello na powitania dysku, Pobierz bloku hello z konta magazynu hello i Zapisz toohello pliku zakresu, zaczynając od przesunięcia 65536 o długości 65536.</span><span class="sxs-lookup"><span data-stu-id="13ebb-165">In this case, hello tool will open hello file on hello drive, download hello block from hello storage account, and write it toohello file range starting from offset 65536 with length 65536.</span></span>  
  
## <a name="using-repairexport-toovalidate-drive-contents"></a><span data-ttu-id="13ebb-166">Przy użyciu zawartości dysku toovalidate RepairExport</span><span class="sxs-lookup"><span data-stu-id="13ebb-166">Using RepairExport toovalidate drive contents</span></span>  
<span data-ttu-id="13ebb-167">Import/Eksport Azure można również używać z hello **RepairExport** opcji toovalidate hello zawartości na dysku hello są poprawne.</span><span class="sxs-lookup"><span data-stu-id="13ebb-167">You can also use Azure Import/Export with hello **RepairExport** option toovalidate hello contents on hello drive are correct.</span></span> <span data-ttu-id="13ebb-168">Plik manifestu Hello na każdym dysku eksportu zawiera MD5s hello zawartość hello dysku.</span><span class="sxs-lookup"><span data-stu-id="13ebb-168">hello manifest file on each export drive contains MD5s for hello contents of hello drive.</span></span>  
  
<span data-ttu-id="13ebb-169">Witaj usługi Import/Eksport Azure można także zapisać pliki manifestu hello tooa konta magazynu podczas procesu eksportowania hello.</span><span class="sxs-lookup"><span data-stu-id="13ebb-169">hello Azure Import/Export service can also save hello manifest files tooa storage account during hello export process.</span></span> <span data-ttu-id="13ebb-170">Witaj lokalizację plików manifestu hello jest dostępny za pośrednictwem hello [pobrania zadania](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operacji po ukończeniu zadania hello.</span><span class="sxs-lookup"><span data-stu-id="13ebb-170">hello location of hello manifest files is available via hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation when hello job has completed.</span></span> <span data-ttu-id="13ebb-171">Zobacz [usługi Import/Eksport Format pliku manifestu](storage-import-export-file-format-metadata-and-properties.md) Aby uzyskać więcej informacji o formacie hello dysku pliku manifestu.</span><span class="sxs-lookup"><span data-stu-id="13ebb-171">See [Import/Export service Manifest File Format](storage-import-export-file-format-metadata-and-properties.md) for more information about hello format of a drive manifest file.</span></span>  
  
<span data-ttu-id="13ebb-172">Witaj poniższy przykład przedstawia sposób toorun hello Azure narzędzie importu/eksportu z hello **/ManifestFile** i **/CopyLogFile** parametry:</span><span class="sxs-lookup"><span data-stu-id="13ebb-172">hello following example shows how toorun hello Azure Import/Export Tool with hello **/ManifestFile** and **/CopyLogFile** parameters:</span></span>  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log /ManifestFile:G:\9WM35C3U.manifest  
```  
  
<span data-ttu-id="13ebb-173">Witaj poniżej znajduje się przykład pliku manifestu:</span><span class="sxs-lookup"><span data-stu-id="13ebb-173">hello following is an example of a manifest file:</span></span>  
  
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
  
<span data-ttu-id="13ebb-174">Po zakończenia procesu naprawy hello narzędzie hello zapoznaj się z artykułem każdego pliku, do którego odwołuje się plik manifestu hello i Sprawdź integralność pliku hello skrótów hello MD5.</span><span class="sxs-lookup"><span data-stu-id="13ebb-174">After finishing hello repair process, hello tool will read through each file referenced in hello manifest file and verify hello file's integrity with hello MD5 hashes.</span></span> <span data-ttu-id="13ebb-175">Dla manifest hello powyżej przechodzą przez hello następujące składniki.</span><span class="sxs-lookup"><span data-stu-id="13ebb-175">For hello manifest above, it will go through hello following components.</span></span>  

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

<span data-ttu-id="13ebb-176">Dowolny składnik Niepowodzenie weryfikacji hello zostanie pobrana przez narzędzie hello i ulegną toohello tego samego pliku na dysku hello.</span><span class="sxs-lookup"><span data-stu-id="13ebb-176">Any component failing hello verification will be downloaded by hello tool and rewritten toohello same file on hello drive.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="13ebb-177">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="13ebb-177">Next steps</span></span>
 
* [<span data-ttu-id="13ebb-178">Definiowanie hello Azure narzędzie importu/eksportu</span><span class="sxs-lookup"><span data-stu-id="13ebb-178">Setting Up hello Azure Import/Export Tool</span></span>](storage-import-export-tool-setup-v1.md)   
* [<span data-ttu-id="13ebb-179">Przygotowywanie dysków twardych do zadania importu</span><span class="sxs-lookup"><span data-stu-id="13ebb-179">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="13ebb-180">Sprawdzanie stanu zadania za pomocą plików dziennika kopiowania</span><span class="sxs-lookup"><span data-stu-id="13ebb-180">Reviewing job status with copy log files</span></span>](storage-import-export-tool-reviewing-job-status-v1.md)   
* [<span data-ttu-id="13ebb-181">Naprawianie zadania importu</span><span class="sxs-lookup"><span data-stu-id="13ebb-181">Repairing an import job</span></span>](storage-import-export-tool-repairing-an-import-job-v1.md)   
* [<span data-ttu-id="13ebb-182">Rozwiązywanie problemów z hello Azure narzędzie importu/eksportu</span><span class="sxs-lookup"><span data-stu-id="13ebb-182">Troubleshooting hello Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
