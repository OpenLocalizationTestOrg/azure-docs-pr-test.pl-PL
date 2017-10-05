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
# <a name="how-to-use-azure-storage-in-windows-store-apps"></a><span data-ttu-id="0d423-103">Jak używać magazynu Azure w aplikacjach w Sklepie Windows</span><span class="sxs-lookup"><span data-stu-id="0d423-103">How to use Azure Storage in Windows Store apps</span></span>
## <a name="overview"></a><span data-ttu-id="0d423-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="0d423-104">Overview</span></span>
<span data-ttu-id="0d423-105">W tym przewodniku pokazano, jak rozpocząć tworzenie aplikacji Sklepu Windows, która korzysta z usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="0d423-105">This guide shows how to get started with developing a Windows Store app that makes use of Azure Storage.</span></span>

## <a name="download-required-tools"></a><span data-ttu-id="0d423-106">Pobierz wymagane narzędzia</span><span class="sxs-lookup"><span data-stu-id="0d423-106">Download required tools</span></span>
* <span data-ttu-id="0d423-107">[Visual Studio](https://www.visualstudio.com/downloads/) ułatwia tworzenie, debugowanie, lokalizowanie, pakowanie i wdrażanie aplikacji ze Sklepu Windows.</span><span class="sxs-lookup"><span data-stu-id="0d423-107">[Visual Studio](https://www.visualstudio.com/downloads/) makes it easy to build, debug, localize, package, and deploy Windows Store apps.</span></span> <span data-ttu-id="0d423-108">Visual Studio 2012 lub nowszy jest wymagany.</span><span class="sxs-lookup"><span data-stu-id="0d423-108">Visual Studio 2012 or later is required.</span></span>
* <span data-ttu-id="0d423-109">[Biblioteki klienta magazynu Azure](https://www.nuget.org/packages/WindowsAzure.Storage) zawiera Biblioteka klas środowiska wykonawczego systemu Windows do pracy z usługą Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="0d423-109">The [Azure Storage Client Library](https://www.nuget.org/packages/WindowsAzure.Storage) provides a Windows Runtime class library for working with Azure Storage.</span></span>
* <span data-ttu-id="0d423-110">[WCF Data Services narzędzia dla aplikacji ze Sklepu Windows](http://www.microsoft.com/download/details.aspx?id=30714) rozszerza środowisko Dodaj odwołanie do usługi z obsługą OData po stronie klienta dla aplikacji ze Sklepu Windows w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0d423-110">[WCF Data Services Tools for Windows Store Apps](http://www.microsoft.com/download/details.aspx?id=30714) extends the Add Service Reference experience with client-side OData support for Windows Store apps in Visual Studio.</span></span>

## <a name="develop-apps"></a><span data-ttu-id="0d423-111">Tworzenie aplikacji</span><span class="sxs-lookup"><span data-stu-id="0d423-111">Develop apps</span></span>
### <a name="getting-ready"></a><span data-ttu-id="0d423-112">Przygotowanie</span><span class="sxs-lookup"><span data-stu-id="0d423-112">Getting ready</span></span>
<span data-ttu-id="0d423-113">Utwórz nowy projekt aplikacji Sklepu Windows w programie Visual Studio 2012 lub nowszym:</span><span class="sxs-lookup"><span data-stu-id="0d423-113">Create a new Windows Store app project in Visual Studio 2012 or later:</span></span>

![Magazyn — aplikacje magazynu--projekt vs][store-apps-storage-vs-project]

<span data-ttu-id="0d423-115">Następnie dodaj odwołanie do biblioteki klienta magazynu Azure, klikając prawym przyciskiem myszy **odwołania**, klikając pozycję **Dodaj odwołanie**i następnie przejdź do biblioteki klienta magazynu dla Windows Runtime które pobrane:</span><span class="sxs-lookup"><span data-stu-id="0d423-115">Next, add a reference to the Azure Storage Client Library by right-clicking **References**, clicking **Add Reference**, and then browsing to the Storage Client Library for Windows Runtime that you downloaded:</span></span>

![Magazyn aplikacji magazynu wybierz biblioteki][store-apps-storage-choose-library]

### <a name="using-the-library-with-the-blob-and-queue-services"></a><span data-ttu-id="0d423-117">Korzystanie z biblioteki usługi obiektów Blob i kolejek</span><span class="sxs-lookup"><span data-stu-id="0d423-117">Using the library with the Blob and Queue services</span></span>
<span data-ttu-id="0d423-118">W tym momencie że aplikacja jest gotowa do wywoływania usług obiektów Blob platformy Azure i kolejki.</span><span class="sxs-lookup"><span data-stu-id="0d423-118">At this point, your app is ready to call the Azure Blob and Queue services.</span></span> <span data-ttu-id="0d423-119">Dodaj następujące **przy użyciu** instrukcje, aby typy magazynu Azure można odwoływać się bezpośrednio:</span><span class="sxs-lookup"><span data-stu-id="0d423-119">Add the following **using** statements so that Azure Storage types can be referenced directly:</span></span>

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
```

<span data-ttu-id="0d423-120">Następnie dodaj przycisk do strony.</span><span class="sxs-lookup"><span data-stu-id="0d423-120">Next, add a button to your page.</span></span> <span data-ttu-id="0d423-121">Dodaj następujący kod do jego **kliknij** zdarzeń i zmodyfikuj metodę procedury obsługi zdarzeń za pomocą [async — słowo kluczowe](http://msdn.microsoft.com/library/vstudio/hh156513.aspx):</span><span class="sxs-lookup"><span data-stu-id="0d423-121">Add the following code to its **Click** event and modify your event handler method by using the [async keyword](http://msdn.microsoft.com/library/vstudio/hh156513.aspx):</span></span>

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var blobClient = account.CreateCloudBlobClient();
var container = blobClient.GetContainerReference("container1");
await container.CreateIfNotExistsAsync();
```

<span data-ttu-id="0d423-122">Ten kod założono, że dwie zmienne ciągu, *accountName* i *accountKey*.</span><span class="sxs-lookup"><span data-stu-id="0d423-122">This code assumes that you have two string variables, *accountName* and *accountKey*.</span></span> <span data-ttu-id="0d423-123">Reprezentują nazwy konta magazynu i klucza konta, który jest skojarzony z tym kontem.</span><span class="sxs-lookup"><span data-stu-id="0d423-123">They represent the name of your storage account and the account key that is associated with that account.</span></span>

<span data-ttu-id="0d423-124">Skompiluj i uruchom aplikację.</span><span class="sxs-lookup"><span data-stu-id="0d423-124">Build and run the application.</span></span> <span data-ttu-id="0d423-125">Kliknięcie przycisku sprawdzi, czy kontener o nazwie *container1* istnieje na koncie, a następnie utwórz ją, jeśli nie.</span><span class="sxs-lookup"><span data-stu-id="0d423-125">Clicking the button will check whether a container named *container1* exists in your account and then create it if not.</span></span>

### <a name="using-the-library-with-the-table-service"></a><span data-ttu-id="0d423-126">Za pomocą biblioteki z usługi tabel</span><span class="sxs-lookup"><span data-stu-id="0d423-126">Using the library with the Table service</span></span>
<span data-ttu-id="0d423-127">Typy, które są używane do komunikacji z usługą Azure tabeli są zależne od usługi danych WCF dla biblioteki aplikacji Sklepu Windows.</span><span class="sxs-lookup"><span data-stu-id="0d423-127">Types that are used to communicate with the Azure Table service depend on WCF Data Services for the Windows Store app library.</span></span> <span data-ttu-id="0d423-128">Następnie dodaj odwołanie do wymaganych bibliotek usługi WCF za pomocą konsoli Menedżera pakietów:</span><span class="sxs-lookup"><span data-stu-id="0d423-128">Next, add a reference to the required WCF libraries by using the Package Manager Console:</span></span>

![Magazyn — aplikacje magazynu-— Menedżera pakietów][store-apps-storage-package-manager]

<span data-ttu-id="0d423-130">Użyj następującego polecenia do Menedżera pakietów punkt lokalizacji na komputerze:</span><span class="sxs-lookup"><span data-stu-id="0d423-130">Use the following command to point Package Manager to the location on your machine:</span></span>

    Install-Package Microsoft.Data.OData.WindowsStore -Source "C:\Program Files (x86)\Microsoft WCF Data Services\5.0\bin\NuGet"

<span data-ttu-id="0d423-131">To polecenie spowoduje automatyczne dodanie wszystkich wymaganych odwołań do projektu.</span><span class="sxs-lookup"><span data-stu-id="0d423-131">This command will automatically add all required references to your project.</span></span> <span data-ttu-id="0d423-132">Jeśli nie chcesz używać konsoli Menedżera pakietów, można dodać folderu NuGet usługi danych WCF na komputerze lokalnym, do listy źródeł pakietów i następnie dodać odwołanie za pośrednictwem interfejsu użytkownika, zgodnie z opisem w [Zarządzanie NuGet pakietów przy użyciu okna dialogowego ](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog).</span><span class="sxs-lookup"><span data-stu-id="0d423-132">If you do not want to use the Package Manager Console, you can add the WCF Data Services NuGet folder on your local machine to the list of package sources and then add the reference through the UI, as described in [Managing NuGet Packages Using the Dialog](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog).</span></span>

<span data-ttu-id="0d423-133">Gdy ma odwołanie do pakietu NuGet usługi danych WCF, Zmień kod w Twojej przycisk **kliknij** zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="0d423-133">When you have referenced the WCF Data Services NuGet package, change the code in your button's **Click** event:</span></span>

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var tableClient = account.CreateCloudTableClient();
var table = tableClient.GetTableReference("table1");
await table.CreateIfNotExistsAsync();
```

<span data-ttu-id="0d423-134">Ten kod sprawdza, czy tabela o nazwie *table1* istnieje na koncie, a następnie tworzy, jeśli nie.</span><span class="sxs-lookup"><span data-stu-id="0d423-134">This code checks whether a table named *table1* exists in your account, and then creates it if not.</span></span>

<span data-ttu-id="0d423-135">Można również dodać odwołanie do Microsoft.WindowsAzure.Storage.Table.dll, który jest dostępny w tym samym pakiecie, który został pobrany.</span><span class="sxs-lookup"><span data-stu-id="0d423-135">You can also add a reference to Microsoft.WindowsAzure.Storage.Table.dll, which is available in the same package that you downloaded.</span></span> <span data-ttu-id="0d423-136">Ta biblioteka zawiera dodatkowe funkcje, takie jak oparty na odbiciu serializacji i rodzajowy zapytania.</span><span class="sxs-lookup"><span data-stu-id="0d423-136">This library contains additional functionality, such as reflection-based serialization and generic queries.</span></span> <span data-ttu-id="0d423-137">Należy pamiętać, że ta biblioteka nie obsługuje języka JavaScript.</span><span class="sxs-lookup"><span data-stu-id="0d423-137">Note that this library does not support JavaScript.</span></span>

[store-apps-storage-vs-project]: ./media/storage-use-store-apps/store-apps-storage-vs-project.png
[store-apps-storage-choose-library]: ./media/storage-use-store-apps/store-apps-storage-choose-library.png
[store-apps-storage-package-manager]: ./media/storage-use-store-apps/store-apps-storage-package-manager.png
