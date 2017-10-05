---
title: "Tworzenie aplikacji sieci web za pomocą platformy Flask na platformie Azure"
description: "Samouczek wprowadzający do uruchamiania aplikacji sieci web języka Python na platformie Azure."
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
ms.openlocfilehash: 29457a39ee3df0bbdbc9869cdce0e14bd85b7302
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="creating-web-apps-with-flask-in-azure"></a><span data-ttu-id="6bab4-103">Tworzenie aplikacji sieci web za pomocą platformy Flask na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="6bab4-103">Creating web apps with Flask in Azure</span></span>
<span data-ttu-id="6bab4-104">Ten samouczek zawiera wprowadzenie do uruchamiania środowiska Python [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="6bab4-104">This tutorial describes how to get started running Python in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>  <span data-ttu-id="6bab4-105">Usługa Web Apps zapewnia ograniczony bezpłatny hosting i szybkie wdrażanie, a także możliwość korzystania z języka Python.</span><span class="sxs-lookup"><span data-stu-id="6bab4-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span>  <span data-ttu-id="6bab4-106">Wraz z rozwojem aplikacji można przejść do płatnego hostingu i przeprowadzić integrację z innymi usługami Azure.</span><span class="sxs-lookup"><span data-stu-id="6bab4-106">As your app grows, you can switch to paid hosting, and you can also integrate with all of the other Azure services.</span></span>

<span data-ttu-id="6bab4-107">Utworzysz aplikację przy użyciu platformy sieci web platformy Flask (zobacz alternatywne wersje tego samouczka dla [Django](web-sites-python-create-deploy-django-app.md) i [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span><span class="sxs-lookup"><span data-stu-id="6bab4-107">You will create an application using the Flask web framework (see alternate versions of this tutorial for [Django](web-sites-python-create-deploy-django-app.md) and [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span></span>  <span data-ttu-id="6bab4-108">Zostanie tworzenie witryny sieci Web z poziomu galerii Azure, skonfigurujesz wdrożenie systemu Git i sklonujesz repozytorium lokalnie.</span><span class="sxs-lookup"><span data-stu-id="6bab4-108">You will create the website from the Azure gallery, set up Git deployment, and clone the repository locally.</span></span>  <span data-ttu-id="6bab4-109">Następnie uruchomisz aplikację lokalnie, wprowadzisz zmiany, które zatwierdzisz i wypchniesz na platformę Azure.</span><span class="sxs-lookup"><span data-stu-id="6bab4-109">Then you will run the application locally, make changes, commit and push them to Azure.</span></span>  <span data-ttu-id="6bab4-110">Samouczek pokazuje, jak można to zrobić w systemie Windows lub Mac/Linux.</span><span class="sxs-lookup"><span data-stu-id="6bab4-110">The tutorial shows how to do this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="6bab4-111">Jeśli chcesz zacząć korzystać z usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź do artykułu [Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), w którym wyjaśniono, jak od razu utworzyć początkową aplikację sieci Web o krótkim okresie istnienia w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="6bab4-111">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="6bab4-112">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="6bab4-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="6bab4-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6bab4-113">Prerequisites</span></span>
* <span data-ttu-id="6bab4-114">System Windows, Mac lub Linux</span><span class="sxs-lookup"><span data-stu-id="6bab4-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="6bab4-115">Środowisko Python w wersji 2.7 lub 3.4</span><span class="sxs-lookup"><span data-stu-id="6bab4-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="6bab4-116">Narzędzia setuptools pip, virtualenv (tylko środowisko Python 2.7)</span><span class="sxs-lookup"><span data-stu-id="6bab4-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="6bab4-117">Usługa Git</span><span class="sxs-lookup"><span data-stu-id="6bab4-117">Git</span></span>
* <span data-ttu-id="6bab4-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) — uwaga: ten składnik jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="6bab4-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="6bab4-119">**Uwaga**: publikowanie TFS nie jest obecnie obsługiwane dla projektów języka Python.</span><span class="sxs-lookup"><span data-stu-id="6bab4-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="6bab4-120">Windows</span><span class="sxs-lookup"><span data-stu-id="6bab4-120">Windows</span></span>
<span data-ttu-id="6bab4-121">Jeśli środowisko Python 2.7 lub 3.4 (32-bitowe) nie zostało jeszcze zainstalowane, zalecane jest zainstalowanie [Zestaw Azure SDK dla języka Python w wersji 2.7] lub [zestawu Azure SDK dla języka Python 3.4] przy użyciu Instalatora platformy sieci Web.</span><span class="sxs-lookup"><span data-stu-id="6bab4-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span>  <span data-ttu-id="6bab4-122">Spowoduje to zainstalowanie 32-bitowej wersji środowiska Python, narzędzi setuptools, pip i virtualenv itp. (32-bitowe środowisko Python jest instalowane na maszynach hostów Azure).</span><span class="sxs-lookup"><span data-stu-id="6bab4-122">This installs the 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on the Azure host machines).</span></span>  <span data-ttu-id="6bab4-123">Możesz również pobrać środowisko Python z witryny [python.org].</span><span class="sxs-lookup"><span data-stu-id="6bab4-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="6bab4-124">W przypadku systemu Git zalecane jest narzędzie [Git dla systemu Windows] lub [Github dla systemu Windows].</span><span class="sxs-lookup"><span data-stu-id="6bab4-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span>  <span data-ttu-id="6bab4-125">Jeśli używasz programu Visual Studio, możesz korzystać ze zintegrowanej obsługi systemu Git.</span><span class="sxs-lookup"><span data-stu-id="6bab4-125">If you use Visual Studio, you can use the integrated Git support.</span></span>

<span data-ttu-id="6bab4-126">Zalecane jest również zainstalowanie narzędzi [Python Tools 2.2 for Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="6bab4-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span>  <span data-ttu-id="6bab4-127">Jest to opcjonalne, ale jeśli masz program [Program Visual Studio], taki jak bezpłatny program Visual Studio Community 2013 lub Visual Studio Express 2013 for Web, możesz korzystać z doskonałego środowiska IDE języka Python.</span><span class="sxs-lookup"><span data-stu-id="6bab4-127">This is optional, but if you have [Visual Studio], including the free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="6bab4-128">System Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="6bab4-128">Mac/Linux</span></span>
<span data-ttu-id="6bab4-129">Środowisko Python i system Git powinny być już zainstalowane, ale upewnij się, że masz środowisko Python 2.7 lub 3.4.</span><span class="sxs-lookup"><span data-stu-id="6bab4-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-create-on-the-azure-portal"></a><span data-ttu-id="6bab4-130">Tworzenie aplikacji sieci Web w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="6bab4-130">Web app create on the Azure Portal</span></span>
<span data-ttu-id="6bab4-131">Pierwszym krokiem procedury tworzenia aplikacji jest utworzenie aplikacji sieci Web za pośrednictwem [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6bab4-131">The first step in creating your app is to create the web app via the [Azure Portal](https://portal.azure.com).</span></span> 

1. <span data-ttu-id="6bab4-132">Zaloguj się do Portalu Azure i kliknij przycisk **NOWY** w lewym dolnym rogu.</span><span class="sxs-lookup"><span data-stu-id="6bab4-132">Log into the Azure Portal and click the **NEW** button in the bottom left corner.</span></span> 
2. <span data-ttu-id="6bab4-133">Kliknij pozycję **Sieci Web i mobilność**.</span><span class="sxs-lookup"><span data-stu-id="6bab4-133">Click **Web + Mobile**.</span></span>
3. <span data-ttu-id="6bab4-134">W polu wyszukiwania wpisz „python”.</span><span class="sxs-lookup"><span data-stu-id="6bab4-134">In the search box, type "python".</span></span>
4. <span data-ttu-id="6bab4-135">W wynikach wyszukiwania wybierz **Flask**, następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="6bab4-135">In the search results, select **Flask**, then click **Create**.</span></span>
5. <span data-ttu-id="6bab4-136">Skonfiguruj nową aplikację platformy Flask, takich jak tworzenie nowego planu usługi App Service i nowej grupy zasobów dla niego.</span><span class="sxs-lookup"><span data-stu-id="6bab4-136">Configure the new Flask app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="6bab4-137">Następnie kliknij pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="6bab4-137">Then, click **Create**.</span></span>
6. <span data-ttu-id="6bab4-138">Skonfiguruj publikowanie w systemie Git dla nowo utworzonej aplikacji sieci Web zgodnie z poniższymi instrukcjami w artykule [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md) (Lokalne wdrażanie przy użyciu systemu Git w usłudze Azure App Service).</span><span class="sxs-lookup"><span data-stu-id="6bab4-138">Configure Git publishing for your newly created web app by following the instructions at [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="6bab4-139">Omówienie aplikacji</span><span class="sxs-lookup"><span data-stu-id="6bab4-139">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="6bab4-140">Zawartość repozytorium Git</span><span class="sxs-lookup"><span data-stu-id="6bab4-140">Git repository contents</span></span>
<span data-ttu-id="6bab4-141">Poniżej przedstawiono pliki w początkowym repozytorium Git, które sklonujemy w następnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="6bab4-141">Here's an overview of the files you'll find in the initial Git repository, which we'll clone in the next section.</span></span>

    \FlaskWebProject\__init__.py
    \FlaskWebProject\views.py
    \FlaskWebProject\static\content\
    \FlaskWebProject\static\fonts\
    \FlaskWebProject\static\scripts\
    \FlaskWebProject\templates\about.html
    \FlaskWebProject\templates\contact.html
    \FlaskWebProject\templates\index.html
    \FlaskWebProject\templates\layout.html

<span data-ttu-id="6bab4-142">Główne źródła dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6bab4-142">Main sources for the application.</span></span>  <span data-ttu-id="6bab4-143">Składa się z 3 stron (indeks, informacje, kontakt) z układem głównym.</span><span class="sxs-lookup"><span data-stu-id="6bab4-143">Consists of 3 pages (index, about, contact) with a master layout.</span></span>  <span data-ttu-id="6bab4-144">Zawartość statyczna i skrypty obejmują bootstrap, jquery, modernizr i respond.</span><span class="sxs-lookup"><span data-stu-id="6bab4-144">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \runserver.py

<span data-ttu-id="6bab4-145">Lokalne działania projektowe obsługi serwera.</span><span class="sxs-lookup"><span data-stu-id="6bab4-145">Local development server support.</span></span> <span data-ttu-id="6bab4-146">Umożliwia uruchamianie aplikacji lokalnie.</span><span class="sxs-lookup"><span data-stu-id="6bab4-146">Use this to run the application locally.</span></span>

    \FlaskWebProject.pyproj
    \FlaskWebProject.sln

<span data-ttu-id="6bab4-147">Pliki projektu do użycia z narzędziami [Python Tools for Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="6bab4-147">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="6bab4-148">Serwer proxy usług IIS dla środowisk wirtualnych i obsługa zdalnego debugowania narzędzi PTVS.</span><span class="sxs-lookup"><span data-stu-id="6bab4-148">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="6bab4-149">Pakiety zewnętrzne wymagane przez tę aplikację.</span><span class="sxs-lookup"><span data-stu-id="6bab4-149">External packages needed by this application.</span></span> <span data-ttu-id="6bab4-150">Skrypt wdrożenia będzie instalować przy użyciu narzędzia pip pakiety wymienione w tym pliku.</span><span class="sxs-lookup"><span data-stu-id="6bab4-150">The deployment script will pip install the packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="6bab4-151">Pliki konfiguracji programu IIS.</span><span class="sxs-lookup"><span data-stu-id="6bab4-151">IIS configuration files.</span></span>  <span data-ttu-id="6bab4-152">Skrypt wdrożenia użyje odpowiedniego pliku web.x.y.config i skopiuje go jako plik web.config.</span><span class="sxs-lookup"><span data-stu-id="6bab4-152">The deployment script will use the appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="6bab4-153">Pliki opcjonalne — dostosowywanie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="6bab4-153">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="6bab4-154">Pliki opcjonalne — środowisko uruchomieniowe języka Python</span><span class="sxs-lookup"><span data-stu-id="6bab4-154">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="6bab4-155">Dodatkowe pliki na serwerze</span><span class="sxs-lookup"><span data-stu-id="6bab4-155">Additional files on server</span></span>
<span data-ttu-id="6bab4-156">Niektóre pliki istnieją na serwerze, ale nie są dodawane do repozytorium git.</span><span class="sxs-lookup"><span data-stu-id="6bab4-156">Some files exist on the server but are not added to the git repository.</span></span>  <span data-ttu-id="6bab4-157">Są one tworzone przez skrypt wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="6bab4-157">These are created by the deployment script.</span></span>

    \web.config

<span data-ttu-id="6bab4-158">Plik konfiguracji programu IIS.</span><span class="sxs-lookup"><span data-stu-id="6bab4-158">IIS configuration file.</span></span>  <span data-ttu-id="6bab4-159">Tworzony na podstawie pliku web.x.y.config przy każdym wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="6bab4-159">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="6bab4-160">Środowisko wirtualne języka Python.</span><span class="sxs-lookup"><span data-stu-id="6bab4-160">Python virtual environment.</span></span>  <span data-ttu-id="6bab4-161">Utworzonych podczas wdrażania, jeśli zgodne środowisko wirtualne już nie istnieje w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6bab4-161">Created during deployment if a compatible virtual environment doesn't already exist on the app.</span></span>  <span data-ttu-id="6bab4-162">Pakiety wymienione w pliku requirements.txt są instalowane przy użyciu narzędzia pip, ale narzędzie pip pomija instalację, jeśli pakiety zostały już zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="6bab4-162">Packages listed in requirements.txt are pip installed, but pip will skip installation if the packages are already installed.</span></span>

<span data-ttu-id="6bab4-163">W 3 następnych sekcjach opisano procedury wdrażania aplikacji sieci Web w 3 różnych środowiskach:</span><span class="sxs-lookup"><span data-stu-id="6bab4-163">The next 3 sections describe how to proceed with the web app development under 3 different environments:</span></span>

* <span data-ttu-id="6bab4-164">System Windows — przy użyciu narzędzi Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6bab4-164">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="6bab4-165">System Windows — przy użyciu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="6bab4-165">Windows, with command line</span></span>
* <span data-ttu-id="6bab4-166">System Mac/Linux — przy użyciu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="6bab4-166">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="6bab4-167">Wdrażanie aplikacji sieci Web — system Windows — narzędzia Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6bab4-167">Web app development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="6bab4-168">Klonowanie repozytorium</span><span class="sxs-lookup"><span data-stu-id="6bab4-168">Clone the repository</span></span>
<span data-ttu-id="6bab4-169">Najpierw sklonuj repozytorium przy użyciu adresu URL podanego w witrynie Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="6bab4-169">First, clone the repository using the URL provided on the Azure Portal.</span></span> <span data-ttu-id="6bab4-170">Aby uzyskać więcej informacji, zobacz [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md) (Lokalne wdrażanie przy użyciu systemu Git w usłudze Azure App Service).</span><span class="sxs-lookup"><span data-stu-id="6bab4-170">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="6bab4-171">Otwórz plik rozwiązania (SLN), który znajduje się w folderze głównym repozytorium.</span><span class="sxs-lookup"><span data-stu-id="6bab4-171">Open the solution file (.sln) that is included in the root of the repository.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-solution-flask.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="6bab4-172">Tworzenie środowiska wirtualnego</span><span class="sxs-lookup"><span data-stu-id="6bab4-172">Create virtual environment</span></span>
<span data-ttu-id="6bab4-173">Teraz utwórz środowisko wirtualne dla wdrożenia lokalnego.</span><span class="sxs-lookup"><span data-stu-id="6bab4-173">Now we'll create a virtual environment for local development.</span></span>  <span data-ttu-id="6bab4-174">Kliknij prawym przyciskiem myszy pozycję **Środowiska Python** i wybierz pozycję **Dodaj środowisko wirtualne**.</span><span class="sxs-lookup"><span data-stu-id="6bab4-174">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="6bab4-175">Upewnij się, że nazwa środowiska to `env`.</span><span class="sxs-lookup"><span data-stu-id="6bab4-175">Make sure the name of the environment is `env`.</span></span>
* <span data-ttu-id="6bab4-176">Wybierz interpreter podstawowy.</span><span class="sxs-lookup"><span data-stu-id="6bab4-176">Select the base interpreter.</span></span>  <span data-ttu-id="6bab4-177">Upewnij się, że jest używana ta sama wersja środowiska Python, którą wybrano dla aplikacji sieci Web (w pliku runtime.txt lub bloku **Ustawienia aplikacji** dla aplikacji sieci Web w Portalu Azure).</span><span class="sxs-lookup"><span data-stu-id="6bab4-177">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span></span>
* <span data-ttu-id="6bab4-178">Upewnij się, że opcja pobierania i instalowania pakietów została zaznaczona.</span><span class="sxs-lookup"><span data-stu-id="6bab4-178">Make sure the option to download and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="6bab4-179">Kliknij pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="6bab4-179">Click **Create**.</span></span>  <span data-ttu-id="6bab4-180">Spowoduje to utworzenie środowiska wirtualnego i zainstalowanie składników zależnych wymienionych w pliku requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="6bab4-180">This will create the virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="6bab4-181">Uruchamianie przy użyciu serwera projektowego</span><span class="sxs-lookup"><span data-stu-id="6bab4-181">Run using development server</span></span>
<span data-ttu-id="6bab4-182">Naciśnij klawisz F5, aby rozpocząć debugowanie. Spowoduje to automatyczne otwarcie przeglądarki sieci Web i wyświetlenie strony uruchomionej lokalnie.</span><span class="sxs-lookup"><span data-stu-id="6bab4-182">Press F5 to start debugging, and your web browser will open automatically to the page running locally.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

<span data-ttu-id="6bab4-183">Można ustawiać punkty przerwania w źródłach, używać okien wyrażeń kontrolnych itp.  Zapoznaj się z [Dokumentacja narzędzi Python Tools for Visual Studio], aby uzyskać więcej informacji na temat różnych funkcji.</span><span class="sxs-lookup"><span data-stu-id="6bab4-183">You can set breakpoints in the sources, use the watch windows, etc.  See the [Python Tools for Visual Studio Documentation] for more information on the various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="6bab4-184">Wprowadzanie zmian</span><span class="sxs-lookup"><span data-stu-id="6bab4-184">Make changes</span></span>
<span data-ttu-id="6bab4-185">Teraz możesz eksperymentować, wprowadzając zmiany w źródłach i/lub szablonach aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6bab4-185">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="6bab4-186">Po przetestowaniu wprowadzonych zmian zatwierdź je w repozytorium Git:</span><span class="sxs-lookup"><span data-stu-id="6bab4-186">After you've tested your changes, commit them to the Git repository:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-commit-flask.png)

### <a name="install-more-packages"></a><span data-ttu-id="6bab4-187">Instalowanie dodatkowych pakietów</span><span class="sxs-lookup"><span data-stu-id="6bab4-187">Install more packages</span></span>
<span data-ttu-id="6bab4-188">Aplikacja może mieć zależności poza środowiskiem Python i platformy Flask.</span><span class="sxs-lookup"><span data-stu-id="6bab4-188">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="6bab4-189">Możesz zainstalować dodatkowe pakiety przy użyciu narzędzia pip.</span><span class="sxs-lookup"><span data-stu-id="6bab4-189">You can install additional packages using pip.</span></span>  <span data-ttu-id="6bab4-190">Aby zainstalować pakiet, kliknij prawym przyciskiem myszy środowisko wirtualne i wybierz pozycję **Zainstaluj pakiet języka Python**.</span><span class="sxs-lookup"><span data-stu-id="6bab4-190">To install a package, right-click on the virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="6bab4-191">Aby na przykład zainstalować zestaw Azure SDK dla języka Python zapewniający dostęp do magazynu Azure, magistrali usług i innych usług Azure, wprowadź `azure`:</span><span class="sxs-lookup"><span data-stu-id="6bab4-191">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-install-package-dialog.png)

<span data-ttu-id="6bab4-192">Kliknij prawym przyciskiem myszy środowisko wirtualne i wybierz pozycję **Generuj plik requirements.txt**, aby zaktualizować plik requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="6bab4-192">Right-click on the virtual environment and select **Generate requirements.txt** to update requirements.txt.</span></span>

<span data-ttu-id="6bab4-193">Następnie zatwierdź zmiany w pliku requirements.txt w repozytorium Git.</span><span class="sxs-lookup"><span data-stu-id="6bab4-193">Then, commit the changes to requirements.txt to the Git repository.</span></span>

### <a name="deploy-to-azure"></a><span data-ttu-id="6bab4-194">Wdrażanie na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="6bab4-194">Deploy to Azure</span></span>
<span data-ttu-id="6bab4-195">Aby wyzwolić wdrożenie, kliknij pozycję **Synchronizuj** lub **Wypchnij**.</span><span class="sxs-lookup"><span data-stu-id="6bab4-195">To trigger a deployment, click on **Sync** or **Push**.</span></span>  <span data-ttu-id="6bab4-196">Synchronizacja obejmuje zarówno wypychanie, jak i ściąganie.</span><span class="sxs-lookup"><span data-stu-id="6bab4-196">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-git-push.png)

<span data-ttu-id="6bab4-197">Pierwsze wdrożenie trwa dłużej, ponieważ obejmuje tworzenie środowiska wirtualnego, instalowanie pakietów itp.</span><span class="sxs-lookup"><span data-stu-id="6bab4-197">The first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="6bab4-198">Program Visual Studio nie wyświetla postępu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="6bab4-198">Visual Studio doesn't show the progress of the deployment.</span></span>  <span data-ttu-id="6bab4-199">Jeśli chcesz przejrzeć dane wyjściowe, zobacz sekcję [Rozwiązywanie problemów — wdrożenie](#troubleshooting-deployment).</span><span class="sxs-lookup"><span data-stu-id="6bab4-199">If you'd like to review the output, see the section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="6bab4-200">Przejdź do adresu URL platformy Azure, aby przejrzeć wprowadzone zmiany.</span><span class="sxs-lookup"><span data-stu-id="6bab4-200">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="6bab4-201">Wdrażanie aplikacji sieci Web — system Windows — wiersz polecenia</span><span class="sxs-lookup"><span data-stu-id="6bab4-201">Web app development - Windows - command line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="6bab4-202">Klonowanie repozytorium</span><span class="sxs-lookup"><span data-stu-id="6bab4-202">Clone the repository</span></span>
<span data-ttu-id="6bab4-203">Najpierw sklonuj repozytorium przy użyciu adresu URL podanego w witrynie Azure Portal i dodaj repozytorium Azure jako repozytorium zdalne.</span><span class="sxs-lookup"><span data-stu-id="6bab4-203">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="6bab4-204">Aby uzyskać więcej informacji, zobacz [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md) (Lokalne wdrażanie przy użyciu systemu Git w usłudze Azure App Service).</span><span class="sxs-lookup"><span data-stu-id="6bab4-204">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="6bab4-205">Tworzenie środowiska wirtualnego</span><span class="sxs-lookup"><span data-stu-id="6bab4-205">Create virtual environment</span></span>
<span data-ttu-id="6bab4-206">Zostanie utworzone nowe środowisko wirtualne dla celów wdrożenia (nie należy dodawać go do repozytorium).</span><span class="sxs-lookup"><span data-stu-id="6bab4-206">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span>  <span data-ttu-id="6bab4-207">Nie można zmieniać lokalizacji wirtualnych środowisk języka Python, dlatego każdy deweloper pracujący nad aplikacją tworzy własne środowisko lokalnie.</span><span class="sxs-lookup"><span data-stu-id="6bab4-207">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="6bab4-208">Upewnij się, że jest używana ta sama wersja środowiska Python, którą wybrano dla aplikacji sieci Web (w pliku runtime.txt lub bloku **Ustawienia aplikacji** dla aplikacji sieci Web w Portalu Azure).</span><span class="sxs-lookup"><span data-stu-id="6bab4-208">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span></span>

<span data-ttu-id="6bab4-209">Dla środowiska Python w wersji 2.7:</span><span class="sxs-lookup"><span data-stu-id="6bab4-209">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="6bab4-210">Dla środowiska Python w wersji 3.4:</span><span class="sxs-lookup"><span data-stu-id="6bab4-210">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="6bab4-211">Zainstaluj pakiety zewnętrzne wymagane przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="6bab4-211">Install any external packages required by your application.</span></span> <span data-ttu-id="6bab4-212">Korzystając z pliku requirements.txt w folderze głównym repozytorium, możesz instalować pakiety w środowisku wirtualnym:</span><span class="sxs-lookup"><span data-stu-id="6bab4-212">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="6bab4-213">Uruchamianie przy użyciu serwera projektowego</span><span class="sxs-lookup"><span data-stu-id="6bab4-213">Run using development server</span></span>
<span data-ttu-id="6bab4-214">Możesz uruchomić aplikację na serwerze projektowym przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="6bab4-214">You can launch the application under a development server with the following command:</span></span>

    env\scripts\python runserver.py

<span data-ttu-id="6bab4-215">Na konsoli zostanie wyświetlony adres URL i port nasłuchiwany przez serwer:</span><span class="sxs-lookup"><span data-stu-id="6bab4-215">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-run-local-flask.png)

<span data-ttu-id="6bab4-216">Następnie otwórz w przeglądarce sieci Web stronę wskazywaną przez ten adres URL.</span><span class="sxs-lookup"><span data-stu-id="6bab4-216">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

### <a name="make-changes"></a><span data-ttu-id="6bab4-217">Wprowadzanie zmian</span><span class="sxs-lookup"><span data-stu-id="6bab4-217">Make changes</span></span>
<span data-ttu-id="6bab4-218">Teraz możesz eksperymentować, wprowadzając zmiany w źródłach i/lub szablonach aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6bab4-218">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="6bab4-219">Po przetestowaniu wprowadzonych zmian zatwierdź je w repozytorium Git:</span><span class="sxs-lookup"><span data-stu-id="6bab4-219">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="6bab4-220">Instalowanie dodatkowych pakietów</span><span class="sxs-lookup"><span data-stu-id="6bab4-220">Install more packages</span></span>
<span data-ttu-id="6bab4-221">Aplikacja może mieć zależności poza środowiskiem Python i platformy Flask.</span><span class="sxs-lookup"><span data-stu-id="6bab4-221">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="6bab4-222">Możesz zainstalować dodatkowe pakiety przy użyciu narzędzia pip.</span><span class="sxs-lookup"><span data-stu-id="6bab4-222">You can install additional packages using pip.</span></span>  <span data-ttu-id="6bab4-223">Aby na przykład zainstalować zestaw Azure SDK dla języka Python zapewniający dostęp do magazynu Azure, magistrali usług i innych usług Azure, wpisz:</span><span class="sxs-lookup"><span data-stu-id="6bab4-223">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="6bab4-224">Pamiętaj o zaktualizowaniu pliku requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="6bab4-224">Make sure to update requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="6bab4-225">Zatwierdź zmiany:</span><span class="sxs-lookup"><span data-stu-id="6bab4-225">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="6bab4-226">Wdrażanie na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="6bab4-226">Deploy to Azure</span></span>
<span data-ttu-id="6bab4-227">Aby wyzwolić wdrożenie, wypchnij zmiany na platformę Azure:</span><span class="sxs-lookup"><span data-stu-id="6bab4-227">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="6bab4-228">Zostaną wyświetlone dane wyjściowe skryptu wdrożenia, łącznie z tworzeniem środowiska wirtualnego, instalowaniem pakietów i tworzeniem pliku web.config.</span><span class="sxs-lookup"><span data-stu-id="6bab4-228">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="6bab4-229">Przejdź do adresu URL platformy Azure, aby przejrzeć wprowadzone zmiany.</span><span class="sxs-lookup"><span data-stu-id="6bab4-229">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="6bab4-230">Wdrażanie aplikacji sieci Web — system Mac/Linux — wiersz polecenia</span><span class="sxs-lookup"><span data-stu-id="6bab4-230">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="6bab4-231">Klonowanie repozytorium</span><span class="sxs-lookup"><span data-stu-id="6bab4-231">Clone the repository</span></span>
<span data-ttu-id="6bab4-232">Najpierw sklonuj repozytorium przy użyciu adresu URL podanego w witrynie Azure Portal i dodaj repozytorium Azure jako repozytorium zdalne.</span><span class="sxs-lookup"><span data-stu-id="6bab4-232">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="6bab4-233">Aby uzyskać więcej informacji, zobacz [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md) (Lokalne wdrażanie przy użyciu systemu Git w usłudze Azure App Service).</span><span class="sxs-lookup"><span data-stu-id="6bab4-233">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="6bab4-234">Tworzenie środowiska wirtualnego</span><span class="sxs-lookup"><span data-stu-id="6bab4-234">Create virtual environment</span></span>
<span data-ttu-id="6bab4-235">Zostanie utworzone nowe środowisko wirtualne dla celów wdrożenia (nie należy dodawać go do repozytorium).</span><span class="sxs-lookup"><span data-stu-id="6bab4-235">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span>  <span data-ttu-id="6bab4-236">Nie można zmieniać lokalizacji wirtualnych środowisk języka Python, dlatego każdy deweloper pracujący nad aplikacją tworzy własne środowisko lokalnie.</span><span class="sxs-lookup"><span data-stu-id="6bab4-236">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="6bab4-237">Upewnij się, że jest używana ta sama wersja środowiska Python, którą wybrano dla aplikacji sieci Web (w pliku runtime.txt lub bloku **Ustawienia aplikacji** dla aplikacji sieci Web w Portalu Azure).</span><span class="sxs-lookup"><span data-stu-id="6bab4-237">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span></span>

<span data-ttu-id="6bab4-238">Dla środowiska Python w wersji 2.7:</span><span class="sxs-lookup"><span data-stu-id="6bab4-238">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="6bab4-239">Dla środowiska Python w wersji 3.4:</span><span class="sxs-lookup"><span data-stu-id="6bab4-239">For Python 3.4:</span></span>

    python -m venv env
<span data-ttu-id="6bab4-240">lub pyvenv env</span><span class="sxs-lookup"><span data-stu-id="6bab4-240">or pyvenv env</span></span>

<span data-ttu-id="6bab4-241">Zainstaluj pakiety zewnętrzne wymagane przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="6bab4-241">Install any external packages required by your application.</span></span> <span data-ttu-id="6bab4-242">Korzystając z pliku requirements.txt w folderze głównym repozytorium, możesz instalować pakiety w środowisku wirtualnym:</span><span class="sxs-lookup"><span data-stu-id="6bab4-242">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="6bab4-243">Uruchamianie przy użyciu serwera projektowego</span><span class="sxs-lookup"><span data-stu-id="6bab4-243">Run using development server</span></span>
<span data-ttu-id="6bab4-244">Możesz uruchomić aplikację na serwerze projektowym przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="6bab4-244">You can launch the application under a development server with the following command:</span></span>

    env/bin/python runserver.py

<span data-ttu-id="6bab4-245">Na konsoli zostanie wyświetlony adres URL i port nasłuchiwany przez serwer:</span><span class="sxs-lookup"><span data-stu-id="6bab4-245">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/mac-run-local-flask.png)

<span data-ttu-id="6bab4-246">Następnie otwórz w przeglądarce sieci Web stronę wskazywaną przez ten adres URL.</span><span class="sxs-lookup"><span data-stu-id="6bab4-246">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/mac-browser-flask.png)

### <a name="make-changes"></a><span data-ttu-id="6bab4-247">Wprowadzanie zmian</span><span class="sxs-lookup"><span data-stu-id="6bab4-247">Make changes</span></span>
<span data-ttu-id="6bab4-248">Teraz możesz eksperymentować, wprowadzając zmiany w źródłach i/lub szablonach aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6bab4-248">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="6bab4-249">Po przetestowaniu wprowadzonych zmian zatwierdź je w repozytorium Git:</span><span class="sxs-lookup"><span data-stu-id="6bab4-249">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="6bab4-250">Instalowanie dodatkowych pakietów</span><span class="sxs-lookup"><span data-stu-id="6bab4-250">Install more packages</span></span>
<span data-ttu-id="6bab4-251">Aplikacja może mieć zależności poza środowiskiem Python i platformy Flask.</span><span class="sxs-lookup"><span data-stu-id="6bab4-251">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="6bab4-252">Możesz zainstalować dodatkowe pakiety przy użyciu narzędzia pip.</span><span class="sxs-lookup"><span data-stu-id="6bab4-252">You can install additional packages using pip.</span></span>  <span data-ttu-id="6bab4-253">Aby na przykład zainstalować zestaw Azure SDK dla języka Python zapewniający dostęp do magazynu Azure, magistrali usług i innych usług Azure, wpisz:</span><span class="sxs-lookup"><span data-stu-id="6bab4-253">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="6bab4-254">Pamiętaj o zaktualizowaniu pliku requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="6bab4-254">Make sure to update requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="6bab4-255">Zatwierdź zmiany:</span><span class="sxs-lookup"><span data-stu-id="6bab4-255">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="6bab4-256">Wdrażanie na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="6bab4-256">Deploy to Azure</span></span>
<span data-ttu-id="6bab4-257">Aby wyzwolić wdrożenie, wypchnij zmiany na platformę Azure:</span><span class="sxs-lookup"><span data-stu-id="6bab4-257">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="6bab4-258">Zostaną wyświetlone dane wyjściowe skryptu wdrożenia, łącznie z tworzeniem środowiska wirtualnego, instalowaniem pakietów i tworzeniem pliku web.config.</span><span class="sxs-lookup"><span data-stu-id="6bab4-258">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="6bab4-259">Przejdź do adresu URL platformy Azure, aby przejrzeć wprowadzone zmiany.</span><span class="sxs-lookup"><span data-stu-id="6bab4-259">Browse to the Azure URL to view your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="6bab4-260">Rozwiązywanie problemów — instalowanie pakietów</span><span class="sxs-lookup"><span data-stu-id="6bab4-260">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="6bab4-261">Rozwiązywanie problemów — środowisko wirtualne</span><span class="sxs-lookup"><span data-stu-id="6bab4-261">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="6bab4-262">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6bab4-262">Next Steps</span></span>
<span data-ttu-id="6bab4-263">Skorzystaj z poniższych linków, aby dowiedzieć się więcej o Flask i narzędzi Python Tools for Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="6bab4-263">Follow these links to learn more about Flask and Python Tools for Visual Studio:</span></span> 

* <span data-ttu-id="6bab4-264">[Dokumentacja platformy flask]</span><span class="sxs-lookup"><span data-stu-id="6bab4-264">[Flask Documentation]</span></span>
* <span data-ttu-id="6bab4-265">[Dokumentacja narzędzi Python Tools for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="6bab4-265">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="6bab4-266">Aby uzyskać informacje o korzystaniu z magazynu tabel platformy Azure i bazy danych MongoDB:</span><span class="sxs-lookup"><span data-stu-id="6bab4-266">For information on using Azure Table Storage and MongoDB:</span></span>

* <span data-ttu-id="6bab4-267">[Flask i bazy danych MongoDB na platformie Azure przy użyciu narzędzi Python Tools for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="6bab4-267">[Flask and MongoDB on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="6bab4-268">[Flask i magazynu tabel platformy Azure na platformie Azure przy użyciu narzędzi Python Tools for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="6bab4-268">[Flask and Azure Table Storage on Azure with Python Tools for Visual Studio]</span></span>

<span data-ttu-id="6bab4-269">Aby uzyskać więcej informacji, zobacz też [Centrum deweloperów języka Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="6bab4-269">For more information, see also the [Python Developer Center](/develop/python/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="6bab4-270">Co zostało zmienione</span><span class="sxs-lookup"><span data-stu-id="6bab4-270">What's changed</span></span>
* <span data-ttu-id="6bab4-271">Przewodnik dotyczący przejścia od usługi Witryny sieci Web do usługi App Service można znaleźć w temacie [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714) (Usługa Azure App Service i jej wpływ na istniejące usługi platformy Azure).</span><span class="sxs-lookup"><span data-stu-id="6bab4-271">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
<span data-ttu-id="6bab4-272">[Flask i bazy danych MongoDB na platformie Azure przy użyciu narzędzi Python Tools for Visual Studio]: https://github.com/microsoft/ptvs/wiki/Flask-and-MongoDB-on-Azure</span><span class="sxs-lookup"><span data-stu-id="6bab4-272">[Flask and MongoDB on Azure with Python Tools for Visual Studio]: https://github.com/microsoft/ptvs/wiki/Flask-and-MongoDB-on-Azure</span></span>
<span data-ttu-id="6bab4-273">[Flask i magazynu tabel platformy Azure na platformie Azure przy użyciu narzędzi Python Tools for Visual Studio]: web-sites-python-ptvs-flask-table-storage.md</span><span class="sxs-lookup"><span data-stu-id="6bab4-273">[Flask and Azure Table Storage on Azure with Python Tools for Visual Studio]: web-sites-python-ptvs-flask-table-storage.md</span></span>

<!--External Link references-->
<span data-ttu-id="6bab4-274">[Zestaw Azure SDK dla języka Python w wersji 2.7]: http://go.microsoft.com/fwlink/?linkid=254281</span><span class="sxs-lookup"><span data-stu-id="6bab4-274">[Azure SDK for Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281</span></span>
<span data-ttu-id="6bab4-275">[zestawu Azure SDK dla języka Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990</span><span class="sxs-lookup"><span data-stu-id="6bab4-275">[Azure SDK for Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990</span></span>
<span data-ttu-id="6bab4-276">[python.org]: http://www.python.org/</span><span class="sxs-lookup"><span data-stu-id="6bab4-276">[python.org]: http://www.python.org/</span></span>
<span data-ttu-id="6bab4-277">[Git dla systemu Windows]: http://msysgit.github.io/</span><span class="sxs-lookup"><span data-stu-id="6bab4-277">[Git for Windows]: http://msysgit.github.io/</span></span>
<span data-ttu-id="6bab4-278">[Github dla systemu Windows]: https://windows.github.com/</span><span class="sxs-lookup"><span data-stu-id="6bab4-278">[GitHub for Windows]: https://windows.github.com/</span></span>
<span data-ttu-id="6bab4-279">[Python Tools for Visual Studio]: http://aka.ms/ptvs</span><span class="sxs-lookup"><span data-stu-id="6bab4-279">[Python Tools for Visual Studio]: http://aka.ms/ptvs</span></span>
<span data-ttu-id="6bab4-280">[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span><span class="sxs-lookup"><span data-stu-id="6bab4-280">[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span></span>
<span data-ttu-id="6bab4-281">[Program Visual Studio]: http://www.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="6bab4-281">[Visual Studio]: http://www.visualstudio.com/</span></span>
<span data-ttu-id="6bab4-282">[Dokumentacja narzędzi Python Tools for Visual Studio]: http://aka.ms/ptvsdocs</span><span class="sxs-lookup"><span data-stu-id="6bab4-282">[Python Tools for Visual Studio Documentation]: http://aka.ms/ptvsdocs</span></span>
<span data-ttu-id="6bab4-283">[Dokumentacja platformy flask]: http://flask.pocoo.org/</span><span class="sxs-lookup"><span data-stu-id="6bab4-283">[Flask Documentation]: http://flask.pocoo.org/</span></span> 

