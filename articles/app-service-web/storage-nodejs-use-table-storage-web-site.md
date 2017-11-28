---
title: "aaaNode.js aplikacji sieci web przy użyciu hello Azure usługa tabel"
description: "Ten samouczek zawiera wskazówki dotyczące sposobu hello toouse tabel Azure usługi toostore danych z aplikacji Node.js, który jest obsługiwany w aplikacji sieci Web usługi aplikacji Azure."
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
ms.openlocfilehash: f6e08335b4c7f62f7b3994287edd586860cb7135
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-web-app-using-hello-azure-table-service"></a><span data-ttu-id="3fc67-103">Aplikacja sieci web node.js za pomocą hello Azure usługa tabel</span><span class="sxs-lookup"><span data-stu-id="3fc67-103">Node.js web app using hello Azure Table Service</span></span>
## <a name="overview"></a><span data-ttu-id="3fc67-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="3fc67-104">Overview</span></span>
<span data-ttu-id="3fc67-105">Ten samouczek pokazuje, jak usługa tabel toouse udostępniane przez zarządzanie danymi Azure toostore i dostępu do danych z [węzła] aplikacji hostowanej w [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="3fc67-105">This tutorial shows you how toouse Table service provided by Azure Data Management toostore and access data from a [node] application hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps.</span></span> <span data-ttu-id="3fc67-106">W tym samouczku założono, że pewne doświadczenie w korzystaniu z węzła i [Git].</span><span class="sxs-lookup"><span data-stu-id="3fc67-106">This tutorial assumes that you have some prior experience using node and [Git].</span></span>

<span data-ttu-id="3fc67-107">Dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="3fc67-107">You will learn:</span></span>

* <span data-ttu-id="3fc67-108">Jak tooinstall npm (węzeł Menedżera pakietów) toouse hello modułów węzła</span><span class="sxs-lookup"><span data-stu-id="3fc67-108">How toouse npm (node package manager) tooinstall hello node modules</span></span>
* <span data-ttu-id="3fc67-109">Jak toowork z hello usługi tabeli platformy Azure</span><span class="sxs-lookup"><span data-stu-id="3fc67-109">How toowork with hello Azure Table service</span></span>
* <span data-ttu-id="3fc67-110">Jak toouse hello toocreate wiersza polecenia platformy Azure, aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="3fc67-110">How toouse hello Azure CLI toocreate a web app.</span></span>

<span data-ttu-id="3fc67-111">W ramach tego samouczka, utworzysz prostą opartych na sieci web aplikacji "Lista zadań do wykonania", która umożliwia tworzenie, pobieranie i kończenie zadań.</span><span class="sxs-lookup"><span data-stu-id="3fc67-111">By following this tutorial, you will build a simple web-based "to-do list" application that allows creating, retrieving and completing tasks.</span></span> <span data-ttu-id="3fc67-112">Witaj zadania są przechowywane w hello usługi tabel.</span><span class="sxs-lookup"><span data-stu-id="3fc67-112">hello tasks are stored in hello Table service.</span></span>

<span data-ttu-id="3fc67-113">Oto aplikacji hello zakończone:</span><span class="sxs-lookup"><span data-stu-id="3fc67-113">Here is hello completed application:</span></span>

![Strona sieci web tasklist pusty][node-table-finished]

> [!NOTE]
> <span data-ttu-id="3fc67-115">Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="3fc67-115">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="3fc67-116">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="3fc67-116">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="3fc67-117">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3fc67-117">Prerequisites</span></span>
<span data-ttu-id="3fc67-118">Przed rozpoczęciem powitalne instrukcje w tym artykule, upewnij się, że mają zainstalowane następujące hello:</span><span class="sxs-lookup"><span data-stu-id="3fc67-118">Before following hello instructions in this article, ensure that you have hello following installed:</span></span>

* <span data-ttu-id="3fc67-119">[węzła] wersji 0.10.24 lub nowszej</span><span class="sxs-lookup"><span data-stu-id="3fc67-119">[node] version 0.10.24 or higher</span></span>
* <span data-ttu-id="3fc67-120">[Git]</span><span class="sxs-lookup"><span data-stu-id="3fc67-120">[Git]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="create-a-storage-account"></a><span data-ttu-id="3fc67-121">Tworzenie konta magazynu</span><span class="sxs-lookup"><span data-stu-id="3fc67-121">Create a storage account</span></span>
<span data-ttu-id="3fc67-122">Utworzenie konta magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3fc67-122">Create an Azure storage account.</span></span> <span data-ttu-id="3fc67-123">Aplikacja Hello będzie używać tego konta toostore hello zadaniach do wykonania.</span><span class="sxs-lookup"><span data-stu-id="3fc67-123">hello app will use this account toostore hello to-do items.</span></span>

1. <span data-ttu-id="3fc67-124">Zaloguj się do hello [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3fc67-124">Log into hello [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="3fc67-125">Kliknij przycisk hello **nowy** ikony na dole hello pozostałych hello portalu, kliknij przycisk **dane i magazyn** > **magazynu**.</span><span class="sxs-lookup"><span data-stu-id="3fc67-125">Click hello **New** icon on hello bottom left of hello portal, then click **Data + Storage** > **Storage**.</span></span> <span data-ttu-id="3fc67-126">Nadaj unikatową nazwę konta magazynu hello i utworzyć nową [grupy zasobów](../azure-resource-manager/resource-group-overview.md) dla niego.</span><span class="sxs-lookup"><span data-stu-id="3fc67-126">Give hello storage account a unique name and create a new [resource group](../azure-resource-manager/resource-group-overview.md) for it.</span></span>
   
      ![Przycisk Nowy](./media/storage-nodejs-use-table-storage-web-site/configure-storage.png)
   
    <span data-ttu-id="3fc67-128">Po utworzeniu konta magazynu hello hello **powiadomienia** przycisk będzie flash zielona **Powodzenie** i bloku konto magazynu hello jest otwarty tooshow należy toohello nowy zasób grupy utworzony.</span><span class="sxs-lookup"><span data-stu-id="3fc67-128">When hello storage account has been created, hello **Notifications** button will flash a green **SUCCESS** and hello storage account's blade is open tooshow that it belongs toohello new resource group you created.</span></span>
3. <span data-ttu-id="3fc67-129">W bloku konto magazynu powitania kliknij **ustawienia** > **klucze**.</span><span class="sxs-lookup"><span data-stu-id="3fc67-129">In hello storage account's blade, click **Settings** > **Keys**.</span></span> <span data-ttu-id="3fc67-130">Kopiuj hello Schowka toohello klucza podstawowego dostępu.</span><span class="sxs-lookup"><span data-stu-id="3fc67-130">Copy hello primary access key toohello clipboard.</span></span>
   
    ![Klucz dostępu][portal-storage-access-keys]

## <a name="install-modules-and-generate-scaffolding"></a><span data-ttu-id="3fc67-132">Zainstaluj moduły i Generowanie szkieletów</span><span class="sxs-lookup"><span data-stu-id="3fc67-132">Install modules and generate scaffolding</span></span>
<span data-ttu-id="3fc67-133">W tej sekcji utworzysz nową aplikację węzła i za pomocą programu npm tooadd modułu pakietów.</span><span class="sxs-lookup"><span data-stu-id="3fc67-133">In this section you will create a new Node application and use npm tooadd module packages.</span></span> <span data-ttu-id="3fc67-134">Dla tej aplikacji będzie używać hello [Express] i [Azure] modułów.</span><span class="sxs-lookup"><span data-stu-id="3fc67-134">For this application you will use hello [Express] and [Azure] modules.</span></span> <span data-ttu-id="3fc67-135">Hello modułu Express zapewnia platformę kontrolera widoku modelu dla węzła, podczas hello modułów Azure udostępnia usługi tabel toohello łączności.</span><span class="sxs-lookup"><span data-stu-id="3fc67-135">hello Express module provides a Model View Controller framework for node, while hello Azure modules provides connectivity toohello Table service.</span></span>

### <a name="install-express-and-generate-scaffolding"></a><span data-ttu-id="3fc67-136">Zainstaluj express i Generowanie szkieletów</span><span class="sxs-lookup"><span data-stu-id="3fc67-136">Install express and generate scaffolding</span></span>
1. <span data-ttu-id="3fc67-137">Z wiersza polecenia hello, Utwórz nowy katalog o nazwie **tasklist** i katalog toothat przełącznika.</span><span class="sxs-lookup"><span data-stu-id="3fc67-137">From hello command line, create a new directory named **tasklist** and switch toothat directory.</span></span>  
2. <span data-ttu-id="3fc67-138">Wprowadź hello następujące polecenia tooinstall hello Express modułu.</span><span class="sxs-lookup"><span data-stu-id="3fc67-138">Enter hello following command tooinstall hello Express module.</span></span>
   
        npm install express-generator@4.2.0 -g
   
    <span data-ttu-id="3fc67-139">W zależności od systemu operacyjnego hello może być konieczne tooput 'sudo' przed wykonaniem polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="3fc67-139">Depending on hello operating system, you may need tooput 'sudo' before hello command:</span></span>
   
        sudo npm install express-generator@4.2.0 -g
   
    <span data-ttu-id="3fc67-140">dane wyjściowe Hello pojawia się toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="3fc67-140">hello output appears similar toohello following example:</span></span>
   
        express-generator@4.2.0 /usr/local/lib/node_modules/express-generator
        ├── mkdirp@0.3.5
        └── commander@1.3.2 (keypress@0.1.0)
   
   > [!NOTE]
   > <span data-ttu-id="3fc67-141">Witaj "-g" parametr instaluje moduł hello globalnie.</span><span class="sxs-lookup"><span data-stu-id="3fc67-141">hello '-g' parameter installs hello module globally.</span></span> <span data-ttu-id="3fc67-142">W ten sposób możemy użyć **express** toogenerate funkcja szkieletów aplikacji sieci web bez konieczności tootype w dodatkowe informacje o ścieżce.</span><span class="sxs-lookup"><span data-stu-id="3fc67-142">That way, we can use **express** toogenerate web app scaffolding without having tootype in additional path information.</span></span>
   > 
   > 
3. <span data-ttu-id="3fc67-143">toocreate hello szkieletów dla aplikacji hello wprowadź hello **express** polecenia:</span><span class="sxs-lookup"><span data-stu-id="3fc67-143">toocreate hello scaffolding for hello application, enter hello **express** command:</span></span>
   
        express
   
    <span data-ttu-id="3fc67-144">Witaj dane wyjściowe tego polecenia zostaną wyświetlone podobne toohello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="3fc67-144">hello output of this command appears similar toohello following example:</span></span>
   
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
   
           run hello app:
             $ DEBUG=my-application ./bin/www
   
    <span data-ttu-id="3fc67-145">Masz teraz kilka nowych katalogów i plików w hello **tasklist** katalogu.</span><span class="sxs-lookup"><span data-stu-id="3fc67-145">You now have several new directories and files in hello **tasklist** directory.</span></span>

### <a name="install-additional-modules"></a><span data-ttu-id="3fc67-146">Instalowanie dodatkowych modułów</span><span class="sxs-lookup"><span data-stu-id="3fc67-146">Install additional modules</span></span>
<span data-ttu-id="3fc67-147">Jeden z hello pliki **express** tworzy jest **package.json**.</span><span class="sxs-lookup"><span data-stu-id="3fc67-147">One of hello files that **express** creates is **package.json**.</span></span> <span data-ttu-id="3fc67-148">Ten plik zawiera listę zależności modułu.</span><span class="sxs-lookup"><span data-stu-id="3fc67-148">This file contains a list of module dependencies.</span></span> <span data-ttu-id="3fc67-149">Później podczas wdrażania tooApp aplikacji hello usługi aplikacje sieci Web, ten plik Określa, które moduły muszą toobe zainstalowane na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="3fc67-149">Later, when you deploy hello application tooApp Service Web Apps, this file determines which modules need toobe installed on Azure.</span></span>

<span data-ttu-id="3fc67-150">Z wiersza polecenia hello, wprowadź następujące moduły hello tooinstall polecenia opisanego w hello hello **package.json** pliku.</span><span class="sxs-lookup"><span data-stu-id="3fc67-150">From hello command-line, enter hello following command tooinstall hello modules described in hello **package.json** file.</span></span> <span data-ttu-id="3fc67-151">Może być konieczne toouse "sudo".</span><span class="sxs-lookup"><span data-stu-id="3fc67-151">You may need toouse 'sudo'.</span></span>

    npm install

<span data-ttu-id="3fc67-152">Witaj dane wyjściowe tego polecenia zostaną wyświetlone podobne toohello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="3fc67-152">hello output of this command appears similar toohello following example:</span></span>

    debug@0.7.4 node_modules\debug

    cookie-parser@1.0.1 node_modules\cookie-parser
    ├── cookie-signature@1.0.3
    └── cookie@0.1.0

    [...]


<span data-ttu-id="3fc67-153">Następnie wprowadź następujące polecenie tooinstall hello hello [azure], [uuid węzła], [nconf] i [async] modułów:</span><span class="sxs-lookup"><span data-stu-id="3fc67-153">Next, enter hello following command tooinstall hello [azure], [node-uuid], [nconf] and [async] modules:</span></span>

    npm install azure-storage node-uuid async nconf --save

<span data-ttu-id="3fc67-154">Witaj **— zapisywanie** Flaga Dodaje wpisy dla tych modułów toohello **package.json** pliku.</span><span class="sxs-lookup"><span data-stu-id="3fc67-154">hello **--save** flag adds entries for these modules toohello **package.json** file.</span></span>

<span data-ttu-id="3fc67-155">Witaj dane wyjściowe tego polecenia zostaną wyświetlone podobne toohello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="3fc67-155">hello output of this command appears similar toohello following example:</span></span>

    async@0.9.0 node_modules\async

    node-uuid@1.4.1 node_modules\node-uuid

    nconf@0.6.9 node_modules\nconf
    ├── ini@1.2.1
    ├── async@0.2.9
    └── optimist@0.6.0 (wordwrap@0.0.2, minimist@0.0.10)

    [...]


## <a name="create-hello-application"></a><span data-ttu-id="3fc67-156">Tworzenie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="3fc67-156">Create hello application</span></span>
<span data-ttu-id="3fc67-157">Jest teraz gotowy toobuild hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3fc67-157">Now we're ready toobuild hello application.</span></span>

### <a name="create-a-model"></a><span data-ttu-id="3fc67-158">Tworzenie modelu</span><span class="sxs-lookup"><span data-stu-id="3fc67-158">Create a model</span></span>
<span data-ttu-id="3fc67-159">A *modelu* jest obiekt, który reprezentuje dane hello w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3fc67-159">A *model* is an object that represents hello data in your application.</span></span> <span data-ttu-id="3fc67-160">Dla aplikacji hello modelu tylko hello jest obiekt zadania, który reprezentuje element w hello listy zadań do wykonania.</span><span class="sxs-lookup"><span data-stu-id="3fc67-160">For hello application, hello only model is a task object, which represents an item in hello to-do list.</span></span> <span data-ttu-id="3fc67-161">Zadania mają hello następujące pola:</span><span class="sxs-lookup"><span data-stu-id="3fc67-161">Tasks will have hello following fields:</span></span>

* <span data-ttu-id="3fc67-162">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="3fc67-162">PartitionKey</span></span>
* <span data-ttu-id="3fc67-163">RowKey</span><span class="sxs-lookup"><span data-stu-id="3fc67-163">RowKey</span></span>
* <span data-ttu-id="3fc67-164">Nazwa (ciąg)</span><span class="sxs-lookup"><span data-stu-id="3fc67-164">name (string)</span></span>
* <span data-ttu-id="3fc67-165">Kategoria (ciąg)</span><span class="sxs-lookup"><span data-stu-id="3fc67-165">category (string)</span></span>
* <span data-ttu-id="3fc67-166">Ukończono (wartość logiczna)</span><span class="sxs-lookup"><span data-stu-id="3fc67-166">completed (Boolean)</span></span>

<span data-ttu-id="3fc67-167">**PartitionKey** i **RowKey** są używane przez usługi tabel hello jako klucze tabeli.</span><span class="sxs-lookup"><span data-stu-id="3fc67-167">**PartitionKey** and **RowKey** are used by hello Table Service as table keys.</span></span> <span data-ttu-id="3fc67-168">Aby uzyskać więcej informacji, zobacz [modelu danych usługi tabel hello opis](https://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="3fc67-168">For more information, see [Understanding hello Table Service data model](https://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

1. <span data-ttu-id="3fc67-169">W hello **tasklist** katalogu, Utwórz nowy katalog o nazwie **modele**.</span><span class="sxs-lookup"><span data-stu-id="3fc67-169">In hello **tasklist** directory, create a new directory named **models**.</span></span>
2. <span data-ttu-id="3fc67-170">W hello **modele** katalogu, Utwórz nowy plik o nazwie **task.js**.</span><span class="sxs-lookup"><span data-stu-id="3fc67-170">In hello **models** directory, create a new file named **task.js**.</span></span> <span data-ttu-id="3fc67-171">Ten plik będzie zawierać hello model dla zadań hello utworzonych przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="3fc67-171">This file will contain hello model for hello tasks created by your application.</span></span>
3. <span data-ttu-id="3fc67-172">Na początku hello hello **task.js** plików, dodawanie hello następującego kodu tooreference wymagane biblioteki:</span><span class="sxs-lookup"><span data-stu-id="3fc67-172">At hello beginning of hello **task.js** file, add hello following code tooreference required libraries:</span></span>
   
        var azure = require('azure-storage');
          var uuid = require('node-uuid');
        var entityGen = azure.TableUtilities.entityGenerator;
4. <span data-ttu-id="3fc67-173">Dodaj następujący hello code toodefine i wyeksportować hello obiektu zadania.</span><span class="sxs-lookup"><span data-stu-id="3fc67-173">Add hello following code toodefine and export hello Task object.</span></span> <span data-ttu-id="3fc67-174">Ten obiekt jest odpowiedzialny za łączenie toohello tabeli.</span><span class="sxs-lookup"><span data-stu-id="3fc67-174">This object is responsible for connecting toohello table.</span></span>
   
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
5. <span data-ttu-id="3fc67-175">Dodaj hello następującego kodu toodefine dodatkowe metody dla obiektu zadania hello, umożliwiające interakcje z danymi przechowywanymi w tabeli hello:</span><span class="sxs-lookup"><span data-stu-id="3fc67-175">Add hello following code toodefine additional methods on hello Task object, which allow interactions with data stored in hello table:</span></span>
   
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
            // use entityGenerator tooset types
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
6. <span data-ttu-id="3fc67-176">Zapisz i zamknij hello **task.js** pliku.</span><span class="sxs-lookup"><span data-stu-id="3fc67-176">Save and close hello **task.js** file.</span></span>

### <a name="create-a-controller"></a><span data-ttu-id="3fc67-177">Tworzenie kontrolera</span><span class="sxs-lookup"><span data-stu-id="3fc67-177">Create a controller</span></span>
<span data-ttu-id="3fc67-178">A *kontrolera* obsługi żądań HTTP i renderuje odpowiedź hello HTML.</span><span class="sxs-lookup"><span data-stu-id="3fc67-178">A *controller* handles HTTP requests and renders hello HTML response.</span></span>

1. <span data-ttu-id="3fc67-179">W hello **tasklist/trasy** katalogu, Utwórz nowy plik o nazwie **tasklist.js** i otwórz go w edytorze tekstów.</span><span class="sxs-lookup"><span data-stu-id="3fc67-179">In hello **tasklist/routes** directory, create a new file named **tasklist.js** and open it in a text editor.</span></span>
2. <span data-ttu-id="3fc67-180">Dodaj hello zbyt następującego kodu**tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="3fc67-180">Add hello following code too**tasklist.js**.</span></span> <span data-ttu-id="3fc67-181">Spowoduje to załadowanie modułów hello azure i async, które są używane przez **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="3fc67-181">This loads hello azure and async modules, which are used by **tasklist.js**.</span></span> <span data-ttu-id="3fc67-182">Definiuje również hello **TaskList** funkcji, która przekazuje wystąpienie hello **zadań** zdefiniowanego wcześniej:</span><span class="sxs-lookup"><span data-stu-id="3fc67-182">This also defines hello **TaskList** function, which is passed an instance of hello **Task** object we defined earlier:</span></span>
   
        var azure = require('azure-storage');
        var async = require('async');
   
        module.exports = TaskList;
3. <span data-ttu-id="3fc67-183">Zdefiniuj **TaskList** obiektu.</span><span class="sxs-lookup"><span data-stu-id="3fc67-183">Define a **TaskList** object.</span></span>
   
        function TaskList(task) {
          this.task = task;
        }
4. <span data-ttu-id="3fc67-184">Dodaj następujące metody zbyt hello**TaskList**:</span><span class="sxs-lookup"><span data-stu-id="3fc67-184">Add hello following methods too**TaskList**:</span></span>
   
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

### <a name="modify-appjs"></a><span data-ttu-id="3fc67-185">Modyfikowanie pliku app.js</span><span class="sxs-lookup"><span data-stu-id="3fc67-185">Modify app.js</span></span>
1. <span data-ttu-id="3fc67-186">Z hello **tasklist** hello katalogu, otwórz **app.js** pliku.</span><span class="sxs-lookup"><span data-stu-id="3fc67-186">From hello **tasklist** directory, open hello **app.js** file.</span></span> <span data-ttu-id="3fc67-187">Ten plik został utworzony wcześniej przez uruchomienie hello **express** polecenia.</span><span class="sxs-lookup"><span data-stu-id="3fc67-187">This file was created earlier by running hello **express** command.</span></span>
2. <span data-ttu-id="3fc67-188">Na początku hello pliku hello, Dodaj powitania po tooload hello azure modułu, nazwa tabeli hello zestawu klucz partycji i poświadczenia magazynu hello zestaw używany w tym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="3fc67-188">At hello beginning of hello file, add hello following tooload hello azure module, set hello table name, partition key, and set hello storage credentials used by this example:</span></span>
   
        var azure = require('azure-storage');
        var nconf = require('nconf');
        nconf.env()
             .file({ file: 'config.json', search: true });
        var tableName = nconf.get("TABLE_NAME");
        var partitionKey = nconf.get("PARTITION_KEY");
        var accountName = nconf.get("STORAGE_NAME");
        var accountKey = nconf.get("STORAGE_KEY");
   
   > [!NOTE]
   > <span data-ttu-id="3fc67-189">nconf załaduje hello konfiguracji wartości zmiennych środowiskowych lub hello **config.json** pliku, który zostanie utworzony później.</span><span class="sxs-lookup"><span data-stu-id="3fc67-189">nconf will load hello configuration values from either environment variables or hello **config.json** file, which we will create later.</span></span>
   > 
   > 
3. <span data-ttu-id="3fc67-190">W pliku app.js hello, przewiń w dół toowhere widzisz hello następujący wiersz:</span><span class="sxs-lookup"><span data-stu-id="3fc67-190">In hello app.js file, scroll down toowhere you see hello following line:</span></span>
   
        app.use('/', routes);
        app.use('/users', users);
   
    <span data-ttu-id="3fc67-191">Zastąp hello powyżej wierszy kodu hello pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="3fc67-191">Replace hello above lines with hello code shown below.</span></span> <span data-ttu-id="3fc67-192">Spowoduje to zainicjować wystąpienia <strong>zadań</strong> z kontem magazynu tooyour połączenia.</span><span class="sxs-lookup"><span data-stu-id="3fc67-192">This will initialize an instance of <strong>Task</strong> with a connection tooyour storage account.</span></span> <span data-ttu-id="3fc67-193">To jest przekazywany toohello <strong>TaskList</strong>, którego użyje on toocommunicate z hello usługa tabel:</span><span class="sxs-lookup"><span data-stu-id="3fc67-193">This is passed toohello <strong>TaskList</strong>, which will use it toocommunicate with hello Table service:</span></span>
   
        var TaskList = require('./routes/tasklist');
        var Task = require('./models/task');
        var task = new Task(azure.createTableService(accountName, accountKey), tableName, partitionKey);
        var taskList = new TaskList(task);
   
        app.get('/', taskList.showTasks.bind(taskList));
        app.post('/addtask', taskList.addTask.bind(taskList));
        app.post('/completetask', taskList.completeTask.bind(taskList));
4. <span data-ttu-id="3fc67-194">Zapisz hello **app.js** pliku.</span><span class="sxs-lookup"><span data-stu-id="3fc67-194">Save hello **app.js** file.</span></span>

### <a name="modify-hello-index-view"></a><span data-ttu-id="3fc67-195">Zmodyfikuj widok indeksu hello</span><span class="sxs-lookup"><span data-stu-id="3fc67-195">Modify hello index view</span></span>
1. <span data-ttu-id="3fc67-196">Otwórz hello **tasklist/views/index.jade** plik w edytorze tekstów.</span><span class="sxs-lookup"><span data-stu-id="3fc67-196">Open hello **tasklist/views/index.jade** file in a text editor.</span></span>
2. <span data-ttu-id="3fc67-197">Zastąp całą zawartość pliku hello hello hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="3fc67-197">Replace hello entire contents of hello file with hello following code.</span></span> <span data-ttu-id="3fc67-198">Określa widok, w którym wyświetlane istniejące zadania oraz formularz służący do dodawania nowych zadań i oznaczenie istniejących jako ukończone.</span><span class="sxs-lookup"><span data-stu-id="3fc67-198">This defines a view that displays existing tasks and includes a form for adding new tasks and marking existing ones as completed.</span></span>
   
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
3. <span data-ttu-id="3fc67-199">Zapisz i Zamknij **index.jade** pliku.</span><span class="sxs-lookup"><span data-stu-id="3fc67-199">Save and close **index.jade** file.</span></span>

### <a name="modify-hello-global-layout"></a><span data-ttu-id="3fc67-200">Modyfikuj hello układ globalne</span><span class="sxs-lookup"><span data-stu-id="3fc67-200">Modify hello global layout</span></span>
<span data-ttu-id="3fc67-201">Witaj **layout.jade** pliku w hello **widoków** katalog jest szablon globalny dla innych **jade** plików.</span><span class="sxs-lookup"><span data-stu-id="3fc67-201">hello **layout.jade** file in hello **views** directory is a global template for other **.jade** files.</span></span> <span data-ttu-id="3fc67-202">W tym kroku zmodyfikujesz go toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), która jest zestawem narzędzi, który umożliwia łatwe toodesign nieuprzywilejowany wyglądającej aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="3fc67-202">In this step you will modify it toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy toodesign a nice looking web app.</span></span>

<span data-ttu-id="3fc67-203">Pobierać i wyodrębniać pliki hello [Twitter Bootstrap](http://getbootstrap.com/).</span><span class="sxs-lookup"><span data-stu-id="3fc67-203">Download and extract hello files for [Twitter Bootstrap](http://getbootstrap.com/).</span></span> <span data-ttu-id="3fc67-204">Hello kopiowania **bootstrap.min.css** pliku z hello Bootstrap **css** folderu do hello **publiczne/arkusze stylów** katalogu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3fc67-204">Copy hello **bootstrap.min.css** file from hello Bootstrap **css** folder into hello **public/stylesheets** directory of your application.</span></span>

<span data-ttu-id="3fc67-205">Z hello **widoków** folder, otwórz **layout.jade** i Zastąp całą zawartość hello hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="3fc67-205">From hello **views** folder, open **layout.jade** and replace hello entire contents with hello following:</span></span>

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

### <a name="create-a-config-file"></a><span data-ttu-id="3fc67-206">Utwórz plik konfiguracji</span><span class="sxs-lookup"><span data-stu-id="3fc67-206">Create a config file</span></span>
<span data-ttu-id="3fc67-207">toorun lokalnie aplikacji hello, będzie testujemy poświadczeń usługi Azure Storage w pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="3fc67-207">toorun hello app locally, we'll put Azure Storage credentials into a config file.</span></span> <span data-ttu-id="3fc67-208">Utwórz plik o nazwie **config.json* * z powitania po JSON:</span><span class="sxs-lookup"><span data-stu-id="3fc67-208">Create a file named **config.json* *with hello following JSON:</span></span>

    {
        "STORAGE_NAME": "<storage account name>",
        "STORAGE_KEY": "<storage access key>",
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

<span data-ttu-id="3fc67-209">Zastąp **nazwy konta magazynu** o nazwie hello magazynu hello konta utworzonego wcześniej i Zastąp **klucz dostępu do magazynu** z hello podstawowy klucz dostępu dla konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="3fc67-209">Replace **storage account name** with hello name of hello storage account you created earlier, and replace **storage access key** with hello primary access key for your storage account.</span></span> <span data-ttu-id="3fc67-210">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="3fc67-210">For example:</span></span>

    {
        "STORAGE_NAME": "nodejsappstorage",
        "STORAGE_KEY": "KG0oDd..."
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

<span data-ttu-id="3fc67-211">Zapisz ten plik *poziomu katalogów wyższych* niż hello **tasklist** katalogu w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="3fc67-211">Save this file *one directory level higher* than hello **tasklist** directory, like this:</span></span>

    parent/
      |-- config.json
      |-- tasklist/

<span data-ttu-id="3fc67-212">Przyczyna Hello w ten sposób jest tooavoid sprawdzanie hello pliku konfiguracji do kontroli źródła, gdzie mogą być publiczny.</span><span class="sxs-lookup"><span data-stu-id="3fc67-212">hello reason for doing this is tooavoid checking hello config file into source control, where it might become public.</span></span> <span data-ttu-id="3fc67-213">Firma Microsoft wdrażania tooAzure aplikacji hello, użyjemy zmienne środowiskowe zamiast pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="3fc67-213">When we deploy hello app tooAzure, we will use environment variables instead of a config file.</span></span>

## <a name="run-hello-application-locally"></a><span data-ttu-id="3fc67-214">Uruchamianie aplikacji hello lokalnie</span><span class="sxs-lookup"><span data-stu-id="3fc67-214">Run hello application locally</span></span>
<span data-ttu-id="3fc67-215">Aplikacja hello tootest na komputerze lokalnym, wykonywać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="3fc67-215">tootest hello application on your local machine, perform hello following steps:</span></span>

1. <span data-ttu-id="3fc67-216">Z wiersza polecenia hello, zmień katalogi toohello **tasklist** katalogu.</span><span class="sxs-lookup"><span data-stu-id="3fc67-216">From hello command-line, change directories toohello **tasklist** directory.</span></span>
2. <span data-ttu-id="3fc67-217">Użyj hello następujące polecenie lokalnie aplikacji hello toolaunch:</span><span class="sxs-lookup"><span data-stu-id="3fc67-217">Use hello following command toolaunch hello application locally:</span></span>
   
        npm start
3. <span data-ttu-id="3fc67-218">Otwórz przeglądarkę sieci web i przejdź toohttp://127.0.0.1:3000.</span><span class="sxs-lookup"><span data-stu-id="3fc67-218">Open a web browser and navigate toohttp://127.0.0.1:3000.</span></span>
   
    <span data-ttu-id="3fc67-219">Zostanie wyświetlona strona sieci web toohello podobne, poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="3fc67-219">A web page similar toohello following example appears.</span></span>
   
    ![Wyświetlanie tasklist puste strony sieci Web][node-table-finished]
4. <span data-ttu-id="3fc67-221">toocreate nowe zadanie do wykonania, wprowadź nazwę i kategorii i kliknij przycisk **Dodaj element**.</span><span class="sxs-lookup"><span data-stu-id="3fc67-221">toocreate a new to-do item, enter a name and category and click **Add Item**.</span></span> 
5. <span data-ttu-id="3fc67-222">zadanie jako zakończone, sprawdź toomark **Complete** i kliknij przycisk **zadania aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="3fc67-222">toomark a task as complete, check **Complete** and click **Update Tasks**.</span></span>
   
    ![Obraz powitania nowy element hello listy zadań][node-table-list-items]

<span data-ttu-id="3fc67-224">Mimo że aplikacja hello działa lokalnie, hello danych jest przechowywana w hello usługi tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="3fc67-224">Even though hello application is running locally, it is storing hello data in hello Azure Table service.</span></span>

## <a name="deploy-your-application-tooazure"></a><span data-ttu-id="3fc67-225">Wdrażanie tooAzure Twojej aplikacji</span><span class="sxs-lookup"><span data-stu-id="3fc67-225">Deploy your application tooAzure</span></span>
<span data-ttu-id="3fc67-226">kroki Hello w tej sekcji Użyj toocreate narzędzi wiersza polecenia platformy Azure hello nowej aplikacji sieci web w usłudze App Service, a następnie użyj Git toodeploy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3fc67-226">hello steps in this section use hello Azure command-line tools toocreate a new web app in App Service, and then use Git toodeploy your application.</span></span> <span data-ttu-id="3fc67-227">tooperform następujące kroki, musi mieć subskrypcję platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3fc67-227">tooperform these steps you must have an Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="3fc67-228">Można także wykonać te czynności przy użyciu hello [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3fc67-228">These steps can also be performed by using hello [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="3fc67-229">Zobacz [tworzenia i wdrażania aplikacji sieci web Node.js w usłudze Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="3fc67-229">See [Build and deploy a Node.js web app in Azure App Service].</span></span>
> 
> <span data-ttu-id="3fc67-230">Jeśli jest to hello pierwszej aplikacji sieci web utworzone, należy użyć hello toodeploy Azure Portal tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3fc67-230">If this is hello first web app you have created, you must use hello Azure Portal toodeploy this application.</span></span>
> 
> 

<span data-ttu-id="3fc67-231">tooget pracę, zainstaluj hello [interfejsu wiersza polecenia Azure] , wprowadzając następujące polecenie z wiersza polecenia hello hello:</span><span class="sxs-lookup"><span data-stu-id="3fc67-231">tooget started, install hello [Azure CLI] by entering hello following command from hello command line:</span></span>

    npm install azure-cli -g

### <a name="import-publishing-settings"></a><span data-ttu-id="3fc67-232">Importowanie ustawień publikowania</span><span class="sxs-lookup"><span data-stu-id="3fc67-232">Import publishing settings</span></span>
<span data-ttu-id="3fc67-233">W tym kroku pobierze plik zawierający informacje o Twojej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="3fc67-233">In this step, you will download a file containing information about your subscription.</span></span>

1. <span data-ttu-id="3fc67-234">Wprowadź hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="3fc67-234">Enter hello following command:</span></span>
   
        azure login
   
    <span data-ttu-id="3fc67-235">To polecenie spowoduje uruchomienie przeglądarki i przechodzi do strony pobierania toohello.</span><span class="sxs-lookup"><span data-stu-id="3fc67-235">This command launches a browser and navigates toohello download page.</span></span> <span data-ttu-id="3fc67-236">W przypadku wyświetlenia monitu zaloguj się przy użyciu konta hello skojarzonego z subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3fc67-236">If prompted, log in with hello account associated with your Azure subscription.</span></span>
   
    <!-- ![hello download page][download-publishing-settings] -->
   
    <span data-ttu-id="3fc67-237">Pobieranie pliku Hello rozpoczyna się automatycznie. Jeśli nie, mogą kliknąć link hello na początku hello hello strony toomanually pobierania hello pliku.</span><span class="sxs-lookup"><span data-stu-id="3fc67-237">hello file download begins automatically; if it does not, you can click hello link at hello beginning of hello page toomanually download hello file.</span></span> <span data-ttu-id="3fc67-238">Zapisz hello plików i Uwaga hello ścieżkę pliku.</span><span class="sxs-lookup"><span data-stu-id="3fc67-238">Save hello file and note hello file path.</span></span>
2. <span data-ttu-id="3fc67-239">Wprowadź następujące ustawienia hello tooimport polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="3fc67-239">Enter hello following command tooimport hello settings:</span></span>
   
        azure account import <path-to-file>
   
    <span data-ttu-id="3fc67-240">Podaj nazwę i ścieżka pliku hello hello publikowania w poprzednim kroku hello pobranego pliku ustawień.</span><span class="sxs-lookup"><span data-stu-id="3fc67-240">Specify hello path and file name of hello publishing settings file you downloaded in hello previous step.</span></span>
3. <span data-ttu-id="3fc67-241">Zaimportowane ustawienia hello usunąć hello pliku ustawień publikowania.</span><span class="sxs-lookup"><span data-stu-id="3fc67-241">After hello settings are imported, delete hello publish settings file.</span></span> <span data-ttu-id="3fc67-242">Nie jest już potrzebne i zawiera poufne informacje dotyczące subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3fc67-242">It is no longer needed, and contains sensitive information regarding your Azure subscription.</span></span>

### <a name="create-an-app-service-web-app"></a><span data-ttu-id="3fc67-243">Tworzenie aplikacji sieci web usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="3fc67-243">Create an App Service web app</span></span>
1. <span data-ttu-id="3fc67-244">Z wiersza polecenia hello, zmień katalogi toohello **tasklist** katalogu.</span><span class="sxs-lookup"><span data-stu-id="3fc67-244">From hello command-line, change directories toohello **tasklist** directory.</span></span>
2. <span data-ttu-id="3fc67-245">Użyj hello następujące polecenia toocreate nowej aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="3fc67-245">Use hello following command toocreate a new web app.</span></span>
   
        azure site create --git
   
    <span data-ttu-id="3fc67-246">Pojawi się monit dla nazwy aplikacji sieci web hello i lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="3fc67-246">You will be prompted for hello web app name and location.</span></span> <span data-ttu-id="3fc67-247">Podaj unikatową nazwę i wybierz hello tej samej lokalizacji geograficznej co konto magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="3fc67-247">Provide a unique name and select hello same geographical location as your Azure Storage account.</span></span>
   
    <span data-ttu-id="3fc67-248">Witaj `--git` parametru tworzy repozytorium Git na platformie Azure dla tej aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="3fc67-248">hello `--git` parameter creates a Git repository on Azure for this web app.</span></span> <span data-ttu-id="3fc67-249">Inicjuje również repozytorium Git w bieżącym katalogu hello Jeśli brak istnieje i dodaje [zdalnego Git] o nazwie "azure", która jest tooAzure aplikacji hello toopublish używane.</span><span class="sxs-lookup"><span data-stu-id="3fc67-249">It also initializes a Git repository in hello current directory if none exists, and adds a [Git remote] named 'azure', which is used toopublish hello application tooAzure.</span></span> <span data-ttu-id="3fc67-250">Na koniec tworzy **web.config** pliku, który zawiera ustawienia używane przez aplikacje węzła toohost platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3fc67-250">Finally, it creates a **web.config** file, which contains settings used by Azure toohost node applications.</span></span> <span data-ttu-id="3fc67-251">W przypadku pominięcia hello `--git` parametr, ale hello katalog zawiera repozytorium Git, polecenie hello nadal utworzy zdalnego hello "azure".</span><span class="sxs-lookup"><span data-stu-id="3fc67-251">If you omit hello `--git` parameter but hello directory contains a Git repository, hello command will still create hello 'azure' remote.</span></span>
   
    <span data-ttu-id="3fc67-252">Po ukończeniu tego polecenia, zostanie wyświetlone dane wyjściowe podobne toohello poniżej.</span><span class="sxs-lookup"><span data-stu-id="3fc67-252">Once this command has completed, you will see output similar toohello following.</span></span> <span data-ttu-id="3fc67-253">Należy pamiętać, że powitania od wiersza z **witryny sieci Web utworzonego w dniu** zawiera adres URL hello hello aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="3fc67-253">Note that hello line beginning with **Website created at** contains hello URL for hello web app.</span></span>
   
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
   > <span data-ttu-id="3fc67-254">Jeśli jest to hello pierwszej aplikacji usługi aplikacji sieci web dla Twojej subskrypcji, będzie aplikacji sieci web hello toocreate instrukcją toouse hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="3fc67-254">If this is hello first App Service web app for your subscription, you will be instructed toouse hello Azure Portal toocreate hello web app.</span></span> <span data-ttu-id="3fc67-255">Aby uzyskać więcej informacji, zobacz [tworzenia i wdrażania aplikacji sieci web Node.js w usłudze Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="3fc67-255">For more information, see [Build and deploy a Node.js web app in Azure App Service].</span></span>
   > 
   > 

### <a name="set-environment-variables"></a><span data-ttu-id="3fc67-256">Ustaw zmienne środowiskowe</span><span class="sxs-lookup"><span data-stu-id="3fc67-256">Set environment variables</span></span>
<span data-ttu-id="3fc67-257">W tym kroku zostaną dodane konfiguracji aplikacji sieci web tooyour zmienne środowiskowe na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="3fc67-257">In this step, you will add environment variables tooyour web app configuration on Azure.</span></span>
<span data-ttu-id="3fc67-258">Z wiersza polecenia hello wprowadź następujące hello:</span><span class="sxs-lookup"><span data-stu-id="3fc67-258">From hello command line, enter hello following:</span></span>

    azure site appsetting add
        STORAGE_NAME=<storage account name>;STORAGE_KEY=<storage access key>;PARTITION_KEY=mytasks;TABLE_NAME=tasks


<span data-ttu-id="3fc67-259">Zastąp  **<storage account name>**  o nazwie hello magazynu hello konta utworzonego wcześniej i Zastąp  **<storage access key>**  z hello podstawowy klucz dostępu dla konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="3fc67-259">Replace **<storage account name>** with hello name of hello storage account you created earlier, and replace **<storage access key>** with hello primary access key for your storage account.</span></span> <span data-ttu-id="3fc67-260">(Użyj hello takie same wartości jak wcześniej utworzony plik config.json hello).</span><span class="sxs-lookup"><span data-stu-id="3fc67-260">(Use hello same values as hello config.json file that you created earlier.)</span></span>

<span data-ttu-id="3fc67-261">Alternatywnie można ustawić zmienne środowiskowe w hello [Azure Portal](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="3fc67-261">Alternatively, you can set environment variables in hello [Azure Portal](https://portal.azure.com/):</span></span>

1. <span data-ttu-id="3fc67-262">Otwarcie bloku aplikacji sieci web hello klikając **Przeglądaj** > **aplikacje sieci Web** > Nazwa aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="3fc67-262">Open hello web app's blade by clicking **Browse** > **Web Apps** > your web app name.</span></span>
2. <span data-ttu-id="3fc67-263">W bloku aplikacja sieci web, kliknij przycisk **wszystkie ustawienia** > **ustawienia aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="3fc67-263">In your web app's blade, click **All Settings** > **Application Settings**.</span></span>
   
     <!-- ![Top Menu](./media/storage-nodejs-use-table-storage-web-site/PollsCommonWebSiteTopMenu.png) -->
3. <span data-ttu-id="3fc67-264">Przewiń w dół toohello **ustawień aplikacji** i Dodaj hello pary klucz wartość.</span><span class="sxs-lookup"><span data-stu-id="3fc67-264">Scroll down toohello **App settings** section and add hello key/value pairs.</span></span>
   
     ![Ustawienia aplikacji](./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png)
4. <span data-ttu-id="3fc67-266">Kliknij przycisk **SAVE** (Zapisz).</span><span class="sxs-lookup"><span data-stu-id="3fc67-266">Click **SAVE**.</span></span>

### <a name="publish-hello-application"></a><span data-ttu-id="3fc67-267">Publikowanie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="3fc67-267">Publish hello application</span></span>
<span data-ttu-id="3fc67-268">Aplikacja hello toopublish, zatwierdzić tooGit plików kodu hello, a następnie Wypchnij tooazure/główną.</span><span class="sxs-lookup"><span data-stu-id="3fc67-268">toopublish hello app, commit hello code files tooGit and then push tooazure/master.</span></span>

1. <span data-ttu-id="3fc67-269">Ustaw poświadczenia wdrażania.</span><span class="sxs-lookup"><span data-stu-id="3fc67-269">Set your deployment credentials.</span></span>
   
        azure site deployment user set <name> <password>
2. <span data-ttu-id="3fc67-270">Dodaj i zatwierdź plików aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3fc67-270">Add and commit your application files.</span></span>
   
        git add .
        git commit -m "adding files"
3. <span data-ttu-id="3fc67-271">Wypchnij hello zatwierdzania toohello aplikacji sieci web usługi aplikacji:</span><span class="sxs-lookup"><span data-stu-id="3fc67-271">Push hello commit toohello App Service web app:</span></span>
   
        git push azure master
   
    <span data-ttu-id="3fc67-272">Użyj **wzorca** jako hello gałęzi docelowej.</span><span class="sxs-lookup"><span data-stu-id="3fc67-272">Use **master** as hello target branch.</span></span> <span data-ttu-id="3fc67-273">Na końcu hello hello wdrożenia zobacz temat instrukcji toohello podobne, poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="3fc67-273">At hello end of hello deployment, you see a statement similar toohello following example:</span></span>
   
        toohttps://username@tabletasklist.azurewebsites.net/TableTasklist.git
          * [new branch]      master -> master
4. <span data-ttu-id="3fc67-274">Po zakończeniu operacji push hello Przeglądaj URL aplikacji sieci web toohello wcześniej zwrócony przez hello `azure create site` polecenia tooview aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3fc67-274">Once hello push operation has completed, browse toohello web app URL returned previously by hello `azure create site` command tooview your application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3fc67-275">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3fc67-275">Next steps</span></span>
<span data-ttu-id="3fc67-276">Gdy hello w tym artykule opisano przy użyciu informacji o toostore usługi tabel hello, można również użyć [MongoDB](https://mlab.com/azure/).</span><span class="sxs-lookup"><span data-stu-id="3fc67-276">While hello steps in this article describe using hello Table Service toostore information, you can also use [MongoDB](https://mlab.com/azure/).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3fc67-277">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="3fc67-277">Additional resources</span></span>
<span data-ttu-id="3fc67-278">[interfejsu wiersza polecenia Azure]</span><span class="sxs-lookup"><span data-stu-id="3fc67-278">[Azure CLI]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="3fc67-279">Co zostało zmienione</span><span class="sxs-lookup"><span data-stu-id="3fc67-279">What's changed</span></span>
* <span data-ttu-id="3fc67-280">Toohello przewodnik zmiany z tooApp witryn sieci Web usługi dla: [usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="3fc67-280">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- URLs -->

[tworzenia i wdrażania aplikacji sieci web Node.js w usłudze Azure App Service]: app-service-web-get-started-nodejs.md
[Azure Developer Center]: /develop/nodejs/

[węzła]: http://nodejs.org
[Git]: http://git-scm.com
[Express]: http://expressjs.com
[for free]: http://windowsazure.com
[zdalnego Git]: http://git-scm.com/docs/git-remote

[interfejsu wiersza polecenia Azure]:../cli-install-nodejs.md

[azure]: https://github.com/Azure/azure-sdk-for-node
[uuid węzła]: https://www.npmjs.com/package/node-uuid
[nconf]: https://www.npmjs.com/package/nconf
[async]: https://www.npmjs.com/package/async

[Azure Portal]: https://portal.azure.com

[Create and deploy a Node.js application tooan Azure Web Site]: app-service-web-get-started-nodejs.md

<!-- Image References -->

[node-table-finished]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_empty.png
[node-table-list-items]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_list.png
[download-publishing-settings]: ./media/storage-nodejs-use-table-storage-web-site/azure-account-download-cli.png
[portal-storage-access-keys]: ./media/storage-nodejs-use-table-storage-web-site/manage-access-keys.png
[app-settings]: ./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png
