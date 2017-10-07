---
title: "aaaSet oraz pobrać obiekt właściwości i metadane w usłudze Azure Storage | Dokumentacja firmy Microsoft"
description: "Przechowywania niestandardowych metadanych na obiektach w usłudze Azure Storage i ustawiania i pobierania właściwości systemu."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 036f9006-273e-400b-844b-3329045e9e1f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: marsma
ms.openlocfilehash: 44f9243183014845964f337b476a6b0069dc0902
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-and-retrieve-properties-and-metadata"></a><span data-ttu-id="13de1-103">Ustawianie i pobieranie właściwości oraz metadanych</span><span class="sxs-lookup"><span data-stu-id="13de1-103">Set and retrieve properties and metadata</span></span>

<span data-ttu-id="13de1-104">Obiekty w właściwości systemu pomocy technicznej usługi Azure Storage i metadanych zdefiniowanych przez użytkownika, oprócz toohello nich danych.</span><span class="sxs-lookup"><span data-stu-id="13de1-104">Objects in Azure Storage support system properties and user-defined metadata, in addition toohello data they contain.</span></span> <span data-ttu-id="13de1-105">W tym artykule omówiono zarządzanie właściwości systemu i użytkownika metadanych z hello [biblioteki klienta magazynu Azure dla platformy .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span><span class="sxs-lookup"><span data-stu-id="13de1-105">This article discusses managing system properties and user-defined metadata with hello [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span></span>

* <span data-ttu-id="13de1-106">**Właściwości systemu**: właściwości systemu istnieje dla każdego zasobu magazynu.</span><span class="sxs-lookup"><span data-stu-id="13de1-106">**System properties**: System properties exist on each storage resource.</span></span> <span data-ttu-id="13de1-107">Niektóre z nich można odczytać lub ustawić, podczas gdy inne dotyczą tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="13de1-107">Some of them can be read or set, while others are read-only.</span></span> <span data-ttu-id="13de1-108">W obszarze obejmuje hello niektórych właściwości systemu odpowiada toocertain standardowymi nagłówkami HTTP.</span><span class="sxs-lookup"><span data-stu-id="13de1-108">Under hello covers, some system properties correspond toocertain standard HTTP headers.</span></span> <span data-ttu-id="13de1-109">Biblioteka klienta magazynu Azure Hello przechowuje są dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="13de1-109">hello Azure storage client library maintains these for you.</span></span>

* <span data-ttu-id="13de1-110">**Zdefiniowane przez użytkownika metadanych**: metadane zdefiniowane przez użytkownika są metadane, które można określić dla danego zasobu w postaci hello pary nazwa wartość.</span><span class="sxs-lookup"><span data-stu-id="13de1-110">**User-defined metadata**: User-defined metadata is metadata that you specify on a given resource in hello form of a name-value pair.</span></span> <span data-ttu-id="13de1-111">Możesz użyć wartości dodatkowe metadane toostore zasobów magazynu.</span><span class="sxs-lookup"><span data-stu-id="13de1-111">You can use metadata toostore additional values with a storage resource.</span></span> <span data-ttu-id="13de1-112">Wartości te dodatkowe metadane służą wyłącznie do własnych, a nie wpływają na zachowanie hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="13de1-112">These additional metadata values are for your own purposes only, and do not affect how hello resource behaves.</span></span>

<span data-ttu-id="13de1-113">Podczas pobierania wartości właściwości i metadanych dla zasobu magazynu jest procesem dwuetapowym.</span><span class="sxs-lookup"><span data-stu-id="13de1-113">Retrieving property and metadata values for a storage resource is a two-step process.</span></span> <span data-ttu-id="13de1-114">Przed możesz przeczytać te wartości, użytkownik musi jawnie pobrać je przez wywołanie hello **FetchAttributes** metody.</span><span class="sxs-lookup"><span data-stu-id="13de1-114">Before you can read these values, you must explicitly fetch them by calling hello **FetchAttributes** method.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="13de1-115">Wartości właściwości i metadanych dla zasobów magazynu nie są wypełniane, chyba że należy wywołać hello **FetchAttributes** metody.</span><span class="sxs-lookup"><span data-stu-id="13de1-115">Property and metadata values for a storage resource are not populated unless you call one of hello **FetchAttributes** methods.</span></span>
>
> <span data-ttu-id="13de1-116">Zostanie wyświetlony `400 Bad Request` Jeśli wszystkie pary nazwa/wartość zawiera znaki spoza zestawu ASCII.</span><span class="sxs-lookup"><span data-stu-id="13de1-116">You will receive a `400 Bad Request` if any name/value pairs contain non-ASCII characters.</span></span> <span data-ttu-id="13de1-117">Pary nazwa/wartość metadanych są prawidłowe nagłówków HTTP i dlatego musi być zgodne tooall ograniczenia dotyczące nagłówków HTTP.</span><span class="sxs-lookup"><span data-stu-id="13de1-117">Metadata name/value pairs are valid HTTP headers, and so must adhere tooall restrictions governing HTTP headers.</span></span> <span data-ttu-id="13de1-118">Dlatego zaleca się użycie kodowania adresu URL lub kodowania Base64 dla nazwy i wartości zawierające znaki spoza zestawu ASCII.</span><span class="sxs-lookup"><span data-stu-id="13de1-118">It is therefore recommended that you use URL encoding or Base64 encoding for names and values containing non-ASCII characters.</span></span>
>

## <a name="setting-and-retrieving-properties"></a><span data-ttu-id="13de1-119">Ustawiania i pobierania właściwości</span><span class="sxs-lookup"><span data-stu-id="13de1-119">Setting and retrieving properties</span></span>
<span data-ttu-id="13de1-120">wartości właściwości tooretrieve, wywołanie hello **FetchAttributes** metody dla obiekt blob lub kontener toopopulate hello właściwości, następnie odczytywane hello wartości.</span><span class="sxs-lookup"><span data-stu-id="13de1-120">tooretrieve property values, call hello **FetchAttributes** method on your blob or container toopopulate hello properties, then read hello values.</span></span>

<span data-ttu-id="13de1-121">tooset właściwości w obiekcie, określ wartość właściwości hello, a następnie wywołaj hello **SetProperties** metody.</span><span class="sxs-lookup"><span data-stu-id="13de1-121">tooset properties on an object, specify hello property value, then call hello **SetProperties** method.</span></span>

<span data-ttu-id="13de1-122">Witaj poniższy przykład kodu tworzy kontener, a następnie zapisuje niektórych okna konsoli tooa wartości właściwości.</span><span class="sxs-lookup"><span data-stu-id="13de1-122">hello following code example creates a container, then writes some of its property values tooa console window.</span></span>

```csharp
//Parse hello connection string for hello storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

//Create hello service client object for credentialed access toohello Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Create hello container if it does not already exist.
container.CreateIfNotExists();

// Fetch container properties and write out their values.
container.FetchAttributes();
Console.WriteLine("Properties for container {0}", container.StorageUri.PrimaryUri.ToString());
Console.WriteLine("LastModifiedUTC: {0}", container.Properties.LastModified.ToString());
Console.WriteLine("ETag: {0}", container.Properties.ETag);
Console.WriteLine();
```

## <a name="setting-and-retrieving-metadata"></a><span data-ttu-id="13de1-123">Ustawianie i pobieranie metadanych</span><span class="sxs-lookup"><span data-stu-id="13de1-123">Setting and retrieving metadata</span></span>
<span data-ttu-id="13de1-124">Metadane można określić jako pary nazwa wartość co najmniej jednego zasobu obiektów blob lub kontenera.</span><span class="sxs-lookup"><span data-stu-id="13de1-124">You can specify metadata as one or more name-value pairs on a blob or container resource.</span></span> <span data-ttu-id="13de1-125">metadane tooset dodać pary nazwa wartość toohello **metadanych** kolekcji hello zasobu, a następnie wywołaj hello **SetMetadata** hello toosave metody wartości toohello usługi.</span><span class="sxs-lookup"><span data-stu-id="13de1-125">tooset metadata, add name-value pairs toohello **Metadata** collection on hello resource, then call hello **SetMetadata** method toosave hello values toohello service.</span></span>

> [!NOTE]
> <span data-ttu-id="13de1-126">Nazwa Hello metadanych musi być zgodna toohello konwencje nazewnictwa dla identyfikatorów języka C#.</span><span class="sxs-lookup"><span data-stu-id="13de1-126">hello name of your metadata must conform toohello naming conventions for C# identifiers.</span></span>
>
>

<span data-ttu-id="13de1-127">Witaj Poniższy przykładowy kod ustawia metadane do kontenera.</span><span class="sxs-lookup"><span data-stu-id="13de1-127">hello following code example sets metadata on a container.</span></span> <span data-ttu-id="13de1-128">Jedna wartość jest ustawiona przy użyciu kolekcji hello **Dodaj** metody.</span><span class="sxs-lookup"><span data-stu-id="13de1-128">One value is set using hello collection's **Add** method.</span></span> <span data-ttu-id="13de1-129">Witaj innych wartość jest ustawiana za pomocą składni niejawne klucza i wartości.</span><span class="sxs-lookup"><span data-stu-id="13de1-129">hello other value is set using implicit key/value syntax.</span></span> <span data-ttu-id="13de1-130">Zarówno są prawidłowe.</span><span class="sxs-lookup"><span data-stu-id="13de1-130">Both are valid.</span></span>

```csharp
public static void AddContainerMetadata(CloudBlobContainer container)
{
    //Add some metadata toohello container.
    container.Metadata.Add("docType", "textDocuments");
    container.Metadata["category"] = "guidance";

    //Set hello container's metadata.
    container.SetMetadata();
}
```

<span data-ttu-id="13de1-131">metadane tooretrieve, wywołanie hello **FetchAttributes** metody na powitania toopopulate Twojego obiektów blob lub kontenera **metadanych** kolekcji, następnie odczytać wartości hello, jak pokazano w poniższym przykładzie hello.</span><span class="sxs-lookup"><span data-stu-id="13de1-131">tooretrieve metadata, call hello **FetchAttributes** method on your blob or container toopopulate hello **Metadata** collection, then read hello values, as shown in hello example below.</span></span>

```csharp
public static void ListContainerMetadata(CloudBlobContainer container)
{
    //Fetch container attributes in order toopopulate hello container's properties and metadata.
    container.FetchAttributes();

    //Enumerate hello container's metadata.
    Console.WriteLine("Container metadata:");
    foreach (var metadataItem in container.Metadata)
    {
        Console.WriteLine("\tKey: {0}", metadataItem.Key);
        Console.WriteLine("\tValue: {0}", metadataItem.Value);
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="13de1-132">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="13de1-132">Next steps</span></span>
* [<span data-ttu-id="13de1-133">Biblioteka klienta usługi Azure Storage dla odwołania .NET</span><span class="sxs-lookup"><span data-stu-id="13de1-133">Azure Storage Client Library for .NET reference</span></span>](/dotnet/api/?term=Microsoft.WindowsAzure.Storage)
* [<span data-ttu-id="13de1-134">Biblioteka klienta usługi Azure Storage dla pakietu NuGet programu .NET</span><span class="sxs-lookup"><span data-stu-id="13de1-134">Azure Storage Client Library for .NET NuGet package</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
