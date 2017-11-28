---
title: "Aplikacji node.js za pomocą użyciu biblioteki Socket.io | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać użyciu biblioteki socket.io w aplikacji node.js hostowanej na platformie Azure."
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
ms.openlocfilehash: a85d4348a13b79b5b7542362de9956aa3398375a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="build-a-nodejs-chat-application-with-socketio-on-an-azure-cloud-service"></a><span data-ttu-id="a941d-103">Tworzenie aplikacji czatu Node.js przy użyciu biblioteki Socket.IO w usłudze chmury Azure</span><span class="sxs-lookup"><span data-stu-id="a941d-103">Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service</span></span>
<span data-ttu-id="a941d-104">Użyciu biblioteki Socket.IO zapewnia czasu rzeczywistego komunikacji między między serwerem środowiska node.js i klientami.</span><span class="sxs-lookup"><span data-stu-id="a941d-104">Socket.IO provides realtime communication between between your node.js server and clients.</span></span> <span data-ttu-id="a941d-105">W tym samouczku opisano za pośrednictwem obsługi gniazda. We/Wy na podstawie rozmów aplikacji na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="a941d-105">This tutorial will walk you through hosting a socket.IO based chat application on Azure.</span></span> <span data-ttu-id="a941d-106">Aby uzyskać więcej informacji o użyciu biblioteki Socket.IO, zobacz <http://socket.io/>.</span><span class="sxs-lookup"><span data-stu-id="a941d-106">For more information on Socket.IO, see <http://socket.io/>.</span></span>

<span data-ttu-id="a941d-107">Zrzut ekranu przedstawiający ukończona aplikacja znajduje się poniżej:</span><span class="sxs-lookup"><span data-stu-id="a941d-107">A screenshot of the completed application is below:</span></span>

![Okno przeglądarki zawierające usługi hostowanej na platformie Azure][completed-app]  

## <a name="prerequisites"></a><span data-ttu-id="a941d-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a941d-109">Prerequisites</span></span>
<span data-ttu-id="a941d-110">Upewnij się, że do pomyślnego ukończenia w przykładzie w tym artykule są zainstalowane następujące produkty i wersje:</span><span class="sxs-lookup"><span data-stu-id="a941d-110">Ensure that the following products and versions are installed to successfully complete the example in this article:</span></span>

