---
title: "aaaUse niestandardowych działań w potoku fabryki danych Azure"
description: "Dowiedz się, jak toocreate niestandardowych działań i używać ich w potoku fabryki danych Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 8dd7ba14-15d2-4fd9-9ada-0b2c684327e9
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: 23e33727b2160541ab40938ffd911fdd484b3daa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-custom-activities-in-an-azure-data-factory-pipeline"></a><span data-ttu-id="d443f-103">Korzystanie z działań niestandardowych w potoku usługi Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d443f-103">Use custom activities in an Azure Data Factory pipeline</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="d443f-104">Działanie gałęzi</span><span class="sxs-lookup"><span data-stu-id="d443f-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="d443f-105">Działanie pig</span><span class="sxs-lookup"><span data-stu-id="d443f-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="d443f-106">Działania MapReduce</span><span class="sxs-lookup"><span data-stu-id="d443f-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="d443f-107">Działaniu przesyłania strumieniowego usługi Hadoop</span><span class="sxs-lookup"><span data-stu-id="d443f-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="d443f-108">Działanie Spark</span><span class="sxs-lookup"><span data-stu-id="d443f-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="d443f-109">Działanie wykonywania wsadowego w usłudze Machine Learning</span><span class="sxs-lookup"><span data-stu-id="d443f-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="d443f-110">Działania aktualizowania zasobów w usłudze Machine Learning</span><span class="sxs-lookup"><span data-stu-id="d443f-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="d443f-111">Działania procedur składowanych</span><span class="sxs-lookup"><span data-stu-id="d443f-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="d443f-112">Działania języka U-SQL usługi Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="d443f-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="d443f-113">Działania niestandardowe .NET</span><span class="sxs-lookup"><span data-stu-id="d443f-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="d443f-114">Istnieją dwa typy działań, które można używać w potoku fabryki danych Azure.</span><span class="sxs-lookup"><span data-stu-id="d443f-114">There are two types of activities that you can use in an Azure Data Factory pipeline.</span></span>

