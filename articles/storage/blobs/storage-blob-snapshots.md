---
title: "Tworzenie migawki tylko do odczytu obiektu blob w usłudze Azure Storage | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć migawki obiektu blob, aby utworzyć kopię zapasową danych obiektów blob w danym momencie w czasie. Dowiedz się, jak są rozliczane migawki i sposób ich użycia, aby zminimalizować koszty pojemności."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 3710705d-e127-4b01-8d0f-29853fb06d0d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/11/2017
ms.author: marsma
ms.openlocfilehash: b1d87cd66457b08bba594bfc7de1e9e4e2dff1e6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-blob-snapshot"></a><span data-ttu-id="c752e-104">Tworzenie migawki obiektu blob</span><span class="sxs-lookup"><span data-stu-id="c752e-104">Create a blob snapshot</span></span>

<span data-ttu-id="c752e-105">Migawka jest tylko do odczytu wersji obiektu blob, która jest wykonywana w punkcie w czasie.</span><span class="sxs-lookup"><span data-stu-id="c752e-105">A snapshot is a read-only version of a blob that's taken at a point in time.</span></span> <span data-ttu-id="c752e-106">Migawki są przydatne w przypadku tworzenia kopii zapasowej obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="c752e-106">Snapshots are useful for backing up blobs.</span></span> <span data-ttu-id="c752e-107">Po utworzeniu migawki, odczytu, skopiuj lub usuń go, ale nie można go modyfikować.</span><span class="sxs-lookup"><span data-stu-id="c752e-107">After you create a snapshot, you can read, copy, or delete it, but you cannot modify it.</span></span>

<span data-ttu-id="c752e-108">Migawki obiektu blob jest taka sama jak podstawowa obiektu blob z tą różnicą, że identyfikator URI obiektu blob ma **DateTime** wartość do obiektu blob identyfikatora URI wskazująca czas, w którym migawki.</span><span class="sxs-lookup"><span data-stu-id="c752e-108">A snapshot of a blob is identical to its base blob, except that the blob URI has a **DateTime** value appended to the blob URI to indicate the time at which the snapshot was taken.</span></span> <span data-ttu-id="c752e-109">Na przykład jeśli identyfikator URI obiektu blob strony jest `http://storagesample.core.blob.windows.net/mydrives/myvhd`, identyfikator URI jest podobny do migawki `http://storagesample.core.blob.windows.net/mydrives/myvhd?snapshot=2011-03-09T01:42:34.9360000Z`.</span><span class="sxs-lookup"><span data-stu-id="c752e-109">For example, if a page blob URI is `http://storagesample.core.blob.windows.net/mydrives/myvhd`, the snapshot URI is similar to `http://storagesample.core.blob.windows.net/mydrives/myvhd?snapshot=2011-03-09T01:42:34.9360000Z`.</span></span>

> [!NOTE]
> <span data-ttu-id="c752e-110">Wszystkie migawki mają podstawowego obiektu blob identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="c752e-110">All snapshots share the base blob's URI.</span></span> <span data-ttu-id="c752e-111">Tylko różnice między podstawową obiektów blob i migawki jest dołączany **DateTime** wartość.</span><span class="sxs-lookup"><span data-stu-id="c752e-111">The only distinction between the base blob and the snapshot is the appended **DateTime** value.</span></span>
>

<span data-ttu-id="c752e-112">Obiekt blob może mieć dowolną liczbę migawek.</span><span class="sxs-lookup"><span data-stu-id="c752e-112">A blob can have any number of snapshots.</span></span> <span data-ttu-id="c752e-113">Migawki zachować, dopóki nie zostaną jawnie usunięte.</span><span class="sxs-lookup"><span data-stu-id="c752e-113">Snapshots persist until they are explicitly deleted.</span></span> <span data-ttu-id="c752e-114">Migawka nie outlive jego podstawowego obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="c752e-114">A snapshot cannot outlive its base blob.</span></span> <span data-ttu-id="c752e-115">Można wyliczyć migawki skojarzone z podstawowego obiektu blob do śledzenia sieci bieżącej migawki.</span><span class="sxs-lookup"><span data-stu-id="c752e-115">You can enumerate the snapshots associated with the base blob to track your current snapshots.</span></span>

