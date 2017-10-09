---
title: "aaaCreate aplikacji Java niezawodnej podmiotów sieć szkieletowa usług Azure w systemie Linux | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate i wdrożenie aplikacji Java sieci szkieletowej usług niezawodnej złośliwych użytkowników w ciągu pięciu minut."
services: service-fabric
documentationcenter: java
author: rwike77
manager: timlt
editor: 
ms.assetid: 02b51f11-5d78-4c54-bb68-8e128677783e
ms.service: service-fabric
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/23/2017
ms.author: ryanwi
ms.openlocfilehash: 11496b767811c89969c65d1682d843448eb6a922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-java-service-fabric-reliable-actors-application-on-linux"></a>Tworzenie pierwszej aplikacji Java z interfejsem Reliable Actors usługi Service Fabric w systemie Linux
> [!div class="op_single_selector"]
> * [C# — Windows](service-fabric-create-your-first-application-in-visual-studio.md)
> * [Java — Linux](service-fabric-create-your-first-linux-application-with-java.md)
> * [C# — Linux](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

Ten przewodnik Szybki start pomaga w ciągu kilku minut utworzyć pierwszą aplikację Java usługi Azure Service Fabric w środowisku projektowym w systemie Linux.  Gdy skończysz, będziesz mieć prostą aplikację usługi pojedynczej Java uruchomionych na powitania lokalnego klastra projektowego.  

## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem pracy Zainstaluj hello zestawu SDK usług sieci szkieletowej, hello usługi sieci szkieletowej interfejsu wiersza polecenia, a konfiguracja klastra Programowanie w Twojej [środowisko projektowe Linux](service-fabric-get-started-linux.md). Jeśli używasz systemu Mac OS X, możesz [skonfigurować środowisko deweloperskie systemu Linux na maszynie wirtualnej za pomocą narzędzia Vagrant](service-fabric-get-started-mac.md).

Ma również tooinstall hello [interfejsu wiersza polecenia usługi sieć szkieletowa](service-fabric-cli.md).

### <a name="install-and-set-up-hello-generators-for-java"></a>Instalowanie i konfigurowanie hello generatory dla języka Java
Usługa Service Fabric udostępnia narzędzia do tworzenia szkieletu, które ułatwiają tworzenie aplikacji Java usługi Service Fabric z poziomu terminalu przy użyciu generatora szablonów Yeoman. Wykonaj kroki hello poniżej tooensure ma generatora narzędzia yeoman szablonu usługi sieć szkieletowa hello for Java działa na tym komputerze.
1. Zainstaluj środowisko NodeJs i menedżera NPM na swojej maszynie

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. Zainstaluj generator szablonów [narzędzia Yeoman](http://yeoman.io/) na swoim komputerze z poziomu narzędzia NPM

  ```bash
  sudo npm install -g yo
  ```
3. Zainstaluj generator aplikacji usługi sieci szkieletowej Yeo Java hello z pakietu NPM

  ```bash
  sudo npm install -g generator-azuresfjava
  ```

## <a name="create-hello-application"></a>Tworzenie aplikacji hello
Aplikacja usługi Service Fabric zawiera jeden lub więcej usług, a każda z określoną rolę w dostarczaniu funkcjonalności aplikacji hello. generator Hello zainstalowane w ostatniej sekcji hello umożliwia łatwe toocreate pierwszą usługi i tooadd więcej później.  Możesz też tworzyć, kompilować i wdrażać aplikacje Java usługi Service Fabric przy użyciu wtyczki dla środowiska Eclipse. Zobacz [Create and deploy your first Java application using Eclipse](service-fabric-get-started-eclipse.md) (Tworzenie i wdrażanie pierwszej aplikacji Java za pomocą środowiska Eclipse). Dla tego szybki start Użyj narzędzia Yeoman toocreate aplikacji za pomocą jednej usługi, która przechowuje i pobiera wartość licznika.

1. Na terminalu wpisz ``yo azuresfjava``.
2. Nadaj nazwę aplikacji.
3. Wybierz typ hello pierwszej usługi i nadaj jej nazwę. Na potrzeby tego samouczka wybierz usługę Reliable Actor Service. Aby uzyskać więcej informacji na temat hello innych typów usług, zobacz [usługi sieć szkieletowa omówienie modelu programowania](service-fabric-choose-framework.md).
   ![Generator Yeoman usługi Service Fabric dla platformy Java][sf-yeoman]

## <a name="build-hello-application"></a>Tworzenie aplikacji hello
Hello narzędzia usługi sieć szkieletowa Yeoman szablony obejmują skryptu kompilacji dla [Gradle](https://gradle.org/), który można użyć aplikacji hello toobuild z hello terminala.
Zależności aplikacji Java usługi Service Fabric są pobierane z narzędzia Maven. toobuild i pracy w aplikacji Java sieci szkieletowej usług hello należy tooensure, że masz JDK i zainstalowane narzędzia Gradle. Jeśli nie został jeszcze zainstalowany, możesz uruchomić hello tooinstall JDK(openjdk-8-jdk) i Gradle -

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

toobuild i pakietów hello aplikacji, uruchom następujące hello:

  ```bash
  cd myapp
  gradle
  ```

## <a name="deploy-hello-application"></a>Wdrażanie aplikacji hello
Po utworzeniu aplikacji hello można wdrożyć klaster lokalny toohello.

1. Połącz toohello lokalnego klastra usługi sieć szkieletowa usług.

    ```bash
    sfctl cluster select --endpoint http://localhost:19080
    ```

2. Uruchom skrypt instalacji hello hello szablonu toocopy aplikacji hello pakietu magazynu obrazu klastra toohello, Rejestracja typu aplikacji hello, i Utwórz wystąpienie aplikacji hello.

    ```bash
    ./install.sh
    ```

Wdrażanie aplikacji hello wbudowane jest hello takie same jak innych aplikacji sieci szkieletowej usług. Zobacz dokumentację hello [Zarządzanie aplikacją sieci szkieletowej usług z hello interfejsu wiersza polecenia usługi sieć szkieletowa](service-fabric-application-lifecycle-sfctl.md) szczegółowe informacje.

Parametry toothese polecenia można znaleźć w manifestach hello generowane w pakiecie aplikacji hello.

Po wdrożeniu aplikacji hello, otwórz przeglądarkę i przejdź do [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) w [http://localhost: 19080/Explorer](http://localhost:19080/Explorer).
Następnie rozwiń hello **aplikacji** węzeł i zwróć uwagę, że istnieją teraz wpis dla danego typu aplikacji i drugi dla hello pierwsze wystąpienie tego typu.

## <a name="start-hello-test-client-and-perform-a-failover"></a>Uruchomić klienta testowego hello i przejściu w tryb failover
Złośliwych użytkowników nie rób nic na ich własnych, wymagają innego toosend usługi lub klienta ich wiadomości. Szablon aktora Hello zawiera skrypt prosty test przy użyciu usługi aktora hello można toointeract.

1. Uruchom skrypt hello przy użyciu hello czujki narzędzie toosee hello dane wyjściowe hello usługi aktora.  skrypt testu Hello wywołuje hello `setCountAsync()` hello wywołania metod na powitania aktora tooincrement licznika, `getCountAsync()` metody na powitania aktora tooget hello nowa wartość licznika i wyświetla, które wartość toohello konsoli.

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```

2. W narzędziu Service Fabric Explorer Znajdź hello węzła hostingu hello repliki podstawowej dla usługi aktora hello. W poniższym zrzucie ekranu hello jest węzeł 3. uchwyty replika podstawowa usługa Hello operacje odczytu i zapisu.  Zmiany stanu usługi są następnie replikowane limit toohello replikach pomocniczych, uruchomione w węzłach 0 i 1 na ekranie powitania zrzut poniżej.

    ![Znajdowanie hello repliki podstawowej w narzędziu Service Fabric Explorer][sfx-primary]

3. W **węzłów**, kliknij węzeł hello można znaleźć w poprzednim kroku hello, a następnie wybierz **Dezaktywuj (ponowne uruchomienie)** z menu Akcje hello. Ta akcja uruchamia ponownie węzeł hello działa replika podstawowa usługa hello i wymusza tooone trybu failover, hello replik pomocniczych uruchomiona w innym węźle.  Tej repliki pomocniczej jest awansowana tooprimary innej repliki pomocniczej jest tworzona na inny węzeł i repliki podstawowej hello rozpoczyna tootake operacji odczytu/zapisu. Podczas ponownego uruchamiania hello węzła, obejrzyj dane wyjściowe hello powitania klienta testowego i Uwaga tego licznika hello nadal tooincrement pomimo hello trybu failover.

## <a name="remove-hello-application"></a>Usuwanie aplikacji hello
Użyj hello Odinstaluj skryptu wystąpienia aplikacji hello hello szablonu toodelete wyrejestrować pakiet aplikacji hello i usuwanie pakietu aplikacji hello z magazynu obrazu klastra hello.

```bash
./uninstall.sh
```

W narzędziu Service Fabric explorer widać, że aplikacja hello i typu aplikacji nie są widoczne w hello **aplikacji** węzła.

## <a name="service-fabric-java-libraries-on-maven"></a>Biblioteki Java usługi Service Fabric w narzędziu Maven
Biblioteki Java usługi Service Fabric są teraz hostowane w narzędziu Maven. Można dodać zależności hello hello ``pom.xml`` lub ``build.gradle`` z bibliotek usługi sieć szkieletowa Java toouse projektów z **mavenCentral**.

### <a name="actors"></a>Aktorzy

Obsługa interfejsu Reliable Actors usługi Service Fabric dla Twojej aplikacji.

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-actors-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-actors-preview:0.10.0'
  }
  ```

### <a name="services"></a>Usługi

Obsługa usługi bezstanowej usługi Service Fabric dla Twojej aplikacji.

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-services-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-services-preview:0.10.0'
  }
  ```

### <a name="others"></a>Inne
#### <a name="transport"></a>Transport

Obsługa warstwy transportowej dla aplikacji Java usługi Service Fabric. Nie trzeba tooexplicitly dodawać tej zależności tooyour niezawodnego aktora lub aplikacje usług, chyba że program na powitania warstwy transportowej.

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-transport-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-transport-preview:0.10.0'
  }
  ```

#### <a name="fabric-support"></a>Obsługa usługi Service Fabric

System poziomu obsługę sieci szkieletowej usług, który zawiera środowisko uruchomieniowe usługi sieć szkieletowa toonative. Nie trzeba tooexplicitly Dodawanie tej zależności tooyour niezawodnego aktora lub aplikacji usługi. Pobiera pobrania automatycznie z Maven, po dołączeniu hello innych zależności powyżej.

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-preview:0.10.0'
  }
  ```

## <a name="migrating-old-service-fabric-java-applications-toobe-used-with-maven"></a>Migrowanie starego toobe aplikacji Java sieci szkieletowej usług używany z Maven
Biblioteki usługi sieć szkieletowa Java niedawno został przeniesiony z repozytorium tooMaven zestawu SDK Java sieci szkieletowej usług. Gdy hello nowe aplikacje, które można wygenerować za pomocą narzędzia Yeoman lub Eclipse, spowoduje wygenerowanie najnowsze zaktualizowane projekty (które będą mogli toowork z Maven), można aktualizacji istniejącej sieci szkieletowej usług bezstanowych lub aplikacji Java aktora, które były używane hello usługi Sieć szkieletowa zestawu Java SDK wcześniej, zależności usługi sieci szkieletowej Java hello toouse z Maven. Wykonaj kroki hello wymienione [tutaj](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure starszych aplikacji współdziała z Maven.

## <a name="next-steps"></a>Następne kroki

* [Tworzenie pierwszej aplikacji Java usługi Service Fabric w systemie Linux przy użyciu środowiska Eclipse](service-fabric-get-started-eclipse.md)
* [Dowiedz się więcej o usłudze Reliable Actors](service-fabric-reliable-actors-introduction.md)
* [Interakcji z klastrami usługi sieć szkieletowa usług za pomocą hello usługi sieci szkieletowej interfejsu wiersza polecenia](service-fabric-cli.md)
* Uzyskaj informacje o [opcjach pomocy technicznej usługi Service Fabric](service-fabric-support.md)
* [Getting started with Service Fabric CLI (Wprowadzenie do interfejsu wiersza polecenia usługi Service Fabric)](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-yeoman.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-java/sfx-primary.png
[sf-eclipse-templates]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-eclipse-templates.png
