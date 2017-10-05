---
title: "Wdrażanie aplikacji sieci Web Spring rozruchu w systemie Linux w usłudze kontenera platformy Azure | Dokumentacja firmy Microsoft"
description: "Ten samouczek przedstawia jednak kroki, aby wdrożyć aplikację rozruchu Spring jako aplikacji sieci web systemu Linux w systemie Microsoft Azure."
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
ms.openlocfilehash: 5f0b470bd46cfeaf00b3092dbe9db507ed50f622
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-a-spring-boot-application-on-linux-in-the-azure-container-service"></a><span data-ttu-id="cfd06-103">Wdrażanie aplikacji Spring rozruchu w systemie Linux w usłudze kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="cfd06-103">Deploy a Spring Boot application on Linux in the Azure Container Service</span></span>

<span data-ttu-id="cfd06-104"> **[Spring Framework]**  to rozwiązanie open source, które pomaga deweloperom języka Java, tworzenie aplikacji na poziomie przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="cfd06-104">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="cfd06-105">Jeden z popularnych więcej projektów, które jest wbudowane znajdujący się na platformy jest [rozruchu Spring], zapewniające uproszczone podejście do tworzenia aplikacji Java autonomicznych.</span><span class="sxs-lookup"><span data-stu-id="cfd06-105">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span>

<span data-ttu-id="cfd06-106">**[Docker]**  jest rozwiązania open source, które pomaga deweloperom automatyzację wdrażania, skalowania i zarządzania ich aplikacji, które są uruchomione w kontenerach.</span><span class="sxs-lookup"><span data-stu-id="cfd06-106">**[Docker]** is open-source solutions that helps developers automate the deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="cfd06-107">Ten samouczek przedstawia przy użyciu rozwiązania Docker do opracowywania i wdrażania aplikacji Spring rozruchu na hoście z systemem Linux w [usługi kontenera platformy Azure (ACS)].</span><span class="sxs-lookup"><span data-stu-id="cfd06-107">This tutorial walks you through using Docker to develop and deploy a Spring Boot application to a Linux host in the [Azure Container Service (ACS)].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cfd06-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="cfd06-108">Prerequisites</span></span>

<span data-ttu-id="cfd06-109">Aby wykonać kroki opisane w tym samouczku, musisz mieć następujące wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="cfd06-109">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="cfd06-110">Subskrypcja platformy Azure; Jeśli nie masz jeszcze subskrypcji platformy Azure, możesz przeprowadzić aktywację Twojej [korzyści dla subskrybentów MSDN] lub zarejestrować się w celu [bezpłatne konto platformy Azure].</span><span class="sxs-lookup"><span data-stu-id="cfd06-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="cfd06-111">[Azure interfejsu wiersza polecenia (CLI)].</span><span class="sxs-lookup"><span data-stu-id="cfd06-111">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="cfd06-112">Aktualne [Java Developer Kit (JDK)].</span><span class="sxs-lookup"><span data-stu-id="cfd06-112">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="cfd06-113">Apache na [Maven] (w wersji 3) Narzędzie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="cfd06-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="cfd06-114">A [Git] klienta.</span><span class="sxs-lookup"><span data-stu-id="cfd06-114">A [Git] client.</span></span>
* <span data-ttu-id="cfd06-115">A [Docker] klienta.</span><span class="sxs-lookup"><span data-stu-id="cfd06-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="cfd06-116">Ze względu na wymagania dotyczące wirtualizacji w tym samouczku nie można wykonać kroki opisane w tym artykule na maszynie wirtualnej; należy użyć komputera fizycznego z włączonymi funkcjami wirtualizacji.</span><span class="sxs-lookup"><span data-stu-id="cfd06-116">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="cfd06-117">Utwórz rozruchu Spring na wprowadzenie Docker aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="cfd06-117">Create the Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="cfd06-118">W poniższych krokach objaśniono kroki, które są wymagane do tworzenia prostej aplikacji sieci web Spring rozruchu i przetestować go lokalnie.</span><span class="sxs-lookup"><span data-stu-id="cfd06-118">The following steps walk you through the steps that are required to create a simple Spring Boot web application and test it locally.</span></span>