<span data-ttu-id="c752e-116">Po utworzeniu migawki obiektu blob właściwości systemu obiektu blob są kopiowane do migawki o takich samych wartości.</span><span class="sxs-lookup"><span data-stu-id="c752e-116">When you create a snapshot of a blob, the blob's system properties are copied to the snapshot with the same values.</span></span> <span data-ttu-id="c752e-117">Metadane podstawowego obiektu blob jest również kopiowane do migawki, chyba że zostanie oddzielne metadanych dla migawki podczas jego tworzenia.</span><span class="sxs-lookup"><span data-stu-id="c752e-117">The base blob's metadata is also copied to the snapshot, unless you specify separate metadata for the snapshot when you create it.</span></span>

<span data-ttu-id="c752e-118">Wszystkie dzierżawy skojarzonego z podstawowego obiektu blob nie wpływają na migawki.</span><span class="sxs-lookup"><span data-stu-id="c752e-118">Any leases associated with the base blob do not affect the snapshot.</span></span> <span data-ttu-id="c752e-119">Nie można pobrać dzierżawy na migawki.</span><span class="sxs-lookup"><span data-stu-id="c752e-119">You cannot acquire a lease on a snapshot.</span></span>

<span data-ttu-id="c752e-120">Plik VHD jest używany do przechowywania informacji o bieżącym i stan dysku maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c752e-120">A VHD file is used to store the current information and status for a VM disk.</span></span> <span data-ttu-id="c752e-121">Można odłączyć dysku z poziomu maszyny Wirtualnej lub zamykania maszyny Wirtualnej, a następnie Utwórz migawkę jego plik VHD.</span><span class="sxs-lookup"><span data-stu-id="c752e-121">You can detach a disk from within the VM or shut down the VM, and then take a snapshot of its VHD file.</span></span> <span data-ttu-id="c752e-122">Ten plik migawki można użyć później można pobrać pliku wirtualnego dysku twardego w danym momencie i Utwórz ponownie maszynę Wirtualną.</span><span class="sxs-lookup"><span data-stu-id="c752e-122">You can use that snapshot file later to retrieve the VHD file at that point in time and recreate the VM.</span></span>

<span data-ttu-id="c752e-123">Jeśli szyfrowanie usługi Magazyn (SSE) jest włączony dla konta magazynu, w której znajduje się obiekt blob, wszystkie migawki wziąć pod uwagę tego obiektu blob będą szyfrowane w stanie spoczynku.</span><span class="sxs-lookup"><span data-stu-id="c752e-123">If Storage Service Encryption (SSE) is enabled for the storage account in which the blob resides, then any snapshots taken of that blob will be encrypted at rest.</span></span>

