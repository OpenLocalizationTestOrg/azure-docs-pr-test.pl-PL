---
title: "Migracja z zestawu Java SDK do narzędzia Maven — aktualizowanie starych aplikacji Java usługi Azure Service Fabric w celu korzystania z narzędzia Maven | Microsoft Docs"
description: "Aktualizowanie starszych aplikacji Java korzystających z zestawu SDK Java usługi Service Fabric w celu pobrania zależności Java usługi Service Fabric z narzędzia Maven. Po ukończeniu tej konfiguracji starsze aplikacje Java będą mogły obsługiwać kompilację."
services: service-fabric
documentationcenter: java
author: rapatchi
manager: timlt
editor: 
ms.assetid: bf84458f-4b87-4de1-9844-19909e368deb
ms.service: service-fabric
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/23/2017
ms.author: rapatchi
ms.openlocfilehash: 229a2cd7c0bb355006349e80b12b0142de6b5cda
ms.sourcegitcommit: 1fbaa2ccda2fb826c74755d42a31835d9d30e05f
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/22/2018
---
# <a name="update-your-previous-java-service-fabric-application-to-fetch-java-libraries-from-maven"></a>Aktualizowanie starszych aplikacji Java usługi Service Fabric w celu pobierania bibliotek z narzędzia Maven
Ostatnio przenieśliśmy biblioteki Java usługi Service Fabric z zestawu SDK Java usługi Service Fabric do hostingu Maven. Teraz możesz używać repozytorium **mavencentral** do pobierania najnowszych zależności Java usługi Service Fabric. Ten artykuł Szybki start pomaga zaktualizować istniejące aplikacje Java, wcześniej utworzone do użycia z zestawem SDK Java usługi Service Fabric (przy użyciu szablonu Yeoman lub środowiska Eclipse), aby były zgodne z kompilacją bazującą na narzędziu Maven.

## <a name="prerequisites"></a>Wymagania wstępne
1. Najpierw musisz odinstalować istniejący zestaw SDK Java.

  ```bash
  sudo dpkg -r servicefabricsdkjava
  ```
2. Zainstaluj najnowszy interfejs wiersza polecenia usługi Service Fabric, wykonując kroki wymienione [tutaj](service-fabric-cli.md).

3. Aby kompilować aplikacje Java usługi Service Fabric i pracować nad nimi, upewnij się, że zainstalowano zestaw JDK 1.8 i narzędzie Gradle. Jeśli ich jeszcze nie zainstalowano, możesz uruchomić następujące polecenia, aby zainstalować zestaw JDK 1.8 (openjdk-8-jdk) i narzędzie Gradle:

 ```bash
 sudo apt-get install openjdk-8-jdk-headless
 sudo apt-get install gradle
 ```
