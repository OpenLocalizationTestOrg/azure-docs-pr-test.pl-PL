---
title: "aaaInstall Python i hello SDK — Azure"
description: "Dowiedz się, jak toouse tooinstall Python i hello zestawu SDK platformy Azure."
services: 
documentationcenter: python
author: lmazuel
manager: wpickett
editor: 
ms.assetid: f36294be-daeb-4caf-9129-fce18130f552
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 09/06/2016
ms.author: lmazuel
ms.openlocfilehash: c1b394770f9abd3e654a23d79ae179a9af89e2fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="installing-python-and-hello-sdk"></a><span data-ttu-id="4a945-103">Instalowanie języka Python i hello zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="4a945-103">Installing Python and hello SDK</span></span>
<span data-ttu-id="4a945-104">Python jest łatwe tooset uruchomiony w systemie Windows i jest wstępnie zainstalowane dla komputerów Mac, Linux, a [Bash dla systemu Windows](https://msdn.microsoft.com/commandline/wsl/about).</span><span class="sxs-lookup"><span data-stu-id="4a945-104">Python is easy tooset up on Windows and comes pre-installed on Mac, Linux, and [Bash for Windows](https://msdn.microsoft.com/commandline/wsl/about).</span></span> <span data-ttu-id="4a945-105">Ten przewodnik przeprowadzi Cię przez instalacji i uzyskiwanie komputerze rozpocząć korzystanie z platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4a945-105">This guide walks you through installation and getting your machine ready for use with Azure.</span></span>

## <a name="whats-in-hello-python-azure-sdk"></a><span data-ttu-id="4a945-106">Co to jest odpowiednio w hello zestawu Azure SDK Python?</span><span class="sxs-lookup"><span data-stu-id="4a945-106">What's in hello Python Azure SDK?</span></span>
<span data-ttu-id="4a945-107">zestaw Azure SDK for Python Hello obejmuje składniki, które pozwalają toodevelop, wdrażanie i zarządzanie aplikacjami języka Python dla platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4a945-107">hello Azure SDK for Python includes components that allow you toodevelop, deploy, and manage Python applications for Azure.</span></span> <span data-ttu-id="4a945-108">W szczególności hello zestaw Azure SDK for Python zawiera następujące hello:</span><span class="sxs-lookup"><span data-stu-id="4a945-108">Specifically, hello Azure SDK for Python includes hello following:</span></span>

* <span data-ttu-id="4a945-109">**Biblioteki zarządzania**.</span><span class="sxs-lookup"><span data-stu-id="4a945-109">**Management libraries**.</span></span> <span data-ttu-id="4a945-110">Te biblioteki klas udostępniają interfejs zarządzania zasobami platformy Azure, takich jak konta magazynu, maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="4a945-110">These class libraries provide an interface managing Azure resources, such as storage accounts, virtual machines.</span></span>
* <span data-ttu-id="4a945-111">**Biblioteki wykonawcze**.</span><span class="sxs-lookup"><span data-stu-id="4a945-111">**Runtime libraries**.</span></span> <span data-ttu-id="4a945-112">Te biblioteki klas zapewniają interfejs do uzyskiwania dostępu do funkcji platformy Azure, takich jak magazyn i usługi magistrali.</span><span class="sxs-lookup"><span data-stu-id="4a945-112">These class libraries provide an interface for accessing Azure features, such as storage and service bus.</span></span>

## <a name="which-python-and-which-version-toouse"></a><span data-ttu-id="4a945-113">Które Python i które toouse wersji</span><span class="sxs-lookup"><span data-stu-id="4a945-113">Which Python and which version toouse</span></span>
<span data-ttu-id="4a945-114">Istnieje kilka odmian Python tłumaczy — przykłady to między innymi:</span><span class="sxs-lookup"><span data-stu-id="4a945-114">There are several flavors of Python interpreters available - examples include:</span></span>

* <span data-ttu-id="4a945-115">Języka CPython - hello standard i najczęściej używane interpreter języka Python</span><span class="sxs-lookup"><span data-stu-id="4a945-115">CPython - hello standard and most commonly used Python interpreter</span></span>
* <span data-ttu-id="4a945-116">PyPy — szybkie, zgodne alternatywną implementację tooCPython</span><span class="sxs-lookup"><span data-stu-id="4a945-116">PyPy - fast, compliant alternative implementation tooCPython</span></span>
* <span data-ttu-id="4a945-117">IronPython - interpreter języka Python, uruchamianego na .net/CLR</span><span class="sxs-lookup"><span data-stu-id="4a945-117">IronPython - Python interpreter that runs on .Net/CLR</span></span>
* <span data-ttu-id="4a945-118">Jython - interpreter języka Python, uruchamianego na powitania maszyny wirtualnej Java</span><span class="sxs-lookup"><span data-stu-id="4a945-118">Jython - Python interpreter that runs on hello Java Virtual Machine</span></span>

<span data-ttu-id="4a945-119">**Języka CPython** v2.7 lub v3.3 + PyPy 5.4.0 przetestowane i obsługiwane w przypadku hello zestawu Azure SDK Python.</span><span class="sxs-lookup"><span data-stu-id="4a945-119">**CPython** v2.7 or v3.3+ and PyPy 5.4.0 are tested and supported for hello Python Azure SDK.</span></span>

## <a name="where-tooget-python"></a><span data-ttu-id="4a945-120">Gdzie tooget Python?</span><span class="sxs-lookup"><span data-stu-id="4a945-120">Where tooget Python?</span></span>
<span data-ttu-id="4a945-121">Istnieje kilka sposobów tooget języka CPython:</span><span class="sxs-lookup"><span data-stu-id="4a945-121">There are several ways tooget CPython:</span></span>

* <span data-ttu-id="4a945-122">Bezpośrednio z [www.python.org][www.python.org]</span><span class="sxs-lookup"><span data-stu-id="4a945-122">Directly from [www.python.org][www.python.org]</span></span>
* <span data-ttu-id="4a945-123">Z zaufanych distro, takich jak [www.continuum.io][www.continuum.io], [www.enthought.com] [ www.enthought.com] lub [www.activestate.com][www.activestate.com]</span><span class="sxs-lookup"><span data-stu-id="4a945-123">From a reputable distro such as [www.continuum.io][www.continuum.io], [www.enthought.com][www.enthought.com] or [www.activestate.com][www.activestate.com]</span></span>
* <span data-ttu-id="4a945-124">Tworzenie źródła!</span><span class="sxs-lookup"><span data-stu-id="4a945-124">Build from source!</span></span>

<span data-ttu-id="4a945-125">W przypadku braku konkretna potrzeba użycia zalecamy hello dwóch pierwszych opcji.</span><span class="sxs-lookup"><span data-stu-id="4a945-125">Unless you have a specific need, we recommend hello first two options.</span></span>

## <a name="sdk-installation-on-windows-linux-and-macos-client-libraries-only"></a><span data-ttu-id="4a945-126">Instalacja zestawu SDK systemu Windows, Linux i MacOS (tylko w przypadku bibliotek klienta)</span><span class="sxs-lookup"><span data-stu-id="4a945-126">SDK Installation on Windows, Linux, and MacOS (client libraries only)</span></span>
<span data-ttu-id="4a945-127">Jeśli masz już zainstalowany języka Python, można użyć narzędzia pip tooinstall pakiet wszystkich bibliotek klienckich hello w istniejących Python 2.7 lub środowiska Python 3.3 +.</span><span class="sxs-lookup"><span data-stu-id="4a945-127">If you already have Python installed, you can use pip tooinstall a bundle of all hello client libraries in your existing Python 2.7 or Python 3.3+ environment.</span></span> <span data-ttu-id="4a945-128">Spowoduje to pobranie pakietów hello z hello [indeksu pakietów języka Python] [ Python Package Index] (PyPI).</span><span class="sxs-lookup"><span data-stu-id="4a945-128">This downloads hello packages from hello [Python Package Index][Python Package Index] (PyPI).</span></span>

<span data-ttu-id="4a945-129">Prawa administratora może być konieczne:</span><span class="sxs-lookup"><span data-stu-id="4a945-129">You may need administrator rights:</span></span>

* <span data-ttu-id="4a945-130">Linux i MacOS, użyj hello `sudo` polecenia: `sudo pip install azure-mgmt-compute`.</span><span class="sxs-lookup"><span data-stu-id="4a945-130">Linux and MacOS, use hello `sudo` command: `sudo pip install azure-mgmt-compute`.</span></span>
* <span data-ttu-id="4a945-131">System Windows: Otwórz z wiersza polecenia/programu PowerShell jako administrator</span><span class="sxs-lookup"><span data-stu-id="4a945-131">Windows: open your PowerShell/Command prompt as an administrator</span></span>

<span data-ttu-id="4a945-132">Można zainstalować oddzielnie każdej biblioteki dla poszczególnych usług Azure:</span><span class="sxs-lookup"><span data-stu-id="4a945-132">You can install individually each library for each Azure service:</span></span>

```console
   $ pip install azure-batch          # Install hello latest Batch runtime library
   $ pip install azure-mgmt-scheduler # Install hello latest Storage management library
```

<span data-ttu-id="4a945-133">Pakiety w wersji zapoznawczej mogą być instalowane za pomocą hello `--pre` flagi:</span><span class="sxs-lookup"><span data-stu-id="4a945-133">Preview packages can be installed using hello `--pre` flag:</span></span>

```console
   $ pip install --pre azure-mgmt-compute # installs only hello latest Compute Management library
```

<span data-ttu-id="4a945-134">Można także zainstalować zestaw Azure bibliotek w jednym wierszu przy użyciu hello `azure` meta-package.</span><span class="sxs-lookup"><span data-stu-id="4a945-134">You can also install a set of Azure libraries in a single line using hello `azure` meta-package.</span></span> <span data-ttu-id="4a945-135">Ponieważ nie wszystkie pakiety w tym pakiecie meta są jeszcze opublikowane jako stabilny, hello `azure` meta pakiet jest dostępny w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="4a945-135">Since not all packages in this meta-package are published as stable yet, hello `azure` meta-package is still in preview.</span></span>
<span data-ttu-id="4a945-136">Jednak hello pakietami podstawowymi, z perspektywy jakości/kompletności kodu jest uznawana za "stabilna" w tym momencie</span><span class="sxs-lookup"><span data-stu-id="4a945-136">However, hello core packages, from code quality/completeness perspectives can be considered "stable" at this time</span></span>

* <span data-ttu-id="4a945-137">jego jest oficjalnie oznaczony jako takie w synchronizacji z innymi językami tak szybko, jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="4a945-137">it is officially labeled as such in sync with other languages as soon as possible.</span></span>
  <span data-ttu-id="4a945-138">Firma Microsoft nie zaplanowano wszelkie dodatkowe istotne zmiany do tego czasu.</span><span class="sxs-lookup"><span data-stu-id="4a945-138">We are not planning on any further major changes until then.</span></span>

<span data-ttu-id="4a945-139">Ponieważ chodzi o wersji zapoznawczej, należy toouse hello `--pre` flagi:</span><span class="sxs-lookup"><span data-stu-id="4a945-139">Since it's a preview release, you need toouse hello `--pre` flag:</span></span>

```console
   $ pip install --pre azure
```

<span data-ttu-id="4a945-140">lub bezpośrednio</span><span class="sxs-lookup"><span data-stu-id="4a945-140">or directly</span></span>

```console
   $ pip install azure==2.0.0rc6
```

## <a name="getting-more-packages"></a><span data-ttu-id="4a945-141">Pobieranie kolejne pakiety</span><span class="sxs-lookup"><span data-stu-id="4a945-141">Getting More Packages</span></span>
<span data-ttu-id="4a945-142">Witaj [indeksu pakietów języka Python] [ Python Package Index] (PyPI) zawiera bogaty wybór bibliotek języka Python.</span><span class="sxs-lookup"><span data-stu-id="4a945-142">hello [Python Package Index][Python Package Index] (PyPI) has a rich selection of Python libraries.</span></span>  <span data-ttu-id="4a945-143">W przypadku wybrania tooinstall Distro będzie już większość hello interesujące usługi bits dla różnych scenariuszy z sieci web development tooTechnical środowisk obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="4a945-143">If you chose tooinstall a Distro, you'll already have most of hello interesting bits for various scenarios from web development tooTechnical Computing.</span></span>

## <a name="python-tools-for-visual-studio"></a><span data-ttu-id="4a945-144">Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4a945-144">Python Tools for Visual Studio</span></span>
<span data-ttu-id="4a945-145">[Narzędzia Python Tools for Visual Studio][narzędzi Python Tools for Visual Studio] (PTVS) jest wolny OSS dodatku firmy Microsoft, która zmieni się VS w pełni funkcjonalnymi IDE języka Python:</span><span class="sxs-lookup"><span data-stu-id="4a945-145">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) is a free/OSS plugin from Microsoft, which turns VS into a full-fledged Python IDE:</span></span>

