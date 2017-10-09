---
title: "Programowanie akcji aaaScript z usługą HDInsight opartą na systemie Linux - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse Bash skrypty toocustomize opartych na systemie Linux klastrów usługi HDInsight. Hello funkcji Akcja skryptu HDInsight umożliwia skrypty toorun podczas lub po utworzeniu klastra. Skrypty można toochange używanych ustawień konfiguracji klastra lub zainstalować dodatkowe oprogramowanie."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: cf4c89cd-f7da-4a10-857f-838004965d3e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 1f504b00365df5f4cfb3ae19ad55ff7630342650
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="script-action-development-with-hdinsight"></a><span data-ttu-id="1aaf2-105">Tworzenie akcji skryptu za pomocą usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="1aaf2-105">Script action development with HDInsight</span></span>

<span data-ttu-id="1aaf2-106">Dowiedz się, jak użyciu klastra usługi HDInsight Bash toocustomize skryptów.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-106">Learn how toocustomize your HDInsight cluster using Bash scripts.</span></span> <span data-ttu-id="1aaf2-107">Akcje skryptu to sposób toocustomize HDInsight podczas lub po utworzeniu klastra.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-107">Script actions are a way toocustomize HDInsight during or after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1aaf2-108">kroki Hello w tym dokumencie wymagają klastra usługi HDInsight, który używa systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-108">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="1aaf2-109">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="1aaf2-110">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="1aaf2-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="what-are-script-actions"></a><span data-ttu-id="1aaf2-111">Co to są akcji skryptu</span><span class="sxs-lookup"><span data-stu-id="1aaf2-111">What are script actions</span></span>

<span data-ttu-id="1aaf2-112">Akcje skryptu to skrypty Bash, które Azure działa na zmiany konfiguracji toomake węzłów klastra hello ani instalować oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-112">Script actions are Bash scripts that Azure runs on hello cluster nodes toomake configuration changes or install software.</span></span> <span data-ttu-id="1aaf2-113">Akcja skryptu jest wykonywany jako główny i zapewnia pełny dostęp węzłów klastra toohello praw.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-113">A script action is executed as root, and provides full access rights toohello cluster nodes.</span></span>

<span data-ttu-id="1aaf2-114">Akcje skryptu można zastosować za pośrednictwem hello następujące metody:</span><span class="sxs-lookup"><span data-stu-id="1aaf2-114">Script actions can be applied through hello following methods:</span></span>

| <span data-ttu-id="1aaf2-115">Użyj tej metody tooapply skryptu...</span><span class="sxs-lookup"><span data-stu-id="1aaf2-115">Use this method tooapply a script...</span></span> | <span data-ttu-id="1aaf2-116">Tworzenie klastra podczas...</span><span class="sxs-lookup"><span data-stu-id="1aaf2-116">During cluster creation...</span></span> | <span data-ttu-id="1aaf2-117">W klastrze uruchomione...</span><span class="sxs-lookup"><span data-stu-id="1aaf2-117">On a running cluster...</span></span> |
| --- |:---:|:---:|
| <span data-ttu-id="1aaf2-118">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="1aaf2-118">Azure portal</span></span> |<span data-ttu-id="1aaf2-119">✓</span><span class="sxs-lookup"><span data-stu-id="1aaf2-119">✓</span></span> |<span data-ttu-id="1aaf2-120">✓</span><span class="sxs-lookup"><span data-stu-id="1aaf2-120">✓</span></span> |
| <span data-ttu-id="1aaf2-121">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1aaf2-121">Azure PowerShell</span></span> |<span data-ttu-id="1aaf2-122">✓</span><span class="sxs-lookup"><span data-stu-id="1aaf2-122">✓</span></span> |<span data-ttu-id="1aaf2-123">✓</span><span class="sxs-lookup"><span data-stu-id="1aaf2-123">✓</span></span> |
| <span data-ttu-id="1aaf2-124">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="1aaf2-124">Azure CLI</span></span> |&nbsp; |<span data-ttu-id="1aaf2-125">✓</span><span class="sxs-lookup"><span data-stu-id="1aaf2-125">✓</span></span> |
| <span data-ttu-id="1aaf2-126">Zestaw SDK dla platformy .NET usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="1aaf2-126">HDInsight .NET SDK</span></span> |<span data-ttu-id="1aaf2-127">✓</span><span class="sxs-lookup"><span data-stu-id="1aaf2-127">✓</span></span> |<span data-ttu-id="1aaf2-128">✓</span><span class="sxs-lookup"><span data-stu-id="1aaf2-128">✓</span></span> |
| <span data-ttu-id="1aaf2-129">Szablonu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1aaf2-129">Azure Resource Manager Template</span></span> |<span data-ttu-id="1aaf2-130">✓</span><span class="sxs-lookup"><span data-stu-id="1aaf2-130">✓</span></span> |&nbsp; |

