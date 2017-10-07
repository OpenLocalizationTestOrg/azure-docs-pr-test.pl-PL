---
title: aaaCreate zadania importu dla Import/Eksport Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toocreate importu dla hello usługi Import/Eksport Microsoft Azure."
author: muralikk
manager: syadav
editor: syadav
services: storage
documentationcenter: 
ms.assetid: 8b886e83-6148-4149-9d0f-5d48ec822475
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: da974c33a3688bb5e2412c8bfcbeca704096c2fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-import-job-for-hello-azure-importexport-service"></a><span data-ttu-id="303b8-103">Tworzenie zadania importu dla hello usługi Import/Eksport Azure</span><span class="sxs-lookup"><span data-stu-id="303b8-103">Creating an import job for hello Azure Import/Export service</span></span>

<span data-ttu-id="303b8-104">Tworzenie zadania importu za pomocą hello interfejsu API REST usługi Import/Eksport Microsoft Azure hello obejmuje hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="303b8-104">Creating an import job for hello Microsoft Azure Import/Export service using hello REST API involves hello following steps:</span></span>

-   <span data-ttu-id="303b8-105">Przygotowywanie stacje z hello Azure narzędzie importu/eksportu.</span><span class="sxs-lookup"><span data-stu-id="303b8-105">Preparing drives with hello Azure Import/Export Tool.</span></span>

-   <span data-ttu-id="303b8-106">Uzyskiwanie hello lokalizacji toowhich tooship hello dysku.</span><span class="sxs-lookup"><span data-stu-id="303b8-106">Obtaining hello location toowhich tooship hello drive.</span></span>

-   <span data-ttu-id="303b8-107">Tworzenie zadania importu hello.</span><span class="sxs-lookup"><span data-stu-id="303b8-107">Creating hello import job.</span></span>

-   <span data-ttu-id="303b8-108">Wysyłanie hello dysków tooMicrosoft za pomocą usługi obsługiwane operatora.</span><span class="sxs-lookup"><span data-stu-id="303b8-108">Shipping hello drives tooMicrosoft via a supported carrier service.</span></span>

