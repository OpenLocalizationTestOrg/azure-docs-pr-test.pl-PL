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
# <a name="how-toocontainerize-your-service-fabric-reliable-services-and-reliable-actors-preview"></a>Jak toocontainerize Twojego niezawodny sieci szkieletowej usług usług i Reliable Actors (wersja zapoznawcza)

Sieć szkieletowa usług obsługuje containerizing mikrousług sieci szkieletowej usług (niezawodnej usługi i usługi niezawodnego aktora na podstawie). Aby uzyskać więcej informacji, zobacz [usługi sieć szkieletowa kontenery](service-fabric-containers-overview.md).


 Ta funkcja jest dostępna w wersji zapoznawczej i w tym artykule przedstawiono hello różnych kroków tooget usługi uruchomione w kontenerze.  

> [!NOTE]
> Ta funkcja jest w wersji zapoznawczej i nie jest obsługiwana w środowisku produkcyjnym. Obecnie ta funkcja działa tylko dla systemu Windows.

## <a name="steps-toocontainerize-your-service-fabric-application"></a>Kroki toocontainerize Twojej aplikacji sieci szkieletowej usług

1. Otwórz aplikację usługi Service Fabric w programie Visual Studio.

2. Dodaj klasę [SFBinaryLoader.cs](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/code/SFBinaryLoaderForContainers/SFBinaryLoader.cs) tooyour projektu. Kod Hello w tej klasie jest pomocnika toocorrectly obciążenia hello sieci szkieletowej usług obsługi plików binarnych wewnątrz aplikacji, gdy jest używany wewnątrz kontenera.

3. Dla każdego pakietu kodu ma zostać toocontainerize, moduł ładujący hello initialize w punkcie wejścia program hello. Dodaj Konstruktor statyczny hello pokazano hello następującego pliku punktu wejścia programu tooyour fragment kodu.

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

4. Tworzenie i [pakietu](service-fabric-package-apps.md#Package-App) Twojego projektu. toobuild i Utwórz pakiet, kliknij prawym przyciskiem myszy projekt aplikacji hello w Eksploratorze rozwiązań i wybierz hello **pakietu** polecenia.

5. Dla każdego pakietu kodu należy toocontainerize, hello wykonywania skryptu PowerShell [CreateDockerPackage.ps1](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/scripts/CodePackageToDockerPackage/CreateDockerPackage.ps1). Użycie Hello jest następujący:
  ```powershell
    $codePackagePath = 'Path toohello code package toocontainerize.'
    $dockerPackageOutputDirectoryPath = 'Output path for hello generated docker folder.'
    $applicationExeName = 'Name of hello ode package executable.'
    CreateDockerPackage.ps1 -CodePackageDirectoryPath $codePackagePath -DockerPackageOutputDirectoryPath $dockerPackageOutputDirectoryPath -ApplicationExeName $applicationExeName
 ```
  Witaj skrypt tworzy folder z artefaktami Docker na $dockerPackageOutputDirectoryPath. Zmodyfikuj hello wygenerowany plik Dockerfile tooexpose żadnych portów, uruchom Instalatora, skrypty itp., na podstawie Twoich potrzeb.

6. Następnie należy się zbyt[kompilacji](service-fabric-get-started-containers.md#Build-Containers) i [wypychania](service-fabric-get-started-containers.md#Push-Containers) repozytorium tooyour pakietu kontenera Docker.

7. Zmodyfikuj hello ApplicationManifest.xml i ServiceManifest.xml tooadd obrazu kontenera, informacje o repozytorium, uwierzytelniania rejestru i mapowania portów do hosta. Do modyfikowania manifestów hello, zobacz [tworzenie aplikacji kontenera platformy Azure Service Fabric](service-fabric-get-started-containers.md). Witaj definicja pakietu kodu toobe potrzeb manifestu usługi hello zastąpione odpowiedniego kontenera obrazu. Upewnij się, że toochange hello punktu wejścia tooa ContainerHost typu.

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

8. Dodaj mapowanie portu na hoście hello replikatora i punktu końcowego usługi. Ponieważ oba te porty są przypisywane w czasie wykonywania przez sieć szkieletowa usług, hello ContainerPort ustawiono hello toouse toozero przypisany port dla mapowania.

 ```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="0" EndpointRef="ServiceEndpoint"/>
    <PortBinding ContainerPort="0" EndpointRef="ReplicatorEndpoint"/>
  </ContainerHostPolicies>
</Policies>
 ```

9. tootest tej aplikacji należy toodeploy go tooa klastra, który działa w wersji 5.7 lub nowszej. Ponadto należy tooedit i zaktualizuj tooenable ustawienia klastra hello tę funkcję w wersji zapoznawczej. Wykonaj kroki hello na tym [artykułu](service-fabric-cluster-fabric-settings.md) ustawienie hello tooadd wyświetlane dalej.
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
10. Następny [wdrażanie](service-fabric-deploy-remove-applications.md) hello edytować klastra toothis pakietu aplikacji.

Teraz powinien mieć konteneryzowanych aplikacji usługi Service Fabric systemem klastra.

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o uruchamianiu [kontenerów w usłudze Service Fabric](service-fabric-get-started-containers.md).
* Dowiedz się więcej o hello sieci szkieletowej usług [cyklu życia aplikacji](service-fabric-application-lifecycle.md).
