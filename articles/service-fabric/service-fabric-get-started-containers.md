---
title: "Tworzenie aplikacji kontenera usługi Azure Service Fabric | Microsoft Docs"
description: "Utwórz pierwszą aplikację kontenera systemu Windows w usłudze Azure Service Fabric.  Zbuduj obraz Docker za pomocą aplikacji w języku Python, wypchnij obraz do rejestru kontenerów, skompiluj i wdróż aplikację kontenera usługi Service Fabric."
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
ms.openlocfilehash: 025bde02b3f342ec3399d51819d1fa8a91f11374
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="create-your-first-service-fabric-container-application-on-windows"></a>Tworzenie pierwszej aplikacji kontenera usługi Service Fabric w systemie Windows
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started-containers.md)
> * [Linux](service-fabric-get-started-containers-linux.md)

Uruchomienie istniejącej aplikacji w kontenerze systemu Windows w klastrze usługi Service Fabric nie wymaga dokonywania żadnych zmian w aplikacji. W tym artykule przedstawiono proces tworzenia obrazu Docker zawierającego aplikację sieci Web w języku Python na platformie [Flask](http://flask.pocoo.org/) oraz wdrażania go w klastrze usługi Service Fabric.  Będziesz również udostępniać aplikację skonteneryzowaną za pomocą usługi [Azure Container Registry](/azure/container-registry/).  W tym artykule przyjęto założenie, że masz podstawową wiedzą dotyczącą platformy Docker. Aby uzyskać informacje dotyczące platformy Docker, przeczytaj artykuł [Docker Overview](https://docs.docker.com/engine/understanding-docker/) (Przegląd platformy Docker).

## <a name="prerequisites"></a>Wymagania wstępne
Komputer dewelopera z następującym oprogramowaniem:
* Program Visual Studio 2015 lub Visual Studio 2017.
* [Zestaw SDK usługi Service Fabric oraz narzędzia](service-fabric-get-started.md).
*  Program Docker dla systemu Windows.  [Pobierz program Docker CE dla systemu Windows (wersja stabilna)](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description). Po zainstalowaniu i uruchomieniu programu Docker kliknij prawym przyciskiem myszy jego ikonę na pasku zadań i wybierz pozycję **Switch to Windows containers** (Przełącz na kontenery systemu Windows). Jest to wymagane do uruchomienia obrazów Docker opartych na systemie Windows.

Klaster systemu Windows z co najmniej trzema węzłami działającymi w systemie Windows Server 2016 z kontenerami — [utwórz klaster](service-fabric-cluster-creation-via-portal.md) lub [wypróbuj bezpłatnie usługę Service Fabric](https://aka.ms/tryservicefabric).

Rejestr w usłudze Azure Container Registry — [utwórz rejestr kontenera](../container-registry/container-registry-get-started-portal.md) w subskrypcji platformy Azure.

## <a name="define-the-docker-container"></a>Definiowanie kontenera platformy Docker
Zbuduj obraz na podstawie [obrazu Python](https://hub.docker.com/_/python/) znajdującego się w usłudze Docker Hub.

Zdefiniuj kontener platformy Docker w pliku Dockerfile. Plik Dockerfile zawiera instrukcje dotyczące konfigurowania środowiska wewnątrz kontenera, ładowania aplikacji do uruchomienia i mapowania portów. Plik Dockerfile stanowi dane wejściowe dla polecenia `docker build`, za pomocą którego jest tworzony obraz.

Utwórz pusty katalog, a następnie utwórz plik *Dockerfile* (bez rozszerzenia). Dodaj następujący kod do pliku *Dockerfile* i zapisz zmiany:

```
# Use an official Python runtime as a base image
FROM python:2.7-windowsservercore

# Set the working directory to /app
WORKDIR /app

# Copy the current directory contents into the container at /app
ADD . /app

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt

# Make port 80 available to the world outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when the container launches
CMD ["python", "app.py"]
```

Przeczytaj artykuł [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) (Informacje o pliku Dockerfile), aby uzyskać więcej informacji.

## <a name="create-a-simple-web-application"></a>Tworzenie prostej aplikacji sieci Web
Utwórz aplikację sieci Web platformy Flask, która nasłuchuje na porcie 80 i zwraca wartość „Hello World!”.  W tym samym katalogu utwórz plik *requirements.txt*.  Dodaj następujący kod i zapisz zmiany:
```
Flask
```

Utwórz również plik *app.py* i dodaj następujący kod:

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
## <a name="build-the-image"></a>Tworzenie obrazu
Uruchom polecenie `docker build`, aby utworzyć obraz uruchamiający aplikację sieci Web. Otwórz okno programu PowerShell i przejdź do katalogu zawierającego plik Dockerfile. Uruchom następujące polecenie:

```
docker build -t helloworldapp .
```

To polecenie powoduje zbudowanie nowego obrazu zgodnie z instrukcjami z pliku Dockerfile i nadanie obrazowi nazwy „helloworldapp” (dzięki zastosowaniu parametru tagowania -t). Proces budowania obrazu powoduje pobranie obrazu podstawowego z usługi Docker Hub i utworzenie nowego obrazu z aplikacją dodaną do obrazu podstawowego.  

Po zakończeniu działania polecenia budowania uruchom polecenie `docker images`, aby wyświetlić informacje o nowym obrazie:

```
$ docker images

REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              8ce25f5d6a79        2 minutes ago       10.4 GB
```

## <a name="run-the-application-locally"></a>Uruchamianie aplikacji lokalnie
Przed wypchnięciem obrazu do rejestru kontenerów należy lokalnie sprawdzić jego działanie.  

Uruchom aplikację:

```
docker run -d --name my-web-site helloworldapp
```

Parametr *name* umożliwia nadanie nazwy działającemu kontenerowi (zamiast identyfikatora kontenera).

Po uruchomieniu kontenera znajdź jego adres IP, dzięki czemu będzie można połączyć się z działającym kontenerem za pomocą przeglądarki:
```
docker inspect -f "{{ .NetworkSettings.Networks.nat.IPAddress }}" my-web-site
```

Nawiąż połączenie z działającym kontenerem.  Otwórz przeglądarkę sieci Web i wpisz zwrócony adres IP, na przykład „http://172.31.194.61”. W przeglądarce powinien zostać wyświetlony nagłówek „Hello World!”.

Aby zatrzymać kontener, uruchom polecenie:

```
docker stop my-web-site
```

Usuń kontener z komputera dewelopera:

```
docker rm my-web-site
```

<a id="Push-Containers"></a>
## <a name="push-the-image-to-the-container-registry"></a>Wypychanie obrazu do rejestru kontenerów
Po sprawdzeniu, że kontener działa na komputerze dewelopera, wypchnij obraz do rejestru w usłudze Azure Container Registry.

Uruchom ``docker login``, aby zalogować się do rejestru kontenera za pomocą Twoich [poświadczeń rejestru](../container-registry/container-registry-authentication.md).

Poniższy przykład przekazuje identyfikator i hasło [nazwy głównej usługi](../active-directory/active-directory-application-objects.md) Azure Active Directory. Na przykład nazwę główną usługi można było przypisać do rejestru dla scenariusza automatyzacji. Możesz również zalogować się za pomocą nazwy i hasła użytkownika rejestru.

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

Następujące polecenie tworzy tag lub alias obrazu z w pełni kwalifikowaną ścieżką do Twojego rejestru. W tym przykładzie obraz jest umieszczany w przestrzeni nazw ```samples```, aby uniknąć zaśmiecania katalogu głównego rejestru.

```
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

Wypchnij obraz do rejestru kontenerów:

```
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="create-the-containerized-service-in-visual-studio"></a>Tworzenie konteneryzowanej usługi w programie Visual Studio
Zestaw SDK oraz narzędzia usługi Service Fabric udostępniają szablon usługi ułatwiający utworzenie konteneryzowanej aplikacji.

1. Uruchom program Visual Studio.  Wybierz kolejno pozycje **Plik** > **Nowy** > **Projekt**.
2. Wybierz pozycję **Aplikacja usługi Service Fabric**, nadaj jej nazwę „MyFirstContainer” i kliknij przycisk **OK**.
3. Z listy **szablonów usług** wybierz pozycję **Kontener gościa**.
4. W polu **Nazwa obrazu** wprowadź „myregistry.azurecr.io/samples/helloworldapp”. Jest to obraz wypchnięty do repozytorium kontenerów.
5. Nadaj nazwę usłudze i kliknij przycisk **OK**.

## <a name="configure-communication"></a>Konfigurowanie komunikacji
Konteneryzowana usługa wymaga punktu końcowego dla celów komunikacyjnych. Dodaj element `Endpoint` z protokołem, portem i typem do pliku ServiceManifest.xml. Na potrzeby tego artykułu konteneryzowana usługa nasłuchuje na porcie 8081.  W tym przykładzie jest używany stały port 8081.  Jeśli nie określono portu, zostanie wybrany losowy port z zakresu portów aplikacji.  

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="Guest1TypeEndpoint" UriScheme="http" Port="8081" Protocol="http"/>
  </Endpoints>
</Resources>
```

Definiując punkt końcowy, usługa Service Fabric publikuje punkt końcowy w usłudze Naming.  Inne usługi działające w klastrze mogą rozpoznać ten kontener.  Komunikację między kontenerami można również realizować za pomocą [odwrotnego serwera proxy](service-fabric-reverseproxy.md).  Aby zrealizować komunikację, należy podać port nasłuchujący HTTP odwrotnego serwera proxy i nazwę usług, z którymi chcesz się komunikować, jako zmienne środowiskowe.

## <a name="configure-and-set-environment-variables"></a>Konfigurowanie i ustawianie zmiennych środowiskowych
Zmienne środowiskowe można określić dla każdego pakietu kodu w manifeście usługi. Ta funkcja jest dostępna dla wszystkich usług niezależnie od tego, czy są one wdrażane jako kontenery, procesy, czy pliki wykonywalne gościa. Wartości zmiennych środowiskowych można przesłonić w manifeście aplikacji lub podać je podczas wdrażania jako parametry aplikacji.

Następujący fragment kodu XML manifestu usługi stanowi przykład sposobu określania zmiennych środowiskowych dla pakietu kodu:
```xml
<CodePackage Name="Code" Version="1.0.0">
  ...
  <EnvironmentVariables>
    <EnvironmentVariable Name="HttpGatewayPort" Value=""/>    
  </EnvironmentVariables>
</CodePackage>
```

Te zmienne środowiskowe można przesłonić w manifeście aplikacji:

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
  </EnvironmentOverrides>
  ...
</ServiceManifestImport>
```

## <a name="configure-container-port-to-host-port-mapping-and-container-to-container-discovery"></a>Konfigurowanie mapowania portów kontenera typu port do hosta i odnajdywania między kontenerami
Skonfiguruj port hosta używany do komunikacji z kontenerem. Powiązanie portu mapuje port, na którym nasłuchuje usługa wewnątrz kontenera, na port na hoście. Dodaj element `PortBinding` w elemencie `ContainerHostPolicies` pliku ApplicationManifest.xml.  W tym artykule wartość portu dla parametru `ContainerPort` to 80 (kontener uwidacznia port 80, jak określono w pliku Dockerfile), a wartością parametru `EndpointRef` jest „Guest1TypeEndpoint” (punkt końcowy zdefiniowany wcześniej w manifeście usługi).  Żądania przychodzące do usługi na porcie 8081 są mapowane na port 80 w kontenerze.

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
  </ContainerHostPolicies>
</Policies>
```

## <a name="configure-container-registry-authentication"></a>Konfigurowanie uwierzytelniania rejestru kontenerów
Skonfiguruj uwierzytelnianie rejestru kontenerów przez dodanie elementu `RepositoryCredentials` do elementu `ContainerHostPolicies` pliku ApplicationManifest.xml. Dodaj nazwę konta i hasło dla rejestru kontenerów myregistry.azurecr.io, dzięki czemu usługa będzie mogła pobrać obraz kontenera z repozytorium.

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

Zalecamy zaszyfrowanie hasła repozytorium przy użyciu certyfikatu szyfrowania wdrożonego na wszystkich węzłach klastra. Gdy usługa Service Fabric wdroży pakiet usług w klastrze, zaszyfrowany tekst zostanie odszyfrowany za pomocą certyfikatu szyfrowania.  Polecenie cmdlet Invoke-ServiceFabricEncryptText jest używane do utworzenia zaszyfrowanego tekstu dla hasła dodawanego do pliku ApplicationManifest.xml.

Poniższy skrypt tworzy nowy certyfikat z podpisem własnym i eksportuje go do pliku PFX.  Certyfikat jest importowany do istniejącego magazynu kluczy, a następnie wdrażany w klastrze usługi Service Fabric.

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

# Create a self signed cert, export to PFX file.
New-SelfSignedCertificate -Type DocumentEncryptionCert -KeyUsage DataEncipherment -Subject $subjectname -Provider 'Microsoft Enhanced Cryptographic Provider v1.0' `
| Export-PfxCertificate -FilePath $filepath -Password $certpwd

# Import the certificate to an existing key vault.  The key vault must be enabled for deployment.
$cer = Import-AzureKeyVaultCertificate -VaultName $vaultName -Name $certificateName -FilePath $filepath -Password $certpwd

Set-AzureRmKeyVaultAccessPolicy -VaultName $vaultName -ResourceGroupName $groupname -EnabledForDeployment

# Add the certificate to all the VMs in the cluster.
Add-AzureRmServiceFabricApplicationCertificate -ResourceGroupName $groupname -Name $clustername -SecretIdentifier $cer.SecretId
```
Zaszyfruj hasło przy użyciu polecenia cmdlet [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps).

```powershell
$text = "=P==/==/=8=/=+u4lyOB=+=nWzEeRfF="
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint $cer.Thumbprint -Text $text -StoreLocation Local -StoreName My
```

Zastąp hasło zaszyfrowanym tekstem zwróconym przez polecenie cmdlet [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) i ustaw właściwość `PasswordEncrypted` na wartość „true”.

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
System Windows obsługuje dwa tryby izolacji dla kontenerów: tryb procesu oraz tryb funkcji Hyper-V. W trybie izolacji procesu wszystkie kontenery działające na tym samym hoście współdzielą jądro z hostem. W trybie izolacji funkcji Hyper-V jądra są odizolowane dla każdego kontenera funkcji Hyper-V i hosta kontenera. Tryb izolacji można określić w elemencie `ContainerHostPolicies` pliku manifestu aplikacji. Tryby izolacji, które można określić, to `process`, `hyperv` i `default`. Wartością domyślną trybu izolacji jest `process` na hostach z systemem Windows Server i `hyperv` na hostach z systemem Windows 10. Poniższy fragment kodu przedstawia sposób określania trybu izolacji w pliku manifestu aplikacji.

```xml
<ContainerHostPolicies CodePackageRef="Code" Isolation="hyperv">
```

## <a name="configure-resource-governance"></a>Konfigurowanie zarządzania zasobami
[Zarządzanie zasobami](service-fabric-resource-governance.md) ogranicza zasoby, z których kontener może korzystać na hoście. Element `ResourceGovernancePolicy` określany w manifeście aplikacji służy do deklarowania limitów zasobów pakietu kodu usługi. Limity można ustawić dla następujących zasobów: Memory, MemorySwap, CpuShares (CPU — względna waga), MemoryReservationInMB, BlkioWeight (BlockIO — względna waga).  W tym przykładzie pakiet usług Guest1Pkg otrzymuje dostęp do jednego rdzenia w węzłach klastra, w których jest umieszczony.  Limity pamięci są bezwzględne, więc pakiet kodu jest ograniczony do 1024 MB pamięci (i ma rezerwację tej samej ilości ze wstępną gwarancją). Pakiety kodu (kontenery lub procesy) nie mogą przydzielać pamięci ponad ten limit. Podjęcie próby takiego przydzielenia spowoduje wyjątek braku pamięci. Aby wymuszanie limitu zasobów działało, wszystkie pakiety kodu w ramach pakietu usług powinny mieć określone limity pamięci.

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
  <Policies>
    <ServicePackageResourceGovernancePolicy CpuCores="1"/>
    <ResourceGovernancePolicy CodePackageRef="Code" MemoryInMB="1024"  />
  </Policies>
</ServiceManifestImport>
```

## <a name="deploy-the-container-application"></a>Wdrażanie aplikacji kontenera
Zapisz wszystkie zmiany i skompiluj aplikację. Aby opublikować aplikację, w Eksploratorze rozwiązań kliknij prawym przyciskiem myszy węzeł **MyFirstContainer** i wybierz pozycję **Publikuj**.

W obszarze **Punkt końcowy połączenia** wprowadź punkt końcowy zarządzania dla klastra.  Na przykład „containercluster.westus2.cloudapp.azure.com:19000”. Punkt końcowy połączenia klienta można znaleźć w bloku Przegląd klastra w witrynie [Azure Portal](https://portal.azure.com).

Kliknij przycisk **Opublikuj**.

[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) to oparte na sieci Web narzędzie do sprawdzania aplikacji i węzłów oraz zarządzania nimi w klastrze usługi Service Fabric. Otwórz przeglądarkę, przejdź do adresu http://containercluster.westus2.cloudapp.azure.com:19080/Explorer/ i wykonaj czynności wdrażania aplikacji.  Aplikacja zostanie wdrożona, ale pozostanie w stanie błędu do czasu pobrania obrazu na węzły klastra (co może zająć trochę czasu w zależności od rozmiaru obrazu): ![Błąd][1]

Aplikacja jest gotowa, gdy ma stan ```Ready```: ![Gotowa][2]

Otwórz przeglądarkę i przejdź do adresu http://containercluster.westus2.cloudapp.azure.com:8081. W przeglądarce powinien zostać wyświetlony nagłówek „Hello World!”.

## <a name="clean-up"></a>Czyszczenie
Jeśli podczas działania klastra nadal są naliczane opłaty, rozważ [usunięcie klastra](service-fabric-get-started-azure-cluster.md#remove-the-cluster).  [Klastry innych firm](http://tryazureservicefabric.westus.cloudapp.azure.com/) są automatycznie usuwane po kilku godzinach.

Po wypchnięciu obrazu do rejestru kontenerów można usunąć lokalny obraz z komputera dewelopera:

```
docker rmi helloworldapp
docker rmi myregistry.azurecr.io/samples/helloworldapp
```

## <a name="complete-example-service-fabric-application-and-service-manifests"></a>Kompletny przykład aplikacji i manifestów usługi Service Fabric
W tym miejscu przedstawiono kompletne manifesty usługi i aplikacji używane w tym artykule.

### <a name="servicemanifestxml"></a>ServiceManifest.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="Guest1Pkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is the name of your ServiceType.
         The UseImplicitHost attribute indicates this is a guest service. -->
    <StatelessServiceType ServiceTypeName="Guest1Type" UseImplicitHost="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <!-- Follow this link for more information about deploying Windows containers to Service Fabric: https://aka.ms/sfguestcontainers -->
      <ContainerHost>
        <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
      </ContainerHost>
    </EntryPoint>
    <!-- Pass environment variables to your container: -->    
    <EnvironmentVariables>
      <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
      <EnvironmentVariable Name="BackendServiceName" Value=""/>
    </EnvironmentVariables>

  </CodePackage>

  <!-- Config package is the contents of the Config directoy under PackageRoot that contains an
       independently-updateable and versioned set of custom configuration settings for your service. -->
  <ConfigPackage Name="Config" Version="1.0.0" />

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by the communication listener to obtain the port on which to
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
  <!-- Import the ServiceManifest from the ServicePackage. The ServiceManifestName and ServiceManifestVersion
       should match the Name and Version attributes of the ServiceManifest element defined in the
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
    <!-- The section below creates instances of service types, when an instance of this
         application type is created. You can also create one or more instances of service type using the
         ServiceFabric PowerShell module.

         The attribute ServiceTypeName below must match the name defined in the imported ServiceManifest.xml file. -->
    <Service Name="Guest1">
      <StatelessService ServiceTypeName="Guest1Type" InstanceCount="[Guest1_InstanceCount]">
        <SingletonPartition />
      </StatelessService>
    </Service>
  </DefaultServices>
</ApplicationManifest>
```

## <a name="configure-time-interval-before-container-is-force-terminated"></a>Konfigurowanie interwału czasu wymuszania przerwania działania kontenera

Możesz skonfigurować interwał czasu środowiska uruchomieniowego, po upływie którego kontener ma zostać usunięty po rozpoczęciu usuwania usługi (lub przenoszenia do innego węzła). Skonfigurowanie interwału czasu powoduje wysłanie polecenia `docker stop <time in seconds>` do kontenera.   Aby uzyskać więcej informacji, zobacz [docker stop](https://docs.docker.com/engine/reference/commandline/stop/). Interwał czasu oczekiwania jest określony w sekcji `Hosting`. W poniższym fragmencie manifestu klastra pokazano, jak ustawić interwał oczekiwania:

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
Domyślny interwał to 10 sekund. Ta konfiguracja jest dynamiczna, dlatego uaktualnienie samej konfiguracji w klastrze powoduje zaktualizowanie limitu czasu. 


## <a name="configure-the-runtime-to-remove-unused-container-images"></a>Konfigurowanie środowiska uruchomieniowego w celu usunięcia nieużywanych obrazów kontenerów

Możesz skonfigurować klaster usługi Service Fabric w celu usuwania nieużywanych obrazów kontenerów z węzła. Ta konfiguracja pozwala na ponowne przechwycenie miejsca na dysku w przypadku zbyt wielu obrazów kontenerów w węźle.  Aby włączyć tę funkcję, zaktualizuj sekcję `Hosting` w manifeście klastra, jak pokazano w poniższym fragmencie kodu: 


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

Jeśli nie chcesz usuwać pewnych obrazów, określ je przy użyciu parametru `ContainerImagesToSkip`. 



## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o uruchamianiu [kontenerów w usłudze Service Fabric](service-fabric-containers-overview.md).
* Zapoznaj się z samouczkiem [Deploy a .NET application in a container](service-fabric-host-app-in-a-container.md) (Wdrażanie aplikacji .NET w kontenerze).
* Uzyskaj informacje o [cyklu życia aplikacji](service-fabric-application-lifecycle.md) usługi Service Fabric.
* Sprawdź [przykłady kodu kontenera usługi Service Fabric](https://github.com/Azure-Samples/service-fabric-dotnet-containers) w witrynie GitHub.

[1]: ./media/service-fabric-get-started-containers/MyFirstContainerError.png
[2]: ./media/service-fabric-get-started-containers/MyFirstContainerReady.png
