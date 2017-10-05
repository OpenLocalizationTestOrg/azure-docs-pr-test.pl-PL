---
title: "Python sieci web aplikacji za pomocą Bottle na platformie Azure"
description: "Samouczek przedstawiający uruchamianie aplikacji sieci Web w języku Python w aplikacjach Web Apps w usłudze Azure App Service."
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
ms.openlocfilehash: de5831defc395cd8a4033be8c1fc5dc6cbc9d683
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="creating-web-apps-with-bottle-in-azure"></a><span data-ttu-id="fbe5f-103">Tworzenie aplikacji sieci web w języku Bottle na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="fbe5f-103">Creating web apps with Bottle in Azure</span></span>
<span data-ttu-id="fbe5f-104">Ten samouczek zawiera wprowadzenie do uruchamiania środowiska Python w aplikacjach sieci Web usługi aplikacji Azure.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-104">This tutorial describes how to get started running Python in Azure App Service Web Apps.</span></span> <span data-ttu-id="fbe5f-105">Usługa Web Apps zapewnia ograniczony bezpłatny hosting i szybkie wdrażanie, a także możliwość korzystania z języka Python.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span> <span data-ttu-id="fbe5f-106">Wraz z rozwojem aplikacji można przejść do płatnego hostingu i przeprowadzić integrację z innymi usługami Azure.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-106">As your app grows, you can switch to paid hosting, and you can also integrate with all of the other Azure services.</span></span>

<span data-ttu-id="fbe5f-107">Utworzysz aplikację sieci web przy użyciu platformy sieci web Bottle (zobacz alternatywne wersje tego samouczka dla [Django](web-sites-python-create-deploy-django-app.md) i [Flask](web-sites-python-create-deploy-flask-app.md)).</span><span class="sxs-lookup"><span data-stu-id="fbe5f-107">You will create a web app using the Bottle web framework (see alternate versions of this tutorial for [Django](web-sites-python-create-deploy-django-app.md) and [Flask](web-sites-python-create-deploy-flask-app.md)).</span></span> <span data-ttu-id="fbe5f-108">Utworzysz aplikację sieci Web z portalu Azure Marketplace, skonfigurujesz wdrożenie systemu Git i sklonujesz repozytorium lokalnie.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-108">You will create the web app from the Azure Marketplace, set up Git deployment, and clone the repository locally.</span></span> <span data-ttu-id="fbe5f-109">Następnie uruchomisz aplikacji sieci web lokalnie, wprowadzić zmiany, zatwierdzenia i wypychanie ich na [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="fbe5f-109">Then you will run the web app locally, make changes, commit and push them to [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="fbe5f-110">Samouczek pokazuje, jak można to zrobić w systemie Windows lub Mac/Linux.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-110">The tutorial shows how to do this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="fbe5f-111">Jeśli chcesz zacząć korzystać z usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź do artykułu [Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), w którym wyjaśniono, jak od razu utworzyć początkową aplikację sieci Web o krótkim okresie istnienia w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-111">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="fbe5f-112">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="fbe5f-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="fbe5f-113">Prerequisites</span></span>
* <span data-ttu-id="fbe5f-114">System Windows, Mac lub Linux</span><span class="sxs-lookup"><span data-stu-id="fbe5f-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="fbe5f-115">Środowisko Python w wersji 2.7 lub 3.4</span><span class="sxs-lookup"><span data-stu-id="fbe5f-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="fbe5f-116">Narzędzia setuptools pip, virtualenv (tylko środowisko Python 2.7)</span><span class="sxs-lookup"><span data-stu-id="fbe5f-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="fbe5f-117">Usługa Git</span><span class="sxs-lookup"><span data-stu-id="fbe5f-117">Git</span></span>
* <span data-ttu-id="fbe5f-118">[Narzędzia Python Tools 2.2 for Visual Studio][Python Tools 2.2 for Visual Studio] (PTVS) — Uwaga: ten krok jest opcjonalny</span><span class="sxs-lookup"><span data-stu-id="fbe5f-118">[Python Tools 2.2 for Visual Studio][Python Tools 2.2 for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="fbe5f-119">**Uwaga**: publikowanie TFS nie jest obecnie obsługiwane dla projektów języka Python.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="fbe5f-120">Windows</span><span class="sxs-lookup"><span data-stu-id="fbe5f-120">Windows</span></span>
<span data-ttu-id="fbe5f-121">Jeśli środowisko Python 2.7 lub 3.4 (32-bitowe) nie zostało jeszcze zainstalowane, zalecane jest zainstalowanie [Zestaw Azure SDK dla języka Python w wersji 2.7] lub [zestawu Azure SDK dla języka Python 3.4] przy użyciu Instalatora platformy sieci Web.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span> <span data-ttu-id="fbe5f-122">Spowoduje to zainstalowanie 32-bitowej wersji środowiska Python, narzędzi setuptools, pip i virtualenv itp. (32-bitowe środowisko Python jest instalowane na maszynach hostów Azure).</span><span class="sxs-lookup"><span data-stu-id="fbe5f-122">This installs the 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on the Azure host machines).</span></span> <span data-ttu-id="fbe5f-123">Możesz również pobrać środowisko Python z witryny [python.org].</span><span class="sxs-lookup"><span data-stu-id="fbe5f-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="fbe5f-124">W przypadku systemu Git zalecane jest narzędzie [Git dla systemu Windows] lub [Github dla systemu Windows].</span><span class="sxs-lookup"><span data-stu-id="fbe5f-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span> <span data-ttu-id="fbe5f-125">Jeśli używasz programu Visual Studio, możesz korzystać ze zintegrowanej obsługi systemu Git.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-125">If you use Visual Studio, you can use the integrated Git support.</span></span>

<span data-ttu-id="fbe5f-126">Zalecane jest również zainstalowanie narzędzi [Python Tools 2.2 for Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="fbe5f-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span> <span data-ttu-id="fbe5f-127">Jest to opcjonalne, ale jeśli masz program [Program Visual Studio], taki jak bezpłatny program Visual Studio Community 2013 lub Visual Studio Express 2013 for Web, możesz korzystać z doskonałego środowiska IDE języka Python.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-127">This is optional, but if you have [Visual Studio], including the free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="fbe5f-128">System Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="fbe5f-128">Mac/Linux</span></span>
<span data-ttu-id="fbe5f-129">Środowisko Python i system Git powinny być już zainstalowane, ale upewnij się, że masz środowisko Python 2.7 lub 3.4.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-creation-on-the-azure-portal"></a><span data-ttu-id="fbe5f-130">Tworzenie aplikacji sieci Web w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="fbe5f-130">Web app creation on the Azure Portal</span></span>
<span data-ttu-id="fbe5f-131">Pierwszym krokiem procedury tworzenia aplikacji jest utworzenie aplikacji sieci Web za pośrednictwem [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fbe5f-131">The first step in creating your app is to create the web app via the [Azure Portal](https://portal.azure.com).</span></span>  

1. <span data-ttu-id="fbe5f-132">Zaloguj się do Portalu Azure i kliknij przycisk **NOWY** w lewym dolnym rogu.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-132">Log into the Azure Portal and click the **NEW** button in the bottom left corner.</span></span> 
2. <span data-ttu-id="fbe5f-133">W polu wyszukiwania wpisz „python”.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-133">In the search box, type "python".</span></span>
3. <span data-ttu-id="fbe5f-134">W wynikach wyszukiwania wybierz **Bottle**, następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-134">In the search results, select **Bottle**, then click **Create**.</span></span>
4. <span data-ttu-id="fbe5f-135">Skonfiguruj nową aplikację Bottle, takich jak tworzenie nowego planu usługi App Service i nowej grupy zasobów dla niego.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-135">Configure the new Bottle app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="fbe5f-136">Następnie kliknij pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-136">Then, click **Create**.</span></span>
5. <span data-ttu-id="fbe5f-137">Skonfiguruj publikowanie w systemie Git dla nowo utworzonej aplikacji sieci Web zgodnie z poniższymi instrukcjami w artykule [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md) (Lokalne wdrażanie przy użyciu systemu Git w usłudze Azure App Service).</span><span class="sxs-lookup"><span data-stu-id="fbe5f-137">Configure Git publishing for your newly created web app by following the instructions at [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="fbe5f-138">Omówienie aplikacji</span><span class="sxs-lookup"><span data-stu-id="fbe5f-138">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="fbe5f-139">Zawartość repozytorium Git</span><span class="sxs-lookup"><span data-stu-id="fbe5f-139">Git repository contents</span></span>
<span data-ttu-id="fbe5f-140">Poniżej przedstawiono pliki w początkowym repozytorium Git, które sklonujemy w następnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-140">Here's an overview of the files you'll find in the initial Git repository, which we'll clone in the next section.</span></span>

    \routes.py
    \static\content\
    \static\fonts\
    \static\scripts\
    \views\about.tpl
    \views\contact.tpl
    \views\index.tpl
    \views\layout.tpl

<span data-ttu-id="fbe5f-141">Główne źródła dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-141">Main sources for the application.</span></span> <span data-ttu-id="fbe5f-142">Składa się z 3 stron (indeks, informacje, kontakt) z układem głównym.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-142">Consists of 3 pages (index, about, contact) with a master layout.</span></span>  <span data-ttu-id="fbe5f-143">Zawartość statyczna i skrypty obejmują bootstrap, jquery, modernizr i respond.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-143">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \app.py

<span data-ttu-id="fbe5f-144">Lokalne działania projektowe obsługi serwera.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-144">Local development server support.</span></span> <span data-ttu-id="fbe5f-145">Umożliwia uruchamianie aplikacji lokalnie.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-145">Use this to run the application locally.</span></span>

    \BottleWebProject.pyproj
    \BottleWebProject.sln

<span data-ttu-id="fbe5f-146">Pliki projektu do użycia z narzędziami [Python Tools for Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="fbe5f-146">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="fbe5f-147">Serwer proxy usług IIS dla środowisk wirtualnych i obsługa zdalnego debugowania narzędzi PTVS.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-147">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="fbe5f-148">Pakiety zewnętrzne wymagane przez tę aplikację.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-148">External packages needed by this application.</span></span> <span data-ttu-id="fbe5f-149">Skrypt wdrożenia będzie instalować przy użyciu narzędzia pip pakiety wymienione w tym pliku.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-149">The deployment script will pip install the packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="fbe5f-150">Pliki konfiguracji programu IIS.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-150">IIS configuration files.</span></span> <span data-ttu-id="fbe5f-151">Skrypt wdrożenia użyje odpowiedniego pliku web.x.y.config i skopiuje go jako plik web.config.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-151">The deployment script will use the appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="fbe5f-152">Pliki opcjonalne — dostosowywanie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="fbe5f-152">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="fbe5f-153">Pliki opcjonalne — środowisko uruchomieniowe języka Python</span><span class="sxs-lookup"><span data-stu-id="fbe5f-153">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="fbe5f-154">Dodatkowe pliki na serwerze</span><span class="sxs-lookup"><span data-stu-id="fbe5f-154">Additional files on server</span></span>
<span data-ttu-id="fbe5f-155">Niektóre pliki istnieją na serwerze, ale nie są dodawane do repozytorium git.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-155">Some files exist on the server but are not added to the git repository.</span></span> <span data-ttu-id="fbe5f-156">Są one tworzone przez skrypt wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-156">These are created by the deployment script.</span></span>

    \web.config

<span data-ttu-id="fbe5f-157">Plik konfiguracji programu IIS.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-157">IIS configuration file.</span></span> <span data-ttu-id="fbe5f-158">Tworzony na podstawie pliku web.x.y.config przy każdym wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-158">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="fbe5f-159">Środowisko wirtualne języka Python.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-159">Python virtual environment.</span></span> <span data-ttu-id="fbe5f-160">Tworzone podczas wdrażania, jeśli nie istnieje jeszcze zgodne środowisko wirtualne dla aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-160">Created during deployment if a compatible virtual environment doesn't already exist on the web app.</span></span>  <span data-ttu-id="fbe5f-161">Pakiety wymienione w pliku requirements.txt są instalowane przy użyciu narzędzia pip, ale narzędzie pip pomija instalację, jeśli pakiety zostały już zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-161">Packages listed in requirements.txt are pip installed, but pip will skip installation if the packages are already installed.</span></span>

<span data-ttu-id="fbe5f-162">W 3 następnych sekcjach opisano procedury wdrażania aplikacji sieci Web w 3 różnych środowiskach:</span><span class="sxs-lookup"><span data-stu-id="fbe5f-162">The next 3 sections describe how to proceed with the web app development under 3 different environments:</span></span>

* <span data-ttu-id="fbe5f-163">System Windows — przy użyciu narzędzi Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fbe5f-163">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="fbe5f-164">System Windows — przy użyciu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="fbe5f-164">Windows, with command line</span></span>
* <span data-ttu-id="fbe5f-165">System Mac/Linux — przy użyciu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="fbe5f-165">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="fbe5f-166">Sieci Web - Windows - Python narzędzia do programowania aplikacji dla programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fbe5f-166">Web App development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="fbe5f-167">Klonowanie repozytorium</span><span class="sxs-lookup"><span data-stu-id="fbe5f-167">Clone the repository</span></span>
<span data-ttu-id="fbe5f-168">Najpierw sklonuj repozytorium przy użyciu adresu url podanego w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-168">First, clone the repository using the url provided on the Azure Portal.</span></span> <span data-ttu-id="fbe5f-169">Aby uzyskać więcej informacji, zobacz [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md) (Lokalne wdrażanie przy użyciu systemu Git w usłudze Azure App Service).</span><span class="sxs-lookup"><span data-stu-id="fbe5f-169">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="fbe5f-170">Otwórz plik rozwiązania (SLN), który znajduje się w folderze głównym repozytorium.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-170">Open the solution file (.sln) that is included in the root of the repository.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-solution-bottle.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="fbe5f-171">Tworzenie środowiska wirtualnego</span><span class="sxs-lookup"><span data-stu-id="fbe5f-171">Create virtual environment</span></span>
<span data-ttu-id="fbe5f-172">Teraz utwórz środowisko wirtualne dla wdrożenia lokalnego.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-172">Now we'll create a virtual environment for local development.</span></span> <span data-ttu-id="fbe5f-173">Kliknij prawym przyciskiem myszy pozycję **Środowiska Python** i wybierz pozycję **Dodaj środowisko wirtualne**.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-173">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="fbe5f-174">Upewnij się, że nazwa środowiska to `env`.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-174">Make sure the name of the environment is `env`.</span></span>
* <span data-ttu-id="fbe5f-175">Wybierz interpreter podstawowy.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-175">Select the base interpreter.</span></span> <span data-ttu-id="fbe5f-176">Upewnij się, że jest używana ta sama wersja środowiska Python, którą wybrano dla aplikacji sieci Web (w pliku runtime.txt lub bloku **Ustawienia aplikacji** dla aplikacji sieci Web w Portalu Azure).</span><span class="sxs-lookup"><span data-stu-id="fbe5f-176">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span></span>
* <span data-ttu-id="fbe5f-177">Upewnij się, że opcja pobierania i instalowania pakietów została zaznaczona.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-177">Make sure the option to download and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="fbe5f-178">Kliknij pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-178">Click **Create**.</span></span> <span data-ttu-id="fbe5f-179">Spowoduje to utworzenie środowiska wirtualnego i zainstalowanie składników zależnych wymienionych w pliku requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-179">This will create the virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="fbe5f-180">Uruchamianie przy użyciu serwera projektowego</span><span class="sxs-lookup"><span data-stu-id="fbe5f-180">Run using development server</span></span>
<span data-ttu-id="fbe5f-181">Naciśnij klawisz F5, aby rozpocząć debugowanie. Spowoduje to automatyczne otwarcie przeglądarki sieci Web i wyświetlenie strony uruchomionej lokalnie.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-181">Press F5 to start debugging, and your web browser will open automatically to the page running locally.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-browser-bottle.png)

<span data-ttu-id="fbe5f-182">Można ustawiać punkty przerwania w źródłach, używać okien wyrażeń kontrolnych itp. Zapoznaj się z [Dokumentacja narzędzi Python Tools for Visual Studio], aby uzyskać więcej informacji na temat różnych funkcji.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-182">You can set breakpoints in the sources, use the watch windows, etc. See the [Python Tools for Visual Studio Documentation] for more information on the various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="fbe5f-183">Wprowadzanie zmian</span><span class="sxs-lookup"><span data-stu-id="fbe5f-183">Make changes</span></span>
<span data-ttu-id="fbe5f-184">Teraz możesz eksperymentować, wprowadzając zmiany w źródłach i/lub szablonach aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-184">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="fbe5f-185">Po przetestowaniu wprowadzonych zmian zatwierdź je w repozytorium Git:</span><span class="sxs-lookup"><span data-stu-id="fbe5f-185">After you've tested your changes, commit them to the Git repository:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-commit-bottle.png)

### <a name="install-more-packages"></a><span data-ttu-id="fbe5f-186">Instalowanie dodatkowych pakietów</span><span class="sxs-lookup"><span data-stu-id="fbe5f-186">Install more packages</span></span>
<span data-ttu-id="fbe5f-187">Aplikacja może mieć zależności poza środowiskiem Python i Bottle.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-187">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="fbe5f-188">Możesz zainstalować dodatkowe pakiety przy użyciu narzędzia pip.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-188">You can install additional packages using pip.</span></span> <span data-ttu-id="fbe5f-189">Aby zainstalować pakiet, kliknij prawym przyciskiem myszy środowisko wirtualne i wybierz pozycję **Zainstaluj pakiet języka Python**.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-189">To install a package, right-click on the virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="fbe5f-190">Aby na przykład zainstalować zestaw Azure SDK dla języka Python zapewniający dostęp do magazynu Azure, magistrali usług i innych usług Azure, wprowadź `azure`:</span><span class="sxs-lookup"><span data-stu-id="fbe5f-190">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-install-package-dialog.png)

<span data-ttu-id="fbe5f-191">Kliknij prawym przyciskiem myszy środowisko wirtualne i wybierz pozycję **Generuj plik requirements.txt**, aby zaktualizować plik requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-191">Right-click on the virtual environment and select **Generate requirements.txt** to update requirements.txt.</span></span>

<span data-ttu-id="fbe5f-192">Następnie zatwierdź zmiany w pliku requirements.txt w repozytorium Git.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-192">Then, commit the changes to requirements.txt to the Git repository.</span></span>

### <a name="deploy-to-azure"></a><span data-ttu-id="fbe5f-193">Wdrażanie na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="fbe5f-193">Deploy to Azure</span></span>
<span data-ttu-id="fbe5f-194">Aby wyzwolić wdrożenie, kliknij pozycję **Synchronizuj** lub **Wypchnij**.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-194">To trigger a deployment, click on **Sync** or **Push**.</span></span> <span data-ttu-id="fbe5f-195">Synchronizacja obejmuje zarówno wypychanie, jak i ściąganie.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-195">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-git-push.png)

<span data-ttu-id="fbe5f-196">Pierwsze wdrożenie trwa dłużej, ponieważ obejmuje tworzenie środowiska wirtualnego, instalowanie pakietów itp.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-196">The first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="fbe5f-197">Program Visual Studio nie wyświetla postępu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-197">Visual Studio doesn't show the progress of the deployment.</span></span> <span data-ttu-id="fbe5f-198">Jeśli chcesz przejrzeć dane wyjściowe, zobacz sekcję [Rozwiązywanie problemów — wdrożenie](#troubleshooting-deployment).</span><span class="sxs-lookup"><span data-stu-id="fbe5f-198">If you'd like to review the output, see the section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="fbe5f-199">Przejdź do adresu URL platformy Azure, aby przejrzeć wprowadzone zmiany.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-199">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="fbe5f-200">Wiersz polecenia - Windows - tworzenie aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="fbe5f-200">Web app development - Windows - Command Line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="fbe5f-201">Klonowanie repozytorium</span><span class="sxs-lookup"><span data-stu-id="fbe5f-201">Clone the repository</span></span>
<span data-ttu-id="fbe5f-202">Najpierw sklonuj repozytorium przy użyciu adresu URL podanego w witrynie Azure Portal i dodaj repozytorium Azure jako repozytorium zdalne.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-202">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="fbe5f-203">Aby uzyskać więcej informacji, zobacz [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md) (Lokalne wdrażanie przy użyciu systemu Git w usłudze Azure App Service).</span><span class="sxs-lookup"><span data-stu-id="fbe5f-203">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="fbe5f-204">Tworzenie środowiska wirtualnego</span><span class="sxs-lookup"><span data-stu-id="fbe5f-204">Create virtual environment</span></span>
<span data-ttu-id="fbe5f-205">Zostanie utworzone nowe środowisko wirtualne dla celów wdrożenia (nie należy dodawać go do repozytorium).</span><span class="sxs-lookup"><span data-stu-id="fbe5f-205">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span> <span data-ttu-id="fbe5f-206">Nie można zmieniać lokalizacji wirtualnych środowisk języka Python, dlatego każdy deweloper pracujący nad aplikacją tworzy własne środowisko lokalnie.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-206">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="fbe5f-207">Upewnij się, że jest używana ta sama wersja środowiska Python, którą wybrano dla aplikacji sieci web (w pliku runtime.txt lub bloku ustawienia aplikacji dla aplikacji sieci web w portalu Azure)</span><span class="sxs-lookup"><span data-stu-id="fbe5f-207">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the Application Settings blade for your web app in the Azure Portal)</span></span>

<span data-ttu-id="fbe5f-208">Dla środowiska Python w wersji 2.7:</span><span class="sxs-lookup"><span data-stu-id="fbe5f-208">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="fbe5f-209">Dla środowiska Python w wersji 3.4:</span><span class="sxs-lookup"><span data-stu-id="fbe5f-209">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="fbe5f-210">Zainstaluj pakiety zewnętrzne wymagane przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-210">Install any external packages required by your application.</span></span> <span data-ttu-id="fbe5f-211">Korzystając z pliku requirements.txt w folderze głównym repozytorium, możesz instalować pakiety w środowisku wirtualnym:</span><span class="sxs-lookup"><span data-stu-id="fbe5f-211">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="fbe5f-212">Uruchamianie przy użyciu serwera projektowego</span><span class="sxs-lookup"><span data-stu-id="fbe5f-212">Run using development server</span></span>
<span data-ttu-id="fbe5f-213">Możesz uruchomić aplikację na serwerze projektowym przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="fbe5f-213">You can launch the application under a development server with the following command:</span></span>

    env\scripts\python app.py

<span data-ttu-id="fbe5f-214">Na konsoli zostanie wyświetlony adres URL i port nasłuchiwany przez serwer:</span><span class="sxs-lookup"><span data-stu-id="fbe5f-214">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-run-local-bottle.png)

<span data-ttu-id="fbe5f-215">Następnie otwórz w przeglądarce sieci Web stronę wskazywaną przez ten adres URL.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-215">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-browser-bottle.png)

### <a name="make-changes"></a><span data-ttu-id="fbe5f-216">Wprowadzanie zmian</span><span class="sxs-lookup"><span data-stu-id="fbe5f-216">Make changes</span></span>
<span data-ttu-id="fbe5f-217">Teraz możesz eksperymentować, wprowadzając zmiany w źródłach i/lub szablonach aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-217">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="fbe5f-218">Po przetestowaniu wprowadzonych zmian zatwierdź je w repozytorium Git:</span><span class="sxs-lookup"><span data-stu-id="fbe5f-218">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="fbe5f-219">Instalowanie dodatkowych pakietów</span><span class="sxs-lookup"><span data-stu-id="fbe5f-219">Install more packages</span></span>
<span data-ttu-id="fbe5f-220">Aplikacja może mieć zależności poza środowiskiem Python i Bottle.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-220">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="fbe5f-221">Możesz zainstalować dodatkowe pakiety przy użyciu narzędzia pip.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-221">You can install additional packages using pip.</span></span> <span data-ttu-id="fbe5f-222">Aby na przykład zainstalować zestaw Azure SDK dla języka Python zapewniający dostęp do magazynu Azure, magistrali usług i innych usług Azure, wpisz:</span><span class="sxs-lookup"><span data-stu-id="fbe5f-222">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="fbe5f-223">Pamiętaj o zaktualizowaniu pliku requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="fbe5f-223">Make sure to update requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="fbe5f-224">Zatwierdź zmiany:</span><span class="sxs-lookup"><span data-stu-id="fbe5f-224">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="fbe5f-225">Wdrażanie na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="fbe5f-225">Deploy to Azure</span></span>
<span data-ttu-id="fbe5f-226">Aby wyzwolić wdrożenie, wypchnij zmiany na platformę Azure:</span><span class="sxs-lookup"><span data-stu-id="fbe5f-226">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="fbe5f-227">Zostaną wyświetlone dane wyjściowe skryptu wdrożenia, łącznie z tworzeniem środowiska wirtualnego, instalowaniem pakietów i tworzeniem pliku web.config.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-227">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="fbe5f-228">Przejdź do adresu URL platformy Azure, aby przejrzeć wprowadzone zmiany.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-228">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="fbe5f-229">Wdrażanie aplikacji sieci Web — system Mac/Linux — wiersz polecenia</span><span class="sxs-lookup"><span data-stu-id="fbe5f-229">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="fbe5f-230">Klonowanie repozytorium</span><span class="sxs-lookup"><span data-stu-id="fbe5f-230">Clone the repository</span></span>
<span data-ttu-id="fbe5f-231">Najpierw sklonuj repozytorium przy użyciu adresu URL podanego w witrynie Azure Portal i dodaj repozytorium Azure jako repozytorium zdalne.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-231">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="fbe5f-232">Aby uzyskać więcej informacji, zobacz [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md) (Lokalne wdrażanie przy użyciu systemu Git w usłudze Azure App Service).</span><span class="sxs-lookup"><span data-stu-id="fbe5f-232">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="fbe5f-233">Tworzenie środowiska wirtualnego</span><span class="sxs-lookup"><span data-stu-id="fbe5f-233">Create virtual environment</span></span>
<span data-ttu-id="fbe5f-234">Zostanie utworzone nowe środowisko wirtualne dla celów wdrożenia (nie należy dodawać go do repozytorium).</span><span class="sxs-lookup"><span data-stu-id="fbe5f-234">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span> <span data-ttu-id="fbe5f-235">Nie można zmieniać lokalizacji wirtualnych środowisk języka Python, dlatego każdy deweloper pracujący nad aplikacją tworzy własne środowisko lokalnie.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-235">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="fbe5f-236">Upewnij się, że jest używana ta sama wersja środowiska Python, którą wybrano dla aplikacji sieci Web (w pliku runtime.txt lub bloku Ustawienia aplikacji dla aplikacji sieci Web w Portalu Azure).</span><span class="sxs-lookup"><span data-stu-id="fbe5f-236">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the Application Settings blade of your web app in the Azure Portal).</span></span>

<span data-ttu-id="fbe5f-237">Dla środowiska Python w wersji 2.7:</span><span class="sxs-lookup"><span data-stu-id="fbe5f-237">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="fbe5f-238">Dla środowiska Python w wersji 3.4:</span><span class="sxs-lookup"><span data-stu-id="fbe5f-238">For Python 3.4:</span></span>

    python -m venv env
<span data-ttu-id="fbe5f-239">lub pyvenv env</span><span class="sxs-lookup"><span data-stu-id="fbe5f-239">or pyvenv env</span></span>

<span data-ttu-id="fbe5f-240">Zainstaluj pakiety zewnętrzne wymagane przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-240">Install any external packages required by your application.</span></span> <span data-ttu-id="fbe5f-241">Korzystając z pliku requirements.txt w folderze głównym repozytorium, możesz instalować pakiety w środowisku wirtualnym:</span><span class="sxs-lookup"><span data-stu-id="fbe5f-241">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="fbe5f-242">Uruchamianie przy użyciu serwera projektowego</span><span class="sxs-lookup"><span data-stu-id="fbe5f-242">Run using development server</span></span>
<span data-ttu-id="fbe5f-243">Możesz uruchomić aplikację na serwerze projektowym przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="fbe5f-243">You can launch the application under a development server with the following command:</span></span>

    env/bin/python app.py

<span data-ttu-id="fbe5f-244">Na konsoli zostanie wyświetlony adres URL i port nasłuchiwany przez serwer:</span><span class="sxs-lookup"><span data-stu-id="fbe5f-244">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/mac-run-local-bottle.png)

<span data-ttu-id="fbe5f-245">Następnie otwórz w przeglądarce sieci Web stronę wskazywaną przez ten adres URL.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-245">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/mac-browser-bottle.png)

### <a name="make-changes"></a><span data-ttu-id="fbe5f-246">Wprowadzanie zmian</span><span class="sxs-lookup"><span data-stu-id="fbe5f-246">Make changes</span></span>
<span data-ttu-id="fbe5f-247">Teraz możesz eksperymentować, wprowadzając zmiany w źródłach i/lub szablonach aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-247">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="fbe5f-248">Po przetestowaniu wprowadzonych zmian zatwierdź je w repozytorium Git:</span><span class="sxs-lookup"><span data-stu-id="fbe5f-248">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="fbe5f-249">Instalowanie dodatkowych pakietów</span><span class="sxs-lookup"><span data-stu-id="fbe5f-249">Install more packages</span></span>
<span data-ttu-id="fbe5f-250">Aplikacja może mieć zależności poza środowiskiem Python i Bottle.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-250">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="fbe5f-251">Możesz zainstalować dodatkowe pakiety przy użyciu narzędzia pip.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-251">You can install additional packages using pip.</span></span> <span data-ttu-id="fbe5f-252">Aby na przykład zainstalować zestaw Azure SDK dla języka Python zapewniający dostęp do magazynu Azure, magistrali usług i innych usług Azure, wpisz:</span><span class="sxs-lookup"><span data-stu-id="fbe5f-252">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="fbe5f-253">Pamiętaj o zaktualizowaniu pliku requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="fbe5f-253">Make sure to update requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="fbe5f-254">Zatwierdź zmiany:</span><span class="sxs-lookup"><span data-stu-id="fbe5f-254">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="fbe5f-255">Wdrażanie na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="fbe5f-255">Deploy to Azure</span></span>
<span data-ttu-id="fbe5f-256">Aby wyzwolić wdrożenie, wypchnij zmiany na platformę Azure:</span><span class="sxs-lookup"><span data-stu-id="fbe5f-256">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="fbe5f-257">Zostaną wyświetlone dane wyjściowe skryptu wdrożenia, łącznie z tworzeniem środowiska wirtualnego, instalowaniem pakietów i tworzeniem pliku web.config.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-257">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="fbe5f-258">Przejdź do adresu URL platformy Azure, aby przejrzeć wprowadzone zmiany.</span><span class="sxs-lookup"><span data-stu-id="fbe5f-258">Browse to the Azure URL to view your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="fbe5f-259">Rozwiązywanie problemów — instalowanie pakietów</span><span class="sxs-lookup"><span data-stu-id="fbe5f-259">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="fbe5f-260">Rozwiązywanie problemów — środowisko wirtualne</span><span class="sxs-lookup"><span data-stu-id="fbe5f-260">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="fbe5f-261">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fbe5f-261">Next Steps</span></span>
<span data-ttu-id="fbe5f-262">Skorzystaj z poniższych linków, aby dowiedzieć się więcej o Bottle i narzędzi Python Tools for Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="fbe5f-262">Follow these links to learn more about Bottle and Python Tools for Visual Studio:</span></span> 

* <span data-ttu-id="fbe5f-263">[Dokumentacja bottle]</span><span class="sxs-lookup"><span data-stu-id="fbe5f-263">[Bottle Documentation]</span></span>
* <span data-ttu-id="fbe5f-264">[Dokumentacja narzędzi Python Tools for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="fbe5f-264">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="fbe5f-265">Aby uzyskać informacje o korzystaniu z magazynu tabel platformy Azure i bazy danych MongoDB:</span><span class="sxs-lookup"><span data-stu-id="fbe5f-265">For information on using Azure Table Storage and MongoDB:</span></span>

* <span data-ttu-id="fbe5f-266">[Bottle i bazy danych MongoDB na platformie Azure przy użyciu narzędzi Python Tools for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="fbe5f-266">[Bottle and MongoDB on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="fbe5f-267">[Bottle i magazynu tabel platformy Azure na platformie Azure przy użyciu narzędzi Python Tools for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="fbe5f-267">[Bottle and Azure Table Storage on Azure with Python Tools for Visual Studio]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="fbe5f-268">Co zostało zmienione</span><span class="sxs-lookup"><span data-stu-id="fbe5f-268">What's changed</span></span>
* <span data-ttu-id="fbe5f-269">Przewodnik dotyczący przejścia od usługi Witryny sieci Web do usługi App Service można znaleźć w temacie [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714) (Usługa Azure App Service i jej wpływ na istniejące usługi platformy Azure).</span><span class="sxs-lookup"><span data-stu-id="fbe5f-269">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
<span data-ttu-id="fbe5f-270">[Bottle i bazy danych MongoDB na platformie Azure przy użyciu narzędzi Python Tools for Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md</span><span class="sxs-lookup"><span data-stu-id="fbe5f-270">[Bottle and MongoDB on Azure with Python Tools for Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md</span></span>
<span data-ttu-id="fbe5f-271">[Bottle i magazynu tabel platformy Azure na platformie Azure przy użyciu narzędzi Python Tools for Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md</span><span class="sxs-lookup"><span data-stu-id="fbe5f-271">[Bottle and Azure Table Storage on Azure with Python Tools for Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md</span></span>

<!--External Link references-->
<span data-ttu-id="fbe5f-272">[Zestaw Azure SDK dla języka Python w wersji 2.7]: http://go.microsoft.com/fwlink/?linkid=254281</span><span class="sxs-lookup"><span data-stu-id="fbe5f-272">[Azure SDK for Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281</span></span>
<span data-ttu-id="fbe5f-273">[zestawu Azure SDK dla języka Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990</span><span class="sxs-lookup"><span data-stu-id="fbe5f-273">[Azure SDK for Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990</span></span>
<span data-ttu-id="fbe5f-274">[python.org]: http://www.python.org/</span><span class="sxs-lookup"><span data-stu-id="fbe5f-274">[python.org]: http://www.python.org/</span></span>
<span data-ttu-id="fbe5f-275">[Git dla systemu Windows]: http://msysgit.github.io/</span><span class="sxs-lookup"><span data-stu-id="fbe5f-275">[Git for Windows]: http://msysgit.github.io/</span></span>
<span data-ttu-id="fbe5f-276">[Github dla systemu Windows]: https://windows.github.com/</span><span class="sxs-lookup"><span data-stu-id="fbe5f-276">[GitHub for Windows]: https://windows.github.com/</span></span>
<span data-ttu-id="fbe5f-277">[Python Tools for Visual Studio]: http://aka.ms/ptvs</span><span class="sxs-lookup"><span data-stu-id="fbe5f-277">[Python Tools for Visual Studio]: http://aka.ms/ptvs</span></span>
<span data-ttu-id="fbe5f-278">[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span><span class="sxs-lookup"><span data-stu-id="fbe5f-278">[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span></span>
<span data-ttu-id="fbe5f-279">[Program Visual Studio]: http://www.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="fbe5f-279">[Visual Studio]: http://www.visualstudio.com/</span></span>
<span data-ttu-id="fbe5f-280">[Dokumentacja narzędzi Python Tools for Visual Studio]: http://aka.ms/ptvsdocs </span><span class="sxs-lookup"><span data-stu-id="fbe5f-280">[Python Tools for Visual Studio Documentation]: http://aka.ms/ptvsdocs </span></span>
<span data-ttu-id="fbe5f-281">[Dokumentacja bottle]: http://bottlepy.org/docs/dev/index.html</span><span class="sxs-lookup"><span data-stu-id="fbe5f-281">[Bottle Documentation]: http://bottlepy.org/docs/dev/index.html</span></span>

