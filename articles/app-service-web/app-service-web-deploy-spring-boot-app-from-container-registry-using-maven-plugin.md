---
title: "Jak używać wtyczki Maven dla aplikacji sieci Web platformy Azure można wdrożyć aplikacji Spring rozruchu w rejestrze kontenera platformy Azure w usłudze Azure App Service"
description: "W tym samouczku opisano jednak kroki, aby wdrożyć aplikację Spring rozruchu w rejestrze kontenera Azure Azure do usługi Azure App Service przy użyciu wtyczki Maven."
services: 
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 08/07/2017
ms.author: robmcm;kevinzha
ms.openlocfilehash: f47ee59d72ea49d62be2cb435ebaf8bc841e4198
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-the-maven-plugin-for-azure-web-apps-to-deploy-a-spring-boot-app-in-azure-container-registry-to-azure-app-service"></a><span data-ttu-id="ef1d2-103">Jak używać wtyczki Maven dla aplikacji sieci Web platformy Azure można wdrożyć aplikacji Spring rozruchu w rejestrze kontenera platformy Azure w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="ef1d2-103">How to use the Maven Plugin for Azure Web Apps to deploy a Spring Boot app in Azure Container Registry to Azure App Service</span></span>

<span data-ttu-id="ef1d2-104"> **[Spring Framework]**  popularnych struktura open source, który pomaga Java deweloperom tworzenie aplikacji interfejsu API, mobilne i sieci web.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-104">The **[Spring Framework]** is a popular open-source framework that helps Java developers create web, mobile, and API applications.</span></span> <span data-ttu-id="ef1d2-105">W tym samouczku używana przykładowej aplikacji utworzony za pomocą [rozruchu Spring], podejście oparte na Konwencji do szybkie rozpoczęcie pracy przy użyciu źródła.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-105">This tutorial uses a sample app created using [Spring Boot], a convention-driven approach for using Spring to get started quickly.</span></span>

<span data-ttu-id="ef1d2-106">W tym artykule przedstawiono sposób wdrażania przykładowej aplikacji Spring rozruchu w rejestrze kontenera Azure i następnie wdrażanie aplikacji w usłudze Azure App Service za pomocą wtyczki Maven dla aplikacji sieci Web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-106">This article demonstrates how to deploy a sample Spring Boot application to Azure Container Registry, and then use the Maven Plugin for Azure Web Apps to deploy your application to Azure App Service.</span></span>

> [!NOTE]
>
> <span data-ttu-id="ef1d2-107">Dodatek plug-in Maven dla aplikacji sieci Web Azure jest obecnie dostępna jako podgląd.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-107">The Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="ef1d2-108">Obecnie jest obsługiwana tylko publikacji FTP, chociaż dodatkowe funkcje są planowane w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-108">For now, only FTP publishing is supported, although additional features are planned for the future.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="ef1d2-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ef1d2-109">Prerequisites</span></span>

<span data-ttu-id="ef1d2-110">Aby wykonać kroki opisane w tym samouczku, musisz mieć następujące wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="ef1d2-110">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="ef1d2-111">Subskrypcja platformy Azure; Jeśli nie masz jeszcze subskrypcji platformy Azure, możesz przeprowadzić aktywację Twojej [korzyści dla subskrybentów MSDN] lub zarejestrować się w celu [bezpłatne konto platformy Azure].</span><span class="sxs-lookup"><span data-stu-id="ef1d2-111">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="ef1d2-112">[Azure interfejsu wiersza polecenia (CLI)].</span><span class="sxs-lookup"><span data-stu-id="ef1d2-112">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="ef1d2-113">Aktualne [Java Development Kit (JDK)], wersja 1.7 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-113">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="ef1d2-114">Apache na [Maven] (w wersji 3) Narzędzie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-114">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="ef1d2-115">A [Git] klienta.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-115">A [Git] client.</span></span>
* <span data-ttu-id="ef1d2-116">A [Docker] klienta.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-116">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="ef1d2-117">Ze względu na wymagania dotyczące wirtualizacji w tym samouczku nie można wykonać kroki opisane w tym artykule na maszynie wirtualnej; należy użyć komputera fizycznego z włączonymi funkcjami wirtualizacji.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-117">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="clone-the-sample-spring-boot-on-docker-web-app"></a><span data-ttu-id="ef1d2-118">Klonowanie próbki Spring rozruchu w aplikacji sieci web Docker</span><span class="sxs-lookup"><span data-stu-id="ef1d2-118">Clone the sample Spring Boot on Docker web app</span></span>

