---
title: "aaaService sieci szkieletowej i wdrażanie kontenerów w systemie Linux | Dokumentacja firmy Microsoft"
description: "Sieć szkieletowa usług i hello używają Linux kontenery toodeploy mikrousługi aplikacji. W tym artykule opisano możliwości hello, które udostępnia sieci szkieletowej usług dla kontenerów i jak toodeploy kontenera Linux obrazu w klastrze"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 4ba99103-6064-429d-ba17-82861b6ddb11
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/29/2017
ms.author: msfussell
ms.openlocfilehash: e28f99a145b0594d871b0ec0566233a7ad235ce8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-linux-container-tooservice-fabric"></a><span data-ttu-id="8c90e-104">Wdrażanie systemu Linux tooService kontenera sieci szkieletowej</span><span class="sxs-lookup"><span data-stu-id="8c90e-104">Deploy a Linux container tooService Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8c90e-105">Wdrażanie kontenera systemu Windows</span><span class="sxs-lookup"><span data-stu-id="8c90e-105">Deploy Windows Container</span></span>](service-fabric-deploy-container.md)
> * [<span data-ttu-id="8c90e-106">Wdrażanie kontenera systemu Linux</span><span class="sxs-lookup"><span data-stu-id="8c90e-106">Deploy Linux Container</span></span>](service-fabric-deploy-container-linux.md)
>
>

<span data-ttu-id="8c90e-107">W tym artykule przedstawiono tworzenie konteneryzowanych usług w kontenerach Docker w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="8c90e-107">This article walks you through building containerized services in Docker containers on Linux.</span></span>

<span data-ttu-id="8c90e-108">Sieć szkieletowa usług ma kilka możliwości kontenera, które zapewniają pomoc podczas tworzenia aplikacji, które składają się z mikrousług, które są konteneryzowanych.</span><span class="sxs-lookup"><span data-stu-id="8c90e-108">Service Fabric has several container capabilities that help you with building applications that are composed of microservices that are containerized.</span></span> <span data-ttu-id="8c90e-109">Te usługi są nazywane konteneryzowanych usług.</span><span class="sxs-lookup"><span data-stu-id="8c90e-109">These services are called containerized services.</span></span>

<span data-ttu-id="8c90e-110">możliwości Hello obejmują;</span><span class="sxs-lookup"><span data-stu-id="8c90e-110">hello capabilities include;</span></span>

* <span data-ttu-id="8c90e-111">Kontener obrazu wdrożenia i aktywacji</span><span class="sxs-lookup"><span data-stu-id="8c90e-111">Container image deployment and activation</span></span>
* <span data-ttu-id="8c90e-112">Zarządzanie zasobów</span><span class="sxs-lookup"><span data-stu-id="8c90e-112">Resource governance</span></span>
* <span data-ttu-id="8c90e-113">Repozytorium uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="8c90e-113">Repository authentication</span></span>
* <span data-ttu-id="8c90e-114">Mapowanie portów toohost port kontenera</span><span class="sxs-lookup"><span data-stu-id="8c90e-114">Container port toohost port mapping</span></span>
* <span data-ttu-id="8c90e-115">Odnajdywanie kontenera do kontenera i komunikacji</span><span class="sxs-lookup"><span data-stu-id="8c90e-115">Container-to-container discovery and communication</span></span>
* <span data-ttu-id="8c90e-116">Możliwość tooconfigure i ustaw zmienne środowiskowe</span><span class="sxs-lookup"><span data-stu-id="8c90e-116">Ability tooconfigure and set environment variables</span></span>

