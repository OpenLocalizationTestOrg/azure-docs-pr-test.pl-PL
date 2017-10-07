---
title: "aaaDeploy aplikacji sieci Web Spring rozruchu w systemie Linux w usłudze kontenera platformy Azure | Dokumentacja firmy Microsoft"
description: Ten samouczek przedstawia jednak hello kroki toodeploy aplikacja rozruchu Spring jako aplikacji sieci web systemu Linux w systemie Microsoft Azure.
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
ms.openlocfilehash: 2c44be1c7f66a38f48239001f0be9e90c7e6edef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-spring-boot-application-on-linux-in-hello-azure-container-service"></a><span data-ttu-id="e7f61-103">Wdrażanie aplikacji Spring rozruchu w systemie Linux w hello usługi kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e7f61-103">Deploy a Spring Boot application on Linux in hello Azure Container Service</span></span>

<span data-ttu-id="e7f61-104">Witaj ** [Spring Framework] ** to rozwiązanie open source, które pomaga deweloperom języka Java, tworzenie aplikacji na poziomie przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="e7f61-104">hello **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="e7f61-105">Jednego z projektów innych popularnych hello, które jest wbudowane znajdujący się na platformie jest [rozruchu Spring], zapewniające uproszczone podejście do tworzenia aplikacji Java autonomicznych.</span><span class="sxs-lookup"><span data-stu-id="e7f61-105">One of hello more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span>

<span data-ttu-id="e7f61-106">**[Docker] ** jest rozwiązania open source, które pomaga deweloperom automatyzację wdrażania hello, skalowania i zarządzania ich aplikacji, które są uruchomione w kontenerach.</span><span class="sxs-lookup"><span data-stu-id="e7f61-106">**[Docker]** is open-source solutions that helps developers automate hello deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="e7f61-107">Ten samouczek przeprowadzi Cię przez kolejne przy użyciu Docker toodevelop i wdrażanie rozruchu Spring aplikacji tooa hoście z systemem Linux w hello [usługi kontenera platformy Azure (ACS)].</span><span class="sxs-lookup"><span data-stu-id="e7f61-107">This tutorial walks you through using Docker toodevelop and deploy a Spring Boot application tooa Linux host in hello [Azure Container Service (ACS)].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e7f61-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e7f61-108">Prerequisites</span></span>

<span data-ttu-id="e7f61-109">Kolejność toocomplete hello kroki w tym samouczku potrzebne hello toohave następujące wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="e7f61-109">In order toocomplete hello steps in this tutorial, you need toohave hello following prerequisites:</span></span>

* <span data-ttu-id="e7f61-110">Subskrypcja platformy Azure; Jeśli nie masz jeszcze subskrypcji platformy Azure, możesz przeprowadzić aktywację Twojej [korzyści dla subskrybentów MSDN] lub zarejestrować się w celu [bezpłatne konto platformy Azure].</span><span class="sxs-lookup"><span data-stu-id="e7f61-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="e7f61-111">Witaj [Azure interfejsu wiersza polecenia (CLI)].</span><span class="sxs-lookup"><span data-stu-id="e7f61-111">hello [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="e7f61-112">Aktualne [Java Developer Kit (JDK)].</span><span class="sxs-lookup"><span data-stu-id="e7f61-112">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="e7f61-113">Apache na [Maven] (w wersji 3) Narzędzie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="e7f61-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="e7f61-114">A [Git] klienta.</span><span class="sxs-lookup"><span data-stu-id="e7f61-114">A [Git] client.</span></span>
* <span data-ttu-id="e7f61-115">A [Docker] klienta.</span><span class="sxs-lookup"><span data-stu-id="e7f61-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="e7f61-116">Ze względu na wymagania dotyczące wirtualizacji toohello tego samouczka nie można wykonać hello opisanych w tym artykule na maszynie wirtualnej; należy użyć komputera fizycznego z włączonymi funkcjami wirtualizacji.</span><span class="sxs-lookup"><span data-stu-id="e7f61-116">Due toohello virtualization requirements of this tutorial, you cannot follow hello steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-hello-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="e7f61-117">Utwórz hello Spring rozruchowego na wprowadzenie Docker aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="e7f61-117">Create hello Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="e7f61-118">Witaj kolejnych krokach objaśniono sposób hello kroki, które są wymagane toocreate prostą aplikację sieci web Spring rozruchu i przetestować go lokalnie.</span><span class="sxs-lookup"><span data-stu-id="e7f61-118">hello following steps walk you through hello steps that are required toocreate a simple Spring Boot web application and test it locally.</span></span>

