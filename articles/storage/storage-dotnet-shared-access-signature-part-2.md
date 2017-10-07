---
title: "aaaCreate i używanie sygnatury dostępu współdzielonego (SAS) z magazynu obiektów Blob platformy Azure | Dokumentacja firmy Microsoft"
description: "Ten samouczek pokazuje, jak toocreate udostępnionych sygnatur dostępu do użycia z magazynem obiektów Blob i jak tooconsume ich w aplikacji klienta."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 491e0b3c-76d4-4149-9a80-bbbd683b1f3e
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/15/2017
ms.author: marsma
ms.openlocfilehash: 629f5c0aee3f41115a0d514a2010d8cc0187126d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="shared-access-signatures-part-2-create-and-use-a-sas-with-blob-storage"></a>Udostępnione sygnatur dostępu, część 2: Tworzenie i sygnatury dostępu Współdzielonego za pomocą magazynu obiektów Blob

[Część 1](storage-dotnet-shared-access-signature-part-1.md) tego samouczka przedstawione udostępnionym sygnatur dostępu (SAS) i wyjaśniono najlepsze rozwiązania dotyczące korzystania z nich. Część 2 pokazuje, jak toogenerate i skorzystaj z udostępnionego dostępu podpisów z magazynem obiektów Blob. Witaj przykłady są napisane w języku C# i użyj hello biblioteki klienta magazynu Azure dla platformy .NET. Przykłady Hello w tym samouczku:

* Generowanie sygnatury dostępu współdzielonego w kontenerze
* Generowanie sygnatury dostępu współdzielonego na obiektu blob
* Przechowywane dostępu do tworzenia podpisów toomanage zasad na zasoby kontenera
* Testowanie sygnatur dostępu hello udostępnionych w aplikacji klienta

## <a name="about-this-tutorial"></a>Informacje o tym samouczku
W tym samouczku utworzymy dwóch aplikacji konsoli, które przedstawiają tworzenia i używania sygnatur dostępu współdzielonego dla kontenerów i obiektów blob:

**1 aplikacja**: hello aplikacji do zarządzania. Generuje sygnaturę dostępu współdzielonego dla kontenera i obiektu blob. Zawiera klucz dostępu do konta magazynu hello w kodzie źródłowym.

**Aplikacja 2**: hello aplikacji klienckiej. Uzyskuje dostęp do kontenera obiektów blob zasobów i za pomocą sygnatur dostępu hello udostępnionych utworzone za pomocą hello pierwszej aplikacji. Używa tylko hello dostępu współdzielonego podpisy tooaccess kontenera i zasobów obiektów blob — działa *nie* obejmują klucz dostępu do konta magazynu hello.

