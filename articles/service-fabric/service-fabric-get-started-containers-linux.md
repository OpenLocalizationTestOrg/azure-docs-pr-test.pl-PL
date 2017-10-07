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
# <a name="create-your-first-service-fabric-container-application-on-linux"></a><span data-ttu-id="1f949-104">Tworzenie pierwszej aplikacji kontenera usługi Service Fabric w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="1f949-104">Create your first Service Fabric container application on Linux</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1f949-105">Windows</span><span class="sxs-lookup"><span data-stu-id="1f949-105">Windows</span></span>](service-fabric-get-started-containers.md)
> * [<span data-ttu-id="1f949-106">Linux</span><span class="sxs-lookup"><span data-stu-id="1f949-106">Linux</span></span>](service-fabric-get-started-containers-linux.md)

<span data-ttu-id="1f949-107">Systemem istniejącej aplikacji w kontenerze systemu Linux w klastrze usługi sieć szkieletowa nie wymaga żadnych zmian tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1f949-107">Running an existing application in a Linux container on a Service Fabric cluster doesn't require any changes tooyour application.</span></span> <span data-ttu-id="1f949-108">W tym artykule przedstawiono tworzenie obrazu Docker zawierający Python [Flask](http://flask.pocoo.org/) sieci web, aplikacji i wdrażania go tooa klastra sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="1f949-108">This article walks you through creating a Docker image containing a Python [Flask](http://flask.pocoo.org/) web application and deploying it tooa Service Fabric cluster.</span></span>  <span data-ttu-id="1f949-109">Będziesz również udostępniać aplikację skonteneryzowaną za pomocą usługi [Azure Container Registry](/azure/container-registry/).</span><span class="sxs-lookup"><span data-stu-id="1f949-109">You will also share your containerized application through [Azure Container Registry](/azure/container-registry/).</span></span>  <span data-ttu-id="1f949-110">W tym artykule przyjęto założenie, że masz podstawową wiedzą dotyczącą platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="1f949-110">This article assumes a basic understanding of Docker.</span></span> <span data-ttu-id="1f949-111">Informacje na temat rozwiązania Docker za odczytywanie hello [omówienie Docker](https://docs.docker.com/engine/understanding-docker/).</span><span class="sxs-lookup"><span data-stu-id="1f949-111">You can learn about Docker by reading hello [Docker Overview](https://docs.docker.com/engine/understanding-docker/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1f949-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1f949-112">Prerequisites</span></span>
* <span data-ttu-id="1f949-113">Komputer dewelopera z następującym oprogramowaniem:</span><span class="sxs-lookup"><span data-stu-id="1f949-113">A development computer running:</span></span>
  * <span data-ttu-id="1f949-114">[Zestaw SDK usługi Service Fabric oraz narzędzia](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="1f949-114">[Service Fabric SDK and tools](service-fabric-get-started-linux.md).</span></span>
  * <span data-ttu-id="1f949-115">[Docker CE dla systemu Linux](https://docs.docker.com/engine/installation/#prior-releases).</span><span class="sxs-lookup"><span data-stu-id="1f949-115">[Docker CE for Linux](https://docs.docker.com/engine/installation/#prior-releases).</span></span> 
  * [<span data-ttu-id="1f949-116">Interfejs wiersza polecenia usługi Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1f949-116">Service Fabric CLI</span></span>](service-fabric-cli.md)

* <span data-ttu-id="1f949-117">Rejestr w usłudze Azure Container Registry — [utwórz rejestr kontenera](../container-registry/container-registry-get-started-portal.md) w subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1f949-117">A registry in Azure Container Registry - [Create a container registry](../container-registry/container-registry-get-started-portal.md) in your Azure subscription.</span></span> 

## <a name="define-hello-docker-container"></a><span data-ttu-id="1f949-118">Zdefiniuj hello kontenera Docker</span><span class="sxs-lookup"><span data-stu-id="1f949-118">Define hello Docker container</span></span>
<span data-ttu-id="1f949-119">Tworzenie obrazu opartego na powitania [obrazu Python](https://hub.docker.com/_/python/) znajduje się w Centrum Docker.</span><span class="sxs-lookup"><span data-stu-id="1f949-119">Build an image based on hello [Python image](https://hub.docker.com/_/python/) located on Docker Hub.</span></span> 

<span data-ttu-id="1f949-120">Zdefiniuj kontener platformy Docker w pliku Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="1f949-120">Define your Docker container in a Dockerfile.</span></span> <span data-ttu-id="1f949-121">Plik Dockerfile Hello zawiera instrukcje dotyczące konfigurowania środowiska hello wewnątrz kontenera sieci, ładowania aplikacji hello ma toorun i mapowania portów.</span><span class="sxs-lookup"><span data-stu-id="1f949-121">hello Dockerfile contains instructions for setting up hello environment inside your container, loading hello application you want toorun, and mapping ports.</span></span> <span data-ttu-id="1f949-122">Hello plik Dockerfile jest toohello wejściowych hello `docker build` polecenia, które tworzy obraz powitania.</span><span class="sxs-lookup"><span data-stu-id="1f949-122">hello Dockerfile is hello input toohello `docker build` command, which creates hello image.</span></span> 

<span data-ttu-id="1f949-123">Utwórz pusty katalog i Utwórz plik hello *plik Dockerfile* (z bez rozszerzenia pliku).</span><span class="sxs-lookup"><span data-stu-id="1f949-123">Create an empty directory and create hello file *Dockerfile* (with no file extension).</span></span> <span data-ttu-id="1f949-124">Dodaje hello zbyt*plik Dockerfile* i Zapisz zmiany:</span><span class="sxs-lookup"><span data-stu-id="1f949-124">Add hello following too*Dockerfile* and save your changes:</span></span>

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

<span data-ttu-id="1f949-125">Witaj odczytu [odwołania plik Dockerfile](https://docs.docker.com/engine/reference/builder/) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="1f949-125">Read hello [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) for more information.</span></span>

## <a name="create-a-simple-web-application"></a><span data-ttu-id="1f949-126">Tworzenie prostej aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="1f949-126">Create a simple web application</span></span>
<span data-ttu-id="1f949-127">Utwórz aplikację sieci Web platformy Flask, która nasłuchuje na porcie 80 i zwraca wartość „Hello World!”.</span><span class="sxs-lookup"><span data-stu-id="1f949-127">Create a Flask web application listening on port 80 that returns "Hello World!".</span></span>  <span data-ttu-id="1f949-128">W hello na tym samym katalogu, Utwórz plik hello *requirements.txt*.</span><span class="sxs-lookup"><span data-stu-id="1f949-128">In hello same directory, create hello file *requirements.txt*.</span></span>  <span data-ttu-id="1f949-129">Dodaj następujące hello i Zapisz zmiany:</span><span class="sxs-lookup"><span data-stu-id="1f949-129">Add hello following and save your changes:</span></span>
```
Flask
```

<span data-ttu-id="1f949-130">Również utworzyć hello *app.py* i dodaj następujące hello:</span><span class="sxs-lookup"><span data-stu-id="1f949-130">Also create hello *app.py* file and add hello following:</span></span>

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello():
    
    return 'Hello World!'

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=80)
```

## <a name="build-hello-image"></a><span data-ttu-id="1f949-131">Utwórz obraz powitania</span><span class="sxs-lookup"><span data-stu-id="1f949-131">Build hello image</span></span>
<span data-ttu-id="1f949-132">Uruchom hello `docker build` polecenia toocreate hello obrazu, który uruchamia aplikację sieci web.</span><span class="sxs-lookup"><span data-stu-id="1f949-132">Run hello `docker build` command toocreate hello image that runs your web application.</span></span> <span data-ttu-id="1f949-133">Otwórz okno programu PowerShell i przejdź zbyt*c:\temp\helloworldapp*.</span><span class="sxs-lookup"><span data-stu-id="1f949-133">Open a PowerShell window and navigate too*c:\temp\helloworldapp*.</span></span> <span data-ttu-id="1f949-134">Uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="1f949-134">Run hello following command:</span></span>

```bash
docker build -t helloworldapp .
```

<span data-ttu-id="1f949-135">To polecenie kompilacji hello nowy obraz przy użyciu instrukcji hello w Twojej plik Dockerfile, nazewnictwa (-t znakowanie) obraz powitania "helloworldapp".</span><span class="sxs-lookup"><span data-stu-id="1f949-135">This command builds hello new image using hello instructions in your Dockerfile, naming (-t tagging) hello image "helloworldapp".</span></span> <span data-ttu-id="1f949-136">Tworzenie obrazu ściąga podstawowy obraz powitania w dół od centrum Docker i tworzy nowy obraz, który dodaje aplikację na podstawowy obraz powitania.</span><span class="sxs-lookup"><span data-stu-id="1f949-136">Building an image pulls hello base image down from Docker Hub and creates a new image that adds your application on top of hello base image.</span></span>  

<span data-ttu-id="1f949-137">Po zakończeniu wykonywania polecenia kompilacji hello Uruchom hello `docker images` polecenia toosee informacji na temat nowego obrazu hello:</span><span class="sxs-lookup"><span data-stu-id="1f949-137">Once hello build command completes, run hello `docker images` command toosee information on hello new image:</span></span>

```bash
$ docker images
    
REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              86838648aab6        2 minutes ago       194 MB
```

## <a name="run-hello-application-locally"></a><span data-ttu-id="1f949-138">Uruchamianie aplikacji hello lokalnie</span><span class="sxs-lookup"><span data-stu-id="1f949-138">Run hello application locally</span></span>
<span data-ttu-id="1f949-139">Sprawdź, czy aplikacja konteneryzowanych działa lokalnie przed wypychanie go hello kontenera rejestru.</span><span class="sxs-lookup"><span data-stu-id="1f949-139">Verify that your containerized application runs locally before pushing it hello container registry.</span></span>  

<span data-ttu-id="1f949-140">Uruchamianie aplikacji hello, mapowanie kontenera komputera port 4000 toohello ekspozycji port 80:</span><span class="sxs-lookup"><span data-stu-id="1f949-140">Run hello application, mapping your computer's port 4000 toohello container's exposed port 80:</span></span>

```bash
docker run -d -p 4000:80 --name my-web-site helloworldapp
```

<span data-ttu-id="1f949-141">*Nazwa* daje toohello nazwy, systemem kontenera (zamiast identyfikator kontenera hello).</span><span class="sxs-lookup"><span data-stu-id="1f949-141">*name* gives a name toohello running container (instead of hello container ID).</span></span>

<span data-ttu-id="1f949-142">Połącz toohello systemem kontenera.</span><span class="sxs-lookup"><span data-stu-id="1f949-142">Connect toohello running container.</span></span>  <span data-ttu-id="1f949-143">Otwórz przeglądarkę sieci web toohello adres IP zwrócony przez port 4000, na przykład "http://localhost:4000".</span><span class="sxs-lookup"><span data-stu-id="1f949-143">Open a web browser pointing toohello IP address returned on port 4000, for example "http://localhost:4000".</span></span> <span data-ttu-id="1f949-144">Powinny pojawić się hello pozycji "Witaj świecie!"</span><span class="sxs-lookup"><span data-stu-id="1f949-144">You should see hello heading "Hello World!"</span></span> <span data-ttu-id="1f949-145">Wyświetl w przeglądarce hello.</span><span class="sxs-lookup"><span data-stu-id="1f949-145">display in hello browser.</span></span>

![Hello World!][hello-world]

<span data-ttu-id="1f949-147">toostop kontenera Uruchom:</span><span class="sxs-lookup"><span data-stu-id="1f949-147">toostop your container, run:</span></span>

```bash
docker stop my-web-site
```

<span data-ttu-id="1f949-148">Usuń kontener hello z komputerze deweloperskim:</span><span class="sxs-lookup"><span data-stu-id="1f949-148">Delete hello container from your development machine:</span></span>

```bash
docker rm my-web-site
```

## <a name="push-hello-image-toohello-container-registry"></a><span data-ttu-id="1f949-149">Wypychanie hello obrazu toohello kontenera rejestru</span><span class="sxs-lookup"><span data-stu-id="1f949-149">Push hello image toohello container registry</span></span>
<span data-ttu-id="1f949-150">Po upewnieniu się, że aplikacja hello jest uruchamiana na Docker, Wypchnij rejestru tooyour obraz powitania w rejestrze kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1f949-150">After you verify that hello application runs in Docker, push hello image tooyour registry in Azure Container Registry.</span></span>

<span data-ttu-id="1f949-151">Uruchom `docker login` toolog w rejestrze kontenera tooyour z Twojej [poświadczenia rejestru](../container-registry/container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="1f949-151">Run `docker login` toolog in tooyour container registry with your [registry credentials](../container-registry/container-registry-authentication.md).</span></span>

<span data-ttu-id="1f949-152">Witaj w poniższym przykładzie przekazuje hello Identyfikatora i hasła usługi Azure Active Directory [nazwy głównej usługi](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="1f949-152">hello following example passes hello ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span></span> <span data-ttu-id="1f949-153">Na przykład może przypisano rejestr tooyour główna usługi scenariusz automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="1f949-153">For example, you might have assigned a service principal tooyour registry for an automation scenario.</span></span>  <span data-ttu-id="1f949-154">Możesz również zalogować się za pomocą nazwy i hasła użytkownika rejestru.</span><span class="sxs-lookup"><span data-stu-id="1f949-154">Or, you could login using your registry username and password.</span></span>

```bash
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="1f949-155">Witaj następujące polecenie tworzy tag lub alias obraz powitania z rejestru tooyour w pełni kwalifikowana.</span><span class="sxs-lookup"><span data-stu-id="1f949-155">hello following command creates a tag, or alias, of hello image, with a fully qualified path tooyour registry.</span></span> <span data-ttu-id="1f949-156">W tym przykładzie miejsca hello obrazu w hello `samples` bałaganu tooavoid przestrzeni nazw w głównym hello hello rejestru.</span><span class="sxs-lookup"><span data-stu-id="1f949-156">This example places hello image in hello `samples` namespace tooavoid clutter in hello root of hello registry.</span></span>

```bash
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

<span data-ttu-id="1f949-157">Wypchnij hello obrazu tooyour kontenera rejestru:</span><span class="sxs-lookup"><span data-stu-id="1f949-157">Push hello image tooyour container registry:</span></span>

```bash
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="package-hello-docker-image-with-yeoman"></a><span data-ttu-id="1f949-158">Pakiet hello Docker obrazu za pomocą narzędzia Yeoman</span><span class="sxs-lookup"><span data-stu-id="1f949-158">Package hello Docker image with Yeoman</span></span>
<span data-ttu-id="1f949-159">Witaj zestawu SDK sieci szkieletowej usług dla systemu Linux zawiera [narzędzia Yeoman](http://yeoman.io/) generator kodu, który umożliwia łatwe toocreate aplikacji i Dodaj obraz kontenera.</span><span class="sxs-lookup"><span data-stu-id="1f949-159">hello Service Fabric SDK for Linux includes a [Yeoman](http://yeoman.io/) generator that makes it easy toocreate your application and add a container image.</span></span> <span data-ttu-id="1f949-160">Można użyć narzędzia Yeoman toocreate o nazwie aplikacji o jeden kontener Docker *SimpleContainerApp*.</span><span class="sxs-lookup"><span data-stu-id="1f949-160">Let's use Yeoman toocreate an application with a single Docker container called *SimpleContainerApp*.</span></span>

<span data-ttu-id="1f949-161">toocreate aplikacji kontenera usługi sieć szkieletowa Otwórz okno terminalu i uruchom `yo azuresfcontainer`.</span><span class="sxs-lookup"><span data-stu-id="1f949-161">toocreate a Service Fabric container application, open a terminal window and run `yo azuresfcontainer`.</span></span>  

<span data-ttu-id="1f949-162">Nadaj nazwę aplikacji (na przykład „mojkontener”).</span><span class="sxs-lookup"><span data-stu-id="1f949-162">Name your application (for example, "mycontainer").</span></span> 

<span data-ttu-id="1f949-163">Podaj adres URL hello hello kontener obrazu w rejestrze kontenera (na przykład, "").</span><span class="sxs-lookup"><span data-stu-id="1f949-163">Provide hello URL for hello container image in a container registry (for example, "").</span></span> 

<span data-ttu-id="1f949-164">Ten obraz ma obciążenia zdefiniowane punktu wejścia, dlatego trzeba tooexplicitly określać polecenia wejściowe (uruchamiane wewnątrz kontenera hello zachowa kontenera hello uruchomiona po uruchomieniu polecenia).</span><span class="sxs-lookup"><span data-stu-id="1f949-164">This image has a workload entry-point defined, so need tooexplicitly specify input commands (commands run inside hello container, which will keep hello container running after startup).</span></span> 

<span data-ttu-id="1f949-165">Określ liczbę wystąpień jako „1”.</span><span class="sxs-lookup"><span data-stu-id="1f949-165">Specify an instance count of "1".</span></span>

![Generator Yeoman usługi Service Fabric dla kontenerów][sf-yeoman]

## <a name="configure-port-mapping-and-container-repository-authentication"></a><span data-ttu-id="1f949-167">Konfigurowanie mapowania portów i uwierzytelniania repozytorium kontenerów</span><span class="sxs-lookup"><span data-stu-id="1f949-167">Configure port mapping and container repository authentication</span></span>
<span data-ttu-id="1f949-168">Skonteneryzowana usługa wymaga punktu końcowego dla celów komunikacyjnych.</span><span class="sxs-lookup"><span data-stu-id="1f949-168">Your containerized service needs an endpoint for communication.</span></span>  <span data-ttu-id="1f949-169">Teraz Dodaj hello protokół, port i typ tooan `Endpoint` w pliku ServiceManifest.xml hello.</span><span class="sxs-lookup"><span data-stu-id="1f949-169">Now add hello protocol, port, and type tooan `Endpoint` in hello ServiceManifest.xml file.</span></span> <span data-ttu-id="1f949-170">W tym artykule usługi hello konteneryzowanych nasłuchuje na porcie 4000:</span><span class="sxs-lookup"><span data-stu-id="1f949-170">For this article, hello containerized service listens on port 4000:</span></span> 

```xml
<Endpoint Name="myserviceTypeEndpoint" UriScheme="http" Port="4000" Protocol="http"/>
```
<span data-ttu-id="1f949-171">Zapewnianie hello `UriScheme` automatycznie rejestruje hello kontener punktu końcowego z hello usługi nazewnictwa sieci szkieletowej usług w celu odnajdywania.</span><span class="sxs-lookup"><span data-stu-id="1f949-171">Providing hello `UriScheme` automatically registers hello container endpoint with hello Service Fabric Naming service for discoverability.</span></span> <span data-ttu-id="1f949-172">Pełna przykładowy plik ServiceManifest.xml znajduje się na końcu hello w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="1f949-172">A full ServiceManifest.xml example file is provided at hello end of this article.</span></span> 

<span data-ttu-id="1f949-173">Skonfiguruj mapowanie portów port kontenera do hosta hello, określając `PortBinding` zasad w `ContainerHostPolicies` pliku ApplicationManifest.xml hello.</span><span class="sxs-lookup"><span data-stu-id="1f949-173">Configure hello container port-to-host port mapping by specifying a `PortBinding` policy in `ContainerHostPolicies` of hello ApplicationManifest.xml file.</span></span>  <span data-ttu-id="1f949-174">W tym artykule `ContainerPort` to 80 (kontenera hello przedstawia portu 80, jak określono w hello plik Dockerfile) i `EndpointRef` jest "myserviceTypeEndpoint" (zdefiniowane w manifeście usługi hello hello punktu końcowego).</span><span class="sxs-lookup"><span data-stu-id="1f949-174">For this article, `ContainerPort` is 80 (hello container exposes port 80, as specified in hello Dockerfile) and `EndpointRef` is "myserviceTypeEndpoint" (hello endpoint defined in hello service manifest).</span></span>  <span data-ttu-id="1f949-175">Przychodzące żądania usługi toohello na porcie 4000 są mapowane tooport 80 kontenera hello.</span><span class="sxs-lookup"><span data-stu-id="1f949-175">Incoming requests toohello service on port 4000 are mapped tooport 80 on hello container.</span></span>  <span data-ttu-id="1f949-176">Jeśli Twoje kontenera musi tooauthenticate z prywatnym repozytorium, Dodaj `RepositoryCredentials`.</span><span class="sxs-lookup"><span data-stu-id="1f949-176">If your container needs tooauthenticate with a private repository, then add `RepositoryCredentials`.</span></span>  <span data-ttu-id="1f949-177">W tym artykule Dodaj hello nazwę konta i hasło dla hello myregistry.azurecr.io kontenera rejestru.</span><span class="sxs-lookup"><span data-stu-id="1f949-177">For this article, add hello account name and password for hello myregistry.azurecr.io container registry.</span></span> 

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="myserviceTypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

## <a name="build-and-package-hello-service-fabric-application"></a><span data-ttu-id="1f949-178">Kompilowanie i pakietu aplikacji usługi Service Fabric hello</span><span class="sxs-lookup"><span data-stu-id="1f949-178">Build and package hello Service Fabric application</span></span>
<span data-ttu-id="1f949-179">Hello narzędzia usługi sieć szkieletowa Yeoman szablony obejmują skryptu kompilacji dla [Gradle](https://gradle.org/), który można użyć aplikacji hello toobuild z hello terminala.</span><span class="sxs-lookup"><span data-stu-id="1f949-179">hello Service Fabric Yeoman templates include a build script for [Gradle](https://gradle.org/), which you can use toobuild hello application from hello terminal.</span></span> <span data-ttu-id="1f949-180">toobuild i pakietów hello aplikacji, uruchom następujące hello:</span><span class="sxs-lookup"><span data-stu-id="1f949-180">toobuild and package hello application, run hello following:</span></span>

```bash
cd mycontainer
gradle
```

## <a name="deploy-hello-application"></a><span data-ttu-id="1f949-181">Wdrażanie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="1f949-181">Deploy hello application</span></span>
<span data-ttu-id="1f949-182">Po utworzeniu aplikacji hello można wdrożyć klaster lokalny toohello przy użyciu hello interfejsu wiersza polecenia usługi sieci szkieletowej.</span><span class="sxs-lookup"><span data-stu-id="1f949-182">Once hello application is built, you can deploy it toohello local cluster using hello Service Fabric CLI.</span></span>

<span data-ttu-id="1f949-183">Połącz toohello lokalnego klastra usługi sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="1f949-183">Connect toohello local Service Fabric cluster.</span></span>

```bash
sfctl cluster select --endpoint http://localhost:19080
```

<span data-ttu-id="1f949-184">Użyj hello zainstalować skrypt toocopy szablonu hello aplikacji hello pakietu magazynu obrazu klastra toohello, Rejestracja typu aplikacji hello, i Utwórz wystąpienie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="1f949-184">Use hello install script provided in hello template toocopy hello application package toohello cluster's image store, register hello application type, and create an instance of hello application.</span></span>

```bash
./install.sh
```

<span data-ttu-id="1f949-185">Otwórz przeglądarkę i przejdź tooService Eksploratora sieci szkieletowej w http://localhost: 19080/Explorer (localhost Zamień z hello prywatnego adresu IP hello maszyny Wirtualnej, jeśli przy użyciu Vagrant w systemie Mac OS X).</span><span class="sxs-lookup"><span data-stu-id="1f949-185">Open a browser and navigate tooService Fabric Explorer at http://localhost:19080/Explorer (replace localhost with hello private IP of hello VM if using Vagrant on Mac OS X).</span></span> <span data-ttu-id="1f949-186">Rozwiń węzeł aplikacji hello i należy pamiętać, że teraz wpis dla danego typu aplikacji i drugi dla hello pierwsze wystąpienie tego typu.</span><span class="sxs-lookup"><span data-stu-id="1f949-186">Expand hello Applications node and note that there is now an entry for your application type and another for hello first instance of that type.</span></span>

<span data-ttu-id="1f949-187">Połącz toohello systemem kontenera.</span><span class="sxs-lookup"><span data-stu-id="1f949-187">Connect toohello running container.</span></span>  <span data-ttu-id="1f949-188">Otwórz przeglądarkę sieci web toohello adres IP zwrócony przez port 4000, na przykład "http://localhost:4000".</span><span class="sxs-lookup"><span data-stu-id="1f949-188">Open a web browser pointing toohello IP address returned on port 4000, for example "http://localhost:4000".</span></span> <span data-ttu-id="1f949-189">Powinny pojawić się hello pozycji "Witaj świecie!"</span><span class="sxs-lookup"><span data-stu-id="1f949-189">You should see hello heading "Hello World!"</span></span> <span data-ttu-id="1f949-190">Wyświetl w przeglądarce hello.</span><span class="sxs-lookup"><span data-stu-id="1f949-190">display in hello browser.</span></span>

![Hello World!][hello-world]

## <a name="clean-up"></a><span data-ttu-id="1f949-192">Czyszczenie</span><span class="sxs-lookup"><span data-stu-id="1f949-192">Clean up</span></span>
<span data-ttu-id="1f949-193">Użyj skryptu Odinstaluj hello podane w hello wystąpienia aplikacji hello toodelete szablonu z hello lokalnego klastra projektowego i wyrejestrowywanie typu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="1f949-193">Use hello uninstall script provided in hello template toodelete hello application instance from hello local development cluster and unregister hello application type.</span></span>

```bash
./uninstall.sh
```

<span data-ttu-id="1f949-194">Po push hello obrazu toohello kontenera rejestru na komputerze projektowym można usunąć obrazu lokalne powitania:</span><span class="sxs-lookup"><span data-stu-id="1f949-194">After you push hello image toohello container registry you can delete hello local image from your development computer:</span></span>

```
docker rmi helloworldapp
docker rmi myregistry.azurecr.io/samples/helloworldapp
```

## <a name="complete-example-service-fabric-application-and-service-manifests"></a><span data-ttu-id="1f949-195">Kompletny przykład aplikacji i manifestów usługi Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1f949-195">Complete example Service Fabric application and service manifests</span></span>
<span data-ttu-id="1f949-196">Oto usługi pełną hello i manifestów aplikacji używane w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="1f949-196">Here are hello complete service and application manifests used in this article.</span></span>

### <a name="servicemanifestxml"></a><span data-ttu-id="1f949-197">ServiceManifest.xml</span><span class="sxs-lookup"><span data-stu-id="1f949-197">ServiceManifest.xml</span></span>
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
### <a name="applicationmanifestxml"></a><span data-ttu-id="1f949-198">ApplicationManifest.xml</span><span class="sxs-lookup"><span data-stu-id="1f949-198">ApplicationManifest.xml</span></span>
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
## <a name="adding-more-services-tooan-existing-application"></a><span data-ttu-id="1f949-199">Dodawanie więcej usług tooan istniejącej aplikacji</span><span class="sxs-lookup"><span data-stu-id="1f949-199">Adding more services tooan existing application</span></span>

<span data-ttu-id="1f949-200">wykonaj inną aplikację kontenera usługi tooan, utworzone za pomocą narzędzia yeoman, tooadd hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="1f949-200">tooadd another container service tooan application already created using yeoman, perform hello following steps:</span></span>

1. <span data-ttu-id="1f949-201">Zmień katalog główny toohello hello istniejącej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1f949-201">Change directory toohello root of hello existing application.</span></span>  <span data-ttu-id="1f949-202">Na przykład `cd ~/YeomanSamples/MyApplication`, jeśli `MyApplication` to aplikacja hello utworzone przez narzędzia Yeoman.</span><span class="sxs-lookup"><span data-stu-id="1f949-202">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is hello application created by Yeoman.</span></span>
2. <span data-ttu-id="1f949-203">Uruchom polecenie `yo azuresfcontainer:AddService`</span><span class="sxs-lookup"><span data-stu-id="1f949-203">Run `yo azuresfcontainer:AddService`</span></span>

<a id="manually"></a>


## <a name="configure-time-interval-before-container-is-force-terminated"></a><span data-ttu-id="1f949-204">Konfigurowanie interwału czasu wymuszania przerwania działania kontenera</span><span class="sxs-lookup"><span data-stu-id="1f949-204">Configure time interval before container is force terminated</span></span>

<span data-ttu-id="1f949-205">Przedział czasu dla toowait środowiska uruchomieniowego hello można skonfigurować przed usunięciem kontenera powitania po hello usunięcia usługi (lub Przenieś węzła tooanother) została uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="1f949-205">You can configure a time interval for hello runtime toowait before hello container is removed after hello service deletion (or a move tooanother node) has started.</span></span> <span data-ttu-id="1f949-206">Konfigurowanie interwał czasu hello wysyła hello `docker stop <time in seconds>` polecenia toohello kontenera.</span><span class="sxs-lookup"><span data-stu-id="1f949-206">Configuring hello time interval sends hello `docker stop <time in seconds>` command toohello container.</span></span>   <span data-ttu-id="1f949-207">Aby uzyskać więcej informacji, zobacz [docker stop](https://docs.docker.com/engine/reference/commandline/stop/).</span><span class="sxs-lookup"><span data-stu-id="1f949-207">For more detail, see [docker stop](https://docs.docker.com/engine/reference/commandline/stop/).</span></span> <span data-ttu-id="1f949-208">toowait interwał czasu Hello jest określony w hello `Hosting` sekcji.</span><span class="sxs-lookup"><span data-stu-id="1f949-208">hello time interval toowait is specified under hello `Hosting` section.</span></span> <span data-ttu-id="1f949-209">Witaj następującego fragmentu manifestu klastra pokazuje, jak tooset hello oczekiwania interwał:</span><span class="sxs-lookup"><span data-stu-id="1f949-209">hello following cluster manifest snippet shows how tooset hello wait interval:</span></span>

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
<span data-ttu-id="1f949-210">Witaj domyślny interwał ustawiono too10 sekund.</span><span class="sxs-lookup"><span data-stu-id="1f949-210">hello default time interval is set too10 seconds.</span></span> <span data-ttu-id="1f949-211">Ponieważ ta konfiguracja jest dynamiczny, config uaktualnić tylko na powitania klastra aktualizacje hello przekroczenia limitu czasu.</span><span class="sxs-lookup"><span data-stu-id="1f949-211">Since this configuration is dynamic, a config only upgrade on hello cluster updates hello timeout.</span></span> 


## <a name="configure-hello-runtime-tooremove-unused-container-images"></a><span data-ttu-id="1f949-212">Skonfiguruj tooremove środowiska uruchomieniowego hello kontenerem nieużywanych obrazów</span><span class="sxs-lookup"><span data-stu-id="1f949-212">Configure hello runtime tooremove unused container images</span></span>

<span data-ttu-id="1f949-213">Można skonfigurować tooremove klastra usługi sieć szkieletowa hello kontenerem nieużywanych obrazów z hello węzła.</span><span class="sxs-lookup"><span data-stu-id="1f949-213">You can configure hello Service Fabric cluster tooremove unused container images from hello node.</span></span> <span data-ttu-id="1f949-214">Ta konfiguracja pozwala przechwyceniem Jeśli zbyt wiele obrazów kontenera znajdują się w węźle hello toobe miejsca na dysku.</span><span class="sxs-lookup"><span data-stu-id="1f949-214">This configuration allows disk space toobe recaptured if too many container images are present on hello node.</span></span>  <span data-ttu-id="1f949-215">tooenable tej funkcji, hello aktualizacji `Hosting` sekcji w manifeście klastra hello pokazane na powitania po fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="1f949-215">tooenable this feature, update hello `Hosting` section in hello cluster manifest as shown in hello following snippet:</span></span> 


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

<span data-ttu-id="1f949-216">Do obrazów, które nie powinny być usuwane, można określić je w obszarze hello `ContainerImagesToSkip` parametru.</span><span class="sxs-lookup"><span data-stu-id="1f949-216">For images that should not be deleted, you can specify them under hello `ContainerImagesToSkip` parameter.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="1f949-217">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1f949-217">Next steps</span></span>
* <span data-ttu-id="1f949-218">Dowiedz się więcej o uruchamianiu [kontenerów w usłudze Service Fabric](service-fabric-containers-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1f949-218">Learn more about running [containers on Service Fabric](service-fabric-containers-overview.md).</span></span>
* <span data-ttu-id="1f949-219">Witaj odczytu [wdrażanie aplikacji .NET w kontenerze](service-fabric-host-app-in-a-container.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="1f949-219">Read hello [Deploy a .NET application in a container](service-fabric-host-app-in-a-container.md) tutorial.</span></span>
* <span data-ttu-id="1f949-220">Dowiedz się więcej o hello sieci szkieletowej usług [cyklu życia aplikacji](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="1f949-220">Learn about hello Service Fabric [application life-cycle](service-fabric-application-lifecycle.md).</span></span>
* <span data-ttu-id="1f949-221">Wyewidencjonowanie hello [przykłady kodu kontenera usługi sieć szkieletowa](https://github.com/Azure-Samples/service-fabric-dotnet-containers) w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="1f949-221">Checkout hello [Service Fabric container code samples](https://github.com/Azure-Samples/service-fabric-dotnet-containers) on GitHub.</span></span>

[hello-world]: ./media/service-fabric-get-started-containers-linux/HelloWorld.png
[sf-yeoman]: ./media/service-fabric-get-started-containers-linux/YoSF.png
