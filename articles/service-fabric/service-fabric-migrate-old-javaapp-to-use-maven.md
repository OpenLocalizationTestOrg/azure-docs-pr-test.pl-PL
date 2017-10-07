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
# <a name="update-your-previous-java-service-fabric-application-toofetch-java-libraries-from-maven"></a><span data-ttu-id="ab50a-104">Zaktualizuj poprzedniej Java sieci szkieletowej usług aplikacji toofetch Java bibliotek z Maven</span><span class="sxs-lookup"><span data-stu-id="ab50a-104">Update your previous Java Service Fabric application toofetch Java libraries from Maven</span></span>
<span data-ttu-id="ab50a-105">Pliki binarne usługi sieć szkieletowa Java niedawno został przeniesiony z hello zestawu SDK usług sieci szkieletowej Java tooMaven hosting.</span><span class="sxs-lookup"><span data-stu-id="ab50a-105">We have recently moved Service Fabric Java binaries from hello Service Fabric Java SDK tooMaven hosting.</span></span> <span data-ttu-id="ab50a-106">Teraz można używać **mavencentral** toofetch hello najnowsze zależności usługi sieci szkieletowej Java.</span><span class="sxs-lookup"><span data-stu-id="ab50a-106">Now you can use **mavencentral** toofetch hello latest Service Fabric Java dependencies.</span></span> <span data-ttu-id="ab50a-107">Dzięki temu szybki start, zaktualizuj istniejących aplikacji Java, które wcześniej utworzone toobe używane z SDK Java usługi sieci szkieletowej, przy użyciu albo narzędzia Yeoman szablon lub Eclipse, toobe zgodny z hello Maven na podstawie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="ab50a-107">This quick-start helps you update your existing Java applications, which you earlier created toobe used with Service Fabric Java SDK, using either Yeoman template or Eclipse, toobe compatible with hello Maven based build.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ab50a-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ab50a-108">Prerequisites</span></span>
1. <span data-ttu-id="ab50a-109">Najpierw należy toouninstall hello istniejącego zestawu Java SDK.</span><span class="sxs-lookup"><span data-stu-id="ab50a-109">First you need toouninstall hello existing Java SDK.</span></span>

  ```bash
  sudo dpkg -r servicefabricsdkjava
  ```