<span data-ttu-id="ef1d2-119">W tej sekcji sklonować konteneryzowanych aplikacji rozruchu Spring i przetestować go lokalnie.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-119">In this section, you clone a containerized Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="ef1d2-120">Otwórz wiersz polecenia lub okno terminalu i utworzyć katalogu lokalnego do przechowywania aplikacji Spring rozruchu, przejdź do tego katalogu; na przykład:</span><span class="sxs-lookup"><span data-stu-id="ef1d2-120">Open a command prompt or terminal window and create a local directory to hold your Spring Boot application, and change to that directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="ef1d2-121">--lub--</span><span class="sxs-lookup"><span data-stu-id="ef1d2-121">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="ef1d2-122">Klonowanie [rozruchu Spring na wprowadzenie Docker] przykładowy projekt do katalogu utworzonego; na przykład:</span><span class="sxs-lookup"><span data-stu-id="ef1d2-122">Clone the [Spring Boot on Docker Getting Started] sample project into the directory you created; for example:</span></span>
   ```shell
   git clone -b private-registry https://github.com/Microsoft/gs-spring-boot-docker
   ```

1. <span data-ttu-id="ef1d2-123">Zmień katalog na ukończone projektu; na przykład:</span><span class="sxs-lookup"><span data-stu-id="ef1d2-123">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="ef1d2-124">Kompiluj plik JAR za pomocą programu Maven; na przykład:</span><span class="sxs-lookup"><span data-stu-id="ef1d2-124">Build the JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="ef1d2-125">Po utworzeniu aplikacji sieci web, należy uruchomić aplikację sieci web za pomocą programu Maven; na przykład:</span><span class="sxs-lookup"><span data-stu-id="ef1d2-125">When the web app has been created, start the web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="ef1d2-126">Testowanie aplikacji sieci web przy użyciu przeglądania lokalnie za pomocą przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-126">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="ef1d2-127">Na przykład można użyć następującego polecenia Jeśli masz curl dostępne:</span><span class="sxs-lookup"><span data-stu-id="ef1d2-127">For example, you could use the following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="ef1d2-128">Powinien zostać wyświetlony następujący komunikat wyświetlany: **Hello, World Docker**</span><span class="sxs-lookup"><span data-stu-id="ef1d2-128">You should see the following message displayed: **Hello Docker World**</span></span>

   ![Przejdź do przykładowej aplikacji lokalnie][SB01]

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="ef1d2-130">Tworzenie nazwy głównej usługi platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ef1d2-130">Create an Azure service principal</span></span>

<span data-ttu-id="ef1d2-131">W tej sekcji utworzysz Azure nazwy głównej usługi używającej wtyczki Maven podczas wdrażania z kontenera na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-131">In this section, you create an Azure service principal that the Maven plugin uses when deploying your container to Azure.</span></span>

1. <span data-ttu-id="ef1d2-132">Otwórz wiersz polecenia.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-132">Open a command prompt.</span></span>

1. <span data-ttu-id="ef1d2-133">Zaloguj się do konta platformy Azure przy użyciu wiersza polecenia platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="ef1d2-133">Sign into your Azure account by using the Azure CLI:</span></span>
   ```azurecli
   az login
   ```
   <span data-ttu-id="ef1d2-134">Postępuj zgodnie z instrukcjami, aby ukończyć proces logowania.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-134">Follow the instructions to complete the sign-in process.</span></span>

