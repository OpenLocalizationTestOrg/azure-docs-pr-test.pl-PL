---
title: "aaaSet się środowiska deweloperskiego w toowork systemu Mac OS X z sieci szkieletowej usług Azure | Dokumentacja firmy Microsoft"
description: "Zainstaluj hello środowiska uruchomieniowego, zestawu SDK i narzędzia i Utwórz lokalny klaster projektowy. Po ukończeniu tej konfiguracji będzie gotowy toobuild aplikacji w systemie Mac OS X."
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: bf84458f-4b87-4de1-9844-19909e368deb
ms.service: service-fabric
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/21/2017
ms.author: saysa
ms.openlocfilehash: 0b8a6c1fc1871fa76f3e21cefbc7f66f79072797
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-your-development-environment-on-mac-os-x"></a>Konfigurowanie środowiska projektowego w systemie Mac OS X
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started.md)
> * [Linux](service-fabric-get-started-linux.md)
> * [OSX](service-fabric-get-started-mac.md)
>
>  

Toorun aplikacji sieci szkieletowej usług mogą być oparte na klastry z systemem Linux przy użyciu systemu Mac OS X. W tym artykule opisano sposób tooset się komputerów Mac na potrzeby programowania.

## <a name="prerequisites"></a>Wymagania wstępne
Sieć szkieletowa usług nie Uruchom natywnie na toorun systemu OS X. lokalnego klastra usługi sieć szkieletowa usług, firma Microsoft udostępnia wstępnie skonfigurowane maszyny wirtualnej systemu Ubuntu przy użyciu Vagrant i VirtualBox. Przed rozpoczęciem potrzebne są następujące elementy:

