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
# <a name="creating-web-apps-with-django-in-azure"></a>Tworzenie aplikacji sieci Web przy użyciu platformy Django na platformie Azure
Ten przewodnik opisuje sposób uruchamiania systemem Python tooget [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714). Usługa Web Apps zapewnia ograniczony bezpłatny hosting i szybkie wdrażanie, a także możliwość korzystania z języka Python. Rozwoju aplikacji, możesz przełączyć toopaid hosting lub można również zintegrować z wszystkimi hello innymi usługami Azure.

Utworzysz aplikację przy użyciu platformy sieci web Django hello (zobacz alternatywne wersje tego samouczka dla [Flask](web-sites-python-create-deploy-flask-app.md) i [Bottle](web-sites-python-create-deploy-bottle-app.md)). Zostanie tworzenie aplikacji sieci web hello z hello Azure Marketplace, skonfigurujesz wdrożenie systemu Git i klonowania repozytorium hello lokalnie. Następnie uruchomisz aplikacji hello lokalnie, wprowadzić zmiany, zatwierdzenia i wypychanie ich tooAzure. Witaj samouczku przedstawiono sposób toodo od systemu Windows lub Mac/Linux.

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
* [Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) — uwaga: ten składnik jest opcjonalny.

**Uwaga**: publikowanie TFS nie jest obecnie obsługiwane dla projektów języka Python.

### <a name="windows"></a>Windows
Jeśli środowisko Python 2.7 lub 3.4 (32-bitowe) nie zostało jeszcze zainstalowane, zalecane jest zainstalowanie [Zestaw Azure SDK dla języka Python w wersji 2.7] lub [zestawu Azure SDK dla języka Python 3.4] przy użyciu Instalatora platformy sieci Web. Spowoduje to zainstalowanie hello 32-bitowej wersji języka Python, narzędzi setuptools, pip, virtualenv itp (32-bitowe środowisko Python jest zainstalowanych na maszynach hostów Azure hello). Możesz również pobrać środowisko Python z witryny [python.org].

W przypadku systemu Git zalecane jest narzędzie [Git dla systemu Windows] lub [Github dla systemu Windows]. Jeśli używasz programu Visual Studio, używając hello zintegrowanej obsługi systemu Git.

Zalecane jest również zainstalowanie narzędzi [Python Tools 2.2 for Visual Studio]. Ten krok jest opcjonalny, ale jeśli masz [programu Visual Studio], włączając hello wolne Visual Studio Community 2013 lub Visual Studio Express 2013 for Web, a następnie zapewni to doskonały IDE języka Python.

### <a name="maclinux"></a>System Mac/Linux
Środowisko Python i system Git powinny być już zainstalowane, ale upewnij się, że masz środowisko Python 2.7 lub 3.4.