1. <span data-ttu-id="ef1d2-135">Tworzenie nazwy głównej usługi platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="ef1d2-135">Create an Azure service principal:</span></span>
   ```azurecli
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="ef1d2-136">Gdzie `uuuuuuuu` jest nazwą użytkownika i `pppppppp` jest hasło dla nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-136">Where `uuuuuuuu` is the user name and `pppppppp` is the password for the service principal.</span></span>

1. <span data-ttu-id="ef1d2-137">Azure odpowiada JSON, który podobnego do następującego:</span><span class="sxs-lookup"><span data-stu-id="ef1d2-137">Azure responds with JSON that resembles the following example:</span></span>
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
   > <span data-ttu-id="ef1d2-138">Po skonfigurowaniu dodatek plug-in Maven, aby wdrożyć z kontenera na platformie Azure, będzie używać wartości z tej odpowiedzi JSON.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-138">You will use the values from this JSON response when you configure the Maven plugin to deploy your container to Azure.</span></span> <span data-ttu-id="ef1d2-139">`aaaaaaaa`, `uuuuuuuu`, `pppppppp`, I `tttttttt` są symbole zastępcze, które są używane w tym przykładzie ułatwiające Mapuj tych wartości do ich odpowiednich elementów, podczas konfigurowania programu Maven `settings.xml` pliku w następnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-139">The `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example to make it easier to map these values to their respective elements when you configure your Maven `settings.xml` file in the next section.</span></span>
   >
   >

## <a name="create-an-azure-container-registry-using-the-azure-cli"></a><span data-ttu-id="ef1d2-140">Tworzenie rejestru kontenera Azure za pomocą wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ef1d2-140">Create an Azure Container Registry using the Azure CLI</span></span>

1. <span data-ttu-id="ef1d2-141">Otwórz wiersz polecenia.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-141">Open a command prompt.</span></span>

1. <span data-ttu-id="ef1d2-142">Zaloguj się do konta platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="ef1d2-142">Log in to your Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="ef1d2-143">Utwórz grupę zasobów dla zasobów platformy Azure, które będą używane w tym artykule:</span><span class="sxs-lookup"><span data-stu-id="ef1d2-143">Create a resource group for the Azure resources you will use in this article:</span></span>
   ```azurecli
   az group create --name=wingtiptoysresources --location=westus
   ```
   <span data-ttu-id="ef1d2-144">Zastąp `wingtiptoysresources` w tym przykładzie z unikatową nazwę grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-144">Replace `wingtiptoysresources` in this example with a unique name for your resource group.</span></span>

1. <span data-ttu-id="ef1d2-145">Utwórz rejestru prywatnej kontenera platformy Azure w grupie zasobów dla aplikacji Spring rozruchu:</span><span class="sxs-lookup"><span data-stu-id="ef1d2-145">Create a private Azure container registry in the resource group for your Spring Boot app:</span></span> 
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoysresources --location westus --name wingtiptoysregistry --sku Basic
   ```
   <span data-ttu-id="ef1d2-146">Zastąp `wingtiptoysregistry` w tym przykładzie z unikatową nazwę rejestru kontenera.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-146">Replace `wingtiptoysregistry` in this example with a unique name for your container registry.</span></span>

1. <span data-ttu-id="ef1d2-147">Pobieranie hasła dla kontenera rejestru:</span><span class="sxs-lookup"><span data-stu-id="ef1d2-147">Retrieve the password for your container registry:</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```
   <span data-ttu-id="ef1d2-148">Azure będzie odpowiadać przy użyciu hasła; na przykład:</span><span class="sxs-lookup"><span data-stu-id="ef1d2-148">Azure will respond with your password; for example:</span></span>
   ```json
   {
      "name": "password",
      "value": "xxxxxxxxxx"
   }
   ```

## <a name="add-your-azure-container-registry-and-azure-service-principal-to-your-maven-settings"></a><span data-ttu-id="ef1d2-149">Dodaj rejestru kontenera platformy Azure i nazwę główną usługi Azure w ustawieniach Maven</span><span class="sxs-lookup"><span data-stu-id="ef1d2-149">Add your Azure container registry and Azure service principal to your Maven settings</span></span>

