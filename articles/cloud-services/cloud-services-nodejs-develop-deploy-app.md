---
title: "aaaNode.js Wprowadzenie — przewodnik | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate proste Node.js aplikacja sieci web, a następnie wdrożyć go tooan usługi w chmurze Azure."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 50951a87-fed4-48e0-bcfa-453b9e50452e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 22945bfcc1b0e5da2a2d37dc5cc86be013cc0b5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="build-and-deploy-a-nodejs-application-tooan-azure-cloud-service"></a><span data-ttu-id="0214b-103">Tworzenie i wdrażanie tooan aplikacji Node.js usługi w chmurze Azure</span><span class="sxs-lookup"><span data-stu-id="0214b-103">Build and deploy a Node.js application tooan Azure Cloud Service</span></span>

<span data-ttu-id="0214b-104">Ten samouczek pokazuje, jak toocreate proste Node.js aplikacji uruchomionej w usłudze w chmurze Azure.</span><span class="sxs-lookup"><span data-stu-id="0214b-104">This tutorial shows how toocreate a simple Node.js application running in an Azure Cloud Service.</span></span> <span data-ttu-id="0214b-105">Usługi w chmurze są blokami konstrukcyjnymi hello z skalowalnych aplikacji w chmurze na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="0214b-105">Cloud Services are hello building blocks of scalable cloud applications in Azure.</span></span> <span data-ttu-id="0214b-106">Umożliwiają one separacji hello oraz niezależne zarządzanie i skalowania w poziomie składników frontonu i zaplecza aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0214b-106">They allow hello separation and independent management and scale-out of front-end and back-end components of your application.</span></span>  <span data-ttu-id="0214b-107">Usługi Cloud Services oferują specjalną maszynę wirtualną, która w niezawodny sposób hostuje poszczególne role.</span><span class="sxs-lookup"><span data-stu-id="0214b-107">Cloud Services provide a robust dedicated virtual machine for hosting each role reliably.</span></span>

<span data-ttu-id="0214b-108">Aby uzyskać więcej informacji dotyczących usługi w chmurze, oraz ich porównanie tooAzure witryn sieci Web i maszyn wirtualnych, zobacz [porównanie witryn sieci Web platformy Azure, usługi w chmurze i maszyn wirtualnych].</span><span class="sxs-lookup"><span data-stu-id="0214b-108">For more information on Cloud Services, and how they compare tooAzure Websites and Virtual machines, see [Azure Websites, Cloud Services and Virtual Machines comparison].</span></span>

> [!TIP]
> <span data-ttu-id="0214b-109">Szukasz toobuild prosty witryny sieci Web?</span><span class="sxs-lookup"><span data-stu-id="0214b-109">Looking toobuild a simple website?</span></span> <span data-ttu-id="0214b-110">Jeśli scenariusz obejmuje tylko prosty fronton witryny sieci Web, rozważ użycie [korzystanie z lekkiej aplikacji sieci web].</span><span class="sxs-lookup"><span data-stu-id="0214b-110">If your scenario involves just a simple website front-end, consider [using a lightweight web app].</span></span> <span data-ttu-id="0214b-111">Możesz łatwo przeprowadzić uaktualnienie tooa usługi w chmurze rozwoju witryny sieci web lub zmiany wymagań.</span><span class="sxs-lookup"><span data-stu-id="0214b-111">You can easily upgrade tooa Cloud Service as your web app grows and your requirements change.</span></span>

<span data-ttu-id="0214b-112">Wykonując czynności opisane w tym samouczku, utworzysz prostą aplikację sieci Web hostowaną wewnątrz roli sieci Web.</span><span class="sxs-lookup"><span data-stu-id="0214b-112">By following this tutorial, you will build a simple web application hosted inside a web role.</span></span> <span data-ttu-id="0214b-113">Będzie korzystać z aplikacji tootest emulatora obliczeń hello lokalnie, a następnie wdróż je za pomocą narzędzia wiersza polecenia programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0214b-113">You will use hello compute emulator tootest your application locally, then deploy it using PowerShell command-line tools.</span></span>

<span data-ttu-id="0214b-114">Aplikacja Hello jest prostą aplikację "hello world":</span><span class="sxs-lookup"><span data-stu-id="0214b-114">hello application is a simple "hello world" application:</span></span>

![Przeglądarka wyświetlająca stronę sieci web Hello World hello][A web browser displaying hello Hello World web page]