- <span data-ttu-id="d443f-115">[Działania przepływu danych](data-factory-data-movement-activities.md) toomove danych między [obsługiwane magazyny danych źródłowy i odbiorczy](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="d443f-115">[Data Movement Activities](data-factory-data-movement-activities.md) toomove data between [supported source and sink data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span>
- <span data-ttu-id="d443f-116">[Działania przekształcania danych](data-factory-data-transformation-activities.md) tootransform danych przy użyciu obliczeniowe usług, takich jak Azure HDInsight, partii zadań Azure i usługi Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="d443f-116">[Data Transformation Activities](data-factory-data-transformation-activities.md) tootransform data using compute services such as Azure HDInsight, Azure Batch, and Azure Machine Learning.</span></span> 

<span data-ttu-id="d443f-117">Utwórz toomove danych do/z magazynem danych, który fabryki danych nie obsługuje, **działania niestandardowego** z własnych danych przepływu logiki i użyj hello działania w potoku.</span><span class="sxs-lookup"><span data-stu-id="d443f-117">toomove data to/from a data store that Data Factory does not support, create a **custom activity** with your own data movement logic and use hello activity in a pipeline.</span></span> <span data-ttu-id="d443f-118">Podobnie tootransform/przetwarzania danych w taki sposób, który nie jest obsługiwany przez fabrykę danych tworzenia działań niestandardowych z własną logikę przekształcania danych i użyj hello działania w potoku.</span><span class="sxs-lookup"><span data-stu-id="d443f-118">Similarly, tootransform/process data in a way that isn't supported by Data Factory, create a custom activity with your own data transformation logic and use hello activity in a pipeline.</span></span> 

<span data-ttu-id="d443f-119">Toorun działania niestandardowego można skonfigurować na **partii zadań Azure** puli maszyn wirtualnych lub z systemem Windows **Azure HDInsight** klastra.</span><span class="sxs-lookup"><span data-stu-id="d443f-119">You can configure a custom activity toorun on an **Azure Batch** pool of virtual machines or a Windows-based **Azure HDInsight** cluster.</span></span> <span data-ttu-id="d443f-120">Korzystając z partii zadań Azure, można użyć tylko istniejącej puli partii zadań Azure.</span><span class="sxs-lookup"><span data-stu-id="d443f-120">When using Azure Batch, you can use only an existing Azure Batch pool.</span></span> <span data-ttu-id="d443f-121">Natomiast podczas korzystania z usługi HDInsight, można użyć istniejącego klastra usługi HDInsight lub w klastrze, który jest automatycznie tworzony należy na żądanie w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="d443f-121">Whereas, when using HDInsight, you can use an existing HDInsight cluster or a cluster that is automatically created for you on-demand at runtime.</span></span>  

<span data-ttu-id="d443f-122">Witaj następujący przewodnik zawiera instrukcje krok po kroku dotyczące tworzenia działań niestandardowych .NET i używania hello niestandardowego działania w potoku.</span><span class="sxs-lookup"><span data-stu-id="d443f-122">hello following walkthrough provides step-by-step instructions for creating a custom .NET activity and using hello custom activity in a pipeline.</span></span> <span data-ttu-id="d443f-123">wskazówki Hello używa **partii zadań Azure** połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="d443f-123">hello walkthrough uses an **Azure Batch** linked service.</span></span> <span data-ttu-id="d443f-124">połączona usługa Azure HDInsight toouse zamiast tego, tworzenie połączonej usługi typu **HDInsight** (własnego klastra usługi HDInsight) lub **HDInsightOnDemand** (fabryka danych powoduje utworzenie klastra usługi HDInsight na żądanie).</span><span class="sxs-lookup"><span data-stu-id="d443f-124">toouse an Azure HDInsight linked service instead, you create a linked service of type **HDInsight** (your own HDInsight cluster) or **HDInsightOnDemand** (Data Factory creates an HDInsight cluster on-demand).</span></span> <span data-ttu-id="d443f-125">Następnie należy skonfigurować hello toouse niestandardowe działanie usługi HDInsight połączone.</span><span class="sxs-lookup"><span data-stu-id="d443f-125">Then, configure custom activity toouse hello HDInsight linked service.</span></span> <span data-ttu-id="d443f-126">Zobacz [użycia usługi Azure HDInsight połączone usługi](#use-hdinsight-compute-service) sekcji, aby uzyskać więcej informacji na temat używania usługi Azure HDInsight toorun hello niestandardowego działania.</span><span class="sxs-lookup"><span data-stu-id="d443f-126">See [Use Azure HDInsight linked services](#use-hdinsight-compute-service) section for details on using Azure HDInsight toorun hello custom activity.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="d443f-127">Niestandardowe działania .NET Hello uruchomić tylko w klastrach HDInsight opartych na systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="d443f-127">hello custom .NET activities run only on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="d443f-128">Obejście tego ograniczenia jest toouse hello działania zmniejszyć mapy toorun Java kodu niestandardowego w klastrze usługi HDInsight opartej na systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="d443f-128">A workaround for this limitation is toouse hello Map Reduce Activity toorun custom Java code on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="d443f-129">Innym rozwiązaniem jest toouse puli partii zadań Azure VMs toorun niestandardowych działań zamiast klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d443f-129">Another option is toouse an Azure Batch pool of VMs toorun custom activities instead of using a HDInsight cluster.</span></span>
> - <span data-ttu-id="d443f-130">Nie jest możliwe toouse bramę zarządzania danymi z działań niestandardowych tooaccess lokalnych źródeł danych.</span><span class="sxs-lookup"><span data-stu-id="d443f-130">It is not possible toouse a Data Management Gateway from a custom activity tooaccess on-premises data sources.</span></span> <span data-ttu-id="d443f-131">Obecnie [brama zarządzania danymi](data-factory-data-management-gateway.md) obsługuje tylko działania kopiowania hello i działania procedury składowanej w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="d443f-131">Currently, [Data Management Gateway](data-factory-data-management-gateway.md) supports only hello copy activity and stored procedure activity in Data Factory.</span></span>   

## <a name="walkthrough-create-a-custom-activity"></a><span data-ttu-id="d443f-132">Wskazówki: Tworzenie niestandardowego działania</span><span class="sxs-lookup"><span data-stu-id="d443f-132">Walkthrough: create a custom activity</span></span>
### <a name="prerequisites"></a><span data-ttu-id="d443f-133">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d443f-133">Prerequisites</span></span>
* <span data-ttu-id="d443f-134">Visual Studio 2012/2013/2015</span><span class="sxs-lookup"><span data-stu-id="d443f-134">Visual Studio 2012/2013/2015</span></span>
* <span data-ttu-id="d443f-135">Pobierz i zainstaluj zestaw [SDK .NET Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="d443f-135">Download and install [Azure .NET SDK](https://azure.microsoft.com/downloads/)</span></span>

### <a name="azure-batch-prerequisites"></a><span data-ttu-id="d443f-136">Wymagania wstępne partii platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d443f-136">Azure Batch prerequisites</span></span>
<span data-ttu-id="d443f-137">W przewodniku hello możesz uruchomić własnych działań platformy .NET przy użyciu partii zadań Azure jako zasoby obliczeniowe.</span><span class="sxs-lookup"><span data-stu-id="d443f-137">In hello walkthrough, you run your custom .NET activities using Azure Batch as a compute resource.</span></span> <span data-ttu-id="d443f-138">**Partia zadań Azure** to platforma usług do uruchomienia równoległego na dużą skalę i wysokiej wydajności aplikacji (HPC) wydajnie w chmurze hello obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="d443f-138">**Azure Batch** is a platform service for running large-scale parallel and high-performance computing (HPC) applications efficiently in hello cloud.</span></span> <span data-ttu-id="d443f-139">Partia zadań Azure planuje toorun pracy obliczeniowych na zarządzanego **kolekcji maszyn wirtualnych**, i może automatycznie skalowania zasobów obliczeniowych zasobów toomeet hello potrzeb zadań.</span><span class="sxs-lookup"><span data-stu-id="d443f-139">Azure Batch schedules compute-intensive work toorun on a managed **collection of virtual machines**, and can automatically scale compute resources toomeet hello needs of your jobs.</span></span> <span data-ttu-id="d443f-140">Zobacz [podstawowe informacje o partii zadań Azure] [ batch-technical-overview] artykułu szczegółowe omówienie hello usługi partia zadań Azure.</span><span class="sxs-lookup"><span data-stu-id="d443f-140">See [Azure Batch basics][batch-technical-overview] article for a detailed overview of hello Azure Batch service.</span></span>

<span data-ttu-id="d443f-141">Samouczek hello należy utworzyć konto partii zadań Azure przy użyciu puli maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="d443f-141">For hello tutorial, create an Azure Batch account with a pool of VMs.</span></span> <span data-ttu-id="d443f-142">Poniżej przedstawiono kroki hello:</span><span class="sxs-lookup"><span data-stu-id="d443f-142">Here are hello steps:</span></span>

1. <span data-ttu-id="d443f-143">Utwórz **konto partii zadań Azure** przy użyciu hello [portalu Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d443f-143">Create an **Azure Batch account** using hello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="d443f-144">Zobacz [tworzenie i zarządzanie nimi konto partii zadań Azure] [ batch-create-account] artykułu, aby uzyskać instrukcje.</span><span class="sxs-lookup"><span data-stu-id="d443f-144">See [Create and manage an Azure Batch account][batch-create-account] article for instructions.</span></span>
2. <span data-ttu-id="d443f-145">Zanotuj nazwę konta partii zadań Azure hello, klucz konta identyfikatora URI i nazwa puli.</span><span class="sxs-lookup"><span data-stu-id="d443f-145">Note down hello Azure Batch account name, account key, URI, and pool name.</span></span> <span data-ttu-id="d443f-146">Należy je toocreate usługi partia zadań Azure połączone.</span><span class="sxs-lookup"><span data-stu-id="d443f-146">You need them toocreate an Azure Batch linked service.</span></span>
    1. <span data-ttu-id="d443f-147">Na stronie głównej hello konto partii zadań Azure, zobacz **adres URL** w hello następującego formatu: `https://myaccount.westus.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="d443f-147">On hello home page for Azure Batch account, you see a **URL** in hello following format: `https://myaccount.westus.batch.azure.com`.</span></span> <span data-ttu-id="d443f-148">W tym przykładzie **myaccount** jest nazwą hello hello konto partii zadań Azure.</span><span class="sxs-lookup"><span data-stu-id="d443f-148">In this example, **myaccount** is hello name of hello Azure Batch account.</span></span> <span data-ttu-id="d443f-149">Identyfikator URI używanych w definicji usługi hello połączony jest adresem URL hello bez nazwy hello hello konta.</span><span class="sxs-lookup"><span data-stu-id="d443f-149">URI you use in hello linked service definition is hello URL without hello name of hello account.</span></span> <span data-ttu-id="d443f-150">Na przykład: `https://<region>.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="d443f-150">For example: `https://<region>.batch.azure.com`.</span></span>
    2. <span data-ttu-id="d443f-151">Kliknij przycisk **klucze** w menu po lewej stronie powitania i kopiowania hello **podstawowy klucz dostępu**.</span><span class="sxs-lookup"><span data-stu-id="d443f-151">Click **Keys** on hello left menu, and copy hello **PRIMARY ACCESS KEY**.</span></span>
    3. <span data-ttu-id="d443f-152">toouse istniejącej puli, kliknij przycisk **pule** w hello menu i zanotuj hello **identyfikator** hello puli.</span><span class="sxs-lookup"><span data-stu-id="d443f-152">toouse an existing pool, click **Pools** on hello menu, and note down hello **ID** of hello pool.</span></span> <span data-ttu-id="d443f-153">Jeśli nie masz istniejącej puli, przenieść toohello następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="d443f-153">If you don't have an existing pool, move toohello next step.</span></span>     
2. <span data-ttu-id="d443f-154">Utwórz **puli partii zadań Azure**.</span><span class="sxs-lookup"><span data-stu-id="d443f-154">Create an **Azure Batch pool**.</span></span>

   1. <span data-ttu-id="d443f-155">W hello [portalu Azure](https://portal.azure.com), kliknij przycisk **Przeglądaj** w hello menu po lewej stronie i kliknij przycisk **konta usługi partia zadań**.</span><span class="sxs-lookup"><span data-stu-id="d443f-155">In hello [Azure portal](https://portal.azure.com), click **Browse** in hello left menu, and click **Batch Accounts**.</span></span>
   2. <span data-ttu-id="d443f-156">Wybierz użytkownika hello tooopen konto partii zadań Azure **konta usługi partia zadań** bloku.</span><span class="sxs-lookup"><span data-stu-id="d443f-156">Select your Azure Batch account tooopen hello **Batch Account** blade.</span></span>
   3. <span data-ttu-id="d443f-157">Kliknij przycisk **pule** kafelka.</span><span class="sxs-lookup"><span data-stu-id="d443f-157">Click **Pools** tile.</span></span>
   4. <span data-ttu-id="d443f-158">W hello **pule** bloku, kliknij przycisk Dodaj na powitania narzędzi tooadd puli.</span><span class="sxs-lookup"><span data-stu-id="d443f-158">In hello **Pools** blade, click Add button on hello toolbar tooadd a pool.</span></span>
      1. <span data-ttu-id="d443f-159">Wpisz identyfikator puli hello (identyfikator puli).</span><span class="sxs-lookup"><span data-stu-id="d443f-159">Enter an ID for hello pool (Pool ID).</span></span> <span data-ttu-id="d443f-160">Uwaga hello **identyfikator puli hello**; potrzebne podczas tworzenia hello rozwiązania fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="d443f-160">Note hello **ID of hello pool**; you need it when creating hello Data Factory solution.</span></span>
      2. <span data-ttu-id="d443f-161">Określ **systemu Windows Server 2012 R2** hello ustawienia rodziny systemów operacyjnych.</span><span class="sxs-lookup"><span data-stu-id="d443f-161">Specify **Windows Server 2012 R2** for hello Operating System Family setting.</span></span>
      3. <span data-ttu-id="d443f-162">Wybierz **warstwę cenową węzła**.</span><span class="sxs-lookup"><span data-stu-id="d443f-162">Select a **node pricing tier**.</span></span>
      4. <span data-ttu-id="d443f-163">Wprowadź **2** jako wartość hello **docelowego w wersji dedykowanej** ustawienie.</span><span class="sxs-lookup"><span data-stu-id="d443f-163">Enter **2** as value for hello **Target Dedicated** setting.</span></span>
      5. <span data-ttu-id="d443f-164">Wprowadź **2** jako wartość hello **maksymalna liczba zadań na węzeł** ustawienie.</span><span class="sxs-lookup"><span data-stu-id="d443f-164">Enter **2** as value for hello **Max tasks per node** setting.</span></span>
   5. <span data-ttu-id="d443f-165">Kliknij przycisk **OK** toocreate hello puli.</span><span class="sxs-lookup"><span data-stu-id="d443f-165">Click **OK** toocreate hello pool.</span></span>
   6. <span data-ttu-id="d443f-166">Zanotuj hello **identyfikator** hello puli.</span><span class="sxs-lookup"><span data-stu-id="d443f-166">Note down hello **ID** of hello pool.</span></span> 



### <a name="high-level-steps"></a><span data-ttu-id="d443f-167">Ogólne kroki</span><span class="sxs-lookup"><span data-stu-id="d443f-167">High-level steps</span></span>
<span data-ttu-id="d443f-168">Poniżej przedstawiono hello dwa ogólne kroki, wykonywanych w ramach tego przewodnika:</span><span class="sxs-lookup"><span data-stu-id="d443f-168">Here are hello two high-level steps you perform as part of this walkthrough:</span></span> 

1. <span data-ttu-id="d443f-169">Tworzenie niestandardowego działania, który zawiera proste danych przekształcania/przetwarzania logiki.</span><span class="sxs-lookup"><span data-stu-id="d443f-169">Create a custom activity that contains simple data transformation/processing logic.</span></span>
2. <span data-ttu-id="d443f-170">Tworzenie fabryki danych Azure z potok, który używa hello działania niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="d443f-170">Create an Azure data factory with a pipeline that uses hello custom activity.</span></span>

### <a name="create-a-custom-activity"></a><span data-ttu-id="d443f-171">Tworzenie niestandardowego działania</span><span class="sxs-lookup"><span data-stu-id="d443f-171">Create a custom activity</span></span>
<span data-ttu-id="d443f-172">Utwórz toocreate .NET działań niestandardowych **Biblioteka klas programu .NET** projektu z klasy, która implementuje, który **IDotNetActivity** interfejsu.</span><span class="sxs-lookup"><span data-stu-id="d443f-172">toocreate a .NET custom activity, create a **.NET Class Library** project with a class that implements that **IDotNetActivity** interface.</span></span> <span data-ttu-id="d443f-173">Ten interfejs jest tylko jedna metoda: [Execute](https://msdn.microsoft.com/library/azure/mt603945.aspx) i podpisie:</span><span class="sxs-lookup"><span data-stu-id="d443f-173">This interface has only one method: [Execute](https://msdn.microsoft.com/library/azure/mt603945.aspx) and its signature is:</span></span>

```csharp
public IDictionary<string, string> Execute(
        IEnumerable<LinkedService> linkedServices,
        IEnumerable<Dataset> datasets,
        Activity activity,
        IActivityLogger logger)
```


<span data-ttu-id="d443f-174">Metoda Hello przyjmuje cztery parametry:</span><span class="sxs-lookup"><span data-stu-id="d443f-174">hello method takes four parameters:</span></span>

- <span data-ttu-id="d443f-175">**linkedServices**.</span><span class="sxs-lookup"><span data-stu-id="d443f-175">**linkedServices**.</span></span> <span data-ttu-id="d443f-176">Ta właściwość jest wyliczalny listę usług połączonych magazyn danych odwołuje się zestaw danych wejścia/wyjścia dla działania hello.</span><span class="sxs-lookup"><span data-stu-id="d443f-176">This property is an enumerable list of Data Store linked services referenced by input/output datasets for hello activity.</span></span>   
- <span data-ttu-id="d443f-177">**zestawy danych**.</span><span class="sxs-lookup"><span data-stu-id="d443f-177">**datasets**.</span></span> <span data-ttu-id="d443f-178">Ta właściwość jest wyliczalny listę zestawów danych wejścia/wyjścia dla działania hello.</span><span class="sxs-lookup"><span data-stu-id="d443f-178">This property is an enumerable list of input/output datasets for hello activity.</span></span> <span data-ttu-id="d443f-179">Można użyć tego parametru tooget hello lokalizacji i schematów wynika z zestawów danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="d443f-179">You can use this parameter tooget hello locations and schemas defined by input and output datasets.</span></span>
- <span data-ttu-id="d443f-180">**działanie**.</span><span class="sxs-lookup"><span data-stu-id="d443f-180">**activity**.</span></span> <span data-ttu-id="d443f-181">Ta właściwość reprezentuje hello bieżącego działania.</span><span class="sxs-lookup"><span data-stu-id="d443f-181">This property represents hello current activity.</span></span> <span data-ttu-id="d443f-182">Może być używane tooaccess rozszerzone właściwości skojarzone z hello działań niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="d443f-182">It can be used tooaccess extended properties associated with hello custom activity.</span></span> <span data-ttu-id="d443f-183">Zobacz [dostępu właściwości rozszerzone](#access-extended-properties) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="d443f-183">See [Access extended properties](#access-extended-properties) for details.</span></span>
- <span data-ttu-id="d443f-184">**Rejestrator**.</span><span class="sxs-lookup"><span data-stu-id="d443f-184">**logger**.</span></span> <span data-ttu-id="d443f-185">Ten obiekt umożliwia zapisanie komentarze debugowania tej powierzchni w dzienniku użytkownika hello hello potoku.</span><span class="sxs-lookup"><span data-stu-id="d443f-185">This object lets you write debug comments that surface in hello user log for hello pipeline.</span></span>

<span data-ttu-id="d443f-186">Witaj, metoda zwraca słownik, który może być działań niestandardowych toochain używane razem w przyszłości hello.</span><span class="sxs-lookup"><span data-stu-id="d443f-186">hello method returns a dictionary that can be used toochain custom activities together in hello future.</span></span> <span data-ttu-id="d443f-187">Ta funkcja nie jest jeszcze zaimplementowana, więc Zwróć pusty słownik z metody hello.</span><span class="sxs-lookup"><span data-stu-id="d443f-187">This feature is not implemented yet, so return an empty dictionary from hello method.</span></span>  

### <a name="procedure"></a><span data-ttu-id="d443f-188">Procedura</span><span class="sxs-lookup"><span data-stu-id="d443f-188">Procedure</span></span>
1. <span data-ttu-id="d443f-189">Utwórz **Biblioteka klas programu .NET** projektu.</span><span class="sxs-lookup"><span data-stu-id="d443f-189">Create a **.NET Class Library** project.</span></span>
   <ol type="a">
     <li><span data-ttu-id="d443f-190">Uruchom <b>programu Visual Studio 2017</b> lub <b>programu Visual Studio 2015</b> lub <b>programu Visual Studio 2013</b> lub <b>programu Visual Studio 2012</b>.</span><span class="sxs-lookup"><span data-stu-id="d443f-190">Launch <b>Visual Studio 2017</b> or <b>Visual Studio 2015</b> or <b>Visual Studio 2013</b> or <b>Visual Studio 2012</b>.</span></span></li>
     <li><span data-ttu-id="d443f-191">Kliknij przycisk <b>pliku</b>, punktu zbyt<b>nowy</b>i kliknij przycisk <b>projektu</b>.</span><span class="sxs-lookup"><span data-stu-id="d443f-191">Click <b>File</b>, point too<b>New</b>, and click <b>Project</b>.</span></span></li>
     <li><span data-ttu-id="d443f-192">Rozwiń węzeł <b>Szablony</b> i wybierz opcję <b>Visual C#</b>.</span><span class="sxs-lookup"><span data-stu-id="d443f-192">Expand <b>Templates</b>, and select <b>Visual C#</b>.</span></span> <span data-ttu-id="d443f-193">W tym przewodniku Użyj C#, ale można użyć dowolnego .NET języka toodevelop hello działania niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="d443f-193">In this walkthrough, you use C#, but you can use any .NET language toodevelop hello custom activity.</span></span></li>
     <li><span data-ttu-id="d443f-194">Wybierz <b>biblioteki klas</b> z hello listy typów projektu na powitania prawo.</span><span class="sxs-lookup"><span data-stu-id="d443f-194">Select <b>Class Library</b> from hello list of project types on hello right.</span></span> <span data-ttu-id="d443f-195">VS 2017 wybierz <b>biblioteki klas (.NET Framework)</b> </span><span class="sxs-lookup"><span data-stu-id="d443f-195">In VS 2017, choose <b>Class Library (.NET Framework)</b> </span></span></li>
     <li><span data-ttu-id="d443f-196">Wprowadź <b>MyDotNetActivity</b> dla hello <b>nazwa</b>.</span><span class="sxs-lookup"><span data-stu-id="d443f-196">Enter <b>MyDotNetActivity</b> for hello <b>Name</b>.</span></span></li>
     <li><span data-ttu-id="d443f-197">Wybierz <b>C:\ADFGetStarted</b> dla hello <b>lokalizacji</b>.</span><span class="sxs-lookup"><span data-stu-id="d443f-197">Select <b>C:\ADFGetStarted</b> for hello <b>Location</b>.</span></span></li>
     <li><span data-ttu-id="d443f-198">Kliknij przycisk <b>OK</b> toocreate hello projektu.</span><span class="sxs-lookup"><span data-stu-id="d443f-198">Click <b>OK</b> toocreate hello project.</span></span></li>
   </ol><span data-ttu-id="d443f-199">
2.Kliknij przycisk **narzędzia**, punktu zbyt**Menedżera pakietów NuGet**i kliknij przycisk **Konsola Menedżera pakietów**.</span><span class="sxs-lookup"><span data-stu-id="d443f-199">
2. Click **Tools**, point too**NuGet Package Manager**, and click **Package Manager Console**.</span></span>
<span data-ttu-id="d443f-200">3.</span><span class="sxs-lookup"><span data-stu-id="d443f-200">3.</span></span> <span data-ttu-id="d443f-201">W konsoli Menedżera pakietów hello, wykonaj następujące polecenie tooimport hello **Microsoft.Azure.Management.DataFactories**.</span><span class="sxs-lookup"><span data-stu-id="d443f-201">In hello Package Manager Console, execute hello following command tooimport **Microsoft.Azure.Management.DataFactories**.</span></span>

    ```PowerShell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. <span data-ttu-id="d443f-202">Importuj hello **usługi Azure Storage** pakietu NuGet w projekcie toohello.</span><span class="sxs-lookup"><span data-stu-id="d443f-202">Import hello **Azure Storage** NuGet package in toohello project.</span></span>

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="d443f-203">Uruchamianie usługi fabryka danych wymaga wersji hello 4.3 WindowsAzure.Storage.</span><span class="sxs-lookup"><span data-stu-id="d443f-203">Data Factory service launcher requires hello 4.3 version of WindowsAzure.Storage.</span></span> <span data-ttu-id="d443f-204">Jeśli dodasz tooa odwołanie do nowszej wersji zestawu Azure Storage w projekcie działań niestandardowych, zostanie wyświetlony błąd podczas działania hello.</span><span class="sxs-lookup"><span data-stu-id="d443f-204">If you add a reference tooa later version of Azure Storage assembly in your custom activity project, you see an error when hello activity executes.</span></span> <span data-ttu-id="d443f-205">Błąd hello tooresolve, zobacz [izolacji elementu Appdomain](#appdomain-isolation) sekcji.</span><span class="sxs-lookup"><span data-stu-id="d443f-205">tooresolve hello error, see [Appdomain isolation](#appdomain-isolation) section.</span></span> 
5. <span data-ttu-id="d443f-206">Dodaj następujące hello **przy użyciu** plik źródłowy toohello instrukcje w projekcie hello.</span><span class="sxs-lookup"><span data-stu-id="d443f-206">Add hello following **using** statements toohello source file in hello project.</span></span>

    ```csharp

    // Comment these lines if using VS 2017
    using System.IO;
    using System.Globalization;
    using System.Diagnostics;
    using System.Linq;
    // --------------------

    // Comment these lines if using <= VS 2015
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    // ---------------------

    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Runtime;

    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```
6. <span data-ttu-id="d443f-207">Zmień nazwę hello hello **przestrzeni nazw** za**MyDotNetActivityNS**.</span><span class="sxs-lookup"><span data-stu-id="d443f-207">Change hello name of hello **namespace** too**MyDotNetActivityNS**.</span></span>

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. <span data-ttu-id="d443f-208">Zmień nazwę hello klasy hello zbyt**MyDotNetActivity** i pochodną hello **IDotNetActivity** interfejsu pokazane na powitania następującego fragmentu kodu:</span><span class="sxs-lookup"><span data-stu-id="d443f-208">Change hello name of hello class too**MyDotNetActivity** and derive it from hello **IDotNetActivity** interface as shown in hello following code snippet:</span></span>

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. <span data-ttu-id="d443f-209">Witaj wdrożenie (Dodaj) **Execute** metody hello **IDotNetActivity** interfejsu toohello **MyDotNetActivity** hello klasy i skopiuj następujące metody toohello kodu przykładowej.</span><span class="sxs-lookup"><span data-stu-id="d443f-209">Implement (Add) hello **Execute** method of hello **IDotNetActivity** interface toohello **MyDotNetActivity** class and copy hello following sample code toohello method.</span></span>

    <span data-ttu-id="d443f-210">Witaj następującym przykładowym zlicza hello wystąpienia terminu wyszukiwania hello ("Microsoft") w każdy obiekt blob skojarzony z wycinka danych.</span><span class="sxs-lookup"><span data-stu-id="d443f-210">hello following sample counts hello number of occurrences of hello search term (“Microsoft”) in each blob associated with a data slice.</span></span>

    ```csharp
    /// <summary>
    /// Execute method is hello only method of IDotNetActivity interface you must implement.
    /// In this sample, hello method invokes hello Calculate method tooperform hello core logic.  
    /// </summary>
    
    public IDictionary<string, string> Execute(
        IEnumerable<LinkedService> linkedServices,
        IEnumerable<Dataset> datasets,
        Activity activity,
        IActivityLogger logger)
    {
        // get extended properties defined in activity JSON definition
        // (for example: SliceStart)
        DotNetActivity dotNetActivity = (DotNetActivity)activity.TypeProperties;
        string sliceStartString = dotNetActivity.ExtendedProperties["SliceStart"];
    
        // toolog information, use hello logger object
        // log all extended properties            
        IDictionary<string, string> extendedProperties = dotNetActivity.ExtendedProperties;
        logger.Write("Logging extended properties if any...");
        foreach (KeyValuePair<string, string> entry in extendedProperties)
        {
            logger.Write("<key:{0}> <value:{1}>", entry.Key, entry.Value);
        }
    
        // linked service for input and output data stores
        // in this example, same storage is used for both input/output
        AzureStorageLinkedService inputLinkedService;

        // get hello input dataset
        Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
        // declare variables toohold type properties of input/output datasets
        AzureBlobDataset inputTypeProperties, outputTypeProperties;
        
        // get type properties from hello dataset object
        inputTypeProperties = inputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // log linked services passed in linkedServices parameter
        // you will see two linked services of type: AzureStorage
        // one for input dataset and hello other for output dataset 
        foreach (LinkedService ls in linkedServices)
            logger.Write("linkedService.Name {0}", ls.Name);
    
        // get hello first Azure Storate linked service from linkedServices object
        // using First method instead of Single since we are using hello same
        // Azure Storage linked service for input and output.
        inputLinkedService = linkedServices.First(
            linkedService =>
            linkedService.Name ==
            inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
            as AzureStorageLinkedService;
    
        // get hello connection string in hello linked service
        string connectionString = inputLinkedService.ConnectionString;
    
        // get hello folder path from hello input dataset definition
        string folderPath = GetFolderPath(inputDataset);
        string output = string.Empty; // for use later.
    
        // create storage client for input. Pass hello connection string.
        CloudStorageAccount inputStorageAccount = CloudStorageAccount.Parse(connectionString);
        CloudBlobClient inputClient = inputStorageAccount.CreateCloudBlobClient();
    
        // initialize hello continuation token before using it in hello do-while loop.
        BlobContinuationToken continuationToken = null;
        do
        {   // get hello list of input blobs from hello input storage client object.
            BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
                                     true,
                                     BlobListingDetails.Metadata,
                                     null,
                                     continuationToken,
                                     null,
                                     null);
    
            // Calculate method returns hello number of occurrences of
            // hello search term (“Microsoft”) in each blob associated
               // with hello data slice. definition of hello method is shown in hello next step.
    
            output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
        } while (continuationToken != null);
    
        // get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
        Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);

        // get type properties for hello output dataset
        outputTypeProperties = outputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // get hello folder path from hello output dataset definition
        folderPath = GetFolderPath(outputDataset);

        // log hello output folder path 
        logger.Write("Writing blob toohello folder: {0}", folderPath);
    
        // create a storage object for hello output blob.
        CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
        // write hello name of hello file.
        Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
        // log hello output file name
        logger.Write("output blob URI: {0}", outputBlobUri.ToString());

        // create a blob and upload hello output text.
        CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
        logger.Write("Writing {0} toohello output blob", output);
        outputBlob.UploadText(output);
    
        // hello dictionary can be used toochain custom activities together in hello future.
        // This feature is not implemented yet, so just return an empty dictionary.  
    
        return new Dictionary<string, string>();
    }
    ```
9. <span data-ttu-id="d443f-211">Dodaj następujące metody pomocnicze hello:</span><span class="sxs-lookup"><span data-stu-id="d443f-211">Add hello following helper methods:</span></span> 

    ```csharp
    /// <summary>
    /// Gets hello folderPath value from hello input/output dataset.
    /// </summary>
    
    private static string GetFolderPath(Dataset dataArtifact)
    {
        if (dataArtifact == null || dataArtifact.Properties == null)
        {
            return null;
        }

        // get type properties of hello dataset 
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return hello folder path found in hello type properties
        return blobDataset.FolderPath;
    }
    
    /// <summary>
    /// Gets hello fileName value from hello input/output dataset.   
    /// </summary>
    
    private static string GetFileName(Dataset dataArtifact)
    {
        if (dataArtifact == null || dataArtifact.Properties == null)
        {
            return null;
        }
    
        // get type properties of hello dataset
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return hello blob/file name in hello type properties
        return blobDataset.FileName;
    }
    
    /// <summary>
    /// Iterates through each blob (file) in hello folder, counts hello number of instances of search term in hello file,
    /// and prepares hello output text that is written toohello output blob.
    /// </summary>
    
    public static string Calculate(BlobResultSegment Bresult, IActivityLogger logger, string folderPath, ref BlobContinuationToken token, string searchTerm)
    {
        string output = string.Empty;
        logger.Write("number of blobs found: {0}", Bresult.Results.Count<IListBlobItem>());
        foreach (IListBlobItem listBlobItem in Bresult.Results)
        {
            CloudBlockBlob inputBlob = listBlobItem as CloudBlockBlob;
            if ((inputBlob != null) && (inputBlob.Name.IndexOf("$$$.$$$") == -1))
            {
                string blobText = inputBlob.DownloadText(Encoding.ASCII, null, null, null);
                logger.Write("input blob text: {0}", blobText);
                string[] source = blobText.Split(new char[] { '.', '?', '!', ' ', ';', ':', ',' }, StringSplitOptions.RemoveEmptyEntries);
                var matchQuery = from word in source
                                 where word.ToLowerInvariant() == searchTerm.ToLowerInvariant()
                                 select word;
                int wordCount = matchQuery.Count();
                output += string.Format("{0} occurrences(s) of hello search term \"{1}\" were found in hello file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
            }
        }
        return output;
    }
    ```

    <span data-ttu-id="d443f-212">Hello GetFolderPath metoda zwraca hello ścieżki toohello folderu, który hello zestawu danych punktów tooand hello GetFileName — metoda zwraca hello nazwę hello obiekt blob/pliku hello wskazuje zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="d443f-212">hello GetFolderPath method returns hello path toohello folder that hello dataset points tooand hello GetFileName method returns hello name of hello blob/file that hello dataset points to.</span></span> <span data-ttu-id="d443f-213">Jeśli użytkownik havefolderPath definiuje, korzystając ze zmiennych, takich jak {Year}, {Month}, {Day} itd., hello metoda zwraca ciąg hello, jak bez zamianę wartości środowiska uruchomieniowego.</span><span class="sxs-lookup"><span data-stu-id="d443f-213">If you havefolderPath defines using variables such as {Year}, {Month}, {Day} etc., hello method returns hello string as it is without replacing them with runtime values.</span></span> <span data-ttu-id="d443f-214">Zobacz [dostępu właściwości rozszerzone](#access-extended-properties) sekcji, aby uzyskać szczegółowe informacje dotyczące uzyskiwania dostępu do SliceStart, SliceEnd itp.</span><span class="sxs-lookup"><span data-stu-id="d443f-214">See [Access extended properties](#access-extended-properties) section for details on accessing SliceStart, SliceEnd, etc.</span></span>    

    ```JSON
    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "adftutorial/inputfolder/",
    ```

    <span data-ttu-id="d443f-215">Hello metody Calculate oblicza hello liczbę wystąpień słowa kluczowego hello plików wejściowych (obiekty BLOB w folderze hello) firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d443f-215">hello Calculate method calculates hello number of instances of keyword Microsoft in hello input files (blobs in hello folder).</span></span> <span data-ttu-id="d443f-216">Witaj terminu wyszukiwania ("Microsoft") jest ustalony w kodzie hello.</span><span class="sxs-lookup"><span data-stu-id="d443f-216">hello search term (“Microsoft”) is hard-coded in hello code.</span></span>
10. <span data-ttu-id="d443f-217">Skompiluj projekt hello.</span><span class="sxs-lookup"><span data-stu-id="d443f-217">Compile hello project.</span></span> <span data-ttu-id="d443f-218">Kliknij przycisk **kompilacji** hello menu i kliknij przycisk **Kompiluj rozwiązanie**.</span><span class="sxs-lookup"><span data-stu-id="d443f-218">Click **Build** from hello menu and click **Build Solution**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="d443f-219">Ustaw 4.5.2 wersję programu .NET Framework jako hello platformy docelowej projektu: kliknij prawym przyciskiem myszy projekt hello, a następnie kliknij przycisk **właściwości** platformy docelowej hello tooset.</span><span class="sxs-lookup"><span data-stu-id="d443f-219">Set 4.5.2 version of .NET Framework as hello target framework for your project: right-click hello project, and click **Properties** tooset hello target framework.</span></span> <span data-ttu-id="d443f-220">Fabryki danych nie obsługuje niestandardowych działań skompilowany .NET Framework w wersji nowszej niż 4.5.2.</span><span class="sxs-lookup"><span data-stu-id="d443f-220">Data Factory does not support custom activities compiled against .NET Framework versions later than 4.5.2.</span></span>

11. <span data-ttu-id="d443f-221">Uruchom **Eksploratora Windows**i przejdź zbyt**bin\debug** lub **bin\release** folder, w zależności od typu hello kompilacji.</span><span class="sxs-lookup"><span data-stu-id="d443f-221">Launch **Windows Explorer**, and navigate too**bin\debug** or **bin\release** folder depending on hello type of build.</span></span>
12. <span data-ttu-id="d443f-222">Utwórz plik zip **MyDotNetActivity.zip** zawierający wszystkie hello pliki binarne w hello <project folder>\bin\Debug folderu.</span><span class="sxs-lookup"><span data-stu-id="d443f-222">Create a zip file **MyDotNetActivity.zip** that contains all hello binaries in hello <project folder>\bin\Debug folder.</span></span> <span data-ttu-id="d443f-223">Zawierają hello **MyDotNetActivity.pdb** pliku, tak aby uzyskać dodatkowe szczegóły, takie jak numer wiersza w kodzie źródłowym hello, który spowodował problem hello, jeśli wystąpił błąd.</span><span class="sxs-lookup"><span data-stu-id="d443f-223">Include hello **MyDotNetActivity.pdb** file so that you get additional details such as line number in hello source code that caused hello issue if there was a failure.</span></span> 

    > [!IMPORTANT]
    > <span data-ttu-id="d443f-224">Wszystkie pliki w pliku zip hello Witaj dla działań niestandardowych hello musi znajdować się na powitania **najwyższego poziomu** z nie podfolderach.</span><span class="sxs-lookup"><span data-stu-id="d443f-224">All hello files in hello zip file for hello custom activity must be at hello **top level** with no sub folders.</span></span>

    ![Binarne pliki wyjściowe](./media/data-factory-use-custom-activities/Binaries.png)
14. <span data-ttu-id="d443f-226">Tworzenie kontenera obiektów blob o nazwie **customactivitycontainer** Jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="d443f-226">Create a blob container named **customactivitycontainer** if it does not already exist.</span></span> 
15. <span data-ttu-id="d443f-227">Przekaż MyDotNetActivity.zip jako customactivitycontainer toohello obiektów blob w **ogólnego przeznaczenia** magazynu obiektów blob platformy Azure (gorącą nie/chłodnej magazynu obiektów Blob), który odwołuje się do AzureStorageLinkedService.</span><span class="sxs-lookup"><span data-stu-id="d443f-227">Upload MyDotNetActivity.zip as a blob toohello customactivitycontainer in a **general-purpose** Azure blob storage (not hot/cool Blob storage) that is referred by AzureStorageLinkedService.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="d443f-228">Jeśli dodawanie tego rozwiązania tooa .NET działania projektu w programie Visual Studio, zawierający projekt fabryki danych i dodać projekt działania too.NET odwołanie z projektu aplikacji hello fabryki danych nie ma potrzeby tooperform hello ostatnie dwa kroki tworzenia ręcznie Witaj pliku zip i przekazać go toohello magazynu ogólnego przeznaczenia obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d443f-228">If you add this .NET activity project tooa solution in Visual Studio that contains a Data Factory project, and add a reference too.NET activity project from hello Data Factory application project, you do not need tooperform hello last two steps of manually creating hello zip file and uploading it toohello general-purpose Azure blob storage.</span></span> <span data-ttu-id="d443f-229">Podczas publikowania jednostek fabryki danych przy użyciu programu Visual Studio, te kroki automatycznie są wykonywane przez proces publikowania hello.</span><span class="sxs-lookup"><span data-stu-id="d443f-229">When you publish Data Factory entities using Visual Studio, these steps are automatically done by hello publishing process.</span></span> <span data-ttu-id="d443f-230">Aby uzyskać więcej informacji, zobacz [fabryki danych projektu programu Visual Studio](#data-factory-project-in-visual-studio) sekcji.</span><span class="sxs-lookup"><span data-stu-id="d443f-230">For more information, see [Data Factory project in Visual Studio](#data-factory-project-in-visual-studio) section.</span></span>

## <a name="create-a-pipeline-with-custom-activity"></a><span data-ttu-id="d443f-231">Utworzyć potok z działań niestandardowych</span><span class="sxs-lookup"><span data-stu-id="d443f-231">Create a pipeline with custom activity</span></span>
<span data-ttu-id="d443f-232">Utworzono niestandardowe działania i przekazać plik zip hello z kontenera obiektów blob tooa plików binarnych w **ogólnego przeznaczenia** konta magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="d443f-232">You have created a custom activity and uploaded hello zip file with binaries tooa blob container in a **general-purpose** Azure Storage Account.</span></span> <span data-ttu-id="d443f-233">W tej sekcji utworzysz fabryki danych Azure z potok, który używa hello działania niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="d443f-233">In this section, you create an Azure data factory with a pipeline that uses hello custom activity.</span></span>

<span data-ttu-id="d443f-234">Witaj wejściowego zestawu danych dla działań niestandardowych hello reprezentuje obiektów blob (pliki) w folderze customactivityinput hello adftutorial kontenera w magazynie obiektów blob hello.</span><span class="sxs-lookup"><span data-stu-id="d443f-234">hello input dataset for hello custom activity represents blobs (files) in hello customactivityinput folder of adftutorial container in hello blob storage.</span></span> <span data-ttu-id="d443f-235">Witaj wyjściowego zestawu danych działania hello reprezentuje obiekty BLOB danych wyjściowych w folderze customactivityoutput hello adftutorial kontenera w magazynie obiektów blob hello.</span><span class="sxs-lookup"><span data-stu-id="d443f-235">hello output dataset for hello activity represents output blobs in hello customactivityoutput folder of adftutorial container in hello blob storage.</span></span>

<span data-ttu-id="d443f-236">Utwórz **plik.txt** pliku z hello poniżej zawartości i przekaż go za**customactivityinput** folderu hello **adftutorial** kontenera.</span><span class="sxs-lookup"><span data-stu-id="d443f-236">Create **file.txt** file with hello following content and upload it too**customactivityinput** folder of hello **adftutorial** container.</span></span> <span data-ttu-id="d443f-237">Tworzenie kontenera adftutorial hello, jeśli już istnieje.</span><span class="sxs-lookup"><span data-stu-id="d443f-237">Create hello adftutorial container if it does not exist already.</span></span> 

```
test custom activity Microsoft test custom activity Microsoft
```

<span data-ttu-id="d443f-238">folder wejściowy Hello odpowiada wycinek tooa w fabryce danych Azure, nawet wtedy, gdy hello folder ma dwa lub więcej plików.</span><span class="sxs-lookup"><span data-stu-id="d443f-238">hello input folder corresponds tooa slice in Azure Data Factory even if hello folder has two or more files.</span></span> <span data-ttu-id="d443f-239">Każdy wycinek jest przetwarzany przez potok hello, działania niestandardowego hello iterację wszystkich hello obiektów blob w folderze wejściowych powitania dla tego wycinka.</span><span class="sxs-lookup"><span data-stu-id="d443f-239">When each slice is processed by hello pipeline, hello custom activity iterates through all hello blobs in hello input folder for that slice.</span></span>

<span data-ttu-id="d443f-240">Zobaczysz, że jeden wyjściowy plik z folderu adftutorial\customactivityoutput hello z jednego lub więcej wierszy (tak samo jak liczbę obiektów blob w folderze wejściowych hello):</span><span class="sxs-lookup"><span data-stu-id="d443f-240">You see one output file with in hello adftutorial\customactivityoutput folder with one or more lines (same as number of blobs in hello input folder):</span></span>

```
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2016-11-16-00/file.txt.
```


<span data-ttu-id="d443f-241">Poniżej przedstawiono kroki hello, wykonywanej w tej sekcji:</span><span class="sxs-lookup"><span data-stu-id="d443f-241">Here are hello steps you perform in this section:</span></span>

1. <span data-ttu-id="d443f-242">Utwórz **fabryki danych**.</span><span class="sxs-lookup"><span data-stu-id="d443f-242">Create a **data factory**.</span></span>
2. <span data-ttu-id="d443f-243">Utwórz **połączone usługi** hello partii zadań Azure puli maszyn wirtualnych, na których hello działania niestandardowego uruchamia i hello magazynu Azure, który przechowuje hello obiekty BLOB wejścia/wyjścia.</span><span class="sxs-lookup"><span data-stu-id="d443f-243">Create **Linked services** for hello Azure Batch pool of VMs on which hello custom activity runs and hello Azure Storage that holds hello input/output blobs.</span></span>
3. <span data-ttu-id="d443f-244">Utwórz dane wejściowe i wyjściowe **zestawów danych** reprezentujące dane wejściowe i wyjściowe hello działania niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="d443f-244">Create input and output **datasets** that represent input and output of hello custom activity.</span></span>
4. <span data-ttu-id="d443f-245">Utwórz **potoku** używającą hello działania niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="d443f-245">Create a **pipeline** that uses hello custom activity.</span></span>

> [!NOTE]
> <span data-ttu-id="d443f-246">Utwórz hello **plik.txt** i przekaż go tooa kontenera obiektów blob, jeśli jeszcze tego nie zrobiono.</span><span class="sxs-lookup"><span data-stu-id="d443f-246">Create hello **file.txt** and upload it tooa blob container if you haven't already done so.</span></span> <span data-ttu-id="d443f-247">Zobacz instrukcje w powyższej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="d443f-247">See instructions in hello preceding section.</span></span>   

### <a name="step-1-create-hello-data-factory"></a><span data-ttu-id="d443f-248">Krok 1: Tworzenie fabryki danych hello</span><span class="sxs-lookup"><span data-stu-id="d443f-248">Step 1: Create hello data factory</span></span>
1. <span data-ttu-id="d443f-249">Po zalogowaniu toohello w portalu Azure hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="d443f-249">After logging in toohello Azure portal, do hello following steps:</span></span>
   1. <span data-ttu-id="d443f-250">Kliknij przycisk **nowy** w menu po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="d443f-250">Click **NEW** on hello left menu.</span></span>
   2. <span data-ttu-id="d443f-251">Kliknij przycisk **dane i analiza** w hello **nowy** bloku.</span><span class="sxs-lookup"><span data-stu-id="d443f-251">Click **Data + Analytics** in hello **New** blade.</span></span>
   3. <span data-ttu-id="d443f-252">Kliknij przycisk **fabryki danych** na powitania **analizy danych** bloku.</span><span class="sxs-lookup"><span data-stu-id="d443f-252">Click **Data Factory** on hello **Data analytics** blade.</span></span>
   
    ![Nowe menu fabryki danych Azure](media/data-factory-use-custom-activities/new-azure-data-factory-menu.png)
2. <span data-ttu-id="d443f-254">W hello **nowa fabryka danych** bloku, wprowadź **CustomActivityFactory** dla hello nazwy.</span><span class="sxs-lookup"><span data-stu-id="d443f-254">In hello **New data factory** blade, enter **CustomActivityFactory** for hello Name.</span></span> <span data-ttu-id="d443f-255">Nazwa fabryki danych Azure hello Hello musi być globalnie unikatowe.</span><span class="sxs-lookup"><span data-stu-id="d443f-255">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="d443f-256">Jeśli wystąpi błąd hello: **nazwa fabryki danych "CustomActivityFactory" nie jest dostępna**, Zmień nazwę hello hello fabryki danych (na przykład **yournameCustomActivityFactory**) i spróbuj utworzyć ponownie.</span><span class="sxs-lookup"><span data-stu-id="d443f-256">If you receive hello error: **Data factory name “CustomActivityFactory” is not available**, change hello name of hello data factory (for example, **yournameCustomActivityFactory**) and try creating again.</span></span>

    ![Nowy blok fabryki danych Azure](media/data-factory-use-custom-activities/new-azure-data-factory-blade.png)
3. <span data-ttu-id="d443f-258">Kliknij przycisk **Nazwa grupy zasobów**i wybierz istniejącą grupę zasobów lub Utwórz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="d443f-258">Click **RESOURCE GROUP NAME**, and select an existing resource group or create a resource group.</span></span>
4. <span data-ttu-id="d443f-259">Sprawdź, czy są używa hello poprawne **subskrypcji** i **region** miejscu toobe fabryki danych hello utworzony.</span><span class="sxs-lookup"><span data-stu-id="d443f-259">Verify that you are using hello correct **subscription** and **region** where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="d443f-260">Kliknij przycisk **Utwórz** na powitania **nowa fabryka danych** bloku.</span><span class="sxs-lookup"><span data-stu-id="d443f-260">Click **Create** on hello **New data factory** blade.</span></span>
6. <span data-ttu-id="d443f-261">Zobacz hello fabryki danych tworzona w hello **pulpitu nawigacyjnego** z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d443f-261">You see hello data factory being created in hello **Dashboard** of hello Azure portal.</span></span>
7. <span data-ttu-id="d443f-262">Po hello fabryki danych został utworzony pomyślnie, zobacz hello fabryki danych bloku, który umożliwia hello zawartość hello fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="d443f-262">After hello data factory has been created successfully, you see hello Data Factory blade, which shows you hello contents of hello data factory.</span></span>
    
    ![Blok Fabryka danych](media/data-factory-use-custom-activities/data-factory-blade.png)

### <a name="step-2-create-linked-services"></a><span data-ttu-id="d443f-264">Krok 2: Tworzenie usługi połączonej</span><span class="sxs-lookup"><span data-stu-id="d443f-264">Step 2: Create linked services</span></span>
<span data-ttu-id="d443f-265">Połączone usługi łączenie magazyny danych lub obliczeniowe fabryki danych Azure tooan usług.</span><span class="sxs-lookup"><span data-stu-id="d443f-265">Linked services link data stores or compute services tooan Azure data factory.</span></span> <span data-ttu-id="d443f-266">W tym kroku możesz połączyć Twoje konto usługi Azure Storage i fabryki danych tooyour konto partii zadań Azure.</span><span class="sxs-lookup"><span data-stu-id="d443f-266">In this step, you link your Azure Storage account and Azure Batch account tooyour data factory.</span></span>

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="d443f-267">Tworzenie połączonej usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="d443f-267">Create Azure Storage linked service</span></span>
1. <span data-ttu-id="d443f-268">Kliknij hello **tworzenie i wdrażanie** Kafelek na powitania **FABRYKI danych** bloku **CustomActivityFactory**.</span><span class="sxs-lookup"><span data-stu-id="d443f-268">Click hello **Author and deploy** tile on hello **DATA FACTORY** blade for **CustomActivityFactory**.</span></span> <span data-ttu-id="d443f-269">Zostanie wyświetlony hello Edytor fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="d443f-269">You see hello Data Factory Editor.</span></span>
2. <span data-ttu-id="d443f-270">Kliknij przycisk **nowy magazyn danych** hello pasek poleceń i wybierz **magazynu Azure**.</span><span class="sxs-lookup"><span data-stu-id="d443f-270">Click **New data store** on hello command bar and choose **Azure storage**.</span></span> <span data-ttu-id="d443f-271">Powinny pojawić się hello skryptu JSON do tworzenia usługi Azure Storage połączonej usługi w edytorze hello.</span><span class="sxs-lookup"><span data-stu-id="d443f-271">You should see hello JSON script for creating an Azure Storage linked service in hello editor.</span></span>
    
    ![Nowy magazyn danych - Azure Storage](media/data-factory-use-custom-activities/new-data-store-menu.png)
3. <span data-ttu-id="d443f-273">Zastąp `<accountname>` z nazwą konta magazynu Azure i `<accountkey>` z kluczem dostępu z hello kontem magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d443f-273">Replace `<accountname>` with name of your Azure storage account and `<accountkey>` with access key of hello Azure storage account.</span></span> <span data-ttu-id="d443f-274">toolearn jak tooget Twojego magazynu uzyskują dostęp do klucza, zobacz [widoku, kopiowania i regenerate magazynu klucze dostępu](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="d443f-274">toolearn how tooget your storage access key, see [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

    ![Usługa Azure Storage zbędne usługi](media/data-factory-use-custom-activities/azure-storage-linked-service.png)
4. <span data-ttu-id="d443f-276">Kliknij przycisk **Wdróż** na pasku toodeploy hello połączone usługi poleceń hello.</span><span class="sxs-lookup"><span data-stu-id="d443f-276">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

#### <a name="create-azure-batch-linked-service"></a><span data-ttu-id="d443f-277">Tworzenie usługi partia zadań Azure połączone</span><span class="sxs-lookup"><span data-stu-id="d443f-277">Create Azure Batch linked service</span></span>
1. <span data-ttu-id="d443f-278">W hello Edytor fabryki danych, kliknij przycisk **... Więcej** na pasku poleceń hello, kliknij przycisk **nowych obliczeń**, a następnie wybierz **partii zadań Azure** hello menu.</span><span class="sxs-lookup"><span data-stu-id="d443f-278">In hello Data Factory Editor, click **... More** on hello command bar, click **New compute**, and then select **Azure Batch** from hello menu.</span></span>

    ![Nowe obliczeń - partii zadań Azure](media/data-factory-use-custom-activities/new-azure-compute-batch.png)
2. <span data-ttu-id="d443f-280">Wprowadź hello następującego skryptu JSON toohello zmiany:</span><span class="sxs-lookup"><span data-stu-id="d443f-280">Make hello following changes toohello JSON script:</span></span>

   1. <span data-ttu-id="d443f-281">Określ nazwę konta partii zadań Azure hello **accountName** właściwości.</span><span class="sxs-lookup"><span data-stu-id="d443f-281">Specify Azure Batch account name for hello **accountName** property.</span></span> <span data-ttu-id="d443f-282">Witaj **adres URL** z hello **bloku konta usługi partia zadań Azure** jest zgodny z formatem hello: `http://accountname.region.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="d443f-282">hello **URL** from hello **Azure Batch account blade** is in hello following format: `http://accountname.region.batch.azure.com`.</span></span> <span data-ttu-id="d443f-283">Dla hello **batchUri** właściwości w hello JSON, należy tooremove `accountname.` z hello adresu URL i użyj hello `accountname` dla hello `accountName` właściwości JSON.</span><span class="sxs-lookup"><span data-stu-id="d443f-283">For hello **batchUri** property in hello JSON, you need tooremove `accountname.` from hello URL and use hello `accountname` for hello `accountName` JSON property.</span></span>
   2. <span data-ttu-id="d443f-284">Określ klucz konta partii zadań Azure hello hello **accessKey** właściwości.</span><span class="sxs-lookup"><span data-stu-id="d443f-284">Specify hello Azure Batch account key for hello **accessKey** property.</span></span>
   3. <span data-ttu-id="d443f-285">Określ nazwę hello puli hello został utworzony jako część wymagania wstępne dotyczące hello **poolName** właściwości.</span><span class="sxs-lookup"><span data-stu-id="d443f-285">Specify hello name of hello pool you created as part of prerequisites for hello **poolName** property.</span></span> <span data-ttu-id="d443f-286">Można również określić identyfikator hello hello puli zamiast nazwy hello hello puli.</span><span class="sxs-lookup"><span data-stu-id="d443f-286">You can also specify hello ID of hello pool instead of hello name of hello pool.</span></span>
   4. <span data-ttu-id="d443f-287">Określ identyfikator URI usługi partia zadań Azure dla hello **batchUri** właściwości.</span><span class="sxs-lookup"><span data-stu-id="d443f-287">Specify Azure Batch URI for hello **batchUri** property.</span></span> <span data-ttu-id="d443f-288">Przykład: `https://westus.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="d443f-288">Example: `https://westus.batch.azure.com`.</span></span>  
   5. <span data-ttu-id="d443f-289">Określ hello **AzureStorageLinkedService** dla hello **linkedServiceName** właściwości.</span><span class="sxs-lookup"><span data-stu-id="d443f-289">Specify hello **AzureStorageLinkedService** for hello **linkedServiceName** property.</span></span>

        ```json
        {
         "name": "AzureBatchLinkedService",
         "properties": {
           "type": "AzureBatch",
           "typeProperties": {
             "accountName": "myazurebatchaccount",
             "batchUri": "https://westus.batch.azure.com",
             "accessKey": "<yourbatchaccountkey>",
             "poolName": "myazurebatchpool",
             "linkedServiceName": "AzureStorageLinkedService"
           }
         }
        }
        ```

       <span data-ttu-id="d443f-290">Dla hello **poolName** właściwości, można również określić identyfikator hello hello puli zamiast nazwy hello hello puli.</span><span class="sxs-lookup"><span data-stu-id="d443f-290">For hello **poolName** property, you can also specify hello ID of hello pool instead of hello name of hello pool.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="d443f-291">Hello usługi fabryka danych nie obsługuje opcji na żądanie dla partii zadań Azure, w przeciwieństwie do usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d443f-291">hello Data Factory service does not support an on-demand option for Azure Batch as it does for HDInsight.</span></span> <span data-ttu-id="d443f-292">Pulę partii zadań Azure można używać tylko w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="d443f-292">You can only use your own Azure Batch pool in an Azure data factory.</span></span>   
    

### <a name="step-3-create-datasets"></a><span data-ttu-id="d443f-293">Krok 3: Tworzenie zestawów danych</span><span class="sxs-lookup"><span data-stu-id="d443f-293">Step 3: Create datasets</span></span>
<span data-ttu-id="d443f-294">W tym kroku możesz utworzyć zestawy danych toorepresent w danych wejściowych i dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="d443f-294">In this step, you create datasets toorepresent input and output data.</span></span>

#### <a name="create-input-dataset"></a><span data-ttu-id="d443f-295">Tworzenie wejściowego zestawu danych</span><span class="sxs-lookup"><span data-stu-id="d443f-295">Create input dataset</span></span>
1. <span data-ttu-id="d443f-296">W hello **edytor** dla hello fabryki danych, kliknij przycisk **... Więcej** na pasku poleceń powitania kliknij **nowy zestaw danych**, a następnie wybierz **magazynu obiektów Blob Azure** z menu rozwijanego hello.</span><span class="sxs-lookup"><span data-stu-id="d443f-296">In hello **Editor** for hello Data Factory, click **... More** on hello command bar, click **New dataset**, and then select **Azure Blob storage** from hello drop-down menu.</span></span>
2. <span data-ttu-id="d443f-297">Zastąp hello JSON w okienku po prawej stronie powitania powitania po fragment kodu JSON:</span><span class="sxs-lookup"><span data-stu-id="d443f-297">Replace hello JSON in hello right pane with hello following JSON snippet:</span></span>

    ```json
    {
     "name": "InputDataset",
     "properties": {
         "type": "AzureBlob",
         "linkedServiceName": "AzureStorageLinkedService",
         "typeProperties": {
             "folderPath": "adftutorial/customactivityinput/",
             "format": {
                 "type": "TextFormat"
             }
         },
         "availability": {
             "frequency": "Hour",
             "interval": 1
         },
         "external": true,
         "policy": {}
     }
    }
    ```

   <span data-ttu-id="d443f-298">Utworzyć potok w dalszej części tego przewodnika, czas rozpoczęcia: 2016-11-16T00:00:00Z i na końcu czasu: 2016-11-16T05:00:00Z.</span><span class="sxs-lookup"><span data-stu-id="d443f-298">You create a pipeline later in this walkthrough with start time: 2016-11-16T00:00:00Z and end time: 2016-11-16T05:00:00Z.</span></span> <span data-ttu-id="d443f-299">Co godzinę, jest zaplanowane tooproduce danych co pięć wycinków wejścia/wyjścia (między **00**: 00:00 -> **05**: 00:00).</span><span class="sxs-lookup"><span data-stu-id="d443f-299">It is scheduled tooproduce data hourly, so there are five input/output slices (between **00**:00:00 -> **05**:00:00).</span></span>

   <span data-ttu-id="d443f-300">Witaj **częstotliwość** i **interwał** dla zestawu danych wejściowych hello jest ustawiony za**godzina** i **1**, co oznacza, że hello danych wejściowych jest dostępny co godzinę.</span><span class="sxs-lookup"><span data-stu-id="d443f-300">hello **frequency** and **interval** for hello input dataset is set too**Hour** and **1**, which means that hello input slice is available hourly.</span></span> <span data-ttu-id="d443f-301">W tym przykładzie jest takie same hello hello intputfolder pliku (plik.txt).</span><span class="sxs-lookup"><span data-stu-id="d443f-301">In this sample, it is hello same file (file.txt) in hello intputfolder.</span></span>

   <span data-ttu-id="d443f-302">Poniżej przedstawiono hello godziny rozpoczęcia dla każdego wycinka, która jest reprezentowana przez SliceStart zmienna w hello powyżej fragment kodu JSON.</span><span class="sxs-lookup"><span data-stu-id="d443f-302">Here are hello start times for each slice, which is represented by SliceStart system variable in hello above JSON snippet.</span></span>
3. <span data-ttu-id="d443f-303">Kliknij przycisk **Wdróż** hello toocreate narzędzi i wdrożyć hello **InputDataset**.</span><span class="sxs-lookup"><span data-stu-id="d443f-303">Click **Deploy** on hello toolbar toocreate and deploy hello **InputDataset**.</span></span> <span data-ttu-id="d443f-304">Upewnij się, że widoczny hello **tabeli UTWORZONE pomyślnie** wiadomości na pasku tytułu hello hello edytora.</span><span class="sxs-lookup"><span data-stu-id="d443f-304">Confirm that you see hello **TABLE CREATED SUCCESSFULLY** message on hello title bar of hello Editor.</span></span>

#### <a name="create-an-output-dataset"></a><span data-ttu-id="d443f-305">Tworzenie wyjściowego zestawu danych</span><span class="sxs-lookup"><span data-stu-id="d443f-305">Create an output dataset</span></span>
1. <span data-ttu-id="d443f-306">W hello **Edytor fabryki danych**, kliknij przycisk **... Więcej** na pasku poleceń powitania kliknij **nowy zestaw danych**, a następnie wybierz **magazynu obiektów Blob Azure**.</span><span class="sxs-lookup"><span data-stu-id="d443f-306">In hello **Data Factory editor**, click **... More** on hello command bar, click **New dataset**, and then select **Azure Blob storage**.</span></span>
2. <span data-ttu-id="d443f-307">Zastąp hello skryptu JSON w okienku po prawej stronie powitania hello następującego skryptu JSON:</span><span class="sxs-lookup"><span data-stu-id="d443f-307">Replace hello JSON script in hello right pane with hello following JSON script:</span></span>

    ```JSON
    {
        "name": "OutputDataset",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "{slice}.txt",
                "folderPath": "adftutorial/customactivityoutput/",
                "partitionedBy": [
                    {
                        "name": "slice",
                        "value": {
                            "type": "DateTime",
                            "date": "SliceStart",
                            "format": "yyyy-MM-dd-HH"
                        }
                    }
                ]
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```

     <span data-ttu-id="d443f-308">Lokalizacja danych wyjściowych jest **adftutorial/customactivityoutput/** i nazwa pliku wyjściowego jest RRRR MM-dd-HH.txt w przypadku RRRR MM-dd gg hello rok, miesiąc, datę i godzinę wycinek hello tworzonym.</span><span class="sxs-lookup"><span data-stu-id="d443f-308">Output location is **adftutorial/customactivityoutput/** and output file name is yyyy-MM-dd-HH.txt where yyyy-MM-dd-HH is hello year, month, date, and hour of hello slice being produced.</span></span> <span data-ttu-id="d443f-309">Zobacz [dokumentacja dla deweloperów] [ adf-developer-reference] szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="d443f-309">See [Developer Reference][adf-developer-reference] for details.</span></span>

    <span data-ttu-id="d443f-310">Obiekt blob/plik wyjściowy jest generowany dla każdego wejściowego wycinka.</span><span class="sxs-lookup"><span data-stu-id="d443f-310">An output blob/file is generated for each input slice.</span></span> <span data-ttu-id="d443f-311">Oto, jak dla każdego wycinka nosi nazwę pliku wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="d443f-311">Here is how an output file is named for each slice.</span></span> <span data-ttu-id="d443f-312">Wszystkie pliki wyjściowe hello są generowane w jednym folderze wyjściowym: **adftutorial\customactivityoutput**.</span><span class="sxs-lookup"><span data-stu-id="d443f-312">All hello output files are generated in one output folder: **adftutorial\customactivityoutput**.</span></span>

   | <span data-ttu-id="d443f-313">Wycinek</span><span class="sxs-lookup"><span data-stu-id="d443f-313">Slice</span></span> | <span data-ttu-id="d443f-314">Godzina rozpoczęcia</span><span class="sxs-lookup"><span data-stu-id="d443f-314">Start time</span></span> | <span data-ttu-id="d443f-315">Plik wyjściowy</span><span class="sxs-lookup"><span data-stu-id="d443f-315">Output file</span></span> |
   |:--- |:--- |:--- |
   | <span data-ttu-id="d443f-316">1</span><span class="sxs-lookup"><span data-stu-id="d443f-316">1</span></span> |<span data-ttu-id="d443f-317">2016-11-16T00:00:00</span><span class="sxs-lookup"><span data-stu-id="d443f-317">2016-11-16T00:00:00</span></span> |<span data-ttu-id="d443f-318">2016-11-16-00.txt</span><span class="sxs-lookup"><span data-stu-id="d443f-318">2016-11-16-00.txt</span></span> |
   | <span data-ttu-id="d443f-319">2</span><span class="sxs-lookup"><span data-stu-id="d443f-319">2</span></span> |<span data-ttu-id="d443f-320">2016-11-16T01:00:00</span><span class="sxs-lookup"><span data-stu-id="d443f-320">2016-11-16T01:00:00</span></span> |<span data-ttu-id="d443f-321">2016-11-16-01.txt</span><span class="sxs-lookup"><span data-stu-id="d443f-321">2016-11-16-01.txt</span></span> |
   | <span data-ttu-id="d443f-322">3</span><span class="sxs-lookup"><span data-stu-id="d443f-322">3</span></span> |<span data-ttu-id="d443f-323">2016-11-16T02:00:00</span><span class="sxs-lookup"><span data-stu-id="d443f-323">2016-11-16T02:00:00</span></span> |<span data-ttu-id="d443f-324">2016-11-16-02.txt</span><span class="sxs-lookup"><span data-stu-id="d443f-324">2016-11-16-02.txt</span></span> |
   | <span data-ttu-id="d443f-325">4</span><span class="sxs-lookup"><span data-stu-id="d443f-325">4</span></span> |<span data-ttu-id="d443f-326">2016-11-16T03:00:00</span><span class="sxs-lookup"><span data-stu-id="d443f-326">2016-11-16T03:00:00</span></span> |<span data-ttu-id="d443f-327">2016-11-16-03.txt</span><span class="sxs-lookup"><span data-stu-id="d443f-327">2016-11-16-03.txt</span></span> |
   | <span data-ttu-id="d443f-328">5</span><span class="sxs-lookup"><span data-stu-id="d443f-328">5</span></span> |<span data-ttu-id="d443f-329">2016-11-16T04:00:00</span><span class="sxs-lookup"><span data-stu-id="d443f-329">2016-11-16T04:00:00</span></span> |<span data-ttu-id="d443f-330">2016-11-16-04.txt</span><span class="sxs-lookup"><span data-stu-id="d443f-330">2016-11-16-04.txt</span></span> |

    <span data-ttu-id="d443f-331">Należy pamiętać, że wszystkie pliki hello w folderze wejściowych część wycinek z godziny rozpoczęcia hello wymienionych powyżej.</span><span class="sxs-lookup"><span data-stu-id="d443f-331">Remember that all hello files in an input folder are part of a slice with hello start times mentioned above.</span></span> <span data-ttu-id="d443f-332">Podczas przetwarzania tego wycinka działania niestandardowego hello skanowania za pomocą każdego pliku i tworzy wiersz w pliku wyjściowym hello hello liczby wystąpień terminu wyszukiwania ("Microsoft").</span><span class="sxs-lookup"><span data-stu-id="d443f-332">When this slice is processed, hello custom activity scans through each file and produces a line in hello output file with hello number of occurrences of search term (“Microsoft”).</span></span> <span data-ttu-id="d443f-333">Jeśli istnieją trzy pliki w hello inputfolder, istnieją trzy wiersze w pliku wyjściowym hello każdego co godzinę wycinka: 2016-11-16-00.txt 2016-11-16:01:00:00.txt itp.</span><span class="sxs-lookup"><span data-stu-id="d443f-333">If there are three files in hello inputfolder, there are three lines in hello output file for each hourly slice: 2016-11-16-00.txt, 2016-11-16:01:00:00.txt, etc.</span></span>
3. <span data-ttu-id="d443f-334">Witaj toodeploy **OutputDataset**, kliknij przycisk **Wdróż** na powitania paska poleceń.</span><span class="sxs-lookup"><span data-stu-id="d443f-334">toodeploy hello **OutputDataset**, click **Deploy** on hello command bar.</span></span>

### <a name="create-and-run-a-pipeline-that-uses-hello-custom-activity"></a><span data-ttu-id="d443f-335">Tworzenie i uruchamianie potok, który używa hello niestandardowego działania</span><span class="sxs-lookup"><span data-stu-id="d443f-335">Create and run a pipeline that uses hello custom activity</span></span>
1. <span data-ttu-id="d443f-336">W hello Edytor fabryki danych, kliknij przycisk **... Więcej**, a następnie wybierz **nowy potok** na powitania paska poleceń.</span><span class="sxs-lookup"><span data-stu-id="d443f-336">In hello Data Factory Editor, click **... More**, and then select **New pipeline** on hello command bar.</span></span> 
2. <span data-ttu-id="d443f-337">Zastąp hello JSON w okienku po prawej stronie powitania hello następującego skryptu JSON:</span><span class="sxs-lookup"><span data-stu-id="d443f-337">Replace hello JSON in hello right pane with hello following JSON script:</span></span>

    ```JSON
    {
      "name": "ADFTutorialPipelineCustom",
      "properties": {
        "description": "Use custom activity",
        "activities": [
          {
            "Name": "MyDotNetActivity",
            "Type": "DotNetActivity",
            "Inputs": [
              {
                "Name": "InputDataset"
              }
            ],
            "Outputs": [
              {
                "Name": "OutputDataset"
              }
            ],
            "LinkedServiceName": "AzureBatchLinkedService",
            "typeProperties": {
              "AssemblyName": "MyDotNetActivity.dll",
              "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
              "PackageLinkedService": "AzureStorageLinkedService",
              "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
              "extendedProperties": {
                "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
              }
            },
            "Policy": {
              "Concurrency": 2,
              "ExecutionPriorityOrder": "OldestFirst",
              "Retry": 3,
              "Timeout": "00:30:00",
              "Delay": "00:00:00"
            }
          }
        ],
        "start": "2016-11-16T00:00:00Z",
        "end": "2016-11-16T05:00:00Z",
        "isPaused": false
      }
    }
    ```

    <span data-ttu-id="d443f-338">Należy zwrócić uwagę hello następujące punkty:</span><span class="sxs-lookup"><span data-stu-id="d443f-338">Note hello following points:</span></span>

   * <span data-ttu-id="d443f-339">**Współbieżność** ustawiono zbyt**2** tak, aby dwa wycinków są przetwarzane równolegle przez 2 maszyny wirtualne w puli partii zadań Azure hello.</span><span class="sxs-lookup"><span data-stu-id="d443f-339">**Concurrency** is set too**2** so that two slices are processed in parallel by 2 VMs in hello Azure Batch pool.</span></span>
   * <span data-ttu-id="d443f-340">W sekcji działania hello jest jedno działanie i jest typu: **DotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="d443f-340">There is one activity in hello activities section and it is of type: **DotNetActivity**.</span></span>
   * <span data-ttu-id="d443f-341">**AssemblyName** jest ustawiona na nazwę toohello hello biblioteki DLL: **MyDotnetActivity.dll**.</span><span class="sxs-lookup"><span data-stu-id="d443f-341">**AssemblyName** is set toohello name of hello DLL: **MyDotnetActivity.dll**.</span></span>
   * <span data-ttu-id="d443f-342">**Punkt wejścia** ustawiono zbyt**MyDotNetActivityNS.MyDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="d443f-342">**EntryPoint** is set too**MyDotNetActivityNS.MyDotNetActivity**.</span></span>
   * <span data-ttu-id="d443f-343">**PackageLinkedService** ustawiono zbyt**AzureStorageLinkedService** wskazującego toohello magazynu obiektów blob, zawierający plik zip hello działania niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="d443f-343">**PackageLinkedService** is set too**AzureStorageLinkedService** that points toohello blob storage that contains hello custom activity zip file.</span></span> <span data-ttu-id="d443f-344">Jeśli korzystasz z innego konta usługi Azure Storage dla wejścia/wyjścia plików i hello działania niestandardowego pliku zip, utworzysz innego połączoną usługą magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="d443f-344">If you are using different Azure Storage accounts for input/output files and hello custom activity zip file, you create another Azure Storage linked service.</span></span> <span data-ttu-id="d443f-345">W tym artykule przyjęto założenie, że używasz hello tego samego konta magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="d443f-345">This article assumes that you are using hello same Azure Storage account.</span></span>
   * <span data-ttu-id="d443f-346">**PackageFile** ustawiono zbyt**customactivitycontainer/MyDotNetActivity.zip**.</span><span class="sxs-lookup"><span data-stu-id="d443f-346">**PackageFile** is set too**customactivitycontainer/MyDotNetActivity.zip**.</span></span> <span data-ttu-id="d443f-347">Jest w formacie hello: containerforthezip/nameofthezip.zip.</span><span class="sxs-lookup"><span data-stu-id="d443f-347">It is in hello format: containerforthezip/nameofthezip.zip.</span></span>
   * <span data-ttu-id="d443f-348">przyjmuje działania niestandardowego Hello **InputDataset** jako dane wejściowe i **OutputDataset** jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="d443f-348">hello custom activity takes **InputDataset** as input and **OutputDataset** as output.</span></span>
   * <span data-ttu-id="d443f-349">Hello właściwość linkedServiceName działania niestandardowego hello punktów toohello **AzureBatchLinkedService**, który informuje usługi fabryka danych Azure tego działania niestandardowego hello musi toorun na maszynach wirtualnych Azure partii.</span><span class="sxs-lookup"><span data-stu-id="d443f-349">hello linkedServiceName property of hello custom activity points toohello **AzureBatchLinkedService**, which tells Azure Data Factory that hello custom activity needs toorun on Azure Batch VMs.</span></span>
   * <span data-ttu-id="d443f-350">**isPaused** właściwość jest ustawiona zbyt**false** domyślnie.</span><span class="sxs-lookup"><span data-stu-id="d443f-350">**isPaused** property is set too**false** by default.</span></span> <span data-ttu-id="d443f-351">potok Hello uruchamia natychmiast w tym przykładzie, ponieważ wycinków hello uruchomić w przeszłości hello.</span><span class="sxs-lookup"><span data-stu-id="d443f-351">hello pipeline runs immediately in this example because hello slices start in hello past.</span></span> <span data-ttu-id="d443f-352">Można ustawić tej właściwości tootrue toopause hello potoku i ustaw ją toorestart toofalse Wstecz.</span><span class="sxs-lookup"><span data-stu-id="d443f-352">You can set this property tootrue toopause hello pipeline and set it back toofalse toorestart.</span></span>
   * <span data-ttu-id="d443f-353">Witaj **start** czasu i **zakończenia** czasy są **pięć** godziny od siebie i wycinki są tworzone co godzinę, więc pięć wycinków są produkowane przez potok hello.</span><span class="sxs-lookup"><span data-stu-id="d443f-353">hello **start** time and **end** times are **five** hours apart and slices are produced hourly, so five slices are produced by hello pipeline.</span></span>
3. <span data-ttu-id="d443f-354">toodeploy hello potoku, kliknij przycisk **Wdróż** na powitania paska poleceń.</span><span class="sxs-lookup"><span data-stu-id="d443f-354">toodeploy hello pipeline, click **Deploy** on hello command bar.</span></span>

### <a name="monitor-hello-pipeline"></a><span data-ttu-id="d443f-355">Monitor hello potoku</span><span class="sxs-lookup"><span data-stu-id="d443f-355">Monitor hello pipeline</span></span>
1. <span data-ttu-id="d443f-356">W bloku fabryki danych hello w hello portalu Azure, kliknij przycisk **Diagram**.</span><span class="sxs-lookup"><span data-stu-id="d443f-356">In hello Data Factory blade in hello Azure portal, click **Diagram**.</span></span>

    ![Kafelek Diagram](./media/data-factory-use-custom-activities/DataFactoryBlade.png)
2. <span data-ttu-id="d443f-358">W hello widoku diagramu kliknij przycisk hello OutputDataset.</span><span class="sxs-lookup"><span data-stu-id="d443f-358">In hello Diagram View, now click hello OutputDataset.</span></span>

    ![Widok diagramu](./media/data-factory-use-custom-activities/diagram.png)
3. <span data-ttu-id="d443f-360">Powinny być widoczne czy hello pięć wycinki danych wyjściowych znajdują się w stanie gotowe hello.</span><span class="sxs-lookup"><span data-stu-id="d443f-360">You should see that hello five output slices are in hello Ready state.</span></span> <span data-ttu-id="d443f-361">Jeśli nie są w stanie gotowe hello, nie została opracowana jeszcze.</span><span class="sxs-lookup"><span data-stu-id="d443f-361">If they are not in hello Ready state, they haven't been produced yet.</span></span> 

   ![Wycinki danych wyjściowych](./media/data-factory-use-custom-activities/OutputSlices.png)
4. <span data-ttu-id="d443f-363">Sprawdź, czy pliki wyjściowe hello są generowane w magazynie obiektów blob hello w hello **adftutorial** kontenera.</span><span class="sxs-lookup"><span data-stu-id="d443f-363">Verify that hello output files are generated in hello blob storage in hello **adftutorial** container.</span></span>

   ![dane wyjściowe z działań niestandardowych][image-data-factory-ouput-from-custom-activity]
5. <span data-ttu-id="d443f-365">Po otwarciu pliku wyjściowego hello powinien pojawić się hello dane wyjściowe podobne toohello następujące dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="d443f-365">If you open hello output file, you should see hello output similar toohello following output:</span></span>

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2016-11-16-00/file.txt.
    ```
6. <span data-ttu-id="d443f-366">Użyj hello [portalu Azure] [ azure-preview-portal] lub toomonitor poleceń cmdlet programu Azure PowerShell z fabryki danych, potoki i zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="d443f-366">Use hello [Azure portal][azure-preview-portal] or Azure PowerShell cmdlets toomonitor your data factory, pipelines, and data sets.</span></span> <span data-ttu-id="d443f-367">Można wyświetlić wiadomości z hello **ActivityLogger** w kodzie hello hello niestandardowego działania w dziennikach hello (w szczególności 0.log użytkownika), które można pobrać z portalu hello lub przy użyciu poleceń cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d443f-367">You can see messages from hello **ActivityLogger** in hello code for hello custom activity in hello logs (specifically user-0.log) that you can download from hello portal or using cmdlets.</span></span>

   ![Pobierz dzienniki z działań niestandardowych][image-data-factory-download-logs-from-custom-activity]

<span data-ttu-id="d443f-369">Zobacz [monitorować i zarządzać potoki](data-factory-monitor-manage-pipelines.md) szczegółowy opis kroków monitorowania zestawy danych i potoki.</span><span class="sxs-lookup"><span data-stu-id="d443f-369">See [Monitor and Manage Pipelines](data-factory-monitor-manage-pipelines.md) for detailed steps for monitoring datasets and pipelines.</span></span>      

## <a name="data-factory-project-in-visual-studio"></a><span data-ttu-id="d443f-370">Projekt fabryki danych w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d443f-370">Data Factory project in Visual Studio</span></span>  
<span data-ttu-id="d443f-371">Można tworzyć i publikować jednostek fabryki danych przy użyciu programu Visual Studio, a za pomocą portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d443f-371">You can create and publish Data Factory entities by using Visual Studio instead of using Azure portal.</span></span> <span data-ttu-id="d443f-372">Szczegółowe informacje na temat tworzenia i publikowania jednostek fabryki danych przy użyciu programu Visual Studio, zobacz [kompilacji swój pierwszy potok, za pomocą programu Visual Studio](data-factory-build-your-first-pipeline-using-vs.md) i [kopiowanie danych z obiektu Blob Azure tooAzure SQL](data-factory-copy-activity-tutorial-using-visual-studio.md) artykuły.</span><span class="sxs-lookup"><span data-stu-id="d443f-372">For detailed information about creating and publishing Data Factory entities by using Visual Studio, See [Build your first pipeline using Visual Studio](data-factory-build-your-first-pipeline-using-vs.md) and [Copy data from Azure Blob tooAzure SQL](data-factory-copy-activity-tutorial-using-visual-studio.md) articles.</span></span>

<span data-ttu-id="d443f-373">Witaj, następujące dodatkowe kroki w przypadku tworzenia projektu fabryki danych w programie Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="d443f-373">Do hello following additional steps if you are creating Data Factory project in Visual Studio:</span></span>
 
1. <span data-ttu-id="d443f-374">Dodaj hello fabryki danych projektu toohello rozwiązania Visual Studio, zawierającego hello projektu działania niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="d443f-374">Add hello Data Factory project toohello Visual Studio solution that contains hello custom activity project.</span></span> 
2. <span data-ttu-id="d443f-375">Dodać projekt działania .NET toohello odwołanie z hello fabryki danych projektu.</span><span class="sxs-lookup"><span data-stu-id="d443f-375">Add a reference toohello .NET activity project from hello Data Factory project.</span></span> <span data-ttu-id="d443f-376">Kliknij prawym przyciskiem myszy projekt w fabryce danych, wskaż zbyt**Dodaj**, a następnie kliknij przycisk **odwołania**.</span><span class="sxs-lookup"><span data-stu-id="d443f-376">Right-click Data Factory project, point too**Add**, and then click **Reference**.</span></span> 
3. <span data-ttu-id="d443f-377">W hello **Dodaj odwołanie** okno dialogowe, wybierz opcję hello **MyDotNetActivity** projektu, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="d443f-377">In hello **Add Reference** dialog box, select hello **MyDotNetActivity** project, and click **OK**.</span></span>
4. <span data-ttu-id="d443f-378">Tworzenie i publikowanie hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="d443f-378">Build and publish hello solution.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="d443f-379">Podczas publikowania jednostek fabryki danych pliku zip jest automatycznie tworzony i jest przekazany toohello kontenera obiektów blob: customactivitycontainer.</span><span class="sxs-lookup"><span data-stu-id="d443f-379">When you publish Data Factory entities, a zip file is automatically created for you and is uploaded toohello blob container: customactivitycontainer.</span></span> <span data-ttu-id="d443f-380">Jeśli hello kontenera obiektów blob nie istnieje, jest on automatycznie tworzony zbyt.</span><span class="sxs-lookup"><span data-stu-id="d443f-380">If hello blob container does not exist, it is automatically created too.</span></span>  


## <a name="data-factory-and-batch-integration"></a><span data-ttu-id="d443f-381">Integracja z fabryki danych i usługi partia zadań</span><span class="sxs-lookup"><span data-stu-id="d443f-381">Data Factory and Batch integration</span></span>
<span data-ttu-id="d443f-382">Witaj usługi fabryka danych tworzy zadanie w partii zadań Azure o nazwie hello: **adf poolname: xxx zadania**.</span><span class="sxs-lookup"><span data-stu-id="d443f-382">hello Data Factory service creates a job in Azure Batch with hello name: **adf-poolname: job-xxx**.</span></span> <span data-ttu-id="d443f-383">Kliknij przycisk **zadania** z menu po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="d443f-383">Click **Jobs** from hello left menu.</span></span> 

![Fabryka danych Azure - zadań wsadowych](media/data-factory-use-custom-activities/data-factory-batch-jobs.png)

<span data-ttu-id="d443f-385">Zadanie jest tworzone przy każdym uruchomieniu działania wycinek.</span><span class="sxs-lookup"><span data-stu-id="d443f-385">A task is created for each activity run of a slice.</span></span> <span data-ttu-id="d443f-386">W przypadku pięć toobe gotowy wycinków przetwarzane pięć zadań są tworzone w ramach tego zadania.</span><span class="sxs-lookup"><span data-stu-id="d443f-386">If there are five slices ready toobe processed, five tasks are created in this job.</span></span> <span data-ttu-id="d443f-387">Jeśli istnieje wiele węzłów obliczeniowych w puli partii hello, co najmniej dwa wycinków można uruchomić równolegle.</span><span class="sxs-lookup"><span data-stu-id="d443f-387">If there are multiple compute nodes in hello Batch pool, two or more slices can run in parallel.</span></span> <span data-ttu-id="d443f-388">Jeśli obliczeniowe hello maksymalną zadań na zestaw węzłów zbyt > 1, może także zawierać więcej niż jeden wycinek uruchomionych na powitania tego samego obliczeń.</span><span class="sxs-lookup"><span data-stu-id="d443f-388">If hello maximum tasks per compute node is set too> 1, you can also have more than one slice running on hello same compute.</span></span>

![Fabryka danych Azure - zadań zadania wsadowego](media/data-factory-use-custom-activities/data-factory-batch-job-tasks.png)

<span data-ttu-id="d443f-390">powitania po diagram ilustruje hello relacji między fabryki danych Azure i partii zadań.</span><span class="sxs-lookup"><span data-stu-id="d443f-390">hello following diagram illustrates hello relationship between Azure Data Factory and Batch tasks.</span></span>

![Fabryka danych & partii](./media/data-factory-use-custom-activities/DataFactoryAndBatch.png)

## <a name="troubleshoot-failures"></a><span data-ttu-id="d443f-392">Rozwiązywanie problemów z błędami</span><span class="sxs-lookup"><span data-stu-id="d443f-392">Troubleshoot failures</span></span>
<span data-ttu-id="d443f-393">Rozwiązywanie problemów z składa się z kilku podstawowych techniki:</span><span class="sxs-lookup"><span data-stu-id="d443f-393">Troubleshooting consists of a few basic techniques:</span></span>

1. <span data-ttu-id="d443f-394">Jeśli zostanie wyświetlony następujący błąd hello, używasz magazynu obiektów blob aktywny/chłodnej zamiast przy użyciu magazynu obiektów blob platformy Azure ogólnego przeznaczenia.</span><span class="sxs-lookup"><span data-stu-id="d443f-394">If you see hello following error, you may be using a Hot/Cool blob storage instead of using a general-purpose Azure blob storage.</span></span> <span data-ttu-id="d443f-395">Przekaż tooa pliku zip hello **ogólnego przeznaczenia konta magazynu Azure**.</span><span class="sxs-lookup"><span data-stu-id="d443f-395">Upload hello zip file tooa **general-purpose Azure Storage Account**.</span></span> 
 
    ```
    Error in Activity: Job encountered scheduling error. Code: BlobDownloadMiscError Category: ServerError Message: Miscellaneous error encountered while downloading one of hello specified Azure Blob(s).
    ``` 
2. <span data-ttu-id="d443f-396">Jeśli zostanie wyświetlony następujący błąd hello, upewnij się, że hello nazwy klasy hello w hello CS dopasowań hello nazwa pliku podana dla hello **punktu wejścia** właściwości w potoku hello JSON.</span><span class="sxs-lookup"><span data-stu-id="d443f-396">If you see hello following error, confirm that hello name of hello class in hello CS file matches hello name you specified for hello **EntryPoint** property in hello pipeline JSON.</span></span> <span data-ttu-id="d443f-397">W przewodniku hello jest nazwa klasy hello: MyDotNetActivity i hello punktu wejścia w hello JSON: MyDotNetActivityNS. **MyDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="d443f-397">In hello walkthrough, name of hello class is: MyDotNetActivity, and hello EntryPoint in hello JSON is: MyDotNetActivityNS.**MyDotNetActivity**.</span></span>

    ```
    MyDotNetActivity assembly does not exist or doesn't implement hello type Microsoft.DataFactories.Runtime.IDotNetActivity properly
    ```

   <span data-ttu-id="d443f-398">Jeśli hello nazwy są zgodne, potwierdź, że wszystkie pliki binarne hello są w hello **folderu głównego** hello pliku zip.</span><span class="sxs-lookup"><span data-stu-id="d443f-398">If hello names do match, confirm that all hello binaries are in hello **root folder** of hello zip file.</span></span> <span data-ttu-id="d443f-399">Oznacza to, że podczas otwierania pliku zip hello powinna zostać wyświetlona wszystkie pliki hello w folderze głównym hello, a nie wszystkie podfoldery.</span><span class="sxs-lookup"><span data-stu-id="d443f-399">That is, when you open hello zip file, you should see all hello files in hello root folder, not in any sub folders.</span></span>   
3. <span data-ttu-id="d443f-400">Jeśli hello wycinek wejściowy nie jest ustawiona zbyt**gotowe**, potwierdź poprawność struktury folderów wejściowych hello i **plik.txt** istnieje w folderach wejściowych hello.</span><span class="sxs-lookup"><span data-stu-id="d443f-400">If hello input slice is not set too**Ready**, confirm that hello input folder structure is correct and **file.txt** exists in hello input folders.</span></span>
3. <span data-ttu-id="d443f-401">W hello **Execute** metody działania niestandardowego, użyj hello **IActivityLogger** toolog informacji o obiekcie, ułatwiające rozwiązywanie problemów.</span><span class="sxs-lookup"><span data-stu-id="d443f-401">In hello **Execute** method of your custom activity, use hello **IActivityLogger** object toolog information that helps you troubleshoot issues.</span></span> <span data-ttu-id="d443f-402">wiadomości powitania rejestrowane uwzględniane w plikach dziennika użytkownika hello (co najmniej jeden plik o nazwie: 0.log użytkownika, 1.log użytkownika, użytkownik 2.log itp.).</span><span class="sxs-lookup"><span data-stu-id="d443f-402">hello logged messages show up in hello user log files (one or more files named: user-0.log, user-1.log, user-2.log, etc.).</span></span>

   <span data-ttu-id="d443f-403">W hello **OutputDataset** bloku, kliknij przycisk hello wycinek toosee hello **WYCINKA danych** bloku dla tego wycinka.</span><span class="sxs-lookup"><span data-stu-id="d443f-403">In hello **OutputDataset** blade, click hello slice toosee hello **DATA SLICE** blade for that slice.</span></span> <span data-ttu-id="d443f-404">Zostanie wyświetlony **uruchomień działania** dla tego wycinka.</span><span class="sxs-lookup"><span data-stu-id="d443f-404">You see **activity runs** for that slice.</span></span> <span data-ttu-id="d443f-405">Powinny pojawić się jeden uruchamiania dla wycinka hello działania.</span><span class="sxs-lookup"><span data-stu-id="d443f-405">You should see one activity run for hello slice.</span></span> <span data-ttu-id="d443f-406">Jeśli na pasku poleceń powitania kliknij przycisk Uruchom, możesz uruchomić innego działania Uruchom hello tego samego wycinka.</span><span class="sxs-lookup"><span data-stu-id="d443f-406">If you click Run in hello command bar, you can start another activity run for hello same slice.</span></span>

   <span data-ttu-id="d443f-407">Po kliknięciu przycisku uruchamiania działania hello Zobacz hello **szczegóły uruchomienia działania** bloku zawierającego listę plików dziennika.</span><span class="sxs-lookup"><span data-stu-id="d443f-407">When you click hello activity run, you see hello **ACTIVITY RUN DETAILS** blade with a list of log files.</span></span> <span data-ttu-id="d443f-408">Zobaczysz zarejestrowane komunikaty, w pliku user_0.log hello.</span><span class="sxs-lookup"><span data-stu-id="d443f-408">You see logged messages in hello user_0.log file.</span></span> <span data-ttu-id="d443f-409">Po wystąpieniu błędu, zobacz trzech uruchomień działania ponieważ liczby ponownych prób hello ustawiono too3 w potoku hello/aktywność JSON.</span><span class="sxs-lookup"><span data-stu-id="d443f-409">When an error occurs, you see three activity runs because hello retry count is set too3 in hello pipeline/activity JSON.</span></span> <span data-ttu-id="d443f-410">Po kliknięciu przycisku uruchamiania działania hello możesz Zobacz pliki dziennika hello możesz przejrzeć tootroubleshoot hello błędu.</span><span class="sxs-lookup"><span data-stu-id="d443f-410">When you click hello activity run, you see hello log files that you can review tootroubleshoot hello error.</span></span>

   <span data-ttu-id="d443f-411">W hello listę plików dziennika, kliknij przycisk hello **0.log użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="d443f-411">In hello list of log files, click hello **user-0.log**.</span></span> <span data-ttu-id="d443f-412">W prawym panelu hello są wyniki hello przy użyciu hello **IActivityLogger.Write** metody.</span><span class="sxs-lookup"><span data-stu-id="d443f-412">In hello right panel are hello results of using hello **IActivityLogger.Write** method.</span></span> <span data-ttu-id="d443f-413">Jeśli nie widzisz wszystkich wiadomości, sprawdź, czy istnieje więcej plików dziennika o nazwie: user_1.log, user_2.log itp. W przeciwnym razie kod hello mogła zakończyć się niepowodzeniem po hello ostatniego logowania wiadomości.</span><span class="sxs-lookup"><span data-stu-id="d443f-413">If you don't see all messages, check if you have more log files named: user_1.log, user_2.log etc. Otherwise, hello code may have failed after hello last logged message.</span></span>

   <span data-ttu-id="d443f-414">Ponadto sprawdź **0.log systemu** za wszelkie komunikaty o błędach systemu i wyjątki.</span><span class="sxs-lookup"><span data-stu-id="d443f-414">In addition, check **system-0.log** for any system error messages and exceptions.</span></span>
4. <span data-ttu-id="d443f-415">Zawierają hello **PDB** plików w pliku zip hello w celu hello szczegóły błędu mają informacje takie jak **stosu wywołań** po wystąpieniu błędu.</span><span class="sxs-lookup"><span data-stu-id="d443f-415">Include hello **PDB** file in hello zip file so that hello error details have information such as **call stack** when an error occurs.</span></span>
5. <span data-ttu-id="d443f-416">Wszystkie pliki w pliku zip hello Witaj dla działań niestandardowych hello musi znajdować się na powitania **najwyższego poziomu** z nie podfolderach.</span><span class="sxs-lookup"><span data-stu-id="d443f-416">All hello files in hello zip file for hello custom activity must be at hello **top level** with no sub folders.</span></span>
6. <span data-ttu-id="d443f-417">Upewnij się, że hello **assemblyName** (MyDotNetActivity.dll), **punktu wejścia**(MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer / MyDotNetActivity.zip) i **packageLinkedService** (powinna wskazywać toohello **ogólnego przeznaczenia**magazynu obiektów blob platformy Azure, który zawiera plik zip hello) są ustawione wartości toocorrect.</span><span class="sxs-lookup"><span data-stu-id="d443f-417">Ensure that hello **assemblyName** (MyDotNetActivity.dll), **entryPoint**(MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer/MyDotNetActivity.zip), and **packageLinkedService** (should point toohello **general-purpose**Azure blob storage that contains hello zip file) are set toocorrect values.</span></span>
7. <span data-ttu-id="d443f-418">Stałe błędu i chcesz wycinek hello tooreprocess, kliknij prawym przyciskiem myszy hello wycinek hello **OutputDataset** bloku i kliknij przycisk **Uruchom**.</span><span class="sxs-lookup"><span data-stu-id="d443f-418">If you fixed an error and want tooreprocess hello slice, right-click hello slice in hello **OutputDataset** blade and click **Run**.</span></span>
8. <span data-ttu-id="d443f-419">Jeśli zostanie wyświetlony następujący błąd hello, używasz pakietu usługi Azure Storage hello wersji > 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="d443f-419">If you see hello following error, you are using hello Azure Storage package of version > 4.3.0.</span></span> <span data-ttu-id="d443f-420">Uruchamianie usługi fabryka danych wymaga wersji hello 4.3 WindowsAzure.Storage.</span><span class="sxs-lookup"><span data-stu-id="d443f-420">Data Factory service launcher requires hello 4.3 version of WindowsAzure.Storage.</span></span> <span data-ttu-id="d443f-421">Zobacz [izolacji elementu Appdomain](#appdomain-isolation) sekcji Obejście należy używać hello nowszej wersji zestawu Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="d443f-421">See [Appdomain isolation](#appdomain-isolation) section for a work-around if you must use hello later version of Azure Storage assembly.</span></span> 

    ```
    Error in Activity: Unknown error in module: System.Reflection.TargetInvocationException: Exception has been thrown by hello target of an invocation. ---> System.TypeLoadException: Could not load type 'Microsoft.WindowsAzure.Storage.Blob.CloudBlob' from assembly 'Microsoft.WindowsAzure.Storage, Version=4.3.0.0, Culture=neutral, 
    ```

    <span data-ttu-id="d443f-422">Jeśli używasz wersji hello 4.3.0 pakietu usługi Azure Storage, Usuń hello istniejące odwołanie tooAzure magazynu pakietu wersji > 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="d443f-422">If you can use hello 4.3.0 version of Azure Storage package, remove hello existing reference tooAzure Storage package of version > 4.3.0.</span></span> <span data-ttu-id="d443f-423">Następnie uruchom następujące polecenie w konsoli Menedżera pakietów NuGet hello.</span><span class="sxs-lookup"><span data-stu-id="d443f-423">Then, run hello following command from NuGet Package Manager Console.</span></span> 

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    <span data-ttu-id="d443f-424">Tworzenie projektu hello.</span><span class="sxs-lookup"><span data-stu-id="d443f-424">Build hello project.</span></span> <span data-ttu-id="d443f-425">Usuń zespół Azure.Storage wersji > 4.3.0 z folderu bin\Debug hello.</span><span class="sxs-lookup"><span data-stu-id="d443f-425">Delete Azure.Storage assembly of version > 4.3.0 from hello bin\Debug folder.</span></span> <span data-ttu-id="d443f-426">Utwórz plik zip zawierający pliki binarne i pliku PDB hello.</span><span class="sxs-lookup"><span data-stu-id="d443f-426">Create a zip file with binaries and hello PDB file.</span></span> <span data-ttu-id="d443f-427">Stary plik zip hello zamienić na w kontenerze obiektów blob hello (customactivitycontainer).</span><span class="sxs-lookup"><span data-stu-id="d443f-427">Replace hello old zip file with this one in hello blob container (customactivitycontainer).</span></span> <span data-ttu-id="d443f-428">Uruchom ponownie hello wycinków, które zakończyły się niepowodzeniem (kliknij prawym przyciskiem myszy wycinek i kliknij przycisk Uruchom).</span><span class="sxs-lookup"><span data-stu-id="d443f-428">Rerun hello slices that failed (right-click slice, and click Run).</span></span>   
8. <span data-ttu-id="d443f-429">działania niestandardowego Hello nie używa hello **app.config** plików z pakietu.</span><span class="sxs-lookup"><span data-stu-id="d443f-429">hello custom activity does not use hello **app.config** file from your package.</span></span> <span data-ttu-id="d443f-430">W związku z tym jeśli kod odczytuje wszelkie parametry połączenia z pliku konfiguracji hello, działa w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="d443f-430">Therefore, if your code reads any connection strings from hello configuration file, it does not work at runtime.</span></span> <span data-ttu-id="d443f-431">Witaj najlepsze rozwiązanie przy użyciu partii zadań Azure jest toohold żadnych kluczy tajnych w **Azure KeyVault**, użyj hello tooprotect główną usługi na podstawie certyfikatu **keyvault**i dystrybuowanie hello certyfikatu tooAzure puli partii.</span><span class="sxs-lookup"><span data-stu-id="d443f-431">hello best practice when using Azure Batch is toohold any secrets in an **Azure KeyVault**, use a certificate-based service principal tooprotect hello **keyvault**, and distribute hello certificate tooAzure Batch pool.</span></span> <span data-ttu-id="d443f-432">Witaj działania niestandardowego .NET, a następnie mogą uzyskiwać dostęp do kluczy tajnych z hello KeyVault w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="d443f-432">hello .NET custom activity then can access secrets from hello KeyVault at runtime.</span></span> <span data-ttu-id="d443f-433">To rozwiązanie jest ogólnego rozwiązania i mogą być skalowane tooany typu klucza tajnego, nie tylko w parametrach połączenia.</span><span class="sxs-lookup"><span data-stu-id="d443f-433">This solution is a generic solution and can scale tooany type of secret, not just connection string.</span></span>

   <span data-ttu-id="d443f-434">Istnieje obejście łatwiejsze (ale nie najlepiej): można utworzyć **Azure SQL połączona usługa** ustawień parametrów połączenia, tworzenie połączonej usługi i dataset hello łańcucha jako fikcyjny wejściowy zestaw danych tekst hello używa zestawu danych toohello niestandardowego działania .NET.</span><span class="sxs-lookup"><span data-stu-id="d443f-434">There is an easier workaround (but not a best practice): you can create an **Azure SQL linked service** with connection string settings, create a dataset that uses hello linked service, and chain hello dataset as a dummy input dataset toohello custom .NET activity.</span></span> <span data-ttu-id="d443f-435">Mogą być następnie hello dostępu połączone usługi parametry połączenia w hello działania niestandardowego kodu.</span><span class="sxs-lookup"><span data-stu-id="d443f-435">You can then access hello linked service's connection string in hello custom activity code.</span></span>  

## <a name="update-custom-activity"></a><span data-ttu-id="d443f-436">Aktualizowanie działań niestandardowych</span><span class="sxs-lookup"><span data-stu-id="d443f-436">Update custom activity</span></span>
<span data-ttu-id="d443f-437">Po zaktualizowaniu hello kodu dla działań niestandardowych hello skompiluj go i przekazać hello plik zip, który zawiera nowego magazynu obiektów blob toohello plików binarnych.</span><span class="sxs-lookup"><span data-stu-id="d443f-437">If you update hello code for hello custom activity, build it, and upload hello zip file that contains new binaries toohello blob storage.</span></span>

## <a name="appdomain-isolation"></a><span data-ttu-id="d443f-438">Izolacja domeny aplikacji</span><span class="sxs-lookup"><span data-stu-id="d443f-438">Appdomain isolation</span></span>
<span data-ttu-id="d443f-439">Zobacz [Cross próbki AppDomain](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) który pokazuje sposób toocreate działania niestandardowego, który nie jest ograniczone wersji tooassembly używanych przez uruchamianie fabryki danych hello (przykład: WindowsAzure.Storage v4.3.0 Newtonsoft.Json v6.0.x, itp.).</span><span class="sxs-lookup"><span data-stu-id="d443f-439">See [Cross AppDomain Sample](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) that shows you how toocreate a custom activity that is not constrained tooassembly versions used by hello Data Factory launcher (example: WindowsAzure.Storage v4.3.0, Newtonsoft.Json v6.0.x, etc.).</span></span>

## <a name="access-extended-properties"></a><span data-ttu-id="d443f-440">Dostęp do właściwości rozszerzone</span><span class="sxs-lookup"><span data-stu-id="d443f-440">Access extended properties</span></span>
<span data-ttu-id="d443f-441">Właściwości rozszerzone można zadeklarować w działaniu hello JSON, jak pokazano w hello następujące przykładowe:</span><span class="sxs-lookup"><span data-stu-id="d443f-441">You can declare extended properties in hello activity JSON as shown in hello following sample:</span></span>

```JSON
"typeProperties": {
  "AssemblyName": "MyDotNetActivity.dll",
  "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
  "PackageLinkedService": "AzureStorageLinkedService",
  "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
  "extendedProperties": {
    "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))",
    "DataFactoryName": "CustomActivityFactory"
  }
},
```


<span data-ttu-id="d443f-442">W przykładzie hello są dwie właściwości rozszerzone: **SliceStart** i **DataFactoryName**.</span><span class="sxs-lookup"><span data-stu-id="d443f-442">In hello example, there are two extended properties: **SliceStart** and **DataFactoryName**.</span></span> <span data-ttu-id="d443f-443">wartość Hello SliceStart opiera się na powitania SliceStart zmienna.</span><span class="sxs-lookup"><span data-stu-id="d443f-443">hello value for SliceStart is based on hello SliceStart system variable.</span></span> <span data-ttu-id="d443f-444">Zobacz [zmienne systemowe](data-factory-functions-variables.md) listę zmiennych obsługiwany system.</span><span class="sxs-lookup"><span data-stu-id="d443f-444">See [System Variables](data-factory-functions-variables.md) for a list of supported system variables.</span></span> <span data-ttu-id="d443f-445">wartość Hello DataFactoryName jest ustalony tooCustomActivityFactory.</span><span class="sxs-lookup"><span data-stu-id="d443f-445">hello value for DataFactoryName is hard-coded tooCustomActivityFactory.</span></span>

<span data-ttu-id="d443f-446">tooaccess tych właściwości w hello rozszerzone **Execute** metody toohello podobny kod Użyj następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="d443f-446">tooaccess these extended properties in hello **Execute** method, use code similar toohello following code:</span></span>

```csharp
// tooget extended properties (for example: SliceStart)
DotNetActivity dotNetActivity = (DotNetActivity)activity.TypeProperties;
string sliceStartString = dotNetActivity.ExtendedProperties["SliceStart"];

// toolog all extended properties                               
IDictionary<string, string> extendedProperties = dotNetActivity.ExtendedProperties;
logger.Write("Logging extended properties if any...");
foreach (KeyValuePair<string, string> entry in extendedProperties)
{
    logger.Write("<key:{0}> <value:{1}>", entry.Key, entry.Value);
}
```

## <a name="auto-scaling-of-azure-batch"></a><span data-ttu-id="d443f-447">Automatyczne skalowanie partii zadań Azure</span><span class="sxs-lookup"><span data-stu-id="d443f-447">Auto-scaling of Azure Batch</span></span>
<span data-ttu-id="d443f-448">Można również utworzyć puli partii zadań Azure z **skalowania automatycznego** funkcji.</span><span class="sxs-lookup"><span data-stu-id="d443f-448">You can also create an Azure Batch pool with **autoscale** feature.</span></span> <span data-ttu-id="d443f-449">Na przykład można utworzyć puli partii zadań azure 0 dedykowanych maszyn wirtualnych i formuły skalowania automatycznego na podstawie hello liczby oczekujących zadań.</span><span class="sxs-lookup"><span data-stu-id="d443f-449">For example, you could create an azure batch pool with 0 dedicated VMs and an autoscale formula based on hello number of pending tasks.</span></span> 

<span data-ttu-id="d443f-450">tutaj Hello przykładowa formuła osiąga hello następujące zachowanie: podczas tworzenia puli hello, rozpoczyna się od 1 maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d443f-450">hello sample formula here achieves hello following behavior: When hello pool is initially created, it starts with 1 VM.</span></span> <span data-ttu-id="d443f-451">Metryka $PendingTasks definiuje hello liczbę zadań uruchomiona + aktywny (w kolejce) stanu.</span><span class="sxs-lookup"><span data-stu-id="d443f-451">$PendingTasks metric defines hello number of tasks in running + active (queued) state.</span></span>  <span data-ttu-id="d443f-452">Formuła Hello znajduje hello średnią liczbę zadań oczekujących w hello ostatnich 180 sekund i odpowiednio ustawia TargetDedicated.</span><span class="sxs-lookup"><span data-stu-id="d443f-452">hello formula finds hello average number of pending tasks in hello last 180 seconds and sets TargetDedicated accordingly.</span></span> <span data-ttu-id="d443f-453">Gwarantuje, że TargetDedicated nigdy nie wykracza poza 25 maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="d443f-453">It ensures that TargetDedicated never goes beyond 25 VMs.</span></span> <span data-ttu-id="d443f-454">Tak, jak nowe zadania są przesyłane, automatycznie zwiększa rozmiar puli i jako zakończenie zadania, maszyn wirtualnych stają się wolnego jeden po drugim i skalowanie automatyczne hello zmniejsza tych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="d443f-454">So, as new tasks are submitted, pool automatically grows and as tasks complete, VMs become free one by one and hello autoscaling shrinks those VMs.</span></span> <span data-ttu-id="d443f-455">startingNumberOfVMs i maxNumberofVMs mogą być dostosowane tooyour potrzeb.</span><span class="sxs-lookup"><span data-stu-id="d443f-455">startingNumberOfVMs and maxNumberofVMs can be adjusted tooyour needs.</span></span>

<span data-ttu-id="d443f-456">Formuła skalowania automatycznego:</span><span class="sxs-lookup"><span data-stu-id="d443f-456">Autoscale formula:</span></span>

``` 
startingNumberOfVMs = 1;
maxNumberofVMs = 25;
pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
$TargetDedicated=min(maxNumberofVMs,pendingTaskSamples);
```

<span data-ttu-id="d443f-457">Zobacz [automatycznie skali obliczeniowe węzłów w puli partii zadań Azure](../batch/batch-automatic-scaling.md) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="d443f-457">See [Automatically scale compute nodes in an Azure Batch pool](../batch/batch-automatic-scaling.md) for details.</span></span>

<span data-ttu-id="d443f-458">Jeśli puli hello używa domyślnej hello [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), hello usługa partia zadań może zająć 15 do 30 minut tooprepare hello maszyny Wirtualnej przed uruchomieniem hello działania niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="d443f-458">If hello pool is using hello default [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), hello Batch service could take 15-30 minutes tooprepare hello VM before running hello custom activity.</span></span>  <span data-ttu-id="d443f-459">Jeśli pula hello jest przy użyciu różnych autoScaleEvaluationInterval, hello usługa partia zadań może zająć autoScaleEvaluationInterval + 10 minut.</span><span class="sxs-lookup"><span data-stu-id="d443f-459">If hello pool is using a different autoScaleEvaluationInterval, hello Batch service could take autoScaleEvaluationInterval + 10 minutes.</span></span>

## <a name="use-hdinsight-compute-service"></a><span data-ttu-id="d443f-460">Korzystanie z usługi obliczeniowe HDInsight</span><span class="sxs-lookup"><span data-stu-id="d443f-460">Use HDInsight compute service</span></span>
<span data-ttu-id="d443f-461">W przewodniku hello używane są działania niestandardowe hello toorun obliczeniowych partii zadań Azure.</span><span class="sxs-lookup"><span data-stu-id="d443f-461">In hello walkthrough, you used Azure Batch compute toorun hello custom activity.</span></span> <span data-ttu-id="d443f-462">Można również użyć klastra usługi HDInsight opartej na systemie Windows lub ma fabryki danych tworzenia klastra usługi HDInsight opartej na systemie Windows na żądanie i ma uruchamiania w klastrze usługi HDInsight hello działania niestandardowe hello.</span><span class="sxs-lookup"><span data-stu-id="d443f-462">You can also use your own Windows-based HDInsight cluster or have Data Factory create an on-demand Windows-based HDInsight cluster and have hello custom activity run on hello HDInsight cluster.</span></span> <span data-ttu-id="d443f-463">Poniżej przedstawiono ogólne kroki hello przy użyciu klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d443f-463">Here are hello high-level steps for using an HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d443f-464">Niestandardowe działania .NET Hello uruchomić tylko w klastrach HDInsight opartych na systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="d443f-464">hello custom .NET activities run only on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="d443f-465">Obejście tego ograniczenia jest toouse hello działania zmniejszyć mapy toorun Java kodu niestandardowego w klastrze usługi HDInsight opartej na systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="d443f-465">A workaround for this limitation is toouse hello Map Reduce Activity toorun custom Java code on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="d443f-466">Innym rozwiązaniem jest toouse puli partii zadań Azure VMs toorun niestandardowych działań zamiast klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d443f-466">Another option is toouse an Azure Batch pool of VMs toorun custom activities instead of using a HDInsight cluster.</span></span>
 

1. <span data-ttu-id="d443f-467">Tworzenie usługi Azure HDInsight połączone.</span><span class="sxs-lookup"><span data-stu-id="d443f-467">Create an Azure HDInsight linked service.</span></span>   
2. <span data-ttu-id="d443f-468">HDInsight Użyj połączonej usługi zamiast **AzureBatchLinkedService** hello w potoku JSON.</span><span class="sxs-lookup"><span data-stu-id="d443f-468">Use HDInsight linked service in place of **AzureBatchLinkedService** in hello pipeline JSON.</span></span>

<span data-ttu-id="d443f-469">Jeśli chcesz, aby tootest go z przewodnikiem hello, zmień **start** i **zakończenia** razy dla potoku hello tak, aby można było testować hello scenariusz hello usługi Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d443f-469">If you want tootest it with hello walkthrough, change **start** and **end** times for hello pipeline so that you can test hello scenario with hello Azure HDInsight service.</span></span>

#### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="d443f-470">Tworzenie połączonej usługi Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="d443f-470">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="d443f-471">Hello usługi fabryka danych Azure obsługuje tworzenie klastra na żądanie i korzystać z niego dane wyjściowe tooprocess tooproduce wejściowego.</span><span class="sxs-lookup"><span data-stu-id="d443f-471">hello Azure Data Factory service supports creation of an on-demand cluster and use it tooprocess input tooproduce output data.</span></span> <span data-ttu-id="d443f-472">Można również użyć własnego klastra tooperform hello takie same.</span><span class="sxs-lookup"><span data-stu-id="d443f-472">You can also use your own cluster tooperform hello same.</span></span> <span data-ttu-id="d443f-473">Korzystając z klastrem usługi HDInsight na żądanie, klaster pobiera utworzone dla każdego wycinka.</span><span class="sxs-lookup"><span data-stu-id="d443f-473">When you use on-demand HDInsight cluster, a cluster gets created for each slice.</span></span> <span data-ttu-id="d443f-474">Korzystając z klastrem usługi HDInsight, klaster hello jest gotowy tooprocess natychmiast hello wycinka.</span><span class="sxs-lookup"><span data-stu-id="d443f-474">Whereas, if you use your own HDInsight cluster, hello cluster is ready tooprocess hello slice immediately.</span></span> <span data-ttu-id="d443f-475">W związku z tym korzystając z klastra na żądanie, nie widać danych wyjściowych hello tak szybko, jak kiedy używać własnego klastra.</span><span class="sxs-lookup"><span data-stu-id="d443f-475">Therefore, when you use on-demand cluster, you may not see hello output data as quickly as when you use your own cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="d443f-476">W czasie wykonywania wystąpienia działania .NET działa tylko na jednym węźle procesu roboczego w klastrze HDInsight hello; nie może być skalowana toorun na wielu węzłach.</span><span class="sxs-lookup"><span data-stu-id="d443f-476">At runtime, an instance of a .NET activity runs only on one worker node in hello HDInsight cluster; it cannot be scaled toorun on multiple nodes.</span></span> <span data-ttu-id="d443f-477">Wiele wystąpień programu .NET działania można uruchomić równolegle w różnych węzłach klastra usługi HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="d443f-477">Multiple instances of .NET activity can run in parallel on different nodes of hello HDInsight cluster.</span></span>
>
>

##### <a name="toouse-an-on-demand-hdinsight-cluster"></a><span data-ttu-id="d443f-478">toouse klaster usługi HDInsight na żądanie</span><span class="sxs-lookup"><span data-stu-id="d443f-478">toouse an on-demand HDInsight cluster</span></span>
1. <span data-ttu-id="d443f-479">W hello **portalu Azure**, kliknij przycisk **Utwórz i wdróż** stronie głównej hello fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="d443f-479">In hello **Azure portal**, click **Author and Deploy** in hello Data Factory home page.</span></span>
2. <span data-ttu-id="d443f-480">W hello Edytor fabryki danych, kliknij przycisk **nowych obliczeń** polecenia hello paska i wybierz pozycję **klastra usługi HDInsight na żądanie** hello menu.</span><span class="sxs-lookup"><span data-stu-id="d443f-480">In hello Data Factory Editor, click **New compute** from hello command bar and select **On-demand HDInsight cluster** from hello menu.</span></span>
3. <span data-ttu-id="d443f-481">Wprowadź hello następującego skryptu JSON toohello zmiany:</span><span class="sxs-lookup"><span data-stu-id="d443f-481">Make hello following changes toohello JSON script:</span></span>

   1. <span data-ttu-id="d443f-482">Dla hello **wartość clusterSize** właściwości, określ rozmiar hello hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d443f-482">For hello **clusterSize** property, specify hello size of hello HDInsight cluster.</span></span>
   2. <span data-ttu-id="d443f-483">Dla hello **timeToLive** właściwości, określ, jak długo powitania klienta może być bezczynne, zanim ich usunięcia.</span><span class="sxs-lookup"><span data-stu-id="d443f-483">For hello **timeToLive** property, specify how long hello customer can be idle before it is deleted.</span></span>
   3. <span data-ttu-id="d443f-484">Dla hello **wersji** właściwości, określ wersję HDInsight hello ma toouse.</span><span class="sxs-lookup"><span data-stu-id="d443f-484">For hello **version** property, specify hello HDInsight version you want toouse.</span></span> <span data-ttu-id="d443f-485">Jeśli należy wykluczyć tę właściwość, najnowsza wersja hello jest używany.</span><span class="sxs-lookup"><span data-stu-id="d443f-485">If you exclude this property, hello latest version is used.</span></span>  
   4. <span data-ttu-id="d443f-486">Dla hello **linkedServiceName**, określ **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="d443f-486">For hello **linkedServiceName**, specify **AzureStorageLinkedService**.</span></span>

        ```JSON
        {
           "name": "HDInsightOnDemandLinkedService",
           "properties": {
               "type": "HDInsightOnDemand",
               "typeProperties": {
                   "clusterSize": 4,
                   "timeToLive": "00:05:00",
                   "osType": "Windows",
                   "linkedServiceName": "AzureStorageLinkedService",
               }
           }
        }
        ```

    > [!IMPORTANT]
    > <span data-ttu-id="d443f-487">Niestandardowe działania .NET Hello uruchomić tylko w klastrach HDInsight opartych na systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="d443f-487">hello custom .NET activities run only on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="d443f-488">Obejście tego ograniczenia jest toouse hello działania zmniejszyć mapy toorun Java kodu niestandardowego w klastrze usługi HDInsight opartej na systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="d443f-488">A workaround for this limitation is toouse hello Map Reduce Activity toorun custom Java code on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="d443f-489">Innym rozwiązaniem jest toouse puli partii zadań Azure VMs toorun niestandardowych działań zamiast klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d443f-489">Another option is toouse an Azure Batch pool of VMs toorun custom activities instead of using a HDInsight cluster.</span></span>

4. <span data-ttu-id="d443f-490">Kliknij przycisk **Wdróż** na pasku toodeploy hello połączone usługi poleceń hello.</span><span class="sxs-lookup"><span data-stu-id="d443f-490">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

##### <a name="toouse-your-own-hdinsight-cluster"></a><span data-ttu-id="d443f-491">toouse klastrem usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="d443f-491">toouse your own HDInsight cluster:</span></span>
1. <span data-ttu-id="d443f-492">W hello **portalu Azure**, kliknij przycisk **Utwórz i wdróż** stronie głównej hello fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="d443f-492">In hello **Azure portal**, click **Author and Deploy** in hello Data Factory home page.</span></span>
2. <span data-ttu-id="d443f-493">W hello **Edytor fabryki danych**, kliknij przycisk **nowych obliczeń** polecenia hello paska i wybierz pozycję **klastra usługi HDInsight** hello menu.</span><span class="sxs-lookup"><span data-stu-id="d443f-493">In hello **Data Factory Editor**, click **New compute** from hello command bar and select **HDInsight cluster** from hello menu.</span></span>
3. <span data-ttu-id="d443f-494">Wprowadź hello następującego skryptu JSON toohello zmiany:</span><span class="sxs-lookup"><span data-stu-id="d443f-494">Make hello following changes toohello JSON script:</span></span>

   1. <span data-ttu-id="d443f-495">Dla hello **clusterUri** właściwości, wprowadź adres URL powitania dla Twojej usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d443f-495">For hello **clusterUri** property, enter hello URL for your HDInsight.</span></span> <span data-ttu-id="d443f-496">Na przykład: https://<clustername>.azurehdinsight.net/</span><span class="sxs-lookup"><span data-stu-id="d443f-496">For example: https://<clustername>.azurehdinsight.net/</span></span>     
   2. <span data-ttu-id="d443f-497">Dla hello **UserName** właściwości, wprowadź nazwę użytkownika hello mającego klastra usługi HDInsight toohello dostępu.</span><span class="sxs-lookup"><span data-stu-id="d443f-497">For hello **UserName** property, enter hello user name who has access toohello HDInsight cluster.</span></span>
   3. <span data-ttu-id="d443f-498">Dla hello **hasło** właściwości, wprowadź hasło hello hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d443f-498">For hello **Password** property, enter hello password for hello user.</span></span>
   4. <span data-ttu-id="d443f-499">Dla hello **LinkedServiceName** właściwości, wprowadź **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="d443f-499">For hello **LinkedServiceName** property, enter **AzureStorageLinkedService**.</span></span>
4. <span data-ttu-id="d443f-500">Kliknij przycisk **Wdróż** na pasku toodeploy hello połączone usługi poleceń hello.</span><span class="sxs-lookup"><span data-stu-id="d443f-500">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

<span data-ttu-id="d443f-501">Zobacz [obliczeniowe połączonych usług](data-factory-compute-linked-services.md) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="d443f-501">See [Compute linked services](data-factory-compute-linked-services.md) for details.</span></span>

<span data-ttu-id="d443f-502">W hello **potoku JSON**, używanie usługi HDInsight (na żądanie lub własne) połączonej usługi:</span><span class="sxs-lookup"><span data-stu-id="d443f-502">In hello **pipeline JSON**, use HDInsight (on-demand or your own) linked service:</span></span>

```JSON
{
  "name": "ADFTutorialPipelineCustom",
  "properties": {
    "description": "Use custom activity",
    "activities": [
      {
        "Name": "MyDotNetActivity",
        "Type": "DotNetActivity",
        "Inputs": [
          {
            "Name": "InputDataset"
          }
        ],
        "Outputs": [
          {
            "Name": "OutputDataset"
          }
        ],
        "LinkedServiceName": "HDInsightOnDemandLinkedService",
        "typeProperties": {
          "AssemblyName": "MyDotNetActivity.dll",
          "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
          "PackageLinkedService": "AzureStorageLinkedService",
          "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
          "extendedProperties": {
            "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
          }
        },
        "Policy": {
          "Concurrency": 2,
          "ExecutionPriorityOrder": "OldestFirst",
          "Retry": 3,
          "Timeout": "00:30:00",
          "Delay": "00:00:00"
        }
      }
    ],
    "start": "2016-11-16T00:00:00Z",
    "end": "2016-11-16T05:00:00Z",
    "isPaused": false
  }
}
```

## <a name="create-a-custom-activity-by-using-net-sdk"></a><span data-ttu-id="d443f-503">Tworzenie niestandardowego działania przy użyciu zestawu .NET SDK</span><span class="sxs-lookup"><span data-stu-id="d443f-503">Create a custom activity by using .NET SDK</span></span>
<span data-ttu-id="d443f-504">W przewodniku hello w tym artykule Tworzenie fabryki danych z potok, który używa niestandardowego działania hello hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d443f-504">In hello walkthrough in this article, you create a data factory with a pipeline that uses hello custom activity by using hello Azure portal.</span></span> <span data-ttu-id="d443f-505">Witaj następującego kodu pokazuje, jak toocreate hello fabryki danych przy użyciu zestawu .NET SDK zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="d443f-505">hello following code shows you how toocreate hello data factory by using .NET SDK instead.</span></span> <span data-ttu-id="d443f-506">Można znaleźć więcej informacji o korzystaniu z zestawu SDK tooprogrammatically tworzenie potoków w hello [utworzyć potok z działania kopiowania przy użyciu interfejsu API platformy .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d443f-506">You can find more details about using SDK tooprogrammatically create pipelines in hello [create a pipeline with copy activity by using .NET API](data-factory-copy-activity-tutorial-using-dotnet-api.md) article.</span></span> 

```csharp
using System;
using System.Configuration;
using System.Collections.ObjectModel;
using System.Threading;
using System.Threading.Tasks;

using Microsoft.Azure;
using Microsoft.Azure.Management.DataFactories;
using Microsoft.Azure.Management.DataFactories.Models;
using Microsoft.Azure.Management.DataFactories.Common.Models;

using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System.Collections.Generic;

namespace DataFactoryAPITestApp
{
    class Program
    {
        static void Main(string[] args)
        {
            // create data factory management client

            // TODO: replace ADFTutorialResourceGroup with hello name of your resource group.
            string resourceGroupName = "ADFTutorialResourceGroup";

            // TODO: replace APITutorialFactory with a name that is globally unique. For example: APITutorialFactory04212017
            string dataFactoryName = "APITutorialFactory";

            TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
                ConfigurationManager.AppSettings["SubscriptionId"],
                GetAuthorizationHeader().Result);

            Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

            DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);

            Console.WriteLine("Creating a data factory");
            client.DataFactories.CreateOrUpdate(resourceGroupName,
                new DataFactoryCreateOrUpdateParameters()
                {
                    DataFactory = new DataFactory()
                    {
                        Name = dataFactoryName,
                        Location = "westus",
                        Properties = new DataFactoryProperties()
                    }
                }
            );

            // create a linked service for input data store: Azure Storage
            Console.WriteLine("Creating Azure Storage linked service");
            client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new LinkedServiceCreateOrUpdateParameters()
                {
                    LinkedService = new LinkedService()
                    {
                        Name = "AzureStorageLinkedService",
                        Properties = new LinkedServiceProperties
                        (
                            // TODO: Replace <accountname> and <accountkey> with name and key of your Azure Storage account.
                            new AzureStorageLinkedService("DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>")
                        )
                    }
                }
            );

            // create a linked service for output data store: Azure SQL Database
            Console.WriteLine("Creating Azure Batch linked service");
            client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new LinkedServiceCreateOrUpdateParameters()
                {
                    LinkedService = new LinkedService()
                    {
                        Name = "AzureBatchLinkedService",
                        Properties = new LinkedServiceProperties
                        (
                            // TODO: replace <batchaccountname> and <yourbatchaccountkey> with name and key of your Azure Batch account
                            new AzureBatchLinkedService("<batchaccountname>", "https://westus.batch.azure.com", "<yourbatchaccountkey>", "myazurebatchpool", "AzureStorageLinkedService")
                        )
                    }
                }
            );

            // create input and output datasets
            Console.WriteLine("Creating input and output datasets");
            string Dataset_Source = "InputDataset";
            string Dataset_Destination = "OutputDataset";

            Console.WriteLine("Creating input dataset of type: Azure Blob");
            client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,

                new DatasetCreateOrUpdateParameters()
                {
                    Dataset = new Dataset()
                    {
                        Name = Dataset_Source,
                        Properties = new DatasetProperties()
                        {
                            LinkedServiceName = "AzureStorageLinkedService",
                            TypeProperties = new AzureBlobDataset()
                            {
                                FolderPath = "adftutorial/customactivityinput/",
                                Format = new TextFormat()
                            },
                            External = true,
                            Availability = new Availability()
                            {
                                Frequency = SchedulePeriod.Hour,
                                Interval = 1,
                            },

                            Policy = new Policy() { }
                        }
                    }
                });

            Console.WriteLine("Creating output dataset of type: Azure Blob");
            client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new DatasetCreateOrUpdateParameters()
                {
                    Dataset = new Dataset()
                    {
                        Name = Dataset_Destination,
                        Properties = new DatasetProperties()
                        {
                            LinkedServiceName = "AzureStorageLinkedService",
                            TypeProperties = new AzureBlobDataset()
                            {
                                FileName = "{slice}.txt",
                                FolderPath = "adftutorial/customactivityoutput/",
                                PartitionedBy = new List<Partition>()
                                {
                                    new Partition()
                                    {
                                        Name = "slice",
                                        Value = new DateTimePartitionValue()
                                        {
                                            Date = "SliceStart",
                                            Format = "yyyy-MM-dd-HH"
                                        }
                                    }
                                }
                            },
                            Availability = new Availability()
                            {
                                Frequency = SchedulePeriod.Hour,
                                Interval = 1,
                            },
                        }
                    }
                });

            Console.WriteLine("Creating a custom activity pipeline");
            DateTime PipelineActivePeriodStartTime = new DateTime(2017, 3, 9, 0, 0, 0, 0, DateTimeKind.Utc);
            DateTime PipelineActivePeriodEndTime = PipelineActivePeriodStartTime.AddMinutes(60);
            string PipelineName = "ADFTutorialPipelineCustom";

            client.Pipelines.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new PipelineCreateOrUpdateParameters()
                {
                    Pipeline = new Pipeline()
                    {
                        Name = PipelineName,
                        Properties = new PipelineProperties()
                        {
                            Description = "Use custom activity",

                            // Initial value for pipeline's active period. With this, you won't need tooset slice status
                            Start = PipelineActivePeriodStartTime,
                            End = PipelineActivePeriodEndTime,
                            IsPaused = false,

                            Activities = new List<Activity>()
                            {
                                new Activity()
                                {
                                    Name = "MyDotNetActivity",
                                    Inputs = new List<ActivityInput>()
                                    {
                                        new ActivityInput() {
                                            Name = Dataset_Source
                                        }
                                    },
                                    Outputs = new List<ActivityOutput>()
                                    {
                                        new ActivityOutput()
                                        {
                                            Name = Dataset_Destination
                                        }
                                    },
                                    LinkedServiceName = "AzureBatchLinkedService",
                                    TypeProperties = new DotNetActivity()
                                    {
                                        AssemblyName = "MyDotNetActivity.dll",
                                        EntryPoint = "MyDotNetActivityNS.MyDotNetActivity",
                                        PackageLinkedService = "AzureStorageLinkedService",
                                        PackageFile = "customactivitycontainer/MyDotNetActivity.zip",
                                        ExtendedProperties = new Dictionary<string, string>()
                                        {
                                            { "SliceStart", "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"}
                                        }
                                    },
                                    Policy = new ActivityPolicy()
                                    {
                                        Concurrency = 2,
                                        ExecutionPriorityOrder = "OldestFirst",
                                        Retry = 3,
                                        Timeout = new TimeSpan(0,0,30,0),
                                        Delay = new TimeSpan()
                                    }
                                }
                            }
                        }
                    }
                });
        }

        public static async Task<string> GetAuthorizationHeader()
        {
            AuthenticationContext context = new AuthenticationContext(ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] + ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
            ClientCredential credential = new ClientCredential(
                ConfigurationManager.AppSettings["ApplicationId"],
                ConfigurationManager.AppSettings["Password"]);
            AuthenticationResult result = await context.AcquireTokenAsync(
                resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
                clientCredential: credential);

            if (result != null)
                return result.AccessToken;

            throw new InvalidOperationException("Failed tooacquire token");
        }
    }
}
```

## <a name="debug-custom-activity-in-visual-studio"></a><span data-ttu-id="d443f-507">Debugowanie działań niestandardowych w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d443f-507">Debug custom activity in Visual Studio</span></span>
<span data-ttu-id="d443f-508">Witaj [fabryki danych Azure - lokalnego środowiska](https://github.com/gbrueckl/Azure.DataFactory.LocalEnvironment) przykładem w witrynie GitHub zawiera narzędzie umożliwiający toodebug niestandardowych działań platformy .NET w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d443f-508">hello [Azure Data Factory - local environment](https://github.com/gbrueckl/Azure.DataFactory.LocalEnvironment) sample on GitHub includes a tool that allows you toodebug custom .NET activities within Visual Studio.</span></span>  


## <a name="sample-custom-activities-on-github"></a><span data-ttu-id="d443f-509">Przykład niestandardowych działań w witrynie GitHub</span><span class="sxs-lookup"><span data-stu-id="d443f-509">Sample custom activities on GitHub</span></span>
| <span data-ttu-id="d443f-510">Przykład</span><span class="sxs-lookup"><span data-stu-id="d443f-510">Sample</span></span> | <span data-ttu-id="d443f-511">Jakie niestandardowe działanie robi</span><span class="sxs-lookup"><span data-stu-id="d443f-511">What custom activity does</span></span> |
| --- | --- |
| <span data-ttu-id="d443f-512">[Narzędzie do pobierania danych HTTP](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample).</span><span class="sxs-lookup"><span data-stu-id="d443f-512">[HTTP Data Downloader](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample).</span></span> |<span data-ttu-id="d443f-513">Pobiera dane z tooAzure punkt końcowy HTTP magazynu obiektów Blob przy użyciu działań niestandardowych C# w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="d443f-513">Downloads data from an HTTP Endpoint tooAzure Blob Storage using custom C# Activity in Data Factory.</span></span> |
| [<span data-ttu-id="d443f-514">Przykładowe wskaźniki nastrojów klientów analizy w usłudze Twitter</span><span class="sxs-lookup"><span data-stu-id="d443f-514">Twitter Sentiment Analysis sample</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TwitterAnalysisSample-CustomC%23Activity) |<span data-ttu-id="d443f-515">Wywołuje model usługi uczenie Maszynowe Azure i analizy wskaźniki nastrojów klientów oceniania, prognozowania itp.</span><span class="sxs-lookup"><span data-stu-id="d443f-515">Invokes an Azure ML model and do sentiment analysis, scoring, prediction etc.</span></span> |
| <span data-ttu-id="d443f-516">[Uruchom skrypt języka R](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample).</span><span class="sxs-lookup"><span data-stu-id="d443f-516">[Run R Script](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample).</span></span> |<span data-ttu-id="d443f-517">Wywołuje skrypt języka R, uruchamiając RScript.exe w klastrze usługi HDInsight, na którym jest już zainstalowany R na nim.</span><span class="sxs-lookup"><span data-stu-id="d443f-517">Invokes R script by running RScript.exe on your HDInsight cluster that already has R Installed on it.</span></span> |
| [<span data-ttu-id="d443f-518">Krzyżowe AppDomain .NET działania</span><span class="sxs-lookup"><span data-stu-id="d443f-518">Cross AppDomain .NET Activity</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) |<span data-ttu-id="d443f-519">Używa innego zestawu wersji z takich, które jest używane przez hello uruchamiania usługi fabryka danych</span><span class="sxs-lookup"><span data-stu-id="d443f-519">Uses different assembly versions from ones used by hello Data Factory launcher</span></span> |
| [<span data-ttu-id="d443f-520">Ponowne przetworzenie modelu w usług Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="d443f-520">Reprocess a model in Azure Analysis Services</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/AzureAnalysisServicesProcessSample) |  <span data-ttu-id="d443f-521">Ponownego przetwarzania modelu w usług Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="d443f-521">Reprocesses a model in Azure Analysis Services.</span></span> |

[batch-net-library]: ../batch/batch-dotnet-get-started.md
[batch-create-account]: ../batch/batch-account-create-portal.md
[batch-technical-overview]: ../batch/batch-technical-overview.md
[batch-get-started]: ../batch/batch-dotnet-get-started.md
[use-custom-activities]: data-factory-use-custom-activities.md
[troubleshoot]: data-factory-troubleshoot.md
[data-factory-introduction]: data-factory-introduction.md
[azure-powershell-install]: https://github.com/Azure/azure-sdk-tools/releases


[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456

[new-azure-batch-account]: https://msdn.microsoft.com/library/mt125880.aspx
[new-azure-batch-pool]: https://msdn.microsoft.com/library/mt125936.aspx
[azure-batch-blog]: http://blogs.technet.com/b/windowshpc/archive/2014/10/28/using-azure-powershell-to-manage-azure-batch-account.aspx

[nuget-package]: http://go.microsoft.com/fwlink/?LinkId=517478
[adf-developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[azure-preview-portal]: https://portal.azure.com/

[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[hivewalkthrough]: data-factory-data-transformation-activities.md

[image-data-factory-ouput-from-custom-activity]: ./media/data-factory-use-custom-activities/OutputFilesFromCustomActivity.png

[image-data-factory-download-logs-from-custom-activity]: ./media/data-factory-use-custom-activities/DownloadLogsFromCustomActivity.png