1. <span data-ttu-id="ef1d2-150">Otwieranie programu Maven `settings.xml` plik w edytorze tekstów; ten plik może być w ścieżce, takie jak następujące przykłady:</span><span class="sxs-lookup"><span data-stu-id="ef1d2-150">Open your Maven `settings.xml` file in a text editor; this file might be in a path like the following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="ef1d2-151">Dodawanie ustawień dostępu do rejestru kontenera platformy Azure z poprzedniej sekcji tego artykułu, aby `<servers>` kolekcji w *settings.xml* pliku; na przykład:</span><span class="sxs-lookup"><span data-stu-id="ef1d2-151">Add your Azure Container Registry access settings from the previous section of this article to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>xxxxxxxxxx</password>
      </server>
   </servers>
   ```
   <span data-ttu-id="ef1d2-152">Gdzie:</span><span class="sxs-lookup"><span data-stu-id="ef1d2-152">Where:</span></span>
   <span data-ttu-id="ef1d2-153">Element</span><span class="sxs-lookup"><span data-stu-id="ef1d2-153">Element</span></span> | <span data-ttu-id="ef1d2-154">Opis</span><span class="sxs-lookup"><span data-stu-id="ef1d2-154">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="ef1d2-155">Zawiera nazwę rejestru prywatnej kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-155">Contains the name of your private Azure container registry.</span></span>
   `<username>` | <span data-ttu-id="ef1d2-156">Zawiera nazwę rejestru prywatnej kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-156">Contains the name of your private Azure container registry.</span></span>
   `<password>` | <span data-ttu-id="ef1d2-157">Zawiera hasło, które są pobierane w poprzedniej sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-157">Contains the password you retrieved in the previous section of this article.</span></span>

1. <span data-ttu-id="ef1d2-158">Dodaj ustawienia podmiotu zabezpieczeń usługi Azure z wcześniejszej sekcji tego artykułu, aby `<servers>` kolekcji w *settings.xml* pliku; na przykład:</span><span class="sxs-lookup"><span data-stu-id="ef1d2-158">Add your Azure service principal settings from an earlier section of this article to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

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
   <span data-ttu-id="ef1d2-159">Gdzie:</span><span class="sxs-lookup"><span data-stu-id="ef1d2-159">Where:</span></span>
   <span data-ttu-id="ef1d2-160">Element</span><span class="sxs-lookup"><span data-stu-id="ef1d2-160">Element</span></span> | <span data-ttu-id="ef1d2-161">Opis</span><span class="sxs-lookup"><span data-stu-id="ef1d2-161">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="ef1d2-162">Określa unikatową nazwę Maven używanym w celu wyszukania ustawień zabezpieczeń podczas wdrażania aplikacji sieci web na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-162">Specifies a unique name which Maven uses to look up your security settings when you deploy your web app to Azure.</span></span>
   `<client>` | <span data-ttu-id="ef1d2-163">Zawiera `appId` wartość z Twojej nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-163">Contains the `appId` value from your service principal.</span></span>
   `<tenant>` | <span data-ttu-id="ef1d2-164">Zawiera `tenant` wartość z Twojej nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-164">Contains the `tenant` value from your service principal.</span></span>
   `<key>` | <span data-ttu-id="ef1d2-165">Zawiera `password` wartość z Twojej nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-165">Contains the `password` value from your service principal.</span></span>
   `<environment>` | <span data-ttu-id="ef1d2-166">Definiuje środowisko chmury Azure docelowych, które jest `AZURE` w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-166">Defines the target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="ef1d2-167">(Pełna lista środowisk jest dostępna w [Maven wtyczki dla aplikacji sieci Web Azure] dokumentacji)</span><span class="sxs-lookup"><span data-stu-id="ef1d2-167">(A full list of environments is available in the [Maven Plugin for Azure Web Apps] documentation)</span></span>

1. <span data-ttu-id="ef1d2-168">Zapisz i Zamknij *settings.xml* pliku.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-168">Save and close the *settings.xml* file.</span></span>

## <a name="build-your-docker-container-image-and-push-it-to-your-azure-container-registry"></a><span data-ttu-id="ef1d2-169">Tworzenie obrazu kontenera programu Docker i wypchnąć go do rejestru kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ef1d2-169">Build your Docker container image and push it to your Azure container registry</span></span>

1. <span data-ttu-id="ef1d2-170">Przejdź do katalogu projektu zakończone aplikacji Spring rozruchu, (np. "*C:\SpringBoot\gs-spring-boot-docker\complete*"lub"*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), a następnie otwórz *pom.xml* plik tekstowy Edytor.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-170">Navigate to the completed project directory for your Spring Boot application, (e.g. "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="ef1d2-171">Aktualizacja `<properties>` kolekcji w *pom.xml* pliku z wartością serwera logowania do rejestru kontenera Azure opisanych w poprzedniej części tego samouczka; na przykład:</span><span class="sxs-lookup"><span data-stu-id="ef1d2-171">Update the `<properties>` collection in the *pom.xml* file with the login server value for your Azure Container Registry from the previous section of this tutorial; for example:</span></span>

   ```xml
   <properties>
      <azure.containerRegistry>wingtiptoysregistry</azure.containerRegistry>
      <docker.image.prefix>${azure.containerRegistry}.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
      <maven.build.timestamp.format>yyyyMMddHHmmssSSS</maven.build.timestamp.format>
   </properties>
   ```
   <span data-ttu-id="ef1d2-172">Gdzie:</span><span class="sxs-lookup"><span data-stu-id="ef1d2-172">Where:</span></span>
   <span data-ttu-id="ef1d2-173">Element</span><span class="sxs-lookup"><span data-stu-id="ef1d2-173">Element</span></span> | <span data-ttu-id="ef1d2-174">Opis</span><span class="sxs-lookup"><span data-stu-id="ef1d2-174">Description</span></span>
   ---|---|---
   `<azure.containerRegistry>` | <span data-ttu-id="ef1d2-175">Określa nazwę rejestru prywatnej kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-175">Specifies the name of your private Azure container registry.</span></span>
   `<docker.image.prefix>` | <span data-ttu-id="ef1d2-176">Określa adres URL rejestru prywatnej kontenera platformy Azure, w którym jest uzyskiwany w wyniku dołączania ". azurecr.io" do nazwy rejestru Kontener prywatny.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-176">Specifies the URL of your private Azure container registry, which is derived by appending ".azurecr.io" to the name of your private container registry.</span></span>

1. <span data-ttu-id="ef1d2-177">Sprawdź, czy `<plugin>` dla wtyczki Docker w Twojej *pom.xml* plik zawiera prawidłowe właściwości logowania adres i rejestru nazwy serwera z poprzedniego kroku, w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-177">Verify that `<plugin>` for the Docker plugin in your *pom.xml* file contains the correct properties for the login server address and registry name from the previous step in this tutorial.</span></span> <span data-ttu-id="ef1d2-178">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="ef1d2-178">For example:</span></span>

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <registryUrl>https://${docker.image.prefix}</registryUrl>
         <serverId>${azure.containerRegistry}</serverId>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```
   <span data-ttu-id="ef1d2-179">Gdzie:</span><span class="sxs-lookup"><span data-stu-id="ef1d2-179">Where:</span></span>
   <span data-ttu-id="ef1d2-180">Element</span><span class="sxs-lookup"><span data-stu-id="ef1d2-180">Element</span></span> | <span data-ttu-id="ef1d2-181">Opis</span><span class="sxs-lookup"><span data-stu-id="ef1d2-181">Description</span></span>
   ---|---|---
   `<serverId>` | <span data-ttu-id="ef1d2-182">Określa właściwość, która zawiera nazwę rejestru prywatnej kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-182">Specifies the property which contains name of your private Azure container registry.</span></span>
   `<registryUrl>` | <span data-ttu-id="ef1d2-183">Określa właściwość, która zawiera adres URL rejestru prywatnej kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-183">Specifies the property which contains the URL of your private Azure container registry.</span></span>

