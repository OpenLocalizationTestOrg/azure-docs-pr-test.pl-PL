---
title: "Rozpoczynanie pracy z magazynu tabel platformy Azure i programu Visual Studio połączone usługi (ASP.NET) | Dokumentacja firmy Microsoft"
description: "Jak rozpocząć korzystanie z magazynu tabel platformy Azure w projekcie platformy ASP.NET w programie Visual Studio po połączeniu z kontem magazynu przy użyciu programu Visual Studio usług połączonych"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: af81a326-18f4-4449-bc0d-e96fba27c1f8
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: tarcher
ms.openlocfilehash: d9cb32483d3f582bbeb0ccc6a204a8b6d9ea5c96
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-azure-table-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="a564b-103">Rozpoczynanie pracy z magazynu tabel platformy Azure i programu Visual Studio połączone usługi (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="a564b-103">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="a564b-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="a564b-104">Overview</span></span>

<span data-ttu-id="a564b-105">Magazyn tabel Azure umożliwia przechowywanie dużych ilości danych strukturalnych.</span><span class="sxs-lookup"><span data-stu-id="a564b-105">Azure Table storage enables you to store large amounts of structured data.</span></span> <span data-ttu-id="a564b-106">Usługa jest magazynem danych NoSQL, który przyjmuje uwierzytelnione wywołania z wewnątrz lub na zewnątrz w chmurze Azure.</span><span class="sxs-lookup"><span data-stu-id="a564b-106">The service is a NoSQL datastore that accepts authenticated calls from inside and outside the Azure cloud.</span></span> <span data-ttu-id="a564b-107">Tabele Azure idealnie nadają się do przechowywania strukturalnych danych nierelacyjnych.</span><span class="sxs-lookup"><span data-stu-id="a564b-107">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="a564b-108">Ten samouczek pokazuje, jak napisać kod ASP.NET dla niektórych typowych scenariuszy przy użyciu jednostek magazynu tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="a564b-108">This tutorial shows how to write ASP.NET code for some common scenarios using Azure table storage entities.</span></span> <span data-ttu-id="a564b-109">Te scenariusze obejmują tworzenie tabeli i dodanie, wyszukiwanie i usuwania jednostek tabeli.</span><span class="sxs-lookup"><span data-stu-id="a564b-109">These scenarios include creating a table, and adding, querying, and deleting table entities.</span></span> 

##<a name="prerequisites"></a><span data-ttu-id="a564b-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a564b-110">Prerequisites</span></span>

* [<span data-ttu-id="a564b-111">Program Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a564b-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="a564b-112">Konto usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="a564b-112">Azure storage account</span></span>](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="a564b-113">Tworzenie kontrolera MVC</span><span class="sxs-lookup"><span data-stu-id="a564b-113">Create an MVC controller</span></span> 

1. <span data-ttu-id="a564b-114">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy **kontrolerów**i z menu kontekstowego wybierz **kontrolera -> Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="a564b-114">In the **Solution Explorer**, right-click **Controllers**, and, from the context menu, select **Add->Controller**.</span></span>

    ![Dodawanie kontrolera do aplikacji ASP.NET MVC](./media/vs-storage-aspnet-getting-started-tables/add-controller-menu.png)

1. <span data-ttu-id="a564b-116">Na **Dodawanie szkieletu** okno dialogowe, wybierz opcję **kontroler MVC 5 — pusty**i wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="a564b-116">On the **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![Określ typ kontrolera MVC](./media/vs-storage-aspnet-getting-started-tables/add-controller.png)

1. <span data-ttu-id="a564b-118">Na **Dodaj kontroler** okna dialogowego, nazwy kontrolera *TablesController*i wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="a564b-118">On the **Add Controller** dialog, name the controller *TablesController*, and select **Add**.</span></span>

    ![Nazwa kontrolera MVC](./media/vs-storage-aspnet-getting-started-tables/add-controller-name.png)

1. <span data-ttu-id="a564b-120">Dodaj następujące *przy użyciu* dyrektywy `TablesController.cs` pliku:</span><span class="sxs-lookup"><span data-stu-id="a564b-120">Add the following *using* directives to the `TablesController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Table;
    ```

### <a name="create-a-model-class"></a><span data-ttu-id="a564b-121">Utwórz klasę modelu</span><span class="sxs-lookup"><span data-stu-id="a564b-121">Create a model class</span></span>

<span data-ttu-id="a564b-122">Wiele przykładów w tym artykule użyj **TableEntity**-klasy o nazwie **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="a564b-122">Many of the examples in this article use a **TableEntity**-derived class called **CustomerEntity**.</span></span> <span data-ttu-id="a564b-123">Poniższe kroki przedstawiono deklarowanie tę klasę jako klasę modelu:</span><span class="sxs-lookup"><span data-stu-id="a564b-123">The following steps guide you through declaring this class as a model class:</span></span>

1. <span data-ttu-id="a564b-124">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy **modele**i z menu kontekstowego wybierz **klasy -> Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="a564b-124">In the **Solution Explorer**, right-click **Models**, and, from the context menu, select **Add->Class**.</span></span>

1. <span data-ttu-id="a564b-125">Na **Dodaj nowy element** okna dialogowego, nazwę klasy, **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="a564b-125">On the **Add New Item** dialog, name the class, **CustomerEntity**.</span></span>

1. <span data-ttu-id="a564b-126">Otwórz `CustomerEntity.cs` pliku i dodaj następującą **przy użyciu** dyrektywy:</span><span class="sxs-lookup"><span data-stu-id="a564b-126">Open the `CustomerEntity.cs` file, and add the following **using** directive:</span></span>

    ```csharp
    using Microsoft.WindowsAzure.Storage.Table;
    ```

1. <span data-ttu-id="a564b-127">Zmodyfikuj klasy, tak, aby po zakończeniu zadeklarowana jest klasa, zgodnie z poniższym kodem.</span><span class="sxs-lookup"><span data-stu-id="a564b-127">Modify the class so that, when finished, the class is declared as in the following code.</span></span> <span data-ttu-id="a564b-128">Klasa deklaruje klasy jednostki o nazwie **CustomerEntity** używającej imienia klienta jako klucza wiersza i nazwiska jako klucza partycji.</span><span class="sxs-lookup"><span data-stu-id="a564b-128">The class declares an entity class called **CustomerEntity** that uses the customer's first name as the row key and last name as the partition key.</span></span>

    ```csharp
    public class CustomerEntity : TableEntity
    {
        public CustomerEntity(string lastName, string firstName)
        {
            this.PartitionKey = lastName;
            this.RowKey = firstName;
        }

        public CustomerEntity() { }

        public string Email { get; set; }
    }
    ```

## <a name="create-a-table"></a><span data-ttu-id="a564b-129">Tworzenie tabeli</span><span class="sxs-lookup"><span data-stu-id="a564b-129">Create a table</span></span>

<span data-ttu-id="a564b-130">Poniższe kroki pokazano, jak utworzyć tabelę:</span><span class="sxs-lookup"><span data-stu-id="a564b-130">The following steps illustrate how to create a table:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="a564b-131">W tej sekcji założono zostały wykonane kroki w [Konfigurowanie środowiska programowania](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="a564b-131">This section assumes you have completed the steps in [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="a564b-132">Otwórz plik `TablesController.cs`.</span><span class="sxs-lookup"><span data-stu-id="a564b-132">Open the `TablesController.cs` file.</span></span>

1. <span data-ttu-id="a564b-133">Dodaj metodę o nazwie **CreateTable** zwracającą **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="a564b-133">Add a method called **CreateTable** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateTable()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="a564b-134">W ramach **CreateTable** metody get **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="a564b-134">Within the **CreateTable** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="a564b-135">Użyj następującego kodu można pobrać parametry połączenia magazynu i informacji o koncie magazynu z konfiguracji usługi platformy Azure: (zmiany  *&lt;nazwy konta magazynu >* do nazwy konta magazynu Azure uzyskujesz dostęp do.)</span><span class="sxs-lookup"><span data-stu-id="a564b-135">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="a564b-136">Pobierz **CloudTableClient** obiekt reprezentuje klienta usługi tabel.</span><span class="sxs-lookup"><span data-stu-id="a564b-136">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="a564b-137">Pobierz **CloudTable** obiekt, który reprezentuje odwołanie do nazwy żądanej tabeli.</span><span class="sxs-lookup"><span data-stu-id="a564b-137">Get a **CloudTable** object that represents a reference to the desired table name.</span></span> <span data-ttu-id="a564b-138">**CloudTableClient.GetTableReference** — metoda nie powoduje żądanie magazyn tabel.</span><span class="sxs-lookup"><span data-stu-id="a564b-138">The **CloudTableClient.GetTableReference** method does not make a request against table storage.</span></span> <span data-ttu-id="a564b-139">Czy tabela istnieje, zwracany jest odwołanie.</span><span class="sxs-lookup"><span data-stu-id="a564b-139">The reference is returned whether or not the table exists.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="a564b-140">Wywołanie **CloudTable.CreateIfNotExists** metodę w celu utworzenia tabeli, jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="a564b-140">Call the **CloudTable.CreateIfNotExists** method to create the table if it does not yet exist.</span></span> <span data-ttu-id="a564b-141">**CloudTable.CreateIfNotExists** metoda zwraca **true** Jeśli tabela nie istnieje i został utworzony pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="a564b-141">The **CloudTable.CreateIfNotExists** method returns **true** if the table does not exist, and is successfully created.</span></span> <span data-ttu-id="a564b-142">W przeciwnym razie **false** jest zwracany.</span><span class="sxs-lookup"><span data-stu-id="a564b-142">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = table.CreateIfNotExists();
    ```

1. <span data-ttu-id="a564b-143">Aktualizacja **obiekt ViewBag** z nazwą tabeli.</span><span class="sxs-lookup"><span data-stu-id="a564b-143">Update the **ViewBag** with the name of the table.</span></span>

    ```csharp
    ViewBag.TableName = table.Name;
    ```

1. <span data-ttu-id="a564b-144">W **Eksploratora rozwiązań**, rozwiń węzeł **widoków** folderu, kliknij prawym przyciskiem myszy **tabel**, a z menu kontekstowego wybierz **Dodaj -> Widok**.</span><span class="sxs-lookup"><span data-stu-id="a564b-144">In the **Solution Explorer**, expand the **Views** folder, right-click **Tables**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="a564b-145">Na **Dodaj widok** okna dialogowego, wprowadź **CreateTable** dla nazwy widoku i wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="a564b-145">On the **Add View** dialog, enter **CreateTable** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="a564b-146">Otwórz `CreateTable.cshtml`i zmodyfikuj go, aby wygląda jak poniższy fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="a564b-146">Open `CreateTable.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Table";
    }
    
    <h2>Create Table results</h2>

    Creation of @ViewBag.TableName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="a564b-147">W **Eksploratora rozwiązań**, rozwiń węzeł **Shared -> widoki** folder, a następnie otwórz `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="a564b-147">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="a564b-148">Po wykonaniu ostatniego **Html.ActionLink**, Dodaj następujący **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="a564b-148">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create table", "CreateTable", "Tables")</li>
    ```

1. <span data-ttu-id="a564b-149">Uruchom aplikację i wybierz **Utwórz tabelę** aby zobaczyć wyniki, podobnie jak na poniższym zrzucie ekranu:</span><span class="sxs-lookup"><span data-stu-id="a564b-149">Run the application, and select **Create table** to see results similar to the following screen shot:</span></span>
  
    ![Tworzenie tabeli](./media/vs-storage-aspnet-getting-started-tables/create-table-results.png)

    <span data-ttu-id="a564b-151">Jak wspomniano wcześniej, **CloudTable.CreateIfNotExists** metoda zwraca **true** tylko po tabeli nie istnieje i jest tworzona.</span><span class="sxs-lookup"><span data-stu-id="a564b-151">As mentioned previously, the **CloudTable.CreateIfNotExists** method returns **true** only when the table doesn't exist and is created.</span></span> <span data-ttu-id="a564b-152">W związku z tym po uruchomieniu aplikacji, gdy tabela istnieje, metoda zwraca **false**.</span><span class="sxs-lookup"><span data-stu-id="a564b-152">Therefore, if you run the app when the table exists, the method returns **false**.</span></span> <span data-ttu-id="a564b-153">Aby uruchomić aplikację wiele razy, możesz usunąć tabeli przed ponownym uruchomieniem aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a564b-153">To run the app multiple times, you must delete the table before running the app again.</span></span> <span data-ttu-id="a564b-154">Usunięcie tabeli może odbywać się za pośrednictwem **CloudTable.Delete** metody.</span><span class="sxs-lookup"><span data-stu-id="a564b-154">Deleting the table can be done via the **CloudTable.Delete** method.</span></span> <span data-ttu-id="a564b-155">Możesz także usunąć za pomocą tabeli [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) lub [Eksploratora usługi Microsoft Azure Storage](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="a564b-155">You can also delete the table using the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or the [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="a564b-156">Dodawanie jednostki do tabeli</span><span class="sxs-lookup"><span data-stu-id="a564b-156">Add an entity to a table</span></span>

<span data-ttu-id="a564b-157">*Jednostki* mapy w celu C\# obiektów przy użyciu niestandardowej klasy pochodzące z **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="a564b-157">*Entities* map to C\# objects by using a custom class derived from **TableEntity**.</span></span> <span data-ttu-id="a564b-158">Aby dodać jednostkę do tabeli, należy utworzyć klasę, która definiuje właściwości jednostki.</span><span class="sxs-lookup"><span data-stu-id="a564b-158">To add an entity to a table, create a class that defines the properties of your entity.</span></span> <span data-ttu-id="a564b-159">W tej sekcji pojawi się, jak zdefiniować klasę jednostki, która używa imienia klienta jako klucza wiersza i nazwiska jako klucza partycji.</span><span class="sxs-lookup"><span data-stu-id="a564b-159">In this section, you'll see how to define an entity class that uses the customer's first name as the row key and last name as the partition key.</span></span> <span data-ttu-id="a564b-160">Razem klucz partycji i klucz wiersza jednostki jednoznacznie identyfikują jednostkę w tabeli.</span><span class="sxs-lookup"><span data-stu-id="a564b-160">Together, an entity's partition and row key uniquely identify the entity in the table.</span></span> <span data-ttu-id="a564b-161">Jednostki z tym samym kluczem partycji mogą być przeszukiwane szybciej niż jednostki o różnych kluczach partycji, niemniej użycie różnych kluczy partycji umożliwia zwiększenie skalowalności operacji równoległych.</span><span class="sxs-lookup"><span data-stu-id="a564b-161">Entities with the same partition key can be queried faster than entities with different partition keys, but using diverse partition keys allows for greater scalability of parallel operations.</span></span> <span data-ttu-id="a564b-162">Dla właściwości, które mają być przechowywane w usłudze tabel właściwość musi być właściwością publiczną obsługiwanego typu, która ujawnia zarówno ustawiania i pobierania wartości.</span><span class="sxs-lookup"><span data-stu-id="a564b-162">For any property that should be stored in the table service, the property must be a public property of a supported type that exposes both setting and retrieving values.</span></span>
<span data-ttu-id="a564b-163">Klasa jednostki *musi* zadeklarować publicznego konstruktora bez parametrów.</span><span class="sxs-lookup"><span data-stu-id="a564b-163">The entity class *must* declare a public parameter-less constructor.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="a564b-164">W tej sekcji założono zostały wykonane kroki w [Konfigurowanie środowiska programowania](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="a564b-164">This section assumes you have completed the steps in [Set up the development environment](#set-up-the-development-environment).</span></span>

1. <span data-ttu-id="a564b-165">Otwórz plik `TablesController.cs`.</span><span class="sxs-lookup"><span data-stu-id="a564b-165">Open the `TablesController.cs` file.</span></span>

1. <span data-ttu-id="a564b-166">Dodaj następujące dyrektywy, aby kod w `TablesController.cs` mogą uzyskiwać dostęp do pliku **CustomerEntity** klasy:</span><span class="sxs-lookup"><span data-stu-id="a564b-166">Add the following directive so that the code in the `TablesController.cs` file can access the **CustomerEntity** class:</span></span>

    ```csharp
    using StorageAspnet.Models;
    ```

1. <span data-ttu-id="a564b-167">Dodaj metodę o nazwie **AddEntity** zwracającą **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="a564b-167">Add a method called **AddEntity** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddEntity()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="a564b-168">W ramach **AddEntity** metody get **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="a564b-168">Within the **AddEntity** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="a564b-169">Użyj następującego kodu można pobrać parametry połączenia magazynu i informacji o koncie magazynu z konfiguracji usługi platformy Azure: (zmiany  *&lt;nazwy konta magazynu >* do nazwy konta magazynu Azure uzyskujesz dostęp do.)</span><span class="sxs-lookup"><span data-stu-id="a564b-169">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="a564b-170">Pobierz **CloudTableClient** obiekt reprezentuje klienta usługi tabel.</span><span class="sxs-lookup"><span data-stu-id="a564b-170">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="a564b-171">Pobierz **CloudTable** obiekt, który reprezentuje odwołanie do tabeli, do której zamierzasz dodać nową jednostkę.</span><span class="sxs-lookup"><span data-stu-id="a564b-171">Get a **CloudTable** object that represents a reference to the table to which you are going to add the new entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="a564b-172">Utwórz wystąpienie i zainicjować **CustomerEntity** klasy.</span><span class="sxs-lookup"><span data-stu-id="a564b-172">Instantiate and initialize the **CustomerEntity** class.</span></span>

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    ```

1. <span data-ttu-id="a564b-173">Utwórz **TableOperation** obiekt, który wstawia jednostki klienta.</span><span class="sxs-lookup"><span data-stu-id="a564b-173">Create a **TableOperation** object that inserts the customer entity.</span></span>

    ```csharp
    TableOperation insertOperation = TableOperation.Insert(customer1);
    ```

1. <span data-ttu-id="a564b-174">Wykonywanie operacji insert, wywołując **CloudTable.Execute** metody.</span><span class="sxs-lookup"><span data-stu-id="a564b-174">Execute the insert operation by calling the **CloudTable.Execute** method.</span></span> <span data-ttu-id="a564b-175">Sprawdź wynik operacji, sprawdzając **TableResult.HttpStatusCode** właściwości.</span><span class="sxs-lookup"><span data-stu-id="a564b-175">You can verify the result of the operation by inspecting the **TableResult.HttpStatusCode** property.</span></span> <span data-ttu-id="a564b-176">Kod stanu 2xx wskazuje, że akcja żądanego przez klienta zostało przetworzone pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="a564b-176">A status code of 2xx indicates the action requested by the client was processed successfully.</span></span> <span data-ttu-id="a564b-177">Na przykład pomyślnie wstawienia nowych jednostek skutkuje kod stanu HTTP 204, co oznacza, że operacja została pomyślnie przetworzył i serwer nie zwrócił żadnej zawartości.</span><span class="sxs-lookup"><span data-stu-id="a564b-177">For example, successful insertions of new entities results in an HTTP status code of 204, meaning that the operation was successfully processed and the server did not return any content.</span></span>

    ```csharp
    TableResult result = table.Execute(insertOperation);
    ```

1. <span data-ttu-id="a564b-178">Aktualizacja **obiekt ViewBag** z nazwą tabeli i wyniki operacji insert.</span><span class="sxs-lookup"><span data-stu-id="a564b-178">Update the **ViewBag** with the table name, and the results of the insert operation.</span></span>

    ```csharp
    ViewBag.TableName = table.Name;
    ViewBag.Result = result.HttpStatusCode;
    ```

1. <span data-ttu-id="a564b-179">W **Eksploratora rozwiązań**, rozwiń węzeł **widoków** folderu, kliknij prawym przyciskiem myszy **tabel**, a z menu kontekstowego wybierz **Dodaj -> Widok**.</span><span class="sxs-lookup"><span data-stu-id="a564b-179">In the **Solution Explorer**, expand the **Views** folder, right-click **Tables**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="a564b-180">Na **Dodaj widok** okna dialogowego, wprowadź **AddEntity** dla nazwy widoku i wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="a564b-180">On the **Add View** dialog, enter **AddEntity** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="a564b-181">Otwórz `AddEntity.cshtml`i zmodyfikuj go, aby wygląda jak poniższy fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="a564b-181">Open `AddEntity.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Add entity";
    }
    
    <h2>Add entity results</h2>

    Insert of entity into @ViewBag.TableName @(ViewBag.Result == 204 ? "succeeded" : "failed")
    ```
1. <span data-ttu-id="a564b-182">W **Eksploratora rozwiązań**, rozwiń węzeł **Shared -> widoki** folder, a następnie otwórz `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="a564b-182">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="a564b-183">Po wykonaniu ostatniego **Html.ActionLink**, Dodaj następujący **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="a564b-183">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add entity", "AddEntity", "Tables")</li>
    ```

1. <span data-ttu-id="a564b-184">Uruchom aplikację i wybierz **dodania jednostki** aby zobaczyć wyniki, podobnie jak na poniższym zrzucie ekranu:</span><span class="sxs-lookup"><span data-stu-id="a564b-184">Run the application, and select **Add entity** to see results similar to the following screen shot:</span></span>
  
    ![Dodawanie jednostki](./media/vs-storage-aspnet-getting-started-tables/add-entity-results.png)

    <span data-ttu-id="a564b-186">Możesz sprawdzić, czy obiekt został dodany, wykonując kroki opisane w sekcji [pobrać pojedynczą jednostką](#get-a-single-entity).</span><span class="sxs-lookup"><span data-stu-id="a564b-186">You can verify that the entity was added by following the steps in the section, [Get a single entity](#get-a-single-entity).</span></span> <span data-ttu-id="a564b-187">Można również użyć [Eksploratora usługi Microsoft Azure Storage](../vs-azure-tools-storage-manage-with-storage-explorer.md) do wyświetlania wszystkich jednostek tabel.</span><span class="sxs-lookup"><span data-stu-id="a564b-187">You can also use the [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) to view all the entities for your tables.</span></span>

## <a name="add-a-batch-of-entities-to-a-table"></a><span data-ttu-id="a564b-188">Dodawanie partię jednostek do tabeli</span><span class="sxs-lookup"><span data-stu-id="a564b-188">Add a batch of entities to a table</span></span>

<span data-ttu-id="a564b-189">Oprócz możliwości [dodać jednostkę do jednej tabeli w czasie](#add-an-entity-to-a-table), możesz także dodać jednostek w partii.</span><span class="sxs-lookup"><span data-stu-id="a564b-189">In addition to being able to [add an entity to a table one at a time](#add-an-entity-to-a-table), you can also add entities in batch.</span></span> <span data-ttu-id="a564b-190">Dodawanie jednostek w partii zmniejsza liczbę przechodzenia między kodu i usługa tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="a564b-190">Adding entities in batch reduces the number of round-trips between your code and the Azure table service.</span></span> <span data-ttu-id="a564b-191">Następujące kroki przedstawiono sposób dodawania wielu jednostek do tabeli za pomocą jednej operacji wstawiania:</span><span class="sxs-lookup"><span data-stu-id="a564b-191">The following steps illustrate how to add multiple entities to a table with a single insert operation:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="a564b-192">W tej sekcji założono zostały wykonane kroki w [Konfigurowanie środowiska programowania](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="a564b-192">This section assumes you have completed the steps in [Set up the development environment](#set-up-the-development-environment).</span></span>

1. <span data-ttu-id="a564b-193">Otwórz plik `TablesController.cs`.</span><span class="sxs-lookup"><span data-stu-id="a564b-193">Open the `TablesController.cs` file.</span></span>

1. <span data-ttu-id="a564b-194">Dodaj metodę o nazwie **AddEntities** zwracającą **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="a564b-194">Add a method called **AddEntities** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddEntities()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="a564b-195">W ramach **AddEntities** metody get **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="a564b-195">Within the **AddEntities** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="a564b-196">Użyj następującego kodu można pobrać parametry połączenia magazynu i informacji o koncie magazynu z konfiguracji usługi platformy Azure: (zmiany  *&lt;nazwy konta magazynu >* do nazwy konta magazynu Azure uzyskujesz dostęp do.)</span><span class="sxs-lookup"><span data-stu-id="a564b-196">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="a564b-197">Pobierz **CloudTableClient** obiekt reprezentuje klienta usługi tabel.</span><span class="sxs-lookup"><span data-stu-id="a564b-197">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="a564b-198">Pobierz **CloudTable** obiekt, który reprezentuje odwołanie do tabeli, do której zamierzasz dodać nowe jednostki.</span><span class="sxs-lookup"><span data-stu-id="a564b-198">Get a **CloudTable** object that represents a reference to the table to which you are going to add the new entities.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="a564b-199">Utworzenie wystąpienia niektórych obiektów klienta na podstawie **CustomerEntity** klasa przedstawione w sekcji modelu [dodać jednostkę do tabeli](#add-an-entity-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="a564b-199">Instantiate some customer objects based on the **CustomerEntity** model class presented in the section, [Add an entity to a table](#add-an-entity-to-a-table).</span></span>

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
    customer1.Email = "Jeff@contoso.com";

    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.Email = "Ben@contoso.com";
    ```

1. <span data-ttu-id="a564b-200">Pobierz **TableBatchOperation** obiektu.</span><span class="sxs-lookup"><span data-stu-id="a564b-200">Get a **TableBatchOperation** object.</span></span>

    ```csharp
    TableBatchOperation batchOperation = new TableBatchOperation();
    ```

1. <span data-ttu-id="a564b-201">Dodaj jednostki do obiektu operacji wstawiania wsadowego.</span><span class="sxs-lookup"><span data-stu-id="a564b-201">Add entities to the batch insert operation object.</span></span>

    ```csharp
    batchOperation.Insert(customer1);
    batchOperation.Insert(customer2);
    ```

1. <span data-ttu-id="a564b-202">Wykonanie operacji wstawiania wsadowego przez wywołanie metody **CloudTable.ExecuteBatch** metody.</span><span class="sxs-lookup"><span data-stu-id="a564b-202">Execute the batch insert operation by calling the **CloudTable.ExecuteBatch** method.</span></span>   

    ```csharp
    IList<TableResult> results = table.ExecuteBatch(batchOperation);
    ```

1. <span data-ttu-id="a564b-203">**CloudTable.ExecuteBatch** metoda zwraca listę **TableResult** obiektów gdzie każdy **TableResult** obiektu można zbadać do ustalenia powodzenia lub niepowodzenia poszczególnych działań.</span><span class="sxs-lookup"><span data-stu-id="a564b-203">The **CloudTable.ExecuteBatch** method returns a list of **TableResult** objects where each **TableResult** object can be examined to determine the success or failure of each individual operation.</span></span> <span data-ttu-id="a564b-204">Na przykład przekazania do widoku listy i pozwól widoku wyświetlane wyniki każdego działania.</span><span class="sxs-lookup"><span data-stu-id="a564b-204">For this example, pass the list to a view and let the view display the results of each operation.</span></span> 
 
    ```csharp
    return View(results);
    ```

1. <span data-ttu-id="a564b-205">W **Eksploratora rozwiązań**, rozwiń węzeł **widoków** folderu, kliknij prawym przyciskiem myszy **tabel**, a z menu kontekstowego wybierz **Dodaj -> Widok**.</span><span class="sxs-lookup"><span data-stu-id="a564b-205">In the **Solution Explorer**, expand the **Views** folder, right-click **Tables**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="a564b-206">Na **Dodaj widok** okna dialogowego, wprowadź **AddEntities** dla nazwy widoku i wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="a564b-206">On the **Add View** dialog, enter **AddEntities** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="a564b-207">Otwórz `AddEntities.cshtml`i zmodyfikuj go, aby wygląda podobnie do poniższego.</span><span class="sxs-lookup"><span data-stu-id="a564b-207">Open `AddEntities.cshtml`, and modify it so that it looks like the following.</span></span>

    ```csharp
    @model IEnumerable<Microsoft.WindowsAzure.Storage.Table.TableResult>
    @{
        ViewBag.Title = "AddEntities";
    }
    
    <h2>Add-entities results</h2>
    
    <table border="1">
        <tr>
            <th>First name</th>
            <th>Last name</th>
            <th>HTTP result</th>
        </tr>
        @foreach (var result in Model)
        {
        <tr>
            <td>@((result.Result as StorageAspnet.Models.CustomerEntity).RowKey)</td>
            <td>@((result.Result as StorageAspnet.Models.CustomerEntity).PartitionKey)</td>
            <td>@result.HttpStatusCode</td>
        </tr>
        }
    </table>
    ```

1. <span data-ttu-id="a564b-208">W **Eksploratora rozwiązań**, rozwiń węzeł **Shared -> widoki** folder, a następnie otwórz `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="a564b-208">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="a564b-209">Po wykonaniu ostatniego **Html.ActionLink**, Dodaj następujący **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="a564b-209">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add entities", "AddEntities", "Tables")</li>
    ```

1. <span data-ttu-id="a564b-210">Uruchom aplikację i wybierz **Dodaj jednostki** aby zobaczyć wyniki, podobnie jak na poniższym zrzucie ekranu:</span><span class="sxs-lookup"><span data-stu-id="a564b-210">Run the application, and select **Add entities** to see results similar to the following screen shot:</span></span>
  
    ![Dodawanie jednostek](./media/vs-storage-aspnet-getting-started-tables/add-entities-results.png)

    <span data-ttu-id="a564b-212">Możesz sprawdzić, czy obiekt został dodany, wykonując kroki opisane w sekcji [pobrać pojedynczą jednostką](#get-a-single-entity).</span><span class="sxs-lookup"><span data-stu-id="a564b-212">You can verify that the entity was added by following the steps in the section, [Get a single entity](#get-a-single-entity).</span></span> <span data-ttu-id="a564b-213">Można również użyć [Eksploratora usługi Microsoft Azure Storage](../vs-azure-tools-storage-manage-with-storage-explorer.md) do wyświetlania wszystkich jednostek tabel.</span><span class="sxs-lookup"><span data-stu-id="a564b-213">You can also use the [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) to view all the entities for your tables.</span></span>

## <a name="get-a-single-entity"></a><span data-ttu-id="a564b-214">Pobierz pojedynczy element</span><span class="sxs-lookup"><span data-stu-id="a564b-214">Get a single entity</span></span>

<span data-ttu-id="a564b-215">W tej części przedstawiono sposób pobierania pojedyncza jednostka z tabeli za pomocą klucz wiersza jednostki i klucz partycji.</span><span class="sxs-lookup"><span data-stu-id="a564b-215">This section illustrates how to get a single entity from a table using the entity's row key and partition key.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="a564b-216">W tej sekcji założono zostały wykonane kroki w [Konfigurowanie środowiska programowania](#set-up-the-development-environment)i korzysta z danych [dodać partię jednostek do tabeli](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="a564b-216">This section assumes you have completed the steps in [Set up the development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities to a table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="a564b-217">Otwórz plik `TablesController.cs`.</span><span class="sxs-lookup"><span data-stu-id="a564b-217">Open the `TablesController.cs` file.</span></span>

1. <span data-ttu-id="a564b-218">Dodaj metodę o nazwie **GetSingle** zwracającą **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="a564b-218">Add a method called **GetSingle** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetSingle()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="a564b-219">W ramach **GetSingle** metody get **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="a564b-219">Within the **GetSingle** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="a564b-220">Użyj następującego kodu można pobrać parametry połączenia magazynu i informacji o koncie magazynu z konfiguracji usługi platformy Azure: (zmiany  *&lt;nazwy konta magazynu >* do nazwy konta magazynu Azure uzyskujesz dostęp do.)</span><span class="sxs-lookup"><span data-stu-id="a564b-220">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="a564b-221">Pobierz **CloudTableClient** obiekt reprezentuje klienta usługi tabel.</span><span class="sxs-lookup"><span data-stu-id="a564b-221">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="a564b-222">Pobierz **CloudTable** obiekt, który reprezentuje odwołanie do tabeli, z którego są pobierane jednostki.</span><span class="sxs-lookup"><span data-stu-id="a564b-222">Get a **CloudTable** object that represents a reference to the table from which you are retrieving the entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="a564b-223">Utwórz obiekt operacji pobierania, który przyjmuje do obiektu jednostki pochodne **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="a564b-223">Create a retrieve operation object that takes an entity object derived from **TableEntity**.</span></span> <span data-ttu-id="a564b-224">Pierwszym parametrem jest *partitionKey*, a drugi parametr jest *rowKey*.</span><span class="sxs-lookup"><span data-stu-id="a564b-224">The first parameter is the *partitionKey*, and the second parameter is the *rowKey*.</span></span> <span data-ttu-id="a564b-225">Przy użyciu **CustomerEntity** klasy i dane podane w sekcji [dodać partię jednostek do tabeli](#add-a-batch-of-entities-to-a-table), poniższy fragment kodu wysyła zapytanie do tabeli dla **CustomerEntity**jednostki o *partitionKey* wartość "Smith" i *rowKey* wartość "Ben":</span><span class="sxs-lookup"><span data-stu-id="a564b-225">Using the **CustomerEntity** class and data presented in the section [Add a batch of entities to a table](#add-a-batch-of-entities-to-a-table), the following code snippet queries the table for a **CustomerEntity** entity with a *partitionKey* value of "Smith" and a *rowKey* value of "Ben":</span></span>

    ```csharp
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");
    ```

1. <span data-ttu-id="a564b-226">Wykonanie operacji pobierania.</span><span class="sxs-lookup"><span data-stu-id="a564b-226">Execute the retrieve operation.</span></span>   

    ```csharp
    TableResult result = table.Execute(retrieveOperation);
    ```

1. <span data-ttu-id="a564b-227">Przekazać wynik do widoku do wyświetlenia.</span><span class="sxs-lookup"><span data-stu-id="a564b-227">Pass the result to the view for display.</span></span>

    ```csharp
    return View(result);
    ```

1. <span data-ttu-id="a564b-228">W **Eksploratora rozwiązań**, rozwiń węzeł **widoków** folderu, kliknij prawym przyciskiem myszy **tabel**, a z menu kontekstowego wybierz **Dodaj -> Widok**.</span><span class="sxs-lookup"><span data-stu-id="a564b-228">In the **Solution Explorer**, expand the **Views** folder, right-click **Tables**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="a564b-229">Na **Dodaj widok** okna dialogowego, wprowadź **GetSingle** dla nazwy widoku i wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="a564b-229">On the **Add View** dialog, enter **GetSingle** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="a564b-230">Otwórz `GetSingle.cshtml`i zmodyfikuj go, aby wygląda jak poniższy fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="a564b-230">Open `GetSingle.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @model Microsoft.WindowsAzure.Storage.Table.TableResult
    @{
        ViewBag.Title = "GetSingle";
    }
    
    <h2>Get Single results</h2>
    
    <table border="1">
        <tr>
            <th>HTTP result</th>
            <th>First name</th>
            <th>Last name</th>
            <th>Email</th>
        </tr>
        <tr>
            <td>@Model.HttpStatusCode</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).RowKey)</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).PartitionKey)</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).Email)</td>
        </tr>
    </table>
    ```

1. <span data-ttu-id="a564b-231">W **Eksploratora rozwiązań**, rozwiń węzeł **Shared -> widoki** folder, a następnie otwórz `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="a564b-231">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="a564b-232">Po wykonaniu ostatniego **Html.ActionLink**, Dodaj następujący **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="a564b-232">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get single", "GetSingle", "Tables")</li>
    ```

1. <span data-ttu-id="a564b-233">Uruchom aplikację i wybierz **Pobierz pojedynczy** aby zobaczyć wyniki, podobnie jak na poniższym zrzucie ekranu:</span><span class="sxs-lookup"><span data-stu-id="a564b-233">Run the application, and select **Get Single** to see results similar to the following screen shot:</span></span>
  
    ![Pobierz pojedynczy](./media/vs-storage-aspnet-getting-started-tables/get-single-results.png)

## <a name="get-all-entities-in-a-partition"></a><span data-ttu-id="a564b-235">Pobieranie wszystkich jednostek w partycji</span><span class="sxs-lookup"><span data-stu-id="a564b-235">Get all entities in a partition</span></span>

<span data-ttu-id="a564b-236">Jak wspomniano w sekcji [dodać jednostkę do tabeli](#add-an-entity-to-a-table), partycji i klucz wiersza jednoznacznie identyfikują jednostkę w tabeli.</span><span class="sxs-lookup"><span data-stu-id="a564b-236">As mentioned in the section, [Add an entity to a table](#add-an-entity-to-a-table), the combination of a partition and a row key uniquely identify an entity in a table.</span></span> <span data-ttu-id="a564b-237">Jednostki z tym samym kluczem partycji mogą być przeszukiwane szybciej niż jednostki o różnych kluczach partycji.</span><span class="sxs-lookup"><span data-stu-id="a564b-237">Entities with the same partition key can be queried faster than entities with different partition keys.</span></span> <span data-ttu-id="a564b-238">W tej części przedstawiono sposób tworzenia zapytań tabeli dla wszystkich obiektów z określonej partycji.</span><span class="sxs-lookup"><span data-stu-id="a564b-238">This section illustrates how to query a table for all the entities from a specified partition.</span></span>  

> [!NOTE]
> 
> <span data-ttu-id="a564b-239">W tej sekcji założono zostały wykonane kroki w [Konfigurowanie środowiska programowania](#set-up-the-development-environment)i korzysta z danych [dodać partię jednostek do tabeli](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="a564b-239">This section assumes you have completed the steps in [Set up the development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities to a table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="a564b-240">Otwórz plik `TablesController.cs`.</span><span class="sxs-lookup"><span data-stu-id="a564b-240">Open the `TablesController.cs` file.</span></span>

1. <span data-ttu-id="a564b-241">Dodaj metodę o nazwie **GetPartition** zwracającą **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="a564b-241">Add a method called **GetPartition** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetPartition()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="a564b-242">W ramach **GetPartition** metody get **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="a564b-242">Within the **GetPartition** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="a564b-243">Użyj następującego kodu można pobrać parametry połączenia magazynu i informacji o koncie magazynu z konfiguracji usługi platformy Azure: (zmiany  *&lt;nazwy konta magazynu >* do nazwy konta magazynu Azure uzyskujesz dostęp do.)</span><span class="sxs-lookup"><span data-stu-id="a564b-243">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="a564b-244">Pobierz **CloudTableClient** obiekt reprezentuje klienta usługi tabel.</span><span class="sxs-lookup"><span data-stu-id="a564b-244">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="a564b-245">Pobierz **CloudTable** obiekt, który reprezentuje odwołanie do tabeli, z którego są pobierane jednostek.</span><span class="sxs-lookup"><span data-stu-id="a564b-245">Get a **CloudTable** object that represents a reference to the table from which you are retrieving the entities.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="a564b-246">Utwórz wystąpienie **TableQuery** obiekt określający zapytanie w **gdzie** klauzuli.</span><span class="sxs-lookup"><span data-stu-id="a564b-246">Instantiate a **TableQuery** object specifying the query in the **Where** clause.</span></span> <span data-ttu-id="a564b-247">Przy użyciu **CustomerEntity** klasy i dane podane w sekcji [dodać partię jednostek do tabeli](#add-a-batch-of-entities-to-a-table), poniższy fragment kodu wysyła zapytanie do tabeli dla wszystkich jednostek gdzie  **PartitionKey** (nazwiska) ma wartość "Smith":</span><span class="sxs-lookup"><span data-stu-id="a564b-247">Using the **CustomerEntity** class and data presented in the section [Add a batch of entities to a table](#add-a-batch-of-entities-to-a-table), the following code snippet queries the table for a all entities where the **PartitionKey** (customer's last name) has a value of "Smith":</span></span>

    ```csharp
    TableQuery<CustomerEntity> query = 
        new TableQuery<CustomerEntity>()
        .Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));
    ```

1. <span data-ttu-id="a564b-248">W pętli, wywołaj **CloudTable.ExecuteQuerySegmented** metody przekazanie obiektu zapytanie utworzone w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="a564b-248">Within a loop, call the **CloudTable.ExecuteQuerySegmented** method passing the query object you instantiated in the previous step.</span></span>  <span data-ttu-id="a564b-249">**CloudTable.ExecuteQuerySegmented** metoda zwraca **TableContinuationToken** obiekt, który — podczas **null** — wskazuje, że nie ma żadnych kolejnych jednostek do pobrania.</span><span class="sxs-lookup"><span data-stu-id="a564b-249">The **CloudTable.ExecuteQuerySegmented** method returns a **TableContinuationToken** object that - when **null** - indicates that there are no more entities to retrieve.</span></span> <span data-ttu-id="a564b-250">W pętli Użyj innego pętli w celu wykonania iteracji zwrócone jednostki.</span><span class="sxs-lookup"><span data-stu-id="a564b-250">Within the loop, use another loop to iterate over the returned entities.</span></span> <span data-ttu-id="a564b-251">W poniższym przykładzie kodu każdy zwrócony obiekt zostanie dodany do listy.</span><span class="sxs-lookup"><span data-stu-id="a564b-251">In the following code example, each returned entity is added to a list.</span></span> <span data-ttu-id="a564b-252">Po zakończenia pętli, listy jest przekazywany do widoku do wyświetlenia:</span><span class="sxs-lookup"><span data-stu-id="a564b-252">Once the loop ends, the list is passed to a view for display:</span></span> 

    ```csharp
    List<CustomerEntity> customers = new List<CustomerEntity>();
    TableContinuationToken token = null;
    do
    {
        TableQuerySegment<CustomerEntity> resultSegment = table.ExecuteQuerySegmented(query, token);
        token = resultSegment.ContinuationToken;

        foreach (CustomerEntity customer in resultSegment.Results)
        {
            customers.Add(customer);
        }
    } while (token != null);

    return View(customers);
    ```

1. <span data-ttu-id="a564b-253">W **Eksploratora rozwiązań**, rozwiń węzeł **widoków** folderu, kliknij prawym przyciskiem myszy **tabel**, a z menu kontekstowego wybierz **Dodaj -> Widok**.</span><span class="sxs-lookup"><span data-stu-id="a564b-253">In the **Solution Explorer**, expand the **Views** folder, right-click **Tables**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="a564b-254">Na **Dodaj widok** okna dialogowego, wprowadź **GetPartition** dla nazwy widoku i wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="a564b-254">On the **Add View** dialog, enter **GetPartition** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="a564b-255">Otwórz `GetPartition.cshtml`i zmodyfikuj go, aby wygląda jak poniższy fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="a564b-255">Open `GetPartition.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @model IEnumerable<StorageAspnet.Models.CustomerEntity>
    @{
        ViewBag.Title = "GetPartition";
    }
    
    <h2>Get Partition results</h2>
    
    <table border="1">
        <tr>
            <th>First name</th>
            <th>Last name</th>
            <th>Email</th>
        </tr>
        @foreach (var customer in Model)
        {
        <tr>
            <td>@(customer.RowKey)</td>
            <td>@(customer.PartitionKey)</td>
            <td>@(customer.Email)</td>
        </tr>
        }
    </table>
    ```

1. <span data-ttu-id="a564b-256">W **Eksploratora rozwiązań**, rozwiń węzeł **Shared -> widoki** folder, a następnie otwórz `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="a564b-256">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="a564b-257">Po wykonaniu ostatniego **Html.ActionLink**, Dodaj następujący **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="a564b-257">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get partition", "GetPartition", "Tables")</li>
    ```

1. <span data-ttu-id="a564b-258">Uruchom aplikację i wybierz **pobrać partycji** aby zobaczyć wyniki, podobnie jak na poniższym zrzucie ekranu:</span><span class="sxs-lookup"><span data-stu-id="a564b-258">Run the application, and select **Get Partition** to see results similar to the following screen shot:</span></span>
  
    ![Pobierz partycji](./media/vs-storage-aspnet-getting-started-tables/get-partition-results.png)

## <a name="delete-an-entity"></a><span data-ttu-id="a564b-260">Usuwanie jednostki</span><span class="sxs-lookup"><span data-stu-id="a564b-260">Delete an entity</span></span>

<span data-ttu-id="a564b-261">W tej części przedstawiono sposób usuwania jednostek z tabeli.</span><span class="sxs-lookup"><span data-stu-id="a564b-261">This section illustrates how to delete an entity from a table.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="a564b-262">W tej sekcji założono zostały wykonane kroki w [Konfigurowanie środowiska programowania](#set-up-the-development-environment)i korzysta z danych [dodać partię jednostek do tabeli](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="a564b-262">This section assumes you have completed the steps in [Set up the development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities to a table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="a564b-263">Otwórz plik `TablesController.cs`.</span><span class="sxs-lookup"><span data-stu-id="a564b-263">Open the `TablesController.cs` file.</span></span>

1. <span data-ttu-id="a564b-264">Dodaj metodę o nazwie **DeleteEntity** zwracającą **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="a564b-264">Add a method called **DeleteEntity** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult DeleteEntity()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="a564b-265">W ramach **DeleteEntity** metody get **CloudStorageAccount** obiekt, który reprezentuje informacje o koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="a564b-265">Within the **DeleteEntity** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="a564b-266">Użyj następującego kodu można pobrać parametry połączenia magazynu i informacji o koncie magazynu z konfiguracji usługi platformy Azure: (zmiany  *&lt;nazwy konta magazynu >* do nazwy konta magazynu Azure uzyskujesz dostęp do.)</span><span class="sxs-lookup"><span data-stu-id="a564b-266">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="a564b-267">Pobierz **CloudTableClient** obiekt reprezentuje klienta usługi tabel.</span><span class="sxs-lookup"><span data-stu-id="a564b-267">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="a564b-268">Pobierz **CloudTable** obiekt, który reprezentuje odwołanie do tabeli, z której po usunięciu jednostki.</span><span class="sxs-lookup"><span data-stu-id="a564b-268">Get a **CloudTable** object that represents a reference to the table from which you are deleting the entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="a564b-269">Utwórz obiekt operacji delete, który przyjmuje do obiektu jednostki pochodne **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="a564b-269">Create a delete operation object that takes an entity object derived from **TableEntity**.</span></span> <span data-ttu-id="a564b-270">W takim przypadku stosujemy **CustomerEntity** klasy i dane podane w sekcji [dodać partię jednostek do tabeli](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="a564b-270">In this case, we use the **CustomerEntity** class and data presented in the section [Add a batch of entities to a table](#add-a-batch-of-entities-to-a-table).</span></span> <span data-ttu-id="a564b-271">Jednostki **ETag** musi mieć ustawioną prawidłową wartość.</span><span class="sxs-lookup"><span data-stu-id="a564b-271">The entity's **ETag** must be set to a valid value.</span></span>  

    ```csharp
    TableOperation deleteOperation = 
        TableOperation.Delete(new CustomerEntity("Smith", "Ben") { ETag = "*" } );
    ```

1. <span data-ttu-id="a564b-272">Wykonanie operacji usuwania.</span><span class="sxs-lookup"><span data-stu-id="a564b-272">Execute the delete operation.</span></span>   

    ```csharp
    TableResult result = table.Execute(deleteOperation);
    ```

1. <span data-ttu-id="a564b-273">Przekazać wynik do widoku do wyświetlenia.</span><span class="sxs-lookup"><span data-stu-id="a564b-273">Pass the result to the view for display.</span></span>

    ```csharp
    return View(result);
    ```

1. <span data-ttu-id="a564b-274">W **Eksploratora rozwiązań**, rozwiń węzeł **widoków** folderu, kliknij prawym przyciskiem myszy **tabel**, a z menu kontekstowego wybierz **Dodaj -> Widok**.</span><span class="sxs-lookup"><span data-stu-id="a564b-274">In the **Solution Explorer**, expand the **Views** folder, right-click **Tables**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="a564b-275">Na **Dodaj widok** okna dialogowego, wprowadź **DeleteEntity** dla nazwy widoku i wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="a564b-275">On the **Add View** dialog, enter **DeleteEntity** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="a564b-276">Otwórz `DeleteEntity.cshtml`i zmodyfikuj go, aby wygląda jak poniższy fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="a564b-276">Open `DeleteEntity.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @model Microsoft.WindowsAzure.Storage.Table.TableResult
    @{
        ViewBag.Title = "DeleteEntity";
    }
    
    <h2>Delete Entity results</h2>
    
    <table border="1">
        <tr>
            <th>First name</th>
            <th>Last name</th>
            <th>HTTP result</th>
        </tr>
        <tr>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).RowKey)</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).PartitionKey)</td>
            <td>@Model.HttpStatusCode</td>
        </tr>
    </table>

    ```

1. <span data-ttu-id="a564b-277">W **Eksploratora rozwiązań**, rozwiń węzeł **Shared -> widoki** folder, a następnie otwórz `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="a564b-277">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="a564b-278">Po wykonaniu ostatniego **Html.ActionLink**, Dodaj następujący **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="a564b-278">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete entity", "DeleteEntity", "Tables")</li>
    ```

1. <span data-ttu-id="a564b-279">Uruchom aplikację i wybierz **usuwanie jednostek** aby zobaczyć wyniki, podobnie jak na poniższym zrzucie ekranu:</span><span class="sxs-lookup"><span data-stu-id="a564b-279">Run the application, and select **Delete entity** to see results similar to the following screen shot:</span></span>
  
    ![Pobierz pojedynczy](./media/vs-storage-aspnet-getting-started-tables/delete-entity-results.png)

## <a name="next-steps"></a><span data-ttu-id="a564b-281">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a564b-281">Next steps</span></span>
<span data-ttu-id="a564b-282">Wyświetl więcej poradników dotyczących funkcji, aby dowiedzieć się więcej o dodatkowych opcjach przechowywania danych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="a564b-282">View more feature guides to learn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="a564b-283">Wprowadzenie do magazynu obiektów blob platformy Azure i programu Visual Studio połączone usługi (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="a564b-283">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-blobs.md)
  * [<span data-ttu-id="a564b-284">Rozpoczynanie pracy z magazynem kolejek Azure i programu Visual Studio połączone usługi (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="a564b-284">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-queues.md)