* [Vagrant (wersja 1.8.4 lub nowsza)](http://www.vagrantup.com/downloads.html)
* [VirtualBox](http://www.virtualbox.org/wiki/Downloads)

>[!NOTE]
> Należy toouse wzajemnie obsługiwane wersje Vagrant i VirtualBox. Program Vagrant może zachowywać się niestabilnie w przypadku nieobsługiwanej wersji programu VirtualBox.
>

## <a name="create-hello-local-vm"></a>Utwórz hello lokalnej maszyny Wirtualnej
toocreate hello lokalnej maszyny Wirtualnej zawierający 5 węzłów klastra usługi sieć szkieletowa, wykonaj następujące kroki hello:

1. Witaj w klonowania `Vagrantfile` repozytorium

    ```bash
    git clone https://github.com/azure/service-fabric-linux-vagrant-onebox.git
    ```
    Ta procedura Przełącz szczegółu hello pliku `Vagrantfile` zawierający hello maszyny Wirtualnej konfiguracji wraz z hello hello lokalizacji maszyny Wirtualnej jest pobierana z.

2. Przejdź toohello klonu lokalne powitania repozytorium

    ```bash
    cd service-fabric-linux-vagrant-onebox
    ```
3. (Opcjonalnie) Zmodyfikuj ustawienia maszyny Wirtualnej domyślne hello

    Domyślnie program hello lokalnej maszyny Wirtualnej jest konfigurowana w następujący sposób:

   * 3 GB przydzielonej pamięci
   * Sieci prywatnych hosta skonfigurowane pod adresem IP 192.168.50.50 umożliwiające przekazywanie ruchu z hello Mac hosta

     Można zmienić w dowolnym z tych ustawień lub dodać inne toohello konfiguracji maszyny Wirtualnej w hello `Vagrantfile`. Zobacz hello [dokumentacji Vagrant](http://www.vagrantup.com/docs) hello pełną listę opcji konfiguracji.
4. Utwórz hello maszyny Wirtualnej

    ```bash
    vagrant up
    ```

   Ten krok pobiera hello wstępnie obrazu maszyny Wirtualnej, rozruchowy, który go lokalnie, a następnie skonfiguruj lokalny usługi Service Fabric klastra w nim. Należy oczekiwać go tootake za kilka minut. Jeśli Instalator zakończy się pomyślnie, zostanie wyświetlony komunikat w danych wyjściowych hello wskazujący, że w tym klastrze hello jest uruchamiany.

    ![Uruchomienie konfiguracji klastra po aprowizacji maszyny wirtualnej][cluster-setup-script]

    >[!TIP]
    > Hello pobierania maszyny Wirtualnej jest zbyt długo, można pobrać przy użyciu wget lub curl lub za pośrednictwem przeglądarki, przechodząc określony przez łącze toohello **config.vm.box_url** w pliku hello `Vagrantfile`. Po pobraniu lokalnie, należy edytować `Vagrantfile` ścieżka lokalna toohello toopoint którego pobrano hello obrazu. Na przykład jeśli pobrano too/home/users/test/azureservicefabric.tp8.box obraz powitania, następnie ustaw **config.vm.box_url** toothat ścieżki.
    >

5. Testowanie hello tego klastra nie został skonfigurowany poprawnie przechodząc tooService Eksploratora sieci szkieletowej w http://192.168.50.50:19080/Explorer (przy założeniu, przechowywane hello domyślne prywatnej sieci IP).

    ![Service Fabric Explorer z hosta hello Mac][sfx-mac]


## <a name="create-application-on-mac-using-yeoman"></a>Tworzenie aplikacji na komputerze Mac przy użyciu narzędzia Yeoman
Usługa Service Fabric udostępnia narzędzia do tworzenia szkieletów, które ułatwiają tworzenie aplikacji usługi Service Fabric z poziomu terminalu przy użyciu generatora szablonów narzędzia Yeoman. Wykonaj kroki hello poniżej tooensure masz generator narzędzia yeoman szablonu usługi sieć szkieletowa hello działa na tym komputerze.

1. Należy toohave Node.js i NPM zainstalowane dla komputerów mac należy. Jeśli nie można zainstalować środowiska Node.js i przy użyciu oprogramowania Homebrew przy użyciu następujących hello NPM. toocheck hello wersji środowiska Node.js i NPM zainstalowany na komputerze Mac, można użyć hello ``-v`` opcji.

  ```bash
  brew install node
  node -v
  npm -v
  ```
2. Zainstaluj generator szablonów [narzędzia Yeoman](http://yeoman.io/) na swoim komputerze z poziomu narzędzia NPM

  ```bash
  npm install -g yo
  ```
3. Zainstaluj narzędzia Yeoman hello generatora ma toouse, wykonaj czynności hello w hello wprowadzenie [dokumentacji](service-fabric-get-started-linux.md). Aplikacje sieci szkieletowej usług toocreate przy użyciu narzędzia Yeoman, wykonaj kroki hello-

  ```bash
  npm install -g generator-azuresfjava       # for Service Fabric Java Applications
  npm install -g generator-azuresfguest      # for Service Fabric Guest executables
  npm install -g generator-azuresfcontainer  # for Service Fabric Container Applications
  ```
4. toobuild aplikacji Java sieci szkieletowej usług dla komputerów Mac, będzie potrzebny - JDK 1.8 i zainstalowane na komputerze hello narzędzia Gradle.


## <a name="install-hello-service-fabric-plugin-for-eclipse-neon"></a>Instalowanie wtyczki usługi sieć szkieletowa powitania dla programu Eclipse Neon

Usługi Service Fabric zawiera dodatek hello **Neon Eclipse dla IDE języka Java** który uprościć proces hello tworzenie, kompilowanie i wdrażanie usług Java. Możesz wykonać kroki instalacji hello wymienione w tym ogólne [dokumentacji](service-fabric-get-started-eclipse.md#install-or-update-the-service-fabric-plug-in-in-eclipse-neon) dotyczących instalowania lub aktualizowania wtyczkę Eclipse sieci szkieletowej usług.

>[!TIP]
> Domyślnie obsługujemy hello domyślne IP jak wspomniano w hello ``Vagrantfile`` w hello ``Local.json`` aplikacji hello wygenerowany. W przypadku zmiany, które i wdrożyć Vagrant z innego adresu IP, zaktualizuj hello odpowiedniego adresu IP w ``Local.json`` również aplikacji.

## <a name="next-steps"></a>Następne kroki
<!-- Links -->
* [Create and deploy your first Service Fabric Java application on Linux using Yeoman](service-fabric-create-your-first-linux-application-with-java.md) (Tworzenie i wdrażanie pierwszej aplikacji Java usługi Service Fabric w systemie Linux przy użyciu programu Yeoman)
* [Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse](service-fabric-get-started-eclipse.md) (Tworzenie i wdrażanie pierwszej aplikacji Java usługi Service Fabric w systemie Linux przy użyciu wtyczki usługi Service Fabric dla środowiska Eclipse)
* [Tworzenie klastra sieci szkieletowej usług w hello portalu Azure](service-fabric-cluster-creation-via-portal.md)
* [Tworzenie klastra sieci szkieletowej usług za pomocą hello Azure Resource Manager](service-fabric-cluster-creation-via-arm.md)
* [Zrozumienie modelu aplikacji hello sieci szkieletowej usług](service-fabric-application-model.md)

<!-- Images -->
[cluster-setup-script]: ./media/service-fabric-get-started-mac/cluster-setup-mac.png
[sfx-mac]: ./media/service-fabric-get-started-mac/sfx-mac.png
[sf-eclipse-plugin-install]: ./media/service-fabric-get-started-mac/sf-eclipse-plugin-install.png
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship
