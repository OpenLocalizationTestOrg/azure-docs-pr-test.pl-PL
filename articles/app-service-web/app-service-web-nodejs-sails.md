---
title: "aaaDeploy Sails.js tooAzure aplikacji sieci web usługi App Service | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toodeploy aplikacji Node.js usługi Azure App Service. Ten samouczek pokazuje, jak jest toodeploy sails.js przy użyciu aplikacji sieci web."
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
ms.openlocfilehash: f5b2518b9c87c040845f7268763862be8c15e83e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-sailsjs-web-app-tooazure-app-service"></a>Wdrażanie Sails.js tooAzure aplikacji sieci web usługi aplikacji
W tym samouczku przedstawiono sposób toodeploy Sails.js tooAzure aplikację usługi aplikacji. W procesie hello można zgromadzonych niektórych ogólnej wiedzy na temat tooconfigure Twojego toorun aplikacji Node.js w usłudze App Service.

W tym miejscu dowiesz się, że przydatne umiejętności, takich jak:

* Konfigurowanie aplikacji Sails.js, uruchom w usłudze App Service.
* Wdróż tooApp aplikacji usługi z wiersza polecenia hello.
* Przeczytaj stderr i stdout tootroubleshoot dzienniki wszelkich problemów dotyczących wdrożenia.
* Przechowywanie zmiennych środowiskowych poza kontrolą źródła.
* Dostęp do zmiennych środowiskowych Azure z aplikacji.
* Połącz tooa bazy danych (bazy danych MongoDB).

Należy mieć praktyczną wiedzę o sails.js przy użyciu. W tym samouczku nie jest zamierzone toohelp toorunning Sail.js z problemów powiązanych ogólnie.

## <a name="cli-versions-toocomplete-hello-task"></a>Zadanie hello toocomplete wersje interfejsu wiersza polecenia

Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:

- [Azure CLI 1.0](app-service-web-nodejs-sails-cli-nodejs.md) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania modelami wdrażania
- [Azure CLI 2.0](app-service-web-nodejs-sails.md) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello

## <a name="prerequisites"></a>Wymagania wstępne
* [Node.js](https://nodejs.org/)
* [Sails.js](http://sailsjs.org/get-started)
* [Git](http://www.git-scm.com/downloads)
* [Interfejs wiersza polecenia platformy Azure 2.0](/cli/azure/install-az-cli2)
* Konto platformy Microsoft Azure. Jeśli nie masz konta, możesz [utworzyć konto bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) lub [aktywować korzyści dla subskrybentów programu Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).

> [!NOTE]
> Usługę [App Service](https://azure.microsoft.com/try/app-service/) możesz wypróbować, nie mając konta platformy Azure. Utwórz początkową aplikację i odtworzyć na temat godzinę tooan — bez karty kredytowej i bez zobowiązań.
> 
> 

## <a name="step-1-create-and-configure-a-sailsjs-app-locally"></a>Krok 1: Tworzenie i konfigurowanie sails.js przy użyciu aplikacji lokalnie
Po pierwsze szybko utworzyć domyślna aplikacja Sails.js w środowisku projektowania wykonaj następujące czynności:

1. Witaj Otwórz terminal wiersza polecenia dowolnego i `CD` tooa katalog roboczy.
2. Tworzenie aplikacji Sails.js i uruchom go:

        sails new <app_name>
        cd <app_name>
        sails lift

    Upewnij się, że można przechodzić toohello domyślną stronę główną w http://localhost:1377.

1. Następnie należy włączyć rejestrowanie dla platformy Azure. W katalogu głównym, Utwórz plik o nazwie `iisnode.yml` i Dodaj hello następujące dwa wiersze:

        loggingEnabled: true
        logDirectory: iisnode

    Włączono rejestrowanie dla hello [iisnode](https://github.com/tjanczuk/iisnode) serwera używany toorun aplikacji Node.js w usłudze Azure App Service. 
    Aby uzyskać więcej informacji o jego działaniu, zobacz [jak toodebug Node.js sieci web aplikacji w usłudze Azure App Service](web-sites-nodejs-debug.md).

2. Skonfiguruj hello sails.js przy użyciu aplikacji toouse środowiska platformy Azure zmiennych. Otwórz config/env/production.js tooconfigure środowiska produkcyjnego i ustaw `port` i `hookTimeout`:

        module.exports = {

            // Use process.env.port toohandle web requests toohello default HTTP port
            port: process.env.port,
            // Increase hooks timout too30 seconds
            // This avoids hello Sails.js error documented at https://github.com/balderdashy/sails/issues/2691
            hookTimeout: 30000,

            ...
        };

    Można znaleźć w dokumentacji tych ustawień konfiguracji w [dokumentacji Sails.js](http://sailsjs.org/documentation/reference/configuration/sails-config).

4. Następnie kodowania hello Node.js w wersji ma toouse. W pliku package.json, należy dodać następujące hello `engines` systemu właściwość tooset hello Node.js wersji tooone który chcemy.

        "engines": {
            "node": "6.9.1"
        },

5. Na koniec zainicjować repozytorium Git i przekazać pliki. W hello katalog główny aplikacji (pliku package.json przypadku), uruchom następujące polecenia usługi Git hello:

        git init
        git add .
        git commit -m "<your commit message>"

Kod jest gotowy toobe wdrożone. 

## <a name="step-2-create-an-azure-app-and-deploy-sailsjs"></a>Krok 2: Tworzenie aplikacji platformy Azure i wdrażanie Sails.js

Następnie utwórz hello zasobów usługi aplikacji na platformie Azure i wdrażanie Twojego Sails.js tooit aplikacji.

1. dziennik w tooAzure w następujący sposób:

        az login

    Wykonaj hello monitu toocontinue hello logowania w przeglądarce za pomocą konta Microsoft, które ma subskrypcji platformy Azure.

3. Ustaw hello użytkownika wdrożenia dla aplikacji usługi. Kod zostanie później wdrożony przy użyciu tych poświadczeń.
   
        az appservice web deployment user set --user-name <username> --password <password>

3. Utwórz [grupy zasobów](../azure-resource-manager/resource-group-overview.md) o nazwie. W tym samouczku środowiska Node.js nie naprawdę potrzebny tooknow co to jest.

        az group create --location "<location>" --name my-sailsjs-app-group

    toosee jakie możliwe wartości można użyć dla `<location>`, użyj hello `az appservice list-locations` polecenia interfejsu wiersza polecenia.

3. Tworzenie "Wolne" [planu usługi aplikacji](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) o nazwie. W tym samouczku środowiska Node.js wystarczy wiedzieć, że użytkownik nie zostanie obciążona dla aplikacji sieci web w tym planie.

        az appservice plan create --name my-sailsjs-appservice-plan --resource-group my-sailsjs-app-group --sku FREE

4. Utwórz nową aplikację sieci Web o unikatowej nazwie wprowadzonej w tagu `<app_name>`.

        az appservice web create --name <app_name> --resource-group my-sailsjs-app-group --plan my-sailsjs-appservice-plan

## <a name="step-3-configure-and-deploy-your-sailsjs-app"></a>Krok 3: Konfigurowanie i wdrażanie aplikacji Sails.js

1. Skonfigurować lokalne wdrożenie Git dla nowej aplikacji sieci web z hello następujące polecenie:

        az appservice web source-control config-local-git --name <app_name> --resource-group my-sailsjs-app-group

    Otrzymasz dane wyjściowe JSON podobny do tego, co oznacza, że skonfigurowano tego hello zdalnego repozytorium Git:

        {
        "url": "https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git"
        }

6. Dodaj adres URL hello w hello JSON jako zdalnego dla lokalnego repozytorium Git (nazywane `azure` dla uproszczenia).

        git remote add azure https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git
   
7. Wdrażanie programu przykładowy kod toohello `azure` zdalnego Git. Po wyświetleniu monitu użyj poświadczeń wdrożenia hello przez skonfigurowane wcześniej.

        git push azure master

7. Na koniec można uruchomić w przeglądarce hello działającą aplikację Azure:

        az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

    Powinien zostać wyświetlony hello tej samej stronie głównej Sails.js.

    ![](./media/app-service-web-nodejs-sails/sails-in-azure.png)

## <a name="troubleshoot-your-deployment"></a>Rozwiązywanie problemów z wdrożeniem
Jeśli zaistnieje w usłudze App Service sails.js przy użyciu aplikacji nie powiedzie się, Znajdź dzienniki stderr hello toohelp Rozwiązywanie problemów.
Aby uzyskać więcej informacji, zobacz [jak toodebug Node.js sieci web aplikacji w usłudze Azure App Service](web-sites-nodejs-debug.md).
Jeśli pomyślnie uruchomił aplikacji hello dziennika stdout hello powinny być widoczne należy zapoznać się wiadomość hello:

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
    toosee your app, visit http://localhost:\\.\pipe\c775303c-0ebc-4854-8ddd-2e280aabccac
    tooshut down Sails, press <CTRL> + C at any time.

Można kontrolować poziom szczegółowości dzienniki stdout hello w hello [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) pliku.

## <a name="connect-tooa-database-in-azure"></a>Połączenia bazy danych tooa na platformie Azure
Baza danych tooa tooconnect na platformie Azure, Utwórz bazę danych hello wybranym na platformie Azure, takich jak bazy danych SQL Azure, MySQL, bazy danych MongoDB, pamięć podręczna Azure (Redis), itp. i użyj odpowiadającego hello [karty magazyn danych](https://github.com/balderdashy/sails#compatibility) tooconnect tooit. Witaj kroki opisane w tej sekcji opisano sposób tooMongoDB tooconnect za pomocą [bazy danych Azure rozwiązania Cosmos](../documentdb/documentdb-protocol-mongodb.md) bazy danych, który może obsługiwać połączeń klienckich bazy danych MongoDB.

1. [Tworzenie konta bazy danych rozwiązania Cosmos z obsługą protokołu bazy danych MongoDB](../documentdb/documentdb-create-mongodb-account.md).
2. [Tworzenie kolekcji rozwiązania Cosmos bazy danych i bazy danych](../documentdb/documentdb-create-collection.md). Nazwa Hello hello kolekcji nie ma znaczenia, ale należy hello nazwa hello bazy danych, podczas łączenia z Sails.js.
3. [Znajdź informacje o połączeniu hello bazy danych DB rozwiązania Cosmos](../cosmos-db/connect-mongodb-account.md#GetCustomConnection).
2. Z wiersza polecenia terminalu Zainstaluj hello bazy danych MongoDB karty:

        npm install sails-mongo --save

3. Otwórz config/connections.js i Dodaj powitania po liście toohello obiektu połączenia:

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
    > Witaj `ssl: true` opcji ważne jest, ponieważ [DB rozwiązania Cosmos wymaga](../cosmos-db/connect-mongodb-account.md#connection-string-requirements). 
    >
    >

4. Dla każdej zmiennej środowiskowej (`process.env.*`), należy tooset go w usłudze App Service. toodo tego hello uruchom następujące polecenia z terminala. Użyj informacji o połączeniu hello Twojego rozwiązania Cosmos bazy danych.

        az appservice web config appsettings update --settings dbuser="<database user>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbpassword="<database password>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbhost="<database hostname>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbport="<database port>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbname="<database name>" --name <app_name> --resource-group my-sailsjs-app-group

    Wprowadzanie ustawień w ustawieniach aplikacji Azure chroni poufne dane poza do kontroli źródła (Git). Następnie należy skonfigurować programowania toouse środowiska hello tych samych informacji połączenia.
5. Otwórz config/local.js i Dodaj powitania od obiektu połączenia:

        connections: {
            docDbMongo: {
                user: "<database user>",
                password: "<database password>",
                host: "<database hostname>",
                database: "<database name>",
                ssl: true
            },
        },

    Ta konfiguracja zastępuje ustawienia hello w pliku config/connections.js hello środowiska lokalnego. Ten plik jest wykluczone przez hello domyślne .gitignore w projekcie, dlatego nie można zapisać w usłudze Git. Teraz jesteś stanie tooconnect tooyour rozwiązania Cosmos bazy danych (bazy danych MongoDB) w bazie danych zarówno z aplikacji sieci web platformy Azure i środowiska deweloperskiego lokalnego.
6. Otwórz config/env/production.js tooconfigure środowiska produkcyjnego i dodaj następujące hello `models` obiektu:

        models: {
            connection: 'docDbMongo',
            migrate: 'safe'
        },
7. Otwórz config/env/development.js tooconfigure środowiska projektowego i dodaj następujące hello `models` obiektu:

        models: {
            connection: 'docDbMongo',
            migrate: 'alter'
        },

    `migrate: 'alter'`pozwala używać toocreate funkcji migracji bazy danych i łatwo aktualizować kolekcje bazy danych lub tabel. Jednak `migrate: 'safe'` służy do środowiska Azure (środowisko produkcyjne), ponieważ Sails.js pozwalają toouse `migrate: 'alter'` w środowisku produkcyjnym (zobacz [dokumentacji Sails.js](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings)).
8. Z hello terminali [Generowanie](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) Sails.js [plan interfejsu API](http://sailsjs.org/documentation/concepts/blueprints) tak jak zwykle następnie należy uruchomić `sails lift` do tworzenia bazy danych hello sails.js przy użyciu bazy danych migracji. Na przykład:

         sails generate api mywidget
         sails lift

    Witaj `mywidget` modelu wygenerowanym przez to polecenie jest pusty, ale firma Microsoft może być używany tooshow, że istnieje łączność z bazą danych.
    Po uruchomieniu `sails lift`, tworzy hello Brak kolekcje i tabel dla hello modele używany przez aplikację.
9. Interfejs API hello plan utworzony w przeglądarce hello. Na przykład:

        http://localhost:1337/mywidget/create

    Witaj interfejsu API powinien zwrócić tooyou wstecz hello utworzony wpis w oknie przeglądarki hello, co oznacza, że pomyślnie utworzono kolekcję.

        {"id":1,"createdAt":"2016-09-23T13:32:00.000Z","updatedAt":"2016-09-23T13:32:00.000Z"}
10. Teraz push tooAzure Twoje zmiany i Przeglądaj toomake aplikacji tooyour się, że nadal działa.

         git add .
         git commit -m "<your commit message>"
         git push azure master
         az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

11. Hello plan interfejsu API dostępu do aplikacji sieci web platformy Azure. Na przykład:

         http://<appname>.azurewebsites.net/mywidget/create

     Jeśli hello interfejsu API zwraca nowy wpis innego, aplikacji sieci web platformy Azure rozmawia tooyour rozwiązania Cosmos bazy danych (bazy danych MongoDB) w bazie danych.

## <a name="more-resources"></a>Więcej zasobów
* [Rozpoczynanie pracy z aplikacjami sieci web Node.js w usłudze Azure App Service](app-service-web-get-started-nodejs.md)
* [Using Node.js Modules with Azure applications (Używanie modułów Node.js z aplikacjami platformy Azure)](../nodejs-use-node-modules-azure-apps.md)
