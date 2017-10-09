---
title: "aaaNode.js aplikacji przy użyciu użyciu biblioteki Socket.io | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse użyciu biblioteki socket.io w aplikacji node.js hostowanej na platformie Azure."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 7f9435e0-7732-4aa1-a4df-ea0e894b847f
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 47c6c4a748938959315b880340f41f31faab4ea9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-chat-application-with-socketio-on-an-azure-cloud-service"></a>Tworzenie aplikacji czatu Node.js przy użyciu biblioteki Socket.IO w usłudze chmury Azure
Użyciu biblioteki Socket.IO zapewnia czasu rzeczywistego komunikacji między między serwerem środowiska node.js i klientami. W tym samouczku opisano za pośrednictwem obsługi gniazda. We/Wy na podstawie rozmów aplikacji na platformie Azure. Aby uzyskać więcej informacji o użyciu biblioteki Socket.IO, zobacz <http://socket.io/>.

Zrzut ekranu aplikacji hello ukończone znajduje się poniżej:

![Okno przeglądarki zawierające hello usługi hostowanej na platformie Azure][completed-app]  

## <a name="prerequisites"></a>Wymagania wstępne
Upewnij się, że hello następujące produkty i wersje to przykład Witaj pełną toosuccessfully zainstalowanych w tym artykule:

* Zainstalować program [Visual Studio](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx)
* Zainstalować środowisko [Node.js](https://nodejs.org/download/).
* Zainstaluj [2.7.10 wersji języka Python](https://www.python.org/)

## <a name="create-a-cloud-service-project"></a>Tworzenie projektu usługi w chmurze
Witaj następujące kroki tworzenia projektu usługi w chmurze hello obsługującym hello użyciu biblioteki Socket.IO aplikacji.

1. Z hello **Start Menu** lub **ekranu startowego**, wyszukaj **programu Windows PowerShell**. Na koniec kliknij prawym przyciskiem myszy **programu Windows PowerShell** i wybierz **Uruchom jako Administrator**.
   
    ![Ikona Azure PowerShell][powershell-menu]
2. Utwórz katalog o nazwie **c:\\węzła**. 
   
        PS C:\> md node
3. Zmień katalogi toohello **c:\\węzła** katalogu
   
        PS C:\> cd node
4. Wprowadź hello następujące polecenia toocreate nowego rozwiązania o nazwie **chatapp** i rolę procesu roboczego o nazwie **WorkerRole1**:
   
        PS C:\node> New-AzureServiceProject chatapp
        PS C:\Node> Add-AzureNodeWorkerRole
   
    Zostanie wyświetlony powitania po odpowiedzi:
   
    ![dane wyjściowe Hello hello nowy azureservice i Dodaj azurenodeworkerrolecmdlets](./media/cloud-services-nodejs-chat-app-socketio/socketio-1.png)

## <a name="download-hello-chat-example"></a>Pobierz hello przykład rozmowy
Dla tego projektu, użyjemy przykład Witaj rozmów z hello [repozytorium GitHub użyciu biblioteki Socket.IO]. Wykonaj poniższy przykład hello toodownload kroki hello i dodaj go projektu toohello, utworzonych wcześniej.

1. Utwórz lokalną kopię hello repozytorium używając hello **klonowania** przycisku. Można także użyć hello **ZIP** przycisk toodownload hello projektu.
   
   ![Wyświetlanie https://github.com/LearnBoost/socket.io/tree/master/examples/chat, ikoną hello ZIP pobrać wyróżniony oknie przeglądarki][chat-example-view]
2. Przejdź struktura katalogów hello hello lokalnego repozytorium, dopóki przyjeździe hello **przykłady\\rozmów** katalogu. Kopiuj zawartość tego katalogu toothe hello **C:\\węzła\\chatapp\\WorkerRole1** Katalog utworzony wcześniej.
   
   ![Explorer wyświetlanie zawartości hello przykłady hello\\wyodrębnione z archiwum hello katalogu rozmowy][chat-contents]
   
   Witaj zaznaczone elementy na powitania zrzucie ekranu pokazano powyżej są hello plików skopiowanych z hello **przykłady\\rozmów** katalogu
3. W hello **C:\\węzła\\chatapp\\WorkerRole1** katalogu, Usuń hello **server.js** pliku, a następnie zmień hello **app.js**pliku zbyt**server.js**. Spowoduje to usunięcie domyślnej hello **server.js** plik utworzony wcześniej przez hello **AzureNodeWorkerRole Dodaj** polecenia cmdlet i zastępuje go przy użyciu aplikacji hello plik hello przykład rozmowy.

### <a name="modify-serverjs-and-install-modules"></a>Modyfikowanie Server.js i zainstalować moduły
Przed testowania aplikacji hello w hello Azure emulator firma Microsoft wprowadzać niektórych drobne zmiany. Wykonaj hello następującego pliku server.js toothe kroki:

1. Otwórz hello **server.js** pliku w Visual Studio lub w dowolnym edytorze tekstów.
2. Znajdź hello **zależności modułu** sekcji początku hello server.js i zmienić hello wiersz zawierający **sio = require('.. //.. lib//Socket.IO ")** za**sio = require('socket.io')** w sposób przedstawiony poniżej:
   
       var express = require('express')
         , stylus = require('stylus')
         , nib = require('nib')
       //, sio = require('..//..//lib//socket.io'); //Original
         , sio = require('socket.io');                //Updated
         var port = process.env.PORT || 3000;         //Updated
3. Aplikacja hello tooensure nasłuchuje na porcie poprawne hello, Otwórz w Notatniku lub ulubionego edytora server.js, a następnie zmień następujący wiersz zastępując **3000** z **process.env.port** pokazany poniżej:
   
       //app.listen(3000, function () {            //Original
       app.listen(process.env.port, function () {  //Updated
         var addr = app.address();
         console.log('   app listening on http://' + addr.address + ':' + addr.port);
       });

Po zapisaniu zmian hello zbyt**server.js**, użyj hello następujące kroki, aby zainstalować wymagane moduły i przetestowanie aplikacji hello w emulatorze platformy Azure:

1. Przy użyciu **programu Azure PowerShell**, zmień katalogi toohello **C:\\węzła\\chatapp\\WorkerRole1** hello katalogu i użyj następującego polecenia tooinstall hello moduły wymagane przez tę aplikację:
   
       PS C:\node\chatapp\WorkerRole1> npm install
   
   Spowoduje to zainstalowanie modułów hello wymienionych w pliku package.json hello. Po zakończeniu wykonywania polecenia hello powinny być widoczne dane wyjściowe podobne toothe poniżej:
   
   ![dane wyjściowe Hello hello npm polecenie instalacji][The-output-of-the-npm-install-command]
2. Ponieważ w tym przykładzie pierwotnie część hello repozytorium GitHub użyciu biblioteki Socket.IO i bezpośrednie odwołanie do biblioteki użyciu biblioteki Socket.IO hello przez ścieżkę względną, użyciu biblioteki Socket.IO nie został przywołany w pliku package.json hello, więc trzeba zainstalować wysyłając hello następujące polecenie:
   
       PS C:\node\chatapp\WorkerRole1> npm install socket.io --save

### <a name="test-and-deploy"></a>Testowania i wdrażania
1. Uruchamianie emulatora hello wysyłając hello następujące polecenie:
   
       PS C:\node\chatapp\WorkerRole1> Start-AzureEmulator -Launch
   
   > [!NOTE]
   > Jeśli wystąpią problemy związane z uruchamianie emulatora, np.: Start AzureEmulator: Wystąpił nieoczekiwany błąd.  Szczegóły: Napotkano nieoczekiwany błąd hello komunikacji, System.ServiceModel.Channels.ServiceChannel, nie można użyć obiektu komunikacji, ponieważ jest w stanie Faulted hello.
   
      Zainstaluj ponownie AzureAuthoringTools v 2.7.1 i AzureComputeEmulator v 2.7 - upewnij się, że ta wersja jest zgodna.
   >
   >


2. Otwórz przeglądarkę i przejdź zbyt**http://127.0.0.1**.
3. Po otwarciu okna przeglądarki hello wprowadź pseudonim, a następnie naciśnij klawisz enter.
   Umożliwi wiadomości toopost jako określonych pseudonim. tootest funkcji wielu użytkowników, Otwórz dodatkowe okna przeglądarki przy użyciu tego samego adresu URL i wprowadź inny pseudonimy.
   
   ![Wyświetlanie wiadomości od użytkowników Użytkownik1 i Użytkownik2 dwa okna przeglądarki](./media/cloud-services-nodejs-chat-app-socketio/socketio-8.png)
4. Po testowania aplikacji hello Zatrzymaj emulatora hello następujące polecenie:
   
       PS C:\node\chatapp\WorkerRole1> Stop-AzureEmulator
5. tooAzure aplikacji hello toodeploy, użyj **Publish-AzureServiceProject** polecenia cmdlet. Na przykład:
   
       PS C:\node\chatapp\WorkerRole1> Publish-AzureServiceProject -ServiceName mychatapp -Location "East US" -Launch
   
   > [!IMPORTANT]
   > Można się toouse unikatową nazwę, w przeciwnym razie hello publikowania proces zakończy się niepowodzeniem. Po zakończeniu wdrożenia hello hello przeglądarki będzie Otwórz i przejdź toohello wdrożona usługa.
   > 
   > Jeśli zostanie wyświetlony błąd informujący o tym hello pod warunkiem, że nazwa subskrypcji nie istnieje w hello zaimportowany profil publikowania, musisz pobrać i zaimportować hello profil publikowania dla subskrypcji przed wdrożeniem tooAzure. Zobacz hello **wdrażanie tooAzure aplikacji hello** sekcji [tworzenia i wdrażania tooan aplikacji Node.js usługi w chmurze Azure](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)
   > 
   > 
   
   ![Okno przeglądarki zawierające hello usługi hostowanej na platformie Azure][completed-app]
   
   > [!NOTE]
   > Jeśli zostanie wyświetlony błąd informujący o tym hello pod warunkiem, że nazwa subskrypcji nie istnieje w hello zaimportowany profil publikowania, musisz pobrać i zaimportować hello profil publikowania dla subskrypcji przed wdrożeniem tooAzure. Zobacz hello **wdrażanie tooAzure aplikacji hello** sekcji [tworzenia i wdrażania tooan aplikacji Node.js usługi w chmurze Azure](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)
   > 
   > 

Aplikacja jest teraz uruchomiona na platformie Azure i możliwość przekazywania wiadomości między różnych klientów przy użyciu użyciu biblioteki Socket.IO.

> [!NOTE]
> Dla uproszczenia, w tym przykładzie jest ograniczona toochatting między toohello połączonych użytkowników tego samego wystąpienia. Oznacza to, że jeśli usługa w chmurze hello tworzy dwa wystąpienia roli procesu roboczego, użytkownicy będą mogli tylko toochat osobom połączone toohello tego samego wystąpienia roli procesu roboczego. tooscale hello toowork aplikacji z wielu wystąpień ról, można użyć technologii takich jak usługi Service Bus tooshare hello użyciu biblioteki Socket.IO przechowywanie stanu w wystąpieniach. Przykłady można znaleźć hello przykłady użycia tematów i kolejek usługi Service Bus w hello [zestawu Azure SDK dla repozytorium Node.js GitHub](https://github.com/WindowsAzure/azure-sdk-for-node).
> 
> 

## <a name="next-steps"></a>Następne kroki
W tym samouczku przedstawiono sposób toocreate aplikacji rozmów podstawowe hostowanej w usłudze w chmurze Azure. toolearn toohost tej aplikacji w witrynie internetowej platformy Azure, zobacz temat [tworzenie aplikacji czatu Node.js przy użyciu biblioteki Socket.IO w witrynie sieci Web Azure][chatwebsite].

Aby uzyskać więcej informacji, zobacz też hello [Centrum deweloperów środowiska Node.js](/develop/nodejs/).

[chatwebsite]: /develop/nodejs/tutorials/website-using-socketio/

[Azure SLA]: http://www.windowsazure.com/support/sla/
[Azure SDK for Node.js GitHub repository]: https://github.com/WindowsAzure/azure-sdk-for-node
[completed-app]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-10.png
[Azure SDK for Node.js]: https://www.windowsazure.com/develop/nodejs/
[Node.js Web Application]: https://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
[repozytorium GitHub użyciu biblioteki Socket.IO]: https://github.com/LearnBoost/socket.io/tree/0.9.14
[Azure Considerations]: #windowsazureconsiderations
[Hosting hello Chat Example in a Worker Role]: #hostingthechatexampleinawebrole
[Summary and Next Steps]: #summary
[powershell-menu]: ./media/cloud-services-nodejs-chat-app-socketio/azure-powershell-start.png

[chat example]: https://github.com/LearnBoost/socket.io/tree/master/examples/chat
[chat-example-view]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-22.png


[chat-contents]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-5.png
[The-output-of-the-npm-install-command]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-7.png
[hello output of hello Publish-AzureService command]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-9.png


