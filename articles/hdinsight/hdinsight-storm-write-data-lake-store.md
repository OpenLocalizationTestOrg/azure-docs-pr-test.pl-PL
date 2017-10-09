---
title: aaaApache Storm zapisu tooStorage/Data Lake Store - Azure HDInsight | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toouse hello Apache Storm toowrite toohello zgodnego systemem plików HDFS magazynu dla usługi HDInsight. Azure magazynu lub usługi Azure Data Lake Store magazynowanie hello HDFS comptabile HDInsight. W tym dokumencie i skojarzone przykład Witaj, pokazują, jak hello HdfsBolt składnika mogą być używane toowrite toohello domyślny magazyn Storm w klastrze usługi HDInsight."
services: hdinsight
documentationcenter: na
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 1df98653-a6c8-4662-a8c6-5d288fc4f3a6
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/19/2017
ms.author: larryfr
ms.openlocfilehash: d76159a9ecd1be18e519511cfdb3bcfd18ae4d33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="write-toohdfs-from-apache-storm-on-hdinsight"></a><span data-ttu-id="85fd5-105">Zapis tooHDFS z systemu Apache Storm w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="85fd5-105">Write tooHDFS from Apache Storm on HDInsight</span></span>

<span data-ttu-id="85fd5-106">Dowiedz się, jak toouse Storm toowrite danych toohello zgodnego systemem plików HDFS magazynu używane przez Apache Storm w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="85fd5-106">Learn how toouse Storm toowrite data toohello HDFS-compatible storage used by Apache Storm on HDInsight.</span></span> <span data-ttu-id="85fd5-107">HDInsight można użyć zarówno usługi Azure Storage i Azure Data Lake przechowywane jako magazyn comptabile systemu plików HDFS.</span><span class="sxs-lookup"><span data-stu-id="85fd5-107">HDInsight can use both Azure Storage and Azure Data Lake store as HDFS-comptabile storage.</span></span> <span data-ttu-id="85fd5-108">STORM udostępnia [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) składnik, który zapisuje tooHDFS danych.</span><span class="sxs-lookup"><span data-stu-id="85fd5-108">Storm provides an [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) component that writes data tooHDFS.</span></span> <span data-ttu-id="85fd5-109">Ten dokument zawiera informacje o pisaniu z hello HdfsBolt tooeither typu magazynu.</span><span class="sxs-lookup"><span data-stu-id="85fd5-109">This document provides information on writing tooeither type of storage from hello HdfsBolt.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="85fd5-110">przykład Witaj topologii używane w tym dokumencie opiera się na składnikach, które są dołączone do systemu Storm w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="85fd5-110">hello example topology used in this document relies on components that are included with Storm on HDInsight.</span></span> <span data-ttu-id="85fd5-111">Może wymagać modyfikacji toowork z usługi Azure Data Lake Store w przypadku użycia z innych klastrów platformy Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="85fd5-111">It may require modification toowork with Azure Data Lake Store when used with other Apache Storm clusters.</span></span>

## <a name="get-hello-code"></a><span data-ttu-id="85fd5-112">Pobierz kod hello</span><span class="sxs-lookup"><span data-stu-id="85fd5-112">Get hello code</span></span>

