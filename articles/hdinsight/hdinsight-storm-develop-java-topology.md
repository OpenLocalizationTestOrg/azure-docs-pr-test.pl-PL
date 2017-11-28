---
title: "aaaApache Storm przykładową topologię Java - Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate topologii Apache Storm w języku Java przez utworzenie przykładowego słowa liczba topologii."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: "Apache storm, przykład storm apache storm w języku java, przykład topologii storm"
ms.assetid: a8838f29-9c08-4fd9-99ef-26655d1bf6d7
ms.service: hdinsight
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/07/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: 54fa9dc3c93ddad83ac861f3101f50f80117d804
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-storm-topology-in-java"></a><span data-ttu-id="f90e7-104">Tworzenie topologii Apache Storm w języku Java</span><span class="sxs-lookup"><span data-stu-id="f90e7-104">Create an Apache Storm topology in Java</span></span>

<span data-ttu-id="f90e7-105">Dowiedz się, jak toocreate topologii opartych na języku Java Apache STORM.</span><span class="sxs-lookup"><span data-stu-id="f90e7-105">Learn how toocreate a Java-based topology for Apache Storm.</span></span> <span data-ttu-id="f90e7-106">Możesz utworzyć topologii Storm, która implementuje aplikacji liczba programu word.</span><span class="sxs-lookup"><span data-stu-id="f90e7-106">You create a Storm topology that implements a word-count application.</span></span> <span data-ttu-id="f90e7-107">Możesz użyć Maven toobuild i pakietów hello projektu.</span><span class="sxs-lookup"><span data-stu-id="f90e7-107">You use Maven toobuild and package hello project.</span></span> <span data-ttu-id="f90e7-108">Następnie dowiesz się, jak przy użyciu topologii hello toodefine hello framework strumienia.</span><span class="sxs-lookup"><span data-stu-id="f90e7-108">Then, you learn how toodefine hello topology using hello Flux framework.</span></span>

> [!NOTE]
> <span data-ttu-id="f90e7-109">framework strumień Hello jest dostępna w Storm 0.10.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="f90e7-109">hello Flux framework is available in Storm 0.10.0 or later.</span></span> <span data-ttu-id="f90e7-110">STORM 0.10.0 jest dostępna w HDInsight 3.3 i 3.4.</span><span class="sxs-lookup"><span data-stu-id="f90e7-110">Storm 0.10.0 is available with HDInsight 3.3 and 3.4.</span></span>

<span data-ttu-id="f90e7-111">Po wykonaniu czynności hello w tym dokumencie można wdrożyć hello tooApache topologii Storm w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f90e7-111">After completing hello steps in this document, you can deploy hello topology tooApache Storm on HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="f90e7-112">Ukończoną wersję przykłady topologii Storm hello utworzone w tym dokumencie znajduje się w temacie [https://github.com/Azure-Samples/hdinsight-java-storm-wordcount](https://github.com/Azure-Samples/hdinsight-java-storm-wordcount).</span><span class="sxs-lookup"><span data-stu-id="f90e7-112">A completed version of hello Storm topology examples created in this document is available at [https://github.com/Azure-Samples/hdinsight-java-storm-wordcount](https://github.com/Azure-Samples/hdinsight-java-storm-wordcount).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f90e7-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f90e7-113">Prerequisites</span></span>

* [<span data-ttu-id="f90e7-114">Java Developer Kit (JDK) w wersji 7</span><span class="sxs-lookup"><span data-stu-id="f90e7-114">Java Developer Kit (JDK) version 7</span></span>](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)

