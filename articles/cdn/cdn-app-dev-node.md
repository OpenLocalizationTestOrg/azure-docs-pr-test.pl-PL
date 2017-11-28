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
# <a name="get-started-with-azure-cdn-development"></a><span data-ttu-id="d3456-103">Rozpoczynanie pracy z wdrażaniem usługi Azure CDN</span><span class="sxs-lookup"><span data-stu-id="d3456-103">Get started with Azure CDN development</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d3456-104">Node.js</span><span class="sxs-lookup"><span data-stu-id="d3456-104">Node.js</span></span>](cdn-app-dev-node.md)
> * [<span data-ttu-id="d3456-105">.NET</span><span class="sxs-lookup"><span data-stu-id="d3456-105">.NET</span></span>](cdn-app-dev-net.md)
> 
> 

<span data-ttu-id="d3456-106">Można użyć hello [Azure CDN SDK dla środowiska Node.js](https://www.npmjs.com/package/azure-arm-cdn) tooautomate tworzenie i zarządzanie profilami sieci CDN i punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="d3456-106">You can use hello [Azure CDN SDK for Node.js](https://www.npmjs.com/package/azure-arm-cdn) tooautomate creation and management of CDN profiles and endpoints.</span></span>  <span data-ttu-id="d3456-107">Ten samouczek przeprowadzi Cię przez hello tworzenia prostej aplikacji konsoli Node.js, która przedstawia niektóre z dostępnych operacji hello.</span><span class="sxs-lookup"><span data-stu-id="d3456-107">This tutorial walks through hello creation of a simple Node.js console application that demonstrates several of hello available operations.</span></span>  <span data-ttu-id="d3456-108">Ten samouczek jest przeznaczony toodescribe wszystkich aspektów hello Azure CDN SDK dla środowiska Node.js szczegółowo.</span><span class="sxs-lookup"><span data-stu-id="d3456-108">This tutorial is not intended toodescribe all aspects of hello Azure CDN SDK for Node.js in detail.</span></span>

<span data-ttu-id="d3456-109">toocomplete tego samouczka należy [Node.js](http://www.nodejs.org) **4.x.x** lub nowszy zainstalowany i skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="d3456-109">toocomplete this tutorial, you should already have [Node.js](http://www.nodejs.org) **4.x.x** or higher installed and configured.</span></span>  <span data-ttu-id="d3456-110">Można użyć dowolnego edytora tekstu, które ma być toocreate aplikację Node.js.</span><span class="sxs-lookup"><span data-stu-id="d3456-110">You can use any text editor you want toocreate your Node.js application.</span></span>  <span data-ttu-id="d3456-111">toowrite tego samouczka używany [Visual Studio Code](https://code.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="d3456-111">toowrite this tutorial, I used [Visual Studio Code](https://code.visualstudio.com).</span></span>  

> [!TIP]
> <span data-ttu-id="d3456-112">Witaj [ukończone projektu z tego samouczka](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74) jest dostępny do pobrania w witrynie MSDN.</span><span class="sxs-lookup"><span data-stu-id="d3456-112">hello [completed project from this tutorial](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74) is available for download on MSDN.</span></span>
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-npm-dependencies"></a><span data-ttu-id="d3456-113">Tworzenie projektu i Dodawanie zależności NPM</span><span class="sxs-lookup"><span data-stu-id="d3456-113">Create your project and add NPM dependencies</span></span>
<span data-ttu-id="d3456-114">Teraz, opracowaliśmy grupę zasobów dla naszych profilów CDN i naszych profilów usługi CDN toomanage uprawnienia aplikacji usługi Azure AD i punkty końcowe w ramach tej grupy, możemy rozpocząć tworzenie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d3456-114">Now that we've created a resource group for our CDN profiles and given our Azure AD application permission toomanage CDN profiles and endpoints within that group, we can start creating our application.</span></span>

<span data-ttu-id="d3456-115">Tworzenie toostore folderu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d3456-115">Create a folder toostore your application.</span></span>  <span data-ttu-id="d3456-116">Z poziomu konsoli narzędzia Node.js hello w bieżącej ścieżce Ustaw bieżącej lokalizacji toothis nowy folder i zainicjować projektu, wykonując:</span><span class="sxs-lookup"><span data-stu-id="d3456-116">From a console with hello Node.js tools in your current path, set your current location toothis new folder and initialize your project by executing:</span></span>

    npm init

<span data-ttu-id="d3456-117">Następnie można przedstawione szereg pytań tooinitialize Twojego projektu.</span><span class="sxs-lookup"><span data-stu-id="d3456-117">You will then be presented a series of questions tooinitialize your project.</span></span>  <span data-ttu-id="d3456-118">Aby uzyskać **punktu wejścia**, w tym samouczku używana *app.js*.</span><span class="sxs-lookup"><span data-stu-id="d3456-118">For **entry point**, this tutorial uses *app.js*.</span></span>  <span data-ttu-id="d3456-119">Moje innych wyborów w hello poniższy przykład jest widoczny.</span><span class="sxs-lookup"><span data-stu-id="d3456-119">You can see my other choices in hello following example.</span></span>

![Dane wyjściowe init NPM](./media/cdn-app-dev-node/cdn-npm-init.png)

<span data-ttu-id="d3456-121">Nasze projektu teraz jest inicjowany z *packages.json* pliku.</span><span class="sxs-lookup"><span data-stu-id="d3456-121">Our project is now initialized with a *packages.json* file.</span></span>  <span data-ttu-id="d3456-122">Nasze projektu będzie toouse niektóre biblioteki Azure zawarte w pakietów NPM.</span><span class="sxs-lookup"><span data-stu-id="d3456-122">Our project is going toouse some Azure libraries contained in NPM packages.</span></span>  <span data-ttu-id="d3456-123">Użyjemy hello środowiska uruchomieniowego klienta Azure dla środowiska Node.js (ms-rest-azure) i hello biblioteki klienta usługi Azure CDN dla środowiska Node.js (azure-arm-cd).</span><span class="sxs-lookup"><span data-stu-id="d3456-123">We'll use hello Azure Client Runtime for Node.js (ms-rest-azure) and hello Azure CDN Client Library for Node.js (azure-arm-cd).</span></span>  <span data-ttu-id="d3456-124">Dodajmy tych toohello projektu jako zależności.</span><span class="sxs-lookup"><span data-stu-id="d3456-124">Let's add those toohello project as dependencies.</span></span>

    npm install --save ms-rest-azure
    npm install --save azure-arm-cdn

<span data-ttu-id="d3456-125">Po hello pakiety są wykonywane instalowania, hello *package.json* pliku powinna wyglądać podobny przykład toothis (wersja numery może różnić się):</span><span class="sxs-lookup"><span data-stu-id="d3456-125">After hello packages are done installing, hello *package.json* file should look similar toothis example (version numbers may differ):</span></span>

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

<span data-ttu-id="d3456-126">Ponadto za pomocą edytora tekstu, Utwórz pusty plik tekstowy i zapisać ją w głównym hello naszych folderu projektu jako *app.js*.</span><span class="sxs-lookup"><span data-stu-id="d3456-126">Finally, using your text editor, create a blank text file and save it in hello root of our project folder as *app.js*.</span></span>  <span data-ttu-id="d3456-127">Jest teraz gotowy toobegin pisania kodu.</span><span class="sxs-lookup"><span data-stu-id="d3456-127">We're now ready toobegin writing code.</span></span>

## <a name="requires-constants-authentication-and-structure"></a><span data-ttu-id="d3456-128">Wymaga uwierzytelniania, stałe i struktury</span><span class="sxs-lookup"><span data-stu-id="d3456-128">Requires, constants, authentication, and structure</span></span>
<span data-ttu-id="d3456-129">Z *app.js* Otwórz w edytorze naszych, załóż hello podstawowej struktury nasz program zapisywane.</span><span class="sxs-lookup"><span data-stu-id="d3456-129">With *app.js* open in our editor, let's get hello basic structure of our program written.</span></span>

1. <span data-ttu-id="d3456-130">Dodaj hello "wymaga" naszych pakietów NPM u góry hello hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="d3456-130">Add hello "requires" for our NPM packages at hello top with hello following:</span></span>
   
    ``` javascript
    var msRestAzure = require('ms-rest-azure');
    var cdnManagementClient = require('azure-arm-cdn');
    ```
2. <span data-ttu-id="d3456-131">Potrzebujemy toodefine niektóre stałe, używanego przez naszych metod.</span><span class="sxs-lookup"><span data-stu-id="d3456-131">We need toodefine some constants our methods will use.</span></span>  <span data-ttu-id="d3456-132">Dodaj następujące hello.</span><span class="sxs-lookup"><span data-stu-id="d3456-132">Add hello following.</span></span>  <span data-ttu-id="d3456-133">Należy się tooreplace symbole zastępcze hello, w tym hello  **&lt;nawiasy&gt;**, z własne wartości zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="d3456-133">Be sure tooreplace hello placeholders, including hello **&lt;angle brackets&gt;**, with your own values as needed.</span></span>
   
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
3. <span data-ttu-id="d3456-134">Następnie firma Microsoft będzie wystąpienia powitania klienta do zarządzania sieci CDN i nadaj naszych poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="d3456-134">Next, we'll instantiate hello CDN management client and give it our credentials.</span></span>
   
    ``` javascript
    var credentials = new msRestAzure.ApplicationTokenCredentials(clientId, tenantId, clientSecret);
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    <span data-ttu-id="d3456-135">Jeśli używasz uwierzytelniania użytkownika, te dwa wiersze będą różnić się nieznacznie.</span><span class="sxs-lookup"><span data-stu-id="d3456-135">If you are using individual user authentication, these two lines will look slightly different.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="d3456-136">Ten przykładowy kod należy używać tylko, jeśli użytkownik zdecyduje toohave uwierzytelniania indywidualnych użytkowników zamiast nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="d3456-136">Only use this code sample if you are choosing toohave individual user authentication instead of a service principal.</span></span>  <span data-ttu-id="d3456-137">Należy zachować ostrożność tooguard poświadczenia użytkownika i nie należy ich ujawniać.</span><span class="sxs-lookup"><span data-stu-id="d3456-137">Be careful tooguard your individual user credentials and keep them secret.</span></span>
   > 
   > 
   
    ``` javascript
    var credentials = new msRestAzure.UserTokenCredentials(clientId, 
        tenantId, '<username>', '<password>', '<redirect URI>');
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    <span data-ttu-id="d3456-138">Należy się tooreplace hello elementów w  **&lt;nawiasy&gt;**  z hello poprawić informacje.</span><span class="sxs-lookup"><span data-stu-id="d3456-138">Be sure tooreplace hello items in **&lt;angle brackets&gt;** with hello correct information.</span></span>  <span data-ttu-id="d3456-139">Aby uzyskać `<redirect URI>`, użyj hello przekierowania URI wprowadzona podczas rejestrowania aplikacji hello w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d3456-139">For `<redirect URI>`, use hello redirect URI you entered when you registered hello application in Azure AD.</span></span>
4. <span data-ttu-id="d3456-140">Nasze aplikacja konsolowa Node.js będzie tootake niektóre parametry wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="d3456-140">Our Node.js console application is going tootake some command-line parameters.</span></span>  <span data-ttu-id="d3456-141">Teraz zweryfikować, że co najmniej jedna został przekazany parametr.</span><span class="sxs-lookup"><span data-stu-id="d3456-141">Let's validate that at least one parameter was passed.</span></span>
   
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
5. <span data-ttu-id="d3456-142">Który zapewnia nam toohello główna część naszego programu, gdy gałęzie możemy tooother funkcje oparte na jakie parametry zostały przekazane.</span><span class="sxs-lookup"><span data-stu-id="d3456-142">That brings us toohello main part of our program, where we branch off tooother functions based on what parameters were passed.</span></span>
   
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
6. <span data-ttu-id="d3456-143">W kilku miejscach nasz program potrzebujemy toomake się hello prawa liczba parametrów zostały przekazane i wyświetlić Pomoc, jeśli nie przynosi poprawne.</span><span class="sxs-lookup"><span data-stu-id="d3456-143">At several places in our program, we'll need toomake sure hello right number of parameters were passed in and display some help if they don't look correct.</span></span>  <span data-ttu-id="d3456-144">Utwórz toodo funkcje który.</span><span class="sxs-lookup"><span data-stu-id="d3456-144">Let's create functions toodo that.</span></span>
   
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
7. <span data-ttu-id="d3456-145">Na koniec hello funkcje, których będziemy używać na powitania klienta do zarządzania CDN są asynchroniczne, więc po ich gotowe muszą toocall — metoda.</span><span class="sxs-lookup"><span data-stu-id="d3456-145">Finally, hello functions we'll be using on hello CDN management client are asynchronous, so they need a method toocall back when they're done.</span></span>  <span data-ttu-id="d3456-146">Upewnij się, który można wyświetlić dane wyjściowe hello powitania klienta zarządzania sieci CDN (jeśli istnieje) i bezpiecznie zamknąć hello program.</span><span class="sxs-lookup"><span data-stu-id="d3456-146">Let's make one that can display hello output from hello CDN management client (if any) and exit hello program gracefully.</span></span>
   
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

<span data-ttu-id="d3456-147">Teraz, gdy podstawowa struktura nasz program hello są zapisywane, utworzymy powinien hello funkcji o nazwie oparte na naszych parametrów.</span><span class="sxs-lookup"><span data-stu-id="d3456-147">Now that hello basic structure of our program is written, we should create hello functions called based on our parameters.</span></span>

## <a name="list-cdn-profiles-and-endpoints"></a><span data-ttu-id="d3456-148">Lista profilów CDN i punkty końcowe</span><span class="sxs-lookup"><span data-stu-id="d3456-148">List CDN profiles and endpoints</span></span>
<span data-ttu-id="d3456-149">Zacznijmy toolist kodu naszych istniejących profilów i punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="d3456-149">Let's start with code toolist our existing profiles and endpoints.</span></span>  <span data-ttu-id="d3456-150">Komentarze w kodzie zawierają hello oczekiwano składni, aby było wiadomo, gdzie każdy parametr przejdzie.</span><span class="sxs-lookup"><span data-stu-id="d3456-150">My code comments provide hello expected syntax so we know where each parameter goes.</span></span>

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

## <a name="create-cdn-profiles-and-endpoints"></a><span data-ttu-id="d3456-151">Tworzenie profilów sieci CDN i punkty końcowe</span><span class="sxs-lookup"><span data-stu-id="d3456-151">Create CDN profiles and endpoints</span></span>
<span data-ttu-id="d3456-152">Następnie firma Microsoft będzie zapisu hello funkcje toocreate profilów i punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="d3456-152">Next, we'll write hello functions toocreate profiles and endpoints.</span></span>

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

## <a name="purge-an-endpoint"></a><span data-ttu-id="d3456-153">Przeczyszczanie punktu końcowego</span><span class="sxs-lookup"><span data-stu-id="d3456-153">Purge an endpoint</span></span>
<span data-ttu-id="d3456-154">Przy założeniu, że utworzono punkt końcowy hello, jednego z typowych zadań, że firma Microsoft może być tooperform w naszym program jest przeczyszczanie zawartości w naszym punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="d3456-154">Assuming hello endpoint has been created, one common task that we might want tooperform in our program is purging content in our endpoint.</span></span>

```javascript
// purge <profile name> <endpoint name> <path>
function cdnPurge() {
    requireParms(4);
    console.log("Purging endpoint...");
    var purgeContentPaths = [ parms[3] ];
    cdnClient.endpoints.purgeContent(parms[2], parms[1], resourceGroupName, purgeContentPaths, callback);
}
```

## <a name="delete-cdn-profiles-and-endpoints"></a><span data-ttu-id="d3456-155">Usuwanie punktów końcowych i profilów usługi CDN</span><span class="sxs-lookup"><span data-stu-id="d3456-155">Delete CDN profiles and endpoints</span></span>
<span data-ttu-id="d3456-156">Funkcja ostatniego Hello przez nas będzie usuwa punkty końcowe i profile.</span><span class="sxs-lookup"><span data-stu-id="d3456-156">hello last function we will include deletes endpoints and profiles.</span></span>

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

## <a name="running-hello-program"></a><span data-ttu-id="d3456-157">Uruchomiony program hello</span><span class="sxs-lookup"><span data-stu-id="d3456-157">Running hello program</span></span>
<span data-ttu-id="d3456-158">Teraz możemy wykonywać naszego programu Node.js za pomocą naszych ulubionych debugera lub hello konsoli.</span><span class="sxs-lookup"><span data-stu-id="d3456-158">We can now execute our Node.js program using our favorite debugger or at hello console.</span></span>

> [!TIP]
> <span data-ttu-id="d3456-159">Jeśli używasz programu Visual Studio Code jako debuger, konieczne będzie tooset się toopass Twojego środowiska w hello parametry wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="d3456-159">If you're using Visual Studio Code as your debugger, you'll need tooset up your environment toopass in hello command-line parameters.</span></span>  <span data-ttu-id="d3456-160">Visual Studio Code robi to hello **lanuch.json** pliku.</span><span class="sxs-lookup"><span data-stu-id="d3456-160">Visual Studio Code does this in hello **lanuch.json** file.</span></span>  <span data-ttu-id="d3456-161">Wyszukaj właściwość o nazwie **argumentów** i Dodaj tablicę wartości ciągu parametry, aby wyglądały one podobnie toothis: `"args": ["list", "profiles"]`.</span><span class="sxs-lookup"><span data-stu-id="d3456-161">Look for a property named **args** and add an array of string values for your parameters, so that it looks similar toothis:  `"args": ["list", "profiles"]`.</span></span>
> 
> 

<span data-ttu-id="d3456-162">Zacznijmy od wyświetlania naszych profilów.</span><span class="sxs-lookup"><span data-stu-id="d3456-162">Let's start by listing our profiles.</span></span>

![Lista profilów](./media/cdn-app-dev-node/cdn-list-profiles.png)

<span data-ttu-id="d3456-164">Firma Microsoft otrzymano pustą tablicę.</span><span class="sxs-lookup"><span data-stu-id="d3456-164">We got back an empty array.</span></span>  <span data-ttu-id="d3456-165">Ponieważ nie mamy żadnych profilów w naszej grupy zasobów, która oczekuje.</span><span class="sxs-lookup"><span data-stu-id="d3456-165">Since we don't have any profiles in our resource group, that's expected.</span></span>  <span data-ttu-id="d3456-166">Teraz Utwórzmy profilu.</span><span class="sxs-lookup"><span data-stu-id="d3456-166">Let's create a profile now.</span></span>

![Utwórz profil](./media/cdn-app-dev-node/cdn-create-profile.png)

<span data-ttu-id="d3456-168">Teraz możemy dodać punkt końcowy.</span><span class="sxs-lookup"><span data-stu-id="d3456-168">Now, let's add an endpoint.</span></span>

![Tworzenie punktu końcowego](./media/cdn-app-dev-node/cdn-create-endpoint.png)

<span data-ttu-id="d3456-170">Ponadto umożliwia usunięcie naszych profilu.</span><span class="sxs-lookup"><span data-stu-id="d3456-170">Finally, let's delete our profile.</span></span>

![Usuwanie profilu](./media/cdn-app-dev-node/cdn-delete-profile.png)

## <a name="next-steps"></a><span data-ttu-id="d3456-172">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d3456-172">Next Steps</span></span>
<span data-ttu-id="d3456-173">Projekt ukończyć powitalnych toosee z tego przewodnika [pobieranie próbki hello](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74).</span><span class="sxs-lookup"><span data-stu-id="d3456-173">toosee hello completed project from this walkthrough, [download hello sample](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74).</span></span>

<span data-ttu-id="d3456-174">Odwołanie hello toosee hello Azure CDN SDK dla środowiska Node.js, widok hello [odwołania](http://azure.github.io/azure-sdk-for-node/azure-arm-cdn/latest/).</span><span class="sxs-lookup"><span data-stu-id="d3456-174">toosee hello reference for hello Azure CDN SDK for Node.js, view hello [reference](http://azure.github.io/azure-sdk-for-node/azure-arm-cdn/latest/).</span></span>

<span data-ttu-id="d3456-175">toofind dodatkową dokumentację hello Azure SDK dla środowiska Node.js, widok hello [pełne odwołanie](http://azure.github.io/azure-sdk-for-node/).</span><span class="sxs-lookup"><span data-stu-id="d3456-175">toofind additional documentation on hello Azure SDK for Node.js, view hello [full reference](http://azure.github.io/azure-sdk-for-node/).</span></span>

<span data-ttu-id="d3456-176">Zarządzanie zasobami CDN za pomocą [PowerShell](cdn-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="d3456-176">Manage your CDN resources with [PowerShell](cdn-manage-powershell.md).</span></span>

