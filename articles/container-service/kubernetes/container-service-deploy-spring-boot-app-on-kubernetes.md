---
title: "Wdrażanie aplikacji rozruchu Spring na Kubernetes w usłudze kontenera platformy Azure | Dokumentacja firmy Microsoft"
description: "Ten samouczek przeprowadzi Cię, chociaż kroki, aby wdrożyć aplikację Spring rozruchu w Kubernetes klastra w systemie Microsoft Azure."
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
ms.openlocfilehash: 7f726436b2d459b8c16abb02e07de099abfd8974
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-a-spring-boot-application-on-a-kubernetes-cluster-in-the-azure-container-service"></a><span data-ttu-id="35e28-103">Wdrażanie aplikacji platformy Spring Boot w klastrze Kubernetes w usłudze Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="35e28-103">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>

<span data-ttu-id="35e28-104"> **[Spring Framework]**  popularnych struktura open source, który pomaga Java deweloperom tworzenie aplikacji interfejsu API, mobilne i sieci web.</span><span class="sxs-lookup"><span data-stu-id="35e28-104">The **[Spring Framework]** is a popular open-source framework that helps Java developers create web, mobile, and API applications.</span></span> <span data-ttu-id="35e28-105">W tym samouczku używana przykładowej aplikacji utworzony za pomocą [rozruchu Spring], podejście oparte na Konwencji do szybkie rozpoczęcie pracy przy użyciu źródła.</span><span class="sxs-lookup"><span data-stu-id="35e28-105">This tutorial uses a sample app created using [Spring Boot], a convention-driven approach for using Spring to get started quickly.</span></span>

<span data-ttu-id="35e28-106">**[Kubernetes]**  i  **[Docker]**  są rozwiązania open source, które ułatwiają deweloperom automatyzację wdrażania, skalowania i zarządzania swoje aplikacje uruchomione kontenery.</span><span class="sxs-lookup"><span data-stu-id="35e28-106">**[Kubernetes]** and **[Docker]** are open-source solutions that help developers automate the deployment, scaling, and management of their applications  running in containers.</span></span>

<span data-ttu-id="35e28-107">Ten samouczek przedstawia Chociaż połączenie tych dwóch popularnych open source technologii do opracowywania i wdrażania aplikacji Spring rozruchu w systemie Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="35e28-107">This tutorial walks you though combining these two popular, open-source technologies to develop and deploy a Spring Boot application to Microsoft Azure.</span></span> <span data-ttu-id="35e28-108">W szczególności, użyj  *[rozruchu Spring]*  przy projektowaniu aplikacji,  *[Kubernetes]*  wdrożenia kontenera i [ Usługa kontenera platformy Azure (ACS)] do hostowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="35e28-108">More specifically, you use *[Spring Boot]* for application development, *[Kubernetes]* for container deployment, and the [Azure Container Service (ACS)] to host your application.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="35e28-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="35e28-109">Prerequisites</span></span>

* <span data-ttu-id="35e28-110">Subskrypcja platformy Azure; Jeśli nie masz jeszcze subskrypcji platformy Azure, możesz przeprowadzić aktywację Twojej [korzyści dla subskrybentów MSDN] lub zarejestrować się w celu [bezpłatne konto platformy Azure].</span><span class="sxs-lookup"><span data-stu-id="35e28-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="35e28-111">[Azure interfejsu wiersza polecenia (CLI)].</span><span class="sxs-lookup"><span data-stu-id="35e28-111">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="35e28-112">Aktualne [Java Developer Kit (JDK)].</span><span class="sxs-lookup"><span data-stu-id="35e28-112">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="35e28-113">Apache na [Maven] (w wersji 3) Narzędzie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="35e28-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="35e28-114">A [Git] klienta.</span><span class="sxs-lookup"><span data-stu-id="35e28-114">A [Git] client.</span></span>
* <span data-ttu-id="35e28-115">A [Docker] klienta.</span><span class="sxs-lookup"><span data-stu-id="35e28-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="35e28-116">Ze względu na wymagania dotyczące wirtualizacji w tym samouczku nie można wykonać kroki opisane w tym artykule na maszynie wirtualnej; należy użyć komputera fizycznego z włączonymi funkcjami wirtualizacji.</span><span class="sxs-lookup"><span data-stu-id="35e28-116">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="35e28-117">Utwórz rozruchu Spring na wprowadzenie Docker aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="35e28-117">Create the Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="35e28-118">W poniższych krokach objaśniono sposób tworzenia aplikacji sieci web Spring rozruchu i testowanie go lokalnie.</span><span class="sxs-lookup"><span data-stu-id="35e28-118">The following steps walk you through building a Spring Boot web application and testing it locally.</span></span>

