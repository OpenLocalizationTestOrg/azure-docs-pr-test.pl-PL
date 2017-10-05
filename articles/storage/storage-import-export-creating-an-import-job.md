---
title: "Utwórz zadania importowania platformy Azure importu/eksportu | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć importu dla usługi Import/Eksport Microsoft Azure."
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
ms.openlocfilehash: d373d2a0e601f2796719fc5efb8761f276ab24d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="creating-an-import-job-for-the-azure-importexport-service"></a><span data-ttu-id="fda0e-103">Tworzenie zadania importu dla usługi Import/Eksport Azure</span><span class="sxs-lookup"><span data-stu-id="fda0e-103">Creating an import job for the Azure Import/Export service</span></span>

<span data-ttu-id="fda0e-104">Tworzenie zadania importu za pomocą interfejsu API REST usługi Import/Eksport Microsoft Azure obejmuje następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="fda0e-104">Creating an import job for the Microsoft Azure Import/Export service using the REST API involves the following steps:</span></span>

-   <span data-ttu-id="fda0e-105">Przygotowywanie dysków za pomocą narzędzia importu/eksportu Azure.</span><span class="sxs-lookup"><span data-stu-id="fda0e-105">Preparing drives with the Azure Import/Export Tool.</span></span>

-   <span data-ttu-id="fda0e-106">Uzyskiwanie lokalizacji, do której należy wysłać dysku.</span><span class="sxs-lookup"><span data-stu-id="fda0e-106">Obtaining the location to which to ship the drive.</span></span>

-   <span data-ttu-id="fda0e-107">Tworzenie zadania importu.</span><span class="sxs-lookup"><span data-stu-id="fda0e-107">Creating the import job.</span></span>

-   <span data-ttu-id="fda0e-108">Wysyłania dysków do firmy Microsoft za pośrednictwem usługi obsługiwane operatora.</span><span class="sxs-lookup"><span data-stu-id="fda0e-108">Shipping the drives to Microsoft via a supported carrier service.</span></span>