1. <span data-ttu-id="cfd06-119">Otwórz wiersz polecenia i utworzyć katalogu lokalnego do przechowywania aplikacji, przejdź do tego katalogu; na przykład:</span><span class="sxs-lookup"><span data-stu-id="cfd06-119">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="cfd06-120">--lub--</span><span class="sxs-lookup"><span data-stu-id="cfd06-120">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="cfd06-121">Klonowanie [rozruchu Spring na wprowadzenie Docker] przykładowy projekt do katalogu utworzonego; na przykład:</span><span class="sxs-lookup"><span data-stu-id="cfd06-121">Clone the [Spring Boot on Docker Getting Started] sample project into the directory you created; for example:</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="cfd06-122">Zmień katalog na ukończone projektu; na przykład:</span><span class="sxs-lookup"><span data-stu-id="cfd06-122">Change directory to the completed project; for example:</span></span>
   ```
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="cfd06-123">Kompiluj plik JAR za pomocą programu Maven; na przykład:</span><span class="sxs-lookup"><span data-stu-id="cfd06-123">Build the JAR file using Maven; for example:</span></span>
   ```
   mvn package
   ```

1. <span data-ttu-id="cfd06-124">Po utworzeniu aplikacji sieci web, zmień katalog na `target` katalog w którym plik JAR znajduje się uruchomić aplikacji sieci web, na przykład:</span><span class="sxs-lookup"><span data-stu-id="cfd06-124">Once the web app has been created, change directory to the `target` directory where the JAR file is located and start the web app; for example:</span></span>
   ```
   cd target
   java -jar gs-spring-boot-docker-0.1.0.jar
   ```

1. <span data-ttu-id="cfd06-125">Testowanie aplikacji sieci web przy użyciu przeglądania lokalnie za pomocą przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="cfd06-125">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="cfd06-126">Na przykład jeśli masz curl dostępny i skonfigurowany serwer Tomcat do uruchomienia na porcie 80:</span><span class="sxs-lookup"><span data-stu-id="cfd06-126">For example, if you have curl available and you configured the Tomcat server to run on port 80:</span></span>
   ```
   curl http://localhost
   ```

1. <span data-ttu-id="cfd06-127">Powinien zostać wyświetlony następujący komunikat wyświetlany: **Hello, World Docker!**</span><span class="sxs-lookup"><span data-stu-id="cfd06-127">You should see the following message displayed: **Hello Docker World!**</span></span>

   ![Przejdź do przykładowej aplikacji lokalnie][SB01]

## <a name="create-an-azure-container-registry-to-use-as-a-private-docker-registry"></a><span data-ttu-id="cfd06-129">Tworzenie rejestru kontenera Azure ma być używana jako prywatnych rejestru Docker</span><span class="sxs-lookup"><span data-stu-id="cfd06-129">Create an Azure Container Registry to use as a Private Docker Registry</span></span>

<span data-ttu-id="cfd06-130">W poniższych krokach objaśniono przy użyciu portalu Azure można utworzyć rejestru kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="cfd06-130">The following steps walk you through using the Azure portal to create an Azure Container Registry.</span></span>

> [!NOTE]
>
> <span data-ttu-id="cfd06-131">Jeśli chcesz użyć wiersza polecenia platformy Azure zamiast portalu Azure, postępuj zgodnie z instrukcjami [tworzenie prywatnych rejestru kontenera Docker przy użyciu programu Azure CLI 2.0](../../container-registry/container-registry-get-started-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="cfd06-131">If you want to use the Azure CLI instead of the Azure portal, follow the steps in [Create a private Docker container registry using the Azure CLI 2.0](../../container-registry/container-registry-get-started-azure-cli.md).</span></span>
>

1. <span data-ttu-id="cfd06-132">Przejdź do [portalu Azure] i zaloguj się.</span><span class="sxs-lookup"><span data-stu-id="cfd06-132">Browse to the [Azure portal] and sign in.</span></span>

   <span data-ttu-id="cfd06-133">Po zalogowaniu się do swojego konta w portalu Azure, możesz wykonać kroki opisane w [tworzenie prywatnych rejestru kontenera Docker przy użyciu portalu Azure] artykułu, które są paraphrased w poniższych krokach dla sake z praktycznych.</span><span class="sxs-lookup"><span data-stu-id="cfd06-133">Once you have signed in to your account on the Azure portal, you can follow the steps in the [Create a private Docker container registry using the Azure portal] article, which are paraphrased in the following steps for the sake of expediency.</span></span>

1. <span data-ttu-id="cfd06-134">Kliknij ikonę menu **+ nowy**, następnie kliknij przycisk **kontenery**, a następnie kliknij przycisk **rejestru kontenera Azure**.</span><span class="sxs-lookup"><span data-stu-id="cfd06-134">Click the menu icon for **+ New**, then click **Containers**, and then click **Azure Container Registry**.</span></span>
   
   ![Tworzenie nowego rejestru kontenera platformy Azure][AR01]

1. <span data-ttu-id="cfd06-136">Po stronie informacje o szablonie rejestru kontenera Azure zostanie wyświetlony, kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="cfd06-136">When the information page for the Azure Container Registry template is displayed, click **Create**.</span></span> 

   ![Tworzenie nowego rejestru kontenera platformy Azure][AR02]

1. <span data-ttu-id="cfd06-138">Gdy **Utwórz kontener rejestru** zostanie wyświetlona strona, wprowadź Twojej **nazwa rejestru** i **grupy zasobów**, wybierz **włączyć** dla **Administrator**, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="cfd06-138">When the **Create container registry** page is displayed, enter your **Registry name** and **Resource group**, choose **Enable** for the **Admin user**, and then click **Create**.</span></span>

   ![Konfigurowanie ustawień rejestru kontenera platformy Azure][AR03]

1. <span data-ttu-id="cfd06-140">Po utworzeniu kontenera rejestru przejdź do kontenera rejestru w portalu Azure, a następnie kliknij przycisk **klucze dostępu**.</span><span class="sxs-lookup"><span data-stu-id="cfd06-140">Once your container registry has been created, navigate to your container registry in the Azure portal, and then click **Access Keys**.</span></span> <span data-ttu-id="cfd06-141">Zanotuj nazwę użytkownika i hasło dla następnych kroków.</span><span class="sxs-lookup"><span data-stu-id="cfd06-141">Take note of the username and password for the next steps.</span></span>

   ![Klawisze dostępu rejestru kontenera platformy Azure][AR04]

## <a name="configure-maven-to-use-your-azure-container-registry-access-keys"></a><span data-ttu-id="cfd06-143">Skonfiguruj Maven do używania kluczy dostępu rejestru kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="cfd06-143">Configure Maven to use your Azure Container Registry access keys</span></span>

1. <span data-ttu-id="cfd06-144">Przejdź do katalogu konfiguracji dla tej instalacji Maven i Otwórz *settings.xml* plik w edytorze tekstów.</span><span class="sxs-lookup"><span data-stu-id="cfd06-144">Navigate to the configuration directory for your Maven installation and open the *settings.xml* file with a text editor.</span></span>

1. <span data-ttu-id="cfd06-145">Dodaj ustawienia dostępu do rejestru kontenera Azure opisanych w poprzedniej części tego samouczka do `<servers>` kolekcji w *settings.xml* pliku; na przykład:</span><span class="sxs-lookup"><span data-stu-id="cfd06-145">Add your Azure Container Registry access settings from the previous section of this tutorial to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. <span data-ttu-id="cfd06-146">Przejdź do katalogu projektu zakończone aplikacji Spring rozruchu, (na przykład: "*C:\SpringBoot\gs-spring-boot-docker\complete*"lub"*/users/robert/SpringBoot/gs-spring-boot-docker/complete* "), a następnie otwórz *pom.xml* plik w edytorze tekstów.</span><span class="sxs-lookup"><span data-stu-id="cfd06-146">Navigate to the completed project directory for your Spring Boot application, (for example: "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="cfd06-147">Aktualizacja `<properties>` kolekcji w *pom.xml* pliku z wartością serwera logowania do rejestru kontenera Azure opisanych w poprzedniej części tego samouczka; na przykład:</span><span class="sxs-lookup"><span data-stu-id="cfd06-147">Update the `<properties>` collection in the *pom.xml* file with the login server value for your Azure Container Registry from the previous section of this tutorial; for example:</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="cfd06-148">Aktualizacja `<plugins>` kolekcji w *pom.xml* pliku, aby `<plugin>` zawiera logowania serwera adresu rejestru nazwę i rejestru kontenera Azure opisanych w poprzedniej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="cfd06-148">Update the `<plugins>` collection in the *pom.xml* file so that the `<plugin>` contains the login server address and registry name for your Azure Container Registry from the previous section of this tutorial.</span></span> <span data-ttu-id="cfd06-149">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="cfd06-149">For example:</span></span>

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

1. <span data-ttu-id="cfd06-150">Przejdź do katalogu projektu zakończone aplikacji Spring rozruchu i uruchom następujące polecenie, aby ponownie skompilować aplikację i push kontenera do rejestru kontenera platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="cfd06-150">Navigate to the completed project directory for your Spring Boot application and run the following command to rebuild the application and push the container to your Azure Container Registry:</span></span>

   ```
   mvn package docker:build -DpushImage 
   ```

> [!NOTE]
>
> <span data-ttu-id="cfd06-151">Gdy push z kontenera Docker na platformie Azure, otrzymasz komunikat o błędzie podobny do jednego z następujących nawet jeśli pomyślnie utworzono kontener programu Docker:</span><span class="sxs-lookup"><span data-stu-id="cfd06-151">When you are pushing your Docker container to Azure, you may receive an error message that is similar to one of the following even though your Docker container was created successfully:</span></span>
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> <span data-ttu-id="cfd06-152">W takim przypadku należy zalogować się do konta platformy Azure z poziomu wiersza polecenia Docker; na przykład:</span><span class="sxs-lookup"><span data-stu-id="cfd06-152">If this happens, you may need to sign in to your Azure account from the Docker command line; for example:</span></span>
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> <span data-ttu-id="cfd06-153">Następnie możesz wypchnąć z kontenera w wierszu polecenia; na przykład:</span><span class="sxs-lookup"><span data-stu-id="cfd06-153">You can then push your container from the command line; for example:</span></span>
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`
>

