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
# <a name="creating-web-apps-with-bottle-in-azure"></a>Tworzenie aplikacji sieci web w języku Bottle na platformie Azure
W tym samouczku opisano, jak tooget uruchomienia Python w aplikacjach sieci Web usługi aplikacji Azure. Usługa Web Apps zapewnia ograniczony bezpłatny hosting i szybkie wdrażanie, a także możliwość korzystania z języka Python. Rozwoju aplikacji, możesz przełączyć toopaid hosting lub można również zintegrować z wszystkimi hello innymi usługami Azure.

Utworzysz aplikację sieci web przy użyciu platformy sieci web Bottle hello (zobacz alternatywne wersje tego samouczka dla [Django](web-sites-python-create-deploy-django-app.md) i [Flask](web-sites-python-create-deploy-flask-app.md)). Zostanie tworzenie aplikacji sieci web hello z hello Azure Marketplace, skonfigurujesz wdrożenie systemu Git i klonowania repozytorium hello lokalnie. Następnie uruchomisz aplikację sieci web hello lokalnie, wprowadzić zmiany, zatwierdzenia i wypychanie ich zbyt[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714). Witaj samouczku przedstawiono sposób toodo od systemu Windows lub Mac/Linux.

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service. Bez kart kredytowych i bez zobowiązań.
> 
> 

## <a name="prerequisites"></a>Wymagania wstępne
* System Windows, Mac lub Linux
* Środowisko Python w wersji 2.7 lub 3.4
* Narzędzia setuptools pip, virtualenv (tylko środowisko Python 2.7)
* Usługa Git
* [Narzędzia Python Tools 2.2 for Visual Studio][Python Tools 2.2 for Visual Studio] (PTVS) — Uwaga: ten krok jest opcjonalny

**Uwaga**: publikowanie TFS nie jest obecnie obsługiwane dla projektów języka Python.

### <a name="windows"></a>Windows
Jeśli środowisko Python 2.7 lub 3.4 (32-bitowe) nie zostało jeszcze zainstalowane, zalecane jest zainstalowanie [Zestaw Azure SDK dla języka Python w wersji 2.7] lub [zestawu Azure SDK dla języka Python 3.4] przy użyciu Instalatora platformy sieci Web. Spowoduje to zainstalowanie hello 32-bitowej wersji języka Python, narzędzi setuptools, pip, virtualenv itp (32-bitowe środowisko Python jest zainstalowanych na maszynach hostów Azure hello). Możesz również pobrać środowisko Python z witryny [python.org].

W przypadku systemu Git zalecane jest narzędzie [Git dla systemu Windows] lub [Github dla systemu Windows]. Jeśli używasz programu Visual Studio, używając hello zintegrowanej obsługi systemu Git.

Zalecane jest również zainstalowanie narzędzi [Python Tools 2.2 for Visual Studio]. Ten krok jest opcjonalny, ale jeśli masz [programu Visual Studio], włączając hello wolne Visual Studio Community 2013 lub Visual Studio Express 2013 for Web, a następnie zapewni to doskonały IDE języka Python.

### <a name="maclinux"></a>System Mac/Linux
Środowisko Python i system Git powinny być już zainstalowane, ale upewnij się, że masz środowisko Python 2.7 lub 3.4.

