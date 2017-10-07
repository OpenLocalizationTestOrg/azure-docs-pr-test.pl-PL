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
# <a name="manage-expiration-of-azure-storage-blobs-in-azure-cdn"></a>Zarządzaj wygasaniem obiektów blob magazynu Azure w usłudze Azure CDN
> [!div class="op_single_selector"]
> * [Usługi aplikacji/w chmurze Azure sieci Web, ASP.NET lub usług IIS](cdn-manage-expiration-of-cloud-service-content.md)
> * [Usługa blob magazynu Azure](cdn-manage-expiration-of-blob-content.md)
> 
> 

Witaj [usługa blob](../storage/common/storage-introduction.md#blob-storage) w [usługi Azure Storage](../storage/common/storage-introduction.md) jest jedną z wielu źródeł opartych na platformie Azure zintegrowanych z usługą Azure CDN.  Zawartość obiektu blob publicznie mogą być buforowane w usłudze Azure CDN, dopóki nie upłynie jego czas wygaśnięcia (TTL).  Witaj czas wygaśnięcia jest określany przez hello [ *Cache-Control* nagłówka](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) hello HTTP odpowiedzi z usługi Azure Storage.

> [!TIP]
> Możesz wybrać tooset nie TTL na obiektu blob.  W takim przypadku Azure CDN automatycznie stosuje domyślny czas wygaśnięcia wynosi siedem dni.
> 
> Aby uzyskać więcej informacji na temat działania usługi Azure CDN toospeed tooblobs dostępu i innych plików, zobacz hello [Omówienie usługi Azure CDN](cdn-overview.md).
> 
> Więcej szczegółów na powitania usługa blob magazynu Azure, zobacz [pojęcia dotyczące usługi Blob](https://msdn.microsoft.com/library/dd179376.aspx). 
> 
> 

W tym samouczku przedstawiono kilka sposobów, że hello TTL można ustawić dla obiektu blob w usłudze Azure Storage.  

## <a name="azure-powershell"></a>Azure PowerShell
[Program Azure PowerShell](/powershell/azure/overview) jest jednym z tooadminister najszybsze i najbardziej efektywny sposób hello usługami Azure.  Użyj hello `Get-AzureStorageBlob` tooget polecenia cmdlet obiektu blob toohello odwołania, a następnie ustaw hello `.ICloudBlob.Properties.CacheControl` właściwości. 

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
> Można również użyć środowiska PowerShell zbyt[Zarządzanie punktów końcowych i profile CDN](cdn-manage-powershell.md).
> 
> 

## <a name="azure-storage-client-library-for-net"></a>Biblioteka klienta usługi Azure Storage dla programu .NET
tooset obiektu blob na TTL przy użyciu platformy .NET, użyj hello [biblioteki klienta magazynu Azure dla platformy .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) tooset hello [CloudBlob.Properties.CacheControl](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.blobproperties.cachecontrol.aspx) właściwości.

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
> Brak dostępnych wiele więcej przykładów kodu platformy .NET w hello [przykłady magazynu obiektów Blob platformy Azure dla platformy .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).
> 
> 

## <a name="other-methods"></a>Inne metody
* [Interfejs wiersza polecenia platformy Azure](../cli-install-nodejs.md)
  
    Podczas przekazywania hello obiektów blob, należy ustawić hello *cacheControl* właściwości przy użyciu hello `-p` przełącznika.  W tym przykładzie hello TTL tooone godzina (3600 sekund).
  
    ```text
    azure storage blob upload -c <connectionstring> -p cacheControl="public, max-age=3600" .\test.txt myContainer test.txt
    ```
* [Interfejs API REST usług Azure Storage](https://msdn.microsoft.com/library/azure/dd179355.aspx)
  
    Jawnie ustaw hello *x-ms-blob-cache-control* właściwość [umieszczanie obiektu Blob](https://msdn.microsoft.com/en-us/library/azure/dd179451.aspx), [Put zablokowanych](https://msdn.microsoft.com/en-us/library/azure/dd179467.aspx), lub [Ustaw właściwości obiektów Blob](https://msdn.microsoft.com/library/azure/ee691966.aspx) żądania.
* Narzędzia do zarządzania magazynem innych firm
  
    Niektóre narzędzia do zarządzania magazynem Azure innej firmy pozwala tooset hello *CacheControl* właściwości obiektów blob. 

## <a name="testing-hello-cache-control-header"></a>Testowanie hello *Cache-Control* nagłówka
Możesz łatwo sprawdzić hello TTL obiektów blob.  Za pomocą przeglądarki [narzędzia dla deweloperów](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/), testów z obiektu blob łącznie z hello *Cache-Control* nagłówka odpowiedzi.  Można także użyć narzędzia, takiego jak **wget**, [Postman](https://www.getpostman.com/), lub [Fiddler](http://www.telerik.com/fiddler) nagłówki odpowiedzi hello tooexamine.

## <a name="next-steps"></a>Następne kroki
* [Przeczytaj informacje o hello *Cache-Control* nagłówka](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9)
* [Dowiedz się, jak toomanage wygasaniem zawartości usługi w chmurze w usłudze Azure CDN](cdn-manage-expiration-of-cloud-service-content.md)

