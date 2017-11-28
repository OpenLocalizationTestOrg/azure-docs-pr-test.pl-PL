---
title: "Jak używać magazynu obiektów Blob platformy Azure z systemem iOS | Dokumentacja firmy Microsoft"
description: "Przechowuj dane niestrukturalne w chmurze za pomocą Magazynu obiektów blob Azure."
services: storage
documentationcenter: ios
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: df188021-86fc-4d31-a810-1b0e7bcd814b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: objective-c
ms.topic: article
ms.date: 05/11/2017
ms.author: michaelhauss
ms.openlocfilehash: b5f43156d46b1ab9dd10ff5a93427270c1b839ca
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-blob-storage-from-ios"></a><span data-ttu-id="e2868-103">Jak używać magazynu obiektów Blob z systemem iOS</span><span class="sxs-lookup"><span data-stu-id="e2868-103">How to use Blob storage from iOS</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="e2868-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="e2868-104">Overview</span></span>
<span data-ttu-id="e2868-105">W tym artykule opisano sposób wykonywania typowych scenariuszy przy użyciu magazynu obiektów Blob Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e2868-105">This article will show you how to perform common scenarios using Microsoft Azure Blob storage.</span></span> <span data-ttu-id="e2868-106">Przykłady są napisane w języku Objective C i użyj [biblioteki klienta magazynu Azure dla systemu iOS](https://github.com/Azure/azure-storage-ios).</span><span class="sxs-lookup"><span data-stu-id="e2868-106">The samples are written in Objective-C and use the [Azure Storage Client Library for iOS](https://github.com/Azure/azure-storage-ios).</span></span> <span data-ttu-id="e2868-107">Omówione scenariusze obejmują **przekazywania**, **wyświetlania**, **pobieranie**, i **usuwanie** obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="e2868-107">The scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="e2868-108">Aby uzyskać więcej informacji dotyczących obiektów blob, zobacz [następne kroki](#next-steps) sekcji.</span><span class="sxs-lookup"><span data-stu-id="e2868-108">For more information on blobs, see the [Next Steps](#next-steps) section.</span></span> <span data-ttu-id="e2868-109">Możesz również pobrać [Przykładowa aplikacja](https://github.com/Azure/azure-storage-ios/tree/master/BlobSample) szybko wyświetlić korzystanie z usługi Azure Storage w aplikacji systemu iOS.</span><span class="sxs-lookup"><span data-stu-id="e2868-109">You can also download the [sample app](https://github.com/Azure/azure-storage-ios/tree/master/BlobSample) to quickly see the use of Azure Storage in an iOS application.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="import-the-azure-storage-ios-library-into-your-application"></a><span data-ttu-id="e2868-110">Importowanie biblioteki z systemem iOS magazynu Azure do aplikacji</span><span class="sxs-lookup"><span data-stu-id="e2868-110">Import the Azure Storage iOS library into your application</span></span>
<span data-ttu-id="e2868-111">Możesz zaimportować biblioteki z systemem iOS magazynu Azure do aplikacji przy użyciu [CocoaPod magazynu Azure](https://cocoapods.org/pods/AZSClient) lub importując **Framework** pliku.</span><span class="sxs-lookup"><span data-stu-id="e2868-111">You can import the Azure Storage iOS library into your application either by using the [Azure Storage CocoaPod](https://cocoapods.org/pods/AZSClient) or by importing the **Framework** file.</span></span> <span data-ttu-id="e2868-112">CocoaPod jest zalecany, ponieważ ułatwia integrowanie łatwiejsze, jednak importowania z pliku framework jest ta opcja jest mniej pożądana dla istniejącego projektu biblioteki.</span><span class="sxs-lookup"><span data-stu-id="e2868-112">CocoaPod is the recommended way as it makes integrating the library easier, however importing from the framework file is less intrusive for your existing project.</span></span>

<span data-ttu-id="e2868-113">Aby użyć tej biblioteki, są potrzebne następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="e2868-113">To use this library, you need the following:</span></span>
- <span data-ttu-id="e2868-114">System iOS 8 i nowsze</span><span class="sxs-lookup"><span data-stu-id="e2868-114">iOS 8+</span></span>
- <span data-ttu-id="e2868-115">Xcode 7 +</span><span class="sxs-lookup"><span data-stu-id="e2868-115">Xcode 7+</span></span>

## <a name="cocoapod"></a><span data-ttu-id="e2868-116">CocoaPod</span><span class="sxs-lookup"><span data-stu-id="e2868-116">CocoaPod</span></span>
1. <span data-ttu-id="e2868-117">Jeśli użytkownik jeszcze tego nie zrobiono, [instalacji programu CocoaPods](https://guides.cocoapods.org/using/getting-started.html#toc_3) na komputerze, otwierając okno terminalu i uruchom następujące polecenie</span><span class="sxs-lookup"><span data-stu-id="e2868-117">If you haven't done so already, [Install CocoaPods](https://guides.cocoapods.org/using/getting-started.html#toc_3) on your computer by opening a terminal window and running the following command</span></span>
    
    ```shell   
    sudo gem install cocoapods
    ```

2. <span data-ttu-id="e2868-118">Następnie w katalogu projektu (katalog zawierający plik .xcodeproj), Utwórz nowy plik o nazwie _Podfile_(bez rozszerzenia pliku).</span><span class="sxs-lookup"><span data-stu-id="e2868-118">Next, in the project directory (the directory containing your .xcodeproj file), create a new file called _Podfile_(no file extension).</span></span> <span data-ttu-id="e2868-119">Dodaj następujący kod do _Podfile_ i Zapisz.</span><span class="sxs-lookup"><span data-stu-id="e2868-119">Add the following to _Podfile_ and save.</span></span>

    ```ruby
    platform :ios, '8.0'

    target 'TargetName' do
      pod 'AZSClient'
    end
    ```

3. <span data-ttu-id="e2868-120">W oknie terminalu przejdź do katalogu projektu i uruchom następujące polecenie</span><span class="sxs-lookup"><span data-stu-id="e2868-120">In the terminal window, navigate to the project directory and run the following command</span></span>

    ```shell    
    pod install
    ```

4. <span data-ttu-id="e2868-121">Jeśli Twoje .xcodeproj jest otwarty w programie Xcode, należy go zamknąć.</span><span class="sxs-lookup"><span data-stu-id="e2868-121">If your .xcodeproj is open in Xcode, close it.</span></span> <span data-ttu-id="e2868-122">W katalogu projektu otwórz plik nowo utworzonego projektu, który ma rozszerzenie .xcworkspace.</span><span class="sxs-lookup"><span data-stu-id="e2868-122">In your project directory open the newly created project file which will have the .xcworkspace extension.</span></span> <span data-ttu-id="e2868-123">Jest to plik, który będzie skorzystać z dla teraz.</span><span class="sxs-lookup"><span data-stu-id="e2868-123">This is the file you'll work from for now on.</span></span>

## <a name="framework"></a><span data-ttu-id="e2868-124">Framework</span><span class="sxs-lookup"><span data-stu-id="e2868-124">Framework</span></span>
<span data-ttu-id="e2868-125">Innym sposobem korzystania z biblioteki jest skompilować platformę ręcznie:</span><span class="sxs-lookup"><span data-stu-id="e2868-125">The other way to use the library is to build the framework manually:</span></span>

1. <span data-ttu-id="e2868-126">Najpierw należy pobrać lub sklonować [repozytorium azure magazynu ios](https://github.com/azure/azure-storage-ios).</span><span class="sxs-lookup"><span data-stu-id="e2868-126">First, download or clone the [azure-storage-ios repo](https://github.com/azure/azure-storage-ios).</span></span>
2. <span data-ttu-id="e2868-127">Przejdź do *systemu ios magazynu azure* -> *Lib* -> *biblioteki klienta magazynu Azure*, a następnie otwórz `AZSClient.xcodeproj` w środowisku Xcode.</span><span class="sxs-lookup"><span data-stu-id="e2868-127">Go into *azure-storage-ios* -> *Lib* -> *Azure Storage Client Library*, and open `AZSClient.xcodeproj` in Xcode.</span></span>
3. <span data-ttu-id="e2868-128">W lewym górnym Xcode należy zmienić schemat active "Biblioteki klienta magazynu Azure" do "Framework".</span><span class="sxs-lookup"><span data-stu-id="e2868-128">At the top-left of Xcode, change the active scheme from "Azure Storage Client Library" to "Framework".</span></span>
4. <span data-ttu-id="e2868-129">Kompilacji projektu (⌘ + B).</span><span class="sxs-lookup"><span data-stu-id="e2868-129">Build the project (⌘+B).</span></span> <span data-ttu-id="e2868-130">Spowoduje to utworzenie `AZSClient.framework` plik na pulpicie.</span><span class="sxs-lookup"><span data-stu-id="e2868-130">This will create an `AZSClient.framework` file on your Desktop.</span></span>

<span data-ttu-id="e2868-131">Następnie można zaimportować plik framework w aplikacji, wykonując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="e2868-131">You can then import the framework file into your application by doing the following:</span></span>

1. <span data-ttu-id="e2868-132">Tworzenie nowego projektu lub otworzenie istniejącego projektu w środowisku Xcode.</span><span class="sxs-lookup"><span data-stu-id="e2868-132">Create a new project or open up your existing project in Xcode.</span></span>
2. <span data-ttu-id="e2868-133">Przeciągnij i upuść `AZSClient.framework` do Nawigatora projektu Xcode.</span><span class="sxs-lookup"><span data-stu-id="e2868-133">Drag and drop the `AZSClient.framework` into your Xcode project navigator.</span></span>
3. <span data-ttu-id="e2868-134">Wybierz *skopiować elementy w razie potrzeby*i kliknij przycisk *Zakończ*.</span><span class="sxs-lookup"><span data-stu-id="e2868-134">Select *Copy items if needed*, and click on *Finish*.</span></span>
4. <span data-ttu-id="e2868-135">Kliknij projekt w obszarze nawigacji po lewej stronie, a następnie kliknij przycisk *ogólne* kartę w górnej części edytora projektu.</span><span class="sxs-lookup"><span data-stu-id="e2868-135">Click on your project in the left-hand navigation and click the *General* tab at the top of the project editor.</span></span>
5. <span data-ttu-id="e2868-136">W obszarze *połączone struktury i biblioteki* sekcji, kliknij przycisk Dodaj (+).</span><span class="sxs-lookup"><span data-stu-id="e2868-136">Under the *Linked Frameworks and Libraries* section, click the Add button (+).</span></span>
6. <span data-ttu-id="e2868-137">Na liście bibliotek już dostarczona, wyszukaj `libxml2.2.tbd` i dodaj go do projektu.</span><span class="sxs-lookup"><span data-stu-id="e2868-137">In the list of libraries already provided, search for `libxml2.2.tbd` and add it to your project.</span></span>

## <a name="import-the-library"></a><span data-ttu-id="e2868-138">Importuj biblioteki</span><span class="sxs-lookup"><span data-stu-id="e2868-138">Import the Library</span></span> 
```objc
// Include the following import statement to use blob APIs.
#import <AZSClient/AZSClient.h>
```

<span data-ttu-id="e2868-139">Jeśli używasz Swift, konieczne będzie Utwórz nagłówek mostkowania i zaimportuj < AZSClient/AZSClient.h > istnieje:</span><span class="sxs-lookup"><span data-stu-id="e2868-139">If you are using Swift, you will need to create a bridging header and import <AZSClient/AZSClient.h> there:</span></span>

1. <span data-ttu-id="e2868-140">Utwórz plik nagłówka `Bridging-Header.h`i Dodaj powyżej instrukcję import.</span><span class="sxs-lookup"><span data-stu-id="e2868-140">Create a header file `Bridging-Header.h`, and add the above import statement.</span></span>
2. <span data-ttu-id="e2868-141">Przejdź do *ustawieniach kompilacji* , a następnie wyszukaj *nagłówków mostkowania języka Objective-C*.</span><span class="sxs-lookup"><span data-stu-id="e2868-141">Go to the *Build Settings* tab, and search for *Objective-C Bridging Header*.</span></span>
3. <span data-ttu-id="e2868-142">Kliknij dwukrotnie w zakresie *nagłówków mostkowania języka Objective-C* i Dodaj ścieżkę do pliku nagłówka:`ProjectName/Bridging-Header.h`</span><span class="sxs-lookup"><span data-stu-id="e2868-142">Double-click on the field of *Objective-C Bridging Header* and add the path to your header file: `ProjectName/Bridging-Header.h`</span></span>
4. <span data-ttu-id="e2868-143">Kompilacji projektu (⌘ + B), aby sprawdzić, czy nagłówek mostkowania została pobrana przez Xcode.</span><span class="sxs-lookup"><span data-stu-id="e2868-143">Build the project (⌘+B) to verify that the bridging header was picked up by Xcode.</span></span>
5. <span data-ttu-id="e2868-144">Rozpoczynanie korzystania z biblioteki bezpośrednio w żadnym pliku Swift, nie istnieje potrzeba dla instrukcje importu.</span><span class="sxs-lookup"><span data-stu-id="e2868-144">Start using the library directly in any Swift file, there is no need for import statements.</span></span>

[!INCLUDE [storage-mobile-authentication-guidance](../../../includes/storage-mobile-authentication-guidance.md)]

## <a name="asynchronous-operations"></a><span data-ttu-id="e2868-145">Operacje asynchroniczne</span><span class="sxs-lookup"><span data-stu-id="e2868-145">Asynchronous Operations</span></span>
> [!NOTE]
> <span data-ttu-id="e2868-146">Wszystkie metody, które wykonują żądania z usługą są operacji asynchronicznych.</span><span class="sxs-lookup"><span data-stu-id="e2868-146">All methods that perform a request against the service are asynchronous operations.</span></span> <span data-ttu-id="e2868-147">W przykładach kodu znajdziesz, że te metody ma obsługi zakończenia.</span><span class="sxs-lookup"><span data-stu-id="e2868-147">In the code samples, you'll find that these methods have a completion handler.</span></span> <span data-ttu-id="e2868-148">Uruchomi kodu wewnątrz obsługi uzupełniania **po** ukończyć żądania.</span><span class="sxs-lookup"><span data-stu-id="e2868-148">Code inside the completion handler will run **after** the request is completed.</span></span> <span data-ttu-id="e2868-149">Kod po zakończeniu obsługi zostanie uruchomiony **podczas** odbywa się żądanie.</span><span class="sxs-lookup"><span data-stu-id="e2868-149">Code after the completion handler will run **while** the request is being made.</span></span>
> 
> 

## <a name="create-a-container"></a><span data-ttu-id="e2868-150">Tworzenie kontenera</span><span class="sxs-lookup"><span data-stu-id="e2868-150">Create a container</span></span>
<span data-ttu-id="e2868-151">Każdy obiekt blob w magazynie Azure musi znajdować się w kontenerze.</span><span class="sxs-lookup"><span data-stu-id="e2868-151">Every blob in Azure Storage must reside in a container.</span></span> <span data-ttu-id="e2868-152">Poniższy przykład przedstawia sposób tworzenia kontenera o nazwie *newcontainer*, na Twoim koncie magazynu, jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="e2868-152">The following example shows how to create a container, called *newcontainer*, in your Storage account if it doesn't already exist.</span></span> <span data-ttu-id="e2868-153">W przypadku wybrania nazwy użytkownika kontenera, należy zachować ostrożność, reguły nazewnictwa wymienionych powyżej.</span><span class="sxs-lookup"><span data-stu-id="e2868-153">When choosing a name for your container, be mindful of the naming rules mentioned above.</span></span>

```objc
-(void)createContainer{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"newcontainer"];

    // Create container in your Storage account if the container doesn't already exist
    [blobContainer createContainerIfNotExistsWithCompletionHandler:^(NSError *error, BOOL exists) {
        if (error){
            NSLog(@"Error in creating container.");
        }
    }];
}
```

<span data-ttu-id="e2868-154">Można potwierdzić, że to działa, analizując [Eksploratora usługi Microsoft Azure Storage](http://storageexplorer.com) i sprawdzić, czy *newcontainer* znajduje się na liście kontenery konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="e2868-154">You can confirm that this works by looking at the [Microsoft Azure Storage Explorer](http://storageexplorer.com) and verifying that *newcontainer* is in the list of containers for your Storage account.</span></span>

## <a name="set-container-permissions"></a><span data-ttu-id="e2868-155">Ustaw uprawnienia do kontenera</span><span class="sxs-lookup"><span data-stu-id="e2868-155">Set Container Permissions</span></span>
<span data-ttu-id="e2868-156">Kontener uprawnienia są skonfigurowane dla **prywatnej** dostępu domyślnie.</span><span class="sxs-lookup"><span data-stu-id="e2868-156">A container's permissions are configured for **Private** access by default.</span></span> <span data-ttu-id="e2868-157">Kontenery zapewnia jednak kilka różnych opcji dla dostępu do kontenera:</span><span class="sxs-lookup"><span data-stu-id="e2868-157">However, containers provide a few different options for container access:</span></span>

* <span data-ttu-id="e2868-158">**Prywatne**: obiektów blob i kontenera danych mogą być odczytywane tylko właściciel konta.</span><span class="sxs-lookup"><span data-stu-id="e2868-158">**Private**: Container and blob data can be read by the account owner only.</span></span>
* <span data-ttu-id="e2868-159">**Obiekt blob**: dane obiektów Blob w tym kontenerze mogą być odczytywane za pomocą żądania od użytkowników anonimowych, ale nie są dostępne dane kontenera.</span><span class="sxs-lookup"><span data-stu-id="e2868-159">**Blob**: Blob data within this container can be read via anonymous request, but container data is not available.</span></span> <span data-ttu-id="e2868-160">Klienci nie można wyliczyć obiektów blob w kontenerze, za pomocą żądania od użytkowników anonimowych.</span><span class="sxs-lookup"><span data-stu-id="e2868-160">Clients cannot enumerate blobs within the container via anonymous request.</span></span>
* <span data-ttu-id="e2868-161">**Kontener**: obiektów blob i kontenera danych mogą być odczytywane za pomocą żądania od użytkowników anonimowych.</span><span class="sxs-lookup"><span data-stu-id="e2868-161">**Container**: Container and blob data can be read via anonymous request.</span></span> <span data-ttu-id="e2868-162">Klientów można wyliczyć obiektów blob w kontenerze, za pomocą żądania od użytkowników anonimowych, ale nie można wyliczyć kontenery w ramach konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="e2868-162">Clients can enumerate blobs within the container via anonymous request, but cannot enumerate containers within the storage account.</span></span>

<span data-ttu-id="e2868-163">Poniższy przykład przedstawia sposób tworzenia kontenera o **kontenera** dostępu uprawnienia, które pozwoli na dostęp publiczny, tylko do odczytu dla wszystkich użytkowników w Internecie:</span><span class="sxs-lookup"><span data-stu-id="e2868-163">The following example shows you how to create a container with **Container** access permissions, which will allow public, read-only access for all users on the Internet:</span></span>

```objc
-(void)createContainerWithPublicAccess{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    // Create container in your Storage account if the container doesn't already exist
    [blobContainer createContainerIfNotExistsWithAccessType:AZSContainerPublicAccessTypeContainer requestOptions:nil operationContext:nil completionHandler:^(NSError *error, BOOL exists){
        if (error){
            NSLog(@"Error in creating container.");
        }
    }];
}
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="e2868-164">Przekazywanie obiektu blob do kontenera</span><span class="sxs-lookup"><span data-stu-id="e2868-164">Upload a blob into a container</span></span>
<span data-ttu-id="e2868-165">Jak wspomniano w [pojęcia dotyczące usługi Blob](#blob-service-concepts) sekcji magazynu obiektów Blob udostępnia trzy typy obiektów blob: blokowe obiekty BLOB, uzupełnialnych obiektów blob i stronicowe.</span><span class="sxs-lookup"><span data-stu-id="e2868-165">As mentioned in the [Blob service concepts](#blob-service-concepts) section, Blob Storage offers three different types of blobs: block blobs, append blobs, and page blobs.</span></span> <span data-ttu-id="e2868-166">Biblioteka systemu iOS usługi Azure Storage obsługuje wszystkie trzy typy obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="e2868-166">The Azure Storage iOS library supports all three types of blobs.</span></span> <span data-ttu-id="e2868-167">W większości przypadków zalecane jest użycie blokowych obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="e2868-167">In most cases, block blob is the recommended type to use.</span></span>

<span data-ttu-id="e2868-168">Poniższy przykład pokazuje, jak przekazać obiekt blob blokowy z NSString.</span><span class="sxs-lookup"><span data-stu-id="e2868-168">The following example shows how to upload a block blob from an NSString.</span></span> <span data-ttu-id="e2868-169">Jeśli obiektu blob o takiej samej nazwie już istnieje w tym kontenerze, zawartość tego obiektu blob zostaną zastąpione.</span><span class="sxs-lookup"><span data-stu-id="e2868-169">If a blob with the same name already exists in this container, the contents of this blob will be overwritten.</span></span>

```objc
-(void)uploadBlobToContainer{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    [blobContainer createContainerIfNotExistsWithAccessType:AZSContainerPublicAccessTypeContainer requestOptions:nil operationContext:nil completionHandler:^(NSError *error, BOOL exists)
        {
            if (error){
                NSLog(@"Error in creating container.");
            }
            else{
                // Create a local blob object
                AZSCloudBlockBlob *blockBlob = [blobContainer blockBlobReferenceFromName:@"sampleblob"];

                // Upload blob to Storage
                [blockBlob uploadFromText:@"This text will be uploaded to Blob Storage." completionHandler:^(NSError *error) {
                    if (error){
                        NSLog(@"Error in creating blob.");
                    }
                }];
            }
        }];
}
```

<span data-ttu-id="e2868-170">Można potwierdzić, że to działa, analizując [Eksploratora usługi Microsoft Azure Storage](http://storageexplorer.com) i sprawdzić, czy kontener, *containerpublic*, zawiera obiekt blob, *sampleblob*.</span><span class="sxs-lookup"><span data-stu-id="e2868-170">You can confirm that this works by looking at the [Microsoft Azure Storage Explorer](http://storageexplorer.com) and verifying that the container, *containerpublic*, contains the blob, *sampleblob*.</span></span> <span data-ttu-id="e2868-171">W tym przykładzie użyliśmy publicznego kontenera, można również sprawdzić, czy tej aplikacji zadziałała, przechodząc do obiektów blob identyfikatora URI:</span><span class="sxs-lookup"><span data-stu-id="e2868-171">In this sample, we used a public container so you can also verify that this application worked by going to the blobs URI:</span></span>

    https://nameofyourstorageaccount.blob.core.windows.net/containerpublic/sampleblob

<span data-ttu-id="e2868-172">Oprócz przekazywania blokowych obiektów blob z NSString, istnieją podobne metody NSData, NSInputStream lub pliku lokalnego.</span><span class="sxs-lookup"><span data-stu-id="e2868-172">In addition to uploading a block blob from an NSString, similar methods exist for NSData, NSInputStream, or a local file.</span></span>

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="e2868-173">Wyświetlanie listy obiektów blob w kontenerze</span><span class="sxs-lookup"><span data-stu-id="e2868-173">List the blobs in a container</span></span>
<span data-ttu-id="e2868-174">Poniższy przykład przedstawia sposób wyświetlania wszystkich obiektów blob w kontenerze.</span><span class="sxs-lookup"><span data-stu-id="e2868-174">The following example shows how to list all blobs in a container.</span></span> <span data-ttu-id="e2868-175">Po wykonaniu tej operacji można mając na uwadze następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="e2868-175">When performing this operation, be mindful of the following parameters:</span></span>     

* <span data-ttu-id="e2868-176">**continuationToken** -reprezentuje token kontynuacji gdzie powinien rozpocząć operację wyświetlania listy.</span><span class="sxs-lookup"><span data-stu-id="e2868-176">**continuationToken** - The continuation token represents where the listing operation should start.</span></span> <span data-ttu-id="e2868-177">Jeśli token nie zostanie podany, będzie zawierała listę obiektów BLOB od początku.</span><span class="sxs-lookup"><span data-stu-id="e2868-177">If no token is provided, it will list blobs from the beginning.</span></span> <span data-ttu-id="e2868-178">Dowolną liczbę obiektów blob może być wymieniona od zera do maksymalnej zestaw.</span><span class="sxs-lookup"><span data-stu-id="e2868-178">Any number of blobs can be listed, from zero up to a set maximum.</span></span> <span data-ttu-id="e2868-179">Nawet jeśli ta metoda zwraca wyników, jeśli `results.continuationToken` nie jest tokenem nil, może być więcej obiektów blob w usłudze, które nie zostały wymienione.</span><span class="sxs-lookup"><span data-stu-id="e2868-179">Even if this method returns zero results, if `results.continuationToken` is not nil, there may be more blobs on the service that have not been listed.</span></span>
* <span data-ttu-id="e2868-180">**prefiks** — można określić prefiks do użycia na potrzeby listę obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="e2868-180">**prefix** - You can specify the prefix to use for blob listing.</span></span> <span data-ttu-id="e2868-181">Zostaną wyświetlone tylko te obiekty BLOB, zaczynające się z tym prefiksem.</span><span class="sxs-lookup"><span data-stu-id="e2868-181">Only blobs that begin with this prefix will be listed.</span></span>
* <span data-ttu-id="e2868-182">**useFlatBlobListing** — jak wspomniano w [nazewnictwa i odwołuje się do kontenerów i obiektów blob](#naming-and-referencing-containers-and-blobs) sekcji, chociaż usługa Blob jest schemat płaskiej magazynu można utworzyć wirtualnego hierarchii za pomocą nazw obiektów blob z informacje o ścieżce.</span><span class="sxs-lookup"><span data-stu-id="e2868-182">**useFlatBlobListing** - As mentioned in the [Naming and referencing containers and blobs](#naming-and-referencing-containers-and-blobs) section, although the Blob service is a flat storage scheme, you can create a virtual hierarchy by naming blobs with path information.</span></span> <span data-ttu-id="e2868-183">Jednak lista-flat nie jest obecnie obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="e2868-183">However, non-flat listing is currently not supported.</span></span> <span data-ttu-id="e2868-184">Ta funkcja będzie dostępna wkrótce.</span><span class="sxs-lookup"><span data-stu-id="e2868-184">This feature is coming soon.</span></span> <span data-ttu-id="e2868-185">Obecnie ta wartość powinna być **tak**.</span><span class="sxs-lookup"><span data-stu-id="e2868-185">For now, this value should be **YES**.</span></span>
* <span data-ttu-id="e2868-186">**blobListingDetails** — można określić elementów do uwzględnienia podczas wyświetlania obiektów blob</span><span class="sxs-lookup"><span data-stu-id="e2868-186">**blobListingDetails** - You can specify which items to include when listing blobs</span></span>
  * <span data-ttu-id="e2868-187">_AZSBlobListingDetailsNone_: wyświetlanie tylko zatwierdzone obiektów blob, a nie zwracać metadane obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="e2868-187">_AZSBlobListingDetailsNone_: List only committed blobs, and do not return blob metadata.</span></span>
  * <span data-ttu-id="e2868-188">_AZSBlobListingDetailsSnapshots_: wyświetlanie obiektów blob zatwierdzone i migawki obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="e2868-188">_AZSBlobListingDetailsSnapshots_: List committed blobs and blob snapshots.</span></span>
  * <span data-ttu-id="e2868-189">_AZSBlobListingDetailsMetadata_: zwrócony pobrać metadane obiektu blob dla każdego obiektu blob na liście.</span><span class="sxs-lookup"><span data-stu-id="e2868-189">_AZSBlobListingDetailsMetadata_: Retrieve blob metadata for each blob returned in the listing.</span></span>
  * <span data-ttu-id="e2868-190">_AZSBlobListingDetailsUncommittedBlobs_: wyświetlanie zatwierdzonej i niezatwierdzone obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="e2868-190">_AZSBlobListingDetailsUncommittedBlobs_: List committed and uncommitted blobs.</span></span>
  * <span data-ttu-id="e2868-191">_AZSBlobListingDetailsCopy_: obejmują kopiowania właściwości na liście.</span><span class="sxs-lookup"><span data-stu-id="e2868-191">_AZSBlobListingDetailsCopy_: Include copy properties in the listing.</span></span>
  * <span data-ttu-id="e2868-192">_AZSBlobListingDetailsAll_: wyświetlić listę wszystkich dostępnych obiektów blob zatwierdzone, niezatwierdzone obiekty BLOB i migawki, a następnie wróć wszystkich metadanych i kopia stanu dla tych obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="e2868-192">_AZSBlobListingDetailsAll_: List all available committed blobs, uncommitted blobs, and snapshots, and return all metadata and copy status for those blobs.</span></span>
* <span data-ttu-id="e2868-193">**maxResults** — maksymalna liczba wyników do zwrócenia do wykonania tej operacji.</span><span class="sxs-lookup"><span data-stu-id="e2868-193">**maxResults** - The maximum number of results to return for this operation.</span></span> <span data-ttu-id="e2868-194">Użyj wartości -1 nie ustawić limit.</span><span class="sxs-lookup"><span data-stu-id="e2868-194">Use -1 to not set a limit.</span></span>
* <span data-ttu-id="e2868-195">**completionHandler** — blok kodu do wykonania z wynikami operację wyświetlania listy.</span><span class="sxs-lookup"><span data-stu-id="e2868-195">**completionHandler** - The block of code to execute with the results of the listing operation.</span></span>

<span data-ttu-id="e2868-196">W tym przykładzie jest używane do metody pomocnika rekursywnie wywołanie listy obiektów blob — metoda, za każdym razem, gdy token kontynuacji jest zwracany.</span><span class="sxs-lookup"><span data-stu-id="e2868-196">In this example, a helper method is used to recursively call the list blobs method every time a continuation token is returned.</span></span>

```objc
-(void)listBlobsInContainer{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    //List all blobs in container
    [self listBlobsInContainerHelper:blobContainer continuationToken:nil prefix:nil blobListingDetails:AZSBlobListingDetailsAll maxResults:-1 completionHandler:^(NSError *error) {
        if (error != nil){
            NSLog(@"Error in creating container.");
        }
    }];
}

//List blobs helper method
-(void)listBlobsInContainerHelper:(AZSCloudBlobContainer *)container continuationToken:(AZSContinuationToken *)continuationToken prefix:(NSString *)prefix blobListingDetails:(AZSBlobListingDetails)blobListingDetails maxResults:(NSUInteger)maxResults completionHandler:(void (^)(NSError *))completionHandler
{
    [container listBlobsSegmentedWithContinuationToken:continuationToken prefix:prefix useFlatBlobListing:YES blobListingDetails:blobListingDetails maxResults:maxResults completionHandler:^(NSError *error, AZSBlobResultSegment *results) {
        if (error)
        {
            completionHandler(error);
        }
        else
        {
            for (int i = 0; i < results.blobs.count; i++) {
                NSLog(@"%@",[(AZSCloudBlockBlob *)results.blobs[i] blobName]);
            }
            if (results.continuationToken)
            {
                [self listBlobsInContainerHelper:container continuationToken:results.continuationToken prefix:prefix blobListingDetails:blobListingDetails maxResults:maxResults completionHandler:completionHandler];
            }
            else
            {
                completionHandler(nil);
            }
        }
    }];
}
```

## <a name="download-a-blob"></a><span data-ttu-id="e2868-197">Pobieranie obiektu blob</span><span class="sxs-lookup"><span data-stu-id="e2868-197">Download a blob</span></span>
<span data-ttu-id="e2868-198">Poniższy przykład przedstawia sposób pobierania obiektu blob do obiektu NSString.</span><span class="sxs-lookup"><span data-stu-id="e2868-198">The following example shows how to download a blob to a NSString object.</span></span>

```objc
-(void)downloadBlobToString{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    // Create a local blob object
    AZSCloudBlockBlob *blockBlob = [blobContainer blockBlobReferenceFromName:@"sampleblob"];

    // Download blob
    [blockBlob downloadToTextWithCompletionHandler:^(NSError *error, NSString *text) {
        if (error) {
            NSLog(@"Error in downloading blob");
        }
        else{
            NSLog(@"%@",text);
        }
    }];
}
```

## <a name="delete-a-blob"></a><span data-ttu-id="e2868-199">Usuwanie obiektu blob</span><span class="sxs-lookup"><span data-stu-id="e2868-199">Delete a blob</span></span>
<span data-ttu-id="e2868-200">Poniższy przykład pokazuje, jak można usunąć obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="e2868-200">The following example shows how to delete a blob.</span></span>

```objc
-(void)deleteBlob{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    // Create a local blob object
    AZSCloudBlockBlob *blockBlob = [blobContainer blockBlobReferenceFromName:@"sampleblob1"];

    // Delete blob
    [blockBlob deleteWithCompletionHandler:^(NSError *error) {
        if (error) {
            NSLog(@"Error in deleting blob.");
        }
    }];
}
```

## <a name="delete-a-blob-container"></a><span data-ttu-id="e2868-201">Usunięcie kontenera obiektów blob</span><span class="sxs-lookup"><span data-stu-id="e2868-201">Delete a blob container</span></span>
<span data-ttu-id="e2868-202">Poniższy przykład pokazuje, jak można usunąć kontenera.</span><span class="sxs-lookup"><span data-stu-id="e2868-202">The following example shows how to delete a container.</span></span>

```objc
-(void)deleteContainer{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    // Delete container
    [blobContainer deleteContainerIfExistsWithCompletionHandler:^(NSError *error, BOOL success) {
        if(error){
            NSLog(@"Error in deleting container");
        }
    }];
}
```

## <a name="next-steps"></a><span data-ttu-id="e2868-203">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e2868-203">Next steps</span></span>
<span data-ttu-id="e2868-204">Teraz, kiedy znasz, jak używać magazynu obiektów Blob z systemem iOS, skorzystaj z poniższych linków, aby dowiedzieć się więcej na temat biblioteki z systemem iOS i usługi magazynu.</span><span class="sxs-lookup"><span data-stu-id="e2868-204">Now that you've learned how to use Blob Storage from iOS, follow these links to learn more about the iOS library and the Storage service.</span></span>

* [<span data-ttu-id="e2868-205">Biblioteka klienta usługi Azure Storage dla systemu iOS</span><span class="sxs-lookup"><span data-stu-id="e2868-205">Azure Storage Client Library for iOS</span></span>](https://github.com/azure/azure-storage-ios)
* [<span data-ttu-id="e2868-206">IOS magazynu Azure dokumentacji</span><span class="sxs-lookup"><span data-stu-id="e2868-206">Azure Storage iOS Reference Documentation</span></span>](http://azure.github.io/azure-storage-ios/)
* [<span data-ttu-id="e2868-207">Interfejs API REST usług Azure Storage</span><span class="sxs-lookup"><span data-stu-id="e2868-207">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="e2868-208">Blog zespołu odpowiedzialnego za usługę Azure Storage</span><span class="sxs-lookup"><span data-stu-id="e2868-208">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage)

<span data-ttu-id="e2868-209">Jeśli masz pytania dotyczące tej biblioteki, możesz do wysłania do naszej [forum MSDN Azure](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=windowsazuredata) lub [przepełnienie stosu](http://stackoverflow.com/questions/tagged/windows-azure-storage+or+windows-azure-storage+or+azure-storage-blobs+or+azure-storage-tables+or+azure-table-storage+or+windows-azure-queues+or+azure-storage-queues+or+azure-storage-emulator+or+azure-storage-files).</span><span class="sxs-lookup"><span data-stu-id="e2868-209">If you have questions regarding this library, feel free to post to our [MSDN Azure forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=windowsazuredata) or [Stack Overflow](http://stackoverflow.com/questions/tagged/windows-azure-storage+or+windows-azure-storage+or+azure-storage-blobs+or+azure-storage-tables+or+azure-table-storage+or+windows-azure-queues+or+azure-storage-queues+or+azure-storage-emulator+or+azure-storage-files).</span></span>
<span data-ttu-id="e2868-210">Jeśli masz sugestie funkcji usługi Azure Storage, Opublikuj do [opinii magazynu Azure](https://feedback.azure.com/forums/217298-storage/).</span><span class="sxs-lookup"><span data-stu-id="e2868-210">If you have feature suggestions for Azure Storage, please post to [Azure Storage Feedback](https://feedback.azure.com/forums/217298-storage/).</span></span>