1. <span data-ttu-id="35e28-119">Otwórz wiersz polecenia i utworzyć katalogu lokalnego do przechowywania aplikacji, przejdź do tego katalogu; na przykład:</span><span class="sxs-lookup"><span data-stu-id="35e28-119">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="35e28-120">--lub--</span><span class="sxs-lookup"><span data-stu-id="35e28-120">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="35e28-121">Klonowanie [rozruchu Spring na wprowadzenie Docker] przykładowy projekt do katalogu.</span><span class="sxs-lookup"><span data-stu-id="35e28-121">Clone the [Spring Boot on Docker Getting Started] sample project into the directory.</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="35e28-122">Zmień katalog projektu zakończone.</span><span class="sxs-lookup"><span data-stu-id="35e28-122">Change directory to the completed project.</span></span>
   ```
   cd gs-spring-boot-docker
   cd complete
   ```

1. <span data-ttu-id="35e28-123">Używanie programu Maven do tworzenia i uruchamianie przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="35e28-123">Use Maven to build and run the sample app.</span></span>
   ```
   mvn package spring-boot:run
   ```

1. <span data-ttu-id="35e28-124">Testowanie aplikacji sieci web, przechodząc do adresem http://localhost: 8080 lub z następującymi `curl` polecenia:</span><span class="sxs-lookup"><span data-stu-id="35e28-124">Test the web app by browsing to http://localhost:8080, or with the following `curl` command:</span></span>
   ```
   curl http://localhost:8080
   ```

1. <span data-ttu-id="35e28-125">Powinien zostać wyświetlony następujący komunikat wyświetlany: **Hello, World Docker**</span><span class="sxs-lookup"><span data-stu-id="35e28-125">You should see the following message displayed: **Hello Docker World**</span></span>

   ![Przejdź do przykładowej aplikacji lokalnie][SB01]

## <a name="create-an-azure-container-registry-using-the-azure-cli"></a><span data-ttu-id="35e28-127">Tworzenie rejestru kontenera Azure za pomocą wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="35e28-127">Create an Azure Container Registry using the Azure CLI</span></span>

1. <span data-ttu-id="35e28-128">Otwórz wiersz polecenia.</span><span class="sxs-lookup"><span data-stu-id="35e28-128">Open a command prompt.</span></span>

1. <span data-ttu-id="35e28-129">Zaloguj się do konta platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="35e28-129">Log in to your Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="35e28-130">Utwórz grupę zasobów dla zasobów platformy Azure używana w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="35e28-130">Create a resource group for the Azure resources used in this tutorial.</span></span>
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=eastus
   ```

1. <span data-ttu-id="35e28-131">Utwórz rejestru prywatnej kontenera platformy Azure w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="35e28-131">Create a private Azure container registry in the resource group.</span></span> <span data-ttu-id="35e28-132">Samouczek wypychanie przykładową aplikację jako obraz Docker do tego rejestru w kolejnych krokach.</span><span class="sxs-lookup"><span data-stu-id="35e28-132">The tutorial pushes the sample app as a Docker image to this registry in later steps.</span></span> <span data-ttu-id="35e28-133">Zastąp `wingtiptoysregistry` o unikatowej nazwie dla rejestru.</span><span class="sxs-lookup"><span data-stu-id="35e28-133">Replace `wingtiptoysregistry` with a unique name for your registry.</span></span>
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoys-kubernetes--location eastus \
    --name wingtiptoysregistry --sku Basic
   ```

## <a name="push-your-app-to-the-container-registry"></a><span data-ttu-id="35e28-134">Wypychanie aplikację do rejestru kontenera</span><span class="sxs-lookup"><span data-stu-id="35e28-134">Push your app to the container registry</span></span>

1. <span data-ttu-id="35e28-135">Przejdź do katalogu konfiguracji dla tej instalacji Maven (~/.m2/ domyślne lub C:\Users\username\.m2), a następnie otwórz *settings.xml* plik w edytorze tekstów.</span><span class="sxs-lookup"><span data-stu-id="35e28-135">Navigate to the configuration directory for your Maven installation (default ~/.m2/ or C:\Users\username\.m2) and open the *settings.xml* file with a text editor.</span></span>

1. <span data-ttu-id="35e28-136">Pobrać hasło do rejestru kontenera z wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="35e28-136">Retrieve the password for your container registry from the Azure CLI.</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```

   ```json
   {
  "name": "password",
  "value": "AbCdEfGhIjKlMnOpQrStUvWxYz"
   }
   ```

1. <span data-ttu-id="35e28-137">Dodaj identyfikator rejestru kontenera Azure i hasło na nowy `<server>` kolekcji w *settings.xml* pliku.</span><span class="sxs-lookup"><span data-stu-id="35e28-137">Add your Azure Container Registry id and password to a new `<server>` collection in the *settings.xml* file.</span></span>
<span data-ttu-id="35e28-138">`id` i `username` są nazwa rejestru.</span><span class="sxs-lookup"><span data-stu-id="35e28-138">The `id` and `username` are the name of the registry.</span></span> <span data-ttu-id="35e28-139">Użyj `password` wartość z zakresu od poprzedniego polecenia (bez cudzysłowów).</span><span class="sxs-lookup"><span data-stu-id="35e28-139">Use the `password` value from the previous command (without quotes).</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. <span data-ttu-id="35e28-140">Przejdź do katalogu projektu zakończone aplikacji Spring rozruchu (na przykład "*C:\SpringBoot\gs-spring-boot-docker\complete*"lub"*/users/robert/SpringBoot/gs-spring-boot-docker/complete* "), a następnie otwórz *pom.xml* plik w edytorze tekstów.</span><span class="sxs-lookup"><span data-stu-id="35e28-140">Navigate to the completed project directory for your Spring Boot application (for example, "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="35e28-141">Aktualizacja `<properties>` kolekcji w *pom.xml* pliku z wartością serwera logowania do rejestru kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="35e28-141">Update the `<properties>` collection in the *pom.xml* file with the login server value for your Azure Container Registry.</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="35e28-142">Aktualizacja `<plugins>` kolekcji w *pom.xml* pliku, aby `<plugin>` zawiera logowania serwera adresu rejestru nazwę i rejestru kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="35e28-142">Update the `<plugins>` collection in the *pom.xml* file so that the `<plugin>` contains the login server address and registry name for your Azure Container Registry.</span></span>

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

1. <span data-ttu-id="35e28-143">Przejdź do katalogu projektu zakończone aplikacji Spring rozruchu i uruchom następujące polecenie, aby utworzyć kontener Docker i Wypchnij obrazu w rejestrze:</span><span class="sxs-lookup"><span data-stu-id="35e28-143">Navigate to the completed project directory for your Spring Boot application and run the following command to build the Docker container and push the image to the registry:</span></span>

   ```
   mvn package docker:build -DpushImage
   ```

> [!NOTE]
>
>  <span data-ttu-id="35e28-144">Użytkownik może zostać wyświetlony komunikat o błędzie jest podobny do jednego z następujących przypadku Maven wypchnięcia obrazu na platformie Azure:</span><span class="sxs-lookup"><span data-stu-id="35e28-144">You may receive an error message that is similar to one of the following when Maven pushes the image to Azure:</span></span>
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> <span data-ttu-id="35e28-145">Jeśli ten błąd, zaloguj się do platformy Azure z poziomu wiersza polecenia Docker.</span><span class="sxs-lookup"><span data-stu-id="35e28-145">If you get this error, log in to Azure from the Docker command line.</span></span>
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> <span data-ttu-id="35e28-146">Następnie Wypchnij z kontenera:</span><span class="sxs-lookup"><span data-stu-id="35e28-146">Then push your container:</span></span>
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`

## <a name="create-a-kubernetes-cluster-on-acs-using-the-azure-cli"></a><span data-ttu-id="35e28-147">Tworzenie klastra Kubernetes na ACS za pomocą wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="35e28-147">Create a Kubernetes Cluster on ACS using the Azure CLI</span></span>

