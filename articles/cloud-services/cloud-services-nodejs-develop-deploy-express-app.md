---
title: "aaaWeb aplikacji za pomocą Express (Node.js) | Dokumentacja firmy Microsoft"
description: "Samouczek, który jest oparty na samouczek usługi chmury hello i pokazuje, jak toouse hello modułu Express."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 24f8e7ef-e90d-4554-9b1e-a9b31d5824e5
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 91921bfbe137eeca9a110d4cb18eb57b46b0060e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-web-application-using-express-on-an-azure-cloud-service"></a><span data-ttu-id="05766-103">Tworzenie aplikacji sieci web Node.js za pomocą ekspresowego na usługi w chmurze platformy Azure</span><span class="sxs-lookup"><span data-stu-id="05766-103">Build a Node.js web application using Express on an Azure Cloud Service</span></span>
<span data-ttu-id="05766-104">Node.js zawiera minimalny zestaw funkcji w hello podstawowego środowiska wykonawczego.</span><span class="sxs-lookup"><span data-stu-id="05766-104">Node.js includes a minimal set of functionality in hello core runtime.</span></span>
<span data-ttu-id="05766-105">Deweloperzy często używają 3 strona modułów tooprovide dodatkowe funkcje, podczas opracowywania aplikacji Node.js.</span><span class="sxs-lookup"><span data-stu-id="05766-105">Developers often use 3rd party modules tooprovide additional functionality when developing a Node.js application.</span></span> <span data-ttu-id="05766-106">W tym samouczku utworzysz nową aplikację przy użyciu hello [Express] [ Express] moduł, który zapewnia platformę MVC do tworzenia aplikacji sieci web Node.js.</span><span class="sxs-lookup"><span data-stu-id="05766-106">In this tutorial you will create a new application using hello [Express][Express] module, which provides an MVC framework for creating Node.js web applications.</span></span>

<span data-ttu-id="05766-107">Zrzut ekranu aplikacji hello ukończone znajduje się poniżej:</span><span class="sxs-lookup"><span data-stu-id="05766-107">A screenshot of hello completed application is below:</span></span>