![How-do-install-python-ptvs](./media/python-how-to-install/how-to-install-python-ptvs.png)

<span data-ttu-id="4a945-147">Przy użyciu narzędzi PTVS jest opcjonalne, ale jest zalecane, ponieważ umożliwia obsługę języka Python i rozwiązanie projektu sieci Web, debugowanie, profilowanie, okna interaktywnego, edytowanie szablonu i Intellisense.</span><span class="sxs-lookup"><span data-stu-id="4a945-147">Using PTVS is optional, but is recommended as it gives you Python and Web Project/Solution support, debugging, profiling, interactive window, Template editing, and Intellisense.</span></span>

<span data-ttu-id="4a945-148">PTVS ułatwia też łatwo toodeploy tooMicrosoft Azure, z obsługą wdrażania zbyt[usługi w chmurze](cloud-services/cloud-services-python-ptvs.md) i [witryn sieci Web](app-service-web/web-sites-python-ptvs-django-mysql.md).</span><span class="sxs-lookup"><span data-stu-id="4a945-148">PTVS also makes it easy toodeploy tooMicrosoft Azure, with support for deployment too[Cloud Services](cloud-services/cloud-services-python-ptvs.md) and [Websites](app-service-web/web-sites-python-ptvs-django-mysql.md).</span></span>

<span data-ttu-id="4a945-149">PTVS współpracuje z istniejącej instalacji programu Visual Studio 2013, 2015 lub 2017 r.</span><span class="sxs-lookup"><span data-stu-id="4a945-149">PTVS works with your existing Visual Studio 2013, 2015, or 2017 installation.</span></span>  <span data-ttu-id="4a945-150">Dokumentacja, pliki do pobrania i dyskusji dla [narzędzi Python Tools for Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="4a945-150">For documentation, downloads and discussions, see [Python Tools for Visual Studio].</span></span>  

## <a name="python-azure-scenarios-for-linux-and-macos"></a><span data-ttu-id="4a945-151">Python scenariuszy Azure dla systemów Linux i MacOS</span><span class="sxs-lookup"><span data-stu-id="4a945-151">Python Azure Scenarios for Linux and MacOS</span></span>
<span data-ttu-id="4a945-152">Dla systemu Linux lub MacOS, główne Azure scenariusze, które są obsługiwane:</span><span class="sxs-lookup"><span data-stu-id="4a945-152">For Linux or MacOS, main Azure scenarios that are supported:</span></span>

1. <span data-ttu-id="4a945-153">Korzystanie z usług Azure przy użyciu bibliotek klienckich powitania dla języka Python</span><span class="sxs-lookup"><span data-stu-id="4a945-153">Consuming Azure Services by using hello client libraries for Python</span></span>
2. <span data-ttu-id="4a945-154">Uruchamianie aplikacji w Maszynę wirtualną systemu Linux</span><span class="sxs-lookup"><span data-stu-id="4a945-154">Running your app in a Linux VM</span></span>
3. <span data-ttu-id="4a945-155">Tworzenie i publikowanie tooAzure witryn sieci Web przy użyciu narzędzia Git</span><span class="sxs-lookup"><span data-stu-id="4a945-155">Developing and publishing tooAzure Websites using Git</span></span>

<span data-ttu-id="4a945-156">pierwszy scenariusz Hello umożliwia tooauthor sformatowanego sieci web aplikacji, które zalet hello Azure PaaS funkcji takich jak [magazynu obiektów blob](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [kolejki magazynu](storage/queues/storage-python-how-to-use-queue-storage.md), [tabeli magazynu](cosmos-db/table-storage-how-to-use-python.md) itp. przy użyciu otoki Pythonic hello interfejsów API REST usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="4a945-156">hello first scenario enables you tooauthor rich web apps that take advantage of hello Azure PaaS capabilities such as [blob storage](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [queue storage](storage/queues/storage-python-how-to-use-queue-storage.md), [table storage](cosmos-db/table-storage-how-to-use-python.md) etc. via Pythonic wrappers for hello Azure REST APIs.</span></span> <span data-ttu-id="4a945-157">Te działają tak samo w systemie Windows, Mac i Linux.</span><span class="sxs-lookup"><span data-stu-id="4a945-157">These work identically on Windows, Mac, and Linux.</span></span>  <span data-ttu-id="4a945-158">Te biblioteki klienta można używać z komputera lokalnego rozwoju lub maszyny Wirtualnej systemu Linux działających na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="4a945-158">You can also use these client libraries from your local development machine or a Linux VM running on Azure.</span></span>

<span data-ttu-id="4a945-159">W scenariuszu maszyna wirtualna hello wystarczy uruchomić maszyny Wirtualnej systemu Linux wybranych przez użytkownika (Ubuntu, CentOS, Suse) i uruchom lub zarządzać co Ci się podoba.</span><span class="sxs-lookup"><span data-stu-id="4a945-159">For hello VM scenario, you simply start a Linux VM of your choice (Ubuntu, CentOS, Suse) and run/manage what you like.</span></span>  <span data-ttu-id="4a945-160">Na przykład można uruchomić [IPython] [ IPython] REPL/Notes na komputerze z systemem Windows lub Mac/Linux i punktu z przeglądarki tooa Linux lub uruchomiona maszyna wirtualna wiele procesów systemu Windows hello aparat IPython na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="4a945-160">As an example, you can run [IPython][IPython] REPL/notebook on your Windows/Mac/Linux machine and point your browser tooa Linux or Windows multi-proc VM running hello IPython Engine on Azure.</span></span>

<span data-ttu-id="4a945-161">Aby uzyskać informacje na temat tooset w górę Maszynę wirtualną systemu Linux, zobacz hello [tworzenia maszyny wirtualnej systemem Linux](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) samouczka.</span><span class="sxs-lookup"><span data-stu-id="4a945-161">For information on how tooset up a Linux VM, see hello [Create a Virtual Machine Running Linux](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tutorial.</span></span>

<span data-ttu-id="4a945-162">Za pomocą narzędzia Git, mogą tworzyć aplikacji sieci web języka Python i opublikować go tooan witryny sieci Web Azure z dowolnego systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="4a945-162">Using Git deployment, you can develop a Python web application and publish it tooan Azure Website from any operating system.</span></span>  <span data-ttu-id="4a945-163">Po naciśnięciu tooAzure Twojego repozytorium, automatycznie tworzy środowisko wirtualne i pip instaluje wymagane pakiety.</span><span class="sxs-lookup"><span data-stu-id="4a945-163">When you push your repository tooAzure, it automatically creates a virtual environment and pip installs your required packages.</span></span>

<span data-ttu-id="4a945-164">Aby uzyskać więcej informacji o tworzeniu i publikowanie witryn sieci Web Azure, zobacz samouczki hello [tworzenia witryn sieci Web przy użyciu platformy Django](app-service-web/web-sites-python-create-deploy-django-app.md), [tworzenia witryn sieci Web z Bottle](app-service-web/web-sites-python-create-deploy-bottle-app.md), i [tworzenia witryn sieci Web z Flask](app-service-web/web-sites-python-create-deploy-flask-app.md).</span><span class="sxs-lookup"><span data-stu-id="4a945-164">For more information on developing and publishing Azure Websites, see hello tutorials for [Creating Websites with Django](app-service-web/web-sites-python-create-deploy-django-app.md), [Creating Websites with Bottle](app-service-web/web-sites-python-create-deploy-bottle-app.md), and [Creating Websites with Flask](app-service-web/web-sites-python-create-deploy-flask-app.md).</span></span> <span data-ttu-id="4a945-165">Więcej ogólnych informacji przy użyciu dowolnej zgodne WSGI architektury, zobacz [Konfigurowanie Python z witryny sieci Web Azure](app-service-web/web-sites-python-configure.md).</span><span class="sxs-lookup"><span data-stu-id="4a945-165">For more general information on using any WSGI-compliant framework, see [Configuring Python with Azure Websites](app-service-web/web-sites-python-configure.md).</span></span>

## <a name="additional-software-and-resources"></a><span data-ttu-id="4a945-166">Dodatkowe oprogramowanie i zasoby:</span><span class="sxs-lookup"><span data-stu-id="4a945-166">Additional Software and Resources:</span></span>
* [<span data-ttu-id="4a945-167">Zestaw Azure SDK dla języka Python ReadTheDocs</span><span class="sxs-lookup"><span data-stu-id="4a945-167">Azure SDK for Python ReadTheDocs</span></span>](http://azure-sdk-for-python.readthedocs.io/en/latest/)
* [<span data-ttu-id="4a945-168">Zestaw Azure SDK dla języka Python GitHub</span><span class="sxs-lookup"><span data-stu-id="4a945-168">Azure SDK for Python GitHub</span></span>](https://github.com/Azure/azure-sdk-for-python)
* [<span data-ttu-id="4a945-169">Oficjalna przykładów dla platformy Azure dla języka Python</span><span class="sxs-lookup"><span data-stu-id="4a945-169">Official Azure samples for Python</span></span>](https://azure.microsoft.com/documentation/samples/?platform=python)
* <span data-ttu-id="4a945-170">[Kontynuacja Analytics Python dystrybucji][Continuum Analytics Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="4a945-170">[Continuum Analytics Python Distribution][Continuum Analytics Python Distribution]</span></span>
* <span data-ttu-id="4a945-171">[Dystrybucję oprogramowania Python Enthought][Enthought Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="4a945-171">[Enthought Python Distribution][Enthought Python Distribution]</span></span>
* <span data-ttu-id="4a945-172">[Dystrybucję oprogramowania Python ActiveState][ActiveState Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="4a945-172">[ActiveState Python Distribution][ActiveState Python Distribution]</span></span>
* <span data-ttu-id="4a945-173">[SciPy — pakiet bibliotek naukowych Python][SciPy - A suite of Scientific Python libraries]</span><span class="sxs-lookup"><span data-stu-id="4a945-173">[SciPy - A suite of Scientific Python libraries][SciPy - A suite of Scientific Python libraries]</span></span>
* <span data-ttu-id="4a945-174">[NumPy — Biblioteka numeryczne dla języka Python][NumPy - A numerics library for Python]</span><span class="sxs-lookup"><span data-stu-id="4a945-174">[NumPy - A numerics library for Python][NumPy - A numerics library for Python]</span></span>
* <span data-ttu-id="4a945-175">[Projekt Django — framework/system CMS dojrzałe sieci web][Django Project - A mature web framework/CMS]</span><span class="sxs-lookup"><span data-stu-id="4a945-175">[Django Project - A mature web framework/CMS][Django Project - A mature web framework/CMS]</span></span>
* <span data-ttu-id="4a945-176">[IPython — zaawansowane REPL/Notes, dla języka Python][IPython - an advanced REPL/Notebook for Python]</span><span class="sxs-lookup"><span data-stu-id="4a945-176">[IPython - an advanced REPL/Notebook for Python][IPython - an advanced REPL/Notebook for Python]</span></span>
* <span data-ttu-id="4a945-177">[Python Tools for Visual Studio w witrynie GitHub][Python Tools for Visual Studio on GitHub]</span><span class="sxs-lookup"><span data-stu-id="4a945-177">[Python Tools for Visual Studio on GitHub][Python Tools for Visual Studio on GitHub]</span></span>
* [<span data-ttu-id="4a945-178">Centrum deweloperów języka Python</span><span class="sxs-lookup"><span data-stu-id="4a945-178">Python Developer Center</span></span>](/develop/python/)

[Continuum Analytics Python Distribution]: http://continuum.io
[Enthought Python Distribution]: http://www.enthought.com
[ActiveState Python Distribution]: http://www.activestate.com
[www.python.org]: http://www.python.org
[www.continuum.io]: http://continuum.io
[www.enthought.com]: http://www.enthought.com
[www.activestate.com]: http://www.activestate.com
[SciPy - A suite of Scientific Python libraries]: http://www.scipy.org
[NumPy - A numerics library for Python]: http://www.numpy.org
[Django Project - A mature web framework/CMS]: http://www.djangoproject.com
[IPython - an advanced REPL/Notebook for Python]: http://ipython.org
[IPython]: http://ipython.org
[IPython Notebook on Azure]: virtual-machines-linux-jupyter-notebook.md
[Cloud Services]: cloud-services-python-ptvs.md
[Websites]: web-sites-python-ptvs-django-mysql.md
[narzędzi Python Tools for Visual Studio]: http://aka.ms/ptvs
[Python Tools for Visual Studio on GitHub]: https://github.com/microsoft/ptvs
[Python Package Index]: http://pypi.python.org/pypi
[Microsoft Azure SDK for Python 2.7]: http://go.microsoft.com/fwlink/?LinkId=254281
[Microsoft Azure SDK for Python 3.4]: http://go.microsoft.com/fwlink/?LinkID=516990
[Setting up a Linux VM via hello Azure portal]: create-and-configure-opensuse-vm-in-portal.md
[How toouse hello Azure Command-Line Interface]: crossplat-cmd-tools.md
[Create a Virtual Machine Running Linux]: virtual-machines-linux-quick-create-cli.md
[Creating Websites with Django]: web-sites-python-create-deploy-django-app.md
[Creating Websites with Bottle]: web-sites-python-create-deploy-bottle-app.md
[Creating Websites with Flask]: web-sites-python-create-deploy-flask-app.md
[Configuring Python with Azure Websites]: web-sites-python-configure.md
[table storage]: storage-python-how-to-use-table-storage.md
[queue storage]: storage-python-how-to-use-queue-storage.md
[blob storage]:storage/blobs/storage-python-how-to-use-blob-storage.md
