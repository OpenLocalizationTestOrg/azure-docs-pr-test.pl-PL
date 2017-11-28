---
title: "aaaAzure wdrożenia maszyny wirtualnej z Chef | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse Chef toodo zautomatyzowane wdrażanie maszyn wirtualnych i konfiguracji w systemie Microsoft Azure"
services: virtual-machines-windows
documentationcenter: 
author: diegoviso
manager: timlt
tags: azure-service-management,azure-resource-manager
editor: 
ms.assetid: 0b82ca70-89ed-496d-bb49-c04ae59b4523
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: diviso
ms.openlocfilehash: c5ea98c673b2ee75dd4cedf27e50330af05230d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="automating-azure-virtual-machine-deployment-with-chef"></a><span data-ttu-id="4fa37-103">Automatyzowanie wdrażania maszyny wirtualnej platformy Azure przy użyciu narzędzia Chef</span><span class="sxs-lookup"><span data-stu-id="4fa37-103">Automating Azure virtual machine deployment with Chef</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="4fa37-104">Chef to doskonałe narzędzie do dostarczania automatyzacji i żądanego stanu konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="4fa37-104">Chef is a great tool for delivering automation and desired state configurations.</span></span>

<span data-ttu-id="4fa37-105">Z naszych najnowszej wersji interfejsu api chmury Chef zapewnia bezproblemową integrację z platformy Azure, umożliwiając hello tooprovision możliwości i wdrożyć stanami konfiguracji, za pomocą jednego polecenia.</span><span class="sxs-lookup"><span data-stu-id="4fa37-105">With our latest cloud-api release, Chef provides seamless integration with Azure, giving you hello ability tooprovision and deploy configuration states through a single command.</span></span>

<span data-ttu-id="4fa37-106">W tym artykule, I opisano sposób tooset się tooprovision środowiska użytkownika Chef wirtualnej Azure maszyny i przeprowadzi użytkownika przez proces tworzenia zasad lub "CookBook", a następnie wdrażania tego tooan cookbook maszyny wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4fa37-106">In this article, I’ll show you how tooset up your Chef environment tooprovision Azure virtual machines and walk you through creating a policy or “CookBook” and then deploying this cookbook tooan Azure virtual machine.</span></span>

<span data-ttu-id="4fa37-107">Zacznijmy!</span><span class="sxs-lookup"><span data-stu-id="4fa37-107">Let’s begin!</span></span>

## <a name="chef-basics"></a><span data-ttu-id="4fa37-108">Podstawy chef</span><span class="sxs-lookup"><span data-stu-id="4fa37-108">Chef basics</span></span>
<span data-ttu-id="4fa37-109">Przed rozpoczęciem sugeruje recenzowania hello podstawowych pojęciach dotyczących Chef.</span><span class="sxs-lookup"><span data-stu-id="4fa37-109">Before you begin, I suggest you review hello basic concepts of Chef.</span></span> <span data-ttu-id="4fa37-110">Istnieje bardzo materiałów <a href="http://www.chef.io/chef" target="_blank">tutaj</a> i najlepiej masz szybkiego odczytu przed podjęciem próby tego przewodnika.</span><span class="sxs-lookup"><span data-stu-id="4fa37-110">There is great material <a href="http://www.chef.io/chef" target="_blank">here</a> and I recommend you have a quick read before you attempt this walkthrough.</span></span> <span data-ttu-id="4fa37-111">Będzie można jednak recap podstawy hello początek.</span><span class="sxs-lookup"><span data-stu-id="4fa37-111">I will however recap hello basics before we get started.</span></span>

<span data-ttu-id="4fa37-112">powitania po diagram przedstawia architekturę Chef wysokiego poziomu hello.</span><span class="sxs-lookup"><span data-stu-id="4fa37-112">hello following diagram depicts hello high-level Chef architecture.</span></span>

![][2]

