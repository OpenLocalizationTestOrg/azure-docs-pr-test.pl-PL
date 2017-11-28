---
title: "czas wygaśnięcia aaaManage obiektów blob magazynu Azure w usłudze Azure CDN | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat opcji hello kontrolowanie time-to-live dla obiektów blob w pamięci podręcznej Azure CDN."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: ad4801e9-d09a-49bf-b35c-efdc4e6034e8
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 9fecae9639deb28977da7f851e1da4a823ddc4e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-expiration-of-azure-storage-blobs-in-azure-cdn"></a><span data-ttu-id="b8d52-103">Zarządzaj wygasaniem obiektów blob magazynu Azure w usłudze Azure CDN</span><span class="sxs-lookup"><span data-stu-id="b8d52-103">Manage expiration of Azure Storage blobs in Azure CDN</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b8d52-104">Usługi aplikacji/w chmurze Azure sieci Web, ASP.NET lub usług IIS</span><span class="sxs-lookup"><span data-stu-id="b8d52-104">Azure Web Apps/Cloud Services, ASP.NET, or IIS</span></span>](cdn-manage-expiration-of-cloud-service-content.md)
> * [<span data-ttu-id="b8d52-105">Usługa blob magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="b8d52-105">Azure Storage blob service</span></span>](cdn-manage-expiration-of-blob-content.md)
> 
> 

