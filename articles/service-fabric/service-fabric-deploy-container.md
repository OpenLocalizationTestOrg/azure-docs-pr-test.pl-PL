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
# <a name="deploy-a-windows-container-to-service-fabric"></a>Wdrażanie kontenera systemu Windows w sieci szkieletowej usług
> [!div class="op_single_selector"]
> * [Wdrażanie kontenera systemu Windows](service-fabric-deploy-container.md)
> * [Wdrażanie kontenera Docker](service-fabric-deploy-container-linux.md)
> 
> 

Ten artykuł przeprowadzi Cię przez proces tworzenia konteneryzowanych usług w kontenerach systemu Windows.

Sieć szkieletowa usług ma kilka możliwości, które zapewniają pomoc podczas tworzenia aplikacji, które składają się z mikrousług uruchomiony kontenerów. 

Funkcje obejmują:

* Kontener obrazu wdrożenia i aktywacji
* Zarządzanie zasobów
* Repozytorium uwierzytelniania
* Mapowanie portów port kontenera do hosta
* Odnajdywanie kontenera do kontenera i komunikacji
* Możliwość konfigurowania i ustaw zmienne środowiskowe

Oto jak działa każdy z możliwości podczas pakowane konteneryzowanych usługi do uwzględnienia w aplikacji.

