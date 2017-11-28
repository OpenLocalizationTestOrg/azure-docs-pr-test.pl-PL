---
title: Witaj toouse aaaHow Maven wtyczki dla aplikacji sieci Web Azure toodeploy w aplikacji Spring rozruchu w tooAzure rejestru kontenera Azure App Service
description: "Ten samouczek przeprowadzi Cię jednak hello kroki toodeploy aplikacja Spring rozruchu w tooAzure tooAzure rejestru kontenera Azure App Service przy użyciu wtyczki Maven."
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
ms.openlocfilehash: 55b95e310c9ee186a6d77d941c5a620c2e259d8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-spring-boot-app-in-azure-container-registry-tooazure-app-service"></a><span data-ttu-id="cbaf4-103">Jak toouse hello Maven wtyczki dla aplikacji sieci Web Azure toodeploy w aplikacji Spring rozruchu w tooAzure rejestru kontenera Azure App Service</span><span class="sxs-lookup"><span data-stu-id="cbaf4-103">How toouse hello Maven Plugin for Azure Web Apps toodeploy a Spring Boot app in Azure Container Registry tooAzure App Service</span></span>

<span data-ttu-id="cbaf4-104">Witaj  **[Spring Framework]**  popularnych struktura open source, który pomaga Java deweloperom tworzenie aplikacji interfejsu API, mobilne i sieci web.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-104">hello **[Spring Framework]** is a popular open-source framework that helps Java developers create web, mobile, and API applications.</span></span> <span data-ttu-id="cbaf4-105">W tym samouczku używana przykładowej aplikacji utworzony za pomocą [rozruchu Spring], podejście oparte na Konwencji poświęcone Spring tooget szybko rozpocząć pracę.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-105">This tutorial uses a sample app created using [Spring Boot], a convention-driven approach for using Spring tooget started quickly.</span></span>

<span data-ttu-id="cbaf4-106">W tym artykule przedstawiono sposób toodeploy próbki tooAzure aplikacji rozruchu Spring kontenera rejestru, a następnie użyć hello Maven wtyczki dla toodeploy Azure Web Apps tooAzure Twojej aplikacji usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-106">This article demonstrates how toodeploy a sample Spring Boot application tooAzure Container Registry, and then use hello Maven Plugin for Azure Web Apps toodeploy your application tooAzure App Service.</span></span>

> [!NOTE]
>
> <span data-ttu-id="cbaf4-107">Witaj Maven wtyczki dla aplikacji sieci Web platformy Azure jest obecnie dostępna jako podgląd.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-107">hello Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="cbaf4-108">Obecnie jest obsługiwana tylko publikacji FTP, chociaż hello przyszłości planowane dodatkowe funkcje.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-108">For now, only FTP publishing is supported, although additional features are planned for hello future.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="cbaf4-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="cbaf4-109">Prerequisites</span></span>

<span data-ttu-id="cbaf4-110">Kolejność toocomplete hello kroki w tym samouczku potrzebne hello toohave następujące wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="cbaf4-110">In order toocomplete hello steps in this tutorial, you need toohave hello following prerequisites:</span></span>

