---
title: "Diagnostyka i błąd odzyskiwania dla zadań Import/Eksport Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak włączyć pełne rejestrowanie dla zadania usługi Import/Eksport Microsoft Azure."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 096cc795-9af6-4335-9fe8-fffa9f239a17
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 0068aae9d6780aa41a070db0eb191d0d5a165d21
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="diagnostics-and-error-recovery-for-azure-importexport-jobs"></a><span data-ttu-id="eeb74-103">Diagnostyka i błąd odzyskiwania dla zadań Import/Eksport Azure</span><span class="sxs-lookup"><span data-stu-id="eeb74-103">Diagnostics and error recovery for Azure Import/Export jobs</span></span>
<span data-ttu-id="eeb74-104">Dla każdego dysku przetwarzane usługi Import/Eksport Azure tworzy dziennik błędów w skojarzonego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="eeb74-104">For each drive processed, the Azure Import/Export service creates an error log in the associated storage account.</span></span> <span data-ttu-id="eeb74-105">Można również włączyć pełne rejestrowanie, ustawiając `LogLevel` właściwości `Verbose` podczas wywoływania metody [zawiesić zadanie](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) lub [właściwości zadania aktualizacji](/rest/api/storageimportexport/jobs#Jobs_Update) operacji.</span><span class="sxs-lookup"><span data-stu-id="eeb74-105">You can also enable verbose logging by setting the `LogLevel` property to `Verbose` when calling the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operations.</span></span>

 <span data-ttu-id="eeb74-106">Domyślnie dzienniki są zapisywane do kontenera o nazwie `waimportexport`.</span><span class="sxs-lookup"><span data-stu-id="eeb74-106">By default, logs are written to a container named `waimportexport`.</span></span> <span data-ttu-id="eeb74-107">Można określić inną nazwę, ustawiając `DiagnosticsPath` właściwości podczas wywoływania metody `Put Job` lub `Update Job Properties` operacji.</span><span class="sxs-lookup"><span data-stu-id="eeb74-107">You can specify a different name by setting the `DiagnosticsPath` property when calling the `Put Job` or `Update Job Properties` operations.</span></span> <span data-ttu-id="eeb74-108">Dzienniki są przechowywane jako blokowych obiektów blob z następującą konwencją nazewnictwa: `waies/jobname_driveid_timestamp_logtype.xml`.</span><span class="sxs-lookup"><span data-stu-id="eeb74-108">The logs are stored as block blobs with the following naming convention: `waies/jobname_driveid_timestamp_logtype.xml`.</span></span>

 <span data-ttu-id="eeb74-109">Można pobrać identyfikatora URI dzienników zadania przez wywołanie metody [pobrania zadania](/rest/api/storageimportexport/jobs#Jobs_Get) operacji.</span><span class="sxs-lookup"><span data-stu-id="eeb74-109">You can retrieve the URI of the logs for a job by calling the [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="eeb74-110">Identyfikator URI dla pełnego dziennika jest zwracany w `VerboseLogUri` właściwości dla każdego dysku, podczas gdy identyfikator URI dla dziennik błędów, jest zwracany w `ErrorLogUri` właściwości.</span><span class="sxs-lookup"><span data-stu-id="eeb74-110">The URI for the verbose log is returned in the `VerboseLogUri` property for each drive, while the URI for the error log is returned in the `ErrorLogUri` property.</span></span>

<span data-ttu-id="eeb74-111">Dane rejestrowania służy do identyfikowania następujące problemy.</span><span class="sxs-lookup"><span data-stu-id="eeb74-111">You can use the logging data to identify the following issues.</span></span>

## <a name="drive-errors"></a><span data-ttu-id="eeb74-112">Błędy dysku</span><span class="sxs-lookup"><span data-stu-id="eeb74-112">Drive errors</span></span>

<span data-ttu-id="eeb74-113">Następujące elementy sklasyfikowanych jako błędy dysku:</span><span class="sxs-lookup"><span data-stu-id="eeb74-113">The following items are classified as drive errors:</span></span>

-   <span data-ttu-id="eeb74-114">Błędy podczas uzyskiwania dostępu do lub odczytywania pliku manifestu</span><span class="sxs-lookup"><span data-stu-id="eeb74-114">Errors in accessing or reading the manifest file</span></span>

-   <span data-ttu-id="eeb74-115">Niepoprawne klucze funkcji BitLocker</span><span class="sxs-lookup"><span data-stu-id="eeb74-115">Incorrect BitLocker keys</span></span>

-   <span data-ttu-id="eeb74-116">Błędy odczytu/zapisu dysków</span><span class="sxs-lookup"><span data-stu-id="eeb74-116">Drive read/write errors</span></span>

## <a name="blob-errors"></a><span data-ttu-id="eeb74-117">Błędy obiektów blob</span><span class="sxs-lookup"><span data-stu-id="eeb74-117">Blob errors</span></span>

<span data-ttu-id="eeb74-118">Następujące elementy sklasyfikowanych jako błędy obiektów blob:</span><span class="sxs-lookup"><span data-stu-id="eeb74-118">The following items are classified as blob errors:</span></span>

-   <span data-ttu-id="eeb74-119">Nazwy lub nieprawidłowa / sprzeczna obiektów blob</span><span class="sxs-lookup"><span data-stu-id="eeb74-119">Incorrect or conflicting blob or names</span></span>

-   <span data-ttu-id="eeb74-120">Brakujące pliki</span><span class="sxs-lookup"><span data-stu-id="eeb74-120">Missing files</span></span>

-   <span data-ttu-id="eeb74-121">Nie znaleziono obiektu blob</span><span class="sxs-lookup"><span data-stu-id="eeb74-121">Blob not found</span></span>

-   <span data-ttu-id="eeb74-122">Skrócona plików (pliki na dysku są mniejsze niż określona w manifeście)</span><span class="sxs-lookup"><span data-stu-id="eeb74-122">Truncated files (the files on the disk are smaller than specified in the manifest)</span></span>

-   <span data-ttu-id="eeb74-123">Uszkodzony plik zawartości (dla zadania importu wykrył z sumy kontrolnej MD5)</span><span class="sxs-lookup"><span data-stu-id="eeb74-123">Corrupted file content (for import jobs, detected with an MD5 checksum mismatch)</span></span>

-   <span data-ttu-id="eeb74-124">Pliki metadanych i właściwości uszkodzony obiekt blob (wykrył z sumy kontrolnej MD5)</span><span class="sxs-lookup"><span data-stu-id="eeb74-124">Corrupted blob metadata and property files (detected with an MD5 checksum mismatch)</span></span>

-   <span data-ttu-id="eeb74-125">Niepoprawny schemat dla właściwości obiektów blob i/lub pliki metadanych</span><span class="sxs-lookup"><span data-stu-id="eeb74-125">Incorrect schema for the blob properties and/or metadata files</span></span>

<span data-ttu-id="eeb74-126">Może to być przypadki, w którym niektórych części zadania importu lub eksportu nie zostało prawidłowo wykonane, ogólną zadanie nadal zakończy pracę.</span><span class="sxs-lookup"><span data-stu-id="eeb74-126">There may be cases where some parts of an import or export job do not complete successfully, while the overall job still completes.</span></span> <span data-ttu-id="eeb74-127">W takim przypadku możesz przekazać lub pobrać brakujące fragmenty danych za pośrednictwem sieci, lub można utworzyć nowe zadanie do transferu danych.</span><span class="sxs-lookup"><span data-stu-id="eeb74-127">In this case, you can either upload or download the missing pieces of the data over network, or you can create a new job to transfer the data.</span></span> <span data-ttu-id="eeb74-128">Zobacz [odwołania narzędzie importu/eksportu Azure](storage-import-export-tool-how-to-v1.md) informacje na temat naprawy danych za pośrednictwem sieci.</span><span class="sxs-lookup"><span data-stu-id="eeb74-128">See the [Azure Import/Export Tool Reference](storage-import-export-tool-how-to-v1.md) to learn how to repair the data over network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eeb74-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="eeb74-129">Next steps</span></span>

* [<span data-ttu-id="eeb74-130">Przy użyciu interfejsu API REST usługi Import/Eksport</span><span class="sxs-lookup"><span data-stu-id="eeb74-130">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
