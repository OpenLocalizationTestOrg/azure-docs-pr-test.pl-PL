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
# <a name="azure-importexport-service-log-file-format"></a><span data-ttu-id="85371-103">Format pliku dziennika usług Azure Import/Eksport</span><span class="sxs-lookup"><span data-stu-id="85371-103">Azure Import/Export service log file format</span></span>
<span data-ttu-id="85371-104">Gdy hello usługi Import/Eksport Microsoft Azure wykonuje akcję na dysku jako część zadania importu lub eksportu, dziennikach tooblock obiekty BLOB na koncie magazynu hello skojarzonego z tym zadaniem.</span><span class="sxs-lookup"><span data-stu-id="85371-104">When hello Microsoft Azure Import/Export service performs an action on a drive as part of an import job or an export job, logs are written tooblock blobs in hello storage account associated with that job.</span></span>  
  
<span data-ttu-id="85371-105">Istnieją dwa dzienniki, które mogą zostać zapisane przez hello importu/eksportu usług:</span><span class="sxs-lookup"><span data-stu-id="85371-105">There are two logs that may be written by hello Import/Export service:</span></span>  
  
-   <span data-ttu-id="85371-106">Dziennik błędów Hello był zawsze generowany w przypadku hello błędu.</span><span class="sxs-lookup"><span data-stu-id="85371-106">hello error log is always generated in hello event of an error.</span></span>  
  
