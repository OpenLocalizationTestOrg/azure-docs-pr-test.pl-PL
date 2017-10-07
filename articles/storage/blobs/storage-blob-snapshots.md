---
title: "aaaCreate migawki tylko do odczytu obiektów blob w usłudze Azure Storage | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate migawkę tooback obiektów blob, zapasową danych obiektów blob w danym momencie w czasie. Zrozumienie, jak migawki są rozliczane i jak toouse ich toominimize pojemności opłat."
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
ms.openlocfilehash: 57f2e76b8899b8a513688bf148dd13673141d5bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-blob-snapshot"></a><span data-ttu-id="2e058-104">Tworzenie migawki obiektu blob</span><span class="sxs-lookup"><span data-stu-id="2e058-104">Create a blob snapshot</span></span>

<span data-ttu-id="2e058-105">Migawka jest tylko do odczytu wersji obiektu blob, która jest wykonywana w punkcie w czasie.</span><span class="sxs-lookup"><span data-stu-id="2e058-105">A snapshot is a read-only version of a blob that's taken at a point in time.</span></span> <span data-ttu-id="2e058-106">Migawki są przydatne w przypadku tworzenia kopii zapasowej obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="2e058-106">Snapshots are useful for backing up blobs.</span></span> <span data-ttu-id="2e058-107">Po utworzeniu migawki, odczytu, skopiuj lub usuń go, ale nie można go modyfikować.</span><span class="sxs-lookup"><span data-stu-id="2e058-107">After you create a snapshot, you can read, copy, or delete it, but you cannot modify it.</span></span>

<span data-ttu-id="2e058-108">Migawki obiektu blob jest identyczne tooits podstawowego obiektu blob, z wyjątkiem tego obiektu blob hello identyfikator URI ma **DateTime** wartość dołączona toohello obiektu blob identyfikatora URI tooindicate hello czas na które hello migawki.</span><span class="sxs-lookup"><span data-stu-id="2e058-108">A snapshot of a blob is identical tooits base blob, except that hello blob URI has a **DateTime** value appended toohello blob URI tooindicate hello time at which hello snapshot was taken.</span></span> <span data-ttu-id="2e058-109">Na przykład jeśli identyfikator URI obiektu blob strony jest `http://storagesample.core.blob.windows.net/mydrives/myvhd`, hello migawki identyfikatora URI jest zbyt podobne`http://storagesample.core.blob.windows.net/mydrives/myvhd?snapshot=2011-03-09T01:42:34.9360000Z`.</span><span class="sxs-lookup"><span data-stu-id="2e058-109">For example, if a page blob URI is `http://storagesample.core.blob.windows.net/mydrives/myvhd`, hello snapshot URI is similar too`http://storagesample.core.blob.windows.net/mydrives/myvhd?snapshot=2011-03-09T01:42:34.9360000Z`.</span></span>

> [!NOTE]
> <span data-ttu-id="2e058-110">Wszystkie migawki mają hello podstawowej przez identyfikator URI obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="2e058-110">All snapshots share hello base blob's URI.</span></span> <span data-ttu-id="2e058-111">Witaj różnicy między hello podstawowej obiektów blob i migawki hello jest dołączany hello tylko **DateTime** wartość.</span><span class="sxs-lookup"><span data-stu-id="2e058-111">hello only distinction between hello base blob and hello snapshot is hello appended **DateTime** value.</span></span>
>

<span data-ttu-id="2e058-112">Obiekt blob może mieć dowolną liczbę migawek.</span><span class="sxs-lookup"><span data-stu-id="2e058-112">A blob can have any number of snapshots.</span></span> <span data-ttu-id="2e058-113">Migawki zachować, dopóki nie zostaną jawnie usunięte.</span><span class="sxs-lookup"><span data-stu-id="2e058-113">Snapshots persist until they are explicitly deleted.</span></span> <span data-ttu-id="2e058-114">Migawka nie outlive jego podstawowego obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="2e058-114">A snapshot cannot outlive its base blob.</span></span> <span data-ttu-id="2e058-115">Można wyliczyć hello migawki skojarzone z hello tootrack podstawowego obiektu blob z bieżącej migawki.</span><span class="sxs-lookup"><span data-stu-id="2e058-115">You can enumerate hello snapshots associated with hello base blob tootrack your current snapshots.</span></span>