* <span data-ttu-id="cbaf4-111">Subskrypcja platformy Azure; Jeśli nie masz jeszcze subskrypcji platformy Azure, możesz przeprowadzić aktywację Twojej [korzyści dla subskrybentów MSDN] lub zarejestrować się w celu [bezpłatne konto platformy Azure].</span><span class="sxs-lookup"><span data-stu-id="cbaf4-111">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="cbaf4-112">Witaj [Azure interfejsu wiersza polecenia (CLI)].</span><span class="sxs-lookup"><span data-stu-id="cbaf4-112">hello [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="cbaf4-113">Aktualne [Java Development Kit (JDK)], wersja 1.7 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-113">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="cbaf4-114">Apache na [Maven] (w wersji 3) Narzędzie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-114">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="cbaf4-115">A [Git] klienta.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-115">A [Git] client.</span></span>
* <span data-ttu-id="cbaf4-116">A [Docker] klienta.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-116">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="cbaf4-117">Ze względu na wymagania dotyczące wirtualizacji toohello tego samouczka nie można wykonać hello opisanych w tym artykule na maszynie wirtualnej; należy użyć komputera fizycznego z włączonymi funkcjami wirtualizacji.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-117">Due toohello virtualization requirements of this tutorial, you cannot follow hello steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="clone-hello-sample-spring-boot-on-docker-web-app"></a><span data-ttu-id="cbaf4-118">Klonowanie hello przykładu rozruchu Spring Docker aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="cbaf4-118">Clone hello sample Spring Boot on Docker web app</span></span>

<span data-ttu-id="cbaf4-119">W tej sekcji sklonować konteneryzowanych aplikacji rozruchu Spring i przetestować go lokalnie.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-119">In this section, you clone a containerized Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="cbaf4-120">Otwórz wiersz polecenia lub okno terminalu i utworzyć toohold lokalnego katalogu aplikacji Spring rozruchu i zmień katalog toothat; na przykład:</span><span class="sxs-lookup"><span data-stu-id="cbaf4-120">Open a command prompt or terminal window and create a local directory toohold your Spring Boot application, and change toothat directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="cbaf4-121">--lub--</span><span class="sxs-lookup"><span data-stu-id="cbaf4-121">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="cbaf4-122">Witaj w klonowania [rozruchu Spring na wprowadzenie Docker] przykładowy projekt do katalogu hello utworzony; na przykład:</span><span class="sxs-lookup"><span data-stu-id="cbaf4-122">Clone hello [Spring Boot on Docker Getting Started] sample project into hello directory you created; for example:</span></span>
   ```shell
   git clone -b private-registry https://github.com/Microsoft/gs-spring-boot-docker
   ```

1. <span data-ttu-id="cbaf4-123">Zmień katalog projektu toohello ukończone; na przykład:</span><span class="sxs-lookup"><span data-stu-id="cbaf4-123">Change directory toohello completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="cbaf4-124">Kompiluj plik JAR hello za pomocą programu Maven; na przykład:</span><span class="sxs-lookup"><span data-stu-id="cbaf4-124">Build hello JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="cbaf4-125">Podczas tworzenia aplikacji sieci web hello uruchomić aplikacji sieci web hello za pomocą programu Maven; na przykład:</span><span class="sxs-lookup"><span data-stu-id="cbaf4-125">When hello web app has been created, start hello web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="cbaf4-126">Testowanie aplikacji sieci web hello przechodząc tooit lokalnie za pomocą przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-126">Test hello web app by browsing tooit locally using a web browser.</span></span> <span data-ttu-id="cbaf4-127">Na przykład można użyć hello następujące polecenie, jeśli masz curl dostępne:</span><span class="sxs-lookup"><span data-stu-id="cbaf4-127">For example, you could use hello following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="cbaf4-128">Powinien zostać wyświetlony komunikat wyświetlany po hello: **Hello Docker World**</span><span class="sxs-lookup"><span data-stu-id="cbaf4-128">You should see hello following message displayed: **Hello Docker World**</span></span>

   ![Przejdź do przykładowej aplikacji lokalnie][SB01]

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="cbaf4-130">Tworzenie nazwy głównej usługi platformy Azure</span><span class="sxs-lookup"><span data-stu-id="cbaf4-130">Create an Azure service principal</span></span>

<span data-ttu-id="cbaf4-131">W tej sekcji utworzysz Azure nazwy głównej usługi, która hello używa wtyczki Maven, wdrażając tooAzure Twojego kontenera.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-131">In this section, you create an Azure service principal that hello Maven plugin uses when deploying your container tooAzure.</span></span>

1. <span data-ttu-id="cbaf4-132">Otwórz wiersz polecenia.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-132">Open a command prompt.</span></span>

1. <span data-ttu-id="cbaf4-133">Zaloguj się do konta platformy Azure przy użyciu hello wiersza polecenia platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="cbaf4-133">Sign into your Azure account by using hello Azure CLI:</span></span>
   ```azurecli
   az login
   ```
   <span data-ttu-id="cbaf4-134">Wykonaj hello instrukcje toocomplete hello procesu logowania.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-134">Follow hello instructions toocomplete hello sign-in process.</span></span>

1. <span data-ttu-id="cbaf4-135">Tworzenie nazwy głównej usługi platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="cbaf4-135">Create an Azure service principal:</span></span>
   ```azurecli
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="cbaf4-136">Gdzie `uuuuuuuu` jest nazwą użytkownika hello i `pppppppp` jest hello hasło dla nazwy głównej usługi hello.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-136">Where `uuuuuuuu` is hello user name and `pppppppp` is hello password for hello service principal.</span></span>

1. <span data-ttu-id="cbaf4-137">Azure odpowiada JSON podobny hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="cbaf4-137">Azure responds with JSON that resembles hello following example:</span></span>
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
   > <span data-ttu-id="cbaf4-138">Po skonfigurowaniu hello Maven wtyczki toodeploy Twojego tooAzure kontenera Użyj wartości hello z odpowiedź w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-138">You will use hello values from this JSON response when you configure hello Maven plugin toodeploy your container tooAzure.</span></span> <span data-ttu-id="cbaf4-139">Hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, i `tttttttt` są symbole zastępcze, które są używane w tej toomake przykład go łatwiejsze toomap tych wartości tootheir odpowiednich elementów podczas konfigurowania programu Maven `settings.xml` w hello obok pliku sekcja.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-139">hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example toomake it easier toomap these values tootheir respective elements when you configure your Maven `settings.xml` file in hello next section.</span></span>
   >
   >

## <a name="create-an-azure-container-registry-using-hello-azure-cli"></a><span data-ttu-id="cbaf4-140">Tworzenie przy użyciu interfejsu wiersza polecenia Azure hello rejestru kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="cbaf4-140">Create an Azure Container Registry using hello Azure CLI</span></span>

1. <span data-ttu-id="cbaf4-141">Otwórz wiersz polecenia.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-141">Open a command prompt.</span></span>

1. <span data-ttu-id="cbaf4-142">Zaloguj się tooyour konto platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="cbaf4-142">Log in tooyour Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="cbaf4-143">Utwórz grupę zasobów dla hello zasobów platformy Azure, które będą używane w tym artykule:</span><span class="sxs-lookup"><span data-stu-id="cbaf4-143">Create a resource group for hello Azure resources you will use in this article:</span></span>
   ```azurecli
   az group create --name=wingtiptoysresources --location=westus
   ```
   <span data-ttu-id="cbaf4-144">Zastąp `wingtiptoysresources` w tym przykładzie z unikatową nazwę grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-144">Replace `wingtiptoysresources` in this example with a unique name for your resource group.</span></span>

1. <span data-ttu-id="cbaf4-145">Utwórz rejestru prywatnej kontenera platformy Azure w grupie zasobów hello aplikacji Spring rozruchu:</span><span class="sxs-lookup"><span data-stu-id="cbaf4-145">Create a private Azure container registry in hello resource group for your Spring Boot app:</span></span> 
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoysresources --location westus --name wingtiptoysregistry --sku Basic
   ```
   <span data-ttu-id="cbaf4-146">Zastąp `wingtiptoysregistry` w tym przykładzie z unikatową nazwę rejestru kontenera.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-146">Replace `wingtiptoysregistry` in this example with a unique name for your container registry.</span></span>

1. <span data-ttu-id="cbaf4-147">Pobrać hasło hello rejestru kontenera:</span><span class="sxs-lookup"><span data-stu-id="cbaf4-147">Retrieve hello password for your container registry:</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```
   <span data-ttu-id="cbaf4-148">Azure będzie odpowiadać przy użyciu hasła; na przykład:</span><span class="sxs-lookup"><span data-stu-id="cbaf4-148">Azure will respond with your password; for example:</span></span>
   ```json
   {
      "name": "password",
      "value": "xxxxxxxxxx"
   }
   ```

## <a name="add-your-azure-container-registry-and-azure-service-principal-tooyour-maven-settings"></a><span data-ttu-id="cbaf4-149">Dodaj rejestru kontenera platformy Azure i ustawienia Maven tooyour główną usługi Azure</span><span class="sxs-lookup"><span data-stu-id="cbaf4-149">Add your Azure container registry and Azure service principal tooyour Maven settings</span></span>

1. <span data-ttu-id="cbaf4-150">Otwieranie programu Maven `settings.xml` plik w edytorze tekstów; ten plik może być w ścieżce, takie jak hello następujące przykłady:</span><span class="sxs-lookup"><span data-stu-id="cbaf4-150">Open your Maven `settings.xml` file in a text editor; this file might be in a path like hello following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="cbaf4-151">Dodawanie ustawień dostępu do rejestru kontenera platformy Azure z poprzedniej sekcji tego artykułu toohello hello `<servers>` kolekcji w hello *settings.xml* pliku; na przykład:</span><span class="sxs-lookup"><span data-stu-id="cbaf4-151">Add your Azure Container Registry access settings from hello previous section of this article toohello `<servers>` collection in hello *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>xxxxxxxxxx</password>
      </server>
   </servers>
   ```
   <span data-ttu-id="cbaf4-152">Gdzie:</span><span class="sxs-lookup"><span data-stu-id="cbaf4-152">Where:</span></span>
   <span data-ttu-id="cbaf4-153">Element</span><span class="sxs-lookup"><span data-stu-id="cbaf4-153">Element</span></span> | <span data-ttu-id="cbaf4-154">Opis</span><span class="sxs-lookup"><span data-stu-id="cbaf4-154">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="cbaf4-155">Zawiera nazwę hello rejestru prywatnej kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-155">Contains hello name of your private Azure container registry.</span></span>
   `<username>` | <span data-ttu-id="cbaf4-156">Zawiera nazwę hello rejestru prywatnej kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-156">Contains hello name of your private Azure container registry.</span></span>
   `<password>` | <span data-ttu-id="cbaf4-157">Zawiera hasło hello pobrany w poprzedniej sekcji hello tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-157">Contains hello password you retrieved in hello previous section of this article.</span></span>

1. <span data-ttu-id="cbaf4-158">Dodaj ustawienia podmiotu zabezpieczeń usługi Azure z wcześniejszej części tego artykułu toohello `<servers>` kolekcji w hello *settings.xml* pliku; na przykład:</span><span class="sxs-lookup"><span data-stu-id="cbaf4-158">Add your Azure service principal settings from an earlier section of this article toohello `<servers>` collection in hello *settings.xml* file; for example:</span></span>

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
   <span data-ttu-id="cbaf4-159">Gdzie:</span><span class="sxs-lookup"><span data-stu-id="cbaf4-159">Where:</span></span>
   <span data-ttu-id="cbaf4-160">Element</span><span class="sxs-lookup"><span data-stu-id="cbaf4-160">Element</span></span> | <span data-ttu-id="cbaf4-161">Opis</span><span class="sxs-lookup"><span data-stu-id="cbaf4-161">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="cbaf4-162">Określa unikatową nazwę używający Maven toolook zapasową ustawień zabezpieczeń podczas wdrażania tooAzure aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-162">Specifies a unique name which Maven uses toolook up your security settings when you deploy your web app tooAzure.</span></span>
   `<client>` | <span data-ttu-id="cbaf4-163">Zawiera hello `appId` wartość z Twojej nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-163">Contains hello `appId` value from your service principal.</span></span>
   `<tenant>` | <span data-ttu-id="cbaf4-164">Zawiera hello `tenant` wartość z Twojej nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-164">Contains hello `tenant` value from your service principal.</span></span>
   `<key>` | <span data-ttu-id="cbaf4-165">Zawiera hello `password` wartość z Twojej nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-165">Contains hello `password` value from your service principal.</span></span>
   `<environment>` | <span data-ttu-id="cbaf4-166">Definiuje hello docelowej chmury Azure środowisko, które jest `AZURE` w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-166">Defines hello target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="cbaf4-167">(Pełna lista środowisk jest dostępna w hello [Maven wtyczki dla aplikacji sieci Web Azure] dokumentacji)</span><span class="sxs-lookup"><span data-stu-id="cbaf4-167">(A full list of environments is available in hello [Maven Plugin for Azure Web Apps] documentation)</span></span>

1. <span data-ttu-id="cbaf4-168">Zapisz i zamknij hello *settings.xml* pliku.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-168">Save and close hello *settings.xml* file.</span></span>

## <a name="build-your-docker-container-image-and-push-it-tooyour-azure-container-registry"></a><span data-ttu-id="cbaf4-169">Tworzenie obrazu kontenera programu Docker i wypchnąć go tooyour rejestru kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="cbaf4-169">Build your Docker container image and push it tooyour Azure container registry</span></span>

1. <span data-ttu-id="cbaf4-170">Przejdź toohello ukończone katalogu projektu aplikacji Spring rozruchu, (np. "*C:\SpringBoot\gs-spring-boot-docker\complete*"lub"*/users/robert/SpringBoot/gs-spring-boot-docker/complete*") i otwórz hello *pom.xml* pliku z Edytor tekstu.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-170">Navigate toohello completed project directory for your Spring Boot application, (e.g. "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open hello *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="cbaf4-171">Aktualizacja hello `<properties>` kolekcji w hello *pom.xml* pliku z wartością serwera logowania hello rejestru kontenera platformy Azure z poprzedniej sekcji hello tego samouczka; na przykład:</span><span class="sxs-lookup"><span data-stu-id="cbaf4-171">Update hello `<properties>` collection in hello *pom.xml* file with hello login server value for your Azure Container Registry from hello previous section of this tutorial; for example:</span></span>

   ```xml
   <properties>
      <azure.containerRegistry>wingtiptoysregistry</azure.containerRegistry>
      <docker.image.prefix>${azure.containerRegistry}.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
      <maven.build.timestamp.format>yyyyMMddHHmmssSSS</maven.build.timestamp.format>
   </properties>
   ```
   <span data-ttu-id="cbaf4-172">Gdzie:</span><span class="sxs-lookup"><span data-stu-id="cbaf4-172">Where:</span></span>
   <span data-ttu-id="cbaf4-173">Element</span><span class="sxs-lookup"><span data-stu-id="cbaf4-173">Element</span></span> | <span data-ttu-id="cbaf4-174">Opis</span><span class="sxs-lookup"><span data-stu-id="cbaf4-174">Description</span></span>
   ---|---|---
   `<azure.containerRegistry>` | <span data-ttu-id="cbaf4-175">Określa nazwę hello rejestru prywatnej kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-175">Specifies hello name of your private Azure container registry.</span></span>
   `<docker.image.prefix>` | <span data-ttu-id="cbaf4-176">Określa adres URL rejestru prywatnej kontenera platformy Azure, w którym jest uzyskiwany w wyniku dołączania hello ". azurecr.io" toohello nazwa rejestru Kontener prywatny.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-176">Specifies hello URL of your private Azure container registry, which is derived by appending ".azurecr.io" toohello name of your private container registry.</span></span>

1. <span data-ttu-id="cbaf4-177">Sprawdź, czy `<plugin>` hello Docker wtyczki w Twojej *pom.xml* plik zawiera prawidłowe właściwości hello powitania serwera adres i rejestru nazwy logowania z poprzedniego kroku hello w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-177">Verify that `<plugin>` for hello Docker plugin in your *pom.xml* file contains hello correct properties for hello login server address and registry name from hello previous step in this tutorial.</span></span> <span data-ttu-id="cbaf4-178">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="cbaf4-178">For example:</span></span>

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
   <span data-ttu-id="cbaf4-179">Gdzie:</span><span class="sxs-lookup"><span data-stu-id="cbaf4-179">Where:</span></span>
   <span data-ttu-id="cbaf4-180">Element</span><span class="sxs-lookup"><span data-stu-id="cbaf4-180">Element</span></span> | <span data-ttu-id="cbaf4-181">Opis</span><span class="sxs-lookup"><span data-stu-id="cbaf4-181">Description</span></span>
   ---|---|---
   `<serverId>` | <span data-ttu-id="cbaf4-182">Określa właściwość hello, która zawiera nazwę rejestru prywatnej kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-182">Specifies hello property which contains name of your private Azure container registry.</span></span>
   `<registryUrl>` | <span data-ttu-id="cbaf4-183">Określa właściwość hello, który zawiera adres URL hello rejestru prywatnej kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-183">Specifies hello property which contains hello URL of your private Azure container registry.</span></span>

1. <span data-ttu-id="cbaf4-184">Przejdź do katalogu projektu toohello ukończone aplikacji Spring rozruchu i uruchom następujące polecenie toorebuild hello aplikacji hello push hello kontenera tooyour rejestru kontenera platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="cbaf4-184">Navigate toohello completed project directory for your Spring Boot application and run hello following command toorebuild hello application and push hello container tooyour Azure container registry:</span></span>

   ```
   mvn package docker:build -DpushImage 
   ```

1. <span data-ttu-id="cbaf4-185">OPCJONALNIE: Przeglądaj toohello [portalu Azure] i sprawdź, czy jest obraz kontenera Docker o nazwie **gs-spring — rozruchu — docker** w rejestrze kontenera.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-185">OPTIONAL: Browse toohello [Azure portal] and verify that there is Docker container image named **gs-spring-boot-docker** in your container registry.</span></span>

   ![Sprawdź kontenera w portalu Azure][CR01]

## <a name="customize-your-pomxml-then-build-and-deploy-your-container-tooazure"></a><span data-ttu-id="cbaf4-187">Dostosowywanie programu pom.xml, a następnie Skompiluj i wdróż tooAzure Twojego kontenera</span><span class="sxs-lookup"><span data-stu-id="cbaf4-187">Customize your pom.xml, then build and deploy your container tooAzure</span></span>

<span data-ttu-id="cbaf4-188">Otwórz hello `pom.xml` pliku aplikacji Spring rozruchu w edytorze tekstu, a następnie zlokalizuj hello `<plugin>` elementu `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-188">Open hello `pom.xml` file for your Spring Boot application in a text editor, and then locate hello `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="cbaf4-189">Ten element powinien wyglądać hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="cbaf4-189">This element should resemble hello following example:</span></span>

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

<span data-ttu-id="cbaf4-190">Istnieje kilka wartości, które można modyfikować dla wtyczki Maven hello i szczegółowy opis każdego z tych elementów jest dostępna w hello [Maven wtyczki dla aplikacji sieci Web Azure] dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-190">There are several values that you can modify for hello Maven plugin, and a detailed description for each of these elements is available in hello [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="cbaf4-191">Który trwa wspomniano, istnieje kilka wartości, które warto wyróżnianie w tym artykule:</span><span class="sxs-lookup"><span data-stu-id="cbaf4-191">That being said, there are several values that are worth highlighting in this article:</span></span>

<span data-ttu-id="cbaf4-192">Element</span><span class="sxs-lookup"><span data-stu-id="cbaf4-192">Element</span></span> | <span data-ttu-id="cbaf4-193">Opis</span><span class="sxs-lookup"><span data-stu-id="cbaf4-193">Description</span></span>
---|---|---
`<version>` | <span data-ttu-id="cbaf4-194">Określa wersję hello hello [Maven wtyczki dla aplikacji sieci Web Azure].</span><span class="sxs-lookup"><span data-stu-id="cbaf4-194">Specifies hello version of hello [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="cbaf4-195">Należy sprawdzić wersji hello na liście hello [Maven centralnym repozytorium](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure, którego używasz hello najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-195">You should check hello version listed in hello [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure that you are using hello latest version.</span></span>
`<authentication>` | <span data-ttu-id="cbaf4-196">Określa hello informacje dotyczące uwierzytelniania dla platformy Azure, który w tym przykładzie zawiera `<serverId>` element, który zawiera `azure-auth`; Maven używa tej wartości toolook wartości podmiotu zabezpieczeń usługi Azure hello programu Maven *settings.xml* pliku, który został zdefiniowany w wcześniejszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-196">Specifies hello authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value toolook up hello Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span>
`<resourceGroup>` | <span data-ttu-id="cbaf4-197">Określa, docelowa grupa zasobów hello, który jest `wingtiptoysresources` w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-197">Specifies hello target resource group, which is `wingtiptoysresources` in this example.</span></span> <span data-ttu-id="cbaf4-198">Grupa zasobów Hello zostanie utworzony podczas wdrażania, jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-198">hello resource group will be created during deployment if it does not already exist.</span></span>
`<appName>` | <span data-ttu-id="cbaf4-199">Określa nazwę docelowej hello aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-199">Specifies hello target name for your web app.</span></span> <span data-ttu-id="cbaf4-200">W tym przykładzie nazwa docelowego hello jest `maven-linux-app-${maven.build.timestamp}`, gdzie hello `${maven.build.timestamp}` jest do niej dołączany sufiks w tej konflikt tooavoid przykład.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-200">In this example, hello target name is `maven-linux-app-${maven.build.timestamp}`, where hello `${maven.build.timestamp}` suffix is appended in this example tooavoid conflict.</span></span> <span data-ttu-id="cbaf4-201">(sygnatura czasowa hello jest opcjonalne; można określić dowolny unikatowy ciąg dla nazwy aplikacji hello).</span><span class="sxs-lookup"><span data-stu-id="cbaf4-201">(hello timestamp is optional; you can specify any unique string for hello app name.)</span></span>
`<region>` | <span data-ttu-id="cbaf4-202">Określa region docelowy hello, czyli w tym przykładzie `westus`.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-202">Specifies hello target region, which in this example is `westus`.</span></span> <span data-ttu-id="cbaf4-203">(Pełna lista jest w hello [Maven wtyczki dla aplikacji sieci Web Azure] dokumentacji.)</span><span class="sxs-lookup"><span data-stu-id="cbaf4-203">(A full list is in hello [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<containerSettings>` | <span data-ttu-id="cbaf4-204">Określa właściwości hello, które zawierają hello nazwy i adresu URL z kontenera.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-204">Specifies hello properties which contain hello name and URL of your container.</span></span>
`<appSettings>` | <span data-ttu-id="cbaf4-205">Określa unikatowy ustawienia Maven toouse, wdrażając tooAzure aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-205">Specifies any unique settings for Maven toouse when deploying your web app tooAzure.</span></span> <span data-ttu-id="cbaf4-206">W tym przykładzie `<property>` element zawiera pary nazwa/wartość elementów podrzędnych, określających hello portu dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-206">In this example, a `<property>` element contains a name/value pair of child elements that specify hello port for your app.</span></span>

> [!NOTE]
>
> <span data-ttu-id="cbaf4-207">numer portu Hello ustawienia toochange hello w tym przykładzie jest konieczne tylko w przypadku, gdy zmieniasz hello portów z domyślnej hello.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-207">hello settings toochange hello port number in this example are only necessary when you are changing hello port from hello default.</span></span>
>

1. <span data-ttu-id="cbaf4-208">Z wiersza polecenia hello lub okno terminalu, które były wcześniej używane odbudować plik JAR hello za pomocą programu Maven Jeśli wprowadzono żadnych zmian toohello *pom.xml* pliku; na przykład:</span><span class="sxs-lookup"><span data-stu-id="cbaf4-208">From hello command prompt or terminal window that you were using earlier, rebuild hello JAR file using Maven if you made any changes toohello *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="cbaf4-209">Wdrażanie tooAzure aplikacji sieci web przy użyciu narzędzia Maven; na przykład:</span><span class="sxs-lookup"><span data-stu-id="cbaf4-209">Deploy your web app tooAzure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="cbaf4-210">Maven wdroży tooAzure aplikacji sieci web; Jeśli aplikacja sieci web hello jeszcze nie istnieje, zostanie utworzona.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-210">Maven will deploy your web app tooAzure; if hello web app does not already exist, it will be created.</span></span>

> [!NOTE]
>
> <span data-ttu-id="cbaf4-211">Jeśli region hello, określany w hello `<region>` elementu z *pom.xml* plik nie ma wystarczającej liczby serwerów, które są dostępne po uruchomieniu wdrożenia, można napotkać błąd toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="cbaf4-211">If hello region which you specify in hello `<region>` element of your *pom.xml* file does not have enough servers available when you start your deployment, you might see an error similar toohello following example:</span></span>
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
> <span data-ttu-id="cbaf4-212">W takim przypadku można określić innego regionu i uruchom ponownie hello toodeploy polecenie narzędzia Maven aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cbaf4-212">If this happens, you can specify another region and re-run hello Maven command toodeploy your application.</span></span>
>
>

<span data-ttu-id="cbaf4-213">Po wdrożeniu sieci web będą mogli toomanage go za pomocą hello [portalu Azure].</span><span class="sxs-lookup"><span data-stu-id="cbaf4-213">When your web has been deployed, you will be able toomanage it by using hello [Azure portal].</span></span>

* <span data-ttu-id="cbaf4-214">Aplikacja sieci web zostaną wyświetlone w **usługi aplikacji**:</span><span class="sxs-lookup"><span data-stu-id="cbaf4-214">Your web app will be listed in **App Services**:</span></span>

   ![Aplikacja sieci Web wyświetlane w portalu Azure usługi aplikacji][AP01]

* <span data-ttu-id="cbaf4-216">I hello adres URL dla aplikacji sieci web zostaną wyświetlone w hello **omówienie** dla aplikacji sieci web:</span><span class="sxs-lookup"><span data-stu-id="cbaf4-216">And hello URL for your web app will be listed in hello **Overview** for your web app:</span></span>

   ![Określanie hello adres URL aplikacji sieci web][AP02]

## <a name="next-steps"></a><span data-ttu-id="cbaf4-218">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cbaf4-218">Next steps</span></span>

<span data-ttu-id="cbaf4-219">Aby uzyskać więcej informacji na temat hello różne technologie omówione w tym artykule, zobacz hello następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="cbaf4-219">For more information about hello various technologies discussed in this article, see hello following articles:</span></span>

* <span data-ttu-id="cbaf4-220">[Maven wtyczki dla aplikacji sieci Web Azure]</span><span class="sxs-lookup"><span data-stu-id="cbaf4-220">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="cbaf4-221">Zaloguj się za tooAzure z hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="cbaf4-221">Log in tooAzure from hello Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="cbaf4-222">Tworzenie nazwy głównej usługi platformy Azure z 2.0 interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="cbaf4-222">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="cbaf4-223">Informacje o ustawieniach maven</span><span class="sxs-lookup"><span data-stu-id="cbaf4-223">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

* <span data-ttu-id="cbaf4-224">[Dodatek docker przypadku Maven]</span><span class="sxs-lookup"><span data-stu-id="cbaf4-224">[Docker plugin for Maven]</span></span>

<!-- URL List -->

[Azure interfejsu wiersza polecenia (CLI)]: /cli/azure/overview
[Azure Container Service (ACS)]: https://azure.microsoft.com/services/container-service/
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[portalu Azure]: https://portal.azure.com/
[Maven wtyczki dla aplikacji sieci Web Azure]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin
[Create a private Docker container registry using hello Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[Dodatek docker przypadku Maven]: https://github.com/spotify/docker-maven-plugin
[bezpłatne konto platformy Azure]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[korzyści dla subskrybentów MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[rozruchu Spring]: http://projects.spring.io/spring-boot/
[rozruchu Spring na wprowadzenie Docker]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/SB01.png
[CR01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/CR01.png
[AP01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/AP02.png
