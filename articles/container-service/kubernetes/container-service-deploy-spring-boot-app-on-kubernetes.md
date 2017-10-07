---
title: "aaaDeploy aplikacji rozruchu sieci Spring na Kubernetes usługi kontenera platformy Azure | Dokumentacja firmy Microsoft"
description: "Ten samouczek przeprowadzi Cię jednak hello kroki toodeploy aplikacja Spring rozruchu w klastrze Kubernetes w systemie Microsoft Azure."
services: container-service
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: container-service
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 08/04/2017
ms.author: asirveda;robmcm
ms.custom: mvc
ms.openlocfilehash: 2bf9df459f874a1f478f43cdd29992d86c370837
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-spring-boot-application-on-a-kubernetes-cluster-in-hello-azure-container-service"></a><span data-ttu-id="078cc-103">Wdrażanie aplikacji rozruchu Spring w klastrze Kubernetes w hello usługi kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="078cc-103">Deploy a Spring Boot Application on a Kubernetes Cluster in hello Azure Container Service</span></span>

<span data-ttu-id="078cc-104">Witaj  **[Spring Framework]**  popularnych struktura open source, który pomaga Java deweloperom tworzenie aplikacji interfejsu API, mobilne i sieci web.</span><span class="sxs-lookup"><span data-stu-id="078cc-104">hello **[Spring Framework]** is a popular open-source framework that helps Java developers create web, mobile, and API applications.</span></span> <span data-ttu-id="078cc-105">W tym samouczku używana przykładowej aplikacji utworzony za pomocą [rozruchu Spring], podejście oparte na Konwencji poświęcone Spring tooget szybko rozpocząć pracę.</span><span class="sxs-lookup"><span data-stu-id="078cc-105">This tutorial uses a sample app created using [Spring Boot], a convention-driven approach for using Spring tooget started quickly.</span></span>

<span data-ttu-id="078cc-106">**[Kubernetes]**  i  **[Docker]**  są rozwiązania open source, które ułatwiają deweloperom automatyzację wdrażania hello, skalowania i zarządzania swoje aplikacje uruchomione w kontenerach.</span><span class="sxs-lookup"><span data-stu-id="078cc-106">**[Kubernetes]** and **[Docker]** are open-source solutions that help developers automate hello deployment, scaling, and management of their applications  running in containers.</span></span>

<span data-ttu-id="078cc-107">Ten samouczek przeprowadzi Cię, jeśli połączenie tych dwóch popularnych open source technologii toodevelop i wdrażanie rozruchu Spring tooMicrosoft aplikacji Azure.</span><span class="sxs-lookup"><span data-stu-id="078cc-107">This tutorial walks you though combining these two popular, open-source technologies toodevelop and deploy a Spring Boot application tooMicrosoft Azure.</span></span> <span data-ttu-id="078cc-108">W szczególności, użyj  *[rozruchu Spring]*  przy projektowaniu aplikacji,  *[Kubernetes]*  wdrożenia kontenera i hello [Usługi kontenera platformy azure (ACS)] toohost aplikacji.</span><span class="sxs-lookup"><span data-stu-id="078cc-108">More specifically, you use *[Spring Boot]* for application development, *[Kubernetes]* for container deployment, and hello [Azure Container Service (ACS)] toohost your application.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="078cc-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="078cc-109">Prerequisites</span></span>

