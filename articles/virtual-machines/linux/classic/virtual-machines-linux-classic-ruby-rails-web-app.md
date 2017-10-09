---
title: aaaHost Ruby w witrynie sieci Web szyny na maszynie Wirtualnej systemu Linux | Dokumentacja firmy Microsoft
description: "Konfigurowanie i udostępniać Ruby na podstawie szyny witryny sieci Web na platformie Azure przy użyciu maszyny wirtualnej systemu Linux."
services: virtual-machines-linux
documentationcenter: ruby
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: aad32685-3550-4bff-9c73-beb8d70b3291
ms.service: virtual-machines-linux
ms.workload: web
ms.tgt_pltfrm: vm-linux
ms.devlang: ruby
ms.topic: article
ms.date: 06/27/2017
ms.author: robmcm
ms.openlocfilehash: c545c24fc6c89497854bbe55a6d0d1d0b072c386
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="ruby-on-rails-web-application-on-an-azure-vm"></a>Aplikacja sieci Web Ruby on Rails na maszynie wirtualnej platformy Azure
Ten samouczek pokazuje, jak toohost Ruby na szyny witryny sieci Web na platformie Azure przy użyciu maszyny wirtualnej systemu Linux.  

W tym samouczku została zweryfikowana przy użyciu Ubuntu Server 14.04 LTS. Jeśli używasz innej dystrybucji systemu Linux, może być konieczne toomodify hello kroki szyny tooinstall.

> [!IMPORTANT]
> Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../../../azure-resource-manager/resource-manager-deployment-model.md).  W tym artykule omówiono przy użyciu hello klasycznego modelu wdrażania. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.
>
>

## <a name="create-an-azure-vm"></a>Tworzenie maszyny Wirtualnej platformy Azure
Rozpocznij od utworzenia maszyny Wirtualnej platformy Azure z obrazem systemu Linux.

toocreate hello maszyny Wirtualnej, można użyć hello portalu Azure lub hello Azure interfejsu wiersza polecenia (CLI).

