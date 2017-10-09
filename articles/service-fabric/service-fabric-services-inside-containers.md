---
title: "aaaHow toocontainerize Twojego mikrousług sieć szkieletowa usług Azure (wersja zapoznawcza)"
description: "Sieć szkieletowa usług Azure został dodany nowy toocontainerize funkcji mikrousług Twojej sieci szkieletowej usług. Ta funkcja jest obecnie dostępna w wersji zapoznawczej."
services: service-fabric
documentationcenter: .net
author: anmolah
manager: anmolah
editor: anmolah
ms.assetid: 0b41efb3-4063-4600-89f5-b077ea81fa3a
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/04/2017
ms.author: anmola
ms.openlocfilehash: 6edaff73c0828707c7fa736669ba8084663d31ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocontainerize-your-service-fabric-reliable-services-and-reliable-actors-preview"></a><span data-ttu-id="0e4ca-104">Jak toocontainerize Twojego niezawodny sieci szkieletowej usług usług i Reliable Actors (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="0e4ca-104">How toocontainerize your Service Fabric Reliable Services and Reliable Actors (Preview)</span></span>

<span data-ttu-id="0e4ca-105">Sieć szkieletowa usług obsługuje containerizing mikrousług sieci szkieletowej usług (niezawodnej usługi i usługi niezawodnego aktora na podstawie).</span><span class="sxs-lookup"><span data-stu-id="0e4ca-105">Service Fabric supports containerizing Service Fabric microservices (Reliable Services, and Reliable Actor based services).</span></span> <span data-ttu-id="0e4ca-106">Aby uzyskać więcej informacji, zobacz [usługi sieć szkieletowa kontenery](service-fabric-containers-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0e4ca-106">For more information, see [service fabric containers](service-fabric-containers-overview.md).</span></span>


 <span data-ttu-id="0e4ca-107">Ta funkcja jest dostępna w wersji zapoznawczej i w tym artykule przedstawiono hello różnych kroków tooget usługi uruchomione w kontenerze.</span><span class="sxs-lookup"><span data-stu-id="0e4ca-107">This feature is in preview and this article provides hello various steps tooget your service running inside a container.</span></span>  

> [!NOTE]
> <span data-ttu-id="0e4ca-108">Ta funkcja jest w wersji zapoznawczej i nie jest obsługiwana w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="0e4ca-108">This feature is in preview and is not supported in production.</span></span> <span data-ttu-id="0e4ca-109">Obecnie ta funkcja działa tylko dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="0e4ca-109">Currently this feature only works for Windows.</span></span>

## <a name="steps-toocontainerize-your-service-fabric-application"></a><span data-ttu-id="0e4ca-110">Kroki toocontainerize Twojej aplikacji sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="0e4ca-110">Steps toocontainerize your Service Fabric Application</span></span>

1. <span data-ttu-id="0e4ca-111">Otwórz aplikację usługi Service Fabric w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0e4ca-111">Open your Service Fabric application in Visual Studio.</span></span>

2. <span data-ttu-id="0e4ca-112">Dodaj klasę [SFBinaryLoader.cs](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/code/SFBinaryLoaderForContainers/SFBinaryLoader.cs) tooyour projektu.</span><span class="sxs-lookup"><span data-stu-id="0e4ca-112">Add class [SFBinaryLoader.cs](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/code/SFBinaryLoaderForContainers/SFBinaryLoader.cs) tooyour project.</span></span> <span data-ttu-id="0e4ca-113">Kod Hello w tej klasie jest pomocnika toocorrectly obciążenia hello sieci szkieletowej usług obsługi plików binarnych wewnątrz aplikacji, gdy jest używany wewnątrz kontenera.</span><span class="sxs-lookup"><span data-stu-id="0e4ca-113">hello code in this class is a helper toocorrectly load hello Service Fabric runtime binaries inside your application when running inside a container.</span></span>

3. <span data-ttu-id="0e4ca-114">Dla każdego pakietu kodu ma zostać toocontainerize, moduł ładujący hello initialize w punkcie wejścia program hello.</span><span class="sxs-lookup"><span data-stu-id="0e4ca-114">For each code package you would like toocontainerize, initialize hello loader at hello program entry point.</span></span> <span data-ttu-id="0e4ca-115">Dodaj Konstruktor statyczny hello pokazano hello następującego pliku punktu wejścia programu tooyour fragment kodu.</span><span class="sxs-lookup"><span data-stu-id="0e4ca-115">Add hello static constructor shown in hello following code snippet tooyour program entry point file.</span></span>

  ```csharp
  namespace MyApplication
  {
      internal static class Program
      {
          static Program()
          {
              SFBinaryLoader.Initialize();
          }

          /// <summary>
          /// This is hello entry point of hello service host process.
          /// </summary>
          private static void Main()
          {
  ```

4. <span data-ttu-id="0e4ca-116">Tworzenie i [pakietu](service-fabric-package-apps.md#Package-App) Twojego projektu.</span><span class="sxs-lookup"><span data-stu-id="0e4ca-116">Build and [package](service-fabric-package-apps.md#Package-App) your project.</span></span> <span data-ttu-id="0e4ca-117">toobuild i Utwórz pakiet, kliknij prawym przyciskiem myszy projekt aplikacji hello w Eksploratorze rozwiązań i wybierz hello **pakietu** polecenia.</span><span class="sxs-lookup"><span data-stu-id="0e4ca-117">toobuild and create a package, right-click hello application project in Solution Explorer and choose hello **Package** command.</span></span>

5. <span data-ttu-id="0e4ca-118">Dla każdego pakietu kodu należy toocontainerize, hello wykonywania skryptu PowerShell [CreateDockerPackage.ps1](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/scripts/CodePackageToDockerPackage/CreateDockerPackage.ps1).</span><span class="sxs-lookup"><span data-stu-id="0e4ca-118">For every code package you need toocontainerize, run hello PowerShell script [CreateDockerPackage.ps1](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/scripts/CodePackageToDockerPackage/CreateDockerPackage.ps1).</span></span> <span data-ttu-id="0e4ca-119">Użycie Hello jest następujący:</span><span class="sxs-lookup"><span data-stu-id="0e4ca-119">hello usage is as follows:</span></span>
  ```powershell
    $codePackagePath = 'Path toohello code package toocontainerize.'
    $dockerPackageOutputDirectoryPath = 'Output path for hello generated docker folder.'
    $applicationExeName = 'Name of hello ode package executable.'
    CreateDockerPackage.ps1 -CodePackageDirectoryPath $codePackagePath -DockerPackageOutputDirectoryPath $dockerPackageOutputDirectoryPath -ApplicationExeName $applicationExeName
 ```
  <span data-ttu-id="0e4ca-120">Witaj skrypt tworzy folder z artefaktami Docker na $dockerPackageOutputDirectoryPath.</span><span class="sxs-lookup"><span data-stu-id="0e4ca-120">hello script creates a folder with Docker artifacts at $dockerPackageOutputDirectoryPath.</span></span> <span data-ttu-id="0e4ca-121">Zmodyfikuj hello wygenerowany plik Dockerfile tooexpose żadnych portów, uruchom Instalatora, skrypty itp., na podstawie Twoich potrzeb.</span><span class="sxs-lookup"><span data-stu-id="0e4ca-121">Modify hello generated Dockerfile tooexpose any ports, run setup scripts etc. based on your needs.</span></span>

6. <span data-ttu-id="0e4ca-122">Następnie należy się zbyt[kompilacji](service-fabric-get-started-containers.md#Build-Containers) i [wypychania](service-fabric-get-started-containers.md#Push-Containers) repozytorium tooyour pakietu kontenera Docker.</span><span class="sxs-lookup"><span data-stu-id="0e4ca-122">Next you need too[build](service-fabric-get-started-containers.md#Build-Containers) and [push](service-fabric-get-started-containers.md#Push-Containers) your Docker container package tooyour repository.</span></span>

7. <span data-ttu-id="0e4ca-123">Zmodyfikuj hello ApplicationManifest.xml i ServiceManifest.xml tooadd obrazu kontenera, informacje o repozytorium, uwierzytelniania rejestru i mapowania portów do hosta.</span><span class="sxs-lookup"><span data-stu-id="0e4ca-123">Modify hello ApplicationManifest.xml and ServiceManifest.xml tooadd your container image, repository information, registry authentication, and port-to-host mapping.</span></span> <span data-ttu-id="0e4ca-124">Do modyfikowania manifestów hello, zobacz [tworzenie aplikacji kontenera platformy Azure Service Fabric](service-fabric-get-started-containers.md).</span><span class="sxs-lookup"><span data-stu-id="0e4ca-124">For modifying hello manifests, see [Create an Azure Service Fabric container application](service-fabric-get-started-containers.md).</span></span> <span data-ttu-id="0e4ca-125">Witaj definicja pakietu kodu toobe potrzeb manifestu usługi hello zastąpione odpowiedniego kontenera obrazu.</span><span class="sxs-lookup"><span data-stu-id="0e4ca-125">hello code package definition in hello service manifest needs toobe replaced with corresponding container image.</span></span> <span data-ttu-id="0e4ca-126">Upewnij się, że toochange hello punktu wejścia tooa ContainerHost typu.</span><span class="sxs-lookup"><span data-stu-id="0e4ca-126">Make sure toochange hello EntryPoint tooa ContainerHost type.</span></span>

  ```xml
<!-- Code package is your service executable. -->
<CodePackage Name="Code" Version="1.0.0">
  <EntryPoint>
    <!-- Follow this link for more information about deploying Windows containers tooService Fabric: https://aka.ms/sfguestcontainers -->
    <ContainerHost>
      <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
    </ContainerHost>
  </EntryPoint>
  <!-- Pass environment variables tooyour container: -->    
</CodePackage>
  ```

8. <span data-ttu-id="0e4ca-127">Dodaj mapowanie portu na hoście hello replikatora i punktu końcowego usługi.</span><span class="sxs-lookup"><span data-stu-id="0e4ca-127">Add hello port-to-host mapping for your replicator and service endpoint.</span></span> <span data-ttu-id="0e4ca-128">Ponieważ oba te porty są przypisywane w czasie wykonywania przez sieć szkieletowa usług, hello ContainerPort ustawiono hello toouse toozero przypisany port dla mapowania.</span><span class="sxs-lookup"><span data-stu-id="0e4ca-128">Since both these ports are assigned at runtime by Service Fabric, hello ContainerPort is set toozero toouse hello assigned port for mapping.</span></span>

 ```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="0" EndpointRef="ServiceEndpoint"/>
    <PortBinding ContainerPort="0" EndpointRef="ReplicatorEndpoint"/>
  </ContainerHostPolicies>
</Policies>
 ```

9. <span data-ttu-id="0e4ca-129">tootest tej aplikacji należy toodeploy go tooa klastra, który działa w wersji 5.7 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="0e4ca-129">tootest this application, you need toodeploy it tooa cluster that is running version 5.7 or higher.</span></span> <span data-ttu-id="0e4ca-130">Ponadto należy tooedit i zaktualizuj tooenable ustawienia klastra hello tę funkcję w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="0e4ca-130">In addition, you need tooedit and update hello cluster settings tooenable this preview feature.</span></span> <span data-ttu-id="0e4ca-131">Wykonaj kroki hello na tym [artykułu](service-fabric-cluster-fabric-settings.md) ustawienie hello tooadd wyświetlane dalej.</span><span class="sxs-lookup"><span data-stu-id="0e4ca-131">Follow hello steps in this [article](service-fabric-cluster-fabric-settings.md) tooadd hello setting shown next.</span></span>
```
      {
        "name": "Hosting",
        "parameters": [
          {
            "name": "FabricContainerAppsEnabled",
            "value": "true"
          }
        ]
      }
```
10. <span data-ttu-id="0e4ca-132">Następny [wdrażanie](service-fabric-deploy-remove-applications.md) hello edytować klastra toothis pakietu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0e4ca-132">Next [deploy](service-fabric-deploy-remove-applications.md) hello edited application package toothis cluster.</span></span>

<span data-ttu-id="0e4ca-133">Teraz powinien mieć konteneryzowanych aplikacji usługi Service Fabric systemem klastra.</span><span class="sxs-lookup"><span data-stu-id="0e4ca-133">You should now have a containerized Service Fabric application running your cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e4ca-134">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0e4ca-134">Next steps</span></span>
* <span data-ttu-id="0e4ca-135">Dowiedz się więcej o uruchamianiu [kontenerów w usłudze Service Fabric](service-fabric-get-started-containers.md).</span><span class="sxs-lookup"><span data-stu-id="0e4ca-135">Learn more about running [containers on Service Fabric](service-fabric-get-started-containers.md).</span></span>
* <span data-ttu-id="0e4ca-136">Dowiedz się więcej o hello sieci szkieletowej usług [cyklu życia aplikacji](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="0e4ca-136">Learn about hello Service Fabric [application life-cycle](service-fabric-application-lifecycle.md).</span></span>