## <a name="part-1-create-a-console-application-toogenerate-shared-access-signatures"></a>Część 1: Tworzenie podpisów dostęp do udostępnionych toogenerate dla aplikacji w konsoli
Najpierw upewnij się, że masz hello biblioteki klienta magazynu Azure dla programu .NET zainstalowane. Można zainstalować hello [pakietu NuGet](http://nuget.org/packages/WindowsAzure.Storage/ "pakietu NuGet") zawierający zestawy aktualną hello powitania klienta biblioteki. Jest to zalecana metoda sprawdzeniu, czy masz najnowsze poprawki hello hello. Możesz również pobrać jako część hello najnowszą wersję hello powitania klienta biblioteki [zestawu Azure SDK dla platformy .NET](https://azure.microsoft.com/downloads/).

W programie Visual Studio Utwórz nową aplikację konsoli systemu Windows i nadaj mu nazwę **GenerateSharedAccessSignatures**. Dodaj odwołania do zbyt[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) i [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/) przy użyciu jednej z następujących podejść hello:

* Użyj hello [Menedżera pakietów NuGet](https://docs.nuget.org/consume/installing-nuget) w programie Visual Studio. Wybierz **projektu** > **Zarządzaj pakietami NuGet**, Wyszukaj w trybie online dla każdego pakietu (Microsoft.WindowsAzure.ConfigurationManager i WindowsAzure.Storage) i zainstaluj je.
* Alternatywnie zlokalizować te zestawy w instalacji hello Azure SDK i Dodaj toothem odwołania:
  * Microsoft.WindowsAzure.Configuration.dll
  * Microsoft.WindowsAzure.Storage.dll

U góry pliku Program.cs hello hello, Dodaj następujące hello **przy użyciu** dyrektywy:

```csharp
using System.IO;
using Microsoft.Azure;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

Edytowanie pliku app.config hello tak, aby zawierał ustawienia konfiguracji z parametrów połączenia, które wskazuje tooyour konta magazynu. Plik app.config powinien wyglądać podobnie toothis, co:

```xml
<configuration>
  <startup>
    <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2" />
  </startup>
  <appSettings>
    <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey"/>
  </appSettings>
</configuration>
```

### <a name="generate-a-shared-access-signature-uri-for-a-container"></a>Generuj identyfikator URI sygnatury dostępu współdzielonego dla kontenera
toobegin z, możemy dodać toogenerate metody sygnatury dostępu współdzielonego na nowy kontener. W takim przypadku hello podpis nie jest skojarzone z zasadami dostępu przechowywane, więc prowadzi hello URI hello informacje wskazujące uprawnienia hello i godzina wygaśnięcia przyznaje.

Najpierw należy dodać kodu toohello **Main()** tooauthenticate metody dostępu konta magazynu tooyour i utworzyć nowy kontener:

```csharp
static void Main(string[] args)
{
    //Parse hello connection string and return a reference toohello storage account.
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));

    //Create hello blob client object.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    //Get a reference tooa container toouse for hello sample code, and create it if it does not exist.
    CloudBlobContainer container = blobClient.GetContainerReference("sascontainer");
    container.CreateIfNotExists();

    //Insert calls toohello methods created below here...

    //Require user input before closing hello console window.
    Console.ReadLine();
}
```

Następnie dodaj metodę hello sygnatury dostępu współdzielonego dla kontenera hello generuje i zwraca podpis hello identyfikatora URI:

```csharp
static string GetContainerSasUri(CloudBlobContainer container)
{
    //Set hello expiry time and permissions for hello container.
    //In this case no start time is specified, so hello shared access signature becomes valid immediately.
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();
    sasConstraints.SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.List | SharedAccessBlobPermissions.Write;

    //Generate hello shared access signature on hello container, setting hello constraints directly on hello signature.
    string sasContainerToken = container.GetSharedAccessSignature(sasConstraints);

    //Return hello URI string for hello container, including hello SAS token.
    return container.Uri + sasContainerToken;
}
```

Dodaj następujące wiersze u dołu hello hello hello **Main()** metody, zanim hello wywołać zbyt**Console.ReadLine()**, toocall **GetContainerSasUri()** i zapisu hello Podpis okna konsoli toohello identyfikatora URI:

```csharp
//Generate a SAS URI for hello container, without a stored access policy.
Console.WriteLine("Container SAS URI: " + GetContainerSasUri(container));
Console.WriteLine();
```

Kompilowanie i uruchamianie toooutput hello sygnatury dostępu współdzielonego identyfikatora URI dla hello nowego kontenera. Hello identyfikator URI będzie podobne toohello następujące czynności:

```
https://storageaccount.blob.core.windows.net/sascontainer?sv=2012-02-12&se=2013-04-13T00%3A12%3A08Z&sr=c&sp=wl&sig=t%2BbzU9%2B7ry4okULN9S0wst%2F8MCUhTjrHyV9rDNLSe8g%3D
```

Po uruchomieniu kodu hello hello sygnatury dostępu współdzielonego, utworzenia kontenera hello będzie obowiązywał dla hello następne 24 godziny. Podpis Hello przyznaje klientowi uprawnienia toolist BLOB w kontenerze hello i nowy kontener obiektów blob toohello toowrite.

### <a name="generate-a-shared-access-signature-uri-for-a-blob"></a>Generowanie sygnatury dostępu współdzielonego identyfikatora URI dla obiektu blob
Następnie możemy zapisać podobny kod toocreate nowych obiektów blob w kontenerze hello i Generowanie sygnatury dostępu współdzielonego dla niego. Ta sygnatura dostępu współdzielonego nie jest skojarzone z zasadami dostępu przechowywane, więc zawiera czas rozpoczęcia hello, czas wygaśnięcia i informacji o uprawnieniach hello identyfikatora URI.

Dodanie nowej metody, która tworzy nowy obiekt blob i zapisuje niektórych tooit tekstu, a następnie generuje sygnaturę dostępu współdzielonego i zwraca podpis hello identyfikatora URI:

```csharp
static string GetBlobSasUri(CloudBlobContainer container)
{
    //Get a reference tooa blob within hello container.
    CloudBlockBlob blob = container.GetBlockBlobReference("sasblob.txt");

    //Upload text toohello blob. If hello blob does not yet exist, it will be created.
    //If hello blob does exist, its existing content will be overwritten.
    string blobContent = "This blob will be accessible tooclients via a shared access signature (SAS).";
    blob.UploadText(blobContent);

    //Set hello expiry time and permissions for hello blob.
    //In this case, hello start time is specified as a few minutes in hello past, toomitigate clock skew.
    //hello shared access signature will be valid immediately.
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();
    sasConstraints.SharedAccessStartTime = DateTimeOffset.UtcNow.AddMinutes(-5);
    sasConstraints.SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Write;

    //Generate hello shared access signature on hello blob, setting hello constraints directly on hello signature.
    string sasBlobToken = blob.GetSharedAccessSignature(sasConstraints);

    //Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```

U dołu hello hello **Main()** metody, Dodaj następujące wiersze toocall hello **GetBlobSasUri()**, zanim hello wywołać zbyt**Console.ReadLine()**i zapisu hello udostępnionych toohello okna konsoli Access podpisu identyfikatora URI:

```csharp
//Generate a SAS URI for a blob within hello container, without a stored access policy.
Console.WriteLine("Blob SAS URI: " + GetBlobSasUri(container));
Console.WriteLine();
```

Kompilowanie i uruchamianie toooutput hello sygnatury dostępu współdzielonego URI hello nowego obiektu blob. Hello identyfikator URI będzie podobne toohello następujące czynności:

```
https://storageaccount.blob.core.windows.net/sascontainer/sasblob.txt?sv=2012-02-12&st=2013-04-12T23%3A37%3A08Z&se=2013-04-13T00%3A12%3A08Z&sr=b&sp=rw&sig=dF2064yHtc8RusQLvkQFPItYdeOz3zR8zHsDMBi4S30%3D
```

### <a name="create-a-stored-access-policy-on-hello-container"></a>Tworzenie zasad dostępu przechowywanych na powitania kontenera
Teraz Utwórzmy zasad dostępu do przechowywanych na powitania kontenera, który będzie definiował hello ograniczenia żadnych sygnatur dostępu współdzielonego, które są skojarzone z nim.

W poprzednich przykładach hello możemy określony czas rozpoczęcia hello (jawnie ani niejawnie), czas wygaśnięcia hello i uprawnień hello hello udostępnionych sygnatury dostępu URI sam. W następujących przykładach hello możemy określić zasady dostępu hello przechowywane, a nie na powitania sygnatury dostępu współdzielonego. Toochange tych warunków ograniczających bez ponownego wystawienia hello udostępnionych nam wykonanie tak umożliwia dostęp do podpisu.

Jest możliwe toohave jednego lub więcej ograniczeń hello na powitania sygnatury dostępu współdzielonego i pozostałej hello hello przechowywane zasady dostępu. Jednak można określić tylko hello czas rozpoczęcia, czas wygaśnięcia i uprawnień w jednym miejscu lub hello innych. Na przykład nie można określić uprawnienia na powitania sygnatury dostępu współdzielonego i określ je w zasadach dostępu hello przechowywane.

Podczas dodawania kontenera tooa zasad dostępu do przechowywanych musi uzyskać uprawnienia istniejącego kontenera hello, Dodaj hello nowej zasady dostępu, a następnie ustaw uprawnienia hello kontenera.

Dodaj nową metodę tworzy nową zasadę przechowywanych dostępu do kontenera i zwraca nazwę hello hello zasad:

```csharp
static void CreateSharedAccessPolicy(CloudBlobClient blobClient, CloudBlobContainer container,
    string policyName)
{
    //Get hello container's existing permissions.
    BlobContainerPermissions permissions = container.GetPermissions();

    //Create a new shared access policy and define its constraints.
    SharedAccessBlobPolicy sharedPolicy = new SharedAccessBlobPolicy()
    {
        SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24),
        Permissions = SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.List | SharedAccessBlobPermissions.Read
    };

    //Add hello new policy toohello container's permissions, and set hello container's permissions.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    container.SetPermissions(permissions);
}
```

U dołu hello hello **Main()** metody, zanim hello wywołać zbyt**Console.ReadLine()**Dodaj hello następujące wiersze toofirst wyczyść wszystkie istniejące zasady dostępu, a następnie wywołać hello  **CreateSharedAccessPolicy()** metody:

```csharp
//Clear any existing access policies on container.
BlobContainerPermissions perms = container.GetPermissions();
perms.SharedAccessPolicies.Clear();
container.SetPermissions(perms);

//Create a new access policy on hello container, which may be optionally used tooprovide constraints for
//shared access signatures on hello container and hello blob.
string sharedAccessPolicyName = "tutorialpolicy";
CreateSharedAccessPolicy(blobClient, container, sharedAccessPolicyName);
```

Po wyczyszczeniu hello zasady dostępu do kontenera, należy najpierw pobrać kontenera hello istniejące uprawnienia, a następnie wyczyść hello uprawnienia, a następnie ponownie ustawić uprawnienia hello.

### <a name="generate-a-shared-access-signature-uri-on-hello-container-that-uses-an-access-policy"></a>Generowanie sygnatury dostępu współdzielonego identyfikatora URI w kontenerze hello, która używa zasad dostępu
Następnie utworzymy innej sygnatury dostępu współdzielonego dla kontenera hello, w którym utworzono wcześniej, ale teraz powiązane hello podpisu z zasad dostępu hello przechowywane utworzone w poprzednim przykładzie hello.

Dodaj nowe toogenerate metody innej sygnatury dostępu współdzielonego dla kontenera hello:

```csharp
static string GetContainerSasUriWithPolicy(CloudBlobContainer container, string policyName)
{
    //Generate hello shared access signature on hello container. In this case, all of hello constraints for the
    //shared access signature are specified on hello stored access policy.
    string sasContainerToken = container.GetSharedAccessSignature(null, policyName);

    //Return hello URI string for hello container, including hello SAS token.
    return container.Uri + sasContainerToken;
}
```

U dołu hello hello **Main()** metody, zanim hello wywołać zbyt**Console.ReadLine()**, Dodaj następujące wiersze toocall hello hello **GetContainerSasUriWithPolicy** — metoda :

```csharp
//Generate a SAS URI for hello container, using a stored access policy tooset constraints on hello SAS.
Console.WriteLine("Container SAS URI using stored access policy: " + GetContainerSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

### <a name="generate-a-shared-access-signature-uri-on-hello-blob-that-uses-an-access-policy"></a>Wygenerować udostępnionego dostępu podpisu identyfikator URI na powitania obiektów Blob, że używa zasad dostępu
Na koniec możemy dodać podobne toocreate — metoda innego obiektu blob i Generowanie sygnatury dostępu współdzielonego, skojarzone z zasadami dostępu przechowywane.

Dodaj nowy toocreate metody obiektu blob i Generowanie sygnatury dostępu współdzielonego:

```csharp
static string GetBlobSasUriWithPolicy(CloudBlobContainer container, string policyName)
{
    //Get a reference tooa blob within hello container.
    CloudBlockBlob blob = container.GetBlockBlobReference("sasblobpolicy.txt");

    //Upload text toohello blob. If hello blob does not yet exist, it will be created.
    //If hello blob does exist, its existing content will be overwritten.
    string blobContent = "This blob will be accessible tooclients via a shared access signature. " +
    "A stored access policy defines hello constraints for hello signature.";
    MemoryStream ms = new MemoryStream(Encoding.UTF8.GetBytes(blobContent));
    ms.Position = 0;
    using (ms)
    {
        blob.UploadFromStream(ms);
    }

    //Generate hello shared access signature on hello blob.
    string sasBlobToken = blob.GetSharedAccessSignature(null, policyName);

    //Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```

U dołu hello hello **Main()** metody, zanim hello wywołać zbyt**Console.ReadLine()**, Dodaj następujące wiersze toocall hello hello **GetBlobSasUriWithPolicy** metody:

```csharp
//Generate a SAS URI for a blob within hello container, using a stored access policy tooset constraints on hello SAS.
Console.WriteLine("Blob SAS URI using stored access policy: " + GetBlobSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

Witaj **Main()** metoda powinna wyglądać tak jak to w całości. Uruchom go sygnatury dostępu współdzielonego hello toowrite okna konsoli toohello identyfikatory URI, a następnie skopiuj i wklej je do pliku tekstowego do użycia w hello drugiej części tego samouczka.

```csharp
static void Main(string[] args)
{
    //Parse hello connection string and return a reference toohello storage account.
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));

    //Create hello blob client object.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    //Get a reference tooa container toouse for hello sample code, and create it if it does not exist.
    CloudBlobContainer container = blobClient.GetContainerReference("sascontainer");
    container.CreateIfNotExists();

    //Generate a SAS URI for hello container, without a stored access policy.
    Console.WriteLine("Container SAS URI: " + GetContainerSasUri(container));
    Console.WriteLine();

    //Generate a SAS URI for a blob within hello container, without a stored access policy.
    Console.WriteLine("Blob SAS URI: " + GetBlobSasUri(container));
    Console.WriteLine();

    //Clear any existing access policies on container.
    BlobContainerPermissions perms = container.GetPermissions();
    perms.SharedAccessPolicies.Clear();
    container.SetPermissions(perms);

    //Create a new access policy on hello container, which may be optionally used tooprovide constraints for
    //shared access signatures on hello container and hello blob.
    string sharedAccessPolicyName = "tutorialpolicy";
    CreateSharedAccessPolicy(blobClient, container, sharedAccessPolicyName);

    //Generate a SAS URI for hello container, using a stored access policy tooset constraints on hello SAS.
    Console.WriteLine("Container SAS URI using stored access policy: " + GetContainerSasUriWithPolicy(container, sharedAccessPolicyName));
    Console.WriteLine();

    //Generate a SAS URI for a blob within hello container, using a stored access policy tooset constraints on hello SAS.
    Console.WriteLine("Blob SAS URI using stored access policy: " + GetBlobSasUriWithPolicy(container, sharedAccessPolicyName));
    Console.WriteLine();

    Console.ReadLine();
}
```

Po uruchomieniu aplikacji konsoli GenerateSharedAccessSignatures hello, zostanie wyświetlone dane wyjściowe podobne toohello poniżej. Są to sygnatur dostępu hello udostępnionych używanych w część 2 samouczka hello.

```
Container SAS URI: https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=pFlEZD%2F6sJTNLxD%2FQ26Hh85j%2FzYPxZav6mP1KJwnvJE%3D&se=2017-05-16T16%3A16%3A47Z&sp=wl

