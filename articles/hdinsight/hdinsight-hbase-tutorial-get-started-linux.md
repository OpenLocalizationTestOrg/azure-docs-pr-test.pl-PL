---
title: "aaaGet pracy z przykładem bazy danych HBase w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Postępuj zgodnie z tym toostart przykład bazy danych Apache HBase przy użyciu platformy hadoop w usłudze HDInsight. Tworzenie tabel na podstawie hello powłoki HBase i wyszukiwać w nich przy użyciu aplikacji Hive."
keywords: "hbasecommand,przykład hbase"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 4d6a2658-6b19-4268-95ee-822890f5a33a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: 43419780142b320b16180a2b1f25020dee2f7a11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-an-apache-hbase-example-in-hdinsight"></a><span data-ttu-id="4745f-105">Rozpoczynanie pracy z przykładem bazy danych Apache HBase w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="4745f-105">Get started with an Apache HBase example in HDInsight</span></span>

<span data-ttu-id="4745f-106">Dowiedz się, jak toocreate klaster HBase w usłudze HDInsight, tworzenia tabel HBase i wykonywać zapytania dotyczące tabel za pomocą aplikacji Hive.</span><span class="sxs-lookup"><span data-stu-id="4745f-106">Learn how toocreate an HBase cluster in HDInsight, create HBase tables, and query tables by using Hive.</span></span> <span data-ttu-id="4745f-107">Aby uzyskać ogólne informacje o bazie danych HBase, zobacz [Omówienie bazy danych HBase w usłudze HDInsight][hdinsight-hbase-overview].</span><span class="sxs-lookup"><span data-stu-id="4745f-107">For general HBase information, see [HDInsight HBase overview][hdinsight-hbase-overview].</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="prerequisites"></a><span data-ttu-id="4745f-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4745f-108">Prerequisites</span></span>
<span data-ttu-id="4745f-109">Przed rozpoczęciem próby w tym przykładzie HBase, musi mieć hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="4745f-109">Before you begin trying this HBase example, you must have hello following items:</span></span>

