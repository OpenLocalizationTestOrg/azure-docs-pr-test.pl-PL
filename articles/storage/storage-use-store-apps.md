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
# <a name="how-toouse-azure-storage-in-windows-store-apps"></a><span data-ttu-id="b5d40-103">Jak toouse usługi Azure Storage w aplikacjach w Sklepie Windows</span><span class="sxs-lookup"><span data-stu-id="b5d40-103">How toouse Azure Storage in Windows Store apps</span></span>
## <a name="overview"></a><span data-ttu-id="b5d40-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="b5d40-104">Overview</span></span>
<span data-ttu-id="b5d40-105">Ten przewodnik przedstawia, jak tooget wprowadzenie do opracowywania aplikacji w Sklepie Windows, który korzysta z usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="b5d40-105">This guide shows how tooget started with developing a Windows Store app that makes use of Azure Storage.</span></span>

## <a name="download-required-tools"></a><span data-ttu-id="b5d40-106">Pobierz wymagane narzędzia</span><span class="sxs-lookup"><span data-stu-id="b5d40-106">Download required tools</span></span>
* <span data-ttu-id="b5d40-107">[Visual Studio](https://www.visualstudio.com/downloads/) umożliwia łatwe toobuild debugowania, lokalizowanie, pakowanie i wdrażanie aplikacji ze Sklepu Windows.</span><span class="sxs-lookup"><span data-stu-id="b5d40-107">[Visual Studio](https://www.visualstudio.com/downloads/) makes it easy toobuild, debug, localize, package, and deploy Windows Store apps.</span></span> <span data-ttu-id="b5d40-108">Visual Studio 2012 lub nowszy jest wymagany.</span><span class="sxs-lookup"><span data-stu-id="b5d40-108">Visual Studio 2012 or later is required.</span></span>
* <span data-ttu-id="b5d40-109">Witaj [biblioteki klienta magazynu Azure](https://www.nuget.org/packages/WindowsAzure.Storage) zawiera Biblioteka klas środowiska wykonawczego systemu Windows do pracy z usługą Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="b5d40-109">hello [Azure Storage Client Library](https://www.nuget.org/packages/WindowsAzure.Storage) provides a Windows Runtime class library for working with Azure Storage.</span></span>
* <span data-ttu-id="b5d40-110">[WCF Data Services narzędzia dla aplikacji ze Sklepu Windows](http://www.microsoft.com/download/details.aspx?id=30714) rozszerza hello Dodaj odwołanie do usługi obsługi z obsługą OData po stronie klienta dla aplikacji ze Sklepu Windows w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b5d40-110">[WCF Data Services Tools for Windows Store Apps](http://www.microsoft.com/download/details.aspx?id=30714) extends hello Add Service Reference experience with client-side OData support for Windows Store apps in Visual Studio.</span></span>

## <a name="develop-apps"></a><span data-ttu-id="b5d40-111">Tworzenie aplikacji</span><span class="sxs-lookup"><span data-stu-id="b5d40-111">Develop apps</span></span>
### <a name="getting-ready"></a><span data-ttu-id="b5d40-112">Przygotowanie</span><span class="sxs-lookup"><span data-stu-id="b5d40-112">Getting ready</span></span>
<span data-ttu-id="b5d40-113">Utwórz nowy projekt aplikacji Sklepu Windows w programie Visual Studio 2012 lub nowszym:</span><span class="sxs-lookup"><span data-stu-id="b5d40-113">Create a new Windows Store app project in Visual Studio 2012 or later:</span></span>

![Magazyn — aplikacje magazynu--projekt vs][store-apps-storage-vs-project]

<span data-ttu-id="b5d40-115">Następnie dodaj toohello odwołanie do biblioteki klienta magazynu Azure, klikając prawym przyciskiem myszy **odwołania**, klikając pozycję **Dodaj odwołanie**, a następnie przeglądać toohello magazynu klienta biblioteki dla środowiska wykonawczego systemu Windows które pobrane:</span><span class="sxs-lookup"><span data-stu-id="b5d40-115">Next, add a reference toohello Azure Storage Client Library by right-clicking **References**, clicking **Add Reference**, and then browsing toohello Storage Client Library for Windows Runtime that you downloaded:</span></span>

![Magazyn aplikacji magazynu wybierz biblioteki][store-apps-storage-choose-library]

### <a name="using-hello-library-with-hello-blob-and-queue-services"></a><span data-ttu-id="b5d40-117">Przy użyciu biblioteki hello z hello obiektów Blob i kolejki usług</span><span class="sxs-lookup"><span data-stu-id="b5d40-117">Using hello library with hello Blob and Queue services</span></span>
<span data-ttu-id="b5d40-118">W tym momencie aplikacji jest gotowy toocall hello usługi kolejek i obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b5d40-118">At this point, your app is ready toocall hello Azure Blob and Queue services.</span></span> <span data-ttu-id="b5d40-119">Dodaj następujące hello **przy użyciu** instrukcje, aby typy magazynu Azure można odwoływać się bezpośrednio:</span><span class="sxs-lookup"><span data-stu-id="b5d40-119">Add hello following **using** statements so that Azure Storage types can be referenced directly:</span></span>

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
```

<span data-ttu-id="b5d40-120">Następnie dodaj stronę tooyour przycisku.</span><span class="sxs-lookup"><span data-stu-id="b5d40-120">Next, add a button tooyour page.</span></span> <span data-ttu-id="b5d40-121">Dodaj hello następującego kodu tooits **kliknij** zdarzeń i zmodyfikuj metodę procedury obsługi zdarzeń za pomocą hello [async — słowo kluczowe](http://msdn.microsoft.com/library/vstudio/hh156513.aspx):</span><span class="sxs-lookup"><span data-stu-id="b5d40-121">Add hello following code tooits **Click** event and modify your event handler method by using hello [async keyword](http://msdn.microsoft.com/library/vstudio/hh156513.aspx):</span></span>

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var blobClient = account.CreateCloudBlobClient();
var container = blobClient.GetContainerReference("container1");
await container.CreateIfNotExistsAsync();
```

<span data-ttu-id="b5d40-122">Ten kod założono, że dwie zmienne ciągu, *accountName* i *accountKey*.</span><span class="sxs-lookup"><span data-stu-id="b5d40-122">This code assumes that you have two string variables, *accountName* and *accountKey*.</span></span> <span data-ttu-id="b5d40-123">Reprezentują hello nazwę konta i hello klucz konta magazynu skojarzonego z tym kontem.</span><span class="sxs-lookup"><span data-stu-id="b5d40-123">They represent hello name of your storage account and hello account key that is associated with that account.</span></span>

<span data-ttu-id="b5d40-124">Tworzenie i uruchamianie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="b5d40-124">Build and run hello application.</span></span> <span data-ttu-id="b5d40-125">Kliknięcie przycisku hello sprawdzi, czy kontener o nazwie *container1* istnieje na koncie, a następnie utwórz ją, jeśli nie.</span><span class="sxs-lookup"><span data-stu-id="b5d40-125">Clicking hello button will check whether a container named *container1* exists in your account and then create it if not.</span></span>

### <a name="using-hello-library-with-hello-table-service"></a><span data-ttu-id="b5d40-126">Korzystanie z biblioteki hello z hello usługi tabel</span><span class="sxs-lookup"><span data-stu-id="b5d40-126">Using hello library with hello Table service</span></span>
<span data-ttu-id="b5d40-127">Typy, które są używane toocommunicate z usługą Azure tabeli hello są zależne od usługi danych WCF dla biblioteki aplikacji Sklepu Windows hello.</span><span class="sxs-lookup"><span data-stu-id="b5d40-127">Types that are used toocommunicate with hello Azure Table service depend on WCF Data Services for hello Windows Store app library.</span></span> <span data-ttu-id="b5d40-128">Następnie dodaj wymagane toohello odwołanie do biblioteki WCF za pomocą hello Konsola Menedżera pakietów:</span><span class="sxs-lookup"><span data-stu-id="b5d40-128">Next, add a reference toohello required WCF libraries by using hello Package Manager Console:</span></span>

![Magazyn — aplikacje magazynu-— Menedżera pakietów][store-apps-storage-package-manager]

<span data-ttu-id="b5d40-130">Witaj Użyj następującego polecenia toopoint toohello Menedżera pakietów lokalizacji na komputerze:</span><span class="sxs-lookup"><span data-stu-id="b5d40-130">Use hello following command toopoint Package Manager toohello location on your machine:</span></span>

    Install-Package Microsoft.Data.OData.WindowsStore -Source "C:\Program Files (x86)\Microsoft WCF Data Services\5.0\bin\NuGet"

<span data-ttu-id="b5d40-131">To polecenie spowoduje automatyczne dodanie wszystkich wymaganych odwołania tooyour projektu.</span><span class="sxs-lookup"><span data-stu-id="b5d40-131">This command will automatically add all required references tooyour project.</span></span> <span data-ttu-id="b5d40-132">Jeśli nie chcesz, aby toouse hello Konsola Menedżera pakietów, można dodać folder NuGet usługi danych WCF hello na liście toohello komputera lokalnego źródła pakietów i następnie dodać odwołanie hello za pośrednictwem hello interfejsu użytkownika, zgodnie z opisem w [zarządzania pomocą pakietów NuGet okno dialogowe Hello](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog).</span><span class="sxs-lookup"><span data-stu-id="b5d40-132">If you do not want toouse hello Package Manager Console, you can add hello WCF Data Services NuGet folder on your local machine toohello list of package sources and then add hello reference through hello UI, as described in [Managing NuGet Packages Using hello Dialog](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog).</span></span>

<span data-ttu-id="b5d40-133">Gdy ma odwołanie do pakietu NuGet usługi danych WCF hello, Zmień kod hello w Twojej przycisku **kliknij** zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="b5d40-133">When you have referenced hello WCF Data Services NuGet package, change hello code in your button's **Click** event:</span></span>

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var tableClient = account.CreateCloudTableClient();
var table = tableClient.GetTableReference("table1");
await table.CreateIfNotExistsAsync();
```

<span data-ttu-id="b5d40-134">Ten kod sprawdza, czy tabela o nazwie *table1* istnieje na koncie, a następnie tworzy, jeśli nie.</span><span class="sxs-lookup"><span data-stu-id="b5d40-134">This code checks whether a table named *table1* exists in your account, and then creates it if not.</span></span>

<span data-ttu-id="b5d40-135">Można również dodać tooMicrosoft.WindowsAzure.Storage.Table.dll odwołania, który jest dostępny w hello sam pakiet został pobrany.</span><span class="sxs-lookup"><span data-stu-id="b5d40-135">You can also add a reference tooMicrosoft.WindowsAzure.Storage.Table.dll, which is available in hello same package that you downloaded.</span></span> <span data-ttu-id="b5d40-136">Ta biblioteka zawiera dodatkowe funkcje, takie jak oparty na odbiciu serializacji i rodzajowy zapytania.</span><span class="sxs-lookup"><span data-stu-id="b5d40-136">This library contains additional functionality, such as reflection-based serialization and generic queries.</span></span> <span data-ttu-id="b5d40-137">Należy pamiętać, że ta biblioteka nie obsługuje języka JavaScript.</span><span class="sxs-lookup"><span data-stu-id="b5d40-137">Note that this library does not support JavaScript.</span></span>

[store-apps-storage-vs-project]: ./media/storage-use-store-apps/store-apps-storage-vs-project.png
[store-apps-storage-choose-library]: ./media/storage-use-store-apps/store-apps-storage-choose-library.png
[store-apps-storage-package-manager]: ./media/storage-use-store-apps/store-apps-storage-package-manager.png
