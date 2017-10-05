---
title: "Wprowadzenie do języka Node.js — przewodnik | Microsoft Docs"
description: "Dowiedz się, jak utworzyć prostą aplikację sieci Web Node.js, a następnie wdrożyć ją do usługi w chmurze Azure."
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
ms.openlocfilehash: 980643f35c78bbae7b1b12336331ca15ad4fb89b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="build-and-deploy-a-nodejs-application-to-an-azure-cloud-service"></a><span data-ttu-id="eb7d0-103">Tworzenie i wdrażanie aplikacji Node.js do usługi w chmurze Azure</span><span class="sxs-lookup"><span data-stu-id="eb7d0-103">Build and deploy a Node.js application to an Azure Cloud Service</span></span>

<span data-ttu-id="eb7d0-104">Ten samouczek pokazuje, jak utworzyć prostą aplikację Node.js działającą w usłudze w chmurze Azure.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-104">This tutorial shows how to create a simple Node.js application running in an Azure Cloud Service.</span></span> <span data-ttu-id="eb7d0-105">Usługi Cloud Services są blokami konstrukcyjnymi skalowalnych aplikacji w chmurze na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-105">Cloud Services are the building blocks of scalable cloud applications in Azure.</span></span> <span data-ttu-id="eb7d0-106">Umożliwiają one rozdzielanie i skalowanie w poziomie składników frontonu i zaplecza aplikacji oraz niezależne zarządzanie nimi.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-106">They allow the separation and independent management and scale-out of front-end and back-end components of your application.</span></span>  <span data-ttu-id="eb7d0-107">Usługi Cloud Services oferują specjalną maszynę wirtualną, która w niezawodny sposób hostuje poszczególne role.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-107">Cloud Services provide a robust dedicated virtual machine for hosting each role reliably.</span></span>

<span data-ttu-id="eb7d0-108">Dalsze informacje na temat usług Cloud Services oraz ich porównanie z usługami Witryny sieci Web i Maszyny wirtualne Azure można znaleźć w temacie [Porównanie usług Azure: Witryny sieci Web, Cloud Services i Virtual Machines].</span><span class="sxs-lookup"><span data-stu-id="eb7d0-108">For more information on Cloud Services, and how they compare to Azure Websites and Virtual machines, see [Azure Websites, Cloud Services and Virtual Machines comparison].</span></span>

> [!TIP]
> <span data-ttu-id="eb7d0-109">Chcesz utworzyć prostą witrynę sieci Web?</span><span class="sxs-lookup"><span data-stu-id="eb7d0-109">Looking to build a simple website?</span></span> <span data-ttu-id="eb7d0-110">Jeśli scenariusz obejmuje tylko prosty fronton witryny sieci Web, rozważ użycie [korzystanie z lekkiej aplikacji sieci web].</span><span class="sxs-lookup"><span data-stu-id="eb7d0-110">If your scenario involves just a simple website front-end, consider [using a lightweight web app].</span></span> <span data-ttu-id="eb7d0-111">Możesz łatwo przeprowadzić uaktualnienie do Usługi w chmurze w przypadku rozwoju witryny sieci Web lub zmiany wymagań.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-111">You can easily upgrade to a Cloud Service as your web app grows and your requirements change.</span></span>

<span data-ttu-id="eb7d0-112">Wykonując czynności opisane w tym samouczku, utworzysz prostą aplikację sieci Web hostowaną wewnątrz roli sieci Web.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-112">By following this tutorial, you will build a simple web application hosted inside a web role.</span></span> <span data-ttu-id="eb7d0-113">Będziesz testować aplikację w środowisku lokalnym przy użyciu emulatora obliczeń, a następnie wdrażać ją za pomocą narzędzi wiersza polecenia programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-113">You will use the compute emulator to test your application locally, then deploy it using PowerShell command-line tools.</span></span>

<span data-ttu-id="eb7d0-114">Będzie to prosta aplikacja „hello world”:</span><span class="sxs-lookup"><span data-stu-id="eb7d0-114">The application is a simple "hello world" application:</span></span>

![Przeglądarka wyświetlająca stronę sieci Web „Hello World”][A web browser displaying the Hello World web page]

## <a name="prerequisites"></a><span data-ttu-id="eb7d0-116">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="eb7d0-116">Prerequisites</span></span>
> [!NOTE]
> <span data-ttu-id="eb7d0-117">W tym samouczku jest używany program Azure PowerShell, który wymaga systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-117">This tutorial uses Azure PowerShell, which requires Windows.</span></span>