## <a name="packaging-a-docker-container-with-yeoman"></a><span data-ttu-id="8c90e-117">Pakowanie kontenera docker z narzędzia yeoman</span><span class="sxs-lookup"><span data-stu-id="8c90e-117">Packaging a docker container with yeoman</span></span>
<span data-ttu-id="8c90e-118">Podczas pakowania kontenera w systemie Linux, można wybrać obu toouse szablonu narzędzia yeoman lub [ręcznie utworzyć pakiet aplikacji hello](#manually).</span><span class="sxs-lookup"><span data-stu-id="8c90e-118">When packaging a container on Linux, you can choose either toouse a yeoman template or [create hello application package manually](#manually).</span></span>

<span data-ttu-id="8c90e-119">Aplikacji usługi Service Fabric może zawierać jeden lub więcej kontenerów, każda z określoną rolę w dostarczaniu funkcjonalności aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="8c90e-119">A Service Fabric application can contain one or more containers, each with a specific role in delivering hello application's functionality.</span></span> <span data-ttu-id="8c90e-120">Witaj zestawu SDK sieci szkieletowej usług dla systemu Linux zawiera [narzędzia Yeoman](http://yeoman.io/) generator kodu, który umożliwia łatwe toocreate aplikacji i Dodaj obraz kontenera.</span><span class="sxs-lookup"><span data-stu-id="8c90e-120">hello Service Fabric SDK for Linux includes a [Yeoman](http://yeoman.io/) generator that makes it easy toocreate your application and add a container image.</span></span> <span data-ttu-id="8c90e-121">Można użyć narzędzia Yeoman toocreate o nazwie aplikacji o jeden kontener Docker *SimpleContainerApp*.</span><span class="sxs-lookup"><span data-stu-id="8c90e-121">Let's use Yeoman toocreate an application with a single Docker container called *SimpleContainerApp*.</span></span> <span data-ttu-id="8c90e-122">Więcej usług można dodać później, edytując hello wygenerować pliki manifestu.</span><span class="sxs-lookup"><span data-stu-id="8c90e-122">You can add more services later by editing hello generated manifest files.</span></span>

## <a name="install-docker-on-your-development-box"></a><span data-ttu-id="8c90e-123">Zainstaluj Docker na Twoje okno programowanie</span><span class="sxs-lookup"><span data-stu-id="8c90e-123">Install Docker on your development box</span></span>

<span data-ttu-id="8c90e-124">Witaj uruchom następujące polecenia docker tooinstall Twojego pole rozwoju systemu Linux (Jeśli używasz vagrant obraz powitania w systemie OSX, docker jest już zainstalowana):</span><span class="sxs-lookup"><span data-stu-id="8c90e-124">Run hello following commands tooinstall docker on your Linux development box (if you are using hello vagrant image on OSX, docker is already installed):</span></span>

```bash
    sudo apt-get install wget
    wget -qO- https://get.docker.io/ | sh
```

## <a name="create-hello-application"></a><span data-ttu-id="8c90e-125">Tworzenie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="8c90e-125">Create hello application</span></span>
1. <span data-ttu-id="8c90e-126">Na terminalu wpisz `yo azuresfcontainer`.</span><span class="sxs-lookup"><span data-stu-id="8c90e-126">In a terminal, type `yo azuresfcontainer`.</span></span>
2. <span data-ttu-id="8c90e-127">Nazwa aplikacji — na przykład mycontainerap</span><span class="sxs-lookup"><span data-stu-id="8c90e-127">Name your application - for example, mycontainerap</span></span>
3. <span data-ttu-id="8c90e-128">Podaj adres URL hello hello kontener obrazu z repozytorium DockerHub.</span><span class="sxs-lookup"><span data-stu-id="8c90e-128">Provide hello URL for hello container image from a DockerHub repo.</span></span> <span data-ttu-id="8c90e-129">Witaj formularz hello przyjmuje parametr obrazu [repozytorium] / [nazwa obrazu]</span><span class="sxs-lookup"><span data-stu-id="8c90e-129">hello image parameter takes hello form [repo]/[image name]</span></span>
4. <span data-ttu-id="8c90e-130">Jeśli obraz powitania nie ma obciążenia punktu wejścia zdefiniowana, a następnie należy tooexplicitly określić wejściowych polecenia przy użyciu zestawu poleceń toorun wewnątrz kontenera hello zachowa kontenera hello uruchomiona po uruchomieniu rozdzielonych przecinkami.</span><span class="sxs-lookup"><span data-stu-id="8c90e-130">If hello image does not have a workload entry-point defined, then you need tooexplicitly specify input commands with a comma-delimited set of commands toorun inside hello container, which will keep hello container running after startup.</span></span>

![Generator Yeoman usługi Service Fabric dla kontenerów][sf-yeoman]

## <a name="deploy-hello-application"></a><span data-ttu-id="8c90e-132">Wdrażanie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="8c90e-132">Deploy hello application</span></span>

### <a name="using-xplat-cli"></a><span data-ttu-id="8c90e-133">Korzystanie z interfejsu wiersza polecenia XPlat</span><span class="sxs-lookup"><span data-stu-id="8c90e-133">Using XPlat CLI</span></span>
<span data-ttu-id="8c90e-134">Po utworzeniu aplikacji hello można wdrożyć klaster lokalny toohello przy użyciu hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="8c90e-134">Once hello application is built, you can deploy it toohello local cluster using hello Azure CLI.</span></span>

1. <span data-ttu-id="8c90e-135">Połącz toohello lokalnego klastra usługi sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="8c90e-135">Connect toohello local Service Fabric cluster.</span></span>

    ```bash
    azure servicefabric cluster connect
    ```

2. <span data-ttu-id="8c90e-136">Użyj hello zainstalować skrypt toocopy szablonu hello aplikacji hello pakietu magazynu obrazu klastra toohello, Rejestracja typu aplikacji hello, i Utwórz wystąpienie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="8c90e-136">Use hello install script provided in hello template toocopy hello application package toohello cluster's image store, register hello application type, and create an instance of hello application.</span></span>

    ```bash
    ./install.sh
    ```

3. <span data-ttu-id="8c90e-137">Otwórz przeglądarkę i przejdź tooService Eksploratora sieci szkieletowej w http://localhost: 19080/Explorer (localhost Zamień z hello prywatnego adresu IP hello maszyny Wirtualnej, jeśli przy użyciu Vagrant w systemie Mac OS X).</span><span class="sxs-lookup"><span data-stu-id="8c90e-137">Open a browser and navigate tooService Fabric Explorer at http://localhost:19080/Explorer (replace localhost with hello private IP of hello VM if using Vagrant on Mac OS X).</span></span>
4. <span data-ttu-id="8c90e-138">Rozwiń węzeł aplikacji hello i należy pamiętać, że teraz wpis dla danego typu aplikacji i drugi dla hello pierwsze wystąpienie tego typu.</span><span class="sxs-lookup"><span data-stu-id="8c90e-138">Expand hello Applications node and note that there is now an entry for your application type and another for hello first instance of that type.</span></span>
5. <span data-ttu-id="8c90e-139">Użyj skryptu Odinstaluj hello podane w wystąpienia aplikacji hello hello szablonu toodelete i wyrejestrowywanie typu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="8c90e-139">Use hello uninstall script provided in hello template toodelete hello application instance and unregister hello application type.</span></span>

    ```bash
    ./uninstall.sh
    ```

### <a name="using-azure-cli-20"></a><span data-ttu-id="8c90e-140">Korzystanie z interfejsu wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="8c90e-140">Using Azure CLI 2.0</span></span>

<span data-ttu-id="8c90e-141">Zobacz hello odwołania dokumentu na zarządzaniu [cyklu życia aplikacji przy użyciu hello Azure CLI 2.0](service-fabric-application-lifecycle-azure-cli-2-0.md).</span><span class="sxs-lookup"><span data-stu-id="8c90e-141">See hello reference doc on managing an [application life cycle using hello Azure CLI 2.0](service-fabric-application-lifecycle-azure-cli-2-0.md).</span></span>

<span data-ttu-id="8c90e-142">Na przykład aplikacja [przykłady hello wyewidencjonowania kodu kontenera sieci szkieletowej usług w witrynie GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span><span class="sxs-lookup"><span data-stu-id="8c90e-142">For an example application, [checkout hello Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>

## <a name="adding-more-services-tooan-existing-application"></a><span data-ttu-id="8c90e-143">Dodawanie więcej usług tooan istniejącej aplikacji</span><span class="sxs-lookup"><span data-stu-id="8c90e-143">Adding more services tooan existing application</span></span>

<span data-ttu-id="8c90e-144">tooadd innego kontenera usługi już utworzone przy użyciu aplikacji tooan `yo`, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="8c90e-144">tooadd another container service tooan application already created using `yo`, perform hello following steps:</span></span>

1. <span data-ttu-id="8c90e-145">Zmień katalog główny toohello hello istniejącej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8c90e-145">Change directory toohello root of hello existing application.</span></span>  <span data-ttu-id="8c90e-146">Na przykład `cd ~/YeomanSamples/MyApplication`, jeśli `MyApplication` to aplikacja hello utworzone przez narzędzia Yeoman.</span><span class="sxs-lookup"><span data-stu-id="8c90e-146">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is hello application created by Yeoman.</span></span>
2. <span data-ttu-id="8c90e-147">Uruchom polecenie `yo azuresfcontainer:AddService`</span><span class="sxs-lookup"><span data-stu-id="8c90e-147">Run `yo azuresfcontainer:AddService`</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a><span data-ttu-id="8c90e-148">Ręcznie pakietów i wdrożyć obraz kontenera</span><span class="sxs-lookup"><span data-stu-id="8c90e-148">Manually package and deploy a container image</span></span>
<span data-ttu-id="8c90e-149">proces Hello ręcznie pakowania konteneryzowanych usługi jest oparty na powitania następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="8c90e-149">hello process of manually packaging a containerized service is based on hello following steps:</span></span>

1. <span data-ttu-id="8c90e-150">Opublikuj hello kontenery tooyour repozytorium.</span><span class="sxs-lookup"><span data-stu-id="8c90e-150">Publish hello containers tooyour repository.</span></span>
2. <span data-ttu-id="8c90e-151">Utwórz strukturę katalogów hello pakietu.</span><span class="sxs-lookup"><span data-stu-id="8c90e-151">Create hello package directory structure.</span></span>
3. <span data-ttu-id="8c90e-152">Edytuj hello pliku manifestu usługi.</span><span class="sxs-lookup"><span data-stu-id="8c90e-152">Edit hello service manifest file.</span></span>
4. <span data-ttu-id="8c90e-153">Edytuj plik manifestu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="8c90e-153">Edit hello application manifest file.</span></span>

## <a name="deploy-and-activate-a-container-image"></a><span data-ttu-id="8c90e-154">Wdrażanie i aktywować obrazu kontenera</span><span class="sxs-lookup"><span data-stu-id="8c90e-154">Deploy and activate a container image</span></span>
<span data-ttu-id="8c90e-155">W sieci szkieletowej usług hello [model aplikacji](service-fabric-application-model.md), kontener reprezentuje hosta aplikacji, w których wiele usługi repliki są umieszczane.</span><span class="sxs-lookup"><span data-stu-id="8c90e-155">In hello Service Fabric [application model](service-fabric-application-model.md), a container represents an application host in which multiple service replicas are placed.</span></span> <span data-ttu-id="8c90e-156">toodeploy i Aktywuj kontener, umieść hello nazwa hello kontener obrazu do `ContainerHost` element hello manifestu usługi.</span><span class="sxs-lookup"><span data-stu-id="8c90e-156">toodeploy and activate a container, put hello name of hello container image into a `ContainerHost` element in hello service manifest.</span></span>

<span data-ttu-id="8c90e-157">W manifeście usługi hello, Dodaj `ContainerHost` hello punktu wejścia.</span><span class="sxs-lookup"><span data-stu-id="8c90e-157">In hello service manifest, add a `ContainerHost` for hello entry point.</span></span> <span data-ttu-id="8c90e-158">Następnie zestaw hello `ImageName` toobe hello nazwę hello kontenera repozytorium i obrazów.</span><span class="sxs-lookup"><span data-stu-id="8c90e-158">Then set hello `ImageName` toobe hello name of hello container repository and image.</span></span> <span data-ttu-id="8c90e-159">Hello następujące manifest częściowe przedstawiono przykład sposobu toodeploy hello kontenera o nazwie `myimage:v1` z repozytorium o nazwie `myrepo`:</span><span class="sxs-lookup"><span data-stu-id="8c90e-159">hello following partial manifest shows an example of how toodeploy hello container called `myimage:v1` from a repository called `myrepo`:</span></span>

```xml
    <CodePackage Name="Code" Version="1.0">
        <EntryPoint>
          <ContainerHost>
            <ImageName>myrepo/myimage:v1</ImageName>
            <Commands></Commands>
          </ContainerHost>
        </EntryPoint>
    </CodePackage>
```

<span data-ttu-id="8c90e-160">Możesz podać polecenia wejściowe, określając hello opcjonalne `Commands` elementu przy użyciu zestawu poleceń toorun wewnątrz kontenera hello rozdzielonych przecinkami.</span><span class="sxs-lookup"><span data-stu-id="8c90e-160">You can provide input commands by specifying hello optional `Commands` element with a comma-delimited set of commands toorun inside hello container.</span></span>

> [!NOTE]
> <span data-ttu-id="8c90e-161">Jeśli obraz powitania nie ma obciążenia punktu wejścia zdefiniowana, a następnie należy tooexplicitly określić polecenia wprowadzania wewnątrz `Commands` elementu przy użyciu zestawu poleceń toorun wewnątrz kontenera hello, w którym zostaną zachowane po kontenera hello rozdzielana przecinkami uruchamianie.</span><span class="sxs-lookup"><span data-stu-id="8c90e-161">If hello image does not have a workload entry-point defined, then you need tooexplicitly specify input commands inside `Commands` element with a comma-delimited set of commands toorun inside hello container, which will keep hello container running after startup.</span></span>

## <a name="understand-resource-governance"></a><span data-ttu-id="8c90e-162">Zrozumienie ładu zasobów</span><span class="sxs-lookup"><span data-stu-id="8c90e-162">Understand resource governance</span></span>
<span data-ttu-id="8c90e-163">Możliwość hello kontenera, który ogranicza hello zasobów, które hello kontenera można używać na hoście hello jest ładu zasobów.</span><span class="sxs-lookup"><span data-stu-id="8c90e-163">Resource governance is a capability of hello container that restricts hello resources that hello container can use on hello host.</span></span> <span data-ttu-id="8c90e-164">Witaj `ResourceGovernancePolicy`, który został określony w manifeście aplikacji hello jest używane toodeclare limity zasobów pakietu kodu usługi.</span><span class="sxs-lookup"><span data-stu-id="8c90e-164">hello `ResourceGovernancePolicy`, which is specified in hello application manifest is used toodeclare resource limits for a service code package.</span></span> <span data-ttu-id="8c90e-165">Limity zasobów można ustawić dla hello następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="8c90e-165">Resource limits can be set for hello following resources:</span></span>

* <span data-ttu-id="8c90e-166">Memory (Pamięć)</span><span class="sxs-lookup"><span data-stu-id="8c90e-166">Memory</span></span>
* <span data-ttu-id="8c90e-167">MemorySwap</span><span class="sxs-lookup"><span data-stu-id="8c90e-167">MemorySwap</span></span>
* <span data-ttu-id="8c90e-168">CpuShares (względną wagę procesora CPU)</span><span class="sxs-lookup"><span data-stu-id="8c90e-168">CpuShares (CPU relative weight)</span></span>
* <span data-ttu-id="8c90e-169">MemoryReservationInMB</span><span class="sxs-lookup"><span data-stu-id="8c90e-169">MemoryReservationInMB</span></span>  
* <span data-ttu-id="8c90e-170">BlkioWeight (BlockIO względną wagę).</span><span class="sxs-lookup"><span data-stu-id="8c90e-170">BlkioWeight (BlockIO relative weight).</span></span>

> [!NOTE]
> <span data-ttu-id="8c90e-171">W przyszłym wydaniu obsługę bloku określonego limity we/wy, takich jak IOPs, określając odczytu/zapisu liczby bitów na Sekundę i inni użytkownicy będą dołączone.</span><span class="sxs-lookup"><span data-stu-id="8c90e-171">In a future release, support for specifying specific block IO limits such as IOPs, read/write BPS, and others will be included.</span></span>
>
>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ResourceGovernancePolicy CodePackageRef="FrontendService.Code" CpuShares="500"
            MemoryInMB="1024" MemorySwapInMB="4084" MemoryReservationInMB="1024" />
        </Policies>
    </ServiceManifestImport>
```

## <a name="authenticate-a-repository"></a><span data-ttu-id="8c90e-172">Uwierzytelnianie repozytorium</span><span class="sxs-lookup"><span data-stu-id="8c90e-172">Authenticate a repository</span></span>
<span data-ttu-id="8c90e-173">toodownload kontener może być tooprovide poświadczenia logowania toohello kontenera repozytorium.</span><span class="sxs-lookup"><span data-stu-id="8c90e-173">toodownload a container, you might have tooprovide sign-in credentials toohello container repository.</span></span> <span data-ttu-id="8c90e-174">Hello poświadczenia logowania, określona w manifeście aplikacji hello, są używane toospecify hello informacje rejestrowania lub klucza SSH do pobrania obrazu kontenera hello hello repozytorium obrazów.</span><span class="sxs-lookup"><span data-stu-id="8c90e-174">hello sign-in credentials, specified in hello application manifest, are used toospecify hello sign-in information, or SSH key, for downloading hello container image from hello image repository.</span></span> <span data-ttu-id="8c90e-175">Witaj poniższy przykład przedstawia konta o nazwie *TestUser* wraz z hello hasła w postaci zwykłego tekstu (*nie* zalecana):</span><span class="sxs-lookup"><span data-stu-id="8c90e-175">hello following example shows an account called *TestUser* along with hello password in clear text (*not* recommended):</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <RepositoryCredentials AccountName="TestUser" Password="12345" PasswordEncrypted="false"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

<span data-ttu-id="8c90e-176">Firma Microsoft zaleca szyfrowania hello hasła przy użyciu certyfikatu, który został wdrożony toohello maszyny.</span><span class="sxs-lookup"><span data-stu-id="8c90e-176">We recommend that you encrypt hello password by using a certificate that's deployed toohello machine.</span></span>

<span data-ttu-id="8c90e-177">Witaj poniższy przykład przedstawia konta o nazwie *TestUser*, gdzie hasło hello została zaszyfrowana przy użyciu certyfikatu o nazwie *MyCert*.</span><span class="sxs-lookup"><span data-stu-id="8c90e-177">hello following example shows an account called *TestUser*, where hello password was encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="8c90e-178">Można użyć hello `Invoke-ServiceFabricEncryptText` tekst toocreate polecenia programu PowerShell tajny szyfrowania hello hello hasła.</span><span class="sxs-lookup"><span data-stu-id="8c90e-178">You can use hello `Invoke-ServiceFabricEncryptText` PowerShell command toocreate hello secret cipher text for hello password.</span></span> <span data-ttu-id="8c90e-179">Aby uzyskać więcej informacji, zobacz artykuł hello [Zarządzanie kluczy tajnych w aplikacji usługi Service Fabric](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="8c90e-179">For more information, see hello article [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md).</span></span>

<span data-ttu-id="8c90e-180">klucz prywatny Hello hello certyfikatu, który został użyty toodecrypt hello hasło musi być wdrożone toohello komputera lokalnego w metodzie poza pasmem.</span><span class="sxs-lookup"><span data-stu-id="8c90e-180">hello private key of hello certificate that's used toodecrypt hello password must be deployed toohello local machine in an out-of-band method.</span></span> <span data-ttu-id="8c90e-181">(Na platformie Azure, ta metoda jest usługi Azure Resource Manager). Następnie gdy usługa sieć szkieletowa wdraża hello usługi pakietu toohello maszyny, może odszyfrować klucza tajnego hello.</span><span class="sxs-lookup"><span data-stu-id="8c90e-181">(In Azure, this method is Azure Resource Manager.) Then, when Service Fabric deploys hello service package toohello machine, it can decrypt hello secret.</span></span> <span data-ttu-id="8c90e-182">Przy użyciu klucza tajnego hello wraz z nazwą konta hello, następnie uwierzytelniania hello kontenera repozytorium.</span><span class="sxs-lookup"><span data-stu-id="8c90e-182">By using hello secret along with hello account name, it can then authenticate with hello container repository.</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <RepositoryCredentials AccountName="TestUser" Password="[Put encrypted password here using MyCert certificate ]" PasswordEncrypted="true"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

## <a name="configure-container-port-to-host-port-mapping"></a><span data-ttu-id="8c90e-183">Skonfiguruj mapowanie portów port kontenera do hosta</span><span class="sxs-lookup"><span data-stu-id="8c90e-183">Configure container port-to-host port mapping</span></span>
<span data-ttu-id="8c90e-184">Można skonfigurować toocommunicate port używany host hello kontenera, określając `PortBinding` w manifeście aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="8c90e-184">You can configure a host port used toocommunicate with hello container by specifying a `PortBinding` in hello application manifest.</span></span> <span data-ttu-id="8c90e-185">wewnątrz hello kontenera tooa portu na hoście hello nasłuchuje Hello portu powiązania mapy hello portu toowhich hello usługa.</span><span class="sxs-lookup"><span data-stu-id="8c90e-185">hello port binding maps hello port toowhich hello service is listening inside hello container tooa port on hello host.</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <PortBinding ContainerPort="8905"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

## <a name="configure-container-to-container-discovery-and-communication"></a><span data-ttu-id="8c90e-186">Konfigurowanie odnajdywania kontenera do kontenera i komunikacji</span><span class="sxs-lookup"><span data-stu-id="8c90e-186">Configure container-to-container discovery and communication</span></span>
<span data-ttu-id="8c90e-187">Za pomocą hello `PortBinding` zasad, możesz mapować tooan port kontenera `Endpoint` w hello manifestu usługi.</span><span class="sxs-lookup"><span data-stu-id="8c90e-187">By using hello `PortBinding` policy, you can map a container port tooan `Endpoint` in hello service manifest.</span></span> <span data-ttu-id="8c90e-188">Witaj punktu końcowego `Endpoint1` można określić stały port (na przykład port 80).</span><span class="sxs-lookup"><span data-stu-id="8c90e-188">hello endpoint `Endpoint1` can specify a fixed port (for example, port 80).</span></span> <span data-ttu-id="8c90e-189">Może również określać nie portu, w tym przypadku losowego portu z zakresu portów aplikacji hello klastra jest wybierany dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="8c90e-189">It can also specify no port at all, in which case a random port from hello cluster's application port range is chosen for you.</span></span>

<span data-ttu-id="8c90e-190">Jeśli określisz punkt końcowy, za pomocą hello `Endpoint` tag w manifeście usługi hello kontenera gościa, Service Fabric automatycznie opublikować toohello tego punktu końcowego usługi nazw.</span><span class="sxs-lookup"><span data-stu-id="8c90e-190">If you specify an endpoint, using hello `Endpoint` tag in hello service manifest of a guest container, Service Fabric can automatically publish this endpoint toohello Naming service.</span></span> <span data-ttu-id="8c90e-191">Inne usługi, które są uruchomione w klastrze hello w związku z tym można odnaleźć tego kontenera za pomocą zapytań REST hello w celu rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="8c90e-191">Other services that are running in hello cluster can thus discover this container using hello REST queries for resolving.</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

<span data-ttu-id="8c90e-192">Zarejestrowani hello Naming service, można łatwo wykonać komunikacji kontenera do kontenera w kodzie hello w Twojej kontenera przy użyciu hello [odwrotny serwer proxy](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="8c90e-192">By registering with hello Naming service, you can easily do container-to-container communication in hello code within your container by using hello [reverse proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="8c90e-193">Komunikacja odbywa się przez podanie port nasłuchujący hello zwrotny serwer proxy http i nazwa hello hello usług, które ma być toocommunicate ze zmiennych środowiskowych.</span><span class="sxs-lookup"><span data-stu-id="8c90e-193">Communication is performed by providing hello reverse proxy http listening port and hello name of hello services that you want toocommunicate with as environment variables.</span></span> <span data-ttu-id="8c90e-194">Aby uzyskać więcej informacji zobacz następną sekcję hello.</span><span class="sxs-lookup"><span data-stu-id="8c90e-194">For more information, see hello next section.</span></span>

## <a name="configure-and-set-environment-variables"></a><span data-ttu-id="8c90e-195">Konfigurowanie i ustawianie zmiennych środowiskowych</span><span class="sxs-lookup"><span data-stu-id="8c90e-195">Configure and set environment variables</span></span>
<span data-ttu-id="8c90e-196">Zmienne środowiskowe można określić dla każdego pakietu kodu w manifeście usługi hello, zarówno dla usługi, które są wdrażane w kontenerach lub usług, które są wdrażane jako pliki wykonywalne procesów/gościa.</span><span class="sxs-lookup"><span data-stu-id="8c90e-196">Environment variables can be specified for each code package in hello service manifest, both for services that are deployed in containers or for services that are deployed as processes/guest executables.</span></span> <span data-ttu-id="8c90e-197">Te wartości zmiennych środowiskowych można zastąpić w szczególności w manifeście aplikacji hello lub określony podczas wdrażania jako parametry aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8c90e-197">These environment variable values can be overridden specifically in hello application manifest or specified during deployment as application parameters.</span></span>

<span data-ttu-id="8c90e-198">Witaj poniższy fragment XML manifestu usługi przedstawia przykładowy sposób zmiennych środowiskowych toospecify pakietu kodu:</span><span class="sxs-lookup"><span data-stu-id="8c90e-198">hello following service manifest XML snippet shows an example of how toospecify environment variables for a code package:</span></span>

```xml
    <ServiceManifest Name="FrontendServicePackage" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description>a guest executable service in a container</Description>
        <ServiceTypes>
            <StatelessServiceType ServiceTypeName="StatelessFrontendService"  UseImplicitHost="true"/>
        </ServiceTypes>
        <CodePackage Name="FrontendService.Code" Version="1.0">
            <EntryPoint>
            <ContainerHost>
                <ImageName>myrepo/myimage:v1</ImageName>
                <Commands></Commands>
            </ContainerHost>
            </EntryPoint>
            <EnvironmentVariables>
                <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
                <EnvironmentVariable Name="BackendServiceName" Value=""/>
            </EnvironmentVariables>
        </CodePackage>
    </ServiceManifest>
```

<span data-ttu-id="8c90e-199">Te zmienne środowiskowe umożliwić przesłanianie go na poziomie manifestu aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="8c90e-199">These environment variables can be overridden at hello application manifest level:</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

<span data-ttu-id="8c90e-200">W poprzednim przykładzie hello, możemy określić jawną wartość dla hello `HttpGateway` zmiennej środowiskowej (19000), gdy firma Microsoft ustaw wartość hello `BackendServiceName` parametr za pomocą hello `[BackendSvc]` parametr aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8c90e-200">In hello previous example, we specified an explicit value for hello `HttpGateway` environment variable (19000), while we set hello value for `BackendServiceName` parameter via hello `[BackendSvc]` application parameter.</span></span> <span data-ttu-id="8c90e-201">Te ustawienia umożliwiają wartość hello toospecify `BackendServiceName`wartość wdrażania aplikacji hello i ma wartość stałą w manifeście hello.</span><span class="sxs-lookup"><span data-stu-id="8c90e-201">These settings enable you toospecify hello value for `BackendServiceName`value when you deploy hello application and not have a fixed value in hello manifest.</span></span>

## <a name="complete-examples-for-application-and-service-manifest"></a><span data-ttu-id="8c90e-202">Zakończenie przykłady aplikacji i manifest usługi</span><span class="sxs-lookup"><span data-stu-id="8c90e-202">Complete examples for application and service manifest</span></span>

<span data-ttu-id="8c90e-203">Następujący przykład manifestu aplikacji:</span><span class="sxs-lookup"><span data-stu-id="8c90e-203">An example application manifest follows:</span></span>

```xml
    <ApplicationManifest ApplicationTypeName="SimpleContainerApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description>A simple service container application</Description>
        <Parameters>
            <Parameter Name="ServiceInstanceCount" DefaultValue="3"></Parameter>
            <Parameter Name="BackEndSvcName" DefaultValue="bkend"></Parameter>
        </Parameters>
        <ServiceManifestImport>
            <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
            <EnvironmentOverrides CodePackageRef="FrontendService.Code">
                <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvcName]"/>
                <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
            </EnvironmentOverrides>
            <Policies>
                <ResourceGovernancePolicy CodePackageRef="Code" CpuShares="500" MemoryInMB="1024" MemorySwapInMB="4084" MemoryReservationInMB="1024" />
                <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                    <RepositoryCredentials AccountName="username" Password="****" PasswordEncrypted="true"/>
                    <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
                </ContainerHostPolicies>
            </Policies>
        </ServiceManifestImport>
    </ApplicationManifest>
```

<span data-ttu-id="8c90e-204">Następujący przykład manifestu usługi (określone w powyższej manifest aplikacji hello):</span><span class="sxs-lookup"><span data-stu-id="8c90e-204">An example service manifest (specified in hello preceding application manifest) follows:</span></span>

```xml
    <ServiceManifest Name="FrontendServicePackage" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description> A service that implements a stateless front end in a container</Description>
        <ServiceTypes>
            <StatelessServiceType ServiceTypeName="StatelessFrontendService"  UseImplicitHost="true"/>
        </ServiceTypes>
        <CodePackage Name="FrontendService.Code" Version="1.0">
            <EntryPoint>
            <ContainerHost>
                <ImageName>myrepo/myimage:v1</ImageName>
                <Commands></Commands>
            </ContainerHost>
            </EntryPoint>
            <EnvironmentVariables>
                <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
                <EnvironmentVariable Name="BackendServiceName" Value=""/>
            </EnvironmentVariables>
        </CodePackage>
        <ConfigPackage Name="FrontendService.Config" Version="1.0" />
        <DataPackage Name="FrontendService.Data" Version="1.0" />
        <Resources>
            <Endpoints>
                <Endpoint Name="Endpoint1" UriScheme="http" Port="80" Protocol="http"/>
            </Endpoints>
        </Resources>
    </ServiceManifest>
```

## <a name="next-steps"></a><span data-ttu-id="8c90e-205">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8c90e-205">Next steps</span></span>
<span data-ttu-id="8c90e-206">Po wdrożeniu usługi konteneryzowanych, Dowiedz się, jak toomanage cykl życia, odczytując [cyklem życia aplikacji usługi sieć szkieletowa](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="8c90e-206">Now that you have deployed a containerized service, learn how toomanage its lifecycle by reading [Service Fabric application lifecycle](service-fabric-application-lifecycle.md).</span></span>

* [<span data-ttu-id="8c90e-207">Omówienie sieci szkieletowej usług i kontenerów</span><span class="sxs-lookup"><span data-stu-id="8c90e-207">Overview of Service Fabric and containers</span></span>](service-fabric-containers-overview.md)
* [<span data-ttu-id="8c90e-208">Interakcja z klastrów sieci szkieletowej usług za pomocą hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="8c90e-208">Interacting with Service Fabric clusters using hello Azure CLI</span></span>](service-fabric-azure-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-deploy-container-linux/sf-container-yeoman1.png

## <a name="related-articles"></a><span data-ttu-id="8c90e-209">Pokrewne artykuły:</span><span class="sxs-lookup"><span data-stu-id="8c90e-209">Related articles</span></span>

* <span data-ttu-id="8c90e-210">[Getting started with Service Fabric and Azure CLI 2.0](service-fabric-azure-cli-2-0.md) (Wprowadzenie do usługi Service Fabric i interfejsu wiersza polecenia platformy Azure 2.0)</span><span class="sxs-lookup"><span data-stu-id="8c90e-210">[Getting started with Service Fabric and Azure CLI 2.0](service-fabric-azure-cli-2-0.md)</span></span>
* <span data-ttu-id="8c90e-211">[Getting started with Service Fabric XPlat CLI](service-fabric-azure-cli.md) (Wprowadzenie do interfejsu wiersza polecenia XPlat usługi Service Fabric)</span><span class="sxs-lookup"><span data-stu-id="8c90e-211">[Getting started with Service Fabric XPlat CLI](service-fabric-azure-cli.md)</span></span>
