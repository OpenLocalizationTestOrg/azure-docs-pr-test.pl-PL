---
title: "aaaSpecifying wersji środowiska Node.js"
description: "Dowiedz się, jak toospecify hello wersji środowiska Node.js używane przez witryny sieci Web platformy Azure i usługi w chmurze"
services: 
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d0e15278-2ab4-4ec8-8256-913839c6d5ef
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 09c27bfc43c132b6d66f9a2943179e06ee75bedc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-a-nodejs-version-in-an-azure-application"></a><span data-ttu-id="a97d3-103">Specifying a Node.js version in an Azure application (Określanie wersji środowiska Node.js w aplikacji Azure)</span><span class="sxs-lookup"><span data-stu-id="a97d3-103">Specifying a Node.js version in an Azure application</span></span>
<span data-ttu-id="a97d3-104">Hosting aplikacji Node.js, możesz tooensure, że aplikacja korzysta z określonej wersji środowiska node.js.</span><span class="sxs-lookup"><span data-stu-id="a97d3-104">When hosting a Node.js application, you may want tooensure that your application uses a specific version of Node.js.</span></span> <span data-ttu-id="a97d3-105">Istnieje kilka sposobów tooaccomplish to dla aplikacji hostowanej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="a97d3-105">There are several ways tooaccomplish this for applications hosted on Azure.</span></span>

## <a name="default-versions"></a><span data-ttu-id="a97d3-106">Wersji domyślnej</span><span class="sxs-lookup"><span data-stu-id="a97d3-106">Default versions</span></span>
<span data-ttu-id="a97d3-107">wersje Node.js Hello dostarczany przez platformę Azure są stale aktualizowane.</span><span class="sxs-lookup"><span data-stu-id="a97d3-107">hello Node.js versions provided by Azure are constantly updated.</span></span> <span data-ttu-id="a97d3-108">Inaczej, hello domyślnej wersji, który określono w hello `WEBSITE_NODE_DEFAULT_VERSION` będzie można użyć zmiennej środowiskowej.</span><span class="sxs-lookup"><span data-stu-id="a97d3-108">Unless otherwise specified, hello default version that is specified in hello `WEBSITE_NODE_DEFAULT_VERSION` environment variable will be used.</span></span> <span data-ttu-id="a97d3-109">toooverride wartość domyślną, wykonaj kroki hello w następujących sekcjach tego artykułu</span><span class="sxs-lookup"><span data-stu-id="a97d3-109">toooverride this default value, follow hello steps in following sections of this article</span></span>

> [!NOTE]
> <span data-ttu-id="a97d3-110">Jeśli są obsługę aplikacji we usługi w chmurze Azure (rola sieci web lub procesu roboczego) i jest pierwszym wdrożeniu aplikacji hello hello, Azure podejmie toouse hello tę samą wersję programu Node.js, jak został zainstalowany na środowiska projektowego, jeśli go zgodny z wersjami domyślne hello dostępnymi na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="a97d3-110">If you are hosting your application in an Azure Cloud Service (web or worker role,) and it is hello first time you have deployed hello application, Azure will attempt toouse hello same version of Node.js as you have installed on your development environment if it matches one of hello default versions available on Azure.</span></span>
>
>

## <a name="versioning-with-packagejson"></a><span data-ttu-id="a97d3-111">Przechowywanie wersji pliku package.json</span><span class="sxs-lookup"><span data-stu-id="a97d3-111">Versioning with package.json</span></span>
<span data-ttu-id="a97d3-112">Można określić wersji hello toobe Node.js używane przez dodanie powitania po tooyour **package.json** pliku:</span><span class="sxs-lookup"><span data-stu-id="a97d3-112">You can specify hello version of Node.js toobe used by adding hello following tooyour **package.json** file:</span></span>

    "engines":{"node":version}

