---
title: "aaaUse Caffe na platformie Azure HDInsight Spark dla rozproszonych learning głębokie | Dokumentacja firmy Microsoft"
description: "Użyj Caffe Azure HDInsight Spark dla rozproszonych learning bezpośrednich"
services: hdinsight
documentationcenter: 
author: xiaoyongzhu
manager: asadk
editor: cgronlun
tags: azure-portal
ms.assetid: 71dcd1ad-4cad-47ad-8a9d-dcb7fa3c2ff9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: xiaoyzhu
ms.openlocfilehash: d6476a7ed3a0df38538e845d7d5404067b01113c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-caffe-on-azure-hdinsight-spark-for-distributed-deep-learning"></a><span data-ttu-id="39df9-103">Użyj Caffe Azure HDInsight Spark dla rozproszonych learning bezpośrednich</span><span class="sxs-lookup"><span data-stu-id="39df9-103">Use Caffe on Azure HDInsight Spark for distributed deep learning</span></span>


## <a name="introduction"></a><span data-ttu-id="39df9-104">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="39df9-104">Introduction</span></span>

<span data-ttu-id="39df9-105">Głębokie learning jest wpływające na od toomanufacturing tootransportation opieki zdrowotnej i inne.</span><span class="sxs-lookup"><span data-stu-id="39df9-105">Deep learning is impacting everything from healthcare tootransportation toomanufacturing, and more.</span></span> <span data-ttu-id="39df9-106">Firm są Włączanie toodeep learning toosolve twardych problemów, takich jak [obrazu klasyfikacji](http://blogs.microsoft.com/next/2015/12/10/microsoft-researchers-win-imagenet-computer-vision-challenge/), [rozpoznawania mowy](http://googleresearch.blogspot.jp/2015/08/the-neural-networks-behind-google-voice.html)obiekt rozpoznawania i komputera tłumaczenia.</span><span class="sxs-lookup"><span data-stu-id="39df9-106">Companies are turning toodeep learning toosolve hard problems, like [image classification](http://blogs.microsoft.com/next/2015/12/10/microsoft-researchers-win-imagenet-computer-vision-challenge/), [speech recognition](http://googleresearch.blogspot.jp/2015/08/the-neural-networks-behind-google-voice.html), object recognition, and machine translation.</span></span> 

<span data-ttu-id="39df9-107">Brak [wielu popularnych środowisk](https://en.wikipedia.org/wiki/Comparison_of_deep_learning_software), takie jak [kognitywnych zestaw narzędzi firmy Microsoft](https://www.microsoft.com/en-us/research/product/cognitive-toolkit/), [Tensorflow](https://www.tensorflow.org/), MXNet, Theano, itp. Caffe jest jednym z hello Najpopularniejsza struktur-symboliczne sieci neuronowej (nadrzędnych), a powszechnie używany w wielu obszarach, w tym komputerze wizji.</span><span class="sxs-lookup"><span data-stu-id="39df9-107">There are [many popular frameworks](https://en.wikipedia.org/wiki/Comparison_of_deep_learning_software), including [Microsoft Cognitive Toolkit](https://www.microsoft.com/en-us/research/product/cognitive-toolkit/), [Tensorflow](https://www.tensorflow.org/), MXNet, Theano, etc. Caffe is one of hello most famous non-symbolic (imperative) neural network frameworks, and widely used in many areas including computer vision.</span></span> <span data-ttu-id="39df9-108">Ponadto [CaffeOnSpark](http://yahoohadoop.tumblr.com/post/139916563586/caffeonspark-open-sourced-for-distributed-deep) łączy Caffe z platformy Apache Spark w takim przypadku głębokość uczenia, które mogą być łatwo używane na platformie Hadoop, istniejącego klastra wraz z potoków Spark ETL zmniejszenie złożoności systemu i czas oczekiwania na learning end-to-end.</span><span class="sxs-lookup"><span data-stu-id="39df9-108">Furthermore, [CaffeOnSpark](http://yahoohadoop.tumblr.com/post/139916563586/caffeonspark-open-sourced-for-distributed-deep) combines Caffe with Apache Spark, in which case deep learning can be easily used on an existing Hadoop cluster together with Spark ETL pipelines, reducing system complexity and latency for end-to-end learning.</span></span>

<span data-ttu-id="39df9-109">[HDInsight](https://azure.microsoft.com/en-us/services/hdinsight/) jest hello tylko klastry analityczne typu open source w pełni zarządzaną chmury Hadoop oferty, który zapewnia zoptymalizowane pod kątem Spark, Hive, MapReduce, HBase, Storm, Kafka i R Server obsługiwana przez SLA 99,9%.</span><span class="sxs-lookup"><span data-stu-id="39df9-109">[HDInsight](https://azure.microsoft.com/en-us/services/hdinsight/) is hello only fully-managed cloud Hadoop offering that provides optimized open source analytic clusters for Spark, Hive, MapReduce, HBase, Storm, Kafka, and R Server backed by a 99.9% SLA.</span></span> <span data-ttu-id="39df9-110">Każda z tych technologii danych big data i aplikacji ISV jest łatwa do wdrożenia w formie zarządzanych klastrów z bezpieczeństwem i monitorowaniem klasy korporacyjnej.</span><span class="sxs-lookup"><span data-stu-id="39df9-110">Each of these big data technologies and ISV applications are easily deployable as managed clusters with enterprise-level security and monitoring.</span></span>

<span data-ttu-id="39df9-111">W przypadku niektórych użytkowników prośbę o nas o tym, jak toouse głębokie uczenia w usłudze HDInsight, czyli produktu PaaS Hadoop firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="39df9-111">Some users are asking us about how toouse deep learning on HDInsight, which is Microsoft's PaaS Hadoop product.</span></span> <span data-ttu-id="39df9-112">Firma Microsoft będzie mieć więcej tooshare w przyszłości hello, ale obecnie chcemy toosummarize techniczne blog na temat toouse Caffe na HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="39df9-112">We will have more tooshare in hello future, but today we want toosummarize a technical blog on how toouse Caffe on HDInsight Spark.</span></span>

<span data-ttu-id="39df9-113">Po zainstalowaniu Caffe przed można zauważyć, że instalacja ta struktura jest nieco trudne.</span><span class="sxs-lookup"><span data-stu-id="39df9-113">If you have installed Caffe before, you will notice that installing this framework is a little bit challenging.</span></span> <span data-ttu-id="39df9-114">W tym wpisie możemy najpierw przedstawiają sposób tooinstall [Caffe na Spark](https://github.com/yahoo/CaffeOnSpark) dla klastra usługi HDInsight, następnie użyć hello wbudowanych MNIST pokaz toodemostrate jak toouse Learning głębokie rozproszonego przy użyciu HDInsight Spark na procesorach.</span><span class="sxs-lookup"><span data-stu-id="39df9-114">In this blog, we will first illustrate how tooinstall [Caffe on Spark](https://github.com/yahoo/CaffeOnSpark) for an HDInsight cluster, then use hello built-in MNIST demo toodemostrate how toouse Distributed Deep Learning using HDInsight Spark on CPUs.</span></span>

<span data-ttu-id="39df9-115">Istnieją cztery główne kroki tooget, działa on w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="39df9-115">There are four major steps tooget it work on HDInsight.</span></span>

1. <span data-ttu-id="39df9-116">Zainstaluj zależności hello wymagane we wszystkich węzłach hello</span><span class="sxs-lookup"><span data-stu-id="39df9-116">Install hello required dependencies on all hello nodes</span></span>
2. <span data-ttu-id="39df9-117">Tworzenie Caffe na Spark dla usługi HDInsight na powitania węzła głównego</span><span class="sxs-lookup"><span data-stu-id="39df9-117">Build Caffe on Spark for HDInsight on hello head node</span></span>
3. <span data-ttu-id="39df9-118">Dystrybuuj węzłów procesu roboczego hello hello wymaganych bibliotek tooall</span><span class="sxs-lookup"><span data-stu-id="39df9-118">Distribute hello required libraries tooall hello worker nodes</span></span>
4. <span data-ttu-id="39df9-119">Napisz modelu Caffe, a następnie uruchom go distributely</span><span class="sxs-lookup"><span data-stu-id="39df9-119">Compose a Caffe model and run it distributely</span></span>

<span data-ttu-id="39df9-120">Ponieważ HDInsight to rozwiązanie typu PaaS, oferuje funkcje platformy dużą — tak jest dość łatwe tooperform niektórych zadań.</span><span class="sxs-lookup"><span data-stu-id="39df9-120">Since HDInsight is a PaaS solution, it offers great platform features - so it is quite easy tooperform some tasks.</span></span> <span data-ttu-id="39df9-121">Nosi nazwę jednej z funkcji hello, które firma Microsoft intensywnie korzystają w tym wpisie w blogu [akcji skryptu](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux), z którego można wykonywać powłoki poleceń toocustomize węzłów klastra (węzła głównego węzła procesu roboczego i węzłem krawędzi).</span><span class="sxs-lookup"><span data-stu-id="39df9-121">One of hello features that we heavily use in this blog post is called [Script Action](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux), with which you can execute shell commands toocustomize cluster nodes (head node, worker node, or edge node).</span></span>

## <a name="step-1--install-hello-required-dependencies-on-all-hello-nodes"></a><span data-ttu-id="39df9-122">Krok 1: Instalowanie zależności hello wymagane we wszystkich węzłach hello</span><span class="sxs-lookup"><span data-stu-id="39df9-122">Step 1:  Install hello required dependencies on all hello nodes</span></span>

<span data-ttu-id="39df9-123">Rozpoczęto tooget, potrzebujemy tooinstall hello zależności, które należy.</span><span class="sxs-lookup"><span data-stu-id="39df9-123">tooget started, we need tooinstall hello dependencies we need.</span></span> <span data-ttu-id="39df9-124">Hello Caffe lokacji i [lokacji CaffeOnSpark](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn) oferuje niektóre przydatne wiki do instalowania zależności hello platformy Spark w trybie YARN (który jest trybem hello Spark w usłudze HDInsight), ale potrzebujemy tooadd kilka zależności więcej HDInsight platformy.</span><span class="sxs-lookup"><span data-stu-id="39df9-124">hello Caffe site and [CaffeOnSpark site](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn) offers some very useful wiki for installing hello dependencies for Spark on YARN mode (which is hello mode for HDInsight Spark), but we need tooadd a few more dependencies for HDInsight platform.</span></span> <span data-ttu-id="39df9-125">Firma Microsoft będzie użyć akcji skryptu hello zgodnie z poniższymi instrukcjami i uruchom go na wszystkich węzłach głównych hello i węzłów procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="39df9-125">We will use hello script action as below and run it on all hello head nodes and worker nodes.</span></span> <span data-ttu-id="39df9-126">Ta akcja skryptu potrwa około 20 minut, jak te zależności również są zależne od innych pakietów.</span><span class="sxs-lookup"><span data-stu-id="39df9-126">This script action will take about 20 minutes, as those dependencies also depend on other packages.</span></span> <span data-ttu-id="39df9-127">Należy umieścić go w niektórych lokalizacji, która jest dostępna tooyour klastra usługi HDInsight, takie jak lokalizacja GitHub lub hello domyślne konto magazynu obiektów BLOB.</span><span class="sxs-lookup"><span data-stu-id="39df9-127">You should put it in some location that is accessible tooyour HDInsight cluster, such as a GitHub location or hello default BLOB storage account.</span></span>

    #!/bin/bash
    #Please be aware that installing hello below will add additional 20 mins toocluster creation because of hello dependencies
    #installing all dependencies, including hello ones mentioned in http://caffe.berkeleyvision.org/install_apt.html, as well a few packages that are not included in HDInsight, such as gflags, glog, lmdb, numpy
    #It seems numpy will only needed during compilation time, but for safety purpose we install them on all hello nodes

    sudo apt-get install -y libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler maven libatlas-base-dev libgflags-dev libgoogle-glog-dev liblmdb-dev build-essential  libboost-all-dev python-numpy python-scipy python-matplotlib ipython ipython-notebook python-pandas python-sympy python-nose

    #install protobuf
    wget https://github.com/google/protobuf/releases/download/v2.5.0/protobuf-2.5.0.tar.gz
    sudo tar xzvf protobuf-2.5.0.tar.gz -C /tmp/
    cd /tmp/protobuf-2.5.0/
    sudo ./configure
    sudo make
    sudo make check
    sudo make install
    sudo ldconfig
    echo "protobuf installation done"


<span data-ttu-id="39df9-128">Istnieją dwa kroki w akcji skryptu hello powyżej.</span><span class="sxs-lookup"><span data-stu-id="39df9-128">There are two steps in hello script action above.</span></span> <span data-ttu-id="39df9-129">pierwszym krokiem Hello jest tooinstall hello wszystkich wymaganych bibliotek.</span><span class="sxs-lookup"><span data-stu-id="39df9-129">hello first step is tooinstall all hello required libraries.</span></span> <span data-ttu-id="39df9-130">Te biblioteki zawierają hello wymagane biblioteki dla kompilacji Caffe (na przykład gflags, glog) i systemem Caffe (na przykład numpy).</span><span class="sxs-lookup"><span data-stu-id="39df9-130">Those libraries include hello necessary libraries for both compiling Caffe(such as gflags, glog) and running Caffe (such as numpy).</span></span> <span data-ttu-id="39df9-131">Używamy libatlas optymalizacji Procesora, ale zawsze można wykonać hello CaffeOnSpark wiki na temat instalowania innych bibliotek optymalizacji, takie jak MKL lub CUDA (dla procesora GPU).</span><span class="sxs-lookup"><span data-stu-id="39df9-131">We are using libatlas for CPU optimization, but you can always follow hello CaffeOnSpark wiki on installing other optimization libraries, such as MKL or CUDA (for GPU).</span></span>

<span data-ttu-id="39df9-132">drugim krokiem Hello jest toodownload, skompilować i zainstalować protobuf 2.5.0 dla Caffe w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="39df9-132">hello second step is toodownload, compile, and install protobuf 2.5.0 for Caffe during runtime.</span></span> <span data-ttu-id="39df9-133">Protobuf 2.5.0 [wymagana jest](https://github.com/yahoo/CaffeOnSpark/issues/87), ale ta wersja nie jest dostępny jako pakiet na Ubuntu 16, więc musimy toocompile z hello kodu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="39df9-133">Protobuf 2.5.0 [is required](https://github.com/yahoo/CaffeOnSpark/issues/87), however this version is not available as a package on Ubuntu 16, so we need toocompile it from hello source code.</span></span> <span data-ttu-id="39df9-134">Dostępne są również kilka zasoby na powitania internetowe na temat toocompile, takich jak [to](http://jugnu-life.blogspot.com/2013/09/install-protobuf-25-on-ubuntu.html)</span><span class="sxs-lookup"><span data-stu-id="39df9-134">There are also a few resources on hello Internet on how toocompile it, such as [this](http://jugnu-life.blogspot.com/2013/09/install-protobuf-25-on-ubuntu.html)</span></span>

<span data-ttu-id="39df9-135">toosimply rozpocząć pracę, możesz tylko uruchamiać tę akcję skryptu na proces roboczy z klastra tooall hello węzły węzłów i head (dla usługi HDInsight 3.5).</span><span class="sxs-lookup"><span data-stu-id="39df9-135">toosimply get started, you can just run this script action against your cluster tooall hello worker nodes and head nodes (for HDInsight 3.5).</span></span> <span data-ttu-id="39df9-136">Można uruchomić akcji skryptu hello uruchomionych klastra lub hello akcji skryptu można również uruchomić w czasie udostępniania klastra hello.</span><span class="sxs-lookup"><span data-stu-id="39df9-136">You can either run hello script actions for a running cluster, or you can also run hello script actions during hello cluster provision time.</span></span> <span data-ttu-id="39df9-137">Więcej szczegółów na powitania akcji skryptu, można znaleźć w dokumentacji hello [tutaj](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux#view-history-promote-and-demote-script-actions)</span><span class="sxs-lookup"><span data-stu-id="39df9-137">For more details on hello script actions, please see hello documentation [here](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux#view-history-promote-and-demote-script-actions)</span></span>

![TooInstall akcji skryptu zależności](./media/hdinsight-deep-learning-caffe-spark/Script-Action-1.png)


## <a name="step-2-build-caffe-on-spark-for-hdinsight-on-hello-head-node"></a><span data-ttu-id="39df9-139">Krok 2: Tworzenie Caffe Spark dla usługi HDInsight na powitania węzła głównego</span><span class="sxs-lookup"><span data-stu-id="39df9-139">Step 2: Build Caffe on Spark for HDInsight on hello head node</span></span>

<span data-ttu-id="39df9-140">drugi etap Hello jest toobuild Caffe na powitania headnode, a następnie dystrybucję węzłów procesu roboczego hello tooall bibliotek hello skompilowany.</span><span class="sxs-lookup"><span data-stu-id="39df9-140">hello second step is toobuild Caffe on hello headnode, and then distribute hello compiled libraries tooall hello worker nodes.</span></span> <span data-ttu-id="39df9-141">W tym kroku należy zbyt[ssh do Twojej headnode](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix), po prostu wykonaj hello [proces kompilacji CaffeOnSpark](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn), i poniżej znajduje się skrypt hello za pomocą toobuild CaffeOnSpark kilka dodatkowych czynności.</span><span class="sxs-lookup"><span data-stu-id="39df9-141">In this step, you will need too[ssh into your headnode](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix), then simply follow hello [CaffeOnSpark build process](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn), and below is hello script you can use toobuild CaffeOnSpark with a few additional steps.</span></span> 

    #!/bin/bash
    git clone https://github.com/yahoo/CaffeOnSpark.git --recursive
    export CAFFE_ON_SPARK=$(pwd)/CaffeOnSpark

    pushd ${CAFFE_ON_SPARK}/caffe-public/
    cp Makefile.config.example Makefile.config
    echo "INCLUDE_DIRS += ${JAVA_HOME}/include" >> Makefile.config
    #Below configurations might need toobe updated based on actual cases. For example, if you are using GPU, or using a different BLAS library, you may want tooupdate those settings accordingly.
    echo "CPU_ONLY := 1" >> Makefile.config
    echo "BLAS := atlas" >> Makefile.config
    echo "INCLUDE_DIRS += /usr/include/hdf5/serial/" >> Makefile.config
    echo "LIBRARY_DIRS += /usr/lib/x86_64-linux-gnu/hdf5/serial/" >> Makefile.config
    popd

    #compile CaffeOnSpark
    pushd ${CAFFE_ON_SPARK}
    #always clean up hello environment before building (especially when rebuiding), or there will be errors such as "failed tooexecute goal org.apache.maven.plugins:maven-antrun-plugin:1.7:run (proto) on project caffe-distri: An Ant BuildException has occured: exec returned: 2"
    make clean 
    #hello build step usually takes 20~30 mins, since it has a lot maven dependencies
    make build 
    popd
    export LD_LIBRARY_PATH=${CAFFE_ON_SPARK}/caffe-public/distribute/lib:${CAFFE_ON_SPARK}/caffe-distri/distribute/lib

    hadoop fs -mkdir -p wasb:///projects/machine_learning/image_dataset

    ${CAFFE_ON_SPARK}/scripts/setup-mnist.sh
    hadoop fs -put -f ${CAFFE_ON_SPARK}/data/mnist_*_lmdb wasb:///projects/machine_learning/image_dataset/

    ${CAFFE_ON_SPARK}/scripts/setup-cifar10.sh
    hadoop fs -put -f ${CAFFE_ON_SPARK}/data/cifar10_*_lmdb wasb:///projects/machine_learning/image_dataset/

    #put hello already compiled CaffeOnSpark libraries toowasb storage, then read back tooeach node using script actions. This is because CaffeOnSpark requires all hello nodes have hello libarries
    hadoop fs -mkdir -p /CaffeOnSpark/caffe-public/distribute/lib/
    hadoop fs -mkdir -p /CaffeOnSpark/caffe-distri/distribute/lib/
    hadoop fs -put CaffeOnSpark/caffe-distri/distribute/lib/* /CaffeOnSpark/caffe-distri/distribute/lib/
    hadoop fs -put CaffeOnSpark/caffe-public/distribute/lib/* /CaffeOnSpark/caffe-public/distribute/lib/

<span data-ttu-id="39df9-142">Może być konieczne toodo więcej niż mówi jakie dokumentacji hello CaffeOnSpark.</span><span class="sxs-lookup"><span data-stu-id="39df9-142">You may need toodo more than what hello documentation of CaffeOnSpark says.</span></span> <span data-ttu-id="39df9-143">zmiany Hello są następujące:</span><span class="sxs-lookup"><span data-stu-id="39df9-143">hello changes are:</span></span>
- <span data-ttu-id="39df9-144">Zmień tylko tooCPU i użyj libatlas w tym konkretnym celu.</span><span class="sxs-lookup"><span data-stu-id="39df9-144">Change tooCPU only and use libatlas for this particular purpose.</span></span>
- <span data-ttu-id="39df9-145">Umieść hello zestawów danych toohello magazynu obiektów BLOB, który prowadzi do lokalizacji udostępnionej, który jest dostępny tooall węzłów procesu roboczego do późniejszego użycia.</span><span class="sxs-lookup"><span data-stu-id="39df9-145">Put hello datasets toohello BLOB storage, which is a shared location that is accessible tooall worker nodes for later use.</span></span>
- <span data-ttu-id="39df9-146">Umieść hello skompilowany Caffe biblioteki tooBLOB magazynu i później skopiuje tych węzłów hello tooall biblioteki za pomocą akcji skryptów w czasie kompilacji dodatkowe tooavoid.</span><span class="sxs-lookup"><span data-stu-id="39df9-146">Put hello compiled Caffe libraries tooBLOB storage, and later you will copy those libraries tooall hello nodes using script actions tooavoid additional compilation time.</span></span>


### <a name="troubleshooting-an-ant-buildexception-has-occured-exec-returned-2"></a><span data-ttu-id="39df9-147">Rozwiązywanie problemów: Wystąpił BuildException Ant: exec zwrócił: 2</span><span class="sxs-lookup"><span data-stu-id="39df9-147">Troubleshooting: An Ant BuildException has occured: exec returned: 2</span></span>

<span data-ttu-id="39df9-148">Podczas próby najpierw toobuild CaffeOnSpark, czasami jest wyświetlany tekst</span><span class="sxs-lookup"><span data-stu-id="39df9-148">When first trying toobuild CaffeOnSpark, sometimes it will say</span></span>

    failed tooexecute goal org.apache.maven.plugins:maven-antrun-plugin:1.7:run (proto) on project caffe-distri: An Ant BuildException has occured: exec returned: 2

<span data-ttu-id="39df9-149">Po prostu czystą hello repozytorium kodu przez "Sprawdź czystą", a następnie wykonywania "Sprawdź kompilacji" rozwiąże ten problem, tak długo, jak długo mają hello prawidłowymi zależnościami.</span><span class="sxs-lookup"><span data-stu-id="39df9-149">Simply clean hello code repository by "make clean" and then run "make build" will solve this issue, as long as you have hello correct dependencies.</span></span>

### <a name="troubleshooting-maven-repository-connection-time-out"></a><span data-ttu-id="39df9-150">Rozwiązywanie problemów: Limit czasu połączenia repozytorium Maven</span><span class="sxs-lookup"><span data-stu-id="39df9-150">Troubleshooting: Maven repository connection time out</span></span>

<span data-ttu-id="39df9-151">Czasami maven zapewnia dużą elastyczność błąd przekroczenia limitu czasu połączenia hello, podobne toobelow:</span><span class="sxs-lookup"><span data-stu-id="39df9-151">Sometimes maven gives me hello connection time out error, similar toobelow:</span></span>

    Retry:
    [INFO] Downloading: https://repo.maven.apache.org/maven2/com/twitter/chill_2.11/0.8.0/chill_2.11-0.8.0.jar
    Feb 01, 2017 5:14:49 AM org.apache.maven.wagon.providers.http.httpclient.impl.execchain.RetryExec execute
    INFO: I/O exception (java.net.SocketException) caught when processing request too{s}->https://repo.maven.apache.org:443: Connection timed out (Read failed)

<span data-ttu-id="39df9-152">Zostanie ono OK po odczekaniu za kilka minut i spróbuj właśnie toorebuild hello kodu, więc może być Maven jakiś sposób limity hello ruch z danego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="39df9-152">It will be OK after waiting for a few minutes and then just try toorebuild hello code, so it might be Maven somehow limits hello traffic from a given IP address.</span></span>


### <a name="troubleshooting-test-failure-for-caffe"></a><span data-ttu-id="39df9-153">Rozwiązywanie problemów: Błąd testowego dla Caffe</span><span class="sxs-lookup"><span data-stu-id="39df9-153">Troubleshooting: Test failure for Caffe</span></span>

<span data-ttu-id="39df9-154">Prawdopodobnie zobaczysz niepowodzenia testu podczas wykonywania hello końcowego sprawdzaj CaffeOnSpark podobne z poniżej.</span><span class="sxs-lookup"><span data-stu-id="39df9-154">You probably will see a test failure when doing hello final check for CaffeOnSpark, similar with below.</span></span> <span data-ttu-id="39df9-155">Jest to prabably związanych z kodowaniem UTF-8, ale powinien mieć wpływu na użycie hello Caffe</span><span class="sxs-lookup"><span data-stu-id="39df9-155">This is prabably related with UTF-8 encoding, but should not impact hello usage of Caffe</span></span>

    Run completed in 32 seconds, 78 milliseconds.
    Total number of tests run: 7
    Suites: completed 5, aborted 0
    Tests: succeeded 6, failed 1, canceled 0, ignored 0, pending 0
    *** 1 TEST FAILED ***

## <a name="step-3-distribute-hello-required-libraries-tooall-hello-worker-nodes"></a><span data-ttu-id="39df9-156">Krok 3: Dystrybucji węzłów procesu roboczego hello hello wymaganych bibliotek tooall</span><span class="sxs-lookup"><span data-stu-id="39df9-156">Step 3: Distribute hello required libraries tooall hello worker nodes</span></span>

<span data-ttu-id="39df9-157">Hello następnym krokiem jest toodistribute hello bibliotek (zasadniczo hello bibliotek CaffeOnSpark/caffe publicznego/dystrybucji/lib/i CaffeOnSpark/caffe dystry/dystrybucji/lib /) węzły hello tooall.</span><span class="sxs-lookup"><span data-stu-id="39df9-157">hello next step is toodistribute hello libraries (basically hello libraries in CaffeOnSpark/caffe-public/distribute/lib/ and CaffeOnSpark/caffe-distri/distribute/lib/) tooall hello nodes.</span></span> <span data-ttu-id="39df9-158">W kroku 2 testujemy tych bibliotek w magazynie obiektów BLOB, a w tym kroku zostanie wykorzystany toocopy akcji skryptu go tooall hello węzłów głównych i węzłów procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="39df9-158">In Step 2, we put those libraries on BLOB storage, and in this step, we will use script actions toocopy it tooall hello head nodes and worker nodes.</span></span>

<span data-ttu-id="39df9-159">toodo, prosty, Uruchom akcję skryptu zgodnie z poniższymi instrukcjami (należy toopoint toohello odpowiedniej lokalizacji tooyour określonego klastra):</span><span class="sxs-lookup"><span data-stu-id="39df9-159">toodo this, simple run a script action as below (you need toopoint toohello right location specific tooyour cluster):</span></span>

    #!/bin/bash
    hadoop fs -get wasb:///CaffeOnSpark /home/changetoyourusername/

<span data-ttu-id="39df9-160">Ponieważ w kroku 2, testujemy go na powitania magazynu obiektów BLOB, który jest dostępny tooall hello węzły, w tym kroku będziemy wystarczy po prostu skopiuj go tooall hello węzłów.</span><span class="sxs-lookup"><span data-stu-id="39df9-160">Because in step 2, we put it on hello BLOB storage which is accessible tooall hello nodes, in this step we just simply copy it tooall hello nodes.</span></span>

## <a name="step-4-compose-a-caffe-model-and-run-it-distributely"></a><span data-ttu-id="39df9-161">Krok 4: Utworzenie modelu Caffe i uruchom go distributely</span><span class="sxs-lookup"><span data-stu-id="39df9-161">Step 4: Compose a Caffe model and run it distributely</span></span>

<span data-ttu-id="39df9-162">Po uruchomieniu hello powyżej kroki, Caffe jest już zainstalowana na powitania headnode i nie jesteśmy toogo dobra.</span><span class="sxs-lookup"><span data-stu-id="39df9-162">After running hello above steps, Caffe is alreay installed on hello headnode and we are good toogo.</span></span> <span data-ttu-id="39df9-163">Witaj następnym krokiem jest toowrite Caffe modelu.</span><span class="sxs-lookup"><span data-stu-id="39df9-163">hello next step is toowrite a Caffe model.</span></span> 

<span data-ttu-id="39df9-164">Caffe używa "Architektura obszerne", gdy do tworzenia modelu, należy po prostu muszą toodefine plik konfiguracji i bez kodowania w ogóle (w większości przypadków).</span><span class="sxs-lookup"><span data-stu-id="39df9-164">Caffe is using an "expressive architecture", where for composing a model, you just need toodefine a configuration file, and without coding at all (in most cases).</span></span> <span data-ttu-id="39df9-165">Dlatego Spójrzmy istnieje.</span><span class="sxs-lookup"><span data-stu-id="39df9-165">So let's take a look there.</span></span> 

<span data-ttu-id="39df9-166">Firma Microsoft będzie dzisiaj uczenia modelu Hello to model próbki szkolenia MNIST.</span><span class="sxs-lookup"><span data-stu-id="39df9-166">hello model we will train today is a sample model for MNIST training.</span></span> <span data-ttu-id="39df9-167">bazy danych MNIST Hello odręcznie cyfr ma zestaw szkolenia 60 000 przykłady i zbiór przykłady 10 000.</span><span class="sxs-lookup"><span data-stu-id="39df9-167">hello MNIST database of handwritten digits has a training set of 60,000 examples, and a test set of 10,000 examples.</span></span> <span data-ttu-id="39df9-168">Jest ona podzbiorem większy zestaw dostępnej w sklepie NIST.</span><span class="sxs-lookup"><span data-stu-id="39df9-168">It is a subset of a larger set available from NIST.</span></span> <span data-ttu-id="39df9-169">Witaj cyfr zostały znormalizowany rozmiar i wyśrodkowany w obrazie stałym rozmiarze.</span><span class="sxs-lookup"><span data-stu-id="39df9-169">hello digits have been size-normalized and centered in a fixed-size image.</span></span> <span data-ttu-id="39df9-170">CaffeOnSpark ma niektóre skrypty toodownload hello dataset i przekształcić ją w prawidłowym formacie hello.</span><span class="sxs-lookup"><span data-stu-id="39df9-170">CaffeOnSpark has some scripts toodownload hello dataset and convert it into hello right format.</span></span>

<span data-ttu-id="39df9-171">CaffeOnSpark zawiera przykładowe topologie sieci MNIST szkolenia.</span><span class="sxs-lookup"><span data-stu-id="39df9-171">CaffeOnSpark provides some network topologies example for MNIST training.</span></span> <span data-ttu-id="39df9-172">Ma ona nieuprzywilejowany projektowania podziału architektury sieci hello (hello topologii sieci hello) i optymalizacji.</span><span class="sxs-lookup"><span data-stu-id="39df9-172">It has a nice design of splitting hello network architecture (hello topology of hello network) and optimization.</span></span> <span data-ttu-id="39df9-173">W takim przypadku istnieją dwa pliki wymagane:</span><span class="sxs-lookup"><span data-stu-id="39df9-173">In this case, There are two files required:</span></span> 

<span data-ttu-id="39df9-174">Witaj "Solver" (${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt) jest używany plik nadzorowaniu hello optymalizacji i generowania parametru aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="39df9-174">hello "Solver" file (${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt) is used for overseeing hello optimization and generating parameter updates.</span></span> <span data-ttu-id="39df9-175">Na przykład, określa czy procesora CPU, czy procesor GPU będą używane, co to jest pęd hello, będzie jak dużo iteracji, itp. Definiuje również, które neuronu topologii sieci należy hello program wykorzystania (hello drugi plik potrzebne).</span><span class="sxs-lookup"><span data-stu-id="39df9-175">For example, it defines whether CPU or GPU will be used, what's hello momentum, how many iterations will be, etc. It also defines which neuron network topology should hello program use (which is hello second file we need).</span></span> <span data-ttu-id="39df9-176">Aby uzyskać więcej informacji na temat Solver można znaleźć zbyt[dokumentacji Caffe](http://caffe.berkeleyvision.org/tutorial/solver.html).</span><span class="sxs-lookup"><span data-stu-id="39df9-176">For more information about Solver, please refer too[Caffe documentation](http://caffe.berkeleyvision.org/tutorial/solver.html).</span></span>

<span data-ttu-id="39df9-177">Na przykład ponieważ używamy Procesora niż procesora GPU, możemy należy zmienić hello ostatni wiersz, aby:</span><span class="sxs-lookup"><span data-stu-id="39df9-177">For this example, since we are using CPU rather than GPU, we should change hello last line to:</span></span>

    # solver mode: CPU or GPU
    solver_mode: CPU

![Caffe konfiguracji](./media/hdinsight-deep-learning-caffe-spark/Caffe-1.png)

<span data-ttu-id="39df9-179">W razie potrzeby można zmienić innych wierszy.</span><span class="sxs-lookup"><span data-stu-id="39df9-179">You can change other lines as needed.</span></span>

<span data-ttu-id="39df9-180">drugi plik Hello (${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt) definiuje sposób sieci neuronu hello wygląda i hello odpowiednie dane wejściowe i pliku wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="39df9-180">hello second file (${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt) defines how hello neuron network looks like, and hello relevant input and output file.</span></span> <span data-ttu-id="39df9-181">Należy również lokalizacja danych szkoleniowych hello tooreflect tooupdate hello pliku.</span><span class="sxs-lookup"><span data-stu-id="39df9-181">We also need tooupdate hello file tooreflect hello training data location.</span></span> <span data-ttu-id="39df9-182">Zmień hello następujące części w lenet_memory_train_test.prototxt (należy toopoint toohello odpowiedniej lokalizacji tooyour określonego klastra):</span><span class="sxs-lookup"><span data-stu-id="39df9-182">Change hello following part in lenet_memory_train_test.prototxt (you need toopoint toohello right location specific tooyour cluster):</span></span>

- <span data-ttu-id="39df9-183">Zmień hello "file:/Users/mridul/bigml/demodl/mnist_train_lmdb" za "wasb: / / / projektów/machine_learning/image_dataset/mnist_train_lmdb"</span><span class="sxs-lookup"><span data-stu-id="39df9-183">change hello "file:/Users/mridul/bigml/demodl/mnist_train_lmdb" too"wasb:///projects/machine_learning/image_dataset/mnist_train_lmdb"</span></span>
- <span data-ttu-id="39df9-184">Zmień "file:/Users/mridul/bigml/demodl/mnist_test_lmdb/" za "wasb: / / / projektów/machine_learning/image_dataset/mnist_test_lmdb"</span><span class="sxs-lookup"><span data-stu-id="39df9-184">change "file:/Users/mridul/bigml/demodl/mnist_test_lmdb/" too"wasb:///projects/machine_learning/image_dataset/mnist_test_lmdb"</span></span>

![Caffe konfiguracji](./media/hdinsight-deep-learning-caffe-spark/Caffe-2.png)

<span data-ttu-id="39df9-186">Aby uzyskać więcej informacji dotyczących sposobu toodefine hello sieci, sprawdź hello [Caffe dokumentacja MNIST zestawu danych](http://caffe.berkeleyvision.org/gathered/examples/mnist.html)</span><span class="sxs-lookup"><span data-stu-id="39df9-186">For more information on how toodefine hello network, please check hello [Caffe documentation on MNIST dataset](http://caffe.berkeleyvision.org/gathered/examples/mnist.html)</span></span>

<span data-ttu-id="39df9-187">W celu hello ten blog używamy są po prostu to prosty przykład MNIST.</span><span class="sxs-lookup"><span data-stu-id="39df9-187">For hello purpose of this blog, we just use this simple MNIST example.</span></span> <span data-ttu-id="39df9-188">Poniższe polecenie hello uruchamiać z węzłem głównym hello:</span><span class="sxs-lookup"><span data-stu-id="39df9-188">You should run hello command below from hello head node:</span></span>

    spark-submit --master yarn --deploy-mode cluster --num-executors 8 --files ${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt,${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt --conf spark.driver.extraLibraryPath="${LD_LIBRARY_PATH}" --conf spark.executorEnv.LD_LIBRARY_PATH="${LD_LIBRARY_PATH}" --class com.yahoo.ml.caffe.CaffeOnSpark ${CAFFE_ON_SPARK}/caffe-grid/target/caffe-grid-0.1-SNAPSHOT-jar-with-dependencies.jar -train -features accuracy,loss -label label -conf lenet_memory_solver.prototxt -devices 1 -connection ethernet -model wasb:///mnist.model -output wasb:///mnist_features_result

<span data-ttu-id="39df9-189">Zasadniczo rozpowszechnia hello wymagane pliki przędza kontenera tooeach (lenet_memory_solver.prototxt i lenet_memory_train_test.prototxt), a także ustawić hello odpowiednich ŚCIEŻKĘ każdego tooLD_LIBRARY_PATH sterownik/Moduł wykonujący Spark, który jest zdefiniowany w hello poprzednie kodu fragment kodu i punktów toohello lokalizacji, która ma CaffeOnSpark biblioteki.</span><span class="sxs-lookup"><span data-stu-id="39df9-189">Basically it distributes hello required files (lenet_memory_solver.prototxt and lenet_memory_train_test.prototxt) tooeach YARN container, and also set hello relevant PATH of each Spark driver/executor tooLD_LIBRARY_PATH, which is defined in hello previous code snippet and points toohello location that has CaffeOnSpark libraries.</span></span> 

## <a name="monitoring-and-troubleshooting"></a><span data-ttu-id="39df9-190">Monitorowanie i rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="39df9-190">Monitoring and troubleshooting</span></span>

<span data-ttu-id="39df9-191">Ponieważ używamy YARN tryb klastra, w tym przypadku sterownik Spark hello będzie zaplanowane tooan dowolnego kontenera (i węzła procesu roboczego dowolnego) powinien widoczne są tylko w konsoli hello Generowanie coś, takich jak:</span><span class="sxs-lookup"><span data-stu-id="39df9-191">Since we are using YARN cluster mode, in which case hello Spark driver will be scheduled tooan arbitrary container (and an arbitrary worker node) you should only see in hello console outputting something like:</span></span>

    17/02/01 23:22:16 INFO Client: Application report for application_1485916338528_0015 (state: RUNNING)

<span data-ttu-id="39df9-192">Jeśli chcesz tooknow, co się stało, należy zwykle sterownika tooget hello Spark dziennika, który zawiera więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="39df9-192">If you want tooknow what happened, you usually need tooget hello Spark driver's log, which has more information.</span></span> <span data-ttu-id="39df9-193">W takim przypadku należy toogo toohello interfejsie użytkownika YARN toofind hello odpowiednich dzienniki YARN.</span><span class="sxs-lookup"><span data-stu-id="39df9-193">In this case, you need toogo toohello YARN UI toofind hello relevant YARN logs.</span></span> <span data-ttu-id="39df9-194">Możesz uzyskać hello interfejsie użytkownika YARN przez ten adres URL:</span><span class="sxs-lookup"><span data-stu-id="39df9-194">You can get hello YARN UI by this URL:</span></span> 

    https://yourclustername.azurehdinsight.net/yarnui
   
![YARN INTERFEJSU UŻYTKOWNIKA](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-1.png)

<span data-ttu-id="39df9-196">Użytkownik może Spójrz na ile zasoby są przydzielane dla konkretnej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="39df9-196">You can take a look at how many resources are allocated for this particular application.</span></span> <span data-ttu-id="39df9-197">Możesz kliknąć łącze "Harmonogramu" hello, a zostanie wyświetlona dla tej aplikacji, czy 9 kontenery uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="39df9-197">You can click hello "Scheduler" link, and then you will see that for this application, there are 9 containers running.</span></span> <span data-ttu-id="39df9-198">Prosimy YARN tooprovide 8 modułów, a innego kontenera jest procesu sterownika.</span><span class="sxs-lookup"><span data-stu-id="39df9-198">We ask YARN tooprovide 8 executors, and another container is for driver process.</span></span> 

![YARN harmonogramu](./media/hdinsight-deep-learning-caffe-spark/YARN-Scheduler.png)

<span data-ttu-id="39df9-200">Jeśli występują błędy może być toocheck hello sterownik dzienników lub dzienniki kontenera.</span><span class="sxs-lookup"><span data-stu-id="39df9-200">You may want toocheck hello  driver logs or container logs if there are failures.</span></span> <span data-ttu-id="39df9-201">W przypadku dzienników sterownika można kliknij Identyfikatora aplikacji hello w interfejsie użytkownika YARN, następnie kliknij przycisk "Dzienniki" hello.</span><span class="sxs-lookup"><span data-stu-id="39df9-201">For driver logs, you can click hello application ID in YARN UI, then click hello "Logs" button.</span></span> <span data-ttu-id="39df9-202">Dzienniki sterownik Hello są zapisywane do strumienia wyjściowego stderr.</span><span class="sxs-lookup"><span data-stu-id="39df9-202">hello driver logs are written into stderr.</span></span>

![INTERFEJS UŻYTKOWNIKA YARN 2](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-2.png)

<span data-ttu-id="39df9-204">Na przykład można napotkać niektóre błąd hello poniżej z dzienników sterownik hello, wskazujący, że przydzielenie zbyt wiele modułów.</span><span class="sxs-lookup"><span data-stu-id="39df9-204">For example, you might see some of hello error below from hello driver logs, indicating you allocate too many executors.</span></span>

    17/02/01 07:26:06 ERROR ApplicationMaster: User class threw exception: java.lang.IllegalStateException: Insufficient training data. Please adjust hyperparameters or increase dataset.
    java.lang.IllegalStateException: Insufficient training data. Please adjust hyperparameters or increase dataset.
        at com.yahoo.ml.caffe.CaffeOnSpark.trainWithValidation(CaffeOnSpark.scala:261)
        at com.yahoo.ml.caffe.CaffeOnSpark$.main(CaffeOnSpark.scala:42)
        at com.yahoo.ml.caffe.CaffeOnSpark.main(CaffeOnSpark.scala)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:498)
        at org.apache.spark.deploy.yarn.ApplicationMaster$$anon$2.run(ApplicationMaster.scala:627)

<span data-ttu-id="39df9-205">Czasami hello problem może się zdarzyć w modułów zamiast sterowniki.</span><span class="sxs-lookup"><span data-stu-id="39df9-205">Sometimes, hello issue can happen in executors rather than drivers.</span></span> <span data-ttu-id="39df9-206">W takim przypadku należy toocheck hello kontenera dzienników.</span><span class="sxs-lookup"><span data-stu-id="39df9-206">In this case, you need toocheck hello container logs.</span></span> <span data-ttu-id="39df9-207">Zawsze uzyskać hello kontenera dzienniki i następnie Uzyskaj hello kontenera nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="39df9-207">You can always get hello container logs, and then get hello failed container.</span></span> <span data-ttu-id="39df9-208">Na przykład ten błąd może spełniać podczas uruchamiania Caffe.</span><span class="sxs-lookup"><span data-stu-id="39df9-208">For example, you might meet this failure when running Caffe.</span></span>

    17/02/01 07:12:05 WARN YarnAllocator: Container marked as failed: container_1485916338528_0008_05_000005 on host: 10.0.0.14. Exit status: 134. Diagnostics: Exception from container-launch.
    Container id: container_1485916338528_0008_05_000005
    Exit code: 134
    Exception message: /bin/bash: line 1: 12230 Aborted                 (core dumped) LD_LIBRARY_PATH=/usr/hdp/current/hadoop-client/lib/native:/usr/hdp/current/hadoop-client/lib/native/Linux-amd64-64:/home/xiaoyzhu/CaffeOnSpark/caffe-public/distribute/lib:/home/xiaoyzhu/CaffeOnSpark/caffe-distri/distribute/lib /usr/lib/jvm/java-8-openjdk-amd64/bin/java -server -Xmx4608m '-Dhdp.version=' '-Detwlogger.component=sparkexecutor' '-DlogFilter.filename=SparkLogFilters.xml' '-DpatternGroup.filename=SparkPatternGroups.xml' '-Dlog4jspark.root.logger=INFO,console,RFA,ETW,Anonymizer' '-Dlog4jspark.log.dir=/var/log/sparkapp/${user.name}' '-Dlog4jspark.log.file=sparkexecutor.log' '-Dlog4j.configuration=file:/usr/hdp/current/spark2-client/conf/log4j.properties' '-Djavax.xml.parsers.SAXParserFactory=com.sun.org.apache.xerces.internal.jaxp.SAXParserFactoryImpl' -Djava.io.tmpdir=/mnt/resource/hadoop/yarn/local/usercache/xiaoyzhu/appcache/application_1485916338528_0008/container_1485916338528_0008_05_000005/tmp '-Dspark.driver.port=43942' '-Dspark.history.ui.port=18080' '-Dspark.ui.port=0' -Dspark.yarn.app.container.log.dir=/mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005 -XX:OnOutOfMemoryError='kill %p' org.apache.spark.executor.CoarseGrainedExecutorBackend --driver-url spark://CoarseGrainedScheduler@10.0.0.13:43942 --executor-id 4 --hostname 10.0.0.14 --cores 3 --app-id application_1485916338528_0008 --user-class-path file:/mnt/resource/hadoop/yarn/local/usercache/xiaoyzhu/appcache/application_1485916338528_0008/container_1485916338528_0008_05_000005/__app__.jar > /mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005/stdout 2> /mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005/stderr

    Stack trace: ExitCodeException exitCode=134: /bin/bash: line 1: 12230 Aborted                 (core dumped) LD_LIBRARY_PATH=/usr/hdp/current/hadoop-client/lib/native:/usr/hdp/current/hadoop-client/lib/native/Linux-amd64-64:/home/xiaoyzhu/CaffeOnSpark/caffe-public/distribute/lib:/home/xiaoyzhu/CaffeOnSpark/caffe-distri/distribute/lib /usr/lib/jvm/java-8-openjdk-amd64/bin/java -server -Xmx4608m '-Dhdp.version=' '-Detwlogger.component=sparkexecutor' '-DlogFilter.filename=SparkLogFilters.xml' '-DpatternGroup.filename=SparkPatternGroups.xml' '-Dlog4jspark.root.logger=INFO,console,RFA,ETW,Anonymizer' '-Dlog4jspark.log.dir=/var/log/sparkapp/${user.name}' '-Dlog4jspark.log.file=sparkexecutor.log' '-Dlog4j.configuration=file:/usr/hdp/current/spark2-client/conf/log4j.properties' '-Djavax.xml.parsers.SAXParserFactory=com.sun.org.apache.xerces.internal.jaxp.SAXParserFactoryImpl' -Djava.io.tmpdir=/mnt/resource/hadoop/yarn/local/usercache/xiaoyzhu/appcache/application_1485916338528_0008/container_1485916338528_0008_05_000005/tmp '-Dspark.driver.port=43942' '-Dspark.history.ui.port=18080' '-Dspark.ui.port=0' -Dspark.yarn.app.container.log.dir=/mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005 -XX:OnOutOfMemoryError='kill %p' org.apache.spark.executor.CoarseGrainedExecutorBackend --driver-url spark://CoarseGrainedScheduler@10.0.0.13:43942 --executor-id 4 --hostname 10.0.0.14 --cores 3 --app-id application_1485916338528_0008 --user-class-path file:/mnt/resource/hadoop/yarn/local/usercache/xiaoyzhu/appcache/application_1485916338528_0008/container_1485916338528_0008_05_000005/__app__.jar > /mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005/stdout 2> /mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005/stderr

        at org.apache.hadoop.util.Shell.runCommand(Shell.java:933)
        at org.apache.hadoop.util.Shell.run(Shell.java:844)
        at org.apache.hadoop.util.Shell$ShellCommandExecutor.execute(Shell.java:1123)
        at org.apache.hadoop.yarn.server.nodemanager.DefaultContainerExecutor.launchContainer(DefaultContainerExecutor.java:225)
        at org.apache.hadoop.yarn.server.nodemanager.containermanager.launcher.ContainerLaunch.call(ContainerLaunch.java:317)
        at org.apache.hadoop.yarn.server.nodemanager.containermanager.launcher.ContainerLaunch.call(ContainerLaunch.java:83)
        at java.util.concurrent.FutureTask.run(FutureTask.java:266)
        at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1142)
        at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:617)
        at java.lang.Thread.run(Thread.java:745)


    Container exited with a non-zero exit code 134

<span data-ttu-id="39df9-209">W takim przypadku należy tooget hello nie powiodło się w kontenerze o identyfikatorze (w hello powyżej case, jest container_1485916338528_0008_05_000005).</span><span class="sxs-lookup"><span data-stu-id="39df9-209">In this case, you need tooget hello failed container ID (in hello above case, it is container_1485916338528_0008_05_000005).</span></span> <span data-ttu-id="39df9-210">Następnie należy toorun</span><span class="sxs-lookup"><span data-stu-id="39df9-210">Then you need toorun</span></span> 

    yarn logs -containerId container_1485916338528_0008_03_000005

<span data-ttu-id="39df9-211">z hello headnode.</span><span class="sxs-lookup"><span data-stu-id="39df9-211">from hello headnode.</span></span> <span data-ttu-id="39df9-212">Po sprawdzeniu kontenera awarii, jest on spowodował przy użyciu trybu procesora GPU (gdzie należy używać trybu Procesora zamiast) w lenet_memory_solver.prototxt.</span><span class="sxs-lookup"><span data-stu-id="39df9-212">After checking container failure, it is caused by using GPU mode (where you should use CPU mode instead) in lenet_memory_solver.prototxt.</span></span>

    17/02/01 07:10:48 INFO LMDB: Batch size:100
    WARNING: Logging before InitGoogleLogging() is written tooSTDERR
    F0201 07:10:48.309725 11624 common.cpp:79] Cannot use GPU in CPU-only Caffe: check mode.


## <a name="getting-results"></a><span data-ttu-id="39df9-213">Uzyskiwanie wyników</span><span class="sxs-lookup"><span data-stu-id="39df9-213">Getting results</span></span>

<span data-ttu-id="39df9-214">Ponieważ firma Microsoft jest alokowany 8 modułów i topologii sieci hello jest proste, trwa tylko około 30 minut toorun hello wynik.</span><span class="sxs-lookup"><span data-stu-id="39df9-214">Since we are allocating 8 executors, and hello network topology is simple, it should only take around 30 minutes toorun hello result.</span></span> <span data-ttu-id="39df9-215">Z wiersza polecenia hello, widać, że firma Microsoft umieścić hello toowasb:///mnist.model modelu, a folder tooa wyniki hello o nazwie wasb: / / / mnist_features_result.</span><span class="sxs-lookup"><span data-stu-id="39df9-215">From hello command line, you can see that we put hello model toowasb:///mnist.model, and put hello results tooa folder named wasb:///mnist_features_result.</span></span>

<span data-ttu-id="39df9-216">Aby uzyskać wyniki hello uruchamiając</span><span class="sxs-lookup"><span data-stu-id="39df9-216">You can get hello results by running</span></span>

    hadoop fs -cat hdfs:///mnist_features_result/*

<span data-ttu-id="39df9-217">i wynik hello wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="39df9-217">and hello result looks like:</span></span>

    {"SampleID":"00009597","accuracy":[1.0],"loss":[0.028171852],"label":[2.0]}
    {"SampleID":"00009598","accuracy":[1.0],"loss":[0.028171852],"label":[6.0]}
    {"SampleID":"00009599","accuracy":[1.0],"loss":[0.028171852],"label":[1.0]}
    {"SampleID":"00009600","accuracy":[0.97],"loss":[0.0677709],"label":[5.0]}
    {"SampleID":"00009601","accuracy":[0.97],"loss":[0.0677709],"label":[0.0]}
    {"SampleID":"00009602","accuracy":[0.97],"loss":[0.0677709],"label":[1.0]}
    {"SampleID":"00009603","accuracy":[0.97],"loss":[0.0677709],"label":[2.0]}
    {"SampleID":"00009604","accuracy":[0.97],"loss":[0.0677709],"label":[3.0]}
    {"SampleID":"00009605","accuracy":[0.97],"loss":[0.0677709],"label":[4.0]}

<span data-ttu-id="39df9-218">Hello SampleID reprezentuje identyfikator hello w zestawie danych MNIST hello i etykiety hello jest identyfikuje numer hello hello modelu.</span><span class="sxs-lookup"><span data-stu-id="39df9-218">hello SampleID represents hello ID in hello MNIST dataset, and hello label is hello number that hello model identifies.</span></span>


## <a name="conclusion"></a><span data-ttu-id="39df9-219">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="39df9-219">Conclusion</span></span>

<span data-ttu-id="39df9-220">W tej dokumentacji nastąpiła tooinstall CaffeOnSpark z systemem prosty przykład.</span><span class="sxs-lookup"><span data-stu-id="39df9-220">In this documentation, you have tried tooinstall CaffeOnSpark with running a simple example.</span></span> <span data-ttu-id="39df9-221">HDInsight to platforma obliczeń rozproszonej pełne zarządzanej chmury i jest hello najlepsze miejsce do uruchamiania uczenia maszynowego i obciążeń zaawansowana analityka w dużych zestawów danych i rozproszonych głębokie szkoleniowe, możesz użyć Caffe w learning głębokie tooperform Spark w usłudze HDInsight zadania.</span><span class="sxs-lookup"><span data-stu-id="39df9-221">HDInsight is a full managed cloud distributed compute platform, and is hello best place for running machine learning and advanced analytics workloads on large data set, and for distributed deep learning, you can use Caffe on HDInsight Spark tooperform deep learning tasks.</span></span>


## <span data-ttu-id="39df9-222"><a name="seealso"></a>Zobacz też</span><span class="sxs-lookup"><span data-stu-id="39df9-222"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="39df9-223">Przegląd: platforma Apache Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="39df9-223">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="39df9-224">Scenariusze</span><span class="sxs-lookup"><span data-stu-id="39df9-224">Scenarios</span></span>
* [<span data-ttu-id="39df9-225">Platforma Spark i usługa Machine Learning: korzystanie z platformy Spark w usłudze HDInsight do analizy temperatury w budynku z użyciem danych HVAC</span><span class="sxs-lookup"><span data-stu-id="39df9-225">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="39df9-226">Platforma Spark przy użyciu Machine Learning: Korzystanie z platformy Spark w wyników inspekcji żywności toopredict HDInsight</span><span class="sxs-lookup"><span data-stu-id="39df9-226">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)

### <a name="manage-resources"></a><span data-ttu-id="39df9-227">Zarządzanie zasobami</span><span class="sxs-lookup"><span data-stu-id="39df9-227">Manage resources</span></span>
* [<span data-ttu-id="39df9-228">Zarządzanie zasobami hello klastra Apache Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="39df9-228">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)

