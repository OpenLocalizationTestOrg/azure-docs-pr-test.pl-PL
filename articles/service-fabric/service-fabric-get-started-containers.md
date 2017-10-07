---
title: aaaCreate aplikacji kontenera platformy Azure Service Fabric | Dokumentacja firmy Microsoft
description: "Utwórz pierwszą aplikację kontenera systemu Windows w usłudze Azure Service Fabric.  Utwórz obraz Docker z aplikacji języka Python, push hello obrazu tooa kontenera rejestru, kompilacji i wdrażania aplikacji kontenera sieci szkieletowej usług."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: vturecek
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/18/2017
ms.author: ryanwi
ms.openlocfilehash: b79d3a41eb2da5f7791266588fe9ea7becb0e58f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-container-application-on-windows"></a>Tworzenie pierwszej aplikacji kontenera usługi Service Fabric w systemie Windows
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started-containers.md)
> * [Linux](service-fabric-get-started-containers-linux.md)

Systemem istniejącej aplikacji w kontenerze systemu Windows w klastrze usługi sieć szkieletowa nie wymaga żadnych zmian tooyour aplikacji. W tym artykule przedstawiono tworzenie obrazu Docker zawierający Python [Flask](http://flask.pocoo.org/) sieci web, aplikacji i wdrażania go tooa klastra sieci szkieletowej usług.  Będziesz również udostępniać aplikację skonteneryzowaną za pomocą usługi [Azure Container Registry](/azure/container-registry/).  W tym artykule przyjęto założenie, że masz podstawową wiedzą dotyczącą platformy Docker. Informacje na temat rozwiązania Docker za odczytywanie hello [omówienie Docker](https://docs.docker.com/engine/understanding-docker/).

## <a name="prerequisites"></a>Wymagania wstępne
Komputer dewelopera z następującym oprogramowaniem:
* Program Visual Studio 2015 lub Visual Studio 2017.
* [Zestaw SDK usługi Service Fabric oraz narzędzia](service-fabric-get-started.md).
*  Program Docker dla systemu Windows.  [Pobierz program Docker CE dla systemu Windows (wersja stabilna)](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description). Po instalacji i uruchamiania Docker, kliknij prawym przyciskiem myszy ikonę na pasku zadań hello i wybierz **przełącznika kontenery tooWindows**. Jest to wymagane toorun obrazy usługi Docker opartych na systemie Windows.

Klaster systemu Windows z co najmniej trzema węzłami działającymi w systemie Windows Server 2016 z kontenerami — [utwórz klaster](service-fabric-cluster-creation-via-portal.md) lub [wypróbuj bezpłatnie usługę Service Fabric](https://aka.ms/tryservicefabric).

Rejestr w usłudze Azure Container Registry — [utwórz rejestr kontenera](../container-registry/container-registry-get-started-portal.md) w subskrypcji platformy Azure.

## <a name="define-hello-docker-container"></a>Zdefiniuj hello kontenera Docker
Tworzenie obrazu opartego na powitania [obrazu Python](https://hub.docker.com/_/python/) znajduje się w Centrum Docker.

Zdefiniuj kontener platformy Docker w pliku Dockerfile. Plik Dockerfile Hello zawiera instrukcje dotyczące konfigurowania środowiska hello wewnątrz kontenera sieci, ładowania aplikacji hello ma toorun i mapowania portów. Hello plik Dockerfile jest toohello wejściowych hello `docker build` polecenia, które tworzy obraz powitania.

Utwórz pusty katalog i Utwórz plik hello *plik Dockerfile* (z bez rozszerzenia pliku). Dodaje hello zbyt*plik Dockerfile* i Zapisz zmiany:

```
# Use an official Python runtime as a base image
FROM python:2.7-windowsservercore

# Set hello working directory too/app
WORKDIR /app

# Copy hello current directory contents into hello container at /app
ADD . /app

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt

# Make port 80 available toohello world outside this container
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

<a id="Build-Containers"></a>
## <a name="build-hello-image"></a>Utwórz obraz powitania
Uruchom hello `docker build` polecenia toocreate hello obrazu, który uruchamia aplikację sieci web. Otwórz okno programu PowerShell i przejdź toohello katalog zawierający plik Dockerfile hello. Uruchom następujące polecenie hello:

```
docker build -t helloworldapp .
```

To polecenie kompilacji hello nowy obraz przy użyciu instrukcji hello w Twojej plik Dockerfile, nazewnictwa (-t znakowanie) obraz powitania "helloworldapp". Tworzenie obrazu ściąga podstawowy obraz powitania w dół od centrum Docker i tworzy nowy obraz, który dodaje aplikację na podstawowy obraz powitania.  

Po zakończeniu wykonywania polecenia kompilacji hello Uruchom hello `docker images` polecenia toosee informacji na temat nowego obrazu hello:

```
$ docker images

REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              8ce25f5d6a79        2 minutes ago       10.4 GB
```

## <a name="run-hello-application-locally"></a>Uruchamianie aplikacji hello lokalnie
Sprawdź obrazu lokalnie przed wypychanie go hello kontenera rejestru.  

Uruchamianie aplikacji hello:

```
docker run -d --name my-web-site helloworldapp
```

*Nazwa* daje toohello nazwy, systemem kontenera (zamiast identyfikator kontenera hello).

Po uruchomieniu kontenera hello, Znajdź adresu IP, dzięki czemu można łączyć tooyour systemem kontenera w przeglądarce:
```
docker inspect -f "{{ .NetworkSettings.Networks.nat.IPAddress }}" my-web-site
```

Połącz toohello systemem kontenera.  Otwórz przeglądarkę sieci web toohello adresu IP zwróconego, na przykład "http://172.31.194.61". Powinny pojawić się hello pozycji "Witaj świecie!" Wyświetl w przeglądarce hello.

toostop kontenera Uruchom:

```
docker stop my-web-site
```

Usuń kontener hello z komputerze deweloperskim:

```
docker rm my-web-site
```

<a id="Push-Containers"></a>
## <a name="push-hello-image-toohello-container-registry"></a>Wypychanie hello obrazu toohello kontenera rejestru
Po upewnieniu się, że kontenera hello jest uruchamiany na komputerze deweloperskim, Wypchnij rejestru tooyour obraz powitania w rejestrze kontenera platformy Azure.

Uruchom ``docker login`` toolog w rejestrze kontenera tooyour z Twojej [poświadczenia rejestru](../container-registry/container-registry-authentication.md).

Witaj w poniższym przykładzie przekazuje hello Identyfikatora i hasła usługi Azure Active Directory [nazwy głównej usługi](../active-directory/active-directory-application-objects.md). Na przykład może przypisano rejestr tooyour główna usługi scenariusz automatyzacji. Możesz również zalogować się za pomocą nazwy i hasła użytkownika rejestru.

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

Witaj następujące polecenie tworzy tag lub alias obraz powitania z rejestru tooyour w pełni kwalifikowana. W tym przykładzie miejsca hello obrazu w hello ```samples``` bałaganu tooavoid przestrzeni nazw w głównym hello hello rejestru.

```
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

Wypchnij hello obrazu tooyour kontenera rejestru:

```
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="create-hello-containerized-service-in-visual-studio"></a>Tworzenie usługi hello konteneryzowanych w programie Visual Studio
Witaj zestawu SDK usług sieci szkieletowej i narzędzia zapewniają toohelp szablonu usługi można utworzyć aplikację konteneryzowanych.

1. Uruchom program Visual Studio.  Wybierz kolejno pozycje **Plik** > **Nowy** > **Projekt**.
2. Wybierz pozycję **Aplikacja usługi Service Fabric**, nadaj jej nazwę „MyFirstContainer” i kliknij przycisk **OK**.
3. Wybierz **kontenera gościa** z listy hello **szablony usługi**.
4. W **nazwa obrazu** wprowadź "myregistry.azurecr.io/samples/helloworldapp" obraz powitania wypychana tooyour kontenera repozytorium.
5. Nadaj nazwę usłudze i kliknij przycisk **OK**.

## <a name="configure-communication"></a>Konfigurowanie komunikacji
punkt końcowy jest wymagane przez usługę Hello konteneryzowanych komunikacji. Dodaj `Endpoint` element z hello protokół, port i plik ServiceManifest.xml toohello typu. W tym artykule usługi hello konteneryzowanych nasłuchuje na porcie 8081.  W tym przykładzie jest używany stały port 8081.  Jeśli nie określono portu, losowego portu z zakresu portów aplikacji hello zostanie wybrany.  

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="Guest1TypeEndpoint" UriScheme="http" Port="8081" Protocol="http"/>
  </Endpoints>
</Resources>
```

Definiując punktu końcowego sieci szkieletowej usług publikuje hello toohello punktu końcowego usługi nazw.  Innych usług uruchomionych w klastrze hello można rozwiązać tego kontenera.  Można również wykonywać kontenerami komunikację z wykorzystaniem hello [odwrotny serwer proxy](service-fabric-reverseproxy.md).  Komunikacja odbywa się przez podanie port nasłuchujący hello zwrotny serwer proxy HTTP i nazwa hello hello usług, które ma być toocommunicate ze zmiennych środowiskowych.

## <a name="configure-and-set-environment-variables"></a>Konfigurowanie i ustawianie zmiennych środowiskowych
Zmienne środowiskowe można określić dla każdego pakietu kodu w hello manifestu usługi. Ta funkcja jest dostępna dla wszystkich usług niezależnie od tego, czy są one wdrażane jako kontenery, procesy, czy pliki wykonywalne gościa. Można zastąpić zmiennej środowiskowej wartości w aplikacji hello manifestu lub określić ich podczas wdrażania jako parametry aplikacji.

Witaj poniższy fragment XML manifestu usługi przedstawia przykładowy sposób zmiennych środowiskowych toospecify pakietu kodu:
```xml
<CodePackage Name="Code" Version="1.0.0">
  ...
  <EnvironmentVariables>
    <EnvironmentVariable Name="HttpGatewayPort" Value=""/>    
  </EnvironmentVariables>
</CodePackage>
```

Te zmienne środowiskowe może zostać zastąpiona w manifeście aplikacji hello:

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
  </EnvironmentOverrides>
  ...
</ServiceManifestImport>
```

## <a name="configure-container-port-to-host-port-mapping-and-container-to-container-discovery"></a>Konfigurowanie mapowania portów kontenera typu port do hosta i odnajdywania między kontenerami
Skonfiguruj toocommunicate port używany host hello kontenera. Powiązanie portu Hello mapuje hello portu, na które hello wewnątrz hello kontenera tooa portu na hoście hello nasłuchuje usługa. Dodaj `PortBinding` element `ContainerHostPolicies` element pliku ApplicationManifest.xml hello.  W tym artykule `ContainerPort` to 80 (kontenera hello przedstawia portu 80, jak określono w hello plik Dockerfile) i `EndpointRef` jest "Guest1TypeEndpoint" (punkt końcowy wcześniej zdefiniowany w manifeście usługi hello hello).  Przychodzące żądania usługi toohello na porcie 8081 są mapowane tooport 80 kontenera hello.

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
  </ContainerHostPolicies>
</Policies>
```

## <a name="configure-container-registry-authentication"></a>Konfigurowanie uwierzytelniania rejestru kontenerów
Skonfiguruj uwierzytelnianie rejestru kontenera przez dodanie `RepositoryCredentials` zbyt`ContainerHostPolicies` pliku ApplicationManifest.xml hello. Dodaj hello konto i hasło dla hello myregistry.azurecr.io kontenera rejestru, dzięki czemu hello usługi toodownload hello kontener obrazu z repozytorium hello.

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

Firma Microsoft zaleca szyfrowania hello repozytorium hasła przy użyciu certyfikatu szyfrowanie, która została wdrożona tooall węzłów klastra hello. Gdy usługa sieć szkieletowa wdraża hello usługi pakietu toohello klastra, certyfikat Szyfrowanie hello jest tekst zaszyfrowany hello toodecrypt używane.  polecenie cmdlet Invoke-ServiceFabricEncryptText Hello jest używany toocreate hello szyfrowania tekst hello hasła, które jest dodawane do pliku ApplicationManifest.xml toohello.

Witaj poniższy skrypt tworzy nowy certyfikat z podpisem własnym i eksportuje je tooa pliku PFX.  certyfikat Hello jest importowany do istniejący magazyn kluczy, a następnie wdrażana toohello klastra sieci szkieletowej usług.

```powershell
# Variables.
$certpwd = ConvertTo-SecureString -String "Pa$$word321!" -Force -AsPlainText
$filepath = "C:\MyCertificates\dataenciphermentcert.pfx"
$subjectname = "dataencipherment"
$vaultname = "mykeyvault"
$certificateName = "dataenciphermentcert"
$groupname="myclustergroup"
$clustername = "mycluster"

$subscriptionId = "subscription ID"

Login-AzureRmAccount

Select-AzureRmSubscription -SubscriptionId $subscriptionId

# Create a self signed cert, export tooPFX file.
New-SelfSignedCertificate -Type DocumentEncryptionCert -KeyUsage DataEncipherment -Subject $subjectname -Provider 'Microsoft Enhanced Cryptographic Provider v1.0' `
| Export-PfxCertificate -FilePath $filepath -Password $certpwd

# Import hello certificate tooan existing key vault.  hello key vault must be enabled for deployment.
$cer = Import-AzureKeyVaultCertificate -VaultName $vaultName -Name $certificateName -FilePath $filepath -Password $certpwd

Set-AzureRmKeyVaultAccessPolicy -VaultName $vaultName -ResourceGroupName $groupname -EnabledForDeployment

# Add hello certificate tooall hello VMs in hello cluster.
Add-AzureRmServiceFabricApplicationCertificate -ResourceGroupName $groupname -Name $clustername -SecretIdentifier $cer.SecretId
```
Szyfrowanie hasła hello przy użyciu hello [Invoke ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) polecenia cmdlet.

```powershell
$text = "=P==/==/=8=/=+u4lyOB=+=nWzEeRfF="
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint $cer.Thumbprint -Text $text -StoreLocation Local -StoreName My
```

Zamień hasło hello tekst zaszyfrowany hello zwrócony przez hello [Invoke ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) polecenia cmdlet i ustaw `PasswordEncrypted` zbyt "true".

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <RepositoryCredentials AccountName="myregistry" Password="MIIB6QYJKoZIhvcNAQcDoIIB2jCCAdYCAQAxggFRMIIBTQIBADA1MCExHzAdBgNVBAMMFnJ5YW53aWRhdGFlbmNpcGhlcm1lbnQCEFfyjOX/17S6RIoSjA6UZ1QwDQYJKoZIhvcNAQEHMAAEg
gEAS7oqxvoz8i6+8zULhDzFpBpOTLU+c2mhBdqXpkLwVfcmWUNA82rEWG57Vl1jZXe7J9BkW9ly4xhU8BbARkZHLEuKqg0saTrTHsMBQ6KMQDotSdU8m8Y2BR5Y100wRjvVx3y5+iNYuy/JmM
gSrNyyMQ/45HfMuVb5B4rwnuP8PAkXNT9VLbPeqAfxsMkYg+vGCDEtd8m+bX/7Xgp/kfwxymOuUCrq/YmSwe9QTG3pBri7Hq1K3zEpX4FH/7W2Zb4o3fBAQ+FuxH4nFjFNoYG29inL0bKEcTX
yNZNKrvhdM3n1Uk/8W2Hr62FQ33HgeFR1yxQjLsUu800PrYcR5tLfyTB8BgkqhkiG9w0BBwEwHQYJYIZIAWUDBAEqBBBybgM5NUV8BeetUbMR8mJhgFBrVSUsnp9B8RyebmtgU36dZiSObDsI
NtTvlzhk11LIlae/5kjPv95r3lw6DHmV4kXLwiCNlcWPYIWBGIuspwyG+28EWSrHmN7Dt2WqEWqeNQ==" PasswordEncrypted="true"/>
    <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
  </ContainerHostPolicies>
</Policies>
```

## <a name="configure-isolation-mode"></a>Konfigurowanie trybu izolacji
System Windows obsługuje dwa tryby izolacji dla kontenerów: tryb procesu oraz tryb funkcji Hyper-V. W trybie izolacji procesu hello wszystkich kontenerów hello systemem hello tego samego hosta maszyny udziału hello jądra z hostem hello. W trybie izolacji hello funkcji Hyper-V między każdego kontenera funkcji Hyper-V a hostem kontenera hello odizolowanych hello jądra. Tryb izolacji Hello jest określony w hello `ContainerHostPolicies` elementu w pliku manifestu aplikacji hello. Tryby izolacji Hello, które można określić są `process`, `hyperv`, i `default`. domyślny tryb izolacji Hello domyślnie przyjmowana jest zbyt`process` w systemie Windows Server obsługuje i domyślnie zbyt`hyperv` na hostach z systemem Windows 10. Hello poniższy fragment kodu przedstawia sposób hello trybu izolacji została określona w pliku manifestu aplikacji hello.

```xml
<ContainerHostPolicies CodePackageRef="Code" Isolation="hyperv">
```

## <a name="configure-resource-governance"></a>Konfigurowanie zarządzania zasobami
[Zarządzanie zasobów](service-fabric-resource-governance.md) ogranicza hello zasobów, które hello kontenera można użyć na hoście hello. Witaj `ResourceGovernancePolicy` element, który określono w manifeście aplikacji hello jest używane toodeclare limity zasobów pakietu kodu usługi. Limity zasobów można ustawić dla hello następujące zasoby: pamięci, MemorySwap, CpuShares (względną wagę Procesora), MemoryReservationInMB, BlkioWeight (BlockIO względną wagę).  W tym przykładzie pakiet usługi Guest1Pkg pobiera jeden rdzeń w węzłach klastra hello, gdzie jest umieszczony.  Limity pamięci są bezwzględne, więc hello pakietu kodu jest ograniczona too1024 MB pamięci (i elastyczne gwarancji zastrzeżenia hello sam). Pakiety kodu (kontenery lub procesów) nie są możliwe tooallocate, który więcej pamięci niż ten limit i podjęto toodo tak powoduje wygenerowanie wyjątku braku pamięci. Toowork wymuszania limit zasobów wszystkie pakiety kodu w ramach pakietu usługi powinny mieć określone limity pamięci.

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
  <Policies>
    <ServicePackageResourceGovernancePolicy CpuCores="1"/>
    <ResourceGovernancePolicy CodePackageRef="Code" MemoryInMB="1024"  />
  </Policies>
</ServiceManifestImport>
```

## <a name="deploy-hello-container-application"></a>Wdrażanie aplikacji kontenera hello
Zapisz wszystkie zmiany i tworzenia aplikacji hello. toopublish aplikacji, kliknij prawym przyciskiem myszy **MyFirstContainer** w Eksploratorze rozwiązań i wybierz **publikowania**.

W **punktu końcowego połączenia**, wprowadź hello punkt końcowy zarządzania dla klastra hello.  Na przykład „containercluster.westus2.cloudapp.azure.com:19000”. Połączenie klienta hello można znaleźć punkt końcowy w bloku omówienie hello klastra w hello [portalu Azure](https://portal.azure.com).

Kliknij przycisk **Opublikuj**.

[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) to oparte na sieci Web narzędzie do sprawdzania aplikacji i węzłów oraz zarządzania nimi w klastrze usługi Service Fabric. Otwórz przeglądarkę i przejdź toohttp://containercluster.westus2.cloudapp.azure.com:19080/Explorer/wykonaj wdrożenie aplikacji hello.  Aplikacja Hello wdraża, ale jest w stanie błędu, dopóki obraz powitania jest pobierany w węzłach klastra hello (które może zająć trochę czasu, w zależności od rozmiaru obrazu hello): ![błąd][1]

Aplikacja Hello jest gotowa, gdy jest on w ```Ready``` stanu: ![gotowe][2]

Otwórz przeglądarkę i przejdź toohttp://containercluster.westus2.cloudapp.azure.com:8081. Powinny pojawić się hello pozycji "Witaj świecie!" Wyświetl w przeglądarce hello.

## <a name="clean-up"></a>Czyszczenie
Możesz kontynuować tooincur opłaty za klaster hello jest uruchomiona, należy wziąć pod uwagę [Usuwanie klastra](service-fabric-get-started-azure-cluster.md#remove-the-cluster).  [Klastry innych firm](http://tryazureservicefabric.westus.cloudapp.azure.com/) są automatycznie usuwane po kilku godzinach.

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
<ServiceManifest Name="Guest1Pkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is hello name of your ServiceType.
         hello UseImplicitHost attribute indicates this is a guest service. -->
    <StatelessServiceType ServiceTypeName="Guest1Type" UseImplicitHost="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <!-- Follow this link for more information about deploying Windows containers tooService Fabric: https://aka.ms/sfguestcontainers -->
      <ContainerHost>
        <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
      </ContainerHost>
    </EntryPoint>
    <!-- Pass environment variables tooyour container: -->    
    <EnvironmentVariables>
      <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
      <EnvironmentVariable Name="BackendServiceName" Value=""/>
    </EnvironmentVariables>

  </CodePackage>

  <!-- Config package is hello contents of hello Config directoy under PackageRoot that contains an
       independently-updateable and versioned set of custom configuration settings for your service. -->
  <ConfigPackage Name="Config" Version="1.0.0" />

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which to
           listen. Please note that if your service is partitioned, this port is shared with
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="Guest1TypeEndpoint" UriScheme="http" Port="8081" Protocol="http"/>
    </Endpoints>
  </Resources>
</ServiceManifest>
```
### <a name="applicationmanifestxml"></a>ApplicationManifest.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest ApplicationTypeName="MyFirstContainerType"
                     ApplicationTypeVersion="1.0.0"
                     xmlns="http://schemas.microsoft.com/2011/01/fabric"
                     xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Parameters>
    <Parameter Name="Guest1_InstanceCount" DefaultValue="-1" />
  </Parameters>
  <!-- Import hello ServiceManifest from hello ServicePackage. hello ServiceManifestName and ServiceManifestVersion
       should match hello Name and Version attributes of hello ServiceManifest element defined in the
       ServiceManifest.xml file. -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentOverrides CodePackageRef="FrontendService.Code">
      <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
    </EnvironmentOverrides>
    <ConfigOverrides />
    <Policies>
      <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="MIIB6QYJKoZIhvcNAQcDoIIB2jCCAdYCAQAxggFRMIIBTQIBADA1MCExHzAdBgNVBAMMFnJ5YW53aWRhdGFlbmNpcGhlcm1lbnQCEFfyjOX/17S6RIoSjA6UZ1QwDQYJKoZIhvcNAQEHMAAEg
gEAS7oqxvoz8i6+8zULhDzFpBpOTLU+c2mhBdqXpkLwVfcmWUNA82rEWG57Vl1jZXe7J9BkW9ly4xhU8BbARkZHLEuKqg0saTrTHsMBQ6KMQDotSdU8m8Y2BR5Y100wRjvVx3y5+iNYuy/JmM
gSrNyyMQ/45HfMuVb5B4rwnuP8PAkXNT9VLbPeqAfxsMkYg+vGCDEtd8m+bX/7Xgp/kfwxymOuUCrq/YmSwe9QTG3pBri7Hq1K3zEpX4FH/7W2Zb4o3fBAQ+FuxH4nFjFNoYG29inL0bKEcTX
yNZNKrvhdM3n1Uk/8W2Hr62FQ33HgeFR1yxQjLsUu800PrYcR5tLfyTB8BgkqhkiG9w0BBwEwHQYJYIZIAWUDBAEqBBBybgM5NUV8BeetUbMR8mJhgFBrVSUsnp9B8RyebmtgU36dZiSObDsI
NtTvlzhk11LIlae/5kjPv95r3lw6DHmV4kXLwiCNlcWPYIWBGIuspwyG+28EWSrHmN7Dt2WqEWqeNQ==" PasswordEncrypted="true"/>
        <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
      </ContainerHostPolicies>
      <ServicePackageResourceGovernancePolicy CpuCores="1"/>
      <ResourceGovernancePolicy CodePackageRef="Code" MemoryInMB="1024"  />
    </Policies>
  </ServiceManifestImport>
  <DefaultServices>
    <!-- hello section below creates instances of service types, when an instance of this
         application type is created. You can also create one or more instances of service type using the
         ServiceFabric PowerShell module.

         hello attribute ServiceTypeName below must match hello name defined in hello imported ServiceManifest.xml file. -->
    <Service Name="Guest1">
      <StatelessService ServiceTypeName="Guest1Type" InstanceCount="[Guest1_InstanceCount]">
        <SingletonPartition />
      </StatelessService>
    </Service>
  </DefaultServices>
</ApplicationManifest>
```

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

[1]: ./media/service-fabric-get-started-containers/MyFirstContainerError.png
[2]: ./media/service-fabric-get-started-containers/MyFirstContainerReady.png