* <span data-ttu-id="4745f-110">**Subskrypcja platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="4745f-110">**An Azure subscription**.</span></span> <span data-ttu-id="4745f-111">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="4745f-111">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="4745f-112">[Bezpieczna powłoka (SSH)](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="4745f-112">[Secure Shell(SSH)](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> 
* <span data-ttu-id="4745f-113">[Program curl](http://curl.haxx.se/download.html).</span><span class="sxs-lookup"><span data-stu-id="4745f-113">[curl](http://curl.haxx.se/download.html).</span></span>

## <a name="create-hbase-cluster"></a><span data-ttu-id="4745f-114">Tworzenie klastra HBase</span><span class="sxs-lookup"><span data-stu-id="4745f-114">Create HBase cluster</span></span>
<span data-ttu-id="4745f-115">Hello poniższej procedury używa toocreate szablonu usługi Azure Resource Manager wersji 3.4 HBase opartych na systemie Linux klaster i hello zależnych domyślne Azure konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="4745f-115">hello following procedure uses an Azure Resource Manager template toocreate a version 3.4 Linux-based HBase cluster and hello dependent default Azure Storage account.</span></span> <span data-ttu-id="4745f-116">Parametry hello toounderstand używany w procedurze hello oraz innymi metodami tworzenia klastra, zobacz [utworzyć Linux opartych klastrów Hadoop w usłudze HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="4745f-116">toounderstand hello parameters used in hello procedure and other cluster creation methods, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

1. <span data-ttu-id="4745f-117">Kliknij przycisk hello następującego szablonu hello tooopen obrazu w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="4745f-117">Click hello following image tooopen hello template in hello Azure portal.</span></span> <span data-ttu-id="4745f-118">Szablon Hello znajduje się w publicznym kontenerze obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="4745f-118">hello template is located in a public blob container.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-tutorial-get-started-linux/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. <span data-ttu-id="4745f-119">Z hello **wdrożenie niestandardowe** bloku, wprowadź hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="4745f-119">From hello **Custom deployment** blade, enter hello following values:</span></span>
   
   * <span data-ttu-id="4745f-120">**Subskrypcja**: Wybierz subskrypcji platformy Azure, która jest używana toocreate hello klastra.</span><span class="sxs-lookup"><span data-stu-id="4745f-120">**Subscription**: Select your Azure subscription that is used toocreate hello cluster.</span></span>
   * <span data-ttu-id="4745f-121">**Grupa zasobów**: utwórz grupę usługi Azure Resource Management lub użyj istniejącej.</span><span class="sxs-lookup"><span data-stu-id="4745f-121">**Resource group**: Create an Azure Resource Management group or use an existing one.</span></span>
   * <span data-ttu-id="4745f-122">**Lokalizacja**: Określ lokalizację hello hello grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="4745f-122">**Location**: Specify hello location of hello resource group.</span></span> 
   * <span data-ttu-id="4745f-123">**ClusterName**: Wprowadź nazwę klastra HBase hello.</span><span class="sxs-lookup"><span data-stu-id="4745f-123">**ClusterName**: Enter a name for hello HBase cluster.</span></span>
   * <span data-ttu-id="4745f-124">**Nazwa logowania i hasło klastra**: hello domyślna nazwa logowania jest **admin**.</span><span class="sxs-lookup"><span data-stu-id="4745f-124">**Cluster login name and password**: hello default login name is **admin**.</span></span>
   * <span data-ttu-id="4745f-125">**Nazwa użytkownika SSH i hasło**: hello domyślna nazwa użytkownika to **sshuser**.</span><span class="sxs-lookup"><span data-stu-id="4745f-125">**SSH username and password**: hello default username is **sshuser**.</span></span>  <span data-ttu-id="4745f-126">Tę nazwę można zmienić.</span><span class="sxs-lookup"><span data-stu-id="4745f-126">You can rename it.</span></span>
     
     <span data-ttu-id="4745f-127">Inne parametry są opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="4745f-127">Other parameters are optional.</span></span>  
     
     <span data-ttu-id="4745f-128">Każdy klaster zależy od konta usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="4745f-128">Each cluster has an Azure Storage account dependency.</span></span> <span data-ttu-id="4745f-129">Po usunięciu klastra dane hello pozostają zachowane na koncie magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="4745f-129">After you delete a cluster, hello data retains in hello storage account.</span></span> <span data-ttu-id="4745f-130">klastra Hello domyślna nazwa konta magazynu jest nazwą klastra hello z dołączany "store".</span><span class="sxs-lookup"><span data-stu-id="4745f-130">hello cluster default storage account name is hello cluster name with "store" appended.</span></span> <span data-ttu-id="4745f-131">Jest zapisane na stałe w sekcji zmiennych szablonu hello.</span><span class="sxs-lookup"><span data-stu-id="4745f-131">It is hardcoded in hello template variables section.</span></span>
3. <span data-ttu-id="4745f-132">Wybierz **zgadzam się toohello warunki i postanowienia, o których wspomniano**, a następnie kliknij przycisk **zakupu**.</span><span class="sxs-lookup"><span data-stu-id="4745f-132">Select **I agree toohello terms and conditions stated above**, and then click **Purchase**.</span></span> <span data-ttu-id="4745f-133">Trwa około 20 minut toocreate klastra.</span><span class="sxs-lookup"><span data-stu-id="4745f-133">It takes about 20 minutes toocreate a cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="4745f-134">Po usunięciu klastra HBase można utworzyć inny klaster HBase przy użyciu hello tego samego domyślnego kontenera obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="4745f-134">After an HBase cluster is deleted, you can create another HBase cluster by using hello same default blob container.</span></span> <span data-ttu-id="4745f-135">nowy klaster Hello przejmuje hello tabele bazy danych HBase utworzone w oryginalnym klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="4745f-135">hello new cluster picks up hello HBase tables you created in hello original cluster.</span></span> <span data-ttu-id="4745f-136">tooavoid niespójności, zaleca się wyłączyć hello tabel HBase, przed usunięciem hello klastra.</span><span class="sxs-lookup"><span data-stu-id="4745f-136">tooavoid inconsistencies, we recommend that you disable hello HBase tables before you delete hello cluster.</span></span>
> 
> 

## <a name="create-tables-and-insert-data"></a><span data-ttu-id="4745f-137">Tworzenie tabel i wstawianie danych</span><span class="sxs-lookup"><span data-stu-id="4745f-137">Create tables and insert data</span></span>
<span data-ttu-id="4745f-138">Można za pomocą protokołu SSH tooconnect tooHBase klastrów i następnie używać tabel HBase toocreate powłoki HBase, wstawiania danych i zapytania o dane.</span><span class="sxs-lookup"><span data-stu-id="4745f-138">You can use SSH tooconnect tooHBase clusters and then use HBase Shell toocreate HBase tables, insert data, and query data.</span></span> <span data-ttu-id="4745f-139">Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="4745f-139">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="4745f-140">Dla większości użytkowników dane są wyświetlane w formacie tabelarycznym hello:</span><span class="sxs-lookup"><span data-stu-id="4745f-140">For most people, data appears in hello tabular format:</span></span>

![Dane tabelaryczne usługi HDInsight HBase][img-hbase-sample-data-tabular]

<span data-ttu-id="4745f-142">W bazie danych HBase (implementacją BigTable) hello tego samego danych wygląda jak:</span><span class="sxs-lookup"><span data-stu-id="4745f-142">In HBase (an implementation of BigTable), hello same data looks like:</span></span>

![Dane BigTable usługi HDInsight HBase][img-hbase-sample-data-bigtable]


<span data-ttu-id="4745f-144">**Witaj toouse powłoki HBase**</span><span class="sxs-lookup"><span data-stu-id="4745f-144">**toouse hello HBase shell**</span></span>

1. <span data-ttu-id="4745f-145">Z SSH uruchom następujące polecenie HBase hello:</span><span class="sxs-lookup"><span data-stu-id="4745f-145">From SSH, run hello following HBase command:</span></span>
   
    ```bash
    hbase shell
    ```

2. <span data-ttu-id="4745f-146">Utwórz bazę danych HBase z dwiema rodzinami kolumn:</span><span class="sxs-lookup"><span data-stu-id="4745f-146">Create an HBase with two-column families:</span></span>

    ```hbaseshell   
    create 'Contacts', 'Personal', 'Office'
    list
    ```
3. <span data-ttu-id="4745f-147">Wstaw dowolne dane:</span><span class="sxs-lookup"><span data-stu-id="4745f-147">Insert some data:</span></span>
    
    ```hbaseshell   
    put 'Contacts', '1000', 'Personal:Name', 'John Dole'
    put 'Contacts', '1000', 'Personal:Phone', '1-425-000-0001'
    put 'Contacts', '1000', 'Office:Phone', '1-425-000-0002'
    put 'Contacts', '1000', 'Office:Address', '1111 San Gabriel Dr.'
    scan 'Contacts'
    ```
   
    ![Powłoka HBase HDInsight Hadoop][img-hbase-shell]
4. <span data-ttu-id="4745f-149">Pobierz pojedynczy wiersz:</span><span class="sxs-lookup"><span data-stu-id="4745f-149">Get a single row</span></span>
   
    ```hbaseshell
    get 'Contacts', '1000'
    ```
   
    <span data-ttu-id="4745f-150">Zostanie wyświetlona hello takie same wyniki jak za pomocą polecenia scan hello, ponieważ istnieje tylko jeden wiersz.</span><span class="sxs-lookup"><span data-stu-id="4745f-150">You shall see hello same results as using hello scan command because there is only one row.</span></span>
   
    <span data-ttu-id="4745f-151">Aby uzyskać więcej informacji na temat schematu tabeli HBase hello, zobacz [tooHBase wprowadzenie projektu schematu][hbase-schema].</span><span class="sxs-lookup"><span data-stu-id="4745f-151">For more information about hello HBase table schema, see [Introduction tooHBase Schema Design][hbase-schema].</span></span> <span data-ttu-id="4745f-152">Więcej poleceń bazy danych HBase można znaleźć w [Podręczniku bazy danych Apache HBase][hbase-quick-start].</span><span class="sxs-lookup"><span data-stu-id="4745f-152">For more HBase commands, see [Apache HBase reference guide][hbase-quick-start].</span></span>
5. <span data-ttu-id="4745f-153">Zakończ hello powłoki</span><span class="sxs-lookup"><span data-stu-id="4745f-153">Exit hello shell</span></span>
   
    ```hbaseshell
    exit
    ```

<span data-ttu-id="4745f-154">**toobulk ładowanie danych do tabeli hello kontaktów HBase**</span><span class="sxs-lookup"><span data-stu-id="4745f-154">**toobulk load data into hello contacts HBase table**</span></span>

<span data-ttu-id="4745f-155">Baza danych HBase obsługuje kilka metod ładowania danych do tabel.</span><span class="sxs-lookup"><span data-stu-id="4745f-155">HBase includes several methods of loading data into tables.</span></span>  <span data-ttu-id="4745f-156">Aby uzyskać więcej informacji, zobacz temat [Ładowanie zbiorcze](http://hbase.apache.org/book.html#arch.bulk.load).</span><span class="sxs-lookup"><span data-stu-id="4745f-156">For more information, see [Bulk loading](http://hbase.apache.org/book.html#arch.bulk.load).</span></span>

<span data-ttu-id="4745f-157">Przykładowy plik danych znajduje się w publicznym kontenerze obiektów blob, *wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt*.</span><span class="sxs-lookup"><span data-stu-id="4745f-157">A sample data file can be found in a public blob container, *wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt*.</span></span>  <span data-ttu-id="4745f-158">zawartość pliku danych hello Hello jest:</span><span class="sxs-lookup"><span data-stu-id="4745f-158">hello content of hello data file is:</span></span>

    8396    Calvin Raji      230-555-0191    230-555-0191    5415 San Gabriel Dr.
    16600   Karen Wu         646-555-0113    230-555-0192    9265 La Paz
    4324    Karl Xie         508-555-0163    230-555-0193    4912 La Vuelta
    16891   Jonn Jackson     674-555-0110    230-555-0194    40 Ellis St.
    3273    Miguel Miller    397-555-0155    230-555-0195    6696 Anchor Drive
    3588    Osa Agbonile     592-555-0152    230-555-0196    1873 Lion Circle
    10272   Julia Lee        870-555-0110    230-555-0197    3148 Rose Street
    4868    Jose Hayes       599-555-0171    230-555-0198    793 Crawford Street
    4761    Caleb Alexander  670-555-0141    230-555-0199    4775 Kentucky Dr.
    16443   Terry Chander    998-555-0171    230-555-0200    771 Northridge Drive

<span data-ttu-id="4745f-159">Można opcjonalnie utworzyć plik tekstowy i przekaż hello pliku tooyour magazynu własne konto.</span><span class="sxs-lookup"><span data-stu-id="4745f-159">You can optionally create a text file and upload hello file tooyour own storage account.</span></span> <span data-ttu-id="4745f-160">Witaj instrukcje, zobacz [przekazywanie danych dotyczących zadań Hadoop w usłudze HDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="4745f-160">For hello instructions, see [Upload data for Hadoop jobs in HDInsight][hdinsight-upload-data].</span></span>

> [!NOTE]
> <span data-ttu-id="4745f-161">Ta procedura wykorzystuje tabela kontaktów HBase hello utworzony w poprzedniej procedurze hello.</span><span class="sxs-lookup"><span data-stu-id="4745f-161">This procedure uses hello Contacts HBase table you have created in hello last procedure.</span></span>
> 

1. <span data-ttu-id="4745f-162">Z SSH uruchom następujące polecenie tootransform hello danych pliku tooStoreFiles i przechowywać w ścieżce względnej określonej przez parametr Dimporttsv.bulk.output hello.</span><span class="sxs-lookup"><span data-stu-id="4745f-162">From SSH, run hello following command tootransform hello data file tooStoreFiles and store at a relative path specified by Dimporttsv.bulk.output.</span></span>  <span data-ttu-id="4745f-163">Powłoka HBase, za pomocą tooexit polecenie zakończenia hello.</span><span class="sxs-lookup"><span data-stu-id="4745f-163">If you are in HBase Shell, use hello exit command tooexit.</span></span>

    ```bash   
    hbase org.apache.hadoop.hbase.mapreduce.ImportTsv -Dimporttsv.columns="HBASE_ROW_KEY,Personal:Name,Personal:Phone,Office:Phone,Office:Address" -Dimporttsv.bulk.output="/example/data/storeDataFileOutput" Contacts wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt
    ```

2. <span data-ttu-id="4745f-164">Uruchom następujące polecenie tooupload hello danych z tabeli HBase toohello /example/data/storeDataFileOutput hello:</span><span class="sxs-lookup"><span data-stu-id="4745f-164">Run hello following command tooupload hello data from  /example/data/storeDataFileOutput toohello HBase table:</span></span>
   
    ```bash
    hbase org.apache.hadoop.hbase.mapreduce.LoadIncrementalHFiles /example/data/storeDataFileOutput Contacts
    ```

3. <span data-ttu-id="4745f-165">Otwórz hello powłoki HBase i użyj hello skanowania polecenia toolist hello tabeli zawartości.</span><span class="sxs-lookup"><span data-stu-id="4745f-165">You can open hello HBase shell, and use hello scan command toolist hello table content.</span></span>

## <a name="use-hive-tooquery-hbase"></a><span data-ttu-id="4745f-166">Użyj Hive tooquery HBase</span><span class="sxs-lookup"><span data-stu-id="4745f-166">Use Hive tooquery HBase</span></span>

<span data-ttu-id="4745f-167">Korzystając z programu Hive, można wykonywać zapytania dotyczące danych w tabelach HBase.</span><span class="sxs-lookup"><span data-stu-id="4745f-167">You can query data in HBase tables by using Hive.</span></span> <span data-ttu-id="4745f-168">W tej sekcji utworzysz tabeli programu Hive który mapuje toohello tabeli HBase i używa go tooquery hello danych w tabeli HBase.</span><span class="sxs-lookup"><span data-stu-id="4745f-168">In this section, you create a Hive table that maps toohello HBase table and uses it tooquery hello data in your HBase table.</span></span>

1. <span data-ttu-id="4745f-169">Otwórz **PuTTY**i połącz toohello klastra.</span><span class="sxs-lookup"><span data-stu-id="4745f-169">Open **PuTTY**, and connect toohello cluster.</span></span>  <span data-ttu-id="4745f-170">Zobacz instrukcje hello w poprzedniej procedurze hello.</span><span class="sxs-lookup"><span data-stu-id="4745f-170">See hello instructions in hello previous procedure.</span></span>
2. <span data-ttu-id="4745f-171">W sesji SSH hello Użyj następującego polecenia toostart Beeline hello:</span><span class="sxs-lookup"><span data-stu-id="4745f-171">From hello SSH session, use hello following command toostart Beeline:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    <span data-ttu-id="4745f-172">Aby uzyskać więcej informacji o usłudze Beeline, zobacz [Używanie technologii Hive z usługą Hadoop w usłudze HDInsight z usługą Beeline](hdinsight-hadoop-use-hive-beeline.md).</span><span class="sxs-lookup"><span data-stu-id="4745f-172">For more information about Beeline, see [Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md).</span></span>
       
3. <span data-ttu-id="4745f-173">Uruchom tabeli programu Hive, który mapuje tabeli HBase toohello powitania po toocreate skrypt HiveQL.</span><span class="sxs-lookup"><span data-stu-id="4745f-173">Run hello following HiveQL script  toocreate a Hive table that maps toohello HBase table.</span></span> <span data-ttu-id="4745f-174">Upewnij się, że utworzono hello Przykładowa tabela odwołuje się do wcześniej w tym samouczku przy użyciu hello powłoki HBase przed uruchomieniem tej instrukcji.</span><span class="sxs-lookup"><span data-stu-id="4745f-174">Make sure that you have created hello sample table referenced earlier in this tutorial by using hello HBase shell before you run this statement.</span></span>

    ```hiveql   
    CREATE EXTERNAL TABLE hbasecontacts(rowkey STRING, name STRING, homephone STRING, officephone STRING, officeaddress STRING)
    STORED BY 'org.apache.hadoop.hive.hbase.HBaseStorageHandler'
    WITH SERDEPROPERTIES ('hbase.columns.mapping' = ':key,Personal:Name,Personal:Phone,Office:Phone,Office:Address')
    TBLPROPERTIES ('hbase.table.name' = 'Contacts');
    ```

4. <span data-ttu-id="4745f-175">Uruchom następujące HiveQL skryptu tooquery hello danych w tabeli HBase hello hello:</span><span class="sxs-lookup"><span data-stu-id="4745f-175">Run hello following HiveQL script tooquery hello data in hello HBase table:</span></span>

    ```hiveql   
    SELECT count(rowkey) FROM hbasecontacts;
    ```

## <a name="use-hbase-rest-apis-using-curl"></a><span data-ttu-id="4745f-176">Korzystanie z interfejsów API REST HBase przy użyciu programu Curl</span><span class="sxs-lookup"><span data-stu-id="4745f-176">Use HBase REST APIs using Curl</span></span>

<span data-ttu-id="4745f-177">Witaj interfejsu API REST jest zabezpieczony za pomocą [uwierzytelnianie podstawowe](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="4745f-177">hello REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="4745f-178">Są zawsze tworzyć żądania przy użyciu HTTPS (HTTP Secure) toohelp upewnij się, że poświadczenia są bezpiecznie wysyłane toohello serwera.</span><span class="sxs-lookup"><span data-stu-id="4745f-178">You shall always make requests by using Secure HTTP (HTTPS) toohelp ensure that your credentials are securely sent toohello server.</span></span>

2. <span data-ttu-id="4745f-179">Użyj hello następujące polecenie toolist hello istniejących tabel HBase:</span><span class="sxs-lookup"><span data-stu-id="4745f-179">Use hello following command toolist hello existing HBase tables:</span></span>

    ```bash
    curl -u <UserName>:<Password> \
    -G https://<ClusterName>.azurehdinsight.net/hbaserest/
    ```

3. <span data-ttu-id="4745f-180">Użyj hello następujące polecenia toocreate nową tabelę HBase z rodziny dwie kolumny:</span><span class="sxs-lookup"><span data-stu-id="4745f-180">Use hello following command toocreate a new HBase table with two-column families:</span></span>

    ```bash   
    curl -u <UserName>:<Password> \
    -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/schema" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -d "{\"@name\":\"Contact1\",\"ColumnSchema\":[{\"name\":\"Personal\"},{\"name\":\"Office\"}]}" \
    -v
    ```

    <span data-ttu-id="4745f-181">Witaj schemat jest podany w formacie JSon hello.</span><span class="sxs-lookup"><span data-stu-id="4745f-181">hello schema is provided in hello JSon format.</span></span>
4. <span data-ttu-id="4745f-182">Użyj następującego polecenia tooinsert hello niektóre dane:</span><span class="sxs-lookup"><span data-stu-id="4745f-182">Use hello following command tooinsert some data:</span></span>

    ```bash   
    curl -u <UserName>:<Password> \
    -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/false-row-key" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -d "{\"Row\":[{\"key\":\"MTAwMA==\",\"Cell\": [{\"column\":\"UGVyc29uYWw6TmFtZQ==\", \"$\":\"Sm9obiBEb2xl\"}]}]}" \
    -v
    ```
   
    <span data-ttu-id="4745f-183">Należy najpierw base64 hello wartości podanych w przełączniku -d hello kodowania.</span><span class="sxs-lookup"><span data-stu-id="4745f-183">You must base64 encode hello values specified in hello -d switch.</span></span> <span data-ttu-id="4745f-184">W przykładzie hello:</span><span class="sxs-lookup"><span data-stu-id="4745f-184">In hello example:</span></span>
   
   * <span data-ttu-id="4745f-185">MTAwMA==: 1000</span><span class="sxs-lookup"><span data-stu-id="4745f-185">MTAwMA==: 1000</span></span>
   * <span data-ttu-id="4745f-186">UGVyc29uYWw6TmFtZQ==: Personal:Name</span><span class="sxs-lookup"><span data-stu-id="4745f-186">UGVyc29uYWw6TmFtZQ==: Personal:Name</span></span>
   * <span data-ttu-id="4745f-187">Sm9obiBEb2xl: John Dole</span><span class="sxs-lookup"><span data-stu-id="4745f-187">Sm9obiBEb2xl: John Dole</span></span>
     
     <span data-ttu-id="4745f-188">[FALSE wiersz klucza](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/rest/package-summary.html#operation_cell_store_single) pozwala tooinsert wiele wartości (wsadów).</span><span class="sxs-lookup"><span data-stu-id="4745f-188">[false-row-key](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/rest/package-summary.html#operation_cell_store_single) allows you tooinsert multiple (batched) values.</span></span>
5. <span data-ttu-id="4745f-189">Użyj hello następujące polecenia tooget wiersza:</span><span class="sxs-lookup"><span data-stu-id="4745f-189">Use hello following command tooget a row:</span></span>
   
    ```bash 
    curl -u <UserName>:<Password> \
    -X GET "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/1000" \
    -H "Accept: application/json" \
    -v
    ```

<span data-ttu-id="4745f-190">Aby uzyskać więcej informacji o interfejsie Rest HBase, zobacz [Apache HBase Reference Guide](https://hbase.apache.org/book.html#_rest) (Podręcznik referencyjny Apache HBase).</span><span class="sxs-lookup"><span data-stu-id="4745f-190">For more information about HBase Rest, see [Apache HBase Reference Guide](https://hbase.apache.org/book.html#_rest).</span></span>

> [!NOTE]
> <span data-ttu-id="4745f-191">Platforma Thrift nie jest obsługiwana przez bazę danych HBase w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4745f-191">Thrift is not supported by HBase in HDInsight.</span></span>
>
> <span data-ttu-id="4745f-192">Po za pomocą Curl lub innego połączenia REST z usługą WebHCat, zapewniając hello nazwę użytkownika i hasło administratora klastra usługi HDInsight hello musi uwierzytelnić się hello żądania.</span><span class="sxs-lookup"><span data-stu-id="4745f-192">When using Curl or any other REST communication with WebHCat, you must authenticate hello requests by providing hello user name and password for hello HDInsight cluster administrator.</span></span> <span data-ttu-id="4745f-193">Należy również użyć nazwy klastra hello jako część hello identyfikator URI (Uniform Resource) używane toosend hello żądań toohello serwera:</span><span class="sxs-lookup"><span data-stu-id="4745f-193">You must also use hello cluster name as part of hello Uniform Resource Identifier (URI) used toosend hello requests toohello server:</span></span>
> 
>   
>        curl -u <UserName>:<Password> \
>        -G https://<ClusterName>.azurehdinsight.net/templeton/v1/status
>   
>    <span data-ttu-id="4745f-194">Powinien zostać wyświetlony odpowiedzi toohello podobne, po odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="4745f-194">You should receive a response similar toohello following response:</span></span>
>   
>        {"status":"ok","version":"v1"}
   


## <a name="check-cluster-status"></a><span data-ttu-id="4745f-195">Sprawdzanie stanu klastra</span><span class="sxs-lookup"><span data-stu-id="4745f-195">Check cluster status</span></span>
<span data-ttu-id="4745f-196">Baza danych HBase w usłudze HDInsight jest dostarczana z interfejsem użytkownika sieci Web służącym do monitorowania klastrów.</span><span class="sxs-lookup"><span data-stu-id="4745f-196">HBase in HDInsight ships with a Web UI for monitoring clusters.</span></span> <span data-ttu-id="4745f-197">Przy użyciu hello interfejsu użytkownika sieci Web, możesz poprosić statystyk lub informacji o regionach.</span><span class="sxs-lookup"><span data-stu-id="4745f-197">Using hello Web UI, you can request statistics or information about regions.</span></span>

<span data-ttu-id="4745f-198">**Witaj tooaccess głównego HBase interfejsu użytkownika**</span><span class="sxs-lookup"><span data-stu-id="4745f-198">**tooaccess hello HBase Master UI**</span></span>

1. <span data-ttu-id="4745f-199">Zaloguj się na powitania hello Interfejsu sieci Web Ambari w https://&lt;Clustername >. azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="4745f-199">Sign into hello hello Ambari Web UI at https://&lt;Clustername>.azurehdinsight.net.</span></span>
2. <span data-ttu-id="4745f-200">Kliknij przycisk **HBase** z menu po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="4745f-200">Click **HBase** from hello left menu.</span></span>
3. <span data-ttu-id="4745f-201">Kliknij przycisk **szybkie linki** na hello górnej części strony hello, toohello punktu aktywnego dozorcy węzła łącza, a następnie kliknij przycisk **interfejsu użytkownika głównego HBase**.</span><span class="sxs-lookup"><span data-stu-id="4745f-201">Click **Quick links** on hello top of hello page, point toohello active Zookeeper node link, and then click **HBase Master UI**.</span></span>  <span data-ttu-id="4745f-202">Witaj interfejsu użytkownika jest otwarty w innej karty przeglądarki:</span><span class="sxs-lookup"><span data-stu-id="4745f-202">hello UI is opened in another browser tab:</span></span>

  ![Główny interfejs użytkownika HDInsight HBase](./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-hmaster-ui.png)

  <span data-ttu-id="4745f-204">Witaj interfejsu użytkownika głównego HBase zawiera hello następujące sekcje:</span><span class="sxs-lookup"><span data-stu-id="4745f-204">hello HBase Master UI contains hello following sections:</span></span>

  - <span data-ttu-id="4745f-205">serwery regionów</span><span class="sxs-lookup"><span data-stu-id="4745f-205">region servers</span></span>
  - <span data-ttu-id="4745f-206">wzorce kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="4745f-206">backup masters</span></span>
  - <span data-ttu-id="4745f-207">tabele</span><span class="sxs-lookup"><span data-stu-id="4745f-207">tables</span></span>
  - <span data-ttu-id="4745f-208">zadania</span><span class="sxs-lookup"><span data-stu-id="4745f-208">tasks</span></span>
  - <span data-ttu-id="4745f-209">atrybuty oprogramowania</span><span class="sxs-lookup"><span data-stu-id="4745f-209">software attributes</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="4745f-210">Usuń klaster hello</span><span class="sxs-lookup"><span data-stu-id="4745f-210">Delete hello cluster</span></span>
<span data-ttu-id="4745f-211">tooavoid niespójności, zaleca się wyłączyć hello tabel HBase, przed usunięciem hello klastra.</span><span class="sxs-lookup"><span data-stu-id="4745f-211">tooavoid inconsistencies, we recommend that you disable hello HBase tables before you delete hello cluster.</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="4745f-212">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="4745f-212">Troubleshoot</span></span>

<span data-ttu-id="4745f-213">W razie problemów podczas tworzenia klastrów usługi HDInsight zapoznaj się z [wymaganiami dotyczącymi kontroli dostępu](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="4745f-213">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4745f-214">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4745f-214">Next steps</span></span>
<span data-ttu-id="4745f-215">W tym artykule przedstawiono sposób toocreate klaster HBase oraz jak toocreate tabele i widoki hello danych w tych tabelach z hello powłoki HBase.</span><span class="sxs-lookup"><span data-stu-id="4745f-215">In this article, you learned how toocreate an HBase cluster and how toocreate tables and view hello data in those tables from hello HBase shell.</span></span> <span data-ttu-id="4745f-216">Przedstawiono również sposób toouse gałąź zapytania na danych w tabelach HBase oraz jak toouse hello toocreate C# interfejsów API REST HBase tabeli HBase i pobierania danych z tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="4745f-216">You also learned how toouse a Hive query on data in HBase tables and how toouse hello HBase C# REST APIs toocreate an HBase table and retrieve data from hello table.</span></span>

<span data-ttu-id="4745f-217">toolearn więcej, zobacz:</span><span class="sxs-lookup"><span data-stu-id="4745f-217">toolearn more, see:</span></span>

* <span data-ttu-id="4745f-218">[Przegląd bazy danych HBase w usłudze HDInsight][hdinsight-hbase-overview]: HBase jest bazą danych Apache NoSQL typu open source opartą na platformie Hadoop, która zapewnia dostęp losowy i wysoki poziom spójności w przypadku dużych ilości danych z częściową strukturą i bez struktury.</span><span class="sxs-lookup"><span data-stu-id="4745f-218">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>

[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hbase-reference]: http://hbase.apache.org/book.html#importtsv
[hbase-schema]: http://0b4af6cdc2f0c5998459-c0245c5c937c5dedcca3f1764ecc9b2f.r43.cf2.rackcdn.com/9353-login1210_khurana.pdf
[hbase-quick-start]: http://hbase.apache.org/book.html#quickstart





[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-versions]: hdinsight-component-versioning.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-portal]: https://portal.azure.com/
[azure-create-storageaccount]: http://azure.microsoft.com/documentation/articles/storage-create-storage-account/

[img-hdinsight-hbase-cluster-quick-create]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-quick-create.png
[img-hdinsight-hbase-hive-editor]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-hive-editor.png
[img-hdinsight-hbase-file-browser]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-file-browser.png
[img-hbase-shell]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-shell.png
[img-hbase-sample-data-tabular]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-contacts-tabular.png
[img-hbase-sample-data-bigtable]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-contacts-bigtable.png