Blob SAS URI: https://storagesample.blob.core.windows.net/sascontainer/sasblob.txt?sv=2016-05-31&sr=b&sig=%2FiBWAZbXESzCMvRcm7JwJBK0gT0BtPSWEq4pRwmlBRI%3D&st=2017-05-15T16%3A11%3A48Z&se=2017-05-16T16%3A16%3A48Z&sp=rw

Container SAS URI using stored access policy: https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&si=tutorialpolicy&sig=aMb6rKDvvpfiGVsZI2rCmyUra6ZPpq%2BZ%2FLyTgAeec%2Bk%3D

Blob SAS URI using stored access policy: https://storagesample.blob.core.windows.net/sascontainer/sasblobpolicy.txt?sv=2016-05-31&sr=b&si=tutorialpolicy&sig=%2FkTWkT23SS45%2FoF4bK2mqXkN%2BPKs%2FyHuzkfQ4GFoZVU%3D
```

## <a name="part-2-create-a-console-application-tootest-hello-shared-access-signatures"></a>Część 2: Utworzyć dostępu hello udostępnionych tootest aplikacji konsoli podpisów
Witaj tootest udostępnione utworzone w poprzednich przykładach hello sygnatur dostępu, utworzymy drugi aplikacja konsolowa, która używa hello podpisy tooperform operacje na powitania kontenera i obiektu blob.

> [!NOTE]
> Jeśli od ukończone hello pierwszej części samouczka hello minęło ponad 24 godzin, podpisy hello, wygenerowanego nie będzie już prawidłowy. W takim przypadku należy uruchomić kod hello w hello pierwszy toogenerate aplikacji konsoli podpisów świeże dostępu współdzielonego do użycia w drugiej części samouczka hello hello.
>

W programie Visual Studio Utwórz nową aplikację konsoli systemu Windows i nadaj mu nazwę **ConsumeSharedAccessSignatures**. Dodaj odwołania do zbyt[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) i [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/), tak jak poprzednio.

U góry pliku Program.cs hello hello, Dodaj następujące hello **przy użyciu** dyrektywy:

```csharp
using System.IO;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