<span data-ttu-id="a97d3-113">Gdzie *wersji* jest toouse numer hello określonej wersji.</span><span class="sxs-lookup"><span data-stu-id="a97d3-113">Where *version* is hello specific version number toouse.</span></span> <span data-ttu-id="a97d3-114">Można określić bardziej skomplikowane warunki dotyczące wersji, takich jak:</span><span class="sxs-lookup"><span data-stu-id="a97d3-114">You can specify more complex conditions for version, such as:</span></span>

    "engines":{"node": "0.6.22 || 0.8.x"}

<span data-ttu-id="a97d3-115">Ponieważ 0.6.22 nie jest jednym z hello wersjami dostępnymi w hello Środowisko hostingu, hello najwyższa wersja hello 0,8 serii, która jest dostępna będzie zamiast tego użyć - 0.8.4.</span><span class="sxs-lookup"><span data-stu-id="a97d3-115">Since 0.6.22 is not one of hello versions available in hello hosting environment, hello highest version of hello 0.8 series that is available will be used instead - 0.8.4.</span></span>

## <a name="versioning-websites-with-app-settings"></a><span data-ttu-id="a97d3-116">Przechowywanie wersji witryn sieci Web przy użyciu ustawień aplikacji</span><span class="sxs-lookup"><span data-stu-id="a97d3-116">Versioning Websites with App Settings</span></span>
<span data-ttu-id="a97d3-117">Jeśli prowadzą hosting aplikacji hello w witrynie sieci Web, można ustawić zmiennej środowiskowej hello **WEBSITE_NODE_DEFAULT_VERSION** toohello żądanej wersji.</span><span class="sxs-lookup"><span data-stu-id="a97d3-117">If you are hosting hello application in a Website, you can set hello environment variable **WEBSITE_NODE_DEFAULT_VERSION** toohello desired version.</span></span>

## <a name="versioning-cloud-services-with-powershell"></a><span data-ttu-id="a97d3-118">Przechowywanie wersji usługi w chmurze przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="a97d3-118">Versioning Cloud Services with PowerShell</span></span>
<span data-ttu-id="a97d3-119">Jeśli są hosting aplikacji hello w usłudze w chmurze i wdrażania aplikacji hello przy użyciu programu Azure PowerShell, można zastąpić domyślną wersję środowiska Node.js hello przy użyciu hello **AzureServiceProjectRole zestaw** polecenia cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a97d3-119">If you are hosting hello application in a Cloud Service, and are deploying hello application using Azure PowerShell, you can override hello default Node.js version by using hello **Set-AzureServiceProjectRole** PowerShell cmdlet.</span></span> <span data-ttu-id="a97d3-120">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="a97d3-120">For example:</span></span>

    Set-AzureServiceProjectRole WebRole1 Node 0.8.4

<span data-ttu-id="a97d3-121">Uwaga hello parametrów w hello powyżej instrukcji jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="a97d3-121">Note hello parameters in hello above statement are case-sensitive.</span></span>  <span data-ttu-id="a97d3-122">Możesz sprawdzić hello poprawną wersję środowiska Node.js została wybrana sprawdzając hello **aparaty** właściwości w roli użytkownika **package.json**.</span><span class="sxs-lookup"><span data-stu-id="a97d3-122">You can verify hello correct version of Node.js has been selected by checking hello **engines** property in your role's **package.json**.</span></span>

<span data-ttu-id="a97d3-123">Można również użyć hello **Get-AzureServiceProjectRoleRuntime** tooretrieve listę dostępnych dla aplikacji hostowanej jako usługa w chmurze wersji środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="a97d3-123">You can also use hello **Get-AzureServiceProjectRoleRuntime** tooretrieve a list of Node.js versions available for applications hosted as a Cloud Service.</span></span>  <span data-ttu-id="a97d3-124">Zawsze, czy wersja hello Node.js zależy od projektu jest na tej liście.</span><span class="sxs-lookup"><span data-stu-id="a97d3-124">Always verify hello version of Node.js your project depends on is in this list.</span></span>

