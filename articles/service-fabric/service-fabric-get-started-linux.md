---
title: "aaaSet się środowisko programowania w systemie Linux | Dokumentacja firmy Microsoft"
description: "Zainstaluj środowisko uruchomieniowe hello i zestawu SDK i Utwórz lokalny klaster projektowy w systemie Linux. Po ukończeniu tej konfiguracji będzie gotowy toobuild aplikacji."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: d552c8cd-67d1-45e8-91dc-871853f44fc6
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/23/2017
ms.author: subramar
ms.openlocfilehash: 9d82c2015f9e2c6fb55f2052c7cdb1e906c5deeb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-development-environment-on-linux"></a><span data-ttu-id="f9cb3-104">Przygotowywanie środowiska projektowego w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="f9cb3-104">Prepare your development environment on Linux</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f9cb3-105">Windows</span><span class="sxs-lookup"><span data-stu-id="f9cb3-105">Windows</span></span>](service-fabric-get-started.md)
> * [<span data-ttu-id="f9cb3-106">Linux</span><span class="sxs-lookup"><span data-stu-id="f9cb3-106">Linux</span></span>](service-fabric-get-started-linux.md)
> * [<span data-ttu-id="f9cb3-107">OSX</span><span class="sxs-lookup"><span data-stu-id="f9cb3-107">OSX</span></span>](service-fabric-get-started-mac.md)
>
>  

<span data-ttu-id="f9cb3-108">toodeploy i uruchom [aplikacji usługi Azure Service Fabric](service-fabric-application-model.md) na komputerze deweloperskim Linux należy zainstalować hello środowiska uruchomieniowego i typowych zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="f9cb3-108">toodeploy and run [Azure Service Fabric applications](service-fabric-application-model.md) on your Linux development machine, install hello runtime and common SDK.</span></span> <span data-ttu-id="f9cb3-109">Można także zainstalować opcjonalne zestawy SDK dla platformy Java i .NET Core.</span><span class="sxs-lookup"><span data-stu-id="f9cb3-109">You can also install optional SDKs for Java and .NET Core.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f9cb3-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f9cb3-110">Prerequisites</span></span>

<span data-ttu-id="f9cb3-111">następujące wersje systemu operacyjnego Hello są obsługiwane w przypadku rozwoju:</span><span class="sxs-lookup"><span data-stu-id="f9cb3-111">hello following operating system versions are supported for development:</span></span>

* <span data-ttu-id="f9cb3-112">Ubuntu 16.04 (`Xenial Xerus`)</span><span class="sxs-lookup"><span data-stu-id="f9cb3-112">Ubuntu 16.04 (`Xenial Xerus`)</span></span>

## <a name="update-your-apt-sources"></a><span data-ttu-id="f9cb3-113">Aktualizowanie źródeł APT</span><span class="sxs-lookup"><span data-stu-id="f9cb3-113">Update your APT sources</span></span>
<span data-ttu-id="f9cb3-114">tooinstall hello zestawu SDK i hello skojarzone środowisko uruchomieniowe pakietu za pomocą narzędzia wiersza polecenia get stanie hello, należy najpierw zaktualizować źródła zaawansowane narzędzia pakowania (APT, Distributed File System).</span><span class="sxs-lookup"><span data-stu-id="f9cb3-114">tooinstall hello SDK and hello associated runtime package via hello apt-get command-line tool, you must first update your Advanced Packaging Tool (APT) sources.</span></span>

1. <span data-ttu-id="f9cb3-115">Otwórz terminal.</span><span class="sxs-lookup"><span data-stu-id="f9cb3-115">Open a terminal.</span></span>
2. <span data-ttu-id="f9cb3-116">Dodawanie listy źródła tooyour hello sieci szkieletowej usług repozytorium.</span><span class="sxs-lookup"><span data-stu-id="f9cb3-116">Add hello Service Fabric repo tooyour sources list.</span></span>

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] http://apt-mo.trafficmanager.net/repos/servicefabric/ xenial main" > /etc/apt/sources.list.d/servicefabric.list'
    ```

3. <span data-ttu-id="f9cb3-117">Dodaj hello `dotnet` listy źródła tooyour repozytorium.</span><span class="sxs-lookup"><span data-stu-id="f9cb3-117">Add hello `dotnet` repo tooyour sources list.</span></span>

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list'
    ```

