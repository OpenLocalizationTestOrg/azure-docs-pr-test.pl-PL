---
title: "za pomocą akcji skryptu - Azure klastrów usługi HDInsight aaaCustomize | Dokumentacja firmy Microsoft"
description: "Dodawanie niestandardowych składników, które klastrów usługi HDInsight opartej na tooLinux za pomocą akcji skryptu. Akcje skryptu to skrypty Bash, które można konfiguracji klastra hello toocustomize używane lub dodać dodatkowych usług i narzędzi, takich jak Hue, Solr lub R."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 48e85f53-87c1-474f-b767-ca772238cc13
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: ff22680a8a50b21985f6941f1edaf1dcf863d13f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="customize-linux-based-hdinsight-clusters-using-script-action"></a><span data-ttu-id="e4333-104">Dostosowywanie klastrów usługi HDInsight opartej na systemie Linux przy użyciu akcji skryptu</span><span class="sxs-lookup"><span data-stu-id="e4333-104">Customize Linux-based HDInsight clusters using Script Action</span></span>

<span data-ttu-id="e4333-105">HDInsight zapewnia opcję konfiguracji o nazwie **akcji skryptu** który wywołuje niestandardowe skrypty umożliwiające dostosowanie hello klastra.</span><span class="sxs-lookup"><span data-stu-id="e4333-105">HDInsight provides a configuration option called **Script Action** that invokes custom scripts that customize hello cluster.</span></span> <span data-ttu-id="e4333-106">Skrypty te są używane tooinstall dodatkowe składniki i zmienić ustawienia konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="e4333-106">These scripts are used tooinstall additional components and change configuration settings.</span></span> <span data-ttu-id="e4333-107">Akcje skryptu można podczas lub po utworzeniu klastra.</span><span class="sxs-lookup"><span data-stu-id="e4333-107">Script actions can be used during or after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e4333-108">Akcje skryptu toouse możliwości Hello w klastrze już uruchomiona jest dostępna tylko dla klastrów usługi HDInsight opartych na systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="e4333-108">hello ability toouse script actions on an already running cluster is only available for Linux-based HDInsight clusters.</span></span>
>
> <span data-ttu-id="e4333-109">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="e4333-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="e4333-110">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="e4333-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="e4333-111">Akcje skryptu można także toohello opublikowane w portalu Azure Marketplace jako aplikacji usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e4333-111">Script actions can also be published toohello Azure Marketplace as an HDInsight application.</span></span> <span data-ttu-id="e4333-112">Niektóre przykłady hello w tym dokumencie widoczne sposobem instalowania aplikacji usługi HDInsight przy użyciu polecenia akcji skryptu środowiska PowerShell i hello zestawu .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="e4333-112">Some of hello examples in this document show how you can install an HDInsight application using script action commands from PowerShell and hello .NET SDK.</span></span> <span data-ttu-id="e4333-113">Aby uzyskać więcej informacji na temat aplikacji w usłudze HDInsight, zobacz [publikować aplikacje usługi HDInsight w portalu Azure Marketplace hello](hdinsight-apps-publish-applications.md).</span><span class="sxs-lookup"><span data-stu-id="e4333-113">For more information on HDInsight applications, see [Publish HDInsight applications into hello Azure Marketplace](hdinsight-apps-publish-applications.md).</span></span>

## <a name="permissions"></a><span data-ttu-id="e4333-114">Uprawnienia</span><span class="sxs-lookup"><span data-stu-id="e4333-114">Permissions</span></span>

<span data-ttu-id="e4333-115">Jeśli korzystasz z klastra usługi HDInsight przyłączonych do domeny, istnieją dwa uprawnienia Ambari, które są wymagane w przypadku klastra hello za pomocą akcji skryptu:</span><span class="sxs-lookup"><span data-stu-id="e4333-115">If you are using a domain-joined HDInsight cluster, there are two Ambari permissions that are required when using script actions with hello cluster:</span></span>

* <span data-ttu-id="e4333-116">**NARZĘDZIA AMBARI. Uruchom\_niestandardowy\_polecenia**: rola administratora Ambari hello domyślnie ma to uprawnienie.</span><span class="sxs-lookup"><span data-stu-id="e4333-116">**AMBARI.RUN\_CUSTOM\_COMMAND**: hello Ambari Administrator role has this permission by default.</span></span>
* <span data-ttu-id="e4333-117">**KLASTER. Uruchom\_niestandardowy\_polecenia**: zarówno hello administratora klastra usługi HDInsight i administratora Ambari to uprawnienie mają domyślnie.</span><span class="sxs-lookup"><span data-stu-id="e4333-117">**CLUSTER.RUN\_CUSTOM\_COMMAND**: Both hello HDInsight Cluster Administrator and Ambari Administrator have this permission by default.</span></span>

<span data-ttu-id="e4333-118">Aby uzyskać więcej informacji na temat pracy z uprawnieniami przyłączonych do domeny usługi HDInsight, zobacz [zarządzania klastrami HDInsight przyłączonych do domeny](hdinsight-domain-joined-manage.md).</span><span class="sxs-lookup"><span data-stu-id="e4333-118">For more information on working with permissions with domain-joined HDInsight, see [Manage domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md).</span></span>

## <a name="access-control"></a><span data-ttu-id="e4333-119">Kontrola dostępu</span><span class="sxs-lookup"><span data-stu-id="e4333-119">Access control</span></span>

<span data-ttu-id="e4333-120">Jeśli nie jesteś administratorem hello/właścicieli subskrypcji platformy Azure, jego konto musi mieć co najmniej **współautora** grupę zasobów toohello dostępu, która zawiera hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e4333-120">If you are not hello administrator/owner of your Azure subscription, your account must have at least **Contributor** access toohello resource group that contains hello HDInsight cluster.</span></span>

<span data-ttu-id="e4333-121">Ponadto podczas tworzenia klastra usługi HDInsight, ktoś z co najmniej **współautora** toohello dostępu do subskrypcji platformy Azure musi zostały wcześniej zarejestrowane hello dostawcy dla usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e4333-121">Additionally, if you are creating an HDInsight cluster, someone with at least **Contributor** access toohello Azure subscription must have previously registered hello provider for HDInsight.</span></span> <span data-ttu-id="e4333-122">Rejestracja dostawcy odbywa się po utworzeniu przez użytkownika z subskrypcją toohello dostępu współautora zasobu na powitania po raz pierwszy na powitania subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="e4333-122">Provider registration happens when a user with Contributor access toohello subscription creates a resource for hello first time on hello subscription.</span></span> <span data-ttu-id="e4333-123">Można to osiągnąć również bez tworzenia zasobu, [rejestrując dostawcę za pomocą interfejsu REST](https://msdn.microsoft.com/library/azure/dn790548.aspx).</span><span class="sxs-lookup"><span data-stu-id="e4333-123">It can also be accomplished without creating a resource by [registering a provider using REST](https://msdn.microsoft.com/library/azure/dn790548.aspx).</span></span>

<span data-ttu-id="e4333-124">Aby uzyskać więcej informacji na temat pracy z zarządzania dostępem Zobacz hello w następujących dokumentach:</span><span class="sxs-lookup"><span data-stu-id="e4333-124">For more information on working with access management, see hello following documents:</span></span>

* [<span data-ttu-id="e4333-125">Wprowadzenie do zarządzania dostępem w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="e4333-125">Get started with access management in hello Azure portal</span></span>](../active-directory/role-based-access-control-what-is.md)
* [<span data-ttu-id="e4333-126">Użyj roli przypisania toomanage dostępu tooyour subskrypcji platformy Azure zasobów</span><span class="sxs-lookup"><span data-stu-id="e4333-126">Use role assignments toomanage access tooyour Azure subscription resources</span></span>](../active-directory/role-based-access-control-configure.md)

## <a name="understanding-script-actions"></a><span data-ttu-id="e4333-127">Opis akcji skryptu</span><span class="sxs-lookup"><span data-stu-id="e4333-127">Understanding Script Actions</span></span>

<span data-ttu-id="e4333-128">Akcja skryptu jest po prostu Podaj identyfikator URI do skryptu Bash i parametry.</span><span class="sxs-lookup"><span data-stu-id="e4333-128">A Script Action is simply a Bash script that you provide a URI to, and parameters for.</span></span> <span data-ttu-id="e4333-129">Witaj skrypt jest uruchamiany na węzłach w klastrze usługi HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="e4333-129">hello script runs on nodes in hello HDInsight cluster.</span></span> <span data-ttu-id="e4333-130">Witaj poniżej przedstawiono cechy i funkcje akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="e4333-130">hello following are characteristics and features of script actions.</span></span>

