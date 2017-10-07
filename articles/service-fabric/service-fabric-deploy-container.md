---
title: "aaaService sieci szkieletowej i wdrażanie kontenerów | Dokumentacja firmy Microsoft"
description: "Sieć szkieletowa usług i hello używają kontenery toodeploy mikrousługi aplikacji. W tym artykule opisano możliwości hello, które zapewnia sieć szkieletowa usług kontenery i jak toodeploy kontenera systemu Windows w obrazie w klastrze."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 799cc9ad-32fd-486e-a6b6-efff6b13622d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 5/16/2017
ms.author: msfussell
ms.openlocfilehash: 8b6540579641474f21b8712b56049c7d177bec26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-windows-container-tooservice-fabric"></a><span data-ttu-id="eb43e-104">Wdrażanie systemu Windows tooService kontenera sieci szkieletowej</span><span class="sxs-lookup"><span data-stu-id="eb43e-104">Deploy a Windows container tooService Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="eb43e-105">Wdrażanie kontenera systemu Windows</span><span class="sxs-lookup"><span data-stu-id="eb43e-105">Deploy Windows Container</span></span>](service-fabric-deploy-container.md)
> * [<span data-ttu-id="eb43e-106">Wdrażanie kontenera Docker</span><span class="sxs-lookup"><span data-stu-id="eb43e-106">Deploy Docker Container</span></span>](service-fabric-deploy-container-linux.md)
> 
> 

<span data-ttu-id="eb43e-107">Ten artykuł przeprowadzi Cię przez proces tworzenia konteneryzowanych usług w kontenerach Windows hello.</span><span class="sxs-lookup"><span data-stu-id="eb43e-107">This article walks you through hello process of building containerized services in Windows containers.</span></span>

<span data-ttu-id="eb43e-108">Sieć szkieletowa usług ma kilka możliwości, które zapewniają pomoc podczas tworzenia aplikacji, które składają się z mikrousług uruchomiony kontenerów.</span><span class="sxs-lookup"><span data-stu-id="eb43e-108">Service Fabric has several capabilities that help you with building applications that are composed of microservices running inside containers.</span></span> 

<span data-ttu-id="eb43e-109">Witaj funkcje obejmują:</span><span class="sxs-lookup"><span data-stu-id="eb43e-109">hello capabilities include:</span></span>

* <span data-ttu-id="eb43e-110">Kontener obrazu wdrożenia i aktywacji</span><span class="sxs-lookup"><span data-stu-id="eb43e-110">Container image deployment and activation</span></span>
* <span data-ttu-id="eb43e-111">Zarządzanie zasobów</span><span class="sxs-lookup"><span data-stu-id="eb43e-111">Resource governance</span></span>
* <span data-ttu-id="eb43e-112">Repozytorium uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="eb43e-112">Repository authentication</span></span>
* <span data-ttu-id="eb43e-113">Mapowanie portów port kontenera do hosta</span><span class="sxs-lookup"><span data-stu-id="eb43e-113">Container port-to-host port mapping</span></span>
* <span data-ttu-id="eb43e-114">Odnajdywanie kontenera do kontenera i komunikacji</span><span class="sxs-lookup"><span data-stu-id="eb43e-114">Container-to-container discovery and communication</span></span>
* <span data-ttu-id="eb43e-115">Możliwość tooconfigure i ustaw zmienne środowiskowe</span><span class="sxs-lookup"><span data-stu-id="eb43e-115">Ability tooconfigure and set environment variables</span></span>

<span data-ttu-id="eb43e-116">Oto jak działa każdy z możliwości podczas pakowane toobe konteneryzowanych usługi, dołączony do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="eb43e-116">Let's look at how each of capabilities works when you're packaging a containerized service toobe included in your application.</span></span>

