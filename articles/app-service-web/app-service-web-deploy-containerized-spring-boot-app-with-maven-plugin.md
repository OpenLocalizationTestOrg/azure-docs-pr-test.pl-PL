---
title: "Jak używać wtyczki Maven dla aplikacji sieci Web Azure wdrażania konteneryzowanych aplikacji Spring rozruchu w systemie Azure"
description: "Informacje o sposobie wdrożenia aplikacji rozruchu Spring na platformie Azure za pomocą wtyczki Maven dla aplikacji sieci Web platformy Azure."
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
ms.openlocfilehash: 883040590291cee94daa227fbc6715ad4be0b393
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-the-maven-plugin-for-azure-web-apps-to-deploy-a-containerized-spring-boot-app-to-azure"></a><span data-ttu-id="37825-103">Jak używać wtyczki Maven dla aplikacji sieci Web Azure wdrażania konteneryzowanych aplikacji Spring rozruchu w systemie Azure</span><span class="sxs-lookup"><span data-stu-id="37825-103">How to use the Maven Plugin for Azure Web Apps to deploy a containerized Spring Boot app to Azure</span></span>

<span data-ttu-id="37825-104">[Maven wtyczki dla aplikacji sieci Web Azure](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) dla [Apache Maven](http://maven.apache.org/) zapewnia bezproblemową integrację usługi Azure App Service w projekty Maven oraz usprawnia proces deweloperom wdrażanie aplikacji sieci web w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="37825-104">The [Maven Plugin for Azure Web Apps](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) for [Apache Maven](http://maven.apache.org/) provides seamless integration of Azure App Service  into Maven projects, and streamlines the process for developers to deploy web apps to Azure App Service .</span></span>

<span data-ttu-id="37825-105">W tym artykule przedstawiono wdrażanie przykładowej aplikacji Spring rozruchu w kontenerze Docker do usługi aplikacji Azure za pomocą wtyczki Maven dla aplikacji sieci Web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="37825-105">This article demonstrates using the Maven Plugin for Azure Web Apps to deploy a sample Spring Boot application in a Docker container to Azure App Services.</span></span>

> [!NOTE]
>
> <span data-ttu-id="37825-106">Dodatek plug-in Maven dla aplikacji sieci Web Azure jest obecnie dostępna jako podgląd.</span><span class="sxs-lookup"><span data-stu-id="37825-106">The Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="37825-107">Obecnie jest obsługiwana tylko publikacji FTP, chociaż dodatkowe funkcje są planowane w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="37825-107">For now, only FTP publishing is supported, although additional features are planned for the future.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="37825-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="37825-108">Prerequisites</span></span>

<span data-ttu-id="37825-109">Aby wykonać kroki opisane w tym samouczku, musisz mieć następujące wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="37825-109">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="37825-110">Subskrypcja platformy Azure; Jeśli nie masz jeszcze subskrypcji platformy Azure, możesz przeprowadzić aktywację Twojej [korzyści dla subskrybentów MSDN] lub zarejestrować się w celu [bezpłatne konto platformy Azure].</span><span class="sxs-lookup"><span data-stu-id="37825-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="37825-111">[Azure interfejsu wiersza polecenia (CLI)].</span><span class="sxs-lookup"><span data-stu-id="37825-111">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="37825-112">Aktualne [Java Development Kit (JDK)], wersja 1.7 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="37825-112">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="37825-113">Apache na [Maven] (w wersji 3) Narzędzie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="37825-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="37825-114">A [Git] klienta.</span><span class="sxs-lookup"><span data-stu-id="37825-114">A [Git] client.</span></span>
* <span data-ttu-id="37825-115">A [Docker] klienta.</span><span class="sxs-lookup"><span data-stu-id="37825-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="37825-116">Ze względu na wymagania dotyczące wirtualizacji w tym samouczku nie można wykonać kroki opisane w tym artykule na maszynie wirtualnej; należy użyć komputera fizycznego z włączonymi funkcjami wirtualizacji.</span><span class="sxs-lookup"><span data-stu-id="37825-116">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="clone-the-sample-spring-boot-on-docker-web-app"></a><span data-ttu-id="37825-117">Klonowanie próbki Spring rozruchu w aplikacji sieci web Docker</span><span class="sxs-lookup"><span data-stu-id="37825-117">Clone the sample Spring Boot on Docker web app</span></span>

<span data-ttu-id="37825-118">W tej sekcji sklonować konteneryzowanych aplikacji rozruchu Spring i przetestować go lokalnie.</span><span class="sxs-lookup"><span data-stu-id="37825-118">In this section, you clone a containerized Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="37825-119">Otwórz wiersz polecenia lub okno terminalu i utworzyć katalogu lokalnego do przechowywania aplikacji Spring rozruchu, przejdź do tego katalogu; na przykład:</span><span class="sxs-lookup"><span data-stu-id="37825-119">Open a command prompt or terminal window and create a local directory to hold your Spring Boot application, and change to that directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="37825-120">--lub--</span><span class="sxs-lookup"><span data-stu-id="37825-120">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="37825-121">Klonowanie [rozruchu Spring na wprowadzenie Docker] przykładowy projekt do katalogu utworzonego; na przykład:</span><span class="sxs-lookup"><span data-stu-id="37825-121">Clone the [Spring Boot on Docker Getting Started] sample project into the directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/microsoft/gs-spring-boot-docker
   ```

1. <span data-ttu-id="37825-122">Zmień katalog na ukończone projektu; na przykład:</span><span class="sxs-lookup"><span data-stu-id="37825-122">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="37825-123">Kompiluj plik JAR za pomocą programu Maven; na przykład:</span><span class="sxs-lookup"><span data-stu-id="37825-123">Build the JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="37825-124">Po utworzeniu aplikacji sieci web, należy uruchomić aplikację sieci web za pomocą programu Maven; na przykład:</span><span class="sxs-lookup"><span data-stu-id="37825-124">When the web app has been created, start the web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="37825-125">Testowanie aplikacji sieci web przy użyciu przeglądania lokalnie za pomocą przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="37825-125">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="37825-126">Na przykład można użyć następującego polecenia Jeśli masz curl dostępne:</span><span class="sxs-lookup"><span data-stu-id="37825-126">For example, you could use the following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="37825-127">Powinien zostać wyświetlony następujący komunikat wyświetlany: **Hello, World Docker**</span><span class="sxs-lookup"><span data-stu-id="37825-127">You should see the following message displayed: **Hello Docker World**</span></span>

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="37825-128">Tworzenie nazwy głównej usługi platformy Azure</span><span class="sxs-lookup"><span data-stu-id="37825-128">Create an Azure service principal</span></span>

<span data-ttu-id="37825-129">W tej sekcji utworzysz Azure nazwy głównej usługi używającej wtyczki Maven podczas wdrażania z kontenera na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="37825-129">In this section, you create an Azure service principal that the Maven plugin uses when deploying your container to Azure.</span></span>

1. <span data-ttu-id="37825-130">Otwórz wiersz polecenia.</span><span class="sxs-lookup"><span data-stu-id="37825-130">Open a command prompt.</span></span>

1. <span data-ttu-id="37825-131">Zaloguj się do konta platformy Azure przy użyciu wiersza polecenia platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="37825-131">Sign into your Azure account by using the Azure CLI:</span></span>
   ```shell
   az login
   ```
   <span data-ttu-id="37825-132">Postępuj zgodnie z instrukcjami, aby ukończyć proces logowania.</span><span class="sxs-lookup"><span data-stu-id="37825-132">Follow the instructions to complete the sign-in process.</span></span>

1. <span data-ttu-id="37825-133">Tworzenie nazwy głównej usługi platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="37825-133">Create an Azure service principal:</span></span>
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="37825-134">Gdzie `uuuuuuuu` jest nazwą użytkownika i `pppppppp` jest hasło dla nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="37825-134">Where `uuuuuuuu` is the user name and `pppppppp` is the password for the service principal.</span></span>

1. <span data-ttu-id="37825-135">Azure odpowiada JSON, który podobnego do następującego:</span><span class="sxs-lookup"><span data-stu-id="37825-135">Azure responds with JSON that resembles the following example:</span></span>
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
   > <span data-ttu-id="37825-136">Po skonfigurowaniu dodatek plug-in Maven, aby wdrożyć z kontenera na platformie Azure, będzie używać wartości z tej odpowiedzi JSON.</span><span class="sxs-lookup"><span data-stu-id="37825-136">You will use the values from this JSON response when you configure the Maven plugin to deploy your container to Azure.</span></span> <span data-ttu-id="37825-137">`aaaaaaaa`, `uuuuuuuu`, `pppppppp`, I `tttttttt` są symbole zastępcze, które są używane w tym przykładzie ułatwiające Mapuj tych wartości do ich odpowiednich elementów, podczas konfigurowania programu Maven `settings.xml` pliku w następnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="37825-137">The `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example to make it easier to map these values to their respective elements when you configure your Maven `settings.xml` file in the next section.</span></span>
   >
   >

## <a name="configure-maven-to-use-your-azure-service-principal"></a><span data-ttu-id="37825-138">Skonfiguruj Maven do użycia z nazwy głównej usługi Azure</span><span class="sxs-lookup"><span data-stu-id="37825-138">Configure Maven to use your Azure service principal</span></span>

<span data-ttu-id="37825-139">W tej sekcji możesz Użyj wartości od podmiotu zabezpieczeń usługi Azure można skonfigurować uwierzytelniania, które Maven będzie używane podczas wdrażania z kontenera na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="37825-139">In this section, you use the values from your Azure service principal to configure the authentication that Maven will use when deploying your container to Azure.</span></span>

1. <span data-ttu-id="37825-140">Otwieranie programu Maven `settings.xml` plik w edytorze tekstów; ten plik może być w ścieżce, takie jak następujące przykłady:</span><span class="sxs-lookup"><span data-stu-id="37825-140">Open your Maven `settings.xml` file in a text editor; this file might be in a path like the following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="37825-141">Dodaj ustawienia głównych usług Azure opisanych w poprzedniej części tego samouczka do `<servers>` kolekcji w *settings.xml* pliku; na przykład:</span><span class="sxs-lookup"><span data-stu-id="37825-141">Add your Azure service principal settings from the previous section of this tutorial to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

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
   <span data-ttu-id="37825-142">Gdzie:</span><span class="sxs-lookup"><span data-stu-id="37825-142">Where:</span></span>
   <span data-ttu-id="37825-143">Element</span><span class="sxs-lookup"><span data-stu-id="37825-143">Element</span></span> | <span data-ttu-id="37825-144">Opis</span><span class="sxs-lookup"><span data-stu-id="37825-144">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="37825-145">Określa unikatową nazwę Maven używanym w celu wyszukania ustawień zabezpieczeń podczas wdrażania aplikacji sieci web na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="37825-145">Specifies a unique name which Maven uses to look up your security settings when you deploy your web app to Azure.</span></span>
   `<client>` | <span data-ttu-id="37825-146">Zawiera `appId` wartość z Twojej nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="37825-146">Contains the `appId` value from your service principal.</span></span>
   `<tenant>` | <span data-ttu-id="37825-147">Zawiera `tenant` wartość z Twojej nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="37825-147">Contains the `tenant` value from your service principal.</span></span>
   `<key>` | <span data-ttu-id="37825-148">Zawiera `password` wartość z Twojej nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="37825-148">Contains the `password` value from your service principal.</span></span>
   `<environment>` | <span data-ttu-id="37825-149">Definiuje środowisko chmury Azure docelowych, które jest `AZURE` w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="37825-149">Defines the target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="37825-150">(Pełna lista środowisk jest dostępna w [Maven wtyczki dla aplikacji sieci Web Azure] dokumentacji)</span><span class="sxs-lookup"><span data-stu-id="37825-150">(A full list of environments is available in the [Maven Plugin for Azure Web Apps] documentation)</span></span>

1. <span data-ttu-id="37825-151">Zapisz i Zamknij *settings.xml* pliku.</span><span class="sxs-lookup"><span data-stu-id="37825-151">Save and close the *settings.xml* file.</span></span>

## <a name="optional-deploy-your-local-docker-file-to-docker-hub"></a><span data-ttu-id="37825-152">OPCJONALNIE: Lokalny plik Docker wdrożyć do Centrum Docker</span><span class="sxs-lookup"><span data-stu-id="37825-152">OPTIONAL: Deploy your local Docker file to Docker Hub</span></span>

<span data-ttu-id="37825-153">Jeśli masz konto Docker można kompilacji programu Docker kontener obrazu lokalnie i wypchnąć go do Centrum Docker.</span><span class="sxs-lookup"><span data-stu-id="37825-153">If you have a Docker account, you can build your Docker container image locally and push it to Docker Hub.</span></span> <span data-ttu-id="37825-154">Aby to zrobić, wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="37825-154">To do so, use the following steps.</span></span>

1. <span data-ttu-id="37825-155">Otwórz `pom.xml` pliku rozruchowego Spring aplikacji w edytorze tekstów.</span><span class="sxs-lookup"><span data-stu-id="37825-155">Open the `pom.xml` file for your Spring Boot application in a text editor.</span></span>

1. <span data-ttu-id="37825-156">Zlokalizuj `<imageName>` elementem podrzędnym `<containerSettings>` elementu.</span><span class="sxs-lookup"><span data-stu-id="37825-156">Locate the `<imageName>` child element of the `<containerSettings>` element.</span></span>

1. <span data-ttu-id="37825-157">Aktualizacja `${docker.image.prefix}` wartości z Docker nazwa konta:</span><span class="sxs-lookup"><span data-stu-id="37825-157">Update the `${docker.image.prefix}` value with your Docker account name:</span></span>
   ```xml
   <containerSettings>
      <imageName>mydockeraccountname/${project.artifactId}</imageName>
   </containerSettings>
   ```

1. <span data-ttu-id="37825-158">Wybierz jedną z następujących metod wdrażania:</span><span class="sxs-lookup"><span data-stu-id="37825-158">Choose one of the following deployment methods:</span></span>

   * <span data-ttu-id="37825-159">Tworzenie obrazu kontenera lokalnie z Maven, a następnie użyj Docker do dystrybuowania z kontenera do Centrum Docker:</span><span class="sxs-lookup"><span data-stu-id="37825-159">Build your container image locally with Maven, and then use Docker to push your container to Docker Hub:</span></span>
      ```shell
      mvn clean package docker:build
      docker push
      ```
   
   * <span data-ttu-id="37825-160">Jeśli masz [wtyczki Docker przypadku Maven] zainstalowana, można automatycznie utworzyć i z kontenera obrazu do Centrum Docker przy użyciu `-DpushImage` parametru:</span><span class="sxs-lookup"><span data-stu-id="37825-160">If you have the [Docker plugin for Maven] installed, you can automatically build and your container image to Docker Hub by using the `-DpushImage` parameter:</span></span>
      ```shell
      mvn clean package docker:build -DpushImage
      ```

## <a name="optional-customize-your-pomxml-before-deploying-your-container-to-azure"></a><span data-ttu-id="37825-161">OPCJONALNIE: Dostosowywanie Twojej pom.xml przed wdrożeniem z kontenera na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="37825-161">OPTIONAL: Customize your pom.xml before deploying your container to Azure</span></span>

<span data-ttu-id="37825-162">Otwórz `pom.xml` pliku aplikacji Spring rozruchu w edytorze tekstu, a następnie zlokalizuj `<plugin>` elementu `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="37825-162">Open the `pom.xml` file for your Spring Boot application in a text editor, and then locate the `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="37825-163">Ten element powinien wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="37825-163">This element should resemble the following example:</span></span>

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

<span data-ttu-id="37825-164">Istnieje kilka wartości, które można modyfikować dla wtyczki Maven i szczegółowy opis każdego z tych elementów jest dostępna w [Maven wtyczki dla aplikacji sieci Web Azure] dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="37825-164">There are several values that you can modify for the Maven plugin, and a detailed description for each of these elements is available in the [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="37825-165">Który trwa wspomniano, istnieje kilka wartości, które warto wyróżnianie w tym artykule:</span><span class="sxs-lookup"><span data-stu-id="37825-165">That being said, there are several values that are worth highlighting in this article:</span></span>

<span data-ttu-id="37825-166">Element</span><span class="sxs-lookup"><span data-stu-id="37825-166">Element</span></span> | <span data-ttu-id="37825-167">Opis</span><span class="sxs-lookup"><span data-stu-id="37825-167">Description</span></span>
---|---|---
`<version>` | <span data-ttu-id="37825-168">Określa wersję [Maven wtyczki dla aplikacji sieci Web Azure].</span><span class="sxs-lookup"><span data-stu-id="37825-168">Specifies the version of the [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="37825-169">Należy sprawdzić wersji na liście [Maven centralnym repozytorium](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) aby upewnić się, że używasz najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="37825-169">You should check the version listed in the [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) to ensure that you are using the latest version.</span></span>
`<authentication>` | <span data-ttu-id="37825-170">Określa informacje dotyczące uwierzytelniania dla platformy Azure, który w tym przykładzie zawiera `<serverId>` element, który zawiera `azure-auth`; Maven używa tej wartości do wyszukania nazwy głównej usługi Azure wartości w Twojej Maven *settings.xml* pliku, który został zdefiniowany w wcześniejszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="37825-170">Specifies the authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value to look up the Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span>
`<resourceGroup>` | <span data-ttu-id="37825-171">Określa, docelowa grupa zasobów, która jest `maven-plugin` w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="37825-171">Specifies the target resource group, which is `maven-plugin` in this example.</span></span> <span data-ttu-id="37825-172">Nazwa grupy zasobów zostanie utworzony podczas wdrażania, jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="37825-172">The resource group will be created during deployment if it does not already exist.</span></span>
`<appName>` | <span data-ttu-id="37825-173">Określa docelową nazwę dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="37825-173">Specifies the target name for your web app.</span></span> <span data-ttu-id="37825-174">W tym przykładzie nazwa docelowa jest `maven-linux-app-${maven.build.timestamp}`, gdzie `${maven.build.timestamp}` jest do niej dołączany sufiks w tym przykładzie, aby uniknąć konfliktu.</span><span class="sxs-lookup"><span data-stu-id="37825-174">In this example, the target name is `maven-linux-app-${maven.build.timestamp}`, where the `${maven.build.timestamp}` suffix is appended in this example to avoid conflict.</span></span> <span data-ttu-id="37825-175">(Sygnatura czasowa jest opcjonalny; można określić dowolny unikatowy ciąg dla nazwy aplikacji).</span><span class="sxs-lookup"><span data-stu-id="37825-175">(The timestamp is optional; you can specify any unique string for the app name.)</span></span>
`<region>` | <span data-ttu-id="37825-176">Określa region docelowy, który w tym przykładzie jest `westus`.</span><span class="sxs-lookup"><span data-stu-id="37825-176">Specifies the target region, which in this example is `westus`.</span></span> <span data-ttu-id="37825-177">(Pełna lista jest w [Maven wtyczki dla aplikacji sieci Web Azure] dokumentacji.)</span><span class="sxs-lookup"><span data-stu-id="37825-177">(A full list is in the [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<appSettings>` | <span data-ttu-id="37825-178">Określa unikatowy ustawienia Maven do użycia podczas wdrażania aplikacji sieci web na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="37825-178">Specifies any unique settings for Maven to use when deploying your web app to Azure.</span></span> <span data-ttu-id="37825-179">W tym przykładzie `<property>` element zawiera pary nazwa/wartość elementów podrzędnych, które określić port dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="37825-179">In this example, a `<property>` element contains a name/value pair of child elements that specify the port for your app.</span></span>

> [!NOTE]
>
> <span data-ttu-id="37825-180">Ustawienia, aby zmienić numer portu w tym przykładzie jest konieczne tylko w przypadku, gdy zmieniasz portu domyślnego.</span><span class="sxs-lookup"><span data-stu-id="37825-180">The settings to change the port number in this example are only necessary when you are changing the port from the default.</span></span>
>

## <a name="build-and-deploy-your-container-to-azure"></a><span data-ttu-id="37825-181">Tworzenie i wdrażanie z kontenera na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="37825-181">Build and deploy your container to Azure</span></span>

<span data-ttu-id="37825-182">Po skonfigurowaniu wszystkich ustawień w poprzednich sekcjach tego artykułu, można przystąpić do wdrażania z kontenera na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="37825-182">Once you have configured all of the settings in the preceding sections of this article, you are ready to deploy your container to Azure.</span></span> <span data-ttu-id="37825-183">Aby to zrobić, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="37825-183">To do so, use the following steps:</span></span>

1. <span data-ttu-id="37825-184">Z wiersza polecenia lub okno terminalu, które były wcześniej używane, skompiluj ponownie plik JAR za pomocą programu Maven Jeśli wprowadzono zmiany do *pom.xml* pliku; na przykład:</span><span class="sxs-lookup"><span data-stu-id="37825-184">From the command prompt or terminal window that you were using earlier, rebuild the JAR file using Maven if you made any changes to the *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="37825-185">Wdrażanie aplikacji sieci web na platformie Azure przy użyciu narzędzia Maven; na przykład:</span><span class="sxs-lookup"><span data-stu-id="37825-185">Deploy your web app to Azure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="37825-186">Maven zostanie wdrożona aplikacja sieci web na platformie Azure; Jeśli aplikacja sieci web nie istnieje, zostanie utworzona.</span><span class="sxs-lookup"><span data-stu-id="37825-186">Maven will deploy your web app to Azure; if the web app does not already exist, it will be created.</span></span>

> [!NOTE]
>
> <span data-ttu-id="37825-187">Jeśli region, który jest określony w `<region>` elementu z *pom.xml* plik nie ma wystarczającej liczby serwerów, które są dostępne po uruchomieniu wdrożenia, można napotkać błąd podobny do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="37825-187">If the region which you specify in the `<region>` element of your *pom.xml* file does not have enough servers available when you start your deployment, you might see an error similar to the following example:</span></span>
>
> ```
> [INFO] Start deploying to Web App maven-linux-app-20170804...
> [INFO] ------------------------------------------------------------------------
> [INFO] BUILD FAILURE
> [INFO] ------------------------------------------------------------------------
> [INFO] Total time: 31.059 s
> [INFO] Finished at: 2017-08-04T12:15:47-07:00
> [INFO] Final Memory: 51M/279M
> [INFO] ------------------------------------------------------------------------
> [ERROR] Failed to execute goal com.microsoft.azure:azure-webapp-maven-plugin:0.1.3:deploy (default-cli) on project gs-spring-boot-docker: null: MojoExecutionException: CloudException: OnError while emitting onNext value: retrofit2.Response.class
> ```
>
> <span data-ttu-id="37825-188">W takim przypadku można określić innego regionu i uruchom ponownie polecenie narzędzia Maven, aby wdrożyć aplikację.</span><span class="sxs-lookup"><span data-stu-id="37825-188">If this happens, you can specify another region and re-run the Maven command to deploy your application.</span></span>
>
>

<span data-ttu-id="37825-189">Po wdrożeniu sieci web będzie można zarządzać nim za pomocą [portalu Azure].</span><span class="sxs-lookup"><span data-stu-id="37825-189">When your web has been deployed, you will be able to manage it by using the [Azure portal].</span></span>

* <span data-ttu-id="37825-190">Aplikacja sieci web zostaną wyświetlone w **usługi aplikacji**:</span><span class="sxs-lookup"><span data-stu-id="37825-190">Your web app will be listed in **App Services**:</span></span>

   ![Aplikacja sieci Web wyświetlane w portalu Azure usługi aplikacji][AP01]

* <span data-ttu-id="37825-192">I adres URL aplikacji sieci web zostaną wyświetlone w **omówienie** dla aplikacji sieci web:</span><span class="sxs-lookup"><span data-stu-id="37825-192">And the URL for your web app will be listed in the **Overview** for your web app:</span></span>

   ![Określanie adresu URL dla aplikacji sieci web][AP02]

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

## <a name="next-steps"></a><span data-ttu-id="37825-194">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="37825-194">Next steps</span></span>

<span data-ttu-id="37825-195">Aby uzyskać więcej informacji na temat różne technologie omówione w tym artykule zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="37825-195">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* <span data-ttu-id="37825-196">[Maven wtyczki dla aplikacji sieci Web Azure]</span><span class="sxs-lookup"><span data-stu-id="37825-196">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="37825-197">Logowanie do platformy Azure z interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="37825-197">Log in to Azure from the Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="37825-198">Jak używać wtyczki Maven dla aplikacji sieci Web platformy Azure można wdrożyć aplikacji Spring rozruchu z usługi aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="37825-198">How to use the Maven Plugin for Azure Web Apps to deploy a Spring Boot app to Azure App Service </span></span>](app-service-web-deploy-spring-boot-app-with-maven-plugin.md)

* [<span data-ttu-id="37825-199">Tworzenie nazwy głównej usługi platformy Azure z 2.0 interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="37825-199">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="37825-200">Informacje o ustawieniach maven</span><span class="sxs-lookup"><span data-stu-id="37825-200">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

* <span data-ttu-id="37825-201">[wtyczki Docker przypadku Maven]</span><span class="sxs-lookup"><span data-stu-id="37825-201">[Docker plugin for Maven]</span></span>

<!-- URL List -->

<span data-ttu-id="37825-202">[Azure interfejsu wiersza polecenia (CLI)]: /cli/azure/overview</span><span class="sxs-lookup"><span data-stu-id="37825-202">[Azure Command-Line Interface (CLI)]: /cli/azure/overview</span></span>
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
<span data-ttu-id="37825-203">[portalu Azure]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="37825-203">[Azure portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="37825-204">[Docker]: https://www.docker.com/</span><span class="sxs-lookup"><span data-stu-id="37825-204">[Docker]: https://www.docker.com/</span></span>
<span data-ttu-id="37825-205">[wtyczki Docker przypadku Maven]: https://github.com/spotify/docker-maven-plugin</span><span class="sxs-lookup"><span data-stu-id="37825-205">[Docker plugin for Maven]: https://github.com/spotify/docker-maven-plugin</span></span>
<span data-ttu-id="37825-206">[bezpłatne konto platformy Azure]: https://azure.microsoft.com/pricing/free-trial/</span><span class="sxs-lookup"><span data-stu-id="37825-206">[free Azure account]: https://azure.microsoft.com/pricing/free-trial/</span></span>
<span data-ttu-id="37825-207">[Git]: https://github.com/</span><span class="sxs-lookup"><span data-stu-id="37825-207">[Git]: https://github.com/</span></span>
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
<span data-ttu-id="37825-208">[Maven]: http://maven.apache.org/</span><span class="sxs-lookup"><span data-stu-id="37825-208">[Maven]: http://maven.apache.org/</span></span>
<span data-ttu-id="37825-209">[korzyści dla subskrybentów MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span><span class="sxs-lookup"><span data-stu-id="37825-209">[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span></span>
[Spring Boot]: http://projects.spring.io/spring-boot/
<span data-ttu-id="37825-210">[rozruchu Spring na wprowadzenie Docker]: https://github.com/spring-guides/gs-spring-boot-docker</span><span class="sxs-lookup"><span data-stu-id="37825-210">[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker</span></span>
[Spring Framework]: https://spring.io/
<span data-ttu-id="37825-211">[Maven wtyczki dla aplikacji sieci Web Azure]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin</span><span class="sxs-lookup"><span data-stu-id="37825-211">[Maven Plugin for Azure Web Apps]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin</span></span>

<!-- IMG List -->

[AP01]: ./media/app-service-web-deploy-containerized-spring-boot-app-with-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-containerized-spring-boot-app-with-maven-plugin/AP02.png
