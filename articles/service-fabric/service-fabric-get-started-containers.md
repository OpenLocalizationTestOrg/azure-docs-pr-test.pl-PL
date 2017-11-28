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
# <a name="create-your-first-service-fabric-container-application-on-windows"></a><span data-ttu-id="497d2-104">Tworzenie pierwszej aplikacji kontenera usługi Service Fabric w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="497d2-104">Create your first Service Fabric container application on Windows</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="497d2-105">Windows</span><span class="sxs-lookup"><span data-stu-id="497d2-105">Windows</span></span>](service-fabric-get-started-containers.md)
> * [<span data-ttu-id="497d2-106">Linux</span><span class="sxs-lookup"><span data-stu-id="497d2-106">Linux</span></span>](service-fabric-get-started-containers-linux.md)

<span data-ttu-id="497d2-107">Systemem istniejącej aplikacji w kontenerze systemu Windows w klastrze usługi sieć szkieletowa nie wymaga żadnych zmian tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="497d2-107">Running an existing application in a Windows container on a Service Fabric cluster doesn't require any changes tooyour application.</span></span> <span data-ttu-id="497d2-108">W tym artykule przedstawiono tworzenie obrazu Docker zawierający Python [Flask](http://flask.pocoo.org/) sieci web, aplikacji i wdrażania go tooa klastra sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="497d2-108">This article walks you through creating a Docker image containing a Python [Flask](http://flask.pocoo.org/) web application and deploying it tooa Service Fabric cluster.</span></span>  <span data-ttu-id="497d2-109">Będziesz również udostępniać aplikację skonteneryzowaną za pomocą usługi [Azure Container Registry](/azure/container-registry/).</span><span class="sxs-lookup"><span data-stu-id="497d2-109">You will also share your containerized application through [Azure Container Registry](/azure/container-registry/).</span></span>  <span data-ttu-id="497d2-110">W tym artykule przyjęto założenie, że masz podstawową wiedzą dotyczącą platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="497d2-110">This article assumes a basic understanding of Docker.</span></span> <span data-ttu-id="497d2-111">Informacje na temat rozwiązania Docker za odczytywanie hello [omówienie Docker](https://docs.docker.com/engine/understanding-docker/).</span><span class="sxs-lookup"><span data-stu-id="497d2-111">You can learn about Docker by reading hello [Docker Overview](https://docs.docker.com/engine/understanding-docker/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="497d2-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="497d2-112">Prerequisites</span></span>
<span data-ttu-id="497d2-113">Komputer dewelopera z następującym oprogramowaniem:</span><span class="sxs-lookup"><span data-stu-id="497d2-113">A development computer running:</span></span>
* <span data-ttu-id="497d2-114">Program Visual Studio 2015 lub Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="497d2-114">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="497d2-115">[Zestaw SDK usługi Service Fabric oraz narzędzia](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="497d2-115">[Service Fabric SDK and tools](service-fabric-get-started.md).</span></span>
*  <span data-ttu-id="497d2-116">Program Docker dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="497d2-116">Docker for Windows.</span></span>  <span data-ttu-id="497d2-117">[Pobierz program Docker CE dla systemu Windows (wersja stabilna)](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description).</span><span class="sxs-lookup"><span data-stu-id="497d2-117">[Get Docker CE for Windows (stable)](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description).</span></span> <span data-ttu-id="497d2-118">Po instalacji i uruchamiania Docker, kliknij prawym przyciskiem myszy ikonę na pasku zadań hello i wybierz **przełącznika kontenery tooWindows**.</span><span class="sxs-lookup"><span data-stu-id="497d2-118">After installing and starting Docker, right-click on hello tray icon and select **Switch tooWindows containers**.</span></span> <span data-ttu-id="497d2-119">Jest to wymagane toorun obrazy usługi Docker opartych na systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="497d2-119">This is required toorun Docker images based on Windows.</span></span>

<span data-ttu-id="497d2-120">Klaster systemu Windows z co najmniej trzema węzłami działającymi w systemie Windows Server 2016 z kontenerami — [utwórz klaster](service-fabric-cluster-creation-via-portal.md) lub [wypróbuj bezpłatnie usługę Service Fabric](https://aka.ms/tryservicefabric).</span><span class="sxs-lookup"><span data-stu-id="497d2-120">A Windows cluster with three or more nodes running on Windows Server 2016 with Containers- [Create a cluster](service-fabric-cluster-creation-via-portal.md) or [try Service Fabric for free](https://aka.ms/tryservicefabric).</span></span>

<span data-ttu-id="497d2-121">Rejestr w usłudze Azure Container Registry — [utwórz rejestr kontenera](../container-registry/container-registry-get-started-portal.md) w subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="497d2-121">A registry in Azure Container Registry - [Create a container registry](../container-registry/container-registry-get-started-portal.md) in your Azure subscription.</span></span>

## <a name="define-hello-docker-container"></a><span data-ttu-id="497d2-122">Zdefiniuj hello kontenera Docker</span><span class="sxs-lookup"><span data-stu-id="497d2-122">Define hello Docker container</span></span>
<span data-ttu-id="497d2-123">Tworzenie obrazu opartego na powitania [obrazu Python](https://hub.docker.com/_/python/) znajduje się w Centrum Docker.</span><span class="sxs-lookup"><span data-stu-id="497d2-123">Build an image based on hello [Python image](https://hub.docker.com/_/python/) located on Docker Hub.</span></span>

<span data-ttu-id="497d2-124">Zdefiniuj kontener platformy Docker w pliku Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="497d2-124">Define your Docker container in a Dockerfile.</span></span> <span data-ttu-id="497d2-125">Plik Dockerfile Hello zawiera instrukcje dotyczące konfigurowania środowiska hello wewnątrz kontenera sieci, ładowania aplikacji hello ma toorun i mapowania portów.</span><span class="sxs-lookup"><span data-stu-id="497d2-125">hello Dockerfile contains instructions for setting up hello environment inside your container, loading hello application you want toorun, and mapping ports.</span></span> <span data-ttu-id="497d2-126">Hello plik Dockerfile jest toohello wejściowych hello `docker build` polecenia, które tworzy obraz powitania.</span><span class="sxs-lookup"><span data-stu-id="497d2-126">hello Dockerfile is hello input toohello `docker build` command, which creates hello image.</span></span>

<span data-ttu-id="497d2-127">Utwórz pusty katalog i Utwórz plik hello *plik Dockerfile* (z bez rozszerzenia pliku).</span><span class="sxs-lookup"><span data-stu-id="497d2-127">Create an empty directory and create hello file *Dockerfile* (with no file extension).</span></span> <span data-ttu-id="497d2-128">Dodaje hello zbyt*plik Dockerfile* i Zapisz zmiany:</span><span class="sxs-lookup"><span data-stu-id="497d2-128">Add hello following too*Dockerfile* and save your changes:</span></span>

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

<span data-ttu-id="497d2-129">Witaj odczytu [odwołania plik Dockerfile](https://docs.docker.com/engine/reference/builder/) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="497d2-129">Read hello [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) for more information.</span></span>

## <a name="create-a-simple-web-application"></a><span data-ttu-id="497d2-130">Tworzenie prostej aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="497d2-130">Create a simple web application</span></span>
<span data-ttu-id="497d2-131">Utwórz aplikację sieci Web platformy Flask, która nasłuchuje na porcie 80 i zwraca wartość „Hello World!”.</span><span class="sxs-lookup"><span data-stu-id="497d2-131">Create a Flask web application listening on port 80 that returns "Hello World!".</span></span>  <span data-ttu-id="497d2-132">W hello na tym samym katalogu, Utwórz plik hello *requirements.txt*.</span><span class="sxs-lookup"><span data-stu-id="497d2-132">In hello same directory, create hello file *requirements.txt*.</span></span>  <span data-ttu-id="497d2-133">Dodaj następujące hello i Zapisz zmiany:</span><span class="sxs-lookup"><span data-stu-id="497d2-133">Add hello following and save your changes:</span></span>
```
Flask
```

<span data-ttu-id="497d2-134">Również utworzyć hello *app.py* i dodaj następujące hello:</span><span class="sxs-lookup"><span data-stu-id="497d2-134">Also create hello *app.py* file and add hello following:</span></span>

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
## <a name="build-hello-image"></a><span data-ttu-id="497d2-135">Utwórz obraz powitania</span><span class="sxs-lookup"><span data-stu-id="497d2-135">Build hello image</span></span>
<span data-ttu-id="497d2-136">Uruchom hello `docker build` polecenia toocreate hello obrazu, który uruchamia aplikację sieci web.</span><span class="sxs-lookup"><span data-stu-id="497d2-136">Run hello `docker build` command toocreate hello image that runs your web application.</span></span> <span data-ttu-id="497d2-137">Otwórz okno programu PowerShell i przejdź toohello katalog zawierający plik Dockerfile hello.</span><span class="sxs-lookup"><span data-stu-id="497d2-137">Open a PowerShell window and navigate toohello directory containing hello Dockerfile.</span></span> <span data-ttu-id="497d2-138">Uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="497d2-138">Run hello following command:</span></span>

```
docker build -t helloworldapp .
```

<span data-ttu-id="497d2-139">To polecenie kompilacji hello nowy obraz przy użyciu instrukcji hello w Twojej plik Dockerfile, nazewnictwa (-t znakowanie) obraz powitania "helloworldapp".</span><span class="sxs-lookup"><span data-stu-id="497d2-139">This command builds hello new image using hello instructions in your Dockerfile, naming (-t tagging) hello image "helloworldapp".</span></span> <span data-ttu-id="497d2-140">Tworzenie obrazu ściąga podstawowy obraz powitania w dół od centrum Docker i tworzy nowy obraz, który dodaje aplikację na podstawowy obraz powitania.</span><span class="sxs-lookup"><span data-stu-id="497d2-140">Building an image pulls hello base image down from Docker Hub and creates a new image that adds your application on top of hello base image.</span></span>  

<span data-ttu-id="497d2-141">Po zakończeniu wykonywania polecenia kompilacji hello Uruchom hello `docker images` polecenia toosee informacji na temat nowego obrazu hello:</span><span class="sxs-lookup"><span data-stu-id="497d2-141">Once hello build command completes, run hello `docker images` command toosee information on hello new image:</span></span>

```
$ docker images

REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              8ce25f5d6a79        2 minutes ago       10.4 GB
```

## <a name="run-hello-application-locally"></a><span data-ttu-id="497d2-142">Uruchamianie aplikacji hello lokalnie</span><span class="sxs-lookup"><span data-stu-id="497d2-142">Run hello application locally</span></span>
<span data-ttu-id="497d2-143">Sprawdź obrazu lokalnie przed wypychanie go hello kontenera rejestru.</span><span class="sxs-lookup"><span data-stu-id="497d2-143">Verify your image locally before pushing it hello container registry.</span></span>  

<span data-ttu-id="497d2-144">Uruchamianie aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="497d2-144">Run hello application:</span></span>

```
docker run -d --name my-web-site helloworldapp
```

<span data-ttu-id="497d2-145">*Nazwa* daje toohello nazwy, systemem kontenera (zamiast identyfikator kontenera hello).</span><span class="sxs-lookup"><span data-stu-id="497d2-145">*name* gives a name toohello running container (instead of hello container ID).</span></span>

<span data-ttu-id="497d2-146">Po uruchomieniu kontenera hello, Znajdź adresu IP, dzięki czemu można łączyć tooyour systemem kontenera w przeglądarce:</span><span class="sxs-lookup"><span data-stu-id="497d2-146">Once hello container starts, find its IP address so that you can connect tooyour running container from a browser:</span></span>
```
docker inspect -f "{{ .NetworkSettings.Networks.nat.IPAddress }}" my-web-site
```

<span data-ttu-id="497d2-147">Połącz toohello systemem kontenera.</span><span class="sxs-lookup"><span data-stu-id="497d2-147">Connect toohello running container.</span></span>  <span data-ttu-id="497d2-148">Otwórz przeglądarkę sieci web toohello adresu IP zwróconego, na przykład "http://172.31.194.61".</span><span class="sxs-lookup"><span data-stu-id="497d2-148">Open a web browser pointing toohello IP address returned, for example "http://172.31.194.61".</span></span> <span data-ttu-id="497d2-149">Powinny pojawić się hello pozycji "Witaj świecie!"</span><span class="sxs-lookup"><span data-stu-id="497d2-149">You should see hello heading "Hello World!"</span></span> <span data-ttu-id="497d2-150">Wyświetl w przeglądarce hello.</span><span class="sxs-lookup"><span data-stu-id="497d2-150">display in hello browser.</span></span>

<span data-ttu-id="497d2-151">toostop kontenera Uruchom:</span><span class="sxs-lookup"><span data-stu-id="497d2-151">toostop your container, run:</span></span>

```
docker stop my-web-site
```

<span data-ttu-id="497d2-152">Usuń kontener hello z komputerze deweloperskim:</span><span class="sxs-lookup"><span data-stu-id="497d2-152">Delete hello container from your development machine:</span></span>

```
docker rm my-web-site
```

<a id="Push-Containers"></a>
## <a name="push-hello-image-toohello-container-registry"></a><span data-ttu-id="497d2-153">Wypychanie hello obrazu toohello kontenera rejestru</span><span class="sxs-lookup"><span data-stu-id="497d2-153">Push hello image toohello container registry</span></span>
<span data-ttu-id="497d2-154">Po upewnieniu się, że kontenera hello jest uruchamiany na komputerze deweloperskim, Wypchnij rejestru tooyour obraz powitania w rejestrze kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="497d2-154">After you verify that hello container runs on your development machine, push hello image tooyour registry in Azure Container Registry.</span></span>

<span data-ttu-id="497d2-155">Uruchom ``docker login`` toolog w rejestrze kontenera tooyour z Twojej [poświadczenia rejestru](../container-registry/container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="497d2-155">Run ``docker login`` toolog in tooyour container registry with your [registry credentials](../container-registry/container-registry-authentication.md).</span></span>

<span data-ttu-id="497d2-156">Witaj w poniższym przykładzie przekazuje hello Identyfikatora i hasła usługi Azure Active Directory [nazwy głównej usługi](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="497d2-156">hello following example passes hello ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span></span> <span data-ttu-id="497d2-157">Na przykład może przypisano rejestr tooyour główna usługi scenariusz automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="497d2-157">For example, you might have assigned a service principal tooyour registry for an automation scenario.</span></span> <span data-ttu-id="497d2-158">Możesz również zalogować się za pomocą nazwy i hasła użytkownika rejestru.</span><span class="sxs-lookup"><span data-stu-id="497d2-158">Or, you could login using your registry username and password.</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="497d2-159">Witaj następujące polecenie tworzy tag lub alias obraz powitania z rejestru tooyour w pełni kwalifikowana.</span><span class="sxs-lookup"><span data-stu-id="497d2-159">hello following command creates a tag, or alias, of hello image, with a fully qualified path tooyour registry.</span></span> <span data-ttu-id="497d2-160">W tym przykładzie miejsca hello obrazu w hello ```samples``` bałaganu tooavoid przestrzeni nazw w głównym hello hello rejestru.</span><span class="sxs-lookup"><span data-stu-id="497d2-160">This example places hello image in hello ```samples``` namespace tooavoid clutter in hello root of hello registry.</span></span>

```
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

<span data-ttu-id="497d2-161">Wypchnij hello obrazu tooyour kontenera rejestru:</span><span class="sxs-lookup"><span data-stu-id="497d2-161">Push hello image tooyour container registry:</span></span>

```
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="create-hello-containerized-service-in-visual-studio"></a><span data-ttu-id="497d2-162">Tworzenie usługi hello konteneryzowanych w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="497d2-162">Create hello containerized service in Visual Studio</span></span>
<span data-ttu-id="497d2-163">Witaj zestawu SDK usług sieci szkieletowej i narzędzia zapewniają toohelp szablonu usługi można utworzyć aplikację konteneryzowanych.</span><span class="sxs-lookup"><span data-stu-id="497d2-163">hello Service Fabric SDK and tools provide a service template toohelp you create a containerized application.</span></span>

1. <span data-ttu-id="497d2-164">Uruchom program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="497d2-164">Start Visual Studio.</span></span>  <span data-ttu-id="497d2-165">Wybierz kolejno pozycje **Plik** > **Nowy** > **Projekt**.</span><span class="sxs-lookup"><span data-stu-id="497d2-165">Select **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="497d2-166">Wybierz pozycję **Aplikacja usługi Service Fabric**, nadaj jej nazwę „MyFirstContainer” i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="497d2-166">Select **Service Fabric application**, name it "MyFirstContainer", and click **OK**.</span></span>
3. <span data-ttu-id="497d2-167">Wybierz **kontenera gościa** z listy hello **szablony usługi**.</span><span class="sxs-lookup"><span data-stu-id="497d2-167">Select **Guest Container** from hello list of **service templates**.</span></span>
4. <span data-ttu-id="497d2-168">W **nazwa obrazu** wprowadź "myregistry.azurecr.io/samples/helloworldapp" obraz powitania wypychana tooyour kontenera repozytorium.</span><span class="sxs-lookup"><span data-stu-id="497d2-168">In **Image Name** enter "myregistry.azurecr.io/samples/helloworldapp", hello image you pushed tooyour container repository.</span></span>
5. <span data-ttu-id="497d2-169">Nadaj nazwę usłudze i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="497d2-169">Give your service a name, and click **OK**.</span></span>

## <a name="configure-communication"></a><span data-ttu-id="497d2-170">Konfigurowanie komunikacji</span><span class="sxs-lookup"><span data-stu-id="497d2-170">Configure communication</span></span>
<span data-ttu-id="497d2-171">punkt końcowy jest wymagane przez usługę Hello konteneryzowanych komunikacji.</span><span class="sxs-lookup"><span data-stu-id="497d2-171">hello containerized service needs an endpoint for communication.</span></span> <span data-ttu-id="497d2-172">Dodaj `Endpoint` element z hello protokół, port i plik ServiceManifest.xml toohello typu.</span><span class="sxs-lookup"><span data-stu-id="497d2-172">Add an `Endpoint` element with hello protocol, port, and type toohello ServiceManifest.xml file.</span></span> <span data-ttu-id="497d2-173">W tym artykule usługi hello konteneryzowanych nasłuchuje na porcie 8081.</span><span class="sxs-lookup"><span data-stu-id="497d2-173">For this article, hello containerized service listens on port 8081.</span></span>  <span data-ttu-id="497d2-174">W tym przykładzie jest używany stały port 8081.</span><span class="sxs-lookup"><span data-stu-id="497d2-174">In this example, a fixed port 8081 is used.</span></span>  <span data-ttu-id="497d2-175">Jeśli nie określono portu, losowego portu z zakresu portów aplikacji hello zostanie wybrany.</span><span class="sxs-lookup"><span data-stu-id="497d2-175">If no port is specified, a random port from hello application port range is chosen.</span></span>  

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="Guest1TypeEndpoint" UriScheme="http" Port="8081" Protocol="http"/>
  </Endpoints>
</Resources>
```

<span data-ttu-id="497d2-176">Definiując punktu końcowego sieci szkieletowej usług publikuje hello toohello punktu końcowego usługi nazw.</span><span class="sxs-lookup"><span data-stu-id="497d2-176">By defining an endpoint, Service Fabric publishes hello endpoint toohello Naming service.</span></span>  <span data-ttu-id="497d2-177">Innych usług uruchomionych w klastrze hello można rozwiązać tego kontenera.</span><span class="sxs-lookup"><span data-stu-id="497d2-177">Other services running in hello cluster can resolve this container.</span></span>  <span data-ttu-id="497d2-178">Można również wykonywać kontenerami komunikację z wykorzystaniem hello [odwrotny serwer proxy](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="497d2-178">You can also perform container-to-container communication using hello [reverse proxy](service-fabric-reverseproxy.md).</span></span>  <span data-ttu-id="497d2-179">Komunikacja odbywa się przez podanie port nasłuchujący hello zwrotny serwer proxy HTTP i nazwa hello hello usług, które ma być toocommunicate ze zmiennych środowiskowych.</span><span class="sxs-lookup"><span data-stu-id="497d2-179">Communication is performed by providing hello reverse proxy HTTP listening port and hello name of hello services that you want toocommunicate with as environment variables.</span></span>

## <a name="configure-and-set-environment-variables"></a><span data-ttu-id="497d2-180">Konfigurowanie i ustawianie zmiennych środowiskowych</span><span class="sxs-lookup"><span data-stu-id="497d2-180">Configure and set environment variables</span></span>
<span data-ttu-id="497d2-181">Zmienne środowiskowe można określić dla każdego pakietu kodu w hello manifestu usługi.</span><span class="sxs-lookup"><span data-stu-id="497d2-181">Environment variables can be specified for each code package in hello service manifest.</span></span> <span data-ttu-id="497d2-182">Ta funkcja jest dostępna dla wszystkich usług niezależnie od tego, czy są one wdrażane jako kontenery, procesy, czy pliki wykonywalne gościa.</span><span class="sxs-lookup"><span data-stu-id="497d2-182">This feature is available for all services irrespective of whether they are deployed as containers or processes or guest executables.</span></span> <span data-ttu-id="497d2-183">Można zastąpić zmiennej środowiskowej wartości w aplikacji hello manifestu lub określić ich podczas wdrażania jako parametry aplikacji.</span><span class="sxs-lookup"><span data-stu-id="497d2-183">You can override environment variable values in hello application manifest or specify them during deployment as application parameters.</span></span>

<span data-ttu-id="497d2-184">Witaj poniższy fragment XML manifestu usługi przedstawia przykładowy sposób zmiennych środowiskowych toospecify pakietu kodu:</span><span class="sxs-lookup"><span data-stu-id="497d2-184">hello following service manifest XML snippet shows an example of how toospecify environment variables for a code package:</span></span>
```xml
<CodePackage Name="Code" Version="1.0.0">
  ...
  <EnvironmentVariables>
    <EnvironmentVariable Name="HttpGatewayPort" Value=""/>    
  </EnvironmentVariables>
</CodePackage>
```

<span data-ttu-id="497d2-185">Te zmienne środowiskowe może zostać zastąpiona w manifeście aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="497d2-185">These environment variables can be overridden in hello application manifest:</span></span>

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
  </EnvironmentOverrides>
  ...
</ServiceManifestImport>
```

## <a name="configure-container-port-to-host-port-mapping-and-container-to-container-discovery"></a><span data-ttu-id="497d2-186">Konfigurowanie mapowania portów kontenera typu port do hosta i odnajdywania między kontenerami</span><span class="sxs-lookup"><span data-stu-id="497d2-186">Configure container port-to-host port mapping and container-to-container discovery</span></span>
<span data-ttu-id="497d2-187">Skonfiguruj toocommunicate port używany host hello kontenera.</span><span class="sxs-lookup"><span data-stu-id="497d2-187">Configure a host port used toocommunicate  with hello container.</span></span> <span data-ttu-id="497d2-188">Powiązanie portu Hello mapuje hello portu, na które hello wewnątrz hello kontenera tooa portu na hoście hello nasłuchuje usługa.</span><span class="sxs-lookup"><span data-stu-id="497d2-188">hello port binding maps hello port on which hello service is listening inside hello container tooa port on hello host.</span></span> <span data-ttu-id="497d2-189">Dodaj `PortBinding` element `ContainerHostPolicies` element pliku ApplicationManifest.xml hello.</span><span class="sxs-lookup"><span data-stu-id="497d2-189">Add a `PortBinding` element in `ContainerHostPolicies` element of hello ApplicationManifest.xml file.</span></span>  <span data-ttu-id="497d2-190">W tym artykule `ContainerPort` to 80 (kontenera hello przedstawia portu 80, jak określono w hello plik Dockerfile) i `EndpointRef` jest "Guest1TypeEndpoint" (punkt końcowy wcześniej zdefiniowany w manifeście usługi hello hello).</span><span class="sxs-lookup"><span data-stu-id="497d2-190">For this article, `ContainerPort` is 80 (hello container exposes port 80, as specified in hello Dockerfile) and `EndpointRef` is "Guest1TypeEndpoint" (hello endpoint previously defined in hello service manifest).</span></span>  <span data-ttu-id="497d2-191">Przychodzące żądania usługi toohello na porcie 8081 są mapowane tooport 80 kontenera hello.</span><span class="sxs-lookup"><span data-stu-id="497d2-191">Incoming requests toohello service on port 8081 are mapped tooport 80 on hello container.</span></span>

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
  </ContainerHostPolicies>
</Policies>
```

## <a name="configure-container-registry-authentication"></a><span data-ttu-id="497d2-192">Konfigurowanie uwierzytelniania rejestru kontenerów</span><span class="sxs-lookup"><span data-stu-id="497d2-192">Configure container registry authentication</span></span>
<span data-ttu-id="497d2-193">Skonfiguruj uwierzytelnianie rejestru kontenera przez dodanie `RepositoryCredentials` zbyt`ContainerHostPolicies` pliku ApplicationManifest.xml hello.</span><span class="sxs-lookup"><span data-stu-id="497d2-193">Configure container registry authentication by adding `RepositoryCredentials` too`ContainerHostPolicies` of hello ApplicationManifest.xml file.</span></span> <span data-ttu-id="497d2-194">Dodaj hello konto i hasło dla hello myregistry.azurecr.io kontenera rejestru, dzięki czemu hello usługi toodownload hello kontener obrazu z repozytorium hello.</span><span class="sxs-lookup"><span data-stu-id="497d2-194">Add hello account and password for hello myregistry.azurecr.io container registry, which allows hello service toodownload hello container image from hello repository.</span></span>

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

<span data-ttu-id="497d2-195">Firma Microsoft zaleca szyfrowania hello repozytorium hasła przy użyciu certyfikatu szyfrowanie, która została wdrożona tooall węzłów klastra hello.</span><span class="sxs-lookup"><span data-stu-id="497d2-195">We recommend that you encrypt hello repository password by using an encipherment certificate that's deployed tooall nodes of hello cluster.</span></span> <span data-ttu-id="497d2-196">Gdy usługa sieć szkieletowa wdraża hello usługi pakietu toohello klastra, certyfikat Szyfrowanie hello jest tekst zaszyfrowany hello toodecrypt używane.</span><span class="sxs-lookup"><span data-stu-id="497d2-196">When Service Fabric deploys hello service package toohello cluster, hello encipherment certificate is used toodecrypt hello cipher text.</span></span>  <span data-ttu-id="497d2-197">polecenie cmdlet Invoke-ServiceFabricEncryptText Hello jest używany toocreate hello szyfrowania tekst hello hasła, które jest dodawane do pliku ApplicationManifest.xml toohello.</span><span class="sxs-lookup"><span data-stu-id="497d2-197">hello Invoke-ServiceFabricEncryptText cmdlet is used toocreate hello cipher text for hello password, which is added toohello ApplicationManifest.xml file.</span></span>

<span data-ttu-id="497d2-198">Witaj poniższy skrypt tworzy nowy certyfikat z podpisem własnym i eksportuje je tooa pliku PFX.</span><span class="sxs-lookup"><span data-stu-id="497d2-198">hello following script creates a new self-signed certificate and exports it tooa PFX file.</span></span>  <span data-ttu-id="497d2-199">certyfikat Hello jest importowany do istniejący magazyn kluczy, a następnie wdrażana toohello klastra sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="497d2-199">hello certificate is imported into an existing key vault and then deployed toohello Service Fabric cluster.</span></span>

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
<span data-ttu-id="497d2-200">Szyfrowanie hasła hello przy użyciu hello [Invoke ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="497d2-200">Encrypt hello password using hello [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet.</span></span>

```powershell
$text = "=P==/==/=8=/=+u4lyOB=+=nWzEeRfF="
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint $cer.Thumbprint -Text $text -StoreLocation Local -StoreName My
```

<span data-ttu-id="497d2-201">Zamień hasło hello tekst zaszyfrowany hello zwrócony przez hello [Invoke ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) polecenia cmdlet i ustaw `PasswordEncrypted` zbyt "true".</span><span class="sxs-lookup"><span data-stu-id="497d2-201">Replace hello password with hello cipher text returned by hello [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet and set `PasswordEncrypted` too"true".</span></span>

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

## <a name="configure-isolation-mode"></a><span data-ttu-id="497d2-202">Konfigurowanie trybu izolacji</span><span class="sxs-lookup"><span data-stu-id="497d2-202">Configure isolation mode</span></span>
<span data-ttu-id="497d2-203">System Windows obsługuje dwa tryby izolacji dla kontenerów: tryb procesu oraz tryb funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="497d2-203">Windows supports two isolation modes for containers: process and Hyper-V.</span></span> <span data-ttu-id="497d2-204">W trybie izolacji procesu hello wszystkich kontenerów hello systemem hello tego samego hosta maszyny udziału hello jądra z hostem hello.</span><span class="sxs-lookup"><span data-stu-id="497d2-204">With hello process isolation mode, all hello containers running on hello same host machine share hello kernel with hello host.</span></span> <span data-ttu-id="497d2-205">W trybie izolacji hello funkcji Hyper-V między każdego kontenera funkcji Hyper-V a hostem kontenera hello odizolowanych hello jądra.</span><span class="sxs-lookup"><span data-stu-id="497d2-205">With hello Hyper-V isolation mode, hello kernels are isolated between each Hyper-V container and hello container host.</span></span> <span data-ttu-id="497d2-206">Tryb izolacji Hello jest określony w hello `ContainerHostPolicies` elementu w pliku manifestu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="497d2-206">hello isolation mode is specified in hello `ContainerHostPolicies` element in hello application manifest file.</span></span> <span data-ttu-id="497d2-207">Tryby izolacji Hello, które można określić są `process`, `hyperv`, i `default`.</span><span class="sxs-lookup"><span data-stu-id="497d2-207">hello isolation modes that can be specified are `process`, `hyperv`, and `default`.</span></span> <span data-ttu-id="497d2-208">domyślny tryb izolacji Hello domyślnie przyjmowana jest zbyt`process` w systemie Windows Server obsługuje i domyślnie zbyt`hyperv` na hostach z systemem Windows 10.</span><span class="sxs-lookup"><span data-stu-id="497d2-208">hello default isolation mode defaults too`process` on Windows Server hosts, and defaults too`hyperv` on Windows 10 hosts.</span></span> <span data-ttu-id="497d2-209">Hello poniższy fragment kodu przedstawia sposób hello trybu izolacji została określona w pliku manifestu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="497d2-209">hello following snippet shows how hello isolation mode is specified in hello application manifest file.</span></span>

```xml
<ContainerHostPolicies CodePackageRef="Code" Isolation="hyperv">
```

## <a name="configure-resource-governance"></a><span data-ttu-id="497d2-210">Konfigurowanie zarządzania zasobami</span><span class="sxs-lookup"><span data-stu-id="497d2-210">Configure resource governance</span></span>
<span data-ttu-id="497d2-211">[Zarządzanie zasobów](service-fabric-resource-governance.md) ogranicza hello zasobów, które hello kontenera można użyć na hoście hello.</span><span class="sxs-lookup"><span data-stu-id="497d2-211">[Resource governance](service-fabric-resource-governance.md) restricts hello resources that hello container can use on hello host.</span></span> <span data-ttu-id="497d2-212">Witaj `ResourceGovernancePolicy` element, który określono w manifeście aplikacji hello jest używane toodeclare limity zasobów pakietu kodu usługi.</span><span class="sxs-lookup"><span data-stu-id="497d2-212">hello `ResourceGovernancePolicy` element, which is specified in hello application manifest, is used toodeclare resource limits for a service code package.</span></span> <span data-ttu-id="497d2-213">Limity zasobów można ustawić dla hello następujące zasoby: pamięci, MemorySwap, CpuShares (względną wagę Procesora), MemoryReservationInMB, BlkioWeight (BlockIO względną wagę).</span><span class="sxs-lookup"><span data-stu-id="497d2-213">Resource limits can be set for hello following resources: Memory, MemorySwap, CpuShares (CPU relative weight), MemoryReservationInMB, BlkioWeight (BlockIO relative weight).</span></span>  <span data-ttu-id="497d2-214">W tym przykładzie pakiet usługi Guest1Pkg pobiera jeden rdzeń w węzłach klastra hello, gdzie jest umieszczony.</span><span class="sxs-lookup"><span data-stu-id="497d2-214">In this example, service package Guest1Pkg gets one core on hello cluster nodes where it is placed.</span></span>  <span data-ttu-id="497d2-215">Limity pamięci są bezwzględne, więc hello pakietu kodu jest ograniczona too1024 MB pamięci (i elastyczne gwarancji zastrzeżenia hello sam).</span><span class="sxs-lookup"><span data-stu-id="497d2-215">Memory limits are absolute, so hello code package is limited too1024 MB of memory (and a soft-guarantee reservation of hello same).</span></span> <span data-ttu-id="497d2-216">Pakiety kodu (kontenery lub procesów) nie są możliwe tooallocate, który więcej pamięci niż ten limit i podjęto toodo tak powoduje wygenerowanie wyjątku braku pamięci.</span><span class="sxs-lookup"><span data-stu-id="497d2-216">Code packages (containers or processes) are not able tooallocate more memory than this limit, and attempting toodo so results in an out-of-memory exception.</span></span> <span data-ttu-id="497d2-217">Toowork wymuszania limit zasobów wszystkie pakiety kodu w ramach pakietu usługi powinny mieć określone limity pamięci.</span><span class="sxs-lookup"><span data-stu-id="497d2-217">For resource limit enforcement toowork, all code packages within a service package should have memory limits specified.</span></span>

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
  <Policies>
    <ServicePackageResourceGovernancePolicy CpuCores="1"/>
    <ResourceGovernancePolicy CodePackageRef="Code" MemoryInMB="1024"  />
  </Policies>
</ServiceManifestImport>
```

## <a name="deploy-hello-container-application"></a><span data-ttu-id="497d2-218">Wdrażanie aplikacji kontenera hello</span><span class="sxs-lookup"><span data-stu-id="497d2-218">Deploy hello container application</span></span>
<span data-ttu-id="497d2-219">Zapisz wszystkie zmiany i tworzenia aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="497d2-219">Save all your changes and build hello application.</span></span> <span data-ttu-id="497d2-220">toopublish aplikacji, kliknij prawym przyciskiem myszy **MyFirstContainer** w Eksploratorze rozwiązań i wybierz **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="497d2-220">toopublish your application, right-click on **MyFirstContainer** in Solution Explorer and select **Publish**.</span></span>

<span data-ttu-id="497d2-221">W **punktu końcowego połączenia**, wprowadź hello punkt końcowy zarządzania dla klastra hello.</span><span class="sxs-lookup"><span data-stu-id="497d2-221">In **Connection Endpoint**, enter hello management endpoint for hello cluster.</span></span>  <span data-ttu-id="497d2-222">Na przykład „containercluster.westus2.cloudapp.azure.com:19000”.</span><span class="sxs-lookup"><span data-stu-id="497d2-222">For example, "containercluster.westus2.cloudapp.azure.com:19000".</span></span> <span data-ttu-id="497d2-223">Połączenie klienta hello można znaleźć punkt końcowy w bloku omówienie hello klastra w hello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="497d2-223">You can find hello client connection endpoint in hello Overview blade for your cluster in hello [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="497d2-224">Kliknij przycisk **Opublikuj**.</span><span class="sxs-lookup"><span data-stu-id="497d2-224">Click **Publish**.</span></span>

<span data-ttu-id="497d2-225">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) to oparte na sieci Web narzędzie do sprawdzania aplikacji i węzłów oraz zarządzania nimi w klastrze usługi Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="497d2-225">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is a web-based tool for inspecting and managing applications and nodes in a Service Fabric cluster.</span></span> <span data-ttu-id="497d2-226">Otwórz przeglądarkę i przejdź toohttp://containercluster.westus2.cloudapp.azure.com:19080/Explorer/wykonaj wdrożenie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="497d2-226">Open a browser and navigate toohttp://containercluster.westus2.cloudapp.azure.com:19080/Explorer/ and follow hello application deployment.</span></span>  <span data-ttu-id="497d2-227">Aplikacja Hello wdraża, ale jest w stanie błędu, dopóki obraz powitania jest pobierany w węzłach klastra hello (które może zająć trochę czasu, w zależności od rozmiaru obrazu hello): ![błąd][1]</span><span class="sxs-lookup"><span data-stu-id="497d2-227">hello application deploys but is in an error state until hello image is downloaded on hello cluster nodes (which can take some time, depending on hello image size): ![Error][1]</span></span>

<span data-ttu-id="497d2-228">Aplikacja Hello jest gotowa, gdy jest on w ```Ready``` stanu: ![gotowe][2]</span><span class="sxs-lookup"><span data-stu-id="497d2-228">hello application is ready when it's in ```Ready``` state: ![Ready][2]</span></span>

<span data-ttu-id="497d2-229">Otwórz przeglądarkę i przejdź toohttp://containercluster.westus2.cloudapp.azure.com:8081.</span><span class="sxs-lookup"><span data-stu-id="497d2-229">Open a browser and navigate toohttp://containercluster.westus2.cloudapp.azure.com:8081.</span></span> <span data-ttu-id="497d2-230">Powinny pojawić się hello pozycji "Witaj świecie!"</span><span class="sxs-lookup"><span data-stu-id="497d2-230">You should see hello heading "Hello World!"</span></span> <span data-ttu-id="497d2-231">Wyświetl w przeglądarce hello.</span><span class="sxs-lookup"><span data-stu-id="497d2-231">display in hello browser.</span></span>

## <a name="clean-up"></a><span data-ttu-id="497d2-232">Czyszczenie</span><span class="sxs-lookup"><span data-stu-id="497d2-232">Clean up</span></span>
<span data-ttu-id="497d2-233">Możesz kontynuować tooincur opłaty za klaster hello jest uruchomiona, należy wziąć pod uwagę [Usuwanie klastra](service-fabric-get-started-azure-cluster.md#remove-the-cluster).</span><span class="sxs-lookup"><span data-stu-id="497d2-233">You continue tooincur charges while hello cluster is running, consider [deleting your cluster](service-fabric-get-started-azure-cluster.md#remove-the-cluster).</span></span>  <span data-ttu-id="497d2-234">[Klastry innych firm](http://tryazureservicefabric.westus.cloudapp.azure.com/) są automatycznie usuwane po kilku godzinach.</span><span class="sxs-lookup"><span data-stu-id="497d2-234">[Party clusters](http://tryazureservicefabric.westus.cloudapp.azure.com/) are automatically deleted after a few hours.</span></span>

<span data-ttu-id="497d2-235">Po push hello obrazu toohello kontenera rejestru na komputerze projektowym można usunąć obrazu lokalne powitania:</span><span class="sxs-lookup"><span data-stu-id="497d2-235">After you push hello image toohello container registry you can delete hello local image from your development computer:</span></span>

```
docker rmi helloworldapp
docker rmi myregistry.azurecr.io/samples/helloworldapp
```

## <a name="complete-example-service-fabric-application-and-service-manifests"></a><span data-ttu-id="497d2-236">Kompletny przykład aplikacji i manifestów usługi Service Fabric</span><span class="sxs-lookup"><span data-stu-id="497d2-236">Complete example Service Fabric application and service manifests</span></span>
<span data-ttu-id="497d2-237">Oto usługi pełną hello i manifestów aplikacji używane w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="497d2-237">Here are hello complete service and application manifests used in this article.</span></span>

### <a name="servicemanifestxml"></a><span data-ttu-id="497d2-238">ServiceManifest.xml</span><span class="sxs-lookup"><span data-stu-id="497d2-238">ServiceManifest.xml</span></span>
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
### <a name="applicationmanifestxml"></a><span data-ttu-id="497d2-239">ApplicationManifest.xml</span><span class="sxs-lookup"><span data-stu-id="497d2-239">ApplicationManifest.xml</span></span>
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

## <a name="configure-time-interval-before-container-is-force-terminated"></a><span data-ttu-id="497d2-240">Konfigurowanie interwału czasu wymuszania przerwania działania kontenera</span><span class="sxs-lookup"><span data-stu-id="497d2-240">Configure time interval before container is force terminated</span></span>

<span data-ttu-id="497d2-241">Przedział czasu dla toowait środowiska uruchomieniowego hello można skonfigurować przed usunięciem kontenera powitania po hello usunięcia usługi (lub Przenieś węzła tooanother) została uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="497d2-241">You can configure a time interval for hello runtime toowait before hello container is removed after hello service deletion (or a move tooanother node) has started.</span></span> <span data-ttu-id="497d2-242">Konfigurowanie interwał czasu hello wysyła hello `docker stop <time in seconds>` polecenia toohello kontenera.</span><span class="sxs-lookup"><span data-stu-id="497d2-242">Configuring hello time interval sends hello `docker stop <time in seconds>` command toohello container.</span></span>   <span data-ttu-id="497d2-243">Aby uzyskać więcej informacji, zobacz [docker stop](https://docs.docker.com/engine/reference/commandline/stop/).</span><span class="sxs-lookup"><span data-stu-id="497d2-243">For more detail, see [docker stop](https://docs.docker.com/engine/reference/commandline/stop/).</span></span> <span data-ttu-id="497d2-244">toowait interwał czasu Hello jest określony w hello `Hosting` sekcji.</span><span class="sxs-lookup"><span data-stu-id="497d2-244">hello time interval toowait is specified under hello `Hosting` section.</span></span> <span data-ttu-id="497d2-245">Witaj następującego fragmentu manifestu klastra pokazuje, jak tooset hello oczekiwania interwał:</span><span class="sxs-lookup"><span data-stu-id="497d2-245">hello following cluster manifest snippet shows how tooset hello wait interval:</span></span>

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
<span data-ttu-id="497d2-246">Witaj domyślny interwał ustawiono too10 sekund.</span><span class="sxs-lookup"><span data-stu-id="497d2-246">hello default time interval is set too10 seconds.</span></span> <span data-ttu-id="497d2-247">Ponieważ ta konfiguracja jest dynamiczny, config uaktualnić tylko na powitania klastra aktualizacje hello przekroczenia limitu czasu.</span><span class="sxs-lookup"><span data-stu-id="497d2-247">Since this configuration is dynamic, a config only upgrade on hello cluster updates hello timeout.</span></span> 


## <a name="configure-hello-runtime-tooremove-unused-container-images"></a><span data-ttu-id="497d2-248">Skonfiguruj tooremove środowiska uruchomieniowego hello kontenerem nieużywanych obrazów</span><span class="sxs-lookup"><span data-stu-id="497d2-248">Configure hello runtime tooremove unused container images</span></span>

<span data-ttu-id="497d2-249">Można skonfigurować tooremove klastra usługi sieć szkieletowa hello kontenerem nieużywanych obrazów z hello węzła.</span><span class="sxs-lookup"><span data-stu-id="497d2-249">You can configure hello Service Fabric cluster tooremove unused container images from hello node.</span></span> <span data-ttu-id="497d2-250">Ta konfiguracja pozwala przechwyceniem Jeśli zbyt wiele obrazów kontenera znajdują się w węźle hello toobe miejsca na dysku.</span><span class="sxs-lookup"><span data-stu-id="497d2-250">This configuration allows disk space toobe recaptured if too many container images are present on hello node.</span></span>  <span data-ttu-id="497d2-251">tooenable tej funkcji, hello aktualizacji `Hosting` sekcji w manifeście klastra hello pokazane na powitania po fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="497d2-251">tooenable this feature, update hello `Hosting` section in hello cluster manifest as shown in hello following snippet:</span></span> 


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

<span data-ttu-id="497d2-252">Do obrazów, które nie powinny być usuwane, można określić je w obszarze hello `ContainerImagesToSkip` parametru.</span><span class="sxs-lookup"><span data-stu-id="497d2-252">For images that should not be deleted, you can specify them under hello `ContainerImagesToSkip` parameter.</span></span> 



## <a name="next-steps"></a><span data-ttu-id="497d2-253">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="497d2-253">Next steps</span></span>
* <span data-ttu-id="497d2-254">Dowiedz się więcej o uruchamianiu [kontenerów w usłudze Service Fabric](service-fabric-containers-overview.md).</span><span class="sxs-lookup"><span data-stu-id="497d2-254">Learn more about running [containers on Service Fabric](service-fabric-containers-overview.md).</span></span>
* <span data-ttu-id="497d2-255">Witaj odczytu [wdrażanie aplikacji .NET w kontenerze](service-fabric-host-app-in-a-container.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="497d2-255">Read hello [Deploy a .NET application in a container](service-fabric-host-app-in-a-container.md) tutorial.</span></span>
* <span data-ttu-id="497d2-256">Dowiedz się więcej o hello sieci szkieletowej usług [cyklu życia aplikacji](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="497d2-256">Learn about hello Service Fabric [application life-cycle](service-fabric-application-lifecycle.md).</span></span>
* <span data-ttu-id="497d2-257">Wyewidencjonowanie hello [przykłady kodu kontenera usługi sieć szkieletowa](https://github.com/Azure-Samples/service-fabric-dotnet-containers) w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="497d2-257">Checkout hello [Service Fabric container code samples](https://github.com/Azure-Samples/service-fabric-dotnet-containers) on GitHub.</span></span>

[1]: ./media/service-fabric-get-started-containers/MyFirstContainerError.png
[2]: ./media/service-fabric-get-started-containers/MyFirstContainerReady.png
