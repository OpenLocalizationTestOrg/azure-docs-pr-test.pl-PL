---
title: aaaDeploy tooLinux aplikacji Node.js maszyn wirtualnych na platformie Azure
description: "Dowiedz się, jak toodeploy Node.js maszyn wirtualnych tooLinux aplikacji na platformie Azure."
services: 
documentationcenter: nodejs
author: stepro
manager: dmitryr
editor: 
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: /azure
ms.assetid: 857a812d-c73e-4af7-a985-2d0baf8b6f71
ms.service: multiple
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2016
ms.author: stephpr
ms.openlocfilehash: e876c8170a06f102f7f32ec7cb930b876647a707
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-nodejs-application-toolinux-virtual-machines-in-azure"></a><span data-ttu-id="9423a-103">Wdrażanie tooLinux aplikacji Node.js maszyn wirtualnych na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="9423a-103">Deploy a Node.js application tooLinux Virtual Machines in Azure</span></span>
<span data-ttu-id="9423a-104">Ten samouczek pokazuje, jak tootake aplikacji Node.js i wdróż je tooLinux maszyn wirtualnych działających na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="9423a-104">This tutorial shows how tootake a Node.js application and deploy it tooLinux virtual machines running in Azure.</span></span> <span data-ttu-id="9423a-105">Witaj instrukcje w tym samouczku można wykonać w dowolnym systemie operacyjnym, który jest w stanie uruchomić środowisko Node.js.</span><span class="sxs-lookup"><span data-stu-id="9423a-105">hello instructions in this tutorial can be followed on any operating system that is capable of running Node.js.</span></span>

<span data-ttu-id="9423a-106">Dowiesz się, jak:</span><span class="sxs-lookup"><span data-stu-id="9423a-106">You'll learn how to:</span></span>