4. <span data-ttu-id="f9cb3-118">Dodaj hello zestaw kluczy stanie tooyour klucza Gnu nowe prywatności Guard (oprogramowania GnuPG lub GPG).</span><span class="sxs-lookup"><span data-stu-id="f9cb3-118">Add hello new Gnu Privacy Guard (GnuPG, or GPG) key tooyour APT keyring.</span></span>

    ```bash
    sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
    ```

5. <span data-ttu-id="f9cb3-119">Dodaj hello oficjalnego Docker GPG klucza tooyour stanie zestaw kluczy.</span><span class="sxs-lookup"><span data-stu-id="f9cb3-119">Add hello official Docker GPG key tooyour APT keyring.</span></span>

    ```bash
    sudo apt-get install curl
    sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    ```

6. <span data-ttu-id="f9cb3-120">Konfigurowanie hello Docker repozytorium.</span><span class="sxs-lookup"><span data-stu-id="f9cb3-120">Set up hello Docker repository.</span></span>

    ```bash
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    ```

7. <span data-ttu-id="f9cb3-121">Odśwież pakiet listy oparte na powitania nowo dodany repozytoriów.</span><span class="sxs-lookup"><span data-stu-id="f9cb3-121">Refresh your package lists based on hello newly added repositories.</span></span>

    ```bash
    sudo apt-get update
    ```

## <a name="install-and-set-up-hello-sdk-for-local-cluster-setup"></a><span data-ttu-id="f9cb3-122">Instalowanie i konfigurowanie hello SDK instalacji klastra lokalnego</span><span class="sxs-lookup"><span data-stu-id="f9cb3-122">Install and set up hello SDK for local cluster setup</span></span>

<span data-ttu-id="f9cb3-123">Po zaktualizowaniu źródła, możesz zainstalować hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="f9cb3-123">After you have updated your sources, you can install hello SDK.</span></span> <span data-ttu-id="f9cb3-124">Zainstaluj pakiet zestawu SDK usług sieci szkieletowej hello, potwierdzenie instalacji hello i zaakceptować umowę licencyjną toohello.</span><span class="sxs-lookup"><span data-stu-id="f9cb3-124">Install hello Service Fabric SDK package, confirm hello installation, and agree toohello license agreement.</span></span>

```bash
sudo apt-get install servicefabricsdkcommon
```

>   [!TIP]
>   <span data-ttu-id="f9cb3-125">Witaj następujące polecenia zautomatyzować akceptują licencji hello pakietów sieci szkieletowej usług:</span><span class="sxs-lookup"><span data-stu-id="f9cb3-125">hello following commands automate accepting hello license for Service Fabric packages:</span></span>
>   ```bash
>   echo "servicefabric servicefabric/accepted-eula-v1 select true" | sudo debconf-set-selections
>   echo "servicefabricsdkcommon servicefabricsdkcommon/accepted-eula-v1 select true" | sudo debconf-set-selections
>   ```

