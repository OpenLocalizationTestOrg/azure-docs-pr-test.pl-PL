---
title: "Włącz publiczny dostęp do odczytu do kontenerów i obiektów blob w magazynie obiektów Blob platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak udostępnić kontenerów i obiektów blob dla dostępu anonimowego i sposób programowy dostęp."
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
ms.openlocfilehash: 8d4f4c7c208baf0db6155eb78a53e37c4ec1e023
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="manage-anonymous-read-access-to-containers-and-blobs"></a><span data-ttu-id="e0eb3-103">Zarządzanie dostępem anonimowym w trybie odczytu do kontenerów i obiektów blob</span><span class="sxs-lookup"><span data-stu-id="e0eb3-103">Manage anonymous read access to containers and blobs</span></span>
<span data-ttu-id="e0eb3-104">Można włączyć anonimowego, publiczny dostęp do odczytu do kontenera i jego obiektów blob w magazynie obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="e0eb3-104">You can enable anonymous, public read access to a container and its blobs in Azure Blob storage.</span></span> <span data-ttu-id="e0eb3-105">W ten sposób można przyznać dostęp tylko do odczytu do tych zasobów, bez udostępniania swój klucz konta usługi i bez konieczności sygnatury dostępu współdzielonego (SAS).</span><span class="sxs-lookup"><span data-stu-id="e0eb3-105">By doing so, you can grant read-only access to these resources without sharing your account key, and without requiring a shared access signature (SAS).</span></span>

