---
title: "aaaUsing tooDev tooPublish skryptów programu Windows PowerShell i środowisk testowych | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skrypty toouse środowiska Windows PowerShell z programu Visual Studio toopublish środowiska toodevelopment i testowania."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5fff1301-5469-4d97-be88-c85c30f837c1
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 491a058f96255576afa74f6156f20ae9559bb9f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-windows-powershell-scripts-toopublish-toodev-and-test-environments"></a><span data-ttu-id="1170c-103">Przy użyciu programu Windows PowerShell skrypty środowiska toopublish toodev i testowania</span><span class="sxs-lookup"><span data-stu-id="1170c-103">Using Windows PowerShell scripts toopublish toodev and test environments</span></span>
<span data-ttu-id="1170c-104">Podczas tworzenia aplikacji sieci web w programie Visual Studio, można wygenerować skrypt programu Windows PowerShell, na której można nowsze publikowanie hello tooautomate Twojego tooAzure witryny sieci Web jako aplikacji sieci Web w usłudze Azure App Service lub maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1170c-104">When you create a web application in Visual Studio, you can generate a Windows PowerShell script that you can use later tooautomate hello publishing of your website tooAzure as a Web App in Azure App Service or a virtual machine.</span></span> <span data-ttu-id="1170c-105">Można edytować i rozszerzyć hello skrypt programu Windows PowerShell w toosuit edytora programu Visual Studio hello wymagań lub zintegrować hello skryptu z istniejących kompilacji, testów i skrypty publikowania.</span><span class="sxs-lookup"><span data-stu-id="1170c-105">You can edit and extend hello Windows PowerShell script in hello Visual Studio editor toosuit your requirements, or integrate hello script with existing build, test, and publishing scripts.</span></span>

