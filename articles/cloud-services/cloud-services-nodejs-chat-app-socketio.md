---
title: "aaaNode.js aplikacji przy użyciu użyciu biblioteki Socket.io | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse użyciu biblioteki socket.io w aplikacji node.js hostowanej na platformie Azure."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 7f9435e0-7732-4aa1-a4df-ea0e894b847f
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 47c6c4a748938959315b880340f41f31faab4ea9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-chat-application-with-socketio-on-an-azure-cloud-service"></a><span data-ttu-id="6eaf6-103">Tworzenie aplikacji czatu Node.js przy użyciu biblioteki Socket.IO w usłudze chmury Azure</span><span class="sxs-lookup"><span data-stu-id="6eaf6-103">Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service</span></span>
<span data-ttu-id="6eaf6-104">Użyciu biblioteki Socket.IO zapewnia czasu rzeczywistego komunikacji między między serwerem środowiska node.js i klientami.</span><span class="sxs-lookup"><span data-stu-id="6eaf6-104">Socket.IO provides realtime communication between between your node.js server and clients.</span></span> <span data-ttu-id="6eaf6-105">W tym samouczku opisano za pośrednictwem obsługi gniazda. We/Wy na podstawie rozmów aplikacji na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="6eaf6-105">This tutorial will walk you through hosting a socket.IO based chat application on Azure.</span></span> <span data-ttu-id="6eaf6-106">Aby uzyskać więcej informacji o użyciu biblioteki Socket.IO, zobacz <http://socket.io/>.</span><span class="sxs-lookup"><span data-stu-id="6eaf6-106">For more information on Socket.IO, see <http://socket.io/>.</span></span>

<span data-ttu-id="6eaf6-107">Zrzut ekranu aplikacji hello ukończone znajduje się poniżej:</span><span class="sxs-lookup"><span data-stu-id="6eaf6-107">A screenshot of hello completed application is below:</span></span>

![Okno przeglądarki zawierające hello usługi hostowanej na platformie Azure][completed-app]  

## <a name="prerequisites"></a><span data-ttu-id="6eaf6-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6eaf6-109">Prerequisites</span></span>
<span data-ttu-id="6eaf6-110">Upewnij się, że hello następujące produkty i wersje to przykład Witaj pełną toosuccessfully zainstalowanych w tym artykule:</span><span class="sxs-lookup"><span data-stu-id="6eaf6-110">Ensure that hello following products and versions are installed toosuccessfully complete hello example in this article:</span></span>

