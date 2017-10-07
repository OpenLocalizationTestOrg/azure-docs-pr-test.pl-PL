---
title: "aaaSet się środowiska deweloperskiego w toowork systemu Mac OS X z sieci szkieletowej usług Azure | Dokumentacja firmy Microsoft"
description: "Zainstaluj hello środowiska uruchomieniowego, zestawu SDK i narzędzia i Utwórz lokalny klaster projektowy. Po ukończeniu tej konfiguracji będzie gotowy toobuild aplikacji w systemie Mac OS X."
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: bf84458f-4b87-4de1-9844-19909e368deb
ms.service: service-fabric
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/21/2017
ms.author: saysa
ms.openlocfilehash: 0b8a6c1fc1871fa76f3e21cefbc7f66f79072797
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-your-development-environment-on-mac-os-x"></a><span data-ttu-id="b0843-104">Konfigurowanie środowiska projektowego w systemie Mac OS X</span><span class="sxs-lookup"><span data-stu-id="b0843-104">Set up your development environment on Mac OS X</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b0843-105">Windows</span><span class="sxs-lookup"><span data-stu-id="b0843-105">Windows</span></span>](service-fabric-get-started.md)
> * [<span data-ttu-id="b0843-106">Linux</span><span class="sxs-lookup"><span data-stu-id="b0843-106">Linux</span></span>](service-fabric-get-started-linux.md)
> * [<span data-ttu-id="b0843-107">OSX</span><span class="sxs-lookup"><span data-stu-id="b0843-107">OSX</span></span>](service-fabric-get-started-mac.md)
>
>  

<span data-ttu-id="b0843-108">Toorun aplikacji sieci szkieletowej usług mogą być oparte na klastry z systemem Linux przy użyciu systemu Mac OS X. W tym artykule opisano sposób tooset się komputerów Mac na potrzeby programowania.</span><span class="sxs-lookup"><span data-stu-id="b0843-108">You can build Service Fabric applications toorun on Linux clusters using Mac OS X. This article covers how tooset up your Mac for development.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b0843-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b0843-109">Prerequisites</span></span>
<span data-ttu-id="b0843-110">Sieć szkieletowa usług nie Uruchom natywnie na toorun systemu OS X. lokalnego klastra usługi sieć szkieletowa usług, firma Microsoft udostępnia wstępnie skonfigurowane maszyny wirtualnej systemu Ubuntu przy użyciu Vagrant i VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="b0843-110">Service Fabric does not run natively on OS X. toorun a local Service Fabric cluster, we provide a pre-configured Ubuntu virtual machine using Vagrant and VirtualBox.</span></span> <span data-ttu-id="b0843-111">Przed rozpoczęciem potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="b0843-111">Before you get started, you need:</span></span>

