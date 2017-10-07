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
# <a name="set-and-retrieve-properties-and-metadata"></a>Ustawianie i pobieranie właściwości oraz metadanych

Obiekty w właściwości systemu pomocy technicznej usługi Azure Storage i metadanych zdefiniowanych przez użytkownika, oprócz toohello nich danych. W tym artykule omówiono zarządzanie właściwości systemu i użytkownika metadanych z hello [biblioteki klienta magazynu Azure dla platformy .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).

* **Właściwości systemu**: właściwości systemu istnieje dla każdego zasobu magazynu. Niektóre z nich można odczytać lub ustawić, podczas gdy inne dotyczą tylko do odczytu. W obszarze obejmuje hello niektórych właściwości systemu odpowiada toocertain standardowymi nagłówkami HTTP. Biblioteka klienta magazynu Azure Hello przechowuje są dla Ciebie.

* **Zdefiniowane przez użytkownika metadanych**: metadane zdefiniowane przez użytkownika są metadane, które można określić dla danego zasobu w postaci hello pary nazwa wartość. Możesz użyć wartości dodatkowe metadane toostore zasobów magazynu. Wartości te dodatkowe metadane służą wyłącznie do własnych, a nie wpływają na zachowanie hello zasobów.

Podczas pobierania wartości właściwości i metadanych dla zasobu magazynu jest procesem dwuetapowym. Przed możesz przeczytać te wartości, użytkownik musi jawnie pobrać je przez wywołanie hello **FetchAttributes** metody.

> [!IMPORTANT]
> Wartości właściwości i metadanych dla zasobów magazynu nie są wypełniane, chyba że należy wywołać hello **FetchAttributes** metody.
>
> Zostanie wyświetlony `400 Bad Request` Jeśli wszystkie pary nazwa/wartość zawiera znaki spoza zestawu ASCII. Pary nazwa/wartość metadanych są prawidłowe nagłówków HTTP i dlatego musi być zgodne tooall ograniczenia dotyczące nagłówków HTTP. Dlatego zaleca się użycie kodowania adresu URL lub kodowania Base64 dla nazwy i wartości zawierające znaki spoza zestawu ASCII.
>

## <a name="setting-and-retrieving-properties"></a>Ustawiania i pobierania właściwości
wartości właściwości tooretrieve, wywołanie hello **FetchAttributes** metody dla obiekt blob lub kontener toopopulate hello właściwości, następnie odczytywane hello wartości.

tooset właściwości w obiekcie, określ wartość właściwości hello, a następnie wywołaj hello **SetProperties** metody.

Witaj poniższy przykład kodu tworzy kontener, a następnie zapisuje niektórych okna konsoli tooa wartości właściwości.

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

## <a name="setting-and-retrieving-metadata"></a>Ustawianie i pobieranie metadanych
Metadane można określić jako pary nazwa wartość co najmniej jednego zasobu obiektów blob lub kontenera. metadane tooset dodać pary nazwa wartość toohello **metadanych** kolekcji hello zasobu, a następnie wywołaj hello **SetMetadata** hello toosave metody wartości toohello usługi.

> [!NOTE]
> Nazwa Hello metadanych musi być zgodna toohello konwencje nazewnictwa dla identyfikatorów języka C#.
>
>

Witaj Poniższy przykładowy kod ustawia metadane do kontenera. Jedna wartość jest ustawiona przy użyciu kolekcji hello **Dodaj** metody. Witaj innych wartość jest ustawiana za pomocą składni niejawne klucza i wartości. Zarówno są prawidłowe.

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

metadane tooretrieve, wywołanie hello **FetchAttributes** metody na powitania toopopulate Twojego obiektów blob lub kontenera **metadanych** kolekcji, następnie odczytać wartości hello, jak pokazano w poniższym przykładzie hello.

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

## <a name="next-steps"></a>Następne kroki
* [Biblioteka klienta usługi Azure Storage dla odwołania .NET](/dotnet/api/?term=Microsoft.WindowsAzure.Storage)
* [Biblioteka klienta usługi Azure Storage dla pakietu NuGet programu .NET](https://www.nuget.org/packages/WindowsAzure.Storage/)
