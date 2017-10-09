---
title: "aaaCreate aplikacji czatu Node.js przy użyciu biblioteki Socket.IO w usłudze Azure App Service"
description: "Samouczek przedstawiający przy użyciu biblioteki socket.io w użyciu w aplikacji sieci web node.js hostowanej na platformie Azure."
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: c4c4af36-3ecf-4619-b586-ca90d53ce35b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 3bd7867ccc297dc0a21c7a00cc9db06358877f5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-nodejs-chat-application-with-socketio-in-azure-app-service"></a><span data-ttu-id="6cbfa-103">Tworzenie aplikacji czatu Node.js przy użyciu biblioteki Socket.IO w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="6cbfa-103">Create a Node.js chat application with Socket.IO in Azure App Service</span></span>
<span data-ttu-id="6cbfa-104">Użyciu biblioteki Socket.IO udostępnia w czasie rzeczywistym komunikacji między serwerem środowiska node.js i klientów przy użyciu protokołu WebSockets.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-104">Socket.IO provides real-time communication between your node.js server and clients using WebSockets.</span></span> <span data-ttu-id="6cbfa-105">Obsługuje ona również transportów tooother rezerwowy (na przykład długiego sondowania) współdziałających ze starszych przeglądarek.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-105">It also supports fallback tooother transports (such as long polling) that work with older browsers.</span></span> <span data-ttu-id="6cbfa-106">Ten samouczek przeprowadzi użytkownika przez proces hostingu użyciu biblioteki Socket.IO na podstawie rozmów aplikacji jako aplikacji sieci web platformy Azure, a pokazują, jak tooscale hello aplikacji przy użyciu [pamięć podręczna Redis Azure].</span><span class="sxs-lookup"><span data-stu-id="6cbfa-106">This tutorial will walk you through hosting a Socket.IO based chat application as an Azure web app, and show you how tooscale hello application using [Azure Redis Cache].</span></span> <span data-ttu-id="6cbfa-107">Aby uzyskać więcej informacji o użyciu biblioteki Socket.IO, zobacz <http://socket.io/>.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-107">For more information on Socket.IO, see <http://socket.io/>.</span></span>

> [!NOTE]
> <span data-ttu-id="6cbfa-108">Hello procedur w tym zadaniu zastosować zbyt[aplikacji usługi sieci Web aplikacji]; dla usługi w chmurze, zobacz [tworzenie aplikacji czatu Node.js przy użyciu biblioteki Socket.IO w usługi w chmurze platformy Azure].</span><span class="sxs-lookup"><span data-stu-id="6cbfa-108">hello procedures in this task apply too[App Service Web Apps]; for Cloud Services, see [Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service].</span></span>
> 
> 

## <a name="download-hello-chat-example"></a><span data-ttu-id="6cbfa-109">Pobierz przykład Witaj rozmowy</span><span class="sxs-lookup"><span data-stu-id="6cbfa-109">Download hello chat example</span></span>
<span data-ttu-id="6cbfa-110">Dla tego projektu, użyjemy przykład Witaj rozmów z hello [repozytorium GitHub użyciu biblioteki Socket.IO].</span><span class="sxs-lookup"><span data-stu-id="6cbfa-110">For this project, we will use hello chat example from hello [Socket.IO GitHub repository].</span></span> <span data-ttu-id="6cbfa-111">Wykonaj poniższy przykład hello toodownload kroki hello i dodaj go projektu toohello, utworzonych wcześniej.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-111">Perform hello following steps toodownload hello example and add it toohello project you previously created.</span></span>

1. <span data-ttu-id="6cbfa-112">Pobierz [ZIP lub GZ zarchiwizowane wersji] hello użyciu biblioteki Socket.IO projektu (wersja 1.3.5 zostało użyte dla tego dokumentu)</span><span class="sxs-lookup"><span data-stu-id="6cbfa-112">Download a [ZIP or GZ archived release] of hello Socket.IO project (version 1.3.5 was used for this document)</span></span>
2. <span data-ttu-id="6cbfa-113">Wyodrębnij hello archiwum i skopiuj hello **przykłady\\rozmów** katalogu tooa nowej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-113">Extract hello archive and copy hello **examples\\chat** directory tooa new location.</span></span> <span data-ttu-id="6cbfa-114">Na przykład  **\\węzła\\rozmów**.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-114">For example, **\\node\\chat**.</span></span>