1. <span data-ttu-id="ef1d2-184">Przejdź do katalogu projektu zakończone aplikacji Spring rozruchu i uruchom następujące polecenie, aby ponownie skompilować aplikację i push kontenera do rejestru kontenera platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="ef1d2-184">Navigate to the completed project directory for your Spring Boot application and run the following command to rebuild the application and push the container to your Azure container registry:</span></span>

   ```
   mvn package docker:build -DpushImage 
   ```

1. <span data-ttu-id="ef1d2-185">OPCJONALNIE: Przejdź do [portalu Azure] i sprawdź, czy jest obraz kontenera Docker o nazwie **gs-spring — rozruchu — docker** w rejestrze kontenera.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-185">OPTIONAL: Browse to the [Azure portal] and verify that there is Docker container image named **gs-spring-boot-docker** in your container registry.</span></span>

   ![Sprawdź kontenera w portalu Azure][CR01]

## <a name="customize-your-pomxml-then-build-and-deploy-your-container-to-azure"></a><span data-ttu-id="ef1d2-187">Dostosowywanie programu pom.xml, a następnie tworzenie i wdrażanie z kontenera na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="ef1d2-187">Customize your pom.xml, then build and deploy your container to Azure</span></span>

<span data-ttu-id="ef1d2-188">Otwórz `pom.xml` pliku aplikacji Spring rozruchu w edytorze tekstu, a następnie zlokalizuj `<plugin>` elementu `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-188">Open the `pom.xml` file for your Spring Boot application in a text editor, and then locate the `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="ef1d2-189">Ten element powinien wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="ef1d2-189">This element should resemble the following example:</span></span>

   ```xml
   <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <version>0.1.3</version>
      <configuration>
         <authentication>
            <serverId>azure-auth</serverId>
         </authentication>
         <resourceGroup>wingtiptoysresources</resourceGroup>
         <appName>maven-linux-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <containerSettings>
            <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
            <registryUrl>https://${docker.image.prefix}</registryUrl>
            <serverId>${azure.containerRegistry}</serverId>
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

<span data-ttu-id="ef1d2-190">Istnieje kilka wartości, które można modyfikować dla wtyczki Maven i szczegółowy opis każdego z tych elementów jest dostępna w [Maven wtyczki dla aplikacji sieci Web Azure] dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-190">There are several values that you can modify for the Maven plugin, and a detailed description for each of these elements is available in the [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="ef1d2-191">Który trwa wspomniano, istnieje kilka wartości, które warto wyróżnianie w tym artykule:</span><span class="sxs-lookup"><span data-stu-id="ef1d2-191">That being said, there are several values that are worth highlighting in this article:</span></span>

<span data-ttu-id="ef1d2-192">Element</span><span class="sxs-lookup"><span data-stu-id="ef1d2-192">Element</span></span> | <span data-ttu-id="ef1d2-193">Opis</span><span class="sxs-lookup"><span data-stu-id="ef1d2-193">Description</span></span>
---|---|---
`<version>` | <span data-ttu-id="ef1d2-194">Określa wersję [Maven wtyczki dla aplikacji sieci Web Azure].</span><span class="sxs-lookup"><span data-stu-id="ef1d2-194">Specifies the version of the [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="ef1d2-195">Należy sprawdzić wersji na liście [Maven centralnym repozytorium](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) aby upewnić się, że używasz najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-195">You should check the version listed in the [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) to ensure that you are using the latest version.</span></span>
`<authentication>` | <span data-ttu-id="ef1d2-196">Określa informacje dotyczące uwierzytelniania dla platformy Azure, który w tym przykładzie zawiera `<serverId>` element, który zawiera `azure-auth`; Maven używa tej wartości do wyszukania nazwy głównej usługi Azure wartości w Twojej Maven *settings.xml* pliku, który został zdefiniowany w wcześniejszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-196">Specifies the authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value to look up the Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span>
`<resourceGroup>` | <span data-ttu-id="ef1d2-197">Określa, docelowa grupa zasobów, która jest `wingtiptoysresources` w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-197">Specifies the target resource group, which is `wingtiptoysresources` in this example.</span></span> <span data-ttu-id="ef1d2-198">Nazwa grupy zasobów zostanie utworzony podczas wdrażania, jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-198">The resource group will be created during deployment if it does not already exist.</span></span>
`<appName>` | <span data-ttu-id="ef1d2-199">Określa docelową nazwę dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-199">Specifies the target name for your web app.</span></span> <span data-ttu-id="ef1d2-200">W tym przykładzie nazwa docelowa jest `maven-linux-app-${maven.build.timestamp}`, gdzie `${maven.build.timestamp}` jest do niej dołączany sufiks w tym przykładzie, aby uniknąć konfliktu.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-200">In this example, the target name is `maven-linux-app-${maven.build.timestamp}`, where the `${maven.build.timestamp}` suffix is appended in this example to avoid conflict.</span></span> <span data-ttu-id="ef1d2-201">(Sygnatura czasowa jest opcjonalny; można określić dowolny unikatowy ciąg dla nazwy aplikacji).</span><span class="sxs-lookup"><span data-stu-id="ef1d2-201">(The timestamp is optional; you can specify any unique string for the app name.)</span></span>
`<region>` | <span data-ttu-id="ef1d2-202">Określa region docelowy, który w tym przykładzie jest `westus`.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-202">Specifies the target region, which in this example is `westus`.</span></span> <span data-ttu-id="ef1d2-203">(Pełna lista jest w [Maven wtyczki dla aplikacji sieci Web Azure] dokumentacji.)</span><span class="sxs-lookup"><span data-stu-id="ef1d2-203">(A full list is in the [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<containerSettings>` | <span data-ttu-id="ef1d2-204">Określa właściwości, które zawierają nazwę i adres URL z kontenera.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-204">Specifies the properties which contain the name and URL of your container.</span></span>
`<appSettings>` | <span data-ttu-id="ef1d2-205">Określa unikatowy ustawienia Maven do użycia podczas wdrażania aplikacji sieci web na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-205">Specifies any unique settings for Maven to use when deploying your web app to Azure.</span></span> <span data-ttu-id="ef1d2-206">W tym przykładzie `<property>` element zawiera pary nazwa/wartość elementów podrzędnych, które określić port dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-206">In this example, a `<property>` element contains a name/value pair of child elements that specify the port for your app.</span></span>