<span data-ttu-id="2e058-116">Po utworzeniu migawki obiektu blob hello właściwości systemu obiektu blob są takie same wartości migawki toohello skopiowanych z hello.</span><span class="sxs-lookup"><span data-stu-id="2e058-116">When you create a snapshot of a blob, hello blob's system properties are copied toohello snapshot with hello same values.</span></span> <span data-ttu-id="2e058-117">Metadane obiektu blob Hello podstawowy jest również skopiowanych toohello migawki, chyba że zostanie oddzielne metadanych dla hello migawki podczas jego tworzenia.</span><span class="sxs-lookup"><span data-stu-id="2e058-117">hello base blob's metadata is also copied toohello snapshot, unless you specify separate metadata for hello snapshot when you create it.</span></span>

<span data-ttu-id="2e058-118">Wszystkie dzierżawy skojarzonego z obiektem blob podstawowej hello nie wpływają na powitania migawki.</span><span class="sxs-lookup"><span data-stu-id="2e058-118">Any leases associated with hello base blob do not affect hello snapshot.</span></span> <span data-ttu-id="2e058-119">Nie można pobrać dzierżawy na migawki.</span><span class="sxs-lookup"><span data-stu-id="2e058-119">You cannot acquire a lease on a snapshot.</span></span>

<span data-ttu-id="2e058-120">Plik VHD jest używane toostore hello aktualne informacje i stan dysku maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2e058-120">A VHD file is used toostore hello current information and status for a VM disk.</span></span> <span data-ttu-id="2e058-121">Można odłączyć dysku od wewnątrz hello maszyny Wirtualnej lub zamknąć hello maszyny Wirtualnej, a następnie Utwórz migawkę jego plik VHD.</span><span class="sxs-lookup"><span data-stu-id="2e058-121">You can detach a disk from within hello VM or shut down hello VM, and then take a snapshot of its VHD file.</span></span> <span data-ttu-id="2e058-122">Możesz użyć tego pliku migawki nowsze hello tooretrieve wirtualnego dysku twardego plików w danym momencie i Utwórz ponownie hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2e058-122">You can use that snapshot file later tooretrieve hello VHD file at that point in time and recreate hello VM.</span></span>

<span data-ttu-id="2e058-123">Jeśli włączono szyfrowanie usługi Magazyn (SSE) dla konta magazynu hello w których hello znajduje się obiekt blob, a następnie magazynowane zostaną zaszyfrowane wszystkie migawki wziąć pod uwagę tego obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="2e058-123">If Storage Service Encryption (SSE) is enabled for hello storage account in which hello blob resides, then any snapshots taken of that blob will be encrypted at rest.</span></span>

