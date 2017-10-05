---
title: "Wdrażanie aplikacji sieci web sails.js przy użyciu usługi Azure App Service | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak wdrożyć aplikację Node.js usługi Azure App Service. Ten samouczek pokazuje, jak wdrożyć aplikację sieci web Sails.js."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 8877ddc8-1476-45ae-9e7f-3c75917b4564
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/16/2016
ms.author: cephalin
ms.openlocfilehash: e36fc5f5273f98c3cca91973db9910f32443ec7c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-a-sailsjs-web-app-to-azure-app-service"></a>Wdrażanie aplikacji sieci Web Sails.js przy użyciu usługi Azure App Service
Ten samouczek przedstawia sposób wdrażania aplikacji Sails.js w usłudze Azure App Service. W procesie można zgromadzonych niektórych ogólnej wiedzy na temat konfigurowania aplikacji Node.js do uruchamiania w usłudze App Service.

W tym miejscu dowiesz się, że przydatne umiejętności, takich jak:

* Konfigurowanie aplikacji Sails.js, uruchom w usłudze App Service.
* Wdrażanie aplikacji w usłudze App Service z wiersza polecenia.
* Przeczytaj dzienniki stderr i stdout rozwiązywać problemy z wdrażaniem.
* Przechowywanie zmiennych środowiskowych poza kontrolą źródła.
* Dostęp do zmiennych środowiskowych Azure z aplikacji.
* Połączenie z bazą danych (bazy danych MongoDB).

Należy mieć praktyczną wiedzę o sails.js przy użyciu. W tym samouczku nie jest przeznaczona do pomocy w rozwiązaniu problemy związane z uruchamianiem Sail.js ogólnie.

## <a name="cli-versions-to-complete-the-task"></a>Wersje interfejsu wiersza polecenia umożliwiające wykonanie zadania

Zadanie można wykonać przy użyciu jednej z następujących wersji interfejsu wiersza polecenia:

- [Interfejs wiersza polecenia platformy Azure w wersji 1.0](app-service-web-nodejs-sails-cli-nodejs.md) — nasz interfejs wiersza polecenia dla klasycznego modelu wdrażania i modelu wdrażania na potrzeby zarządzania zasobami
- [Interfejs wiersza polecenia platformy Azure w wersji 2.0](app-service-web-nodejs-sails.md) — nasz interfejs wiersza polecenia nowej generacji dla modelu wdrażania na potrzeby zarządzania zasobami

