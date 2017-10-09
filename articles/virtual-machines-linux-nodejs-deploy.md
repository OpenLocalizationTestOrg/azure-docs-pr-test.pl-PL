---
title: aaaDeploy tooLinux aplikacji Node.js maszyn wirtualnych na platformie Azure
description: "Dowiedz się, jak toodeploy Node.js maszyn wirtualnych tooLinux aplikacji na platformie Azure."
services: 
documentationcenter: nodejs
author: stepro
manager: dmitryr
editor: 
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: /azure
ms.assetid: 857a812d-c73e-4af7-a985-2d0baf8b6f71
ms.service: multiple
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2016
ms.author: stephpr
ms.openlocfilehash: e876c8170a06f102f7f32ec7cb930b876647a707
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-nodejs-application-toolinux-virtual-machines-in-azure"></a>Wdrażanie tooLinux aplikacji Node.js maszyn wirtualnych na platformie Azure
Ten samouczek pokazuje, jak tootake aplikacji Node.js i wdróż je tooLinux maszyn wirtualnych działających na platformie Azure. Witaj instrukcje w tym samouczku można wykonać w dowolnym systemie operacyjnym, który jest w stanie uruchomić środowisko Node.js.

Dowiesz się, jak:

* Rozwidlenia i klonowania repozytorium GitHub zawierające prostej aplikacji TODO;
* Tworzenie i konfigurowanie aplikacji hello Azure toorun; dwóch maszyn wirtualnych systemu Linux
* Iterowanie w aplikacji hello przesyłając maszyny wirtualnej frontonu sieci web toohello aktualizacji.

