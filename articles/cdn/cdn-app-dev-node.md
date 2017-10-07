---
title: "aaaGet wprowadzenie hello Azure CDN SDK dla środowiska Node.js | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomanage aplikacji Node.js toowrite Azure CDN."
services: cdn
documentationcenter: nodejs
author: zhangmanling
manager: erikre
editor: 
ms.assetid: c4bb6a61-de3d-4f0c-9dca-202554c43dfa
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 6c805e5fb8e0b471e8b248cb2f4b29efd6c85940
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-cdn-development"></a>Rozpoczynanie pracy z wdrażaniem usługi Azure CDN
> [!div class="op_single_selector"]
> * [Node.js](cdn-app-dev-node.md)
> * [.NET](cdn-app-dev-net.md)
> 
> 

Można użyć hello [Azure CDN SDK dla środowiska Node.js](https://www.npmjs.com/package/azure-arm-cdn) tooautomate tworzenie i zarządzanie profilami sieci CDN i punktów końcowych.  Ten samouczek przeprowadzi Cię przez hello tworzenia prostej aplikacji konsoli Node.js, która przedstawia niektóre z dostępnych operacji hello.  Ten samouczek jest przeznaczony toodescribe wszystkich aspektów hello Azure CDN SDK dla środowiska Node.js szczegółowo.

toocomplete tego samouczka należy [Node.js](http://www.nodejs.org) **4.x.x** lub nowszy zainstalowany i skonfigurowany.  Można użyć dowolnego edytora tekstu, które ma być toocreate aplikację Node.js.  toowrite tego samouczka używany [Visual Studio Code](https://code.visualstudio.com).  

> [!TIP]
> Witaj [ukończone projektu z tego samouczka](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74) jest dostępny do pobrania w witrynie MSDN.
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-npm-dependencies"></a>Tworzenie projektu i Dodawanie zależności NPM
Teraz, opracowaliśmy grupę zasobów dla naszych profilów CDN i naszych profilów usługi CDN toomanage uprawnienia aplikacji usługi Azure AD i punkty końcowe w ramach tej grupy, możemy rozpocząć tworzenie aplikacji.

Tworzenie toostore folderu aplikacji.  Z poziomu konsoli narzędzia Node.js hello w bieżącej ścieżce Ustaw bieżącej lokalizacji toothis nowy folder i zainicjować projektu, wykonując:

    npm init

Następnie można przedstawione szereg pytań tooinitialize Twojego projektu.  Aby uzyskać **punktu wejścia**, w tym samouczku używana *app.js*.  Moje innych wyborów w hello poniższy przykład jest widoczny.

![Dane wyjściowe init NPM](./media/cdn-app-dev-node/cdn-npm-init.png)

Nasze projektu teraz jest inicjowany z *packages.json* pliku.  Nasze projektu będzie toouse niektóre biblioteki Azure zawarte w pakietów NPM.  Użyjemy hello środowiska uruchomieniowego klienta Azure dla środowiska Node.js (ms-rest-azure) i hello biblioteki klienta usługi Azure CDN dla środowiska Node.js (azure-arm-cd).  Dodajmy tych toohello projektu jako zależności.

    npm install --save ms-rest-azure
    npm install --save azure-arm-cdn

Po hello pakiety są wykonywane instalowania, hello *package.json* pliku powinna wyglądać podobny przykład toothis (wersja numery może różnić się):

``` json
{
  "name": "cdn_node",
  "version": "1.0.0",
  "description": "Azure CDN Node.js tutorial project",
  "main": "app.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "Cam Soper",
  "license": "MIT",
  "dependencies": {
    "azure-arm-cdn": "^0.2.1",
    "ms-rest-azure": "^1.14.4"
  }
}
```

Ponadto za pomocą edytora tekstu, Utwórz pusty plik tekstowy i zapisać ją w głównym hello naszych folderu projektu jako *app.js*.  Jest teraz gotowy toobegin pisania kodu.

## <a name="requires-constants-authentication-and-structure"></a>Wymaga uwierzytelniania, stałe i struktury
Z *app.js* Otwórz w edytorze naszych, załóż hello podstawowej struktury nasz program zapisywane.

1. Dodaj hello "wymaga" naszych pakietów NPM u góry hello hello poniżej:
   
    ``` javascript
    var msRestAzure = require('ms-rest-azure');
    var cdnManagementClient = require('azure-arm-cdn');
    ```
2. Potrzebujemy toodefine niektóre stałe, używanego przez naszych metod.  Dodaj następujące hello.  Należy się tooreplace symbole zastępcze hello, w tym hello  **&lt;nawiasy&gt;**, z własne wartości zgodnie z potrzebami.
   
    ``` javascript
    //Tenant app constants
    const clientId = "<YOUR CLIENT ID>";
    const clientSecret = "<YOUR CLIENT AUTHENTICATION KEY>"; //Only for service principals
    const tenantId = "<YOUR TENANT ID>";
   
    //Application constants
    const subscriptionId = "<YOUR SUBSCRIPTION ID>";
    const resourceGroupName = "CdnConsoleTutorial";
    const resourceLocation = "<YOUR PREFERRED AZURE LOCATION, SUCH AS Central US>";
    ```
3. Następnie firma Microsoft będzie wystąpienia powitania klienta do zarządzania sieci CDN i nadaj naszych poświadczeń.
   
    ``` javascript
    var credentials = new msRestAzure.ApplicationTokenCredentials(clientId, tenantId, clientSecret);
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    Jeśli używasz uwierzytelniania użytkownika, te dwa wiersze będą różnić się nieznacznie.
   
   > [!IMPORTANT]
   > Ten przykładowy kod należy używać tylko, jeśli użytkownik zdecyduje toohave uwierzytelniania indywidualnych użytkowników zamiast nazwy głównej usługi.  Należy zachować ostrożność tooguard poświadczenia użytkownika i nie należy ich ujawniać.
   > 
   > 
   
    ``` javascript
    var credentials = new msRestAzure.UserTokenCredentials(clientId, 
        tenantId, '<username>', '<password>', '<redirect URI>');
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    Należy się tooreplace hello elementów w  **&lt;nawiasy&gt;**  z hello poprawić informacje.  Aby uzyskać `<redirect URI>`, użyj hello przekierowania URI wprowadzona podczas rejestrowania aplikacji hello w usłudze Azure AD.
4. Nasze aplikacja konsolowa Node.js będzie tootake niektóre parametry wiersza polecenia.  Teraz zweryfikować, że co najmniej jedna został przekazany parametr.
   
   ```javascript
   //Collect command-line parameters
   var parms = process.argv.slice(2);
   
   //Do we have parameters?
   if(parms == null || parms.length == 0)
   {
       console.log("Not enough parameters!");
       console.log("Valid commands are list, delete, create, and purge.");
       process.exit(1);
   }
   ```
5. Który zapewnia nam toohello główna część naszego programu, gdy gałęzie możemy tooother funkcje oparte na jakie parametry zostały przekazane.
   
    ```javascript
    switch(parms[0].toLowerCase())
    {
        case "list":
            cdnList();
            break;
   
        case "create":
            cdnCreate();
            break;
   
        case "delete":
            cdnDelete();
            break;
   
        case "purge":
            cdnPurge();
            break;
   
        default:
            console.log("Valid commands are list, delete, create, and purge.");
            process.exit(1);
    }
    ```
6. W kilku miejscach nasz program potrzebujemy toomake się hello prawa liczba parametrów zostały przekazane i wyświetlić Pomoc, jeśli nie przynosi poprawne.  Utwórz toodo funkcje który.
   
   ```javascript
   function requireParms(parmCount) {
       if(parms.length < parmCount) {
           usageHelp(parms[0].toLowerCase());
           process.exit(1);
       }
   }
   
   function usageHelp(cmd) {
       console.log("Usage for " + cmd + ":");
       switch(cmd)
       {
           case "list":
               console.log("list profiles");
               console.log("list endpoints <profile name>");
               break;
   
           case "create":
               console.log("create profile <profile name>");
               console.log("create endpoint <profile name> <endpoint name> <origin hostname>");
               break;
   
           case "delete":
               console.log("delete profile <profile name>");
               console.log("delete endpoint <profile name> <endpoint name>");
               break;
   
           case "purge":
               console.log("purge <profile name> <endpoint name> <path>");
               break;
   
           default:
               console.log("Invalid command.");
       }
   }
   ```
7. Na koniec hello funkcje, których będziemy używać na powitania klienta do zarządzania CDN są asynchroniczne, więc po ich gotowe muszą toocall — metoda.  Upewnij się, który można wyświetlić dane wyjściowe hello powitania klienta zarządzania sieci CDN (jeśli istnieje) i bezpiecznie zamknąć hello program.
   
    ```javascript
    function callback(err, result, request, response) {
        if (err) {
            console.log(err);
            process.exit(1);
        } else {
            console.log((result == null) ? "Done!" : result);
            process.exit(0);
        }
    }
    ```

Teraz, gdy podstawowa struktura nasz program hello są zapisywane, utworzymy powinien hello funkcji o nazwie oparte na naszych parametrów.

## <a name="list-cdn-profiles-and-endpoints"></a>Lista profilów CDN i punkty końcowe
Zacznijmy toolist kodu naszych istniejących profilów i punktów końcowych.  Komentarze w kodzie zawierają hello oczekiwano składni, aby było wiadomo, gdzie każdy parametr przejdzie.

```javascript
// list profiles
// list endpoints <profile name>
function cdnList(){
    requireParms(2);
    switch(parms[1].toLowerCase())
    {
        case "profiles":
            console.log("Listing profiles...");
            cdnClient.profiles.listByResourceGroup(resourceGroupName, callback);
            break;

        case "endpoints":
            requireParms(3);
            console.log("Listing endpoints...");
            cdnClient.endpoints.listByProfile(parms[2], resourceGroupName, callback);
            break;

        default:
            console.log("Invalid parameter.");
            process.exit(1);
    }
}
```

## <a name="create-cdn-profiles-and-endpoints"></a>Tworzenie profilów sieci CDN i punkty końcowe
Następnie firma Microsoft będzie zapisu hello funkcje toocreate profilów i punktów końcowych.

```javascript
function cdnCreate() {
    requireParms(2);
    switch(parms[1].toLowerCase())
    {
        case "profile":
            cdnCreateProfile();
            break;

        case "endpoint":
            cdnCreateEndpoint();
            break;

        default:
            console.log("Invalid parameter.");
            process.exit(1);
    }
}

// create profile <profile name>
function cdnCreateProfile() {
    requireParms(3);
    console.log("Creating profile...");
    var standardCreateParameters = {
        location: resourceLocation,
        sku: {
            name: 'Standard_Verizon'
        }
    };

    cdnClient.profiles.create(parms[2], standardCreateParameters, resourceGroupName, callback);
}

// create endpoint <profile name> <endpoint name> <origin hostname>        
function cdnCreateEndpoint() {
    requireParms(5);
    console.log("Creating endpoint...");
    var endpointProperties = {
        location: resourceLocation,
        origins: [{
            name: parms[4],
            hostName: parms[4]
        }]
    };

    cdnClient.endpoints.create(parms[3], endpointProperties, parms[2], resourceGroupName, callback);
}
```

## <a name="purge-an-endpoint"></a>Przeczyszczanie punktu końcowego
Przy założeniu, że utworzono punkt końcowy hello, jednego z typowych zadań, że firma Microsoft może być tooperform w naszym program jest przeczyszczanie zawartości w naszym punktu końcowego.

```javascript
// purge <profile name> <endpoint name> <path>
function cdnPurge() {
    requireParms(4);
    console.log("Purging endpoint...");
    var purgeContentPaths = [ parms[3] ];
    cdnClient.endpoints.purgeContent(parms[2], parms[1], resourceGroupName, purgeContentPaths, callback);
}
```

## <a name="delete-cdn-profiles-and-endpoints"></a>Usuwanie punktów końcowych i profilów usługi CDN
Funkcja ostatniego Hello przez nas będzie usuwa punkty końcowe i profile.

```javascript
function cdnDelete() {
    requireParms(2);
    switch(parms[1].toLowerCase())
    {
        // delete profile <profile name>
        case "profile":
            requireParms(3);
            console.log("Deleting profile...");
            cdnClient.profiles.deleteIfExists(parms[2], resourceGroupName, callback);
            break;

        // delete endpoint <profile name> <endpoint name>
        case "endpoint":
            requireParms(4);
            console.log("Deleting endpoint...");
            cdnClient.endpoints.deleteIfExists(parms[3], parms[2], resourceGroupName, callback);
            break;

        default:
            console.log("Invalid parameter.");
            process.exit(1);
    }
}
```

## <a name="running-hello-program"></a>Uruchomiony program hello
Teraz możemy wykonywać naszego programu Node.js za pomocą naszych ulubionych debugera lub hello konsoli.

> [!TIP]
> Jeśli używasz programu Visual Studio Code jako debuger, konieczne będzie tooset się toopass Twojego środowiska w hello parametry wiersza polecenia.  Visual Studio Code robi to hello **lanuch.json** pliku.  Wyszukaj właściwość o nazwie **argumentów** i Dodaj tablicę wartości ciągu parametry, aby wyglądały one podobnie toothis: `"args": ["list", "profiles"]`.
> 
> 

Zacznijmy od wyświetlania naszych profilów.

![Lista profilów](./media/cdn-app-dev-node/cdn-list-profiles.png)

Firma Microsoft otrzymano pustą tablicę.  Ponieważ nie mamy żadnych profilów w naszej grupy zasobów, która oczekuje.  Teraz Utwórzmy profilu.

![Utwórz profil](./media/cdn-app-dev-node/cdn-create-profile.png)

Teraz możemy dodać punkt końcowy.

![Tworzenie punktu końcowego](./media/cdn-app-dev-node/cdn-create-endpoint.png)

Ponadto umożliwia usunięcie naszych profilu.

![Usuwanie profilu](./media/cdn-app-dev-node/cdn-delete-profile.png)

## <a name="next-steps"></a>Następne kroki
Projekt ukończyć powitalnych toosee z tego przewodnika [pobieranie próbki hello](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74).

Odwołanie hello toosee hello Azure CDN SDK dla środowiska Node.js, widok hello [odwołania](http://azure.github.io/azure-sdk-for-node/azure-arm-cdn/latest/).

toofind dodatkową dokumentację hello Azure SDK dla środowiska Node.js, widok hello [pełne odwołanie](http://azure.github.io/azure-sdk-for-node/).

Zarządzanie zasobami CDN za pomocą [PowerShell](cdn-manage-powershell.md).