4. Zaktualizuj skrypty instalacji/dezinstalacji aplikacji w celu używania nowego interfejsu wiersza polecenia usługi Service Fabric, wykonując kroki wymienione [tutaj](service-fabric-application-lifecycle-sfctl.md). Możesz skorzystać z naszych [przykładów](https://github.com/Azure-Samples/service-fabric-java-getting-started) ułatwiających rozpoczęcie pracy.

>[!TIP]
> Po odinstalowaniu zestawu SDK Java usługi Service Fabric narzędzie Yeoman nie będzie działać. Spełnij wymagania wstępne opisane [tutaj](service-fabric-create-your-first-linux-application-with-java.md), aby mieć działający generator szablonów Yeoman usługi Service Fabric dla języka Java.

## <a name="service-fabric-java-libraries-on-maven"></a>Biblioteki Java usługi Service Fabric w narzędziu Maven
Biblioteki Java usługi Service Fabric są teraz hostowane w narzędziu Maven. Zależności możesz dodać w pliku ``pom.xml`` lub ``build.gradle`` projektów, aby używać bibliotek Java usługi Service Fabric z repozytorium **mavenCentral**.

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

Obsługa warstwy transportowej dla aplikacji Java usługi Service Fabric. Nie trzeba jawnie dodawać tej zależności do aplikacji Reliable Actors lub aplikacji usługi, chyba że programujesz w warstwie transportowej.

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

Obsługa na poziomie systemu dla usługi Service Fabric, która komunikuje się z natywnym środowiskiem uruchomieniowym usługi Service Fabric. Nie trzeba jawnie dodawać tej zależności do aplikacji Reliable Actors lub aplikacji usługi. Jest ona automatycznie pobierana z narzędzia Maven, kiedy uwzględnisz pozostałe powyższe zależności.

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


## <a name="migrating-service-fabric-stateless-service"></a>Migrowanie usługi bezstanowej usługi Service Fabric

Aby móc kompilować istniejącą usługę bezstanową Java usługi Service Fabric przy użyciu zależności pobieranych z narzędzia Maven, musisz zaktualizować plik ``build.gradle`` wewnątrz usługi. Wcześniej wyglądał on następująco:
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
    compile project(':Interface')
}
.
.
.
jar {
    manifest {
    attributes(
                'Main-Class': 'statelessservice.MyStatelessServiceHost',
                "Class-Path": configurations.compile.collect { 'lib/' + it.getName() }.join(' '))
    baseName "MyStateless"
    destinationDir = file('./../MyStatelessApplication/MyStatelessPkg/Code')
}
.
.
.
task copyDeps <<{
    copy {
        from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
        into("./../MyStatelessApplication/MyStatelessPkg/Code/lib")
        include('*.jar')
    }
    copy {
        from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
        into("./../MyStatelessApplication/MyStatelessPkg/Code/lib")
        include('libj*.so')
    }
}
```
Teraz, aby pobierać zależności z Maven, odpowiednie części **zaktualizowanego** pliku ``build.gradle`` powinny wyglądać następująco:
```
repositories {
        mavenCentral()
}

configurations {
    azuresf
}

dependencies {
    compile project(':Interface')
    azuresf ('com.microsoft.servicefabric:sf-services-preview:0.10.0')
    compile fileTree(dir: 'lib', include: '*.jar')
}

task explodeDeps(type: Copy, dependsOn:configurations.azuresf) { task ->
    configurations.azuresf.filter { it.toString().contains("native-preview") }.each{
        from zipTree(it)
    }
    configurations.azuresf.filter { !it.toString().contains("native-preview") }.each {
        from it
    }
    into "lib"
    include "libj*.so", "*.jar"
}

compileJava.dependsOn(explodeDeps)
.
.
.
jar {
    manifest {
        def mpath = configurations.compile.collect {'lib/'+it.getName()}.join (' ')
        mpath = mpath + ' ' + configurations.azuresf.collect {'lib/'+it.getName()}.join (' ')
        attributes(
                'Main-Class': 'statelessservice.MyStatelessServiceHost',
                "Class-Path": mpath)
    baseName "MyStateless"
    destinationDir = file('./../MyStatelessApplication/MyStatelessPkg/Code')
   }
}
.
.
.
task copyDeps <<{
    copy {
        from("lib/")
        into("./../MyStatelessApplication/MyStatelessPkg/Code/lib")
        include('*')
    }
}
```
Aby zyskać ogólne pojęcie o tym, jak będzie wyglądać skrypt kompilacji dla usługi bezstanowej Java usługi Service Fabric, możesz odwołać się do dowolnego przykładu w naszych przykładach ułatwiających rozpoczęcie pracy. Tutaj znajdziesz plik [build.gradle](https://github.com/Azure-Samples/service-fabric-java-getting-started/blob/master/Services/EchoServer/EchoServer1.0/EchoServerService/build.gradle) dla przykładu serwera EchoServer.

## <a name="migrating-service-fabric-actor-service"></a>Migrowanie usługi aktora usługi Service Fabric

Aby móc kompilować istniejącą aplikację Java aktora usługi Service Fabric przy użyciu zależności pobieranych z narzędzia Maven, musisz zaktualizować plik ``build.gradle`` wewnątrz pakietu interfejsu i w pakiecie usługi. Jeśli masz pakiet TestClient, również musisz go zaktualizować. A więc dla Twojej aktora ``Myactor`` należałoby zaktualizować go w następujących miejscach:
```
./Myactor/build.gradle
./MyactorInterface/build.gradle
./MyactorTestClient/build.gradle
```

#### <a name="updating-build-script-for-the-interface-project"></a>Aktualizowanie skryptu kompilacji dla projektu interfejsu

Wcześniej wyglądał on następująco:
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
}
.
.
```
Teraz, aby pobierać zależności z Maven, odpowiednie części **zaktualizowanego** pliku ``build.gradle`` powinny wyglądać następująco:
```
repositories {
    mavenCentral()
}

configurations {
    azuresf
}

dependencies {
    azuresf ('com.microsoft.servicefabric:sf-actors-preview:0.10.0')
    compile fileTree(dir: 'lib', include: '*.jar')
}

task explodeDeps(type: Copy, dependsOn:configurations.azuresf) { task ->
    configurations.azuresf.filter { it.toString().contains("native-preview") }.each{
        from zipTree(it)
    }
    configurations.azuresf.filter { !it.toString().contains("native-preview") }.each {
        from it
    }
    into "lib"
    include "libj*.so", "*.jar"
}

compileJava.dependsOn(explodeDeps)
.
.
```

#### <a name="updating-build-script-for-the-actor-project"></a>Aktualizowanie skryptu kompilacji dla projektu aktora

Wcześniej wyglądał on następująco:
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
    compile project(':MyactorInterface')
}
.
.
.
jar {
    manifest {
    attributes(
                'Main-Class': 'reliableactor.MyactorHost',
                "Class-Path": configurations.compile.collect { 'lib/' + it.getName() }.join(' '))
      baseName "myactor"
    destinationDir = file('./../myjavaapp/MyactorPkg/Code')
    }
}
.
.
.
task copyDeps<< {
    copy {
        from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
        into("./../myjavaapp/MyactorPkg/Code/lib")
        include('*.jar')
    }
    copy {
        from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
        into("./../myjavaapp/MyactorPkg/Code/lib")
        include('libj*.so')
    }
    copy {
        from("../MyactorInterface/out/lib")
        into("./../myjavaapp/MyactorPkg/Code/lib")
        include('*.jar')
    }
}
```
Teraz, aby pobierać zależności z Maven, odpowiednie części **zaktualizowanego** pliku ``build.gradle`` powinny wyglądać następująco:
```
repositories {
    mavenCentral()
}

