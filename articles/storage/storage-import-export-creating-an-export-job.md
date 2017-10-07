---
title: aaaCreate eksportu zadania dla Import/Eksport Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak zadanie toocreate eksportu hello usługi Import/Eksport Microsoft Azure."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 613d480b-a8ef-4b28-8f54-54174d59b3f4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 4a10b42cc86dbf3bcea3a515bc065e2259228ef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-export-job-for-hello-azure-importexport-service"></a><span data-ttu-id="2f448-103">Tworzenie zadania eksportu dla hello usługi Import/Eksport Azure</span><span class="sxs-lookup"><span data-stu-id="2f448-103">Creating an export job for hello Azure Import/Export service</span></span>
<span data-ttu-id="2f448-104">Tworzenie zadania eksportu przy użyciu hello interfejsu API REST usługi Import/Eksport Microsoft Azure hello obejmuje hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="2f448-104">Creating an export job for hello Microsoft Azure Import/Export service using hello REST API involves hello following steps:</span></span>

-   <span data-ttu-id="2f448-105">Wybieranie hello obiektów blob tooexport.</span><span class="sxs-lookup"><span data-stu-id="2f448-105">Selecting hello blobs tooexport.</span></span>

-   <span data-ttu-id="2f448-106">Uzyskiwanie lokalizacji wysyłki.</span><span class="sxs-lookup"><span data-stu-id="2f448-106">Obtaining a shipping location.</span></span>

-   <span data-ttu-id="2f448-107">Tworzenie zadania eksportu hello.</span><span class="sxs-lookup"><span data-stu-id="2f448-107">Creating hello export job.</span></span>

-   <span data-ttu-id="2f448-108">Wysyłanie tooMicrosoft Twojego pustych dysków za pomocą usługi obsługiwane operatora.</span><span class="sxs-lookup"><span data-stu-id="2f448-108">Shipping your empty drives tooMicrosoft via a supported carrier service.</span></span>

-   <span data-ttu-id="2f448-109">Uaktualnianie informacji o pakiecie hello hello zadanie eksportu.</span><span class="sxs-lookup"><span data-stu-id="2f448-109">Updating hello export job with hello package information.</span></span>

