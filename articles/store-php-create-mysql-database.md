---
title: "aaaCreate i połącz tooa baza danych MySQL na platformie Azure"
description: "Dowiedz się, jak toouse hello Azure toocreate portalu bazę danych MySQL, a następnie połącz tooit z aplikacji sieci web PHP na platformie Azure."
documentationcenter: php
services: app-service\web
author: cephalin
manager: erikre
editor: 
tags: mysql
ms.assetid: 55465a9a-7e65-4fd9-8a65-dd83ee41f3e5
ms.service: multiple
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm;cephalin
ms.openlocfilehash: 3abc02f8887432625666afd847e9dc0c0a4db2e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-connect-tooa-mysql-database-in-azure"></a>Tworzenie i łączenie tooa baza danych MySQL na platformie Azure
Ten samouczek pokazuje, jak hello bazę danych MySQL toocreate [portalu Azure](https://portal.azure.com) (dostawca jest [ClearDB](http://www.cleardb.com/)) i jak tooit tooconnect za pomocą języka PHP sieci web aplikacji uruchomionej [usłudze Azure App Service](app-service/app-service-value-prop-what-is.md).

> [!NOTE]
> Można również utworzyć bazę danych MySQL jako część [szablon aplikacji Marketplace](app-service-web/app-service-web-create-web-app-from-marketplace.md).
>
>

## <a name="create-a-mysql-database-in-azure-portal"></a>Utwórz bazę danych MySQL w portalu Azure
toocreate bazy danych MySQL w hello portalu Azure, hello następujące:

1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com).
2. W menu po lewej stronie powitania kliknij **nowy** > **dane i magazyn** > **baza danych MySQL**.

    ![Utwórz bazę danych MySQL na platformie Azure - start](./media/store-php-create-mysql-database/create-db-1-start.png)
3. W hello nową bazę danych MySQL [bloku](azure-portal-overview.md), skonfiguruj nową bazę danych MySQL w następujący sposób (*bloku*: strony portalu, który zostanie otwarty w poziomie):

   * **Nazwa bazy danych**: wpisz nazwę unikatową identyfikację
   * **Subskrypcja**: Wybierz hello toouse subskrypcji
   * **Bazy danych typu**: Wybierz **Shared** ekonomicznych lub wolnego warstw, lub **dedykowana** tooget dedykowanego zasobów.
   * **Grupa zasobów**: Dodaj istniejącą tooan bazy danych MySQL hello [grupy zasobów](azure-resource-manager/resource-group-overview.md) lub umieść je w nowej. Zasoby w tej samej grupie można łatwo zarządzać razem powitalne.
   * **Lokalizacja**: Wybierz lokalizację tooyou Zamknij. Podczas dodawania tooan istniejącej grupy zasobów, możesz lokalizacja grupy zasobów toohello zablokowanym.
   * **Warstwy cenowej**: kliknij **warstwy cenowej**, następnie wybierz opcję cenową (**Mercury** warstwa jest bezpłatna), a następnie kliknij przycisk **wybierz**.
   * **Postanowienia prawne**: kliknij **postanowienia prawne**, przejrzyj szczegóły zakupu hello i kliknij przycisk **zakupu**.
   * **Numer PIN toodashboard**: zaznaczyć tooaccess bezpośrednio z poziomu pulpitu nawigacyjnego hello. Jest to szczególnie przydatne, jeśli nie znasz jeszcze nawigacji w portalu.

     Witaj następującego zrzutu ekranu jest tylko przykładem sposobu konfigurowania bazy danych MySQL.  
     ![Utwórz bazę danych MySQL na platformie Azure — Konfigurowanie](./media/store-php-create-mysql-database/create-db-2-configure.png)
4. Po zakończeniu konfigurowania, kliknij przycisk **Utwórz**.

    ![Utwórz bazę danych MySQL na platformie Azure — tworzenie](./media/store-php-create-mysql-database/create-db-3-create.png)

    Zostanie wyświetlone powiadomienie wyskakujące, dzięki czemu będzie wiadomo, że rozpoczęło się wdrażanie.

    ![Trwa tworzenie bazy danych MySQL na platformie Azure-](./media/store-php-create-mysql-database/create-db-4-started-status.png)

    Otrzymasz innej wyskakujących po pomyślnym zakończeniu wdrożenia. Hello portal również zostanie automatycznie otworzyć bloku bazy danych MySQL.

<a name="connect"></a>

## <a name="connect-tooyour-mysql-database"></a>Połącz tooyour baza danych MySQL
informacje o połączeniu hello toosee dla nowej bazy danych MySQL, wystarczy kliknąć **właściwości** w bloku aplikacja sieci web.

![Utwórz bazę danych MySQL na platformie Azure — blok bazy danych MySQL](./media/store-php-create-mysql-database/create-db-5-finished-db-blade.png)

