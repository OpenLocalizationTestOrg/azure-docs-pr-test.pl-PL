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
# <a name="set-and-retrieve-properties-and-metadata"></a>Ustawianie i pobieranie właściwości oraz metadanych

W właściwości systemu pomocy technicznej usługi Azure Storage i metadanych zdefiniowanych przez użytkownika, oprócz danych, które zawierają obiekty. W tym artykule omówiono zarządzanie właściwości systemu i użytkownika metadanych z [biblioteki klienta magazynu Azure dla platformy .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).

* **Właściwości systemu**: właściwości systemu istnieje dla każdego zasobu magazynu. Niektóre z nich można odczytać lub ustawić, podczas gdy inne dotyczą tylko do odczytu. W obszarze obejmuje niektóre właściwości systemu odpowiadają niektórych standardowymi nagłówkami HTTP. Biblioteka klienta magazynu Azure obsługuje są dla Ciebie.

* **Zdefiniowane przez użytkownika metadanych**: metadane zdefiniowane przez użytkownika są metadane, które można określić dla danego zasobu w postaci pary nazwa wartość. Metadanych umożliwiają przechowywanie dodatkowe wartości zasobów magazynu. Wartości te dodatkowe metadane służą wyłącznie do własnych, a nie wpływają na zachowanie zasobu.

Podczas pobierania wartości właściwości i metadanych dla zasobu magazynu jest procesem dwuetapowym. Przed możesz przeczytać te wartości, użytkownik musi jawnie pobrać je przez wywołanie metody **FetchAttributes** metody.

> [!IMPORTANT]
> Wartości właściwości i metadanych dla zasobów magazynu nie są wypełniane, chyba że wywoływanie jednego z **FetchAttributes** metody.
>
> Zostanie wyświetlony `400 Bad Request` Jeśli wszystkie pary nazwa/wartość zawiera znaki spoza zestawu ASCII. Pary nazwa/wartość metadanych są prawidłowe nagłówków HTTP, a więc muszą spełniać wszystkie ograniczenia dotyczące nagłówków HTTP. Dlatego zaleca się użycie kodowania adresu URL lub kodowania Base64 dla nazwy i wartości zawierające znaki spoza zestawu ASCII.
>

## <a name="setting-and-retrieving-properties"></a>Ustawiania i pobierania właściwości
Aby pobrać wartości właściwości, należy wywołać **FetchAttributes** metody na obiekt blob lub kontener, aby wypełnić właściwości, następnie odczytać wartości.

Aby ustawić właściwości dla obiektu, określ właściwość value, a następnie wywołaj **SetProperties** metody.

Poniższy przykład kodu tworzy kontener, a następnie zapisuje niektóre z jej wartości właściwości w oknie konsoli.

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

## <a name="setting-and-retrieving-metadata"></a>Ustawianie i pobieranie metadanych
Metadane można określić jako pary nazwa wartość co najmniej jednego zasobu obiektów blob lub kontenera. Aby ustawić metadane, należy dodać pary nazwa wartość do **metadanych** kolekcji na zasobie, następnie wywołaj **SetMetadata** metody, aby zapisać wartości do usługi.

> [!NOTE]
> Nazwa metadanych musi być zgodna z konwencji nazewnictwa dla identyfikatorów języka C#.
>
>

Poniższy przykład kodu Ustawia metadane do kontenera. Jedna wartość jest ustawiona przy użyciu kolekcji **Dodaj** metody. Inne ma wartość przy użyciu składni niejawne klucza i wartości. Zarówno są prawidłowe.

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

Aby pobrać metadane, należy wywołać **FetchAttributes** metody na obiekt blob lub kontener, aby wypełnić **metadanych** kolekcji, następnie odczytać wartości, jak pokazano w poniższym przykładzie.

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

## <a name="next-steps"></a>Następne kroki
* [Biblioteka klienta usługi Azure Storage dla odwołania .NET](/dotnet/api/?term=Microsoft.WindowsAzure.Storage)
* [Biblioteka klienta usługi Azure Storage dla pakietu NuGet programu .NET](https://www.nuget.org/packages/WindowsAzure.Storage/)
