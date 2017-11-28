---
title: Witaj toouse aaaHow Maven wtyczki dla aplikacji sieci Web Azure toodeploy tooAzure aplikacji Spring rozruchu
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
ms.openlocfilehash: 376fe90fe20621e15d7c9856214937c78b66026a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-spring-boot-app-tooazure"></a><span data-ttu-id="8913f-103">Jak toouse hello wtyczki Maven dla aplikacji sieci Web Azure toodeploy tooAzure aplikacji Spring rozruchu</span><span class="sxs-lookup"><span data-stu-id="8913f-103">How toouse hello Maven Plugin for Azure Web Apps toodeploy a Spring Boot app tooAzure</span></span>

<span data-ttu-id="8913f-104">Witaj [Maven wtyczki dla aplikacji sieci Web Azure](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) dla [Apache Maven](http://maven.apache.org/) zapewnia bezproblemową integrację usługi Azure App Service w projekty Maven oraz usprawnia proces powitania dla aplikacji sieci web do deweloperzy toodeploy tooAzure usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8913f-104">hello [Maven Plugin for Azure Web Apps](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) for [Apache Maven](http://maven.apache.org/) provides seamless integration of Azure App Service into Maven projects, and streamlines hello process for developers toodeploy web apps tooAzure App Service.</span></span>

<span data-ttu-id="8913f-105">W tym artykule przedstawiono przy użyciu hello Maven wtyczki dla aplikacji sieci Web Azure toodeploy próbki tooAzure aplikacji rozruchu Spring usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8913f-105">This article demonstrates using hello Maven Plugin for Azure Web Apps toodeploy a sample Spring Boot application tooAzure App Services.</span></span>

> [!NOTE]
>
> <span data-ttu-id="8913f-106">Witaj Maven wtyczki dla aplikacji sieci Web platformy Azure jest obecnie dostępna jako podgląd.</span><span class="sxs-lookup"><span data-stu-id="8913f-106">hello Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="8913f-107">Obecnie jest obsługiwana tylko publikacji FTP, chociaż hello przyszłości planowane dodatkowe funkcje.</span><span class="sxs-lookup"><span data-stu-id="8913f-107">For now, only FTP publishing is supported, although additional features are planned for hello future.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="8913f-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8913f-108">Prerequisites</span></span>

<span data-ttu-id="8913f-109">Kolejność toocomplete hello kroki w tym samouczku potrzebne hello toohave następujące wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="8913f-109">In order toocomplete hello steps in this tutorial, you need toohave hello following prerequisites:</span></span>

* <span data-ttu-id="8913f-110">Subskrypcja platformy Azure; Jeśli nie masz jeszcze subskrypcji platformy Azure, możesz przeprowadzić aktywację Twojej [korzyści dla subskrybentów MSDN] lub zarejestrować się w celu [bezpłatne konto platformy Azure].</span><span class="sxs-lookup"><span data-stu-id="8913f-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="8913f-111">Witaj [Azure interfejsu wiersza polecenia (CLI)].</span><span class="sxs-lookup"><span data-stu-id="8913f-111">hello [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="8913f-112">Aktualne [Java Development Kit (JDK)], wersja 1.7 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="8913f-112">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="8913f-113">Apache na [Maven] (w wersji 3) Narzędzie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="8913f-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="8913f-114">A [Git] klienta.</span><span class="sxs-lookup"><span data-stu-id="8913f-114">A [Git] client.</span></span>

## <a name="clone-hello-sample-spring-boot-web-app"></a><span data-ttu-id="8913f-115">Witaj klonowania Spring rozruchu przykładową aplikację sieci web</span><span class="sxs-lookup"><span data-stu-id="8913f-115">Clone hello sample Spring Boot web app</span></span>

<span data-ttu-id="8913f-116">W tej sekcji sklonować ukończona aplikacja Spring rozruchu i przetestować go lokalnie.</span><span class="sxs-lookup"><span data-stu-id="8913f-116">In this section, you clone a completed Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="8913f-117">Otwórz wiersz polecenia lub okno terminalu i utworzyć toohold lokalnego katalogu aplikacji Spring rozruchu i zmień katalog toothat; na przykład:</span><span class="sxs-lookup"><span data-stu-id="8913f-117">Open a command prompt or terminal window and create a local directory toohold your Spring Boot application, and change toothat directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="8913f-118">--lub--</span><span class="sxs-lookup"><span data-stu-id="8913f-118">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="8913f-119">Witaj w klonowania [Spring wprowadzenie rozruchu] przykładowy projekt do katalogu hello utworzony; na przykład:</span><span class="sxs-lookup"><span data-stu-id="8913f-119">Clone hello [Spring Boot Getting Started] sample project into hello directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/microsoft/gs-spring-boot
   ```

1. <span data-ttu-id="8913f-120">Zmień katalog projektu toohello ukończone; na przykład:</span><span class="sxs-lookup"><span data-stu-id="8913f-120">Change directory toohello completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot/complete
   ```

1. <span data-ttu-id="8913f-121">Kompiluj plik JAR hello za pomocą programu Maven; na przykład:</span><span class="sxs-lookup"><span data-stu-id="8913f-121">Build hello JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="8913f-122">Podczas tworzenia aplikacji sieci web hello uruchomić aplikacji sieci web hello za pomocą programu Maven; na przykład:</span><span class="sxs-lookup"><span data-stu-id="8913f-122">When hello web app has been created, start hello web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="8913f-123">Testowanie aplikacji sieci web hello przechodząc tooit lokalnie za pomocą przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="8913f-123">Test hello web app by browsing tooit locally using a web browser.</span></span> <span data-ttu-id="8913f-124">Na przykład można użyć hello następujące polecenie, jeśli masz curl dostępne:</span><span class="sxs-lookup"><span data-stu-id="8913f-124">For example, you could use hello following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="8913f-125">Powinien zostać wyświetlony komunikat wyświetlany po hello: **pozdrowienia z Spring rozruchowe!**</span><span class="sxs-lookup"><span data-stu-id="8913f-125">You should see hello following message displayed: **Greetings from Spring Boot!**</span></span>

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="8913f-126">Tworzenie nazwy głównej usługi platformy Azure</span><span class="sxs-lookup"><span data-stu-id="8913f-126">Create an Azure service principal</span></span>

<span data-ttu-id="8913f-127">W tej sekcji utworzysz Azure nazwy głównej usługi, który używa wtyczki Maven Witaj, wdrażając tooAzure aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="8913f-127">In this section, you create an Azure service principal that hello Maven plugin uses when deploying your web app tooAzure.</span></span>

1. <span data-ttu-id="8913f-128">Otwórz wiersz polecenia.</span><span class="sxs-lookup"><span data-stu-id="8913f-128">Open a command prompt.</span></span>

1. <span data-ttu-id="8913f-129">Zaloguj się do konta platformy Azure przy użyciu hello wiersza polecenia platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="8913f-129">Sign into your Azure account by using hello Azure CLI:</span></span>
   ```shell
   az login
   ```
   <span data-ttu-id="8913f-130">Wykonaj hello instrukcje toocomplete hello procesu logowania.</span><span class="sxs-lookup"><span data-stu-id="8913f-130">Follow hello instructions toocomplete hello sign-in process.</span></span>

1. <span data-ttu-id="8913f-131">Tworzenie nazwy głównej usługi platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="8913f-131">Create an Azure service principal:</span></span>
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="8913f-132">Gdzie `uuuuuuuu` jest nazwą użytkownika hello i `pppppppp` jest hello hasło dla nazwy głównej usługi hello.</span><span class="sxs-lookup"><span data-stu-id="8913f-132">Where `uuuuuuuu` is hello user name and `pppppppp` is hello password for hello service principal.</span></span>

1. <span data-ttu-id="8913f-133">Azure odpowiada JSON podobny hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="8913f-133">Azure responds with JSON that resembles hello following example:</span></span>
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
   > <span data-ttu-id="8913f-134">Po skonfigurowaniu hello Maven wtyczki toodeploy tooAzure aplikacji sieci web, użyje hello wartości z tej odpowiedzi JSON.</span><span class="sxs-lookup"><span data-stu-id="8913f-134">You will use hello values from this JSON response when you configure hello Maven plugin toodeploy your web app tooAzure.</span></span> <span data-ttu-id="8913f-135">Hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, i `tttttttt` są symbole zastępcze, które są używane w tej toomake przykład go łatwiejsze toomap tych wartości tootheir odpowiednich elementów podczas konfigurowania programu Maven `settings.xml` w hello obok pliku sekcja.</span><span class="sxs-lookup"><span data-stu-id="8913f-135">hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example toomake it easier toomap these values tootheir respective elements when you configure your Maven `settings.xml` file in hello next section.</span></span>
   >
   >

## <a name="configure-maven-toouse-your-azure-service-principal"></a><span data-ttu-id="8913f-136">Skonfiguruj Maven toouse Twojej nazwy głównej usługi Azure</span><span class="sxs-lookup"><span data-stu-id="8913f-136">Configure Maven toouse your Azure service principal</span></span>

<span data-ttu-id="8913f-137">W tej sekcji można użyć wartości hello z uwierzytelniania hello tooconfigure główną usługi Azure używającej Maven, wdrażając tooAzure aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="8913f-137">In this section, you use hello values from your Azure service principal tooconfigure hello authentication that Maven uses when deploying your web app tooAzure.</span></span>

1. <span data-ttu-id="8913f-138">Otwieranie programu Maven `settings.xml` plik w edytorze tekstów; ten plik może być w ścieżce, takie jak hello następujące przykłady:</span><span class="sxs-lookup"><span data-stu-id="8913f-138">Open your Maven `settings.xml` file in a text editor; this file might be in a path like hello following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="8913f-139">Dodaj ustawienia głównych usług Azure hello w poprzedniej sekcji tego samouczka toohello `<servers>` kolekcji w hello *settings.xml* pliku; na przykład:</span><span class="sxs-lookup"><span data-stu-id="8913f-139">Add your Azure service principal settings from hello previous section of this tutorial toohello `<servers>` collection in hello *settings.xml* file; for example:</span></span>

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
   <span data-ttu-id="8913f-140">Gdzie:</span><span class="sxs-lookup"><span data-stu-id="8913f-140">Where:</span></span>
   <span data-ttu-id="8913f-141">Element</span><span class="sxs-lookup"><span data-stu-id="8913f-141">Element</span></span> | <span data-ttu-id="8913f-142">Opis</span><span class="sxs-lookup"><span data-stu-id="8913f-142">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="8913f-143">Określa unikatową nazwę używający Maven toolook zapasową ustawień zabezpieczeń podczas wdrażania tooAzure aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="8913f-143">Specifies a unique name which Maven uses toolook up your security settings when you deploy your web app tooAzure.</span></span>
   `<client>` | <span data-ttu-id="8913f-144">Zawiera hello `appId` wartość z Twojej nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="8913f-144">Contains hello `appId` value from your service principal.</span></span>
   `<tenant>` | <span data-ttu-id="8913f-145">Zawiera hello `tenant` wartość z Twojej nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="8913f-145">Contains hello `tenant` value from your service principal.</span></span>
   `<key>` | <span data-ttu-id="8913f-146">Zawiera hello `password` wartość z Twojej nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="8913f-146">Contains hello `password` value from your service principal.</span></span>
   `<environment>` | <span data-ttu-id="8913f-147">Definiuje hello docelowej chmury Azure środowisko, które jest `AZURE` w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="8913f-147">Defines hello target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="8913f-148">(Pełna lista środowisk jest dostępna w hello [Maven wtyczki dla aplikacji sieci Web Azure] dokumentacji)</span><span class="sxs-lookup"><span data-stu-id="8913f-148">(A full list of environments is available in hello [Maven Plugin for Azure Web Apps] documentation)</span></span>

1. <span data-ttu-id="8913f-149">Zapisz i zamknij hello *settings.xml* pliku.</span><span class="sxs-lookup"><span data-stu-id="8913f-149">Save and close hello *settings.xml* file.</span></span>

## <a name="optional-customize-your-pomxml-before-deploying-your-web-app-tooazure"></a><span data-ttu-id="8913f-150">OPCJONALNIE: Dostosowywanie programu pom.xml przed wdrożeniem tooAzure aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="8913f-150">OPTIONAL: Customize your pom.xml before deploying your web app tooAzure</span></span>

<span data-ttu-id="8913f-151">Otwórz hello `pom.xml` pliku aplikacji Spring rozruchu w edytorze tekstu, a następnie zlokalizuj hello `<plugin>` elementu `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="8913f-151">Open hello `pom.xml` file for your Spring Boot application in a text editor, and then locate hello `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="8913f-152">Ten element powinien wyglądać hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="8913f-152">This element should resemble hello following example:</span></span>

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
         <appName>maven-web-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <javaVersion>1.8</javaVersion>
         <deploymentType>ftp</deploymentType>
         <resources>
            <resource>
               <directory>${project.basedir}/target</directory>
               <targetPath>/</targetPath>
               <includes>
                  <include>*.jar</include>
               </includes>
            </resource>
            <resource>
               <directory>${project.basedir}</directory>
               <targetPath>/</targetPath>
               <includes>
                  <include>web.config</include>
               </includes>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```

<span data-ttu-id="8913f-153">Istnieje kilka wartości, które można modyfikować dla wtyczki Maven hello i szczegółowy opis każdego z tych elementów jest dostępna w hello [Maven wtyczki dla aplikacji sieci Web Azure] dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="8913f-153">There are several values that you can modify for hello Maven plugin, and a detailed description for each of these elements is available in hello [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="8913f-154">Który trwa wspomniano, istnieje kilka wartości, które warto wyróżnianie w tym artykule:</span><span class="sxs-lookup"><span data-stu-id="8913f-154">That being said, there are several values that are worth highlighting in this article:</span></span>

<span data-ttu-id="8913f-155">Element</span><span class="sxs-lookup"><span data-stu-id="8913f-155">Element</span></span> | <span data-ttu-id="8913f-156">Opis</span><span class="sxs-lookup"><span data-stu-id="8913f-156">Description</span></span>
---|---|---
`<version>` | <span data-ttu-id="8913f-157">Określa wersję hello hello [Maven wtyczki dla aplikacji sieci Web Azure].</span><span class="sxs-lookup"><span data-stu-id="8913f-157">Specifies hello version of hello [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="8913f-158">Należy sprawdzić wersji hello na liście hello [Maven centralnym repozytorium](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure, którego używasz hello najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="8913f-158">You should check hello version listed in hello [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure that you are using hello latest version.</span></span>
`<authentication>` | <span data-ttu-id="8913f-159">Określa hello informacje dotyczące uwierzytelniania dla platformy Azure, który w tym przykładzie zawiera `<serverId>` element, który zawiera `azure-auth`; Maven używa tej wartości toolook wartości podmiotu zabezpieczeń usługi Azure hello programu Maven *settings.xml* pliku, który został zdefiniowany w wcześniejszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="8913f-159">Specifies hello authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value toolook up hello Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span>
`<resourceGroup>` | <span data-ttu-id="8913f-160">Określa, docelowa grupa zasobów hello, który jest `maven-plugin` w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="8913f-160">Specifies hello target resource group, which is `maven-plugin` in this example.</span></span> <span data-ttu-id="8913f-161">Grupa zasobów Hello jest tworzona podczas wdrażania, jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="8913f-161">hello resource group is created during deployment if it does not already exist.</span></span>
`<appName>` | <span data-ttu-id="8913f-162">Określa nazwę docelowej hello aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="8913f-162">Specifies hello target name for your web app.</span></span> <span data-ttu-id="8913f-163">W tym przykładzie nazwa docelowego hello jest `maven-web-app-${maven.build.timestamp}`, gdzie hello `${maven.build.timestamp}` jest do niej dołączany sufiks w tej konflikt tooavoid przykład.</span><span class="sxs-lookup"><span data-stu-id="8913f-163">In this example, hello target name is `maven-web-app-${maven.build.timestamp}`, where hello `${maven.build.timestamp}` suffix is appended in this example tooavoid conflict.</span></span> <span data-ttu-id="8913f-164">(sygnatura czasowa hello jest opcjonalne; można określić dowolny unikatowy ciąg dla nazwy aplikacji hello).</span><span class="sxs-lookup"><span data-stu-id="8913f-164">(hello timestamp is optional; you can specify any unique string for hello app name.)</span></span>
`<region>` | <span data-ttu-id="8913f-165">Określa region docelowy hello, czyli w tym przykładzie `westus`.</span><span class="sxs-lookup"><span data-stu-id="8913f-165">Specifies hello target region, which in this example is `westus`.</span></span> <span data-ttu-id="8913f-166">(Pełna lista jest w hello [Maven wtyczki dla aplikacji sieci Web Azure] dokumentacji.)</span><span class="sxs-lookup"><span data-stu-id="8913f-166">(A full list is in hello [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<javaVersion>` | <span data-ttu-id="8913f-167">Określa wersję środowiska uruchomieniowego języka Java powitania dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="8913f-167">Specifies hello Java runtime version for your web app.</span></span> <span data-ttu-id="8913f-168">(Pełna lista jest w hello [Maven wtyczki dla aplikacji sieci Web Azure] dokumentacji.)</span><span class="sxs-lookup"><span data-stu-id="8913f-168">(A full list is in hello [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<deploymentType>` | <span data-ttu-id="8913f-169">Określa typ wdrożenia dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="8913f-169">Specifies deployment type for your web app.</span></span> <span data-ttu-id="8913f-170">Obecnie tylko `ftp` jest obsługiwana, chociaż obsługuje inne typy wdrożenia jest programowanie.</span><span class="sxs-lookup"><span data-stu-id="8913f-170">For now, only `ftp` is supported, although support for other deployment types is in development.</span></span>
`<resources>` | <span data-ttu-id="8913f-171">Określa zasobów i docelowy miejsc docelowych, które Maven używa podczas wdrażania tooAzure aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="8913f-171">Specifies resources and target destinations which Maven uses when deploying your web app tooAzure.</span></span> <span data-ttu-id="8913f-172">W tym przykładzie dwa `<resource>` elementy Określ, czy Maven wdroży hello plik JAR dla aplikacji sieci web i hello *web.config* pliku z hello rozruchu Spring projektu.</span><span class="sxs-lookup"><span data-stu-id="8913f-172">In this example, two `<resource>` elements specify that Maven will deploy hello JAR file for your web app and hello *web.config* file from hello Spring Boot project.</span></span>

## <a name="build-and-deploy-your-web-app-tooazure"></a><span data-ttu-id="8913f-173">Tworzenie i wdrażanie tooAzure aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="8913f-173">Build and deploy your web app tooAzure</span></span>

<span data-ttu-id="8913f-174">Po skonfigurowaniu wszystkich ustawień hello w hello powyższej sekcji tego artykułu, są gotowe toodeploy tooAzure aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="8913f-174">Once you have configured all of hello settings in hello preceding sections of this article, you are ready toodeploy your web app tooAzure.</span></span> <span data-ttu-id="8913f-175">toodo tak, użycie hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="8913f-175">toodo so, use hello following steps:</span></span>

1. <span data-ttu-id="8913f-176">Z wiersza polecenia hello lub okno terminalu, które były wcześniej używane odbudować plik JAR hello za pomocą programu Maven Jeśli wprowadzono żadnych zmian toohello *pom.xml* pliku; na przykład:</span><span class="sxs-lookup"><span data-stu-id="8913f-176">From hello command prompt or terminal window that you were using earlier, rebuild hello JAR file using Maven if you made any changes toohello *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="8913f-177">Wdrażanie tooAzure aplikacji sieci web przy użyciu narzędzia Maven; na przykład:</span><span class="sxs-lookup"><span data-stu-id="8913f-177">Deploy your web app tooAzure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="8913f-178">Maven wdroży tooAzure aplikacji sieci web; Jeśli aplikacja sieci web hello jeszcze nie istnieje, zostanie utworzona.</span><span class="sxs-lookup"><span data-stu-id="8913f-178">Maven will deploy your web app tooAzure; if hello web app does not already exist, it will be created.</span></span>

<span data-ttu-id="8913f-179">Po wdrożeniu sieci web będą mogli toomanage go za pomocą hello [portalu Azure].</span><span class="sxs-lookup"><span data-stu-id="8913f-179">When your web has been deployed, you will be able toomanage it by using hello [Azure portal].</span></span>

* <span data-ttu-id="8913f-180">Aplikacja sieci web zostaną wyświetlone w **usługi aplikacji**:</span><span class="sxs-lookup"><span data-stu-id="8913f-180">Your web app will be listed in **App Services**:</span></span>

   ![Aplikacja sieci Web wyświetlane w portalu Azure usługi aplikacji][AP01]

* <span data-ttu-id="8913f-182">I hello adres URL dla aplikacji sieci web zostaną wyświetlone w hello **omówienie** dla aplikacji sieci web:</span><span class="sxs-lookup"><span data-stu-id="8913f-182">And hello URL for your web app will be listed in hello **Overview** for your web app:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="8913f-184">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8913f-184">Next steps</span></span>

<span data-ttu-id="8913f-185">Aby uzyskać więcej informacji na temat hello różne technologie omówione w tym artykule, zobacz hello następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="8913f-185">For more information about hello various technologies discussed in this article, see hello following articles:</span></span>

* <span data-ttu-id="8913f-186">[Maven wtyczki dla aplikacji sieci Web Azure]</span><span class="sxs-lookup"><span data-stu-id="8913f-186">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="8913f-187">Zaloguj się za tooAzure z hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="8913f-187">Log in tooAzure from hello Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="8913f-188">Jak toouse hello wtyczki Maven dla aplikacji sieci Web Azure toodeploy konteneryzowanych tooAzure aplikacji Spring rozruchu</span><span class="sxs-lookup"><span data-stu-id="8913f-188">How toouse hello Maven Plugin for Azure Web Apps toodeploy a containerized Spring Boot app tooAzure</span></span>](app-service-web-deploy-containerized-spring-boot-app-with-maven-plugin.md)

* [<span data-ttu-id="8913f-189">Tworzenie nazwy głównej usługi platformy Azure z 2.0 interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="8913f-189">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="8913f-190">Informacje o ustawieniach maven</span><span class="sxs-lookup"><span data-stu-id="8913f-190">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

<!-- URL List -->

[Azure interfejsu wiersza polecenia (CLI)]: /cli/azure/overview
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[portalu Azure]: https://portal.azure.com/
[bezpłatne konto platformy Azure]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[korzyści dla subskrybentów MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring wprowadzenie rozruchu]: https://github.com/microsoft/gs-spring-boot
[Spring Framework]: https://spring.io/
[Maven wtyczki dla aplikacji sieci Web Azure]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin

<!-- IMG List -->

[AP01]: ./media/app-service-web-deploy-spring-boot-app-with-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-spring-boot-app-with-maven-plugin/AP02.png