-   <span data-ttu-id="2f448-110">Odbieranie hello dysków od firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2f448-110">Receiving hello drives back from Microsoft.</span></span>

 <span data-ttu-id="2f448-111">Zobacz [przy użyciu hello systemu Windows Azure Import/Eksport usługi tooTransfer danych tooBlob magazynu](storage-import-export-service.md) Omówienie usługi Import/Eksport hello i samouczek, który demonstruje sposób toouse hello [portalu Azure](https://portal.azure.com/) toocreate i zarządzanie importowanie i eksportowanie zadań.</span><span class="sxs-lookup"><span data-stu-id="2f448-111">See [Using hello Windows Azure Import/Export service tooTransfer Data tooBlob Storage](storage-import-export-service.md) for an overview of hello Import/Export service and a tutorial that demonstrates how toouse hello [Azure portal](https://portal.azure.com/) toocreate and manage import and export jobs.</span></span>

## <a name="selecting-blobs-tooexport"></a><span data-ttu-id="2f448-112">Wybieranie tooexport obiektów blob</span><span class="sxs-lookup"><span data-stu-id="2f448-112">Selecting blobs tooexport</span></span>
 <span data-ttu-id="2f448-113">toocreate zadanie eksportu, konieczne będzie tooprovide listy mają tooexport z konta magazynu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="2f448-113">toocreate an export job, you will need tooprovide a list of blobs that you want tooexport from your storage account.</span></span> <span data-ttu-id="2f448-114">Istnieje kilka sposobów tooselect obiektów blob toobe wyeksportowane:</span><span class="sxs-lookup"><span data-stu-id="2f448-114">There are a few ways tooselect blobs toobe exported:</span></span>

-   <span data-ttu-id="2f448-115">Tooselect ścieżki względnej blob można użyć pojedynczego obiektu blob i wszystkie jego migawek.</span><span class="sxs-lookup"><span data-stu-id="2f448-115">You can use a relative blob path tooselect a single blob and all of its snapshots.</span></span>

-   <span data-ttu-id="2f448-116">Tooselect ścieżki względnej blob można użyć pojedynczego obiektu blob, z wyłączeniem jego migawek.</span><span class="sxs-lookup"><span data-stu-id="2f448-116">You can use a relative blob path tooselect a single blob excluding its snapshots.</span></span>

-   <span data-ttu-id="2f448-117">Można użyć ścieżki względnej obiektów blob i tooselect czasu migawki jedna migawka.</span><span class="sxs-lookup"><span data-stu-id="2f448-117">You can use a relative blob path and a snapshot time tooselect a single snapshot.</span></span>

-   <span data-ttu-id="2f448-118">Można użyć tooselect prefiks obiektu blob wszystkie obiekty BLOB i migawki z hello podany prefiks.</span><span class="sxs-lookup"><span data-stu-id="2f448-118">You can use a blob prefix tooselect all blobs and snapshots with hello given prefix.</span></span>

-   <span data-ttu-id="2f448-119">Możesz wyeksportować wszystkie obiekty BLOB i migawek hello koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="2f448-119">You can export all blobs and snapshots in hello storage account.</span></span>

 <span data-ttu-id="2f448-120">Aby uzyskać więcej informacji na temat określania obiektów blob tooexport, zobacz hello [zawiesić zadanie](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operacji.</span><span class="sxs-lookup"><span data-stu-id="2f448-120">For more information about specifying blobs tooexport, see hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span>

## <a name="obtaining-your-shipping-location"></a><span data-ttu-id="2f448-121">Uzyskiwanie lokalizacji wysyłki</span><span class="sxs-lookup"><span data-stu-id="2f448-121">Obtaining your shipping location</span></span>
<span data-ttu-id="2f448-122">Przed utworzeniem zadania eksportu, należy tooobtain wysyłanie nazwy lokalizacji i adres przez wywołanie hello [pobrać lokalizacji](https://portal.azure.com) lub [lokalizacje listy](/rest/api/storageimportexport/listlocations) operacji.</span><span class="sxs-lookup"><span data-stu-id="2f448-122">Before creating an export job, you need tooobtain a shipping location name and address by calling hello [Get Location](https://portal.azure.com) or [List Locations](/rest/api/storageimportexport/listlocations) operation.</span></span> <span data-ttu-id="2f448-123">`List Locations`Zwraca listę lokalizacje i ich adres wysyłkowy.</span><span class="sxs-lookup"><span data-stu-id="2f448-123">`List Locations` will return a list of locations and their mailing addresses.</span></span> <span data-ttu-id="2f448-124">Można wybrać lokalizację z hello zwrócił listę i dostarczać adres toothat dysków twardych.</span><span class="sxs-lookup"><span data-stu-id="2f448-124">You can select a location from hello returned list and ship your hard drives toothat address.</span></span> <span data-ttu-id="2f448-125">Można również użyć hello `Get Location` hello tooobtain operacji wysyłania bezpośrednio adres dla określonej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="2f448-125">You can also use hello `Get Location` operation tooobtain hello shipping address for a specific location directly.</span></span>

<span data-ttu-id="2f448-126">Wykonaj kroki hello poniżej tooobtain hello wysyłanie lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="2f448-126">Follow hello steps below tooobtain hello shipping location:</span></span>

-   <span data-ttu-id="2f448-127">Określ nazwę hello hello Lokalizacja konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="2f448-127">Identify hello name of hello location of your storage account.</span></span> <span data-ttu-id="2f448-128">Tę wartość można znaleźć w hello **lokalizacji** na konto magazynu hello **pulpitu nawigacyjnego** w klasycznym hello portalu lub, którego dotyczy kwerenda dla za pomocą zarządzania usługami hello operacji interfejsu API [Get Właściwości konta magazynu](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span><span class="sxs-lookup"><span data-stu-id="2f448-128">This value can be found under hello **Location** field on hello storage account's **Dashboard** in hello classic portal or queried for by using hello service management API operation [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span></span>

-   <span data-ttu-id="2f448-129">Pobieranie lokalizacji hello, które są dostępne tooprocess tego konta magazynu przez wywołanie hello `Get Location` operacji.</span><span class="sxs-lookup"><span data-stu-id="2f448-129">Retrieve hello location that are available tooprocess this storage account by calling hello `Get Location` operation.</span></span>

-   <span data-ttu-id="2f448-130">Jeśli hello `AlternateLocations` właściwość lokalizacji hello zawiera samą powitalnych lokalizację, a następnie jest poprawny toouse tej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="2f448-130">If hello `AlternateLocations` property of hello location contains hello location itself, then it is okay toouse this location.</span></span> <span data-ttu-id="2f448-131">W przeciwnym razie wywołać hello `Get Location` ponownie operację, używając jednej z hello lokalizacji alternatywnej.</span><span class="sxs-lookup"><span data-stu-id="2f448-131">Otherwise, call hello `Get Location` operation again with one of hello alternate locations.</span></span> <span data-ttu-id="2f448-132">Hello oryginalnej lokalizacji może być tymczasowo zamknięte konserwacji.</span><span class="sxs-lookup"><span data-stu-id="2f448-132">hello original location might be temporarily closed for maintenance.</span></span>

## <a name="creating-hello-export-job"></a><span data-ttu-id="2f448-133">Tworzenie zadania eksportu hello</span><span class="sxs-lookup"><span data-stu-id="2f448-133">Creating hello export job</span></span>
 <span data-ttu-id="2f448-134">zadanie eksportu hello toocreate, wywołanie hello [zawiesić zadanie](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operacji.</span><span class="sxs-lookup"><span data-stu-id="2f448-134">toocreate hello export job, call hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="2f448-135">Konieczne będzie hello tooprovide następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="2f448-135">You will need tooprovide hello following information:</span></span>

-   <span data-ttu-id="2f448-136">Nazwa zadania hello.</span><span class="sxs-lookup"><span data-stu-id="2f448-136">A name for hello job.</span></span>

-   <span data-ttu-id="2f448-137">Nazwa konta magazynu Hello.</span><span class="sxs-lookup"><span data-stu-id="2f448-137">hello storage account name.</span></span>

-   <span data-ttu-id="2f448-138">Witaj wysyłania nazwy lokalizacji, uzyskanych w poprzednim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="2f448-138">hello shipping location name, obtained in hello previous step.</span></span>

-   <span data-ttu-id="2f448-139">Typ zadania (Eksportowanie).</span><span class="sxs-lookup"><span data-stu-id="2f448-139">A job type (Export).</span></span>

-   <span data-ttu-id="2f448-140">adres zwrotny Hello gdzie hello dyski mają być wysyłane po zakończeniu zadania eksportu hello.</span><span class="sxs-lookup"><span data-stu-id="2f448-140">hello return address where hello drives should be sent after hello export job has completed.</span></span>

-   <span data-ttu-id="2f448-141">wyeksportowane Hello toobe listę obiektów blob (lub prefiksy obiektów blob).</span><span class="sxs-lookup"><span data-stu-id="2f448-141">hello list of blobs (or blob prefixes) toobe exported.</span></span>

## <a name="shipping-your-drives"></a><span data-ttu-id="2f448-142">Wysyłanie dysków</span><span class="sxs-lookup"><span data-stu-id="2f448-142">Shipping your drives</span></span>
 <span data-ttu-id="2f448-143">Następnie użyj hello Azure narzędzie importu/eksportu toodetermine hello liczba dysków należy toosend oparte na obiekty BLOB hello wybrano toobe wyeksportowany i hello rozmiar dysku.</span><span class="sxs-lookup"><span data-stu-id="2f448-143">Next, use hello Azure Import/Export Tool toodetermine hello number of drives you need toosend, based on hello blobs you have selected toobe exported and hello drive size.</span></span> <span data-ttu-id="2f448-144">Zobacz hello [odwołania narzędzie importu/eksportu Azure](storage-import-export-tool-how-to-v1.md) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="2f448-144">See hello [Azure Import/Export Tool Reference](storage-import-export-tool-how-to-v1.md) for details.</span></span>

 <span data-ttu-id="2f448-145">Pakiet hello dysków w jednej pakietu i wysłać je toohello adres uzyskane w hello wcześniejszym kroku.</span><span class="sxs-lookup"><span data-stu-id="2f448-145">Package hello drives in a single package and ship them toohello address obtained in hello earlier step.</span></span> <span data-ttu-id="2f448-146">Należy zwrócić uwagę hello numer pakietu kolejny krok opisany hello śledzenia.</span><span class="sxs-lookup"><span data-stu-id="2f448-146">Note hello tracking number of your package for hello next step.</span></span>

> [!NOTE]
>  <span data-ttu-id="2f448-147">Muszą dostarczać dysków za pomocą usługi obsługiwane operatora, który dostarczy numer identyfikacyjny pakietu.</span><span class="sxs-lookup"><span data-stu-id="2f448-147">You must ship your drives via a supported carrier service, which will provide a tracking number for your package.</span></span>

## <a name="updating-hello-export-job-with-your-package-information"></a><span data-ttu-id="2f448-148">Trwa aktualizowanie zadania eksportu hello o informacje o pakiecie</span><span class="sxs-lookup"><span data-stu-id="2f448-148">Updating hello export job with your package information</span></span>
 <span data-ttu-id="2f448-149">Po utworzeniu numer śledzenia wywołań hello [właściwości zadania aktualizacji](/rest/api/storageimportexport/jobs#Jobs_Update) nazwy operatora hello tooupdated operacji i śledzenie liczby hello zadania.</span><span class="sxs-lookup"><span data-stu-id="2f448-149">After you have your tracking number, call hello [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation tooupdated hello carrier name and tracking number for hello job.</span></span> <span data-ttu-id="2f448-150">Opcjonalnie można określić numer hello dysków, adres zwrotny hello i hello także data wysyłki.</span><span class="sxs-lookup"><span data-stu-id="2f448-150">You can optionally specify hello number of drives, hello return address, and hello shipping date as well.</span></span>

## <a name="receiving-hello-package"></a><span data-ttu-id="2f448-151">Odbieranie hello pakietu</span><span class="sxs-lookup"><span data-stu-id="2f448-151">Receiving hello package</span></span>
 <span data-ttu-id="2f448-152">Po przetworzeniu zadanie eksportu, dyski zostaną zwrócone tooyou z zaszyfrowanych danych.</span><span class="sxs-lookup"><span data-stu-id="2f448-152">After your export job has been processed, your drives will be returned tooyou with your encrypted data.</span></span> <span data-ttu-id="2f448-153">Możesz pobrać hello klucza funkcji BitLocker dla poszczególnych dysków hello przez wywołanie hello [pobrania zadania](/rest/api/storageimportexport/jobs#Jobs_Get) operacji.</span><span class="sxs-lookup"><span data-stu-id="2f448-153">You can retrieve hello BitLocker key for each of hello drives by calling hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="2f448-154">Następnie można odblokować dysku hello przy użyciu klucza hello.</span><span class="sxs-lookup"><span data-stu-id="2f448-154">You can then unlock hello drive using hello key.</span></span> <span data-ttu-id="2f448-155">Plik manifestu dysku Hello na każdym dysku, zawiera listę hello plików hello dysku, a także hello oryginalny adres obiektu blob dla każdego pliku.</span><span class="sxs-lookup"><span data-stu-id="2f448-155">hello drive manifest file on each drive contains hello list of files on hello drive, as well as hello original blob address for each file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f448-156">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2f448-156">Next steps</span></span>

* [<span data-ttu-id="2f448-157">Przy użyciu interfejsu API REST usługi Import/Eksport hello</span><span class="sxs-lookup"><span data-stu-id="2f448-157">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