* <span data-ttu-id="078cc-110">Subskrypcja platformy Azure; Jeśli nie masz jeszcze subskrypcji platformy Azure, możesz przeprowadzić aktywację Twojej [korzyści dla subskrybentów MSDN] lub zarejestrować się w celu [bezpłatne konto platformy Azure].</span><span class="sxs-lookup"><span data-stu-id="078cc-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="078cc-111">Witaj [Azure interfejsu wiersza polecenia (CLI)].</span><span class="sxs-lookup"><span data-stu-id="078cc-111">hello [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="078cc-112">Aktualne [Java Developer Kit (JDK)].</span><span class="sxs-lookup"><span data-stu-id="078cc-112">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="078cc-113">Apache na [Maven] (w wersji 3) Narzędzie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="078cc-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="078cc-114">A [Git] klienta.</span><span class="sxs-lookup"><span data-stu-id="078cc-114">A [Git] client.</span></span>
* <span data-ttu-id="078cc-115">A [Docker] klienta.</span><span class="sxs-lookup"><span data-stu-id="078cc-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="078cc-116">Ze względu na wymagania dotyczące wirtualizacji toohello tego samouczka nie można wykonać hello opisanych w tym artykule na maszynie wirtualnej; należy użyć komputera fizycznego z włączonymi funkcjami wirtualizacji.</span><span class="sxs-lookup"><span data-stu-id="078cc-116">Due toohello virtualization requirements of this tutorial, you cannot follow hello steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-hello-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="078cc-117">Utwórz hello Spring rozruchowego na wprowadzenie Docker aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="078cc-117">Create hello Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="078cc-118">Witaj następujące kroki opisano tworzenie aplikacji sieci web Spring rozruchu i testowanie go lokalnie.</span><span class="sxs-lookup"><span data-stu-id="078cc-118">hello following steps walk you through building a Spring Boot web application and testing it locally.</span></span>

1. <span data-ttu-id="078cc-119">Otwórz wiersz polecenia i utworzyć toohold lokalnego katalogu aplikacji i zmień katalog toothat; na przykład:</span><span class="sxs-lookup"><span data-stu-id="078cc-119">Open a command-prompt and create a local directory toohold your application, and change toothat directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="078cc-120">--lub--</span><span class="sxs-lookup"><span data-stu-id="078cc-120">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="078cc-121">Witaj w klonowania [rozruchu Spring na wprowadzenie Docker] przykładowy projekt do katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="078cc-121">Clone hello [Spring Boot on Docker Getting Started] sample project into hello directory.</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="078cc-122">Zmień katalog projektu toohello ukończone.</span><span class="sxs-lookup"><span data-stu-id="078cc-122">Change directory toohello completed project.</span></span>
   ```
   cd gs-spring-boot-docker
   cd complete
   ```

1. <span data-ttu-id="078cc-123">Użyj Maven toobuild i wykonywania hello przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="078cc-123">Use Maven toobuild and run hello sample app.</span></span>
   ```
   mvn package spring-boot:run
   ```

1. <span data-ttu-id="078cc-124">Test aplikacji sieci web hello przechodząc toohttp://localhost:8080 lub następujący hello `curl` polecenia:</span><span class="sxs-lookup"><span data-stu-id="078cc-124">Test hello web app by browsing toohttp://localhost:8080, or with hello following `curl` command:</span></span>
   ```
   curl http://localhost:8080
   ```

1. <span data-ttu-id="078cc-125">Powinien zostać wyświetlony komunikat wyświetlany po hello: **Hello Docker World**</span><span class="sxs-lookup"><span data-stu-id="078cc-125">You should see hello following message displayed: **Hello Docker World**</span></span>

   ![Przejdź do przykładowej aplikacji lokalnie][SB01]

## <a name="create-an-azure-container-registry-using-hello-azure-cli"></a><span data-ttu-id="078cc-127">Tworzenie przy użyciu interfejsu wiersza polecenia Azure hello rejestru kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="078cc-127">Create an Azure Container Registry using hello Azure CLI</span></span>

1. <span data-ttu-id="078cc-128">Otwórz wiersz polecenia.</span><span class="sxs-lookup"><span data-stu-id="078cc-128">Open a command prompt.</span></span>

1. <span data-ttu-id="078cc-129">Zaloguj się tooyour konto platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="078cc-129">Log in tooyour Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="078cc-130">Utwórz grupę zasobów dla hello Azure zasoby używane w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="078cc-130">Create a resource group for hello Azure resources used in this tutorial.</span></span>
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=eastus
   ```

1. <span data-ttu-id="078cc-131">Utwórz rejestru prywatnej kontenera platformy Azure w grupie zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="078cc-131">Create a private Azure container registry in hello resource group.</span></span> <span data-ttu-id="078cc-132">Samouczek Hello wypycha hello przykładową aplikację jako rejestru toothis Docker obrazu w kolejnych krokach.</span><span class="sxs-lookup"><span data-stu-id="078cc-132">hello tutorial pushes hello sample app as a Docker image toothis registry in later steps.</span></span> <span data-ttu-id="078cc-133">Zastąp `wingtiptoysregistry` o unikatowej nazwie dla rejestru.</span><span class="sxs-lookup"><span data-stu-id="078cc-133">Replace `wingtiptoysregistry` with a unique name for your registry.</span></span>
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoys-kubernetes--location eastus \
    --name wingtiptoysregistry --sku Basic
   ```