<span data-ttu-id="e0eb3-106">Najlepiej w scenariuszach, w którym ma niektórych obiektów blob zawsze być dostępna dla anonimowy dostęp do odczytu jest publiczny dostęp do odczytu.</span><span class="sxs-lookup"><span data-stu-id="e0eb3-106">Public read access is best for scenarios where you want certain blobs to always be available for anonymous read access.</span></span> <span data-ttu-id="e0eb3-107">Aby uzyskać bardziej precyzyjną kontrolę można utworzyć sygnatury dostępu współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="e0eb3-107">For more fine-grained control, you can create a shared access signature.</span></span> <span data-ttu-id="e0eb3-108">Sygnatury dostępu współdzielonego umożliwiają stosowanie ograniczony dostęp przy użyciu różnych uprawnień w określonym przedziale czasu.</span><span class="sxs-lookup"><span data-stu-id="e0eb3-108">Shared access signatures enable you to provide restricted access using different permissions, for a specific time period.</span></span> <span data-ttu-id="e0eb3-109">Aby uzyskać więcej informacji o tworzeniu udostępnionych sygnatur dostępu, zobacz [używanie udostępnionych sygnatur dostępu (SAS) w usłudze Azure Storage](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e0eb3-109">For more information about creating shared access signatures, see [Using shared access signatures (SAS) in Azure Storage](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span>

## <a name="grant-anonymous-users-permissions-to-containers-and-blobs"></a><span data-ttu-id="e0eb3-110">Udzielanie uprawnień użytkownikom anonimowym do kontenerów i obiektów blob</span><span class="sxs-lookup"><span data-stu-id="e0eb3-110">Grant anonymous users permissions to containers and blobs</span></span>
<span data-ttu-id="e0eb3-111">Domyślnie kontener i wszystkie obiekty BLOB w nim mogą być używane tylko przez właściciela konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="e0eb3-111">By default, a container and any blobs within it may be accessed only by the owner of the storage account.</span></span> <span data-ttu-id="e0eb3-112">Aby udostępnić użytkownikom anonimowym uprawnienia odczytu do kontenera i jego obiektów blob, można ustawić uprawnień kontenera, aby zezwolić na publiczny dostęp.</span><span class="sxs-lookup"><span data-stu-id="e0eb3-112">To give anonymous users read permissions to a container and its blobs, you can set the container permissions to allow public access.</span></span> <span data-ttu-id="e0eb3-113">Użytkownicy anonimowi mogą odczytywać obiekty BLOB w kontenerze publicznie bez uwierzytelniania żądania.</span><span class="sxs-lookup"><span data-stu-id="e0eb3-113">Anonymous users can read blobs within a publicly accessible container without authenticating the request.</span></span>

<span data-ttu-id="e0eb3-114">Kontener można skonfigurować następujące uprawnienia:</span><span class="sxs-lookup"><span data-stu-id="e0eb3-114">You can configure a container with the following permissions:</span></span>

* <span data-ttu-id="e0eb3-115">**Dostęp do odczytu żadnego elementu publicznego public:** kontenera i jego obiektów blob są dostępne tylko przez właściciela konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="e0eb3-115">**No public read access:** The container and its blobs can be accessed only by the storage account owner.</span></span> <span data-ttu-id="e0eb3-116">Jest to wartość domyślna dla wszystkich nowych kontenerów.</span><span class="sxs-lookup"><span data-stu-id="e0eb3-116">This is the default for all new containers.</span></span>
* <span data-ttu-id="e0eb3-117">**Dostęp do obiektów blob tylko odczytu publicznego:** obiekty BLOB w kontenerze może zostać odczytany przez żądania od użytkowników anonimowych, ale nie są dostępne dane kontenera.</span><span class="sxs-lookup"><span data-stu-id="e0eb3-117">**Public read access for blobs only:** Blobs within the container can be read by anonymous request, but container data is not available.</span></span> <span data-ttu-id="e0eb3-118">Anonimowe klientów nie można wyliczyć obiektów blob w kontenerze.</span><span class="sxs-lookup"><span data-stu-id="e0eb3-118">Anonymous clients cannot enumerate the blobs within the container.</span></span>
* <span data-ttu-id="e0eb3-119">**Pełne publiczny dostęp do odczytu:** wszystkie dane obiektów blob i kontener może zostać odczytany przez żądania od użytkowników anonimowych.</span><span class="sxs-lookup"><span data-stu-id="e0eb3-119">**Full public read access:** All container and blob data can be read by anonymous request.</span></span> <span data-ttu-id="e0eb3-120">Klientów można wyliczyć obiektów blob w kontenerze przez żądania od użytkowników anonimowych, ale nie można wyliczyć kontenery w ramach konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="e0eb3-120">Clients can enumerate blobs within the container by anonymous request, but cannot enumerate containers within the storage account.</span></span>

<span data-ttu-id="e0eb3-121">Następujące służy do ustawiania uprawnień kontenera:</span><span class="sxs-lookup"><span data-stu-id="e0eb3-121">You can use the following to set container permissions:</span></span>

* [<span data-ttu-id="e0eb3-122">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e0eb3-122">Azure portal</span></span>](https://portal.azure.com)
* [<span data-ttu-id="e0eb3-123">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e0eb3-123">Azure PowerShell</span></span>](../common/storage-powershell-guide-full.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#how-to-manage-azure-blobs)
* [<span data-ttu-id="e0eb3-124">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="e0eb3-124">Azure CLI 2.0</span></span>](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#create-and-manage-blobs)
* <span data-ttu-id="e0eb3-125">Programowo za pomocą jednej z bibliotek klienckich magazynu lub interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="e0eb3-125">Programmatically, by using one of the storage client libraries or the REST API</span></span>

### <a name="set-container-permissions-in-the-azure-portal"></a><span data-ttu-id="e0eb3-126">Ustaw uprawnienia kontenera w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="e0eb3-126">Set container permissions in the Azure portal</span></span>
<span data-ttu-id="e0eb3-127">Aby ustawić uprawnienia do kontenera w [portalu Azure](https://portal.azure.com), wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="e0eb3-127">To set container permissions in the [Azure portal](https://portal.azure.com), follow these steps:</span></span>

1. <span data-ttu-id="e0eb3-128">Otwórz z **konta magazynu** bloku w portalu.</span><span class="sxs-lookup"><span data-stu-id="e0eb3-128">Open your **Storage account** blade in the portal.</span></span> <span data-ttu-id="e0eb3-129">Można znaleźć konta magazynu, wybierając **kont magazynu** w bloku portalu menu głównego.</span><span class="sxs-lookup"><span data-stu-id="e0eb3-129">You can find your storage account by selecting **Storage accounts** in the main portal menu blade.</span></span>
1. <span data-ttu-id="e0eb3-130">W obszarze **usługa BLOB** w bloku menu wybierz **kontenery**.</span><span class="sxs-lookup"><span data-stu-id="e0eb3-130">Under **BLOB SERVICE** on the menu blade, select **Containers**.</span></span>
1. <span data-ttu-id="e0eb3-131">Kliknij prawym przyciskiem myszy w wierszu kontenera lub wybierz przycisk wielokropka, aby otworzyć kontenera **menu kontekstowe**.</span><span class="sxs-lookup"><span data-stu-id="e0eb3-131">Right-click on the container row or select the ellipsis to open the container's **Context menu**.</span></span>
1. <span data-ttu-id="e0eb3-132">Wybierz **zasady dostępu** w menu kontekstowym.</span><span class="sxs-lookup"><span data-stu-id="e0eb3-132">Select **Access policy** in the context menu.</span></span>
1. <span data-ttu-id="e0eb3-133">Wybierz **dostęp typu** z menu rozwijanego.</span><span class="sxs-lookup"><span data-stu-id="e0eb3-133">Select an **Access type** from the drop down menu.</span></span>

    ![Okno dialogowe metadanych kontenera Edycja](./media/storage-manage-access-to-resources/storage-manage-access-to-resources-0.png)

### <a name="set-container-permissions-with-net"></a><span data-ttu-id="e0eb3-135">Ustawianie uprawnień kontenera z platformą .NET</span><span class="sxs-lookup"><span data-stu-id="e0eb3-135">Set container permissions with .NET</span></span>
<span data-ttu-id="e0eb3-136">Aby ustawić uprawnienia do kontenera przy użyciu języka C# i biblioteki klienta usługi Storage dla platformy .NET, najpierw pobrać kontenera istniejące uprawnienia, wywołując **GetPermissions** metody.</span><span class="sxs-lookup"><span data-stu-id="e0eb3-136">To set permissions for a container using C# and the Storage Client Library for .NET, first retrieve the container's existing permissions by calling the **GetPermissions** method.</span></span> <span data-ttu-id="e0eb3-137">Następnie ustaw **PublicAccess** właściwość **BlobContainerPermissions** obiektu, który jest zwracany przez **GetPermissions** metody.</span><span class="sxs-lookup"><span data-stu-id="e0eb3-137">Then set the **PublicAccess** property for the **BlobContainerPermissions** object that is returned by the **GetPermissions** method.</span></span> <span data-ttu-id="e0eb3-138">Na koniec wywołania **ustawiania** metody zaktualizowano uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="e0eb3-138">Finally, call the **SetPermissions** method with the updated permissions.</span></span>

<span data-ttu-id="e0eb3-139">Poniższy przykład ustawia kontenera uprawnienia do pełnej publiczny dostęp do odczytu.</span><span class="sxs-lookup"><span data-stu-id="e0eb3-139">The following example sets the container's permissions to full public read access.</span></span> <span data-ttu-id="e0eb3-140">Uprawnienia do publiczny dostęp do odczytu obiektów blob jedynie ustawia **PublicAccess** właściwości **BlobContainerPublicAccessType.Blob**.</span><span class="sxs-lookup"><span data-stu-id="e0eb3-140">To set permissions to public read access for blobs only, set the **PublicAccess** property to **BlobContainerPublicAccessType.Blob**.</span></span> <span data-ttu-id="e0eb3-141">Aby usunąć wszystkie uprawnienia dla użytkowników anonimowych, ustaw dla właściwości **BlobContainerPublicAccessType.Off**.</span><span class="sxs-lookup"><span data-stu-id="e0eb3-141">To remove all permissions for anonymous users, set the property to **BlobContainerPublicAccessType.Off**.</span></span>

```csharp
public static void SetPublicContainerPermissions(CloudBlobContainer container)
{
    BlobContainerPermissions permissions = container.GetPermissions();
    permissions.PublicAccess = BlobContainerPublicAccessType.Container;
    container.SetPermissions(permissions);
}
```

## <a name="access-containers-and-blobs-anonymously"></a><span data-ttu-id="e0eb3-142">Dostęp do kontenerów i obiektów blob anonimowo</span><span class="sxs-lookup"><span data-stu-id="e0eb3-142">Access containers and blobs anonymously</span></span>
<span data-ttu-id="e0eb3-143">Klient, który uzyskuje dostęp do kontenerów i obiektów blob anonimowo można użyć konstruktorów, które nie wymagają poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="e0eb3-143">A client that accesses containers and blobs anonymously can use constructors that do not require credentials.</span></span> <span data-ttu-id="e0eb3-144">W poniższych przykładach pokazano na kilka różnych sposobów odwołanie do obiektu Blob usługi zasobów anonimowo.</span><span class="sxs-lookup"><span data-stu-id="e0eb3-144">The following examples show a few different ways to reference Blob service resources anonymously.</span></span>

### <a name="create-an-anonymous-client-object"></a><span data-ttu-id="e0eb3-145">Tworzenie obiektu anonimowego klienta</span><span class="sxs-lookup"><span data-stu-id="e0eb3-145">Create an anonymous client object</span></span>
<span data-ttu-id="e0eb3-146">Można utworzyć nowy obiekt klienta usługi dla dostępu anonimowego, podając konto punkt końcowy usługi Blob.</span><span class="sxs-lookup"><span data-stu-id="e0eb3-146">You can create a new service client object for anonymous access by providing the Blob service endpoint for the account.</span></span> <span data-ttu-id="e0eb3-147">Jednak również musi znać nazwę kontenera na tym koncie, który jest dostępny dla dostępu anonimowego.</span><span class="sxs-lookup"><span data-stu-id="e0eb3-147">However, you must also know the name of a container in that account that's available for anonymous access.</span></span>

```csharp
public static void CreateAnonymousBlobClient()
{
    // Create the client object using the Blob service endpoint.
    CloudBlobClient blobClient = new CloudBlobClient(new Uri(@"https://storagesample.blob.core.windows.net"));

    // Get a reference to a container that's available for anonymous access.
    CloudBlobContainer container = blobClient.GetContainerReference("sample-container");

    // Read the container's properties. Note this is only possible when the container supports full public read access.
    container.FetchAttributes();
    Console.WriteLine(container.Properties.LastModified);
    Console.WriteLine(container.Properties.ETag);
}
```

### <a name="reference-a-container-anonymously"></a><span data-ttu-id="e0eb3-148">Odwołanie kontenera anonimowego</span><span class="sxs-lookup"><span data-stu-id="e0eb3-148">Reference a container anonymously</span></span>
<span data-ttu-id="e0eb3-149">Jeśli adres URL do kontenera, który jest dostępny anonimowo, można go bezpośrednio odwoływać kontenera.</span><span class="sxs-lookup"><span data-stu-id="e0eb3-149">If you have the URL to a container that is anonymously available, you can use it to reference the container directly.</span></span>

```csharp
public static void ListBlobsAnonymously()
{
    // Get a reference to a container that's available for anonymous access.
    CloudBlobContainer container = new CloudBlobContainer(new Uri(@"https://storagesample.blob.core.windows.net/sample-container"));

    // List blobs in the container.
    foreach (IListBlobItem blobItem in container.ListBlobs())
    {
        Console.WriteLine(blobItem.Uri);
    }
}
```

### <a name="reference-a-blob-anonymously"></a><span data-ttu-id="e0eb3-150">Odwołanie obiektu blob anonimowo</span><span class="sxs-lookup"><span data-stu-id="e0eb3-150">Reference a blob anonymously</span></span>
<span data-ttu-id="e0eb3-151">Jeśli adres URL obiektu blob, który jest dostępny dla dostępu anonimowego, może odwoływać się bezpośrednio przy użyciu tego adresu URL obiektu blob:</span><span class="sxs-lookup"><span data-stu-id="e0eb3-151">If you have the URL to a blob that is available for anonymous access, you can reference the blob directly using that URL:</span></span>

```csharp
public static void DownloadBlobAnonymously()
{
    CloudBlockBlob blob = new CloudBlockBlob(new Uri(@"https://storagesample.blob.core.windows.net/sample-container/logfile.txt"));
    blob.DownloadToFile(@"C:\Temp\logfile.txt", System.IO.FileMode.Create);
}
```

## <a name="features-available-to-anonymous-users"></a><span data-ttu-id="e0eb3-152">Funkcje dostępne dla użytkowników anonimowych</span><span class="sxs-lookup"><span data-stu-id="e0eb3-152">Features available to anonymous users</span></span>
<span data-ttu-id="e0eb3-153">Poniższej tabeli operacje może zostać wywołana przez użytkowników anonimowych ustawianą ACL kontenera umożliwiających dostęp do publicznego.</span><span class="sxs-lookup"><span data-stu-id="e0eb3-153">The following table shows which operations may be called by anonymous users when a container's ACL is set to allow public access.</span></span>

| <span data-ttu-id="e0eb3-154">Operacji REST</span><span class="sxs-lookup"><span data-stu-id="e0eb3-154">REST Operation</span></span> | <span data-ttu-id="e0eb3-155">Uprawnienie o pełnej publiczny dostęp do odczytu</span><span class="sxs-lookup"><span data-stu-id="e0eb3-155">Permission with full public read access</span></span> | <span data-ttu-id="e0eb3-156">Uprawnienie o publiczny dostęp do odczytu obiektów blob tylko</span><span class="sxs-lookup"><span data-stu-id="e0eb3-156">Permission with public read access for blobs only</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e0eb3-157">Kontenery listy</span><span class="sxs-lookup"><span data-stu-id="e0eb3-157">List Containers</span></span> |<span data-ttu-id="e0eb3-158">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="e0eb3-158">Owner only</span></span> |<span data-ttu-id="e0eb3-159">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="e0eb3-159">Owner only</span></span> |
| <span data-ttu-id="e0eb3-160">Tworzenie kontenera</span><span class="sxs-lookup"><span data-stu-id="e0eb3-160">Create Container</span></span> |<span data-ttu-id="e0eb3-161">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="e0eb3-161">Owner only</span></span> |<span data-ttu-id="e0eb3-162">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="e0eb3-162">Owner only</span></span> |
| <span data-ttu-id="e0eb3-163">Pobierz właściwości kontenera</span><span class="sxs-lookup"><span data-stu-id="e0eb3-163">Get Container Properties</span></span> |<span data-ttu-id="e0eb3-164">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="e0eb3-164">All</span></span> |<span data-ttu-id="e0eb3-165">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="e0eb3-165">Owner only</span></span> |
| <span data-ttu-id="e0eb3-166">Pobranie metadanych kontenera</span><span class="sxs-lookup"><span data-stu-id="e0eb3-166">Get Container Metadata</span></span> |<span data-ttu-id="e0eb3-167">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="e0eb3-167">All</span></span> |<span data-ttu-id="e0eb3-168">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="e0eb3-168">Owner only</span></span> |
| <span data-ttu-id="e0eb3-169">Ustaw metadanych kontenera</span><span class="sxs-lookup"><span data-stu-id="e0eb3-169">Set Container Metadata</span></span> |<span data-ttu-id="e0eb3-170">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="e0eb3-170">Owner only</span></span> |<span data-ttu-id="e0eb3-171">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="e0eb3-171">Owner only</span></span> |
| <span data-ttu-id="e0eb3-172">Pobierz ACL kontenera</span><span class="sxs-lookup"><span data-stu-id="e0eb3-172">Get Container ACL</span></span> |<span data-ttu-id="e0eb3-173">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="e0eb3-173">Owner only</span></span> |<span data-ttu-id="e0eb3-174">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="e0eb3-174">Owner only</span></span> |
| <span data-ttu-id="e0eb3-175">Ustaw ACL kontenera</span><span class="sxs-lookup"><span data-stu-id="e0eb3-175">Set Container ACL</span></span> |<span data-ttu-id="e0eb3-176">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="e0eb3-176">Owner only</span></span> |<span data-ttu-id="e0eb3-177">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="e0eb3-177">Owner only</span></span> |
| <span data-ttu-id="e0eb3-178">Usunąć kontenera</span><span class="sxs-lookup"><span data-stu-id="e0eb3-178">Delete Container</span></span> |<span data-ttu-id="e0eb3-179">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="e0eb3-179">Owner only</span></span> |<span data-ttu-id="e0eb3-180">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="e0eb3-180">Owner only</span></span> |
| <span data-ttu-id="e0eb3-181">Lista obiektów blob</span><span class="sxs-lookup"><span data-stu-id="e0eb3-181">List Blobs</span></span> |<span data-ttu-id="e0eb3-182">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="e0eb3-182">All</span></span> |<span data-ttu-id="e0eb3-183">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="e0eb3-183">Owner only</span></span> |
| <span data-ttu-id="e0eb3-184">Umieszczanie obiektu Blob</span><span class="sxs-lookup"><span data-stu-id="e0eb3-184">Put Blob</span></span> |<span data-ttu-id="e0eb3-185">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="e0eb3-185">Owner only</span></span> |<span data-ttu-id="e0eb3-186">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="e0eb3-186">Owner only</span></span> |
| <span data-ttu-id="e0eb3-187">Pobierz obiekt Blob</span><span class="sxs-lookup"><span data-stu-id="e0eb3-187">Get Blob</span></span> |<span data-ttu-id="e0eb3-188">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="e0eb3-188">All</span></span> |<span data-ttu-id="e0eb3-189">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="e0eb3-189">All</span></span> |
| <span data-ttu-id="e0eb3-190">Pobierz właściwości obiektu Blob</span><span class="sxs-lookup"><span data-stu-id="e0eb3-190">Get Blob Properties</span></span> |<span data-ttu-id="e0eb3-191">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="e0eb3-191">All</span></span> |<span data-ttu-id="e0eb3-192">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="e0eb3-192">All</span></span> |
| <span data-ttu-id="e0eb3-193">Ustaw właściwości obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="e0eb3-193">Set Blob Properties</span></span> |<span data-ttu-id="e0eb3-194">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="e0eb3-194">Owner only</span></span> |<span data-ttu-id="e0eb3-195">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="e0eb3-195">Owner only</span></span> |
| <span data-ttu-id="e0eb3-196">Pobierz metadane obiektu Blob</span><span class="sxs-lookup"><span data-stu-id="e0eb3-196">Get Blob Metadata</span></span> |<span data-ttu-id="e0eb3-197">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="e0eb3-197">All</span></span> |<span data-ttu-id="e0eb3-198">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="e0eb3-198">All</span></span> |
| <span data-ttu-id="e0eb3-199">Ustaw metadane obiektu Blob</span><span class="sxs-lookup"><span data-stu-id="e0eb3-199">Set Blob Metadata</span></span> |<span data-ttu-id="e0eb3-200">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="e0eb3-200">Owner only</span></span> |<span data-ttu-id="e0eb3-201">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="e0eb3-201">Owner only</span></span> |
| <span data-ttu-id="e0eb3-202">Umieść bloku</span><span class="sxs-lookup"><span data-stu-id="e0eb3-202">Put Block</span></span> |<span data-ttu-id="e0eb3-203">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="e0eb3-203">Owner only</span></span> |<span data-ttu-id="e0eb3-204">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="e0eb3-204">Owner only</span></span> |
| <span data-ttu-id="e0eb3-205">Pobierz listę zablokowanych (tylko zatwierdzone bloki)</span><span class="sxs-lookup"><span data-stu-id="e0eb3-205">Get Block List (committed blocks only)</span></span> |<span data-ttu-id="e0eb3-206">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="e0eb3-206">All</span></span> |<span data-ttu-id="e0eb3-207">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="e0eb3-207">All</span></span> |
| <span data-ttu-id="e0eb3-208">Pobierz listę bloku (tylko niezatwierdzone bloków lub wszystkie bloki)</span><span class="sxs-lookup"><span data-stu-id="e0eb3-208">Get Block List (uncommitted blocks only or all blocks)</span></span> |<span data-ttu-id="e0eb3-209">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="e0eb3-209">Owner only</span></span> |<span data-ttu-id="e0eb3-210">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="e0eb3-210">Owner only</span></span> |
| <span data-ttu-id="e0eb3-211">Umieść zablokowanych</span><span class="sxs-lookup"><span data-stu-id="e0eb3-211">Put Block List</span></span> |<span data-ttu-id="e0eb3-212">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="e0eb3-212">Owner only</span></span> |<span data-ttu-id="e0eb3-213">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="e0eb3-213">Owner only</span></span> |
| <span data-ttu-id="e0eb3-214">Usuwanie obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="e0eb3-214">Delete Blob</span></span> |<span data-ttu-id="e0eb3-215">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="e0eb3-215">Owner only</span></span> |<span data-ttu-id="e0eb3-216">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="e0eb3-216">Owner only</span></span> |
| <span data-ttu-id="e0eb3-217">Kopiowanie obiektu Blob</span><span class="sxs-lookup"><span data-stu-id="e0eb3-217">Copy Blob</span></span> |<span data-ttu-id="e0eb3-218">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="e0eb3-218">Owner only</span></span> |<span data-ttu-id="e0eb3-219">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="e0eb3-219">Owner only</span></span> |
| <span data-ttu-id="e0eb3-220">Migawki obiektu Blob</span><span class="sxs-lookup"><span data-stu-id="e0eb3-220">Snapshot Blob</span></span> |<span data-ttu-id="e0eb3-221">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="e0eb3-221">Owner only</span></span> |<span data-ttu-id="e0eb3-222">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="e0eb3-222">Owner only</span></span> |
| <span data-ttu-id="e0eb3-223">Obiekt Blob dzierżawy</span><span class="sxs-lookup"><span data-stu-id="e0eb3-223">Lease Blob</span></span> |<span data-ttu-id="e0eb3-224">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="e0eb3-224">Owner only</span></span> |<span data-ttu-id="e0eb3-225">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="e0eb3-225">Owner only</span></span> |
| <span data-ttu-id="e0eb3-226">Umieść stronę</span><span class="sxs-lookup"><span data-stu-id="e0eb3-226">Put Page</span></span> |<span data-ttu-id="e0eb3-227">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="e0eb3-227">Owner only</span></span> |<span data-ttu-id="e0eb3-228">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="e0eb3-228">Owner only</span></span> |
| <span data-ttu-id="e0eb3-229">Get zakresów stron</span><span class="sxs-lookup"><span data-stu-id="e0eb3-229">Get Page Ranges</span></span> |<span data-ttu-id="e0eb3-230">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="e0eb3-230">All</span></span> |<span data-ttu-id="e0eb3-231">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="e0eb3-231">All</span></span> |
| <span data-ttu-id="e0eb3-232">Dołącz obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="e0eb3-232">Append Blob</span></span> |<span data-ttu-id="e0eb3-233">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="e0eb3-233">Owner only</span></span> |<span data-ttu-id="e0eb3-234">Tylko właściciel</span><span class="sxs-lookup"><span data-stu-id="e0eb3-234">Owner only</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e0eb3-235">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e0eb3-235">Next steps</span></span>

* [<span data-ttu-id="e0eb3-236">Uwierzytelnianie dla usług Azure Storage</span><span class="sxs-lookup"><span data-stu-id="e0eb3-236">Authentication for the Azure Storage Services</span></span>](https://msdn.microsoft.com/library/azure/dd179428.aspx)
* [<span data-ttu-id="e0eb3-237">Przy użyciu sygnatury dostępu współdzielonego (SAS)</span><span class="sxs-lookup"><span data-stu-id="e0eb3-237">Using Shared Access Signatures (SAS)</span></span>](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [<span data-ttu-id="e0eb3-238">Delegowanie dostępu za pomocą sygnatury dostępu współdzielonego</span><span class="sxs-lookup"><span data-stu-id="e0eb3-238">Delegating Access with a Shared Access Signature</span></span>](https://msdn.microsoft.com/library/azure/ee395415.aspx)