## <a name="web-app-creation-on-hello-azure-portal"></a>Tworzenie aplikacji sieci Web na powitania portalu Azure
Witaj pierwszym krokiem tworzenia aplikacji jest toocreate hello aplikacja sieci web za pośrednictwem hello [Azure Portal](https://portal.azure.com).  

1. Zaloguj się do hello portalu Azure i kliknij przycisk hello **nowy** przycisku na powitania lewym dolnym rogu. 
2. W polu wyszukiwania hello wpisz "python".
3. W wynikach wyszukiwania hello, wybierz **Bottle**, następnie kliknij przycisk **Utwórz**.
4. Skonfiguruj hello nowej Bottle aplikacji, takich jak tworzenie nowego planu usługi App Service i nowej grupy zasobów dla niego. Następnie kliknij pozycję **Utwórz**.
5. Konfigurowanie publikowania Git dla aplikacji sieci web nowo utworzony wykonując instrukcje hello [tooAzure lokalnego wdrożenia Git usługi aplikacji](app-service-deploy-local-git.md).

## <a name="application-overview"></a>Omówienie aplikacji
### <a name="git-repository-contents"></a>Zawartość repozytorium Git
Poniżej przedstawiono omówienie hello plików, które znajdują się w początkowym repozytorium Git hello, które sklonujemy w następnej sekcji hello.

    \routes.py
    \static\content\
    \static\fonts\
    \static\scripts\
    \views\about.tpl
    \views\contact.tpl
    \views\index.tpl
    \views\layout.tpl

Główne źródła dla aplikacji hello. Składa się z 3 stron (indeks, informacje, kontakt) z układem głównym.  Zawartość statyczna i skrypty obejmują bootstrap, jquery, modernizr i respond.

    \app.py

Lokalne działania projektowe obsługi serwera. Za pomocą tej aplikacji hello toorun lokalnie.

    \BottleWebProject.pyproj
    \BottleWebProject.sln

Pliki projektu do użycia z narzędziami [Python Tools for Visual Studio].

    \ptvs_virtualenv_proxy.py

Serwer proxy usług IIS dla środowisk wirtualnych i obsługa zdalnego debugowania narzędzi PTVS.

    \requirements.txt

Pakiety zewnętrzne wymagane przez tę aplikację. skrypt wdrożenia Hello będzie narzędzia pip instalowanie pakietów hello wymienione w tym pliku.

    \web.2.7.config
    \web.3.4.config

Pliki konfiguracji programu IIS. skrypt wdrożenia Hello Użyj hello odpowiedniego pliku web.x.y.config i skopiuje go jako plik web.config.

### <a name="optional-files---customizing-deployment"></a>Pliki opcjonalne — dostosowywanie wdrożenia
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a>Pliki opcjonalne — środowisko uruchomieniowe języka Python
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a>Dodatkowe pliki na serwerze
Niektóre pliki na powitania serwera istnieje, ale nie są dodawane toohello repozytorium git. Są one tworzone przez skrypt wdrożenia hello.

    \web.config

Plik konfiguracji programu IIS. Tworzony na podstawie pliku web.x.y.config przy każdym wdrożeniu.

    \env\

Środowisko wirtualne języka Python. Utworzonych podczas wdrażania, jeśli zgodne środowisko wirtualne już nie istnieje na powitania aplikacji sieci web.  Pakiety wymienione w pliku requirements.txt są zainstalowane narzędzia pip, ale narzędzie pip pomija instalację, jeśli hello pakiety są już zainstalowane.

Witaj 3 następnych sekcjach opisano sposób tworzenia aplikacji w 3 różnych środowiskach sieci web na tooproceed z hello:

* System Windows — przy użyciu narzędzi Python Tools for Visual Studio
* System Windows — przy użyciu wiersza polecenia
* System Mac/Linux — przy użyciu wiersza polecenia

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a>Sieci Web - Windows - Python narzędzia do programowania aplikacji dla programu Visual Studio
### <a name="clone-hello-repository"></a>Klonowanie repozytorium hello
Najpierw sklonuj repozytorium hello przy użyciu adresu url hello na powitania portalu Azure. Aby uzyskać więcej informacji, zobacz [tooAzure lokalnego wdrożenia Git usługi aplikacji](app-service-deploy-local-git.md).

Otwórz plik rozwiązania hello (.sln), który znajduje się w katalogu głównego repozytorium hello hello.

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-solution-bottle.png)

### <a name="create-virtual-environment"></a>Tworzenie środowiska wirtualnego
Teraz utwórz środowisko wirtualne dla wdrożenia lokalnego. Kliknij prawym przyciskiem myszy pozycję **Środowiska Python** i wybierz pozycję **Dodaj środowisko wirtualne**.

* Upewnij się, że nazwa hello środowiska hello jest `env`.
* Wybierz interpreter podstawowy hello. Upewnij się, że toouse hello sama wersja środowiska Python, którą wybrano dla aplikacji sieci web (w pliku runtime.txt lub hello **ustawienia aplikacji** bloku aplikacji sieci web w portalu Azure hello).
* Upewnij się, zaznaczono opcję hello toodownload i zainstaluj pakiety.

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-add-virtual-env-27.png)

Kliknij przycisk **Utwórz**. Spowoduje to utworzenie środowiska wirtualnego hello i zainstalowanie składników zależnych wymienionych w pliku requirements.txt.

### <a name="run-using-development-server"></a>Uruchamianie przy użyciu serwera projektowego
Naciśnij klawisz F5 toostart debugowania i przeglądarki sieci web zostanie otwarty toohello strony uruchomionej lokalnie.

![](./media/web-sites-python-create-deploy-bottle-app/windows-browser-bottle.png)

Można ustawić punktów przerwania w hello źródeł, użyj hello czujki systemu windows itd. Zobacz hello [narzędzi Python Tools for Visual Studio dokumentacji] Aby uzyskać więcej informacji na temat hello różnych funkcji.