-   <span data-ttu-id="303b8-109">Uaktualnianie zadania importu hello hello szczegóły wysyłki.</span><span class="sxs-lookup"><span data-stu-id="303b8-109">Updating hello import job with hello shipping details.</span></span>

 <span data-ttu-id="303b8-110">Zobacz [przy użyciu hello Import/Eksport Microsoft Azure service tooTransfer danych tooBlob magazynu](storage-import-export-service.md) Omówienie usługi Import/Eksport hello i samouczek, który demonstruje sposób toouse hello [portalu Azure](https://portal.azure.com/) toocreate i zarządzanie importowanie i eksportowanie zadań.</span><span class="sxs-lookup"><span data-stu-id="303b8-110">See [Using hello Microsoft Azure Import/Export service tooTransfer Data tooBlob Storage](storage-import-export-service.md) for an overview of hello Import/Export service and a tutorial that demonstrates how toouse hello [Azure  portal](https://portal.azure.com/) toocreate and manage import and export jobs.</span></span>

## <a name="preparing-drives-with-hello-azure-importexport-tool"></a><span data-ttu-id="303b8-111">Przygotowywanie stacje z hello Azure narzędzie importu/eksportu</span><span class="sxs-lookup"><span data-stu-id="303b8-111">Preparing drives with hello Azure Import/Export Tool</span></span>

<span data-ttu-id="303b8-112">Witaj kroki tooprepare dysków dla zadania importu są hello sama czy tworzyć hello jobvia hello portalu lub za pośrednictwem hello interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="303b8-112">hello steps tooprepare drives for an import job are hello same whether you create hello jobvia hello portal or via hello REST API.</span></span>

<span data-ttu-id="303b8-113">Poniżej znajduje się krótki przegląd Przygotowanie stacji.</span><span class="sxs-lookup"><span data-stu-id="303b8-113">Below is a brief overview of drive preparation.</span></span> <span data-ttu-id="303b8-114">Zobacz toohello [odwołania ExportTool importu Azure](storage-import-export-tool-how-to-v1.md) Aby uzyskać pełne instrukcje.</span><span class="sxs-lookup"><span data-stu-id="303b8-114">Refer toohello [Azure Import-ExportTool Reference](storage-import-export-tool-how-to-v1.md) for complete instructions.</span></span> <span data-ttu-id="303b8-115">Możesz pobrać hello Azure narzędzie importu/eksportu [tutaj](http://go.microsoft.com/fwlink/?LinkID=301900).</span><span class="sxs-lookup"><span data-stu-id="303b8-115">You can download hello Azure Import/Export Tool [here](http://go.microsoft.com/fwlink/?LinkID=301900).</span></span>

<span data-ttu-id="303b8-116">Przygotowywanie dysku obejmuje:</span><span class="sxs-lookup"><span data-stu-id="303b8-116">Preparing your drive involves:</span></span>

-   <span data-ttu-id="303b8-117">Toobe dane identyfikacyjne hello zaimportowane.</span><span class="sxs-lookup"><span data-stu-id="303b8-117">Identifying hello data toobe imported.</span></span>

-   <span data-ttu-id="303b8-118">Identyfikowanie hello docelowego BLOB w magazynie Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="303b8-118">Identifying hello destination blobs in Windows Azure Storage.</span></span>

-   <span data-ttu-id="303b8-119">Przy użyciu hello Azure narzędzie importu/eksportu toocopy Twojego tooone danych lub większej liczby dysków twardych.</span><span class="sxs-lookup"><span data-stu-id="303b8-119">Using hello Azure Import/Export Tool toocopy your data tooone or more hard drives.</span></span>

 <span data-ttu-id="303b8-120">Hello Azure narzędzie importu/eksportu również spowoduje wygenerowanie pliku manifestu dla poszczególnych dysków hello, jak jest przygotowana.</span><span class="sxs-lookup"><span data-stu-id="303b8-120">hello Azure Import/Export Tool will also generate a manifest file for each of hello drives as it is prepared.</span></span> <span data-ttu-id="303b8-121">Plik manifestu zawiera:</span><span class="sxs-lookup"><span data-stu-id="303b8-121">A manifest file contains:</span></span>

-   <span data-ttu-id="303b8-122">Wyliczenie wszystkich plików hello przeznaczonych do przekazywania i mapowania hello z tooblobs tych plików.</span><span class="sxs-lookup"><span data-stu-id="303b8-122">An enumeration of all hello files intended for upload and hello mappings from these files tooblobs.</span></span>

-   <span data-ttu-id="303b8-123">Sum kontrolnych segmentów hello każdego pliku.</span><span class="sxs-lookup"><span data-stu-id="303b8-123">Checksums of hello segments of each file.</span></span>

-   <span data-ttu-id="303b8-124">Informacje o metadanych i właściwości tooassociate hello z każdy obiekt blob.</span><span class="sxs-lookup"><span data-stu-id="303b8-124">Information about hello metadata and properties tooassociate with each blob.</span></span>

-   <span data-ttu-id="303b8-125">Lista tootake akcji hello Jeśli obiektu blob, który jest przekazywanych ma hello takie same nazwy jako istniejącym obiektem blob w kontenerze hello.</span><span class="sxs-lookup"><span data-stu-id="303b8-125">A listing of hello action tootake if a blob that is being uploaded has hello same name as an existing blob in hello container.</span></span> <span data-ttu-id="303b8-126">Dostępne są opcje:) Zastąp hello blob pliku hello, (b) zachować hello istniejących obiektów blob i Pomiń przekazywanie pliku hello, c) dołączyć nazwę toohello sufiksu tak, aby nie powoduje konfliktu z innymi plikami.</span><span class="sxs-lookup"><span data-stu-id="303b8-126">Possible options are: a) overwrite hello blob with hello file, b) keep hello existing blob and skip uploading hello file, c) append a suffix toohello name so that it does not conflict with other files.</span></span>

## <a name="obtaining-your-shipping-location"></a><span data-ttu-id="303b8-127">Uzyskiwanie lokalizacji wysyłki</span><span class="sxs-lookup"><span data-stu-id="303b8-127">Obtaining your shipping location</span></span>

