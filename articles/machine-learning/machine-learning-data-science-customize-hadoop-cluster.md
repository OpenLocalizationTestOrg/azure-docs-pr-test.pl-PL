---
title: aaaCustomize Hadoop clusters dla hello proces nauki danych Team | Dokumentacja firmy Microsoft
description: "Udostępniona w niestandardowych usługi Azure HDInsight Hadoop klastrów popularnych modułów środowiska Python."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 0c115dca-2565-4e7a-9536-6002af5c786a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: e192542dd39f71bccbb5163382b4050d0f12ad95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="customize-azure-hdinsight-hadoop-clusters-for-hello-team-data-science-process"></a><span data-ttu-id="b187b-103">Dostosowywanie klastrów usługi Azure HDInsight Hadoop dla hello proces nauki danych Team</span><span class="sxs-lookup"><span data-stu-id="b187b-103">Customize Azure HDInsight Hadoop clusters for hello Team Data Science Process</span></span>
<span data-ttu-id="b187b-104">W tym artykule opisano sposób toocustomize HDInsight Hadoop cluster instalując Anaconda 64-bitowych (Python 2.7) na każdym węźle po zainicjowaniu obsługi klastra hello jako usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b187b-104">This article describes how toocustomize an HDInsight Hadoop cluster by installing 64-bit Anaconda (Python 2.7) on each node when hello cluster is provisioned as an HDInsight service.</span></span> <span data-ttu-id="b187b-105">Pokazuje też, jak tooaccess hello headnode toosubmit zadania niestandardowe toohello klastra.</span><span class="sxs-lookup"><span data-stu-id="b187b-105">It also shows how tooaccess hello headnode toosubmit custom jobs toohello cluster.</span></span> <span data-ttu-id="b187b-106">Takie dostosowanie sprawia, że wielu popularnych modułów środowiska Python, które są objęte Anaconda, łatwo dostępne dla użytkowników funkcji zdefiniowanej (UDF), które są zaprojektowane tooprocess rekordów gałęzi w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="b187b-106">This customization makes many popular Python modules, that are included in Anaconda, conveniently available for use in user defined functions (UDFs) that are designed tooprocess Hive records in hello cluster.</span></span> <span data-ttu-id="b187b-107">Aby uzyskać instrukcje dotyczące procedur hello używaną w tym scenariuszu, zobacz [jak zapytań programu Hive toosubmit](machine-learning-data-science-move-hive-tables.md#submit).</span><span class="sxs-lookup"><span data-stu-id="b187b-107">For instructions on hello procedures used in this scenario, see [How toosubmit Hive queries](machine-learning-data-science-move-hive-tables.md#submit).</span></span>

