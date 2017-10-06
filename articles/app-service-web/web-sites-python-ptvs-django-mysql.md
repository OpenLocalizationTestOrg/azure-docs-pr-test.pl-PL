---
title: "aaaDjango i bazy danych MySQL na platformie Azure za pomocą narzędzia Python Tools 2.2 for Visual Studio"
description: "Dowiedz się jak toouse hello narzędzi Python Tools dla Visual Studio toocreate aplikacji sieci web Django przechowującej dane w wystąpieniu bazy danych MySQL i wdróż je tooAzure aplikacji usługi sieci Web aplikacji."
services: app-service\web
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: c60a50b5-8b5e-4818-a442-16362273dabb
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: 1597c391d20c8e8ef629b4e4d05c9eb64c83bffc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="django-and-mysql-on-azure-with-python-tools-22-for-visual-studio"></a>Obsługa platformy Django i bazy danych MySQL na platformie Azure przy użyciu narzędzi Python Tools 2.2 for Visual Studio
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

W tym samouczku użyjesz [narzędzi Python Tools for Visual Studio](https://www.visualstudio.com/vs/python) toocreate prostą sonduje aplikacji sieci web przy użyciu jednej z hello PTVS przykładowe szablony. Dowiesz się, jak toouse usługi MySQL hostowanej na platformie Azure, jak tooconfigure hello toouse aplikacji sieci web MySQL i jak toopublish hello aplikacji sieci web zbyt[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).

> [!NOTE]
> Hello informacje zawarte w tym samouczku jest również dostępna w powitania po wideo:
> 
> [PTVS 2.1: Aplikacja Django z obsługą MySQL][video]
> 
> 

Zobacz hello [Centrum deweloperów języka Python] więcej artykułów o programowaniu aplikacji sieci Web usługi aplikacji Azure z narzędziami PTVS przy użyciu Bottle, Flask i Django oraz sieci web z usługami Azure Table Storage, MySQL i bazy danych SQL. Gdy ten artykuł dotyczy usługi App Service, hello kroki są podobne do programowania [usługi w chmurze Azure].

## <a name="prerequisites"></a>Wymagania wstępne
* Visual Studio 2015
* [32-bitowe środowisko Python w wersji 2.7] lub [32-bitowe środowisko Python w wersji 3.4]
* [Python Tools 2.2 for Visual Studio]
* [Python Tools 2.2 for Visual Studio przykładów VSIX]
* [Azure SDK Tools for VS 2015]
* Django 1.9 lub nowsze

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<!-- This note should not render as part of hello hello previous include. -->

> [!NOTE]
> Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service. Karta kredytowa nie jest wymagana i nie musisz się do niczego zobowiązywać.
> 
> 

## <a name="create-hello-project"></a>Utwórz hello projektu
W tej sekcji utworzysz projekt programu Visual Studio przy użyciu przykładowego szablonu. Utworzysz środowisko wirtualne i zainstalujesz wymagane pakiety. Utworzysz także lokalną bazę danych przy użyciu systemu SQLite. Następnie uruchomisz aplikację hello lokalnie.

1. W programie Visual Studio wybierz pozycje **Plik**, **Nowy projekt**.
2. Szablony projektu z hello Hello [Python Tools 2.2 for Visual Studio przykładów VSIX] są dostępne w ramach **Python**, **przykłady**. Wybierz **projektu sieci Web Django sond** i kliknij przycisk OK toocreate hello projektu.
   
    ![Okno dialogowe Nowy projekt](./media/web-sites-python-ptvs-django-mysql/PollsDjangoNewProject.png)
3. Pakiety zewnętrzne zostanie wyświetlony monit o tooinstall będzie. Wybierz pozycję **Zainstaluj w środowisku wirtualnym**.
   
    ![Okno dialogowe Pakiety zewnętrzne](./media/web-sites-python-ptvs-django-mysql/PollsDjangoExternalPackages.png)
4. Wybierz **Python 2.7** lub **języka Python 3.4** jako podstawowy interpreter hello.
   
    ![Okno dialogowe Dodawanie środowiska wirtualnego](./media/web-sites-python-ptvs-django-mysql/PollsCommonAddVirtualEnv.png)
5. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy węzeł projektu hello i wybierz **Python**, a następnie wybierz **migracji Django**.  Następnie wybierz pozycję **Django — tworzenie administratora**.
6. Spowoduje to otwarcie konsoli zarządzania Django i utworzenie bazy danych sqlite w folderze projektu hello. Wykonaj hello toocreate monity użytkownika.
7. Upewnij się, że aplikacja hello działa, naciskając `F5`.
8. Kliknij przycisk **Zaloguj** z paska nawigacji hello u góry hello.
   
    ![Pasek nawigacyjny Django](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalMenu.png)
9. Wprowadź poświadczenia hello hello użytkownika, który został utworzony podczas synchronizowania bazy danych hello.
   
    ![Formularz logowania](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalLogin.png)
10. Kliknij pozycję **Utwórz przykładową ankietę**.
    
     ![Tworzenie przykładowej ankiety](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserNoPolls.png)
11. Kliknij ankietę i zagłosuj.
    
     ![Głosowanie w przykładowej ankiecie](./media/web-sites-python-ptvs-django-mysql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-mysql-database"></a>Tworzenie bazy danych MySQL
W przypadku bazy danych hello utworzysz danych ClearDB MySQL hostowaną na platformie Azure.

Ewentualnie możesz utworzyć własną maszynę wirtualną działającą na platformie Azure, a następnie samodzielnie zainstalować środowisko MySQL i administrować nim.

Wykonując poniższe kroki, możesz utworzyć bazę danych z użyciem planu Free.

1. Zaloguj się za toohello [Azure Portal].
2. W górnej części okienka nawigacji hello hello, kliknij **nowy**, następnie kliknij przycisk **dane i magazyn**, a następnie kliknij przycisk **baza danych MySQL**.
3. Skonfiguruj hello nową bazę danych MySQL, tworząc nową grupę zasobów, a następnie wybierz powitania dla niej odpowiednią lokalizację.
4. Po utworzeniu bazy danych MySQL powitania kliknij **właściwości** w hello bloku bazy danych.
5. Hello kopiowania przycisk tooput hello wartości **ciąg połączenia** hello w Schowku.

## <a name="configure-hello-project"></a>Skonfiguruj hello projektu
W tej sekcji skonfigurujesz naszych sieci web aplikacji toouse hello baza danych MySQL utworzonej przed chwilą. Zainstalujesz również dodatkowe Python pakietów wymagane toouse baz danych MySQL przy użyciu platformy Django. Następnie uruchomisz aplikację sieci web hello lokalnie.

1. W programie Visual Studio Otwórz **settings.py**, z hello *ProjectName* folderu. Wklej tymczasowo parametry połączenia hello w edytorze hello. Witaj parametry połączenia mają następujący format:
   
        Database=<NAME>;Data Source=<HOST>;User Id=<USER>;Password=<PASSWORD>
   
    Zmień hello domyślna baza danych **aparat** toouse MySQL i ustaw wartości hello **nazwa**, **użytkownika**, **hasło** i  **HOST** z hello **CONNECTIONSTRING**.
   
        DATABASES = {
            'default': {
                'ENGINE': 'django.db.backends.mysql',
                'NAME': '<Database>',
                'USER': '<User Id>',
                'PASSWORD': '<Password>',
                'HOST': '<Data Source>',
                'PORT': '',
            }
        }
2. W Eksploratorze rozwiązań w obszarze **środowiska Python**, kliknij prawym przyciskiem myszy na powitania środowisko wirtualne i wybierz **zainstaluj pakiet języka Python**.
3. Zainstaluj pakiet hello `mysqlclient` przy użyciu **pip**.
   
    ![Okno dialogowe Instalowanie pakietu](./media/web-sites-python-ptvs-django-mysql/PollsDjangoMySQLInstallPackage.png)
4. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy węzeł projektu hello i wybierz **Python**, a następnie wybierz **migracji Django**.  Następnie wybierz pozycję **Django — tworzenie administratora**.
   
    Spowoduje to utworzenie tabel hello hello bazy danych MySQL utworzonej w poprzedniej sekcji hello. Wykonaj hello toocreate monity użytkownika, który nie ma toomatch hello użytkownika w bazie danych sqlite hello utworzone w pierwszej sekcji tego artykułu hello.
5. Uruchamianie aplikacji hello z `F5`. Ankieta utworzona za pomocą **tworzenie przykładowej ankiety** i hello dane przesłane podczas głosowania zostaną zserializowane w hello baza danych MySQL.

## <a name="publish-hello-web-app-tooazure-app-service"></a>Publikowanie tooAzure aplikacji sieci web hello usługi aplikacji
Hello Azure .NET SDK udostępnia toodeploy łatwy sposób tooAzure aplikacji sieci web usługi aplikacji.

1. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy węzeł projektu hello i wybierz **publikowania**.
   
    ![Okno dialogowe Publikowanie w sieci Web](./media/web-sites-python-ptvs-django-mysql/PollsCommonPublishWebSiteDialog.png)
2. Kliknij pozycję **Usługa aplikacji Microsoft Azure**.
3. Polecenie **nowy** toocreate nowej aplikacji sieci web.
4. Wypełnij następujące pola hello i kliknij przycisk **Utwórz**:
   
   * **Nazwa aplikacji sieci Web**
   * **Plan usługi App Service**
   * **Grupa zasobów**
   * **Region**
   * Pozostaw **serwera bazy danych** ustawić także**bazy danych**
5. Zaakceptuj wszystkie inne ustawienia domyślne i kliknij przycisk **Opublikuj**.
6. Przeglądarki sieci web zostanie otwarty toohello opublikowana aplikacja sieci web. Powinny pojawić się pracy aplikacji sieci web hello zgodnie z oczekiwaniami, za pomocą hello **MySQL** bazy danych hostowanej na platformie Azure.
   
    ![Przeglądarka internetowa](./media/web-sites-python-ptvs-django-mysql/PollsDjangoAzureBrowser.png)
   
    Gratulacje! Został pomyślnie opublikowany Twojej tooAzure aplikacji sieci web opartych na MySQL.

## <a name="next-steps"></a>Następne kroki
Wykonaj te toolearn łącza więcej informacji na temat narzędzi Python Tools for Visual Studio, Django i MySQL.

* [Dokumentacja narzędzi Python Tools for Visual Studio]
  * [Projekty sieci Web]
  * [Projekty usługi w chmurze]
  * [Debugowanie zdalne na platformie Microsoft Azure]
* [Dokumentacja platformy Django]
* [MySQL]

Aby uzyskać więcej informacji, zobacz hello [Centrum deweloperów języka Python](/develop/python/).

<!--Link references-->

[Centrum deweloperów języka Python]: /develop/python/
[usługi w chmurze Azure]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->

[Azure Portal]: https://portal.azure.com
[Python Tools for Visual Studio]: https://www.visualstudio.com/vs/python/
[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Python Tools 2.2 for Visual Studio przykładów VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025
[Azure SDK Tools for VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[32-bitowe środowisko Python w wersji 2.7]: http://go.microsoft.com/fwlink/?LinkId=517190
[32-bitowe środowisko Python w wersji 3.4]: http://go.microsoft.com/fwlink/?LinkId=517191
[Dokumentacja narzędzi Python Tools for Visual Studio]: http://aka.ms/ptvsdocs
[Debugowanie zdalne na platformie Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Projekty sieci Web]: http://go.microsoft.com/fwlink/?LinkId=624027
[Projekty usługi w chmurze]: http://go.microsoft.com/fwlink/?LinkId=624028
[Dokumentacja platformy Django]: https://www.djangoproject.com/
[MySQL]: http://www.mysql.com/
[video]: http://youtu.be/oKCApIrS0Lo
