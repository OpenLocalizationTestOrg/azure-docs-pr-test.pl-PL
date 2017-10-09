---
title: aplikacje sieci web aaaPython z Bottle na platformie Azure
description: "Samouczek przedstawiający toorunning aplikacji sieci web języka Python w aplikacjach sieci Web usługi aplikacji Azure."
services: app-service\web
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 84f043b8-9d05-479f-a9d0-d0d9a32a0bb9
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/19/2016
ms.author: huvalo
ms.openlocfilehash: 98acd7d8fcdbba326625121c20f9237d2663ea1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-web-apps-with-bottle-in-azure"></a><span data-ttu-id="d105f-103">Tworzenie aplikacji sieci web w języku Bottle na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="d105f-103">Creating web apps with Bottle in Azure</span></span>
<span data-ttu-id="d105f-104">W tym samouczku opisano, jak tooget uruchomienia Python w aplikacjach sieci Web usługi aplikacji Azure.</span><span class="sxs-lookup"><span data-stu-id="d105f-104">This tutorial describes how tooget started running Python in Azure App Service Web Apps.</span></span> <span data-ttu-id="d105f-105">Usługa Web Apps zapewnia ograniczony bezpłatny hosting i szybkie wdrażanie, a także możliwość korzystania z języka Python.</span><span class="sxs-lookup"><span data-stu-id="d105f-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span> <span data-ttu-id="d105f-106">Rozwoju aplikacji, możesz przełączyć toopaid hosting lub można również zintegrować z wszystkimi hello innymi usługami Azure.</span><span class="sxs-lookup"><span data-stu-id="d105f-106">As your app grows, you can switch toopaid hosting, and you can also integrate with all of hello other Azure services.</span></span>