* <span data-ttu-id="f90e7-115">[Maven (https://maven.apache.org/download.cgi)](https://maven.apache.org/download.cgi): Maven to system projektu kompilacji dla projektów języka Java.</span><span class="sxs-lookup"><span data-stu-id="f90e7-115">[Maven (https://maven.apache.org/download.cgi)](https://maven.apache.org/download.cgi): Maven is a project build system for Java projects.</span></span>

* <span data-ttu-id="f90e7-116">Edytor tekstu lub IDE.</span><span class="sxs-lookup"><span data-stu-id="f90e7-116">A text editor or IDE.</span></span>

## <a name="configure-environment-variables"></a><span data-ttu-id="f90e7-117">Skonfiguruj zmienne środowiskowe</span><span class="sxs-lookup"><span data-stu-id="f90e7-117">Configure environment variables</span></span>

<span data-ttu-id="f90e7-118">Witaj następujące zmienne środowiskowe mogą zostać ustawione podczas instalacji języka Java i hello JDK.</span><span class="sxs-lookup"><span data-stu-id="f90e7-118">hello following environment variables may be set when you install Java and hello JDK.</span></span> <span data-ttu-id="f90e7-119">Jednak należy sprawdzić, czy istnieją i że zawierają one hello poprawne wartości dla systemu.</span><span class="sxs-lookup"><span data-stu-id="f90e7-119">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="f90e7-120">**JAVA_HOME** -powinny wskazywać katalog toohello zainstalowanym hello środowiska uruchomieniowego (JRE).</span><span class="sxs-lookup"><span data-stu-id="f90e7-120">**JAVA_HOME** - should point toohello directory where hello Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="f90e7-121">Na przykład w systemie Unix lub Linux dystrybucji, powinien on wartość podobną zbyt`/usr/lib/jvm/java-7-oracle`.</span><span class="sxs-lookup"><span data-stu-id="f90e7-121">For example, in a Unix or Linux distribution, it should have a value similar too`/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="f90e7-122">W systemie Windows czy ma on wartość podobną zbyt`c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="f90e7-122">In Windows, it would have a value similar too`c:\Program Files (x86)\Java\jre1.7`</span></span>

* <span data-ttu-id="f90e7-123">**ŚCIEŻKA** -powinien zawierać hello następującej ścieżki:</span><span class="sxs-lookup"><span data-stu-id="f90e7-123">**PATH** - should contain hello following paths:</span></span>

  * <span data-ttu-id="f90e7-124">**JAVA_HOME** (lub równoważne ścieżki hello)</span><span class="sxs-lookup"><span data-stu-id="f90e7-124">**JAVA_HOME** (or hello equivalent path)</span></span>

  * <span data-ttu-id="f90e7-125">**JAVA_HOME\bin** (lub równoważne ścieżki hello)</span><span class="sxs-lookup"><span data-stu-id="f90e7-125">**JAVA_HOME\bin** (or hello equivalent path)</span></span>

  * <span data-ttu-id="f90e7-126">katalog Hello zainstalowanym Maven</span><span class="sxs-lookup"><span data-stu-id="f90e7-126">hello directory where Maven is installed</span></span>

## <a name="create-a-maven-project"></a><span data-ttu-id="f90e7-127">Utwórz projekt Maven</span><span class="sxs-lookup"><span data-stu-id="f90e7-127">Create a Maven project</span></span>

<span data-ttu-id="f90e7-128">Z wiersza polecenia hello, użyj hello następujące polecenie toocreate projekt Maven o nazwie **WordCount**:</span><span class="sxs-lookup"><span data-stu-id="f90e7-128">From hello command line, use hello following command toocreate a Maven project named **WordCount**:</span></span>

```bash
mvn archetype:generate -DarchetypeArtifactId=maven-archetype-quickstart -DgroupId=com.microsoft.example -DartifactId=WordCount -DinteractiveMode=false
```

> [!NOTE]
> <span data-ttu-id="f90e7-129">Jeśli używasz programu PowerShell, należy otoczyć`-D` parametry z cudzysłowami podwójnymi.</span><span class="sxs-lookup"><span data-stu-id="f90e7-129">If you are using PowerShell, you must surround the`-D` parameters with double quotes.</span></span>
>
> `mvn archetype:generate "-DarchetypeArtifactId=maven-archetype-quickstart" "-DgroupId=com.microsoft.example" "-DartifactId=WordCount" "-DinteractiveMode=false"`

<span data-ttu-id="f90e7-130">To polecenie tworzy katalog o nazwie `WordCount` w bieżącej lokalizacji hello, który zawiera podstawowe projekt Maven.</span><span class="sxs-lookup"><span data-stu-id="f90e7-130">This command creates a directory named `WordCount` at hello current location, which contains a basic Maven project.</span></span> <span data-ttu-id="f90e7-131">Witaj `WordCount` katalog zawiera hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="f90e7-131">hello `WordCount` directory contains hello following items:</span></span>

* <span data-ttu-id="f90e7-132">`pom.xml`: Zawiera ustawienia hello projekt Maven.</span><span class="sxs-lookup"><span data-stu-id="f90e7-132">`pom.xml`: Contains settings for hello Maven project.</span></span>
* <span data-ttu-id="f90e7-133">`src\main\java\com\microsoft\example`: Zawiera kod aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f90e7-133">`src\main\java\com\microsoft\example`: Contains your application code.</span></span>
* <span data-ttu-id="f90e7-134">`src\test\java\com\microsoft\example`: Zawiera testy dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f90e7-134">`src\test\java\com\microsoft\example`: Contains tests for your application.</span></span> 

### <a name="remove-hello-generated-example-code"></a><span data-ttu-id="f90e7-135">Usuń wygenerowane hello przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="f90e7-135">Remove hello generated example code</span></span>

<span data-ttu-id="f90e7-136">Usuń hello wygenerowanych testów i pliki aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="f90e7-136">Delete hello generated test and hello application files:</span></span>

* <span data-ttu-id="f90e7-137">**src\test\java\com\microsoft\example\AppTest.Java**</span><span class="sxs-lookup"><span data-stu-id="f90e7-137">**src\test\java\com\microsoft\example\AppTest.java**</span></span>
* <span data-ttu-id="f90e7-138">**src\main\java\com\microsoft\example\App.Java**</span><span class="sxs-lookup"><span data-stu-id="f90e7-138">**src\main\java\com\microsoft\example\App.java**</span></span>

## <a name="add-maven-repositories"></a><span data-ttu-id="f90e7-139">Dodaj repozytoria Maven</span><span class="sxs-lookup"><span data-stu-id="f90e7-139">Add Maven repositories</span></span>

<span data-ttu-id="f90e7-140">HDInsight jest oparta na powitania Hortonworks Data Platform (HDP), dlatego firma Microsoft zaleca używanie hello Hortonworks repozytorium toodownload zależności dla projektów Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="f90e7-140">HDInsight is based on hello Hortonworks Data Platform (HDP), so we recommend using hello Hortonworks repository toodownload dependencies for your Apache Storm projects.</span></span> <span data-ttu-id="f90e7-141">W hello __pom.xml__ plików, Dodaj następujące XML po hello hello `<url>http://maven.apache.org</url>` wiersza:</span><span class="sxs-lookup"><span data-stu-id="f90e7-141">In hello __pom.xml__ file, add hello following XML after hello `<url>http://maven.apache.org</url>` line:</span></span>

```xml
<repositories>
    <repository>
        <releases>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
            <checksumPolicy>warn</checksumPolicy>
        </releases>
        <snapshots>
            <enabled>false</enabled>
            <updatePolicy>never</updatePolicy>
            <checksumPolicy>fail</checksumPolicy>
        </snapshots>
        <id>HDPReleases</id>
        <name>HDP Releases</name>
        <url>http://repo.hortonworks.com/content/repositories/releases/</url>
        <layout>default</layout>
    </repository>
    <repository>
        <releases>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
            <checksumPolicy>warn</checksumPolicy>
        </releases>
        <snapshots>
            <enabled>false</enabled>
            <updatePolicy>never</updatePolicy>
            <checksumPolicy>fail</checksumPolicy>
        </snapshots>
        <id>HDPJetty</id>
        <name>Hadoop Jetty</name>
        <url>http://repo.hortonworks.com/content/repositories/jetty-hadoop/</url>
        <layout>default</layout>
    </repository>
</repositories>
```

## <a name="add-properties"></a><span data-ttu-id="f90e7-142">Dodawanie właściwości</span><span class="sxs-lookup"><span data-stu-id="f90e7-142">Add properties</span></span>

<span data-ttu-id="f90e7-143">Maven umożliwia toodefine wartości Poziom projektu o nazwie właściwości.</span><span class="sxs-lookup"><span data-stu-id="f90e7-143">Maven allows you toodefine project-level values called properties.</span></span> <span data-ttu-id="f90e7-144">W hello __pom.xml__, Dodaj następujące tekstu po hello hello `</repositories>` wiersza:</span><span class="sxs-lookup"><span data-stu-id="f90e7-144">In hello __pom.xml__, add hello following text after hello `</repositories>` line:</span></span>

```xml
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <!--
    This is a version of Storm from hello Hortonworks repository that is compatible with HDInsight.
    -->
    <storm.version>1.0.1.2.5.3.0-37</storm.version>
</properties>
```

<span data-ttu-id="f90e7-145">Tę wartość można teraz używać w innych częściach hello `pom.xml`.</span><span class="sxs-lookup"><span data-stu-id="f90e7-145">You can now use this value in other sections of hello `pom.xml`.</span></span> <span data-ttu-id="f90e7-146">Na przykład podczas określania wersji hello składników systemu Storm, można użyć `${storm.version}` zamiast twardych kodowania wartość.</span><span class="sxs-lookup"><span data-stu-id="f90e7-146">For example, when specifying hello version of Storm components, you can use `${storm.version}` instead of hard coding a value.</span></span>

## <a name="add-dependencies"></a><span data-ttu-id="f90e7-147">Dodaj zależności</span><span class="sxs-lookup"><span data-stu-id="f90e7-147">Add dependencies</span></span>

<span data-ttu-id="f90e7-148">Dodawanie zależności dla składników systemu Storm.</span><span class="sxs-lookup"><span data-stu-id="f90e7-148">Add a dependency for Storm components.</span></span> <span data-ttu-id="f90e7-149">Otwórz hello `pom.xml` plik i dodać hello następującego kodu w hello `<dependencies>` sekcji:</span><span class="sxs-lookup"><span data-stu-id="f90e7-149">Open hello `pom.xml` file and add hello following code in hello `<dependencies>` section:</span></span>

```xml
<dependency>
    <groupId>org.apache.storm</groupId>
    <artifactId>storm-core</artifactId>
    <version>${storm.version}</version>
    <!-- keep storm out of hello jar-with-dependencies -->
    <scope>provided</scope>
</dependency>
```

<span data-ttu-id="f90e7-150">W czasie kompilacji Maven korzysta z tej informacji toolook `storm-core` hello Maven repozytorium.</span><span class="sxs-lookup"><span data-stu-id="f90e7-150">At compile time, Maven uses this information toolook up `storm-core` in hello Maven repository.</span></span> <span data-ttu-id="f90e7-151">Najpierw wyszukiwana w repozytorium hello na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="f90e7-151">It first looks in hello repository on your local computer.</span></span> <span data-ttu-id="f90e7-152">Jeśli nie są pliki hello, Maven pobiera ich z publicznego repozytorium Maven hello i przechowuje je w repozytorium lokalne powitania.</span><span class="sxs-lookup"><span data-stu-id="f90e7-152">If hello files aren't there, Maven downloads them from hello public Maven repository and stores them in hello local repository.</span></span>

> [!NOTE]
> <span data-ttu-id="f90e7-153">Powiadomienie hello `<scope>provided</scope>` wiersza w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="f90e7-153">Notice hello `<scope>provided</scope>` line in this section.</span></span> <span data-ttu-id="f90e7-154">To ustawienie określa, że Maven tooexclude **storm core** z pliki JAR, które są tworzone, ponieważ są dostarczane przez hello system.</span><span class="sxs-lookup"><span data-stu-id="f90e7-154">This setting tells Maven tooexclude **storm-core** from any JAR files that are created, because it is provided by hello system.</span></span>

## <a name="build-configuration"></a><span data-ttu-id="f90e7-155">Konfiguracja kompilacji</span><span class="sxs-lookup"><span data-stu-id="f90e7-155">Build configuration</span></span>

<span data-ttu-id="f90e7-156">Maven dodatków plug-in pozwalają toocustomize hello kompilacji etapach hello projektu.</span><span class="sxs-lookup"><span data-stu-id="f90e7-156">Maven plug-ins allow you toocustomize hello build stages of hello project.</span></span> <span data-ttu-id="f90e7-157">Na przykład sposobu kompilowania projektu hello lub jak toopackage go do pliku JAR.</span><span class="sxs-lookup"><span data-stu-id="f90e7-157">For example, how hello project is compiled or how toopackage it into a JAR file.</span></span> <span data-ttu-id="f90e7-158">Otwórz hello `pom.xml` plik i dodać hello następującego kodu bezpośrednio nad hello `</project>` wiersza.</span><span class="sxs-lookup"><span data-stu-id="f90e7-158">Open hello `pom.xml` file and add hello following code directly above hello `</project>` line.</span></span>

```xml
<build>
    <plugins>
    </plugins>
    <resources>
    </resources>
</build>
```

<span data-ttu-id="f90e7-159">Ta sekcja jest używane tooadd dodatków plug-in, zasobów i innych opcji konfiguracji kompilacji.</span><span class="sxs-lookup"><span data-stu-id="f90e7-159">This section is used tooadd plug-ins, resources, and other build configuration options.</span></span> <span data-ttu-id="f90e7-160">Pełną dokumentację hello **pom.xml** plików, zobacz [http://maven.apache.org/pom.html](http://maven.apache.org/pom.html).</span><span class="sxs-lookup"><span data-stu-id="f90e7-160">For a full reference of hello **pom.xml** file, see [http://maven.apache.org/pom.html](http://maven.apache.org/pom.html).</span></span>

### <a name="add-plug-ins"></a><span data-ttu-id="f90e7-161">Dodawanie wtyczki</span><span class="sxs-lookup"><span data-stu-id="f90e7-161">Add plug-ins</span></span>

<span data-ttu-id="f90e7-162">Dla topologii Apache Storm w języku Java, hello [wtyczki Maven Exec](http://www.mojohaus.org/exec-maven-plugin/) jest przydatne, ponieważ umożliwia tooeasily uruchomić topologii hello lokalnie w środowisku projektowania.</span><span class="sxs-lookup"><span data-stu-id="f90e7-162">For Apache Storm topologies implemented in Java, hello [Exec Maven Plugin](http://www.mojohaus.org/exec-maven-plugin/) is useful because it allows you tooeasily run hello topology locally in your development environment.</span></span> <span data-ttu-id="f90e7-163">Dodaj następujące toohello hello `<plugins>` sekcji hello `pom.xml` pliku tooinclude hello Exec Maven wtyczki:</span><span class="sxs-lookup"><span data-stu-id="f90e7-163">Add hello following toohello `<plugins>` section of hello `pom.xml` file tooinclude hello Exec Maven plugin:</span></span>

```xml
<plugin>
    <groupId>org.codehaus.mojo</groupId>
    <artifactId>exec-maven-plugin</artifactId>
    <version>1.4.0</version>
    <executions>
    <execution>
    <goals>
        <goal>exec</goal>
    </goals>
    </execution>
    </executions>
    <configuration>
    <executable>java</executable>
    <includeProjectDependencies>true</includeProjectDependencies>
    <includePluginDependencies>false</includePluginDependencies>
    <classpathScope>compile</classpathScope>
    <mainClass>${storm.topology}</mainClass>
    <cleanupDaemonThreads>false</cleanupDaemonThreads> 
    </configuration>
</plugin>
```

<span data-ttu-id="f90e7-164">Inny przydatne dodatek jest hello [Apache Maven kompilatora wtyczki](http://maven.apache.org/plugins/maven-compiler-plugin/), która jest używana toochange opcje kompilacji.</span><span class="sxs-lookup"><span data-stu-id="f90e7-164">Another useful plug-in is hello [Apache Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/), which is used toochange compilation options.</span></span> <span data-ttu-id="f90e7-165">zmiany Hello hello wersję Java, używającego Maven hello źródłowa i docelowa dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f90e7-165">hello changes hello Java version that Maven uses for hello source and target for your application.</span></span>

* <span data-ttu-id="f90e7-166">Dla usługi HDInsight __3.4 lub starszym__, ustaw źródło hello i docelowymi too__1.7__ wersji języka Java.</span><span class="sxs-lookup"><span data-stu-id="f90e7-166">For HDInsight __3.4 or earlier__, set hello source and target Java version too__1.7__.</span></span>

* <span data-ttu-id="f90e7-167">Dla usługi HDInsight __3.5__, ustaw źródło hello i docelowymi too__1.8__ wersji języka Java.</span><span class="sxs-lookup"><span data-stu-id="f90e7-167">For HDInsight __3.5__, set hello source and target Java version too__1.8__.</span></span>

<span data-ttu-id="f90e7-168">Dodaj następującego tekstu w hello hello `<plugins>` sekcji hello `pom.xml` pliku tooinclude hello Apache Maven kompilatora wtyczki.</span><span class="sxs-lookup"><span data-stu-id="f90e7-168">Add hello following text in hello `<plugins>` section of hello `pom.xml` file tooinclude hello Apache Maven Compiler plugin.</span></span> <span data-ttu-id="f90e7-169">W tym przykładzie określa 1.8, tak aby hello docelowej usługi HDInsight w wersji 3.5.</span><span class="sxs-lookup"><span data-stu-id="f90e7-169">This example specifies 1.8, so hello target HDInsight version is 3.5.</span></span>

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-compiler-plugin</artifactId>
    <version>3.3</version>
    <configuration>
    <source>1.8</source>
    <target>1.8</target>
    </configuration>
</plugin>
```

### <a name="configure-resources"></a><span data-ttu-id="f90e7-170">Konfigurowanie zasobów</span><span class="sxs-lookup"><span data-stu-id="f90e7-170">Configure resources</span></span>

<span data-ttu-id="f90e7-171">sekcja zasobów Hello umożliwia tooinclude-code zasobów takich jak pliki konfiguracji wymagane przez składniki w topologii hello.</span><span class="sxs-lookup"><span data-stu-id="f90e7-171">hello resources section allows you tooinclude non-code resources such as configuration files needed by components in hello topology.</span></span> <span data-ttu-id="f90e7-172">Na przykład dodać hello następującego tekstu w hello `<resources>` sekcji hello "plik pom.xml.</span><span class="sxs-lookup"><span data-stu-id="f90e7-172">For this example, add hello following text in hello `<resources>` section of hello \`pom.xml file.</span></span>

```xml
<resource>
    <directory>${basedir}/resources</directory>
    <filtering>false</filtering>
    <includes>
        <include>log4j2.xml</include>
    </includes>
</resource>
```

<span data-ttu-id="f90e7-173">W tym przykładzie dodaje hello katalogu zasobów w katalogu głównym hello hello projektu (`${basedir}`) jako lokalizację, która zawiera zasoby i obejmuje hello plik o nazwie `log4j2.xml`.</span><span class="sxs-lookup"><span data-stu-id="f90e7-173">This example adds hello resources directory in hello root of hello project (`${basedir}`) as a location that contains resources, and includes hello file named `log4j2.xml`.</span></span> <span data-ttu-id="f90e7-174">Ten plik jest używany tooconfigure informacjach jest rejestrowane przez hello topologii.</span><span class="sxs-lookup"><span data-stu-id="f90e7-174">This file is used tooconfigure what information is logged by hello topology.</span></span>

## <a name="create-hello-topology"></a><span data-ttu-id="f90e7-175">Tworzenie topologii hello</span><span class="sxs-lookup"><span data-stu-id="f90e7-175">Create hello topology</span></span>

<span data-ttu-id="f90e7-176">Topologia opartych na języku Java Apache Storm składa się z trzech składników, które należy utworzyć (lub odwołania) jako zależność.</span><span class="sxs-lookup"><span data-stu-id="f90e7-176">A Java-based Apache Storm topology consists of three components that you must author (or reference) as a dependency.</span></span>

* <span data-ttu-id="f90e7-177">**Spouts**: odczytuje dane z zewnętrznego źródła i emituje strumieni danych w topologii hello.</span><span class="sxs-lookup"><span data-stu-id="f90e7-177">**Spouts**: Reads data from external sources and emits streams of data into hello topology.</span></span>

* <span data-ttu-id="f90e7-178">**Bolts**: przetwarza strumieni emitowane przez elementach spout lub innych elementów bolt i emituje jeden lub więcej strumieni.</span><span class="sxs-lookup"><span data-stu-id="f90e7-178">**Bolts**: Performs processing on streams emitted by spouts or other bolts, and emits one or more streams.</span></span>

* <span data-ttu-id="f90e7-179">**Topologia**: definiuje sposób hello spouts i elementów bolt ułożone i zapewnia punkt wejścia hello hello topologii.</span><span class="sxs-lookup"><span data-stu-id="f90e7-179">**Topology**: Defines how hello spouts and bolts are arranged, and provides hello entry point for hello topology.</span></span>

### <a name="create-hello-spout"></a><span data-ttu-id="f90e7-180">Utwórz elementy spout hello</span><span class="sxs-lookup"><span data-stu-id="f90e7-180">Create hello spout</span></span>

<span data-ttu-id="f90e7-181">Witaj tooreduce wymagania dotyczące konfigurowania zewnętrznych źródeł danych, następujące elementy spout po prostu emituje losowe zdań.</span><span class="sxs-lookup"><span data-stu-id="f90e7-181">tooreduce requirements for setting up external data sources, hello following spout simply emits random sentences.</span></span> <span data-ttu-id="f90e7-182">Jest zmodyfikowanej wersji spout, udostępniana z hello [przykłady z projektu Storm Starter](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter).</span><span class="sxs-lookup"><span data-stu-id="f90e7-182">It is a modified version of a spout that is provided with hello [Storm-Starter examples](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter).</span></span>

> [!NOTE]
> <span data-ttu-id="f90e7-183">Na przykład spout, która odczytuje z zewnętrznego źródła danych Zobacz jedną z hello następujące przykłady:</span><span class="sxs-lookup"><span data-stu-id="f90e7-183">For an example of a spout that reads from an external data source, see one of hello following examples:</span></span>
>
> * <span data-ttu-id="f90e7-184">[TwitterSampleSPout](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter/spout/TwitterSampleSpout.java): spout przykład, która odczytuje z serwisem Twitter</span><span class="sxs-lookup"><span data-stu-id="f90e7-184">[TwitterSampleSPout](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter/spout/TwitterSampleSpout.java): An example spout that reads from Twitter</span></span>
> * <span data-ttu-id="f90e7-185">[STORM Kafka](https://github.com/apache/storm/tree/0.10.x-branch/external/storm-kafka): spout, która odczytuje z Kafka</span><span class="sxs-lookup"><span data-stu-id="f90e7-185">[Storm-Kafka](https://github.com/apache/storm/tree/0.10.x-branch/external/storm-kafka): A spout that reads from Kafka</span></span>

<span data-ttu-id="f90e7-186">Dla hello spout, Utwórz plik o nazwie `RandomSentenceSpout.java` w hello `src\main\java\com\microsoft\example` hello katalogu i użyj następującego kodu języka Java jako zawartość hello:</span><span class="sxs-lookup"><span data-stu-id="f90e7-186">For hello spout, create a file named `RandomSentenceSpout.java` in hello `src\main\java\com\microsoft\example` directory and use hello following Java code as hello contents:</span></span>

```java
package com.microsoft.example;

import org.apache.storm.spout.SpoutOutputCollector;
import org.apache.storm.task.TopologyContext;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseRichSpout;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Values;
import org.apache.storm.utils.Utils;

import java.util.Map;
import java.util.Random;

//This spout randomly emits sentences
public class RandomSentenceSpout extends BaseRichSpout {
  //Collector used tooemit output
  SpoutOutputCollector _collector;
  //Used toogenerate a random number
  Random _rand;

  //Open is called when an instance of hello class is created
  @Override
  public void open(Map conf, TopologyContext context, SpoutOutputCollector collector) {
  //Set hello instance collector toohello one passed in
    _collector = collector;
    //For randomness
    _rand = new Random();
  }

  //Emit data toohello stream
  @Override
  public void nextTuple() {
  //Sleep for a bit
    Utils.sleep(100);
    //hello sentences that are randomly emitted
    String[] sentences = new String[]{ "hello cow jumped over hello moon", "an apple a day keeps hello doctor away",
        "four score and seven years ago", "snow white and hello seven dwarfs", "i am at two with nature" };
    //Randomly pick a sentence
    String sentence = sentences[_rand.nextInt(sentences.length)];
    //Emit hello sentence
    _collector.emit(new Values(sentence));
  }

  //Ack is not implemented since this is a basic example
  @Override
  public void ack(Object id) {
  }

  //Fail is not implemented since this is a basic example
  @Override
  public void fail(Object id) {
  }

  //Declare hello output fields. In this case, an sentence
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("sentence"));
  }
}
```

> [!NOTE]
> <span data-ttu-id="f90e7-187">Mimo że ta topologia używa tylko jeden spout, inne mogą zawierać kilka, które do topologii hello strumieniowe źródło danych z różnych źródeł.</span><span class="sxs-lookup"><span data-stu-id="f90e7-187">Although this topology uses only one spout, others may have several that feed data from different sources into hello topology.</span></span>

### <a name="create-hello-bolts"></a><span data-ttu-id="f90e7-188">Tworzenie elementów bolt hello</span><span class="sxs-lookup"><span data-stu-id="f90e7-188">Create hello bolts</span></span>

<span data-ttu-id="f90e7-189">Elementów bolt obsługi hello przetwarzania danych.</span><span class="sxs-lookup"><span data-stu-id="f90e7-189">Bolts handle hello data processing.</span></span> <span data-ttu-id="f90e7-190">Ta topologia używa dwóch elementów bolt:</span><span class="sxs-lookup"><span data-stu-id="f90e7-190">This topology uses two bolts:</span></span>

* <span data-ttu-id="f90e7-191">**SplitSentence**: dzieli zdań hello emitowane przez **RandomSentenceSpout** do poszczególnych wyrazów.</span><span class="sxs-lookup"><span data-stu-id="f90e7-191">**SplitSentence**: Splits hello sentences emitted by **RandomSentenceSpout** into individual words.</span></span>

* <span data-ttu-id="f90e7-192">**WordCount**: zlicza, ile razy podczas każdego wyrazu.</span><span class="sxs-lookup"><span data-stu-id="f90e7-192">**WordCount**: Counts how many times each word has occurred.</span></span>

> [!NOTE]
> <span data-ttu-id="f90e7-193">Można to zrobić niczego, na przykład obliczeń, trwałości lub mówić składniki tooexternal elementów bolt.</span><span class="sxs-lookup"><span data-stu-id="f90e7-193">Bolts can do anything, for example, computation, persistence, or talking tooexternal components.</span></span>

<span data-ttu-id="f90e7-194">Utwórz dwa nowe pliki `SplitSentence.java` i `WordCount.java` w hello `src\main\java\com\microsoft\example` katalogu.</span><span class="sxs-lookup"><span data-stu-id="f90e7-194">Create two new files, `SplitSentence.java` and `WordCount.java` in hello `src\main\java\com\microsoft\example` directory.</span></span> <span data-ttu-id="f90e7-195">Użyj hello następującego tekstu jako zawartość hello hello plików:</span><span class="sxs-lookup"><span data-stu-id="f90e7-195">Use hello following text as hello contents for hello files:</span></span>

#### <a name="splitsentence"></a><span data-ttu-id="f90e7-196">SplitSentence</span><span class="sxs-lookup"><span data-stu-id="f90e7-196">SplitSentence</span></span>

```java
package com.microsoft.example;

import java.text.BreakIterator;

import org.apache.storm.topology.BasicOutputCollector;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseBasicBolt;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Tuple;
import org.apache.storm.tuple.Values;

//There are a variety of bolt types. In this case, use BaseBasicBolt
public class SplitSentence extends BaseBasicBolt {

  //Execute is called tooprocess tuples
  @Override
  public void execute(Tuple tuple, BasicOutputCollector collector) {
    //Get hello sentence content from hello tuple
    String sentence = tuple.getString(0);
    //An iterator tooget each word
    BreakIterator boundary=BreakIterator.getWordInstance();
    //Give hello iterator hello sentence
    boundary.setText(sentence);
    //Find hello beginning first word
    int start=boundary.first();
    //Iterate over each word and emit it toohello output stream
    for (int end=boundary.next(); end != BreakIterator.DONE; start=end, end=boundary.next()) {
      //get hello word
      String word=sentence.substring(start,end);
      //If a word is whitespace characters, replace it with empty
      word=word.replaceAll("\\s+","");
      //if it's an actual word, emit it
      if (!word.equals("")) {
        collector.emit(new Values(word));
      }
    }
  }

  //Declare that emitted tuples contain a word field
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("word"));
  }
}
```

#### <a name="wordcount"></a><span data-ttu-id="f90e7-197">WordCount</span><span class="sxs-lookup"><span data-stu-id="f90e7-197">WordCount</span></span>

```java
package com.microsoft.example;

import java.util.HashMap;
import java.util.Map;
import java.util.Iterator;

import org.apache.storm.Constants;
import org.apache.storm.topology.BasicOutputCollector;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseBasicBolt;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Tuple;
import org.apache.storm.tuple.Values;
import org.apache.storm.Config;

// For logging
import org.apache.logging.log4j.Logger;
import org.apache.logging.log4j.LogManager;

//There are a variety of bolt types. In this case, use BaseBasicBolt
public class WordCount extends BaseBasicBolt {
  //Create logger for this class
  private static final Logger logger = LogManager.getLogger(WordCount.class);
  //For holding words and counts
  Map<String, Integer> counts = new HashMap<String, Integer>();
  //How often tooemit a count of words
  private Integer emitFrequency;

  // Default constructor
  public WordCount() {
      emitFrequency=5; // Default too60 seconds
  }

  // Constructor that sets emit frequency
  public WordCount(Integer frequency) {
      emitFrequency=frequency;
  }

  //Configure frequency of tick tuples for this bolt
  //This delivers a 'tick' tuple on a specific interval,
  //which is used tootrigger certain actions
  @Override
  public Map<String, Object> getComponentConfiguration() {
      Config conf = new Config();
      conf.put(Config.TOPOLOGY_TICK_TUPLE_FREQ_SECS, emitFrequency);
      return conf;
  }

  //execute is called tooprocess tuples
  @Override
  public void execute(Tuple tuple, BasicOutputCollector collector) {
    //If it's a tick tuple, emit all words and counts
    if(tuple.getSourceComponent().equals(Constants.SYSTEM_COMPONENT_ID)
            && tuple.getSourceStreamId().equals(Constants.SYSTEM_TICK_STREAM_ID)) {
      for(String word : counts.keySet()) {
        Integer count = counts.get(word);
        collector.emit(new Values(word, count));
        logger.info("Emitting a count of " + count + " for word " + word);
      }
    } else {
      //Get hello word contents from hello tuple
      String word = tuple.getString(0);
      //Have we counted any already?
      Integer count = counts.get(word);
      if (count == null)
        count = 0;
      //Increment hello count and store it
      count++;
      counts.put(word, count);
    }
  }

  //Declare that this emits a tuple containing two fields; word and count
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("word", "count"));
  }
}
```

### <a name="define-hello-topology"></a><span data-ttu-id="f90e7-198">Zdefiniuj topologię hello</span><span class="sxs-lookup"><span data-stu-id="f90e7-198">Define hello topology</span></span>

<span data-ttu-id="f90e7-199">Topologia Hello wiąże elementach spout hello i bolts ze sobą do wykresu, który definiuje sposób dane przepływają między składnikami hello.</span><span class="sxs-lookup"><span data-stu-id="f90e7-199">hello topology ties hello spouts and bolts together into a graph, which defines how data flows between hello components.</span></span> <span data-ttu-id="f90e7-200">Umożliwia także wskazówki równoległości, Storm używane podczas tworzenia wystąpienia hello składników w klastrze hello przez.</span><span class="sxs-lookup"><span data-stu-id="f90e7-200">It also provides parallelism hints that Storm uses when creating instances of hello components within hello cluster.</span></span>

<span data-ttu-id="f90e7-201">Witaj poniższy obraz jest diagram podstawowy wykresu hello składników dla tej topologii.</span><span class="sxs-lookup"><span data-stu-id="f90e7-201">hello following image is a basic diagram of hello graph of components for this topology.</span></span>

![Diagram przedstawiający hello spouts i bolts rozmieszczenie](./media/hdinsight-storm-develop-java-topology/wordcount-topology.png)

<span data-ttu-id="f90e7-203">tooimplement hello topologii, Utwórz plik o nazwie `WordCountTopology.java` w hello `src\main\java\com\microsoft\example` katalogu.</span><span class="sxs-lookup"><span data-stu-id="f90e7-203">tooimplement hello topology, create a file named `WordCountTopology.java` in hello `src\main\java\com\microsoft\example` directory.</span></span> <span data-ttu-id="f90e7-204">Użyj następującego kodu języka Java jako hello zawartość pliku hello hello:</span><span class="sxs-lookup"><span data-stu-id="f90e7-204">Use hello following Java code as hello contents of hello file:</span></span>

```java
package com.microsoft.example;

