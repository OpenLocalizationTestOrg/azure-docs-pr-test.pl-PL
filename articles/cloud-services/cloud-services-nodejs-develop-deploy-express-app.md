---
title: "aaaWeb aplikacji za pomocą Express (Node.js) | Dokumentacja firmy Microsoft"
description: "Samouczek, który jest oparty na samouczek usługi chmury hello i pokazuje, jak toouse hello modułu Express."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 24f8e7ef-e90d-4554-9b1e-a9b31d5824e5
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 91921bfbe137eeca9a110d4cb18eb57b46b0060e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-web-application-using-express-on-an-azure-cloud-service"></a>Tworzenie aplikacji sieci web Node.js za pomocą ekspresowego na usługi w chmurze platformy Azure
Node.js zawiera minimalny zestaw funkcji w hello podstawowego środowiska wykonawczego.
Deweloperzy często używają 3 strona modułów tooprovide dodatkowe funkcje, podczas opracowywania aplikacji Node.js. W tym samouczku utworzysz nową aplikację przy użyciu hello [Express] [ Express] moduł, który zapewnia platformę MVC do tworzenia aplikacji sieci web Node.js.

Zrzut ekranu aplikacji hello ukończone znajduje się poniżej:

![Przeglądarka wyświetlająca powitalnej tooExpress na platformie Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="create-a-cloud-service-project"></a>Tworzenie projektu usługi w chmurze
[!INCLUDE [install-dev-tools](../../includes/install-dev-tools.md)]

Wykonaj następujące hello toocreate czynności nowy projekt usługi w chmurze o nazwie "expressapp":

1. Z hello **Start Menu** lub **ekranu startowego**, wyszukaj **programu Windows PowerShell**. Na koniec kliknij prawym przyciskiem myszy **programu Windows PowerShell** i wybierz **Uruchom jako Administrator**.
   
    ![Ikona Azure PowerShell](./media/cloud-services-nodejs-develop-deploy-express-app/azure-powershell-start.png)
2. Zmień katalogi toohello **c:\\węzła** katalogu, a następnie wprowadź hello następujące polecenia toocreate nowego rozwiązania o nazwie **expressapp** i rolę sieci web o nazwie **WebRole1** :
   
        PS C:\node> New-AzureServiceProject expressapp
        PS C:\Node\expressapp> Add-AzureNodeWebRole
        PS C:\Node\expressapp> Set-AzureServiceProjectRole WebRole1 Node 0.10.21
   
    > [!NOTE]
    > Domyślnie **Add-AzureNodeWebRole** używa starszej wersji środowiska node.js. Witaj **AzureServiceProjectRole zestaw** v0.10.21 Azure toouse węzła nakazuje powyższych instrukcji.  Należy zauważyć, że parametry hello jest rozróżniana wielkość liter.  Możesz sprawdzić hello poprawną wersję środowiska Node.js została wybrana sprawdzając hello **aparaty** właściwości w **WebRole1\package.json**.
    > 
    > 

## <a name="install-express"></a>Zainstaluj Express
1. Zainstaluj generator aplikacji Express hello wysyłając hello następujące polecenie:
   
        PS C:\node\expressapp> npm install express-generator -g
   
    dane wyjściowe Hello hello npm polecenia powinny wyglądać podobnie wynik toohello poniżej. 
   
    ![Programu Windows PowerShell wyświetlania hello dane wyjściowe programu hello npm instalacji ekspresowej polecenia.](./media/cloud-services-nodejs-develop-deploy-express-app/express-g.png)
2. Zmień katalogi toohello **WebRole1** hello katalogu i użyj polecenia express toogenerate nowej aplikacji:
   
        PS C:\node\expressapp\WebRole1> express
   
    Użytkownik będzie zostanie wyświetlony monit o toooverwrite starszych aplikacji. Wprowadź **y** lub **tak** toocontinue. Express spowoduje wygenerowanie pliku app.js hello i struktury folderów, do tworzenia aplikacji.
   
    ![Witaj dane wyjściowe polecenia express hello](./media/cloud-services-nodejs-develop-deploy-express-app/node23.png)
3. dodatkowe zależności tooinstall zdefiniowane w pliku package.json hello, wprowadź następujące polecenie hello:
   
       PS C:\node\expressapp\WebRole1> npm install
   
   ![dane wyjściowe Hello hello npm polecenie instalacji](./media/cloud-services-nodejs-develop-deploy-express-app/node26.png)
4. Użyj hello następujące polecenie toocopy hello **bin/www** pliku zbyt**server.js**. Jest to tak hello usługi w chmurze można znaleźć punktu wejścia powitania dla tej aplikacji.
   
       PS C:\node\expressapp\WebRole1> copy bin/www server.js
   
   Po wykonaniu tego polecenia, powinien mieć **server.js** pliku w katalogu hello WebRole1.
5. Modyfikowanie hello **server.js** tooremove jedną hello "." znaki z hello następującego wiersza.
   
       var app = require('../app');
   
   Po wprowadzeniu tej zmiany należy wiersz hello powinna wyglądać następująco.
   
       var app = require('./app');
   
   Ta zmiana jest wymagana, ponieważ przenieśliśmy hello pliku (dawniej **bin/www**,) toohello tym samym katalogu co plik aplikacji hello jest wymagane. Po wprowadzeniu tej zmiany należy zapisać hello **server.js** pliku.
6. Użyj następującego polecenia toorun hello aplikacji hello Azure emulator hello:
   
       PS C:\node\expressapp\WebRole1> Start-AzureEmulator -launch
   
    ![Strony sieci web zawierającej tooexpress powitalnej.](./media/cloud-services-nodejs-develop-deploy-express-app/node28.png)

## <a name="modifying-hello-view"></a>Modyfikowanie hello widoku
Teraz zmodyfikuj wiadomości powitania toodisplay widoku hello "Zapraszamy tooExpress na platformie Azure".

1. Wprowadź poniższe polecenie tooopen hello index.jade plik hello:
   
       PS C:\node\expressapp\WebRole1> notepad views/index.jade
   
   ![zawartość Hello hello index.jade pliku.](./media/cloud-services-nodejs-develop-deploy-express-app/getting-started-19.png)
   
   Jade jest hello domyślny aparat widoku używany przez aplikacje Express. Aby uzyskać więcej informacji na powitania aparatu Jade widoku, zobacz [http://jade-lang.com][http://jade-lang.com].
2. Modyfikowanie hello ostatni wiersz tekstu przez dołączenie **na platformie Azure**.
   
   ![odczytuje hello ostatni wiersz pliku index.jade Hello: p Witamy zbyt\#{nazwa} na platformie Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node31.png)
3. Zapisz plik hello i Zakończ działanie Notatnika.
4. Odśwież przeglądarkę i zobaczą zmiany.
   
   ![Okno przeglądarki, strona hello zawiera powitalnej tooExpress na platformie Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node32.png)

Po testowania aplikacji hello, użyj hello **Stop AzureEmulator** emulatora hello toostop polecenia cmdlet.

## <a name="publishing-hello-application-tooazure"></a>Publikowanie tooAzure aplikacji hello
W oknie programu PowerShell Azure hello, użyj hello **Publish-AzureServiceProject** usługi chmury tooa aplikacji hello toodeploy polecenia cmdlet

    PS C:\node\expressapp\WebRole1> Publish-AzureServiceProject -ServiceName myexpressapp -Location "East US" -Launch

Po zakończeniu operacji wdrażania hello przeglądarki otworzyć i wyświetlić stronę sieci web hello.

![Przeglądarka wyświetlająca stronę Express hello. adres URL Hello wskazuje, że jest ona obecnie hostowana na platformie Azure.](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji, zobacz hello [Centrum deweloperów środowiska Node.js](/develop/nodejs/).

[Node.js Web Application]: http://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
[Express]: http://expressjs.com/
[http://jade-lang.com]: http://jade-lang.com


