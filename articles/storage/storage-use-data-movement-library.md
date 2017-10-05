---
title: "Transfer danych za pomocą Biblioteka przenoszenia danych magazynu Microsoft Azure | Dokumentacja firmy Microsoft"
description: "Biblioteka przenoszenia danych umożliwia przenoszenie lub kopiowanie danych do lub z obiektu blob i zawartości pliku. Kopiowanie danych do magazynu Azure z lokalnych plików lub kopiowania danych w ramach urządzeń magazynujących lub między kontami magazynu. Łatwo przeprowadzić migrację danych do usługi Azure Storage."
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
ms.openlocfilehash: 2ba94e4dd931b6d385101c7dadccfa3583b5296e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="transfer-data-with-the-microsoft-azure-storage-data-movement-library"></a><span data-ttu-id="47c0e-105">Transfer danych za pomocą Biblioteka przenoszenia danych magazynu Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="47c0e-105">Transfer Data with the Microsoft Azure Storage Data Movement Library</span></span>

## <a name="overview"></a><span data-ttu-id="47c0e-106">Omówienie</span><span class="sxs-lookup"><span data-stu-id="47c0e-106">Overview</span></span>
<span data-ttu-id="47c0e-107">Biblioteka przenoszenia danych w programie Microsoft Azure magazynu jest biblioteki typu open source i platform, która jest przeznaczona dla wysokiej wydajności, przekazywanie, pobieranie i kopiowania plików i obiektów blob magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="47c0e-107">The Microsoft Azure Storage Data Movement Library is a cross-platform open source library that is designed for high performance uploading, downloading, and copying of Azure Storage Blobs and Files.</span></span> <span data-ttu-id="47c0e-108">Ta biblioteka jest podstawowym środowisku przenoszenia danych, które obsługuje [AzCopy](storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="47c0e-108">This library is the core data movement framework that powers [AzCopy](storage-use-azcopy.md).</span></span> <span data-ttu-id="47c0e-109">Biblioteka przenoszenia danych udostępnia wygodne metody, które nie są dostępne w przypadku naszego tradycyjnych [biblioteki klienta magazynu Azure .NET](storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="47c0e-109">The Data Movement Library provides convenient methods that aren't available in our traditional [.NET Azure Storage Client Library](storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="47c0e-110">Obejmuje to możliwość Ustaw liczbę operacji równoległych, śledzić postępu przenoszenia, łatwe wznawianie transferu anulowane i o wiele więcej.</span><span class="sxs-lookup"><span data-stu-id="47c0e-110">This includes the ability to set the number of parallel operations, track transfer progress, easily resume a canceled transfer, and much more.</span></span>  

<span data-ttu-id="47c0e-111">Ta biblioteka używa również .NET Core, co oznacza, że użytkownik może być używany podczas tworzenia aplikacji programu .NET dla systemu Windows, Linux i macOS.</span><span class="sxs-lookup"><span data-stu-id="47c0e-111">This library also uses .NET Core, which means you can use it when building .NET apps for Windows, Linux and macOS.</span></span> <span data-ttu-id="47c0e-112">Aby dowiedzieć się więcej na temat platformy .NET Core, zobacz [dokumentacji platformy .NET Core](https://dotnet.github.io/).</span><span class="sxs-lookup"><span data-stu-id="47c0e-112">To learn more about .NET Core, refer to the [.NET Core documentation](https://dotnet.github.io/).</span></span> <span data-ttu-id="47c0e-113">Ta biblioteka działa także dla tradycyjnej aplikacji .NET Framework dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="47c0e-113">This library also works for traditional .NET Framework apps for Windows.</span></span> 

<span data-ttu-id="47c0e-114">W tym dokumencie przedstawiono sposób tworzenia aplikacji konsoli .NET Core, który działającą w systemach Windows, Linux i macOS i wykonuje następujące scenariusze:</span><span class="sxs-lookup"><span data-stu-id="47c0e-114">This document demonstrates how to create a .NET Core console application that that runs on Windows, Linux, and macOS and performs the following scenarios:</span></span>

- <span data-ttu-id="47c0e-115">Przekazywanie plików i katalogów do magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="47c0e-115">Upload files and directories to Blob Storage.</span></span>
- <span data-ttu-id="47c0e-116">Określ liczbę operacji równoległych podczas transferu danych.</span><span class="sxs-lookup"><span data-stu-id="47c0e-116">Define the number of parallel operations when transferring data.</span></span>
- <span data-ttu-id="47c0e-117">Śledź postęp transferu danych.</span><span class="sxs-lookup"><span data-stu-id="47c0e-117">Track data transfer progress.</span></span>
- <span data-ttu-id="47c0e-118">Transfer danych Wznów anulowane.</span><span class="sxs-lookup"><span data-stu-id="47c0e-118">Resume canceled data transfer.</span></span> 
- <span data-ttu-id="47c0e-119">Skopiuj plik z adresu URL do magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="47c0e-119">Copy file from URL to Blob Storage.</span></span> 
- <span data-ttu-id="47c0e-120">Skopiuj z magazynu obiektów Blob do magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="47c0e-120">Copy from Blob Storage to Blob Storage.</span></span>

<span data-ttu-id="47c0e-121">**Co jest potrzebne:**</span><span class="sxs-lookup"><span data-stu-id="47c0e-121">**What you need:**</span></span>

* [<span data-ttu-id="47c0e-122">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="47c0e-122">Visual Studio Code</span></span>](https://code.visualstudio.com/)
* <span data-ttu-id="47c0e-123">[Konto usługi Azure Storage](storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="47c0e-123">An [Azure storage account](storage-create-storage-account.md#create-a-storage-account)</span></span>

> [!NOTE]
> <span data-ttu-id="47c0e-124">W tym przewodniku założono, że czytelnik zna już [usługi Azure Storage](https://azure.microsoft.com/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="47c0e-124">This guide assumes that you are already familiar with [Azure Storage](https://azure.microsoft.com/services/storage/).</span></span> <span data-ttu-id="47c0e-125">Jeśli nie, odczytywanie [wprowadzenie do usługi Azure Storage](storage-introduction.md) warto dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="47c0e-125">If not, reading the [Introduction to Azure Storage](storage-introduction.md) documentation is helpful.</span></span> <span data-ttu-id="47c0e-126">Przede wszystkim należy [Utwórz konto magazynu](storage-create-storage-account.md#create-a-storage-account) aby rozpocząć korzystanie z Biblioteka przenoszenia danych.</span><span class="sxs-lookup"><span data-stu-id="47c0e-126">Most importantly, you need to [create a Storage account](storage-create-storage-account.md#create-a-storage-account) to start using the Data Movement Library.</span></span>
> 
> 

## <a name="setup"></a><span data-ttu-id="47c0e-127">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="47c0e-127">Setup</span></span>  

1. <span data-ttu-id="47c0e-128">Odwiedź stronę [Przewodnik instalacji programu .NET Core](https://www.microsoft.com/net/core) do zainstalowania platformy .NET Core.</span><span class="sxs-lookup"><span data-stu-id="47c0e-128">Visit the [.NET Core Installation Guide](https://www.microsoft.com/net/core) to install .NET Core.</span></span> <span data-ttu-id="47c0e-129">Podczas wybierania środowiska, należy wybrać opcję wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="47c0e-129">When selecting your environment, choose the command-line option.</span></span> 
2. <span data-ttu-id="47c0e-130">W wierszu polecenia Utwórz katalog projektu.</span><span class="sxs-lookup"><span data-stu-id="47c0e-130">From the command line, create a directory for your project.</span></span> <span data-ttu-id="47c0e-131">Przejdź do tego katalogu, wpisz `dotnet new` do tworzenia projektu konsoli C#.</span><span class="sxs-lookup"><span data-stu-id="47c0e-131">Navigate into this directory, then type `dotnet new` to create a C# console project.</span></span>
3. <span data-ttu-id="47c0e-132">Otwórz ustawienia tego katalogu w Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="47c0e-132">Open this directory in Visual Studio Code.</span></span> <span data-ttu-id="47c0e-133">Ten krok można szybko zrobić przy użyciu wiersza polecenia, wpisując `code .`.</span><span class="sxs-lookup"><span data-stu-id="47c0e-133">This step can be quickly done via the command line by typing `code .`.</span></span>  
4. <span data-ttu-id="47c0e-134">Zainstaluj [C# rozszerzenia](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) z Visual Studio Marketplace kodu.</span><span class="sxs-lookup"><span data-stu-id="47c0e-134">Install the [C# extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) from the Visual Studio Code Marketplace.</span></span> <span data-ttu-id="47c0e-135">Uruchom ponownie program Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="47c0e-135">Restart Visual Studio Code.</span></span> 
5. <span data-ttu-id="47c0e-136">W tym momencie powinny zostać wyświetlone dwa monity.</span><span class="sxs-lookup"><span data-stu-id="47c0e-136">At this point, you should see two prompts.</span></span> <span data-ttu-id="47c0e-137">W przypadku dodawania "zasoby wymagane do tworzenia i debugowania."</span><span class="sxs-lookup"><span data-stu-id="47c0e-137">One is for adding "required assets to build and debug."</span></span> <span data-ttu-id="47c0e-138">Kliknij przycisk "tak".</span><span class="sxs-lookup"><span data-stu-id="47c0e-138">Click "yes."</span></span> <span data-ttu-id="47c0e-139">Innego wiersza jest przywracania nierozwiązane zależności.</span><span class="sxs-lookup"><span data-stu-id="47c0e-139">Another prompt is for restoring unresolved dependencies.</span></span> <span data-ttu-id="47c0e-140">Kliknij pozycję "Przywróć".</span><span class="sxs-lookup"><span data-stu-id="47c0e-140">Click "restore."</span></span>
6. <span data-ttu-id="47c0e-141">Teraz powinien zawierać aplikacji `launch.json` plików w obszarze `.vscode` katalogu.</span><span class="sxs-lookup"><span data-stu-id="47c0e-141">Your application should now contain a `launch.json` file under the `.vscode` directory.</span></span> <span data-ttu-id="47c0e-142">W tym pliku, zmień `externalConsole` do wartości `true`.</span><span class="sxs-lookup"><span data-stu-id="47c0e-142">In this file, change the `externalConsole` value to `true`.</span></span>
7. <span data-ttu-id="47c0e-143">Visual Studio Code pozwala na debugowanie aplikacji .NET Core.</span><span class="sxs-lookup"><span data-stu-id="47c0e-143">Visual Studio Code allows you to debug .NET Core applications.</span></span> <span data-ttu-id="47c0e-144">Trafienia `F5` do uruchomienia aplikacji, a następnie zweryfikować konfigurację.</span><span class="sxs-lookup"><span data-stu-id="47c0e-144">Hit `F5` to run your application and verify that your setup is working.</span></span> <span data-ttu-id="47c0e-145">Powinny pojawić się "Witaj świecie!"</span><span class="sxs-lookup"><span data-stu-id="47c0e-145">You should see "Hello World!"</span></span> <span data-ttu-id="47c0e-146">podane w konsoli.</span><span class="sxs-lookup"><span data-stu-id="47c0e-146">printed to the console.</span></span> 

## <a name="add-data-movement-library-to-your-project"></a><span data-ttu-id="47c0e-147">Dodaj Biblioteka przenoszenia danych do projektu</span><span class="sxs-lookup"><span data-stu-id="47c0e-147">Add Data Movement Library to your project</span></span>

1. <span data-ttu-id="47c0e-148">Dodaj Biblioteka przenoszenia danych do najnowszej wersji `dependencies` części Twojego `project.json` pliku.</span><span class="sxs-lookup"><span data-stu-id="47c0e-148">Add the latest version of the Data Movement Library to the `dependencies` section of your `project.json` file.</span></span> <span data-ttu-id="47c0e-149">W czasie zapisywania będzie to wersja`"Microsoft.Azure.Storage.DataMovement": "0.5.0"`</span><span class="sxs-lookup"><span data-stu-id="47c0e-149">At the time of writing, this version would be `"Microsoft.Azure.Storage.DataMovement": "0.5.0"`</span></span> 
2. <span data-ttu-id="47c0e-150">Dodaj `"portable-net45+win8"` do `imports` sekcji.</span><span class="sxs-lookup"><span data-stu-id="47c0e-150">Add `"portable-net45+win8"` to the `imports` section.</span></span> 
3. <span data-ttu-id="47c0e-151">Aby przywrócić projekt powinien być wyświetlany monit.</span><span class="sxs-lookup"><span data-stu-id="47c0e-151">A prompt should display to restore your project.</span></span> <span data-ttu-id="47c0e-152">Kliknij przycisk "Przywracanie".</span><span class="sxs-lookup"><span data-stu-id="47c0e-152">Click the "restore" button.</span></span> <span data-ttu-id="47c0e-153">Można też przywrócić projektu z poziomu wiersza polecenia, wpisując polecenie `dotnet restore` w głównym katalogu projektu.</span><span class="sxs-lookup"><span data-stu-id="47c0e-153">You can also restore your project from the command line by typing the command `dotnet restore` in the root of your project directory.</span></span>

<span data-ttu-id="47c0e-154">Modyfikowanie `project.json`:</span><span class="sxs-lookup"><span data-stu-id="47c0e-154">Modify `project.json`:</span></span>

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

## <a name="set-up-the-skeleton-of-your-application"></a><span data-ttu-id="47c0e-155">Konfigurowanie szkielet aplikacji</span><span class="sxs-lookup"><span data-stu-id="47c0e-155">Set up the skeleton of your application</span></span>
<span data-ttu-id="47c0e-156">Najpierw nie skonfigurowano kodu "szkielet" naszej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="47c0e-156">The first thing we do is set up the "skeleton" code of our application.</span></span> <span data-ttu-id="47c0e-157">Ten kod wyświetla monit o nas dla konta magazynu kluczy nazwy i konta i używa tych poświadczeń w celu utworzenia `CloudStorageAccount` obiektu.</span><span class="sxs-lookup"><span data-stu-id="47c0e-157">This code prompts us for a Storage account name and account key and uses those credentials to create a `CloudStorageAccount` object.</span></span> <span data-ttu-id="47c0e-158">Ten obiekt służy do interakcji z nasze konto magazynu we wszystkich scenariuszach transferu.</span><span class="sxs-lookup"><span data-stu-id="47c0e-158">This object is used to interact with our Storage account in all transfer scenarios.</span></span> <span data-ttu-id="47c0e-159">Kod monituje nam wybierz typ operacji transferu, którą chcemy do wykonania.</span><span class="sxs-lookup"><span data-stu-id="47c0e-159">The code also prompts us to choose the type of transfer operation we would like to execute.</span></span> 

<span data-ttu-id="47c0e-160">Modyfikowanie `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="47c0e-160">Modify `Program.cs`:</span></span>

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
            Console.WriteLine("\nWhat type of transfer would you like to execute?\n1. Local file --> Azure Blob\n2. Local directory --> Azure Blob directory\n3. URL (e.g. Amazon S3 file) --> Azure Blob\n4. Azure Blob --> Azure Blob");
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

## <a name="transfer-local-file-to-azure-blob"></a><span data-ttu-id="47c0e-161">Przenieś plik lokalny do obiektów Blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="47c0e-161">Transfer local file to Azure Blob</span></span>
<span data-ttu-id="47c0e-162">Dodaj metody `GetSourcePath` i `GetBlob` do `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="47c0e-162">Add the methods `GetSourcePath` and `GetBlob` to `Program.cs`:</span></span>

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

<span data-ttu-id="47c0e-163">Modyfikowanie `TransferLocalFileToAzureBlob` metody:</span><span class="sxs-lookup"><span data-stu-id="47c0e-163">Modify the `TransferLocalFileToAzureBlob` method:</span></span>

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

<span data-ttu-id="47c0e-164">Ten kod nam monituje o podanie ścieżki do pliku lokalnego, Nazwa nowego lub istniejącego kontenera i nazwę nowego obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="47c0e-164">This code prompts us for the path to a local file, the name of a new or existing container, and the name of a new blob.</span></span> <span data-ttu-id="47c0e-165">`TransferManager.UploadAsync` Metoda przeprowadza przekazywania, korzystając z tych informacji.</span><span class="sxs-lookup"><span data-stu-id="47c0e-165">The `TransferManager.UploadAsync` method performs the upload using this information.</span></span> 

<span data-ttu-id="47c0e-166">Trafienia `F5` do uruchamiania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="47c0e-166">Hit `F5` to run your application.</span></span> <span data-ttu-id="47c0e-167">Możesz sprawdzić, czy przekazywania wystąpił wyświetlając konta magazynu z [Eksploratora usługi Microsoft Azure Storage](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="47c0e-167">You can verify that the upload occurred by viewing your Storage account with the [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

## <a name="set-number-of-parallel-operations"></a><span data-ttu-id="47c0e-168">Ustaw liczbę operacji równoległych</span><span class="sxs-lookup"><span data-stu-id="47c0e-168">Set number of parallel operations</span></span>
<span data-ttu-id="47c0e-169">Wspaniałych funkcji oferowanych przez Biblioteka przenoszenia danych jest możliwość określenia liczbę operacji równoległych w celu zwiększenia przepływności transferu danych.</span><span class="sxs-lookup"><span data-stu-id="47c0e-169">A great feature offered by the Data Movement Library is the ability to set the number of parallel operations to increase the data transfer throughput.</span></span> <span data-ttu-id="47c0e-170">Domyślnie biblioteka przenoszenia danych Ustawia liczbę operacji równoległych 8 * liczba rdzeni na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="47c0e-170">By default, the Data Movement Library sets the number of parallel operations to 8 * the number of cores on your machine.</span></span> 

<span data-ttu-id="47c0e-171">Należy pamiętać, że wiele operacji równoległych w środowisku niskiej przepustowości może przeciąży połączenie sieciowe i faktycznie zapobiec operacji pełni zakończenie działania.</span><span class="sxs-lookup"><span data-stu-id="47c0e-171">Keep in mind that many parallel operations in a low-bandwidth environment may overwhelm the network connection and actually prevent operations from fully completing.</span></span> <span data-ttu-id="47c0e-172">Należy wypróbować to ustawienie, aby określić, co działa najlepiej oparte na dostępną przepustowość sieci.</span><span class="sxs-lookup"><span data-stu-id="47c0e-172">You'll need to experiment with this setting to determine what works best based on your available network bandwidth.</span></span> 

<span data-ttu-id="47c0e-173">Dodajmy trochę kodu, który pozwala ustawić liczbę operacji równoległych.</span><span class="sxs-lookup"><span data-stu-id="47c0e-173">Let's add some code that allows us to set the number of parallel operations.</span></span> <span data-ttu-id="47c0e-174">Umożliwia również Dodaj kod, który czas to czas transferu zakończyć.</span><span class="sxs-lookup"><span data-stu-id="47c0e-174">Let's also add code that times how long it takes for the transfer to complete.</span></span>

<span data-ttu-id="47c0e-175">Dodaj `SetNumberOfParallelOperations` metody `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="47c0e-175">Add a `SetNumberOfParallelOperations` method to `Program.cs`:</span></span>

```csharp
public static void SetNumberOfParallelOperations()
{
    Console.WriteLine("\nHow many parallel operations would you like to use?");
    string parallelOperations = Console.ReadLine();
    TransferManager.Configurations.ParallelOperations = int.Parse(parallelOperations);
}
```

<span data-ttu-id="47c0e-176">Modyfikowanie `ExecuteChoice` metodę `SetNumberOfParallelOperations`:</span><span class="sxs-lookup"><span data-stu-id="47c0e-176">Modify the `ExecuteChoice` method to use `SetNumberOfParallelOperations`:</span></span>

```csharp
public static void ExecuteChoice(CloudStorageAccount account)
{
    Console.WriteLine("\nWhat type of transfer would you like to execute?\n1. Local file --> Azure Blob\n2. Local directory --> Azure Blob directory\n3. URL (e.g. Amazon S3 file) --> Azure Blob\n4. Azure Blob --> Azure Blob");
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

<span data-ttu-id="47c0e-177">Modyfikowanie `TransferLocalFileToAzureBlob` metodę czasomierza:</span><span class="sxs-lookup"><span data-stu-id="47c0e-177">Modify the `TransferLocalFileToAzureBlob` method to use a timer:</span></span>

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

## <a name="track-transfer-progress"></a><span data-ttu-id="47c0e-178">Śledź postęp transferu</span><span class="sxs-lookup"><span data-stu-id="47c0e-178">Track transfer progress</span></span>
<span data-ttu-id="47c0e-179">Znajomość czas trwania dla naszych danych do przesłania jest doskonałym rozwiązaniem.</span><span class="sxs-lookup"><span data-stu-id="47c0e-179">Knowing how long it took for our data to transfer is great.</span></span> <span data-ttu-id="47c0e-180">Jednak możliwość wyświetlany jest postęp naszego przenoszenia *podczas* operacji transferu będą jeszcze bardziej poprawić jakość.</span><span class="sxs-lookup"><span data-stu-id="47c0e-180">However, being able to see the progress of our transfer *during* the transfer operation would be even better.</span></span> <span data-ttu-id="47c0e-181">Aby zrealizować ten scenariusz, należy utworzyć `TransferContext` obiektu.</span><span class="sxs-lookup"><span data-stu-id="47c0e-181">To achieve this scenario, we need to create a `TransferContext` object.</span></span> <span data-ttu-id="47c0e-182">`TransferContext` Obiektu jest dostarczany w dwóch formach: `SingleTransferContext` i `DirectoryTransferContext`.</span><span class="sxs-lookup"><span data-stu-id="47c0e-182">The `TransferContext` object comes in two forms: `SingleTransferContext` and `DirectoryTransferContext`.</span></span> <span data-ttu-id="47c0e-183">Jest transferowania jednym pliku (czyli co to jest robimy teraz) i jest on transferowania katalogu plików (które dodajemy później).</span><span class="sxs-lookup"><span data-stu-id="47c0e-183">The former is for transferring a single file (which is what we're doing now) and the latter is for transferring a directory of files (which we are adding later).</span></span>

<span data-ttu-id="47c0e-184">Dodaj metody `GetSingleTransferContext` i `GetDirectoryTransferContext` do `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="47c0e-184">Add the methods `GetSingleTransferContext` and `GetDirectoryTransferContext` to `Program.cs`:</span></span> 

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

<span data-ttu-id="47c0e-185">Modyfikowanie `TransferLocalFileToAzureBlob` metodę `GetSingleTransferContext`:</span><span class="sxs-lookup"><span data-stu-id="47c0e-185">Modify the `TransferLocalFileToAzureBlob` method to use `GetSingleTransferContext`:</span></span>

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

## <a name="resume-a-canceled-transfer"></a><span data-ttu-id="47c0e-186">Wznawianie transferu anulowane</span><span class="sxs-lookup"><span data-stu-id="47c0e-186">Resume a canceled transfer</span></span>
<span data-ttu-id="47c0e-187">Inna funkcja wygodny oferowane przez Biblioteka przenoszenia danych jest możliwość wznowić transfer anulowane.</span><span class="sxs-lookup"><span data-stu-id="47c0e-187">Another convenient feature offered by the Data Movement Library is the ability to resume a canceled transfer.</span></span> <span data-ttu-id="47c0e-188">Dodajmy trochę kodu umożliwiający tymczasowo anulować transfer wpisując `c`, a następnie Wznów transferu 3 sekundy później.</span><span class="sxs-lookup"><span data-stu-id="47c0e-188">Let's add some code that allows us to temporarily cancel the transfer by typing `c`, and then resume the transfer 3 seconds later.</span></span>

<span data-ttu-id="47c0e-189">Modyfikowanie `TransferLocalFileToAzureBlob`:</span><span class="sxs-lookup"><span data-stu-id="47c0e-189">Modify `TransferLocalFileToAzureBlob`:</span></span>

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' to temporarily cancel your transfer...\n");

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

<span data-ttu-id="47c0e-190">Dotychczas naszych `checkpoint` zawsze ustawiono wartość `null`.</span><span class="sxs-lookup"><span data-stu-id="47c0e-190">Up until now, our `checkpoint` value has always been set to `null`.</span></span> <span data-ttu-id="47c0e-191">Teraz wycofanie transferu możemy pobrać ostatniego punktu kontrolnego wynoszącego naszego przenoszenia, a następnie użyj tego nowego punktu kontrolnego w kontekście naszego przenoszenia.</span><span class="sxs-lookup"><span data-stu-id="47c0e-191">Now, if we cancel the transfer, we retrieve the last checkpoint of our transfer, then use this new checkpoint in our transfer context.</span></span> 

## <a name="transfer-local-directory-to-azure-blob-directory"></a><span data-ttu-id="47c0e-192">Przesunięcia katalogu lokalnego do katalogu obiektów Blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="47c0e-192">Transfer local directory to Azure Blob directory</span></span>
<span data-ttu-id="47c0e-193">Byłoby zadowalające, jeśli biblioteka przenoszenia danych w czasie może przekazać tylko jeden plik.</span><span class="sxs-lookup"><span data-stu-id="47c0e-193">It would be disappointing if the Data Movement Library could only transfer one file at a time.</span></span> <span data-ttu-id="47c0e-194">Na szczęście to nie jest wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="47c0e-194">Luckily, this is not the case.</span></span> <span data-ttu-id="47c0e-195">Biblioteka przenoszenia danych umożliwia transfer plików i wszystkich jego podkatalogach katalogu.</span><span class="sxs-lookup"><span data-stu-id="47c0e-195">The Data Movement Library provides the ability to transfer a directory of files and all of its subdirectories.</span></span> <span data-ttu-id="47c0e-196">Dodajmy trochę kodu, który pozwala spełniają właśnie tę funkcję.</span><span class="sxs-lookup"><span data-stu-id="47c0e-196">Let's add some code that allows us to do just that.</span></span>

<span data-ttu-id="47c0e-197">Najpierw dodaj metody `GetBlobDirectory` do `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="47c0e-197">First, add the method `GetBlobDirectory` to `Program.cs`:</span></span>

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

<span data-ttu-id="47c0e-198">Następnie należy zmodyfikować `TransferLocalDirectoryToAzureBlobDirectory`:</span><span class="sxs-lookup"><span data-stu-id="47c0e-198">Then, modify `TransferLocalDirectoryToAzureBlobDirectory`:</span></span>

```csharp
public static async Task TransferLocalDirectoryToAzureBlobDirectory(CloudStorageAccount account)
{ 
    string localDirectoryPath = GetSourcePath();
    CloudBlobDirectory blobDirectory = GetBlobDirectory(account); 
    TransferCheckpoint checkpoint = null;
    DirectoryTransferContext context = GetDirectoryTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' to temporarily cancel your transfer...\n");

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

<span data-ttu-id="47c0e-199">Istnieje kilka różnic między tą metodą a metoda przekazywania jednego pliku.</span><span class="sxs-lookup"><span data-stu-id="47c0e-199">There are a few differences between this method and the method for uploading a single file.</span></span> <span data-ttu-id="47c0e-200">Używamy teraz `TransferManager.UploadDirectoryAsync` i `getDirectoryTransferContext` metody utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="47c0e-200">We're now using `TransferManager.UploadDirectoryAsync` and the `getDirectoryTransferContext` method we created earlier.</span></span> <span data-ttu-id="47c0e-201">Ponadto obecnie udostępniamy `options` wartość naszych operacji przekazywania, co pozwala wskazać, że firma Microsoft ma należeć podkatalogi przesyłania.</span><span class="sxs-lookup"><span data-stu-id="47c0e-201">In addition, we now provide an `options` value to our upload operation, which allows us to indicate that we want to include subdirectories in our upload.</span></span> 

## <a name="copy-file-from-url-to-azure-blob"></a><span data-ttu-id="47c0e-202">Skopiuj plik z adresu URL do obiektów Blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="47c0e-202">Copy file from URL to Azure Blob</span></span>
<span data-ttu-id="47c0e-203">Teraz możemy dodać kod, który pozwala kopiować pliki z adresu URL do obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="47c0e-203">Now, let's add code that allows us to copy a file from a URL to an Azure Blob.</span></span> 

<span data-ttu-id="47c0e-204">Modyfikowanie `TransferUrlToAzureBlob`:</span><span class="sxs-lookup"><span data-stu-id="47c0e-204">Modify `TransferUrlToAzureBlob`:</span></span>

```csharp
public static async Task TransferUrlToAzureBlob(CloudStorageAccount account)
{
    Uri uri = new Uri(GetSourcePath());
    CloudBlockBlob blob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' to temporarily cancel your transfer...\n");

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

<span data-ttu-id="47c0e-205">Jeden przypadek użycia ważne dla tej funkcji jest, gdy trzeba przenieść danych z innej usługi w chmurze (np. AWS) na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="47c0e-205">One important use case for this feature is when you need to move data from another cloud service (e.g. AWS) to Azure.</span></span> <span data-ttu-id="47c0e-206">Zawiera adres URL, który umożliwia dostęp do zasobu, można łatwo przenosić tego zasobu w obiektach blob Azure przy użyciu `TransferManager.CopyAsync` metody.</span><span class="sxs-lookup"><span data-stu-id="47c0e-206">As long as you have a URL that gives you access to the resource, you can easily move that resource into Azure Blobs by using the `TransferManager.CopyAsync` method.</span></span> <span data-ttu-id="47c0e-207">Ta metoda wprowadza również nowe parametrów typu boolean.</span><span class="sxs-lookup"><span data-stu-id="47c0e-207">This method also introduces a new boolean parameter.</span></span> <span data-ttu-id="47c0e-208">Ustawienie tego parametru `true` wskazuje chęć wykonaj asynchroniczne kopiowania po stronie serwera.</span><span class="sxs-lookup"><span data-stu-id="47c0e-208">Setting this parameter to `true` indicates that we want to do an asynchronous server-side copy.</span></span> <span data-ttu-id="47c0e-209">Ustawienie tego parametru `false` wskazuje synchroniczne kopię - oznacza zasób jest najpierw pobierany do naszej komputera lokalnego, a następnie przekazać do obiektu Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="47c0e-209">Setting this parameter to `false` indicates a synchronous copy - meaning the resource is downloaded to our local machine first, then uploaded to Azure Blob.</span></span> <span data-ttu-id="47c0e-210">Jednak synchronicznego kopiowania jest obecnie dostępna tylko do skopiowania z jednego zasobu usługi Magazyn Azure.</span><span class="sxs-lookup"><span data-stu-id="47c0e-210">However, synchronous copy is currently only available for copying from one Azure Storage resource to another.</span></span> 

## <a name="transfer-azure-blob-to-azure-blob"></a><span data-ttu-id="47c0e-211">Przenoszenie obiektów Blob platformy Azure do obiektów Blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="47c0e-211">Transfer Azure Blob to Azure Blob</span></span>
<span data-ttu-id="47c0e-212">Inna funkcja jednoznacznie zapewnianej przez Biblioteka przenoszenia danych jest możliwość kopiowania z jednego zasobu magazynu Azure do innego.</span><span class="sxs-lookup"><span data-stu-id="47c0e-212">Another feature that's uniquely provided by the Data Movement Library is the ability to copy from one Azure Storage resource to another.</span></span> 

<span data-ttu-id="47c0e-213">Modyfikowanie `TransferAzureBlobToAzureBlob`:</span><span class="sxs-lookup"><span data-stu-id="47c0e-213">Modify `TransferAzureBlobToAzureBlob`:</span></span>

```csharp
public static async Task TransferAzureBlobToAzureBlob(CloudStorageAccount account)
{
    CloudBlockBlob sourceBlob = GetBlob(account);
    CloudBlockBlob destinationBlob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' to temporarily cancel your transfer...\n");

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

<span data-ttu-id="47c0e-214">W tym przykładzie firma Microsoft ustaw dla parametru logicznych `TransferManager.CopyAsync` do `false` wskazująca chęć wykonaj kopię synchronicznego.</span><span class="sxs-lookup"><span data-stu-id="47c0e-214">In this example, we set the boolean parameter in `TransferManager.CopyAsync` to `false` to indicate that we want to do a synchronous copy.</span></span> <span data-ttu-id="47c0e-215">Oznacza to, czy zasób jest najpierw pobierany do naszej komputera lokalnego, a następnie przekazać do obiektu Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="47c0e-215">This means that the resource is downloaded to our local machine first, then uploaded to Azure Blob.</span></span> <span data-ttu-id="47c0e-216">Opcja synchronicznego kopiowania jest doskonały sposób, aby upewnić się, że operacji kopiowania ma spójne szybkości.</span><span class="sxs-lookup"><span data-stu-id="47c0e-216">The synchronous copy option is a great way to ensure that your copy operation has a consistent speed.</span></span> <span data-ttu-id="47c0e-217">Z kolei szybkości asynchroniczne kopiowania po stronie serwera jest zależny od dostępną przepustowość sieci na serwerze, które mogą się zmieniać.</span><span class="sxs-lookup"><span data-stu-id="47c0e-217">In contrast, the speed of an asynchronous server-side copy is dependent on the available network bandwidth on the server, which can fluctuate.</span></span> <span data-ttu-id="47c0e-218">Jednak synchronicznych kopii może wygenerować dodatkowe wyjście koszt w porównaniu do kopiowania asynchronicznego.</span><span class="sxs-lookup"><span data-stu-id="47c0e-218">However, synchronous copy may generate additional egress cost compared to asynchronous copy.</span></span> <span data-ttu-id="47c0e-219">Zalecanym podejściem jest Użyj synchronicznych kopii w maszynie Wirtualnej platformy Azure, który znajduje się w tym samym regionie co konta magazynu źródłowego, aby uniknąć kosztów wyjście.</span><span class="sxs-lookup"><span data-stu-id="47c0e-219">The recommended approach is to use synchronous copy in an Azure VM that is in the same region as your source storage account to avoid egress cost.</span></span>

## <a name="conclusion"></a><span data-ttu-id="47c0e-220">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="47c0e-220">Conclusion</span></span>
<span data-ttu-id="47c0e-221">Naszej aplikacji przepływu danych jest teraz ukończona.</span><span class="sxs-lookup"><span data-stu-id="47c0e-221">Our data movement application is now complete.</span></span> <span data-ttu-id="47c0e-222">[Przykład pełny kod jest dostępny w witrynie GitHub](https://github.com/azure-samples/storage-dotnet-data-movement-library-app).</span><span class="sxs-lookup"><span data-stu-id="47c0e-222">[The full code sample is available on GitHub](https://github.com/azure-samples/storage-dotnet-data-movement-library-app).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="47c0e-223">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="47c0e-223">Next steps</span></span>
<span data-ttu-id="47c0e-224">W tym wprowadzenie, utworzyliśmy aplikację, która współdziała z usługą Azure Storage i działa w systemach Windows, Linux i macOS.</span><span class="sxs-lookup"><span data-stu-id="47c0e-224">In this getting started, we created an application that interacts with Azure Storage and runs on Windows, Linux, and macOS.</span></span> <span data-ttu-id="47c0e-225">Rozpoczęto pobieranie ukierunkowanych na magazyn obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="47c0e-225">This getting started focused on Blob Storage.</span></span> <span data-ttu-id="47c0e-226">Jednak ten sam wiedzy może odnosić się do przechowywania plików.</span><span class="sxs-lookup"><span data-stu-id="47c0e-226">However, this same knowledge can be applied to File Storage.</span></span> <span data-ttu-id="47c0e-227">Aby dowiedzieć się więcej, zapoznaj się [Biblioteka przenoszenia danych magazynu Azure dokumentacji](https://azure.github.io/azure-storage-net-data-movement).</span><span class="sxs-lookup"><span data-stu-id="47c0e-227">To learn more, check out [Azure Storage Data Movement Library reference documentation](https://azure.github.io/azure-storage-net-data-movement).</span></span>

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]