> [!NOTE]
>
> <span data-ttu-id="ef1d2-207">Ustawienia, aby zmienić numer portu w tym przykładzie jest konieczne tylko w przypadku, gdy zmieniasz portu domyślnego.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-207">The settings to change the port number in this example are only necessary when you are changing the port from the default.</span></span>
>

1. <span data-ttu-id="ef1d2-208">Z wiersza polecenia lub okno terminalu, które były wcześniej używane, skompiluj ponownie plik JAR za pomocą programu Maven Jeśli wprowadzono zmiany do *pom.xml* pliku; na przykład:</span><span class="sxs-lookup"><span data-stu-id="ef1d2-208">From the command prompt or terminal window that you were using earlier, rebuild the JAR file using Maven if you made any changes to the *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="ef1d2-209">Wdrażanie aplikacji sieci web na platformie Azure przy użyciu narzędzia Maven; na przykład:</span><span class="sxs-lookup"><span data-stu-id="ef1d2-209">Deploy your web app to Azure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="ef1d2-210">Maven zostanie wdrożona aplikacja sieci web na platformie Azure; Jeśli aplikacja sieci web nie istnieje, zostanie utworzona.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-210">Maven will deploy your web app to Azure; if the web app does not already exist, it will be created.</span></span>

> [!NOTE]
>
> <span data-ttu-id="ef1d2-211">Jeśli region, który jest określony w `<region>` elementu z *pom.xml* plik nie ma wystarczającej liczby serwerów, które są dostępne po uruchomieniu wdrożenia, można napotkać błąd podobny do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="ef1d2-211">If the region which you specify in the `<region>` element of your *pom.xml* file does not have enough servers available when you start your deployment, you might see an error similar to the following example:</span></span>
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
> <span data-ttu-id="ef1d2-212">W takim przypadku można określić innego regionu i uruchom ponownie polecenie narzędzia Maven, aby wdrożyć aplikację.</span><span class="sxs-lookup"><span data-stu-id="ef1d2-212">If this happens, you can specify another region and re-run the Maven command to deploy your application.</span></span>
>
>