1. <span data-ttu-id="e7f61-119">Otwórz wiersz polecenia i utworzyć toohold lokalnego katalogu aplikacji i zmień katalog toothat; na przykład:</span><span class="sxs-lookup"><span data-stu-id="e7f61-119">Open a command-prompt and create a local directory toohold your application, and change toothat directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="e7f61-120">--lub--</span><span class="sxs-lookup"><span data-stu-id="e7f61-120">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="e7f61-121">Witaj w klonowania [rozruchu Spring na wprowadzenie Docker] przykładowy projekt do katalogu hello utworzony; na przykład:</span><span class="sxs-lookup"><span data-stu-id="e7f61-121">Clone hello [Spring Boot on Docker Getting Started] sample project into hello directory you created; for example:</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="e7f61-122">Zmień katalog projektu toohello ukończone; na przykład:</span><span class="sxs-lookup"><span data-stu-id="e7f61-122">Change directory toohello completed project; for example:</span></span>
   ```
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="e7f61-123">Kompiluj plik JAR hello za pomocą programu Maven; na przykład:</span><span class="sxs-lookup"><span data-stu-id="e7f61-123">Build hello JAR file using Maven; for example:</span></span>
   ```
   mvn package
   ```

1. <span data-ttu-id="e7f61-124">Po utworzeniu aplikacji sieci web hello zmienić katalogu toohello `target` katalog w którym plik JAR hello znajduje się uruchomić aplikacji sieci web hello; na przykład:</span><span class="sxs-lookup"><span data-stu-id="e7f61-124">Once hello web app has been created, change directory toohello `target` directory where hello JAR file is located and start hello web app; for example:</span></span>
   ```
   cd target
   java -jar gs-spring-boot-docker-0.1.0.jar
   ```

1. <span data-ttu-id="e7f61-125">Testowanie aplikacji sieci web hello przechodząc tooit lokalnie za pomocą przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="e7f61-125">Test hello web app by browsing tooit locally using a web browser.</span></span> <span data-ttu-id="e7f61-126">Na przykład jeśli masz curl dostępny i skonfigurowany toorun serwera Tomcat hello na porcie 80:</span><span class="sxs-lookup"><span data-stu-id="e7f61-126">For example, if you have curl available and you configured hello Tomcat server toorun on port 80:</span></span>
   ```
   curl http://localhost
   ```

1. <span data-ttu-id="e7f61-127">Powinien zostać wyświetlony komunikat wyświetlany po hello: **Hello Docker World!**</span><span class="sxs-lookup"><span data-stu-id="e7f61-127">You should see hello following message displayed: **Hello Docker World!**</span></span>

   ![Przejdź do przykładowej aplikacji lokalnie][SB01]

## <a name="create-an-azure-container-registry-toouse-as-a-private-docker-registry"></a><span data-ttu-id="e7f61-129">Utwórz toouse rejestru kontenera Azure jako prywatnych rejestru Docker</span><span class="sxs-lookup"><span data-stu-id="e7f61-129">Create an Azure Container Registry toouse as a Private Docker Registry</span></span>

<span data-ttu-id="e7f61-130">Witaj kolejnych krokach objaśniono sposób przy użyciu hello Azure toocreate portalu rejestru kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e7f61-130">hello following steps walk you through using hello Azure portal toocreate an Azure Container Registry.</span></span>

> [!NOTE]
>
> <span data-ttu-id="e7f61-131">Toouse hello Azure CLI zamiast hello portalu Azure, należy wykonać kroki hello [tworzenie prywatnych rejestru kontenera Docker przy użyciu hello Azure CLI 2.0](../../container-registry/container-registry-get-started-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="e7f61-131">If you want toouse hello Azure CLI instead of hello Azure portal, follow hello steps in [Create a private Docker container registry using hello Azure CLI 2.0](../../container-registry/container-registry-get-started-azure-cli.md).</span></span>
>

1. <span data-ttu-id="e7f61-132">Przeglądaj toohello [portalu Azure] i zaloguj się.</span><span class="sxs-lookup"><span data-stu-id="e7f61-132">Browse toohello [Azure portal] and sign in.</span></span>

   <span data-ttu-id="e7f61-133">Po zalogowaniu się na koncie tooyour na powitania portalu Azure, można wykonać kroki hello w hello [tworzenie prywatnych rejestru kontenera Docker przy użyciu portalu Azure hello] artykułu, które są paraphrased w hello następujące kroki dla hello zapewnienia praktycznych.</span><span class="sxs-lookup"><span data-stu-id="e7f61-133">Once you have signed in tooyour account on hello Azure portal, you can follow hello steps in hello [Create a private Docker container registry using hello Azure portal] article, which are paraphrased in hello following steps for hello sake of expediency.</span></span>

1. <span data-ttu-id="e7f61-134">Kliknij ikonę menu hello **+ nowy**, następnie kliknij przycisk **kontenery**, a następnie kliknij przycisk **rejestru kontenera Azure**.</span><span class="sxs-lookup"><span data-stu-id="e7f61-134">Click hello menu icon for **+ New**, then click **Containers**, and then click **Azure Container Registry**.</span></span>
   
   ![Tworzenie nowego rejestru kontenera platformy Azure][AR01]

1. <span data-ttu-id="e7f61-136">Gdy zostanie wyświetlona strona informacji hello hello rejestru kontenera Azure szablonu, kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="e7f61-136">When hello information page for hello Azure Container Registry template is displayed, click **Create**.</span></span> 

   ![Tworzenie nowego rejestru kontenera platformy Azure][AR02]

1. <span data-ttu-id="e7f61-138">Gdy hello **Utwórz kontener rejestru** zostanie wyświetlona strona, wprowadź użytkownika **nazwa rejestru** i **grupy zasobów**, wybierz **włączyć** dla Witaj **administrator**, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="e7f61-138">When hello **Create container registry** page is displayed, enter your **Registry name** and **Resource group**, choose **Enable** for hello **Admin user**, and then click **Create**.</span></span>

   ![Konfigurowanie ustawień rejestru kontenera platformy Azure][AR03]

1. <span data-ttu-id="e7f61-140">Po utworzeniu kontenera rejestru przejdź do klucza rejestru kontenera tooyour hello portalu Azure, a następnie kliknij **klucze dostępu**.</span><span class="sxs-lookup"><span data-stu-id="e7f61-140">Once your container registry has been created, navigate tooyour container registry in hello Azure portal, and then click **Access Keys**.</span></span> <span data-ttu-id="e7f61-141">Zwróć uwagę na powitania nazwę użytkownika i hasło hello następnych kroków.</span><span class="sxs-lookup"><span data-stu-id="e7f61-141">Take note of hello username and password for hello next steps.</span></span>

   ![Klawisze dostępu rejestru kontenera platformy Azure][AR04]

## <a name="configure-maven-toouse-your-azure-container-registry-access-keys"></a><span data-ttu-id="e7f61-143">Skonfiguruj Maven toouse klucze dostępu do rejestru kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e7f61-143">Configure Maven toouse your Azure Container Registry access keys</span></span>

1. <span data-ttu-id="e7f61-144">Przejdź do katalogu konfiguracji toohello instalacji Maven i otwórz hello *settings.xml* plik w edytorze tekstów.</span><span class="sxs-lookup"><span data-stu-id="e7f61-144">Navigate toohello configuration directory for your Maven installation and open hello *settings.xml* file with a text editor.</span></span>

1. <span data-ttu-id="e7f61-145">Dodaj ustawienia dostępu do rejestru kontenera Azure hello w poprzedniej sekcji tego samouczka toohello `<servers>` kolekcji w hello *settings.xml* pliku; na przykład:</span><span class="sxs-lookup"><span data-stu-id="e7f61-145">Add your Azure Container Registry access settings from hello previous section of this tutorial toohello `<servers>` collection in hello *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. <span data-ttu-id="e7f61-146">Przejdź do katalogu projektu ukończona toohello aplikacji Spring rozruchu, (na przykład: "*C:\SpringBoot\gs-spring-boot-docker\complete*"lub"*/users/robert/SpringBoot/gs-spring-boot-docker / pełne*") i otwórz hello *pom.xml* plik w edytorze tekstów.</span><span class="sxs-lookup"><span data-stu-id="e7f61-146">Navigate toohello completed project directory for your Spring Boot application, (for example: "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open hello *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="e7f61-147">Aktualizacja hello `<properties>` kolekcji w hello *pom.xml* pliku z wartością serwera logowania hello rejestru kontenera platformy Azure z poprzedniej sekcji hello tego samouczka; na przykład:</span><span class="sxs-lookup"><span data-stu-id="e7f61-147">Update hello `<properties>` collection in hello *pom.xml* file with hello login server value for your Azure Container Registry from hello previous section of this tutorial; for example:</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="e7f61-148">Aktualizacja hello `<plugins>` kolekcji w hello *pom.xml* pliku, który hello `<plugin>` zawiera powitania serwera adres i rejestru nazwę logowania dla rejestr kontenera platformy Azure z poprzedniej sekcji hello tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="e7f61-148">Update hello `<plugins>` collection in hello *pom.xml* file so that hello `<plugin>` contains hello login server address and registry name for your Azure Container Registry from hello previous section of this tutorial.</span></span> <span data-ttu-id="e7f61-149">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="e7f61-149">For example:</span></span>

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

1. <span data-ttu-id="e7f61-150">Przejdź do katalogu projektu toohello ukończone aplikacji Spring rozruchu i uruchom następujące polecenie toorebuild hello aplikacji hello i push hello kontenera tooyour rejestru kontenera Azure:</span><span class="sxs-lookup"><span data-stu-id="e7f61-150">Navigate toohello completed project directory for your Spring Boot application and run hello following command toorebuild hello application and push hello container tooyour Azure Container Registry:</span></span>

   ```
   mvn package docker:build -DpushImage 
   ```

> [!NOTE]
>
> <span data-ttu-id="e7f61-151">Gdy push Twojej tooAzure kontenera Docker może zostać wyświetlony komunikat o błędzie jest podobny tooone hello następujących, mimo że pomyślnie utworzono kontener programu Docker:</span><span class="sxs-lookup"><span data-stu-id="e7f61-151">When you are pushing your Docker container tooAzure, you may receive an error message that is similar tooone of hello following even though your Docker container was created successfully:</span></span>
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> <span data-ttu-id="e7f61-152">W takiej sytuacji może być konieczne toosign w tooyour konto platformy Azure z wiersza polecenia Docker hello; na przykład:</span><span class="sxs-lookup"><span data-stu-id="e7f61-152">If this happens, you may need toosign in tooyour Azure account from hello Docker command line; for example:</span></span>
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> <span data-ttu-id="e7f61-153">Następnie możesz wypchnąć z kontenera z wiersza polecenia hello; na przykład:</span><span class="sxs-lookup"><span data-stu-id="e7f61-153">You can then push your container from hello command line; for example:</span></span>
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`
>