<span data-ttu-id="1aaf2-131">Aby uzyskać więcej informacji na za pomocą akcji skryptu tooapply tych metod, zobacz [HDInsight dostosować klastry za pomocą akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="1aaf2-131">For more information on using these methods tooapply script actions, see [Customize HDInsight clusters using script actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <span data-ttu-id="1aaf2-132"><a name="bestPracticeScripting"></a>Najlepsze rozwiązania dotyczące tworzenia skryptów</span><span class="sxs-lookup"><span data-stu-id="1aaf2-132"><a name="bestPracticeScripting"></a>Best practices for script development</span></span>

<span data-ttu-id="1aaf2-133">Podczas opracowywania niestandardowego skryptu dla klastra usługi HDInsight są kilka tookeep najlepszych praktyk pamiętać:</span><span class="sxs-lookup"><span data-stu-id="1aaf2-133">When you develop a custom script for an HDInsight cluster, there are several best practices tookeep in mind:</span></span>

* [<span data-ttu-id="1aaf2-134">Docelowa wersja platformy Hadoop hello</span><span class="sxs-lookup"><span data-stu-id="1aaf2-134">Target hello Hadoop version</span></span>](#bPS1)
* [<span data-ttu-id="1aaf2-135">Witaj docelowej wersji systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="1aaf2-135">Target hello OS Version</span></span>](#bps10)
* [<span data-ttu-id="1aaf2-136">Znajdują się stabilne łączy tooscript zasoby</span><span class="sxs-lookup"><span data-stu-id="1aaf2-136">Provide stable links tooscript resources</span></span>](#bPS2)
* [<span data-ttu-id="1aaf2-137">Użyj wstępnie skompilowanym zasobów</span><span class="sxs-lookup"><span data-stu-id="1aaf2-137">Use pre-compiled resources</span></span>](#bPS4)
* [<span data-ttu-id="1aaf2-138">Upewnij się, że hello klastra dostosowywania skryptu jest idempotentności</span><span class="sxs-lookup"><span data-stu-id="1aaf2-138">Ensure that hello cluster customization script is idempotent</span></span>](#bPS3)
* [<span data-ttu-id="1aaf2-139">Zapewni to wysoką dostępność hello architektury klastra</span><span class="sxs-lookup"><span data-stu-id="1aaf2-139">Ensure high availability of hello cluster architecture</span></span>](#bPS5)
* [<span data-ttu-id="1aaf2-140">Konfigurowanie magazynu obiektów Blob platformy Azure toouse niestandardowych składników hello</span><span class="sxs-lookup"><span data-stu-id="1aaf2-140">Configure hello custom components toouse Azure Blob storage</span></span>](#bPS6)
* [<span data-ttu-id="1aaf2-141">Zapis tooSTDOUT informacji i STDERR.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-141">Write information tooSTDOUT and STDERR</span></span>](#bPS7)
* [<span data-ttu-id="1aaf2-142">Zapisz pliki jako ASCII z końców LF</span><span class="sxs-lookup"><span data-stu-id="1aaf2-142">Save files as ASCII with LF line endings</span></span>](#bps8)
* [<span data-ttu-id="1aaf2-143">Użyj toorecover logiki ponownych prób w przypadku błędów przejściowych</span><span class="sxs-lookup"><span data-stu-id="1aaf2-143">Use retry logic toorecover from transient errors</span></span>](#bps9)

> [!IMPORTANT]
> <span data-ttu-id="1aaf2-144">Akcje skryptu musi zostać zakończone w ciągu 60 minut lub hello proces zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-144">Script actions must complete within 60 minutes or hello process fails.</span></span> <span data-ttu-id="1aaf2-145">Podczas inicjowania obsługi węzła, hello skrypt jest uruchamiany równocześnie z innymi procesami instalacji i konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-145">During node provisioning, hello script runs concurrently with other setup and configuration processes.</span></span> <span data-ttu-id="1aaf2-146">Konkurowanie o zasoby, takie jak czas lub sieci przepustowości Procesora może powodować hello skryptu tootake dłużej toofinish niż w środowisku projektowania.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-146">Competition for resources such as CPU time or network bandwidth may cause hello script tootake longer toofinish than it does in your development environment.</span></span>

### <span data-ttu-id="1aaf2-147"><a name="bPS1"></a>Docelowa wersja platformy Hadoop hello</span><span class="sxs-lookup"><span data-stu-id="1aaf2-147"><a name="bPS1"></a>Target hello Hadoop version</span></span>

<span data-ttu-id="1aaf2-148">Różne wersje HDInsight korzystają z różnych wersji usług Hadoop i zainstalowanych składników.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-148">Different versions of HDInsight have different versions of Hadoop services and components installed.</span></span> <span data-ttu-id="1aaf2-149">Jeśli skrypt oczekuje określoną wersję usługi lub składnika, skrypt hello należy używać tylko z wersją hello HDInsight zawierającym hello wymagane składniki.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-149">If your script expects a specific version of a service or component, you should only use hello script with hello version of HDInsight that includes hello required components.</span></span> <span data-ttu-id="1aaf2-150">Informacje można znaleźć w wersji składników dołączone do usługi HDInsight przy użyciu hello [przechowywanie wersji składnika usługi HDInsight](hdinsight-component-versioning.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-150">You can find information on component versions included with HDInsight using hello [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

### <span data-ttu-id="1aaf2-151"><a name="bps10"></a>Docelowa wersja hello systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="1aaf2-151"><a name="bps10"></a> Target hello OS version</span></span>

<span data-ttu-id="1aaf2-152">HDInsight opartych na systemie Linux jest oparta na powitania dystrybucji Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-152">Linux-based HDInsight is based on hello Ubuntu Linux distribution.</span></span> <span data-ttu-id="1aaf2-153">Różnych wersji usługi hdinsight korzystają z różnych wersji systemu Ubuntu, która może zmienić sposób działania skryptu.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-153">Different versions of HDInsight rely on different versions of Ubuntu, which may change how your script behaves.</span></span> <span data-ttu-id="1aaf2-154">Na przykład HDInsight 3.4 i starsze wersje są oparte na wersji Ubuntu, które używają Upstart.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-154">For example, HDInsight 3.4 and earlier are based on Ubuntu versions that use Upstart.</span></span> <span data-ttu-id="1aaf2-155">Wersja 3.5 jest oparta na 16.04 Ubuntu, który używa Systemd.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-155">Version 3.5 is based on Ubuntu 16.04, which uses Systemd.</span></span> <span data-ttu-id="1aaf2-156">Systemd i Upstart zależne inne polecenia, aby skrypt powinien być zapisywany toowork zarówno.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-156">Systemd and Upstart rely on different commands, so your script should be written toowork with both.</span></span>

<span data-ttu-id="1aaf2-157">Inna ważna różnica między HDInsight 3.4 i 3.5 jest to, że `JAVA_HOME` teraz punkty tooJava 8.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-157">Another important difference between HDInsight 3.4 and 3.5 is that `JAVA_HOME` now points tooJava 8.</span></span>

<span data-ttu-id="1aaf2-158">Wersja systemu operacyjnego hello można sprawdzić za pomocą `lsb_release`.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-158">You can check hello OS version by using `lsb_release`.</span></span> <span data-ttu-id="1aaf2-159">Witaj poniższy kod przedstawia sposób toodetermine Jeśli hello skryptu systemem Ubuntu 14 lub 16:</span><span class="sxs-lookup"><span data-stu-id="1aaf2-159">hello following code demonstrates how toodetermine if hello script is running on Ubuntu 14 or 16:</span></span>

```bash
OS_VERSION=$(lsb_release -sr)
if [[ $OS_VERSION == 14* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-14-04."
    HUE_TARFILE=hue-binaries-14-04.tgz
elif [[ $OS_VERSION == 16* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-16-04."
    HUE_TARFILE=hue-binaries-16-04.tgz
fi
...
if [[ $OS_VERSION == 16* ]]; then
    echo "Using systemd configuration"
    systemctl daemon-reload
    systemctl stop webwasb.service    
    systemctl start webwasb.service
else
    echo "Using upstart configuration"
    initctl reload-configuration
    stop webwasb
    start webwasb
fi
...
if [[ $OS_VERSION == 14* ]]; then
    export JAVA_HOME=/usr/lib/jvm/java-7-openjdk-amd64
elif [[ $OS_VERSION == 16* ]]; then
    export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
fi
```

<span data-ttu-id="1aaf2-160">Można znaleźć hello pełne skrypt, który zawiera te wstawki na https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-160">You can find hello full script that contains these snippets at https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh.</span></span>

<span data-ttu-id="1aaf2-161">Wersję hello Ubuntu, który jest używany przez usługi HDInsight, zobacz hello [składnika usługi HDInsight w wersji](hdinsight-component-versioning.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-161">For hello version of Ubuntu that is used by HDInsight, see hello [HDInsight component version](hdinsight-component-versioning.md) document.</span></span>

<span data-ttu-id="1aaf2-162">toounderstand hello różnice między Systemd i Upstart, zobacz [Systemd dla użytkowników Upstart](https://wiki.ubuntu.com/SystemdForUpstartUsers).</span><span class="sxs-lookup"><span data-stu-id="1aaf2-162">toounderstand hello differences between Systemd and Upstart, see [Systemd for Upstart users](https://wiki.ubuntu.com/SystemdForUpstartUsers).</span></span>

### <span data-ttu-id="1aaf2-163"><a name="bPS2"></a>Znajdują się stabilne łączy tooscript zasoby</span><span class="sxs-lookup"><span data-stu-id="1aaf2-163"><a name="bPS2"></a>Provide stable links tooscript resources</span></span>

<span data-ttu-id="1aaf2-164">Witaj skrypt i skojarzonych zasobów musi być dostępna przez cały okres istnienia hello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-164">hello script and associated resources must remain available throughout hello lifetime of hello cluster.</span></span> <span data-ttu-id="1aaf2-165">Te zasoby są wymagane, jeśli zostaną dodane nowe węzły klastra toohello podczas operacji skalowania.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-165">These resources are required if new nodes are added toohello cluster during scaling operations.</span></span>

<span data-ttu-id="1aaf2-166">Witaj, najlepszym rozwiązaniem jest toodownload i zarchiwizowanie wszystkich na koncie magazynu Azure w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-166">hello best practice is toodownload and archive everything in an Azure Storage account on your subscription.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1aaf2-167">Konto magazynu Hello używane musi być hello domyślne konto magazynu dla klastra hello lub kontener publiczne, tylko do odczytu na inne konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-167">hello storage account used must be hello default storage account for hello cluster or a public, read-only container on any other storage account.</span></span>

<span data-ttu-id="1aaf2-168">Na przykład przykłady hello obsługiwane przez firmę Microsoft są przechowywane w hello [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/) konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-168">For example, hello samples provided by Microsoft are stored in hello [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/) storage account.</span></span> <span data-ttu-id="1aaf2-169">Jest obsługiwana przez zespół usługi HDInsight hello kontener publiczne, tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-169">This is a public, read-only container maintained by hello HDInsight team.</span></span>

### <span data-ttu-id="1aaf2-170"><a name="bPS4"></a>Użyj wstępnie skompilowanym zasobów</span><span class="sxs-lookup"><span data-stu-id="1aaf2-170"><a name="bPS4"></a>Use pre-compiled resources</span></span>

<span data-ttu-id="1aaf2-171">tooreduce hello czasu zajmuje toorun hello skryptu, uniknąć operacji kompilowane zasobów z kodu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-171">tooreduce hello time it takes toorun hello script, avoid operations that compile resources from source code.</span></span> <span data-ttu-id="1aaf2-172">Na przykład wstępnie skompilować zasobów i zapisanie ich w obiekcie blob konta usługi Azure Storage w hello tego samego centrum danych, w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-172">For example, pre-compile resources and store them in an Azure Storage account blob in hello same data center as HDInsight.</span></span>

### <span data-ttu-id="1aaf2-173"><a name="bPS3"></a>Upewnij się, że hello klastra dostosowywania skryptu jest idempotentności</span><span class="sxs-lookup"><span data-stu-id="1aaf2-173"><a name="bPS3"></a>Ensure that hello cluster customization script is idempotent</span></span>

<span data-ttu-id="1aaf2-174">Skrypty musi być idempotentności.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-174">Scripts must be idempotent.</span></span> <span data-ttu-id="1aaf2-175">Jeśli hello skrypt jest uruchamiany wiele razy, powinien on zwrócić hello sam stan zawsze toohello klastra.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-175">If hello script runs multiple times, it should return hello cluster toohello same state every time.</span></span>

<span data-ttu-id="1aaf2-176">Na przykład skrypt, który modyfikuje pliki konfiguracji nie dodać zduplikowanych wpisów, gdy uruchomiono wiele razy.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-176">For example, a script that modifies configuration files should not add duplicate entries if ran multiple times.</span></span>

### <span data-ttu-id="1aaf2-177"><a name="bPS5"></a>Zapewni to wysoką dostępność hello architektury klastra</span><span class="sxs-lookup"><span data-stu-id="1aaf2-177"><a name="bPS5"></a>Ensure high availability of hello cluster architecture</span></span>

<span data-ttu-id="1aaf2-178">Klastry HDInsight opartych na systemie Linux zapewniają dwa węzły head, które są aktywne w ramach klastra hello, a akcji skryptu, uruchom na obu węzłów.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-178">Linux-based HDInsight clusters provide two head nodes that are active within hello cluster, and script actions run on both nodes.</span></span> <span data-ttu-id="1aaf2-179">Jeżeli hello składniki, które można zainstalować tylko jednego węzła głównego, nie należy instalować na obu węzłów głównych hello składników.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-179">If hello components you install expect only one head node, do not install hello components on both head nodes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1aaf2-180">Usługi w ramach usługi HDInsight są zaprojektowane toofail za pośrednictwem, między dwoma węzłami head hello, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-180">Services provided as part of HDInsight are designed toofail over between hello two head nodes as needed.</span></span> <span data-ttu-id="1aaf2-181">Ta funkcja nie jest przedłużana toocustom składniki zainstalowane za pomocą akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-181">This functionality is not extended toocustom components installed through script actions.</span></span> <span data-ttu-id="1aaf2-182">Jeśli potrzebujesz wysokiej dostępności dla niestandardowych składników, musisz zaimplementować własny mechanizm pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-182">If you need high availability for custom components, you must implement your own failover mechanism.</span></span>

### <span data-ttu-id="1aaf2-183"><a name="bPS6"></a>Konfigurowanie magazynu obiektów Blob platformy Azure toouse niestandardowych składników hello</span><span class="sxs-lookup"><span data-stu-id="1aaf2-183"><a name="bPS6"></a>Configure hello custom components toouse Azure Blob storage</span></span>

<span data-ttu-id="1aaf2-184">Składniki, które można zainstalować w klastrze hello może mieć konfigurację domyślną, która korzysta z magazynu systemu Distributed plików Hadoop (HDFS).</span><span class="sxs-lookup"><span data-stu-id="1aaf2-184">Components that you install on hello cluster might have a default configuration that uses Hadoop Distributed File System (HDFS) storage.</span></span> <span data-ttu-id="1aaf2-185">HDInsight używa magazynu Azure lub usługi Data Lake Store jako hello domyślny magazyn.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-185">HDInsight uses either Azure Storage or Data Lake Store as hello default storage.</span></span> <span data-ttu-id="1aaf2-186">Podaj zarówno systemu plików zgodny system plików HDFS, który będzie się powtarzać danych, nawet jeśli klaster hello jest usunięty.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-186">Both provide an HDFS compatible file system that persists data even if hello cluster is deleted.</span></span> <span data-ttu-id="1aaf2-187">Może być konieczne składniki tooconfigure zainstalować toouse WASB lub ADL zamiast systemu plików HDFS.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-187">You may need tooconfigure components you install toouse WASB or ADL instead of HDFS.</span></span>

<span data-ttu-id="1aaf2-188">Dla większości operacji nie trzeba toospecify hello w systemie plików.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-188">For most operations, you do not need toospecify hello file system.</span></span> <span data-ttu-id="1aaf2-189">Na przykład następujące hello kopiuje plik giraph-examples.jar hello z hello pliku lokalnego systemu toocluster magazynu:</span><span class="sxs-lookup"><span data-stu-id="1aaf2-189">For example, hello following copies hello giraph-examples.jar file from hello local file system toocluster storage:</span></span>

```bash
hdfs dfs -put /usr/hdp/current/giraph/giraph-examples.jar /example/jars/
```

<span data-ttu-id="1aaf2-190">W tym przykładzie hello `hdfs` polecenie niewidocznie używa magazynu klastra hello domyślne.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-190">In this example, hello `hdfs` command transparently uses hello default cluster storage.</span></span> <span data-ttu-id="1aaf2-191">Dla niektórych operacji może być konieczne hello toospecify identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-191">For some operations, you may need toospecify hello URI.</span></span> <span data-ttu-id="1aaf2-192">Na przykład `adl:///example/jars` dla usługi Data Lake Store lub `wasb:///example/jars` usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-192">For example, `adl:///example/jars` for Data Lake Store or `wasb:///example/jars` for Azure Storage.</span></span>

### <span data-ttu-id="1aaf2-193"><a name="bPS7"></a>Zapis tooSTDOUT informacji i STDERR.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-193"><a name="bPS7"></a>Write information tooSTDOUT and STDERR</span></span>

<span data-ttu-id="1aaf2-194">HDInsight rejestruje dane wyjściowe skryptu jest zapisywane tooSTDOUT i STDERR.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-194">HDInsight logs script output that is written tooSTDOUT and STDERR.</span></span> <span data-ttu-id="1aaf2-195">Można wyświetlić te informacje przy użyciu hello Ambari web UI.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-195">You can view this information using hello Ambari web UI.</span></span>

> [!NOTE]
> <span data-ttu-id="1aaf2-196">Ambari jest dostępna tylko jeśli hello klaster został utworzony pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-196">Ambari is only available if hello cluster is successfully created.</span></span> <span data-ttu-id="1aaf2-197">Jeśli używasz akcji skryptu podczas tworzenia klastra i utworzenie kończy się niepowodzeniem, zobacz hello Rozwiązywanie problemów z sekcji [HDInsight dostosować klastry za pomocą akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) dotyczące innych metod uzyskiwania dostępu do zarejestrowane informacje.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-197">If you use a script action during cluster creation, and creation fails, see hello troubleshooting section [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) for other ways of accessing logged information.</span></span>

<span data-ttu-id="1aaf2-198">Większość narzędzi i pakiety instalacyjne już zapisu tooSTDOUT informacji i STDERR, jednak może być tooadd dodatkowe rejestrowanie.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-198">Most utilities and installation packages already write information tooSTDOUT and STDERR, however you may want tooadd additional logging.</span></span> <span data-ttu-id="1aaf2-199">toosend tekst tooSTDOUT, użyj `echo`.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-199">toosend text tooSTDOUT, use `echo`.</span></span> <span data-ttu-id="1aaf2-200">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="1aaf2-200">For example:</span></span>

```bash
echo "Getting ready tooinstall Foo"
```

<span data-ttu-id="1aaf2-201">Domyślnie `echo` wysyła hello tooSTDOUT ciągu.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-201">By default, `echo` sends hello string tooSTDOUT.</span></span> <span data-ttu-id="1aaf2-202">toodirect go tooSTDERR, Dodaj `>&2` przed `echo`.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-202">toodirect it tooSTDERR, add `>&2` before `echo`.</span></span> <span data-ttu-id="1aaf2-203">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="1aaf2-203">For example:</span></span>

```bash
>&2 echo "An error occurred installing Foo"
```

<span data-ttu-id="1aaf2-204">To przekierowuje informacje zapisane zamiast tooSTDERR tooSTDOUT (2).</span><span class="sxs-lookup"><span data-stu-id="1aaf2-204">This redirects information written tooSTDOUT tooSTDERR (2) instead.</span></span> <span data-ttu-id="1aaf2-205">Aby uzyskać więcej informacji dotyczących przekierowania we/wy, zobacz [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html).</span><span class="sxs-lookup"><span data-stu-id="1aaf2-205">For more information on IO redirection, see [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html).</span></span>

<span data-ttu-id="1aaf2-206">Aby uzyskać więcej informacji o wyświetlaniu informacji zarejestrowanych przez akcje skryptu, zobacz [HDInsight dostosować klastry za pomocą akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)</span><span class="sxs-lookup"><span data-stu-id="1aaf2-206">For more information on viewing information logged by script actions, see [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)</span></span>

### <span data-ttu-id="1aaf2-207"><a name="bps8"></a>Zapisz pliki jako ASCII z końców LF</span><span class="sxs-lookup"><span data-stu-id="1aaf2-207"><a name="bps8"></a> Save files as ASCII with LF line endings</span></span>

<span data-ttu-id="1aaf2-208">Skrypty powłoki systemowej powinny być przechowywane w formacie ASCII, liniami został przerwany przez wysuwu wiersza.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-208">Bash scripts should be stored as ASCII format, with lines terminated by LF.</span></span> <span data-ttu-id="1aaf2-209">Pliki, które są przechowywane w formacie UTF-8, lub użyj CRLF jako zakończenie wiersza hello może zakończyć się niepowodzeniem z hello następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="1aaf2-209">Files that are stored as UTF-8, or use CRLF as hello line ending may fail with hello following error:</span></span>

```
$'\r': command not found
line 1: #!/usr/bin/env: No such file or directory
```

### <span data-ttu-id="1aaf2-210"><a name="bps9"></a>Użyj toorecover logiki ponownych prób w przypadku błędów przejściowych</span><span class="sxs-lookup"><span data-stu-id="1aaf2-210"><a name="bps9"></a> Use retry logic toorecover from transient errors</span></span>

<span data-ttu-id="1aaf2-211">Podczas pobierania plików, instalowanie pakietów przy użyciu stanie get lub innych działań, których dane są przesyłane za pośrednictwem hello internet, akcja hello może zakończyć się niepowodzeniem ze względu na błędy łączności sieciowej tootransient.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-211">When downloading files, installing packages using apt-get, or other actions that transmit data over hello internet, hello action may fail due tootransient networking errors.</span></span> <span data-ttu-id="1aaf2-212">Na przykład zasób zdalny hello, które komunikują się z może być w procesie hello niepowodzenie nad węzłem kopii zapasowej tooa.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-212">For example, hello remote resource you are communicating with may be in hello process of failing over tooa backup node.</span></span>

<span data-ttu-id="1aaf2-213">toomake tootransient odporność błędy skryptu, można implementację logiki ponawiania próby.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-213">toomake your script resilient tootransient errors, you can implement retry logic.</span></span> <span data-ttu-id="1aaf2-214">powitania po funkcja pokazano, jak Logika ponawiania próby tooimplement.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-214">hello following function demonstrates how tooimplement retry logic.</span></span> <span data-ttu-id="1aaf2-215">Ponowną operacji hello trzy razy przed niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-215">It retries hello operation three times before failing.</span></span>

```bash
#retry
MAXATTEMPTS=3

retry() {
    local -r CMD="$@"
    local -i ATTMEPTNUM=1
    local -i RETRYINTERVAL=2

    until $CMD
    do
        if (( ATTMEPTNUM == MAXATTEMPTS ))
        then
                echo "Attempt $ATTMEPTNUM failed. no more attempts left."
                return 1
        else
                echo "Attempt $ATTMEPTNUM failed! Retrying in $RETRYINTERVAL seconds..."
                sleep $(( RETRYINTERVAL ))
                ATTMEPTNUM=$ATTMEPTNUM+1
        fi
    done
}
```

<span data-ttu-id="1aaf2-216">Witaj poniższe przykłady pokazują, jak toouse tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-216">hello following examples demonstrate how toouse this function.</span></span>

```bash
retry ls -ltr foo

retry wget -O ./tmpfile.sh https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh
```

## <span data-ttu-id="1aaf2-217"><a name="helpermethods"></a>Metody pomocnicze dla niestandardowych skryptów</span><span class="sxs-lookup"><span data-stu-id="1aaf2-217"><a name="helpermethods"></a>Helper methods for custom scripts</span></span>

<span data-ttu-id="1aaf2-218">Metody pomocnicze akcji skryptu są narzędzia, które można użyć podczas pisania skryptów niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-218">Script action helper methods are utilities that you can use while writing custom scripts.</span></span> <span data-ttu-id="1aaf2-219">Te metody są zawarte w[https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh) skryptu.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-219">These methods are contained in the[https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh) script.</span></span> <span data-ttu-id="1aaf2-220">Użyj następującego toodownload hello i używać ich jako część skryptu:</span><span class="sxs-lookup"><span data-stu-id="1aaf2-220">Use hello following toodownload and use them as part of your script:</span></span>

```bash
# Import hello helper method module.
wget -O /tmp/HDInsightUtilities-v01.sh -q https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh && source /tmp/HDInsightUtilities-v01.sh && rm -f /tmp/HDInsightUtilities-v01.sh
```

<span data-ttu-id="1aaf2-221">powitania po pomocników dostępne do użycia w skrypcie:</span><span class="sxs-lookup"><span data-stu-id="1aaf2-221">hello following helpers available for use in your script:</span></span>

| <span data-ttu-id="1aaf2-222">Użycie pomocnika</span><span class="sxs-lookup"><span data-stu-id="1aaf2-222">Helper usage</span></span> | <span data-ttu-id="1aaf2-223">Opis</span><span class="sxs-lookup"><span data-stu-id="1aaf2-223">Description</span></span> |
| --- | --- |
| `download_file SOURCEURL DESTFILEPATH [OVERWRITE]` |<span data-ttu-id="1aaf2-224">Pobiera plik z hello źródła identyfikatora URI toohello określona ścieżka pliku.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-224">Downloads a file from hello source URI toohello specified file path.</span></span> <span data-ttu-id="1aaf2-225">Domyślnie go nie zastępuj istniejącego pliku.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-225">By default, it does not overwrite an existing file.</span></span> |
| `untar_file TARFILE DESTDIR` |<span data-ttu-id="1aaf2-226">Wyodrębnia plik tar (przy użyciu `-xf`) toohello katalogu docelowego.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-226">Extracts a tar file (using `-xf`) toohello destination directory.</span></span> |
| `test_is_headnode` |<span data-ttu-id="1aaf2-227">Jeśli został uruchomiony na węzła głównego klastra zwracany 1; w przeciwnym razie wartość 0.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-227">If ran on a cluster head node, return 1; otherwise, 0.</span></span> |
| `test_is_datanode` |<span data-ttu-id="1aaf2-228">W przypadku hello bieżący węzeł jest węzłem danych (proces roboczy), zwraca 1; w przeciwnym razie wartość 0.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-228">If hello current node is a data (worker) node, return a 1; otherwise, 0.</span></span> |
| `test_is_first_datanode` |<span data-ttu-id="1aaf2-229">W przypadku bieżącego węzła hello jest pierwsze dane hello (proces roboczy) węzła (o nazwie workernode0) zwraca 1; w przeciwnym razie wartość 0.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-229">If hello current node is hello first data (worker) node (named workernode0) return a 1; otherwise, 0.</span></span> |
| `get_headnodes` |<span data-ttu-id="1aaf2-230">Zwraca nazwę FQDN hello hello headnodes hello klastra.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-230">Return hello fully qualified domain name of hello headnodes in hello cluster.</span></span> <span data-ttu-id="1aaf2-231">Nazwy są rozdzielone przecinkami.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-231">Names are comma delimited.</span></span> <span data-ttu-id="1aaf2-232">Ciąg pusty jest zwracana w przypadku błędu.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-232">An empty string is returned on error.</span></span> |
| `get_primary_headnode` |<span data-ttu-id="1aaf2-233">Pobiera nazwę FQDN hello hello headnode podstawowego.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-233">Gets hello fully qualified domain name of hello primary headnode.</span></span> <span data-ttu-id="1aaf2-234">Ciąg pusty jest zwracana w przypadku błędu.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-234">An empty string is returned on error.</span></span> |
| `get_secondary_headnode` |<span data-ttu-id="1aaf2-235">Pobiera nazwę FQDN hello hello headnode dodatkowej.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-235">Gets hello fully qualified domain name of hello secondary headnode.</span></span> <span data-ttu-id="1aaf2-236">Ciąg pusty jest zwracana w przypadku błędu.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-236">An empty string is returned on error.</span></span> |
| `get_primary_headnode_number` |<span data-ttu-id="1aaf2-237">Pobiera sufiks numeryczny hello z hello headnode podstawowego.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-237">Gets hello numeric suffix of hello primary headnode.</span></span> <span data-ttu-id="1aaf2-238">Ciąg pusty jest zwracana w przypadku błędu.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-238">An empty string is returned on error.</span></span> |
| `get_secondary_headnode_number` |<span data-ttu-id="1aaf2-239">Pobiera sufiks numeryczny hello z hello headnode dodatkowej.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-239">Gets hello numeric suffix of hello secondary headnode.</span></span> <span data-ttu-id="1aaf2-240">Ciąg pusty jest zwracana w przypadku błędu.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-240">An empty string is returned on error.</span></span> |

## <span data-ttu-id="1aaf2-241"><a name="commonusage"></a>Wspólne wzorce użycia</span><span class="sxs-lookup"><span data-stu-id="1aaf2-241"><a name="commonusage"></a>Common usage patterns</span></span>

<span data-ttu-id="1aaf2-242">Ta sekcja zawiera wskazówki dotyczące implementowania niektóre hello typowe wzorce użycia, które możesz napotkać podczas pisania skryptu niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-242">This section provides guidance on implementing some of hello common usage patterns that you might run into while writing your own custom script.</span></span>

### <a name="passing-parameters-tooa-script"></a><span data-ttu-id="1aaf2-243">Przekazywanie parametrów tooa skryptu</span><span class="sxs-lookup"><span data-stu-id="1aaf2-243">Passing parameters tooa script</span></span>

<span data-ttu-id="1aaf2-244">W niektórych przypadkach skrypt może wymagać parametrów.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-244">In some cases, your script may require parameters.</span></span> <span data-ttu-id="1aaf2-245">Na przykład mogą być potrzebne hasło administratora hello hello klastra, korzystając z interfejsu API REST Ambari hello.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-245">For example, you may need hello admin password for hello cluster when using hello Ambari REST API.</span></span>

<span data-ttu-id="1aaf2-246">Parametry przekazywane do skryptu toohello są określane jako *parametrów pozycyjnych*i są przydzielane za`$1` dla pierwszego parametru hello `$2` dla hello drugi i tak w przypadku.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-246">Parameters passed toohello script are known as *positional parameters*, and are assigned too`$1` for hello first parameter, `$2` for hello second, and so-on.</span></span> <span data-ttu-id="1aaf2-247">`$0`zawiera nazwę hello hello sam skrypt.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-247">`$0` contains hello name of hello script itself.</span></span>

<span data-ttu-id="1aaf2-248">Wartości przekazane jako parametry skryptu toohello powinna zostać ujęta w pojedynczym cudzysłowie (').</span><span class="sxs-lookup"><span data-stu-id="1aaf2-248">Values passed toohello script as parameters should be enclosed by single quotes (').</span></span> <span data-ttu-id="1aaf2-249">Daje to gwarancję, że hello przekazana wartość jest traktowany jako literału.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-249">Doing so ensures that hello passed value is treated as a literal.</span></span>

### <a name="setting-environment-variables"></a><span data-ttu-id="1aaf2-250">Ustawianie zmiennych środowiskowych</span><span class="sxs-lookup"><span data-stu-id="1aaf2-250">Setting environment variables</span></span>

<span data-ttu-id="1aaf2-251">Ustawienie zmiennej środowiskowej jest wykonywane przez hello następującej instrukcji:</span><span class="sxs-lookup"><span data-stu-id="1aaf2-251">Setting an environment variable is performed by hello following statement:</span></span>

    VARIABLENAME=value

<span data-ttu-id="1aaf2-252">Gdzie NAZWA_ZMIENNEJ to nazwa hello hello zmiennej.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-252">Where VARIABLENAME is hello name of hello variable.</span></span> <span data-ttu-id="1aaf2-253">Użycie zmiennej, hello tooaccess `$VARIABLENAME`.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-253">tooaccess hello variable, use `$VARIABLENAME`.</span></span> <span data-ttu-id="1aaf2-254">Na przykład tooassign dla wartości dostarczonej przez parametrów pozycyjnych jako zmienną środowiskową o nazwie HASŁA, należy użyć następującej instrukcji hello:</span><span class="sxs-lookup"><span data-stu-id="1aaf2-254">For example, tooassign a value provided by a positional parameter as an environment variable named PASSWORD, you would use hello following statement:</span></span>

    PASSWORD=$1

<span data-ttu-id="1aaf2-255">Dostęp do informacji toohello można następnie użyć `$PASSWORD`.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-255">Subsequent access toohello information could then use `$PASSWORD`.</span></span>

<span data-ttu-id="1aaf2-256">Zmienne środowiskowe w hello skrypt istnieje tylko w zakresie hello hello skryptu.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-256">Environment variables set within hello script only exist within hello scope of hello script.</span></span> <span data-ttu-id="1aaf2-257">W niektórych przypadkach może być konieczne tooadd zmiennych środowiskowych całego systemu, które pozostają po zakończeniu działania skryptu hello.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-257">In some cases, you may need tooadd system-wide environment variables that will persist after hello script has finished.</span></span> <span data-ttu-id="1aaf2-258">zmienne środowiskowe systemowe tooadd, Dodaj zmienną hello zbyt`/etc/environment`.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-258">tooadd system-wide environment variables, add hello variable too`/etc/environment`.</span></span> <span data-ttu-id="1aaf2-259">Na przykład dodaje powitania po instrukcji `HADOOP_CONF_DIR`:</span><span class="sxs-lookup"><span data-stu-id="1aaf2-259">For example, hello following statement adds `HADOOP_CONF_DIR`:</span></span>

```bash
echo "HADOOP_CONF_DIR=/etc/hadoop/conf" | sudo tee -a /etc/environment
```

### <a name="access-toolocations-where-hello-custom-scripts-are-stored"></a><span data-ttu-id="1aaf2-260">Gdzie są przechowywane niestandardowe skrypty hello toolocations dostępu</span><span class="sxs-lookup"><span data-stu-id="1aaf2-260">Access toolocations where hello custom scripts are stored</span></span>

<span data-ttu-id="1aaf2-261">Skrypty używane toocustomize klastra musi toobe przechowywane w jednej z następujących lokalizacji hello:</span><span class="sxs-lookup"><span data-stu-id="1aaf2-261">Scripts used toocustomize a cluster needs toobe stored in one of hello following locations:</span></span>

* <span data-ttu-id="1aaf2-262">__Konta magazynu Azure__ skojarzonego z klastrem hello.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-262">An __Azure Storage account__ that is associated with hello cluster.</span></span>

* <span data-ttu-id="1aaf2-263">__Konta magazynu dodatkowe__ skojarzony z klastrem hello.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-263">An __additional storage account__ associated with hello cluster.</span></span>

* <span data-ttu-id="1aaf2-264">A __publicznie można odczytać identyfikatora URI__.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-264">A __publicly readable URI__.</span></span> <span data-ttu-id="1aaf2-265">Na przykład adres URL toodata przechowywane na OneDrive, Dropbox lub innych plików usługi hosta.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-265">For example, a URL toodata stored on OneDrive, Dropbox, or other file hosting service.</span></span>

* <span data-ttu-id="1aaf2-266">__Konta usługi Azure Data Lake Store__ skojarzonego z klastrem usługi HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-266">An __Azure Data Lake Store account__ that is associated with hello HDInsight cluster.</span></span> <span data-ttu-id="1aaf2-267">Aby uzyskać więcej informacji na temat używania usługi Azure Data Lake Store z usługą HDInsight, zobacz [tworzenia klastra usługi HDInsight z usługą Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1aaf2-267">For more information on using Azure Data Lake Store with HDInsight, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="1aaf2-268">Hello usługi głównej HDInsight używa tooaccess Data Lake — Magazyn musi mieć dostęp do odczytu toohello skryptu.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-268">hello service principal HDInsight uses tooaccess Data Lake Store must have read access toohello script.</span></span>

<span data-ttu-id="1aaf2-269">Zasoby używane przez skrypt hello również musi być publicznie dostępny.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-269">Resources used by hello script must also be publicly available.</span></span>

<span data-ttu-id="1aaf2-270">Przechowywanie plików hello w koncie magazynu Azure lub usługi Azure Data Lake Store zapewnia szybki dostęp, jako zarówno w ramach hello sieć platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-270">Storing hello files in an Azure Storage account or Azure Data Lake Store provides fast access, as both within hello Azure network.</span></span>

> [!NOTE]
> <span data-ttu-id="1aaf2-271">w zależności od używanej usługi hello różni się Hello skryptu hello tooreference formatu identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-271">hello URI format used tooreference hello script differs depending on hello service being used.</span></span> <span data-ttu-id="1aaf2-272">Dla konta magazynu skojarzone z klastrem usługi HDInsight hello, użyj `wasb://` lub `wasbs://`.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-272">For storage accounts associated with hello HDInsight cluster, use `wasb://` or `wasbs://`.</span></span> <span data-ttu-id="1aaf2-273">Identyfikatory URI publicznie do odczytu, użyj `http://` lub `https://`.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-273">For publicly readable URIs, use `http://` or `https://`.</span></span> <span data-ttu-id="1aaf2-274">Data Lake Store, użyj `adl://`.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-274">For Data Lake Store, use `adl://`.</span></span>

### <a name="checking-hello-operating-system-version"></a><span data-ttu-id="1aaf2-275">Sprawdzanie wersji systemu operacyjnego hello</span><span class="sxs-lookup"><span data-stu-id="1aaf2-275">Checking hello operating system version</span></span>

<span data-ttu-id="1aaf2-276">Różne wersje HDInsight korzystają z określonych wersji systemu Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-276">Different versions of HDInsight rely on specific versions of Ubuntu.</span></span> <span data-ttu-id="1aaf2-277">Może to być różnice między systemami Operacyjnymi, które muszą sprawdzaj w skrypcie.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-277">There may be differences between OS versions that you must check for in your script.</span></span> <span data-ttu-id="1aaf2-278">Na przykład może być konieczne tooinstall pliku binarnego, który jest wersja wiązanej toohello Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-278">For example, you may need tooinstall a binary that is tied toohello version of Ubuntu.</span></span>

<span data-ttu-id="1aaf2-279">toocheck wersji hello systemu operacyjnego, użyj `lsb_release`.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-279">toocheck hello OS version, use `lsb_release`.</span></span> <span data-ttu-id="1aaf2-280">Na przykład hello następującego skryptu pokazano, jak tooreference tar określonego pliku w zależności od wersji systemu operacyjnego hello:</span><span class="sxs-lookup"><span data-stu-id="1aaf2-280">For example, hello following script demonstrates how tooreference a specific tar file depending on hello OS version:</span></span>

```bash
OS_VERSION=$(lsb_release -sr)
if [[ $OS_VERSION == 14* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-14-04."
    HUE_TARFILE=hue-binaries-14-04.tgz
elif [[ $OS_VERSION == 16* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-16-04."
    HUE_TARFILE=hue-binaries-16-04.tgz
fi
```

## <span data-ttu-id="1aaf2-281"><a name="deployScript"></a>Lista kontrolna wdrażania akcji skryptu</span><span class="sxs-lookup"><span data-stu-id="1aaf2-281"><a name="deployScript"></a>Checklist for deploying a script action</span></span>

<span data-ttu-id="1aaf2-282">Poniżej przedstawiono kroki hello Wybraliśmy podczas przygotowywania toodeploy te skrypty:</span><span class="sxs-lookup"><span data-stu-id="1aaf2-282">Here are hello steps we took when preparing toodeploy these scripts:</span></span>

* <span data-ttu-id="1aaf2-283">Umieść hello pliki, które zawierają hello niestandardowych skryptów w miejscu, który jest dostępny dla węzłów klastra hello podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-283">Put hello files that contain hello custom scripts in a place that is accessible by hello cluster nodes during deployment.</span></span> <span data-ttu-id="1aaf2-284">Na przykład hello domyślny magazyn dla klastra hello.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-284">For example, hello default storage for hello cluster.</span></span> <span data-ttu-id="1aaf2-285">Pliki mogą być również przechowywane w publicznie do odczytu usług hostingu.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-285">Files can also be stored in publicly readable hosting services.</span></span>
* <span data-ttu-id="1aaf2-286">Sprawdź, czy skrypt hello impotent.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-286">Verify that hello script is impotent.</span></span> <span data-ttu-id="1aaf2-287">Dzięki temu toobe skryptu hello wykonywane wiele razy na powitania sam węzeł.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-287">Doing so allows hello script toobe executed multiple times on hello same node.</span></span>
* <span data-ttu-id="1aaf2-288">Użyj pliku tymczasowego katalogu /tmp tookeep hello pobrane pliki używane przez skrypty hello i następnie wyczyść je po wykonaniu skryptów.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-288">Use a temporary file directory /tmp tookeep hello downloaded files used by hello scripts and then clean them up after scripts have executed.</span></span>
* <span data-ttu-id="1aaf2-289">Jeśli ustawienia na poziomie systemu operacyjnego lub plików konfiguracyjnych usługi Hadoop są zmieniane, możesz toorestart usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-289">If OS-level settings or Hadoop service configuration files are changed, you may want toorestart HDInsight services.</span></span>

## <span data-ttu-id="1aaf2-290"><a name="runScriptAction"></a>Jak toorun akcji skryptu</span><span class="sxs-lookup"><span data-stu-id="1aaf2-290"><a name="runScriptAction"></a>How toorun a script action</span></span>

<span data-ttu-id="1aaf2-291">Można użyć skryptu akcje toocustomize klastrów usługi HDInsight przy użyciu hello następujące metody:</span><span class="sxs-lookup"><span data-stu-id="1aaf2-291">You can use script actions toocustomize HDInsight clusters using hello following methods:</span></span>

* <span data-ttu-id="1aaf2-292">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="1aaf2-292">Azure portal</span></span>
* <span data-ttu-id="1aaf2-293">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1aaf2-293">Azure PowerShell</span></span>
* <span data-ttu-id="1aaf2-294">Szablony usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1aaf2-294">Azure Resource Manager templates</span></span>
* <span data-ttu-id="1aaf2-295">Witaj zestawu .NET SDK usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-295">hello HDInsight .NET SDK.</span></span>

<span data-ttu-id="1aaf2-296">Aby uzyskać więcej informacji na temat używania każdej z metod, zobacz [jak toouse skryptu akcji](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="1aaf2-296">For more information on using each method, see [How toouse script action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <span data-ttu-id="1aaf2-297"><a name="sampleScripts"></a>Przykłady niestandardowych skryptów</span><span class="sxs-lookup"><span data-stu-id="1aaf2-297"><a name="sampleScripts"></a>Custom script samples</span></span>

<span data-ttu-id="1aaf2-298">Firma Microsoft udostępnia przykładowe skrypty tooinstall składników w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-298">Microsoft provides sample scripts tooinstall components on an HDInsight cluster.</span></span> <span data-ttu-id="1aaf2-299">Zobacz następujące łącza więcej akcji skryptu przykład hello.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-299">See hello following links for more example script actions.</span></span>

* [<span data-ttu-id="1aaf2-300">Zainstalować i używać Hue w klastrach HDInsight</span><span class="sxs-lookup"><span data-stu-id="1aaf2-300">Install and use Hue on HDInsight clusters</span></span>](hdinsight-hadoop-hue-linux.md)
* [<span data-ttu-id="1aaf2-301">Zainstalować i używać Solr w klastrach HDInsight</span><span class="sxs-lookup"><span data-stu-id="1aaf2-301">Install and use Solr on HDInsight clusters</span></span>](hdinsight-hadoop-solr-install-linux.md)
* [<span data-ttu-id="1aaf2-302">Zainstalować i używać Giraph w klastrach HDInsight</span><span class="sxs-lookup"><span data-stu-id="1aaf2-302">Install and use Giraph on HDInsight clusters</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* [<span data-ttu-id="1aaf2-303">Zainstaluj lub Uaktualnij Mono w klastrach HDInsight</span><span class="sxs-lookup"><span data-stu-id="1aaf2-303">Install or upgrade Mono on HDInsight clusters</span></span>](hdinsight-hadoop-install-mono.md)

## <a name="troubleshooting"></a><span data-ttu-id="1aaf2-304">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="1aaf2-304">Troubleshooting</span></span>

<span data-ttu-id="1aaf2-305">błędy, które mogą wystąpić podczas za pomocą skryptów, które zostały opracowane są następujące Hello:</span><span class="sxs-lookup"><span data-stu-id="1aaf2-305">hello following are errors you may encounter when using scripts you have developed:</span></span>

<span data-ttu-id="1aaf2-306">**Błąd**: `$'\r': command not found`.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-306">**Error**: `$'\r': command not found`.</span></span> <span data-ttu-id="1aaf2-307">Czasami następuje `syntax error: unexpected end of file`.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-307">Sometimes followed by `syntax error: unexpected end of file`.</span></span>

<span data-ttu-id="1aaf2-308">*Przyczyna*: ten błąd występuje, gdy hello wierszy w skrypcie kończyć CRLF.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-308">*Cause*: This error is caused when hello lines in a script end with CRLF.</span></span> <span data-ttu-id="1aaf2-309">Systemy UNIX oczekiwać tylko LF jako hello koniec wiersza.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-309">Unix systems expect only LF as hello line ending.</span></span>

<span data-ttu-id="1aaf2-310">Ten problem najczęściej występuje, gdy hello skrypt został utworzony w środowisku Windows CRLF jest linii Kończenie dla wielu edytory tekstów w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-310">This problem most often occurs when hello script is authored on a Windows environment, as CRLF is a common line ending for many text editors on Windows.</span></span>

<span data-ttu-id="1aaf2-311">*Rozdzielczość*: Jeśli jest to opcja w edytorze tekstu, wybierz format systemu Unix lub LF dla hello zakończenia wiersza.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-311">*Resolution*: If it is an option in your text editor, select Unix format or LF for hello line ending.</span></span> <span data-ttu-id="1aaf2-312">Można także użyć następujących poleceń na Unix systemu toochange hello CRLF tooan LF hello:</span><span class="sxs-lookup"><span data-stu-id="1aaf2-312">You may also use hello following commands on a Unix system toochange hello CRLF tooan LF:</span></span>

> [!NOTE]
> <span data-ttu-id="1aaf2-313">Witaj poniższe polecenia są w przybliżeniu powinny one zmieniać tooLF zakończenia wiersza CRLF hello.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-313">hello following commands are roughly equivalent in that they should change hello CRLF line endings tooLF.</span></span> <span data-ttu-id="1aaf2-314">Wybierz jedną oparte na powitania narzędzi dostępnych w systemie.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-314">Select one based on hello utilities available on your system.</span></span>

| <span data-ttu-id="1aaf2-315">Polecenie</span><span class="sxs-lookup"><span data-stu-id="1aaf2-315">Command</span></span> | <span data-ttu-id="1aaf2-316">Uwagi</span><span class="sxs-lookup"><span data-stu-id="1aaf2-316">Notes</span></span> |
| --- | --- |
| `unix2dos -b INFILE` |<span data-ttu-id="1aaf2-317">kopii zapasowej oryginalnego pliku Hello z. Rozszerzeniem BAK</span><span class="sxs-lookup"><span data-stu-id="1aaf2-317">hello original file is backed up with a .BAK extension</span></span> |
| `tr -d '\r' < INFILE > OUTFILE` |<span data-ttu-id="1aaf2-318">PLIKWYJŚCIOWY zawiera wersję z tylko LF zakończenia</span><span class="sxs-lookup"><span data-stu-id="1aaf2-318">OUTFILE contains a version with only LF endings</span></span> |
| `perl -pi -e 's/\r\n/\n/g' INFILE` | <span data-ttu-id="1aaf2-319">Modyfikuje plik hello bezpośrednio</span><span class="sxs-lookup"><span data-stu-id="1aaf2-319">Modifies hello file directly</span></span> |
| ```sed 's/$'"/`echo \\\r`/" INFILE > OUTFILE``` |<span data-ttu-id="1aaf2-320">PLIKWYJŚCIOWY zawiera wersję z tylko LF zakończenia.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-320">OUTFILE contains a version with only LF endings.</span></span> |

<span data-ttu-id="1aaf2-321">**Błąd**: `line 1: #!/usr/bin/env: No such file or directory`.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-321">**Error**: `line 1: #!/usr/bin/env: No such file or directory`.</span></span>

<span data-ttu-id="1aaf2-322">*Przyczyna*: ten błąd występuje, gdy hello skrypt został zapisany jako UTF-8 z znacznik kolejności bajtów (BOM).</span><span class="sxs-lookup"><span data-stu-id="1aaf2-322">*Cause*: This error occurs when hello script was saved as UTF-8 with a Byte Order Mark (BOM).</span></span>

<span data-ttu-id="1aaf2-323">*Rozdzielczość*: hello Zapisz albo jako ASCII lub UTF-8 bez BOM.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-323">*Resolution*: Save hello file either as ASCII, or as UTF-8 without a BOM.</span></span> <span data-ttu-id="1aaf2-324">Można także użyć następującego polecenia w systemie Linux lub Unix systemu toocreate pliku bez hello BOM hello:</span><span class="sxs-lookup"><span data-stu-id="1aaf2-324">You may also use hello following command on a Linux or Unix system toocreate a file without hello BOM:</span></span>

    awk 'NR==1{sub(/^\xef\xbb\xbf/,"")}{print}' INFILE > OUTFILE

<span data-ttu-id="1aaf2-325">Zastąp `INFILE` hello plik zawierający hello BOM.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-325">Replace `INFILE` with hello file containing hello BOM.</span></span> <span data-ttu-id="1aaf2-326">`OUTFILE`powinien być nową nazwę pliku, zawierającego hello skryptu bez hello BOM.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-326">`OUTFILE` should be a new file name, which contains hello script without hello BOM.</span></span>

## <span data-ttu-id="1aaf2-327"><a name="seeAlso"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1aaf2-327"><a name="seeAlso"></a>Next steps</span></span>

* <span data-ttu-id="1aaf2-328">Dowiedz się, jak za[HDInsight dostosować klastry za pomocą akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md)</span><span class="sxs-lookup"><span data-stu-id="1aaf2-328">Learn how too[Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>
* <span data-ttu-id="1aaf2-329">Użyj hello [odwołania do zestawu SDK .NET usługi HDInsight](https://msdn.microsoft.com/library/mt271028.aspx) toolearn więcej informacji na temat tworzenia aplikacji .NET, które zarządzają HDInsight</span><span class="sxs-lookup"><span data-stu-id="1aaf2-329">Use hello [HDInsight .NET SDK reference](https://msdn.microsoft.com/library/mt271028.aspx) toolearn more about creating .NET applications that manage HDInsight</span></span>
* <span data-ttu-id="1aaf2-330">Użyj hello [interfejsu API REST usługi HDInsight](https://msdn.microsoft.com/library/azure/mt622197.aspx) toolearn jak klastrów akcje zarządzania tooperform toouse REST w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1aaf2-330">Use hello [HDInsight REST API](https://msdn.microsoft.com/library/azure/mt622197.aspx) toolearn how toouse REST tooperform management actions on HDInsight clusters.</span></span>