* <span data-ttu-id="eb7d0-118">Zainstalowanie i skonfigurowanie programu [Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="eb7d0-118">Install and configure [Azure Powershell].</span></span>
* <span data-ttu-id="eb7d0-119">Pobranie i zainstalowanie zestawu [Azure SDK for .NET 2.7].</span><span class="sxs-lookup"><span data-stu-id="eb7d0-119">Download and install the [Azure SDK for .NET 2.7].</span></span> <span data-ttu-id="eb7d0-120">Podczas instalacji wybierz następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="eb7d0-120">In the install setup, select:</span></span>
  * <span data-ttu-id="eb7d0-121">MicrosoftAzureAuthoringTools</span><span class="sxs-lookup"><span data-stu-id="eb7d0-121">MicrosoftAzureAuthoringTools</span></span>
  * <span data-ttu-id="eb7d0-122">MicrosoftAzureComputeEmulator</span><span class="sxs-lookup"><span data-stu-id="eb7d0-122">MicrosoftAzureComputeEmulator</span></span>

## <a name="create-an-azure-cloud-service-project"></a><span data-ttu-id="eb7d0-123">Tworzenie projektu Usługi w chmurze Azure</span><span class="sxs-lookup"><span data-stu-id="eb7d0-123">Create an Azure Cloud Service project</span></span>
<span data-ttu-id="eb7d0-124">Wykonaj poniższe zadania w celu utworzenia nowego projektu Usługi w chmurze Azure oraz utworzenia podstawowych szkieletów języka Node.js:</span><span class="sxs-lookup"><span data-stu-id="eb7d0-124">Perform the following tasks to create a new Azure Cloud Service project, along with basic Node.js scaffolding:</span></span>

1. <span data-ttu-id="eb7d0-125">Uruchom program **Windows PowerShell** jako administrator. Przy użyciu **menu Start** lub **ekranu startowego** wyszukaj program **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-125">Run **Windows PowerShell** as Administrator; from the **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span>
2. <span data-ttu-id="eb7d0-126">[Connect PowerShell] z subskrypcją.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-126">[Connect PowerShell] to your subscription.</span></span>
3. <span data-ttu-id="eb7d0-127">Wprowadź następujące polecenie cmdlet programu PowerShell, aby utworzyć projekt:</span><span class="sxs-lookup"><span data-stu-id="eb7d0-127">Enter the following PowerShell cmdlet to create to create the project:</span></span>

        New-AzureServiceProject helloworld

    ![Wynik użycia polecenia New-AzureService helloworld][The result of the New-AzureService helloworld command]

    <span data-ttu-id="eb7d0-129">Polecenie cmdlet **New-AzureServiceProject** powoduje wygenerowanie podstawowej struktury publikowania aplikacji Node.js w Usłudze w chmurze.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-129">The **New-AzureServiceProject** cmdlet generates a basic structure for publishing a Node.js application to a Cloud Service.</span></span> <span data-ttu-id="eb7d0-130">Zawiera ona pliki konfiguracji niezbędne do publikowania na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-130">It contains configuration files necessary for publishing to Azure.</span></span> <span data-ttu-id="eb7d0-131">Polecenie cmdlet zmienia także katalog roboczy na katalog usługi.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-131">The cmdlet also changes your working directory to the directory for the service.</span></span>

    <span data-ttu-id="eb7d0-132">Polecenie cmdlet powoduje utworzenie następujących plików:</span><span class="sxs-lookup"><span data-stu-id="eb7d0-132">The cmdlet creates the following files:</span></span>

   * <span data-ttu-id="eb7d0-133">**ServiceConfiguration.Cloud.cscfg**, **ServiceConfiguration.Local.cscfg** i **ServiceDefinition.csdef**: specyficzne dla platformy Azure pliki niezbędne do publikowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-133">**ServiceConfiguration.Cloud.cscfg**, **ServiceConfiguration.Local.cscfg** and **ServiceDefinition.csdef**: Azure-specific files necessary for publishing your application.</span></span> <span data-ttu-id="eb7d0-134">Aby uzyskać więcej informacji, zobacz [Tworzenie hostowanej usługi platformy Azure — omówienie].</span><span class="sxs-lookup"><span data-stu-id="eb7d0-134">For more information, see [Overview of Creating a Hosted Service for Azure].</span></span>
   * <span data-ttu-id="eb7d0-135">**deploymentSettings.json**: przechowuje ustawienia lokalne, które są używane przez polecenia cmdlet programu Azure PowerShell dotyczące wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-135">**deploymentSettings.json**: Stores local settings that are used by the Azure PowerShell deployment cmdlets.</span></span>
4. <span data-ttu-id="eb7d0-136">Wprowadź poniższe polecenie, aby dodać nową rolę sieci Web:</span><span class="sxs-lookup"><span data-stu-id="eb7d0-136">Enter the following command to add a new web role:</span></span>

       Add-AzureNodeWebRole

   ![Dane wyjściowe polecenia Add-AzureNodeWebRole][The output of the Add-AzureNodeWebRole command]

   <span data-ttu-id="eb7d0-138">Polecenie cmdlet **Add-AzureNodeWebRole** służy do tworzenia podstawowej aplikacji Node.js.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-138">The **Add-AzureNodeWebRole** cmdlet creates a basic Node.js application.</span></span> <span data-ttu-id="eb7d0-139">Powoduje ono również modyfikowanie plików **.csfg** i **.csdef** w celu dodania wpisów konfiguracji dla nowej roli.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-139">It also modifies the **.csfg** and **.csdef** files to add configuration entries for the new role.</span></span>

   > [!NOTE]
   > <span data-ttu-id="eb7d0-140">Jeśli nie określisz nazwy roli, będzie używana nazwa domyślna.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-140">If you do not specify a role name, a default name is used.</span></span> <span data-ttu-id="eb7d0-141">Nazwa może być pierwszym parametrem polecenia cmdlet: `Add-AzureNodeWebRole MyRole`</span><span class="sxs-lookup"><span data-stu-id="eb7d0-141">You can provide a name as the first cmdlet parameter: `Add-AzureNodeWebRole MyRole`</span></span>

<span data-ttu-id="eb7d0-142">Aplikacja Node.js jest definiowana w pliku **server.js**, który znajduje się w katalogu dla roli sieci Web (domyślnie **WebRole1**).</span><span class="sxs-lookup"><span data-stu-id="eb7d0-142">The Node.js app is defined in the file **server.js**, located in the directory for the web role (**WebRole1** by default).</span></span> <span data-ttu-id="eb7d0-143">Oto kod:</span><span class="sxs-lookup"><span data-stu-id="eb7d0-143">Here is the code:</span></span>

    var http = require('http');
    var port = process.env.port || 1337;
    http.createServer(function (req, res) {
        res.writeHead(200, { 'Content-Type': 'text/plain' });
        res.end('Hello World\n');
    }).listen(port);

<span data-ttu-id="eb7d0-144">Ten kod jest zasadniczo taki sam jak przykładowy kod „Hello World” w witrynie sieci Web [nodejs.org], z wyjątkiem tego, że używa numeru portu przypisanego przez środowisko chmury.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-144">This code is essentially the same as the "Hello World" sample on the [nodejs.org] website, except it uses the port number assigned by the cloud environment.</span></span>

## <a name="deploy-the-application-to-azure"></a><span data-ttu-id="eb7d0-145">Wdrażanie aplikacji na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="eb7d0-145">Deploy the application to Azure</span></span>

> [!NOTE]
> <span data-ttu-id="eb7d0-146">Do ukończenia tego samouczka jest potrzebne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-146">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="eb7d0-147">Możesz [aktywować korzyści dla subskrybentów MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A85619ABF) lub [zarejestrować się w celu uzyskania bezpłatnego konta](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).</span><span class="sxs-lookup"><span data-stu-id="eb7d0-147">You can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A85619ABF) or [sign up for a free account](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).</span></span>

### <a name="download-the-azure-publishing-settings"></a><span data-ttu-id="eb7d0-148">Pobieranie ustawień publikowania na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="eb7d0-148">Download the Azure publishing settings</span></span>
<span data-ttu-id="eb7d0-149">Aby wdrożyć aplikację na platformie Azure, należy najpierw pobrać ustawienia publikowania dla subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-149">To deploy your application to Azure, you must first download the publishing settings for your Azure subscription.</span></span>

1. <span data-ttu-id="eb7d0-150">Uruchom poniższe polecenie cmdlet programu Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="eb7d0-150">Run the following Azure PowerShell cmdlet:</span></span>

       Get-AzurePublishSettingsFile

   <span data-ttu-id="eb7d0-151">Spowoduje to przejście do strony pobierania ustawień publikowania w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-151">This will use your browser to navigate to the publish settings download page.</span></span> <span data-ttu-id="eb7d0-152">Może pojawić się monit o zalogowanie się przy użyciu konta Microsoft.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-152">You may be prompted to log in with a Microsoft Account.</span></span> <span data-ttu-id="eb7d0-153">W takiej sytuacji należy użyć konta skojarzonego z subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-153">If so, use the account associated with your Azure subscription.</span></span>

   <span data-ttu-id="eb7d0-154">Zapisz pobrany profil w łatwo dostępnej lokalizacji pliku.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-154">Save the downloaded profile to a file location you can easily access.</span></span>
2. <span data-ttu-id="eb7d0-155">Uruchom poniższe polecenie cmdlet, aby zaimportować pobrany profil publikowania:</span><span class="sxs-lookup"><span data-stu-id="eb7d0-155">Run following cmdlet to import the publishing profile you downloaded:</span></span>

       Import-AzurePublishSettingsFile [path to file]

    > [!NOTE]
    > <span data-ttu-id="eb7d0-156">Po zaimportowaniu ustawień publikowania rozważ usunięcie pobranego pliku .publishSettings, ponieważ zawiera on informacje, które mogłyby umożliwić innym osobom uzyskanie dostępu do Twojego konta.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-156">After importing the publish settings, consider deleting the downloaded .publishSettings file, because it contains information that could allow someone to access your account.</span></span>

### <a name="publish-the-application"></a><span data-ttu-id="eb7d0-157">Publikowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="eb7d0-157">Publish the application</span></span>
<span data-ttu-id="eb7d0-158">Aby opublikować aplikację, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="eb7d0-158">To publish, run the following commands:</span></span>

      $ServiceName = "NodeHelloWorld" + $(Get-Date -Format ('ddhhmm'))
    Publish-AzureServiceProject -ServiceName $ServiceName  -Location "East US" -Launch

* <span data-ttu-id="eb7d0-159">**-ServiceName** — określa nazwę wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-159">**-ServiceName** specifies the name for the deployment.</span></span> <span data-ttu-id="eb7d0-160">Musi być to nazwa unikatowa. W przeciwnym razie proces publikowania zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-160">This must be a unique name, otherwise the publish process will fail.</span></span> <span data-ttu-id="eb7d0-161">Polecenie **Get-Date** uwzględnia ciąg daty i godziny, który powinien zapewnić unikatowość nazwy.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-161">The **Get-Date** command tacks on a date/time string that should make the name unique.</span></span>
* <span data-ttu-id="eb7d0-162">**-Location** — określa centrum danych, w którym aplikacja będzie hostowana.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-162">**-Location** specifies the datacenter that the application will be hosted in.</span></span> <span data-ttu-id="eb7d0-163">Aby wyświetlić listę dostępnych centrów danych, użyj polecenia cmdlet **Get-AzureLocation**.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-163">To see a list of available datacenters, use the **Get-AzureLocation** cmdlet.</span></span>
* <span data-ttu-id="eb7d0-164">**-Launch** — otwiera okno przeglądarki i przechodzi do usługi hostowanej po zakończeniu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-164">**-Launch** opens a browser window and navigates to the hosted service after deployment has completed.</span></span>

<span data-ttu-id="eb7d0-165">Po pomyślnym zakończeniu publikowania zostanie wyświetlona odpowiedź podobna do następującej:</span><span class="sxs-lookup"><span data-stu-id="eb7d0-165">After publishing succeeds, you will see a response similar to the following:</span></span>

![Dane wyjściowe polecenia Publish-AzureService][The output of the Publish-AzureService command]

> [!NOTE]
> <span data-ttu-id="eb7d0-167">W przypadku publikowania aplikacji po raz pierwszy jej wdrożenie i udostępnienie może potrwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-167">It can take several minutes for the application to deploy and become available when first published.</span></span>

<span data-ttu-id="eb7d0-168">Po zakończeniu wdrożenia zostanie otwarte okno przeglądarki i nastąpi przejście do usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-168">Once the deployment has completed, a browser window will open and navigate to the cloud service.</span></span>

![Okno przeglądarki ze stroną „hello world”; adres URL wskazuje, że strona jest obsługiwana na platformie Azure.][A browser window displaying the hello world page; the URL indicates the page is hosted on Azure.]

<span data-ttu-id="eb7d0-170">Aplikacja działa teraz na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-170">Your application is now running on Azure.</span></span>

<span data-ttu-id="eb7d0-171">Polecenie cmdlet **Publish-AzureServiceProject** wykonuje następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="eb7d0-171">The **Publish-AzureServiceProject** cmdlet performs the following steps:</span></span>

1. <span data-ttu-id="eb7d0-172">Tworzy pakiet do wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-172">Creates a package to deploy.</span></span> <span data-ttu-id="eb7d0-173">Pakiet zawiera wszystkie pliki w folderze aplikacji.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-173">The package contains all the files in your application folder.</span></span>
2. <span data-ttu-id="eb7d0-174">Tworzy nowe **konto magazynu**, jeśli takie konto jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-174">Creates a new **storage account** if one does not exist.</span></span> <span data-ttu-id="eb7d0-175">Konto magazynu Azure jest używane do przechowywania pakietu aplikacji podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-175">The Azure storage account is used to store the application package during deployment.</span></span> <span data-ttu-id="eb7d0-176">Po ukończeniu wdrażania konto magazynu można bezpiecznie usunąć.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-176">You can safely delete the storage account after deployment is done.</span></span>
3. <span data-ttu-id="eb7d0-177">Tworzy nową **usługę w chmurze**, jeśli taka usługa jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-177">Creates a new **cloud service** if one does not already exist.</span></span> <span data-ttu-id="eb7d0-178">**Usługa w chmurze** to kontener, w którym aplikacja jest hostowana po wdrożeniu na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-178">A **cloud service** is the container in which your application is hosted when it is deployed to Azure.</span></span> <span data-ttu-id="eb7d0-179">Aby uzyskać więcej informacji, zobacz [Tworzenie hostowanej usługi platformy Azure — omówienie].</span><span class="sxs-lookup"><span data-stu-id="eb7d0-179">For more information, see [Overview of Creating a Hosted Service for Azure].</span></span>
4. <span data-ttu-id="eb7d0-180">Publikuje pakiet wdrożeniowy na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-180">Publishes the deployment package to Azure.</span></span>

## <a name="stopping-and-deleting-your-application"></a><span data-ttu-id="eb7d0-181">Zatrzymywanie i usuwanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="eb7d0-181">Stopping and deleting your application</span></span>
<span data-ttu-id="eb7d0-182">Po wdrożeniu aplikacji można ją wyłączyć, aby uniknąć dodatkowych kosztów.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-182">After deploying your application, you may want to disable it so you can avoid extra costs.</span></span> <span data-ttu-id="eb7d0-183">Opłaty za wystąpienia ról sieci Web na platformie Azure są naliczane za godzinę korzystania z serwera.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-183">Azure bills web role instances per hour of server time consumed.</span></span> <span data-ttu-id="eb7d0-184">Czas serwera jest używany po wdrożeniu aplikacji, nawet jeśli wystąpienia nie zostały uruchomione i są w stanie zatrzymania.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-184">Server time is consumed once your application is deployed, even if the instances are not running and are in the stopped state.</span></span>

1. <span data-ttu-id="eb7d0-185">W oknie programu Windows PowerShell zatrzymaj wdrożenie usługi utworzone w poprzedniej sekcji za pomocą następującego polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="eb7d0-185">In the Windows PowerShell window, stop the service deployment created in the previous section with the following cmdlet:</span></span>

       Stop-AzureService

   <span data-ttu-id="eb7d0-186">Zatrzymywanie usługi może potrwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-186">Stopping the service may take several minutes.</span></span> <span data-ttu-id="eb7d0-187">Po zatrzymaniu usługi pojawi się komunikat wskazujący, że usługa została zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-187">When the service is stopped, you receive a message indicating that it has stopped.</span></span>

   ![Stan polecenia Stop-AzureService][The status of the Stop-AzureService command]
2. <span data-ttu-id="eb7d0-189">Aby usunąć usługę, wywołaj następujące polecenie cmdlet:</span><span class="sxs-lookup"><span data-stu-id="eb7d0-189">To delete the service, call the following cmdlet:</span></span>

       Remove-AzureService

   <span data-ttu-id="eb7d0-190">Po wyświetleniu monitu wpisz **Y**, aby usunąć usługę.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-190">When prompted, enter **Y** to delete the service.</span></span>

   <span data-ttu-id="eb7d0-191">Usuwanie usługi może potrwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-191">Deleting the service may take several minutes.</span></span> <span data-ttu-id="eb7d0-192">Po usunięciu usługi pojawi się komunikat z informacją, że usługa została usunięta.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-192">After the service has been deleted you receive a message indicating that the service was deleted.</span></span>

   ![Stan polecenia Remove-AzureService][The status of the Remove-AzureService command]

   > [!NOTE]
   > <span data-ttu-id="eb7d0-194">Usunięcie usługi nie powoduje usunięcia konta magazynu, które zostało utworzone po początkowym opublikowaniu usługi, a opłaty za użycie magazynu będą nadal naliczane.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-194">Deleting the service does not delete the storage account that was created when the service was initially published, and you will continue to be billed for storage used.</span></span> <span data-ttu-id="eb7d0-195">Jeśli nic innego nie korzysta z magazynu, możesz go usunąć.</span><span class="sxs-lookup"><span data-stu-id="eb7d0-195">If nothing else is using the storage, you may want to delete it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eb7d0-196">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="eb7d0-196">Next steps</span></span>
<span data-ttu-id="eb7d0-197">Aby uzyskać więcej informacji, odwiedź stronę [Centrum deweloperów środowiska Node.js].</span><span class="sxs-lookup"><span data-stu-id="eb7d0-197">For more information, see the [Node.js Developer Center].</span></span>

<!-- URL List -->

<span data-ttu-id="eb7d0-198">[Porównanie usług Azure: Witryny sieci Web, Cloud Services i Virtual Machines]: ../app-service-web/choose-web-site-cloud-service-vm.md</span><span class="sxs-lookup"><span data-stu-id="eb7d0-198">[Azure Websites, Cloud Services and Virtual Machines comparison]: ../app-service-web/choose-web-site-cloud-service-vm.md</span></span>
<span data-ttu-id="eb7d0-199">[korzystanie z lekkiej aplikacji sieci web]: ../app-service-web/app-service-web-get-started-nodejs.md</span><span class="sxs-lookup"><span data-stu-id="eb7d0-199">[using a lightweight web app]: ../app-service-web/app-service-web-get-started-nodejs.md</span></span>
<span data-ttu-id="eb7d0-200">[Azure PowerShell]: /powershell/azureps-cmdlets-docs</span><span class="sxs-lookup"><span data-stu-id="eb7d0-200">[Azure Powershell]: /powershell/azureps-cmdlets-docs</span></span>
<span data-ttu-id="eb7d0-201">[Azure SDK for .NET 2.7]: http://www.microsoft.com/en-us/download/details.aspx?id=48178</span><span class="sxs-lookup"><span data-stu-id="eb7d0-201">[Azure SDK for .NET 2.7]: http://www.microsoft.com/en-us/download/details.aspx?id=48178</span></span>
<span data-ttu-id="eb7d0-202">[Connect PowerShell]: /powershell/azureps-cmdlets-docs#step-3-connect</span><span class="sxs-lookup"><span data-stu-id="eb7d0-202">[Connect PowerShell]: /powershell/azureps-cmdlets-docs#step-3-connect</span></span>
<span data-ttu-id="eb7d0-203">[nodejs.org]: http://nodejs.org/</span><span class="sxs-lookup"><span data-stu-id="eb7d0-203">[nodejs.org]: http://nodejs.org/</span></span>
<span data-ttu-id="eb7d0-204">[Tworzenie hostowanej usługi platformy Azure — omówienie]: https://azure.microsoft.com/documentation/services/cloud-services/</span><span class="sxs-lookup"><span data-stu-id="eb7d0-204">[Overview of Creating a Hosted Service for Azure]: https://azure.microsoft.com/documentation/services/cloud-services/</span></span>
<span data-ttu-id="eb7d0-205">[Centrum deweloperów środowiska Node.js]: https://azure.microsoft.com/develop/nodejs/</span><span class="sxs-lookup"><span data-stu-id="eb7d0-205">[Node.js Developer Center]: https://azure.microsoft.com/develop/nodejs/</span></span>

<!-- IMG List -->

[The result of the New-AzureService helloworld command]: ./media/cloud-services-nodejs-develop-deploy-app/node9.png
[The output of the Add-AzureNodeWebRole command]: ./media/cloud-services-nodejs-develop-deploy-app/node11.png
[A web browser displaying the Hello World web page]: ./media/cloud-services-nodejs-develop-deploy-app/node14.png
[The output of the Publish-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node19.png
[A browser window displaying the hello world page; the URL indicates the page is hosted on Azure.]: ./media/cloud-services-nodejs-develop-deploy-app/node21.png
[The status of the Stop-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node48.png
[The status of the Remove-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node49.png