![Przeglądarka wyświetlająca powitalnej tooExpress na platformie Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="create-a-cloud-service-project"></a><span data-ttu-id="05766-109">Tworzenie projektu usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="05766-109">Create a Cloud Service Project</span></span>
[!INCLUDE [install-dev-tools](../../includes/install-dev-tools.md)]

<span data-ttu-id="05766-110">Wykonaj następujące hello toocreate czynności nowy projekt usługi w chmurze o nazwie "expressapp":</span><span class="sxs-lookup"><span data-stu-id="05766-110">Perform hello following steps toocreate a new cloud service project named 'expressapp':</span></span>

1. <span data-ttu-id="05766-111">Z hello **Start Menu** lub **ekranu startowego**, wyszukaj **programu Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="05766-111">From hello **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span> <span data-ttu-id="05766-112">Na koniec kliknij prawym przyciskiem myszy **programu Windows PowerShell** i wybierz **Uruchom jako Administrator**.</span><span class="sxs-lookup"><span data-stu-id="05766-112">Finally, right-click **Windows PowerShell** and select **Run As Administrator**.</span></span>
   
    ![Ikona Azure PowerShell](./media/cloud-services-nodejs-develop-deploy-express-app/azure-powershell-start.png)
2. <span data-ttu-id="05766-114">Zmień katalogi toohello **c:\\węzła** katalogu, a następnie wprowadź hello następujące polecenia toocreate nowego rozwiązania o nazwie **expressapp** i rolę sieci web o nazwie **WebRole1** :</span><span class="sxs-lookup"><span data-stu-id="05766-114">Change directories toohello **c:\\node** directory and then enter hello following commands toocreate a new solution named **expressapp** and a web role named **WebRole1**:</span></span>
   
        PS C:\node> New-AzureServiceProject expressapp
        PS C:\Node\expressapp> Add-AzureNodeWebRole
        PS C:\Node\expressapp> Set-AzureServiceProjectRole WebRole1 Node 0.10.21
   
    > [!NOTE]
    > <span data-ttu-id="05766-115">Domyślnie **Add-AzureNodeWebRole** używa starszej wersji środowiska node.js.</span><span class="sxs-lookup"><span data-stu-id="05766-115">By default, **Add-AzureNodeWebRole** uses an older version of Node.js.</span></span> <span data-ttu-id="05766-116">Witaj **AzureServiceProjectRole zestaw** v0.10.21 Azure toouse węzła nakazuje powyższych instrukcji.</span><span class="sxs-lookup"><span data-stu-id="05766-116">hello **Set-AzureServiceProjectRole** statement above instructs Azure toouse v0.10.21 of Node.</span></span>  <span data-ttu-id="05766-117">Należy zauważyć, że parametry hello jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="05766-117">Note hello parameters are case-sensitive.</span></span>  <span data-ttu-id="05766-118">Możesz sprawdzić hello poprawną wersję środowiska Node.js została wybrana sprawdzając hello **aparaty** właściwości w **WebRole1\package.json**.</span><span class="sxs-lookup"><span data-stu-id="05766-118">You can verify hello correct version of Node.js has been selected by checking hello **engines** property in **WebRole1\package.json**.</span></span>
    > 
    > 

## <a name="install-express"></a><span data-ttu-id="05766-119">Zainstaluj Express</span><span class="sxs-lookup"><span data-stu-id="05766-119">Install Express</span></span>
1. <span data-ttu-id="05766-120">Zainstaluj generator aplikacji Express hello wysyłając hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="05766-120">Install hello Express generator by issuing hello following command:</span></span>
   
        PS C:\node\expressapp> npm install express-generator -g
   
    <span data-ttu-id="05766-121">dane wyjściowe Hello hello npm polecenia powinny wyglądać podobnie wynik toohello poniżej.</span><span class="sxs-lookup"><span data-stu-id="05766-121">hello output of hello npm command should look similar toohello result below.</span></span> 
   
    ![Programu Windows PowerShell wyświetlania hello dane wyjściowe programu hello npm instalacji ekspresowej polecenia.](./media/cloud-services-nodejs-develop-deploy-express-app/express-g.png)
2. <span data-ttu-id="05766-123">Zmień katalogi toohello **WebRole1** hello katalogu i użyj polecenia express toogenerate nowej aplikacji:</span><span class="sxs-lookup"><span data-stu-id="05766-123">Change directories toohello **WebRole1** directory and use hello express command toogenerate a new application:</span></span>
   
        PS C:\node\expressapp\WebRole1> express
   
    <span data-ttu-id="05766-124">Użytkownik będzie zostanie wyświetlony monit o toooverwrite starszych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="05766-124">You will be prompted toooverwrite your earlier application.</span></span> <span data-ttu-id="05766-125">Wprowadź **y** lub **tak** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="05766-125">Enter **y** or **yes** toocontinue.</span></span> <span data-ttu-id="05766-126">Express spowoduje wygenerowanie pliku app.js hello i struktury folderów, do tworzenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="05766-126">Express will generate hello app.js file and a folder structure for building your application.</span></span>
   
    ![Witaj dane wyjściowe polecenia express hello](./media/cloud-services-nodejs-develop-deploy-express-app/node23.png)
3. <span data-ttu-id="05766-128">dodatkowe zależności tooinstall zdefiniowane w pliku package.json hello, wprowadź następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="05766-128">tooinstall additional dependencies defined in hello package.json file, enter hello following command:</span></span>
   
       PS C:\node\expressapp\WebRole1> npm install
   
   ![dane wyjściowe Hello hello npm polecenie instalacji](./media/cloud-services-nodejs-develop-deploy-express-app/node26.png)
4. <span data-ttu-id="05766-130">Użyj hello następujące polecenie toocopy hello **bin/www** pliku zbyt**server.js**.</span><span class="sxs-lookup"><span data-stu-id="05766-130">Use hello following command toocopy hello **bin/www** file too**server.js**.</span></span> <span data-ttu-id="05766-131">Jest to tak hello usługi w chmurze można znaleźć punktu wejścia powitania dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="05766-131">This is so hello cloud service can find hello entry point for this application.</span></span>
   
       PS C:\node\expressapp\WebRole1> copy bin/www server.js
   
   <span data-ttu-id="05766-132">Po wykonaniu tego polecenia, powinien mieć **server.js** pliku w katalogu hello WebRole1.</span><span class="sxs-lookup"><span data-stu-id="05766-132">After this command completes, you should have a **server.js** file in hello WebRole1 directory.</span></span>
5. <span data-ttu-id="05766-133">Modyfikowanie hello **server.js** tooremove jedną hello "." znaki z hello następującego wiersza.</span><span class="sxs-lookup"><span data-stu-id="05766-133">Modify hello **server.js** tooremove one of hello '.' characters from hello following line.</span></span>
   
       var app = require('../app');
   
   <span data-ttu-id="05766-134">Po wprowadzeniu tej zmiany należy wiersz hello powinna wyglądać następująco.</span><span class="sxs-lookup"><span data-stu-id="05766-134">After making this modification, hello line should appear as follows.</span></span>
   
       var app = require('./app');
   
   <span data-ttu-id="05766-135">Ta zmiana jest wymagana, ponieważ przenieśliśmy hello pliku (dawniej **bin/www**,) toohello tym samym katalogu co plik aplikacji hello jest wymagane.</span><span class="sxs-lookup"><span data-stu-id="05766-135">This change is required since we moved hello file (formerly **bin/www**,) toohello same directory as hello app file being required.</span></span> <span data-ttu-id="05766-136">Po wprowadzeniu tej zmiany należy zapisać hello **server.js** pliku.</span><span class="sxs-lookup"><span data-stu-id="05766-136">After making this change, save hello **server.js** file.</span></span>
6. <span data-ttu-id="05766-137">Użyj następującego polecenia toorun hello aplikacji hello Azure emulator hello:</span><span class="sxs-lookup"><span data-stu-id="05766-137">Use hello following command toorun hello application in hello Azure emulator:</span></span>
   
       PS C:\node\expressapp\WebRole1> Start-AzureEmulator -launch
   
    ![Strony sieci web zawierającej tooexpress powitalnej.](./media/cloud-services-nodejs-develop-deploy-express-app/node28.png)

## <a name="modifying-hello-view"></a><span data-ttu-id="05766-139">Modyfikowanie hello widoku</span><span class="sxs-lookup"><span data-stu-id="05766-139">Modifying hello View</span></span>
<span data-ttu-id="05766-140">Teraz zmodyfikuj wiadomości powitania toodisplay widoku hello "Zapraszamy tooExpress na platformie Azure".</span><span class="sxs-lookup"><span data-stu-id="05766-140">Now modify hello view toodisplay hello message "Welcome tooExpress in Azure".</span></span>

1. <span data-ttu-id="05766-141">Wprowadź poniższe polecenie tooopen hello index.jade plik hello:</span><span class="sxs-lookup"><span data-stu-id="05766-141">Enter hello following command tooopen hello index.jade file:</span></span>
   
       PS C:\node\expressapp\WebRole1> notepad views/index.jade
   
   ![zawartość Hello hello index.jade pliku.](./media/cloud-services-nodejs-develop-deploy-express-app/getting-started-19.png)
   
   <span data-ttu-id="05766-143">Jade jest hello domyślny aparat widoku używany przez aplikacje Express.</span><span class="sxs-lookup"><span data-stu-id="05766-143">Jade is hello default view engine used by Express applications.</span></span> <span data-ttu-id="05766-144">Aby uzyskać więcej informacji na powitania aparatu Jade widoku, zobacz [http://jade-lang.com][http://jade-lang.com].</span><span class="sxs-lookup"><span data-stu-id="05766-144">For more information on hello Jade view engine, see [http://jade-lang.com][http://jade-lang.com].</span></span>
2. <span data-ttu-id="05766-145">Modyfikowanie hello ostatni wiersz tekstu przez dołączenie **na platformie Azure**.</span><span class="sxs-lookup"><span data-stu-id="05766-145">Modify hello last line of text by appending **in Azure**.</span></span>
   
   ![odczytuje hello ostatni wiersz pliku index.jade Hello: p Witamy zbyt\#{nazwa} na platformie Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node31.png)
3. <span data-ttu-id="05766-147">Zapisz plik hello i Zakończ działanie Notatnika.</span><span class="sxs-lookup"><span data-stu-id="05766-147">Save hello file and exit Notepad.</span></span>
4. <span data-ttu-id="05766-148">Odśwież przeglądarkę i zobaczą zmiany.</span><span class="sxs-lookup"><span data-stu-id="05766-148">Refresh your browser and you will see your changes.</span></span>
   
   ![Okno przeglądarki, strona hello zawiera powitalnej tooExpress na platformie Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node32.png)

<span data-ttu-id="05766-150">Po testowania aplikacji hello, użyj hello **Stop AzureEmulator** emulatora hello toostop polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="05766-150">After testing hello application, use hello **Stop-AzureEmulator** cmdlet toostop hello emulator.</span></span>

## <a name="publishing-hello-application-tooazure"></a><span data-ttu-id="05766-151">Publikowanie tooAzure aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="05766-151">Publishing hello Application tooAzure</span></span>
<span data-ttu-id="05766-152">W oknie programu PowerShell Azure hello, użyj hello **Publish-AzureServiceProject** usługi chmury tooa aplikacji hello toodeploy polecenia cmdlet</span><span class="sxs-lookup"><span data-stu-id="05766-152">In hello Azure PowerShell window, use hello **Publish-AzureServiceProject** cmdlet toodeploy hello application tooa cloud service</span></span>

    PS C:\node\expressapp\WebRole1> Publish-AzureServiceProject -ServiceName myexpressapp -Location "East US" -Launch

<span data-ttu-id="05766-153">Po zakończeniu operacji wdrażania hello przeglądarki otworzyć i wyświetlić stronę sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="05766-153">Once hello deployment operation completes, your browser will open and display hello web page.</span></span>

![Przeglądarka wyświetlająca stronę Express hello.](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="next-steps"></a><span data-ttu-id="05766-156">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="05766-156">Next steps</span></span>
<span data-ttu-id="05766-157">Aby uzyskać więcej informacji, zobacz hello [Centrum deweloperów środowiska Node.js](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="05766-157">For more information, see hello [Node.js Developer Center](/develop/nodejs/).</span></span>

[Node.js Web Application]: http://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
[Express]: http://expressjs.com/
[http://jade-lang.com]: http://jade-lang.com