## <a name="create-a-web-app-on-linux-on-azure-app-service-using-your-container-image"></a><span data-ttu-id="e7f61-154">Tworzenie aplikacji sieci web w systemie Linux w usłudze Azure App Service przy użyciu obrazu kontenera</span><span class="sxs-lookup"><span data-stu-id="e7f61-154">Create a web app on Linux on Azure App Service using your container image</span></span>

1. <span data-ttu-id="e7f61-155">Przeglądaj toohello [portalu Azure] i zaloguj się.</span><span class="sxs-lookup"><span data-stu-id="e7f61-155">Browse toohello [Azure portal] and sign in.</span></span>

1. <span data-ttu-id="e7f61-156">Kliknij ikonę menu hello **+ nowy**, następnie kliknij przycisk **sieci Web i mobilność**, a następnie kliknij przycisk **aplikacji sieci Web w systemie Linux**.</span><span class="sxs-lookup"><span data-stu-id="e7f61-156">Click hello menu icon for **+ New**, then click **Web + Mobile**, and then click **Web App on Linux**.</span></span>
   
   ![Utwórz nową aplikację sieci web w portalu Azure hello][LX01]

1. <span data-ttu-id="e7f61-158">Gdy hello **aplikacji sieci Web w systemie Linux** zostanie wyświetlona strona, wprowadź hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="e7f61-158">When hello **Web App on Linux** page is displayed, enter hello following information:</span></span>

   <span data-ttu-id="e7f61-159">a.</span><span class="sxs-lookup"><span data-stu-id="e7f61-159">a.</span></span> <span data-ttu-id="e7f61-160">Wprowadź unikatową nazwę hello **Nazwa aplikacji**, na przykład: "*wingtiptoyslinux*."</span><span class="sxs-lookup"><span data-stu-id="e7f61-160">Enter a unique name for hello **App name**; for example: "*wingtiptoyslinux*."</span></span>

   <span data-ttu-id="e7f61-161">b.</span><span class="sxs-lookup"><span data-stu-id="e7f61-161">b.</span></span> <span data-ttu-id="e7f61-162">Wybierz użytkownika **subskrypcji** z listy rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="e7f61-162">Choose your **Subscription** from hello drop-down list.</span></span>

   <span data-ttu-id="e7f61-163">c.</span><span class="sxs-lookup"><span data-stu-id="e7f61-163">c.</span></span> <span data-ttu-id="e7f61-164">Wybierz istniejące **grupy zasobów**, lub określ toocreate nazwę nowej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="e7f61-164">Choose an existing **Resource Group**, or specify a name toocreate a new resource group.</span></span>

   <span data-ttu-id="e7f61-165">d.</span><span class="sxs-lookup"><span data-stu-id="e7f61-165">d.</span></span> <span data-ttu-id="e7f61-166">Kliknij przycisk **kontenera konfiguracji** , a następnie wprowadź hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="e7f61-166">Click **Configure container** and enter hello following information:</span></span>

      * <span data-ttu-id="e7f61-167">Wybierz **prywatnej rejestru**.</span><span class="sxs-lookup"><span data-stu-id="e7f61-167">Choose **Private registry**.</span></span>

      * <span data-ttu-id="e7f61-168">**Obraz i opcjonalnie tag**: Określ nazwę kontenera z wcześniej, na przykład: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*"</span><span class="sxs-lookup"><span data-stu-id="e7f61-168">**Image and optional tag**: Specify your container name from earlier; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*"</span></span>

      * <span data-ttu-id="e7f61-169">**Adres URL serwera**: Określ adres URL rejestru z wcześniej, na przykład: "*https://wingtiptoysregistry.azurecr.io*"</span><span class="sxs-lookup"><span data-stu-id="e7f61-169">**Server URL**: Specify your registry URL from earlier; for example: "*https://wingtiptoysregistry.azurecr.io*"</span></span>

      * <span data-ttu-id="e7f61-170">**Nazwa użytkownika logowania** i **hasło**: Określ poświadczenia logowania z użytkownika **klucze dostępu** używanego w poprzednich krokach.</span><span class="sxs-lookup"><span data-stu-id="e7f61-170">**Login username** and **Password**: Specify your login credentials from your **Access Keys** that you used in previous steps.</span></span>
   
   <span data-ttu-id="e7f61-171">e.</span><span class="sxs-lookup"><span data-stu-id="e7f61-171">e.</span></span> <span data-ttu-id="e7f61-172">Po wprowadzeniu wszystkich hello powyżej informacji, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="e7f61-172">Once you have entered all of hello above information, click **OK**.</span></span>

   ![Konfiguruj ustawienia aplikacji sieci web][LX02]

