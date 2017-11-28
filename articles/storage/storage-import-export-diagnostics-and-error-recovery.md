---
title: "aaaDiagnostics i błąd odzyskiwania dla zadań Import/Eksport Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooenable pełne rejestrowanie dla programu Microsoft Azure Import/Eksport usługi zadania."
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
ms.openlocfilehash: 48164279e7904c78fed802aa3cff66e589c3f12c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-and-error-recovery-for-azure-importexport-jobs"></a><span data-ttu-id="a0b6e-103">Diagnostyka i błąd odzyskiwania dla zadań Import/Eksport Azure</span><span class="sxs-lookup"><span data-stu-id="a0b6e-103">Diagnostics and error recovery for Azure Import/Export jobs</span></span>
<span data-ttu-id="a0b6e-104">Dla każdego dysku przetwarzane hello usługi Import/Eksport Azure tworzy dziennik błędów w hello skojarzone konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-104">For each drive processed, hello Azure Import/Export service creates an error log in hello associated storage account.</span></span> <span data-ttu-id="a0b6e-105">Można również włączyć pełne rejestrowanie przez ustawienie hello `LogLevel` właściwości zbyt`Verbose` podczas wywoływania metody hello [zawiesić zadanie](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) lub [właściwości zadania aktualizacji](/rest/api/storageimportexport/jobs#Jobs_Update) operacji.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-105">You can also enable verbose logging by setting hello `LogLevel` property too`Verbose` when calling hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operations.</span></span>

 <span data-ttu-id="a0b6e-106">Domyślnie dzienniki są zapisywane tooa kontener o nazwie `waimportexport`.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-106">By default, logs are written tooa container named `waimportexport`.</span></span> <span data-ttu-id="a0b6e-107">Określ inną nazwę, przez ustawienie hello `DiagnosticsPath` właściwości podczas wywoływania metody hello `Put Job` lub `Update Job Properties` operacji.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-107">You can specify a different name by setting hello `DiagnosticsPath` property when calling hello `Put Job` or `Update Job Properties` operations.</span></span> <span data-ttu-id="a0b6e-108">Witaj dzienniki są przechowywane jako blokowych obiektów blob z następującą konwencją hello: `waies/jobname_driveid_timestamp_logtype.xml`.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-108">hello logs are stored as block blobs with hello following naming convention: `waies/jobname_driveid_timestamp_logtype.xml`.</span></span>

 <span data-ttu-id="a0b6e-109">Możesz pobrać hello URI hello dzienników zadania przez wywołanie hello [pobrania zadania](/rest/api/storageimportexport/jobs#Jobs_Get) operacji.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-109">You can retrieve hello URI of hello logs for a job by calling hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="a0b6e-110">Hello identyfikatora URI dla pełnego dziennika hello jest zwracany w hello `VerboseLogUri` właściwości dla każdego dysku, gdy hello identyfikator URI do dziennika błędów hello jest zwracany w hello `ErrorLogUri` właściwości.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-110">hello URI for hello verbose log is returned in hello `VerboseLogUri` property for each drive, while hello URI for hello error log is returned in hello `ErrorLogUri` property.</span></span>

<span data-ttu-id="a0b6e-111">Możesz użyć hello rejestrowania danych tooidentify hello następujące problemy.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-111">You can use hello logging data tooidentify hello following issues.</span></span>

## <a name="drive-errors"></a><span data-ttu-id="a0b6e-112">Błędy dysku</span><span class="sxs-lookup"><span data-stu-id="a0b6e-112">Drive errors</span></span>

<span data-ttu-id="a0b6e-113">Witaj w poniższych elementach sklasyfikowanych jako błędy dysku:</span><span class="sxs-lookup"><span data-stu-id="a0b6e-113">hello following items are classified as drive errors:</span></span>

-   <span data-ttu-id="a0b6e-114">Błędy podczas uzyskiwania dostępu do lub odczytywania hello pliku manifestu</span><span class="sxs-lookup"><span data-stu-id="a0b6e-114">Errors in accessing or reading hello manifest file</span></span>

-   <span data-ttu-id="a0b6e-115">Niepoprawne klucze funkcji BitLocker</span><span class="sxs-lookup"><span data-stu-id="a0b6e-115">Incorrect BitLocker keys</span></span>

-   <span data-ttu-id="a0b6e-116">Błędy odczytu/zapisu dysków</span><span class="sxs-lookup"><span data-stu-id="a0b6e-116">Drive read/write errors</span></span>

## <a name="blob-errors"></a><span data-ttu-id="a0b6e-117">Błędy obiektów blob</span><span class="sxs-lookup"><span data-stu-id="a0b6e-117">Blob errors</span></span>

<span data-ttu-id="a0b6e-118">Witaj w poniższych elementach sklasyfikowanych jako błędy obiektów blob:</span><span class="sxs-lookup"><span data-stu-id="a0b6e-118">hello following items are classified as blob errors:</span></span>

-   <span data-ttu-id="a0b6e-119">Nazwy lub nieprawidłowa / sprzeczna obiektów blob</span><span class="sxs-lookup"><span data-stu-id="a0b6e-119">Incorrect or conflicting blob or names</span></span>

-   <span data-ttu-id="a0b6e-120">Brakujące pliki</span><span class="sxs-lookup"><span data-stu-id="a0b6e-120">Missing files</span></span>

-   <span data-ttu-id="a0b6e-121">Nie znaleziono obiektu blob</span><span class="sxs-lookup"><span data-stu-id="a0b6e-121">Blob not found</span></span>

-   <span data-ttu-id="a0b6e-122">Skrócona plików (hello plików na dysku hello są mniejsze niż określona w manifeście hello)</span><span class="sxs-lookup"><span data-stu-id="a0b6e-122">Truncated files (hello files on hello disk are smaller than specified in hello manifest)</span></span>

-   <span data-ttu-id="a0b6e-123">Uszkodzony plik zawartości (dla zadania importu wykrył z sumy kontrolnej MD5)</span><span class="sxs-lookup"><span data-stu-id="a0b6e-123">Corrupted file content (for import jobs, detected with an MD5 checksum mismatch)</span></span>

-   <span data-ttu-id="a0b6e-124">Pliki metadanych i właściwości uszkodzony obiekt blob (wykrył z sumy kontrolnej MD5)</span><span class="sxs-lookup"><span data-stu-id="a0b6e-124">Corrupted blob metadata and property files (detected with an MD5 checksum mismatch)</span></span>

-   <span data-ttu-id="a0b6e-125">Niepoprawny schemat dla właściwości obiektu blob hello i/lub pliki metadanych</span><span class="sxs-lookup"><span data-stu-id="a0b6e-125">Incorrect schema for hello blob properties and/or metadata files</span></span>

<span data-ttu-id="a0b6e-126">Może to być przypadki, w którym niektórych części zadania importu lub eksportu nie zostało prawidłowo wykonane, hello ogólne zadanie nadal zakończy pracę.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-126">There may be cases where some parts of an import or export job do not complete successfully, while hello overall job still completes.</span></span> <span data-ttu-id="a0b6e-127">W takim przypadku możesz przekazać lub pobrać hello Brak fragmentów danych hello za pośrednictwem sieci, lub można utworzyć nowe dane hello tootransfer zadania.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-127">In this case, you can either upload or download hello missing pieces of hello data over network, or you can create a new job tootransfer hello data.</span></span> <span data-ttu-id="a0b6e-128">Zobacz hello [odwołania narzędzie importu/eksportu Azure](storage-import-export-tool-how-to-v1.md) toolearn jak toorepair hello danych za pośrednictwem sieci.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-128">See hello [Azure Import/Export Tool Reference](storage-import-export-tool-how-to-v1.md) toolearn how toorepair hello data over network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a0b6e-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a0b6e-129">Next steps</span></span>

* [<span data-ttu-id="a0b6e-130">Przy użyciu interfejsu API REST usługi Import/Eksport hello</span><span class="sxs-lookup"><span data-stu-id="a0b6e-130">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
