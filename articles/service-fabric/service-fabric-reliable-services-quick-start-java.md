---
title: "aaaCreate Twojego pierwszego niezawodnej mikrousługi Azure w języku Java | Dokumentacja firmy Microsoft"
description: "Wprowadzenie toocreating aplikację usługi sieć szkieletowa usług Microsoft Azure z usług bezstanowych i stanowych."
services: service-fabric
documentationcenter: java
author: vturecek
manager: timlt
editor: 
ms.assetid: 7831886f-7ec4-4aef-95c5-b2469a5b7b5d
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 577d96591797bbfe6be5c1094426b5f1435cca0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-reliable-services"></a>Wprowadzenie do usług Reliable Services
> [!div class="op_single_selector"]
> * [C# w systemie Windows](service-fabric-reliable-services-quick-start.md)
> * [Java w systemie Linux](service-fabric-reliable-services-quick-start-java.md)
>
>

W tym artykule opisano podstawy hello Azure Usługa sieci szkieletowej niezawodnej usługi oraz przedstawiono sposób tworzenia i wdrażania prostą aplikację niezawodnej usługi napisane w języku Java. Ten film Microsoft Virtual Academy również przedstawiono toocreate bezstanowej niezawodnej usługi:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965">  
<img src="./media/service-fabric-reliable-services-quick-start-java/ReliableServicesJavaVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="installation-and-setup"></a>Instalacja i Konfiguracja
Przed rozpoczęciem upewnij się, że masz środowisko projektowania sieci szkieletowej usług hello na tym komputerze.
Jeśli potrzebujesz tooset go, przejdź do zbyt[wprowadzenie dla komputerów Mac](service-fabric-get-started-mac.md) lub [wprowadzenie w systemie Linux](service-fabric-get-started-linux.md).

## <a name="basic-concepts"></a>Podstawowe pojęcia
tooget pracy z usługami Reliable Services, musisz tylko należy toounderstand kilka podstawowych pojęć:

* **Typ usługi**: jest to implementacji usługi. Jest on zdefiniowany przez klasę hello pisania, rozszerzający `StatelessService` i innego kodu lub zależności używany, oraz nazwę i numer wersji.
* **Nazwane wystąpienie usługi**: toorun usługi tworzenia nazwanego wystąpienia danego typu usługi znacznie tak, jak utworzyć wystąpienia obiektu typu klasy. Wystąpienie usługi są w istocie wystąpieniami klasie usługi, który można zapisać obiektu.
* **Host usługi**: hello nazwane wystąpienia usługi, utworzyć toorun potrzeby wewnątrz hosta. host usługi Hello jest właśnie procesu, których można uruchomić wystąpienia usługi.
* **Usługa rejestracji**: rejestracji, połączono wszystko. Witaj typ usługi musi być zarejestrowana z hello sieci szkieletowej usług środowiska uruchomieniowego w usłudze hosta tooallow sieci szkieletowej usług toocreate wystąpień toorun.  

## <a name="create-a-stateless-service"></a>Tworzenie usługi bezstanowej
Rozpocznij od utworzenia aplikacji sieci szkieletowej usług. Witaj zestawu SDK sieci szkieletowej usług dla systemu Linux zawiera narzędzia Yeoman generator tooprovide hello szkieletów dla aplikacji sieci szkieletowej usług za pomocą usługi bezstanowej. Zacznij od uruchomienia hello następujące narzędzia Yeoman polecenia:

```bash
$ yo azuresfjava
```

Wykonaj hello instrukcje toocreate **usługi bezstanowej niezawodnej**. W tym samouczku aplikacji hello nazwy "HelloWorldApplication" i hello usługi "HelloWorld". wynik Hello obejmuje katalogów hello `HelloWorldApplication` i `HelloWorld`.

```bash
HelloWorldApplication/
├── build.gradle
├── HelloWorld
│   ├── build.gradle
│   └── src
│       └── statelessservice
│           ├── HelloWorldServiceHost.java
│           └── HelloWorldService.java
├── HelloWorldApplication
│   ├── ApplicationManifest.xml
│   └── HelloWorldPkg
│       ├── Code
│       │   ├── entryPoint.sh
│       │   └── _readme.txt
│       ├── Config
│       │   └── _readme.txt
│       ├── Data
│       │   └── _readme.txt
│       └── ServiceManifest.xml
├── install.sh
├── settings.gradle
└── uninstall.sh
```

## <a name="implement-hello-service"></a>Wdrożenie usługi hello
Otwórz **HelloWorldApplication/HelloWorld/src/statelessservice/HelloWorldService.java**. Ta klasa definiuje typ usługi hello i można uruchomić dowolny kod. Interfejs API usługi Hello zawiera dwa punkty wejścia kodu:

* Metoda punktu wejścia otwarty, nazywany `runAsync()`, w którym można rozpocząć wykonywania dowolnych zadań, w tym obciążeń obliczeniowych długotrwałe.

```java
@Override
protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {
    ...
}
```

* Punkt wejścia komunikacji, gdzie można podłączyć stosu komunikacji wyboru. Jest to, gdzie można uruchomić odbieranie żądań od użytkowników i innych usług.

```java
@Override
protected List<ServiceInstanceListener> createServiceInstanceListeners() {
    ...
}
```

W tym samouczku, możemy skupić się na powitania `runAsync()` metoda punktu wejścia. Jest to, gdzie natychmiast można rozpocząć uruchamianie kodu.

### <a name="runasync"></a>RunAsync
Platforma Hello wywołuje tę metodę, gdy wystąpienie usługi jest tooexecute umieścić i gotowe. Dla usługi bezstanowej po prostu oznacza to, gdy wystąpienie usługi hello jest otwarty. Token anulowania podano toocoordinate, gdy wystąpienie usługi musi toobe zamknięte. W sieci szkieletowej usług ten cykl otwarcie i zamknięcie wystąpienia usługi może wystąpić wiele razy w ciągu okresu istnienia hello hello usługi jako całość. Może się to zdarzyć z różnych powodów, w tym:

* Hello system przenosi swoich wystąpień usługi dla równoważenia zasobów.
* Błędy występują w kodzie.
* Uaktualnianie aplikacji Hello lub systemu.
* używany sprzęt Hello ulegnie awarii.

Aranżacja jest zarządzana przez sieć szkieletowa usług tookeep usługi wysokiej dostępności i nieprawidłowo zrównoważone.

`runAsync()`nie zablokować synchronicznie. Implementacji runAsync powinien zwrócić CompletableFuture tooallow hello środowiska uruchomieniowego toocontinue. Jeśli obciążenie musi tooimplement długotrwała zadanie, które należy wykonać wewnątrz hello CompletableFuture.

#### <a name="cancellation"></a>Anulowanie
Anulowanie obciążenie jest współpracy wysiłku, zorkiestrowana przez hello podany token anulowania. Hello system oczekuje tooend Twojego zadania (przez pomyślne zakończenie anulowania lub fault) przed przesyłane w. Jest ważne toohonor hello anulowania tokenu, Zakończ wszelkie pracy i zamknięcie `runAsync()` tak szybko jak to możliwe, gdy hello system żądań anulowania. Witaj poniższym przykładzie pokazano, jak toohandle zdarzenia anulowania:

```java
    @Override
    protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {

        // TODO: Replace hello following sample code with your own logic
        // or remove this runAsync override if it's not needed in your service.

        CompletableFuture.runAsync(() -> {
          long iterations = 0;
          while(true)
          {
            cancellationToken.throwIfCancellationRequested();
            logger.log(Level.INFO, "Working-{0}", ++iterations);

            try
            {
              Thread.sleep(1000);
            }
            catch (IOException ex) {}
          }
        });
    }
```

### <a name="service-registration"></a>Rejestracja usługi
Środowisko uruchomieniowe usługi sieć szkieletowa hello musi być zarejestrowany typów usług. Typ usługi Hello jest zdefiniowany w hello `ServiceManifest.xml` i klasie usługi, który implementuje `StatelessService`. Rejestracja usługi jest wykonywane w hello proces główny punkt wejścia. W tym przykładzie hello jest główny punkt wejścia procesu `HelloWorldServiceHost.java`:

```java
public static void main(String[] args) throws Exception {
    try {
        ServiceRuntime.registerStatelessServiceAsync("HelloWorldType", (context) -> new HelloWorldService(), Duration.ofSeconds(10));
        logger.log(Level.INFO, "Registered stateless service type HelloWorldType.");
        Thread.sleep(Long.MAX_VALUE);
    }
    catch (Exception ex) {
        logger.log(Level.SEVERE, "Exception in registration:", ex);
        throw ex;
    }
}
```

## <a name="run-hello-application"></a>Uruchamianie aplikacji hello

Witaj narzędzia Yeoman szkieletów zawiera narzędzia gradle skryptu toobuild hello aplikacji i bash skrypty toodeploy i Usuń aplikację. Aplikacja hello toorun, pierwsza aplikacja hello kompilacji z narzędziem gradle:

```bash
$ gradle
```

Daje to pakiet aplikacji sieci szkieletowej usług, które można wdrożyć przy użyciu interfejsu wiersza polecenia usługi sieci szkieletowej.

### <a name="deploy-with-service-fabric-cli"></a>Wdrażanie z sieci szkieletowej usług interfejsu wiersza polecenia

skrypt install.sh Hello zawiera hello niezbędne usługi sieci szkieletowej interfejsu wiersza polecenia polecenia toodeploy hello pakietu aplikacji. Uruchamianie aplikacji hello toodeploy skryptu install.sh.

```bash
$ ./install.sh
```

## <a name="next-steps"></a>Następne kroki

* [Getting started with Service Fabric CLI (Wprowadzenie do interfejsu wiersza polecenia usługi Service Fabric)](service-fabric-cli.md)