## <a name="create-a-snapshot"></a><span data-ttu-id="c752e-124">Utwórz migawkę</span><span class="sxs-lookup"><span data-stu-id="c752e-124">Create a snapshot</span></span>
<span data-ttu-id="c752e-125">W poniższym przykładzie przedstawiono sposób tworzenia migawki za pomocą [biblioteki klienta magazynu Azure dla platformy .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span><span class="sxs-lookup"><span data-stu-id="c752e-125">The following code example shows how to create a snapshot by using the [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span></span> <span data-ttu-id="c752e-126">W tym przykładzie określa dodatkowe metadane dla migawki podczas jego tworzenia.</span><span class="sxs-lookup"><span data-stu-id="c752e-126">This example specifies additional metadata for the snapshot when it is created.</span></span>

```csharp
private static async Task CreateBlockBlobSnapshot(CloudBlobContainer container)
{
    // Create a new block blob in the container.
    CloudBlockBlob baseBlob = container.GetBlockBlobReference("sample-base-blob.txt");

    // Add blob metadata.
    baseBlob.Metadata.Add("ApproxBlobCreatedDate", DateTime.UtcNow.ToString());

    try
    {
        // Upload the blob to create it, with its metadata.
        await baseBlob.UploadTextAsync(string.Format("Base blob: {0}", baseBlob.Uri.ToString()));

        // Sleep 5 seconds.
        System.Threading.Thread.Sleep(5000);

        // Create a snapshot of the base blob.
        // Specify metadata at the time that the snapshot is created to specify unique metadata for the snapshot.
        // If no metadata is specified when the snapshot is created, the base blob's metadata is copied to the snapshot.
        Dictionary<string, string> metadata = new Dictionary<string, string>();
        metadata.Add("ApproxSnapshotCreatedDate", DateTime.UtcNow.ToString());
        await baseBlob.CreateSnapshotAsync(metadata, null, null, null);
    }
    catch (StorageException e)
    {
        Console.WriteLine(e.Message);
        Console.ReadLine();
        throw;
    }
}
```

## <a name="copy-snapshots"></a><span data-ttu-id="c752e-127">Kopiowanie migawek</span><span class="sxs-lookup"><span data-stu-id="c752e-127">Copy snapshots</span></span>
<span data-ttu-id="c752e-128">Operacje kopiowania obejmujące obiekty BLOB i migawek wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c752e-128">Copy operations involving blobs and snapshots follow these rules:</span></span>

* <span data-ttu-id="c752e-129">Możesz skopiować migawki za pośrednictwem jego podstawowego obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="c752e-129">You can copy a snapshot over its base blob.</span></span> <span data-ttu-id="c752e-130">Promowanie migawki do położenia podstawowego obiektu blob, można przywrócić wcześniejszą wersję obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="c752e-130">By promoting a snapshot to the position of the base blob, you can restore an earlier version of a blob.</span></span> <span data-ttu-id="c752e-131">Pozostaje migawki, ale bazie obiektu blob jest zastępowany kopię zapisu migawki.</span><span class="sxs-lookup"><span data-stu-id="c752e-131">The snapshot remains, but the base blob is overwritten with a writable copy of the snapshot.</span></span>
* <span data-ttu-id="c752e-132">Migawki można skopiować do docelowego obiektu blob o innej nazwie.</span><span class="sxs-lookup"><span data-stu-id="c752e-132">You can copy a snapshot to a destination blob with a different name.</span></span> <span data-ttu-id="c752e-133">Wynikowa docelowego obiektu blob jest zapisywalny obiektów blob i nie migawki.</span><span class="sxs-lookup"><span data-stu-id="c752e-133">The resulting destination blob is a writable blob and not a snapshot.</span></span>
* <span data-ttu-id="c752e-134">Po skopiowaniu źródłowego obiektu blob wszystkie migawki źródłowego obiektu blob nie są kopiowane do lokalizacji docelowej.</span><span class="sxs-lookup"><span data-stu-id="c752e-134">When a source blob is copied, any snapshots of the source blob are not copied to the destination.</span></span> <span data-ttu-id="c752e-135">Gdy docelowego obiektu blob jest zastępowany kopii, wszystkie migawki skojarzone z oryginalnego docelowego obiektu blob pozostaną nienaruszone.</span><span class="sxs-lookup"><span data-stu-id="c752e-135">When a destination blob is overwritten with a copy, any snapshots associated with the original destination blob remain intact.</span></span>
* <span data-ttu-id="c752e-136">Po utworzeniu migawki blokowych obiektów blob zablokowanych zatwierdzone obiektu blob jest również kopiowany do migawki.</span><span class="sxs-lookup"><span data-stu-id="c752e-136">When you create a snapshot of a block blob, the blob's committed block list is also copied to the snapshot.</span></span> <span data-ttu-id="c752e-137">Niezatwierdzone bloków nie są kopiowane.</span><span class="sxs-lookup"><span data-stu-id="c752e-137">Any uncommitted blocks are not copied.</span></span>

## <a name="specify-an-access-condition"></a><span data-ttu-id="c752e-138">Określ warunek dostępu</span><span class="sxs-lookup"><span data-stu-id="c752e-138">Specify an access condition</span></span>
<span data-ttu-id="c752e-139">Podczas wywoływania [CreateSnapshotAsync][dotnet_CreateSnapshotAsync], można określić warunki dostępu, aby migawki jest tworzony tylko wtedy, gdy warunek jest spełniony.</span><span class="sxs-lookup"><span data-stu-id="c752e-139">When you call [CreateSnapshotAsync][dotnet_CreateSnapshotAsync], you can specify an access condition so that the snapshot is created only if a condition is met.</span></span> <span data-ttu-id="c752e-140">Aby określić warunki dostępu, użyj [AccessCondition] [ dotnet_AccessCondition] parametru.</span><span class="sxs-lookup"><span data-stu-id="c752e-140">To specify an access condition, use the [AccessCondition][dotnet_AccessCondition] parameter.</span></span> <span data-ttu-id="c752e-141">Jeśli nie zostanie spełniony określony warunek, migawki nie zostanie utworzony, a usługa Blob zwraca kod stanu [HTTPStatusCode][dotnet_HTTPStatusCode]. PreconditionFailed.</span><span class="sxs-lookup"><span data-stu-id="c752e-141">If the specified condition is not met, the snapshot is not created, and the Blob service returns status code [HTTPStatusCode][dotnet_HTTPStatusCode].PreconditionFailed.</span></span>

## <a name="delete-snapshots"></a><span data-ttu-id="c752e-142">Usuń migawki</span><span class="sxs-lookup"><span data-stu-id="c752e-142">Delete snapshots</span></span>
<span data-ttu-id="c752e-143">Nie można usunąć obiektu blob z migawki, chyba że migawki, również zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="c752e-143">You can't delete a blob with snapshots unless the snapshots are also deleted.</span></span> <span data-ttu-id="c752e-144">Możesz usunąć migawkę indywidualnie lub określić, że wszystkie migawki usunięte po usunięciu źródłowego obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="c752e-144">You can delete a snapshot individually, or specify that all snapshots be deleted when the source blob is deleted.</span></span> <span data-ttu-id="c752e-145">Jeśli próbujesz usunąć obiektu blob, które nadal istnieją migawki, powoduje błąd.</span><span class="sxs-lookup"><span data-stu-id="c752e-145">If you attempt to delete a blob that still has snapshots, an error results.</span></span>

<span data-ttu-id="c752e-146">W poniższym przykładzie pokazano, jak można usunąć obiektu blob i jego migawek w środowisku .NET, gdzie `blockBlob` jest obiektem typu [CloudBlockBlob][dotnet_CloudBlockBlob]:</span><span class="sxs-lookup"><span data-stu-id="c752e-146">The following code example shows how to delete a blob and its snapshots in .NET, where `blockBlob` is an object of type [CloudBlockBlob][dotnet_CloudBlockBlob]:</span></span>

```csharp
await blockBlob.DeleteIfExistsAsync(DeleteSnapshotsOption.IncludeSnapshots, null, null, null);
```

## <a name="snapshots-with-azure-premium-storage"></a><span data-ttu-id="c752e-147">Migawki z magazynem Azure — warstwa Premium</span><span class="sxs-lookup"><span data-stu-id="c752e-147">Snapshots with Azure Premium Storage</span></span>
<span data-ttu-id="c752e-148">Korzystając z migawki z magazyn w warstwie Premium, obowiązują następujące reguły:</span><span class="sxs-lookup"><span data-stu-id="c752e-148">When using snapshots with Premium Storage, the following rules apply:</span></span>

* <span data-ttu-id="c752e-149">Maksymalna liczba migawek na stronicowych obiektów blob na koncie magazynu premium to 100.</span><span class="sxs-lookup"><span data-stu-id="c752e-149">The maximum number of snapshots per page blob in a premium storage account is 100.</span></span> <span data-ttu-id="c752e-150">Po przekroczeniu tego limitu operacji migawki obiektu Blob zwraca kod błędu 409 (`SnapshotCountExceeded`).</span><span class="sxs-lookup"><span data-stu-id="c752e-150">If that limit is exceeded, the Snapshot Blob operation returns error code 409 (`SnapshotCountExceeded`).</span></span>
* <span data-ttu-id="c752e-151">Można utworzyć migawkę stronicowych obiektów blob na koncie magazynu premium co 10 minut.</span><span class="sxs-lookup"><span data-stu-id="c752e-151">You can take a snapshot of a page blob in a premium storage account once every 10 minutes.</span></span> <span data-ttu-id="c752e-152">Po przekroczeniu tego kursu operacji migawki obiektu Blob zwraca kod błędu 409 (`SnapshotOperationRateExceeded`).</span><span class="sxs-lookup"><span data-stu-id="c752e-152">If that rate is exceeded, the Snapshot Blob operation returns error code 409 (`SnapshotOperationRateExceeded`).</span></span>
* <span data-ttu-id="c752e-153">Za pomocą operacji kopiowania obiektu Blob można skopiować migawki do innego obiektu blob strony w konto, odczytać migawki.</span><span class="sxs-lookup"><span data-stu-id="c752e-153">To read a snapshot, you can use the Copy Blob operation to copy a snapshot to another page blob in the account.</span></span> <span data-ttu-id="c752e-154">Docelowego obiektu blob dla operacji kopiowania nie może mieć żadnych istniejących migawki.</span><span class="sxs-lookup"><span data-stu-id="c752e-154">The destination blob for the copy operation must not have any existing snapshots.</span></span> <span data-ttu-id="c752e-155">Jeśli docelowego obiektu blob migawki, a następnie zwraca kod błędu 409, operacja kopiowania obiektów Blob (`SnapshotsPresent`).</span><span class="sxs-lookup"><span data-stu-id="c752e-155">If the destination blob does have snapshots, then the Copy Blob operation returns error code 409 (`SnapshotsPresent`).</span></span>

## <a name="return-the-absolute-uri-to-a-snapshot"></a><span data-ttu-id="c752e-156">Zwraca bezwzględny identyfikator URI do migawki</span><span class="sxs-lookup"><span data-stu-id="c752e-156">Return the absolute URI to a snapshot</span></span>
<span data-ttu-id="c752e-157">W tym przykładzie kodu C# tworzy migawkę i zapisuje limit bezwzględny identyfikator URI lokalizacji głównej.</span><span class="sxs-lookup"><span data-stu-id="c752e-157">This C# code example creates a snapshot and writes out the absolute URI for the primary location.</span></span>

```csharp
//Create the blob service client object.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";

CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

//Get a reference to a container.
CloudBlobContainer container = blobClient.GetContainerReference("sample-container");
container.CreateIfNotExists();

//Get a reference to a blob.
CloudBlockBlob blob = container.GetBlockBlobReference("sampleblob.txt");
blob.UploadText("This is a blob.");

//Create a snapshot of the blob and write out its primary URI.
CloudBlockBlob blobSnapshot = blob.CreateSnapshot();
Console.WriteLine(blobSnapshot.SnapshotQualifiedStorageUri.PrimaryUri);
```

## <a name="understand-how-snapshots-accrue-charges"></a><span data-ttu-id="c752e-158">Zrozumienie sposobu migawki naliczania opłat</span><span class="sxs-lookup"><span data-stu-id="c752e-158">Understand how snapshots accrue charges</span></span>
<span data-ttu-id="c752e-159">Tworzenie migawek, która jest tylko do odczytu kopię obiektu blob, może spowodować opłaty za magazyn dodatkowe dane do Twojego konta.</span><span class="sxs-lookup"><span data-stu-id="c752e-159">Creating a snapshot, which is a read-only copy of a blob, can result in additional data storage charges to your account.</span></span> <span data-ttu-id="c752e-160">Podczas projektowania aplikacji, należy mieć świadomość sposobu naliczania może tych opłat, dzięki czemu można zminimalizować koszty.</span><span class="sxs-lookup"><span data-stu-id="c752e-160">When designing your application, it is important to be aware of how these charges might accrue so that you can minimize costs.</span></span>

### <a name="important-billing-considerations"></a><span data-ttu-id="c752e-161">Istotne zagadnienia dotyczące rozliczeń</span><span class="sxs-lookup"><span data-stu-id="c752e-161">Important billing considerations</span></span>
<span data-ttu-id="c752e-162">Poniższa lista zawiera klucz wskazuje należy wziąć pod uwagę podczas tworzenia migawki.</span><span class="sxs-lookup"><span data-stu-id="c752e-162">The following list includes key points to consider when creating a snapshot.</span></span>

* <span data-ttu-id="c752e-163">Konta magazynu ponosi opłaty za bloki unikatowy lub stron, czy znajdują się w obiekcie blob lub w migawce.</span><span class="sxs-lookup"><span data-stu-id="c752e-163">Your storage account incurs charges for unique blocks or pages, whether they are in the blob or in the snapshot.</span></span> <span data-ttu-id="c752e-164">Twoje konto nie spowodować naliczenie dodatkowych opłat za migawki skojarzone z obiektu blob, dopóki nie zostanie zaktualizowany obiekt blob, na którym są one oparte na.</span><span class="sxs-lookup"><span data-stu-id="c752e-164">Your account does not incur additional charges for snapshots associated with a blob until you update the blob on which they are based.</span></span> <span data-ttu-id="c752e-165">Po zaktualizowaniu podstawowego obiektu blob diverges go z jego migawek.</span><span class="sxs-lookup"><span data-stu-id="c752e-165">After you update the base blob, it diverges from its snapshots.</span></span> <span data-ttu-id="c752e-166">W takim przypadku są naliczane opłaty za bloki unikatowy lub strony w poszczególnych obiektów blob lub migawki.</span><span class="sxs-lookup"><span data-stu-id="c752e-166">When this happens, you are charged for the unique blocks or pages in each blob or snapshot.</span></span>
* <span data-ttu-id="c752e-167">Podczas zastępowania blok w ramach blokowych obiektów blob tego bloku jest następnie rozliczany jako unikatowy bloku.</span><span class="sxs-lookup"><span data-stu-id="c752e-167">When you replace a block within a block blob, that block is subsequently charged as a unique block.</span></span> <span data-ttu-id="c752e-168">Dotyczy to nawet wtedy, gdy blok ma ten sam identyfikator bloku i samych danych, ponieważ ma ona migawki.</span><span class="sxs-lookup"><span data-stu-id="c752e-168">This is true even if the block has the same block ID and the same data as it has in the snapshot.</span></span> <span data-ttu-id="c752e-169">Po bloku dba ponownie, diverges go z jego odpowiednikiem w dowolnym migawki i zostanie naliczona danych.</span><span class="sxs-lookup"><span data-stu-id="c752e-169">After the block is committed again, it diverges from its counterpart in any snapshot, and you will be charged for its data.</span></span> <span data-ttu-id="c752e-170">To samo dla strony w stronicowych obiektów blob, która jest aktualizowana mają identyczne dane.</span><span class="sxs-lookup"><span data-stu-id="c752e-170">The same holds true for a page in a page blob that's updated with identical data.</span></span>
* <span data-ttu-id="c752e-171">Zastępowanie blokowych obiektów blob, wywołując [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], lub [UploadFromByteArray] [ dotnet_UploadFromByteArray] metoda zastępuje wszystkie bloki w obiekcie blob.</span><span class="sxs-lookup"><span data-stu-id="c752e-171">Replacing a block blob by calling the [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray] method replaces all blocks in the blob.</span></span> <span data-ttu-id="c752e-172">Jeśli masz migawki skojarzone z tego obiektu blob, wszystkie bloki w podstawowej obiektów blob i migawki teraz różni się i zostanie naliczona dla wszystkich bloków w obu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="c752e-172">If you have a snapshot associated with that blob, all blocks in the base blob and snapshot now diverge, and you will be charged for all the blocks in both blobs.</span></span> <span data-ttu-id="c752e-173">Dotyczy to nawet wtedy, gdy dane w podstawowej obiektów blob i migawki pozostają identyczne.</span><span class="sxs-lookup"><span data-stu-id="c752e-173">This is true even if the data in the base blob and the snapshot remain identical.</span></span>
* <span data-ttu-id="c752e-174">Usługa Azure Blob nie ma sposób, aby określić, czy dwa bloki zawierają identyczne dane.</span><span class="sxs-lookup"><span data-stu-id="c752e-174">The Azure Blob service does not have a means to determine whether two blocks contain identical data.</span></span> <span data-ttu-id="c752e-175">Każdy blok przekazane i zatwierdzone jest traktowany jako unikatowy, nawet jeśli ma te same dane i ten sam identyfikator bloku.</span><span class="sxs-lookup"><span data-stu-id="c752e-175">Each block that is uploaded and committed is treated as unique, even if it has the same data and the same block ID.</span></span> <span data-ttu-id="c752e-176">Ponieważ opłaty naliczane unikatowy bloków, należy wziąć pod uwagę, że aktualizowanie obiektu blob zawierający migawki spowoduje dodatkowe bloki unikatowy dodatkowych opłat.</span><span class="sxs-lookup"><span data-stu-id="c752e-176">Because charges accrue for unique blocks, it's important to consider that updating a blob that has a snapshot results in additional unique blocks and additional charges.</span></span>

### <a name="minimize-cost-with-snapshot-management"></a><span data-ttu-id="c752e-177">Minimalizuje koszt z zarządzania migawkami</span><span class="sxs-lookup"><span data-stu-id="c752e-177">Minimize cost with snapshot management</span></span>

<span data-ttu-id="c752e-178">Zaleca się zarządzanie migawki w dokładnie, aby uniknąć dodatkowych opłat.</span><span class="sxs-lookup"><span data-stu-id="c752e-178">We recommend managing your snapshots carefully to avoid extra charges.</span></span> <span data-ttu-id="c752e-179">Możesz wykonać następujące najlepsze rozwiązania, aby zminimalizować kosztów ponoszonych przez Magazyn z migawki:</span><span class="sxs-lookup"><span data-stu-id="c752e-179">You can follow these best practices to help minimize the costs incurred by the storage of your snapshots:</span></span>

* <span data-ttu-id="c752e-180">Usunięcie i ponowne utworzenie migawki skojarzone z obiektu blob po zaktualizowaniu obiektu blob, nawet jeśli aktualizujesz mają identyczne dane, chyba że projektu aplikacji wymaga, aby zachować migawki.</span><span class="sxs-lookup"><span data-stu-id="c752e-180">Delete and re-create snapshots associated with a blob whenever you update the blob, even if you are updating with identical data, unless your application design requires that you maintain snapshots.</span></span> <span data-ttu-id="c752e-181">Przez usunięcie i ponowne utworzenie migawki obiektu blob, można zagwarantować, że migawki i obiektów blob nie odbiegają.</span><span class="sxs-lookup"><span data-stu-id="c752e-181">By deleting and re-creating the blob's snapshots, you can ensure that the blob and snapshots do not diverge.</span></span>
* <span data-ttu-id="c752e-182">Jeśli obsługujesz migawek dla obiekt blob, należy unikać wywoływania [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], lub [UploadFromByteArray] [ dotnet_UploadFromByteArray] można zaktualizować obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="c752e-182">If you are maintaining snapshots for a blob, avoid calling [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray] to update the blob.</span></span> <span data-ttu-id="c752e-183">Te metody zastąpić wszystkie bloki w obiekcie blob, powodując sieci podstawowej obiektów blob i jego migawek odchodzenia znacznie.</span><span class="sxs-lookup"><span data-stu-id="c752e-183">These methods replace all of the blocks in the blob, causing your base blob and its snapshots to diverge significantly.</span></span> <span data-ttu-id="c752e-184">Zamiast tego należy zaktualizować za pomocą najmniejszej liczby bloków [PutBlock] [ dotnet_PutBlock] i [metoda PutBlockList] [ dotnet_PutBlockList] metody.</span><span class="sxs-lookup"><span data-stu-id="c752e-184">Instead, update the fewest possible number of blocks by using the [PutBlock][dotnet_PutBlock] and [PutBlockList][dotnet_PutBlockList] methods.</span></span>

### <a name="snapshot-billing-scenarios"></a><span data-ttu-id="c752e-185">Migawki rozliczeń scenariuszy</span><span class="sxs-lookup"><span data-stu-id="c752e-185">Snapshot billing scenarios</span></span>
<span data-ttu-id="c752e-186">Poniższe scenariusze pokazują, jak Naliczanie opłat dla blokowych obiektów blob i jego migawek.</span><span class="sxs-lookup"><span data-stu-id="c752e-186">The following scenarios demonstrate how charges accrue for a block blob and its snapshots.</span></span>

<span data-ttu-id="c752e-187">**Scenariusz 1**</span><span class="sxs-lookup"><span data-stu-id="c752e-187">**Scenario 1**</span></span>

<span data-ttu-id="c752e-188">W scenariuszu 1 podstawowego obiektu blob nie został zaktualizowany po migawki, więc jest obciążany tylko dla bloków unikatowy 1, 2 i 3.</span><span class="sxs-lookup"><span data-stu-id="c752e-188">In scenario 1, the base blob has not been updated after the snapshot was taken, so charges are incurred only for unique blocks 1, 2, and 3.</span></span>

![Zasoby usługi Azure Storage](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-1.png)

<span data-ttu-id="c752e-190">**Scenariusz 2**</span><span class="sxs-lookup"><span data-stu-id="c752e-190">**Scenario 2**</span></span>

<span data-ttu-id="c752e-191">W scenariuszu 2 podstawowego obiektu blob zostały zaktualizowane, ale migawka nie ma.</span><span class="sxs-lookup"><span data-stu-id="c752e-191">In scenario 2, the base blob has been updated, but the snapshot has not.</span></span> <span data-ttu-id="c752e-192">Blok 3 został zaktualizowany, a nawet, jeśli zawiera te same dane, a tym samym identyfikatorze, nie jest taka sama jak zablokować 3 w migawce.</span><span class="sxs-lookup"><span data-stu-id="c752e-192">Block 3 was updated, and even though it contains the same data and the same ID, it is not the same as block 3 in the snapshot.</span></span> <span data-ttu-id="c752e-193">W związku z tym konta jest pobierana cztery bloków.</span><span class="sxs-lookup"><span data-stu-id="c752e-193">As a result, the account is charged for four blocks.</span></span>

![Zasoby usługi Azure Storage](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-2.png)

<span data-ttu-id="c752e-195">**Scenariusz 3**</span><span class="sxs-lookup"><span data-stu-id="c752e-195">**Scenario 3**</span></span>

<span data-ttu-id="c752e-196">W scenariuszu 3 podstawowego obiektu blob zostały zaktualizowane, ale migawka nie ma.</span><span class="sxs-lookup"><span data-stu-id="c752e-196">In scenario 3, the base blob has been updated, but the snapshot has not.</span></span> <span data-ttu-id="c752e-197">3 blokowych zamieniono bloku 4 w obiekcie blob podstawowej, ale migawki nadal odzwierciedla blok 3.</span><span class="sxs-lookup"><span data-stu-id="c752e-197">Block 3 was replaced with block 4 in the base blob, but the snapshot still reflects block 3.</span></span> <span data-ttu-id="c752e-198">W związku z tym konta jest pobierana cztery bloków.</span><span class="sxs-lookup"><span data-stu-id="c752e-198">As a result, the account is charged for four blocks.</span></span>

![Zasoby usługi Azure Storage](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-3.png)

<span data-ttu-id="c752e-200">**Scenariusz 4**</span><span class="sxs-lookup"><span data-stu-id="c752e-200">**Scenario 4**</span></span>

<span data-ttu-id="c752e-201">W scenariuszu 4 podstawowego obiektu blob została całkowicie zaktualizowana i zawiera żaden z jego oryginalnych bloków.</span><span class="sxs-lookup"><span data-stu-id="c752e-201">In scenario 4, the base blob has been completely updated and contains none of its original blocks.</span></span> <span data-ttu-id="c752e-202">W związku z tym rozliczany konta dla wszystkich osiem bloków unikatowy.</span><span class="sxs-lookup"><span data-stu-id="c752e-202">As a result, the account is charged for all eight unique blocks.</span></span> <span data-ttu-id="c752e-203">Ten scenariusz może wystąpić, jeśli używasz metody aktualizacji takich jak [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], lub [UploadFromByteArray][dotnet_UploadFromByteArray], ponieważ metody te zastąpienie całej zawartości obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="c752e-203">This scenario can occur if you are using an update method such as [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray], because these methods replace all of the contents of a blob.</span></span>

![Zasoby usługi Azure Storage](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-4.png)

## <a name="next-steps"></a><span data-ttu-id="c752e-205">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c752e-205">Next steps</span></span>

* <span data-ttu-id="c752e-206">Można znaleźć więcej informacji na temat pracy z migawek dysków maszyny wirtualnej (VM) w [kopia zapasowa Azure niezarządzane dysków maszyny Wirtualnej z migawkami przyrostowe](../../virtual-machines/windows/incremental-snapshots.md)</span><span class="sxs-lookup"><span data-stu-id="c752e-206">You can find more information about working with virtual machine (VM) disk snapshots in [Back up Azure unmanaged VM disks with incremental snapshots](../../virtual-machines/windows/incremental-snapshots.md)</span></span>

* <span data-ttu-id="c752e-207">Dla dodatkowych przykładów kodu przy użyciu magazynu obiektów Blob, zobacz [przykłady kodu Azure](https://azure.microsoft.com/documentation/samples/?service=storage&term=blob).</span><span class="sxs-lookup"><span data-stu-id="c752e-207">For additional code examples using Blob storage, see [Azure Code Samples](https://azure.microsoft.com/documentation/samples/?service=storage&term=blob).</span></span> <span data-ttu-id="c752e-208">Możesz pobrać przykładową aplikację i uruchom go lub Przeglądaj kodu w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="c752e-208">You can download a sample application and run it, or browse the code on GitHub.</span></span>

[dotnet_AccessCondition]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.accesscondition.aspx
[dotnet_CloudBlockBlob]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.aspx
[dotnet_CreateSnapshotAsync]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.createsnapshotasync.aspx
[dotnet_HTTPStatusCode]: https://msdn.microsoft.com/library/system.net.httpstatuscode(v=vs.110).aspx
[dotnet_PutBlockList]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.putblocklist.aspx
[dotnet_PutBlock]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.putblock.aspx
[dotnet_UploadFromByteArray]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.uploadfrombytearray.aspx
[dotnet_UploadFromFile]: https://msdn.microsoft.com/library/azure/mt705654.aspx
[dotnet_UploadFromStream]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.uploadfromstream.aspx
[dotnet_UploadText]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.uploadtext.aspx