## <a name="using-a-custom-version-with-azure-websites"></a><span data-ttu-id="a97d3-125">Przy użyciu dostosowanej wersji z witrynami sieci Web Azure</span><span class="sxs-lookup"><span data-stu-id="a97d3-125">Using a custom version with Azure Websites</span></span>
<span data-ttu-id="a97d3-126">Azure zapewnia kilka wersji domyślnej Node.js, jednocześnie może być toouse wersji, która domyślnie nie jest dostępne.</span><span class="sxs-lookup"><span data-stu-id="a97d3-126">While Azure provides several default versions of Node.js, you may want toouse a version that is not provided by default.</span></span> <span data-ttu-id="a97d3-127">Jeśli aplikacja jest obsługiwana jako witryny sieci Web platformy Azure, możesz to zrobić przy użyciu hello **plik iisnode.yml** pliku.</span><span class="sxs-lookup"><span data-stu-id="a97d3-127">If your application is hosted as an Azure Website, you can accomplish this by using hello **iisnode.yml** file.</span></span> <span data-ttu-id="a97d3-128">Witaj kolejnych krokach objaśniono proces hello przy użyciu dostosowanej wersji środowiska Node.Js z witryny sieci Web platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="a97d3-128">hello following steps walk through hello process of using a custom version of Node.Js with an Azure Website:</span></span>

1. <span data-ttu-id="a97d3-129">Utwórz nowy katalog, a następnie utwórz **server.js** pliku w katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="a97d3-129">Create a new directory, and then create a **server.js** file within hello directory.</span></span> <span data-ttu-id="a97d3-130">Witaj **server.js** plik powinien zawierać hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a97d3-130">hello **server.js** file should contain hello following:</span></span>

        var http = require('http');
        http.createServer(function(req,res) {
          res.writeHead(200, {'Content-Type': 'text/html'});
          res.end('Hello from Azure running node version: ' + process.version + '</br>');
        }).listen(process.env.PORT || 3000);

    <span data-ttu-id="a97d3-131">Spowoduje to wyświetlenie wersji środowiska Node.js hello używane podczas przeglądania hello witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="a97d3-131">This will display hello Node.js version being used when you browse hello website.</span></span>
2. <span data-ttu-id="a97d3-132">Tworzenie nowej witryny sieci Web i nazwa hello Uwaga hello witryny.</span><span class="sxs-lookup"><span data-stu-id="a97d3-132">Create a new Website and note hello name of hello site.</span></span> <span data-ttu-id="a97d3-133">Na przykład następujące hello używa hello [narzędzi wiersza polecenia platformy Azure] toocreate nowej witryny internetowej platformy Azure o nazwie **MojaWitrynaSieciWeb**, a następnie włącz repozytorium Git hello witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="a97d3-133">For example, hello following uses hello [Azure Command-line tools] toocreate a new Azure Website named **mywebsite**, and then enable a Git repository for hello website.</span></span>

        azure site create mywebsite --git
3. <span data-ttu-id="a97d3-134">Utwórz nowy katalog o nazwie **bin** jako element podrzędny hello katalog zawierający hello **server.js** pliku.</span><span class="sxs-lookup"><span data-stu-id="a97d3-134">Create a new directory named **bin** as a child of hello directory containing hello **server.js** file.</span></span>
4. <span data-ttu-id="a97d3-135">Pobierz hello określonej wersji **node.exe** (wersja systemu Windows hello) mają toouse z aplikacją.</span><span class="sxs-lookup"><span data-stu-id="a97d3-135">Download hello specific version of **node.exe** (hello Windows version) that you wish toouse with your application.</span></span> <span data-ttu-id="a97d3-136">Na przykład Witaj następujących używa **curl** toodownload wersji 0.8.1:</span><span class="sxs-lookup"><span data-stu-id="a97d3-136">For example, hello following uses **curl** toodownload version 0.8.1:</span></span>

        curl -O http://nodejs.org/dist/v0.8.1/node.exe

    <span data-ttu-id="a97d3-137">Zapisz hello **node.exe** pliku do hello **bin** folder utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="a97d3-137">Save hello **node.exe** file into hello **bin** folder created previously.</span></span>
