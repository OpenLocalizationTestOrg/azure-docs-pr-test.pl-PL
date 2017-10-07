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
# <a name="installing-python-and-hello-sdk"></a>Instalowanie języka Python i hello zestawu SDK
Python jest łatwe tooset uruchomiony w systemie Windows i jest wstępnie zainstalowane dla komputerów Mac, Linux, a [Bash dla systemu Windows](https://msdn.microsoft.com/commandline/wsl/about). Ten przewodnik przeprowadzi Cię przez instalacji i uzyskiwanie komputerze rozpocząć korzystanie z platformy Azure.

## <a name="whats-in-hello-python-azure-sdk"></a>Co to jest odpowiednio w hello zestawu Azure SDK Python?
zestaw Azure SDK for Python Hello obejmuje składniki, które pozwalają toodevelop, wdrażanie i zarządzanie aplikacjami języka Python dla platformy Azure. W szczególności hello zestaw Azure SDK for Python zawiera następujące hello:

* **Biblioteki zarządzania**. Te biblioteki klas udostępniają interfejs zarządzania zasobami platformy Azure, takich jak konta magazynu, maszyn wirtualnych.
* **Biblioteki wykonawcze**. Te biblioteki klas zapewniają interfejs do uzyskiwania dostępu do funkcji platformy Azure, takich jak magazyn i usługi magistrali.

## <a name="which-python-and-which-version-toouse"></a>Które Python i które toouse wersji
Istnieje kilka odmian Python tłumaczy — przykłady to między innymi:

* Języka CPython - hello standard i najczęściej używane interpreter języka Python
* PyPy — szybkie, zgodne alternatywną implementację tooCPython
* IronPython - interpreter języka Python, uruchamianego na .net/CLR
* Jython - interpreter języka Python, uruchamianego na powitania maszyny wirtualnej Java

**Języka CPython** v2.7 lub v3.3 + PyPy 5.4.0 przetestowane i obsługiwane w przypadku hello zestawu Azure SDK Python.

## <a name="where-tooget-python"></a>Gdzie tooget Python?
Istnieje kilka sposobów tooget języka CPython:

* Bezpośrednio z [www.python.org][www.python.org]
* Z zaufanych distro, takich jak [www.continuum.io][www.continuum.io], [www.enthought.com] [ www.enthought.com] lub [www.activestate.com][www.activestate.com]
* Tworzenie źródła!

W przypadku braku konkretna potrzeba użycia zalecamy hello dwóch pierwszych opcji.

## <a name="sdk-installation-on-windows-linux-and-macos-client-libraries-only"></a>Instalacja zestawu SDK systemu Windows, Linux i MacOS (tylko w przypadku bibliotek klienta)
Jeśli masz już zainstalowany języka Python, można użyć narzędzia pip tooinstall pakiet wszystkich bibliotek klienckich hello w istniejących Python 2.7 lub środowiska Python 3.3 +. Spowoduje to pobranie pakietów hello z hello [indeksu pakietów języka Python] [ Python Package Index] (PyPI).

Prawa administratora może być konieczne:

* Linux i MacOS, użyj hello `sudo` polecenia: `sudo pip install azure-mgmt-compute`.
* System Windows: Otwórz z wiersza polecenia/programu PowerShell jako administrator

Można zainstalować oddzielnie każdej biblioteki dla poszczególnych usług Azure:

```console
   $ pip install azure-batch          # Install hello latest Batch runtime library
   $ pip install azure-mgmt-scheduler # Install hello latest Storage management library
```

Pakiety w wersji zapoznawczej mogą być instalowane za pomocą hello `--pre` flagi:

```console
   $ pip install --pre azure-mgmt-compute # installs only hello latest Compute Management library
```

Można także zainstalować zestaw Azure bibliotek w jednym wierszu przy użyciu hello `azure` meta-package. Ponieważ nie wszystkie pakiety w tym pakiecie meta są jeszcze opublikowane jako stabilny, hello `azure` meta pakiet jest dostępny w wersji zapoznawczej.
Jednak hello pakietami podstawowymi, z perspektywy jakości/kompletności kodu jest uznawana za "stabilna" w tym momencie

* jego jest oficjalnie oznaczony jako takie w synchronizacji z innymi językami tak szybko, jak to możliwe.
  Firma Microsoft nie zaplanowano wszelkie dodatkowe istotne zmiany do tego czasu.

Ponieważ chodzi o wersji zapoznawczej, należy toouse hello `--pre` flagi:

```console
   $ pip install --pre azure
```

lub bezpośrednio

```console
   $ pip install azure==2.0.0rc6
```

## <a name="getting-more-packages"></a>Pobieranie kolejne pakiety
Witaj [indeksu pakietów języka Python] [ Python Package Index] (PyPI) zawiera bogaty wybór bibliotek języka Python.  W przypadku wybrania tooinstall Distro będzie już większość hello interesujące usługi bits dla różnych scenariuszy z sieci web development tooTechnical środowisk obliczeniowych.

## <a name="python-tools-for-visual-studio"></a>Python Tools for Visual Studio
[Narzędzia Python Tools for Visual Studio][narzędzi Python Tools for Visual Studio] (PTVS) jest wolny OSS dodatku firmy Microsoft, która zmieni się VS w pełni funkcjonalnymi IDE języka Python:

![How-do-install-python-ptvs](./media/python-how-to-install/how-to-install-python-ptvs.png)

Przy użyciu narzędzi PTVS jest opcjonalne, ale jest zalecane, ponieważ umożliwia obsługę języka Python i rozwiązanie projektu sieci Web, debugowanie, profilowanie, okna interaktywnego, edytowanie szablonu i Intellisense.

PTVS ułatwia też łatwo toodeploy tooMicrosoft Azure, z obsługą wdrażania zbyt[usługi w chmurze](cloud-services/cloud-services-python-ptvs.md) i [witryn sieci Web](app-service-web/web-sites-python-ptvs-django-mysql.md).

PTVS współpracuje z istniejącej instalacji programu Visual Studio 2013, 2015 lub 2017 r.  Dokumentacja, pliki do pobrania i dyskusji dla [narzędzi Python Tools for Visual Studio].  

## <a name="python-azure-scenarios-for-linux-and-macos"></a>Python scenariuszy Azure dla systemów Linux i MacOS
Dla systemu Linux lub MacOS, główne Azure scenariusze, które są obsługiwane:

1. Korzystanie z usług Azure przy użyciu bibliotek klienckich powitania dla języka Python
2. Uruchamianie aplikacji w Maszynę wirtualną systemu Linux
3. Tworzenie i publikowanie tooAzure witryn sieci Web przy użyciu narzędzia Git

pierwszy scenariusz Hello umożliwia tooauthor sformatowanego sieci web aplikacji, które zalet hello Azure PaaS funkcji takich jak [magazynu obiektów blob](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [kolejki magazynu](storage/queues/storage-python-how-to-use-queue-storage.md), [tabeli magazynu](cosmos-db/table-storage-how-to-use-python.md) itp. przy użyciu otoki Pythonic hello interfejsów API REST usługi Azure. Te działają tak samo w systemie Windows, Mac i Linux.  Te biblioteki klienta można używać z komputera lokalnego rozwoju lub maszyny Wirtualnej systemu Linux działających na platformie Azure.

W scenariuszu maszyna wirtualna hello wystarczy uruchomić maszyny Wirtualnej systemu Linux wybranych przez użytkownika (Ubuntu, CentOS, Suse) i uruchom lub zarządzać co Ci się podoba.  Na przykład można uruchomić [IPython] [ IPython] REPL/Notes na komputerze z systemem Windows lub Mac/Linux i punktu z przeglądarki tooa Linux lub uruchomiona maszyna wirtualna wiele procesów systemu Windows hello aparat IPython na platformie Azure.

Aby uzyskać informacje na temat tooset w górę Maszynę wirtualną systemu Linux, zobacz hello [tworzenia maszyny wirtualnej systemem Linux](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) samouczka.

Za pomocą narzędzia Git, mogą tworzyć aplikacji sieci web języka Python i opublikować go tooan witryny sieci Web Azure z dowolnego systemu operacyjnego.  Po naciśnięciu tooAzure Twojego repozytorium, automatycznie tworzy środowisko wirtualne i pip instaluje wymagane pakiety.

Aby uzyskać więcej informacji o tworzeniu i publikowanie witryn sieci Web Azure, zobacz samouczki hello [tworzenia witryn sieci Web przy użyciu platformy Django](app-service-web/web-sites-python-create-deploy-django-app.md), [tworzenia witryn sieci Web z Bottle](app-service-web/web-sites-python-create-deploy-bottle-app.md), i [tworzenia witryn sieci Web z Flask](app-service-web/web-sites-python-create-deploy-flask-app.md). Więcej ogólnych informacji przy użyciu dowolnej zgodne WSGI architektury, zobacz [Konfigurowanie Python z witryny sieci Web Azure](app-service-web/web-sites-python-configure.md).

## <a name="additional-software-and-resources"></a>Dodatkowe oprogramowanie i zasoby:
* [Zestaw Azure SDK dla języka Python ReadTheDocs](http://azure-sdk-for-python.readthedocs.io/en/latest/)
* [Zestaw Azure SDK dla języka Python GitHub](https://github.com/Azure/azure-sdk-for-python)
* [Oficjalna przykładów dla platformy Azure dla języka Python](https://azure.microsoft.com/documentation/samples/?platform=python)
* [Kontynuacja Analytics Python dystrybucji][Continuum Analytics Python Distribution]
* [Dystrybucję oprogramowania Python Enthought][Enthought Python Distribution]
* [Dystrybucję oprogramowania Python ActiveState][ActiveState Python Distribution]
* [SciPy — pakiet bibliotek naukowych Python][SciPy - A suite of Scientific Python libraries]
* [NumPy — Biblioteka numeryczne dla języka Python][NumPy - A numerics library for Python]
* [Projekt Django — framework/system CMS dojrzałe sieci web][Django Project - A mature web framework/CMS]
* [IPython — zaawansowane REPL/Notes, dla języka Python][IPython - an advanced REPL/Notebook for Python]
* [Python Tools for Visual Studio w witrynie GitHub][Python Tools for Visual Studio on GitHub]
* [Centrum deweloperów języka Python](/develop/python/)

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
