---
title: aaaCreate aplikacji kontenera platformy Azure Service Fabric w systemie Linux | Dokumentacja firmy Microsoft
description: "Utwórz swoją pierwszą aplikację kontenera systemu Linux w usłudze Azure Service Fabric.  Utwórz obraz Docker z aplikacją, push hello obrazu tooa kontenera rejestru, kompilacji i wdrażania aplikacji kontenera sieci szkieletowej usług."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/28/2017
ms.author: ryanwi
ms.openlocfilehash: 348dbcbaa1a534fb2808450e4c2d5f9acc7c7b35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-container-application-on-linux"></a>Tworzenie pierwszej aplikacji kontenera usługi Service Fabric w systemie Linux
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started-containers.md)
> * [Linux](service-fabric-get-started-containers-linux.md)

Systemem istniejącej aplikacji w kontenerze systemu Linux w klastrze usługi sieć szkieletowa nie wymaga żadnych zmian tooyour aplikacji. W tym artykule przedstawiono tworzenie obrazu Docker zawierający Python [Flask](http://flask.pocoo.org/) sieci web, aplikacji i wdrażania go tooa klastra sieci szkieletowej usług.  Będziesz również udostępniać aplikację skonteneryzowaną za pomocą usługi [Azure Container Registry](/azure/container-registry/).  W tym artykule przyjęto założenie, że masz podstawową wiedzą dotyczącą platformy Docker. Informacje na temat rozwiązania Docker za odczytywanie hello [omówienie Docker](https://docs.docker.com/engine/understanding-docker/).

## <a name="prerequisites"></a>Wymagania wstępne
* Komputer dewelopera z następującym oprogramowaniem:
  * [Zestaw SDK usługi Service Fabric oraz narzędzia](service-fabric-get-started-linux.md).
  * [Docker CE dla systemu Linux](https://docs.docker.com/engine/installation/#prior-releases). 
  * [Interfejs wiersza polecenia usługi Service Fabric](service-fabric-cli.md)

* Rejestr w usłudze Azure Container Registry — [utwórz rejestr kontenera](../container-registry/container-registry-get-started-portal.md) w subskrypcji platformy Azure. 

## <a name="define-hello-docker-container"></a>Zdefiniuj hello kontenera Docker
Tworzenie obrazu opartego na powitania [obrazu Python](https://hub.docker.com/_/python/) znajduje się w Centrum Docker. 

Zdefiniuj kontener platformy Docker w pliku Dockerfile. Plik Dockerfile Hello zawiera instrukcje dotyczące konfigurowania środowiska hello wewnątrz kontenera sieci, ładowania aplikacji hello ma toorun i mapowania portów. Hello plik Dockerfile jest toohello wejściowych hello `docker build` polecenia, które tworzy obraz powitania. 

Utwórz pusty katalog i Utwórz plik hello *plik Dockerfile* (z bez rozszerzenia pliku). Dodaje hello zbyt*plik Dockerfile* i Zapisz zmiany:

```
# Use an official Python runtime as a base image
FROM python:2.7-slim

# Set hello working directory too/app
WORKDIR /app

# Copy hello current directory contents into hello container at /app
ADD . /app

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt

# Make port 80 available outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when hello container launches
CMD ["python", "app.py"]
```

Witaj odczytu [odwołania plik Dockerfile](https://docs.docker.com/engine/reference/builder/) Aby uzyskać więcej informacji.

## <a name="create-a-simple-web-application"></a>Tworzenie prostej aplikacji sieci Web
Utwórz aplikację sieci Web platformy Flask, która nasłuchuje na porcie 80 i zwraca wartość „Hello World!”.  W hello na tym samym katalogu, Utwórz plik hello *requirements.txt*.  Dodaj następujące hello i Zapisz zmiany:
```
Flask
```

Również utworzyć hello *app.py* i dodaj następujące hello:

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello():
    
    return 'Hello World!'

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=80)
```

## <a name="build-hello-image"></a>Utwórz obraz powitania
Uruchom hello `docker build` polecenia toocreate hello obrazu, który uruchamia aplikację sieci web. Otwórz okno programu PowerShell i przejdź zbyt*c:\temp\helloworldapp*. Uruchom następujące polecenie hello:

```bash
docker build -t helloworldapp .
```

To polecenie kompilacji hello nowy obraz przy użyciu instrukcji hello w Twojej plik Dockerfile, nazewnictwa (-t znakowanie) obraz powitania "helloworldapp". Tworzenie obrazu ściąga podstawowy obraz powitania w dół od centrum Docker i tworzy nowy obraz, który dodaje aplikację na podstawowy obraz powitania.  

Po zakończeniu wykonywania polecenia kompilacji hello Uruchom hello `docker images` polecenia toosee informacji na temat nowego obrazu hello:

```bash
$ docker images
    
REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              86838648aab6        2 minutes ago       194 MB
```

## <a name="run-hello-application-locally"></a>Uruchamianie aplikacji hello lokalnie
Sprawdź, czy aplikacja konteneryzowanych działa lokalnie przed wypychanie go hello kontenera rejestru.  

Uruchamianie aplikacji hello, mapowanie kontenera komputera port 4000 toohello ekspozycji port 80:

```bash
docker run -d -p 4000:80 --name my-web-site helloworldapp
```

*Nazwa* daje toohello nazwy, systemem kontenera (zamiast identyfikator kontenera hello).

Połącz toohello systemem kontenera.  Otwórz przeglądarkę sieci web toohello adres IP zwrócony przez port 4000, na przykład "http://localhost:4000". Powinny pojawić się hello pozycji "Witaj świecie!" Wyświetl w przeglądarce hello.

![Hello World!][hello-world]

toostop kontenera Uruchom:

```bash
docker stop my-web-site
```

Usuń kontener hello z komputerze deweloperskim:

```bash
docker rm my-web-site
```

## <a name="push-hello-image-toohello-container-registry"></a>Wypychanie hello obrazu toohello kontenera rejestru
Po upewnieniu się, że aplikacja hello jest uruchamiana na Docker, Wypchnij rejestru tooyour obraz powitania w rejestrze kontenera platformy Azure.

Uruchom `docker login` toolog w rejestrze kontenera tooyour z Twojej [poświadczenia rejestru](../container-registry/container-registry-authentication.md).

Witaj w poniższym przykładzie przekazuje hello Identyfikatora i hasła usługi Azure Active Directory [nazwy głównej usługi](../active-directory/active-directory-application-objects.md). Na przykład może przypisano rejestr tooyour główna usługi scenariusz automatyzacji.  Możesz również zalogować się za pomocą nazwy i hasła użytkownika rejestru.

```bash
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

Witaj następujące polecenie tworzy tag lub alias obraz powitania z rejestru tooyour w pełni kwalifikowana. W tym przykładzie miejsca hello obrazu w hello `samples` bałaganu tooavoid przestrzeni nazw w głównym hello hello rejestru.

```bash
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

Wypchnij hello obrazu tooyour kontenera rejestru:

```bash
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="package-hello-docker-image-with-yeoman"></a>Pakiet hello Docker obrazu za pomocą narzędzia Yeoman
Witaj zestawu SDK sieci szkieletowej usług dla systemu Linux zawiera [narzędzia Yeoman](http://yeoman.io/) generator kodu, który umożliwia łatwe toocreate aplikacji i Dodaj obraz kontenera. Można użyć narzędzia Yeoman toocreate o nazwie aplikacji o jeden kontener Docker *SimpleContainerApp*.

toocreate aplikacji kontenera usługi sieć szkieletowa Otwórz okno terminalu i uruchom `yo azuresfcontainer`.  

Nadaj nazwę aplikacji (na przykład „mojkontener”). 

Podaj adres URL hello hello kontener obrazu w rejestrze kontenera (na przykład, ""). 

Ten obraz ma obciążenia zdefiniowane punktu wejścia, dlatego trzeba tooexplicitly określać polecenia wejściowe (uruchamiane wewnątrz kontenera hello zachowa kontenera hello uruchomiona po uruchomieniu polecenia). 

Określ liczbę wystąpień jako „1”.

![Generator Yeoman usługi Service Fabric dla kontenerów][sf-yeoman]

## <a name="configure-port-mapping-and-container-repository-authentication"></a>Konfigurowanie mapowania portów i uwierzytelniania repozytorium kontenerów
Skonteneryzowana usługa wymaga punktu końcowego dla celów komunikacyjnych.  Teraz Dodaj hello protokół, port i typ tooan `Endpoint` w pliku ServiceManifest.xml hello. W tym artykule usługi hello konteneryzowanych nasłuchuje na porcie 4000: 

```xml
<Endpoint Name="myserviceTypeEndpoint" UriScheme="http" Port="4000" Protocol="http"/>
```
Zapewnianie hello `UriScheme` automatycznie rejestruje hello kontener punktu końcowego z hello usługi nazewnictwa sieci szkieletowej usług w celu odnajdywania. Pełna przykładowy plik ServiceManifest.xml znajduje się na końcu hello w tym artykule. 

Skonfiguruj mapowanie portów port kontenera do hosta hello, określając `PortBinding` zasad w `ContainerHostPolicies` pliku ApplicationManifest.xml hello.  W tym artykule `ContainerPort` to 80 (kontenera hello przedstawia portu 80, jak określono w hello plik Dockerfile) i `EndpointRef` jest "myserviceTypeEndpoint" (zdefiniowane w manifeście usługi hello hello punktu końcowego).  Przychodzące żądania usługi toohello na porcie 4000 są mapowane tooport 80 kontenera hello.  Jeśli Twoje kontenera musi tooauthenticate z prywatnym repozytorium, Dodaj `RepositoryCredentials`.  W tym artykule Dodaj hello nazwę konta i hasło dla hello myregistry.azurecr.io kontenera rejestru. 

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="myserviceTypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

## <a name="build-and-package-hello-service-fabric-application"></a>Kompilowanie i pakietu aplikacji usługi Service Fabric hello
Hello narzędzia usługi sieć szkieletowa Yeoman szablony obejmują skryptu kompilacji dla [Gradle](https://gradle.org/), który można użyć aplikacji hello toobuild z hello terminala. toobuild i pakietów hello aplikacji, uruchom następujące hello:

```bash
cd mycontainer
gradle
```

## <a name="deploy-hello-application"></a>Wdrażanie aplikacji hello
Po utworzeniu aplikacji hello można wdrożyć klaster lokalny toohello przy użyciu hello interfejsu wiersza polecenia usługi sieci szkieletowej.

Połącz toohello lokalnego klastra usługi sieć szkieletowa usług.

```bash
sfctl cluster select --endpoint http://localhost:19080
```

Użyj hello zainstalować skrypt toocopy szablonu hello aplikacji hello pakietu magazynu obrazu klastra toohello, Rejestracja typu aplikacji hello, i Utwórz wystąpienie aplikacji hello.

```bash
./install.sh
```

Otwórz przeglądarkę i przejdź tooService Eksploratora sieci szkieletowej w http://localhost: 19080/Explorer (localhost Zamień z hello prywatnego adresu IP hello maszyny Wirtualnej, jeśli przy użyciu Vagrant w systemie Mac OS X). Rozwiń węzeł aplikacji hello i należy pamiętać, że teraz wpis dla danego typu aplikacji i drugi dla hello pierwsze wystąpienie tego typu.

Połącz toohello systemem kontenera.  Otwórz przeglądarkę sieci web toohello adres IP zwrócony przez port 4000, na przykład "http://localhost:4000". Powinny pojawić się hello pozycji "Witaj świecie!" Wyświetl w przeglądarce hello.

![Hello World!][hello-world]

## <a name="clean-up"></a>Czyszczenie
Użyj skryptu Odinstaluj hello podane w hello wystąpienia aplikacji hello toodelete szablonu z hello lokalnego klastra projektowego i wyrejestrowywanie typu aplikacji hello.

```bash
./uninstall.sh
```

Po push hello obrazu toohello kontenera rejestru na komputerze projektowym można usunąć obrazu lokalne powitania:

```
docker rmi helloworldapp
docker rmi myregistry.azurecr.io/samples/helloworldapp
```

## <a name="complete-example-service-fabric-application-and-service-manifests"></a>Kompletny przykład aplikacji i manifestów usługi Service Fabric
Oto usługi pełną hello i manifestów aplikacji używane w tym artykule.

### <a name="servicemanifestxml"></a>ServiceManifest.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="myservicePkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is hello name of your ServiceType.
         hello UseImplicitHost attribute indicates this is a guest service. -->
    <StatelessServiceType ServiceTypeName="myserviceType" UseImplicitHost="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <!-- Follow this link for more information about deploying Windows containers 
      tooService Fabric: https://aka.ms/sfguestcontainers -->
      <ContainerHost>
        <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
        <Commands></Commands>
      </ContainerHost>
    </EntryPoint>
    <!-- Pass environment variables tooyour container: -->
    
    <EnvironmentVariables>
      <!--
      <EnvironmentVariable Name="VariableName" Value="VariableValue"/>
      -->
    </EnvironmentVariables>
    
  </CodePackage>

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which too
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="myserviceTypeEndpoint" UriScheme="http" Port="4000" Protocol="http"/>
    </Endpoints>
  </Resources>
</ServiceManifest>
```
### <a name="applicationmanifestxml"></a>ApplicationManifest.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest ApplicationTypeName="mycontainerType"
                     ApplicationTypeVersion="1.0.0"
                     xmlns="http://schemas.microsoft.com/2011/01/fabric"
                     xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <!-- Import hello ServiceManifest from hello ServicePackage. hello ServiceManifestName and ServiceManifestVersion 
       should match hello Name and Version attributes of hello ServiceManifest element defined in hello 
       ServiceManifest.xml file. -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="myservicePkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
    <Policies>
      <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="myserviceTypeEndpoint"/>
      </ContainerHostPolicies>
    </Policies>
  </ServiceManifestImport>
  <DefaultServices>
    <!-- hello section below creates instances of service types, when an instance of this 
         application type is created. You can also create one or more instances of service type using hello 
         ServiceFabric PowerShell module.
         
         hello attribute ServiceTypeName below must match hello name defined in hello imported ServiceManifest.xml file. -->
    <Service Name="myservice">
      <!-- On a local development cluster, set InstanceCount too1.  On a multi-node production 
      cluster, set InstanceCount too-1 for hello container service toorun on every node in 
      hello cluster.
      -->
      <StatelessService ServiceTypeName="myserviceType" InstanceCount="1">
        <SingletonPartition />
      </StatelessService>
    </Service>
  </DefaultServices>
</ApplicationManifest>
```
## <a name="adding-more-services-tooan-existing-application"></a>Dodawanie więcej usług tooan istniejącej aplikacji

wykonaj inną aplikację kontenera usługi tooan, utworzone za pomocą narzędzia yeoman, tooadd hello następujące kroki:

1. Zmień katalog główny toohello hello istniejącej aplikacji.  Na przykład `cd ~/YeomanSamples/MyApplication`, jeśli `MyApplication` to aplikacja hello utworzone przez narzędzia Yeoman.
2. Uruchom polecenie `yo azuresfcontainer:AddService`

<a id="manually"></a>


## <a name="configure-time-interval-before-container-is-force-terminated"></a>Konfigurowanie interwału czasu wymuszania przerwania działania kontenera

Przedział czasu dla toowait środowiska uruchomieniowego hello można skonfigurować przed usunięciem kontenera powitania po hello usunięcia usługi (lub Przenieś węzła tooanother) została uruchomiona. Konfigurowanie interwał czasu hello wysyła hello `docker stop <time in seconds>` polecenia toohello kontenera.   Aby uzyskać więcej informacji, zobacz [docker stop](https://docs.docker.com/engine/reference/commandline/stop/). toowait interwał czasu Hello jest określony w hello `Hosting` sekcji. Witaj następującego fragmentu manifestu klastra pokazuje, jak tooset hello oczekiwania interwał:

```xml
{
        "name": "Hosting",
        "parameters": [
          {
            "ContainerDeactivationTimeout": "10",
          ...
          }
        ]
}
```
Witaj domyślny interwał ustawiono too10 sekund. Ponieważ ta konfiguracja jest dynamiczny, config uaktualnić tylko na powitania klastra aktualizacje hello przekroczenia limitu czasu. 


## <a name="configure-hello-runtime-tooremove-unused-container-images"></a>Skonfiguruj tooremove środowiska uruchomieniowego hello kontenerem nieużywanych obrazów

Można skonfigurować tooremove klastra usługi sieć szkieletowa hello kontenerem nieużywanych obrazów z hello węzła. Ta konfiguracja pozwala przechwyceniem Jeśli zbyt wiele obrazów kontenera znajdują się w węźle hello toobe miejsca na dysku.  tooenable tej funkcji, hello aktualizacji `Hosting` sekcji w manifeście klastra hello pokazane na powitania po fragment kodu: 


```xml
{
        "name": "Hosting",
        "parameters": [
          {
            "PruneContainerImages": “True”,
            "ContainerImagesToSkip": "microsoft/windowsservercore|microsoft/nanoserver|…",
          ...
          }
        ]
} 
```

Do obrazów, które nie powinny być usuwane, można określić je w obszarze hello `ContainerImagesToSkip` parametru. 


## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o uruchamianiu [kontenerów w usłudze Service Fabric](service-fabric-containers-overview.md).
* Witaj odczytu [wdrażanie aplikacji .NET w kontenerze](service-fabric-host-app-in-a-container.md) samouczka.
* Dowiedz się więcej o hello sieci szkieletowej usług [cyklu życia aplikacji](service-fabric-application-lifecycle.md).
* Wyewidencjonowanie hello [przykłady kodu kontenera usługi sieć szkieletowa](https://github.com/Azure-Samples/service-fabric-dotnet-containers) w witrynie GitHub.

[hello-world]: ./media/service-fabric-get-started-containers-linux/HelloWorld.png
[sf-yeoman]: ./media/service-fabric-get-started-containers-linux/YoSF.png
