---
title: Host Ruby w witrynie sieci Web szyny na maszynie Wirtualnej systemu Linux | Dokumentacja firmy Microsoft
description: "Konfigurowanie i udostępniać Ruby na podstawie szyny witryny sieci Web na platformie Azure przy użyciu maszyny wirtualnej systemu Linux."
services: virtual-machines-linux
documentationcenter: ruby
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: aad32685-3550-4bff-9c73-beb8d70b3291
ms.service: virtual-machines-linux
ms.workload: web
ms.tgt_pltfrm: vm-linux
ms.devlang: ruby
ms.topic: article
ms.date: 06/27/2017
ms.author: robmcm
ms.openlocfilehash: 0518519da6c5e62a863a47d6743ab7b7c5923acf
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="ruby-on-rails-web-application-on-an-azure-vm"></a><span data-ttu-id="13d9a-103">Aplikacja sieci Web Ruby on Rails na maszynie wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="13d9a-103">Ruby on Rails Web application on an Azure VM</span></span>
<span data-ttu-id="13d9a-104">Ten samouczek pokazuje, jak udostępniać Ruby na szyny witryny sieci Web na platformie Azure przy użyciu maszyny wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="13d9a-104">This tutorial shows how to host a Ruby on Rails website on Azure using a Linux virtual machine.</span></span>  

<span data-ttu-id="13d9a-105">W tym samouczku została zweryfikowana przy użyciu Ubuntu Server 14.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="13d9a-105">This tutorial was validated using Ubuntu Server 14.04 LTS.</span></span> <span data-ttu-id="13d9a-106">Jeśli używasz innej dystrybucji systemu Linux, może być konieczne zmodyfikowanie kroki, aby zainstalować szyny.</span><span class="sxs-lookup"><span data-stu-id="13d9a-106">If you use a different Linux distribution, you might need to modify the steps to install Rails.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="13d9a-107">Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="13d9a-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="13d9a-108">Ten artykuł dotyczy klasycznego modelu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="13d9a-108">This article covers using the classic deployment model.</span></span> <span data-ttu-id="13d9a-109">Firma Microsoft zaleca, aby w przypadku większości nowych wdrożeń korzystać z modelu opartego na programie Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="13d9a-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>
>
>

## <a name="create-an-azure-vm"></a><span data-ttu-id="13d9a-110">Tworzenie maszyny Wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="13d9a-110">Create an Azure VM</span></span>
<span data-ttu-id="13d9a-111">Rozpocznij od utworzenia maszyny Wirtualnej platformy Azure z obrazem systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="13d9a-111">Start by creating an Azure VM with a Linux image.</span></span>

<span data-ttu-id="13d9a-112">Aby utworzyć maszynę Wirtualną, używając portalu Azure lub interfejsu wiersza polecenia platformy Azure (CLI).</span><span class="sxs-lookup"><span data-stu-id="13d9a-112">To create the VM, you can use the Azure portal or the Azure Command-Line Interface (CLI).</span></span>

