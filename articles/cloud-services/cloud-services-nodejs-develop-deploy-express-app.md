---
title: "Sieci Web aplikacji w usłudze Express (Node.js) | Dokumentacja firmy Microsoft"
description: "Samouczek, opiera się na samouczek usługi chmury, która ilustruje sposób korzystania z modułu Express."
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
ms.openlocfilehash: 54b715695e24786ec4e8dfcabefc648d76179c8b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="build-a-nodejs-web-application-using-express-on-an-azure-cloud-service"></a><span data-ttu-id="197f1-103">Tworzenie aplikacji sieci web Node.js za pomocą ekspresowego na usługi w chmurze platformy Azure</span><span class="sxs-lookup"><span data-stu-id="197f1-103">Build a Node.js web application using Express on an Azure Cloud Service</span></span>
<span data-ttu-id="197f1-104">Node.js zawiera minimalny zestaw funkcji w podstawowego środowiska wykonawczego.</span><span class="sxs-lookup"><span data-stu-id="197f1-104">Node.js includes a minimal set of functionality in the core runtime.</span></span>
<span data-ttu-id="197f1-105">Deweloperzy często używane 3 modułów strona oferowanie dodatkowych funkcji podczas opracowywania aplikacji Node.js.</span><span class="sxs-lookup"><span data-stu-id="197f1-105">Developers often use 3rd party modules to provide additional functionality when developing a Node.js application.</span></span> <span data-ttu-id="197f1-106">W tym samouczku spowoduje utworzenie nowej aplikacji przy użyciu [Express] [ Express] moduł, który zapewnia platformę MVC do tworzenia aplikacji sieci web Node.js.</span><span class="sxs-lookup"><span data-stu-id="197f1-106">In this tutorial you will create a new application using the [Express][Express] module, which provides an MVC framework for creating Node.js web applications.</span></span>

<span data-ttu-id="197f1-107">Zrzut ekranu przedstawiający ukończona aplikacja znajduje się poniżej:</span><span class="sxs-lookup"><span data-stu-id="197f1-107">A screenshot of the completed application is below:</span></span>