* <span data-ttu-id="a941d-111">Zainstalować program [Visual Studio](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx)</span><span class="sxs-lookup"><span data-stu-id="a941d-111">Install [Visual Studio](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx)</span></span>
* <span data-ttu-id="a941d-112">Zainstalować środowisko [Node.js](https://nodejs.org/download/).</span><span class="sxs-lookup"><span data-stu-id="a941d-112">Install [Node.js](https://nodejs.org/download/)</span></span>
* <span data-ttu-id="a941d-113">Zainstaluj [2.7.10 wersji języka Python](https://www.python.org/)</span><span class="sxs-lookup"><span data-stu-id="a941d-113">Install [Python version 2.7.10](https://www.python.org/)</span></span>

## <a name="create-a-cloud-service-project"></a><span data-ttu-id="a941d-114">Tworzenie projektu usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="a941d-114">Create a Cloud Service Project</span></span>
<span data-ttu-id="a941d-115">Poniższe kroki tworzenia projektu usługi w chmurze, który będzie hostem aplikacji użyciu biblioteki Socket.IO.</span><span class="sxs-lookup"><span data-stu-id="a941d-115">The following steps create the cloud service project that will host the Socket.IO application.</span></span>

1. <span data-ttu-id="a941d-116">Z **Start Menu** lub **ekranu startowego**, wyszukaj **programu Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="a941d-116">From the **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span> <span data-ttu-id="a941d-117">Na koniec kliknij prawym przyciskiem myszy **programu Windows PowerShell** i wybierz **Uruchom jako Administrator**.</span><span class="sxs-lookup"><span data-stu-id="a941d-117">Finally, right-click **Windows PowerShell** and select **Run As Administrator**.</span></span>
   
    ![Ikona Azure PowerShell][powershell-menu]
2. <span data-ttu-id="a941d-119">Utwórz katalog o nazwie **c:\\węzła**.</span><span class="sxs-lookup"><span data-stu-id="a941d-119">Create a directory called **c:\\node**.</span></span> 
   
        PS C:\> md node
3. <span data-ttu-id="a941d-120">Przejdź do **c:\\węzła** katalogu</span><span class="sxs-lookup"><span data-stu-id="a941d-120">Change directories to the **c:\\node** directory</span></span>
   
        PS C:\> cd node
4. <span data-ttu-id="a941d-121">Wprowadź następujące polecenia, aby utworzyć nowe rozwiązanie o nazwie **chatapp** i rolę procesu roboczego o nazwie **WorkerRole1**:</span><span class="sxs-lookup"><span data-stu-id="a941d-121">Enter the following commands to create a new solution named **chatapp** and a worker role named **WorkerRole1**:</span></span>
   
        PS C:\node> New-AzureServiceProject chatapp
        PS C:\Node> Add-AzureNodeWorkerRole
   
    <span data-ttu-id="a941d-122">Zostanie wyświetlony następujący odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="a941d-122">You will see the following response:</span></span>
   
    ![Dane wyjściowe nowy azureservice i Dodaj azurenodeworkerrolecmdlets](./media/cloud-services-nodejs-chat-app-socketio/socketio-1.png)

## <a name="download-the-chat-example"></a><span data-ttu-id="a941d-124">Pobierz przykład rozmowy</span><span class="sxs-lookup"><span data-stu-id="a941d-124">Download the Chat Example</span></span>
<span data-ttu-id="a941d-125">Dla tego projektu, użyjemy przykład rozmów z [repozytorium GitHub użyciu biblioteki Socket.IO].</span><span class="sxs-lookup"><span data-stu-id="a941d-125">For this project, we will use the chat example from the [Socket.IO GitHub repository].</span></span> <span data-ttu-id="a941d-126">Wykonaj poniższe kroki, aby pobrać przykład i dodaj go do projektu, utworzonych wcześniej.</span><span class="sxs-lookup"><span data-stu-id="a941d-126">Perform the following steps to download the example and add it to the project you previously created.</span></span>

1. <span data-ttu-id="a941d-127">Utwórz kopię lokalną repozytorium przy użyciu **klonowania** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a941d-127">Create a local copy of the repository by using the **Clone** button.</span></span> <span data-ttu-id="a941d-128">Można także użyć **ZIP** przycisk, aby pobrać projekt.</span><span class="sxs-lookup"><span data-stu-id="a941d-128">You may also use the **ZIP** button to download the project.</span></span>
   
   ![Wyświetlanie https://github.com/LearnBoost/socket.io/tree/master/examples/chat, z ikoną pobierania ZIP wyróżnione oknie przeglądarki][chat-example-view]
2. <span data-ttu-id="a941d-130">Przejdź struktury katalogu lokalnego repozytorium, dopóki przyjeździe **przykłady\\rozmów** katalogu.</span><span class="sxs-lookup"><span data-stu-id="a941d-130">Navigate the directory structure of the local repository until you arrive at the **examples\\chat** directory.</span></span> <span data-ttu-id="a941d-131">Skopiuj zawartość tego katalogu, aby **C:\\węzła\\chatapp\\WorkerRole1** Katalog utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="a941d-131">Copy the contents of this directory to the **C:\\node\\chatapp\\WorkerRole1** directory created earlier.</span></span>
   
   ![Eksplorator, wyświetlania zawartości przykłady\\katalogu rozmów wyodrębnione z archiwum][chat-contents]
   
   <span data-ttu-id="a941d-133">Zaznaczone elementy na zrzucie ekranu powyżej znajdują się pliki kopiowane z **przykłady\\rozmów** katalogu</span><span class="sxs-lookup"><span data-stu-id="a941d-133">The highlighted items in the screenshot above are the files copied from the **examples\\chat** directory</span></span>
3. <span data-ttu-id="a941d-134">W **C:\\węzła\\chatapp\\WorkerRole1** katalogu, Usuń **server.js** pliku, a następnie zmień **app.js** pliku **server.js**.</span><span class="sxs-lookup"><span data-stu-id="a941d-134">In the **C:\\node\\chatapp\\WorkerRole1** directory, delete the **server.js** file, and then rename the **app.js** file to **server.js**.</span></span> <span data-ttu-id="a941d-135">Spowoduje to usunięcie domyślnie **server.js** plik utworzony wcześniej przez **AzureNodeWorkerRole Dodaj** polecenia cmdlet i zastępuje go z plikiem aplikacji z przykładu rozmów.</span><span class="sxs-lookup"><span data-stu-id="a941d-135">This removes the default **server.js** file created previously by the **Add-AzureNodeWorkerRole** cmdlet and replaces it with the application file from the chat example.</span></span>

### <a name="modify-serverjs-and-install-modules"></a><span data-ttu-id="a941d-136">Modyfikowanie Server.js i zainstalować moduły</span><span class="sxs-lookup"><span data-stu-id="a941d-136">Modify Server.js and Install Modules</span></span>
<span data-ttu-id="a941d-137">Przed testowaniem aplikacji w emulatorze platformy Azure, firma Microsoft wprowadzać niektórych drobne zmiany.</span><span class="sxs-lookup"><span data-stu-id="a941d-137">Before testing the application in the Azure emulator, we must make some minor modifications.</span></span> <span data-ttu-id="a941d-138">Wykonaj poniższe kroki, aby pliku server.js:</span><span class="sxs-lookup"><span data-stu-id="a941d-138">Perform the following steps to the server.js file:</span></span>

1. <span data-ttu-id="a941d-139">Otwórz **server.js** pliku w Visual Studio lub w dowolnym edytorze tekstów.</span><span class="sxs-lookup"><span data-stu-id="a941d-139">Open the **server.js** file in Visual Studio or any text editor.</span></span>
2. <span data-ttu-id="a941d-140">Znajdź **zależności modułu** sekcji na początku server.js i zmień wiersz zawierający **sio = require('.. //.. lib//Socket.IO ")** do **sio = require('socket.io')** w sposób przedstawiony poniżej:</span><span class="sxs-lookup"><span data-stu-id="a941d-140">Find the **Module dependencies** section at the beginning of server.js and change the line containing **sio = require('..//..//lib//socket.io')** to **sio = require('socket.io')** as shown below:</span></span>
   
       var express = require('express')
         , stylus = require('stylus')
         , nib = require('nib')
       //, sio = require('..//..//lib//socket.io'); //Original
         , sio = require('socket.io');                //Updated
         var port = process.env.PORT || 3000;         //Updated
3. <span data-ttu-id="a941d-141">Aby upewnić się, aplikacja nasłuchuje właściwego portu, Otwórz w Notatniku lub ulubionego edytora server.js, a następnie zmień następujący wiersz zastępując **3000** z **process.env.port** w sposób przedstawiony poniżej:</span><span class="sxs-lookup"><span data-stu-id="a941d-141">To ensure the application listens on the correct port, open server.js in Notepad or your favorite editor, and then change the following line by replacing **3000** with **process.env.port** as shown below:</span></span>
   
       //app.listen(3000, function () {            //Original
       app.listen(process.env.port, function () {  //Updated
         var addr = app.address();
         console.log('   app listening on http://' + addr.address + ':' + addr.port);
       });

<span data-ttu-id="a941d-142">Po zapisaniu zmian do **server.js**, wykonaj następujące kroki, aby zainstalować wymagane moduły, a następnie przetestować aplikację w emulatorze platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="a941d-142">After saving the changes to **server.js**, use the following steps to install required modules, and then test the application in the Azure emulator:</span></span>

1. <span data-ttu-id="a941d-143">Przy użyciu **programu Azure PowerShell**, przejdź do **C:\\węzła\\chatapp\\WorkerRole1** katalogu i użyj następujące polecenie, aby zainstalować moduły wymagane przez tę aplikację:</span><span class="sxs-lookup"><span data-stu-id="a941d-143">Using **Azure PowerShell**, change directories to the **C:\\node\\chatapp\\WorkerRole1** directory and use the following command to install the modules required by this application:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> npm install
   
   <span data-ttu-id="a941d-144">Spowoduje to zainstalowanie modułów wymieniony w pliku package.json.</span><span class="sxs-lookup"><span data-stu-id="a941d-144">This will install the modules listed in the package.json file.</span></span> <span data-ttu-id="a941d-145">Po zakończeniu wykonywania polecenia, powinny być widoczne dane wyjściowe podobne do następującego:</span><span class="sxs-lookup"><span data-stu-id="a941d-145">After the command completes, you should see output similar to the following:</span></span>
   
   ![Dane wyjściowe programu npm install, polecenie][The-output-of-the-npm-install-command]
2. <span data-ttu-id="a941d-147">Ponieważ w tym przykładzie pierwotnie częścią repozytorium GitHub użyciu biblioteki Socket.IO i bezpośrednie odwołanie do biblioteki użyciu biblioteki Socket.IO przez ścieżkę względną, użyciu biblioteki Socket.IO nie został przywołany w pliku package.json, więc trzeba zainstalować wydając polecenie:</span><span class="sxs-lookup"><span data-stu-id="a941d-147">Since this example was originally a part of the Socket.IO GitHub repository, and directly referenced the Socket.IO library by relative path, Socket.IO was not referenced in the package.json file, so we must install it by issuing the following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> npm install socket.io --save

### <a name="test-and-deploy"></a><span data-ttu-id="a941d-148">Testowania i wdrażania</span><span class="sxs-lookup"><span data-stu-id="a941d-148">Test and Deploy</span></span>
1. <span data-ttu-id="a941d-149">Uruchom emulator, wykonując następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="a941d-149">Launch the emulator by issuing the following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Start-AzureEmulator -Launch
   
   > [!NOTE]
   > <span data-ttu-id="a941d-150">Jeśli wystąpią problemy związane z uruchamianie emulatora, np.: Start AzureEmulator: Wystąpił nieoczekiwany błąd.</span><span class="sxs-lookup"><span data-stu-id="a941d-150">If you encounter issues with launching emulator, eg.: Start-AzureEmulator : An unexpected failure occurred.</span></span>  <span data-ttu-id="a941d-151">Szczegóły: Napotkano nieoczekiwany błąd obiektu komunikacji System.ServiceModel.Channels.ServiceChannel, nie można użyć do komunikacji, ponieważ jest w stanie Faulted.</span><span class="sxs-lookup"><span data-stu-id="a941d-151">Details: Encountered an unexpected error The communication object,  System.ServiceModel.Channels.ServiceChannel, cannot be used for communication because it is in the Faulted state.</span></span>
   
      <span data-ttu-id="a941d-152">Zainstaluj ponownie AzureAuthoringTools v 2.7.1 i AzureComputeEmulator v 2.7 - upewnij się, że ta wersja jest zgodna.</span><span class="sxs-lookup"><span data-stu-id="a941d-152">reinstall AzureAuthoringTools v 2.7.1 and AzureComputeEmulator v 2.7 - make sure that version matches.</span></span>
   >
   >


2. <span data-ttu-id="a941d-153">Otwórz przeglądarkę i przejdź do **http://127.0.0.1**.</span><span class="sxs-lookup"><span data-stu-id="a941d-153">Open a browser and navigate to **http://127.0.0.1**.</span></span>
3. <span data-ttu-id="a941d-154">Po otwarciu okna przeglądarki, wprowadź pseudonim, a następnie naciśnij klawisz enter.</span><span class="sxs-lookup"><span data-stu-id="a941d-154">When the browser window opens, enter a nickname and then hit enter.</span></span>
   <span data-ttu-id="a941d-155">Umożliwi to publikowania wiadomości jako określonych pseudonim.</span><span class="sxs-lookup"><span data-stu-id="a941d-155">This will allow you to post messages as a specific nickname.</span></span> <span data-ttu-id="a941d-156">Aby przetestować funkcje wielu użytkowników, Otwórz dodatkowe okna przeglądarki przy użyciu tego samego adresu URL i wprowadź inny pseudonimy.</span><span class="sxs-lookup"><span data-stu-id="a941d-156">To test multi-user functionality, open additional browser windows using the same URL and enter different nicknames.</span></span>
   
   ![Wyświetlanie wiadomości od użytkowników Użytkownik1 i Użytkownik2 dwa okna przeglądarki](./media/cloud-services-nodejs-chat-app-socketio/socketio-8.png)
4. <span data-ttu-id="a941d-158">Po zakończeniu testowania aplikacji, należy zatrzymać emulator wydając polecenie:</span><span class="sxs-lookup"><span data-stu-id="a941d-158">After testing the application, stop the emulator by issuing the following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Stop-AzureEmulator
5. <span data-ttu-id="a941d-159">Aby wdrożyć aplikację na platformie Azure, użyj **Publish-AzureServiceProject** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a941d-159">To deploy the application to Azure, use the **Publish-AzureServiceProject** cmdlet.</span></span> <span data-ttu-id="a941d-160">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="a941d-160">For example:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Publish-AzureServiceProject -ServiceName mychatapp -Location "East US" -Launch
   
   > [!IMPORTANT]
   > <span data-ttu-id="a941d-161">Należy użyć unikatową nazwę, w przeciwnym razie proces publikowania zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="a941d-161">Be sure to use a unique name, otherwise the publish process will fail.</span></span> <span data-ttu-id="a941d-162">Po zakończeniu wdrożenia przeglądarki otworzyć i przejdź do wdrożonej usługi.</span><span class="sxs-lookup"><span data-stu-id="a941d-162">After the deployment has completed, the browser will open and navigate to the deployed service.</span></span>
   > 
   > <span data-ttu-id="a941d-163">Jeśli zostanie wyświetlony komunikat o błędzie informujący, że nazwa podana subskrypcja nie istnieje w profilu publikowania importowane, musisz pobrać i zaimportować profil publikowania dla subskrypcji przed wdrożeniem na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="a941d-163">If you receive an error stating that the provided subscription name doesn't exist in the imported publish profile, you must download and import the publishing profile for your subscription before deploying to Azure.</span></span> <span data-ttu-id="a941d-164">Zobacz **wdrażanie aplikacji na platformie Azure** sekcji [tworzenia i wdrażania aplikacji Node.js do usługi w chmurze platformy Azure](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span><span class="sxs-lookup"><span data-stu-id="a941d-164">See the **Deploying the Application to Azure** section of [Build and deploy a Node.js application to an Azure Cloud Service](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span></span>
   > 
   > 
   
   ![Okno przeglądarki zawierające usługi hostowanej na platformie Azure][completed-app]
   
   > [!NOTE]
   > <span data-ttu-id="a941d-166">Jeśli zostanie wyświetlony komunikat o błędzie informujący, że nazwa podana subskrypcja nie istnieje w profilu publikowania importowane, musisz pobrać i zaimportować profil publikowania dla subskrypcji przed wdrożeniem na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="a941d-166">If you receive an error stating that the provided subscription name doesn't exist in the imported publish profile, you must download and import the publishing profile for your subscription before deploying to Azure.</span></span> <span data-ttu-id="a941d-167">Zobacz **wdrażanie aplikacji na platformie Azure** sekcji [tworzenia i wdrażania aplikacji Node.js do usługi w chmurze platformy Azure](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span><span class="sxs-lookup"><span data-stu-id="a941d-167">See the **Deploying the Application to Azure** section of [Build and deploy a Node.js application to an Azure Cloud Service](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span></span>
   > 
   > 

<span data-ttu-id="a941d-168">Aplikacja jest teraz uruchomiona na platformie Azure i możliwość przekazywania wiadomości między różnych klientów przy użyciu użyciu biblioteki Socket.IO.</span><span class="sxs-lookup"><span data-stu-id="a941d-168">Your application is now running on Azure, and can relay chat messages between different clients using Socket.IO.</span></span>

> [!NOTE]
> <span data-ttu-id="a941d-169">Dla uproszczenia w tym przykładzie jest ograniczona do rozmowy między użytkowników podłączonych do tego samego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="a941d-169">For simplicity, this sample is limited to chatting between users connected to the same instance.</span></span> <span data-ttu-id="a941d-170">Oznacza to, że jeśli usługa w chmurze tworzy dwa wystąpienia roli procesu roboczego, użytkownicy będą mieć tylko rozmawiać z innymi podłączone do tego samego wystąpienia roli procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="a941d-170">This means that if the cloud service creates two worker role instances, users will only be able to chat with others connected to the same worker role instance.</span></span> <span data-ttu-id="a941d-171">Do skalowania aplikacji do pracy z wielu wystąpień ról, można użyć technologii, takich jak usługi Service Bus do udostępniania stanu magazynu użyciu biblioteki Socket.IO w wystąpieniach.</span><span class="sxs-lookup"><span data-stu-id="a941d-171">To scale the application to work with multiple role instances, you could use a technology like Service Bus to share the Socket.IO store state across instances.</span></span> <span data-ttu-id="a941d-172">Przykłady można znaleźć przykłady użycia tematów i kolejek usługi Service Bus w [zestawu Azure SDK dla repozytorium Node.js GitHub](https://github.com/WindowsAzure/azure-sdk-for-node).</span><span class="sxs-lookup"><span data-stu-id="a941d-172">For examples, see the Service Bus Queues and Topics usage samples in the [Azure SDK for Node.js GitHub repository](https://github.com/WindowsAzure/azure-sdk-for-node).</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="a941d-173">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a941d-173">Next steps</span></span>
<span data-ttu-id="a941d-174">W tym samouczku przedstawiono sposób tworzenia aplikacji rozmów podstawowe hostowanych w usłudze w chmurze Azure.</span><span class="sxs-lookup"><span data-stu-id="a941d-174">In this tutorial you learned how to create a basic chat application hosted in an Azure Cloud Service.</span></span> <span data-ttu-id="a941d-175">Aby uzyskać informacje o obsłudze tej aplikacji w witrynie sieci Web platformy Azure, zobacz [tworzenie aplikacji czatu Node.js przy użyciu biblioteki Socket.IO w witrynie sieci Web Azure][chatwebsite].</span><span class="sxs-lookup"><span data-stu-id="a941d-175">To learn how to host this application in an Azure Website, see [Build a Node.js Chat Application with Socket.IO on an Azure Web Site][chatwebsite].</span></span>

<span data-ttu-id="a941d-176">Aby uzyskać więcej informacji, zobacz też [Centrum deweloperów środowiska Node.js](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="a941d-176">For more information, see also the [Node.js Developer Center](/develop/nodejs/).</span></span>

[chatwebsite]: /develop/nodejs/tutorials/website-using-socketio/

[Azure SLA]: http://www.windowsazure.com/support/sla/
[Azure SDK for Node.js GitHub repository]: https://github.com/WindowsAzure/azure-sdk-for-node
[completed-app]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-10.png
[Azure SDK for Node.js]: https://www.windowsazure.com/develop/nodejs/
[Node.js Web Application]: https://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
<span data-ttu-id="a941d-177">[repozytorium GitHub użyciu biblioteki Socket.IO]: https://github.com/LearnBoost/socket.io/tree/0.9.14</span><span class="sxs-lookup"><span data-stu-id="a941d-177">[Socket.IO GitHub repository]: https://github.com/LearnBoost/socket.io/tree/0.9.14</span></span>
[Azure Considerations]: #windowsazureconsiderations
[Hosting the Chat Example in a Worker Role]: #hostingthechatexampleinawebrole
[Summary and Next Steps]: #summary
[powershell-menu]: ./media/cloud-services-nodejs-chat-app-socketio/azure-powershell-start.png

[chat example]: https://github.com/LearnBoost/socket.io/tree/master/examples/chat
[chat-example-view]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-22.png


[chat-contents]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-5.png
[The-output-of-the-npm-install-command]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-7.png
[The output of the Publish-AzureService command]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-9.png


