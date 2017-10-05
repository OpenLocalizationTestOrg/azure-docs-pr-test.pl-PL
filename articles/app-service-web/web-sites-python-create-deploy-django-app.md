---
title: "Tworzenie aplikacji sieci Web przy użyciu platformy Django na platformie Azure"
description: "Samouczek przedstawiający uruchamianie aplikacji sieci Web w języku Python w aplikacjach Web Apps w usłudze Azure App Service."
services: app-service\web
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 9be1a05a-9460-49ae-94fb-9798f82c11cf
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/19/2016
ms.author: huvalo
ms.openlocfilehash: 388a2db21dd1669b48b3204aaa322d7915905506
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="creating-web-apps-with-django-in-azure"></a><span data-ttu-id="103a7-103">Tworzenie aplikacji sieci Web przy użyciu platformy Django na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="103a7-103">Creating web apps with Django in Azure</span></span>
<span data-ttu-id="103a7-104">Ten samouczek zawiera wprowadzenie do uruchamiania skryptów w języku Python w [aplikacjach Web Apps w usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="103a7-104">This tutorial describes how to get started running Python on [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="103a7-105">Usługa Web Apps zapewnia ograniczony bezpłatny hosting i szybkie wdrażanie, a także możliwość korzystania z języka Python.</span><span class="sxs-lookup"><span data-stu-id="103a7-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span> <span data-ttu-id="103a7-106">Wraz z rozwojem aplikacji można przejść do płatnego hostingu i przeprowadzić integrację z innymi usługami Azure.</span><span class="sxs-lookup"><span data-stu-id="103a7-106">As your app grows, you can switch to paid hosting, and you can also integrate with all of the other Azure services.</span></span>

<span data-ttu-id="103a7-107">Aplikacja zostanie utworzona przy użyciu platformy sieci Web Django (zobacz alternatywne wersje tego samouczka dla platform [Flask](web-sites-python-create-deploy-flask-app.md) i [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span><span class="sxs-lookup"><span data-stu-id="103a7-107">You will create an application using the Django web framework (see alternate versions of this tutorial for [Flask](web-sites-python-create-deploy-flask-app.md) and [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span></span> <span data-ttu-id="103a7-108">Utworzysz aplikację sieci Web z portalu Azure Marketplace, skonfigurujesz wdrożenie systemu Git i sklonujesz repozytorium lokalnie.</span><span class="sxs-lookup"><span data-stu-id="103a7-108">You will create the web app from the Azure Marketplace, set up Git deployment, and clone the repository locally.</span></span> <span data-ttu-id="103a7-109">Następnie uruchomisz aplikację lokalnie, wprowadzisz zmiany, które zatwierdzisz i wypchniesz na platformę Azure.</span><span class="sxs-lookup"><span data-stu-id="103a7-109">Then you will run the application locally, make changes, commit and push them to Azure.</span></span> <span data-ttu-id="103a7-110">Samouczek pokazuje, jak można to zrobić w systemie Windows lub Mac/Linux.</span><span class="sxs-lookup"><span data-stu-id="103a7-110">The tutorial shows how to do this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="103a7-111">Jeśli chcesz zacząć korzystać z usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź do artykułu [Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), w którym wyjaśniono, jak od razu utworzyć początkową aplikację sieci Web o krótkim okresie istnienia w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="103a7-111">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="103a7-112">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="103a7-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="103a7-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="103a7-113">Prerequisites</span></span>
* <span data-ttu-id="103a7-114">System Windows, Mac lub Linux</span><span class="sxs-lookup"><span data-stu-id="103a7-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="103a7-115">Środowisko Python w wersji 2.7 lub 3.4</span><span class="sxs-lookup"><span data-stu-id="103a7-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="103a7-116">Narzędzia setuptools pip, virtualenv (tylko środowisko Python 2.7)</span><span class="sxs-lookup"><span data-stu-id="103a7-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="103a7-117">Usługa Git</span><span class="sxs-lookup"><span data-stu-id="103a7-117">Git</span></span>
* <span data-ttu-id="103a7-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) — uwaga: ten składnik jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="103a7-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="103a7-119">**Uwaga**: publikowanie TFS nie jest obecnie obsługiwane dla projektów języka Python.</span><span class="sxs-lookup"><span data-stu-id="103a7-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="103a7-120">Windows</span><span class="sxs-lookup"><span data-stu-id="103a7-120">Windows</span></span>
<span data-ttu-id="103a7-121">Jeśli środowisko Python 2.7 lub 3.4 (32-bitowe) nie zostało jeszcze zainstalowane, zalecane jest zainstalowanie [Zestaw Azure SDK dla języka Python w wersji 2.7] lub [zestawu Azure SDK dla języka Python 3.4] przy użyciu Instalatora platformy sieci Web.</span><span class="sxs-lookup"><span data-stu-id="103a7-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span> <span data-ttu-id="103a7-122">Spowoduje to zainstalowanie 32-bitowej wersji środowiska Python, narzędzi setuptools, pip i virtualenv itp. (32-bitowe środowisko Python jest instalowane na maszynach hostów Azure).</span><span class="sxs-lookup"><span data-stu-id="103a7-122">This installs the 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on the Azure host machines).</span></span> <span data-ttu-id="103a7-123">Możesz również pobrać środowisko Python z witryny [python.org].</span><span class="sxs-lookup"><span data-stu-id="103a7-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="103a7-124">W przypadku systemu Git zalecane jest narzędzie [Git dla systemu Windows] lub [Github dla systemu Windows].</span><span class="sxs-lookup"><span data-stu-id="103a7-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span> <span data-ttu-id="103a7-125">Jeśli używasz programu Visual Studio, możesz korzystać ze zintegrowanej obsługi systemu Git.</span><span class="sxs-lookup"><span data-stu-id="103a7-125">If you use Visual Studio, you can use the integrated Git support.</span></span>

<span data-ttu-id="103a7-126">Zalecane jest również zainstalowanie narzędzi [Python Tools 2.2 for Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="103a7-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span> <span data-ttu-id="103a7-127">Jest to opcjonalne, ale jeśli masz program [Program Visual Studio], taki jak bezpłatny program Visual Studio Community 2013 lub Visual Studio Express 2013 for Web, możesz korzystać z doskonałego środowiska IDE języka Python.</span><span class="sxs-lookup"><span data-stu-id="103a7-127">This is optional, but if you have [Visual Studio], including the free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="103a7-128">System Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="103a7-128">Mac/Linux</span></span>
<span data-ttu-id="103a7-129">Środowisko Python i system Git powinny być już zainstalowane, ale upewnij się, że masz środowisko Python 2.7 lub 3.4.</span><span class="sxs-lookup"><span data-stu-id="103a7-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-creation-on-portal"></a><span data-ttu-id="103a7-130">Tworzenie aplikacji sieci Web w portalu</span><span class="sxs-lookup"><span data-stu-id="103a7-130">Web App Creation on Portal</span></span>
<span data-ttu-id="103a7-131">Pierwszym krokiem procedury tworzenia aplikacji jest utworzenie aplikacji sieci Web za pośrednictwem [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="103a7-131">The first step in creating your app is to create the web app via the [Azure Portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="103a7-132">Zaloguj się do Portalu Azure i kliknij przycisk **NOWY** w lewym dolnym rogu.</span><span class="sxs-lookup"><span data-stu-id="103a7-132">Log into the Azure Portal and click the **NEW** button in the bottom left corner.</span></span>
2. <span data-ttu-id="103a7-133">W polu wyszukiwania wpisz „python”.</span><span class="sxs-lookup"><span data-stu-id="103a7-133">In the search box, type "python".</span></span>
3. <span data-ttu-id="103a7-134">W wynikach wyszukiwania wybierz pozycję **Django** (opublikowane przez rozszerzenie PTVS), a następnie kliknij pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="103a7-134">In the search results, select **Django** (published by PTVS), then click **Create**.</span></span>
4. <span data-ttu-id="103a7-135">Skonfiguruj nową aplikację Django, taką jak tworzenie nowego planu usługi App Service i nowej grupy zasobów dla tego planu.</span><span class="sxs-lookup"><span data-stu-id="103a7-135">Configure the new Django app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="103a7-136">Następnie kliknij pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="103a7-136">Then, click **Create**.</span></span>
5. <span data-ttu-id="103a7-137">Skonfiguruj publikowanie w systemie Git dla nowo utworzonej aplikacji sieci Web zgodnie z poniższymi instrukcjami w artykule [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md) (Lokalne wdrażanie przy użyciu systemu Git w usłudze Azure App Service).</span><span class="sxs-lookup"><span data-stu-id="103a7-137">Configure Git publishing for your newly created web app by following the instructions at [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="103a7-138">Omówienie aplikacji</span><span class="sxs-lookup"><span data-stu-id="103a7-138">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="103a7-139">Zawartość repozytorium Git</span><span class="sxs-lookup"><span data-stu-id="103a7-139">Git repository contents</span></span>
<span data-ttu-id="103a7-140">Poniżej przedstawiono pliki w początkowym repozytorium Git, które sklonujemy w następnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="103a7-140">Here's an overview of the files you'll find in the initial Git repository, which we'll clone in the next section.</span></span>

    \app\__init__.py
    \app\forms.py
    \app\models.py
    \app\tests.py
    \app\views.py
    \app\static\content\
    \app\static\fonts\
    \app\static\scripts\
    \app\templates\about.html
    \app\templates\contact.html
    \app\templates\index.html
    \app\templates\layout.html
    \app\templates\login.html
    \app\templates\loginpartial.html
    \DjangoWebProject\__init__.py
    \DjangoWebProject\settings.py
    \DjangoWebProject\urls.py
    \DjangoWebProject\wsgi.py

<span data-ttu-id="103a7-141">Główne źródła dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="103a7-141">Main sources for the application.</span></span> <span data-ttu-id="103a7-142">Składa się z 3 stron (indeks, informacje, kontakt) z układem głównym.</span><span class="sxs-lookup"><span data-stu-id="103a7-142">Consists of 3 pages (index, about, contact) with a master layout.</span></span> <span data-ttu-id="103a7-143">Zawartość statyczna i skrypty obejmują bootstrap, jquery, modernizr i respond.</span><span class="sxs-lookup"><span data-stu-id="103a7-143">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \manage.py

<span data-ttu-id="103a7-144">Obsługa zarządzania lokalnego i serwera projektowego.</span><span class="sxs-lookup"><span data-stu-id="103a7-144">Local management and development server support.</span></span> <span data-ttu-id="103a7-145">Umożliwia to uruchamianie aplikacji lokalnie, synchronizowanie bazy danych itp.</span><span class="sxs-lookup"><span data-stu-id="103a7-145">Use this to run the application locally, synchronize the database, etc.</span></span>

    \db.sqlite3

<span data-ttu-id="103a7-146">Domyślna baza danych.</span><span class="sxs-lookup"><span data-stu-id="103a7-146">Default database.</span></span> <span data-ttu-id="103a7-147">Zawiera tabele niezbędne do uruchomienia aplikacji, ale nie zawiera żadnych użytkowników (należy zsynchronizować bazę danych w celu utworzenia użytkownika).</span><span class="sxs-lookup"><span data-stu-id="103a7-147">Includes the necessary tables for the application to run, but does not contain any users (synchronize the database to create a user).</span></span>

    \DjangoWebProject.pyproj
    \DjangoWebProject.sln

<span data-ttu-id="103a7-148">Pliki projektu do użycia z narzędziami [Python Tools for Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="103a7-148">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="103a7-149">Serwer proxy usług IIS dla środowisk wirtualnych i obsługa zdalnego debugowania narzędzi PTVS.</span><span class="sxs-lookup"><span data-stu-id="103a7-149">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="103a7-150">Pakiety zewnętrzne wymagane przez tę aplikację.</span><span class="sxs-lookup"><span data-stu-id="103a7-150">External packages needed by this application.</span></span> <span data-ttu-id="103a7-151">Skrypt wdrożenia będzie instalować przy użyciu narzędzia pip pakiety wymienione w tym pliku.</span><span class="sxs-lookup"><span data-stu-id="103a7-151">The deployment script will pip install the packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="103a7-152">Pliki konfiguracji programu IIS.</span><span class="sxs-lookup"><span data-stu-id="103a7-152">IIS configuration files.</span></span> <span data-ttu-id="103a7-153">Skrypt wdrożenia użyje odpowiedniego pliku web.x.y.config i skopiuje go jako plik web.config.</span><span class="sxs-lookup"><span data-stu-id="103a7-153">The deployment script will use the appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="103a7-154">Pliki opcjonalne — dostosowywanie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="103a7-154">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-django-customizing-deployment](../../includes/web-sites-python-django-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="103a7-155">Pliki opcjonalne — środowisko uruchomieniowe języka Python</span><span class="sxs-lookup"><span data-stu-id="103a7-155">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="103a7-156">Dodatkowe pliki na serwerze</span><span class="sxs-lookup"><span data-stu-id="103a7-156">Additional files on server</span></span>
<span data-ttu-id="103a7-157">Niektóre pliki istnieją na serwerze, ale nie są dodawane do repozytorium git.</span><span class="sxs-lookup"><span data-stu-id="103a7-157">Some files exist on the server but are not added to the git repository.</span></span> <span data-ttu-id="103a7-158">Są one tworzone przez skrypt wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="103a7-158">These are created by the deployment script.</span></span>

    \web.config

<span data-ttu-id="103a7-159">Plik konfiguracji programu IIS.</span><span class="sxs-lookup"><span data-stu-id="103a7-159">IIS configuration file.</span></span> <span data-ttu-id="103a7-160">Tworzony na podstawie pliku web.x.y.config przy każdym wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="103a7-160">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="103a7-161">Środowisko wirtualne języka Python.</span><span class="sxs-lookup"><span data-stu-id="103a7-161">Python virtual environment.</span></span> <span data-ttu-id="103a7-162">Tworzone podczas wdrażania, jeśli nie istnieje jeszcze zgodne środowisko wirtualne dla aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="103a7-162">Created during deployment if a compatible virtual environment doesn't already exist on the web app.</span></span> <span data-ttu-id="103a7-163">Pakiety wymienione w pliku requirements.txt są instalowane przy użyciu narzędzia pip, ale narzędzie pip pomija instalację, jeśli pakiety zostały już zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="103a7-163">Packages listed in requirements.txt are pip installed, but pip will skip installation if the packages are already installed.</span></span>

<span data-ttu-id="103a7-164">W 3 następnych sekcjach opisano procedury wdrażania aplikacji sieci Web w 3 różnych środowiskach:</span><span class="sxs-lookup"><span data-stu-id="103a7-164">The next 3 sections describe how to proceed with the web app development under 3 different environments:</span></span>

* <span data-ttu-id="103a7-165">System Windows — przy użyciu narzędzi Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="103a7-165">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="103a7-166">System Windows — przy użyciu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="103a7-166">Windows, with command line</span></span>
* <span data-ttu-id="103a7-167">System Mac/Linux — przy użyciu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="103a7-167">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="103a7-168">Wdrażanie aplikacji sieci Web — system Windows — narzędzia Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="103a7-168">Web app development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="103a7-169">Klonowanie repozytorium</span><span class="sxs-lookup"><span data-stu-id="103a7-169">Clone the repository</span></span>
<span data-ttu-id="103a7-170">Najpierw sklonuj repozytorium przy użyciu adresu URL podanego w witrynie Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="103a7-170">First, clone the repository using the URL provided on the Azure Portal.</span></span> <span data-ttu-id="103a7-171">Aby uzyskać więcej informacji, zobacz [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md) (Lokalne wdrażanie przy użyciu systemu Git w usłudze Azure App Service).</span><span class="sxs-lookup"><span data-stu-id="103a7-171">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="103a7-172">Otwórz plik rozwiązania (SLN), który znajduje się w folderze głównym repozytorium.</span><span class="sxs-lookup"><span data-stu-id="103a7-172">Open the solution file (.sln) that is included in the root of the repository.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-solution-django.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="103a7-173">Tworzenie środowiska wirtualnego</span><span class="sxs-lookup"><span data-stu-id="103a7-173">Create virtual environment</span></span>
<span data-ttu-id="103a7-174">Teraz utwórz środowisko wirtualne dla wdrożenia lokalnego.</span><span class="sxs-lookup"><span data-stu-id="103a7-174">Now we'll create a virtual environment for local development.</span></span> <span data-ttu-id="103a7-175">Kliknij prawym przyciskiem myszy pozycję **Środowiska Python** i wybierz pozycję **Dodaj środowisko wirtualne**.</span><span class="sxs-lookup"><span data-stu-id="103a7-175">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="103a7-176">Upewnij się, że nazwa środowiska to `env`.</span><span class="sxs-lookup"><span data-stu-id="103a7-176">Make sure the name of the environment is `env`.</span></span>
* <span data-ttu-id="103a7-177">Wybierz interpreter podstawowy.</span><span class="sxs-lookup"><span data-stu-id="103a7-177">Select the base interpreter.</span></span> <span data-ttu-id="103a7-178">Upewnij się, że jest używana ta sama wersja środowiska Python, którą wybrano dla aplikacji sieci Web (w pliku runtime.txt lub bloku **Ustawienia aplikacji** dla aplikacji sieci Web w Portalu Azure).</span><span class="sxs-lookup"><span data-stu-id="103a7-178">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span></span>
* <span data-ttu-id="103a7-179">Upewnij się, że opcja pobierania i instalowania pakietów została zaznaczona.</span><span class="sxs-lookup"><span data-stu-id="103a7-179">Make sure the option to download and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="103a7-180">Kliknij pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="103a7-180">Click **Create**.</span></span> <span data-ttu-id="103a7-181">Spowoduje to utworzenie środowiska wirtualnego i zainstalowanie składników zależnych wymienionych w pliku requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="103a7-181">This will create the virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="create-a-superuser"></a><span data-ttu-id="103a7-182">Tworzenie administratora</span><span class="sxs-lookup"><span data-stu-id="103a7-182">Create a superuser</span></span>
<span data-ttu-id="103a7-183">Baza danych dołączona do aplikacji nie zawiera definicji administratora.</span><span class="sxs-lookup"><span data-stu-id="103a7-183">The database included with the application does not have any superuser defined.</span></span> <span data-ttu-id="103a7-184">Aby można było używać funkcji logowania w aplikacji lub interfejsu administracyjnego Django (jeśli zostanie włączony przez użytkownika), musisz utworzyć administratora.</span><span class="sxs-lookup"><span data-stu-id="103a7-184">In order to use the sign-in functionality in the application, or the Django admin interface (if you decide to enable it), you'll need to create a superuser.</span></span>

<span data-ttu-id="103a7-185">Uruchom poniższe polecenie z poziomu wiersza polecenia w folderze projektu:</span><span class="sxs-lookup"><span data-stu-id="103a7-185">Run this from the command-line from your project folder:</span></span>

    env\scripts\python manage.py createsuperuser

<span data-ttu-id="103a7-186">Postępuj zgodnie z monitami, aby ustawić nazwę użytkownika, hasło itp.</span><span class="sxs-lookup"><span data-stu-id="103a7-186">Follow the prompts to set the user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="103a7-187">Uruchamianie przy użyciu serwera projektowego</span><span class="sxs-lookup"><span data-stu-id="103a7-187">Run using development server</span></span>
<span data-ttu-id="103a7-188">Naciśnij klawisz F5, aby rozpocząć debugowanie. Spowoduje to automatyczne otwarcie przeglądarki sieci Web i wyświetlenie strony uruchomionej lokalnie.</span><span class="sxs-lookup"><span data-stu-id="103a7-188">Press F5 to start debugging, and your web browser will open automatically to the page running locally.</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

<span data-ttu-id="103a7-189">Można ustawiać punkty przerwania w źródłach, używać okien wyrażeń kontrolnych itp. Zapoznaj się z [Dokumentacja narzędzi Python Tools for Visual Studio], aby uzyskać więcej informacji na temat różnych funkcji.</span><span class="sxs-lookup"><span data-stu-id="103a7-189">You can set breakpoints in the sources, use the watch windows, etc. See the [Python Tools for Visual Studio Documentation] for more information on the various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="103a7-190">Wprowadzanie zmian</span><span class="sxs-lookup"><span data-stu-id="103a7-190">Make changes</span></span>
<span data-ttu-id="103a7-191">Teraz możesz eksperymentować, wprowadzając zmiany w źródłach i/lub szablonach aplikacji.</span><span class="sxs-lookup"><span data-stu-id="103a7-191">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="103a7-192">Po przetestowaniu wprowadzonych zmian zatwierdź je w repozytorium Git:</span><span class="sxs-lookup"><span data-stu-id="103a7-192">After you've tested your changes, commit them to the Git repository:</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-commit-django.png)

### <a name="install-more-packages"></a><span data-ttu-id="103a7-193">Instalowanie dodatkowych pakietów</span><span class="sxs-lookup"><span data-stu-id="103a7-193">Install more packages</span></span>
<span data-ttu-id="103a7-194">Aplikacja może mieć zależności poza środowiskiem Python i platformą Django.</span><span class="sxs-lookup"><span data-stu-id="103a7-194">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="103a7-195">Możesz zainstalować dodatkowe pakiety przy użyciu narzędzia pip.</span><span class="sxs-lookup"><span data-stu-id="103a7-195">You can install additional packages using pip.</span></span> <span data-ttu-id="103a7-196">Aby zainstalować pakiet, kliknij prawym przyciskiem myszy środowisko wirtualne i wybierz pozycję **Zainstaluj pakiet języka Python**.</span><span class="sxs-lookup"><span data-stu-id="103a7-196">To install a package, right-click on the virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="103a7-197">Aby na przykład zainstalować zestaw Azure SDK dla języka Python zapewniający dostęp do magazynu Azure, magistrali usług i innych usług Azure, wprowadź `azure`:</span><span class="sxs-lookup"><span data-stu-id="103a7-197">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-install-package-dialog.png)

<span data-ttu-id="103a7-198">Kliknij prawym przyciskiem myszy środowisko wirtualne i wybierz pozycję **Generuj plik requirements.txt**, aby zaktualizować plik requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="103a7-198">Right-click on the virtual environment and select **Generate requirements.txt** to update requirements.txt.</span></span>

<span data-ttu-id="103a7-199">Następnie zatwierdź zmiany w pliku requirements.txt w repozytorium Git.</span><span class="sxs-lookup"><span data-stu-id="103a7-199">Then, commit the changes to requirements.txt to the Git repository.</span></span>

### <a name="deploy-to-azure"></a><span data-ttu-id="103a7-200">Wdrażanie na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="103a7-200">Deploy to Azure</span></span>
<span data-ttu-id="103a7-201">Aby wyzwolić wdrożenie, kliknij pozycję **Synchronizuj** lub **Wypchnij**.</span><span class="sxs-lookup"><span data-stu-id="103a7-201">To trigger a deployment, click on **Sync** or **Push**.</span></span> <span data-ttu-id="103a7-202">Synchronizacja obejmuje zarówno wypychanie, jak i ściąganie.</span><span class="sxs-lookup"><span data-stu-id="103a7-202">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-git-push.png)

<span data-ttu-id="103a7-203">Pierwsze wdrożenie trwa dłużej, ponieważ obejmuje tworzenie środowiska wirtualnego, instalowanie pakietów itp.</span><span class="sxs-lookup"><span data-stu-id="103a7-203">The first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="103a7-204">Program Visual Studio nie wyświetla postępu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="103a7-204">Visual Studio doesn't show the progress of the deployment.</span></span> <span data-ttu-id="103a7-205">Jeśli chcesz przejrzeć dane wyjściowe, zobacz sekcję [Rozwiązywanie problemów — wdrożenie](#troubleshooting-deployment).</span><span class="sxs-lookup"><span data-stu-id="103a7-205">If you'd like to review the output, see the section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="103a7-206">Przejdź do adresu URL platformy Azure, aby przejrzeć wprowadzone zmiany.</span><span class="sxs-lookup"><span data-stu-id="103a7-206">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="103a7-207">Wdrażanie aplikacji sieci Web — system Windows — wiersz polecenia</span><span class="sxs-lookup"><span data-stu-id="103a7-207">Web app development - Windows - command line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="103a7-208">Klonowanie repozytorium</span><span class="sxs-lookup"><span data-stu-id="103a7-208">Clone the repository</span></span>
<span data-ttu-id="103a7-209">Najpierw sklonuj repozytorium przy użyciu adresu URL podanego w witrynie Azure Portal i dodaj repozytorium Azure jako repozytorium zdalne.</span><span class="sxs-lookup"><span data-stu-id="103a7-209">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="103a7-210">Aby uzyskać więcej informacji, zobacz [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md) (Lokalne wdrażanie przy użyciu systemu Git w usłudze Azure App Service).</span><span class="sxs-lookup"><span data-stu-id="103a7-210">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url>

### <a name="create-virtual-environment"></a><span data-ttu-id="103a7-211">Tworzenie środowiska wirtualnego</span><span class="sxs-lookup"><span data-stu-id="103a7-211">Create virtual environment</span></span>
<span data-ttu-id="103a7-212">Zostanie utworzone nowe środowisko wirtualne dla celów wdrożenia (nie należy dodawać go do repozytorium).</span><span class="sxs-lookup"><span data-stu-id="103a7-212">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span> <span data-ttu-id="103a7-213">Nie można zmieniać lokalizacji wirtualnych środowisk języka Python, dlatego każdy deweloper pracujący nad aplikacją tworzy własne środowisko lokalnie.</span><span class="sxs-lookup"><span data-stu-id="103a7-213">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="103a7-214">Upewnij się, że jest używana ta sama wersja środowiska Python, którą wybrano dla aplikacji sieci Web (w pliku runtime.txt lub bloku Ustawienia aplikacji dla aplikacji sieci Web w Portalu Azure).</span><span class="sxs-lookup"><span data-stu-id="103a7-214">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the Application Settings blade of your web app in the Azure Portal).</span></span>

<span data-ttu-id="103a7-215">Dla środowiska Python w wersji 2.7:</span><span class="sxs-lookup"><span data-stu-id="103a7-215">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="103a7-216">Dla środowiska Python w wersji 3.4:</span><span class="sxs-lookup"><span data-stu-id="103a7-216">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="103a7-217">Zainstaluj pakiety zewnętrzne wymagane przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="103a7-217">Install any external packages required by your application.</span></span> <span data-ttu-id="103a7-218">Korzystając z pliku requirements.txt w folderze głównym repozytorium, możesz instalować pakiety w środowisku wirtualnym:</span><span class="sxs-lookup"><span data-stu-id="103a7-218">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="create-a-superuser"></a><span data-ttu-id="103a7-219">Tworzenie administratora</span><span class="sxs-lookup"><span data-stu-id="103a7-219">Create a superuser</span></span>
<span data-ttu-id="103a7-220">Baza danych dołączona do aplikacji nie zawiera definicji administratora.</span><span class="sxs-lookup"><span data-stu-id="103a7-220">The database included with the application does not have any superuser defined.</span></span> <span data-ttu-id="103a7-221">Aby można było używać funkcji logowania w aplikacji lub interfejsu administracyjnego Django (jeśli zostanie włączony przez użytkownika), musisz utworzyć administratora.</span><span class="sxs-lookup"><span data-stu-id="103a7-221">In order to use the sign-in functionality in the application, or the Django admin interface (if you decide to enable it), you'll need to create a superuser.</span></span>

<span data-ttu-id="103a7-222">Uruchom poniższe polecenie z poziomu wiersza polecenia w folderze projektu:</span><span class="sxs-lookup"><span data-stu-id="103a7-222">Run this from the command-line from your project folder:</span></span>

    env\scripts\python manage.py createsuperuser

<span data-ttu-id="103a7-223">Postępuj zgodnie z monitami, aby ustawić nazwę użytkownika, hasło itp.</span><span class="sxs-lookup"><span data-stu-id="103a7-223">Follow the prompts to set the user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="103a7-224">Uruchamianie przy użyciu serwera projektowego</span><span class="sxs-lookup"><span data-stu-id="103a7-224">Run using development server</span></span>
<span data-ttu-id="103a7-225">Możesz uruchomić aplikację na serwerze projektowym przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="103a7-225">You can launch the application under a development server with the following command:</span></span>

    env\scripts\python manage.py runserver

<span data-ttu-id="103a7-226">Na konsoli zostanie wyświetlony adres URL i port nasłuchiwany przez serwer:</span><span class="sxs-lookup"><span data-stu-id="103a7-226">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-run-local-django.png)

<span data-ttu-id="103a7-227">Następnie otwórz w przeglądarce sieci Web stronę wskazywaną przez ten adres URL.</span><span class="sxs-lookup"><span data-stu-id="103a7-227">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

### <a name="make-changes"></a><span data-ttu-id="103a7-228">Wprowadzanie zmian</span><span class="sxs-lookup"><span data-stu-id="103a7-228">Make changes</span></span>
<span data-ttu-id="103a7-229">Teraz możesz eksperymentować, wprowadzając zmiany w źródłach i/lub szablonach aplikacji.</span><span class="sxs-lookup"><span data-stu-id="103a7-229">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="103a7-230">Po przetestowaniu wprowadzonych zmian zatwierdź je w repozytorium Git:</span><span class="sxs-lookup"><span data-stu-id="103a7-230">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="103a7-231">Instalowanie dodatkowych pakietów</span><span class="sxs-lookup"><span data-stu-id="103a7-231">Install more packages</span></span>
<span data-ttu-id="103a7-232">Aplikacja może mieć zależności poza środowiskiem Python i platformą Django.</span><span class="sxs-lookup"><span data-stu-id="103a7-232">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="103a7-233">Możesz zainstalować dodatkowe pakiety przy użyciu narzędzia pip.</span><span class="sxs-lookup"><span data-stu-id="103a7-233">You can install additional packages using pip.</span></span> <span data-ttu-id="103a7-234">Aby na przykład zainstalować zestaw Azure SDK dla języka Python zapewniający dostęp do magazynu Azure, magistrali usług i innych usług Azure, wpisz:</span><span class="sxs-lookup"><span data-stu-id="103a7-234">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="103a7-235">Pamiętaj o zaktualizowaniu pliku requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="103a7-235">Make sure to update requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="103a7-236">Zatwierdź zmiany:</span><span class="sxs-lookup"><span data-stu-id="103a7-236">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="103a7-237">Wdrażanie na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="103a7-237">Deploy to Azure</span></span>
<span data-ttu-id="103a7-238">Aby wyzwolić wdrożenie, wypchnij zmiany na platformę Azure:</span><span class="sxs-lookup"><span data-stu-id="103a7-238">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="103a7-239">Zostaną wyświetlone dane wyjściowe skryptu wdrożenia, łącznie z tworzeniem środowiska wirtualnego, instalowaniem pakietów i tworzeniem pliku web.config.</span><span class="sxs-lookup"><span data-stu-id="103a7-239">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="103a7-240">Przejdź do adresu URL platformy Azure, aby przejrzeć wprowadzone zmiany.</span><span class="sxs-lookup"><span data-stu-id="103a7-240">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="103a7-241">Wdrażanie aplikacji sieci Web — system Mac/Linux — wiersz polecenia</span><span class="sxs-lookup"><span data-stu-id="103a7-241">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="103a7-242">Klonowanie repozytorium</span><span class="sxs-lookup"><span data-stu-id="103a7-242">Clone the repository</span></span>
<span data-ttu-id="103a7-243">Najpierw sklonuj repozytorium przy użyciu adresu URL podanego w witrynie Azure Portal i dodaj repozytorium Azure jako repozytorium zdalne.</span><span class="sxs-lookup"><span data-stu-id="103a7-243">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="103a7-244">Aby uzyskać więcej informacji, zobacz [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md) (Lokalne wdrażanie przy użyciu systemu Git w usłudze Azure App Service).</span><span class="sxs-lookup"><span data-stu-id="103a7-244">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url>

### <a name="create-virtual-environment"></a><span data-ttu-id="103a7-245">Tworzenie środowiska wirtualnego</span><span class="sxs-lookup"><span data-stu-id="103a7-245">Create virtual environment</span></span>
<span data-ttu-id="103a7-246">Zostanie utworzone nowe środowisko wirtualne dla celów wdrożenia (nie należy dodawać go do repozytorium).</span><span class="sxs-lookup"><span data-stu-id="103a7-246">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span> <span data-ttu-id="103a7-247">Nie można zmieniać lokalizacji wirtualnych środowisk języka Python, dlatego każdy deweloper pracujący nad aplikacją tworzy własne środowisko lokalnie.</span><span class="sxs-lookup"><span data-stu-id="103a7-247">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="103a7-248">Upewnij się, że jest używana ta sama wersja środowiska Python, którą wybrano dla aplikacji sieci Web (w pliku runtime.txt lub bloku Ustawienia aplikacji dla aplikacji sieci Web w Portalu Azure).</span><span class="sxs-lookup"><span data-stu-id="103a7-248">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the Application Settings blade of your web app in the Azure Portal).</span></span>

<span data-ttu-id="103a7-249">Dla środowiska Python w wersji 2.7:</span><span class="sxs-lookup"><span data-stu-id="103a7-249">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="103a7-250">Dla środowiska Python w wersji 3.4:</span><span class="sxs-lookup"><span data-stu-id="103a7-250">For Python 3.4:</span></span>

    python -m venv env

<span data-ttu-id="103a7-251">lub</span><span class="sxs-lookup"><span data-stu-id="103a7-251">or</span></span>

    pyvenv env

<span data-ttu-id="103a7-252">Zainstaluj pakiety zewnętrzne wymagane przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="103a7-252">Install any external packages required by your application.</span></span> <span data-ttu-id="103a7-253">Korzystając z pliku requirements.txt w folderze głównym repozytorium, możesz instalować pakiety w środowisku wirtualnym:</span><span class="sxs-lookup"><span data-stu-id="103a7-253">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="create-a-superuser"></a><span data-ttu-id="103a7-254">Tworzenie administratora</span><span class="sxs-lookup"><span data-stu-id="103a7-254">Create a superuser</span></span>
<span data-ttu-id="103a7-255">Baza danych dołączona do aplikacji nie zawiera definicji administratora.</span><span class="sxs-lookup"><span data-stu-id="103a7-255">The database included with the application does not have any superuser defined.</span></span> <span data-ttu-id="103a7-256">Aby można było używać funkcji logowania w aplikacji lub interfejsu administracyjnego Django (jeśli zostanie włączony przez użytkownika), musisz utworzyć administratora.</span><span class="sxs-lookup"><span data-stu-id="103a7-256">In order to use the sign-in functionality in the application, or the Django admin interface (if you decide to enable it), you'll need to create a superuser.</span></span>

<span data-ttu-id="103a7-257">Uruchom poniższe polecenie z poziomu wiersza polecenia w folderze projektu:</span><span class="sxs-lookup"><span data-stu-id="103a7-257">Run this from the command-line from your project folder:</span></span>

    env/bin/python manage.py createsuperuser

<span data-ttu-id="103a7-258">Postępuj zgodnie z monitami, aby ustawić nazwę użytkownika, hasło itp.</span><span class="sxs-lookup"><span data-stu-id="103a7-258">Follow the prompts to set the user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="103a7-259">Uruchamianie przy użyciu serwera projektowego</span><span class="sxs-lookup"><span data-stu-id="103a7-259">Run using development server</span></span>
<span data-ttu-id="103a7-260">Możesz uruchomić aplikację na serwerze projektowym przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="103a7-260">You can launch the application under a development server with the following command:</span></span>

    env/bin/python manage.py runserver

<span data-ttu-id="103a7-261">Na konsoli zostanie wyświetlony adres URL i port nasłuchiwany przez serwer:</span><span class="sxs-lookup"><span data-stu-id="103a7-261">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-django-app/mac-run-local-django.png)

<span data-ttu-id="103a7-262">Następnie otwórz w przeglądarce sieci Web stronę wskazywaną przez ten adres URL.</span><span class="sxs-lookup"><span data-stu-id="103a7-262">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-django-app/mac-browser-django.png)

### <a name="make-changes"></a><span data-ttu-id="103a7-263">Wprowadzanie zmian</span><span class="sxs-lookup"><span data-stu-id="103a7-263">Make changes</span></span>
<span data-ttu-id="103a7-264">Teraz możesz eksperymentować, wprowadzając zmiany w źródłach i/lub szablonach aplikacji.</span><span class="sxs-lookup"><span data-stu-id="103a7-264">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="103a7-265">Po przetestowaniu wprowadzonych zmian zatwierdź je w repozytorium Git:</span><span class="sxs-lookup"><span data-stu-id="103a7-265">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="103a7-266">Instalowanie dodatkowych pakietów</span><span class="sxs-lookup"><span data-stu-id="103a7-266">Install more packages</span></span>
<span data-ttu-id="103a7-267">Aplikacja może mieć zależności poza środowiskiem Python i platformą Django.</span><span class="sxs-lookup"><span data-stu-id="103a7-267">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="103a7-268">Możesz zainstalować dodatkowe pakiety przy użyciu narzędzia pip.</span><span class="sxs-lookup"><span data-stu-id="103a7-268">You can install additional packages using pip.</span></span> <span data-ttu-id="103a7-269">Aby na przykład zainstalować zestaw Azure SDK dla języka Python zapewniający dostęp do magazynu Azure, magistrali usług i innych usług Azure, wpisz:</span><span class="sxs-lookup"><span data-stu-id="103a7-269">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="103a7-270">Pamiętaj o zaktualizowaniu pliku requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="103a7-270">Make sure to update requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="103a7-271">Zatwierdź zmiany:</span><span class="sxs-lookup"><span data-stu-id="103a7-271">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="103a7-272">Wdrażanie na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="103a7-272">Deploy to Azure</span></span>
<span data-ttu-id="103a7-273">Aby wyzwolić wdrożenie, wypchnij zmiany na platformę Azure:</span><span class="sxs-lookup"><span data-stu-id="103a7-273">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="103a7-274">Zostaną wyświetlone dane wyjściowe skryptu wdrożenia, łącznie z tworzeniem środowiska wirtualnego, instalowaniem pakietów i tworzeniem pliku web.config.</span><span class="sxs-lookup"><span data-stu-id="103a7-274">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="103a7-275">Przejdź do adresu URL platformy Azure, aby przejrzeć wprowadzone zmiany.</span><span class="sxs-lookup"><span data-stu-id="103a7-275">Browse to the Azure URL to view your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="103a7-276">Rozwiązywanie problemów — instalowanie pakietów</span><span class="sxs-lookup"><span data-stu-id="103a7-276">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="103a7-277">Rozwiązywanie problemów — środowisko wirtualne</span><span class="sxs-lookup"><span data-stu-id="103a7-277">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="troubleshooting---static-files"></a><span data-ttu-id="103a7-278">Rozwiązywanie problemów — pliki statyczne</span><span class="sxs-lookup"><span data-stu-id="103a7-278">Troubleshooting - Static Files</span></span>
<span data-ttu-id="103a7-279">Platforma Django korzysta z koncepcji zbierania plików statycznych.</span><span class="sxs-lookup"><span data-stu-id="103a7-279">Django has the concept of collecting static files.</span></span> <span data-ttu-id="103a7-280">Polega to na skopiowaniu wszystkich plików statycznych z oryginalnej lokalizacji do pojedynczego folderu.</span><span class="sxs-lookup"><span data-stu-id="103a7-280">This takes all the static files from their original location and copies them to a single folder.</span></span> <span data-ttu-id="103a7-281">W przypadku tej aplikacji są one kopiowane do folderu `/static`.</span><span class="sxs-lookup"><span data-stu-id="103a7-281">For this application, they are copied to `/static`.</span></span>

<span data-ttu-id="103a7-282">Ta operacja jest wykonywana, ponieważ pliki statyczne mogą pochodzić z różnych „aplikacji” Django.</span><span class="sxs-lookup"><span data-stu-id="103a7-282">This is done because static files may come from different Django 'apps'.</span></span> <span data-ttu-id="103a7-283">Na przykład pliki statyczne z interfejsów administracyjnych Django znajdują się w podfolderze biblioteki Django w środowisku wirtualnym.</span><span class="sxs-lookup"><span data-stu-id="103a7-283">For example, the static files from the Django admin interfaces are located in a Django library subfolder in the virtual environment.</span></span> <span data-ttu-id="103a7-284">Pliki statyczne zdefiniowane przez tę aplikację znajdują się w folderze `/app/static`.</span><span class="sxs-lookup"><span data-stu-id="103a7-284">Static files defined by this application are located in `/app/static`.</span></span> <span data-ttu-id="103a7-285">W przypadku użycia dodatkowych „aplikacji” Django pliki statyczne będą znajdować się w kilku miejscach.</span><span class="sxs-lookup"><span data-stu-id="103a7-285">As you use more Django 'apps', you'll have static files located in multiple places.</span></span>

<span data-ttu-id="103a7-286">Aplikacja uruchomiona w trybie debugowania udostępnia pliki statyczne z oryginalnej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="103a7-286">When running the application in debug mode, the application serves the static files from their original location.</span></span>

<span data-ttu-id="103a7-287">Aplikacja uruchomiona w trybie przygotowania do wydania **nie** udostępnia plików statycznych.</span><span class="sxs-lookup"><span data-stu-id="103a7-287">When running the application in release mode, the application does **not** serve the static files.</span></span> <span data-ttu-id="103a7-288">Serwer sieci Web jest zobowiązany do udostępniania plików.</span><span class="sxs-lookup"><span data-stu-id="103a7-288">It is the responsibility of the web server to serve the files.</span></span> <span data-ttu-id="103a7-289">W przypadku tej aplikacji usługa IIS udostępnia pliki statyczne z folderu `/static`.</span><span class="sxs-lookup"><span data-stu-id="103a7-289">For this application, IIS will serve the static files from `/static`.</span></span>

<span data-ttu-id="103a7-290">Pliki statyczne są zbierane automatycznie w ramach skryptu wdrożenia, a uprzednio zebrane pliki są czyszczone.</span><span class="sxs-lookup"><span data-stu-id="103a7-290">The collection of static files is done automatically as part of the deployment script, clearing previously collected files.</span></span> <span data-ttu-id="103a7-291">Oznacza to, że pliki są zbierane przy każdym wdrożeniu, co powoduje nieznaczne spowolnienie wdrażania, ale gwarantuje, że nieaktualne pliki będą niedostępne i nie wystąpi potencjalny problem z zabezpieczeniami.</span><span class="sxs-lookup"><span data-stu-id="103a7-291">This means the collection occurs on every deployment, slowing down deployment a bit, but it ensures that obsolete files won't be available, avoiding a potential security issue.</span></span>

<span data-ttu-id="103a7-292">Jeśli chcesz pominąć zbieranie plików statycznych dla aplikacji Django:</span><span class="sxs-lookup"><span data-stu-id="103a7-292">If you want to skip collection of static files for your Django application:</span></span>

    \.skipDjango

<span data-ttu-id="103a7-293">Musisz zebrać pliki ręcznie na komputerze lokalnym:</span><span class="sxs-lookup"><span data-stu-id="103a7-293">Then you'll need to do the collection manually on your local machine:</span></span>

    env\scripts\python manage.py collectstatic

<span data-ttu-id="103a7-294">Następnie usuń folder `\static` z pliku `.gitignore` i dodaj go do repozytorium Git.</span><span class="sxs-lookup"><span data-stu-id="103a7-294">Then remove the `\static` folder from `.gitignore` and add it to the Git repository.</span></span>

## <a name="troubleshooting---settings"></a><span data-ttu-id="103a7-295">Rozwiązywanie problemów — ustawienia</span><span class="sxs-lookup"><span data-stu-id="103a7-295">Troubleshooting - Settings</span></span>
<span data-ttu-id="103a7-296">Różne ustawienia dla aplikacji można zmienić w pliku `DjangoWebProject/settings.py`.</span><span class="sxs-lookup"><span data-stu-id="103a7-296">Various settings for the application can be changed in `DjangoWebProject/settings.py`.</span></span>

<span data-ttu-id="103a7-297">Dla wygody deweloperów tryb debugowania jest włączony.</span><span class="sxs-lookup"><span data-stu-id="103a7-297">For developer convenience, debug mode is enabled.</span></span> <span data-ttu-id="103a7-298">Jedną z zalet tego rozwiązania jest możliwość wyświetlania obrazów i innej zawartości statycznej podczas uruchamiania lokalnego bez konieczności zbierania plików statycznych.</span><span class="sxs-lookup"><span data-stu-id="103a7-298">One nice side effect of that is you'll be able to see images and other static content when running locally, without having to collect static files.</span></span>

<span data-ttu-id="103a7-299">Aby wyłączyć tryb debugowania:</span><span class="sxs-lookup"><span data-stu-id="103a7-299">To disable debug mode:</span></span>

    DEBUG = False

<span data-ttu-id="103a7-300">Po wyłączeniu debugowania konieczne jest zaktualizowanie wartości `ALLOWED_HOSTS` w celu uwzględnienia nazwy hosta Azure.</span><span class="sxs-lookup"><span data-stu-id="103a7-300">When debug is disabled, the value for `ALLOWED_HOSTS` needs to be updated to include the Azure host name.</span></span> <span data-ttu-id="103a7-301">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="103a7-301">For example:</span></span>

    ALLOWED_HOSTS = (
        'pythonapp.azurewebsites.net',
    )

<span data-ttu-id="103a7-302">lub zezwolenie na dowolne hosty:</span><span class="sxs-lookup"><span data-stu-id="103a7-302">or to enable any:</span></span>

    ALLOWED_HOSTS = (
        '*',
    )

<span data-ttu-id="103a7-303">W praktyce może być konieczne wykonanie bardziej złożonych czynności w celu uwzględnienia przełączania trybów debugowania i przygotowania do wydania oraz pobrania nazwy hosta.</span><span class="sxs-lookup"><span data-stu-id="103a7-303">In practice, you may want to do something more complex to deal with switching between debug and release mode, and getting the host name.</span></span>

<span data-ttu-id="103a7-304">Można ustawić zmienne środowiskowe za pośrednictwem strony **KONFIGURACJA** Portalu Azure w sekcji **Ustawienia aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="103a7-304">You can set environment variables through the Azure portal **CONFIGURE** page, in the **app settings** section.</span></span>  <span data-ttu-id="103a7-305">Może to być przydatne do ustawiania wartości, które nie powinny pojawiać się w źródłach (parametry połączenia, hasła itp.) lub powinny zostać ustawione inaczej dla platformy Azure i komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="103a7-305">This can be useful for setting values that you may not want to appear in the sources (connection strings, passwords, etc), or that you want to set differently between Azure and your local machine.</span></span> <span data-ttu-id="103a7-306">W pliku `settings.py` możesz wykonać zapytanie dotyczące zmiennych środowiskowych przy użyciu pliku `os.getenv`.</span><span class="sxs-lookup"><span data-stu-id="103a7-306">In `settings.py`, you can query the environment variables using `os.getenv`.</span></span>

## <a name="using-a-database"></a><span data-ttu-id="103a7-307">Korzystanie z bazy danych</span><span class="sxs-lookup"><span data-stu-id="103a7-307">Using a Database</span></span>
<span data-ttu-id="103a7-308">Bazy danych dołączona do aplikacji jest bazą danych SQLite.</span><span class="sxs-lookup"><span data-stu-id="103a7-308">The database that is included with the application is a sqlite database.</span></span> <span data-ttu-id="103a7-309">Jest to wygodna i przydatna domyślna baza danych, której można użyć dla wdrożenia, ponieważ prawie nie wymaga konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="103a7-309">This is a convenient and useful default database to use for development, as it requires almost no setup.</span></span> <span data-ttu-id="103a7-310">Baza danych jest przechowywana w pliku db.sqlite3 w folderze projektu.</span><span class="sxs-lookup"><span data-stu-id="103a7-310">The database is stored in the db.sqlite3 file in the project folder.</span></span>

<span data-ttu-id="103a7-311">Platforma Azure oferuje usługi bazy danych, które są łatwe w użyciu z poziomu aplikacji Django.</span><span class="sxs-lookup"><span data-stu-id="103a7-311">Azure provides database services which are easy to use from a Django application.</span></span> <span data-ttu-id="103a7-312">Samouczki dotyczące użycia [SQL Database] i [MySQL] z poziomu aplikacji Django przedstawiają kroki niezbędne do utworzenia usługi bazy danych, zmiany ustawień bazy danych w pliku `DjangoWebProject/settings.py` i identyfikacji bibliotek wymaganych do instalacji.</span><span class="sxs-lookup"><span data-stu-id="103a7-312">Tutorials for using [SQL Database] and [MySQL] from a Django application show the steps necessary to create the database service, change the database settings in `DjangoWebProject/settings.py`, and the libraries required to install.</span></span>

<span data-ttu-id="103a7-313">Oczywiście jeśli wolisz zarządzać własnymi serwerami bazy danych, możesz to zrobić przy użyciu maszyn wirtualnych systemu Windows lub Linux działających na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="103a7-313">Of course, if you prefer to manage your own database servers, you can do so using Windows or Linux virtual machines running on Azure.</span></span>

## <a name="django-admin-interface"></a><span data-ttu-id="103a7-314">Interfejs administracyjny Django</span><span class="sxs-lookup"><span data-stu-id="103a7-314">Django Admin Interface</span></span>
<span data-ttu-id="103a7-315">Po rozpoczęciu tworzenia modeli może być konieczne wypełnienie bazy danych określonymi danymi.</span><span class="sxs-lookup"><span data-stu-id="103a7-315">Once you start building your models, you'll want to populate the database with some data.</span></span> <span data-ttu-id="103a7-316">Prostą metodą interakcyjnego dodawania i edytowania zawartości jest użycie interfejsu administracyjnego Django.</span><span class="sxs-lookup"><span data-stu-id="103a7-316">An easy way to do add and edit content interactively is to use the Django administration interface.</span></span>

<span data-ttu-id="103a7-317">Kod dla interfejsu administracyjnego został umieszczony w komentarzach w źródłach aplikacji, ale jest jednoznacznie oznaczony, dlatego możesz go łatwo uaktywnić (wyszukaj „admin”).</span><span class="sxs-lookup"><span data-stu-id="103a7-317">The code for the admin interface is commented out in the application sources, but it's clearly marked so you can easily enable it (search for 'admin').</span></span>

<span data-ttu-id="103a7-318">Po uaktywnieniu tego kodu zsynchronizuj bazę danych, uruchom aplikację i przejdź do folderu `/admin`.</span><span class="sxs-lookup"><span data-stu-id="103a7-318">After it's enabled, synchronize the database, run the application and navigate to `/admin`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="103a7-319">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="103a7-319">Next Steps</span></span>
<span data-ttu-id="103a7-320">Aby dowiedzieć się więcej na temat struktury Django i narzędzi Python Tools for Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="103a7-320">Follow these links to learn more about Django and Python Tools for Visual Studio:</span></span>

* <span data-ttu-id="103a7-321">[Dokumentacja platformy Django]</span><span class="sxs-lookup"><span data-stu-id="103a7-321">[Django Documentation]</span></span>
* <span data-ttu-id="103a7-322">[Dokumentacja narzędzi Python Tools for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="103a7-322">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="103a7-323">Aby uzyskać informacje na temat baz danych SQL Database i MySQL:</span><span class="sxs-lookup"><span data-stu-id="103a7-323">For information on using SQL Database and MySQL:</span></span>

* <span data-ttu-id="103a7-324">[Obsługa platformy Django i bazy danych MySQL na platformie Azure przy użyciu narzędzi Python Tools for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="103a7-324">[Django and MySQL on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="103a7-325">[Obsługa platformy Django i bazy danych SQL Database na platformie Azure przy użyciu narzędzi Python Tools for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="103a7-325">[Django and SQL Database on Azure with Python Tools for Visual Studio]</span></span>

<span data-ttu-id="103a7-326">Więcej informacji możesz znaleźć w [Centrum deweloperów języka Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="103a7-326">For more information, see the [Python Developer Center](/develop/python/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="103a7-327">Co zostało zmienione</span><span class="sxs-lookup"><span data-stu-id="103a7-327">What's changed</span></span>
* <span data-ttu-id="103a7-328">Przewodnik dotyczący przejścia od usługi Witryny sieci Web do usługi App Service można znaleźć w temacie [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714) (Usługa Azure App Service i jej wpływ na istniejące usługi platformy Azure).</span><span class="sxs-lookup"><span data-stu-id="103a7-328">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Obsługa platformy Django i bazy danych MySQL na platformie Azure przy użyciu narzędzi Python Tools for Visual Studio]: web-sites-python-ptvs-django-mysql.md
[Obsługa platformy Django i bazy danych SQL Database na platformie Azure przy użyciu narzędzi Python Tools for Visual Studio]: web-sites-python-ptvs-django-sql.md
[SQL Database]: web-sites-python-ptvs-django-sql.md
[MySQL]: web-sites-python-ptvs-django-mysql.md

<!--External Link references-->
[Zestaw Azure SDK dla języka Python w wersji 2.7]: http://go.microsoft.com/fwlink/?linkid=254281
[zestawu Azure SDK dla języka Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990
[python.org]: http://www.python.org/
[Git dla systemu Windows]: http://msysgit.github.io/
[Github dla systemu Windows]: https://windows.github.com/
[Python Tools for Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Program Visual Studio]: http://www.visualstudio.com/
[Dokumentacja narzędzi Python Tools for Visual Studio]: http://aka.ms/ptvsdocs
[Dokumentacja platformy Django]: https://www.djangoproject.com/
