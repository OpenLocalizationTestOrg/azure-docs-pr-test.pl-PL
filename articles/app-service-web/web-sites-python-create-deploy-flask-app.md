---
title: aplikacje sieci web aaaCreating z Flask na platformie Azure
description: "Samouczek przedstawiający toorunning Python aplikacji sieci web na platformie Azure."
services: app-service\web
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: b7f4ca3a-0b52-4108-90a7-f7e07ac73da0
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/20/2016
ms.author: huvalo
ms.openlocfilehash: 3362047b3106b4380b5971e47cbd8042d38a792b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-web-apps-with-flask-in-azure"></a><span data-ttu-id="f18a5-103">Tworzenie aplikacji sieci web za pomocą platformy Flask na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="f18a5-103">Creating web apps with Flask in Azure</span></span>
<span data-ttu-id="f18a5-104">W tym samouczku opisano, jak tooget uruchomienia Python [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="f18a5-104">This tutorial describes how tooget started running Python in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>  <span data-ttu-id="f18a5-105">Usługa Web Apps zapewnia ograniczony bezpłatny hosting i szybkie wdrażanie, a także możliwość korzystania z języka Python.</span><span class="sxs-lookup"><span data-stu-id="f18a5-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span>  <span data-ttu-id="f18a5-106">Rozwoju aplikacji, możesz przełączyć toopaid hosting lub można również zintegrować z wszystkimi hello innymi usługami Azure.</span><span class="sxs-lookup"><span data-stu-id="f18a5-106">As your app grows, you can switch toopaid hosting, and you can also integrate with all of hello other Azure services.</span></span>

<span data-ttu-id="f18a5-107">Utworzysz aplikację przy użyciu platformy sieci web platformy Flask hello (zobacz alternatywne wersje tego samouczka dla [Django](web-sites-python-create-deploy-django-app.md) i [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span><span class="sxs-lookup"><span data-stu-id="f18a5-107">You will create an application using hello Flask web framework (see alternate versions of this tutorial for [Django](web-sites-python-create-deploy-django-app.md) and [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span></span>  <span data-ttu-id="f18a5-108">Utworzysz hello witryny sieci Web z hello galerii Azure, skonfigurujesz wdrożenie systemu Git i klonowania repozytorium hello lokalnie.</span><span class="sxs-lookup"><span data-stu-id="f18a5-108">You will create hello website from hello Azure gallery, set up Git deployment, and clone hello repository locally.</span></span>  <span data-ttu-id="f18a5-109">Następnie uruchomisz aplikacji hello lokalnie, wprowadzić zmiany, zatwierdzenia i wypychanie ich tooAzure.</span><span class="sxs-lookup"><span data-stu-id="f18a5-109">Then you will run hello application locally, make changes, commit and push them tooAzure.</span></span>  <span data-ttu-id="f18a5-110">Witaj samouczku przedstawiono sposób toodo od systemu Windows lub Mac/Linux.</span><span class="sxs-lookup"><span data-stu-id="f18a5-110">hello tutorial shows how toodo this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="f18a5-111">Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="f18a5-111">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="f18a5-112">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="f18a5-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="f18a5-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f18a5-113">Prerequisites</span></span>
* <span data-ttu-id="f18a5-114">System Windows, Mac lub Linux</span><span class="sxs-lookup"><span data-stu-id="f18a5-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="f18a5-115">Środowisko Python w wersji 2.7 lub 3.4</span><span class="sxs-lookup"><span data-stu-id="f18a5-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="f18a5-116">Narzędzia setuptools pip, virtualenv (tylko środowisko Python 2.7)</span><span class="sxs-lookup"><span data-stu-id="f18a5-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="f18a5-117">Usługa Git</span><span class="sxs-lookup"><span data-stu-id="f18a5-117">Git</span></span>
* <span data-ttu-id="f18a5-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) — uwaga: ten składnik jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="f18a5-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="f18a5-119">**Uwaga**: publikowanie TFS nie jest obecnie obsługiwane dla projektów języka Python.</span><span class="sxs-lookup"><span data-stu-id="f18a5-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="f18a5-120">Windows</span><span class="sxs-lookup"><span data-stu-id="f18a5-120">Windows</span></span>
<span data-ttu-id="f18a5-121">Jeśli środowisko Python 2.7 lub 3.4 (32-bitowe) nie zostało jeszcze zainstalowane, zalecane jest zainstalowanie [Zestaw Azure SDK dla języka Python w wersji 2.7] lub [zestawu Azure SDK dla języka Python 3.4] przy użyciu Instalatora platformy sieci Web.</span><span class="sxs-lookup"><span data-stu-id="f18a5-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span>  <span data-ttu-id="f18a5-122">Spowoduje to zainstalowanie hello 32-bitowej wersji języka Python, narzędzi setuptools, pip, virtualenv itp (32-bitowe środowisko Python jest zainstalowanych na maszynach hostów Azure hello).</span><span class="sxs-lookup"><span data-stu-id="f18a5-122">This installs hello 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on hello Azure host machines).</span></span>  <span data-ttu-id="f18a5-123">Możesz również pobrać środowisko Python z witryny [python.org].</span><span class="sxs-lookup"><span data-stu-id="f18a5-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="f18a5-124">W przypadku systemu Git zalecane jest narzędzie [Git dla systemu Windows] lub [Github dla systemu Windows].</span><span class="sxs-lookup"><span data-stu-id="f18a5-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span>  <span data-ttu-id="f18a5-125">Jeśli używasz programu Visual Studio, używając hello zintegrowanej obsługi systemu Git.</span><span class="sxs-lookup"><span data-stu-id="f18a5-125">If you use Visual Studio, you can use hello integrated Git support.</span></span>

<span data-ttu-id="f18a5-126">Zalecane jest również zainstalowanie narzędzi [Python Tools 2.2 for Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="f18a5-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span>  <span data-ttu-id="f18a5-127">Ten krok jest opcjonalny, ale jeśli masz [programu Visual Studio], włączając hello wolne Visual Studio Community 2013 lub Visual Studio Express 2013 for Web, a następnie zapewni to doskonały IDE języka Python.</span><span class="sxs-lookup"><span data-stu-id="f18a5-127">This is optional, but if you have [Visual Studio], including hello free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="f18a5-128">System Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="f18a5-128">Mac/Linux</span></span>
<span data-ttu-id="f18a5-129">Środowisko Python i system Git powinny być już zainstalowane, ale upewnij się, że masz środowisko Python 2.7 lub 3.4.</span><span class="sxs-lookup"><span data-stu-id="f18a5-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-create-on-hello-azure-portal"></a><span data-ttu-id="f18a5-130">Tworzenie aplikacji sieci Web na powitania portalu Azure</span><span class="sxs-lookup"><span data-stu-id="f18a5-130">Web app create on hello Azure Portal</span></span>
<span data-ttu-id="f18a5-131">Witaj pierwszym krokiem tworzenia aplikacji jest toocreate hello aplikacja sieci web za pośrednictwem hello [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f18a5-131">hello first step in creating your app is toocreate hello web app via hello [Azure Portal](https://portal.azure.com).</span></span> 

1. <span data-ttu-id="f18a5-132">Zaloguj się do hello portalu Azure i kliknij przycisk hello **nowy** przycisku na powitania lewym dolnym rogu.</span><span class="sxs-lookup"><span data-stu-id="f18a5-132">Log into hello Azure Portal and click hello **NEW** button in hello bottom left corner.</span></span> 
2. <span data-ttu-id="f18a5-133">Kliknij pozycję **Sieci Web i mobilność**.</span><span class="sxs-lookup"><span data-stu-id="f18a5-133">Click **Web + Mobile**.</span></span>
3. <span data-ttu-id="f18a5-134">W polu wyszukiwania hello wpisz "python".</span><span class="sxs-lookup"><span data-stu-id="f18a5-134">In hello search box, type "python".</span></span>
4. <span data-ttu-id="f18a5-135">W wynikach wyszukiwania hello, wybierz **Flask**, następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="f18a5-135">In hello search results, select **Flask**, then click **Create**.</span></span>
5. <span data-ttu-id="f18a5-136">Skonfiguruj hello nowej Flask aplikacji, takich jak tworzenie nowego planu usługi App Service i nowej grupy zasobów dla niego.</span><span class="sxs-lookup"><span data-stu-id="f18a5-136">Configure hello new Flask app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="f18a5-137">Następnie kliknij pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="f18a5-137">Then, click **Create**.</span></span>
6. <span data-ttu-id="f18a5-138">Konfigurowanie publikowania Git dla aplikacji sieci web nowo utworzony wykonując instrukcje hello [tooAzure lokalnego wdrożenia Git usługi aplikacji](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="f18a5-138">Configure Git publishing for your newly created web app by following hello instructions at [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="f18a5-139">Omówienie aplikacji</span><span class="sxs-lookup"><span data-stu-id="f18a5-139">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="f18a5-140">Zawartość repozytorium Git</span><span class="sxs-lookup"><span data-stu-id="f18a5-140">Git repository contents</span></span>
<span data-ttu-id="f18a5-141">Poniżej przedstawiono omówienie hello plików, które znajdują się w początkowym repozytorium Git hello, które sklonujemy w następnej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="f18a5-141">Here's an overview of hello files you'll find in hello initial Git repository, which we'll clone in hello next section.</span></span>

    \FlaskWebProject\__init__.py
    \FlaskWebProject\views.py
    \FlaskWebProject\static\content\
    \FlaskWebProject\static\fonts\
    \FlaskWebProject\static\scripts\
    \FlaskWebProject\templates\about.html
    \FlaskWebProject\templates\contact.html
    \FlaskWebProject\templates\index.html
    \FlaskWebProject\templates\layout.html

<span data-ttu-id="f18a5-142">Główne źródła dla aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="f18a5-142">Main sources for hello application.</span></span>  <span data-ttu-id="f18a5-143">Składa się z 3 stron (indeks, informacje, kontakt) z układem głównym.</span><span class="sxs-lookup"><span data-stu-id="f18a5-143">Consists of 3 pages (index, about, contact) with a master layout.</span></span>  <span data-ttu-id="f18a5-144">Zawartość statyczna i skrypty obejmują bootstrap, jquery, modernizr i respond.</span><span class="sxs-lookup"><span data-stu-id="f18a5-144">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \runserver.py

<span data-ttu-id="f18a5-145">Lokalne działania projektowe obsługi serwera.</span><span class="sxs-lookup"><span data-stu-id="f18a5-145">Local development server support.</span></span> <span data-ttu-id="f18a5-146">Za pomocą tej aplikacji hello toorun lokalnie.</span><span class="sxs-lookup"><span data-stu-id="f18a5-146">Use this toorun hello application locally.</span></span>

    \FlaskWebProject.pyproj
    \FlaskWebProject.sln

<span data-ttu-id="f18a5-147">Pliki projektu do użycia z narzędziami [Python Tools for Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="f18a5-147">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="f18a5-148">Serwer proxy usług IIS dla środowisk wirtualnych i obsługa zdalnego debugowania narzędzi PTVS.</span><span class="sxs-lookup"><span data-stu-id="f18a5-148">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="f18a5-149">Pakiety zewnętrzne wymagane przez tę aplikację.</span><span class="sxs-lookup"><span data-stu-id="f18a5-149">External packages needed by this application.</span></span> <span data-ttu-id="f18a5-150">skrypt wdrożenia Hello będzie narzędzia pip instalowanie pakietów hello wymienione w tym pliku.</span><span class="sxs-lookup"><span data-stu-id="f18a5-150">hello deployment script will pip install hello packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="f18a5-151">Pliki konfiguracji programu IIS.</span><span class="sxs-lookup"><span data-stu-id="f18a5-151">IIS configuration files.</span></span>  <span data-ttu-id="f18a5-152">skrypt wdrożenia Hello Użyj hello odpowiedniego pliku web.x.y.config i skopiuje go jako plik web.config.</span><span class="sxs-lookup"><span data-stu-id="f18a5-152">hello deployment script will use hello appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="f18a5-153">Pliki opcjonalne — dostosowywanie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="f18a5-153">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="f18a5-154">Pliki opcjonalne — środowisko uruchomieniowe języka Python</span><span class="sxs-lookup"><span data-stu-id="f18a5-154">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="f18a5-155">Dodatkowe pliki na serwerze</span><span class="sxs-lookup"><span data-stu-id="f18a5-155">Additional files on server</span></span>
<span data-ttu-id="f18a5-156">Niektóre pliki na powitania serwera istnieje, ale nie są dodawane toohello repozytorium git.</span><span class="sxs-lookup"><span data-stu-id="f18a5-156">Some files exist on hello server but are not added toohello git repository.</span></span>  <span data-ttu-id="f18a5-157">Są one tworzone przez skrypt wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="f18a5-157">These are created by hello deployment script.</span></span>

    \web.config

<span data-ttu-id="f18a5-158">Plik konfiguracji programu IIS.</span><span class="sxs-lookup"><span data-stu-id="f18a5-158">IIS configuration file.</span></span>  <span data-ttu-id="f18a5-159">Tworzony na podstawie pliku web.x.y.config przy każdym wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="f18a5-159">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="f18a5-160">Środowisko wirtualne języka Python.</span><span class="sxs-lookup"><span data-stu-id="f18a5-160">Python virtual environment.</span></span>  <span data-ttu-id="f18a5-161">Jeśli zgodne środowisko wirtualne już nie istnieje w aplikacji hello i utworzyć podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="f18a5-161">Created during deployment if a compatible virtual environment doesn't already exist on hello app.</span></span>  <span data-ttu-id="f18a5-162">Pakiety wymienione w pliku requirements.txt są zainstalowane narzędzia pip, ale narzędzie pip pomija instalację, jeśli hello pakiety są już zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="f18a5-162">Packages listed in requirements.txt are pip installed, but pip will skip installation if hello packages are already installed.</span></span>

<span data-ttu-id="f18a5-163">Witaj 3 następnych sekcjach opisano sposób tworzenia aplikacji w 3 różnych środowiskach sieci web na tooproceed z hello:</span><span class="sxs-lookup"><span data-stu-id="f18a5-163">hello next 3 sections describe how tooproceed with hello web app development under 3 different environments:</span></span>

* <span data-ttu-id="f18a5-164">System Windows — przy użyciu narzędzi Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f18a5-164">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="f18a5-165">System Windows — przy użyciu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="f18a5-165">Windows, with command line</span></span>
* <span data-ttu-id="f18a5-166">System Mac/Linux — przy użyciu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="f18a5-166">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="f18a5-167">Wdrażanie aplikacji sieci Web — system Windows — narzędzia Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f18a5-167">Web app development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="f18a5-168">Klonowanie repozytorium hello</span><span class="sxs-lookup"><span data-stu-id="f18a5-168">Clone hello repository</span></span>
<span data-ttu-id="f18a5-169">Najpierw sklonuj repozytorium hello przy użyciu adresu URL hello na powitania portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f18a5-169">First, clone hello repository using hello URL provided on hello Azure Portal.</span></span> <span data-ttu-id="f18a5-170">Aby uzyskać więcej informacji, zobacz [tooAzure lokalnego wdrożenia Git usługi aplikacji](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="f18a5-170">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="f18a5-171">Otwórz plik rozwiązania hello (.sln), który znajduje się w katalogu głównego repozytorium hello hello.</span><span class="sxs-lookup"><span data-stu-id="f18a5-171">Open hello solution file (.sln) that is included in hello root of hello repository.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-solution-flask.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="f18a5-172">Tworzenie środowiska wirtualnego</span><span class="sxs-lookup"><span data-stu-id="f18a5-172">Create virtual environment</span></span>
<span data-ttu-id="f18a5-173">Teraz utwórz środowisko wirtualne dla wdrożenia lokalnego.</span><span class="sxs-lookup"><span data-stu-id="f18a5-173">Now we'll create a virtual environment for local development.</span></span>  <span data-ttu-id="f18a5-174">Kliknij prawym przyciskiem myszy pozycję **Środowiska Python** i wybierz pozycję **Dodaj środowisko wirtualne**.</span><span class="sxs-lookup"><span data-stu-id="f18a5-174">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="f18a5-175">Upewnij się, że nazwa hello środowiska hello jest `env`.</span><span class="sxs-lookup"><span data-stu-id="f18a5-175">Make sure hello name of hello environment is `env`.</span></span>
* <span data-ttu-id="f18a5-176">Wybierz interpreter podstawowy hello.</span><span class="sxs-lookup"><span data-stu-id="f18a5-176">Select hello base interpreter.</span></span>  <span data-ttu-id="f18a5-177">Upewnij się, że toouse hello sama wersja środowiska Python, którą wybrano dla aplikacji sieci web (w pliku runtime.txt lub hello **ustawienia aplikacji** bloku aplikacji sieci web w portalu Azure hello).</span><span class="sxs-lookup"><span data-stu-id="f18a5-177">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello **Application Settings** blade of your web app in hello Azure Portal).</span></span>
* <span data-ttu-id="f18a5-178">Upewnij się, zaznaczono opcję hello toodownload i zainstaluj pakiety.</span><span class="sxs-lookup"><span data-stu-id="f18a5-178">Make sure hello option toodownload and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="f18a5-179">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="f18a5-179">Click **Create**.</span></span>  <span data-ttu-id="f18a5-180">Spowoduje to utworzenie środowiska wirtualnego hello i zainstalowanie składników zależnych wymienionych w pliku requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="f18a5-180">This will create hello virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="f18a5-181">Uruchamianie przy użyciu serwera projektowego</span><span class="sxs-lookup"><span data-stu-id="f18a5-181">Run using development server</span></span>
<span data-ttu-id="f18a5-182">Naciśnij klawisz F5 toostart debugowania i przeglądarki sieci web zostanie otwarty toohello strony uruchomionej lokalnie.</span><span class="sxs-lookup"><span data-stu-id="f18a5-182">Press F5 toostart debugging, and your web browser will open automatically toohello page running locally.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

<span data-ttu-id="f18a5-183">Można ustawić punktów przerwania w hello źródeł, użyj hello czujki systemu windows itd.  Zobacz hello [narzędzi Python Tools for Visual Studio dokumentacji] Aby uzyskać więcej informacji na temat hello różnych funkcji.</span><span class="sxs-lookup"><span data-stu-id="f18a5-183">You can set breakpoints in hello sources, use hello watch windows, etc.  See hello [Python Tools for Visual Studio Documentation] for more information on hello various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="f18a5-184">Wprowadzanie zmian</span><span class="sxs-lookup"><span data-stu-id="f18a5-184">Make changes</span></span>
<span data-ttu-id="f18a5-185">Teraz możesz eksperymentować, wprowadzając zmiany toohello aplikacji źródeł i/lub szablonach.</span><span class="sxs-lookup"><span data-stu-id="f18a5-185">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="f18a5-186">Po przetestowaniu zmiany je zatwierdzić toohello repozytorium Git:</span><span class="sxs-lookup"><span data-stu-id="f18a5-186">After you've tested your changes, commit them toohello Git repository:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-commit-flask.png)

### <a name="install-more-packages"></a><span data-ttu-id="f18a5-187">Instalowanie dodatkowych pakietów</span><span class="sxs-lookup"><span data-stu-id="f18a5-187">Install more packages</span></span>
<span data-ttu-id="f18a5-188">Aplikacja może mieć zależności poza środowiskiem Python i platformy Flask.</span><span class="sxs-lookup"><span data-stu-id="f18a5-188">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="f18a5-189">Możesz zainstalować dodatkowe pakiety przy użyciu narzędzia pip.</span><span class="sxs-lookup"><span data-stu-id="f18a5-189">You can install additional packages using pip.</span></span>  <span data-ttu-id="f18a5-190">tooinstall pakiet, kliknij prawym przyciskiem myszy na powitania środowisko wirtualne i wybierz **zainstaluj pakiet języka Python**.</span><span class="sxs-lookup"><span data-stu-id="f18a5-190">tooinstall a package, right-click on hello virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="f18a5-191">Na przykład tooinstall hello Azure SDK dla języka Python, który zapewnia dostęp tooAzure magazynu, usługi service bus i innymi usługami Azure, wprowadź `azure`:</span><span class="sxs-lookup"><span data-stu-id="f18a5-191">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-install-package-dialog.png)

<span data-ttu-id="f18a5-192">Kliknij prawym przyciskiem myszy na powitania środowiska wirtualnego, a następnie wybierz **Generuj plik requirements.txt** tooupdate requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="f18a5-192">Right-click on hello virtual environment and select **Generate requirements.txt** tooupdate requirements.txt.</span></span>

<span data-ttu-id="f18a5-193">Następnie Zatwierdź repozytorium Git toohello toorequirements.txt zmiany hello.</span><span class="sxs-lookup"><span data-stu-id="f18a5-193">Then, commit hello changes toorequirements.txt toohello Git repository.</span></span>

### <a name="deploy-tooazure"></a><span data-ttu-id="f18a5-194">Wdrażanie tooAzure</span><span class="sxs-lookup"><span data-stu-id="f18a5-194">Deploy tooAzure</span></span>
<span data-ttu-id="f18a5-195">polecenie tootrigger wdrożenia, **synchronizacji** lub **Push**.</span><span class="sxs-lookup"><span data-stu-id="f18a5-195">tootrigger a deployment, click on **Sync** or **Push**.</span></span>  <span data-ttu-id="f18a5-196">Synchronizacja obejmuje zarówno wypychanie, jak i ściąganie.</span><span class="sxs-lookup"><span data-stu-id="f18a5-196">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-git-push.png)

<span data-ttu-id="f18a5-197">pierwszym wdrożeniu Hello wymaga czasu, ponieważ obejmuje tworzenie środowiska wirtualnego, instalowanie pakietów itp.</span><span class="sxs-lookup"><span data-stu-id="f18a5-197">hello first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="f18a5-198">Program Visual Studio nie wyświetla postęp hello hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="f18a5-198">Visual Studio doesn't show hello progress of hello deployment.</span></span>  <span data-ttu-id="f18a5-199">Jeśli chcesz tooreview hello w danych wyjściowych, zobacz sekcję hello na [Rozwiązywanie problemów — wdrożenie](#troubleshooting-deployment).</span><span class="sxs-lookup"><span data-stu-id="f18a5-199">If you'd like tooreview hello output, see hello section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="f18a5-200">Przeglądaj zmiany toohello tooview adresu URL platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f18a5-200">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="f18a5-201">Wdrażanie aplikacji sieci Web — system Windows — wiersz polecenia</span><span class="sxs-lookup"><span data-stu-id="f18a5-201">Web app development - Windows - command line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="f18a5-202">Klonowanie repozytorium hello</span><span class="sxs-lookup"><span data-stu-id="f18a5-202">Clone hello repository</span></span>
<span data-ttu-id="f18a5-203">Najpierw sklonować repozytorium hello przy użyciu adresu URL hello na powitania portalu Azure i dodać hello repozytorium Azure jako zdalnej.</span><span class="sxs-lookup"><span data-stu-id="f18a5-203">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="f18a5-204">Aby uzyskać więcej informacji, zobacz [tooAzure lokalnego wdrożenia Git usługi aplikacji](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="f18a5-204">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="f18a5-205">Tworzenie środowiska wirtualnego</span><span class="sxs-lookup"><span data-stu-id="f18a5-205">Create virtual environment</span></span>
<span data-ttu-id="f18a5-206">Utworzymy nowe środowisko wirtualne dla celów programistycznych (nie należy dodawać go toohello repozytorium).</span><span class="sxs-lookup"><span data-stu-id="f18a5-206">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span>  <span data-ttu-id="f18a5-207">Wirtualnych środowisk języka Python nie są można zmieniać lokalizacji, dlatego każdy Deweloper pracujący nad aplikacji hello tworzy własne środowisko lokalnie.</span><span class="sxs-lookup"><span data-stu-id="f18a5-207">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="f18a5-208">Upewnij się, że toouse hello sama wersja środowiska Python, którą wybrano dla aplikacji sieci web (w pliku runtime.txt lub hello **ustawienia aplikacji** bloku aplikacji sieci web w portalu Azure hello).</span><span class="sxs-lookup"><span data-stu-id="f18a5-208">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello **Application Settings** blade of your web app in hello Azure Portal).</span></span>

<span data-ttu-id="f18a5-209">Dla środowiska Python w wersji 2.7:</span><span class="sxs-lookup"><span data-stu-id="f18a5-209">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="f18a5-210">Dla środowiska Python w wersji 3.4:</span><span class="sxs-lookup"><span data-stu-id="f18a5-210">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="f18a5-211">Zainstaluj pakiety zewnętrzne wymagane przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="f18a5-211">Install any external packages required by your application.</span></span> <span data-ttu-id="f18a5-212">Możesz użyć pliku requirements.txt hello w głównym hello hello repozytorium tooinstall hello pakietów w środowisku wirtualnym:</span><span class="sxs-lookup"><span data-stu-id="f18a5-212">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="f18a5-213">Uruchamianie przy użyciu serwera projektowego</span><span class="sxs-lookup"><span data-stu-id="f18a5-213">Run using development server</span></span>
<span data-ttu-id="f18a5-214">Można uruchomić aplikacji hello na serwerze projektowym z hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="f18a5-214">You can launch hello application under a development server with hello following command:</span></span>

    env\scripts\python runserver.py

<span data-ttu-id="f18a5-215">Witaj konsoli zostanie wyświetlony adres URL hello i nasłuchuje portu powitania serwera:</span><span class="sxs-lookup"><span data-stu-id="f18a5-215">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-run-local-flask.png)

<span data-ttu-id="f18a5-216">Następnie otwórz adres URL toothat przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="f18a5-216">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

### <a name="make-changes"></a><span data-ttu-id="f18a5-217">Wprowadzanie zmian</span><span class="sxs-lookup"><span data-stu-id="f18a5-217">Make changes</span></span>
<span data-ttu-id="f18a5-218">Teraz możesz eksperymentować, wprowadzając zmiany toohello aplikacji źródeł i/lub szablonach.</span><span class="sxs-lookup"><span data-stu-id="f18a5-218">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="f18a5-219">Po przetestowaniu zmiany je zatwierdzić toohello repozytorium Git:</span><span class="sxs-lookup"><span data-stu-id="f18a5-219">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="f18a5-220">Instalowanie dodatkowych pakietów</span><span class="sxs-lookup"><span data-stu-id="f18a5-220">Install more packages</span></span>
<span data-ttu-id="f18a5-221">Aplikacja może mieć zależności poza środowiskiem Python i platformy Flask.</span><span class="sxs-lookup"><span data-stu-id="f18a5-221">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="f18a5-222">Możesz zainstalować dodatkowe pakiety przy użyciu narzędzia pip.</span><span class="sxs-lookup"><span data-stu-id="f18a5-222">You can install additional packages using pip.</span></span>  <span data-ttu-id="f18a5-223">Na przykład tooinstall hello Azure SDK dla języka Python, co pozwala na dostęp do magazynu tooAzure, magistrali usług i innych usług Azure, wpisz:</span><span class="sxs-lookup"><span data-stu-id="f18a5-223">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="f18a5-224">Upewnij się, że tooupdate pliku requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="f18a5-224">Make sure tooupdate requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="f18a5-225">Zatwierdź zmiany hello:</span><span class="sxs-lookup"><span data-stu-id="f18a5-225">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="f18a5-226">Wdrażanie tooAzure</span><span class="sxs-lookup"><span data-stu-id="f18a5-226">Deploy tooAzure</span></span>
<span data-ttu-id="f18a5-227">tootrigger wdrożenia hello wypychania zmiany tooAzure:</span><span class="sxs-lookup"><span data-stu-id="f18a5-227">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="f18a5-228">Zostanie wyświetlone dane wyjściowe hello hello skryptu wdrożenia, łącznie z tworzeniem środowiska wirtualnego, instalowaniem pakietów i tworzeniem pliku web.config.</span><span class="sxs-lookup"><span data-stu-id="f18a5-228">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="f18a5-229">Przeglądaj zmiany toohello tooview adresu URL platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f18a5-229">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="f18a5-230">Wdrażanie aplikacji sieci Web — system Mac/Linux — wiersz polecenia</span><span class="sxs-lookup"><span data-stu-id="f18a5-230">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="f18a5-231">Klonowanie repozytorium hello</span><span class="sxs-lookup"><span data-stu-id="f18a5-231">Clone hello repository</span></span>
<span data-ttu-id="f18a5-232">Najpierw sklonować repozytorium hello przy użyciu adresu URL hello na powitania portalu Azure i dodać hello repozytorium Azure jako zdalnej.</span><span class="sxs-lookup"><span data-stu-id="f18a5-232">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="f18a5-233">Aby uzyskać więcej informacji, zobacz [tooAzure lokalnego wdrożenia Git usługi aplikacji](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="f18a5-233">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="f18a5-234">Tworzenie środowiska wirtualnego</span><span class="sxs-lookup"><span data-stu-id="f18a5-234">Create virtual environment</span></span>
<span data-ttu-id="f18a5-235">Utworzymy nowe środowisko wirtualne dla celów programistycznych (nie należy dodawać go toohello repozytorium).</span><span class="sxs-lookup"><span data-stu-id="f18a5-235">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span>  <span data-ttu-id="f18a5-236">Wirtualnych środowisk języka Python nie są można zmieniać lokalizacji, dlatego każdy Deweloper pracujący nad aplikacji hello tworzy własne środowisko lokalnie.</span><span class="sxs-lookup"><span data-stu-id="f18a5-236">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="f18a5-237">Upewnij się, że toouse hello sama wersja środowiska Python, którą wybrano dla aplikacji sieci web (w pliku runtime.txt lub hello **ustawienia aplikacji** bloku aplikacji sieci web w portalu Azure hello).</span><span class="sxs-lookup"><span data-stu-id="f18a5-237">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello **Application Settings** blade of your web app in hello Azure Portal).</span></span>

<span data-ttu-id="f18a5-238">Dla środowiska Python w wersji 2.7:</span><span class="sxs-lookup"><span data-stu-id="f18a5-238">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="f18a5-239">Dla środowiska Python w wersji 3.4:</span><span class="sxs-lookup"><span data-stu-id="f18a5-239">For Python 3.4:</span></span>

    python -m venv env
<span data-ttu-id="f18a5-240">lub pyvenv env</span><span class="sxs-lookup"><span data-stu-id="f18a5-240">or pyvenv env</span></span>

<span data-ttu-id="f18a5-241">Zainstaluj pakiety zewnętrzne wymagane przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="f18a5-241">Install any external packages required by your application.</span></span> <span data-ttu-id="f18a5-242">Możesz użyć pliku requirements.txt hello w głównym hello hello repozytorium tooinstall hello pakietów w środowisku wirtualnym:</span><span class="sxs-lookup"><span data-stu-id="f18a5-242">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="f18a5-243">Uruchamianie przy użyciu serwera projektowego</span><span class="sxs-lookup"><span data-stu-id="f18a5-243">Run using development server</span></span>
<span data-ttu-id="f18a5-244">Można uruchomić aplikacji hello na serwerze projektowym z hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="f18a5-244">You can launch hello application under a development server with hello following command:</span></span>

    env/bin/python runserver.py

<span data-ttu-id="f18a5-245">Witaj konsoli zostanie wyświetlony adres URL hello i nasłuchuje portu powitania serwera:</span><span class="sxs-lookup"><span data-stu-id="f18a5-245">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/mac-run-local-flask.png)

<span data-ttu-id="f18a5-246">Następnie otwórz adres URL toothat przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="f18a5-246">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/mac-browser-flask.png)

### <a name="make-changes"></a><span data-ttu-id="f18a5-247">Wprowadzanie zmian</span><span class="sxs-lookup"><span data-stu-id="f18a5-247">Make changes</span></span>
<span data-ttu-id="f18a5-248">Teraz możesz eksperymentować, wprowadzając zmiany toohello aplikacji źródeł i/lub szablonach.</span><span class="sxs-lookup"><span data-stu-id="f18a5-248">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="f18a5-249">Po przetestowaniu zmiany je zatwierdzić toohello repozytorium Git:</span><span class="sxs-lookup"><span data-stu-id="f18a5-249">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="f18a5-250">Instalowanie dodatkowych pakietów</span><span class="sxs-lookup"><span data-stu-id="f18a5-250">Install more packages</span></span>
<span data-ttu-id="f18a5-251">Aplikacja może mieć zależności poza środowiskiem Python i platformy Flask.</span><span class="sxs-lookup"><span data-stu-id="f18a5-251">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="f18a5-252">Możesz zainstalować dodatkowe pakiety przy użyciu narzędzia pip.</span><span class="sxs-lookup"><span data-stu-id="f18a5-252">You can install additional packages using pip.</span></span>  <span data-ttu-id="f18a5-253">Na przykład tooinstall hello Azure SDK dla języka Python, co pozwala na dostęp do magazynu tooAzure, magistrali usług i innych usług Azure, wpisz:</span><span class="sxs-lookup"><span data-stu-id="f18a5-253">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="f18a5-254">Upewnij się, że tooupdate pliku requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="f18a5-254">Make sure tooupdate requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="f18a5-255">Zatwierdź zmiany hello:</span><span class="sxs-lookup"><span data-stu-id="f18a5-255">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="f18a5-256">Wdrażanie tooAzure</span><span class="sxs-lookup"><span data-stu-id="f18a5-256">Deploy tooAzure</span></span>
<span data-ttu-id="f18a5-257">tootrigger wdrożenia hello wypychania zmiany tooAzure:</span><span class="sxs-lookup"><span data-stu-id="f18a5-257">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="f18a5-258">Zostanie wyświetlone dane wyjściowe hello hello skryptu wdrożenia, łącznie z tworzeniem środowiska wirtualnego, instalowaniem pakietów i tworzeniem pliku web.config.</span><span class="sxs-lookup"><span data-stu-id="f18a5-258">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="f18a5-259">Przeglądaj zmiany toohello tooview adresu URL platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f18a5-259">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="f18a5-260">Rozwiązywanie problemów — instalowanie pakietów</span><span class="sxs-lookup"><span data-stu-id="f18a5-260">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="f18a5-261">Rozwiązywanie problemów — środowisko wirtualne</span><span class="sxs-lookup"><span data-stu-id="f18a5-261">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="f18a5-262">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f18a5-262">Next Steps</span></span>
<span data-ttu-id="f18a5-263">Wykonaj te toolearn łącza więcej informacji na temat platformy Flask i narzędzi Python Tools for Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="f18a5-263">Follow these links toolearn more about Flask and Python Tools for Visual Studio:</span></span> 

* <span data-ttu-id="f18a5-264">[Dokumentacja platformy flask]</span><span class="sxs-lookup"><span data-stu-id="f18a5-264">[Flask Documentation]</span></span>
* <span data-ttu-id="f18a5-265">[narzędzi Python Tools for Visual Studio dokumentacji]</span><span class="sxs-lookup"><span data-stu-id="f18a5-265">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="f18a5-266">Aby uzyskać informacje o korzystaniu z magazynu tabel platformy Azure i bazy danych MongoDB:</span><span class="sxs-lookup"><span data-stu-id="f18a5-266">For information on using Azure Table Storage and MongoDB:</span></span>

* <span data-ttu-id="f18a5-267">[Flask i bazy danych MongoDB na platformie Azure przy użyciu narzędzi Python Tools for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="f18a5-267">[Flask and MongoDB on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="f18a5-268">[Flask i magazynu tabel platformy Azure na platformie Azure przy użyciu narzędzi Python Tools for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="f18a5-268">[Flask and Azure Table Storage on Azure with Python Tools for Visual Studio]</span></span>

<span data-ttu-id="f18a5-269">Aby uzyskać więcej informacji, zobacz też hello [Centrum deweloperów języka Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="f18a5-269">For more information, see also hello [Python Developer Center](/develop/python/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="f18a5-270">Co zostało zmienione</span><span class="sxs-lookup"><span data-stu-id="f18a5-270">What's changed</span></span>
* <span data-ttu-id="f18a5-271">Toohello przewodnik zmiany z tooApp witryn sieci Web usługi dla: [usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="f18a5-271">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Flask i bazy danych MongoDB na platformie Azure przy użyciu narzędzi Python Tools for Visual Studio]: https://github.com/microsoft/ptvs/wiki/Flask-and-MongoDB-on-Azure
[Flask i magazynu tabel platformy Azure na platformie Azure przy użyciu narzędzi Python Tools for Visual Studio]: web-sites-python-ptvs-flask-table-storage.md

<!--External Link references-->
[Zestaw Azure SDK dla języka Python w wersji 2.7]: http://go.microsoft.com/fwlink/?linkid=254281
[zestawu Azure SDK dla języka Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990
[python.org]: http://www.python.org/
[Git dla systemu Windows]: http://msysgit.github.io/
[Github dla systemu Windows]: https://windows.github.com/
[Python Tools for Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[programu Visual Studio]: http://www.visualstudio.com/
[narzędzi Python Tools for Visual Studio dokumentacji]: http://aka.ms/ptvsdocs
[Dokumentacja platformy flask]: http://flask.pocoo.org/ 