## <a name="modify-appjs-and-install-modules"></a><span data-ttu-id="6cbfa-115">Modyfikowanie pliku app.js i zainstalować moduły</span><span class="sxs-lookup"><span data-stu-id="6cbfa-115">Modify app.js and install modules</span></span>
1. <span data-ttu-id="6cbfa-116">Zmień nazwę hello **index.js** pliku zbyt**app.js**.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-116">Rename hello **index.js** file too**app.js**.</span></span> <span data-ttu-id="6cbfa-117">Dzięki temu Azure toodetect, że jest to aplikacji Node.js.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-117">This allows Azure toodetect that this is a Node.js application.</span></span>
2. <span data-ttu-id="6cbfa-118">Otwórz hello **app.js** plik w edytorze tekstów.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-118">Open hello **app.js** file in a text editor.</span></span> <span data-ttu-id="6cbfa-119">Zmień hello wiersz zawierający `var io = require('../..')(server);` w sposób przedstawiony poniżej:</span><span class="sxs-lookup"><span data-stu-id="6cbfa-119">Change hello line containing `var io = require('../..')(server);` as shown below:</span></span>
   
       var express = require('express');
       var app = express();
       var server = require('http').createServer(app);
       // var io = require('../..')(server);
       // New:
       var io = require('socket.io')(server);
       var port = process.env.PORT || 3000;
3. <span data-ttu-id="6cbfa-120">Otwórz hello **package.json** plik i dodać toosocket.io odwołania, w obszarze `dependencies`, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="6cbfa-120">Open hello **package.json** file and add a reference toosocket.io under `dependencies`, as shown below:</span></span>
   
        "dependencies": {
          "express": "3.4.8",
          "socket.io": "1.3.5"
        }
4. <span data-ttu-id="6cbfa-121">Z wiersza polecenia hello, zmień toohello  **\\węzła\\rozmów** katalogu i użyj tooinstall hello moduły npm wymagane przez tę aplikację:</span><span class="sxs-lookup"><span data-stu-id="6cbfa-121">From hello command-line, change toohello **\\node\\chat** directory and use npm tooinstall hello modules required by this application:</span></span>
   
        npm install
   
    <span data-ttu-id="6cbfa-122">Spowoduje to zainstalowanie modułów hello do podfolderu o nazwie **node_modules**.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-122">This will install hello modules into a subfolder named **node_modules**.</span></span>

## <a name="create-an-azure-web-app"></a><span data-ttu-id="6cbfa-123">Tworzenie aplikacji sieci Web platformy Azure</span><span class="sxs-lookup"><span data-stu-id="6cbfa-123">Create an Azure Web App</span></span>
<span data-ttu-id="6cbfa-124">Wykonaj te kroki toocreate aplikacji sieci web platformy Azure, włączyć publikowanie w usłudze Git, a następnie włącz obsługę protokołu WebSocket dla aplikacji sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-124">Follow these steps toocreate an Azure web app, enable Git publishing, and then enable WebSocket support for hello web app.</span></span>

> [!NOTE]
> <span data-ttu-id="6cbfa-125">toocomplete tego samouczka jest potrzebne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-125">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="6cbfa-126">Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-126">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="6cbfa-127">Aby uzyskać szczegółowe informacje, zobacz artykuł <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">Bezpłatna wersja próbna platformy Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-127">For details, see <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">Azure Free Trial</a>.</span></span>
> 
> 

1. <span data-ttu-id="6cbfa-128">Zainstaluj hello interfejsu wiersza polecenia platformy Azure (Azure CLI), a następnie połącz tooyour subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-128">Install hello Azure Command-Line Interface (Azure CLI) and connect tooyour Azure subscription.</span></span> <span data-ttu-id="6cbfa-129">Zobacz [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="6cbfa-129">See [Install and Configure hello Azure CLI](../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="6cbfa-130">Jeśli jest to pierwszy ustawienia czasu zapasowej repozytorium na platformie Azure, należy toocreate poświadczenia logowania.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-130">If this is your first time setting up a repository in Azure, you need toocreate login credentials.</span></span> <span data-ttu-id="6cbfa-131">Z hello Azure CLI wprowadź następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="6cbfa-131">From hello Azure CLI, enter hello following command:</span></span>
   
        azure site deployment user set [username] [password]
3. <span data-ttu-id="6cbfa-132">Zmień toohello  **\\node\chat** katalogu i użyj hello następujące polecenia toocreate nowej aplikacji sieci web platformy Azure i lokalnego repozytorium Git.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-132">Change toohello **\\node\chat** directory and use hello following command toocreate a new Azure web app and a local Git repository.</span></span> <span data-ttu-id="6cbfa-133">To polecenie tworzy również Git zdalnego o nazwie "azure".</span><span class="sxs-lookup"><span data-stu-id="6cbfa-133">This command also creates a Git remote named 'azure'.</span></span>
   
        azure site create mysitename --git
   
    <span data-ttu-id="6cbfa-134">"Mysitename" należy zamienić na unikatową nazwę aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-134">You must replace 'mysitename' with a unique name for your web app.</span></span>