configurations {
    azuresf
}

dependencies {
    compile project(':MyactorInterface')
    azuresf ('com.microsoft.servicefabric:sf-actors-preview:0.10.0')
    compile fileTree(dir: 'lib', include: '*.jar')
}

task explodeDeps(type: Copy, dependsOn:configurations.azuresf) { task ->
    configurations.azuresf.filter { it.toString().contains("native-preview") }.each{
        from zipTree(it)
    }
    configurations.azuresf.filter { !it.toString().contains("native-preview") }.each {
        from it
    }
    into "lib"
    include "libj*.so", "*.jar"
}

compileJava.dependsOn(explodeDeps)
.
.
.
jar {
    manifest {
        def mpath = configurations.compile.collect {'lib/'+it.getName()}.join (' ')
        mpath = mpath + ' ' + configurations.azuresf.collect {'lib/'+it.getName()}.join (' ')
        attributes(
                'Main-Class': 'reliableactor.MyactorHost',
                "Class-Path": mpath)
    baseName "myactor"
    destinationDir = file('../myjavaapp/MyactorPkg/Code')}
 }
.
.
.
task copyDeps<< {
      copy {
              from("lib/")
              into("../myjavaapp/MyactorPkg/Code/lib")
              include('*')
      }
      copy {
              from("../MyactorInterface/out/lib")
              into("../myjavaapp/MyactorPkg/Code/lib")
              include('*.jar')
      }
}
```

#### <a name="updating-build-script-for-the-test-client-project"></a>Aktualizowanie skryptu kompilacji dla projektu klienta testowego

Zmiany tutaj są podobne do zmian opisanych w poprzedniej sekcji, dotyczącej projektu aktora. Wcześniej skrypt Gradle wyglądał następująco:
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
      compile project(':MyactorInterface')
}
.
.
.
jar
{
    manifest {
    attributes(
        'Main-Class': 'reliableactor.test.MyactorTestClient',
        "Class-Path": configurations.compile.collect { 'lib/' + it.getName() }.join(' '))
    }
    baseName "myactor-test"
  destinationDir = file('out/lib')
}
.
.
.
task copyDeps<< {
        copy {
                from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
                into("./out/lib/lib")
                include('*.jar')
        }
        copy {
                from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
                into("./out/lib/lib")
                include('libj*.so')
        }
        copy {
                from("../MyactorInterface/out/lib")
                into("./out/lib/lib")
                include('*.jar')
        }
}
```
Teraz, aby pobierać zależności z Maven, odpowiednie części **zaktualizowanego** pliku ``build.gradle`` powinny wyglądać następująco:
```
repositories {
    mavenCentral()
}

configurations {
    azuresf
}

dependencies {
    compile project(':MyactorInterface')
    azuresf ('com.microsoft.servicefabric:sf-actors-preview:0.10.0')
    compile fileTree(dir: 'lib', include: '*.jar')
}

task explodeDeps(type: Copy, dependsOn:configurations.azuresf) { task ->
    configurations.azuresf.filter { it.toString().contains("native-preview") }.each{
        from zipTree(it)
    }
    configurations.azuresf.filter { !it.toString().contains("native-preview") }.each {
        from it
    }
    into "lib"
    include "libj*.so", "*.jar"
}

compileJava.dependsOn(explodeDeps)
.
.
.
jar
{
    manifest {
        def mpath = configurations.compile.collect {'lib/'+it.getName()}.join (' ')
        mpath = mpath + ' ' + configurations.azuresf.collect {'lib/'+it.getName()}.join (' ')
    attributes(
                'Main-Class': 'reliableactor.test.MyactorTestClient',
                "Class-Path": mpath)
    baseName "myactor-test"
    destinationDir = file('./out/lib')
        }
}
.
.
.
task copyDeps<< {
        copy {
                from("lib/")
                into("./out/lib/lib")
                include('*')
        }
        copy {
                from("../MyactorInterface/out/lib")
                into("./out/lib/lib")
                include('*.jar')
        }
}
```

## <a name="next-steps"></a>Następne kroki

* [Create and deploy your first Service Fabric Java application on Linux using Yeoman](service-fabric-create-your-first-linux-application-with-java.md) (Tworzenie i wdrażanie pierwszej aplikacji Java usługi Service Fabric w systemie Linux przy użyciu programu Yeoman)
* [Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse](service-fabric-get-started-eclipse.md) (Tworzenie i wdrażanie pierwszej aplikacji Java usługi Service Fabric w systemie Linux przy użyciu wtyczki usługi Service Fabric dla środowiska Eclipse)
* [Interact with Service Fabric clusters using the Service Fabric CLI (Interakcja z klastrami usługi Service Fabric przy użyciu interfejsu wiersza polecenia usługi Service Fabric)](service-fabric-cli.md)