## <a name="create-a-web-app-on-linux-on-azure-app-service-using-your-container-image"></a><span data-ttu-id="cfd06-154">Tworzenie aplikacji sieci web w systemie Linux w usłudze Azure App Service przy użyciu obrazu kontenera</span><span class="sxs-lookup"><span data-stu-id="cfd06-154">Create a web app on Linux on Azure App Service using your container image</span></span>

1. <span data-ttu-id="cfd06-155">Przejdź do [portalu Azure] i zaloguj się.</span><span class="sxs-lookup"><span data-stu-id="cfd06-155">Browse to the [Azure portal] and sign in.</span></span>

1. <span data-ttu-id="cfd06-156">Kliknij ikonę menu **+ nowy**, następnie kliknij przycisk **sieci Web i mobilność**, a następnie kliknij przycisk **aplikacji sieci Web w systemie Linux**.</span><span class="sxs-lookup"><span data-stu-id="cfd06-156">Click the menu icon for **+ New**, then click **Web + Mobile**, and then click **Web App on Linux**.</span></span>
   
   ![Utwórz nową aplikację sieci web w portalu Azure][LX01]

1. <span data-ttu-id="cfd06-158">Gdy **aplikacji sieci Web w systemie Linux** zostanie wyświetlona strona, wprowadź następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="cfd06-158">When the **Web App on Linux** page is displayed, enter the following information:</span></span>

   <span data-ttu-id="cfd06-159">a.</span><span class="sxs-lookup"><span data-stu-id="cfd06-159">a.</span></span> <span data-ttu-id="cfd06-160">Wprowadź unikatową nazwę **Nazwa aplikacji**, na przykład: "*wingtiptoyslinux*."</span><span class="sxs-lookup"><span data-stu-id="cfd06-160">Enter a unique name for the **App name**; for example: "*wingtiptoyslinux*."</span></span>

   <span data-ttu-id="cfd06-161">b.</span><span class="sxs-lookup"><span data-stu-id="cfd06-161">b.</span></span> <span data-ttu-id="cfd06-162">Wybierz użytkownika **subskrypcji** z listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="cfd06-162">Choose your **Subscription** from the drop-down list.</span></span>

   <span data-ttu-id="cfd06-163">c.</span><span class="sxs-lookup"><span data-stu-id="cfd06-163">c.</span></span> <span data-ttu-id="cfd06-164">Wybierz istniejące **grupy zasobów**, lub określ nazwę, aby utworzyć nową grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="cfd06-164">Choose an existing **Resource Group**, or specify a name to create a new resource group.</span></span>

   <span data-ttu-id="cfd06-165">d.</span><span class="sxs-lookup"><span data-stu-id="cfd06-165">d.</span></span> <span data-ttu-id="cfd06-166">Kliknij przycisk **kontenera konfiguracji** i wprowadź następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="cfd06-166">Click **Configure container** and enter the following information:</span></span>

      * <span data-ttu-id="cfd06-167">Wybierz **prywatnej rejestru**.</span><span class="sxs-lookup"><span data-stu-id="cfd06-167">Choose **Private registry**.</span></span>

      * <span data-ttu-id="cfd06-168">**Obraz i opcjonalnie tag**: Określ nazwę kontenera z wcześniej, na przykład: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*"</span><span class="sxs-lookup"><span data-stu-id="cfd06-168">**Image and optional tag**: Specify your container name from earlier; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*"</span></span>

      * <span data-ttu-id="cfd06-169">**Adres URL serwera**: Określ adres URL rejestru z wcześniej, na przykład: "*https://wingtiptoysregistry.azurecr.io*"</span><span class="sxs-lookup"><span data-stu-id="cfd06-169">**Server URL**: Specify your registry URL from earlier; for example: "*https://wingtiptoysregistry.azurecr.io*"</span></span>

      * <span data-ttu-id="cfd06-170">**Nazwa użytkownika logowania** i **hasło**: Określ poświadczenia logowania z użytkownika **klucze dostępu** używanego w poprzednich krokach.</span><span class="sxs-lookup"><span data-stu-id="cfd06-170">**Login username** and **Password**: Specify your login credentials from your **Access Keys** that you used in previous steps.</span></span>
   
   <span data-ttu-id="cfd06-171">e.</span><span class="sxs-lookup"><span data-stu-id="cfd06-171">e.</span></span> <span data-ttu-id="cfd06-172">Po wprowadzeniu wszystkich powyższych informacji, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="cfd06-172">Once you have entered all of the above information, click **OK**.</span></span>

   ![Konfiguruj ustawienia aplikacji sieci web][LX02]

