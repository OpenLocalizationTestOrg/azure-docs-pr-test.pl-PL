---
title: aaaTransfer danych z hello Biblioteka przenoszenia danych Microsoft Azure Storage | Dokumentacja firmy Microsoft
description: "Użyj hello Biblioteka przenoszenia danych toomove lub kopiowania danych tooor z obiektu blob i zawartości pliku. Kopiowanie danych tooAzure magazynu z lokalnych plików, lub danych w ramach urządzeń magazynujących lub między kontami magazynu. Łatwo przeprowadzić migrację z tooAzure danych magazynu."
services: storage
documentationcenter: 
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/22/2017
ms.author: seguler
ms.openlocfilehash: 5de902d132565a8eafdc672f7a1a18e1a2db3a06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-hello-microsoft-azure-storage-data-movement-library"></a>Transfer danych z hello Biblioteka przenoszenia danych Microsoft Azure Storage

## <a name="overview"></a>Omówienie
Witaj Biblioteka przenoszenia danych Microsoft Azure Storage jest biblioteki typu open source i platform, która jest przeznaczona dla wysokiej wydajności, przekazywanie, pobieranie i kopiowania plików i obiektów blob magazynu Azure. Ta biblioteka jest hello podstawowym środowisku przenoszenia danych obsługującego [AzCopy](storage-use-azcopy.md). Hello Biblioteka przenoszenia danych udostępnia wygodne metody, które nie są dostępne w przypadku naszego tradycyjnych [biblioteki klienta magazynu Azure .NET](storage-dotnet-how-to-use-blobs.md). Dotyczy to również hello możliwości tooset hello liczbę operacji równoległych, śledzenie postępu przenoszenia, łatwe wznawianie transferu anulowane i o wiele więcej.  

