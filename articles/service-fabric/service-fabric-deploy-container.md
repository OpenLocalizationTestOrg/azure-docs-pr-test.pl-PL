---
title: "Sieć szkieletowa usług i wdrażanie kontenerów | Dokumentacja firmy Microsoft"
description: "Sieć szkieletowa usług i korzystanie z kontenerów do wdrażania aplikacji mikrousługi. W tym artykule opisano możliwości, które zapewnia sieć szkieletowa usług dla kontenerów i sposobu wdrażania obrazu systemu Windows kontenera w klastrze."
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
ms.openlocfilehash: 25d6b056421e71fa70ed20a39589f77dbbc25c69
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-windows-container-to-service-fabric"></a><span data-ttu-id="11253-104">Wdrażanie kontenera systemu Windows w sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="11253-104">Deploy a Windows container to Service Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="11253-105">Wdrażanie kontenera systemu Windows</span><span class="sxs-lookup"><span data-stu-id="11253-105">Deploy Windows Container</span></span>](service-fabric-deploy-container.md)
> * [<span data-ttu-id="11253-106">Wdrażanie kontenera Docker</span><span class="sxs-lookup"><span data-stu-id="11253-106">Deploy Docker Container</span></span>](service-fabric-deploy-container-linux.md)
> 
> 

<span data-ttu-id="11253-107">Ten artykuł przeprowadzi Cię przez proces tworzenia konteneryzowanych usług w kontenerach systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="11253-107">This article walks you through the process of building containerized services in Windows containers.</span></span>

<span data-ttu-id="11253-108">Sieć szkieletowa usług ma kilka możliwości, które zapewniają pomoc podczas tworzenia aplikacji, które składają się z mikrousług uruchomiony kontenerów.</span><span class="sxs-lookup"><span data-stu-id="11253-108">Service Fabric has several capabilities that help you with building applications that are composed of microservices running inside containers.</span></span> 

<span data-ttu-id="11253-109">Funkcje obejmują:</span><span class="sxs-lookup"><span data-stu-id="11253-109">The capabilities include:</span></span>

* <span data-ttu-id="11253-110">Kontener obrazu wdrożenia i aktywacji</span><span class="sxs-lookup"><span data-stu-id="11253-110">Container image deployment and activation</span></span>
* <span data-ttu-id="11253-111">Zarządzanie zasobów</span><span class="sxs-lookup"><span data-stu-id="11253-111">Resource governance</span></span>
* <span data-ttu-id="11253-112">Repozytorium uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="11253-112">Repository authentication</span></span>
* <span data-ttu-id="11253-113">Mapowanie portów port kontenera do hosta</span><span class="sxs-lookup"><span data-stu-id="11253-113">Container port-to-host port mapping</span></span>
* <span data-ttu-id="11253-114">Odnajdywanie kontenera do kontenera i komunikacji</span><span class="sxs-lookup"><span data-stu-id="11253-114">Container-to-container discovery and communication</span></span>
* <span data-ttu-id="11253-115">Możliwość konfigurowania i ustaw zmienne środowiskowe</span><span class="sxs-lookup"><span data-stu-id="11253-115">Ability to configure and set environment variables</span></span>

<span data-ttu-id="11253-116">Oto jak działa każdy z możliwości podczas pakowane konteneryzowanych usługi do uwzględnienia w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="11253-116">Let's look at how each of capabilities works when you're packaging a containerized service to be included in your application.</span></span>

