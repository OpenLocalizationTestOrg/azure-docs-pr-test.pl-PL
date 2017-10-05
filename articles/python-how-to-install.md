---
title: "Instalowanie języka Python i zestawu SDK - Azure"
description: "Dowiedz się, jak zainstalować Python i zestawu SDK do korzystania z usługi Azure."
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
ms.openlocfilehash: c9df4e1f7677b2ed10684f6f3c981f2abf64f171
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="installing-python-and-the-sdk"></a><span data-ttu-id="f82c6-103">Instalowanie języka Python i zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="f82c6-103">Installing Python and the SDK</span></span>
<span data-ttu-id="f82c6-104">Python jest łatwo skonfigurować w systemie Windows i jest wstępnie zainstalowane dla komputerów Mac, Linux, a [Bash dla systemu Windows](https://msdn.microsoft.com/commandline/wsl/about).</span><span class="sxs-lookup"><span data-stu-id="f82c6-104">Python is easy to set up on Windows and comes pre-installed on Mac, Linux, and [Bash for Windows](https://msdn.microsoft.com/commandline/wsl/about).</span></span> <span data-ttu-id="f82c6-105">Ten przewodnik przeprowadzi Cię przez instalacji i uzyskiwanie komputerze rozpocząć korzystanie z platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f82c6-105">This guide walks you through installation and getting your machine ready for use with Azure.</span></span>

## <a name="whats-in-the-python-azure-sdk"></a><span data-ttu-id="f82c6-106">Co to jest w języku Python SDK platformy Azure?</span><span class="sxs-lookup"><span data-stu-id="f82c6-106">What's in the Python Azure SDK?</span></span>
<span data-ttu-id="f82c6-107">Zestaw Azure SDK for Python zawiera składniki, które umożliwiają tworzenie, wdrażanie i zarządzanie aplikacjami języka Python dla platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f82c6-107">The Azure SDK for Python includes components that allow you to develop, deploy, and manage Python applications for Azure.</span></span> <span data-ttu-id="f82c6-108">W szczególności zestaw Azure SDK for Python obejmuje następujące funkcje:</span><span class="sxs-lookup"><span data-stu-id="f82c6-108">Specifically, the Azure SDK for Python includes the following:</span></span>

* <span data-ttu-id="f82c6-109">**Biblioteki zarządzania**.</span><span class="sxs-lookup"><span data-stu-id="f82c6-109">**Management libraries**.</span></span> <span data-ttu-id="f82c6-110">Te biblioteki klas udostępniają interfejs zarządzania zasobami platformy Azure, takich jak konta magazynu, maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="f82c6-110">These class libraries provide an interface managing Azure resources, such as storage accounts, virtual machines.</span></span>
* <span data-ttu-id="f82c6-111">**Biblioteki wykonawcze**.</span><span class="sxs-lookup"><span data-stu-id="f82c6-111">**Runtime libraries**.</span></span> <span data-ttu-id="f82c6-112">Te biblioteki klas zapewniają interfejs do uzyskiwania dostępu do funkcji platformy Azure, takich jak magazyn i usługi magistrali.</span><span class="sxs-lookup"><span data-stu-id="f82c6-112">These class libraries provide an interface for accessing Azure features, such as storage and service bus.</span></span>

## <a name="which-python-and-which-version-to-use"></a><span data-ttu-id="f82c6-113">Które Python i wersji do użycia</span><span class="sxs-lookup"><span data-stu-id="f82c6-113">Which Python and which version to use</span></span>
<span data-ttu-id="f82c6-114">Istnieje kilka odmian Python tłumaczy — przykłady to między innymi:</span><span class="sxs-lookup"><span data-stu-id="f82c6-114">There are several flavors of Python interpreters available - examples include:</span></span>

* <span data-ttu-id="f82c6-115">Języka CPython - standard i najczęściej używane interpreter języka Python</span><span class="sxs-lookup"><span data-stu-id="f82c6-115">CPython - the standard and most commonly used Python interpreter</span></span>
* <span data-ttu-id="f82c6-116">PyPy — szybkie, zgodne alternatywnej implementacji języka CPython</span><span class="sxs-lookup"><span data-stu-id="f82c6-116">PyPy - fast, compliant alternative implementation to CPython</span></span>
* <span data-ttu-id="f82c6-117">IronPython - interpreter języka Python, uruchamianego na .net/CLR</span><span class="sxs-lookup"><span data-stu-id="f82c6-117">IronPython - Python interpreter that runs on .Net/CLR</span></span>
* <span data-ttu-id="f82c6-118">Jython - interpreter języka Python, który działa na maszynie wirtualnej Java</span><span class="sxs-lookup"><span data-stu-id="f82c6-118">Jython - Python interpreter that runs on the Java Virtual Machine</span></span>

<span data-ttu-id="f82c6-119">**Języka CPython** v2.7 lub v3.3 + PyPy 5.4.0 przetestowane i obsługiwane w przypadku zestawu Azure SDK dla języka Python.</span><span class="sxs-lookup"><span data-stu-id="f82c6-119">**CPython** v2.7 or v3.3+ and PyPy 5.4.0 are tested and supported for the Python Azure SDK.</span></span>

## <a name="where-to-get-python"></a><span data-ttu-id="f82c6-120">Skąd uzyskać Python?</span><span class="sxs-lookup"><span data-stu-id="f82c6-120">Where to get Python?</span></span>
<span data-ttu-id="f82c6-121">Istnieje kilka sposobów, aby uzyskać języka CPython:</span><span class="sxs-lookup"><span data-stu-id="f82c6-121">There are several ways to get CPython:</span></span>

* <span data-ttu-id="f82c6-122">Bezpośrednio z [www.python.org][www.python.org]</span><span class="sxs-lookup"><span data-stu-id="f82c6-122">Directly from [www.python.org][www.python.org]</span></span>
* <span data-ttu-id="f82c6-123">Z zaufanych distro, takich jak [www.continuum.io][www.continuum.io], [www.enthought.com] [ www.enthought.com] lub [www.activestate.com][www.activestate.com]</span><span class="sxs-lookup"><span data-stu-id="f82c6-123">From a reputable distro such as [www.continuum.io][www.continuum.io], [www.enthought.com][www.enthought.com] or [www.activestate.com][www.activestate.com]</span></span>
* <span data-ttu-id="f82c6-124">Tworzenie źródła!</span><span class="sxs-lookup"><span data-stu-id="f82c6-124">Build from source!</span></span>

<span data-ttu-id="f82c6-125">W przypadku braku konkretna potrzeba użycia firma Microsoft zaleca dwóch pierwszych opcji.</span><span class="sxs-lookup"><span data-stu-id="f82c6-125">Unless you have a specific need, we recommend the first two options.</span></span>

## <a name="sdk-installation-on-windows-linux-and-macos-client-libraries-only"></a><span data-ttu-id="f82c6-126">Instalacja zestawu SDK systemu Windows, Linux i MacOS (tylko w przypadku bibliotek klienta)</span><span class="sxs-lookup"><span data-stu-id="f82c6-126">SDK Installation on Windows, Linux, and MacOS (client libraries only)</span></span>
<span data-ttu-id="f82c6-127">Jeśli masz już zainstalowany języka Python, należy zainstalować pakiet biblioteki klienta w istniejących Python 2.7 lub środowiska Python 3.3 + przez osoby pip.</span><span class="sxs-lookup"><span data-stu-id="f82c6-127">If you already have Python installed, you can use pip to install a bundle of all the client libraries in your existing Python 2.7 or Python 3.3+ environment.</span></span> <span data-ttu-id="f82c6-128">Spowoduje to pobranie pakietów z [indeksu pakietów języka Python] [ Python Package Index] (PyPI).</span><span class="sxs-lookup"><span data-stu-id="f82c6-128">This downloads the packages from the [Python Package Index][Python Package Index] (PyPI).</span></span>

<span data-ttu-id="f82c6-129">Prawa administratora może być konieczne:</span><span class="sxs-lookup"><span data-stu-id="f82c6-129">You may need administrator rights:</span></span>

* <span data-ttu-id="f82c6-130">Linux i MacOS, użyj `sudo` polecenia: `sudo pip install azure-mgmt-compute`.</span><span class="sxs-lookup"><span data-stu-id="f82c6-130">Linux and MacOS, use the `sudo` command: `sudo pip install azure-mgmt-compute`.</span></span>
* <span data-ttu-id="f82c6-131">System Windows: Otwórz z wiersza polecenia/programu PowerShell jako administrator</span><span class="sxs-lookup"><span data-stu-id="f82c6-131">Windows: open your PowerShell/Command prompt as an administrator</span></span>

<span data-ttu-id="f82c6-132">Można zainstalować oddzielnie każdej biblioteki dla poszczególnych usług Azure:</span><span class="sxs-lookup"><span data-stu-id="f82c6-132">You can install individually each library for each Azure service:</span></span>

```console
   $ pip install azure-batch          # Install the latest Batch runtime library
   $ pip install azure-mgmt-scheduler # Install the latest Storage management library
```

<span data-ttu-id="f82c6-133">Pakiety w wersji zapoznawczej mogą być instalowane za pomocą `--pre` flagi:</span><span class="sxs-lookup"><span data-stu-id="f82c6-133">Preview packages can be installed using the `--pre` flag:</span></span>

```console
   $ pip install --pre azure-mgmt-compute # installs only the latest Compute Management library
```

<span data-ttu-id="f82c6-134">Można także zainstalować zestaw Azure bibliotek w jednym wierszu przy użyciu `azure` meta-package.</span><span class="sxs-lookup"><span data-stu-id="f82c6-134">You can also install a set of Azure libraries in a single line using the `azure` meta-package.</span></span> <span data-ttu-id="f82c6-135">Ponieważ nie wszystkie pakiety w tym pakiecie meta są publikowane jako stabilny jeszcze `azure` meta pakiet jest dostępny w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="f82c6-135">Since not all packages in this meta-package are published as stable yet, the `azure` meta-package is still in preview.</span></span>
<span data-ttu-id="f82c6-136">Jednak pakietami podstawowymi, z perspektywy jakości/kompletności kodu jest uznawana za "stabilna" w tym momencie</span><span class="sxs-lookup"><span data-stu-id="f82c6-136">However, the core packages, from code quality/completeness perspectives can be considered "stable" at this time</span></span>

* <span data-ttu-id="f82c6-137">jego jest oficjalnie oznaczony jako takie w synchronizacji z innymi językami tak szybko, jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="f82c6-137">it is officially labeled as such in sync with other languages as soon as possible.</span></span>
  <span data-ttu-id="f82c6-138">Firma Microsoft nie zaplanowano wszelkie dodatkowe istotne zmiany do tego czasu.</span><span class="sxs-lookup"><span data-stu-id="f82c6-138">We are not planning on any further major changes until then.</span></span>

<span data-ttu-id="f82c6-139">Ponieważ chodzi o wersji zapoznawczej, należy użyć `--pre` flagi:</span><span class="sxs-lookup"><span data-stu-id="f82c6-139">Since it's a preview release, you need to use the `--pre` flag:</span></span>

```console
   $ pip install --pre azure
```

<span data-ttu-id="f82c6-140">lub bezpośrednio</span><span class="sxs-lookup"><span data-stu-id="f82c6-140">or directly</span></span>

```console
   $ pip install azure==2.0.0rc6
```

## <a name="getting-more-packages"></a><span data-ttu-id="f82c6-141">Pobieranie kolejne pakiety</span><span class="sxs-lookup"><span data-stu-id="f82c6-141">Getting More Packages</span></span>
<span data-ttu-id="f82c6-142">[Indeksu pakietów języka Python] [ Python Package Index] (PyPI) zawiera bogaty wybór bibliotek języka Python.</span><span class="sxs-lookup"><span data-stu-id="f82c6-142">The [Python Package Index][Python Package Index] (PyPI) has a rich selection of Python libraries.</span></span>  <span data-ttu-id="f82c6-143">Jeśli wybrano opcję zainstalowania Distro, konieczne będzie już najbardziej interesujące usługi bits dla różnych scenariuszy z projektowanie witryn sieci web do przetwarzania danych technicznych.</span><span class="sxs-lookup"><span data-stu-id="f82c6-143">If you chose to install a Distro, you'll already have most of the interesting bits for various scenarios from web development to Technical Computing.</span></span>

## <a name="python-tools-for-visual-studio"></a><span data-ttu-id="f82c6-144">Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f82c6-144">Python Tools for Visual Studio</span></span>
<span data-ttu-id="f82c6-145">[Narzędzia Python Tools for Visual Studio][narzędzi Python Tools for Visual Studio] (PTVS) jest wolny OSS dodatku firmy Microsoft, która zmieni się VS w pełni funkcjonalnymi IDE języka Python:</span><span class="sxs-lookup"><span data-stu-id="f82c6-145">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) is a free/OSS plugin from Microsoft, which turns VS into a full-fledged Python IDE:</span></span>