-   <span data-ttu-id="fda0e-109">Uaktualnianie zadania importu szczegóły dotyczące wysyłki.</span><span class="sxs-lookup"><span data-stu-id="fda0e-109">Updating the import job with the shipping details.</span></span>

 <span data-ttu-id="fda0e-110">Zobacz [za pomocą usługi Import/Eksport Microsoft Azure przesyłanie danych do magazynu obiektów Blob](storage-import-export-service.md) Omówienie usługi Import/Eksport i samouczek, który demonstruje sposób użycia [portalu Azure](https://portal.azure.com/) do tworzenia i zarządzania importowanie i eksportowanie zadań.</span><span class="sxs-lookup"><span data-stu-id="fda0e-110">See [Using the Microsoft Azure Import/Export service to Transfer Data to Blob Storage](storage-import-export-service.md) for an overview of the Import/Export service and a tutorial that demonstrates how to use the [Azure  portal](https://portal.azure.com/) to create and manage import and export jobs.</span></span>

## <a name="preparing-drives-with-the-azure-importexport-tool"></a><span data-ttu-id="fda0e-111">Przygotowywanie dysków za pomocą narzędzia importu/eksportu Azure</span><span class="sxs-lookup"><span data-stu-id="fda0e-111">Preparing drives with the Azure Import/Export Tool</span></span>

<span data-ttu-id="fda0e-112">Kroki, aby przygotować dyski dla zadania importu, są takie same, czy utworzyć jobvia portalu lub za pośrednictwem interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="fda0e-112">The steps to prepare drives for an import job are the same whether you create the jobvia the portal or via the REST API.</span></span>

<span data-ttu-id="fda0e-113">Poniżej znajduje się krótki przegląd Przygotowanie stacji.</span><span class="sxs-lookup"><span data-stu-id="fda0e-113">Below is a brief overview of drive preparation.</span></span> <span data-ttu-id="fda0e-114">Zapoznaj się [odwołania ExportTool importu Azure](storage-import-export-tool-how-to-v1.md) Aby uzyskać pełne instrukcje.</span><span class="sxs-lookup"><span data-stu-id="fda0e-114">Refer to the [Azure Import-ExportTool Reference](storage-import-export-tool-how-to-v1.md) for complete instructions.</span></span> <span data-ttu-id="fda0e-115">Narzędzie importu/eksportu Azure można pobrać [tutaj](http://go.microsoft.com/fwlink/?LinkID=301900).</span><span class="sxs-lookup"><span data-stu-id="fda0e-115">You can download the Azure Import/Export Tool [here](http://go.microsoft.com/fwlink/?LinkID=301900).</span></span>

<span data-ttu-id="fda0e-116">Przygotowywanie dysku obejmuje:</span><span class="sxs-lookup"><span data-stu-id="fda0e-116">Preparing your drive involves:</span></span>

-   <span data-ttu-id="fda0e-117">Identyfikowanie dane do zaimportowania.</span><span class="sxs-lookup"><span data-stu-id="fda0e-117">Identifying the data to be imported.</span></span>

-   <span data-ttu-id="fda0e-118">Identyfikowanie przeznaczenia obiekty BLOB w magazynie Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="fda0e-118">Identifying the destination blobs in Windows Azure Storage.</span></span>

-   <span data-ttu-id="fda0e-119">Za pomocą narzędzia importu/eksportu Azure, aby skopiować dane do jednego lub więcej dysków twardych.</span><span class="sxs-lookup"><span data-stu-id="fda0e-119">Using the Azure Import/Export Tool to copy your data to one or more hard drives.</span></span>

 <span data-ttu-id="fda0e-120">Narzędzie importu/eksportu Azure również spowoduje wygenerowanie pliku manifestu dla poszczególnych dysków, jak jest przygotowana.</span><span class="sxs-lookup"><span data-stu-id="fda0e-120">The Azure Import/Export Tool will also generate a manifest file for each of the drives as it is prepared.</span></span> <span data-ttu-id="fda0e-121">Plik manifestu zawiera:</span><span class="sxs-lookup"><span data-stu-id="fda0e-121">A manifest file contains:</span></span>

-   <span data-ttu-id="fda0e-122">Wyliczenie wszystkich plików przeznaczonych do przekazywania i mapowania z tych plików do obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="fda0e-122">An enumeration of all the files intended for upload and the mappings from these files to blobs.</span></span>

-   <span data-ttu-id="fda0e-123">Sum kontrolnych segmentów każdego pliku.</span><span class="sxs-lookup"><span data-stu-id="fda0e-123">Checksums of the segments of each file.</span></span>

-   <span data-ttu-id="fda0e-124">Informacje o właściwości do skojarzenia z każdy obiekt blob i metadanych.</span><span class="sxs-lookup"><span data-stu-id="fda0e-124">Information about the metadata and properties to associate with each blob.</span></span>

-   <span data-ttu-id="fda0e-125">Lista działanie w przypadku obiektów blob, który jest przekazywanych ma taką samą nazwę jak istniejącym obiektem blob w kontenerze.</span><span class="sxs-lookup"><span data-stu-id="fda0e-125">A listing of the action to take if a blob that is being uploaded has the same name as an existing blob in the container.</span></span> <span data-ttu-id="fda0e-126">Dostępne są opcje:) zastępowania obiektu blob z plikiem, (b) aktualizowanie istniejących obiektów blob i Pomiń przekazywania pliku, c) dodać sufiks nazwy nie powoduje konfliktu z innymi plikami.</span><span class="sxs-lookup"><span data-stu-id="fda0e-126">Possible options are: a) overwrite the blob with the file, b) keep the existing blob and skip uploading the file, c) append a suffix to the name so that it does not conflict with other files.</span></span>

## <a name="obtaining-your-shipping-location"></a><span data-ttu-id="fda0e-127">Uzyskiwanie lokalizacji wysyłki</span><span class="sxs-lookup"><span data-stu-id="fda0e-127">Obtaining your shipping location</span></span>

