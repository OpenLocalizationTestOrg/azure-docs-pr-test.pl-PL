---
title: "Tworzenie tabel programu Hive i ładowanie danych z magazynu obiektów Blob platformy Azure | Dokumentacja firmy Microsoft"
description: "Tworzenie tabel programu Hive i ładowania danych w obiekcie blob do tabel"
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
ms.openlocfilehash: eca4ecd8f639bb9816903f4b1d1f999755da819c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-hive-tables-and-load-data-from-azure-blob-storage"></a><span data-ttu-id="e00e1-103">Tworzenie tabel programu Hive i ładowanie danych z magazynu obiektów Blob Azure</span><span class="sxs-lookup"><span data-stu-id="e00e1-103">Create Hive tables and load data from Azure Blob Storage</span></span>
<span data-ttu-id="e00e1-104">W tym temacie przedstawiono ogólne zapytań Hive, które Tworzenie tabel programu Hive i ładowanie danych z magazynu obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e00e1-104">This topic presents generic Hive queries that create Hive tables and load data from Azure blob storage.</span></span> <span data-ttu-id="e00e1-105">Instrukcje dostępne są również na partycje tabele programu Hive i przy użyciu zoptymalizowanych pod kątem wiersza kolumnowy (ORC) formatowanie, aby poprawić wydajność zapytań.</span><span class="sxs-lookup"><span data-stu-id="e00e1-105">Some guidance is also provided on partitioning Hive tables and on using the Optimized Row Columnar (ORC) formatting to improve query performance.</span></span>

<span data-ttu-id="e00e1-106">To **menu** linki do tematów opisujących sposób pozyskiwania danych w środowisku docelowym, gdzie dane mogą być przechowywane i przetwarzane podczas procesu nauki danych zespołu (TDSP).</span><span class="sxs-lookup"><span data-stu-id="e00e1-106">This **menu** links to topics that describe how to ingest data into target environments where the data can be stored and processed during the Team Data Science Process (TDSP).</span></span>

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="e00e1-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e00e1-107">Prerequisites</span></span>
<span data-ttu-id="e00e1-108">W tym artykule przyjęto założenie, że masz:</span><span class="sxs-lookup"><span data-stu-id="e00e1-108">This article assumes that you have:</span></span>

* <span data-ttu-id="e00e1-109">Utworzone konto magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e00e1-109">Created an Azure storage account.</span></span> <span data-ttu-id="e00e1-110">Aby uzyskać instrukcje, zobacz [kont magazynu Azure o](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="e00e1-110">If you need instructions, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
* <span data-ttu-id="e00e1-111">Zainicjowano obsługę administracyjną dostosowane klastra usługi Hadoop w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e00e1-111">Provisioned a customized Hadoop cluster with the HDInsight service.</span></span>  <span data-ttu-id="e00e1-112">Aby uzyskać instrukcje, zobacz [dostosować Azure HDInsight Hadoop clusters zaawansowana analityka](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="e00e1-112">If you need instructions, see [Customize Azure HDInsight Hadoop clusters for advanced analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="e00e1-113">Włączony dostęp zdalny do klastra, zalogowany i otworzyć konsolę wiersza polecenia usługi Hadoop.</span><span class="sxs-lookup"><span data-stu-id="e00e1-113">Enabled remote access to the cluster, logged in, and opened the Hadoop Command-Line console.</span></span> <span data-ttu-id="e00e1-114">Aby uzyskać instrukcje, zobacz [dostęp węzła Head klastra usługi Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="e00e1-114">If you need instructions, see [Access the Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>

## <a name="upload-data-to-azure-blob-storage"></a><span data-ttu-id="e00e1-115">Przekazywanie danych do magazynu obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e00e1-115">Upload data to Azure blob storage</span></span>
<span data-ttu-id="e00e1-116">Jeśli utworzono maszynę wirtualną platformy Azure, wykonując instrukcje podane w [Konfigurowanie maszyny wirtualnej platformy Azure, zaawansowana analityka](machine-learning-data-science-setup-virtual-machine.md), ten plik skryptu powinien zostały pobrane *C:\\użytkowników \\ \<nazwy użytkownika\>\\dokumenty\\skryptów nauki danych* katalogu na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e00e1-116">If you created an Azure virtual machine by following the instructions provided in [Set up an Azure virtual machine for advanced analytics](machine-learning-data-science-setup-virtual-machine.md), this script file should have been downloaded to the *C:\\Users\\\<user name\>\\Documents\\Data Science Scripts* directory on the virtual machine.</span></span> <span data-ttu-id="e00e1-117">Te zapytania Hive wymagają tylko należy podłączyć własny schemat danych i konfiguracji magazynu obiektów blob platformy Azure w odpowiednich polach gotowość do przesłania.</span><span class="sxs-lookup"><span data-stu-id="e00e1-117">These Hive queries only require that you plug in your own data schema and Azure blob storage configuration in the appropriate fields to be ready for submission.</span></span>

<span data-ttu-id="e00e1-118">Przyjęto założenie, że dane dla tabele programu Hive jest w **nieskompresowanych** tabelarycznej i czy dane został przesłany do domyślnej (lub dodatkowe) kontenera konta magazynu używane przez klaster usługi Hadoop.</span><span class="sxs-lookup"><span data-stu-id="e00e1-118">We assume that the data for Hive tables is in an **uncompressed** tabular format, and that the data has been uploaded to the default (or to an additional) container of the storage account used by the Hadoop cluster.</span></span>

