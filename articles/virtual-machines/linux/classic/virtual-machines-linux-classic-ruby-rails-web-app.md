---
title: aaaHost Ruby w witrynie sieci Web szyny na maszynie Wirtualnej systemu Linux | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: c545c24fc6c89497854bbe55a6d0d1d0b072c386
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="ruby-on-rails-web-application-on-an-azure-vm"></a><span data-ttu-id="26172-103">Aplikacja sieci Web Ruby on Rails na maszynie wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="26172-103">Ruby on Rails Web application on an Azure VM</span></span>
<span data-ttu-id="26172-104">Ten samouczek pokazuje, jak toohost Ruby na szyny witryny sieci Web na platformie Azure przy użyciu maszyny wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="26172-104">This tutorial shows how toohost a Ruby on Rails website on Azure using a Linux virtual machine.</span></span>  

<span data-ttu-id="26172-105">W tym samouczku została zweryfikowana przy użyciu Ubuntu Server 14.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="26172-105">This tutorial was validated using Ubuntu Server 14.04 LTS.</span></span> <span data-ttu-id="26172-106">Jeśli używasz innej dystrybucji systemu Linux, może być konieczne toomodify hello kroki szyny tooinstall.</span><span class="sxs-lookup"><span data-stu-id="26172-106">If you use a different Linux distribution, you might need toomodify hello steps tooinstall Rails.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="26172-107">Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="26172-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="26172-108">W tym artykule omówiono przy użyciu hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="26172-108">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="26172-109">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="26172-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
>
>

## <a name="create-an-azure-vm"></a><span data-ttu-id="26172-110">Tworzenie maszyny Wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="26172-110">Create an Azure VM</span></span>
<span data-ttu-id="26172-111">Rozpocznij od utworzenia maszyny Wirtualnej platformy Azure z obrazem systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="26172-111">Start by creating an Azure VM with a Linux image.</span></span>

<span data-ttu-id="26172-112">toocreate hello maszyny Wirtualnej, można użyć hello portalu Azure lub hello Azure interfejsu wiersza polecenia (CLI).</span><span class="sxs-lookup"><span data-stu-id="26172-112">toocreate hello VM, you can use hello Azure portal or hello Azure Command-Line Interface (CLI).</span></span>