Informacje o połączeniu można teraz używać we wszystkich aplikacjach sieci web. Przykład pokazujący, jak informacje o połączeniu hello toouse z prostej aplikacji PHP są dostępne [tutaj](https://github.com/WindowsAzure/azure-sdk-for-php-samples/tree/master/tasklist-mysql).

## <a name="connect-a-laravel-web-app-from-hello-php-get-started-tutorial"></a>Łączenie aplikacji sieci web Laravel (od hello PHP get samouczku)
Załóżmy, że użytkownik właśnie zakończono hello samouczek [tworzenie, konfigurowanie i wdrażanie tooAzure aplikacji sieci web PHP](app-service-web/app-service-web-php-get-started.md) i mieć [Laravel](https://www.laravel.com/) aplikacji sieci web działających na platformie Azure. Możesz łatwo dodać aplikację Laravel tooyour możliwości bazy danych. Wykonaj poniższe kroki hello:

> [!NOTE]
> Witaj następujących krokach założono zakończeniu samouczka hello [tworzenie, konfigurowanie i wdrażanie tooAzure aplikacji sieci web PHP](app-service-web/app-service-web-php-get-started.md).
>
>

1. Skonfiguruj aplikację Laravel hello w bazie danych MySQL toohello toopoint środowisko rozwoju lokalnego. toodo, otwórz `.env` z aplikacji Laravel katalogu głównego i skonfigurować opcje bazy danych MySQL hello.

        DB_CONNECTION=mysql
        DB_HOST=<HOSTNAME_from_properties_blade>
        DB_PORT=<PORT_from_properties_blade>
        DB_DATABASE=<see_note_below>
        DB_USERNAME=<USERNAME_from_properties_blade>
        DB_PASSWORD=<PASSWORD_from_properties_blade>

   > [!NOTE]
   > W hello **właściwości** bloku może hello nazwę bazy danych MySQL lub może nie być hello jedną wyświetlany w hello **Nazwa bazy danych** pola. Jest lepsze toocheck hello bazy danych parametru w hello **ciąg połączenia** pola.    
   >
   > ![Trwa tworzenie bazy danych MySQL na platformie Azure-](./media/store-php-create-mysql-database/connect-db-1-database-name.png)
   >
   >
2. Witaj najszybszy sposób tooverify, ma dostęp MySQL jest toouse [Laravel przez domyślne uwierzytelnianie szkieletów](https://laravel.com/docs/5.2/authentication#authentication-quickstart).
   W hello terminal wiersza polecenia Uruchom następujące polecenia z katalogu głównego aplikacji Laravel hello:

         php artisan migrate
         php artisan make:auth

    pierwsze polecenie Hello tworzy tabele hello na platformie Azure, oparte na wstępnie zdefiniowanych migracje w hello `database/migrations` katalogu, a drugie polecenie hello rusztowania hello podstawowe widoków i tras do uwierzytelniania i rejestracja użytkownika.
3. Teraz uruchomić serwera wdrożeniowego hello:

        php artisan serve
4. W przeglądarce hello Przejdź toohttp://localhost:8000 i zarejestrować nowego użytkownika, jak pokazano:

    ![Połączenia bazy danych tooMySQL na platformie Azure — zarejestrowania użytkownika](./media/store-php-create-mysql-database/connect-db-2-development-server.png)

    Wykonaj hello interfejsu użytkownika monitu hello ukończenia rejestracji. Po zakończeniu rejestracji, będziesz się logować.

    ![Połączenia bazy danych tooMySQL na platformie Azure — zarejestrowania użytkownika](./media/store-php-create-mysql-database/connect-db-3-registered-user.png)

    Teraz tworzysz aplikację przed hello baza danych MySQL na platformie Azure.
5. Teraz, po prostu potrzebujesz tooreplicate Twojego `.env` ustawienia tooyour aplikacji sieci web Azure. Uruchom następujące polecenia interfejsu wiersza polecenia Azure hello:

        azure site appsetting add DB_CONNECTION=mysql
        azure site appsetting add DB_HOST=<HOSTNAME_from_properties_blade>
        azure site appsetting add DB_PORT=<PORT_from_properties_blade>
        azure site appsetting add DB_DATABASE=<Database_param_from_CONNECTION_INFO_from_properties_blade>
        azure site appsetting add DB_USERNAME=<USERNAME_from_properties_blade>
        azure site appsetting add DB_PASSWORD=<PASSWORD_from_properties_blade>

6. Następnie Zatwierdź i Wypchnij tooAzure hello lokalne zmiany wprowadzone wcześniej uruchomionej `php artisan make:auth`.

        git add .
        git commit -m "scaffold auth views and routes"
        git push azure master
7. Przeglądaj toohello aplikacji sieci web platformy Azure.

        azure site browse
8. Zaloguj się za pomocą poświadczeń użytkownika hello utworzony wcześniej.

    ![Połączenia bazy danych tooMySQL na platformie Azure — przejście tooAzure aplikacji sieci web](./media/store-php-create-mysql-database/connect-db-4-browse-azure-webapp.png)

    Po zalogowaniu, powinna zostać wyświetlona hello przyjazną ekranu po logowaniu.

    ![Połączenia bazy danych tooMySQL na platformie Azure — zalogowany](./media/store-php-create-mysql-database/connect-db-5-logged-in.png)

    Gratulacje, aplikacji sieci web PHP na platformie Azure jest teraz dostęp do danych z bazy danych MySQL.

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji, zobacz hello [Centrum deweloperów języka PHP](/develop/php/).