### <a name="make-changes"></a>Wprowadzanie zmian
Teraz możesz eksperymentować, wprowadzając zmiany toohello aplikacji źródeł i/lub szablonach.

Po przetestowaniu zmiany je zatwierdzić toohello repozytorium Git:

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-commit-bottle.png)

### <a name="install-more-packages"></a>Instalowanie dodatkowych pakietów
Aplikacja może mieć zależności poza środowiskiem Python i Bottle.

Możesz zainstalować dodatkowe pakiety przy użyciu narzędzia pip. tooinstall pakiet, kliknij prawym przyciskiem myszy na powitania środowisko wirtualne i wybierz **zainstaluj pakiet języka Python**.

Na przykład tooinstall hello Azure SDK dla języka Python, który zapewnia dostęp tooAzure magazynu, usługi service bus i innymi usługami Azure, wprowadź `azure`:

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-install-package-dialog.png)

Kliknij prawym przyciskiem myszy na powitania środowiska wirtualnego, a następnie wybierz **Generuj plik requirements.txt** tooupdate requirements.txt.

Następnie Zatwierdź repozytorium Git toohello toorequirements.txt zmiany hello.

### <a name="deploy-tooazure"></a>Wdrażanie tooAzure
polecenie tootrigger wdrożenia, **synchronizacji** lub **Push**. Synchronizacja obejmuje zarówno wypychanie, jak i ściąganie.

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-git-push.png)

pierwszym wdrożeniu Hello wymaga czasu, ponieważ obejmuje tworzenie środowiska wirtualnego, instalowanie pakietów itp.

