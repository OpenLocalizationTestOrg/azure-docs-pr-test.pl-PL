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
# <a name="create-a-mongodb-express-angularjs-and-nodejs-mean-stack-on-a-linux-vm-in-azure"></a>Tworzenie stosu bazy danych MongoDB, Express AngularJS i Node.js (średnia) na maszynie Wirtualnej systemu Linux na platformie Azure

Ten samouczek pokazuje, jak stosu tooimplement bazy danych MongoDB, Express AngularJS i Node.js (średnia) na maszynie Wirtualnej systemu Linux na platformie Azure. stos średniej Hello utworzonego umożliwia dodawanie, usuwanie i wyświetlanie listy książek w bazie danych. Omawiane kwestie:

> [!div class="checklist"]
> * Tworzenie maszyny wirtualnej z systemem Linux
> * Instalowanie środowiska Node.js
> * Instalowanie bazy danych MongoDB i konfigurowanie powitania serwera
> * Zainstaluj Express i konfigurowanie serwera toohello tras
> * Dostęp hello tras z AngularJS
> * Uruchamianie aplikacji hello

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym samouczku wymaga działają hello Azure CLI w wersji 2.0.4 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).


## <a name="create-a-linux-vm"></a>Tworzenie maszyny wirtualnej z systemem Linux

