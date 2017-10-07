---
title: "aaaDjango i bazy danych SQL na platformie Azure za pomocą narzędzia Python Tools 2.2 for Visual Studio"
description: "Dowiedz się jak toouse hello narzędzi Python Tools dla Visual Studio toocreate aplikacji sieci web Django przechowującej dane w wystąpieniu bazy danych SQL i wdróż je tooAzure aplikacji usługi sieci Web aplikacji."
services: app-service\web
tags: python
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 3a677e64-b5a9-4d43-b9c0-66246368b483
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: b5b2ef4f3292e7df85007465c5394c8660a7d231
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="django-and-sql-database-on-azure-with-python-tools-22-for-visual-studio"></a>Obsługa platformy Django i bazy danych SQL Database na platformie Azure przy użyciu narzędzi Python Tools 2.2 for Visual Studio
W tym samouczku użyjemy [narzędzi Python Tools for Visual Studio] toocreate prostą sonduje aplikacji sieci web przy użyciu jednej z hello PTVS przykładowe szablony. W tym samouczku jest również dostępny jako [wideo](https://www.youtube.com/watch?v=ZwcoGcIeHF4).

Firma Microsoft dowiesz się, jak toouse bazy danych SQL hostowanej na platformie Azure, jak tooconfigure hello toouse aplikacji sieci web bazy danych SQL i jak toopublish hello aplikacji sieci web za[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).

Zobacz hello [Centrum deweloperów języka Python] więcej artykułów o programowaniu aplikacji sieci Web usługi aplikacji Azure z narzędziami PTVS przy użyciu Bottle, Flask i Django oraz sieci web z usługami Azure Table Storage, MySQL i bazy danych SQL. Gdy ten artykuł dotyczy usługi App Service, hello kroki są podobne do programowania [usługi w chmurze Azure].

## <a name="prerequisites"></a>Wymagania wstępne
* Visual Studio 2015
* [32-bitowe środowisko Python w wersji 2.7]
* [Python Tools 2.2 for Visual Studio]
* [Python Tools 2.2 for Visual Studio przykładów VSIX]
* [Azure SDK Tools for VS 2015]
* Django 1.9 lub nowsze

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service. Bez kart kredytowych i bez zobowiązań.
>
>

## <a name="create-hello-project"></a>Utwórz hello projektu
W tej sekcji utworzymy projektu programu Visual Studio przy użyciu przykładowego szablonu. Firma Microsoft będzie utworzyć środowisko wirtualne i zainstalujesz wymagane pakiety. Utworzymy lokalnej bazy danych przy użyciu systemu sqlite. Następnie hello aplikacji sieci web zostanie uruchomiony lokalnie.

1. W programie Visual Studio wybierz pozycje **Plik**, **Nowy projekt**.
2. Szablony projektu z hello Hello [Python Tools 2.2 for Visual Studio przykładów VSIX] są dostępne w ramach **Python**, **przykłady**. Wybierz **projektu sieci Web Django sond** i kliknij przycisk OK toocreate hello projektu.

     ![Okno dialogowe Nowy projekt](./media/web-sites-python-ptvs-django-sql/PollsDjangoNewProject.png)
3. Pakiety zewnętrzne zostanie wyświetlony monit o tooinstall będzie. Wybierz pozycję **Zainstaluj w środowisku wirtualnym**.

     ![Okno dialogowe Pakiety zewnętrzne](./media/web-sites-python-ptvs-django-sql/PollsDjangoExternalPackages.png)
4. Wybierz **Python 2.7** jako podstawowy interpreter hello.

     ![Okno dialogowe Dodawanie środowiska wirtualnego](./media/web-sites-python-ptvs-django-sql/PollsCommonAddVirtualEnv.png)
5. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy węzeł projektu hello i wybierz **Python**, a następnie wybierz **migracji Django**.  Następnie wybierz pozycję **Django — tworzenie administratora**.
6. Spowoduje to otwarcie konsoli zarządzania Django i utworzenie bazy danych sqlite w folderze projektu hello. Wykonaj hello toocreate monity użytkownika.
7. Upewnij się, że aplikacja hello działa, naciskając <kbd>F5</kbd>.
8. Kliknij przycisk **Zaloguj** z paska nawigacji hello u góry hello.

     ![Przeglądarka internetowa](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalMenu.png)
9. Wprowadź poświadczenia hello hello użytkownika, który został utworzony podczas synchronizowania bazy danych hello.

     ![Przeglądarka internetowa](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalLogin.png)
10. Kliknij pozycję **Utwórz przykładową ankietę**.

      ![Przeglądarka internetowa](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserNoPolls.png)
11. Kliknij ankietę i zagłosuj.

      ![Przeglądarka internetowa](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-sql-database"></a>Tworzenie bazy danych SQL
W przypadku bazy danych hello utworzymy bazy danych Azure SQL.

Można utworzyć bazy danych, wykonaj następujące czynności.

1. Zaloguj się do hello [Azure Portal].
2. U dołu okienka nawigacji hello hello, kliknij przycisk **nowy**. , kliknij przycisk **dane i magazyn** > **bazy danych SQL**.
3. Skonfiguruj hello nowej bazy danych SQL, tworząc nową grupę zasobów i wybierz Witaj dla niej odpowiednią lokalizację.
4. Po utworzeniu hello bazy danych SQL, kliknij przycisk **Otwórz w programie Visual Studio** w hello bloku bazy danych.
5. Kliknij przycisk **skonfigurowanie zapory**.
6. W hello **ustawienia zapory** bloku, Dodaj regułę zapory z **START IP** i **KOŃCOWEMU adresowi IP** ustawić toohello publicznego adresu IP komputerze deweloperskim. Kliknij pozycję **Zapisz**.

   Dzięki temu serwer bazy danych toohello połączeń z komputerze deweloperskim.
7. W bloku bazy danych powitania kliknij **właściwości**, następnie kliknij przycisk **Pokaż parametry połączenia bazy danych**.
8. Witaj kopiowania przycisk tooput hello wartości **ADO.NET** hello w Schowku.

## <a name="configure-hello-project"></a>Skonfiguruj hello projektu
W tej sekcji skonfigurujemy naszych sieci web aplikacji toouse hello bazy danych SQL, którą właśnie utworzyliśmy. Firma Microsoft będzie także zainstalować dodatkowe baz toouse wymagane pakiety języka Python przy użyciu platformy Django. Następnie hello aplikacji sieci web zostanie uruchomiony lokalnie.

1. W programie Visual Studio Otwórz **settings.py**, z hello *ProjectName* folderu. Wklej tymczasowo parametry połączenia hello w edytorze hello. Witaj parametry połączenia mają następujący format:

       Server=<ServerName>,<ServerPort>;Database=<DatabaseName>;User ID=<UserName>;Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;

Edytowanie definicji hello `DATABASES` wartości hello toouse powyżej.

        DATABASES = {
            'default': {
                'ENGINE': 'sql_server.pyodbc',
                'NAME': '<DatabaseName>',
                'USER': '<UserName>',
                'PASSWORD': '{your_password_here}',
                'HOST': '<ServerName>',
                'PORT': '<ServerPort>',
                'OPTIONS': {
                    'driver': 'SQL Server Native Client 11.0',
                    'MARS_Connection': 'True',
                }
            }
        }

1. W Eksploratorze rozwiązań w obszarze **środowiska Python**, kliknij prawym przyciskiem myszy na powitania środowisko wirtualne i wybierz **zainstaluj pakiet języka Python**.
2. Zainstaluj pakiet hello `pyodbc` przy użyciu **pip**.

     ![Zainstaluj pakiet języka Python w oknie dialogowym](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackagePyodbc.png)
3. Zainstaluj pakiet hello `django-pyodbc-azure` przy użyciu **pip**.

     ![Zainstaluj pakiet języka Python w oknie dialogowym](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackageDjangoPyodbcAzure.png)
4. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy węzeł projektu hello i wybierz **Python**, a następnie wybierz **migracji Django**.  Następnie wybierz pozycję **Django — tworzenie administratora**.

   Spowoduje to utworzenie tabel hello hello bazy danych SQL utworzony w poprzedniej sekcji hello. Wykonaj hello toocreate monity użytkownika, który nie ma toomatch hello użytkownika w bazie danych sqlite hello utworzone w pierwszej sekcji hello.
5. Uruchamianie aplikacji hello z `F5`. Ankieta utworzona za pomocą **tworzenie przykładowej ankiety** i hello dane przesłane podczas głosowania zostaną zserializowane w bazie danych SQL hello.

## <a name="publish-hello-web-app-tooazure-app-service"></a>Publikowanie tooAzure aplikacji sieci web hello usługi aplikacji
Hello zestawu .NET SDK usługi Azure zapewnia łatwy sposób toodeploy Twojej aplikacji usługi sieci Web aplikacji tooAzure aplikacji sieci web w sieci web.

1. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy węzeł projektu hello i wybierz **publikowania**.

     ![Okno dialogowe Publikowanie w sieci Web](./media/web-sites-python-ptvs-django-sql/PollsCommonPublishWebSiteDialog.png)
2. Kliknij pozycję **Microsoft Azure Web Apps**.
3. Polecenie **nowy** toocreate nowej aplikacji sieci web.
4. Wypełnij następujące pola hello i kliknij przycisk **Utwórz**.

   * **Nazwa aplikacji sieci Web**
   * **Plan usługi App Service**
   * **Grupa zasobów**
   * **Region**
   * Pozostaw **serwera bazy danych** ustawić także**bazy danych**
5. Zaakceptuj wszystkie inne ustawienia domyślne i kliknij przycisk **Opublikuj**.
6. Przeglądarki sieci web zostanie otwarty toohello opublikowana aplikacja sieci web. Powinny pojawić się pracy aplikacji sieci web hello zgodnie z oczekiwaniami, za pomocą hello **SQL** bazy danych hostowanej na platformie Azure.

   Gratulacje!

     ![Przeglądarka internetowa](./media/web-sites-python-ptvs-django-sql/PollsDjangoAzureBrowser.png)

## <a name="next-steps"></a>Następne kroki
Wykonaj te toolearn łącza więcej informacji na temat narzędzi Python Tools for Visual Studio, Django i bazy danych SQL.

* [Dokumentacja narzędzi Python Tools for Visual Studio]
  * [Projekty sieci Web]
  * [Projekty usługi w chmurze]
  * [Debugowanie zdalne na platformie Microsoft Azure]
* [Dokumentacja platformy Django]
* [SQL Database]

## <a name="whats-changed"></a>Co zostało zmienione
* Toohello przewodnik zmiany z tooApp witryn sieci Web usługi dla: [usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

<!--Link references-->
[Centrum deweloperów języka Python]: /develop/python/
[usługi w chmurze Azure]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->
[Azure Portal]: https://portal.azure.com
[narzędzi Python Tools for Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Python Tools 2.2 for Visual Studio przykładów VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025
[Azure SDK Tools for VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[32-bitowe środowisko Python w wersji 2.7]: http://go.microsoft.com/fwlink/?LinkId=517190
[Dokumentacja narzędzi Python Tools for Visual Studio]: http://aka.ms/ptvsdocs
[Debugowanie zdalne na platformie Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Projekty sieci Web]: http://go.microsoft.com/fwlink/?LinkId=624027
[Projekty usługi w chmurze]: http://go.microsoft.com/fwlink/?LinkId=624028
[Dokumentacja platformy Django]: https://www.djangoproject.com/
[SQL Database]: /documentation/services/sql-database/
