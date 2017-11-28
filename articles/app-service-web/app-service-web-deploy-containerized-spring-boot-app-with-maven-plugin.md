---
title: Witaj toouse aaaHow Maven wtyczki dla aplikacji sieci Web Azure toodeploy konteneryzowanych tooAzure aplikacji Spring rozruchu
description: "Dowiedz się, jak toouse hello wtyczki Maven dla aplikacji sieci Web Azure toodeploy tooAzure aplikacji Spring rozruchu."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 08/07/2017
ms.author: robmcm;kevinzha
ms.openlocfilehash: e7e760d4ef5bd4c92a4126a50a2b12e5c8f2b4a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-containerized-spring-boot-app-tooazure"></a><span data-ttu-id="4b1d1-103">Jak toouse hello wtyczki Maven dla aplikacji sieci Web Azure toodeploy konteneryzowanych tooAzure aplikacji Spring rozruchu</span><span class="sxs-lookup"><span data-stu-id="4b1d1-103">How toouse hello Maven Plugin for Azure Web Apps toodeploy a containerized Spring Boot app tooAzure</span></span>

<span data-ttu-id="4b1d1-104">Witaj [Maven wtyczki dla aplikacji sieci Web Azure](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) dla [Apache Maven](http://maven.apache.org/) zapewnia bezproblemową integrację usługi Azure App Service w projekty Maven oraz usprawnia proces powitania dla aplikacji sieci web do deweloperzy toodeploy tooAzure usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4b1d1-104">hello [Maven Plugin for Azure Web Apps](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) for [Apache Maven](http://maven.apache.org/) provides seamless integration of Azure App Service  into Maven projects, and streamlines hello process for developers toodeploy web apps tooAzure App Service .</span></span>

<span data-ttu-id="4b1d1-105">W tym artykule przedstawiono przy użyciu hello Maven wtyczki dla aplikacji sieci Web Azure toodeploy przykładowej aplikacji Spring rozruchu w tooAzure kontenera Docker usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4b1d1-105">This article demonstrates using hello Maven Plugin for Azure Web Apps toodeploy a sample Spring Boot application in a Docker container tooAzure App Services.</span></span>

> [!NOTE]
>
> <span data-ttu-id="4b1d1-106">Witaj Maven wtyczki dla aplikacji sieci Web platformy Azure jest obecnie dostępna jako podgląd.</span><span class="sxs-lookup"><span data-stu-id="4b1d1-106">hello Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="4b1d1-107">Obecnie jest obsługiwana tylko publikacji FTP, chociaż hello przyszłości planowane dodatkowe funkcje.</span><span class="sxs-lookup"><span data-stu-id="4b1d1-107">For now, only FTP publishing is supported, although additional features are planned for hello future.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="4b1d1-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4b1d1-108">Prerequisites</span></span>

<span data-ttu-id="4b1d1-109">Kolejność toocomplete hello kroki w tym samouczku potrzebne hello toohave następujące wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="4b1d1-109">In order toocomplete hello steps in this tutorial, you need toohave hello following prerequisites:</span></span>

* <span data-ttu-id="4b1d1-110">Subskrypcja platformy Azure; Jeśli nie masz jeszcze subskrypcji platformy Azure, możesz przeprowadzić aktywację Twojej [korzyści dla subskrybentów MSDN] lub zarejestrować się w celu [bezpłatne konto platformy Azure].</span><span class="sxs-lookup"><span data-stu-id="4b1d1-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="4b1d1-111">Witaj [Azure interfejsu wiersza polecenia (CLI)].</span><span class="sxs-lookup"><span data-stu-id="4b1d1-111">hello [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="4b1d1-112">Aktualne [Java Development Kit (JDK)], wersja 1.7 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="4b1d1-112">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="4b1d1-113">Apache na [Maven] (w wersji 3) Narzędzie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="4b1d1-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="4b1d1-114">A [Git] klienta.</span><span class="sxs-lookup"><span data-stu-id="4b1d1-114">A [Git] client.</span></span>
* <span data-ttu-id="4b1d1-115">A [Docker] klienta.</span><span class="sxs-lookup"><span data-stu-id="4b1d1-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="4b1d1-116">Ze względu na wymagania dotyczące wirtualizacji toohello tego samouczka nie można wykonać hello opisanych w tym artykule na maszynie wirtualnej; należy użyć komputera fizycznego z włączonymi funkcjami wirtualizacji.</span><span class="sxs-lookup"><span data-stu-id="4b1d1-116">Due toohello virtualization requirements of this tutorial, you cannot follow hello steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="clone-hello-sample-spring-boot-on-docker-web-app"></a><span data-ttu-id="4b1d1-117">Klonowanie hello przykładu rozruchu Spring Docker aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="4b1d1-117">Clone hello sample Spring Boot on Docker web app</span></span>

<span data-ttu-id="4b1d1-118">W tej sekcji sklonować konteneryzowanych aplikacji rozruchu Spring i przetestować go lokalnie.</span><span class="sxs-lookup"><span data-stu-id="4b1d1-118">In this section, you clone a containerized Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="4b1d1-119">Otwórz wiersz polecenia lub okno terminalu i utworzyć toohold lokalnego katalogu aplikacji Spring rozruchu i zmień katalog toothat; na przykład:</span><span class="sxs-lookup"><span data-stu-id="4b1d1-119">Open a command prompt or terminal window and create a local directory toohold your Spring Boot application, and change toothat directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="4b1d1-120">--lub--</span><span class="sxs-lookup"><span data-stu-id="4b1d1-120">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="4b1d1-121">Witaj w klonowania [rozruchu Spring na wprowadzenie Docker] przykładowy projekt do katalogu hello utworzony; na przykład:</span><span class="sxs-lookup"><span data-stu-id="4b1d1-121">Clone hello [Spring Boot on Docker Getting Started] sample project into hello directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/microsoft/gs-spring-boot-docker
   ```

1. <span data-ttu-id="4b1d1-122">Zmień katalog projektu toohello ukończone; na przykład:</span><span class="sxs-lookup"><span data-stu-id="4b1d1-122">Change directory toohello completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="4b1d1-123">Kompiluj plik JAR hello za pomocą programu Maven; na przykład:</span><span class="sxs-lookup"><span data-stu-id="4b1d1-123">Build hello JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="4b1d1-124">Podczas tworzenia aplikacji sieci web hello uruchomić aplikacji sieci web hello za pomocą programu Maven; na przykład:</span><span class="sxs-lookup"><span data-stu-id="4b1d1-124">When hello web app has been created, start hello web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="4b1d1-125">Testowanie aplikacji sieci web hello przechodząc tooit lokalnie za pomocą przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="4b1d1-125">Test hello web app by browsing tooit locally using a web browser.</span></span> <span data-ttu-id="4b1d1-126">Na przykład można użyć hello następujące polecenie, jeśli masz curl dostępne:</span><span class="sxs-lookup"><span data-stu-id="4b1d1-126">For example, you could use hello following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="4b1d1-127">Powinien zostać wyświetlony komunikat wyświetlany po hello: **Hello Docker World**</span><span class="sxs-lookup"><span data-stu-id="4b1d1-127">You should see hello following message displayed: **Hello Docker World**</span></span>

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="4b1d1-128">Tworzenie nazwy głównej usługi platformy Azure</span><span class="sxs-lookup"><span data-stu-id="4b1d1-128">Create an Azure service principal</span></span>

<span data-ttu-id="4b1d1-129">W tej sekcji utworzysz Azure nazwy głównej usługi, która hello używa wtyczki Maven, wdrażając tooAzure Twojego kontenera.</span><span class="sxs-lookup"><span data-stu-id="4b1d1-129">In this section, you create an Azure service principal that hello Maven plugin uses when deploying your container tooAzure.</span></span>

1. <span data-ttu-id="4b1d1-130">Otwórz wiersz polecenia.</span><span class="sxs-lookup"><span data-stu-id="4b1d1-130">Open a command prompt.</span></span>

1. <span data-ttu-id="4b1d1-131">Zaloguj się do konta platformy Azure przy użyciu hello wiersza polecenia platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="4b1d1-131">Sign into your Azure account by using hello Azure CLI:</span></span>
   ```shell
   az login
   ```
   <span data-ttu-id="4b1d1-132">Wykonaj hello instrukcje toocomplete hello procesu logowania.</span><span class="sxs-lookup"><span data-stu-id="4b1d1-132">Follow hello instructions toocomplete hello sign-in process.</span></span>

1. <span data-ttu-id="4b1d1-133">Tworzenie nazwy głównej usługi platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="4b1d1-133">Create an Azure service principal:</span></span>
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="4b1d1-134">Gdzie `uuuuuuuu` jest nazwą użytkownika hello i `pppppppp` jest hello hasło dla nazwy głównej usługi hello.</span><span class="sxs-lookup"><span data-stu-id="4b1d1-134">Where `uuuuuuuu` is hello user name and `pppppppp` is hello password for hello service principal.</span></span>

1. <span data-ttu-id="4b1d1-135">Azure odpowiada JSON podobny hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="4b1d1-135">Azure responds with JSON that resembles hello following example:</span></span>
   ```json
   {
      "appId": "aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa",
      "displayName": "uuuuuuuu",
      "name": "http://uuuuuuuu",
      "password": "pppppppp",
      "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
   }
   ```

   > [!NOTE]
   >
   > <span data-ttu-id="4b1d1-136">Po skonfigurowaniu hello Maven wtyczki toodeploy Twojego tooAzure kontenera Użyj wartości hello z odpowiedź w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="4b1d1-136">You will use hello values from this JSON response when you configure hello Maven plugin toodeploy your container tooAzure.</span></span> <span data-ttu-id="4b1d1-137">Hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, i `tttttttt` są symbole zastępcze, które są używane w tej toomake przykład go łatwiejsze toomap tych wartości tootheir odpowiednich elementów podczas konfigurowania programu Maven `settings.xml` w hello obok pliku sekcja.</span><span class="sxs-lookup"><span data-stu-id="4b1d1-137">hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example toomake it easier toomap these values tootheir respective elements when you configure your Maven `settings.xml` file in hello next section.</span></span>
   >
   >

## <a name="configure-maven-toouse-your-azure-service-principal"></a><span data-ttu-id="4b1d1-138">Skonfiguruj Maven toouse Twojej nazwy głównej usługi Azure</span><span class="sxs-lookup"><span data-stu-id="4b1d1-138">Configure Maven toouse your Azure service principal</span></span>

<span data-ttu-id="4b1d1-139">W tej sekcji można użyć wartości hello z Twojej uwierzytelniania hello tooconfigure główną usługi Azure Maven będzie używane podczas wdrażania sieci tooAzure kontenera.</span><span class="sxs-lookup"><span data-stu-id="4b1d1-139">In this section, you use hello values from your Azure service principal tooconfigure hello authentication that Maven will use when deploying your container tooAzure.</span></span>

1. <span data-ttu-id="4b1d1-140">Otwieranie programu Maven `settings.xml` plik w edytorze tekstów; ten plik może być w ścieżce, takie jak hello następujące przykłady:</span><span class="sxs-lookup"><span data-stu-id="4b1d1-140">Open your Maven `settings.xml` file in a text editor; this file might be in a path like hello following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="4b1d1-141">Dodaj ustawienia głównych usług Azure hello w poprzedniej sekcji tego samouczka toohello `<servers>` kolekcji w hello *settings.xml* pliku; na przykład:</span><span class="sxs-lookup"><span data-stu-id="4b1d1-141">Add your Azure service principal settings from hello previous section of this tutorial toohello `<servers>` collection in hello *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
        <id>azure-auth</id>
         <configuration>
            <client>aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa</client>
            <tenant>tttttttt-tttt-tttt-tttt-tttttttttttt</tenant>
            <key>pppppppp</key>
            <environment>AZURE</environment>
         </configuration>
      </server>
   </servers>
   ```
   <span data-ttu-id="4b1d1-142">Gdzie:</span><span class="sxs-lookup"><span data-stu-id="4b1d1-142">Where:</span></span>
   <span data-ttu-id="4b1d1-143">Element</span><span class="sxs-lookup"><span data-stu-id="4b1d1-143">Element</span></span> | <span data-ttu-id="4b1d1-144">Opis</span><span class="sxs-lookup"><span data-stu-id="4b1d1-144">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="4b1d1-145">Określa unikatową nazwę używający Maven toolook zapasową ustawień zabezpieczeń podczas wdrażania tooAzure aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="4b1d1-145">Specifies a unique name which Maven uses toolook up your security settings when you deploy your web app tooAzure.</span></span>
   `<client>` | <span data-ttu-id="4b1d1-146">Zawiera hello `appId` wartość z Twojej nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="4b1d1-146">Contains hello `appId` value from your service principal.</span></span>
   `<tenant>` | <span data-ttu-id="4b1d1-147">Zawiera hello `tenant` wartość z Twojej nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="4b1d1-147">Contains hello `tenant` value from your service principal.</span></span>
   `<key>` | <span data-ttu-id="4b1d1-148">Zawiera hello `password` wartość z Twojej nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="4b1d1-148">Contains hello `password` value from your service principal.</span></span>
   `<environment>` | <span data-ttu-id="4b1d1-149">Definiuje hello docelowej chmury Azure środowisko, które jest `AZURE` w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="4b1d1-149">Defines hello target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="4b1d1-150">(Pełna lista środowisk jest dostępna w hello [Maven wtyczki dla aplikacji sieci Web Azure] dokumentacji)</span><span class="sxs-lookup"><span data-stu-id="4b1d1-150">(A full list of environments is available in hello [Maven Plugin for Azure Web Apps] documentation)</span></span>

1. <span data-ttu-id="4b1d1-151">Zapisz i zamknij hello *settings.xml* pliku.</span><span class="sxs-lookup"><span data-stu-id="4b1d1-151">Save and close hello *settings.xml* file.</span></span>

## <a name="optional-deploy-your-local-docker-file-toodocker-hub"></a><span data-ttu-id="4b1d1-152">OPCJONALNIE: Wdrożenia z lokalnego pliku Docker tooDocker Centrum</span><span class="sxs-lookup"><span data-stu-id="4b1d1-152">OPTIONAL: Deploy your local Docker file tooDocker Hub</span></span>

<span data-ttu-id="4b1d1-153">Jeśli masz konto Docker można kompilacji programu Docker kontener obrazu lokalnie i wypchnąć go tooDocker koncentratora.</span><span class="sxs-lookup"><span data-stu-id="4b1d1-153">If you have a Docker account, you can build your Docker container image locally and push it tooDocker Hub.</span></span> <span data-ttu-id="4b1d1-154">toodo tak, użycie hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="4b1d1-154">toodo so, use hello following steps.</span></span>

1. <span data-ttu-id="4b1d1-155">Otwórz hello `pom.xml` pliku rozruchowego Spring aplikacji w edytorze tekstów.</span><span class="sxs-lookup"><span data-stu-id="4b1d1-155">Open hello `pom.xml` file for your Spring Boot application in a text editor.</span></span>

1. <span data-ttu-id="4b1d1-156">Zlokalizuj hello `<imageName>` elementem podrzędnym hello `<containerSettings>` elementu.</span><span class="sxs-lookup"><span data-stu-id="4b1d1-156">Locate hello `<imageName>` child element of hello `<containerSettings>` element.</span></span>

1. <span data-ttu-id="4b1d1-157">Aktualizacja hello `${docker.image.prefix}` wartości z Docker nazwa konta:</span><span class="sxs-lookup"><span data-stu-id="4b1d1-157">Update hello `${docker.image.prefix}` value with your Docker account name:</span></span>
   ```xml
   <containerSettings>
      <imageName>mydockeraccountname/${project.artifactId}</imageName>
   </containerSettings>
   ```

1. <span data-ttu-id="4b1d1-158">Wybierz jedną z hello następujące metody wdrażania:</span><span class="sxs-lookup"><span data-stu-id="4b1d1-158">Choose one of hello following deployment methods:</span></span>

   * <span data-ttu-id="4b1d1-159">Tworzenie obrazu kontenera lokalnie z Maven, a następnie użyj Docker toopush tooDocker Twojego kontenera Centrum:</span><span class="sxs-lookup"><span data-stu-id="4b1d1-159">Build your container image locally with Maven, and then use Docker toopush your container tooDocker Hub:</span></span>
      ```shell
      mvn clean package docker:build
      docker push
      ```
   
   * <span data-ttu-id="4b1d1-160">Jeśli masz hello [wtyczki Docker przypadku Maven] zainstalowana, można automatycznie utworzyć i hello z kontenera obrazu tooDocker koncentratora za pomocą `-DpushImage` parametru:</span><span class="sxs-lookup"><span data-stu-id="4b1d1-160">If you have hello [Docker plugin for Maven] installed, you can automatically build and your container image tooDocker Hub by using hello `-DpushImage` parameter:</span></span>
      ```shell
      mvn clean package docker:build -DpushImage
      ```

## <a name="optional-customize-your-pomxml-before-deploying-your-container-tooazure"></a><span data-ttu-id="4b1d1-161">OPCJONALNIE: Dostosowywanie programu pom.xml przed wdrożeniem programu tooAzure kontenera</span><span class="sxs-lookup"><span data-stu-id="4b1d1-161">OPTIONAL: Customize your pom.xml before deploying your container tooAzure</span></span>

<span data-ttu-id="4b1d1-162">Otwórz hello `pom.xml` pliku aplikacji Spring rozruchu w edytorze tekstu, a następnie zlokalizuj hello `<plugin>` elementu `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="4b1d1-162">Open hello `pom.xml` file for your Spring Boot application in a text editor, and then locate hello `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="4b1d1-163">Ten element powinien wyglądać hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="4b1d1-163">This element should resemble hello following example:</span></span>

   ```xml
   <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <version>0.1.3</version>
      <configuration>
         <authentication>
            <serverId>azure-auth</serverId>
         </authentication>
         <resourceGroup>maven-plugin</resourceGroup>
         <appName>maven-linux-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <containerSettings>
            <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         </containerSettings>
         <appSettings>
            <property>
               <name>PORT</name>
               <value>8080</value>
            </property>
         </appSettings>
      </configuration>
   </plugin>
   ```

<span data-ttu-id="4b1d1-164">Istnieje kilka wartości, które można modyfikować dla wtyczki Maven hello i szczegółowy opis każdego z tych elementów jest dostępna w hello [Maven wtyczki dla aplikacji sieci Web Azure] dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="4b1d1-164">There are several values that you can modify for hello Maven plugin, and a detailed description for each of these elements is available in hello [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="4b1d1-165">Który trwa wspomniano, istnieje kilka wartości, które warto wyróżnianie w tym artykule:</span><span class="sxs-lookup"><span data-stu-id="4b1d1-165">That being said, there are several values that are worth highlighting in this article:</span></span>

<span data-ttu-id="4b1d1-166">Element</span><span class="sxs-lookup"><span data-stu-id="4b1d1-166">Element</span></span> | <span data-ttu-id="4b1d1-167">Opis</span><span class="sxs-lookup"><span data-stu-id="4b1d1-167">Description</span></span>
---|---|---
`<version>` | <span data-ttu-id="4b1d1-168">Określa wersję hello hello [Maven wtyczki dla aplikacji sieci Web Azure].</span><span class="sxs-lookup"><span data-stu-id="4b1d1-168">Specifies hello version of hello [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="4b1d1-169">Należy sprawdzić wersji hello na liście hello [Maven centralnym repozytorium](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure, którego używasz hello najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="4b1d1-169">You should check hello version listed in hello [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure that you are using hello latest version.</span></span>
`<authentication>` | <span data-ttu-id="4b1d1-170">Określa hello informacje dotyczące uwierzytelniania dla platformy Azure, który w tym przykładzie zawiera `<serverId>` element, który zawiera `azure-auth`; Maven używa tej wartości toolook wartości podmiotu zabezpieczeń usługi Azure hello programu Maven *settings.xml* pliku, który został zdefiniowany w wcześniejszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="4b1d1-170">Specifies hello authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value toolook up hello Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span>
`<resourceGroup>` | <span data-ttu-id="4b1d1-171">Określa, docelowa grupa zasobów hello, który jest `maven-plugin` w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="4b1d1-171">Specifies hello target resource group, which is `maven-plugin` in this example.</span></span> <span data-ttu-id="4b1d1-172">Grupa zasobów Hello zostanie utworzony podczas wdrażania, jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="4b1d1-172">hello resource group will be created during deployment if it does not already exist.</span></span>
`<appName>` | <span data-ttu-id="4b1d1-173">Określa nazwę docelowej hello aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="4b1d1-173">Specifies hello target name for your web app.</span></span> <span data-ttu-id="4b1d1-174">W tym przykładzie nazwa docelowego hello jest `maven-linux-app-${maven.build.timestamp}`, gdzie hello `${maven.build.timestamp}` jest do niej dołączany sufiks w tej konflikt tooavoid przykład.</span><span class="sxs-lookup"><span data-stu-id="4b1d1-174">In this example, hello target name is `maven-linux-app-${maven.build.timestamp}`, where hello `${maven.build.timestamp}` suffix is appended in this example tooavoid conflict.</span></span> <span data-ttu-id="4b1d1-175">(sygnatura czasowa hello jest opcjonalne; można określić dowolny unikatowy ciąg dla nazwy aplikacji hello).</span><span class="sxs-lookup"><span data-stu-id="4b1d1-175">(hello timestamp is optional; you can specify any unique string for hello app name.)</span></span>
`<region>` | <span data-ttu-id="4b1d1-176">Określa region docelowy hello, czyli w tym przykładzie `westus`.</span><span class="sxs-lookup"><span data-stu-id="4b1d1-176">Specifies hello target region, which in this example is `westus`.</span></span> <span data-ttu-id="4b1d1-177">(Pełna lista jest w hello [Maven wtyczki dla aplikacji sieci Web Azure] dokumentacji.)</span><span class="sxs-lookup"><span data-stu-id="4b1d1-177">(A full list is in hello [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<appSettings>` | <span data-ttu-id="4b1d1-178">Określa unikatowy ustawienia Maven toouse, wdrażając tooAzure aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="4b1d1-178">Specifies any unique settings for Maven toouse when deploying your web app tooAzure.</span></span> <span data-ttu-id="4b1d1-179">W tym przykładzie `<property>` element zawiera pary nazwa/wartość elementów podrzędnych, określających hello portu dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4b1d1-179">In this example, a `<property>` element contains a name/value pair of child elements that specify hello port for your app.</span></span>

> [!NOTE]
>
> <span data-ttu-id="4b1d1-180">numer portu Hello ustawienia toochange hello w tym przykładzie jest konieczne tylko w przypadku, gdy zmieniasz hello portów z domyślnej hello.</span><span class="sxs-lookup"><span data-stu-id="4b1d1-180">hello settings toochange hello port number in this example are only necessary when you are changing hello port from hello default.</span></span>
>

## <a name="build-and-deploy-your-container-tooazure"></a><span data-ttu-id="4b1d1-181">Tworzenie i wdrażanie tooAzure Twojego kontenera</span><span class="sxs-lookup"><span data-stu-id="4b1d1-181">Build and deploy your container tooAzure</span></span>

<span data-ttu-id="4b1d1-182">Po skonfigurowaniu wszystkich ustawień hello w hello powyższej sekcji tego artykułu, są gotowe toodeploy Twojego tooAzure kontenera.</span><span class="sxs-lookup"><span data-stu-id="4b1d1-182">Once you have configured all of hello settings in hello preceding sections of this article, you are ready toodeploy your container tooAzure.</span></span> <span data-ttu-id="4b1d1-183">toodo tak, użycie hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="4b1d1-183">toodo so, use hello following steps:</span></span>

1. <span data-ttu-id="4b1d1-184">Z wiersza polecenia hello lub okno terminalu, które były wcześniej używane odbudować plik JAR hello za pomocą programu Maven Jeśli wprowadzono żadnych zmian toohello *pom.xml* pliku; na przykład:</span><span class="sxs-lookup"><span data-stu-id="4b1d1-184">From hello command prompt or terminal window that you were using earlier, rebuild hello JAR file using Maven if you made any changes toohello *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="4b1d1-185">Wdrażanie tooAzure aplikacji sieci web przy użyciu narzędzia Maven; na przykład:</span><span class="sxs-lookup"><span data-stu-id="4b1d1-185">Deploy your web app tooAzure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="4b1d1-186">Maven wdroży tooAzure aplikacji sieci web; Jeśli aplikacja sieci web hello jeszcze nie istnieje, zostanie utworzona.</span><span class="sxs-lookup"><span data-stu-id="4b1d1-186">Maven will deploy your web app tooAzure; if hello web app does not already exist, it will be created.</span></span>

> [!NOTE]
>
> <span data-ttu-id="4b1d1-187">Jeśli region hello, określany w hello `<region>` elementu z *pom.xml* plik nie ma wystarczającej liczby serwerów, które są dostępne po uruchomieniu wdrożenia, można napotkać błąd toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="4b1d1-187">If hello region which you specify in hello `<region>` element of your *pom.xml* file does not have enough servers available when you start your deployment, you might see an error similar toohello following example:</span></span>
>
> ```
> [INFO] Start deploying tooWeb App maven-linux-app-20170804...
> [INFO] ------------------------------------------------------------------------
> [INFO] BUILD FAILURE
> [INFO] ------------------------------------------------------------------------
> [INFO] Total time: 31.059 s
> [INFO] Finished at: 2017-08-04T12:15:47-07:00
> [INFO] Final Memory: 51M/279M
> [INFO] ------------------------------------------------------------------------
> [ERROR] Failed tooexecute goal com.microsoft.azure:azure-webapp-maven-plugin:0.1.3:deploy (default-cli) on project gs-spring-boot-docker: null: MojoExecutionException: CloudException: OnError while emitting onNext value: retrofit2.Response.class
> ```
>
> <span data-ttu-id="4b1d1-188">W takim przypadku można określić innego regionu i uruchom ponownie hello toodeploy polecenie narzędzia Maven aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4b1d1-188">If this happens, you can specify another region and re-run hello Maven command toodeploy your application.</span></span>
>
>

<span data-ttu-id="4b1d1-189">Po wdrożeniu sieci web będą mogli toomanage go za pomocą hello [portalu Azure].</span><span class="sxs-lookup"><span data-stu-id="4b1d1-189">When your web has been deployed, you will be able toomanage it by using hello [Azure portal].</span></span>

* <span data-ttu-id="4b1d1-190">Aplikacja sieci web zostaną wyświetlone w **usługi aplikacji**:</span><span class="sxs-lookup"><span data-stu-id="4b1d1-190">Your web app will be listed in **App Services**:</span></span>

   ![Aplikacja sieci Web wyświetlane w portalu Azure usługi aplikacji][AP01]

* <span data-ttu-id="4b1d1-192">I hello adres URL dla aplikacji sieci web zostaną wyświetlone w hello **omówienie** dla aplikacji sieci web:</span><span class="sxs-lookup"><span data-stu-id="4b1d1-192">And hello URL for your web app will be listed in hello **Overview** for your web app:</span></span>

   ![Określanie hello adres URL aplikacji sieci web][AP02]

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

## <a name="next-steps"></a><span data-ttu-id="4b1d1-194">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4b1d1-194">Next steps</span></span>

<span data-ttu-id="4b1d1-195">Aby uzyskać więcej informacji na temat hello różne technologie omówione w tym artykule, zobacz hello następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="4b1d1-195">For more information about hello various technologies discussed in this article, see hello following articles:</span></span>

* <span data-ttu-id="4b1d1-196">[Maven wtyczki dla aplikacji sieci Web Azure]</span><span class="sxs-lookup"><span data-stu-id="4b1d1-196">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="4b1d1-197">Zaloguj się za tooAzure z hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="4b1d1-197">Log in tooAzure from hello Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="4b1d1-198">Jak toouse hello Maven wtyczki dla aplikacji sieci Web Azure toodeploy rozruchu Spring tooAzure aplikacji usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="4b1d1-198">How toouse hello Maven Plugin for Azure Web Apps toodeploy a Spring Boot app tooAzure App Service </span></span>](app-service-web-deploy-spring-boot-app-with-maven-plugin.md)

* [<span data-ttu-id="4b1d1-199">Tworzenie nazwy głównej usługi platformy Azure z 2.0 interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="4b1d1-199">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="4b1d1-200">Informacje o ustawieniach maven</span><span class="sxs-lookup"><span data-stu-id="4b1d1-200">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

* <span data-ttu-id="4b1d1-201">[wtyczki Docker przypadku Maven]</span><span class="sxs-lookup"><span data-stu-id="4b1d1-201">[Docker plugin for Maven]</span></span>

<!-- URL List -->

[Azure interfejsu wiersza polecenia (CLI)]: /cli/azure/overview
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[portalu Azure]: https://portal.azure.com/
[Docker]: https://www.docker.com/
[wtyczki Docker przypadku Maven]: https://github.com/spotify/docker-maven-plugin
[bezpłatne konto platformy Azure]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[korzyści dla subskrybentów MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[rozruchu Spring na wprowadzenie Docker]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/
[Maven wtyczki dla aplikacji sieci Web Azure]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin

<!-- IMG List -->

[AP01]: ./media/app-service-web-deploy-containerized-spring-boot-app-with-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-containerized-spring-boot-app-with-maven-plugin/AP02.png