Utwórz grupę zasobów o hello [Tworzenie grupy az](https://docs.microsoft.com/cli/azure/group#create) polecenie i Utwórz Maszynę wirtualną systemu Linux z hello [tworzenia maszyny wirtualnej az](https://docs.microsoft.com/cli/azure/vm#create) polecenia. Grupa zasobów platformy Azure to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi.

Witaj poniższym przykładzie użyto hello Azure CLI toocreate grupę zasobów o nazwie *myResourceGroupMEAN* w hello *eastus* lokalizacji. Maszyna wirtualna jest tworzony o nazwie *myVM* z kluczy SSH, jeśli nie już istnieją w domyślnej lokalizacji klucza. toouse określony zestaw kluczy, użyj hello — opcja ssh klucz wartość.

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

Podczas tworzenia maszyny Wirtualnej hello hello Azure CLI pokazuje informacje toohello podobnie poniższy przykład: 

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
Zwróć uwagę na powitania `publicIpAddress`. Ten adres jest używany tooaccess hello maszyny Wirtualnej.

Użyj hello następujące polecenie toocreate jako sesji SSH z hello maszyny Wirtualnej. Upewnij się, toouse hello poprawne publicznego adresu IP. W naszym przykładzie powyżej naszych IP adres był 13.72.77.9.

```bash
ssh azureuser@13.72.77.9
```

## <a name="install-nodejs"></a>Instalowanie środowiska Node.js

[Node.js](https://nodejs.org/en/) jest oparty na jego Chrome V8 JavaScript aparatu środowiska wykonawczego języka JavaScript. Node.js jest używany podczas tego samouczka tooset powitalne Express trasy i kontrolery AngularJS.

Na powitania maszyny Wirtualnej za pomocą powłoki bash hello, który został otwarty przy użyciu protokołu SSH zainstaluj środowisko Node.js.

```bash
sudo apt-get install -y nodejs
```

## <a name="install-mongodb-and-set-up-hello-server"></a>Instalowanie bazy danych MongoDB i konfigurowanie powitania serwera
[Bazy danych MongoDB](http://www.mongodb.com) przechowuje dane w dokumentach elastyczną i notacji JSON. Pola w bazie danych może się różnić od toodocument dokumentu i struktury danych można zmienić w czasie. Dla naszej aplikacji przykład dodajemy tooMongoDB rekordów książki, zawierające nazwa, numer isbn, autora i liczba stron. 

1. Na powitania maszyny Wirtualnej za pomocą powłoki bash hello, który został otwarty przy użyciu protokołu SSH należy ustawić klucz bazy danych MongoDB hello.

    ```bash
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6
    echo "deb [ arch=amd64 ] http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list
    ```

2. Menedżer pakietów hello aktualizacji z kluczem hello.
  
    ```bash
    sudo apt-get update
    ```

3. Instalowanie bazy danych MongoDB.

    ```bash
    sudo apt-get install -y mongodb
    ```

4. Uruchom serwer hello.

    ```bash
    sudo service mongodb start
    ```

5. Potrzebujemy tooinstall hello [analizator treści](https://www.npmjs.com/package/body-parser-json) toohelp pakietu nam hello JSON przekazano żądań toohello serwera przetwarzania.

    Zainstaluj Menedżera pakietów npm hello.

    ```bash
    sudo apt-get install npm
    ```

    Zainstaluj pakiet analizator treści hello.
    
    ```bash
    sudo npm install body-parser
    ```

6. Utwórz folder o nazwie *książki* i Dodaj tooit pliku o nazwie *server.js* zawierający konfiguracji hello hello przez serwer sieci web.

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

## <a name="install-express-and-set-up-routes-toohello-server"></a>Zainstaluj Express i konfigurowanie serwera toohello tras

[Express](https://expressjs.com) jest minimalną i elastyczną Node.js platforma aplikacji sieci web zapewniająca funkcje sieci web i aplikacji dla urządzeń przenośnych. Express jest używany podczas tego samouczka toopass książki informacji tooand z naszej bazy danych MongoDB. [Mongoose](http://mongoosejs.com) zapewnia toomodel proste, na podstawie schematu rozwiązanie dla danych aplikacji. Mongoose jest używana w tym samouczku tooprovide schemat książki hello bazy danych.

1. Zainstaluj Express i Mongoose.

    ```bash
    sudo npm install express mongoose
    ```

2. W hello *książki* folderu, Utwórz folder o nazwie *aplikacje* i Dodaj plik o nazwie *routes.js* z hello express trasy zdefiniowane.

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

3. W hello *aplikacje* folderu, Utwórz folder o nazwie *modele* i Dodaj plik o nazwie *book.js* z konfiguracją modelu książki hello zdefiniowane.  

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

## <a name="access-hello-routes-with-angularjs"></a>Dostęp hello tras z AngularJS

[AngularJS](https://angularjs.org) zapewnia platformę sieci web do tworzenia dynamicznych widoków w aplikacji sieci web. W tym samouczku firma Microsoft za pomocą AngularJS tooconnect naszą stronę sieci web Express i wykonywać działania na naszych książki bazy danych.

1. Zmień katalog hello Utwórz kopię zapasową za*— książki* (`cd ../..`), a następnie utwórz folder o nazwie *publicznego* i Dodaj plik o nazwie *script.js* z kontrolerem hello Konfiguracja zdefiniowane.

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
    
2. W hello *publicznego* folderu, Utwórz plik o nazwie *index.html* hello strony sieci web zdefiniowany.

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

##  <a name="run-hello-application"></a>Uruchamianie aplikacji hello

1. Zmień katalog hello Utwórz kopię zapasową za*książki* (`cd ..`) i uruchomić powitania serwera, uruchamiając polecenie:

    ```bash
    nodejs server.js
    ```

2. Otwórz adres toohello przeglądarki sieci web zapisane dla hello maszyny Wirtualnej. Na przykład *http://13.72.77.9:3300*. Powinny zostać wyświetlone informacje takie jak hello następujące strony:

    ![Rekord książki](media/tutorial-mean/meanstack-init.png)

3. Wprowadź dane do pól tekstowych hello, a następnie kliknij przycisk **Dodaj**. Na przykład:

    ![Dodaj rekord książki](media/tutorial-mean/meanstack-add.png)

4. Po odświeżeniu strony hello, powinien zostać wyświetlony ekran podobny do tej strony:

    ![Lista rekordów książki](media/tutorial-mean/meanstack-list.png)

5. Można kliknąć przycisk **usunąć** i usuwania rekordu książki hello z hello bazy danych.

## <a name="next-steps"></a>Następne kroki

W tym samouczku, utworzyć aplikacji sieci web, który śledzi książki rekordów przy użyciu średniej stosu na maszynie Wirtualnej systemu Linux. W tym samouczku omówiono:

> [!div class="checklist"]
> * Tworzenie maszyny wirtualnej z systemem Linux
> * Instalowanie środowiska Node.js
> * Instalowanie bazy danych MongoDB i konfigurowanie powitania serwera
> * Zainstaluj Express i konfigurowanie serwera toohello tras
> * Dostęp hello tras z AngularJS
> * Uruchamianie aplikacji hello

Jak przejść dalej toolearn samouczka toohello toosecure serwerów sieci web z certyfikatów SSL.

> [!div class="nextstepaction"]
> [Zabezpieczenia serwera sieci web przy użyciu protokołu SSL](tutorial-secure-web-server.md)
