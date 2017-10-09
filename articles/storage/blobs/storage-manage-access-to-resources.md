---
title: "aaaEnable publiczny dostęp do odczytu do kontenerów i obiektów blob w magazynie obiektów Blob platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomake kontenerów i obiektów blob jest dostępna dla dostępu anonimowego i w jaki sposób tooaccess je programowo."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: a2cffee6-3224-4f2a-8183-66ca23b2d2d7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: marsma
ms.openlocfilehash: dd8ffdb39a66aa06f65ad3cdd4315d47c117f059
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-anonymous-read-access-toocontainers-and-blobs"></a><span data-ttu-id="846ce-103">Zarządzanie toocontainers anonimowy dostęp do odczytu i obiektów blob</span><span class="sxs-lookup"><span data-stu-id="846ce-103">Manage anonymous read access toocontainers and blobs</span></span>
<span data-ttu-id="846ce-104">Można włączyć anonimowego, publiczny dostęp do odczytu tooa kontenera i jego obiektów blob w magazynie obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="846ce-104">You can enable anonymous, public read access tooa container and its blobs in Azure Blob storage.</span></span> <span data-ttu-id="846ce-105">W ten sposób można przyznać dostęp tylko do odczytu zasobów toothese bez udostępniania swój klucz konta usługi i bez konieczności sygnatury dostępu współdzielonego (SAS).</span><span class="sxs-lookup"><span data-stu-id="846ce-105">By doing so, you can grant read-only access toothese resources without sharing your account key, and without requiring a shared access signature (SAS).</span></span>