* [<span data-ttu-id="b0843-112">Vagrant (wersja 1.8.4 lub nowsza)</span><span class="sxs-lookup"><span data-stu-id="b0843-112">Vagrant (v1.8.4 or later)</span></span>](http://www.vagrantup.com/downloads.html)
* [<span data-ttu-id="b0843-113">VirtualBox</span><span class="sxs-lookup"><span data-stu-id="b0843-113">VirtualBox</span></span>](http://www.virtualbox.org/wiki/Downloads)

>[!NOTE]
> <span data-ttu-id="b0843-114">Należy toouse wzajemnie obsługiwane wersje Vagrant i VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="b0843-114">You need toouse mutually supported versions of Vagrant and VirtualBox.</span></span> <span data-ttu-id="b0843-115">Program Vagrant może zachowywać się niestabilnie w przypadku nieobsługiwanej wersji programu VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="b0843-115">Vagrant might behave erratically on an unsupported VirtualBox version.</span></span>
>

## <a name="create-hello-local-vm"></a><span data-ttu-id="b0843-116">Utwórz hello lokalnej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="b0843-116">Create hello local VM</span></span>
<span data-ttu-id="b0843-117">toocreate hello lokalnej maszyny Wirtualnej zawierający 5 węzłów klastra usługi sieć szkieletowa, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="b0843-117">toocreate hello local VM containing a 5-node Service Fabric cluster, perform hello following steps:</span></span>

1. <span data-ttu-id="b0843-118">Witaj w klonowania `Vagrantfile` repozytorium</span><span class="sxs-lookup"><span data-stu-id="b0843-118">Clone hello `Vagrantfile` repo</span></span>

    ```bash
    git clone https://github.com/azure/service-fabric-linux-vagrant-onebox.git
    ```
    <span data-ttu-id="b0843-119">Ta procedura Przełącz szczegółu hello pliku `Vagrantfile` zawierający hello maszyny Wirtualnej konfiguracji wraz z hello hello lokalizacji maszyny Wirtualnej jest pobierana z.</span><span class="sxs-lookup"><span data-stu-id="b0843-119">This steps bring downs hello file `Vagrantfile` containing hello VM configuration along with hello location hello VM is downloaded from.</span></span>

2. <span data-ttu-id="b0843-120">Przejdź toohello klonu lokalne powitania repozytorium</span><span class="sxs-lookup"><span data-stu-id="b0843-120">Navigate toohello local clone of hello repo</span></span>

    ```bash
    cd service-fabric-linux-vagrant-onebox
    ```
3. <span data-ttu-id="b0843-121">(Opcjonalnie) Zmodyfikuj ustawienia maszyny Wirtualnej domyślne hello</span><span class="sxs-lookup"><span data-stu-id="b0843-121">(Optional) Modify hello default VM settings</span></span>

    <span data-ttu-id="b0843-122">Domyślnie program hello lokalnej maszyny Wirtualnej jest konfigurowana w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="b0843-122">By default, hello local VM is configured as follows:</span></span>

   * <span data-ttu-id="b0843-123">3 GB przydzielonej pamięci</span><span class="sxs-lookup"><span data-stu-id="b0843-123">3 GB of memory allocated</span></span>
   * <span data-ttu-id="b0843-124">Sieci prywatnych hosta skonfigurowane pod adresem IP 192.168.50.50 umożliwiające przekazywanie ruchu z hello Mac hosta</span><span class="sxs-lookup"><span data-stu-id="b0843-124">Private host network configured at IP 192.168.50.50 enabling passthrough of traffic from hello Mac host</span></span>

     <span data-ttu-id="b0843-125">Można zmienić w dowolnym z tych ustawień lub dodać inne toohello konfiguracji maszyny Wirtualnej w hello `Vagrantfile`.</span><span class="sxs-lookup"><span data-stu-id="b0843-125">You can change either of these settings or add other configuration toohello VM in hello `Vagrantfile`.</span></span> <span data-ttu-id="b0843-126">Zobacz hello [dokumentacji Vagrant](http://www.vagrantup.com/docs) hello pełną listę opcji konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="b0843-126">See hello [Vagrant documentation](http://www.vagrantup.com/docs) for hello full list of configuration options.</span></span>
4. <span data-ttu-id="b0843-127">Utwórz hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="b0843-127">Create hello VM</span></span>

    ```bash
    vagrant up
    ```

   <span data-ttu-id="b0843-128">Ten krok pobiera hello wstępnie obrazu maszyny Wirtualnej, rozruchowy, który go lokalnie, a następnie skonfiguruj lokalny usługi Service Fabric klastra w nim.</span><span class="sxs-lookup"><span data-stu-id="b0843-128">This step downloads hello preconfigured VM image, boot it locally, and then set up a local Service Fabric cluster in it.</span></span> <span data-ttu-id="b0843-129">Należy oczekiwać go tootake za kilka minut.</span><span class="sxs-lookup"><span data-stu-id="b0843-129">You should expect it tootake a few minutes.</span></span> <span data-ttu-id="b0843-130">Jeśli Instalator zakończy się pomyślnie, zostanie wyświetlony komunikat w danych wyjściowych hello wskazujący, że w tym klastrze hello jest uruchamiany.</span><span class="sxs-lookup"><span data-stu-id="b0843-130">If setup completes successfully, you see a message in hello output indicating that hello cluster is starting up.</span></span>

    ![Uruchomienie konfiguracji klastra po aprowizacji maszyny wirtualnej][cluster-setup-script]

    >[!TIP]
    > <span data-ttu-id="b0843-132">Hello pobierania maszyny Wirtualnej jest zbyt długo, można pobrać przy użyciu wget lub curl lub za pośrednictwem przeglądarki, przechodząc określony przez łącze toohello **config.vm.box_url** w pliku hello `Vagrantfile`.</span><span class="sxs-lookup"><span data-stu-id="b0843-132">If hello VM download is taking a long time, you can download it using wget or curl or through a browser by navigating toohello link specified by **config.vm.box_url** in hello file `Vagrantfile`.</span></span> <span data-ttu-id="b0843-133">Po pobraniu lokalnie, należy edytować `Vagrantfile` ścieżka lokalna toohello toopoint którego pobrano hello obrazu.</span><span class="sxs-lookup"><span data-stu-id="b0843-133">After downloading it locally, edit `Vagrantfile` toopoint toohello local path where you downloaded hello image.</span></span> <span data-ttu-id="b0843-134">Na przykład jeśli pobrano too/home/users/test/azureservicefabric.tp8.box obraz powitania, następnie ustaw **config.vm.box_url** toothat ścieżki.</span><span class="sxs-lookup"><span data-stu-id="b0843-134">For example if you downloaded hello image too/home/users/test/azureservicefabric.tp8.box, then set **config.vm.box_url** toothat path.</span></span>
    >

5. <span data-ttu-id="b0843-135">Testowanie hello tego klastra nie został skonfigurowany poprawnie przechodząc tooService Eksploratora sieci szkieletowej w http://192.168.50.50:19080/Explorer (przy założeniu, przechowywane hello domyślne prywatnej sieci IP).</span><span class="sxs-lookup"><span data-stu-id="b0843-135">Test that hello cluster has been set up correctly by navigating tooService Fabric Explorer at http://192.168.50.50:19080/Explorer (assuming you kept hello default private network IP).</span></span>

    ![Service Fabric Explorer z hosta hello Mac][sfx-mac]


## <a name="create-application-on-mac-using-yeoman"></a><span data-ttu-id="b0843-137">Tworzenie aplikacji na komputerze Mac przy użyciu narzędzia Yeoman</span><span class="sxs-lookup"><span data-stu-id="b0843-137">Create application on Mac using Yeoman</span></span>
<span data-ttu-id="b0843-138">Usługa Service Fabric udostępnia narzędzia do tworzenia szkieletów, które ułatwiają tworzenie aplikacji usługi Service Fabric z poziomu terminalu przy użyciu generatora szablonów narzędzia Yeoman.</span><span class="sxs-lookup"><span data-stu-id="b0843-138">Service Fabric provides scaffolding tools which will help you create a Service Fabric application from terminal using Yeoman template generator.</span></span> <span data-ttu-id="b0843-139">Wykonaj kroki hello poniżej tooensure masz generator narzędzia yeoman szablonu usługi sieć szkieletowa hello działa na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="b0843-139">Please follow hello steps below tooensure you have hello Service Fabric yeoman template generator working on your machine.</span></span>

1. <span data-ttu-id="b0843-140">Należy toohave Node.js i NPM zainstalowane dla komputerów mac należy.</span><span class="sxs-lookup"><span data-stu-id="b0843-140">You need toohave Node.js and NPM installed on you mac.</span></span> <span data-ttu-id="b0843-141">Jeśli nie można zainstalować środowiska Node.js i przy użyciu oprogramowania Homebrew przy użyciu następujących hello NPM.</span><span class="sxs-lookup"><span data-stu-id="b0843-141">If not you can install Node.js and NPM using Homebrew using hello following.</span></span> <span data-ttu-id="b0843-142">toocheck hello wersji środowiska Node.js i NPM zainstalowany na komputerze Mac, można użyć hello ``-v`` opcji.</span><span class="sxs-lookup"><span data-stu-id="b0843-142">toocheck hello versions of Node.js and NPM installed on your Mac, you can use hello ``-v`` option.</span></span>

  ```bash
  brew install node
  node -v
  npm -v
  ```
2. <span data-ttu-id="b0843-143">Zainstaluj generator szablonów [narzędzia Yeoman](http://yeoman.io/) na swoim komputerze z poziomu narzędzia NPM</span><span class="sxs-lookup"><span data-stu-id="b0843-143">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  npm install -g yo
  ```
3. <span data-ttu-id="b0843-144">Zainstaluj narzędzia Yeoman hello generatora ma toouse, wykonaj czynności hello w hello wprowadzenie [dokumentacji](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="b0843-144">Install hello Yeoman generator you want toouse, following hello steps in hello getting started [documentation](service-fabric-get-started-linux.md).</span></span> <span data-ttu-id="b0843-145">Aplikacje sieci szkieletowej usług toocreate przy użyciu narzędzia Yeoman, wykonaj kroki hello-</span><span class="sxs-lookup"><span data-stu-id="b0843-145">toocreate Service Fabric Applications using Yeoman, follow hello steps -</span></span>

  ```bash
  npm install -g generator-azuresfjava       # for Service Fabric Java Applications
  npm install -g generator-azuresfguest      # for Service Fabric Guest executables
  npm install -g generator-azuresfcontainer  # for Service Fabric Container Applications
  ```
4. <span data-ttu-id="b0843-146">toobuild aplikacji Java sieci szkieletowej usług dla komputerów Mac, będzie potrzebny - JDK 1.8 i zainstalowane na komputerze hello narzędzia Gradle.</span><span class="sxs-lookup"><span data-stu-id="b0843-146">toobuild a Service Fabric Java application on Mac, you would need - JDK 1.8 and Gradle installed on hello machine.</span></span>


## <a name="install-hello-service-fabric-plugin-for-eclipse-neon"></a><span data-ttu-id="b0843-147">Instalowanie wtyczki usługi sieć szkieletowa powitania dla programu Eclipse Neon</span><span class="sxs-lookup"><span data-stu-id="b0843-147">Install hello Service Fabric plugin for Eclipse Neon</span></span>

<span data-ttu-id="b0843-148">Usługi Service Fabric zawiera dodatek hello **Neon Eclipse dla IDE języka Java** który uprościć proces hello tworzenie, kompilowanie i wdrażanie usług Java.</span><span class="sxs-lookup"><span data-stu-id="b0843-148">Service Fabric provides a plugin for hello **Eclipse Neon for Java IDE** that can simplify hello process of creating, building, and deploying Java services.</span></span> <span data-ttu-id="b0843-149">Możesz wykonać kroki instalacji hello wymienione w tym ogólne [dokumentacji](service-fabric-get-started-eclipse.md#install-or-update-the-service-fabric-plug-in-in-eclipse-neon) dotyczących instalowania lub aktualizowania wtyczkę Eclipse sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="b0843-149">You can follow hello installation steps mentioned in this general [documentation](service-fabric-get-started-eclipse.md#install-or-update-the-service-fabric-plug-in-in-eclipse-neon) about installing or updating Service Fabric Eclipse plugin.</span></span>

>[!TIP]
> <span data-ttu-id="b0843-150">Domyślnie obsługujemy hello domyślne IP jak wspomniano w hello ``Vagrantfile`` w hello ``Local.json`` aplikacji hello wygenerowany.</span><span class="sxs-lookup"><span data-stu-id="b0843-150">By default we support hello default IP as mentioned in hello ``Vagrantfile`` in hello ``Local.json`` of hello generated application.</span></span> <span data-ttu-id="b0843-151">W przypadku zmiany, które i wdrożyć Vagrant z innego adresu IP, zaktualizuj hello odpowiedniego adresu IP w ``Local.json`` również aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b0843-151">In case you change that and deploy Vagrant with a different IP, please update hello corresponding IP in ``Local.json`` of your application as well.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b0843-152">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b0843-152">Next steps</span></span>
<!-- Links -->
* <span data-ttu-id="b0843-153">[Create and deploy your first Service Fabric Java application on Linux using Yeoman](service-fabric-create-your-first-linux-application-with-java.md) (Tworzenie i wdrażanie pierwszej aplikacji Java usługi Service Fabric w systemie Linux przy użyciu programu Yeoman)</span><span class="sxs-lookup"><span data-stu-id="b0843-153">[Create and deploy your first Service Fabric Java application on Linux using Yeoman](service-fabric-create-your-first-linux-application-with-java.md)</span></span>
* <span data-ttu-id="b0843-154">[Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse](service-fabric-get-started-eclipse.md) (Tworzenie i wdrażanie pierwszej aplikacji Java usługi Service Fabric w systemie Linux przy użyciu wtyczki usługi Service Fabric dla środowiska Eclipse)</span><span class="sxs-lookup"><span data-stu-id="b0843-154">[Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse](service-fabric-get-started-eclipse.md)</span></span>
* [<span data-ttu-id="b0843-155">Tworzenie klastra sieci szkieletowej usług w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="b0843-155">Create a Service Fabric cluster in hello Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
* [<span data-ttu-id="b0843-156">Tworzenie klastra sieci szkieletowej usług za pomocą hello Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b0843-156">Create a Service Fabric cluster using hello Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
* [<span data-ttu-id="b0843-157">Zrozumienie modelu aplikacji hello sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="b0843-157">Understand hello Service Fabric application model</span></span>](service-fabric-application-model.md)

<!-- Images -->
[cluster-setup-script]: ./media/service-fabric-get-started-mac/cluster-setup-mac.png
[sfx-mac]: ./media/service-fabric-get-started-mac/sfx-mac.png
[sf-eclipse-plugin-install]: ./media/service-fabric-get-started-mac/sf-eclipse-plugin-install.png
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship
