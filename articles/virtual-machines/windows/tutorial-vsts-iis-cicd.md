---
title: "aaaCreate potok CI/CD w platformie Azure za pomocą usługi Team Services | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate Visual Studio Team Services potoku dla ciągłej integracji i dostarczania, która wdraża tooIIS aplikacji sieci web, na maszynie Wirtualnej systemu Windows"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: b758a124c4742854dd3b543f747fd8700f954414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-continuous-integration-pipeline-with-visual-studio-team-services-and-iis"></a><span data-ttu-id="5018f-103">Tworzenie potoku ciągłej integracji z Visual Studio Team Services i IIS</span><span class="sxs-lookup"><span data-stu-id="5018f-103">Create a continuous integration pipeline with Visual Studio Team Services and IIS</span></span>
<span data-ttu-id="5018f-104">tooautomate hello kompilację, testów i wdrożenia etapy tworzenia aplikacji, można użyć ciągłej integracji i wdrażania (CI/CD) potoku.</span><span class="sxs-lookup"><span data-stu-id="5018f-104">tooautomate hello build, test, and deployment phases of application development, you can use a continuous integration and deployment (CI/CD) pipeline.</span></span> <span data-ttu-id="5018f-105">W tym samouczku utworzysz potok CI/CD przy użyciu programu Visual Studio Team Services i Windows maszyny wirtualnej (VM) na platformie Azure z uruchomionymi usługami IIS.</span><span class="sxs-lookup"><span data-stu-id="5018f-105">In this tutorial, you create a CI/CD pipeline using Visual Studio Team Services and a Windows virtual machine (VM) in Azure that runs IIS.</span></span> <span data-ttu-id="5018f-106">Omawiane kwestie:</span><span class="sxs-lookup"><span data-stu-id="5018f-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5018f-107">Publikuj projekt usługi Team Services tooa aplikacji sieci web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="5018f-107">Publish an ASP.NET web application tooa Team Services project</span></span>
> * <span data-ttu-id="5018f-108">Tworzenie definicji kompilacji, która jest wyzwalany przez kod zatwierdzenia</span><span class="sxs-lookup"><span data-stu-id="5018f-108">Create a build definition that is triggered by code commits</span></span>
> * <span data-ttu-id="5018f-109">Instalowanie i konfigurowanie usług IIS na maszynie wirtualnej na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="5018f-109">Install and configure IIS on a virtual machine in Azure</span></span>
> * <span data-ttu-id="5018f-110">Dodaj grupę wdrożenia tooa wystąpienia usług IIS hello w Team Services</span><span class="sxs-lookup"><span data-stu-id="5018f-110">Add hello IIS instance tooa deployment group in Team Services</span></span>
> * <span data-ttu-id="5018f-111">Utwórz nową web toopublish definicji wersji tooIIS pakiety wdrażania</span><span class="sxs-lookup"><span data-stu-id="5018f-111">Create a release definition toopublish new web deploy packages tooIIS</span></span>
> * <span data-ttu-id="5018f-112">Test hello CI/CD potoku</span><span class="sxs-lookup"><span data-stu-id="5018f-112">Test hello CI/CD pipeline</span></span>

