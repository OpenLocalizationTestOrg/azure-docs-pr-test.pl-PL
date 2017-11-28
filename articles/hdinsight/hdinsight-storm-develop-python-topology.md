---
title: aaaApache Storm z comopnents Python - Azure HDInsight | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toocreate topologii Apache Storm, która używa składników języka Python."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
keywords: "Apache storm w języku python"
ms.assetid: edd0ec4f-664d-4266-910c-6ecc94172ad8
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: python
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/04/2017
ms.author: larryfr
ms.openlocfilehash: 143c639623f1992f913900a7c52d6e3f03c701e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="develop-apache-storm-topologies-using-python-on-hdinsight"></a><span data-ttu-id="be2d1-104">Opracowywanie topologii Apache Storm w usłudze HDInsight przy użyciu języka Python</span><span class="sxs-lookup"><span data-stu-id="be2d1-104">Develop Apache Storm topologies using Python on HDInsight</span></span>

<span data-ttu-id="be2d1-105">Dowiedz się, jak toocreate topologii Apache Storm, która używa składników języka Python.</span><span class="sxs-lookup"><span data-stu-id="be2d1-105">Learn how toocreate an Apache Storm topology that uses Python components.</span></span> <span data-ttu-id="be2d1-106">Apache Storm obsługuje wiele języków, nawet co toocombine składniki z kilku języków w topologii jeden.</span><span class="sxs-lookup"><span data-stu-id="be2d1-106">Apache Storm supports multiple languages, even allowing you toocombine components from several languages in one topology.</span></span> <span data-ttu-id="be2d1-107">Witaj strumień framework (wprowadzona w systemie Storm 0.10.0) pozwala tooeasily tworzenia rozwiązania, które używają składników języka Python.</span><span class="sxs-lookup"><span data-stu-id="be2d1-107">hello Flux framework (introduced with Storm 0.10.0) allows you tooeasily create solutions that use Python components.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="be2d1-108">Witaj informacje w tym dokumencie przetestowano korzystanie z systemu Storm w usłudze HDInsight 3,6.</span><span class="sxs-lookup"><span data-stu-id="be2d1-108">hello information in this document was tested using Storm on HDInsight 3.6.</span></span> <span data-ttu-id="be2d1-109">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="be2d1-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="be2d1-110">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="be2d1-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="be2d1-111">Witaj kod dla tego projektu jest dostępny w [https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount).</span><span class="sxs-lookup"><span data-stu-id="be2d1-111">hello code for this project is available at [https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="be2d1-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="be2d1-112">Prerequisites</span></span>

* <span data-ttu-id="be2d1-113">Python 2.7 lub nowszej</span><span class="sxs-lookup"><span data-stu-id="be2d1-113">Python 2.7 or higher</span></span>

* <span data-ttu-id="be2d1-114">Java JDK 1.8 lub nowszej</span><span class="sxs-lookup"><span data-stu-id="be2d1-114">Java JDK 1.8 or higher</span></span>

* <span data-ttu-id="be2d1-115">Maven 3</span><span class="sxs-lookup"><span data-stu-id="be2d1-115">Maven 3</span></span>

* <span data-ttu-id="be2d1-116">(Opcjonalnie) Lokalne Środowisko deweloperskie Storm.</span><span class="sxs-lookup"><span data-stu-id="be2d1-116">(Optional) A local Storm development environment.</span></span> <span data-ttu-id="be2d1-117">Środowisko lokalne Storm jest potrzebne tylko wtedy, jeśli chcesz, aby lokalnie toorun hello topologii.</span><span class="sxs-lookup"><span data-stu-id="be2d1-117">A local Storm environment is only needed if you want toorun hello topology locally.</span></span> <span data-ttu-id="be2d1-118">Aby uzyskać więcej informacji, zobacz [Konfigurowanie środowiska projektowego](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html).</span><span class="sxs-lookup"><span data-stu-id="be2d1-118">For more information, see [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html).</span></span>

## <a name="storm-multi-language-support"></a><span data-ttu-id="be2d1-119">Obsługa wielu języków STORM</span><span class="sxs-lookup"><span data-stu-id="be2d1-119">Storm multi-language support</span></span>

<span data-ttu-id="be2d1-120">Apache Storm została zaprojektowana toowork ze składnikami napisane przy użyciu dowolnego języka programowania.</span><span class="sxs-lookup"><span data-stu-id="be2d1-120">Apache Storm was designed toowork with components written using any programming language.</span></span> <span data-ttu-id="be2d1-121">składniki Hello, trzeba zrozumieć, jak toowork z hello [Thrift definicji Storm](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift).</span><span class="sxs-lookup"><span data-stu-id="be2d1-121">hello components must understand how toowork with hello [Thrift definition for Storm](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift).</span></span> <span data-ttu-id="be2d1-122">Dla języka Python moduł jest dostarczana jako część hello Apache Storm projektu, który pozwala interfejsu tooeasily z systemu Storm.</span><span class="sxs-lookup"><span data-stu-id="be2d1-122">For Python, a module is provided as part of hello Apache Storm project that allows you tooeasily interface with Storm.</span></span> <span data-ttu-id="be2d1-123">Możesz znaleźć tego modułu w [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py).</span><span class="sxs-lookup"><span data-stu-id="be2d1-123">You can find this module at [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py).</span></span>

<span data-ttu-id="be2d1-124">STORM jest proces Java, który jest uruchamiany na powitania maszyny wirtualnej Java (JVM).</span><span class="sxs-lookup"><span data-stu-id="be2d1-124">Storm is a Java process that runs on hello Java Virtual Machine (JVM).</span></span> <span data-ttu-id="be2d1-125">Składniki napisanych w innych językach są wykonywane jako podprocesy.</span><span class="sxs-lookup"><span data-stu-id="be2d1-125">Components written in other languages are executed as subprocesses.</span></span> <span data-ttu-id="be2d1-126">Witaj Storm komunikuje się z tych podprocesy przy użyciu JSON wiadomości wysyłane za pośrednictwem stdin/stdout.</span><span class="sxs-lookup"><span data-stu-id="be2d1-126">hello Storm communicates with these subprocesses using JSON messages sent over stdin/stdout.</span></span> <span data-ttu-id="be2d1-127">Więcej informacji dotyczących komunikacji między składnikami znajdują się w hello [protokołu Multi-lang](https://storm.apache.org/documentation/Multilang-protocol.html) dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="be2d1-127">More details on communication between components can be found in hello [Multi-lang Protocol](https://storm.apache.org/documentation/Multilang-protocol.html) documentation.</span></span>

## <a name="python-with-hello-flux-framework"></a><span data-ttu-id="be2d1-128">Python hello strumień Framework</span><span class="sxs-lookup"><span data-stu-id="be2d1-128">Python with hello Flux framework</span></span>

<span data-ttu-id="be2d1-129">framework strumień Hello umożliwia topologii Storm toodefine niezależnie od hello składników.</span><span class="sxs-lookup"><span data-stu-id="be2d1-129">hello Flux framework allows you toodefine Storm topologies separately from hello components.</span></span> <span data-ttu-id="be2d1-130">Platforma strumień Hello korzysta z topologii Storm hello toodefine yaml programu.</span><span class="sxs-lookup"><span data-stu-id="be2d1-130">hello Flux framework uses YAML toodefine hello Storm topology.</span></span> <span data-ttu-id="be2d1-131">Witaj następujący tekst jest przykładem tooreference składnika Python w dokumencie yaml programu hello:</span><span class="sxs-lookup"><span data-stu-id="be2d1-131">hello following text is an example of how tooreference a Python component in hello YAML document:</span></span>

```yaml
# Spout definitions
spouts:
  - id: "sentence-spout"
    className: "org.apache.storm.flux.wrappers.spouts.FluxShellSpout"
    constructorArgs:
      # Command line
      - ["python", "sentencespout.py"]
      # Output field(s)
      - ["sentence"]
    # parallelism hint
    parallelism: 1
```

<span data-ttu-id="be2d1-132">Witaj klasy `FluxShellSpout` jest używane toostart hello `sentencespout.py` skrypt, który implementuje hello spout.</span><span class="sxs-lookup"><span data-stu-id="be2d1-132">hello class `FluxShellSpout` is used toostart hello `sentencespout.py` script that implements hello spout.</span></span>

<span data-ttu-id="be2d1-133">Strumień oczekuje toobe skrypty języka Python hello w hello `/resources` katalogu wewnątrz hello jar zawierający hello topologii.</span><span class="sxs-lookup"><span data-stu-id="be2d1-133">Flux expects hello Python scripts toobe in hello `/resources` directory inside hello jar file that contains hello topology.</span></span> <span data-ttu-id="be2d1-134">Dlatego w tym przykładzie przechowuje hello skrypty języka Python w hello `/multilang/resources` katalogu.</span><span class="sxs-lookup"><span data-stu-id="be2d1-134">So this example stores hello Python scripts in hello `/multilang/resources` directory.</span></span> <span data-ttu-id="be2d1-135">Witaj `pom.xml` zawiera ten plik przy użyciu następującego XML hello:</span><span class="sxs-lookup"><span data-stu-id="be2d1-135">hello `pom.xml` includes this file using hello following XML:</span></span>

```xml
<!-- include hello Python components -->
<resource>
    <directory>${basedir}/multilang</directory>
    <filtering>false</filtering>
</resource>
```

<span data-ttu-id="be2d1-136">Jak wspomniano wcześniej, Brak `storm.py` pliku, który implementuje definicji Thrift hello Storm.</span><span class="sxs-lookup"><span data-stu-id="be2d1-136">As mentioned earlier, there is a `storm.py` file that implements hello Thrift definition for Storm.</span></span> <span data-ttu-id="be2d1-137">Struktura strumień Hello obejmuje `storm.py` automatycznie po hello projekt jest budowany, dzięki czemu nie trzeba tooworry o tym go.</span><span class="sxs-lookup"><span data-stu-id="be2d1-137">hello Flux framework includes `storm.py` automatically when hello project is built, so you don't have tooworry about including it.</span></span>

## <a name="build-hello-project"></a><span data-ttu-id="be2d1-138">Tworzenie projektu hello</span><span class="sxs-lookup"><span data-stu-id="be2d1-138">Build hello project</span></span>

<span data-ttu-id="be2d1-139">Witaj katalog główny projektu hello używając hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="be2d1-139">From hello root of hello project, use hello following command:</span></span>

```bash
mvn clean compile package
```

<span data-ttu-id="be2d1-140">To polecenie tworzy `target/WordCount-1.0-SNAPSHOT.jar` plik zawierający hello skompilowany topologii.</span><span class="sxs-lookup"><span data-stu-id="be2d1-140">This command creates a `target/WordCount-1.0-SNAPSHOT.jar` file that contains hello compiled topology.</span></span>

## <a name="run-hello-topology-locally"></a><span data-ttu-id="be2d1-141">Uruchom lokalnie hello topologii</span><span class="sxs-lookup"><span data-stu-id="be2d1-141">Run hello topology locally</span></span>

<span data-ttu-id="be2d1-142">Topologia hello toorun lokalnie, należy użyć hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="be2d1-142">toorun hello topology locally, use hello following command:</span></span>

```bash
storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -l -R /topology.yaml
```

> [!NOTE]
> <span data-ttu-id="be2d1-143">To polecenie wymaga lokalne Środowisko deweloperskie Storm.</span><span class="sxs-lookup"><span data-stu-id="be2d1-143">This command requires a local Storm development environment.</span></span> <span data-ttu-id="be2d1-144">Aby uzyskać więcej informacji, zobacz [Konfigurowanie środowiska projektowego](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html)</span><span class="sxs-lookup"><span data-stu-id="be2d1-144">For more information, see [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html)</span></span>

<span data-ttu-id="be2d1-145">Po uruchomieniu topologii hello, go emituje informacji toohello konsoli lokalnej podobne toohello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="be2d1-145">Once hello topology starts, it emits information toohello local console similar toohello following text:</span></span>


    24302 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting hello cow jumped over hello moon
    24302 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting the
    24302 [Thread-28] INFO  o.a.s.t.ShellBolt - ShellLog pid:2437, name:counter-bolt Emitting years:160
    24302 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=the, count=599}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=seven, count=302}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=dwarfs, count=143}
    24303 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting hello cow jumped over hello moon
    24303 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting cow
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=four, count=160}


