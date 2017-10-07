---
title: "aaaQuery danych z systemu plików HDFS zgodnego magazynu Azure - Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooquery danych z magazynu Azure i usługi Azure Data Lake Store toostore wyniki analiz."
keywords: blob storage,hdfs,structured data,unstructured data,data lake store,Hadoop input,Hadoop output, hadoop storage, hdfs input,hdfs output,hdfs storage,wasb azure
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 1d2e65f2-16de-449e-915f-3ffbc230f815
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: jgao
ms.openlocfilehash: 1032d60424b65e3c0c54a25c7c15970b017a788f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-storage-with-azure-hdinsight-clusters"></a><span data-ttu-id="90086-104">Korzystanie z usługi Azure Storage w połączeniu z klastrami usługi Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="90086-104">Use Azure storage with Azure HDInsight clusters</span></span>

<span data-ttu-id="90086-105">dane tooanalyze w klastrze usługi HDInsight, dane można przechowywać hello w usłudze Azure Storage i Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="90086-105">tooanalyze data in HDInsight cluster, you can store hello data either in Azure Storage, Azure Data Lake Store, or both.</span></span> <span data-ttu-id="90086-106">Obie te opcje magazynu Włącz toosafely usunąć klastrów usługi HDInsight używane do obliczeń bez utraty danych użytkownika.</span><span class="sxs-lookup"><span data-stu-id="90086-106">Both storage options enable you toosafely delete HDInsight clusters that are used for computation without losing user data.</span></span>