<span data-ttu-id="d105f-107">Utworzysz aplikację sieci web przy użyciu platformy sieci web Bottle hello (zobacz alternatywne wersje tego samouczka dla [Django](web-sites-python-create-deploy-django-app.md) i [Flask](web-sites-python-create-deploy-flask-app.md)).</span><span class="sxs-lookup"><span data-stu-id="d105f-107">You will create a web app using hello Bottle web framework (see alternate versions of this tutorial for [Django](web-sites-python-create-deploy-django-app.md) and [Flask](web-sites-python-create-deploy-flask-app.md)).</span></span> <span data-ttu-id="d105f-108">Zostanie tworzenie aplikacji sieci web hello z hello Azure Marketplace, skonfigurujesz wdrożenie systemu Git i klonowania repozytorium hello lokalnie.</span><span class="sxs-lookup"><span data-stu-id="d105f-108">You will create hello web app from hello Azure Marketplace, set up Git deployment, and clone hello repository locally.</span></span> <span data-ttu-id="d105f-109">Następnie uruchomisz aplikację sieci web hello lokalnie, wprowadzić zmiany, zatwierdzenia i wypychanie ich zbyt[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="d105f-109">Then you will run hello web app locally, make changes, commit and push them too[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="d105f-110">Witaj samouczku przedstawiono sposób toodo od systemu Windows lub Mac/Linux.</span><span class="sxs-lookup"><span data-stu-id="d105f-110">hello tutorial shows how toodo this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="d105f-111">Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="d105f-111">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="d105f-112">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="d105f-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="d105f-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d105f-113">Prerequisites</span></span>
* <span data-ttu-id="d105f-114">System Windows, Mac lub Linux</span><span class="sxs-lookup"><span data-stu-id="d105f-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="d105f-115">Środowisko Python w wersji 2.7 lub 3.4</span><span class="sxs-lookup"><span data-stu-id="d105f-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="d105f-116">Narzędzia setuptools pip, virtualenv (tylko środowisko Python 2.7)</span><span class="sxs-lookup"><span data-stu-id="d105f-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="d105f-117">Usługa Git</span><span class="sxs-lookup"><span data-stu-id="d105f-117">Git</span></span>
* <span data-ttu-id="d105f-118">[Narzędzia Python Tools 2.2 for Visual Studio][Python Tools 2.2 for Visual Studio] (PTVS) — Uwaga: ten krok jest opcjonalny</span><span class="sxs-lookup"><span data-stu-id="d105f-118">[Python Tools 2.2 for Visual Studio][Python Tools 2.2 for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="d105f-119">**Uwaga**: publikowanie TFS nie jest obecnie obsługiwane dla projektów języka Python.</span><span class="sxs-lookup"><span data-stu-id="d105f-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="d105f-120">Windows</span><span class="sxs-lookup"><span data-stu-id="d105f-120">Windows</span></span>
<span data-ttu-id="d105f-121">Jeśli środowisko Python 2.7 lub 3.4 (32-bitowe) nie zostało jeszcze zainstalowane, zalecane jest zainstalowanie [Zestaw Azure SDK dla języka Python w wersji 2.7] lub [zestawu Azure SDK dla języka Python 3.4] przy użyciu Instalatora platformy sieci Web.</span><span class="sxs-lookup"><span data-stu-id="d105f-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span> <span data-ttu-id="d105f-122">Spowoduje to zainstalowanie hello 32-bitowej wersji języka Python, narzędzi setuptools, pip, virtualenv itp (32-bitowe środowisko Python jest zainstalowanych na maszynach hostów Azure hello).</span><span class="sxs-lookup"><span data-stu-id="d105f-122">This installs hello 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on hello Azure host machines).</span></span> <span data-ttu-id="d105f-123">Możesz również pobrać środowisko Python z witryny [python.org].</span><span class="sxs-lookup"><span data-stu-id="d105f-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="d105f-124">W przypadku systemu Git zalecane jest narzędzie [Git dla systemu Windows] lub [Github dla systemu Windows].</span><span class="sxs-lookup"><span data-stu-id="d105f-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span> <span data-ttu-id="d105f-125">Jeśli używasz programu Visual Studio, używając hello zintegrowanej obsługi systemu Git.</span><span class="sxs-lookup"><span data-stu-id="d105f-125">If you use Visual Studio, you can use hello integrated Git support.</span></span>

<span data-ttu-id="d105f-126">Zalecane jest również zainstalowanie narzędzi [Python Tools 2.2 for Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="d105f-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span> <span data-ttu-id="d105f-127">Ten krok jest opcjonalny, ale jeśli masz [programu Visual Studio], włączając hello wolne Visual Studio Community 2013 lub Visual Studio Express 2013 for Web, a następnie zapewni to doskonały IDE języka Python.</span><span class="sxs-lookup"><span data-stu-id="d105f-127">This is optional, but if you have [Visual Studio], including hello free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="d105f-128">System Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="d105f-128">Mac/Linux</span></span>
<span data-ttu-id="d105f-129">Środowisko Python i system Git powinny być już zainstalowane, ale upewnij się, że masz środowisko Python 2.7 lub 3.4.</span><span class="sxs-lookup"><span data-stu-id="d105f-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-creation-on-hello-azure-portal"></a><span data-ttu-id="d105f-130">Tworzenie aplikacji sieci Web na powitania portalu Azure</span><span class="sxs-lookup"><span data-stu-id="d105f-130">Web app creation on hello Azure Portal</span></span>
<span data-ttu-id="d105f-131">Witaj pierwszym krokiem tworzenia aplikacji jest toocreate hello aplikacja sieci web za pośrednictwem hello [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d105f-131">hello first step in creating your app is toocreate hello web app via hello [Azure Portal](https://portal.azure.com).</span></span>  

1. <span data-ttu-id="d105f-132">Zaloguj się do hello portalu Azure i kliknij przycisk hello **nowy** przycisku na powitania lewym dolnym rogu.</span><span class="sxs-lookup"><span data-stu-id="d105f-132">Log into hello Azure Portal and click hello **NEW** button in hello bottom left corner.</span></span> 
2. <span data-ttu-id="d105f-133">W polu wyszukiwania hello wpisz "python".</span><span class="sxs-lookup"><span data-stu-id="d105f-133">In hello search box, type "python".</span></span>
3. <span data-ttu-id="d105f-134">W wynikach wyszukiwania hello, wybierz **Bottle**, następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d105f-134">In hello search results, select **Bottle**, then click **Create**.</span></span>
4. <span data-ttu-id="d105f-135">Skonfiguruj hello nowej Bottle aplikacji, takich jak tworzenie nowego planu usługi App Service i nowej grupy zasobów dla niego.</span><span class="sxs-lookup"><span data-stu-id="d105f-135">Configure hello new Bottle app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="d105f-136">Następnie kliknij pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d105f-136">Then, click **Create**.</span></span>
5. <span data-ttu-id="d105f-137">Konfigurowanie publikowania Git dla aplikacji sieci web nowo utworzony wykonując instrukcje hello [tooAzure lokalnego wdrożenia Git usługi aplikacji](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="d105f-137">Configure Git publishing for your newly created web app by following hello instructions at [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="d105f-138">Omówienie aplikacji</span><span class="sxs-lookup"><span data-stu-id="d105f-138">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="d105f-139">Zawartość repozytorium Git</span><span class="sxs-lookup"><span data-stu-id="d105f-139">Git repository contents</span></span>
<span data-ttu-id="d105f-140">Poniżej przedstawiono omówienie hello plików, które znajdują się w początkowym repozytorium Git hello, które sklonujemy w następnej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="d105f-140">Here's an overview of hello files you'll find in hello initial Git repository, which we'll clone in hello next section.</span></span>

    \routes.py
    \static\content\
    \static\fonts\
    \static\scripts\
    \views\about.tpl
    \views\contact.tpl
    \views\index.tpl
    \views\layout.tpl

<span data-ttu-id="d105f-141">Główne źródła dla aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="d105f-141">Main sources for hello application.</span></span> <span data-ttu-id="d105f-142">Składa się z 3 stron (indeks, informacje, kontakt) z układem głównym.</span><span class="sxs-lookup"><span data-stu-id="d105f-142">Consists of 3 pages (index, about, contact) with a master layout.</span></span>  <span data-ttu-id="d105f-143">Zawartość statyczna i skrypty obejmują bootstrap, jquery, modernizr i respond.</span><span class="sxs-lookup"><span data-stu-id="d105f-143">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \app.py

<span data-ttu-id="d105f-144">Lokalne działania projektowe obsługi serwera.</span><span class="sxs-lookup"><span data-stu-id="d105f-144">Local development server support.</span></span> <span data-ttu-id="d105f-145">Za pomocą tej aplikacji hello toorun lokalnie.</span><span class="sxs-lookup"><span data-stu-id="d105f-145">Use this toorun hello application locally.</span></span>

    \BottleWebProject.pyproj
    \BottleWebProject.sln

<span data-ttu-id="d105f-146">Pliki projektu do użycia z narzędziami [Python Tools for Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="d105f-146">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="d105f-147">Serwer proxy usług IIS dla środowisk wirtualnych i obsługa zdalnego debugowania narzędzi PTVS.</span><span class="sxs-lookup"><span data-stu-id="d105f-147">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="d105f-148">Pakiety zewnętrzne wymagane przez tę aplikację.</span><span class="sxs-lookup"><span data-stu-id="d105f-148">External packages needed by this application.</span></span> <span data-ttu-id="d105f-149">skrypt wdrożenia Hello będzie narzędzia pip instalowanie pakietów hello wymienione w tym pliku.</span><span class="sxs-lookup"><span data-stu-id="d105f-149">hello deployment script will pip install hello packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="d105f-150">Pliki konfiguracji programu IIS.</span><span class="sxs-lookup"><span data-stu-id="d105f-150">IIS configuration files.</span></span> <span data-ttu-id="d105f-151">skrypt wdrożenia Hello Użyj hello odpowiedniego pliku web.x.y.config i skopiuje go jako plik web.config.</span><span class="sxs-lookup"><span data-stu-id="d105f-151">hello deployment script will use hello appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="d105f-152">Pliki opcjonalne — dostosowywanie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="d105f-152">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="d105f-153">Pliki opcjonalne — środowisko uruchomieniowe języka Python</span><span class="sxs-lookup"><span data-stu-id="d105f-153">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="d105f-154">Dodatkowe pliki na serwerze</span><span class="sxs-lookup"><span data-stu-id="d105f-154">Additional files on server</span></span>
<span data-ttu-id="d105f-155">Niektóre pliki na powitania serwera istnieje, ale nie są dodawane toohello repozytorium git.</span><span class="sxs-lookup"><span data-stu-id="d105f-155">Some files exist on hello server but are not added toohello git repository.</span></span> <span data-ttu-id="d105f-156">Są one tworzone przez skrypt wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="d105f-156">These are created by hello deployment script.</span></span>

    \web.config

<span data-ttu-id="d105f-157">Plik konfiguracji programu IIS.</span><span class="sxs-lookup"><span data-stu-id="d105f-157">IIS configuration file.</span></span> <span data-ttu-id="d105f-158">Tworzony na podstawie pliku web.x.y.config przy każdym wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="d105f-158">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="d105f-159">Środowisko wirtualne języka Python.</span><span class="sxs-lookup"><span data-stu-id="d105f-159">Python virtual environment.</span></span> <span data-ttu-id="d105f-160">Utworzonych podczas wdrażania, jeśli zgodne środowisko wirtualne już nie istnieje na powitania aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="d105f-160">Created during deployment if a compatible virtual environment doesn't already exist on hello web app.</span></span>  <span data-ttu-id="d105f-161">Pakiety wymienione w pliku requirements.txt są zainstalowane narzędzia pip, ale narzędzie pip pomija instalację, jeśli hello pakiety są już zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="d105f-161">Packages listed in requirements.txt are pip installed, but pip will skip installation if hello packages are already installed.</span></span>

<span data-ttu-id="d105f-162">Witaj 3 następnych sekcjach opisano sposób tworzenia aplikacji w 3 różnych środowiskach sieci web na tooproceed z hello:</span><span class="sxs-lookup"><span data-stu-id="d105f-162">hello next 3 sections describe how tooproceed with hello web app development under 3 different environments:</span></span>

* <span data-ttu-id="d105f-163">System Windows — przy użyciu narzędzi Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d105f-163">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="d105f-164">System Windows — przy użyciu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="d105f-164">Windows, with command line</span></span>
* <span data-ttu-id="d105f-165">System Mac/Linux — przy użyciu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="d105f-165">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="d105f-166">Sieci Web - Windows - Python narzędzia do programowania aplikacji dla programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d105f-166">Web App development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="d105f-167">Klonowanie repozytorium hello</span><span class="sxs-lookup"><span data-stu-id="d105f-167">Clone hello repository</span></span>
<span data-ttu-id="d105f-168">Najpierw sklonuj repozytorium hello przy użyciu adresu url hello na powitania portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d105f-168">First, clone hello repository using hello url provided on hello Azure Portal.</span></span> <span data-ttu-id="d105f-169">Aby uzyskać więcej informacji, zobacz [tooAzure lokalnego wdrożenia Git usługi aplikacji](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="d105f-169">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="d105f-170">Otwórz plik rozwiązania hello (.sln), który znajduje się w katalogu głównego repozytorium hello hello.</span><span class="sxs-lookup"><span data-stu-id="d105f-170">Open hello solution file (.sln) that is included in hello root of hello repository.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-solution-bottle.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="d105f-171">Tworzenie środowiska wirtualnego</span><span class="sxs-lookup"><span data-stu-id="d105f-171">Create virtual environment</span></span>
<span data-ttu-id="d105f-172">Teraz utwórz środowisko wirtualne dla wdrożenia lokalnego.</span><span class="sxs-lookup"><span data-stu-id="d105f-172">Now we'll create a virtual environment for local development.</span></span> <span data-ttu-id="d105f-173">Kliknij prawym przyciskiem myszy pozycję **Środowiska Python** i wybierz pozycję **Dodaj środowisko wirtualne**.</span><span class="sxs-lookup"><span data-stu-id="d105f-173">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="d105f-174">Upewnij się, że nazwa hello środowiska hello jest `env`.</span><span class="sxs-lookup"><span data-stu-id="d105f-174">Make sure hello name of hello environment is `env`.</span></span>
* <span data-ttu-id="d105f-175">Wybierz interpreter podstawowy hello.</span><span class="sxs-lookup"><span data-stu-id="d105f-175">Select hello base interpreter.</span></span> <span data-ttu-id="d105f-176">Upewnij się, że toouse hello sama wersja środowiska Python, którą wybrano dla aplikacji sieci web (w pliku runtime.txt lub hello **ustawienia aplikacji** bloku aplikacji sieci web w portalu Azure hello).</span><span class="sxs-lookup"><span data-stu-id="d105f-176">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello **Application Settings** blade of your web app in hello Azure Portal).</span></span>
* <span data-ttu-id="d105f-177">Upewnij się, zaznaczono opcję hello toodownload i zainstaluj pakiety.</span><span class="sxs-lookup"><span data-stu-id="d105f-177">Make sure hello option toodownload and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="d105f-178">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d105f-178">Click **Create**.</span></span> <span data-ttu-id="d105f-179">Spowoduje to utworzenie środowiska wirtualnego hello i zainstalowanie składników zależnych wymienionych w pliku requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="d105f-179">This will create hello virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="d105f-180">Uruchamianie przy użyciu serwera projektowego</span><span class="sxs-lookup"><span data-stu-id="d105f-180">Run using development server</span></span>
<span data-ttu-id="d105f-181">Naciśnij klawisz F5 toostart debugowania i przeglądarki sieci web zostanie otwarty toohello strony uruchomionej lokalnie.</span><span class="sxs-lookup"><span data-stu-id="d105f-181">Press F5 toostart debugging, and your web browser will open automatically toohello page running locally.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-browser-bottle.png)

<span data-ttu-id="d105f-182">Można ustawić punktów przerwania w hello źródeł, użyj hello czujki systemu windows itd. Zobacz hello [narzędzi Python Tools for Visual Studio dokumentacji] Aby uzyskać więcej informacji na temat hello różnych funkcji.</span><span class="sxs-lookup"><span data-stu-id="d105f-182">You can set breakpoints in hello sources, use hello watch windows, etc. See hello [Python Tools for Visual Studio Documentation] for more information on hello various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="d105f-183">Wprowadzanie zmian</span><span class="sxs-lookup"><span data-stu-id="d105f-183">Make changes</span></span>
<span data-ttu-id="d105f-184">Teraz możesz eksperymentować, wprowadzając zmiany toohello aplikacji źródeł i/lub szablonach.</span><span class="sxs-lookup"><span data-stu-id="d105f-184">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="d105f-185">Po przetestowaniu zmiany je zatwierdzić toohello repozytorium Git:</span><span class="sxs-lookup"><span data-stu-id="d105f-185">After you've tested your changes, commit them toohello Git repository:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-commit-bottle.png)

### <a name="install-more-packages"></a><span data-ttu-id="d105f-186">Instalowanie dodatkowych pakietów</span><span class="sxs-lookup"><span data-stu-id="d105f-186">Install more packages</span></span>
<span data-ttu-id="d105f-187">Aplikacja może mieć zależności poza środowiskiem Python i Bottle.</span><span class="sxs-lookup"><span data-stu-id="d105f-187">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="d105f-188">Możesz zainstalować dodatkowe pakiety przy użyciu narzędzia pip.</span><span class="sxs-lookup"><span data-stu-id="d105f-188">You can install additional packages using pip.</span></span> <span data-ttu-id="d105f-189">tooinstall pakiet, kliknij prawym przyciskiem myszy na powitania środowisko wirtualne i wybierz **zainstaluj pakiet języka Python**.</span><span class="sxs-lookup"><span data-stu-id="d105f-189">tooinstall a package, right-click on hello virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="d105f-190">Na przykład tooinstall hello Azure SDK dla języka Python, który zapewnia dostęp tooAzure magazynu, usługi service bus i innymi usługami Azure, wprowadź `azure`:</span><span class="sxs-lookup"><span data-stu-id="d105f-190">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-install-package-dialog.png)

<span data-ttu-id="d105f-191">Kliknij prawym przyciskiem myszy na powitania środowiska wirtualnego, a następnie wybierz **Generuj plik requirements.txt** tooupdate requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="d105f-191">Right-click on hello virtual environment and select **Generate requirements.txt** tooupdate requirements.txt.</span></span>

<span data-ttu-id="d105f-192">Następnie Zatwierdź repozytorium Git toohello toorequirements.txt zmiany hello.</span><span class="sxs-lookup"><span data-stu-id="d105f-192">Then, commit hello changes toorequirements.txt toohello Git repository.</span></span>

### <a name="deploy-tooazure"></a><span data-ttu-id="d105f-193">Wdrażanie tooAzure</span><span class="sxs-lookup"><span data-stu-id="d105f-193">Deploy tooAzure</span></span>
<span data-ttu-id="d105f-194">polecenie tootrigger wdrożenia, **synchronizacji** lub **Push**.</span><span class="sxs-lookup"><span data-stu-id="d105f-194">tootrigger a deployment, click on **Sync** or **Push**.</span></span> <span data-ttu-id="d105f-195">Synchronizacja obejmuje zarówno wypychanie, jak i ściąganie.</span><span class="sxs-lookup"><span data-stu-id="d105f-195">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-git-push.png)

<span data-ttu-id="d105f-196">pierwszym wdrożeniu Hello wymaga czasu, ponieważ obejmuje tworzenie środowiska wirtualnego, instalowanie pakietów itp.</span><span class="sxs-lookup"><span data-stu-id="d105f-196">hello first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="d105f-197">Program Visual Studio nie wyświetla postęp hello hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="d105f-197">Visual Studio doesn't show hello progress of hello deployment.</span></span> <span data-ttu-id="d105f-198">Jeśli chcesz tooreview hello w danych wyjściowych, zobacz sekcję hello na [Rozwiązywanie problemów — wdrożenie](#troubleshooting-deployment).</span><span class="sxs-lookup"><span data-stu-id="d105f-198">If you'd like tooreview hello output, see hello section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="d105f-199">Przeglądaj zmiany toohello tooview adresu URL platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d105f-199">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="d105f-200">Wiersz polecenia - Windows - tworzenie aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="d105f-200">Web app development - Windows - Command Line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="d105f-201">Klonowanie repozytorium hello</span><span class="sxs-lookup"><span data-stu-id="d105f-201">Clone hello repository</span></span>
<span data-ttu-id="d105f-202">Najpierw sklonować repozytorium hello przy użyciu adresu URL hello na powitania portalu Azure i dodać hello repozytorium Azure jako zdalnej.</span><span class="sxs-lookup"><span data-stu-id="d105f-202">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="d105f-203">Aby uzyskać więcej informacji, zobacz [tooAzure lokalnego wdrożenia Git usługi aplikacji](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="d105f-203">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="d105f-204">Tworzenie środowiska wirtualnego</span><span class="sxs-lookup"><span data-stu-id="d105f-204">Create virtual environment</span></span>
<span data-ttu-id="d105f-205">Utworzymy nowe środowisko wirtualne dla celów programistycznych (nie należy dodawać go toohello repozytorium).</span><span class="sxs-lookup"><span data-stu-id="d105f-205">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span> <span data-ttu-id="d105f-206">Wirtualnych środowisk języka Python nie są można zmieniać lokalizacji, dlatego każdy Deweloper pracujący nad aplikacji hello tworzy własne środowisko lokalnie.</span><span class="sxs-lookup"><span data-stu-id="d105f-206">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="d105f-207">Upewnij się, że toouse hello sama wersja środowiska Python, którą wybrano dla aplikacji sieci web (w pliku runtime.txt lub hello bloku ustawienia aplikacji dla aplikacji sieci web w portalu Azure hello)</span><span class="sxs-lookup"><span data-stu-id="d105f-207">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello Application Settings blade for your web app in hello Azure Portal)</span></span>

<span data-ttu-id="d105f-208">Dla środowiska Python w wersji 2.7:</span><span class="sxs-lookup"><span data-stu-id="d105f-208">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="d105f-209">Dla środowiska Python w wersji 3.4:</span><span class="sxs-lookup"><span data-stu-id="d105f-209">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="d105f-210">Zainstaluj pakiety zewnętrzne wymagane przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="d105f-210">Install any external packages required by your application.</span></span> <span data-ttu-id="d105f-211">Możesz użyć pliku requirements.txt hello w głównym hello hello repozytorium tooinstall hello pakietów w środowisku wirtualnym:</span><span class="sxs-lookup"><span data-stu-id="d105f-211">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="d105f-212">Uruchamianie przy użyciu serwera projektowego</span><span class="sxs-lookup"><span data-stu-id="d105f-212">Run using development server</span></span>
<span data-ttu-id="d105f-213">Można uruchomić aplikacji hello na serwerze projektowym z hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="d105f-213">You can launch hello application under a development server with hello following command:</span></span>

    env\scripts\python app.py

<span data-ttu-id="d105f-214">Witaj konsoli zostanie wyświetlony adres URL hello i nasłuchuje portu powitania serwera:</span><span class="sxs-lookup"><span data-stu-id="d105f-214">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-run-local-bottle.png)

<span data-ttu-id="d105f-215">Następnie otwórz adres URL toothat przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="d105f-215">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-browser-bottle.png)

### <a name="make-changes"></a><span data-ttu-id="d105f-216">Wprowadzanie zmian</span><span class="sxs-lookup"><span data-stu-id="d105f-216">Make changes</span></span>
<span data-ttu-id="d105f-217">Teraz możesz eksperymentować, wprowadzając zmiany toohello aplikacji źródeł i/lub szablonach.</span><span class="sxs-lookup"><span data-stu-id="d105f-217">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="d105f-218">Po przetestowaniu zmiany je zatwierdzić toohello repozytorium Git:</span><span class="sxs-lookup"><span data-stu-id="d105f-218">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="d105f-219">Instalowanie dodatkowych pakietów</span><span class="sxs-lookup"><span data-stu-id="d105f-219">Install more packages</span></span>
<span data-ttu-id="d105f-220">Aplikacja może mieć zależności poza środowiskiem Python i Bottle.</span><span class="sxs-lookup"><span data-stu-id="d105f-220">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="d105f-221">Możesz zainstalować dodatkowe pakiety przy użyciu narzędzia pip.</span><span class="sxs-lookup"><span data-stu-id="d105f-221">You can install additional packages using pip.</span></span> <span data-ttu-id="d105f-222">Na przykład tooinstall hello Azure SDK dla języka Python, co pozwala na dostęp do magazynu tooAzure, magistrali usług i innych usług Azure, wpisz:</span><span class="sxs-lookup"><span data-stu-id="d105f-222">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="d105f-223">Upewnij się, że tooupdate pliku requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="d105f-223">Make sure tooupdate requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="d105f-224">Zatwierdź zmiany hello:</span><span class="sxs-lookup"><span data-stu-id="d105f-224">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="d105f-225">Wdrażanie tooAzure</span><span class="sxs-lookup"><span data-stu-id="d105f-225">Deploy tooAzure</span></span>
<span data-ttu-id="d105f-226">tootrigger wdrożenia hello wypychania zmiany tooAzure:</span><span class="sxs-lookup"><span data-stu-id="d105f-226">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="d105f-227">Zostanie wyświetlone dane wyjściowe hello hello skryptu wdrożenia, łącznie z tworzeniem środowiska wirtualnego, instalowaniem pakietów i tworzeniem pliku web.config.</span><span class="sxs-lookup"><span data-stu-id="d105f-227">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="d105f-228">Przeglądaj zmiany toohello tooview adresu URL platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d105f-228">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="d105f-229">Wdrażanie aplikacji sieci Web — system Mac/Linux — wiersz polecenia</span><span class="sxs-lookup"><span data-stu-id="d105f-229">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="d105f-230">Klonowanie repozytorium hello</span><span class="sxs-lookup"><span data-stu-id="d105f-230">Clone hello repository</span></span>
<span data-ttu-id="d105f-231">Najpierw sklonować repozytorium hello przy użyciu adresu URL hello na powitania portalu Azure i dodać hello repozytorium Azure jako zdalnej.</span><span class="sxs-lookup"><span data-stu-id="d105f-231">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="d105f-232">Aby uzyskać więcej informacji, zobacz [tooAzure lokalnego wdrożenia Git usługi aplikacji](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="d105f-232">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="d105f-233">Tworzenie środowiska wirtualnego</span><span class="sxs-lookup"><span data-stu-id="d105f-233">Create virtual environment</span></span>
<span data-ttu-id="d105f-234">Utworzymy nowe środowisko wirtualne dla celów programistycznych (nie należy dodawać go toohello repozytorium).</span><span class="sxs-lookup"><span data-stu-id="d105f-234">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span> <span data-ttu-id="d105f-235">Wirtualnych środowisk języka Python nie są można zmieniać lokalizacji, dlatego każdy Deweloper pracujący nad aplikacji hello tworzy własne środowisko lokalnie.</span><span class="sxs-lookup"><span data-stu-id="d105f-235">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="d105f-236">Upewnij się, toouse hello sama wersja środowiska Python, którą wybrano dla aplikacji sieci web (w pliku runtime.txt lub hello bloku ustawienia aplikacji aplikacji sieci web w portalu Azure hello).</span><span class="sxs-lookup"><span data-stu-id="d105f-236">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello Application Settings blade of your web app in hello Azure Portal).</span></span>

<span data-ttu-id="d105f-237">Dla środowiska Python w wersji 2.7:</span><span class="sxs-lookup"><span data-stu-id="d105f-237">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="d105f-238">Dla środowiska Python w wersji 3.4:</span><span class="sxs-lookup"><span data-stu-id="d105f-238">For Python 3.4:</span></span>

    python -m venv env
<span data-ttu-id="d105f-239">lub pyvenv env</span><span class="sxs-lookup"><span data-stu-id="d105f-239">or pyvenv env</span></span>

<span data-ttu-id="d105f-240">Zainstaluj pakiety zewnętrzne wymagane przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="d105f-240">Install any external packages required by your application.</span></span> <span data-ttu-id="d105f-241">Możesz użyć pliku requirements.txt hello w głównym hello hello repozytorium tooinstall hello pakietów w środowisku wirtualnym:</span><span class="sxs-lookup"><span data-stu-id="d105f-241">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="d105f-242">Uruchamianie przy użyciu serwera projektowego</span><span class="sxs-lookup"><span data-stu-id="d105f-242">Run using development server</span></span>
<span data-ttu-id="d105f-243">Można uruchomić aplikacji hello na serwerze projektowym z hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="d105f-243">You can launch hello application under a development server with hello following command:</span></span>

    env/bin/python app.py

<span data-ttu-id="d105f-244">Witaj konsoli zostanie wyświetlony adres URL hello i nasłuchuje portu powitania serwera:</span><span class="sxs-lookup"><span data-stu-id="d105f-244">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/mac-run-local-bottle.png)

<span data-ttu-id="d105f-245">Następnie otwórz adres URL toothat przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="d105f-245">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/mac-browser-bottle.png)