5. <span data-ttu-id="a97d3-138">Utwórz **plik iisnode.yml** w pliku hello sam katalogu jako hello **server.js** pliku, a następnie dodaj powitania po zawartości toohello **plik iisnode.yml** pliku:</span><span class="sxs-lookup"><span data-stu-id="a97d3-138">Create an **iisnode.yml** file in hello same directory as hello **server.js** file, and then add hello following content toohello **iisnode.yml** file:</span></span>

        nodeProcessCommandLine: "D:\home\site\wwwroot\bin\node.exe"

    <span data-ttu-id="a97d3-139">Jest to ścieżka, gdzie hello **node.exe** pliku w projekcie zostaną umieszczone po opublikowaniu toohello Twojej aplikacji witryny sieci Web Azure.</span><span class="sxs-lookup"><span data-stu-id="a97d3-139">This path is where hello **node.exe** file within your project will be located once you have published your application toohello Azure Website.</span></span>
6. <span data-ttu-id="a97d3-140">Publikowanie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a97d3-140">Publish your application.</span></span> <span data-ttu-id="a97d3-141">Na przykład ponieważ wcześniej utworzona nowej witryny sieci Web z parametrem--git hello, hello następujące polecenia spowoduje dodanie hello aplikacji pliki toomy lokalnego repozytorium Git i następnie wypchniesz toohello repozytorium witryny sieci Web:</span><span class="sxs-lookup"><span data-stu-id="a97d3-141">For example, since I created a new website with hello --git parameter earlier, hello following commands will add hello application files toomy local Git repository, and then push them toohello website repository:</span></span>

        git add .
        git commit -m "testing node v0.8.1"
        git push azure master

    <span data-ttu-id="a97d3-142">Po opublikowaniu aplikacji hello ma Otwórz hello witryny sieci Web w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="a97d3-142">After hello application has published, open hello website in a browser.</span></span> <span data-ttu-id="a97d3-143">Powinien zostać wyświetlony komunikat z informacją "Hello Azure uruchomionej wersji węzła: v0.8.1".</span><span class="sxs-lookup"><span data-stu-id="a97d3-143">You should see a message stating "Hello from Azure running node version: v0.8.1".</span></span>

## <a name="next-steps"></a><span data-ttu-id="a97d3-144">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a97d3-144">Next Steps</span></span>
<span data-ttu-id="a97d3-145">Teraz, że rozumiesz, jak wersja hello toospecify Node.js używanych przez aplikację, Dowiedz się, jak za[Praca z modułami], [tworzenia i wdrażania witryn sieci Web Node.js](app-service-web/app-service-web-get-started-nodejs.md), i [jak toouse hello Azure Narzędzia wiersza polecenia dla komputerów Mac i Linux].</span><span class="sxs-lookup"><span data-stu-id="a97d3-145">Now that you understand how toospecify hello version of Node.js used by your application, learn how too[work with modules], [build and deploy a Node.js Web Site](app-service-web/app-service-web-get-started-nodejs.md), and [How toouse hello Azure Command-Line Tools for Mac and Linux].</span></span>

<span data-ttu-id="a97d3-146">Aby uzyskać więcej informacji, zobacz hello [Centrum deweloperów środowiska Node.js](https://azure.microsoft.com/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="a97d3-146">For more information, see hello [Node.js Developer Center](https://azure.microsoft.com/develop/nodejs/).</span></span>

[jak toouse hello Azure Narzędzia wiersza polecenia dla komputerów Mac i Linux]:cli-install-nodejs.md
[narzędzi wiersza polecenia platformy Azure]:cli-install-nodejs.md
[Praca z modułami]: nodejs-use-node-modules-azure-apps.md
[build and deploy a Node.js Web Site]: app-service-web/app-service-web-get-started-nodejs.md