<span data-ttu-id="be2d1-146">Topologia hello toostop, użyj __klawisze Ctrl + C__.</span><span class="sxs-lookup"><span data-stu-id="be2d1-146">toostop hello topology, use __Ctrl + C__.</span></span>

## <a name="run-hello-storm-topology-on-hdinsight"></a><span data-ttu-id="be2d1-147">Uruchom hello topologii Storm w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="be2d1-147">Run hello Storm topology on HDInsight</span></span>

1. <span data-ttu-id="be2d1-148">Użyj hello następujące polecenie toocopy hello `WordCount-1.0-SNAPSHOT.jar` pliku tooyour Storm w klastrze usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="be2d1-148">Use hello following command toocopy hello `WordCount-1.0-SNAPSHOT.jar` file tooyour Storm on HDInsight cluster:</span></span>

    ```bash
    scp target\WordCount-1.0-SNAPSHOT.jar sshuser@mycluster-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="be2d1-149">Zastąp `sshuser` hello użytkownika SSH dla klastra.</span><span class="sxs-lookup"><span data-stu-id="be2d1-149">Replace `sshuser` with hello SSH user for your cluster.</span></span> <span data-ttu-id="be2d1-150">Zastąp `mycluster` hello nazwą klastra.</span><span class="sxs-lookup"><span data-stu-id="be2d1-150">Replace `mycluster` with hello cluster name.</span></span> <span data-ttu-id="be2d1-151">Może być tooenter zostanie wyświetlony monit o hasło hello hello użytkownika SSH.</span><span class="sxs-lookup"><span data-stu-id="be2d1-151">You may be prompted tooenter hello password for hello SSH user.</span></span>

    <span data-ttu-id="be2d1-152">Aby uzyskać więcej informacji o korzystaniu protokołów SSH i SCP, zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="be2d1-152">For more information on using SSH and SCP, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="be2d1-153">Po przekazaniu pliku hello, podłącz toohello klastra przy użyciu protokołu SSH:</span><span class="sxs-lookup"><span data-stu-id="be2d1-153">Once hello file has been uploaded, connect toohello cluster using SSH:</span></span>

    ```bash
    ssh sshuser@mycluster-ssh.azurehdinsight.net
    ```

3. <span data-ttu-id="be2d1-154">W sesji SSH hello Użyj następującego polecenia toostart hello topologii w klastrze hello hello:</span><span class="sxs-lookup"><span data-stu-id="be2d1-154">From hello SSH session, use hello following command toostart hello topology on hello cluster:</span></span>

    ```bash
    storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -r -R /topology.yaml
    ```

3. <span data-ttu-id="be2d1-155">W klastrze hello służy hello interfejsu użytkownika platformy Storm tooview hello topologii.</span><span class="sxs-lookup"><span data-stu-id="be2d1-155">You can use hello Storm UI tooview hello topology on hello cluster.</span></span> <span data-ttu-id="be2d1-156">Witaj interfejsu użytkownika platformy Storm znajduje się pod adresem https://mycluster.azurehdinsight.net/stormui.</span><span class="sxs-lookup"><span data-stu-id="be2d1-156">hello Storm UI is located at https://mycluster.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="be2d1-157">Zastąp `mycluster` z nazwą klastra.</span><span class="sxs-lookup"><span data-stu-id="be2d1-157">Replace `mycluster` with your cluster name.</span></span>

> [!NOTE]
> <span data-ttu-id="be2d1-158">Po rozpoczęciu topologii Storm uruchamia aż do zatrzymania.</span><span class="sxs-lookup"><span data-stu-id="be2d1-158">Once started, a Storm topology runs until stopped.</span></span> <span data-ttu-id="be2d1-159">toostop hello topologii, użyj jednej z następujących metod hello:</span><span class="sxs-lookup"><span data-stu-id="be2d1-159">toostop hello topology, use one of hello following methods:</span></span>
>
> * <span data-ttu-id="be2d1-160">Witaj `storm kill TOPOLOGYNAME` polecenia z wiersza polecenia hello</span><span class="sxs-lookup"><span data-stu-id="be2d1-160">hello `storm kill TOPOLOGYNAME` command from hello command line</span></span>
> * <span data-ttu-id="be2d1-161">Witaj **Kill** przycisku na powitania interfejsu użytkownika platformy Storm.</span><span class="sxs-lookup"><span data-stu-id="be2d1-161">hello **Kill** button in hello Storm UI.</span></span>


## <a name="next-steps"></a><span data-ttu-id="be2d1-162">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="be2d1-162">Next steps</span></span>

<span data-ttu-id="be2d1-163">Zobacz hello następujące dokumenty dla innych sposobów toouse Python z usługą HDInsight:</span><span class="sxs-lookup"><span data-stu-id="be2d1-163">See hello following documents for other ways toouse Python with HDInsight:</span></span>

* [<span data-ttu-id="be2d1-164">Jak toouse języka Python dla zadań MapReduce przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="be2d1-164">How toouse Python for streaming MapReduce jobs</span></span>](hdinsight-hadoop-streaming-python.md)
* [<span data-ttu-id="be2d1-165">Jak toouse Python użytkownika określone funkcje (UDF) i Hive</span><span class="sxs-lookup"><span data-stu-id="be2d1-165">How toouse Python User Defined Functions (UDF) in Pig and Hive</span></span>](hdinsight-python.md)
