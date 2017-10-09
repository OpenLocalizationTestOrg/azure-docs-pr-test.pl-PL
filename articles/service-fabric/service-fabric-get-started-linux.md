---
title: "aaaSet się środowisko programowania w systemie Linux | Dokumentacja firmy Microsoft"
description: "Zainstaluj środowisko uruchomieniowe hello i zestawu SDK i Utwórz lokalny klaster projektowy w systemie Linux. Po ukończeniu tej konfiguracji będzie gotowy toobuild aplikacji."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: d552c8cd-67d1-45e8-91dc-871853f44fc6
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/23/2017
ms.author: subramar
ms.openlocfilehash: 9d82c2015f9e2c6fb55f2052c7cdb1e906c5deeb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-development-environment-on-linux"></a>Przygotowywanie środowiska projektowego w systemie Linux
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started.md)
> * [Linux](service-fabric-get-started-linux.md)
> * [OSX](service-fabric-get-started-mac.md)
>
>  

toodeploy i uruchom [aplikacji usługi Azure Service Fabric](service-fabric-application-model.md) na komputerze deweloperskim Linux należy zainstalować hello środowiska uruchomieniowego i typowych zestawu SDK. Można także zainstalować opcjonalne zestawy SDK dla platformy Java i .NET Core.

## <a name="prerequisites"></a>Wymagania wstępne

następujące wersje systemu operacyjnego Hello są obsługiwane w przypadku rozwoju:

* Ubuntu 16.04 (`Xenial Xerus`)

## <a name="update-your-apt-sources"></a>Aktualizowanie źródeł APT
tooinstall hello zestawu SDK i hello skojarzone środowisko uruchomieniowe pakietu za pomocą narzędzia wiersza polecenia get stanie hello, należy najpierw zaktualizować źródła zaawansowane narzędzia pakowania (APT, Distributed File System).

1. Otwórz terminal.
2. Dodawanie listy źródła tooyour hello sieci szkieletowej usług repozytorium.

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] http://apt-mo.trafficmanager.net/repos/servicefabric/ xenial main" > /etc/apt/sources.list.d/servicefabric.list'
    ```

3. Dodaj hello `dotnet` listy źródła tooyour repozytorium.

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list'
    ```

4. Dodaj hello zestaw kluczy stanie tooyour klucza Gnu nowe prywatności Guard (oprogramowania GnuPG lub GPG).

    ```bash
    sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
    ```

5. Dodaj hello oficjalnego Docker GPG klucza tooyour stanie zestaw kluczy.

    ```bash
    sudo apt-get install curl
    sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    ```

6. Konfigurowanie hello Docker repozytorium.

    ```bash
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    ```

7. Odśwież pakiet listy oparte na powitania nowo dodany repozytoriów.

    ```bash
    sudo apt-get update
    ```

## <a name="install-and-set-up-hello-sdk-for-local-cluster-setup"></a>Instalowanie i konfigurowanie hello SDK instalacji klastra lokalnego

Po zaktualizowaniu źródła, możesz zainstalować hello zestawu SDK. Zainstaluj pakiet zestawu SDK usług sieci szkieletowej hello, potwierdzenie instalacji hello i zaakceptować umowę licencyjną toohello.

```bash
sudo apt-get install servicefabricsdkcommon
```

>   [!TIP]
>   Witaj następujące polecenia zautomatyzować akceptują licencji hello pakietów sieci szkieletowej usług:
>   ```bash
>   echo "servicefabric servicefabric/accepted-eula-v1 select true" | sudo debconf-set-selections
>   echo "servicefabricsdkcommon servicefabricsdkcommon/accepted-eula-v1 select true" | sudo debconf-set-selections
>   ```

