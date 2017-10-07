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
# <a name="deploy-a-windows-container-tooservice-fabric"></a>Wdrażanie systemu Windows tooService kontenera sieci szkieletowej
> [!div class="op_single_selector"]
> * [Wdrażanie kontenera systemu Windows](service-fabric-deploy-container.md)
> * [Wdrażanie kontenera Docker](service-fabric-deploy-container-linux.md)
> 
> 

Ten artykuł przeprowadzi Cię przez proces tworzenia konteneryzowanych usług w kontenerach Windows hello.

Sieć szkieletowa usług ma kilka możliwości, które zapewniają pomoc podczas tworzenia aplikacji, które składają się z mikrousług uruchomiony kontenerów. 

Witaj funkcje obejmują:

* Kontener obrazu wdrożenia i aktywacji
* Zarządzanie zasobów
* Repozytorium uwierzytelniania
* Mapowanie portów port kontenera do hosta
* Odnajdywanie kontenera do kontenera i komunikacji
* Możliwość tooconfigure i ustaw zmienne środowiskowe

Oto jak działa każdy z możliwości podczas pakowane toobe konteneryzowanych usługi, dołączony do aplikacji.

## <a name="package-a-windows-container"></a>Pakiet kontenera systemu Windows
Podczas pakowania kontener możesz toouse albo szablon projektu Visual Studio lub [ręcznie utworzyć pakiet aplikacji hello](#manually).  Gdy używasz programu Visual Studio, struktura pakietu aplikacji hello i pliki manifestu zostają utworzone przez szablon nowego projektu hello.

> [!TIP]
> Witaj najprostszy sposób toopackage istniejącego obrazu kontenera do usługi jest toouse programu Visual Studio.

## <a name="use-visual-studio-toopackage-an-existing-container-image"></a>Użyj programu Visual Studio toopackage istniejącego obrazu kontenera
Program Visual Studio udostępnia usługi sieć szkieletowa toohelp szablonu usługi, w przypadku wdrażania klastra usługi sieć szkieletowa tooa kontenera.

1. Wybierz **pliku** > **nowy projekt**i tworzenie aplikacji sieci szkieletowej usług.
2. Wybierz **kontenera gościa** jako hello szablonu usługi.
3. Wybierz **nazwa obrazu** i podaj hello ścieżki toohello obrazu w repozytorium kontenera. Na przykład `myrepo/myimage:v1` w https://hub.docker.com
4. Nadaj nazwę usłudze i kliknij przycisk **OK**.
5. Jeśli usługa konteneryzowanych musi punkt końcowy komunikacji, można teraz dodawać hello protokół, port i plik ServiceManifest.xml toohello typu. Na przykład: 
     
    `<Endpoint Name="MyContainerServiceEndpoint" Protocol="http" Port="80" UriScheme="http" PathSuffix="myapp/" Type="Input" />`
    
    Zapewniając hello `UriScheme`, usługi sieć szkieletowa automatycznie rejestruje punkt końcowy kontenera hello hello usługi nazewnictwa w celu odnajdywania. Hello port być stałe (jak pokazano w hello poprzedzających przykład) lub dynamicznie przydzielane. Jeśli nie określisz port dynamicznie nadawany z zakresu portów aplikacji hello (co się stanie z dowolnej usługi).
    Należy również mapowanie portów toohost tooconfigure hello kontenera, określając `PortBinding` zasad w manifeście aplikacji hello. Aby uzyskać więcej informacji, zobacz [skonfigurować mapowanie portów toohost kontenera](#Portsection).
6. Jeśli z kontenera musi ładu zasobów, a następnie dodaj `ResourceGovernancePolicy`.
8. Jeśli Twoje kontenera musi tooauthenticate z prywatnym repozytorium, Dodaj `RepositoryCredentials`.
7. Jeśli są uruchomione na komputerze z systemem Windows Server 2016, z włączoną obsługą kontenera, można użyć pakietu hello i opublikować akcji toodeploy tooyour lokalnym klastrem. 
8. Po wykonaniu tych czynności można publikować klastra zdalnego tooa aplikacji hello lub zaewidencjonować hello rozwiązania toosource formantu. 

Na przykład hello wyewidencjonowania [przykłady kodu kontenera sieci szkieletowej usług w witrynie GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="creating-a-windows-server-2016-cluster"></a>Tworzenie klastra z systemem Windows Server 2016
toodeploy konteneryzowanych aplikacji, należy toocreate włączone klastra z systemem Windows Server 2016 z obsługą kontenera. Klaster może działać lokalnie lub wdrożone za pośrednictwem usługi Azure Resource Manager na platformie Azure. 

toodeploy klastra przy użyciu usługi Azure Resource Manager, wybierz hello **systemu Windows Server 2016 z kontenerami** obrazu opcji na platformie Azure. Zobacz artykuł hello [tworzenia klastra usługi sieć szkieletowa usług za pomocą usługi Azure Resource Manager](service-fabric-cluster-creation-via-arm.md). Upewnij się, że używasz hello następujące ustawienia usługi Azure Resource Manager:

```xml
"vmImageOffer": { "type": "string","defaultValue": "WindowsServer"     },
"vmImageSku": { "defaultValue": "2016-Datacenter-with-Containers","type": "string"     },
"vmImageVersion": { "defaultValue": "latest","type": "string"     },  
```
Można również użyć hello [szablonu pięć węzłów usługi Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) toocreate klastra. Można również odczytać społeczność [wpis w blogu](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html) przy użyciu kontenerów sieci szkieletowej usług i systemu Windows.

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a>Ręcznie pakietów i wdrożyć obraz kontenera
proces Hello ręcznie pakowania konteneryzowanych usługi jest oparty na powitania następujące kroki:

1. Opublikuj hello kontenery tooyour repozytorium.
2. Utwórz strukturę katalogów hello pakietu.
3. Edytuj hello pliku manifestu usługi.
4. Edytuj plik manifestu aplikacji hello.

## <a name="deploy-and-activate-a-container-image"></a>Wdrażanie i aktywować obrazu kontenera
W sieci szkieletowej usług hello [model aplikacji](service-fabric-application-model.md), kontener reprezentuje hosta aplikacji, w których wiele usługi repliki są umieszczane. toodeploy i Aktywuj kontener, umieść hello nazwa hello kontener obrazu do `ContainerHost` element hello manifestu usługi.

W manifeście usługi hello, Dodaj `ContainerHost` hello punktu wejścia. Następnie zestaw hello `ImageName` toobe hello nazwę hello kontenera repozytorium i obrazów. Hello następujące manifest częściowe przedstawiono przykład sposobu toodeploy hello kontenera o nazwie `myimage:v1` z repozytorium o nazwie `myrepo`:

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

Można określić opcjonalne polecenia toorun po uruchomieniu hello kontenerów hello `Commands` elementu. Dla wielu poleceń przecinkami ograniczyć ich. 

## <a name="understand-resource-governance"></a>Zrozumienie ładu zasobów
Możliwość hello kontenera, który ogranicza hello zasobów, które hello kontenera można używać na hoście hello jest ładu zasobów. Witaj `ResourceGovernancePolicy`, który został określony w manifeście aplikacji hello jest używane toodeclare limity zasobów pakietu kodu usługi. Limity zasobów można ustawić dla hello następujące zasoby:

* Memory (Pamięć)
* MemorySwap
* CpuShares (względną wagę procesora CPU)
* MemoryReservationInMB  
* BlkioWeight (BlockIO względną wagę).

> [!NOTE]
> Obsługa służącą do określonego bloku limity we/wy, takie jak IOPs, odczytu/zapisu liczby bitów na Sekundę i inne osoby, które są planowane w przyszłości.
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

## <a name="authenticate-a-repository"></a>Uwierzytelnianie repozytorium
toodownload kontener może być tooprovide poświadczenia logowania toohello kontenera repozytorium. Hello poświadczenia logowania, określona w manifeście aplikacji hello, są używane toospecify hello informacje rejestrowania lub klucza SSH do pobrania obrazu kontenera hello hello repozytorium obrazów. Witaj poniższy przykład przedstawia konta o nazwie *TestUser* wraz z hello hasła w postaci zwykłego tekstu (*nie* zalecana):

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

Firma Microsoft zaleca szyfrowania hello hasła przy użyciu certyfikatu, który został wdrożony toohello maszyny.

Witaj poniższy przykład przedstawia konta o nazwie *TestUser*, gdzie hasło hello została zaszyfrowana przy użyciu certyfikatu o nazwie *MyCert*. Można użyć hello `Invoke-ServiceFabricEncryptText` tekst toocreate polecenia programu PowerShell tajny szyfrowania hello hello hasła. Aby uzyskać więcej informacji, zobacz artykuł hello [Zarządzanie kluczy tajnych w aplikacji usługi Service Fabric](service-fabric-application-secret-management.md).

klucz prywatny Hello hello certyfikatu, który został użyty toodecrypt hello hasło musi być wdrożone toohello komputera lokalnego w metodzie poza pasmem. (Na platformie Azure, ta metoda jest usługi Azure Resource Manager). Następnie gdy usługa sieć szkieletowa wdraża hello usługi pakietu toohello maszyny, może odszyfrować klucza tajnego hello. Przy użyciu klucza tajnego hello wraz z nazwą konta hello, następnie uwierzytelniania hello kontenera repozytorium.

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

## <a name ="Portsection"></a>Skonfiguruj mapowanie portów toohost kontenera
Można skonfigurować toocommunicate port używany host hello kontenera, określając `PortBinding` w manifeście aplikacji hello. wewnątrz hello kontenera tooa portu na hoście hello nasłuchuje Hello portu powiązania mapy hello portu toowhich hello usługa.

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

## <a name="configure-container-to-container-discovery-and-communication"></a>Konfigurowanie odnajdywania kontenera do kontenera i komunikacji
Można użyć hello `PortBinding` toomap elementu punktu końcowego tooan port kontenera w hello manifestu usługi. W hello poniższy przykład, hello punktu końcowego `Endpoint1` określa 8905 stałego portu. Może również określać nie portu, w tym przypadku losowego portu z zakresu portów aplikacji hello klastra jest wybierany dla Ciebie.


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
Jeśli określisz punkt końcowy, za pomocą hello `Endpoint` tag w manifeście usługi hello kontenera gościa, Service Fabric automatycznie opublikować toohello tego punktu końcowego usługi nazw. Inne usługi, które są uruchomione w klastrze hello w związku z tym można odnaleźć tego kontenera za pomocą zapytań REST hello w celu rozwiązania.

Zarejestrowani hello Naming service, można wykonać kontenera do kontenera komunikacji z kontenera za pomocą hello [odwrotny serwer proxy](service-fabric-reverseproxy.md). Komunikacja odbywa się przez podanie port nasłuchujący hello zwrotny serwer proxy http i nazwa hello hello usług, które ma być toocommunicate ze zmiennych środowiskowych. Aby uzyskać więcej informacji zobacz następną sekcję hello. 

## <a name="configure-and-set-environment-variables"></a>Konfigurowanie i ustawianie zmiennych środowiskowych
Zmienne środowiskowe można określić dla każdego pakietu kodu w hello manifestu usługi. Ta funkcja jest dostępna dla wszystkich usług niezależnie od tego, czy są one wdrażane jako kontenery, procesy, czy pliki wykonywalne gościa. Można zastąpić zmiennej środowiskowej wartości w aplikacji hello manifestu lub określić ich podczas wdrażania jako parametry aplikacji.

Witaj poniższy fragment XML manifestu usługi przedstawia przykładowy sposób zmiennych środowiskowych toospecify pakietu kodu:

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

Te zmienne środowiskowe umożliwić przesłanianie go na poziomie manifestu aplikacji hello:

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

W poprzednim przykładzie hello, możemy określić jawną wartość dla hello `HttpGateway` zmiennej środowiskowej (19000), gdy firma Microsoft ustaw wartość hello `BackendServiceName` parametr za pomocą hello `[BackendSvc]` parametr aplikacji. Te ustawienia umożliwiają wartość hello toospecify `BackendServiceName`wartość wdrażania aplikacji hello i ma wartość stałą w manifeście hello.

## <a name="configure-isolation-mode"></a>Konfigurowanie trybu izolacji

System Windows obsługuje dwa tryby izolacji dla kontenerów - procesu oraz funkcji Hyper-V.  W trybie izolacji procesu hello wszystkich kontenerów hello systemem hello tego samego hosta maszyny udziału hello jądra z hostem hello. W trybie izolacji hello funkcji Hyper-V między każdego kontenera funkcji Hyper-V a hostem kontenera hello odizolowanych hello jądra. Tryb izolacji Hello jest określony w hello `ContainerHostPolicies` znacznika w pliku manifestu aplikacji hello.  Tryby izolacji Hello, które można określić są `process`, `hyperv`, i `default`. Witaj `default` trybu izolacji domyślnie przyjmowana jest zbyt`process` w systemie Windows Server obsługuje i domyślnie przyjmowana jest zbyt`hyperv` na hostach z systemem Windows 10.  Hello poniższy fragment kodu przedstawia sposób hello trybu izolacji została określona w pliku manifestu aplikacji hello.

```xml
   <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="hyperv">
```


## <a name="complete-examples-for-application-and-service-manifest"></a>Zakończenie przykłady aplikacji i manifest usługi

Następujący przykład manifestu aplikacji:

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

Następujący przykład manifestu usługi (określone w powyższej manifest aplikacji hello):

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

## <a name="next-steps"></a>Następne kroki
Po wdrożeniu usługi konteneryzowanych, Dowiedz się, jak toomanage cykl życia, odczytując [cyklem życia aplikacji usługi sieć szkieletowa](service-fabric-application-lifecycle.md).

* [Omówienie sieci szkieletowej usług i kontenerów](service-fabric-containers-overview.md)
* Na przykład wyewidencjonowania [przykłady kodu kontenera sieci szkieletowej usług w witrynie GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