<span data-ttu-id="ef1d2-213">Po wdrożeniu sieci web będzie można zarządzać nim za pomocą [portalu Azure].</span><span class="sxs-lookup"><span data-stu-id="ef1d2-213">When your web has been deployed, you will be able to manage it by using the [Azure portal].</span></span>

* <span data-ttu-id="ef1d2-214">Aplikacja sieci web zostaną wyświetlone w **usługi aplikacji**:</span><span class="sxs-lookup"><span data-stu-id="ef1d2-214">Your web app will be listed in **App Services**:</span></span>

   ![Aplikacja sieci Web wyświetlane w portalu Azure usługi aplikacji][AP01]

* <span data-ttu-id="ef1d2-216">I adres URL aplikacji sieci web zostaną wyświetlone w **omówienie** dla aplikacji sieci web:</span><span class="sxs-lookup"><span data-stu-id="ef1d2-216">And the URL for your web app will be listed in the **Overview** for your web app:</span></span>

   ![Określanie adresu URL dla aplikacji sieci web][AP02]

## <a name="next-steps"></a><span data-ttu-id="ef1d2-218">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ef1d2-218">Next steps</span></span>

<span data-ttu-id="ef1d2-219">Aby uzyskać więcej informacji na temat różne technologie omówione w tym artykule zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="ef1d2-219">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* <span data-ttu-id="ef1d2-220">[Maven wtyczki dla aplikacji sieci Web Azure]</span><span class="sxs-lookup"><span data-stu-id="ef1d2-220">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="ef1d2-221">Logowanie do platformy Azure z interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ef1d2-221">Log in to Azure from the Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="ef1d2-222">Tworzenie nazwy głównej usługi platformy Azure z 2.0 interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ef1d2-222">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="ef1d2-223">Informacje o ustawieniach maven</span><span class="sxs-lookup"><span data-stu-id="ef1d2-223">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