### <a name="make-changes"></a><span data-ttu-id="d105f-246">Wprowadzanie zmian</span><span class="sxs-lookup"><span data-stu-id="d105f-246">Make changes</span></span>
<span data-ttu-id="d105f-247">Teraz możesz eksperymentować, wprowadzając zmiany toohello aplikacji źródeł i/lub szablonach.</span><span class="sxs-lookup"><span data-stu-id="d105f-247">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="d105f-248">Po przetestowaniu zmiany je zatwierdzić toohello repozytorium Git:</span><span class="sxs-lookup"><span data-stu-id="d105f-248">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="d105f-249">Instalowanie dodatkowych pakietów</span><span class="sxs-lookup"><span data-stu-id="d105f-249">Install more packages</span></span>
<span data-ttu-id="d105f-250">Aplikacja może mieć zależności poza środowiskiem Python i Bottle.</span><span class="sxs-lookup"><span data-stu-id="d105f-250">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="d105f-251">Możesz zainstalować dodatkowe pakiety przy użyciu narzędzia pip.</span><span class="sxs-lookup"><span data-stu-id="d105f-251">You can install additional packages using pip.</span></span> <span data-ttu-id="d105f-252">Na przykład tooinstall hello Azure SDK dla języka Python, co pozwala na dostęp do magazynu tooAzure, magistrali usług i innych usług Azure, wpisz:</span><span class="sxs-lookup"><span data-stu-id="d105f-252">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="d105f-253">Upewnij się, że tooupdate pliku requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="d105f-253">Make sure tooupdate requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="d105f-254">Zatwierdź zmiany hello:</span><span class="sxs-lookup"><span data-stu-id="d105f-254">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="d105f-255">Wdrażanie tooAzure</span><span class="sxs-lookup"><span data-stu-id="d105f-255">Deploy tooAzure</span></span>
<span data-ttu-id="d105f-256">tootrigger wdrożenia hello wypychania zmiany tooAzure:</span><span class="sxs-lookup"><span data-stu-id="d105f-256">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="d105f-257">Zostanie wyświetlone dane wyjściowe hello hello skryptu wdrożenia, łącznie z tworzeniem środowiska wirtualnego, instalowaniem pakietów i tworzeniem pliku web.config.</span><span class="sxs-lookup"><span data-stu-id="d105f-257">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="d105f-258">Przeglądaj zmiany toohello tooview adresu URL platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d105f-258">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="d105f-259">Rozwiązywanie problemów — instalowanie pakietów</span><span class="sxs-lookup"><span data-stu-id="d105f-259">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="d105f-260">Rozwiązywanie problemów — środowisko wirtualne</span><span class="sxs-lookup"><span data-stu-id="d105f-260">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="d105f-261">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d105f-261">Next Steps</span></span>
<span data-ttu-id="d105f-262">Wykonaj te toolearn łącza więcej informacji na temat Bottle i narzędzi Python Tools for Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="d105f-262">Follow these links toolearn more about Bottle and Python Tools for Visual Studio:</span></span> 

