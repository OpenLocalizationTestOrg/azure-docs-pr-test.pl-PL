---
title: "aaaMigrate z zestawu Java SDK tooMaven — aktualizacja starego aplikacji Java sieci szkieletowej usług Azure toouse Maven | Dokumentacja firmy Microsoft"
description: "Aktualizacja hello starszych aplikacji Java wykorzystujące hello toouse zestawu SDK Java sieci szkieletowej usług, zależności usługi sieci szkieletowej Java toofetch z Maven. Po ukończeniu tej konfiguracji starszych aplikacji Java będą mogli toobuild."
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
ms.date: 08/23/2017
ms.author: saysa
ms.openlocfilehash: 11b979facd7b3865141a6d3a035a6021dd06ca0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="update-your-previous-java-service-fabric-application-toofetch-java-libraries-from-maven"></a>Zaktualizuj poprzedniej Java sieci szkieletowej usług aplikacji toofetch Java bibliotek z Maven
Pliki binarne usługi sieć szkieletowa Java niedawno został przeniesiony z hello zestawu SDK usług sieci szkieletowej Java tooMaven hosting. Teraz można używać **mavencentral** toofetch hello najnowsze zależności usługi sieci szkieletowej Java. Dzięki temu szybki start, zaktualizuj istniejących aplikacji Java, które wcześniej utworzone toobe używane z SDK Java usługi sieci szkieletowej, przy użyciu albo narzędzia Yeoman szablon lub Eclipse, toobe zgodny z hello Maven na podstawie kompilacji.

## <a name="prerequisites"></a>Wymagania wstępne
1. Najpierw należy toouninstall hello istniejącego zestawu Java SDK.

  ```bash
  sudo dpkg -r servicefabricsdkjava
  ```
2. Najnowsze następujące usługi sieci szkieletowej interfejsu wiersza polecenia instalacji hello hello czynności wymienionych [tutaj](service-fabric-cli.md).

3. toobuild i pracy w aplikacji Java sieci szkieletowej usług hello należy tooensure, że masz JDK 1.8 i zainstalowane narzędzia Gradle. Jeśli nie został jeszcze zainstalowany, możesz uruchomić hello następujących tooinstall 1.8 JDK (openjdk-8-jdk) i Gradle -

 ```bash
 sudo apt-get install openjdk-8-jdk-headless
 sudo apt-get install gradle
 ```
4. Aktualizacja hello Instalowanie/Odinstalowywanie skrypty toouse Twojej aplikacji hello nowej usługi sieci szkieletowej interfejsu wiersza polecenia następujące kroki hello wymienionych [tutaj](service-fabric-application-lifecycle-sfctl.md). Może się odwoływać tooour — wprowadzenie [przykłady](https://github.com/Azure-Samples/service-fabric-java-getting-started) odwołania.

>[!TIP]
> Po odinstalowaniu hello zestawu SDK usług sieci szkieletowej Java narzędzia Yeoman nie będzie działać. Wykonaj hello wymagania wstępne wymienione [tutaj](service-fabric-create-your-first-linux-application-with-java.md) toohave Java narzędzia usługi sieć szkieletowa Yeoman generatora szablonu w górę i działa.

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


## <a name="migrating-service-fabric-stateless-service"></a>Migrowanie usługi bezstanowej usługi Service Fabric

toobe toobuild możliwe do istniejącej sieci szkieletowej usług bezstanowych Java usługi przy użyciu zależności usługi sieć szkieletowa pobranych z Maven, potrzebujesz tooupdate hello ``build.gradle`` pliku wewnątrz hello usługi. Wcześniej toobe, takie jak jego używane w następujący sposób-
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
Teraz, hello toofetch hello zależności z Maven, **zaktualizowane** ``build.gradle`` byłyby odpowiednie części hello następujący -
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
Ogólnie rzecz biorąc tooget pomysł ogólną o sposobie hello tworzenia skryptu będzie wyglądała usługi sieć szkieletowa usług bezstanowych Java, tooany próbki mogą odwoływać się w naszych przykładach — wprowadzenie. Oto hello [build.gradle](https://github.com/Azure-Samples/service-fabric-java-getting-started/blob/master/Services/EchoServer/EchoServer1.0/EchoServerService/build.gradle) hello EchoServer próbki.

## <a name="migrating-service-fabric-actor-service"></a>Migrowanie usługi aktora usługi Service Fabric

toobe toobuild stanie istniejącej aplikacji Java aktora sieci szkieletowej usług za pomocą zależności usługi sieć szkieletowa pobranych z Maven, potrzebujesz tooupdate hello ``build.gradle`` plików w pakiecie interfejsu hello i w pakiecie usługi hello. Jeśli masz pakiet TestClient, należy to również tooupdate. Tak, dla Twojej aktora ``Myactor``, następujące hello byłoby hello miejsc, w których należy tooupdate -
```
./Myactor/build.gradle
./MyactorInterface/build.gradle
./MyactorTestClient/build.gradle
```

#### <a name="updating-build-script-for-hello-interface-project"></a>Aktualizowanie kompilacji skryptu dla projektu interfejsu hello

Wcześniej toobe, takie jak jego używane w następujący sposób-
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
}
.
.
```
Teraz, hello toofetch hello zależności z Maven, **zaktualizowane** ``build.gradle`` byłyby odpowiednie części hello następujący -
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

#### <a name="updating-build-script-for-hello-actor-project"></a>Aktualizowanie kompilacji skryptu dla hello aktora projektu

Wcześniej toobe, takie jak jego używane w następujący sposób-
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
Teraz, hello toofetch hello zależności z Maven, **zaktualizowane** ``build.gradle`` byłyby odpowiednie części hello następujący -
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

#### <a name="updating-build-script-for-hello-test-client-project"></a>Aktualizowanie skryptu kompilacji projektu klienta testowego hello

Zmiany w tym miejscu są podobne zmiany toohello opisanych w poprzedniej sekcji, to znaczy hello aktora projektu. Wcześniej hello toobe skryptu używanego w następujący sposób — takich jak narzędzia Gradle
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
Teraz, hello toofetch hello zależności z Maven, **zaktualizowane** ``build.gradle`` byłyby odpowiednie części hello następujący -
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
* [Interakcji z klastrami usługi sieć szkieletowa usług za pomocą hello usługi sieci szkieletowej interfejsu wiersza polecenia](service-fabric-cli.md)