1. <span data-ttu-id="35e28-148">Utwórz klaster Kubernetes usługi kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="35e28-148">Create a Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="35e28-149">Poniższe polecenie tworzy *kubernetes* klastra w *wingtiptoys kubernetes* zasobów grupy z *wingtiptoys containerservice* jako nazwę klastra i *wingtiptoys kubernetes* jako DNS prefiksu:</span><span class="sxs-lookup"><span data-stu-id="35e28-149">The following command creates a *kubernetes* cluster in the *wingtiptoys-kubernetes* resource group, with *wingtiptoys-containerservice* as the cluster name, and *wingtiptoys-kubernetes* as the DNS prefix:</span></span>
   ```azurecli
   az acs create --orchestrator-type=kubernetes --resource-group=wingtiptoys-kubernetes \ 
    --name=wingtiptoys-containerservice --dns-prefix=wingtiptoys-kubernetes
   ```
   <span data-ttu-id="35e28-150">To polecenie może zająć trochę czasu, aby zakończyć.</span><span class="sxs-lookup"><span data-stu-id="35e28-150">This command may take a while to complete.</span></span>

1. <span data-ttu-id="35e28-151">Zainstaluj `kubectl` przy użyciu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="35e28-151">Install `kubectl` using the Azure CLI.</span></span> <span data-ttu-id="35e28-152">Linux użytkownicy mogą mieć do prefiksu to polecenie z `sudo` ponieważ wdrażania Kubernetes CLI `/usr/local/bin`.</span><span class="sxs-lookup"><span data-stu-id="35e28-152">Linux users may have to prefix this command with `sudo` since it deploys the Kubernetes CLI to `/usr/local/bin`.</span></span>
   ```azurecli
   az acs kubernetes install-cli
   ```

1. <span data-ttu-id="35e28-153">Pobierz informacje o konfiguracji klastra, klaster można zarządzać za pomocą interfejsu sieci web Kubernetes i `kubectl`.</span><span class="sxs-lookup"><span data-stu-id="35e28-153">Download the cluster configuration information so you can manage your cluster from the Kubernetes web interface and `kubectl`.</span></span> 
   ```azurecli
   az acs kubernetes get-credentials --resource-group=wingtiptoys-kubernetes  \ 
    --name=wingtiptoys-containerservice
   ```

## <a name="deploy-the-image-to-your-kubernetes-cluster"></a><span data-ttu-id="35e28-154">Wdrażanie obrazu do klastra Kubernetes</span><span class="sxs-lookup"><span data-stu-id="35e28-154">Deploy the image to your Kubernetes cluster</span></span>

<span data-ttu-id="35e28-155">W tym samouczku wdraża aplikacje przy użyciu funkcji `kubectl`, umożliwiają następnie eksplorować wdrożenia za pomocą interfejsu sieci web Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="35e28-155">This tutorial deploys the app using `kubectl`, then allow you to explore the deployment through the Kubernetes web interface.</span></span>

### <a name="deploy-with-the-kubernetes-web-interface"></a><span data-ttu-id="35e28-156">Rozmieszczanie za pomocą interfejsu sieci web Kubernetes</span><span class="sxs-lookup"><span data-stu-id="35e28-156">Deploy with the Kubernetes web interface</span></span>

1. <span data-ttu-id="35e28-157">Otwórz wiersz polecenia.</span><span class="sxs-lookup"><span data-stu-id="35e28-157">Open a command prompt.</span></span>

1. <span data-ttu-id="35e28-158">Otwórz konfigurację witryny sieci Web dla klastra Kubernetes w domyślnej przeglądarce:</span><span class="sxs-lookup"><span data-stu-id="35e28-158">Open the configuration website for your Kubernetes cluster in your default browser:</span></span>
   ```
   az acs kubernetes browse --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-containerservice
   ```

1. <span data-ttu-id="35e28-159">Po otwarciu Kubernetes konfiguracji witryny sieci Web w przeglądarce, kliknij łącze, aby **wdrażania konteneryzowanych aplikacji**:</span><span class="sxs-lookup"><span data-stu-id="35e28-159">When the Kubernetes configuration website opens in your browser, click the link to **deploy a containerized app**:</span></span>

   ![Kubernetes konfiguracji witryny sieci Web][KB01]