## <a name="set-up-a-local-cluster"></a><span data-ttu-id="f9cb3-126">Tworzenie klastra lokalnego</span><span class="sxs-lookup"><span data-stu-id="f9cb3-126">Set up a local cluster</span></span>
  <span data-ttu-id="f9cb3-127">Jeśli hello instalacja zakończy się pomyślnie, powinny być możliwe toostart klastra lokalnego.</span><span class="sxs-lookup"><span data-stu-id="f9cb3-127">If hello installation is successful, you should be able toostart a local cluster.</span></span>

  1. <span data-ttu-id="f9cb3-128">Uruchom skrypt instalacji klastra hello.</span><span class="sxs-lookup"><span data-stu-id="f9cb3-128">Run hello cluster setup script.</span></span>

      ```bash
      sudo /opt/microsoft/sdk/servicefabric/common/clustersetup/devclustersetup.sh
      ```

  2. <span data-ttu-id="f9cb3-129">Otwórz przeglądarkę sieci web i przejdź zbyt[Service Fabric Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="f9cb3-129">Open a web browser and go too[Service Fabric Explorer](http://localhost:19080/Explorer).</span></span> <span data-ttu-id="f9cb3-130">Jeśli hello klastra została uruchomiona, powinna zostać wyświetlona hello Service Fabric Explorer z pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="f9cb3-130">If hello cluster has started, you should see hello Service Fabric Explorer dashboard.</span></span>

      ![Narzędzie Service Fabric Explorer w systemie Linux][sfx-linux]

  <span data-ttu-id="f9cb3-132">W tym momencie możliwe jest wdrożenie wstępnie skompilowanych pakietów aplikacji usługi Service Fabric lub nowych pakietów opartych na kontenerach gościa bądź plikach wykonywalnych gościa.</span><span class="sxs-lookup"><span data-stu-id="f9cb3-132">At this point, you can deploy pre-built Service Fabric application packages or new ones based on guest containers or guest executables.</span></span> <span data-ttu-id="f9cb3-133">toobuild nowych usług za pomocą języka Java hello lub .NET Core SDK, wykonaj kroki opcjonalne ustawienia hello, które zostały opublikowane w kolejnych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="f9cb3-133">toobuild new services by using hello Java or .NET Core SDKs, follow hello optional setup steps that are provided in subsequent sections.</span></span>


  > [!NOTE]
  > <span data-ttu-id="f9cb3-134">Klastry autonomiczne nie są obsługiwane w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="f9cb3-134">Standalone clusters aren't supported in Linux.</span></span> <span data-ttu-id="f9cb3-135">Witaj w wersji zapoznawczej obsługuje tylko jednego pola i Azure Linux klastrach obejmujących wiele maszyn.</span><span class="sxs-lookup"><span data-stu-id="f9cb3-135">hello preview supports only one-box and Azure Linux multi-machine clusters.</span></span>
  >

## <a name="set-up-hello-service-fabric-cli"></a><span data-ttu-id="f9cb3-136">Konfigurowanie hello usługi sieci szkieletowej interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="f9cb3-136">Set up hello Service Fabric CLI</span></span>

<span data-ttu-id="f9cb3-137">Witaj [interfejsu wiersza polecenia usługi sieć szkieletowa](service-fabric-cli.md) zawiera polecenia do interakcji z jednostek usługi Service Fabric, łącznie z klastrów i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f9cb3-137">hello [Service Fabric CLI](service-fabric-cli.md) has commands for interacting with Service Fabric entities, including clusters and applications.</span></span> <span data-ttu-id="f9cb3-138">Jest on oparty na języku python, dlatego należy się toohave python i pip zainstalowane przed kontynuowaniem hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="f9cb3-138">It is based on python, so be sure toohave python and pip installed before you proceed with hello following command:</span></span>

```bash
pip install sfctl
```

## <a name="install-and-set-up-hello-generators-for-containers-and-guest-executables"></a><span data-ttu-id="f9cb3-139">Instalowanie i konfigurowanie generatory hello kontenery i plików wykonywalnych gościa</span><span class="sxs-lookup"><span data-stu-id="f9cb3-139">Install and set up hello generators for containers and guest-executables</span></span>
<span data-ttu-id="f9cb3-140">Usługa Service Fabric udostępnia narzędzia do tworzenia szkieletów, które ułatwiają tworzenie aplikacji usługi Service Fabric z poziomu terminalu przy użyciu generatora szablonów narzędzia Yeoman.</span><span class="sxs-lookup"><span data-stu-id="f9cb3-140">Service Fabric provides scaffolding tools which will help you create a Service Fabric applications from terminal using Yeoman template generator.</span></span> <span data-ttu-id="f9cb3-141">Wykonaj kroki hello poniżej tooensure masz generatora narzędzia yeoman szablonu usługi sieć szkieletowa hello do pracy na komputerze.</span><span class="sxs-lookup"><span data-stu-id="f9cb3-141">Please follow hello steps below tooensure you have hello Service Fabric yeoman template generator for working on your machine.</span></span>

1. <span data-ttu-id="f9cb3-142">Zainstaluj środowisko NodeJs i menedżera NPM na swojej maszynie</span><span class="sxs-lookup"><span data-stu-id="f9cb3-142">Install nodejs and NPM on your machine</span></span>

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. <span data-ttu-id="f9cb3-143">Zainstaluj generator szablonów [narzędzia Yeoman](http://yeoman.io/) na swoim komputerze z poziomu narzędzia NPM</span><span class="sxs-lookup"><span data-stu-id="f9cb3-143">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  sudo npm install -g yo
  ```
3. <span data-ttu-id="f9cb3-144">Zainstaluj generator kontenera usługi sieć szkieletowa Yeo hello i generator execuatble gościa z pakietu NPM</span><span class="sxs-lookup"><span data-stu-id="f9cb3-144">Install hello Service Fabric Yeo container generator and guest execuatble generator from NPM</span></span>

  ```bash
  sudo npm install -g generator-azuresfcontainer  # for Service Fabric container application
  sudo npm install -g generator-azuresfguest      # for Service Fabric guest executable application
  ```

<span data-ttu-id="f9cb3-145">Po zainstalowaniu hello powyżej generatory powinno być możliwe toocreate aplikacji za pomocą pliku wykonywalnego lub kontener usług gościa, uruchamiając `yo azuresfguest` lub `yo azuresfcontainer` odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="f9cb3-145">After you have installed hello above generators, you should be able toocreate apps with guest executable or container services by running `yo azuresfguest` or `yo azuresfcontainer` respectively.</span></span>

## <a name="install-hello-necessary-java-artifacts-optional-if-you-want-toouse-hello-java-programming-models"></a><span data-ttu-id="f9cb3-146">Zainstaluj hello niezbędne Java artefakty (opcjonalnie, jeśli chcesz toouse hello Java modele programowania)</span><span class="sxs-lookup"><span data-stu-id="f9cb3-146">Install hello necessary Java artifacts (optional, if you want toouse hello Java programming models)</span></span>

<span data-ttu-id="f9cb3-147">toobuild usługi sieć szkieletowa usług za pomocą języka Java, upewnij się, że 1.8 JDK instalowane wraz z narzędzia Gradle, który służy do uruchamiania zadań kompilacji.</span><span class="sxs-lookup"><span data-stu-id="f9cb3-147">toobuild Service Fabric services using Java, ensure you have JDK 1.8 installed along with Gradle which is used for running build tasks.</span></span> <span data-ttu-id="f9cb3-148">Witaj następującego fragmentu instaluje Otwórz 1.8 JDK wraz z narzędzia Gradle.</span><span class="sxs-lookup"><span data-stu-id="f9cb3-148">hello following snippet installs Open JDK 1.8 along with Gradle.</span></span> <span data-ttu-id="f9cb3-149">biblioteki usługi sieć szkieletowa Java Hello są pobierane z Maven.</span><span class="sxs-lookup"><span data-stu-id="f9cb3-149">hello Service Fabric Java libraries are pulled from Maven.</span></span>

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

## <a name="install-hello-eclipse-neon-plug-in-optional"></a><span data-ttu-id="f9cb3-150">Zainstaluj hello Neon Eclipse wtyczki (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="f9cb3-150">Install hello Eclipse Neon plug-in (optional)</span></span>

<span data-ttu-id="f9cb3-151">Można zainstalować hello Eclipse wtyczki dla sieci szkieletowej usług z wewnątrz hello **Eclipse IDE dla deweloperów języka Java**.</span><span class="sxs-lookup"><span data-stu-id="f9cb3-151">You can install hello Eclipse plug-in for Service Fabric from within hello **Eclipse IDE for Java Developers**.</span></span> <span data-ttu-id="f9cb3-152">W aplikacji Java sieci szkieletowej tooService dodanie służy aplikacji pliku wykonywalnego gościa Eclipse toocreate sieci szkieletowej usług i aplikacji kontenera.</span><span class="sxs-lookup"><span data-stu-id="f9cb3-152">You can use Eclipse toocreate Service Fabric guest executable applications and container applications in addition tooService Fabric Java applications.</span></span>

1. <span data-ttu-id="f9cb3-153">W środowisku Eclipse, upewnij się, czy masz najnowsze Neon Eclipse, a hello najnowszej wersji Buildship (1.0.17 lub nowszym) zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="f9cb3-153">In Eclipse, ensure that you have latest Eclipse Neon and hello latest Buildship version (1.0.17 or later) installed.</span></span> <span data-ttu-id="f9cb3-154">Można sprawdzić wersji hello zainstalowanych składników, wybierając **pomocy** > **szczegółowe informacje dotyczące instalacji**.</span><span class="sxs-lookup"><span data-stu-id="f9cb3-154">You can check hello versions of installed components by selecting **Help** > **Installation Details**.</span></span> <span data-ttu-id="f9cb3-155">Buildship można zaktualizować przy użyciu instrukcji hello na [Eclipse Buildship: Eclipse wtyczek dla narzędzia Gradle][buildship-update].</span><span class="sxs-lookup"><span data-stu-id="f9cb3-155">You can update Buildship by using hello instructions at [Eclipse Buildship: Eclipse Plug-ins for Gradle][buildship-update].</span></span>

2. <span data-ttu-id="f9cb3-156">tooinstall hello wtyczki, wybierz sieć szkieletowa usług **pomocy** > **zainstalować nowe oprogramowanie**.</span><span class="sxs-lookup"><span data-stu-id="f9cb3-156">tooinstall hello Service Fabric plug-in, select **Help** > **Install New Software**.</span></span>

3. <span data-ttu-id="f9cb3-157">W hello **pracować z** wpisz **http://dl.microsoft.com/eclipse**.</span><span class="sxs-lookup"><span data-stu-id="f9cb3-157">In hello **Work with** box, type **http://dl.microsoft.com/eclipse**.</span></span>

4. <span data-ttu-id="f9cb3-158">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="f9cb3-158">Click **Add**.</span></span>

    ![Witaj dostępnego oprogramowania strony][sf-eclipse-plugin]

5. <span data-ttu-id="f9cb3-160">Wybierz hello **ServiceFabric** wtyczki, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="f9cb3-160">Select hello **ServiceFabric** plug-in, and then click **Next**.</span></span>

6. <span data-ttu-id="f9cb3-161">Wykonaj kroki instalacji hello, a następnie zaakceptuj umowę licencyjną użytkownika oprogramowania hello.</span><span class="sxs-lookup"><span data-stu-id="f9cb3-161">Complete hello installation steps, and then accept hello end-user license agreement.</span></span>

<span data-ttu-id="f9cb3-162">Jeśli masz już hello usługi sieć szkieletowa Eclipse wtyczki zainstalowane, upewnij się, że masz hello najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="f9cb3-162">If you already have hello Service Fabric Eclipse plug-in installed, make sure that you have hello latest version.</span></span> <span data-ttu-id="f9cb3-163">Można sprawdzić, wybierając **pomocy** > **szczegółowe informacje dotyczące instalacji** , a następnie wyszukiwanie sieci szkieletowej usług hello lista zainstalowanych wtyczek. Wybierz opcję **Aktualizacja**, jeśli jest dostępna nowsza wersja.</span><span class="sxs-lookup"><span data-stu-id="f9cb3-163">You can check by selecting **Help** > **Installation Details** and then searching for Service Fabric in hello list of installed plug-ins. If a newer version is available, select **Update**.</span></span>

<span data-ttu-id="f9cb3-164">Aby uzyskać więcej informacji, zobacz artykuł [Wtyczka usługi Service Fabric na potrzeby tworzenia aplikacji Java w środowisku Eclipse](service-fabric-get-started-eclipse.md).</span><span class="sxs-lookup"><span data-stu-id="f9cb3-164">For more information, see [Service Fabric plug-in for Eclipse Java application development](service-fabric-get-started-eclipse.md).</span></span>


## <a name="install-hello-net-core-sdk-optional-if-you-want-toouse-hello-net-core-programming-models"></a><span data-ttu-id="f9cb3-165">Zainstaluj hello .NET Core SDK (opcjonalnie, jeśli chcesz, aby modele programowania .NET Core hello toouse)</span><span class="sxs-lookup"><span data-stu-id="f9cb3-165">Install hello .NET Core SDK (optional, if you want toouse hello .NET Core programming models)</span></span>
<span data-ttu-id="f9cb3-166">Hello .NET Core SDK udostępnia biblioteki hello i szablony, które są wymagane toobuild usługi sieć szkieletowa usług z platformą .NET Core.</span><span class="sxs-lookup"><span data-stu-id="f9cb3-166">hello .NET Core SDK provides hello libraries and templates that are required toobuild Service Fabric services with .NET Core.</span></span> <span data-ttu-id="f9cb3-167">Zainstaluj pakiet zestawu SDK programu .NET Core hello przez uruchomione hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="f9cb3-167">Install hello .NET Core SDK package by running hello following -</span></span>

   ```bash
   sudo apt-get install servicefabricsdkcsharp
   ```

## <a name="update-hello-sdk-and-runtime"></a><span data-ttu-id="f9cb3-168">Aktualizacja hello zestawu SDK i środowiska wykonawczego</span><span class="sxs-lookup"><span data-stu-id="f9cb3-168">Update hello SDK and runtime</span></span>

<span data-ttu-id="f9cb3-169">najnowszą wersję toohello tooupdate hello zestawu SDK i środowiska uruchomieniowego, uruchom następujące polecenia hello (odznacz hello zestawów SDK, które nie mają):</span><span class="sxs-lookup"><span data-stu-id="f9cb3-169">tooupdate toohello latest version of hello SDK and runtime, run hello following commands (deselect hello SDKs that you don't want):</span></span>

```bash
sudo apt-get update
sudo apt-get install servicefabric servicefabricsdkcommon servicefabricsdkcsharp
```
<span data-ttu-id="f9cb3-170">tooupdate hello plików binarnych zestawu Java SDK z Maven, należy tooupdate hello wersji szczegóły hello odpowiedniego pliku binarnego w hello ``build.gradle`` pliku toopoint toohello najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="f9cb3-170">tooupdate hello Java SDK binaries from Maven, you need tooupdate hello version details of hello corresponding binary in hello ``build.gradle`` file toopoint toohello latest version.</span></span> <span data-ttu-id="f9cb3-171">tooknow dokładnie konieczne tooupdate hello wersji, może się odwoływać tooany ``build.gradle`` plików w sieci szkieletowej usług — wprowadzenie przykłady [tutaj](https://github.com/Azure-Samples/service-fabric-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="f9cb3-171">tooknow exactly where you need tooupdate hello version, you can refer tooany ``build.gradle`` file in Service Fabric getting-started samples [here](https://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>

> [!NOTE]
> <span data-ttu-id="f9cb3-172">Aktualizowanie pakietów hello może spowodować Twojej toostop klastra rozwoju lokalnego uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="f9cb3-172">Updating hello packages might cause your local development cluster toostop running.</span></span> <span data-ttu-id="f9cb3-173">Uruchom ponownie klaster lokalny po uaktualnieniu instrukcjami hello na tej stronie.</span><span class="sxs-lookup"><span data-stu-id="f9cb3-173">Restart your local cluster after an upgrade by following hello instructions on this page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f9cb3-174">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f9cb3-174">Next steps</span></span>

* <span data-ttu-id="f9cb3-175">[Create and deploy your first Service Fabric Java application on Linux using Yeoman](service-fabric-create-your-first-linux-application-with-java.md) (Tworzenie i wdrażanie pierwszej aplikacji Java usługi Service Fabric w systemie Linux przy użyciu programu Yeoman)</span><span class="sxs-lookup"><span data-stu-id="f9cb3-175">[Create and deploy your first Service Fabric Java application on Linux by using Yeoman](service-fabric-create-your-first-linux-application-with-java.md)</span></span>
* <span data-ttu-id="f9cb3-176">[Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse](service-fabric-get-started-eclipse.md) (Tworzenie i wdrażanie pierwszej aplikacji Java usługi Service Fabric w systemie Linux przy użyciu wtyczki usługi Service Fabric dla środowiska Eclipse)</span><span class="sxs-lookup"><span data-stu-id="f9cb3-176">[Create and deploy your first Service Fabric Java application on Linux by using Service Fabric Plugin for Eclipse](service-fabric-get-started-eclipse.md)</span></span>
* <span data-ttu-id="f9cb3-177">[Create your first CSharp application on Linux](service-fabric-create-your-first-linux-application-with-csharp.md) (Tworzenie pierwszej aplikacji CSharp w systemie Linux)</span><span class="sxs-lookup"><span data-stu-id="f9cb3-177">[Create your first CSharp application on Linux](service-fabric-create-your-first-linux-application-with-csharp.md)</span></span>
* [<span data-ttu-id="f9cb3-178">Przygotowywanie środowiska projektowego w systemie OSX</span><span class="sxs-lookup"><span data-stu-id="f9cb3-178">Prepare your development environment on OSX</span></span>](service-fabric-get-started-mac.md)
* [<span data-ttu-id="f9cb3-179">Użyj aplikacji hello toomanage usługi sieci szkieletowej interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="f9cb3-179">Use hello Service Fabric CLI toomanage your applications</span></span>](service-fabric-application-lifecycle-sfctl.md)
* [<span data-ttu-id="f9cb3-180">Różnice w usłudze Service Fabric w systemie Windows i Linux</span><span class="sxs-lookup"><span data-stu-id="f9cb3-180">Service Fabric Windows/Linux differences</span></span>](service-fabric-linux-windows-differences.md)
* <span data-ttu-id="f9cb3-181">[Get started with Service Fabric CLI](service-fabric-cli.md) (Wprowadzenie do interfejsu wiersza polecenia usługi Service Fabric)</span><span class="sxs-lookup"><span data-stu-id="f9cb3-181">[Get started with Service Fabric CLI](service-fabric-cli.md)</span></span>

<!-- Links -->

[azure-xplat-cli-github]: https://github.com/Azure/azure-xplat-cli
[install-node]: https://nodejs.org/en/download/package-manager/#installing-node-js-via-package-manager
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship

<!--Images -->

[sf-eclipse-plugin]: ./media/service-fabric-get-started-linux/service-fabric-eclipse-plugin.png
[sfx-linux]: ./media/service-fabric-get-started-linux/sfx-linux.png