![How-do-install-python-ptvs](./media/python-how-to-install/how-to-install-python-ptvs.png)

<span data-ttu-id="f82c6-147">Przy użyciu narzędzi PTVS jest opcjonalne, ale jest zalecane, ponieważ umożliwia obsługę języka Python i rozwiązanie projektu sieci Web, debugowanie, profilowanie, okna interaktywnego, edytowanie szablonu i Intellisense.</span><span class="sxs-lookup"><span data-stu-id="f82c6-147">Using PTVS is optional, but is recommended as it gives you Python and Web Project/Solution support, debugging, profiling, interactive window, Template editing, and Intellisense.</span></span>

<span data-ttu-id="f82c6-148">PTVS również ułatwia wdrażanie do systemu Microsoft Azure z obsługą wdrażania na [usługi w chmurze](cloud-services/cloud-services-python-ptvs.md) i [witryn sieci Web](app-service-web/web-sites-python-ptvs-django-mysql.md).</span><span class="sxs-lookup"><span data-stu-id="f82c6-148">PTVS also makes it easy to deploy to Microsoft Azure, with support for deployment to [Cloud Services](cloud-services/cloud-services-python-ptvs.md) and [Websites](app-service-web/web-sites-python-ptvs-django-mysql.md).</span></span>

<span data-ttu-id="f82c6-149">PTVS współpracuje z istniejącej instalacji programu Visual Studio 2013, 2015 lub 2017 r.</span><span class="sxs-lookup"><span data-stu-id="f82c6-149">PTVS works with your existing Visual Studio 2013, 2015, or 2017 installation.</span></span>  <span data-ttu-id="f82c6-150">Dokumentacja, pliki do pobrania i dyskusji dla [narzędzi Python Tools for Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="f82c6-150">For documentation, downloads and discussions, see [Python Tools for Visual Studio].</span></span>  

## <a name="python-azure-scenarios-for-linux-and-macos"></a><span data-ttu-id="f82c6-151">Python scenariuszy Azure dla systemów Linux i MacOS</span><span class="sxs-lookup"><span data-stu-id="f82c6-151">Python Azure Scenarios for Linux and MacOS</span></span>
<span data-ttu-id="f82c6-152">Dla systemu Linux lub MacOS, główne Azure scenariusze, które są obsługiwane:</span><span class="sxs-lookup"><span data-stu-id="f82c6-152">For Linux or MacOS, main Azure scenarios that are supported:</span></span>

1. <span data-ttu-id="f82c6-153">Korzystanie z usług Azure za pomocą biblioteki klienta dla języka Python</span><span class="sxs-lookup"><span data-stu-id="f82c6-153">Consuming Azure Services by using the client libraries for Python</span></span>
2. <span data-ttu-id="f82c6-154">Uruchamianie aplikacji w Maszynę wirtualną systemu Linux</span><span class="sxs-lookup"><span data-stu-id="f82c6-154">Running your app in a Linux VM</span></span>
3. <span data-ttu-id="f82c6-155">Tworzenie i publikowanie witryn sieci Web platformy Azure przy użyciu narzędzia Git</span><span class="sxs-lookup"><span data-stu-id="f82c6-155">Developing and publishing to Azure Websites using Git</span></span>

<span data-ttu-id="f82c6-156">Pierwszy scenariusz umożliwia tworzenie aplikacji sieci web sformatowanego, które korzystają z możliwości Azure PaaS takich jak [magazynu obiektów blob](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [kolejki magazynu](storage/queues/storage-python-how-to-use-queue-storage.md), [tabeli magazynu](cosmos-db/table-storage-how-to-use-python.md) itp., za pomocą Pythonic otoki dla interfejsów API REST usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="f82c6-156">The first scenario enables you to author rich web apps that take advantage of the Azure PaaS capabilities such as [blob storage](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [queue storage](storage/queues/storage-python-how-to-use-queue-storage.md), [table storage](cosmos-db/table-storage-how-to-use-python.md) etc. via Pythonic wrappers for the Azure REST APIs.</span></span> <span data-ttu-id="f82c6-157">Te działają tak samo w systemie Windows, Mac i Linux.</span><span class="sxs-lookup"><span data-stu-id="f82c6-157">These work identically on Windows, Mac, and Linux.</span></span>  <span data-ttu-id="f82c6-158">Te biblioteki klienta można używać z komputera lokalnego rozwoju lub maszyny Wirtualnej systemu Linux działających na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="f82c6-158">You can also use these client libraries from your local development machine or a Linux VM running on Azure.</span></span>

<span data-ttu-id="f82c6-159">W scenariuszu maszyny Wirtualnej wystarczy uruchomić maszyny Wirtualnej systemu Linux wybranych przez użytkownika (Ubuntu, CentOS, Suse) i uruchom lub zarządzać co Ci się podoba.</span><span class="sxs-lookup"><span data-stu-id="f82c6-159">For the VM scenario, you simply start a Linux VM of your choice (Ubuntu, CentOS, Suse) and run/manage what you like.</span></span>  <span data-ttu-id="f82c6-160">Na przykład można uruchomić [IPython] [ IPython] REPL/Notes w z systemem Windows lub Mac/Linux komputera, a następnie wskaż przeglądarkę Linux lub maszyny Wirtualnej wiele procesów systemu Windows uruchomiony aparat IPython na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="f82c6-160">As an example, you can run [IPython][IPython] REPL/notebook on your Windows/Mac/Linux machine and point your browser to a Linux or Windows multi-proc VM running the IPython Engine on Azure.</span></span>

<span data-ttu-id="f82c6-161">Aby uzyskać informacje na temat sposobu konfigurowania maszyny Wirtualnej systemu Linux, zobacz [tworzenia maszyny wirtualnej systemem Linux](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) samouczka.</span><span class="sxs-lookup"><span data-stu-id="f82c6-161">For information on how to set up a Linux VM, see the [Create a Virtual Machine Running Linux](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tutorial.</span></span>

<span data-ttu-id="f82c6-162">Za pomocą narzędzia Git, mogą tworzyć aplikacji sieci web języka Python i opublikować go do witryny sieci Web platformy Azure z dowolnego systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="f82c6-162">Using Git deployment, you can develop a Python web application and publish it to an Azure Website from any operating system.</span></span>  <span data-ttu-id="f82c6-163">Po naciśnięciu repozytorium Azure automatycznie tworzy środowisko wirtualne i pip instaluje wymagane pakiety.</span><span class="sxs-lookup"><span data-stu-id="f82c6-163">When you push your repository to Azure, it automatically creates a virtual environment and pip installs your required packages.</span></span>

<span data-ttu-id="f82c6-164">Aby uzyskać więcej informacji o tworzeniu i publikowanie witryn sieci Web Azure, zobacz samouczki dotyczące [tworzenia witryn sieci Web przy użyciu platformy Django](app-service-web/web-sites-python-create-deploy-django-app.md), [tworzenia witryn sieci Web z Bottle](app-service-web/web-sites-python-create-deploy-bottle-app.md), i [tworzenia witryn sieci Web z Flask](app-service-web/web-sites-python-create-deploy-flask-app.md).</span><span class="sxs-lookup"><span data-stu-id="f82c6-164">For more information on developing and publishing Azure Websites, see the tutorials for [Creating Websites with Django](app-service-web/web-sites-python-create-deploy-django-app.md), [Creating Websites with Bottle](app-service-web/web-sites-python-create-deploy-bottle-app.md), and [Creating Websites with Flask](app-service-web/web-sites-python-create-deploy-flask-app.md).</span></span> <span data-ttu-id="f82c6-165">Więcej ogólnych informacji przy użyciu dowolnej zgodne WSGI architektury, zobacz [Konfigurowanie Python z witryny sieci Web Azure](app-service-web/web-sites-python-configure.md).</span><span class="sxs-lookup"><span data-stu-id="f82c6-165">For more general information on using any WSGI-compliant framework, see [Configuring Python with Azure Websites](app-service-web/web-sites-python-configure.md).</span></span>

## <a name="additional-software-and-resources"></a><span data-ttu-id="f82c6-166">Dodatkowe oprogramowanie i zasoby:</span><span class="sxs-lookup"><span data-stu-id="f82c6-166">Additional Software and Resources:</span></span>
* [<span data-ttu-id="f82c6-167">Zestaw Azure SDK dla języka Python ReadTheDocs</span><span class="sxs-lookup"><span data-stu-id="f82c6-167">Azure SDK for Python ReadTheDocs</span></span>](http://azure-sdk-for-python.readthedocs.io/en/latest/)
* [<span data-ttu-id="f82c6-168">Zestaw Azure SDK dla języka Python GitHub</span><span class="sxs-lookup"><span data-stu-id="f82c6-168">Azure SDK for Python GitHub</span></span>](https://github.com/Azure/azure-sdk-for-python)
* [<span data-ttu-id="f82c6-169">Oficjalna przykładów dla platformy Azure dla języka Python</span><span class="sxs-lookup"><span data-stu-id="f82c6-169">Official Azure samples for Python</span></span>](https://azure.microsoft.com/documentation/samples/?platform=python)
* <span data-ttu-id="f82c6-170">[Kontynuacja Analytics Python dystrybucji][Continuum Analytics Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="f82c6-170">[Continuum Analytics Python Distribution][Continuum Analytics Python Distribution]</span></span>
* <span data-ttu-id="f82c6-171">[Dystrybucję oprogramowania Python Enthought][Enthought Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="f82c6-171">[Enthought Python Distribution][Enthought Python Distribution]</span></span>
* <span data-ttu-id="f82c6-172">[Dystrybucję oprogramowania Python ActiveState][ActiveState Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="f82c6-172">[ActiveState Python Distribution][ActiveState Python Distribution]</span></span>
* <span data-ttu-id="f82c6-173">[SciPy — pakiet bibliotek naukowych Python][SciPy - A suite of Scientific Python libraries]</span><span class="sxs-lookup"><span data-stu-id="f82c6-173">[SciPy - A suite of Scientific Python libraries][SciPy - A suite of Scientific Python libraries]</span></span>
* <span data-ttu-id="f82c6-174">[NumPy — Biblioteka numeryczne dla języka Python][NumPy - A numerics library for Python]</span><span class="sxs-lookup"><span data-stu-id="f82c6-174">[NumPy - A numerics library for Python][NumPy - A numerics library for Python]</span></span>
* <span data-ttu-id="f82c6-175">[Projekt Django — framework/system CMS dojrzałe sieci web][Django Project - A mature web framework/CMS]</span><span class="sxs-lookup"><span data-stu-id="f82c6-175">[Django Project - A mature web framework/CMS][Django Project - A mature web framework/CMS]</span></span>
* <span data-ttu-id="f82c6-176">[IPython — zaawansowane REPL/Notes, dla języka Python][IPython - an advanced REPL/Notebook for Python]</span><span class="sxs-lookup"><span data-stu-id="f82c6-176">[IPython - an advanced REPL/Notebook for Python][IPython - an advanced REPL/Notebook for Python]</span></span>
* <span data-ttu-id="f82c6-177">[Python Tools for Visual Studio w witrynie GitHub][Python Tools for Visual Studio on GitHub]</span><span class="sxs-lookup"><span data-stu-id="f82c6-177">[Python Tools for Visual Studio on GitHub][Python Tools for Visual Studio on GitHub]</span></span>
* [<span data-ttu-id="f82c6-178">Centrum deweloperów języka Python</span><span class="sxs-lookup"><span data-stu-id="f82c6-178">Python Developer Center</span></span>](/develop/python/)

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
[Setting up a Linux VM via the Azure portal]: create-and-configure-opensuse-vm-in-portal.md
[How to use the Azure Command-Line Interface]: crossplat-cmd-tools.md
[Create a Virtual Machine Running Linux]: virtual-machines-linux-quick-create-cli.md
[Creating Websites with Django]: web-sites-python-create-deploy-django-app.md
[Creating Websites with Bottle]: web-sites-python-create-deploy-bottle-app.md
[Creating Websites with Flask]: web-sites-python-create-deploy-flask-app.md
[Configuring Python with Azure Websites]: web-sites-python-configure.md
[table storage]: storage-python-how-to-use-table-storage.md
[queue storage]: storage-python-how-to-use-queue-storage.md
[blob storage]:storage/blobs/storage-python-how-to-use-blob-storage.md
