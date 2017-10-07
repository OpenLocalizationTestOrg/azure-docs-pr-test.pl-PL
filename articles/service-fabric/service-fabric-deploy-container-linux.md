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
# <a name="deploy-a-linux-container-tooservice-fabric"></a>Wdrażanie systemu Linux tooService kontenera sieci szkieletowej
> [!div class="op_single_selector"]
> * [Wdrażanie kontenera systemu Windows](service-fabric-deploy-container.md)
> * [Wdrażanie kontenera systemu Linux](service-fabric-deploy-container-linux.md)
>
>

W tym artykule przedstawiono tworzenie konteneryzowanych usług w kontenerach Docker w systemie Linux.

Sieć szkieletowa usług ma kilka możliwości kontenera, które zapewniają pomoc podczas tworzenia aplikacji, które składają się z mikrousług, które są konteneryzowanych. Te usługi są nazywane konteneryzowanych usług.

możliwości Hello obejmują;

* Kontener obrazu wdrożenia i aktywacji
* Zarządzanie zasobów
* Repozytorium uwierzytelniania
* Mapowanie portów toohost port kontenera
* Odnajdywanie kontenera do kontenera i komunikacji
* Możliwość tooconfigure i ustaw zmienne środowiskowe

## <a name="packaging-a-docker-container-with-yeoman"></a>Pakowanie kontenera docker z narzędzia yeoman
Podczas pakowania kontenera w systemie Linux, można wybrać obu toouse szablonu narzędzia yeoman lub [ręcznie utworzyć pakiet aplikacji hello](#manually).

Aplikacji usługi Service Fabric może zawierać jeden lub więcej kontenerów, każda z określoną rolę w dostarczaniu funkcjonalności aplikacji hello. Witaj zestawu SDK sieci szkieletowej usług dla systemu Linux zawiera [narzędzia Yeoman](http://yeoman.io/) generator kodu, który umożliwia łatwe toocreate aplikacji i Dodaj obraz kontenera. Można użyć narzędzia Yeoman toocreate o nazwie aplikacji o jeden kontener Docker *SimpleContainerApp*. Więcej usług można dodać później, edytując hello wygenerować pliki manifestu.

## <a name="install-docker-on-your-development-box"></a>Zainstaluj Docker na Twoje okno programowanie

Witaj uruchom następujące polecenia docker tooinstall Twojego pole rozwoju systemu Linux (Jeśli używasz vagrant obraz powitania w systemie OSX, docker jest już zainstalowana):

```bash
    sudo apt-get install wget
    wget -qO- https://get.docker.io/ | sh
```

## <a name="create-hello-application"></a>Tworzenie aplikacji hello
1. Na terminalu wpisz `yo azuresfcontainer`.
2. Nazwa aplikacji — na przykład mycontainerap
3. Podaj adres URL hello hello kontener obrazu z repozytorium DockerHub. Witaj formularz hello przyjmuje parametr obrazu [repozytorium] / [nazwa obrazu]
4. Jeśli obraz powitania nie ma obciążenia punktu wejścia zdefiniowana, a następnie należy tooexplicitly określić wejściowych polecenia przy użyciu zestawu poleceń toorun wewnątrz kontenera hello zachowa kontenera hello uruchomiona po uruchomieniu rozdzielonych przecinkami.

![Generator Yeoman usługi Service Fabric dla kontenerów][sf-yeoman]

## <a name="deploy-hello-application"></a>Wdrażanie aplikacji hello

### <a name="using-xplat-cli"></a>Korzystanie z interfejsu wiersza polecenia XPlat
Po utworzeniu aplikacji hello można wdrożyć klaster lokalny toohello przy użyciu hello Azure CLI.

1. Połącz toohello lokalnego klastra usługi sieć szkieletowa usług.

    ```bash
    azure servicefabric cluster connect
    ```

2. Użyj hello zainstalować skrypt toocopy szablonu hello aplikacji hello pakietu magazynu obrazu klastra toohello, Rejestracja typu aplikacji hello, i Utwórz wystąpienie aplikacji hello.

    ```bash
    ./install.sh
    ```

3. Otwórz przeglądarkę i przejdź tooService Eksploratora sieci szkieletowej w http://localhost: 19080/Explorer (localhost Zamień z hello prywatnego adresu IP hello maszyny Wirtualnej, jeśli przy użyciu Vagrant w systemie Mac OS X).
4. Rozwiń węzeł aplikacji hello i należy pamiętać, że teraz wpis dla danego typu aplikacji i drugi dla hello pierwsze wystąpienie tego typu.
5. Użyj skryptu Odinstaluj hello podane w wystąpienia aplikacji hello hello szablonu toodelete i wyrejestrowywanie typu aplikacji hello.

    ```bash
    ./uninstall.sh
    ```

### <a name="using-azure-cli-20"></a>Korzystanie z interfejsu wiersza polecenia platformy Azure 2.0

Zobacz hello odwołania dokumentu na zarządzaniu [cyklu życia aplikacji przy użyciu hello Azure CLI 2.0](service-fabric-application-lifecycle-azure-cli-2-0.md).

Na przykład aplikacja [przykłady hello wyewidencjonowania kodu kontenera sieci szkieletowej usług w witrynie GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="adding-more-services-tooan-existing-application"></a>Dodawanie więcej usług tooan istniejącej aplikacji

tooadd innego kontenera usługi już utworzone przy użyciu aplikacji tooan `yo`, wykonaj następujące kroki hello:

1. Zmień katalog główny toohello hello istniejącej aplikacji.  Na przykład `cd ~/YeomanSamples/MyApplication`, jeśli `MyApplication` to aplikacja hello utworzone przez narzędzia Yeoman.
2. Uruchom polecenie `yo azuresfcontainer:AddService`

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

Możesz podać polecenia wejściowe, określając hello opcjonalne `Commands` elementu przy użyciu zestawu poleceń toorun wewnątrz kontenera hello rozdzielonych przecinkami.

> [!NOTE]
> Jeśli obraz powitania nie ma obciążenia punktu wejścia zdefiniowana, a następnie należy tooexplicitly określić polecenia wprowadzania wewnątrz `Commands` elementu przy użyciu zestawu poleceń toorun wewnątrz kontenera hello, w którym zostaną zachowane po kontenera hello rozdzielana przecinkami uruchamianie.

## <a name="understand-resource-governance"></a>Zrozumienie ładu zasobów
Możliwość hello kontenera, który ogranicza hello zasobów, które hello kontenera można używać na hoście hello jest ładu zasobów. Witaj `ResourceGovernancePolicy`, który został określony w manifeście aplikacji hello jest używane toodeclare limity zasobów pakietu kodu usługi. Limity zasobów można ustawić dla hello następujące zasoby:

* Memory (Pamięć)
* MemorySwap
* CpuShares (względną wagę procesora CPU)
* MemoryReservationInMB  
* BlkioWeight (BlockIO względną wagę).

> [!NOTE]
> W przyszłym wydaniu obsługę bloku określonego limity we/wy, takich jak IOPs, określając odczytu/zapisu liczby bitów na Sekundę i inni użytkownicy będą dołączone.
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

## <a name="configure-container-port-to-host-port-mapping"></a>Skonfiguruj mapowanie portów port kontenera do hosta
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
Za pomocą hello `PortBinding` zasad, możesz mapować tooan port kontenera `Endpoint` w hello manifestu usługi. Witaj punktu końcowego `Endpoint1` można określić stały port (na przykład port 80). Może również określać nie portu, w tym przypadku losowego portu z zakresu portów aplikacji hello klastra jest wybierany dla Ciebie.

Jeśli określisz punkt końcowy, za pomocą hello `Endpoint` tag w manifeście usługi hello kontenera gościa, Service Fabric automatycznie opublikować toohello tego punktu końcowego usługi nazw. Inne usługi, które są uruchomione w klastrze hello w związku z tym można odnaleźć tego kontenera za pomocą zapytań REST hello w celu rozwiązania.

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

Zarejestrowani hello Naming service, można łatwo wykonać komunikacji kontenera do kontenera w kodzie hello w Twojej kontenera przy użyciu hello [odwrotny serwer proxy](service-fabric-reverseproxy.md). Komunikacja odbywa się przez podanie port nasłuchujący hello zwrotny serwer proxy http i nazwa hello hello usług, które ma być toocommunicate ze zmiennych środowiskowych. Aby uzyskać więcej informacji zobacz następną sekcję hello.

## <a name="configure-and-set-environment-variables"></a>Konfigurowanie i ustawianie zmiennych środowiskowych
Zmienne środowiskowe można określić dla każdego pakietu kodu w manifeście usługi hello, zarówno dla usługi, które są wdrażane w kontenerach lub usług, które są wdrażane jako pliki wykonywalne procesów/gościa. Te wartości zmiennych środowiskowych można zastąpić w szczególności w manifeście aplikacji hello lub określony podczas wdrażania jako parametry aplikacji.

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
* [Interakcja z klastrów sieci szkieletowej usług za pomocą hello wiersza polecenia platformy Azure](service-fabric-azure-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-deploy-container-linux/sf-container-yeoman1.png

## <a name="related-articles"></a>Pokrewne artykuły:

* [Getting started with Service Fabric and Azure CLI 2.0](service-fabric-azure-cli-2-0.md) (Wprowadzenie do usługi Service Fabric i interfejsu wiersza polecenia platformy Azure 2.0)
* [Getting started with Service Fabric XPlat CLI](service-fabric-azure-cli.md) (Wprowadzenie do interfejsu wiersza polecenia XPlat usługi Service Fabric)
