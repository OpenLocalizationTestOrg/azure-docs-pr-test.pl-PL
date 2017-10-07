---
title: "tooAzure aaaDeploy App Service przy użyciu wtyczki Wpięć | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse Wpięć usługi aplikacji Azure wtyczki toodeploy Java web app tooAzure w Wpięć"
services: app-service\web
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 7/24/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 080be7277555ce7d688dccdf38eef309e7a7b194
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-app-service-with-jenkins-plugin"></a><span data-ttu-id="8cdf5-103">Wdrażanie tooAzure aplikacji usługi z Wpięć wtyczki</span><span class="sxs-lookup"><span data-stu-id="8cdf5-103">Deploy tooAzure App Service with Jenkins plugin</span></span> 
<span data-ttu-id="8cdf5-104">toodeploy tooAzure aplikacji sieci web Java można użyć wiersza polecenia platformy Azure w [potoku Wpięć](/azure/jenkins/execute-cli-jenkins-pipeline) można też korzystać z hello [wtyczki Wpięć usługi aplikacji Azure](https://plugins.jenkins.io/azure-app-service).</span><span class="sxs-lookup"><span data-stu-id="8cdf5-104">toodeploy a Java web app tooAzure, you can use Azure CLI in [Jenkins Pipeline](/azure/jenkins/execute-cli-jenkins-pipeline) or you can make use of hello [Azure App Service Jenkins plugin](https://plugins.jenkins.io/azure-app-service).</span></span> <span data-ttu-id="8cdf5-105">Ten samouczek zawiera informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="8cdf5-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8cdf5-106">Skonfiguruj tooAzure toodeploy Wpięć usługi aplikacji za pośrednictwem FTP</span><span class="sxs-lookup"><span data-stu-id="8cdf5-106">Configure Jenkins toodeploy tooAzure App Service through FTP</span></span> 
> * <span data-ttu-id="8cdf5-107">Skonfiguruj tooAzure toodeploy Wpięć usługi aplikacji w systemie Linux przy użyciu rozwiązania Docker</span><span class="sxs-lookup"><span data-stu-id="8cdf5-107">Configure Jenkins toodeploy tooAzure App Service on Linux through Docker</span></span> 

## <a name="create-and-configure-jenkins-instance"></a><span data-ttu-id="8cdf5-108">Tworzenie i konfigurowanie Wpięć wystąpienia</span><span class="sxs-lookup"><span data-stu-id="8cdf5-108">Create and Configure Jenkins instance</span></span>
<span data-ttu-id="8cdf5-109">Jeśli nie masz już wzorca Wpięć, rozpoczynać hello [szablon rozwiązania](install-jenkins-solution-template.md), w tym JDK8 oraz hello następujące wymagane wtyczek:</span><span class="sxs-lookup"><span data-stu-id="8cdf5-109">If you do not already have a Jenkins master, start with hello [Solution Template](install-jenkins-solution-template.md), which includes JDK8 and hello following required plugins:</span></span>

* <span data-ttu-id="8cdf5-110">[Dodatek klienta Git Wpięć](https://plugins.jenkins.io/git-client) v.2.4.6</span><span class="sxs-lookup"><span data-stu-id="8cdf5-110">[Jenkins Git client plugin](https://plugins.jenkins.io/git-client) v.2.4.6</span></span> 
* <span data-ttu-id="8cdf5-111">[Dodatek docker Commons](https://plugins.jenkins.io/docker-commons) v.1.4.0</span><span class="sxs-lookup"><span data-stu-id="8cdf5-111">[Docker Commons Plugin](https://plugins.jenkins.io/docker-commons) v.1.4.0</span></span>
* <span data-ttu-id="8cdf5-112">[Poświadczenia Azure](https://plugins.jenkins.io/azure-credentials) v.1.2</span><span class="sxs-lookup"><span data-stu-id="8cdf5-112">[Azure Credentials](https://plugins.jenkins.io/azure-credentials) v.1.2</span></span>
* <span data-ttu-id="8cdf5-113">[Usługa aplikacji Azure](https://plugins.jenkins.io/azure-app-server) v.0.1</span><span class="sxs-lookup"><span data-stu-id="8cdf5-113">[Azure App Service](https://plugins.jenkins.io/azure-app-server) v.0.1</span></span>

<span data-ttu-id="8cdf5-114">Możesz użyć hello usługi aplikacji wtyczki toodeploy aplikacji sieci Web we wszystkich językach (na przykład C#, PHP, Java i node.js itp.) obsługiwanych przez usługę Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-114">You can use hello App Service plugin toodeploy Web App in all languages (for instance, C#, PHP, Java, and node.js etc.) supported by Azure App Service.</span></span> <span data-ttu-id="8cdf5-115">W tym samouczku używamy hello przykładowej aplikacji Java, [prostej aplikacji sieci Web Java na platformie Azure](https://github.com/azure-devops/javawebappsample).</span><span class="sxs-lookup"><span data-stu-id="8cdf5-115">In this tutorial, we are using hello sample Java app, [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample).</span></span> <span data-ttu-id="8cdf5-116">toofork hello repozytorium tooyour własne konto GitHub, kliknij przycisk hello **rozwidlenia** przycisk w prawym górnym rogu hello.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-116">toofork hello repo tooyour own GitHub account, click hello **Fork** button in hello top right-hand corner.</span></span>  

<span data-ttu-id="8cdf5-117">Wymagane do tworzenia projektu języka Java hello są Java JDK i Maven.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-117">Java JDK and Maven are required for building hello Java project.</span></span> <span data-ttu-id="8cdf5-118">Sprawdź, czy zainstalować składniki hello w głównym Wpięć hello lub hello agenta maszyny Wirtualnej, jeśli używany jest jeden dla ciągłej integracji.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-118">Make sure you install hello components in hello Jenkins master or hello VM agent if you use one for continuous integration.</span></span> 

<span data-ttu-id="8cdf5-119">tooinstall, zaloguj się przy użyciu protokołu SSH wystąpienia Wpięć toohello i uruchom następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="8cdf5-119">tooinstall, log in toohello Jenkins instance using SSH and run hello following commands:</span></span>

```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

<span data-ttu-id="8cdf5-120">Podczas wdrażania usługi w systemie Linux tooApp, konieczne są również tooinstall Docker wzorca Wpięć hello lub agenta maszyny Wirtualnej hello używany dla kompilacji.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-120">For deploying tooApp Service on Linux, you also need tooinstall Docker on hello Jenkins master or hello VM agent used for build.</span></span> <span data-ttu-id="8cdf5-121">Zobacz toothis artykułu tooinstall Docker: https://docs.docker.com/engine/installation/linux/ubuntu/.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-121">Refer toothis article tooinstall Docker: https://docs.docker.com/engine/installation/linux/ubuntu/.</span></span>

## <a name="add-azure-service-principal-toojenkins-credential"></a><span data-ttu-id="8cdf5-122">Dodaj poświadczenie tooJenkins główną usługi Azure</span><span class="sxs-lookup"><span data-stu-id="8cdf5-122">Add Azure service principal tooJenkins credential</span></span>

<span data-ttu-id="8cdf5-123">Podmiot zabezpieczeń usługi Azure jest wymagane toodeploy tooAzure.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-123">An Azure service principal is needed toodeploy tooAzure.</span></span> 

<ol>
<li><span data-ttu-id="8cdf5-124">Użyj [interfejsu wiersza polecenia Azure](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) lub [portalu Azure](/azure/azure-resource-manager/resource-group-create-service-principal-portal) toocreate nazwy głównej usługi Azure</span><span class="sxs-lookup"><span data-stu-id="8cdf5-124">Use [Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) or [Azure portal](/azure/azure-resource-manager/resource-group-create-service-principal-portal) toocreate an Azure service principal</span></span></li>
<li><span data-ttu-id="8cdf5-125">W ramach hello Wpięć pulpitu nawigacyjnego, kliknij przycisk **poświadczeń -> System ->**.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-125">Within hello Jenkins dashboard, click **Credentials -> System ->**.</span></span> <span data-ttu-id="8cdf5-126">Kliknij przycisk **credentials(unrestricted) globalne**.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-126">Click **Global credentials(unrestricted)**.</span></span></li>
<li><span data-ttu-id="8cdf5-127">Kliknij przycisk **dodać poświadczenia** tooadd nazwy głównej usługi Microsoft Azure wypełniając hello identyfikator subskrypcji, Identyfikatora klienta, klucz tajny klienta i końcowym tokenów OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-127">Click **Add Credentials** tooadd a Microsoft Azure service principal by filling out hello Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span> <span data-ttu-id="8cdf5-128">Podaj identyfikator **mySp**, do użycia w kolejnych krokach.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-128">Provide an ID, **mySp**, for use in subsequent steps.</span></span></li>
</ol>

## <a name="azure-app-service-plugin"></a><span data-ttu-id="8cdf5-129">Wtyczka usługi aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="8cdf5-129">Azure App Service plugin</span></span>

<span data-ttu-id="8cdf5-130">Azure App Service wtyczki 1.0 obsługuje tooAzure ciągłego wdrażania aplikacji sieci Web za pomocą:</span><span class="sxs-lookup"><span data-stu-id="8cdf5-130">Azure App Service plugin v1.0 supports continuous deployment tooAzure Web App through:</span></span>

* <span data-ttu-id="8cdf5-131">Git i FTP.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-131">Git and FTP</span></span>
* <span data-ttu-id="8cdf5-132">Docker dla aplikacji sieci Web w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="8cdf5-132">Docker for Web App on Linux</span></span>

## <a name="configure-jenkins-toodeploy-web-app-through-ftp-using-hello-jenkins-dashboard"></a><span data-ttu-id="8cdf5-133">Skonfiguruj toodeploy Wpięć aplikacji sieci Web za pośrednictwem FTP przy użyciu pulpitu nawigacyjnego Wpięć hello</span><span class="sxs-lookup"><span data-stu-id="8cdf5-133">Configure Jenkins toodeploy Web App through FTP using hello Jenkins dashboard</span></span>

<span data-ttu-id="8cdf5-134">toodeploy tooAzure Twojego projektu aplikacji sieci Web, możesz przekazać Twojej artefaktów kompilacji (na przykład plik .war w języku Java) przy użyciu narzędzia Git i FTP.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-134">toodeploy your project tooAzure Web App, you can upload your build artifacts (for example, .war file in Java) using Git or FTP.</span></span>

<span data-ttu-id="8cdf5-135">Przed skonfigurowaniem zadania hello w Wpięć, należy plan usługi aplikacji Azure i aplikacji sieci Web dla uruchomionej aplikacji Java hello.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-135">Before setting up hello job in Jenkins, you need an Azure App Service plan and a Web App for running hello Java app.</span></span>


1. <span data-ttu-id="8cdf5-136">Tworzenie planu usługi aplikacji Azure z hello **wolne** przy użyciu hello warstwy cenowej [Tworzenie planu usług aplikacji az](/cli/azure/appservice/plan#create) polecenia interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-136">Create an Azure App Service plan with hello **FREE** pricing tier using hello  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="8cdf5-137">planu usług aplikacji Hello definiuje hello toohost fizyczne zasoby używane aplikacje.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-137">hello appservice plan defines hello physical resources used toohost your apps.</span></span> <span data-ttu-id="8cdf5-138">Wszystkie aplikacje przypisane planu usług aplikacji tooan udostępniania tych zasobów, umożliwiając koszt toosave odnośnie do hostowania wielu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-138">All applications assigned tooan appservice plan share these resources, allowing you toosave cost when hosting multiple apps.</span></span>
2. <span data-ttu-id="8cdf5-139">Utwórz aplikację sieci Web.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-139">Create a Web App.</span></span> <span data-ttu-id="8cdf5-140">Można albo użyj hello [portalu Azure](/azure/app-service-web/web-sites-configure) lub hello Użyj następującego polecenia Az interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="8cdf5-140">You can either use hello [Azure portal](/azure/app-service-web/web-sites-configure) or use hello following Az CLI command:</span></span>
```azurecli-interactive 
az webapp create --name <myAppName> --resource-group <myResourceGroup> --plan <myAppServicePlan>
```

3. <span data-ttu-id="8cdf5-141">Upewnij się, że konfigurowanie hello konfigurację środowiska uruchomieniowego języka Java, która Twoja aplikacja powinna.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-141">Make sure you set up hello Java runtime configuration that your app needs.</span></span> <span data-ttu-id="8cdf5-142">Witaj następującego polecenia wiersza polecenia platformy Azure konfiguruje toorun aplikacji sieci web hello na ostatnie JDK 8 Java i [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-142">hello following Azure CLI command configures hello web app toorun on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>
```azurecli-interactive
az webapp config set \
--name <myAppName> \
--resource-group <myResourceGroup> \
--java-version 1.8 \
--java-container Tomcat \
--java-container-version 8.0
```

### <a name="set-up-hello-jenkins-job"></a><span data-ttu-id="8cdf5-143">Konfigurowanie hello Wpięć zadania</span><span class="sxs-lookup"><span data-stu-id="8cdf5-143">Set up hello Jenkins job</span></span>


1. <span data-ttu-id="8cdf5-144">Utwórz nową **dowolne** projektu na pulpicie nawigacyjnym Wpięć</span><span class="sxs-lookup"><span data-stu-id="8cdf5-144">Create a new **freestyle** project in Jenkins Dashboard</span></span>
2. <span data-ttu-id="8cdf5-145">Skonfiguruj **zarządzania kodem źródłowym** toouse rozwidlenia lokalnego z [prostej aplikacji sieci Web Java na platformie Azure](https://github.com/azure-devops/javawebappsample) zapewniając hello **adres URL repozytorium**.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-145">Configure **Source Code Management** toouse your local fork of [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) by providing hello **Repository URL**.</span></span> <span data-ttu-id="8cdf5-146">Na przykład: http://github.com/&lt;yourID > / javawebappsample.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-146">For example: http://github.com/&lt;yourID>/javawebappsample.</span></span>
3. <span data-ttu-id="8cdf5-147">Dodaj projekt hello toobuild kroku kompilacji za pomocą programu Maven.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-147">Add a Build step toobuild hello project using Maven.</span></span> <span data-ttu-id="8cdf5-148">W tym celu Dodawanie **wykonywania powłoki**.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-148">Do so by adding an **Execute shell**.</span></span> <span data-ttu-id="8cdf5-149">Na przykład potrzebujemy pliku dodatkowego kroku toorename hello *.war w tooROOT.war folderu docelowego.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-149">For this example, we need an additional step toorename hello *.war file in target folder tooROOT.war.</span></span>   
```bash
mvn clean package
mv target/*.war target/ROOT.war
```

4. <span data-ttu-id="8cdf5-150">Dodaj akcję po kompilacji, wybierając **publikowania aplikacji sieci Web platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-150">Add a post-build action by selecting **Publish an Azure Web App**.</span></span>
5. <span data-ttu-id="8cdf5-151">Podaj "mySp", podmiot zabezpieczeń usługi Azure hello przechowywane w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-151">Supply, "mySp", hello Azure service principal stored in previous step.</span></span>
6. <span data-ttu-id="8cdf5-152">W **Konfiguracja aplikacji** wybierz hello aplikacji sieci web i grupy zasobów w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-152">In **App Configuration** section, choose hello resource group and web app in your subscription.</span></span> <span data-ttu-id="8cdf5-153">Dodatek Hello automatycznie wykrywa, czy Windows hello aplikacji sieci Web lub opartych na systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-153">hello plugin automatically detects whether hello Web App is Windows or Linux-based.</span></span> <span data-ttu-id="8cdf5-154">W przypadku aplikacji sieci Web opartych na systemie Windows hello opcji "Publikowania plików" jest widoczne.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-154">For a Windows-based Web App, hello option "Publish Files" is presented.</span></span>
7. <span data-ttu-id="8cdf5-155">Wypełnij w plikach hello ma toodeploy (na przykład plik war pakiet Jeśli używasz programu Java.) Katalog źródłowy i katalog docelowy są opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-155">Fill in hello files you want toodeploy (for example, a war package if you're using Java.) Source Directory and Target Directory are optional.</span></span> <span data-ttu-id="8cdf5-156">Parametry Hello Zezwalaj folder źródłowy i docelowy toospecify przekazywania plików.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-156">hello parameters allow you toospecify source and target folders when uploading files.</span></span> <span data-ttu-id="8cdf5-157">Aplikacja sieci web Java na platformie Azure jest uruchamiane na serwerze Tomcat.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-157">Java web app on Azure is run in a Tomcat server.</span></span> <span data-ttu-id="8cdf5-158">Dlatego możesz przekazać war się pakiet do folderu webapps.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-158">So you upload you war package to webapps folder.</span></span> <span data-ttu-id="8cdf5-159">Na przykład ustawić **katalog źródłowy** zbyt "target" i "Używanie" podać **katalog docelowy**.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-159">For this example, set **Source Directory** too"target" and supply "webapps" for **Target Directory**.</span></span>
8. <span data-ttu-id="8cdf5-160">Jeśli chcesz toodeploy tooa miejsca niż produkcji, można również ustawić **miejsca** nazwy.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-160">If you want toodeploy tooa slot other than production, you can also set **Slot** Name.</span></span>
9. <span data-ttu-id="8cdf5-161">Zapisz hello projektu i skompiluj go.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-161">Save hello project and build it.</span></span> <span data-ttu-id="8cdf5-162">Aplikacja sieci web jest wdrożony tooAzure po zakończeniu kompilacji.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-162">Your web app is deployed tooAzure when build is complete.</span></span>

### <a name="deploy-web-app-through-ftp-using-jenkins-pipeline"></a><span data-ttu-id="8cdf5-163">Wdrażanie aplikacji sieci Web za pośrednictwem FTP za pomocą potoku Wpięć</span><span class="sxs-lookup"><span data-stu-id="8cdf5-163">Deploy Web App through FTP using Jenkins pipeline</span></span>

<span data-ttu-id="8cdf5-164">Wtyczka Hello jest gotowe do potoku.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-164">hello plugin is pipeline-ready.</span></span> <span data-ttu-id="8cdf5-165">Może się odwoływać próbki tooa w repozytorium GitHub hello.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-165">You can refer tooa sample in hello GitHub repo.</span></span>

1. <span data-ttu-id="8cdf5-166">W witrynie GitHub interfejsu użytkownika sieci web, otwórz **Jenkinsfile_ftp_plugin** pliku.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-166">In GitHub web UI, open **Jenkinsfile_ftp_plugin** file.</span></span> <span data-ttu-id="8cdf5-167">Kliknij przycisk tooedit ikonę ołówka hello tej grupy zasobów hello tooupdate pliku i nazwa aplikacji sieci web w wierszu 11 i 12.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-167">Click hello pencil icon tooedit this file tooupdate hello resource group and name of your web app on line 11 and 12 respectively.</span></span>    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. <span data-ttu-id="8cdf5-168">Zmień identyfikator poświadczeń 14 tooupdate wiersz w wystąpieniu Wpięć.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-168">Change line 14 tooupdate credential ID in your Jenkins instance.</span></span>    
```java
withCredentials([azureServicePrincipal('<mySp>')]) {
```

### <a name="create-a-jenkins-pipeline"></a><span data-ttu-id="8cdf5-169">Tworzenie potoku Wpięć</span><span class="sxs-lookup"><span data-stu-id="8cdf5-169">Create a Jenkins pipeline</span></span>

1. <span data-ttu-id="8cdf5-170">Otwórz Wpięć w przeglądarce sieci web, kliknij pozycję **nowy element**.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-170">Open Jenkins in a web browser, click **New Item**.</span></span>
2. <span data-ttu-id="8cdf5-171">Podaj nazwę zadania hello i wybierz **potoku**.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-171">Provide a name for hello job and select **Pipeline**.</span></span> <span data-ttu-id="8cdf5-172">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-172">Click **OK**.</span></span>
3. <span data-ttu-id="8cdf5-173">Kliknij przycisk hello **potoku** karcie dalej.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-173">Click hello **Pipeline** tab next.</span></span>
4. <span data-ttu-id="8cdf5-174">Dla **definicji**, wybierz pozycję **potoku skryptu z SCM**.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-174">For **Definition**, select **Pipeline script from SCM**.</span></span>
5. <span data-ttu-id="8cdf5-175">Aby uzyskać **SCM**, wybierz pozycję **Git**.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-175">For **SCM**, select **Git**.</span></span> <span data-ttu-id="8cdf5-176">Wprowadź hello GitHub adres URL dla Twojego repozytorium rozwidlonych: https:&lt;Twojego repozytorium rozwidlonych > .git</span><span class="sxs-lookup"><span data-stu-id="8cdf5-176">Enter hello GitHub URL for your forked repo: https:&lt;your forked repo>.git</span></span>
6. <span data-ttu-id="8cdf5-177">Aktualizacja **ścieżka skryptu** zbyt "Jenkinsfile_ftp_plugin"</span><span class="sxs-lookup"><span data-stu-id="8cdf5-177">Update **Script Path** too"Jenkinsfile_ftp_plugin"</span></span>
7. <span data-ttu-id="8cdf5-178">Kliknij przycisk **zapisać** i hello wykonywania zadania.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-178">Click **Save** and run hello job.</span></span>

## <a name="configure-jenkins-toodeploy-web-app-on-linux-through-docker"></a><span data-ttu-id="8cdf5-179">Skonfiguruj toodeploy Wpięć aplikacji sieci Web w systemie Linux przy użyciu rozwiązania Docker</span><span class="sxs-lookup"><span data-stu-id="8cdf5-179">Configure Jenkins toodeploy Web App on Linux through Docker</span></span>

<span data-ttu-id="8cdf5-180">Oprócz Git/FTP aplikacji sieci Web w systemie Linux obsługuje wdrażanie przy użyciu rozwiązania Docker.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-180">Apart from Git/FTP, Web App on Linux supports deployment using Docker.</span></span> <span data-ttu-id="8cdf5-181">toodeploy przy użyciu rozwiązania Docker, należy tooprovide plik Dockerfile, które pakiety aplikacji sieci web za pomocą usługi czasu wykonywania w obrazie docker.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-181">toodeploy using Docker, you need tooprovide a Dockerfile that packages your web app with service runtime into a docker image.</span></span> <span data-ttu-id="8cdf5-182">Następnie wtyczki hello tworzy obraz powitania, wypchnięcia jej tooa docker rejestru i wdraża aplikację sieci web tooyour obraz powitania.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-182">Then hello plugin builds hello image, pushes it tooa docker registry and deploys hello image tooyour web app.</span></span>

<span data-ttu-id="8cdf5-183">Aplikacji w systemie Linux sieci Web obsługuje także tradycyjnych sposoby, takie jak usługi Git i FTP, ale tylko dla wbudowanych języków (.NET Core, Node.js, PHP i Ruby).</span><span class="sxs-lookup"><span data-stu-id="8cdf5-183">Web App on Linux also supports traditional ways like Git and FTP, but only for built-in languages (.NET Core, Node.js, PHP, and Ruby).</span></span> <span data-ttu-id="8cdf5-184">W przypadku innych języków toopackage runtime kod i usługi aplikacji razem w obrazie docker a za pomocą docker toodeploy.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-184">For other languages, you need toopackage your application code and service runtime together into a docker image and use docker toodeploy.</span></span>

<span data-ttu-id="8cdf5-185">Przed skonfigurowaniem zadania hello w Wpięć, należy usługi aplikacji Azure w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-185">Before setting up hello job in Jenkins, you need an Azure app service on Linux.</span></span> <span data-ttu-id="8cdf5-186">Rejestru kontenera jest również wymagana toostore i zarządzaj nimi prywatnej obrazy usługi Docker kontenera.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-186">A container registry is also needed toostore and manage your private Docker container images.</span></span> <span data-ttu-id="8cdf5-187">Można użyć DockerHub; w tym przykładzie jest używany rejestru kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-187">You can use DockerHub; we are using Azure Container Registry for this example.</span></span>

* <span data-ttu-id="8cdf5-188">Możesz wykonać kroki hello [tutaj](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate aplikacji sieci Web w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="8cdf5-188">You can follow hello steps [here](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate a Web App on Linux</span></span> 
* <span data-ttu-id="8cdf5-189">Rejestru kontenera platformy Azure jest zarządzany [Docker rejestru] usługi (https://docs.docker.com/registry/) na podstawie hello 2.0 rejestru Docker open source.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-189">Azure Container Registry is a managed [Docker registry] (https://docs.docker.com/registry/) service based on hello open-source Docker Registry 2.0.</span></span> <span data-ttu-id="8cdf5-190">Wykonaj kroki hello [tutaj] (/ azure/container-registry/container-registry-get-started-azure-cli) Aby uzyskać więcej pomocy na temat toodo tak.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-190">Follow hello steps [here] (/azure/container-registry/container-registry-get-started-azure-cli) for more guidance on how toodo so.</span></span> <span data-ttu-id="8cdf5-191">Można również użyć DockerHub.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-191">You can also use DockerHub.</span></span>

### <a name="toodeploy-using-docker"></a><span data-ttu-id="8cdf5-192">przy użyciu rozwiązania docker toodeploy:</span><span class="sxs-lookup"><span data-stu-id="8cdf5-192">toodeploy using docker:</span></span>

1. <span data-ttu-id="8cdf5-193">Utwórz nowy projekt stylu Wpięć w pulpicie nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-193">Create a new freestyle project in Jenkins Dashboard.</span></span>
2. <span data-ttu-id="8cdf5-194">Skonfiguruj **zarządzania kodem źródłowym** toouse rozwidlenia lokalnego z [prostej aplikacji sieci Web Java na platformie Azure](https://github.com/azure-devops/javawebappsample) zapewniając hello **adres URL repozytorium**.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-194">Configure **Source Code Management** toouse your local fork of [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) by providing hello **Repository URL**.</span></span> <span data-ttu-id="8cdf5-195">Na przykład: http://github.com/&lt;yourid > / javawebappsample.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-195">For example: http://github.com/&lt;yourid>/javawebappsample.</span></span>
<span data-ttu-id="8cdf5-196">Dodaj projekt hello toobuild kroku kompilacji za pomocą programu Maven.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-196">Add a Build step toobuild hello project using Maven.</span></span> <span data-ttu-id="8cdf5-197">To zrobić przez dodanie **wykonywania powłoki** i Dodaj powitania po wierszu **polecenia**:</span><span class="sxs-lookup"><span data-stu-id="8cdf5-197">Do so by adding an **Execute shell** and add hello following line in **Command**:</span></span>    
```bash
mvn clean package
```

3. <span data-ttu-id="8cdf5-198">Dodaj akcję po kompilacji, wybierając **publikowania aplikacji sieci Web platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-198">Add a post-build action by selecting **Publish an Azure Web App**.</span></span>
4. <span data-ttu-id="8cdf5-199">Podaj, **mySp**, podmiot zabezpieczeń usługi Azure hello przechowywane w poprzednim kroku jako poświadczeń usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-199">Supply, **mySp**, hello Azure service principal stored in previous step as Azure Credentials.</span></span>
5. <span data-ttu-id="8cdf5-200">W **Konfiguracja aplikacji** wybierz hello grupy zasobów i aplikacji sieci web systemu Linux w Twojej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-200">In **App Configuration** section, choose hello resource group and a Linux web app in your subscription.</span></span>
6. <span data-ttu-id="8cdf5-201">Wybierz publikowanie za pośrednictwem Docker.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-201">Choose Publish via Docker.</span></span>
7. <span data-ttu-id="8cdf5-202">Wypełnij **plik Dockerfile** ścieżki.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-202">Fill in **Dockerfile** path.</span></span> <span data-ttu-id="8cdf5-203">Umożliwia zachowanie domyślne hello "/ plik Dockerfile" dla **URL rejestru Docker**, dostawy w formacie hello https://&lt;myRegistry >. azurecr.io, korzystając z rejestru kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-203">You can keep hello default "/Dockerfile" For **Docker registry URL**, supply in hello format of https://&lt;myRegistry>.azurecr.io if you use Azure Container Registry.</span></span> <span data-ttu-id="8cdf5-204">Pozostaw pole puste, jeśli używasz DockerHub.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-204">Leave it blank if you use DockerHub.</span></span>
8. <span data-ttu-id="8cdf5-205">Dla **poświadczenia rejestru**, Dodaj poświadczenie hello hello rejestru kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-205">For **Registry credentials**, add hello credential for hello Azure Container Registry.</span></span> <span data-ttu-id="8cdf5-206">Witaj identyfikator użytkownika i hasło można uzyskać, uruchamiając hello następującego polecenia wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-206">You can get hello userid and password by running hello following commands in Azure CLI.</span></span> <span data-ttu-id="8cdf5-207">pierwsze polecenie Hello umożliwia hello konta administratora.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-207">hello first command enables hello administrator account.</span></span>    
```azurecli-interactive
az acr update -n <yourRegistry> --admin-enabled true
az acr credential show -n <yourRegistry>
```

9. <span data-ttu-id="8cdf5-208">Witaj nazwa obrazu docker i tagu w **zaawansowane** kartę są opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-208">hello docker image name and tag in **Advanced** tab are optional.</span></span> <span data-ttu-id="8cdf5-209">Domyślnie nazwa obrazu są uzyskiwane z obrazu hello nazwę skonfigurowaną w tagu Azure hello portalu (w kontenerze Docker ustawienie.) są generowane na podstawie $BUILD_NUMBER.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-209">By default, image name is obtained from hello image name you configured in Azure portal (in Docker Container setting.) hello tag is generated from $BUILD_NUMBER.</span></span> <span data-ttu-id="8cdf5-210">Upewnij się, określ nazwę obraz powitania w jednej wersji portalu Azure lub podać wartość **obrazu Docker** w **zaawansowane** kartę. Na przykład Podaj "&lt;yourRegistry >.azurecr.io/calculator" dla **obrazu Docker** i pozostawić **Tag obrazu Docker** puste.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-210">Make sure you specify hello image name in either Azure portal or supply a value for **Docker Image** in **Advanced** tab. For this example, supply "&lt;yourRegistry>.azurecr.io/calculator" for **Docker image** and leave **Docker Image Tag** blank.</span></span>
10. <span data-ttu-id="8cdf5-211">Uwaga, wdrożenie zakończy się niepowodzeniem, korzystając z wbudowanego ustawienie obrazu Docker.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-211">Note deployment fails if you use built-in Docker image setting.</span></span> <span data-ttu-id="8cdf5-212">Upewnij się, że zmiana docker config toouse niestandardowego obrazu w kontenerze Docker ustawienia w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-212">Make sure you change docker config toouse custom image in Docker Container setting in Azure portal.</span></span> <span data-ttu-id="8cdf5-213">Wbudowane obrazu użyj toodeploy podejście przekazywania plików.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-213">For built-in image, use file upload approach toodeploy.</span></span>
11. <span data-ttu-id="8cdf5-214">Podejście podobne przekazywania toofile, można wybrać różne miejsca niż produkcji.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-214">Similar toofile upload approach, you can choose a different slot other than production.</span></span>
12. <span data-ttu-id="8cdf5-215">Zapisania i skompilowania projektu hello.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-215">Save and build hello project.</span></span> <span data-ttu-id="8cdf5-216">Zobaczysz kontener obrazu spoczywa tooyour rejestru i wdrażania aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-216">You see your container image is pushed tooyour registry and web app is deployed.</span></span>

### <a name="deploy-tooweb-app-on-linux-through-docker-using-jenkins-pipeline"></a><span data-ttu-id="8cdf5-217">Wdrażanie aplikacji w systemie Linux przy użyciu rozwiązania Docker za pomocą potoku Wpięć tooWeb</span><span class="sxs-lookup"><span data-stu-id="8cdf5-217">Deploy tooWeb App on Linux through Docker using Jenkins pipeline</span></span>

1. <span data-ttu-id="8cdf5-218">W witrynie GitHub interfejsu użytkownika sieci web, otwórz **Jenkinsfile_container_plugin** pliku.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-218">In GitHub web UI, open **Jenkinsfile_container_plugin** file.</span></span> <span data-ttu-id="8cdf5-219">Kliknij przycisk tooedit ikonę ołówka hello tej grupy zasobów hello tooupdate pliku i nazwa aplikacji sieci web w wierszu 11 i 12.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-219">Click hello pencil icon tooedit this file tooupdate hello resource group and name of your web app on line 11 and 12 respectively.</span></span>    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. <span data-ttu-id="8cdf5-220">Zmiana wiersza 13 tooyour kontenera rejestru serwera</span><span class="sxs-lookup"><span data-stu-id="8cdf5-220">Change line 13 tooyour container registry server</span></span>    
```java
def registryServer = '<registryURL>'
```    

3. <span data-ttu-id="8cdf5-221">Zmień identyfikator poświadczeń 16 tooupdate wiersz w wystąpieniu Wpięć</span><span class="sxs-lookup"><span data-stu-id="8cdf5-221">Change line 16 tooupdate credential ID in your Jenkins instance</span></span>    
```java
azureWebAppPublish azureCredentialsId: '<mySp>', publishType: 'docker', resourceGroup: resourceGroup, appName: webAppName, dockerImageName: imageName, dockerImageTag: imageTag, dockerRegistryEndpoint: [credentialsId: 'acr', url: "http://$registryServer"]
```    
### <a name="create-jenkins-pipeline"></a><span data-ttu-id="8cdf5-222">Tworzenie potoku Wpięć</span><span class="sxs-lookup"><span data-stu-id="8cdf5-222">Create Jenkins pipeline</span></span>    

1. <span data-ttu-id="8cdf5-223">Otwórz Wpięć w przeglądarce sieci web, kliknij pozycję **nowy element**.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-223">Open Jenkins in a web browser, click **New Item**.</span></span>
2. <span data-ttu-id="8cdf5-224">Podaj nazwę zadania hello i wybierz **potoku**.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-224">Provide a name for hello job and select **Pipeline**.</span></span> <span data-ttu-id="8cdf5-225">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-225">Click **OK**.</span></span>
3. <span data-ttu-id="8cdf5-226">Kliknij przycisk hello **potoku** karcie dalej.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-226">Click hello **Pipeline** tab next.</span></span>
4. <span data-ttu-id="8cdf5-227">Dla **definicji**, wybierz pozycję **potoku skryptu z SCM**.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-227">For **Definition**, select **Pipeline script from SCM**.</span></span>
5. <span data-ttu-id="8cdf5-228">Aby uzyskać **SCM**, wybierz pozycję **Git**.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-228">For **SCM**, select **Git**.</span></span>
6. <span data-ttu-id="8cdf5-229">Wprowadź hello GitHub adres URL dla Twojego repozytorium rozwidlonych: https:&lt;Twojego repozytorium rozwidlonych > .git</span><span class="sxs-lookup"><span data-stu-id="8cdf5-229">Enter hello GitHub URL for your forked repo: https:&lt;your forked repo>.git</span></span></li>
<span data-ttu-id="8cdf5-230">Zaktualizuj 7, **ścieżka skryptu** zbyt "Jenkinsfile_container_plugin"</span><span class="sxs-lookup"><span data-stu-id="8cdf5-230">7, Update **Script Path** too"Jenkinsfile_container_plugin"</span></span>
8. <span data-ttu-id="8cdf5-231">Kliknij przycisk **zapisać** i hello wykonywania zadania.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-231">Click **Save** and run hello job.</span></span>

## <a name="verify-your-web-app"></a><span data-ttu-id="8cdf5-232">Sprawdź aplikację sieci web</span><span class="sxs-lookup"><span data-stu-id="8cdf5-232">Verify your web app</span></span>

1. <span data-ttu-id="8cdf5-233">plik WAR hello tooverify został wdrożony pomyślnie tooyour aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-233">tooverify hello WAR file is deployed successfully tooyour web app.</span></span> <span data-ttu-id="8cdf5-234">Otwórz przeglądarkę sieci web.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-234">Open a web browser.</span></span>
2. <span data-ttu-id="8cdf5-235">Przejdź toohttp: / /&lt;nazwa_aplikacji >.azurewebsites.net/api/calculator/ping zostanie wyświetlony:</span><span class="sxs-lookup"><span data-stu-id="8cdf5-235">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/ping You see:</span></span>    
     <span data-ttu-id="8cdf5-236">Zapraszamy tooJava aplikacji sieci Web!</span><span class="sxs-lookup"><span data-stu-id="8cdf5-236">Welcome tooJava Web App!!!</span></span> <span data-ttu-id="8cdf5-237">Ta wartość jest aktualizowana!</span><span class="sxs-lookup"><span data-stu-id="8cdf5-237">This is updated!</span></span>
   <span data-ttu-id="8cdf5-238">Sun cze 17 16:39:10 UTC 2017</span><span class="sxs-lookup"><span data-stu-id="8cdf5-238">Sun Jun 17 16:39:10 UTC 2017</span></span>
3. <span data-ttu-id="8cdf5-239">Przejdź toohttp: / /&lt;nazwa_aplikacji >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (Zastąp &lt;x > i &lt;y > z dowolnej liczby) tooget hello sumę x i y</span><span class="sxs-lookup"><span data-stu-id="8cdf5-239">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) tooget hello sum of x and y</span></span>        
    ![Kalkulator: Dodaj](./media/execute-cli-jenkins-pipeline/calculator-add.png)

### <a name="for-app-service-on-linux"></a><span data-ttu-id="8cdf5-241">Usługi aplikacji w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="8cdf5-241">For App service on Linux</span></span>

* <span data-ttu-id="8cdf5-242">tooverify w wiersza polecenia platformy Azure, uruchom:</span><span class="sxs-lookup"><span data-stu-id="8cdf5-242">tooverify, in Azure CLI, run:</span></span>

    ```
    az acr repository list -n <myRegistry> -o json
    ```

    <span data-ttu-id="8cdf5-243">Możesz uzyskać hello następujące wyniki:</span><span class="sxs-lookup"><span data-stu-id="8cdf5-243">You get hello following result:</span></span>
    
    ```
    [
    "calculator"
    ]
    ```
    
    <span data-ttu-id="8cdf5-244">Przejdź toohttp: / /&lt;nazwa_aplikacji >.azurewebsites.net/api/calculator/ping.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-244">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/ping.</span></span> <span data-ttu-id="8cdf5-245">Zostanie wyświetlony komunikat hello:</span><span class="sxs-lookup"><span data-stu-id="8cdf5-245">You see hello message:</span></span> 
    
        Welcome tooJava Web App!!! This is updated!
        Sun Jul 09 16:39:10 UTC 2017

    <span data-ttu-id="8cdf5-246">Przejdź toohttp: / /&lt;nazwa_aplikacji >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (Zastąp &lt;x > i &lt;y > z dowolnej liczby) tooget hello sumę x i y</span><span class="sxs-lookup"><span data-stu-id="8cdf5-246">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) tooget hello sum of x and y</span></span>
    
## <a name="next-steps"></a><span data-ttu-id="8cdf5-247">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8cdf5-247">Next steps</span></span>

<span data-ttu-id="8cdf5-248">W tym samouczku używamy tooAzure toodeploy wtyczki hello w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="8cdf5-248">In this tutorial, you use hello Azure App Service plugin toodeploy tooAzure.</span></span>

<span data-ttu-id="8cdf5-249">W tym samouczku omówiono:</span><span class="sxs-lookup"><span data-stu-id="8cdf5-249">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8cdf5-250">Skonfiguruj toodeploy Wpięć usługi Azure App Service za pośrednictwem FTP</span><span class="sxs-lookup"><span data-stu-id="8cdf5-250">Configure Jenkins toodeploy Azure App Service through FTP</span></span> 
> * <span data-ttu-id="8cdf5-251">Skonfiguruj tooAzure toodeploy Wpięć usługi aplikacji w systemie Linux przy użyciu rozwiązania Docker</span><span class="sxs-lookup"><span data-stu-id="8cdf5-251">Configure Jenkins toodeploy tooAzure App Service on Linux through Docker</span></span> 
