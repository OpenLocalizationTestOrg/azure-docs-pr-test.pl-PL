---
title: "Rozpoczęcie pracy z przykładem bazy danych HBase w usłudze HDInsight Azure | Microsoft Docs"
description: "Zapoznaj się z tym przykładem bazy danych Apache HBase, aby rozpocząć korzystanie z usługi Hadoop w usłudze HDInsight. Utwórz tabele z poziomu powłoki HBase i wykonuj zapytania przy użyciu aplikacji Hive."
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
ms.openlocfilehash: bbd8a838062795ee03ae02dc5e3fd45d841a6e17
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-an-apache-hbase-example-in-hdinsight"></a><span data-ttu-id="affad-105">Rozpoczynanie pracy z przykładem bazy danych Apache HBase w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="affad-105">Get started with an Apache HBase example in HDInsight</span></span>

<span data-ttu-id="affad-106">Dowiedz się, jak utworzyć klaster HBase w usłudze HDInsight i tabele bazy danych HBase oraz jak wykonywać zapytania dotyczące tabel za pomocą aplikacji Hive.</span><span class="sxs-lookup"><span data-stu-id="affad-106">Learn how to create an HBase cluster in HDInsight, create HBase tables, and query tables by using Hive.</span></span> <span data-ttu-id="affad-107">Aby uzyskać ogólne informacje o bazie danych HBase, zobacz [Omówienie bazy danych HBase w usłudze HDInsight][hdinsight-hbase-overview].</span><span class="sxs-lookup"><span data-stu-id="affad-107">For general HBase information, see [HDInsight HBase overview][hdinsight-hbase-overview].</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="prerequisites"></a><span data-ttu-id="affad-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="affad-108">Prerequisites</span></span>
<span data-ttu-id="affad-109">Przed rozpoczęciem prób korzystania z tego przykładu bazy danych HBase należy dysponować następującymi elementami:</span><span class="sxs-lookup"><span data-stu-id="affad-109">Before you begin trying this HBase example, you must have the following items:</span></span>