<span data-ttu-id="fda0e-128">Przed utworzeniem zadania importu, należy uzyskać wysyłanie nazwy lokalizacji i adres wywołując [lokalizacje listy](/rest/api/storageimportexport/listlocations) operacji.</span><span class="sxs-lookup"><span data-stu-id="fda0e-128">Before creating an import job, you need to obtain a shipping location name and address by calling the [List Locations](/rest/api/storageimportexport/listlocations) operation.</span></span> <span data-ttu-id="fda0e-129">`List Locations`Zwraca listę lokalizacje i ich adres wysyłkowy.</span><span class="sxs-lookup"><span data-stu-id="fda0e-129">`List Locations` will return a list of locations and their mailing addresses.</span></span> <span data-ttu-id="fda0e-130">Możesz wybrać lokalizację z listy zwróconych i wysłać dyskach twardych na ten adres.</span><span class="sxs-lookup"><span data-stu-id="fda0e-130">You can select a location from the returned list and ship your hard drives to that address.</span></span> <span data-ttu-id="fda0e-131">Można również użyć `Get Location` operacji bezpośrednio uzyskać adres wysyłkowy dla określonej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="fda0e-131">You can also use the `Get Location` operation to obtain the shipping address for a specific location directly.</span></span>

 <span data-ttu-id="fda0e-132">Wykonaj poniższe kroki, aby uzyskać lokalizacji wysyłki:</span><span class="sxs-lookup"><span data-stu-id="fda0e-132">Follow the steps below to obtain the shipping location:</span></span>

