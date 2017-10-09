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
ms.openlocfilehash: 9aec6cb171f794cc6ca432938ce499079e7dfdec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-hello-microsoft-azure-storage-data-movement-library"></a><span data-ttu-id="b2428-105">Transfer danych z hello Biblioteka przenoszenia danych Microsoft Azure Storage</span><span class="sxs-lookup"><span data-stu-id="b2428-105">Transfer Data with hello Microsoft Azure Storage Data Movement Library</span></span>

## <a name="overview"></a><span data-ttu-id="b2428-106">Omówienie</span><span class="sxs-lookup"><span data-stu-id="b2428-106">Overview</span></span>
<span data-ttu-id="b2428-107">Witaj Biblioteka przenoszenia danych Microsoft Azure Storage jest biblioteki typu open source i platform, która jest przeznaczona dla wysokiej wydajności, przekazywanie, pobieranie i kopiowania plików i obiektów blob magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="b2428-107">hello Microsoft Azure Storage Data Movement Library is a cross-platform open source library that is designed for high performance uploading, downloading, and copying of Azure Storage Blobs and Files.</span></span> <span data-ttu-id="b2428-108">Ta biblioteka jest hello podstawowym środowisku przenoszenia danych obsługującego [AzCopy](../storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="b2428-108">This library is hello core data movement framework that powers [AzCopy](../storage-use-azcopy.md).</span></span> <span data-ttu-id="b2428-109">Hello Biblioteka przenoszenia danych udostępnia wygodne metody, które nie są dostępne w przypadku naszego tradycyjnych [biblioteki klienta magazynu Azure .NET](../blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="b2428-109">hello Data Movement Library provides convenient methods that aren't available in our traditional [.NET Azure Storage Client Library](../blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="b2428-110">Dotyczy to również hello możliwości tooset hello liczbę operacji równoległych, śledzenie postępu przenoszenia, łatwe wznawianie transferu anulowane i o wiele więcej.</span><span class="sxs-lookup"><span data-stu-id="b2428-110">This includes hello ability tooset hello number of parallel operations, track transfer progress, easily resume a canceled transfer, and much more.</span></span>  

<span data-ttu-id="b2428-111">Ta biblioteka używa również .NET Core, co oznacza, że użytkownik może być używany podczas tworzenia aplikacji programu .NET dla systemu Windows, Linux i macOS.</span><span class="sxs-lookup"><span data-stu-id="b2428-111">This library also uses .NET Core, which means you can use it when building .NET apps for Windows, Linux and macOS.</span></span> <span data-ttu-id="b2428-112">toolearn więcej informacji na temat platformy .NET Core, zobacz toohello [dokumentacji platformy .NET Core](https://dotnet.github.io/).</span><span class="sxs-lookup"><span data-stu-id="b2428-112">toolearn more about .NET Core, refer toohello [.NET Core documentation](https://dotnet.github.io/).</span></span> <span data-ttu-id="b2428-113">Ta biblioteka działa także dla tradycyjnej aplikacji .NET Framework dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="b2428-113">This library also works for traditional .NET Framework apps for Windows.</span></span> 

<span data-ttu-id="b2428-114">W tym dokumencie przedstawiono sposób toocreate .NET Core konsoli aplikacji, która działa w systemach Windows, Linux i macOS i wykonuje hello następujące scenariusze:</span><span class="sxs-lookup"><span data-stu-id="b2428-114">This document demonstrates how toocreate a .NET Core console application that that runs on Windows, Linux, and macOS and performs hello following scenarios:</span></span>

- <span data-ttu-id="b2428-115">Przekazywanie plików i katalogów tooBlob magazynu.</span><span class="sxs-lookup"><span data-stu-id="b2428-115">Upload files and directories tooBlob Storage.</span></span>
- <span data-ttu-id="b2428-116">Podczas transferu danych, należy zdefiniować hello liczbę operacji równoległych.</span><span class="sxs-lookup"><span data-stu-id="b2428-116">Define hello number of parallel operations when transferring data.</span></span>
- <span data-ttu-id="b2428-117">Śledź postęp transferu danych.</span><span class="sxs-lookup"><span data-stu-id="b2428-117">Track data transfer progress.</span></span>
- <span data-ttu-id="b2428-118">Transfer danych Wznów anulowane.</span><span class="sxs-lookup"><span data-stu-id="b2428-118">Resume canceled data transfer.</span></span> 
- <span data-ttu-id="b2428-119">Skopiuj plik z tooBlob adres URL magazynu.</span><span class="sxs-lookup"><span data-stu-id="b2428-119">Copy file from URL tooBlob Storage.</span></span> 
- <span data-ttu-id="b2428-120">Kopiowanie z magazynu obiektów Blob tooBlob magazynu.</span><span class="sxs-lookup"><span data-stu-id="b2428-120">Copy from Blob Storage tooBlob Storage.</span></span>

<span data-ttu-id="b2428-121">**Co jest potrzebne:**</span><span class="sxs-lookup"><span data-stu-id="b2428-121">**What you need:**</span></span>

* [<span data-ttu-id="b2428-122">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="b2428-122">Visual Studio Code</span></span>](https://code.visualstudio.com/)
* <span data-ttu-id="b2428-123">[Konto usługi Azure Storage](storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="b2428-123">An [Azure storage account](storage-create-storage-account.md#create-a-storage-account)</span></span>

> [!NOTE]
> <span data-ttu-id="b2428-124">W tym przewodniku założono, że czytelnik zna już [usługi Azure Storage](https://azure.microsoft.com/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="b2428-124">This guide assumes that you are already familiar with [Azure Storage](https://azure.microsoft.com/services/storage/).</span></span> <span data-ttu-id="b2428-125">Jeśli nie, odczytywanie hello [tooAzure wprowadzenie magazynu](storage-introduction.md) warto dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="b2428-125">If not, reading hello [Introduction tooAzure Storage](storage-introduction.md) documentation is helpful.</span></span> <span data-ttu-id="b2428-126">Przede wszystkim należy się zbyt[Utwórz konto magazynu](storage-create-storage-account.md#create-a-storage-account) przy użyciu toostart hello Biblioteka przenoszenia danych.</span><span class="sxs-lookup"><span data-stu-id="b2428-126">Most importantly, you need too[create a Storage account](storage-create-storage-account.md#create-a-storage-account) toostart using hello Data Movement Library.</span></span>
> 
> 

## <a name="setup"></a><span data-ttu-id="b2428-127">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="b2428-127">Setup</span></span>  

1. <span data-ttu-id="b2428-128">Odwiedź hello [Przewodnik instalacji programu .NET Core](https://www.microsoft.com/net/core) tooinstall .NET Core.</span><span class="sxs-lookup"><span data-stu-id="b2428-128">Visit hello [.NET Core Installation Guide](https://www.microsoft.com/net/core) tooinstall .NET Core.</span></span> <span data-ttu-id="b2428-129">Wybierz opcję wiersza polecenia hello, wybierając środowiska.</span><span class="sxs-lookup"><span data-stu-id="b2428-129">When selecting your environment, choose hello command-line option.</span></span> 
2. <span data-ttu-id="b2428-130">Z wiersza polecenia hello Utwórz katalog projektu.</span><span class="sxs-lookup"><span data-stu-id="b2428-130">From hello command line, create a directory for your project.</span></span> <span data-ttu-id="b2428-131">Przejdź do tego katalogu, wpisz `dotnet new` projekt konsoli toocreate C#.</span><span class="sxs-lookup"><span data-stu-id="b2428-131">Navigate into this directory, then type `dotnet new` toocreate a C# console project.</span></span>
3. <span data-ttu-id="b2428-132">Otwórz ustawienia tego katalogu w Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="b2428-132">Open this directory in Visual Studio Code.</span></span> <span data-ttu-id="b2428-133">Ten krok można szybko zrobić przy użyciu wiersza polecenia hello wpisując `code .`.</span><span class="sxs-lookup"><span data-stu-id="b2428-133">This step can be quickly done via hello command line by typing `code .`.</span></span>  
4. <span data-ttu-id="b2428-134">Zainstaluj hello [C# rozszerzenia](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) z hello Visual Studio Marketplace kodu.</span><span class="sxs-lookup"><span data-stu-id="b2428-134">Install hello [C# extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) from hello Visual Studio Code Marketplace.</span></span> <span data-ttu-id="b2428-135">Uruchom ponownie program Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="b2428-135">Restart Visual Studio Code.</span></span> 
5. <span data-ttu-id="b2428-136">W tym momencie powinny zostać wyświetlone dwa monity.</span><span class="sxs-lookup"><span data-stu-id="b2428-136">At this point, you should see two prompts.</span></span> <span data-ttu-id="b2428-137">W przypadku dodawania "toobuild wymaganych zasobów i debugowania."</span><span class="sxs-lookup"><span data-stu-id="b2428-137">One is for adding "required assets toobuild and debug."</span></span> <span data-ttu-id="b2428-138">Kliknij przycisk "tak".</span><span class="sxs-lookup"><span data-stu-id="b2428-138">Click "yes."</span></span> <span data-ttu-id="b2428-139">Innego wiersza jest przywracania nierozwiązane zależności.</span><span class="sxs-lookup"><span data-stu-id="b2428-139">Another prompt is for restoring unresolved dependencies.</span></span> <span data-ttu-id="b2428-140">Kliknij pozycję "Przywróć".</span><span class="sxs-lookup"><span data-stu-id="b2428-140">Click "restore."</span></span>
6. <span data-ttu-id="b2428-141">Teraz powinien zawierać aplikacji `launch.json` plik pod hello `.vscode` katalogu.</span><span class="sxs-lookup"><span data-stu-id="b2428-141">Your application should now contain a `launch.json` file under hello `.vscode` directory.</span></span> <span data-ttu-id="b2428-142">W tym pliku, zmień hello `externalConsole` wartość zbyt`true`.</span><span class="sxs-lookup"><span data-stu-id="b2428-142">In this file, change hello `externalConsole` value too`true`.</span></span>
7. <span data-ttu-id="b2428-143">Visual Studio Code umożliwia toodebug aplikacji .NET Core.</span><span class="sxs-lookup"><span data-stu-id="b2428-143">Visual Studio Code allows you toodebug .NET Core applications.</span></span> <span data-ttu-id="b2428-144">Trafienia `F5` toorun aplikacji oraz zweryfikować konfigurację.</span><span class="sxs-lookup"><span data-stu-id="b2428-144">Hit `F5` toorun your application and verify that your setup is working.</span></span> <span data-ttu-id="b2428-145">Powinny pojawić się "Witaj świecie!"</span><span class="sxs-lookup"><span data-stu-id="b2428-145">You should see "Hello World!"</span></span> <span data-ttu-id="b2428-146">Konsola toohello wydruku.</span><span class="sxs-lookup"><span data-stu-id="b2428-146">printed toohello console.</span></span> 

## <a name="add-data-movement-library-tooyour-project"></a><span data-ttu-id="b2428-147">Dodaj projekt tooyour Biblioteka przenoszenia danych</span><span class="sxs-lookup"><span data-stu-id="b2428-147">Add Data Movement Library tooyour project</span></span>

1. <span data-ttu-id="b2428-148">Dodaj hello najnowszą wersję hello Biblioteka przenoszenia danych toohello `dependencies` części z `project.json` pliku.</span><span class="sxs-lookup"><span data-stu-id="b2428-148">Add hello latest version of hello Data Movement Library toohello `dependencies` section of your `project.json` file.</span></span> <span data-ttu-id="b2428-149">W czasie hello zapisu będzie tej wersji`"Microsoft.Azure.Storage.DataMovement": "0.5.0"`</span><span class="sxs-lookup"><span data-stu-id="b2428-149">At hello time of writing, this version would be `"Microsoft.Azure.Storage.DataMovement": "0.5.0"`</span></span> 
2. <span data-ttu-id="b2428-150">Dodaj `"portable-net45+win8"` toohello `imports` sekcji.</span><span class="sxs-lookup"><span data-stu-id="b2428-150">Add `"portable-net45+win8"` toohello `imports` section.</span></span> 
3. <span data-ttu-id="b2428-151">Wiersz powinien być wyświetlany toorestore Twojego projektu.</span><span class="sxs-lookup"><span data-stu-id="b2428-151">A prompt should display toorestore your project.</span></span> <span data-ttu-id="b2428-152">Kliknij przycisk "Przywróć" hello.</span><span class="sxs-lookup"><span data-stu-id="b2428-152">Click hello "restore" button.</span></span> <span data-ttu-id="b2428-153">Można też przywrócić projektu z wiersza polecenia hello, wpisując polecenie hello `dotnet restore` w głównym hello katalogu projektu.</span><span class="sxs-lookup"><span data-stu-id="b2428-153">You can also restore your project from hello command line by typing hello command `dotnet restore` in hello root of your project directory.</span></span>

<span data-ttu-id="b2428-154">Modyfikowanie `project.json`:</span><span class="sxs-lookup"><span data-stu-id="b2428-154">Modify `project.json`:</span></span>

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

## <a name="set-up-hello-skeleton-of-your-application"></a><span data-ttu-id="b2428-155">Konfigurowanie hello szkielet aplikacji</span><span class="sxs-lookup"><span data-stu-id="b2428-155">Set up hello skeleton of your application</span></span>
<span data-ttu-id="b2428-156">Witaj najpierw nie skonfigurowano kodu "szkielet" hello naszej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b2428-156">hello first thing we do is set up hello "skeleton" code of our application.</span></span> <span data-ttu-id="b2428-157">Ten kod wyświetla monit o nas dla konta magazynu kluczy nazwy i konta i używa tych poświadczeń toocreate `CloudStorageAccount` obiektu.</span><span class="sxs-lookup"><span data-stu-id="b2428-157">This code prompts us for a Storage account name and account key and uses those credentials toocreate a `CloudStorageAccount` object.</span></span> <span data-ttu-id="b2428-158">Ten obiekt jest używany toointeract z nasze konto magazynu we wszystkich scenariuszach transferu.</span><span class="sxs-lookup"><span data-stu-id="b2428-158">This object is used toointeract with our Storage account in all transfer scenarios.</span></span> <span data-ttu-id="b2428-159">Kod Hello również monituje nam toochoose hello rodzaj operacji transferu chcielibyśmy tooexecute.</span><span class="sxs-lookup"><span data-stu-id="b2428-159">hello code also prompts us toochoose hello type of transfer operation we would like tooexecute.</span></span> 

<span data-ttu-id="b2428-160">Modyfikowanie `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="b2428-160">Modify `Program.cs`:</span></span>

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

## <a name="transfer-local-file-tooazure-blob"></a><span data-ttu-id="b2428-161">Transfer pliku lokalnego tooAzure obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="b2428-161">Transfer local file tooAzure Blob</span></span>
<span data-ttu-id="b2428-162">Dodaj metody hello `GetSourcePath` i `GetBlob` zbyt`Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="b2428-162">Add hello methods `GetSourcePath` and `GetBlob` too`Program.cs`:</span></span>

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

<span data-ttu-id="b2428-163">Modyfikowanie hello `TransferLocalFileToAzureBlob` metody:</span><span class="sxs-lookup"><span data-stu-id="b2428-163">Modify hello `TransferLocalFileToAzureBlob` method:</span></span>

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

<span data-ttu-id="b2428-164">Ten kod nam monit o podanie ścieżki hello tooa pliku lokalnego, hello Nazwa nowego lub istniejącego kontenera i hello nazwę nowego obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="b2428-164">This code prompts us for hello path tooa local file, hello name of a new or existing container, and hello name of a new blob.</span></span> <span data-ttu-id="b2428-165">Witaj `TransferManager.UploadAsync` metoda przeprowadza hello przekazywania, korzystając z tych informacji.</span><span class="sxs-lookup"><span data-stu-id="b2428-165">hello `TransferManager.UploadAsync` method performs hello upload using this information.</span></span> 

<span data-ttu-id="b2428-166">Trafienia `F5` toorun aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b2428-166">Hit `F5` toorun your application.</span></span> <span data-ttu-id="b2428-167">Możesz sprawdzić, że przekazywania hello wystąpił wyświetlając konta magazynu z hello [Eksploratora usługi Microsoft Azure Storage](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="b2428-167">You can verify that hello upload occurred by viewing your Storage account with hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

## <a name="set-number-of-parallel-operations"></a><span data-ttu-id="b2428-168">Ustaw liczbę operacji równoległych</span><span class="sxs-lookup"><span data-stu-id="b2428-168">Set number of parallel operations</span></span>
<span data-ttu-id="b2428-169">Funkcja dużą oferowane przez hello Biblioteka przenoszenia danych jest hello możliwości tooset hello liczbę operacji równoległych tooincrease hello danych przeniesienie przepływności.</span><span class="sxs-lookup"><span data-stu-id="b2428-169">A great feature offered by hello Data Movement Library is hello ability tooset hello number of parallel operations tooincrease hello data transfer throughput.</span></span> <span data-ttu-id="b2428-170">Domyślnie program hello Biblioteka przenoszenia danych ustawia hello liczbę operacji równoległych too8 * hello liczba rdzeni na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="b2428-170">By default, hello Data Movement Library sets hello number of parallel operations too8 * hello number of cores on your machine.</span></span> 

<span data-ttu-id="b2428-171">Należy pamiętać, że wiele operacji równoległych w środowisku niskiej przepustowości może przeciąży hello połączenie sieciowe i faktycznie zapobiec operacji pełni zakończenie działania.</span><span class="sxs-lookup"><span data-stu-id="b2428-171">Keep in mind that many parallel operations in a low-bandwidth environment may overwhelm hello network connection and actually prevent operations from fully completing.</span></span> <span data-ttu-id="b2428-172">Będziesz potrzebować tooexperiment z tym toodetermine ustawienie co działa najlepiej oparte na na dostępną przepustowość sieci.</span><span class="sxs-lookup"><span data-stu-id="b2428-172">You'll need tooexperiment with this setting toodetermine what works best based on your available network bandwidth.</span></span> 

<span data-ttu-id="b2428-173">Dodajmy trochę kodu, który pozwala nam tooset hello liczbę operacji równoległych.</span><span class="sxs-lookup"><span data-stu-id="b2428-173">Let's add some code that allows us tooset hello number of parallel operations.</span></span> <span data-ttu-id="b2428-174">Umożliwia również Dodaj kod, który razy, jak długo hello toocomplete transferu.</span><span class="sxs-lookup"><span data-stu-id="b2428-174">Let's also add code that times how long it takes for hello transfer toocomplete.</span></span>

<span data-ttu-id="b2428-175">Dodaj `SetNumberOfParallelOperations` metody zbyt`Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="b2428-175">Add a `SetNumberOfParallelOperations` method too`Program.cs`:</span></span>

```csharp
public static void SetNumberOfParallelOperations()
{
    Console.WriteLine("\nHow many parallel operations would you like toouse?");
    string parallelOperations = Console.ReadLine();
    TransferManager.Configurations.ParallelOperations = int.Parse(parallelOperations);
}
```

<span data-ttu-id="b2428-176">Modyfikowanie hello `ExecuteChoice` toouse metody `SetNumberOfParallelOperations`:</span><span class="sxs-lookup"><span data-stu-id="b2428-176">Modify hello `ExecuteChoice` method toouse `SetNumberOfParallelOperations`:</span></span>

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

<span data-ttu-id="b2428-177">Modyfikowanie hello `TransferLocalFileToAzureBlob` toouse metody czasomierza:</span><span class="sxs-lookup"><span data-stu-id="b2428-177">Modify hello `TransferLocalFileToAzureBlob` method toouse a timer:</span></span>

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

## <a name="track-transfer-progress"></a><span data-ttu-id="b2428-178">Śledź postęp transferu</span><span class="sxs-lookup"><span data-stu-id="b2428-178">Track transfer progress</span></span>
<span data-ttu-id="b2428-179">Znajomość czas trwania dla naszych tootransfer danych jest doskonałym rozwiązaniem.</span><span class="sxs-lookup"><span data-stu-id="b2428-179">Knowing how long it took for our data tootransfer is great.</span></span> <span data-ttu-id="b2428-180">Jednak jest możliwe toosee postęp hello naszego przenoszenia *podczas* operacji transferu hello będą jeszcze bardziej poprawić jakość.</span><span class="sxs-lookup"><span data-stu-id="b2428-180">However, being able toosee hello progress of our transfer *during* hello transfer operation would be even better.</span></span> <span data-ttu-id="b2428-181">tooachieve tego scenariusza, potrzebujemy toocreate `TransferContext` obiektu.</span><span class="sxs-lookup"><span data-stu-id="b2428-181">tooachieve this scenario, we need toocreate a `TransferContext` object.</span></span> <span data-ttu-id="b2428-182">Witaj `TransferContext` obiektu jest dostarczany w dwóch formach: `SingleTransferContext` i `DirectoryTransferContext`.</span><span class="sxs-lookup"><span data-stu-id="b2428-182">hello `TransferContext` object comes in two forms: `SingleTransferContext` and `DirectoryTransferContext`.</span></span> <span data-ttu-id="b2428-183">wcześniejsze Hello jest przeznaczona przesyłania jednym pliku (czyli co to jest robimy teraz) i hello ostatnie transferowania katalogu plików (które dodajemy później).</span><span class="sxs-lookup"><span data-stu-id="b2428-183">hello former is for transferring a single file (which is what we're doing now) and hello latter is for transferring a directory of files (which we are adding later).</span></span>

<span data-ttu-id="b2428-184">Dodaj metody hello `GetSingleTransferContext` i `GetDirectoryTransferContext` zbyt`Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="b2428-184">Add hello methods `GetSingleTransferContext` and `GetDirectoryTransferContext` too`Program.cs`:</span></span> 

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

<span data-ttu-id="b2428-185">Modyfikowanie hello `TransferLocalFileToAzureBlob` toouse metody `GetSingleTransferContext`:</span><span class="sxs-lookup"><span data-stu-id="b2428-185">Modify hello `TransferLocalFileToAzureBlob` method toouse `GetSingleTransferContext`:</span></span>

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

## <a name="resume-a-canceled-transfer"></a><span data-ttu-id="b2428-186">Wznawianie transferu anulowane</span><span class="sxs-lookup"><span data-stu-id="b2428-186">Resume a canceled transfer</span></span>
<span data-ttu-id="b2428-187">Inna funkcja wygodny oferowane przez hello Biblioteka przenoszenia danych jest tooresume możliwości hello anulowane transferu.</span><span class="sxs-lookup"><span data-stu-id="b2428-187">Another convenient feature offered by hello Data Movement Library is hello ability tooresume a canceled transfer.</span></span> <span data-ttu-id="b2428-188">Dodajmy trochę kodu, który umożliwia transfer hello Anuluj tootemporarily, wpisując `c`, a następnie Wznów hello transfer później 3 sekundy.</span><span class="sxs-lookup"><span data-stu-id="b2428-188">Let's add some code that allows us tootemporarily cancel hello transfer by typing `c`, and then resume hello transfer 3 seconds later.</span></span>

<span data-ttu-id="b2428-189">Modyfikowanie `TransferLocalFileToAzureBlob`:</span><span class="sxs-lookup"><span data-stu-id="b2428-189">Modify `TransferLocalFileToAzureBlob`:</span></span>

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

<span data-ttu-id="b2428-190">Dotychczas naszych `checkpoint` wartość została ustawiona zawsze zbyt`null`.</span><span class="sxs-lookup"><span data-stu-id="b2428-190">Up until now, our `checkpoint` value has always been set too`null`.</span></span> <span data-ttu-id="b2428-191">Teraz Jeśli trwa anulowanie transferu hello, możemy pobrać hello ostatniego punktu kontrolnego naszego przenoszenia, a następnie używać tego nowego punktu kontrolnego w kontekście naszego przenoszenia.</span><span class="sxs-lookup"><span data-stu-id="b2428-191">Now, if we cancel hello transfer, we retrieve hello last checkpoint of our transfer, then use this new checkpoint in our transfer context.</span></span> 

## <a name="transfer-local-directory-tooazure-blob-directory"></a><span data-ttu-id="b2428-192">Transfer katalogu obiektu Blob tooAzure katalogu lokalnego</span><span class="sxs-lookup"><span data-stu-id="b2428-192">Transfer local directory tooAzure Blob directory</span></span>
<span data-ttu-id="b2428-193">Byłoby zadowalające hello Biblioteka przenoszenia danych w czasie może przekazać tylko jeden plik.</span><span class="sxs-lookup"><span data-stu-id="b2428-193">It would be disappointing if hello Data Movement Library could only transfer one file at a time.</span></span> <span data-ttu-id="b2428-194">Na szczęście to nie jest hello.</span><span class="sxs-lookup"><span data-stu-id="b2428-194">Luckily, this is not hello case.</span></span> <span data-ttu-id="b2428-195">Witaj Biblioteka przenoszenia danych zawiera tootransfer możliwości hello katalog plików i wszystkich jego podkatalogach.</span><span class="sxs-lookup"><span data-stu-id="b2428-195">hello Data Movement Library provides hello ability tootransfer a directory of files and all of its subdirectories.</span></span> <span data-ttu-id="b2428-196">Dodajmy trochę kodu umożliwiający wykonywanie toodo tylko dla niej.</span><span class="sxs-lookup"><span data-stu-id="b2428-196">Let's add some code that allows us toodo just that.</span></span>

<span data-ttu-id="b2428-197">Najpierw dodaj metody hello `GetBlobDirectory` zbyt`Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="b2428-197">First, add hello method `GetBlobDirectory` too`Program.cs`:</span></span>

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

<span data-ttu-id="b2428-198">Następnie należy zmodyfikować `TransferLocalDirectoryToAzureBlobDirectory`:</span><span class="sxs-lookup"><span data-stu-id="b2428-198">Then, modify `TransferLocalDirectoryToAzureBlobDirectory`:</span></span>

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

<span data-ttu-id="b2428-199">Istnieje kilka różnic między tej metody oraz metody hello przekazywania jednego pliku.</span><span class="sxs-lookup"><span data-stu-id="b2428-199">There are a few differences between this method and hello method for uploading a single file.</span></span> <span data-ttu-id="b2428-200">Używamy teraz `TransferManager.UploadDirectoryAsync` i hello `getDirectoryTransferContext` metody utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="b2428-200">We're now using `TransferManager.UploadDirectoryAsync` and hello `getDirectoryTransferContext` method we created earlier.</span></span> <span data-ttu-id="b2428-201">Ponadto obecnie udostępniamy `options` wartość tooour operacji przekazywania, która pozwala nam tooindicate chcemy tooinclude podkatalogów w przesyłania.</span><span class="sxs-lookup"><span data-stu-id="b2428-201">In addition, we now provide an `options` value tooour upload operation, which allows us tooindicate that we want tooinclude subdirectories in our upload.</span></span> 

## <a name="copy-file-from-url-tooazure-blob"></a><span data-ttu-id="b2428-202">Skopiuj plik z tooAzure adresu URL obiektu Blob</span><span class="sxs-lookup"><span data-stu-id="b2428-202">Copy file from URL tooAzure Blob</span></span>
<span data-ttu-id="b2428-203">Teraz możemy dodać kod, który pozwala nam toocopy pliku z adresu URL tooan obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b2428-203">Now, let's add code that allows us toocopy a file from a URL tooan Azure Blob.</span></span> 

<span data-ttu-id="b2428-204">Modyfikowanie `TransferUrlToAzureBlob`:</span><span class="sxs-lookup"><span data-stu-id="b2428-204">Modify `TransferUrlToAzureBlob`:</span></span>

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

<span data-ttu-id="b2428-205">Jeden przypadek użycia ważne dla tej funkcji jest gdy będziesz potrzebować toomove dane z innego tooAzure usługi (np. AWS) w chmurze.</span><span class="sxs-lookup"><span data-stu-id="b2428-205">One important use case for this feature is when you need toomove data from another cloud service (e.g. AWS) tooAzure.</span></span> <span data-ttu-id="b2428-206">Tak długo, jak adres URL, który zapewnia dostęp toohello zasobów, tego zasobu można łatwo przenosić do obiektów blob Azure przy użyciu hello `TransferManager.CopyAsync` metody.</span><span class="sxs-lookup"><span data-stu-id="b2428-206">As long as you have a URL that gives you access toohello resource, you can easily move that resource into Azure Blobs by using hello `TransferManager.CopyAsync` method.</span></span> <span data-ttu-id="b2428-207">Ta metoda wprowadza również nowe parametrów typu boolean.</span><span class="sxs-lookup"><span data-stu-id="b2428-207">This method also introduces a new boolean parameter.</span></span> <span data-ttu-id="b2428-208">Ustawienie tego parametru zbyt`true` wskazuje, że firma Microsoft kopiowania toodo asynchronicznych po stronie serwera.</span><span class="sxs-lookup"><span data-stu-id="b2428-208">Setting this parameter too`true` indicates that we want toodo an asynchronous server-side copy.</span></span> <span data-ttu-id="b2428-209">Ustawienie tego parametru zbyt`false` wskazuje synchronicznych kopii - oznacza zasób hello jest pobrany tooour komputera lokalnego, następnie przekazać tooAzure obiektu Blob.</span><span class="sxs-lookup"><span data-stu-id="b2428-209">Setting this parameter too`false` indicates a synchronous copy - meaning hello resource is downloaded tooour local machine first, then uploaded tooAzure Blob.</span></span> <span data-ttu-id="b2428-210">Jednak synchronicznego kopiowania jest obecnie dostępna tylko do kopiowania z jednego tooanother zasobów usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="b2428-210">However, synchronous copy is currently only available for copying from one Azure Storage resource tooanother.</span></span> 

## <a name="transfer-azure-blob-tooazure-blob"></a><span data-ttu-id="b2428-211">Transfer tooAzure obiektów Blob platformy Azure Blob</span><span class="sxs-lookup"><span data-stu-id="b2428-211">Transfer Azure Blob tooAzure Blob</span></span>
<span data-ttu-id="b2428-212">Inna funkcja jednoznacznie zapewnianej przez hello Biblioteka przenoszenia danych jest toocopy możliwości hello z jednego tooanother zasobów usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="b2428-212">Another feature that's uniquely provided by hello Data Movement Library is hello ability toocopy from one Azure Storage resource tooanother.</span></span> 

<span data-ttu-id="b2428-213">Modyfikowanie `TransferAzureBlobToAzureBlob`:</span><span class="sxs-lookup"><span data-stu-id="b2428-213">Modify `TransferAzureBlobToAzureBlob`:</span></span>

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

<span data-ttu-id="b2428-214">W tym przykładzie parametr logiczna hello umieszczania `TransferManager.CopyAsync` zbyt`false` tooindicate czy chcemy toodo synchronicznych kopii.</span><span class="sxs-lookup"><span data-stu-id="b2428-214">In this example, we set hello boolean parameter in `TransferManager.CopyAsync` too`false` tooindicate that we want toodo a synchronous copy.</span></span> <span data-ttu-id="b2428-215">Oznacza to, że hello zasobów jest najpierw pobrany tooour komputera lokalnego, a następnie przekazać tooAzure obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="b2428-215">This means that hello resource is downloaded tooour local machine first, then uploaded tooAzure Blob.</span></span> <span data-ttu-id="b2428-216">Opcja synchronicznych kopii Hello jest tooensure doskonały sposób, że operacji kopiowania ma spójne szybkości.</span><span class="sxs-lookup"><span data-stu-id="b2428-216">hello synchronous copy option is a great way tooensure that your copy operation has a consistent speed.</span></span> <span data-ttu-id="b2428-217">Z kolei szybkości hello asynchroniczne kopii po stronie serwera jest zależny od hello dostępną przepustowość sieci na powitania serwera, który mogą się zmieniać.</span><span class="sxs-lookup"><span data-stu-id="b2428-217">In contrast, hello speed of an asynchronous server-side copy is dependent on hello available network bandwidth on hello server, which can fluctuate.</span></span> <span data-ttu-id="b2428-218">Jednak synchronicznych kopii może wygenerować dodatkowe wyjście koszt w porównaniu tooasynchronous kopiowania.</span><span class="sxs-lookup"><span data-stu-id="b2428-218">However, synchronous copy may generate additional egress cost compared tooasynchronous copy.</span></span> <span data-ttu-id="b2428-219">Witaj zalecane podejście jest toouse synchronicznych kopii w maszynie Wirtualnej platformy Azure, który znajduje się w hello tego samego regionu koszt wyjście tooavoid konta magazynu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="b2428-219">hello recommended approach is toouse synchronous copy in an Azure VM that is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="conclusion"></a><span data-ttu-id="b2428-220">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="b2428-220">Conclusion</span></span>
<span data-ttu-id="b2428-221">Naszej aplikacji przepływu danych jest teraz ukończona.</span><span class="sxs-lookup"><span data-stu-id="b2428-221">Our data movement application is now complete.</span></span> <span data-ttu-id="b2428-222">[przykład pełny kod Hello jest dostępny w witrynie GitHub](https://github.com/azure-samples/storage-dotnet-data-movement-library-app).</span><span class="sxs-lookup"><span data-stu-id="b2428-222">[hello full code sample is available on GitHub](https://github.com/azure-samples/storage-dotnet-data-movement-library-app).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b2428-223">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b2428-223">Next steps</span></span>
<span data-ttu-id="b2428-224">W tym wprowadzenie, utworzyliśmy aplikację, która współdziała z usługą Azure Storage i działa w systemach Windows, Linux i macOS.</span><span class="sxs-lookup"><span data-stu-id="b2428-224">In this getting started, we created an application that interacts with Azure Storage and runs on Windows, Linux, and macOS.</span></span> <span data-ttu-id="b2428-225">Rozpoczęto pobieranie ukierunkowanych na magazyn obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="b2428-225">This getting started focused on Blob Storage.</span></span> <span data-ttu-id="b2428-226">Jednak ten sam wiedzy może być zastosowane tooFile magazynu.</span><span class="sxs-lookup"><span data-stu-id="b2428-226">However, this same knowledge can be applied tooFile Storage.</span></span> <span data-ttu-id="b2428-227">toolearn więcej, zapoznaj się z [Biblioteka przenoszenia danych magazynu Azure dokumentacji](https://azure.github.io/azure-storage-net-data-movement).</span><span class="sxs-lookup"><span data-stu-id="b2428-227">toolearn more, check out [Azure Storage Data Movement Library reference documentation](https://azure.github.io/azure-storage-net-data-movement).</span></span>

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]




