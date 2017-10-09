---
title: "aaaCreate Twojego pierwszego na podstawie aktora Azure mikrousługi w języku Java | Dokumentacja firmy Microsoft"
description: "Ten samouczek przedstawia kroki tworzenia, debugowania i wdrażania prostego usługi aktora na podstawie przy użyciu usługi sieci szkieletowej Reliable Actors hello."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d31dc8ab-9760-4619-a641-facb8324c759
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/04/2017
ms.author: vturecek
ms.openlocfilehash: 24718a8d7034360c53597f139169580f1a6ce732
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-reliable-actors"></a>Wprowadzenie do korzystania z Reliable Actors
> [!div class="op_single_selector"]
> * [C# w systemie Windows](service-fabric-reliable-actors-get-started.md)
> * [Java w systemie Linux](service-fabric-reliable-actors-get-started-java.md)
> 
> 

W tym artykule opisano podstawy hello Azure Service Fabric Reliable Actors oraz przedstawiono sposób tworzenia i wdrażania prostą aplikację niezawodnego aktora w języku Java.

## <a name="installation-and-setup"></a>Instalacja i Konfiguracja
Przed rozpoczęciem upewnij się, że masz środowisko projektowania sieci szkieletowej usług hello na tym komputerze.
Jeśli potrzebujesz tooset go, przejdź do zbyt[wprowadzenie dla komputerów Mac](service-fabric-get-started-mac.md) lub [wprowadzenie w systemie Linux](service-fabric-get-started-linux.md).

## <a name="basic-concepts"></a>Podstawowe pojęcia
wprowadzenie Reliable Actors, możesz tylko tooget należy toounderstand kilka podstawowych pojęć:

* **Usługa aktora**. Reliable Actors są popakowane w niezawodnej usługi, które można wdrożyć w infrastrukturze sieci szkieletowej usług hello. Wystąpienia aktora zostaną aktywowane w wystąpieniu usługi o nazwie.
* **Rejestracja aktora**. Jako z usługami Reliable Services, usługi niezawodnego aktora musi toobe zarejestrowane ze środowiskiem uruchomieniowym usługi sieć szkieletowa hello. Ponadto typ aktora hello musi toobe zarejestrowany hello aktora w czasie wykonywania.
* **Interfejs aktora**. Interfejs aktora Hello jest używany toodefine jednoznacznie interfejs publiczny aktora. W terminologii modelu niezawodnego aktora hello hello aktora interfejs definiuje hello typów komunikatów, które hello aktora można zrozumieć i przetworzyć. Interfejs aktora Hello jest używany przez innych uczestników i aplikacje klienckie zbyt "Wyślij" (asynchronicznie) aktora toohello wiadomości. Reliable Actors można zaimplementować wiele interfejsów.
* **Klasa ActorProxy**. Hello ActorProxy klasy jest używany przez klienta tooinvoke aplikacji hello metod udostępnianych za pośrednictwem interfejsu aktora hello. Witaj klasy ActorProxy zawiera dwie ważne funkcje:
  
  * Rozpoznawanie nazw: jest w stanie toolocate hello aktora w klastrze hello (Znajdź hello węzeł klastra hello, w którym jest hostowany).
  * Obsługa błąd: można ponowić próbę wywołania metody i ponownie rozwiązania lokalizacji aktora powitania po, na przykład błąd, który wymaga toobe aktora hello przeniesiony tooanother węzła w klastrze hello.

następujące reguły, które odnoszą się interfejsów tooactor Hello są warto zauważyć:

* Metody interfejsu aktora nie może być przeciążony.
* Interfejs aktora metody nie może mieć wychodzących, ref lub parametrów opcjonalnych.
* Interfejsy ogólne nie są obsługiwane.

## <a name="create-an-actor-service"></a>Tworzenie usługi aktora
Rozpocznij od utworzenia nowej aplikacji sieci szkieletowej usług. Witaj zestawu SDK sieci szkieletowej usług dla systemu Linux zawiera narzędzia Yeoman generator tooprovide hello szkieletów dla aplikacji sieci szkieletowej usług za pomocą usługi bezstanowej. Zacznij od uruchomienia hello następujące narzędzia Yeoman polecenia:

```bash
$ yo azuresfjava
```

Wykonaj hello instrukcje toocreate **niezawodnej usługi aktora**. W tym samouczku nazwa hello aplikacji "HelloWorldActorApplication" i hello aktora "HelloWorldActor." zostanie utworzony po szkieletów Hello:

```bash
HelloWorldActorApplication/
├── build.gradle
├── HelloWorldActor
│   ├── build.gradle
│   ├── settings.gradle
│   └── src
│       └── reliableactor
│           ├── HelloWorldActorHost.java
│           └── HelloWorldActorImpl.java
├── HelloWorldActorApplication
│   ├── ApplicationManifest.xml
│   └── HelloWorldActorPkg
│       ├── Code
│       │   ├── entryPoint.sh
│       │   └── _readme.txt
│       ├── Config
│       │   ├── _readme.txt
│       │   └── Settings.xml
│       ├── Data
│       │   └── _readme.txt
│       └── ServiceManifest.xml
├── HelloWorldActorInterface
│   ├── build.gradle
│   └── src
│       └── reliableactor
│           └── HelloWorldActor.java
├── HelloWorldActorTestClient
│   ├── build.gradle
│   ├── settings.gradle
│   ├── src
│   │   └── reliableactor
│   │       └── test
│   │           └── HelloWorldActorTestClient.java
│   └── testclient.sh
├── install.sh
├── settings.gradle
└── uninstall.sh
```

## <a name="reliable-actors-basic-building-blocks"></a>Niezawodne złośliwych użytkowników podstawowych bloków konstrukcyjnych
podstawowe pojęcia dotyczące Hello opisanych wcześniej przetłumaczenie hello podstawowe bloki konstrukcyjne usługi niezawodnego aktora.

### <a name="actor-interface"></a>Interfejs aktora
Zawiera definicję interfejsu hello hello aktora. Ten interfejs definiuje kontrakt aktora hello, który jest współużytkowany przez hello aktora implementacji i klientom Witaj wywoływania aktora hello, dlatego zazwyczaj ułatwia wykrywanie toodefine w miejscu, które jest oddzielić od hello aktora implementacji i może być współużytkowane przez wiele innych usługi lub aplikacje klienckie.

`HelloWorldActorInterface/src/reliableactor/HelloWorldActor.java`:

```java
public interface HelloWorldActor extends Actor {
    @Readonly   
    CompletableFuture<Integer> getCountAsync();

    CompletableFuture<?> setCountAsync(int count);
}
```

### <a name="actor-service"></a>Usługa aktora
Zawiera to implementacja aktora i kod rejestracji aktora. Klasa aktora Hello implementuje interfejs aktora hello. Jest to, gdzie aktora sieci działa jej.

`HelloWorldActor/src/reliableactor/HelloWorldActorImpl`:

```java
@ActorServiceAttribute(name = "HelloWorldActor.HelloWorldActorService")
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
public class HelloWorldActorImpl extends ReliableActor implements HelloWorldActor {
    Logger logger = Logger.getLogger(this.getClass().getName());

    protected CompletableFuture<?> onActivateAsync() {
        logger.log(Level.INFO, "onActivateAsync");

        return this.stateManager().tryAddStateAsync("count", 0);
    }

    @Override
    public CompletableFuture<Integer> getCountAsync() {
        logger.log(Level.INFO, "Getting current count value");
        return this.stateManager().getStateAsync("count");
    }

    @Override
    public CompletableFuture<?> setCountAsync(int count) {
        logger.log(Level.INFO, "Setting current count value {0}", count);
        return this.stateManager().addOrUpdateStateAsync("count", count, (key, value) -> count > value ? count : value);
    }
}
```

### <a name="actor-registration"></a>Rejestracja aktora
Usługa aktora Hello musi być zarejestrowany w środowisku uruchomieniowym usługi sieć szkieletowa hello typ usługi. W celu dla hello toorun usługi aktora swoich wystąpień aktora, danego typu aktora również musi być zarejestrowany hello usługi aktora. Witaj `ActorRuntime` metoda rejestracji wykonuje tej pracy dla osób.

`HelloWorldActor/src/reliableactor/HelloWorldActorHost`:

```java
public class HelloWorldActorHost {

    public static void main(String[] args) throws Exception {

        try {
            ActorRuntime.registerActorAsync(HelloWorldActorImpl.class, (context, actorType) -> new ActorServiceImpl(context, actorType, ()-> new HelloWorldActorImpl()), Duration.ofSeconds(10));

            Thread.sleep(Long.MAX_VALUE);

        } catch (Exception e) {
            e.printStackTrace();
            throw e;
        }
    }
}
```

### <a name="test-client"></a>Klient testowy
To jest aplikacją kliencką prosty test można uruchomić osobno z tootest aplikacji usługi sieć szkieletowa hello usługi aktora. To jest przykład gdzie hello ActorProxy może być używane tooactivate i komunikować się z wystąpieniami aktora. Pobierz nie wdrożone przy użyciu usługi.

### <a name="hello-application"></a>Aplikacja Hello
Ponadto pakiety aplikacji hello hello usługi aktora i innych usług, dodawany w hello przyszłych razem dla wdrożenia. Zawiera on hello *ApplicationManifest.xml* i symbole zastępcze dla pakietu z hello aktora.

## <a name="run-hello-application"></a>Uruchamianie aplikacji hello

Witaj narzędzia Yeoman szkieletów zawiera narzędzia gradle skryptu toobuild hello aplikacji i bash skrypty toodeploy i Usuń aplikację. Aplikacja hello toodeploy, pierwsza aplikacja hello kompilacji z narzędziem gradle:

```bash
$ gradle
```

Spowoduje to utworzenie pakietu aplikacji sieci szkieletowej usług, które można wdrożyć przy użyciu narzędzi interfejsu wiersza polecenia usługi sieci szkieletowej.

### <a name="deploy-service-fabric-cli"></a>Wdrażanie usługi sieci szkieletowej interfejsu wiersza polecenia

skrypt install.sh Hello zawiera hello niezbędne usługi sieci szkieletowej interfejsu wiersza polecenia (sfctl) polecenia toodeploy hello pakietu aplikacji.
Uruchom hello install.sh skryptu toodeploy hello aplikacji.

```bash
$ ./install.sh
```

## <a name="next-steps"></a>Następne kroki

* [Getting started with Service Fabric CLI (Wprowadzenie do interfejsu wiersza polecenia usługi Service Fabric)](service-fabric-cli.md)
