---
title: "Ustawianie i pobieranie metadanych w usłudze Azure Storage i właściwości obiektu | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 6af66607478c58874f00bcf017a35abfc37888df
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="set-and-retrieve-properties-and-metadata"></a><span data-ttu-id="79781-103">Ustawianie i pobieranie właściwości oraz metadanych</span><span class="sxs-lookup"><span data-stu-id="79781-103">Set and retrieve properties and metadata</span></span>

<span data-ttu-id="79781-104">W właściwości systemu pomocy technicznej usługi Azure Storage i metadanych zdefiniowanych przez użytkownika, oprócz danych, które zawierają obiekty.</span><span class="sxs-lookup"><span data-stu-id="79781-104">Objects in Azure Storage support system properties and user-defined metadata, in addition to the data they contain.</span></span> <span data-ttu-id="79781-105">W tym artykule omówiono zarządzanie właściwości systemu i użytkownika metadanych z [biblioteki klienta magazynu Azure dla platformy .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span><span class="sxs-lookup"><span data-stu-id="79781-105">This article discusses managing system properties and user-defined metadata with the [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span></span>

* <span data-ttu-id="79781-106">**Właściwości systemu**: właściwości systemu istnieje dla każdego zasobu magazynu.</span><span class="sxs-lookup"><span data-stu-id="79781-106">**System properties**: System properties exist on each storage resource.</span></span> <span data-ttu-id="79781-107">Niektóre z nich można odczytać lub ustawić, podczas gdy inne dotyczą tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="79781-107">Some of them can be read or set, while others are read-only.</span></span> <span data-ttu-id="79781-108">W obszarze obejmuje niektóre właściwości systemu odpowiadają niektórych standardowymi nagłówkami HTTP.</span><span class="sxs-lookup"><span data-stu-id="79781-108">Under the covers, some system properties correspond to certain standard HTTP headers.</span></span> <span data-ttu-id="79781-109">Biblioteka klienta magazynu Azure obsługuje są dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="79781-109">The Azure storage client library maintains these for you.</span></span>

* <span data-ttu-id="79781-110">**Zdefiniowane przez użytkownika metadanych**: metadane zdefiniowane przez użytkownika są metadane, które można określić dla danego zasobu w postaci pary nazwa wartość.</span><span class="sxs-lookup"><span data-stu-id="79781-110">**User-defined metadata**: User-defined metadata is metadata that you specify on a given resource in the form of a name-value pair.</span></span> <span data-ttu-id="79781-111">Metadanych umożliwiają przechowywanie dodatkowe wartości zasobów magazynu.</span><span class="sxs-lookup"><span data-stu-id="79781-111">You can use metadata to store additional values with a storage resource.</span></span> <span data-ttu-id="79781-112">Wartości te dodatkowe metadane służą wyłącznie do własnych, a nie wpływają na zachowanie zasobu.</span><span class="sxs-lookup"><span data-stu-id="79781-112">These additional metadata values are for your own purposes only, and do not affect how the resource behaves.</span></span>

<span data-ttu-id="79781-113">Podczas pobierania wartości właściwości i metadanych dla zasobu magazynu jest procesem dwuetapowym.</span><span class="sxs-lookup"><span data-stu-id="79781-113">Retrieving property and metadata values for a storage resource is a two-step process.</span></span> <span data-ttu-id="79781-114">Przed możesz przeczytać te wartości, użytkownik musi jawnie pobrać je przez wywołanie metody **FetchAttributes** metody.</span><span class="sxs-lookup"><span data-stu-id="79781-114">Before you can read these values, you must explicitly fetch them by calling the **FetchAttributes** method.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="79781-115">Wartości właściwości i metadanych dla zasobów magazynu nie są wypełniane, chyba że wywoływanie jednego z **FetchAttributes** metody.</span><span class="sxs-lookup"><span data-stu-id="79781-115">Property and metadata values for a storage resource are not populated unless you call one of the **FetchAttributes** methods.</span></span>
>
> <span data-ttu-id="79781-116">Zostanie wyświetlony `400 Bad Request` Jeśli wszystkie pary nazwa/wartość zawiera znaki spoza zestawu ASCII.</span><span class="sxs-lookup"><span data-stu-id="79781-116">You will receive a `400 Bad Request` if any name/value pairs contain non-ASCII characters.</span></span> <span data-ttu-id="79781-117">Pary nazwa/wartość metadanych są prawidłowe nagłówków HTTP, a więc muszą spełniać wszystkie ograniczenia dotyczące nagłówków HTTP.</span><span class="sxs-lookup"><span data-stu-id="79781-117">Metadata name/value pairs are valid HTTP headers, and so must adhere to all restrictions governing HTTP headers.</span></span> <span data-ttu-id="79781-118">Dlatego zaleca się użycie kodowania adresu URL lub kodowania Base64 dla nazwy i wartości zawierające znaki spoza zestawu ASCII.</span><span class="sxs-lookup"><span data-stu-id="79781-118">It is therefore recommended that you use URL encoding or Base64 encoding for names and values containing non-ASCII characters.</span></span>
>

## <a name="setting-and-retrieving-properties"></a><span data-ttu-id="79781-119">Ustawiania i pobierania właściwości</span><span class="sxs-lookup"><span data-stu-id="79781-119">Setting and retrieving properties</span></span>
<span data-ttu-id="79781-120">Aby pobrać wartości właściwości, należy wywołać **FetchAttributes** metody na obiekt blob lub kontener, aby wypełnić właściwości, następnie odczytać wartości.</span><span class="sxs-lookup"><span data-stu-id="79781-120">To retrieve property values, call the **FetchAttributes** method on your blob or container to populate the properties, then read the values.</span></span>

<span data-ttu-id="79781-121">Aby ustawić właściwości dla obiektu, określ właściwość value, a następnie wywołaj **SetProperties** metody.</span><span class="sxs-lookup"><span data-stu-id="79781-121">To set properties on an object, specify the property value, then call the **SetProperties** method.</span></span>

<span data-ttu-id="79781-122">Poniższy przykład kodu tworzy kontener, a następnie zapisuje niektóre z jej wartości właściwości w oknie konsoli.</span><span class="sxs-lookup"><span data-stu-id="79781-122">The following code example creates a container, then writes some of its property values to a console window.</span></span>

```csharp
//Parse the connection string for the storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

//Create the service client object for credentialed access to the Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve a reference to a container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Create the container if it does not already exist.
container.CreateIfNotExists();

// Fetch container properties and write out their values.
container.FetchAttributes();
Console.WriteLine("Properties for container {0}", container.StorageUri.PrimaryUri.ToString());
Console.WriteLine("LastModifiedUTC: {0}", container.Properties.LastModified.ToString());
Console.WriteLine("ETag: {0}", container.Properties.ETag);
Console.WriteLine();
```

## <a name="setting-and-retrieving-metadata"></a><span data-ttu-id="79781-123">Ustawianie i pobieranie metadanych</span><span class="sxs-lookup"><span data-stu-id="79781-123">Setting and retrieving metadata</span></span>
<span data-ttu-id="79781-124">Metadane można określić jako pary nazwa wartość co najmniej jednego zasobu obiektów blob lub kontenera.</span><span class="sxs-lookup"><span data-stu-id="79781-124">You can specify metadata as one or more name-value pairs on a blob or container resource.</span></span> <span data-ttu-id="79781-125">Aby ustawić metadane, należy dodać pary nazwa wartość do **metadanych** kolekcji na zasobie, następnie wywołaj **SetMetadata** metody, aby zapisać wartości do usługi.</span><span class="sxs-lookup"><span data-stu-id="79781-125">To set metadata, add name-value pairs to the **Metadata** collection on the resource, then call the **SetMetadata** method to save the values to the service.</span></span>

> [!NOTE]
> <span data-ttu-id="79781-126">Nazwa metadanych musi być zgodna z konwencji nazewnictwa dla identyfikatorów języka C#.</span><span class="sxs-lookup"><span data-stu-id="79781-126">The name of your metadata must conform to the naming conventions for C# identifiers.</span></span>
>
>

<span data-ttu-id="79781-127">Poniższy przykład kodu Ustawia metadane do kontenera.</span><span class="sxs-lookup"><span data-stu-id="79781-127">The following code example sets metadata on a container.</span></span> <span data-ttu-id="79781-128">Jedna wartość jest ustawiona przy użyciu kolekcji **Dodaj** metody.</span><span class="sxs-lookup"><span data-stu-id="79781-128">One value is set using the collection's **Add** method.</span></span> <span data-ttu-id="79781-129">Inne ma wartość przy użyciu składni niejawne klucza i wartości.</span><span class="sxs-lookup"><span data-stu-id="79781-129">The other value is set using implicit key/value syntax.</span></span> <span data-ttu-id="79781-130">Zarówno są prawidłowe.</span><span class="sxs-lookup"><span data-stu-id="79781-130">Both are valid.</span></span>

```csharp
public static void AddContainerMetadata(CloudBlobContainer container)
{
    //Add some metadata to the container.
    container.Metadata.Add("docType", "textDocuments");
    container.Metadata["category"] = "guidance";

    //Set the container's metadata.
    container.SetMetadata();
}
```

<span data-ttu-id="79781-131">Aby pobrać metadane, należy wywołać **FetchAttributes** metody na obiekt blob lub kontener, aby wypełnić **metadanych** kolekcji, następnie odczytać wartości, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="79781-131">To retrieve metadata, call the **FetchAttributes** method on your blob or container to populate the **Metadata** collection, then read the values, as shown in the example below.</span></span>

```csharp
public static void ListContainerMetadata(CloudBlobContainer container)
{
    //Fetch container attributes in order to populate the container's properties and metadata.
    container.FetchAttributes();

    //Enumerate the container's metadata.
    Console.WriteLine("Container metadata:");
    foreach (var metadataItem in container.Metadata)
    {
        Console.WriteLine("\tKey: {0}", metadataItem.Key);
        Console.WriteLine("\tValue: {0}", metadataItem.Value);
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="79781-132">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="79781-132">Next steps</span></span>
* [<span data-ttu-id="79781-133">Biblioteka klienta usługi Azure Storage dla odwołania .NET</span><span class="sxs-lookup"><span data-stu-id="79781-133">Azure Storage Client Library for .NET reference</span></span>](/dotnet/api/?term=Microsoft.WindowsAzure.Storage)
* [<span data-ttu-id="79781-134">Biblioteka klienta usługi Azure Storage dla pakietu NuGet programu .NET</span><span class="sxs-lookup"><span data-stu-id="79781-134">Azure Storage Client Library for .NET NuGet package</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