<span data-ttu-id="1170c-106">Skrypty te można udostępnić dostosowane wersje (znanej także jako środowiskach programistycznych i testowych) lokacji do użytku tymczasowego.</span><span class="sxs-lookup"><span data-stu-id="1170c-106">Using these scripts, you can provision customized versions (also known as dev and test environments) of your site for temporary use.</span></span> <span data-ttu-id="1170c-107">Może na przykład skonfigurować konkretnej wersji witryny sieci Web na maszynie wirtualnej platformy Azure lub na powitania miejsca na toorun witryny sieci Web zestawu testów, występuje błąd, przetestować poprawkę, wersja próbna proponowanej zmiany lub skonfigurować niestandardowe środowisko pokaz lub prezentacji.</span><span class="sxs-lookup"><span data-stu-id="1170c-107">For example, you might set up a particular version of your website on an Azure virtual machine or on hello staging slot on a website toorun a test suite, reproduce a bug, test a bug fix, trial a proposed change, or set up a custom environment for a demo or presentation.</span></span> <span data-ttu-id="1170c-108">Po utworzeniu skryptu, który publikuje projektu można odtworzyć identyczne środowisk, ponownie uruchamiając skrypt hello zgodnie z potrzebami lub uruchom skrypt hello z własnych kompilacji toocreate aplikacji sieci web niestandardowego środowiska do testowania.</span><span class="sxs-lookup"><span data-stu-id="1170c-108">After you've created a script that publishes your project, you can recreate identical environments by re-running hello script as needed, or run hello script with your own build of your web application toocreate a custom environment for testing.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="1170c-109">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="1170c-109">What you need</span></span>
* <span data-ttu-id="1170c-110">Zestaw Azure SDK 2.3 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="1170c-110">Azure SDK 2.3 or later.</span></span> <span data-ttu-id="1170c-111">Zobacz [programu Visual Studio pobiera](http://go.microsoft.com/fwlink/?LinkID=624384) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="1170c-111">See [Visual Studio Downloads](http://go.microsoft.com/fwlink/?LinkID=624384) for more information.</span></span>

<span data-ttu-id="1170c-112">Nie trzeba hello Azure SDK toogenerate hello skryptów dla projektów sieci web.</span><span class="sxs-lookup"><span data-stu-id="1170c-112">You do not need hello Azure SDK toogenerate hello scripts for web projects.</span></span> <span data-ttu-id="1170c-113">Ta funkcja jest dla projektów sieci web, nie role sieci web usług w chmurze.</span><span class="sxs-lookup"><span data-stu-id="1170c-113">This feature is for web projects, not web roles in cloud services.</span></span>

* <span data-ttu-id="1170c-114">Program Azure PowerShell 0.7.4 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="1170c-114">Azure PowerShell 0.7.4 or later.</span></span> <span data-ttu-id="1170c-115">Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="1170c-115">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>
* <span data-ttu-id="1170c-116">[Program Windows PowerShell 3.0](http://go.microsoft.com/?linkid=9811175) lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="1170c-116">[Windows PowerShell 3.0](http://go.microsoft.com/?linkid=9811175) or later.</span></span>

## <a name="additional-tools"></a><span data-ttu-id="1170c-117">Dodatkowe narzędzia</span><span class="sxs-lookup"><span data-stu-id="1170c-117">Additional tools</span></span>
<span data-ttu-id="1170c-118">Dodatkowych narzędzi i zasobów do pracy z programu PowerShell w programie Visual Studio do tworzenia aplikacji platformy Azure są dostępne.</span><span class="sxs-lookup"><span data-stu-id="1170c-118">Additional tools and resources for working with PowerShell in Visual Studio for Azure development are available.</span></span> <span data-ttu-id="1170c-119">Zobacz [narzędzia programu PowerShell dla programu Visual Studio](http://go.microsoft.com/fwlink/?LinkId=404012).</span><span class="sxs-lookup"><span data-stu-id="1170c-119">See [PowerShell Tools for Visual Studio](http://go.microsoft.com/fwlink/?LinkId=404012).</span></span>

## <a name="generating-hello-publish-scripts"></a><span data-ttu-id="1170c-120">Generowanie hello publikowanie skryptów</span><span class="sxs-lookup"><span data-stu-id="1170c-120">Generating hello publish scripts</span></span>
<span data-ttu-id="1170c-121">Możesz wygenerować hello publikowanie skryptów do maszyny wirtualnej, który jest hostem witryny sieci Web, podczas tworzenia nowego projektu wykonując [tych instrukcji](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1170c-121">You can generate hello publish scripts for a virtual machine that hosts your website when you create a new project by following [these instructions](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="1170c-122">Możesz również [Generowanie publikowanie skryptów dla aplikacji sieci web w usłudze Azure App Service](app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="1170c-122">You can also [generate publish scripts for web apps in Azure App Service](app-service-web/app-service-web-get-started-dotnet.md).</span></span>

## <a name="scripts-that-visual-studio-generates"></a><span data-ttu-id="1170c-123">Skrypty, które generuje Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1170c-123">Scripts that Visual Studio generates</span></span>
<span data-ttu-id="1170c-124">Visual Studio generuje folder rozwiązania poziomu o nazwie **PublishScripts** skrypt publikowania dla maszyny wirtualnej lub witryny sieci Web i moduł, który zawiera funkcje, których można używać w hello zawiera dwa pliki programu Windows PowerShell, skrypty.</span><span class="sxs-lookup"><span data-stu-id="1170c-124">Visual Studio generates a solution-level folder called **PublishScripts** that contains two Windows PowerShell files, a publish script for your virtual machine or website, and a module that contains functions that you can use in hello scripts.</span></span> <span data-ttu-id="1170c-125">Visual Studio także generuje plik w formacie JSON hello, który określa szczegóły hello hello projektu, który jest wdrażany.</span><span class="sxs-lookup"><span data-stu-id="1170c-125">Visual Studio also generates a file in hello JSON format that specifies hello details of hello project you are deploying.</span></span>

### <a name="windows-powershell-publish-script"></a><span data-ttu-id="1170c-126">Skrypt publikowanie programu Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="1170c-126">Windows PowerShell publish script</span></span>
<span data-ttu-id="1170c-127">Witaj publikowania skryptu zawiera określone publikowania kroki wdrażania tooa witryny sieci Web lub maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1170c-127">hello publish script contains specific publish steps for deploying tooa website or virtual machine.</span></span> <span data-ttu-id="1170c-128">Program Visual Studio udostępnia kolorowania rozwoju środowiska Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1170c-128">Visual Studio provides syntax coloring for Windows PowerShell development.</span></span> <span data-ttu-id="1170c-129">Pomoc dla funkcji hello jest dostępne, a można swobodnie edytować funkcji hello w toosuit skryptu hello zmieniających się wymagań.</span><span class="sxs-lookup"><span data-stu-id="1170c-129">Help for hello functions is available, and you can freely edit hello functions in hello script toosuit your changing requirements.</span></span>

### <a name="windows-powershell-module"></a><span data-ttu-id="1170c-130">Moduł programu Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="1170c-130">Windows PowerShell module</span></span>
<span data-ttu-id="1170c-131">Witaj środowiska Windows PowerShell moduł, który generuje Visual Studio zawiera funkcje, które hello publikowania używa skryptu.</span><span class="sxs-lookup"><span data-stu-id="1170c-131">hello Windows PowerShell module that Visual Studio generates contains functions that hello publish script uses.</span></span> <span data-ttu-id="1170c-132">Są to funkcje środowiska Azure PowerShell które nie mają zamierzonego toobe zmodyfikowane.</span><span class="sxs-lookup"><span data-stu-id="1170c-132">These are Azure PowerShell functions and are not intended toobe modified.</span></span> <span data-ttu-id="1170c-133">Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="1170c-133">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>

### <a name="json-configuration-file"></a><span data-ttu-id="1170c-134">Plik JSON konfiguracji</span><span class="sxs-lookup"><span data-stu-id="1170c-134">JSON configuration file</span></span>
<span data-ttu-id="1170c-135">Plik JSON Hello jest tworzony w hello **konfiguracje** folderu i zawiera dane konfiguracji, które określa dokładnie które tooAzure toodeploy zasobów.</span><span class="sxs-lookup"><span data-stu-id="1170c-135">hello JSON file is created in hello **Configurations** folder and contains configuration data that specifies exactly which resources toodeploy tooAzure.</span></span> <span data-ttu-id="1170c-136">Nazwa Hello hello pliku, który generuje Visual Studio jest projektu name-WAWS-dev.json Jeśli utworzono witrynę sieci Web lub projektu Nazwa-maszyny Wirtualnej — dev.json Jeśli utworzono maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="1170c-136">hello name of hello file that Visual Studio generates is project-name-WAWS-dev.json if you created a website, or project name-VM-dev.json if you created a virtual machine.</span></span> <span data-ttu-id="1170c-137">Oto przykładowy plik JSON konfiguracji, który jest generowany podczas tworzenia witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="1170c-137">Here's an example of a JSON configuration file that's generated when you create a website.</span></span> <span data-ttu-id="1170c-138">Większość wartości hello nie wymaga wyjaśnień.</span><span class="sxs-lookup"><span data-stu-id="1170c-138">Most of hello values are self-explanatory.</span></span> <span data-ttu-id="1170c-139">Nazwa witryny sieci Web Hello jest generowany przez Azure, dlatego mogą być niezgodne nazwę projektu.</span><span class="sxs-lookup"><span data-stu-id="1170c-139">hello website name is generated by Azure, so it might not match your project name.</span></span>

```json
{
    "environmentSettings": {
        "webSite": {
            "name": "WebApplication26632",
            "location": "West US"
        },
        "databases": [{
            "connectionStringName": "DefaultConnection",
            "databaseName": "WebApplication26632_db",
            "serverName": "YourDatabaseServerName",
            "user": "sqluser2",
            "password": "",
            "edition": "",
            "size": "",
            "collation": "",
            "location": "West US"
        }]
    }
}
```
<span data-ttu-id="1170c-140">Podczas tworzenia maszyny wirtualnej pliku konfiguracji JSON hello wygląda podobnie następujące toohello.</span><span class="sxs-lookup"><span data-stu-id="1170c-140">When you create a virtual machine, hello JSON configuration file looks similar toohello following.</span></span> <span data-ttu-id="1170c-141">Należy pamiętać, że usługa w chmurze jest tworzony jako kontener dla maszyny wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="1170c-141">Note that a cloud service is created as a container for hello virtual machine.</span></span> <span data-ttu-id="1170c-142">Maszyna wirtualna Hello zawiera hello zwykle punktów końcowych dostęp w sieci web za pośrednictwem protokołu HTTP i HTTPS, a także punktów końcowych dla narzędzia Web Deploy, który umożliwia publikowanie toohello witryny sieci Web z komputera lokalnego, pulpitu zdalnego i środowiska Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1170c-142">hello virtual machine contains hello usual endpoints for web access through HTTP and HTTPS, as well as endpoints for Web Deploy, which lets you publish toohello website from your local machine, Remote Desktop, and Windows PowerShell.</span></span>

```json
{
    "environmentSettings": {
        "cloudService": {
            "name": "myusernamevm1",
            "affinityGroup": "",
            "location": "West US",
            "virtualNetwork": "",
            "subnet": "",
            "availabilitySet": "",
            "virtualMachine": {
                "name": "myusernamevm1",
                "vhdImage": "a699494373c04fc0bc8f2bb1389d6106__Win2K8R2SP1-Datacenter-201403.01-en.us-127GB.vhd",
                "size": "Small",
                "user": "vmuser1",
                "password": "",
                "enableWebDeployExtension": true,
                "endpoints": [{
                        "name": "Http",
                        "protocol": "TCP",
                        "publicPort": "80",
                        "privatePort": "80"
                    },
                    {
                        "name": "Https",
                        "protocol": "TCP",
                        "publicPort": "443",
                        "privatePort": "443"
                    },
                    {
                        "name": "WebDeploy",
                        "protocol": "TCP",
                        "publicPort": "8172",
                        "privatePort": "8172"
                    },
                    {
                        "name": "Remote Desktop",
                        "protocol": "TCP",
                        "publicPort": "3389",
                        "privatePort": "3389"
                    },
                    {
                        "name": "Powershell",
                        "protocol": "TCP",
                        "publicPort": "5986",
                        "privatePort": "5986"
                    }
                ]
            }
        },
        "databases": [{
            "connectionStringName": "",
            "databaseName": "",
            "serverName": "",
            "user": "",
            "password": ""
        }],
        "webDeployParameters": {
            "iisWebApplicationName": "Default Web Site"
        }
    }
}
```

<span data-ttu-id="1170c-143">Co się stanie po uruchomieniu hello można edytować hello JSON konfiguracji toochange publikowanie skryptów.</span><span class="sxs-lookup"><span data-stu-id="1170c-143">You can edit hello JSON configuration toochange what happens when you run hello publish scripts.</span></span> <span data-ttu-id="1170c-144">Witaj `cloudService` i `virtualMachine` sekcje są wymagane, ale można usunąć hello `databases` sekcji, jeśli nie jest potrzebna.</span><span class="sxs-lookup"><span data-stu-id="1170c-144">hello `cloudService` and `virtualMachine` sections are required, but you can delete hello `databases` section if you don't need it.</span></span> <span data-ttu-id="1170c-145">Hello właściwości, które są puste w hello domyślny plik konfiguracji generowany w programie Visual Studio jest opcjonalna. te, które mają wartości w pliku konfiguracyjnym domyślna hello są wymagane.</span><span class="sxs-lookup"><span data-stu-id="1170c-145">hello properties that are empty in hello default configuration file that Visual Studio generates are optional; those that have values in hello default configuration file are required.</span></span>

<span data-ttu-id="1170c-146">Jeśli masz witrynę sieci Web, który ma wiele środowisk wdrażania (nazywanych miejscami) zamiast lokacji pojedynczego produkcji na platformie Azure, hello z nazwą miejsca można uwzględnić w nazwie hello hello witryny sieci Web w pliku konfiguracji JSON hello.</span><span class="sxs-lookup"><span data-stu-id="1170c-146">If you have a website that has multiple deployment environments (known as slots) instead of a single production site in Azure, you can include hello slot name in hello name of hello website in hello JSON configuration file.</span></span> <span data-ttu-id="1170c-147">Na przykład, jeśli masz witrynę sieci Web o nazwie **witryna** z miejscem dla niego o nazwie **test** , a następnie hello identyfikatora URI jest test.cloudapp.net witrynę, ale hello poprawną nazwę toouse w pliku konfiguracyjnym hello jest mysite(test) .</span><span class="sxs-lookup"><span data-stu-id="1170c-147">For example, if you have a website that's named **mysite** and a slot for it named **test** then hello URI is mysite-test.cloudapp.net, but hello correct name toouse in hello configuration file is mysite(test).</span></span> <span data-ttu-id="1170c-148">Tylko można to zrobić, jeśli hello witryny sieci Web i gniazd już istnieją w Twojej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="1170c-148">You can only do this if hello website and slots already exist in your subscription.</span></span> <span data-ttu-id="1170c-149">Jeśli nie istnieją, Utwórz hello witryny sieci Web, uruchamiając skrypt hello bez określania miejsca hello, a następnie utworzyć gniazda hello hello [klasycznego portalu Azure](http://go.microsoft.com/fwlink/?LinkID=213885), a następnie uruchom skrypt hello o nazwie modyfikacji witryny sieci Web hello.</span><span class="sxs-lookup"><span data-stu-id="1170c-149">If they don't exist, create hello website by running hello script without specifying hello slot, then create hello slot in hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), and thereafter run hello script with hello modified website name.</span></span> <span data-ttu-id="1170c-150">Aby uzyskać więcej informacji dotyczących miejsc wdrożenia dla aplikacji sieci web, zobacz [Konfigurowanie środowiska dla aplikacji sieci web w usłudze Azure App Service przejściowe](app-service-web/web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="1170c-150">For more information about deployment slots for web apps, see [Set up staging environments for web apps in Azure App Service](app-service-web/web-sites-staged-publishing.md).</span></span>

## <a name="how-toorun-hello-publish-scripts"></a><span data-ttu-id="1170c-151">Jak toorun hello opublikować skryptów</span><span class="sxs-lookup"><span data-stu-id="1170c-151">How toorun hello publish scripts</span></span>
<span data-ttu-id="1170c-152">Jeśli nigdy nie zostało uruchomione przed skrypt programu Windows PowerShell, należy najpierw ustawić hello wykonywania zasad tooenable skrypty toorun.</span><span class="sxs-lookup"><span data-stu-id="1170c-152">If you have never run a Windows PowerShell script before, you must first set hello execution policy tooenable scripts toorun.</span></span> <span data-ttu-id="1170c-153">Jest to użytkowników tooprevent funkcji zabezpieczeń, uruchamiania skryptów programu Windows PowerShell, jeśli są one narażone toomalware i wirusami, które obejmują wykonywanie skryptów.</span><span class="sxs-lookup"><span data-stu-id="1170c-153">This is a security feature tooprevent users from running Windows PowerShell scripts if they're vulnerable toomalware or viruses that involve executing scripts.</span></span>

### <a name="run-hello-script"></a><span data-ttu-id="1170c-154">Uruchom skrypt hello</span><span class="sxs-lookup"><span data-stu-id="1170c-154">Run hello script</span></span>
1. <span data-ttu-id="1170c-155">Utwórz hello pakietu Narzędzia Web Deploy w dla projektu.</span><span class="sxs-lookup"><span data-stu-id="1170c-155">Create hello Web Deploy package for your project.</span></span> <span data-ttu-id="1170c-156">Pakiet Web Deploy jest skompresowanego archiwum (pliku .zip), zawierających pliki mają toocopy tooyour witryny sieci Web lub maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1170c-156">A Web Deploy package is a compressed archive (.zip file) that contain files that you want toocopy tooyour website or virtual machine.</span></span> <span data-ttu-id="1170c-157">Pakiety Web Deploy można tworzyć w programie Visual Studio dla dowolnej aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="1170c-157">You can create Web Deploy packages in Visual Studio for any web application.</span></span>

![Tworzenie sieci Web wdrażanie pakietu](./media/vs-azure-tools-publishing-using-powershell-scripts/IC767885.png)

<span data-ttu-id="1170c-159">Aby uzyskać więcej informacji, zobacz [jak: utworzyć pakiet wdrożeniowy sieci Web w programie Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span><span class="sxs-lookup"><span data-stu-id="1170c-159">For more information, see [How to: Create a Web Deployment Package in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span></span> <span data-ttu-id="1170c-160">Można również zautomatyzować tworzenie hello pakietu Narzędzia Web Deploy, zgodnie z opisem w sekcji hello **dostosowywanie i rozszerzanie hello publikowanie skryptów** dalszej części tego tematu.</span><span class="sxs-lookup"><span data-stu-id="1170c-160">You can also automate hello creation of your Web Deploy package, as described in hello section **Customizing and extending hello publish scripts** later in this topic.</span></span>

1. <span data-ttu-id="1170c-161">W **Eksploratora rozwiązań**, otwórz menu kontekstowe hello hello skryptu, a następnie wybierz **otworzyć za pomocą programu PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="1170c-161">In **Solution Explorer**, open hello context menu for hello script, and then choose **Open with PowerShell ISE**.</span></span>
2. <span data-ttu-id="1170c-162">Jeśli jest to hello na tym komputerze uruchomiono skryptów programu Windows PowerShell po raz pierwszy, Otwórz okno wiersza polecenia z uprawnieniami administratora i hello wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="1170c-162">If this is hello first time you've run Windows PowerShell scripts on this computer, open a command prompt window with Administrator privileges and type hello following command:</span></span>

    ```powershell
    Set-ExecutionPolicy RemoteSigned
    ```

3. <span data-ttu-id="1170c-163">Zaloguj przy użyciu następującego polecenia hello tooAzure.</span><span class="sxs-lookup"><span data-stu-id="1170c-163">Sign in tooAzure by using hello following command.</span></span>

    ```powershell
    Add-AzureAccount
    ```

    <span data-ttu-id="1170c-164">Po wyświetleniu monitu podaj nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="1170c-164">When prompted, supply your username and password.</span></span>

    <span data-ttu-id="1170c-165">Należy zwrócić uwagę podczas automatyzacji hello skryptu, ta metoda podawania poświadczeń platformy Azure nie będą działać.</span><span class="sxs-lookup"><span data-stu-id="1170c-165">Note that when you automate hello script, this method of providing Azure credentials won't work.</span></span> <span data-ttu-id="1170c-166">Zamiast tego należy używać poświadczeń tooprovide pliku .publishsettings hello.</span><span class="sxs-lookup"><span data-stu-id="1170c-166">Instead, you should use hello .publishsettings file tooprovide credentials.</span></span> <span data-ttu-id="1170c-167">Jeden raz, możesz użyć polecenia hello **Get-AzurePublishSettingsFile** toodownload hello pliku z platformy Azure, a następnie użyć **AzurePublishSettingsFile importu** tooimport hello pliku.</span><span class="sxs-lookup"><span data-stu-id="1170c-167">One time only, you use hello command **Get-AzurePublishSettingsFile** toodownload hello file from Azure, and thereafter use **Import-AzurePublishSettingsFile** tooimport hello file.</span></span> <span data-ttu-id="1170c-168">Aby uzyskać szczegółowe instrukcje, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1170c-168">For detailed instructions, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

4. <span data-ttu-id="1170c-169">(Opcjonalnie) Jeśli chcesz, aby toocreate Azure zasoby, takie jak hello maszyny wirtualnej, bazy danych i witryny sieci Web bez publikowania aplikacji sieci web, użyj hello **WebApplication.ps1 publikowania** z hello **-konfiguracji** pliku konfiguracji JSON toohello wartość argumentu.</span><span class="sxs-lookup"><span data-stu-id="1170c-169">(Optional) If you want toocreate Azure resources such as hello virtual machine, database, and website without publishing your web application, use hello **Publish-WebApplication.ps1** command with hello **-Configuration** argument set toohello JSON configuration file.</span></span> <span data-ttu-id="1170c-170">Ten wiersz polecenia korzysta toodetermine pliku konfiguracji JSON hello które toocreate zasobów.</span><span class="sxs-lookup"><span data-stu-id="1170c-170">This command line uses hello JSON configuration file toodetermine which resources toocreate.</span></span> <span data-ttu-id="1170c-171">Ponieważ używa ustawień domyślnych hello inne argumenty wiersza polecenia, tworzy hello zasobów, ale nie publikowania aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="1170c-171">Because it uses hello default settings for other command-line arguments, it creates hello resources, but doesn't publish your web application.</span></span> <span data-ttu-id="1170c-172">Witaj — opcja pełne zapewnia więcej informacji o tym, co dzieje.</span><span class="sxs-lookup"><span data-stu-id="1170c-172">hello –Verbose option gives you more information about what's happening.</span></span>

    ```powershell
    Publish-WebApplication.ps1 -Verbose –Configuration C:\Path\WebProject-WAWS-dev.json
    ```

5. <span data-ttu-id="1170c-173">Użyj hello **WebApplication.ps1 publikowania** polecenia, jak pokazano w jednym z hello następujące przykłady tooinvoke hello skrypt i opublikować aplikację sieci web.</span><span class="sxs-lookup"><span data-stu-id="1170c-173">Use hello **Publish-WebApplication.ps1** command as shown in one of hello following examples tooinvoke hello script and publish your web application.</span></span> <span data-ttu-id="1170c-174">Jeśli potrzebujesz toooverride hello domyślne ustawienia dla każdego hello inne argumenty, takie jak nazwa subskrypcji hello, publikowanie nazwy pakietu, poświadczenia maszyny wirtualnej lub poświadczenia serwera bazy danych, można określić tych parametrów.</span><span class="sxs-lookup"><span data-stu-id="1170c-174">If you need toooverride hello default settings for any of hello other arguments, such as hello subscription name, publish package name, virtual machine credentials, or database server credentials, you can specify those parameters.</span></span> <span data-ttu-id="1170c-175">Użyj hello **— pełne** opcję toosee więcej informacji na temat postępu hello hello procesu publikowania.</span><span class="sxs-lookup"><span data-stu-id="1170c-175">Use hello **–Verbose** option toosee more information about hello progress of hello publishing process.</span></span>

    ```powershell
    Publish-WebApplication.ps1 –Configuration C:\Path\WebProject-WAWS-dev-json `
    –SubscriptionName Contoso `
    -WebDeployPackage C:\Documents\Azure\ADWebApp.zip `
    -DatabaseServerPassword @{Name="dbServerName";Password="adminPassword"} `
    -Verbose
    ```

    <span data-ttu-id="1170c-176">Jeśli tworzysz maszynę wirtualną, polecenie hello wygląda hello.</span><span class="sxs-lookup"><span data-stu-id="1170c-176">If you're creating a virtual machine, hello command looks like hello following.</span></span> <span data-ttu-id="1170c-177">W tym przykładzie przedstawiono również sposób toospecify hello poświadczeń dla wielu baz danych.</span><span class="sxs-lookup"><span data-stu-id="1170c-177">This example also shows how toospecify hello credentials for multiple databases.</span></span> <span data-ttu-id="1170c-178">Hello maszyn wirtualnych utworzonych przez te skrypty hello certyfikat SSL nie pochodzi z zaufanego głównego urzędu.</span><span class="sxs-lookup"><span data-stu-id="1170c-178">For hello virtual machines that these scripts create, hello SSL certificate is not from a trusted root authority.</span></span> <span data-ttu-id="1170c-179">Dlatego należy toouse hello **— AllowUntrusted** opcji.</span><span class="sxs-lookup"><span data-stu-id="1170c-179">Therefore, you need toouse hello **–AllowUntrusted** option.</span></span>

    ```powershell
    Publish-WebApplication.ps1 `
    -Configuration C:\Path\ADVM-VM-test.json `
    -SubscriptionName Contoso `
    -WebDeployPackage C:\Path\ADVM.zip `
    -AllowUntrusted `
    -VMPassword @{name = "vmUserName"; password = "YourPasswordHere"} `
    -DatabaseServerPassword @{Name="server1";Password="adminPassword1"}, @{Name="server2";Password="adminPassword2"} `
    -Verbose
    ```

    <span data-ttu-id="1170c-180">skrypt Hello można utworzyć bazy danych, ale nie tworzy serwerów baz danych.</span><span class="sxs-lookup"><span data-stu-id="1170c-180">hello script can create databases, but it doesn't create database servers.</span></span> <span data-ttu-id="1170c-181">Jeśli chcesz toocreate serwera bazy danych, można użyć hello **AzureSqlDatabaseServer nowy** funkcji w hello modułu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1170c-181">If you want toocreate a database server, you can use hello **New-AzureSqlDatabaseServer** function in hello Azure module.</span></span>

## <a name="customizing-and-extending-hello-publish-scripts"></a><span data-ttu-id="1170c-182">Dostosowywanie i rozszerzanie hello publikowanie skryptów</span><span class="sxs-lookup"><span data-stu-id="1170c-182">Customizing and extending hello publish scripts</span></span>
<span data-ttu-id="1170c-183">Można dostosować hello publikowania skryptu i pliku konfiguracji JSON.</span><span class="sxs-lookup"><span data-stu-id="1170c-183">You can customize hello publish script and JSON configuration file.</span></span> <span data-ttu-id="1170c-184">Witaj funkcji w module środowiska Windows PowerShell hello **AzureWebAppPublishModule.psm1** nie są zamierzone toobe zmodyfikowane.</span><span class="sxs-lookup"><span data-stu-id="1170c-184">hello functions in hello Windows PowerShell module **AzureWebAppPublishModule.psm1** are not intended toobe modified.</span></span> <span data-ttu-id="1170c-185">Po prostu toospecify innej bazy danych lub zmienić niektóre właściwości hello hello maszyny wirtualnej, należy edytować plik konfiguracji JSON hello.</span><span class="sxs-lookup"><span data-stu-id="1170c-185">If you just want toospecify a different database or change some of hello properties of hello virtual machine, edit hello JSON configuration file.</span></span> <span data-ttu-id="1170c-186">Chcąc tooextend funkcjonalność hello hello skryptu tooautomate tworzenia i testowania projektu, można zaimplementować klas zastępczych funkcji w **WebApplication.ps1 publikowania**.</span><span class="sxs-lookup"><span data-stu-id="1170c-186">If you want tooextend hello functionality of hello script tooautomate building and testing your project, you can implement function stubs in **Publish-WebApplication.ps1**.</span></span>

<span data-ttu-id="1170c-187">tooautomate tworzenia projektu, Dodaj kod, który wywołuje MSBuild zbyt`New-WebDeployPackage` opisane w tym przykładzie kodu.</span><span class="sxs-lookup"><span data-stu-id="1170c-187">tooautomate building your project, add code that calls MSBuild too`New-WebDeployPackage` as shown in this code example.</span></span> <span data-ttu-id="1170c-188">toohello ścieżka Hello polecenie MSBuild różni się w zależności od wersji hello programu Visual Studio został zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="1170c-188">hello path toohello MSBuild command is different depending on hello version of Visual Studio you have installed.</span></span> <span data-ttu-id="1170c-189">tooget hello poprawną ścieżkę, możesz użyć funkcji hello **Get-MSBuildCmd**, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="1170c-189">tooget hello correct path, you can use hello function **Get-MSBuildCmd**, as shown in this example.</span></span>

### <a name="tooautomate-building-your-project"></a><span data-ttu-id="1170c-190">tooautomate tworzenia projektu</span><span class="sxs-lookup"><span data-stu-id="1170c-190">tooautomate building your project</span></span>
1. <span data-ttu-id="1170c-191">Dodaj hello `$ProjectFile` parametru w sekcji globalne param hello.</span><span class="sxs-lookup"><span data-stu-id="1170c-191">Add hello `$ProjectFile` parameter in hello global param section.</span></span>

    ```powershell
    [Parameter(Mandatory = $false)]
    [ValidateScript({Test-Path $_ -PathType Leaf})]
    [String]
    $ProjectFile,
    ```

2. <span data-ttu-id="1170c-192">Copy — funkcja hello `Get-MSBuildCmd` do pliku skryptu.</span><span class="sxs-lookup"><span data-stu-id="1170c-192">Copy hello function `Get-MSBuildCmd` into your script file.</span></span>

    ```powershell
    function Get-MSBuildCmd
    {
            process
    {

                $path =  Get-ChildItem "HKLM:\SOFTWARE\Microsoft\MSBuild\ToolsVersions\" |
                                    Sort-Object {[double]$_.PSChildName} -Descending |
                                    Select-Object -First 1 |
                                    Get-ItemProperty -Name MSBuildToolsPath |
                                    Select -ExpandProperty MSBuildToolsPath

                $path = (Join-Path -Path $path -ChildPath 'msbuild.exe')

            return Get-Item $path
        }
    }
    ```

3. <span data-ttu-id="1170c-193">Zastąp `New-WebDeployPackage` z hello następujący kod i zastąp symbole zastępcze hello podczas tworzenia wiersza hello `$msbuildCmd`.</span><span class="sxs-lookup"><span data-stu-id="1170c-193">Replace `New-WebDeployPackage` with hello following code and replace hello placeholders in hello line constructing `$msbuildCmd`.</span></span> <span data-ttu-id="1170c-194">Ten kod jest dla programu Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="1170c-194">This code is for Visual Studio 2015.</span></span> <span data-ttu-id="1170c-195">Jeśli używasz programu Visual Studio 2013, zmień hello **VisualStudioVersion** właściwości poniżej zbyt`12.0`.</span><span class="sxs-lookup"><span data-stu-id="1170c-195">If you're using Visual Studio 2013, change hello **VisualStudioVersion** property below too`12.0`.</span></span>

    ```powershell
    function New-WebDeployPackage
    {
        #Write a function toobuild and package your web application
    ```

    <span data-ttu-id="1170c-196">toobuild Twojej aplikacji sieci web, użyj MsBuild.exe.</span><span class="sxs-lookup"><span data-stu-id="1170c-196">toobuild your web application, use MsBuild.exe.</span></span> <span data-ttu-id="1170c-197">Aby uzyskać pomoc, zobacz MSBuild wiersza polecenia pod adresem: [http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339)</span><span class="sxs-lookup"><span data-stu-id="1170c-197">For help, see MSBuild Command-Line Reference at: [http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339)</span></span>

    ```powershell
    Write-VerboseWithTime 'Build-WebDeployPackage: Start'

    $msbuildCmd = '"{0}" "{1}" /T:Rebuild;Package /P:VisualStudioVersion=14.0 /p:OutputPath="{2}\MSBuildOutputPath" /flp:logfile=msbuild.log,v=d' -f (Get-MSBuildCmd), $ProjectFile, $scriptDirectory

    Write-VerboseWithTime ('Build-WebDeployPackage: ' + $msbuildCmd)
    ```

### <a name="start-execution-of-hello-build-command"></a><span data-ttu-id="1170c-198">Wykonanie polecenia kompilacji hello Start</span><span class="sxs-lookup"><span data-stu-id="1170c-198">Start execution of hello build command</span></span>

```powershell
$job = Start-Process cmd.exe -ArgumentList('/C "' + $msbuildCmd + '"') -WindowStyle Normal -Wait -PassThru

if ($job.ExitCode -ne 0) {
    throw('MsBuild exited with an error. ExitCode:' + $job.ExitCode)
}

#Obtain hello project name
$projectName = (Get-Item $ProjectFile).BaseName

#Construct hello path tooweb deploy zip package
$DeployPackageDir =  '.\MSBuildOutputPath\_PublishedWebsites\{0}_Package\{0}.zip' -f $projectName

#Get hello full path for hello web deploy zip package. This is required for MSDeploy toowork
$WebDeployPackage = Resolve-Path –LiteralPath $DeployPackageDir

Write-VerboseWithTime 'Build-WebDeployPackage: End'

return $WebDeployPackage
}
```

1. <span data-ttu-id="1170c-199">Wywołaj hello `New-WebDeployPackage` funkcja przed wierszem: `$Config = Read-ConfigFile $Configuration` dla aplikacji sieci web lub `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` dla maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="1170c-199">Call hello `New-WebDeployPackage` function before this line: `$Config = Read-ConfigFile $Configuration` for web apps or `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` for virtual machines.</span></span>

    ```powershell
    if($ProjectFile)
    {
    $WebDeployPackage = New-WebDeployPackage
    }
    ```

2. <span data-ttu-id="1170c-200">Wywołanie skryptu hello dostosowane z wiersza polecenia przy użyciu hello przekazywanie `$Project` argumentu, tak jak powitania po przykład wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="1170c-200">Invoke hello customized script from command line using passing hello `$Project` argument, as in hello following example command line.</span></span>

    ```powershell
    .\Publish-WebApplicationVM.ps1 -Configuration .\Configurations\WebApplication5-VM-dev.json `
    -ProjectFile ..\WebApplication5\WebApplication5.csproj `
    -VMPassword @{Name="VMUser";Password="Test.123"} `
    -AllowUntrusted `
    -Verbose
    ```

    <span data-ttu-id="1170c-201">tooautomate testowania aplikacji, Dodaj kod zbyt`Test-WebApplication`.</span><span class="sxs-lookup"><span data-stu-id="1170c-201">tooautomate testing of your application, add code too`Test-WebApplication`.</span></span> <span data-ttu-id="1170c-202">Należy się toouncomment hello wierszy w **WebApplication.ps1 publikowania** gdzie te funkcje są wywoływane.</span><span class="sxs-lookup"><span data-stu-id="1170c-202">Be sure toouncomment hello lines in **Publish-WebApplication.ps1** where these functions are called.</span></span> <span data-ttu-id="1170c-203">Jeśli nie zapewniać implementację, można ręcznie utworzyć projektu za pomocą programu Visual Studio, a następnie uruchom hello Opublikuj tooAzure toopublish skryptu.</span><span class="sxs-lookup"><span data-stu-id="1170c-203">If you don't provide an implementation, you can manually build your project with Visual Studio, and then run hello publish script toopublish tooAzure.</span></span>

## <a name="publishing-function-summary"></a><span data-ttu-id="1170c-204">Podsumowanie funkcji publikowania</span><span class="sxs-lookup"><span data-stu-id="1170c-204">Publishing function summary</span></span>
<span data-ttu-id="1170c-205">tooget pomocy dla funkcji, można użyć w wierszu polecenia programu Windows PowerShell hello, użyj polecenia hello `Get-Help function-name`.</span><span class="sxs-lookup"><span data-stu-id="1170c-205">tooget help for functions you can use at hello Windows PowerShell command prompt, use hello command `Get-Help function-name`.</span></span> <span data-ttu-id="1170c-206">Pomoc Hello zawiera parametr pomocy i przykłady.</span><span class="sxs-lookup"><span data-stu-id="1170c-206">hello help includes parameter help and examples.</span></span> <span data-ttu-id="1170c-207">Witaj tego samego tekstu pomocy jest również w plikach źródłowych skryptu hello, **AzureWebAppPublishModule.psm1** i **WebApplication.ps1 publikowania**.</span><span class="sxs-lookup"><span data-stu-id="1170c-207">hello same help text is also in hello script source files, **AzureWebAppPublishModule.psm1** and **Publish-WebApplication.ps1**.</span></span> <span data-ttu-id="1170c-208">skrypt Hello i pomocy są zlokalizowane w języku Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1170c-208">hello script and help are localized in your Visual Studio language.</span></span>

<span data-ttu-id="1170c-209">**AzureWebAppPublishModule**</span><span class="sxs-lookup"><span data-stu-id="1170c-209">**AzureWebAppPublishModule**</span></span>

| <span data-ttu-id="1170c-210">Nazwa funkcji</span><span class="sxs-lookup"><span data-stu-id="1170c-210">Function name</span></span> | <span data-ttu-id="1170c-211">Opis</span><span class="sxs-lookup"><span data-stu-id="1170c-211">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1170c-212">Dodaj AzureSQLDatabase</span><span class="sxs-lookup"><span data-stu-id="1170c-212">Add-AzureSQLDatabase</span></span> |<span data-ttu-id="1170c-213">Tworzy nową bazę danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="1170c-213">Creates a new Azure SQL database.</span></span> |
| <span data-ttu-id="1170c-214">Dodaj AzureSQLDatabases</span><span class="sxs-lookup"><span data-stu-id="1170c-214">Add-AzureSQLDatabases</span></span> |<span data-ttu-id="1170c-215">Tworzy baz danych Azure SQL z hello wartości w pliku konfiguracji JSON hello, który generuje Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1170c-215">Creates Azure SQL databases from hello values in hello JSON configuration file that Visual Studio generates.</span></span> |
| <span data-ttu-id="1170c-216">Dodaj AzureVM</span><span class="sxs-lookup"><span data-stu-id="1170c-216">Add-AzureVM</span></span> |<span data-ttu-id="1170c-217">Tworzy maszynę wirtualną platformy Azure i zwraca adres URL hello hello wdrożyć maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1170c-217">Creates a Azure virtual machine and returns hello URL of hello deployed VM.</span></span> <span data-ttu-id="1170c-218">Witaj funkcja konfiguruje hello wymagania wstępne, a następnie wywołania hello **AzureVM nowy** funkcji toocreate (moduł Azure) nowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1170c-218">hello function sets up hello prerequisites and then calls hello **New-AzureVM** function (Azure module) toocreate a new virtual machine.</span></span> |
| <span data-ttu-id="1170c-219">Dodaj AzureVMEndpoints</span><span class="sxs-lookup"><span data-stu-id="1170c-219">Add-AzureVMEndpoints</span></span> |<span data-ttu-id="1170c-220">Dodaje nową maszynę wirtualną tooa wejściowych punktów końcowych i zwraca hello maszynę wirtualną z hello nowy punkt końcowy.</span><span class="sxs-lookup"><span data-stu-id="1170c-220">Adds new input endpoints tooa virtual machine and returns hello virtual machine with hello new endpoint.</span></span> |
| <span data-ttu-id="1170c-221">Dodaj AzureVMStorage</span><span class="sxs-lookup"><span data-stu-id="1170c-221">Add-AzureVMStorage</span></span> |<span data-ttu-id="1170c-222">Tworzy nowe konto magazynu Azure w hello bieżącej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="1170c-222">Creates a new Azure storage account in hello current subscription.</span></span> <span data-ttu-id="1170c-223">Nazwa Hello hello konta zaczyna się od "devtest", po której następują unikatowy ciąg alfanumeryczny.</span><span class="sxs-lookup"><span data-stu-id="1170c-223">hello name of hello account begins with "devtest" followed by a unique alphanumeric string.</span></span> <span data-ttu-id="1170c-224">Funkcja Hello zwraca nazwę hello hello nowe konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="1170c-224">hello function returns hello name of hello new storage account.</span></span> <span data-ttu-id="1170c-225">Należy określić lokalizację i grupę koligacji dla hello nowe konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="1170c-225">You must specify either a location or an affinity group for hello new storage account.</span></span> |
| <span data-ttu-id="1170c-226">Dodaj AzureWebsite</span><span class="sxs-lookup"><span data-stu-id="1170c-226">Add-AzureWebsite</span></span> |<span data-ttu-id="1170c-227">Tworzy witrynę sieci Web z hello określonej nazwy i lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="1170c-227">Creates a website with hello specified name and location.</span></span> <span data-ttu-id="1170c-228">Ta funkcja wymaga hello **AzureWebsite nowy** funkcji w hello modułu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1170c-228">This function calls hello **New-AzureWebsite** function in hello Azure module.</span></span> <span data-ttu-id="1170c-229">Jeśli subskrypcja hello już nie obejmuje witrynę sieci Web przy użyciu określonej nazwy hello, funkcja ta tworzy hello witryny sieci Web i zwraca obiekt witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="1170c-229">If hello subscription doesn't already include a website with hello specified name, this function creates hello website and returns a website object.</span></span> <span data-ttu-id="1170c-230">W przeciwnym razie zwraca `$null`.</span><span class="sxs-lookup"><span data-stu-id="1170c-230">Otherwise, it returns `$null`.</span></span> |
| <span data-ttu-id="1170c-231">Subskrypcji kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="1170c-231">Backup-Subscription</span></span> |<span data-ttu-id="1170c-232">Zapisuje hello bieżącej subskrypcji platformy Azure w hello `$Script:originalSubscription` zmiennej w zakresie skryptu. Ta funkcja jest zapisywany hello bieżącej subskrypcji platformy Azure (uzyskanych przez `Get-AzureSubscription -Current`) i jego konta magazynu oraz hello subskrypcji, która zostanie zmieniona przez ten skrypt (przechowywana w zmiennej hello `$UserSpecifiedSubscription`), a jego konto magazynu w zakresie skryptu.</span><span class="sxs-lookup"><span data-stu-id="1170c-232">Saves hello current Azure subscription in hello `$Script:originalSubscription` variable in script scope.This function saves hello current Azure subscription (as obtained by `Get-AzureSubscription -Current`) and its storage account, and hello subscription that is changed by this script (stored in hello variable `$UserSpecifiedSubscription`) and its storage account, in script scope.</span></span> <span data-ttu-id="1170c-233">Zapisując hello wartości można użyć funkcji, takich jak `Restore-Subscription`, toorestore hello oryginalnego bieżącej subskrypcji i magazynu toocurrent stan konta Jeśli hello bieżący stan został zmieniony.</span><span class="sxs-lookup"><span data-stu-id="1170c-233">By saving hello values, you can use a function, such as `Restore-Subscription`, toorestore hello original current subscription and storage account toocurrent status if hello current status has changed.</span></span> |
| <span data-ttu-id="1170c-234">Znajdź AzureVM</span><span class="sxs-lookup"><span data-stu-id="1170c-234">Find-AzureVM</span></span> |<span data-ttu-id="1170c-235">Pobiera hello określonej maszyny wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1170c-235">Gets hello specified Azure virtual machine.</span></span> |
| <span data-ttu-id="1170c-236">Format DevTestMessageWithTime</span><span class="sxs-lookup"><span data-stu-id="1170c-236">Format-DevTestMessageWithTime</span></span> |<span data-ttu-id="1170c-237">Dołącza wiadomość hello Data i godzina tooa.</span><span class="sxs-lookup"><span data-stu-id="1170c-237">Prepends hello date and time tooa message.</span></span> <span data-ttu-id="1170c-238">Ta funkcja jest przeznaczona dla komunikatów zapisanych toohello błąd i pełne strumieni.</span><span class="sxs-lookup"><span data-stu-id="1170c-238">This function is designed for messages written toohello Error and Verbose streams.</span></span> |
| <span data-ttu-id="1170c-239">Get-AzureSQLDatabaseConnectionString</span><span class="sxs-lookup"><span data-stu-id="1170c-239">Get-AzureSQLDatabaseConnectionString</span></span> |<span data-ttu-id="1170c-240">Składana bazy danych Azure SQL tooan tooconnect ciąg połączenia.</span><span class="sxs-lookup"><span data-stu-id="1170c-240">Assembles a connection string tooconnect tooan Azure SQL database.</span></span> |
| <span data-ttu-id="1170c-241">Get-AzureVMStorage</span><span class="sxs-lookup"><span data-stu-id="1170c-241">Get-AzureVMStorage</span></span> |<span data-ttu-id="1170c-242">Zwraca hello nazwę pierwszego konta magazynu hello mających wzorzec nazwy hello "devtest*" (bez uwzględniania wielkości liter) w określonej lokalizacji lub koligacji grupy hello. Jeśli hello "devtest*" hello lokalizacja lub grupa koligacji nie jest zgodna konta magazynu, funkcja hello ignoruje go.</span><span class="sxs-lookup"><span data-stu-id="1170c-242">Returns hello name of hello first storage account with hello name pattern "devtest*" (case insensitive) in hello specified location or affinity group. If hello "devtest*" storage account doesn't match hello location or affinity group, hello function ignores it.</span></span> <span data-ttu-id="1170c-243">Należy określić lokalizację i grupę koligacji.</span><span class="sxs-lookup"><span data-stu-id="1170c-243">You must specify either a location or an affinity group.</span></span> |
| <span data-ttu-id="1170c-244">Get-MSDeployCmd</span><span class="sxs-lookup"><span data-stu-id="1170c-244">Get-MSDeployCmd</span></span> |<span data-ttu-id="1170c-245">Zwraca narzędzie MsDeploy.exe hello toorun polecenia.</span><span class="sxs-lookup"><span data-stu-id="1170c-245">Returns a command toorun hello MsDeploy.exe tool.</span></span> |
| <span data-ttu-id="1170c-246">Nowe AzureVMEnvironment</span><span class="sxs-lookup"><span data-stu-id="1170c-246">New-AzureVMEnvironment</span></span> |<span data-ttu-id="1170c-247">Wyszukuje lub tworzy maszynę wirtualną w hello subskrypcji, która odpowiada wartości hello w pliku konfiguracji JSON hello.</span><span class="sxs-lookup"><span data-stu-id="1170c-247">Finds or creates a virtual machine in hello subscription that matches hello values in hello JSON configuration file.</span></span> |
| <span data-ttu-id="1170c-248">Publikowanie WebPackage</span><span class="sxs-lookup"><span data-stu-id="1170c-248">Publish-WebPackage</span></span> |<span data-ttu-id="1170c-249">Używa MsDeploy.exe i sieci web publikowania pakietu. ZIP pliku toodeploy zasobów tooa witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="1170c-249">Uses MsDeploy.exe and a web publish package .Zip file toodeploy resources tooa website.</span></span> <span data-ttu-id="1170c-250">Ta funkcja nie generuje żadnego wyniku.</span><span class="sxs-lookup"><span data-stu-id="1170c-250">This function doesn't generate any output.</span></span> <span data-ttu-id="1170c-251">W przypadku niepowodzenia hello tooMSDeploy.exe wywołanie funkcji hello zgłasza wyjątek.</span><span class="sxs-lookup"><span data-stu-id="1170c-251">If hello call tooMSDeploy.exe fails, hello function throws an exception.</span></span> <span data-ttu-id="1170c-252">tooget bardziej szczegółowe dane wyjściowe, użyj hello **-Verbose** opcji.</span><span class="sxs-lookup"><span data-stu-id="1170c-252">tooget more detailed output, use hello **-Verbose** option.</span></span> |
| <span data-ttu-id="1170c-253">Publikowanie WebPackageToVM</span><span class="sxs-lookup"><span data-stu-id="1170c-253">Publish-WebPackageToVM</span></span> |<span data-ttu-id="1170c-254">Sprawdza, czy hello wartości parametrów, a następnie wywołuje hello **WebPackage publikowania** funkcji.</span><span class="sxs-lookup"><span data-stu-id="1170c-254">Verifies hello parameter values, and then calls hello **Publish-WebPackage** function.</span></span> |
| <span data-ttu-id="1170c-255">ConfigFile odczytu</span><span class="sxs-lookup"><span data-stu-id="1170c-255">Read-ConfigFile</span></span> |<span data-ttu-id="1170c-256">Sprawdza poprawność pliku konfiguracji JSON hello i zwraca tablicy skrótów, wybranych wartości.</span><span class="sxs-lookup"><span data-stu-id="1170c-256">Validates hello JSON configuration file and returns a hash table of selected values.</span></span> |
| <span data-ttu-id="1170c-257">Przywracanie subskrypcji</span><span class="sxs-lookup"><span data-stu-id="1170c-257">Restore-Subscription</span></span> |<span data-ttu-id="1170c-258">Resetuje hello bieżącej subskrypcji toohello oryginalnego subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="1170c-258">Resets hello current subscription toohello original subscription.</span></span> |
| <span data-ttu-id="1170c-259">AzureModule testu</span><span class="sxs-lookup"><span data-stu-id="1170c-259">Test-AzureModule</span></span> |<span data-ttu-id="1170c-260">Zwraca `$true` w przypadku wersji modułu Azure hello zainstalowany 0.7.4 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="1170c-260">Returns `$true` if hello installed Azure module version is 0.7.4 or later.</span></span> <span data-ttu-id="1170c-261">Zwraca `$false` hello modułu nie jest zainstalowany lub jest starsza wersja.</span><span class="sxs-lookup"><span data-stu-id="1170c-261">Returns `$false` if hello module isn't installed or is an earlier version.</span></span> <span data-ttu-id="1170c-262">Ta funkcja nie ma parametrów.</span><span class="sxs-lookup"><span data-stu-id="1170c-262">This function has no parameters.</span></span> |
| <span data-ttu-id="1170c-263">AzureModuleVersion testu</span><span class="sxs-lookup"><span data-stu-id="1170c-263">Test-AzureModuleVersion</span></span> |<span data-ttu-id="1170c-264">Zwraca `$true` Jeśli wersja hello hello Azure modułu jest 0.7.4 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="1170c-264">Returns `$true` if hello version of hello Azure module is 0.7.4 or later.</span></span> <span data-ttu-id="1170c-265">Zwraca `$false` hello modułu nie jest zainstalowany lub jest starsza wersja.</span><span class="sxs-lookup"><span data-stu-id="1170c-265">Returns `$false` if hello module isn't installed or is an earlier version.</span></span> <span data-ttu-id="1170c-266">Ta funkcja nie ma parametrów.</span><span class="sxs-lookup"><span data-stu-id="1170c-266">This function has no parameters.</span></span> |
| <span data-ttu-id="1170c-267">HttpsUrl testu</span><span class="sxs-lookup"><span data-stu-id="1170c-267">Test-HttpsUrl</span></span> |<span data-ttu-id="1170c-268">Konwertuje obiekt System.Uri tooa wejściowy adres URL hello.</span><span class="sxs-lookup"><span data-stu-id="1170c-268">Converts hello input URL tooa System.Uri object.</span></span> <span data-ttu-id="1170c-269">Zwraca `$True` Jeśli bezwzględny adres URL hello i jego schemat jest typu https.</span><span class="sxs-lookup"><span data-stu-id="1170c-269">Returns `$True` if hello URL is absolute and its scheme is https.</span></span> <span data-ttu-id="1170c-270">Zwraca `$false` hello adres URL jest względny, jego schematu nie HTTPS, czy hello ciąg wejściowy nie może być przekonwertowany tooa adresu URL.</span><span class="sxs-lookup"><span data-stu-id="1170c-270">Returns `$false` if hello URL is relative, its scheme isn't HTTPS, or hello input string can't be converted tooa URL.</span></span> |
| <span data-ttu-id="1170c-271">Element członkowski testu</span><span class="sxs-lookup"><span data-stu-id="1170c-271">Test-Member</span></span> |<span data-ttu-id="1170c-272">Zwraca `$true` Jeśli właściwość lub metoda jest elementem członkowskim obiektu hello.</span><span class="sxs-lookup"><span data-stu-id="1170c-272">Returns `$true` if a property or method is a member of hello object.</span></span> <span data-ttu-id="1170c-273">W przeciwnym razie zwraca `$false`.</span><span class="sxs-lookup"><span data-stu-id="1170c-273">Otherwise, returns `$false`.</span></span> |
| <span data-ttu-id="1170c-274">ErrorWithTime zapisu</span><span class="sxs-lookup"><span data-stu-id="1170c-274">Write-ErrorWithTime</span></span> |<span data-ttu-id="1170c-275">Zapisuje komunikat o błędzie z prefiksem hello bieżącego czasu.</span><span class="sxs-lookup"><span data-stu-id="1170c-275">Writes an error message prefixed with hello current time.</span></span> <span data-ttu-id="1170c-276">Ta funkcja wymaga hello **Format DevTestMessageWithTime** funkcja tooprepend hello czasu przed zapisaniem strumień błędów toohello wiadomość hello.</span><span class="sxs-lookup"><span data-stu-id="1170c-276">This function calls hello **Format-DevTestMessageWithTime** function tooprepend hello time before writing hello message toohello Error stream.</span></span> |
| <span data-ttu-id="1170c-277">HostWithTime zapisu</span><span class="sxs-lookup"><span data-stu-id="1170c-277">Write-HostWithTime</span></span> |<span data-ttu-id="1170c-278">Zapisuje komunikat toohello hosta programu (**Write-Host**) i jest poprzedzony prefiksem hello bieżący czas.</span><span class="sxs-lookup"><span data-stu-id="1170c-278">Writes a message toohello host program (**Write-Host**) prefixed with hello current time.</span></span> <span data-ttu-id="1170c-279">efekt Hello zapisywania toohello hosta programu może być różna.</span><span class="sxs-lookup"><span data-stu-id="1170c-279">hello effect of writing toohello host program varies.</span></span> <span data-ttu-id="1170c-280">Większość programów obsługujących środowiska Windows PowerShell zapisu te komunikaty toostandard danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="1170c-280">Most programs that host Windows PowerShell write these messages toostandard output.</span></span> |
| <span data-ttu-id="1170c-281">VerboseWithTime zapisu</span><span class="sxs-lookup"><span data-stu-id="1170c-281">Write-VerboseWithTime</span></span> |<span data-ttu-id="1170c-282">Zapisuje komunikat trybu informacji pełnej prefiksem hello bieżącego czasu.</span><span class="sxs-lookup"><span data-stu-id="1170c-282">Writes a verbose message prefixed with hello current time.</span></span> <span data-ttu-id="1170c-283">Ponieważ wywołuje **Write-Verbose**, wiadomość hello wyświetla tylko, gdy hello skrypt jest uruchamiany z hello **pełne** parametru lub gdy hello **VerbosePreference** jest preferencji Ustaw zbyt**Kontynuuj**.</span><span class="sxs-lookup"><span data-stu-id="1170c-283">Because it calls **Write-Verbose**, hello message displays only when hello script runs with hello **Verbose** parameter or when hello **VerbosePreference** preference is set too**Continue**.</span></span> |

<span data-ttu-id="1170c-284">**Publikowanie aplikacji sieci Web**</span><span class="sxs-lookup"><span data-stu-id="1170c-284">**Publish-WebApplication**</span></span>

| <span data-ttu-id="1170c-285">Nazwa funkcji</span><span class="sxs-lookup"><span data-stu-id="1170c-285">Function name</span></span> | <span data-ttu-id="1170c-286">Opis</span><span class="sxs-lookup"><span data-stu-id="1170c-286">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1170c-287">Nowe AzureWebApplicationEnvironment</span><span class="sxs-lookup"><span data-stu-id="1170c-287">New-AzureWebApplicationEnvironment</span></span> |<span data-ttu-id="1170c-288">Tworzy zasobów platformy Azure, takich jak witryny sieci Web lub maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1170c-288">Creates Azure resources, such as a website or virtual machine.</span></span> |
| <span data-ttu-id="1170c-289">Nowe WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="1170c-289">New-WebDeployPackage</span></span> |<span data-ttu-id="1170c-290">Ta funkcja nie jest zaimplementowana.</span><span class="sxs-lookup"><span data-stu-id="1170c-290">This function isn't implemented.</span></span> <span data-ttu-id="1170c-291">Można dodać polecenia w tej funkcji toobuild projektu.</span><span class="sxs-lookup"><span data-stu-id="1170c-291">You can add commands in this function toobuild your project.</span></span> |
| <span data-ttu-id="1170c-292">Publikowanie AzureWebApplication</span><span class="sxs-lookup"><span data-stu-id="1170c-292">Publish-AzureWebApplication</span></span> |<span data-ttu-id="1170c-293">Publikuje tooAzure aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="1170c-293">Publishes a web application tooAzure.</span></span> |
| <span data-ttu-id="1170c-294">Publikowanie aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="1170c-294">Publish-WebApplication</span></span> |<span data-ttu-id="1170c-295">Tworzy i wdraża aplikacje sieci Web, maszyn wirtualnych, baz danych i konta magazynu dla projektu sieci web programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1170c-295">Creates and deploys Web Apps, virtual machines, SQL databases, and storage accounts for a Visual Studio web project.</span></span> |
| <span data-ttu-id="1170c-296">Test-WebApplication</span><span class="sxs-lookup"><span data-stu-id="1170c-296">Test-WebApplication</span></span> |<span data-ttu-id="1170c-297">Ta funkcja nie jest zaimplementowana.</span><span class="sxs-lookup"><span data-stu-id="1170c-297">This function isn't implemented.</span></span> <span data-ttu-id="1170c-298">Można dodać polecenia w tym tootest funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1170c-298">You can add commands in this function tootest your application.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1170c-299">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1170c-299">Next steps</span></span>
<span data-ttu-id="1170c-300">Dowiedz się więcej na temat skryptów środowiska PowerShell, odczytując [skryptów programu Windows PowerShell](https://technet.microsoft.com/library/bb978526.aspx) zobaczyć inne skrypty programu PowerShell systemu Azure w hello [Centrum skryptów](https://azure.microsoft.com/documentation/scripts/).</span><span class="sxs-lookup"><span data-stu-id="1170c-300">Learn more about PowerShell scripting by reading [Scripting with Windows PowerShell](https://technet.microsoft.com/library/bb978526.aspx) and see other Azure PowerShell scripts at hello [Script Center](https://azure.microsoft.com/documentation/scripts/).</span></span>
