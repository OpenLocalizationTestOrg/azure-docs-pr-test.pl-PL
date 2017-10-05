---
title: "Użyj magazynu Azure w aplikacjach Sklepu Windows | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć aplikację ze Sklepu Windows korzystającym z magazynu obiektów Blob platformy Azure, kolejki, tabeli lub pliku."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 63c4b29d-b2f2-4d7c-b164-a0d38f4d14f6
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 43d38584270fbbbe6fa4e4ff8cef72ca44e14acc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-azure-storage-in-windows-store-apps"></a>Jak używać magazynu Azure w aplikacjach w Sklepie Windows
## <a name="overview"></a>Omówienie
W tym przewodniku pokazano, jak rozpocząć tworzenie aplikacji Sklepu Windows, która korzysta z usługi Azure Storage.

## <a name="download-required-tools"></a>Pobierz wymagane narzędzia
* [Visual Studio](https://www.visualstudio.com/downloads/) ułatwia tworzenie, debugowanie, lokalizowanie, pakowanie i wdrażanie aplikacji ze Sklepu Windows. Visual Studio 2012 lub nowszy jest wymagany.
* [Biblioteki klienta magazynu Azure](https://www.nuget.org/packages/WindowsAzure.Storage) zawiera Biblioteka klas środowiska wykonawczego systemu Windows do pracy z usługą Azure Storage.
* [WCF Data Services narzędzia dla aplikacji ze Sklepu Windows](http://www.microsoft.com/download/details.aspx?id=30714) rozszerza środowisko Dodaj odwołanie do usługi z obsługą OData po stronie klienta dla aplikacji ze Sklepu Windows w programie Visual Studio.

## <a name="develop-apps"></a>Tworzenie aplikacji
### <a name="getting-ready"></a>Przygotowanie
Utwórz nowy projekt aplikacji Sklepu Windows w programie Visual Studio 2012 lub nowszym:

![Magazyn — aplikacje magazynu--projekt vs][store-apps-storage-vs-project]

Następnie dodaj odwołanie do biblioteki klienta magazynu Azure, klikając prawym przyciskiem myszy **odwołania**, klikając pozycję **Dodaj odwołanie**i następnie przejdź do biblioteki klienta magazynu dla Windows Runtime które pobrane:

![Magazyn aplikacji magazynu wybierz biblioteki][store-apps-storage-choose-library]

### <a name="using-the-library-with-the-blob-and-queue-services"></a>Korzystanie z biblioteki usługi obiektów Blob i kolejek
W tym momencie że aplikacja jest gotowa do wywoływania usług obiektów Blob platformy Azure i kolejki. Dodaj następujące **przy użyciu** instrukcje, aby typy magazynu Azure można odwoływać się bezpośrednio:

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
```

Następnie dodaj przycisk do strony. Dodaj następujący kod do jego **kliknij** zdarzeń i zmodyfikuj metodę procedury obsługi zdarzeń za pomocą [async — słowo kluczowe](http://msdn.microsoft.com/library/vstudio/hh156513.aspx):

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var blobClient = account.CreateCloudBlobClient();
var container = blobClient.GetContainerReference("container1");
await container.CreateIfNotExistsAsync();
```

Ten kod założono, że dwie zmienne ciągu, *accountName* i *accountKey*. Reprezentują nazwy konta magazynu i klucza konta, który jest skojarzony z tym kontem.

Skompiluj i uruchom aplikację. Kliknięcie przycisku sprawdzi, czy kontener o nazwie *container1* istnieje na koncie, a następnie utwórz ją, jeśli nie.

### <a name="using-the-library-with-the-table-service"></a>Za pomocą biblioteki z usługi tabel
Typy, które są używane do komunikacji z usługą Azure tabeli są zależne od usługi danych WCF dla biblioteki aplikacji Sklepu Windows. Następnie dodaj odwołanie do wymaganych bibliotek usługi WCF za pomocą konsoli Menedżera pakietów:

![Magazyn — aplikacje magazynu-— Menedżera pakietów][store-apps-storage-package-manager]

Użyj następującego polecenia do Menedżera pakietów punkt lokalizacji na komputerze:

    Install-Package Microsoft.Data.OData.WindowsStore -Source "C:\Program Files (x86)\Microsoft WCF Data Services\5.0\bin\NuGet"

To polecenie spowoduje automatyczne dodanie wszystkich wymaganych odwołań do projektu. Jeśli nie chcesz używać konsoli Menedżera pakietów, można dodać folderu NuGet usługi danych WCF na komputerze lokalnym, do listy źródeł pakietów i następnie dodać odwołanie za pośrednictwem interfejsu użytkownika, zgodnie z opisem w [Zarządzanie NuGet pakietów przy użyciu okna dialogowego ](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog).

Gdy ma odwołanie do pakietu NuGet usługi danych WCF, Zmień kod w Twojej przycisk **kliknij** zdarzeń:

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var tableClient = account.CreateCloudTableClient();
var table = tableClient.GetTableReference("table1");
await table.CreateIfNotExistsAsync();
```

Ten kod sprawdza, czy tabela o nazwie *table1* istnieje na koncie, a następnie tworzy, jeśli nie.

Można również dodać odwołanie do Microsoft.WindowsAzure.Storage.Table.dll, który jest dostępny w tym samym pakiecie, który został pobrany. Ta biblioteka zawiera dodatkowe funkcje, takie jak oparty na odbiciu serializacji i rodzajowy zapytania. Należy pamiętać, że ta biblioteka nie obsługuje języka JavaScript.

[store-apps-storage-vs-project]: ./media/storage-use-store-apps/store-apps-storage-vs-project.png
[store-apps-storage-choose-library]: ./media/storage-use-store-apps/store-apps-storage-choose-library.png
[store-apps-storage-package-manager]: ./media/storage-use-store-apps/store-apps-storage-package-manager.png