* <span data-ttu-id="6eaf6-111">Zainstalować program [Visual Studio](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx)</span><span class="sxs-lookup"><span data-stu-id="6eaf6-111">Install [Visual Studio](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx)</span></span>
* <span data-ttu-id="6eaf6-112">Zainstalować środowisko [Node.js](https://nodejs.org/download/).</span><span class="sxs-lookup"><span data-stu-id="6eaf6-112">Install [Node.js](https://nodejs.org/download/)</span></span>
* <span data-ttu-id="6eaf6-113">Zainstaluj [2.7.10 wersji języka Python](https://www.python.org/)</span><span class="sxs-lookup"><span data-stu-id="6eaf6-113">Install [Python version 2.7.10](https://www.python.org/)</span></span>

## <a name="create-a-cloud-service-project"></a><span data-ttu-id="6eaf6-114">Tworzenie projektu usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="6eaf6-114">Create a Cloud Service Project</span></span>
<span data-ttu-id="6eaf6-115">Witaj następujące kroki tworzenia projektu usługi w chmurze hello obsługującym hello użyciu biblioteki Socket.IO aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6eaf6-115">hello following steps create hello cloud service project that will host hello Socket.IO application.</span></span>

1. <span data-ttu-id="6eaf6-116">Z hello **Start Menu** lub **ekranu startowego**, wyszukaj **programu Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="6eaf6-116">From hello **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span> <span data-ttu-id="6eaf6-117">Na koniec kliknij prawym przyciskiem myszy **programu Windows PowerShell** i wybierz **Uruchom jako Administrator**.</span><span class="sxs-lookup"><span data-stu-id="6eaf6-117">Finally, right-click **Windows PowerShell** and select **Run As Administrator**.</span></span>
   
    ![Ikona Azure PowerShell][powershell-menu]
2. <span data-ttu-id="6eaf6-119">Utwórz katalog o nazwie **c:\\węzła**.</span><span class="sxs-lookup"><span data-stu-id="6eaf6-119">Create a directory called **c:\\node**.</span></span> 
   
        PS C:\> md node
3. <span data-ttu-id="6eaf6-120">Zmień katalogi toohello **c:\\węzła** katalogu</span><span class="sxs-lookup"><span data-stu-id="6eaf6-120">Change directories toohello **c:\\node** directory</span></span>
   
        PS C:\> cd node
4. <span data-ttu-id="6eaf6-121">Wprowadź hello następujące polecenia toocreate nowego rozwiązania o nazwie **chatapp** i rolę procesu roboczego o nazwie **WorkerRole1**:</span><span class="sxs-lookup"><span data-stu-id="6eaf6-121">Enter hello following commands toocreate a new solution named **chatapp** and a worker role named **WorkerRole1**:</span></span>
   
        PS C:\node> New-AzureServiceProject chatapp
        PS C:\Node> Add-AzureNodeWorkerRole
   
    <span data-ttu-id="6eaf6-122">Zostanie wyświetlony powitania po odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="6eaf6-122">You will see hello following response:</span></span>
   
    ![dane wyjściowe Hello hello nowy azureservice i Dodaj azurenodeworkerrolecmdlets](./media/cloud-services-nodejs-chat-app-socketio/socketio-1.png)

## <a name="download-hello-chat-example"></a><span data-ttu-id="6eaf6-124">Pobierz hello przykład rozmowy</span><span class="sxs-lookup"><span data-stu-id="6eaf6-124">Download hello Chat Example</span></span>
<span data-ttu-id="6eaf6-125">Dla tego projektu, użyjemy przykład Witaj rozmów z hello [repozytorium GitHub użyciu biblioteki Socket.IO].</span><span class="sxs-lookup"><span data-stu-id="6eaf6-125">For this project, we will use hello chat example from hello [Socket.IO GitHub repository].</span></span> <span data-ttu-id="6eaf6-126">Wykonaj poniższy przykład hello toodownload kroki hello i dodaj go projektu toohello, utworzonych wcześniej.</span><span class="sxs-lookup"><span data-stu-id="6eaf6-126">Perform hello following steps toodownload hello example and add it toohello project you previously created.</span></span>

1. <span data-ttu-id="6eaf6-127">Utwórz lokalną kopię hello repozytorium używając hello **klonowania** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6eaf6-127">Create a local copy of hello repository by using hello **Clone** button.</span></span> <span data-ttu-id="6eaf6-128">Można także użyć hello **ZIP** przycisk toodownload hello projektu.</span><span class="sxs-lookup"><span data-stu-id="6eaf6-128">You may also use hello **ZIP** button toodownload hello project.</span></span>
   
   ![Wyświetlanie https://github.com/LearnBoost/socket.io/tree/master/examples/chat, ikoną hello ZIP pobrać wyróżniony oknie przeglądarki][chat-example-view]
2. <span data-ttu-id="6eaf6-130">Przejdź struktura katalogów hello hello lokalnego repozytorium, dopóki przyjeździe hello **przykłady\\rozmów** katalogu.</span><span class="sxs-lookup"><span data-stu-id="6eaf6-130">Navigate hello directory structure of hello local repository until you arrive at hello **examples\\chat** directory.</span></span> <span data-ttu-id="6eaf6-131">Kopiuj zawartość tego katalogu toothe hello **C:\\węzła\\chatapp\\WorkerRole1** Katalog utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="6eaf6-131">Copy hello contents of this directory toothe **C:\\node\\chatapp\\WorkerRole1** directory created earlier.</span></span>
   
   ![Explorer wyświetlanie zawartości hello przykłady hello\\wyodrębnione z archiwum hello katalogu rozmowy][chat-contents]
   
   <span data-ttu-id="6eaf6-133">Witaj zaznaczone elementy na powitania zrzucie ekranu pokazano powyżej są hello plików skopiowanych z hello **przykłady\\rozmów** katalogu</span><span class="sxs-lookup"><span data-stu-id="6eaf6-133">hello highlighted items in hello screenshot above are hello files copied from hello **examples\\chat** directory</span></span>
3. <span data-ttu-id="6eaf6-134">W hello **C:\\węzła\\chatapp\\WorkerRole1** katalogu, Usuń hello **server.js** pliku, a następnie zmień hello **app.js**pliku zbyt**server.js**.</span><span class="sxs-lookup"><span data-stu-id="6eaf6-134">In hello **C:\\node\\chatapp\\WorkerRole1** directory, delete hello **server.js** file, and then rename hello **app.js** file too**server.js**.</span></span> <span data-ttu-id="6eaf6-135">Spowoduje to usunięcie domyślnej hello **server.js** plik utworzony wcześniej przez hello **AzureNodeWorkerRole Dodaj** polecenia cmdlet i zastępuje go przy użyciu aplikacji hello plik hello przykład rozmowy.</span><span class="sxs-lookup"><span data-stu-id="6eaf6-135">This removes hello default **server.js** file created previously by hello **Add-AzureNodeWorkerRole** cmdlet and replaces it with hello application file from hello chat example.</span></span>

### <a name="modify-serverjs-and-install-modules"></a><span data-ttu-id="6eaf6-136">Modyfikowanie Server.js i zainstalować moduły</span><span class="sxs-lookup"><span data-stu-id="6eaf6-136">Modify Server.js and Install Modules</span></span>
<span data-ttu-id="6eaf6-137">Przed testowania aplikacji hello w hello Azure emulator firma Microsoft wprowadzać niektórych drobne zmiany.</span><span class="sxs-lookup"><span data-stu-id="6eaf6-137">Before testing hello application in hello Azure emulator, we must make some minor modifications.</span></span> <span data-ttu-id="6eaf6-138">Wykonaj hello następującego pliku server.js toothe kroki:</span><span class="sxs-lookup"><span data-stu-id="6eaf6-138">Perform hello following steps toothe server.js file:</span></span>

1. <span data-ttu-id="6eaf6-139">Otwórz hello **server.js** pliku w Visual Studio lub w dowolnym edytorze tekstów.</span><span class="sxs-lookup"><span data-stu-id="6eaf6-139">Open hello **server.js** file in Visual Studio or any text editor.</span></span>
2. <span data-ttu-id="6eaf6-140">Znajdź hello **zależności modułu** sekcji początku hello server.js i zmienić hello wiersz zawierający **sio = require('.. //.. lib//Socket.IO ")** za**sio = require('socket.io')** w sposób przedstawiony poniżej:</span><span class="sxs-lookup"><span data-stu-id="6eaf6-140">Find hello **Module dependencies** section at hello beginning of server.js and change hello line containing **sio = require('..//..//lib//socket.io')** too**sio = require('socket.io')** as shown below:</span></span>
   
       var express = require('express')
         , stylus = require('stylus')
         , nib = require('nib')
       //, sio = require('..//..//lib//socket.io'); //Original
         , sio = require('socket.io');                //Updated
         var port = process.env.PORT || 3000;         //Updated
3. <span data-ttu-id="6eaf6-141">Aplikacja hello tooensure nasłuchuje na porcie poprawne hello, Otwórz w Notatniku lub ulubionego edytora server.js, a następnie zmień następujący wiersz zastępując **3000** z **process.env.port** pokazany poniżej:</span><span class="sxs-lookup"><span data-stu-id="6eaf6-141">tooensure hello application listens on hello correct port, open server.js in Notepad or your favorite editor, and then change the following line by replacing **3000** with **process.env.port** as shown below:</span></span>
   
       //app.listen(3000, function () {            //Original
       app.listen(process.env.port, function () {  //Updated
         var addr = app.address();
         console.log('   app listening on http://' + addr.address + ':' + addr.port);
       });

<span data-ttu-id="6eaf6-142">Po zapisaniu zmian hello zbyt**server.js**, użyj hello następujące kroki, aby zainstalować wymagane moduły i przetestowanie aplikacji hello w emulatorze platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="6eaf6-142">After saving hello changes too**server.js**, use hello following steps to install required modules, and then test hello application in the Azure emulator:</span></span>

1. <span data-ttu-id="6eaf6-143">Przy użyciu **programu Azure PowerShell**, zmień katalogi toohello **C:\\węzła\\chatapp\\WorkerRole1** hello katalogu i użyj następującego polecenia tooinstall hello moduły wymagane przez tę aplikację:</span><span class="sxs-lookup"><span data-stu-id="6eaf6-143">Using **Azure PowerShell**, change directories toohello **C:\\node\\chatapp\\WorkerRole1** directory and use hello following command tooinstall hello modules required by this application:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> npm install
   
   <span data-ttu-id="6eaf6-144">Spowoduje to zainstalowanie modułów hello wymienionych w pliku package.json hello.</span><span class="sxs-lookup"><span data-stu-id="6eaf6-144">This will install hello modules listed in hello package.json file.</span></span> <span data-ttu-id="6eaf6-145">Po zakończeniu wykonywania polecenia hello powinny być widoczne dane wyjściowe podobne toothe poniżej:</span><span class="sxs-lookup"><span data-stu-id="6eaf6-145">After hello command completes, you should see output similar toothe following:</span></span>
   
   ![dane wyjściowe Hello hello npm polecenie instalacji][The-output-of-the-npm-install-command]
2. <span data-ttu-id="6eaf6-147">Ponieważ w tym przykładzie pierwotnie część hello repozytorium GitHub użyciu biblioteki Socket.IO i bezpośrednie odwołanie do biblioteki użyciu biblioteki Socket.IO hello przez ścieżkę względną, użyciu biblioteki Socket.IO nie został przywołany w pliku package.json hello, więc trzeba zainstalować wysyłając hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="6eaf6-147">Since this example was originally a part of hello Socket.IO GitHub repository, and directly referenced hello Socket.IO library by relative path, Socket.IO was not referenced in hello package.json file, so we must install it by issuing hello following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> npm install socket.io --save

### <a name="test-and-deploy"></a><span data-ttu-id="6eaf6-148">Testowania i wdrażania</span><span class="sxs-lookup"><span data-stu-id="6eaf6-148">Test and Deploy</span></span>
1. <span data-ttu-id="6eaf6-149">Uruchamianie emulatora hello wysyłając hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="6eaf6-149">Launch hello emulator by issuing hello following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Start-AzureEmulator -Launch
   
   > [!NOTE]
   > <span data-ttu-id="6eaf6-150">Jeśli wystąpią problemy związane z uruchamianie emulatora, np.: Start AzureEmulator: Wystąpił nieoczekiwany błąd.</span><span class="sxs-lookup"><span data-stu-id="6eaf6-150">If you encounter issues with launching emulator, eg.: Start-AzureEmulator : An unexpected failure occurred.</span></span>  <span data-ttu-id="6eaf6-151">Szczegóły: Napotkano nieoczekiwany błąd hello komunikacji, System.ServiceModel.Channels.ServiceChannel, nie można użyć obiektu komunikacji, ponieważ jest w stanie Faulted hello.</span><span class="sxs-lookup"><span data-stu-id="6eaf6-151">Details: Encountered an unexpected error hello communication object,  System.ServiceModel.Channels.ServiceChannel, cannot be used for communication because it is in hello Faulted state.</span></span>
   
      <span data-ttu-id="6eaf6-152">Zainstaluj ponownie AzureAuthoringTools v 2.7.1 i AzureComputeEmulator v 2.7 - upewnij się, że ta wersja jest zgodna.</span><span class="sxs-lookup"><span data-stu-id="6eaf6-152">reinstall AzureAuthoringTools v 2.7.1 and AzureComputeEmulator v 2.7 - make sure that version matches.</span></span>
   >
   >


2. <span data-ttu-id="6eaf6-153">Otwórz przeglądarkę i przejdź zbyt**http://127.0.0.1**.</span><span class="sxs-lookup"><span data-stu-id="6eaf6-153">Open a browser and navigate too**http://127.0.0.1**.</span></span>
3. <span data-ttu-id="6eaf6-154">Po otwarciu okna przeglądarki hello wprowadź pseudonim, a następnie naciśnij klawisz enter.</span><span class="sxs-lookup"><span data-stu-id="6eaf6-154">When hello browser window opens, enter a nickname and then hit enter.</span></span>
   <span data-ttu-id="6eaf6-155">Umożliwi wiadomości toopost jako określonych pseudonim.</span><span class="sxs-lookup"><span data-stu-id="6eaf6-155">This will allow you toopost messages as a specific nickname.</span></span> <span data-ttu-id="6eaf6-156">tootest funkcji wielu użytkowników, Otwórz dodatkowe okna przeglądarki przy użyciu tego samego adresu URL i wprowadź inny pseudonimy.</span><span class="sxs-lookup"><span data-stu-id="6eaf6-156">tootest multi-user functionality, open additional browser windows using the same URL and enter different nicknames.</span></span>
   
   ![Wyświetlanie wiadomości od użytkowników Użytkownik1 i Użytkownik2 dwa okna przeglądarki](./media/cloud-services-nodejs-chat-app-socketio/socketio-8.png)
4. <span data-ttu-id="6eaf6-158">Po testowania aplikacji hello Zatrzymaj emulatora hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="6eaf6-158">After testing hello application, stop hello emulator by issuing the following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Stop-AzureEmulator
5. <span data-ttu-id="6eaf6-159">tooAzure aplikacji hello toodeploy, użyj **Publish-AzureServiceProject** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6eaf6-159">toodeploy hello application tooAzure, use the **Publish-AzureServiceProject** cmdlet.</span></span> <span data-ttu-id="6eaf6-160">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="6eaf6-160">For example:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Publish-AzureServiceProject -ServiceName mychatapp -Location "East US" -Launch
   
   > [!IMPORTANT]
   > <span data-ttu-id="6eaf6-161">Można się toouse unikatową nazwę, w przeciwnym razie hello publikowania proces zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="6eaf6-161">Be sure toouse a unique name, otherwise hello publish process will fail.</span></span> <span data-ttu-id="6eaf6-162">Po zakończeniu wdrożenia hello hello przeglądarki będzie Otwórz i przejdź toohello wdrożona usługa.</span><span class="sxs-lookup"><span data-stu-id="6eaf6-162">After hello deployment has completed, hello browser will open and navigate toohello deployed service.</span></span>
   > 
   > <span data-ttu-id="6eaf6-163">Jeśli zostanie wyświetlony błąd informujący o tym hello pod warunkiem, że nazwa subskrypcji nie istnieje w hello zaimportowany profil publikowania, musisz pobrać i zaimportować hello profil publikowania dla subskrypcji przed wdrożeniem tooAzure.</span><span class="sxs-lookup"><span data-stu-id="6eaf6-163">If you receive an error stating that hello provided subscription name doesn't exist in hello imported publish profile, you must download and import hello publishing profile for your subscription before deploying tooAzure.</span></span> <span data-ttu-id="6eaf6-164">Zobacz hello **wdrażanie tooAzure aplikacji hello** sekcji [tworzenia i wdrażania tooan aplikacji Node.js usługi w chmurze Azure](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span><span class="sxs-lookup"><span data-stu-id="6eaf6-164">See hello **Deploying hello Application tooAzure** section of [Build and deploy a Node.js application tooan Azure Cloud Service](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span></span>
   > 
   > 
   
   ![Okno przeglądarki zawierające hello usługi hostowanej na platformie Azure][completed-app]
   
   > [!NOTE]
   > <span data-ttu-id="6eaf6-166">Jeśli zostanie wyświetlony błąd informujący o tym hello pod warunkiem, że nazwa subskrypcji nie istnieje w hello zaimportowany profil publikowania, musisz pobrać i zaimportować hello profil publikowania dla subskrypcji przed wdrożeniem tooAzure.</span><span class="sxs-lookup"><span data-stu-id="6eaf6-166">If you receive an error stating that hello provided subscription name doesn't exist in hello imported publish profile, you must download and import hello publishing profile for your subscription before deploying tooAzure.</span></span> <span data-ttu-id="6eaf6-167">Zobacz hello **wdrażanie tooAzure aplikacji hello** sekcji [tworzenia i wdrażania tooan aplikacji Node.js usługi w chmurze Azure](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span><span class="sxs-lookup"><span data-stu-id="6eaf6-167">See hello **Deploying hello Application tooAzure** section of [Build and deploy a Node.js application tooan Azure Cloud Service](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span></span>
   > 
   > 

<span data-ttu-id="6eaf6-168">Aplikacja jest teraz uruchomiona na platformie Azure i możliwość przekazywania wiadomości między różnych klientów przy użyciu użyciu biblioteki Socket.IO.</span><span class="sxs-lookup"><span data-stu-id="6eaf6-168">Your application is now running on Azure, and can relay chat messages between different clients using Socket.IO.</span></span>

> [!NOTE]
> <span data-ttu-id="6eaf6-169">Dla uproszczenia, w tym przykładzie jest ograniczona toochatting między toohello połączonych użytkowników tego samego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="6eaf6-169">For simplicity, this sample is limited toochatting between users connected toohello same instance.</span></span> <span data-ttu-id="6eaf6-170">Oznacza to, że jeśli usługa w chmurze hello tworzy dwa wystąpienia roli procesu roboczego, użytkownicy będą mogli tylko toochat osobom połączone toohello tego samego wystąpienia roli procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="6eaf6-170">This means that if hello cloud service creates two worker role instances, users will only be able toochat with others connected toohello same worker role instance.</span></span> <span data-ttu-id="6eaf6-171">tooscale hello toowork aplikacji z wielu wystąpień ról, można użyć technologii takich jak usługi Service Bus tooshare hello użyciu biblioteki Socket.IO przechowywanie stanu w wystąpieniach.</span><span class="sxs-lookup"><span data-stu-id="6eaf6-171">tooscale hello application toowork with multiple role instances, you could use a technology like Service Bus tooshare hello Socket.IO store state across instances.</span></span> <span data-ttu-id="6eaf6-172">Przykłady można znaleźć hello przykłady użycia tematów i kolejek usługi Service Bus w hello [zestawu Azure SDK dla repozytorium Node.js GitHub](https://github.com/WindowsAzure/azure-sdk-for-node).</span><span class="sxs-lookup"><span data-stu-id="6eaf6-172">For examples, see hello Service Bus Queues and Topics usage samples in hello [Azure SDK for Node.js GitHub repository](https://github.com/WindowsAzure/azure-sdk-for-node).</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="6eaf6-173">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6eaf6-173">Next steps</span></span>
<span data-ttu-id="6eaf6-174">W tym samouczku przedstawiono sposób toocreate aplikacji rozmów podstawowe hostowanej w usłudze w chmurze Azure.</span><span class="sxs-lookup"><span data-stu-id="6eaf6-174">In this tutorial you learned how toocreate a basic chat application hosted in an Azure Cloud Service.</span></span> <span data-ttu-id="6eaf6-175">toolearn toohost tej aplikacji w witrynie internetowej platformy Azure, zobacz temat [tworzenie aplikacji czatu Node.js przy użyciu biblioteki Socket.IO w witrynie sieci Web Azure][chatwebsite].</span><span class="sxs-lookup"><span data-stu-id="6eaf6-175">toolearn how toohost this application in an Azure Website, see [Build a Node.js Chat Application with Socket.IO on an Azure Web Site][chatwebsite].</span></span>

<span data-ttu-id="6eaf6-176">Aby uzyskać więcej informacji, zobacz też hello [Centrum deweloperów środowiska Node.js](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="6eaf6-176">For more information, see also hello [Node.js Developer Center](/develop/nodejs/).</span></span>

[chatwebsite]: /develop/nodejs/tutorials/website-using-socketio/

[Azure SLA]: http://www.windowsazure.com/support/sla/
[Azure SDK for Node.js GitHub repository]: https://github.com/WindowsAzure/azure-sdk-for-node
[completed-app]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-10.png
[Azure SDK for Node.js]: https://www.windowsazure.com/develop/nodejs/
[Node.js Web Application]: https://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
[repozytorium GitHub użyciu biblioteki Socket.IO]: https://github.com/LearnBoost/socket.io/tree/0.9.14
[Azure Considerations]: #windowsazureconsiderations
[Hosting hello Chat Example in a Worker Role]: #hostingthechatexampleinawebrole
[Summary and Next Steps]: #summary
[powershell-menu]: ./media/cloud-services-nodejs-chat-app-socketio/azure-powershell-start.png

[chat example]: https://github.com/LearnBoost/socket.io/tree/master/examples/chat
[chat-example-view]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-22.png


[chat-contents]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-5.png
[The-output-of-the-npm-install-command]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-7.png
[hello output of hello Publish-AzureService command]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-9.png


