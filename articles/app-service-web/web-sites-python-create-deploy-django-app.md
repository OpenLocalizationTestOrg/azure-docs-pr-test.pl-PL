---
title: "aplikacje sieci web aaaCreating przy użyciu platformy Django na platformie Azure"
description: "Samouczek przedstawiający toorunning aplikacji sieci web języka Python w aplikacjach sieci Web usługi aplikacji Azure."
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
ms.openlocfilehash: 26a131da358748bd6fe4ee5c114d0a8f91b83cfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-web-apps-with-django-in-azure"></a><span data-ttu-id="c6f58-103">Tworzenie aplikacji sieci Web przy użyciu platformy Django na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="c6f58-103">Creating web apps with Django in Azure</span></span>
<span data-ttu-id="c6f58-104">Ten przewodnik opisuje sposób uruchamiania systemem Python tooget [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="c6f58-104">This tutorial describes how tooget started running Python on [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="c6f58-105">Usługa Web Apps zapewnia ograniczony bezpłatny hosting i szybkie wdrażanie, a także możliwość korzystania z języka Python.</span><span class="sxs-lookup"><span data-stu-id="c6f58-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span> <span data-ttu-id="c6f58-106">Rozwoju aplikacji, możesz przełączyć toopaid hosting lub można również zintegrować z wszystkimi hello innymi usługami Azure.</span><span class="sxs-lookup"><span data-stu-id="c6f58-106">As your app grows, you can switch toopaid hosting, and you can also integrate with all of hello other Azure services.</span></span>

<span data-ttu-id="c6f58-107">Utworzysz aplikację przy użyciu platformy sieci web Django hello (zobacz alternatywne wersje tego samouczka dla [Flask](web-sites-python-create-deploy-flask-app.md) i [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span><span class="sxs-lookup"><span data-stu-id="c6f58-107">You will create an application using hello Django web framework (see alternate versions of this tutorial for [Flask](web-sites-python-create-deploy-flask-app.md) and [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span></span> <span data-ttu-id="c6f58-108">Zostanie tworzenie aplikacji sieci web hello z hello Azure Marketplace, skonfigurujesz wdrożenie systemu Git i klonowania repozytorium hello lokalnie.</span><span class="sxs-lookup"><span data-stu-id="c6f58-108">You will create hello web app from hello Azure Marketplace, set up Git deployment, and clone hello repository locally.</span></span> <span data-ttu-id="c6f58-109">Następnie uruchomisz aplikacji hello lokalnie, wprowadzić zmiany, zatwierdzenia i wypychanie ich tooAzure.</span><span class="sxs-lookup"><span data-stu-id="c6f58-109">Then you will run hello application locally, make changes, commit and push them tooAzure.</span></span> <span data-ttu-id="c6f58-110">Witaj samouczku przedstawiono sposób toodo od systemu Windows lub Mac/Linux.</span><span class="sxs-lookup"><span data-stu-id="c6f58-110">hello tutorial shows how toodo this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="c6f58-111">Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="c6f58-111">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="c6f58-112">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="c6f58-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="c6f58-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c6f58-113">Prerequisites</span></span>
* <span data-ttu-id="c6f58-114">System Windows, Mac lub Linux</span><span class="sxs-lookup"><span data-stu-id="c6f58-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="c6f58-115">Środowisko Python w wersji 2.7 lub 3.4</span><span class="sxs-lookup"><span data-stu-id="c6f58-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="c6f58-116">Narzędzia setuptools pip, virtualenv (tylko środowisko Python 2.7)</span><span class="sxs-lookup"><span data-stu-id="c6f58-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="c6f58-117">Usługa Git</span><span class="sxs-lookup"><span data-stu-id="c6f58-117">Git</span></span>
* <span data-ttu-id="c6f58-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) — uwaga: ten składnik jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="c6f58-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="c6f58-119">**Uwaga**: publikowanie TFS nie jest obecnie obsługiwane dla projektów języka Python.</span><span class="sxs-lookup"><span data-stu-id="c6f58-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="c6f58-120">Windows</span><span class="sxs-lookup"><span data-stu-id="c6f58-120">Windows</span></span>
<span data-ttu-id="c6f58-121">Jeśli środowisko Python 2.7 lub 3.4 (32-bitowe) nie zostało jeszcze zainstalowane, zalecane jest zainstalowanie [Zestaw Azure SDK dla języka Python w wersji 2.7] lub [zestawu Azure SDK dla języka Python 3.4] przy użyciu Instalatora platformy sieci Web.</span><span class="sxs-lookup"><span data-stu-id="c6f58-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span> <span data-ttu-id="c6f58-122">Spowoduje to zainstalowanie hello 32-bitowej wersji języka Python, narzędzi setuptools, pip, virtualenv itp (32-bitowe środowisko Python jest zainstalowanych na maszynach hostów Azure hello).</span><span class="sxs-lookup"><span data-stu-id="c6f58-122">This installs hello 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on hello Azure host machines).</span></span> <span data-ttu-id="c6f58-123">Możesz również pobrać środowisko Python z witryny [python.org].</span><span class="sxs-lookup"><span data-stu-id="c6f58-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="c6f58-124">W przypadku systemu Git zalecane jest narzędzie [Git dla systemu Windows] lub [Github dla systemu Windows].</span><span class="sxs-lookup"><span data-stu-id="c6f58-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span> <span data-ttu-id="c6f58-125">Jeśli używasz programu Visual Studio, używając hello zintegrowanej obsługi systemu Git.</span><span class="sxs-lookup"><span data-stu-id="c6f58-125">If you use Visual Studio, you can use hello integrated Git support.</span></span>

<span data-ttu-id="c6f58-126">Zalecane jest również zainstalowanie narzędzi [Python Tools 2.2 for Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="c6f58-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span> <span data-ttu-id="c6f58-127">Ten krok jest opcjonalny, ale jeśli masz [programu Visual Studio], włączając hello wolne Visual Studio Community 2013 lub Visual Studio Express 2013 for Web, a następnie zapewni to doskonały IDE języka Python.</span><span class="sxs-lookup"><span data-stu-id="c6f58-127">This is optional, but if you have [Visual Studio], including hello free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="c6f58-128">System Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="c6f58-128">Mac/Linux</span></span>
<span data-ttu-id="c6f58-129">Środowisko Python i system Git powinny być już zainstalowane, ale upewnij się, że masz środowisko Python 2.7 lub 3.4.</span><span class="sxs-lookup"><span data-stu-id="c6f58-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-creation-on-portal"></a><span data-ttu-id="c6f58-130">Tworzenie aplikacji sieci Web w portalu</span><span class="sxs-lookup"><span data-stu-id="c6f58-130">Web App Creation on Portal</span></span>
<span data-ttu-id="c6f58-131">Witaj pierwszym krokiem tworzenia aplikacji jest toocreate hello aplikacja sieci web za pośrednictwem hello [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c6f58-131">hello first step in creating your app is toocreate hello web app via hello [Azure Portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="c6f58-132">Zaloguj się do hello portalu Azure i kliknij przycisk hello **nowy** przycisku na powitania lewym dolnym rogu.</span><span class="sxs-lookup"><span data-stu-id="c6f58-132">Log into hello Azure Portal and click hello **NEW** button in hello bottom left corner.</span></span>
2. <span data-ttu-id="c6f58-133">W polu wyszukiwania hello wpisz "python".</span><span class="sxs-lookup"><span data-stu-id="c6f58-133">In hello search box, type "python".</span></span>
3. <span data-ttu-id="c6f58-134">W wynikach wyszukiwania hello, wybierz **Django** (opublikowanych przez PTVS), następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="c6f58-134">In hello search results, select **Django** (published by PTVS), then click **Create**.</span></span>
4. <span data-ttu-id="c6f58-135">Skonfiguruj hello nową aplikację Django, takich jak tworzenie nowego planu usługi App Service i nowej grupy zasobów dla niego.</span><span class="sxs-lookup"><span data-stu-id="c6f58-135">Configure hello new Django app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="c6f58-136">Następnie kliknij pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="c6f58-136">Then, click **Create**.</span></span>
5. <span data-ttu-id="c6f58-137">Konfigurowanie publikowania Git dla aplikacji sieci web nowo utworzony wykonując instrukcje hello [tooAzure lokalnego wdrożenia Git usługi aplikacji](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="c6f58-137">Configure Git publishing for your newly created web app by following hello instructions at [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="c6f58-138">Omówienie aplikacji</span><span class="sxs-lookup"><span data-stu-id="c6f58-138">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="c6f58-139">Zawartość repozytorium Git</span><span class="sxs-lookup"><span data-stu-id="c6f58-139">Git repository contents</span></span>
<span data-ttu-id="c6f58-140">Poniżej przedstawiono omówienie hello plików, które znajdują się w początkowym repozytorium Git hello, które sklonujemy w następnej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="c6f58-140">Here's an overview of hello files you'll find in hello initial Git repository, which we'll clone in hello next section.</span></span>

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

<span data-ttu-id="c6f58-141">Główne źródła dla aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="c6f58-141">Main sources for hello application.</span></span> <span data-ttu-id="c6f58-142">Składa się z 3 stron (indeks, informacje, kontakt) z układem głównym.</span><span class="sxs-lookup"><span data-stu-id="c6f58-142">Consists of 3 pages (index, about, contact) with a master layout.</span></span> <span data-ttu-id="c6f58-143">Zawartość statyczna i skrypty obejmują bootstrap, jquery, modernizr i respond.</span><span class="sxs-lookup"><span data-stu-id="c6f58-143">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \manage.py

<span data-ttu-id="c6f58-144">Obsługa zarządzania lokalnego i serwera projektowego.</span><span class="sxs-lookup"><span data-stu-id="c6f58-144">Local management and development server support.</span></span> <span data-ttu-id="c6f58-145">Za pomocą tej aplikacji hello toorun lokalnie, synchronizowanie bazy danych hello itp.</span><span class="sxs-lookup"><span data-stu-id="c6f58-145">Use this toorun hello application locally, synchronize hello database, etc.</span></span>

    \db.sqlite3

<span data-ttu-id="c6f58-146">Domyślna baza danych.</span><span class="sxs-lookup"><span data-stu-id="c6f58-146">Default database.</span></span> <span data-ttu-id="c6f58-147">Zawiera tabele niezbędne hello toorun aplikacji hello, ale nie zawiera żadnych użytkowników (należy zsynchronizować hello toocreate bazy danych użytkownika).</span><span class="sxs-lookup"><span data-stu-id="c6f58-147">Includes hello necessary tables for hello application toorun, but does not contain any users (synchronize hello database toocreate a user).</span></span>

    \DjangoWebProject.pyproj
    \DjangoWebProject.sln

<span data-ttu-id="c6f58-148">Pliki projektu do użycia z narzędziami [Python Tools for Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="c6f58-148">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="c6f58-149">Serwer proxy usług IIS dla środowisk wirtualnych i obsługa zdalnego debugowania narzędzi PTVS.</span><span class="sxs-lookup"><span data-stu-id="c6f58-149">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="c6f58-150">Pakiety zewnętrzne wymagane przez tę aplikację.</span><span class="sxs-lookup"><span data-stu-id="c6f58-150">External packages needed by this application.</span></span> <span data-ttu-id="c6f58-151">skrypt wdrożenia Hello będzie narzędzia pip instalowanie pakietów hello wymienione w tym pliku.</span><span class="sxs-lookup"><span data-stu-id="c6f58-151">hello deployment script will pip install hello packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="c6f58-152">Pliki konfiguracji programu IIS.</span><span class="sxs-lookup"><span data-stu-id="c6f58-152">IIS configuration files.</span></span> <span data-ttu-id="c6f58-153">skrypt wdrożenia Hello Użyj hello odpowiedniego pliku web.x.y.config i skopiuje go jako plik web.config.</span><span class="sxs-lookup"><span data-stu-id="c6f58-153">hello deployment script will use hello appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="c6f58-154">Pliki opcjonalne — dostosowywanie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="c6f58-154">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-django-customizing-deployment](../../includes/web-sites-python-django-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="c6f58-155">Pliki opcjonalne — środowisko uruchomieniowe języka Python</span><span class="sxs-lookup"><span data-stu-id="c6f58-155">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="c6f58-156">Dodatkowe pliki na serwerze</span><span class="sxs-lookup"><span data-stu-id="c6f58-156">Additional files on server</span></span>
<span data-ttu-id="c6f58-157">Niektóre pliki na powitania serwera istnieje, ale nie są dodawane toohello repozytorium git.</span><span class="sxs-lookup"><span data-stu-id="c6f58-157">Some files exist on hello server but are not added toohello git repository.</span></span> <span data-ttu-id="c6f58-158">Są one tworzone przez skrypt wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="c6f58-158">These are created by hello deployment script.</span></span>

    \web.config

<span data-ttu-id="c6f58-159">Plik konfiguracji programu IIS.</span><span class="sxs-lookup"><span data-stu-id="c6f58-159">IIS configuration file.</span></span> <span data-ttu-id="c6f58-160">Tworzony na podstawie pliku web.x.y.config przy każdym wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="c6f58-160">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="c6f58-161">Środowisko wirtualne języka Python.</span><span class="sxs-lookup"><span data-stu-id="c6f58-161">Python virtual environment.</span></span> <span data-ttu-id="c6f58-162">Utworzonych podczas wdrażania, jeśli zgodne środowisko wirtualne już nie istnieje na powitania aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="c6f58-162">Created during deployment if a compatible virtual environment doesn't already exist on hello web app.</span></span> <span data-ttu-id="c6f58-163">Pakiety wymienione w pliku requirements.txt są zainstalowane narzędzia pip, ale narzędzie pip pomija instalację, jeśli hello pakiety są już zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="c6f58-163">Packages listed in requirements.txt are pip installed, but pip will skip installation if hello packages are already installed.</span></span>

<span data-ttu-id="c6f58-164">Witaj 3 następnych sekcjach opisano sposób tworzenia aplikacji w 3 różnych środowiskach sieci web na tooproceed z hello:</span><span class="sxs-lookup"><span data-stu-id="c6f58-164">hello next 3 sections describe how tooproceed with hello web app development under 3 different environments:</span></span>

* <span data-ttu-id="c6f58-165">System Windows — przy użyciu narzędzi Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c6f58-165">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="c6f58-166">System Windows — przy użyciu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="c6f58-166">Windows, with command line</span></span>
* <span data-ttu-id="c6f58-167">System Mac/Linux — przy użyciu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="c6f58-167">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="c6f58-168">Wdrażanie aplikacji sieci Web — system Windows — narzędzia Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c6f58-168">Web app development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="c6f58-169">Klonowanie repozytorium hello</span><span class="sxs-lookup"><span data-stu-id="c6f58-169">Clone hello repository</span></span>
<span data-ttu-id="c6f58-170">Najpierw sklonuj repozytorium hello przy użyciu adresu URL hello na powitania portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c6f58-170">First, clone hello repository using hello URL provided on hello Azure Portal.</span></span> <span data-ttu-id="c6f58-171">Aby uzyskać więcej informacji, zobacz [tooAzure lokalnego wdrożenia Git usługi aplikacji](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="c6f58-171">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="c6f58-172">Otwórz plik rozwiązania hello (.sln), który znajduje się w katalogu głównego repozytorium hello hello.</span><span class="sxs-lookup"><span data-stu-id="c6f58-172">Open hello solution file (.sln) that is included in hello root of hello repository.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-solution-django.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="c6f58-173">Tworzenie środowiska wirtualnego</span><span class="sxs-lookup"><span data-stu-id="c6f58-173">Create virtual environment</span></span>
<span data-ttu-id="c6f58-174">Teraz utwórz środowisko wirtualne dla wdrożenia lokalnego.</span><span class="sxs-lookup"><span data-stu-id="c6f58-174">Now we'll create a virtual environment for local development.</span></span> <span data-ttu-id="c6f58-175">Kliknij prawym przyciskiem myszy pozycję **Środowiska Python** i wybierz pozycję **Dodaj środowisko wirtualne**.</span><span class="sxs-lookup"><span data-stu-id="c6f58-175">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="c6f58-176">Upewnij się, że nazwa hello środowiska hello jest `env`.</span><span class="sxs-lookup"><span data-stu-id="c6f58-176">Make sure hello name of hello environment is `env`.</span></span>
* <span data-ttu-id="c6f58-177">Wybierz interpreter podstawowy hello.</span><span class="sxs-lookup"><span data-stu-id="c6f58-177">Select hello base interpreter.</span></span> <span data-ttu-id="c6f58-178">Upewnij się, że toouse hello sama wersja środowiska Python, którą wybrano dla aplikacji sieci web (w pliku runtime.txt lub hello **ustawienia aplikacji** bloku aplikacji sieci web w portalu Azure hello).</span><span class="sxs-lookup"><span data-stu-id="c6f58-178">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello **Application Settings** blade of your web app in hello Azure Portal).</span></span>
* <span data-ttu-id="c6f58-179">Upewnij się, zaznaczono opcję hello toodownload i zainstaluj pakiety.</span><span class="sxs-lookup"><span data-stu-id="c6f58-179">Make sure hello option toodownload and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="c6f58-180">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="c6f58-180">Click **Create**.</span></span> <span data-ttu-id="c6f58-181">Spowoduje to utworzenie środowiska wirtualnego hello i zainstalowanie składników zależnych wymienionych w pliku requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="c6f58-181">This will create hello virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="create-a-superuser"></a><span data-ttu-id="c6f58-182">Tworzenie administratora</span><span class="sxs-lookup"><span data-stu-id="c6f58-182">Create a superuser</span></span>
<span data-ttu-id="c6f58-183">Baza danych Hello dołączona aplikacji hello nie zawiera definicji administratora.</span><span class="sxs-lookup"><span data-stu-id="c6f58-183">hello database included with hello application does not have any superuser defined.</span></span> <span data-ttu-id="c6f58-184">W kolejności toouse hello logowania funkcjonalności aplikacji hello lub interfejsu administracyjnego Django hello (Jeśli zdecydujesz tooenable go), będziesz potrzebować toocreate administratora.</span><span class="sxs-lookup"><span data-stu-id="c6f58-184">In order toouse hello sign-in functionality in hello application, or hello Django admin interface (if you decide tooenable it), you'll need toocreate a superuser.</span></span>

<span data-ttu-id="c6f58-185">Uruchom to z hello wiersza polecenia w folderze projektu:</span><span class="sxs-lookup"><span data-stu-id="c6f58-185">Run this from hello command-line from your project folder:</span></span>

    env\scripts\python manage.py createsuperuser

<span data-ttu-id="c6f58-186">Postępuj zgodnie z nazwy użytkownika hello hello monity tooset, hasło itp.</span><span class="sxs-lookup"><span data-stu-id="c6f58-186">Follow hello prompts tooset hello user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="c6f58-187">Uruchamianie przy użyciu serwera projektowego</span><span class="sxs-lookup"><span data-stu-id="c6f58-187">Run using development server</span></span>
<span data-ttu-id="c6f58-188">Naciśnij klawisz F5 toostart debugowania i przeglądarki sieci web zostanie otwarty toohello strony uruchomionej lokalnie.</span><span class="sxs-lookup"><span data-stu-id="c6f58-188">Press F5 toostart debugging, and your web browser will open automatically toohello page running locally.</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

<span data-ttu-id="c6f58-189">Można ustawić punktów przerwania w hello źródeł, użyj hello czujki systemu windows itd. Zobacz hello [narzędzi Python Tools for Visual Studio dokumentacji] Aby uzyskać więcej informacji na temat hello różnych funkcji.</span><span class="sxs-lookup"><span data-stu-id="c6f58-189">You can set breakpoints in hello sources, use hello watch windows, etc. See hello [Python Tools for Visual Studio Documentation] for more information on hello various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="c6f58-190">Wprowadzanie zmian</span><span class="sxs-lookup"><span data-stu-id="c6f58-190">Make changes</span></span>
<span data-ttu-id="c6f58-191">Teraz możesz eksperymentować, wprowadzając zmiany toohello aplikacji źródeł i/lub szablonach.</span><span class="sxs-lookup"><span data-stu-id="c6f58-191">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="c6f58-192">Po przetestowaniu zmiany je zatwierdzić toohello repozytorium Git:</span><span class="sxs-lookup"><span data-stu-id="c6f58-192">After you've tested your changes, commit them toohello Git repository:</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-commit-django.png)

### <a name="install-more-packages"></a><span data-ttu-id="c6f58-193">Instalowanie dodatkowych pakietów</span><span class="sxs-lookup"><span data-stu-id="c6f58-193">Install more packages</span></span>
<span data-ttu-id="c6f58-194">Aplikacja może mieć zależności poza środowiskiem Python i platformą Django.</span><span class="sxs-lookup"><span data-stu-id="c6f58-194">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="c6f58-195">Możesz zainstalować dodatkowe pakiety przy użyciu narzędzia pip.</span><span class="sxs-lookup"><span data-stu-id="c6f58-195">You can install additional packages using pip.</span></span> <span data-ttu-id="c6f58-196">tooinstall pakiet, kliknij prawym przyciskiem myszy na powitania środowisko wirtualne i wybierz **zainstaluj pakiet języka Python**.</span><span class="sxs-lookup"><span data-stu-id="c6f58-196">tooinstall a package, right-click on hello virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="c6f58-197">Na przykład tooinstall hello Azure SDK dla języka Python, który zapewnia dostęp tooAzure magazynu, usługi service bus i innymi usługami Azure, wprowadź `azure`:</span><span class="sxs-lookup"><span data-stu-id="c6f58-197">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-install-package-dialog.png)

<span data-ttu-id="c6f58-198">Kliknij prawym przyciskiem myszy na powitania środowiska wirtualnego, a następnie wybierz **Generuj plik requirements.txt** tooupdate requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="c6f58-198">Right-click on hello virtual environment and select **Generate requirements.txt** tooupdate requirements.txt.</span></span>

<span data-ttu-id="c6f58-199">Następnie Zatwierdź repozytorium Git toohello toorequirements.txt zmiany hello.</span><span class="sxs-lookup"><span data-stu-id="c6f58-199">Then, commit hello changes toorequirements.txt toohello Git repository.</span></span>

### <a name="deploy-tooazure"></a><span data-ttu-id="c6f58-200">Wdrażanie tooAzure</span><span class="sxs-lookup"><span data-stu-id="c6f58-200">Deploy tooAzure</span></span>
<span data-ttu-id="c6f58-201">polecenie tootrigger wdrożenia, **synchronizacji** lub **Push**.</span><span class="sxs-lookup"><span data-stu-id="c6f58-201">tootrigger a deployment, click on **Sync** or **Push**.</span></span> <span data-ttu-id="c6f58-202">Synchronizacja obejmuje zarówno wypychanie, jak i ściąganie.</span><span class="sxs-lookup"><span data-stu-id="c6f58-202">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-git-push.png)

<span data-ttu-id="c6f58-203">pierwszym wdrożeniu Hello wymaga czasu, ponieważ obejmuje tworzenie środowiska wirtualnego, instalowanie pakietów itp.</span><span class="sxs-lookup"><span data-stu-id="c6f58-203">hello first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="c6f58-204">Program Visual Studio nie wyświetla postęp hello hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="c6f58-204">Visual Studio doesn't show hello progress of hello deployment.</span></span> <span data-ttu-id="c6f58-205">Jeśli chcesz tooreview hello w danych wyjściowych, zobacz sekcję hello na [Rozwiązywanie problemów — wdrożenie](#troubleshooting-deployment).</span><span class="sxs-lookup"><span data-stu-id="c6f58-205">If you'd like tooreview hello output, see hello section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="c6f58-206">Przeglądaj zmiany toohello tooview adresu URL platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c6f58-206">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="c6f58-207">Wdrażanie aplikacji sieci Web — system Windows — wiersz polecenia</span><span class="sxs-lookup"><span data-stu-id="c6f58-207">Web app development - Windows - command line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="c6f58-208">Klonowanie repozytorium hello</span><span class="sxs-lookup"><span data-stu-id="c6f58-208">Clone hello repository</span></span>
<span data-ttu-id="c6f58-209">Najpierw sklonować repozytorium hello przy użyciu adresu URL hello na powitania portalu Azure i dodać hello repozytorium Azure jako zdalnej.</span><span class="sxs-lookup"><span data-stu-id="c6f58-209">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="c6f58-210">Aby uzyskać więcej informacji, zobacz [tooAzure lokalnego wdrożenia Git usługi aplikacji](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="c6f58-210">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url>

### <a name="create-virtual-environment"></a><span data-ttu-id="c6f58-211">Tworzenie środowiska wirtualnego</span><span class="sxs-lookup"><span data-stu-id="c6f58-211">Create virtual environment</span></span>
<span data-ttu-id="c6f58-212">Utworzymy nowe środowisko wirtualne dla celów programistycznych (nie należy dodawać go toohello repozytorium).</span><span class="sxs-lookup"><span data-stu-id="c6f58-212">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span> <span data-ttu-id="c6f58-213">Wirtualnych środowisk języka Python nie są można zmieniać lokalizacji, dlatego każdy Deweloper pracujący nad aplikacji hello tworzy własne środowisko lokalnie.</span><span class="sxs-lookup"><span data-stu-id="c6f58-213">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="c6f58-214">Upewnij się, toouse hello sama wersja środowiska Python, którą wybrano dla aplikacji sieci web (w pliku runtime.txt lub hello bloku ustawienia aplikacji aplikacji sieci web w portalu Azure hello).</span><span class="sxs-lookup"><span data-stu-id="c6f58-214">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello Application Settings blade of your web app in hello Azure Portal).</span></span>

<span data-ttu-id="c6f58-215">Dla środowiska Python w wersji 2.7:</span><span class="sxs-lookup"><span data-stu-id="c6f58-215">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="c6f58-216">Dla środowiska Python w wersji 3.4:</span><span class="sxs-lookup"><span data-stu-id="c6f58-216">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="c6f58-217">Zainstaluj pakiety zewnętrzne wymagane przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="c6f58-217">Install any external packages required by your application.</span></span> <span data-ttu-id="c6f58-218">Możesz użyć pliku requirements.txt hello w głównym hello hello repozytorium tooinstall hello pakietów w środowisku wirtualnym:</span><span class="sxs-lookup"><span data-stu-id="c6f58-218">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="create-a-superuser"></a><span data-ttu-id="c6f58-219">Tworzenie administratora</span><span class="sxs-lookup"><span data-stu-id="c6f58-219">Create a superuser</span></span>
<span data-ttu-id="c6f58-220">Baza danych Hello dołączona aplikacji hello nie zawiera definicji administratora.</span><span class="sxs-lookup"><span data-stu-id="c6f58-220">hello database included with hello application does not have any superuser defined.</span></span> <span data-ttu-id="c6f58-221">W kolejności toouse hello logowania funkcjonalności aplikacji hello lub interfejsu administracyjnego Django hello (Jeśli zdecydujesz tooenable go), będziesz potrzebować toocreate administratora.</span><span class="sxs-lookup"><span data-stu-id="c6f58-221">In order toouse hello sign-in functionality in hello application, or hello Django admin interface (if you decide tooenable it), you'll need toocreate a superuser.</span></span>

<span data-ttu-id="c6f58-222">Uruchom to z hello wiersza polecenia w folderze projektu:</span><span class="sxs-lookup"><span data-stu-id="c6f58-222">Run this from hello command-line from your project folder:</span></span>

    env\scripts\python manage.py createsuperuser

<span data-ttu-id="c6f58-223">Postępuj zgodnie z nazwy użytkownika hello hello monity tooset, hasło itp.</span><span class="sxs-lookup"><span data-stu-id="c6f58-223">Follow hello prompts tooset hello user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="c6f58-224">Uruchamianie przy użyciu serwera projektowego</span><span class="sxs-lookup"><span data-stu-id="c6f58-224">Run using development server</span></span>
<span data-ttu-id="c6f58-225">Można uruchomić aplikacji hello na serwerze projektowym z hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="c6f58-225">You can launch hello application under a development server with hello following command:</span></span>

    env\scripts\python manage.py runserver

<span data-ttu-id="c6f58-226">Witaj konsoli zostanie wyświetlony adres URL hello i nasłuchuje portu powitania serwera:</span><span class="sxs-lookup"><span data-stu-id="c6f58-226">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-run-local-django.png)

<span data-ttu-id="c6f58-227">Następnie otwórz adres URL toothat przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="c6f58-227">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

### <a name="make-changes"></a><span data-ttu-id="c6f58-228">Wprowadzanie zmian</span><span class="sxs-lookup"><span data-stu-id="c6f58-228">Make changes</span></span>
<span data-ttu-id="c6f58-229">Teraz możesz eksperymentować, wprowadzając zmiany toohello aplikacji źródeł i/lub szablonach.</span><span class="sxs-lookup"><span data-stu-id="c6f58-229">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="c6f58-230">Po przetestowaniu zmiany je zatwierdzić toohello repozytorium Git:</span><span class="sxs-lookup"><span data-stu-id="c6f58-230">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="c6f58-231">Instalowanie dodatkowych pakietów</span><span class="sxs-lookup"><span data-stu-id="c6f58-231">Install more packages</span></span>
<span data-ttu-id="c6f58-232">Aplikacja może mieć zależności poza środowiskiem Python i platformą Django.</span><span class="sxs-lookup"><span data-stu-id="c6f58-232">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="c6f58-233">Możesz zainstalować dodatkowe pakiety przy użyciu narzędzia pip.</span><span class="sxs-lookup"><span data-stu-id="c6f58-233">You can install additional packages using pip.</span></span> <span data-ttu-id="c6f58-234">Na przykład tooinstall hello Azure SDK dla języka Python, co pozwala na dostęp do magazynu tooAzure, magistrali usług i innych usług Azure, wpisz:</span><span class="sxs-lookup"><span data-stu-id="c6f58-234">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="c6f58-235">Upewnij się, że tooupdate pliku requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="c6f58-235">Make sure tooupdate requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="c6f58-236">Zatwierdź zmiany hello:</span><span class="sxs-lookup"><span data-stu-id="c6f58-236">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="c6f58-237">Wdrażanie tooAzure</span><span class="sxs-lookup"><span data-stu-id="c6f58-237">Deploy tooAzure</span></span>
<span data-ttu-id="c6f58-238">tootrigger wdrożenia hello wypychania zmiany tooAzure:</span><span class="sxs-lookup"><span data-stu-id="c6f58-238">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="c6f58-239">Zostanie wyświetlone dane wyjściowe hello hello skryptu wdrożenia, łącznie z tworzeniem środowiska wirtualnego, instalowaniem pakietów i tworzeniem pliku web.config.</span><span class="sxs-lookup"><span data-stu-id="c6f58-239">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="c6f58-240">Przeglądaj zmiany toohello tooview adresu URL platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c6f58-240">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="c6f58-241">Wdrażanie aplikacji sieci Web — system Mac/Linux — wiersz polecenia</span><span class="sxs-lookup"><span data-stu-id="c6f58-241">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="c6f58-242">Klonowanie repozytorium hello</span><span class="sxs-lookup"><span data-stu-id="c6f58-242">Clone hello repository</span></span>
<span data-ttu-id="c6f58-243">Najpierw sklonować repozytorium hello przy użyciu adresu URL hello na powitania portalu Azure i dodać hello repozytorium Azure jako zdalnej.</span><span class="sxs-lookup"><span data-stu-id="c6f58-243">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="c6f58-244">Aby uzyskać więcej informacji, zobacz [tooAzure lokalnego wdrożenia Git usługi aplikacji](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="c6f58-244">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url>

### <a name="create-virtual-environment"></a><span data-ttu-id="c6f58-245">Tworzenie środowiska wirtualnego</span><span class="sxs-lookup"><span data-stu-id="c6f58-245">Create virtual environment</span></span>
<span data-ttu-id="c6f58-246">Utworzymy nowe środowisko wirtualne dla celów programistycznych (nie należy dodawać go toohello repozytorium).</span><span class="sxs-lookup"><span data-stu-id="c6f58-246">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span> <span data-ttu-id="c6f58-247">Wirtualnych środowisk języka Python nie są można zmieniać lokalizacji, dlatego każdy Deweloper pracujący nad aplikacji hello tworzy własne środowisko lokalnie.</span><span class="sxs-lookup"><span data-stu-id="c6f58-247">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="c6f58-248">Upewnij się, toouse hello sama wersja środowiska Python, którą wybrano dla aplikacji sieci web (w pliku runtime.txt lub hello bloku ustawienia aplikacji aplikacji sieci web w portalu Azure hello).</span><span class="sxs-lookup"><span data-stu-id="c6f58-248">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello Application Settings blade of your web app in hello Azure Portal).</span></span>

<span data-ttu-id="c6f58-249">Dla środowiska Python w wersji 2.7:</span><span class="sxs-lookup"><span data-stu-id="c6f58-249">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="c6f58-250">Dla środowiska Python w wersji 3.4:</span><span class="sxs-lookup"><span data-stu-id="c6f58-250">For Python 3.4:</span></span>

    python -m venv env

<span data-ttu-id="c6f58-251">lub</span><span class="sxs-lookup"><span data-stu-id="c6f58-251">or</span></span>

    pyvenv env

<span data-ttu-id="c6f58-252">Zainstaluj pakiety zewnętrzne wymagane przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="c6f58-252">Install any external packages required by your application.</span></span> <span data-ttu-id="c6f58-253">Możesz użyć pliku requirements.txt hello w głównym hello hello repozytorium tooinstall hello pakietów w środowisku wirtualnym:</span><span class="sxs-lookup"><span data-stu-id="c6f58-253">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="create-a-superuser"></a><span data-ttu-id="c6f58-254">Tworzenie administratora</span><span class="sxs-lookup"><span data-stu-id="c6f58-254">Create a superuser</span></span>
<span data-ttu-id="c6f58-255">Baza danych Hello dołączona aplikacji hello nie zawiera definicji administratora.</span><span class="sxs-lookup"><span data-stu-id="c6f58-255">hello database included with hello application does not have any superuser defined.</span></span> <span data-ttu-id="c6f58-256">W kolejności toouse hello logowania funkcjonalności aplikacji hello lub interfejsu administracyjnego Django hello (Jeśli zdecydujesz tooenable go), będziesz potrzebować toocreate administratora.</span><span class="sxs-lookup"><span data-stu-id="c6f58-256">In order toouse hello sign-in functionality in hello application, or hello Django admin interface (if you decide tooenable it), you'll need toocreate a superuser.</span></span>

<span data-ttu-id="c6f58-257">Uruchom to z hello wiersza polecenia w folderze projektu:</span><span class="sxs-lookup"><span data-stu-id="c6f58-257">Run this from hello command-line from your project folder:</span></span>

    env/bin/python manage.py createsuperuser

<span data-ttu-id="c6f58-258">Postępuj zgodnie z nazwy użytkownika hello hello monity tooset, hasło itp.</span><span class="sxs-lookup"><span data-stu-id="c6f58-258">Follow hello prompts tooset hello user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="c6f58-259">Uruchamianie przy użyciu serwera projektowego</span><span class="sxs-lookup"><span data-stu-id="c6f58-259">Run using development server</span></span>
<span data-ttu-id="c6f58-260">Można uruchomić aplikacji hello na serwerze projektowym z hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="c6f58-260">You can launch hello application under a development server with hello following command:</span></span>

    env/bin/python manage.py runserver

<span data-ttu-id="c6f58-261">Witaj konsoli zostanie wyświetlony adres URL hello i nasłuchuje portu powitania serwera:</span><span class="sxs-lookup"><span data-stu-id="c6f58-261">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-django-app/mac-run-local-django.png)

<span data-ttu-id="c6f58-262">Następnie otwórz adres URL toothat przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="c6f58-262">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-django-app/mac-browser-django.png)

### <a name="make-changes"></a><span data-ttu-id="c6f58-263">Wprowadzanie zmian</span><span class="sxs-lookup"><span data-stu-id="c6f58-263">Make changes</span></span>
<span data-ttu-id="c6f58-264">Teraz możesz eksperymentować, wprowadzając zmiany toohello aplikacji źródeł i/lub szablonach.</span><span class="sxs-lookup"><span data-stu-id="c6f58-264">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="c6f58-265">Po przetestowaniu zmiany je zatwierdzić toohello repozytorium Git:</span><span class="sxs-lookup"><span data-stu-id="c6f58-265">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="c6f58-266">Instalowanie dodatkowych pakietów</span><span class="sxs-lookup"><span data-stu-id="c6f58-266">Install more packages</span></span>
<span data-ttu-id="c6f58-267">Aplikacja może mieć zależności poza środowiskiem Python i platformą Django.</span><span class="sxs-lookup"><span data-stu-id="c6f58-267">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="c6f58-268">Możesz zainstalować dodatkowe pakiety przy użyciu narzędzia pip.</span><span class="sxs-lookup"><span data-stu-id="c6f58-268">You can install additional packages using pip.</span></span> <span data-ttu-id="c6f58-269">Na przykład tooinstall hello Azure SDK dla języka Python, co pozwala na dostęp do magazynu tooAzure, magistrali usług i innych usług Azure, wpisz:</span><span class="sxs-lookup"><span data-stu-id="c6f58-269">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="c6f58-270">Upewnij się, że tooupdate pliku requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="c6f58-270">Make sure tooupdate requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="c6f58-271">Zatwierdź zmiany hello:</span><span class="sxs-lookup"><span data-stu-id="c6f58-271">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="c6f58-272">Wdrażanie tooAzure</span><span class="sxs-lookup"><span data-stu-id="c6f58-272">Deploy tooAzure</span></span>
<span data-ttu-id="c6f58-273">tootrigger wdrożenia hello wypychania zmiany tooAzure:</span><span class="sxs-lookup"><span data-stu-id="c6f58-273">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="c6f58-274">Zostanie wyświetlone dane wyjściowe hello hello skryptu wdrożenia, łącznie z tworzeniem środowiska wirtualnego, instalowaniem pakietów i tworzeniem pliku web.config.</span><span class="sxs-lookup"><span data-stu-id="c6f58-274">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="c6f58-275">Przeglądaj zmiany toohello tooview adresu URL platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c6f58-275">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="c6f58-276">Rozwiązywanie problemów — instalowanie pakietów</span><span class="sxs-lookup"><span data-stu-id="c6f58-276">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="c6f58-277">Rozwiązywanie problemów — środowisko wirtualne</span><span class="sxs-lookup"><span data-stu-id="c6f58-277">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="troubleshooting---static-files"></a><span data-ttu-id="c6f58-278">Rozwiązywanie problemów — pliki statyczne</span><span class="sxs-lookup"><span data-stu-id="c6f58-278">Troubleshooting - Static Files</span></span>
<span data-ttu-id="c6f58-279">Platforma Django korzysta hello koncepcji zbierania plików statycznych.</span><span class="sxs-lookup"><span data-stu-id="c6f58-279">Django has hello concept of collecting static files.</span></span> <span data-ttu-id="c6f58-280">Pobiera wszystkie hello pliki statyczne z oryginalnej lokalizacji i kopiuje je tooa pojedynczy folder.</span><span class="sxs-lookup"><span data-stu-id="c6f58-280">This takes all hello static files from their original location and copies them tooa single folder.</span></span> <span data-ttu-id="c6f58-281">Dla tej aplikacji, kopiowane są zbyt`/static`.</span><span class="sxs-lookup"><span data-stu-id="c6f58-281">For this application, they are copied too`/static`.</span></span>

<span data-ttu-id="c6f58-282">Ta operacja jest wykonywana, ponieważ pliki statyczne mogą pochodzić z różnych „aplikacji” Django.</span><span class="sxs-lookup"><span data-stu-id="c6f58-282">This is done because static files may come from different Django 'apps'.</span></span> <span data-ttu-id="c6f58-283">Na przykład hello pliki statyczne z interfejsów administracyjnych Django hello znajdują się w podfolderze biblioteki Django w środowisku wirtualnym hello.</span><span class="sxs-lookup"><span data-stu-id="c6f58-283">For example, hello static files from hello Django admin interfaces are located in a Django library subfolder in hello virtual environment.</span></span> <span data-ttu-id="c6f58-284">Pliki statyczne zdefiniowane przez tę aplikację znajdują się w folderze `/app/static`.</span><span class="sxs-lookup"><span data-stu-id="c6f58-284">Static files defined by this application are located in `/app/static`.</span></span> <span data-ttu-id="c6f58-285">W przypadku użycia dodatkowych „aplikacji” Django pliki statyczne będą znajdować się w kilku miejscach.</span><span class="sxs-lookup"><span data-stu-id="c6f58-285">As you use more Django 'apps', you'll have static files located in multiple places.</span></span>

<span data-ttu-id="c6f58-286">Przy uruchamianiu aplikacji hello w trybie debugowania, aplikacja hello służy hello pliki statyczne z oryginalnej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="c6f58-286">When running hello application in debug mode, hello application serves hello static files from their original location.</span></span>

<span data-ttu-id="c6f58-287">Przy uruchamianiu aplikacji hello w trybie wersji, aplikacja hello jest **nie** służyć hello plików statycznych.</span><span class="sxs-lookup"><span data-stu-id="c6f58-287">When running hello application in release mode, hello application does **not** serve hello static files.</span></span> <span data-ttu-id="c6f58-288">Jest odpowiedzialny za hello hello — plików hello tooserve serwera sieci web.</span><span class="sxs-lookup"><span data-stu-id="c6f58-288">It is hello responsibility of hello web server tooserve hello files.</span></span> <span data-ttu-id="c6f58-289">Dla tej aplikacji IIS udostępnia pliki statyczne hello z `/static`.</span><span class="sxs-lookup"><span data-stu-id="c6f58-289">For this application, IIS will serve hello static files from `/static`.</span></span>

<span data-ttu-id="c6f58-290">Zbieranie plików statycznych Hello odbywa się automatycznie jako część hello skryptu wdrożenia, a uprzednio zebrane pliki.</span><span class="sxs-lookup"><span data-stu-id="c6f58-290">hello collection of static files is done automatically as part of hello deployment script, clearing previously collected files.</span></span> <span data-ttu-id="c6f58-291">Oznacza to kolekcji hello występuje przy każdym wdrożeniu spowolnienie wdrażania bit, ale gwarantuje, że nieaktualne pliki będą niedostępne i potencjalny problem z zabezpieczeniami.</span><span class="sxs-lookup"><span data-stu-id="c6f58-291">This means hello collection occurs on every deployment, slowing down deployment a bit, but it ensures that obsolete files won't be available, avoiding a potential security issue.</span></span>

<span data-ttu-id="c6f58-292">Jeśli chcesz tooskip zbieranie plików statycznych dla aplikacji Django:</span><span class="sxs-lookup"><span data-stu-id="c6f58-292">If you want tooskip collection of static files for your Django application:</span></span>

    \.skipDjango

<span data-ttu-id="c6f58-293">Następnie należy kolekcji hello toodo ręcznie na komputerze lokalnym:</span><span class="sxs-lookup"><span data-stu-id="c6f58-293">Then you'll need toodo hello collection manually on your local machine:</span></span>

    env\scripts\python manage.py collectstatic

<span data-ttu-id="c6f58-294">Następnie usuń hello `\static` z folderu `.gitignore` i dodaj go toohello repozytorium Git.</span><span class="sxs-lookup"><span data-stu-id="c6f58-294">Then remove hello `\static` folder from `.gitignore` and add it toohello Git repository.</span></span>

## <a name="troubleshooting---settings"></a><span data-ttu-id="c6f58-295">Rozwiązywanie problemów — ustawienia</span><span class="sxs-lookup"><span data-stu-id="c6f58-295">Troubleshooting - Settings</span></span>
<span data-ttu-id="c6f58-296">Różne ustawienia dla aplikacji hello można zmienić w `DjangoWebProject/settings.py`.</span><span class="sxs-lookup"><span data-stu-id="c6f58-296">Various settings for hello application can be changed in `DjangoWebProject/settings.py`.</span></span>

<span data-ttu-id="c6f58-297">Dla wygody deweloperów tryb debugowania jest włączony.</span><span class="sxs-lookup"><span data-stu-id="c6f58-297">For developer convenience, debug mode is enabled.</span></span> <span data-ttu-id="c6f58-298">Jeden zalet który jest będziesz w stanie toosee obrazów i innej zawartości statycznej podczas uruchamiania lokalnego bez konieczności toocollect plików statycznych.</span><span class="sxs-lookup"><span data-stu-id="c6f58-298">One nice side effect of that is you'll be able toosee images and other static content when running locally, without having toocollect static files.</span></span>

<span data-ttu-id="c6f58-299">tryb debugowania toodisable:</span><span class="sxs-lookup"><span data-stu-id="c6f58-299">toodisable debug mode:</span></span>

    DEBUG = False

<span data-ttu-id="c6f58-300">Po wyłączeniu debugowania hello wartość `ALLOWED_HOSTS` toobe musi zaktualizować nazwy hosta Azure hello tooinclude.</span><span class="sxs-lookup"><span data-stu-id="c6f58-300">When debug is disabled, hello value for `ALLOWED_HOSTS` needs toobe updated tooinclude hello Azure host name.</span></span> <span data-ttu-id="c6f58-301">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="c6f58-301">For example:</span></span>

    ALLOWED_HOSTS = (
        'pythonapp.azurewebsites.net',
    )

<span data-ttu-id="c6f58-302">lub tooenable żadnych:</span><span class="sxs-lookup"><span data-stu-id="c6f58-302">or tooenable any:</span></span>

    ALLOWED_HOSTS = (
        '*',
    )

<span data-ttu-id="c6f58-303">W praktyce może być toodo coś bardziej złożonych toodeal przełączania debugowania i wydania tryb i nazwy hosta hello pobierania.</span><span class="sxs-lookup"><span data-stu-id="c6f58-303">In practice, you may want toodo something more complex toodeal with switching between debug and release mode, and getting hello host name.</span></span>

<span data-ttu-id="c6f58-304">Można ustawić zmienne środowiskowe za pośrednictwem portalu Azure hello **Konfiguruj** strony w hello **ustawień aplikacji** sekcji.</span><span class="sxs-lookup"><span data-stu-id="c6f58-304">You can set environment variables through hello Azure portal **CONFIGURE** page, in hello **app settings** section.</span></span>  <span data-ttu-id="c6f58-305">Może to być przydatne do ustawiania wartości, które nie mogą podlegać tooappear w hello źródłach (parametry połączenia, hasła itp.) lub, które mają tooset inaczej platformy Azure i komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="c6f58-305">This can be useful for setting values that you may not want tooappear in hello sources (connection strings, passwords, etc), or that you want tooset differently between Azure and your local machine.</span></span> <span data-ttu-id="c6f58-306">W `settings.py`, można zbadać za pomocą zmiennych środowiskowych hello `os.getenv`.</span><span class="sxs-lookup"><span data-stu-id="c6f58-306">In `settings.py`, you can query hello environment variables using `os.getenv`.</span></span>

## <a name="using-a-database"></a><span data-ttu-id="c6f58-307">Korzystanie z bazy danych</span><span class="sxs-lookup"><span data-stu-id="c6f58-307">Using a Database</span></span>
<span data-ttu-id="c6f58-308">Hello bazy danych, która jest zawarta w aplikacji hello jest bazą danych sqlite.</span><span class="sxs-lookup"><span data-stu-id="c6f58-308">hello database that is included with hello application is a sqlite database.</span></span> <span data-ttu-id="c6f58-309">Jest to wygodna i przydatna domyślna baza danych toouse rozwoju, nie wymaga prawie ustawień.</span><span class="sxs-lookup"><span data-stu-id="c6f58-309">This is a convenient and useful default database toouse for development, as it requires almost no setup.</span></span> <span data-ttu-id="c6f58-310">Hello bazy danych są przechowywane w pliku db.sqlite3 hello w folderze projektu hello.</span><span class="sxs-lookup"><span data-stu-id="c6f58-310">hello database is stored in hello db.sqlite3 file in hello project folder.</span></span>

<span data-ttu-id="c6f58-311">Platforma Azure oferuje usługi bazy danych, które są łatwe toouse z poziomu aplikacji Django.</span><span class="sxs-lookup"><span data-stu-id="c6f58-311">Azure provides database services which are easy toouse from a Django application.</span></span> <span data-ttu-id="c6f58-312">Samouczki dotyczące użycia [bazy danych SQL] i [MySQL] z poziomu aplikacji Django Pokaż kroki hello niezbędne toocreate hello bazy danych usługi, Zmień ustawienia bazy danych hello w `DjangoWebProject/settings.py`i hello biblioteki wymagane tooinstall.</span><span class="sxs-lookup"><span data-stu-id="c6f58-312">Tutorials for using [SQL Database] and [MySQL] from a Django application show hello steps necessary toocreate hello database service, change hello database settings in `DjangoWebProject/settings.py`, and hello libraries required tooinstall.</span></span>

<span data-ttu-id="c6f58-313">Oczywiście jeśli wolisz toomanage własnymi serwerami bazy danych, możesz to zrobić przy użyciu systemu Windows lub Linux maszyn wirtualnych działających na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="c6f58-313">Of course, if you prefer toomanage your own database servers, you can do so using Windows or Linux virtual machines running on Azure.</span></span>

## <a name="django-admin-interface"></a><span data-ttu-id="c6f58-314">Interfejs administracyjny Django</span><span class="sxs-lookup"><span data-stu-id="c6f58-314">Django Admin Interface</span></span>
<span data-ttu-id="c6f58-315">Po rozpoczęciu tworzenia modeli, można toopopulate hello bazy danych określonymi danymi.</span><span class="sxs-lookup"><span data-stu-id="c6f58-315">Once you start building your models, you'll want toopopulate hello database with some data.</span></span> <span data-ttu-id="c6f58-316">Łatwe toodo dodawania i edytowania zawartości w trybie interakcyjnym jest interfejsu administracyjnego Django hello toouse.</span><span class="sxs-lookup"><span data-stu-id="c6f58-316">An easy way toodo add and edit content interactively is toouse hello Django administration interface.</span></span>

<span data-ttu-id="c6f58-317">Hello kod dla interfejsu administracyjnego hello jest umieszczony w komentarzach w źródłach aplikacji hello, ale jest jednoznacznie oznaczony, dlatego możesz go łatwo uaktywnić (Wyszukaj "admin").</span><span class="sxs-lookup"><span data-stu-id="c6f58-317">hello code for hello admin interface is commented out in hello application sources, but it's clearly marked so you can easily enable it (search for 'admin').</span></span>

<span data-ttu-id="c6f58-318">Po włączeniu synchronizacji hello bazy danych, uruchamianie aplikacji hello i przejdź zbyt`/admin`.</span><span class="sxs-lookup"><span data-stu-id="c6f58-318">After it's enabled, synchronize hello database, run hello application and navigate too`/admin`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6f58-319">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c6f58-319">Next Steps</span></span>
<span data-ttu-id="c6f58-320">Wykonaj te toolearn łącza więcej informacji na temat Django i narzędzi Python Tools for Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="c6f58-320">Follow these links toolearn more about Django and Python Tools for Visual Studio:</span></span>

* <span data-ttu-id="c6f58-321">[Dokumentacja platformy Django]</span><span class="sxs-lookup"><span data-stu-id="c6f58-321">[Django Documentation]</span></span>
* <span data-ttu-id="c6f58-322">[narzędzi Python Tools for Visual Studio dokumentacji]</span><span class="sxs-lookup"><span data-stu-id="c6f58-322">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="c6f58-323">Aby uzyskać informacje na temat baz danych SQL Database i MySQL:</span><span class="sxs-lookup"><span data-stu-id="c6f58-323">For information on using SQL Database and MySQL:</span></span>

* <span data-ttu-id="c6f58-324">[Obsługa platformy Django i bazy danych MySQL na platformie Azure przy użyciu narzędzi Python Tools for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="c6f58-324">[Django and MySQL on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="c6f58-325">[Obsługa platformy Django i bazy danych SQL Database na platformie Azure przy użyciu narzędzi Python Tools for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="c6f58-325">[Django and SQL Database on Azure with Python Tools for Visual Studio]</span></span>

<span data-ttu-id="c6f58-326">Aby uzyskać więcej informacji, zobacz hello [Centrum deweloperów języka Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="c6f58-326">For more information, see hello [Python Developer Center](/develop/python/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="c6f58-327">Co zostało zmienione</span><span class="sxs-lookup"><span data-stu-id="c6f58-327">What's changed</span></span>
* <span data-ttu-id="c6f58-328">Toohello przewodnik zmiany z tooApp witryn sieci Web usługi dla: [usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="c6f58-328">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Obsługa platformy Django i bazy danych MySQL na platformie Azure przy użyciu narzędzi Python Tools for Visual Studio]: web-sites-python-ptvs-django-mysql.md
[Obsługa platformy Django i bazy danych SQL Database na platformie Azure przy użyciu narzędzi Python Tools for Visual Studio]: web-sites-python-ptvs-django-sql.md
[bazy danych SQL]: web-sites-python-ptvs-django-sql.md
[MySQL]: web-sites-python-ptvs-django-mysql.md

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
[Dokumentacja platformy Django]: https://www.djangoproject.com/