## <a name="prerequisites"></a><span data-ttu-id="0214b-116">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="0214b-116">Prerequisites</span></span>
> [!NOTE]
> <span data-ttu-id="0214b-117">W tym samouczku jest używany program Azure PowerShell, który wymaga systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="0214b-117">This tutorial uses Azure PowerShell, which requires Windows.</span></span>

* <span data-ttu-id="0214b-118">Zainstalowanie i skonfigurowanie programu [Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="0214b-118">Install and configure [Azure Powershell].</span></span>
* <span data-ttu-id="0214b-119">Pobierz i zainstaluj hello [zestaw Azure SDK for .NET 2.7].</span><span class="sxs-lookup"><span data-stu-id="0214b-119">Download and install hello [Azure SDK for .NET 2.7].</span></span> <span data-ttu-id="0214b-120">W hello instalacji Instalatora, wybierz opcję:</span><span class="sxs-lookup"><span data-stu-id="0214b-120">In hello install setup, select:</span></span>
  * <span data-ttu-id="0214b-121">MicrosoftAzureAuthoringTools</span><span class="sxs-lookup"><span data-stu-id="0214b-121">MicrosoftAzureAuthoringTools</span></span>
  * <span data-ttu-id="0214b-122">MicrosoftAzureComputeEmulator</span><span class="sxs-lookup"><span data-stu-id="0214b-122">MicrosoftAzureComputeEmulator</span></span>

## <a name="create-an-azure-cloud-service-project"></a><span data-ttu-id="0214b-123">Tworzenie projektu Usługi w chmurze Azure</span><span class="sxs-lookup"><span data-stu-id="0214b-123">Create an Azure Cloud Service project</span></span>
<span data-ttu-id="0214b-124">Wykonaj następujące zadania toocreate nowy projekt usługi w chmurze Azure, wraz z podstawowych szkieletów języka Node.js hello:</span><span class="sxs-lookup"><span data-stu-id="0214b-124">Perform hello following tasks toocreate a new Azure Cloud Service project, along with basic Node.js scaffolding:</span></span>

1. <span data-ttu-id="0214b-125">Uruchom **programu Windows PowerShell** jako Administrator; z hello **Start Menu** lub **ekranu startowego**, wyszukaj **programu Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="0214b-125">Run **Windows PowerShell** as Administrator; from hello **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span>
2. <span data-ttu-id="0214b-126">[Connect PowerShell] tooyour subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="0214b-126">[Connect PowerShell] tooyour subscription.</span></span>
3. <span data-ttu-id="0214b-127">Wprowadź hello następującego środowiska PowerShell polecenia cmdlet toocreate toocreate hello projektu:</span><span class="sxs-lookup"><span data-stu-id="0214b-127">Enter hello following PowerShell cmdlet toocreate toocreate hello project:</span></span>

        New-AzureServiceProject helloworld

    ![wynik Hello hello New-AzureService helloworld polecenia][hello result of hello New-AzureService helloworld command]

    <span data-ttu-id="0214b-129">Witaj **New-AzureServiceProject** polecenia cmdlet wygenerowanie podstawowej struktury publikowania tooa aplikacji Node.js usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="0214b-129">hello **New-AzureServiceProject** cmdlet generates a basic structure for publishing a Node.js application tooa Cloud Service.</span></span> <span data-ttu-id="0214b-130">Zawiera ona pliki konfiguracji niezbędne do publikowania tooAzure.</span><span class="sxs-lookup"><span data-stu-id="0214b-130">It contains configuration files necessary for publishing tooAzure.</span></span> <span data-ttu-id="0214b-131">Witaj polecenie cmdlet zmienia także katalog roboczy katalogu toohello hello usługi.</span><span class="sxs-lookup"><span data-stu-id="0214b-131">hello cmdlet also changes your working directory toohello directory for hello service.</span></span>

    <span data-ttu-id="0214b-132">polecenie cmdlet Hello tworzy hello następujące pliki:</span><span class="sxs-lookup"><span data-stu-id="0214b-132">hello cmdlet creates hello following files:</span></span>

   * <span data-ttu-id="0214b-133">**ServiceConfiguration.Cloud.cscfg**, **ServiceConfiguration.Local.cscfg** i **ServiceDefinition.csdef**: specyficzne dla platformy Azure pliki niezbędne do publikowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0214b-133">**ServiceConfiguration.Cloud.cscfg**, **ServiceConfiguration.Local.cscfg** and **ServiceDefinition.csdef**: Azure-specific files necessary for publishing your application.</span></span> <span data-ttu-id="0214b-134">Aby uzyskać więcej informacji, zobacz [Tworzenie hostowanej usługi platformy Azure — omówienie].</span><span class="sxs-lookup"><span data-stu-id="0214b-134">For more information, see [Overview of Creating a Hosted Service for Azure].</span></span>
   * <span data-ttu-id="0214b-135">**deploymentSettings.json**: przechowuje ustawienia lokalne, które są używane przez hello polecenia cmdlet wdrażania programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0214b-135">**deploymentSettings.json**: Stores local settings that are used by hello Azure PowerShell deployment cmdlets.</span></span>
4. <span data-ttu-id="0214b-136">Wprowadź hello następujące polecenia tooadd nową rolę sieci web:</span><span class="sxs-lookup"><span data-stu-id="0214b-136">Enter hello following command tooadd a new web role:</span></span>

       Add-AzureNodeWebRole

   ![dane wyjściowe Hello hello polecenia Add-AzureNodeWebRole][hello output of hello Add-AzureNodeWebRole command]

   <span data-ttu-id="0214b-138">Witaj **Add-AzureNodeWebRole** polecenie cmdlet tworzy podstawowej aplikacji Node.js.</span><span class="sxs-lookup"><span data-stu-id="0214b-138">hello **Add-AzureNodeWebRole** cmdlet creates a basic Node.js application.</span></span> <span data-ttu-id="0214b-139">Także modyfikuje hello **.csfg** i **csdef** tooadd wpisów konfiguracji dla nowej roli hello pliki.</span><span class="sxs-lookup"><span data-stu-id="0214b-139">It also modifies hello **.csfg** and **.csdef** files tooadd configuration entries for hello new role.</span></span>

   > [!NOTE]
   > <span data-ttu-id="0214b-140">Jeśli nie określisz nazwy roli, będzie używana nazwa domyślna.</span><span class="sxs-lookup"><span data-stu-id="0214b-140">If you do not specify a role name, a default name is used.</span></span> <span data-ttu-id="0214b-141">Można podać nazwę jako pierwszym parametrem polecenia cmdlet hello:`Add-AzureNodeWebRole MyRole`</span><span class="sxs-lookup"><span data-stu-id="0214b-141">You can provide a name as hello first cmdlet parameter: `Add-AzureNodeWebRole MyRole`</span></span>

<span data-ttu-id="0214b-142">Aplikacja Node.js Hello jest zdefiniowana w pliku hello **server.js**, który znajduje się w katalogu hello hello roli sieci web (**WebRole1** domyślnie).</span><span class="sxs-lookup"><span data-stu-id="0214b-142">hello Node.js app is defined in hello file **server.js**, located in hello directory for hello web role (**WebRole1** by default).</span></span> <span data-ttu-id="0214b-143">Oto kod hello:</span><span class="sxs-lookup"><span data-stu-id="0214b-143">Here is hello code:</span></span>

    var http = require('http');
    var port = process.env.port || 1337;
    http.createServer(function (req, res) {
        res.writeHead(200, { 'Content-Type': 'text/plain' });
        res.end('Hello World\n');
    }).listen(port);

<span data-ttu-id="0214b-144">Ten kod jest zasadniczo hello tak samo jak Witaj "Hello World" przykładowe na powitania [nodejs.org] witryny sieci Web, z wyjątkiem używa hello numeru portu przypisanego przez hello środowiska chmury.</span><span class="sxs-lookup"><span data-stu-id="0214b-144">This code is essentially hello same as hello "Hello World" sample on hello [nodejs.org] website, except it uses hello port number assigned by hello cloud environment.</span></span>

## <a name="deploy-hello-application-tooazure"></a><span data-ttu-id="0214b-145">Wdrażanie tooAzure aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="0214b-145">Deploy hello application tooAzure</span></span>

> [!NOTE]
> <span data-ttu-id="0214b-146">toocomplete tego samouczka jest potrzebne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0214b-146">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="0214b-147">Możesz [aktywować korzyści dla subskrybentów MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A85619ABF) lub [zarejestrować się w celu uzyskania bezpłatnego konta](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).</span><span class="sxs-lookup"><span data-stu-id="0214b-147">You can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A85619ABF) or [sign up for a free account](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).</span></span>

### <a name="download-hello-azure-publishing-settings"></a><span data-ttu-id="0214b-148">Pobierz hello Azure ustawienia publikowania</span><span class="sxs-lookup"><span data-stu-id="0214b-148">Download hello Azure publishing settings</span></span>
<span data-ttu-id="0214b-149">toodeploy Twojego tooAzure aplikacji, należy najpierw pobrać hello publikowania ustawienia dla Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0214b-149">toodeploy your application tooAzure, you must first download hello publishing settings for your Azure subscription.</span></span>

1. <span data-ttu-id="0214b-150">Uruchom następujące polecenia cmdlet programu Azure PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="0214b-150">Run hello following Azure PowerShell cmdlet:</span></span>

       Get-AzurePublishSettingsFile

   <span data-ttu-id="0214b-151">Zostaną użyte przeglądarkę toonavigate toohello strona pobierania ustawień publikowania.</span><span class="sxs-lookup"><span data-stu-id="0214b-151">This will use your browser toonavigate toohello publish settings download page.</span></span> <span data-ttu-id="0214b-152">Może być zostanie wyświetlony monit o toolog za pomocą Account firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0214b-152">You may be prompted toolog in with a Microsoft Account.</span></span> <span data-ttu-id="0214b-153">Jeśli tak, użyj konta hello skojarzonego z subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0214b-153">If so, use hello account associated with your Azure subscription.</span></span>

   <span data-ttu-id="0214b-154">Hello pobrany profil tooa pliku lokalizacji, które łatwo uzyskiwać dostęp do zapisu.</span><span class="sxs-lookup"><span data-stu-id="0214b-154">Save hello downloaded profile tooa file location you can easily access.</span></span>
2. <span data-ttu-id="0214b-155">Uruchom następujące polecenia cmdlet tooimport hello pobrany profil publikowania:</span><span class="sxs-lookup"><span data-stu-id="0214b-155">Run following cmdlet tooimport hello publishing profile you downloaded:</span></span>

       Import-AzurePublishSettingsFile [path toofile]

    > [!NOTE]
    > <span data-ttu-id="0214b-156">Po zaimportowaniu hello ustawień publikowania, rozważ usunięcie hello pobrany plik .publishSettings, ponieważ zawiera on informacje, które mogłyby umożliwić innym osobom tooaccess Twojego konta.</span><span class="sxs-lookup"><span data-stu-id="0214b-156">After importing hello publish settings, consider deleting hello downloaded .publishSettings file, because it contains information that could allow someone tooaccess your account.</span></span>

### <a name="publish-hello-application"></a><span data-ttu-id="0214b-157">Publikowanie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="0214b-157">Publish hello application</span></span>
<span data-ttu-id="0214b-158">toopublish, uruchom następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="0214b-158">toopublish, run hello following commands:</span></span>

      $ServiceName = "NodeHelloWorld" + $(Get-Date -Format ('ddhhmm'))
    Publish-AzureServiceProject -ServiceName $ServiceName  -Location "East US" -Launch

* <span data-ttu-id="0214b-159">**-ServiceName** Określa nazwę hello hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="0214b-159">**-ServiceName** specifies hello name for hello deployment.</span></span> <span data-ttu-id="0214b-160">To musi być unikatowa nazwa, w przeciwnym razie hello publikowanie proces zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="0214b-160">This must be a unique name, otherwise hello publish process will fail.</span></span> <span data-ttu-id="0214b-161">Witaj **Get-Date** polecenia uwzględnia ciąg daty/godziny, który powinien zapewnić, że nazwa hello unikatowy.</span><span class="sxs-lookup"><span data-stu-id="0214b-161">hello **Get-Date** command tacks on a date/time string that should make hello name unique.</span></span>
* <span data-ttu-id="0214b-162">**-Lokalizacji** określa hello centrum danych, którego aplikacja hello będzie obsługiwana w systemie.</span><span class="sxs-lookup"><span data-stu-id="0214b-162">**-Location** specifies hello datacenter that hello application will be hosted in.</span></span> <span data-ttu-id="0214b-163">listę dostępnych centrów danych, użyj hello toosee **Get-AzureLocation** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0214b-163">toosee a list of available datacenters, use hello **Get-AzureLocation** cmdlet.</span></span>
* <span data-ttu-id="0214b-164">**-Launch** otwiera okno przeglądarki i przechodzi toohello hostowane usługi, po zakończeniu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="0214b-164">**-Launch** opens a browser window and navigates toohello hosted service after deployment has completed.</span></span>

<span data-ttu-id="0214b-165">Po publikowanie powiedzie się, zostanie wyświetlony poniżej toohello podobne odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="0214b-165">After publishing succeeds, you will see a response similar toohello following:</span></span>

![dane wyjściowe Hello hello polecenia Publish-AzureService][hello output of hello Publish-AzureService command]

> [!NOTE]
> <span data-ttu-id="0214b-167">Ona potrwać kilka minut toodeploy aplikacji hello i stają się dostępne po pierwszej publikacji.</span><span class="sxs-lookup"><span data-stu-id="0214b-167">It can take several minutes for hello application toodeploy and become available when first published.</span></span>

<span data-ttu-id="0214b-168">Po zakończeniu wdrażania hello oknie przeglądarki zostanie Otwórz i przejdź toohello usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="0214b-168">Once hello deployment has completed, a browser window will open and navigate toohello cloud service.</span></span>

![Okno przeglądarki zawierające hello hello world strony; adres URL Hello wskazuje, że strona hello jest obsługiwana na platformie Azure.][A browser window displaying hello hello world page; hello URL indicates hello page is hosted on Azure.]

<span data-ttu-id="0214b-170">Aplikacja działa teraz na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="0214b-170">Your application is now running on Azure.</span></span>

<span data-ttu-id="0214b-171">Witaj **Publish-AzureServiceProject** polecenia cmdlet wykonuje hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="0214b-171">hello **Publish-AzureServiceProject** cmdlet performs hello following steps:</span></span>

1. <span data-ttu-id="0214b-172">Tworzy toodeploy pakietu.</span><span class="sxs-lookup"><span data-stu-id="0214b-172">Creates a package toodeploy.</span></span> <span data-ttu-id="0214b-173">Pakiet HELLO zawiera wszystkie pliki hello w folderze aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0214b-173">hello package contains all hello files in your application folder.</span></span>
2. <span data-ttu-id="0214b-174">Tworzy nowe **konto magazynu**, jeśli takie konto jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="0214b-174">Creates a new **storage account** if one does not exist.</span></span> <span data-ttu-id="0214b-175">Witaj kontem magazynu platformy Azure jest pakiet aplikacji hello toostore używane podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="0214b-175">hello Azure storage account is used toostore hello application package during deployment.</span></span> <span data-ttu-id="0214b-176">Można bezpiecznie usunąć konto magazynu powitania po ukończeniu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="0214b-176">You can safely delete hello storage account after deployment is done.</span></span>
3. <span data-ttu-id="0214b-177">Tworzy nową **usługę w chmurze**, jeśli taka usługa jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="0214b-177">Creates a new **cloud service** if one does not already exist.</span></span> <span data-ttu-id="0214b-178">A **usługi w chmurze** jest kontenerem hello, w którym aplikacja jest hostowana po tooAzure wdrożone.</span><span class="sxs-lookup"><span data-stu-id="0214b-178">A **cloud service** is hello container in which your application is hosted when it is deployed tooAzure.</span></span> <span data-ttu-id="0214b-179">Aby uzyskać więcej informacji, zobacz [Tworzenie hostowanej usługi platformy Azure — omówienie].</span><span class="sxs-lookup"><span data-stu-id="0214b-179">For more information, see [Overview of Creating a Hosted Service for Azure].</span></span>
4. <span data-ttu-id="0214b-180">Publikuje hello wdrożenia pakietu tooAzure.</span><span class="sxs-lookup"><span data-stu-id="0214b-180">Publishes hello deployment package tooAzure.</span></span>

## <a name="stopping-and-deleting-your-application"></a><span data-ttu-id="0214b-181">Zatrzymywanie i usuwanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="0214b-181">Stopping and deleting your application</span></span>
<span data-ttu-id="0214b-182">Po wdrożeniu aplikacji, może być toodisable go, aby uniknąć dodatkowych kosztów.</span><span class="sxs-lookup"><span data-stu-id="0214b-182">After deploying your application, you may want toodisable it so you can avoid extra costs.</span></span> <span data-ttu-id="0214b-183">Opłaty za wystąpienia ról sieci Web na platformie Azure są naliczane za godzinę korzystania z serwera.</span><span class="sxs-lookup"><span data-stu-id="0214b-183">Azure bills web role instances per hour of server time consumed.</span></span> <span data-ttu-id="0214b-184">Czas serwera jest używany, gdy aplikacja jest wdrażana, nawet jeśli hello wystąpień nie są uruchomione i są w stanie hello zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="0214b-184">Server time is consumed once your application is deployed, even if hello instances are not running and are in hello stopped state.</span></span>

1. <span data-ttu-id="0214b-185">W oknie programu PowerShell Windows hello Zatrzymaj wdrożenie usługi hello utworzony w poprzedniej sekcji hello z hello następującego polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="0214b-185">In hello Windows PowerShell window, stop hello service deployment created in hello previous section with hello following cmdlet:</span></span>

       Stop-AzureService

   <span data-ttu-id="0214b-186">Zatrzymywanie usługi hello może potrwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="0214b-186">Stopping hello service may take several minutes.</span></span> <span data-ttu-id="0214b-187">Witaj, usługa zostanie zatrzymana, pojawi się komunikat wskazujący, że usługa została zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="0214b-187">When hello service is stopped, you receive a message indicating that it has stopped.</span></span>

   ![Stan Hello polecenia hello Stop-AzureService][hello status of hello Stop-AzureService command]
2. <span data-ttu-id="0214b-189">Usługa hello toodelete, wywołanie hello następującego polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="0214b-189">toodelete hello service, call hello following cmdlet:</span></span>

       Remove-AzureService

   <span data-ttu-id="0214b-190">Po wyświetleniu monitu wprowadź **Y** toodelete hello usługi.</span><span class="sxs-lookup"><span data-stu-id="0214b-190">When prompted, enter **Y** toodelete hello service.</span></span>

   <span data-ttu-id="0214b-191">Usuwanie hello usługi może potrwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="0214b-191">Deleting hello service may take several minutes.</span></span> <span data-ttu-id="0214b-192">Po usunięciu hello usługi pojawi się komunikat wskazujący, że usługa hello została usunięta.</span><span class="sxs-lookup"><span data-stu-id="0214b-192">After hello service has been deleted you receive a message indicating that hello service was deleted.</span></span>

   ![Stan Hello polecenia hello Remove-AzureService][hello status of hello Remove-AzureService command]

   > [!NOTE]
   > <span data-ttu-id="0214b-194">Usunięcie usługi hello nie powoduje usunięcia konta magazynu hello, które zostało utworzone po początkowym opublikowaniu usługi hello i będzie toobe rozliczane użycie magazynu.</span><span class="sxs-lookup"><span data-stu-id="0214b-194">Deleting hello service does not delete hello storage account that was created when hello service was initially published, and you will continue toobe billed for storage used.</span></span> <span data-ttu-id="0214b-195">Jeśli nic nie używa hello magazynu, może być toodelete go.</span><span class="sxs-lookup"><span data-stu-id="0214b-195">If nothing else is using hello storage, you may want toodelete it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0214b-196">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0214b-196">Next steps</span></span>
<span data-ttu-id="0214b-197">Aby uzyskać więcej informacji, zobacz hello [Centrum deweloperów środowiska Node.js].</span><span class="sxs-lookup"><span data-stu-id="0214b-197">For more information, see hello [Node.js Developer Center].</span></span>

<!-- URL List -->

[porównanie witryn sieci Web platformy Azure, usługi w chmurze i maszyn wirtualnych]: ../app-service-web/choose-web-site-cloud-service-vm.md
[korzystanie z lekkiej aplikacji sieci web]: ../app-service-web/app-service-web-get-started-nodejs.md
[Azure PowerShell]: /powershell/azureps-cmdlets-docs
[zestaw Azure SDK for .NET 2.7]: http://www.microsoft.com/en-us/download/details.aspx?id=48178
[Connect PowerShell]: /powershell/azureps-cmdlets-docs#step-3-connect
[nodejs.org]: http://nodejs.org/
[Tworzenie hostowanej usługi platformy Azure — omówienie]: https://azure.microsoft.com/documentation/services/cloud-services/
[Centrum deweloperów środowiska Node.js]: https://azure.microsoft.com/develop/nodejs/

<!-- IMG List -->

[hello result of hello New-AzureService helloworld command]: ./media/cloud-services-nodejs-develop-deploy-app/node9.png
[hello output of hello Add-AzureNodeWebRole command]: ./media/cloud-services-nodejs-develop-deploy-app/node11.png
[A web browser displaying hello Hello World web page]: ./media/cloud-services-nodejs-develop-deploy-app/node14.png
[hello output of hello Publish-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node19.png
[A browser window displaying hello hello world page; hello URL indicates hello page is hosted on Azure.]: ./media/cloud-services-nodejs-develop-deploy-app/node21.png
[hello status of hello Stop-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node48.png
[hello status of hello Remove-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node49.png