## <a name="push-your-app-toohello-container-registry"></a><span data-ttu-id="078cc-134">Wypychanie rejestru kontenera toohello aplikacji</span><span class="sxs-lookup"><span data-stu-id="078cc-134">Push your app toohello container registry</span></span>

1. <span data-ttu-id="078cc-135">Przejdź do katalogu konfiguracji toohello instalacji Maven (~/.m2/ domyślne lub C:\Users\username\.m2) i otwórz hello *settings.xml* plik w edytorze tekstów.</span><span class="sxs-lookup"><span data-stu-id="078cc-135">Navigate toohello configuration directory for your Maven installation (default ~/.m2/ or C:\Users\username\.m2) and open hello *settings.xml* file with a text editor.</span></span>

1. <span data-ttu-id="078cc-136">Pobrać hasło hello rejestru kontenera z hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="078cc-136">Retrieve hello password for your container registry from hello Azure CLI.</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```

   ```json
   {
  "name": "password",
  "value": "AbCdEfGhIjKlMnOpQrStUvWxYz"
   }
   ```

1. <span data-ttu-id="078cc-137">Dodaj z rejestru kontenera Azure id i hasła tooa nowe `<server>` kolekcji w hello *settings.xml* pliku.</span><span class="sxs-lookup"><span data-stu-id="078cc-137">Add your Azure Container Registry id and password tooa new `<server>` collection in hello *settings.xml* file.</span></span>
<span data-ttu-id="078cc-138">Witaj `id` i `username` są nazwa hello hello rejestru.</span><span class="sxs-lookup"><span data-stu-id="078cc-138">hello `id` and `username` are hello name of hello registry.</span></span> <span data-ttu-id="078cc-139">Użyj hello `password` wartość z zakresu od poprzedniego polecenia hello (bez cudzysłowów).</span><span class="sxs-lookup"><span data-stu-id="078cc-139">Use hello `password` value from hello previous command (without quotes).</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. <span data-ttu-id="078cc-140">Przejdź do katalogu projektu toohello ukończone aplikacji Spring rozruchu (na przykład "*C:\SpringBoot\gs-spring-boot-docker\complete*"lub"*/users/robert/SpringBoot/gs-spring-boot-docker / pełne*") i otwórz hello *pom.xml* plik w edytorze tekstów.</span><span class="sxs-lookup"><span data-stu-id="078cc-140">Navigate toohello completed project directory for your Spring Boot application (for example, "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open hello *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="078cc-141">Aktualizacja hello `<properties>` kolekcji w hello *pom.xml* pliku z wartością serwera logowania hello rejestru kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="078cc-141">Update hello `<properties>` collection in hello *pom.xml* file with hello login server value for your Azure Container Registry.</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="078cc-142">Aktualizacja hello `<plugins>` kolekcji w hello *pom.xml* pliku, który hello `<plugin>` zawiera powitania serwera adres i rejestru nazwę logowania dla rejestr kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="078cc-142">Update hello `<plugins>` collection in hello *pom.xml* file so that hello `<plugin>` contains hello login server address and registry name for your Azure Container Registry.</span></span>

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
         <serverId>wingtiptoysregistry</serverId>
         <registryUrl>https://wingtiptoysregistry.azurecr.io</registryUrl>
      </configuration>
   </plugin>
   ```

1. <span data-ttu-id="078cc-143">Przejdź do katalogu projektu toohello ukończone aplikacji Spring rozruchu i uruchom następujące polecenie toobuild hello Docker kontenera i wypychania hello obrazu toohello rejestru hello:</span><span class="sxs-lookup"><span data-stu-id="078cc-143">Navigate toohello completed project directory for your Spring Boot application and run hello following command toobuild hello Docker container and push hello image toohello registry:</span></span>

   ```
   mvn package docker:build -DpushImage
   ```