import org.apache.storm.Config;
import org.apache.storm.LocalCluster;
import org.apache.storm.StormSubmitter;
import org.apache.storm.topology.TopologyBuilder;
import org.apache.storm.tuple.Fields;

import com.microsoft.example.RandomSentenceSpout;

public class WordCountTopology {

  //Entry point for hello topology
  public static void main(String[] args) throws Exception {
  //Used toobuild hello topology
    TopologyBuilder builder = new TopologyBuilder();
    //Add hello spout, with a name of 'spout'
    //and parallelism hint of 5 executors
    builder.setSpout("spout", new RandomSentenceSpout(), 5);
    //Add hello SplitSentence bolt, with a name of 'split'
    //and parallelism hint of 8 executors
    //shufflegrouping subscribes toohello spout, and equally distributes
    //tuples (sentences) across instances of hello SplitSentence bolt
    builder.setBolt("split", new SplitSentence(), 8).shuffleGrouping("spout");
    //Add hello counter, with a name of 'count'
    //and parallelism hint of 12 executors
    //fieldsgrouping subscribes toohello split bolt, and
    //ensures that hello same word is sent toohello same instance (group by field 'word')
    builder.setBolt("count", new WordCount(), 12).fieldsGrouping("split", new Fields("word"));

    //new configuration
    Config conf = new Config();
    //Set toofalse toodisable debug information when
    // running in production on a cluster
    conf.setDebug(false);

    //If there are arguments, we are running on a cluster
    if (args != null && args.length > 0) {
      //parallelism hint tooset hello number of workers
      conf.setNumWorkers(3);
      //submit hello topology
      StormSubmitter.submitTopology(args[0], conf, builder.createTopology());
    }
    //Otherwise, we are running locally
    else {
      //Cap hello maximum number of executors that can be spawned
      //for a component too3
      conf.setMaxTaskParallelism(3);
      //LocalCluster is used toorun locally
      LocalCluster cluster = new LocalCluster();
      //submit hello topology
      cluster.submitTopology("word-count", conf, builder.createTopology());
      //sleep
      Thread.sleep(10000);
      //shut down hello cluster
      cluster.shutdown();
    }
  }
}
```

### <a name="configure-logging"></a><span data-ttu-id="f90e7-205">Konfigurowanie rejestrowania</span><span class="sxs-lookup"><span data-stu-id="f90e7-205">Configure logging</span></span>

<span data-ttu-id="f90e7-206">STORM używa Apache Log4j toolog informacji.</span><span class="sxs-lookup"><span data-stu-id="f90e7-206">Storm uses Apache Log4j toolog information.</span></span> <span data-ttu-id="f90e7-207">Jeśli rejestrowanie nie zostanie skonfigurowane, topologii hello emituje informacje diagnostyczne.</span><span class="sxs-lookup"><span data-stu-id="f90e7-207">If you do not configure logging, hello topology emits diagnostic information.</span></span> <span data-ttu-id="f90e7-208">toocontrol, co jest rejestrowane, Utwórz plik o nazwie `log4j2.xml` w hello `resources` katalogu.</span><span class="sxs-lookup"><span data-stu-id="f90e7-208">toocontrol what is logged, create a file named `log4j2.xml` in hello `resources` directory.</span></span> <span data-ttu-id="f90e7-209">Użyj powitania po jako zawartość hello hello pliku XML.</span><span class="sxs-lookup"><span data-stu-id="f90e7-209">Use hello following XML as hello contents of hello file.</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Configuration>
<Appenders>
    <Console name="STDOUT" target="SYSTEM_OUT">
        <PatternLayout pattern="%d{HH:mm:ss} [%t] %-5level %logger{36} - %msg%n"/>
    </Console>
</Appenders>
<Loggers>
    <Logger name="com.microsoft.example" level="trace" additivity="false">
        <AppenderRef ref="STDOUT"/>
    </Logger>
    <Root level="error">
        <Appender-Ref ref="STDOUT"/>
    </Root>
</Loggers>
</Configuration>
```