<span data-ttu-id="b8d52-106">Witaj [usługa blob](../storage/common/storage-introduction.md#blob-storage) w [usługi Azure Storage](../storage/common/storage-introduction.md) jest jedną z wielu źródeł opartych na platformie Azure zintegrowanych z usługą Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="b8d52-106">hello [blob service](../storage/common/storage-introduction.md#blob-storage) in [Azure Storage](../storage/common/storage-introduction.md) is one of several Azure-based origins integrated with Azure CDN.</span></span>  <span data-ttu-id="b8d52-107">Zawartość obiektu blob publicznie mogą być buforowane w usłudze Azure CDN, dopóki nie upłynie jego czas wygaśnięcia (TTL).</span><span class="sxs-lookup"><span data-stu-id="b8d52-107">Any publicly accessible blob content can be cached in Azure CDN until its time-to-live (TTL) elapses.</span></span>  <span data-ttu-id="b8d52-108">Witaj czas wygaśnięcia jest określany przez hello [ *Cache-Control* nagłówka](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) hello HTTP odpowiedzi z usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="b8d52-108">hello TTL is determined by hello [*Cache-Control* header](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) in hello HTTP response from Azure Storage.</span></span>

> [!TIP]
> <span data-ttu-id="b8d52-109">Możesz wybrać tooset nie TTL na obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="b8d52-109">You may choose tooset no TTL on a blob.</span></span>  <span data-ttu-id="b8d52-110">W takim przypadku Azure CDN automatycznie stosuje domyślny czas wygaśnięcia wynosi siedem dni.</span><span class="sxs-lookup"><span data-stu-id="b8d52-110">In this case, Azure CDN automatically applies a default TTL of seven days.</span></span>
> 
> <span data-ttu-id="b8d52-111">Aby uzyskać więcej informacji na temat działania usługi Azure CDN toospeed tooblobs dostępu i innych plików, zobacz hello [Omówienie usługi Azure CDN](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b8d52-111">For more information about how Azure CDN works toospeed up access tooblobs and other files, see hello [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> <span data-ttu-id="b8d52-112">Więcej szczegółów na powitania usługa blob magazynu Azure, zobacz [pojęcia dotyczące usługi Blob](https://msdn.microsoft.com/library/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="b8d52-112">For more details on hello Azure Storage blob service, see [Blob Service Concepts](https://msdn.microsoft.com/library/dd179376.aspx).</span></span> 
> 
> 

<span data-ttu-id="b8d52-113">W tym samouczku przedstawiono kilka sposobów, że hello TTL można ustawić dla obiektu blob w usłudze Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="b8d52-113">This tutorial demonstrates several ways that you can set hello TTL on a blob in Azure Storage.</span></span>  

## <a name="azure-powershell"></a><span data-ttu-id="b8d52-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b8d52-114">Azure PowerShell</span></span>
<span data-ttu-id="b8d52-115">[Program Azure PowerShell](/powershell/azure/overview) jest jednym z tooadminister najszybsze i najbardziej efektywny sposób hello usługami Azure.</span><span class="sxs-lookup"><span data-stu-id="b8d52-115">[Azure PowerShell](/powershell/azure/overview) is one of hello quickest, most powerful ways tooadminister your Azure services.</span></span>  <span data-ttu-id="b8d52-116">Użyj hello `Get-AzureStorageBlob` tooget polecenia cmdlet obiektu blob toohello odwołania, a następnie ustaw hello `.ICloudBlob.Properties.CacheControl` właściwości.</span><span class="sxs-lookup"><span data-stu-id="b8d52-116">Use hello `Get-AzureStorageBlob` cmdlet tooget a reference toohello blob, then set hello `.ICloudBlob.Properties.CacheControl` property.</span></span> 

```powershell
# Create a storage context
$context = New-AzureStorageContext -StorageAccountName "<storage account name>" -StorageAccountKey "<storage account key>"

# Get a reference toohello blob
$blob = Get-AzureStorageBlob -Context $context -Container "<container name>" -Blob "<blob name>"

# Set hello CacheControl property tooexpire in 1 hour (3600 seconds)
$blob.ICloudBlob.Properties.CacheControl = "public, max-age=3600"

# Send hello update toohello cloud
$blob.ICloudBlob.SetProperties()
```

> [!TIP]
> <span data-ttu-id="b8d52-117">Można również użyć środowiska PowerShell zbyt[Zarządzanie punktów końcowych i profile CDN](cdn-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="b8d52-117">You can also use PowerShell too[manage your CDN profiles and endpoints](cdn-manage-powershell.md).</span></span>
> 
> 

## <a name="azure-storage-client-library-for-net"></a><span data-ttu-id="b8d52-118">Biblioteka klienta usługi Azure Storage dla programu .NET</span><span class="sxs-lookup"><span data-stu-id="b8d52-118">Azure Storage Client Library for .NET</span></span>
<span data-ttu-id="b8d52-119">tooset obiektu blob na TTL przy użyciu platformy .NET, użyj hello [biblioteki klienta magazynu Azure dla platformy .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) tooset hello [CloudBlob.Properties.CacheControl](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.blobproperties.cachecontrol.aspx) właściwości.</span><span class="sxs-lookup"><span data-stu-id="b8d52-119">tooset a blob's TTL using .NET, use hello [Azure Storage Client Library for .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) tooset hello [CloudBlob.Properties.CacheControl](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.blobproperties.cachecontrol.aspx) property.</span></span>

```csharp
class Program
{
    const string connectionString = "<storage connection string>";
    static void Main()
    {
        // Retrieve storage account information from connection string
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);

        // Create a blob client for interacting with hello blob service.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

        // Create a reference toohello container
        CloudBlobContainer container = blobClient.GetContainerReference("<container name>");

        // Create a reference toohello blob
        CloudBlob blob = container.GetBlobReference("<blob name>");

        // Set hello CacheControl property tooexpire in 1 hour (3600 seconds)
        blob.Properties.CacheControl = "public, max-age=3600";

        // Update hello blob's properties in hello cloud
        blob.SetProperties();
    }
}
```

> [!TIP]
> <span data-ttu-id="b8d52-120">Brak dostępnych wiele więcej przykładów kodu platformy .NET w hello [przykłady magazynu obiektów Blob platformy Azure dla platformy .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="b8d52-120">There are many more .NET code samples available in hello [Azure Blob Storage Samples for .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span></span>
> 
> 

## <a name="other-methods"></a><span data-ttu-id="b8d52-121">Inne metody</span><span class="sxs-lookup"><span data-stu-id="b8d52-121">Other methods</span></span>
* [<span data-ttu-id="b8d52-122">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b8d52-122">Azure Command-Line Interface</span></span>](../cli-install-nodejs.md)
  
    <span data-ttu-id="b8d52-123">Podczas przekazywania hello obiektów blob, należy ustawić hello *cacheControl* właściwości przy użyciu hello `-p` przełącznika.</span><span class="sxs-lookup"><span data-stu-id="b8d52-123">When uploading hello blob, set hello *cacheControl* property using hello `-p` switch.</span></span>  <span data-ttu-id="b8d52-124">W tym przykładzie hello TTL tooone godzina (3600 sekund).</span><span class="sxs-lookup"><span data-stu-id="b8d52-124">This example sets hello TTL tooone hour (3600 seconds).</span></span>
  
    ```text
    azure storage blob upload -c <connectionstring> -p cacheControl="public, max-age=3600" .\test.txt myContainer test.txt
    ```
* [<span data-ttu-id="b8d52-125">Interfejs API REST usług Azure Storage</span><span class="sxs-lookup"><span data-stu-id="b8d52-125">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
  
    <span data-ttu-id="b8d52-126">Jawnie ustaw hello *x-ms-blob-cache-control* właściwość [umieszczanie obiektu Blob](https://msdn.microsoft.com/en-us/library/azure/dd179451.aspx), [Put zablokowanych](https://msdn.microsoft.com/en-us/library/azure/dd179467.aspx), lub [Ustaw właściwości obiektów Blob](https://msdn.microsoft.com/library/azure/ee691966.aspx) żądania.</span><span class="sxs-lookup"><span data-stu-id="b8d52-126">Explicitly set hello *x-ms-blob-cache-control* property on a [Put Blob](https://msdn.microsoft.com/en-us/library/azure/dd179451.aspx), [Put Block List](https://msdn.microsoft.com/en-us/library/azure/dd179467.aspx), or [Set Blob Properties](https://msdn.microsoft.com/library/azure/ee691966.aspx) request.</span></span>
* <span data-ttu-id="b8d52-127">Narzędzia do zarządzania magazynem innych firm</span><span class="sxs-lookup"><span data-stu-id="b8d52-127">Third-party storage management tools</span></span>
  
    <span data-ttu-id="b8d52-128">Niektóre narzędzia do zarządzania magazynem Azure innej firmy pozwala tooset hello *CacheControl* właściwości obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="b8d52-128">Some third-party Azure Storage management tools allow you tooset hello *CacheControl* property on blobs.</span></span> 

## <a name="testing-hello-cache-control-header"></a><span data-ttu-id="b8d52-129">Testowanie hello *Cache-Control* nagłówka</span><span class="sxs-lookup"><span data-stu-id="b8d52-129">Testing hello *Cache-Control* header</span></span>
<span data-ttu-id="b8d52-130">Możesz łatwo sprawdzić hello TTL obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="b8d52-130">You can easily verify hello TTL of your blobs.</span></span>  <span data-ttu-id="b8d52-131">Za pomocą przeglądarki [narzędzia dla deweloperów](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/), testów z obiektu blob łącznie z hello *Cache-Control* nagłówka odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="b8d52-131">Using your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/), test that your blob is including hello *Cache-Control* response header.</span></span>  <span data-ttu-id="b8d52-132">Można także użyć narzędzia, takiego jak **wget**, [Postman](https://www.getpostman.com/), lub [Fiddler](http://www.telerik.com/fiddler) nagłówki odpowiedzi hello tooexamine.</span><span class="sxs-lookup"><span data-stu-id="b8d52-132">You can also use a tool like **wget**, [Postman](https://www.getpostman.com/), or [Fiddler](http://www.telerik.com/fiddler) tooexamine hello response headers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b8d52-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b8d52-133">Next Steps</span></span>
* [<span data-ttu-id="b8d52-134">Przeczytaj informacje o hello *Cache-Control* nagłówka</span><span class="sxs-lookup"><span data-stu-id="b8d52-134">Read about hello *Cache-Control* header</span></span>](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9)
* [<span data-ttu-id="b8d52-135">Dowiedz się, jak toomanage wygasaniem zawartości usługi w chmurze w usłudze Azure CDN</span><span class="sxs-lookup"><span data-stu-id="b8d52-135">Learn how toomanage expiration of Cloud Service content in Azure CDN</span></span>](cdn-manage-expiration-of-cloud-service-content.md)