<span data-ttu-id="303b8-128">Przed utworzeniem zadania importu, należy tooobtain wysyłanie nazwy lokalizacji i adres przez wywołanie hello [lokalizacje listy](/rest/api/storageimportexport/listlocations) operacji.</span><span class="sxs-lookup"><span data-stu-id="303b8-128">Before creating an import job, you need tooobtain a shipping location name and address by calling hello [List Locations](/rest/api/storageimportexport/listlocations) operation.</span></span> <span data-ttu-id="303b8-129">`List Locations`Zwraca listę lokalizacje i ich adres wysyłkowy.</span><span class="sxs-lookup"><span data-stu-id="303b8-129">`List Locations` will return a list of locations and their mailing addresses.</span></span> <span data-ttu-id="303b8-130">Można wybrać lokalizację z hello zwrócił listę i dostarczać adres toothat dysków twardych.</span><span class="sxs-lookup"><span data-stu-id="303b8-130">You can select a location from hello returned list and ship your hard drives toothat address.</span></span> <span data-ttu-id="303b8-131">Można również użyć hello `Get Location` hello tooobtain operacji wysyłania bezpośrednio adres dla określonej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="303b8-131">You can also use hello `Get Location` operation tooobtain hello shipping address for a specific location directly.</span></span>

 <span data-ttu-id="303b8-132">Wykonaj kroki hello poniżej tooobtain hello wysyłanie lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="303b8-132">Follow hello steps below tooobtain hello shipping location:</span></span>

