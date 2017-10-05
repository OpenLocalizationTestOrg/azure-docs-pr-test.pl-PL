---
title: "Aplikacja sieci Web w technologii Node.js wykorzystująca usługę Azure Table Service"
description: "W tym samouczku jest przedstawienie sposobu korzystania z usługi tabel Azure do przechowywania danych z aplikacji Node.js, która jest hostowana w aplikacji sieci Web usługi aplikacji Azure."
tags: azure-portal
services: app-service\web, storage
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 029e6f46-f586-4309-adbf-71c7b8d537d4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 3252914934c1084a165fa39ee983d3039e04d567
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="nodejs-web-app-using-the-azure-table-service"></a><span data-ttu-id="1b5e7-103">Aplikacja sieci Web w technologii Node.js wykorzystująca usługę Azure Table Service</span><span class="sxs-lookup"><span data-stu-id="1b5e7-103">Node.js web app using the Azure Table Service</span></span>
## <a name="overview"></a><span data-ttu-id="1b5e7-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="1b5e7-104">Overview</span></span>
<span data-ttu-id="1b5e7-105">Ten samouczek pokazuje, jak korzystać z usługi tabeli przez zarządzanie danymi Azure do przechowywania i uzyskać dostęp do danych z [węzła] aplikacji hostowanej w [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-105">This tutorial shows you how to use Table service provided by Azure Data Management to store and access data from a [node] application hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps.</span></span> <span data-ttu-id="1b5e7-106">W tym samouczku założono, że pewne doświadczenie w korzystaniu z węzła i [Git].</span><span class="sxs-lookup"><span data-stu-id="1b5e7-106">This tutorial assumes that you have some prior experience using node and [Git].</span></span>

<span data-ttu-id="1b5e7-107">Dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="1b5e7-107">You will learn:</span></span>

* <span data-ttu-id="1b5e7-108">Jak używać programu npm (węzeł Menedżera pakietów) Aby zainstalować moduły węzła</span><span class="sxs-lookup"><span data-stu-id="1b5e7-108">How to use npm (node package manager) to install the node modules</span></span>
* <span data-ttu-id="1b5e7-109">Jak pracować z usługą Azure tabeli</span><span class="sxs-lookup"><span data-stu-id="1b5e7-109">How to work with the Azure Table service</span></span>
* <span data-ttu-id="1b5e7-110">Jak utworzyć aplikację sieci web za pomocą wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-110">How to use the Azure CLI to create a web app.</span></span>

<span data-ttu-id="1b5e7-111">W ramach tego samouczka, utworzysz prostą opartych na sieci web aplikacji "Lista zadań do wykonania", która umożliwia tworzenie, pobieranie i kończenie zadań.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-111">By following this tutorial, you will build a simple web-based "to-do list" application that allows creating, retrieving and completing tasks.</span></span> <span data-ttu-id="1b5e7-112">Zadania są przechowywane w usłudze tabel.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-112">The tasks are stored in the Table service.</span></span>

<span data-ttu-id="1b5e7-113">W tym miejscu jest ukończona aplikacja:</span><span class="sxs-lookup"><span data-stu-id="1b5e7-113">Here is the completed application:</span></span>

![Strona sieci web tasklist pusty][node-table-finished]

> [!NOTE]
> <span data-ttu-id="1b5e7-115">Jeśli chcesz zacząć korzystać z usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź do artykułu [Try App Service](https://azure.microsoft.com/try/app-service/) (Wypróbuj usługę App Service), w którym wyjaśniono, jak od razu utworzyć początkową aplikację sieci Web o krótkim okresie istnienia w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-115">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="1b5e7-116">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-116">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="1b5e7-117">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1b5e7-117">Prerequisites</span></span>
<span data-ttu-id="1b5e7-118">Przed wykonaniem instrukcji zawartych w tym artykule, upewnij się, że masz następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="1b5e7-118">Before following the instructions in this article, ensure that you have the following installed:</span></span>

* <span data-ttu-id="1b5e7-119">[węzła] wersji 0.10.24 lub nowszej</span><span class="sxs-lookup"><span data-stu-id="1b5e7-119">[node] version 0.10.24 or higher</span></span>
* <span data-ttu-id="1b5e7-120">[Git]</span><span class="sxs-lookup"><span data-stu-id="1b5e7-120">[Git]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="create-a-storage-account"></a><span data-ttu-id="1b5e7-121">Tworzenie konta magazynu</span><span class="sxs-lookup"><span data-stu-id="1b5e7-121">Create a storage account</span></span>
<span data-ttu-id="1b5e7-122">Utworzenie konta magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-122">Create an Azure storage account.</span></span> <span data-ttu-id="1b5e7-123">Aplikacja będzie używać tego konta do przechowywania elementów do wykonania.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-123">The app will use this account to store the to-do items.</span></span>

1. <span data-ttu-id="1b5e7-124">Zaloguj się do [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1b5e7-124">Log into the [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="1b5e7-125">Kliknij przycisk **nowy** pozostałych ikony w dolnej części portalu, kliknij przycisk **dane i magazyn** > **magazynu**.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-125">Click the **New** icon on the bottom left of the portal, then click **Data + Storage** > **Storage**.</span></span> <span data-ttu-id="1b5e7-126">Nadaj unikatową nazwę konta magazynu i utworzyć nową [grupy zasobów](../azure-resource-manager/resource-group-overview.md) dla niego.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-126">Give the storage account a unique name and create a new [resource group](../azure-resource-manager/resource-group-overview.md) for it.</span></span>
   
      ![Przycisk Nowy](./media/storage-nodejs-use-table-storage-web-site/configure-storage.png)
   
    <span data-ttu-id="1b5e7-128">Po utworzeniu konta magazynu, **powiadomienia** przycisk będzie flash zielona **Powodzenie** i bloku konto magazynu jest otwarty, aby pokazać, że należy on do tworzenia nowej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-128">When the storage account has been created, the **Notifications** button will flash a green **SUCCESS** and the storage account's blade is open to show that it belongs to the new resource group you created.</span></span>
3. <span data-ttu-id="1b5e7-129">W bloku konto magazynu, kliknij **ustawienia** > **klucze**.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-129">In the storage account's blade, click **Settings** > **Keys**.</span></span> <span data-ttu-id="1b5e7-130">Skopiuj podstawowy klucz dostępu do Schowka.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-130">Copy the primary access key to the clipboard.</span></span>
   
    ![Klucz dostępu][portal-storage-access-keys]

## <a name="install-modules-and-generate-scaffolding"></a><span data-ttu-id="1b5e7-132">Zainstaluj moduły i Generowanie szkieletów</span><span class="sxs-lookup"><span data-stu-id="1b5e7-132">Install modules and generate scaffolding</span></span>
<span data-ttu-id="1b5e7-133">W tej sekcji utworzysz nową aplikację węzła i umożliwia dodawanie pakietów moduł npm.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-133">In this section you will create a new Node application and use npm to add module packages.</span></span> <span data-ttu-id="1b5e7-134">Ta aplikacja będzie używać [Express] i [Azure] modułów.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-134">For this application you will use the [Express] and [Azure] modules.</span></span> <span data-ttu-id="1b5e7-135">Modułu Express zapewnia platformę kontrolera widoku modelu dla węzła, gdy moduł Azure zapewnia łączność z usługą tabeli.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-135">The Express module provides a Model View Controller framework for node, while the Azure modules provides connectivity to the Table service.</span></span>

### <a name="install-express-and-generate-scaffolding"></a><span data-ttu-id="1b5e7-136">Zainstaluj express i Generowanie szkieletów</span><span class="sxs-lookup"><span data-stu-id="1b5e7-136">Install express and generate scaffolding</span></span>
1. <span data-ttu-id="1b5e7-137">W wierszu polecenia Utwórz nowy katalog o nazwie **tasklist** i przełączać się do tego katalogu.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-137">From the command line, create a new directory named **tasklist** and switch to that directory.</span></span>  
2. <span data-ttu-id="1b5e7-138">Wprowadź następujące polecenie, aby zainstalować moduł Express.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-138">Enter the following command to install the Express module.</span></span>
   
        npm install express-generator@4.2.0 -g
   
    <span data-ttu-id="1b5e7-139">W zależności od systemu operacyjnego może być konieczne umieszczanie 'sudo' przed wykonaniem polecenia:</span><span class="sxs-lookup"><span data-stu-id="1b5e7-139">Depending on the operating system, you may need to put 'sudo' before the command:</span></span>
   
        sudo npm install express-generator@4.2.0 -g
   
    <span data-ttu-id="1b5e7-140">Dane wyjściowe wygląda podobnie do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="1b5e7-140">The output appears similar to the following example:</span></span>
   
        express-generator@4.2.0 /usr/local/lib/node_modules/express-generator
        ├── mkdirp@0.3.5
        └── commander@1.3.2 (keypress@0.1.0)
   
   > [!NOTE]
   > <span data-ttu-id="1b5e7-141">"-G" parametr instaluje moduł globalnie.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-141">The '-g' parameter installs the module globally.</span></span> <span data-ttu-id="1b5e7-142">W ten sposób możemy użyć **express** do generowania szkieletu aplikacji sieci web bez konieczności wpisz dodatkowe informacje o ścieżce.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-142">That way, we can use **express** to generate web app scaffolding without having to type in additional path information.</span></span>
   > 
   > 
3. <span data-ttu-id="1b5e7-143">Aby utworzyć szkielet aplikacji, wprowadź **express** polecenia:</span><span class="sxs-lookup"><span data-stu-id="1b5e7-143">To create the scaffolding for the application, enter the **express** command:</span></span>
   
        express
   
    <span data-ttu-id="1b5e7-144">Dane wyjściowe tego polecenia jest podobny do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="1b5e7-144">The output of this command appears similar to the following example:</span></span>
   
           create : .
           create : ./package.json
           create : ./app.js
           create : ./public
           create : ./public/images
           create : ./routes
           create : ./routes/index.js
           create : ./routes/users.js
           create : ./public/stylesheets
           create : ./public/stylesheets/style.css
           create : ./views
           create : ./views/index.jade
           create : ./views/layout.jade
           create : ./views/error.jade
           create : ./public/javascripts
           create : ./bin
           create : ./bin/www
   
           install dependencies:
             $ cd . && npm install
   
           run the app:
             $ DEBUG=my-application ./bin/www
   
    <span data-ttu-id="1b5e7-145">Masz teraz kilka nowych katalogów i plików w **tasklist** katalogu.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-145">You now have several new directories and files in the **tasklist** directory.</span></span>

### <a name="install-additional-modules"></a><span data-ttu-id="1b5e7-146">Instalowanie dodatkowych modułów</span><span class="sxs-lookup"><span data-stu-id="1b5e7-146">Install additional modules</span></span>
<span data-ttu-id="1b5e7-147">Jeden z plików który **express** tworzy jest **package.json**.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-147">One of the files that **express** creates is **package.json**.</span></span> <span data-ttu-id="1b5e7-148">Ten plik zawiera listę zależności modułu.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-148">This file contains a list of module dependencies.</span></span> <span data-ttu-id="1b5e7-149">Później podczas wdrażania aplikacji do aplikacji usługi sieci Web aplikacji, ten plik Określa, które moduły muszą być zainstalowane na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-149">Later, when you deploy the application to App Service Web Apps, this file determines which modules need to be installed on Azure.</span></span>

<span data-ttu-id="1b5e7-150">W wierszu polecenia wprowadź następujące polecenie, aby zainstalować moduły opisanego w **package.json** pliku.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-150">From the command-line, enter the following command to install the modules described in the **package.json** file.</span></span> <span data-ttu-id="1b5e7-151">Może być konieczne użycie "sudo".</span><span class="sxs-lookup"><span data-stu-id="1b5e7-151">You may need to use 'sudo'.</span></span>

    npm install

<span data-ttu-id="1b5e7-152">Dane wyjściowe tego polecenia jest podobny do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="1b5e7-152">The output of this command appears similar to the following example:</span></span>

    debug@0.7.4 node_modules\debug

    cookie-parser@1.0.1 node_modules\cookie-parser
    ├── cookie-signature@1.0.3
    └── cookie@0.1.0

    [...]


<span data-ttu-id="1b5e7-153">Następnie wprowadź następujące polecenie, aby zainstalować [azure], [uuid węzła], [nconf] i [async] modułów:</span><span class="sxs-lookup"><span data-stu-id="1b5e7-153">Next, enter the following command to install the [azure], [node-uuid], [nconf] and [async] modules:</span></span>

    npm install azure-storage node-uuid async nconf --save

<span data-ttu-id="1b5e7-154">**— Zapisywanie** Flaga Dodaje wpisy dla tych modułów, aby **package.json** pliku.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-154">The **--save** flag adds entries for these modules to the **package.json** file.</span></span>

<span data-ttu-id="1b5e7-155">Dane wyjściowe tego polecenia jest podobny do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="1b5e7-155">The output of this command appears similar to the following example:</span></span>

    async@0.9.0 node_modules\async

    node-uuid@1.4.1 node_modules\node-uuid

    nconf@0.6.9 node_modules\nconf
    ├── ini@1.2.1
    ├── async@0.2.9
    └── optimist@0.6.0 (wordwrap@0.0.2, minimist@0.0.10)

    [...]


## <a name="create-the-application"></a><span data-ttu-id="1b5e7-156">Tworzenie aplikacji</span><span class="sxs-lookup"><span data-stu-id="1b5e7-156">Create the application</span></span>
<span data-ttu-id="1b5e7-157">Teraz już wszystko gotowe do tworzenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-157">Now we're ready to build the application.</span></span>

### <a name="create-a-model"></a><span data-ttu-id="1b5e7-158">Tworzenie modelu</span><span class="sxs-lookup"><span data-stu-id="1b5e7-158">Create a model</span></span>
<span data-ttu-id="1b5e7-159">A *modelu* jest obiekt, który reprezentuje dane w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-159">A *model* is an object that represents the data in your application.</span></span> <span data-ttu-id="1b5e7-160">Dla aplikacji tylko model jest obiekt zadania, który reprezentuje element na liście zadań do wykonania.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-160">For the application, the only model is a task object, which represents an item in the to-do list.</span></span> <span data-ttu-id="1b5e7-161">Zadania będzie zawierać następujące pola:</span><span class="sxs-lookup"><span data-stu-id="1b5e7-161">Tasks will have the following fields:</span></span>

* <span data-ttu-id="1b5e7-162">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="1b5e7-162">PartitionKey</span></span>
* <span data-ttu-id="1b5e7-163">RowKey</span><span class="sxs-lookup"><span data-stu-id="1b5e7-163">RowKey</span></span>
* <span data-ttu-id="1b5e7-164">Nazwa (ciąg)</span><span class="sxs-lookup"><span data-stu-id="1b5e7-164">name (string)</span></span>
* <span data-ttu-id="1b5e7-165">Kategoria (ciąg)</span><span class="sxs-lookup"><span data-stu-id="1b5e7-165">category (string)</span></span>
* <span data-ttu-id="1b5e7-166">Ukończono (wartość logiczna)</span><span class="sxs-lookup"><span data-stu-id="1b5e7-166">completed (Boolean)</span></span>

<span data-ttu-id="1b5e7-167">**PartitionKey** i **RowKey** są używane przez usługę tabeli jako klucze tabeli.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-167">**PartitionKey** and **RowKey** are used by the Table Service as table keys.</span></span> <span data-ttu-id="1b5e7-168">Aby uzyskać więcej informacji, zobacz [opis modelu danych usługi tabel](https://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="1b5e7-168">For more information, see [Understanding the Table Service data model](https://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

1. <span data-ttu-id="1b5e7-169">W **tasklist** katalogu, Utwórz nowy katalog o nazwie **modele**.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-169">In the **tasklist** directory, create a new directory named **models**.</span></span>
2. <span data-ttu-id="1b5e7-170">W **modele** katalogu, Utwórz nowy plik o nazwie **task.js**.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-170">In the **models** directory, create a new file named **task.js**.</span></span> <span data-ttu-id="1b5e7-171">Ten plik zawiera model dla zadań tworzonych przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-171">This file will contain the model for the tasks created by your application.</span></span>
3. <span data-ttu-id="1b5e7-172">Na początku **task.js** pliku, Dodaj następujący kod, aby odwołać wymagane biblioteki:</span><span class="sxs-lookup"><span data-stu-id="1b5e7-172">At the beginning of the **task.js** file, add the following code to reference required libraries:</span></span>
   
        var azure = require('azure-storage');
          var uuid = require('node-uuid');
        var entityGen = azure.TableUtilities.entityGenerator;
4. <span data-ttu-id="1b5e7-173">Dodaj następujący kod w celu zdefiniowania i wyeksportowania obiektu Task.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-173">Add the following code to define and export the Task object.</span></span> <span data-ttu-id="1b5e7-174">Ten obiekt jest odpowiedzialny za nawiązywania połączenia z tabeli.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-174">This object is responsible for connecting to the table.</span></span>
   
          module.exports = Task;
   
        function Task(storageClient, tableName, partitionKey) {
          this.storageClient = storageClient;
          this.tableName = tableName;
          this.partitionKey = partitionKey;
          this.storageClient.createTableIfNotExists(tableName, function tableCreated(error) {
            if(error) {
              throw error;
            }
          });
        };
5. <span data-ttu-id="1b5e7-175">Dodaj następujący kod, aby zdefiniować dodatkowe metody dla obiektu Task umożliwiające interakcje z danymi przechowywanymi w tabeli:</span><span class="sxs-lookup"><span data-stu-id="1b5e7-175">Add the following code to define additional methods on the Task object, which allow interactions with data stored in the table:</span></span>
   
        Task.prototype = {
          find: function(query, callback) {
            self = this;
            self.storageClient.queryEntities(this.tableName, query, null, function entitiesQueried(error, result) {
              if(error) {
                callback(error);
              } else {
                callback(null, result.entries);
              }
            });
          },
   
          addItem: function(item, callback) {
            self = this;
            // use entityGenerator to set types
            // NOTE: RowKey must be a string type, even though
            // it contains a GUID in this example.
            var itemDescriptor = {
              PartitionKey: entityGen.String(self.partitionKey),
              RowKey: entityGen.String(uuid()),
              name: entityGen.String(item.name),
              category: entityGen.String(item.category),
              completed: entityGen.Boolean(false)
            };
            self.storageClient.insertEntity(self.tableName, itemDescriptor, function entityInserted(error) {
              if(error){  
                callback(error);
              }
              callback(null);
            });
          },
   
          updateItem: function(rKey, callback) {
            self = this;
            self.storageClient.retrieveEntity(self.tableName, self.partitionKey, rKey, function entityQueried(error, entity) {
              if(error) {
                callback(error);
              }
              entity.completed._ = true;
              self.storageClient.updateEntity(self.tableName, entity, function entityUpdated(error) {
                if(error) {
                  callback(error);
                }
                callback(null);
              });
            });
          }
        }
6. <span data-ttu-id="1b5e7-176">Zapisz i Zamknij **task.js** pliku.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-176">Save and close the **task.js** file.</span></span>

### <a name="create-a-controller"></a><span data-ttu-id="1b5e7-177">Tworzenie kontrolera</span><span class="sxs-lookup"><span data-stu-id="1b5e7-177">Create a controller</span></span>
<span data-ttu-id="1b5e7-178">A *kontrolera* obsługi żądań HTTP i renderuje odpowiedzi HTML.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-178">A *controller* handles HTTP requests and renders the HTML response.</span></span>

1. <span data-ttu-id="1b5e7-179">W **tasklist/trasy** katalogu, Utwórz nowy plik o nazwie **tasklist.js** i otwórz go w edytorze tekstów.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-179">In the **tasklist/routes** directory, create a new file named **tasklist.js** and open it in a text editor.</span></span>
2. <span data-ttu-id="1b5e7-180">Dodaj następujący kod do pliku **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-180">Add the following code to **tasklist.js**.</span></span> <span data-ttu-id="1b5e7-181">Spowoduje to załadowanie modułów azure i async, które są używane przez **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-181">This loads the azure and async modules, which are used by **tasklist.js**.</span></span> <span data-ttu-id="1b5e7-182">Definiuje również **TaskList** funkcji, która została przekazana wystąpienia **zadań** zdefiniowanego wcześniej:</span><span class="sxs-lookup"><span data-stu-id="1b5e7-182">This also defines the **TaskList** function, which is passed an instance of the **Task** object we defined earlier:</span></span>
   
        var azure = require('azure-storage');
        var async = require('async');
   
        module.exports = TaskList;
3. <span data-ttu-id="1b5e7-183">Zdefiniuj **TaskList** obiektu.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-183">Define a **TaskList** object.</span></span>
   
        function TaskList(task) {
          this.task = task;
        }
4. <span data-ttu-id="1b5e7-184">Dodaj następujące metody umożliwiające **TaskList**:</span><span class="sxs-lookup"><span data-stu-id="1b5e7-184">Add the following methods to **TaskList**:</span></span>
   
        TaskList.prototype = {
          showTasks: function(req, res) {
            self = this;
            var query = new azure.TableQuery()
              .where('completed eq ?', false);
            self.task.find(query, function itemsFound(error, items) {
              res.render('index',{title: 'My ToDo List ', tasks: items});
            });
          },
   
          addTask: function(req,res) {
            var self = this;
            var item = req.body.item;
            self.task.addItem(item, function itemAdded(error) {
              if(error) {
                throw error;
              }
              res.redirect('/');
            });
          },
   
          completeTask: function(req,res) {
            var self = this;
            var completedTasks = Object.keys(req.body);
            async.forEach(completedTasks, function taskIterator(completedTask, callback) {
              self.task.updateItem(completedTask, function itemsUpdated(error) {
                if(error){
                  callback(error);
                } else {
                  callback(null);
                }
              });
            }, function goHome(error){
              if(error) {
                throw error;
              } else {
               res.redirect('/');
              }
            });
          }
        }

### <a name="modify-appjs"></a><span data-ttu-id="1b5e7-185">Modyfikowanie pliku app.js</span><span class="sxs-lookup"><span data-stu-id="1b5e7-185">Modify app.js</span></span>
1. <span data-ttu-id="1b5e7-186">Z **tasklist** katalogu, otwórz **app.js** pliku.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-186">From the **tasklist** directory, open the **app.js** file.</span></span> <span data-ttu-id="1b5e7-187">Ten plik został utworzony wcześniej przez uruchomienie **express** polecenia.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-187">This file was created earlier by running the **express** command.</span></span>
2. <span data-ttu-id="1b5e7-188">Na początku pliku Dodaj następujące polecenie, aby załadować moduł azure, ustaw nazwę tabeli klucza partycji i Ustaw poświadczenia magazynu użyte w tym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="1b5e7-188">At the beginning of the file, add the following to load the azure module, set the table name, partition key, and set the storage credentials used by this example:</span></span>
   
        var azure = require('azure-storage');
        var nconf = require('nconf');
        nconf.env()
             .file({ file: 'config.json', search: true });
        var tableName = nconf.get("TABLE_NAME");
        var partitionKey = nconf.get("PARTITION_KEY");
        var accountName = nconf.get("STORAGE_NAME");
        var accountKey = nconf.get("STORAGE_KEY");
   
   > [!NOTE]
   > <span data-ttu-id="1b5e7-189">nconf załaduje wartości konfiguracji z obu zmiennych środowiskowych lub **config.json** pliku, który zostanie utworzony później.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-189">nconf will load the configuration values from either environment variables or the **config.json** file, which we will create later.</span></span>
   > 
   > 
3. <span data-ttu-id="1b5e7-190">W pliku app.js przewiń w dół, do której występuje następujący wiersz:</span><span class="sxs-lookup"><span data-stu-id="1b5e7-190">In the app.js file, scroll down to where you see the following line:</span></span>
   
        app.use('/', routes);
        app.use('/users', users);
   
    <span data-ttu-id="1b5e7-191">Zamień wiersze powyżej kodu pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-191">Replace the above lines with the code shown below.</span></span> <span data-ttu-id="1b5e7-192">Spowoduje to zainicjować wystąpienia <strong>zadań</strong> z połączeniem z konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-192">This will initialize an instance of <strong>Task</strong> with a connection to your storage account.</span></span> <span data-ttu-id="1b5e7-193">To jest przekazywana do <strong>TaskList</strong>, który zostanie użyty do komunikowania się z usługą tabeli:</span><span class="sxs-lookup"><span data-stu-id="1b5e7-193">This is passed to the <strong>TaskList</strong>, which will use it to communicate with the Table service:</span></span>
   
        var TaskList = require('./routes/tasklist');
        var Task = require('./models/task');
        var task = new Task(azure.createTableService(accountName, accountKey), tableName, partitionKey);
        var taskList = new TaskList(task);
   
        app.get('/', taskList.showTasks.bind(taskList));
        app.post('/addtask', taskList.addTask.bind(taskList));
        app.post('/completetask', taskList.completeTask.bind(taskList));
4. <span data-ttu-id="1b5e7-194">Zapisz **app.js** pliku.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-194">Save the **app.js** file.</span></span>

### <a name="modify-the-index-view"></a><span data-ttu-id="1b5e7-195">Zmodyfikuj widok indeksu</span><span class="sxs-lookup"><span data-stu-id="1b5e7-195">Modify the index view</span></span>
1. <span data-ttu-id="1b5e7-196">Otwórz **tasklist/views/index.jade** plik w edytorze tekstów.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-196">Open the **tasklist/views/index.jade** file in a text editor.</span></span>
2. <span data-ttu-id="1b5e7-197">Zastąp całą zawartość pliku następującym kodem.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-197">Replace the entire contents of the file with the following code.</span></span> <span data-ttu-id="1b5e7-198">Określa widok, w którym wyświetlane istniejące zadania oraz formularz służący do dodawania nowych zadań i oznaczenie istniejących jako ukończone.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-198">This defines a view that displays existing tasks and includes a form for adding new tasks and marking existing ones as completed.</span></span>
   
        extends layout
   
        block content
          h1= title
          br
   
          form(action="/completetask", method="post")
            table.table.table-striped.table-bordered
              tr
                td Name
                td Category
                td Date
                td Complete
              if (typeof tasks === "undefined")
                tr
                  td
              else
                each task in tasks
                  tr
                    td #{task.name._}
                    td #{task.category._}
                    - var day   = task.Timestamp._.getDate();
                    - var month = task.Timestamp._.getMonth() + 1;
                    - var year  = task.Timestamp._.getFullYear();
                    td #{month + "/" + day + "/" + year}
                    td
                      input(type="checkbox", name="#{task.RowKey._}", value="#{!task.completed._}", checked=task.completed._)
            button.btn(type="submit") Update tasks
          hr
          form.well(action="/addtask", method="post")
            label Item Name:
            input(name="item[name]", type="textbox")
            label Item Category:
            input(name="item[category]", type="textbox")
            br
            button.btn(type="submit") Add item
3. <span data-ttu-id="1b5e7-199">Zapisz i Zamknij **index.jade** pliku.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-199">Save and close **index.jade** file.</span></span>

### <a name="modify-the-global-layout"></a><span data-ttu-id="1b5e7-200">Modyfikowanie globalnych układu</span><span class="sxs-lookup"><span data-stu-id="1b5e7-200">Modify the global layout</span></span>
<span data-ttu-id="1b5e7-201">**Layout.jade** w pliku **widoków** katalog jest szablon globalny dla innych **jade** plików.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-201">The **layout.jade** file in the **views** directory is a global template for other **.jade** files.</span></span> <span data-ttu-id="1b5e7-202">W tym kroku zmodyfikujesz go do korzystania ze [Twitter Bootstrap](https://github.com/twbs/bootstrap), która jest zestawem narzędzi ułatwiającym projektowanie nieuprzywilejowany wyglądającej aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-202">In this step you will modify it to use [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy to design a nice looking web app.</span></span>

<span data-ttu-id="1b5e7-203">Pobierz i Wyodrębnij pliki do [Twitter Bootstrap](http://getbootstrap.com/).</span><span class="sxs-lookup"><span data-stu-id="1b5e7-203">Download and extract the files for [Twitter Bootstrap](http://getbootstrap.com/).</span></span> <span data-ttu-id="1b5e7-204">Kopiuj **bootstrap.min.css** pliku z ładowania początkowego programu **css** do folderu **publiczne/arkusze stylów** katalogu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-204">Copy the **bootstrap.min.css** file from the Bootstrap **css** folder into the **public/stylesheets** directory of your application.</span></span>

<span data-ttu-id="1b5e7-205">Z **widoków** folder, otwórz **layout.jade** i Zastąp całą zawartość następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="1b5e7-205">From the **views** folder, open **layout.jade** and replace the entire contents with the following:</span></span>

    doctype html
    html
      head
        title= title
        link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')
        link(rel='stylesheet', href='/stylesheets/style.css')
      body.app
        nav.navbar.navbar-default
          div.navbar-header
          a.navbar-brand(href='/') My Tasks
        block content

### <a name="create-a-config-file"></a><span data-ttu-id="1b5e7-206">Utwórz plik konfiguracji</span><span class="sxs-lookup"><span data-stu-id="1b5e7-206">Create a config file</span></span>
<span data-ttu-id="1b5e7-207">Aby uruchomić aplikację lokalnie, będzie testujemy poświadczeń usługi Azure Storage w pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-207">To run the app locally, we'll put Azure Storage credentials into a config file.</span></span> <span data-ttu-id="1b5e7-208">Utwórz plik o nazwie **config.json* * z następujących JSON:</span><span class="sxs-lookup"><span data-stu-id="1b5e7-208">Create a file named **config.json* *with the following JSON:</span></span>

    {
        "STORAGE_NAME": "<storage account name>",
        "STORAGE_KEY": "<storage access key>",
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

<span data-ttu-id="1b5e7-209">Zastąp **nazwy konta magazynu** o nazwie magazynu konta utworzonego wcześniej i Zastąp **klucz dostępu do magazynu** z podstawowy klucz dostępu dla konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-209">Replace **storage account name** with the name of the storage account you created earlier, and replace **storage access key** with the primary access key for your storage account.</span></span> <span data-ttu-id="1b5e7-210">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="1b5e7-210">For example:</span></span>

    {
        "STORAGE_NAME": "nodejsappstorage",
        "STORAGE_KEY": "KG0oDd..."
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

<span data-ttu-id="1b5e7-211">Zapisz ten plik *poziomu katalogów wyższych* niż **tasklist** katalogu w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="1b5e7-211">Save this file *one directory level higher* than the **tasklist** directory, like this:</span></span>

    parent/
      |-- config.json
      |-- tasklist/

<span data-ttu-id="1b5e7-212">Przyczyna w ten sposób jest uniknięcie sprawdzania pliku konfiguracji do kontroli źródła, gdzie mogą być publiczny.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-212">The reason for doing this is to avoid checking the config file into source control, where it might become public.</span></span> <span data-ttu-id="1b5e7-213">Firma Microsoft wdrażania aplikacji na platformie Azure, użyjemy zmienne środowiskowe zamiast pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-213">When we deploy the app to Azure, we will use environment variables instead of a config file.</span></span>

## <a name="run-the-application-locally"></a><span data-ttu-id="1b5e7-214">Uruchamianie aplikacji lokalnie</span><span class="sxs-lookup"><span data-stu-id="1b5e7-214">Run the application locally</span></span>
<span data-ttu-id="1b5e7-215">Aby przetestować aplikację na komputerze lokalnym, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="1b5e7-215">To test the application on your local machine, perform the following steps:</span></span>

1. <span data-ttu-id="1b5e7-216">W wierszu polecenia Zmień katalog na **tasklist** katalogu.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-216">From the command-line, change directories to the **tasklist** directory.</span></span>
2. <span data-ttu-id="1b5e7-217">Aby uruchomić aplikację lokalnie, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="1b5e7-217">Use the following command to launch the application locally:</span></span>
   
        npm start
3. <span data-ttu-id="1b5e7-218">Otwórz przeglądarkę sieci web i przejdź do http://127.0.0.1:3000.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-218">Open a web browser and navigate to http://127.0.0.1:3000.</span></span>
   
    <span data-ttu-id="1b5e7-219">Zostanie wyświetlona strona sieci web podobny do poniższego przykładu.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-219">A web page similar to the following example appears.</span></span>
   
    ![Wyświetlanie tasklist puste strony sieci Web][node-table-finished]
4. <span data-ttu-id="1b5e7-221">Aby utworzyć nowe zadanie do wykonania, wprowadź nazwę i kategorii, a następnie kliknij przycisk **Dodaj element**.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-221">To create a new to-do item, enter a name and category and click **Add Item**.</span></span> 
5. <span data-ttu-id="1b5e7-222">Aby oznaczyć zadanie jako zakończone, sprawdź **Complete** i kliknij przycisk **zadania aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-222">To mark a task as complete, check **Complete** and click **Update Tasks**.</span></span>
   
    ![Obraz nowego elementu na liście zadań][node-table-list-items]

<span data-ttu-id="1b5e7-224">Mimo że aplikacja działa lokalnie, danych jest przechowywana w usłudze tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-224">Even though the application is running locally, it is storing the data in the Azure Table service.</span></span>

## <a name="deploy-your-application-to-azure"></a><span data-ttu-id="1b5e7-225">Wdrażanie aplikacji na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="1b5e7-225">Deploy your application to Azure</span></span>
<span data-ttu-id="1b5e7-226">Kroki opisane w tej sekcji umożliwiają tworzenie nowej aplikacji sieci web w usłudze App Service narzędzia wiersza polecenia platformy Azure, a następnie użyj Git do wdrożenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-226">The steps in this section use the Azure command-line tools to create a new web app in App Service, and then use Git to deploy your application.</span></span> <span data-ttu-id="1b5e7-227">Aby wykonać te czynności musi mieć subskrypcję platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-227">To perform these steps you must have an Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="1b5e7-228">Można także wykonać te czynności przy użyciu [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1b5e7-228">These steps can also be performed by using the [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="1b5e7-229">Zobacz [tworzenia i wdrażania aplikacji sieci web Node.js w usłudze Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="1b5e7-229">See [Build and deploy a Node.js web app in Azure App Service].</span></span>
> 
> <span data-ttu-id="1b5e7-230">Jeśli jest to pierwszej aplikacji sieci web, które zostały utworzone, należy wdrożyć tę aplikację za pomocą portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-230">If this is the first web app you have created, you must use the Azure Portal to deploy this application.</span></span>
> 
> 

<span data-ttu-id="1b5e7-231">Aby rozpocząć pracę, należy zainstalować [interfejsu wiersza polecenia Azure] , wprowadzając następujące polecenie w wierszu polecenia:</span><span class="sxs-lookup"><span data-stu-id="1b5e7-231">To get started, install the [Azure CLI] by entering the following command from the command line:</span></span>

    npm install azure-cli -g

### <a name="import-publishing-settings"></a><span data-ttu-id="1b5e7-232">Importowanie ustawień publikowania</span><span class="sxs-lookup"><span data-stu-id="1b5e7-232">Import publishing settings</span></span>
<span data-ttu-id="1b5e7-233">W tym kroku pobierze plik zawierający informacje o Twojej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-233">In this step, you will download a file containing information about your subscription.</span></span>

1. <span data-ttu-id="1b5e7-234">Wprowadź następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="1b5e7-234">Enter the following command:</span></span>
   
        azure login
   
    <span data-ttu-id="1b5e7-235">To polecenie spowoduje uruchomienie przeglądarki i przechodzi do strony pobierania.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-235">This command launches a browser and navigates to the download page.</span></span> <span data-ttu-id="1b5e7-236">W przypadku wyświetlenia monitu zaloguj się przy użyciu konta skojarzonego z subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-236">If prompted, log in with the account associated with your Azure subscription.</span></span>
   
    <!-- ![The download page][download-publishing-settings] -->
   
    <span data-ttu-id="1b5e7-237">Pobieranie pliku rozpoczyna się automatycznie. Jeśli nie, kliknięcie łącza na początku strony, aby ręcznie pobrać plik.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-237">The file download begins automatically; if it does not, you can click the link at the beginning of the page to manually download the file.</span></span> <span data-ttu-id="1b5e7-238">Zapisz plik i Zanotuj ścieżkę pliku.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-238">Save the file and note the file path.</span></span>
2. <span data-ttu-id="1b5e7-239">Wprowadź następujące polecenie, aby zaimportować ustawienia:</span><span class="sxs-lookup"><span data-stu-id="1b5e7-239">Enter the following command to import the settings:</span></span>
   
        azure account import <path-to-file>
   
    <span data-ttu-id="1b5e7-240">Określ ścieżkę i nazwę pliku ustawień publikowania, który został pobrany w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-240">Specify the path and file name of the publishing settings file you downloaded in the previous step.</span></span>
3. <span data-ttu-id="1b5e7-241">Zaimportowane ustawienia, należy usunąć plik ustawień publikowania.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-241">After the settings are imported, delete the publish settings file.</span></span> <span data-ttu-id="1b5e7-242">Nie jest już potrzebne i zawiera poufne informacje dotyczące subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-242">It is no longer needed, and contains sensitive information regarding your Azure subscription.</span></span>

### <a name="create-an-app-service-web-app"></a><span data-ttu-id="1b5e7-243">Tworzenie aplikacji sieci web usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="1b5e7-243">Create an App Service web app</span></span>
1. <span data-ttu-id="1b5e7-244">W wierszu polecenia Zmień katalog na **tasklist** katalogu.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-244">From the command-line, change directories to the **tasklist** directory.</span></span>
2. <span data-ttu-id="1b5e7-245">Użyj następującego polecenia, aby utworzyć nową aplikację sieci web.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-245">Use the following command to create a new web app.</span></span>
   
        azure site create --git
   
    <span data-ttu-id="1b5e7-246">Pojawi się monit dla nazwy aplikacji sieci web i lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-246">You will be prompted for the web app name and location.</span></span> <span data-ttu-id="1b5e7-247">Podaj unikatową nazwę i wybierz tej samej lokalizacji geograficznej co konto magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-247">Provide a unique name and select the same geographical location as your Azure Storage account.</span></span>
   
    <span data-ttu-id="1b5e7-248">`--git` Parametr tworzy repozytorium Git na platformie Azure dla tej aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-248">The `--git` parameter creates a Git repository on Azure for this web app.</span></span> <span data-ttu-id="1b5e7-249">Inicjuje również repozytorium Git w bieżącym katalogu, jeśli nie istnieje i dodaje [zdalnego Git] o nazwie "azure", która jest używana do publikowania aplikacji na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-249">It also initializes a Git repository in the current directory if none exists, and adds a [Git remote] named 'azure', which is used to publish the application to Azure.</span></span> <span data-ttu-id="1b5e7-250">Na koniec tworzy **web.config** pliku, który zawiera ustawienia używane przez usługę Azure umożliwia obsługę aplikacji węzła.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-250">Finally, it creates a **web.config** file, which contains settings used by Azure to host node applications.</span></span> <span data-ttu-id="1b5e7-251">W przypadku pominięcia `--git` parametr, ale katalog zawiera repozytorium Git, polecenie nadal utworzy azure zdalnego.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-251">If you omit the `--git` parameter but the directory contains a Git repository, the command will still create the 'azure' remote.</span></span>
   
    <span data-ttu-id="1b5e7-252">Po ukończeniu tego polecenia, zostanie wyświetlone dane wyjściowe podobne do następującego.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-252">Once this command has completed, you will see output similar to the following.</span></span> <span data-ttu-id="1b5e7-253">Należy pamiętać, że wiersz, począwszy od **witryny sieci Web utworzonego w dniu** zawiera adres URL aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-253">Note that the line beginning with **Website created at** contains the URL for the web app.</span></span>
   
        info:   Executing command site create
        help:   Need a site name
        Name: TableTasklist
        info:   Using location southcentraluswebspace
        info:   Executing `git init`
        info:   Creating default .gitignore file
        info:   Creating a new web site
        info:   Created web site at  tabletasklist.azurewebsites.net
        info:   Initializing repository
        info:   Repository initialized
        info:   Executing `git remote add azure https://username@tabletasklist.azurewebsites.net/TableTasklist.git`
        info:   site create command OK
   
   > [!NOTE]
   > <span data-ttu-id="1b5e7-254">Jeśli jest to pierwszej aplikacji sieci web usługi aplikacji — dla Twojej subskrypcji, pojawi się instrukcja za pomocą portalu Azure do utworzenia aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-254">If this is the first App Service web app for your subscription, you will be instructed to use the Azure Portal to create the web app.</span></span> <span data-ttu-id="1b5e7-255">Aby uzyskać więcej informacji, zobacz [tworzenia i wdrażania aplikacji sieci web Node.js w usłudze Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="1b5e7-255">For more information, see [Build and deploy a Node.js web app in Azure App Service].</span></span>
   > 
   > 

### <a name="set-environment-variables"></a><span data-ttu-id="1b5e7-256">Ustaw zmienne środowiskowe</span><span class="sxs-lookup"><span data-stu-id="1b5e7-256">Set environment variables</span></span>
<span data-ttu-id="1b5e7-257">W tym kroku zmiennych środowiskowych zostaną dodane do konfiguracji aplikacji sieci web na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-257">In this step, you will add environment variables to your web app configuration on Azure.</span></span>
<span data-ttu-id="1b5e7-258">W wierszu polecenia wprowadź następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="1b5e7-258">From the command line, enter the following:</span></span>

    azure site appsetting add
        STORAGE_NAME=<storage account name>;STORAGE_KEY=<storage access key>;PARTITION_KEY=mytasks;TABLE_NAME=tasks


<span data-ttu-id="1b5e7-259">Zastąp  **<storage account name>**  o nazwie magazynu konta utworzonego wcześniej i Zastąp  **<storage access key>**  z podstawowy klucz dostępu dla konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-259">Replace **<storage account name>** with the name of the storage account you created earlier, and replace **<storage access key>** with the primary access key for your storage account.</span></span> <span data-ttu-id="1b5e7-260">(Użyj tej samej wartości jako plik config.json, który został utworzony wcześniej).</span><span class="sxs-lookup"><span data-stu-id="1b5e7-260">(Use the same values as the config.json file that you created earlier.)</span></span>

<span data-ttu-id="1b5e7-261">Alternatywnie można ustawić zmienne środowiskowe [Azure Portal](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="1b5e7-261">Alternatively, you can set environment variables in the [Azure Portal](https://portal.azure.com/):</span></span>

1. <span data-ttu-id="1b5e7-262">Otwarcie bloku aplikacji sieci web, klikając **Przeglądaj** > **aplikacje sieci Web** > Nazwa aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-262">Open the web app's blade by clicking **Browse** > **Web Apps** > your web app name.</span></span>
2. <span data-ttu-id="1b5e7-263">W bloku aplikacja sieci web, kliknij przycisk **wszystkie ustawienia** > **ustawienia aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-263">In your web app's blade, click **All Settings** > **Application Settings**.</span></span>
   
     <!-- ![Top Menu](./media/storage-nodejs-use-table-storage-web-site/PollsCommonWebSiteTopMenu.png) -->
3. <span data-ttu-id="1b5e7-264">Przewiń w dół do **ustawień aplikacji** i Dodaj pary klucz wartość.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-264">Scroll down to the **App settings** section and add the key/value pairs.</span></span>
   
     ![Ustawienia aplikacji](./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png)
4. <span data-ttu-id="1b5e7-266">Kliknij przycisk **SAVE** (Zapisz).</span><span class="sxs-lookup"><span data-stu-id="1b5e7-266">Click **SAVE**.</span></span>

### <a name="publish-the-application"></a><span data-ttu-id="1b5e7-267">Publikowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="1b5e7-267">Publish the application</span></span>
<span data-ttu-id="1b5e7-268">Aby opublikować aplikację, Przekaż plików kodu do Git, a następnie Wypchnij azure/wzorzec.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-268">To publish the app, commit the code files to Git and then push to azure/master.</span></span>

1. <span data-ttu-id="1b5e7-269">Ustaw poświadczenia wdrażania.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-269">Set your deployment credentials.</span></span>
   
        azure site deployment user set <name> <password>
2. <span data-ttu-id="1b5e7-270">Dodaj i zatwierdź plików aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-270">Add and commit your application files.</span></span>
   
        git add .
        git commit -m "adding files"
3. <span data-ttu-id="1b5e7-271">Wypchnij zatwierdzenia do aplikacji sieci web usługi aplikacji:</span><span class="sxs-lookup"><span data-stu-id="1b5e7-271">Push the commit to the App Service web app:</span></span>
   
        git push azure master
   
    <span data-ttu-id="1b5e7-272">Użyj **wzorca** jako gałęzi docelowej.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-272">Use **master** as the target branch.</span></span> <span data-ttu-id="1b5e7-273">Po zakończeniu wdrażania zobacz temat instrukcję podobny do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="1b5e7-273">At the end of the deployment, you see a statement similar to the following example:</span></span>
   
        To https://username@tabletasklist.azurewebsites.net/TableTasklist.git
          * [new branch]      master -> master
4. <span data-ttu-id="1b5e7-274">Po ukończeniu operacji wypychania, przejdź do adresu URL aplikacji sieci web, które zostały wcześniej zwrócony przez `azure create site` polecenie, aby wyświetlić aplikację.</span><span class="sxs-lookup"><span data-stu-id="1b5e7-274">Once the push operation has completed, browse to the web app URL returned previously by the `azure create site` command to view your application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b5e7-275">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1b5e7-275">Next steps</span></span>
<span data-ttu-id="1b5e7-276">Podczas czynności opisane w tym artykule opisano przy użyciu usługi tabel do przechowywania informacji, można również użyć [MongoDB](https://mlab.com/azure/).</span><span class="sxs-lookup"><span data-stu-id="1b5e7-276">While the steps in this article describe using the Table Service to store information, you can also use [MongoDB](https://mlab.com/azure/).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1b5e7-277">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="1b5e7-277">Additional resources</span></span>
<span data-ttu-id="1b5e7-278">[interfejsu wiersza polecenia Azure]</span><span class="sxs-lookup"><span data-stu-id="1b5e7-278">[Azure CLI]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="1b5e7-279">Co zostało zmienione</span><span class="sxs-lookup"><span data-stu-id="1b5e7-279">What's changed</span></span>
* <span data-ttu-id="1b5e7-280">Przewodnik dotyczący przejścia od usługi Witryny sieci Web do usługi App Service można znaleźć w temacie [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714) (Usługa Azure App Service i jej wpływ na istniejące usługi platformy Azure).</span><span class="sxs-lookup"><span data-stu-id="1b5e7-280">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- URLs -->

<span data-ttu-id="1b5e7-281">[tworzenia i wdrażania aplikacji sieci web Node.js w usłudze Azure App Service]: app-service-web-get-started-nodejs.md</span><span class="sxs-lookup"><span data-stu-id="1b5e7-281">[Build and deploy a Node.js web app in Azure App Service]: app-service-web-get-started-nodejs.md</span></span>
[Azure Developer Center]: /develop/nodejs/

<span data-ttu-id="1b5e7-282">[węzła]: http://nodejs.org</span><span class="sxs-lookup"><span data-stu-id="1b5e7-282">[node]: http://nodejs.org</span></span>
<span data-ttu-id="1b5e7-283">[Git]: http://git-scm.com</span><span class="sxs-lookup"><span data-stu-id="1b5e7-283">[Git]: http://git-scm.com</span></span>
<span data-ttu-id="1b5e7-284">[Express]: http://expressjs.com</span><span class="sxs-lookup"><span data-stu-id="1b5e7-284">[Express]: http://expressjs.com</span></span>
[for free]: http://windowsazure.com
<span data-ttu-id="1b5e7-285">[zdalnego Git]: http://git-scm.com/docs/git-remote</span><span class="sxs-lookup"><span data-stu-id="1b5e7-285">[Git remote]: http://git-scm.com/docs/git-remote</span></span>

<span data-ttu-id="1b5e7-286">[interfejsu wiersza polecenia Azure]:../cli-install-nodejs.md</span><span class="sxs-lookup"><span data-stu-id="1b5e7-286">[Azure CLI]:../cli-install-nodejs.md</span></span>

<span data-ttu-id="1b5e7-287">[azure]: https://github.com/Azure/azure-sdk-for-node</span><span class="sxs-lookup"><span data-stu-id="1b5e7-287">[azure]: https://github.com/Azure/azure-sdk-for-node</span></span>
<span data-ttu-id="1b5e7-288">[uuid węzła]: https://www.npmjs.com/package/node-uuid</span><span class="sxs-lookup"><span data-stu-id="1b5e7-288">[node-uuid]: https://www.npmjs.com/package/node-uuid</span></span>
<span data-ttu-id="1b5e7-289">[nconf]: https://www.npmjs.com/package/nconf</span><span class="sxs-lookup"><span data-stu-id="1b5e7-289">[nconf]: https://www.npmjs.com/package/nconf</span></span>
<span data-ttu-id="1b5e7-290">[async]: https://www.npmjs.com/package/async</span><span class="sxs-lookup"><span data-stu-id="1b5e7-290">[async]: https://www.npmjs.com/package/async</span></span>

[Azure Portal]: https://portal.azure.com

[Create and deploy a Node.js application to an Azure Web Site]: app-service-web-get-started-nodejs.md

<!-- Image References -->

[node-table-finished]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_empty.png
[node-table-list-items]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_list.png
[download-publishing-settings]: ./media/storage-nodejs-use-table-storage-web-site/azure-account-download-cli.png
[portal-storage-access-keys]: ./media/storage-nodejs-use-table-storage-web-site/manage-access-keys.png
[app-settings]: ./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png