1. <span data-ttu-id="35e28-161">Gdy **wdrażania konteneryzowanych aplikacji** zostanie wyświetlona strona, określ następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="35e28-161">When the **Deploy a containerized app** page is displayed, specify the following options:</span></span>

   <span data-ttu-id="35e28-162">a.</span><span class="sxs-lookup"><span data-stu-id="35e28-162">a.</span></span> <span data-ttu-id="35e28-163">Wybierz **Określ szczegóły aplikacji poniżej**.</span><span class="sxs-lookup"><span data-stu-id="35e28-163">Select **Specify app details below**.</span></span>

   <span data-ttu-id="35e28-164">b.</span><span class="sxs-lookup"><span data-stu-id="35e28-164">b.</span></span> <span data-ttu-id="35e28-165">Wprowadź nazwę aplikacji Spring rozruchu dla **Nazwa aplikacji**, na przykład: "*gs-spring — rozruchu — docker*".</span><span class="sxs-lookup"><span data-stu-id="35e28-165">Enter your Spring Boot application name for the **App name**; for example: "*gs-spring-boot-docker*".</span></span>

   <span data-ttu-id="35e28-166">c.</span><span class="sxs-lookup"><span data-stu-id="35e28-166">c.</span></span> <span data-ttu-id="35e28-167">Wprowadź identyfikator logowania serwera i kontener obrazu z wcześniej **obrazu kontenera**, na przykład: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".</span><span class="sxs-lookup"><span data-stu-id="35e28-167">Enter your login server and container image from earlier for the **Container image**; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".</span></span>

   <span data-ttu-id="35e28-168">d.</span><span class="sxs-lookup"><span data-stu-id="35e28-168">d.</span></span> <span data-ttu-id="35e28-169">Wybierz **zewnętrznych** dla **usługi**.</span><span class="sxs-lookup"><span data-stu-id="35e28-169">Choose **External** for the **Service**.</span></span>

   <span data-ttu-id="35e28-170">e.</span><span class="sxs-lookup"><span data-stu-id="35e28-170">e.</span></span> <span data-ttu-id="35e28-171">Określ sieci zewnętrznych i wewnętrznych portów w **portu** i **docelowy port** pól tekstowych.</span><span class="sxs-lookup"><span data-stu-id="35e28-171">Specify your external and internal ports in the **Port** and **Target port** text boxes.</span></span>

   ![Kubernetes konfiguracji witryny sieci Web][KB02]


1. <span data-ttu-id="35e28-173">Kliknij przycisk **Wdróż** celu wdrożenia kontenera.</span><span class="sxs-lookup"><span data-stu-id="35e28-173">Click **Deploy** to deploy the container.</span></span>

   ![Wdrażanie kontenera][KB05]

1. <span data-ttu-id="35e28-175">Po wdrożeniu aplikacji, zostanie wyświetlona aplikacji rozruchu Spring kategorii **usług**.</span><span class="sxs-lookup"><span data-stu-id="35e28-175">Once your application has been deployed, you will see your Spring Boot application listed under **Services**.</span></span>

   ![Kubernetes usług][KB06]

1. <span data-ttu-id="35e28-177">Jeśli klikniesz link do **zewnętrzne punkty końcowe**, zobaczysz rozruchu Spring aplikacji działających na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="35e28-177">If you click the link for **External endpoints**, you can see your Spring Boot application running on Azure.</span></span>

   ![Kubernetes usług][KB07]

   ![Przejdź do przykładowej aplikacji na platformie Azure][SB02]


### <a name="deploy-with-kubectl"></a><span data-ttu-id="35e28-180">Wdrażanie z kubectl</span><span class="sxs-lookup"><span data-stu-id="35e28-180">Deploy with kubectl</span></span>

1. <span data-ttu-id="35e28-181">Otwórz wiersz polecenia.</span><span class="sxs-lookup"><span data-stu-id="35e28-181">Open a command prompt.</span></span>

