---
title: "aaaConnect tooAzure aplikacji bazy danych MongoDB rozwiązania Cosmos bazy danych przy użyciu środowiska Node.js | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconnect istniejących aplikacji Node.js bazy danych MongoDB tooAzure DB rozwiązania Cosmos"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 06/19/2017
ms.author: mimig
ms.openlocfilehash: 4bc4f17a31d8c18d1ce5e3f002462f4d48eeb1f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-migrate-an-existing-nodejs-mongodb-web-app"></a>Azure Cosmos DB: migracja istniejącej aplikacji sieci Web MongoDB w środowisku Node.js 

Azure Cosmos DB to rozproszona globalnie wielomodelowa usługa bazy danych firmy Microsoft. Można szybko utworzyć i wyszukiwać dokumentu, klucza i wartości i wykres baz danych, które korzystają z dystrybucji globalne hello i możliwości skalowanie w poziomie na podstawowe hello Azure DB rozwiązania Cosmos. 

Ta opcja szybkiego startu przedstawia sposób toouse istniejące [MongoDB](mongodb-introduction.md) aplikacji napisanych w Node.js i podłącz go bazy danych Azure DB rozwiązania Cosmos tooyour, która obsługuje połączenia klienta bazy danych MongoDB. Innymi słowy aplikację Node.js tylko wie, że nawiązuje połączenie tooa bazy danych przy użyciu interfejsów API bazy danych MongoDB. Jest niewidoczne toohello aplikacji hello dane są przechowywane w usłudze Azure DB rozwiązania Cosmos.

Gdy wszystko będzie gotowe, aplikacja MEAN (MongoDB, Express, AngularJS i Node.js) będzie uruchomiona dla bazy danych [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/). 

![Aplikacja MEAN.js uruchomiona w usłudze Azure App Service](./media/create-mongodb-nodejs/meanjs-in-azure.png)