* <span data-ttu-id="e4333-131">Muszą być przechowywane na identyfikator URI, który jest dostępny z klastra usługi HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="e4333-131">Must be stored on a URI that is accessible from hello HDInsight cluster.</span></span> <span data-ttu-id="e4333-132">Lokalizacje magazynu możliwe są następujące Hello:</span><span class="sxs-lookup"><span data-stu-id="e4333-132">hello following are possible storage locations:</span></span>

    * <span data-ttu-id="e4333-133">**Azure Data Lake Store** konta, który jest dostępny dla klastra usługi HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="e4333-133">An **Azure Data Lake Store** account that is accessible by hello HDInsight cluster.</span></span> <span data-ttu-id="e4333-134">Aby uzyskać informacje na temat używania usługi Azure Data Lake Store z usługą HDInsight, zobacz [tworzenia klastra usługi HDInsight z usługą Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e4333-134">For information on using Azure Data Lake Store with HDInsight, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

        <span data-ttu-id="e4333-135">Podczas używania skryptu przechowywane w usłudze Data Lake Store, format identyfikatora URI hello jest `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`.</span><span class="sxs-lookup"><span data-stu-id="e4333-135">When using a script stored in Data Lake Store, hello URI format is `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`.</span></span>

        > [!NOTE]
        > <span data-ttu-id="e4333-136">Hello usługi głównej HDInsight używa tooaccess Data Lake — Magazyn musi mieć dostęp do odczytu toohello skryptu.</span><span class="sxs-lookup"><span data-stu-id="e4333-136">hello service principal HDInsight uses tooaccess Data Lake Store must have read access toohello script.</span></span>

    * <span data-ttu-id="e4333-137">Obiekt blob w **konta magazynu Azure** to albo hello konto podstawowego lub dodatkowego magazynu dla klastra usługi HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="e4333-137">A blob in an **Azure Storage account** that is either hello primary or additional storage account for hello HDInsight cluster.</span></span> <span data-ttu-id="e4333-138">HDInsight udzielono dostępu tooboth tego typu konta magazynu podczas tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="e4333-138">HDInsight is granted access tooboth of these types of storage accounts during cluster creation.</span></span>

    * <span data-ttu-id="e4333-139">Plik publicznego udostępniania usługi takie jak obiektów Blob platformy Azure, GitHub, usługi OneDrive, Dropbox itp.</span><span class="sxs-lookup"><span data-stu-id="e4333-139">A public file sharing service such as Azure Blob, GitHub, OneDrive, Dropbox, etc.</span></span>

        <span data-ttu-id="e4333-140">Na przykład identyfikatory URI, zobacz hello [przykładowe skrypty akcji skryptu](#example-script-action-scripts) sekcji.</span><span class="sxs-lookup"><span data-stu-id="e4333-140">For example URIs, see hello [Example script action scripts](#example-script-action-scripts) section.</span></span>

        > [!WARNING]
        > <span data-ttu-id="e4333-141">HDInsight obsługuje tylko __ogólnego przeznaczenia__ konta usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="e4333-141">HDInsight only supports __General-purpose__ Azure Storage accounts.</span></span> <span data-ttu-id="e4333-142">Nie obsługuje obecnie hello __magazynu obiektów Blob__ typ konta.</span><span class="sxs-lookup"><span data-stu-id="e4333-142">It does not currently support hello __Blob storage__ account type.</span></span>

* <span data-ttu-id="e4333-143">Można ograniczyć za**uruchomienia dla niektórych typów węzła**, na przykład węzłów głównych lub węzłów procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="e4333-143">Can be restricted too**run on only certain node types**, for example head nodes or worker nodes.</span></span>

  > [!NOTE]
  > <span data-ttu-id="e4333-144">W przypadku użycia z HDInsight Premium, można określić, czy skrypt hello powinien być używany w hello węzła krawędzi.</span><span class="sxs-lookup"><span data-stu-id="e4333-144">When used with HDInsight Premium, you can specify that hello script should be used on hello edge node.</span></span>

* <span data-ttu-id="e4333-145">Może być **utrwalone** lub **ad hoc**.</span><span class="sxs-lookup"><span data-stu-id="e4333-145">Can be **persisted** or **ad hoc**.</span></span>

    <span data-ttu-id="e4333-146">**Utrwalone** skrypty są zastosowane tooworker węzłów dodanych toohello klastra po uruchomieniu skryptu hello.</span><span class="sxs-lookup"><span data-stu-id="e4333-146">**Persisted** scripts are applied tooworker nodes added toohello cluster after hello script runs.</span></span> <span data-ttu-id="e4333-147">Na przykład podczas skalowania w górę hello klastra.</span><span class="sxs-lookup"><span data-stu-id="e4333-147">For example, when scaling up hello cluster.</span></span>

    <span data-ttu-id="e4333-148">Utrwalony skrypt może również zastosować zmiany tooanother węzła typu, na przykład węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="e4333-148">A persisted script might also apply changes tooanother node type, such as a head node.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="e4333-149">Akcji utrwalonego skryptu musi mieć unikatową nazwę.</span><span class="sxs-lookup"><span data-stu-id="e4333-149">Persisted script actions must have a unique name.</span></span>

    <span data-ttu-id="e4333-150">**Ad hoc** skryptów nie są zachowywane.</span><span class="sxs-lookup"><span data-stu-id="e4333-150">**Ad hoc** scripts are not persisted.</span></span> <span data-ttu-id="e4333-151">Nie są zastosowane tooworker węzłów dodanych toohello klastra po hello skryptu ma został uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="e4333-151">They are not applied tooworker nodes added toohello cluster after hello script has ran.</span></span> <span data-ttu-id="e4333-152">Następnie Podwyższ poziom tooa skryptów ad hoc utrwalony skrypt lub obniżyć poziom skryptów ad hoc tooan utrwalonych skryptów.</span><span class="sxs-lookup"><span data-stu-id="e4333-152">You can subsequently promote an ad hoc script tooa persisted script, or demote a persisted script tooan ad hoc script.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="e4333-153">Akcje skryptu używane podczas tworzenia klastra automatycznie są zachowywane.</span><span class="sxs-lookup"><span data-stu-id="e4333-153">Script actions used during cluster creation are automatically persisted.</span></span>
  >
  > <span data-ttu-id="e4333-154">Skrypty, które nie są niepowodzenie utrwalone, nawet jeśli w szczególności wskazują one powinna być.</span><span class="sxs-lookup"><span data-stu-id="e4333-154">Scripts that fail are not persisted, even if you specifically indicate that they should be.</span></span>

* <span data-ttu-id="e4333-155">Można zaakceptować **parametry** używane przez skrypt hello podczas wykonywania.</span><span class="sxs-lookup"><span data-stu-id="e4333-155">Can accept **parameters** that are used by hello script during execution.</span></span>
* <span data-ttu-id="e4333-156">Uruchom z **głównego poziomu uprawnień** hello węzłów klastra.</span><span class="sxs-lookup"><span data-stu-id="e4333-156">Run with **root level privileges** on hello cluster nodes.</span></span>
* <span data-ttu-id="e4333-157">Mogą być używane za pośrednictwem hello **portalu Azure**, **programu Azure PowerShell**, **interfejsu wiersza polecenia Azure**, lub **zestawu .NET SDK usługi HDInsight**</span><span class="sxs-lookup"><span data-stu-id="e4333-157">Can be used through hello **Azure portal**, **Azure PowerShell**, **Azure CLI**, or **HDInsight .NET SDK**</span></span>

<span data-ttu-id="e4333-158">klaster Hello przechowuje historię wszystkie skrypty, które zostały uruchomione.</span><span class="sxs-lookup"><span data-stu-id="e4333-158">hello cluster keeps a history of all scripts that have been ran.</span></span> <span data-ttu-id="e4333-159">Historia Hello jest przydatne, gdy potrzebny jest identyfikator hello toofind skryptu dla operacji podwyższenia poziomu lub obniżania poziomu.</span><span class="sxs-lookup"><span data-stu-id="e4333-159">hello history is useful when you need toofind hello ID of a script for promotion or demotion operations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e4333-160">Nie istnieje żadne tooundo automatyczny sposób hello zmiany wprowadzone przez akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="e4333-160">There is no automatic way tooundo hello changes made by a script action.</span></span> <span data-ttu-id="e4333-161">Należy ręcznie cofnąć zmiany hello lub Podaj skrypt, który odwraca je.</span><span class="sxs-lookup"><span data-stu-id="e4333-161">Either manually reverse hello changes or provide a script that reverses them.</span></span>


### <a name="script-action-in-hello-cluster-creation-process"></a><span data-ttu-id="e4333-162">Akcja skryptu w procesie tworzenia klastra hello</span><span class="sxs-lookup"><span data-stu-id="e4333-162">Script Action in hello cluster creation process</span></span>

<span data-ttu-id="e4333-163">Akcje skryptu używane podczas tworzenia klastra są nieco inne niż skryptu, który akcje został uruchomiony w istniejącym klastrze:</span><span class="sxs-lookup"><span data-stu-id="e4333-163">Script Actions used during cluster creation are slightly different from script actions ran on an existing cluster:</span></span>

* <span data-ttu-id="e4333-164">skrypt Hello jest **automatycznie utrwalonego**.</span><span class="sxs-lookup"><span data-stu-id="e4333-164">hello script is **automatically persisted**.</span></span>
* <span data-ttu-id="e4333-165">A **błąd** w hello skryptu może spowodować toofail procesu tworzenia klastra hello.</span><span class="sxs-lookup"><span data-stu-id="e4333-165">A **failure** in hello script can cause hello cluster creation process toofail.</span></span>

<span data-ttu-id="e4333-166">Witaj poniższym diagramie przedstawiono podczas wykonywania akcji skryptu podczas procesu tworzenia hello:</span><span class="sxs-lookup"><span data-stu-id="e4333-166">hello following diagram illustrates when Script Action is executed during hello creation process:</span></span>

<span data-ttu-id="e4333-167">![Dostosowywanie klastrów usługi HDInsight i etapy podczas tworzenia klastra][img-hdi-cluster-states]</span><span class="sxs-lookup"><span data-stu-id="e4333-167">![HDInsight cluster customization and stages during cluster creation][img-hdi-cluster-states]</span></span>

<span data-ttu-id="e4333-168">Witaj skrypt jest uruchamiany, gdy skonfigurowano usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e4333-168">hello script runs while HDInsight is being configured.</span></span> <span data-ttu-id="e4333-169">Na tym etapie hello skrypt będzie uruchamiany równolegle na wszystkich hello określonych węzłów w klastrze hello i jest uruchamiany z uprawnieniami głównego na węzłach hello.</span><span class="sxs-lookup"><span data-stu-id="e4333-169">At this stage, hello script runs in parallel on all hello specified nodes in hello cluster, and runs with root privileges on hello nodes.</span></span>

> [!NOTE]
> <span data-ttu-id="e4333-170">Ponieważ hello skrypt jest uruchamiany z uprawnieniami poziomu głównego na powitania węzłów klastra, można wykonywać operacje, takie jak zatrzymanie i uruchomienie usług, w tym usług związanych z usługi Hadoop.</span><span class="sxs-lookup"><span data-stu-id="e4333-170">Because hello script runs with root level privilege on hello cluster nodes, you can perform operations like stopping and starting services, including Hadoop-related services.</span></span> <span data-ttu-id="e4333-171">Zatrzymanie usługi, upewnij się, czy hello Ambari usługi i innych usług związanych z Hadoop są gotowe do działania przed skryptu hello zakończeniu.</span><span class="sxs-lookup"><span data-stu-id="e4333-171">If you stop services, you must ensure that hello Ambari service and other Hadoop-related services are up and running before hello script finishes running.</span></span> <span data-ttu-id="e4333-172">Te usługi są wymagane toosuccessfully określić hello kondycję i stan hello klastra podczas jego tworzenia.</span><span class="sxs-lookup"><span data-stu-id="e4333-172">These services are required toosuccessfully determine hello health and state of hello cluster while it is being created.</span></span>


<span data-ttu-id="e4333-173">Podczas tworzenia klastra można użyć jednocześnie wiele akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="e4333-173">During cluster creation, you can use multiple script actions at once.</span></span> <span data-ttu-id="e4333-174">Skrypty te są wywoływane w kolejności hello, w jakiej zostały określone.</span><span class="sxs-lookup"><span data-stu-id="e4333-174">These scripts are invoked in hello order in which they were specified.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e4333-175">Akcje skryptu należy wykonać w ciągu 60 minut lub limitu czasu.</span><span class="sxs-lookup"><span data-stu-id="e4333-175">Script actions must complete within 60 minutes, or timeout.</span></span> <span data-ttu-id="e4333-176">Podczas inicjowania obsługi klastra hello skrypt jest uruchamiany równocześnie z innymi procesami instalacji i konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="e4333-176">During cluster provisioning, hello script runs concurrently with other setup and configuration processes.</span></span> <span data-ttu-id="e4333-177">Konkurowanie o zasoby, takie jak czas lub sieci przepustowości Procesora może powodować hello skryptu tootake dłużej toofinish niż w środowisku projektowania.</span><span class="sxs-lookup"><span data-stu-id="e4333-177">Competition for resources such as CPU time or network bandwidth may cause hello script tootake longer toofinish than it does in your development environment.</span></span>
>
> <span data-ttu-id="e4333-178">toominimize hello czasu zajmuje toorun hello skryptu, należy unikać zadań, takich jak pobieranie i kompilowanie aplikacji ze źródła.</span><span class="sxs-lookup"><span data-stu-id="e4333-178">toominimize hello time it takes toorun hello script, avoid tasks such as downloading and compiling applications from source.</span></span> <span data-ttu-id="e4333-179">Wstępnie skompilować aplikacje i przechowywać dane binarne hello w usłudze Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="e4333-179">Pre-compile applications and store hello binary in Azure Storage.</span></span>


### <a name="script-action-on-a-running-cluster"></a><span data-ttu-id="e4333-180">Akcja skryptu w klastrze uruchomione</span><span class="sxs-lookup"><span data-stu-id="e4333-180">Script action on a running cluster</span></span>

<span data-ttu-id="e4333-181">W przeciwieństwie do skryptu, który akcje używane podczas tworzenia klastra, błąd skryptu uruchomionego na już działającego klastra nie powoduje automatycznego hello klastra toochange tooa nie powiodło się stan.</span><span class="sxs-lookup"><span data-stu-id="e4333-181">Unlike script actions used during cluster creation, a failure in a script ran on an already running cluster does not automatically cause hello cluster toochange tooa failed state.</span></span> <span data-ttu-id="e4333-182">Po ukończeniu działania skryptu hello klastra powinna zwrócić tooa "uruchomiona".</span><span class="sxs-lookup"><span data-stu-id="e4333-182">Once a script completes, hello cluster should return tooa "running" state.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e4333-183">Nawet jeśli hello klastra ma stan "uruchomiona", hello skryptu nie powiodło się mogą zawierać uszkodzone elementy.</span><span class="sxs-lookup"><span data-stu-id="e4333-183">Even if hello cluster has a 'running' state, hello failed script may have broken things.</span></span> <span data-ttu-id="e4333-184">Na przykład skrypt można usunąć pliki wymagane przez hello klastra.</span><span class="sxs-lookup"><span data-stu-id="e4333-184">For example, a script could delete files needed by hello cluster.</span></span>
>
> <span data-ttu-id="e4333-185">Skrypty akcje uruchamiane z uprawnieniami głównego, dlatego należy się zapoznać przed zastosowaniem klastra tooyour działania skryptu.</span><span class="sxs-lookup"><span data-stu-id="e4333-185">Scripts actions run with root privileges, so you should make sure that you understand what a script does before applying it tooyour cluster.</span></span>

<span data-ttu-id="e4333-186">Podczas stosowania klastra tooa skryptu, hello klastra stan zmieni się toofrom **systemem** za**zaakceptowane**, następnie **konfiguracji HDInsight**, a na koniec z powrotem zbyt**Systemem** skryptów powiodło się.</span><span class="sxs-lookup"><span data-stu-id="e4333-186">When applying a script tooa cluster, hello cluster state changes toofrom **Running** too**Accepted**, then **HDInsight configuration**, and finally back too**Running** for successful scripts.</span></span> <span data-ttu-id="e4333-187">Stan skryptu Hello jest rejestrowane w historii akcji skryptu hello i za pomocą tego toodetermine informacji czy skrypt hello powodzeniem lub niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="e4333-187">hello script status is logged in hello script action history, and you can use this information toodetermine whether hello script succeeded or failed.</span></span> <span data-ttu-id="e4333-188">Na przykład Witaj `Get-AzureRmHDInsightScriptActionHistory` polecenia cmdlet programu PowerShell może być używane tooview hello stanu skryptu.</span><span class="sxs-lookup"><span data-stu-id="e4333-188">For example, hello `Get-AzureRmHDInsightScriptActionHistory` PowerShell cmdlet can be used tooview hello status of a script.</span></span> <span data-ttu-id="e4333-189">Zwraca informacje toohello podobne następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="e4333-189">It returns information similar toohello following text:</span></span>

    ScriptExecutionId : 635918532516474303
    StartTime         : 8/14/2017 7:40:55 PM
    EndTime           : 8/14/2017 7:41:05 PM
    Status            : Succeeded

> [!NOTE]
> <span data-ttu-id="e4333-190">Jeśli zmienisz hasło użytkownika (Administrator) klastra powitania po utworzeniu klastra hello, skryptów, które akcje przeprowadzony na ten klaster może zakończyć się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="e4333-190">If you have changed hello cluster user (admin) password after hello cluster was created, script actions ran against this cluster may fail.</span></span> <span data-ttu-id="e4333-191">Jeśli masz żadnych akcji utrwalonego skryptu tej docelowej węzłów procesu roboczego, te skrypty może zakończyć się niepowodzeniem podczas skalowania hello klastra.</span><span class="sxs-lookup"><span data-stu-id="e4333-191">If you have any persisted script actions that target worker nodes, these scripts may fail when you scale hello cluster.</span></span>

## <a name="example-script-action-scripts"></a><span data-ttu-id="e4333-192">Przykładowe skrypty akcji skryptu</span><span class="sxs-lookup"><span data-stu-id="e4333-192">Example Script Action scripts</span></span>

<span data-ttu-id="e4333-193">Skrypt skrypty akcji mogą być używane za pośrednictwem hello następujące narzędzia:</span><span class="sxs-lookup"><span data-stu-id="e4333-193">Script Action scripts can be used through hello following utilities:</span></span>

* <span data-ttu-id="e4333-194">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e4333-194">Azure portal</span></span>
* <span data-ttu-id="e4333-195">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e4333-195">Azure PowerShell</span></span>
* <span data-ttu-id="e4333-196">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e4333-196">Azure CLI</span></span>
* <span data-ttu-id="e4333-197">Zestaw SDK dla platformy .NET usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="e4333-197">HDInsight .NET SDK</span></span>

<span data-ttu-id="e4333-198">Usługa HDInsight zapewnia następujące składniki w klastrach HDInsight hello tooinstall skrypty:</span><span class="sxs-lookup"><span data-stu-id="e4333-198">HDInsight provides scripts tooinstall hello following components on HDInsight clusters:</span></span>

| <span data-ttu-id="e4333-199">Nazwa</span><span class="sxs-lookup"><span data-stu-id="e4333-199">Name</span></span> | <span data-ttu-id="e4333-200">Skrypt</span><span class="sxs-lookup"><span data-stu-id="e4333-200">Script</span></span> |
| --- | --- |
| <span data-ttu-id="e4333-201">**Dodaj konto usługi Azure Storage**</span><span class="sxs-lookup"><span data-stu-id="e4333-201">**Add an Azure Storage account**</span></span> |<span data-ttu-id="e4333-202">https://hdiconfigactions.blob.Core.Windows.NET/linuxaddstorageaccountv01/Add-Storage-Account-v01.sh. Zobacz [klastra usługi HDInsight tooan dodatkowego magazynu Dodaj](hdinsight-hadoop-add-storage.md).</span><span class="sxs-lookup"><span data-stu-id="e4333-202">https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh. See [Add additional storage tooan HDInsight cluster](hdinsight-hadoop-add-storage.md).</span></span> |
| <span data-ttu-id="e4333-203">**Instalowanie aplikacji Hue**</span><span class="sxs-lookup"><span data-stu-id="e4333-203">**Install Hue**</span></span> |<span data-ttu-id="e4333-204">https://hdiconfigactions.blob.Core.Windows.NET/linuxhueconfigactionv02/Install-Hue-Uber-v02.sh. Zobacz [instalacji i używania aplikacji Hue w usłudze HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="e4333-204">https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh. See [Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> |
| <span data-ttu-id="e4333-205">**Zainstaluj Presto**</span><span class="sxs-lookup"><span data-stu-id="e4333-205">**Install Presto**</span></span> |<span data-ttu-id="e4333-206">https://RAW.githubusercontent.com/hdinsight/Presto-hdinsight/Master/installpresto.sh. Zobacz [instalacji i używania Presto w usłudze HDInsight clusters](hdinsight-hadoop-install-presto.md).</span><span class="sxs-lookup"><span data-stu-id="e4333-206">https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh. See [Install and use Presto on HDInsight clusters](hdinsight-hadoop-install-presto.md).</span></span> |
| <span data-ttu-id="e4333-207">**Zainstaluj Solr**</span><span class="sxs-lookup"><span data-stu-id="e4333-207">**Install Solr**</span></span> |<span data-ttu-id="e4333-208">https://hdiconfigactions.blob.Core.Windows.NET/linuxsolrconfigactionv01/solr-Installer-v01.sh. Zobacz [instalacji i używania Solr w usłudze HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="e4333-208">https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh. See [Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span> |
| <span data-ttu-id="e4333-209">**Zainstaluj Giraph**</span><span class="sxs-lookup"><span data-stu-id="e4333-209">**Install Giraph**</span></span> |<span data-ttu-id="e4333-210">https://hdiconfigactions.blob.Core.Windows.NET/linuxgiraphconfigactionv01/giraph-Installer-v01.sh. Zobacz [instalacji i używania Giraph w usłudze HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="e4333-210">https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh. See [Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> |
| <span data-ttu-id="e4333-211">**Wstępne ładowanie bibliotek technologii Hive**</span><span class="sxs-lookup"><span data-stu-id="e4333-211">**Pre-load Hive libraries**</span></span> |<span data-ttu-id="e4333-212">https://hdiconfigactions.blob.Core.Windows.NET/linuxsetupcustomhivelibsv01/Setup-customhivelibs-v01.sh. Zobacz [dodać Hive bibliotek w klastrach HDInsight](hdinsight-hadoop-add-hive-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="e4333-212">https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh. See [Add Hive libraries on HDInsight clusters](hdinsight-hadoop-add-hive-libraries.md).</span></span> |
| <span data-ttu-id="e4333-213">**Instalowanie i aktualizowanie środowiska Mono**</span><span class="sxs-lookup"><span data-stu-id="e4333-213">**Install or update Mono**</span></span> | <span data-ttu-id="e4333-214">https://hdiconfigactions.blob.Core.Windows.NET/Install-mono/Install-mono.bash.</span><span class="sxs-lookup"><span data-stu-id="e4333-214">https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash.</span></span> <span data-ttu-id="e4333-215">Zobacz [instalacji lub aktualizacji Mono w usłudze HDInsight](hdinsight-hadoop-install-mono.md).</span><span class="sxs-lookup"><span data-stu-id="e4333-215">See [Install or update Mono on HDInsight](hdinsight-hadoop-install-mono.md).</span></span> |

## <a name="use-a-script-action-during-cluster-creation"></a><span data-ttu-id="e4333-216">Użyć akcji skryptu podczas tworzenia klastra</span><span class="sxs-lookup"><span data-stu-id="e4333-216">Use a Script Action during cluster creation</span></span>

<span data-ttu-id="e4333-217">Ta sekcja zawiera przykłady na różne sposoby hello akcji skryptu można użyć podczas tworzenia klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e4333-217">This section provides examples on hello different ways you can use script actions when creating an HDInsight cluster.</span></span>

### <a name="use-a-script-action-during-cluster-creation-from-hello-azure-portal"></a><span data-ttu-id="e4333-218">Użyć akcji skryptu podczas tworzenia klastra z hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="e4333-218">Use a Script Action during cluster creation from hello Azure portal</span></span>

1. <span data-ttu-id="e4333-219">Rozpocznij tworzenie klastra, zgodnie z opisem w [klastrów utworzyć Hadoop w HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="e4333-219">Start creating a cluster as described at [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="e4333-220">Zatrzymać po osiągnięciu hello __klastra Podsumowanie__ sekcji.</span><span class="sxs-lookup"><span data-stu-id="e4333-220">Stop when you reach hello __Cluster summary__ section.</span></span>

2. <span data-ttu-id="e4333-221">Z hello __klastra Podsumowanie__ sekcji, wybierz hello __Edytuj__ łączy dla __Zaawansowane ustawienia__.</span><span class="sxs-lookup"><span data-stu-id="e4333-221">From hello __Cluster summary__ section, select hello __edit__ link for __Advanced settings__.</span></span>

    ![Łącze Ustawienia zaawansowane](./media/hdinsight-hadoop-customize-cluster-linux/advanced-settings-link.png)

3. <span data-ttu-id="e4333-223">Z hello __Zaawansowane ustawienia__ zaznacz __skryptu akcji__.</span><span class="sxs-lookup"><span data-stu-id="e4333-223">From hello __Advanced settings__ section, select __Script actions__.</span></span> <span data-ttu-id="e4333-224">Z hello __skryptu akcje__ zaznacz __+ nowy przesyłania__</span><span class="sxs-lookup"><span data-stu-id="e4333-224">From hello __Script actions__ section, select __+ Submit new__</span></span>

    ![Przedstawia nowa akcja skryptu](./media/hdinsight-hadoop-customize-cluster-linux/add-script-action.png)

4. <span data-ttu-id="e4333-226">Użyj hello __wybierz skrypt__ tooselect wpis wstępnie przygotowanych skryptu.</span><span class="sxs-lookup"><span data-stu-id="e4333-226">Use hello __Select a script__ entry tooselect a pre-made script.</span></span> <span data-ttu-id="e4333-227">Wybierz toouse skryptu niestandardowego __niestandardowych__ , a następnie wprowadź hello __nazwa__ i __Bash skryptu identyfikatora URI__ skryptu.</span><span class="sxs-lookup"><span data-stu-id="e4333-227">toouse a custom script, select __Custom__ and then provide hello __Name__ and __Bash script URI__ for your script.</span></span>

    ![Dodawanie skryptu w formie skryptu wybierz hello](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    <span data-ttu-id="e4333-229">Witaj w poniższej tabeli opisano elementy hello w formularzu hello:</span><span class="sxs-lookup"><span data-stu-id="e4333-229">hello following table describes hello elements on hello form:</span></span>

    | <span data-ttu-id="e4333-230">Właściwość</span><span class="sxs-lookup"><span data-stu-id="e4333-230">Property</span></span> | <span data-ttu-id="e4333-231">Wartość</span><span class="sxs-lookup"><span data-stu-id="e4333-231">Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="e4333-232">Wybierz skrypt</span><span class="sxs-lookup"><span data-stu-id="e4333-232">Select a script</span></span> | <span data-ttu-id="e4333-233">toouse własnego skryptu, wybierz opcję __niestandardowy__.</span><span class="sxs-lookup"><span data-stu-id="e4333-233">toouse your own script, select __Custom__.</span></span> <span data-ttu-id="e4333-234">W przeciwnym razie wybierz hello podane skryptów.</span><span class="sxs-lookup"><span data-stu-id="e4333-234">Otherwise, select one of hello provided scripts.</span></span> |
    | <span data-ttu-id="e4333-235">Nazwa</span><span class="sxs-lookup"><span data-stu-id="e4333-235">Name</span></span> |<span data-ttu-id="e4333-236">Określ nazwę hello akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="e4333-236">Specify a name for hello script action.</span></span> |
    | <span data-ttu-id="e4333-237">Skrypt bash identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="e4333-237">Bash script URI</span></span> |<span data-ttu-id="e4333-238">Określ hello URI toohello skrypt, który jest wywołana toocustomize hello klastra.</span><span class="sxs-lookup"><span data-stu-id="e4333-238">Specify hello URI toohello script that is invoked toocustomize hello cluster.</span></span> |
    | <span data-ttu-id="e4333-239">Dozorcy HEAD/procesu roboczego</span><span class="sxs-lookup"><span data-stu-id="e4333-239">Head/Worker/Zookeeper</span></span> |<span data-ttu-id="e4333-240">Określ węzły hello (**Head**, **procesu roboczego**, lub **dozorcy**) na których dostosowanie hello skrypt jest uruchamiany.</span><span class="sxs-lookup"><span data-stu-id="e4333-240">Specify hello nodes (**Head**, **Worker**, or **ZooKeeper**) on which hello customization script is run.</span></span> |
    | <span data-ttu-id="e4333-241">Parametry</span><span class="sxs-lookup"><span data-stu-id="e4333-241">Parameters</span></span> |<span data-ttu-id="e4333-242">Określ parametry hello, jeśli są wymagane przez skrypt hello.</span><span class="sxs-lookup"><span data-stu-id="e4333-242">Specify hello parameters, if required by hello script.</span></span> |

    <span data-ttu-id="e4333-243">Użyj hello __Utrwal tę akcję skryptu__ tooensure wpis, który hello skryptu jest stosowany podczas operacji skalowania.</span><span class="sxs-lookup"><span data-stu-id="e4333-243">Use hello __Persist this script action__ entry tooensure that hello script is applied during scaling operations.</span></span>

5. <span data-ttu-id="e4333-244">Wybierz __Utwórz__ toosave hello skryptu.</span><span class="sxs-lookup"><span data-stu-id="e4333-244">Select __Create__ toosave hello script.</span></span> <span data-ttu-id="e4333-245">Następnie można użyć __+ przesyłania nowych__ tooadd inny skrypt.</span><span class="sxs-lookup"><span data-stu-id="e4333-245">You can then use __+ Submit new__ tooadd another script.</span></span>

    ![Wiele akcji skryptu](./media/hdinsight-hadoop-customize-cluster-linux/multiple-scripts.png)

    <span data-ttu-id="e4333-247">Po zakończeniu dodawania skryptów, użyj hello __wybierz__ przycisk, a następnie hello __dalej__ toohello tooreturn przycisk __klastra Podsumowanie__ sekcji.</span><span class="sxs-lookup"><span data-stu-id="e4333-247">When you are done adding scripts, use hello __Select__ button, and then hello __Next__ button tooreturn toohello __Cluster summary__ section.</span></span>

3. <span data-ttu-id="e4333-248">toocreate hello klastra, wybierz opcję __Utwórz__ z hello __klastra Podsumowanie__ zaznaczenia.</span><span class="sxs-lookup"><span data-stu-id="e4333-248">toocreate hello cluster, select __Create__ from hello __Cluster summary__ selection.</span></span>

### <a name="use-a-script-action-from-azure-resource-manager-templates"></a><span data-ttu-id="e4333-249">Użyć akcji skryptu z szablonów usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e4333-249">Use a Script Action from Azure Resource Manager templates</span></span>

<span data-ttu-id="e4333-250">Przykłady Hello w tej sekcji pokazują, jak toouse skryptu akcji przy użyciu szablonów usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e4333-250">hello examples in this section demonstrate how toouse script actions with Azure Resource Manager templates.</span></span>

#### <a name="before-you-begin"></a><span data-ttu-id="e4333-251">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="e4333-251">Before you begin</span></span>

* <span data-ttu-id="e4333-252">Aby uzyskać informacji na temat konfigurowania stacji roboczej toorun poleceń cmdlet programu Powershell w usłudze HDInsight, zobacz [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e4333-252">For information about configuring a workstation toorun HDInsight Powershell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="e4333-253">Aby uzyskać instrukcje na temat szablonów toocreate, zobacz [szablonów Authoring Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="e4333-253">For instructions on how toocreate templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="e4333-254">Jeśli nie były wcześniej używane programu Azure PowerShell z usługą Resource Manager, zobacz [przy użyciu programu Azure PowerShell z usługą Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="e4333-254">If you have not previously used Azure PowerShell with Resource Manager, see [Using Azure PowerShell with Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

#### <a name="create-clusters-using-script-action"></a><span data-ttu-id="e4333-255">Tworzenie klastrów za pomocą akcji skryptu</span><span class="sxs-lookup"><span data-stu-id="e4333-255">Create clusters using Script Action</span></span>

1. <span data-ttu-id="e4333-256">Skopiuj hello następującego szablonu tooa lokalizacji na komputerze.</span><span class="sxs-lookup"><span data-stu-id="e4333-256">Copy hello following template tooa location on your computer.</span></span> <span data-ttu-id="e4333-257">Ten szablon instaluje Giraph hello headnodes i proces roboczy węzłach klastra hello.</span><span class="sxs-lookup"><span data-stu-id="e4333-257">This template installs Giraph on hello headnodes and worker nodes in hello cluster.</span></span> <span data-ttu-id="e4333-258">Możesz również sprawdzić, czy szablon JSON hello jest prawidłowy.</span><span class="sxs-lookup"><span data-stu-id="e4333-258">You can also verify if hello JSON template is valid.</span></span> <span data-ttu-id="e4333-259">Wklej szablon zawartości do [JSONLint](http://jsonlint.com/), narzędzie sprawdzania poprawności online JSON.</span><span class="sxs-lookup"><span data-stu-id="e4333-259">Paste your template content into [JSONLint](http://jsonlint.com/), an online JSON validation tool.</span></span>

            {
            "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
            "contentVersion": "1.0.0.0",
            "parameters": {
                "clusterLocation": {
                    "type": "string",
                    "defaultValue": "West US",
                    "allowedValues": [ "West US" ]
                },
                "clusterName": {
                    "type": "string"
                },
                "clusterUserName": {
                    "type": "string",
                    "defaultValue": "admin"
                },
                "clusterUserPassword": {
                    "type": "securestring"
                },
                "sshUserName": {
                    "type": "string",
                    "defaultValue": "username"
                },
                "sshPassword": {
                    "type": "securestring"
                },
                "clusterStorageAccountName": {
                    "type": "string"
                },
                "clusterStorageAccountResourceGroup": {
                    "type": "string"
                },
                "clusterStorageType": {
                    "type": "string",
                    "defaultValue": "Standard_LRS",
                    "allowedValues": [
                        "Standard_LRS",
                        "Standard_GRS",
                        "Standard_ZRS"
                    ]
                },
                "clusterStorageAccountContainer": {
                    "type": "string"
                },
                "clusterHeadNodeCount": {
                    "type": "int",
                    "defaultValue": 1
                },
                "clusterWorkerNodeCount": {
                    "type": "int",
                    "defaultValue": 2
                }
            },
            "variables": {
            },
            "resources": [
                {
                    "name": "[parameters('clusterStorageAccountName')]",
                    "type": "Microsoft.Storage/storageAccounts",
                    "location": "[parameters('clusterLocation')]",
                    "apiVersion": "2015-05-01-preview",
                    "dependsOn": [ ],
                    "tags": { },
                    "properties": {
                        "accountType": "[parameters('clusterStorageType')]"
                    }
                },
                {
                    "name": "[parameters('clusterName')]",
                    "type": "Microsoft.HDInsight/clusters",
                    "location": "[parameters('clusterLocation')]",
                    "apiVersion": "2015-03-01-preview",
                    "dependsOn": [
                        "[concat('Microsoft.Storage/storageAccounts/', parameters('clusterStorageAccountName'))]"
                    ],
                    "tags": { },
                    "properties": {
                        "clusterVersion": "3.2",
                        "osType": "Linux",
                        "clusterDefinition": {
                            "kind": "hadoop",
                            "configurations": {
                                "gateway": {
                                    "restAuthCredential.isEnabled": true,
                                    "restAuthCredential.username": "[parameters('clusterUserName')]",
                                    "restAuthCredential.password": "[parameters('clusterUserPassword')]"
                                }
                            }
                        },
                        "storageProfile": {
                            "storageaccounts": [
                                {
                                    "name": "[concat(parameters('clusterStorageAccountName'),'.blob.core.windows.net')]",
                                    "isDefault": true,
                                    "container": "[parameters('clusterStorageAccountContainer')]",
                                    "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('clusterStorageAccountName')), '2015-05-01-preview').key1]"
                                }
                            ]
                        },
                        "computeProfile": {
                            "roles": [
                                {
                                    "name": "headnode",
                                    "targetInstanceCount": "[parameters('clusterHeadNodeCount')]",
                                    "hardwareProfile": {
                                        "vmSize": "Large"
                                    },
                                    "osProfile": {
                                        "linuxOperatingSystemProfile": {
                                            "username": "[parameters('sshUserName')]",
                                            "password": "[parameters('sshPassword')]"
                                        }
                                    },
                                    "scriptActions": [
                                        {
                                            "name": "installGiraph",
                                            "uri": "https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh",
                                            "parameters": ""
                                        }
                                    ]
                                },
                                {
                                    "name": "workernode",
                                    "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                                    "hardwareProfile": {
                                        "vmSize": "Large"
                                    },
                                    "osProfile": {
                                        "linuxOperatingSystemProfile": {
                                            "username": "[parameters('sshUserName')]",
                                            "password": "[parameters('sshPassword')]"
                                        }
                                    },
                                    "scriptActions": [
                                        {
                                            "name": "installR",
                                            "uri": "https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh",
                                            "parameters": ""
                                        }
                                    ]
                                }
                            ]
                        }
                    }
                }
            ],
            "outputs": {
                "cluster":{
                    "type" : "object",
                    "value" : "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
                }
            }
        }
2. <span data-ttu-id="e4333-260">Uruchom program Azure PowerShell i logowania tooyour konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e4333-260">Start Azure PowerShell and Log in tooyour Azure account.</span></span> <span data-ttu-id="e4333-261">Po podaniu poświadczeń, hello polecenie zwraca informacje o Twoim koncie.</span><span class="sxs-lookup"><span data-stu-id="e4333-261">After providing your credentials, hello command returns information about your account.</span></span>

        Add-AzureRmAccount

        Id                             Type       ...
        --                             ----
        someone@example.com            User       ...
3. <span data-ttu-id="e4333-262">Jeśli masz wiele subskrypcji, podaj identyfikator subskrypcji hello mają toouse dla wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="e4333-262">If you have multiple subscriptions, provide hello subscription ID you wish toouse for deployment.</span></span>

        Select-AzureRmSubscription -SubscriptionID <YourSubscriptionId>

    > [!NOTE]
    > <span data-ttu-id="e4333-263">Można użyć `Get-AzureRmSubscription` tooget listę wszystkich subskrypcji skojarzonych z Twoim kontem, w tym hello identyfikator subskrypcji dla każdej z nich.</span><span class="sxs-lookup"><span data-stu-id="e4333-263">You can use `Get-AzureRmSubscription` tooget a list of all subscriptions associated with your account, which includes hello subscription ID for each one.</span></span>

4. <span data-ttu-id="e4333-264">Jeśli nie masz istniejącej grupy zasobów, należy utworzyć grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="e4333-264">If you do not have an existing resource group, create a resource group.</span></span> <span data-ttu-id="e4333-265">Podaj nazwę hello hello grupy zasobów i lokalizacji, która należy do rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="e4333-265">Provide hello name of hello resource group and location that you need for your solution.</span></span> <span data-ttu-id="e4333-266">Zwracany jest podsumowanie hello nową grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="e4333-266">A summary of hello new resource group is returned.</span></span>

        New-AzureRmResourceGroup -Name myresourcegroup -Location "West US"

        ResourceGroupName : myresourcegroup
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/######/resourceGroups/ExampleResourceGroup

5. <span data-ttu-id="e4333-267">toocreate wdrożenia dla grupy zasobów, uruchom hello **AzureRmResourceGroupDeployment nowy** poleceń i podaj hello wymaganych parametrów.</span><span class="sxs-lookup"><span data-stu-id="e4333-267">toocreate a deployment for your resource group, run hello **New-AzureRmResourceGroupDeployment** command and provide hello necessary parameters.</span></span> <span data-ttu-id="e4333-268">Parametry Hello zawierają hello następujące dane:</span><span class="sxs-lookup"><span data-stu-id="e4333-268">hello parameters include hello following data:</span></span>

    * <span data-ttu-id="e4333-269">Nazwa wdrożenia</span><span class="sxs-lookup"><span data-stu-id="e4333-269">A name for your deployment</span></span>
    * <span data-ttu-id="e4333-270">Witaj nazwę grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="e4333-270">hello name of your resource group</span></span>
    * <span data-ttu-id="e4333-271">Ścieżka Hello lub utworzony szablon toohello adresu URL.</span><span class="sxs-lookup"><span data-stu-id="e4333-271">hello path or URL toohello template you created.</span></span>

  <span data-ttu-id="e4333-272">Jeśli szablon wymaga parametrów, należy podać także tych parametrów.</span><span class="sxs-lookup"><span data-stu-id="e4333-272">If your template requires any parameters, you must pass those parameters as well.</span></span> <span data-ttu-id="e4333-273">W takim przypadku tooinstall akcji skryptu hello R w klastrze hello nie wymaga żadnych parametrów.</span><span class="sxs-lookup"><span data-stu-id="e4333-273">In this case, hello script action tooinstall R on hello cluster does not require any parameters.</span></span>

        New-AzureRmResourceGroupDeployment -Name mydeployment -ResourceGroupName myresourcegroup -TemplateFile <PathOrLinkToTemplate>

    <span data-ttu-id="e4333-274">Jesteś tooprovide zostanie wyświetlony monit o wartości parametrów hello zdefiniowane w szablonie hello.</span><span class="sxs-lookup"><span data-stu-id="e4333-274">You are prompted tooprovide values for hello parameters defined in hello template.</span></span>

1. <span data-ttu-id="e4333-275">Po wdrożeniu grupy zasobów hello zostanie wyświetlone podsumowanie wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="e4333-275">When hello resource group has been deployed, a summary of hello deployment is displayed.</span></span>

          DeploymentName    : mydeployment
          ResourceGroupName : myresourcegroup
          ProvisioningState : Succeeded
          Timestamp         : 8/14/2017 7:00:27 PM
          Mode              : Incremental
          ...

2. <span data-ttu-id="e4333-276">Jeśli wdrożenie nie powiedzie się, można użyć następującego polecenia cmdlet tooget informacje o niepowodzeniach hello hello.</span><span class="sxs-lookup"><span data-stu-id="e4333-276">If your deployment fails, you can use hello following cmdlets tooget information about hello failures.</span></span>

        Get-AzureRmResourceGroupDeployment -ResourceGroupName myresourcegroup -ProvisioningState Failed

### <a name="use-a-script-action-during-cluster-creation-from-azure-powershell"></a><span data-ttu-id="e4333-277">Użyć akcji skryptu podczas tworzenia klastra z programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e4333-277">Use a Script Action during cluster creation from Azure PowerShell</span></span>

<span data-ttu-id="e4333-278">W tej sekcji użyjesz hello [AzureRmHDInsightScriptAction Dodaj](https://msdn.microsoft.com/library/mt603527.aspx) skrypty tooinvoke polecenia cmdlet, za pomocą akcji skryptu toocustomize klastra.</span><span class="sxs-lookup"><span data-stu-id="e4333-278">In this section, we use hello [Add-AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx) cmdlet tooinvoke scripts by using Script Action toocustomize a cluster.</span></span> <span data-ttu-id="e4333-279">Przed kontynuowaniem upewnij się, zainstalowaniu i skonfigurowaniu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e4333-279">Before proceeding, make sure you have installed and configured Azure PowerShell.</span></span> <span data-ttu-id="e4333-280">Aby uzyskać informacji na temat konfigurowania stacji roboczej toorun poleceń cmdlet programu PowerShell w usłudze HDInsight, zobacz [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e4333-280">For information about configuring a workstation toorun HDInsight PowerShell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="e4333-281">Witaj poniższy skrypt pokazuje, jak tooapply akcji skryptu podczas tworzenia klastra przy użyciu programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="e4333-281">hello following script demonstrates how tooapply a script action when creating a cluster using PowerShell:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=5-90)]

<span data-ttu-id="e4333-282">Może upłynąć kilka minut przed utworzeniem klastra hello.</span><span class="sxs-lookup"><span data-stu-id="e4333-282">It can take several minutes before hello cluster is created.</span></span>

### <a name="use-a-script-action-during-cluster-creation-from-hello-hdinsight-net-sdk"></a><span data-ttu-id="e4333-283">Użyć akcji skryptu podczas tworzenia klastra z hello zestawu .NET SDK usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="e4333-283">Use a Script Action during cluster creation from hello HDInsight .NET SDK</span></span>

<span data-ttu-id="e4333-284">Witaj zestawu .NET SDK usługi HDInsight zapewnia bibliotek klienckich, które umożliwia łatwiejsze toowork z usługą HDInsight z poziomu aplikacji .NET.</span><span class="sxs-lookup"><span data-stu-id="e4333-284">hello HDInsight .NET SDK provides client libraries that makes it easier toowork with HDInsight from a .NET application.</span></span> <span data-ttu-id="e4333-285">Przykładowy kod [opartych na systemie Linux z tworzenia klastrów w usłudze HDInsight przy użyciu hello zestawu .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action).</span><span class="sxs-lookup"><span data-stu-id="e4333-285">For a code sample, see [Create Linux-based clusters in HDInsight using hello .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action).</span></span>

## <a name="apply-a-script-action-tooa-running-cluster"></a><span data-ttu-id="e4333-286">Zastosuj tooa akcji skryptu, z klastra</span><span class="sxs-lookup"><span data-stu-id="e4333-286">Apply a Script Action tooa running cluster</span></span>

<span data-ttu-id="e4333-287">W tej sekcji Dowiedz się, jak tooapply skryptu tooa akcji uruchamiania klastra.</span><span class="sxs-lookup"><span data-stu-id="e4333-287">In this section, learn how tooapply script actions tooa running cluster.</span></span>

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-azure-portal"></a><span data-ttu-id="e4333-288">Zastosuj tooa akcji skryptu, uruchamiając klastra z hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="e4333-288">Apply a Script Action tooa running cluster from hello Azure portal</span></span>

1. <span data-ttu-id="e4333-289">Z hello [portalu Azure](https://portal.azure.com), wybierz z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e4333-289">From hello [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span>

2. <span data-ttu-id="e4333-290">Omówienie klastrów HDInsight hello, zaznacz hello **akcji skryptu** kafelka.</span><span class="sxs-lookup"><span data-stu-id="e4333-290">From hello HDInsight cluster overview, select hello **Script Actions** tile.</span></span>

    ![Kafelek akcji skryptu](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > <span data-ttu-id="e4333-292">Możesz też wybrać **wszystkie ustawienia** , a następnie wybierz **akcji skryptu** z hello w sekcji Ustawienia.</span><span class="sxs-lookup"><span data-stu-id="e4333-292">You can also select **All settings** and then select **Script Actions** from hello Settings section.</span></span>

3. <span data-ttu-id="e4333-293">Z góry hello hello sekcji akcji skryptu, wybierz **przesyłania nowych**.</span><span class="sxs-lookup"><span data-stu-id="e4333-293">From hello top of hello Script Actions section, select **Submit new**.</span></span>

    ![Dodaj tooa skryptu, z klastra](./media/hdinsight-hadoop-customize-cluster-linux/add-script-running-cluster.png)

4. <span data-ttu-id="e4333-295">Użyj hello __wybierz skrypt__ tooselect wpis wstępnie przygotowanych skryptu.</span><span class="sxs-lookup"><span data-stu-id="e4333-295">Use hello __Select a script__ entry tooselect a pre-made script.</span></span> <span data-ttu-id="e4333-296">Wybierz toouse skryptu niestandardowego __niestandardowych__ , a następnie wprowadź hello __nazwa__ i __Bash skryptu identyfikatora URI__ skryptu.</span><span class="sxs-lookup"><span data-stu-id="e4333-296">toouse a custom script, select __Custom__ and then provide hello __Name__ and __Bash script URI__ for your script.</span></span>

    ![Dodawanie skryptu w formie skryptu wybierz hello](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    <span data-ttu-id="e4333-298">Witaj w poniższej tabeli opisano elementy hello w formularzu hello:</span><span class="sxs-lookup"><span data-stu-id="e4333-298">hello following table describes hello elements on hello form:</span></span>

    | <span data-ttu-id="e4333-299">Właściwość</span><span class="sxs-lookup"><span data-stu-id="e4333-299">Property</span></span> | <span data-ttu-id="e4333-300">Wartość</span><span class="sxs-lookup"><span data-stu-id="e4333-300">Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="e4333-301">Wybierz skrypt</span><span class="sxs-lookup"><span data-stu-id="e4333-301">Select a script</span></span> | <span data-ttu-id="e4333-302">toouse własnego skryptu, wybierz opcję __niestandardowych__.</span><span class="sxs-lookup"><span data-stu-id="e4333-302">toouse your own script, select __custom__.</span></span> <span data-ttu-id="e4333-303">W przeciwnym razie wybierz udostępnionego skryptu.</span><span class="sxs-lookup"><span data-stu-id="e4333-303">Otherwise, select a provided script.</span></span> |
    | <span data-ttu-id="e4333-304">Nazwa</span><span class="sxs-lookup"><span data-stu-id="e4333-304">Name</span></span> |<span data-ttu-id="e4333-305">Określ nazwę hello akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="e4333-305">Specify a name for hello script action.</span></span> |
    | <span data-ttu-id="e4333-306">Skrypt bash identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="e4333-306">Bash script URI</span></span> |<span data-ttu-id="e4333-307">Określ hello URI toohello skrypt, który jest wywołana toocustomize hello klastra.</span><span class="sxs-lookup"><span data-stu-id="e4333-307">Specify hello URI toohello script that is invoked toocustomize hello cluster.</span></span> |
    | <span data-ttu-id="e4333-308">Dozorcy HEAD/procesu roboczego</span><span class="sxs-lookup"><span data-stu-id="e4333-308">Head/Worker/Zookeeper</span></span> |<span data-ttu-id="e4333-309">Określ węzły hello (**Head**, **procesu roboczego**, lub **dozorcy**) na których dostosowanie hello skrypt jest uruchamiany.</span><span class="sxs-lookup"><span data-stu-id="e4333-309">Specify hello nodes (**Head**, **Worker**, or **ZooKeeper**) on which hello customization script is run.</span></span> |
    | <span data-ttu-id="e4333-310">Parametry</span><span class="sxs-lookup"><span data-stu-id="e4333-310">Parameters</span></span> |<span data-ttu-id="e4333-311">Określ parametry hello, jeśli są wymagane przez skrypt hello.</span><span class="sxs-lookup"><span data-stu-id="e4333-311">Specify hello parameters, if required by hello script.</span></span> |

    <span data-ttu-id="e4333-312">Użyj hello __Utrwal tę akcję skryptu__ wpis toomake się, że skrypt hello jest stosowany podczas operacji skalowania.</span><span class="sxs-lookup"><span data-stu-id="e4333-312">Use hello __Persist this script action__ entry toomake sure hello script is applied during scaling operations.</span></span>

5. <span data-ttu-id="e4333-313">Na koniec użyj hello **Utwórz** przycisk tooapply hello skryptu toohello klastra.</span><span class="sxs-lookup"><span data-stu-id="e4333-313">Finally, use hello **Create** button tooapply hello script toohello cluster.</span></span>

### <a name="apply-a-script-action-tooa-running-cluster-from-azure-powershell"></a><span data-ttu-id="e4333-314">Zastosuj tooa akcji skryptu, uruchamiając klastra z programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e4333-314">Apply a Script Action tooa running cluster from Azure PowerShell</span></span>

<span data-ttu-id="e4333-315">Przed kontynuowaniem upewnij się, zainstalowaniu i skonfigurowaniu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e4333-315">Before proceeding, make sure you have installed and configured Azure PowerShell.</span></span> <span data-ttu-id="e4333-316">Aby uzyskać informacji na temat konfigurowania stacji roboczej toorun poleceń cmdlet programu PowerShell w usłudze HDInsight, zobacz [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e4333-316">For information about configuring a workstation toorun HDInsight PowerShell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="e4333-317">Witaj poniższym przykładzie pokazano, jak tooapply klastra uruchomione tooa akcji skryptu:</span><span class="sxs-lookup"><span data-stu-id="e4333-317">hello following example demonstrates how tooapply a script action tooa running cluster:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=105-117)]

<span data-ttu-id="e4333-318">Po zakończeniu operacji hello, pojawi się informacji toohello podobne następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="e4333-318">Once hello operation completes, you receive information similar toohello following text:</span></span>

    OperationState  : Succeeded
    ErrorMessage    :
    Name            : Giraph
    Uri             : https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh
    Parameters      :
    NodeTypes       : {HeadNode, WorkerNode}

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-azure-cli"></a><span data-ttu-id="e4333-319">Zastosuj tooa akcji skryptu, uruchamiając klastra z hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e4333-319">Apply a Script Action tooa running cluster from hello Azure CLI</span></span>

<span data-ttu-id="e4333-320">Przed kontynuowaniem upewnij się, zostanie zainstalowany i skonfigurowany hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e4333-320">Before proceeding, make sure you have installed and configured hello Azure CLI.</span></span> <span data-ttu-id="e4333-321">Aby uzyskać więcej informacji, zobacz [hello instalowanie interfejsu wiersza polecenia Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="e4333-321">For more information, see [Install hello Azure CLI](../cli-install-nodejs.md).</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. <span data-ttu-id="e4333-322">tooAzure tooswitch tryb usługi Resource Manager, użyj hello następujące polecenie w wierszu polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="e4333-322">tooswitch tooAzure Resource Manager mode, use hello following command at hello command line:</span></span>

        azure config mode arm

2. <span data-ttu-id="e4333-323">Użyj powitania po tooyour tooauthenticate subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e4333-323">Use hello following tooauthenticate tooyour Azure subscription.</span></span>

        azure login

3. <span data-ttu-id="e4333-324">Użyj hello następujące polecenia tooapply tooa akcji skryptu, z klastra</span><span class="sxs-lookup"><span data-stu-id="e4333-324">Use hello following command tooapply a script action tooa running cluster</span></span>

        azure hdinsight script-action create <clustername> -g <resourcegroupname> -n <scriptname> -u <scriptURI> -t <nodetypes>

    <span data-ttu-id="e4333-325">W przypadku pominięcia parametrów dla tego polecenia, zostanie wyświetlony monit o ich.</span><span class="sxs-lookup"><span data-stu-id="e4333-325">If you omit parameters for this command, you are prompted for them.</span></span> <span data-ttu-id="e4333-326">Jeśli hello skryptu z `-u` akceptuje parametry, można określić je przy użyciu hello `-p` parametru.</span><span class="sxs-lookup"><span data-stu-id="e4333-326">If hello script you specify with `-u` accepts parameters, you can specify them using hello `-p` parameter.</span></span>

    <span data-ttu-id="e4333-327">Nieprawidłowy węzeł typy `headnode`, `workernode`, i `zookeeper`.</span><span class="sxs-lookup"><span data-stu-id="e4333-327">Valid node types are `headnode`, `workernode`, and `zookeeper`.</span></span> <span data-ttu-id="e4333-328">Jeśli skrypt hello powinno być zastosowane toomultiple typy węzłów, określić typy hello oddzielone ";".</span><span class="sxs-lookup"><span data-stu-id="e4333-328">If hello script should be applied toomultiple node types, specify hello types separated by a ';'.</span></span> <span data-ttu-id="e4333-329">Na przykład `-n headnode;workernode`.</span><span class="sxs-lookup"><span data-stu-id="e4333-329">For example, `-n headnode;workernode`.</span></span>

    <span data-ttu-id="e4333-330">toopersist hello skryptu, Dodaj hello `--persistOnSuccess`.</span><span class="sxs-lookup"><span data-stu-id="e4333-330">toopersist hello script, add hello `--persistOnSuccess`.</span></span> <span data-ttu-id="e4333-331">Można również utrwalić skryptu hello później za pomocą `azure hdinsight script-action persisted set`.</span><span class="sxs-lookup"><span data-stu-id="e4333-331">You can also persist hello script later by using `azure hdinsight script-action persisted set`.</span></span>

    <span data-ttu-id="e4333-332">Po zakończeniu zadania hello, pojawi się toohello podobne dane wyjściowe następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="e4333-332">Once hello job completes, you receive output similar toohello following text:</span></span>

        info:    Executing command hdinsight script-action create
        + Executing Script Action on HDInsight cluster
        data:    Operation Info
        data:    ---------------
        data:    Operation status:
        data:    Operation ID:  b707b10e-e633-45c0-baa9-8aed3d348c13
        info:    hdinsight script-action create command OK

### <a name="apply-a-script-action-tooa-running-cluster-using-rest-api"></a><span data-ttu-id="e4333-333">Zastosuj tooa akcji skryptu, systemem klastra przy użyciu interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="e4333-333">Apply a Script Action tooa running cluster using REST API</span></span>

<span data-ttu-id="e4333-334">Zobacz [uruchomienia akcji skryptu w klastrze uruchomione](https://msdn.microsoft.com/library/azure/mt668441.aspx).</span><span class="sxs-lookup"><span data-stu-id="e4333-334">See [Run Script Actions on a running cluster](https://msdn.microsoft.com/library/azure/mt668441.aspx).</span></span>

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-hdinsight-net-sdk"></a><span data-ttu-id="e4333-335">Zastosuj tooa akcji skryptu, uruchamiając klastra z hello zestawu .NET SDK usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="e4333-335">Apply a Script Action tooa running cluster from hello HDInsight .NET SDK</span></span>

<span data-ttu-id="e4333-336">Na przykład przy użyciu hello zestawu .NET SDK tooapply skrypty tooa klastra, zobacz [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span><span class="sxs-lookup"><span data-stu-id="e4333-336">For an example of using hello .NET SDK tooapply scripts tooa cluster, see [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span></span>

## <a name="view-history-promote-and-demote-script-actions"></a><span data-ttu-id="e4333-337">Wyświetlanie historii, wspierania i obniżyć poziom akcji skryptu</span><span class="sxs-lookup"><span data-stu-id="e4333-337">View history, promote, and demote Script Actions</span></span>

### <a name="using-hello-azure-portal"></a><span data-ttu-id="e4333-338">Przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="e4333-338">Using hello Azure portal</span></span>

1. <span data-ttu-id="e4333-339">Z hello [portalu Azure](https://portal.azure.com), wybierz z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e4333-339">From hello [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span>

2. <span data-ttu-id="e4333-340">Omówienie klastrów HDInsight hello, zaznacz hello **akcji skryptu** kafelka.</span><span class="sxs-lookup"><span data-stu-id="e4333-340">From hello HDInsight cluster overview, select hello **Script Actions** tile.</span></span>

    ![Kafelek akcji skryptu](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > <span data-ttu-id="e4333-342">Możesz też wybrać **wszystkie ustawienia** , a następnie wybierz **akcji skryptu** z hello w sekcji Ustawienia.</span><span class="sxs-lookup"><span data-stu-id="e4333-342">You can also select **All settings** and then select **Script Actions** from hello Settings section.</span></span>

4. <span data-ttu-id="e4333-343">Historia skryptów dla tego klastra jest wyświetlany na powitania sekcji akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="e4333-343">A history of scripts for this cluster is displayed on hello Script Actions section.</span></span> <span data-ttu-id="e4333-344">Informacje te obejmują listę utrwalonych skryptów.</span><span class="sxs-lookup"><span data-stu-id="e4333-344">This information includes a list of persisted scripts.</span></span> <span data-ttu-id="e4333-345">Poniższy zrzut ekranu hello zawiera ten powitalne Solr skryptu zostało uruchomione w tym klastrze.</span><span class="sxs-lookup"><span data-stu-id="e4333-345">In hello screenshot below, you can see that hello Solr script has been ran on this cluster.</span></span> <span data-ttu-id="e4333-346">Zrzut ekranu Hello nie są wyświetlane wszystkie skrypty utrwalonych.</span><span class="sxs-lookup"><span data-stu-id="e4333-346">hello screenshot does not show any persisted scripts.</span></span>

    ![Sekcji działania skryptu](./media/hdinsight-hadoop-customize-cluster-linux/script-action-history.png)

5. <span data-ttu-id="e4333-348">Wybranie skryptu z historii hello powoduje wyświetlenie sekcja właściwości hello w ramach tego skryptu.</span><span class="sxs-lookup"><span data-stu-id="e4333-348">Selecting a script from hello history displays hello Properties section for this script.</span></span> <span data-ttu-id="e4333-349">Z góry hello ekranu hello można ponownie uruchomić skrypt hello lub Podwyższ go.</span><span class="sxs-lookup"><span data-stu-id="e4333-349">From hello top of hello screen, you can rerun hello script or promote it.</span></span>

    ![Właściwości działania skryptu](./media/hdinsight-hadoop-customize-cluster-linux/promote-script-actions.png)

6. <span data-ttu-id="e4333-351">Można również użyć hello **...**  toohello prawo do wpisów na powitania akcji skryptu sekcji tooperform akcje.</span><span class="sxs-lookup"><span data-stu-id="e4333-351">You can also use hello **...** toohello right of entries on hello Script Actions section tooperform actions.</span></span>

    ![Skrypt akcje... użycia](./media/hdinsight-hadoop-customize-cluster-linux/deletepromoted.png)

### <a name="using-azure-powershell"></a><span data-ttu-id="e4333-353">Korzystanie z programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e4333-353">Using Azure PowerShell</span></span>

| <span data-ttu-id="e4333-354">Użyj następujących hello...</span><span class="sxs-lookup"><span data-stu-id="e4333-354">Use hello following...</span></span> | <span data-ttu-id="e4333-355">zbyt...</span><span class="sxs-lookup"><span data-stu-id="e4333-355">too...</span></span> |
| --- | --- |
| <span data-ttu-id="e4333-356">Get-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="e4333-356">Get-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="e4333-357">Pobieranie informacji na temat akcji utrwalonego skryptu</span><span class="sxs-lookup"><span data-stu-id="e4333-357">Retrieve information on persisted script actions</span></span> |
| <span data-ttu-id="e4333-358">Get-AzureRmHDInsightScriptActionHistory</span><span class="sxs-lookup"><span data-stu-id="e4333-358">Get-AzureRmHDInsightScriptActionHistory</span></span> |<span data-ttu-id="e4333-359">Pobierz historię skryptu akcje zastosowane toohello klastra lub szczegółów dla określonego skryptu</span><span class="sxs-lookup"><span data-stu-id="e4333-359">Retrieve a history of script actions applied toohello cluster, or details for a specific script</span></span> |
| <span data-ttu-id="e4333-360">Set-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="e4333-360">Set-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="e4333-361">Zamienia ad hoc tooa akcji skryptów trwale akcji skryptu</span><span class="sxs-lookup"><span data-stu-id="e4333-361">Promotes an ad hoc script action tooa persisted script action</span></span> |
| <span data-ttu-id="e4333-362">Remove-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="e4333-362">Remove-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="e4333-363">Przenosi akcji ad hoc tooan akcji utrwalonego skryptu</span><span class="sxs-lookup"><span data-stu-id="e4333-363">Demotes a persisted script action tooan ad hoc action</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="e4333-364">Przy użyciu `Remove-AzureRmHDInsightPersistedScriptAction` nie cofa hello akcje wykonywane przez skrypt.</span><span class="sxs-lookup"><span data-stu-id="e4333-364">Using `Remove-AzureRmHDInsightPersistedScriptAction` does not undo hello actions performed by a script.</span></span> <span data-ttu-id="e4333-365">To polecenie cmdlet usuwa tylko hello utrwalonego flagę.</span><span class="sxs-lookup"><span data-stu-id="e4333-365">This cmdlet only removes hello persisted flag.</span></span>

<span data-ttu-id="e4333-366">powitania po przykładowy skrypt pokazuje przy użyciu hello toopromote poleceń cmdlet, a następnie obniżenia poziomu skryptu.</span><span class="sxs-lookup"><span data-stu-id="e4333-366">hello following example script demonstrates using hello cmdlets toopromote, then demote a script.</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=123-140)]

### <a name="using-hello-azure-cli"></a><span data-ttu-id="e4333-367">Przy użyciu hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e4333-367">Using hello Azure CLI</span></span>

| <span data-ttu-id="e4333-368">Użyj następujących hello...</span><span class="sxs-lookup"><span data-stu-id="e4333-368">Use hello following...</span></span> | <span data-ttu-id="e4333-369">zbyt...</span><span class="sxs-lookup"><span data-stu-id="e4333-369">too...</span></span> |
| --- | --- |
| `azure hdinsight script-action persisted list <clustername>` |<span data-ttu-id="e4333-370">Pobierz listę akcji utrwalonego skryptu</span><span class="sxs-lookup"><span data-stu-id="e4333-370">Retrieve a list of persisted script actions</span></span> |
| `azure hdinsight script-action persisted show <clustername> <scriptname>` |<span data-ttu-id="e4333-371">Pobieranie informacji na temat akcji określonych utrwalonego skryptu</span><span class="sxs-lookup"><span data-stu-id="e4333-371">Retrieve information on a specific persisted script action</span></span> |
| `azure hdinsight script-action history list <clustername>` |<span data-ttu-id="e4333-372">Pobierz historię skryptu akcje zastosowane toohello klastra</span><span class="sxs-lookup"><span data-stu-id="e4333-372">Retrieve a history of script actions applied toohello cluster</span></span> |
| `azure hdinsight script-action history show <clustername> <scriptname>` |<span data-ttu-id="e4333-373">Pobieranie informacji na temat działań określonego skryptu</span><span class="sxs-lookup"><span data-stu-id="e4333-373">Retrieve information on a specific script action</span></span> |
| `azure hdinsight script action persisted set <clustername> <scriptexecutionid>` |<span data-ttu-id="e4333-374">Zamienia ad hoc tooa akcji skryptów trwale akcji skryptu</span><span class="sxs-lookup"><span data-stu-id="e4333-374">Promotes an ad hoc script action tooa persisted script action</span></span> |
| `azure hdinsight script-action persisted delete <clustername> <scriptname>` |<span data-ttu-id="e4333-375">Przenosi akcji ad hoc tooan akcji utrwalonego skryptu</span><span class="sxs-lookup"><span data-stu-id="e4333-375">Demotes a persisted script action tooan ad hoc action</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="e4333-376">Przy użyciu `azure hdinsight script-action persisted delete` nie cofa hello akcje wykonywane przez skrypt.</span><span class="sxs-lookup"><span data-stu-id="e4333-376">Using `azure hdinsight script-action persisted delete` does not undo hello actions performed by a script.</span></span> <span data-ttu-id="e4333-377">To polecenie cmdlet usuwa tylko hello utrwalonego flagę.</span><span class="sxs-lookup"><span data-stu-id="e4333-377">This cmdlet only removes hello persisted flag.</span></span>

### <a name="using-hello-hdinsight-net-sdk"></a><span data-ttu-id="e4333-378">Przy użyciu zestawu .NET SDK HDInsight hello</span><span class="sxs-lookup"><span data-stu-id="e4333-378">Using hello HDInsight .NET SDK</span></span>

<span data-ttu-id="e4333-379">Na przykład za pomocą historii hello zestawu .NET SDK tooretrieve skryptu z klastra, podwyższyć poziom lub obniżyć poziom skryptów, zobacz [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span><span class="sxs-lookup"><span data-stu-id="e4333-379">For an example of using hello .NET SDK tooretrieve script history from a cluster, promote or demote scripts, see [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span></span>

> [!NOTE]
> <span data-ttu-id="e4333-380">Również w przykładzie pokazano, jak tooinstall aplikacji usługi HDInsight przy użyciu hello zestawu .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="e4333-380">This example also demonstrates how tooinstall an HDInsight application using hello .NET SDK.</span></span>

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a><span data-ttu-id="e4333-381">Obsługa oprogramowania typu open source używane w klastrach HDInsight</span><span class="sxs-lookup"><span data-stu-id="e4333-381">Support for open-source software used on HDInsight clusters</span></span>

<span data-ttu-id="e4333-382">Witaj usługi Microsoft Azure HDInsight używa ekosystem technologii open source utworzona wokół Hadoop.</span><span class="sxs-lookup"><span data-stu-id="e4333-382">hello Microsoft Azure HDInsight service uses an ecosystem of open-source technologies formed around Hadoop.</span></span> <span data-ttu-id="e4333-383">Microsoft Azure udostępnia ogólnego poziomu wsparcia dla technologii open source.</span><span class="sxs-lookup"><span data-stu-id="e4333-383">Microsoft Azure provides a general level of support for open-source technologies.</span></span> <span data-ttu-id="e4333-384">Aby uzyskać więcej informacji, zobacz hello **zakres obsługi** sekcji hello [witryny sieci Web pomocy technicznej platformy Azure — często zadawane pytania](https://azure.microsoft.com/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="e4333-384">For more information, see hello **Support Scope** section of hello [Azure Support FAQ website](https://azure.microsoft.com/support/faq/).</span></span> <span data-ttu-id="e4333-385">Witaj usługa HDInsight zapewnia dodatkowy poziom obsługi wbudowanych składników.</span><span class="sxs-lookup"><span data-stu-id="e4333-385">hello HDInsight service provides an additional level of support for built-in components.</span></span>

<span data-ttu-id="e4333-386">Istnieją dwa typy składników open source, które są dostępne w hello usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="e4333-386">There are two types of open-source components that are available in hello HDInsight service:</span></span>

* <span data-ttu-id="e4333-387">**Wbudowanych składników** — te składniki są wstępnie zainstalowane w klastrach HDInsight i podaj podstawowych funkcji programu hello klastra.</span><span class="sxs-lookup"><span data-stu-id="e4333-387">**Built-in components** - These components are pre-installed on HDInsight clusters and provide core functionality of hello cluster.</span></span> <span data-ttu-id="e4333-388">Na przykład YARN ResourceManager, język zapytań Hive hello (HiveQL) i biblioteki Mahout hello należy toothis kategorii.</span><span class="sxs-lookup"><span data-stu-id="e4333-388">For example, YARN ResourceManager, hello Hive query language (HiveQL), and hello Mahout library belong toothis category.</span></span> <span data-ttu-id="e4333-389">Pełna lista składniki klastra jest dostępna w [nowości w wersjach klastra Hadoop hello dostarczanych z usługą HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="e4333-389">A full list of cluster components is available in [What's new in hello Hadoop cluster versions provided by HDInsight](hdinsight-component-versioning.md).</span></span>
* <span data-ttu-id="e4333-390">**Niestandardowe składniki** -, jako użytkownik hello klastra, można zainstalować lub użyć w obciążenie jakiegokolwiek składnika dostępne w społeczności hello lub utworzone przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e4333-390">**Custom components** - You, as a user of hello cluster, can install or use in your workload any component available in hello community or created by you.</span></span>

> [!WARNING]
> <span data-ttu-id="e4333-391">Składniki dostarczony z klastrem usługi HDInsight hello są w pełni obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="e4333-391">Components provided with hello HDInsight cluster are fully supported.</span></span> <span data-ttu-id="e4333-392">Microsoft Support pomaga tooisolate i rozwiąż problemy toothese powiązane składniki.</span><span class="sxs-lookup"><span data-stu-id="e4333-392">Microsoft Support helps tooisolate and resolve issues related toothese components.</span></span>
>
> <span data-ttu-id="e4333-393">Niestandardowe składniki odbierania toohelp Obsługa uzasadnione ekonomicznie toofurther należy rozwiązać problem hello.</span><span class="sxs-lookup"><span data-stu-id="e4333-393">Custom components receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="e4333-394">Pomocy technicznej firmy Microsoft może być możliwe tooresolve hello problem lub ich może zapytać tooengage dostępne kanały o technologiach typu open source hello wykryto głębokie doświadczenia z tej technologii.</span><span class="sxs-lookup"><span data-stu-id="e4333-394">Microsoft support may be able tooresolve hello issue OR they may ask you tooengage available channels for hello open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="e4333-395">Na przykład istnieje wiele witryn społeczności, które mogą być używane, takie jak: [forum MSDN dla usługi HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Projekty Apache mieć witryny projektu na [http://apache.org](http://apache.org), na przykład: [Hadoop](http://hadoop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="e4333-395">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>

<span data-ttu-id="e4333-396">Witaj usługi HDInsight udostępnia kilka metod toouse niestandardowych składników.</span><span class="sxs-lookup"><span data-stu-id="e4333-396">hello HDInsight service provides several ways toouse custom components.</span></span> <span data-ttu-id="e4333-397">Witaj, który dotyczy tego samego poziomu wsparcia, niezależnie od tego, jak używać lub zainstalowany w klastrze hello składnika.</span><span class="sxs-lookup"><span data-stu-id="e4333-397">hello same level of support applies, regardless of how a component is used or installed on hello cluster.</span></span> <span data-ttu-id="e4333-398">Witaj Poniższa lista zawiera opis hello Najczęstszym z niestandardowych składników można używać w klastrach HDInsight:</span><span class="sxs-lookup"><span data-stu-id="e4333-398">hello following list describes hello most common ways that custom components can be used on HDInsight clusters:</span></span>

1. <span data-ttu-id="e4333-399">Przesyłanie zadań — usługi Hadoop i innych typów zadań, które wykonać albo użyć niestandardowych składników mogą być przesłane toohello klastra.</span><span class="sxs-lookup"><span data-stu-id="e4333-399">Job submission - Hadoop or other types of jobs that execute or use custom components can be submitted toohello cluster.</span></span>

2. <span data-ttu-id="e4333-400">Dostosowywanie klastra — podczas tworzenia klastra, można określić dodatkowe ustawienia i niestandardowe składniki, które są zainstalowane na węzłach klastra hello.</span><span class="sxs-lookup"><span data-stu-id="e4333-400">Cluster customization - During cluster creation, you can specify additional settings and custom components that are installed on hello cluster nodes.</span></span>

3. <span data-ttu-id="e4333-401">Próbek - dla popularnych niestandardowych składników, firma Microsoft i inne osoby mogą powodować przykłady sposobu użycia tych składników na powitania klastrów usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e4333-401">Samples - For popular custom components, Microsoft and others may provide samples of how these components can be used on hello HDInsight clusters.</span></span> <span data-ttu-id="e4333-402">Te przykłady są udostępniane bez obsługi.</span><span class="sxs-lookup"><span data-stu-id="e4333-402">These samples are provided without support.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="e4333-403">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="e4333-403">Troubleshooting</span></span>

<span data-ttu-id="e4333-404">Można użyć narzędzia Ambari web interfejsu użytkownika tooview informacji rejestrowanych przez akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="e4333-404">You can use Ambari web UI tooview information logged by script actions.</span></span> <span data-ttu-id="e4333-405">W przypadku niepowodzenia podczas tworzenia klastra skryptu hello hello dzienniki dostępne są również hello domyślnego konta magazynu skojarzone z klastrem hello.</span><span class="sxs-lookup"><span data-stu-id="e4333-405">If hello script fails during cluster creation, hello logs are also available in hello default storage account associated with hello cluster.</span></span> <span data-ttu-id="e4333-406">Ta sekcja zawiera informacje dotyczące sposobu tooretrieve hello logowania za pomocą obu tych opcji.</span><span class="sxs-lookup"><span data-stu-id="e4333-406">This section provides information on how tooretrieve hello logs using both these options.</span></span>

### <a name="using-hello-ambari-web-ui"></a><span data-ttu-id="e4333-407">Przy użyciu hello Interfejsu sieci Web Ambari</span><span class="sxs-lookup"><span data-stu-id="e4333-407">Using hello Ambari Web UI</span></span>

1. <span data-ttu-id="e4333-408">W przeglądarce Przejdź toohttps://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="e4333-408">In your browser, navigate toohttps://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="e4333-409">Zamień NAZWAKLASTRA hello nazwę klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e4333-409">Replace CLUSTERNAME with hello name of your HDInsight cluster.</span></span>

    <span data-ttu-id="e4333-410">Po wyświetleniu monitu wprowadź nazwę konta administratora hello (Administrator) i hasło klastra hello.</span><span class="sxs-lookup"><span data-stu-id="e4333-410">When prompted, enter hello admin account name (admin) and password for hello cluster.</span></span> <span data-ttu-id="e4333-411">Masz poświadczenia administratora hello tooreenter w formularzu sieci web.</span><span class="sxs-lookup"><span data-stu-id="e4333-411">You may have tooreenter hello admin credentials in a web form.</span></span>

2. <span data-ttu-id="e4333-412">Pasek hello u góry strony hello hello, zaznacz hello **ops** wpisu.</span><span class="sxs-lookup"><span data-stu-id="e4333-412">From hello bar at hello top of hello page, select hello **ops** entry.</span></span> <span data-ttu-id="e4333-413">Zostanie wyświetlona lista bieżące i poprzednie operacje wykonywane na powitania klastra za pomocą narzędzia Ambari.</span><span class="sxs-lookup"><span data-stu-id="e4333-413">A list of current and previous operations performed on hello cluster through Ambari is displayed.</span></span>

    ![Pasek interfejsu użytkownika sieci web Ambari z ops wybrane](./media/hdinsight-hadoop-customize-cluster-linux/ambari-nav.png)

3. <span data-ttu-id="e4333-415">Znajdź hello wpisów, które mają **Uruchom\_customscriptaction** w hello **operacji** kolumny.</span><span class="sxs-lookup"><span data-stu-id="e4333-415">Find hello entries that have **run\_customscriptaction** in hello **Operations** column.</span></span> <span data-ttu-id="e4333-416">Te wpisy są tworzone przy uruchamianiu hello akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="e4333-416">These entries are created when hello Script Actions run.</span></span>

    ![Zrzut ekranu przedstawiający operacji](./media/hdinsight-hadoop-customize-cluster-linux/ambariscriptaction.png)

    <span data-ttu-id="e4333-418">tooview hello STDOUT i STDERR dane wyjściowe, wybierz wpis run\customscriptaction hello i przejść za pośrednictwem łącza hello.</span><span class="sxs-lookup"><span data-stu-id="e4333-418">tooview hello STDOUT and STDERR output, select hello run\customscriptaction entry and drill down through hello links.</span></span> <span data-ttu-id="e4333-419">Te dane wyjściowe jest generowany po uruchomieniu skryptu hello i mogą zawierać przydatne informacje.</span><span class="sxs-lookup"><span data-stu-id="e4333-419">This output is generated when hello script runs, and may contain useful information.</span></span>

### <a name="access-logs-from-hello-default-storage-account"></a><span data-ttu-id="e4333-420">Dzienniki dostępu z hello domyślne konto magazynu</span><span class="sxs-lookup"><span data-stu-id="e4333-420">Access logs from hello default storage account</span></span>

<span data-ttu-id="e4333-421">W przypadku niepowodzenia tworzenia klastra hello ze względu na błąd akcji skryptu tooa hello dzienniki są dostępne z konta magazynu klastra hello.</span><span class="sxs-lookup"><span data-stu-id="e4333-421">If hello cluster creation fails due tooa script action error, hello logs can be accessed from hello cluster storage account.</span></span>

* <span data-ttu-id="e4333-422">Witaj dzienniki magazynu są dostępne pod adresem `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`.</span><span class="sxs-lookup"><span data-stu-id="e4333-422">hello storage logs are available at `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`.</span></span>

    ![Zrzut ekranu przedstawiający operacji](./media/hdinsight-hadoop-customize-cluster-linux/script_action_logs_in_storage.png)

    <span data-ttu-id="e4333-424">W tym katalogu dzienników hello są zorganizowane oddzielnie headnode, workernode i węzły dozorcy.</span><span class="sxs-lookup"><span data-stu-id="e4333-424">Under this directory, hello logs are organized separately for headnode, workernode, and zookeeper nodes.</span></span> <span data-ttu-id="e4333-425">Przykłady to:</span><span class="sxs-lookup"><span data-stu-id="e4333-425">Some examples are:</span></span>

    * <span data-ttu-id="e4333-426">**Headnode** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="e4333-426">**Headnode** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`</span></span>

    * <span data-ttu-id="e4333-427">**Węzła procesu roboczego** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="e4333-427">**Worker node** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`</span></span>

    * <span data-ttu-id="e4333-428">**Węzeł dozorcy** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="e4333-428">**Zookeeper node** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`</span></span>

* <span data-ttu-id="e4333-429">Wszystkie stdout i stderr hello odpowiedniego hosta jest przekazywane toohello konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="e4333-429">All stdout and stderr of hello corresponding host is uploaded toohello storage account.</span></span> <span data-ttu-id="e4333-430">Istnieje **dane wyjściowe -\*.txt** i **błędy -\*.txt** dla każdej akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="e4333-430">There is one **output-\*.txt** and **errors-\*.txt** for each script action.</span></span> <span data-ttu-id="e4333-431">Plik wyjściowy *.txt Hello zawiera informacje o hello identyfikatora URI hello skryptu, który został uruchomiony na hoście hello.</span><span class="sxs-lookup"><span data-stu-id="e4333-431">hello output-*.txt file contains information about hello URI of hello script that got run on hello host.</span></span> <span data-ttu-id="e4333-432">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="e4333-432">For example</span></span>

        'Start downloading script locally: ', u'https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh'

* <span data-ttu-id="e4333-433">Istnieje możliwość wielokrotnie utworzyć klaster akcji skryptu z hello tej samej nazwy.</span><span class="sxs-lookup"><span data-stu-id="e4333-433">It's possible that you repeatedly create a script action cluster with hello same name.</span></span> <span data-ttu-id="e4333-434">W takim przypadku można odróżnić hello dzienniki odpowiednie na podstawie nazwy folderu Data hello.</span><span class="sxs-lookup"><span data-stu-id="e4333-434">In such case, you can distinguish hello relevant logs based on hello DATE folder name.</span></span> <span data-ttu-id="e4333-435">Na przykład hello struktura folderów dla klastra (mycluster) utworzone w różnych terminach zostaną wyświetlone podobne toohello następujące wpisy dziennika:</span><span class="sxs-lookup"><span data-stu-id="e4333-435">For example, hello folder structure for a cluster (mycluster) created on different dates appears similar toohello following log entries:</span></span>

    <span data-ttu-id="e4333-436">`\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04` `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`</span><span class="sxs-lookup"><span data-stu-id="e4333-436">`\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04` `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`</span></span>

* <span data-ttu-id="e4333-437">Po utworzeniu klastra akcji skryptu z hello sama nazwa na powitania sam dzień, można użyć hello unikatowy prefiks tooidentify hello odpowiednich plików dziennika.</span><span class="sxs-lookup"><span data-stu-id="e4333-437">If you create a script action cluster with hello same name on hello same day, you can use hello unique prefix tooidentify hello relevant log files.</span></span>

* <span data-ttu-id="e4333-438">Po utworzeniu klastra w pobliżu 00:00:00 (północ), jest to możliwe, że pliki dziennika hello obejmują przez dwa dni.</span><span class="sxs-lookup"><span data-stu-id="e4333-438">If you create a cluster near 12:00AM (midnight), it's possible that hello log files span across two days.</span></span> <span data-ttu-id="e4333-439">W takich przypadkach, zobacz dwa foldery inną datę dla hello tego samego klastra.</span><span class="sxs-lookup"><span data-stu-id="e4333-439">In such cases, you see two different date folders for hello same cluster.</span></span>

* <span data-ttu-id="e4333-440">Przekazywanie dzienników pliki toohello domyślny kontener może potrwać too5 min, zwłaszcza w przypadku dużych klastrów.</span><span class="sxs-lookup"><span data-stu-id="e4333-440">Uploading log files toohello default container can take up too5 mins, especially for large clusters.</span></span> <span data-ttu-id="e4333-441">Tak Jeśli chcesz tooaccess hello dzienniki, nie należy natychmiast usuwać klastra hello Jeśli zawodzi Akcja skryptu.</span><span class="sxs-lookup"><span data-stu-id="e4333-441">So, if you want tooaccess hello logs, you should not immediately delete hello cluster if a script action fails.</span></span>

### <a name="ambari-watchdog"></a><span data-ttu-id="e4333-442">Ambari programu alarmowego</span><span class="sxs-lookup"><span data-stu-id="e4333-442">Ambari watchdog</span></span>

> [!WARNING]
> <span data-ttu-id="e4333-443">Nie należy zmieniać hasła hello hello Ambari programu alarmowego (hdinsightwatchdog) w klastrze usługi HDInsight opartej na systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="e4333-443">Do not change hello password for hello Ambari Watchdog (hdinsightwatchdog) on your Linux-based HDInsight cluster.</span></span> <span data-ttu-id="e4333-444">Zmiany hasła hello na tym koncie dzieli hello możliwości toorun nowych skrypt akcji w klastrze usługi HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="e4333-444">Changing hello password for this account breaks hello ability toorun new script actions on hello HDInsight cluster.</span></span>

### <a name="cant-import-name-blobservice"></a><span data-ttu-id="e4333-445">Nie można zaimportować nazwa BlobService</span><span class="sxs-lookup"><span data-stu-id="e4333-445">Can't import name BlobService</span></span>

<span data-ttu-id="e4333-446">__Objawy__: hello skryptu kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="e4333-446">__Symptoms__: hello script action fails.</span></span> <span data-ttu-id="e4333-447">Tekst toohello podobne następujący błąd jest wyświetlany podczas przeglądania operacji hello w Ambari:</span><span class="sxs-lookup"><span data-stu-id="e4333-447">Text similar toohello following error is displayed when you view hello operation in Ambari:</span></span>

```
Traceback (most recent call list):
  File "/var/lib/ambari-agent/cache/custom_actions/scripts/run_customscriptaction.py", line 21, in <module>
    from azure.storage.blob import BlobService
ImportError: cannot import name BlobService
```

<span data-ttu-id="e4333-448">__Przyczyna__: ten błąd występuje podczas uaktualniania klienta magazynu Azure Python hello, dostępnej z klastrem usługi HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="e4333-448">__Cause__: This error occurs if you upgrade hello Python Azure Storage client that is included with hello HDInsight cluster.</span></span> <span data-ttu-id="e4333-449">HDInsight oczekuje klienta usługi Azure Storage 0.20.0.</span><span class="sxs-lookup"><span data-stu-id="e4333-449">HDInsight expects Azure Storage client 0.20.0.</span></span>

<span data-ttu-id="e4333-450">__Rozdzielczość__: tooresolve ten błąd, ręcznie połączyć za pomocą węzła klastra tooeach `ssh` i hello Użyj następującego polecenia tooreinstall hello poprawne magazynu klient w wersji:</span><span class="sxs-lookup"><span data-stu-id="e4333-450">__Resolution__: tooresolve this error, manually connect tooeach cluster node using `ssh` and use hello following command tooreinstall hello correct storage client version:</span></span>

```
sudo pip install azure-storage==0.20.0
```

<span data-ttu-id="e4333-451">Aby uzyskać informacji na temat łączenia toohello klastra przy użyciu protokołu SSH, zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="e4333-451">For information on connecting toohello cluster with SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

### <a name="history-doesnt-show-scripts-used-during-cluster-creation"></a><span data-ttu-id="e4333-452">Historia nie wyświetla skrypty używane podczas tworzenia klastra</span><span class="sxs-lookup"><span data-stu-id="e4333-452">History doesn't show scripts used during cluster creation</span></span>

<span data-ttu-id="e4333-453">Jeśli klaster został utworzony przed 15 marca 2016 r nie miało wpis w historii akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="e4333-453">If your cluster was created before March 15, 2016, you may not see an entry in Script Action history.</span></span> <span data-ttu-id="e4333-454">Jeśli rozmiar klastra powitania po 15 marca 2016 r skrypty hello przy użyciu podczas tworzenia klastra pojawiają się w historii zgodnie z ich stosowania toonew węzłów w klastrze hello jako część hello operacja zmiany rozmiaru.</span><span class="sxs-lookup"><span data-stu-id="e4333-454">If you resize hello cluster after March 15, 2016, hello scripts using during cluster creation appear in history as they are applied toonew nodes in hello cluster as part of hello resize operation.</span></span>

<span data-ttu-id="e4333-455">Istnieją jednak dwa wyjątki:</span><span class="sxs-lookup"><span data-stu-id="e4333-455">There are two exceptions:</span></span>

* <span data-ttu-id="e4333-456">Jeśli klaster został utworzony przed 1 września 2015 r.</span><span class="sxs-lookup"><span data-stu-id="e4333-456">If your cluster was created before September 1, 2015.</span></span> <span data-ttu-id="e4333-457">Ta data jest w przypadku akcji skryptu zostały wprowadzone.</span><span class="sxs-lookup"><span data-stu-id="e4333-457">This date is when Script Actions were introduced.</span></span> <span data-ttu-id="e4333-458">Dowolnego klastra utworzone przed tą datą nie ma użyć akcji skryptu do tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="e4333-458">Any cluster created before this date could not have used Script Actions for cluster creation.</span></span>

* <span data-ttu-id="e4333-459">Jeśli można użyć wielu akcji skryptu podczas tworzenia klastra i hello tej samej nazwy dla wielu skryptów lub hello takie same nazwy, tym samym identyfikatorze URI, ale różne parametry dla wielu skryptów.</span><span class="sxs-lookup"><span data-stu-id="e4333-459">If you used multiple Script Actions during cluster creation, and used hello same name for multiple scripts, or hello same name, same URI, but different parameters for multiple scripts.</span></span> <span data-ttu-id="e4333-460">W takich przypadkach jest wyświetlany hello następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="e4333-460">In these cases, you receive hello following error:</span></span>

    <span data-ttu-id="e4333-461">Skryptu nowych akcji może być uruchomione w tym klastrze powodu tooconflicting skryptu nazw w istniejących skryptów.</span><span class="sxs-lookup"><span data-stu-id="e4333-461">No new script actions can be ran on this cluster due tooconflicting script names in existing scripts.</span></span> <span data-ttu-id="e4333-462">Nazwy skrypt podanych w klastrze utworzyć musi być unikatowe.</span><span class="sxs-lookup"><span data-stu-id="e4333-462">Script names provided at cluster create must be all unique.</span></span> <span data-ttu-id="e4333-463">Istniejące skrypty są uruchomione na zmiany rozmiaru.</span><span class="sxs-lookup"><span data-stu-id="e4333-463">Existing scripts are ran on resize.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e4333-464">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e4333-464">Next steps</span></span>

* [<span data-ttu-id="e4333-465">Tworzenie skryptów akcji skryptu dla usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="e4333-465">Develop Script Action scripts for HDInsight</span></span>](hdinsight-hadoop-script-actions-linux.md)
* [<span data-ttu-id="e4333-466">Zainstalować i używać Solr w klastrach HDInsight</span><span class="sxs-lookup"><span data-stu-id="e4333-466">Install and use Solr on HDInsight clusters</span></span>](hdinsight-hadoop-solr-install-linux.md)
* [<span data-ttu-id="e4333-467">Zainstalować i używać Giraph w klastrach HDInsight</span><span class="sxs-lookup"><span data-stu-id="e4333-467">Install and use Giraph on HDInsight clusters</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* [<span data-ttu-id="e4333-468">Dodaj klaster usługi HDInsight tooan dodatkowego miejsca do magazynowania</span><span class="sxs-lookup"><span data-stu-id="e4333-468">Add additional storage tooan HDInsight cluster</span></span>](hdinsight-hadoop-add-storage.md)

[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster-linux/HDI-Cluster-state.png "Etapy podczas tworzenia klastra"