<span data-ttu-id="e00e1-119">Jeśli chcesz praktyki na **NYC taksówki podróży danych**, musisz:</span><span class="sxs-lookup"><span data-stu-id="e00e1-119">If you want to practice on the **NYC Taxi Trip Data**, you need to:</span></span>

* <span data-ttu-id="e00e1-120">**Pobierz** 24 [danych podróży taksówki NYC](http://www.andresmh.com/nyctaxitrips) plików (12 pliki podróży i pliki taryfy 12),</span><span class="sxs-lookup"><span data-stu-id="e00e1-120">**download** the 24 [NYC Taxi Trip Data](http://www.andresmh.com/nyctaxitrips) files (12 Trip files and 12 Fare files),</span></span>
* <span data-ttu-id="e00e1-121">**Rozpakuj** wszystkie pliki w pliki CSV, a następnie</span><span class="sxs-lookup"><span data-stu-id="e00e1-121">**unzip** all files into .csv files, and then</span></span>
* <span data-ttu-id="e00e1-122">**Przekaż** ich domyślne (lub odpowiedniego kontenera) konto magazynu Azure, która została utworzona przez procedury opisane w temacie [dostosować Azure HDInsight Hadoop clusters zaawansowane procesu analizy i technologii](machine-learning-data-science-customize-hadoop-cluster.md)tematu.</span><span class="sxs-lookup"><span data-stu-id="e00e1-122">**upload** them to the default (or appropriate container) of the Azure storage account that was created by the procedure outlined in the [Customize Azure HDInsight Hadoop clusters for Advanced Analytics Process and Technology](machine-learning-data-science-customize-hadoop-cluster.md) topic.</span></span> <span data-ttu-id="e00e1-123">Proces przekazywania plików CSV do domyślnego kontenera na koncie magazynu można znaleźć na tym [strony](machine-learning-data-science-process-hive-walkthrough.md#upload).</span><span class="sxs-lookup"><span data-stu-id="e00e1-123">The process to upload the .csv files to the default container on the storage account can be found on this [page](machine-learning-data-science-process-hive-walkthrough.md#upload).</span></span>

## <span data-ttu-id="e00e1-124"><a name="submit"></a>Temat dotyczący przesyłania zapytań programu Hive</span><span class="sxs-lookup"><span data-stu-id="e00e1-124"><a name="submit"></a>How to submit Hive queries</span></span>
<span data-ttu-id="e00e1-125">Można przesłać zapytań programu hive za pomocą:</span><span class="sxs-lookup"><span data-stu-id="e00e1-125">Hive queries can be submitted by using:</span></span>

1. [<span data-ttu-id="e00e1-126">Wysyłanie zapytań programu Hive za pomocą wiersza polecenia platformy Hadoop w headnode klastra usługi Hadoop</span><span class="sxs-lookup"><span data-stu-id="e00e1-126">Submit Hive queries through Hadoop Command Line in headnode of Hadoop cluster</span></span>](#headnode)
2. [<span data-ttu-id="e00e1-127">Wysyłanie zapytań programu Hive w edytorze Hive</span><span class="sxs-lookup"><span data-stu-id="e00e1-127">Submit Hive queries with the Hive Editor</span></span>](#hive-editor)
3. [<span data-ttu-id="e00e1-128">Wysyłanie zapytań programu Hive z poleceń programu PowerShell Azure</span><span class="sxs-lookup"><span data-stu-id="e00e1-128">Submit Hive queries with Azure PowerShell Commands</span></span>](#ps)

<span data-ttu-id="e00e1-129">Zapytania hive są przypominającego SQL.</span><span class="sxs-lookup"><span data-stu-id="e00e1-129">Hive queries are SQL-like.</span></span> <span data-ttu-id="e00e1-130">Jeśli znasz SQL, może się okazać [Hive arkusza Cheat użytkowników SQL](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf) przydatne.</span><span class="sxs-lookup"><span data-stu-id="e00e1-130">If you are familiar with SQL, you may find the [Hive for SQL Users Cheat Sheet](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf) useful.</span></span>

<span data-ttu-id="e00e1-131">Podczas składania zapytań programu Hive, można też kontrolować miejsce docelowe danych wyjściowych z zapytań programu Hive, czy jest na ekranie lub do pliku lokalnego w węźle głównym lub obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e00e1-131">When submitting a Hive query, you can also control the destination of the output from Hive queries, whether it be on the screen or to a local file on the head node or to an Azure blob.</span></span>

### <span data-ttu-id="e00e1-132"><a name="headnode"></a> 1. Wysyłanie zapytań programu Hive za pomocą wiersza polecenia platformy Hadoop w headnode klastra usługi Hadoop</span><span class="sxs-lookup"><span data-stu-id="e00e1-132"><a name="headnode"></a> 1. Submit Hive queries through Hadoop Command Line in headnode of Hadoop cluster</span></span>
<span data-ttu-id="e00e1-133">Jeśli zapytanie Hive jest złożone, przesłania go bezpośrednio w węźle głównym Hadoop klastra zwykle prowadzi do szybciej włączyć niż przesłania go za pomocą skryptów Edytor Hive lub Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e00e1-133">If the Hive query is complex, submitting it directly in the head node of the Hadoop cluster typically leads to faster turn around than submitting it with a Hive Editor or Azure PowerShell scripts.</span></span>

<span data-ttu-id="e00e1-134">Zaloguj się do węzła głównego klastra usługi Hadoop, Otwórz okno wiersza polecenia usługi Hadoop na pulpicie węzła głównego, a następnie wprowadź polecenie `cd %hive_home%\bin`.</span><span class="sxs-lookup"><span data-stu-id="e00e1-134">Log in to the head node of the Hadoop cluster, open the Hadoop Command Line on the desktop of the head node, and enter command `cd %hive_home%\bin`.</span></span>

<span data-ttu-id="e00e1-135">Istnieją trzy sposoby wysyłanie zapytań programu Hive w wierszu polecenia Hadoop:</span><span class="sxs-lookup"><span data-stu-id="e00e1-135">You have three ways to submit Hive queries in the Hadoop Command Line:</span></span>

* <span data-ttu-id="e00e1-136">bezpośrednio</span><span class="sxs-lookup"><span data-stu-id="e00e1-136">directly</span></span>
* <span data-ttu-id="e00e1-137">przy użyciu plików .hql</span><span class="sxs-lookup"><span data-stu-id="e00e1-137">using .hql files</span></span>
* <span data-ttu-id="e00e1-138">z konsoli poleceń gałęzi</span><span class="sxs-lookup"><span data-stu-id="e00e1-138">with the Hive command console</span></span>

#### <a name="submit-hive-queries-directly-in-hadoop-command-line"></a><span data-ttu-id="e00e1-139">Wysyłanie zapytań programu Hive bezpośrednio w Hadoop wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="e00e1-139">Submit Hive queries directly in Hadoop Command Line.</span></span>
<span data-ttu-id="e00e1-140">Możesz uruchomić polecenie, takie jak `hive -e "<your hive query>;` do przesyłania zapytań programu Hive proste bezpośrednio w Hadoop wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="e00e1-140">You can run command like `hive -e "<your hive query>;` to submit simple Hive queries directly in Hadoop Command Line.</span></span> <span data-ttu-id="e00e1-141">Oto przykład, gdzie czerwonym prostokątem przedstawiono polecenia, który przesyła zapytanie Hive, a pole zielony przedstawiono dane wyjściowe z zapytania Hive.</span><span class="sxs-lookup"><span data-stu-id="e00e1-141">Here is an example, where the red box outlines the command that submits the Hive query, and the green box outlines the output from the Hive query.</span></span>

![Tworzenie obszaru roboczego](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-1.png)

#### <a name="submit-hive-queries-in-hql-files"></a><span data-ttu-id="e00e1-143">Wysyłanie zapytań programu Hive w plikach .hql</span><span class="sxs-lookup"><span data-stu-id="e00e1-143">Submit Hive queries in .hql files</span></span>
<span data-ttu-id="e00e1-144">Jeśli zapytanie Hive jest bardziej skomplikowany i zawiera wiele wierszy, edytowanie zapytań w wierszu polecenia lub gałęzi konsoli poleceń nie jest praktyczne.</span><span class="sxs-lookup"><span data-stu-id="e00e1-144">When the Hive query is more complicated and has multiple lines, editing queries in command line or Hive command console is not practical.</span></span> <span data-ttu-id="e00e1-145">Alternatywą jest używany edytor tekstu w węzła głównego klastra usługi Hadoop do zapisania zapytań Hive w pliku .hql w katalogu lokalnym węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="e00e1-145">An alternative is to use a text editor in the head node of the Hadoop cluster to save the Hive queries in a .hql file in a local directory of the head node.</span></span> <span data-ttu-id="e00e1-146">Następnie można przesłać zapytań Hive w pliku .hql przy użyciu `-f` argument w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="e00e1-146">Then the Hive query in the .hql file can be submitted by using the `-f` argument as follows:</span></span>

    hive -f "<path to the .hql file>"

![Tworzenie obszaru roboczego](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-3.png)

<span data-ttu-id="e00e1-148">**Pomiń postępu stan ekranu drukowania zapytań Hive**</span><span class="sxs-lookup"><span data-stu-id="e00e1-148">**Suppress progress status screen print of Hive queries**</span></span>

<span data-ttu-id="e00e1-149">Domyślnie po wysłaniu zapytania Hive w wierszu polecenia Hadoop postęp zadania mapy/Zmniejsz jest drukowany na ekranie.</span><span class="sxs-lookup"><span data-stu-id="e00e1-149">By default, after Hive query is submitted in Hadoop Command Line, the progress of the Map/Reduce job is printed out on screen.</span></span> <span data-ttu-id="e00e1-150">Aby pominąć drukowania ekranu mapy/Zmniejsz postępu zadania, można użyć argumentu `-S` ("S" wielkimi literami) w poleceniu wiersza w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="e00e1-150">To suppress the screen print of the Map/Reduce job progress, you can use an argument `-S` ("S" in upper case) in the command line as follows:</span></span>

    hive -S -f "<path to the .hql file>"
<span data-ttu-id="e00e1-151">.</span><span class="sxs-lookup"><span data-stu-id="e00e1-151">.</span></span>    <span data-ttu-id="e00e1-152">-S -e hive "<Hive queries>"</span><span class="sxs-lookup"><span data-stu-id="e00e1-152">hive -S -e "<Hive queries>"</span></span>

#### <a name="submit-hive-queries-in-hive-command-console"></a><span data-ttu-id="e00e1-153">Wysyłanie zapytań programu Hive z konsoli poleceń Hive.</span><span class="sxs-lookup"><span data-stu-id="e00e1-153">Submit Hive queries in Hive command console.</span></span>
<span data-ttu-id="e00e1-154">Można również najpierw wprowadzić konsoli poleceń Hive, uruchamiając polecenie `hive` w wierszu polecenia Hadoop, a następnie wysyłanie zapytań programu Hive z konsoli poleceń Hive.</span><span class="sxs-lookup"><span data-stu-id="e00e1-154">You can also first enter the Hive command console by running command `hive` in Hadoop Command Line, and then submit Hive queries in Hive command console.</span></span> <span data-ttu-id="e00e1-155">Oto przykład.</span><span class="sxs-lookup"><span data-stu-id="e00e1-155">Here is an example.</span></span> <span data-ttu-id="e00e1-156">W tym przykładzie dwa pola czerwone zaznacz polecenia służące do wprowadzania Hive konsoli poleceń i zapytań Hive przesłane w konsoli polecenie gałęzi, odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="e00e1-156">In this example, the two red boxes highlight the commands used to enter the Hive command console, and the Hive query submitted in Hive command console, respectively.</span></span> <span data-ttu-id="e00e1-157">Pole zielony prezentuje dane wyjściowe z zapytania Hive.</span><span class="sxs-lookup"><span data-stu-id="e00e1-157">The green box highlights the output from the Hive query.</span></span>

![Tworzenie obszaru roboczego](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-2.png)

<span data-ttu-id="e00e1-159">Poprzednich przykładach output bezpośrednio na ekranie wyniki zapytania Hive.</span><span class="sxs-lookup"><span data-stu-id="e00e1-159">The previous examples directly output the Hive query results on screen.</span></span> <span data-ttu-id="e00e1-160">Można także zapisywać dane wyjściowe do pliku lokalnego węzła głównego lub do obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e00e1-160">You can also write the output to a local file on the head node, or to an Azure blob.</span></span> <span data-ttu-id="e00e1-161">Następnie można użyć innych narzędzi do dalszej analizy dane wyjściowe zapytań programu Hive.</span><span class="sxs-lookup"><span data-stu-id="e00e1-161">Then, you can use other tools to further analyze the output of Hive queries.</span></span>

<span data-ttu-id="e00e1-162">**Dane wyjściowe Hive wyników zapytania do pliku lokalnego.**</span><span class="sxs-lookup"><span data-stu-id="e00e1-162">**Output Hive query results to a local file.**</span></span>
<span data-ttu-id="e00e1-163">Można wyświetlić wyników zapytania Hive w lokalnym katalogu w węźle głównym, należy przesłać zapytanie Hive w wierszu polecenia Hadoop w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="e00e1-163">To output Hive query results to a local directory on the head node, you have to submit the Hive query in the Hadoop Command Line as follows:</span></span>

    hive -e "<hive query>" > <local path in the head node>

<span data-ttu-id="e00e1-164">W poniższym przykładzie zapytanie Hive dane wyjściowe są zapisywane do pliku `hivequeryoutput.txt` w katalogu `C:\apps\temp`.</span><span class="sxs-lookup"><span data-stu-id="e00e1-164">In the following example, the output of Hive query is written into a file `hivequeryoutput.txt` in directory `C:\apps\temp`.</span></span>

![Tworzenie obszaru roboczego](./media/machine-learning-data-science-move-hive-tables/output-hive-results-1.png)

<span data-ttu-id="e00e1-166">**Wyniki zapytania Hive dane wyjściowe do obiektów blob platformy Azure**</span><span class="sxs-lookup"><span data-stu-id="e00e1-166">**Output Hive query results to an Azure blob**</span></span>

<span data-ttu-id="e00e1-167">Można również output wyników zapytania Hive do obiektów blob platformy Azure, w ramach kontenera domyślnego klastra usługi Hadoop.</span><span class="sxs-lookup"><span data-stu-id="e00e1-167">You can also output the Hive query results to an Azure blob, within the default container of the Hadoop cluster.</span></span> <span data-ttu-id="e00e1-168">Zapytanie Hive to wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="e00e1-168">The Hive query for this is as follows:</span></span>

    insert overwrite directory wasb:///<directory within the default container> <select clause from ...>

<span data-ttu-id="e00e1-169">W poniższym przykładzie danych wyjściowych zapytanie Hive są zapisywane do katalogu obiektu blob `queryoutputdir` w domyślnym kontenerze klastra usługi Hadoop.</span><span class="sxs-lookup"><span data-stu-id="e00e1-169">In the following example, the output of Hive query is written to a blob directory `queryoutputdir` within the default container of the Hadoop cluster.</span></span> <span data-ttu-id="e00e1-170">W tym miejscu wystarczy podać nazwę katalogu bez nazwy obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="e00e1-170">Here, you only need to provide the directory name, without the blob name.</span></span> <span data-ttu-id="e00e1-171">Zostanie zgłoszony błąd, jeśli zostaną podane nazwy usługi directory i obiektów blob, takich jak `wasb:///queryoutputdir/queryoutput.txt`.</span><span class="sxs-lookup"><span data-stu-id="e00e1-171">An error is thrown if you provide both directory and blob names, such as `wasb:///queryoutputdir/queryoutput.txt`.</span></span>

![Tworzenie obszaru roboczego](./media/machine-learning-data-science-move-hive-tables/output-hive-results-2.png)

<span data-ttu-id="e00e1-173">Po otwarciu domyślny kontener klastra usługi Hadoop przy użyciu Eksploratora usługi Storage Azure zostanie wyświetlone dane wyjściowe zapytania Hive, jak pokazano na poniższej ilustracji.</span><span class="sxs-lookup"><span data-stu-id="e00e1-173">If you open the default container of the Hadoop cluster using Azure Storage Explorer, you can see the output of the Hive query as shown in the following figure.</span></span> <span data-ttu-id="e00e1-174">Filtr (wyróżniony przez czerwonym prostokątem) może dotyczyć tylko pobieranie obiektu blob o określonej litery w nazwach.</span><span class="sxs-lookup"><span data-stu-id="e00e1-174">You can apply the filter (highlighted by red box) to only retrieve the blob with specified letters in names.</span></span>

![Tworzenie obszaru roboczego](./media/machine-learning-data-science-move-hive-tables/output-hive-results-3.png)

### <span data-ttu-id="e00e1-176"><a name="hive-editor"></a> 2. Wysyłanie zapytań programu Hive w edytorze Hive</span><span class="sxs-lookup"><span data-stu-id="e00e1-176"><a name="hive-editor"></a> 2. Submit Hive queries with the Hive Editor</span></span>
<span data-ttu-id="e00e1-177">Umożliwia także konsolę kwerendy (Edytor Hive), wprowadzając adres URL w formacie *https://&#60; Nazwa klastra Hadoop >.azurehdinsight.net/Home/HiveEditor* w przeglądarce sieci web.</span><span class="sxs-lookup"><span data-stu-id="e00e1-177">You can also use the Query Console (Hive Editor) by entering a URL of the form *https://&#60;Hadoop cluster name>.azurehdinsight.net/Home/HiveEditor* into a web browser.</span></span> <span data-ttu-id="e00e1-178">Musi być rejestrowane widzą tę konsolę i dlatego należy poświadczenia klastra usługi Hadoop.</span><span class="sxs-lookup"><span data-stu-id="e00e1-178">You must be logged in the see this console and so you need your Hadoop cluster credentials here.</span></span>

### <span data-ttu-id="e00e1-179"><a name="ps"></a> 3. Wysyłanie zapytań programu Hive z poleceń programu PowerShell Azure</span><span class="sxs-lookup"><span data-stu-id="e00e1-179"><a name="ps"></a> 3. Submit Hive queries with Azure PowerShell Commands</span></span>
<span data-ttu-id="e00e1-180">Można również wysyłanie zapytań programu Hive za pomocą programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e00e1-180">You can also use PowerShell to submit Hive queries.</span></span> <span data-ttu-id="e00e1-181">Aby uzyskać instrukcje, zobacz [zadania Hive przesyłania przy użyciu programu PowerShell](../hdinsight/hdinsight-hadoop-use-hive-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e00e1-181">For instructions, see [Submit Hive jobs using PowerShell](../hdinsight/hdinsight-hadoop-use-hive-powershell.md).</span></span>

## <span data-ttu-id="e00e1-182"><a name="create-tables"></a>Utwórz gałąź bazy danych i tabel</span><span class="sxs-lookup"><span data-stu-id="e00e1-182"><a name="create-tables"></a>Create Hive database and tables</span></span>
<span data-ttu-id="e00e1-183">Zapytania Hive są udostępniane w [repozytorium GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql) i może zostać pobrany z tego miejsca.</span><span class="sxs-lookup"><span data-stu-id="e00e1-183">The Hive queries are shared in the [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql) and can be downloaded from there.</span></span>

<span data-ttu-id="e00e1-184">Oto zapytania Hive, która tworzy tabeli programu Hive.</span><span class="sxs-lookup"><span data-stu-id="e00e1-184">Here is the Hive query that creates a Hive table.</span></span>

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

<span data-ttu-id="e00e1-185">Poniżej przedstawiono opisy pola, które należy podłączyć i inne konfiguracje:</span><span class="sxs-lookup"><span data-stu-id="e00e1-185">Here are the descriptions of the fields that you need to plug in and other configurations:</span></span>

* <span data-ttu-id="e00e1-186">**&#60; Nazwa bazy danych >**: Nazwa bazy danych, który chcesz utworzyć.</span><span class="sxs-lookup"><span data-stu-id="e00e1-186">**&#60;database name>**: the name of the database that you want to create.</span></span> <span data-ttu-id="e00e1-187">Jeśli chcesz użyć domyślnej bazy danych, zapytanie *tworzenie bazy danych...*  można pominąć.</span><span class="sxs-lookup"><span data-stu-id="e00e1-187">If you just want to use the default database, the query *create database...* can be omitted.</span></span>
* <span data-ttu-id="e00e1-188">**&#60; Nazwa tabeli >**: Nazwa tabeli, która ma zostać utworzona w ramach określonej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="e00e1-188">**&#60;table name>**: the name of the table that you want to create within the specified database.</span></span> <span data-ttu-id="e00e1-189">Jeśli chcesz użyć domyślnej bazy danych, tabeli może być bezpośrednio odwołuje się *&#60; Nazwa tabeli >* bez &#60; Nazwa bazy danych >.</span><span class="sxs-lookup"><span data-stu-id="e00e1-189">If you want to use the default database, the table can be directly referred by *&#60;table name>* without &#60;database name>.</span></span>
* <span data-ttu-id="e00e1-190">**&#60; separator pola >**: separator ograniczającego pól w pliku danych do przekazania do tabeli Hive.</span><span class="sxs-lookup"><span data-stu-id="e00e1-190">**&#60;field separator>**: the separator that delimits fields in the data file to be uploaded to the Hive table.</span></span>
* <span data-ttu-id="e00e1-191">**&#60; linii separatora >**: separator ograniczającego wierszy w pliku danych.</span><span class="sxs-lookup"><span data-stu-id="e00e1-191">**&#60;line separator>**: the separator that delimits lines in the data file.</span></span>
* <span data-ttu-id="e00e1-192">**&#60; lokalizacja magazynu >**: lokalizację magazynu Azure, aby zapisać dane tabele programu Hive.</span><span class="sxs-lookup"><span data-stu-id="e00e1-192">**&#60;storage location>**: the Azure storage location to save the data of Hive tables.</span></span> <span data-ttu-id="e00e1-193">Jeśli nie określisz *lokalizacji &#60; lokalizacja magazynu >*, bazy danych i tabele są przechowywane w *gałęzi/magazynu/* katalogu w domyślnym kontenerze klastra gałąź domyślną.</span><span class="sxs-lookup"><span data-stu-id="e00e1-193">If you do not specify *LOCATION &#60;storage location>*, the database and the tables are stored in *hive/warehouse/* directory in the default container of the Hive cluster by default.</span></span> <span data-ttu-id="e00e1-194">Jeśli chcesz określić lokalizację magazynu, lokalizacja magazynu musi być w kontenerze domyślna bazy danych i tabele.</span><span class="sxs-lookup"><span data-stu-id="e00e1-194">If you want to specify the storage location, the storage location has to be within the default container for the database and tables.</span></span> <span data-ttu-id="e00e1-195">Tej lokalizacji musi być określony jako lokalizacji względnej wobec domyślny kontener klastra w formacie *"wasb: / / / &#60; katalogu 1 > /"* lub *"wasb: / / / &#60; katalogu 1 > / &#60; katalog 2 > / "*itp. Po wykonaniu zapytania względną katalogi są tworzone w ramach kontenera domyślnego.</span><span class="sxs-lookup"><span data-stu-id="e00e1-195">This location has to be referred as location relative to the default container of the cluster in the format of *'wasb:///&#60;directory 1>/'* or *'wasb:///&#60;directory 1>/&#60;directory 2>/'*, etc. After the query is executed, the relative directories are created within the default container.</span></span>
* <span data-ttu-id="e00e1-196">**TBLPROPERTIES("SKIP.Header.line.Count"="1")**: Jeśli plik danych ma wiersz nagłówka, należy dodać tę właściwość **na końcu** z *Utwórz tabelę* zapytania.</span><span class="sxs-lookup"><span data-stu-id="e00e1-196">**TBLPROPERTIES("skip.header.line.count"="1")**: If the data file has a header line, you have to add this property **at the end** of the *create table* query.</span></span> <span data-ttu-id="e00e1-197">W przeciwnym razie wiersz nagłówka jest załadowany jako rekordu do tabeli.</span><span class="sxs-lookup"><span data-stu-id="e00e1-197">Otherwise, the header line is loaded as a record to the table.</span></span> <span data-ttu-id="e00e1-198">Jeśli plik danych nie ma wiersz nagłówka, można pominąć tej konfiguracji w zapytaniu.</span><span class="sxs-lookup"><span data-stu-id="e00e1-198">If the data file does not have a header line, this configuration can be omitted in the query.</span></span>

## <span data-ttu-id="e00e1-199"><a name="load-data"></a>Ładowanie danych do tabele programu Hive</span><span class="sxs-lookup"><span data-stu-id="e00e1-199"><a name="load-data"></a>Load data to Hive tables</span></span>
<span data-ttu-id="e00e1-200">Oto zapytania Hive, który ładuje dane do tabeli programu Hive.</span><span class="sxs-lookup"><span data-stu-id="e00e1-200">Here is the Hive query that loads data into a Hive table.</span></span>

    LOAD DATA INPATH '<path to blob data>' INTO TABLE <database name>.<table name>;

* <span data-ttu-id="e00e1-201">**&#60; ścieżka do danych obiektów blob >**: Jeśli plik obiektu blob do przekazania do tabeli Hive znajduje się w domyślnym kontenerze klastra usługi HDInsight Hadoop *&#60; ścieżka do danych obiektów blob >* powinien być w formacie *" wasb: / / / &#60; katalog, w tym kontenerze > / &#60; nazwa pliku obiektu blob > "*.</span><span class="sxs-lookup"><span data-stu-id="e00e1-201">**&#60;path to blob data>**: If the blob file to be uploaded to the Hive table is in the default container of the HDInsight Hadoop cluster, the *&#60;path to blob data>* should be in the format *'wasb:///&#60;directory in this container>/&#60;blob file name>'*.</span></span> <span data-ttu-id="e00e1-202">Można też pliku obiektu blob w kontenerze dodatkowe klastra usługi HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="e00e1-202">The blob file can also be in an additional container of the HDInsight Hadoop cluster.</span></span> <span data-ttu-id="e00e1-203">W takim przypadku *&#60; ścieżka do danych obiektów blob >* powinien być w formacie *"wasb: / / &#60; nazwa kontenera > @&#60; nazwa konta magazynu >.blob.core.windows.net/ &#60; nazwa pliku obiektu blob >"*.</span><span class="sxs-lookup"><span data-stu-id="e00e1-203">In this case, *&#60;path to blob data>* should be in the format *'wasb://&#60;container name>@&#60;storage account name>.blob.core.windows.net/&#60;blob file name>'*.</span></span>

  > [!NOTE]
  > <span data-ttu-id="e00e1-204">Dane obiektu blob do przekazania do tabeli Hive musi się znajdować w domyślnych lub dodatkowego kontenera konta magazynu dla klastra usługi Hadoop.</span><span class="sxs-lookup"><span data-stu-id="e00e1-204">The blob data to be uploaded to Hive table has to be in the default or additional container of the storage account for the Hadoop cluster.</span></span> <span data-ttu-id="e00e1-205">W przeciwnym razie *danych obciążenia* działanie nie powiodło się Strona skarżąca, że nie można uzyskać dostępu do danych.</span><span class="sxs-lookup"><span data-stu-id="e00e1-205">Otherwise, the *LOAD DATA* query fails complaining that it cannot access the data.</span></span>
  >
  >

## <span data-ttu-id="e00e1-206"><a name="partition-orc"></a>Tematy zaawansowane: podzielona na partycje tabeli i magazynu danych gałęzi w formacie ORC</span><span class="sxs-lookup"><span data-stu-id="e00e1-206"><a name="partition-orc"></a>Advanced topics: partitioned table and store Hive data in ORC format</span></span>
<span data-ttu-id="e00e1-207">W przypadku dużych danych partycjonowania tabeli jest korzystne dla zapytań, które należy tylko skanowanie kilka partycji tabeli.</span><span class="sxs-lookup"><span data-stu-id="e00e1-207">If the data is large, partitioning the table is beneficial for queries that only need to scan a few partitions of the table.</span></span> <span data-ttu-id="e00e1-208">Na przykład jest uzasadnione do partycjonowania danych dziennika witryny sieci web według daty.</span><span class="sxs-lookup"><span data-stu-id="e00e1-208">For instance, it is reasonable to partition the log data of a web site by dates.</span></span>

<span data-ttu-id="e00e1-209">Oprócz partycje tabele programu Hive, jest również przydatne do przechowywania danych gałęzi w formacie zoptymalizowanych pod kątem wiersza kolumnowy (ORC).</span><span class="sxs-lookup"><span data-stu-id="e00e1-209">In addition to partitioning Hive tables, it is also beneficial to store the Hive data in the Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="e00e1-210">Aby uzyskać więcej informacji na ORC formatowania, zobacz <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">plików ORC przy użyciu zwiększa wydajność podczas czytania, zapisywania i przetwarzania danych Hive</a>.</span><span class="sxs-lookup"><span data-stu-id="e00e1-210">For more information on ORC formatting, see <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">Using ORC files improves performance when Hive is reading, writing, and processing data</a>.</span></span>

### <a name="partitioned-table"></a><span data-ttu-id="e00e1-211">Tabeli partycjonowanej</span><span class="sxs-lookup"><span data-stu-id="e00e1-211">Partitioned table</span></span>
<span data-ttu-id="e00e1-212">Oto zapytania Hive, które tworzy tabeli partycjonowanej i ładuje dane do niego.</span><span class="sxs-lookup"><span data-stu-id="e00e1-212">Here is the Hive query that creates a partitioned table and loads data into it.</span></span>

    CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<table name>
    (field1 string,
    ...
    fieldN string
    )
    PARTITIONED BY (<partitionfieldname> vartype) ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
         lines terminated by '<line separator>' TBLPROPERTIES("skip.header.line.count"="1");
    LOAD DATA INPATH '<path to the source file>' INTO TABLE <database name>.<partitioned table name>
        PARTITION (<partitionfieldname>=<partitionfieldvalue>);

<span data-ttu-id="e00e1-213">Podczas wykonywania zapytania partycjonowane tabele, zalecane jest aby dodać warunek partycji w **początku** z `where` skuteczności wyszukiwanie znacznie zwiększa klauzuli jako to.</span><span class="sxs-lookup"><span data-stu-id="e00e1-213">When querying partitioned tables, it is recommended to add the partition condition in the **beginning** of the `where` clause as this improves the efficacy of searching significantly.</span></span>

    select
        field1, field2, ..., fieldN
    from <database name>.<partitioned table name>
    where <partitionfieldname>=<partitionfieldvalue> and ...;

### <span data-ttu-id="e00e1-214"><a name="orc"></a>Przechowywanie danych gałęzi w formacie ORC</span><span class="sxs-lookup"><span data-stu-id="e00e1-214"><a name="orc"></a>Store Hive data in ORC format</span></span>
<span data-ttu-id="e00e1-215">Nie można bezpośrednio ładowanie danych z magazynu obiektów blob do gałęzi tabel, które są przechowywane w formacie ORC.</span><span class="sxs-lookup"><span data-stu-id="e00e1-215">You cannot directly load data from blob storage into Hive tables that is stored in the ORC format.</span></span> <span data-ttu-id="e00e1-216">Poniżej przedstawiono kroki, które należy wykonać, aby załadować dane platformy Azure z obiektów blob do tabele programu Hive przechowywane w formacie ORC.</span><span class="sxs-lookup"><span data-stu-id="e00e1-216">Here are the steps that the you need to take to load data from Azure blobs to Hive tables stored in ORC format.</span></span>

<span data-ttu-id="e00e1-217">Tworzenie tabeli zewnętrznej **TEXTFILE AS PRZECHOWYWANE** i ładowanie danych z magazynu obiektów blob do tabeli.</span><span class="sxs-lookup"><span data-stu-id="e00e1-217">Create an external table **STORED AS TEXTFILE** and load data from blob storage to the table.</span></span>

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

        LOAD DATA INPATH '<path to the source file>' INTO TABLE <database name>.<table name>;

<span data-ttu-id="e00e1-218">Tworzenie wewnętrznej tabeli z tym samym schematem co tabeli zewnętrznej w kroku 1, z tym samym ogranicznik pola i przechowywania danych gałęzi w formacie ORC.</span><span class="sxs-lookup"><span data-stu-id="e00e1-218">Create an internal table with the same schema as the external table in step 1, with the same field delimiter, and store the Hive data in the ORC format.</span></span>

        CREATE TABLE IF NOT EXISTS <database name>.<ORC table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' STORED AS ORC;

<span data-ttu-id="e00e1-219">Wybierz dane z tabeli zewnętrznej w kroku 1 i Wstaw do tabeli ORC</span><span class="sxs-lookup"><span data-stu-id="e00e1-219">Select data from the external table in step 1 and insert into the ORC table</span></span>

        INSERT OVERWRITE TABLE <database name>.<ORC table name>
            SELECT * FROM <database name>.<external textfile table name>;

> [!NOTE]
> <span data-ttu-id="e00e1-220">Jeśli w tabeli TEXTFILE *&#60; Nazwa bazy danych >. &#60; Nazwa tabeli zewnętrznej textfile >* zawiera partycje, w KROKU 3 `SELECT * FROM <database name>.<external textfile table name>` polecenia wybiera zmiennej partycji jako pole w zestawie danych zwracanych.</span><span class="sxs-lookup"><span data-stu-id="e00e1-220">If the TEXTFILE table *&#60;database name>.&#60;external textfile table name>* has partitions, in STEP 3, the `SELECT * FROM <database name>.<external textfile table name>` command selects the partition variable as a field in the returned data set.</span></span> <span data-ttu-id="e00e1-221">Wstawianie do *&#60; Nazwa bazy danych >. &#60; Nazwa tabeli ORC >* nie powiedzie się, ponieważ *&#60; Nazwa bazy danych >. &#60; Nazwa tabeli ORC >* nie ma partycji zmiennej jako pola w schemacie tabeli.</span><span class="sxs-lookup"><span data-stu-id="e00e1-221">Inserting it into the *&#60;database name>.&#60;ORC table name>* fails since *&#60;database name>.&#60;ORC table name>* does not have the partition variable as a field in the table schema.</span></span> <span data-ttu-id="e00e1-222">W takim przypadku należy wybrać pola, które ma zostać wstawiony do *&#60; Nazwa bazy danych >. &#60; Nazwa tabeli ORC >* w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="e00e1-222">In this case, you need to specifically select the fields to be inserted to *&#60;database name>.&#60;ORC table name>* as follows:</span></span>
>
>

        INSERT OVERWRITE TABLE <database name>.<ORC table name> PARTITION (<partition variable>=<partition value>)
           SELECT field1, field2, ..., fieldN
           FROM <database name>.<external textfile table name>
           WHERE <partition variable>=<partition value>;

<span data-ttu-id="e00e1-223">Można bezpiecznie usunąć *&#60; Nazwa tabeli zewnętrznej textfile >* po po wszystkich danych za pomocą następującej kwerendy został wstawiony do *&#60; Nazwa bazy danych >. &#60; Nazwa tabeli ORC >*:</span><span class="sxs-lookup"><span data-stu-id="e00e1-223">It is safe to drop the *&#60;external textfile table name>* when using the following query after all data has been inserted into *&#60;database name>.&#60;ORC table name>*:</span></span>

        DROP TABLE IF EXISTS <database name>.<external textfile table name>;

<span data-ttu-id="e00e1-224">Po wykonaniu tej procedury, powinien mieć tabelę z danymi w formacie ORC gotowe do użycia.</span><span class="sxs-lookup"><span data-stu-id="e00e1-224">After following this procedure, you should have a table with data in the ORC format ready to use.</span></span>  
