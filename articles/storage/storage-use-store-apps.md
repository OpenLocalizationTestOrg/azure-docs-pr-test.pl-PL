---
title: aaaUse magazynu Azure w aplikacjach Sklepu Windows | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toocreate ze Sklepu Windows aplikacji, która korzysta z magazynu obiektów Blob platformy Azure, kolejki, tabeli lub pliku."
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
ms.openlocfilehash: ac21b0695c0d77c1d81c1b921718fb929945d45e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-storage-in-windows-store-apps"></a>Jak toouse usługi Azure Storage w aplikacjach w Sklepie Windows
## <a name="overview"></a>Omówienie
Ten przewodnik przedstawia, jak tooget wprowadzenie do opracowywania aplikacji w Sklepie Windows, który korzysta z usługi Azure Storage.

## <a name="download-required-tools"></a>Pobierz wymagane narzędzia
* [Visual Studio](https://www.visualstudio.com/downloads/) umożliwia łatwe toobuild debugowania, lokalizowanie, pakowanie i wdrażanie aplikacji ze Sklepu Windows. Visual Studio 2012 lub nowszy jest wymagany.
* Witaj [biblioteki klienta magazynu Azure](https://www.nuget.org/packages/WindowsAzure.Storage) zawiera Biblioteka klas środowiska wykonawczego systemu Windows do pracy z usługą Azure Storage.
* [WCF Data Services narzędzia dla aplikacji ze Sklepu Windows](http://www.microsoft.com/download/details.aspx?id=30714) rozszerza hello Dodaj odwołanie do usługi obsługi z obsługą OData po stronie klienta dla aplikacji ze Sklepu Windows w programie Visual Studio.

## <a name="develop-apps"></a>Tworzenie aplikacji
### <a name="getting-ready"></a>Przygotowanie
Utwórz nowy projekt aplikacji Sklepu Windows w programie Visual Studio 2012 lub nowszym:

![Magazyn — aplikacje magazynu--projekt vs][store-apps-storage-vs-project]

Następnie dodaj toohello odwołanie do biblioteki klienta magazynu Azure, klikając prawym przyciskiem myszy **odwołania**, klikając pozycję **Dodaj odwołanie**, a następnie przeglądać toohello magazynu klienta biblioteki dla środowiska wykonawczego systemu Windows które pobrane:

![Magazyn aplikacji magazynu wybierz biblioteki][store-apps-storage-choose-library]

### <a name="using-hello-library-with-hello-blob-and-queue-services"></a>Przy użyciu biblioteki hello z hello obiektów Blob i kolejki usług
W tym momencie aplikacji jest gotowy toocall hello usługi kolejek i obiektów Blob platformy Azure. Dodaj następujące hello **przy użyciu** instrukcje, aby typy magazynu Azure można odwoływać się bezpośrednio:

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
```

Następnie dodaj stronę tooyour przycisku. Dodaj hello następującego kodu tooits **kliknij** zdarzeń i zmodyfikuj metodę procedury obsługi zdarzeń za pomocą hello [async — słowo kluczowe](http://msdn.microsoft.com/library/vstudio/hh156513.aspx):

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var blobClient = account.CreateCloudBlobClient();
var container = blobClient.GetContainerReference("container1");
await container.CreateIfNotExistsAsync();
```

Ten kod założono, że dwie zmienne ciągu, *accountName* i *accountKey*. Reprezentują hello nazwę konta i hello klucz konta magazynu skojarzonego z tym kontem.

Tworzenie i uruchamianie aplikacji hello. Kliknięcie przycisku hello sprawdzi, czy kontener o nazwie *container1* istnieje na koncie, a następnie utwórz ją, jeśli nie.

### <a name="using-hello-library-with-hello-table-service"></a>Korzystanie z biblioteki hello z hello usługi tabel
Typy, które są używane toocommunicate z usługą Azure tabeli hello są zależne od usługi danych WCF dla biblioteki aplikacji Sklepu Windows hello. Następnie dodaj wymagane toohello odwołanie do biblioteki WCF za pomocą hello Konsola Menedżera pakietów:

![Magazyn — aplikacje magazynu-— Menedżera pakietów][store-apps-storage-package-manager]

Witaj Użyj następującego polecenia toopoint toohello Menedżera pakietów lokalizacji na komputerze:

    Install-Package Microsoft.Data.OData.WindowsStore -Source "C:\Program Files (x86)\Microsoft WCF Data Services\5.0\bin\NuGet"

To polecenie spowoduje automatyczne dodanie wszystkich wymaganych odwołania tooyour projektu. Jeśli nie chcesz, aby toouse hello Konsola Menedżera pakietów, można dodać folder NuGet usługi danych WCF hello na liście toohello komputera lokalnego źródła pakietów i następnie dodać odwołanie hello za pośrednictwem hello interfejsu użytkownika, zgodnie z opisem w [zarządzania pomocą pakietów NuGet okno dialogowe Hello](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog).

Gdy ma odwołanie do pakietu NuGet usługi danych WCF hello, Zmień kod hello w Twojej przycisku **kliknij** zdarzeń:

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var tableClient = account.CreateCloudTableClient();
var table = tableClient.GetTableReference("table1");
await table.CreateIfNotExistsAsync();
```

Ten kod sprawdza, czy tabela o nazwie *table1* istnieje na koncie, a następnie tworzy, jeśli nie.

Można również dodać tooMicrosoft.WindowsAzure.Storage.Table.dll odwołania, który jest dostępny w hello sam pakiet został pobrany. Ta biblioteka zawiera dodatkowe funkcje, takie jak oparty na odbiciu serializacji i rodzajowy zapytania. Należy pamiętać, że ta biblioteka nie obsługuje języka JavaScript.

[store-apps-storage-vs-project]: ./media/storage-use-store-apps/store-apps-storage-vs-project.png
[store-apps-storage-choose-library]: ./media/storage-use-store-apps/store-apps-storage-choose-library.png
[store-apps-storage-package-manager]: ./media/storage-use-store-apps/store-apps-storage-package-manager.png