## <a name="prerequisites"></a>Wymagania wstępne
* [Node.js](https://nodejs.org/)
* [Sails.js](http://sailsjs.org/get-started)
* [Git](http://www.git-scm.com/downloads)
* [Interfejs wiersza polecenia platformy Azure 2.0](/cli/azure/install-az-cli2)
* Konto platformy Microsoft Azure. Jeśli nie masz konta, możesz [utworzyć konto bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) lub [aktywować korzyści dla subskrybentów programu Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).

> [!NOTE]
> Usługę [App Service](https://azure.microsoft.com/try/app-service/) możesz wypróbować, nie mając konta platformy Azure. Utwórz aplikację startową i testuj ją nawet przez godzinę — bez kart kredytowych i bez zobowiązań.
> 
> 

## <a name="step-1-create-and-configure-a-sailsjs-app-locally"></a>Krok 1: Tworzenie i konfigurowanie sails.js przy użyciu aplikacji lokalnie
Po pierwsze szybko utworzyć domyślna aplikacja Sails.js w środowisku projektowania wykonaj następujące czynności:

1. Otwórz wybrany terminal wiersza polecenia dowolnego i `CD` do katalogu roboczego.
2. Tworzenie aplikacji Sails.js i uruchom go:

        sails new <app_name>
        cd <app_name>
        sails lift

    Upewnij się, że można przejść do domyślnej strony głównej w http://localhost:1377.

1. Następnie należy włączyć rejestrowanie dla platformy Azure. W katalogu głównym, Utwórz plik o nazwie `iisnode.yml` i dodaj następujące dwa wiersze:

        loggingEnabled: true
        logDirectory: iisnode

    Włączono rejestrowanie dla [iisnode](https://github.com/tjanczuk/iisnode) serwera, który używa usługi Azure App Service uruchamia aplikacje Node.js. 
    Aby uzyskać więcej informacji o jego działaniu, zobacz [debugowanie aplikacji sieci web Node.js w usłudze Azure App Service](web-sites-nodejs-debug.md).

2. Skonfiguruj aplikację Sails.js do używania zmiennych środowiskowych systemu Azure. Otwórz config/env/production.js do skonfigurowania środowiska produkcyjnego i `port` i `hookTimeout`:

        module.exports = {

            // Use process.env.port to handle web requests to the default HTTP port
            port: process.env.port,
            // Increase hooks timout to 30 seconds
            // This avoids the Sails.js error documented at https://github.com/balderdashy/sails/issues/2691
            hookTimeout: 30000,

            ...
        };

    Można znaleźć w dokumentacji tych ustawień konfiguracji w [dokumentacji Sails.js](http://sailsjs.org/documentation/reference/configuration/sails-config).

4. Następnie kodowania wersji środowiska Node.js, który ma być używany. W pliku package.json, Dodaj następujący `engines` właściwość umożliwiająca ustawienie wersji środowiska Node.js na taki, który chcemy.

        "engines": {
            "node": "6.9.1"
        },

5. Na koniec zainicjować repozytorium Git i przekazać pliki. W katalogu głównym aplikacji (pliku package.json przypadku) uruchom następujące polecenia Git:

        git init
        git add .
        git commit -m "<your commit message>"

Kod jest gotowa do wdrożenia. 

## <a name="step-2-create-an-azure-app-and-deploy-sailsjs"></a>Krok 2: Tworzenie aplikacji platformy Azure i wdrażanie Sails.js

Następnie utwórz zasób usługi aplikacji na platformie Azure i wdrażanie aplikacji Sails.js do niego.

1. Zaloguj się do platformy Azure w następujący sposób:

        az login

    Postępuj zgodnie z wyświetlanymi instrukcjami, aby kontynuować logowanie w przeglądarce za pomocą konta Microsoft zawierającego subskrypcję Azure.

3. Ustaw użytkownika wdrożenia dla usługi App Service. Kod zostanie później wdrożony przy użyciu tych poświadczeń.
   
        az appservice web deployment user set --user-name <username> --password <password>

3. Utwórz [grupy zasobów](../azure-resource-manager/resource-group-overview.md) o nazwie. W tym samouczku środowiska Node.js nie naprawdę musisz wiedzieć, co to jest.

        az group create --location "<location>" --name my-sailsjs-app-group

    Aby sprawdzić, jakich wartości można użyć dla lokalizacji `<location>`, użyj polecenia interfejsu wiersza polecenia `az appservice list-locations`.

3. Tworzenie "Wolne" [planu usługi aplikacji](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) o nazwie. W tym samouczku środowiska Node.js wystarczy wiedzieć, że użytkownik nie zostanie obciążona dla aplikacji sieci web w tym planie.

        az appservice plan create --name my-sailsjs-appservice-plan --resource-group my-sailsjs-app-group --sku FREE

4. Utwórz nową aplikację sieci Web o unikatowej nazwie wprowadzonej w tagu `<app_name>`.

        az appservice web create --name <app_name> --resource-group my-sailsjs-app-group --plan my-sailsjs-appservice-plan

## <a name="step-3-configure-and-deploy-your-sailsjs-app"></a>Krok 3: Konfigurowanie i wdrażanie aplikacji Sails.js

1. Skonfiguruj lokalne wdrożenie narzędzia Git dla aplikacji sieci Web za pomocą następującego polecenia:

        az appservice web source-control config-local-git --name <app_name> --resource-group my-sailsjs-app-group

    Otrzymasz dane wyjściowe JSON podobne do następujących, co oznacza, że skonfigurowano zdalne repozytorium Git:

        {
        "url": "https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git"
        }

6. Dodaj adres URL w formacie JSON jako zdalny obiekt narzędzia Git lokalnego repozytorium Git (nazywanego dla uproszczenia `azure`).

        git remote add azure https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git
   
7. Wdróż przykładowy kod w zdalnym obiekcie narzędzia Git `azure`. Gdy zostanie wyświetlony odpowiedni monit, użyj skonfigurowanych wcześniej poświadczeń wdrożenia.

        git push azure master

7. Na koniec można uruchomić działającą aplikację Azure w przeglądarce:

        az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

    Powinna zostać wyświetlona strona główna sails.js przy użyciu tego samego.

    ![](./media/app-service-web-nodejs-sails/sails-in-azure.png)

## <a name="troubleshoot-your-deployment"></a>Rozwiązywanie problemów z wdrożeniem
Jeśli zaistnieje w usłudze App Service sails.js przy użyciu aplikacji nie powiedzie się, Znajdź dzienniki stderr, aby ułatwić rozwiązywanie problemów.
Aby uzyskać więcej informacji, zobacz [debugowanie aplikacji sieci web Node.js w usłudze Azure App Service](web-sites-nodejs-debug.md).
Jeśli aplikacja została uruchomiona pomyślnie, dziennika stdout powinien być wyświetlony zostanie znanych komunikat:

                   .-..-.
    
       Sails              <|    .-..-.
       v0.12.11            |\
                          /|.\
                         / || \
                       ,'  |'  \
                    .-'.-==|/_--'
                    `--'-------' 
       __---___--___---___--___---___--___
     ____---___--___---___--___---___--___-__

    Server lifted in `D:\home\site\wwwroot`
    To see your app, visit http://localhost:\\.\pipe\c775303c-0ebc-4854-8ddd-2e280aabccac
    To shut down Sails, press <CTRL> + C at any time.

Można kontrolować poziom szczegółowości dzienniki stdout w [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) pliku.

## <a name="connect-to-a-database-in-azure"></a>Połączenie z bazą danych na platformie Azure
Do połączenia z bazą danych na platformie Azure, utworzyć bazę danych, wybranych przez użytkownika na platformie Azure, takich jak bazy danych SQL Azure, MySQL, bazy danych MongoDB, pamięć podręczna Azure (Redis), itp. i użyj odpowiadającego [karty magazyn danych](https://github.com/balderdashy/sails#compatibility) się z nią połączyć. Kroki opisane w tej sekcji opisano sposób nawiązywania połączenia z bazy danych MongoDB przy użyciu [bazy danych Azure rozwiązania Cosmos](../documentdb/documentdb-protocol-mongodb.md) bazy danych, który może obsługiwać połączeń klienckich bazy danych MongoDB.

1. [Tworzenie konta bazy danych rozwiązania Cosmos z obsługą protokołu bazy danych MongoDB](../documentdb/documentdb-create-mongodb-account.md).
2. [Tworzenie kolekcji rozwiązania Cosmos bazy danych i bazy danych](../documentdb/documentdb-create-collection.md). Nazwa kolekcji nie ma znaczenia, ale potrzebna jest nazwa bazy danych podczas nawiązywania połączenia z Sails.js.
3. [Znajdź informacje o połączeniu dla bazy danych DB rozwiązania Cosmos](../cosmos-db/connect-mongodb-account.md#GetCustomConnection).
2. Z wiersza polecenia terminalu należy zainstalować adapter bazy danych MongoDB:

        npm install sails-mongo --save

3. Otwórz config/connections.js i Dodaj następujący obiekt połączenie do listy:

        docDbMongo: {
            adapter: 'sails-mongo',
            user: process.env.dbuser,
            password: process.env.dbpassword,
            host: process.env.dbhost,
            port: process.env.dbport,
            database: process.env.dbname,
            ssl: true
        },

    > [!NOTE] 
    > `ssl: true` Ważne jest opcja, ponieważ [DB rozwiązania Cosmos wymaga](../cosmos-db/connect-mongodb-account.md#connection-string-requirements). 
    >
    >

4. Dla każdej zmiennej środowiskowej (`process.env.*`), należy ustawić go w usłudze App Service. Aby to zrobić, uruchom następujące polecenia z terminala. Użyj informacji o połączeniu dla Twojej bazy danych rozwiązania Cosmos.

        az appservice web config appsettings update --settings dbuser="<database user>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbpassword="<database password>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbhost="<database hostname>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbport="<database port>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbname="<database name>" --name <app_name> --resource-group my-sailsjs-app-group

    Wprowadzanie ustawień w ustawieniach aplikacji Azure chroni poufne dane poza do kontroli źródła (Git). Następnie należy skonfigurować środowiska deweloperskiego, aby użyć tego samego informacji o połączeniu.
5. Otwórz config/local.js i Dodaj następujący obiekt połączenia:

        connections: {
            docDbMongo: {
                user: "<database user>",
                password: "<database password>",
                host: "<database hostname>",
                database: "<database name>",
                ssl: true
            },
        },

    Ta konfiguracja zastępuje ustawienia w pliku config/connections.js w środowisku lokalnym. Ten plik jest wykluczone przez domyślne .gitignore w projekcie, dlatego nie można zapisać w usłudze Git. Teraz jest możliwość połączenia z bazą danych rozwiązania Cosmos bazy danych (bazy danych MongoDB) zarówno z aplikacji sieci web platformy Azure i środowiska deweloperskiego lokalnego.
6. Otwórz config/env/production.js do konfigurowania środowiska produkcyjnego i dodaj następujące `models` obiektu:

        models: {
            connection: 'docDbMongo',
            migrate: 'safe'
        },
7. Otwórz config/env/development.js do konfigurowania środowiska deweloperskiego i dodaj następujące `models` obiektu:

        models: {
            connection: 'docDbMongo',
            migrate: 'alter'
        },

    `migrate: 'alter'`Umożliwia tworzenie i aktualizowanie kolekcji bazy danych lub tabel łatwo przy użyciu funkcji migracji bazy danych. Jednak `migrate: 'safe'` służy do środowiska Azure (środowisko produkcyjne), ponieważ Sails.js nie będzie można korzystać `migrate: 'alter'` w środowisku produkcyjnym (zobacz [dokumentacji Sails.js](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings)).
8. Z poziomu terminala [Generowanie](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) Sails.js [plan interfejsu API](http://sailsjs.org/documentation/concepts/blueprints) tak jak zwykle następnie należy uruchomić `sails lift` utworzyć bazę danych z Sails.js migracja bazy danych. Na przykład:

         sails generate api mywidget
         sails lift

    `mywidget` Modelu wygenerowanym przez to polecenie jest pusty, ale możemy ich użyć do wyświetlenia, że istnieje łączność z bazą danych.
    Po uruchomieniu `sails lift`, tworzy Brak kolekcje i tabel dla modeli aplikacji używa.
9. Dostęp do planu API właśnie utworzony w przeglądarce. Na przykład:

        http://localhost:1337/mywidget/create

    Interfejs API należy wrócić utworzony wpis do w oknie przeglądarki, co oznacza, że pomyślnie utworzono kolekcję.

        {"id":1,"createdAt":"2016-09-23T13:32:00.000Z","updatedAt":"2016-09-23T13:32:00.000Z"}
10. Teraz Wypchnij zmiany do platformy Azure i przejdź do aplikacji w taki sposób, aby upewnić się, że nadal działa.

         git add .
         git commit -m "<your commit message>"
         git push azure master
         az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

11. Dostęp do aplikacji sieci web platformy Azure plan interfejsu API. Na przykład:

         http://<appname>.azurewebsites.net/mywidget/create

     Jeśli interfejs API zwraca nowy wpis innego, aplikacji sieci web platformy Azure jest rozmowie z bazy danych DB rozwiązania Cosmos (MongoDB).

## <a name="more-resources"></a>Więcej zasobów
* [Rozpoczynanie pracy z aplikacjami sieci web Node.js w usłudze Azure App Service](app-service-web-get-started-nodejs.md)
* [Using Node.js Modules with Azure applications (Używanie modułów Node.js z aplikacjami platformy Azure)](../nodejs-use-node-modules-azure-apps.md)