-   <span data-ttu-id="fda0e-133">Określ nazwę lokalizacji konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="fda0e-133">Identify the name of the location of your storage account.</span></span> <span data-ttu-id="fda0e-134">Tę wartość można znaleźć w **lokalizacji** na konto magazynu **pulpitu nawigacyjnego** na platformie Azure, w portalu lub, którego dotyczy kwerenda dla za pomocą operacji interfejsu API zarządzania usługami [Get właściwości konta magazynu](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span><span class="sxs-lookup"><span data-stu-id="fda0e-134">This value can be found under the **Location** field on the storage account's **Dashboard** in the Azure portal or queried for by using the service management API operation [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span></span>

-   <span data-ttu-id="fda0e-135">Pobieranie lokalizacji, która jest dostępnych do przetworzenia tego konta magazynu przez wywołanie metody `Get Location` operacji.</span><span class="sxs-lookup"><span data-stu-id="fda0e-135">Retrieve the location that is available to process this storage account by calling the `Get Location` operation.</span></span>

-   <span data-ttu-id="fda0e-136">Jeśli `AlternateLocations` właściwość lokalizacji zawiera samą lokalizację, a następnie można użyć tej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="fda0e-136">If the `AlternateLocations` property of the location contains the location itself, then it is okay to use this location.</span></span> <span data-ttu-id="fda0e-137">W przeciwnym razie wywołać `Get Location` ponownie operację, używając jednej z lokalizacji alternatywnej.</span><span class="sxs-lookup"><span data-stu-id="fda0e-137">Otherwise, call the `Get Location` operation again with one of the alternate locations.</span></span> <span data-ttu-id="fda0e-138">Oryginalnej lokalizacji może być tymczasowo zamknięte konserwacji.</span><span class="sxs-lookup"><span data-stu-id="fda0e-138">The original location might be temporarily closed for maintenance.</span></span>

## <a name="creating-the-import-job"></a><span data-ttu-id="fda0e-139">Tworzenie zadania importu</span><span class="sxs-lookup"><span data-stu-id="fda0e-139">Creating the import job</span></span>
<span data-ttu-id="fda0e-140">Aby utworzyć zadanie importu, należy wywołać [zawiesić zadanie](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operacji.</span><span class="sxs-lookup"><span data-stu-id="fda0e-140">To create the import job, call the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="fda0e-141">Należy podać następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="fda0e-141">You will need to provide the following information:</span></span>

-   <span data-ttu-id="fda0e-142">Nazwa zadania.</span><span class="sxs-lookup"><span data-stu-id="fda0e-142">A name for the job.</span></span>

-   <span data-ttu-id="fda0e-143">Nazwa konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="fda0e-143">The storage account name.</span></span>

-   <span data-ttu-id="fda0e-144">Wysyłanie nazwy lokalizacji, uzyskanych w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="fda0e-144">The shipping location name, obtained from the previous step.</span></span>

-   <span data-ttu-id="fda0e-145">Typ zadania (Importuj).</span><span class="sxs-lookup"><span data-stu-id="fda0e-145">A job type (Import).</span></span>

-   <span data-ttu-id="fda0e-146">Adres zwrotny, gdzie dyski mają być wysyłane po zakończeniu zadania importu.</span><span class="sxs-lookup"><span data-stu-id="fda0e-146">The return address where the drives should be sent after the import job has completed.</span></span>

-   <span data-ttu-id="fda0e-147">Lista dysków w zadaniu.</span><span class="sxs-lookup"><span data-stu-id="fda0e-147">The list of drives in the job.</span></span> <span data-ttu-id="fda0e-148">Dla każdego dysku musi zawierać następujące informacje, które jest prefiksem uzyskanym w kroku przygotowania dysku:</span><span class="sxs-lookup"><span data-stu-id="fda0e-148">For each drive, you must include the following information that was obtained during the drive preparation step:</span></span>

    -   <span data-ttu-id="fda0e-149">Identyfikator dysku</span><span class="sxs-lookup"><span data-stu-id="fda0e-149">The drive Id</span></span>

    -   <span data-ttu-id="fda0e-150">Klucza funkcji BitLocker</span><span class="sxs-lookup"><span data-stu-id="fda0e-150">The BitLocker key</span></span>

    -   <span data-ttu-id="fda0e-151">Względna ścieżka pliku manifestu na dysku twardym</span><span class="sxs-lookup"><span data-stu-id="fda0e-151">The manifest file relative path on the hard drive</span></span>

    -   <span data-ttu-id="fda0e-152">Base16 algorytmem wyznaczania wartości skrótu MD5 w pliku manifestu</span><span class="sxs-lookup"><span data-stu-id="fda0e-152">The Base16 encoded manifest file MD5 hash</span></span>

## <a name="shipping-your-drives"></a><span data-ttu-id="fda0e-153">Wysyłanie dysków</span><span class="sxs-lookup"><span data-stu-id="fda0e-153">Shipping your drives</span></span>
<span data-ttu-id="fda0e-154">Muszą dostarczać dysków na adres, który został uzyskany z poprzedniego kroku, a usługi Import/Eksport należy podać numer śledzenia pakietu.</span><span class="sxs-lookup"><span data-stu-id="fda0e-154">You must ship your drives to the address that you obtained from the previous step, and you must provide the Import/Export service with the tracking number of the package.</span></span>

> [!NOTE]
>  <span data-ttu-id="fda0e-155">Muszą dostarczać dysków za pomocą usługi obsługiwane operatora, który dostarczy numer identyfikacyjny pakietu.</span><span class="sxs-lookup"><span data-stu-id="fda0e-155">You must ship your drives via a supported carrier service, which will provide a tracking number for your package.</span></span>

## <a name="updating-the-import-job-with-your-shipping-information"></a><span data-ttu-id="fda0e-156">Aktualizowanie zadania importu z informacjami o wysyłki</span><span class="sxs-lookup"><span data-stu-id="fda0e-156">Updating the import job with your shipping information</span></span>
<span data-ttu-id="fda0e-157">Po utworzeniu numer śledzenia wywołań [właściwości zadania aktualizacji](/api/storageimportexport/jobs#Jobs_Update) Operacja aktualizowania wysyłanie Nazwa operatora, numer zadania i operatora numer konta do wysyłki zwracany.</span><span class="sxs-lookup"><span data-stu-id="fda0e-157">After you have your tracking number, call the [Update Job Properties](/api/storageimportexport/jobs#Jobs_Update) operation to update the shipping carrier name, the tracking number for the job, and the carrier account number for return shipping.</span></span> <span data-ttu-id="fda0e-158">Opcjonalnie można określić liczbę dysków, a także data wysyłki.</span><span class="sxs-lookup"><span data-stu-id="fda0e-158">You can optionally specify the number of drives and the shipping date as well.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fda0e-159">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fda0e-159">Next steps</span></span>

* [<span data-ttu-id="fda0e-160">Przy użyciu interfejsu API REST usługi Import/Eksport</span><span class="sxs-lookup"><span data-stu-id="fda0e-160">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