### <a name="azure-portal"></a><span data-ttu-id="13d9a-113">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="13d9a-113">Azure portal</span></span>
1. <span data-ttu-id="13d9a-114">Zaloguj się do [portalu Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="13d9a-114">Sign into the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="13d9a-115">Kliknij przycisk **nowy**, następnie w polu wyszukiwania wpisz "Ubuntu Server 14.04".</span><span class="sxs-lookup"><span data-stu-id="13d9a-115">Click **New**, then type "Ubuntu Server 14.04" in the search box.</span></span> <span data-ttu-id="13d9a-116">Kliknij wpis zwrócony przez wyszukiwanie.</span><span class="sxs-lookup"><span data-stu-id="13d9a-116">Click the entry returned by the search.</span></span> <span data-ttu-id="13d9a-117">Wybierz model wdrażania **klasycznego**, następnie kliknij przycisk "Utwórz".</span><span class="sxs-lookup"><span data-stu-id="13d9a-117">For the deployment model, select **Classic**, then click "Create".</span></span>
3. <span data-ttu-id="13d9a-118">Podaj wartości dla pól wymaganych w bloku podstawowe służące: Nazwa (VM), nazwę użytkownika, typ uwierzytelniania i odpowiednie poświadczenia subskrypcji platformy Azure, lokalizacji i grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="13d9a-118">In the Basics blade, supply values for the required fields: Name (for the VM), User name, Authentication type and the corresponding credentials, Azure subscription, Resource group, and Location.</span></span>

   ![Utwórz nowy obraz Ubuntu](./media/virtual-machines-linux-classic-ruby-rails-web-app/createvm.png)

4. <span data-ttu-id="13d9a-120">Po zainicjowaniu obsługi maszyny Wirtualnej, kliknij nazwę maszyny Wirtualnej i kliknij przycisk **punkty końcowe** w **ustawienia** kategorii.</span><span class="sxs-lookup"><span data-stu-id="13d9a-120">After the VM is provisioned, click on the VM name, and click **Endpoints** in the **Settings** category.</span></span> <span data-ttu-id="13d9a-121">Znaleźć punkt końcowy SSH, kategorii **autonomiczny**.</span><span class="sxs-lookup"><span data-stu-id="13d9a-121">Find the SSH endpoint, listed under **Standalone**.</span></span>

   ![Domyślny punkt końcowy](./media/virtual-machines-linux-classic-ruby-rails-web-app/endpointsnewportal.png)

### <a name="azure-cli"></a><span data-ttu-id="13d9a-123">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="13d9a-123">Azure CLI</span></span>
<span data-ttu-id="13d9a-124">Postępuj zgodnie z instrukcjami [tworzenia maszyny wirtualnej systemem Linux][vm-instructions].</span><span class="sxs-lookup"><span data-stu-id="13d9a-124">Follow the steps in [Create a Virtual Machine Running Linux][vm-instructions].</span></span>

<span data-ttu-id="13d9a-125">Po zainicjowaniu obsługi maszyny Wirtualnej, można uzyskać punkt końcowy SSH, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="13d9a-125">After the VM is provisioned, you can get the SSH endpoint by running the following command:</span></span>

    azure vm endpoint list <vm-name>  

## <a name="install-ruby-on-rails"></a><span data-ttu-id="13d9a-126">Zainstaluj na szyny Ruby</span><span class="sxs-lookup"><span data-stu-id="13d9a-126">Install Ruby on Rails</span></span>
1. <span data-ttu-id="13d9a-127">Używanie protokołu SSH, aby nawiązać połączenie z maszyną Wirtualną.</span><span class="sxs-lookup"><span data-stu-id="13d9a-127">Use SSH to connect to the VM.</span></span>
2. <span data-ttu-id="13d9a-128">W sesji SSH Aby zainstalować Ruby na maszynie Wirtualnej należy użyć następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="13d9a-128">From the SSH session, use the following commands to install Ruby on the VM:</span></span>

        sudo apt-get update -y
        sudo apt-get upgrade -y

        sudo apt-add-repository ppa:brightbox/ruby-ng
        sudo apt-get update
        sudo apt-get install ruby2.4

        > [!TIP]
        > The brightbox repository contains the current Ruby distribution.

    <span data-ttu-id="13d9a-129">Instalacja może zająć kilka minut.</span><span class="sxs-lookup"><span data-stu-id="13d9a-129">The installation may take a few minutes.</span></span> <span data-ttu-id="13d9a-130">Po ukończeniu, użyj następującego polecenia, aby sprawdzić, czy zainstalowano Ruby:</span><span class="sxs-lookup"><span data-stu-id="13d9a-130">When it completes, use the following command to verify that Ruby is installed:</span></span>

        ruby -v

3. <span data-ttu-id="13d9a-131">Aby zainstalować szyny, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="13d9a-131">Use the following command to install Rails:</span></span>

        sudo gem install rails --no-rdoc --no-ri -V

    <span data-ttu-id="13d9a-132">Użyj nie rdoc i--nie ri flagi pomijania instalowanie dokumentacji, co jest szybsze.</span><span class="sxs-lookup"><span data-stu-id="13d9a-132">Use the --no-rdoc and --no-ri flags to skip installing the documentation, which is faster.</span></span>
    <span data-ttu-id="13d9a-133">To polecenie będzie prawdopodobnie zająć dużo czasu do wykonania, więc Dodawanie -V zostaną wyświetlone informacje o postępie instalacji.</span><span class="sxs-lookup"><span data-stu-id="13d9a-133">This command will likely take a long time to execute, so adding the -V will display information about the installation progress.</span></span>

## <a name="create-and-run-an-app"></a><span data-ttu-id="13d9a-134">Tworzenie i uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="13d9a-134">Create and run an app</span></span>
<span data-ttu-id="13d9a-135">Jest nadal zalogowany za pośrednictwem protokołu SSH, uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="13d9a-135">While still logged in via SSH, run the following commands:</span></span>

    rails new myapp
    cd myapp
    rails server -b 0.0.0.0 -p 3000

<span data-ttu-id="13d9a-136">[Nowe](http://guides.rubyonrails.org/command_line.html#rails-new) polecenie tworzy nową aplikację szyny.</span><span class="sxs-lookup"><span data-stu-id="13d9a-136">The [new](http://guides.rubyonrails.org/command_line.html#rails-new) command creates a new Rails app.</span></span> <span data-ttu-id="13d9a-137">[Serwera](http://guides.rubyonrails.org/command_line.html#rails-server) polecenie uruchamia serwer sieci web WEBrick dołączony do szyny.</span><span class="sxs-lookup"><span data-stu-id="13d9a-137">The [server](http://guides.rubyonrails.org/command_line.html#rails-server) command starts the WEBrick web server that comes with Rails.</span></span> <span data-ttu-id="13d9a-138">(Do użytku produkcyjnego będzie prawdopodobnie chcesz użyć innego serwera, takie jak Unicorn lub pasażerów.)</span><span class="sxs-lookup"><span data-stu-id="13d9a-138">(For production use, you would probably want to use a different server, such as Unicorn or Passenger.)</span></span>

<span data-ttu-id="13d9a-139">Powinny pojawić się dane wyjściowe podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="13d9a-139">You should see output similar to the following.</span></span>

    => Booting WEBrick
    => Rails 4.2.1 application starting in development on http://0.0.0.0:3000
    => Run `rails server -h` for more startup options
    => Ctrl-C to shutdown server
    [2015-06-09 23:34:23] INFO  WEBrick 1.3.1
    [2015-06-09 23:34:23] INFO  ruby 1.9.3 (2013-11-22) [x86_64-linux]
    [2015-06-09 23:34:23] INFO  WEBrick::HTTPServer#start: pid=27766 port=3000

## <a name="add-an-endpoint"></a><span data-ttu-id="13d9a-140">Dodawanie punktu końcowego</span><span class="sxs-lookup"><span data-stu-id="13d9a-140">Add an endpoint</span></span>
1. <span data-ttu-id="13d9a-141">Przejdź do [Azure portal] [https://portal.azure.com] i wybierz maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="13d9a-141">Go to the [Azure portal][https://portal.azure.com] and select your VM.</span></span>

2. <span data-ttu-id="13d9a-142">Wybierz **punkty końcowe** w **ustawienia** wzdłuż lewej krawędzi strony.</span><span class="sxs-lookup"><span data-stu-id="13d9a-142">Select **ENDPOINTS** in the **Settings** along the left edge the page.</span></span>

3. <span data-ttu-id="13d9a-143">Kliknij przycisk **dodać** w górnej części strony.</span><span class="sxs-lookup"><span data-stu-id="13d9a-143">Click **ADD** at the top of the page.</span></span>

4. <span data-ttu-id="13d9a-144">W **dodać punkt końcowy** okna dialogowego wprowadź następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="13d9a-144">In the **Add endpoint** dialog page, enter the following information:</span></span>

   * <span data-ttu-id="13d9a-145">**Nazwa**: HTTP</span><span class="sxs-lookup"><span data-stu-id="13d9a-145">**Name**: HTTP</span></span>
   * <span data-ttu-id="13d9a-146">**Protokół**: TCP</span><span class="sxs-lookup"><span data-stu-id="13d9a-146">**Protocol**: TCP</span></span>
   * <span data-ttu-id="13d9a-147">**Port publiczny**: 80</span><span class="sxs-lookup"><span data-stu-id="13d9a-147">**Public port**: 80</span></span>
   * <span data-ttu-id="13d9a-148">**Port prywatny**: 3000</span><span class="sxs-lookup"><span data-stu-id="13d9a-148">**Private port**: 3000</span></span>
   * <span data-ttu-id="13d9a-149">**Pływającego adresu PI**: wyłączone</span><span class="sxs-lookup"><span data-stu-id="13d9a-149">**Floating PI address**: Disabled</span></span>
   * <span data-ttu-id="13d9a-150">**Listy kontroli dostępu — kolejność**: 1001 lub inną wartość, która ustawia priorytet tej reguły dostępu.</span><span class="sxs-lookup"><span data-stu-id="13d9a-150">**Access control list - Order**: 1001, or another value that sets the priority of this access rule.</span></span>
   * <span data-ttu-id="13d9a-151">**Listy kontroli dostępu — nazwa**: allowHTTP</span><span class="sxs-lookup"><span data-stu-id="13d9a-151">**Access control list - Name**: allowHTTP</span></span>
   * <span data-ttu-id="13d9a-152">**Listy kontroli dostępu — Akcja**: Zezwalaj</span><span class="sxs-lookup"><span data-stu-id="13d9a-152">**Access control list - Action**: permit</span></span>
   * <span data-ttu-id="13d9a-153">**Listy kontroli dostępu - podsieci zdalnej**: 1.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="13d9a-153">**Access control list - Remote subnet**: 1.0.0.0/16</span></span>

     <span data-ttu-id="13d9a-154">Ten punkt końcowy ma publiczny port 80, które będzie kierować ruch do port prywatny 3000, gdzie serwer szyny nasłuchuje.</span><span class="sxs-lookup"><span data-stu-id="13d9a-154">This endpoint  has a public port of 80 that will route traffic to the private port of 3000, where the Rails server is listening.</span></span> <span data-ttu-id="13d9a-155">Reguły listy kontroli dostępu zezwala na publiczny ruch na porcie 80.</span><span class="sxs-lookup"><span data-stu-id="13d9a-155">The access control list rule allows public traffic on port 80.</span></span>

     ![nowy punkt końcowy](./media/virtual-machines-linux-classic-ruby-rails-web-app/createendpoint.png)

5. <span data-ttu-id="13d9a-157">Kliknij przycisk OK, aby zapisać punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="13d9a-157">Click OK to save the endpoint.</span></span>

6. <span data-ttu-id="13d9a-158">Komunikat powinien zostać wyświetlony stwierdzający **zapisywanie punktu końcowego maszyny wirtualnej**.</span><span class="sxs-lookup"><span data-stu-id="13d9a-158">A message should appear that states **Saving virtual machine endpoint**.</span></span> <span data-ttu-id="13d9a-159">Gdy ten komunikat nie zniknie, punkt końcowy jest aktywna.</span><span class="sxs-lookup"><span data-stu-id="13d9a-159">Once this message disappears, the endpoint is active.</span></span> <span data-ttu-id="13d9a-160">Może teraz przetestować aplikację, przechodząc do nazwę DNS maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="13d9a-160">You may now test your application by navigating to the DNS name of your virtual machine.</span></span> <span data-ttu-id="13d9a-161">Witryna sieci Web powinna wyglądać podobnie do następującego:</span><span class="sxs-lookup"><span data-stu-id="13d9a-161">The website should appear similar to the following:</span></span>

    ![Domyślna strona szyny][default-rails-cloud]

## <a name="next-steps"></a><span data-ttu-id="13d9a-163">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="13d9a-163">Next steps</span></span>
<span data-ttu-id="13d9a-164">W tym samouczku jak większość czynności ręcznie.</span><span class="sxs-lookup"><span data-stu-id="13d9a-164">In this tutorial, you did most of the steps manually.</span></span> <span data-ttu-id="13d9a-165">W środowisku produkcyjnym może napisać aplikację na komputerze deweloperskim i wdrożyć go na maszynie Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="13d9a-165">In a production environment, you would write your app on a development machine and deploy it to the Azure VM.</span></span> <span data-ttu-id="13d9a-166">Ponadto większość środowisk produkcyjnych hostowania aplikacji szyny w połączeniu z innym procesem serwera, takich jak Apache lub NginX, która obsługuje żądania routingu do wielu wystąpień aplikacji szyny i obsługująca zasoby statyczne.</span><span class="sxs-lookup"><span data-stu-id="13d9a-166">Also, most production environments host the Rails application in conjunction with another server process such as Apache or NginX, which handles request routing to multiple instances of the Rails application and serving static resources.</span></span> <span data-ttu-id="13d9a-167">Aby uzyskać więcej informacji zobacz http://rubyonrails.org/deploy/.</span><span class="sxs-lookup"><span data-stu-id="13d9a-167">For more information, see http://rubyonrails.org/deploy/.</span></span>

<span data-ttu-id="13d9a-168">Aby dowiedzieć się więcej na temat Ruby na szyny, odwiedź stronę [dopisków fonetycznych w przewodnikach szyny][rails-guides].</span><span class="sxs-lookup"><span data-stu-id="13d9a-168">To learn more about Ruby on Rails, visit the [Ruby on Rails Guides][rails-guides].</span></span>

<span data-ttu-id="13d9a-169">Aby korzystać z aplikacji dopisków fonetycznych usług Azure, zobacz:</span><span class="sxs-lookup"><span data-stu-id="13d9a-169">To use Azure services from your Ruby application, see:</span></span>

* <span data-ttu-id="13d9a-170">[Przechowywania danych niestrukturalnych przy użyciu obiektów blob][blobs]</span><span class="sxs-lookup"><span data-stu-id="13d9a-170">[Store unstructured data using blobs][blobs]</span></span>
* <span data-ttu-id="13d9a-171">[Pary klucz wartość magazynu przy użyciu tabel][tables]</span><span class="sxs-lookup"><span data-stu-id="13d9a-171">[Store key/value pairs using tables][tables]</span></span>
* <span data-ttu-id="13d9a-172">[Udostępniać zawartość dużej przepustowości w sieci dostarczania zawartości][cdn-howto]</span><span class="sxs-lookup"><span data-stu-id="13d9a-172">[Serve high bandwidth content with the Content Delivery Network][cdn-howto]</span></span>

<!-- WA.com links -->
[blobs]:../../../storage/blobs/storage-ruby-how-to-use-blob-storage.md
[cdn-howto]:https://azure.microsoft.com/develop/ruby/app-services/
[tables]:../../../cosmos-db/table-storage-how-to-use-ruby.md
[vm-instructions]:createportal.md

<!-- External Links -->
[rails-guides]:http://guides.rubyonrails.org/
[sqlite3]:http://www.sqlite.org/

<!-- Images -->

[default-rails-cloud]:./media/virtual-machines-linux-classic-ruby-rails-web-app/basicrailscloud.png
[vmlist]:./media/virtual-machines-linux-classic-ruby-rails-web-app/vmlist.png
[endpoints]:./media/virtual-machines-linux-classic-ruby-rails-web-app/endpoints.png
[new-endpoint]:./media/virtual-machines-linux-classic-ruby-rails-web-app/newendpoint.png
[new-endpoint1]:./media/virtual-machines-linux-classic-ruby-rails-web-app/newendpoint1.png
