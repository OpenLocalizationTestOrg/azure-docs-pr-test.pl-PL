---
title: "Rozpoczynanie pracy z zestawem SDK usługi Azure CDN dla środowiska Node.js | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak pisanie aplikacji Node.js do zarządzania usługi Azure CDN."
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
ms.openlocfilehash: 46ae8cd9775432d126cbde856c1fb06ea319297e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-cdn-development"></a><span data-ttu-id="c007e-103">Rozpoczynanie pracy z wdrażaniem usługi Azure CDN</span><span class="sxs-lookup"><span data-stu-id="c007e-103">Get started with Azure CDN development</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c007e-104">Node.js</span><span class="sxs-lookup"><span data-stu-id="c007e-104">Node.js</span></span>](cdn-app-dev-node.md)
> * [<span data-ttu-id="c007e-105">.NET</span><span class="sxs-lookup"><span data-stu-id="c007e-105">.NET</span></span>](cdn-app-dev-net.md)
> 
> 

<span data-ttu-id="c007e-106">Można użyć [Azure CDN SDK dla środowiska Node.js](https://www.npmjs.com/package/azure-arm-cdn) można zautomatyzować tworzenie i zarządzanie profilami sieci CDN i punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="c007e-106">You can use the [Azure CDN SDK for Node.js](https://www.npmjs.com/package/azure-arm-cdn) to automate creation and management of CDN profiles and endpoints.</span></span>  <span data-ttu-id="c007e-107">Ten samouczek przeprowadza przez tworzenie prostej aplikacji konsoli Node.js, która przedstawia niektóre z dostępnych operacji.</span><span class="sxs-lookup"><span data-stu-id="c007e-107">This tutorial walks through the creation of a simple Node.js console application that demonstrates several of the available operations.</span></span>  <span data-ttu-id="c007e-108">W tym samouczku nie ma na celu opis wszystkich aspektów zestaw SDK usługi Azure CDN dla środowiska Node.js szczegółowo.</span><span class="sxs-lookup"><span data-stu-id="c007e-108">This tutorial is not intended to describe all aspects of the Azure CDN SDK for Node.js in detail.</span></span>

<span data-ttu-id="c007e-109">Do ukończenia tego samouczka, powinien zostać [Node.js](http://www.nodejs.org) **4.x.x** lub nowszy zainstalowany i skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="c007e-109">To complete this tutorial, you should already have [Node.js](http://www.nodejs.org) **4.x.x** or higher installed and configured.</span></span>  <span data-ttu-id="c007e-110">Można użyć dowolnego edytora tekstów, aby utworzyć aplikację Node.js.</span><span class="sxs-lookup"><span data-stu-id="c007e-110">You can use any text editor you want to create your Node.js application.</span></span>  <span data-ttu-id="c007e-111">Można zapisać w tym samouczku, używany [Visual Studio Code](https://code.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="c007e-111">To write this tutorial, I used [Visual Studio Code](https://code.visualstudio.com).</span></span>  

> [!TIP]
> <span data-ttu-id="c007e-112">[Ukończone projektu z tego samouczka](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74) jest dostępny do pobrania w witrynie MSDN.</span><span class="sxs-lookup"><span data-stu-id="c007e-112">The [completed project from this tutorial](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74) is available for download on MSDN.</span></span>
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-npm-dependencies"></a><span data-ttu-id="c007e-113">Tworzenie projektu i Dodawanie zależności NPM</span><span class="sxs-lookup"><span data-stu-id="c007e-113">Create your project and add NPM dependencies</span></span>
<span data-ttu-id="c007e-114">Teraz, opracowaliśmy grupę zasobów dla naszych profilów CDN i naszych uprawnienia aplikacji usługi Azure AD do zarządzania profilami sieci CDN i punkty końcowe w ramach tej grupy, możemy rozpocząć tworzenie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c007e-114">Now that we've created a resource group for our CDN profiles and given our Azure AD application permission to manage CDN profiles and endpoints within that group, we can start creating our application.</span></span>

<span data-ttu-id="c007e-115">Utwórz folder do przechowywania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c007e-115">Create a folder to store your application.</span></span>  <span data-ttu-id="c007e-116">Z poziomu konsoli przy użyciu narzędzi Node.js w bieżącej ścieżce Ustaw bieżącą lokalizację tego nowego folderu, a inicjowanie projektu, wykonując:</span><span class="sxs-lookup"><span data-stu-id="c007e-116">From a console with the Node.js tools in your current path, set your current location to this new folder and initialize your project by executing:</span></span>

    npm init

<span data-ttu-id="c007e-117">Zostanie następnie wyświetlona szereg pytań, można zainicjować projektu.</span><span class="sxs-lookup"><span data-stu-id="c007e-117">You will then be presented a series of questions to initialize your project.</span></span>  <span data-ttu-id="c007e-118">Aby uzyskać **punktu wejścia**, w tym samouczku używana *app.js*.</span><span class="sxs-lookup"><span data-stu-id="c007e-118">For **entry point**, this tutorial uses *app.js*.</span></span>  <span data-ttu-id="c007e-119">Moje innych wyborów w poniższym przykładzie jest widoczny.</span><span class="sxs-lookup"><span data-stu-id="c007e-119">You can see my other choices in the following example.</span></span>

![Dane wyjściowe init NPM](./media/cdn-app-dev-node/cdn-npm-init.png)

<span data-ttu-id="c007e-121">Nasze projektu teraz jest inicjowany z *packages.json* pliku.</span><span class="sxs-lookup"><span data-stu-id="c007e-121">Our project is now initialized with a *packages.json* file.</span></span>  <span data-ttu-id="c007e-122">Nasze projektu będzie korzystać z niektórych bibliotek Azure zawartych w pakietach NPM.</span><span class="sxs-lookup"><span data-stu-id="c007e-122">Our project is going to use some Azure libraries contained in NPM packages.</span></span>  <span data-ttu-id="c007e-123">Użyjemy środowiska uruchomieniowego klienta Azure dla środowiska Node.js (ms-rest-azure) i biblioteki klienta usługi Azure CDN dla środowiska Node.js (azure-arm-cd).</span><span class="sxs-lookup"><span data-stu-id="c007e-123">We'll use the Azure Client Runtime for Node.js (ms-rest-azure) and the Azure CDN Client Library for Node.js (azure-arm-cd).</span></span>  <span data-ttu-id="c007e-124">Dodajmy tych do projektu jako zależności.</span><span class="sxs-lookup"><span data-stu-id="c007e-124">Let's add those to the project as dependencies.</span></span>

    npm install --save ms-rest-azure
    npm install --save azure-arm-cdn

<span data-ttu-id="c007e-125">Po zakończeniu pakiety instalowania, *package.json* pliku powinna wyglądać podobnie jak w tym przykładzie (wersja numery może różnić się):</span><span class="sxs-lookup"><span data-stu-id="c007e-125">After the packages are done installing, the *package.json* file should look similar to this example (version numbers may differ):</span></span>

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

<span data-ttu-id="c007e-126">Na koniec za pomocą edytora tekstu, Utwórz pusty plik tekstowy i zapisz go w katalogu głównym folderu naszych projektu jako *app.js*.</span><span class="sxs-lookup"><span data-stu-id="c007e-126">Finally, using your text editor, create a blank text file and save it in the root of our project folder as *app.js*.</span></span>  <span data-ttu-id="c007e-127">Jest teraz gotowy do rozpoczęcia pisania kodu.</span><span class="sxs-lookup"><span data-stu-id="c007e-127">We're now ready to begin writing code.</span></span>

## <a name="requires-constants-authentication-and-structure"></a><span data-ttu-id="c007e-128">Wymaga uwierzytelniania, stałe i struktury</span><span class="sxs-lookup"><span data-stu-id="c007e-128">Requires, constants, authentication, and structure</span></span>
<span data-ttu-id="c007e-129">Z *app.js* Otwórz w edytorze naszych, załóż podstawowej struktury nasz program zapisywane.</span><span class="sxs-lookup"><span data-stu-id="c007e-129">With *app.js* open in our editor, let's get the basic structure of our program written.</span></span>

1. <span data-ttu-id="c007e-130">Dodaj "wymaga" naszych pakietów NPM u góry z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="c007e-130">Add the "requires" for our NPM packages at the top with the following:</span></span>
   
    ``` javascript
    var msRestAzure = require('ms-rest-azure');
    var cdnManagementClient = require('azure-arm-cdn');
    ```
2. <span data-ttu-id="c007e-131">Musimy zdefiniować niektóre stałe, używanego przez naszych metod.</span><span class="sxs-lookup"><span data-stu-id="c007e-131">We need to define some constants our methods will use.</span></span>  <span data-ttu-id="c007e-132">Dodaj następujące czynności.</span><span class="sxs-lookup"><span data-stu-id="c007e-132">Add the following.</span></span>  <span data-ttu-id="c007e-133">Koniecznie Zastąp symbole zastępcze w tym  **&lt;nawiasy&gt;**, z własne wartości zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="c007e-133">Be sure to replace the placeholders, including the **&lt;angle brackets&gt;**, with your own values as needed.</span></span>
   
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
3. <span data-ttu-id="c007e-134">Następnie firma Microsoft będzie wystąpienia klienta zarządzania w sieci CDN i nadaj naszych poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="c007e-134">Next, we'll instantiate the CDN management client and give it our credentials.</span></span>
   
    ``` javascript
    var credentials = new msRestAzure.ApplicationTokenCredentials(clientId, tenantId, clientSecret);
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    <span data-ttu-id="c007e-135">Jeśli używasz uwierzytelniania użytkownika, te dwa wiersze będą różnić się nieznacznie.</span><span class="sxs-lookup"><span data-stu-id="c007e-135">If you are using individual user authentication, these two lines will look slightly different.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="c007e-136">Ten przykładowy kod należy używać, tylko jeśli wybierzesz do uwierzytelniania indywidualnych użytkowników zamiast nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="c007e-136">Only use this code sample if you are choosing to have individual user authentication instead of a service principal.</span></span>  <span data-ttu-id="c007e-137">Należy zachować ostrożność zabezpieczyć poświadczenia użytkownika i nie należy ich ujawniać.</span><span class="sxs-lookup"><span data-stu-id="c007e-137">Be careful to guard your individual user credentials and keep them secret.</span></span>
   > 
   > 
   
    ``` javascript
    var credentials = new msRestAzure.UserTokenCredentials(clientId, 
        tenantId, '<username>', '<password>', '<redirect URI>');
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    <span data-ttu-id="c007e-138">Należy zastąpić elementy w  **&lt;nawiasy&gt;**  przy użyciu prawidłowych informacji.</span><span class="sxs-lookup"><span data-stu-id="c007e-138">Be sure to replace the items in **&lt;angle brackets&gt;** with the correct information.</span></span>  <span data-ttu-id="c007e-139">Aby uzyskać `<redirect URI>`, użyj przekierowania URI wprowadzona podczas rejestrowania aplikacji w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c007e-139">For `<redirect URI>`, use the redirect URI you entered when you registered the application in Azure AD.</span></span>
4. <span data-ttu-id="c007e-140">Nasze aplikacja konsolowa Node.js ma wykonać niektóre parametry wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="c007e-140">Our Node.js console application is going to take some command-line parameters.</span></span>  <span data-ttu-id="c007e-141">Teraz zweryfikować, że co najmniej jedna został przekazany parametr.</span><span class="sxs-lookup"><span data-stu-id="c007e-141">Let's validate that at least one parameter was passed.</span></span>
   
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
5. <span data-ttu-id="c007e-142">Które nam wprowadzono do głównej części nasz program, w którym firma Microsoft gałęzie na inne funkcje oparte na jakie parametry zostały przekazane.</span><span class="sxs-lookup"><span data-stu-id="c007e-142">That brings us to the main part of our program, where we branch off to other functions based on what parameters were passed.</span></span>
   
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
6. <span data-ttu-id="c007e-143">W kilku miejscach nasz program potrzebujemy upewnij się, że prawa liczba parametrów zostały przekazane i wyświetlić Pomoc, jeśli nie przynosi poprawne.</span><span class="sxs-lookup"><span data-stu-id="c007e-143">At several places in our program, we'll need to make sure the right number of parameters were passed in and display some help if they don't look correct.</span></span>  <span data-ttu-id="c007e-144">Funkcje, w tym celu Utwórz.</span><span class="sxs-lookup"><span data-stu-id="c007e-144">Let's create functions to do that.</span></span>
   
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
7. <span data-ttu-id="c007e-145">Na koniec funkcje, których będziemy używać w sieci CDN w warstwie klienta zarządzania są asynchroniczne, więc potrzebują metody do wywołania po ich wszystko gotowe.</span><span class="sxs-lookup"><span data-stu-id="c007e-145">Finally, the functions we'll be using on the CDN management client are asynchronous, so they need a method to call back when they're done.</span></span>  <span data-ttu-id="c007e-146">Upewnij się, który można wyświetlić dane wyjściowe z sieci CDN w warstwie klienta zarządzania (jeśli istnieje) i bezpiecznie zamknąć program.</span><span class="sxs-lookup"><span data-stu-id="c007e-146">Let's make one that can display the output from the CDN management client (if any) and exit the program gracefully.</span></span>
   
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

<span data-ttu-id="c007e-147">Teraz, gdy podstawowa struktura nasz program napisano, utworzymy powinien funkcji o nazwie oparte na naszych parametrów.</span><span class="sxs-lookup"><span data-stu-id="c007e-147">Now that the basic structure of our program is written, we should create the functions called based on our parameters.</span></span>

## <a name="list-cdn-profiles-and-endpoints"></a><span data-ttu-id="c007e-148">Lista profilów CDN i punkty końcowe</span><span class="sxs-lookup"><span data-stu-id="c007e-148">List CDN profiles and endpoints</span></span>
<span data-ttu-id="c007e-149">Zacznijmy od kodu do listy naszych istniejących profilów i punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="c007e-149">Let's start with code to list our existing profiles and endpoints.</span></span>  <span data-ttu-id="c007e-150">Komentarze w kodzie Podaj oczekiwanego składni, aby było wiadomo, gdzie każdy parametr przejdzie.</span><span class="sxs-lookup"><span data-stu-id="c007e-150">My code comments provide the expected syntax so we know where each parameter goes.</span></span>

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

## <a name="create-cdn-profiles-and-endpoints"></a><span data-ttu-id="c007e-151">Tworzenie profilów sieci CDN i punkty końcowe</span><span class="sxs-lookup"><span data-stu-id="c007e-151">Create CDN profiles and endpoints</span></span>
<span data-ttu-id="c007e-152">Firma Microsoft będzie następnie należy napisać funkcje do tworzenia profilów i punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="c007e-152">Next, we'll write the functions to create profiles and endpoints.</span></span>

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

## <a name="purge-an-endpoint"></a><span data-ttu-id="c007e-153">Przeczyszczanie punktu końcowego</span><span class="sxs-lookup"><span data-stu-id="c007e-153">Purge an endpoint</span></span>
<span data-ttu-id="c007e-154">Zakładając, że utworzono punkt końcowy, jeden typowe zadania, które firma Microsoft może być wykonanie w nasz program jest przeczyszczanie zawartości w naszym punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="c007e-154">Assuming the endpoint has been created, one common task that we might want to perform in our program is purging content in our endpoint.</span></span>

```javascript
// purge <profile name> <endpoint name> <path>
function cdnPurge() {
    requireParms(4);
    console.log("Purging endpoint...");
    var purgeContentPaths = [ parms[3] ];
    cdnClient.endpoints.purgeContent(parms[2], parms[1], resourceGroupName, purgeContentPaths, callback);
}
```

## <a name="delete-cdn-profiles-and-endpoints"></a><span data-ttu-id="c007e-155">Usuwanie punktów końcowych i profilów usługi CDN</span><span class="sxs-lookup"><span data-stu-id="c007e-155">Delete CDN profiles and endpoints</span></span>
<span data-ttu-id="c007e-156">Ostatniej funkcji, które firma Microsoft będzie zawierać usuwa punkty końcowe i profilów.</span><span class="sxs-lookup"><span data-stu-id="c007e-156">The last function we will include deletes endpoints and profiles.</span></span>

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

## <a name="running-the-program"></a><span data-ttu-id="c007e-157">Uruchomienie programu</span><span class="sxs-lookup"><span data-stu-id="c007e-157">Running the program</span></span>
<span data-ttu-id="c007e-158">Teraz możemy wykonywać naszego programu Node.js za pomocą naszych ulubionych debugera lub za pomocą konsoli.</span><span class="sxs-lookup"><span data-stu-id="c007e-158">We can now execute our Node.js program using our favorite debugger or at the console.</span></span>

> [!TIP]
> <span data-ttu-id="c007e-159">Jeśli używasz programu Visual Studio Code jako debuger, należy skonfigurować środowisko do przekazania parametrów wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="c007e-159">If you're using Visual Studio Code as your debugger, you'll need to set up your environment to pass in the command-line parameters.</span></span>  <span data-ttu-id="c007e-160">Robi to programie Visual Studio Code **lanuch.json** pliku.</span><span class="sxs-lookup"><span data-stu-id="c007e-160">Visual Studio Code does this in the **lanuch.json** file.</span></span>  <span data-ttu-id="c007e-161">Wyszukaj właściwość o nazwie **argumentów** i Dodaj tablicę wartości ciągu parametry, aby wyglądały one podobnie do poniższego: `"args": ["list", "profiles"]`.</span><span class="sxs-lookup"><span data-stu-id="c007e-161">Look for a property named **args** and add an array of string values for your parameters, so that it looks similar to this:  `"args": ["list", "profiles"]`.</span></span>
> 
> 

<span data-ttu-id="c007e-162">Zacznijmy od wyświetlania naszych profilów.</span><span class="sxs-lookup"><span data-stu-id="c007e-162">Let's start by listing our profiles.</span></span>

![Lista profilów](./media/cdn-app-dev-node/cdn-list-profiles.png)

<span data-ttu-id="c007e-164">Firma Microsoft otrzymano pustą tablicę.</span><span class="sxs-lookup"><span data-stu-id="c007e-164">We got back an empty array.</span></span>  <span data-ttu-id="c007e-165">Ponieważ nie mamy żadnych profilów w naszej grupy zasobów, która oczekuje.</span><span class="sxs-lookup"><span data-stu-id="c007e-165">Since we don't have any profiles in our resource group, that's expected.</span></span>  <span data-ttu-id="c007e-166">Teraz Utwórzmy profilu.</span><span class="sxs-lookup"><span data-stu-id="c007e-166">Let's create a profile now.</span></span>

![Utwórz profil](./media/cdn-app-dev-node/cdn-create-profile.png)

<span data-ttu-id="c007e-168">Teraz możemy dodać punkt końcowy.</span><span class="sxs-lookup"><span data-stu-id="c007e-168">Now, let's add an endpoint.</span></span>

![Tworzenie punktu końcowego](./media/cdn-app-dev-node/cdn-create-endpoint.png)

<span data-ttu-id="c007e-170">Ponadto umożliwia usunięcie naszych profilu.</span><span class="sxs-lookup"><span data-stu-id="c007e-170">Finally, let's delete our profile.</span></span>

![Usuwanie profilu](./media/cdn-app-dev-node/cdn-delete-profile.png)

## <a name="next-steps"></a><span data-ttu-id="c007e-172">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c007e-172">Next Steps</span></span>
<span data-ttu-id="c007e-173">Aby wyświetlić ukończone projektu z tego przewodnika [Pobierz przykład](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74).</span><span class="sxs-lookup"><span data-stu-id="c007e-173">To see the completed project from this walkthrough, [download the sample](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74).</span></span>

<span data-ttu-id="c007e-174">Odwołanie do zestawu SDK usługi Azure CDN dla środowiska Node.js, przejrzeć [odwołania](http://azure.github.io/azure-sdk-for-node/azure-arm-cdn/latest/).</span><span class="sxs-lookup"><span data-stu-id="c007e-174">To see the reference for the Azure CDN SDK for Node.js, view the [reference](http://azure.github.io/azure-sdk-for-node/azure-arm-cdn/latest/).</span></span>

<span data-ttu-id="c007e-175">Aby znaleźć dodatkową dokumentację zestawu Azure SDK dla środowiska Node.js, Wyświetl [pełne odwołanie](http://azure.github.io/azure-sdk-for-node/).</span><span class="sxs-lookup"><span data-stu-id="c007e-175">To find additional documentation on the Azure SDK for Node.js, view the [full reference](http://azure.github.io/azure-sdk-for-node/).</span></span>

<span data-ttu-id="c007e-176">Zarządzanie zasobami CDN za pomocą [PowerShell](cdn-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c007e-176">Manage your CDN resources with [PowerShell](cdn-manage-powershell.md).</span></span>