* <span data-ttu-id="ef1d2-224">[Dodatek docker przypadku Maven]</span><span class="sxs-lookup"><span data-stu-id="ef1d2-224">[Docker plugin for Maven]</span></span>

<!-- URL List -->

<span data-ttu-id="ef1d2-225">[Azure interfejsu wiersza polecenia (CLI)]: /cli/azure/overview</span><span class="sxs-lookup"><span data-stu-id="ef1d2-225">[Azure Command-Line Interface (CLI)]: /cli/azure/overview</span></span>
[Azure Container Service (ACS)]: https://azure.microsoft.com/services/container-service/
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
<span data-ttu-id="ef1d2-226">[portalu Azure]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="ef1d2-226">[Azure portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="ef1d2-227">[Maven wtyczki dla aplikacji sieci Web Azure]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin</span><span class="sxs-lookup"><span data-stu-id="ef1d2-227">[Maven Plugin for Azure Web Apps]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin</span></span>
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
<span data-ttu-id="ef1d2-228">[Docker]: https://www.docker.com/</span><span class="sxs-lookup"><span data-stu-id="ef1d2-228">[Docker]: https://www.docker.com/</span></span>
<span data-ttu-id="ef1d2-229">[Dodatek docker przypadku Maven]: https://github.com/spotify/docker-maven-plugin</span><span class="sxs-lookup"><span data-stu-id="ef1d2-229">[Docker plugin for Maven]: https://github.com/spotify/docker-maven-plugin</span></span>
<span data-ttu-id="ef1d2-230">[bezpłatne konto platformy Azure]: https://azure.microsoft.com/pricing/free-trial/</span><span class="sxs-lookup"><span data-stu-id="ef1d2-230">[free Azure account]: https://azure.microsoft.com/pricing/free-trial/</span></span>
<span data-ttu-id="ef1d2-231">[Git]: https://github.com/</span><span class="sxs-lookup"><span data-stu-id="ef1d2-231">[Git]: https://github.com/</span></span>
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
<span data-ttu-id="ef1d2-232">[Maven]: http://maven.apache.org/</span><span class="sxs-lookup"><span data-stu-id="ef1d2-232">[Maven]: http://maven.apache.org/</span></span>
<span data-ttu-id="ef1d2-233">[korzyści dla subskrybentów MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span><span class="sxs-lookup"><span data-stu-id="ef1d2-233">[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span></span>
<span data-ttu-id="ef1d2-234">[rozruchu Spring]: http://projects.spring.io/spring-boot/</span><span class="sxs-lookup"><span data-stu-id="ef1d2-234">[Spring Boot]: http://projects.spring.io/spring-boot/</span></span>
<span data-ttu-id="ef1d2-235">[rozruchu Spring na wprowadzenie Docker]: https://github.com/spring-guides/gs-spring-boot-docker</span><span class="sxs-lookup"><span data-stu-id="ef1d2-235">[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker</span></span>
<span data-ttu-id="ef1d2-236">[Spring Framework]: https://spring.io/</span><span class="sxs-lookup"><span data-stu-id="ef1d2-236">[Spring Framework]: https://spring.io/</span></span>

<!-- IMG List -->

[SB01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/SB01.png
[CR01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/CR01.png
[AP01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/AP02.png