[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="prerequisites"></a>Wymagania wstępne 
Ponadto tooAzure interfejsu wiersza polecenia, należy [Node.js](https://nodejs.org/) i [Git](http://www.git-scm.com/downloads) zainstalowane lokalnie toorun `npm` i `git` poleceń.

Niezbędna jest praktyczna wiedza na temat Node.js. Ta opcja szybkiego startu nie jest zamierzone toohelp z ogólnie opracowywanie aplikacji Node.js.

## <a name="clone-hello-sample-application"></a>Klonowanie hello przykładowej aplikacji

Otwórz okno terminala git, np. git bash, i `cd` tooa katalog roboczy.  

Hello uruchom następujące polecenia tooclone hello próbki repozytorium. To repozytorium przykładowej zawiera domyślne hello [MEAN.js](http://meanjs.org/) aplikacji. 

```bash
git clone https://github.com/prashanthmadi/mean
```

## <a name="run-hello-application"></a>Uruchamianie aplikacji hello

Instalowanie pakietów hello wymagane, a następnie uruchom aplikację hello.

```bash
cd mean
npm install
npm start
```

## <a name="log-in-tooazure"></a>Zaloguj się za tooAzure

Jeśli używane są zainstalowane wiersza polecenia platformy Azure, zaloguj się za tooyour subskrypcji platformy Azure z hello [logowania az](/cli/azure/#login) poleceń i wykonaj hello wyświetlanymi instrukcjami. Ten krok można pominąć, jeśli używasz hello powłoki chmury Azure.

```azurecli
az login 
``` 
   
## <a name="add-hello-azure-cosmos-db-module"></a>Dodaj moduł Azure DB rozwiązania Cosmos hello

Jeśli używane są zainstalowane wiersza polecenia platformy Azure, określ, czy toosee hello `cosmosdb` uruchamiając hello jest już zainstalowany składnik `az` polecenia. Jeśli `cosmosdb` jest hello listy poleceń podstawowej, kontynuować toohello następnego polecenia. Ten krok można pominąć, jeśli używasz hello powłoki chmury Azure.

Jeśli `cosmosdb` nie jest w hello listę poleceń, podstawowe, należy ponownie zainstalować [Azure CLI 2.0]( /cli/azure/install-azure-cli).

## <a name="create-a-resource-group"></a>Tworzenie grupy zasobów

Utwórz [grupy zasobów](../azure-resource-manager/resource-group-overview.md) z hello [Tworzenie grupy az](/cli/azure/group#create). Grupa zasobów platformy Azure to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure, takich jak aplikacje sieci Web, bazy danych i konta magazynu, oraz zarządzania nimi. 

Witaj poniższy przykład tworzy grupę zasobów w regionie Europy Zachodniej hello. Wybierz unikatową nazwę grupy zasobów hello.

Jeśli korzystasz z powłoki chmury Azure, kliknij przycisk **spróbuj on**, wykonaj toologin wyświetlanymi na ekranie powitania, a następnie skopiuj hello polecenie w wierszu polecenia hello.

```azurecli-interactive
az group create --name myResourceGroup --location "West Europe"
```

## <a name="create-an-azure-cosmos-db-account"></a>Tworzenie konta usługi Azure Cosmos DB

Tworzenie konta bazy danych Azure rozwiązania Cosmos z hello [az cosmosdb utworzyć](/cli/azure/cosmosdb#create) polecenia.

W hello następujące polecenia, należy zastąpić własną unikatową nazwę konta bazy danych Azure rozwiązania Cosmos której występuje hello `<cosmosdb-name>` symbolu zastępczego. Ta nazwa będzie służyć jako część bazy danych Azure rozwiązania Cosmos punktu końcowego (`https://<cosmosdb-name>.documents.azure.com/`), więc nazwa hello musi toobe unikatowy wszystkich kont Azure DB rozwiązania Cosmos na platformie Azure. 

```azurecli-interactive
az cosmosdb create --name <cosmosdb-name> --resource-group myResourceGroup --kind MongoDB
```

Witaj `--kind MongoDB` parametru zapewnia połączeń klienckich bazy danych MongoDB.

Po utworzeniu konta bazy danych Azure rozwiązania Cosmos hello hello Azure CLI pokazuje informacje toohello podobnie poniższy przykład. 

> [!NOTE]
> W tym przykładzie używane JSON jako hello Azure CLI format wyjściowy hello domyślne. toouse output inny format, zobacz [formatów poleceń Azure CLI 2.0](https://docs.microsoft.com/cli/azure/format-output-azure-cli).

```json
{
  "databaseAccountOfferType": "Standard",
  "documentEndpoint": "https://<cosmosdb-name>.documents.azure.com:443/",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Document
DB/databaseAccounts/<cosmosdb-name>",
  "kind": "MongoDB",
  "location": "West Europe",
  "name": "<cosmosdb-name>",
  "readLocations": [
    {
      "documentEndpoint": "https://<cosmosdb-name>-westeurope.documents.azure.com:443/",
      "failoverPriority": 0,
      "id": "<cosmosdb-name>-westeurope",
      "locationName": "West Europe",
      "provisioningState": "Succeeded"
    }
  ],
  "resourceGroup": "myResourceGroup",
  "type": "Microsoft.DocumentDB/databaseAccounts",
  "writeLocations": [
    {
      "documentEndpoint": "https://<cosmosdb-name>-westeurope.documents.azure.com:443/",
      "failoverPriority": 0,
      "id": "<cosmosdb-name>-westeurope",
      "locationName": "West Europe",
      "provisioningState": "Succeeded"
    }
  ]
} 
```

## <a name="connect-your-nodejs-application-toohello-database"></a>Połączenia bazy danych toohello aplikacji Node.js

W tym kroku połączenie MEAN.js przykładowej bazy danych aplikacji tooan bazy danych Azure rozwiązania Cosmos utworzony, przy użyciu parametrów połączenia bazy danych MongoDB. 

<a name="devconfig"></a>
## <a name="configure-hello-connection-string-in-your-nodejs-application"></a>Konfigurowanie parametrów połączenia hello w aplikacji Node.js

W repozytorium MEAN.js otwórz plik `config/env/local-development.js`.

Zastąp hello następującego kodu hello zawartości tego pliku. Tooalso Zastąp hello dwa upewnij się, `<cosmosdb-name>` symbole zastępcze nazwą konta bazy danych Azure rozwiązania Cosmos.

```javascript
'use strict';

module.exports = {
  db: {
    uri: 'mongodb://<cosmosdb-name>:<primary_master_key>@<cosmosdb-name>.documents.azure.com:10255/mean-dev?ssl=true&sslverifycertificate=false'
  }
};
```

## <a name="retrieve-hello-key"></a>Pobierz klucz hello

W kolejności tooconnect tooan bazy danych Azure rozwiązania Cosmos bazy danych należy hello klucza bazy danych. Użyj hello [az cosmosdb listy kluczy](/cli/azure/cosmosdb#list-keys) klucz podstawowy hello tooretrieve polecenia.

```azurecli-interactive
az cosmosdb list-keys --name <cosmosdb-name> --resource-group myResourceGroup --query "primaryMasterKey"
```

Hello Azure CLI generuje informacje toohello podobnie poniższy przykład. 

```json
"RUayjYjixJDWG5xTqIiXjC..."
```

Skopiuj wartość hello `primaryMasterKey`. Wklej to za pośrednictwem hello `<primary_master_key>` w `local-development.js`.

Zapisz zmiany.

### <a name="run-hello-application-again"></a>Uruchom ponownie aplikację hello.

Uruchom ponownie polecenie `npm start`. 

```bash
npm start
```

Komunikat konsoli powinna teraz informujące, że środowisko projektowe hello jest uruchomiona. 

Przejdź do zbyt`http://localhost:3000` w przeglądarce. Kliknij przycisk **Utwórz konto** w górnego menu i spróbuj toocreate hello fikcyjny dwóch użytkowników. 

Witaj MEAN.js Przykładowa aplikacja przechowuje dane użytkownika w bazie danych hello. Jeśli pomyślnie i MEAN.js automatycznie zaloguje się do hello utworzony użytkownik, a następnie połączenie bazy danych Azure rozwiązania Cosmos działa. 

![MEAN.js pomyślnie łączy tooMongoDB](./media/create-mongodb-nodejs/mongodb-connect-success.png)

## <a name="view-data-in-data-explorer"></a>Wyświetlanie danych w Eksploratorze danych

Dane przechowywane przez bazy danych Azure rozwiązania Cosmos jest dostępne tooview, zapytań i wykonywania logiki biznesowej w w hello portalu Azure.

tooview, zapytań i pracować z danymi użytkownika hello utworzone hello poprzedniego kroku, logowania toohello [portalu Azure](https://portal.azure.com) w przeglądarce sieci web.

W polu wyszukiwania górnego hello wpisz bazy danych Azure rozwiązania Cosmos. Po otwarciu bloku konta usługi Cosmos DB wybierz swoje konto usługi Cosmos DB. W hello lewy pasek nawigacyjny kliknij przycisk Eksploratora danych. Rozwiń w okienku Kolekcje hello kolekcji, a następnie można wyświetlać dokumenty hello w kolekcji hello, dane hello kwerendy i nawet utworzyć i uruchomić procedur składowanych, wyzwalaczy i funkcji UDF. 

![Eksplorator danych w hello portalu Azure](./media/create-mongodb-nodejs/cosmosdb-connect-mongodb-data-explorer.png)


## <a name="deploy-hello-nodejs-application-tooazure"></a>Wdrażanie tooAzure aplikacji Node.js hello

W tym kroku możesz wdrożyć tooAzure aplikacji programu Node.js połączenia bazy danych MongoDB DB rozwiązania Cosmos.

Można zauważyć czy plik konfiguracyjny hello, który został zmodyfikowany wcześniej jest przeznaczony dla środowiska deweloperskiego hello (`/config/env/local-development.js`). Podczas wdrażania tooApp Twojej aplikacji usługi, domyślnie jest uruchamiana w środowisku produkcyjnym hello. Dlatego teraz należy toomake hello same zmiany toohello odpowiednich konfiguracji pliku.

W repozytorium MEAN.js otwórz plik `config/env/production.js`.

W hello `db` obiektów, zastąp wartość hello `uri` jako Pokaż w hello poniższy przykład. Należy się tooreplace hello symbole zastępcze jako przed.

```javascript
'mongodb://<cosmosdb-name>:<primary_master_key>@<cosmosdb-name>.documents.azure.com:10255/mean?ssl=true&sslverifycertificate=false',
```

> [!NOTE] 
> Witaj `ssl=true` opcji ważne jest, ponieważ [bazy danych rozwiązania Cosmos Azure wymaga protokołu SSL](connect-mongodb-account.md#connection-string-requirements). 
>
>

W terminalu hello Zatwierdź wszystkie zmiany do Git. Możesz kopiować zarówno toorun polecenia je razem.

```bash
git add .
git commit -m "configured MongoDB connection string"
```
## <a name="clean-up-resources"></a>Oczyszczanie zasobów

Jeśli nie będzie toocontinue toouse tej aplikacji, należy usunąć wszystkie zasoby utworzone przez tego przewodnika Szybki Start w hello portalu Azure z hello następujące kroki:

1. Z menu po lewej stronie powitania w hello portalu Azure, kliknij przycisk **grup zasobów** a następnie kliknij nazwę hello zasobu hello został utworzony. 
2. Na stronie grupy zasobów, kliknij przycisk **usunąć**, wpisz nazwę hello toodelete zasobów hello w polu tekstowym hello, a następnie kliknij **usunąć**.

## <a name="next-steps"></a>Następne kroki

W tym szybkiego startu, kiedy znasz już jak toocreate bazy danych Azure rozwiązania Cosmos konta, a następnie utwórz kolekcję bazy danych MongoDB przy użyciu hello Eksploratora danych. Teraz można migrować tooAzure danych z bazy danych MongoDB DB rozwiązania Cosmos.  

> [!div class="nextstepaction"]
> [Importowanie danych z bazy danych MongoDB do usługi Azure Cosmos DB](mongodb-migrate.md)