1. <span data-ttu-id="35e28-182">Uruchom z kontenera w klastrze Kubernetes przy użyciu `kubectl run` polecenia.</span><span class="sxs-lookup"><span data-stu-id="35e28-182">Run your container in the Kubernetes cluster by using the `kubectl run` command.</span></span> <span data-ttu-id="35e28-183">Nadaj nazwę usługi dla aplikacji na Kubernetes i nazwę pełnego obrazu.</span><span class="sxs-lookup"><span data-stu-id="35e28-183">Give a service name for your app in Kubernetes and the full image name.</span></span> <span data-ttu-id="35e28-184">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="35e28-184">For example:</span></span>
   ```
   kubectl run gs-spring-boot-docker --image=wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest
   ```
   <span data-ttu-id="35e28-185">W tym poleceniu:</span><span class="sxs-lookup"><span data-stu-id="35e28-185">In this command:</span></span>

   * <span data-ttu-id="35e28-186">Nazwa kontenera `gs-spring-boot-docker` określono natychmiast po `run` polecenia</span><span class="sxs-lookup"><span data-stu-id="35e28-186">The container name `gs-spring-boot-docker` is specified immediately after the `run` command</span></span>

   * <span data-ttu-id="35e28-187">`--image` Parametr określa nazwę serwera i obrazu połączonego logowania jako`wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span><span class="sxs-lookup"><span data-stu-id="35e28-187">The `--image` parameter specifies the combined login server and image name as `wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span></span>

1. <span data-ttu-id="35e28-188">Udostępnianie klastra Kubernetes zewnętrznie przy użyciu `kubectl expose` polecenia.</span><span class="sxs-lookup"><span data-stu-id="35e28-188">Expose your Kubernetes cluster externally by using the `kubectl expose` command.</span></span> <span data-ttu-id="35e28-189">Określ nazwę usługi, port TCP publicznych umożliwiają dostęp do aplikacji i port docelowy wewnętrznego, które nasłuchuje aplikacja.</span><span class="sxs-lookup"><span data-stu-id="35e28-189">Specify your service name, the public-facing TCP port used to access the app, and the internal target port your app listens on.</span></span> <span data-ttu-id="35e28-190">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="35e28-190">For example:</span></span>
   ```
   kubectl expose deployment gs-spring-boot-docker --type=LoadBalancer --port=80 --target-port=8080
   ```
   <span data-ttu-id="35e28-191">W tym poleceniu:</span><span class="sxs-lookup"><span data-stu-id="35e28-191">In this command:</span></span>

   * <span data-ttu-id="35e28-192">Nazwa kontenera `gs-spring-boot-docker` określono natychmiast po `expose deployment` polecenia</span><span class="sxs-lookup"><span data-stu-id="35e28-192">The container name `gs-spring-boot-docker` is specified immediately after the `expose deployment` command</span></span>

   * <span data-ttu-id="35e28-193">`--type` Parametr określa, że klaster używa modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="35e28-193">The `--type` parameter specifies that the cluster uses load balancer</span></span>

   * <span data-ttu-id="35e28-194">`--port` Parametr określa publicznych port TCP 80.</span><span class="sxs-lookup"><span data-stu-id="35e28-194">The `--port` parameter specifies the public-facing TCP port of 80.</span></span> <span data-ttu-id="35e28-195">Możesz uzyskać dostępu do aplikacji na tym porcie.</span><span class="sxs-lookup"><span data-stu-id="35e28-195">You access the app on this port.</span></span>

   * <span data-ttu-id="35e28-196">`--target-port` Parametr określa wewnętrzny port TCP 8080.</span><span class="sxs-lookup"><span data-stu-id="35e28-196">The `--target-port` parameter specifies the internal TCP port of 8080.</span></span> <span data-ttu-id="35e28-197">Moduł równoważenia obciążenia przekazuje żądania do aplikacji na tym porcie.</span><span class="sxs-lookup"><span data-stu-id="35e28-197">The load balancer forwards requests to your app on this port.</span></span>

1. <span data-ttu-id="35e28-198">Po wdrożeniu aplikacji do klastra, zapytania zewnętrzny adres IP, a następnie otwórz go w przeglądarce sieci web:</span><span class="sxs-lookup"><span data-stu-id="35e28-198">Once the app is deployed to the cluster, query the external IP address and open it in your web browser:</span></span>

   ```
   kubectl get services -o jsonpath={.items[*].status.loadBalancer.ingress[0].ip} --namespace=${namespace}
   ```

   ![Przejdź do przykładowej aplikacji na platformie Azure][SB02]


## <a name="next-steps"></a><span data-ttu-id="35e28-200">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="35e28-200">Next steps</span></span>