> [!NOTE]
> toocomplete tego samouczka wymagane konto usługi GitHub i konto Microsoft Azure i hello możliwości toouse Git z komputerze deweloperskim.
> 
> Jeśli nie masz konto GitHub, można założyć [tutaj](https://github.com/join).
> 
> Jeśli nie masz [Microsoft Azure](https://azure.microsoft.com/) konta, można założyć bezpłatnej wersji próbnej [tutaj](https://azure.microsoft.com/pricing/free-trial/). To również przeprowadzi Cię przez proces dla tworzenia konta hello [Account Microsoft](http://account.microsoft.com) Jeśli użytkownik nie ma jeszcze jednej. W przypadku subskrybentów programu Visual Studio można też [Aktywuj swoje korzyści MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).
> 
> Jeśli nie masz git na komputerze deweloperskim, to jeśli używasz komputera Macintosh lub Windows zainstaluj z usługi git [tutaj](http://www.git-scm.com). Jeśli używasz systemu Linux, zainstaluj usługę git przy użyciu mechanizmu hello najbardziej odpowiednie dla Ciebie, takich jak `sudo apt-get install git`.
> 
> 

## <a name="forking-and-cloning-hello-todo-application"></a>Rozwidlania i klonowania hello aplikacji TODO
Hello aplikacji TODO, w tym samouczku implementuje frontonu sieci web prostego przez wystąpienie bazy danych MongoDB, który śledzi lista czynności do wykonania. Po zalogowaniu tooGitHub Przejdź [tutaj](https://github.com/stepro/node-todo) toofind hello aplikacji i rozwidlania przy użyciu łącza hello w hello w prawym górnym narożniku. Ten należy utworzyć repozytorium na koncie o nazwie *accountname*/node-todo.

Teraz na komputerze deweloperskim Klonuj to repozytorium:

    git clone https://github.com/accountname/node-todo.git

Użyjemy tego klonu lokalnego repozytorium hello nieco później podczas wprowadzania zmian w kodzie źródłowym toohello.

## <a name="creating-and-configuring-hello-linux-virtual-machines"></a>Tworzenie i konfigurowanie hello maszyn wirtualnych systemu Linux
Platforma Azure ma doskonałą pomoc techniczną dla nieprzetworzonej obliczeń przy użyciu maszyn wirtualnych systemu Linux. Ta część hello samouczek pokazuje, jak można łatwo aż dwóch maszyn wirtualnych systemu Linux i wdrożyć toothem aplikacji hello TODO, systemem hello frontonu sieci web na jednym i hello wystąpienie bazy danych MongoDB na powitania innych.

### <a name="creating-virtual-machines"></a>Tworzenie maszyn wirtualnych
Witaj najprostszy sposób toocreate nowej maszyny wirtualnej na platformie Azure jest hello toouse portalu Azure. Kliknij przycisk [tutaj](https://portal.azure.com) toosign w, a następnie uruchom hello portalu Azure w przeglądarce sieci web. Po załadowaniu hello portalu Azure, wykonaj następujące kroki hello:

* Kliknij przycisk hello "+ nowy" link;
* Wybierz kategorię "Obliczeniowe" hello, a następnie wybierz pozycję "Ubuntu Server 14.04 LTS";
* Wybierz model wdrażania "Resource Manager" hello, a następnie kliknij przycisk "Utwórz";
* Wypełnij podstawy hello poniższych wskazówek:
  * Określ nazwę, którą można było później łatwo rozpoznać;
  * W tym samouczku wybierz uwierzytelnianie hasła;
  * Utwórz nową grupę zasobów o nazwie do zidentyfikowania.
* Hello rozmiar maszyny wirtualnej "A1 Standard" jest uzasadnione wybór dla tego samouczka.
* Dodatkowe ustawienia upewnij się, że "Standard" hello, typ dysku i zaakceptować hello wszystkie pozostałe wartości domyślne.
* Rozpocząć poza tworzenia hello na stronie podsumowania hello.

Wykonaj powyższe hello przetwarzania dwukrotnie toocreate dwóch maszyn wirtualnych systemu Linux, jeden dla hello frontonu sieci web i jeden dla hello wystąpienie bazy danych MongoDB. Tworzenie maszyn wirtualnych hello potrwa około 5 – 10 minut.

### <a name="assigning-a-dns-entry-for-virtual-machines"></a>Przypisywanie wpis DNS dla maszyn wirtualnych
Maszyny wirtualne utworzone na platformie Azure są domyślnie dostępne tylko za pośrednictwem publicznego adresu IP, takich jak 1.2.3.4. Upewnijmy maszyny hello identyfikacji przez przypisywanie ich wpisy DNS.

Po portalu hello wskazuje, czy hello maszyny wirtualnej zostały utworzone, kliknij łącze "Maszyny wirtualnej" hello w lewy pasek nawigacyjny hello, a następnie zlokalizuj maszynach. Dla każdego komputera:

* Karta Essentials hello zlokalizuj i kliknij pozycję hello publicznego adresu IP;
* W hello publiczny adres IP należy przypisać etykieta nazwy DNS i Zapisz.

Hello portal będzie upewnij się, czy nazwa hello przez użytkownika jest dostępna. Po zapisaniu konfiguracji hello, maszyn wirtualnych będą mieć nazwy hosta, które są podobne zbyt`machinename.region.cloudapp.azure.com`.

### <a name="connecting-toohello-virtual-machines"></a>Łączenie toohello maszyny wirtualne
Gdy udostępnionych maszynach wirtualnych, były tooallow wstępnie skonfigurowane zdalne połączenia za pomocą protokołu SSH. Jest to mechanizm hello będziemy używać maszyn wirtualnych hello tooconfigure. Jeśli używasz systemu Windows na komputerze, należy tooget klienta SSH, jeśli użytkownik nie ma jeszcze jednej. Programu PuTTY, który można pobrać z jest tutaj wspólnej wybór [tutaj](http://www.chiark.greenend.org.uk/~sgtatham/putty/). Przy użyciu wersji SSH preinstalowanym pochodzą Macintosh i systemów operacyjnych Linux.

### <a name="configuring-hello-web-frontend-virtual-machine"></a>Konfigurowanie hello maszyny wirtualnej frontonu sieci Web
Maszyna frontonu sieci web toohello SSH utworzonych przy użyciu programu PuTTY, ssh wiersza polecenia lub innych ulubionego narzędzia SSH. Powinien zostać wyświetlony komunikat powitalny, a następnie w wierszu polecenia.

Po pierwsze upewnijmy się, że git i węzła zainstalowano:

    sudo apt-get install -y git
    curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
    sudo apt-get install -y nodejs

Ponieważ frontonu sieci web aplikacji hello opiera się na niektórych modułów macierzystych Node.js, potrzebujemy również tooinstall hello niezbędny zestaw narzędzi kompilacji:

    sudo apt-get install -y build-essential

Na koniec zainstalujmy aplikację Node.js o nazwie *nieskończona*, co pozwala aplikacji serwerowych toorun Node.js:

    sudo npm install -g forever

Są to wszystkie zależności hello na tej maszyny wirtualnej toobe toorun stanie hello aplikacji frontonu sieci web, więc korzystaj z systemem. toodo, najpierw utworzymy systemu od zera klonowania repozytorium GitHub hello wcześniej rozwidlone tak, aby łatwo opublikować maszyny wirtualnej toohello aktualizacji (omówione zostaną następujące czynności w tym scenariuszu aktualizacji później), a następnie sklonować tooprovide systemu od zera klonowania hello wersji hello repozytorium, który faktycznie może zostać wykonany.

Począwszy od hello katalog macierzysty (~), uruchom następujące polecenia hello (zastępowanie *accountname* z nazwą konta użytkownika usługi GitHub):

    git clone --bare https://github.com/accountname/node-todo.git
    git clone node-todo.git

Teraz wprowadź hello todo węzeł katalog i uruchom następujące polecenia:

    npm install
    forever start server.js

Witaj aplikacji frontonu sieci web jest teraz uruchomiona, jednak jest jeden krok w celu uzyskania dostępu do aplikacji hello z przeglądarki sieci web. Witaj tworzenia maszyny wirtualnej jest chroniony przez zasobów platformy Azure o nazwie *grupy zabezpieczeń sieci*, który został utworzony dla hello podczas aprowizowanej maszyny wirtualnej. Obecnie ten zasób umożliwia zewnętrznych żądań tooport 22 toobe kierowane toohello maszynę wirtualną, która umożliwia komunikacji SSH z hello maszyny, ale nic. Dlatego w kolejności tooview hello aplikacji TODO, które są skonfigurowane toorun portu 8080, ten port musi także toobe otwarte.

Zwraca toohello portalu Azure i ukończyć powitalnych następujące kroki:

* Kliknij pozycję "Grupy zasobów" hello lewy pasek nawigacyjny;
* Wybierz grupę zasobów hello, który zawiera maszyny wirtualnej;
* Hello wynikowej listy zasobów wybierz grupę zabezpieczeń sieci hello (hello jedną z ikona tarczy);
* W oknie dialogowym właściwości hello wybierz "zasady zabezpieczeń dla ruchu przychodzącego";
* Witaj pasku narzędzi kliknij przycisk "Dodaj";
* Podaj nazwę, takich jak "domyślny — Zezwalaj todo";
* Ustawienie zbyt protokołu hello "TCP";
* Ustaw zakres portów docelowych hello zbyt "8080";
* Kliknij przycisk OK i poczekaj, aż toobe reguły zabezpieczeń hello utworzony.

Po utworzeniu tej reguły zabezpieczeń, jest publicznie widoczna na powitania TODO aplikacji hello internet i możesz przeglądać tooit, takich jak na przykład przy użyciu adresu URL:

    http://machinename.region.cloudapp.azure.com:8080

Można zauważyć, że mimo że firma Microsoft nie skonfigurował jeszcze maszyny wirtualnej bazy danych MongoDB hello, hello aplikacji TODO pojawia się toobe dość funkcjonalności. Jest to spowodowane repozytorium źródłowe hello jest zapisane na stałe toouse wstępnie wdrożone wystąpienie bazy danych MongoDB. Po skonfigurowaliśmy maszyny wirtualnej bazy danych MongoDB hello, firma Microsoft będzie Przejdź wstecz i zmień tooutilize kodu źródłowego hello, naszych prywatnej wystąpienie bazy danych MongoDB zamiast tego.

### <a name="configuring-hello-mongodb-virtual-machine"></a>Konfigurowanie hello maszyny wirtualnej bazy danych MongoDB
SSH toohello drugiej maszyny utworzonych przy użyciu programu PuTTY, ssh wiersza polecenia lub innych ulubionego narzędzia SSH. Po przejrzeniu powitalna wiadomość hello i wiersz polecenia, należy zainstalować bazy danych MongoDB (instrukcje te zostały pobrane z [tutaj](https://docs.mongodb.org/master/tutorial/install-mongodb-on-ubuntu/)):

    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
    echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
    sudo apt-get update
    sudo apt-get install -y mongodb-org

Domyślnie bazy danych MongoDB jest skonfigurowany tak go można uzyskać tylko lokalnie. W tym samouczku firma Microsoft będzie Konfigurowanie bazy danych MongoDB są dostępne z aplikacji hello maszyny wirtualnej. W kontekście sudo, otwórz plik /etc/mongod.conf hello i Znajdź hello `# network interfaces` sekcji. Zmień hello `net.bindIp` konfiguracji wartość zbyt`0.0.0.0`.

> [!NOTE]
> Ta konfiguracja służy do celów hello tylko tego samouczka. Jest **nie** zalecane rozwiązanie w zakresie zabezpieczeń i nie powinna być używana w środowisku produkcyjnym.
> 
> 

Teraz upewnij się, hello bazy danych MongoDB usługa została uruchomiona:

    sudo service mongod restart

Bazy danych MongoDB działa za pośrednictwem portu 27017 domyślnie. Dlatego w hello taki sam sposób, że firma potrzebuje tooopen portu 8080 na maszynie wirtualnej frontonu sieci web hello, potrzebujemy portu tooopen 27017 na maszynie wirtualnej hello bazy danych MongoDB.

Zwraca toohello portalu Azure i ukończyć powitalnych następujące kroki:

* Kliknij pozycję "Grupy zasobów" hello lewy pasek nawigacyjny;
* Wybierz grupę zasobów hello, który zawiera maszyny wirtualnej bazy danych MongoDB hello;
* Hello wynikowej listy zasobów wybierz grupę zabezpieczeń sieci hello (hello jedną z ikona tarczy) z hello sama nazwa nadanym dla maszyny wirtualnej bazy danych MongoDB toohello;
* W oknie dialogowym właściwości hello wybierz "zasady zabezpieczeń dla ruchu przychodzącego";
* Witaj pasku narzędzi kliknij przycisk "Dodaj";
* Podaj nazwę, takich jak "domyślny — Zezwalaj mongo";
* Ustawienie zbyt protokołu hello "TCP";
* Ustaw zakres portów docelowych hello zbyt "27017";
* Kliknij przycisk OK i poczekaj, aż toobe reguły zabezpieczeń hello utworzony.

## <a name="iterating-on-hello-todo-application"></a>Iteracja na powitania aplikacji TODO
Do tej pory uprzednim udostępnieniu dwóch maszyn wirtualnych systemu Linux:, który jest uruchomiony hello aplikacji frontonu sieci web, a drugi działa wystąpienie bazy danych MongoDB. Ale występuje problem — frontonu sieci web hello faktycznie nie używa wystąpienie bazy danych MongoDB hello elastycznie jeszcze. Załóżmy rozwiązać ten problem, aktualizując toouse kod frontonu sieci web hello zmienną środowiskową zamiast wystąpieniem ustalony.

### <a name="changing-hello-todo-application"></a>Zmiana hello aplikacji TODO
Na komputerze deweloperskim, gdzie najpierw sklonować repozytorium todo węzła hello, otwórz hello `node-todo/config/database.js` plik w edytorze ulubionych i zmień wartość adresu url hello z hello ustalony wartości podobnie jak `mongodb://...` zbyt`process.env.MONGODB`.

Zatwierdź zmiany i Wypchnij toohello GitHub głównego:

    git commit -am "Get MongoDB instance from env"
    git push origin master

Niestety to nie publikuje maszyny wirtualnej frontonu sieci web toohello hello zmiany. Można wprowadzić kilka więcej tooenable maszyny wirtualnej toothat zmiany prostą, ale efektywny mechanizm publikowania aktualizacji, można szybko obserwować wpływ hello hello zmian w środowisku produkcyjnym hello.

### <a name="configuring-hello-web-frontend-virtual-machine"></a>Konfigurowanie hello maszyny wirtualnej frontonu sieci Web
Odwołaj możemy wcześniej utworzona bez systemu operacyjnego klonowania repozytorium todo węzła hello na maszynie wirtualnej frontonu sieci web hello. Okaże się utworzenia nowego Git, może zostać umieszczony zdalnego toowhich zmiany tej akcji. Jednak po prostu wypychanie zdalnego toothis dość nie zapewnia hello szybkie iteracji modelu, który szukasz deweloperzy podczas pracy na ich kodu.

Co mamy ma toobe toodo możliwe jest upewnij się, że w przypadku wypychania toohello zdalnego repozytorium na maszynie wirtualnej hello działającej aplikacji TODO hello jest automatycznie aktualizowany. Na szczęście to łatwe tooachieve za pomocą narzędzia git.

Git eksponuje pewną liczbę punkty zaczepienia wywoływanych w podejmowaną w odniesieniu do repozytorium hello tooactions tooreact określonego czasu. Są one określone przy użyciu skryptów powłoki w repozytorium hello `hooks` folderu. hak Hello, który jest najbardziej odpowiednie dla scenariusza automatycznej aktualizacji hello jest hello `post-update` zdarzeń.

W SSH sesji toohello sieci web frontonu maszynę wirtualną, zmień toohello `~/node-todo.git/hooks` katalogu i Dodaj powitania po tooa zawartości pliku o nazwie `post-update` (zastępowanie `machinename` i `region` z informacjami o MongoDB maszyny wirtualnej):

    #!/bin/bash

    forever stopall
    unset 'GIT_DIR'
    export MONGODB="mongodb://machinename.region.cloudapp.azure.com:27017/tododb"
    cd ~/node-todo && git fetch origin && git pull origin master && npm install && forever start ~/node-todo/server.js
    exec git update-server-info

Upewnij się, że ten plik wykonywalny, uruchamiając następujące polecenie hello:

    chmod 755 post-update

Ten skrypt temu hello bieżącego serwera aplikacji jest zatrzymana, kod hello w hello sklonowanego repozytorium jest zaktualizowane toohello najnowsza wersja, wszelkie zaktualizowane zależności i ponownego uruchomienia serwera hello. Gwarantuje również, że środowisko to hello został skonfigurowany w ramach przygotowania do odbierania naszym pierwszym aplikacji aktualizacji tooget hello wystąpienie bazy danych MongoDB z zmiennej środowiskowej.

### <a name="configuring-your-development-machine"></a>Konfigurowanie na komputerze deweloperskim
Teraz Zaloguj się na komputerze deweloperskim podłączonymi maszyny wirtualnej frontonu sieci web toohello. Jest tak proste, jak dodawanie hello repozytorium bez systemu operacyjnego na maszynie wirtualnej hello jako zdalnej. Uruchom następujące polecenie toodo hello to (zastępowanie *użytkownika* nazwą logowania użytkownika sieci web frontonu maszyny wirtualnej i *machinename* i *region* jako odpowiednie):

    git remote add azure user@machinename.region.cloudapp.azure.com:node-todo.git

To są wszystkie wymagane tooenable wypychanie lub w celu publikowania, maszyna wirtualna frontonu sieci web toohello zmiany.

### <a name="publishing-updates"></a>Publikowanie aktualizacji
Umożliwia publikowanie hello jednej zmiany się do tej pory tak, aby aplikacja hello będzie korzystać z własnej wystąpienie bazy danych MongoDB:

    git push azure master

Powinny pojawić się dane wyjściowe podobne toothis:

    Counting objects: 4, done.
    Delta compression using up too4 threads.
    Compressing objects: 100% (3/3), done.
    Writing objects: 100% (4/4), 406 bytes | 0 bytes/s, done.
    Total 4 (delta 1), reused 0 (delta 0)
    remote: info:    Forever stopped processes:
    remote: data:        uid  command         script    forever pid  id logfile                         uptime
    remote: data:    [0] 0Lyh /usr/bin/nodejs server.js 9064    9301    /home/username/.forever/0Lyh.log 0:0:3:17.487
    remote: From /home/username/node-todo
    remote:    5f31fd7..5bc7be5  master     -> origin/master
    remote: From /home/username/node-todo
    remote:  * branch            master     -> FETCH_HEAD
    remote: Updating 5f31fd7..5bc7be5
    remote: Fast-forward
    remote:  config/database.js | 2 +-
    remote:  1 file changed, 1 insertion(+), 1 deletion(-)
    remote: npm WARN package.json node-todo@0.0.0 No repository field.
    remote: npm WARN package.json node-todo@0.0.0 No license field.
    remote: warn:    --minUptime not set. Defaulting to: 1000ms
    remote: warn:    --spinSleepTime not set. Your script will exit if it does not stay up for at least 1000ms
    remote: info:    Forever processing file: /home/username/node-todo/server.js
    toousername@machinename.region.cloudapp.azure.com:node-todo.git
    5f31fd7..5bc7be5  master -> master

Po wykonaniu tego polecenia, spróbuj odświeżyć aplikacji hello w przeglądarce sieci web. Powinno być możliwe toosee, że lista czynności do wykonania hello przedstawionych w tym miejscu jest pusta i nie jest już wiązanej toohello udostępnionych wdrożono wystąpienie bazy danych MongoDB.

Samouczek hello toocomplete, można wprowadzić zmiany, bardziej widoczne. Na komputerze deweloperskim Otwórz plik node-todo/public/index.html hello za pomocą ulubionego edytora. Znajdź hello jumbotron nagłówka i Zmień tytuł powitania od "Jestem aholic Todo" za "Jestem aholic Todo na platformie Azure!".

Teraz załóżmy zatwierdzenia:

    git commit -am "Azurify hello title"

Ten czas, umożliwia publikowanie hello tooAzure zmiany przed wypchnięciem go repozytorium GitHub toohello tooback:

    git push azure master

Po zakończeniu wykonywania tego polecenia strony sieci web hello odświeżania i zmiany będą widoczne hello. Ponieważ one świetnie push pochodzenia wstecz toohello zmiany hello zdalnego: 

    git push origin master

## <a name="next-steps"></a>Następne kroki
W tym artykule pokazano, jak tootake aplikacji Node.js i wdróż je tooLinux maszyn wirtualnych działających na platformie Azure. toolearn więcej informacji na temat maszyn wirtualnych systemu Linux na platformie Azure, zobacz [tooLinux wprowadzenie na platformie Azure](/documentation/articles/virtual-machines-linux-introduction/).

Aby uzyskać więcej informacji o tym, jak toodevelop aplikacji Node.js na platformie Azure, zobacz hello [Centrum deweloperów środowiska Node.js](/develop/nodejs/).