<span data-ttu-id="5018f-113">Ten samouczek wymaga hello Azure PowerShell w wersji modułu 3,6 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="5018f-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="5018f-114">Uruchom `Get-Module -ListAvailable AzureRM` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="5018f-114">Run `Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="5018f-115">Jeśli potrzebujesz tooupgrade, zobacz [modułu instalacji programu Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="5018f-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="create-project-in-team-services"></a><span data-ttu-id="5018f-116">Tworzenie projektu na Team Services</span><span class="sxs-lookup"><span data-stu-id="5018f-116">Create project in Team Services</span></span>
<span data-ttu-id="5018f-117">Visual Studio Team Services umożliwia łatwe współpracy i rozwoju bez zachowania to rozwiązanie do zarządzania lokalnymi kodu.</span><span class="sxs-lookup"><span data-stu-id="5018f-117">Visual Studio Team Services allows for easy collaboration and development without maintaining an on-premises code management solution.</span></span> <span data-ttu-id="5018f-118">Usługi Team Services zapewnia testowania kodu w chmurze, kompilacji i usługi application insights.</span><span class="sxs-lookup"><span data-stu-id="5018f-118">Team Services provides cloud code testing, build, and application insights.</span></span> <span data-ttu-id="5018f-119">Można wybrać repozytorium kontroli wersji i IDE, która najlepiej pasuje do programowania kodu.</span><span class="sxs-lookup"><span data-stu-id="5018f-119">You can choose a version control repo and IDE that best fits your code development.</span></span> <span data-ttu-id="5018f-120">W tym samouczku można użyć bezpłatnego konta toocreate Podstawowa aplikacja sieci web ASP.NET i CI/CD potoku.</span><span class="sxs-lookup"><span data-stu-id="5018f-120">For this tutorial, you can use a free account toocreate a basic ASP.NET web app and CI/CD pipeline.</span></span> <span data-ttu-id="5018f-121">Jeśli nie masz już konto usługi Team Services [utworzyć](http://go.microsoft.com/fwlink/?LinkId=307137).</span><span class="sxs-lookup"><span data-stu-id="5018f-121">If you do not already have a Team Services account, [create one](http://go.microsoft.com/fwlink/?LinkId=307137).</span></span>

<span data-ttu-id="5018f-122">toomanage hello kod proces, definicje, kompilacji i wydania definicje, tworzenie projektu na Team Services w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="5018f-122">toomanage hello code commit process, build definitions, and release definitions, create a project in Team Services as follows:</span></span>

1. <span data-ttu-id="5018f-123">Otwórz pulpit nawigacyjny usługi Team Services w przeglądarce sieci web i wybierz polecenie **nowy projekt**.</span><span class="sxs-lookup"><span data-stu-id="5018f-123">Open your Team Services dashboard in a web browser and choose **New project**.</span></span>
2. <span data-ttu-id="5018f-124">Wprowadź *myWebApp* dla hello **Nazwa projektu**.</span><span class="sxs-lookup"><span data-stu-id="5018f-124">Enter *myWebApp* for hello **Project name**.</span></span> <span data-ttu-id="5018f-125">Pozostaw wszystkie inne toouse wartości domyślne *Git* kontroli wersji i *Agile* elementów roboczych procesu.</span><span class="sxs-lookup"><span data-stu-id="5018f-125">Leave all other default values toouse *Git* version control and *Agile* work item process.</span></span>
3. <span data-ttu-id="5018f-126">Wybierz opcję hello zbyt**udostępniać** *członków zespołu*, a następnie wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="5018f-126">Choose hello option too**Share with** *Team Members*, then select **Create**.</span></span>
5. <span data-ttu-id="5018f-127">Po utworzeniu projektu, wybierz opcję hello zbyt**zainicjować README lub gitignore**, następnie **zainicjować**.</span><span class="sxs-lookup"><span data-stu-id="5018f-127">Once your project has been created, choose hello option too**Initialize with a README or gitignore**, then **Initialize**.</span></span>
6. <span data-ttu-id="5018f-128">Wewnątrz nowego projektu, wybierz **pulpity nawigacyjne** górze hello, następnie wybierz **Otwórz w programie Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="5018f-128">Inside your new project, choose **Dashboards** across hello top, then select **Open in Visual Studio**.</span></span>


## <a name="create-aspnet-web-application"></a><span data-ttu-id="5018f-129">Tworzenie aplikacji sieci web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="5018f-129">Create ASP.NET web application</span></span>
<span data-ttu-id="5018f-130">W poprzednim kroku hello utworzonego projektu w Team Services.</span><span class="sxs-lookup"><span data-stu-id="5018f-130">In hello previous step, you created a project in Team Services.</span></span> <span data-ttu-id="5018f-131">Ostatnim krokiem Hello zostanie otwarty nowy projekt w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5018f-131">hello final step opens your new project in Visual Studio.</span></span> <span data-ttu-id="5018f-132">Zarządzanie zatwierdzenia kodu w hello **Team Explorer** okna.</span><span class="sxs-lookup"><span data-stu-id="5018f-132">You manage your code commits in hello **Team Explorer** window.</span></span> <span data-ttu-id="5018f-133">Utwórz lokalną kopię nowego projektu, a następnie utworzyć aplikację sieci web platformy ASP.NET na podstawie szablonu w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="5018f-133">Create a local copy of your new project, then create an ASP.NET web application from a template as follows:</span></span>

1. <span data-ttu-id="5018f-134">Wybierz **klonowania** toocreate repozytorium git lokalnego projektu Team Services.</span><span class="sxs-lookup"><span data-stu-id="5018f-134">Select **Clone** toocreate a local git repo of your Team Services project.</span></span>
    
    ![Klonowanie repozytorium z projektu Team Services](media/tutorial-vsts-iis-cicd/clone_repo.png)

2. <span data-ttu-id="5018f-136">W obszarze **rozwiązań**, wybierz pozycję **nowy**.</span><span class="sxs-lookup"><span data-stu-id="5018f-136">Under **Solutions**, select **New**.</span></span>

    ![Utwórz rozwiązanie aplikacji sieci web](media/tutorial-vsts-iis-cicd/new_solution.png)

3. <span data-ttu-id="5018f-138">Wybierz **sieci Web** szablonów, a następnie wybierz pozycję hello **aplikacji sieci Web ASP.NET** szablonu.</span><span class="sxs-lookup"><span data-stu-id="5018f-138">Select **Web** templates, and then choose hello **ASP.NET Web Application** template.</span></span>
    1. <span data-ttu-id="5018f-139">Wprowadź nazwę aplikacji, takich jak *myWebApp*i usuń zaznaczenie pola hello **Utwórz katalog rozwiązania**.</span><span class="sxs-lookup"><span data-stu-id="5018f-139">Enter a name for your application, such as *myWebApp*, and uncheck hello box for **Create directory for solution**.</span></span>
    2. <span data-ttu-id="5018f-140">Jeśli jest dostępna opcja hello, hello Usuń zaznaczenie pola wyboru zbyt**tooproject Dodaj usługę Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="5018f-140">If hello option is available, uncheck hello box too**Add Application Insights tooproject**.</span></span> <span data-ttu-id="5018f-141">Usługa Application Insights wymaga tooauthorize użytkownik aplikacji sieci web z usługą Azure Application Insights.</span><span class="sxs-lookup"><span data-stu-id="5018f-141">Application Insights requires you tooauthorize your web application with Azure Application Insights.</span></span> <span data-ttu-id="5018f-142">tookeep prostotę, w tym samouczku, Pomiń ten proces.</span><span class="sxs-lookup"><span data-stu-id="5018f-142">tookeep it simple in this tutorial, skip this process.</span></span>
    3. <span data-ttu-id="5018f-143">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="5018f-143">Select **OK**.</span></span>
4. <span data-ttu-id="5018f-144">Wybierz **MVC** z listy szablonów hello.</span><span class="sxs-lookup"><span data-stu-id="5018f-144">Choose **MVC** from hello template list.</span></span>
    1. <span data-ttu-id="5018f-145">Wybierz **Zmień uwierzytelnianie**, wybierz **bez uwierzytelniania**, a następnie wybierz pozycję **OK**.</span><span class="sxs-lookup"><span data-stu-id="5018f-145">Select **Change Authentication**, choose **No Authentication**, then select **OK**.</span></span>
    2. <span data-ttu-id="5018f-146">Wybierz **OK** toocreate rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="5018f-146">Select **OK** toocreate your solution.</span></span>
5. <span data-ttu-id="5018f-147">W hello **Team Explorer** okna, wybierz **zmiany**.</span><span class="sxs-lookup"><span data-stu-id="5018f-147">In hello **Team Explorer** window, choose **Changes**.</span></span>

    ![Zatwierdź repozytorium git usługi tooTeam lokalne zmiany](media/tutorial-vsts-iis-cicd/commit_changes.png)

6. <span data-ttu-id="5018f-149">W polu tekstowym zatwierdzania hello, wpisz wiadomość, takich jak *zatwierdzania początkowego*.</span><span class="sxs-lookup"><span data-stu-id="5018f-149">In hello commit text box, enter a message such as *Initial commit*.</span></span> <span data-ttu-id="5018f-150">Wybierz **zatwierdzić wszystkie i synchronizacji** z menu rozwijanego hello.</span><span class="sxs-lookup"><span data-stu-id="5018f-150">Choose **Commit All and Sync** from hello drop-down menu.</span></span>


## <a name="create-build-definition"></a><span data-ttu-id="5018f-151">Tworzenie definicji kompilacji</span><span class="sxs-lookup"><span data-stu-id="5018f-151">Create build definition</span></span>
<span data-ttu-id="5018f-152">W Team Services należy użyć toooutline definicji kompilacji, jak powinny zostać skompilowane aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5018f-152">In Team Services, you use a build definition toooutline how your application should be built.</span></span> <span data-ttu-id="5018f-153">W tym samouczku utworzymy podstawową definicję przyjmuje naszego kodu źródłowego buduje rozwiązanie hello, a następnie tworzy sieci web do wdrożenia pakietu aplikacji sieci web hello toorun możemy użyć na serwerze IIS.</span><span class="sxs-lookup"><span data-stu-id="5018f-153">In this tutorial, we create a basic definition that takes our source code, builds hello solution, then creates web deploy package we can use toorun hello web app on an IIS server.</span></span>

1. <span data-ttu-id="5018f-154">W projekcie usługi Team Services, wybierz **kompilacji i wydania** górze hello, następnie wybierz **kompilacje**.</span><span class="sxs-lookup"><span data-stu-id="5018f-154">In your Team Services project, choose **Build & Release** across hello top, then select **Builds**.</span></span>
3. <span data-ttu-id="5018f-155">Wybierz **+ nową definicję**.</span><span class="sxs-lookup"><span data-stu-id="5018f-155">Select **+ New definition**.</span></span>
4. <span data-ttu-id="5018f-156">Wybierz hello **ASP.NET (wersja ZAPOZNAWCZA)** szablonu, a następnie wybierz **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="5018f-156">Choose hello **ASP.NET (PREVIEW)** template and select **Apply**.</span></span>
5. <span data-ttu-id="5018f-157">Pozostaw wszystkie domyślne hello wartości zadania.</span><span class="sxs-lookup"><span data-stu-id="5018f-157">Leave all hello default task values.</span></span> <span data-ttu-id="5018f-158">W obszarze **Pobierz źródła**, upewnij się, że hello *myWebApp* repozytorium i *wzorca* są zaznaczone oddziału.</span><span class="sxs-lookup"><span data-stu-id="5018f-158">Under **Get sources**, ensure that hello *myWebApp* repository and *master* branch are selected.</span></span>

    ![Utwórz definicję kompilacji w projekcie usługi Team Services](media/tutorial-vsts-iis-cicd/create_build_definition.png)

6. <span data-ttu-id="5018f-160">Na powitania **wyzwalaczy** karcie, przesuń suwak hello **włączyć tego wyzwalacza** za*włączone*.</span><span class="sxs-lookup"><span data-stu-id="5018f-160">On hello **Triggers** tab, move hello slider for **Enable this trigger** too*Enabled*.</span></span>
7. <span data-ttu-id="5018f-161">Zapisz definicję kompilacji hello i kolejki nowej kompilacji, wybierając **Zapisz & kolejka** , następnie **Zapisz & kolejka** ponownie.</span><span class="sxs-lookup"><span data-stu-id="5018f-161">Save hello build definition and queue a new build by selecting **Save & queue** , then **Save & queue** again.</span></span> <span data-ttu-id="5018f-162">Pozostaw wartości domyślne hello i wybierz **kolejki**.</span><span class="sxs-lookup"><span data-stu-id="5018f-162">Leave hello defaults and select **Queue**.</span></span>

<span data-ttu-id="5018f-163">Obejrzyj jako kompilacji hello jest zaplanowane na agencie hostowanej, następnie rozpoczyna toobuild.</span><span class="sxs-lookup"><span data-stu-id="5018f-163">Watch as hello build is scheduled on a hosted agent, then begins toobuild.</span></span> <span data-ttu-id="5018f-164">Witaj danych wyjściowych jest toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="5018f-164">hello output is similar toohello following example:</span></span>

![Pomyślnie kompilacji projektu Team Services](media/tutorial-vsts-iis-cicd/successful_build.png)


## <a name="create-virtual-machine"></a><span data-ttu-id="5018f-166">Tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="5018f-166">Create virtual machine</span></span>
<span data-ttu-id="5018f-167">tooprovide toorun platforma aplikacji sieci web ASP.NET, należy maszyny wirtualnej systemu Windows z uruchomionymi usługami IIS.</span><span class="sxs-lookup"><span data-stu-id="5018f-167">tooprovide a platform toorun your ASP.NET web app, you need a Windows virtual machine that runs IIS.</span></span> <span data-ttu-id="5018f-168">Usługi Team Services używa toointeract agenta z wystąpieniem usług IIS hello zatwierdzisz kod i kompilacje są wyzwalane.</span><span class="sxs-lookup"><span data-stu-id="5018f-168">Team Services uses an agent toointeract with hello IIS instance as you commit code and builds are triggered.</span></span>

<span data-ttu-id="5018f-169">Tworzenie maszyny Wirtualnej systemu Windows Server 2016 przy użyciu [w tym przykładzie skrypt](../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5018f-169">Create a Windows Server 2016 VM using [this script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json).</span></span> <span data-ttu-id="5018f-170">Go zajmuje kilka minut dla hello skryptu toorun i Utwórz hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5018f-170">It takes a few minutes for hello script toorun and create hello VM.</span></span> <span data-ttu-id="5018f-171">Po utworzeniu hello maszyny Wirtualnej, należy otworzyć port 80 dla ruchu w sieci web z [AzureRmNetworkSecurityRuleConfig Dodaj](/powershell/module/azurerm.resources/new-azurermresourcegroup) w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="5018f-171">Once hello VM has been created, open port 80 for web traffic with [Add-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.resources/new-azurermresourcegroup) as follows:</span></span>

```powershell
Get-AzureRmNetworkSecurityGroup `
  -ResourceGroupName $resourceGroup `
  -Name "myNetworkSecurityGroup" | `
Add-AzureRmNetworkSecurityRuleConfig `
  -Name "myNetworkSecurityGroupRuleWeb" `
  -Protocol "Tcp" `
  -Direction "Inbound" `
  -Priority "1001" `
  -SourceAddressPrefix "*" `
  -SourcePortRange "*" `
  -DestinationAddressPrefix "*" `
  -DestinationPortRange "80" `
  -Access "Allow" | `
Set-AzureRmNetworkSecurityGroup
```

<span data-ttu-id="5018f-172">tooyour tooconnect maszyny Wirtualnej, Uzyskaj hello publicznego adresu IP z [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="5018f-172">tooconnect tooyour VM, obtain hello public IP address with [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) as follows:</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName $resourceGroup | Select IpAddress
```

<span data-ttu-id="5018f-173">Tworzenie sesji usług pulpitu zdalnego tooyour maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="5018f-173">Create a remote desktop session tooyour VM:</span></span>

```cmd
mstsc /v:<publicIpAddress>
```

<span data-ttu-id="5018f-174">Na powitania maszyny Wirtualnej, otwórz **administratora programu PowerShell** wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="5018f-174">On hello VM, open an **Administrator PowerShell** command prompt.</span></span> <span data-ttu-id="5018f-175">Zainstaluj usługi IIS i wymagane funkcje platformy .NET:</span><span class="sxs-lookup"><span data-stu-id="5018f-175">Install IIS and required .NET features as follows:</span></span>

```powershell
Install-WindowsFeature Web-Server,Web-Asp-Net45,NET-Framework-Features
```


## <a name="create-deployment-group"></a><span data-ttu-id="5018f-176">Utwórz grupę wdrożenia</span><span class="sxs-lookup"><span data-stu-id="5018f-176">Create deployment group</span></span>
<span data-ttu-id="5018f-177">toopush limit hello web wdrażanie serwera IIS toohello pakietu, zdefiniuj grupę wdrożenia w Team Services.</span><span class="sxs-lookup"><span data-stu-id="5018f-177">toopush out hello web deploy package toohello IIS server, you define a deployment group in Team Services.</span></span> <span data-ttu-id="5018f-178">Ta grupa umożliwia toospecify serwerów, które są hello docelowy nowych kompilacji, jak zatwierdzić tooTeam kodu usługi i kompilacji zostały zakończone.</span><span class="sxs-lookup"><span data-stu-id="5018f-178">This group allows you toospecify which servers are hello target of new builds as you commit code tooTeam Services and builds are completed.</span></span>

1. <span data-ttu-id="5018f-179">W usłudze Team Services, wybierz **kompilacji i wydania** , a następnie wybierz **grupy wdrożenia**.</span><span class="sxs-lookup"><span data-stu-id="5018f-179">In Team Services, choose **Build & Release** and then select **Deployment groups**.</span></span>
2. <span data-ttu-id="5018f-180">Wybierz **Dodaj wdrożenie grupy**.</span><span class="sxs-lookup"><span data-stu-id="5018f-180">Choose **Add Deployment group**.</span></span>
3. <span data-ttu-id="5018f-181">Wprowadź nazwę grupy hello, takich jak *Mój_iis*, a następnie wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="5018f-181">Enter a name for hello group, such as *myIIS*, then select **Create**.</span></span>
4. <span data-ttu-id="5018f-182">W hello **rejestrowania maszyn** upewnij się, *Windows* jest zaznaczone, a następnie zaznacz pole hello zbyt**używania osobisty token dostępu w skrypcie hello w celu uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="5018f-182">In hello **Register machines** section, ensure *Windows* is selected, then check hello box too**Use a personal access token in hello script for authentication**.</span></span>
5. <span data-ttu-id="5018f-183">Wybierz **Skopiuj skrypt tooclipboard**.</span><span class="sxs-lookup"><span data-stu-id="5018f-183">Select **Copy script tooclipboard**.</span></span>


### <a name="add-iis-vm-toohello-deployment-group"></a><span data-ttu-id="5018f-184">Dodaj grupę wdrożenia toohello maszyn wirtualnych usług IIS</span><span class="sxs-lookup"><span data-stu-id="5018f-184">Add IIS VM toohello deployment group</span></span>
<span data-ttu-id="5018f-185">Witaj utworzoną grupę wdrożenia dodawać każdej grupy toohello wystąpienia usług IIS.</span><span class="sxs-lookup"><span data-stu-id="5018f-185">With hello deployment group created, add each IIS instance toohello group.</span></span> <span data-ttu-id="5018f-186">Usługi Team Services generuje skrypt, który pobiera i konfiguruje agenta na powitania wdrożyć maszynę Wirtualną, która odbiera nowej sieci web pakiety, a następnie stosuje je tooIIS.</span><span class="sxs-lookup"><span data-stu-id="5018f-186">Team Services generates a script that downloads and configures an agent on hello VM that receives new web deploy packages then applies it tooIIS.</span></span>

1. <span data-ttu-id="5018f-187">Po powrocie do hello **administratora programu PowerShell** sesji na maszynie Wirtualnej, Wklej i uruchom skrypt hello skopiowanych z usługi Team Services.</span><span class="sxs-lookup"><span data-stu-id="5018f-187">Back in hello **Administrator PowerShell** session on your VM, paste and run hello script copied from Team Services.</span></span>
2. <span data-ttu-id="5018f-188">Gdy zostanie wyświetlony monit o tooconfigure tagi dla agenta hello wybierz *Y* , a następnie wprowadź *web*.</span><span class="sxs-lookup"><span data-stu-id="5018f-188">When prompted tooconfigure tags for hello agent, choose *Y* and enter *web*.</span></span>
3. <span data-ttu-id="5018f-189">Po wyświetleniu monitu dla konta użytkownika hello, naciśnij klawisz *zwracać* tooaccept hello domyślne.</span><span class="sxs-lookup"><span data-stu-id="5018f-189">When prompted for hello user account, press *Return* tooaccept hello defaults.</span></span>
4. <span data-ttu-id="5018f-190">Poczekaj, aż hello toofinish skryptu z następującym komunikatem *vstsagent.account.computername usługa została uruchomiona pomyślnie*.</span><span class="sxs-lookup"><span data-stu-id="5018f-190">Wait for hello script toofinish with a message *Service vstsagent.account.computername started successfully*.</span></span>
5. <span data-ttu-id="5018f-191">W hello **grupy wdrożenia** strony hello **kompilacji i wydania** menu, otwórz hello *Mój_iis* grupę wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="5018f-191">In hello **Deployment groups** page of hello **Build & Release** menu, open hello *myIIS* deployment group.</span></span> <span data-ttu-id="5018f-192">Na powitania **maszyny** karcie, sprawdź, czy maszyna wirtualna jest wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="5018f-192">On hello **Machines** tab, verify that your VM is listed.</span></span>

    ![Maszyna wirtualna pomyślnie dodano grupę wdrożenia usług tooTeam](media/tutorial-vsts-iis-cicd/deployment_group.png)


## <a name="create-release-definition"></a><span data-ttu-id="5018f-194">Utwórz definicję zlecenia</span><span class="sxs-lookup"><span data-stu-id="5018f-194">Create release definition</span></span>
<span data-ttu-id="5018f-195">toopublish kompilacji, możesz utworzyć definicję wersji w Team Services.</span><span class="sxs-lookup"><span data-stu-id="5018f-195">toopublish your builds, you create a release definition in Team Services.</span></span> <span data-ttu-id="5018f-196">Ta definicja jest automatycznie wyzwalane przez to pomyślnego utworzenia kompilacji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5018f-196">This definition is triggered automatically by a successful build of your application.</span></span> <span data-ttu-id="5018f-197">Wybierz toopush grupy wdrożenia hello pakiet do wdrożenia sieci web, a następnie zdefiniuj hello odpowiednie ustawienia usług IIS.</span><span class="sxs-lookup"><span data-stu-id="5018f-197">You choose hello deployment group toopush your web deploy package to, and define hello appropriate IIS settings.</span></span>

1. <span data-ttu-id="5018f-198">Wybierz **kompilacji i wydania**, a następnie wybierz pozycję **kompilacje**.</span><span class="sxs-lookup"><span data-stu-id="5018f-198">Choose **Build & Release**, then select **Builds**.</span></span> <span data-ttu-id="5018f-199">Wybierz definicję kompilacji hello utworzony w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="5018f-199">Choose hello build definition created in a previous step.</span></span>
2. <span data-ttu-id="5018f-200">W obszarze **niedawno ukończoną**, wybierz hello ostatniej kompilacji, a następnie wybierz **wersji**.</span><span class="sxs-lookup"><span data-stu-id="5018f-200">Under **Recently completed**, choose hello most recent build, then select **Release**.</span></span>
3. <span data-ttu-id="5018f-201">Wybierz **tak** toocreate definicji wersji.</span><span class="sxs-lookup"><span data-stu-id="5018f-201">Choose **Yes** toocreate a release definition.</span></span>
4. <span data-ttu-id="5018f-202">Wybierz hello **pusty** szablonu, następnie wybierz **dalej**.</span><span class="sxs-lookup"><span data-stu-id="5018f-202">Choose hello **Empty** template, then select **Next**.</span></span>
5. <span data-ttu-id="5018f-203">Sprawdź definicję kompilacji projektu i źródło hello są wypełniane przy użyciu projektu.</span><span class="sxs-lookup"><span data-stu-id="5018f-203">Verify hello project and source build definition are populated with your project.</span></span>
6. <span data-ttu-id="5018f-204">Wybierz hello **ciągłe wdrażanie** pole wyboru, a następnie wybierz **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="5018f-204">Select hello **Continuous deployment** check box, then select **Create**.</span></span>
7. <span data-ttu-id="5018f-205">Zaznacz pole listy rozwijanej hello obok zbyt**+ Dodaj zadania** i wybierz polecenie *dodać faza wdrożenia grupy*.</span><span class="sxs-lookup"><span data-stu-id="5018f-205">Select hello drop-down box next too**+ Add tasks** and choose *Add a deployment group phase*.</span></span>
    
    ![Dodaj definicję toorelease zadania w usłudze Team Services](media/tutorial-vsts-iis-cicd/add_release_task.png)

8. <span data-ttu-id="5018f-207">Wybierz **Dodaj** dalej zbyt**Deploy(Preview) aplikacji sieci Web usług IIS**, a następnie wybierz pozycję **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="5018f-207">Choose **Add** next too**IIS Web App Deploy(Preview)**, then select **Close**.</span></span>
9. <span data-ttu-id="5018f-208">Wybierz hello **Uruchom na grupę wdrożenia** zadaniem nadrzędnym.</span><span class="sxs-lookup"><span data-stu-id="5018f-208">Select hello **Run on deployment group** parent task.</span></span>
    1. <span data-ttu-id="5018f-209">Dla **grupę wdrożenia**, wybierz pozycję hello wdrożenia grupy utworzonej wcześniej, takich jak *Mój_iis*.</span><span class="sxs-lookup"><span data-stu-id="5018f-209">For **Deployment Group**, select hello deployment group you created earlier, such as *myIIS*.</span></span>
    2. <span data-ttu-id="5018f-210">W hello **komputera tagi** wybierz opcję **Dodaj** i wybierz polecenie hello *web* tagu.</span><span class="sxs-lookup"><span data-stu-id="5018f-210">In hello **Machine tags** box, select **Add** and choose hello *web* tag.</span></span>
    
    ![Zwolnij definicji zadania wdrażania w grupie dla usług IIS](media/tutorial-vsts-iis-cicd/release_definition_iis.png)
 
11. <span data-ttu-id="5018f-212">Wybierz hello **Wdróż: Wdrażanie aplikacji sieci Web usług IIS** tooconfigure zadań programu IIS wystąpienia następujące ustawienia:</span><span class="sxs-lookup"><span data-stu-id="5018f-212">Select hello **Deploy: IIS Web App Deploy** task tooconfigure your IIS instance settings as follows:</span></span>
    1. <span data-ttu-id="5018f-213">Aby uzyskać **nazwa witryny sieci Web**, wprowadź *domyślna witryna sieci Web*.</span><span class="sxs-lookup"><span data-stu-id="5018f-213">For **Website Name**, enter *Default Web Site*.</span></span>
    2. <span data-ttu-id="5018f-214">Pozostaw hello wszystkie inne ustawienia domyślne.</span><span class="sxs-lookup"><span data-stu-id="5018f-214">Leave all hello other default settings.</span></span>
12. <span data-ttu-id="5018f-215">Wybierz **zapisać**, a następnie wybierz pozycję **OK** dwa razy.</span><span class="sxs-lookup"><span data-stu-id="5018f-215">Choose **Save**, then select **OK** twice.</span></span>


## <a name="create-a-release-and-publish"></a><span data-ttu-id="5018f-216">Tworzenie zlecenia i publikowanie</span><span class="sxs-lookup"><span data-stu-id="5018f-216">Create a release and publish</span></span>
<span data-ttu-id="5018f-217">Teraz możesz wypchnąć sieci web wdrażanie pakietu jako nową wersję.</span><span class="sxs-lookup"><span data-stu-id="5018f-217">You can now push your web deploy package as a new release.</span></span> <span data-ttu-id="5018f-218">Ten krok komunikuje się z agentem hello na każdego wystąpienia, które jest częścią grupy wdrożenia hello, wypchnięcia hello web wdrożenia pakietu, a następnie konfiguruje aplikacji sieci web programu IIS toorun hello zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="5018f-218">This step communicates with hello agent on each instance that is part of hello deployment group, pushes hello web deploy package, then configures IIS toorun hello updated web application.</span></span>

1. <span data-ttu-id="5018f-219">W definicji wersji, wybierz **+ wersji**, a następnie wybierz **Tworzenie wersji**.</span><span class="sxs-lookup"><span data-stu-id="5018f-219">In your release definition, select **+ Release**, then choose **Create Release**.</span></span>
2. <span data-ttu-id="5018f-220">Sprawdź, czy hello ostatniej kompilacji jest zaznaczony na liście rozwijanej hello wraz z **automatycznego wdrożenia: po utworzeniu wersji**.</span><span class="sxs-lookup"><span data-stu-id="5018f-220">Verify that hello latest build is selected in hello drop-down list, along with **Automated deployment: After release creation**.</span></span> <span data-ttu-id="5018f-221">Wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="5018f-221">Select **Create**.</span></span>
3. <span data-ttu-id="5018f-222">Transparent małych hello górze wyświetlany definicję zlecenia, takie jak *wersji "Wersji 1" utworzył*.</span><span class="sxs-lookup"><span data-stu-id="5018f-222">A small banner appears across hello top of your release definition, such as *Release 'Release-1' has been created*.</span></span> <span data-ttu-id="5018f-223">Wybierz hello wersji łącze.</span><span class="sxs-lookup"><span data-stu-id="5018f-223">Select hello release link.</span></span>
4. <span data-ttu-id="5018f-224">Otwórz hello **dzienniki** karcie toowatch hello wersji postępu.</span><span class="sxs-lookup"><span data-stu-id="5018f-224">Open hello **Logs** tab toowatch hello release progress.</span></span>
    
    ![Pomyślne wersji Team Services i sieci web wdrażanie pakietu wypychania](media/tutorial-vsts-iis-cicd/successful_release.png)

5. <span data-ttu-id="5018f-226">Po zakończeniu wersji hello Otwórz przeglądarkę sieci web, a następnie wprowadź hello publiczny adres OPS maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5018f-226">After hello release is complete, open a web browser and enter hello public IIP address of your VM.</span></span> <span data-ttu-id="5018f-227">Aplikacja sieci web programu ASP.NET jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="5018f-227">Your ASP.NET web application is running.</span></span>

    ![Uruchomiona na maszynie Wirtualnej IIS aplikacji sieci web ASP.NET](media/tutorial-vsts-iis-cicd/running_web_app.png)


## <a name="test-hello-whole-cicd-pipeline"></a><span data-ttu-id="5018f-229">Test hello całego elementu konfiguracji/CD potoku</span><span class="sxs-lookup"><span data-stu-id="5018f-229">Test hello whole CI/CD pipeline</span></span>
<span data-ttu-id="5018f-230">Z aplikacji sieci web uruchomionej na serwerze IIS teraz spróbuj hello całego elementu konfiguracji/CD potoku.</span><span class="sxs-lookup"><span data-stu-id="5018f-230">With your web application running on IIS, now try hello whole CI/CD pipeline.</span></span> <span data-ttu-id="5018f-231">Po wprowadzeniu zmiany w Visual Studio i zatwierdzania wyzwolenia kodu, kompilacji, następnie wyzwalające zlecenia sieci web zaktualizowane wdrożyć tooIIS pakietu:</span><span class="sxs-lookup"><span data-stu-id="5018f-231">After you make a change in Visual Studio and commit your code, a build is triggered which then triggers a release of your updated web deploy package tooIIS:</span></span>

1. <span data-ttu-id="5018f-232">W programie Visual Studio Otwórz hello **Eksploratora rozwiązań** okna.</span><span class="sxs-lookup"><span data-stu-id="5018f-232">In Visual Studio, open hello **Solution Explorer** window.</span></span>
2. <span data-ttu-id="5018f-233">Przejdź Otwórz tooand *myWebApp | Widoki | Strona główna | Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="5018f-233">Navigate tooand open *myWebApp | Views | Home | Index.cshtml*</span></span>
3. <span data-ttu-id="5018f-234">Edytuj tooread wiersz 6:</span><span class="sxs-lookup"><span data-stu-id="5018f-234">Edit line 6 tooread:</span></span>

    `<h1>ASP.NET with VSTS and CI/CD!</h1>`

4. <span data-ttu-id="5018f-235">Zapisz plik hello.</span><span class="sxs-lookup"><span data-stu-id="5018f-235">Save hello file.</span></span>
5. <span data-ttu-id="5018f-236">Otwórz hello **Team Explorer** okna, wybierz hello *myWebApp* projektu, a następnie wybierz pozycję **zmiany**.</span><span class="sxs-lookup"><span data-stu-id="5018f-236">Open hello **Team Explorer** window, select hello *myWebApp* project, then choose **Changes**.</span></span>
6. <span data-ttu-id="5018f-237">Wpisz wiadomość, zatwierdzania, takich jak *potoku testowania CI/CD*, a następnie wybierz **wszystkie zatwierdzenia i synchronizacji** z menu rozwijanego hello.</span><span class="sxs-lookup"><span data-stu-id="5018f-237">Enter a commit message, such as *Testing CI/CD pipeline*, then choose **Commit All and Sync** from hello drop-down menu.</span></span>
7. <span data-ttu-id="5018f-238">W obszarze roboczym Team Services nowej kompilacji zostanie wywołany z hello kod zatwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="5018f-238">In Team Services workspace, a new build is triggered from hello code commit.</span></span> 
    - <span data-ttu-id="5018f-239">Wybierz **kompilacji i wydania**, a następnie wybierz pozycję **kompilacje**.</span><span class="sxs-lookup"><span data-stu-id="5018f-239">Choose **Build & Release**, then select **Builds**.</span></span> 
    - <span data-ttu-id="5018f-240">Wybierz definicję kompilacji, a następnie wybierz hello **w kolejce & uruchomiona** toowatch kompilacji jako hello kompilacji realizowany.</span><span class="sxs-lookup"><span data-stu-id="5018f-240">Choose your build definition, then select hello **Queued & running** build toowatch as hello build progresses.</span></span>
9. <span data-ttu-id="5018f-241">Po kompilacji hello zakończy się pomyślnie, zostanie wywołany nowej wersji.</span><span class="sxs-lookup"><span data-stu-id="5018f-241">Once hello build is successful, a new release is triggered.</span></span>
    - <span data-ttu-id="5018f-242">Wybierz **kompilacji i wydania**, następnie **wersje** toosee hello web wdrożyć pakiet wypychana tooyour maszyn wirtualnych usług IIS.</span><span class="sxs-lookup"><span data-stu-id="5018f-242">Choose **Build & Release**, then **Releases** toosee hello web deploy package pushed tooyour IIS VM.</span></span> 
    - <span data-ttu-id="5018f-243">Wybierz hello **Odśwież** ikona tooupdate hello stanu.</span><span class="sxs-lookup"><span data-stu-id="5018f-243">Select hello **Refresh** icon tooupdate hello status.</span></span> <span data-ttu-id="5018f-244">Gdy hello *środowisk* kolumna zawiera zielony znacznik wyboru, wersji hello zostało pomyślnie wdrożone tooIIS.</span><span class="sxs-lookup"><span data-stu-id="5018f-244">When hello *Environments* column shows a green check mark, hello release has successfully deployed tooIIS.</span></span>
11. <span data-ttu-id="5018f-245">toosee zastosować zmian użytkownika, Odśwież witryny usług IIS w przeglądarce sieci Web.</span><span class="sxs-lookup"><span data-stu-id="5018f-245">toosee your changes applied, refresh your IIS website in a browser.</span></span>

    ![Uruchamianie na IIS maszyny Wirtualnej na podstawie elementu konfiguracji/CD potoku aplikacji sieci web ASP.NET](media/tutorial-vsts-iis-cicd/running_web_app_cicd.png)


## <a name="next-steps"></a><span data-ttu-id="5018f-247">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5018f-247">Next steps</span></span>

<span data-ttu-id="5018f-248">W tym samouczku utworzono aplikację sieci web platformy ASP.NET w Team Services i skonfigurowany kompilacji i wersji definicji toodeploy nowej sieci web wdrażanie pakietów tooIIS na każdym zatwierdzeniu kodu.</span><span class="sxs-lookup"><span data-stu-id="5018f-248">In this tutorial, you created an ASP.NET web application in Team Services and configured build and release definitions toodeploy new web deploy packages tooIIS on each code commit.</span></span> <span data-ttu-id="5018f-249">W tym samouczku omówiono:</span><span class="sxs-lookup"><span data-stu-id="5018f-249">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5018f-250">Publikuj projekt usługi Team Services tooa aplikacji sieci web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="5018f-250">Publish an ASP.NET web application tooa Team Services project</span></span>
> * <span data-ttu-id="5018f-251">Tworzenie definicji kompilacji, która jest wyzwalany przez kod zatwierdzenia</span><span class="sxs-lookup"><span data-stu-id="5018f-251">Create a build definition that is triggered by code commits</span></span>
> * <span data-ttu-id="5018f-252">Instalowanie i konfigurowanie usług IIS na maszynie wirtualnej na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="5018f-252">Install and configure IIS on a virtual machine in Azure</span></span>
> * <span data-ttu-id="5018f-253">Dodaj grupę wdrożenia tooa wystąpienia usług IIS hello w Team Services</span><span class="sxs-lookup"><span data-stu-id="5018f-253">Add hello IIS instance tooa deployment group in Team Services</span></span>
> * <span data-ttu-id="5018f-254">Utwórz nową web toopublish definicji wersji tooIIS pakiety wdrażania</span><span class="sxs-lookup"><span data-stu-id="5018f-254">Create a release definition toopublish new web deploy packages tooIIS</span></span>
> * <span data-ttu-id="5018f-255">Test hello CI/CD potoku</span><span class="sxs-lookup"><span data-stu-id="5018f-255">Test hello CI/CD pipeline</span></span>

<span data-ttu-id="5018f-256">Jak przejść dalej toolearn samouczka toohello toosecure serwera sieci web z certyfikatów SSL.</span><span class="sxs-lookup"><span data-stu-id="5018f-256">Advance toohello next tutorial toolearn how toosecure a web server with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5018f-257">Zabezpieczenia serwera sieci web przy użyciu protokołu SSL</span><span class="sxs-lookup"><span data-stu-id="5018f-257">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)