## <a name="package-a-windows-container"></a>Pakiet kontenera systemu Windows
Podczas pakowania kontener, można użyć albo szablon projektu Visual Studio lub [ręcznie utworzyć pakiet aplikacji](#manually).  Korzystając z programu Visual Studio, struktura pakietu aplikacji i pliki manifestu są tworzone przez szablon nowego projektu dla Ciebie.

> [!TIP]
> Najprostszym sposobem pakietu istniejącego obrazu kontenera do usługi jest używać programu Visual Studio.

## <a name="use-visual-studio-to-package-an-existing-container-image"></a>Pakiet istniejącego obrazu kontenera za pomocą programu Visual Studio
Program Visual Studio udostępnia szablonu usługi Service Fabric ułatwiają wdrażanie kontenera do klastra usługi sieć szkieletowa usług.

1. Wybierz **pliku** > **nowy projekt**i tworzenie aplikacji sieci szkieletowej usług.
2. Wybierz **kontenera gościa** jako szablonu usługi.
3. Wybierz **nazwa obrazu** i podaj ścieżkę do obrazu w repozytorium kontenera. Na przykład `myrepo/myimage:v1` w https://hub.docker.com
4. Nadaj nazwę usłudze i kliknij przycisk **OK**.
5. Jeśli usługa konteneryzowanych musi punkt końcowy komunikacji, protokół, port i typ można teraz dodać do pliku ServiceManifest.xml. Na przykład: 
     
    `<Endpoint Name="MyContainerServiceEndpoint" Protocol="http" Port="80" UriScheme="http" PathSuffix="myapp/" Type="Input" />`
    
    Zapewniając `UriScheme`, automatycznie rejestruje punkt końcowy kontenera nazewnictwa w usłudze odnajdywania w sieci szkieletowej usług. Port można stałej (jak pokazano w poprzednim przykładzie) lub dynamicznie przydzielane. Jeśli nie określisz port dynamicznie nadawany z zakresu aplikacji (co się stanie z dowolnej usługi).
    Należy również skonfigurować kontener, aby mapowanie portów hosta, określając `PortBinding` zasad w manifeście aplikacji. Aby uzyskać więcej informacji, zobacz [kontenera konfiguracji do mapowania port hosta](#Portsection).
6. Jeśli z kontenera musi ładu zasobów, a następnie dodaj `ResourceGovernancePolicy`.
8. Jeśli kontener wymaga uwierzytelniania w prywatnym repozytorium, dodaj parametr `RepositoryCredentials`.
7. Jeśli są uruchomione na komputerze z systemem Windows Server 2016, z włączoną obsługą kontenera, można za pomocą pakietu i opublikować akcji do wdrożenia na lokalny klaster. 
8. Po wykonaniu tych czynności możesz opublikować aplikację do zdalnego klastra lub zaewidencjonować rozwiązanie do kontroli źródła. 

Na przykład wyewidencjonowania [przykłady kodu kontenera sieci szkieletowej usług w witrynie GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="creating-a-windows-server-2016-cluster"></a>Tworzenie klastra z systemem Windows Server 2016
Aby wdrożyć aplikację konteneryzowanych, musisz utworzyć klastra z systemem Windows Server 2016 z włączoną obsługą usługi kontenera. Klaster może działać lokalnie lub wdrożone za pośrednictwem usługi Azure Resource Manager na platformie Azure. 

Aby wdrożyć klaster za pomocą usługi Azure Resource Manager, wybierz **systemu Windows Server 2016 z kontenerami** obrazu opcji na platformie Azure. Zapoznaj się z artykułem [tworzenia klastra usługi sieć szkieletowa usług za pomocą usługi Azure Resource Manager](service-fabric-cluster-creation-via-arm.md). Upewnij się, że używasz następujące ustawienia usługi Azure Resource Manager:

```xml
"vmImageOffer": { "type": "string","defaultValue": "WindowsServer"     },
"vmImageSku": { "defaultValue": "2016-Datacenter-with-Containers","type": "string"     },
"vmImageVersion": { "defaultValue": "latest","type": "string"     },  
```
Można również użyć [szablonu pięć węzłów usługi Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) do utworzenia klastra. Można również odczytać społeczność [wpis w blogu](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html) przy użyciu kontenerów sieci szkieletowej usług i systemu Windows.

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a>Ręcznie pakietów i wdrożyć obraz kontenera
Proces ręcznie pakowania konteneryzowanych usługa jest oparta na następujące czynności:

1. Opublikuj kontenerów do repozytorium.
2. Utwórz strukturę katalogu pakietu.
3. Edytuj plik manifestu usługi.
4. Przeprowadź edycję pliku manifestu aplikacji.

## <a name="deploy-and-activate-a-container-image"></a>Wdrażanie i aktywować obrazu kontenera
W sieci szkieletowej usług [model aplikacji](service-fabric-application-model.md), kontener reprezentuje hosta aplikacji, w których wiele usługi repliki są umieszczane. Aby wdrożyć i aktywować kontener, put nazwa obrazu kontenera do `ContainerHost` element manifestu usługi.

W manifeście usługi, dodać `ContainerHost` dla punktu wejścia. Następnie ustaw `ImageName` nazwę kontenera repozytorium i obrazów. Manifest częściowe następujące przedstawiono przykład sposobu wdrażania kontenera o nazwie `myimage:v1` z repozytorium o nazwie `myrepo`:

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

Można określić opcjonalne polecenia do uruchomienia po rozpoczęciu kontenera w obszarze `Commands` elementu. Dla wielu poleceń przecinkami ograniczyć ich. 

## <a name="understand-resource-governance"></a>Zrozumienie ładu zasobów
Ładu zasobów jest możliwość kontenera, który ogranicza zasobów korzystających przez kontener na hoście. `ResourceGovernancePolicy`, Który został określony w manifeście aplikacji służy do deklarowania limity zasobów pakietu kodu usługi. Limity zasobów można ustawić dla następujących zasobów:

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
Aby pobrać kontener, może być konieczne podanie poświadczeń logowania do repozytorium kontenera. Poświadczenia logowania, określona w manifeście aplikacji są używane do określenia informacji logowania lub klucza SSH do pobierania obrazu kontenera z repozytorium obrazów. W poniższym przykładzie przedstawiono konta o nazwie *TestUser* wraz z hasła w postaci zwykłego tekstu (*nie* zalecana):

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

Firma Microsoft zaleca szyfrowania hasła przy użyciu certyfikatu, które zostały wdrożone na maszynie.

W poniższym przykładzie przedstawiono konta o nazwie *TestUser*, gdzie hasło została zaszyfrowana przy użyciu certyfikatu o nazwie *MyCert*. Można użyć `Invoke-ServiceFabricEncryptText` polecenie programu PowerShell, aby utworzyć tekst tajny szyfrowania hasła. Aby uzyskać więcej informacji, zobacz artykuł [Zarządzanie kluczy tajnych w aplikacji usługi Service Fabric](service-fabric-application-secret-management.md).

Klucz prywatny certyfikatu, który jest używany do odszyfrowywania hasła należy wdrożyć na komputerze lokalnym w metodzie poza pasmem. (Na platformie Azure, ta metoda jest usługi Azure Resource Manager). Następnie gdy sieć szkieletowa usług wdraża pakiet usługi do komputera, może odszyfrować klucza tajnego. Przy użyciu klucza tajnego wraz z nazwą konta, następnie uwierzytelniania z repozytorium kontenera.

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

## <a name ="Portsection"></a>Skonfiguruj kontener, aby mapowanie portów hosta
Można skonfigurować port hosta używany do komunikacji z kontenerem, określając `PortBinding` w manifeście aplikacji. Powiązanie portu mapy numer portu, z którym nasłuchuje usługa wewnątrz kontenera do portu na hoście.

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
Można użyć `PortBinding` elementu, aby mapować port kontenera do punktu końcowego w manifeście usługi. W poniższym przykładzie punktu końcowego `Endpoint1` określa 8905 stałego portu. Może również określać żadnego portu, w takim przypadku losowego portu z zakresu portów aplikacji klastra jest wybierany dla Ciebie.


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
Jeśli określisz punkt końcowy, za pomocą `Endpoint` tag w manifeście usługi kontenera gościa, Service Fabric automatycznie opublikować ten punkt końcowy usługi nazw. Inne usługi, które są uruchomione w klastrze w związku z tym umożliwia odnalezienie tego kontenera za pomocą zapytań REST dla rozwiązania.

Rejestrując z usługą Naming mogą wykonywać kontenera do kontenera komunikacji z kontenera za pomocą [odwrotny serwer proxy](service-fabric-reverseproxy.md). Komunikacja odbywa się przez podanie port nasłuchiwania zwrotny serwer proxy http i nazwę usługi, która ma do komunikowania się z jako zmienne środowiskowe. Aby uzyskać więcej informacji zobacz następną sekcję. 

## <a name="configure-and-set-environment-variables"></a>Konfigurowanie i ustawianie zmiennych środowiskowych
Zmienne środowiskowe można określić dla każdego pakietu kodu w manifeście usługi. Ta funkcja jest dostępna dla wszystkich usług niezależnie od tego, czy są one wdrażane jako kontenery, procesy, czy pliki wykonywalne gościa. Wartości zmiennych środowiskowych można przesłonić w manifeście aplikacji lub podać je podczas wdrażania jako parametry aplikacji.

Następujący fragment kodu XML manifestu usługi stanowi przykład sposobu określania zmiennych środowiskowych dla pakietu kodu:

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

Te zmienne środowiskowe umożliwić przesłanianie go na poziomie manifestu aplikacji:

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

W poprzednim przykładzie, możemy określić jawną wartość dla `HttpGateway` zmiennej środowiskowej (19000), gdy firma Microsoft ustaw wartość `BackendServiceName` parametr za pomocą `[BackendSvc]` parametr aplikacji. Te ustawienia umożliwiają określenie wartości `BackendServiceName`wartość wdrażania aplikacji i nie ma wartości stałej w manifeście.

## <a name="configure-isolation-mode"></a>Konfigurowanie trybu izolacji

System Windows obsługuje dwa tryby izolacji dla kontenerów - procesu oraz funkcji Hyper-V.  W trybie izolacji procesu wszystkie kontenery działające na tym samym hoście współdzielą jądro z hostem. W trybie izolacji funkcji Hyper-V jądra są odizolowane dla każdego kontenera funkcji Hyper-V i hosta kontenera. W trybie izolacji określono `ContainerHostPolicies` znacznika w pliku manifestu aplikacji.  Tryby izolacji, które można określić, to `process`, `hyperv` i `default`. `default` Domyślnym trybem izolacji `process` na hostach z systemem Windows Server i wartość domyślna to `hyperv` na hostach z systemem Windows 10.  Poniższy fragment kodu przedstawia sposób określania trybu izolacji w pliku manifestu aplikacji.

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

Następujący przykład manifestu usługi (określony w poprzednim manifest aplikacji):

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
Teraz, zostały wdrożone usługi konteneryzowanych, Dowiedz się, jak zarządzać jego cyklem odczytując [cyklem życia aplikacji usługi sieć szkieletowa](service-fabric-application-lifecycle.md).

* [Omówienie sieci szkieletowej usług i kontenerów](service-fabric-containers-overview.md)
* Na przykład wyewidencjonowania [przykłady kodu kontenera sieci szkieletowej usług w witrynie GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