4. <span data-ttu-id="6cbfa-135">Zatwierdź hello istniejące pliki toohello lokalnego repozytorium przy użyciu hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="6cbfa-135">Commit hello existing files toohello local repository by using hello following commands:</span></span>
   
        git add .
        git commit -m "Initial commit"
5. <span data-ttu-id="6cbfa-136">Wypchnij repozytorium Azure Web Apps toohello pliki hello za pomocą hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="6cbfa-136">Push hello files toohello Azure Web Apps repository with hello following command:</span></span>
   
        git push azure master
   
    <span data-ttu-id="6cbfa-137">Po wyświetleniu monitu wprowadź swoje poświadczenia w kroku 2.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-137">When prompted, enter your credentials from step 2.</span></span> <span data-ttu-id="6cbfa-138">Komunikaty o stanie zostanie wyświetlony jako moduły są importowane na powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-138">You will receive status messages as modules are imported on hello server.</span></span> <span data-ttu-id="6cbfa-139">Po zakończeniu tego procesu aplikacji hello będzie udostępniana w aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-139">Once this process has completed, hello application will be hosted on your Azure web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6cbfa-140">Podczas instalacji modułu mogą pojawić się błędy który "hello... zaimportowanego projektu nie został znaleziony '.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-140">During module installation, you may notice errors that 'hello imported project ... was not found'.</span></span> <span data-ttu-id="6cbfa-141">Te można bezpiecznie zignorować.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-141">These can safely be ignored.</span></span>
   > 
   > 