## <a name="package-a-windows-container"></a><span data-ttu-id="11253-117">Pakiet kontenera systemu Windows</span><span class="sxs-lookup"><span data-stu-id="11253-117">Package a Windows container</span></span>
<span data-ttu-id="11253-118">Podczas pakowania kontener, można użyć albo szablon projektu Visual Studio lub [ręcznie utworzyć pakiet aplikacji](#manually).</span><span class="sxs-lookup"><span data-stu-id="11253-118">When you package a container, you can choose to use either a Visual Studio project template or [create the application package manually](#manually).</span></span>  <span data-ttu-id="11253-119">Korzystając z programu Visual Studio, struktura pakietu aplikacji i pliki manifestu są tworzone przez szablon nowego projektu dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="11253-119">When you use Visual Studio, the application package structure and manifest files are created by the New Project template for you.</span></span>

> [!TIP]
> <span data-ttu-id="11253-120">Najprostszym sposobem pakietu istniejącego obrazu kontenera do usługi jest używać programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="11253-120">The easiest way to package an existing container image into a service is to use Visual Studio.</span></span>

## <a name="use-visual-studio-to-package-an-existing-container-image"></a><span data-ttu-id="11253-121">Pakiet istniejącego obrazu kontenera za pomocą programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="11253-121">Use Visual Studio to package an existing container image</span></span>
<span data-ttu-id="11253-122">Program Visual Studio udostępnia szablonu usługi Service Fabric ułatwiają wdrażanie kontenera do klastra usługi sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="11253-122">Visual Studio provides a Service Fabric service template to help you deploy a container to a Service Fabric cluster.</span></span>

1. <span data-ttu-id="11253-123">Wybierz **pliku** > **nowy projekt**i tworzenie aplikacji sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="11253-123">Choose **File** > **New Project**, and create a Service Fabric application.</span></span>
2. <span data-ttu-id="11253-124">Wybierz **kontenera gościa** jako szablonu usługi.</span><span class="sxs-lookup"><span data-stu-id="11253-124">Choose **Guest Container** as the service template.</span></span>
3. <span data-ttu-id="11253-125">Wybierz **nazwa obrazu** i podaj ścieżkę do obrazu w repozytorium kontenera.</span><span class="sxs-lookup"><span data-stu-id="11253-125">Choose **Image Name** and provide the path to the image in your container repository.</span></span> <span data-ttu-id="11253-126">Na przykład `myrepo/myimage:v1` w https://hub.docker.com</span><span class="sxs-lookup"><span data-stu-id="11253-126">For example, `myrepo/myimage:v1` in https://hub.docker.com</span></span>
4. <span data-ttu-id="11253-127">Nadaj nazwę usłudze i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="11253-127">Give your service a name, and click **OK**.</span></span>
5. <span data-ttu-id="11253-128">Jeśli usługa konteneryzowanych musi punkt końcowy komunikacji, protokół, port i typ można teraz dodać do pliku ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="11253-128">If your containerized service needs an endpoint for communication, you can now add the protocol, port, and type to the ServiceManifest.xml file.</span></span> <span data-ttu-id="11253-129">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="11253-129">For example:</span></span> 
     
    `<Endpoint Name="MyContainerServiceEndpoint" Protocol="http" Port="80" UriScheme="http" PathSuffix="myapp/" Type="Input" />`
    
    <span data-ttu-id="11253-130">Zapewniając `UriScheme`, automatycznie rejestruje punkt końcowy kontenera nazewnictwa w usłudze odnajdywania w sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="11253-130">By providing the `UriScheme`, Service Fabric automatically registers the container endpoint with the Naming service for discoverability.</span></span> <span data-ttu-id="11253-131">Port można stałej (jak pokazano w poprzednim przykładzie) lub dynamicznie przydzielane.</span><span class="sxs-lookup"><span data-stu-id="11253-131">The port can either be fixed (as shown in the preceding example) or dynamically allocated.</span></span> <span data-ttu-id="11253-132">Jeśli nie określisz port dynamicznie nadawany z zakresu aplikacji (co się stanie z dowolnej usługi).</span><span class="sxs-lookup"><span data-stu-id="11253-132">If you don't specify a port, it is dynamically allocated from the application port range (as would happen with any service).</span></span>
    <span data-ttu-id="11253-133">Należy również skonfigurować kontener, aby mapowanie portów hosta, określając `PortBinding` zasad w manifeście aplikacji.</span><span class="sxs-lookup"><span data-stu-id="11253-133">You also need to configure the container to host port mapping by specifying a `PortBinding` policy in the application manifest.</span></span> <span data-ttu-id="11253-134">Aby uzyskać więcej informacji, zobacz [kontenera konfiguracji do mapowania port hosta](#Portsection).</span><span class="sxs-lookup"><span data-stu-id="11253-134">For more information, see [Configure container to host port mapping](#Portsection).</span></span>
6. <span data-ttu-id="11253-135">Jeśli z kontenera musi ładu zasobów, a następnie dodaj `ResourceGovernancePolicy`.</span><span class="sxs-lookup"><span data-stu-id="11253-135">If your container needs resource governance then add a `ResourceGovernancePolicy`.</span></span>
8. <span data-ttu-id="11253-136">Jeśli kontener wymaga uwierzytelniania w prywatnym repozytorium, dodaj parametr `RepositoryCredentials`.</span><span class="sxs-lookup"><span data-stu-id="11253-136">If your container needs to authenticate with a private repository, then add `RepositoryCredentials`.</span></span>
7. <span data-ttu-id="11253-137">Jeśli są uruchomione na komputerze z systemem Windows Server 2016, z włączoną obsługą kontenera, można za pomocą pakietu i opublikować akcji do wdrożenia na lokalny klaster.</span><span class="sxs-lookup"><span data-stu-id="11253-137">If you are running on a Windows Server 2016 machine with container support enabled, you can use the package and publish action to deploy to your local cluster.</span></span> 
8. <span data-ttu-id="11253-138">Po wykonaniu tych czynności możesz opublikować aplikację do zdalnego klastra lub zaewidencjonować rozwiązanie do kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="11253-138">When ready, you can publish the application to a remote cluster or check in the solution to source control.</span></span> 

<span data-ttu-id="11253-139">Na przykład wyewidencjonowania [przykłady kodu kontenera sieci szkieletowej usług w witrynie GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span><span class="sxs-lookup"><span data-stu-id="11253-139">For an example, checkout the [Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>

## <a name="creating-a-windows-server-2016-cluster"></a><span data-ttu-id="11253-140">Tworzenie klastra z systemem Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="11253-140">Creating a Windows Server 2016 cluster</span></span>
<span data-ttu-id="11253-141">Aby wdrożyć aplikację konteneryzowanych, musisz utworzyć klastra z systemem Windows Server 2016 z włączoną obsługą usługi kontenera.</span><span class="sxs-lookup"><span data-stu-id="11253-141">To deploy your containerized application, you need to create a cluster running Windows Server 2016 with container support enabled.</span></span> <span data-ttu-id="11253-142">Klaster może działać lokalnie lub wdrożone za pośrednictwem usługi Azure Resource Manager na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="11253-142">Your cluster may be running locally, or deployed via Azure Resource Manager in Azure.</span></span> 

<span data-ttu-id="11253-143">Aby wdrożyć klaster za pomocą usługi Azure Resource Manager, wybierz **systemu Windows Server 2016 z kontenerami** obrazu opcji na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="11253-143">To deploy a cluster using Azure Resource Manager, choose the **Windows Server 2016 with Containers** image option in Azure.</span></span> <span data-ttu-id="11253-144">Zapoznaj się z artykułem [tworzenia klastra usługi sieć szkieletowa usług za pomocą usługi Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="11253-144">See the article [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="11253-145">Upewnij się, że używasz następujące ustawienia usługi Azure Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="11253-145">Ensure that you use the following Azure Resource Manager settings:</span></span>

```xml
"vmImageOffer": { "type": "string","defaultValue": "WindowsServer"     },
"vmImageSku": { "defaultValue": "2016-Datacenter-with-Containers","type": "string"     },
"vmImageVersion": { "defaultValue": "latest","type": "string"     },  
```
<span data-ttu-id="11253-146">Można również użyć [szablonu pięć węzłów usługi Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) do utworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="11253-146">You can also use the [Five Node Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) to create a cluster.</span></span> <span data-ttu-id="11253-147">Można również odczytać społeczność [wpis w blogu](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html) przy użyciu kontenerów sieci szkieletowej usług i systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="11253-147">Alternatively read a community [blog post](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html) on using Service Fabric and Windows containers.</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a><span data-ttu-id="11253-148">Ręcznie pakietów i wdrożyć obraz kontenera</span><span class="sxs-lookup"><span data-stu-id="11253-148">Manually package and deploy a container image</span></span>
<span data-ttu-id="11253-149">Proces ręcznie pakowania konteneryzowanych usługa jest oparta na następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="11253-149">The process of manually packaging a containerized service is based on the following steps:</span></span>

1. <span data-ttu-id="11253-150">Opublikuj kontenerów do repozytorium.</span><span class="sxs-lookup"><span data-stu-id="11253-150">Publish the containers to your repository.</span></span>
2. <span data-ttu-id="11253-151">Utwórz strukturę katalogu pakietu.</span><span class="sxs-lookup"><span data-stu-id="11253-151">Create the package directory structure.</span></span>
3. <span data-ttu-id="11253-152">Edytuj plik manifestu usługi.</span><span class="sxs-lookup"><span data-stu-id="11253-152">Edit the service manifest file.</span></span>
4. <span data-ttu-id="11253-153">Przeprowadź edycję pliku manifestu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="11253-153">Edit the application manifest file.</span></span>

## <a name="deploy-and-activate-a-container-image"></a><span data-ttu-id="11253-154">Wdrażanie i aktywować obrazu kontenera</span><span class="sxs-lookup"><span data-stu-id="11253-154">Deploy and activate a container image</span></span>
<span data-ttu-id="11253-155">W sieci szkieletowej usług [model aplikacji](service-fabric-application-model.md), kontener reprezentuje hosta aplikacji, w których wiele usługi repliki są umieszczane.</span><span class="sxs-lookup"><span data-stu-id="11253-155">In the Service Fabric [application model](service-fabric-application-model.md), a container represents an application host in which multiple service replicas are placed.</span></span> <span data-ttu-id="11253-156">Aby wdrożyć i aktywować kontener, put nazwa obrazu kontenera do `ContainerHost` element manifestu usługi.</span><span class="sxs-lookup"><span data-stu-id="11253-156">To deploy and activate a container, put the name of the container image into a `ContainerHost` element in the service manifest.</span></span>

<span data-ttu-id="11253-157">W manifeście usługi, dodać `ContainerHost` dla punktu wejścia.</span><span class="sxs-lookup"><span data-stu-id="11253-157">In the service manifest, add a `ContainerHost` for the entry point.</span></span> <span data-ttu-id="11253-158">Następnie ustaw `ImageName` nazwę kontenera repozytorium i obrazów.</span><span class="sxs-lookup"><span data-stu-id="11253-158">Then set the `ImageName` to be the name of the container repository and image.</span></span> <span data-ttu-id="11253-159">Manifest częściowe następujące przedstawiono przykład sposobu wdrażania kontenera o nazwie `myimage:v1` z repozytorium o nazwie `myrepo`:</span><span class="sxs-lookup"><span data-stu-id="11253-159">The following partial manifest shows an example of how to deploy the container called `myimage:v1` from a repository called `myrepo`:</span></span>

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

<span data-ttu-id="11253-160">Można określić opcjonalne polecenia do uruchomienia po rozpoczęciu kontenera w obszarze `Commands` elementu.</span><span class="sxs-lookup"><span data-stu-id="11253-160">You can specify optional commands to run upon starting the container under the `Commands` element.</span></span> <span data-ttu-id="11253-161">Dla wielu poleceń przecinkami ograniczyć ich.</span><span class="sxs-lookup"><span data-stu-id="11253-161">For multiple commands, comma-delimit them.</span></span> 

## <a name="understand-resource-governance"></a><span data-ttu-id="11253-162">Zrozumienie ładu zasobów</span><span class="sxs-lookup"><span data-stu-id="11253-162">Understand resource governance</span></span>
<span data-ttu-id="11253-163">Ładu zasobów jest możliwość kontenera, który ogranicza zasobów korzystających przez kontener na hoście.</span><span class="sxs-lookup"><span data-stu-id="11253-163">Resource governance is a capability of the container that restricts the resources that the container can use on the host.</span></span> <span data-ttu-id="11253-164">`ResourceGovernancePolicy`, Który został określony w manifeście aplikacji służy do deklarowania limity zasobów pakietu kodu usługi.</span><span class="sxs-lookup"><span data-stu-id="11253-164">The `ResourceGovernancePolicy`, which is specified in the application manifest is used to declare resource limits for a service code package.</span></span> <span data-ttu-id="11253-165">Limity zasobów można ustawić dla następujących zasobów:</span><span class="sxs-lookup"><span data-stu-id="11253-165">Resource limits can be set for the following resources:</span></span>

* <span data-ttu-id="11253-166">Memory (Pamięć)</span><span class="sxs-lookup"><span data-stu-id="11253-166">Memory</span></span>
* <span data-ttu-id="11253-167">MemorySwap</span><span class="sxs-lookup"><span data-stu-id="11253-167">MemorySwap</span></span>
* <span data-ttu-id="11253-168">CpuShares (względną wagę procesora CPU)</span><span class="sxs-lookup"><span data-stu-id="11253-168">CpuShares (CPU relative weight)</span></span>
* <span data-ttu-id="11253-169">MemoryReservationInMB</span><span class="sxs-lookup"><span data-stu-id="11253-169">MemoryReservationInMB</span></span>  
* <span data-ttu-id="11253-170">BlkioWeight (BlockIO względną wagę).</span><span class="sxs-lookup"><span data-stu-id="11253-170">BlkioWeight (BlockIO relative weight).</span></span>

> [!NOTE]
> <span data-ttu-id="11253-171">Obsługa służącą do określonego bloku limity we/wy, takie jak IOPs, odczytu/zapisu liczby bitów na Sekundę i inne osoby, które są planowane w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="11253-171">Support for specifying specific block IO limits such as IOPs, read/write BPS, and others are planned for a future release.</span></span>
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

## <a name="authenticate-a-repository"></a><span data-ttu-id="11253-172">Uwierzytelnianie repozytorium</span><span class="sxs-lookup"><span data-stu-id="11253-172">Authenticate a repository</span></span>
<span data-ttu-id="11253-173">Aby pobrać kontener, może być konieczne podanie poświadczeń logowania do repozytorium kontenera.</span><span class="sxs-lookup"><span data-stu-id="11253-173">To download a container, you might have to provide sign-in credentials to the container repository.</span></span> <span data-ttu-id="11253-174">Poświadczenia logowania, określona w manifeście aplikacji są używane do określenia informacji logowania lub klucza SSH do pobierania obrazu kontenera z repozytorium obrazów.</span><span class="sxs-lookup"><span data-stu-id="11253-174">The sign-in credentials, specified in the application manifest, are used to specify the sign-in information, or SSH key, for downloading the container image from the image repository.</span></span> <span data-ttu-id="11253-175">W poniższym przykładzie przedstawiono konta o nazwie *TestUser* wraz z hasła w postaci zwykłego tekstu (*nie* zalecana):</span><span class="sxs-lookup"><span data-stu-id="11253-175">The following example shows an account called *TestUser* along with the password in clear text (*not* recommended):</span></span>

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

<span data-ttu-id="11253-176">Firma Microsoft zaleca szyfrowania hasła przy użyciu certyfikatu, które zostały wdrożone na maszynie.</span><span class="sxs-lookup"><span data-stu-id="11253-176">We recommend that you encrypt the password by using a certificate that's deployed to the machine.</span></span>

<span data-ttu-id="11253-177">W poniższym przykładzie przedstawiono konta o nazwie *TestUser*, gdzie hasło została zaszyfrowana przy użyciu certyfikatu o nazwie *MyCert*.</span><span class="sxs-lookup"><span data-stu-id="11253-177">The following example shows an account called *TestUser*, where the password was encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="11253-178">Można użyć `Invoke-ServiceFabricEncryptText` polecenie programu PowerShell, aby utworzyć tekst tajny szyfrowania hasła.</span><span class="sxs-lookup"><span data-stu-id="11253-178">You can use the `Invoke-ServiceFabricEncryptText` PowerShell command to create the secret cipher text for the password.</span></span> <span data-ttu-id="11253-179">Aby uzyskać więcej informacji, zobacz artykuł [Zarządzanie kluczy tajnych w aplikacji usługi Service Fabric](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="11253-179">For more information, see the article [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md).</span></span>

<span data-ttu-id="11253-180">Klucz prywatny certyfikatu, który jest używany do odszyfrowywania hasła należy wdrożyć na komputerze lokalnym w metodzie poza pasmem.</span><span class="sxs-lookup"><span data-stu-id="11253-180">The private key of the certificate that's used to decrypt the password must be deployed to the local machine in an out-of-band method.</span></span> <span data-ttu-id="11253-181">(Na platformie Azure, ta metoda jest usługi Azure Resource Manager). Następnie gdy sieć szkieletowa usług wdraża pakiet usługi do komputera, może odszyfrować klucza tajnego.</span><span class="sxs-lookup"><span data-stu-id="11253-181">(In Azure, this method is Azure Resource Manager.) Then, when Service Fabric deploys the service package to the machine, it can decrypt the secret.</span></span> <span data-ttu-id="11253-182">Przy użyciu klucza tajnego wraz z nazwą konta, następnie uwierzytelniania z repozytorium kontenera.</span><span class="sxs-lookup"><span data-stu-id="11253-182">By using the secret along with the account name, it can then authenticate with the container repository.</span></span>

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

## <span data-ttu-id="11253-183"><a name ="Portsection"></a>Skonfiguruj kontener, aby mapowanie portów hosta</span><span class="sxs-lookup"><span data-stu-id="11253-183"><a name ="Portsection"></a> Configure container to host port mapping</span></span>
<span data-ttu-id="11253-184">Można skonfigurować port hosta używany do komunikacji z kontenerem, określając `PortBinding` w manifeście aplikacji.</span><span class="sxs-lookup"><span data-stu-id="11253-184">You can configure a host port used to communicate with the container by specifying a `PortBinding` in the application manifest.</span></span> <span data-ttu-id="11253-185">Powiązanie portu mapy numer portu, z którym nasłuchuje usługa wewnątrz kontenera do portu na hoście.</span><span class="sxs-lookup"><span data-stu-id="11253-185">The port binding maps the port to which the service is listening inside the container to a port on the host.</span></span>

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

## <a name="configure-container-to-container-discovery-and-communication"></a><span data-ttu-id="11253-186">Konfigurowanie odnajdywania kontenera do kontenera i komunikacji</span><span class="sxs-lookup"><span data-stu-id="11253-186">Configure container-to-container discovery and communication</span></span>
<span data-ttu-id="11253-187">Można użyć `PortBinding` elementu, aby mapować port kontenera do punktu końcowego w manifeście usługi.</span><span class="sxs-lookup"><span data-stu-id="11253-187">You can use the `PortBinding` element to map a container port to an endpoint in the service manifest.</span></span> <span data-ttu-id="11253-188">W poniższym przykładzie punktu końcowego `Endpoint1` określa 8905 stałego portu.</span><span class="sxs-lookup"><span data-stu-id="11253-188">In the following example, the endpoint `Endpoint1` specifies a fixed port, 8905.</span></span> <span data-ttu-id="11253-189">Może również określać żadnego portu, w takim przypadku losowego portu z zakresu portów aplikacji klastra jest wybierany dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="11253-189">It can also specify no port at all, in which case a random port from the cluster's application port range is chosen for you.</span></span>


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
<span data-ttu-id="11253-190">Jeśli określisz punkt końcowy, za pomocą `Endpoint` tag w manifeście usługi kontenera gościa, Service Fabric automatycznie opublikować ten punkt końcowy usługi nazw.</span><span class="sxs-lookup"><span data-stu-id="11253-190">If you specify an endpoint, using the `Endpoint` tag in the service manifest of a guest container, Service Fabric can automatically publish this endpoint to the Naming service.</span></span> <span data-ttu-id="11253-191">Inne usługi, które są uruchomione w klastrze w związku z tym umożliwia odnalezienie tego kontenera za pomocą zapytań REST dla rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="11253-191">Other services that are running in the cluster can thus discover this container using the REST queries for resolving.</span></span>

<span data-ttu-id="11253-192">Rejestrując z usługą Naming mogą wykonywać kontenera do kontenera komunikacji z kontenera za pomocą [odwrotny serwer proxy](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="11253-192">By registering with the Naming service, you can perform container-to-container communication within your container by using the [reverse proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="11253-193">Komunikacja odbywa się przez podanie port nasłuchiwania zwrotny serwer proxy http i nazwę usługi, która ma do komunikowania się z jako zmienne środowiskowe.</span><span class="sxs-lookup"><span data-stu-id="11253-193">Communication is performed by providing the reverse proxy http listening port and the name of the services that you want to communicate with as environment variables.</span></span> <span data-ttu-id="11253-194">Aby uzyskać więcej informacji zobacz następną sekcję.</span><span class="sxs-lookup"><span data-stu-id="11253-194">For more information, see the next section.</span></span> 

## <a name="configure-and-set-environment-variables"></a><span data-ttu-id="11253-195">Konfigurowanie i ustawianie zmiennych środowiskowych</span><span class="sxs-lookup"><span data-stu-id="11253-195">Configure and set environment variables</span></span>
<span data-ttu-id="11253-196">Zmienne środowiskowe można określić dla każdego pakietu kodu w manifeście usługi.</span><span class="sxs-lookup"><span data-stu-id="11253-196">Environment variables can be specified for each code package in the service manifest.</span></span> <span data-ttu-id="11253-197">Ta funkcja jest dostępna dla wszystkich usług niezależnie od tego, czy są one wdrażane jako kontenery, procesy, czy pliki wykonywalne gościa.</span><span class="sxs-lookup"><span data-stu-id="11253-197">This feature is available for all services irrespective of whether they are deployed as containers or processes or guest executables.</span></span> <span data-ttu-id="11253-198">Wartości zmiennych środowiskowych można przesłonić w manifeście aplikacji lub podać je podczas wdrażania jako parametry aplikacji.</span><span class="sxs-lookup"><span data-stu-id="11253-198">You can override environment variable values in the application manifest or specify them during deployment as application parameters.</span></span>

<span data-ttu-id="11253-199">Następujący fragment kodu XML manifestu usługi stanowi przykład sposobu określania zmiennych środowiskowych dla pakietu kodu:</span><span class="sxs-lookup"><span data-stu-id="11253-199">The following service manifest XML snippet shows an example of how to specify environment variables for a code package:</span></span>

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

<span data-ttu-id="11253-200">Te zmienne środowiskowe umożliwić przesłanianie go na poziomie manifestu aplikacji:</span><span class="sxs-lookup"><span data-stu-id="11253-200">These environment variables can be overridden at the application manifest level:</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

<span data-ttu-id="11253-201">W poprzednim przykładzie, możemy określić jawną wartość dla `HttpGateway` zmiennej środowiskowej (19000), gdy firma Microsoft ustaw wartość `BackendServiceName` parametr za pomocą `[BackendSvc]` parametr aplikacji.</span><span class="sxs-lookup"><span data-stu-id="11253-201">In the previous example, we specified an explicit value for the `HttpGateway` environment variable (19000), while we set the value for `BackendServiceName` parameter via the `[BackendSvc]` application parameter.</span></span> <span data-ttu-id="11253-202">Te ustawienia umożliwiają określenie wartości `BackendServiceName`wartość wdrażania aplikacji i nie ma wartości stałej w manifeście.</span><span class="sxs-lookup"><span data-stu-id="11253-202">These settings enable you to specify the value for `BackendServiceName`value when you deploy the application and not have a fixed value in the manifest.</span></span>

## <a name="configure-isolation-mode"></a><span data-ttu-id="11253-203">Konfigurowanie trybu izolacji</span><span class="sxs-lookup"><span data-stu-id="11253-203">Configure isolation mode</span></span>

<span data-ttu-id="11253-204">System Windows obsługuje dwa tryby izolacji dla kontenerów - procesu oraz funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="11253-204">Windows supports two isolation modes for containers - process and Hyper-V.</span></span>  <span data-ttu-id="11253-205">W trybie izolacji procesu wszystkie kontenery działające na tym samym hoście współdzielą jądro z hostem.</span><span class="sxs-lookup"><span data-stu-id="11253-205">With the process isolation mode, all the containers running on the same host machine share the kernel with the host.</span></span> <span data-ttu-id="11253-206">W trybie izolacji funkcji Hyper-V jądra są odizolowane dla każdego kontenera funkcji Hyper-V i hosta kontenera.</span><span class="sxs-lookup"><span data-stu-id="11253-206">With the Hyper-V isolation mode, the kernels are isolated between each Hyper-V container and the container host.</span></span> <span data-ttu-id="11253-207">W trybie izolacji określono `ContainerHostPolicies` znacznika w pliku manifestu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="11253-207">The isolation mode is specified in the `ContainerHostPolicies` tag in the application manifest file.</span></span>  <span data-ttu-id="11253-208">Tryby izolacji, które można określić, to `process`, `hyperv` i `default`.</span><span class="sxs-lookup"><span data-stu-id="11253-208">The isolation modes that can be specified are `process`, `hyperv`, and `default`.</span></span> <span data-ttu-id="11253-209">`default` Domyślnym trybem izolacji `process` na hostach z systemem Windows Server i wartość domyślna to `hyperv` na hostach z systemem Windows 10.</span><span class="sxs-lookup"><span data-stu-id="11253-209">The `default` isolation mode defaults to `process` on Windows Server hosts, and defaults to `hyperv` on Windows 10 hosts.</span></span>  <span data-ttu-id="11253-210">Poniższy fragment kodu przedstawia sposób określania trybu izolacji w pliku manifestu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="11253-210">The following snippet shows how the isolation mode is specified in the application manifest file.</span></span>

```xml
   <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="hyperv">
```


## <a name="complete-examples-for-application-and-service-manifest"></a><span data-ttu-id="11253-211">Zakończenie przykłady aplikacji i manifest usługi</span><span class="sxs-lookup"><span data-stu-id="11253-211">Complete examples for application and service manifest</span></span>

<span data-ttu-id="11253-212">Następujący przykład manifestu aplikacji:</span><span class="sxs-lookup"><span data-stu-id="11253-212">An example application manifest follows:</span></span>

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

<span data-ttu-id="11253-213">Następujący przykład manifestu usługi (określony w poprzednim manifest aplikacji):</span><span class="sxs-lookup"><span data-stu-id="11253-213">An example service manifest (specified in the preceding application manifest) follows:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="11253-214">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="11253-214">Next steps</span></span>
<span data-ttu-id="11253-215">Teraz, zostały wdrożone usługi konteneryzowanych, Dowiedz się, jak zarządzać jego cyklem odczytując [cyklem życia aplikacji usługi sieć szkieletowa](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="11253-215">Now that you have deployed a containerized service, learn how to manage its lifecycle by reading [Service Fabric application lifecycle](service-fabric-application-lifecycle.md).</span></span>

* [<span data-ttu-id="11253-216">Omówienie sieci szkieletowej usług i kontenerów</span><span class="sxs-lookup"><span data-stu-id="11253-216">Overview of Service Fabric and containers</span></span>](service-fabric-containers-overview.md)
* <span data-ttu-id="11253-217">Na przykład wyewidencjonowania [przykłady kodu kontenera sieci szkieletowej usług w witrynie GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span><span class="sxs-lookup"><span data-stu-id="11253-217">For an example, checkout [Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>