## <a name="web-app-creation-on-portal"></a>Tworzenie aplikacji sieci Web w portalu
Witaj pierwszym krokiem tworzenia aplikacji jest toocreate hello aplikacja sieci web za pośrednictwem hello [Azure Portal](https://portal.azure.com).

1. Zaloguj się do hello portalu Azure i kliknij przycisk hello **nowy** przycisku na powitania lewym dolnym rogu.
2. W polu wyszukiwania hello wpisz "python".
3. W wynikach wyszukiwania hello, wybierz **Django** (opublikowanych przez PTVS), następnie kliknij przycisk **Utwórz**.
4. Skonfiguruj hello nową aplikację Django, takich jak tworzenie nowego planu usługi App Service i nowej grupy zasobów dla niego. Następnie kliknij pozycję **Utwórz**.
5. Konfigurowanie publikowania Git dla aplikacji sieci web nowo utworzony wykonując instrukcje hello [tooAzure lokalnego wdrożenia Git usługi aplikacji](app-service-deploy-local-git.md).

## <a name="application-overview"></a>Omówienie aplikacji
### <a name="git-repository-contents"></a>Zawartość repozytorium Git
Poniżej przedstawiono omówienie hello plików, które znajdują się w początkowym repozytorium Git hello, które sklonujemy w następnej sekcji hello.

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

Główne źródła dla aplikacji hello. Składa się z 3 stron (indeks, informacje, kontakt) z układem głównym. Zawartość statyczna i skrypty obejmują bootstrap, jquery, modernizr i respond.

    \manage.py

Obsługa zarządzania lokalnego i serwera projektowego. Za pomocą tej aplikacji hello toorun lokalnie, synchronizowanie bazy danych hello itp.

    \db.sqlite3

Domyślna baza danych. Zawiera tabele niezbędne hello toorun aplikacji hello, ale nie zawiera żadnych użytkowników (należy zsynchronizować hello toocreate bazy danych użytkownika).

    \DjangoWebProject.pyproj
    \DjangoWebProject.sln

Pliki projektu do użycia z narzędziami [Python Tools for Visual Studio].

    \ptvs_virtualenv_proxy.py

Serwer proxy usług IIS dla środowisk wirtualnych i obsługa zdalnego debugowania narzędzi PTVS.

    \requirements.txt

Pakiety zewnętrzne wymagane przez tę aplikację. skrypt wdrożenia Hello będzie narzędzia pip instalowanie pakietów hello wymienione w tym pliku.

    \web.2.7.config
    \web.3.4.config

Pliki konfiguracji programu IIS. skrypt wdrożenia Hello Użyj hello odpowiedniego pliku web.x.y.config i skopiuje go jako plik web.config.

### <a name="optional-files---customizing-deployment"></a>Pliki opcjonalne — dostosowywanie wdrożenia
[!INCLUDE [web-sites-python-django-customizing-deployment](../../includes/web-sites-python-django-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a>Pliki opcjonalne — środowisko uruchomieniowe języka Python
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a>Dodatkowe pliki na serwerze
Niektóre pliki na powitania serwera istnieje, ale nie są dodawane toohello repozytorium git. Są one tworzone przez skrypt wdrożenia hello.

    \web.config

Plik konfiguracji programu IIS. Tworzony na podstawie pliku web.x.y.config przy każdym wdrożeniu.

    \env\

Środowisko wirtualne języka Python. Utworzonych podczas wdrażania, jeśli zgodne środowisko wirtualne już nie istnieje na powitania aplikacji sieci web. Pakiety wymienione w pliku requirements.txt są zainstalowane narzędzia pip, ale narzędzie pip pomija instalację, jeśli hello pakiety są już zainstalowane.

Witaj 3 następnych sekcjach opisano sposób tworzenia aplikacji w 3 różnych środowiskach sieci web na tooproceed z hello:

* System Windows — przy użyciu narzędzi Python Tools for Visual Studio
* System Windows — przy użyciu wiersza polecenia
* System Mac/Linux — przy użyciu wiersza polecenia

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a>Wdrażanie aplikacji sieci Web — system Windows — narzędzia Python Tools for Visual Studio
### <a name="clone-hello-repository"></a>Klonowanie repozytorium hello
Najpierw sklonuj repozytorium hello przy użyciu adresu URL hello na powitania portalu Azure. Aby uzyskać więcej informacji, zobacz [tooAzure lokalnego wdrożenia Git usługi aplikacji](app-service-deploy-local-git.md).

Otwórz plik rozwiązania hello (.sln), który znajduje się w katalogu głównego repozytorium hello hello.

![](./media/web-sites-python-create-deploy-django-app/ptvs-solution-django.png)

### <a name="create-virtual-environment"></a>Tworzenie środowiska wirtualnego
Teraz utwórz środowisko wirtualne dla wdrożenia lokalnego. Kliknij prawym przyciskiem myszy pozycję **Środowiska Python** i wybierz pozycję **Dodaj środowisko wirtualne**.

* Upewnij się, że nazwa hello środowiska hello jest `env`.
* Wybierz interpreter podstawowy hello. Upewnij się, że toouse hello sama wersja środowiska Python, którą wybrano dla aplikacji sieci web (w pliku runtime.txt lub hello **ustawienia aplikacji** bloku aplikacji sieci web w portalu Azure hello).
* Upewnij się, zaznaczono opcję hello toodownload i zainstaluj pakiety.

![](./media/web-sites-python-create-deploy-django-app/ptvs-add-virtual-env-27.png)

Kliknij przycisk **Utwórz**. Spowoduje to utworzenie środowiska wirtualnego hello i zainstalowanie składników zależnych wymienionych w pliku requirements.txt.

### <a name="create-a-superuser"></a>Tworzenie administratora
Baza danych Hello dołączona aplikacji hello nie zawiera definicji administratora. W kolejności toouse hello logowania funkcjonalności aplikacji hello lub interfejsu administracyjnego Django hello (Jeśli zdecydujesz tooenable go), będziesz potrzebować toocreate administratora.

Uruchom to z hello wiersza polecenia w folderze projektu:

    env\scripts\python manage.py createsuperuser

Postępuj zgodnie z nazwy użytkownika hello hello monity tooset, hasło itp.

### <a name="run-using-development-server"></a>Uruchamianie przy użyciu serwera projektowego
Naciśnij klawisz F5 toostart debugowania i przeglądarki sieci web zostanie otwarty toohello strony uruchomionej lokalnie.

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

Można ustawić punktów przerwania w hello źródeł, użyj hello czujki systemu windows itd. Zobacz hello [narzędzi Python Tools for Visual Studio dokumentacji] Aby uzyskać więcej informacji na temat hello różnych funkcji.

### <a name="make-changes"></a>Wprowadzanie zmian
Teraz możesz eksperymentować, wprowadzając zmiany toohello aplikacji źródeł i/lub szablonach.

Po przetestowaniu zmiany je zatwierdzić toohello repozytorium Git:

![](./media/web-sites-python-create-deploy-django-app/ptvs-commit-django.png)

### <a name="install-more-packages"></a>Instalowanie dodatkowych pakietów
Aplikacja może mieć zależności poza środowiskiem Python i platformą Django.

Możesz zainstalować dodatkowe pakiety przy użyciu narzędzia pip. tooinstall pakiet, kliknij prawym przyciskiem myszy na powitania środowisko wirtualne i wybierz **zainstaluj pakiet języka Python**.

Na przykład tooinstall hello Azure SDK dla języka Python, który zapewnia dostęp tooAzure magazynu, usługi service bus i innymi usługami Azure, wprowadź `azure`:

![](./media/web-sites-python-create-deploy-django-app/ptvs-install-package-dialog.png)

Kliknij prawym przyciskiem myszy na powitania środowiska wirtualnego, a następnie wybierz **Generuj plik requirements.txt** tooupdate requirements.txt.

Następnie Zatwierdź repozytorium Git toohello toorequirements.txt zmiany hello.

### <a name="deploy-tooazure"></a>Wdrażanie tooAzure
polecenie tootrigger wdrożenia, **synchronizacji** lub **Push**. Synchronizacja obejmuje zarówno wypychanie, jak i ściąganie.

![](./media/web-sites-python-create-deploy-django-app/ptvs-git-push.png)

pierwszym wdrożeniu Hello wymaga czasu, ponieważ obejmuje tworzenie środowiska wirtualnego, instalowanie pakietów itp.

Program Visual Studio nie wyświetla postęp hello hello wdrożenia. Jeśli chcesz tooreview hello w danych wyjściowych, zobacz sekcję hello na [Rozwiązywanie problemów — wdrożenie](#troubleshooting-deployment).

Przeglądaj zmiany toohello tooview adresu URL platformy Azure.

## <a name="web-app-development---windows---command-line"></a>Wdrażanie aplikacji sieci Web — system Windows — wiersz polecenia
### <a name="clone-hello-repository"></a>Klonowanie repozytorium hello
Najpierw sklonować repozytorium hello przy użyciu adresu URL hello na powitania portalu Azure i dodać hello repozytorium Azure jako zdalnej. Aby uzyskać więcej informacji, zobacz [tooAzure lokalnego wdrożenia Git usługi aplikacji](app-service-deploy-local-git.md).

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url>

### <a name="create-virtual-environment"></a>Tworzenie środowiska wirtualnego
Utworzymy nowe środowisko wirtualne dla celów programistycznych (nie należy dodawać go toohello repozytorium). Wirtualnych środowisk języka Python nie są można zmieniać lokalizacji, dlatego każdy Deweloper pracujący nad aplikacji hello tworzy własne środowisko lokalnie.

Upewnij się, toouse hello sama wersja środowiska Python, którą wybrano dla aplikacji sieci web (w pliku runtime.txt lub hello bloku ustawienia aplikacji aplikacji sieci web w portalu Azure hello).

Dla środowiska Python w wersji 2.7:

    c:\python27\python.exe -m virtualenv env

Dla środowiska Python w wersji 3.4:

    c:\python34\python.exe -m venv env

Zainstaluj pakiety zewnętrzne wymagane przez aplikację. Możesz użyć pliku requirements.txt hello w głównym hello hello repozytorium tooinstall hello pakietów w środowisku wirtualnym:

    env\scripts\pip install -r requirements.txt

### <a name="create-a-superuser"></a>Tworzenie administratora
Baza danych Hello dołączona aplikacji hello nie zawiera definicji administratora. W kolejności toouse hello logowania funkcjonalności aplikacji hello lub interfejsu administracyjnego Django hello (Jeśli zdecydujesz tooenable go), będziesz potrzebować toocreate administratora.

Uruchom to z hello wiersza polecenia w folderze projektu:

    env\scripts\python manage.py createsuperuser

Postępuj zgodnie z nazwy użytkownika hello hello monity tooset, hasło itp.

### <a name="run-using-development-server"></a>Uruchamianie przy użyciu serwera projektowego
Można uruchomić aplikacji hello na serwerze projektowym z hello następujące polecenie:

    env\scripts\python manage.py runserver

Witaj konsoli zostanie wyświetlony adres URL hello i nasłuchuje portu powitania serwera:

![](./media/web-sites-python-create-deploy-django-app/windows-run-local-django.png)

Następnie otwórz adres URL toothat przeglądarki sieci web.

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

### <a name="make-changes"></a>Wprowadzanie zmian
Teraz możesz eksperymentować, wprowadzając zmiany toohello aplikacji źródeł i/lub szablonach.

Po przetestowaniu zmiany je zatwierdzić toohello repozytorium Git:

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a>Instalowanie dodatkowych pakietów
Aplikacja może mieć zależności poza środowiskiem Python i platformą Django.

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

lub

    pyvenv env

Zainstaluj pakiety zewnętrzne wymagane przez aplikację. Możesz użyć pliku requirements.txt hello w głównym hello hello repozytorium tooinstall hello pakietów w środowisku wirtualnym:

    env/bin/pip install -r requirements.txt

### <a name="create-a-superuser"></a>Tworzenie administratora
Baza danych Hello dołączona aplikacji hello nie zawiera definicji administratora. W kolejności toouse hello logowania funkcjonalności aplikacji hello lub interfejsu administracyjnego Django hello (Jeśli zdecydujesz tooenable go), będziesz potrzebować toocreate administratora.

Uruchom to z hello wiersza polecenia w folderze projektu:

    env/bin/python manage.py createsuperuser

Postępuj zgodnie z nazwy użytkownika hello hello monity tooset, hasło itp.

### <a name="run-using-development-server"></a>Uruchamianie przy użyciu serwera projektowego
Można uruchomić aplikacji hello na serwerze projektowym z hello następujące polecenie:

    env/bin/python manage.py runserver

Witaj konsoli zostanie wyświetlony adres URL hello i nasłuchuje portu powitania serwera:

![](./media/web-sites-python-create-deploy-django-app/mac-run-local-django.png)

Następnie otwórz adres URL toothat przeglądarki sieci web.

![](./media/web-sites-python-create-deploy-django-app/mac-browser-django.png)

### <a name="make-changes"></a>Wprowadzanie zmian
Teraz możesz eksperymentować, wprowadzając zmiany toohello aplikacji źródeł i/lub szablonach.

Po przetestowaniu zmiany je zatwierdzić toohello repozytorium Git:

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a>Instalowanie dodatkowych pakietów
Aplikacja może mieć zależności poza środowiskiem Python i platformą Django.

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

## <a name="troubleshooting---static-files"></a>Rozwiązywanie problemów — pliki statyczne
Platforma Django korzysta hello koncepcji zbierania plików statycznych. Pobiera wszystkie hello pliki statyczne z oryginalnej lokalizacji i kopiuje je tooa pojedynczy folder. Dla tej aplikacji, kopiowane są zbyt`/static`.

Ta operacja jest wykonywana, ponieważ pliki statyczne mogą pochodzić z różnych „aplikacji” Django. Na przykład hello pliki statyczne z interfejsów administracyjnych Django hello znajdują się w podfolderze biblioteki Django w środowisku wirtualnym hello. Pliki statyczne zdefiniowane przez tę aplikację znajdują się w folderze `/app/static`. W przypadku użycia dodatkowych „aplikacji” Django pliki statyczne będą znajdować się w kilku miejscach.

Przy uruchamianiu aplikacji hello w trybie debugowania, aplikacja hello służy hello pliki statyczne z oryginalnej lokalizacji.

Przy uruchamianiu aplikacji hello w trybie wersji, aplikacja hello jest **nie** służyć hello plików statycznych. Jest odpowiedzialny za hello hello — plików hello tooserve serwera sieci web. Dla tej aplikacji IIS udostępnia pliki statyczne hello z `/static`.

Zbieranie plików statycznych Hello odbywa się automatycznie jako część hello skryptu wdrożenia, a uprzednio zebrane pliki. Oznacza to kolekcji hello występuje przy każdym wdrożeniu spowolnienie wdrażania bit, ale gwarantuje, że nieaktualne pliki będą niedostępne i potencjalny problem z zabezpieczeniami.

Jeśli chcesz tooskip zbieranie plików statycznych dla aplikacji Django:

    \.skipDjango

Następnie należy kolekcji hello toodo ręcznie na komputerze lokalnym:

    env\scripts\python manage.py collectstatic

Następnie usuń hello `\static` z folderu `.gitignore` i dodaj go toohello repozytorium Git.

## <a name="troubleshooting---settings"></a>Rozwiązywanie problemów — ustawienia
Różne ustawienia dla aplikacji hello można zmienić w `DjangoWebProject/settings.py`.

Dla wygody deweloperów tryb debugowania jest włączony. Jeden zalet który jest będziesz w stanie toosee obrazów i innej zawartości statycznej podczas uruchamiania lokalnego bez konieczności toocollect plików statycznych.

tryb debugowania toodisable:

    DEBUG = False

Po wyłączeniu debugowania hello wartość `ALLOWED_HOSTS` toobe musi zaktualizować nazwy hosta Azure hello tooinclude. Na przykład:

    ALLOWED_HOSTS = (
        'pythonapp.azurewebsites.net',
    )

lub tooenable żadnych:

    ALLOWED_HOSTS = (
        '*',
    )

W praktyce może być toodo coś bardziej złożonych toodeal przełączania debugowania i wydania tryb i nazwy hosta hello pobierania.

Można ustawić zmienne środowiskowe za pośrednictwem portalu Azure hello **Konfiguruj** strony w hello **ustawień aplikacji** sekcji.  Może to być przydatne do ustawiania wartości, które nie mogą podlegać tooappear w hello źródłach (parametry połączenia, hasła itp.) lub, które mają tooset inaczej platformy Azure i komputera lokalnego. W `settings.py`, można zbadać za pomocą zmiennych środowiskowych hello `os.getenv`.

## <a name="using-a-database"></a>Korzystanie z bazy danych
Hello bazy danych, która jest zawarta w aplikacji hello jest bazą danych sqlite. Jest to wygodna i przydatna domyślna baza danych toouse rozwoju, nie wymaga prawie ustawień. Hello bazy danych są przechowywane w pliku db.sqlite3 hello w folderze projektu hello.

Platforma Azure oferuje usługi bazy danych, które są łatwe toouse z poziomu aplikacji Django. Samouczki dotyczące użycia [bazy danych SQL] i [MySQL] z poziomu aplikacji Django Pokaż kroki hello niezbędne toocreate hello bazy danych usługi, Zmień ustawienia bazy danych hello w `DjangoWebProject/settings.py`i hello biblioteki wymagane tooinstall.

Oczywiście jeśli wolisz toomanage własnymi serwerami bazy danych, możesz to zrobić przy użyciu systemu Windows lub Linux maszyn wirtualnych działających na platformie Azure.

## <a name="django-admin-interface"></a>Interfejs administracyjny Django
Po rozpoczęciu tworzenia modeli, można toopopulate hello bazy danych określonymi danymi. Łatwe toodo dodawania i edytowania zawartości w trybie interakcyjnym jest interfejsu administracyjnego Django hello toouse.

Hello kod dla interfejsu administracyjnego hello jest umieszczony w komentarzach w źródłach aplikacji hello, ale jest jednoznacznie oznaczony, dlatego możesz go łatwo uaktywnić (Wyszukaj "admin").

Po włączeniu synchronizacji hello bazy danych, uruchamianie aplikacji hello i przejdź zbyt`/admin`.

## <a name="next-steps"></a>Następne kroki
Wykonaj te toolearn łącza więcej informacji na temat Django i narzędzi Python Tools for Visual Studio:

* [Dokumentacja platformy Django]
* [narzędzi Python Tools for Visual Studio dokumentacji]

Aby uzyskać informacje na temat baz danych SQL Database i MySQL:

* [Obsługa platformy Django i bazy danych MySQL na platformie Azure przy użyciu narzędzi Python Tools for Visual Studio]
* [Obsługa platformy Django i bazy danych SQL Database na platformie Azure przy użyciu narzędzi Python Tools for Visual Studio]

Aby uzyskać więcej informacji, zobacz hello [Centrum deweloperów języka Python](/develop/python/).

## <a name="whats-changed"></a>Co zostało zmienione
* Toohello przewodnik zmiany z tooApp witryn sieci Web usługi dla: [usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

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