<span data-ttu-id="846ce-106">Najlepiej w scenariuszach, w miejsce niektórych obiektów blob tooalways można anonimowy dostęp do odczytu jest publiczny dostęp do odczytu.</span><span class="sxs-lookup"><span data-stu-id="846ce-106">Public read access is best for scenarios where you want certain blobs tooalways be available for anonymous read access.</span></span> <span data-ttu-id="846ce-107">Aby uzyskać bardziej precyzyjną kontrolę można utworzyć sygnatury dostępu współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="846ce-107">For more fine-grained control, you can create a shared access signature.</span></span> <span data-ttu-id="846ce-108">Sygnatury dostępu współdzielonego umożliwiają tooprovide ograniczony dostęp przy użyciu różnych uprawnień w określonym przedziale czasu.</span><span class="sxs-lookup"><span data-stu-id="846ce-108">Shared access signatures enable you tooprovide restricted access using different permissions, for a specific time period.</span></span> <span data-ttu-id="846ce-109">Aby uzyskać więcej informacji o tworzeniu udostępnionych sygnatur dostępu, zobacz [używanie udostępnionych sygnatur dostępu (SAS) w usłudze Azure Storage](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="846ce-109">For more information about creating shared access signatures, see [Using shared access signatures (SAS) in Azure Storage](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span>

## <a name="grant-anonymous-users-permissions-toocontainers-and-blobs"></a><span data-ttu-id="846ce-110">Udziel toocontainers uprawnień użytkowników anonimowych, jak i obiektów blob</span><span class="sxs-lookup"><span data-stu-id="846ce-110">Grant anonymous users permissions toocontainers and blobs</span></span>
<span data-ttu-id="846ce-111">Domyślnie kontener i wszystkie obiekty BLOB w nim mogą być używane tylko przez właściciela hello hello konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="846ce-111">By default, a container and any blobs within it may be accessed only by hello owner of hello storage account.</span></span> <span data-ttu-id="846ce-112">toogive anonimowym użytkownikom uprawnienia do odczytu tooa kontenera i jego obiektów blob, można ustawić dostępu publicznego tooallow hello kontenera uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="846ce-112">toogive anonymous users read permissions tooa container and its blobs, you can set hello container permissions tooallow public access.</span></span> <span data-ttu-id="846ce-113">Użytkownicy anonimowi mogą odczytywać obiekty BLOB w kontenerze publicznie bez uwierzytelniania hello żądania.</span><span class="sxs-lookup"><span data-stu-id="846ce-113">Anonymous users can read blobs within a publicly accessible container without authenticating hello request.</span></span>

<span data-ttu-id="846ce-114">Można skonfigurować kontener hello następujących uprawnień:</span><span class="sxs-lookup"><span data-stu-id="846ce-114">You can configure a container with hello following permissions:</span></span>

* <span data-ttu-id="846ce-115">**Dostęp do odczytu żadnego elementu publicznego public:** hello kontenera i jego obiektów blob są dostępne tylko przez właściciela konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="846ce-115">**No public read access:** hello container and its blobs can be accessed only by hello storage account owner.</span></span> <span data-ttu-id="846ce-116">Jest to domyślna powitania dla wszystkich nowych kontenerów.</span><span class="sxs-lookup"><span data-stu-id="846ce-116">This is hello default for all new containers.</span></span>
* <span data-ttu-id="846ce-117">**Dostęp do obiektów blob tylko odczytu publicznego:** obiekty BLOB w kontenerze hello może zostać odczytany przez żądania od użytkowników anonimowych, ale nie są dostępne dane kontenera.</span><span class="sxs-lookup"><span data-stu-id="846ce-117">**Public read access for blobs only:** Blobs within hello container can be read by anonymous request, but container data is not available.</span></span> <span data-ttu-id="846ce-118">Anonimowe klientów nie można wyliczyć obiektów blob hello w kontenerze hello.</span><span class="sxs-lookup"><span data-stu-id="846ce-118">Anonymous clients cannot enumerate hello blobs within hello container.</span></span>
* <span data-ttu-id="846ce-119">**Pełne publiczny dostęp do odczytu:** wszystkie dane obiektów blob i kontener może zostać odczytany przez żądania od użytkowników anonimowych.</span><span class="sxs-lookup"><span data-stu-id="846ce-119">**Full public read access:** All container and blob data can be read by anonymous request.</span></span> <span data-ttu-id="846ce-120">Klientów można wyliczyć obiektów blob w kontenerze hello przez żądania od użytkowników anonimowych, ale nie można wyliczyć kontenery w ramach konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="846ce-120">Clients can enumerate blobs within hello container by anonymous request, but cannot enumerate containers within hello storage account.</span></span>

<span data-ttu-id="846ce-121">Można użyć następujących uprawnień kontenera tooset hello:</span><span class="sxs-lookup"><span data-stu-id="846ce-121">You can use hello following tooset container permissions:</span></span>

* [<span data-ttu-id="846ce-122">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="846ce-122">Azure portal</span></span>](https://portal.azure.com)
* [<span data-ttu-id="846ce-123">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="846ce-123">Azure PowerShell</span></span>](../common/storage-powershell-guide-full.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#how-to-manage-azure-blobs)
* [<span data-ttu-id="846ce-124">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="846ce-124">Azure CLI 2.0</span></span>](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#create-and-manage-blobs)
* <span data-ttu-id="846ce-125">Programowo za pomocą jednej z bibliotek klienckich magazynu hello lub hello interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="846ce-125">Programmatically, by using one of hello storage client libraries or hello REST API</span></span>

### <a name="set-container-permissions-in-hello-azure-portal"></a><span data-ttu-id="846ce-126">Ustaw uprawnienia kontenera w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="846ce-126">Set container permissions in hello Azure portal</span></span>
<span data-ttu-id="846ce-127">tooset uprawnień kontenera w hello [portalu Azure](https://portal.azure.com), wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="846ce-127">tooset container permissions in hello [Azure portal](https://portal.azure.com), follow these steps:</span></span>

1. <span data-ttu-id="846ce-128">Otwórz z **konta magazynu** bloku w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="846ce-128">Open your **Storage account** blade in hello portal.</span></span> <span data-ttu-id="846ce-129">Można znaleźć konta magazynu, wybierając **kont magazynu** w bloku portalu menu głównego hello.</span><span class="sxs-lookup"><span data-stu-id="846ce-129">You can find your storage account by selecting **Storage accounts** in hello main portal menu blade.</span></span>
1. <span data-ttu-id="846ce-130">W obszarze **usługa BLOB** na powitania bloku menu, wybierz **kontenery**.</span><span class="sxs-lookup"><span data-stu-id="846ce-130">Under **BLOB SERVICE** on hello menu blade, select **Containers**.</span></span>
1. <span data-ttu-id="846ce-131">Kliknij prawym przyciskiem myszy na wiersz kontenera hello lub wybierz hello wielokropka tooopen hello kontenera **menu kontekstowe**.</span><span class="sxs-lookup"><span data-stu-id="846ce-131">Right-click on hello container row or select hello ellipsis tooopen hello container's **Context menu**.</span></span>
1. <span data-ttu-id="846ce-132">Wybierz **zasady dostępu** w menu kontekstowym hello.</span><span class="sxs-lookup"><span data-stu-id="846ce-132">Select **Access policy** in hello context menu.</span></span>
1. <span data-ttu-id="846ce-133">Wybierz **dostęp typu** z hello menu rozwijanym.</span><span class="sxs-lookup"><span data-stu-id="846ce-133">Select an **Access type** from hello drop down menu.</span></span>

    ![Okno dialogowe metadanych kontenera Edycja](./media/storage-manage-access-to-resources/storage-manage-access-to-resources-0.png)

### <a name="set-container-permissions-with-net"></a><span data-ttu-id="846ce-135">Ustawianie uprawnień kontenera z platformą .NET</span><span class="sxs-lookup"><span data-stu-id="846ce-135">Set container permissions with .NET</span></span>
<span data-ttu-id="846ce-136">tooset uprawnienia do kontenera przy użyciu języka C# i hello biblioteki klienta usługi Storage dla platformy .NET, najpierw pobrać kontenera hello istniejące uprawnienia przez wywołanie hello **GetPermissions** metody.</span><span class="sxs-lookup"><span data-stu-id="846ce-136">tooset permissions for a container using C# and hello Storage Client Library for .NET, first retrieve hello container's existing permissions by calling hello **GetPermissions** method.</span></span> <span data-ttu-id="846ce-137">Następnie zestaw hello **PublicAccess** właściwość hello **BlobContainerPermissions** obiektu, który jest zwracany przez hello **GetPermissions** metody.</span><span class="sxs-lookup"><span data-stu-id="846ce-137">Then set hello **PublicAccess** property for hello **BlobContainerPermissions** object that is returned by hello **GetPermissions** method.</span></span> <span data-ttu-id="846ce-138">Na koniec wywołania hello **ustawiania** metody z hello zaktualizowano uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="846ce-138">Finally, call hello **SetPermissions** method with hello updated permissions.</span></span>

<span data-ttu-id="846ce-139">Poniższy przykład Hello ustawia uprawnienia kontenera hello toofull publiczny dostęp do odczytu.</span><span class="sxs-lookup"><span data-stu-id="846ce-139">hello following example sets hello container's permissions toofull public read access.</span></span> <span data-ttu-id="846ce-140">dostęp do odczytu tooset toopublic uprawnienia dla obiektów blob, należy ustawić hello **PublicAccess** właściwości zbyt**BlobContainerPublicAccessType.Blob**.</span><span class="sxs-lookup"><span data-stu-id="846ce-140">tooset permissions toopublic read access for blobs only, set hello **PublicAccess** property too**BlobContainerPublicAccessType.Blob**.</span></span> <span data-ttu-id="846ce-141">Ustaw wszystkie uprawnienia dla użytkowników anonimowych tooremove zbyt hello właściwości**BlobContainerPublicAccessType.Off**.</span><span class="sxs-lookup"><span data-stu-id="846ce-141">tooremove all permissions for anonymous users, set hello property too**BlobContainerPublicAccessType.Off**.</span></span>

```csharp
public static void SetPublicContainerPermissions(CloudBlobContainer container)
{
    BlobContainerPermissions permissions = container.GetPermissions();
    permissions.PublicAccess = BlobContainerPublicAccessType.Container;
    container.SetPermissions(permissions);
}
```

## <a name="access-containers-and-blobs-anonymously"></a><span data-ttu-id="846ce-142">Dostęp do kontenerów i obiektów blob anonimowo</span><span class="sxs-lookup"><span data-stu-id="846ce-142">Access containers and blobs anonymously</span></span>
<span data-ttu-id="846ce-143">Klient, który uzyskuje dostęp do kontenerów i obiektów blob anonimowo można użyć konstruktorów, które nie wymagają poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="846ce-143">A client that accesses containers and blobs anonymously can use constructors that do not require credentials.</span></span> <span data-ttu-id="846ce-144">Następujące przykłady Hello Pokaż na kilka różnych sposobów zasoby usługi Blob tooreference anonimowo.</span><span class="sxs-lookup"><span data-stu-id="846ce-144">hello following examples show a few different ways tooreference Blob service resources anonymously.</span></span>

### <a name="create-an-anonymous-client-object"></a><span data-ttu-id="846ce-145">Tworzenie obiektu anonimowego klienta</span><span class="sxs-lookup"><span data-stu-id="846ce-145">Create an anonymous client object</span></span>
<span data-ttu-id="846ce-146">Można utworzyć nowy obiekt klienta usługi dla dostępu anonimowego, podając punkt końcowy usługi Blob hello hello konta.</span><span class="sxs-lookup"><span data-stu-id="846ce-146">You can create a new service client object for anonymous access by providing hello Blob service endpoint for hello account.</span></span> <span data-ttu-id="846ce-147">Należy jednak znać nazwę hello kontenera na tym koncie, który jest dostępny dla dostępu anonimowego.</span><span class="sxs-lookup"><span data-stu-id="846ce-147">However, you must also know hello name of a container in that account that's available for anonymous access.</span></span>

```csharp
public static void CreateAnonymousBlobClient()
{
    // Create hello client object using hello Blob service endpoint.
    CloudBlobClient blobClient = new CloudBlobClient(new Uri(@"https://storagesample.blob.core.windows.net"));

    // Get a reference tooa container that's available for anonymous access.
    CloudBlobContainer container = blobClient.GetContainerReference("sample-container");

    // Read hello container's properties. Note this is only possible when hello container supports full public read access.
    container.FetchAttributes();
    Console.WriteLine(container.Properties.LastModified);
    Console.WriteLine(container.Properties.ETag);
}
```

### <a name="reference-a-container-anonymously"></a><span data-ttu-id="846ce-148">Odwołanie kontenera anonimowego</span><span class="sxs-lookup"><span data-stu-id="846ce-148">Reference a container anonymously</span></span>
<span data-ttu-id="846ce-149">Jeśli masz hello adres URL tooa kontener, który jest dostępny anonimowo umożliwia kontenera hello tooreference bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="846ce-149">If you have hello URL tooa container that is anonymously available, you can use it tooreference hello container directly.</span></span>

```csharp
public static void ListBlobsAnonymously()
{
    // Get a reference tooa container that's available for anonymous access.
    CloudBlobContainer container = new CloudBlobContainer(new Uri(@"https://storagesample.blob.core.windows.net/sample-container"));

    // List blobs in hello container.
    foreach (IListBlobItem blobItem in container.ListBlobs())
    {
        Console.WriteLine(blobItem.Uri);
    }
}
```

### <a name="reference-a-blob-anonymously"></a><span data-ttu-id="846ce-150">Odwołanie obiektu blob anonimowo</span><span class="sxs-lookup"><span data-stu-id="846ce-150">Reference a blob anonymously</span></span>
<span data-ttu-id="846ce-151">Jeśli masz hello adresu URL tooa blob, który jest dostępny dla dostępu anonimowego, możesz odwoływać się do obiektu blob hello bezpośrednio przy użyciu tego adresu URL:</span><span class="sxs-lookup"><span data-stu-id="846ce-151">If you have hello URL tooa blob that is available for anonymous access, you can reference hello blob directly using that URL:</span></span>

```csharp
public static void DownloadBlobAnonymously()
{
    CloudBlockBlob blob = new CloudBlockBlob(new Uri(@"https://storagesample.blob.core.windows.net/sample-container/logfile.txt"));
    blob.DownloadToFile(@"C:\Temp\logfile.txt", System.IO.FileMode.Create);
}
```

## <a name="features-available-tooanonymous-users"></a><span data-ttu-id="846ce-152">Funkcje dostępne tooanonymous użytkowników</span><span class="sxs-lookup"><span data-stu-id="846ce-152">Features available tooanonymous users</span></span>
<span data-ttu-id="846ce-153">Witaj w poniższej tabeli przedstawiono operacje może zostać wywołana przez anonimowych użytkowników, gdy ACL kontenera ustawiono tooallow dostępu publicznego.</span><span class="sxs-lookup"><span data-stu-id="846ce-153">hello following table shows which operations may be called by anonymous users when a container's ACL is set tooallow public access.</span></span>

| <span data-ttu-id="846ce-154">Operacji REST</span><span class="sxs-lookup"><span data-stu-id="846ce-154">REST Operation</span></span> | <span data-ttu-id="846ce-155">Uprawnienie o pełnej publiczny dostęp do odczytu</span><span class="sxs-lookup"><span data-stu-id="846ce-155">Permission with full public read access</span></span> | <span data-ttu-id="846ce-156">Uprawnienie o publiczny dostęp do odczytu obiektów blob tylko</span><span class="sxs-lookup"><span data-stu-id="846ce-156">Permission with public read access for blobs only</span></span> |
| --- | --- | --- |
| <span data-ttu-id="846ce-157">Kontenery listy</span><span class="sxs-lookup"><span data-stu-id="846ce-157">List Containers</span></span> |<span data-ttu-id="846ce-158">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="846ce-158">Owner only</span></span> |<span data-ttu-id="846ce-159">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="846ce-159">Owner only</span></span> |
| <span data-ttu-id="846ce-160">Tworzenie kontenera</span><span class="sxs-lookup"><span data-stu-id="846ce-160">Create Container</span></span> |<span data-ttu-id="846ce-161">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="846ce-161">Owner only</span></span> |<span data-ttu-id="846ce-162">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="846ce-162">Owner only</span></span> |
| <span data-ttu-id="846ce-163">Pobierz właściwości kontenera</span><span class="sxs-lookup"><span data-stu-id="846ce-163">Get Container Properties</span></span> |<span data-ttu-id="846ce-164">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="846ce-164">All</span></span> |<span data-ttu-id="846ce-165">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="846ce-165">Owner only</span></span> |
| <span data-ttu-id="846ce-166">Pobranie metadanych kontenera</span><span class="sxs-lookup"><span data-stu-id="846ce-166">Get Container Metadata</span></span> |<span data-ttu-id="846ce-167">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="846ce-167">All</span></span> |<span data-ttu-id="846ce-168">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="846ce-168">Owner only</span></span> |
| <span data-ttu-id="846ce-169">Ustaw metadanych kontenera</span><span class="sxs-lookup"><span data-stu-id="846ce-169">Set Container Metadata</span></span> |<span data-ttu-id="846ce-170">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="846ce-170">Owner only</span></span> |<span data-ttu-id="846ce-171">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="846ce-171">Owner only</span></span> |
| <span data-ttu-id="846ce-172">Pobierz ACL kontenera</span><span class="sxs-lookup"><span data-stu-id="846ce-172">Get Container ACL</span></span> |<span data-ttu-id="846ce-173">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="846ce-173">Owner only</span></span> |<span data-ttu-id="846ce-174">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="846ce-174">Owner only</span></span> |
| <span data-ttu-id="846ce-175">Ustaw ACL kontenera</span><span class="sxs-lookup"><span data-stu-id="846ce-175">Set Container ACL</span></span> |<span data-ttu-id="846ce-176">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="846ce-176">Owner only</span></span> |<span data-ttu-id="846ce-177">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="846ce-177">Owner only</span></span> |
| <span data-ttu-id="846ce-178">Usunąć kontenera</span><span class="sxs-lookup"><span data-stu-id="846ce-178">Delete Container</span></span> |<span data-ttu-id="846ce-179">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="846ce-179">Owner only</span></span> |<span data-ttu-id="846ce-180">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="846ce-180">Owner only</span></span> |
| <span data-ttu-id="846ce-181">Lista obiektów blob</span><span class="sxs-lookup"><span data-stu-id="846ce-181">List Blobs</span></span> |<span data-ttu-id="846ce-182">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="846ce-182">All</span></span> |<span data-ttu-id="846ce-183">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="846ce-183">Owner only</span></span> |
| <span data-ttu-id="846ce-184">Umieszczanie obiektu Blob</span><span class="sxs-lookup"><span data-stu-id="846ce-184">Put Blob</span></span> |<span data-ttu-id="846ce-185">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="846ce-185">Owner only</span></span> |<span data-ttu-id="846ce-186">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="846ce-186">Owner only</span></span> |
| <span data-ttu-id="846ce-187">Pobierz obiekt Blob</span><span class="sxs-lookup"><span data-stu-id="846ce-187">Get Blob</span></span> |<span data-ttu-id="846ce-188">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="846ce-188">All</span></span> |<span data-ttu-id="846ce-189">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="846ce-189">All</span></span> |
| <span data-ttu-id="846ce-190">Pobierz właściwości obiektu Blob</span><span class="sxs-lookup"><span data-stu-id="846ce-190">Get Blob Properties</span></span> |<span data-ttu-id="846ce-191">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="846ce-191">All</span></span> |<span data-ttu-id="846ce-192">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="846ce-192">All</span></span> |
| <span data-ttu-id="846ce-193">Ustaw właściwości obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="846ce-193">Set Blob Properties</span></span> |<span data-ttu-id="846ce-194">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="846ce-194">Owner only</span></span> |<span data-ttu-id="846ce-195">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="846ce-195">Owner only</span></span> |
| <span data-ttu-id="846ce-196">Pobierz metadane obiektu Blob</span><span class="sxs-lookup"><span data-stu-id="846ce-196">Get Blob Metadata</span></span> |<span data-ttu-id="846ce-197">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="846ce-197">All</span></span> |<span data-ttu-id="846ce-198">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="846ce-198">All</span></span> |
| <span data-ttu-id="846ce-199">Ustaw metadane obiektu Blob</span><span class="sxs-lookup"><span data-stu-id="846ce-199">Set Blob Metadata</span></span> |<span data-ttu-id="846ce-200">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="846ce-200">Owner only</span></span> |<span data-ttu-id="846ce-201">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="846ce-201">Owner only</span></span> |
| <span data-ttu-id="846ce-202">Umieść bloku</span><span class="sxs-lookup"><span data-stu-id="846ce-202">Put Block</span></span> |<span data-ttu-id="846ce-203">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="846ce-203">Owner only</span></span> |<span data-ttu-id="846ce-204">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="846ce-204">Owner only</span></span> |
| <span data-ttu-id="846ce-205">Pobierz listę zablokowanych (tylko zatwierdzone bloki)</span><span class="sxs-lookup"><span data-stu-id="846ce-205">Get Block List (committed blocks only)</span></span> |<span data-ttu-id="846ce-206">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="846ce-206">All</span></span> |<span data-ttu-id="846ce-207">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="846ce-207">All</span></span> |
| <span data-ttu-id="846ce-208">Pobierz listę bloku (tylko niezatwierdzone bloków lub wszystkie bloki)</span><span class="sxs-lookup"><span data-stu-id="846ce-208">Get Block List (uncommitted blocks only or all blocks)</span></span> |<span data-ttu-id="846ce-209">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="846ce-209">Owner only</span></span> |<span data-ttu-id="846ce-210">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="846ce-210">Owner only</span></span> |
| <span data-ttu-id="846ce-211">Umieść zablokowanych</span><span class="sxs-lookup"><span data-stu-id="846ce-211">Put Block List</span></span> |<span data-ttu-id="846ce-212">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="846ce-212">Owner only</span></span> |<span data-ttu-id="846ce-213">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="846ce-213">Owner only</span></span> |
| <span data-ttu-id="846ce-214">Usuwanie obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="846ce-214">Delete Blob</span></span> |<span data-ttu-id="846ce-215">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="846ce-215">Owner only</span></span> |<span data-ttu-id="846ce-216">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="846ce-216">Owner only</span></span> |
| <span data-ttu-id="846ce-217">Kopiowanie obiektu Blob</span><span class="sxs-lookup"><span data-stu-id="846ce-217">Copy Blob</span></span> |<span data-ttu-id="846ce-218">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="846ce-218">Owner only</span></span> |<span data-ttu-id="846ce-219">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="846ce-219">Owner only</span></span> |
| <span data-ttu-id="846ce-220">Migawki obiektu Blob</span><span class="sxs-lookup"><span data-stu-id="846ce-220">Snapshot Blob</span></span> |<span data-ttu-id="846ce-221">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="846ce-221">Owner only</span></span> |<span data-ttu-id="846ce-222">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="846ce-222">Owner only</span></span> |
| <span data-ttu-id="846ce-223">Obiekt Blob dzierżawy</span><span class="sxs-lookup"><span data-stu-id="846ce-223">Lease Blob</span></span> |<span data-ttu-id="846ce-224">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="846ce-224">Owner only</span></span> |<span data-ttu-id="846ce-225">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="846ce-225">Owner only</span></span> |
| <span data-ttu-id="846ce-226">Umieść stronę</span><span class="sxs-lookup"><span data-stu-id="846ce-226">Put Page</span></span> |<span data-ttu-id="846ce-227">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="846ce-227">Owner only</span></span> |<span data-ttu-id="846ce-228">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="846ce-228">Owner only</span></span> |
| <span data-ttu-id="846ce-229">Get zakresów stron</span><span class="sxs-lookup"><span data-stu-id="846ce-229">Get Page Ranges</span></span> |<span data-ttu-id="846ce-230">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="846ce-230">All</span></span> |<span data-ttu-id="846ce-231">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="846ce-231">All</span></span> |
| <span data-ttu-id="846ce-232">Dołącz obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="846ce-232">Append Blob</span></span> |<span data-ttu-id="846ce-233">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="846ce-233">Owner only</span></span> |<span data-ttu-id="846ce-234">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="846ce-234">Owner only</span></span> |

## <a name="next-steps"></a><span data-ttu-id="846ce-235">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="846ce-235">Next steps</span></span>

* [<span data-ttu-id="846ce-236">Uwierzytelnianie dla hello usług magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="846ce-236">Authentication for hello Azure Storage Services</span></span>](https://msdn.microsoft.com/library/azure/dd179428.aspx)
* [<span data-ttu-id="846ce-237">Przy użyciu sygnatury dostępu współdzielonego (SAS)</span><span class="sxs-lookup"><span data-stu-id="846ce-237">Using Shared Access Signatures (SAS)</span></span>](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [<span data-ttu-id="846ce-238">Delegowanie dostępu za pomocą sygnatury dostępu współdzielonego</span><span class="sxs-lookup"><span data-stu-id="846ce-238">Delegating Access with a Shared Access Signature</span></span>](https://msdn.microsoft.com/library/azure/ee395415.aspx)
