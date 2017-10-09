---
title: "aaaCreate pierwszej aplikacji platformy Azure mikrousług w systemie Linux przy użyciu języka C# | Dokumentacja firmy Microsoft"
description: "Tworzenie i wdrażanie aplikacji usługi Service Fabric przy użyciu platformy C#"
services: service-fabric
documentationcenter: csharp
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 5a96d21d-fa4a-4dc2-abe8-a830a3482fb1
ms.service: service-fabric
ms.devlang: csharp
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/21/2017
ms.author: subramar
ms.openlocfilehash: 68d685e130be338ebcdb2f1af24b66d1e14f580a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-azure-service-fabric-application"></a>Tworzenie pierwszej aplikacji usługi Azure Service Fabric
> [!div class="op_single_selector"]
> * [C# — Windows](service-fabric-create-your-first-application-in-visual-studio.md)
> * [Java — Linux](service-fabric-create-your-first-linux-application-with-java.md)
> * [C# — Linux](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

Usługa Service Fabric udostępnia zestawy SDK do kompilowania usług w systemie Linux przy użyciu platform .NET Core i Java. W tym samouczku opisano, jak toocreate aplikacji dla systemu Linux i kompilacji usługi przy użyciu języka C# (.NET Core).

## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem upewnij się, że masz [skonfigurowane środowisko programowania systemu Linux](service-fabric-get-started-linux.md). Jeśli używasz systemu Mac OS X, możesz [skonfigurować jednopunktowe środowisko systemu Linux na maszynie wirtualnej za pomocą narzędzia Vagrant](service-fabric-get-started-mac.md).

Ma również tooinstall hello [usługi sieci szkieletowej interfejsu wiersza polecenia](service-fabric-cli.md)

### <a name="install-and-set-up-hello-generators-for-csharp"></a>Instalowanie i konfigurowanie hello generatory kodu dla języka CSharp
Usługa Service Fabric udostępnia narzędzia do tworzenia szkieletu, które ułatwiają tworzenie aplikacji CSharp usługi Service Fabric z poziomu terminalu przy użyciu generatora szablonów Yeoman. Wykonaj kroki hello poniżej tooensure masz generatora narzędzia yeoman szablonu usługi sieć szkieletowa hello CSharp działa na tym komputerze.
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
  sudo npm install -g generator-azuresfcsharp
  ```

## <a name="create-hello-application"></a>Tworzenie aplikacji hello
Aplikacja usługi Service Fabric może zawierać jeden lub więcej usług, a każda z określoną rolę w dostarczaniu funkcjonalności aplikacji hello. Witaj sieci szkieletowej usług [narzędzia Yeoman](http://yeoman.io/) generator języka CSharp, które zostaną zainstalowane w ostatnim kroku, umożliwia łatwe toocreate pierwszą usługi i tooadd więcej później. Użyjmy toocreate narzędzia Yeoman aplikacji z jedną usługą.

1. W terminalu wpisz następujące polecenie toostart tworzenia szkieletów hello hello:`yo azuresfcsharp`
2. Nadaj nazwę aplikacji.
3. Wybierz typ hello pierwszej usługi i nadaj jej nazwę. Do celów tego samouczka hello wybieramy opcję niezawodnej usługi aktora.

   ![Generator Yeoman usługi Service Fabric dla platformy C#][sf-yeoman]

> [!NOTE]
> Aby uzyskać więcej informacji na temat opcji hello, zobacz [usługi sieć szkieletowa omówienie modelu programowania](service-fabric-choose-framework.md).
>
>

## <a name="build-hello-application"></a>Tworzenie aplikacji hello
Witaj narzędzia usługi sieć szkieletowa Yeoman szablony obejmują skryptu kompilacji, czy można użyć aplikacji hello toobuild z hello terminali (po Nawigacja toohello folderu aplikacji).

  ```sh
 cd myapp
 ./build.sh
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

Po wdrożeniu aplikacji hello, otwórz przeglądarkę i przejdź do [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) w [http://localhost: 19080/Explorer](http://localhost:19080/Explorer). Następnie rozwiń hello **aplikacji** węzeł i zwróć uwagę, że istnieją teraz wpis dla danego typu aplikacji i drugi dla hello pierwsze wystąpienie tego typu.

## <a name="start-hello-test-client-and-perform-a-failover"></a>Uruchomić klienta testowego hello i przejściu w tryb failover
Projekty aktora nie działają samodzielnie. Wymagają one innej usługi lub klienta toosend ich wiadomości. Szablon aktora Hello zawiera skrypt prosty test przy użyciu usługi aktora hello można toointeract.

1. Uruchom skrypt hello przy użyciu hello czujki narzędzie toosee hello dane wyjściowe hello usługi aktora.

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```
2. W narzędziu Service Fabric Explorer Znajdź węzeł obsługujący replikę podstawową hello hello usługi aktora. W poniższym zrzucie ekranu hello jest węzeł 3.

    ![Znajdowanie hello repliki podstawowej w narzędziu Service Fabric Explorer][sfx-primary]
3. Kliknij węzeł hello można znaleźć w poprzednim kroku hello, a następnie wybierz **Dezaktywuj (ponowne uruchomienie)** z menu Akcje hello. Ta akcja powoduje ponowne uruchomienie jednego węzła w klastrze lokalnym wymuszenia pracy awaryjnej tooa replikę pomocniczą uruchomiona w innym węźle. Jak to zrobić, należy zwrócić uwagę toohello w danych wyjściowych powitania klienta testowego i Uwaga tego licznika hello nadal tooincrement pomimo hello trybu failover.

## <a name="adding-more-services-tooan-existing-application"></a>Dodawanie więcej usług tooan istniejącej aplikacji

tooadd inną tooan aplikację usługi już utworzone przy użyciu `yo`, wykonaj następujące kroki hello:
1. Zmień katalog główny toohello hello istniejącej aplikacji.  Na przykład `cd ~/YeomanSamples/MyApplication`, jeśli `MyApplication` to aplikacja hello utworzone przez narzędzia Yeoman.
2. Uruchom polecenie `yo azuresfcsharp:AddService`

## <a name="migrating-from-projectjson-toocsproj"></a>Migrowanie z project.json too.csproj
1. Uruchamianie "dotnet migracji" w katalogu głównym projektu zostanie poddana migracji wszystkich hello project.json toocsproj format.
2. Aktualizacja hello projekt zawiera odwołania do odpowiednio toocsproj plików w projekcie.
3. Zaktualizuj hello pliki toocsproj nazwy pliku projektu w build.sh.

## <a name="next-steps"></a>Następne kroki

* [Dowiedz się więcej o usłudze Reliable Actors](service-fabric-reliable-actors-introduction.md)
* [Interakcja z klastrów sieci szkieletowej usług za pomocą hello usługi sieci szkieletowej interfejsu wiersza polecenia](service-fabric-cli.md)
* Uzyskaj informacje o [opcjach pomocy technicznej usługi Service Fabric](service-fabric-support.md)
* [Getting started with Service Fabric CLI (Wprowadzenie do interfejsu wiersza polecenia usługi Service Fabric)](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-csharp/yeoman-csharp.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-csharp/sfx-primary.png
