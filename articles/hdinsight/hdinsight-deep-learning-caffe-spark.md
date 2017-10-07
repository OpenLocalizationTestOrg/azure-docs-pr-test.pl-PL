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
# <a name="use-caffe-on-azure-hdinsight-spark-for-distributed-deep-learning"></a>Użyj Caffe Azure HDInsight Spark dla rozproszonych learning bezpośrednich


## <a name="introduction"></a>Wprowadzenie

Głębokie learning jest wpływające na od toomanufacturing tootransportation opieki zdrowotnej i inne. Firm są Włączanie toodeep learning toosolve twardych problemów, takich jak [obrazu klasyfikacji](http://blogs.microsoft.com/next/2015/12/10/microsoft-researchers-win-imagenet-computer-vision-challenge/), [rozpoznawania mowy](http://googleresearch.blogspot.jp/2015/08/the-neural-networks-behind-google-voice.html)obiekt rozpoznawania i komputera tłumaczenia. 

Brak [wielu popularnych środowisk](https://en.wikipedia.org/wiki/Comparison_of_deep_learning_software), takie jak [kognitywnych zestaw narzędzi firmy Microsoft](https://www.microsoft.com/en-us/research/product/cognitive-toolkit/), [Tensorflow](https://www.tensorflow.org/), MXNet, Theano, itp. Caffe jest jednym z hello Najpopularniejsza struktur-symboliczne sieci neuronowej (nadrzędnych), a powszechnie używany w wielu obszarach, w tym komputerze wizji. Ponadto [CaffeOnSpark](http://yahoohadoop.tumblr.com/post/139916563586/caffeonspark-open-sourced-for-distributed-deep) łączy Caffe z platformy Apache Spark w takim przypadku głębokość uczenia, które mogą być łatwo używane na platformie Hadoop, istniejącego klastra wraz z potoków Spark ETL zmniejszenie złożoności systemu i czas oczekiwania na learning end-to-end.

[HDInsight](https://azure.microsoft.com/en-us/services/hdinsight/) jest hello tylko klastry analityczne typu open source w pełni zarządzaną chmury Hadoop oferty, który zapewnia zoptymalizowane pod kątem Spark, Hive, MapReduce, HBase, Storm, Kafka i R Server obsługiwana przez SLA 99,9%. Każda z tych technologii danych big data i aplikacji ISV jest łatwa do wdrożenia w formie zarządzanych klastrów z bezpieczeństwem i monitorowaniem klasy korporacyjnej.

W przypadku niektórych użytkowników prośbę o nas o tym, jak toouse głębokie uczenia w usłudze HDInsight, czyli produktu PaaS Hadoop firmy Microsoft. Firma Microsoft będzie mieć więcej tooshare w przyszłości hello, ale obecnie chcemy toosummarize techniczne blog na temat toouse Caffe na HDInsight Spark.

Po zainstalowaniu Caffe przed można zauważyć, że instalacja ta struktura jest nieco trudne. W tym wpisie możemy najpierw przedstawiają sposób tooinstall [Caffe na Spark](https://github.com/yahoo/CaffeOnSpark) dla klastra usługi HDInsight, następnie użyć hello wbudowanych MNIST pokaz toodemostrate jak toouse Learning głębokie rozproszonego przy użyciu HDInsight Spark na procesorach.

Istnieją cztery główne kroki tooget, działa on w usłudze HDInsight.

1. Zainstaluj zależności hello wymagane we wszystkich węzłach hello
2. Tworzenie Caffe na Spark dla usługi HDInsight na powitania węzła głównego
3. Dystrybuuj węzłów procesu roboczego hello hello wymaganych bibliotek tooall
4. Napisz modelu Caffe, a następnie uruchom go distributely

Ponieważ HDInsight to rozwiązanie typu PaaS, oferuje funkcje platformy dużą — tak jest dość łatwe tooperform niektórych zadań. Nosi nazwę jednej z funkcji hello, które firma Microsoft intensywnie korzystają w tym wpisie w blogu [akcji skryptu](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux), z którego można wykonywać powłoki poleceń toocustomize węzłów klastra (węzła głównego węzła procesu roboczego i węzłem krawędzi).

## <a name="step-1--install-hello-required-dependencies-on-all-hello-nodes"></a>Krok 1: Instalowanie zależności hello wymagane we wszystkich węzłach hello

Rozpoczęto tooget, potrzebujemy tooinstall hello zależności, które należy. Hello Caffe lokacji i [lokacji CaffeOnSpark](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn) oferuje niektóre przydatne wiki do instalowania zależności hello platformy Spark w trybie YARN (który jest trybem hello Spark w usłudze HDInsight), ale potrzebujemy tooadd kilka zależności więcej HDInsight platformy. Firma Microsoft będzie użyć akcji skryptu hello zgodnie z poniższymi instrukcjami i uruchom go na wszystkich węzłach głównych hello i węzłów procesu roboczego. Ta akcja skryptu potrwa około 20 minut, jak te zależności również są zależne od innych pakietów. Należy umieścić go w niektórych lokalizacji, która jest dostępna tooyour klastra usługi HDInsight, takie jak lokalizacja GitHub lub hello domyślne konto magazynu obiektów BLOB.

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


Istnieją dwa kroki w akcji skryptu hello powyżej. pierwszym krokiem Hello jest tooinstall hello wszystkich wymaganych bibliotek. Te biblioteki zawierają hello wymagane biblioteki dla kompilacji Caffe (na przykład gflags, glog) i systemem Caffe (na przykład numpy). Używamy libatlas optymalizacji Procesora, ale zawsze można wykonać hello CaffeOnSpark wiki na temat instalowania innych bibliotek optymalizacji, takie jak MKL lub CUDA (dla procesora GPU).

drugim krokiem Hello jest toodownload, skompilować i zainstalować protobuf 2.5.0 dla Caffe w czasie wykonywania. Protobuf 2.5.0 [wymagana jest](https://github.com/yahoo/CaffeOnSpark/issues/87), ale ta wersja nie jest dostępny jako pakiet na Ubuntu 16, więc musimy toocompile z hello kodu źródłowego. Dostępne są również kilka zasoby na powitania internetowe na temat toocompile, takich jak [to](http://jugnu-life.blogspot.com/2013/09/install-protobuf-25-on-ubuntu.html)

toosimply rozpocząć pracę, możesz tylko uruchamiać tę akcję skryptu na proces roboczy z klastra tooall hello węzły węzłów i head (dla usługi HDInsight 3.5). Można uruchomić akcji skryptu hello uruchomionych klastra lub hello akcji skryptu można również uruchomić w czasie udostępniania klastra hello. Więcej szczegółów na powitania akcji skryptu, można znaleźć w dokumentacji hello [tutaj](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux#view-history-promote-and-demote-script-actions)

![TooInstall akcji skryptu zależności](./media/hdinsight-deep-learning-caffe-spark/Script-Action-1.png)


## <a name="step-2-build-caffe-on-spark-for-hdinsight-on-hello-head-node"></a>Krok 2: Tworzenie Caffe Spark dla usługi HDInsight na powitania węzła głównego

drugi etap Hello jest toobuild Caffe na powitania headnode, a następnie dystrybucję węzłów procesu roboczego hello tooall bibliotek hello skompilowany. W tym kroku należy zbyt[ssh do Twojej headnode](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix), po prostu wykonaj hello [proces kompilacji CaffeOnSpark](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn), i poniżej znajduje się skrypt hello za pomocą toobuild CaffeOnSpark kilka dodatkowych czynności. 

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

Może być konieczne toodo więcej niż mówi jakie dokumentacji hello CaffeOnSpark. zmiany Hello są następujące:
- Zmień tylko tooCPU i użyj libatlas w tym konkretnym celu.
- Umieść hello zestawów danych toohello magazynu obiektów BLOB, który prowadzi do lokalizacji udostępnionej, który jest dostępny tooall węzłów procesu roboczego do późniejszego użycia.
- Umieść hello skompilowany Caffe biblioteki tooBLOB magazynu i później skopiuje tych węzłów hello tooall biblioteki za pomocą akcji skryptów w czasie kompilacji dodatkowe tooavoid.


### <a name="troubleshooting-an-ant-buildexception-has-occured-exec-returned-2"></a>Rozwiązywanie problemów: Wystąpił BuildException Ant: exec zwrócił: 2

Podczas próby najpierw toobuild CaffeOnSpark, czasami jest wyświetlany tekst

    failed tooexecute goal org.apache.maven.plugins:maven-antrun-plugin:1.7:run (proto) on project caffe-distri: An Ant BuildException has occured: exec returned: 2

Po prostu czystą hello repozytorium kodu przez "Sprawdź czystą", a następnie wykonywania "Sprawdź kompilacji" rozwiąże ten problem, tak długo, jak długo mają hello prawidłowymi zależnościami.

### <a name="troubleshooting-maven-repository-connection-time-out"></a>Rozwiązywanie problemów: Limit czasu połączenia repozytorium Maven

Czasami maven zapewnia dużą elastyczność błąd przekroczenia limitu czasu połączenia hello, podobne toobelow:

    Retry:
    [INFO] Downloading: https://repo.maven.apache.org/maven2/com/twitter/chill_2.11/0.8.0/chill_2.11-0.8.0.jar
    Feb 01, 2017 5:14:49 AM org.apache.maven.wagon.providers.http.httpclient.impl.execchain.RetryExec execute
    INFO: I/O exception (java.net.SocketException) caught when processing request too{s}->https://repo.maven.apache.org:443: Connection timed out (Read failed)

Zostanie ono OK po odczekaniu za kilka minut i spróbuj właśnie toorebuild hello kodu, więc może być Maven jakiś sposób limity hello ruch z danego adresu IP.


### <a name="troubleshooting-test-failure-for-caffe"></a>Rozwiązywanie problemów: Błąd testowego dla Caffe

Prawdopodobnie zobaczysz niepowodzenia testu podczas wykonywania hello końcowego sprawdzaj CaffeOnSpark podobne z poniżej. Jest to prabably związanych z kodowaniem UTF-8, ale powinien mieć wpływu na użycie hello Caffe

    Run completed in 32 seconds, 78 milliseconds.
    Total number of tests run: 7
    Suites: completed 5, aborted 0
    Tests: succeeded 6, failed 1, canceled 0, ignored 0, pending 0
    *** 1 TEST FAILED ***

## <a name="step-3-distribute-hello-required-libraries-tooall-hello-worker-nodes"></a>Krok 3: Dystrybucji węzłów procesu roboczego hello hello wymaganych bibliotek tooall

Hello następnym krokiem jest toodistribute hello bibliotek (zasadniczo hello bibliotek CaffeOnSpark/caffe publicznego/dystrybucji/lib/i CaffeOnSpark/caffe dystry/dystrybucji/lib /) węzły hello tooall. W kroku 2 testujemy tych bibliotek w magazynie obiektów BLOB, a w tym kroku zostanie wykorzystany toocopy akcji skryptu go tooall hello węzłów głównych i węzłów procesu roboczego.

toodo, prosty, Uruchom akcję skryptu zgodnie z poniższymi instrukcjami (należy toopoint toohello odpowiedniej lokalizacji tooyour określonego klastra):

    #!/bin/bash
    hadoop fs -get wasb:///CaffeOnSpark /home/changetoyourusername/

Ponieważ w kroku 2, testujemy go na powitania magazynu obiektów BLOB, który jest dostępny tooall hello węzły, w tym kroku będziemy wystarczy po prostu skopiuj go tooall hello węzłów.

## <a name="step-4-compose-a-caffe-model-and-run-it-distributely"></a>Krok 4: Utworzenie modelu Caffe i uruchom go distributely

Po uruchomieniu hello powyżej kroki, Caffe jest już zainstalowana na powitania headnode i nie jesteśmy toogo dobra. Witaj następnym krokiem jest toowrite Caffe modelu. 

Caffe używa "Architektura obszerne", gdy do tworzenia modelu, należy po prostu muszą toodefine plik konfiguracji i bez kodowania w ogóle (w większości przypadków). Dlatego Spójrzmy istnieje. 

Firma Microsoft będzie dzisiaj uczenia modelu Hello to model próbki szkolenia MNIST. bazy danych MNIST Hello odręcznie cyfr ma zestaw szkolenia 60 000 przykłady i zbiór przykłady 10 000. Jest ona podzbiorem większy zestaw dostępnej w sklepie NIST. Witaj cyfr zostały znormalizowany rozmiar i wyśrodkowany w obrazie stałym rozmiarze. CaffeOnSpark ma niektóre skrypty toodownload hello dataset i przekształcić ją w prawidłowym formacie hello.

CaffeOnSpark zawiera przykładowe topologie sieci MNIST szkolenia. Ma ona nieuprzywilejowany projektowania podziału architektury sieci hello (hello topologii sieci hello) i optymalizacji. W takim przypadku istnieją dwa pliki wymagane: 

Witaj "Solver" (${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt) jest używany plik nadzorowaniu hello optymalizacji i generowania parametru aktualizacji. Na przykład, określa czy procesora CPU, czy procesor GPU będą używane, co to jest pęd hello, będzie jak dużo iteracji, itp. Definiuje również, które neuronu topologii sieci należy hello program wykorzystania (hello drugi plik potrzebne). Aby uzyskać więcej informacji na temat Solver można znaleźć zbyt[dokumentacji Caffe](http://caffe.berkeleyvision.org/tutorial/solver.html).

Na przykład ponieważ używamy Procesora niż procesora GPU, możemy należy zmienić hello ostatni wiersz, aby:

    # solver mode: CPU or GPU
    solver_mode: CPU

![Caffe konfiguracji](./media/hdinsight-deep-learning-caffe-spark/Caffe-1.png)

W razie potrzeby można zmienić innych wierszy.

drugi plik Hello (${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt) definiuje sposób sieci neuronu hello wygląda i hello odpowiednie dane wejściowe i pliku wyjściowego. Należy również lokalizacja danych szkoleniowych hello tooreflect tooupdate hello pliku. Zmień hello następujące części w lenet_memory_train_test.prototxt (należy toopoint toohello odpowiedniej lokalizacji tooyour określonego klastra):

- Zmień hello "file:/Users/mridul/bigml/demodl/mnist_train_lmdb" za "wasb: / / / projektów/machine_learning/image_dataset/mnist_train_lmdb"
- Zmień "file:/Users/mridul/bigml/demodl/mnist_test_lmdb/" za "wasb: / / / projektów/machine_learning/image_dataset/mnist_test_lmdb"

![Caffe konfiguracji](./media/hdinsight-deep-learning-caffe-spark/Caffe-2.png)

Aby uzyskać więcej informacji dotyczących sposobu toodefine hello sieci, sprawdź hello [Caffe dokumentacja MNIST zestawu danych](http://caffe.berkeleyvision.org/gathered/examples/mnist.html)

W celu hello ten blog używamy są po prostu to prosty przykład MNIST. Poniższe polecenie hello uruchamiać z węzłem głównym hello:

    spark-submit --master yarn --deploy-mode cluster --num-executors 8 --files ${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt,${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt --conf spark.driver.extraLibraryPath="${LD_LIBRARY_PATH}" --conf spark.executorEnv.LD_LIBRARY_PATH="${LD_LIBRARY_PATH}" --class com.yahoo.ml.caffe.CaffeOnSpark ${CAFFE_ON_SPARK}/caffe-grid/target/caffe-grid-0.1-SNAPSHOT-jar-with-dependencies.jar -train -features accuracy,loss -label label -conf lenet_memory_solver.prototxt -devices 1 -connection ethernet -model wasb:///mnist.model -output wasb:///mnist_features_result

Zasadniczo rozpowszechnia hello wymagane pliki przędza kontenera tooeach (lenet_memory_solver.prototxt i lenet_memory_train_test.prototxt), a także ustawić hello odpowiednich ŚCIEŻKĘ każdego tooLD_LIBRARY_PATH sterownik/Moduł wykonujący Spark, który jest zdefiniowany w hello poprzednie kodu fragment kodu i punktów toohello lokalizacji, która ma CaffeOnSpark biblioteki. 

## <a name="monitoring-and-troubleshooting"></a>Monitorowanie i rozwiązywanie problemów

Ponieważ używamy YARN tryb klastra, w tym przypadku sterownik Spark hello będzie zaplanowane tooan dowolnego kontenera (i węzła procesu roboczego dowolnego) powinien widoczne są tylko w konsoli hello Generowanie coś, takich jak:

    17/02/01 23:22:16 INFO Client: Application report for application_1485916338528_0015 (state: RUNNING)

Jeśli chcesz tooknow, co się stało, należy zwykle sterownika tooget hello Spark dziennika, który zawiera więcej informacji. W takim przypadku należy toogo toohello interfejsie użytkownika YARN toofind hello odpowiednich dzienniki YARN. Możesz uzyskać hello interfejsie użytkownika YARN przez ten adres URL: 

    https://yourclustername.azurehdinsight.net/yarnui
   
![YARN INTERFEJSU UŻYTKOWNIKA](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-1.png)

Użytkownik może Spójrz na ile zasoby są przydzielane dla konkretnej aplikacji. Możesz kliknąć łącze "Harmonogramu" hello, a zostanie wyświetlona dla tej aplikacji, czy 9 kontenery uruchomiona. Prosimy YARN tooprovide 8 modułów, a innego kontenera jest procesu sterownika. 

![YARN harmonogramu](./media/hdinsight-deep-learning-caffe-spark/YARN-Scheduler.png)

Jeśli występują błędy może być toocheck hello sterownik dzienników lub dzienniki kontenera. W przypadku dzienników sterownika można kliknij Identyfikatora aplikacji hello w interfejsie użytkownika YARN, następnie kliknij przycisk "Dzienniki" hello. Dzienniki sterownik Hello są zapisywane do strumienia wyjściowego stderr.

![INTERFEJS UŻYTKOWNIKA YARN 2](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-2.png)

Na przykład można napotkać niektóre błąd hello poniżej z dzienników sterownik hello, wskazujący, że przydzielenie zbyt wiele modułów.

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

Czasami hello problem może się zdarzyć w modułów zamiast sterowniki. W takim przypadku należy toocheck hello kontenera dzienników. Zawsze uzyskać hello kontenera dzienniki i następnie Uzyskaj hello kontenera nie powiodło się. Na przykład ten błąd może spełniać podczas uruchamiania Caffe.

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

W takim przypadku należy tooget hello nie powiodło się w kontenerze o identyfikatorze (w hello powyżej case, jest container_1485916338528_0008_05_000005). Następnie należy toorun 

    yarn logs -containerId container_1485916338528_0008_03_000005

z hello headnode. Po sprawdzeniu kontenera awarii, jest on spowodował przy użyciu trybu procesora GPU (gdzie należy używać trybu Procesora zamiast) w lenet_memory_solver.prototxt.

    17/02/01 07:10:48 INFO LMDB: Batch size:100
    WARNING: Logging before InitGoogleLogging() is written tooSTDERR
    F0201 07:10:48.309725 11624 common.cpp:79] Cannot use GPU in CPU-only Caffe: check mode.


## <a name="getting-results"></a>Uzyskiwanie wyników

Ponieważ firma Microsoft jest alokowany 8 modułów i topologii sieci hello jest proste, trwa tylko około 30 minut toorun hello wynik. Z wiersza polecenia hello, widać, że firma Microsoft umieścić hello toowasb:///mnist.model modelu, a folder tooa wyniki hello o nazwie wasb: / / / mnist_features_result.

Aby uzyskać wyniki hello uruchamiając

    hadoop fs -cat hdfs:///mnist_features_result/*

i wynik hello wygląda następująco:

    {"SampleID":"00009597","accuracy":[1.0],"loss":[0.028171852],"label":[2.0]}
    {"SampleID":"00009598","accuracy":[1.0],"loss":[0.028171852],"label":[6.0]}
    {"SampleID":"00009599","accuracy":[1.0],"loss":[0.028171852],"label":[1.0]}
    {"SampleID":"00009600","accuracy":[0.97],"loss":[0.0677709],"label":[5.0]}
    {"SampleID":"00009601","accuracy":[0.97],"loss":[0.0677709],"label":[0.0]}
    {"SampleID":"00009602","accuracy":[0.97],"loss":[0.0677709],"label":[1.0]}
    {"SampleID":"00009603","accuracy":[0.97],"loss":[0.0677709],"label":[2.0]}
    {"SampleID":"00009604","accuracy":[0.97],"loss":[0.0677709],"label":[3.0]}
    {"SampleID":"00009605","accuracy":[0.97],"loss":[0.0677709],"label":[4.0]}

Hello SampleID reprezentuje identyfikator hello w zestawie danych MNIST hello i etykiety hello jest identyfikuje numer hello hello modelu.


## <a name="conclusion"></a>Podsumowanie

W tej dokumentacji nastąpiła tooinstall CaffeOnSpark z systemem prosty przykład. HDInsight to platforma obliczeń rozproszonej pełne zarządzanej chmury i jest hello najlepsze miejsce do uruchamiania uczenia maszynowego i obciążeń zaawansowana analityka w dużych zestawów danych i rozproszonych głębokie szkoleniowe, możesz użyć Caffe w learning głębokie tooperform Spark w usłudze HDInsight zadania.


## <a name="seealso"></a>Zobacz też
* [Przegląd: platforma Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Scenariusze
* [Platforma Spark i usługa Machine Learning: korzystanie z platformy Spark w usłudze HDInsight do analizy temperatury w budynku z użyciem danych HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Platforma Spark przy użyciu Machine Learning: Korzystanie z platformy Spark w wyników inspekcji żywności toopredict HDInsight](hdinsight-apache-spark-machine-learning-mllib-ipython.md)

### <a name="manage-resources"></a>Zarządzanie zasobami
* [Zarządzanie zasobami hello klastra Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-resource-manager.md)