<span data-ttu-id="4fa37-113">Chef ma trzy główne składniki architektury: Chef, Chef klienta (węzeł), Chef stacji roboczej i serwerze.</span><span class="sxs-lookup"><span data-stu-id="4fa37-113">Chef has three main architectural components: Chef Server, Chef Client (node), and Chef Workstation.</span></span>

<span data-ttu-id="4fa37-114">powitania serwera Chef jest naszych punkt zarządzania i dostępne są dwie opcje dla powitania serwera Chef: hostowanej rozwiązania lub rozwiązaniem w firmie.</span><span class="sxs-lookup"><span data-stu-id="4fa37-114">hello Chef Server is our management point and there are two options for hello Chef Server: a hosted solution or an on-premises solution.</span></span> <span data-ttu-id="4fa37-115">Użyjemy hostowanego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="4fa37-115">We will be using a hosted solution.</span></span>

<span data-ttu-id="4fa37-116">Witaj Chef klienta (węzeł) jest hello agenta, która znajduje się na serwerach hello, którym zarządzasz.</span><span class="sxs-lookup"><span data-stu-id="4fa37-116">hello Chef Client (node) is hello agent that sits on hello servers you are managing.</span></span>

<span data-ttu-id="4fa37-117">Witaj Chef stacji roboczej jest naszych administracyjnej stacji roboczej, którym możemy tworzyć nasze zasady i wykonywać polecenia nasze management.</span><span class="sxs-lookup"><span data-stu-id="4fa37-117">hello Chef Workstation is our admin workstation where we create our policies and execute our management commands.</span></span> <span data-ttu-id="4fa37-118">Przeprowadzana hello **nóż** poleceń z hello toomanage stacji roboczej Chef naszej infrastruktury.</span><span class="sxs-lookup"><span data-stu-id="4fa37-118">We run hello **knife** command from hello Chef Workstation toomanage our infrastructure.</span></span>

<span data-ttu-id="4fa37-119">Istnieje również hello pojęcie "Cookbooks" i "Przepisami".</span><span class="sxs-lookup"><span data-stu-id="4fa37-119">There is also hello concept of “Cookbooks” and “Recipes”.</span></span> <span data-ttu-id="4fa37-120">Efektywne są zasady hello możemy Zdefiniuj i Zastosuj tooour serwerów.</span><span class="sxs-lookup"><span data-stu-id="4fa37-120">These are effectively hello policies we define and apply tooour servers.</span></span>

## <a name="preparing-hello-workstation"></a><span data-ttu-id="4fa37-121">Przygotowanie stacji roboczej hello</span><span class="sxs-lookup"><span data-stu-id="4fa37-121">Preparing hello workstation</span></span>
<span data-ttu-id="4fa37-122">Po pierwsze umożliwia hello przygotowywania stacji roboczej.</span><span class="sxs-lookup"><span data-stu-id="4fa37-122">First, lets prep hello workstation.</span></span> <span data-ttu-id="4fa37-123">Używam standardowe stacji roboczej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="4fa37-123">I’m using a standard Windows workstation.</span></span> <span data-ttu-id="4fa37-124">Potrzebujemy toocreate toostore katalogu plików konfiguracji i cookbooks firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4fa37-124">We need toocreate a directory toostore our config files and cookbooks.</span></span>

<span data-ttu-id="4fa37-125">Najpierw utwórz katalog o nazwie C:\chef.</span><span class="sxs-lookup"><span data-stu-id="4fa37-125">First create a directory called C:\chef.</span></span>

<span data-ttu-id="4fa37-126">Następnie utwórz drugi katalog o nazwie c:\chef\cookbooks.</span><span class="sxs-lookup"><span data-stu-id="4fa37-126">Then create a second directory called c:\chef\cookbooks.</span></span>

<span data-ttu-id="4fa37-127">Teraz potrzebujemy toodownload naszych pliku ustawień platformy Azure, Chef może komunikować się z naszym subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4fa37-127">We now need toodownload our Azure settings file so Chef can communicate with our Azure subscription.</span></span>

