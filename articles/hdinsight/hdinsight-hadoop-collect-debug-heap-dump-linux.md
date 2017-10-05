---
title: "Włącz zrzuty stosu dla usługi Hadoop w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 59942e989d622c2486edf181d76e13344c71e6f9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="enable-heap-dumps-for-hadoop-services-on-linux-based-hdinsight"></a><span data-ttu-id="82833-103">Włącz zrzuty stosu dla usługi Hadoop w HDInsight opartych na systemie Linux</span><span class="sxs-lookup"><span data-stu-id="82833-103">Enable heap dumps for Hadoop services on Linux-based HDInsight</span></span>

[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

<span data-ttu-id="82833-104">Zrzuty stosu zawierającego migawkę pamięci aplikacji, w tym wartości zmiennych w czasie tworzenia zrzutu.</span><span class="sxs-lookup"><span data-stu-id="82833-104">Heap dumps contain a snapshot of the application's memory, including the values of variables at the time the dump was created.</span></span> <span data-ttu-id="82833-105">Tak, aby były przydatne do diagnozowania problemów występujących w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="82833-105">So they are useful for diagnosing problems that occur at run-time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="82833-106">Kroki opisane w tym dokumencie pracować tylko z klastrami usługi HDInsight, które używają systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="82833-106">The steps in this document only work with HDInsight clusters that use Linux.</span></span> <span data-ttu-id="82833-107">Linux jest jedynym systemem operacyjnym używanym w połączeniu z usługą HDInsight w wersji 3.4 lub nowszą.</span><span class="sxs-lookup"><span data-stu-id="82833-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="82833-108">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="82833-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="82833-109"><a name="whichServices"></a>Usługi</span><span class="sxs-lookup"><span data-stu-id="82833-109"><a name="whichServices"></a>Services</span></span>

<span data-ttu-id="82833-110">Można włączyć zrzuty stosu dla następujących usług:</span><span class="sxs-lookup"><span data-stu-id="82833-110">You can enable heap dumps for the following services:</span></span>

* <span data-ttu-id="82833-111">**hcatalog** -tempelton</span><span class="sxs-lookup"><span data-stu-id="82833-111">**hcatalog** - tempelton</span></span>
* <span data-ttu-id="82833-112">**gałąź** -serwera hiveserver2, potrzeby magazynu metadanych, derbyserver</span><span class="sxs-lookup"><span data-stu-id="82833-112">**hive** - hiveserver2, metastore, derbyserver</span></span>
* <span data-ttu-id="82833-113">**mapreduce** -jobhistoryserver</span><span class="sxs-lookup"><span data-stu-id="82833-113">**mapreduce** - jobhistoryserver</span></span>
* <span data-ttu-id="82833-114">**yarn** -resourcemanager nodemanager, timelineserver</span><span class="sxs-lookup"><span data-stu-id="82833-114">**yarn** - resourcemanager, nodemanager, timelineserver</span></span>
* <span data-ttu-id="82833-115">**System plików hdfs** -datanode secondarynamenode, namenode</span><span class="sxs-lookup"><span data-stu-id="82833-115">**hdfs** - datanode, secondarynamenode, namenode</span></span>

<span data-ttu-id="82833-116">Można także włączyć zrzuty stosu mapy i zmniejszyć procesów uruchomionych przez usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="82833-116">You can also enable heap dumps for the map and reduce processes ran by HDInsight.</span></span>

## <span data-ttu-id="82833-117"><a name="configuration"></a>Opis sterty zrzutu konfiguracji</span><span class="sxs-lookup"><span data-stu-id="82833-117"><a name="configuration"></a>Understanding heap dump configuration</span></span>

<span data-ttu-id="82833-118">Zrzuty stosu są włączane przez przeniesienie opcji (czasami znana jako zdecyduje, lub parametrów) do maszyny JVM podczas uruchamiania usługi.</span><span class="sxs-lookup"><span data-stu-id="82833-118">Heap dumps are enabled by passing options (sometimes known as opts, or parameters) to the JVM when a service is started.</span></span> <span data-ttu-id="82833-119">Dla większości usług Hadoop można zmodyfikować skrypt powłoki, używane do uruchamiania usługi do przekazania tych opcji.</span><span class="sxs-lookup"><span data-stu-id="82833-119">For most Hadoop services, you can modify the shell script used to start the service to pass these options.</span></span>

<span data-ttu-id="82833-120">Każdy skrypt ma Eksport  **\* \_OPTS**, który zawiera opcje przekazane do maszyny wirtualnej Java.</span><span class="sxs-lookup"><span data-stu-id="82833-120">In each script, there is an export for **\*\_OPTS**, which contains the options passed to the JVM.</span></span> <span data-ttu-id="82833-121">Na przykład w **hadoop env.sh** skryptu wiersza, który rozpoczyna się od `export HADOOP_NAMENODE_OPTS=` zawiera opcje usługi NameNode.</span><span class="sxs-lookup"><span data-stu-id="82833-121">For example, in the **hadoop-env.sh** script, the line that begins with `export HADOOP_NAMENODE_OPTS=` contains the options for the NameNode service.</span></span>

<span data-ttu-id="82833-122">Mapowanie i zmniejszenie procesy są nieco inne operacje te są Proces podrzędny usługi MapReduce.</span><span class="sxs-lookup"><span data-stu-id="82833-122">Map and reduce processes are slightly different, as these operations are a child process of the MapReduce service.</span></span> <span data-ttu-id="82833-123">Każdy mapy lub Zmniejsz proces jest uruchomiony w kontenerze, a dwa wpisy zawierające opcje maszyny wirtualnej Java.</span><span class="sxs-lookup"><span data-stu-id="82833-123">Each map or reduce process runs in a child container, and there are two entries that contain the JVM options.</span></span> <span data-ttu-id="82833-124">Zarówno zawarte w **mapred-site.xml**:</span><span class="sxs-lookup"><span data-stu-id="82833-124">Both contained in **mapred-site.xml**:</span></span>

* <span data-ttu-id="82833-125">**mapreduce.Admin.map.child.Java.opts**</span><span class="sxs-lookup"><span data-stu-id="82833-125">**mapreduce.admin.map.child.java.opts**</span></span>
* <span data-ttu-id="82833-126">**mapreduce.Admin.Reduce.child.Java.opts**</span><span class="sxs-lookup"><span data-stu-id="82833-126">**mapreduce.admin.reduce.child.java.opts**</span></span>

> [!NOTE]
> <span data-ttu-id="82833-127">Firma Microsoft zaleca, aby zmodyfikować skrypty i ustawienia mapred-site.xml jako dojście Ambari replikowanie zmian w węzłach w klastrze za pomocą narzędzia Ambari.</span><span class="sxs-lookup"><span data-stu-id="82833-127">We recommend using Ambari to modify both the scripts and mapred-site.xml settings, as Ambari handle replicating changes across nodes in the cluster.</span></span> <span data-ttu-id="82833-128">Zobacz [przy użyciu Ambari](#using-ambari) sekcji, aby poznać konkretne kroki.</span><span class="sxs-lookup"><span data-stu-id="82833-128">See the [Using Ambari](#using-ambari) section for specific steps.</span></span>

### <a name="enable-heap-dumps"></a><span data-ttu-id="82833-129">Włączanie zrzutów stosu</span><span class="sxs-lookup"><span data-stu-id="82833-129">Enable heap dumps</span></span>

<span data-ttu-id="82833-130">Poniższa opcja umożliwia zrzuty stosu po wystąpieniu OutOfMemoryError:</span><span class="sxs-lookup"><span data-stu-id="82833-130">The following option enables heap dumps when an OutOfMemoryError occurs:</span></span>

    -XX:+HeapDumpOnOutOfMemoryError

<span data-ttu-id="82833-131"> **+**  Wskazuje, że ta opcja jest włączona.</span><span class="sxs-lookup"><span data-stu-id="82833-131">The **+** indicates that this option is enabled.</span></span> <span data-ttu-id="82833-132">Domyślnie jest wyłączona.</span><span class="sxs-lookup"><span data-stu-id="82833-132">The default is disabled.</span></span>

> [!WARNING]
> <span data-ttu-id="82833-133">Zrzuty stosu nie są włączone dla usługi Hadoop w usłudze HDInsight domyślnie jako pliki zrzutu mogą być duże.</span><span class="sxs-lookup"><span data-stu-id="82833-133">Heap dumps are not enabled for Hadoop services on HDInsight by default, as the dump files can be large.</span></span> <span data-ttu-id="82833-134">Jeśli włączysz ich do rozwiązywania problemów, pamiętaj, aby je wyłączyć, po problemu i zebranych plików zrzutu.</span><span class="sxs-lookup"><span data-stu-id="82833-134">If you do enable them for troubleshooting, remember to disable them once you have reproduced the problem and gathered the dump files.</span></span>

### <a name="dump-location"></a><span data-ttu-id="82833-135">Lokalizacja zrzutu</span><span class="sxs-lookup"><span data-stu-id="82833-135">Dump location</span></span>

<span data-ttu-id="82833-136">Domyślna lokalizacja pliku zrzutu jest bieżący katalog roboczy.</span><span class="sxs-lookup"><span data-stu-id="82833-136">The default location for the dump file is the current working directory.</span></span> <span data-ttu-id="82833-137">Można kontrolować, w przypadku, gdy plik jest przechowywany przy użyciu następujących opcji:</span><span class="sxs-lookup"><span data-stu-id="82833-137">You can control where the file is stored using the following option:</span></span>

    -XX:HeapDumpPath=/path

<span data-ttu-id="82833-138">Na przykład za pomocą `-XX:HeapDumpPath=/tmp` powoduje, że zrzuty mają być przechowywane w TMP.</span><span class="sxs-lookup"><span data-stu-id="82833-138">For example, using `-XX:HeapDumpPath=/tmp` causes the dumps to be stored in the /tmp directory.</span></span>

### <a name="scripts"></a><span data-ttu-id="82833-139">Skrypty</span><span class="sxs-lookup"><span data-stu-id="82833-139">Scripts</span></span>

<span data-ttu-id="82833-140">Można również uruchomić skrypt po **OutOfMemoryError** występuje.</span><span class="sxs-lookup"><span data-stu-id="82833-140">You can also trigger a script when an **OutOfMemoryError** occurs.</span></span> <span data-ttu-id="82833-141">Na przykład wyzwalania powiadomienie, aby wiedzieć, że wystąpił błąd.</span><span class="sxs-lookup"><span data-stu-id="82833-141">For example, triggering a notification so you know that the error has occurred.</span></span> <span data-ttu-id="82833-142">Użyj opcji, aby wyzwolić skrypt na __OutOfMemoryError__:</span><span class="sxs-lookup"><span data-stu-id="82833-142">Use the following option to trigger a script on an __OutOfMemoryError__:</span></span>

    -XX:OnOutOfMemoryError=/path/to/script

> [!NOTE]
> <span data-ttu-id="82833-143">Ponieważ Hadoop to Rozproszony system, dowolny skrypt używany muszą znajdować się na wszystkich węzłach w klastrze, na którym usługa jest uruchamiana na.</span><span class="sxs-lookup"><span data-stu-id="82833-143">Since Hadoop is a distributed system, any script used must be placed on all nodes in the cluster that the service runs on.</span></span>
> 
> <span data-ttu-id="82833-144">Skrypt musi również być w lokalizacji, która jest dostępny dla konta usługi działa jako i podać uprawnienia do wykonywania.</span><span class="sxs-lookup"><span data-stu-id="82833-144">The script must also be in a location that is accessible by the account the service runs as, and must provide execute permissions.</span></span> <span data-ttu-id="82833-145">Na przykład, warto przechowywać skryptów w `/usr/local/bin` i użyj `chmod go+rx /usr/local/bin/filename.sh` Aby udzielić odczytu i uprawnienia do wykonywania.</span><span class="sxs-lookup"><span data-stu-id="82833-145">For example, you may wish to store scripts in `/usr/local/bin` and use `chmod go+rx /usr/local/bin/filename.sh` to grant read and execute permissions.</span></span>

## <a name="using-ambari"></a><span data-ttu-id="82833-146">Za pomocą narzędzia Ambari</span><span class="sxs-lookup"><span data-stu-id="82833-146">Using Ambari</span></span>

<span data-ttu-id="82833-147">Aby zmodyfikować konfigurację usługi, użyj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="82833-147">To modify the configuration for a service, use the following steps:</span></span>

1. <span data-ttu-id="82833-148">Otwórz Ambari web UI dla klastra.</span><span class="sxs-lookup"><span data-stu-id="82833-148">Open the Ambari web UI for your cluster.</span></span> <span data-ttu-id="82833-149">Adres URL jest https://YOURCLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="82833-149">The URL is https://YOURCLUSTERNAME.azurehdinsight.net.</span></span>

    <span data-ttu-id="82833-150">Po wyświetleniu monitu uwierzytelniania do witryny przy użyciu nazwy konta HTTP (domyślne: admin) i hasło dla klastra.</span><span class="sxs-lookup"><span data-stu-id="82833-150">When prompted, authenticate to the site using the HTTP account name (default: admin) and password for your cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="82833-151">Może pojawić się prośba po raz drugi przez Ambari dla nazwy użytkownika i hasła.</span><span class="sxs-lookup"><span data-stu-id="82833-151">You may be prompted a second time by Ambari for the user name and password.</span></span> <span data-ttu-id="82833-152">Jeśli tak, wprowadź nazwę konta i hasło</span><span class="sxs-lookup"><span data-stu-id="82833-152">If so, enter the same account name and password</span></span>

2. <span data-ttu-id="82833-153">Przy użyciu listy po lewej stronie, wybierz obszar usługi, który chcesz zmodyfikować.</span><span class="sxs-lookup"><span data-stu-id="82833-153">Using the list of on the left, select the service area you want to modify.</span></span> <span data-ttu-id="82833-154">Na przykład **HDFS**.</span><span class="sxs-lookup"><span data-stu-id="82833-154">For example, **HDFS**.</span></span> <span data-ttu-id="82833-155">W obszarze Centrum wybierz **Configs** kartę.</span><span class="sxs-lookup"><span data-stu-id="82833-155">In the center area, select the **Configs** tab.</span></span>

    ![Obraz z wybraną kartą Configs systemu plików HDFS w sieci Web Ambari](./media/hdinsight-hadoop-heap-dump-linux/serviceconfig.png)

3. <span data-ttu-id="82833-157">Przy użyciu **filtru...**  wpisu, wprowadź **zdecyduje**.</span><span class="sxs-lookup"><span data-stu-id="82833-157">Using the **Filter...** entry, enter **opts**.</span></span> <span data-ttu-id="82833-158">Tylko elementy zawierające ten tekst są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="82833-158">Only items containing this text are displayed.</span></span>

    ![Filtrowana lista](./media/hdinsight-hadoop-heap-dump-linux/filter.png)

4. <span data-ttu-id="82833-160">Znajdź  **\* \_OPTS** wpisu dla usługi chcesz włączyć zrzuty stosu dla, a następnie dodaj odpowiednie opcje, które mają zostać włączone.</span><span class="sxs-lookup"><span data-stu-id="82833-160">Find the **\*\_OPTS** entry for the service you want to enable heap dumps for, and add the options you wish to enable.</span></span> <span data-ttu-id="82833-161">Na poniższej ilustracji, zostały dodane `-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/` do **HADOOP\_NAMENODE\_OPTS** wpis:</span><span class="sxs-lookup"><span data-stu-id="82833-161">In the following image, I've added `-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/` to the **HADOOP\_NAMENODE\_OPTS** entry:</span></span>

    ![HADOOP_NAMENODE_OPTS z - XX: + HeapDumpOnOutOfMemoryError - XX: HeapDumpPath = / tmp /](./media/hdinsight-hadoop-heap-dump-linux/opts.png)

   > [!NOTE]
   > <span data-ttu-id="82833-163">Podczas włączania sterty zrzuty mapy lub Zmniejsz procesu podrzędnego poszukać w polach o nazwie **mapreduce.admin.map.child.java.opts** i **mapreduce.admin.reduce.child.java.opts**.</span><span class="sxs-lookup"><span data-stu-id="82833-163">When enabling heap dumps for the map or reduce child process, look for the fields named **mapreduce.admin.map.child.java.opts** and **mapreduce.admin.reduce.child.java.opts**.</span></span>

    <span data-ttu-id="82833-164">Użyj **zapisać** przycisk, aby zapisać zmiany.</span><span class="sxs-lookup"><span data-stu-id="82833-164">Use the **Save** button to save the changes.</span></span> <span data-ttu-id="82833-165">Można podać krótkiej uwagi opisujące zmiany.</span><span class="sxs-lookup"><span data-stu-id="82833-165">You can enter a short note describing the changes.</span></span>

5. <span data-ttu-id="82833-166">Po zastosowaniu zmiany **wymagane jest ponowne uruchomienie** pojawi się ikona obok co najmniej jedna usługa.</span><span class="sxs-lookup"><span data-stu-id="82833-166">Once the changes have been applied, the **Restart required** icon appears beside one or more services.</span></span>

    ![ponowne uruchomienie ikonę wymagane i uruchom ponownie przycisku](./media/hdinsight-hadoop-heap-dump-linux/restartrequiredicon.png)

6. <span data-ttu-id="82833-168">Wybierz każda usługa, która wymaga ponownego uruchomienia i użyj **akcji usługi** przycisk, aby **włączyć w trybie konserwacji**.</span><span class="sxs-lookup"><span data-stu-id="82833-168">Select each service that needs a restart, and use the **Service Actions** button to **Turn On Maintenance Mode**.</span></span> <span data-ttu-id="82833-169">Tryb konserwacji zapobiega alerty generowane z usługi po ponownym jej uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="82833-169">Maintenance mode prevents alerts from being generated from the service when you restart it.</span></span>

    ![Włącz menu Tryb konserwacji](./media/hdinsight-hadoop-heap-dump-linux/maintenancemode.png)

7. <span data-ttu-id="82833-171">Po włączeniu trybu konserwacji, użyj **Uruchom ponownie** przycisk usługi **Uruchom ponownie wszystkie dokonane**</span><span class="sxs-lookup"><span data-stu-id="82833-171">Once you have enabled maintenance mode, use the **Restart** button for the service to **Restart All Effected**</span></span>

    ![Uruchom ponownie wszystkie dotyczy wpisu](./media/hdinsight-hadoop-heap-dump-linux/restartbutton.png)

   > [!NOTE]
   > <span data-ttu-id="82833-173">wpisy **ponowne uruchomienie** przycisk mogą być różne dla innych usług.</span><span class="sxs-lookup"><span data-stu-id="82833-173">the entries for the **Restart** button may be different for other services.</span></span>

8. <span data-ttu-id="82833-174">Po uruchomieniu usługi, użyj **akcji usługi** przycisk, aby **włączyć Wyłącz tryb konserwacji**.</span><span class="sxs-lookup"><span data-stu-id="82833-174">Once the services have been restarted, use the **Service Actions** button to **Turn Off Maintenance Mode**.</span></span> <span data-ttu-id="82833-175">Tego narzędzia Ambari można wznowić monitorowania alertów dla usługi.</span><span class="sxs-lookup"><span data-stu-id="82833-175">This Ambari to resume monitoring for alerts for the service.</span></span>

