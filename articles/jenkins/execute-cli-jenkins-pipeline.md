---
title: "Witaj aaaExecute wiersza polecenia platformy Azure z Wpięć | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse toodeploy interfejsu wiersza polecenia Azure Java web tooAzure aplikacji w potoku Wpięć"
services: app-service\web
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: jenkins
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 6/7/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 4bd1e12e6de1f010453ff51c835f84e7361962f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-app-service-with-jenkins-and-hello-azure-cli"></a><span data-ttu-id="1c46c-103">Wdrażanie aplikacji usługi z Wpięć tooAzure i hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="1c46c-103">Deploy tooAzure App Service with Jenkins and hello Azure CLI</span></span>
<span data-ttu-id="1c46c-104">toodeploy tooAzure aplikacji sieci web Java można użyć wiersza polecenia platformy Azure w [potoku Wpięć](https://jenkins.io/doc/book/pipeline/).</span><span class="sxs-lookup"><span data-stu-id="1c46c-104">toodeploy a Java web app tooAzure, you can use Azure CLI in [Jenkins Pipeline](https://jenkins.io/doc/book/pipeline/).</span></span> <span data-ttu-id="1c46c-105">W tym samouczku, możesz utworzyć potok CI/CD na maszynie Wirtualnej platformy Azure w tym jak:</span><span class="sxs-lookup"><span data-stu-id="1c46c-105">In this tutorial, you create a CI/CD pipeline on an Azure VM including how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1c46c-106">Tworzenie maszyny Wirtualnej z Wpięć</span><span class="sxs-lookup"><span data-stu-id="1c46c-106">Create a Jenkins VM</span></span>
> * <span data-ttu-id="1c46c-107">Skonfiguruj Wpięć</span><span class="sxs-lookup"><span data-stu-id="1c46c-107">Configure Jenkins</span></span>
> * <span data-ttu-id="1c46c-108">Tworzenie aplikacji sieci web na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="1c46c-108">Create a web app in Azure</span></span>
> * <span data-ttu-id="1c46c-109">Przygotowanie repozytorium GitHub</span><span class="sxs-lookup"><span data-stu-id="1c46c-109">Prepare a GitHub repository</span></span>
> * <span data-ttu-id="1c46c-110">Tworzenie potoku Wpięć</span><span class="sxs-lookup"><span data-stu-id="1c46c-110">Create Jenkins pipeline</span></span>
> * <span data-ttu-id="1c46c-111">Należy uruchomić potoku hello i sprawdzić hello aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="1c46c-111">Run hello pipeline and verify hello web app</span></span>

<span data-ttu-id="1c46c-112">Ten samouczek wymaga hello Azure CLI w wersji 2.0.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="1c46c-112">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="1c46c-113">Wersja hello toofind, uruchom `az --version`.</span><span class="sxs-lookup"><span data-stu-id="1c46c-113">toofind hello version, run `az --version`.</span></span> <span data-ttu-id="1c46c-114">Jeśli potrzebujesz tooupgrade, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="1c46c-114">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-and-configure-jenkins-instance"></a><span data-ttu-id="1c46c-115">Tworzenie i konfigurowanie Wpięć wystąpienia</span><span class="sxs-lookup"><span data-stu-id="1c46c-115">Create and Configure Jenkins instance</span></span>
<span data-ttu-id="1c46c-116">Jeśli nie masz już wzorca Wpięć, rozpoczynać hello [szablon rozwiązania](install-jenkins-solution-template.md), która obejmuje hello wymagane [poświadczenia Azure](https://plugins.jenkins.io/azure-credentials) wtyczki domyślnie.</span><span class="sxs-lookup"><span data-stu-id="1c46c-116">If you do not already have a Jenkins master, start with hello [Solution Template](install-jenkins-solution-template.md), which includes hello required [Azure Credentials](https://plugins.jenkins.io/azure-credentials) plugin by default.</span></span> 

<span data-ttu-id="1c46c-117">wtyczki poświadczenia Azure Hello umożliwia toostore poświadczenia główne usługi Microsoft Azure z Wpięć.</span><span class="sxs-lookup"><span data-stu-id="1c46c-117">hello Azure Credential plugin allows you toostore Microsoft Azure service principal credentials in Jenkins.</span></span> <span data-ttu-id="1c46c-118">W wersji 1.2 Dodaliśmy obsługę hello dlatego tego potoku Wpięć można pobrać hello Azure poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="1c46c-118">In version 1.2, we added hello support so that Jenkins Pipeline can get hello Azure credentials.</span></span> 

<span data-ttu-id="1c46c-119">Upewnij się, że w wersji 1.2 lub nowszej:</span><span class="sxs-lookup"><span data-stu-id="1c46c-119">Ensure you have version 1.2 or later:</span></span>
* <span data-ttu-id="1c46c-120">W ramach hello Wpięć pulpitu nawigacyjnego, kliknij przycisk **Menedżera wtyczki -> Zarządzaj Wpięć ->** i wyszukaj **poświadczenia Azure**.</span><span class="sxs-lookup"><span data-stu-id="1c46c-120">Within hello Jenkins dashboard, click **Manage Jenkins -> Plugin Manager ->** and search for **Azure Credential**.</span></span> 
* <span data-ttu-id="1c46c-121">Zaktualizuj hello wtyczki, jeśli wersja hello jest starsza niż 1.2.</span><span class="sxs-lookup"><span data-stu-id="1c46c-121">Update hello plugin if hello version is earlier than 1.2.</span></span>

<span data-ttu-id="1c46c-122">Java JDK i Maven są również wymagane w hello Wpięć wzorca.</span><span class="sxs-lookup"><span data-stu-id="1c46c-122">Java JDK and Maven are also required in hello Jenkins master.</span></span> <span data-ttu-id="1c46c-123">tooinstall, zaloguj się przy użyciu protokołu SSH wzorca tooJenkins i uruchom następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="1c46c-123">tooinstall, log in tooJenkins master using SSH and run hello following commands:</span></span>
```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

## <a name="add-azure-service-principal-toojenkins-credential"></a><span data-ttu-id="1c46c-124">Dodaj poświadczenie tooJenkins główną usługi Azure</span><span class="sxs-lookup"><span data-stu-id="1c46c-124">Add Azure service principal tooJenkins credential</span></span>

<span data-ttu-id="1c46c-125">Poświadczenie Azure jest wymagane tooexecute wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1c46c-125">An Azure credential is needed tooexecute Azure CLI.</span></span>

* <span data-ttu-id="1c46c-126">W ramach hello Wpięć pulpitu nawigacyjnego, kliknij przycisk **poświadczeń -> System ->**.</span><span class="sxs-lookup"><span data-stu-id="1c46c-126">Within hello Jenkins dashboard, click **Credentials -> System ->**.</span></span> <span data-ttu-id="1c46c-127">Kliknij przycisk **credentials(unrestricted) globalne**.</span><span class="sxs-lookup"><span data-stu-id="1c46c-127">Click **Global credentials(unrestricted)**.</span></span>
* <span data-ttu-id="1c46c-128">Kliknij przycisk **dodać poświadczenia** tooadd [nazwy głównej usługi Microsoft Azure](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) wypełniając hello identyfikator subskrypcji, Identyfikatora klienta, klucz tajny klienta i końcowym tokenów OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="1c46c-128">Click **Add Credentials** tooadd a [Microsoft Azure service principal](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) by filling out hello Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span> <span data-ttu-id="1c46c-129">Podaj identyfikator do użycia w kolejnym kroku.</span><span class="sxs-lookup"><span data-stu-id="1c46c-129">Provide an ID for use in subsequent step.</span></span>

![Dodawanie poświadczeń](./media/execute-cli-jenkins-pipeline/add-credentials.png)

## <a name="create-an-azure-app-service-for-deploying-hello-java-web-app"></a><span data-ttu-id="1c46c-131">Tworzenie usługi aplikacji Azure do wdrażania aplikacji sieci web Java hello</span><span class="sxs-lookup"><span data-stu-id="1c46c-131">Create an Azure App Service for deploying hello Java web app</span></span>

<span data-ttu-id="1c46c-132">Tworzenie planu usługi aplikacji Azure z hello **wolne** przy użyciu hello warstwy cenowej [Tworzenie planu usług aplikacji az](/cli/azure/appservice/plan#create) polecenia interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="1c46c-132">Create an Azure App Service plan with hello **FREE** pricing tier using hello  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="1c46c-133">planu usług aplikacji Hello definiuje hello toohost fizyczne zasoby używane aplikacje.</span><span class="sxs-lookup"><span data-stu-id="1c46c-133">hello appservice plan defines hello physical resources used toohost your apps.</span></span> <span data-ttu-id="1c46c-134">Wszystkie aplikacje przypisane planu usług aplikacji tooan udostępniania tych zasobów, umożliwiając koszt toosave odnośnie do hostowania wielu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1c46c-134">All applications assigned tooan appservice plan share these resources, allowing you toosave cost when hosting multiple apps.</span></span> 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

<span data-ttu-id="1c46c-135">Jeśli hello plan jest gotowy, powitalne interfejsu wiersza polecenia Azure zawiera podobne dane wyjściowe toohello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="1c46c-135">When hello plan is ready, hello Azure CLI shows similar output toohello following example:</span></span>

```json
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "North Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/0000-0000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan",
  "kind": "app",
  "location": "North Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  ...
  < Output has been truncated for readability >
} 
``` 

### <a name="create-an-azure-web-app"></a><span data-ttu-id="1c46c-136">Tworzenie aplikacji sieci Web platformy Azure</span><span class="sxs-lookup"><span data-stu-id="1c46c-136">Create an Azure Web app</span></span>

 <span data-ttu-id="1c46c-137">Użyj hello [tworzenie aplikacji sieci Web az](/cli/azure/appservice/web#create) toocreate polecenia interfejsu wiersza polecenia definicję aplikacji sieci web w hello `myAppServicePlan` planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1c46c-137">Use hello [az webapp create](/cli/azure/appservice/web#create) CLI command toocreate a web app definition in hello `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="1c46c-138">definicję aplikacji sieci web Hello zapewnia tooaccess adres URL aplikacji przy użyciu i konfiguruje kilka opcji toodeploy Twojego tooAzure kodu.</span><span class="sxs-lookup"><span data-stu-id="1c46c-138">hello web app definition provides a URL tooaccess your application with and configures several options toodeploy your code tooAzure.</span></span> 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

<span data-ttu-id="1c46c-139">SUBSTITUTE hello `<app_name>` symbol zastępczy własne unikatowej nazwy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1c46c-139">Substitute hello `<app_name>` placeholder with your own unique app name.</span></span> <span data-ttu-id="1c46c-140">Ta nazwa jest część hello domyślna nazwa domeny dla aplikacji sieci web hello, więc nazwa hello musi toobe unikatowy przez wszystkie aplikacje w usłudze Azure.</span><span class="sxs-lookup"><span data-stu-id="1c46c-140">This unique name is part of hello default domain name for hello web app, so hello name needs toobe unique across all apps in Azure.</span></span> <span data-ttu-id="1c46c-141">Przed udostępnieniem jej tooyour użytkowników, możesz mapować aplikacji sieci web toohello wpis nazwy domeny niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="1c46c-141">You can map a custom domain name entry toohello web app before you expose it tooyour users.</span></span>

<span data-ttu-id="1c46c-142">Podczas definiowania aplikacji sieci web hello jest gotowy, hello Azure CLI pokazuje informacje toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="1c46c-142">When hello web app definition is ready, hello Azure CLI shows information similar toohello following example:</span></span> 

```json 
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
   ...
  < Output has been truncated for readability >
}
```

### <a name="configure-java"></a><span data-ttu-id="1c46c-143">Konfigurowanie języka Java</span><span class="sxs-lookup"><span data-stu-id="1c46c-143">Configure Java</span></span> 

<span data-ttu-id="1c46c-144">Skonfigurować hello Java runtime wymagające aplikacji z hello [aktualizacja konfiguracji sieci web appservice az](/cli/azure/appservice/web/config#update) polecenia.</span><span class="sxs-lookup"><span data-stu-id="1c46c-144">Set up hello Java runtime configuration that your app needs with hello  [az appservice web config update](/cli/azure/appservice/web/config#update) command.</span></span>

<span data-ttu-id="1c46c-145">Witaj następujące polecenie konfiguruje toorun aplikacji sieci web hello na ostatnie JDK 8 Java i [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span><span class="sxs-lookup"><span data-stu-id="1c46c-145">hello following command configures hello web app toorun on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

## <a name="prepare-a-github-repository"></a><span data-ttu-id="1c46c-146">Przygotowanie repozytorium GitHub</span><span class="sxs-lookup"><span data-stu-id="1c46c-146">Prepare a GitHub Repository</span></span>
<span data-ttu-id="1c46c-147">Otwórz hello [prostej aplikacji sieci Web Java na platformie Azure](https://github.com/azure-devops/javawebappsample) repozytorium.</span><span class="sxs-lookup"><span data-stu-id="1c46c-147">Open hello [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) repo.</span></span> <span data-ttu-id="1c46c-148">toofork hello repozytorium tooyour własne konto GitHub, kliknij przycisk hello **rozwidlenia** przycisk w prawym górnym rogu hello.</span><span class="sxs-lookup"><span data-stu-id="1c46c-148">toofork hello repo tooyour own GitHub account, click hello **Fork** button in hello top right-hand corner.</span></span>

* <span data-ttu-id="1c46c-149">W witrynie GitHub interfejsu użytkownika sieci web, otwórz **Jenkinsfile** pliku.</span><span class="sxs-lookup"><span data-stu-id="1c46c-149">In GitHub web UI, open **Jenkinsfile** file.</span></span> <span data-ttu-id="1c46c-150">Kliknij przycisk tooedit ikonę ołówka hello tej grupy zasobów hello tooupdate pliku i nazwa aplikacji sieci web w wierszu 20 i 21.</span><span class="sxs-lookup"><span data-stu-id="1c46c-150">Click hello pencil icon tooedit this file tooupdate hello resource group and name of your web app on line 20 and 21 respectively.</span></span>

```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<app_name>'
```

* <span data-ttu-id="1c46c-151">Zmień identyfikator poświadczeń 23 tooupdate wiersz w wystąpieniu Wpięć</span><span class="sxs-lookup"><span data-stu-id="1c46c-151">Change line 23 tooupdate credential ID in your Jenkins instance</span></span>

```java
withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
```

## <a name="create-jenkins-pipeline"></a><span data-ttu-id="1c46c-152">Tworzenie potoku Wpięć</span><span class="sxs-lookup"><span data-stu-id="1c46c-152">Create Jenkins pipeline</span></span>
<span data-ttu-id="1c46c-153">Otwórz Wpięć w przeglądarce sieci web, kliknij pozycję **nowy element**.</span><span class="sxs-lookup"><span data-stu-id="1c46c-153">Open Jenkins in a web browser, click **New Item**.</span></span> 

* <span data-ttu-id="1c46c-154">Podaj nazwę zadania hello i wybierz **potoku**.</span><span class="sxs-lookup"><span data-stu-id="1c46c-154">Provide a name for hello job and select **Pipeline**.</span></span> <span data-ttu-id="1c46c-155">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="1c46c-155">Click **OK**.</span></span>
* <span data-ttu-id="1c46c-156">Kliknij przycisk hello **potoku** karcie dalej.</span><span class="sxs-lookup"><span data-stu-id="1c46c-156">Click hello **Pipeline** tab next.</span></span> 
* <span data-ttu-id="1c46c-157">Dla **definicji**, wybierz pozycję **potoku skryptu z SCM**.</span><span class="sxs-lookup"><span data-stu-id="1c46c-157">For **Definition**, select **Pipeline script from SCM**.</span></span>
* <span data-ttu-id="1c46c-158">Aby uzyskać **SCM**, wybierz pozycję **Git**.</span><span class="sxs-lookup"><span data-stu-id="1c46c-158">For **SCM**, select **Git**.</span></span>
* <span data-ttu-id="1c46c-159">Wprowadź hello GitHub adres URL dla Twojego repozytorium rozwidlonych: https:\<Twojego repozytorium rozwidlonych\>.git</span><span class="sxs-lookup"><span data-stu-id="1c46c-159">Enter hello GitHub URL for your forked repo: https:\<your forked repo\>.git</span></span>
* <span data-ttu-id="1c46c-160">Kliknij przycisk **Zapisz**</span><span class="sxs-lookup"><span data-stu-id="1c46c-160">Click **Save**</span></span>

## <a name="test-your-pipeline"></a><span data-ttu-id="1c46c-161">Testowanie potoku sieci</span><span class="sxs-lookup"><span data-stu-id="1c46c-161">Test your pipeline</span></span>
* <span data-ttu-id="1c46c-162">Przejdź toohello potok został utworzony, kliknij przycisk **kompilacji teraz**</span><span class="sxs-lookup"><span data-stu-id="1c46c-162">Go toohello pipeline you created, click **Build Now**</span></span>
* <span data-ttu-id="1c46c-163">Kompilacja ma być pomyślnie wykonane w ciągu kilku sekund i można go toohello kompilacji i kliknij przycisk **dane wyjściowe konsoli** toosee hello szczegóły</span><span class="sxs-lookup"><span data-stu-id="1c46c-163">A build should succeed in a few seconds, and you can go toohello build and click **Console Output** toosee hello details</span></span>

## <a name="verify-your-web-app"></a><span data-ttu-id="1c46c-164">Sprawdź aplikację sieci web</span><span class="sxs-lookup"><span data-stu-id="1c46c-164">Verify your web app</span></span>
<span data-ttu-id="1c46c-165">plik WAR hello tooverify został wdrożony pomyślnie tooyour aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="1c46c-165">tooverify hello WAR file is deployed successfully tooyour web app.</span></span> <span data-ttu-id="1c46c-166">Otwórz przeglądarkę sieci web:</span><span class="sxs-lookup"><span data-stu-id="1c46c-166">Open a web browser:</span></span>

* <span data-ttu-id="1c46c-167">Przejdź toohttp: / /&lt;nazwa_aplikacji >.azurewebsites.net/api/calculator/ping</span><span class="sxs-lookup"><span data-stu-id="1c46c-167">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/ping</span></span>  
<span data-ttu-id="1c46c-168">Zobacz:</span><span class="sxs-lookup"><span data-stu-id="1c46c-168">You see:</span></span>

        Welcome tooJava Web App!!! This is updated!
        Sun Jun 17 16:39:10 UTC 2017

* <span data-ttu-id="1c46c-169">Przejdź toohttp: / /&lt;nazwa_aplikacji >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (Zastąp &lt;x > i &lt;y > z dowolnej liczby) tooget hello sumę x i y</span><span class="sxs-lookup"><span data-stu-id="1c46c-169">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) tooget hello sum of x and y</span></span>

![Kalkulator: Dodaj](./media/execute-cli-jenkins-pipeline/calculator-add.png)

## <a name="deploy-tooazure-web-app-on-linux"></a><span data-ttu-id="1c46c-171">Wdrażanie tooAzure aplikacji sieci Web w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="1c46c-171">Deploy tooAzure Web App on Linux</span></span>
<span data-ttu-id="1c46c-172">Teraz, gdy wiesz, jak toouse wiersza polecenia platformy Azure w sieci Wpięć potoku, można zmodyfikować hello skryptu toodeploy tooan aplikacji sieci Web platformy Azure w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="1c46c-172">Now that you know how toouse Azure CLI in your Jenkins pipeline, you can modify hello script toodeploy tooan Azure Web App on Linux.</span></span>

<span data-ttu-id="1c46c-173">Aplikacji w systemie Linux sieci Web obsługuje wdrożenia hello toodo inny sposób, który jest toouse Docker.</span><span class="sxs-lookup"><span data-stu-id="1c46c-173">Web App on Linux supports a different way toodo hello deployment, which is toouse Docker.</span></span> <span data-ttu-id="1c46c-174">toodeploy, należy tooprovide plik Dockerfile, które pakiety aplikacji sieci web za pomocą usługi czasu wykonywania w obrazie Docker.</span><span class="sxs-lookup"><span data-stu-id="1c46c-174">toodeploy, you need tooprovide a Dockerfile that packages your web app with service runtime into a Docker image.</span></span> <span data-ttu-id="1c46c-175">Dodatek Hello następnie utworzyć obraz powitania, wypchnąć go tooa Docker rejestru i wdrażanie aplikacji sieci web tooyour obraz powitania.</span><span class="sxs-lookup"><span data-stu-id="1c46c-175">hello plugin will then build hello image, push it tooa Docker registry and deploy hello image tooyour web app.</span></span>

* <span data-ttu-id="1c46c-176">Wykonaj kroki hello [tutaj](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate jako aplikacji sieci Web Azure z systemem Linux.</span><span class="sxs-lookup"><span data-stu-id="1c46c-176">Follow hello steps [here](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate an Azure Web App running on Linux.</span></span>
* <span data-ttu-id="1c46c-177">Zainstaluj Docker na wystąpienie Wpięć, wykonując instrukcje hello na tym [artykułu](https://docs.docker.com/engine/installation/linux/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="1c46c-177">Install Docker on your Jenkins instance by following hello instructions in this [article](https://docs.docker.com/engine/installation/linux/ubuntu/).</span></span>
* <span data-ttu-id="1c46c-178">Tworzenie rejestru kontenera w hello portalu Azure za pomocą kroków hello [tutaj](/azure/container-registry/container-registry-get-started-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="1c46c-178">Create a Container Registry in hello Azure portal by using hello steps [here](/azure/container-registry/container-registry-get-started-azure-cli).</span></span>
* <span data-ttu-id="1c46c-179">W hello sam [prostej aplikacji sieci Web Java na platformie Azure](https://github.com/azure-devops/javawebappsample) repozytorium rozwidlone, Edytuj hello **Jenkinsfile2** pliku:</span><span class="sxs-lookup"><span data-stu-id="1c46c-179">In hello same [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) repo you forked, edit hello **Jenkinsfile2** file:</span></span>
    * <span data-ttu-id="1c46c-180">Wiersz 18-21, odpowiednio zaktualizować toohello nazwy grupy zasobów, aplikacji sieci web i ACR.</span><span class="sxs-lookup"><span data-stu-id="1c46c-180">Line 18-21, update toohello names of your resource group, web app, and ACR respectively.</span></span> 
        ```
        def webAppResourceGroup = '<myResourceGroup>'
        def webAppName = '<app_name>'
        def acrName = '<myRegistry>'
        ```

    * <span data-ttu-id="1c46c-181">Wiersz 24, aktualizacja \<azsrvprincipal\> tooyour identyfikator poświadczeń</span><span class="sxs-lookup"><span data-stu-id="1c46c-181">Line 24, update \<azsrvprincipal\> tooyour credential ID</span></span>
        ```
        withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
        ```

* <span data-ttu-id="1c46c-182">Utwórz nowy potok Wpięć tak samo jak w przypadku wdrażania aplikacji sieci web tooAzure w systemie Windows, ten czas, użyj **Jenkinsfile2** zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="1c46c-182">Create a new Jenkins pipeline as you did when deploying tooAzure web app in Windows, only this time, use **Jenkinsfile2** instead.</span></span>
* <span data-ttu-id="1c46c-183">Uruchom nowe zadanie.</span><span class="sxs-lookup"><span data-stu-id="1c46c-183">Run your new job.</span></span>
* <span data-ttu-id="1c46c-184">tooverify w wiersza polecenia platformy Azure, uruchom:</span><span class="sxs-lookup"><span data-stu-id="1c46c-184">tooverify, in Azure CLI, run:</span></span>

    ```
    az acr repository list -n <myRegistry> -o json
    ```

    <span data-ttu-id="1c46c-185">Możesz uzyskać hello następujące wyniki:</span><span class="sxs-lookup"><span data-stu-id="1c46c-185">You get hello following result:</span></span>
    
    ```
    [
    "calculator"
    ]
    ```
    
    <span data-ttu-id="1c46c-186">Przejdź toohttp: / /&lt;nazwa_aplikacji >.azurewebsites.net/api/calculator/ping.</span><span class="sxs-lookup"><span data-stu-id="1c46c-186">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/ping.</span></span> <span data-ttu-id="1c46c-187">Zostanie wyświetlony komunikat hello:</span><span class="sxs-lookup"><span data-stu-id="1c46c-187">You see hello message:</span></span> 
    
        Welcome tooJava Web App!!! This is updated!
        Sun Jul 09 16:39:10 UTC 2017

    <span data-ttu-id="1c46c-188">Przejdź toohttp: / /&lt;nazwa_aplikacji >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (Zastąp &lt;x > i &lt;y > z dowolnej liczby) tooget hello sumę x i y</span><span class="sxs-lookup"><span data-stu-id="1c46c-188">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) tooget hello sum of x and y</span></span>
    
## <a name="next-steps"></a><span data-ttu-id="1c46c-189">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1c46c-189">Next steps</span></span>
<span data-ttu-id="1c46c-190">W tym samouczku należy skonfigurować Wpięć potok, który umożliwia wyewidencjonowanie hello kodu źródłowego w repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="1c46c-190">In this tutorial, you configured a Jenkins pipeline that checks out hello source code in GitHub repo.</span></span> <span data-ttu-id="1c46c-191">Uruchamia Maven toobuild plik war, a następnie używa tooAzure toodeploy interfejsu wiersza polecenia Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="1c46c-191">Runs Maven toobuild a war file and then uses Azure CLI toodeploy tooAzure App Service.</span></span> <span data-ttu-id="1c46c-192">W tym samouczku omówiono:</span><span class="sxs-lookup"><span data-stu-id="1c46c-192">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1c46c-193">Tworzenie maszyny Wirtualnej z Wpięć</span><span class="sxs-lookup"><span data-stu-id="1c46c-193">Create a Jenkins VM</span></span>
> * <span data-ttu-id="1c46c-194">Skonfiguruj Wpięć</span><span class="sxs-lookup"><span data-stu-id="1c46c-194">Configure Jenkins</span></span>
> * <span data-ttu-id="1c46c-195">Tworzenie aplikacji sieci web na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="1c46c-195">Create a web app in Azure</span></span>
> * <span data-ttu-id="1c46c-196">Przygotowanie repozytorium GitHub</span><span class="sxs-lookup"><span data-stu-id="1c46c-196">Prepare a GitHub repository</span></span>
> * <span data-ttu-id="1c46c-197">Tworzenie potoku Wpięć</span><span class="sxs-lookup"><span data-stu-id="1c46c-197">Create Jenkins pipeline</span></span>
> * <span data-ttu-id="1c46c-198">Należy uruchomić potoku hello i sprawdzić hello aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="1c46c-198">Run hello pipeline and verify hello web app</span></span>