-   <span data-ttu-id="85371-107">Witaj pełnego dziennika nie jest domyślnie włączona, ale może zostać włączona przez ustawienie hello `EnableVerboseLog` właściwość [zawiesić zadanie](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) lub [właściwości zadania aktualizacji](/rest/api/storageimportexport/jobs#Jobs_Update) operacji.</span><span class="sxs-lookup"><span data-stu-id="85371-107">hello verbose log is not enabled by default, but may be enabled by setting hello `EnableVerboseLog` property on a [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation.</span></span>  
  
## <a name="log-file-location"></a><span data-ttu-id="85371-108">Lokalizacja pliku dziennika</span><span class="sxs-lookup"><span data-stu-id="85371-108">Log file location</span></span>  
<span data-ttu-id="85371-109">Witaj dziennikach tooblock obiekty BLOB w kontenerze hello lub określony przez hello katalog wirtualny `ImportExportStatesPath` ustawienie, które można ustawić na `Put Job` operacji.</span><span class="sxs-lookup"><span data-stu-id="85371-109">hello logs are written tooblock blobs in hello container or virtual directory specified by hello `ImportExportStatesPath` setting, which you can set on a `Put Job` operation.</span></span> <span data-ttu-id="85371-110">Witaj lokalizacji toowhich hello dziennikach zależy od sposobu uwierzytelniania jest określona dla zadania hello, wraz z hello wartość określona dla `ImportExportStatesPath`.</span><span class="sxs-lookup"><span data-stu-id="85371-110">hello location toowhich hello logs are written depends on how authentication is specified for hello job, together with hello value specified for `ImportExportStatesPath`.</span></span> <span data-ttu-id="85371-111">Uwierzytelnianie hello zadania można określić za pomocą klucza konta magazynu lub kontener SAS (sygnatury dostępu współdzielonego).</span><span class="sxs-lookup"><span data-stu-id="85371-111">Authentication for hello job may be specified via a storage account key, or a container SAS (shared access signature).</span></span>  
  
<span data-ttu-id="85371-112">Nazwa Hello kontenera hello lub katalog wirtualny może być hello domyślną nazwę `waimportexport`, lub innego kontenera ani nazwy katalogu wirtualnego, który określisz.</span><span class="sxs-lookup"><span data-stu-id="85371-112">hello name of hello container or virtual directory may either be hello default name of `waimportexport`, or another container or virtual directory name that you specify.</span></span>  
  
<span data-ttu-id="85371-113">Witaj w poniższej tabeli przedstawiono hello możliwe opcje:</span><span class="sxs-lookup"><span data-stu-id="85371-113">hello table below shows hello possible options:</span></span>  
  
|<span data-ttu-id="85371-114">Metoda uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="85371-114">Authentication Method</span></span>|<span data-ttu-id="85371-115">Wartość `ImportExportStatesPath`elementu</span><span class="sxs-lookup"><span data-stu-id="85371-115">Value of `ImportExportStatesPath`Element</span></span>|<span data-ttu-id="85371-116">Lokalizacja dziennika obiektów blob</span><span class="sxs-lookup"><span data-stu-id="85371-116">Location of Log Blobs</span></span>|  
|---------------------------|----------------------------------------------|---------------------------|  
|<span data-ttu-id="85371-117">Klucz konta magazynu</span><span class="sxs-lookup"><span data-stu-id="85371-117">Storage account key</span></span>|<span data-ttu-id="85371-118">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="85371-118">Default value</span></span>|<span data-ttu-id="85371-119">Kontener o nazwie `waimportexport`, która jest hello domyślnego kontenera.</span><span class="sxs-lookup"><span data-stu-id="85371-119">A container named `waimportexport`, which is hello default container.</span></span> <span data-ttu-id="85371-120">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="85371-120">For example:</span></span><br /><br /> `https://myaccount.blob.core.windows.net/waimportexport`|  
|<span data-ttu-id="85371-121">Klucz konta magazynu</span><span class="sxs-lookup"><span data-stu-id="85371-121">Storage account key</span></span>|<span data-ttu-id="85371-122">Wartość określona przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="85371-122">User-specified value</span></span>|<span data-ttu-id="85371-123">Kontener o nazwie przez użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="85371-123">A container named by hello user.</span></span> <span data-ttu-id="85371-124">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="85371-124">For example:</span></span><br /><br /> `https://myaccount.blob.core.windows.net/mylogcontainer`|  
|<span data-ttu-id="85371-125">Kontener SAS</span><span class="sxs-lookup"><span data-stu-id="85371-125">Container SAS</span></span>|<span data-ttu-id="85371-126">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="85371-126">Default value</span></span>|<span data-ttu-id="85371-127">Katalog wirtualny o nazwie `waimportexport`, czyli hello domyślną nazwę poniżej kontenera hello określone w hello sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="85371-127">A virtual directory named `waimportexport`, which is hello default name, beneath hello container specified in hello SAS.</span></span><br /><br /> <span data-ttu-id="85371-128">Na przykład jeśli hello SAS określone dla zadania hello jest `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, następnie będzie hello lokalizacja dziennika`https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport`</span><span class="sxs-lookup"><span data-stu-id="85371-128">For example, if hello SAS specified for hello job is  `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, then hello log location would be `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport`</span></span>|  
|<span data-ttu-id="85371-129">Kontener SAS</span><span class="sxs-lookup"><span data-stu-id="85371-129">Container SAS</span></span>|<span data-ttu-id="85371-130">Wartość określona przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="85371-130">User-specified value</span></span>|<span data-ttu-id="85371-131">Katalog wirtualny o nazwie użytkownika hello, poniżej kontenera hello określone w hello sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="85371-131">A virtual directory named by hello user, beneath hello container specified in hello SAS.</span></span><br /><br /> <span data-ttu-id="85371-132">Na przykład jeśli hello SAS określone dla zadania hello jest `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, i hello określony katalog wirtualny nosi nazwę `mylogblobs`, następnie będzie lokalizacja dziennika hello `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport/mylogblobs`.</span><span class="sxs-lookup"><span data-stu-id="85371-132">For example, if hello SAS specified for hello job is  `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, and hello specified virtual directory is named `mylogblobs`, then hello log location would be `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport/mylogblobs`.</span></span>|  
  
<span data-ttu-id="85371-133">Można pobrać adresu URL hello hello błąd i pełne dzienniki hello wywoływania [pobrania zadania](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operacji.</span><span class="sxs-lookup"><span data-stu-id="85371-133">You can retrieve hello URL for hello error and verbose logs by calling hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="85371-134">Dzienniki Hello są dostępne po zakończeniu przetwarzania hello dysku.</span><span class="sxs-lookup"><span data-stu-id="85371-134">hello logs are available after processing of hello drive is complete.</span></span>  
  
## <a name="log-file-format"></a><span data-ttu-id="85371-135">Format pliku dziennika</span><span class="sxs-lookup"><span data-stu-id="85371-135">Log file format</span></span>  
<span data-ttu-id="85371-136">Witaj formatu dla obu dzienników jest hello takie same: obiektu blob zawierające opisy XML hello zdarzeń, które wystąpiły podczas kopiowania obiektów blob między hello dysk twardy i konta powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="85371-136">hello format for both logs is hello same: a blob containing XML descriptions of hello events that occurred while copying blobs between hello hard drive and hello customer's account.</span></span>  
  
<span data-ttu-id="85371-137">Pełny dziennik Hello zawiera pełne informacje na temat stanu hello hello operacji kopiowania dla każdego obiektu blob (w przypadku zadania importu) lub pliku (dla zadania eksportu), tylko hello informacje dotyczące obiektów blob lub plików, które napotkały błędy podczas hello zawiera dziennik błędów hello Importowanie lub eksportowanie zadania.</span><span class="sxs-lookup"><span data-stu-id="85371-137">hello verbose log contains complete information about hello status of hello copy operation for every blob (for an import job) or file (for an export job), whereas hello error log contains only hello information for blobs or files that encountered errors during hello import or export job.</span></span>  
  
<span data-ttu-id="85371-138">format pełny dziennik Hello jest pokazany poniżej.</span><span class="sxs-lookup"><span data-stu-id="85371-138">hello verbose log format is shown below.</span></span> <span data-ttu-id="85371-139">Dziennik błędów Hello ma hello takie same struktury, ale odfiltrowuje pomyślnych operacji.</span><span class="sxs-lookup"><span data-stu-id="85371-139">hello error log has hello same structure, but filters out successful operations.</span></span>  

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

<span data-ttu-id="85371-140">Witaj poniższej tabeli opisano elementy hello hello pliku dziennika.</span><span class="sxs-lookup"><span data-stu-id="85371-140">hello following table describes hello elements of hello log file.</span></span>  
  
|<span data-ttu-id="85371-141">XML Element</span><span class="sxs-lookup"><span data-stu-id="85371-141">XML Element</span></span>|<span data-ttu-id="85371-142">Typ</span><span class="sxs-lookup"><span data-stu-id="85371-142">Type</span></span>|<span data-ttu-id="85371-143">Opis</span><span class="sxs-lookup"><span data-stu-id="85371-143">Description</span></span>|  
|-----------------|----------|-----------------|  
|`DriveLog`|<span data-ttu-id="85371-144">XML Element</span><span class="sxs-lookup"><span data-stu-id="85371-144">XML Element</span></span>|<span data-ttu-id="85371-145">Reprezentuje dziennika dysku.</span><span class="sxs-lookup"><span data-stu-id="85371-145">Represents a drive log.</span></span>|  
|`Version`|<span data-ttu-id="85371-146">Atrybut ciągu</span><span class="sxs-lookup"><span data-stu-id="85371-146">Attribute, String</span></span>|<span data-ttu-id="85371-147">Wersja Hello hello format dziennika.</span><span class="sxs-lookup"><span data-stu-id="85371-147">hello version of hello log format.</span></span>|  
|`DriveId`|<span data-ttu-id="85371-148">Ciąg</span><span class="sxs-lookup"><span data-stu-id="85371-148">String</span></span>|<span data-ttu-id="85371-149">Witaj numer seryjny sprzętu stacji.</span><span class="sxs-lookup"><span data-stu-id="85371-149">hello drive's hardware serial number.</span></span>|  
|`Status`|<span data-ttu-id="85371-150">Ciąg</span><span class="sxs-lookup"><span data-stu-id="85371-150">String</span></span>|<span data-ttu-id="85371-151">Stan przetwarzania dysku hello.</span><span class="sxs-lookup"><span data-stu-id="85371-151">Status of hello drive processing.</span></span> <span data-ttu-id="85371-152">Zobacz hello `Drive Status Codes` tabela poniżej, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="85371-152">See hello `Drive Status Codes` table below for more information.</span></span>|  
|`Blob`|<span data-ttu-id="85371-153">Zagnieżdżone — element XML</span><span class="sxs-lookup"><span data-stu-id="85371-153">Nested XML element</span></span>|<span data-ttu-id="85371-154">Reprezentuje obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="85371-154">Represents a blob.</span></span>|  
|`Blob/BlobPath`|<span data-ttu-id="85371-155">Ciąg</span><span class="sxs-lookup"><span data-stu-id="85371-155">String</span></span>|<span data-ttu-id="85371-156">Identyfikator URI obiektu hello blob Hello.</span><span class="sxs-lookup"><span data-stu-id="85371-156">hello URI of hello blob.</span></span>|  
|`Blob/FilePath`|<span data-ttu-id="85371-157">Ciąg</span><span class="sxs-lookup"><span data-stu-id="85371-157">String</span></span>|<span data-ttu-id="85371-158">Witaj ścieżki względnej toohello pliku na dysku hello.</span><span class="sxs-lookup"><span data-stu-id="85371-158">hello relative path toohello file on hello drive.</span></span>|  
|`Blob/Snapshot`|<span data-ttu-id="85371-159">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="85371-159">DateTime</span></span>|<span data-ttu-id="85371-160">Wersja migawki Hello hello obiektów blob, tylko zadania eksportu.</span><span class="sxs-lookup"><span data-stu-id="85371-160">hello snapshot version of hello blob, for an export job only.</span></span>|  
|`Blob/Length`|<span data-ttu-id="85371-161">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="85371-161">Integer</span></span>|<span data-ttu-id="85371-162">Witaj całkowita długość obiektu blob hello w bajtach.</span><span class="sxs-lookup"><span data-stu-id="85371-162">hello total length of hello blob in bytes.</span></span>|  
|`Blob/LastModified`|<span data-ttu-id="85371-163">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="85371-163">DateTime</span></span>|<span data-ttu-id="85371-164">Witaj daty/godziny tego obiektu blob hello ostatniej modyfikacji, tylko zadania eksportu.</span><span class="sxs-lookup"><span data-stu-id="85371-164">hello date/time that hello blob was last modified, for an export job only.</span></span>|  
|`Blob/ImportDisposition`|<span data-ttu-id="85371-165">Ciąg</span><span class="sxs-lookup"><span data-stu-id="85371-165">String</span></span>|<span data-ttu-id="85371-166">Hello zaimportować dyspozycji hello obiektów blob, tylko zadania importu.</span><span class="sxs-lookup"><span data-stu-id="85371-166">hello import disposition of hello blob, for an import job only.</span></span>|  
|`Blob/ImportDisposition/@Status`|<span data-ttu-id="85371-167">Atrybut ciągu</span><span class="sxs-lookup"><span data-stu-id="85371-167">Attribute, String</span></span>|<span data-ttu-id="85371-168">Stan Hello hello zaimportować dyspozycji.</span><span class="sxs-lookup"><span data-stu-id="85371-168">hello status of hello import disposition.</span></span>|  
|`PageRangeList`|<span data-ttu-id="85371-169">Zagnieżdżone — element XML</span><span class="sxs-lookup"><span data-stu-id="85371-169">Nested XML element</span></span>|<span data-ttu-id="85371-170">Reprezentuje listę zakresów stron dla stronicowych obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="85371-170">Represents a list of page ranges for a page blob.</span></span>|  
|`PageRange`|<span data-ttu-id="85371-171">XML element</span><span class="sxs-lookup"><span data-stu-id="85371-171">XML element</span></span>|<span data-ttu-id="85371-172">Reprezentuje zakres stron.</span><span class="sxs-lookup"><span data-stu-id="85371-172">Represents a page range.</span></span>|  
|`PageRange/@Offset`|<span data-ttu-id="85371-173">Atrybut, liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="85371-173">Attribute, Integer</span></span>|<span data-ttu-id="85371-174">Początkowe przesunięcie zakresu strony hello w obiekcie blob hello.</span><span class="sxs-lookup"><span data-stu-id="85371-174">Starting offset of hello page range in hello blob.</span></span>|  
|`PageRange/@Length`|<span data-ttu-id="85371-175">Atrybut, liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="85371-175">Attribute, Integer</span></span>|<span data-ttu-id="85371-176">Długość w bajtach hello zakres stron.</span><span class="sxs-lookup"><span data-stu-id="85371-176">Length in bytes of hello page range.</span></span>|  
|`PageRange/@Hash`|<span data-ttu-id="85371-177">Atrybut ciągu</span><span class="sxs-lookup"><span data-stu-id="85371-177">Attribute, String</span></span>|<span data-ttu-id="85371-178">Kodowany w formacie Base16 Skrót MD5 hello strony zakresu.</span><span class="sxs-lookup"><span data-stu-id="85371-178">Base16-encoded MD5 hash of hello page range.</span></span>|  
|`PageRange/@Status`|<span data-ttu-id="85371-179">Atrybut ciągu</span><span class="sxs-lookup"><span data-stu-id="85371-179">Attribute, String</span></span>|<span data-ttu-id="85371-180">Stan przetwarzania hello zakres stron.</span><span class="sxs-lookup"><span data-stu-id="85371-180">Status of processing hello page range.</span></span>|  
|`BlockList`|<span data-ttu-id="85371-181">Zagnieżdżone — element XML</span><span class="sxs-lookup"><span data-stu-id="85371-181">Nested XML element</span></span>|<span data-ttu-id="85371-182">Reprezentuje listę bloków dla blokowego obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="85371-182">Represents a list of blocks for a block blob.</span></span>|  
|`Block`|<span data-ttu-id="85371-183">XML element</span><span class="sxs-lookup"><span data-stu-id="85371-183">XML element</span></span>|<span data-ttu-id="85371-184">Reprezentuje blok.</span><span class="sxs-lookup"><span data-stu-id="85371-184">Represents a block.</span></span>|  
|`Block/@Offset`|<span data-ttu-id="85371-185">Atrybut, liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="85371-185">Attribute, Integer</span></span>|<span data-ttu-id="85371-186">Przesunięcie początkowe bloku hello w obiekcie blob hello.</span><span class="sxs-lookup"><span data-stu-id="85371-186">Starting offset of hello block in hello blob.</span></span>|  
|`Block/@Length`|<span data-ttu-id="85371-187">Atrybut, liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="85371-187">Attribute, Integer</span></span>|<span data-ttu-id="85371-188">Długość w bajtach hello bloku.</span><span class="sxs-lookup"><span data-stu-id="85371-188">Length in bytes of hello block.</span></span>|  
|`Block/@Id`|<span data-ttu-id="85371-189">Atrybut ciągu</span><span class="sxs-lookup"><span data-stu-id="85371-189">Attribute, String</span></span>|<span data-ttu-id="85371-190">Identyfikator bloku Hello.</span><span class="sxs-lookup"><span data-stu-id="85371-190">hello block ID.</span></span>|  
|`Block/@Hash`|<span data-ttu-id="85371-191">Atrybut ciągu</span><span class="sxs-lookup"><span data-stu-id="85371-191">Attribute, String</span></span>|<span data-ttu-id="85371-192">Kodowany w formacie Base16 Skrót MD5 hello bloku.</span><span class="sxs-lookup"><span data-stu-id="85371-192">Base16-encoded MD5 hash of hello block.</span></span>|  
|`Block/@Status`|<span data-ttu-id="85371-193">Atrybut ciągu</span><span class="sxs-lookup"><span data-stu-id="85371-193">Attribute, String</span></span>|<span data-ttu-id="85371-194">Stan przetwarzania hello bloku.</span><span class="sxs-lookup"><span data-stu-id="85371-194">Status of processing hello block.</span></span>|  
|`Metadata`|<span data-ttu-id="85371-195">Zagnieżdżone — element XML</span><span class="sxs-lookup"><span data-stu-id="85371-195">Nested XML element</span></span>|<span data-ttu-id="85371-196">Reprezentuje metadane hello obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="85371-196">Represents hello blob's metadata.</span></span>|  
|`Metadata/@Status`|<span data-ttu-id="85371-197">Atrybut ciągu</span><span class="sxs-lookup"><span data-stu-id="85371-197">Attribute, String</span></span>|<span data-ttu-id="85371-198">Stan przetwarzania hello metadane obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="85371-198">Status of processing of hello blob metadata.</span></span>|  
|`Metadata/GlobalPath`|<span data-ttu-id="85371-199">Ciąg</span><span class="sxs-lookup"><span data-stu-id="85371-199">String</span></span>|<span data-ttu-id="85371-200">Ścieżka względna toohello globalnych metadanych pliku.</span><span class="sxs-lookup"><span data-stu-id="85371-200">Relative path toohello global metadata file.</span></span>|  
|`Metadata/GlobalPath/@Hash`|<span data-ttu-id="85371-201">Atrybut ciągu</span><span class="sxs-lookup"><span data-stu-id="85371-201">Attribute, String</span></span>|<span data-ttu-id="85371-202">Kodowany w formacie Base16 Skrót MD5 hello globalnych metadanych pliku.</span><span class="sxs-lookup"><span data-stu-id="85371-202">Base16-encoded MD5 hash of hello global metadata file.</span></span>|  
|`Metadata/Path`|<span data-ttu-id="85371-203">Ciąg</span><span class="sxs-lookup"><span data-stu-id="85371-203">String</span></span>|<span data-ttu-id="85371-204">Ścieżka względna toohello pliku metadanych.</span><span class="sxs-lookup"><span data-stu-id="85371-204">Relative path toohello metadata file.</span></span>|  
|`Metadata/Path/@Hash`|<span data-ttu-id="85371-205">Atrybut ciągu</span><span class="sxs-lookup"><span data-stu-id="85371-205">Attribute, String</span></span>|<span data-ttu-id="85371-206">Kodowany w formacie Base16 Skrót MD5 hello pliku metadanych.</span><span class="sxs-lookup"><span data-stu-id="85371-206">Base16-encoded MD5 hash of hello metadata file.</span></span>|  
|`Properties`|<span data-ttu-id="85371-207">Zagnieżdżone — element XML</span><span class="sxs-lookup"><span data-stu-id="85371-207">Nested XML element</span></span>|<span data-ttu-id="85371-208">Reprezentuje hello właściwości obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="85371-208">Represents hello blob properties.</span></span>|  
|`Properties/@Status`|<span data-ttu-id="85371-209">Atrybut ciągu</span><span class="sxs-lookup"><span data-stu-id="85371-209">Attribute, String</span></span>|<span data-ttu-id="85371-210">Stan przetwarzania hello właściwości obiektu blob, np. nie można odnaleźć pliku, ukończone.</span><span class="sxs-lookup"><span data-stu-id="85371-210">Status of processing hello blob properties, e.g. file not found, completed.</span></span>|  
|`Properties/GlobalPath`|<span data-ttu-id="85371-211">Ciąg</span><span class="sxs-lookup"><span data-stu-id="85371-211">String</span></span>|<span data-ttu-id="85371-212">Ścieżka względna toohello globalnych właściwości pliku.</span><span class="sxs-lookup"><span data-stu-id="85371-212">Relative path toohello global properties file.</span></span>|  
|`Properties/GlobalPath/@Hash`|<span data-ttu-id="85371-213">Atrybut ciągu</span><span class="sxs-lookup"><span data-stu-id="85371-213">Attribute, String</span></span>|<span data-ttu-id="85371-214">Kodowany w formacie Base16 Skrót MD5 hello globalnych właściwości pliku.</span><span class="sxs-lookup"><span data-stu-id="85371-214">Base16-encoded MD5 hash of hello global properties file.</span></span>|  
|`Properties/Path`|<span data-ttu-id="85371-215">Ciąg</span><span class="sxs-lookup"><span data-stu-id="85371-215">String</span></span>|<span data-ttu-id="85371-216">Ścieżka względna toohello właściwości pliku.</span><span class="sxs-lookup"><span data-stu-id="85371-216">Relative path toohello properties file.</span></span>|  
|`Properties/Path/@Hash`|<span data-ttu-id="85371-217">Atrybut ciągu</span><span class="sxs-lookup"><span data-stu-id="85371-217">Attribute, String</span></span>|<span data-ttu-id="85371-218">Kodowany w formacie Base16 Skrót MD5 hello właściwości pliku.</span><span class="sxs-lookup"><span data-stu-id="85371-218">Base16-encoded MD5 hash of hello properties file.</span></span>|  
|`Blob/Status`|<span data-ttu-id="85371-219">Ciąg</span><span class="sxs-lookup"><span data-stu-id="85371-219">String</span></span>|<span data-ttu-id="85371-220">Stan przetwarzania obiektu blob hello.</span><span class="sxs-lookup"><span data-stu-id="85371-220">Status of processing hello blob.</span></span>|  
  
# <a name="drive-status-codes"></a><span data-ttu-id="85371-221">Kody stanu dysku</span><span class="sxs-lookup"><span data-stu-id="85371-221">Drive status codes</span></span>  
<span data-ttu-id="85371-222">Witaj Poniższa tabela zawiera listę kodów stanu hello przetwarzania dysku.</span><span class="sxs-lookup"><span data-stu-id="85371-222">hello following table lists hello status codes for processing a drive.</span></span>  
  
|<span data-ttu-id="85371-223">Kod stanu</span><span class="sxs-lookup"><span data-stu-id="85371-223">Status code</span></span>|<span data-ttu-id="85371-224">Opis</span><span class="sxs-lookup"><span data-stu-id="85371-224">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="85371-225">dysk Hello zakończył przetwarzanie bez żadnych błędów.</span><span class="sxs-lookup"><span data-stu-id="85371-225">hello drive has finished processing without any errors.</span></span>|  
|`CompletedWithWarnings`|<span data-ttu-id="85371-226">dysk Hello zakończył przetwarzanie z ostrzeżeniami w jeden lub więcej obiektów blob na powitania importu przepisy określone dla obiektów blob hello.</span><span class="sxs-lookup"><span data-stu-id="85371-226">hello drive has finished processing with warnings in one or more blobs per hello import dispositions specified for hello blobs.</span></span>|  
|`CompletedWithErrors`|<span data-ttu-id="85371-227">dysk Hello zostało zakończone z błędami obiektów blob lub fragmentów.</span><span class="sxs-lookup"><span data-stu-id="85371-227">hello drive has finished with errors in one or more blobs or chunks.</span></span>|  
|`DiskNotFound`|<span data-ttu-id="85371-228">Dysk nie znajduje się na dysku hello.</span><span class="sxs-lookup"><span data-stu-id="85371-228">No disk is found on hello drive.</span></span>|  
|`VolumeNotNtfs`|<span data-ttu-id="85371-229">Hello pierwszy wolumin danych na dysku hello nie jest w formacie NTFS.</span><span class="sxs-lookup"><span data-stu-id="85371-229">hello first data volume on hello disk is not in NTFS format.</span></span>|  
|`DiskOperationFailed`|<span data-ttu-id="85371-230">Wystąpił nieznany błąd podczas wykonywania operacji na powitania dysku.</span><span class="sxs-lookup"><span data-stu-id="85371-230">An unknown failure occurred when performing operations on hello drive.</span></span>|  
|`BitLockerVolumeNotFound`|<span data-ttu-id="85371-231">Znaleziono encryptable woluminu funkcji BitLocker.</span><span class="sxs-lookup"><span data-stu-id="85371-231">No BitLocker encryptable volume is found.</span></span>|  
|`BitLockerNotActivated`|<span data-ttu-id="85371-232">Nie włączono funkcji BitLocker w woluminie hello.</span><span class="sxs-lookup"><span data-stu-id="85371-232">BitLocker is not enabled on hello volume.</span></span>|  
|`BitLockerProtectorNotFound`|<span data-ttu-id="85371-233">Ochrona klucza Hello numerycznym hasłem nie istnieje na woluminie hello.</span><span class="sxs-lookup"><span data-stu-id="85371-233">hello numerical password key protector does not exist on hello volume.</span></span>|  
|`BitLockerKeyInvalid`|<span data-ttu-id="85371-234">podane hasło numeryczne Hello nie można odblokować hello woluminu.</span><span class="sxs-lookup"><span data-stu-id="85371-234">hello numerical password provided cannot unlock hello volume.</span></span>|  
|`BitLockerUnlockVolumeFailed`|<span data-ttu-id="85371-235">Nieznany błąd wystąpił podczas próby toounlock hello woluminu.</span><span class="sxs-lookup"><span data-stu-id="85371-235">Unknown failure has happened when trying toounlock hello volume.</span></span>|  
|`BitLockerFailed`|<span data-ttu-id="85371-236">Wystąpił nieznany błąd podczas wykonywania operacji funkcji BitLocker.</span><span class="sxs-lookup"><span data-stu-id="85371-236">An unknown failure occurred while performing BitLocker operations.</span></span>|  
|`ManifestNameInvalid`|<span data-ttu-id="85371-237">Nazwa pliku manifestu Hello jest nieprawidłowa.</span><span class="sxs-lookup"><span data-stu-id="85371-237">hello manifest file name is invalid.</span></span>|  
|`ManifestNameTooLong`|<span data-ttu-id="85371-238">Nazwa pliku manifestu Hello jest zbyt długa.</span><span class="sxs-lookup"><span data-stu-id="85371-238">hello manifest file name is too long.</span></span>|  
|`ManifestNotFound`|<span data-ttu-id="85371-239">Nie znaleziono pliku manifestu Hello.</span><span class="sxs-lookup"><span data-stu-id="85371-239">hello manifest file is not found.</span></span>|  
|`ManifestAccessDenied`|<span data-ttu-id="85371-240">Odmowa pliku manifestu toohello dostępu.</span><span class="sxs-lookup"><span data-stu-id="85371-240">Access toohello manifest file is denied.</span></span>|  
|`ManifestCorrupted`|<span data-ttu-id="85371-241">Witaj pliku manifestu jest uszkodzony (zawartość hello nie odpowiada jego skrót).</span><span class="sxs-lookup"><span data-stu-id="85371-241">hello manifest file is corrupted (hello content does not match its hash).</span></span>|  
|`ManifestFormatInvalid`|<span data-ttu-id="85371-242">zawartość manifestu Hello jest niezgodny z wymaganym formatem toohello.</span><span class="sxs-lookup"><span data-stu-id="85371-242">hello manifest content does not conform toohello required format.</span></span>|  
|`ManifestDriveIdMismatch`|<span data-ttu-id="85371-243">Witaj Identyfikatora w pliku manifestu hello jest niezgodna z jedną odczytu z dysku hello hello dysku.</span><span class="sxs-lookup"><span data-stu-id="85371-243">hello drive ID in hello manifest file does not match hello one read from hello drive.</span></span>|  
|`ReadManifestFailed`|<span data-ttu-id="85371-244">Wystąpił błąd We/Wy dysku podczas odczytu z hello manifestu.</span><span class="sxs-lookup"><span data-stu-id="85371-244">A disk I/O failure occurred while reading from hello manifest.</span></span>|  
|`BlobListFormatInvalid`|<span data-ttu-id="85371-245">blob listę obiektów blob eksportu Hello jest niezgodny z wymaganym formatem toohello.</span><span class="sxs-lookup"><span data-stu-id="85371-245">hello export blob list blob does not conform toohello required format.</span></span>|  
|`BlobRequestForbidden`|<span data-ttu-id="85371-246">Dostęp do obiektów blob toohello na koncie magazynu hello jest zabronione.</span><span class="sxs-lookup"><span data-stu-id="85371-246">Access toohello blobs in hello storage account is forbidden.</span></span> <span data-ttu-id="85371-247">Może to być klucz konta magazynu tooinvalid lub kontener sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="85371-247">This might be due tooinvalid storage account key or container SAS.</span></span>|  
|`InternalError`|<span data-ttu-id="85371-248">I wystąpił błąd wewnętrzny podczas przetwarzania hello dysku.</span><span class="sxs-lookup"><span data-stu-id="85371-248">And internal error occurred while processing hello drive.</span></span>|  
  
## <a name="blob-status-codes"></a><span data-ttu-id="85371-249">Kody stanu obiektu blob</span><span class="sxs-lookup"><span data-stu-id="85371-249">Blob status codes</span></span>  
<span data-ttu-id="85371-250">Witaj Poniższa tabela zawiera listę kodów stanu hello do przetwarzania obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="85371-250">hello following table lists hello status codes for processing a blob.</span></span>  
  
|<span data-ttu-id="85371-251">Kod stanu</span><span class="sxs-lookup"><span data-stu-id="85371-251">Status code</span></span>|<span data-ttu-id="85371-252">Opis</span><span class="sxs-lookup"><span data-stu-id="85371-252">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="85371-253">Obiekt blob Hello zakończył przetwarzanie bez błędów.</span><span class="sxs-lookup"><span data-stu-id="85371-253">hello blob has finished processing without errors.</span></span>|  
|`CompletedWithErrors`|<span data-ttu-id="85371-254">Obiekt blob Hello zakończył przetwarzanie z błędami w jednej lub więcej zakresów stron lub bloków metadanych i właściwości.</span><span class="sxs-lookup"><span data-stu-id="85371-254">hello blob has finished processing with errors in one or more page ranges or blocks, metadata, or properties.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="85371-255">Nazwa pliku Hello jest nieprawidłowa.</span><span class="sxs-lookup"><span data-stu-id="85371-255">hello file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="85371-256">Nazwa pliku Hello jest zbyt długa.</span><span class="sxs-lookup"><span data-stu-id="85371-256">hello file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="85371-257">Nie znaleziono pliku Hello.</span><span class="sxs-lookup"><span data-stu-id="85371-257">hello file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="85371-258">Odmowa dostępu do pliku toohello.</span><span class="sxs-lookup"><span data-stu-id="85371-258">Access toohello file is denied.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="85371-259">żądanie usługi Blob Hello się, że tooaccess hello obiektów blob nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="85371-259">hello Blob service request tooaccess hello blob has failed.</span></span>|  
|`BlobRequestForbidden`|<span data-ttu-id="85371-260">żądanie usługi Blob Hello się, że tooaccess hello obiektu blob jest zabronione.</span><span class="sxs-lookup"><span data-stu-id="85371-260">hello Blob service request tooaccess hello blob is forbidden.</span></span> <span data-ttu-id="85371-261">Może to być klucz konta magazynu tooinvalid lub kontener sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="85371-261">This might be due tooinvalid storage account key or container SAS.</span></span>|  
|`RenameFailed`|<span data-ttu-id="85371-262">Nie można obiektu blob hello toorename (dla zadania importu) lub pliku hello (dla zadania eksportu).</span><span class="sxs-lookup"><span data-stu-id="85371-262">Failed toorename hello blob (for an import job) or hello file (for an export job).</span></span>|  
|`BlobUnexpectedChange`|<span data-ttu-id="85371-263">Nieoczekiwana zmiana wystąpił błąd związany z obiektu blob hello (dla zadania eksportu).</span><span class="sxs-lookup"><span data-stu-id="85371-263">An unexpected change has occurred with hello blob (for an export job).</span></span>|  
|`LeasePresent`|<span data-ttu-id="85371-264">Brak dzierżawę na powitania obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="85371-264">There is a lease present on hello blob.</span></span>|  
|`IOFailed`|<span data-ttu-id="85371-265">Podczas przetwarzania obiektu blob hello wystąpił dysku lub w sieci, błąd We/Wy.</span><span class="sxs-lookup"><span data-stu-id="85371-265">A disk or network I/O failure occurred while processing hello blob.</span></span>|  
|`Failed`|<span data-ttu-id="85371-266">Wystąpił nieznany błąd podczas przetwarzania hello obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="85371-266">An unknown failure occurred while processing hello blob.</span></span>|  
  
## <a name="import-disposition-status-codes"></a><span data-ttu-id="85371-267">Kody stanu dyspozycji importu</span><span class="sxs-lookup"><span data-stu-id="85371-267">Import disposition status codes</span></span>  
<span data-ttu-id="85371-268">Witaj Poniższa tabela zawiera listę kodów stanu hello w celu rozwiązania dyspozycji importu.</span><span class="sxs-lookup"><span data-stu-id="85371-268">hello following table lists hello status codes for resolving an import disposition.</span></span>  
  
|<span data-ttu-id="85371-269">Kod stanu</span><span class="sxs-lookup"><span data-stu-id="85371-269">Status code</span></span>|<span data-ttu-id="85371-270">Opis</span><span class="sxs-lookup"><span data-stu-id="85371-270">Description</span></span>|  
|-----------------|-----------------|  
|`Created`|<span data-ttu-id="85371-271">Utworzono Hello obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="85371-271">hello blob has been created.</span></span>|  
|`Renamed`|<span data-ttu-id="85371-272">Obiekt blob Hello została zmieniona na dyspozycji importu zmiany nazwy.</span><span class="sxs-lookup"><span data-stu-id="85371-272">hello blob has been renamed per rename import disposition.</span></span> <span data-ttu-id="85371-273">Witaj `Blob/BlobPath` element zawiera hello identyfikator URI obiektu blob hello zmieniono jego nazwę.</span><span class="sxs-lookup"><span data-stu-id="85371-273">hello `Blob/BlobPath` element contains hello URI for hello renamed blob.</span></span>|  
|`Skipped`|<span data-ttu-id="85371-274">Obiekt blob Hello zostało pominięte na `no-overwrite` zaimportować dyspozycji.</span><span class="sxs-lookup"><span data-stu-id="85371-274">hello blob has been skipped per `no-overwrite` import disposition.</span></span>|  
|`Overwritten`|<span data-ttu-id="85371-275">Obiekt blob Hello zastąpiły istniejącym obiektem blob na `overwrite` zaimportować dyspozycji.</span><span class="sxs-lookup"><span data-stu-id="85371-275">hello blob has overwritten an existing blob per `overwrite` import disposition.</span></span>|  
|`Cancelled`|<span data-ttu-id="85371-276">Niepowodzenia wcześniejszego została zatrzymana, dalsze przetwarzanie hello dyspozycji importu.</span><span class="sxs-lookup"><span data-stu-id="85371-276">A prior failure has stopped further processing of hello import disposition.</span></span>|  
  
## <a name="page-rangeblock-status-codes"></a><span data-ttu-id="85371-277">Kody stanu zakres/blok strony</span><span class="sxs-lookup"><span data-stu-id="85371-277">Page range/block status codes</span></span>  
<span data-ttu-id="85371-278">Witaj Poniższa tabela zawiera listę kodów stanu hello przetwarzania strony zakres lub blok.</span><span class="sxs-lookup"><span data-stu-id="85371-278">hello following table lists hello status codes for processing a page range or a block.</span></span>  
  
|<span data-ttu-id="85371-279">Kod stanu</span><span class="sxs-lookup"><span data-stu-id="85371-279">Status code</span></span>|<span data-ttu-id="85371-280">Opis</span><span class="sxs-lookup"><span data-stu-id="85371-280">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="85371-281">Witaj strony zakres lub blok zakończył przetwarzanie bez żadnych błędów.</span><span class="sxs-lookup"><span data-stu-id="85371-281">hello page range or block has finished processing without any errors.</span></span>|  
|`Committed`|<span data-ttu-id="85371-282">Blok Hello został przekazany, ale nie w hello pełne zablokowanych ponieważ inne bloki mają nie powiodło się lub umieść samej listy pełny blok nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="85371-282">hello block has been committed,  but not in hello full block list because other blocks have failed, or put full block list itself has failed.</span></span>|  
|`Uncommitted`|<span data-ttu-id="85371-283">Blok Hello jest przekazany, ale nie zostało zatwierdzone.</span><span class="sxs-lookup"><span data-stu-id="85371-283">hello block is uploaded but not committed.</span></span>|  
|`Corrupted`|<span data-ttu-id="85371-284">Witaj strony zakres lub blok jest uszkodzony (zawartość hello nie odpowiada jego skrót).</span><span class="sxs-lookup"><span data-stu-id="85371-284">hello page range or block is corrupted (hello content does not match its hash).</span></span>|  
|`FileUnexpectedEnd`|<span data-ttu-id="85371-285">Napotkano nieoczekiwany koniec pliku.</span><span class="sxs-lookup"><span data-stu-id="85371-285">An unexpected end of file has been encountered.</span></span>|  
|`BlobUnexpectedEnd`|<span data-ttu-id="85371-286">Napotkano nieoczekiwany koniec obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="85371-286">An unexpected end of blob has been encountered.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="85371-287">Witaj obiektu Blob usługi żądania tooaccess hello zakres stron lub blok nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="85371-287">hello Blob service request tooaccess hello page range or block has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="85371-288">Podczas przetwarzania hello strony zakres lub blok wystąpił dysku lub w sieci, błąd We/Wy.</span><span class="sxs-lookup"><span data-stu-id="85371-288">A disk or network I/O failure occurred while processing hello page range or block.</span></span>|  
|`Failed`|<span data-ttu-id="85371-289">Wystąpił nieznany błąd podczas przetwarzania hello strony zakres lub blok.</span><span class="sxs-lookup"><span data-stu-id="85371-289">An unknown failure occurred while processing hello page range or block.</span></span>|  
|`Cancelled`|<span data-ttu-id="85371-290">Błąd przed została zatrzymana, dalsze przetwarzanie hello strony zakres lub blok.</span><span class="sxs-lookup"><span data-stu-id="85371-290">A prior failure has stopped further processing of hello page range or block.</span></span>|  
  
## <a name="metadata-status-codes"></a><span data-ttu-id="85371-291">Kody stanu metadanych</span><span class="sxs-lookup"><span data-stu-id="85371-291">Metadata status codes</span></span>  
<span data-ttu-id="85371-292">Witaj Poniższa tabela zawiera listę kodów stanu powitania dla przetwarzania metadane obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="85371-292">hello following table lists hello status codes for processing blob metadata.</span></span>  
  
|<span data-ttu-id="85371-293">Kod stanu</span><span class="sxs-lookup"><span data-stu-id="85371-293">Status code</span></span>|<span data-ttu-id="85371-294">Opis</span><span class="sxs-lookup"><span data-stu-id="85371-294">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="85371-295">metadane Hello zakończył przetwarzanie bez błędów.</span><span class="sxs-lookup"><span data-stu-id="85371-295">hello metadata has finished processing without errors.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="85371-296">Nazwa pliku metadanych Hello jest nieprawidłowa.</span><span class="sxs-lookup"><span data-stu-id="85371-296">hello metadata file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="85371-297">Nazwa pliku metadanych Hello jest zbyt długa.</span><span class="sxs-lookup"><span data-stu-id="85371-297">hello metadata file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="85371-298">Nie znaleziono pliku metadanych Hello.</span><span class="sxs-lookup"><span data-stu-id="85371-298">hello metadata file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="85371-299">Odmowa dostępu toohello metadane pliku.</span><span class="sxs-lookup"><span data-stu-id="85371-299">Access toohello metadata file is denied.</span></span>|  
|`Corrupted`|<span data-ttu-id="85371-300">Plik metadanych Hello jest uszkodzony (zawartość hello nie odpowiada jego skrót).</span><span class="sxs-lookup"><span data-stu-id="85371-300">hello metadata file is corrupted (hello content does not match its hash).</span></span>|  
|`XmlReadFailed`|<span data-ttu-id="85371-301">Hello metadane zawartości jest niezgodny z wymaganym formatem toohello.</span><span class="sxs-lookup"><span data-stu-id="85371-301">hello metadata content does not conform toohello required format.</span></span>|  
|`XmlWriteFailed`|<span data-ttu-id="85371-302">Zapisywanie metadanych hello XML nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="85371-302">Writing hello metadata XML has failed.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="85371-303">żądanie usługi Blob Hello się, że tooaccess hello metadanych nie powiodła się.</span><span class="sxs-lookup"><span data-stu-id="85371-303">hello Blob service request tooaccess hello metadata has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="85371-304">Podczas przetwarzania metadanych hello wystąpił błąd We/Wy dysku lub w sieci.</span><span class="sxs-lookup"><span data-stu-id="85371-304">A disk or network I/O failure occurred while processing hello metadata.</span></span>|  
|`Failed`|<span data-ttu-id="85371-305">Wystąpił nieznany błąd podczas przetwarzania hello metadanych.</span><span class="sxs-lookup"><span data-stu-id="85371-305">An unknown failure occurred while processing hello metadata.</span></span>|  
|`Cancelled`|<span data-ttu-id="85371-306">Błąd przed została zatrzymana, dalsze przetwarzanie hello metadanych.</span><span class="sxs-lookup"><span data-stu-id="85371-306">A prior failure has stopped further processing of hello metadata.</span></span>|  
  
## <a name="properties-status-codes"></a><span data-ttu-id="85371-307">Kody stanu właściwości</span><span class="sxs-lookup"><span data-stu-id="85371-307">Properties status codes</span></span>  
<span data-ttu-id="85371-308">Witaj Poniższa tabela zawiera listę kodów stanu hello przetwarzania właściwości obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="85371-308">hello following table lists hello status codes for processing blob properties.</span></span>  
  
|<span data-ttu-id="85371-309">Kod stanu</span><span class="sxs-lookup"><span data-stu-id="85371-309">Status code</span></span>|<span data-ttu-id="85371-310">Opis</span><span class="sxs-lookup"><span data-stu-id="85371-310">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="85371-311">właściwości Hello Zakończono przetwarzanie bez żadnych błędów.</span><span class="sxs-lookup"><span data-stu-id="85371-311">hello properties have finished processing without any errors.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="85371-312">Nazwa pliku właściwości Hello jest nieprawidłowa.</span><span class="sxs-lookup"><span data-stu-id="85371-312">hello properties file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="85371-313">Nazwa pliku właściwości Hello jest zbyt długa.</span><span class="sxs-lookup"><span data-stu-id="85371-313">hello properties file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="85371-314">Nie znaleziono Hello właściwości pliku.</span><span class="sxs-lookup"><span data-stu-id="85371-314">hello properties file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="85371-315">Odmowa dostępu toohello właściwości pliku.</span><span class="sxs-lookup"><span data-stu-id="85371-315">Access toohello properties file is denied.</span></span>|  
|`Corrupted`|<span data-ttu-id="85371-316">Plik właściwości Hello jest uszkodzony (zawartość hello nie odpowiada jego skrót).</span><span class="sxs-lookup"><span data-stu-id="85371-316">hello properties file is corrupted (hello content does not match its hash).</span></span>|  
|`XmlReadFailed`|<span data-ttu-id="85371-317">Hello właściwości zawartości jest niezgodny z wymaganym formatem toohello.</span><span class="sxs-lookup"><span data-stu-id="85371-317">hello properties content does not conform toohello required format.</span></span>|  
|`XmlWriteFailed`|<span data-ttu-id="85371-318">Zapisywanie właściwości hello XML nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="85371-318">Writing hello properties XML has failed.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="85371-319">żądanie usługi Blob Hello się, że tooaccess hello właściwości nie powiodła się.</span><span class="sxs-lookup"><span data-stu-id="85371-319">hello Blob service request tooaccess hello properties has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="85371-320">Wystąpił błąd We/Wy dysku lub w sieci podczas przetwarzania hello właściwości.</span><span class="sxs-lookup"><span data-stu-id="85371-320">A disk or network I/O failure occurred while processing hello properties.</span></span>|  
|`Failed`|<span data-ttu-id="85371-321">Wystąpił nieznany błąd podczas przetwarzania hello właściwości.</span><span class="sxs-lookup"><span data-stu-id="85371-321">An unknown failure occurred while processing hello properties.</span></span>|  
|`Cancelled`|<span data-ttu-id="85371-322">Błąd przed została zatrzymana, dalsze przetwarzanie hello właściwości.</span><span class="sxs-lookup"><span data-stu-id="85371-322">A prior failure has stopped further processing of hello properties.</span></span>|  
  
## <a name="sample-logs"></a><span data-ttu-id="85371-323">Dzienniki próbki</span><span class="sxs-lookup"><span data-stu-id="85371-323">Sample logs</span></span>  
<span data-ttu-id="85371-324">Hello Oto przykład pełnego dziennika.</span><span class="sxs-lookup"><span data-stu-id="85371-324">hello following is an example of verbose log.</span></span>  
  
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
  
<span data-ttu-id="85371-325">Poniżej przedstawiono Hello odpowiedni dziennik błędów.</span><span class="sxs-lookup"><span data-stu-id="85371-325">hello corresponding error log is shown below.</span></span>  
  
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

 <span data-ttu-id="85371-326">Dziennik błędów wykonaj powitania dla zadania importu zawiera błąd o pliku nie można odnaleźć na powitania importowania dysku.</span><span class="sxs-lookup"><span data-stu-id="85371-326">hello follow error log for an import job contains an error about a file not found on hello import drive.</span></span> <span data-ttu-id="85371-327">Należy pamiętać, że stan hello kolejnych składników `Cancelled`.</span><span class="sxs-lookup"><span data-stu-id="85371-327">Note that hello status of subsequent components is `Cancelled`.</span></span>  
  
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

<span data-ttu-id="85371-328">Hello następujące dziennik błędów dla zadania eksportu wskazuje, czy zawartość obiektu blob hello został zapisany pomyślnie toohello dysku, ale że wystąpił błąd podczas eksportowania właściwości hello obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="85371-328">hello following error log for an export job indicates that hello blob content has been successfully written toohello drive, but that an error occurred while exporting hello blob's properties.</span></span>  
  
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
  
## <a name="next-steps"></a><span data-ttu-id="85371-329">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="85371-329">Next steps</span></span>
 
* [<span data-ttu-id="85371-330">Interfejs API REST importu/eksportu magazynu</span><span class="sxs-lookup"><span data-stu-id="85371-330">Storage Import/Export REST API</span></span>](/rest/api/storageimportexport/)