<span data-ttu-id="b187b-108">Witaj menu następujących łączy tootopics, które opisują sposób tooset się hello różnych środowiskach nauki danych przez hello [zespołu danych nauki procesu (TDSP)](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b187b-108">hello following menu links tootopics that describe how tooset up hello various data science environments used by hello [Team Data Science Process (TDSP)](data-science-process-overview.md).</span></span>

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

## <span data-ttu-id="b187b-109"><a name="customize"></a>Dostosowywanie klastra usługi Hadoop w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="b187b-109"><a name="customize"></a>Customize Azure HDInsight Hadoop Cluster</span></span>
<span data-ttu-id="b187b-110">Uruchom toocreate dostosowane klastra usługi HDInsight Hadoop, logując się za[**klasycznego portalu Azure**](https://manage.windowsazure.com/), kliknij przycisk **nowy** w lewo hello dolnego rogu, a następnie wybierz usługi danych -> HDINSIGHT -> **Utwórz niestandardowy** toobring się hello **szczegółów klastra** okna.</span><span class="sxs-lookup"><span data-stu-id="b187b-110">toocreate a customized HDInsight Hadoop cluster, start by logging on too[**Azure classic portal**](https://manage.windowsazure.com/), click **New** at hello left bottom corner, and then select DATA SERVICES -> HDINSIGHT -> **CUSTOM CREATE** toobring up hello **Cluster Details** window.</span></span> 

![Tworzenie obszaru roboczego](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

<span data-ttu-id="b187b-112">Wprowadź nazwę hello hello toobe klastra utworzone na stronie konfiguracji 1, a następnie zaakceptuj wartości domyślne dla hello innych pól.</span><span class="sxs-lookup"><span data-stu-id="b187b-112">Input hello name of hello cluster toobe created on configuration page 1, and accept default values for hello other fields.</span></span> <span data-ttu-id="b187b-113">Kliknij przycisk hello Strzałka toogo toohello następnej konfiguracji strony.</span><span class="sxs-lookup"><span data-stu-id="b187b-113">Click hello arrow toogo toohello next configuration page.</span></span> 

![Tworzenie obszaru roboczego](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

<span data-ttu-id="b187b-115">Na stronie konfiguracji 2, wprowadź numer hello **węzły danych**, wybierz pozycję hello **REGION/WIRTUALNEJ sieci**i wybierz rozmiary hello hello **HEAD, węzła** i hello **Węzeł danych**.</span><span class="sxs-lookup"><span data-stu-id="b187b-115">On configuration page 2, input hello number of **DATA NODES**, select hello **REGION/VIRTUAL NETWORK**, and select hello sizes of hello **HEAD NODE** and hello **DATA NODE**.</span></span> <span data-ttu-id="b187b-116">Kliknij przycisk hello Strzałka toogo toohello następnej konfiguracji strony.</span><span class="sxs-lookup"><span data-stu-id="b187b-116">Click hello arrow toogo toohello next configuration page.</span></span>

> [!NOTE]
> <span data-ttu-id="b187b-117">Witaj **REGION/WIRTUALNEJ sieci** ma toobe hello sam jako region hello hello konta magazynu, które będzie używane dla klastra usługi HDInsight Hadoop hello toobe.</span><span class="sxs-lookup"><span data-stu-id="b187b-117">hello **REGION/VIRTUAL NETWORK** has toobe hello same as hello region of hello storage account that is going toobe used for hello HDInsight Hadoop cluster.</span></span> <span data-ttu-id="b187b-118">W przeciwnym razie w czwartej stronie konfiguracji hello hello konta magazynu nie będą wyświetlane na liście rozwijanej hello **nazwa konta**.</span><span class="sxs-lookup"><span data-stu-id="b187b-118">Otherwise, in hello fourth configuration page, hello storage account will not appear on hello dropdown list of **ACCOUNT NAME**.</span></span>
> 
> 

![Tworzenie obszaru roboczego](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img3.png)

<span data-ttu-id="b187b-120">Na stronie konfiguracji 3 Podaj nazwę użytkownika i hasło dla hello klastra usługi HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="b187b-120">On configuration page 3, provide a user name and password for hello HDInsight Hadoop cluster.</span></span> <span data-ttu-id="b187b-121">**Nie** wybierz hello *hello Enter potrzeby magazynu metadanych Hive/Oozie*.</span><span class="sxs-lookup"><span data-stu-id="b187b-121">**Do not** select hello *Enter hello Hive/Oozie Metastore*.</span></span> <span data-ttu-id="b187b-122">Następnie kliknij przycisk hello Strzałka toogo toohello następnej konfiguracji strony.</span><span class="sxs-lookup"><span data-stu-id="b187b-122">Then, click hello arrow toogo toohello next configuration page.</span></span> 

![Tworzenie obszaru roboczego](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img4.png)

<span data-ttu-id="b187b-124">Na stronie konfiguracji 4 należy określić nazwę konta magazynu hello, kontener domyślny hello hello klastra usługi HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="b187b-124">On configuration page 4, specify hello storage account name, hello default container of hello HDInsight Hadoop cluster.</span></span> <span data-ttu-id="b187b-125">W przypadku wybrania *Utwórz domyślny kontener* w hello **domyślny KONTENER** listy rozwijanej, kontener z hello takie same nazwy jako hello klastra zostaną utworzone.</span><span class="sxs-lookup"><span data-stu-id="b187b-125">If you select *Create default container* in hello **DEFAULT CONTAINER** dropdown list, a container with hello same name as hello cluster will be created.</span></span> <span data-ttu-id="b187b-126">Kliknij przycisk hello Strzałka toogo toohello ostatniej strony konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="b187b-126">Click hello arrow toogo toohello last configuration page.</span></span>

![Tworzenie obszaru roboczego](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img5.png)

<span data-ttu-id="b187b-128">Na powitania końcowego **akcji skryptu** strony konfiguracji, kliknij przycisk **dodać akcję skryptu** przycisk i wypełnienie pól tekstowych hello hello następujące wartości.</span><span class="sxs-lookup"><span data-stu-id="b187b-128">On hello final **Script Actions** configuration page, click **add script action** button, and fill hello text fields with hello following values.</span></span>

* <span data-ttu-id="b187b-129">**Nazwa** -dowolnego ciągu jako nazwy hello tej akcji skryptu</span><span class="sxs-lookup"><span data-stu-id="b187b-129">**NAME** - any string as hello name of this script action</span></span>
* <span data-ttu-id="b187b-130">**Typ węzła** — wybierz tę opcję **wszystkie węzły**</span><span class="sxs-lookup"><span data-stu-id="b187b-130">**NODE TYPE** - select **All nodes**</span></span>
* <span data-ttu-id="b187b-131">**Identyfikator URI skryptu** - *http://getgoing.blob.core.windows.net/publicscripts/Azure_HDI_Setup_Windows.ps1*</span><span class="sxs-lookup"><span data-stu-id="b187b-131">**SCRIPT URI** - *http://getgoing.blob.core.windows.net/publicscripts/Azure_HDI_Setup_Windows.ps1*</span></span> 
  * <span data-ttu-id="b187b-132">*publicscripts* jest publicznego kontenera na koncie magazynu hello</span><span class="sxs-lookup"><span data-stu-id="b187b-132">*publicscripts* is a public container in hello storage account</span></span> 
  * <span data-ttu-id="b187b-133">*getgoing* używamy pracy tooshare PowerShell skryptu pliki toofacilitate użytkowników na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="b187b-133">*getgoing* we use tooshare PowerShell script files toofacilitate users' work in Azure</span></span>
* <span data-ttu-id="b187b-134">**Parametry** -(puste)</span><span class="sxs-lookup"><span data-stu-id="b187b-134">**PARAMETERS** - (leave blank)</span></span>

<span data-ttu-id="b187b-135">Na koniec kliknij hello znacznik wyboru toostart hello tworzenia klastra usługi HDInsight Hadoop hello dostosowane.</span><span class="sxs-lookup"><span data-stu-id="b187b-135">Finally, click hello check mark toostart hello creation of hello customized HDInsight Hadoop cluster.</span></span> 

![Tworzenie obszaru roboczego](./media/machine-learning-data-science-customize-hadoop-cluster/script-actions.png)

## <span data-ttu-id="b187b-137"><a name="headnode"></a>Witaj dostępu Head węzeł z klastra usługi Hadoop</span><span class="sxs-lookup"><span data-stu-id="b187b-137"><a name="headnode"></a> Access hello Head Node of Hadoop Cluster</span></span>
<span data-ttu-id="b187b-138">Należy włączyć dostępu zdalnego klastra usługi Hadoop toohello na platformie Azure, aby hello węzła głównego klastra usługi Hadoop hello są dostępne za pośrednictwem protokołu RDP.</span><span class="sxs-lookup"><span data-stu-id="b187b-138">You must enable remote access toohello Hadoop cluster in Azure before you can access hello head node of hello Hadoop cluster through RDP.</span></span> 

1. <span data-ttu-id="b187b-139">Zaloguj się za toohello [ **klasycznego portalu Azure**](https://manage.windowsazure.com/), wybierz pozycję **HDInsight** powitania po lewej stronie, wybierz klaster Hadoop z listy hello klastrów, kliknij przycisk hello  **Konfiguracja** , a następnie kliknij pozycję hello **Włącz zdalne** ikona u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="b187b-139">Log in toohello [**Azure classic portal**](https://manage.windowsazure.com/), select **HDInsight** on hello left, select your Hadoop cluster from hello list of clusters, click hello **CONFIGURATION** tab, and then click hello **ENABLE REMOTE** icon at hello bottom of hello page.</span></span>
   
    ![Tworzenie obszaru roboczego](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-1.png)
2. <span data-ttu-id="b187b-141">W hello **Konfigurowanie pulpitu zdalnego** okna, wprowadź hello nazwy użytkownika i HASŁA pola i wybierz datę wygaśnięcia hello dostępu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="b187b-141">In hello **Configure Remote Desktop** window, enter hello USER NAME and PASSWORD fields, and select hello expiration date for remote access.</span></span> <span data-ttu-id="b187b-142">Następnie kliknij przycisk hello znacznik wyboru tooenable hello dostępu zdalnego toohello węzła głównego klastra usługi Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="b187b-142">Then click hello check mark tooenable hello remote access toohello head node of hello Hadoop cluster.</span></span>
   
    ![Tworzenie obszaru roboczego](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-2.png)

> [!NOTE]
> <span data-ttu-id="b187b-144">Hello nazwę użytkownika i hasło dla dostępu zdalnego hello nie są hello nazwy użytkownika i hasła, który jest używany podczas tworzenia klastra usługi Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="b187b-144">hello user name and password for hello remote access are not hello user name and password that you use when you created hello Hadoop cluster.</span></span> <span data-ttu-id="b187b-145">Jest to osobny zestaw poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="b187b-145">This is a separate set of credentials.</span></span> <span data-ttu-id="b187b-146">Ponadto Data wygaśnięcia hello hello dostępu zdalnego ma toobe w ciągu 7 dni od hello bieżącą datę.</span><span class="sxs-lookup"><span data-stu-id="b187b-146">Also, hello expiration date of hello remote access has toobe within 7 days from hello current date.</span></span>
> 
> 

<span data-ttu-id="b187b-147">Po włączeniu dostępu zdalnego, kliknij przycisk **CONNECT** u dołu hello hello tooremote strony do hello węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="b187b-147">After remote access is enabled, click **CONNECT** at hello bottom of hello page tooremote into hello head node.</span></span> <span data-ttu-id="b187b-148">Logowania toohello węzła głównego klastra usługi Hadoop hello wprowadzając hello poświadczeń dla użytkownika dostępu zdalnego hello, określony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="b187b-148">You log on toohello head node of hello Hadoop cluster by entering hello credentials for hello remote access user that you specified earlier.</span></span>

![Tworzenie obszaru roboczego](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-3.png)

<span data-ttu-id="b187b-150">Witaj kolejne kroki w hello zaawansowane analizy procesu są mapowane w hello [zespołu danych nauki procesu (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) i mogą obejmować następujące kroki, które przenoszenie danych do usługi HDInsight, a następnie przetworzyć i przykładowe go w ramach przygotowania do uczenia z danych hello przy użyciu usługi Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="b187b-150">hello next steps in hello advanced analytics process are mapped in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) and may include steps that move data into HDInsight, then process and sample it there in preparation for learning from hello data with Azure Machine Learning.</span></span>

<span data-ttu-id="b187b-151">Zobacz [jak zapytań programu Hive toosubmit](machine-learning-data-science-move-hive-tables.md#submit) instrukcje dotyczące sposobu tooaccess hello modułów środowiska Python, które są objęte Anaconda z hello węzła głównego klastra hello w funkcji zdefiniowanej przez użytkownika (UDF), które są używane tooprocess Hive rekordów w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="b187b-151">See [How toosubmit Hive queries](machine-learning-data-science-move-hive-tables.md#submit) for instructions on how tooaccess hello Python modules that are included in Anaconda from hello head node of hello cluster in user-defined functions (UDFs) that are used tooprocess Hive records stored in hello cluster.</span></span>