Program Visual Studio nie wyświetla postęp hello hello wdrożenia. Jeśli chcesz tooreview hello w danych wyjściowych, zobacz sekcję hello na [Rozwiązywanie problemów — wdrożenie](#troubleshooting-deployment).

Przeglądaj zmiany toohello tooview adresu URL platformy Azure.

## <a name="web-app-development---windows---command-line"></a>Wiersz polecenia - Windows - tworzenie aplikacji sieci Web
### <a name="clone-hello-repository"></a>Klonowanie repozytorium hello
Najpierw sklonować repozytorium hello przy użyciu adresu URL hello na powitania portalu Azure i dodać hello repozytorium Azure jako zdalnej. Aby uzyskać więcej informacji, zobacz [tooAzure lokalnego wdrożenia Git usługi aplikacji](app-service-deploy-local-git.md).

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a>Tworzenie środowiska wirtualnego
Utworzymy nowe środowisko wirtualne dla celów programistycznych (nie należy dodawać go toohello repozytorium). Wirtualnych środowisk języka Python nie są można zmieniać lokalizacji, dlatego każdy Deweloper pracujący nad aplikacji hello tworzy własne środowisko lokalnie.

Upewnij się, że toouse hello sama wersja środowiska Python, którą wybrano dla aplikacji sieci web (w pliku runtime.txt lub hello bloku ustawienia aplikacji dla aplikacji sieci web w portalu Azure hello)

Dla środowiska Python w wersji 2.7:

    c:\python27\python.exe -m virtualenv env

Dla środowiska Python w wersji 3.4:

    c:\python34\python.exe -m venv env

Zainstaluj pakiety zewnętrzne wymagane przez aplikację. Możesz użyć pliku requirements.txt hello w głównym hello hello repozytorium tooinstall hello pakietów w środowisku wirtualnym:

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a>Uruchamianie przy użyciu serwera projektowego
Można uruchomić aplikacji hello na serwerze projektowym z hello następujące polecenie:

    env\scripts\python app.py

Witaj konsoli zostanie wyświetlony adres URL hello i nasłuchuje portu powitania serwera:

![](./media/web-sites-python-create-deploy-bottle-app/windows-run-local-bottle.png)

Następnie otwórz adres URL toothat przeglądarki sieci web.

![](./media/web-sites-python-create-deploy-bottle-app/windows-browser-bottle.png)

### <a name="make-changes"></a>Wprowadzanie zmian
Teraz możesz eksperymentować, wprowadzając zmiany toohello aplikacji źródeł i/lub szablonach.

Po przetestowaniu zmiany je zatwierdzić toohello repozytorium Git:

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a>Instalowanie dodatkowych pakietów
Aplikacja może mieć zależności poza środowiskiem Python i Bottle.

Możesz zainstalować dodatkowe pakiety przy użyciu narzędzia pip. Na przykład tooinstall hello Azure SDK dla języka Python, co pozwala na dostęp do magazynu tooAzure, magistrali usług i innych usług Azure, wpisz:

    env\scripts\pip install azure

Upewnij się, że tooupdate pliku requirements.txt:

    env\scripts\pip freeze > requirements.txt

Zatwierdź zmiany hello:

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a>Wdrażanie tooAzure
tootrigger wdrożenia hello wypychania zmiany tooAzure:

    git push azure master

Zostanie wyświetlone dane wyjściowe hello hello skryptu wdrożenia, łącznie z tworzeniem środowiska wirtualnego, instalowaniem pakietów i tworzeniem pliku web.config.

Przeglądaj zmiany toohello tooview adresu URL platformy Azure.

## <a name="web-app-development---maclinux---command-line"></a>Wdrażanie aplikacji sieci Web — system Mac/Linux — wiersz polecenia
### <a name="clone-hello-repository"></a>Klonowanie repozytorium hello
Najpierw sklonować repozytorium hello przy użyciu adresu URL hello na powitania portalu Azure i dodać hello repozytorium Azure jako zdalnej. Aby uzyskać więcej informacji, zobacz [tooAzure lokalnego wdrożenia Git usługi aplikacji](app-service-deploy-local-git.md).

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a>Tworzenie środowiska wirtualnego
Utworzymy nowe środowisko wirtualne dla celów programistycznych (nie należy dodawać go toohello repozytorium). Wirtualnych środowisk języka Python nie są można zmieniać lokalizacji, dlatego każdy Deweloper pracujący nad aplikacji hello tworzy własne środowisko lokalnie.

Upewnij się, toouse hello sama wersja środowiska Python, którą wybrano dla aplikacji sieci web (w pliku runtime.txt lub hello bloku ustawienia aplikacji aplikacji sieci web w portalu Azure hello).

Dla środowiska Python w wersji 2.7:

    python -m virtualenv env

Dla środowiska Python w wersji 3.4:

    python -m venv env
lub pyvenv env

Zainstaluj pakiety zewnętrzne wymagane przez aplikację. Możesz użyć pliku requirements.txt hello w głównym hello hello repozytorium tooinstall hello pakietów w środowisku wirtualnym:

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a>Uruchamianie przy użyciu serwera projektowego
Można uruchomić aplikacji hello na serwerze projektowym z hello następujące polecenie:

    env/bin/python app.py

Witaj konsoli zostanie wyświetlony adres URL hello i nasłuchuje portu powitania serwera:

![](./media/web-sites-python-create-deploy-bottle-app/mac-run-local-bottle.png)

Następnie otwórz adres URL toothat przeglądarki sieci web.

![](./media/web-sites-python-create-deploy-bottle-app/mac-browser-bottle.png)

### <a name="make-changes"></a>Wprowadzanie zmian
Teraz możesz eksperymentować, wprowadzając zmiany toohello aplikacji źródeł i/lub szablonach.

Po przetestowaniu zmiany je zatwierdzić toohello repozytorium Git:

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a>Instalowanie dodatkowych pakietów
Aplikacja może mieć zależności poza środowiskiem Python i Bottle.

Możesz zainstalować dodatkowe pakiety przy użyciu narzędzia pip. Na przykład tooinstall hello Azure SDK dla języka Python, co pozwala na dostęp do magazynu tooAzure, magistrali usług i innych usług Azure, wpisz:

    env/bin/pip install azure

Upewnij się, że tooupdate pliku requirements.txt:

    env/bin/pip freeze > requirements.txt

Zatwierdź zmiany hello:

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a>Wdrażanie tooAzure
tootrigger wdrożenia hello wypychania zmiany tooAzure:

    git push azure master

Zostanie wyświetlone dane wyjściowe hello hello skryptu wdrożenia, łącznie z tworzeniem środowiska wirtualnego, instalowaniem pakietów i tworzeniem pliku web.config.

Przeglądaj zmiany toohello tooview adresu URL platformy Azure.

## <a name="troubleshooting---package-installation"></a>Rozwiązywanie problemów — instalowanie pakietów
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a>Rozwiązywanie problemów — środowisko wirtualne
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a>Następne kroki
Wykonaj te toolearn łącza więcej informacji na temat Bottle i narzędzi Python Tools for Visual Studio: 

* [Dokumentacja bottle]
* [narzędzi Python Tools for Visual Studio dokumentacji]

Aby uzyskać informacje o korzystaniu z magazynu tabel platformy Azure i bazy danych MongoDB:

* [Bottle i bazy danych MongoDB na platformie Azure przy użyciu narzędzi Python Tools for Visual Studio]
* [Bottle i magazynu tabel platformy Azure na platformie Azure przy użyciu narzędzi Python Tools for Visual Studio]

## <a name="whats-changed"></a>Co zostało zmienione
* Toohello przewodnik zmiany z tooApp witryn sieci Web usługi dla: [usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

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