> [!NOTE]
>
>  <span data-ttu-id="078cc-144">Użytkownik może zostać wyświetlony komunikat o błędzie jest podobny tooone hello następującego przypadku Maven wypchnięcia tooAzure obrazu hello:</span><span class="sxs-lookup"><span data-stu-id="078cc-144">You may receive an error message that is similar tooone of hello following when Maven pushes hello image tooAzure:</span></span>
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> <span data-ttu-id="078cc-145">Jeśli ten błąd wystąpi, zaloguj się za tooAzure z wiersza polecenia Docker hello.</span><span class="sxs-lookup"><span data-stu-id="078cc-145">If you get this error, log in tooAzure from hello Docker command line.</span></span>
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> <span data-ttu-id="078cc-146">Następnie Wypchnij z kontenera:</span><span class="sxs-lookup"><span data-stu-id="078cc-146">Then push your container:</span></span>
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`

## <a name="create-a-kubernetes-cluster-on-acs-using-hello-azure-cli"></a><span data-ttu-id="078cc-147">Tworzenie klastra Kubernetes na ACS za pomocą hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="078cc-147">Create a Kubernetes Cluster on ACS using hello Azure CLI</span></span>

1. <span data-ttu-id="078cc-148">Utwórz klaster Kubernetes usługi kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="078cc-148">Create a Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="078cc-149">Witaj poniższe polecenie tworzy *kubernetes* klastra w hello *wingtiptoys kubernetes* zasobów grupy z *wingtiptoys containerservice* jako klaster hello Nazwa i *wingtiptoys kubernetes* jako prefiks DNS hello:</span><span class="sxs-lookup"><span data-stu-id="078cc-149">hello following command creates a *kubernetes* cluster in hello *wingtiptoys-kubernetes* resource group, with *wingtiptoys-containerservice* as hello cluster name, and *wingtiptoys-kubernetes* as hello DNS prefix:</span></span>
   ```azurecli
   az acs create --orchestrator-type=kubernetes --resource-group=wingtiptoys-kubernetes \ 
    --name=wingtiptoys-containerservice --dns-prefix=wingtiptoys-kubernetes
   ```
   <span data-ttu-id="078cc-150">Polecenie to może chwilę potrwać toocomplete.</span><span class="sxs-lookup"><span data-stu-id="078cc-150">This command may take a while toocomplete.</span></span>

1. <span data-ttu-id="078cc-151">Zainstaluj `kubectl` przy użyciu hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="078cc-151">Install `kubectl` using hello Azure CLI.</span></span> <span data-ttu-id="078cc-152">Użytkownicy systemu Linux mogą mieć tooprefix, to polecenie z `sudo` ponieważ wdraża hello Kubernetes CLI zbyt`/usr/local/bin`.</span><span class="sxs-lookup"><span data-stu-id="078cc-152">Linux users may have tooprefix this command with `sudo` since it deploys hello Kubernetes CLI too`/usr/local/bin`.</span></span>
   ```azurecli
   az acs kubernetes install-cli
   ```

1. <span data-ttu-id="078cc-153">Pobierz informacje o konfiguracji klastra hello tak klastra można zarządzać za pomocą interfejsu sieci web Kubernetes hello i `kubectl`.</span><span class="sxs-lookup"><span data-stu-id="078cc-153">Download hello cluster configuration information so you can manage your cluster from hello Kubernetes web interface and `kubectl`.</span></span> 
   ```azurecli
   az acs kubernetes get-credentials --resource-group=wingtiptoys-kubernetes  \ 
    --name=wingtiptoys-containerservice
   ```

## <a name="deploy-hello-image-tooyour-kubernetes-cluster"></a><span data-ttu-id="078cc-154">Wdrażanie klastra Kubernetes tooyour obraz powitania</span><span class="sxs-lookup"><span data-stu-id="078cc-154">Deploy hello image tooyour Kubernetes cluster</span></span>

<span data-ttu-id="078cc-155">W tym samouczku wdraża przy użyciu aplikacji hello `kubectl`, pozwoli Ci tooexplore hello wdrożenia za pośrednictwem interfejsu sieci web Kubernetes hello.</span><span class="sxs-lookup"><span data-stu-id="078cc-155">This tutorial deploys hello app using `kubectl`, then allow you tooexplore hello deployment through hello Kubernetes web interface.</span></span>

### <a name="deploy-with-hello-kubernetes-web-interface"></a><span data-ttu-id="078cc-156">Rozmieszczanie za pomocą interfejsu sieci web Kubernetes hello</span><span class="sxs-lookup"><span data-stu-id="078cc-156">Deploy with hello Kubernetes web interface</span></span>

1. <span data-ttu-id="078cc-157">Otwórz wiersz polecenia.</span><span class="sxs-lookup"><span data-stu-id="078cc-157">Open a command prompt.</span></span>

1. <span data-ttu-id="078cc-158">Otwórz hello konfiguracji witryny sieci Web dla klastra Kubernetes w domyślnej przeglądarce:</span><span class="sxs-lookup"><span data-stu-id="078cc-158">Open hello configuration website for your Kubernetes cluster in your default browser:</span></span>
   ```
   az acs kubernetes browse --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-containerservice
   ```

1. <span data-ttu-id="078cc-159">Po otwarciu hello Kubernetes konfiguracji witryny sieci Web w przeglądarce, kliknij łącze hello zbyt**wdrażania konteneryzowanych aplikacji**:</span><span class="sxs-lookup"><span data-stu-id="078cc-159">When hello Kubernetes configuration website opens in your browser, click hello link too**deploy a containerized app**:</span></span>

   ![Kubernetes konfiguracji witryny sieci Web][KB01]

1. <span data-ttu-id="078cc-161">Gdy hello **wdrażania konteneryzowanych aplikacji** zostanie wyświetlona strona, określ hello następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="078cc-161">When hello **Deploy a containerized app** page is displayed, specify hello following options:</span></span>

   <span data-ttu-id="078cc-162">a.</span><span class="sxs-lookup"><span data-stu-id="078cc-162">a.</span></span> <span data-ttu-id="078cc-163">Wybierz **Określ szczegóły aplikacji poniżej**.</span><span class="sxs-lookup"><span data-stu-id="078cc-163">Select **Specify app details below**.</span></span>

   <span data-ttu-id="078cc-164">b.</span><span class="sxs-lookup"><span data-stu-id="078cc-164">b.</span></span> <span data-ttu-id="078cc-165">Wprowadź nazwę aplikacji Spring rozruchu dla hello **Nazwa aplikacji**, na przykład: "*gs-spring — rozruchu — docker*".</span><span class="sxs-lookup"><span data-stu-id="078cc-165">Enter your Spring Boot application name for hello **App name**; for example: "*gs-spring-boot-docker*".</span></span>

   <span data-ttu-id="078cc-166">c.</span><span class="sxs-lookup"><span data-stu-id="078cc-166">c.</span></span> <span data-ttu-id="078cc-167">Wprowadź nazwy logowania serwera i kontener obrazu z wcześniej hello **obrazu kontenera**, na przykład: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".</span><span class="sxs-lookup"><span data-stu-id="078cc-167">Enter your login server and container image from earlier for hello **Container image**; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".</span></span>

   <span data-ttu-id="078cc-168">d.</span><span class="sxs-lookup"><span data-stu-id="078cc-168">d.</span></span> <span data-ttu-id="078cc-169">Wybierz **zewnętrznych** dla hello **usługi**.</span><span class="sxs-lookup"><span data-stu-id="078cc-169">Choose **External** for hello **Service**.</span></span>

   <span data-ttu-id="078cc-170">e.</span><span class="sxs-lookup"><span data-stu-id="078cc-170">e.</span></span> <span data-ttu-id="078cc-171">Określ sieci zewnętrznych i wewnętrznych portów w hello **portu** i **docelowy port** pól tekstowych.</span><span class="sxs-lookup"><span data-stu-id="078cc-171">Specify your external and internal ports in hello **Port** and **Target port** text boxes.</span></span>

   ![Kubernetes konfiguracji witryny sieci Web][KB02]


1. <span data-ttu-id="078cc-173">Kliknij przycisk **Wdróż** toodeploy hello kontenera.</span><span class="sxs-lookup"><span data-stu-id="078cc-173">Click **Deploy** toodeploy hello container.</span></span>

   ![Wdrażanie kontenera][KB05]

1. <span data-ttu-id="078cc-175">Po wdrożeniu aplikacji, zostanie wyświetlona aplikacji rozruchu Spring kategorii **usług**.</span><span class="sxs-lookup"><span data-stu-id="078cc-175">Once your application has been deployed, you will see your Spring Boot application listed under **Services**.</span></span>

   ![Kubernetes usług][KB06]

1. <span data-ttu-id="078cc-177">Po kliknięciu łącza hello **zewnętrzne punkty końcowe**, zobaczysz rozruchu Spring aplikacji działających na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="078cc-177">If you click hello link for **External endpoints**, you can see your Spring Boot application running on Azure.</span></span>

   ![Kubernetes usług][KB07]

   ![Przejdź do przykładowej aplikacji na platformie Azure][SB02]


### <a name="deploy-with-kubectl"></a><span data-ttu-id="078cc-180">Wdrażanie z kubectl</span><span class="sxs-lookup"><span data-stu-id="078cc-180">Deploy with kubectl</span></span>

1. <span data-ttu-id="078cc-181">Otwórz wiersz polecenia.</span><span class="sxs-lookup"><span data-stu-id="078cc-181">Open a command prompt.</span></span>

1. <span data-ttu-id="078cc-182">Uruchom z kontenera hello Kubernetes klastra przy użyciu hello `kubectl run` polecenia.</span><span class="sxs-lookup"><span data-stu-id="078cc-182">Run your container in hello Kubernetes cluster by using hello `kubectl run` command.</span></span> <span data-ttu-id="078cc-183">Nadaj nazwę usługi dla aplikacji na Kubernetes i hello pełnego obrazu.</span><span class="sxs-lookup"><span data-stu-id="078cc-183">Give a service name for your app in Kubernetes and hello full image name.</span></span> <span data-ttu-id="078cc-184">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="078cc-184">For example:</span></span>
   ```
   kubectl run gs-spring-boot-docker --image=wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest
   ```
   <span data-ttu-id="078cc-185">W tym poleceniu:</span><span class="sxs-lookup"><span data-stu-id="078cc-185">In this command:</span></span>

   * <span data-ttu-id="078cc-186">Nazwa kontenera Hello `gs-spring-boot-docker` określono natychmiast po hello `run` polecenia</span><span class="sxs-lookup"><span data-stu-id="078cc-186">hello container name `gs-spring-boot-docker` is specified immediately after hello `run` command</span></span>

   * <span data-ttu-id="078cc-187">Witaj `--image` parametr określa hello połączone nazwy logowania serwera i nazwa obrazu jako`wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span><span class="sxs-lookup"><span data-stu-id="078cc-187">hello `--image` parameter specifies hello combined login server and image name as `wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span></span>

1. <span data-ttu-id="078cc-188">Udostępnianie klastra Kubernetes zewnętrznie, używając hello `kubectl expose` polecenia.</span><span class="sxs-lookup"><span data-stu-id="078cc-188">Expose your Kubernetes cluster externally by using hello `kubectl expose` command.</span></span> <span data-ttu-id="078cc-189">Określ nazwę usługi, hello publicznych TCP port używany tooaccess hello aplikacji i hello wewnętrzny docelowy port, którego nasłuchuje aplikacji.</span><span class="sxs-lookup"><span data-stu-id="078cc-189">Specify your service name, hello public-facing TCP port used tooaccess hello app, and hello internal target port your app listens on.</span></span> <span data-ttu-id="078cc-190">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="078cc-190">For example:</span></span>
   ```
   kubectl expose deployment gs-spring-boot-docker --type=LoadBalancer --port=80 --target-port=8080
   ```
   <span data-ttu-id="078cc-191">W tym poleceniu:</span><span class="sxs-lookup"><span data-stu-id="078cc-191">In this command:</span></span>

   * <span data-ttu-id="078cc-192">Nazwa kontenera Hello `gs-spring-boot-docker` określono natychmiast po hello `expose deployment` polecenia</span><span class="sxs-lookup"><span data-stu-id="078cc-192">hello container name `gs-spring-boot-docker` is specified immediately after hello `expose deployment` command</span></span>

   * <span data-ttu-id="078cc-193">Witaj `--type` parametr określa klastra hello używa modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="078cc-193">hello `--type` parameter specifies that hello cluster uses load balancer</span></span>

   * <span data-ttu-id="078cc-194">Witaj `--port` parametr określa hello publicznych port TCP 80.</span><span class="sxs-lookup"><span data-stu-id="078cc-194">hello `--port` parameter specifies hello public-facing TCP port of 80.</span></span> <span data-ttu-id="078cc-195">Możesz uzyskać dostępu do aplikacji hello na tym porcie.</span><span class="sxs-lookup"><span data-stu-id="078cc-195">You access hello app on this port.</span></span>

   * <span data-ttu-id="078cc-196">Witaj `--target-port` parametr określa hello wewnętrznego portu TCP 8080.</span><span class="sxs-lookup"><span data-stu-id="078cc-196">hello `--target-port` parameter specifies hello internal TCP port of 8080.</span></span> <span data-ttu-id="078cc-197">Moduł równoważenia obciążenia Hello przekazuje żądania tooyour aplikacji na tym porcie.</span><span class="sxs-lookup"><span data-stu-id="078cc-197">hello load balancer forwards requests tooyour app on this port.</span></span>

1. <span data-ttu-id="078cc-198">Po wdrożeniu aplikacji hello klastra toohello zapytania hello zewnętrzny adres IP i otworzyć go w przeglądarce sieci web:</span><span class="sxs-lookup"><span data-stu-id="078cc-198">Once hello app is deployed toohello cluster, query hello external IP address and open it in your web browser:</span></span>

   ```
   kubectl get services -o jsonpath={.items[*].status.loadBalancer.ingress[0].ip} --namespace=${namespace}
   ```

   ![Przejdź do przykładowej aplikacji na platformie Azure][SB02]


## <a name="next-steps"></a><span data-ttu-id="078cc-200">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="078cc-200">Next steps</span></span>

<span data-ttu-id="078cc-201">Aby uzyskać więcej informacji na temat Spring rozruch przy użyciu na platformie Azure zobacz następujące artykuły hello:</span><span class="sxs-lookup"><span data-stu-id="078cc-201">For more information about using Spring Boot on Azure, see hello following articles:</span></span>

* [<span data-ttu-id="078cc-202">Wdrażanie aplikacji rozruchu Spring toohello usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="078cc-202">Deploy a Spring Boot Application toohello Azure App Service</span></span>](../../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)
* [<span data-ttu-id="078cc-203">Wdrażanie aplikacji Spring rozruchu w systemie Linux w hello usługi kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="078cc-203">Deploy a Spring Boot application on Linux in hello Azure Container Service</span></span>](container-service-deploy-spring-boot-app-on-linux.md)

<span data-ttu-id="078cc-204">Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz hello [Azure Java Developer Center] i hello [Java Tools for Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="078cc-204">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="078cc-205">Aby uzyskać więcej informacji na temat hello Spring rozruchu na Docker przykładowy projekt, zobacz [rozruchu Spring na wprowadzenie Docker].</span><span class="sxs-lookup"><span data-stu-id="078cc-205">For more information about hello Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="078cc-206">Witaj następującego łącza znajdują się dodatkowe informacje o tworzeniu aplikacji Spring rozruchu:</span><span class="sxs-lookup"><span data-stu-id="078cc-206">hello following links provide additional information about creating Spring Boot applications:</span></span>

* <span data-ttu-id="078cc-207">Aby uzyskać więcej informacji dotyczących tworzenia prostej aplikacji Spring rozruchu Zobacz hello Spring Initializr na https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="078cc-207">For more information about creating a simple Spring Boot application, see hello Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="078cc-208">Witaj poniższe linki udostępniają dodatkowe informacje dotyczące korzystania z usługi Azure Kubernetes:</span><span class="sxs-lookup"><span data-stu-id="078cc-208">hello following links provide additional information about using Kubernetes with Azure:</span></span>

* [<span data-ttu-id="078cc-209">Rozpoczynanie pracy z klastrem Kubernetes w usłudze kontenera</span><span class="sxs-lookup"><span data-stu-id="078cc-209">Get started with a Kubernetes cluster in Container Service</span></span>](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-walkthrough)
* [<span data-ttu-id="078cc-210">Przy użyciu hello Kubernetes interfejs użytkownika sieci web z usługi kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="078cc-210">Using hello Kubernetes web UI with Azure Container Service</span></span>](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-ui)

<span data-ttu-id="078cc-211">Więcej informacji na temat przy użyciu interfejsu wiersza polecenia Kubernetes jest dostępna w hello **kubectl** Podręcznik użytkownika w <https://kubernetes.io/docs/user-guide/kubectl/>.</span><span class="sxs-lookup"><span data-stu-id="078cc-211">More information about using Kubernetes command-line interface is available in hello **kubectl** user guide at <https://kubernetes.io/docs/user-guide/kubectl/>.</span></span>

<span data-ttu-id="078cc-212">Witaj Kubernetes witryny sieci Web ma kilka artykuł, w którym omówiono w nim przy użyciu obrazów w rejestrach prywatnych:</span><span class="sxs-lookup"><span data-stu-id="078cc-212">hello Kubernetes website has several articles that discuss using images in private registries:</span></span>

* <span data-ttu-id="078cc-213">[Konfigurowanie usługi konta dla stanowiskami]</span><span class="sxs-lookup"><span data-stu-id="078cc-213">[Configuring Service Accounts for Pods]</span></span>
* <span data-ttu-id="078cc-214">[Przestrzenie nazw]</span><span class="sxs-lookup"><span data-stu-id="078cc-214">[Namespaces]</span></span>
* <span data-ttu-id="078cc-215">[Ściąganie obrazu z rejestru prywatnych]</span><span class="sxs-lookup"><span data-stu-id="078cc-215">[Pulling an Image from a Private Registry]</span></span>

<span data-ttu-id="078cc-216">Aby uzyskać dodatkowe przykłady sposobu toouse Docker niestandardowe obrazy z platformy Azure, zobacz [dla aplikacji sieci Web platformy Azure w systemie Linux przy użyciu niestandardowego obrazu Docker].</span><span class="sxs-lookup"><span data-stu-id="078cc-216">For additional examples for how toouse custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

[Azure interfejsu wiersza polecenia (CLI)]: /cli/azure/overview
[Usługi kontenera platformy azure (ACS)]: https://azure.microsoft.com/services/container-service/
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using hello Azure portal]: /azure/container-registry/container-registry-get-started-portal
[dla aplikacji sieci Web platformy Azure w systemie Linux przy użyciu niestandardowego obrazu Docker]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[bezpłatne konto platformy Azure]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Kubernetes]: https://kubernetes.io/
[Kubernetes Command-Line Interface (kubectl)]: https://kubernetes.io/docs/user-guide/kubectl-overview/
[Maven]: http://maven.apache.org/
[korzyści dla subskrybentów MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[rozruchu Spring]: http://projects.spring.io/spring-boot/
[rozruchu Spring na wprowadzenie Docker]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/
[Konfigurowanie usługi konta dla stanowiskami]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/
[Przestrzenie nazw]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/
[Ściąganie obrazu z rejestru prywatnych]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/

<!-- IMG List -->

[SB01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/SB01.png
[SB02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/SB02.png

[AR01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR01.png
[AR02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR02.png
[AR03]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR03.png
[AR04]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR04.png

[KB01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB01.png
[KB02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB02.png
[KB03]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB03.png
[KB04]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB04.png
[KB05]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB05.png
[KB06]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB06.png
[KB07]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB07.png
