---
title: "zrzuty stosu aaaEnable usługi Hadoop w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Włącz zrzuty stosu dla usług Hadoop z klastrów usługi HDInsight opartych na systemie Linux debugowania i analizy."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8f151adb-f687-41e4-aca0-82b551953725
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 49e30f26e1a83f19e068e9da253b5548caec70d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-heap-dumps-for-hadoop-services-on-linux-based-hdinsight"></a><span data-ttu-id="42661-103">Włącz zrzuty stosu dla usługi Hadoop w HDInsight opartych na systemie Linux</span><span class="sxs-lookup"><span data-stu-id="42661-103">Enable heap dumps for Hadoop services on Linux-based HDInsight</span></span>

[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

<span data-ttu-id="42661-104">Zrzuty stosu zawierającego migawkę pamięci aplikacji hello, w tym hello wartości zmiennych w czasie hello zrzutu hello został utworzony.</span><span class="sxs-lookup"><span data-stu-id="42661-104">Heap dumps contain a snapshot of hello application's memory, including hello values of variables at hello time hello dump was created.</span></span> <span data-ttu-id="42661-105">Tak, aby były przydatne do diagnozowania problemów występujących w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="42661-105">So they are useful for diagnosing problems that occur at run-time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="42661-106">Hello kroki opisane w tym dokumencie pracować tylko z klastrami usługi HDInsight, które używają systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="42661-106">hello steps in this document only work with HDInsight clusters that use Linux.</span></span> <span data-ttu-id="42661-107">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="42661-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="42661-108">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="42661-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="42661-109"><a name="whichServices"></a>Usługi</span><span class="sxs-lookup"><span data-stu-id="42661-109"><a name="whichServices"></a>Services</span></span>

<span data-ttu-id="42661-110">Można włączyć zrzuty stosu dla hello następujące usługi:</span><span class="sxs-lookup"><span data-stu-id="42661-110">You can enable heap dumps for hello following services:</span></span>

* <span data-ttu-id="42661-111">**hcatalog** -tempelton</span><span class="sxs-lookup"><span data-stu-id="42661-111">**hcatalog** - tempelton</span></span>
* <span data-ttu-id="42661-112">**gałąź** -serwera hiveserver2, potrzeby magazynu metadanych, derbyserver</span><span class="sxs-lookup"><span data-stu-id="42661-112">**hive** - hiveserver2, metastore, derbyserver</span></span>
* <span data-ttu-id="42661-113">**mapreduce** -jobhistoryserver</span><span class="sxs-lookup"><span data-stu-id="42661-113">**mapreduce** - jobhistoryserver</span></span>
* <span data-ttu-id="42661-114">**yarn** -resourcemanager nodemanager, timelineserver</span><span class="sxs-lookup"><span data-stu-id="42661-114">**yarn** - resourcemanager, nodemanager, timelineserver</span></span>
* <span data-ttu-id="42661-115">**System plików hdfs** -datanode secondarynamenode, namenode</span><span class="sxs-lookup"><span data-stu-id="42661-115">**hdfs** - datanode, secondarynamenode, namenode</span></span>

<span data-ttu-id="42661-116">Można także włączyć zrzuty stosu mapę hello i zmniejszyć procesów uruchomionych przez usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="42661-116">You can also enable heap dumps for hello map and reduce processes ran by HDInsight.</span></span>

## <span data-ttu-id="42661-117"><a name="configuration"></a>Opis sterty zrzutu konfiguracji</span><span class="sxs-lookup"><span data-stu-id="42661-117"><a name="configuration"></a>Understanding heap dump configuration</span></span>

<span data-ttu-id="42661-118">Zrzuty stosu są włączane przez przeniesienie opcji (czasami znana jako zdecyduje, lub parametry) toohello JVM podczas uruchamiania usługi.</span><span class="sxs-lookup"><span data-stu-id="42661-118">Heap dumps are enabled by passing options (sometimes known as opts, or parameters) toohello JVM when a service is started.</span></span> <span data-ttu-id="42661-119">Dla większości usług Hadoop można zmodyfikować hello powłoki skryptu używanego toostart hello usługi toopass tych opcji.</span><span class="sxs-lookup"><span data-stu-id="42661-119">For most Hadoop services, you can modify hello shell script used toostart hello service toopass these options.</span></span>

<span data-ttu-id="42661-120">Każdy skrypt ma Eksport  **\* \_OPTS**, który zawiera opcje hello przekazany toohello maszyny JVM.</span><span class="sxs-lookup"><span data-stu-id="42661-120">In each script, there is an export for **\*\_OPTS**, which contains hello options passed toohello JVM.</span></span> <span data-ttu-id="42661-121">Na przykład w hello **hadoop env.sh** skryptu hello wiersza, który rozpoczyna się od `export HADOOP_NAMENODE_OPTS=` zawiera opcje hello hello NameNode usługi.</span><span class="sxs-lookup"><span data-stu-id="42661-121">For example, in hello **hadoop-env.sh** script, hello line that begins with `export HADOOP_NAMENODE_OPTS=` contains hello options for hello NameNode service.</span></span>

<span data-ttu-id="42661-122">Mapowanie i zmniejszenie procesy są nieco inne operacje te są Proces podrzędny programu hello usługi MapReduce.</span><span class="sxs-lookup"><span data-stu-id="42661-122">Map and reduce processes are slightly different, as these operations are a child process of hello MapReduce service.</span></span> <span data-ttu-id="42661-123">Każdy mapy lub Zmniejsz proces jest uruchomiony w kontenerze, a dwa wpisy zawierające hello JVM opcje.</span><span class="sxs-lookup"><span data-stu-id="42661-123">Each map or reduce process runs in a child container, and there are two entries that contain hello JVM options.</span></span> <span data-ttu-id="42661-124">Zarówno zawarte w **mapred-site.xml**:</span><span class="sxs-lookup"><span data-stu-id="42661-124">Both contained in **mapred-site.xml**:</span></span>

* <span data-ttu-id="42661-125">**mapreduce.Admin.map.child.Java.opts**</span><span class="sxs-lookup"><span data-stu-id="42661-125">**mapreduce.admin.map.child.java.opts**</span></span>
* <span data-ttu-id="42661-126">**mapreduce.Admin.Reduce.child.Java.opts**</span><span class="sxs-lookup"><span data-stu-id="42661-126">**mapreduce.admin.reduce.child.java.opts**</span></span>

> [!NOTE]
> <span data-ttu-id="42661-127">Zaleca się przy użyciu Ambari toomodify zarówno hello skryptów i ustawienia mapred-site.xml jako Ambari obsługi replikacji zmian w węzłach w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="42661-127">We recommend using Ambari toomodify both hello scripts and mapred-site.xml settings, as Ambari handle replicating changes across nodes in hello cluster.</span></span> <span data-ttu-id="42661-128">Zobacz hello [przy użyciu Ambari](#using-ambari) sekcji, aby poznać konkretne kroki.</span><span class="sxs-lookup"><span data-stu-id="42661-128">See hello [Using Ambari](#using-ambari) section for specific steps.</span></span>

### <a name="enable-heap-dumps"></a><span data-ttu-id="42661-129">Włączanie zrzutów stosu</span><span class="sxs-lookup"><span data-stu-id="42661-129">Enable heap dumps</span></span>

<span data-ttu-id="42661-130">Witaj Poniższa opcja umożliwia zrzuty stosu po wystąpieniu OutOfMemoryError:</span><span class="sxs-lookup"><span data-stu-id="42661-130">hello following option enables heap dumps when an OutOfMemoryError occurs:</span></span>

    -XX:+HeapDumpOnOutOfMemoryError

<span data-ttu-id="42661-131">Witaj  **+**  wskazuje, że ta opcja jest włączona.</span><span class="sxs-lookup"><span data-stu-id="42661-131">hello **+** indicates that this option is enabled.</span></span> <span data-ttu-id="42661-132">Domyślnie Hello jest wyłączona.</span><span class="sxs-lookup"><span data-stu-id="42661-132">hello default is disabled.</span></span>

> [!WARNING]
> <span data-ttu-id="42661-133">Zrzuty stosu nie są włączone dla usługi Hadoop w usłudze HDInsight domyślnie jako pliki zrzutu hello mogą być duże.</span><span class="sxs-lookup"><span data-stu-id="42661-133">Heap dumps are not enabled for Hadoop services on HDInsight by default, as hello dump files can be large.</span></span> <span data-ttu-id="42661-134">Włączenie ich do rozwiązywania problemów, należy pamiętać toodisable hello je po odtworzeniu problemu i hello zebranych plików zrzutu.</span><span class="sxs-lookup"><span data-stu-id="42661-134">If you do enable them for troubleshooting, remember toodisable them once you have reproduced hello problem and gathered hello dump files.</span></span>

### <a name="dump-location"></a><span data-ttu-id="42661-135">Lokalizacja zrzutu</span><span class="sxs-lookup"><span data-stu-id="42661-135">Dump location</span></span>

<span data-ttu-id="42661-136">Domyślna lokalizacja pliku zrzutu hello Hello jest hello bieżący katalog roboczy.</span><span class="sxs-lookup"><span data-stu-id="42661-136">hello default location for hello dump file is hello current working directory.</span></span> <span data-ttu-id="42661-137">Można kontrolować, gdzie hello plik jest przechowywany przy użyciu hello następujących opcji:</span><span class="sxs-lookup"><span data-stu-id="42661-137">You can control where hello file is stored using hello following option:</span></span>

    -XX:HeapDumpPath=/path

<span data-ttu-id="42661-138">Na przykład za pomocą `-XX:HeapDumpPath=/tmp` powoduje, że toobe zrzuty hello przechowywane w TMP hello.</span><span class="sxs-lookup"><span data-stu-id="42661-138">For example, using `-XX:HeapDumpPath=/tmp` causes hello dumps toobe stored in hello /tmp directory.</span></span>

### <a name="scripts"></a><span data-ttu-id="42661-139">Skrypty</span><span class="sxs-lookup"><span data-stu-id="42661-139">Scripts</span></span>

<span data-ttu-id="42661-140">Można również uruchomić skrypt po **OutOfMemoryError** występuje.</span><span class="sxs-lookup"><span data-stu-id="42661-140">You can also trigger a script when an **OutOfMemoryError** occurs.</span></span> <span data-ttu-id="42661-141">Na przykład wyzwalania powiadomienie, aby wiedzieć, że błąd hello wystąpił.</span><span class="sxs-lookup"><span data-stu-id="42661-141">For example, triggering a notification so you know that hello error has occurred.</span></span> <span data-ttu-id="42661-142">Użyj następujących hello opcję tootrigger skrypt na __OutOfMemoryError__:</span><span class="sxs-lookup"><span data-stu-id="42661-142">Use hello following option tootrigger a script on an __OutOfMemoryError__:</span></span>

    -XX:OnOutOfMemoryError=/path/to/script

> [!NOTE]
> <span data-ttu-id="42661-143">Ponieważ Hadoop to Rozproszony system, dowolny skrypt używany muszą znajdować się we wszystkich węzłach w klastrze hello hello usługa jest uruchomiona na.</span><span class="sxs-lookup"><span data-stu-id="42661-143">Since Hadoop is a distributed system, any script used must be placed on all nodes in hello cluster that hello service runs on.</span></span>
> 
> <span data-ttu-id="42661-144">skrypt Hello musi również być w lokalizacji, która jest dostępna przez program hello konta hello usługa działa jako i podać uprawnienia do wykonywania.</span><span class="sxs-lookup"><span data-stu-id="42661-144">hello script must also be in a location that is accessible by hello account hello service runs as, and must provide execute permissions.</span></span> <span data-ttu-id="42661-145">Na przykład możesz toostore skryptów w `/usr/local/bin` i użyj `chmod go+rx /usr/local/bin/filename.sh` toogrant uprawnienia Odczyt i wykonywanie.</span><span class="sxs-lookup"><span data-stu-id="42661-145">For example, you may wish toostore scripts in `/usr/local/bin` and use `chmod go+rx /usr/local/bin/filename.sh` toogrant read and execute permissions.</span></span>

## <a name="using-ambari"></a><span data-ttu-id="42661-146">Za pomocą narzędzia Ambari</span><span class="sxs-lookup"><span data-stu-id="42661-146">Using Ambari</span></span>

<span data-ttu-id="42661-147">toomodify hello konfiguracji dla usługi, użyj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="42661-147">toomodify hello configuration for a service, use hello following steps:</span></span>

1. <span data-ttu-id="42661-148">Otwórz hello Ambari web UI dla klastra.</span><span class="sxs-lookup"><span data-stu-id="42661-148">Open hello Ambari web UI for your cluster.</span></span> <span data-ttu-id="42661-149">adres URL Hello jest https://YOURCLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="42661-149">hello URL is https://YOURCLUSTERNAME.azurehdinsight.net.</span></span>

    <span data-ttu-id="42661-150">Po wyświetleniu monitu uwierzytelniania przy użyciu nazwy konta hello HTTP witryny toohello (domyślne: admin) i hasło dla klastra.</span><span class="sxs-lookup"><span data-stu-id="42661-150">When prompted, authenticate toohello site using hello HTTP account name (default: admin) and password for your cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="42661-151">Może pojawić się prośba po raz drugi przez Ambari hello nazwy użytkownika i hasła.</span><span class="sxs-lookup"><span data-stu-id="42661-151">You may be prompted a second time by Ambari for hello user name and password.</span></span> <span data-ttu-id="42661-152">Jeśli tak, wprowadź hello tę samą nazwę konta i hasło</span><span class="sxs-lookup"><span data-stu-id="42661-152">If so, enter hello same account name and password</span></span>

2. <span data-ttu-id="42661-153">Przy użyciu listy hello powitania po lewej stronie, wybierz obszar usługi hello ma toomodify.</span><span class="sxs-lookup"><span data-stu-id="42661-153">Using hello list of on hello left, select hello service area you want toomodify.</span></span> <span data-ttu-id="42661-154">Na przykład **HDFS**.</span><span class="sxs-lookup"><span data-stu-id="42661-154">For example, **HDFS**.</span></span> <span data-ttu-id="42661-155">W obszarze center hello, wybierz hello **Configs** kartę.</span><span class="sxs-lookup"><span data-stu-id="42661-155">In hello center area, select hello **Configs** tab.</span></span>

    ![Obraz z wybraną kartą Configs systemu plików HDFS w sieci Web Ambari](./media/hdinsight-hadoop-heap-dump-linux/serviceconfig.png)

3. <span data-ttu-id="42661-157">Przy użyciu hello **filtru...**  wpisu, wprowadź **zdecyduje**.</span><span class="sxs-lookup"><span data-stu-id="42661-157">Using hello **Filter...** entry, enter **opts**.</span></span> <span data-ttu-id="42661-158">Tylko elementy zawierające ten tekst są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="42661-158">Only items containing this text are displayed.</span></span>

    ![Filtrowana lista](./media/hdinsight-hadoop-heap-dump-linux/filter.png)

4. <span data-ttu-id="42661-160">Znajdź hello  **\* \_OPTS** wpisu dla usługi hello tooenable zrzuty stosu dla, a następnie dodaj hello opcje chcesz tooenable.</span><span class="sxs-lookup"><span data-stu-id="42661-160">Find hello **\*\_OPTS** entry for hello service you want tooenable heap dumps for, and add hello options you wish tooenable.</span></span> <span data-ttu-id="42661-161">W następujących obrazu hello, zostały dodane `-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/` toohello **HADOOP\_NAMENODE\_OPTS** wpis:</span><span class="sxs-lookup"><span data-stu-id="42661-161">In hello following image, I've added `-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/` toohello **HADOOP\_NAMENODE\_OPTS** entry:</span></span>

    ![HADOOP_NAMENODE_OPTS z - XX: + HeapDumpOnOutOfMemoryError - XX: HeapDumpPath = / tmp /](./media/hdinsight-hadoop-heap-dump-linux/opts.png)

   > [!NOTE]
   > <span data-ttu-id="42661-163">Podczas włączania zrzuty stosu dla hello mapy lub Zmniejsz procesu podrzędnego, wyszukaj hello pola o nazwie **mapreduce.admin.map.child.java.opts** i **mapreduce.admin.reduce.child.java.opts**.</span><span class="sxs-lookup"><span data-stu-id="42661-163">When enabling heap dumps for hello map or reduce child process, look for hello fields named **mapreduce.admin.map.child.java.opts** and **mapreduce.admin.reduce.child.java.opts**.</span></span>

    <span data-ttu-id="42661-164">Użyj hello **zapisać** przycisk toosave hello zmiany.</span><span class="sxs-lookup"><span data-stu-id="42661-164">Use hello **Save** button toosave hello changes.</span></span> <span data-ttu-id="42661-165">Można wprowadzić krótkiej uwagi opisujące hello zmiany.</span><span class="sxs-lookup"><span data-stu-id="42661-165">You can enter a short note describing hello changes.</span></span>

5. <span data-ttu-id="42661-166">Po zastosowaniu zmian hello hello **wymagane jest ponowne uruchomienie** pojawi się ikona obok co najmniej jedna usługa.</span><span class="sxs-lookup"><span data-stu-id="42661-166">Once hello changes have been applied, hello **Restart required** icon appears beside one or more services.</span></span>

    ![ponowne uruchomienie ikonę wymagane i uruchom ponownie przycisku](./media/hdinsight-hadoop-heap-dump-linux/restartrequiredicon.png)

6. <span data-ttu-id="42661-168">Wybierz każda usługa, która wymaga ponownego uruchomienia i użyj hello **akcji usługi** przycisk zbyt**włączyć w trybie konserwacji**.</span><span class="sxs-lookup"><span data-stu-id="42661-168">Select each service that needs a restart, and use hello **Service Actions** button too**Turn On Maintenance Mode**.</span></span> <span data-ttu-id="42661-169">Tryb konserwacji zapobiega alerty generowane z hello usługi po ponownym jej uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="42661-169">Maintenance mode prevents alerts from being generated from hello service when you restart it.</span></span>

    ![Włącz menu Tryb konserwacji](./media/hdinsight-hadoop-heap-dump-linux/maintenancemode.png)

7. <span data-ttu-id="42661-171">Po włączeniu trybu konserwacji, użyj hello **Uruchom ponownie** przycisk usługi hello zbyt**Uruchom ponownie wszystkie dokonane**</span><span class="sxs-lookup"><span data-stu-id="42661-171">Once you have enabled maintenance mode, use hello **Restart** button for hello service too**Restart All Effected**</span></span>

    ![Uruchom ponownie wszystkie dotyczy wpisu](./media/hdinsight-hadoop-heap-dump-linux/restartbutton.png)

   > [!NOTE]
   > <span data-ttu-id="42661-173">Witaj wpisy dla hello **ponowne uruchomienie** przycisk mogą być różne dla innych usług.</span><span class="sxs-lookup"><span data-stu-id="42661-173">hello entries for hello **Restart** button may be different for other services.</span></span>

8. <span data-ttu-id="42661-174">Po uruchomieniu usługi hello Użyj hello **akcji usługi** przycisk zbyt**włączyć Wyłącz tryb konserwacji**.</span><span class="sxs-lookup"><span data-stu-id="42661-174">Once hello services have been restarted, use hello **Service Actions** button too**Turn Off Maintenance Mode**.</span></span> <span data-ttu-id="42661-175">To monitorowanie dla alertów dla usługi hello tooresume Ambari.</span><span class="sxs-lookup"><span data-stu-id="42661-175">This Ambari tooresume monitoring for alerts for hello service.</span></span>