6. <span data-ttu-id="6cbfa-142">Użyciu biblioteki Socket.IO używa protokołu Websocket, które nie są włączone domyślnie na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-142">Socket.IO uses WebSockets, which are not enabled by default on Azure.</span></span> <span data-ttu-id="6cbfa-143">tooenable gniazda sieci web, należy użyć następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="6cbfa-143">tooenable web sockets, use hello following command:</span></span>
   
        azure site set -w
   
    <span data-ttu-id="6cbfa-144">Jeśli zostanie wyświetlony monit, wprowadź nazwę hello hello aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-144">If prompted, enter hello name of hello web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6cbfa-145">Witaj "set -w witrynie azure" zostanie polecenie pracować tylko z wersji 0.7.4 lub nowszej hello interfejsu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-145">hello 'azure site set -w' command will work only with version 0.7.4 or higher of hello Azure Command-Line Interface.</span></span> <span data-ttu-id="6cbfa-146">Można również włączyć obsługę protokołu WebSocket przy użyciu hello [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6cbfa-146">You can also enable WebSocket support using hello [Azure Portal](https://portal.azure.com).</span></span>
   > 
   > <span data-ttu-id="6cbfa-147">przy użyciu protokołu WebSockets tooenable hello portalu Azure kliknij hello aplikacji sieci web z hello blok aplikacje sieci Web, kliknij przycisk **wszystkie ustawienia** > **ustawienia aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-147">tooenable WebSockets using hello Azure Portal, click hello web app from hello Web Apps blade, click **All settings** > **Application settings**.</span></span> <span data-ttu-id="6cbfa-148">W obszarze **gniazda sieci Web**, kliknij przycisk **na**.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-148">Under **Web Sockets**, click **On**.</span></span> <span data-ttu-id="6cbfa-149">Następnie kliknij przycisk **Save** (Zapisz).</span><span class="sxs-lookup"><span data-stu-id="6cbfa-149">Then click **Save**.</span></span>
   > 
   > 
7. <span data-ttu-id="6cbfa-150">aplikacji sieci web hello tooview po hello w usłudze Azure, użyj polecenia toolaunch przeglądarki sieci web i przejdź toohello hostowanych aplikacji sieci web:</span><span class="sxs-lookup"><span data-stu-id="6cbfa-150">tooview hello web app on Azure, use hello following command toolaunch your web browser and navigate toohello hosted web app:</span></span>
   
        azure site browse

<span data-ttu-id="6cbfa-151">Aplikacja jest teraz uruchomiona na platformie Azure i możliwość przekazywania wiadomości między różnych klientów przy użyciu użyciu biblioteki Socket.IO.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-151">Your app is now running on Azure, and can relay chat messages between different clients using Socket.IO.</span></span>

## <a name="scale-out"></a><span data-ttu-id="6cbfa-152">Skalowanie w poziomie</span><span class="sxs-lookup"><span data-stu-id="6cbfa-152">Scale out</span></span>
<span data-ttu-id="6cbfa-153">Użyciu biblioteki Socket.IO aplikacji może być skalowana w poziomie za pomocą **karty** toodistribute wiadomości i zdarzenia między wiele wystąpień aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-153">Socket.IO applications can be scaled out by using an **adapter** toodistribute messages and events between multiple application instances.</span></span> <span data-ttu-id="6cbfa-154">Mimo że dostępnych jest kilka kart, hello [redis użyciu biblioteki socket.io] karty mogą być łatwo używane z funkcją pamięć podręczna Redis Azure hello.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-154">While there are several adapters available, hello [socket.io-redis] adapter can be easily used with hello Azure Redis Cache feature.</span></span>

> [!NOTE]
> <span data-ttu-id="6cbfa-155">Dodatkowe wymagania dla skalowania rozwiązania użyciu biblioteki Socket.IO jest obsługa trwałe sesje.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-155">An additional requirement for scaling out a Socket.IO solution is support for sticky sessions.</span></span> <span data-ttu-id="6cbfa-156">Trwałe sesje są domyślnie włączone dla aplikacji sieci Web platformy Azure za pośrednictwem Routing żądań Azure.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-156">Sticky sessions are enabled by default for Azure Web Apps through Azure Request Routing.</span></span> <span data-ttu-id="6cbfa-157">Aby uzyskać więcej informacji, zobacz [wystąpienia koligacji w Azure Web Sites].</span><span class="sxs-lookup"><span data-stu-id="6cbfa-157">For more information, see [Instance Affinity in Azure Web Sites].</span></span>
> 
> 

### <a name="create-a-redis-cache"></a><span data-ttu-id="6cbfa-158">Tworzenie pamięci podręcznej Redis</span><span class="sxs-lookup"><span data-stu-id="6cbfa-158">Create a Redis cache</span></span>
<span data-ttu-id="6cbfa-159">Wykonaj kroki opisane hello w [tworzenia pamięci podręcznej w pamięci podręcznej Redis Azure] toocreate nowej pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-159">Perform hello steps in [Create a cache in Azure Redis Cache] toocreate a new cache.</span></span>

> [!NOTE]
> <span data-ttu-id="6cbfa-160">Zapisz hello **nazwy hosta** i **klucz podstawowy** dla pamięci podręcznej, ponieważ będą one potrzebne w hello następnych kroków.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-160">Save hello **Host name** and **Primary key** for your cache, as these will be needed in hello next steps.</span></span>
> 
> 

### <a name="add-hello-redis-and-socketio-redis-modules"></a><span data-ttu-id="6cbfa-161">Dodaj hello redis i użyciu biblioteki socket.io redis modułów</span><span class="sxs-lookup"><span data-stu-id="6cbfa-161">Add hello redis and socket.io-redis modules</span></span>
1. <span data-ttu-id="6cbfa-162">W wierszu polecenia Zmień toohello  **\\węzła\\rozmów** hello katalogu i użyj następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-162">From a command-line, change toohello **\\node\\chat** directory and use hello following command.</span></span>
   
        npm install socket.io-redis@0.1.4 redis@0.12.1 --save
   
   > [!NOTE]
   > <span data-ttu-id="6cbfa-163">wersje Hello określone w tym poleceniu są używane podczas testowania w tym artykule wersje hello.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-163">hello versions specified in this command are hello versions used when testing this article.</span></span>
   > 
   > 
2. <span data-ttu-id="6cbfa-164">Modyfikowanie hello **app.js** pliku tooadd hello następujące wiersze natychmiast po`var io = require('socket.io')(server);`</span><span class="sxs-lookup"><span data-stu-id="6cbfa-164">Modify hello **app.js** file tooadd hello following lines immediately after `var io = require('socket.io')(server);`</span></span>
   
        var pub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
        var sub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
   
        var redis = require('socket.io-redis');
        io.adapter(redis({pubClient: pub, subClient: sub}));
   
    <span data-ttu-id="6cbfa-165">Zastąp **redishostname** i **rediskey** z nazwą hosta hello i klucza pamięci podręcznej Redis.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-165">Replace **redishostname** and **rediskey** with hello host name and key for your Redis cache.</span></span>
   
    <span data-ttu-id="6cbfa-166">Spowoduje to utworzenie Publikuj i Subskrybuj toohello klienta pamięci podręcznej Redis utworzone wcześniej.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-166">This will create a publish and subscribe client toohello Redis cache created previously.</span></span> <span data-ttu-id="6cbfa-167">Klienci Hello są następnie używane z tooconfigure karty hello hello toouse użyciu biblioteki Socket.IO pamięć podręczna Redis do przekazywania wiadomości i zdarzenia między wystąpieniami aplikacji</span><span class="sxs-lookup"><span data-stu-id="6cbfa-167">hello clients are then used with hello adapter tooconfigure Socket.IO toouse hello Redis cache for passing messages and events between instances of your application</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6cbfa-168">Podczas hello **redis użyciu biblioteki socket.io** karty może komunikować się bezpośrednio tooRedis, hello bieżąca wersja nie obsługuje uwierzytelniania hello wymagane przez pamięci podręcznej Azure Redis.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-168">While hello **socket.io-redis** adapter can communicate directly tooRedis, hello current version does not support hello authentication required by Azure Redis cache.</span></span> <span data-ttu-id="6cbfa-169">Dlatego połączenia początkowego hello jest tworzony przy użyciu hello **redis** modułu, następnie powitania klienta jest przekazywany toohello **redis użyciu biblioteki socket.io** karty.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-169">So hello initial connection is created using hello **redis** module, then hello client is passed toohello **socket.io-redis** adapter.</span></span>
   > 
   > <span data-ttu-id="6cbfa-170">Pamięć podręczna Redis Azure obsługuje bezpiecznych połączeń przy użyciu portu 6380, moduły hello używane w tym przykładzie nie obsługują bezpiecznych połączeń wersji 2014-7-14.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-170">While Azure Redis Cache supports secure connections using port 6380, hello modules used in this example do not support secure connections as of 7/14/2014.</span></span> <span data-ttu-id="6cbfa-171">Hello powyżej kod używa hello domyślnie niezabezpieczone port 6379.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-171">hello above code uses hello default, unsecure port of 6379.</span></span>
   > 
   > 
3. <span data-ttu-id="6cbfa-172">Witaj Zapisz zmodyfikowany **app.js**</span><span class="sxs-lookup"><span data-stu-id="6cbfa-172">Save hello modified **app.js**</span></span>

### <a name="commit-changes-and-redeploy"></a><span data-ttu-id="6cbfa-173">Zatwierdź zmiany i ponownie wdrożyć</span><span class="sxs-lookup"><span data-stu-id="6cbfa-173">Commit changes and redeploy</span></span>
<span data-ttu-id="6cbfa-174">Z wiersza polecenia w hello hello  **\\węzła\\rozmów** katalogu, użyj hello następujące zmiany toocommit poleceń i wdrożenie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-174">From hello command-line in hello **\\node\\chat** directory, use hello following commands toocommit changes and redeploy hello application.</span></span>

    git add .
    git commit -m "implementing scale out"
    git push azure master

<span data-ttu-id="6cbfa-175">Po hello zmiany mają został naciśnięty toohello serwera, witryny można skalować w wielu wystąpieniach za pomocą następującego polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-175">Once hello changes have been pushed toohello server, you can scale your site across multiple instances by using hello following command.</span></span>

    azure site scale instances --instances #

<span data-ttu-id="6cbfa-176">Gdzie  **#**  hello liczbę wystąpień toocreate.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-176">Where **#** is hello number of instances toocreate.</span></span>

<span data-ttu-id="6cbfa-177">Aplikacja sieci web tooyour można połączyć z wielu tooverify przeglądarki lub komputery, które są prawidłowo wysyłane tooall klientów.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-177">You can connect tooyour web app from multiple browsers or computers tooverify that messages are correctly sent tooall clients.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="6cbfa-178">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="6cbfa-178">Troubleshooting</span></span>
### <a name="connection-limits"></a><span data-ttu-id="6cbfa-179">Limity połączeń</span><span class="sxs-lookup"><span data-stu-id="6cbfa-179">Connection limits</span></span>
<span data-ttu-id="6cbfa-180">Aplikacje sieci Web platformy Azure są dostępne w wielu jednostki magazynowe, które określają hello zasoby dostępne tooyour lokacji.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-180">Azure Web Apps is available in multiple SKUs, which determine hello resources available tooyour site.</span></span> <span data-ttu-id="6cbfa-181">W tym hello liczbę dozwolonych połączeń protokołu WebSocket.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-181">This includes hello number of allowed WebSocket connections.</span></span> <span data-ttu-id="6cbfa-182">Aby uzyskać więcej informacji, zobacz hello [stronie cennika usługi sieci Web Apps].</span><span class="sxs-lookup"><span data-stu-id="6cbfa-182">For more information, see hello [Web Apps Pricing page].</span></span>

### <a name="messages-arent-being-sent-using-websockets"></a><span data-ttu-id="6cbfa-183">Komunikaty nie są wysyłane przy użyciu protokołu WebSockets</span><span class="sxs-lookup"><span data-stu-id="6cbfa-183">Messages aren't being sent using WebSockets</span></span>
<span data-ttu-id="6cbfa-184">Jeśli przeglądarka klienta zachować nastąpi powrót toolong sondowania zamiast Websocket, może być ze względu na jedną z następujących hello.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-184">If client browsers keep falling back toolong polling instead of using WebSockets, it may be because of one of hello following.</span></span>

* <span data-ttu-id="6cbfa-185">**Spróbuj ograniczyć hello transportu toojust WebSockets**</span><span class="sxs-lookup"><span data-stu-id="6cbfa-185">**Try limiting hello transport toojust WebSockets**</span></span>
  
    <span data-ttu-id="6cbfa-186">Aby toouse użyciu biblioteki Socket.IO Websocket jako hello transportu do obsługi komunikatów zarówno powitania serwera i klienta muszą obsługiwać protokół WebSockets.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-186">In order for Socket.IO toouse WebSockets as hello messaging transport, both hello server and client must support WebSockets.</span></span> <span data-ttu-id="6cbfa-187">Jeśli co najmniej hello innych nie, użyciu biblioteki Socket.IO będzie negocjował innego transportu, takich jak długiego sondowania.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-187">If one or hello other does not, Socket.IO will negotiate another transport, such as long polling.</span></span> <span data-ttu-id="6cbfa-188">Witaj domyślna lista transportów używany przy użyciu biblioteki Socket.IO ` websocket, htmlfile, xhr-polling, jsonp-polling`.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-188">hello default list of transports used by Socket.IO is ` websocket, htmlfile, xhr-polling, jsonp-polling`.</span></span> <span data-ttu-id="6cbfa-189">Aby wymusić użycie tooonly Websocket przez dodanie powitania po toohello kodu **app.js** pliku po hello wiersz zawierający `, nicknames = {};`.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-189">You can force it tooonly use WebSockets by adding hello following code toohello **app.js** file, after hello line containing `, nicknames = {};`.</span></span>
  
        io.configure(function() {
          io.set('transports', ['websocket']);
        });
  
  > [!NOTE]
  > <span data-ttu-id="6cbfa-190">Należy pamiętać, że starszych przeglądarek, które nie obsługują protokół WebSockets nie będą mogli tooconnect toohello lokacji podczas hello powyżej kodu jest aktywny, ponieważ ogranicza komunikację tooWebSockets tylko.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-190">Note that older browsers that do not support WebSockets will not be able tooconnect toohello site while hello above code is active, as it restricts communication tooWebSockets only.</span></span>
  > 
  > 
* <span data-ttu-id="6cbfa-191">**Użyj protokołu SSL**</span><span class="sxs-lookup"><span data-stu-id="6cbfa-191">**Use SSL**</span></span>
  
    <span data-ttu-id="6cbfa-192">Protokół WebSockets opiera się na niektórych mniejszym używane nagłówków HTTP, takie jak hello **uaktualnienia** nagłówka.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-192">WebSockets relies on some lesser used HTTP headers, such as hello **Upgrade** header.</span></span> <span data-ttu-id="6cbfa-193">Niektóre urządzenia sieci pośredniczącej, takich jak serwer proxy sieci web, może spowodować usunięcie tych nagłówków.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-193">Some intermediate network devices, such as web proxies, may remove these headers.</span></span> <span data-ttu-id="6cbfa-194">tooavoid ten problem, można ustanowić połączenia obiektu WebSocket hello za pośrednictwem protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-194">tooavoid this problem, you can establish hello WebSocket connection over SSL.</span></span>
  
    <span data-ttu-id="6cbfa-195">Tooaccomplish łatwo jest zbyt tooconfigure użyciu biblioteki Socket.IO`match origin protocol`.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-195">An easy way tooaccomplish this is tooconfigure Socket.IO too`match origin protocol`.</span></span> <span data-ttu-id="6cbfa-196">To powoduje, że użyciu biblioteki Socket.IO toosecure Websocket komunikacji hello identyczny hello pochodzących HTTP/HTTPS Żądanie hello strony sieci web.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-196">This instructs Socket.IO toosecure WebSockets communication hello same as hello originating HTTP/HTTPS request for hello web page.</span></span> <span data-ttu-id="6cbfa-197">Jeśli przeglądarka używa toovisit adres HTTPS URL witryny sieci Web, kolejne komunikacji protokołu WebSocket za pośrednictwem użyciu biblioteki Socket.IO będą chronione za pośrednictwem protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-197">If a browser uses an HTTPS URL toovisit your website, subsequent WebSocket communications through Socket.IO will be secured over SSL.</span></span>
  
    <span data-ttu-id="6cbfa-198">toomodify tooenable w tym przykładzie tę konfigurację, Dodaj hello następującego kodu toohello **app.js** plik po hello wiersz zawierający `, nicknames = {};`.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-198">toomodify this example tooenable this configuration, add hello following code toohello **app.js** file after hello line containing `, nicknames = {};`.</span></span>
  
        io.configure(function() {
          io.set('match origin protocol', true);
        });
* <span data-ttu-id="6cbfa-199">**Sprawdź ustawienia pliku web.config**</span><span class="sxs-lookup"><span data-stu-id="6cbfa-199">**Verify web.config settings**</span></span>
  
    <span data-ttu-id="6cbfa-200">Aplikacje sieci web platformy Azure, które obsługę aplikacji programu Node.js Użyj hello **web.config** tooroute plików przychodzących żądań toohello aplikacji Node.js.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-200">Azure web apps that host Node.js applications use hello **web.config** file tooroute incoming requests toohello Node.js application.</span></span> <span data-ttu-id="6cbfa-201">Dla toofunction Websocket poprawnie z aplikacji programu Node.js, hello **web.config** musi zawierać hello wejścia.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-201">For WebSockets toofunction correctly with Node.js applications, hello **web.config** must contain hello following entry.</span></span>
  
        <webSocket enabled="false"/>
  
    <span data-ttu-id="6cbfa-202">Powoduje wyłączenie hello moduł Websocket usług IIS, który zawiera własną implementację Websocket i powoduje konflikt z Node.js określone moduły protokołu WebSocket, takich jak użyciu biblioteki Socket.IO.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-202">This disables hello IIS WebSockets module, which includes its own implementation of WebSockets and conflicts with Node.js specific WebSocket modules such as Socket.IO.</span></span> <span data-ttu-id="6cbfa-203">Jeśli ten wiersz nie jest obecny lub jest zbyt`true`, może to być powód hello hello transportu protokołu WebSocket nie działa dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-203">If this line is not present, or is set too`true`, this may be hello reason that hello WebSocket transport is not working for your application.</span></span>
  
    <span data-ttu-id="6cbfa-204">Zwykle nie dołączaj aplikacji Node.js **web.config** pliku, więc witryn sieci Web Azure automatycznie generuje jeden dla aplikacji programu Node.js podczas ich wdrażania.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-204">Normally, Node.js applications do not include a **web.config** file, so Azure Websites will automatically generate one for Node.js applications when they are deployed.</span></span> <span data-ttu-id="6cbfa-205">Ponieważ ten plik jest automatycznie generowany na powitania serwera, należy użyć hello FTP i FTPS adres URL dla Twojej witryny sieci Web tooview tego pliku.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-205">Since this file is automatically generated on hello server, you must use hello FTP or FTPS URL for your website tooview this file.</span></span> <span data-ttu-id="6cbfa-206">Znajdowanie hello FTP i FTPS adres URL witryny w portalu klasycznym hello przez wybranie aplikacji sieci web i następnie hello **pulpitu nawigacyjnego** łącza.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-206">You can find hello FTP and FTPS URLs for your site in hello classic portal by selecting your web app, and then hello **Dashboard** link.</span></span> <span data-ttu-id="6cbfa-207">Witaj adresy URL są wyświetlane w hello **szybkiego dostępu** sekcji.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-207">hello URLs are displayed in hello **quick glance** section.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="6cbfa-208">Witaj **web.config** pliku tylko jest generowany przez usługę Azure Websites, jeśli aplikacja nie zapewnia.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-208">hello **web.config** file is only generated by Azure Websites if your application does not provide one.</span></span> <span data-ttu-id="6cbfa-209">Jeśli podasz **web.config** pliku w katalogu głównym hello projektu aplikacji, będzie używany przez aplikacje sieci Web Azure.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-209">If you provide a **web.config** file in hello root of your application project, it will be used by Azure Web Apps.</span></span>
  > 
  > 
  
    <span data-ttu-id="6cbfa-210">Hello wpis nie jest obecny, czy ustawiono wartość tooa `true`, a następnie należy utworzyć **web.config** w hello katalogu głównego aplikacji Node.js i określ wartość `false`.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-210">If hello entry is not present, or is set tooa value of `true`, then you should create a **web.config** in hello root of your Node.js application and specify a value of `false`.</span></span>  <span data-ttu-id="6cbfa-211">Odwołania, poniżej hello jest domyślnie **web.config** dla aplikacji, która używa **app.js** jako punkt wejścia hello.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-211">For reference, hello below is a default **web.config** for an application that uses **app.js** as hello entry point.</span></span>
  
        <?xml version="1.0" encoding="utf-8"?>
        <!--
             This configuration file is required if iisnode is used toorun node processes behind
             IIS or IIS Express.  For more information, visit:
  
             https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config
        -->
  
        <configuration>
          <system.webServer>
            <!-- Visit http://blogs.msdn.com/b/windowsazure/archive/2013/11/14/introduction-to-websockets-on-windows-azure-web-sites.aspx for more information on WebSocket support -->
            <webSocket enabled="false" />
            <handlers>
              <!-- Indicates that hello server.js file is a node.js web app toobe handled by hello iisnode module -->
              <add name="iisnode" path="app.js" verb="*" modules="iisnode"/>
            </handlers>
            <rewrite>
              <rules>
                <!-- Do not interfere with requests for node-inspector debugging -->
                <rule name="NodeInspector" patternSyntax="ECMAScript" stopProcessing="true">
                  <match url="^app.js\/debug[\/]?" />
                </rule>
  
                <!-- First we consider whether hello incoming URL matches a physical file in hello /public folder -->
                <rule name="StaticContent">
                  <action type="Rewrite" url="public{REQUEST_URI}"/>
                </rule>
  
                <!-- All other URLs are mapped toohello node.js web app entry point -->
                <rule name="DynamicContent">
                  <conditions>
                    <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="True"/>
                  </conditions>
                  <action type="Rewrite" url="app.js"/>
                </rule>
              </rules>
            </rewrite>
            <!--
              You can control how Node is hosted within IIS using hello following options:
                * watchedFiles: semi-colon separated list of files that will be watched for changes toorestart hello server
                * node_env: will be propagated toonode as NODE_ENV environment variable
                * debuggingEnabled - controls whether hello built-in debugger is enabled
  
              See https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config for a full list of options
            -->
            <!--<iisnode watchedFiles="web.config;*.js"/>-->
          </system.webServer>
        </configuration>
  
    <span data-ttu-id="6cbfa-212">Jeśli aplikacja używa innej niż punkt wejścia **app.js**, musisz zastąpić wszystkie wystąpienia **app.js** z hello Popraw punktu wejścia.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-212">If your application uses an entry point other than **app.js**, you must replace all occurrences of **app.js** with hello correct entry point.</span></span> <span data-ttu-id="6cbfa-213">Na przykład, zastępując **app.js** z **server.js**.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-213">For example, replacing **app.js** with **server.js**.</span></span>

> [!NOTE]
> <span data-ttu-id="6cbfa-214">Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service], gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-214">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service], where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="6cbfa-215">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-215">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="6cbfa-216">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6cbfa-216">Next steps</span></span>
<span data-ttu-id="6cbfa-217">W tym samouczku przedstawiono sposób toocreate aplikacji czatu hostowanej w aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-217">In this tutorial you learned how toocreate a chat application hosted in an Azure web app.</span></span> <span data-ttu-id="6cbfa-218">Może również obsługiwać tę aplikację jako usługi w chmurze platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-218">You can also host this application as an Azure Cloud Service.</span></span> <span data-ttu-id="6cbfa-219">Instrukcje na temat tooaccomplish tego, zobacz [tworzenie aplikacji czatu Node.js przy użyciu biblioteki Socket.IO w usługi w chmurze platformy Azure].</span><span class="sxs-lookup"><span data-stu-id="6cbfa-219">For steps on how tooaccomplish this, see [Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service].</span></span>