1. <span data-ttu-id="cfd06-174">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="cfd06-174">Click **Create**.</span></span>

> [!NOTE]
>
> <span data-ttu-id="cfd06-175">Azure automatycznie przypisze żądań internetowych do osadzonego serwer Tomcat, który działa na standardowe porty 80 lub 8080.</span><span class="sxs-lookup"><span data-stu-id="cfd06-175">Azure will automatically map Internet requests to embedded Tomcat server that is running on the standard ports of 80 or 8080.</span></span> <span data-ttu-id="cfd06-176">Jednak jeśli skonfigurowano serwer Tomcat osadzonych do uruchamiania na port niestandardowy, należy dodać zmienną środowiskową do aplikacji sieci web, który definiuje port serwera Tomcat osadzonych.</span><span class="sxs-lookup"><span data-stu-id="cfd06-176">However, if you configured your embedded Tomcat server to run on a custom port, you need to add an environment variable to your web app that defines the port for your embedded Tomcat server.</span></span> <span data-ttu-id="cfd06-177">Aby to zrobić, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="cfd06-177">To do so, use the following steps:</span></span>
>
> 1. <span data-ttu-id="cfd06-178">Przejdź do [portalu Azure] i zaloguj się.</span><span class="sxs-lookup"><span data-stu-id="cfd06-178">Browse to the [Azure portal] and sign in.</span></span>
> 
> 2. <span data-ttu-id="cfd06-179">Kliknij ikonę **usługi aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="cfd06-179">Click the icon for **App Services**.</span></span> <span data-ttu-id="cfd06-180">(Zobacz element #1 na obrazie poniżej).</span><span class="sxs-lookup"><span data-stu-id="cfd06-180">(See item #1 in the image below.)</span></span>
>
> 3. <span data-ttu-id="cfd06-181">Wybierz swoją aplikację internetową z listy.</span><span class="sxs-lookup"><span data-stu-id="cfd06-181">Select your web app from the list.</span></span> <span data-ttu-id="cfd06-182">(Element #2 na poniższym obrazie.)</span><span class="sxs-lookup"><span data-stu-id="cfd06-182">(Item #2 in the image below.)</span></span>
>
> 4. <span data-ttu-id="cfd06-183">Kliknij przycisk **ustawienia aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="cfd06-183">Click **Application Settings**.</span></span> <span data-ttu-id="cfd06-184">(Element #3 na poniższym obrazie.)</span><span class="sxs-lookup"><span data-stu-id="cfd06-184">(Item #3 in the image below.)</span></span>
>
> 5. <span data-ttu-id="cfd06-185">W **ustawień aplikacji** Dodaj nową zmienną środowiskową o nazwie **portu** i wprowadź numer portu niestandardowego dla wartości.</span><span class="sxs-lookup"><span data-stu-id="cfd06-185">In the **App settings** section, add a new environment variable named **PORT** and enter your custom port number for the value.</span></span> <span data-ttu-id="cfd06-186">(Element #4 obraz poniżej.)</span><span class="sxs-lookup"><span data-stu-id="cfd06-186">(Item #4 in the image below.)</span></span>
>
> 6. <span data-ttu-id="cfd06-187">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="cfd06-187">Click **Save**.</span></span> <span data-ttu-id="cfd06-188">(Element #5 na poniższej ilustracji.)</span><span class="sxs-lookup"><span data-stu-id="cfd06-188">(Item #5 in the image below.)</span></span>
>
> ![Zapisywanie niestandardowy numer portu w portalu Azure][LX03]
>

<!--
##  OPTIONAL: Configure the embedded Tomcat server to run on a different port

The embedded Tomcat server in the sample Spring Boot application is configured to run on port 8080 by default. However, if you want to run the embedded Tomcat server to run on a different port, such as port 80 for local testing, you can configure the port by using the following steps.

1. Go to the *resources* directory (or create the directory if it does not exist); for example:
   ```shell
   cd src/main/resources
   ```

1. Open the *application.yml* file in a text editor if it exists, or create a new YAML file if it does not exist.

1. Modify the **server** setting so that the server runs on port 80; for example:
   ```yaml
   server:
      port: 80
   ```

1. Save and close the *application.yml* file.
-->

## <a name="next-steps"></a><span data-ttu-id="cfd06-190">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cfd06-190">Next steps</span></span>

<span data-ttu-id="cfd06-191">Aby uzyskać więcej informacji o używaniu aplikacji rozruchu Spring na platformie Azure zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="cfd06-191">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="cfd06-192">Wdrażanie aplikacji rozruchu Spring w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="cfd06-192">Deploy a Spring Boot Application to the Azure App Service</span></span>](../../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)
* [<span data-ttu-id="cfd06-193">Wdrażanie aplikacji rozruchu Spring w klastrze Kubernetes w usłudze kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="cfd06-193">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="cfd06-194">Aby uzyskać więcej informacji o używaniu platformy Azure z językiem Java, zobacz [Centrum deweloperów języka Java dla platformy Azure] i [Java Tools for Visual Studio Team Services] (Narzędzia języka Java dla usługi Visual Studio Team Services).</span><span class="sxs-lookup"><span data-stu-id="cfd06-194">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="cfd06-195">Aby uzyskać dalsze informacje na temat rozruchu Spring na Docker przykładowy projekt, zobacz [rozruchu Spring na wprowadzenie Docker].</span><span class="sxs-lookup"><span data-stu-id="cfd06-195">For further details about the Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="cfd06-196">Aby uzyskać pomoc dotyczącą Rozpoczynanie pracy z aplikacjami Spring rozruchu, zobacz **Spring Initializr** na https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="cfd06-196">For help with getting started with your own Spring Boot applications, see the **Spring Initializr** at https://start.spring.io/.</span></span>

<span data-ttu-id="cfd06-197">Aby uzyskać więcej informacji na temat rozpoczynania pracy z tworzenia prostej aplikacji Spring rozruchu Zobacz Initializr Spring na https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="cfd06-197">For more information about getting started with creating a simple Spring Boot application, see the Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="cfd06-198">Dodatkowe przykłady korzystania z platformy Azure, niestandardowe obrazy usługi Docker można znaleźć [dla aplikacji sieci Web platformy Azure w systemie Linux przy użyciu niestandardowego obrazu Docker].</span><span class="sxs-lookup"><span data-stu-id="cfd06-198">For additional examples for how to use custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

<span data-ttu-id="cfd06-199">[Azure interfejsu wiersza polecenia (CLI)]: /cli/azure/overview</span><span class="sxs-lookup"><span data-stu-id="cfd06-199">[Azure Command-Line Interface (CLI)]: /cli/azure/overview</span></span>
<span data-ttu-id="cfd06-200">[usługi kontenera platformy Azure (ACS)]: https://azure.microsoft.com/services/container-service/</span><span class="sxs-lookup"><span data-stu-id="cfd06-200">[Azure Container Service (ACS)]: https://azure.microsoft.com/services/container-service/</span></span>
<span data-ttu-id="cfd06-201">[Centrum deweloperów języka Java dla platformy Azure]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="cfd06-201">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="cfd06-202">[portalu Azure]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="cfd06-202">[Azure portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="cfd06-203">[tworzenie prywatnych rejestru kontenera Docker przy użyciu portalu Azure]: /azure/container-registry/container-registry-get-started-portal</span><span class="sxs-lookup"><span data-stu-id="cfd06-203">[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal</span></span>
<span data-ttu-id="cfd06-204">[dla aplikacji sieci Web platformy Azure w systemie Linux przy użyciu niestandardowego obrazu Docker]: /azure/app-service-web/app-service-linux-using-custom-docker-image</span><span class="sxs-lookup"><span data-stu-id="cfd06-204">[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image</span></span>
<span data-ttu-id="cfd06-205">[Docker]: https://www.docker.com/</span><span class="sxs-lookup"><span data-stu-id="cfd06-205">[Docker]: https://www.docker.com/</span></span>
<span data-ttu-id="cfd06-206">[bezpłatne konto platformy Azure]: https://azure.microsoft.com/pricing/free-trial/</span><span class="sxs-lookup"><span data-stu-id="cfd06-206">[free Azure account]: https://azure.microsoft.com/pricing/free-trial/</span></span>
<span data-ttu-id="cfd06-207">[Git]: https://github.com/</span><span class="sxs-lookup"><span data-stu-id="cfd06-207">[Git]: https://github.com/</span></span>
<span data-ttu-id="cfd06-208">[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/</span><span class="sxs-lookup"><span data-stu-id="cfd06-208">[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/</span></span>
<span data-ttu-id="cfd06-209">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="cfd06-209">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>
<span data-ttu-id="cfd06-210">[Maven]: http://maven.apache.org/</span><span class="sxs-lookup"><span data-stu-id="cfd06-210">[Maven]: http://maven.apache.org/</span></span>
<span data-ttu-id="cfd06-211">[korzyści dla subskrybentów MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span><span class="sxs-lookup"><span data-stu-id="cfd06-211">[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span></span>
<span data-ttu-id="cfd06-212">[rozruchu Spring]: http://projects.spring.io/spring-boot/</span><span class="sxs-lookup"><span data-stu-id="cfd06-212">[Spring Boot]: http://projects.spring.io/spring-boot/</span></span>
<span data-ttu-id="cfd06-213">[rozruchu Spring na wprowadzenie Docker]: https://github.com/spring-guides/gs-spring-boot-docker</span><span class="sxs-lookup"><span data-stu-id="cfd06-213">[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker</span></span>
<span data-ttu-id="cfd06-214">[Spring Framework]: https://spring.io/</span><span class="sxs-lookup"><span data-stu-id="cfd06-214">[Spring Framework]: https://spring.io/</span></span>

<!-- IMG List -->

[SB01]: ./media/container-service-deploy-spring-boot-app-on-linux/SB01.png
[SB02]: ./media/container-service-deploy-spring-boot-app-on-linux/SB02.png

[AR01]: ./media/container-service-deploy-spring-boot-app-on-linux/AR01.png
[AR02]: ./media/container-service-deploy-spring-boot-app-on-linux/AR02.png
[AR03]: ./media/container-service-deploy-spring-boot-app-on-linux/AR03.png
[AR04]: ./media/container-service-deploy-spring-boot-app-on-linux/AR04.png

[LX01]: ./media/container-service-deploy-spring-boot-app-on-linux/LX01.png
[LX02]: ./media/container-service-deploy-spring-boot-app-on-linux/LX02.png
[LX03]: ./media/container-service-deploy-spring-boot-app-on-linux/LX03.png