## <a name="set-up-a-local-cluster"></a>Tworzenie klastra lokalnego
  Jeśli hello instalacja zakończy się pomyślnie, powinny być możliwe toostart klastra lokalnego.

  1. Uruchom skrypt instalacji klastra hello.

      ```bash
      sudo /opt/microsoft/sdk/servicefabric/common/clustersetup/devclustersetup.sh
      ```

  2. Otwórz przeglądarkę sieci web i przejdź zbyt[Service Fabric Explorer](http://localhost:19080/Explorer). Jeśli hello klastra została uruchomiona, powinna zostać wyświetlona hello Service Fabric Explorer z pulpitu nawigacyjnego.

      ![Narzędzie Service Fabric Explorer w systemie Linux][sfx-linux]

  W tym momencie możliwe jest wdrożenie wstępnie skompilowanych pakietów aplikacji usługi Service Fabric lub nowych pakietów opartych na kontenerach gościa bądź plikach wykonywalnych gościa. toobuild nowych usług za pomocą języka Java hello lub .NET Core SDK, wykonaj kroki opcjonalne ustawienia hello, które zostały opublikowane w kolejnych sekcjach.


  > [!NOTE]
  > Klastry autonomiczne nie są obsługiwane w systemie Linux. Witaj w wersji zapoznawczej obsługuje tylko jednego pola i Azure Linux klastrach obejmujących wiele maszyn.
  >

## <a name="set-up-hello-service-fabric-cli"></a>Konfigurowanie hello usługi sieci szkieletowej interfejsu wiersza polecenia

Witaj [interfejsu wiersza polecenia usługi sieć szkieletowa](service-fabric-cli.md) zawiera polecenia do interakcji z jednostek usługi Service Fabric, łącznie z klastrów i aplikacji. Jest on oparty na języku python, dlatego należy się toohave python i pip zainstalowane przed kontynuowaniem hello następujące polecenie:

```bash
pip install sfctl
```

## <a name="install-and-set-up-hello-generators-for-containers-and-guest-executables"></a>Instalowanie i konfigurowanie generatory hello kontenery i plików wykonywalnych gościa
Usługa Service Fabric udostępnia narzędzia do tworzenia szkieletów, które ułatwiają tworzenie aplikacji usługi Service Fabric z poziomu terminalu przy użyciu generatora szablonów narzędzia Yeoman. Wykonaj kroki hello poniżej tooensure masz generatora narzędzia yeoman szablonu usługi sieć szkieletowa hello do pracy na komputerze.

1. Zainstaluj środowisko NodeJs i menedżera NPM na swojej maszynie

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. Zainstaluj generator szablonów [narzędzia Yeoman](http://yeoman.io/) na swoim komputerze z poziomu narzędzia NPM

  ```bash
  sudo npm install -g yo
  ```
3. Zainstaluj generator kontenera usługi sieć szkieletowa Yeo hello i generator execuatble gościa z pakietu NPM

  ```bash
  sudo npm install -g generator-azuresfcontainer  # for Service Fabric container application
  sudo npm install -g generator-azuresfguest      # for Service Fabric guest executable application
  ```

Po zainstalowaniu hello powyżej generatory powinno być możliwe toocreate aplikacji za pomocą pliku wykonywalnego lub kontener usług gościa, uruchamiając `yo azuresfguest` lub `yo azuresfcontainer` odpowiednio.

## <a name="install-hello-necessary-java-artifacts-optional-if-you-want-toouse-hello-java-programming-models"></a>Zainstaluj hello niezbędne Java artefakty (opcjonalnie, jeśli chcesz toouse hello Java modele programowania)

toobuild usługi sieć szkieletowa usług za pomocą języka Java, upewnij się, że 1.8 JDK instalowane wraz z narzędzia Gradle, który służy do uruchamiania zadań kompilacji. Witaj następującego fragmentu instaluje Otwórz 1.8 JDK wraz z narzędzia Gradle. biblioteki usługi sieć szkieletowa Java Hello są pobierane z Maven.

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

## <a name="install-hello-eclipse-neon-plug-in-optional"></a>Zainstaluj hello Neon Eclipse wtyczki (opcjonalnie)

Można zainstalować hello Eclipse wtyczki dla sieci szkieletowej usług z wewnątrz hello **Eclipse IDE dla deweloperów języka Java**. W aplikacji Java sieci szkieletowej tooService dodanie służy aplikacji pliku wykonywalnego gościa Eclipse toocreate sieci szkieletowej usług i aplikacji kontenera.

1. W środowisku Eclipse, upewnij się, czy masz najnowsze Neon Eclipse, a hello najnowszej wersji Buildship (1.0.17 lub nowszym) zainstalowany. Można sprawdzić wersji hello zainstalowanych składników, wybierając **pomocy** > **szczegółowe informacje dotyczące instalacji**. Buildship można zaktualizować przy użyciu instrukcji hello na [Eclipse Buildship: Eclipse wtyczek dla narzędzia Gradle][buildship-update].

2. tooinstall hello wtyczki, wybierz sieć szkieletowa usług **pomocy** > **zainstalować nowe oprogramowanie**.

3. W hello **pracować z** wpisz **http://dl.microsoft.com/eclipse**.

4. Kliknij pozycję **Dodaj**.

    ![Witaj dostępnego oprogramowania strony][sf-eclipse-plugin]

5. Wybierz hello **ServiceFabric** wtyczki, a następnie kliknij przycisk **dalej**.

6. Wykonaj kroki instalacji hello, a następnie zaakceptuj umowę licencyjną użytkownika oprogramowania hello.

Jeśli masz już hello usługi sieć szkieletowa Eclipse wtyczki zainstalowane, upewnij się, że masz hello najnowszej wersji. Można sprawdzić, wybierając **pomocy** > **szczegółowe informacje dotyczące instalacji** , a następnie wyszukiwanie sieci szkieletowej usług hello lista zainstalowanych wtyczek. Wybierz opcję **Aktualizacja**, jeśli jest dostępna nowsza wersja.

Aby uzyskać więcej informacji, zobacz artykuł [Wtyczka usługi Service Fabric na potrzeby tworzenia aplikacji Java w środowisku Eclipse](service-fabric-get-started-eclipse.md).


## <a name="install-hello-net-core-sdk-optional-if-you-want-toouse-hello-net-core-programming-models"></a>Zainstaluj hello .NET Core SDK (opcjonalnie, jeśli chcesz, aby modele programowania .NET Core hello toouse)
Hello .NET Core SDK udostępnia biblioteki hello i szablony, które są wymagane toobuild usługi sieć szkieletowa usług z platformą .NET Core. Zainstaluj pakiet zestawu SDK programu .NET Core hello przez uruchomione hello następujących informacji:

   ```bash
   sudo apt-get install servicefabricsdkcsharp
   ```

## <a name="update-hello-sdk-and-runtime"></a>Aktualizacja hello zestawu SDK i środowiska wykonawczego

najnowszą wersję toohello tooupdate hello zestawu SDK i środowiska uruchomieniowego, uruchom następujące polecenia hello (odznacz hello zestawów SDK, które nie mają):

```bash
sudo apt-get update
sudo apt-get install servicefabric servicefabricsdkcommon servicefabricsdkcsharp
```
tooupdate hello plików binarnych zestawu Java SDK z Maven, należy tooupdate hello wersji szczegóły hello odpowiedniego pliku binarnego w hello ``build.gradle`` pliku toopoint toohello najnowszej wersji. tooknow dokładnie konieczne tooupdate hello wersji, może się odwoływać tooany ``build.gradle`` plików w sieci szkieletowej usług — wprowadzenie przykłady [tutaj](https://github.com/Azure-Samples/service-fabric-java-getting-started).

> [!NOTE]
> Aktualizowanie pakietów hello może spowodować Twojej toostop klastra rozwoju lokalnego uruchamiania. Uruchom ponownie klaster lokalny po uaktualnieniu instrukcjami hello na tej stronie.

## <a name="next-steps"></a>Następne kroki

* [Create and deploy your first Service Fabric Java application on Linux using Yeoman](service-fabric-create-your-first-linux-application-with-java.md) (Tworzenie i wdrażanie pierwszej aplikacji Java usługi Service Fabric w systemie Linux przy użyciu programu Yeoman)
* [Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse](service-fabric-get-started-eclipse.md) (Tworzenie i wdrażanie pierwszej aplikacji Java usługi Service Fabric w systemie Linux przy użyciu wtyczki usługi Service Fabric dla środowiska Eclipse)
* [Create your first CSharp application on Linux](service-fabric-create-your-first-linux-application-with-csharp.md) (Tworzenie pierwszej aplikacji CSharp w systemie Linux)
* [Przygotowywanie środowiska projektowego w systemie OSX](service-fabric-get-started-mac.md)
* [Użyj aplikacji hello toomanage usługi sieci szkieletowej interfejsu wiersza polecenia](service-fabric-application-lifecycle-sfctl.md)
* [Różnice w usłudze Service Fabric w systemie Windows i Linux](service-fabric-linux-windows-differences.md)
* [Get started with Service Fabric CLI](service-fabric-cli.md) (Wprowadzenie do interfejsu wiersza polecenia usługi Service Fabric)

<!-- Links -->

[azure-xplat-cli-github]: https://github.com/Azure/azure-xplat-cli
[install-node]: https://nodejs.org/en/download/package-manager/#installing-node-js-via-package-manager
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship

<!--Images -->

[sf-eclipse-plugin]: ./media/service-fabric-get-started-linux/service-fabric-eclipse-plugin.png
[sfx-linux]: ./media/service-fabric-get-started-linux/sfx-linux.png
