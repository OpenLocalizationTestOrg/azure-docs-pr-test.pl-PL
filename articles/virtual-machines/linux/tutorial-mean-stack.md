---
title: "aaaCreate średniej stosu na maszynie Wirtualnej systemu Linux na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak stosu toocreate bazy danych MongoDB, Express AngularJS i Node.js (średnia) na maszynie Wirtualnej systemu Linux na platformie Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/08/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 82a8e34e60d2bb6e6670ee007faa1113ea78b716
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-mongodb-express-angularjs-and-nodejs-mean-stack-on-a-linux-vm-in-azure"></a><span data-ttu-id="80860-103">Tworzenie stosu bazy danych MongoDB, Express AngularJS i Node.js (średnia) na maszynie Wirtualnej systemu Linux na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="80860-103">Create a MongoDB, Express, AngularJS, and Node.js (MEAN) stack on a Linux VM in Azure</span></span>

<span data-ttu-id="80860-104">Ten samouczek pokazuje, jak stosu tooimplement bazy danych MongoDB, Express AngularJS i Node.js (średnia) na maszynie Wirtualnej systemu Linux na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="80860-104">This tutorial shows you how tooimplement a MongoDB, Express, AngularJS, and Node.js (MEAN) stack on a Linux VM in Azure.</span></span> <span data-ttu-id="80860-105">stos średniej Hello utworzonego umożliwia dodawanie, usuwanie i wyświetlanie listy książek w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="80860-105">hello MEAN stack that you create enables adding, deleting, and listing books in a database.</span></span> <span data-ttu-id="80860-106">Omawiane kwestie:</span><span class="sxs-lookup"><span data-stu-id="80860-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="80860-107">Tworzenie maszyny wirtualnej z systemem Linux</span><span class="sxs-lookup"><span data-stu-id="80860-107">Create a Linux VM</span></span>
> * <span data-ttu-id="80860-108">Instalowanie środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="80860-108">Install Node.js</span></span>
> * <span data-ttu-id="80860-109">Instalowanie bazy danych MongoDB i konfigurowanie powitania serwera</span><span class="sxs-lookup"><span data-stu-id="80860-109">Install MongoDB and set up hello server</span></span>
> * <span data-ttu-id="80860-110">Zainstaluj Express i konfigurowanie serwera toohello tras</span><span class="sxs-lookup"><span data-stu-id="80860-110">Install Express and set up routes toohello server</span></span>
> * <span data-ttu-id="80860-111">Dostęp hello tras z AngularJS</span><span class="sxs-lookup"><span data-stu-id="80860-111">Access hello routes with AngularJS</span></span>
> * <span data-ttu-id="80860-112">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="80860-112">Run hello application</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="80860-113">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym samouczku wymaga działają hello Azure CLI w wersji 2.0.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="80860-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="80860-114">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="80860-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="80860-115">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="80860-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>


## <a name="create-a-linux-vm"></a><span data-ttu-id="80860-116">Tworzenie maszyny wirtualnej z systemem Linux</span><span class="sxs-lookup"><span data-stu-id="80860-116">Create a Linux VM</span></span>

<span data-ttu-id="80860-117">Utwórz grupę zasobów o hello [Tworzenie grupy az](https://docs.microsoft.com/cli/azure/group#create) polecenie i Utwórz Maszynę wirtualną systemu Linux z hello [tworzenia maszyny wirtualnej az](https://docs.microsoft.com/cli/azure/vm#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="80860-117">Create a resource group with hello [az group create](https://docs.microsoft.com/cli/azure/group#create) command and create a Linux VM with hello [az vm create](https://docs.microsoft.com/cli/azure/vm#create) command.</span></span> <span data-ttu-id="80860-118">Grupa zasobów platformy Azure to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="80860-118">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="80860-119">Witaj poniższym przykładzie użyto hello Azure CLI toocreate grupę zasobów o nazwie *myResourceGroupMEAN* w hello *eastus* lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="80860-119">hello following example uses hello Azure CLI toocreate a resource group named *myResourceGroupMEAN* in hello *eastus* location.</span></span> <span data-ttu-id="80860-120">Maszyna wirtualna jest tworzony o nazwie *myVM* z kluczy SSH, jeśli nie już istnieją w domyślnej lokalizacji klucza.</span><span class="sxs-lookup"><span data-stu-id="80860-120">A VM is created named *myVM* with SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="80860-121">toouse określony zestaw kluczy, użyj hello — opcja ssh klucz wartość.</span><span class="sxs-lookup"><span data-stu-id="80860-121">toouse a specific set of keys, use hello --ssh-key-value option.</span></span>

```azurecli-interactive
az group create --name myResourceGroupMEAN --location eastus
az vm create \
    --resource-group myResourceGroupMEAN \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --admin-password 'Azure12345678!' \
    --generate-ssh-keys
az vm open-port --port 3300 --resource-group myResourceGroupMEAN --name myVM
```

<span data-ttu-id="80860-122">Podczas tworzenia maszyny Wirtualnej hello hello Azure CLI pokazuje informacje toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="80860-122">When hello VM has been created, hello Azure CLI shows information similar toohello following example:</span></span> 

```azurecli-interactive
{
  "fqdns": "",
  "id": "/subscriptions/{subscription-id}/resourceGroups/myResourceGroupMEAN/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "13.72.77.9",
  "resourceGroup": "myResourceGroupMEAN"
}
```
<span data-ttu-id="80860-123">Zwróć uwagę na powitania `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="80860-123">Take note of hello `publicIpAddress`.</span></span> <span data-ttu-id="80860-124">Ten adres jest używany tooaccess hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="80860-124">This address is used tooaccess hello VM.</span></span>

<span data-ttu-id="80860-125">Użyj hello następujące polecenie toocreate jako sesji SSH z hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="80860-125">Use hello following command toocreate an SSH session with hello VM.</span></span> <span data-ttu-id="80860-126">Upewnij się, toouse hello poprawne publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="80860-126">Make sure toouse hello correct public IP address.</span></span> <span data-ttu-id="80860-127">W naszym przykładzie powyżej naszych IP adres był 13.72.77.9.</span><span class="sxs-lookup"><span data-stu-id="80860-127">In our example above our IP address was 13.72.77.9.</span></span>

```bash
ssh azureuser@13.72.77.9
```

## <a name="install-nodejs"></a><span data-ttu-id="80860-128">Instalowanie środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="80860-128">Install Node.js</span></span>

<span data-ttu-id="80860-129">[Node.js](https://nodejs.org/en/) jest oparty na jego Chrome V8 JavaScript aparatu środowiska wykonawczego języka JavaScript.</span><span class="sxs-lookup"><span data-stu-id="80860-129">[Node.js](https://nodejs.org/en/) is a JavaScript runtime built on Chrome's V8 JavaScript engine.</span></span> <span data-ttu-id="80860-130">Node.js jest używany podczas tego samouczka tooset powitalne Express trasy i kontrolery AngularJS.</span><span class="sxs-lookup"><span data-stu-id="80860-130">Node.js is used in this tutorial tooset up hello Express routes and AngularJS controllers.</span></span>

<span data-ttu-id="80860-131">Na powitania maszyny Wirtualnej za pomocą powłoki bash hello, który został otwarty przy użyciu protokołu SSH zainstaluj środowisko Node.js.</span><span class="sxs-lookup"><span data-stu-id="80860-131">On hello VM, using hello bash shell that you opened with SSH, install Node.js.</span></span>

```bash
sudo apt-get install -y nodejs
```

## <a name="install-mongodb-and-set-up-hello-server"></a><span data-ttu-id="80860-132">Instalowanie bazy danych MongoDB i konfigurowanie powitania serwera</span><span class="sxs-lookup"><span data-stu-id="80860-132">Install MongoDB and set up hello server</span></span>
<span data-ttu-id="80860-133">[Bazy danych MongoDB](http://www.mongodb.com) przechowuje dane w dokumentach elastyczną i notacji JSON.</span><span class="sxs-lookup"><span data-stu-id="80860-133">[MongoDB](http://www.mongodb.com) stores data in flexible, JSON-like documents.</span></span> <span data-ttu-id="80860-134">Pola w bazie danych może się różnić od toodocument dokumentu i struktury danych można zmienić w czasie.</span><span class="sxs-lookup"><span data-stu-id="80860-134">Fields in a database can vary from document toodocument and data structure can be changed over time.</span></span> <span data-ttu-id="80860-135">Dla naszej aplikacji przykład dodajemy tooMongoDB rekordów książki, zawierające nazwa, numer isbn, autora i liczba stron.</span><span class="sxs-lookup"><span data-stu-id="80860-135">For our example application, we are adding book records tooMongoDB that contain book name, isbn number, author, and number of pages.</span></span> 

1. <span data-ttu-id="80860-136">Na powitania maszyny Wirtualnej za pomocą powłoki bash hello, który został otwarty przy użyciu protokołu SSH należy ustawić klucz bazy danych MongoDB hello.</span><span class="sxs-lookup"><span data-stu-id="80860-136">On hello VM, using hello bash shell that you opened with SSH, set hello MongoDB key.</span></span>

    ```bash
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6
    echo "deb [ arch=amd64 ] http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list
    ```

2. <span data-ttu-id="80860-137">Menedżer pakietów hello aktualizacji z kluczem hello.</span><span class="sxs-lookup"><span data-stu-id="80860-137">Update hello package manager with hello key.</span></span>
  
    ```bash
    sudo apt-get update
    ```

3. <span data-ttu-id="80860-138">Instalowanie bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="80860-138">Install MongoDB.</span></span>

    ```bash
    sudo apt-get install -y mongodb
    ```

4. <span data-ttu-id="80860-139">Uruchom serwer hello.</span><span class="sxs-lookup"><span data-stu-id="80860-139">Start hello server.</span></span>

    ```bash
    sudo service mongodb start
    ```

5. <span data-ttu-id="80860-140">Potrzebujemy tooinstall hello [analizator treści](https://www.npmjs.com/package/body-parser-json) toohelp pakietu nam hello JSON przekazano żądań toohello serwera przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="80860-140">We also need tooinstall hello [body-parser](https://www.npmjs.com/package/body-parser-json) package toohelp us process hello JSON passed in requests toohello server.</span></span>

    <span data-ttu-id="80860-141">Zainstaluj Menedżera pakietów npm hello.</span><span class="sxs-lookup"><span data-stu-id="80860-141">Install hello npm package manager.</span></span>

    ```bash
    sudo apt-get install npm
    ```

    <span data-ttu-id="80860-142">Zainstaluj pakiet analizator treści hello.</span><span class="sxs-lookup"><span data-stu-id="80860-142">Install hello body parser package.</span></span>
    
    ```bash
    sudo npm install body-parser
    ```

6. <span data-ttu-id="80860-143">Utwórz folder o nazwie *książki* i Dodaj tooit pliku o nazwie *server.js* zawierający konfiguracji hello hello przez serwer sieci web.</span><span class="sxs-lookup"><span data-stu-id="80860-143">Create a folder named *Books* and add a file tooit named *server.js* that contains hello configuration for hello web server.</span></span>

    ```node.js
    var express = require('express');
    var bodyParser = require('body-parser');
    var app = express();
    app.use(express.static(__dirname + '/public'));
    app.use(bodyParser.json());
    require('./apps/routes')(app);
    app.set('port', 3300);
    app.listen(app.get('port'), function() {
        console.log('Server up: http://localhost:' + app.get('port'));
    });
    ```

## <a name="install-express-and-set-up-routes-toohello-server"></a><span data-ttu-id="80860-144">Zainstaluj Express i konfigurowanie serwera toohello tras</span><span class="sxs-lookup"><span data-stu-id="80860-144">Install Express and set up routes toohello server</span></span>

<span data-ttu-id="80860-145">[Express](https://expressjs.com) jest minimalną i elastyczną Node.js platforma aplikacji sieci web zapewniająca funkcje sieci web i aplikacji dla urządzeń przenośnych.</span><span class="sxs-lookup"><span data-stu-id="80860-145">[Express](https://expressjs.com) is a minimal and flexible Node.js web application framework that provides features for web and mobile applications.</span></span> <span data-ttu-id="80860-146">Express jest używany podczas tego samouczka toopass książki informacji tooand z naszej bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="80860-146">Express is used in this tutorial toopass book information tooand from our MongoDB database.</span></span> <span data-ttu-id="80860-147">[Mongoose](http://mongoosejs.com) zapewnia toomodel proste, na podstawie schematu rozwiązanie dla danych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="80860-147">[Mongoose](http://mongoosejs.com) provides a straight-forward, schema-based solution toomodel your application data.</span></span> <span data-ttu-id="80860-148">Mongoose jest używana w tym samouczku tooprovide schemat książki hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="80860-148">Mongoose is used in this tutorial tooprovide a book schema for hello database.</span></span>

1. <span data-ttu-id="80860-149">Zainstaluj Express i Mongoose.</span><span class="sxs-lookup"><span data-stu-id="80860-149">Install Express and Mongoose.</span></span>

    ```bash
    sudo npm install express mongoose
    ```

2. <span data-ttu-id="80860-150">W hello *książki* folderu, Utwórz folder o nazwie *aplikacje* i Dodaj plik o nazwie *routes.js* z hello express trasy zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="80860-150">In hello *Books* folder, create a folder named *apps* and add a file named *routes.js* with hello express routes defined.</span></span>

    ```node.js
    var Book = require('./models/book');
    module.exports = function(app) {
      app.get('/book', function(req, res) {
        Book.find({}, function(err, result) {
          if ( err ) throw err;
          res.json(result);
        });
      }); 
      app.post('/book', function(req, res) {
        var book = new Book( {
          name:req.body.name,
          isbn:req.body.isbn,
          author:req.body.author,
          pages:req.body.pages
        });
        book.save(function(err, result) {
          if ( err ) throw err;
          res.json( {
            message:"Successfully added book",
            book:result
          });
        });
      });
      app.delete("/book/:isbn", function(req, res) {
        Book.findOneAndRemove(req.query, function(err, result) {
          if ( err ) throw err;
          res.json( {
            message: "Successfully deleted hello book",
            book: result
          });
        });
      });
      var path = require('path');
      app.get('*', function(req, res) {
        res.sendfile(path.join(__dirname + '/public', 'index.html'));
      });
    };
    ```

3. <span data-ttu-id="80860-151">W hello *aplikacje* folderu, Utwórz folder o nazwie *modele* i Dodaj plik o nazwie *book.js* z konfiguracją modelu książki hello zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="80860-151">In hello *apps* folder, create a folder named *models* and add a file named *book.js* with hello book model configuration defined.</span></span>  

    ```node.js
    var mongoose = require('mongoose');
    var dbHost = 'mongodb://localhost:27017/test';
    mongoose.connect(dbHost);
    mongoose.connection;
    mongoose.set('debug', true);
    var bookSchema = mongoose.Schema( {
      name: String,
      isbn: {type: String, index: true},
      author: String,
      pages: Number
    });
    var Book = mongoose.model('Book', bookSchema);
    module.exports = mongoose.model('Book', bookSchema); 
    ```

## <a name="access-hello-routes-with-angularjs"></a><span data-ttu-id="80860-152">Dostęp hello tras z AngularJS</span><span class="sxs-lookup"><span data-stu-id="80860-152">Access hello routes with AngularJS</span></span>

<span data-ttu-id="80860-153">[AngularJS](https://angularjs.org) zapewnia platformę sieci web do tworzenia dynamicznych widoków w aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="80860-153">[AngularJS](https://angularjs.org) provides a web framework for creating dynamic views in your web applications.</span></span> <span data-ttu-id="80860-154">W tym samouczku firma Microsoft za pomocą AngularJS tooconnect naszą stronę sieci web Express i wykonywać działania na naszych książki bazy danych.</span><span class="sxs-lookup"><span data-stu-id="80860-154">In this tutorial, we use AngularJS tooconnect our web page with Express and perform actions on our book database.</span></span>

1. <span data-ttu-id="80860-155">Zmień katalog hello Utwórz kopię zapasową za*— książki* (`cd ../..`), a następnie utwórz folder o nazwie *publicznego* i Dodaj plik o nazwie *script.js* z kontrolerem hello Konfiguracja zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="80860-155">Change hello directory back up too*Books* (`cd ../..`), and then create a folder named *public* and add a file named *script.js* with hello controller configuration defined.</span></span>

    ```node.js
    var app = angular.module('myApp', []);
    app.controller('myCtrl', function($scope, $http) {
      $http( {
        method: 'GET',
        url: '/book'
      }).then(function successCallback(response) {
        $scope.books = response.data;
      }, function errorCallback(response) {
        console.log('Error: ' + response);
      });
      $scope.del_book = function(book) {
        $http( {
          method: 'DELETE',
          url: '/book/:isbn',
          params: {'isbn': book.isbn}
        }).then(function successCallback(response) {
          console.log(response);
        }, function errorCallback(response) {
          console.log('Error: ' + response);
        });
      };
      $scope.add_book = function() {
        var body = '{ "name": "' + $scope.Name + 
        '", "isbn": "' + $scope.Isbn +
        '", "author": "' + $scope.Author + 
        '", "pages": "' + $scope.Pages + '" }';
        $http({
          method: 'POST',
          url: '/book',
          data: body
        }).then(function successCallback(response) {
          console.log(response);
        }, function errorCallback(response) {
          console.log('Error: ' + response);
        });
      };
    });
    ```
    
2. <span data-ttu-id="80860-156">W hello *publicznego* folderu, Utwórz plik o nazwie *index.html* hello strony sieci web zdefiniowany.</span><span class="sxs-lookup"><span data-stu-id="80860-156">In hello *public* folder, create a file named *index.html* with hello web page defined.</span></span>

    ```html
    <!doctype html>
    <html ng-app="myApp" ng-controller="myCtrl">
      <head>
        <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.4/angular.min.js"></script>
        <script src="script.js"></script>
      </head>
      <body>
        <div>
          <table>
            <tr>
              <td>Name:</td> 
              <td><input type="text" ng-model="Name"></td>
            </tr>
            <tr>
              <td>Isbn:</td>
              <td><input type="text" ng-model="Isbn"></td>
            </tr>
            <tr>
              <td>Author:</td> 
              <td><input type="text" ng-model="Author"></td>
            </tr>
            <tr>
              <td>Pages:</td>
              <td><input type="number" ng-model="Pages"></td>
            </tr>
          </table>
          <button ng-click="add_book()">Add</button>
        </div>
        <hr>
        <div>
          <table>
            <tr>
              <th>Name</th>
              <th>Isbn</th>
              <th>Author</th>
              <th>Pages</th>
            </tr>
            <tr ng-repeat="book in books">
              <td><input type="button" value="Delete" data-ng-click="del_book(book)"></td>
              <td>{{book.name}}</td>
              <td>{{book.isbn}}</td>
              <td>{{book.author}}</td>
              <td>{{book.pages}}</td>
            </tr>
          </table>
        </div>
      </body>
    </html>
    ```

##  <a name="run-hello-application"></a><span data-ttu-id="80860-157">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="80860-157">Run hello application</span></span>

1. <span data-ttu-id="80860-158">Zmień katalog hello Utwórz kopię zapasową za*książki* (`cd ..`) i uruchomić powitania serwera, uruchamiając polecenie:</span><span class="sxs-lookup"><span data-stu-id="80860-158">Change hello directory back up too*Books* (`cd ..`) and start hello server by running this command:</span></span>

    ```bash
    nodejs server.js
    ```

2. <span data-ttu-id="80860-159">Otwórz adres toohello przeglądarki sieci web zapisane dla hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="80860-159">Open a web browser toohello address that you recorded for hello VM.</span></span> <span data-ttu-id="80860-160">Na przykład *http://13.72.77.9:3300*.</span><span class="sxs-lookup"><span data-stu-id="80860-160">For example, *http://13.72.77.9:3300*.</span></span> <span data-ttu-id="80860-161">Powinny zostać wyświetlone informacje takie jak hello następujące strony:</span><span class="sxs-lookup"><span data-stu-id="80860-161">You should see something like hello following page:</span></span>

    ![Rekord książki](media/tutorial-mean/meanstack-init.png)

3. <span data-ttu-id="80860-163">Wprowadź dane do pól tekstowych hello, a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="80860-163">Enter data into hello textboxes and click **Add**.</span></span> <span data-ttu-id="80860-164">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="80860-164">For example:</span></span>

    ![Dodaj rekord książki](media/tutorial-mean/meanstack-add.png)

4. <span data-ttu-id="80860-166">Po odświeżeniu strony hello, powinien zostać wyświetlony ekran podobny do tej strony:</span><span class="sxs-lookup"><span data-stu-id="80860-166">After refreshing hello page, you should see something like this page:</span></span>

    ![Lista rekordów książki](media/tutorial-mean/meanstack-list.png)

5. <span data-ttu-id="80860-168">Można kliknąć przycisk **usunąć** i usuwania rekordu książki hello z hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="80860-168">You could click **Delete** and remove hello book record from hello database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="80860-169">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="80860-169">Next steps</span></span>

<span data-ttu-id="80860-170">W tym samouczku, utworzyć aplikacji sieci web, który śledzi książki rekordów przy użyciu średniej stosu na maszynie Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="80860-170">In this tutorial, you created a web application that keeps track of book records using a MEAN stack on a Linux VM.</span></span> <span data-ttu-id="80860-171">W tym samouczku omówiono:</span><span class="sxs-lookup"><span data-stu-id="80860-171">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="80860-172">Tworzenie maszyny wirtualnej z systemem Linux</span><span class="sxs-lookup"><span data-stu-id="80860-172">Create a Linux VM</span></span>
> * <span data-ttu-id="80860-173">Instalowanie środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="80860-173">Install Node.js</span></span>
> * <span data-ttu-id="80860-174">Instalowanie bazy danych MongoDB i konfigurowanie powitania serwera</span><span class="sxs-lookup"><span data-stu-id="80860-174">Install MongoDB and set up hello server</span></span>
> * <span data-ttu-id="80860-175">Zainstaluj Express i konfigurowanie serwera toohello tras</span><span class="sxs-lookup"><span data-stu-id="80860-175">Install Express and set up routes toohello server</span></span>
> * <span data-ttu-id="80860-176">Dostęp hello tras z AngularJS</span><span class="sxs-lookup"><span data-stu-id="80860-176">Access hello routes with AngularJS</span></span>
> * <span data-ttu-id="80860-177">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="80860-177">Run hello application</span></span>

<span data-ttu-id="80860-178">Jak przejść dalej toolearn samouczka toohello toosecure serwerów sieci web z certyfikatów SSL.</span><span class="sxs-lookup"><span data-stu-id="80860-178">Advance toohello next tutorial toolearn how toosecure web servers with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="80860-179">Zabezpieczenia serwera sieci web przy użyciu protokołu SSL</span><span class="sxs-lookup"><span data-stu-id="80860-179">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)
