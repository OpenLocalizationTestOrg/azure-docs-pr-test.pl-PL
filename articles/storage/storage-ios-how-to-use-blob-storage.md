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
# <a name="how-toouse-blob-storage-from-ios"></a>Jak toouse magazynu obiektów Blob z systemem iOS
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Omówienie
W tym artykule opisano, jak tooperform typowych scenariuszy przy użyciu magazynu obiektów Blob Microsoft Azure. Witaj przykłady są napisane w języku Objective C i używają hello [biblioteki klienta magazynu Azure dla systemu iOS](https://github.com/Azure/azure-storage-ios). Witaj omówione scenariusze obejmują **przekazywania**, **wyświetlania**, **pobieranie**, i **usuwanie** obiektów blob. Aby uzyskać więcej informacji dotyczących obiektów blob, zobacz hello [następne kroki](#next-steps) sekcji. Możesz również pobrać hello [Przykładowa aplikacja](https://github.com/Azure/azure-storage-ios/tree/master/BlobSample) Zobacz tooquickly hello korzystanie z usługi Azure Storage w aplikacji systemu iOS.

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="import-hello-azure-storage-ios-library-into-your-application"></a>Importowanie biblioteki dla systemu iOS usługi Azure Storage hello do aplikacji
Możesz zaimportować hello Azure Storage iOS biblioteki do aplikacji przy użyciu hello [CocoaPod magazynu Azure](https://cocoapods.org/pods/AZSClient) lub importując hello **Framework** pliku. CocoaPod jest hello zalecany sposób, zgodnie z jego ułatwia całkującej biblioteki hello, jednak importowania z pliku framework hello jest ta opcja jest mniej pożądana dla istniejącego projektu.

toouse tej biblioteki, trzeba hello następujące:
- System iOS 8 i nowsze
- Xcode 7 +

## <a name="cocoapod"></a>CocoaPod
1. Jeśli użytkownik jeszcze tego nie zrobiono, [instalacji programu CocoaPods](https://guides.cocoapods.org/using/getting-started.html#toc_3) na komputerze, otwierając okno terminalu i uruchamiając następujące polecenie hello
    
    ```shell   
    sudo gem install cocoapods
    ```

2. Następnie w katalogu projektu hello (hello katalog zawierający plik .xcodeproj), Utwórz nowy plik o nazwie _Podfile_(bez rozszerzenia pliku). Dodaj następujące too_Podfile_ hello i Zapisz.

    ```ruby
    platform :ios, '8.0'

    target 'TargetName' do
      pod 'AZSClient'
    end
    ```

3. Hello okno terminalu Przejdź toohello katalogu projektu i hello uruchom następujące polecenie

    ```shell    
    pod install
    ```

4. Jeśli Twoje .xcodeproj jest otwarty w programie Xcode, należy go zamknąć. W pliku projektu hello Otwórz nowo utworzony katalog projektu będą mieć hello .xcworkspace rozszerzenia. Jest to plik hello, który będzie skorzystać z dla teraz.

## <a name="framework"></a>Framework
Witaj innych sposób biblioteki hello toouse toobuild hello framework ręcznie:

1. Pierwszy, pobierania lub hello w klonowania [repozytorium azure magazynu ios](https://github.com/azure/azure-storage-ios).
2. Przejdź do *systemu ios magazynu azure* -> *Lib* -> *biblioteki klienta magazynu Azure*, a następnie otwórz `AZSClient.xcodeproj` w środowisku Xcode.
3. Na powitania lewego górnego narzędzia xcode, zmień hello active schemat z "Biblioteki klienta magazynu Azure" za "Framework".
4. Tworzenie projektu hello (⌘ + B). Spowoduje to utworzenie `AZSClient.framework` plik na pulpicie.

Następnie można zaimportować plik framework hello w aplikacji, wykonując następujące hello:

1. Tworzenie nowego projektu lub otworzenie istniejącego projektu w środowisku Xcode.
2. Przeciąganie i upuszczanie hello `AZSClient.framework` do Nawigatora projektu Xcode.
3. Wybierz *skopiować elementy w razie potrzeby*i kliknij przycisk *Zakończ*.
4. Kliknij projekt w hello nawigacji po lewej stronie, a następnie kliknij przycisk hello *ogólne* u góry hello hello projektu edytora.
5. W obszarze hello *połączone struktury i biblioteki* sekcji, kliknij przycisk Dodaj hello (+).
6. Na liście hello biblioteki są dostępne, wyszukaj `libxml2.2.tbd` i dodaj go tooyour projektu.

## <a name="import-hello-library"></a>Witaj Importuj biblioteki 
```objc
// Include hello following import statement toouse blob APIs.
#import <AZSClient/AZSClient.h>
```

Jeśli używasz Swift, należy toocreate nagłówek mostkowania, a importowanie < AZSClient/AZSClient.h >:

1. Utwórz plik nagłówka `Bridging-Header.h`i Dodaj hello powyżej instrukcję import.
2. Przejdź toohello *ustawieniach kompilacji* , a następnie wyszukaj *nagłówków mostkowania języka Objective-C*.
3. Kliknij dwukrotnie pole hello *nagłówków mostkowania języka Objective-C* i Dodaj hello ścieżki tooyour nagłówka pliku:`ProjectName/Bridging-Header.h`
4. Tooverify kompilacji projektu (⌘ + B) hello, który hello nagłówka mostkowania została pobrana przez Xcode.
5. Rozpoczynanie korzystania z biblioteki hello bezpośrednio w żadnym pliku Swift, nie istnieje potrzeba dla instrukcje importu.

[!INCLUDE [storage-mobile-authentication-guidance](../../includes/storage-mobile-authentication-guidance.md)]

## <a name="asynchronous-operations"></a>Operacje asynchroniczne
> [!NOTE]
> Wszystkie metody, które wykonania żądania usługi hello są operacji asynchronicznych. W przykładach kodu hello znajdziesz, czy te metody ma obsługi zakończenia. Uruchomi kodu wewnątrz obsługi uzupełniania hello **po** hello żądania zostało zakończone. Kod po hello zakończenia obsługi zostanie uruchomiony **podczas** hello jest żądań.
> 
> 

## <a name="create-a-container"></a>Tworzenie kontenera
Każdy obiekt blob w magazynie Azure musi znajdować się w kontenerze. Witaj poniższy przykład przedstawia sposób toocreate kontener o nazwie *newcontainer*, na Twoim koncie magazynu, jeśli jeszcze nie istnieje. W przypadku wybrania nazwy użytkownika kontenera, można w trosce o hello nazewnictwa zasad wymienione powyżej.

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

Można potwierdzić, że to działa, analizując hello [Eksploratora usługi Microsoft Azure Storage](http://storageexplorer.com) i sprawdzić, czy *newcontainer* się na liście hello kontenerów dla konta magazynu.

## <a name="set-container-permissions"></a>Ustaw uprawnienia do kontenera
Kontener uprawnienia są skonfigurowane dla **prywatnej** dostępu domyślnie. Kontenery zapewnia jednak kilka różnych opcji dla dostępu do kontenera:

* **Prywatne**: obiektów blob i kontenera danych może zostać odczytany przez hello tylko właściciel konta.
* **Obiekt blob**: dane obiektów Blob w tym kontenerze mogą być odczytywane za pomocą żądania od użytkowników anonimowych, ale nie są dostępne dane kontenera. Klienci nie można wyliczyć obiektów blob w kontenerze hello za pomocą żądania od użytkowników anonimowych.
* **Kontener**: obiektów blob i kontenera danych mogą być odczytywane za pomocą żądania od użytkowników anonimowych. Klientów można wyliczyć obiektów blob w kontenerze hello za pomocą żądania od użytkowników anonimowych, ale nie można wyliczyć kontenery w ramach konta magazynu hello.

Witaj poniższym przykładzie pokazano, jak toocreate a kontener z **kontenera** uprawnienia, które zezwoli na dostęp publiczny, tylko do odczytu dla wszystkich użytkowników na powitania Internet dostępu:

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

## <a name="upload-a-blob-into-a-container"></a>Przekazywanie obiektu blob do kontenera
Jak wspomniano w hello [pojęcia dotyczące usługi Blob](#blob-service-concepts) sekcji magazynu obiektów Blob udostępnia trzy typy obiektów blob: blokowe obiekty BLOB, uzupełnialnych obiektów blob i stronicowe. Biblioteka systemu iOS usługi Azure Storage Hello obsługuje wszystkie trzy typy obiektów blob. W większości przypadków blokowych obiektów blob jest hello zalecane toouse typu.

Witaj poniższy przykład pokazuje, jak tooupload blokowych obiektów blob z NSString. Jeśli obiekt blob o takiej nazwie już istnieje w tym kontenerze powitalne hello zawartość tego obiektu blob zostaną zastąpione.

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

Można potwierdzić, że to działa, analizując hello [Eksploratora usługi Microsoft Azure Storage](http://storageexplorer.com) i weryfikowania tego kontenera hello *containerpublic*, zawiera hello blob *sampleblob*. W tym przykładzie użyliśmy publicznego kontenera, można również sprawdzić, czy ta aplikacja pracy będzie toohello obiekty BLOB identyfikatora URI:

    https://nameofyourstorageaccount.blob.core.windows.net/containerpublic/sampleblob

Ponadto toouploading blokowych obiektów blob z NSString podobnych metod istnieje NSData, NSInputStream lub pliku lokalnego.

## <a name="list-hello-blobs-in-a-container"></a>Lista hello BLOB w kontenerze
Witaj poniższy przykład przedstawia sposób toolist wszystkie obiekty BLOB w kontenerze. Po wykonaniu tej operacji można mając na uwadze hello następujące parametry:     

* **continuationToken** — Witaj reprezentuje token kontynuacji, gdzie powinna zaczynać się hello listę operacji. Jeśli token nie zostanie podany, będzie zawierała listę obiektów BLOB od początku hello. Dowolną liczbę obiektów blob może być wymieniona od zera się tooa wartość maksymalna. Nawet jeśli ta metoda zwraca wyników, jeśli `results.continuationToken` nie jest tokenem nil, może być więcej obiektów blob na powitania usługi, które nie zostały wymienione.
* **prefiks** — można określić hello prefiks toouse listę obiektów blob. Zostaną wyświetlone tylko te obiekty BLOB, zaczynające się z tym prefiksem.
* **useFlatBlobListing** — jak wspomniano w hello [nazewnictwa i odwołuje się do kontenerów i obiektów blob](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata) sekcji hello usługi obiektów Blob jest schemat płaskiej magazynu można utworzyć wirtualnego hierarchii za pomocą nazw obiektów blob ze ścieżką informacje. Jednak lista-flat nie jest obecnie obsługiwane. Ta funkcja będzie dostępna wkrótce. Obecnie ta wartość powinna być **tak**.

* **blobListingDetails** -tooinclude elementów, które można określić podczas wyświetlania obiektów blob
  * _AZSBlobListingDetailsNone_: wyświetlanie tylko zatwierdzone obiektów blob, a nie zwracać metadane obiektu blob.
  * _AZSBlobListingDetailsSnapshots_: wyświetlanie obiektów blob zatwierdzone i migawki obiektu blob.
  * _AZSBlobListingDetailsMetadata_: pobieranie metadane obiektu blob dla każdego obiektu blob zwrócił liście hello.
  * _AZSBlobListingDetailsUncommittedBlobs_: wyświetlanie zatwierdzonej i niezatwierdzone obiektów blob.
  * _AZSBlobListingDetailsCopy_: obejmują kopiowania właściwości liście hello.
  * _AZSBlobListingDetailsAll_: wyświetlić listę wszystkich dostępnych obiektów blob zatwierdzone, niezatwierdzone obiekty BLOB i migawki, a następnie wróć wszystkich metadanych i kopia stanu dla tych obiektów blob.
* **maxResults** — Witaj maksymalną liczbę wyników tooreturn dla tej operacji. Użyj wartości -1 toonot ustawienie limitu.
* **completionHandler** -hello blok kodu tooexecute z wynikiem hello hello listę operacji.

W tym przykładzie metoda pomocnika jest toorecursively używane wywołania hello listy obiektów blob metoda, za każdym razem, gdy token kontynuacji jest zwracany.

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

## <a name="download-a-blob"></a>Pobieranie obiektu blob
powitania po przykładzie pokazano, jak toodownload obiektu blob tooa NSString.

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

## <a name="delete-a-blob"></a>Usuwanie obiektu blob
powitania po przykładzie pokazano, jak toodelete obiektu blob.

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

## <a name="delete-a-blob-container"></a>Usunięcie kontenera obiektów blob
powitania po przykładzie pokazano, jak toodelete kontenera.

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

## <a name="next-steps"></a>Następne kroki
Teraz, kiedy znasz już jak toouse magazynu obiektów Blob z systemem iOS, wykonaj te toolearn łącza więcej informacji na temat biblioteki z systemem iOS hello i hello usługi magazynu.

* [Biblioteka klienta usługi Azure Storage dla systemu iOS](https://github.com/azure/azure-storage-ios)
* [IOS magazynu Azure dokumentacji](http://azure.github.io/azure-storage-ios/)
* [Interfejs API REST usług Azure Storage](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Blog zespołu odpowiedzialnego za usługę Azure Storage](http://blogs.msdn.com/b/windowsazurestorage)

Jeśli masz pytania dotyczące tej biblioteki, możesz tooour wolnego toopost [forum MSDN Azure](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=windowsazuredata) lub [przepełnienie stosu](http://stackoverflow.com/questions/tagged/windows-azure-storage+or+windows-azure-storage+or+azure-storage-blobs+or+azure-storage-tables+or+azure-table-storage+or+windows-azure-queues+or+azure-storage-queues+or+azure-storage-emulator+or+azure-storage-files).
Jeśli masz sugestie funkcji usługi Azure Storage, Opublikuj zbyt[opinii magazynu Azure](https://feedback.azure.com/forums/217298-storage/).