-   <span data-ttu-id="303b8-133">Określ nazwę hello hello Lokalizacja konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="303b8-133">Identify hello name of hello location of your storage account.</span></span> <span data-ttu-id="303b8-134">Tę wartość można znaleźć w hello **lokalizacji** na konto magazynu hello **pulpitu nawigacyjnego** w hello Azure portalu lub, którego dotyczy kwerenda dla za pomocą zarządzania usługami hello operacji interfejsu API [uzyskiwanie magazynów Właściwości konta](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span><span class="sxs-lookup"><span data-stu-id="303b8-134">This value can be found under hello **Location** field on hello storage account's **Dashboard** in hello Azure portal or queried for by using hello service management API operation [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span></span>

-   <span data-ttu-id="303b8-135">Pobrać hello lokalizacji, która jest dostępna tooprocess tego konta magazynu przez wywołanie hello `Get Location` operacji.</span><span class="sxs-lookup"><span data-stu-id="303b8-135">Retrieve hello location that is available tooprocess this storage account by calling hello `Get Location` operation.</span></span>

-   <span data-ttu-id="303b8-136">Jeśli hello `AlternateLocations` właściwość lokalizacji hello zawiera samą powitalnych lokalizację, a następnie jest poprawny toouse tej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="303b8-136">If hello `AlternateLocations` property of hello location contains hello location itself, then it is okay toouse this location.</span></span> <span data-ttu-id="303b8-137">W przeciwnym razie wywołać hello `Get Location` ponownie operację, używając jednej z hello lokalizacji alternatywnej.</span><span class="sxs-lookup"><span data-stu-id="303b8-137">Otherwise, call hello `Get Location` operation again with one of hello alternate locations.</span></span> <span data-ttu-id="303b8-138">Hello oryginalnej lokalizacji może być tymczasowo zamknięte konserwacji.</span><span class="sxs-lookup"><span data-stu-id="303b8-138">hello original location might be temporarily closed for maintenance.</span></span>

## <a name="creating-hello-import-job"></a><span data-ttu-id="303b8-139">Tworzenie zadania importu hello</span><span class="sxs-lookup"><span data-stu-id="303b8-139">Creating hello import job</span></span>
<span data-ttu-id="303b8-140">zadania importu hello toocreate, wywołanie hello [zawiesić zadanie](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operacji.</span><span class="sxs-lookup"><span data-stu-id="303b8-140">toocreate hello import job, call hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="303b8-141">Konieczne będzie hello tooprovide następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="303b8-141">You will need tooprovide hello following information:</span></span>

-   <span data-ttu-id="303b8-142">Nazwa zadania hello.</span><span class="sxs-lookup"><span data-stu-id="303b8-142">A name for hello job.</span></span>

-   <span data-ttu-id="303b8-143">Nazwa konta magazynu Hello.</span><span class="sxs-lookup"><span data-stu-id="303b8-143">hello storage account name.</span></span>

-   <span data-ttu-id="303b8-144">Witaj wysyłania nazwy lokalizacji, uzyskane w poprzednim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="303b8-144">hello shipping location name, obtained from hello previous step.</span></span>

-   <span data-ttu-id="303b8-145">Typ zadania (Importuj).</span><span class="sxs-lookup"><span data-stu-id="303b8-145">A job type (Import).</span></span>

-   <span data-ttu-id="303b8-146">adres zwrotny Hello gdzie hello dyski mają być wysyłane po zakończeniu zadania importu hello.</span><span class="sxs-lookup"><span data-stu-id="303b8-146">hello return address where hello drives should be sent after hello import job has completed.</span></span>

-   <span data-ttu-id="303b8-147">Lista Hello dysków w hello zadania.</span><span class="sxs-lookup"><span data-stu-id="303b8-147">hello list of drives in hello job.</span></span> <span data-ttu-id="303b8-148">Dla każdego dysku należy uwzględnić następujące informacje, który został uzyskany w kroku przygotowania dysku hello hello:</span><span class="sxs-lookup"><span data-stu-id="303b8-148">For each drive, you must include hello following information that was obtained during hello drive preparation step:</span></span>

    -   <span data-ttu-id="303b8-149">dysk Hello identyfikator</span><span class="sxs-lookup"><span data-stu-id="303b8-149">hello drive Id</span></span>

    -   <span data-ttu-id="303b8-150">Witaj klucza funkcji BitLocker</span><span class="sxs-lookup"><span data-stu-id="303b8-150">hello BitLocker key</span></span>

    -   <span data-ttu-id="303b8-151">Ścieżka względna pliku manifestu Hello na dysku twardym powitania</span><span class="sxs-lookup"><span data-stu-id="303b8-151">hello manifest file relative path on hello hard drive</span></span>

    -   <span data-ttu-id="303b8-152">Witaj Base16 algorytmem wyznaczania wartości skrótu MD5 pliku manifestu</span><span class="sxs-lookup"><span data-stu-id="303b8-152">hello Base16 encoded manifest file MD5 hash</span></span>

## <a name="shipping-your-drives"></a><span data-ttu-id="303b8-153">Wysyłanie dysków</span><span class="sxs-lookup"><span data-stu-id="303b8-153">Shipping your drives</span></span>
<span data-ttu-id="303b8-154">Należy wysłać swój adres toohello dysków, która pochodzi z poprzedniego kroku hello i musisz podać hello usługi Import/Eksport z hello śledzenia liczby pakietów hello.</span><span class="sxs-lookup"><span data-stu-id="303b8-154">You must ship your drives toohello address that you obtained from hello previous step, and you must provide hello Import/Export service with hello tracking number of hello package.</span></span>

> [!NOTE]
>  <span data-ttu-id="303b8-155">Muszą dostarczać dysków za pomocą usługi obsługiwane operatora, który dostarczy numer identyfikacyjny pakietu.</span><span class="sxs-lookup"><span data-stu-id="303b8-155">You must ship your drives via a supported carrier service, which will provide a tracking number for your package.</span></span>

## <a name="updating-hello-import-job-with-your-shipping-information"></a><span data-ttu-id="303b8-156">Aktualizowanie zadania importu hello z informacjami o wysyłki</span><span class="sxs-lookup"><span data-stu-id="303b8-156">Updating hello import job with your shipping information</span></span>
<span data-ttu-id="303b8-157">Po utworzeniu numer śledzenia wywołań hello [właściwości zadania aktualizacji](/api/storageimportexport/jobs#Jobs_Update) hello tooupdate operacji wysyłania Nazwa operatora, numer śledzenia hello hello zadania i numer konta operator hello zwracany wysyłki.</span><span class="sxs-lookup"><span data-stu-id="303b8-157">After you have your tracking number, call hello [Update Job Properties](/api/storageimportexport/jobs#Jobs_Update) operation tooupdate hello shipping carrier name, hello tracking number for hello job, and hello carrier account number for return shipping.</span></span> <span data-ttu-id="303b8-158">Opcjonalnie możesz określić liczbę hello dysków i hello Data również wysyłki.</span><span class="sxs-lookup"><span data-stu-id="303b8-158">You can optionally specify hello number of drives and hello shipping date as well.</span></span>

## <a name="next-steps"></a><span data-ttu-id="303b8-159">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="303b8-159">Next steps</span></span>

* [<span data-ttu-id="303b8-160">Przy użyciu interfejsu API REST usługi Import/Eksport hello</span><span class="sxs-lookup"><span data-stu-id="303b8-160">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