## <a name="package-a-windows-container"></a><span data-ttu-id="eb43e-117">Pakiet kontenera systemu Windows</span><span class="sxs-lookup"><span data-stu-id="eb43e-117">Package a Windows container</span></span>
<span data-ttu-id="eb43e-118">Podczas pakowania kontener możesz toouse albo szablon projektu Visual Studio lub [ręcznie utworzyć pakiet aplikacji hello](#manually).</span><span class="sxs-lookup"><span data-stu-id="eb43e-118">When you package a container, you can choose toouse either a Visual Studio project template or [create hello application package manually](#manually).</span></span>  <span data-ttu-id="eb43e-119">Gdy używasz programu Visual Studio, struktura pakietu aplikacji hello i pliki manifestu zostają utworzone przez szablon nowego projektu hello.</span><span class="sxs-lookup"><span data-stu-id="eb43e-119">When you use Visual Studio, hello application package structure and manifest files are created by hello New Project template for you.</span></span>

> [!TIP]
> <span data-ttu-id="eb43e-120">Witaj najprostszy sposób toopackage istniejącego obrazu kontenera do usługi jest toouse programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="eb43e-120">hello easiest way toopackage an existing container image into a service is toouse Visual Studio.</span></span>

## <a name="use-visual-studio-toopackage-an-existing-container-image"></a><span data-ttu-id="eb43e-121">Użyj programu Visual Studio toopackage istniejącego obrazu kontenera</span><span class="sxs-lookup"><span data-stu-id="eb43e-121">Use Visual Studio toopackage an existing container image</span></span>
<span data-ttu-id="eb43e-122">Program Visual Studio udostępnia usługi sieć szkieletowa toohelp szablonu usługi, w przypadku wdrażania klastra usługi sieć szkieletowa tooa kontenera.</span><span class="sxs-lookup"><span data-stu-id="eb43e-122">Visual Studio provides a Service Fabric service template toohelp you deploy a container tooa Service Fabric cluster.</span></span>

1. <span data-ttu-id="eb43e-123">Wybierz **pliku** > **nowy projekt**i tworzenie aplikacji sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="eb43e-123">Choose **File** > **New Project**, and create a Service Fabric application.</span></span>
2. <span data-ttu-id="eb43e-124">Wybierz **kontenera gościa** jako hello szablonu usługi.</span><span class="sxs-lookup"><span data-stu-id="eb43e-124">Choose **Guest Container** as hello service template.</span></span>
3. <span data-ttu-id="eb43e-125">Wybierz **nazwa obrazu** i podaj hello ścieżki toohello obrazu w repozytorium kontenera.</span><span class="sxs-lookup"><span data-stu-id="eb43e-125">Choose **Image Name** and provide hello path toohello image in your container repository.</span></span> <span data-ttu-id="eb43e-126">Na przykład `myrepo/myimage:v1` w https://hub.docker.com</span><span class="sxs-lookup"><span data-stu-id="eb43e-126">For example, `myrepo/myimage:v1` in https://hub.docker.com</span></span>
4. <span data-ttu-id="eb43e-127">Nadaj nazwę usłudze i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="eb43e-127">Give your service a name, and click **OK**.</span></span>
5. <span data-ttu-id="eb43e-128">Jeśli usługa konteneryzowanych musi punkt końcowy komunikacji, można teraz dodawać hello protokół, port i plik ServiceManifest.xml toohello typu.</span><span class="sxs-lookup"><span data-stu-id="eb43e-128">If your containerized service needs an endpoint for communication, you can now add hello protocol, port, and type toohello ServiceManifest.xml file.</span></span> <span data-ttu-id="eb43e-129">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="eb43e-129">For example:</span></span> 
     
    `<Endpoint Name="MyContainerServiceEndpoint" Protocol="http" Port="80" UriScheme="http" PathSuffix="myapp/" Type="Input" />`
    
    <span data-ttu-id="eb43e-130">Zapewniając hello `UriScheme`, usługi sieć szkieletowa automatycznie rejestruje punkt końcowy kontenera hello hello usługi nazewnictwa w celu odnajdywania.</span><span class="sxs-lookup"><span data-stu-id="eb43e-130">By providing hello `UriScheme`, Service Fabric automatically registers hello container endpoint with hello Naming service for discoverability.</span></span> <span data-ttu-id="eb43e-131">Hello port być stałe (jak pokazano w hello poprzedzających przykład) lub dynamicznie przydzielane.</span><span class="sxs-lookup"><span data-stu-id="eb43e-131">hello port can either be fixed (as shown in hello preceding example) or dynamically allocated.</span></span> <span data-ttu-id="eb43e-132">Jeśli nie określisz port dynamicznie nadawany z zakresu portów aplikacji hello (co się stanie z dowolnej usługi).</span><span class="sxs-lookup"><span data-stu-id="eb43e-132">If you don't specify a port, it is dynamically allocated from hello application port range (as would happen with any service).</span></span>
    <span data-ttu-id="eb43e-133">Należy również mapowanie portów toohost tooconfigure hello kontenera, określając `PortBinding` zasad w manifeście aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="eb43e-133">You also need tooconfigure hello container toohost port mapping by specifying a `PortBinding` policy in hello application manifest.</span></span> <span data-ttu-id="eb43e-134">Aby uzyskać więcej informacji, zobacz [skonfigurować mapowanie portów toohost kontenera](#Portsection).</span><span class="sxs-lookup"><span data-stu-id="eb43e-134">For more information, see [Configure container toohost port mapping](#Portsection).</span></span>
6. <span data-ttu-id="eb43e-135">Jeśli z kontenera musi ładu zasobów, a następnie dodaj `ResourceGovernancePolicy`.</span><span class="sxs-lookup"><span data-stu-id="eb43e-135">If your container needs resource governance then add a `ResourceGovernancePolicy`.</span></span>
8. <span data-ttu-id="eb43e-136">Jeśli Twoje kontenera musi tooauthenticate z prywatnym repozytorium, Dodaj `RepositoryCredentials`.</span><span class="sxs-lookup"><span data-stu-id="eb43e-136">If your container needs tooauthenticate with a private repository, then add `RepositoryCredentials`.</span></span>
7. <span data-ttu-id="eb43e-137">Jeśli są uruchomione na komputerze z systemem Windows Server 2016, z włączoną obsługą kontenera, można użyć pakietu hello i opublikować akcji toodeploy tooyour lokalnym klastrem.</span><span class="sxs-lookup"><span data-stu-id="eb43e-137">If you are running on a Windows Server 2016 machine with container support enabled, you can use hello package and publish action toodeploy tooyour local cluster.</span></span> 
8. <span data-ttu-id="eb43e-138">Po wykonaniu tych czynności można publikować klastra zdalnego tooa aplikacji hello lub zaewidencjonować hello rozwiązania toosource formantu.</span><span class="sxs-lookup"><span data-stu-id="eb43e-138">When ready, you can publish hello application tooa remote cluster or check in hello solution toosource control.</span></span> 

<span data-ttu-id="eb43e-139">Na przykład hello wyewidencjonowania [przykłady kodu kontenera sieci szkieletowej usług w witrynie GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span><span class="sxs-lookup"><span data-stu-id="eb43e-139">For an example, checkout hello [Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>

## <a name="creating-a-windows-server-2016-cluster"></a><span data-ttu-id="eb43e-140">Tworzenie klastra z systemem Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="eb43e-140">Creating a Windows Server 2016 cluster</span></span>
<span data-ttu-id="eb43e-141">toodeploy konteneryzowanych aplikacji, należy toocreate włączone klastra z systemem Windows Server 2016 z obsługą kontenera.</span><span class="sxs-lookup"><span data-stu-id="eb43e-141">toodeploy your containerized application, you need toocreate a cluster running Windows Server 2016 with container support enabled.</span></span> <span data-ttu-id="eb43e-142">Klaster może działać lokalnie lub wdrożone za pośrednictwem usługi Azure Resource Manager na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="eb43e-142">Your cluster may be running locally, or deployed via Azure Resource Manager in Azure.</span></span> 

<span data-ttu-id="eb43e-143">toodeploy klastra przy użyciu usługi Azure Resource Manager, wybierz hello **systemu Windows Server 2016 z kontenerami** obrazu opcji na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="eb43e-143">toodeploy a cluster using Azure Resource Manager, choose hello **Windows Server 2016 with Containers** image option in Azure.</span></span> <span data-ttu-id="eb43e-144">Zobacz artykuł hello [tworzenia klastra usługi sieć szkieletowa usług za pomocą usługi Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="eb43e-144">See hello article [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="eb43e-145">Upewnij się, że używasz hello następujące ustawienia usługi Azure Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="eb43e-145">Ensure that you use hello following Azure Resource Manager settings:</span></span>

```xml
"vmImageOffer": { "type": "string","defaultValue": "WindowsServer"     },
"vmImageSku": { "defaultValue": "2016-Datacenter-with-Containers","type": "string"     },
"vmImageVersion": { "defaultValue": "latest","type": "string"     },  
```
<span data-ttu-id="eb43e-146">Można również użyć hello [szablonu pięć węzłów usługi Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) toocreate klastra.</span><span class="sxs-lookup"><span data-stu-id="eb43e-146">You can also use hello [Five Node Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) toocreate a cluster.</span></span> <span data-ttu-id="eb43e-147">Można również odczytać społeczność [wpis w blogu](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html) przy użyciu kontenerów sieci szkieletowej usług i systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="eb43e-147">Alternatively read a community [blog post](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html) on using Service Fabric and Windows containers.</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a><span data-ttu-id="eb43e-148">Ręcznie pakietów i wdrożyć obraz kontenera</span><span class="sxs-lookup"><span data-stu-id="eb43e-148">Manually package and deploy a container image</span></span>
<span data-ttu-id="eb43e-149">proces Hello ręcznie pakowania konteneryzowanych usługi jest oparty na powitania następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="eb43e-149">hello process of manually packaging a containerized service is based on hello following steps:</span></span>

1. <span data-ttu-id="eb43e-150">Opublikuj hello kontenery tooyour repozytorium.</span><span class="sxs-lookup"><span data-stu-id="eb43e-150">Publish hello containers tooyour repository.</span></span>
2. <span data-ttu-id="eb43e-151">Utwórz strukturę katalogów hello pakietu.</span><span class="sxs-lookup"><span data-stu-id="eb43e-151">Create hello package directory structure.</span></span>
3. <span data-ttu-id="eb43e-152">Edytuj hello pliku manifestu usługi.</span><span class="sxs-lookup"><span data-stu-id="eb43e-152">Edit hello service manifest file.</span></span>
4. <span data-ttu-id="eb43e-153">Edytuj plik manifestu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="eb43e-153">Edit hello application manifest file.</span></span>

## <a name="deploy-and-activate-a-container-image"></a><span data-ttu-id="eb43e-154">Wdrażanie i aktywować obrazu kontenera</span><span class="sxs-lookup"><span data-stu-id="eb43e-154">Deploy and activate a container image</span></span>
<span data-ttu-id="eb43e-155">W sieci szkieletowej usług hello [model aplikacji](service-fabric-application-model.md), kontener reprezentuje hosta aplikacji, w których wiele usługi repliki są umieszczane.</span><span class="sxs-lookup"><span data-stu-id="eb43e-155">In hello Service Fabric [application model](service-fabric-application-model.md), a container represents an application host in which multiple service replicas are placed.</span></span> <span data-ttu-id="eb43e-156">toodeploy i Aktywuj kontener, umieść hello nazwa hello kontener obrazu do `ContainerHost` element hello manifestu usługi.</span><span class="sxs-lookup"><span data-stu-id="eb43e-156">toodeploy and activate a container, put hello name of hello container image into a `ContainerHost` element in hello service manifest.</span></span>

<span data-ttu-id="eb43e-157">W manifeście usługi hello, Dodaj `ContainerHost` hello punktu wejścia.</span><span class="sxs-lookup"><span data-stu-id="eb43e-157">In hello service manifest, add a `ContainerHost` for hello entry point.</span></span> <span data-ttu-id="eb43e-158">Następnie zestaw hello `ImageName` toobe hello nazwę hello kontenera repozytorium i obrazów.</span><span class="sxs-lookup"><span data-stu-id="eb43e-158">Then set hello `ImageName` toobe hello name of hello container repository and image.</span></span> <span data-ttu-id="eb43e-159">Hello następujące manifest częściowe przedstawiono przykład sposobu toodeploy hello kontenera o nazwie `myimage:v1` z repozytorium o nazwie `myrepo`:</span><span class="sxs-lookup"><span data-stu-id="eb43e-159">hello following partial manifest shows an example of how toodeploy hello container called `myimage:v1` from a repository called `myrepo`:</span></span>

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

<span data-ttu-id="eb43e-160">Można określić opcjonalne polecenia toorun po uruchomieniu hello kontenerów hello `Commands` elementu.</span><span class="sxs-lookup"><span data-stu-id="eb43e-160">You can specify optional commands toorun upon starting hello container under hello `Commands` element.</span></span> <span data-ttu-id="eb43e-161">Dla wielu poleceń przecinkami ograniczyć ich.</span><span class="sxs-lookup"><span data-stu-id="eb43e-161">For multiple commands, comma-delimit them.</span></span> 

## <a name="understand-resource-governance"></a><span data-ttu-id="eb43e-162">Zrozumienie ładu zasobów</span><span class="sxs-lookup"><span data-stu-id="eb43e-162">Understand resource governance</span></span>
<span data-ttu-id="eb43e-163">Możliwość hello kontenera, który ogranicza hello zasobów, które hello kontenera można używać na hoście hello jest ładu zasobów.</span><span class="sxs-lookup"><span data-stu-id="eb43e-163">Resource governance is a capability of hello container that restricts hello resources that hello container can use on hello host.</span></span> <span data-ttu-id="eb43e-164">Witaj `ResourceGovernancePolicy`, który został określony w manifeście aplikacji hello jest używane toodeclare limity zasobów pakietu kodu usługi.</span><span class="sxs-lookup"><span data-stu-id="eb43e-164">hello `ResourceGovernancePolicy`, which is specified in hello application manifest is used toodeclare resource limits for a service code package.</span></span> <span data-ttu-id="eb43e-165">Limity zasobów można ustawić dla hello następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="eb43e-165">Resource limits can be set for hello following resources:</span></span>

* <span data-ttu-id="eb43e-166">Memory (Pamięć)</span><span class="sxs-lookup"><span data-stu-id="eb43e-166">Memory</span></span>
* <span data-ttu-id="eb43e-167">MemorySwap</span><span class="sxs-lookup"><span data-stu-id="eb43e-167">MemorySwap</span></span>
* <span data-ttu-id="eb43e-168">CpuShares (względną wagę procesora CPU)</span><span class="sxs-lookup"><span data-stu-id="eb43e-168">CpuShares (CPU relative weight)</span></span>
* <span data-ttu-id="eb43e-169">MemoryReservationInMB</span><span class="sxs-lookup"><span data-stu-id="eb43e-169">MemoryReservationInMB</span></span>  
* <span data-ttu-id="eb43e-170">BlkioWeight (BlockIO względną wagę).</span><span class="sxs-lookup"><span data-stu-id="eb43e-170">BlkioWeight (BlockIO relative weight).</span></span>

> [!NOTE]
> <span data-ttu-id="eb43e-171">Obsługa służącą do określonego bloku limity we/wy, takie jak IOPs, odczytu/zapisu liczby bitów na Sekundę i inne osoby, które są planowane w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="eb43e-171">Support for specifying specific block IO limits such as IOPs, read/write BPS, and others are planned for a future release.</span></span>
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

## <a name="authenticate-a-repository"></a><span data-ttu-id="eb43e-172">Uwierzytelnianie repozytorium</span><span class="sxs-lookup"><span data-stu-id="eb43e-172">Authenticate a repository</span></span>
<span data-ttu-id="eb43e-173">toodownload kontener może być tooprovide poświadczenia logowania toohello kontenera repozytorium.</span><span class="sxs-lookup"><span data-stu-id="eb43e-173">toodownload a container, you might have tooprovide sign-in credentials toohello container repository.</span></span> <span data-ttu-id="eb43e-174">Hello poświadczenia logowania, określona w manifeście aplikacji hello, są używane toospecify hello informacje rejestrowania lub klucza SSH do pobrania obrazu kontenera hello hello repozytorium obrazów.</span><span class="sxs-lookup"><span data-stu-id="eb43e-174">hello sign-in credentials, specified in hello application manifest, are used toospecify hello sign-in information, or SSH key, for downloading hello container image from hello image repository.</span></span> <span data-ttu-id="eb43e-175">Witaj poniższy przykład przedstawia konta o nazwie *TestUser* wraz z hello hasła w postaci zwykłego tekstu (*nie* zalecana):</span><span class="sxs-lookup"><span data-stu-id="eb43e-175">hello following example shows an account called *TestUser* along with hello password in clear text (*not* recommended):</span></span>

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

<span data-ttu-id="eb43e-176">Firma Microsoft zaleca szyfrowania hello hasła przy użyciu certyfikatu, który został wdrożony toohello maszyny.</span><span class="sxs-lookup"><span data-stu-id="eb43e-176">We recommend that you encrypt hello password by using a certificate that's deployed toohello machine.</span></span>

<span data-ttu-id="eb43e-177">Witaj poniższy przykład przedstawia konta o nazwie *TestUser*, gdzie hasło hello została zaszyfrowana przy użyciu certyfikatu o nazwie *MyCert*.</span><span class="sxs-lookup"><span data-stu-id="eb43e-177">hello following example shows an account called *TestUser*, where hello password was encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="eb43e-178">Można użyć hello `Invoke-ServiceFabricEncryptText` tekst toocreate polecenia programu PowerShell tajny szyfrowania hello hello hasła.</span><span class="sxs-lookup"><span data-stu-id="eb43e-178">You can use hello `Invoke-ServiceFabricEncryptText` PowerShell command toocreate hello secret cipher text for hello password.</span></span> <span data-ttu-id="eb43e-179">Aby uzyskać więcej informacji, zobacz artykuł hello [Zarządzanie kluczy tajnych w aplikacji usługi Service Fabric](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="eb43e-179">For more information, see hello article [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md).</span></span>

<span data-ttu-id="eb43e-180">klucz prywatny Hello hello certyfikatu, który został użyty toodecrypt hello hasło musi być wdrożone toohello komputera lokalnego w metodzie poza pasmem.</span><span class="sxs-lookup"><span data-stu-id="eb43e-180">hello private key of hello certificate that's used toodecrypt hello password must be deployed toohello local machine in an out-of-band method.</span></span> <span data-ttu-id="eb43e-181">(Na platformie Azure, ta metoda jest usługi Azure Resource Manager). Następnie gdy usługa sieć szkieletowa wdraża hello usługi pakietu toohello maszyny, może odszyfrować klucza tajnego hello.</span><span class="sxs-lookup"><span data-stu-id="eb43e-181">(In Azure, this method is Azure Resource Manager.) Then, when Service Fabric deploys hello service package toohello machine, it can decrypt hello secret.</span></span> <span data-ttu-id="eb43e-182">Przy użyciu klucza tajnego hello wraz z nazwą konta hello, następnie uwierzytelniania hello kontenera repozytorium.</span><span class="sxs-lookup"><span data-stu-id="eb43e-182">By using hello secret along with hello account name, it can then authenticate with hello container repository.</span></span>

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

## <span data-ttu-id="eb43e-183"><a name ="Portsection"></a>Skonfiguruj mapowanie portów toohost kontenera</span><span class="sxs-lookup"><span data-stu-id="eb43e-183"><a name ="Portsection"></a> Configure container toohost port mapping</span></span>
<span data-ttu-id="eb43e-184">Można skonfigurować toocommunicate port używany host hello kontenera, określając `PortBinding` w manifeście aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="eb43e-184">You can configure a host port used toocommunicate with hello container by specifying a `PortBinding` in hello application manifest.</span></span> <span data-ttu-id="eb43e-185">wewnątrz hello kontenera tooa portu na hoście hello nasłuchuje Hello portu powiązania mapy hello portu toowhich hello usługa.</span><span class="sxs-lookup"><span data-stu-id="eb43e-185">hello port binding maps hello port toowhich hello service is listening inside hello container tooa port on hello host.</span></span>

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

## <a name="configure-container-to-container-discovery-and-communication"></a><span data-ttu-id="eb43e-186">Konfigurowanie odnajdywania kontenera do kontenera i komunikacji</span><span class="sxs-lookup"><span data-stu-id="eb43e-186">Configure container-to-container discovery and communication</span></span>
<span data-ttu-id="eb43e-187">Można użyć hello `PortBinding` toomap elementu punktu końcowego tooan port kontenera w hello manifestu usługi.</span><span class="sxs-lookup"><span data-stu-id="eb43e-187">You can use hello `PortBinding` element toomap a container port tooan endpoint in hello service manifest.</span></span> <span data-ttu-id="eb43e-188">W hello poniższy przykład, hello punktu końcowego `Endpoint1` określa 8905 stałego portu.</span><span class="sxs-lookup"><span data-stu-id="eb43e-188">In hello following example, hello endpoint `Endpoint1` specifies a fixed port, 8905.</span></span> <span data-ttu-id="eb43e-189">Może również określać nie portu, w tym przypadku losowego portu z zakresu portów aplikacji hello klastra jest wybierany dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="eb43e-189">It can also specify no port at all, in which case a random port from hello cluster's application port range is chosen for you.</span></span>


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
<span data-ttu-id="eb43e-190">Jeśli określisz punkt końcowy, za pomocą hello `Endpoint` tag w manifeście usługi hello kontenera gościa, Service Fabric automatycznie opublikować toohello tego punktu końcowego usługi nazw.</span><span class="sxs-lookup"><span data-stu-id="eb43e-190">If you specify an endpoint, using hello `Endpoint` tag in hello service manifest of a guest container, Service Fabric can automatically publish this endpoint toohello Naming service.</span></span> <span data-ttu-id="eb43e-191">Inne usługi, które są uruchomione w klastrze hello w związku z tym można odnaleźć tego kontenera za pomocą zapytań REST hello w celu rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="eb43e-191">Other services that are running in hello cluster can thus discover this container using hello REST queries for resolving.</span></span>

<span data-ttu-id="eb43e-192">Zarejestrowani hello Naming service, można wykonać kontenera do kontenera komunikacji z kontenera za pomocą hello [odwrotny serwer proxy](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="eb43e-192">By registering with hello Naming service, you can perform container-to-container communication within your container by using hello [reverse proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="eb43e-193">Komunikacja odbywa się przez podanie port nasłuchujący hello zwrotny serwer proxy http i nazwa hello hello usług, które ma być toocommunicate ze zmiennych środowiskowych.</span><span class="sxs-lookup"><span data-stu-id="eb43e-193">Communication is performed by providing hello reverse proxy http listening port and hello name of hello services that you want toocommunicate with as environment variables.</span></span> <span data-ttu-id="eb43e-194">Aby uzyskać więcej informacji zobacz następną sekcję hello.</span><span class="sxs-lookup"><span data-stu-id="eb43e-194">For more information, see hello next section.</span></span> 

## <a name="configure-and-set-environment-variables"></a><span data-ttu-id="eb43e-195">Konfigurowanie i ustawianie zmiennych środowiskowych</span><span class="sxs-lookup"><span data-stu-id="eb43e-195">Configure and set environment variables</span></span>
<span data-ttu-id="eb43e-196">Zmienne środowiskowe można określić dla każdego pakietu kodu w hello manifestu usługi.</span><span class="sxs-lookup"><span data-stu-id="eb43e-196">Environment variables can be specified for each code package in hello service manifest.</span></span> <span data-ttu-id="eb43e-197">Ta funkcja jest dostępna dla wszystkich usług niezależnie od tego, czy są one wdrażane jako kontenery, procesy, czy pliki wykonywalne gościa.</span><span class="sxs-lookup"><span data-stu-id="eb43e-197">This feature is available for all services irrespective of whether they are deployed as containers or processes or guest executables.</span></span> <span data-ttu-id="eb43e-198">Można zastąpić zmiennej środowiskowej wartości w aplikacji hello manifestu lub określić ich podczas wdrażania jako parametry aplikacji.</span><span class="sxs-lookup"><span data-stu-id="eb43e-198">You can override environment variable values in hello application manifest or specify them during deployment as application parameters.</span></span>

<span data-ttu-id="eb43e-199">Witaj poniższy fragment XML manifestu usługi przedstawia przykładowy sposób zmiennych środowiskowych toospecify pakietu kodu:</span><span class="sxs-lookup"><span data-stu-id="eb43e-199">hello following service manifest XML snippet shows an example of how toospecify environment variables for a code package:</span></span>

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

<span data-ttu-id="eb43e-200">Te zmienne środowiskowe umożliwić przesłanianie go na poziomie manifestu aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="eb43e-200">These environment variables can be overridden at hello application manifest level:</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

<span data-ttu-id="eb43e-201">W poprzednim przykładzie hello, możemy określić jawną wartość dla hello `HttpGateway` zmiennej środowiskowej (19000), gdy firma Microsoft ustaw wartość hello `BackendServiceName` parametr za pomocą hello `[BackendSvc]` parametr aplikacji.</span><span class="sxs-lookup"><span data-stu-id="eb43e-201">In hello previous example, we specified an explicit value for hello `HttpGateway` environment variable (19000), while we set hello value for `BackendServiceName` parameter via hello `[BackendSvc]` application parameter.</span></span> <span data-ttu-id="eb43e-202">Te ustawienia umożliwiają wartość hello toospecify `BackendServiceName`wartość wdrażania aplikacji hello i ma wartość stałą w manifeście hello.</span><span class="sxs-lookup"><span data-stu-id="eb43e-202">These settings enable you toospecify hello value for `BackendServiceName`value when you deploy hello application and not have a fixed value in hello manifest.</span></span>

## <a name="configure-isolation-mode"></a><span data-ttu-id="eb43e-203">Konfigurowanie trybu izolacji</span><span class="sxs-lookup"><span data-stu-id="eb43e-203">Configure isolation mode</span></span>

<span data-ttu-id="eb43e-204">System Windows obsługuje dwa tryby izolacji dla kontenerów - procesu oraz funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="eb43e-204">Windows supports two isolation modes for containers - process and Hyper-V.</span></span>  <span data-ttu-id="eb43e-205">W trybie izolacji procesu hello wszystkich kontenerów hello systemem hello tego samego hosta maszyny udziału hello jądra z hostem hello.</span><span class="sxs-lookup"><span data-stu-id="eb43e-205">With hello process isolation mode, all hello containers running on hello same host machine share hello kernel with hello host.</span></span> <span data-ttu-id="eb43e-206">W trybie izolacji hello funkcji Hyper-V między każdego kontenera funkcji Hyper-V a hostem kontenera hello odizolowanych hello jądra.</span><span class="sxs-lookup"><span data-stu-id="eb43e-206">With hello Hyper-V isolation mode, hello kernels are isolated between each Hyper-V container and hello container host.</span></span> <span data-ttu-id="eb43e-207">Tryb izolacji Hello jest określony w hello `ContainerHostPolicies` znacznika w pliku manifestu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="eb43e-207">hello isolation mode is specified in hello `ContainerHostPolicies` tag in hello application manifest file.</span></span>  <span data-ttu-id="eb43e-208">Tryby izolacji Hello, które można określić są `process`, `hyperv`, i `default`.</span><span class="sxs-lookup"><span data-stu-id="eb43e-208">hello isolation modes that can be specified are `process`, `hyperv`, and `default`.</span></span> <span data-ttu-id="eb43e-209">Witaj `default` trybu izolacji domyślnie przyjmowana jest zbyt`process` w systemie Windows Server obsługuje i domyślnie przyjmowana jest zbyt`hyperv` na hostach z systemem Windows 10.</span><span class="sxs-lookup"><span data-stu-id="eb43e-209">hello `default` isolation mode defaults too`process` on Windows Server hosts, and defaults too`hyperv` on Windows 10 hosts.</span></span>  <span data-ttu-id="eb43e-210">Hello poniższy fragment kodu przedstawia sposób hello trybu izolacji została określona w pliku manifestu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="eb43e-210">hello following snippet shows how hello isolation mode is specified in hello application manifest file.</span></span>

```xml
   <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="hyperv">
```


## <a name="complete-examples-for-application-and-service-manifest"></a><span data-ttu-id="eb43e-211">Zakończenie przykłady aplikacji i manifest usługi</span><span class="sxs-lookup"><span data-stu-id="eb43e-211">Complete examples for application and service manifest</span></span>

<span data-ttu-id="eb43e-212">Następujący przykład manifestu aplikacji:</span><span class="sxs-lookup"><span data-stu-id="eb43e-212">An example application manifest follows:</span></span>

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

<span data-ttu-id="eb43e-213">Następujący przykład manifestu usługi (określone w powyższej manifest aplikacji hello):</span><span class="sxs-lookup"><span data-stu-id="eb43e-213">An example service manifest (specified in hello preceding application manifest) follows:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="eb43e-214">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="eb43e-214">Next steps</span></span>
<span data-ttu-id="eb43e-215">Po wdrożeniu usługi konteneryzowanych, Dowiedz się, jak toomanage cykl życia, odczytując [cyklem życia aplikacji usługi sieć szkieletowa](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="eb43e-215">Now that you have deployed a containerized service, learn how toomanage its lifecycle by reading [Service Fabric application lifecycle](service-fabric-application-lifecycle.md).</span></span>

* [<span data-ttu-id="eb43e-216">Omówienie sieci szkieletowej usług i kontenerów</span><span class="sxs-lookup"><span data-stu-id="eb43e-216">Overview of Service Fabric and containers</span></span>](service-fabric-containers-overview.md)
* <span data-ttu-id="eb43e-217">Na przykład wyewidencjonowania [przykłady kodu kontenera sieci szkieletowej usług w witrynie GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span><span class="sxs-lookup"><span data-stu-id="eb43e-217">For an example, checkout [Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>