<!--Download your publish settings from [here](https://manage.windowsazure.com/publishsettings/).-->
<span data-ttu-id="4fa37-128">Pobierz Twoje ustawienia za pomocą hello PowerShell Azure publikowania [Get AzurePublishSettingsFile](https://docs.microsoft.com/en-us/powershell/module/azure/get-azurepublishsettingsfile?view=azuresmps-4.0.0) polecenia.</span><span class="sxs-lookup"><span data-stu-id="4fa37-128">Download your publish settings using hello PowerShell Azure [Get-AzurePublishSettingsFile](https://docs.microsoft.com/en-us/powershell/module/azure/get-azurepublishsettingsfile?view=azuresmps-4.0.0) command.</span></span> 

<span data-ttu-id="4fa37-129">Zapisz hello pliku ustawień publikowania w C:\chef.</span><span class="sxs-lookup"><span data-stu-id="4fa37-129">Save hello publish settings file in C:\chef.</span></span>

## <a name="creating-a-managed-chef-account"></a><span data-ttu-id="4fa37-130">Tworzenie zarządzanego konta Chef</span><span class="sxs-lookup"><span data-stu-id="4fa37-130">Creating a managed Chef account</span></span>
<span data-ttu-id="4fa37-131">Załóż konto hostowanej Chef [tutaj](https://manage.chef.io/signup).</span><span class="sxs-lookup"><span data-stu-id="4fa37-131">Sign up for a hosted Chef account [here](https://manage.chef.io/signup).</span></span>

<span data-ttu-id="4fa37-132">W trakcie zapisywania hello będzie zadawane toocreate nowej organizacji.</span><span class="sxs-lookup"><span data-stu-id="4fa37-132">During hello signup process, you will be asked toocreate a new organization.</span></span>

![][3]

<span data-ttu-id="4fa37-133">Po utworzeniu organizacji, Pobierz hello starter kit.</span><span class="sxs-lookup"><span data-stu-id="4fa37-133">Once your organization is created, download hello starter kit.</span></span>

![][4]

> [!NOTE]
> <span data-ttu-id="4fa37-134">Jeśli zostanie wyświetlony monit, ostrzeżenie, że spowoduje zresetowanie kluczy, jest ok tooproceed jak mamy bez istniejącej infrastruktury jeszcze skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="4fa37-134">If you receive a prompt warning you that your keys will be reset, it’s ok tooproceed as we have no existing infrastructure configured as yet.</span></span>
> 
> 

<span data-ttu-id="4fa37-135">Ten plik starter kit zip zawiera organizacji plików konfiguracji i kluczy.</span><span class="sxs-lookup"><span data-stu-id="4fa37-135">This starter kit zip file contains your organization config files and keys.</span></span>

## <a name="configuring-hello-chef-workstation"></a><span data-ttu-id="4fa37-136">Konfigurowanie stacji roboczej Chef hello</span><span class="sxs-lookup"><span data-stu-id="4fa37-136">Configuring hello Chef workstation</span></span>
<span data-ttu-id="4fa37-137">Wyodrębnij zawartość hello hello tooC:\chef chef starter.zip.</span><span class="sxs-lookup"><span data-stu-id="4fa37-137">Extract hello content of hello chef-starter.zip tooC:\chef.</span></span>

<span data-ttu-id="4fa37-138">Kopiowanie wszystkich plików w katalogu chef-starter\chef repozytorium\.chef tooyour c:\chef katalogu.</span><span class="sxs-lookup"><span data-stu-id="4fa37-138">Copy all files under chef-starter\chef-repo\.chef tooyour c:\chef directory.</span></span>

<span data-ttu-id="4fa37-139">Katalogu powinien teraz wyglądać hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="4fa37-139">Your directory should now look something like hello following example.</span></span>

![][5]

<span data-ttu-id="4fa37-140">Teraz powinien mieć cztery pliki, w tym hello Azure publikowania plików w katalogu głównym hello c:\chef.</span><span class="sxs-lookup"><span data-stu-id="4fa37-140">You should now have four files including hello Azure publishing file in hello root of c:\chef.</span></span>

<span data-ttu-id="4fa37-141">pliki PEM Hello zawierają organizacji i administratora klucze prywatne do komunikacji podczas hello knife.rb plik zawiera konfigurację Nóż.</span><span class="sxs-lookup"><span data-stu-id="4fa37-141">hello PEM files contain your organization and admin private keys for communication while hello knife.rb file contains your knife configuration.</span></span> <span data-ttu-id="4fa37-142">Potrzebujemy tooedit hello knife.rb pliku.</span><span class="sxs-lookup"><span data-stu-id="4fa37-142">We will need tooedit hello knife.rb file.</span></span>

<span data-ttu-id="4fa37-143">Otwórz plik hello w wybranym edytorze i zmodyfikować hello "cookbook_path", usuwając hello /... / ze ścieżki hello tak wygląda na to, jak pokazano w następnym.</span><span class="sxs-lookup"><span data-stu-id="4fa37-143">Open hello file in your editor of choice and modify hello “cookbook_path” by removing hello /../ from hello path so it appears as shown next.</span></span>

    cookbook_path  ["#{current_dir}/cookbooks"]

<span data-ttu-id="4fa37-144">Również dodać hello następująca linia odbicia nazwę hello Azure pliku ustawień publikowania.</span><span class="sxs-lookup"><span data-stu-id="4fa37-144">Also add hello following line reflecting hello name of your Azure publish settings file.</span></span>

    knife[:azure_publish_settings_file] = "yourfilename.publishsettings"

<span data-ttu-id="4fa37-145">Plik knife.rb powinna wyglądać podobnie toohello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="4fa37-145">Your knife.rb file should now look similar toohello following example.</span></span>

![][6]

<span data-ttu-id="4fa37-146">Te wiersze zapewnia, że nóż odwołuje się do katalogu cookbooks hello c:\chef\cookbooks i używa również naszych pliku ustawień publikowania platformy Azure podczas operacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4fa37-146">These lines will ensure that Knife references hello cookbooks directory under c:\chef\cookbooks, and also uses our Azure Publish Settings file during Azure operations.</span></span>

## <a name="installing-hello-chef-development-kit"></a><span data-ttu-id="4fa37-147">Instalowanie hello Chef Development Kit</span><span class="sxs-lookup"><span data-stu-id="4fa37-147">Installing hello Chef Development Kit</span></span>
<span data-ttu-id="4fa37-148">Następny [Pobierz i zainstaluj](http://downloads.getchef.com/chef-dk/windows) hello tooset ChefDK (Chef Development Kit) zapasowej stacji roboczej Chef.</span><span class="sxs-lookup"><span data-stu-id="4fa37-148">Next [download and install](http://downloads.getchef.com/chef-dk/windows) hello ChefDK (Chef Development Kit) tooset up your Chef Workstation.</span></span>

![][7]

<span data-ttu-id="4fa37-149">Zainstaluj w lokalizacji domyślnej hello c:\opscode.</span><span class="sxs-lookup"><span data-stu-id="4fa37-149">Install in hello default location of c:\opscode.</span></span> <span data-ttu-id="4fa37-150">Ta instalacja potrwa około 10 minut.</span><span class="sxs-lookup"><span data-stu-id="4fa37-150">This install will take around 10 minutes.</span></span>

<span data-ttu-id="4fa37-151">Upewnij się, że zmiennej PATH zawiera wpisy dla C:\opscode\chefdk\bin; C:\opscode\chefdk\embedded\bin;c:\users\yourusername\.chefdk\gem\ruby\2.0.0\bin</span><span class="sxs-lookup"><span data-stu-id="4fa37-151">Confirm your PATH variable contains entries for C:\opscode\chefdk\bin;C:\opscode\chefdk\embedded\bin;c:\users\yourusername\.chefdk\gem\ruby\2.0.0\bin</span></span>

<span data-ttu-id="4fa37-152">Jeśli nie są dostępne, upewnij się, że możesz dodać tych ścieżek!</span><span class="sxs-lookup"><span data-stu-id="4fa37-152">If they are not there, make sure you add these paths!</span></span>

<span data-ttu-id="4fa37-153">*Uwaga hello kolejności z hello ścieżki jest ważne!*</span><span class="sxs-lookup"><span data-stu-id="4fa37-153">*NOTE hello ORDER OF hello PATH IS IMPORTANT!*</span></span> <span data-ttu-id="4fa37-154">Jeśli Twoje opscode ścieżek nie są w odpowiedniej kolejności hello masz problemy.</span><span class="sxs-lookup"><span data-stu-id="4fa37-154">If your opscode paths are not in hello correct order you will have issues.</span></span>

<span data-ttu-id="4fa37-155">Przed kontynuowaniem uruchom ponownie stację roboczą.</span><span class="sxs-lookup"><span data-stu-id="4fa37-155">Reboot your workstation before you continue.</span></span>

<span data-ttu-id="4fa37-156">Następnie zostanie zainstalowany hello Azure nóż rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="4fa37-156">Next, we will install hello Knife Azure extension.</span></span> <span data-ttu-id="4fa37-157">To zapewnia nóż hello "Wtyczkę Azure".</span><span class="sxs-lookup"><span data-stu-id="4fa37-157">This provides Knife with hello “Azure Plugin”.</span></span>

<span data-ttu-id="4fa37-158">Uruchom następujące polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="4fa37-158">Run hello following command.</span></span>

    chef gem install knife-azure ––pre

> [!NOTE]
> <span data-ttu-id="4fa37-159">argument — sprzed Hello gwarantuje, że otrzymujesz hello najnowszej wersji RC hello nóż Azure wtyczkę, która zapewnia dostęp toohello najnowszy zestaw interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="4fa37-159">hello –pre argument ensures you are receiving hello latest RC version of hello Knife Azure Plugin which provides access toohello latest set of APIs.</span></span>
> 
> 

<span data-ttu-id="4fa37-160">Istnieje prawdopodobieństwo, że liczba zależności także zostaną zainstalowane na powitania tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="4fa37-160">It’s likely that a number of dependencies will also be installed at hello same time.</span></span>

![][8]

<span data-ttu-id="4fa37-161">tooensure, wszystko jest poprawnie skonfigurowana; hello uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="4fa37-161">tooensure everything is configured correctly, run hello following command.</span></span>

    knife azure image list

<span data-ttu-id="4fa37-162">Jeśli wszystko jest poprawnie skonfigurowane, zobaczysz listę dostępnych obrazów Azure przewiń.</span><span class="sxs-lookup"><span data-stu-id="4fa37-162">If everything is configured correctly, you will see a list of available Azure images scroll through.</span></span>

<span data-ttu-id="4fa37-163">Gratulacje.</span><span class="sxs-lookup"><span data-stu-id="4fa37-163">Congratulations.</span></span> <span data-ttu-id="4fa37-164">Konfigurowanie stacji roboczej Witaj!</span><span class="sxs-lookup"><span data-stu-id="4fa37-164">hello workstation is set up!</span></span>

## <a name="creating-a-cookbook"></a><span data-ttu-id="4fa37-165">Tworzenie Cookbook</span><span class="sxs-lookup"><span data-stu-id="4fa37-165">Creating a Cookbook</span></span>
<span data-ttu-id="4fa37-166">Cookbook jest używany przez Chef toodefine zestaw poleceń, które chcesz tooexecute na zarządzanym kliencie.</span><span class="sxs-lookup"><span data-stu-id="4fa37-166">A Cookbook is used by Chef toodefine a set of commands that you wish tooexecute on your managed client.</span></span> <span data-ttu-id="4fa37-167">Tworzenie Cookbook jest proste i używamy hello **chef Generowanie cookbook** polecenia toogenerate naszych Cookbook szablonu.</span><span class="sxs-lookup"><span data-stu-id="4fa37-167">Creating a Cookbook is straightforward and we use hello **chef generate cookbook** command toogenerate our Cookbook template.</span></span> <span data-ttu-id="4fa37-168">I będzie wywoływany serwer sieci web Cookbook jako chcę zasadę, która powoduje automatyczne wdrożenie usług IIS.</span><span class="sxs-lookup"><span data-stu-id="4fa37-168">I will be calling my Cookbook web server as I would like a policy that automatically deploys IIS.</span></span>

<span data-ttu-id="4fa37-169">W obszarze katalogu C:\Chef Uruchom hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="4fa37-169">Under your C:\Chef directory run hello following command.</span></span>

    chef generate cookbook webserver

<span data-ttu-id="4fa37-170">Spowoduje to wygenerowanie zestawu plików w katalogu hello C:\Chef\cookbooks\webserver.</span><span class="sxs-lookup"><span data-stu-id="4fa37-170">This will generate a set of files under hello directory C:\Chef\cookbooks\webserver.</span></span> <span data-ttu-id="4fa37-171">Teraz potrzebujemy toodefine hello zestaw poleceń, chcielibyśmy naszych tooexecute klienta Chef w naszym zarządzanej maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4fa37-171">We now need toodefine hello set of commands we would like our Chef client tooexecute on our managed virtual machine.</span></span>

<span data-ttu-id="4fa37-172">polecenia Hello są przechowywane w hello default.rb pliku.</span><span class="sxs-lookup"><span data-stu-id="4fa37-172">hello commands are stored in hello file default.rb.</span></span> <span data-ttu-id="4fa37-173">W tym pliku I będzie można definiujący zestaw poleceń, który instaluje usługi IIS, uruchamiania usług IIS i kopiuje folder wwwroot toohello pliku szablonu.</span><span class="sxs-lookup"><span data-stu-id="4fa37-173">In this file, I’ll be defining a set of commands that installs IIS, starts IIS and copies a template file toohello wwwroot folder.</span></span>

<span data-ttu-id="4fa37-174">Zmodyfikuj C:\chef\cookbooks\webserver\recipes\default.rb hello i dodaj następujące wiersze hello.</span><span class="sxs-lookup"><span data-stu-id="4fa37-174">Modify hello C:\chef\cookbooks\webserver\recipes\default.rb file and add hello following lines.</span></span>

    powershell_script 'Install IIS' do
         action :run
         code 'add-windowsfeature Web-Server'
    end

    service 'w3svc' do
         action [ :enable, :start ]
    end

    template 'c:\inetpub\wwwroot\Default.htm' do
         source 'Default.htm.erb'
         rights :read, 'Everyone'
    end

<span data-ttu-id="4fa37-175">Zapisz plik hello, gdy wszystko będzie gotowe.</span><span class="sxs-lookup"><span data-stu-id="4fa37-175">Save hello file once you are done.</span></span>

## <a name="creating-a-template"></a><span data-ttu-id="4fa37-176">Tworzenie szablonu</span><span class="sxs-lookup"><span data-stu-id="4fa37-176">Creating a template</span></span>
<span data-ttu-id="4fa37-177">Jak wspomniano wcześniej, potrzebujemy toogenerate pliku szablonu, który będzie używany jako naszą stronę default.html.</span><span class="sxs-lookup"><span data-stu-id="4fa37-177">As we mentioned previously, we need toogenerate a template file which will be used as our default.html page.</span></span>

<span data-ttu-id="4fa37-178">Witaj uruchom następujące polecenie toogenerate hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="4fa37-178">Run hello following command toogenerate hello template.</span></span>

    chef generate template webserver Default.htm

<span data-ttu-id="4fa37-179">Teraz przejdź toohello C:\chef\cookbooks\webserver\templates\default\Default.htm.erb pliku.</span><span class="sxs-lookup"><span data-stu-id="4fa37-179">Now navigate toohello C:\chef\cookbooks\webserver\templates\default\Default.htm.erb file.</span></span> <span data-ttu-id="4fa37-180">Edytuj plik hello przez dodanie prostego kodu "Hello World" HTML, a następnie zapisz plik hello.</span><span class="sxs-lookup"><span data-stu-id="4fa37-180">Edit hello file by adding some simple “Hello World” HTML code, and then save hello file.</span></span>

## <a name="upload-hello-cookbook-toohello-chef-server"></a><span data-ttu-id="4fa37-181">Przekaż hello Cookbook toohello Chef serwera</span><span class="sxs-lookup"><span data-stu-id="4fa37-181">Upload hello Cookbook toohello Chef Server</span></span>
<span data-ttu-id="4fa37-182">W tym kroku wiemy zabierać hello Cookbook, który został utworzony w naszym komputera lokalnego i przekazać go toohello Chef hostowana serwera.</span><span class="sxs-lookup"><span data-stu-id="4fa37-182">In this step, we are taking a copy of hello Cookbook that we have created on our local machine and uploading it toohello Chef Hosted Server.</span></span> <span data-ttu-id="4fa37-183">Po przekazaniu plików hello Cookbook zostanie wyświetlony w obszarze hello **zasad** kartę.</span><span class="sxs-lookup"><span data-stu-id="4fa37-183">Once uploaded, hello Cookbook will appear under hello **Policy** tab.</span></span>

    knife cookbook upload webserver

![][9]

## <a name="deploy-a-virtual-machine-with-knife-azure"></a><span data-ttu-id="4fa37-184">Wdrażanie maszyny wirtualnej z platformy Azure, nóż</span><span class="sxs-lookup"><span data-stu-id="4fa37-184">Deploy a virtual machine with Knife Azure</span></span>
<span data-ttu-id="4fa37-185">Firma Microsoft będzie teraz wdrożyć maszyny wirtualnej platformy Azure i stosować hello Cookbook "Serwer sieci Web", co spowoduje zainstalowanie naszych usług IIS sieci web usługi i domyślnej strony sieci web.</span><span class="sxs-lookup"><span data-stu-id="4fa37-185">We will now deploy an Azure virtual machine and apply hello “Webserver” Cookbook which will install our IIS web service and default web page.</span></span>

<span data-ttu-id="4fa37-186">W kolejności toodo, to należy użyć hello **utworzenie przez serwer nóż azure** polecenia.</span><span class="sxs-lookup"><span data-stu-id="4fa37-186">In order toodo this, use hello **knife azure server create** command.</span></span>

<span data-ttu-id="4fa37-187">Czy na przykład hello polecenia pojawi się dalej.</span><span class="sxs-lookup"><span data-stu-id="4fa37-187">Am example of hello command appears next.</span></span>

    knife azure server create --azure-dns-name 'diegotest01' --azure-vm-name 'testserver01' --azure-vm-size 'Small' --azure-storage-account 'portalvhdsxxxx' --bootstrap-protocol 'cloud-api' --azure-source-image 'a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-Datacenter-201411.01-en.us-127GB.vhd' --azure-service-location 'Southeast Asia' --winrm-user azureuser --winrm-password 'myPassword123' --tcp-endpoints 80,3389 --r 'recipe[webserver]'

<span data-ttu-id="4fa37-188">Parametry Hello nie wymaga wyjaśnień.</span><span class="sxs-lookup"><span data-stu-id="4fa37-188">hello parameters are self-explanatory.</span></span> <span data-ttu-id="4fa37-189">Zastąp określonego zmiennych, a następnie uruchom.</span><span class="sxs-lookup"><span data-stu-id="4fa37-189">Substitute your particular variables and run.</span></span>

> [!NOTE]
> <span data-ttu-id="4fa37-190">Za pomocą wiersza polecenia hello hello I używam również Automatyzacja reguł filtra punktu końcowego sieci przy użyciu parametru punkty końcowe tcp — Witaj.</span><span class="sxs-lookup"><span data-stu-id="4fa37-190">Through hello hello command line, I’m also automating my endpoint network filter rules by using hello –tcp-endpoints parameter.</span></span> <span data-ttu-id="4fa37-191">I zostały otwarte porty 80 i 3389 strony sieci web toomy dostępu tooprovide i sesji protokołu RDP.</span><span class="sxs-lookup"><span data-stu-id="4fa37-191">I’ve opened up ports 80 and 3389 tooprovide access toomy web page and RDP session.</span></span>
> 
> 

<span data-ttu-id="4fa37-192">Po uruchomieniu polecenia hello Przejdź toohello Azure portal i zostanie wyświetlony rozpocząć tooprovision komputer.</span><span class="sxs-lookup"><span data-stu-id="4fa37-192">Once you run hello command, go toohello Azure portal and you will see your machine begin tooprovision.</span></span>

![][13]

<span data-ttu-id="4fa37-193">następnie zostanie wyświetlona Hello wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="4fa37-193">hello command prompt appears next.</span></span>

![][10]

<span data-ttu-id="4fa37-194">Po zakończeniu wdrażania hello będziemy usługi sieci web toohello tooconnect stanie za pośrednictwem portu 80 jak firma Microsoft ma otwarty hello port podczas przydzielania firma Microsoft hello maszynę wirtualną z hello Azure nóż polecenia.</span><span class="sxs-lookup"><span data-stu-id="4fa37-194">Once hello deployment is complete, we should be able tooconnect toohello web service over port 80 as we had opened hello port when we provisioned hello virtual machine with hello Knife Azure command.</span></span> <span data-ttu-id="4fa37-195">Ta maszyna wirtualna jest hello tylko maszyny wirtualnej w usłudze w chmurze, połączę go z adresem url usługi chmury hello.</span><span class="sxs-lookup"><span data-stu-id="4fa37-195">As this virtual machine is hello only virtual machine in my cloud service, I’ll connect it with hello cloud service url.</span></span>

![][11]

<span data-ttu-id="4fa37-196">Jak widać, otrzymano creative z mojego kodu HTML.</span><span class="sxs-lookup"><span data-stu-id="4fa37-196">As you can see, I got creative with my HTML code.</span></span>

<span data-ttu-id="4fa37-197">Pamiętaj, że firma Microsoft mogą łączyć za pomocą sesji protokołu RDP z portalu Azure za pośrednictwem portu 3389 hello.</span><span class="sxs-lookup"><span data-stu-id="4fa37-197">Don’t forget we can also connect through an RDP session from hello Azure portal via port 3389.</span></span>

<span data-ttu-id="4fa37-198">Mam nadzieję, że było to pomocne!</span><span class="sxs-lookup"><span data-stu-id="4fa37-198">I hope this has been helpful!</span></span> <span data-ttu-id="4fa37-199">Przejdź i uruchom infrastruktury jako przebieg kodu z platformą Azure już dziś!</span><span class="sxs-lookup"><span data-stu-id="4fa37-199">Go  and start your infrastructure as code journey with Azure today!</span></span>

<!--Image references-->
[2]: media/chef-automation/2.png
[3]: media/chef-automation/3.png
[4]: media/chef-automation/4.png
[5]: media/chef-automation/5.png
[6]: media/chef-automation/6.png
[7]: media/chef-automation/7.png
[8]: media/chef-automation/8.png
[9]: media/chef-automation/9.png
[10]: media/chef-automation/10.png
[11]: media/chef-automation/11.png
[13]: media/chef-automation/13.png


<!--Link references-->