W treści hello hello **Main()** metody, Dodaj powitania po stałe typu string, zmiana ich wartości sygnatur dostępu toohello udostępnionych wygenerowanych w hello samouczek, część 1.

```csharp
static void Main(string[] args)
{
    const string containerSAS = "<your container SAS>";
    const string blobSAS = "<your blob SAS>";
    const string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    const string blobSASWithAccessPolicy = "<your blob SAS with access policy>";
}
```

### <a name="add-a-method-tootry-container-operations-using-a-shared-access-signature"></a>Dodaj metodę operacji kontenera tootry przy użyciu sygnatury dostępu współdzielonego
Następnie dodaj metodę, która sprawdza niektóre operacje kontenera przy użyciu sygnatury dostępu współdzielonego dla kontenera hello. sygnatury dostępu współdzielonego Hello jest używany tooreturn kontener toohello odwołanie do uwierzytelniania dostępu do kontenera toohello podpisu hello wyłącznie w oparciu.

Dodaj następujące metody tooProgram.cs hello:

```csharp
static void UseContainerSAS(string sas)
{
    //Try performing container operations with hello SAS provided.

    //Return a reference toohello container using hello SAS URI.
    CloudBlobContainer container = new CloudBlobContainer(new Uri(sas));

    //Create a list toostore blob URIs returned by a listing operation on hello container.
    List<ICloudBlob> blobList = new List<ICloudBlob>();

    //Write operation: write a new blob toohello container.
    try
    {
        CloudBlockBlob blob = container.GetBlockBlobReference("blobCreatedViaSAS.txt");
        string blobContent = "This blob was created with a shared access signature granting write permissions toohello container. ";
        blob.UploadText(blobContent);

        Console.WriteLine("Write operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Write operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //List operation: List hello blobs in hello container.
    try
    {
        foreach (ICloudBlob blob in container.ListBlobs())
        {
            blobList.Add(blob);
        }
        Console.WriteLine("List operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("List operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //Read operation: Get a reference tooone of hello blobs in hello container and read it.
    try
    {
        CloudBlockBlob blob = container.GetBlockBlobReference(blobList[0].Name);
        MemoryStream msRead = new MemoryStream();
        msRead.Position = 0;
        using (msRead)
        {
            blob.DownloadToStream(msRead);
            Console.WriteLine(msRead.Length);
        }
        Console.WriteLine("Read operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Read operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
    Console.WriteLine();

    //Delete operation: Delete a blob in hello container.
    try
    {
        CloudBlockBlob blob = container.GetBlockBlobReference(blobList[0].Name);
        blob.Delete();
        Console.WriteLine("Delete operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Delete operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
}
```