### <a name="azure-portal"></a><span data-ttu-id="26172-113">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="26172-113">Azure portal</span></span>
1. <span data-ttu-id="26172-114">Zaloguj się na powitania [portalu Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="26172-114">Sign into hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="26172-115">Kliknij przycisk **nowy**, wpisz "Ubuntu Server 14.04" hello pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="26172-115">Click **New**, then type "Ubuntu Server 14.04" in hello search box.</span></span> <span data-ttu-id="26172-116">Kliknij pozycję hello zwróconych hello wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="26172-116">Click hello entry returned by hello search.</span></span> <span data-ttu-id="26172-117">Wybierz model wdrażania hello, **klasycznego**, następnie kliknij przycisk "Utwórz".</span><span class="sxs-lookup"><span data-stu-id="26172-117">For hello deployment model, select **Classic**, then click "Create".</span></span>
3. <span data-ttu-id="26172-118">W bloku podstawy hello, podaj wartości dla pól wymaganych hello: Nazwa (hello maszyny Wirtualnej), nazwę użytkownika, typ uwierzytelniania i hello odpowiednie poświadczenia, subskrypcji platformy Azure, grupy zasobów i lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="26172-118">In hello Basics blade, supply values for hello required fields: Name (for hello VM), User name, Authentication type and hello corresponding credentials, Azure subscription, Resource group, and Location.</span></span>

   ![Utwórz nowy obraz Ubuntu](./media/virtual-machines-linux-classic-ruby-rails-web-app/createvm.png)

4. <span data-ttu-id="26172-120">Po udostępnieniu hello maszyny Wirtualnej, kliknij nazwę maszyny Wirtualnej hello i kliknij przycisk **punkty końcowe** w hello **ustawienia** kategorii.</span><span class="sxs-lookup"><span data-stu-id="26172-120">After hello VM is provisioned, click on hello VM name, and click **Endpoints** in hello **Settings** category.</span></span> <span data-ttu-id="26172-121">Znajdź hello punkt końcowy SSH, kategorii **autonomiczny**.</span><span class="sxs-lookup"><span data-stu-id="26172-121">Find hello SSH endpoint, listed under **Standalone**.</span></span>

   ![Domyślny punkt końcowy](./media/virtual-machines-linux-classic-ruby-rails-web-app/endpointsnewportal.png)

### <a name="azure-cli"></a><span data-ttu-id="26172-123">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="26172-123">Azure CLI</span></span>
<span data-ttu-id="26172-124">Wykonaj kroki hello w [tworzenia maszyny wirtualnej systemem Linux][vm-instructions].</span><span class="sxs-lookup"><span data-stu-id="26172-124">Follow hello steps in [Create a Virtual Machine Running Linux][vm-instructions].</span></span>

<span data-ttu-id="26172-125">Po udostępnieniu hello maszyny Wirtualnej można uzyskać, uruchamiając następujące polecenie hello punkt końcowy SSH hello:</span><span class="sxs-lookup"><span data-stu-id="26172-125">After hello VM is provisioned, you can get hello SSH endpoint by running hello following command:</span></span>

    azure vm endpoint list <vm-name>  

## <a name="install-ruby-on-rails"></a><span data-ttu-id="26172-126">Zainstaluj na szyny Ruby</span><span class="sxs-lookup"><span data-stu-id="26172-126">Install Ruby on Rails</span></span>
1. <span data-ttu-id="26172-127">Użyj toohello tooconnect SSH maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="26172-127">Use SSH tooconnect toohello VM.</span></span>
2. <span data-ttu-id="26172-128">Hello sesji SSH używając hello, wykonując polecenia tooinstall Ruby na powitania maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="26172-128">From hello SSH session, use hello following commands tooinstall Ruby on hello VM:</span></span>

        sudo apt-get update -y
        sudo apt-get upgrade -y

        sudo apt-add-repository ppa:brightbox/ruby-ng
        sudo apt-get update
        sudo apt-get install ruby2.4

        > [!TIP]
        > hello brightbox repository contains hello current Ruby distribution.

    <span data-ttu-id="26172-129">Witaj, instalacja może zająć kilka minut.</span><span class="sxs-lookup"><span data-stu-id="26172-129">hello installation may take a few minutes.</span></span> <span data-ttu-id="26172-130">Po ukończeniu, należy użyć powitania po tooverify polecenia zainstalowano Ruby:</span><span class="sxs-lookup"><span data-stu-id="26172-130">When it completes, use hello following command tooverify that Ruby is installed:</span></span>

        ruby -v

3. <span data-ttu-id="26172-131">Użyj hello następujące polecenie szyny tooinstall:</span><span class="sxs-lookup"><span data-stu-id="26172-131">Use hello following command tooinstall Rails:</span></span>

        sudo gem install rails --no-rdoc --no-ri -V

    <span data-ttu-id="26172-132">Użyj hello--nie rdoc i--nie ri flagi tooskip instalowanie dokumentacji hello jest szybszy.</span><span class="sxs-lookup"><span data-stu-id="26172-132">Use hello --no-rdoc and --no-ri flags tooskip installing hello documentation, which is faster.</span></span>
    <span data-ttu-id="26172-133">To polecenie będzie może zająć dużo czasu tooexecute, więc Dodawanie hello -V zostaną wyświetlone informacje o postępie instalacji hello.</span><span class="sxs-lookup"><span data-stu-id="26172-133">This command will likely take a long time tooexecute, so adding hello -V will display information about hello installation progress.</span></span>

## <a name="create-and-run-an-app"></a><span data-ttu-id="26172-134">Tworzenie i uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="26172-134">Create and run an app</span></span>
<span data-ttu-id="26172-135">Jest nadal zalogowany za pośrednictwem protokołu SSH, uruchom następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="26172-135">While still logged in via SSH, run hello following commands:</span></span>

    rails new myapp
    cd myapp
    rails server -b 0.0.0.0 -p 3000

<span data-ttu-id="26172-136">Witaj [nowe](http://guides.rubyonrails.org/command_line.html#rails-new) polecenie tworzy nową aplikację szyny.</span><span class="sxs-lookup"><span data-stu-id="26172-136">hello [new](http://guides.rubyonrails.org/command_line.html#rails-new) command creates a new Rails app.</span></span> <span data-ttu-id="26172-137">Witaj [serwera](http://guides.rubyonrails.org/command_line.html#rails-server) polecenie uruchamia hello serwera sieci web WEBrick dołączony do szyny.</span><span class="sxs-lookup"><span data-stu-id="26172-137">hello [server](http://guides.rubyonrails.org/command_line.html#rails-server) command starts hello WEBrick web server that comes with Rails.</span></span> <span data-ttu-id="26172-138">(Do użytku produkcyjnego prawdopodobnie odpowiedni będzie toouse innego serwera, takie jak Unicorn lub pasażerów.)</span><span class="sxs-lookup"><span data-stu-id="26172-138">(For production use, you would probably want toouse a different server, such as Unicorn or Passenger.)</span></span>

<span data-ttu-id="26172-139">Powinny pojawić się dane wyjściowe podobne toohello poniżej.</span><span class="sxs-lookup"><span data-stu-id="26172-139">You should see output similar toohello following.</span></span>

    => Booting WEBrick
    => Rails 4.2.1 application starting in development on http://0.0.0.0:3000
    => Run `rails server -h` for more startup options
    => Ctrl-C tooshutdown server
    [2015-06-09 23:34:23] INFO  WEBrick 1.3.1
    [2015-06-09 23:34:23] INFO  ruby 1.9.3 (2013-11-22) [x86_64-linux]
    [2015-06-09 23:34:23] INFO  WEBrick::HTTPServer#start: pid=27766 port=3000

## <a name="add-an-endpoint"></a><span data-ttu-id="26172-140">Dodawanie punktu końcowego</span><span class="sxs-lookup"><span data-stu-id="26172-140">Add an endpoint</span></span>
1. <span data-ttu-id="26172-141">Przejdź toohello [portalu Azure] [https://portal.azure.com] i wybierz maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="26172-141">Go toohello [Azure portal][https://portal.azure.com] and select your VM.</span></span>

2. <span data-ttu-id="26172-142">Wybierz **punkty końcowe** w hello **ustawienia** wzdłuż hello lewej krawędzi hello strony.</span><span class="sxs-lookup"><span data-stu-id="26172-142">Select **ENDPOINTS** in hello **Settings** along hello left edge hello page.</span></span>

3. <span data-ttu-id="26172-143">Kliknij przycisk **dodać** u góry hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="26172-143">Click **ADD** at hello top of hello page.</span></span>

4. <span data-ttu-id="26172-144">W hello **dodać punkt końcowy** okna dialogowego wprowadź hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="26172-144">In hello **Add endpoint** dialog page, enter hello following information:</span></span>

   * <span data-ttu-id="26172-145">**Nazwa**: HTTP</span><span class="sxs-lookup"><span data-stu-id="26172-145">**Name**: HTTP</span></span>
   * <span data-ttu-id="26172-146">**Protokół**: TCP</span><span class="sxs-lookup"><span data-stu-id="26172-146">**Protocol**: TCP</span></span>
   * <span data-ttu-id="26172-147">**Port publiczny**: 80</span><span class="sxs-lookup"><span data-stu-id="26172-147">**Public port**: 80</span></span>
   * <span data-ttu-id="26172-148">**Port prywatny**: 3000</span><span class="sxs-lookup"><span data-stu-id="26172-148">**Private port**: 3000</span></span>
   * <span data-ttu-id="26172-149">**Pływającego adresu PI**: wyłączone</span><span class="sxs-lookup"><span data-stu-id="26172-149">**Floating PI address**: Disabled</span></span>
   * <span data-ttu-id="26172-150">**Listy kontroli dostępu — kolejność**: 1001 lub inną wartość, która ustawia hello priorytet tej reguły dostępu.</span><span class="sxs-lookup"><span data-stu-id="26172-150">**Access control list - Order**: 1001, or another value that sets hello priority of this access rule.</span></span>
   * <span data-ttu-id="26172-151">**Listy kontroli dostępu — nazwa**: allowHTTP</span><span class="sxs-lookup"><span data-stu-id="26172-151">**Access control list - Name**: allowHTTP</span></span>
   * <span data-ttu-id="26172-152">**Listy kontroli dostępu — Akcja**: Zezwalaj</span><span class="sxs-lookup"><span data-stu-id="26172-152">**Access control list - Action**: permit</span></span>
   * <span data-ttu-id="26172-153">**Listy kontroli dostępu - podsieci zdalnej**: 1.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="26172-153">**Access control list - Remote subnet**: 1.0.0.0/16</span></span>

     <span data-ttu-id="26172-154">Ten punkt końcowy ma publiczny port 80, który skieruje ruchu toohello port prywatny 3000, gdzie hello szyny serwer nasłuchuje.</span><span class="sxs-lookup"><span data-stu-id="26172-154">This endpoint  has a public port of 80 that will route traffic toohello private port of 3000, where hello Rails server is listening.</span></span> <span data-ttu-id="26172-155">reguły listy kontroli dostępu Hello umożliwia publiczny ruch na porcie 80.</span><span class="sxs-lookup"><span data-stu-id="26172-155">hello access control list rule allows public traffic on port 80.</span></span>

     ![nowy punkt końcowy](./media/virtual-machines-linux-classic-ruby-rails-web-app/createendpoint.png)

5. <span data-ttu-id="26172-157">Kliknij przycisk OK toosave hello endpoint.</span><span class="sxs-lookup"><span data-stu-id="26172-157">Click OK toosave hello endpoint.</span></span>

6. <span data-ttu-id="26172-158">Komunikat powinien zostać wyświetlony stwierdzający **zapisywanie punktu końcowego maszyny wirtualnej**.</span><span class="sxs-lookup"><span data-stu-id="26172-158">A message should appear that states **Saving virtual machine endpoint**.</span></span> <span data-ttu-id="26172-159">Gdy ten komunikat nie zniknie, punktu końcowego hello jest aktywna.</span><span class="sxs-lookup"><span data-stu-id="26172-159">Once this message disappears, hello endpoint is active.</span></span> <span data-ttu-id="26172-160">Może teraz przetestować aplikację, przechodząc toohello nazwę DNS maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="26172-160">You may now test your application by navigating toohello DNS name of your virtual machine.</span></span> <span data-ttu-id="26172-161">Hello witryny sieci Web powinna wyglądać podobnie toohello następujące:</span><span class="sxs-lookup"><span data-stu-id="26172-161">hello website should appear similar toohello following:</span></span>

    ![Domyślna strona szyny][default-rails-cloud]

## <a name="next-steps"></a><span data-ttu-id="26172-163">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="26172-163">Next steps</span></span>
<span data-ttu-id="26172-164">W tym samouczku jak większość kroków hello ręcznie.</span><span class="sxs-lookup"><span data-stu-id="26172-164">In this tutorial, you did most of hello steps manually.</span></span> <span data-ttu-id="26172-165">W środowisku produkcyjnym może napisać aplikację na komputerze deweloperskim i wdrożyć ją toohello maszyny Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="26172-165">In a production environment, you would write your app on a development machine and deploy it toohello Azure VM.</span></span> <span data-ttu-id="26172-166">Ponadto większość środowisk produkcyjnych hostowanie aplikacji szyny hello w połączeniu z innym procesem serwera, takich jak Apache lub NginX, która obsługuje żądania routingu wystąpień toomultiple hello szyny aplikacji oraz obsługująca zasoby statyczne.</span><span class="sxs-lookup"><span data-stu-id="26172-166">Also, most production environments host hello Rails application in conjunction with another server process such as Apache or NginX, which handles request routing toomultiple instances of hello Rails application and serving static resources.</span></span> <span data-ttu-id="26172-167">Aby uzyskać więcej informacji zobacz http://rubyonrails.org/deploy/.</span><span class="sxs-lookup"><span data-stu-id="26172-167">For more information, see http://rubyonrails.org/deploy/.</span></span>

<span data-ttu-id="26172-168">toolearn więcej informacji na temat Ruby na szyny, odwiedź stronę hello [dopisków fonetycznych w przewodnikach szyny][rails-guides].</span><span class="sxs-lookup"><span data-stu-id="26172-168">toolearn more about Ruby on Rails, visit hello [Ruby on Rails Guides][rails-guides].</span></span>

<span data-ttu-id="26172-169">toouse Azure usług z aplikacji dopisków fonetycznych, zobacz:</span><span class="sxs-lookup"><span data-stu-id="26172-169">toouse Azure services from your Ruby application, see:</span></span>

* <span data-ttu-id="26172-170">[Przechowywania danych niestrukturalnych przy użyciu obiektów blob][blobs]</span><span class="sxs-lookup"><span data-stu-id="26172-170">[Store unstructured data using blobs][blobs]</span></span>
* <span data-ttu-id="26172-171">[Pary klucz wartość magazynu przy użyciu tabel][tables]</span><span class="sxs-lookup"><span data-stu-id="26172-171">[Store key/value pairs using tables][tables]</span></span>
* <span data-ttu-id="26172-172">[Obsługiwać zawartości wysokiej przepustowości z hello sieci dostarczania zawartości][cdn-howto]</span><span class="sxs-lookup"><span data-stu-id="26172-172">[Serve high bandwidth content with hello Content Delivery Network][cdn-howto]</span></span>

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
