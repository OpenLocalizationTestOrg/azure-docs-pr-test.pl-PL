---
title: "Obsługa platformy Django i bazy danych SQL Database na platformie Azure przy użyciu narzędzi Python Tools 2.2 for Visual Studio"
description: "Dowiedz się, jak używać narzędzi Python Tools for Visual Studio do tworzenia aplikacji sieci web Django przechowującej dane w wystąpieniu bazy danych SQL i wdróż je do aplikacji sieci Web usługi aplikacji Azure."
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
ms.openlocfilehash: 65b59dee2b7bddca77d31c692dab713c68d67e24
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="django-and-sql-database-on-azure-with-python-tools-22-for-visual-studio"></a>Obsługa platformy Django i bazy danych SQL Database na platformie Azure przy użyciu narzędzi Python Tools 2.2 for Visual Studio
W tym samouczku użyjemy [narzędzi Python Tools for Visual Studio] utworzyć prostą sondy sieci web aplikacji przy użyciu jednego z szablonów próbki PTVS. W tym samouczku jest również dostępny jako [wideo](https://www.youtube.com/watch?v=ZwcoGcIeHF4).

Firma Microsoft dowiesz się, sposobu korzystania z bazy danych SQL hostowanej na platformie Azure, jak skonfigurować aplikację sieci web do używania bazy danych SQL i jak opublikować aplikację sieci web, aby [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).

Zobacz [Centrum deweloperów języka Python] więcej artykułów o programowaniu aplikacji sieci Web usługi aplikacji Azure z narzędziami PTVS przy użyciu Bottle, Flask i Django oraz sieci web z usługami Azure Table Storage, MySQL i bazy danych SQL. Chociaż ten artykuł dotyczy usługi App Service, opisane kroki są podobne do programowania [usług Azure Cloud Services].

## <a name="prerequisites"></a>Wymagania wstępne
* Visual Studio 2015
* [32-bitowe środowisko Python w wersji 2.7]
* [Python Tools 2.2 for Visual Studio]
* [Zestaw przykładów VSIX dla narzędzi Python Tools 2.2 for Visual Studio]
* [Azure SDK Tools for VS 2015]
* Django 1.9 lub nowsze

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Jeśli chcesz zacząć korzystać z usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź do artykułu [Try App Service](https://azure.microsoft.com/try/app-service/) (Wypróbuj usługę App Service), w którym wyjaśniono, jak od razu utworzyć początkową aplikację sieci Web o krótkim okresie istnienia w usłudze App Service. Bez kart kredytowych i bez zobowiązań.
>
>

## <a name="create-the-project"></a>Tworzenie projektu
W tej sekcji utworzymy projektu programu Visual Studio przy użyciu przykładowego szablonu. Firma Microsoft będzie utworzyć środowisko wirtualne i zainstalujesz wymagane pakiety. Utworzymy lokalnej bazy danych przy użyciu systemu sqlite. Następnie aplikacja sieci web zostanie uruchomiony lokalnie.

1. W programie Visual Studio wybierz pozycje **Plik**, **Nowy projekt**.
2. Szablony projektu z [Zestaw przykładów VSIX dla narzędzi Python Tools 2.2 for Visual Studio] są dostępne w menu **Python**, **Przykłady**. Wybierz pozycję **Polls Django Web Project** (Projekt sieci Web Django z ankietą) i kliknij przycisk OK, aby utworzyć projekt.

     ![Okno dialogowe Nowy projekt](./media/web-sites-python-ptvs-django-sql/PollsDjangoNewProject.png)
3. Zostanie wyświetlony monit o zainstalowanie pakietów zewnętrznych. Wybierz pozycję **Zainstaluj w środowisku wirtualnym**.

     ![Okno dialogowe Pakiety zewnętrzne](./media/web-sites-python-ptvs-django-sql/PollsDjangoExternalPackages.png)
4. Wybierz jako podstawowy interpreter **Python 2.7**.

     ![Okno dialogowe Dodawanie środowiska wirtualnego](./media/web-sites-python-ptvs-django-sql/PollsCommonAddVirtualEnv.png)
5. W **Eksploratorze rozwiązań** kliknij prawym przyciskiem myszy węzeł projektu i wybierz pozycję **Python**, a następnie wybierz pozycję **Migracja platformy Django**.  Następnie wybierz pozycję **Django — tworzenie administratora**.
6. Spowoduje to otwarcie konsoli zarządzania Django i utworzenie bazy danych SQLite w folderze projektu. Postępuj zgodnie z monitami, aby utworzyć użytkownika.
7. Upewnij się, że aplikacja działa, naciskając <kbd>F5</kbd>.
8. Kliknij pozycję **Zaloguj** na górnym pasku nawigacyjnym.

     ![Przeglądarka internetowa](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalMenu.png)
9. Wprowadź poświadczenia użytkownika, który został utworzony podczas synchronizowania bazy danych.

     ![Przeglądarka internetowa](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalLogin.png)
10. Kliknij pozycję **Utwórz przykładową ankietę**.

      ![Przeglądarka internetowa](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserNoPolls.png)
11. Kliknij ankietę i zagłosuj.

      ![Przeglądarka internetowa](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-sql-database"></a>Tworzenie bazy danych SQL
Dla bazy danych utworzymy bazy danych Azure SQL.

Można utworzyć bazy danych, wykonaj następujące czynności.

1. Zaloguj się do [portalu Azure].
2. W dolnej części okienka nawigacji kliknij **nowy**. , kliknij przycisk **dane i magazyn** > **bazy danych SQL**.
3. Skonfiguruj nową bazę danych SQL, tworząc nową grupę zasobów, a następnie wybierz dla niej odpowiednią lokalizację.
4. Po utworzeniu bazy danych SQL, kliknij przycisk **Otwórz w programie Visual Studio** w bloku bazy danych.
5. Kliknij przycisk **skonfigurowanie zapory**.
6. W **ustawienia zapory** bloku, Dodaj regułę zapory z **START IP** i **KOŃCOWEMU adresowi IP** ustawiona na komputerze deweloperskim publiczny adres IP. Kliknij pozycję **Zapisz**.

   Pozwoli to połączenia z serwerem bazy danych w komputerze deweloperskim.
7. W bloku bazy danych, kliknij **właściwości**, następnie kliknij przycisk **Pokaż parametry połączenia bazy danych**.
8. Użyj przycisku kopiowania, aby umieścić wartość elementu **ADO.NET** w Schowku.

## <a name="configure-the-project"></a>Konfigurowanie projektu
W tej sekcji skonfigurujemy swoją aplikację sieci web do używania bazy danych SQL, które właśnie utworzyliśmy. Firma Microsoft będzie także zainstalować dodatkowe pakiety Python niezbędne do używania bazy danych SQL przy użyciu platformy Django. Następnie aplikacja sieci web zostanie uruchomiony lokalnie.

1. W programie Visual Studio otwórz plik **settings.py** z folderu *NazwaProjektu*. Wklej tymczasowo parametry połączenia w edytorze. Parametry połączenia mają następujący format:

       Server=<ServerName>,<ServerPort>;Database=<DatabaseName>;User ID=<UserName>;Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;

Edytowanie definicji `DATABASES` powyżej wartości.

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

1. W Eksploratorze rozwiązań w obszarze **Środowiska Python** kliknij prawym przyciskiem myszy środowisko wirtualne i wybierz polecenie **Zainstaluj pakiet języka Python**.
2. Zainstaluj pakiet `pyodbc`, korzystając z polecenia **pip**.

     ![Zainstaluj pakiet języka Python w oknie dialogowym](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackagePyodbc.png)
3. Zainstaluj pakiet `django-pyodbc-azure`, korzystając z polecenia **pip**.

     ![Zainstaluj pakiet języka Python w oknie dialogowym](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackageDjangoPyodbcAzure.png)
4. W **Eksploratorze rozwiązań** kliknij prawym przyciskiem myszy węzeł projektu i wybierz pozycję **Python**, a następnie wybierz pozycję **Migracja platformy Django**.  Następnie wybierz pozycję **Django — tworzenie administratora**.

   Spowoduje to utworzenie tabel dla bazy danych SQL, utworzony w poprzedniej sekcji. Postępuj zgodnie z monitami, aby utworzyć użytkownika, nie musi odpowiadać nazwie użytkownika w bazie danych sqlite utworzone w pierwszej sekcji.
5. Uruchom aplikację klawiszem `F5`. Ankieta utworzona za pomocą **tworzenie przykładowej ankiety** oraz dane przesłane podczas głosowania zostaną zserializowane w bazie danych SQL.

## <a name="publish-the-web-app-to-azure-app-service"></a>Publikowanie aplikacji sieci Web w usłudze Azure App Service
Zestaw .NET SDK usługi Azure zapewnia łatwy sposób wdrażania aplikacji sieci web w sieci web do aplikacji sieci Web usługi aplikacji Azure.

1. W **Eksploratorze rozwiązań** kliknij prawym przyciskiem myszy węzeł projektu i wybierz polecenie **Opublikuj**.

     ![Okno dialogowe Publikowanie w sieci Web](./media/web-sites-python-ptvs-django-sql/PollsCommonPublishWebSiteDialog.png)
2. Kliknij pozycję **Microsoft Azure Web Apps**.
3. Kliknij pozycję **Nowa**, aby utworzyć nową aplikację sieci Web.
4. Wypełnij następujące pola i kliknij przycisk **Utwórz**.

   * **Nazwa aplikacji sieci Web**
   * **Plan usługi App Service**
   * **Grupa zasobów**
   * **Region**
   * W polu **Serwer bazy danych** pozostaw wartość **Brak bazy danych**
5. Zaakceptuj wszystkie inne ustawienia domyślne i kliknij przycisk **Opublikuj**.
6. Opublikowana aplikacja sieci Web zostanie automatycznie otwarta w przeglądarce internetowej. Powinna zostać wyświetlona aplikacja sieci web działa zgodnie z oczekiwaniami, za pomocą **SQL** bazy danych hostowanej na platformie Azure.

   Gratulacje!

     ![Przeglądarka internetowa](./media/web-sites-python-ptvs-django-sql/PollsDjangoAzureBrowser.png)

## <a name="next-steps"></a>Następne kroki
Skorzystaj z poniższych linków, aby dowiedzieć się więcej informacji na temat narzędzi Python Tools dla programu Visual Studio, Django i bazy danych SQL.

* [Dokumentacja narzędzi Python Tools for Visual Studio]
  * [Projekty sieci Web]
  * [Projekty usługi w chmurze]
  * [Debugowanie zdalne na platformie Microsoft Azure]
* [Dokumentacja platformy Django]
* [SQL Database]

## <a name="whats-changed"></a>Co zostało zmienione
* Przewodnik dotyczący przejścia od usługi Witryny sieci Web do usługi App Service można znaleźć w temacie [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714) (Usługa Azure App Service i jej wpływ na istniejące usługi platformy Azure).

<!--Link references-->
[Centrum deweloperów języka Python]: /develop/python/
[usług Azure Cloud Services]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->
[portalu Azure]: https://portal.azure.com
[narzędzi Python Tools for Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Zestaw przykładów VSIX dla narzędzi Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Azure SDK Tools for VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[32-bitowe środowisko Python w wersji 2.7]: http://go.microsoft.com/fwlink/?LinkId=517190
[Dokumentacja narzędzi Python Tools for Visual Studio]: http://aka.ms/ptvsdocs
[Debugowanie zdalne na platformie Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Projekty sieci Web]: http://go.microsoft.com/fwlink/?LinkId=624027
[Projekty usługi w chmurze]: http://go.microsoft.com/fwlink/?LinkId=624028
[Dokumentacja platformy Django]: https://www.djangoproject.com/
[SQL Database]: /documentation/services/sql-database/