![Przeglądarka wyświetlająca Zapraszamy do Express na platformie Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="create-a-cloud-service-project"></a><span data-ttu-id="197f1-109">Tworzenie projektu usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="197f1-109">Create a Cloud Service Project</span></span>
[!INCLUDE [install-dev-tools](../../includes/install-dev-tools.md)]

<span data-ttu-id="197f1-110">Wykonaj poniższe kroki, aby utworzyć nowy projekt usługi w chmurze o nazwie "expressapp":</span><span class="sxs-lookup"><span data-stu-id="197f1-110">Perform the following steps to create a new cloud service project named 'expressapp':</span></span>

1. <span data-ttu-id="197f1-111">Z **Start Menu** lub **ekranu startowego**, wyszukaj **programu Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="197f1-111">From the **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span> <span data-ttu-id="197f1-112">Na koniec kliknij prawym przyciskiem myszy **programu Windows PowerShell** i wybierz **Uruchom jako Administrator**.</span><span class="sxs-lookup"><span data-stu-id="197f1-112">Finally, right-click **Windows PowerShell** and select **Run As Administrator**.</span></span>
   
    ![Ikona Azure PowerShell](./media/cloud-services-nodejs-develop-deploy-express-app/azure-powershell-start.png)
2. <span data-ttu-id="197f1-114">Przejdź do **c:\\węzła** katalogu, a następnie wprowadź następujące polecenia, aby utworzyć nowe rozwiązanie o nazwie **expressapp** i rolę sieci web o nazwie **WebRole1**:</span><span class="sxs-lookup"><span data-stu-id="197f1-114">Change directories to the **c:\\node** directory and then enter the following commands to create a new solution named **expressapp** and a web role named **WebRole1**:</span></span>
   
        PS C:\node> New-AzureServiceProject expressapp
        PS C:\Node\expressapp> Add-AzureNodeWebRole
        PS C:\Node\expressapp> Set-AzureServiceProjectRole WebRole1 Node 0.10.21
   
    > [!NOTE]
    > <span data-ttu-id="197f1-115">Domyślnie **Add-AzureNodeWebRole** używa starszej wersji środowiska node.js.</span><span class="sxs-lookup"><span data-stu-id="197f1-115">By default, **Add-AzureNodeWebRole** uses an older version of Node.js.</span></span> <span data-ttu-id="197f1-116">**AzureServiceProjectRole zestaw** powyższych instrukcji nakazuje Azure, aby użyć v0.10.21 węzła.</span><span class="sxs-lookup"><span data-stu-id="197f1-116">The **Set-AzureServiceProjectRole** statement above instructs Azure to use v0.10.21 of Node.</span></span>  <span data-ttu-id="197f1-117">Należy zauważyć, że parametry jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="197f1-117">Note the parameters are case-sensitive.</span></span>  <span data-ttu-id="197f1-118">Można sprawdzić poprawnej wersji środowiska Node.js została wybrana sprawdzając **aparaty** właściwości w **WebRole1\package.json**.</span><span class="sxs-lookup"><span data-stu-id="197f1-118">You can verify the correct version of Node.js has been selected by checking the **engines** property in **WebRole1\package.json**.</span></span>
    > 
    > 

## <a name="install-express"></a><span data-ttu-id="197f1-119">Zainstaluj Express</span><span class="sxs-lookup"><span data-stu-id="197f1-119">Install Express</span></span>
1. <span data-ttu-id="197f1-120">Generator aplikacji Express należy zainstalować wydając polecenie:</span><span class="sxs-lookup"><span data-stu-id="197f1-120">Install the Express generator by issuing the following command:</span></span>
   
        PS C:\node\expressapp> npm install express-generator -g
   
    <span data-ttu-id="197f1-121">Dane wyjściowe polecenia npm powinien wyglądać podobnie do poniższych wyników.</span><span class="sxs-lookup"><span data-stu-id="197f1-121">The output of the npm command should look similar to the result below.</span></span> 
   
    ![Wyświetlanie npm środowiska Windows PowerShell instalacji ekspresowej polecenia.](./media/cloud-services-nodejs-develop-deploy-express-app/express-g.png)
2. <span data-ttu-id="197f1-123">Przejdź do **WebRole1** katalogu i użyj polecenia express, aby wygenerować nową aplikację:</span><span class="sxs-lookup"><span data-stu-id="197f1-123">Change directories to the **WebRole1** directory and use the express command to generate a new application:</span></span>
   
        PS C:\node\expressapp\WebRole1> express
   
    <span data-ttu-id="197f1-124">Pojawi się monit zastąpienie starszych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="197f1-124">You will be prompted to overwrite your earlier application.</span></span> <span data-ttu-id="197f1-125">Wprowadź **y** lub **tak** aby kontynuować.</span><span class="sxs-lookup"><span data-stu-id="197f1-125">Enter **y** or **yes** to continue.</span></span> <span data-ttu-id="197f1-126">Express spowoduje wygenerowanie pliku app.js i struktury folderów, do tworzenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="197f1-126">Express will generate the app.js file and a folder structure for building your application.</span></span>
   
    ![Dane wyjściowe polecenia express](./media/cloud-services-nodejs-develop-deploy-express-app/node23.png)
3. <span data-ttu-id="197f1-128">Aby zainstalować dodatkowe zależności zdefiniowane w pliku package.json, wprowadź następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="197f1-128">To install additional dependencies defined in the package.json file, enter the following command:</span></span>
   
       PS C:\node\expressapp\WebRole1> npm install
   
   ![Dane wyjściowe programu npm install, polecenie](./media/cloud-services-nodejs-develop-deploy-express-app/node26.png)
4. <span data-ttu-id="197f1-130">Użyj następującego polecenia, aby skopiować **bin/www** pliku **server.js**.</span><span class="sxs-lookup"><span data-stu-id="197f1-130">Use the following command to copy the **bin/www** file to **server.js**.</span></span> <span data-ttu-id="197f1-131">Jest to tak usługi w chmurze można znaleźć punktu wejścia dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="197f1-131">This is so the cloud service can find the entry point for this application.</span></span>
   
       PS C:\node\expressapp\WebRole1> copy bin/www server.js
   
   <span data-ttu-id="197f1-132">Po wykonaniu tego polecenia, powinien mieć **server.js** pliku w katalogu WebRole1.</span><span class="sxs-lookup"><span data-stu-id="197f1-132">After this command completes, you should have a **server.js** file in the WebRole1 directory.</span></span>
5. <span data-ttu-id="197f1-133">Modyfikowanie **server.js** Aby usunąć jedną z '.' znaków z następującego wiersza.</span><span class="sxs-lookup"><span data-stu-id="197f1-133">Modify the **server.js** to remove one of the '.' characters from the following line.</span></span>
   
       var app = require('../app');
   
   <span data-ttu-id="197f1-134">Po wprowadzeniu tej zmiany należy wiersz powinna wyglądać następująco.</span><span class="sxs-lookup"><span data-stu-id="197f1-134">After making this modification, the line should appear as follows.</span></span>
   
       var app = require('./app');
   
   <span data-ttu-id="197f1-135">Ta zmiana jest wymagana, ponieważ przenieśliśmy pliku (dawniej **bin/www**,) na tym samym katalogu co plik aplikacji jest wymagany.</span><span class="sxs-lookup"><span data-stu-id="197f1-135">This change is required since we moved the file (formerly **bin/www**,) to the same directory as the app file being required.</span></span> <span data-ttu-id="197f1-136">Po wprowadzeniu tej zmiany należy zapisać **server.js** pliku.</span><span class="sxs-lookup"><span data-stu-id="197f1-136">After making this change, save the **server.js** file.</span></span>
6. <span data-ttu-id="197f1-137">Aby uruchomić aplikację w emulatorze platformy Azure, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="197f1-137">Use the following command to run the application in the Azure emulator:</span></span>
   
       PS C:\node\expressapp\WebRole1> Start-AzureEmulator -launch
   
    ![Strony sieci web zawierającej express — Zapraszamy!.](./media/cloud-services-nodejs-develop-deploy-express-app/node28.png)

## <a name="modifying-the-view"></a><span data-ttu-id="197f1-139">Zmodyfikowanie widoku</span><span class="sxs-lookup"><span data-stu-id="197f1-139">Modifying the View</span></span>
<span data-ttu-id="197f1-140">Teraz zmodyfikuj widok, aby wyświetlić komunikat "Zapraszamy do Express w Azure".</span><span class="sxs-lookup"><span data-stu-id="197f1-140">Now modify the view to display the message "Welcome to Express in Azure".</span></span>

1. <span data-ttu-id="197f1-141">Wprowadź następujące polecenie, aby otworzyć plik index.jade:</span><span class="sxs-lookup"><span data-stu-id="197f1-141">Enter the following command to open the index.jade file:</span></span>
   
       PS C:\node\expressapp\WebRole1> notepad views/index.jade
   
   ![Zawartość pliku index.jade.](./media/cloud-services-nodejs-develop-deploy-express-app/getting-started-19.png)
   
   <span data-ttu-id="197f1-143">Jade jest domyślny aparat widoku używany przez aplikacje Express.</span><span class="sxs-lookup"><span data-stu-id="197f1-143">Jade is the default view engine used by Express applications.</span></span> <span data-ttu-id="197f1-144">Aby uzyskać więcej informacji na aparatu Jade widoku, zobacz [http://jade-lang.com][http://jade-lang.com].</span><span class="sxs-lookup"><span data-stu-id="197f1-144">For more information on the Jade view engine, see [http://jade-lang.com][http://jade-lang.com].</span></span>
2. <span data-ttu-id="197f1-145">Modyfikowanie ostatniego wiersza tekstu przez dołączenie **na platformie Azure**.</span><span class="sxs-lookup"><span data-stu-id="197f1-145">Modify the last line of text by appending **in Azure**.</span></span>
   
   ![Odczytuje ostatni wiersz w pliku index.jade: p — Zapraszamy! \#{nazwa} na platformie Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node31.png)
3. <span data-ttu-id="197f1-147">Zapisz plik i zamknij Notatnik.</span><span class="sxs-lookup"><span data-stu-id="197f1-147">Save the file and exit Notepad.</span></span>
4. <span data-ttu-id="197f1-148">Odśwież przeglądarkę i zobaczą zmiany.</span><span class="sxs-lookup"><span data-stu-id="197f1-148">Refresh your browser and you will see your changes.</span></span>
   
   ![Okno przeglądarki, strona zawiera Express na platformie Azure — Zapraszamy!](./media/cloud-services-nodejs-develop-deploy-express-app/node32.png)

<span data-ttu-id="197f1-150">Po zakończeniu testowania aplikacji, użyj **Stop AzureEmulator** polecenia cmdlet, aby zatrzymać emulator.</span><span class="sxs-lookup"><span data-stu-id="197f1-150">After testing the application, use the **Stop-AzureEmulator** cmdlet to stop the emulator.</span></span>

## <a name="publishing-the-application-to-azure"></a><span data-ttu-id="197f1-151">Publikowanie aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="197f1-151">Publishing the Application to Azure</span></span>
<span data-ttu-id="197f1-152">W oknie programu Azure PowerShell, użyj **Publish-AzureServiceProject** polecenia cmdlet, aby wdrożyć aplikację usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="197f1-152">In the Azure PowerShell window, use the **Publish-AzureServiceProject** cmdlet to deploy the application to a cloud service</span></span>

    PS C:\node\expressapp\WebRole1> Publish-AzureServiceProject -ServiceName myexpressapp -Location "East US" -Launch

<span data-ttu-id="197f1-153">Po zakończeniu operacji wdrażania, przeglądarki otworzyć i wyświetli tej strony sieci web.</span><span class="sxs-lookup"><span data-stu-id="197f1-153">Once the deployment operation completes, your browser will open and display the web page.</span></span>

![Przeglądarka wyświetlająca stronę Express.](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="next-steps"></a><span data-ttu-id="197f1-156">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="197f1-156">Next steps</span></span>
<span data-ttu-id="197f1-157">Aby uzyskać więcej informacji, odwiedź stronę [Centrum deweloperów środowiska Node.js](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="197f1-157">For more information, see the [Node.js Developer Center](/develop/nodejs/).</span></span>

[Node.js Web Application]: http://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
[Express]: http://expressjs.com/
[http://jade-lang.com]: http://jade-lang.com