<span data-ttu-id="35e28-201">Aby uzyskać więcej informacji na temat Spring rozruch przy użyciu na platformie Azure zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="35e28-201">For more information about using Spring Boot on Azure, see the following articles:</span></span>

* [<span data-ttu-id="35e28-202">Wdrażanie aplikacji rozruchu Spring w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="35e28-202">Deploy a Spring Boot Application to the Azure App Service</span></span>](../../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)
* [<span data-ttu-id="35e28-203">Wdrażanie aplikacji Spring rozruchu w systemie Linux w usłudze kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="35e28-203">Deploy a Spring Boot application on Linux in the Azure Container Service</span></span>](container-service-deploy-spring-boot-app-on-linux.md)

<span data-ttu-id="35e28-204">Aby uzyskać więcej informacji o używaniu platformy Azure z językiem Java, zobacz [Centrum deweloperów języka Java dla platformy Azure] i [Java Tools for Visual Studio Team Services] (Narzędzia języka Java dla usługi Visual Studio Team Services).</span><span class="sxs-lookup"><span data-stu-id="35e28-204">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="35e28-205">Aby uzyskać więcej informacji na temat rozruchu Spring na Docker przykładowy projekt, zobacz [rozruchu Spring na wprowadzenie Docker].</span><span class="sxs-lookup"><span data-stu-id="35e28-205">For more information about the Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="35e28-206">Poniższe linki udostępniają dodatkowe informacje na temat tworzenia aplikacji Spring rozruchu:</span><span class="sxs-lookup"><span data-stu-id="35e28-206">The following links provide additional information about creating Spring Boot applications:</span></span>

* <span data-ttu-id="35e28-207">Aby uzyskać więcej informacji dotyczących tworzenia prostej aplikacji Spring rozruchu Zobacz Initializr Spring na https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="35e28-207">For more information about creating a simple Spring Boot application, see the Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="35e28-208">Poniższe linki udostępniają dodatkowe informacje dotyczące korzystania z usługi Azure Kubernetes:</span><span class="sxs-lookup"><span data-stu-id="35e28-208">The following links provide additional information about using Kubernetes with Azure:</span></span>

* [<span data-ttu-id="35e28-209">Rozpoczynanie pracy z klastrem Kubernetes w usłudze kontenera</span><span class="sxs-lookup"><span data-stu-id="35e28-209">Get started with a Kubernetes cluster in Container Service</span></span>](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-walkthrough)
* [<span data-ttu-id="35e28-210">Przy użyciu interfejsu użytkownika sieci web Kubernetes z usługi kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="35e28-210">Using the Kubernetes web UI with Azure Container Service</span></span>](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-ui)

<span data-ttu-id="35e28-211">Więcej informacji na temat przy użyciu interfejsu wiersza polecenia Kubernetes jest dostępna w **kubectl** Podręcznik użytkownika w <https://kubernetes.io/docs/user-guide/kubectl/>.</span><span class="sxs-lookup"><span data-stu-id="35e28-211">More information about using Kubernetes command-line interface is available in the **kubectl** user guide at <https://kubernetes.io/docs/user-guide/kubectl/>.</span></span>

<span data-ttu-id="35e28-212">Kubernetes witryny sieci Web ma kilka artykuł, w którym omówiono w nim przy użyciu obrazów w rejestrach prywatnych:</span><span class="sxs-lookup"><span data-stu-id="35e28-212">The Kubernetes website has several articles that discuss using images in private registries:</span></span>

* <span data-ttu-id="35e28-213">[Konfigurowanie usługi konta dla stanowiskami]</span><span class="sxs-lookup"><span data-stu-id="35e28-213">[Configuring Service Accounts for Pods]</span></span>
* <span data-ttu-id="35e28-214">[Przestrzenie nazw]</span><span class="sxs-lookup"><span data-stu-id="35e28-214">[Namespaces]</span></span>
* <span data-ttu-id="35e28-215">[Ściąganie obrazu z rejestru prywatnych]</span><span class="sxs-lookup"><span data-stu-id="35e28-215">[Pulling an Image from a Private Registry]</span></span>