<span data-ttu-id="90086-107">Platforma Hadoop obsługuje pojęcie domyślnego systemu plików hello.</span><span class="sxs-lookup"><span data-stu-id="90086-107">Hadoop supports a notion of hello default file system.</span></span> <span data-ttu-id="90086-108">system plików domyślne Hello wyznacza domyślny schemat i urząd.</span><span class="sxs-lookup"><span data-stu-id="90086-108">hello default file system implies a default scheme and authority.</span></span> <span data-ttu-id="90086-109">Można także używane tooresolve ścieżek względnych.</span><span class="sxs-lookup"><span data-stu-id="90086-109">It can also be used tooresolve relative paths.</span></span> <span data-ttu-id="90086-110">Podczas procesu tworzenia klastra usługi HDInsight hello można określić kontenera obiektów blob w magazynie Azure jako domyślny system plików hello, lub z HDInsight 3.5, można wybrać magazyn Azure lub usługi Azure Data Lake Store jako system plików domyślne hello kilka wyjątków.</span><span class="sxs-lookup"><span data-stu-id="90086-110">During hello HDInsight cluster creation process, you can specify a blob container in Azure Storage as hello default file system, or with HDInsight 3.5, you can select either Azure Storage or Azure Data Lake Store as hello default files system with a few exceptions.</span></span> <span data-ttu-id="90086-111">Aby hello możliwość wykorzystania usługi Data Lake Store jako domyślny hello i magazynu połączone, zobacz [dostępność dla klastra usługi HDInsight](./hdinsight-hadoop-use-data-lake-store.md#availabilities-for-hdinsight-clusters).</span><span class="sxs-lookup"><span data-stu-id="90086-111">For hello supportability of using Data Lake Store as both hello default and linked storage, see [Availabilities for HDInsight cluster](./hdinsight-hadoop-use-data-lake-store.md#availabilities-for-hdinsight-clusters).</span></span>

<span data-ttu-id="90086-112">W tym artykule omówiono współdziałanie usługi Azure Storage z klastrami usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="90086-112">In this article, you learn how Azure Storage works with HDInsight clusters.</span></span> <span data-ttu-id="90086-113">toolearn Data Lake Store współpracuje z klastrami HDInsight, zobacz [użycia usługi Azure Data Lake Store z usługą Azure HDInsight clusters](hdinsight-hadoop-use-data-lake-store.md).</span><span class="sxs-lookup"><span data-stu-id="90086-113">toolearn how Data Lake Store works with HDInsight clusters, see [Use Azure Data Lake Store with Azure HDInsight clusters](hdinsight-hadoop-use-data-lake-store.md).</span></span> <span data-ttu-id="90086-114">Więcej informacji dotyczących tworzenia klastra usługi HDInsight można znaleźć w artykule [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md) (Tworzenie klastrów platformy Hadoop w usłudze HDInsight).</span><span class="sxs-lookup"><span data-stu-id="90086-114">For more information about creating an HDInsight cluster, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

<span data-ttu-id="90086-115">Usługa Azure Storage to niezawodne rozwiązanie ogólnego przeznaczenia, które bezproblemowo integruje się z usługą HDInsight.</span><span class="sxs-lookup"><span data-stu-id="90086-115">Azure storage is a robust, general-purpose storage solution that integrates seamlessly with HDInsight.</span></span> <span data-ttu-id="90086-116">HDInsight można użyć kontenera obiektów blob w magazynie Azure jako hello domyślnego systemu plików dla klastra hello.</span><span class="sxs-lookup"><span data-stu-id="90086-116">HDInsight can use a blob container in Azure Storage as hello default file system for hello cluster.</span></span> <span data-ttu-id="90086-117">Za pomocą interfejsu systemu (HDFS) DFS Hadoop hello pełny zestaw składników usługi HDInsight może operować bezpośrednio na danych strukturalnych lub bez struktury przechowywanych jako obiekty BLOB.</span><span class="sxs-lookup"><span data-stu-id="90086-117">Through a Hadoop distributed file system (HDFS) interface, hello full set of components in HDInsight can operate directly on structured or unstructured data stored as blobs.</span></span>

> [!WARNING]
> <span data-ttu-id="90086-118">Podczas tworzenia konta usługi Azure Storage jest dostępnych kilka opcji.</span><span class="sxs-lookup"><span data-stu-id="90086-118">There are several options available when creating an Azure Storage account.</span></span> <span data-ttu-id="90086-119">Witaj w poniższej tabeli podano informacje, na jakie opcje są obsługiwane z usługą HDInsight:</span><span class="sxs-lookup"><span data-stu-id="90086-119">hello following table provides information on what options are supported with HDInsight:</span></span>
> 
> | <span data-ttu-id="90086-120">Typ konta magazynu</span><span class="sxs-lookup"><span data-stu-id="90086-120">Storage account type</span></span> | <span data-ttu-id="90086-121">Warstwa magazynu</span><span class="sxs-lookup"><span data-stu-id="90086-121">Storage tier</span></span> | <span data-ttu-id="90086-122">Obsługiwane z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="90086-122">Supported with HDInsight</span></span> |
> | ------- | ------- | ------- |
> | <span data-ttu-id="90086-123">Konto magazynu ogólnego przeznaczenia</span><span class="sxs-lookup"><span data-stu-id="90086-123">General-purpose Storage Account</span></span> | <span data-ttu-id="90086-124">Standardowa</span><span class="sxs-lookup"><span data-stu-id="90086-124">Standard</span></span> | <span data-ttu-id="90086-125">__Tak__</span><span class="sxs-lookup"><span data-stu-id="90086-125">__Yes__</span></span> |
> | &nbsp; | <span data-ttu-id="90086-126">Premium</span><span class="sxs-lookup"><span data-stu-id="90086-126">Premium</span></span> | <span data-ttu-id="90086-127">Nie</span><span class="sxs-lookup"><span data-stu-id="90086-127">No</span></span> |
> | <span data-ttu-id="90086-128">Konto magazynu obiektów blob</span><span class="sxs-lookup"><span data-stu-id="90086-128">Blob Storage Account</span></span> | <span data-ttu-id="90086-129">Gorąca</span><span class="sxs-lookup"><span data-stu-id="90086-129">Hot</span></span> | <span data-ttu-id="90086-130">Nie</span><span class="sxs-lookup"><span data-stu-id="90086-130">No</span></span> |
> | &nbsp; | <span data-ttu-id="90086-131">Chłodna</span><span class="sxs-lookup"><span data-stu-id="90086-131">Cool</span></span> | <span data-ttu-id="90086-132">Nie</span><span class="sxs-lookup"><span data-stu-id="90086-132">No</span></span> |

<span data-ttu-id="90086-133">Nie zaleca się użycie hello domyślnego kontenera obiektów blob do przechowywania danych biznesowych.</span><span class="sxs-lookup"><span data-stu-id="90086-133">We do not recommend that you use hello default blob container for storing business data.</span></span> <span data-ttu-id="90086-134">Usunięcie domyślnego kontenera obiektów blob powitania po każdym tooreduce Użyj przestrzeni magazynowej jest dobrym rozwiązaniem.</span><span class="sxs-lookup"><span data-stu-id="90086-134">Deleting hello default blob container after each use tooreduce storage cost is a good practice.</span></span> <span data-ttu-id="90086-135">Uwaga kontenera domyślnego hello zawierającym węzły aplikacji i systemu dzienników.</span><span class="sxs-lookup"><span data-stu-id="90086-135">Note that hello default container contains application and system logs.</span></span> <span data-ttu-id="90086-136">Upewnij się, że tooretrieve hello dzienniki przed usunięciem hello kontenera.</span><span class="sxs-lookup"><span data-stu-id="90086-136">Make sure tooretrieve hello logs before deleting hello container.</span></span>

<span data-ttu-id="90086-137">Udostępnianie jednego kontenera obiektów blob dla wielu klastrów nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="90086-137">Sharing one blob container for multiple clusters is not supported.</span></span>

## <a name="hdinsight-storage-architecture"></a><span data-ttu-id="90086-138">Architektura magazynu usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="90086-138">HDInsight storage architecture</span></span>
<span data-ttu-id="90086-139">powitania po diagram zawiera abstrakcyjny widok architektury magazynu usługi HDInsight przy użyciu usługi Azure Storage hello:</span><span class="sxs-lookup"><span data-stu-id="90086-139">hello following diagram provides an abstract view of hello HDInsight storage architecture of using Azure Storage:</span></span>

<span data-ttu-id="90086-140">![Klastry Hadoop Użyj hello interfejsu API systemu plików HDFS tooaccess i przechowywania danych strukturalnych i bez struktury w magazynie obiektów Blob. ] (./media/hdinsight-hadoop-use-blob-storage/HDI.WASB.Arch.png "Architektura magazynu usługi HDInsight")</span><span class="sxs-lookup"><span data-stu-id="90086-140">![Hadoop clusters use hello HDFS API tooaccess and store structured and unstructured data in Blob storage.](./media/hdinsight-hadoop-use-blob-storage/HDI.WASB.Arch.png "HDInsight Storage Architecture")</span></span>

<span data-ttu-id="90086-141">Usługa HDInsight zapewnia dostęp do systemu plików toohello rozproszonych, który jest lokalnie dołączony toohello węzłów obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="90086-141">HDInsight provides access toohello distributed file system that is locally attached toohello compute nodes.</span></span> <span data-ttu-id="90086-142">W tym systemie plików jest możliwy za pomocą hello w pełni kwalifikowana identyfikatora URI, na przykład:</span><span class="sxs-lookup"><span data-stu-id="90086-142">This file system can be accessed by using hello fully qualified URI, for example:</span></span>

    hdfs://<namenodehost>/<path>

<span data-ttu-id="90086-143">Ponadto HDInsight umożliwia tooaccess danych przechowywanych w usłudze Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="90086-143">In addition, HDInsight allows you tooaccess data that is stored in Azure Storage.</span></span> <span data-ttu-id="90086-144">Składnia Hello jest następująca:</span><span class="sxs-lookup"><span data-stu-id="90086-144">hello syntax is:</span></span>

    wasb[s]://<containername>@<accountname>.blob.core.windows.net/<path>

<span data-ttu-id="90086-145">Poniżej przedstawiono kilka zagadnień dotyczących korzystania z konta usługi Azure Storage w połączeniu z klastrami usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="90086-145">Here are some considerations when using Azure Storage account with HDInsight clusters.</span></span>

* <span data-ttu-id="90086-146">**Kontenery na kontach magazynu hello, które są połączone tooa klastra:** ponieważ hello nazwę konta i klucz są skojarzone z klastrem hello podczas tworzenia, masz pełny dostęp do toohello obiektów blob w tych kontenerach.</span><span class="sxs-lookup"><span data-stu-id="90086-146">**Containers in hello storage accounts that are connected tooa cluster:** Because hello account name and key are associated with hello cluster during creation, you have full access toohello blobs in those containers.</span></span>

* <span data-ttu-id="90086-147">**Publiczne kontenery lub publiczne obiekty BLOB na kontach magazynu, które nie są połączone klastra tooa:** masz uprawnienia tylko do odczytu toohello BLOB w kontenerach hello.</span><span class="sxs-lookup"><span data-stu-id="90086-147">**Public containers or public blobs in storage accounts that are NOT connected tooa cluster:** You have read-only permission toohello blobs in hello containers.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="90086-148">Kontenery publiczne pozwalają tooget listę wszystkich obiektów blob, które są dostępne w danym kontenerze oraz pobranie metadanych kontenera.</span><span class="sxs-lookup"><span data-stu-id="90086-148">Public containers allow you tooget a list of all blobs that are available in that container and get container metadata.</span></span> <span data-ttu-id="90086-149">Publiczne obiekty BLOB umożliwiają tooaccess hello blob jedynie osobom znającym dokładny adres URL hello.</span><span class="sxs-lookup"><span data-stu-id="90086-149">Public blobs allow you tooaccess hello blobs only if you know hello exact URL.</span></span> <span data-ttu-id="90086-150">Aby uzyskać więcej informacji, zobacz <a href="http://msdn.microsoft.com/library/windowsazure/dd179354.aspx">ograniczanie dostępu toocontainers i obiekty BLOB</a>.</span><span class="sxs-lookup"><span data-stu-id="90086-150">For more information, see <a href="http://msdn.microsoft.com/library/windowsazure/dd179354.aspx">Restrict access toocontainers and blobs</a>.</span></span>
  > 
  > 
* <span data-ttu-id="90086-151">**Prywatne kontenery na kontach magazynu, które nie są połączone w klaster tooa:** nie masz dostępu do obiektów blob hello w kontenerach hello chyba że zdefiniujesz konto magazynu hello podczas przesyłania zadań WebHCat hello.</span><span class="sxs-lookup"><span data-stu-id="90086-151">**Private containers in storage accounts that are NOT connected tooa cluster:** You can't access hello blobs in hello containers unless you define hello storage account when you submit hello WebHCat jobs.</span></span> <span data-ttu-id="90086-152">Wyjaśnienie jest zawarte w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="90086-152">This is explained later in this article.</span></span>

<span data-ttu-id="90086-153">Witaj kontach magazynu, które są definiowane w procesie tworzenia hello i ich kluczy są przechowywane w %HADOOP_HOME%/conf/core-site.xml w węzłach klastra hello.</span><span class="sxs-lookup"><span data-stu-id="90086-153">hello storage accounts that are defined in hello creation process and their keys are stored in %HADOOP_HOME%/conf/core-site.xml on hello cluster nodes.</span></span> <span data-ttu-id="90086-154">domyślne zachowanie Hello HDInsight jest kont magazynu hello toouse zdefiniowanych w pliku core-site.xml hello.</span><span class="sxs-lookup"><span data-stu-id="90086-154">hello default behavior of HDInsight is toouse hello storage accounts defined in hello core-site.xml file.</span></span> <span data-ttu-id="90086-155">To ustawienie możesz zmodyfikować przy użyciu narzędzia [Ambari](./hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="90086-155">You can modify this setting using [Ambari](./hdinsight-hadoop-manage-ambari.md)</span></span>

<span data-ttu-id="90086-156">Wiele zadań WebHCat, w tym Hive, MapReduce, przesyłanie strumieniowe Hadoop, a także Pig, może przenosić ze sobą opis kont magazynu i metadane.</span><span class="sxs-lookup"><span data-stu-id="90086-156">Multiple WebHCat jobs, including Hive, MapReduce, Hadoop streaming, and Pig, can carry a description of storage accounts and metadata with them.</span></span> <span data-ttu-id="90086-157">(W przypadku technologii Pig obecnie działa to z kontami magazynu, ale nie dla metadanych). Aby uzyskać więcej informacji, zobacz [Using an HDInsight Cluster with Alternate Storage Accounts and Metastores](http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx) (Używanie klastra usługi HDInsight z alternatywnymi kontami magazynu i magazynami metadanych).</span><span class="sxs-lookup"><span data-stu-id="90086-157">(This currently works for Pig with storage accounts, but not for metadata.) For more information, see [Using an HDInsight Cluster with Alternate Storage Accounts and Metastores](http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx).</span></span>

<span data-ttu-id="90086-158">Obiekty blob mogą być używane z danymi ze strukturą i bez niej.</span><span class="sxs-lookup"><span data-stu-id="90086-158">Blobs can be used for structured and unstructured data.</span></span> <span data-ttu-id="90086-159">Kontenery obiektów blob przechowują dane jako pary klucz/wartość, bez hierarchii katalogów.</span><span class="sxs-lookup"><span data-stu-id="90086-159">Blob containers store data as key/value pairs, and there is no directory hierarchy.</span></span> <span data-ttu-id="90086-160">Jednak hello znaku ukośnika (/) może być używana w hello toomake nazwa klucza wydaje się tak, jakby plik był przechowywany w ramach struktury katalogów.</span><span class="sxs-lookup"><span data-stu-id="90086-160">However hello slash character ( / ) can be used within hello key name toomake it appear as if a file is stored within a directory structure.</span></span> <span data-ttu-id="90086-161">Na przykład klucz obiektu blob może mieć postać *input/log1.txt*.</span><span class="sxs-lookup"><span data-stu-id="90086-161">For example, a blob's key may be *input/log1.txt*.</span></span> <span data-ttu-id="90086-162">Nie rzeczywiste *wejściowych* katalog istnieje, ale powodu obecności toohello hello znaku ukośnika w nazwie klucza hello, ma wygląd hello ścieżki do pliku.</span><span class="sxs-lookup"><span data-stu-id="90086-162">No actual *input* directory exists, but due toohello presence of hello slash character in hello key name, it has hello appearance of a file path.</span></span>

## <span data-ttu-id="90086-163"><a id="benefits"></a>Korzyści z usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="90086-163"><a id="benefits"></a>Benefits of Azure Storage</span></span>
<span data-ttu-id="90086-164">Witaj DOROZUMIANE skuteczność została osłabiona przez hello sposób tworzenia klastrów obliczeniowych hello zasobów konta magazynu zamknij toohello wewnątrz hello regionu Azure, w którym hello szybkie sieci zapewniają koszt wydajności nie wspólnie lokalizowania klastrów obliczeniowych i zasobów magazynowania efektywne dla węzłów obliczeniowych hello tooaccess hello danych wewnątrz magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="90086-164">hello implied performance cost of not co-locating compute clusters and storage resources is mitigated by hello way hello compute clusters are created close toohello storage account resources inside hello Azure region, where hello high-speed network makes it efficient for hello compute nodes tooaccess hello data inside Azure storage.</span></span>

<span data-ttu-id="90086-165">Istnieje kilka korzyści związanych z przechowywaniem danych hello w magazynie Azure zamiast systemu plików HDFS:</span><span class="sxs-lookup"><span data-stu-id="90086-165">There are several benefits associated with storing hello data in Azure storage instead of HDFS:</span></span>

* <span data-ttu-id="90086-166">**Udostępnianie i ponowne użycie danych:** hello dane w systemie plików HDFS znajdują się wewnątrz klastra obliczeniowego hello.</span><span class="sxs-lookup"><span data-stu-id="90086-166">**Data reuse and sharing:** hello data in HDFS is located inside hello compute cluster.</span></span> <span data-ttu-id="90086-167">Tylko aplikacji hello, które mają dostęp toohello obliczeń klaster może używać hello danych przy użyciu interfejsów API systemu plików HDFS.</span><span class="sxs-lookup"><span data-stu-id="90086-167">Only hello applications that have access toohello compute cluster can use hello data by using HDFS APIs.</span></span> <span data-ttu-id="90086-168">Witaj dane w magazynie Azure są dostępne za pośrednictwem interfejsów API systemu plików HDFS hello lub hello [interfejsów API REST magazynu obiektów Blob][blob-storage-restAPI].</span><span class="sxs-lookup"><span data-stu-id="90086-168">hello data in Azure storage can be accessed either through hello HDFS APIs or through hello [Blob Storage REST APIs][blob-storage-restAPI].</span></span> <span data-ttu-id="90086-169">W związku z tym większy zestaw narzędzi i aplikacji (w tym inne klastry HDInsight) można tooproduce używane i wykorzystują dane hello.</span><span class="sxs-lookup"><span data-stu-id="90086-169">Thus, a larger set of applications (including other HDInsight clusters) and tools can be used tooproduce and consume hello data.</span></span>
* <span data-ttu-id="90086-170">**Archiwizacja danych:** przechowywanie danych w magazynie Azure umożliwia hello klastrów usługi HDInsight używane do obliczeń toobe bezpiecznie usunąć bez utraty danych użytkownika.</span><span class="sxs-lookup"><span data-stu-id="90086-170">**Data archiving:** Storing data in Azure storage enables hello HDInsight clusters used for computation toobe safely deleted without losing user data.</span></span>
* <span data-ttu-id="90086-171">**Koszt magazynowania danych:** przechowywania danych w systemie plików DFS długoterminowej hello jest droższe niż przechowywanie danych hello w magazynie Azure, ponieważ hello koszt klastra obliczeniowego jest wyższy niż koszt hello magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="90086-171">**Data storage cost:** Storing data in DFS for hello long term is more costly than storing hello data in Azure storage because hello cost of a compute cluster is higher than hello cost of Azure storage.</span></span> <span data-ttu-id="90086-172">Ponadto ponieważ hello danych nie ma toobe ponownie załadowana każdej generacji klastra obliczeniowego, oszczędzamy również koszty ładowania danych.</span><span class="sxs-lookup"><span data-stu-id="90086-172">In addition, because hello data does not have toobe reloaded for every compute cluster generation, you are also saving data loading costs.</span></span>
* <span data-ttu-id="90086-173">**Elastyczne skalowalnego w poziomie:** Chociaż system plików HDFS zapewnia system plików skalowalnych w poziomie, skala hello jest określany przez hello liczbę węzłów tworzonych dla klastra.</span><span class="sxs-lookup"><span data-stu-id="90086-173">**Elastic scale-out:** Although HDFS provides you with a scaled-out file system, hello scale is determined by hello number of nodes that you create for your cluster.</span></span> <span data-ttu-id="90086-174">Zmiana skali hello może stać się procesem bardziej skomplikowane niż polegania na elastyczne hello możliwościami skalowania, które można uzyskać automatycznie w magazynie Azure.</span><span class="sxs-lookup"><span data-stu-id="90086-174">Changing hello scale can become a more complicated process than relying on hello elastic scaling capabilities that you get automatically in Azure storage.</span></span>
* <span data-ttu-id="90086-175">**Replikacja geograficzna:** usługę Azure Storage można replikować geograficznie.</span><span class="sxs-lookup"><span data-stu-id="90086-175">**Geo-replication:** Your Azure storage can be geo-replicated.</span></span> <span data-ttu-id="90086-176">Chociaż zapewnia to odzyskiwanie geograficzne i nadmiarowość danych, lokalizacji zreplikowanych geograficznie trybu failover toohello poważnie wpływa na wydajność i może pociągnąć za sobą dodatkowe koszty.</span><span class="sxs-lookup"><span data-stu-id="90086-176">Although this gives you geographic recovery and data redundancy, a failover toohello geo-replicated location severely impacts your performance, and it may incur additional costs.</span></span> <span data-ttu-id="90086-177">Dlatego zalecamy toochoose hello — replikacja geograficzna rozsądny sposób i tylko wtedy, gdy wartość hello hello danych uzasadnia ponoszenie dodatkowych kosztów hello.</span><span class="sxs-lookup"><span data-stu-id="90086-177">So our recommendation is toochoose hello geo-replication wisely and only if hello value of hello data is worth hello additional cost.</span></span>

<span data-ttu-id="90086-178">Niektóre zadania i pakiety MapReduce mogą tworzyć wyniki pośrednie, że nie naprawdę chcesz toostore w magazynie Azure.</span><span class="sxs-lookup"><span data-stu-id="90086-178">Certain MapReduce jobs and packages may create intermediate results that you don't really want toostore in Azure storage.</span></span> <span data-ttu-id="90086-179">W tym przypadku można wybrać toostore hello danych w hello lokalnego systemu plików HDFS.</span><span class="sxs-lookup"><span data-stu-id="90086-179">In that case, you can elect toostore hello data in hello local HDFS.</span></span> <span data-ttu-id="90086-180">W rzeczywistości HDInsight używa systemu plików DFS dla wielu wyników pośrednich w zadaniach Hive i innych procesach.</span><span class="sxs-lookup"><span data-stu-id="90086-180">In fact, HDInsight uses DFS for several of these intermediate results in Hive jobs and other processes.</span></span>

> [!NOTE]
> <span data-ttu-id="90086-181">Większość poleceń systemu plików HDFS (na przykład <b>ls</b>, <b>copyFromLocal</b> i <b>mkdir</b>) nadal działa zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="90086-181">Most HDFS commands (for example, <b>ls</b>, <b>copyFromLocal</b> and <b>mkdir</b>) still work as expected.</span></span> <span data-ttu-id="90086-182">Tylko hello poleceń, które są określone toohello natywnych implementacji systemu plików HDFS (czyli tooas określonego systemu plików DFS), takich jak <b>fschk</b> i <b>dfsadmin</b>, Pokaż inaczej w magazynie Azure.</span><span class="sxs-lookup"><span data-stu-id="90086-182">Only hello commands that are specific toohello native HDFS implementation (which is referred tooas DFS), such as <b>fschk</b> and <b>dfsadmin</b>, show different behavior in Azure storage.</span></span>
> 
> 

## <a name="create-blob-containers"></a><span data-ttu-id="90086-183">Tworzenie kontenerów obiektów blob</span><span class="sxs-lookup"><span data-stu-id="90086-183">Create Blob containers</span></span>
<span data-ttu-id="90086-184">toouse obiektów blob, należy najpierw utworzyć [konta magazynu Azure][azure-storage-create].</span><span class="sxs-lookup"><span data-stu-id="90086-184">toouse blobs, you first create an [Azure Storage account][azure-storage-create].</span></span> <span data-ttu-id="90086-185">W ramach tego możesz określić region platformy Azure, gdzie hello konto magazynu jest tworzone.</span><span class="sxs-lookup"><span data-stu-id="90086-185">As part of this, you specify an Azure region where hello storage account is created.</span></span> <span data-ttu-id="90086-186">Witaj klaster i konto magazynu hello musi być obsługiwana przez hello tego samego regionu.</span><span class="sxs-lookup"><span data-stu-id="90086-186">hello cluster and hello storage account must be hosted in hello same region.</span></span> <span data-ttu-id="90086-187">Hello Hive potrzeby magazynu metadanych serwera SQL w bazie danych i Oozie potrzeby magazynu metadanych programu SQL Server, bazy danych, również muszą znajdować się w hello tego samego regionu.</span><span class="sxs-lookup"><span data-stu-id="90086-187">hello Hive metastore SQL Server database and Oozie metastore SQL Server database must also be located in hello same region.</span></span>

<span data-ttu-id="90086-188">Wszędzie tam, gdzie go umieszczono, każdy utworzony obiekt blob należy tooa kontenera na koncie magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="90086-188">Wherever it lives, each blob you create belongs tooa container in your Azure Storage account.</span></span> <span data-ttu-id="90086-189">Ten kontener może być istniejącym obiektem blob utworzonym poza usługą HDInsight lub może być kontenerem, który jest tworzony dla klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="90086-189">This container may be an existing blob that was created outside of HDInsight, or it may be a container that is created for an HDInsight cluster.</span></span>

<span data-ttu-id="90086-190">Witaj domyślnego kontenera obiektów Blob przechowuje informacje specyficzne dla klastra, takie jak dzienniki i historię zadań.</span><span class="sxs-lookup"><span data-stu-id="90086-190">hello default Blob container stores cluster-specific information such as job history and logs.</span></span> <span data-ttu-id="90086-191">Nie należy współużytkować domyślnego kontenera obiektów blob dla wielu klastrów usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="90086-191">Don't share a default Blob container with multiple HDInsight clusters.</span></span> <span data-ttu-id="90086-192">Może to spowodować uszkodzenie historii zadań.</span><span class="sxs-lookup"><span data-stu-id="90086-192">This might corrupt job history.</span></span> <span data-ttu-id="90086-193">Zalecane jest toouse innego kontenera dla każdego klastra i umieszczanie udostępnionych danych w połączonym koncie magazynu określonym we wdrożeniu wszystkich odpowiednich klastrów zamiast hello domyślne konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="90086-193">It is recommended toouse a different container for each cluster and put shared data on a linked storage account specified in deployment of all relevant clusters rather than hello default storage account.</span></span> <span data-ttu-id="90086-194">Aby uzyskać więcej informacji na temat konfigurowania połączonych kont magazynu, zobacz artykuł [Tworzenie klastrów usługi HDInsight][hdinsight-creation].</span><span class="sxs-lookup"><span data-stu-id="90086-194">For more information on configuring linked storage accounts, see [Create HDInsight clusters][hdinsight-creation].</span></span> <span data-ttu-id="90086-195">Jednak po usunięciu oryginalnego klastra usługi HDInsight hello można ponownie użyć domyślnego kontenera magazynu.</span><span class="sxs-lookup"><span data-stu-id="90086-195">However you can reuse a default storage container after hello original HDInsight cluster has been deleted.</span></span> <span data-ttu-id="90086-196">W przypadku klastrów HBase faktycznie można zachować schemat tabeli HBase hello i danych przez utworzenie nowego klastra HBase przy użyciu hello domyślnego kontenera obiektów blob używanego przez klaster HBase, który został usunięty.</span><span class="sxs-lookup"><span data-stu-id="90086-196">For HBase clusters, you can actually retain hello HBase table schema and data by creating a new HBase cluster using hello default blob container that is used by an HBase cluster that has been deleted.</span></span>

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]

### <a name="use-hello-azure-portal"></a><span data-ttu-id="90086-197">Użyj hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="90086-197">Use hello Azure portal</span></span>
<span data-ttu-id="90086-198">Podczas tworzenia klastra usługi HDInsight z hello portalu, masz szczegóły konta magazynu tooprovide hello hello opcje (jak pokazano poniżej).</span><span class="sxs-lookup"><span data-stu-id="90086-198">When creating an HDInsight cluster from hello Portal, you have hello options (as shown below) tooprovide hello storage account details.</span></span> <span data-ttu-id="90086-199">Można również określić, czy mają konta dodatkowego magazynu skojarzone z hello klastra i jeśli tak, wybierz z usługi Data Lake Store lub innego obiektu blob magazynu Azure jako hello dodatkowego magazynu.</span><span class="sxs-lookup"><span data-stu-id="90086-199">You can also specify whether you want an additional storage account associated with hello cluster, and if so, choose from Data Lake Store or another Azure Storage blob as hello additional storage.</span></span>

![HDInsight, hadoop, tworzenie źródła danych](./media/hdinsight-hadoop-use-blob-storage/hdinsight.provision.data.source.png)

> [!WARNING]
> <span data-ttu-id="90086-201">Przy użyciu konta, dodatkowe miejsce do magazynowania w innej lokalizacji niż hello klastra usługi HDInsight nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="90086-201">Using an additional storage account in a different location than hello HDInsight cluster is not supported.</span></span>


### <a name="use-azure-powershell"></a><span data-ttu-id="90086-202">Korzystanie z programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="90086-202">Use Azure PowerShell</span></span>
<span data-ttu-id="90086-203">Jeśli użytkownik [zainstalowaniu i skonfigurowaniu programu Azure PowerShell][powershell-install], można użyć poniższych z hello Azure PowerShell monitu toocreate konto magazynu i kontener hello:</span><span class="sxs-lookup"><span data-stu-id="90086-203">If you [installed and configured Azure PowerShell][powershell-install], you can use hello following from hello Azure PowerShell prompt toocreate a storage account and container:</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    $SubscriptionID = "<Your Azure Subscription ID>"
    $ResourceGroupName = "<New Azure Resource Group Name>"
    $Location = "EAST US 2"

    $StorageAccountName = "<New Azure Storage Account Name>"
    $containerName = "<New Azure Blob Container Name>"

    Add-AzureRmAccount
    Select-AzureRmSubscription -SubscriptionId $SubscriptionID

    # Create resource group
    New-AzureRmResourceGroup -name $ResourceGroupName -Location $Location

    # Create default storage account
    New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Location $Location -Type Standard_LRS 

    # Create default blob containers
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -StorageAccountName $StorageAccountName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey  
    New-AzureStorageContainer -Name $containerName -Context $destContext

### <a name="use-azure-cli"></a><span data-ttu-id="90086-204">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="90086-204">Use Azure CLI</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

<span data-ttu-id="90086-205">Jeśli masz [zainstalowany i skonfigurowany hello Azure CLI](../cli-install-nodejs.md), hello następujące polecenie, mogą być używane tooa konto magazynu i kontener.</span><span class="sxs-lookup"><span data-stu-id="90086-205">If you have [installed and configured hello Azure CLI](../cli-install-nodejs.md), hello following command can be used tooa storage account and container.</span></span>

    azure storage account create <storageaccountname> --type LRS

> [!NOTE]
> <span data-ttu-id="90086-206">Witaj `--type` parametr wskazuje sposób replikacji konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="90086-206">hello `--type` parameter indicates how hello storage account is replicated.</span></span> <span data-ttu-id="90086-207">Aby uzyskać więcej informacji, zobacz artykuł [Azure Storage Replication](../storage/storage-redundancy.md) (Replikacja usługi Azure Storage).</span><span class="sxs-lookup"><span data-stu-id="90086-207">For more information, see [Azure Storage Replication](../storage/storage-redundancy.md).</span></span> <span data-ttu-id="90086-208">Nie używaj magazynu strefowo nadmiarowego, ponieważ nie obsługuje on stronicowych obiektów blob, plików, tabel ani kolejek.</span><span class="sxs-lookup"><span data-stu-id="90086-208">Don't use ZRS as ZRS doesn't support page blob, file, table, or queue.</span></span>
> 
> 

<span data-ttu-id="90086-209">Jesteś toospecify zostanie wyświetlony monit o hello region geograficzny w utworzeniu konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="90086-209">You are prompted toospecify hello geographic region that hello storage account is created in.</span></span> <span data-ttu-id="90086-210">Należy utworzyć konta magazynu hello w hello tym samym regionie, w którym planujesz utworzenie klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="90086-210">You should create hello storage account in hello same region that you plan on creating your HDInsight cluster.</span></span>

<span data-ttu-id="90086-211">Po utworzeniu konta magazynu hello Użyj hello następujące klucze konta magazynu hello tooretrieve polecenia:</span><span class="sxs-lookup"><span data-stu-id="90086-211">Once hello storage account is created, use hello following command tooretrieve hello storage account keys:</span></span>

    azure storage account keys list <storageaccountname>

<span data-ttu-id="90086-212">toocreate kontener hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="90086-212">toocreate a container, use hello following command:</span></span>

    azure storage container create <containername> --account-name <storageaccountname> --account-key <storageaccountkey>

## <a name="address-files-in-azure-storage"></a><span data-ttu-id="90086-213">Adresowanie plików w usłudze Azure Storage</span><span class="sxs-lookup"><span data-stu-id="90086-213">Address files in Azure storage</span></span>
<span data-ttu-id="90086-214">schemat identyfikatora URI Hello dla uzyskiwania dostępu do plików w magazynie Azure z usługi HDInsight to:</span><span class="sxs-lookup"><span data-stu-id="90086-214">hello URI scheme for accessing files in Azure storage from HDInsight is:</span></span>

    wasb[s]://<BlobStorageContainerName>@<StorageAccountName>.blob.core.windows.net/<path>

<span data-ttu-id="90086-215">Witaj schemat identyfikatora URI zapewnia nieszyfrowany dostęp (z hello *wasb:* prefiks) oraz szyfrowany dostęp SSL (z *wasbs*).</span><span class="sxs-lookup"><span data-stu-id="90086-215">hello URI scheme provides unencrypted access (with hello *wasb:* prefix) and SSL encrypted access (with *wasbs*).</span></span> <span data-ttu-id="90086-216">Firma Microsoft zaleca używanie *wasbs* wszędzie tam, gdzie to możliwe, nawet wtedy, gdy podczas uzyskiwania dostępu do danych, które znajdują się wewnątrz hello tego samego regionu w systemie Azure.</span><span class="sxs-lookup"><span data-stu-id="90086-216">We recommend using *wasbs* wherever possible, even when accessing data that lives inside hello same region in Azure.</span></span>

<span data-ttu-id="90086-217">Witaj &lt;BlobStorageContainerName&gt; identyfikuje nazwę hello hello kontenera obiektów blob w magazynie Azure.</span><span class="sxs-lookup"><span data-stu-id="90086-217">hello &lt;BlobStorageContainerName&gt; identifies hello name of hello blob container in Azure storage.</span></span>
<span data-ttu-id="90086-218">Witaj &lt;StorageAccountName&gt; identyfikuje nazwę konta usługi Azure Storage hello.</span><span class="sxs-lookup"><span data-stu-id="90086-218">hello &lt;StorageAccountName&gt; identifies hello Azure Storage account name.</span></span> <span data-ttu-id="90086-219">Wymagana jest w pełni kwalifikowana nazwa domeny (FQDN).</span><span class="sxs-lookup"><span data-stu-id="90086-219">A fully qualified domain name (FQDN) is required.</span></span>

<span data-ttu-id="90086-220">Jeśli żadna &lt;BlobStorageContainerName&gt; ani &lt;StorageAccountName&gt; został określony, domyślny system plików hello jest używany.</span><span class="sxs-lookup"><span data-stu-id="90086-220">If neither &lt;BlobStorageContainerName&gt; nor &lt;StorageAccountName&gt; has been specified, hello default file system is used.</span></span> <span data-ttu-id="90086-221">Dla plików hello na powitania domyślnego systemu plików można użyć ścieżkę względną lub ścieżką bezwzględną.</span><span class="sxs-lookup"><span data-stu-id="90086-221">For hello files on hello default file system, you can use a relative path or an absolute path.</span></span> <span data-ttu-id="90086-222">Na przykład Witaj *hadoop-mapreduce-examples.jar* dostarczanego z klastrami usługi HDInsight może być określony tooby przy użyciu jednej z następujących hello:</span><span class="sxs-lookup"><span data-stu-id="90086-222">For example, hello *hadoop-mapreduce-examples.jar* file that comes with HDInsight clusters can be referred tooby using one of hello following:</span></span>

    wasb://mycontainer@myaccount.blob.core.windows.net/example/jars/hadoop-mapreduce-examples.jar
    wasb:///example/jars/hadoop-mapreduce-examples.jar
    /example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> <span data-ttu-id="90086-223">Nazwa pliku Hello jest <i>hadoop-examples.jar</i> w klastrach usługi HDInsight w wersji 2.1 i 1.6.</span><span class="sxs-lookup"><span data-stu-id="90086-223">hello file name is <i>hadoop-examples.jar</i> in HDInsight versions 2.1 and 1.6 clusters.</span></span>
> 
> 

<span data-ttu-id="90086-224">Witaj &lt;ścieżki&gt; jest hello pliku lub katalogu systemu plików HDFS nazwą ścieżki.</span><span class="sxs-lookup"><span data-stu-id="90086-224">hello &lt;path&gt; is hello file or directory HDFS path name.</span></span> <span data-ttu-id="90086-225">Ponieważ kontenery w usłudze Azure Storage przechowują po prostu pary klucz-wartość, nie istnieje prawdziwy hierarchiczny system plików.</span><span class="sxs-lookup"><span data-stu-id="90086-225">Because containers in Azure storage are simply key-value stores, there is no true hierarchical file system.</span></span> <span data-ttu-id="90086-226">Znak ukośnika (/) wewnątrz klucza obiektu blob jest interpretowany jako separator katalogu.</span><span class="sxs-lookup"><span data-stu-id="90086-226">A slash character ( / ) inside a blob key is interpreted as a directory separator.</span></span> <span data-ttu-id="90086-227">Na przykład nazwą obiektu blob powitania dla *hadoop-mapreduce-examples.jar* jest:</span><span class="sxs-lookup"><span data-stu-id="90086-227">For example, hello blob name for *hadoop-mapreduce-examples.jar* is:</span></span>

    example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> <span data-ttu-id="90086-228">Podczas pracy z obiektami blob poza usługą HDInsight, większość narzędzi nie rozpoznaje formatu WASB hello i zamiast tego oczekuje podstawowego formatu ścieżki, takie jak `example/jars/hadoop-mapreduce-examples.jar`.</span><span class="sxs-lookup"><span data-stu-id="90086-228">When working with blobs outside of HDInsight, most utilities do not recognize hello WASB format and instead expect a basic path format, such as `example/jars/hadoop-mapreduce-examples.jar`.</span></span>
> 
> 

## <a name="access-blobs"></a><span data-ttu-id="90086-229">Dostęp do obiektów blob</span><span class="sxs-lookup"><span data-stu-id="90086-229">Access blobs</span></span> 


### <span data-ttu-id="90086-230"><a name="access-blobs-using-azure-powershell"></a> Korzystanie z programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="90086-230"><a name="access-blobs-using-azure-powershell"></a> Use Azure PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="90086-231">Witaj polecenia w tej sekcji stanowią podstawowy przykład przy użyciu programu PowerShell tooaccess dane przechowywane w obiektach blob.</span><span class="sxs-lookup"><span data-stu-id="90086-231">hello commands in this section provide a basic example of using PowerShell tooaccess data stored in blobs.</span></span> <span data-ttu-id="90086-232">Na przykład obszerniejszy dostosowany do pracy z usługą HDInsight, zobacz hello [narzędzi HDInsight Tools](https://github.com/Blackmist/hdinsight-tools).</span><span class="sxs-lookup"><span data-stu-id="90086-232">For a more full-featured example that is customized for working with HDInsight, see hello [HDInsight Tools](https://github.com/Blackmist/hdinsight-tools).</span></span>
> 
> 

<span data-ttu-id="90086-233">Użyj następującego polecenia cmdlet związanych z obiektami blob hello toolist hello:</span><span class="sxs-lookup"><span data-stu-id="90086-233">Use hello following command toolist hello blob-related cmdlets:</span></span>

    Get-Command *blob*

![Lista poleceń cmdlet programu PowerShell związanych z obiektami blob.][img-hdi-powershell-blobcommands]

#### <a name="upload-files"></a><span data-ttu-id="90086-235">Przekazywanie plików</span><span class="sxs-lookup"><span data-stu-id="90086-235">Upload files</span></span>
<span data-ttu-id="90086-236">Zobacz [przekazywanie danych tooHDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="90086-236">See [Upload data tooHDInsight][hdinsight-upload-data].</span></span>

#### <a name="download-files"></a><span data-ttu-id="90086-237">Pobieranie plików</span><span class="sxs-lookup"><span data-stu-id="90086-237">Download files</span></span>
<span data-ttu-id="90086-238">Witaj poniższy skrypt pobiera bloku folderu bieżącego toohello obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="90086-238">hello following script downloads a block blob toohello current folder.</span></span> <span data-ttu-id="90086-239">Przed uruchamianie skryptu hello Zmień folder tooa katalogu hello, w którym masz uprawnienia do zapisu.</span><span class="sxs-lookup"><span data-stu-id="90086-239">Before running hello script, change hello directory tooa folder where you have write permissions.</span></span>

    $resourceGroupName = "<AzureResourceGroupName>"
    $storageAccountName = "<AzureStorageAccountName>"   # hello storage account used for hello default file system specified at creation.
    $containerName = "<BlobStorageContainerName>"  # hello default file system container has hello same name as hello cluster.
    $blob = "example/data/sample.log" # hello name of hello blob toobe downloaded.

    # Use Add-AzureAccount if you haven't connected tooyour Azure subscription
    Login-AzureRmAccount 
    Select-AzureRmSubscription -SubscriptionID "<Your Azure Subscription ID>"

    Write-Host "Create a context object ... " -ForegroundColor Green
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey  

    Write-Host "Download hello blob ..." -ForegroundColor Green
    Get-AzureStorageBlobContent -Container $ContainerName -Blob $blob -Context $storageContext -Force

    Write-Host "List hello downloaded file ..." -ForegroundColor Green
    cat "./$blob"

<span data-ttu-id="90086-240">Jeśli nazwa grupy zasobów hello i nazwa klastra hello, można użyć hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="90086-240">Providing hello resource group name and hello cluster name, you can use hello following code:</span></span>

    $resourceGroupName = "<AzureResourceGroupName>"
    $clusterName = "<HDInsightClusterName>"
    $blob = "example/data/sample.log" # hello name of hello blob toobe downloaded.

    $cluster = Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName
    $defaultStorageAccount = $cluster.DefaultStorageAccount -replace '.blob.core.windows.net'
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccount)[0].Value
    $defaultStorageContainer = $cluster.DefaultStorageContainer
    $storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccount -StorageAccountKey $defaultStorageAccountKey 

    Write-Host "Download hello blob ..." -ForegroundColor Green
    Get-AzureStorageBlobContent -Container $defaultStorageContainer -Blob $blob -Context $storageContext -Force


#### <a name="delete-files"></a><span data-ttu-id="90086-241">Usuwanie plików</span><span class="sxs-lookup"><span data-stu-id="90086-241">Delete files</span></span>
    Remove-AzureStorageBlob -Container $containerName -Context $storageContext -blob $blob

#### <a name="list-files"></a><span data-ttu-id="90086-242">Lista plików</span><span class="sxs-lookup"><span data-stu-id="90086-242">List files</span></span>
    Get-AzureStorageBlob -Container $containerName -Context $storageContext -prefix "example/data/"

#### <a name="run-hive-queries-using-an-undefined-storage-account"></a><span data-ttu-id="90086-243">Uruchamianie zapytań Hive przy użyciu niezdefiniowanego konta magazynu</span><span class="sxs-lookup"><span data-stu-id="90086-243">Run Hive queries using an undefined storage account</span></span>
<span data-ttu-id="90086-244">Ten przykład przedstawia, jak toolist folderu z konta magazynu, który nie jest zdefiniowany podczas hello procesu tworzenia.</span><span class="sxs-lookup"><span data-stu-id="90086-244">This example shows how toolist a folder from storage account that is not defined during hello creating process.</span></span>
<span data-ttu-id="90086-245">$clusterName = "<HDInsightClusterName>"</span><span class="sxs-lookup"><span data-stu-id="90086-245">$clusterName = "<HDInsightClusterName>"</span></span>

    $undefinedStorageAccount = "<UnboundedStorageAccountUnderTheSameSubscription>"
    $undefinedContainer = "<UnboundedBlobContainerAssociatedWithTheStorageAccount>"

    $undefinedStorageKey = Get-AzureStorageKey $undefinedStorageAccount | %{ $_.Primary }

    Use-AzureRmHDInsightCluster $clusterName

    $defines = @{}
    $defines.Add("fs.azure.account.key.$undefinedStorageAccount.blob.core.windows.net", $undefinedStorageKey)

    Invoke-AzureRmHDInsightHiveJob -Defines $defines -Query "dfs -ls wasb://$undefinedContainer@$undefinedStorageAccount.blob.core.windows.net/;"

### <a name="use-azure-cli"></a><span data-ttu-id="90086-246">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="90086-246">Use Azure CLI</span></span>
<span data-ttu-id="90086-247">Użyj powitania po toolist hello związanych z obiektami blob poleceń:</span><span class="sxs-lookup"><span data-stu-id="90086-247">Use hello following command toolist hello blob-related commands:</span></span>

    azure storage blob

<span data-ttu-id="90086-248">**Przykład użycia interfejsu wiersza polecenia Azure tooupload pliku**</span><span class="sxs-lookup"><span data-stu-id="90086-248">**Example of using Azure CLI tooupload a file**</span></span>

    azure storage blob upload <sourcefilename> <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

<span data-ttu-id="90086-249">**Przykład użycia interfejsu wiersza polecenia Azure toodownload pliku**</span><span class="sxs-lookup"><span data-stu-id="90086-249">**Example of using Azure CLI toodownload a file**</span></span>

    azure storage blob download <containername> <blobname> <destinationfilename> --account-name <storageaccountname> --account-key <storageaccountkey>

<span data-ttu-id="90086-250">**Przykład użycia interfejsu wiersza polecenia Azure toodelete pliku**</span><span class="sxs-lookup"><span data-stu-id="90086-250">**Example of using Azure CLI toodelete a file**</span></span>

    azure storage blob delete <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

<span data-ttu-id="90086-251">**Przykład użycia interfejsu wiersza polecenia Azure toolist plików**</span><span class="sxs-lookup"><span data-stu-id="90086-251">**Example of using Azure CLI toolist files**</span></span>

    azure storage blob list <containername> <blobname|prefix> --account-name <storageaccountname> --account-key <storageaccountkey>

## <a name="use-additional-storage-accounts"></a><span data-ttu-id="90086-252">Używanie dodatkowych kont magazynu</span><span class="sxs-lookup"><span data-stu-id="90086-252">Use additional storage accounts</span></span>

<span data-ttu-id="90086-253">Podczas tworzenia klastra usługi HDInsight, możesz określić hello konto Azure Storage, które chcesz tooassociate z nim.</span><span class="sxs-lookup"><span data-stu-id="90086-253">While creating an HDInsight cluster, you specify hello Azure Storage account you want tooassociate with it.</span></span> <span data-ttu-id="90086-254">Ponadto toothis konta magazynu, można dodać dodatkowe konta magazynu z hello sam subskrypcji platformy Azure lub różnych subskrypcji Azure, podczas procesu tworzenia hello lub po utworzeniu klastra.</span><span class="sxs-lookup"><span data-stu-id="90086-254">In addition toothis storage account, you can add additional storage accounts from hello same Azure subscription or different Azure subscriptions during hello creation process or after a cluster has been created.</span></span> <span data-ttu-id="90086-255">Aby uzyskać instrukcje dotyczące dodawania kolejnych kont magazynu, zobacz [Tworzenie klastrów usługi HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="90086-255">For instructions about adding additional storage accounts, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

> [!WARNING]
> <span data-ttu-id="90086-256">Przy użyciu konta, dodatkowe miejsce do magazynowania w innej lokalizacji niż hello klastra usługi HDInsight nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="90086-256">Using an additional storage account in a different location than hello HDInsight cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="90086-257">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="90086-257">Next steps</span></span>
<span data-ttu-id="90086-258">W tym artykule należy przedstawiono sposób toouse zgodnego systemem plików HDFS magazynu platformy Azure z usługą HDInsight.</span><span class="sxs-lookup"><span data-stu-id="90086-258">In this article, you learned how toouse HDFS-compatible Azure storage with HDInsight.</span></span> <span data-ttu-id="90086-259">Dzięki temu można toobuild skalowalnych, długoterminowych, archiwizacji rozwiązań do pozyskiwania danych i użyj HDInsight toounlock hello informacji wewnątrz hello przechowywane strukturalnych i danych bez struktury.</span><span class="sxs-lookup"><span data-stu-id="90086-259">This allows you toobuild scalable, long-term, archiving data acquisition solutions and use HDInsight toounlock hello information inside hello stored structured and unstructured data.</span></span>

<span data-ttu-id="90086-260">Aby uzyskać więcej informacji, zobacz:</span><span class="sxs-lookup"><span data-stu-id="90086-260">For more information, see:</span></span>

* <span data-ttu-id="90086-261">[Wprowadzenie do usługi Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="90086-261">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* [<span data-ttu-id="90086-262">Wprowadzenie do usługi Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="90086-262">Get started with Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-get-started-portal.md)
* <span data-ttu-id="90086-263">[Przekazywanie danych tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="90086-263">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="90086-264">[Korzystanie z programu Hive z usługą HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="90086-264">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="90086-265">[Korzystanie z języka Pig z usługą HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="90086-265">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="90086-266">[Korzystanie z usługą HDInsight toodata dostępu toorestrict sygnatury dostępu współdzielonego magazynu Azure][hdinsight-use-sas]</span><span class="sxs-lookup"><span data-stu-id="90086-266">[Use Azure Storage Shared Access Signatures toorestrict access toodata with HDInsight][hdinsight-use-sas]</span></span>

[hdinsight-use-sas]: hdinsight-storage-sharedaccesssignature-permissions.md
[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-creation]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md

[blob-storage-restAPI]: http://msdn.microsoft.com/library/windowsazure/dd135733.aspx
[azure-storage-create]:../storage/common/storage-create-storage-account.md

[img-hdi-powershell-blobcommands]: ./media/hdinsight-hadoop-use-blob-storage/HDI.PowerShell.BlobCommands.png
[img-hdi-quick-create]: ./media/hdinsight-hadoop-use-blob-storage/HDI.QuickCreateCluster.png
[img-hdi-custom-create-storage-account]: ./media/hdinsight-hadoop-use-blob-storage/HDI.CustomCreateStorageAccount.png  
