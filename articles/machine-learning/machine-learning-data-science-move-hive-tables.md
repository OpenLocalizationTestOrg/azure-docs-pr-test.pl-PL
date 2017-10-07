---
title: "aaaCreate Hive tabel i ładowanie danych z magazynu obiektów Blob platformy Azure | Dokumentacja firmy Microsoft"
description: "Tworzenie tabel programu Hive i załadować dane w tabelach toohive obiektów blob"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: cff9280d-18ce-4b66-a54f-19f358d1ad90
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 09622972bcac31c2971858393a8340f24e4b7390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-hive-tables-and-load-data-from-azure-blob-storage"></a><span data-ttu-id="3b81f-103">Tworzenie tabel programu Hive i ładowanie danych z magazynu obiektów Blob Azure</span><span class="sxs-lookup"><span data-stu-id="3b81f-103">Create Hive tables and load data from Azure Blob Storage</span></span>
<span data-ttu-id="3b81f-104">W tym temacie przedstawiono ogólne zapytań Hive, które Tworzenie tabel programu Hive i ładowanie danych z magazynu obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3b81f-104">This topic presents generic Hive queries that create Hive tables and load data from Azure blob storage.</span></span> <span data-ttu-id="3b81f-105">Instrukcje dostępne są również na partycje tabele programu Hive i przy użyciu hello zoptymalizowanych pod kątem wiersza kolumnowy (ORC) formatowania tooimprove kwerendy wydajności.</span><span class="sxs-lookup"><span data-stu-id="3b81f-105">Some guidance is also provided on partitioning Hive tables and on using hello Optimized Row Columnar (ORC) formatting tooimprove query performance.</span></span>

<span data-ttu-id="3b81f-106">To **menu** łączy tootopics, które opisują sposób tooingest danych w środowisku docelowym, gdzie hello dane mogą być przechowywane i przetwarzane podczas hello zespołu danych nauki procesu (TDSP).</span><span class="sxs-lookup"><span data-stu-id="3b81f-106">This **menu** links tootopics that describe how tooingest data into target environments where hello data can be stored and processed during hello Team Data Science Process (TDSP).</span></span>

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="3b81f-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3b81f-107">Prerequisites</span></span>
<span data-ttu-id="3b81f-108">W tym artykule przyjęto założenie, że masz:</span><span class="sxs-lookup"><span data-stu-id="3b81f-108">This article assumes that you have:</span></span>

* <span data-ttu-id="3b81f-109">Utworzone konto magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3b81f-109">Created an Azure storage account.</span></span> <span data-ttu-id="3b81f-110">Aby uzyskać instrukcje, zobacz [kont magazynu Azure o](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="3b81f-110">If you need instructions, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
* <span data-ttu-id="3b81f-111">Zainicjowano obsługę administracyjną dostosowane klastra usługi Hadoop z hello usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3b81f-111">Provisioned a customized Hadoop cluster with hello HDInsight service.</span></span>  <span data-ttu-id="3b81f-112">Aby uzyskać instrukcje, zobacz [dostosować Azure HDInsight Hadoop clusters zaawansowana analityka](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="3b81f-112">If you need instructions, see [Customize Azure HDInsight Hadoop clusters for advanced analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="3b81f-113">Klastra toohello włączone dostępu zdalnego, zalogowany i otworzyć konsolę wiersza polecenia hello Hadoop.</span><span class="sxs-lookup"><span data-stu-id="3b81f-113">Enabled remote access toohello cluster, logged in, and opened hello Hadoop Command-Line console.</span></span> <span data-ttu-id="3b81f-114">Aby uzyskać instrukcje, zobacz [hello dostępu Head węzeł z klastra usługi Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="3b81f-114">If you need instructions, see [Access hello Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>

## <a name="upload-data-tooazure-blob-storage"></a><span data-ttu-id="3b81f-115">Przekazywanie danych tooAzure obiektu blob magazynu</span><span class="sxs-lookup"><span data-stu-id="3b81f-115">Upload data tooAzure blob storage</span></span>
<span data-ttu-id="3b81f-116">Jeśli utworzono maszynę wirtualną platformy Azure, wykonując instrukcje hello podane w [Konfigurowanie maszyny wirtualnej platformy Azure, zaawansowana analityka](machine-learning-data-science-setup-virtual-machine.md), ten plik skryptu powinien być pobrany toohello *C:\\ Użytkownicy\\\<nazwy użytkownika\>\\dokumenty\\skryptów nauki danych* katalogu hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3b81f-116">If you created an Azure virtual machine by following hello instructions provided in [Set up an Azure virtual machine for advanced analytics](machine-learning-data-science-setup-virtual-machine.md), this script file should have been downloaded toohello *C:\\Users\\\<user name\>\\Documents\\Data Science Scripts* directory on hello virtual machine.</span></span> <span data-ttu-id="3b81f-117">Te zapytania Hive wymagają tylko należy podłączyć własny schemat danych i konfiguracji magazynu obiektów blob platformy Azure w toobe odpowiednich pól hello jest gotowy do przesłania.</span><span class="sxs-lookup"><span data-stu-id="3b81f-117">These Hive queries only require that you plug in your own data schema and Azure blob storage configuration in hello appropriate fields toobe ready for submission.</span></span>