1. <span data-ttu-id="e7f61-174">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="e7f61-174">Click **Create**.</span></span>

> [!NOTE]
>
> <span data-ttu-id="e7f61-175">Azure automatycznie przypisze Internet żądań tooembedded Tomcat serwera, który działa na standardowe porty hello 80 lub 8080.</span><span class="sxs-lookup"><span data-stu-id="e7f61-175">Azure will automatically map Internet requests tooembedded Tomcat server that is running on hello standard ports of 80 or 8080.</span></span> <span data-ttu-id="e7f61-176">Jednak z osadzonych toorun serwer Tomcat jest skonfigurowany na port niestandardowy, należy najpierw tooadd aplikacji sieci web tooyour zmiennej środowiska, który definiuje hello port serwera Tomcat osadzonych.</span><span class="sxs-lookup"><span data-stu-id="e7f61-176">However, if you configured your embedded Tomcat server toorun on a custom port, you need tooadd an environment variable tooyour web app that defines hello port for your embedded Tomcat server.</span></span> <span data-ttu-id="e7f61-177">toodo tak, użycie hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="e7f61-177">toodo so, use hello following steps:</span></span>
>
> 1. <span data-ttu-id="e7f61-178">Przeglądaj toohello [portalu Azure] i zaloguj się.</span><span class="sxs-lookup"><span data-stu-id="e7f61-178">Browse toohello [Azure portal] and sign in.</span></span>
> 
> 2. <span data-ttu-id="e7f61-179">Kliknij ikonę hello **usługi aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="e7f61-179">Click hello icon for **App Services**.</span></span> <span data-ttu-id="e7f61-180">(Zobacz poniższy obraz powitania element #1).</span><span class="sxs-lookup"><span data-stu-id="e7f61-180">(See item #1 in hello image below.)</span></span>
>
> 3. <span data-ttu-id="e7f61-181">Wybierz aplikację sieci web z listy hello.</span><span class="sxs-lookup"><span data-stu-id="e7f61-181">Select your web app from hello list.</span></span> <span data-ttu-id="e7f61-182">(Element #2 na poniższym obrazie hello.)</span><span class="sxs-lookup"><span data-stu-id="e7f61-182">(Item #2 in hello image below.)</span></span>
>
> 4. <span data-ttu-id="e7f61-183">Kliknij przycisk **ustawienia aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="e7f61-183">Click **Application Settings**.</span></span> <span data-ttu-id="e7f61-184">(Element #3 na poniższym obrazie hello.)</span><span class="sxs-lookup"><span data-stu-id="e7f61-184">(Item #3 in hello image below.)</span></span>
>
> 5. <span data-ttu-id="e7f61-185">W hello **ustawień aplikacji** Dodaj nową zmienną środowiskową o nazwie **portu** i wprowadź numer portu niestandardowego hello wartości.</span><span class="sxs-lookup"><span data-stu-id="e7f61-185">In hello **App settings** section, add a new environment variable named **PORT** and enter your custom port number for hello value.</span></span> <span data-ttu-id="e7f61-186">(Element #4 hello obraz poniżej.)</span><span class="sxs-lookup"><span data-stu-id="e7f61-186">(Item #4 in hello image below.)</span></span>
>
> 6. <span data-ttu-id="e7f61-187">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="e7f61-187">Click **Save**.</span></span> <span data-ttu-id="e7f61-188">(Element #5 na poniższym obrazie hello.)</span><span class="sxs-lookup"><span data-stu-id="e7f61-188">(Item #5 in hello image below.)</span></span>
>
> ![Zapisywanie niestandardowy numer portu w hello portalu Azure][LX03]
>

<!--
##  OPTIONAL: Configure hello embedded Tomcat server toorun on a different port

hello embedded Tomcat server in hello sample Spring Boot application is configured toorun on port 8080 by default. However, if you want toorun hello embedded Tomcat server toorun on a different port, such as port 80 for local testing, you can configure hello port by using hello following steps.

1. Go toohello *resources* directory (or create hello directory if it does not exist); for example:
   ```shell
   cd src/main/resources
   ```

1. Open hello *application.yml* file in a text editor if it exists, or create a new YAML file if it does not exist.

1. Modify hello **server** setting so that hello server runs on port 80; for example:
   ```yaml
   server:
      port: 80
   ```

1. Save and close hello *application.yml* file.
-->

## <a name="next-steps"></a><span data-ttu-id="e7f61-190">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e7f61-190">Next steps</span></span>

<span data-ttu-id="e7f61-191">Aby uzyskać więcej informacji o używaniu aplikacji rozruchu Spring na platformie Azure zobacz następujące artykuły hello:</span><span class="sxs-lookup"><span data-stu-id="e7f61-191">For more information about using Spring Boot applications on Azure, see hello following articles:</span></span>

* [<span data-ttu-id="e7f61-192">Wdrażanie aplikacji rozruchu Spring toohello usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="e7f61-192">Deploy a Spring Boot Application toohello Azure App Service</span></span>](../../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)
* [<span data-ttu-id="e7f61-193">Wdrażanie aplikacji rozruchu Spring w klastrze Kubernetes w hello usługi kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e7f61-193">Deploy a Spring Boot Application on a Kubernetes Cluster in hello Azure Container Service</span></span>](container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="e7f61-194">Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz hello [Azure Java Developer Center] i hello [Java Tools for Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="e7f61-194">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="e7f61-195">Aby uzyskać dalsze informacje na temat hello Spring rozruchowego na Docker przykładowy projekt, zobacz [rozruchu Spring na wprowadzenie Docker].</span><span class="sxs-lookup"><span data-stu-id="e7f61-195">For further details about hello Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="e7f61-196">Aby uzyskać pomoc dotyczącą Rozpoczynanie pracy z aplikacjami Spring rozruchu, zobacz hello **Spring Initializr** na https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="e7f61-196">For help with getting started with your own Spring Boot applications, see hello **Spring Initializr** at https://start.spring.io/.</span></span>

<span data-ttu-id="e7f61-197">Aby uzyskać więcej informacji na temat rozpoczynania pracy z tworzenia prostej aplikacji Spring rozruchu Zobacz hello Spring Initializr na https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="e7f61-197">For more information about getting started with creating a simple Spring Boot application, see hello Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="e7f61-198">Aby uzyskać dodatkowe przykłady sposobu toouse Docker niestandardowe obrazy z platformy Azure, zobacz [dla aplikacji sieci Web platformy Azure w systemie Linux przy użyciu niestandardowego obrazu Docker].</span><span class="sxs-lookup"><span data-stu-id="e7f61-198">For additional examples for how toouse custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

[Azure interfejsu wiersza polecenia (CLI)]: /cli/azure/overview
[Usługa kontenera platformy Azure (ACS)]: https://azure.microsoft.com/services/container-service/
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Witryna Azure Portal]: https://portal.azure.com/
[Utwórz prywatne rejestru kontenera Docker przy użyciu hello portalu Azure]: /azure/container-registry/container-registry-get-started-portal
[Przy użyciu niestandardowego obrazu Docker dla aplikacji sieci Web platformy Azure w systemie Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[bezpłatne konto platformy Azure]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Narzędzia języka Java dla programu Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[Korzyści dla subskrybentów MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring rozruchu]: http://projects.spring.io/spring-boot/
[Spring rozruchowego na wprowadzenie Docker]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

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