<span data-ttu-id="35e28-216">Dodatkowe przykłady korzystania z platformy Azure, niestandardowe obrazy usługi Docker można znaleźć [dla aplikacji sieci Web platformy Azure w systemie Linux przy użyciu niestandardowego obrazu Docker].</span><span class="sxs-lookup"><span data-stu-id="35e28-216">For additional examples for how to use custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

<span data-ttu-id="35e28-217">[Azure interfejsu wiersza polecenia (CLI)]: /cli/azure/overview</span><span class="sxs-lookup"><span data-stu-id="35e28-217">[Azure Command-Line Interface (CLI)]: /cli/azure/overview</span></span>
<span data-ttu-id="35e28-218">[ Usługa kontenera platformy Azure (ACS)]: https://azure.microsoft.com/services/container-service/</span><span class="sxs-lookup"><span data-stu-id="35e28-218">[Azure Container Service (ACS)]: https://azure.microsoft.com/services/container-service/</span></span>
<span data-ttu-id="35e28-219">[Centrum deweloperów języka Java dla platformy Azure]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="35e28-219">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
<span data-ttu-id="35e28-220">[dla aplikacji sieci Web platformy Azure w systemie Linux przy użyciu niestandardowego obrazu Docker]: /azure/app-service-web/app-service-linux-using-custom-docker-image</span><span class="sxs-lookup"><span data-stu-id="35e28-220">[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image</span></span>
<span data-ttu-id="35e28-221">[Docker]: https://www.docker.com/</span><span class="sxs-lookup"><span data-stu-id="35e28-221">[Docker]: https://www.docker.com/</span></span>
<span data-ttu-id="35e28-222">[bezpłatne konto platformy Azure]: https://azure.microsoft.com/pricing/free-trial/</span><span class="sxs-lookup"><span data-stu-id="35e28-222">[free Azure account]: https://azure.microsoft.com/pricing/free-trial/</span></span>
<span data-ttu-id="35e28-223">[Git]: https://github.com/</span><span class="sxs-lookup"><span data-stu-id="35e28-223">[Git]: https://github.com/</span></span>
<span data-ttu-id="35e28-224">[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/</span><span class="sxs-lookup"><span data-stu-id="35e28-224">[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/</span></span>
<span data-ttu-id="35e28-225">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="35e28-225">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>
<span data-ttu-id="35e28-226">[Kubernetes]: https://kubernetes.io/</span><span class="sxs-lookup"><span data-stu-id="35e28-226">[Kubernetes]: https://kubernetes.io/</span></span>
[Kubernetes Command-Line Interface (kubectl)]: https://kubernetes.io/docs/user-guide/kubectl-overview/
<span data-ttu-id="35e28-227">[Maven]: http://maven.apache.org/</span><span class="sxs-lookup"><span data-stu-id="35e28-227">[Maven]: http://maven.apache.org/</span></span>
<span data-ttu-id="35e28-228">[korzyści dla subskrybentów MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span><span class="sxs-lookup"><span data-stu-id="35e28-228">[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span></span>
<span data-ttu-id="35e28-229">[rozruchu Spring]: http://projects.spring.io/spring-boot/</span><span class="sxs-lookup"><span data-stu-id="35e28-229">[Spring Boot]: http://projects.spring.io/spring-boot/</span></span>
<span data-ttu-id="35e28-230">[rozruchu Spring na wprowadzenie Docker]: https://github.com/spring-guides/gs-spring-boot-docker</span><span class="sxs-lookup"><span data-stu-id="35e28-230">[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker</span></span>
<span data-ttu-id="35e28-231">[Spring Framework]: https://spring.io/</span><span class="sxs-lookup"><span data-stu-id="35e28-231">[Spring Framework]: https://spring.io/</span></span>
<span data-ttu-id="35e28-232">[Konfigurowanie usługi konta dla stanowiskami]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/</span><span class="sxs-lookup"><span data-stu-id="35e28-232">[Configuring Service Accounts for Pods]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/</span></span>
<span data-ttu-id="35e28-233">[Przestrzenie nazw]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/</span><span class="sxs-lookup"><span data-stu-id="35e28-233">[Namespaces]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/</span></span>
<span data-ttu-id="35e28-234">[Ściąganie obrazu z rejestru prywatnych]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/</span><span class="sxs-lookup"><span data-stu-id="35e28-234">[Pulling an Image from a Private Registry]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/</span></span>

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