## <a name="create-a-snapshot"></a><span data-ttu-id="2e058-124">Utwórz migawkę</span><span class="sxs-lookup"><span data-stu-id="2e058-124">Create a snapshot</span></span>
<span data-ttu-id="2e058-125">Witaj Poniższy przykładowy kod przedstawia sposób hello toocreate migawki za pomocą [biblioteki klienta magazynu Azure dla platformy .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span><span class="sxs-lookup"><span data-stu-id="2e058-125">hello following code example shows how toocreate a snapshot by using hello [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span></span> <span data-ttu-id="2e058-126">W tym przykładzie określa dodatkowe metadane dla migawki hello podczas jego tworzenia.</span><span class="sxs-lookup"><span data-stu-id="2e058-126">This example specifies additional metadata for hello snapshot when it is created.</span></span>

```csharp
private static async Task CreateBlockBlobSnapshot(CloudBlobContainer container)
{
    // Create a new block blob in hello container.
    CloudBlockBlob baseBlob = container.GetBlockBlobReference("sample-base-blob.txt");

    // Add blob metadata.
    baseBlob.Metadata.Add("ApproxBlobCreatedDate", DateTime.UtcNow.ToString());

    try
    {
        // Upload hello blob toocreate it, with its metadata.
        await baseBlob.UploadTextAsync(string.Format("Base blob: {0}", baseBlob.Uri.ToString()));

        // Sleep 5 seconds.
        System.Threading.Thread.Sleep(5000);

        // Create a snapshot of hello base blob.
        // Specify metadata at hello time that hello snapshot is created toospecify unique metadata for hello snapshot.
        // If no metadata is specified when hello snapshot is created, hello base blob's metadata is copied toohello snapshot.
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

## <a name="copy-snapshots"></a><span data-ttu-id="2e058-127">Kopiowanie migawek</span><span class="sxs-lookup"><span data-stu-id="2e058-127">Copy snapshots</span></span>
<span data-ttu-id="2e058-128">Operacje kopiowania obejmujące obiekty BLOB i migawek wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="2e058-128">Copy operations involving blobs and snapshots follow these rules:</span></span>

* <span data-ttu-id="2e058-129">Możesz skopiować migawki za pośrednictwem jego podstawowego obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="2e058-129">You can copy a snapshot over its base blob.</span></span> <span data-ttu-id="2e058-130">Promowanie pozycji toohello migawki obiektu blob podstawowej hello, można przywrócić wcześniejszą wersję obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="2e058-130">By promoting a snapshot toohello position of hello base blob, you can restore an earlier version of a blob.</span></span> <span data-ttu-id="2e058-131">Witaj pozostaje migawki, ale hello podstawowego obiektu blob jest zastępowany kopię zapisu hello migawki.</span><span class="sxs-lookup"><span data-stu-id="2e058-131">hello snapshot remains, but hello base blob is overwritten with a writable copy of hello snapshot.</span></span>
* <span data-ttu-id="2e058-132">Można skopiować obiektu blob migawki tooa docelowy o innej nazwie.</span><span class="sxs-lookup"><span data-stu-id="2e058-132">You can copy a snapshot tooa destination blob with a different name.</span></span> <span data-ttu-id="2e058-133">Hello wynikowy docelowego obiektu blob jest zapisywalny obiektów blob i nie migawki.</span><span class="sxs-lookup"><span data-stu-id="2e058-133">hello resulting destination blob is a writable blob and not a snapshot.</span></span>
* <span data-ttu-id="2e058-134">Po skopiowaniu źródłowego obiektu blob wszystkie migawki hello źródłowego obiektu blob nie są toohello skopiowanych docelowego.</span><span class="sxs-lookup"><span data-stu-id="2e058-134">When a source blob is copied, any snapshots of hello source blob are not copied toohello destination.</span></span> <span data-ttu-id="2e058-135">Gdy docelowego obiektu blob jest zastępowany kopii, wszystkie migawki skojarzone z hello oryginalnego docelowego obiektu blob pozostaną nienaruszone.</span><span class="sxs-lookup"><span data-stu-id="2e058-135">When a destination blob is overwritten with a copy, any snapshots associated with hello original destination blob remain intact.</span></span>
* <span data-ttu-id="2e058-136">Po utworzeniu migawki blokowych obiektów blob zablokowanych zatwierdzone hello blob jest również skopiowanych toohello migawki.</span><span class="sxs-lookup"><span data-stu-id="2e058-136">When you create a snapshot of a block blob, hello blob's committed block list is also copied toohello snapshot.</span></span> <span data-ttu-id="2e058-137">Niezatwierdzone bloków nie są kopiowane.</span><span class="sxs-lookup"><span data-stu-id="2e058-137">Any uncommitted blocks are not copied.</span></span>

## <a name="specify-an-access-condition"></a><span data-ttu-id="2e058-138">Określ warunek dostępu</span><span class="sxs-lookup"><span data-stu-id="2e058-138">Specify an access condition</span></span>
<span data-ttu-id="2e058-139">Podczas wywoływania [CreateSnapshotAsync][dotnet_CreateSnapshotAsync], można określić warunki dostępu, dzięki czemu hello migawki jest tworzony tylko wtedy, gdy warunek jest spełniony.</span><span class="sxs-lookup"><span data-stu-id="2e058-139">When you call [CreateSnapshotAsync][dotnet_CreateSnapshotAsync], you can specify an access condition so that hello snapshot is created only if a condition is met.</span></span> <span data-ttu-id="2e058-140">toospecify warunki dostępu, użyj hello [AccessCondition] [ dotnet_AccessCondition] parametru.</span><span class="sxs-lookup"><span data-stu-id="2e058-140">toospecify an access condition, use hello [AccessCondition][dotnet_AccessCondition] parameter.</span></span> <span data-ttu-id="2e058-141">Jeśli hello określony warunek nie jest spełniony, nie jest utworzona migawka hello i hello usługa Blob zwraca kod stanu [HTTPStatusCode][dotnet_HTTPStatusCode]. PreconditionFailed.</span><span class="sxs-lookup"><span data-stu-id="2e058-141">If hello specified condition is not met, hello snapshot is not created, and hello Blob service returns status code [HTTPStatusCode][dotnet_HTTPStatusCode].PreconditionFailed.</span></span>

## <a name="delete-snapshots"></a><span data-ttu-id="2e058-142">Usuń migawki</span><span class="sxs-lookup"><span data-stu-id="2e058-142">Delete snapshots</span></span>
<span data-ttu-id="2e058-143">Nie można usunąć obiektu blob z migawkami, chyba że hello migawek, również zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="2e058-143">You can't delete a blob with snapshots unless hello snapshots are also deleted.</span></span> <span data-ttu-id="2e058-144">Możesz usunąć migawkę indywidualnie lub określ, że wszystkie migawki usunięte po usunięciu hello źródłowego obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="2e058-144">You can delete a snapshot individually, or specify that all snapshots be deleted when hello source blob is deleted.</span></span> <span data-ttu-id="2e058-145">Jeśli próba toodelete obiektu blob, które nadal istnieją migawki, powoduje błąd.</span><span class="sxs-lookup"><span data-stu-id="2e058-145">If you attempt toodelete a blob that still has snapshots, an error results.</span></span>

<span data-ttu-id="2e058-146">Witaj, jak po przedstawia przykładowy kod toodelete obiektu blob i jego migawek w środowisku .NET, gdzie `blockBlob` jest obiektem typu [CloudBlockBlob][dotnet_CloudBlockBlob]:</span><span class="sxs-lookup"><span data-stu-id="2e058-146">hello following code example shows how toodelete a blob and its snapshots in .NET, where `blockBlob` is an object of type [CloudBlockBlob][dotnet_CloudBlockBlob]:</span></span>

```csharp
await blockBlob.DeleteIfExistsAsync(DeleteSnapshotsOption.IncludeSnapshots, null, null, null);
```

## <a name="snapshots-with-azure-premium-storage"></a><span data-ttu-id="2e058-147">Migawki z magazynem Azure — warstwa Premium</span><span class="sxs-lookup"><span data-stu-id="2e058-147">Snapshots with Azure Premium Storage</span></span>
<span data-ttu-id="2e058-148">Korzystając z migawki z magazyn w warstwie Premium, zastosuj hello następujące reguły:</span><span class="sxs-lookup"><span data-stu-id="2e058-148">When using snapshots with Premium Storage, hello following rules apply:</span></span>

* <span data-ttu-id="2e058-149">Maksymalna liczba migawek na stronicowych obiektów blob na koncie magazynu premium Hello to 100.</span><span class="sxs-lookup"><span data-stu-id="2e058-149">hello maximum number of snapshots per page blob in a premium storage account is 100.</span></span> <span data-ttu-id="2e058-150">Zwraca kod błędu 409, po przekroczeniu tego limitu hello migawki obiektu Blob operacji (`SnapshotCountExceeded`).</span><span class="sxs-lookup"><span data-stu-id="2e058-150">If that limit is exceeded, hello Snapshot Blob operation returns error code 409 (`SnapshotCountExceeded`).</span></span>
* <span data-ttu-id="2e058-151">Można utworzyć migawkę stronicowych obiektów blob na koncie magazynu premium co 10 minut.</span><span class="sxs-lookup"><span data-stu-id="2e058-151">You can take a snapshot of a page blob in a premium storage account once every 10 minutes.</span></span> <span data-ttu-id="2e058-152">Zwraca kod błędu 409, po przekroczeniu tego kursu hello migawki obiektu Blob operacji (`SnapshotOperationRateExceeded`).</span><span class="sxs-lookup"><span data-stu-id="2e058-152">If that rate is exceeded, hello Snapshot Blob operation returns error code 409 (`SnapshotOperationRateExceeded`).</span></span>
* <span data-ttu-id="2e058-153">tooread migawki, można użyć toocopy operacji kopiowania obiektu Blob hello tooanother migawki stronicowy obiekt blob na koncie hello.</span><span class="sxs-lookup"><span data-stu-id="2e058-153">tooread a snapshot, you can use hello Copy Blob operation toocopy a snapshot tooanother page blob in hello account.</span></span> <span data-ttu-id="2e058-154">Hello docelowego obiektu blob dla operacji kopiowania hello nie może mieć żadnych istniejących migawki.</span><span class="sxs-lookup"><span data-stu-id="2e058-154">hello destination blob for hello copy operation must not have any existing snapshots.</span></span> <span data-ttu-id="2e058-155">Jeśli hello docelowego obiektu blob migawki, a następnie zwraca kod błędu 409, hello operacji kopiowania obiektów Blob (`SnapshotsPresent`).</span><span class="sxs-lookup"><span data-stu-id="2e058-155">If hello destination blob does have snapshots, then hello Copy Blob operation returns error code 409 (`SnapshotsPresent`).</span></span>

## <a name="return-hello-absolute-uri-tooa-snapshot"></a><span data-ttu-id="2e058-156">Zwraca hello bezwzględny identyfikator URI tooa migawki</span><span class="sxs-lookup"><span data-stu-id="2e058-156">Return hello absolute URI tooa snapshot</span></span>
<span data-ttu-id="2e058-157">W tym przykładzie kodu C# tworzy migawkę i zapisuje się hello bezwzględny identyfikator URI dla hello lokalizacji głównej.</span><span class="sxs-lookup"><span data-stu-id="2e058-157">This C# code example creates a snapshot and writes out hello absolute URI for hello primary location.</span></span>

```csharp
//Create hello blob service client object.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";

CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

//Get a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("sample-container");
container.CreateIfNotExists();

//Get a reference tooa blob.
CloudBlockBlob blob = container.GetBlockBlobReference("sampleblob.txt");
blob.UploadText("This is a blob.");

//Create a snapshot of hello blob and write out its primary URI.
CloudBlockBlob blobSnapshot = blob.CreateSnapshot();
Console.WriteLine(blobSnapshot.SnapshotQualifiedStorageUri.PrimaryUri);
```

## <a name="understand-how-snapshots-accrue-charges"></a><span data-ttu-id="2e058-158">Zrozumienie sposobu migawki naliczania opłat</span><span class="sxs-lookup"><span data-stu-id="2e058-158">Understand how snapshots accrue charges</span></span>
<span data-ttu-id="2e058-159">Tworzenie migawek, która jest tylko do odczytu kopię obiektu blob, może spowodować konta tooyour opłaty za magazyn dodatkowe dane.</span><span class="sxs-lookup"><span data-stu-id="2e058-159">Creating a snapshot, which is a read-only copy of a blob, can result in additional data storage charges tooyour account.</span></span> <span data-ttu-id="2e058-160">Podczas projektowania aplikacji, jest ważne toobe uwagę sposobu naliczania może tych opłat, dzięki czemu można zminimalizować koszty.</span><span class="sxs-lookup"><span data-stu-id="2e058-160">When designing your application, it is important toobe aware of how these charges might accrue so that you can minimize costs.</span></span>

### <a name="important-billing-considerations"></a><span data-ttu-id="2e058-161">Istotne zagadnienia dotyczące rozliczeń</span><span class="sxs-lookup"><span data-stu-id="2e058-161">Important billing considerations</span></span>
<span data-ttu-id="2e058-162">następujące listy Hello obejmuje tooconsider klucz wskazuje podczas tworzenia migawki.</span><span class="sxs-lookup"><span data-stu-id="2e058-162">hello following list includes key points tooconsider when creating a snapshot.</span></span>

* <span data-ttu-id="2e058-163">Konta magazynu ponosi opłaty za bloki unikatowy lub stron, czy znajdują się w obiekcie blob hello lub w migawce hello.</span><span class="sxs-lookup"><span data-stu-id="2e058-163">Your storage account incurs charges for unique blocks or pages, whether they are in hello blob or in hello snapshot.</span></span> <span data-ttu-id="2e058-164">Twoje konto nie spowodować naliczenie dodatkowych opłat za migawki skojarzone z obiektu blob, dopóki nie zostanie zaktualizowany hello obiektów blob, na którym są one oparte na.</span><span class="sxs-lookup"><span data-stu-id="2e058-164">Your account does not incur additional charges for snapshots associated with a blob until you update hello blob on which they are based.</span></span> <span data-ttu-id="2e058-165">Po zaktualizowaniu obiektu blob podstawowej hello diverges go z jego migawek.</span><span class="sxs-lookup"><span data-stu-id="2e058-165">After you update hello base blob, it diverges from its snapshots.</span></span> <span data-ttu-id="2e058-166">W takim przypadku są naliczane opłaty za bloki unikatowy hello lub strony w poszczególnych obiektów blob lub migawki.</span><span class="sxs-lookup"><span data-stu-id="2e058-166">When this happens, you are charged for hello unique blocks or pages in each blob or snapshot.</span></span>
* <span data-ttu-id="2e058-167">Podczas zastępowania blok w ramach blokowych obiektów blob tego bloku jest następnie rozliczany jako unikatowy bloku.</span><span class="sxs-lookup"><span data-stu-id="2e058-167">When you replace a block within a block blob, that block is subsequently charged as a unique block.</span></span> <span data-ttu-id="2e058-168">Dotyczy to nawet wtedy, gdy blok hello ma hello sam identyfikator blokowania i hello na tym samym ma dane w postaci w migawce hello.</span><span class="sxs-lookup"><span data-stu-id="2e058-168">This is true even if hello block has hello same block ID and hello same data as it has in hello snapshot.</span></span> <span data-ttu-id="2e058-169">Po bloku hello dba ponownie, diverges go z jego odpowiednikiem w dowolnym migawki i zostanie naliczona danych.</span><span class="sxs-lookup"><span data-stu-id="2e058-169">After hello block is committed again, it diverges from its counterpart in any snapshot, and you will be charged for its data.</span></span> <span data-ttu-id="2e058-170">powitalne samo dla strony w stronicowych obiektów blob, która jest aktualizowana mają identyczne dane.</span><span class="sxs-lookup"><span data-stu-id="2e058-170">hello same holds true for a page in a page blob that's updated with identical data.</span></span>
* <span data-ttu-id="2e058-171">Zastępowanie blokowych obiektów blob przez wywołanie hello [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream] [ dotnet_UploadFromStream], lub [UploadFromByteArray] [ dotnet_UploadFromByteArray] metoda zastępuje wszystkie bloki w obiekcie blob hello.</span><span class="sxs-lookup"><span data-stu-id="2e058-171">Replacing a block blob by calling hello [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray] method replaces all blocks in hello blob.</span></span> <span data-ttu-id="2e058-172">Jeśli masz migawki skojarzone z tego obiektu blob, teraz odchodzenia wszystkich bloków blob podstawowej hello i migawki, a zostanie naliczona dla wszystkich bloków hello w obu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="2e058-172">If you have a snapshot associated with that blob, all blocks in hello base blob and snapshot now diverge, and you will be charged for all hello blocks in both blobs.</span></span> <span data-ttu-id="2e058-173">Dotyczy to nawet wtedy, gdy dane hello hello podstawowej obiektów blob i migawki hello pozostać identyczne.</span><span class="sxs-lookup"><span data-stu-id="2e058-173">This is true even if hello data in hello base blob and hello snapshot remain identical.</span></span>
* <span data-ttu-id="2e058-174">Hello usługi obiektów Blob platformy Azure nie ma toodetermine oznacza, czy dwa bloki zawierają identyczne dane.</span><span class="sxs-lookup"><span data-stu-id="2e058-174">hello Azure Blob service does not have a means toodetermine whether two blocks contain identical data.</span></span> <span data-ttu-id="2e058-175">Każdy blok przekazane i zatwierdzone jest traktowany jako unikatowy, nawet wtedy, gdy ma ona hello tych samych danych i hello zablokować sam identyfikator.</span><span class="sxs-lookup"><span data-stu-id="2e058-175">Each block that is uploaded and committed is treated as unique, even if it has hello same data and hello same block ID.</span></span> <span data-ttu-id="2e058-176">Ponieważ Naliczanie opłat dla bloków unikatowe, jest ważne tooconsider, który aktualizowania obiektów blob, który ma migawkę powoduje dodatkowe bloki unikatowy i dodatkowych opłat.</span><span class="sxs-lookup"><span data-stu-id="2e058-176">Because charges accrue for unique blocks, it's important tooconsider that updating a blob that has a snapshot results in additional unique blocks and additional charges.</span></span>

### <a name="minimize-cost-with-snapshot-management"></a><span data-ttu-id="2e058-177">Minimalizuje koszt z zarządzania migawkami</span><span class="sxs-lookup"><span data-stu-id="2e058-177">Minimize cost with snapshot management</span></span>

<span data-ttu-id="2e058-178">Zaleca się zarządzanie z migawki dokładnie tooavoid dodatkowych opłat.</span><span class="sxs-lookup"><span data-stu-id="2e058-178">We recommend managing your snapshots carefully tooavoid extra charges.</span></span> <span data-ttu-id="2e058-179">Możesz wykonać następujące najlepsze rozwiązania toohelp zminimalizować hello kosztów ponoszonych przez hello magazynu migawek sieci:</span><span class="sxs-lookup"><span data-stu-id="2e058-179">You can follow these best practices toohelp minimize hello costs incurred by hello storage of your snapshots:</span></span>

* <span data-ttu-id="2e058-180">Usunięcie i ponowne utworzenie migawki skojarzone z obiektu blob po zaktualizowaniu hello obiektów blob, nawet jeśli aktualizujesz mają identyczne dane, chyba że projektu aplikacji wymaga, aby zachować migawki.</span><span class="sxs-lookup"><span data-stu-id="2e058-180">Delete and re-create snapshots associated with a blob whenever you update hello blob, even if you are updating with identical data, unless your application design requires that you maintain snapshots.</span></span> <span data-ttu-id="2e058-181">Przez usunięcie i ponowne utworzenie migawki obiektu blob hello, możesz upewnij się, że hello obiektów blob i migawek nie odbiegają.</span><span class="sxs-lookup"><span data-stu-id="2e058-181">By deleting and re-creating hello blob's snapshots, you can ensure that hello blob and snapshots do not diverge.</span></span>
* <span data-ttu-id="2e058-182">Jeśli obsługujesz migawek dla obiekt blob, należy unikać wywoływania [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [ UploadFromStream][dotnet_UploadFromStream], lub [UploadFromByteArray] [ dotnet_UploadFromByteArray] tooupdate hello blob.</span><span class="sxs-lookup"><span data-stu-id="2e058-182">If you are maintaining snapshots for a blob, avoid calling [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray] tooupdate hello blob.</span></span> <span data-ttu-id="2e058-183">Te metody Zamień wszystkie bloki hello w obiekcie blob hello, znacznie powoduje sieci podstawowej obiektów blob i jego toodiverge migawki.</span><span class="sxs-lookup"><span data-stu-id="2e058-183">These methods replace all of hello blocks in hello blob, causing your base blob and its snapshots toodiverge significantly.</span></span> <span data-ttu-id="2e058-184">Zamiast tego aktualizacji hello najmniejszą możliwą liczbę bloków przy użyciu hello [PutBlock] [ dotnet_PutBlock] i [metoda PutBlockList] [ dotnet_PutBlockList] metody.</span><span class="sxs-lookup"><span data-stu-id="2e058-184">Instead, update hello fewest possible number of blocks by using hello [PutBlock][dotnet_PutBlock] and [PutBlockList][dotnet_PutBlockList] methods.</span></span>

### <a name="snapshot-billing-scenarios"></a><span data-ttu-id="2e058-185">Migawki rozliczeń scenariuszy</span><span class="sxs-lookup"><span data-stu-id="2e058-185">Snapshot billing scenarios</span></span>
<span data-ttu-id="2e058-186">następujące scenariusze Hello pokazują, jak Naliczanie opłat dla blokowych obiektów blob i jego migawek.</span><span class="sxs-lookup"><span data-stu-id="2e058-186">hello following scenarios demonstrate how charges accrue for a block blob and its snapshots.</span></span>

<span data-ttu-id="2e058-187">**Scenariusz 1**</span><span class="sxs-lookup"><span data-stu-id="2e058-187">**Scenario 1**</span></span>

<span data-ttu-id="2e058-188">W scenariuszu 1 hello podstawowego obiektu blob nie został zaktualizowany po hello migawki, więc jest obciążany tylko dla bloków unikatowy 1, 2 i 3.</span><span class="sxs-lookup"><span data-stu-id="2e058-188">In scenario 1, hello base blob has not been updated after hello snapshot was taken, so charges are incurred only for unique blocks 1, 2, and 3.</span></span>

![Zasoby usługi Azure Storage](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-1.png)

<span data-ttu-id="2e058-190">**Scenariusz 2**</span><span class="sxs-lookup"><span data-stu-id="2e058-190">**Scenario 2**</span></span>

<span data-ttu-id="2e058-191">W scenariuszu 2 podstawowego obiektu blob hello zostały zaktualizowane, ale hello migawka nie ma.</span><span class="sxs-lookup"><span data-stu-id="2e058-191">In scenario 2, hello base blob has been updated, but hello snapshot has not.</span></span> <span data-ttu-id="2e058-192">Blok 3 został zaktualizowany, a nawet, jeśli zawiera ona hello tych samych danych i hello na tym samym identyfikatorze, jest taki sam, jak zablokować 3 w migawce hello nie hello.</span><span class="sxs-lookup"><span data-stu-id="2e058-192">Block 3 was updated, and even though it contains hello same data and hello same ID, it is not hello same as block 3 in hello snapshot.</span></span> <span data-ttu-id="2e058-193">W związku z tym kontem hello jest pobierana cztery bloków.</span><span class="sxs-lookup"><span data-stu-id="2e058-193">As a result, hello account is charged for four blocks.</span></span>

![Zasoby usługi Azure Storage](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-2.png)

<span data-ttu-id="2e058-195">**Scenariusz 3**</span><span class="sxs-lookup"><span data-stu-id="2e058-195">**Scenario 3**</span></span>

<span data-ttu-id="2e058-196">W scenariuszu 3 podstawowego obiektu blob hello zostały zaktualizowane, ale hello migawka nie ma.</span><span class="sxs-lookup"><span data-stu-id="2e058-196">In scenario 3, hello base blob has been updated, but hello snapshot has not.</span></span> <span data-ttu-id="2e058-197">3 blokowych zamieniono bloku 4 w obiekcie blob podstawowej hello, ale migawki hello nadal odzwierciedla blok 3.</span><span class="sxs-lookup"><span data-stu-id="2e058-197">Block 3 was replaced with block 4 in hello base blob, but hello snapshot still reflects block 3.</span></span> <span data-ttu-id="2e058-198">W związku z tym kontem hello jest pobierana cztery bloków.</span><span class="sxs-lookup"><span data-stu-id="2e058-198">As a result, hello account is charged for four blocks.</span></span>

![Zasoby usługi Azure Storage](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-3.png)

<span data-ttu-id="2e058-200">**Scenariusz 4**</span><span class="sxs-lookup"><span data-stu-id="2e058-200">**Scenario 4**</span></span>

<span data-ttu-id="2e058-201">W scenariuszu 4 hello podstawowego obiektu blob została całkowicie zaktualizowana i zawiera żaden z jego oryginalnych bloków.</span><span class="sxs-lookup"><span data-stu-id="2e058-201">In scenario 4, hello base blob has been completely updated and contains none of its original blocks.</span></span> <span data-ttu-id="2e058-202">W związku z tym rozliczany hello konta dla wszystkich osiem bloków unikatowy.</span><span class="sxs-lookup"><span data-stu-id="2e058-202">As a result, hello account is charged for all eight unique blocks.</span></span> <span data-ttu-id="2e058-203">Ten scenariusz może wystąpić, jeśli używasz metody aktualizacji takich jak [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [ UploadFromStream][dotnet_UploadFromStream], lub [UploadFromByteArray][dotnet_UploadFromByteArray], ponieważ metody te Zastąp całą zawartość hello obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="2e058-203">This scenario can occur if you are using an update method such as [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray], because these methods replace all of hello contents of a blob.</span></span>

![Zasoby usługi Azure Storage](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-4.png)

## <a name="next-steps"></a><span data-ttu-id="2e058-205">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2e058-205">Next steps</span></span>

* <span data-ttu-id="2e058-206">Można znaleźć więcej informacji na temat pracy z migawek dysków maszyny wirtualnej (VM) w [kopia zapasowa Azure niezarządzane dysków maszyny Wirtualnej z migawkami przyrostowe](../../virtual-machines/windows/incremental-snapshots.md)</span><span class="sxs-lookup"><span data-stu-id="2e058-206">You can find more information about working with virtual machine (VM) disk snapshots in [Back up Azure unmanaged VM disks with incremental snapshots](../../virtual-machines/windows/incremental-snapshots.md)</span></span>

* <span data-ttu-id="2e058-207">Dla dodatkowych przykładów kodu przy użyciu magazynu obiektów Blob, zobacz [przykłady kodu Azure](https://azure.microsoft.com/documentation/samples/?service=storage&term=blob).</span><span class="sxs-lookup"><span data-stu-id="2e058-207">For additional code examples using Blob storage, see [Azure Code Samples](https://azure.microsoft.com/documentation/samples/?service=storage&term=blob).</span></span> <span data-ttu-id="2e058-208">Można pobrać przykładową aplikację i uruchom go lub Przeglądaj hello kodu w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="2e058-208">You can download a sample application and run it, or browse hello code on GitHub.</span></span>

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