<span data-ttu-id="85fd5-113">Projekt Hello zawierający Ta topologia jest dostępny do pobrania z [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="85fd5-113">hello project containing this topology is available as a download from [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store).</span></span>

<span data-ttu-id="85fd5-114">toocompile tego projektu należy hello następującej konfiguracji dla swojego środowiska programowania:</span><span class="sxs-lookup"><span data-stu-id="85fd5-114">toocompile this project, you need hello following configuration for your development environment:</span></span>

* <span data-ttu-id="85fd5-115">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="85fd5-115">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span> <span data-ttu-id="85fd5-116">HDInsight w wersji 3.5 lub nowszej wymagają Java 8.</span><span class="sxs-lookup"><span data-stu-id="85fd5-116">HDInsight 3.5 or higher require Java 8.</span></span>

* [<span data-ttu-id="85fd5-117">Maven 3.x</span><span class="sxs-lookup"><span data-stu-id="85fd5-117">Maven 3.x</span></span>](https://maven.apache.org/download.cgi)

<span data-ttu-id="85fd5-118">Witaj następujące zmienne środowiskowe mogą zostać ustawione podczas instalowania Java i hello JDK na deweloperskiej stacji roboczej.</span><span class="sxs-lookup"><span data-stu-id="85fd5-118">hello following environment variables may be set when you install Java and hello JDK on your development workstation.</span></span> <span data-ttu-id="85fd5-119">Jednak należy sprawdzić, czy istnieją i że zawierają one hello poprawne wartości dla systemu.</span><span class="sxs-lookup"><span data-stu-id="85fd5-119">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="85fd5-120">`JAVA_HOME`— powinna wskazywać katalog toohello hello JDK zainstalowanym.</span><span class="sxs-lookup"><span data-stu-id="85fd5-120">`JAVA_HOME` - should point toohello directory where hello JDK is installed.</span></span>
* <span data-ttu-id="85fd5-121">`PATH`— powinna zawierać hello następującej ścieżki:</span><span class="sxs-lookup"><span data-stu-id="85fd5-121">`PATH` - should contain hello following paths:</span></span>
  
    * <span data-ttu-id="85fd5-122">`JAVA_HOME`(lub równoważne ścieżki hello).</span><span class="sxs-lookup"><span data-stu-id="85fd5-122">`JAVA_HOME` (or hello equivalent path).</span></span>
    * <span data-ttu-id="85fd5-123">`JAVA_HOME\bin`(lub równoważne ścieżki hello).</span><span class="sxs-lookup"><span data-stu-id="85fd5-123">`JAVA_HOME\bin` (or hello equivalent path).</span></span>
    * <span data-ttu-id="85fd5-124">Hello katalog, w którym zainstalowano Maven.</span><span class="sxs-lookup"><span data-stu-id="85fd5-124">hello directory where Maven is installed.</span></span>

## <a name="how-toouse-hello-hdfsbolt-with-hdinsight"></a><span data-ttu-id="85fd5-125">Jak toouse hello HdfsBolt z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="85fd5-125">How toouse hello HdfsBolt with HDInsight</span></span>

> [!IMPORTANT]
> <span data-ttu-id="85fd5-126">Przed użyciem hello HdfsBolt z systemu Storm w usłudze HDInsight, musisz najpierw użyć pliki jar toocopy wymagana akcja skryptu do hello `extpath` systemu STORM.</span><span class="sxs-lookup"><span data-stu-id="85fd5-126">Before using hello HdfsBolt with Storm on HDInsight, you must first use a script action toocopy required jar files into hello `extpath` for Storm.</span></span> <span data-ttu-id="85fd5-127">Aby uzyskać więcej informacji, zobacz hello [Konfigurowanie klastra hello](#configure) sekcji.</span><span class="sxs-lookup"><span data-stu-id="85fd5-127">For more information, see hello [Configure hello cluster](#configure) section.</span></span>

<span data-ttu-id="85fd5-128">Witaj HdfsBolt wykorzystuje schemat pliku hello jak zapewnić toounderstand toowrite tooHDFS.</span><span class="sxs-lookup"><span data-stu-id="85fd5-128">hello HdfsBolt uses hello file scheme that you provide toounderstand how toowrite tooHDFS.</span></span> <span data-ttu-id="85fd5-129">Z usługą HDInsight użyj jednej z hello następujące programy:</span><span class="sxs-lookup"><span data-stu-id="85fd5-129">With HDInsight, use one of hello following schemes:</span></span>

* <span data-ttu-id="85fd5-130">`wasb://`: Używany przy użyciu konta usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="85fd5-130">`wasb://`: Used with an Azure Storage account.</span></span>
* <span data-ttu-id="85fd5-131">`adl://`: Używane z usługi Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="85fd5-131">`adl://`: Used with Azure Data Lake Store.</span></span>

<span data-ttu-id="85fd5-132">Witaj poniższej tabeli przedstawiono przykłady użycia hello pliku schematu dla różnych scenariuszy:</span><span class="sxs-lookup"><span data-stu-id="85fd5-132">hello following table provides examples of using hello file scheme for different scenarios:</span></span>

| <span data-ttu-id="85fd5-133">Schemat</span><span class="sxs-lookup"><span data-stu-id="85fd5-133">Scheme</span></span> | <span data-ttu-id="85fd5-134">Uwagi</span><span class="sxs-lookup"><span data-stu-id="85fd5-134">Notes</span></span> |
| ----- | ----- |
| `wasb:///` | <span data-ttu-id="85fd5-135">Witaj domyślne konto magazynu jest kontenera obiektów blob na koncie magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="85fd5-135">hello default storage account is a blob container in an Azure Storage account</span></span> |
| `adl:///` | <span data-ttu-id="85fd5-136">Witaj domyślne konto magazynu jest katalogiem w usłudze Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="85fd5-136">hello default storage account is a directory in Azure Data Lake Store.</span></span> <span data-ttu-id="85fd5-137">Podczas tworzenia klastra należy określić katalog hello w usługi Data Lake Store jest głównym hello hello klastra systemu plików HDFS.</span><span class="sxs-lookup"><span data-stu-id="85fd5-137">During cluster creation, you specify hello directory in Data Lake Store that is hello root of hello cluster's HDFS.</span></span> <span data-ttu-id="85fd5-138">Na przykład Witaj `/clusters/myclustername/` katalogu.</span><span class="sxs-lookup"><span data-stu-id="85fd5-138">For example, hello `/clusters/myclustername/` directory.</span></span> |
| `wasb://CONTAINER@ACCOUNT.blob.core.windows.net/` | <span data-ttu-id="85fd5-139">Konto magazynu platformy Azure (dodatkowe) innych niż domyślne skojarzone z klastrem hello.</span><span class="sxs-lookup"><span data-stu-id="85fd5-139">A non-default (additional) Azure storage account associated with hello cluster.</span></span> |
| `adl://STORENAME/` | <span data-ttu-id="85fd5-140">katalog główny Hello hello używane przez klaster hello usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="85fd5-140">hello root of hello Data Lake Store used by hello cluster.</span></span> <span data-ttu-id="85fd5-141">Ten program umożliwia tooaccess danych, który znajduje się poza katalogiem hello, zawierający system plików klastra hello.</span><span class="sxs-lookup"><span data-stu-id="85fd5-141">This scheme allows you tooaccess data that is located outside hello directory that contains hello cluster file system.</span></span> |

<span data-ttu-id="85fd5-142">Aby uzyskać więcej informacji, zobacz hello [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) odwołania w serwisie Apache.org.</span><span class="sxs-lookup"><span data-stu-id="85fd5-142">For more information, see hello [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) reference at Apache.org.</span></span>

### <a name="example-configuration"></a><span data-ttu-id="85fd5-143">Przykładowa konfiguracja</span><span class="sxs-lookup"><span data-stu-id="85fd5-143">Example configuration</span></span>

<span data-ttu-id="85fd5-144">Witaj następujące yaml programu znajduje się fragment hello `resources/writetohdfs.yaml` dołączony przykład Witaj.</span><span class="sxs-lookup"><span data-stu-id="85fd5-144">hello following YAML is an excerpt from hello `resources/writetohdfs.yaml` file included in hello example.</span></span> <span data-ttu-id="85fd5-145">Ten plik definiuje topologii Storm hello przy użyciu hello [strumień](https://storm.apache.org/releases/1.1.0/flux.html) framework Apache STORM.</span><span class="sxs-lookup"><span data-stu-id="85fd5-145">This file defines hello Storm topology using hello [Flux](https://storm.apache.org/releases/1.1.0/flux.html) framework for Apache Storm.</span></span>

```yaml
components:
  - id: "syncPolicy"
    className: "org.apache.storm.hdfs.bolt.sync.CountSyncPolicy"
    constructorArgs:
      - 1000

  - id: "rotationPolicy"
    className: "org.apache.storm.hdfs.bolt.rotation.NoRotationPolicy"

  - id: "fileNameFormat"
    className: "org.apache.storm.hdfs.bolt.format.DefaultFileNameFormat"
    configMethods:
      - name: "withPath"
        args: ["${hdfs.write.dir}"]
      - name: "withExtension"
        args: [".txt"]

  - id: "recordFormat"
    className: "org.apache.storm.hdfs.bolt.format.DelimitedRecordFormat"
    configMethods:
      - name: "withFieldDelimiter"
        args: ["|"]

# spout definitions
spouts:
  - id: "tick-spout"
    className: "com.microsoft.example.TickSpout"
    parallelism: 1


# bolt definitions
bolts:
  - id: "hdfs-bolt"
    className: "org.apache.storm.hdfs.bolt.HdfsBolt"
    configMethods:
      - name: "withConfigKey"
        args: ["hdfs.config"]
      - name: "withFsUrl"
        args: ["${hdfs.url}"]
      - name: "withFileNameFormat"
        args: [ref: "fileNameFormat"]
      - name: "withRecordFormat"
        args: [ref: "recordFormat"]
      - name: "withRotationPolicy"
        args: [ref: "rotationPolicy"]
      - name: "withSyncPolicy"
        args: [ref: "syncPolicy"]
```

<span data-ttu-id="85fd5-146">Ta yaml programu definiuje hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="85fd5-146">This YAML defines hello following items:</span></span>

* <span data-ttu-id="85fd5-147">`syncPolicy`: Określa, kiedy pliki są zsynchronizowane opróżnionych toohello systemu plików.</span><span class="sxs-lookup"><span data-stu-id="85fd5-147">`syncPolicy`: Defines when files are synched/flushed toohello file system.</span></span> <span data-ttu-id="85fd5-148">W tym przykładzie każdy krotek 1000.</span><span class="sxs-lookup"><span data-stu-id="85fd5-148">In this example, every 1000 tuples.</span></span>
* <span data-ttu-id="85fd5-149">`fileNameFormat`: Definiuje hello ścieżkę i nazwę wzorca toouse podczas zapisywania plików.</span><span class="sxs-lookup"><span data-stu-id="85fd5-149">`fileNameFormat`: Defines hello path and file name pattern toouse when writing files.</span></span> <span data-ttu-id="85fd5-150">W tym przykładzie zostanie podana ścieżka hello w środowisku uruchomieniowym przy użyciu filtru i rozszerzenie pliku hello jest `.txt`.</span><span class="sxs-lookup"><span data-stu-id="85fd5-150">In this example, hello path is provided at runtime using a filter, and hello file extension is `.txt`.</span></span>
* <span data-ttu-id="85fd5-151">`recordFormat`: Definiuje hello wewnętrzny format plików hello zapisywane.</span><span class="sxs-lookup"><span data-stu-id="85fd5-151">`recordFormat`: Defines hello internal format of hello files written.</span></span> <span data-ttu-id="85fd5-152">W tym przykładzie pola są rozdzielone hello `|` znaków.</span><span class="sxs-lookup"><span data-stu-id="85fd5-152">In this example, fields are delimited by hello `|` character.</span></span>
* <span data-ttu-id="85fd5-153">`rotationPolicy`: Określa, kiedy toorotate plików.</span><span class="sxs-lookup"><span data-stu-id="85fd5-153">`rotationPolicy`: Defines when toorotate files.</span></span> <span data-ttu-id="85fd5-154">W tym przykładzie jest wykonywane bez obrotu.</span><span class="sxs-lookup"><span data-stu-id="85fd5-154">In this example, no rotation is performed.</span></span>
* <span data-ttu-id="85fd5-155">`hdfs-bolt`: Używa hello poprzednie składniki jako parametry konfiguracji hello `HdfsBolt` klasy.</span><span class="sxs-lookup"><span data-stu-id="85fd5-155">`hdfs-bolt`: Uses hello previous components as configuration parameters for hello `HdfsBolt` class.</span></span>

<span data-ttu-id="85fd5-156">Aby uzyskać więcej informacji na powitania strumień framework, zobacz [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="85fd5-156">For more information on hello Flux framework, see [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span></span>

## <a name="configure-hello-cluster"></a><span data-ttu-id="85fd5-157">Konfigurowanie klastra hello</span><span class="sxs-lookup"><span data-stu-id="85fd5-157">Configure hello cluster</span></span>

<span data-ttu-id="85fd5-158">Domyślnie Storm w usłudze HDInsight nie zawiera składników hello HdfsBolt używa toocommunicate z magazynu Azure lub usługi Data Lake Store w Storm w ścieżce.</span><span class="sxs-lookup"><span data-stu-id="85fd5-158">By default, Storm on HDInsight does not include hello components that HdfsBolt uses toocommunicate with Azure Storage or Data Lake Store in Storm's classpath.</span></span> <span data-ttu-id="85fd5-159">Użyj następujących hello skryptu akcji tooadd toohello te składniki `extlib` katalogu systemu STORM w klastrze:</span><span class="sxs-lookup"><span data-stu-id="85fd5-159">Use hello following script action tooadd these components toohello `extlib` directory for Storm on your cluster:</span></span>

<span data-ttu-id="85fd5-160">| Identyfikator URI skryptu | Węzły tooapply go do | Parametry || `https://000aarperiscus.blob.core.windows.net/certs/stormextlib.sh` | Nimbus, przełożonego | None |</span><span class="sxs-lookup"><span data-stu-id="85fd5-160">| Script URI | Nodes tooapply it to| Parameters | | `https://000aarperiscus.blob.core.windows.net/certs/stormextlib.sh` | Nimbus, Supervisor | None |</span></span>

<span data-ttu-id="85fd5-161">Uzyskać informacji na temat używania tego skryptu z klastrem, zobacz hello [HDInsight dostosować klastry za pomocą akcji skryptu](./hdinsight-hadoop-customize-cluster-linux.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="85fd5-161">For information on using this script with your cluster, see hello [Customize HDInsight clusters using script actions](./hdinsight-hadoop-customize-cluster-linux.md) document.</span></span>

## <a name="build-and-package-hello-topology"></a><span data-ttu-id="85fd5-162">Topologia hello kompilacji i pakietu</span><span class="sxs-lookup"><span data-stu-id="85fd5-162">Build and package hello topology</span></span>

1. <span data-ttu-id="85fd5-163">Pobierz hello przykładowy projekt z [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) tooyour Środowisko deweloperskie.</span><span class="sxs-lookup"><span data-stu-id="85fd5-163">Download hello example project from [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) tooyour development environment.</span></span>

2. <span data-ttu-id="85fd5-164">W wierszu polecenia terminal lub sesję powłoki, zmień katalogi toohello głównym hello pobrane projektu.</span><span class="sxs-lookup"><span data-stu-id="85fd5-164">From a command prompt, terminal, or shell session, change directories toohello root of hello downloaded project.</span></span> <span data-ttu-id="85fd5-165">toobuild i pakietu hello topologii, należy użyć następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="85fd5-165">toobuild and package hello topology, use hello following command:</span></span>
   
        mvn compile package
   
    <span data-ttu-id="85fd5-166">Po zakończeniu kompilacji hello i opakowanie jest nowy katalog o nazwie `target`, który zawiera plik o nazwie `StormToHdfs-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="85fd5-166">Once hello build and packaging completes, there is a new directory named `target`, that contains a file named `StormToHdfs-1.0-SNAPSHOT.jar`.</span></span> <span data-ttu-id="85fd5-167">Ten plik zawiera topologii hello skompilowany.</span><span class="sxs-lookup"><span data-stu-id="85fd5-167">This file contains hello compiled topology.</span></span>

## <a name="deploy-and-run-hello-topology"></a><span data-ttu-id="85fd5-168">Wdrażanie i uruchamianie hello topologii</span><span class="sxs-lookup"><span data-stu-id="85fd5-168">Deploy and run hello topology</span></span>

1. <span data-ttu-id="85fd5-169">Użyj powitania po klastra usługi HDInsight toohello polecenia toocopy hello topologii.</span><span class="sxs-lookup"><span data-stu-id="85fd5-169">Use hello following command toocopy hello topology toohello HDInsight cluster.</span></span> <span data-ttu-id="85fd5-170">Zastąp **użytkownika** z nazwą użytkownika SSH hello są używane podczas tworzenia klastra hello.</span><span class="sxs-lookup"><span data-stu-id="85fd5-170">Replace **USER** with hello SSH user name you used when creating hello cluster.</span></span> <span data-ttu-id="85fd5-171">Zastąp **CLUSTERNAME** o nazwie hello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="85fd5-171">Replace **CLUSTERNAME** with hello name of hello cluster.</span></span>
   
        scp target\StormToHdfs-1.0-SNAPSHOT.jar USER@CLUSTERNAME-ssh.azurehdinsight.net:StormToHdfs1.0-SNAPSHOT.jar
   
    <span data-ttu-id="85fd5-172">Po wyświetleniu monitu wprowadź hasło hello używany podczas tworzenia użytkownika SSH hello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="85fd5-172">When prompted, enter hello password used when creating hello SSH user for hello cluster.</span></span> <span data-ttu-id="85fd5-173">Jeśli używasz klucza publicznego zamiast hasła, może być konieczne toouse hello `-i` parametru toospecify hello ścieżki toohello pasujących do klucza prywatnego.</span><span class="sxs-lookup"><span data-stu-id="85fd5-173">If you used a public key instead of a password, you may need toouse hello `-i` parameter toospecify hello path toohello matching private key.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="85fd5-174">Aby uzyskać więcej informacji na temat używania `scp` z usługą HDInsight, zobacz [używanie SSH z usługą HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="85fd5-174">For more information on using `scp` with HDInsight, see [Use SSH with HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="85fd5-175">Po ukończeniu przekazywania hello Użyj powitania po klastra usługi HDInsight toohello tooconnect przy użyciu protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="85fd5-175">Once hello upload completes, use hello following tooconnect toohello HDInsight cluster using SSH.</span></span> <span data-ttu-id="85fd5-176">Zastąp **użytkownika** z nazwą użytkownika SSH hello są używane podczas tworzenia klastra hello.</span><span class="sxs-lookup"><span data-stu-id="85fd5-176">Replace **USER** with hello SSH user name you used when creating hello cluster.</span></span> <span data-ttu-id="85fd5-177">Zastąp **CLUSTERNAME** o nazwie hello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="85fd5-177">Replace **CLUSTERNAME** with hello name of hello cluster.</span></span>
   
        ssh USER@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="85fd5-178">Po wyświetleniu monitu wprowadź hasło hello używany podczas tworzenia użytkownika SSH hello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="85fd5-178">When prompted, enter hello password used when creating hello SSH user for hello cluster.</span></span> <span data-ttu-id="85fd5-179">Jeśli używasz klucza publicznego zamiast hasła, może być konieczne toouse hello `-i` parametru toospecify hello ścieżki toohello pasujących do klucza prywatnego.</span><span class="sxs-lookup"><span data-stu-id="85fd5-179">If you used a public key instead of a password, you may need toouse hello `-i` parameter toospecify hello path toohello matching private key.</span></span>
   
   <span data-ttu-id="85fd5-180">Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="85fd5-180">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="85fd5-181">Po nawiązaniu połączenia użyj hello następujące polecenie toocreate plik o nazwie `dev.properties`:</span><span class="sxs-lookup"><span data-stu-id="85fd5-181">Once connected, use hello following command toocreate a file named `dev.properties`:</span></span>

        nano dev.properties

4. <span data-ttu-id="85fd5-182">Witaj Użyj następującego tekstu jako zawartość hello hello `dev.properties` pliku:</span><span class="sxs-lookup"><span data-stu-id="85fd5-182">Use hello following text as hello contents of hello `dev.properties` file:</span></span>

        hdfs.write.dir: /stormdata/
        hdfs.url: wasb:///

    > [!IMPORTANT]
    > <span data-ttu-id="85fd5-183">W tym przykładzie przyjęto założenie, że klaster używa konta usługi Azure Storage jako hello domyślny magazyn.</span><span class="sxs-lookup"><span data-stu-id="85fd5-183">This example assumes that your cluster uses an Azure Storage account as hello default storage.</span></span> <span data-ttu-id="85fd5-184">Jeśli klaster używa usługi Azure Data Lake Store, użyj `hdfs.url: adl:///` zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="85fd5-184">If your cluster uses Azure Data Lake Store, use `hdfs.url: adl:///` instead.</span></span>
    
    <span data-ttu-id="85fd5-185">toosave hello pliku, użyj __Ctrl + X__, następnie __Y__, a na końcu __Enter__.</span><span class="sxs-lookup"><span data-stu-id="85fd5-185">toosave hello file, use __Ctrl + X__, then __Y__, and finally __Enter__.</span></span> <span data-ttu-id="85fd5-186">Witaj wartości w tym pliku Ustaw adres URL Sklepu usługi Data Lake hello i hello nazwę katalogu, którego dane są zapisywane.</span><span class="sxs-lookup"><span data-stu-id="85fd5-186">hello values in this file set hello Data Lake store URL and hello directory name that data is written to.</span></span>

3. <span data-ttu-id="85fd5-187">Witaj Użyj następującego polecenia toostart hello topologii:</span><span class="sxs-lookup"><span data-stu-id="85fd5-187">Use hello following command toostart hello topology:</span></span>
   
        storm jar StormToHdfs-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writetohdfs.yaml --filter dev.properties

    <span data-ttu-id="85fd5-188">To polecenie uruchamia topologii hello przy użyciu framework strumień hello przesyłając węzeł Nimbus toohello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="85fd5-188">This command starts hello topology using hello Flux framework by submitting it toohello Nimbus node of hello cluster.</span></span> <span data-ttu-id="85fd5-189">Topologia Hello jest definiowana za pomocą hello `writetohdfs.yaml` pliku hello jar.</span><span class="sxs-lookup"><span data-stu-id="85fd5-189">hello topology is defined by hello `writetohdfs.yaml` file included in hello jar.</span></span> <span data-ttu-id="85fd5-190">Witaj `dev.properties` plik jest przekazywany jako filtru, a wartości hello zawartych w pliku hello są odczytywane przez hello topologii.</span><span class="sxs-lookup"><span data-stu-id="85fd5-190">hello `dev.properties` file is passed as a filter, and hello values contained in hello file are read by hello topology.</span></span>

## <a name="view-output-data"></a><span data-ttu-id="85fd5-191">Widok danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="85fd5-191">View output data</span></span>

<span data-ttu-id="85fd5-192">tooview hello dane hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="85fd5-192">tooview hello data, use hello following command:</span></span>

    hdfs dfs -ls /stormdata/

<span data-ttu-id="85fd5-193">Zostanie wyświetlona lista plików hello utworzone przez tej topologii.</span><span class="sxs-lookup"><span data-stu-id="85fd5-193">A list of hello files created by this topology is displayed.</span></span>

<span data-ttu-id="85fd5-194">Witaj poniżej znajduje się przykład hello danych zwróconej przez poprzednie polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="85fd5-194">hello following list is an example of hello data retuned by hello previous commands:</span></span>

    Found 30 items
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-0-1488568403092.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-1-1488568404567.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-10-1488568408678.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-11-1488568411636.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-12-1488568411884.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-13-1488568412603.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-14-1488568415055.txt

## <a name="stop-hello-topology"></a><span data-ttu-id="85fd5-195">Zatrzymywanie topologii hello</span><span class="sxs-lookup"><span data-stu-id="85fd5-195">Stop hello topology</span></span>

<span data-ttu-id="85fd5-196">STORM topologie działają aż do zatrzymania lub klaster hello jest usunięty.</span><span class="sxs-lookup"><span data-stu-id="85fd5-196">Storm topologies run until stopped, or hello cluster is deleted.</span></span> <span data-ttu-id="85fd5-197">toostop hello topologii hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="85fd5-197">toostop hello topology, use hello following command:</span></span>

    storm kill hdfswriter

## <a name="delete-your-cluster"></a><span data-ttu-id="85fd5-198">Usuwanie klastra</span><span class="sxs-lookup"><span data-stu-id="85fd5-198">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="85fd5-199">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="85fd5-199">Next steps</span></span>

<span data-ttu-id="85fd5-200">Teraz, gdy wiesz już, jak toouse Storm toowrite tooAzure magazynu i usługi Azure Data Lake Store, odnajdywanie innych [Storm przykłady dla usługi HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="85fd5-200">Now that you have learned how toouse Storm toowrite tooAzure Storage and Azure Data Lake Store, discover other [Storm examples for HDInsight](hdinsight-storm-example-topology.md).</span></span>