### <a name="azure-portal"></a>Azure Portal
1. Zaloguj się na powitania [portalu Azure](https://portal.azure.com)
2. Kliknij przycisk **nowy**, wpisz "Ubuntu Server 14.04" hello pola wyszukiwania. Kliknij pozycję hello zwróconych hello wyszukiwania. Wybierz model wdrażania hello, **klasycznego**, następnie kliknij przycisk "Utwórz".
3. W bloku podstawy hello, podaj wartości dla pól wymaganych hello: Nazwa (hello maszyny Wirtualnej), nazwę użytkownika, typ uwierzytelniania i hello odpowiednie poświadczenia, subskrypcji platformy Azure, grupy zasobów i lokalizacji.

   ![Utwórz nowy obraz Ubuntu](./media/virtual-machines-linux-classic-ruby-rails-web-app/createvm.png)

4. Po udostępnieniu hello maszyny Wirtualnej, kliknij nazwę maszyny Wirtualnej hello i kliknij przycisk **punkty końcowe** w hello **ustawienia** kategorii. Znajdź hello punkt końcowy SSH, kategorii **autonomiczny**.

   ![Domyślny punkt końcowy](./media/virtual-machines-linux-classic-ruby-rails-web-app/endpointsnewportal.png)

### <a name="azure-cli"></a>Interfejs wiersza polecenia platformy Azure
Wykonaj kroki hello w [tworzenia maszyny wirtualnej systemem Linux][vm-instructions].

Po udostępnieniu hello maszyny Wirtualnej można uzyskać, uruchamiając następujące polecenie hello punkt końcowy SSH hello:

    azure vm endpoint list <vm-name>  

## <a name="install-ruby-on-rails"></a>Zainstaluj na szyny Ruby
1. Użyj toohello tooconnect SSH maszyny Wirtualnej.
2. Hello sesji SSH używając hello, wykonując polecenia tooinstall Ruby na powitania maszyny Wirtualnej:

        sudo apt-get update -y
        sudo apt-get upgrade -y

        sudo apt-add-repository ppa:brightbox/ruby-ng
        sudo apt-get update
        sudo apt-get install ruby2.4

        > [!TIP]
        > hello brightbox repository contains hello current Ruby distribution.

    Witaj, instalacja może zająć kilka minut. Po ukończeniu, należy użyć powitania po tooverify polecenia zainstalowano Ruby:

        ruby -v

3. Użyj hello następujące polecenie szyny tooinstall:

        sudo gem install rails --no-rdoc --no-ri -V

    Użyj hello--nie rdoc i--nie ri flagi tooskip instalowanie dokumentacji hello jest szybszy.
    To polecenie będzie może zająć dużo czasu tooexecute, więc Dodawanie hello -V zostaną wyświetlone informacje o postępie instalacji hello.

## <a name="create-and-run-an-app"></a>Tworzenie i uruchamianie aplikacji
Jest nadal zalogowany za pośrednictwem protokołu SSH, uruchom następujące polecenia hello:

    rails new myapp
    cd myapp
    rails server -b 0.0.0.0 -p 3000

Witaj [nowe](http://guides.rubyonrails.org/command_line.html#rails-new) polecenie tworzy nową aplikację szyny. Witaj [serwera](http://guides.rubyonrails.org/command_line.html#rails-server) polecenie uruchamia hello serwera sieci web WEBrick dołączony do szyny. (Do użytku produkcyjnego prawdopodobnie odpowiedni będzie toouse innego serwera, takie jak Unicorn lub pasażerów.)

Powinny pojawić się dane wyjściowe podobne toohello poniżej.

    => Booting WEBrick
    => Rails 4.2.1 application starting in development on http://0.0.0.0:3000
    => Run `rails server -h` for more startup options
    => Ctrl-C tooshutdown server
    [2015-06-09 23:34:23] INFO  WEBrick 1.3.1
    [2015-06-09 23:34:23] INFO  ruby 1.9.3 (2013-11-22) [x86_64-linux]
    [2015-06-09 23:34:23] INFO  WEBrick::HTTPServer#start: pid=27766 port=3000

## <a name="add-an-endpoint"></a>Dodawanie punktu końcowego
1. Przejdź toohello [portalu Azure] [https://portal.azure.com] i wybierz maszyny Wirtualnej.

2. Wybierz **punkty końcowe** w hello **ustawienia** wzdłuż hello lewej krawędzi hello strony.

3. Kliknij przycisk **dodać** u góry hello hello strony.

4. W hello **dodać punkt końcowy** okna dialogowego wprowadź hello następujących informacji:

   * **Nazwa**: HTTP
   * **Protokół**: TCP
   * **Port publiczny**: 80
   * **Port prywatny**: 3000
   * **Pływającego adresu PI**: wyłączone
   * **Listy kontroli dostępu — kolejność**: 1001 lub inną wartość, która ustawia hello priorytet tej reguły dostępu.
   * **Listy kontroli dostępu — nazwa**: allowHTTP
   * **Listy kontroli dostępu — Akcja**: Zezwalaj
   * **Listy kontroli dostępu - podsieci zdalnej**: 1.0.0.0/16

     Ten punkt końcowy ma publiczny port 80, który skieruje ruchu toohello port prywatny 3000, gdzie hello szyny serwer nasłuchuje. reguły listy kontroli dostępu Hello umożliwia publiczny ruch na porcie 80.

     ![nowy punkt końcowy](./media/virtual-machines-linux-classic-ruby-rails-web-app/createendpoint.png)

5. Kliknij przycisk OK toosave hello endpoint.

6. Komunikat powinien zostać wyświetlony stwierdzający **zapisywanie punktu końcowego maszyny wirtualnej**. Gdy ten komunikat nie zniknie, punktu końcowego hello jest aktywna. Może teraz przetestować aplikację, przechodząc toohello nazwę DNS maszyny wirtualnej. Hello witryny sieci Web powinna wyglądać podobnie toohello następujące:

    ![Domyślna strona szyny][default-rails-cloud]

## <a name="next-steps"></a>Następne kroki
W tym samouczku jak większość kroków hello ręcznie. W środowisku produkcyjnym może napisać aplikację na komputerze deweloperskim i wdrożyć ją toohello maszyny Wirtualnej platformy Azure. Ponadto większość środowisk produkcyjnych hostowanie aplikacji szyny hello w połączeniu z innym procesem serwera, takich jak Apache lub NginX, która obsługuje żądania routingu wystąpień toomultiple hello szyny aplikacji oraz obsługująca zasoby statyczne. Aby uzyskać więcej informacji zobacz http://rubyonrails.org/deploy/.

toolearn więcej informacji na temat Ruby na szyny, odwiedź stronę hello [dopisków fonetycznych w przewodnikach szyny][rails-guides].

toouse Azure usług z aplikacji dopisków fonetycznych, zobacz:

* [Przechowywania danych niestrukturalnych przy użyciu obiektów blob][blobs]
* [Pary klucz wartość magazynu przy użyciu tabel][tables]
* [Obsługiwać zawartości wysokiej przepustowości z hello sieci dostarczania zawartości][cdn-howto]

<!-- WA.com links -->
[blobs]:../../../storage/blobs/storage-ruby-how-to-use-blob-storage.md
[cdn-howto]:https://azure.microsoft.com/develop/ruby/app-services/
[tables]:../../../cosmos-db/table-storage-how-to-use-ruby.md
[vm-instructions]:createportal.md

<!-- External Links -->
[rails-guides]:http://guides.rubyonrails.org/
[sqlite3]:http://www.sqlite.org/

<!-- Images -->

[default-rails-cloud]:./media/virtual-machines-linux-classic-ruby-rails-web-app/basicrailscloud.png
[vmlist]:./media/virtual-machines-linux-classic-ruby-rails-web-app/vmlist.png
[endpoints]:./media/virtual-machines-linux-classic-ruby-rails-web-app/endpoints.png
[new-endpoint]:./media/virtual-machines-linux-classic-ruby-rails-web-app/newendpoint.png
[new-endpoint1]:./media/virtual-machines-linux-classic-ruby-rails-web-app/newendpoint1.png