Ta biblioteka używa również .NET Core, co oznacza, że użytkownik może być używany podczas tworzenia aplikacji programu .NET dla systemu Windows, Linux i macOS. toolearn więcej informacji na temat platformy .NET Core, zobacz toohello [dokumentacji platformy .NET Core](https://dotnet.github.io/). Ta biblioteka działa także dla tradycyjnej aplikacji .NET Framework dla systemu Windows. 

W tym dokumencie przedstawiono sposób toocreate .NET Core konsoli aplikacji, która działa w systemach Windows, Linux i macOS i wykonuje hello następujące scenariusze:

- Przekazywanie plików i katalogów tooBlob magazynu.
- Podczas transferu danych, należy zdefiniować hello liczbę operacji równoległych.
- Śledź postęp transferu danych.
- Transfer danych Wznów anulowane. 
- Skopiuj plik z tooBlob adres URL magazynu. 
- Kopiowanie z magazynu obiektów Blob tooBlob magazynu.

**Co jest potrzebne:**

* [Visual Studio Code](https://code.visualstudio.com/)
* [Konto usługi Azure Storage](storage-create-storage-account.md#create-a-storage-account)

> [!NOTE]
> W tym przewodniku założono, że czytelnik zna już [usługi Azure Storage](https://azure.microsoft.com/services/storage/). Jeśli nie, odczytywanie hello [tooAzure wprowadzenie magazynu](storage-introduction.md) warto dokumentacji. Przede wszystkim należy się zbyt[Utwórz konto magazynu](storage-create-storage-account.md#create-a-storage-account) przy użyciu toostart hello Biblioteka przenoszenia danych.
> 
> 

## <a name="setup"></a>Konfiguracja  

1. Odwiedź hello [Przewodnik instalacji programu .NET Core](https://www.microsoft.com/net/core) tooinstall .NET Core. Wybierz opcję wiersza polecenia hello, wybierając środowiska. 
2. Z wiersza polecenia hello Utwórz katalog projektu. Przejdź do tego katalogu, wpisz `dotnet new` projekt konsoli toocreate C#.
3. Otwórz ustawienia tego katalogu w Visual Studio Code. Ten krok można szybko zrobić przy użyciu wiersza polecenia hello wpisując `code .`.  
4. Zainstaluj hello [C# rozszerzenia](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) z hello Visual Studio Marketplace kodu. Uruchom ponownie program Visual Studio Code. 
5. W tym momencie powinny zostać wyświetlone dwa monity. W przypadku dodawania "toobuild wymaganych zasobów i debugowania." Kliknij przycisk "tak". Innego wiersza jest przywracania nierozwiązane zależności. Kliknij pozycję "Przywróć".
6. Teraz powinien zawierać aplikacji `launch.json` plik pod hello `.vscode` katalogu. W tym pliku, zmień hello `externalConsole` wartość zbyt`true`.
7. Visual Studio Code umożliwia toodebug aplikacji .NET Core. Trafienia `F5` toorun aplikacji oraz zweryfikować konfigurację. Powinny pojawić się "Witaj świecie!" Konsola toohello wydruku. 

## <a name="add-data-movement-library-tooyour-project"></a>Dodaj projekt tooyour Biblioteka przenoszenia danych

1. Dodaj hello najnowszą wersję hello Biblioteka przenoszenia danych toohello `dependencies` części z `project.json` pliku. W czasie hello zapisu będzie tej wersji`"Microsoft.Azure.Storage.DataMovement": "0.5.0"` 
2. Dodaj `"portable-net45+win8"` toohello `imports` sekcji. 
3. Wiersz powinien być wyświetlany toorestore Twojego projektu. Kliknij przycisk "Przywróć" hello. Można też przywrócić projektu z wiersza polecenia hello, wpisując polecenie hello `dotnet restore` w głównym hello katalogu projektu.

Modyfikowanie `project.json`:

    {
      "version": "1.0.0-*",
      "buildOptions": {
        "debugType": "portable",
        "emitEntryPoint": true
      },
      "dependencies": {
        "Microsoft.Azure.Storage.DataMovement": "0.5.0"
      },
      "frameworks": {
        "netcoreapp1.1": {
          "dependencies": {
            "Microsoft.NETCore.App": {
              "type": "platform",
              "version": "1.1.0"
            }
          },
          "imports": [
            "dnxcore50",
            "portable-net45+win8"
          ]
        }
      }
    }

## <a name="set-up-hello-skeleton-of-your-application"></a>Konfigurowanie hello szkielet aplikacji
Witaj najpierw nie skonfigurowano kodu "szkielet" hello naszej aplikacji. Ten kod wyświetla monit o nas dla konta magazynu kluczy nazwy i konta i używa tych poświadczeń toocreate `CloudStorageAccount` obiektu. Ten obiekt jest używany toointeract z nasze konto magazynu we wszystkich scenariuszach transferu. Kod Hello również monituje nam toochoose hello rodzaj operacji transferu chcielibyśmy tooexecute. 

Modyfikowanie `Program.cs`:

```csharp
using System;
using System.Threading;
using System.Diagnostics;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
using Microsoft.WindowsAzure.Storage.DataMovement;

namespace DMLibSample
{
    public class Program
    {
        public static void Main()
        {
            Console.WriteLine("Enter Storage account name:");           
            string accountName = Console.ReadLine();

            Console.WriteLine("\nEnter Storage account key:");           
            string accountKey = Console.ReadLine();

            string storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=" + accountName + ";AccountKey=" + accountKey;
            CloudStorageAccount account = CloudStorageAccount.Parse(storageConnectionString);

            ExecuteChoice(account);
        }

        public static void ExecuteChoice(CloudStorageAccount account)
        {
            Console.WriteLine("\nWhat type of transfer would you like tooexecute?\n1. Local file --> Azure Blob\n2. Local directory --> Azure Blob directory\n3. URL (e.g. Amazon S3 file) --> Azure Blob\n4. Azure Blob --> Azure Blob");
            int choice = int.Parse(Console.ReadLine());

            if(choice == 1)
            {
                TransferLocalFileToAzureBlob(account).Wait();
            }
            else if(choice == 2)
            {
                TransferLocalDirectoryToAzureBlobDirectory(account).Wait();
            }
            else if(choice == 3)
            {
                TransferUrlToAzureBlob(account).Wait();
            }
            else if(choice == 4)
            {
                TransferAzureBlobToAzureBlob(account).Wait();
            }
        }

        public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
        { 
            
        }

        public static async Task TransferLocalDirectoryToAzureBlobDirectory(CloudStorageAccount account)
        { 
            
        }

        public static async Task TransferUrlToAzureBlob(CloudStorageAccount account)
        {

        }

        public static async Task TransferAzureBlobToAzureBlob(CloudStorageAccount account)
        {

        }
    }
}
```

## <a name="transfer-local-file-tooazure-blob"></a>Transfer pliku lokalnego tooAzure obiektów Blob
Dodaj metody hello `GetSourcePath` i `GetBlob` zbyt`Program.cs`:

```csharp
public static string GetSourcePath()
{
    Console.WriteLine("\nProvide path for source:");
    string sourcePath = Console.ReadLine();

    return sourcePath;
}

public static CloudBlockBlob GetBlob(CloudStorageAccount account)
{
    CloudBlobClient blobClient = account.CreateCloudBlobClient();

    Console.WriteLine("\nProvide name of Blob container:");
    string containerName = Console.ReadLine();
    CloudBlobContainer container = blobClient.GetContainerReference(containerName);
    container.CreateIfNotExistsAsync().Wait();

    Console.WriteLine("\nProvide name of new Blob:");
    string blobName = Console.ReadLine();
    CloudBlockBlob blob = container.GetBlockBlobReference(blobName);

    return blob;
}
```

Modyfikowanie hello `TransferLocalFileToAzureBlob` metody:

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account);
    Console.WriteLine("\nTransfer started...");
    await TransferManager.UploadAsync(localFilePath, blob);
    Console.WriteLine("\nTransfer operation complete.");
    ExecuteChoice(account);
}
```

Ten kod nam monit o podanie ścieżki hello tooa pliku lokalnego, hello Nazwa nowego lub istniejącego kontenera i hello nazwę nowego obiektu blob. Witaj `TransferManager.UploadAsync` metoda przeprowadza hello przekazywania, korzystając z tych informacji. 

Trafienia `F5` toorun aplikacji. Możesz sprawdzić, że przekazywania hello wystąpił wyświetlając konta magazynu z hello [Eksploratora usługi Microsoft Azure Storage](http://storageexplorer.com/).

## <a name="set-number-of-parallel-operations"></a>Ustaw liczbę operacji równoległych
Funkcja dużą oferowane przez hello Biblioteka przenoszenia danych jest hello możliwości tooset hello liczbę operacji równoległych tooincrease hello danych przeniesienie przepływności. Domyślnie program hello Biblioteka przenoszenia danych ustawia hello liczbę operacji równoległych too8 * hello liczba rdzeni na tym komputerze. 

Należy pamiętać, że wiele operacji równoległych w środowisku niskiej przepustowości może przeciąży hello połączenie sieciowe i faktycznie zapobiec operacji pełni zakończenie działania. Będziesz potrzebować tooexperiment z tym toodetermine ustawienie co działa najlepiej oparte na na dostępną przepustowość sieci. 

Dodajmy trochę kodu, który pozwala nam tooset hello liczbę operacji równoległych. Umożliwia również Dodaj kod, który razy, jak długo hello toocomplete transferu.

Dodaj `SetNumberOfParallelOperations` metody zbyt`Program.cs`:

```csharp
public static void SetNumberOfParallelOperations()
{
    Console.WriteLine("\nHow many parallel operations would you like toouse?");
    string parallelOperations = Console.ReadLine();
    TransferManager.Configurations.ParallelOperations = int.Parse(parallelOperations);
}
```

Modyfikowanie hello `ExecuteChoice` toouse metody `SetNumberOfParallelOperations`:

```csharp
public static void ExecuteChoice(CloudStorageAccount account)
{
    Console.WriteLine("\nWhat type of transfer would you like tooexecute?\n1. Local file --> Azure Blob\n2. Local directory --> Azure Blob directory\n3. URL (e.g. Amazon S3 file) --> Azure Blob\n4. Azure Blob --> Azure Blob");
    int choice = int.Parse(Console.ReadLine());

    SetNumberOfParallelOperations();

    if(choice == 1)
    {
        TransferLocalFileToAzureBlob(account).Wait();
    }
    else if(choice == 2)
    {
        TransferLocalDirectoryToAzureBlobDirectory(account).Wait();
    }
    else if(choice == 3)
    {
        TransferUrlToAzureBlob(account).Wait();
    }
    else if(choice == 4)
    {
        TransferAzureBlobToAzureBlob(account).Wait();
    }
}
```

Modyfikowanie hello `TransferLocalFileToAzureBlob` toouse metody czasomierza:

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account);
    Console.WriteLine("\nTransfer started...");
    Stopwatch stopWatch = Stopwatch.StartNew();
    await TransferManager.UploadAsync(localFilePath, blob);
    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

## <a name="track-transfer-progress"></a>Śledź postęp transferu
Znajomość czas trwania dla naszych tootransfer danych jest doskonałym rozwiązaniem. Jednak jest możliwe toosee postęp hello naszego przenoszenia *podczas* operacji transferu hello będą jeszcze bardziej poprawić jakość. tooachieve tego scenariusza, potrzebujemy toocreate `TransferContext` obiektu. Witaj `TransferContext` obiektu jest dostarczany w dwóch formach: `SingleTransferContext` i `DirectoryTransferContext`. wcześniejsze Hello jest przeznaczona przesyłania jednym pliku (czyli co to jest robimy teraz) i hello ostatnie transferowania katalogu plików (które dodajemy później).

Dodaj metody hello `GetSingleTransferContext` i `GetDirectoryTransferContext` zbyt`Program.cs`: 

```csharp
public static SingleTransferContext GetSingleTransferContext(TransferCheckpoint checkpoint)
{
    SingleTransferContext context = new SingleTransferContext(checkpoint);

    context.ProgressHandler = new Progress<TransferStatus>((progress) =>
    {
        Console.Write("\rBytes transferred: {0}", progress.BytesTransferred );
    });
    
    return context;
}

public static DirectoryTransferContext GetDirectoryTransferContext(TransferCheckpoint checkpoint)
{
    DirectoryTransferContext context = new DirectoryTransferContext(checkpoint);

    context.ProgressHandler = new Progress<TransferStatus>((progress) =>
    {
        Console.Write("\rBytes transferred: {0}", progress.BytesTransferred );
    });
    
    return context;
}
```

Modyfikowanie hello `TransferLocalFileToAzureBlob` toouse metody `GetSingleTransferContext`:

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account);
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint);
    Console.WriteLine("\nTransfer started...\n");
    Stopwatch stopWatch = Stopwatch.StartNew();
    await TransferManager.UploadAsync(localFilePath, blob, null, context);
    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

## <a name="resume-a-canceled-transfer"></a>Wznawianie transferu anulowane
Inna funkcja wygodny oferowane przez hello Biblioteka przenoszenia danych jest tooresume możliwości hello anulowane transferu. Dodajmy trochę kodu, który umożliwia transfer hello Anuluj tootemporarily, wpisując `c`, a następnie Wznów hello transfer później 3 sekundy.

Modyfikowanie `TransferLocalFileToAzureBlob`:

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' tootemporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    try
    {
        task = TransferManager.UploadAsync(localFilePath, blob, null, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetSingleTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.UploadAsync(localFilePath, blob, null, context);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

Dotychczas naszych `checkpoint` wartość została ustawiona zawsze zbyt`null`. Teraz Jeśli trwa anulowanie transferu hello, możemy pobrać hello ostatniego punktu kontrolnego naszego przenoszenia, a następnie używać tego nowego punktu kontrolnego w kontekście naszego przenoszenia. 

## <a name="transfer-local-directory-tooazure-blob-directory"></a>Transfer katalogu obiektu Blob tooAzure katalogu lokalnego
Byłoby zadowalające hello Biblioteka przenoszenia danych w czasie może przekazać tylko jeden plik. Na szczęście to nie jest hello. Witaj Biblioteka przenoszenia danych zawiera tootransfer możliwości hello katalog plików i wszystkich jego podkatalogach. Dodajmy trochę kodu umożliwiający wykonywanie toodo tylko dla niej.

Najpierw dodaj metody hello `GetBlobDirectory` zbyt`Program.cs`:

```csharp
public static CloudBlobDirectory GetBlobDirectory(CloudStorageAccount account)
{
    CloudBlobClient blobClient = account.CreateCloudBlobClient();

    Console.WriteLine("\nProvide name of Blob container. This can be a new or existing Blob container:");
    string containerName = Console.ReadLine();
    CloudBlobContainer container = blobClient.GetContainerReference(containerName);
    container.CreateIfNotExistsAsync().Wait();

    CloudBlobDirectory blobDirectory = container.GetDirectoryReference("");

    return blobDirectory;
}
```

Następnie należy zmodyfikować `TransferLocalDirectoryToAzureBlobDirectory`:

```csharp
public static async Task TransferLocalDirectoryToAzureBlobDirectory(CloudStorageAccount account)
{ 
    string localDirectoryPath = GetSourcePath();
    CloudBlobDirectory blobDirectory = GetBlobDirectory(account); 
    TransferCheckpoint checkpoint = null;
    DirectoryTransferContext context = GetDirectoryTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' tootemporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    UploadDirectoryOptions options = new UploadDirectoryOptions()
    {
        Recursive = true
    };

    try
    {
        task = TransferManager.UploadDirectoryAsync(localDirectoryPath, blobDirectory, options, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetDirectoryTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.UploadDirectoryAsync(localDirectoryPath, blobDirectory, options, context);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

Istnieje kilka różnic między tej metody oraz metody hello przekazywania jednego pliku. Używamy teraz `TransferManager.UploadDirectoryAsync` i hello `getDirectoryTransferContext` metody utworzony wcześniej. Ponadto obecnie udostępniamy `options` wartość tooour operacji przekazywania, która pozwala nam tooindicate chcemy tooinclude podkatalogów w przesyłania. 

## <a name="copy-file-from-url-tooazure-blob"></a>Skopiuj plik z tooAzure adresu URL obiektu Blob
Teraz możemy dodać kod, który pozwala nam toocopy pliku z adresu URL tooan obiektów Blob platformy Azure. 

Modyfikowanie `TransferUrlToAzureBlob`:

```csharp
public static async Task TransferUrlToAzureBlob(CloudStorageAccount account)
{
    Uri uri = new Uri(GetSourcePath());
    CloudBlockBlob blob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' tootemporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    try
    {
        task = TransferManager.CopyAsync(uri, blob, true, null, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetSingleTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.CopyAsync(uri, blob, true, null, context, cancellationSource.Token);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

Jeden przypadek użycia ważne dla tej funkcji jest gdy będziesz potrzebować toomove dane z innego tooAzure usługi (np. AWS) w chmurze. Tak długo, jak adres URL, który zapewnia dostęp toohello zasobów, tego zasobu można łatwo przenosić do obiektów blob Azure przy użyciu hello `TransferManager.CopyAsync` metody. Ta metoda wprowadza również nowe parametrów typu boolean. Ustawienie tego parametru zbyt`true` wskazuje, że firma Microsoft kopiowania toodo asynchronicznych po stronie serwera. Ustawienie tego parametru zbyt`false` wskazuje synchronicznych kopii - oznacza zasób hello jest pobrany tooour komputera lokalnego, następnie przekazać tooAzure obiektu Blob. Jednak synchronicznego kopiowania jest obecnie dostępna tylko do kopiowania z jednego tooanother zasobów usługi Azure Storage. 

## <a name="transfer-azure-blob-tooazure-blob"></a>Transfer tooAzure obiektów Blob platformy Azure Blob
Inna funkcja jednoznacznie zapewnianej przez hello Biblioteka przenoszenia danych jest toocopy możliwości hello z jednego tooanother zasobów usługi Azure Storage. 

Modyfikowanie `TransferAzureBlobToAzureBlob`:

```csharp
public static async Task TransferAzureBlobToAzureBlob(CloudStorageAccount account)
{
    CloudBlockBlob sourceBlob = GetBlob(account);
    CloudBlockBlob destinationBlob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' tootemporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    try
    {
        task = TransferManager.CopyAsync(sourceBlob, destinationBlob, true, null, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetSingleTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.CopyAsync(sourceBlob, destinationBlob, false, null, context, cancellationSource.Token);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

W tym przykładzie parametr logiczna hello umieszczania `TransferManager.CopyAsync` zbyt`false` tooindicate czy chcemy toodo synchronicznych kopii. Oznacza to, że hello zasobów jest najpierw pobrany tooour komputera lokalnego, a następnie przekazać tooAzure obiektów Blob. Opcja synchronicznych kopii Hello jest tooensure doskonały sposób, że operacji kopiowania ma spójne szybkości. Z kolei szybkości hello asynchroniczne kopii po stronie serwera jest zależny od hello dostępną przepustowość sieci na powitania serwera, który mogą się zmieniać. Jednak synchronicznych kopii może wygenerować dodatkowe wyjście koszt w porównaniu tooasynchronous kopiowania. Witaj zalecane podejście jest toouse synchronicznych kopii w maszynie Wirtualnej platformy Azure, który znajduje się w hello tego samego regionu koszt wyjście tooavoid konta magazynu źródłowego.

## <a name="conclusion"></a>Podsumowanie
Naszej aplikacji przepływu danych jest teraz ukończona. [przykład pełny kod Hello jest dostępny w witrynie GitHub](https://github.com/azure-samples/storage-dotnet-data-movement-library-app). 

## <a name="next-steps"></a>Następne kroki
W tym wprowadzenie, utworzyliśmy aplikację, która współdziała z usługą Azure Storage i działa w systemach Windows, Linux i macOS. Rozpoczęto pobieranie ukierunkowanych na magazyn obiektów Blob. Jednak ten sam wiedzy może być zastosowane tooFile magazynu. toolearn więcej, zapoznaj się z [Biblioteka przenoszenia danych magazynu Azure dokumentacji](https://azure.github.io/azure-storage-net-data-movement).

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]