<span data-ttu-id="6cbfa-220">Aby uzyskać więcej informacji, zobacz też hello [Centrum deweloperów środowiska Node.js].</span><span class="sxs-lookup"><span data-stu-id="6cbfa-220">For more information, see also hello [Node.js Developer Center].</span></span>

## <a name="whats-changed"></a><span data-ttu-id="6cbfa-221">Co zostało zmienione</span><span class="sxs-lookup"><span data-stu-id="6cbfa-221">What's changed</span></span>
* <span data-ttu-id="6cbfa-222">Toohello przewodnik zmiany z tooApp witryn sieci Web usługi dla: [usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure].</span><span class="sxs-lookup"><span data-stu-id="6cbfa-222">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services].</span></span>

<!-- URL List -->

[pamięć podręczna Redis Azure]: /documentation/services/redis-cache/
[aplikacji usługi sieci Web aplikacji]: http://go.microsoft.com/fwlink/?LinkId=529714
[stronie cennika usługi sieci Web Apps]: http://go.microsoft.com/fwlink/?LinkId=511643
[tworzenie aplikacji czatu Node.js przy użyciu biblioteki Socket.IO w usługi w chmurze platformy Azure]: ../cloud-services/cloud-services-nodejs-chat-app-socketio.md
[Install and Configure hello Azure CLI]: ../cli-install-nodejs.md
[usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure]: http://go.microsoft.com/fwlink/?LinkId=529714
[Centrum deweloperów środowiska Node.js]: /develop/nodejs/
[Wypróbuj usługę App Service]: https://azure.microsoft.com/try/app-service/
[wystąpienia koligacji w Azure Web Sites]: https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/
[tworzenia pamięci podręcznej w pamięci podręcznej Redis Azure]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md

[redis użyciu biblioteki socket.io]: https://github.com/socketio/socket.io-redis
[repozytorium GitHub użyciu biblioteki Socket.IO]: https://github.com/socketio/socket.io
[ZIP lub GZ zarchiwizowane wersji]: https://github.com/socketio/socket.io/releases

<!-- IMG List -->

[chat-example-view]: ./media/web-sites-nodejs-chat-app-socketio/socketio-2.png
[npm-output]: ./media/web-sites-nodejs-chat-app-socketio/socketio-7.png
[completed-app]: ./media/web-sites-nodejs-chat-app-socketio/websitesocketcomplete.png
