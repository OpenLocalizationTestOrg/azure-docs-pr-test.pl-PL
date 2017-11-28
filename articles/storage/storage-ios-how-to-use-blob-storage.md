---
title: "toouse aaaHow magazynu obiektów Blob platformy Azure z systemem iOS | Dokumentacja firmy Microsoft"
description: "Przechowuj dane niestrukturalne w chmurze hello z magazynu obiektów Blob platformy Azure (obiekt magazynu)."
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
ms.openlocfilehash: 474c4263a4bfbd61bfa39e4fdb01ddd9c3829c77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-ios"></a><span data-ttu-id="5d65b-103">Jak toouse magazynu obiektów Blob z systemem iOS</span><span class="sxs-lookup"><span data-stu-id="5d65b-103">How toouse Blob storage from iOS</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="5d65b-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="5d65b-104">Overview</span></span>
<span data-ttu-id="5d65b-105">W tym artykule opisano, jak tooperform typowych scenariuszy przy użyciu magazynu obiektów Blob Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="5d65b-105">This article will show you how tooperform common scenarios using Microsoft Azure Blob storage.</span></span> <span data-ttu-id="5d65b-106">Witaj przykłady są napisane w języku Objective C i używają hello [biblioteki klienta magazynu Azure dla systemu iOS](https://github.com/Azure/azure-storage-ios).</span><span class="sxs-lookup"><span data-stu-id="5d65b-106">hello samples are written in Objective-C and use hello [Azure Storage Client Library for iOS](https://github.com/Azure/azure-storage-ios).</span></span> <span data-ttu-id="5d65b-107">Witaj omówione scenariusze obejmują **przekazywania**, **wyświetlania**, **pobieranie**, i **usuwanie** obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="5d65b-107">hello scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="5d65b-108">Aby uzyskać więcej informacji dotyczących obiektów blob, zobacz hello [następne kroki](#next-steps) sekcji.</span><span class="sxs-lookup"><span data-stu-id="5d65b-108">For more information on blobs, see hello [Next Steps](#next-steps) section.</span></span> <span data-ttu-id="5d65b-109">Możesz również pobrać hello [Przykładowa aplikacja](https://github.com/Azure/azure-storage-ios/tree/master/BlobSample) Zobacz tooquickly hello korzystanie z usługi Azure Storage w aplikacji systemu iOS.</span><span class="sxs-lookup"><span data-stu-id="5d65b-109">You can also download hello [sample app](https://github.com/Azure/azure-storage-ios/tree/master/BlobSample) tooquickly see hello use of Azure Storage in an iOS application.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="import-hello-azure-storage-ios-library-into-your-application"></a><span data-ttu-id="5d65b-110">Importowanie biblioteki dla systemu iOS usługi Azure Storage hello do aplikacji</span><span class="sxs-lookup"><span data-stu-id="5d65b-110">Import hello Azure Storage iOS library into your application</span></span>
<span data-ttu-id="5d65b-111">Możesz zaimportować hello Azure Storage iOS biblioteki do aplikacji przy użyciu hello [CocoaPod magazynu Azure](https://cocoapods.org/pods/AZSClient) lub importując hello **Framework** pliku.</span><span class="sxs-lookup"><span data-stu-id="5d65b-111">You can import hello Azure Storage iOS library into your application either by using hello [Azure Storage CocoaPod](https://cocoapods.org/pods/AZSClient) or by importing hello **Framework** file.</span></span> <span data-ttu-id="5d65b-112">CocoaPod jest hello zalecany sposób, zgodnie z jego ułatwia całkującej biblioteki hello, jednak importowania z pliku framework hello jest ta opcja jest mniej pożądana dla istniejącego projektu.</span><span class="sxs-lookup"><span data-stu-id="5d65b-112">CocoaPod is hello recommended way as it makes integrating hello library easier, however importing from hello framework file is less intrusive for your existing project.</span></span>

<span data-ttu-id="5d65b-113">toouse tej biblioteki, trzeba hello następujące:</span><span class="sxs-lookup"><span data-stu-id="5d65b-113">toouse this library, you need hello following:</span></span>
- <span data-ttu-id="5d65b-114">System iOS 8 i nowsze</span><span class="sxs-lookup"><span data-stu-id="5d65b-114">iOS 8+</span></span>
- <span data-ttu-id="5d65b-115">Xcode 7 +</span><span class="sxs-lookup"><span data-stu-id="5d65b-115">Xcode 7+</span></span>

## <a name="cocoapod"></a><span data-ttu-id="5d65b-116">CocoaPod</span><span class="sxs-lookup"><span data-stu-id="5d65b-116">CocoaPod</span></span>
1. <span data-ttu-id="5d65b-117">Jeśli użytkownik jeszcze tego nie zrobiono, [instalacji programu CocoaPods](https://guides.cocoapods.org/using/getting-started.html#toc_3) na komputerze, otwierając okno terminalu i uruchamiając następujące polecenie hello</span><span class="sxs-lookup"><span data-stu-id="5d65b-117">If you haven't done so already, [Install CocoaPods](https://guides.cocoapods.org/using/getting-started.html#toc_3) on your computer by opening a terminal window and running hello following command</span></span>
    
    ```shell   
    sudo gem install cocoapods
    ```

2. <span data-ttu-id="5d65b-118">Następnie w katalogu projektu hello (hello katalog zawierający plik .xcodeproj), Utwórz nowy plik o nazwie _Podfile_(bez rozszerzenia pliku).</span><span class="sxs-lookup"><span data-stu-id="5d65b-118">Next, in hello project directory (hello directory containing your .xcodeproj file), create a new file called _Podfile_(no file extension).</span></span> <span data-ttu-id="5d65b-119">Dodaj następujące too_Podfile_ hello i Zapisz.</span><span class="sxs-lookup"><span data-stu-id="5d65b-119">Add hello following too_Podfile_ and save.</span></span>

    ```ruby
    platform :ios, '8.0'

    target 'TargetName' do
      pod 'AZSClient'
    end
    ```

3. <span data-ttu-id="5d65b-120">Hello okno terminalu Przejdź toohello katalogu projektu i hello uruchom następujące polecenie</span><span class="sxs-lookup"><span data-stu-id="5d65b-120">In hello terminal window, navigate toohello project directory and run hello following command</span></span>

    ```shell    
    pod install
    ```

4. <span data-ttu-id="5d65b-121">Jeśli Twoje .xcodeproj jest otwarty w programie Xcode, należy go zamknąć.</span><span class="sxs-lookup"><span data-stu-id="5d65b-121">If your .xcodeproj is open in Xcode, close it.</span></span> <span data-ttu-id="5d65b-122">W pliku projektu hello Otwórz nowo utworzony katalog projektu będą mieć hello .xcworkspace rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="5d65b-122">In your project directory open hello newly created project file which will have hello .xcworkspace extension.</span></span> <span data-ttu-id="5d65b-123">Jest to plik hello, który będzie skorzystać z dla teraz.</span><span class="sxs-lookup"><span data-stu-id="5d65b-123">This is hello file you'll work from for now on.</span></span>

## <a name="framework"></a><span data-ttu-id="5d65b-124">Framework</span><span class="sxs-lookup"><span data-stu-id="5d65b-124">Framework</span></span>
<span data-ttu-id="5d65b-125">Witaj innych sposób biblioteki hello toouse toobuild hello framework ręcznie:</span><span class="sxs-lookup"><span data-stu-id="5d65b-125">hello other way toouse hello library is toobuild hello framework manually:</span></span>

1. <span data-ttu-id="5d65b-126">Pierwszy, pobierania lub hello w klonowania [repozytorium azure magazynu ios](https://github.com/azure/azure-storage-ios).</span><span class="sxs-lookup"><span data-stu-id="5d65b-126">First, download or clone hello [azure-storage-ios repo](https://github.com/azure/azure-storage-ios).</span></span>
2. <span data-ttu-id="5d65b-127">Przejdź do *systemu ios magazynu azure* -> *Lib* -> *biblioteki klienta magazynu Azure*, a następnie otwórz `AZSClient.xcodeproj` w środowisku Xcode.</span><span class="sxs-lookup"><span data-stu-id="5d65b-127">Go into *azure-storage-ios* -> *Lib* -> *Azure Storage Client Library*, and open `AZSClient.xcodeproj` in Xcode.</span></span>
3. <span data-ttu-id="5d65b-128">Na powitania lewego górnego narzędzia xcode, zmień hello active schemat z "Biblioteki klienta magazynu Azure" za "Framework".</span><span class="sxs-lookup"><span data-stu-id="5d65b-128">At hello top-left of Xcode, change hello active scheme from "Azure Storage Client Library" too"Framework".</span></span>
4. <span data-ttu-id="5d65b-129">Tworzenie projektu hello (⌘ + B).</span><span class="sxs-lookup"><span data-stu-id="5d65b-129">Build hello project (⌘+B).</span></span> <span data-ttu-id="5d65b-130">Spowoduje to utworzenie `AZSClient.framework` plik na pulpicie.</span><span class="sxs-lookup"><span data-stu-id="5d65b-130">This will create an `AZSClient.framework` file on your Desktop.</span></span>

<span data-ttu-id="5d65b-131">Następnie można zaimportować plik framework hello w aplikacji, wykonując następujące hello:</span><span class="sxs-lookup"><span data-stu-id="5d65b-131">You can then import hello framework file into your application by doing hello following:</span></span>

1. <span data-ttu-id="5d65b-132">Tworzenie nowego projektu lub otworzenie istniejącego projektu w środowisku Xcode.</span><span class="sxs-lookup"><span data-stu-id="5d65b-132">Create a new project or open up your existing project in Xcode.</span></span>
2. <span data-ttu-id="5d65b-133">Przeciąganie i upuszczanie hello `AZSClient.framework` do Nawigatora projektu Xcode.</span><span class="sxs-lookup"><span data-stu-id="5d65b-133">Drag and drop hello `AZSClient.framework` into your Xcode project navigator.</span></span>
3. <span data-ttu-id="5d65b-134">Wybierz *skopiować elementy w razie potrzeby*i kliknij przycisk *Zakończ*.</span><span class="sxs-lookup"><span data-stu-id="5d65b-134">Select *Copy items if needed*, and click on *Finish*.</span></span>
4. <span data-ttu-id="5d65b-135">Kliknij projekt w hello nawigacji po lewej stronie, a następnie kliknij przycisk hello *ogólne* u góry hello hello projektu edytora.</span><span class="sxs-lookup"><span data-stu-id="5d65b-135">Click on your project in hello left-hand navigation and click hello *General* tab at hello top of hello project editor.</span></span>
5. <span data-ttu-id="5d65b-136">W obszarze hello *połączone struktury i biblioteki* sekcji, kliknij przycisk Dodaj hello (+).</span><span class="sxs-lookup"><span data-stu-id="5d65b-136">Under hello *Linked Frameworks and Libraries* section, click hello Add button (+).</span></span>
6. <span data-ttu-id="5d65b-137">Na liście hello biblioteki są dostępne, wyszukaj `libxml2.2.tbd` i dodaj go tooyour projektu.</span><span class="sxs-lookup"><span data-stu-id="5d65b-137">In hello list of libraries already provided, search for `libxml2.2.tbd` and add it tooyour project.</span></span>

## <a name="import-hello-library"></a><span data-ttu-id="5d65b-138">Witaj Importuj biblioteki</span><span class="sxs-lookup"><span data-stu-id="5d65b-138">Import hello Library</span></span> 
```objc
// Include hello following import statement toouse blob APIs.
#import <AZSClient/AZSClient.h>
```

<span data-ttu-id="5d65b-139">Jeśli używasz Swift, należy toocreate nagłówek mostkowania, a importowanie < AZSClient/AZSClient.h >:</span><span class="sxs-lookup"><span data-stu-id="5d65b-139">If you are using Swift, you will need toocreate a bridging header and import <AZSClient/AZSClient.h> there:</span></span>

1. <span data-ttu-id="5d65b-140">Utwórz plik nagłówka `Bridging-Header.h`i Dodaj hello powyżej instrukcję import.</span><span class="sxs-lookup"><span data-stu-id="5d65b-140">Create a header file `Bridging-Header.h`, and add hello above import statement.</span></span>
2. <span data-ttu-id="5d65b-141">Przejdź toohello *ustawieniach kompilacji* , a następnie wyszukaj *nagłówków mostkowania języka Objective-C*.</span><span class="sxs-lookup"><span data-stu-id="5d65b-141">Go toohello *Build Settings* tab, and search for *Objective-C Bridging Header*.</span></span>
3. <span data-ttu-id="5d65b-142">Kliknij dwukrotnie pole hello *nagłówków mostkowania języka Objective-C* i Dodaj hello ścieżki tooyour nagłówka pliku:`ProjectName/Bridging-Header.h`</span><span class="sxs-lookup"><span data-stu-id="5d65b-142">Double-click on hello field of *Objective-C Bridging Header* and add hello path tooyour header file: `ProjectName/Bridging-Header.h`</span></span>
4. <span data-ttu-id="5d65b-143">Tooverify kompilacji projektu (⌘ + B) hello, który hello nagłówka mostkowania została pobrana przez Xcode.</span><span class="sxs-lookup"><span data-stu-id="5d65b-143">Build hello project (⌘+B) tooverify that hello bridging header was picked up by Xcode.</span></span>
5. <span data-ttu-id="5d65b-144">Rozpoczynanie korzystania z biblioteki hello bezpośrednio w żadnym pliku Swift, nie istnieje potrzeba dla instrukcje importu.</span><span class="sxs-lookup"><span data-stu-id="5d65b-144">Start using hello library directly in any Swift file, there is no need for import statements.</span></span>

[!INCLUDE [storage-mobile-authentication-guidance](../../includes/storage-mobile-authentication-guidance.md)]

## <a name="asynchronous-operations"></a><span data-ttu-id="5d65b-145">Operacje asynchroniczne</span><span class="sxs-lookup"><span data-stu-id="5d65b-145">Asynchronous Operations</span></span>
> [!NOTE]
> <span data-ttu-id="5d65b-146">Wszystkie metody, które wykonania żądania usługi hello są operacji asynchronicznych.</span><span class="sxs-lookup"><span data-stu-id="5d65b-146">All methods that perform a request against hello service are asynchronous operations.</span></span> <span data-ttu-id="5d65b-147">W przykładach kodu hello znajdziesz, czy te metody ma obsługi zakończenia.</span><span class="sxs-lookup"><span data-stu-id="5d65b-147">In hello code samples, you'll find that these methods have a completion handler.</span></span> <span data-ttu-id="5d65b-148">Uruchomi kodu wewnątrz obsługi uzupełniania hello **po** hello żądania zostało zakończone.</span><span class="sxs-lookup"><span data-stu-id="5d65b-148">Code inside hello completion handler will run **after** hello request is completed.</span></span> <span data-ttu-id="5d65b-149">Kod po hello zakończenia obsługi zostanie uruchomiony **podczas** hello jest żądań.</span><span class="sxs-lookup"><span data-stu-id="5d65b-149">Code after hello completion handler will run **while** hello request is being made.</span></span>
> 
> 

## <a name="create-a-container"></a><span data-ttu-id="5d65b-150">Tworzenie kontenera</span><span class="sxs-lookup"><span data-stu-id="5d65b-150">Create a container</span></span>
<span data-ttu-id="5d65b-151">Każdy obiekt blob w magazynie Azure musi znajdować się w kontenerze.</span><span class="sxs-lookup"><span data-stu-id="5d65b-151">Every blob in Azure Storage must reside in a container.</span></span> <span data-ttu-id="5d65b-152">Witaj poniższy przykład przedstawia sposób toocreate kontener o nazwie *newcontainer*, na Twoim koncie magazynu, jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="5d65b-152">hello following example shows how toocreate a container, called *newcontainer*, in your Storage account if it doesn't already exist.</span></span> <span data-ttu-id="5d65b-153">W przypadku wybrania nazwy użytkownika kontenera, można w trosce o hello nazewnictwa zasad wymienione powyżej.</span><span class="sxs-lookup"><span data-stu-id="5d65b-153">When choosing a name for your container, be mindful of hello naming rules mentioned above.</span></span>

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

    // Create container in your Storage account if hello container doesn't already exist
    [blobContainer createContainerIfNotExistsWithCompletionHandler:^(NSError *error, BOOL exists) {
        if (error){
            NSLog(@"Error in creating container.");
        }
    }];
}
```

<span data-ttu-id="5d65b-154">Można potwierdzić, że to działa, analizując hello [Eksploratora usługi Microsoft Azure Storage](http://storageexplorer.com) i sprawdzić, czy *newcontainer* się na liście hello kontenerów dla konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="5d65b-154">You can confirm that this works by looking at hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) and verifying that *newcontainer* is in hello list of containers for your Storage account.</span></span>

## <a name="set-container-permissions"></a><span data-ttu-id="5d65b-155">Ustaw uprawnienia do kontenera</span><span class="sxs-lookup"><span data-stu-id="5d65b-155">Set Container Permissions</span></span>
<span data-ttu-id="5d65b-156">Kontener uprawnienia są skonfigurowane dla **prywatnej** dostępu domyślnie.</span><span class="sxs-lookup"><span data-stu-id="5d65b-156">A container's permissions are configured for **Private** access by default.</span></span> <span data-ttu-id="5d65b-157">Kontenery zapewnia jednak kilka różnych opcji dla dostępu do kontenera:</span><span class="sxs-lookup"><span data-stu-id="5d65b-157">However, containers provide a few different options for container access:</span></span>

* <span data-ttu-id="5d65b-158">**Prywatne**: obiektów blob i kontenera danych może zostać odczytany przez hello tylko właściciel konta.</span><span class="sxs-lookup"><span data-stu-id="5d65b-158">**Private**: Container and blob data can be read by hello account owner only.</span></span>
* <span data-ttu-id="5d65b-159">**Obiekt blob**: dane obiektów Blob w tym kontenerze mogą być odczytywane za pomocą żądania od użytkowników anonimowych, ale nie są dostępne dane kontenera.</span><span class="sxs-lookup"><span data-stu-id="5d65b-159">**Blob**: Blob data within this container can be read via anonymous request, but container data is not available.</span></span> <span data-ttu-id="5d65b-160">Klienci nie można wyliczyć obiektów blob w kontenerze hello za pomocą żądania od użytkowników anonimowych.</span><span class="sxs-lookup"><span data-stu-id="5d65b-160">Clients cannot enumerate blobs within hello container via anonymous request.</span></span>
* <span data-ttu-id="5d65b-161">**Kontener**: obiektów blob i kontenera danych mogą być odczytywane za pomocą żądania od użytkowników anonimowych.</span><span class="sxs-lookup"><span data-stu-id="5d65b-161">**Container**: Container and blob data can be read via anonymous request.</span></span> <span data-ttu-id="5d65b-162">Klientów można wyliczyć obiektów blob w kontenerze hello za pomocą żądania od użytkowników anonimowych, ale nie można wyliczyć kontenery w ramach konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="5d65b-162">Clients can enumerate blobs within hello container via anonymous request, but cannot enumerate containers within hello storage account.</span></span>

<span data-ttu-id="5d65b-163">Witaj poniższym przykładzie pokazano, jak toocreate a kontener z **kontenera** uprawnienia, które zezwoli na dostęp publiczny, tylko do odczytu dla wszystkich użytkowników na powitania Internet dostępu:</span><span class="sxs-lookup"><span data-stu-id="5d65b-163">hello following example shows you how toocreate a container with **Container** access permissions, which will allow public, read-only access for all users on hello Internet:</span></span>

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

    // Create container in your Storage account if hello container doesn't already exist
    [blobContainer createContainerIfNotExistsWithAccessType:AZSContainerPublicAccessTypeContainer requestOptions:nil operationContext:nil completionHandler:^(NSError *error, BOOL exists){
        if (error){
            NSLog(@"Error in creating container.");
        }
    }];
}
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="5d65b-164">Przekazywanie obiektu blob do kontenera</span><span class="sxs-lookup"><span data-stu-id="5d65b-164">Upload a blob into a container</span></span>
<span data-ttu-id="5d65b-165">Jak wspomniano w hello [pojęcia dotyczące usługi Blob](#blob-service-concepts) sekcji magazynu obiektów Blob udostępnia trzy typy obiektów blob: blokowe obiekty BLOB, uzupełnialnych obiektów blob i stronicowe.</span><span class="sxs-lookup"><span data-stu-id="5d65b-165">As mentioned in hello [Blob service concepts](#blob-service-concepts) section, Blob Storage offers three different types of blobs: block blobs, append blobs, and page blobs.</span></span> <span data-ttu-id="5d65b-166">Biblioteka systemu iOS usługi Azure Storage Hello obsługuje wszystkie trzy typy obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="5d65b-166">hello Azure Storage iOS library supports all three types of blobs.</span></span> <span data-ttu-id="5d65b-167">W większości przypadków blokowych obiektów blob jest hello zalecane toouse typu.</span><span class="sxs-lookup"><span data-stu-id="5d65b-167">In most cases, block blob is hello recommended type toouse.</span></span>

<span data-ttu-id="5d65b-168">Witaj poniższy przykład pokazuje, jak tooupload blokowych obiektów blob z NSString.</span><span class="sxs-lookup"><span data-stu-id="5d65b-168">hello following example shows how tooupload a block blob from an NSString.</span></span> <span data-ttu-id="5d65b-169">Jeśli obiekt blob o takiej nazwie już istnieje w tym kontenerze powitalne hello zawartość tego obiektu blob zostaną zastąpione.</span><span class="sxs-lookup"><span data-stu-id="5d65b-169">If a blob with hello same name already exists in this container, hello contents of this blob will be overwritten.</span></span>

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

                // Upload blob tooStorage
                [blockBlob uploadFromText:@"This text will be uploaded tooBlob Storage." completionHandler:^(NSError *error) {
                    if (error){
                        NSLog(@"Error in creating blob.");
                    }
                }];
            }
        }];
}
```

<span data-ttu-id="5d65b-170">Można potwierdzić, że to działa, analizując hello [Eksploratora usługi Microsoft Azure Storage](http://storageexplorer.com) i weryfikowania tego kontenera hello *containerpublic*, zawiera hello blob *sampleblob*.</span><span class="sxs-lookup"><span data-stu-id="5d65b-170">You can confirm that this works by looking at hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) and verifying that hello container, *containerpublic*, contains hello blob, *sampleblob*.</span></span> <span data-ttu-id="5d65b-171">W tym przykładzie użyliśmy publicznego kontenera, można również sprawdzić, czy ta aplikacja pracy będzie toohello obiekty BLOB identyfikatora URI:</span><span class="sxs-lookup"><span data-stu-id="5d65b-171">In this sample, we used a public container so you can also verify that this application worked by going toohello blobs URI:</span></span>

    https://nameofyourstorageaccount.blob.core.windows.net/containerpublic/sampleblob

<span data-ttu-id="5d65b-172">Ponadto toouploading blokowych obiektów blob z NSString podobnych metod istnieje NSData, NSInputStream lub pliku lokalnego.</span><span class="sxs-lookup"><span data-stu-id="5d65b-172">In addition toouploading a block blob from an NSString, similar methods exist for NSData, NSInputStream, or a local file.</span></span>

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="5d65b-173">Lista hello BLOB w kontenerze</span><span class="sxs-lookup"><span data-stu-id="5d65b-173">List hello blobs in a container</span></span>
<span data-ttu-id="5d65b-174">Witaj poniższy przykład przedstawia sposób toolist wszystkie obiekty BLOB w kontenerze.</span><span class="sxs-lookup"><span data-stu-id="5d65b-174">hello following example shows how toolist all blobs in a container.</span></span> <span data-ttu-id="5d65b-175">Po wykonaniu tej operacji można mając na uwadze hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="5d65b-175">When performing this operation, be mindful of hello following parameters:</span></span>     

* <span data-ttu-id="5d65b-176">**continuationToken** — Witaj reprezentuje token kontynuacji, gdzie powinna zaczynać się hello listę operacji.</span><span class="sxs-lookup"><span data-stu-id="5d65b-176">**continuationToken** - hello continuation token represents where hello listing operation should start.</span></span> <span data-ttu-id="5d65b-177">Jeśli token nie zostanie podany, będzie zawierała listę obiektów BLOB od początku hello.</span><span class="sxs-lookup"><span data-stu-id="5d65b-177">If no token is provided, it will list blobs from hello beginning.</span></span> <span data-ttu-id="5d65b-178">Dowolną liczbę obiektów blob może być wymieniona od zera się tooa wartość maksymalna.</span><span class="sxs-lookup"><span data-stu-id="5d65b-178">Any number of blobs can be listed, from zero up tooa set maximum.</span></span> <span data-ttu-id="5d65b-179">Nawet jeśli ta metoda zwraca wyników, jeśli `results.continuationToken` nie jest tokenem nil, może być więcej obiektów blob na powitania usługi, które nie zostały wymienione.</span><span class="sxs-lookup"><span data-stu-id="5d65b-179">Even if this method returns zero results, if `results.continuationToken` is not nil, there may be more blobs on hello service that have not been listed.</span></span>
* <span data-ttu-id="5d65b-180">**prefiks** — można określić hello prefiks toouse listę obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="5d65b-180">**prefix** - You can specify hello prefix toouse for blob listing.</span></span> <span data-ttu-id="5d65b-181">Zostaną wyświetlone tylko te obiekty BLOB, zaczynające się z tym prefiksem.</span><span class="sxs-lookup"><span data-stu-id="5d65b-181">Only blobs that begin with this prefix will be listed.</span></span>
* <span data-ttu-id="5d65b-182">**useFlatBlobListing** — jak wspomniano w hello [nazewnictwa i odwołuje się do kontenerów i obiektów blob](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata) sekcji hello usługi obiektów Blob jest schemat płaskiej magazynu można utworzyć wirtualnego hierarchii za pomocą nazw obiektów blob ze ścieżką informacje.</span><span class="sxs-lookup"><span data-stu-id="5d65b-182">**useFlatBlobListing** - As mentioned in hello [Naming and referencing containers and blobs](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata) section, although hello Blob service is a flat storage scheme, you can create a virtual hierarchy by naming blobs with path information.</span></span> <span data-ttu-id="5d65b-183">Jednak lista-flat nie jest obecnie obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="5d65b-183">However, non-flat listing is currently not supported.</span></span> <span data-ttu-id="5d65b-184">Ta funkcja będzie dostępna wkrótce.</span><span class="sxs-lookup"><span data-stu-id="5d65b-184">This feature is coming soon.</span></span> <span data-ttu-id="5d65b-185">Obecnie ta wartość powinna być **tak**.</span><span class="sxs-lookup"><span data-stu-id="5d65b-185">For now, this value should be **YES**.</span></span>

* <span data-ttu-id="5d65b-186">**blobListingDetails** -tooinclude elementów, które można określić podczas wyświetlania obiektów blob</span><span class="sxs-lookup"><span data-stu-id="5d65b-186">**blobListingDetails** - You can specify which items tooinclude when listing blobs</span></span>
  * <span data-ttu-id="5d65b-187">_AZSBlobListingDetailsNone_: wyświetlanie tylko zatwierdzone obiektów blob, a nie zwracać metadane obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="5d65b-187">_AZSBlobListingDetailsNone_: List only committed blobs, and do not return blob metadata.</span></span>
  * <span data-ttu-id="5d65b-188">_AZSBlobListingDetailsSnapshots_: wyświetlanie obiektów blob zatwierdzone i migawki obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="5d65b-188">_AZSBlobListingDetailsSnapshots_: List committed blobs and blob snapshots.</span></span>
  * <span data-ttu-id="5d65b-189">_AZSBlobListingDetailsMetadata_: pobieranie metadane obiektu blob dla każdego obiektu blob zwrócił liście hello.</span><span class="sxs-lookup"><span data-stu-id="5d65b-189">_AZSBlobListingDetailsMetadata_: Retrieve blob metadata for each blob returned in hello listing.</span></span>
  * <span data-ttu-id="5d65b-190">_AZSBlobListingDetailsUncommittedBlobs_: wyświetlanie zatwierdzonej i niezatwierdzone obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="5d65b-190">_AZSBlobListingDetailsUncommittedBlobs_: List committed and uncommitted blobs.</span></span>
  * <span data-ttu-id="5d65b-191">_AZSBlobListingDetailsCopy_: obejmują kopiowania właściwości liście hello.</span><span class="sxs-lookup"><span data-stu-id="5d65b-191">_AZSBlobListingDetailsCopy_: Include copy properties in hello listing.</span></span>
  * <span data-ttu-id="5d65b-192">_AZSBlobListingDetailsAll_: wyświetlić listę wszystkich dostępnych obiektów blob zatwierdzone, niezatwierdzone obiekty BLOB i migawki, a następnie wróć wszystkich metadanych i kopia stanu dla tych obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="5d65b-192">_AZSBlobListingDetailsAll_: List all available committed blobs, uncommitted blobs, and snapshots, and return all metadata and copy status for those blobs.</span></span>
* <span data-ttu-id="5d65b-193">**maxResults** — Witaj maksymalną liczbę wyników tooreturn dla tej operacji.</span><span class="sxs-lookup"><span data-stu-id="5d65b-193">**maxResults** - hello maximum number of results tooreturn for this operation.</span></span> <span data-ttu-id="5d65b-194">Użyj wartości -1 toonot ustawienie limitu.</span><span class="sxs-lookup"><span data-stu-id="5d65b-194">Use -1 toonot set a limit.</span></span>
* <span data-ttu-id="5d65b-195">**completionHandler** -hello blok kodu tooexecute z wynikiem hello hello listę operacji.</span><span class="sxs-lookup"><span data-stu-id="5d65b-195">**completionHandler** - hello block of code tooexecute with hello results of hello listing operation.</span></span>

<span data-ttu-id="5d65b-196">W tym przykładzie metoda pomocnika jest toorecursively używane wywołania hello listy obiektów blob metoda, za każdym razem, gdy token kontynuacji jest zwracany.</span><span class="sxs-lookup"><span data-stu-id="5d65b-196">In this example, a helper method is used toorecursively call hello list blobs method every time a continuation token is returned.</span></span>

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

## <a name="download-a-blob"></a><span data-ttu-id="5d65b-197">Pobieranie obiektu blob</span><span class="sxs-lookup"><span data-stu-id="5d65b-197">Download a blob</span></span>
<span data-ttu-id="5d65b-198">powitania po przykładzie pokazano, jak toodownload obiektu blob tooa NSString.</span><span class="sxs-lookup"><span data-stu-id="5d65b-198">hello following example shows how toodownload a blob tooa NSString object.</span></span>

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

## <a name="delete-a-blob"></a><span data-ttu-id="5d65b-199">Usuwanie obiektu blob</span><span class="sxs-lookup"><span data-stu-id="5d65b-199">Delete a blob</span></span>
<span data-ttu-id="5d65b-200">powitania po przykładzie pokazano, jak toodelete obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="5d65b-200">hello following example shows how toodelete a blob.</span></span>

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

## <a name="delete-a-blob-container"></a><span data-ttu-id="5d65b-201">Usunięcie kontenera obiektów blob</span><span class="sxs-lookup"><span data-stu-id="5d65b-201">Delete a blob container</span></span>
<span data-ttu-id="5d65b-202">powitania po przykładzie pokazano, jak toodelete kontenera.</span><span class="sxs-lookup"><span data-stu-id="5d65b-202">hello following example shows how toodelete a container.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="5d65b-203">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5d65b-203">Next steps</span></span>
<span data-ttu-id="5d65b-204">Teraz, kiedy znasz już jak toouse magazynu obiektów Blob z systemem iOS, wykonaj te toolearn łącza więcej informacji na temat biblioteki z systemem iOS hello i hello usługi magazynu.</span><span class="sxs-lookup"><span data-stu-id="5d65b-204">Now that you've learned how toouse Blob Storage from iOS, follow these links toolearn more about hello iOS library and hello Storage service.</span></span>

* [<span data-ttu-id="5d65b-205">Biblioteka klienta usługi Azure Storage dla systemu iOS</span><span class="sxs-lookup"><span data-stu-id="5d65b-205">Azure Storage Client Library for iOS</span></span>](https://github.com/azure/azure-storage-ios)
* [<span data-ttu-id="5d65b-206">IOS magazynu Azure dokumentacji</span><span class="sxs-lookup"><span data-stu-id="5d65b-206">Azure Storage iOS Reference Documentation</span></span>](http://azure.github.io/azure-storage-ios/)
* [<span data-ttu-id="5d65b-207">Interfejs API REST usług Azure Storage</span><span class="sxs-lookup"><span data-stu-id="5d65b-207">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="5d65b-208">Blog zespołu odpowiedzialnego za usługę Azure Storage</span><span class="sxs-lookup"><span data-stu-id="5d65b-208">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage)

<span data-ttu-id="5d65b-209">Jeśli masz pytania dotyczące tej biblioteki, możesz tooour wolnego toopost [forum MSDN Azure](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=windowsazuredata) lub [przepełnienie stosu](http://stackoverflow.com/questions/tagged/windows-azure-storage+or+windows-azure-storage+or+azure-storage-blobs+or+azure-storage-tables+or+azure-table-storage+or+windows-azure-queues+or+azure-storage-queues+or+azure-storage-emulator+or+azure-storage-files).</span><span class="sxs-lookup"><span data-stu-id="5d65b-209">If you have questions regarding this library, feel free toopost tooour [MSDN Azure forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=windowsazuredata) or [Stack Overflow](http://stackoverflow.com/questions/tagged/windows-azure-storage+or+windows-azure-storage+or+azure-storage-blobs+or+azure-storage-tables+or+azure-table-storage+or+windows-azure-queues+or+azure-storage-queues+or+azure-storage-emulator+or+azure-storage-files).</span></span>
<span data-ttu-id="5d65b-210">Jeśli masz sugestie funkcji usługi Azure Storage, Opublikuj zbyt[opinii magazynu Azure](https://feedback.azure.com/forums/217298-storage/).</span><span class="sxs-lookup"><span data-stu-id="5d65b-210">If you have feature suggestions for Azure Storage, please post too[Azure Storage Feedback](https://feedback.azure.com/forums/217298-storage/).</span></span>