Aktualizacja hello **Main()** toocall — metoda **UseContainerSAS()** zarówno hello udostępniane sygnatur dostępu tworzone w kontenerze hello:

```csharp
static void Main(string[] args)
{
    string containerSAS = "<your container SAS>";
    string blobSAS = "<your blob SAS>";
    string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    string blobSASWithAccessPolicy = "<your blob SAS with access policy>";

    //Call hello test methods with hello shared access signatures created on hello container, with and without hello access policy.
    UseContainerSAS(containerSAS);
    UseContainerSAS(containerSASWithAccessPolicy);

    Console.ReadLine();
}
```

### <a name="add-a-method-tootry-blob-operations-using-a-shared-access-signature"></a>Dodaj metodę operacji obiektu blob tootry przy użyciu sygnatury dostępu współdzielonego
Na koniec należy dodać metody, która sprawdza operacje niektórych obiektów blob przy użyciu sygnatury dostępu współdzielonego dla obiektu blob hello. W takim przypadku stosujemy konstruktora hello **CloudBlockBlob(String)**, przekazując hello sygnatury dostępu współdzielonego, tooreturn toohello odwołanie do obiektu blob. Żadne inne uwierzytelnianie nie jest wymagane; jest on oparty na podpis hello samodzielnie.

Dodaj następujące metody tooProgram.cs hello:

```csharp
static void UseBlobSAS(string sas)
{
    //Try performing blob operations using hello SAS provided.

    //Return a reference toohello blob using hello SAS URI.
    CloudBlockBlob blob = new CloudBlockBlob(new Uri(sas));

    //Write operation: Write a new blob toohello container.
    try
    {
        string blobContent = "This blob was created with a shared access signature granting write permissions toohello blob. ";
        MemoryStream msWrite = new MemoryStream(Encoding.UTF8.GetBytes(blobContent));
        msWrite.Position = 0;
        using (msWrite)
        {
            blob.UploadFromStream(msWrite);
        }
        Console.WriteLine("Write operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Write operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //Read operation: Read hello contents of hello blob.
    try
    {
        MemoryStream msRead = new MemoryStream();
        using (msRead)
        {
            blob.DownloadToStream(msRead);
            msRead.Position = 0;
            using (StreamReader reader = new StreamReader(msRead, true))
            {
                string line;
                while ((line = reader.ReadLine()) != null)
                {
                    Console.WriteLine(line);
                }
            }
        }
        Console.WriteLine("Read operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Read operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //Delete operation: Delete hello blob.
    try
    {
        blob.Delete();
        Console.WriteLine("Delete operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Delete operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
}
```

Aktualizacja hello **Main()** toocall — metoda **UseBlobSAS()** zarówno hello udostępniane sygnatur dostępu, utworzonych na powitania obiektów blob:

```csharp
static void Main(string[] args)
{
    string containerSAS = "<your container SAS>";
    string blobSAS = "<your blob SAS>";
    string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    string blobSASWithAccessPolicy = "<your blob SAS with access policy>";

    //Call hello test methods with hello shared access signatures created on hello container, with and without hello access policy.
    UseContainerSAS(containerSAS);
    UseContainerSAS(containerSASWithAccessPolicy);

    //Call hello test methods with hello shared access signatures created on hello blob, with and without hello access policy.
    UseBlobSAS(blobSAS);
    UseBlobSAS(blobSASWithAccessPolicy);

    Console.ReadLine();
}
```

Uruchom aplikację konsolową hello i sprawdź toosee dane wyjściowe hello, jakie operacje są dozwolone w przypadku których podpisów. dane wyjściowe Hello w oknie konsoli hello będzie wyglądać podobnie toohello następujące:

```
Write operation succeeded for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl

List operation succeeded for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl

Read operation failed for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl
Additional error information: hello remote server returned an error: (403) Forbidden.

Delete operation failed for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl
Additional error information: hello remote server returned an error: (403) Forbidden.

...
```

## <a name="next-steps"></a>Następne kroki

* [Udostępnione sygnatur dostępu, część 1: Opis modelu sygnatur dostępu Współdzielonego hello](storage-dotnet-shared-access-signature-part-1.md)
* [Zarządzanie toocontainers anonimowy dostęp do odczytu i obiektów blob](storage-manage-access-to-resources.md)
* [Delegowanie dostępu za pomocą podpisu dostępu współdzielonego (interfejsu API REST)](http://msdn.microsoft.com/library/azure/ee395415.aspx)
* [Wprowadzenie do tabeli i kolejki SAS](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)