* <span data-ttu-id="9423a-107">Rozwidlenia i klonowania repozytorium GitHub zawierające prostej aplikacji TODO;</span><span class="sxs-lookup"><span data-stu-id="9423a-107">Fork and clone a GitHub repository containing a simple TODO application;</span></span>
* <span data-ttu-id="9423a-108">Tworzenie i konfigurowanie aplikacji hello Azure toorun; dwóch maszyn wirtualnych systemu Linux</span><span class="sxs-lookup"><span data-stu-id="9423a-108">Create and configure two Linux virtual machines in Azure toorun hello application;</span></span>
* <span data-ttu-id="9423a-109">Iterowanie w aplikacji hello przesyłając maszyny wirtualnej frontonu sieci web toohello aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="9423a-109">Iterate on hello application by pushing updates toohello web frontend virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="9423a-110">toocomplete tego samouczka wymagane konto usługi GitHub i konto Microsoft Azure i hello możliwości toouse Git z komputerze deweloperskim.</span><span class="sxs-lookup"><span data-stu-id="9423a-110">toocomplete this tutorial, you need a GitHub account and a Microsoft Azure account, and hello ability toouse Git from a development machine.</span></span>
> 
> <span data-ttu-id="9423a-111">Jeśli nie masz konto GitHub, można założyć [tutaj](https://github.com/join).</span><span class="sxs-lookup"><span data-stu-id="9423a-111">If you don't have a GitHub account, you can sign up [here](https://github.com/join).</span></span>
> 
> <span data-ttu-id="9423a-112">Jeśli nie masz [Microsoft Azure](https://azure.microsoft.com/) konta, można założyć bezpłatnej wersji próbnej [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9423a-112">If you don't have a [Microsoft Azure](https://azure.microsoft.com/) account, you can sign up for a FREE trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="9423a-113">To również przeprowadzi Cię przez proces dla tworzenia konta hello [Account Microsoft](http://account.microsoft.com) Jeśli użytkownik nie ma jeszcze jednej.</span><span class="sxs-lookup"><span data-stu-id="9423a-113">This will also lead you through hello sign up process for a [Microsoft Account](http://account.microsoft.com) if you do not already have one.</span></span> <span data-ttu-id="9423a-114">W przypadku subskrybentów programu Visual Studio można też [Aktywuj swoje korzyści MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="9423a-114">Alternatively, if you are a Visual Studio subscriber, you can [activate your MSDN benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>
> 
> <span data-ttu-id="9423a-115">Jeśli nie masz git na komputerze deweloperskim, to jeśli używasz komputera Macintosh lub Windows zainstaluj z usługi git [tutaj](http://www.git-scm.com).</span><span class="sxs-lookup"><span data-stu-id="9423a-115">If you do not have git on your development machine, then if you are using a Macintosh or Windows machine, install git from [here](http://www.git-scm.com).</span></span> <span data-ttu-id="9423a-116">Jeśli używasz systemu Linux, zainstaluj usługę git przy użyciu mechanizmu hello najbardziej odpowiednie dla Ciebie, takich jak `sudo apt-get install git`.</span><span class="sxs-lookup"><span data-stu-id="9423a-116">If you are using Linux, install git using hello mechanism most appropriate for you, such as `sudo apt-get install git`.</span></span>
> 
> 

## <a name="forking-and-cloning-hello-todo-application"></a><span data-ttu-id="9423a-117">Rozwidlania i klonowania hello aplikacji TODO</span><span class="sxs-lookup"><span data-stu-id="9423a-117">Forking and Cloning hello TODO Application</span></span>
<span data-ttu-id="9423a-118">Hello aplikacji TODO, w tym samouczku implementuje frontonu sieci web prostego przez wystąpienie bazy danych MongoDB, który śledzi lista czynności do wykonania.</span><span class="sxs-lookup"><span data-stu-id="9423a-118">hello TODO application used by this tutorial implements a simple web frontend over a MongoDB instance that keeps track of a TODO list.</span></span> <span data-ttu-id="9423a-119">Po zalogowaniu tooGitHub Przejdź [tutaj](https://github.com/stepro/node-todo) toofind hello aplikacji i rozwidlania przy użyciu łącza hello w hello w prawym górnym narożniku.</span><span class="sxs-lookup"><span data-stu-id="9423a-119">After signing in tooGitHub, go [here](https://github.com/stepro/node-todo) toofind hello application and fork it using hello link in hello top right.</span></span> <span data-ttu-id="9423a-120">Ten należy utworzyć repozytorium na koncie o nazwie *accountname*/node-todo.</span><span class="sxs-lookup"><span data-stu-id="9423a-120">This should create a repository in your account named *accountname*/node-todo.</span></span>

<span data-ttu-id="9423a-121">Teraz na komputerze deweloperskim Klonuj to repozytorium:</span><span class="sxs-lookup"><span data-stu-id="9423a-121">Now on your development machine, clone this repository:</span></span>

    git clone https://github.com/accountname/node-todo.git

<span data-ttu-id="9423a-122">Użyjemy tego klonu lokalnego repozytorium hello nieco później podczas wprowadzania zmian w kodzie źródłowym toohello.</span><span class="sxs-lookup"><span data-stu-id="9423a-122">We'll use this local clone of hello repository a little later when making changes toohello source code.</span></span>

## <a name="creating-and-configuring-hello-linux-virtual-machines"></a><span data-ttu-id="9423a-123">Tworzenie i konfigurowanie hello maszyn wirtualnych systemu Linux</span><span class="sxs-lookup"><span data-stu-id="9423a-123">Creating and Configuring hello Linux Virtual Machines</span></span>
<span data-ttu-id="9423a-124">Platforma Azure ma doskonałą pomoc techniczną dla nieprzetworzonej obliczeń przy użyciu maszyn wirtualnych systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="9423a-124">Azure has great support for raw compute using Linux virtual machines.</span></span> <span data-ttu-id="9423a-125">Ta część hello samouczek pokazuje, jak można łatwo aż dwóch maszyn wirtualnych systemu Linux i wdrożyć toothem aplikacji hello TODO, systemem hello frontonu sieci web na jednym i hello wystąpienie bazy danych MongoDB na powitania innych.</span><span class="sxs-lookup"><span data-stu-id="9423a-125">This part of hello tutorial shows how you can easily spin up two Linux virtual machines and deploy hello TODO application toothem, running hello web frontend on one and hello MongoDB instance on hello other.</span></span>

### <a name="creating-virtual-machines"></a><span data-ttu-id="9423a-126">Tworzenie maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="9423a-126">Creating Virtual Machines</span></span>
<span data-ttu-id="9423a-127">Witaj najprostszy sposób toocreate nowej maszyny wirtualnej na platformie Azure jest hello toouse portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="9423a-127">hello easiest way toocreate a new virtual machine in Azure is toouse hello Azure Portal.</span></span> <span data-ttu-id="9423a-128">Kliknij przycisk [tutaj](https://portal.azure.com) toosign w, a następnie uruchom hello portalu Azure w przeglądarce sieci web.</span><span class="sxs-lookup"><span data-stu-id="9423a-128">Click [here](https://portal.azure.com) toosign in and launch hello Azure Portal in your web browser.</span></span> <span data-ttu-id="9423a-129">Po załadowaniu hello portalu Azure, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="9423a-129">Once hello Azure Portal has loaded, complete hello following steps:</span></span>

* <span data-ttu-id="9423a-130">Kliknij przycisk hello "+ nowy" link;</span><span class="sxs-lookup"><span data-stu-id="9423a-130">Click hello "+ New" link;</span></span>
* <span data-ttu-id="9423a-131">Wybierz kategorię "Obliczeniowe" hello, a następnie wybierz pozycję "Ubuntu Server 14.04 LTS";</span><span class="sxs-lookup"><span data-stu-id="9423a-131">Pick hello "Compute" category and choose "Ubuntu Server 14.04 LTS";</span></span>
* <span data-ttu-id="9423a-132">Wybierz model wdrażania "Resource Manager" hello, a następnie kliknij przycisk "Utwórz";</span><span class="sxs-lookup"><span data-stu-id="9423a-132">Select hello "Resource Manager" deployment model and click "Create";</span></span>
* <span data-ttu-id="9423a-133">Wypełnij podstawy hello poniższych wskazówek:</span><span class="sxs-lookup"><span data-stu-id="9423a-133">Fill in hello basics following these guidelines:</span></span>
  * <span data-ttu-id="9423a-134">Określ nazwę, którą można było później łatwo rozpoznać;</span><span class="sxs-lookup"><span data-stu-id="9423a-134">Specify a name you can easily identify later;</span></span>
  * <span data-ttu-id="9423a-135">W tym samouczku wybierz uwierzytelnianie hasła;</span><span class="sxs-lookup"><span data-stu-id="9423a-135">For this tutorial, choose Password authentication;</span></span>
  * <span data-ttu-id="9423a-136">Utwórz nową grupę zasobów o nazwie do zidentyfikowania.</span><span class="sxs-lookup"><span data-stu-id="9423a-136">Create a new resource group with an identifiable name.</span></span>
* <span data-ttu-id="9423a-137">Hello rozmiar maszyny wirtualnej "A1 Standard" jest uzasadnione wybór dla tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="9423a-137">For hello Virtual Machine size, "A1 Standard" is a reasonable choice for this tutorial.</span></span>
* <span data-ttu-id="9423a-138">Dodatkowe ustawienia upewnij się, że "Standard" hello, typ dysku i zaakceptować hello wszystkie pozostałe wartości domyślne.</span><span class="sxs-lookup"><span data-stu-id="9423a-138">For additional settings, ensure hello disk type is "Standard" and accept all hello remaining defaults.</span></span>
* <span data-ttu-id="9423a-139">Rozpocząć poza tworzenia hello na stronie podsumowania hello.</span><span class="sxs-lookup"><span data-stu-id="9423a-139">Kick off hello creation on hello summary page.</span></span>

<span data-ttu-id="9423a-140">Wykonaj powyższe hello przetwarzania dwukrotnie toocreate dwóch maszyn wirtualnych systemu Linux, jeden dla hello frontonu sieci web i jeden dla hello wystąpienie bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="9423a-140">Perform hello above process twice toocreate two Linux virtual machines, one for hello web frontend and one for hello MongoDB instance.</span></span> <span data-ttu-id="9423a-141">Tworzenie maszyn wirtualnych hello potrwa około 5 – 10 minut.</span><span class="sxs-lookup"><span data-stu-id="9423a-141">Creation of hello virtual machines will take about 5-10 minutes.</span></span>

### <a name="assigning-a-dns-entry-for-virtual-machines"></a><span data-ttu-id="9423a-142">Przypisywanie wpis DNS dla maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="9423a-142">Assigning a DNS entry for Virtual Machines</span></span>
<span data-ttu-id="9423a-143">Maszyny wirtualne utworzone na platformie Azure są domyślnie dostępne tylko za pośrednictwem publicznego adresu IP, takich jak 1.2.3.4.</span><span class="sxs-lookup"><span data-stu-id="9423a-143">Virtual machines created in Azure are by default only accessible through a public IP address like 1.2.3.4.</span></span> <span data-ttu-id="9423a-144">Upewnijmy maszyny hello identyfikacji przez przypisywanie ich wpisy DNS.</span><span class="sxs-lookup"><span data-stu-id="9423a-144">Let's make hello machines more easily identifiable by assigning them DNS entries.</span></span>

<span data-ttu-id="9423a-145">Po portalu hello wskazuje, czy hello maszyny wirtualnej zostały utworzone, kliknij łącze "Maszyny wirtualnej" hello w lewy pasek nawigacyjny hello, a następnie zlokalizuj maszynach.</span><span class="sxs-lookup"><span data-stu-id="9423a-145">Once hello portal indicates that hello virtual machines have been created, click on hello "Virtual machines" link in hello left navbar and locate your machines.</span></span> <span data-ttu-id="9423a-146">Dla każdego komputera:</span><span class="sxs-lookup"><span data-stu-id="9423a-146">For each machine:</span></span>

* <span data-ttu-id="9423a-147">Karta Essentials hello zlokalizuj i kliknij pozycję hello publicznego adresu IP;</span><span class="sxs-lookup"><span data-stu-id="9423a-147">Locate hello Essentials tab and click on hello Public IP Address;</span></span>
* <span data-ttu-id="9423a-148">W hello publiczny adres IP należy przypisać etykieta nazwy DNS i Zapisz.</span><span class="sxs-lookup"><span data-stu-id="9423a-148">In hello public IP address configuration, assign a DNS name label and save.</span></span>

<span data-ttu-id="9423a-149">Hello portal będzie upewnij się, czy nazwa hello przez użytkownika jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="9423a-149">hello portal will ensure that hello name you specify is available.</span></span> <span data-ttu-id="9423a-150">Po zapisaniu konfiguracji hello, maszyn wirtualnych będą mieć nazwy hosta, które są podobne zbyt`machinename.region.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="9423a-150">After saving hello configuration, your virtual machines will have host names similar too`machinename.region.cloudapp.azure.com`.</span></span>

### <a name="connecting-toohello-virtual-machines"></a><span data-ttu-id="9423a-151">Łączenie toohello maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="9423a-151">Connecting toohello Virtual Machines</span></span>
<span data-ttu-id="9423a-152">Gdy udostępnionych maszynach wirtualnych, były tooallow wstępnie skonfigurowane zdalne połączenia za pomocą protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="9423a-152">When your virtual machines were provisioned, they were pre-configured tooallow remote connections over SSH.</span></span> <span data-ttu-id="9423a-153">Jest to mechanizm hello będziemy używać maszyn wirtualnych hello tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="9423a-153">This is hello mechanism we will use tooconfigure hello virtual machines.</span></span> <span data-ttu-id="9423a-154">Jeśli używasz systemu Windows na komputerze, należy tooget klienta SSH, jeśli użytkownik nie ma jeszcze jednej.</span><span class="sxs-lookup"><span data-stu-id="9423a-154">If you are using Windows for your development, you will need tooget an SSH client if you do not already have one.</span></span> <span data-ttu-id="9423a-155">Programu PuTTY, który można pobrać z jest tutaj wspólnej wybór [tutaj](http://www.chiark.greenend.org.uk/~sgtatham/putty/).</span><span class="sxs-lookup"><span data-stu-id="9423a-155">A common choice here is PuTTY, which can be downloaded from [here](http://www.chiark.greenend.org.uk/~sgtatham/putty/).</span></span> <span data-ttu-id="9423a-156">Przy użyciu wersji SSH preinstalowanym pochodzą Macintosh i systemów operacyjnych Linux.</span><span class="sxs-lookup"><span data-stu-id="9423a-156">Macintosh and Linux OSes come with a version of SSH pre-installed.</span></span>

### <a name="configuring-hello-web-frontend-virtual-machine"></a><span data-ttu-id="9423a-157">Konfigurowanie hello maszyny wirtualnej frontonu sieci Web</span><span class="sxs-lookup"><span data-stu-id="9423a-157">Configuring hello Web Frontend Virtual Machine</span></span>
<span data-ttu-id="9423a-158">Maszyna frontonu sieci web toohello SSH utworzonych przy użyciu programu PuTTY, ssh wiersza polecenia lub innych ulubionego narzędzia SSH.</span><span class="sxs-lookup"><span data-stu-id="9423a-158">SSH toohello web frontend machine you created using PuTTY, ssh command line or your other favorite SSH tool.</span></span> <span data-ttu-id="9423a-159">Powinien zostać wyświetlony komunikat powitalny, a następnie w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="9423a-159">You should see a welcome message followed by a command prompt.</span></span>

<span data-ttu-id="9423a-160">Po pierwsze upewnijmy się, że git i węzła zainstalowano:</span><span class="sxs-lookup"><span data-stu-id="9423a-160">First, let's make sure that git and node are both installed:</span></span>

    sudo apt-get install -y git
    curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
    sudo apt-get install -y nodejs

<span data-ttu-id="9423a-161">Ponieważ frontonu sieci web aplikacji hello opiera się na niektórych modułów macierzystych Node.js, potrzebujemy również tooinstall hello niezbędny zestaw narzędzi kompilacji:</span><span class="sxs-lookup"><span data-stu-id="9423a-161">Since hello application's web frontend relies on some native Node.js modules, we also need tooinstall hello essential set of build tools:</span></span>

    sudo apt-get install -y build-essential

<span data-ttu-id="9423a-162">Na koniec zainstalujmy aplikację Node.js o nazwie *nieskończona*, co pozwala aplikacji serwerowych toorun Node.js:</span><span class="sxs-lookup"><span data-stu-id="9423a-162">Finally, let's install a Node.js application called *forever*, which helps toorun Node.js server applications:</span></span>

    sudo npm install -g forever

<span data-ttu-id="9423a-163">Są to wszystkie zależności hello na tej maszyny wirtualnej toobe toorun stanie hello aplikacji frontonu sieci web, więc korzystaj z systemem.</span><span class="sxs-lookup"><span data-stu-id="9423a-163">These are all hello dependencies needed on this virtual machine toobe able toorun hello application's web frontend, so let's get that running.</span></span> <span data-ttu-id="9423a-164">toodo, najpierw utworzymy systemu od zera klonowania repozytorium GitHub hello wcześniej rozwidlone tak, aby łatwo opublikować maszyny wirtualnej toohello aktualizacji (omówione zostaną następujące czynności w tym scenariuszu aktualizacji później), a następnie sklonować tooprovide systemu od zera klonowania hello wersji hello repozytorium, który faktycznie może zostać wykonany.</span><span class="sxs-lookup"><span data-stu-id="9423a-164">toodo this, we will first create a bare clone of hello GitHub repository you previously forked so that you can easily publish updates toohello virtual machine (we'll cover this update scenario later), and then clone hello bare clone tooprovide a version of hello repository that can actually be executed.</span></span>

<span data-ttu-id="9423a-165">Począwszy od hello katalog macierzysty (~), uruchom następujące polecenia hello (zastępowanie *accountname* z nazwą konta użytkownika usługi GitHub):</span><span class="sxs-lookup"><span data-stu-id="9423a-165">Starting from hello home (~) directory, run hello following commands (replacing *accountname* with your GitHub user account name):</span></span>

    git clone --bare https://github.com/accountname/node-todo.git
    git clone node-todo.git

<span data-ttu-id="9423a-166">Teraz wprowadź hello todo węzeł katalog i uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="9423a-166">Now enter hello node-todo directory and run these commands:</span></span>

    npm install
    forever start server.js

<span data-ttu-id="9423a-167">Witaj aplikacji frontonu sieci web jest teraz uruchomiona, jednak jest jeden krok w celu uzyskania dostępu do aplikacji hello z przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="9423a-167">hello application's web frontend is now running, however there is one more step before you can access hello application from a web browser.</span></span> <span data-ttu-id="9423a-168">Witaj tworzenia maszyny wirtualnej jest chroniony przez zasobów platformy Azure o nazwie *grupy zabezpieczeń sieci*, który został utworzony dla hello podczas aprowizowanej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9423a-168">hello virtual machine you created is protected by an Azure resource called a *network security group*, which was created for you when you provisioned hello virtual machine.</span></span> <span data-ttu-id="9423a-169">Obecnie ten zasób umożliwia zewnętrznych żądań tooport 22 toobe kierowane toohello maszynę wirtualną, która umożliwia komunikacji SSH z hello maszyny, ale nic.</span><span class="sxs-lookup"><span data-stu-id="9423a-169">Currently, this resource only allows external requests tooport 22 toobe routed toohello virtual machine, which enables SSH communication with hello machine but nothing else.</span></span> <span data-ttu-id="9423a-170">Dlatego w kolejności tooview hello aplikacji TODO, które są skonfigurowane toorun portu 8080, ten port musi także toobe otwarte.</span><span class="sxs-lookup"><span data-stu-id="9423a-170">So in order tooview hello TODO application, which is configured toorun on port 8080, this port also needs toobe opened up.</span></span>

<span data-ttu-id="9423a-171">Zwraca toohello portalu Azure i ukończyć powitalnych następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="9423a-171">Return toohello Azure Portal and complete hello following steps:</span></span>

* <span data-ttu-id="9423a-172">Kliknij pozycję "Grupy zasobów" hello lewy pasek nawigacyjny;</span><span class="sxs-lookup"><span data-stu-id="9423a-172">Click on "Resource groups" in hello left navbar;</span></span>
* <span data-ttu-id="9423a-173">Wybierz grupę zasobów hello, który zawiera maszyny wirtualnej;</span><span class="sxs-lookup"><span data-stu-id="9423a-173">Select hello resource group that contains your virtual machine;</span></span>
* <span data-ttu-id="9423a-174">Hello wynikowej listy zasobów wybierz grupę zabezpieczeń sieci hello (hello jedną z ikona tarczy);</span><span class="sxs-lookup"><span data-stu-id="9423a-174">In hello resulting list of resources, select hello network security group (hello one with a shield icon);</span></span>
* <span data-ttu-id="9423a-175">W oknie dialogowym właściwości hello wybierz "zasady zabezpieczeń dla ruchu przychodzącego";</span><span class="sxs-lookup"><span data-stu-id="9423a-175">In hello properties, choose "Inbound security rules";</span></span>
* <span data-ttu-id="9423a-176">Witaj pasku narzędzi kliknij przycisk "Dodaj";</span><span class="sxs-lookup"><span data-stu-id="9423a-176">In hello toolbar, click "Add";</span></span>
* <span data-ttu-id="9423a-177">Podaj nazwę, takich jak "domyślny — Zezwalaj todo";</span><span class="sxs-lookup"><span data-stu-id="9423a-177">Provide a name like "default-allow-todo";</span></span>
* <span data-ttu-id="9423a-178">Ustawienie zbyt protokołu hello "TCP";</span><span class="sxs-lookup"><span data-stu-id="9423a-178">Set hello protocol too"TCP";</span></span>
* <span data-ttu-id="9423a-179">Ustaw zakres portów docelowych hello zbyt "8080";</span><span class="sxs-lookup"><span data-stu-id="9423a-179">Set hello destination port range too"8080";</span></span>
* <span data-ttu-id="9423a-180">Kliknij przycisk OK i poczekaj, aż toobe reguły zabezpieczeń hello utworzony.</span><span class="sxs-lookup"><span data-stu-id="9423a-180">Click OK and wait for hello security rule toobe created.</span></span>

<span data-ttu-id="9423a-181">Po utworzeniu tej reguły zabezpieczeń, jest publicznie widoczna na powitania TODO aplikacji hello internet i możesz przeglądać tooit, takich jak na przykład przy użyciu adresu URL:</span><span class="sxs-lookup"><span data-stu-id="9423a-181">After creating this security rule, hello TODO application is publically visible on hello internet and you can browse tooit, for instance using a URL such as:</span></span>

    http://machinename.region.cloudapp.azure.com:8080

<span data-ttu-id="9423a-182">Można zauważyć, że mimo że firma Microsoft nie skonfigurował jeszcze maszyny wirtualnej bazy danych MongoDB hello, hello aplikacji TODO pojawia się toobe dość funkcjonalności.</span><span class="sxs-lookup"><span data-stu-id="9423a-182">You will notice that even though we have not yet configured hello MongoDB virtual machine, hello TODO application appears toobe quite functional.</span></span> <span data-ttu-id="9423a-183">Jest to spowodowane repozytorium źródłowe hello jest zapisane na stałe toouse wstępnie wdrożone wystąpienie bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="9423a-183">This is because hello source repository is hardcoded toouse a pre-deployed MongoDB instance.</span></span> <span data-ttu-id="9423a-184">Po skonfigurowaliśmy maszyny wirtualnej bazy danych MongoDB hello, firma Microsoft będzie Przejdź wstecz i zmień tooutilize kodu źródłowego hello, naszych prywatnej wystąpienie bazy danych MongoDB zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="9423a-184">Once we have configured hello MongoDB virtual machine, we will go back and change hello source code tooutilize our private MongoDB instance instead.</span></span>

### <a name="configuring-hello-mongodb-virtual-machine"></a><span data-ttu-id="9423a-185">Konfigurowanie hello maszyny wirtualnej bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="9423a-185">Configuring hello MongoDB Virtual Machine</span></span>
<span data-ttu-id="9423a-186">SSH toohello drugiej maszyny utworzonych przy użyciu programu PuTTY, ssh wiersza polecenia lub innych ulubionego narzędzia SSH.</span><span class="sxs-lookup"><span data-stu-id="9423a-186">SSH toohello second machine you created using PuTTY, ssh command line or your other favorite SSH tool.</span></span> <span data-ttu-id="9423a-187">Po przejrzeniu powitalna wiadomość hello i wiersz polecenia, należy zainstalować bazy danych MongoDB (instrukcje te zostały pobrane z [tutaj](https://docs.mongodb.org/master/tutorial/install-mongodb-on-ubuntu/)):</span><span class="sxs-lookup"><span data-stu-id="9423a-187">After seeing hello welcome message and command prompt, install MongoDB (these instructions were taken from [here](https://docs.mongodb.org/master/tutorial/install-mongodb-on-ubuntu/)):</span></span>

    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
    echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
    sudo apt-get update
    sudo apt-get install -y mongodb-org

<span data-ttu-id="9423a-188">Domyślnie bazy danych MongoDB jest skonfigurowany tak go można uzyskać tylko lokalnie.</span><span class="sxs-lookup"><span data-stu-id="9423a-188">By default, MongoDB is configured so it can only be accessed locally.</span></span> <span data-ttu-id="9423a-189">W tym samouczku firma Microsoft będzie Konfigurowanie bazy danych MongoDB są dostępne z aplikacji hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9423a-189">For this tutorial, we will configure MongoDB so it can be accessed from hello application's virtual machine.</span></span> <span data-ttu-id="9423a-190">W kontekście sudo, otwórz plik /etc/mongod.conf hello i Znajdź hello `# network interfaces` sekcji.</span><span class="sxs-lookup"><span data-stu-id="9423a-190">In a sudo context, open hello /etc/mongod.conf file and locate hello `# network interfaces` section.</span></span> <span data-ttu-id="9423a-191">Zmień hello `net.bindIp` konfiguracji wartość zbyt`0.0.0.0`.</span><span class="sxs-lookup"><span data-stu-id="9423a-191">Change hello `net.bindIp` configuration value too`0.0.0.0`.</span></span>

> [!NOTE]
> <span data-ttu-id="9423a-192">Ta konfiguracja służy do celów hello tylko tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="9423a-192">This configuration is for hello purposes of this tutorial only.</span></span> <span data-ttu-id="9423a-193">Jest **nie** zalecane rozwiązanie w zakresie zabezpieczeń i nie powinna być używana w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="9423a-193">It is **NOT** a recommended security practice and should not be used in production environments.</span></span>
> 
> 

<span data-ttu-id="9423a-194">Teraz upewnij się, hello bazy danych MongoDB usługa została uruchomiona:</span><span class="sxs-lookup"><span data-stu-id="9423a-194">Now ensure hello MongoDB service has been started:</span></span>

    sudo service mongod restart

<span data-ttu-id="9423a-195">Bazy danych MongoDB działa za pośrednictwem portu 27017 domyślnie.</span><span class="sxs-lookup"><span data-stu-id="9423a-195">MongoDB operates over port 27017 by default.</span></span> <span data-ttu-id="9423a-196">Dlatego w hello taki sam sposób, że firma potrzebuje tooopen portu 8080 na maszynie wirtualnej frontonu sieci web hello, potrzebujemy portu tooopen 27017 na maszynie wirtualnej hello bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="9423a-196">So, in hello same way that we needed tooopen port 8080 on hello web frontend virtual machine, we need tooopen port 27017 on hello MongoDB virtual machine.</span></span>

<span data-ttu-id="9423a-197">Zwraca toohello portalu Azure i ukończyć powitalnych następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="9423a-197">Return toohello Azure Portal and complete hello following steps:</span></span>

* <span data-ttu-id="9423a-198">Kliknij pozycję "Grupy zasobów" hello lewy pasek nawigacyjny;</span><span class="sxs-lookup"><span data-stu-id="9423a-198">Click on "Resource groups" in hello left navbar;</span></span>
* <span data-ttu-id="9423a-199">Wybierz grupę zasobów hello, który zawiera maszyny wirtualnej bazy danych MongoDB hello;</span><span class="sxs-lookup"><span data-stu-id="9423a-199">Select hello resource group that contains hello MongoDB virtual machine;</span></span>
* <span data-ttu-id="9423a-200">Hello wynikowej listy zasobów wybierz grupę zabezpieczeń sieci hello (hello jedną z ikona tarczy) z hello sama nazwa nadanym dla maszyny wirtualnej bazy danych MongoDB toohello;</span><span class="sxs-lookup"><span data-stu-id="9423a-200">In hello resulting list of resources, select hello network security group (hello one with a shield icon) with hello same name that you gave toohello MongoDB virtual machine;</span></span>
* <span data-ttu-id="9423a-201">W oknie dialogowym właściwości hello wybierz "zasady zabezpieczeń dla ruchu przychodzącego";</span><span class="sxs-lookup"><span data-stu-id="9423a-201">In hello properties, choose "Inbound security rules";</span></span>
* <span data-ttu-id="9423a-202">Witaj pasku narzędzi kliknij przycisk "Dodaj";</span><span class="sxs-lookup"><span data-stu-id="9423a-202">In hello toolbar, click "Add";</span></span>
* <span data-ttu-id="9423a-203">Podaj nazwę, takich jak "domyślny — Zezwalaj mongo";</span><span class="sxs-lookup"><span data-stu-id="9423a-203">Provide a name like "default-allow-mongo";</span></span>
* <span data-ttu-id="9423a-204">Ustawienie zbyt protokołu hello "TCP";</span><span class="sxs-lookup"><span data-stu-id="9423a-204">Set hello protocol too"TCP";</span></span>
* <span data-ttu-id="9423a-205">Ustaw zakres portów docelowych hello zbyt "27017";</span><span class="sxs-lookup"><span data-stu-id="9423a-205">Set hello destination port range too"27017";</span></span>
* <span data-ttu-id="9423a-206">Kliknij przycisk OK i poczekaj, aż toobe reguły zabezpieczeń hello utworzony.</span><span class="sxs-lookup"><span data-stu-id="9423a-206">Click OK and wait for hello security rule toobe created.</span></span>

## <a name="iterating-on-hello-todo-application"></a><span data-ttu-id="9423a-207">Iteracja na powitania aplikacji TODO</span><span class="sxs-lookup"><span data-stu-id="9423a-207">Iterating on hello TODO application</span></span>
<span data-ttu-id="9423a-208">Do tej pory uprzednim udostępnieniu dwóch maszyn wirtualnych systemu Linux:, który jest uruchomiony hello aplikacji frontonu sieci web, a drugi działa wystąpienie bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="9423a-208">So far, we have provisioned two Linux virtual machines: one that is running hello application's web frontend and one that is running a MongoDB instance.</span></span> <span data-ttu-id="9423a-209">Ale występuje problem — frontonu sieci web hello faktycznie nie używa wystąpienie bazy danych MongoDB hello elastycznie jeszcze.</span><span class="sxs-lookup"><span data-stu-id="9423a-209">But there is a problem - hello web frontend isn't actually using hello provisioned MongoDB instance yet.</span></span> <span data-ttu-id="9423a-210">Załóżmy rozwiązać ten problem, aktualizując toouse kod frontonu sieci web hello zmienną środowiskową zamiast wystąpieniem ustalony.</span><span class="sxs-lookup"><span data-stu-id="9423a-210">Let's fix that by updating hello web frontend code toouse an environment variable instead of a hard-coded instance.</span></span>

### <a name="changing-hello-todo-application"></a><span data-ttu-id="9423a-211">Zmiana hello aplikacji TODO</span><span class="sxs-lookup"><span data-stu-id="9423a-211">Changing hello TODO application</span></span>
<span data-ttu-id="9423a-212">Na komputerze deweloperskim, gdzie najpierw sklonować repozytorium todo węzła hello, otwórz hello `node-todo/config/database.js` plik w edytorze ulubionych i zmień wartość adresu url hello z hello ustalony wartości podobnie jak `mongodb://...` zbyt`process.env.MONGODB`.</span><span class="sxs-lookup"><span data-stu-id="9423a-212">On your development machine where you first cloned hello node-todo repository, open hello `node-todo/config/database.js` file in your favorite editor and change hello url value from hello hard-coded value like `mongodb://...` too`process.env.MONGODB`.</span></span>

<span data-ttu-id="9423a-213">Zatwierdź zmiany i Wypchnij toohello GitHub głównego:</span><span class="sxs-lookup"><span data-stu-id="9423a-213">Commit your changes and push toohello GitHub master:</span></span>

    git commit -am "Get MongoDB instance from env"
    git push origin master

<span data-ttu-id="9423a-214">Niestety to nie publikuje maszyny wirtualnej frontonu sieci web toohello hello zmiany.</span><span class="sxs-lookup"><span data-stu-id="9423a-214">Unfortunately, this doesn't publish hello change toohello web frontend virtual machine.</span></span> <span data-ttu-id="9423a-215">Można wprowadzić kilka więcej tooenable maszyny wirtualnej toothat zmiany prostą, ale efektywny mechanizm publikowania aktualizacji, można szybko obserwować wpływ hello hello zmian w środowisku produkcyjnym hello.</span><span class="sxs-lookup"><span data-stu-id="9423a-215">Let's make a few more changes toothat virtual machine tooenable a simple but effective mechanism for publishing updates so you can quickly observe hello effect of hello changes in hello live environment.</span></span>

### <a name="configuring-hello-web-frontend-virtual-machine"></a><span data-ttu-id="9423a-216">Konfigurowanie hello maszyny wirtualnej frontonu sieci Web</span><span class="sxs-lookup"><span data-stu-id="9423a-216">Configuring hello Web Frontend Virtual Machine</span></span>
<span data-ttu-id="9423a-217">Odwołaj możemy wcześniej utworzona bez systemu operacyjnego klonowania repozytorium todo węzła hello na maszynie wirtualnej frontonu sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="9423a-217">Recall that we previously created a bare clone of hello node-todo repository on hello web frontend virtual machine.</span></span> <span data-ttu-id="9423a-218">Okaże się utworzenia nowego Git, może zostać umieszczony zdalnego toowhich zmiany tej akcji.</span><span class="sxs-lookup"><span data-stu-id="9423a-218">It turns out that this action created a new Git remote toowhich changes can be pushed.</span></span> <span data-ttu-id="9423a-219">Jednak po prostu wypychanie zdalnego toothis dość nie zapewnia hello szybkie iteracji modelu, który szukasz deweloperzy podczas pracy na ich kodu.</span><span class="sxs-lookup"><span data-stu-id="9423a-219">However, simply pushing toothis remote doesn't quite give hello rapid iteration model that developers are looking for when working on their code.</span></span>

<span data-ttu-id="9423a-220">Co mamy ma toobe toodo możliwe jest upewnij się, że w przypadku wypychania toohello zdalnego repozytorium na maszynie wirtualnej hello działającej aplikacji TODO hello jest automatycznie aktualizowany.</span><span class="sxs-lookup"><span data-stu-id="9423a-220">What we would like toobe able toodo is ensure that when a push toohello remote repository on hello virtual machine occurs, hello running TODO application is automatically updated.</span></span> <span data-ttu-id="9423a-221">Na szczęście to łatwe tooachieve za pomocą narzędzia git.</span><span class="sxs-lookup"><span data-stu-id="9423a-221">Fortunately, this is easy tooachieve with git.</span></span>

<span data-ttu-id="9423a-222">Git eksponuje pewną liczbę punkty zaczepienia wywoływanych w podejmowaną w odniesieniu do repozytorium hello tooactions tooreact określonego czasu.</span><span class="sxs-lookup"><span data-stu-id="9423a-222">Git exposes a number of hooks that are called at particular times tooreact tooactions taken on hello repository.</span></span> <span data-ttu-id="9423a-223">Są one określone przy użyciu skryptów powłoki w repozytorium hello `hooks` folderu.</span><span class="sxs-lookup"><span data-stu-id="9423a-223">These are specified using shell scripts in hello repository's `hooks` folder.</span></span> <span data-ttu-id="9423a-224">hak Hello, który jest najbardziej odpowiednie dla scenariusza automatycznej aktualizacji hello jest hello `post-update` zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="9423a-224">hello hook that is most applicable for hello auto-update scenario is hello `post-update` event.</span></span>

<span data-ttu-id="9423a-225">W SSH sesji toohello sieci web frontonu maszynę wirtualną, zmień toohello `~/node-todo.git/hooks` katalogu i Dodaj powitania po tooa zawartości pliku o nazwie `post-update` (zastępowanie `machinename` i `region` z informacjami o MongoDB maszyny wirtualnej):</span><span class="sxs-lookup"><span data-stu-id="9423a-225">In a SSH session toohello web frontend virtual machine, change toohello `~/node-todo.git/hooks` directory and add hello following content tooa file named `post-update` (replacing `machinename` and `region` with your MongoDB virtual machine information):</span></span>

    #!/bin/bash

    forever stopall
    unset 'GIT_DIR'
    export MONGODB="mongodb://machinename.region.cloudapp.azure.com:27017/tododb"
    cd ~/node-todo && git fetch origin && git pull origin master && npm install && forever start ~/node-todo/server.js
    exec git update-server-info

<span data-ttu-id="9423a-226">Upewnij się, że ten plik wykonywalny, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="9423a-226">Ensure this file is executable by running hello following command:</span></span>

    chmod 755 post-update

<span data-ttu-id="9423a-227">Ten skrypt temu hello bieżącego serwera aplikacji jest zatrzymana, kod hello w hello sklonowanego repozytorium jest zaktualizowane toohello najnowsza wersja, wszelkie zaktualizowane zależności i ponownego uruchomienia serwera hello.</span><span class="sxs-lookup"><span data-stu-id="9423a-227">This script ensures that hello current server application is stopped, hello code in hello cloned repository is updated toohello latest, any updated dependencies are satisfied, and hello server is restarted.</span></span> <span data-ttu-id="9423a-228">Gwarantuje również, że środowisko to hello został skonfigurowany w ramach przygotowania do odbierania naszym pierwszym aplikacji aktualizacji tooget hello wystąpienie bazy danych MongoDB z zmiennej środowiskowej.</span><span class="sxs-lookup"><span data-stu-id="9423a-228">It also ensures that hello environment has been configured in preparation for receiving our first application update tooget hello MongoDB instance from an environment variable.</span></span>

### <a name="configuring-your-development-machine"></a><span data-ttu-id="9423a-229">Konfigurowanie na komputerze deweloperskim</span><span class="sxs-lookup"><span data-stu-id="9423a-229">Configuring your Development Machine</span></span>
<span data-ttu-id="9423a-230">Teraz Zaloguj się na komputerze deweloperskim podłączonymi maszyny wirtualnej frontonu sieci web toohello.</span><span class="sxs-lookup"><span data-stu-id="9423a-230">Now let's get your development machine hooked up toohello web frontend virtual machine.</span></span> <span data-ttu-id="9423a-231">Jest tak proste, jak dodawanie hello repozytorium bez systemu operacyjnego na maszynie wirtualnej hello jako zdalnej.</span><span class="sxs-lookup"><span data-stu-id="9423a-231">This is as simple as adding hello bare repository on hello virtual machine as a remote.</span></span> <span data-ttu-id="9423a-232">Uruchom następujące polecenie toodo hello to (zastępowanie *użytkownika* nazwą logowania użytkownika sieci web frontonu maszyny wirtualnej i *machinename* i *region* jako odpowiednie):</span><span class="sxs-lookup"><span data-stu-id="9423a-232">Run hello following command toodo this (replacing *user* with your web frontend virtual machine login name and *machinename* and *region* as appropriate):</span></span>

    git remote add azure user@machinename.region.cloudapp.azure.com:node-todo.git

<span data-ttu-id="9423a-233">To są wszystkie wymagane tooenable wypychanie lub w celu publikowania, maszyna wirtualna frontonu sieci web toohello zmiany.</span><span class="sxs-lookup"><span data-stu-id="9423a-233">This is all that is needed tooenable pushing, or in effect publishing, changes toohello web frontend virtual machine.</span></span>

### <a name="publishing-updates"></a><span data-ttu-id="9423a-234">Publikowanie aktualizacji</span><span class="sxs-lookup"><span data-stu-id="9423a-234">Publishing Updates</span></span>
<span data-ttu-id="9423a-235">Umożliwia publikowanie hello jednej zmiany się do tej pory tak, aby aplikacja hello będzie korzystać z własnej wystąpienie bazy danych MongoDB:</span><span class="sxs-lookup"><span data-stu-id="9423a-235">Let's publish hello one change that has been made so far so that hello application will use our own MongoDB instance:</span></span>

    git push azure master

<span data-ttu-id="9423a-236">Powinny pojawić się dane wyjściowe podobne toothis:</span><span class="sxs-lookup"><span data-stu-id="9423a-236">You should see output similar toothis:</span></span>

    Counting objects: 4, done.
    Delta compression using up too4 threads.
    Compressing objects: 100% (3/3), done.
    Writing objects: 100% (4/4), 406 bytes | 0 bytes/s, done.
    Total 4 (delta 1), reused 0 (delta 0)
    remote: info:    Forever stopped processes:
    remote: data:        uid  command         script    forever pid  id logfile                         uptime
    remote: data:    [0] 0Lyh /usr/bin/nodejs server.js 9064    9301    /home/username/.forever/0Lyh.log 0:0:3:17.487
    remote: From /home/username/node-todo
    remote:    5f31fd7..5bc7be5  master     -> origin/master
    remote: From /home/username/node-todo
    remote:  * branch            master     -> FETCH_HEAD
    remote: Updating 5f31fd7..5bc7be5
    remote: Fast-forward
    remote:  config/database.js | 2 +-
    remote:  1 file changed, 1 insertion(+), 1 deletion(-)
    remote: npm WARN package.json node-todo@0.0.0 No repository field.
    remote: npm WARN package.json node-todo@0.0.0 No license field.
    remote: warn:    --minUptime not set. Defaulting to: 1000ms
    remote: warn:    --spinSleepTime not set. Your script will exit if it does not stay up for at least 1000ms
    remote: info:    Forever processing file: /home/username/node-todo/server.js
    toousername@machinename.region.cloudapp.azure.com:node-todo.git
    5f31fd7..5bc7be5  master -> master

<span data-ttu-id="9423a-237">Po wykonaniu tego polecenia, spróbuj odświeżyć aplikacji hello w przeglądarce sieci web.</span><span class="sxs-lookup"><span data-stu-id="9423a-237">After this command completes, try refreshing hello application in a web browser.</span></span> <span data-ttu-id="9423a-238">Powinno być możliwe toosee, że lista czynności do wykonania hello przedstawionych w tym miejscu jest pusta i nie jest już wiązanej toohello udostępnionych wdrożono wystąpienie bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="9423a-238">You should be able toosee that hello TODO list presented here is empty and no longer tied toohello shared deployed MongoDB instance.</span></span>

<span data-ttu-id="9423a-239">Samouczek hello toocomplete, można wprowadzić zmiany, bardziej widoczne.</span><span class="sxs-lookup"><span data-stu-id="9423a-239">toocomplete hello tutorial, let's make another, more visible change.</span></span> <span data-ttu-id="9423a-240">Na komputerze deweloperskim Otwórz plik node-todo/public/index.html hello za pomocą ulubionego edytora.</span><span class="sxs-lookup"><span data-stu-id="9423a-240">On your development machine, open hello node-todo/public/index.html file using your favorite editor.</span></span> <span data-ttu-id="9423a-241">Znajdź hello jumbotron nagłówka i Zmień tytuł powitania od "Jestem aholic Todo" za "Jestem aholic Todo na platformie Azure!".</span><span class="sxs-lookup"><span data-stu-id="9423a-241">Locate hello jumbotron header and change  hello title from "I'm a Todo-aholic" too"I'm a Todo-aholic on Azure!".</span></span>

<span data-ttu-id="9423a-242">Teraz załóżmy zatwierdzenia:</span><span class="sxs-lookup"><span data-stu-id="9423a-242">Now let's commit:</span></span>

    git commit -am "Azurify hello title"

<span data-ttu-id="9423a-243">Ten czas, umożliwia publikowanie hello tooAzure zmiany przed wypchnięciem go repozytorium GitHub toohello tooback:</span><span class="sxs-lookup"><span data-stu-id="9423a-243">This time, let's publish hello change tooAzure before pushing it tooback toohello GitHub repo:</span></span>

    git push azure master

<span data-ttu-id="9423a-244">Po zakończeniu wykonywania tego polecenia strony sieci web hello odświeżania i zmiany będą widoczne hello.</span><span class="sxs-lookup"><span data-stu-id="9423a-244">Once this command completes, refresh hello web page and you will see hello changes.</span></span> <span data-ttu-id="9423a-245">Ponieważ one świetnie push pochodzenia wstecz toohello zmiany hello zdalnego:</span><span class="sxs-lookup"><span data-stu-id="9423a-245">Since they look good, push hello change back toohello origin remote:</span></span> 

    git push origin master

## <a name="next-steps"></a><span data-ttu-id="9423a-246">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9423a-246">Next Steps</span></span>
<span data-ttu-id="9423a-247">W tym artykule pokazano, jak tootake aplikacji Node.js i wdróż je tooLinux maszyn wirtualnych działających na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="9423a-247">This article showed how tootake a Node.js application and deploy it tooLinux virtual machines running in Azure.</span></span> <span data-ttu-id="9423a-248">toolearn więcej informacji na temat maszyn wirtualnych systemu Linux na platformie Azure, zobacz [tooLinux wprowadzenie na platformie Azure](/documentation/articles/virtual-machines-linux-introduction/).</span><span class="sxs-lookup"><span data-stu-id="9423a-248">toolearn more about Linux virtual machines in Azure, see [Introduction tooLinux on Azure](/documentation/articles/virtual-machines-linux-introduction/).</span></span>

<span data-ttu-id="9423a-249">Aby uzyskać więcej informacji o tym, jak toodevelop aplikacji Node.js na platformie Azure, zobacz hello [Centrum deweloperów środowiska Node.js](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="9423a-249">For more information about how toodevelop Node.js applications on Azure, see hello [Node.js Developer Center](/develop/nodejs/).</span></span>