* <span data-ttu-id="d105f-263">[Dokumentacja bottle]</span><span class="sxs-lookup"><span data-stu-id="d105f-263">[Bottle Documentation]</span></span>
* <span data-ttu-id="d105f-264">[narzędzi Python Tools for Visual Studio dokumentacji]</span><span class="sxs-lookup"><span data-stu-id="d105f-264">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="d105f-265">Aby uzyskać informacje o korzystaniu z magazynu tabel platformy Azure i bazy danych MongoDB:</span><span class="sxs-lookup"><span data-stu-id="d105f-265">For information on using Azure Table Storage and MongoDB:</span></span>

* <span data-ttu-id="d105f-266">[Bottle i bazy danych MongoDB na platformie Azure przy użyciu narzędzi Python Tools for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="d105f-266">[Bottle and MongoDB on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="d105f-267">[Bottle i magazynu tabel platformy Azure na platformie Azure przy użyciu narzędzi Python Tools for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="d105f-267">[Bottle and Azure Table Storage on Azure with Python Tools for Visual Studio]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="d105f-268">Co zostało zmienione</span><span class="sxs-lookup"><span data-stu-id="d105f-268">What's changed</span></span>
* <span data-ttu-id="d105f-269">Toohello przewodnik zmiany z tooApp witryn sieci Web usługi dla: [usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="d105f-269">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Bottle i bazy danych MongoDB na platformie Azure przy użyciu narzędzi Python Tools for Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md
[Bottle i magazynu tabel platformy Azure na platformie Azure przy użyciu narzędzi Python Tools for Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md

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
[Dokumentacja bottle]: http://bottlepy.org/docs/dev/index.html