<span data-ttu-id="f90e7-210">Plik XML Konfiguruje nowy rejestratora dla hello `com.microsoft.example` klasy, która obejmuje składniki hello w tym przykładzie topologii.</span><span class="sxs-lookup"><span data-stu-id="f90e7-210">This XML configures a new logger for hello `com.microsoft.example` class, which includes hello components in this example topology.</span></span> <span data-ttu-id="f90e7-211">poziom Hello jest ustawiany tootrace dla tego rejestratora, który przechwytuje informacje rejestrowania emitowane przez składniki w tej topologii.</span><span class="sxs-lookup"><span data-stu-id="f90e7-211">hello level is set tootrace for this logger, which captures any logging information emitted by components in this topology.</span></span>

<span data-ttu-id="f90e7-212">Witaj `<Root level="error">` sekcji konfiguruje hello główny poziom rejestrowania (wszystko, co nie `com.microsoft.example`) informacje o błędzie tooonly dziennika.</span><span class="sxs-lookup"><span data-stu-id="f90e7-212">hello `<Root level="error">` section configures hello root level of logging (everything not in `com.microsoft.example`) tooonly log error information.</span></span>

<span data-ttu-id="f90e7-213">Aby uzyskać więcej informacji na temat konfigurowania rejestrowanie dla narzędzia Log4j, zobacz [http://logging.apache.org/log4j/2.x/manual/configuration.html](http://logging.apache.org/log4j/2.x/manual/configuration.html).</span><span class="sxs-lookup"><span data-stu-id="f90e7-213">For more information on configuring logging for Log4j, see [http://logging.apache.org/log4j/2.x/manual/configuration.html](http://logging.apache.org/log4j/2.x/manual/configuration.html).</span></span>

> [!NOTE]
> <span data-ttu-id="f90e7-214">STORM w wersji 0.10.0 i wyższe użycie narzędzia Log4j 2.x.</span><span class="sxs-lookup"><span data-stu-id="f90e7-214">Storm version 0.10.0 and higher use Log4j 2.x.</span></span> <span data-ttu-id="f90e7-215">Starsze wersje storm używane Log4j 1.x, którego użyć innego formatu dla konfiguracji dziennika.</span><span class="sxs-lookup"><span data-stu-id="f90e7-215">Older versions of storm used Log4j 1.x, which used a different format for log configuration.</span></span> <span data-ttu-id="f90e7-216">Uzyskać informacji o konfiguracji starsze hello, zobacz [http://wiki.apache.org/logging-log4j/Log4jXmlFormat](http://wiki.apache.org/logging-log4j/Log4jXmlFormat).</span><span class="sxs-lookup"><span data-stu-id="f90e7-216">For information on hello older configuration, see [http://wiki.apache.org/logging-log4j/Log4jXmlFormat](http://wiki.apache.org/logging-log4j/Log4jXmlFormat).</span></span>

## <a name="test-hello-topology-locally"></a><span data-ttu-id="f90e7-217">Test hello lokalnie topologii</span><span class="sxs-lookup"><span data-stu-id="f90e7-217">Test hello topology locally</span></span>

<span data-ttu-id="f90e7-218">Po zapisaniu plików hello, należy użyć hello następujące polecenia tootest hello topologii lokalnie.</span><span class="sxs-lookup"><span data-stu-id="f90e7-218">After you save hello files, use hello following command tootest hello topology locally.</span></span>

```bash
mvn compile exec:java -Dstorm.topology=com.microsoft.example.WordCountTopology
```

<span data-ttu-id="f90e7-219">Podczas wykonywania, topologii hello Wyświetla informacje o uruchamianiu.</span><span class="sxs-lookup"><span data-stu-id="f90e7-219">As it runs, hello topology displays startup information.</span></span> <span data-ttu-id="f90e7-220">Witaj następujący tekst jest przykład danych wyjściowych liczba word hello:</span><span class="sxs-lookup"><span data-stu-id="f90e7-220">hello following text is an example of hello word count output:</span></span>

    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
    17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word snow

<span data-ttu-id="f90e7-221">Ten przykładowy dziennik wskazuje wyrazie hello "i" zostały wyemitowane 113 razy.</span><span class="sxs-lookup"><span data-stu-id="f90e7-221">This example log indicates that hello word 'and' has been emitted 113 times.</span></span> <span data-ttu-id="f90e7-222">Witaj liczba nadal toogo się tak długo, jak działa topologia hello ponieważ hello spout stale emituje hello tego samego zdań.</span><span class="sxs-lookup"><span data-stu-id="f90e7-222">hello count continues toogo up as long as hello topology runs because hello spout continuously emits hello same sentences.</span></span>

<span data-ttu-id="f90e7-223">Brak interwału 5 sekund między emisji słów i liczby.</span><span class="sxs-lookup"><span data-stu-id="f90e7-223">There is a 5-second interval between emission of words and counts.</span></span> <span data-ttu-id="f90e7-224">Witaj **WordCount** składnik został skonfigurowany tooonly Emituj informacje, gdy dociera krotką znacznikową.</span><span class="sxs-lookup"><span data-stu-id="f90e7-224">hello **WordCount** component is configured tooonly emit information when a tick tuple arrives.</span></span> <span data-ttu-id="f90e7-225">Żąda tego znaczników krotek tylko są przeprowadzane co pięć sekund.</span><span class="sxs-lookup"><span data-stu-id="f90e7-225">It requests that tick tuples are only delivered every five seconds.</span></span>

## <a name="convert-hello-topology-tooflux"></a><span data-ttu-id="f90e7-226">Konwertuj hello topologii tooFlux</span><span class="sxs-lookup"><span data-stu-id="f90e7-226">Convert hello topology tooFlux</span></span>

<span data-ttu-id="f90e7-227">Strumień jest nowa struktura dostępne z systemu Storm 0.10.0 lub nowszy, co pozwala tooseparate konfiguracji z wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="f90e7-227">Flux is a new framework available with Storm 0.10.0 and higher, which allows you tooseparate configuration from implementation.</span></span> <span data-ttu-id="f90e7-228">Składniki nadal są zdefiniowane w języku Java, ale topologii hello jest definiowana za pomocą pliku yaml programu.</span><span class="sxs-lookup"><span data-stu-id="f90e7-228">Your components are still defined in Java, but hello topology is defined using a YAML file.</span></span> <span data-ttu-id="f90e7-229">Pakiet definicji topologii domyślnej z projektu lub podczas przesyłania topologii hello przy użyciu pliku autonomicznym.</span><span class="sxs-lookup"><span data-stu-id="f90e7-229">You can package a default topology definition with your project, or use a standalone file when submitting hello topology.</span></span> <span data-ttu-id="f90e7-230">Podczas przesyłania tooStorm topologii hello, można użyć zmiennych środowiskowych lub wartości toopopulate pliki konfiguracji w hello definicji topologii yaml programu.</span><span class="sxs-lookup"><span data-stu-id="f90e7-230">When submitting hello topology tooStorm, you can use environment variables or configuration files toopopulate values in hello YAML topology definition.</span></span>

<span data-ttu-id="f90e7-231">Plik yaml programu Hello definiuje toouse składniki hello hello topologii i hello przepływ danych między nimi.</span><span class="sxs-lookup"><span data-stu-id="f90e7-231">hello YAML file defines hello components toouse for hello topology and hello data flow between them.</span></span> <span data-ttu-id="f90e7-232">Plik yaml programu można dodać jako część pliku jar hello lub skorzystać z zewnętrznego pliku yaml programu.</span><span class="sxs-lookup"><span data-stu-id="f90e7-232">You can include a YAML file as part of hello jar file or you can use an external YAML file.</span></span>

<span data-ttu-id="f90e7-233">Aby uzyskać więcej informacji na strumienia, zobacz [framework strumienia (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="f90e7-233">For more information on Flux, see [Flux framework (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span></span>

> [!WARNING]
> <span data-ttu-id="f90e7-234">Termin tooa [usterek (https://issues.apache.org/jira/browse/STORM-2055)](https://issues.apache.org/jira/browse/STORM-2055) z systemu Storm 1.0.1, może być konieczne tooinstall [środowisko projektowe Storm](https://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) toorun strumień lokalnie topologii.</span><span class="sxs-lookup"><span data-stu-id="f90e7-234">Due tooa [bug (https://issues.apache.org/jira/browse/STORM-2055)](https://issues.apache.org/jira/browse/STORM-2055) with Storm 1.0.1, you may need tooinstall a [Storm development environment](https://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) toorun Flux topologies locally.</span></span>

1. <span data-ttu-id="f90e7-235">Przenieś hello `WordCountTopology.java` pliku poza hello projektu.</span><span class="sxs-lookup"><span data-stu-id="f90e7-235">Move hello `WordCountTopology.java` file out of hello project.</span></span> <span data-ttu-id="f90e7-236">Wcześniej ten plik zdefiniowany hello topologii, ale nie jest wymagane ze strumienia.</span><span class="sxs-lookup"><span data-stu-id="f90e7-236">Previously, this file defined hello topology, but isn't needed with Flux.</span></span>

2. <span data-ttu-id="f90e7-237">W hello `resources` katalogu, Utwórz plik o nazwie `topology.yaml`.</span><span class="sxs-lookup"><span data-stu-id="f90e7-237">In hello `resources` directory, create a file named `topology.yaml`.</span></span> <span data-ttu-id="f90e7-238">Użyj hello następującego tekstu jako hello zawartość tego pliku.</span><span class="sxs-lookup"><span data-stu-id="f90e7-238">Use hello following text as hello contents of this file.</span></span>

        name: "wordcount"       # friendly name for hello topology
        
        config:                 # Topology configuration
        topology.workers: 1     # Hint for hello number of workers toocreate
        
        spouts:                 # Spout definitions
        - id: "sentence-spout"
            className: "com.microsoft.example.RandomSentenceSpout"
            parallelism: 1      # parallelism hint
        
        bolts:                  # Bolt definitions
        - id: "splitter-bolt"
            className: "com.microsoft.example.SplitSentence"
            parallelism: 1
         
        - id: "counter-bolt"
            className: "com.microsoft.example.WordCount"
            constructorArgs:
                - 10
            parallelism: 1
        
        streams:                # Stream definitions
            - name: "Spout --> Splitter" # name isn't used (placeholder for logging, UI, etc.)
            from: "sentence-spout"       # hello stream emitter
            to: "splitter-bolt"          # hello stream consumer
            grouping:                    # Grouping type
                type: SHUFFLE
          
            - name: "Splitter -> Counter"
            from: "splitter-bolt"
            to: "counter-bolt"
            grouping:
            type: FIELDS
                args: ["word"]           # field(s) toogroup on

3. <span data-ttu-id="f90e7-239">Wprowadź następujące zmiany toohello hello `pom.xml` pliku.</span><span class="sxs-lookup"><span data-stu-id="f90e7-239">Make hello following changes toohello `pom.xml` file.</span></span>
   
   * <span data-ttu-id="f90e7-240">Dodaj następujące nowe zależności w hello hello `<dependencies>` sekcji:</span><span class="sxs-lookup"><span data-stu-id="f90e7-240">Add hello following new dependency in hello `<dependencies>` section:</span></span>
     
        ```xml
        <!-- Add a dependency on hello Flux framework -->
        <dependency>
            <groupId>org.apache.storm</groupId>
            <artifactId>flux-core</artifactId>
            <version>${storm.version}</version>
        </dependency>
        ```
   * <span data-ttu-id="f90e7-241">Dodaj następujące wtyczki toohello hello `<plugins>` sekcji.</span><span class="sxs-lookup"><span data-stu-id="f90e7-241">Add hello following plugin toohello `<plugins>` section.</span></span> <span data-ttu-id="f90e7-242">Tej wtyczki obsługuje hello tworzenia pakietu (plik jar) dla projektu hello i zastosowanie niektórych przekształcenia tooFlux określonych podczas tworzenia pakietu hello.</span><span class="sxs-lookup"><span data-stu-id="f90e7-242">This plugin handles hello creation of a package (jar file) for hello project, and applies some transformations specific tooFlux when creating hello package.</span></span>
     
        ```xml
        <!-- build an uber jar -->
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-shade-plugin</artifactId>
            <version>2.3</version>
            <configuration>
                <transformers>
                    <!-- Keep us from getting a "can't overwrite file error" -->
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer" />
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer" />
                    <!-- We're using Flux, so refer tooit as main -->
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
                        <mainClass>org.apache.storm.flux.Flux</mainClass>
                    </transformer>
                </transformers>
                <!-- Keep us from getting a bad signature error -->
                <filters>
                    <filter>
                        <artifact>*:*</artifact>
                        <excludes>
                            <exclude>META-INF/*.SF</exclude>
                            <exclude>META-INF/*.DSA</exclude>
                            <exclude>META-INF/*.RSA</exclude>
                        </excludes>
                    </filter>
                </filters>
            </configuration>
            <executions>
                <execution>
                    <phase>package</phase>
                    <goals>
                        <goal>shade</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
        ```

   * <span data-ttu-id="f90e7-243">W hello **wtyczki exec-maven** `<configuration>` sekcji, zmień wartość hello `<mainClass>` zbyt`org.apache.storm.flux.Flux`.</span><span class="sxs-lookup"><span data-stu-id="f90e7-243">In hello **exec-maven-plugin** `<configuration>` section, change hello value for `<mainClass>` too`org.apache.storm.flux.Flux`.</span></span> <span data-ttu-id="f90e7-244">To ustawienie umożliwia uruchomionych topologii hello lokalnie w rozwoju toohandle strumienia.</span><span class="sxs-lookup"><span data-stu-id="f90e7-244">This setting allows Flux toohandle running hello topology locally in development.</span></span>

   * <span data-ttu-id="f90e7-245">W hello `<resources>` Dodaj powitania po toohello `<includes>`.</span><span class="sxs-lookup"><span data-stu-id="f90e7-245">In hello `<resources>` section, add hello following toohello `<includes>`.</span></span> <span data-ttu-id="f90e7-246">Plik XML zawiera hello yaml programu pliku, który definiuje topologii hello jako część hello projektu.</span><span class="sxs-lookup"><span data-stu-id="f90e7-246">This XML includes hello YAML file that defines hello topology as part of hello project.</span></span>

        ```xml
        <include>topology.yaml</include>
        ```

## <a name="test-hello-flux-topology-locally"></a><span data-ttu-id="f90e7-247">Topologia strumień hello testu lokalnie</span><span class="sxs-lookup"><span data-stu-id="f90e7-247">Test hello flux topology locally</span></span>

1. <span data-ttu-id="f90e7-248">Użyj następującego toocompile hello i wykonaj hello strumień topologii za pomocą programu Maven:</span><span class="sxs-lookup"><span data-stu-id="f90e7-248">Use hello following toocompile and execute hello Flux topology using Maven:</span></span>

    ```bash
    mvn compile exec:java -Dexec.args="--local -R /topology.yaml"
    ```

    <span data-ttu-id="f90e7-249">Jeśli używasz programu PowerShell, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="f90e7-249">If you are using PowerShell, use hello following command:</span></span>

    ```bash
    mvn compile exec:java "-Dexec.args=--local -R /topology.yaml"
    ```

    > [!WARNING]
    > <span data-ttu-id="f90e7-250">Jeśli topologii korzysta z usługi bits Storm 1.0.1, to polecenie nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="f90e7-250">If your topology uses Storm 1.0.1 bits, this command fails.</span></span> <span data-ttu-id="f90e7-251">Ten błąd jest spowodowany przez [https://issues.apache.org/jira/browse/STORM-2055](https://issues.apache.org/jira/browse/STORM-2055).</span><span class="sxs-lookup"><span data-stu-id="f90e7-251">This failure is caused by [https://issues.apache.org/jira/browse/STORM-2055](https://issues.apache.org/jira/browse/STORM-2055).</span></span> <span data-ttu-id="f90e7-252">Zamiast tego [zainstalować Storm w środowisku projektowania](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html) i hello Użyj następujących informacji.</span><span class="sxs-lookup"><span data-stu-id="f90e7-252">Instead, [install Storm in your development environment](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html) and use hello following information.</span></span>

    <span data-ttu-id="f90e7-253">Jeśli masz [zainstalowane Storm w środowisku projektowania](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html), można użyć hello zamiast tego następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="f90e7-253">If you have [installed Storm in your development environment](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html), you can use hello following commands instead:</span></span>

    ```bash
    mvn compile package
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /topology.yaml
    ```

    <span data-ttu-id="f90e7-254">Witaj `--local` parametr działa topologia hello w trybie lokalnym na środowiska deweloperskiego.</span><span class="sxs-lookup"><span data-stu-id="f90e7-254">hello `--local` parameter runs hello topology in local mode on your development environment.</span></span> <span data-ttu-id="f90e7-255">Witaj `-R /topology.yaml` parametr używa hello `topology.yaml` pliku zasobu z hello jar pliku toodefine hello topologii.</span><span class="sxs-lookup"><span data-stu-id="f90e7-255">hello `-R /topology.yaml` parameter uses hello `topology.yaml` file resource from hello jar file toodefine hello topology.</span></span>

    <span data-ttu-id="f90e7-256">Podczas wykonywania, topologii hello Wyświetla informacje o uruchamianiu.</span><span class="sxs-lookup"><span data-stu-id="f90e7-256">As it runs, hello topology displays startup information.</span></span> <span data-ttu-id="f90e7-257">przykład danych wyjściowych hello znajduje się w Hello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="f90e7-257">hello following text is an example of hello output:</span></span>

        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
        17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs

    <span data-ttu-id="f90e7-258">Brak 10-sekundowe opóźnienie między partie zarejestrowane informacje.</span><span class="sxs-lookup"><span data-stu-id="f90e7-258">There is a 10-second delay between batches of logged information.</span></span>

2. <span data-ttu-id="f90e7-259">Utwórz kopię hello `topology.yaml` plik z projektu hello.</span><span class="sxs-lookup"><span data-stu-id="f90e7-259">Make a copy of hello `topology.yaml` file from hello project.</span></span> <span data-ttu-id="f90e7-260">Nazwa hello nowy plik `newtopology.yaml`.</span><span class="sxs-lookup"><span data-stu-id="f90e7-260">Name hello new file `newtopology.yaml`.</span></span> <span data-ttu-id="f90e7-261">W hello `newtopology.yaml` pliku, znajdź następujący hello sekcji i zmienić wartość hello `10` zbyt`5`.</span><span class="sxs-lookup"><span data-stu-id="f90e7-261">In hello `newtopology.yaml` file, find hello following section and change hello value of `10` too`5`.</span></span> <span data-ttu-id="f90e7-262">Zlicza ta modyfikacja zmiany hello odstęp między emitowania partii programu word z too5 10 sekund.</span><span class="sxs-lookup"><span data-stu-id="f90e7-262">This modification changes hello interval between emitting batches of word counts from 10 seconds too5.</span></span>

    ```yaml
    - id: "counter-bolt"
    className: "com.microsoft.example.WordCount"
    constructorArgs:
    - 5
    parallelism: 1
    ```yaml

3. toorun hello topology, use hello following command:

    ```bash
    mvn exec:java -Dexec.args="--local /path/to/newtopology.yaml"
    ```

    <span data-ttu-id="f90e7-263">Lub, jeśli masz Storm środowiska programowania:</span><span class="sxs-lookup"><span data-stu-id="f90e7-263">Or, if you have Storm on your development environment:</span></span>

    ```bash
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local /path/to/newtopology.yaml
    ```

    <span data-ttu-id="f90e7-264">Zmień hello `/path/to/newtopology.yaml` utworzony w poprzednim kroku hello toohello ścieżki toohello newtopology.yaml pliku.</span><span class="sxs-lookup"><span data-stu-id="f90e7-264">Change hello `/path/to/newtopology.yaml` toohello path toohello newtopology.yaml file you created in hello previous step.</span></span> <span data-ttu-id="f90e7-265">To polecenie używa hello newtopology.yaml jako hello topologii definicji.</span><span class="sxs-lookup"><span data-stu-id="f90e7-265">This command uses hello newtopology.yaml as hello topology definition.</span></span> <span data-ttu-id="f90e7-266">Ponieważ firma Microsoft nie obejmują hello `compile` parametru Maven używa wersji hello projektu hello utworzony w poprzednich krokach.</span><span class="sxs-lookup"><span data-stu-id="f90e7-266">Since we didn't include hello `compile` parameter, Maven uses hello version of hello project built in previous steps.</span></span>

    <span data-ttu-id="f90e7-267">Raz hello rozpoczyna topologii, można zauważyć, że hello czas między emitowany partie została zmieniona wartość hello tooreflect newtopology.yaml.</span><span class="sxs-lookup"><span data-stu-id="f90e7-267">Once hello topology starts, you should notice that hello time between emitted batches has changed tooreflect hello value in newtopology.yaml.</span></span> <span data-ttu-id="f90e7-268">Aby było widać, konfigurację można zmienić za pomocą pliku yaml programu bez konieczności toorecompile hello topologii.</span><span class="sxs-lookup"><span data-stu-id="f90e7-268">So you can see that you can change your configuration through a YAML file without having toorecompile hello topology.</span></span>

<span data-ttu-id="f90e7-269">Aby uzyskać więcej informacji na temat tych i innych funkcji hello strumień framework, zobacz [strumienia (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="f90e7-269">For more information on these and other features of hello Flux framework, see [Flux (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span></span>

## <a name="trident"></a><span data-ttu-id="f90e7-270">Trident</span><span class="sxs-lookup"><span data-stu-id="f90e7-270">Trident</span></span>

<span data-ttu-id="f90e7-271">Trident to Abstrakcja wysokiego poziomu zapewnianej przez Storm.</span><span class="sxs-lookup"><span data-stu-id="f90e7-271">Trident is a high-level abstraction that is provided by Storm.</span></span> <span data-ttu-id="f90e7-272">Obsługuje ona stanowe przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="f90e7-272">It supports stateful processing.</span></span> <span data-ttu-id="f90e7-273">główną zaletą Trident Hello jest, że go gwarantuje, że każdy komunikat, który przechodzi topologii hello jest przetwarzany tylko raz.</span><span class="sxs-lookup"><span data-stu-id="f90e7-273">hello primary advantage of Trident is that it can guarantee that every message that enters hello topology is processed only once.</span></span> <span data-ttu-id="f90e7-274">Bez użycia języka Trident, topologii można tylko gwarantuje, że komunikaty są przetwarzane co najmniej raz.</span><span class="sxs-lookup"><span data-stu-id="f90e7-274">Without using Trident, your topology can only guarantee that messages are processed at least once.</span></span> <span data-ttu-id="f90e7-275">Istnieją także inne różnice, takich jak wbudowanych składników, które mogą być używane zamiast tworzenia elementów bolt.</span><span class="sxs-lookup"><span data-stu-id="f90e7-275">There are also other differences, such as built-in components that can be used instead of creating bolts.</span></span> <span data-ttu-id="f90e7-276">W rzeczywistości elementów bolt są zastępowane przez składniki mniej ogólny, takie jak filtry, rzutowania i funkcje.</span><span class="sxs-lookup"><span data-stu-id="f90e7-276">In fact, bolts are replaced by less-generic components, such as filters, projections, and functions.</span></span>

<span data-ttu-id="f90e7-277">Trident aplikacje mogą być tworzone przy użyciu projekty Maven.</span><span class="sxs-lookup"><span data-stu-id="f90e7-277">Trident applications can be created by using Maven projects.</span></span> <span data-ttu-id="f90e7-278">Użyj hello tego samego basic kroki przedstawione w tym artykule — tylko kod hello różni się.</span><span class="sxs-lookup"><span data-stu-id="f90e7-278">You use hello same basic steps as presented earlier in this article—only hello code is different.</span></span> <span data-ttu-id="f90e7-279">Trident również nie (obecnie) można używać z hello framework strumienia.</span><span class="sxs-lookup"><span data-stu-id="f90e7-279">Trident also cannot (currently) be used with hello Flux framework.</span></span>

<span data-ttu-id="f90e7-280">Aby uzyskać więcej informacji na temat języka Trident, zobacz hello [omówienie API Trident](http://storm.apache.org/documentation/Trident-API-Overview.html).</span><span class="sxs-lookup"><span data-stu-id="f90e7-280">For more information about Trident, see hello [Trident API Overview](http://storm.apache.org/documentation/Trident-API-Overview.html).</span></span>

<span data-ttu-id="f90e7-281">Na przykład aplikację języka Trident, zobacz [trendów tematy z systemu Apache Storm w usłudze HDInsight w usłudze Twitter](hdinsight-storm-twitter-trending.md).</span><span class="sxs-lookup"><span data-stu-id="f90e7-281">For an example of a Trident application, see [Twitter trending topics with Apache Storm on HDInsight](hdinsight-storm-twitter-trending.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f90e7-282">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f90e7-282">Next Steps</span></span>

<span data-ttu-id="f90e7-283">Wiesz już, jak toocreate topologii Storm za pomocą języka Java.</span><span class="sxs-lookup"><span data-stu-id="f90e7-283">You have learned how toocreate a Storm topology by using Java.</span></span> <span data-ttu-id="f90e7-284">Teraz Dowiedz się, jak:</span><span class="sxs-lookup"><span data-stu-id="f90e7-284">Now learn how to:</span></span>

* [<span data-ttu-id="f90e7-285">Wdrażanie i zarządzanie nimi topologii Apache Storm w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="f90e7-285">Deploy and manage Apache Storm topologies on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology.md)

* [<span data-ttu-id="f90e7-286">Tworzenie topologii C# dla Apache Storm w usłudze HDInsight przy użyciu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f90e7-286">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

<span data-ttu-id="f90e7-287">Można znaleźć więcej przykład topologii Storm po przejściu na stronę [przykładowe topologie dla systemu Storm w usłudze HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="f90e7-287">You can find more example Storm topologies by visiting [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>