<span data-ttu-id="3b81f-118">Przyjęto założenie, że dane hello tabele programu Hive są w **nieskompresowanych** tabelarycznej i że hello dane zostały przekazane toohello domyślne (lub tooan dodatkowe) kontenera konta magazynu hello używane przez klaster Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="3b81f-118">We assume that hello data for Hive tables is in an **uncompressed** tabular format, and that hello data has been uploaded toohello default (or tooan additional) container of hello storage account used by hello Hadoop cluster.</span></span>

<span data-ttu-id="3b81f-119">Jeśli chcesz, aby toopractice na powitania **NYC taksówki podróży danych**, musisz:</span><span class="sxs-lookup"><span data-stu-id="3b81f-119">If you want toopractice on hello **NYC Taxi Trip Data**, you need to:</span></span>

* <span data-ttu-id="3b81f-120">**Pobierz** hello 24 [danych podróży taksówki NYC](http://www.andresmh.com/nyctaxitrips) plików (12 pliki podróży i pliki taryfy 12),</span><span class="sxs-lookup"><span data-stu-id="3b81f-120">**download** hello 24 [NYC Taxi Trip Data](http://www.andresmh.com/nyctaxitrips) files (12 Trip files and 12 Fare files),</span></span>
* <span data-ttu-id="3b81f-121">**Rozpakuj** wszystkie pliki w pliki CSV, a następnie</span><span class="sxs-lookup"><span data-stu-id="3b81f-121">**unzip** all files into .csv files, and then</span></span>
* <span data-ttu-id="3b81f-122">**Przekaż** ich toohello domyślne lub odpowiedniego kontenera hello kontem magazynu platformy Azure, który został utworzony przez hello procedury opisane w hello [dostosować Azure HDInsight Hadoop clusters zaawansowane procesu analizy i technologii ](machine-learning-data-science-customize-hadoop-cluster.md) tematu.</span><span class="sxs-lookup"><span data-stu-id="3b81f-122">**upload** them toohello default (or appropriate container) of hello Azure storage account that was created by hello procedure outlined in hello [Customize Azure HDInsight Hadoop clusters for Advanced Analytics Process and Technology](machine-learning-data-science-customize-hadoop-cluster.md) topic.</span></span> <span data-ttu-id="3b81f-123">Witaj procesu tooupload hello CSV pliki toohello domyślnego kontenera na koncie magazynu hello znajduje się na tym [strony](machine-learning-data-science-process-hive-walkthrough.md#upload).</span><span class="sxs-lookup"><span data-stu-id="3b81f-123">hello process tooupload hello .csv files toohello default container on hello storage account can be found on this [page](machine-learning-data-science-process-hive-walkthrough.md#upload).</span></span>

## <span data-ttu-id="3b81f-124"><a name="submit"></a>Jak toosubmit zapytań programu Hive</span><span class="sxs-lookup"><span data-stu-id="3b81f-124"><a name="submit"></a>How toosubmit Hive queries</span></span>
<span data-ttu-id="3b81f-125">Można przesłać zapytań programu hive za pomocą:</span><span class="sxs-lookup"><span data-stu-id="3b81f-125">Hive queries can be submitted by using:</span></span>

1. [<span data-ttu-id="3b81f-126">Wysyłanie zapytań programu Hive za pomocą wiersza polecenia platformy Hadoop w headnode klastra usługi Hadoop</span><span class="sxs-lookup"><span data-stu-id="3b81f-126">Submit Hive queries through Hadoop Command Line in headnode of Hadoop cluster</span></span>](#headnode)
2. [<span data-ttu-id="3b81f-127">Wysyłanie zapytań programu Hive z hello Edytor Hive</span><span class="sxs-lookup"><span data-stu-id="3b81f-127">Submit Hive queries with hello Hive Editor</span></span>](#hive-editor)
3. [<span data-ttu-id="3b81f-128">Wysyłanie zapytań programu Hive z poleceń programu PowerShell Azure</span><span class="sxs-lookup"><span data-stu-id="3b81f-128">Submit Hive queries with Azure PowerShell Commands</span></span>](#ps)

<span data-ttu-id="3b81f-129">Zapytania hive są przypominającego SQL.</span><span class="sxs-lookup"><span data-stu-id="3b81f-129">Hive queries are SQL-like.</span></span> <span data-ttu-id="3b81f-130">Jeśli znasz SQL, może się okazać hello [Hive arkusza Cheat użytkowników SQL](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf) przydatne.</span><span class="sxs-lookup"><span data-stu-id="3b81f-130">If you are familiar with SQL, you may find hello [Hive for SQL Users Cheat Sheet](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf) useful.</span></span>

<span data-ttu-id="3b81f-131">Podczas składania zapytań programu Hive, można też kontrolować hello miejsce docelowe danych wyjściowych hello z zapytań programu Hive, czy jest na powitania ekranu lub tooa pliku lokalnego dla węzła głównego hello lub tooan obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3b81f-131">When submitting a Hive query, you can also control hello destination of hello output from Hive queries, whether it be on hello screen or tooa local file on hello head node or tooan Azure blob.</span></span>

### <span data-ttu-id="3b81f-132"><a name="headnode"></a> 1. Wysyłanie zapytań programu Hive za pomocą wiersza polecenia platformy Hadoop w headnode klastra usługi Hadoop</span><span class="sxs-lookup"><span data-stu-id="3b81f-132"><a name="headnode"></a> 1. Submit Hive queries through Hadoop Command Line in headnode of Hadoop cluster</span></span>
<span data-ttu-id="3b81f-133">Jeśli hello Hive zapytanie jest złożony, przesłanie bezpośrednio w hello węzła głównego klastra usługi Hadoop hello zwykle prowadzi Włącz toofaster wokół niż przesłania go w edytorze Hive lub skryptów programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3b81f-133">If hello Hive query is complex, submitting it directly in hello head node of hello Hadoop cluster typically leads toofaster turn around than submitting it with a Hive Editor or Azure PowerShell scripts.</span></span>

<span data-ttu-id="3b81f-134">Zaloguj się za toohello węzła głównego klastra usługi Hadoop hello, otwórz hello wiersza polecenia usługi Hadoop na pulpicie hello hello węzła głównego i wprowadź polecenie `cd %hive_home%\bin`.</span><span class="sxs-lookup"><span data-stu-id="3b81f-134">Log in toohello head node of hello Hadoop cluster, open hello Hadoop Command Line on hello desktop of hello head node, and enter command `cd %hive_home%\bin`.</span></span>

<span data-ttu-id="3b81f-135">Masz zapytań programu Hive toosubmit trzy sposoby w hello Hadoop wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="3b81f-135">You have three ways toosubmit Hive queries in hello Hadoop Command Line:</span></span>

* <span data-ttu-id="3b81f-136">bezpośrednio</span><span class="sxs-lookup"><span data-stu-id="3b81f-136">directly</span></span>
* <span data-ttu-id="3b81f-137">przy użyciu plików .hql</span><span class="sxs-lookup"><span data-stu-id="3b81f-137">using .hql files</span></span>
* <span data-ttu-id="3b81f-138">z hello Hive konsoli poleceń</span><span class="sxs-lookup"><span data-stu-id="3b81f-138">with hello Hive command console</span></span>

#### <a name="submit-hive-queries-directly-in-hadoop-command-line"></a><span data-ttu-id="3b81f-139">Wysyłanie zapytań programu Hive bezpośrednio w Hadoop wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="3b81f-139">Submit Hive queries directly in Hadoop Command Line.</span></span>
<span data-ttu-id="3b81f-140">Możesz uruchomić polecenie, takie jak `hive -e "<your hive query>;` toosubmit prostych zapytań programu Hive bezpośrednio w Hadoop wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="3b81f-140">You can run command like `hive -e "<your hive query>;` toosubmit simple Hive queries directly in Hadoop Command Line.</span></span> <span data-ttu-id="3b81f-141">Oto przykład, gdy zawiera pole hello red hello polecenia, który przesyła zapytanie Hive hello i hello zielone pole zawiera hello dane wyjściowe zapytań Hive hello.</span><span class="sxs-lookup"><span data-stu-id="3b81f-141">Here is an example, where hello red box outlines hello command that submits hello Hive query, and hello green box outlines hello output from hello Hive query.</span></span>

![Tworzenie obszaru roboczego](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-1.png)

#### <a name="submit-hive-queries-in-hql-files"></a><span data-ttu-id="3b81f-143">Wysyłanie zapytań programu Hive w plikach .hql</span><span class="sxs-lookup"><span data-stu-id="3b81f-143">Submit Hive queries in .hql files</span></span>
<span data-ttu-id="3b81f-144">Jeśli zapytanie Hive hello jest bardziej skomplikowany i ma wiele wierszy, edytowanie zapytań w wierszu polecenia lub konsoli poleceń gałęzi nie jest praktyczne.</span><span class="sxs-lookup"><span data-stu-id="3b81f-144">When hello Hive query is more complicated and has multiple lines, editing queries in command line or Hive command console is not practical.</span></span> <span data-ttu-id="3b81f-145">Alternatywą jest toouse edytora tekstu, w węźle głównym hello hello Hadoop klastra toosave hello zapytań programu Hive w pliku .hql w katalogu lokalnym hello węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="3b81f-145">An alternative is toouse a text editor in hello head node of hello Hadoop cluster toosave hello Hive queries in a .hql file in a local directory of hello head node.</span></span> <span data-ttu-id="3b81f-146">Następnie hello zapytanie Hive w pliku .hql hello można przesłać za pomocą hello `-f` argument w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="3b81f-146">Then hello Hive query in hello .hql file can be submitted by using hello `-f` argument as follows:</span></span>

    hive -f "<path toohello .hql file>"

![Tworzenie obszaru roboczego](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-3.png)

<span data-ttu-id="3b81f-148">**Pomiń postępu stan ekranu drukowania zapytań Hive**</span><span class="sxs-lookup"><span data-stu-id="3b81f-148">**Suppress progress status screen print of Hive queries**</span></span>

<span data-ttu-id="3b81f-149">Domyślnie po wysłaniu zapytania Hive w wierszu polecenia Hadoop hello postęp zadania mapy/Zmniejsz hello jest drukowany na ekranie.</span><span class="sxs-lookup"><span data-stu-id="3b81f-149">By default, after Hive query is submitted in Hadoop Command Line, hello progress of hello Map/Reduce job is printed out on screen.</span></span> <span data-ttu-id="3b81f-150">toosuppress hello drukowania ekran postępu zadania mapy/Zmniejsz hello, można użyć argumentu `-S` ("S" wielkimi literami) w hello wiersza polecenia w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="3b81f-150">toosuppress hello screen print of hello Map/Reduce job progress, you can use an argument `-S` ("S" in upper case) in hello command line as follows:</span></span>

    hive -S -f "<path toohello .hql file>"
<span data-ttu-id="3b81f-151">.</span><span class="sxs-lookup"><span data-stu-id="3b81f-151">.</span></span>    <span data-ttu-id="3b81f-152">-S -e hive "<Hive queries>"</span><span class="sxs-lookup"><span data-stu-id="3b81f-152">hive -S -e "<Hive queries>"</span></span>

#### <a name="submit-hive-queries-in-hive-command-console"></a><span data-ttu-id="3b81f-153">Wysyłanie zapytań programu Hive z konsoli poleceń Hive.</span><span class="sxs-lookup"><span data-stu-id="3b81f-153">Submit Hive queries in Hive command console.</span></span>
<span data-ttu-id="3b81f-154">Można również najpierw wprowadzić konsoli poleceń hello Hive, uruchamiając polecenie `hive` w wierszu polecenia Hadoop, a następnie wysyłanie zapytań programu Hive z konsoli poleceń Hive.</span><span class="sxs-lookup"><span data-stu-id="3b81f-154">You can also first enter hello Hive command console by running command `hive` in Hadoop Command Line, and then submit Hive queries in Hive command console.</span></span> <span data-ttu-id="3b81f-155">Oto przykład.</span><span class="sxs-lookup"><span data-stu-id="3b81f-155">Here is an example.</span></span> <span data-ttu-id="3b81f-156">W tym przykładzie hello dwa pola czerwone wyróżnienie hello polecenia używane tooenter hello Hive konsoli poleceń i hello przesłane w konsoli polecenie gałęzi odpowiednio zapytanie Hive.</span><span class="sxs-lookup"><span data-stu-id="3b81f-156">In this example, hello two red boxes highlight hello commands used tooenter hello Hive command console, and hello Hive query submitted in Hive command console, respectively.</span></span> <span data-ttu-id="3b81f-157">wyróżnione hello dane wyjściowe zapytań Hive hello Hello zielony.</span><span class="sxs-lookup"><span data-stu-id="3b81f-157">hello green box highlights hello output from hello Hive query.</span></span>

![Tworzenie obszaru roboczego](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-2.png)

<span data-ttu-id="3b81f-159">Witaj w poprzednich przykładach output bezpośrednio wyników zapytania Hive hello na ekranie.</span><span class="sxs-lookup"><span data-stu-id="3b81f-159">hello previous examples directly output hello Hive query results on screen.</span></span> <span data-ttu-id="3b81f-160">Można również napisać pliku lokalnego tooa dane wyjściowe hello na powitania węzła głównego lub tooan obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3b81f-160">You can also write hello output tooa local file on hello head node, or tooan Azure blob.</span></span> <span data-ttu-id="3b81f-161">Następnie należy użyć innych narzędzi toofurther analizować dane wyjściowe hello zapytań programu Hive.</span><span class="sxs-lookup"><span data-stu-id="3b81f-161">Then, you can use other tools toofurther analyze hello output of Hive queries.</span></span>

<span data-ttu-id="3b81f-162">**Dane wyjściowe pliku lokalnego tooa wyników zapytania Hive.**</span><span class="sxs-lookup"><span data-stu-id="3b81f-162">**Output Hive query results tooa local file.**</span></span>
<span data-ttu-id="3b81f-163">toooutput Hive zapytania wyniki tooa katalogu lokalnego na powitania węzła głównego, masz zapytanie Hive hello toosubmit w hello wiersza polecenia platformy Hadoop w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="3b81f-163">toooutput Hive query results tooa local directory on hello head node, you have toosubmit hello Hive query in hello Hadoop Command Line as follows:</span></span>

    hive -e "<hive query>" > <local path in hello head node>

<span data-ttu-id="3b81f-164">W hello poniższy przykład, dane wyjściowe hello zapytania Hive są zapisywane do pliku `hivequeryoutput.txt` w katalogu `C:\apps\temp`.</span><span class="sxs-lookup"><span data-stu-id="3b81f-164">In hello following example, hello output of Hive query is written into a file `hivequeryoutput.txt` in directory `C:\apps\temp`.</span></span>

![Tworzenie obszaru roboczego](./media/machine-learning-data-science-move-hive-tables/output-hive-results-1.png)

<span data-ttu-id="3b81f-166">**Dane wyjściowe tooan wyników zapytania Hive obiektów blob platformy Azure**</span><span class="sxs-lookup"><span data-stu-id="3b81f-166">**Output Hive query results tooan Azure blob**</span></span>

<span data-ttu-id="3b81f-167">Można również output hello Hive zapytania wyniki tooan obiektów blob platformy Azure w kontenerze domyślna hello hello klastra usługi Hadoop.</span><span class="sxs-lookup"><span data-stu-id="3b81f-167">You can also output hello Hive query results tooan Azure blob, within hello default container of hello Hadoop cluster.</span></span> <span data-ttu-id="3b81f-168">Zapytanie Hive Hello tego przebiega następująco:</span><span class="sxs-lookup"><span data-stu-id="3b81f-168">hello Hive query for this is as follows:</span></span>

    insert overwrite directory wasb:///<directory within hello default container> <select clause from ...>

<span data-ttu-id="3b81f-169">W hello poniższy przykład, dane wyjściowe hello zapytania Hive są zapisywane katalogu obiektu blob tooa `queryoutputdir` w kontenerze domyślna hello hello klastra usługi Hadoop.</span><span class="sxs-lookup"><span data-stu-id="3b81f-169">In hello following example, hello output of Hive query is written tooa blob directory `queryoutputdir` within hello default container of hello Hadoop cluster.</span></span> <span data-ttu-id="3b81f-170">W tym miejscu wystarczy tylko nazwę katalogu hello tooprovide, bez hello nazwa obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="3b81f-170">Here, you only need tooprovide hello directory name, without hello blob name.</span></span> <span data-ttu-id="3b81f-171">Zostanie zgłoszony błąd, jeśli zostaną podane nazwy usługi directory i obiektów blob, takich jak `wasb:///queryoutputdir/queryoutput.txt`.</span><span class="sxs-lookup"><span data-stu-id="3b81f-171">An error is thrown if you provide both directory and blob names, such as `wasb:///queryoutputdir/queryoutput.txt`.</span></span>

![Tworzenie obszaru roboczego](./media/machine-learning-data-science-move-hive-tables/output-hive-results-2.png)

<span data-ttu-id="3b81f-173">Po otwarciu hello domyślny kontener hello klastra platformy Hadoop za pomocą Eksploratora usługi Storage Azure widać hello dane wyjściowe zapytań Hive hello pokazane na powitania po rysunku.</span><span class="sxs-lookup"><span data-stu-id="3b81f-173">If you open hello default container of hello Hadoop cluster using Azure Storage Explorer, you can see hello output of hello Hive query as shown in hello following figure.</span></span> <span data-ttu-id="3b81f-174">Możesz zastosować hello blob hello pobrać tooonly filtru (wyróżniony przez czerwonym prostokątem) z określonej litery w nazwach.</span><span class="sxs-lookup"><span data-stu-id="3b81f-174">You can apply hello filter (highlighted by red box) tooonly retrieve hello blob with specified letters in names.</span></span>

![Tworzenie obszaru roboczego](./media/machine-learning-data-science-move-hive-tables/output-hive-results-3.png)

### <span data-ttu-id="3b81f-176"><a name="hive-editor"></a> 2. Wysyłanie zapytań programu Hive z hello Edytor Hive</span><span class="sxs-lookup"><span data-stu-id="3b81f-176"><a name="hive-editor"></a> 2. Submit Hive queries with hello Hive Editor</span></span>
<span data-ttu-id="3b81f-177">Umożliwia także hello zapytania konsoli (Edytor Hive), wprowadzając adres URL w postaci hello *https://&#60; Nazwa klastra Hadoop >.azurehdinsight.net/Home/HiveEditor* w przeglądarce sieci web.</span><span class="sxs-lookup"><span data-stu-id="3b81f-177">You can also use hello Query Console (Hive Editor) by entering a URL of hello form *https://&#60;Hadoop cluster name>.azurehdinsight.net/Home/HiveEditor* into a web browser.</span></span> <span data-ttu-id="3b81f-178">Musi być zalogowany Zobacz hello tej konsoli i dlatego potrzebne są poświadczenia klastra usługi Hadoop.</span><span class="sxs-lookup"><span data-stu-id="3b81f-178">You must be logged in hello see this console and so you need your Hadoop cluster credentials here.</span></span>

### <span data-ttu-id="3b81f-179"><a name="ps"></a> 3. Wysyłanie zapytań programu Hive z poleceń programu PowerShell Azure</span><span class="sxs-lookup"><span data-stu-id="3b81f-179"><a name="ps"></a> 3. Submit Hive queries with Azure PowerShell Commands</span></span>
<span data-ttu-id="3b81f-180">Umożliwia także zapytań Hive toosubmit środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3b81f-180">You can also use PowerShell toosubmit Hive queries.</span></span> <span data-ttu-id="3b81f-181">Aby uzyskać instrukcje, zobacz [zadania Hive przesyłania przy użyciu programu PowerShell](../hdinsight/hdinsight-hadoop-use-hive-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="3b81f-181">For instructions, see [Submit Hive jobs using PowerShell](../hdinsight/hdinsight-hadoop-use-hive-powershell.md).</span></span>

## <span data-ttu-id="3b81f-182"><a name="create-tables"></a>Utwórz gałąź bazy danych i tabel</span><span class="sxs-lookup"><span data-stu-id="3b81f-182"><a name="create-tables"></a>Create Hive database and tables</span></span>
<span data-ttu-id="3b81f-183">Witaj zapytań programu Hive są udostępniane w hello [repozytorium GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql) i może zostać pobrany z tego miejsca.</span><span class="sxs-lookup"><span data-stu-id="3b81f-183">hello Hive queries are shared in hello [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql) and can be downloaded from there.</span></span>

<span data-ttu-id="3b81f-184">Oto zapytanie Hive hello utworzona tabela programu Hive.</span><span class="sxs-lookup"><span data-stu-id="3b81f-184">Here is hello Hive query that creates a Hive table.</span></span>

    create database if not exists <database name>;
    CREATE EXTERNAL TABLE if not exists <database name>.<table name>
    (
        field1 string,
        field2 int,
        field3 float,
        field4 double,
        ...,
        fieldN string
    )
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' lines terminated by '<line separator>'
    STORED AS TEXTFILE LOCATION '<storage location>' TBLPROPERTIES("skip.header.line.count"="1");

<span data-ttu-id="3b81f-185">Poniżej przedstawiono opisy hello hello pola, które muszą tooplug w i inne konfiguracje:</span><span class="sxs-lookup"><span data-stu-id="3b81f-185">Here are hello descriptions of hello fields that you need tooplug in and other configurations:</span></span>

* <span data-ttu-id="3b81f-186">**&#60; Nazwa bazy danych >**: Nazwa hello hello bazy danych, które mają toocreate.</span><span class="sxs-lookup"><span data-stu-id="3b81f-186">**&#60;database name>**: hello name of hello database that you want toocreate.</span></span> <span data-ttu-id="3b81f-187">Jeśli chcesz toouse hello domyślna baza danych, hello zapytania *tworzenie bazy danych...*  można pominąć.</span><span class="sxs-lookup"><span data-stu-id="3b81f-187">If you just want toouse hello default database, hello query *create database...* can be omitted.</span></span>
* <span data-ttu-id="3b81f-188">**&#60; Nazwa tabeli >**: hello Nazwa tabeli hello, które mają toocreate w hello określonej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="3b81f-188">**&#60;table name>**: hello name of hello table that you want toocreate within hello specified database.</span></span> <span data-ttu-id="3b81f-189">Toouse hello domyślna baza danych należy hello tabeli mogą być bezpośrednio przywoływane przez *&#60; Nazwa tabeli >* bez &#60; Nazwa bazy danych >.</span><span class="sxs-lookup"><span data-stu-id="3b81f-189">If you want toouse hello default database, hello table can be directly referred by *&#60;table name>* without &#60;database name>.</span></span>
* <span data-ttu-id="3b81f-190">**&#60; separator pola >**: hello separatora, ograniczającego pól w toobe pliku danych hello przekazać toohello tabelę programu Hive.</span><span class="sxs-lookup"><span data-stu-id="3b81f-190">**&#60;field separator>**: hello separator that delimits fields in hello data file toobe uploaded toohello Hive table.</span></span>
* <span data-ttu-id="3b81f-191">**&#60; linii separatora >**: hello separatora, ograniczającego wierszy w pliku danych hello.</span><span class="sxs-lookup"><span data-stu-id="3b81f-191">**&#60;line separator>**: hello separator that delimits lines in hello data file.</span></span>
* <span data-ttu-id="3b81f-192">**&#60; lokalizacja magazynu >**: hello danych hello toosave lokalizacji magazynu platformy Azure z tabele programu Hive.</span><span class="sxs-lookup"><span data-stu-id="3b81f-192">**&#60;storage location>**: hello Azure storage location toosave hello data of Hive tables.</span></span> <span data-ttu-id="3b81f-193">Jeśli nie określisz *lokalizacji &#60; lokalizacja magazynu >*, hello bazy danych i hello tabele są przechowywane w *gałęzi/magazynu/* katalogu w kontenerze domyślna hello hello klastra gałąź domyślną.</span><span class="sxs-lookup"><span data-stu-id="3b81f-193">If you do not specify *LOCATION &#60;storage location>*, hello database and hello tables are stored in *hive/warehouse/* directory in hello default container of hello Hive cluster by default.</span></span> <span data-ttu-id="3b81f-194">Lokalizacja magazynu hello toospecify należy hello lokalizacji magazynu ma toobe w kontenerze domyślna hello hello bazy danych i tabele.</span><span class="sxs-lookup"><span data-stu-id="3b81f-194">If you want toospecify hello storage location, hello storage location has toobe within hello default container for hello database and tables.</span></span> <span data-ttu-id="3b81f-195">Tej lokalizacji jest określane jako lokalizacji względnej toohello domyślny kontener hello klastra w formacie hello toobe *"wasb: / / / &#60; katalogu 1 > /"* lub *"wasb: lokalizacje &#60; katalogu 1 > / &#60; katalog 2 > / "*itp. Po wykonaniu zapytania hello hello względną katalogi są tworzone w ramach hello domyślnego kontenera.</span><span class="sxs-lookup"><span data-stu-id="3b81f-195">This location has toobe referred as location relative toohello default container of hello cluster in hello format of *'wasb:///&#60;directory 1>/'* or *'wasb:///&#60;directory 1>/&#60;directory 2>/'*, etc. After hello query is executed, hello relative directories are created within hello default container.</span></span>
* <span data-ttu-id="3b81f-196">**TBLPROPERTIES("SKIP.Header.line.Count"="1")**: Jeśli plik danych hello ma wiersz nagłówka, masz tooadd tej właściwości **na końcu hello** z hello *Utwórz tabelę* zapytania.</span><span class="sxs-lookup"><span data-stu-id="3b81f-196">**TBLPROPERTIES("skip.header.line.count"="1")**: If hello data file has a header line, you have tooadd this property **at hello end** of hello *create table* query.</span></span> <span data-ttu-id="3b81f-197">W przeciwnym razie wiersz nagłówka hello jest ładowany jako tabelę toohello rekordów.</span><span class="sxs-lookup"><span data-stu-id="3b81f-197">Otherwise, hello header line is loaded as a record toohello table.</span></span> <span data-ttu-id="3b81f-198">Jeśli plik danych hello nie ma wiersz nagłówka, w zapytaniu hello można pominąć tej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="3b81f-198">If hello data file does not have a header line, this configuration can be omitted in hello query.</span></span>

## <span data-ttu-id="3b81f-199"><a name="load-data"></a>Tabele tooHive danych obciążenia</span><span class="sxs-lookup"><span data-stu-id="3b81f-199"><a name="load-data"></a>Load data tooHive tables</span></span>
<span data-ttu-id="3b81f-200">Oto hello zapytania Hive, który ładuje dane do tabeli programu Hive.</span><span class="sxs-lookup"><span data-stu-id="3b81f-200">Here is hello Hive query that loads data into a Hive table.</span></span>

    LOAD DATA INPATH '<path tooblob data>' INTO TABLE <database name>.<table name>;

* <span data-ttu-id="3b81f-201">**&#60; ścieżka tooblob dane >**: w przypadku tabeli Hive toohello toobe przekazany plik hello obiektów blob w kontenerze domyślna hello z hello klastra usługi HDInsight Hadoop, hello *&#60; ścieżka tooblob dane >* powinna mieć format hello *"wasb: / / / &#60; katalog, w tym kontenerze > / &#60; nazwa pliku obiektu blob >"*.</span><span class="sxs-lookup"><span data-stu-id="3b81f-201">**&#60;path tooblob data>**: If hello blob file toobe uploaded toohello Hive table is in hello default container of hello HDInsight Hadoop cluster, hello *&#60;path tooblob data>* should be in hello format *'wasb:///&#60;directory in this container>/&#60;blob file name>'*.</span></span> <span data-ttu-id="3b81f-202">Witaj pliku blob może być również w dodatkowych kontenera hello klastra usługi HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="3b81f-202">hello blob file can also be in an additional container of hello HDInsight Hadoop cluster.</span></span> <span data-ttu-id="3b81f-203">W takim przypadku *&#60; ścieżka tooblob dane >* powinna mieć format hello *"wasb: / / &#60; nazwa kontenera > @&#60; nazwa konta magazynu >.blob.core.windows.net/ &#60; nazwa pliku obiektu blob >"*.</span><span class="sxs-lookup"><span data-stu-id="3b81f-203">In this case, *&#60;path tooblob data>* should be in hello format *'wasb://&#60;container name>@&#60;storage account name>.blob.core.windows.net/&#60;blob file name>'*.</span></span>

  > [!NOTE]
  > <span data-ttu-id="3b81f-204">Hello obiektu blob danych toobe przekazać tooHive tabela ma toobe w domyślnej hello lub dodatkowego kontenera hello konta magazynu dla klastra usługi Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="3b81f-204">hello blob data toobe uploaded tooHive table has toobe in hello default or additional container of hello storage account for hello Hadoop cluster.</span></span> <span data-ttu-id="3b81f-205">W przeciwnym razie hello *danych obciążenia* działanie nie powiodło się Strona skarżąca, że nie ma dostępu do danych hello.</span><span class="sxs-lookup"><span data-stu-id="3b81f-205">Otherwise, hello *LOAD DATA* query fails complaining that it cannot access hello data.</span></span>
  >
  >

## <span data-ttu-id="3b81f-206"><a name="partition-orc"></a>Tematy zaawansowane: podzielona na partycje tabeli i magazynu danych gałęzi w formacie ORC</span><span class="sxs-lookup"><span data-stu-id="3b81f-206"><a name="partition-orc"></a>Advanced topics: partitioned table and store Hive data in ORC format</span></span>
<span data-ttu-id="3b81f-207">W przypadku dużych danych hello partycjonowania tabeli hello jest korzystne dla zapytań, które potrzebują tylko tooscan kilka partycji tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="3b81f-207">If hello data is large, partitioning hello table is beneficial for queries that only need tooscan a few partitions of hello table.</span></span> <span data-ttu-id="3b81f-208">Na przykład jest uzasadnione toopartition hello dziennika danych witryny sieci web według daty.</span><span class="sxs-lookup"><span data-stu-id="3b81f-208">For instance, it is reasonable toopartition hello log data of a web site by dates.</span></span>

<span data-ttu-id="3b81f-209">W dodatku toopartitioning Hive tabel, jest również przydatne toostore hello Hive dane w formacie zoptymalizowanych pod kątem wiersza kolumnowy (ORC) hello.</span><span class="sxs-lookup"><span data-stu-id="3b81f-209">In addition toopartitioning Hive tables, it is also beneficial toostore hello Hive data in hello Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="3b81f-210">Aby uzyskać więcej informacji na ORC formatowania, zobacz <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">plików ORC przy użyciu zwiększa wydajność podczas czytania, zapisywania i przetwarzania danych Hive</a>.</span><span class="sxs-lookup"><span data-stu-id="3b81f-210">For more information on ORC formatting, see <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">Using ORC files improves performance when Hive is reading, writing, and processing data</a>.</span></span>

### <a name="partitioned-table"></a><span data-ttu-id="3b81f-211">Tabeli partycjonowanej</span><span class="sxs-lookup"><span data-stu-id="3b81f-211">Partitioned table</span></span>
<span data-ttu-id="3b81f-212">Oto zapytanie Hive hello tworzy tabeli partycjonowanej i ładuje dane do niego.</span><span class="sxs-lookup"><span data-stu-id="3b81f-212">Here is hello Hive query that creates a partitioned table and loads data into it.</span></span>

    CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<table name>
    (field1 string,
    ...
    fieldN string
    )
    PARTITIONED BY (<partitionfieldname> vartype) ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
         lines terminated by '<line separator>' TBLPROPERTIES("skip.header.line.count"="1");
    LOAD DATA INPATH '<path toohello source file>' INTO TABLE <database name>.<partitioned table name>
        PARTITION (<partitionfieldname>=<partitionfieldvalue>);

<span data-ttu-id="3b81f-213">Podczas wykonywania zapytania partycjonowane tabele, zaleca się tooadd hello partycji warunku w hello **początku** z hello `where` skuteczności hello wyszukiwanie znacznie zwiększa klauzuli jako to.</span><span class="sxs-lookup"><span data-stu-id="3b81f-213">When querying partitioned tables, it is recommended tooadd hello partition condition in hello **beginning** of hello `where` clause as this improves hello efficacy of searching significantly.</span></span>

    select
        field1, field2, ..., fieldN
    from <database name>.<partitioned table name>
    where <partitionfieldname>=<partitionfieldvalue> and ...;

### <span data-ttu-id="3b81f-214"><a name="orc"></a>Przechowywanie danych gałęzi w formacie ORC</span><span class="sxs-lookup"><span data-stu-id="3b81f-214"><a name="orc"></a>Store Hive data in ORC format</span></span>
<span data-ttu-id="3b81f-215">Nie można bezpośrednio ładowanie danych z magazynu obiektów blob do gałęzi tabel, które są przechowywane w formacie ORC hello.</span><span class="sxs-lookup"><span data-stu-id="3b81f-215">You cannot directly load data from blob storage into Hive tables that is stored in hello ORC format.</span></span> <span data-ttu-id="3b81f-216">Poniżej przedstawiono kroki hello tooHive tabel są przechowywane w formacie ORC obiektów blob tego hello należy tootake tooload danych z platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3b81f-216">Here are hello steps that hello you need tootake tooload data from Azure blobs tooHive tables stored in ORC format.</span></span>

<span data-ttu-id="3b81f-217">Tworzenie tabeli zewnętrznej **TEXTFILE AS PRZECHOWYWANE** i ładowanie danych z tabeli toohello magazynu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="3b81f-217">Create an external table **STORED AS TEXTFILE** and load data from blob storage toohello table.</span></span>

        CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<external textfile table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
            lines terminated by '<line separator>' STORED AS TEXTFILE
            LOCATION 'wasb:///<directory in Azure blob>' TBLPROPERTIES("skip.header.line.count"="1");

        LOAD DATA INPATH '<path toohello source file>' INTO TABLE <database name>.<table name>;

<span data-ttu-id="3b81f-218">Tworzenie wewnętrznej tabeli z hello tego samego schematu jako hello tabeli zewnętrznej w kroku 1, z hello sam ogranicznik pola i przechowywać hello Hive dane w formacie ORC hello.</span><span class="sxs-lookup"><span data-stu-id="3b81f-218">Create an internal table with hello same schema as hello external table in step 1, with hello same field delimiter, and store hello Hive data in hello ORC format.</span></span>

        CREATE TABLE IF NOT EXISTS <database name>.<ORC table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' STORED AS ORC;

<span data-ttu-id="3b81f-219">Wybierz dane z tabeli zewnętrznej hello w kroku 1 i Wstaw do tabeli ORC hello</span><span class="sxs-lookup"><span data-stu-id="3b81f-219">Select data from hello external table in step 1 and insert into hello ORC table</span></span>

        INSERT OVERWRITE TABLE <database name>.<ORC table name>
            SELECT * FROM <database name>.<external textfile table name>;

> [!NOTE]
> <span data-ttu-id="3b81f-220">Jeśli tabela TEXTFILE hello *&#60; Nazwa bazy danych >. &#60; Nazwa tabeli zewnętrznej textfile >* zawiera partycje, w KROKU 3 hello `SELECT * FROM <database name>.<external textfile table name>` polecenia wybiera hello zmiennej partycji pola w hello zwrócony zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="3b81f-220">If hello TEXTFILE table *&#60;database name>.&#60;external textfile table name>* has partitions, in STEP 3, hello `SELECT * FROM <database name>.<external textfile table name>` command selects hello partition variable as a field in hello returned data set.</span></span> <span data-ttu-id="3b81f-221">Wstawienie go w hello *&#60; Nazwa bazy danych >. &#60; Nazwa tabeli ORC >* nie powiedzie się, ponieważ *&#60; Nazwa bazy danych >. &#60; Nazwa tabeli ORC >* nie ma hello partycji zmiennej jako pole w hello schemat tabeli.</span><span class="sxs-lookup"><span data-stu-id="3b81f-221">Inserting it into hello *&#60;database name>.&#60;ORC table name>* fails since *&#60;database name>.&#60;ORC table name>* does not have hello partition variable as a field in hello table schema.</span></span> <span data-ttu-id="3b81f-222">W takim przypadku należy toobe pól select hello toospecifically dodaje zbyt*&#60; Nazwa bazy danych >. &#60; Nazwa tabeli ORC >* w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="3b81f-222">In this case, you need toospecifically select hello fields toobe inserted too*&#60;database name>.&#60;ORC table name>* as follows:</span></span>
>
>

        INSERT OVERWRITE TABLE <database name>.<ORC table name> PARTITION (<partition variable>=<partition value>)
           SELECT field1, field2, ..., fieldN
           FROM <database name>.<external textfile table name>
           WHERE <partition variable>=<partition value>;

<span data-ttu-id="3b81f-223">Jest bezpieczne toodrop hello *&#60; Nazwa tabeli zewnętrznej textfile >* po użyciu hello następującego zapytania po wszystkich danych został wstawiony do *&#60; Nazwa bazy danych >. &#60; Nazwa tabeli ORC >*:</span><span class="sxs-lookup"><span data-stu-id="3b81f-223">It is safe toodrop hello *&#60;external textfile table name>* when using hello following query after all data has been inserted into *&#60;database name>.&#60;ORC table name>*:</span></span>

        DROP TABLE IF EXISTS <database name>.<external textfile table name>;

<span data-ttu-id="3b81f-224">Po wykonaniu tej procedury, powinien mieć tabelę z danymi w toouse gotowy hello ORC format.</span><span class="sxs-lookup"><span data-stu-id="3b81f-224">After following this procedure, you should have a table with data in hello ORC format ready toouse.</span></span>  
