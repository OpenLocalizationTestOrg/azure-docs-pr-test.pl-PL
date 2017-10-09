---
title: "aaaEnable publiczny dostęp do odczytu do kontenerów i obiektów blob w magazynie obiektów Blob platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomake kontenerów i obiektów blob jest dostępna dla dostępu anonimowego i w jaki sposób tooaccess je programowo."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: a2cffee6-3224-4f2a-8183-66ca23b2d2d7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: marsma
ms.openlocfilehash: 0675b5dc4d32a3a0a34376ae4c049542b07ba03a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-anonymous-read-access-toocontainers-and-blobs"></a>Zarządzanie toocontainers anonimowy dostęp do odczytu i obiektów blob
Można włączyć anonimowego, publiczny dostęp do odczytu tooa kontenera i jego obiektów blob w magazynie obiektów Blob Azure. W ten sposób można przyznać dostęp tylko do odczytu zasobów toothese bez udostępniania swój klucz konta usługi i bez konieczności sygnatury dostępu współdzielonego (SAS).

Najlepiej w scenariuszach, w miejsce niektórych obiektów blob tooalways można anonimowy dostęp do odczytu jest publiczny dostęp do odczytu. Aby uzyskać bardziej precyzyjną kontrolę można utworzyć sygnatury dostępu współdzielonego. Sygnatury dostępu współdzielonego umożliwiają tooprovide ograniczony dostęp przy użyciu różnych uprawnień w określonym przedziale czasu. Aby uzyskać więcej informacji o tworzeniu udostępnionych sygnatur dostępu, zobacz [używanie udostępnionych sygnatur dostępu (SAS) w usłudze Azure Storage](storage-dotnet-shared-access-signature-part-1.md).

## <a name="grant-anonymous-users-permissions-toocontainers-and-blobs"></a>Udziel toocontainers uprawnień użytkowników anonimowych, jak i obiektów blob
Domyślnie kontener i wszystkie obiekty BLOB w nim mogą być używane tylko przez właściciela hello hello konta magazynu. toogive anonimowym użytkownikom uprawnienia do odczytu tooa kontenera i jego obiektów blob, można ustawić dostępu publicznego tooallow hello kontenera uprawnienia. Użytkownicy anonimowi mogą odczytywać obiekty BLOB w kontenerze publicznie bez uwierzytelniania hello żądania.

Można skonfigurować kontener hello następujących uprawnień:

* **Dostęp do odczytu żadnego elementu publicznego public:** hello kontenera i jego obiektów blob są dostępne tylko przez właściciela konta magazynu hello. Jest to domyślna powitania dla wszystkich nowych kontenerów.
* **Dostęp do obiektów blob tylko odczytu publicznego:** obiekty BLOB w kontenerze hello może zostać odczytany przez żądania od użytkowników anonimowych, ale nie są dostępne dane kontenera. Anonimowe klientów nie można wyliczyć obiektów blob hello w kontenerze hello.
* **Pełne publiczny dostęp do odczytu:** wszystkie dane obiektów blob i kontener może zostać odczytany przez żądania od użytkowników anonimowych. Klientów można wyliczyć obiektów blob w kontenerze hello przez żądania od użytkowników anonimowych, ale nie można wyliczyć kontenery w ramach konta magazynu hello.

Można użyć następujących uprawnień kontenera tooset hello:

* [Witryna Azure Portal](https://portal.azure.com)
* [Azure PowerShell](storage-powershell-guide-full.md#how-to-manage-azure-blobs)
* [Interfejs wiersza polecenia platformy Azure 2.0](storage-azure-cli.md#create-and-manage-blobs)
* Programowo za pomocą jednej z bibliotek klienckich magazynu hello lub hello interfejsu API REST

### <a name="set-container-permissions-in-hello-azure-portal"></a>Ustaw uprawnienia kontenera w hello portalu Azure
tooset uprawnień kontenera w hello [portalu Azure](https://portal.azure.com), wykonaj następujące kroki:

1. Otwórz z **konta magazynu** bloku w portalu hello. Można znaleźć konta magazynu, wybierając **kont magazynu** w bloku portalu menu głównego hello.
1. W obszarze **usługa BLOB** na powitania bloku menu, wybierz **kontenery**.
1. Kliknij prawym przyciskiem myszy na wiersz kontenera hello lub wybierz hello wielokropka tooopen hello kontenera **menu kontekstowe**.
1. Wybierz **zasady dostępu** w menu kontekstowym hello.
1. Wybierz **dostęp typu** z hello menu rozwijanym.

    ![Okno dialogowe metadanych kontenera Edycja](./media/storage-manage-access-to-resources/storage-manage-access-to-resources-0.png)

### <a name="set-container-permissions-with-net"></a>Ustawianie uprawnień kontenera z platformą .NET
tooset uprawnienia do kontenera przy użyciu języka C# i hello biblioteki klienta usługi Storage dla platformy .NET, najpierw pobrać kontenera hello istniejące uprawnienia przez wywołanie hello **GetPermissions** metody. Następnie zestaw hello **PublicAccess** właściwość hello **BlobContainerPermissions** obiektu, który jest zwracany przez hello **GetPermissions** metody. Na koniec wywołania hello **ustawiania** metody z hello zaktualizowano uprawnienia.

Poniższy przykład Hello ustawia uprawnienia kontenera hello toofull publiczny dostęp do odczytu. dostęp do odczytu tooset toopublic uprawnienia dla obiektów blob, należy ustawić hello **PublicAccess** właściwości zbyt**BlobContainerPublicAccessType.Blob**. Ustaw wszystkie uprawnienia dla użytkowników anonimowych tooremove zbyt hello właściwości**BlobContainerPublicAccessType.Off**.

```csharp
public static void SetPublicContainerPermissions(CloudBlobContainer container)
{
    BlobContainerPermissions permissions = container.GetPermissions();
    permissions.PublicAccess = BlobContainerPublicAccessType.Container;
    container.SetPermissions(permissions);
}
```

## <a name="access-containers-and-blobs-anonymously"></a>Dostęp do kontenerów i obiektów blob anonimowo
Klient, który uzyskuje dostęp do kontenerów i obiektów blob anonimowo można użyć konstruktorów, które nie wymagają poświadczeń. Następujące przykłady Hello Pokaż na kilka różnych sposobów zasoby usługi Blob tooreference anonimowo.

### <a name="create-an-anonymous-client-object"></a>Tworzenie obiektu anonimowego klienta
Można utworzyć nowy obiekt klienta usługi dla dostępu anonimowego, podając punkt końcowy usługi Blob hello hello konta. Należy jednak znać nazwę hello kontenera na tym koncie, który jest dostępny dla dostępu anonimowego.

```csharp
public static void CreateAnonymousBlobClient()
{
    // Create hello client object using hello Blob service endpoint.
    CloudBlobClient blobClient = new CloudBlobClient(new Uri(@"https://storagesample.blob.core.windows.net"));

    // Get a reference tooa container that's available for anonymous access.
    CloudBlobContainer container = blobClient.GetContainerReference("sample-container");

    // Read hello container's properties. Note this is only possible when hello container supports full public read access.
    container.FetchAttributes();
    Console.WriteLine(container.Properties.LastModified);
    Console.WriteLine(container.Properties.ETag);
}
```

### <a name="reference-a-container-anonymously"></a>Odwołanie kontenera anonimowego
Jeśli masz hello adres URL tooa kontener, który jest dostępny anonimowo umożliwia kontenera hello tooreference bezpośrednio.

```csharp
public static void ListBlobsAnonymously()
{
    // Get a reference tooa container that's available for anonymous access.
    CloudBlobContainer container = new CloudBlobContainer(new Uri(@"https://storagesample.blob.core.windows.net/sample-container"));

    // List blobs in hello container.
    foreach (IListBlobItem blobItem in container.ListBlobs())
    {
        Console.WriteLine(blobItem.Uri);
    }
}
```

### <a name="reference-a-blob-anonymously"></a>Odwołanie obiektu blob anonimowo
Jeśli masz hello adresu URL tooa blob, który jest dostępny dla dostępu anonimowego, możesz odwoływać się do obiektu blob hello bezpośrednio przy użyciu tego adresu URL:

```csharp
public static void DownloadBlobAnonymously()
{
    CloudBlockBlob blob = new CloudBlockBlob(new Uri(@"https://storagesample.blob.core.windows.net/sample-container/logfile.txt"));
    blob.DownloadToFile(@"C:\Temp\logfile.txt", System.IO.FileMode.Create);
}
```

## <a name="features-available-tooanonymous-users"></a>Funkcje dostępne tooanonymous użytkowników
Witaj w poniższej tabeli przedstawiono operacje może zostać wywołana przez anonimowych użytkowników, gdy ACL kontenera ustawiono tooallow dostępu publicznego.

| Operacji REST | Uprawnienie o pełnej publiczny dostęp do odczytu | Uprawnienie o publiczny dostęp do odczytu obiektów blob tylko |
| --- | --- | --- |
| Kontenery listy |Tylko właściciel |Tylko właściciel |
| Tworzenie kontenera |Tylko właściciel |Tylko właściciel |
| Pobierz właściwości kontenera |Wszystkie |Tylko właściciel |
| Pobranie metadanych kontenera |Wszystkie |Tylko właściciel |
| Ustaw metadanych kontenera |Tylko właściciel |Tylko właściciel |
| Pobierz ACL kontenera |Tylko właściciel |Tylko właściciel |
| Ustaw ACL kontenera |Tylko właściciel |Tylko właściciel |
| Usunąć kontenera |Tylko właściciel |Tylko właściciel |
| Lista obiektów blob |Wszystkie |Tylko właściciel |
| Umieszczanie obiektu Blob |Tylko właściciel |Tylko właściciel |
| Pobierz obiekt Blob |Wszystkie |Wszystkie |
| Pobierz właściwości obiektu Blob |Wszystkie |Wszystkie |
| Ustaw właściwości obiektów Blob |Tylko właściciel |Tylko właściciel |
| Pobierz metadane obiektu Blob |Wszystkie |Wszystkie |
| Ustaw metadane obiektu Blob |Tylko właściciel |Tylko właściciel |
| Umieść bloku |Tylko właściciel |Tylko właściciel |
| Pobierz listę zablokowanych (tylko zatwierdzone bloki) |Wszystkie |Wszystkie |
| Pobierz listę bloku (tylko niezatwierdzone bloków lub wszystkie bloki) |Tylko właściciel |Tylko właściciel |
| Umieść zablokowanych |Tylko właściciel |Tylko właściciel |
| Usuwanie obiektów Blob |Tylko właściciel |Tylko właściciel |
| Kopiowanie obiektu Blob |Tylko właściciel |Tylko właściciel |
| Migawki obiektu Blob |Tylko właściciel |Tylko właściciel |
| Obiekt Blob dzierżawy |Tylko właściciel |Tylko właściciel |
| Umieść stronę |Tylko właściciel |Tylko właściciel |
| Get zakresów stron |Wszystkie |Wszystkie |
| Dołącz obiektów Blob |Tylko właściciel |Tylko właściciel |

## <a name="next-steps"></a>Następne kroki

* [Uwierzytelnianie dla hello usług magazynu Azure](https://msdn.microsoft.com/library/azure/dd179428.aspx)
* [Przy użyciu sygnatury dostępu współdzielonego (SAS)](storage-dotnet-shared-access-signature-part-1.md)
* [Delegowanie dostępu za pomocą sygnatury dostępu współdzielonego](https://msdn.microsoft.com/library/azure/ee395415.aspx)