* <span data-ttu-id="affad-110">**Subskrypcja platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="affad-110">**An Azure subscription**.</span></span> <span data-ttu-id="affad-111">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="affad-111">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="affad-112">[Bezpieczna powłoka (SSH)](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="affad-112">[Secure Shell(SSH)](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> 
* <span data-ttu-id="affad-113">[Program curl](http://curl.haxx.se/download.html).</span><span class="sxs-lookup"><span data-stu-id="affad-113">[curl](http://curl.haxx.se/download.html).</span></span>

## <a name="create-hbase-cluster"></a><span data-ttu-id="affad-114">Tworzenie klastra HBase</span><span class="sxs-lookup"><span data-stu-id="affad-114">Create HBase cluster</span></span>
<span data-ttu-id="affad-115">W poniższej procedurze użyto szablonu usługi Azure Resource Manager do utworzenia klastra HBase opartego na systemie Linux w wersji 3.4 i zależnego domyślnego konta usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="affad-115">The following procedure uses an Azure Resource Manager template to create a version 3.4 Linux-based HBase cluster and the dependent default Azure Storage account.</span></span> <span data-ttu-id="affad-116">Aby zapoznać się z parametrami używanymi w tej procedurze oraz innymi metodami tworzenia klastra, zobacz temat [Tworzenie opartych na systemie Linux klastrów Hadoop w usłudze HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="affad-116">To understand the parameters used in the procedure and other cluster creation methods, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

1. <span data-ttu-id="affad-117">Kliknij poniższy obraz, aby otworzyć szablon w usłudze Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="affad-117">Click the following image to open the template in the Azure portal.</span></span> <span data-ttu-id="affad-118">Szablon znajduje się w publicznym kontenerze obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="affad-118">The template is located in a public blob container.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-tutorial-get-started-linux/deploy-to-azure.png" alt="Deploy to Azure"></a>
2. <span data-ttu-id="affad-119">W bloku **Wdrożenie niestandardowe** wprowadź następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="affad-119">From the **Custom deployment** blade, enter the following values:</span></span>
   
   * <span data-ttu-id="affad-120">**Subskrypcja**: wybierz subskrypcję platformy Azure używaną do utworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="affad-120">**Subscription**: Select your Azure subscription that is used to create the cluster.</span></span>
   * <span data-ttu-id="affad-121">**Grupa zasobów**: utwórz grupę usługi Azure Resource Management lub użyj istniejącej.</span><span class="sxs-lookup"><span data-stu-id="affad-121">**Resource group**: Create an Azure Resource Management group or use an existing one.</span></span>
   * <span data-ttu-id="affad-122">**Lokalizacja**: określ lokalizację grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="affad-122">**Location**: Specify the location of the resource group.</span></span> 
   * <span data-ttu-id="affad-123">**ClusterName**: wprowadź nazwę klastra HBase.</span><span class="sxs-lookup"><span data-stu-id="affad-123">**ClusterName**: Enter a name for the HBase cluster.</span></span>
   * <span data-ttu-id="affad-124">**Nazwa logowania i hasło klastra**: domyślna nazwa logowania to **admin**.</span><span class="sxs-lookup"><span data-stu-id="affad-124">**Cluster login name and password**: The default login name is **admin**.</span></span>
   * <span data-ttu-id="affad-125">**Nazwa użytkownika i hasło SSH**: domyślna nazwa użytkownika to **sshuser**.</span><span class="sxs-lookup"><span data-stu-id="affad-125">**SSH username and password**: The default username is **sshuser**.</span></span>  <span data-ttu-id="affad-126">Tę nazwę można zmienić.</span><span class="sxs-lookup"><span data-stu-id="affad-126">You can rename it.</span></span>
     
     <span data-ttu-id="affad-127">Inne parametry są opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="affad-127">Other parameters are optional.</span></span>  
     
     <span data-ttu-id="affad-128">Każdy klaster zależy od konta usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="affad-128">Each cluster has an Azure Storage account dependency.</span></span> <span data-ttu-id="affad-129">Po usunięciu klastra dane pozostają zachowane na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="affad-129">After you delete a cluster, the data retains in the storage account.</span></span> <span data-ttu-id="affad-130">Domyślna nazwa konta magazynu klastra to nazwa klastra z dołączonym ciągiem „store”.</span><span class="sxs-lookup"><span data-stu-id="affad-130">The cluster default storage account name is the cluster name with "store" appended.</span></span> <span data-ttu-id="affad-131">Jest ona umieszczona w kodzie w sekcji zmiennych szablonu.</span><span class="sxs-lookup"><span data-stu-id="affad-131">It is hardcoded in the template variables section.</span></span>
3. <span data-ttu-id="affad-132">Zaznacz pozycję **Wyrażam zgodę na powyższe warunki i postanowienia**, a następnie kliknij przycisk **Kup**.</span><span class="sxs-lookup"><span data-stu-id="affad-132">Select **I agree to the terms and conditions stated above**, and then click **Purchase**.</span></span> <span data-ttu-id="affad-133">Utworzenie klastra trwa około 20 minut.</span><span class="sxs-lookup"><span data-stu-id="affad-133">It takes about 20 minutes to create a cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="affad-134">Po usunięciu klastra HBase można utworzyć inny klaster HBase za pomocą tego samego domyślnego kontenera obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="affad-134">After an HBase cluster is deleted, you can create another HBase cluster by using the same default blob container.</span></span> <span data-ttu-id="affad-135">Nowy klaster przejmuje tabele bazy danych HBase utworzone w oryginalnym klastrze.</span><span class="sxs-lookup"><span data-stu-id="affad-135">The new cluster picks up the HBase tables you created in the original cluster.</span></span> <span data-ttu-id="affad-136">Aby uniknąć niespójności, zaleca się wyłączenie tabel HBase przed usunięciem klastra.</span><span class="sxs-lookup"><span data-stu-id="affad-136">To avoid inconsistencies, we recommend that you disable the HBase tables before you delete the cluster.</span></span>
> 
> 

## <a name="create-tables-and-insert-data"></a><span data-ttu-id="affad-137">Tworzenie tabel i wstawianie danych</span><span class="sxs-lookup"><span data-stu-id="affad-137">Create tables and insert data</span></span>
<span data-ttu-id="affad-138">Protokół SSH umożliwia połączenie z klastrami HBase, a następnie korzystanie z powłoki HBase w celu tworzenia tabel bazy danych HBase, wstawiania danych i wykonywania zapytań.</span><span class="sxs-lookup"><span data-stu-id="affad-138">You can use SSH to connect to HBase clusters and then use HBase Shell to create HBase tables, insert data, and query data.</span></span> <span data-ttu-id="affad-139">Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="affad-139">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="affad-140">Dla większości użytkowników dane są wyświetlane w formacie tabelarycznym:</span><span class="sxs-lookup"><span data-stu-id="affad-140">For most people, data appears in the tabular format:</span></span>

![Dane tabelaryczne usługi HDInsight HBase][img-hbase-sample-data-tabular]

<span data-ttu-id="affad-142">W bazie danych HBase (będącej implementacją BigTable) te same dane wyglądają następująco:</span><span class="sxs-lookup"><span data-stu-id="affad-142">In HBase (an implementation of BigTable), the same data looks like:</span></span>

![Dane BigTable usługi HDInsight HBase][img-hbase-sample-data-bigtable]


<span data-ttu-id="affad-144">**Aby użyć powłoki HBase**</span><span class="sxs-lookup"><span data-stu-id="affad-144">**To use the HBase shell**</span></span>

1. <span data-ttu-id="affad-145">Z poziomu bezpiecznej powłoki (SSH) uruchom następujące polecenie bazy danych HBase:</span><span class="sxs-lookup"><span data-stu-id="affad-145">From SSH, run the following HBase command:</span></span>
   
    ```bash
    hbase shell
    ```

2. <span data-ttu-id="affad-146">Utwórz bazę danych HBase z dwiema rodzinami kolumn:</span><span class="sxs-lookup"><span data-stu-id="affad-146">Create an HBase with two-column families:</span></span>

    ```hbaseshell   
    create 'Contacts', 'Personal', 'Office'
    list
    ```
3. <span data-ttu-id="affad-147">Wstaw dowolne dane:</span><span class="sxs-lookup"><span data-stu-id="affad-147">Insert some data:</span></span>
    
    ```hbaseshell   
    put 'Contacts', '1000', 'Personal:Name', 'John Dole'
    put 'Contacts', '1000', 'Personal:Phone', '1-425-000-0001'
    put 'Contacts', '1000', 'Office:Phone', '1-425-000-0002'
    put 'Contacts', '1000', 'Office:Address', '1111 San Gabriel Dr.'
    scan 'Contacts'
    ```
   
    ![Powłoka HBase HDInsight Hadoop][img-hbase-shell]
4. <span data-ttu-id="affad-149">Pobierz pojedynczy wiersz:</span><span class="sxs-lookup"><span data-stu-id="affad-149">Get a single row</span></span>
   
    ```hbaseshell
    get 'Contacts', '1000'
    ```
   
    <span data-ttu-id="affad-150">Wyświetlone zostaną te same wyniki, co w przypadku polecenia scan, ponieważ istnieje tylko jeden wiersz.</span><span class="sxs-lookup"><span data-stu-id="affad-150">You shall see the same results as using the scan command because there is only one row.</span></span>
   
    <span data-ttu-id="affad-151">Aby uzyskać więcej informacji na temat schematu tabeli bazy danych HBase, zobacz [Introduction to HBase Schema Design][hbase-schema] (Wprowadzenie do projektowania schematu bazy danych HBase).</span><span class="sxs-lookup"><span data-stu-id="affad-151">For more information about the HBase table schema, see [Introduction to HBase Schema Design][hbase-schema].</span></span> <span data-ttu-id="affad-152">Więcej poleceń bazy danych HBase można znaleźć w [Podręczniku bazy danych Apache HBase][hbase-quick-start].</span><span class="sxs-lookup"><span data-stu-id="affad-152">For more HBase commands, see [Apache HBase reference guide][hbase-quick-start].</span></span>
5. <span data-ttu-id="affad-153">Wyjdź z powłoki:</span><span class="sxs-lookup"><span data-stu-id="affad-153">Exit the shell</span></span>
   
    ```hbaseshell
    exit
    ```

<span data-ttu-id="affad-154">**Aby zbiorczo załadować dane do tabeli kontaktów HBase**</span><span class="sxs-lookup"><span data-stu-id="affad-154">**To bulk load data into the contacts HBase table**</span></span>

<span data-ttu-id="affad-155">Baza danych HBase obsługuje kilka metod ładowania danych do tabel.</span><span class="sxs-lookup"><span data-stu-id="affad-155">HBase includes several methods of loading data into tables.</span></span>  <span data-ttu-id="affad-156">Aby uzyskać więcej informacji, zobacz temat [Ładowanie zbiorcze](http://hbase.apache.org/book.html#arch.bulk.load).</span><span class="sxs-lookup"><span data-stu-id="affad-156">For more information, see [Bulk loading](http://hbase.apache.org/book.html#arch.bulk.load).</span></span>

<span data-ttu-id="affad-157">Przykładowy plik danych znajduje się w publicznym kontenerze obiektów blob, *wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt*.</span><span class="sxs-lookup"><span data-stu-id="affad-157">A sample data file can be found in a public blob container, *wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt*.</span></span>  <span data-ttu-id="affad-158">Plik danych ma następującą zawartość:</span><span class="sxs-lookup"><span data-stu-id="affad-158">The content of the data file is:</span></span>

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

<span data-ttu-id="affad-159">Opcjonalnie możesz utworzyć plik tekstowy i przesłać go na swoje konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="affad-159">You can optionally create a text file and upload the file to your own storage account.</span></span> <span data-ttu-id="affad-160">Aby uzyskać instrukcje, zobacz [Przekazywanie danych dla zadań Hadoop w usłudze HDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="affad-160">For the instructions, see [Upload data for Hadoop jobs in HDInsight][hdinsight-upload-data].</span></span>

> [!NOTE]
> <span data-ttu-id="affad-161">W tej procedurze jest używana tabela kontaktów HBase utworzona w poprzedniej procedurze.</span><span class="sxs-lookup"><span data-stu-id="affad-161">This procedure uses the Contacts HBase table you have created in the last procedure.</span></span>
> 

1. <span data-ttu-id="affad-162">Z poziomu bezpiecznej powłoki (SSH) uruchom następujące polecenie, aby przekształcić plik danych do postaci StoreFiles i zapisać go w ścieżce względnej określonej przez parametr Dimporttsv.bulk.output.</span><span class="sxs-lookup"><span data-stu-id="affad-162">From SSH, run the following command to transform the data file to StoreFiles and store at a relative path specified by Dimporttsv.bulk.output.</span></span>  <span data-ttu-id="affad-163">Jeśli jest otwarta powłoka HBase, użyj polecenia exit, aby z niej wyjść.</span><span class="sxs-lookup"><span data-stu-id="affad-163">If you are in HBase Shell, use the exit command to exit.</span></span>

    ```bash   
    hbase org.apache.hadoop.hbase.mapreduce.ImportTsv -Dimporttsv.columns="HBASE_ROW_KEY,Personal:Name,Personal:Phone,Office:Phone,Office:Address" -Dimporttsv.bulk.output="/example/data/storeDataFileOutput" Contacts wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt
    ```

2. <span data-ttu-id="affad-164">Uruchom następujące polecenie, aby przekazać dane z katalogu /example/data/storeDataFileOutput do tabeli HBase:</span><span class="sxs-lookup"><span data-stu-id="affad-164">Run the following command to upload the data from  /example/data/storeDataFileOutput to the HBase table:</span></span>
   
    ```bash
    hbase org.apache.hadoop.hbase.mapreduce.LoadIncrementalHFiles /example/data/storeDataFileOutput Contacts
    ```

3. <span data-ttu-id="affad-165">Możesz otworzyć powłokę HBase i użyć polecenia scan w celu wyświetlenia zawartości tabeli.</span><span class="sxs-lookup"><span data-stu-id="affad-165">You can open the HBase shell, and use the scan command to list the table content.</span></span>

## <a name="use-hive-to-query-hbase"></a><span data-ttu-id="affad-166">Uruchamianie zapytania bazy danych HBase przy użyciu programu Hive</span><span class="sxs-lookup"><span data-stu-id="affad-166">Use Hive to query HBase</span></span>

<span data-ttu-id="affad-167">Korzystając z programu Hive, można wykonywać zapytania dotyczące danych w tabelach HBase.</span><span class="sxs-lookup"><span data-stu-id="affad-167">You can query data in HBase tables by using Hive.</span></span> <span data-ttu-id="affad-168">W tej sekcji zostanie utworzona tabela programu Hive odwzorowująca dane w tabeli HBase, która będzie używana do wykonywania zapytań o dane w tabeli HBase.</span><span class="sxs-lookup"><span data-stu-id="affad-168">In this section, you create a Hive table that maps to the HBase table and uses it to query the data in your HBase table.</span></span>

1. <span data-ttu-id="affad-169">Otwórz program **PuTTY** i połącz się z klastrem.</span><span class="sxs-lookup"><span data-stu-id="affad-169">Open **PuTTY**, and connect to the cluster.</span></span>  <span data-ttu-id="affad-170">Zapoznaj się z instrukcjami w poprzedniej procedurze.</span><span class="sxs-lookup"><span data-stu-id="affad-170">See the instructions in the previous procedure.</span></span>
2. <span data-ttu-id="affad-171">W sesji SSH wpisz następujące polecenie, aby uruchomić usługę Beeline:</span><span class="sxs-lookup"><span data-stu-id="affad-171">From the SSH session, use the following command to start Beeline:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    <span data-ttu-id="affad-172">Aby uzyskać więcej informacji o usłudze Beeline, zobacz [Używanie technologii Hive z usługą Hadoop w usłudze HDInsight z usługą Beeline](hdinsight-hadoop-use-hive-beeline.md).</span><span class="sxs-lookup"><span data-stu-id="affad-172">For more information about Beeline, see [Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md).</span></span>
       
3. <span data-ttu-id="affad-173">Uruchom poniższy skrypt HiveQL, aby utworzyć tabelę programu Hive, która mapuje dane na tabelę HBase.</span><span class="sxs-lookup"><span data-stu-id="affad-173">Run the following HiveQL script  to create a Hive table that maps to the HBase table.</span></span> <span data-ttu-id="affad-174">Upewnij się, że utworzono wspomnianą wcześniej w tym samouczku tabelę przykładową, używając powłoki HBase przed uruchomieniem tej instrukcji.</span><span class="sxs-lookup"><span data-stu-id="affad-174">Make sure that you have created the sample table referenced earlier in this tutorial by using the HBase shell before you run this statement.</span></span>

    ```hiveql   
    CREATE EXTERNAL TABLE hbasecontacts(rowkey STRING, name STRING, homephone STRING, officephone STRING, officeaddress STRING)
    STORED BY 'org.apache.hadoop.hive.hbase.HBaseStorageHandler'
    WITH SERDEPROPERTIES ('hbase.columns.mapping' = ':key,Personal:Name,Personal:Phone,Office:Phone,Office:Address')
    TBLPROPERTIES ('hbase.table.name' = 'Contacts');
    ```

4. <span data-ttu-id="affad-175">Uruchom poniższy skrypt HiveQL, aby wykonać zapytanie o dane w tabeli HBase:</span><span class="sxs-lookup"><span data-stu-id="affad-175">Run the following HiveQL script to query the data in the HBase table:</span></span>

    ```hiveql   
    SELECT count(rowkey) FROM hbasecontacts;
    ```

## <a name="use-hbase-rest-apis-using-curl"></a><span data-ttu-id="affad-176">Korzystanie z interfejsów API REST HBase przy użyciu programu Curl</span><span class="sxs-lookup"><span data-stu-id="affad-176">Use HBase REST APIs using Curl</span></span>

<span data-ttu-id="affad-177">Interfejs API REST jest zabezpieczony za pomocą [uwierzytelniania podstawowego](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="affad-177">The REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="affad-178">Należy zawsze tworzyć żądania przy użyciu protokołu HTTPS (HTTP Secure), aby mieć pewność, że poświadczenia są bezpiecznie wysyłane do serwera.</span><span class="sxs-lookup"><span data-stu-id="affad-178">You shall always make requests by using Secure HTTP (HTTPS) to help ensure that your credentials are securely sent to the server.</span></span>

2. <span data-ttu-id="affad-179">Użyj następującego polecenia, aby wyświetlić listę istniejących tabel HBase:</span><span class="sxs-lookup"><span data-stu-id="affad-179">Use the following command to list the existing HBase tables:</span></span>

    ```bash
    curl -u <UserName>:<Password> \
    -G https://<ClusterName>.azurehdinsight.net/hbaserest/
    ```

3. <span data-ttu-id="affad-180">Użyj następującego polecenia, aby utworzyć nową tabelę HBase z dwiema rodzinami kolumn:</span><span class="sxs-lookup"><span data-stu-id="affad-180">Use the following command to create a new HBase table with two-column families:</span></span>

    ```bash   
    curl -u <UserName>:<Password> \
    -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/schema" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -d "{\"@name\":\"Contact1\",\"ColumnSchema\":[{\"name\":\"Personal\"},{\"name\":\"Office\"}]}" \
    -v
    ```

    <span data-ttu-id="affad-181">Schemat jest podany w formacie JSon.</span><span class="sxs-lookup"><span data-stu-id="affad-181">The schema is provided in the JSon format.</span></span>
4. <span data-ttu-id="affad-182">Użyj następującego polecenia, aby wstawić dane:</span><span class="sxs-lookup"><span data-stu-id="affad-182">Use the following command to insert some data:</span></span>

    ```bash   
    curl -u <UserName>:<Password> \
    -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/false-row-key" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -d "{\"Row\":[{\"key\":\"MTAwMA==\",\"Cell\": [{\"column\":\"UGVyc29uYWw6TmFtZQ==\", \"$\":\"Sm9obiBEb2xl\"}]}]}" \
    -v
    ```
   
    <span data-ttu-id="affad-183">Należy zakodować wartości określone w przełączniku -d w formacie base64.</span><span class="sxs-lookup"><span data-stu-id="affad-183">You must base64 encode the values specified in the -d switch.</span></span> <span data-ttu-id="affad-184">W przykładzie:</span><span class="sxs-lookup"><span data-stu-id="affad-184">In the example:</span></span>
   
   * <span data-ttu-id="affad-185">MTAwMA==: 1000</span><span class="sxs-lookup"><span data-stu-id="affad-185">MTAwMA==: 1000</span></span>
   * <span data-ttu-id="affad-186">UGVyc29uYWw6TmFtZQ==: Personal:Name</span><span class="sxs-lookup"><span data-stu-id="affad-186">UGVyc29uYWw6TmFtZQ==: Personal:Name</span></span>
   * <span data-ttu-id="affad-187">Sm9obiBEb2xl: John Dole</span><span class="sxs-lookup"><span data-stu-id="affad-187">Sm9obiBEb2xl: John Dole</span></span>
     
     <span data-ttu-id="affad-188">[false-row-key](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/rest/package-summary.html#operation_cell_store_single) umożliwia wstawianie wielu wartości (w partiach).</span><span class="sxs-lookup"><span data-stu-id="affad-188">[false-row-key](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/rest/package-summary.html#operation_cell_store_single) allows you to insert multiple (batched) values.</span></span>
5. <span data-ttu-id="affad-189">Użyj następującego polecenia, aby pobrać wiersz:</span><span class="sxs-lookup"><span data-stu-id="affad-189">Use the following command to get a row:</span></span>
   
    ```bash 
    curl -u <UserName>:<Password> \
    -X GET "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/1000" \
    -H "Accept: application/json" \
    -v
    ```

<span data-ttu-id="affad-190">Aby uzyskać więcej informacji o interfejsie Rest HBase, zobacz [Apache HBase Reference Guide](https://hbase.apache.org/book.html#_rest) (Podręcznik referencyjny Apache HBase).</span><span class="sxs-lookup"><span data-stu-id="affad-190">For more information about HBase Rest, see [Apache HBase Reference Guide](https://hbase.apache.org/book.html#_rest).</span></span>

> [!NOTE]
> <span data-ttu-id="affad-191">Platforma Thrift nie jest obsługiwana przez bazę danych HBase w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="affad-191">Thrift is not supported by HBase in HDInsight.</span></span>
>
> <span data-ttu-id="affad-192">Używając programu Curl lub innego połączenia REST z usługą WebHCat, należy uwierzytelnić żądania, podając nazwę użytkownika i hasło administratora klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="affad-192">When using Curl or any other REST communication with WebHCat, you must authenticate the requests by providing the user name and password for the HDInsight cluster administrator.</span></span> <span data-ttu-id="affad-193">Należy również użyć nazwy klastra jako części identyfikatora URI stosowanego przy wysyłaniu żądań do serwera:</span><span class="sxs-lookup"><span data-stu-id="affad-193">You must also use the cluster name as part of the Uniform Resource Identifier (URI) used to send the requests to the server:</span></span>
> 
>   
>        curl -u <UserName>:<Password> \
>        -G https://<ClusterName>.azurehdinsight.net/templeton/v1/status
>   
>    <span data-ttu-id="affad-194">Powinna zostać zwrócona odpowiedź podobna do następującej:</span><span class="sxs-lookup"><span data-stu-id="affad-194">You should receive a response similar to the following response:</span></span>
>   
>        {"status":"ok","version":"v1"}
   


## <a name="check-cluster-status"></a><span data-ttu-id="affad-195">Sprawdzanie stanu klastra</span><span class="sxs-lookup"><span data-stu-id="affad-195">Check cluster status</span></span>
<span data-ttu-id="affad-196">Baza danych HBase w usłudze HDInsight jest dostarczana z interfejsem użytkownika sieci Web służącym do monitorowania klastrów.</span><span class="sxs-lookup"><span data-stu-id="affad-196">HBase in HDInsight ships with a Web UI for monitoring clusters.</span></span> <span data-ttu-id="affad-197">Za pośrednictwem interfejsu użytkownika sieci Web możesz przesyłać żądania dotyczące statystyk lub informacji o regionach.</span><span class="sxs-lookup"><span data-stu-id="affad-197">Using the Web UI, you can request statistics or information about regions.</span></span>

<span data-ttu-id="affad-198">**Aby uzyskać dostęp do głównego interfejsu użytkownika HBase**</span><span class="sxs-lookup"><span data-stu-id="affad-198">**To access the HBase Master UI**</span></span>

1. <span data-ttu-id="affad-199">Zaloguj się do internetowego interfejsu użytkownika systemu Ambari pod adresem https://&lt;nazwa_klastra>.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="affad-199">Sign into the the Ambari Web UI at https://&lt;Clustername>.azurehdinsight.net.</span></span>
2. <span data-ttu-id="affad-200">W menu po lewej kliknij pozycję **HBase**.</span><span class="sxs-lookup"><span data-stu-id="affad-200">Click **HBase** from the left menu.</span></span>
3. <span data-ttu-id="affad-201">Na górze strony kliknij pozycję **Szybkie linki**, wskaż aktywny link węzła dozorcy, a następnie kliknij pozycję **Główny interfejs użytkownika bazy danych HBase**.</span><span class="sxs-lookup"><span data-stu-id="affad-201">Click **Quick links** on the top of the page, point to the active Zookeeper node link, and then click **HBase Master UI**.</span></span>  <span data-ttu-id="affad-202">Interfejs użytkownika zostanie otwarty w innej karcie przeglądarki:</span><span class="sxs-lookup"><span data-stu-id="affad-202">The UI is opened in another browser tab:</span></span>

  ![Główny interfejs użytkownika HDInsight HBase](./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-hmaster-ui.png)

  <span data-ttu-id="affad-204">Główny interfejs użytkownika HBase zawiera następujące sekcje:</span><span class="sxs-lookup"><span data-stu-id="affad-204">The HBase Master UI contains the following sections:</span></span>

  - <span data-ttu-id="affad-205">serwery regionów</span><span class="sxs-lookup"><span data-stu-id="affad-205">region servers</span></span>
  - <span data-ttu-id="affad-206">wzorce kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="affad-206">backup masters</span></span>
  - <span data-ttu-id="affad-207">tabele</span><span class="sxs-lookup"><span data-stu-id="affad-207">tables</span></span>
  - <span data-ttu-id="affad-208">zadania</span><span class="sxs-lookup"><span data-stu-id="affad-208">tasks</span></span>
  - <span data-ttu-id="affad-209">atrybuty oprogramowania</span><span class="sxs-lookup"><span data-stu-id="affad-209">software attributes</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="affad-210">Usuwanie klastra</span><span class="sxs-lookup"><span data-stu-id="affad-210">Delete the cluster</span></span>
<span data-ttu-id="affad-211">Aby uniknąć niespójności, zaleca się wyłączenie tabel HBase przed usunięciem klastra.</span><span class="sxs-lookup"><span data-stu-id="affad-211">To avoid inconsistencies, we recommend that you disable the HBase tables before you delete the cluster.</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="affad-212">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="affad-212">Troubleshoot</span></span>

<span data-ttu-id="affad-213">W razie problemów podczas tworzenia klastrów usługi HDInsight zapoznaj się z [wymaganiami dotyczącymi kontroli dostępu](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="affad-213">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="affad-214">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="affad-214">Next steps</span></span>
<span data-ttu-id="affad-215">W tym artykule pokazano, jak utworzyć klaster HBase i tabele oraz jak wyświetlać dane w tych tabelach z poziomu powłoki HBase.</span><span class="sxs-lookup"><span data-stu-id="affad-215">In this article, you learned how to create an HBase cluster and how to create tables and view the data in those tables from the HBase shell.</span></span> <span data-ttu-id="affad-216">Przedstawiono również sposób wykonywania zapytań programu Hive względem danych w tabelach HBase oraz korzystania z interfejsów API REST HBase w języku C# w celu tworzenia tabel HBase i pobierania danych z tabeli.</span><span class="sxs-lookup"><span data-stu-id="affad-216">You also learned how to use a Hive query on data in HBase tables and how to use the HBase C# REST APIs to create an HBase table and retrieve data from the table.</span></span>

<span data-ttu-id="affad-217">Aby dowiedzieć się więcej, zobacz:</span><span class="sxs-lookup"><span data-stu-id="affad-217">To learn more, see:</span></span>

* <span data-ttu-id="affad-218">[Przegląd bazy danych HBase w usłudze HDInsight][hdinsight-hbase-overview]: HBase jest bazą danych Apache NoSQL typu open source opartą na platformie Hadoop, która zapewnia dostęp losowy i wysoki poziom spójności w przypadku dużych ilości danych z częściową strukturą i bez struktury.</span><span class="sxs-lookup"><span data-stu-id="affad-218">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>

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