2. <span data-ttu-id="ab50a-110">Najnowsze następujące usługi sieci szkieletowej interfejsu wiersza polecenia instalacji hello hello czynności wymienionych [tutaj](service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="ab50a-110">Install hello latest Service Fabric CLI following hello steps mentioned [here](service-fabric-cli.md).</span></span>

3. <span data-ttu-id="ab50a-111">toobuild i pracy w aplikacji Java sieci szkieletowej usług hello należy tooensure, że masz JDK 1.8 i zainstalowane narzędzia Gradle.</span><span class="sxs-lookup"><span data-stu-id="ab50a-111">toobuild and work on hello Service Fabric Java applications, you need tooensure that you have JDK 1.8 and Gradle installed.</span></span> <span data-ttu-id="ab50a-112">Jeśli nie został jeszcze zainstalowany, możesz uruchomić hello następujących tooinstall 1.8 JDK (openjdk-8-jdk) i Gradle -</span><span class="sxs-lookup"><span data-stu-id="ab50a-112">If not yet installed, you can run hello following tooinstall JDK 1.8 (openjdk-8-jdk) and Gradle -</span></span>

 ```bash
 sudo apt-get install openjdk-8-jdk-headless
 sudo apt-get install gradle
 ```
4. <span data-ttu-id="ab50a-113">Aktualizacja hello Instalowanie/Odinstalowywanie skrypty toouse Twojej aplikacji hello nowej usługi sieci szkieletowej interfejsu wiersza polecenia następujące kroki hello wymienionych [tutaj](service-fabric-application-lifecycle-sfctl.md).</span><span class="sxs-lookup"><span data-stu-id="ab50a-113">Update hello install/uninstall scripts of your application toouse hello new Service Fabric CLI following hello steps mentioned [here](service-fabric-application-lifecycle-sfctl.md).</span></span> <span data-ttu-id="ab50a-114">Może się odwoływać tooour — wprowadzenie [przykłady](https://github.com/Azure-Samples/service-fabric-java-getting-started) odwołania.</span><span class="sxs-lookup"><span data-stu-id="ab50a-114">You can refer tooour getting-started [examples](https://github.com/Azure-Samples/service-fabric-java-getting-started) for reference.</span></span>

>[!TIP]
> <span data-ttu-id="ab50a-115">Po odinstalowaniu hello zestawu SDK usług sieci szkieletowej Java narzędzia Yeoman nie będzie działać.</span><span class="sxs-lookup"><span data-stu-id="ab50a-115">After uninstalling hello Service Fabric Java SDK, Yeoman will not work.</span></span> <span data-ttu-id="ab50a-116">Wykonaj hello wymagania wstępne wymienione [tutaj](service-fabric-create-your-first-linux-application-with-java.md) toohave Java narzędzia usługi sieć szkieletowa Yeoman generatora szablonu w górę i działa.</span><span class="sxs-lookup"><span data-stu-id="ab50a-116">Follow hello Prerequisites mentioned [here](service-fabric-create-your-first-linux-application-with-java.md) toohave Service Fabric Yeoman Java template generator up and working.</span></span>

## <a name="service-fabric-java-libraries-on-maven"></a><span data-ttu-id="ab50a-117">Biblioteki Java usługi Service Fabric w narzędziu Maven</span><span class="sxs-lookup"><span data-stu-id="ab50a-117">Service Fabric Java libraries on Maven</span></span>
<span data-ttu-id="ab50a-118">Biblioteki Java usługi Service Fabric są teraz hostowane w narzędziu Maven.</span><span class="sxs-lookup"><span data-stu-id="ab50a-118">Service Fabric Java libraries have been hosted in Maven.</span></span> <span data-ttu-id="ab50a-119">Można dodać zależności hello hello ``pom.xml`` lub ``build.gradle`` z bibliotek usługi sieć szkieletowa Java toouse projektów z **mavenCentral**.</span><span class="sxs-lookup"><span data-stu-id="ab50a-119">You can add hello dependencies in hello ``pom.xml`` or ``build.gradle`` of your projects toouse Service Fabric Java libraries from **mavenCentral**.</span></span>

### <a name="actors"></a><span data-ttu-id="ab50a-120">Aktorzy</span><span class="sxs-lookup"><span data-stu-id="ab50a-120">Actors</span></span>

<span data-ttu-id="ab50a-121">Obsługa interfejsu Reliable Actors usługi Service Fabric dla Twojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ab50a-121">Service Fabric Reliable Actor support for your application.</span></span>

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

### <a name="services"></a><span data-ttu-id="ab50a-122">Usługi</span><span class="sxs-lookup"><span data-stu-id="ab50a-122">Services</span></span>

<span data-ttu-id="ab50a-123">Obsługa usługi bezstanowej usługi Service Fabric dla Twojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ab50a-123">Service Fabric Stateless Service support for your application.</span></span>

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

### <a name="others"></a><span data-ttu-id="ab50a-124">Inne</span><span class="sxs-lookup"><span data-stu-id="ab50a-124">Others</span></span>
#### <a name="transport"></a><span data-ttu-id="ab50a-125">Transport</span><span class="sxs-lookup"><span data-stu-id="ab50a-125">Transport</span></span>

<span data-ttu-id="ab50a-126">Obsługa warstwy transportowej dla aplikacji Java usługi Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ab50a-126">Transport layer support for Service Fabric Java application.</span></span> <span data-ttu-id="ab50a-127">Nie trzeba tooexplicitly dodawać tej zależności tooyour niezawodnego aktora lub aplikacje usług, chyba że program na powitania warstwy transportowej.</span><span class="sxs-lookup"><span data-stu-id="ab50a-127">You do not need tooexplicitly add this dependency tooyour Reliable Actor or Service applications, unless you program at hello transport layer.</span></span>

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

#### <a name="fabric-support"></a><span data-ttu-id="ab50a-128">Obsługa usługi Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ab50a-128">Fabric support</span></span>

<span data-ttu-id="ab50a-129">System poziomu obsługę sieci szkieletowej usług, który zawiera środowisko uruchomieniowe usługi sieć szkieletowa toonative.</span><span class="sxs-lookup"><span data-stu-id="ab50a-129">System level support for Service Fabric, which talks toonative Service Fabric runtime.</span></span> <span data-ttu-id="ab50a-130">Nie trzeba tooexplicitly Dodawanie tej zależności tooyour niezawodnego aktora lub aplikacji usługi.</span><span class="sxs-lookup"><span data-stu-id="ab50a-130">You do not need tooexplicitly add this dependency tooyour Reliable Actor or Service applications.</span></span> <span data-ttu-id="ab50a-131">Pobiera pobrania automatycznie z Maven, po dołączeniu hello innych zależności powyżej.</span><span class="sxs-lookup"><span data-stu-id="ab50a-131">This gets fetched automatically from Maven, when you include hello other dependencies above.</span></span>

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


## <a name="migrating-service-fabric-stateless-service"></a><span data-ttu-id="ab50a-132">Migrowanie usługi bezstanowej usługi Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ab50a-132">Migrating Service Fabric Stateless Service</span></span>

<span data-ttu-id="ab50a-133">toobe toobuild możliwe do istniejącej sieci szkieletowej usług bezstanowych Java usługi przy użyciu zależności usługi sieć szkieletowa pobranych z Maven, potrzebujesz tooupdate hello ``build.gradle`` pliku wewnątrz hello usługi.</span><span class="sxs-lookup"><span data-stu-id="ab50a-133">toobe able toobuild your existing Service Fabric stateless Java service using Service Fabric dependencies fetched from Maven, you need tooupdate hello ``build.gradle`` file inside hello Service.</span></span> <span data-ttu-id="ab50a-134">Wcześniej toobe, takie jak jego używane w następujący sposób-</span><span class="sxs-lookup"><span data-stu-id="ab50a-134">Previously it used toobe like as follows -</span></span>
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
<span data-ttu-id="ab50a-135">Teraz, hello toofetch hello zależności z Maven, **zaktualizowane** ``build.gradle`` byłyby odpowiednie części hello następujący -</span><span class="sxs-lookup"><span data-stu-id="ab50a-135">Now, toofetch hello dependencies from Maven, hello **updated** ``build.gradle`` would have hello corresponding parts as follows -</span></span>
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
<span data-ttu-id="ab50a-136">Ogólnie rzecz biorąc tooget pomysł ogólną o sposobie hello tworzenia skryptu będzie wyglądała usługi sieć szkieletowa usług bezstanowych Java, tooany próbki mogą odwoływać się w naszych przykładach — wprowadzenie.</span><span class="sxs-lookup"><span data-stu-id="ab50a-136">In general, tooget an overall idea about how hello build script would look like for a Service Fabric stateless Java service, you can refer tooany sample from our getting-started examples.</span></span> <span data-ttu-id="ab50a-137">Oto hello [build.gradle](https://github.com/Azure-Samples/service-fabric-java-getting-started/blob/master/Services/EchoServer/EchoServer1.0/EchoServerService/build.gradle) hello EchoServer próbki.</span><span class="sxs-lookup"><span data-stu-id="ab50a-137">Here is hello [build.gradle](https://github.com/Azure-Samples/service-fabric-java-getting-started/blob/master/Services/EchoServer/EchoServer1.0/EchoServerService/build.gradle) for hello EchoServer sample.</span></span>

## <a name="migrating-service-fabric-actor-service"></a><span data-ttu-id="ab50a-138">Migrowanie usługi aktora usługi Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ab50a-138">Migrating Service Fabric Actor Service</span></span>

<span data-ttu-id="ab50a-139">toobe toobuild stanie istniejącej aplikacji Java aktora sieci szkieletowej usług za pomocą zależności usługi sieć szkieletowa pobranych z Maven, potrzebujesz tooupdate hello ``build.gradle`` plików w pakiecie interfejsu hello i w pakiecie usługi hello.</span><span class="sxs-lookup"><span data-stu-id="ab50a-139">toobe able toobuild your existing Service Fabric Actor Java application using Service Fabric dependencies fetched from Maven, you need tooupdate hello ``build.gradle`` file inside hello interface package and in hello Service package.</span></span> <span data-ttu-id="ab50a-140">Jeśli masz pakiet TestClient, należy to również tooupdate.</span><span class="sxs-lookup"><span data-stu-id="ab50a-140">If you have a TestClient package, you need tooupdate that as well.</span></span> <span data-ttu-id="ab50a-141">Tak, dla Twojej aktora ``Myactor``, następujące hello byłoby hello miejsc, w których należy tooupdate -</span><span class="sxs-lookup"><span data-stu-id="ab50a-141">So, for your actor ``Myactor``, hello following would be hello places where you need tooupdate -</span></span>
```
./Myactor/build.gradle
./MyactorInterface/build.gradle
./MyactorTestClient/build.gradle
```

#### <a name="updating-build-script-for-hello-interface-project"></a><span data-ttu-id="ab50a-142">Aktualizowanie kompilacji skryptu dla projektu interfejsu hello</span><span class="sxs-lookup"><span data-stu-id="ab50a-142">Updating build script for hello interface project</span></span>

<span data-ttu-id="ab50a-143">Wcześniej toobe, takie jak jego używane w następujący sposób-</span><span class="sxs-lookup"><span data-stu-id="ab50a-143">Previously it used toobe like as follows -</span></span>
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
}
.
.
```
<span data-ttu-id="ab50a-144">Teraz, hello toofetch hello zależności z Maven, **zaktualizowane** ``build.gradle`` byłyby odpowiednie części hello następujący -</span><span class="sxs-lookup"><span data-stu-id="ab50a-144">Now, toofetch hello dependencies from Maven, hello **updated** ``build.gradle`` would have hello corresponding parts as follows -</span></span>
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

#### <a name="updating-build-script-for-hello-actor-project"></a><span data-ttu-id="ab50a-145">Aktualizowanie kompilacji skryptu dla hello aktora projektu</span><span class="sxs-lookup"><span data-stu-id="ab50a-145">Updating build script for hello actor project</span></span>

<span data-ttu-id="ab50a-146">Wcześniej toobe, takie jak jego używane w następujący sposób-</span><span class="sxs-lookup"><span data-stu-id="ab50a-146">Previously it used toobe like as follows -</span></span>
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
<span data-ttu-id="ab50a-147">Teraz, hello toofetch hello zależności z Maven, **zaktualizowane** ``build.gradle`` byłyby odpowiednie części hello następujący -</span><span class="sxs-lookup"><span data-stu-id="ab50a-147">Now, toofetch hello dependencies from Maven, hello **updated** ``build.gradle`` would have hello corresponding parts as follows -</span></span>
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

#### <a name="updating-build-script-for-hello-test-client-project"></a><span data-ttu-id="ab50a-148">Aktualizowanie skryptu kompilacji projektu klienta testowego hello</span><span class="sxs-lookup"><span data-stu-id="ab50a-148">Updating build script for hello test client project</span></span>

<span data-ttu-id="ab50a-149">Zmiany w tym miejscu są podobne zmiany toohello opisanych w poprzedniej sekcji, to znaczy hello aktora projektu.</span><span class="sxs-lookup"><span data-stu-id="ab50a-149">Changes here are similar toohello changes discussed in previous section, that is, hello actor project.</span></span> <span data-ttu-id="ab50a-150">Wcześniej hello toobe skryptu używanego w następujący sposób — takich jak narzędzia Gradle</span><span class="sxs-lookup"><span data-stu-id="ab50a-150">Previously hello Gradle script used toobe like as follows -</span></span>
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
<span data-ttu-id="ab50a-151">Teraz, hello toofetch hello zależności z Maven, **zaktualizowane** ``build.gradle`` byłyby odpowiednie części hello następujący -</span><span class="sxs-lookup"><span data-stu-id="ab50a-151">Now, toofetch hello dependencies from Maven, hello **updated** ``build.gradle`` would have hello corresponding parts as follows -</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="ab50a-152">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ab50a-152">Next steps</span></span>

* <span data-ttu-id="ab50a-153">[Create and deploy your first Service Fabric Java application on Linux using Yeoman](service-fabric-create-your-first-linux-application-with-java.md) (Tworzenie i wdrażanie pierwszej aplikacji Java usługi Service Fabric w systemie Linux przy użyciu programu Yeoman)</span><span class="sxs-lookup"><span data-stu-id="ab50a-153">[Create and deploy your first Service Fabric Java application on Linux by using Yeoman](service-fabric-create-your-first-linux-application-with-java.md)</span></span>
* <span data-ttu-id="ab50a-154">[Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse](service-fabric-get-started-eclipse.md) (Tworzenie i wdrażanie pierwszej aplikacji Java usługi Service Fabric w systemie Linux przy użyciu wtyczki usługi Service Fabric dla środowiska Eclipse)</span><span class="sxs-lookup"><span data-stu-id="ab50a-154">[Create and deploy your first Service Fabric Java application on Linux by using Service Fabric Plugin for Eclipse](service-fabric-get-started-eclipse.md)</span></span>
* [<span data-ttu-id="ab50a-155">Interakcji z klastrami usługi sieć szkieletowa usług za pomocą hello usługi sieci szkieletowej interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="ab50a-155">Interact with Service Fabric clusters using hello Service Fabric CLI</span></span>](service-fabric-cli.md)
