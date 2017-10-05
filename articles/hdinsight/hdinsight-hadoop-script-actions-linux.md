---
title: "Skrypt programowanie akcji z usługą HDInsight opartą na systemie Linux - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skrypty powłoki systemowej umożliwia dostosowywanie klastrów usługi HDInsight opartych na systemie Linux. Funkcja Akcja skryptu HDInsight pozwala na uruchamianie skryptów podczas lub po utworzeniu klastra. Skrypty można zmienić ustawienia konfiguracji klastra lub zainstalować dodatkowe oprogramowanie."
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
ms.openlocfilehash: 7f1a0bd8c7e60770d376f10eaea136a55c632c5e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="script-action-development-with-hdinsight"></a><span data-ttu-id="ef9b7-105">Tworzenie akcji skryptu za pomocą usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="ef9b7-105">Script action development with HDInsight</span></span>

<span data-ttu-id="ef9b7-106">Dowiedz się, jak dostosować z klastrem usługi HDInsight przy użyciu skrypty Bash.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-106">Learn how to customize your HDInsight cluster using Bash scripts.</span></span> <span data-ttu-id="ef9b7-107">Akcje skryptu to sposób, aby dostosować HDInsight podczas lub po utworzeniu klastra.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-107">Script actions are a way to customize HDInsight during or after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ef9b7-108">Kroki opisane w tym dokumencie wymagają klastra usługi HDInsight, który używa systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-108">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="ef9b7-109">Linux jest jedynym systemem operacyjnym używanym w połączeniu z usługą HDInsight w wersji 3.4 lub nowszą.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ef9b7-110">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="ef9b7-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="what-are-script-actions"></a><span data-ttu-id="ef9b7-111">Co to są akcji skryptu</span><span class="sxs-lookup"><span data-stu-id="ef9b7-111">What are script actions</span></span>

<span data-ttu-id="ef9b7-112">Akcje skryptu to skrypty Bash, które Azure działa na węzłach klastra dokonać zmian konfiguracji lub instalacja oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-112">Script actions are Bash scripts that Azure runs on the cluster nodes to make configuration changes or install software.</span></span> <span data-ttu-id="ef9b7-113">Akcja skryptu jest wykonywany jako główny i zapewnia pełne prawa dostępu do węzłów klastra.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-113">A script action is executed as root, and provides full access rights to the cluster nodes.</span></span>

<span data-ttu-id="ef9b7-114">Akcje skryptu można zastosować za pomocą następujących metod:</span><span class="sxs-lookup"><span data-stu-id="ef9b7-114">Script actions can be applied through the following methods:</span></span>

| <span data-ttu-id="ef9b7-115">Ta metoda umożliwia zastosowanie skryptu...</span><span class="sxs-lookup"><span data-stu-id="ef9b7-115">Use this method to apply a script...</span></span> | <span data-ttu-id="ef9b7-116">Tworzenie klastra podczas...</span><span class="sxs-lookup"><span data-stu-id="ef9b7-116">During cluster creation...</span></span> | <span data-ttu-id="ef9b7-117">W klastrze uruchomione...</span><span class="sxs-lookup"><span data-stu-id="ef9b7-117">On a running cluster...</span></span> |
| --- |:---:|:---:|
| <span data-ttu-id="ef9b7-118">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ef9b7-118">Azure portal</span></span> |<span data-ttu-id="ef9b7-119">✓</span><span class="sxs-lookup"><span data-stu-id="ef9b7-119">✓</span></span> |<span data-ttu-id="ef9b7-120">✓</span><span class="sxs-lookup"><span data-stu-id="ef9b7-120">✓</span></span> |
| <span data-ttu-id="ef9b7-121">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ef9b7-121">Azure PowerShell</span></span> |<span data-ttu-id="ef9b7-122">✓</span><span class="sxs-lookup"><span data-stu-id="ef9b7-122">✓</span></span> |<span data-ttu-id="ef9b7-123">✓</span><span class="sxs-lookup"><span data-stu-id="ef9b7-123">✓</span></span> |
| <span data-ttu-id="ef9b7-124">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ef9b7-124">Azure CLI</span></span> |&nbsp; |<span data-ttu-id="ef9b7-125">✓</span><span class="sxs-lookup"><span data-stu-id="ef9b7-125">✓</span></span> |
| <span data-ttu-id="ef9b7-126">Zestaw SDK dla platformy .NET usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="ef9b7-126">HDInsight .NET SDK</span></span> |<span data-ttu-id="ef9b7-127">✓</span><span class="sxs-lookup"><span data-stu-id="ef9b7-127">✓</span></span> |<span data-ttu-id="ef9b7-128">✓</span><span class="sxs-lookup"><span data-stu-id="ef9b7-128">✓</span></span> |
| <span data-ttu-id="ef9b7-129">Szablonu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ef9b7-129">Azure Resource Manager Template</span></span> |<span data-ttu-id="ef9b7-130">✓</span><span class="sxs-lookup"><span data-stu-id="ef9b7-130">✓</span></span> |&nbsp; |

<span data-ttu-id="ef9b7-131">Aby uzyskać więcej informacji o używaniu tych metod do zastosowania akcji skryptu, zobacz [HDInsight dostosować klastry za pomocą akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="ef9b7-131">For more information on using these methods to apply script actions, see [Customize HDInsight clusters using script actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <span data-ttu-id="ef9b7-132"><a name="bestPracticeScripting"></a>Najlepsze rozwiązania dotyczące tworzenia skryptów</span><span class="sxs-lookup"><span data-stu-id="ef9b7-132"><a name="bestPracticeScripting"></a>Best practices for script development</span></span>

<span data-ttu-id="ef9b7-133">Podczas opracowywania niestandardowego skryptu dla klastra usługi HDInsight, istnieje kilka najlepszych rozwiązań, które należy wziąć pod uwagę:</span><span class="sxs-lookup"><span data-stu-id="ef9b7-133">When you develop a custom script for an HDInsight cluster, there are several best practices to keep in mind:</span></span>

* [<span data-ttu-id="ef9b7-134">Docelowa wersja platformy Hadoop</span><span class="sxs-lookup"><span data-stu-id="ef9b7-134">Target the Hadoop version</span></span>](#bPS1)
* [<span data-ttu-id="ef9b7-135">Docelowa wersja systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="ef9b7-135">Target the OS Version</span></span>](#bps10)
* [<span data-ttu-id="ef9b7-136">Podaj stabilna linki do zasobów skryptu</span><span class="sxs-lookup"><span data-stu-id="ef9b7-136">Provide stable links to script resources</span></span>](#bPS2)
* [<span data-ttu-id="ef9b7-137">Użyj wstępnie skompilowanym zasobów</span><span class="sxs-lookup"><span data-stu-id="ef9b7-137">Use pre-compiled resources</span></span>](#bPS4)
* [<span data-ttu-id="ef9b7-138">Upewnij się, że skrypt dostosowywania klastra jest idempotentności</span><span class="sxs-lookup"><span data-stu-id="ef9b7-138">Ensure that the cluster customization script is idempotent</span></span>](#bPS3)
* [<span data-ttu-id="ef9b7-139">Zapewni to wysoką dostępność architektury klastra</span><span class="sxs-lookup"><span data-stu-id="ef9b7-139">Ensure high availability of the cluster architecture</span></span>](#bPS5)
* [<span data-ttu-id="ef9b7-140">Konfigurowanie niestandardowych składników można używać magazynu obiektów Blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ef9b7-140">Configure the custom components to use Azure Blob storage</span></span>](#bPS6)
* [<span data-ttu-id="ef9b7-141">Zapisywanie informacji o STDOUT i STDERR.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-141">Write information to STDOUT and STDERR</span></span>](#bPS7)
* [<span data-ttu-id="ef9b7-142">Zapisz pliki jako ASCII z końców LF</span><span class="sxs-lookup"><span data-stu-id="ef9b7-142">Save files as ASCII with LF line endings</span></span>](#bps8)
* [<span data-ttu-id="ef9b7-143">Logika ponawiania umożliwia odzyskanie w przypadku błędów przejściowych</span><span class="sxs-lookup"><span data-stu-id="ef9b7-143">Use retry logic to recover from transient errors</span></span>](#bps9)

> [!IMPORTANT]
> <span data-ttu-id="ef9b7-144">Akcje skryptu należy zakończyć w ciągu 60 minut lub proces nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-144">Script actions must complete within 60 minutes or the process fails.</span></span> <span data-ttu-id="ef9b7-145">Podczas inicjowania obsługi węzła, skrypt zostanie uruchomiony równocześnie z innymi procesami instalacji i konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-145">During node provisioning, the script runs concurrently with other setup and configuration processes.</span></span> <span data-ttu-id="ef9b7-146">Konkurowanie o zasoby, takie jak czas lub sieci przepustowości Procesora może powodować skrypt potrwać dłużej niż w środowisku projektowania.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-146">Competition for resources such as CPU time or network bandwidth may cause the script to take longer to finish than it does in your development environment.</span></span>

### <span data-ttu-id="ef9b7-147"><a name="bPS1"></a>Docelowa wersja platformy Hadoop</span><span class="sxs-lookup"><span data-stu-id="ef9b7-147"><a name="bPS1"></a>Target the Hadoop version</span></span>

<span data-ttu-id="ef9b7-148">Różne wersje HDInsight korzystają z różnych wersji usług Hadoop i zainstalowanych składników.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-148">Different versions of HDInsight have different versions of Hadoop services and components installed.</span></span> <span data-ttu-id="ef9b7-149">Jeśli skrypt oczekuje określoną wersję usługi lub składnika, skrypt należy używać tylko z wersją HDInsight, która zawiera wymagane składniki.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-149">If your script expects a specific version of a service or component, you should only use the script with the version of HDInsight that includes the required components.</span></span> <span data-ttu-id="ef9b7-150">Można znaleźć informacje o wersji składników uwzględnionych w usłudze HDInsight przy użyciu [przechowywanie wersji składnika usługi HDInsight](hdinsight-component-versioning.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-150">You can find information on component versions included with HDInsight using the [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

### <span data-ttu-id="ef9b7-151"><a name="bps10"></a>Docelowa wersja systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="ef9b7-151"><a name="bps10"></a> Target the OS version</span></span>

<span data-ttu-id="ef9b7-152">HDInsight opartych na systemie Linux jest oparta na dystrybucji Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-152">Linux-based HDInsight is based on the Ubuntu Linux distribution.</span></span> <span data-ttu-id="ef9b7-153">Różnych wersji usługi hdinsight korzystają z różnych wersji systemu Ubuntu, która może zmienić sposób działania skryptu.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-153">Different versions of HDInsight rely on different versions of Ubuntu, which may change how your script behaves.</span></span> <span data-ttu-id="ef9b7-154">Na przykład HDInsight 3.4 i starsze wersje są oparte na wersji Ubuntu, które używają Upstart.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-154">For example, HDInsight 3.4 and earlier are based on Ubuntu versions that use Upstart.</span></span> <span data-ttu-id="ef9b7-155">Wersja 3.5 jest oparta na 16.04 Ubuntu, który używa Systemd.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-155">Version 3.5 is based on Ubuntu 16.04, which uses Systemd.</span></span> <span data-ttu-id="ef9b7-156">Systemd i Upstart zależne inne polecenia, aby skrypt powinien być zapisywany do pracy z programem.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-156">Systemd and Upstart rely on different commands, so your script should be written to work with both.</span></span>

<span data-ttu-id="ef9b7-157">Inna ważna różnica między HDInsight 3.4 i 3.5 jest to, że `JAVA_HOME` teraz wskazuje Java 8.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-157">Another important difference between HDInsight 3.4 and 3.5 is that `JAVA_HOME` now points to Java 8.</span></span>

<span data-ttu-id="ef9b7-158">Wersja systemu operacyjnego można sprawdzić za pomocą `lsb_release`.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-158">You can check the OS version by using `lsb_release`.</span></span> <span data-ttu-id="ef9b7-159">Poniższy kod przedstawia sposób określania, czy skrypt jest uruchomiony na Ubuntu 14 lub 16:</span><span class="sxs-lookup"><span data-stu-id="ef9b7-159">The following code demonstrates how to determine if the script is running on Ubuntu 14 or 16:</span></span>

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

<span data-ttu-id="ef9b7-160">Można znaleźć pełnej skrypt, który zawiera te wstawki na https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-160">You can find the full script that contains these snippets at https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh.</span></span>

<span data-ttu-id="ef9b7-161">Wersja Ubuntu, który jest używany przez usługi HDInsight dla [składnika usługi HDInsight w wersji](hdinsight-component-versioning.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-161">For the version of Ubuntu that is used by HDInsight, see the [HDInsight component version](hdinsight-component-versioning.md) document.</span></span>

<span data-ttu-id="ef9b7-162">Aby poznać różnice między Systemd i Upstart, zobacz [Systemd dla użytkowników Upstart](https://wiki.ubuntu.com/SystemdForUpstartUsers).</span><span class="sxs-lookup"><span data-stu-id="ef9b7-162">To understand the differences between Systemd and Upstart, see [Systemd for Upstart users](https://wiki.ubuntu.com/SystemdForUpstartUsers).</span></span>

### <span data-ttu-id="ef9b7-163"><a name="bPS2"></a>Podaj stabilna linki do zasobów skryptu</span><span class="sxs-lookup"><span data-stu-id="ef9b7-163"><a name="bPS2"></a>Provide stable links to script resources</span></span>

<span data-ttu-id="ef9b7-164">Skrypt i skojarzonych zasobów musi być dostępna przez cały cykl życia klastra.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-164">The script and associated resources must remain available throughout the lifetime of the cluster.</span></span> <span data-ttu-id="ef9b7-165">Te zasoby są wymagane, jeśli zostaną dodane nowe węzły do klastra podczas operacji skalowania.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-165">These resources are required if new nodes are added to the cluster during scaling operations.</span></span>

<span data-ttu-id="ef9b7-166">Najlepszym rozwiązaniem jest, aby pobrać i zarchiwizowanie wszystkich na koncie magazynu Azure w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-166">The best practice is to download and archive everything in an Azure Storage account on your subscription.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ef9b7-167">Konto magazynu używane musi być domyślne konto magazynu dla klastra lub kontener publiczne, tylko do odczytu na inne konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-167">The storage account used must be the default storage account for the cluster or a public, read-only container on any other storage account.</span></span>

<span data-ttu-id="ef9b7-168">Na przykład przykłady obsługiwane przez firmę Microsoft są przechowywane w [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/) konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-168">For example, the samples provided by Microsoft are stored in the [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/) storage account.</span></span> <span data-ttu-id="ef9b7-169">To jest kontenerem publiczne, tylko do odczytu obsługiwanego przez zespół usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-169">This is a public, read-only container maintained by the HDInsight team.</span></span>

### <span data-ttu-id="ef9b7-170"><a name="bPS4"></a>Użyj wstępnie skompilowanym zasobów</span><span class="sxs-lookup"><span data-stu-id="ef9b7-170"><a name="bPS4"></a>Use pre-compiled resources</span></span>

<span data-ttu-id="ef9b7-171">Aby skrócić czas wymagany do uruchomienia skryptu, należy unikać operacji kompilowane zasobów z kodu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-171">To reduce the time it takes to run the script, avoid operations that compile resources from source code.</span></span> <span data-ttu-id="ef9b7-172">Na przykład wstępnie skompilować zasobów i przechowywać je w obiekcie blob konta magazynu Azure w tym samym centrum danych jako HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-172">For example, pre-compile resources and store them in an Azure Storage account blob in the same data center as HDInsight.</span></span>

### <span data-ttu-id="ef9b7-173"><a name="bPS3"></a>Upewnij się, że skrypt dostosowywania klastra jest idempotentności</span><span class="sxs-lookup"><span data-stu-id="ef9b7-173"><a name="bPS3"></a>Ensure that the cluster customization script is idempotent</span></span>

<span data-ttu-id="ef9b7-174">Skrypty musi być idempotentności.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-174">Scripts must be idempotent.</span></span> <span data-ttu-id="ef9b7-175">Jeśli skrypt jest uruchamiany wiele razy, jego powinien zwrócić klastra do tego samego stanu zawsze.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-175">If the script runs multiple times, it should return the cluster to the same state every time.</span></span>

<span data-ttu-id="ef9b7-176">Na przykład skrypt, który modyfikuje pliki konfiguracji nie dodać zduplikowanych wpisów, gdy uruchomiono wiele razy.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-176">For example, a script that modifies configuration files should not add duplicate entries if ran multiple times.</span></span>

### <span data-ttu-id="ef9b7-177"><a name="bPS5"></a>Zapewni to wysoką dostępność architektury klastra</span><span class="sxs-lookup"><span data-stu-id="ef9b7-177"><a name="bPS5"></a>Ensure high availability of the cluster architecture</span></span>

<span data-ttu-id="ef9b7-178">Klastry HDInsight opartych na systemie Linux zapewniają dwa węzły head, które są aktywne w klastrze, a akcji skryptu, uruchom na obu węzłów.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-178">Linux-based HDInsight clusters provide two head nodes that are active within the cluster, and script actions run on both nodes.</span></span> <span data-ttu-id="ef9b7-179">Jeśli składniki, które będą instalowane oczekuje tylko jednego węzła głównego, nie należy instalować na obu węzłów głównych składników.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-179">If the components you install expect only one head node, do not install the components on both head nodes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ef9b7-180">Usługi w ramach usługi HDInsight zostały zaprojektowane do pracy awaryjnej między dwoma węzłami head, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-180">Services provided as part of HDInsight are designed to fail over between the two head nodes as needed.</span></span> <span data-ttu-id="ef9b7-181">Ta funkcja nie jest rozszerzony do niestandardowe składniki zainstalowane za pomocą akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-181">This functionality is not extended to custom components installed through script actions.</span></span> <span data-ttu-id="ef9b7-182">Jeśli potrzebujesz wysokiej dostępności dla niestandardowych składników, musisz zaimplementować własny mechanizm pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-182">If you need high availability for custom components, you must implement your own failover mechanism.</span></span>

### <span data-ttu-id="ef9b7-183"><a name="bPS6"></a>Konfigurowanie niestandardowych składników można używać magazynu obiektów Blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ef9b7-183"><a name="bPS6"></a>Configure the custom components to use Azure Blob storage</span></span>

<span data-ttu-id="ef9b7-184">Składniki, które można zainstalować w klastrze może być konfigurację domyślną, która korzysta z magazynu systemu Distributed plików Hadoop (HDFS).</span><span class="sxs-lookup"><span data-stu-id="ef9b7-184">Components that you install on the cluster might have a default configuration that uses Hadoop Distributed File System (HDFS) storage.</span></span> <span data-ttu-id="ef9b7-185">HDInsight używa magazynu Azure lub usługi Data Lake Store jako domyślnego magazynu.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-185">HDInsight uses either Azure Storage or Data Lake Store as the default storage.</span></span> <span data-ttu-id="ef9b7-186">Podaj zarówno systemu plików zgodny system plików HDFS, który będzie się powtarzał danych, nawet jeśli klaster zostanie usunięty.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-186">Both provide an HDFS compatible file system that persists data even if the cluster is deleted.</span></span> <span data-ttu-id="ef9b7-187">Może być konieczne skonfigurowanie składników, które można zainstalować, aby użyć WASB lub ADL zamiast systemu plików HDFS.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-187">You may need to configure components you install to use WASB or ADL instead of HDFS.</span></span>

<span data-ttu-id="ef9b7-188">Dla większości operacji nie trzeba określić system plików.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-188">For most operations, you do not need to specify the file system.</span></span> <span data-ttu-id="ef9b7-189">Na przykład następujące kopiuje plik giraph-examples.jar z lokalnego systemu plików do magazynu klastra:</span><span class="sxs-lookup"><span data-stu-id="ef9b7-189">For example, the following copies the giraph-examples.jar file from the local file system to cluster storage:</span></span>

```bash
hdfs dfs -put /usr/hdp/current/giraph/giraph-examples.jar /example/jars/
```

<span data-ttu-id="ef9b7-190">W tym przykładzie `hdfs` polecenie niewidocznie używa domyślnego magazynu klastra.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-190">In this example, the `hdfs` command transparently uses the default cluster storage.</span></span> <span data-ttu-id="ef9b7-191">Dla niektórych operacji może być konieczne Określ identyfikator URI.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-191">For some operations, you may need to specify the URI.</span></span> <span data-ttu-id="ef9b7-192">Na przykład `adl:///example/jars` dla usługi Data Lake Store lub `wasb:///example/jars` usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-192">For example, `adl:///example/jars` for Data Lake Store or `wasb:///example/jars` for Azure Storage.</span></span>

### <span data-ttu-id="ef9b7-193"><a name="bPS7"></a>Zapisywanie informacji o STDOUT i STDERR.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-193"><a name="bPS7"></a>Write information to STDOUT and STDERR</span></span>

<span data-ttu-id="ef9b7-194">HDInsight rejestruje dane wyjściowe skryptu, które są zapisywane do strumienia wyjściowego STDOUT i STDERR.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-194">HDInsight logs script output that is written to STDOUT and STDERR.</span></span> <span data-ttu-id="ef9b7-195">Można wyświetlić te informacje przy użyciu interfejsu użytkownika sieci web Ambari.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-195">You can view this information using the Ambari web UI.</span></span>

> [!NOTE]
> <span data-ttu-id="ef9b7-196">Ambari jest dostępna tylko jeśli klaster został utworzony pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-196">Ambari is only available if the cluster is successfully created.</span></span> <span data-ttu-id="ef9b7-197">Jeśli używasz akcji skryptu podczas tworzenia klastra i utworzenie kończy się niepowodzeniem, zobacz sekcję dotyczącą rozwiązywania problemów [HDInsight dostosować klastry za pomocą akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) dotyczące innych metod uzyskiwania dostępu do zarejestrowane informacje.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-197">If you use a script action during cluster creation, and creation fails, see the troubleshooting section [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) for other ways of accessing logged information.</span></span>

<span data-ttu-id="ef9b7-198">Większość narzędzi i pakiety instalacyjne już zapisuje informacje o do STDOUT i STDERR, jednak można dodać dodatkowe rejestrowanie.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-198">Most utilities and installation packages already write information to STDOUT and STDERR, however you may want to add additional logging.</span></span> <span data-ttu-id="ef9b7-199">Aby wysłać tekst do STDOUT, należy użyć `echo`.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-199">To send text to STDOUT, use `echo`.</span></span> <span data-ttu-id="ef9b7-200">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="ef9b7-200">For example:</span></span>

```bash
echo "Getting ready to install Foo"
```

<span data-ttu-id="ef9b7-201">Domyślnie `echo` wysyła ciąg do STDOUT.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-201">By default, `echo` sends the string to STDOUT.</span></span> <span data-ttu-id="ef9b7-202">Aby skierować ją stderr, Dodaj `>&2` przed `echo`.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-202">To direct it to STDERR, add `>&2` before `echo`.</span></span> <span data-ttu-id="ef9b7-203">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="ef9b7-203">For example:</span></span>

```bash
>&2 echo "An error occurred installing Foo"
```

<span data-ttu-id="ef9b7-204">To przekierowuje informacje zapisane zamiast tego do STDOUT stderr (2).</span><span class="sxs-lookup"><span data-stu-id="ef9b7-204">This redirects information written to STDOUT to STDERR (2) instead.</span></span> <span data-ttu-id="ef9b7-205">Aby uzyskać więcej informacji dotyczących przekierowania we/wy, zobacz [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html).</span><span class="sxs-lookup"><span data-stu-id="ef9b7-205">For more information on IO redirection, see [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html).</span></span>

<span data-ttu-id="ef9b7-206">Aby uzyskać więcej informacji o wyświetlaniu informacji zarejestrowanych przez akcje skryptu, zobacz [HDInsight dostosować klastry za pomocą akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)</span><span class="sxs-lookup"><span data-stu-id="ef9b7-206">For more information on viewing information logged by script actions, see [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)</span></span>

### <span data-ttu-id="ef9b7-207"><a name="bps8"></a>Zapisz pliki jako ASCII z końców LF</span><span class="sxs-lookup"><span data-stu-id="ef9b7-207"><a name="bps8"></a> Save files as ASCII with LF line endings</span></span>

<span data-ttu-id="ef9b7-208">Skrypty powłoki systemowej powinny być przechowywane w formacie ASCII, liniami został przerwany przez wysuwu wiersza.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-208">Bash scripts should be stored as ASCII format, with lines terminated by LF.</span></span> <span data-ttu-id="ef9b7-209">Pliki, które są przechowywane w formacie UTF-8, lub użyj CRLF jako zakończenie wiersza może zakończyć się niepowodzeniem z powodu następującego błędu:</span><span class="sxs-lookup"><span data-stu-id="ef9b7-209">Files that are stored as UTF-8, or use CRLF as the line ending may fail with the following error:</span></span>

```
$'\r': command not found
line 1: #!/usr/bin/env: No such file or directory
```

### <span data-ttu-id="ef9b7-210"><a name="bps9"></a>Logika ponawiania umożliwia odzyskanie w przypadku błędów przejściowych</span><span class="sxs-lookup"><span data-stu-id="ef9b7-210"><a name="bps9"></a> Use retry logic to recover from transient errors</span></span>

<span data-ttu-id="ef9b7-211">Pobieranie plików, instalowanie pakietów przy użyciu stanie get lub innych działań, których dane są przesyłane za pośrednictwem Internetu, akcja może zakończyć się niepowodzeniem z powodu przejściowych błędów sieci.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-211">When downloading files, installing packages using apt-get, or other actions that transmit data over the internet, the action may fail due to transient networking errors.</span></span> <span data-ttu-id="ef9b7-212">Na przykład zasób zdalny, które komunikują się z może być w trakcie awarii węzła kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-212">For example, the remote resource you are communicating with may be in the process of failing over to a backup node.</span></span>

<span data-ttu-id="ef9b7-213">Aby skrypt odporność błędów przejściowych, można implementację logiki ponawiania próby.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-213">To make your script resilient to transient errors, you can implement retry logic.</span></span> <span data-ttu-id="ef9b7-214">Następująca funkcja demonstracja implementację logiki ponawiania próby.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-214">The following function demonstrates how to implement retry logic.</span></span> <span data-ttu-id="ef9b7-215">Ponowną operacji trzy razy przed niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-215">It retries the operation three times before failing.</span></span>

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

<span data-ttu-id="ef9b7-216">Poniższe przykłady pokazują, jak użyć tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-216">The following examples demonstrate how to use this function.</span></span>

```bash
retry ls -ltr foo

retry wget -O ./tmpfile.sh https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh
```

## <span data-ttu-id="ef9b7-217"><a name="helpermethods"></a>Metody pomocnicze dla niestandardowych skryptów</span><span class="sxs-lookup"><span data-stu-id="ef9b7-217"><a name="helpermethods"></a>Helper methods for custom scripts</span></span>

<span data-ttu-id="ef9b7-218">Metody pomocnicze akcji skryptu są narzędzia, które można użyć podczas pisania skryptów niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-218">Script action helper methods are utilities that you can use while writing custom scripts.</span></span> <span data-ttu-id="ef9b7-219">Te metody są zawarte w[https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh) skryptu.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-219">These methods are contained in the[https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh) script.</span></span> <span data-ttu-id="ef9b7-220">Pobranie i użycie ich jako część skryptu należy wykonać następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="ef9b7-220">Use the following to download and use them as part of your script:</span></span>

```bash
# Import the helper method module.
wget -O /tmp/HDInsightUtilities-v01.sh -q https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh && source /tmp/HDInsightUtilities-v01.sh && rm -f /tmp/HDInsightUtilities-v01.sh
```

<span data-ttu-id="ef9b7-221">Następujące pomocników dostępne do użycia w skrypcie:</span><span class="sxs-lookup"><span data-stu-id="ef9b7-221">The following helpers available for use in your script:</span></span>

| <span data-ttu-id="ef9b7-222">Użycie pomocnika</span><span class="sxs-lookup"><span data-stu-id="ef9b7-222">Helper usage</span></span> | <span data-ttu-id="ef9b7-223">Opis</span><span class="sxs-lookup"><span data-stu-id="ef9b7-223">Description</span></span> |
| --- | --- |
| `download_file SOURCEURL DESTFILEPATH [OVERWRITE]` |<span data-ttu-id="ef9b7-224">Pobiera ze źródła identyfikatora URI pliku określona ścieżka pliku.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-224">Downloads a file from the source URI to the specified file path.</span></span> <span data-ttu-id="ef9b7-225">Domyślnie go nie zastępuj istniejącego pliku.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-225">By default, it does not overwrite an existing file.</span></span> |
| `untar_file TARFILE DESTDIR` |<span data-ttu-id="ef9b7-226">Wyodrębnia plik tar (przy użyciu `-xf`) do katalogu docelowego.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-226">Extracts a tar file (using `-xf`) to the destination directory.</span></span> |
| `test_is_headnode` |<span data-ttu-id="ef9b7-227">Jeśli został uruchomiony na węzła głównego klastra zwracany 1; w przeciwnym razie wartość 0.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-227">If ran on a cluster head node, return 1; otherwise, 0.</span></span> |
| `test_is_datanode` |<span data-ttu-id="ef9b7-228">Jeśli bieżący węzeł jest węzłem danych (proces roboczy), zwraca 1; w przeciwnym razie wartość 0.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-228">If the current node is a data (worker) node, return a 1; otherwise, 0.</span></span> |
| `test_is_first_datanode` |<span data-ttu-id="ef9b7-229">W przypadku bieżącego węzła jest pierwsze dane (proces roboczy) węzła (o nazwie workernode0) zwraca 1; w przeciwnym razie wartość 0.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-229">If the current node is the first data (worker) node (named workernode0) return a 1; otherwise, 0.</span></span> |
| `get_headnodes` |<span data-ttu-id="ef9b7-230">Zwraca w pełni kwalifikowaną nazwę domeny z headnodes w klastrze.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-230">Return the fully qualified domain name of the headnodes in the cluster.</span></span> <span data-ttu-id="ef9b7-231">Nazwy są rozdzielone przecinkami.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-231">Names are comma delimited.</span></span> <span data-ttu-id="ef9b7-232">Ciąg pusty jest zwracana w przypadku błędu.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-232">An empty string is returned on error.</span></span> |
| `get_primary_headnode` |<span data-ttu-id="ef9b7-233">Pobiera nazwę FQDN headnode podstawowego.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-233">Gets the fully qualified domain name of the primary headnode.</span></span> <span data-ttu-id="ef9b7-234">Ciąg pusty jest zwracana w przypadku błędu.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-234">An empty string is returned on error.</span></span> |
| `get_secondary_headnode` |<span data-ttu-id="ef9b7-235">Pobiera nazwę FQDN headnode dodatkowej.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-235">Gets the fully qualified domain name of the secondary headnode.</span></span> <span data-ttu-id="ef9b7-236">Ciąg pusty jest zwracana w przypadku błędu.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-236">An empty string is returned on error.</span></span> |
| `get_primary_headnode_number` |<span data-ttu-id="ef9b7-237">Pobiera liczbowego sufiksu podstawowej headnode.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-237">Gets the numeric suffix of the primary headnode.</span></span> <span data-ttu-id="ef9b7-238">Ciąg pusty jest zwracana w przypadku błędu.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-238">An empty string is returned on error.</span></span> |
| `get_secondary_headnode_number` |<span data-ttu-id="ef9b7-239">Pobiera sufiks numeryczny z headnode dodatkowej.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-239">Gets the numeric suffix of the secondary headnode.</span></span> <span data-ttu-id="ef9b7-240">Ciąg pusty jest zwracana w przypadku błędu.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-240">An empty string is returned on error.</span></span> |

## <span data-ttu-id="ef9b7-241"><a name="commonusage"></a>Wspólne wzorce użycia</span><span class="sxs-lookup"><span data-stu-id="ef9b7-241"><a name="commonusage"></a>Common usage patterns</span></span>

<span data-ttu-id="ef9b7-242">Ta sekcja zawiera wskazówki dotyczące implementowania niektóre typowe wzorce użycia, które możesz napotkać podczas pisania skryptu niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-242">This section provides guidance on implementing some of the common usage patterns that you might run into while writing your own custom script.</span></span>

### <a name="passing-parameters-to-a-script"></a><span data-ttu-id="ef9b7-243">Przekazywanie parametrów do skryptu</span><span class="sxs-lookup"><span data-stu-id="ef9b7-243">Passing parameters to a script</span></span>

<span data-ttu-id="ef9b7-244">W niektórych przypadkach skrypt może wymagać parametrów.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-244">In some cases, your script may require parameters.</span></span> <span data-ttu-id="ef9b7-245">Na przykład mogą być potrzebne hasło administratora klastra, korzystając z interfejsu API REST Ambari.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-245">For example, you may need the admin password for the cluster when using the Ambari REST API.</span></span>

<span data-ttu-id="ef9b7-246">Parametry przekazywane do skryptu są określane jako *parametrów pozycyjnych*i są przypisane do `$1` jako pierwszy parametr `$2` sekundy i dlatego w przypadku.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-246">Parameters passed to the script are known as *positional parameters*, and are assigned to `$1` for the first parameter, `$2` for the second, and so-on.</span></span> <span data-ttu-id="ef9b7-247">`$0`zawiera nazwę sam skrypt.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-247">`$0` contains the name of the script itself.</span></span>

<span data-ttu-id="ef9b7-248">Wartości przekazywane do skryptu jako parametry powinna zostać ujęta w apostrofy (').</span><span class="sxs-lookup"><span data-stu-id="ef9b7-248">Values passed to the script as parameters should be enclosed by single quotes (').</span></span> <span data-ttu-id="ef9b7-249">Daje to gwarancję, że przekazana wartość jest traktowany jako literału.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-249">Doing so ensures that the passed value is treated as a literal.</span></span>

### <a name="setting-environment-variables"></a><span data-ttu-id="ef9b7-250">Ustawianie zmiennych środowiskowych</span><span class="sxs-lookup"><span data-stu-id="ef9b7-250">Setting environment variables</span></span>

<span data-ttu-id="ef9b7-251">Ustawienie zmiennej środowiskowej jest wykonywane przez następująca instrukcja:</span><span class="sxs-lookup"><span data-stu-id="ef9b7-251">Setting an environment variable is performed by the following statement:</span></span>

    VARIABLENAME=value

<span data-ttu-id="ef9b7-252">Gdzie NAZWA_ZMIENNEJ to nazwa zmiennej.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-252">Where VARIABLENAME is the name of the variable.</span></span> <span data-ttu-id="ef9b7-253">Aby uzyskać dostęp do zmiennej, należy użyć `$VARIABLENAME`.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-253">To access the variable, use `$VARIABLENAME`.</span></span> <span data-ttu-id="ef9b7-254">Na przykład można przypisać dla wartości dostarczonej przez parametrów pozycyjnych jako zmienną środowiskową o nazwie HASŁA, należy użyć następującej instrukcji:</span><span class="sxs-lookup"><span data-stu-id="ef9b7-254">For example, to assign a value provided by a positional parameter as an environment variable named PASSWORD, you would use the following statement:</span></span>

    PASSWORD=$1

<span data-ttu-id="ef9b7-255">Następnie można użyć kolejnych dostępu do informacji `$PASSWORD`.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-255">Subsequent access to the information could then use `$PASSWORD`.</span></span>

<span data-ttu-id="ef9b7-256">Zmienne środowiskowe w skrypt istnieje tylko w zakresie skryptu.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-256">Environment variables set within the script only exist within the scope of the script.</span></span> <span data-ttu-id="ef9b7-257">W niektórych przypadkach może być konieczne dodanie zmiennych środowiskowych na poziomie całego systemu, zachowywanych po zakończeniu działania skryptu.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-257">In some cases, you may need to add system-wide environment variables that will persist after the script has finished.</span></span> <span data-ttu-id="ef9b7-258">Aby dodać zmiennych środowiskowych na poziomie całego systemu, należy dodać zmienną `/etc/environment`.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-258">To add system-wide environment variables, add the variable to `/etc/environment`.</span></span> <span data-ttu-id="ef9b7-259">Na przykład następująca instrukcja dodaje `HADOOP_CONF_DIR`:</span><span class="sxs-lookup"><span data-stu-id="ef9b7-259">For example, the following statement adds `HADOOP_CONF_DIR`:</span></span>

```bash
echo "HADOOP_CONF_DIR=/etc/hadoop/conf" | sudo tee -a /etc/environment
```

### <a name="access-to-locations-where-the-custom-scripts-are-stored"></a><span data-ttu-id="ef9b7-260">Dostęp do lokalizacji, w którym są przechowywane niestandardowe skrypty</span><span class="sxs-lookup"><span data-stu-id="ef9b7-260">Access to locations where the custom scripts are stored</span></span>

<span data-ttu-id="ef9b7-261">Skrypty używane w celu dostosowania klastra musi być przechowywany w jednym z następujących lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="ef9b7-261">Scripts used to customize a cluster needs to be stored in one of the following locations:</span></span>

* <span data-ttu-id="ef9b7-262">__Konta magazynu Azure__ skojarzonego z klastrem.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-262">An __Azure Storage account__ that is associated with the cluster.</span></span>

* <span data-ttu-id="ef9b7-263">__Konta magazynu dodatkowe__ skojarzony z klastrem.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-263">An __additional storage account__ associated with the cluster.</span></span>

* <span data-ttu-id="ef9b7-264">A __publicznie można odczytać identyfikatora URI__.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-264">A __publicly readable URI__.</span></span> <span data-ttu-id="ef9b7-265">Na przykład adres URL, do danych przechowywanych na OneDrive, Dropbox lub innych plików obsługującego usługę.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-265">For example, a URL to data stored on OneDrive, Dropbox, or other file hosting service.</span></span>

* <span data-ttu-id="ef9b7-266">__Konta usługi Azure Data Lake Store__ skojarzonego z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-266">An __Azure Data Lake Store account__ that is associated with the HDInsight cluster.</span></span> <span data-ttu-id="ef9b7-267">Aby uzyskać więcej informacji na temat używania usługi Azure Data Lake Store z usługą HDInsight, zobacz [tworzenia klastra usługi HDInsight z usługą Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ef9b7-267">For more information on using Azure Data Lake Store with HDInsight, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="ef9b7-268">Nazwy głównej usługi, które HDInsight używa do uzyskiwania dostępu usługi Data Lake Store musi mieć dostęp do odczytu do skryptu.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-268">The service principal HDInsight uses to access Data Lake Store must have read access to the script.</span></span>

<span data-ttu-id="ef9b7-269">Zasoby używane przez skrypt również musi być publicznie dostępny.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-269">Resources used by the script must also be publicly available.</span></span>

<span data-ttu-id="ef9b7-270">Przechowywanie plików w koncie magazynu Azure lub usługi Azure Data Lake Store zapewnia szybki dostęp, jako zarówno w ramach sieci platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-270">Storing the files in an Azure Storage account or Azure Data Lake Store provides fast access, as both within the Azure network.</span></span>

> [!NOTE]
> <span data-ttu-id="ef9b7-271">Format identyfikatora URI używany w celu skrypt różni się w zależności od używanej usługi.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-271">The URI format used to reference the script differs depending on the service being used.</span></span> <span data-ttu-id="ef9b7-272">Dla konta magazynu skojarzone z klastrem usługi HDInsight, użyj `wasb://` lub `wasbs://`.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-272">For storage accounts associated with the HDInsight cluster, use `wasb://` or `wasbs://`.</span></span> <span data-ttu-id="ef9b7-273">Identyfikatory URI publicznie do odczytu, użyj `http://` lub `https://`.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-273">For publicly readable URIs, use `http://` or `https://`.</span></span> <span data-ttu-id="ef9b7-274">Data Lake Store, użyj `adl://`.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-274">For Data Lake Store, use `adl://`.</span></span>

### <a name="checking-the-operating-system-version"></a><span data-ttu-id="ef9b7-275">Sprawdzanie wersji systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="ef9b7-275">Checking the operating system version</span></span>

<span data-ttu-id="ef9b7-276">Różne wersje HDInsight korzystają z określonych wersji systemu Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-276">Different versions of HDInsight rely on specific versions of Ubuntu.</span></span> <span data-ttu-id="ef9b7-277">Może to być różnice między systemami Operacyjnymi, które muszą sprawdzaj w skrypcie.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-277">There may be differences between OS versions that you must check for in your script.</span></span> <span data-ttu-id="ef9b7-278">Na przykład konieczne może zainstalować pliku binarnego, który jest powiązany z wersją Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-278">For example, you may need to install a binary that is tied to the version of Ubuntu.</span></span>

<span data-ttu-id="ef9b7-279">Aby sprawdzić wersję systemu operacyjnego, należy użyć `lsb_release`.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-279">To check the OS version, use `lsb_release`.</span></span> <span data-ttu-id="ef9b7-280">Na przykład poniższy skrypt pokazuje, jak odwołać plik tar określonych w zależności od wersji systemu operacyjnego:</span><span class="sxs-lookup"><span data-stu-id="ef9b7-280">For example, the following script demonstrates how to reference a specific tar file depending on the OS version:</span></span>

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

## <span data-ttu-id="ef9b7-281"><a name="deployScript"></a>Lista kontrolna wdrażania akcji skryptu</span><span class="sxs-lookup"><span data-stu-id="ef9b7-281"><a name="deployScript"></a>Checklist for deploying a script action</span></span>

<span data-ttu-id="ef9b7-282">Poniżej przedstawiono kroki, które Wybraliśmy podczas przygotowania do wdrożenia tych skryptów:</span><span class="sxs-lookup"><span data-stu-id="ef9b7-282">Here are the steps we took when preparing to deploy these scripts:</span></span>

* <span data-ttu-id="ef9b7-283">Umieścić pliki, które zawierają niestandardowe skrypty w miejscu, który jest dostępny dla węzłów klastra podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-283">Put the files that contain the custom scripts in a place that is accessible by the cluster nodes during deployment.</span></span> <span data-ttu-id="ef9b7-284">Na przykład domyślny magazyn dla klastra.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-284">For example, the default storage for the cluster.</span></span> <span data-ttu-id="ef9b7-285">Pliki mogą być również przechowywane w publicznie do odczytu usług hostingu.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-285">Files can also be stored in publicly readable hosting services.</span></span>
* <span data-ttu-id="ef9b7-286">Sprawdź, czy skrypt impotent.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-286">Verify that the script is impotent.</span></span> <span data-ttu-id="ef9b7-287">Dzięki temu skryptu do wykonania wiele razy w tym samym węźle.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-287">Doing so allows the script to be executed multiple times on the same node.</span></span>
* <span data-ttu-id="ef9b7-288">Użyj /tmp katalogu plików tymczasowych, aby zachować pobrane pliki używane przez skrypty i następnie wyczyść je po wykonaniu skryptów.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-288">Use a temporary file directory /tmp to keep the downloaded files used by the scripts and then clean them up after scripts have executed.</span></span>
* <span data-ttu-id="ef9b7-289">Ustawienia na poziomie systemu operacyjnego lub plików konfiguracyjnych usługi Hadoop są zmieniane, można ponownie uruchomić usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-289">If OS-level settings or Hadoop service configuration files are changed, you may want to restart HDInsight services.</span></span>

## <span data-ttu-id="ef9b7-290"><a name="runScriptAction"></a>Jak uruchomić akcję skryptu</span><span class="sxs-lookup"><span data-stu-id="ef9b7-290"><a name="runScriptAction"></a>How to run a script action</span></span>

<span data-ttu-id="ef9b7-291">Akcje skryptu umożliwia dostosowywanie klastrów usługi HDInsight przy użyciu następujących metod:</span><span class="sxs-lookup"><span data-stu-id="ef9b7-291">You can use script actions to customize HDInsight clusters using the following methods:</span></span>

* <span data-ttu-id="ef9b7-292">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ef9b7-292">Azure portal</span></span>
* <span data-ttu-id="ef9b7-293">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ef9b7-293">Azure PowerShell</span></span>
* <span data-ttu-id="ef9b7-294">Szablony usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ef9b7-294">Azure Resource Manager templates</span></span>
* <span data-ttu-id="ef9b7-295">Zestaw .NET SDK usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-295">The HDInsight .NET SDK.</span></span>

<span data-ttu-id="ef9b7-296">Aby uzyskać więcej informacji na temat używania każdej z metod, zobacz [sposób użycia akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="ef9b7-296">For more information on using each method, see [How to use script action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <span data-ttu-id="ef9b7-297"><a name="sampleScripts"></a>Przykłady niestandardowych skryptów</span><span class="sxs-lookup"><span data-stu-id="ef9b7-297"><a name="sampleScripts"></a>Custom script samples</span></span>

<span data-ttu-id="ef9b7-298">Firma Microsoft udostępnia przykładowe skrypty, aby zainstalować składniki w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-298">Microsoft provides sample scripts to install components on an HDInsight cluster.</span></span> <span data-ttu-id="ef9b7-299">Zobacz następujące linki dla więcej przykład akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-299">See the following links for more example script actions.</span></span>

* [<span data-ttu-id="ef9b7-300">Zainstalować i używać Hue w klastrach HDInsight</span><span class="sxs-lookup"><span data-stu-id="ef9b7-300">Install and use Hue on HDInsight clusters</span></span>](hdinsight-hadoop-hue-linux.md)
* [<span data-ttu-id="ef9b7-301">Zainstalować i używać Solr w klastrach HDInsight</span><span class="sxs-lookup"><span data-stu-id="ef9b7-301">Install and use Solr on HDInsight clusters</span></span>](hdinsight-hadoop-solr-install-linux.md)
* [<span data-ttu-id="ef9b7-302">Zainstalować i używać Giraph w klastrach HDInsight</span><span class="sxs-lookup"><span data-stu-id="ef9b7-302">Install and use Giraph on HDInsight clusters</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* [<span data-ttu-id="ef9b7-303">Zainstaluj lub Uaktualnij Mono w klastrach HDInsight</span><span class="sxs-lookup"><span data-stu-id="ef9b7-303">Install or upgrade Mono on HDInsight clusters</span></span>](hdinsight-hadoop-install-mono.md)

## <a name="troubleshooting"></a><span data-ttu-id="ef9b7-304">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="ef9b7-304">Troubleshooting</span></span>

<span data-ttu-id="ef9b7-305">Błędy, które mogą wystąpić podczas za pomocą skryptów, które zostały opracowane są następujące:</span><span class="sxs-lookup"><span data-stu-id="ef9b7-305">The following are errors you may encounter when using scripts you have developed:</span></span>

<span data-ttu-id="ef9b7-306">**Błąd**: `$'\r': command not found`.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-306">**Error**: `$'\r': command not found`.</span></span> <span data-ttu-id="ef9b7-307">Czasami następuje `syntax error: unexpected end of file`.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-307">Sometimes followed by `syntax error: unexpected end of file`.</span></span>

<span data-ttu-id="ef9b7-308">*Przyczyna*: ten błąd występuje, gdy wierszy w skrypcie kończyć CRLF.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-308">*Cause*: This error is caused when the lines in a script end with CRLF.</span></span> <span data-ttu-id="ef9b7-309">Systemy UNIX oczekiwać tylko LF jako zakończenia linii.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-309">Unix systems expect only LF as the line ending.</span></span>

<span data-ttu-id="ef9b7-310">Ten problem najczęściej występuje, gdy skrypt został utworzony w środowisku Windows CRLF jest linii Kończenie dla wielu edytory tekstów w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-310">This problem most often occurs when the script is authored on a Windows environment, as CRLF is a common line ending for many text editors on Windows.</span></span>

<span data-ttu-id="ef9b7-311">*Rozdzielczość*: Jeśli jest to opcja w edytorze tekstu, wybierz Unix format lub LF na koniec wiersza.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-311">*Resolution*: If it is an option in your text editor, select Unix format or LF for the line ending.</span></span> <span data-ttu-id="ef9b7-312">Aby zmienić CRLF LF może także użyć następujących poleceń w systemie Unix:</span><span class="sxs-lookup"><span data-stu-id="ef9b7-312">You may also use the following commands on a Unix system to change the CRLF to an LF:</span></span>

> [!NOTE]
> <span data-ttu-id="ef9b7-313">Poniższe polecenia są w przybliżeniu w tym powinien Zmień zakończenia wierszy CRLF wysuwu wiersza.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-313">The following commands are roughly equivalent in that they should change the CRLF line endings to LF.</span></span> <span data-ttu-id="ef9b7-314">Wybierz jedno z narzędzi dostępnych w systemie w oparciu.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-314">Select one based on the utilities available on your system.</span></span>

| <span data-ttu-id="ef9b7-315">Polecenie</span><span class="sxs-lookup"><span data-stu-id="ef9b7-315">Command</span></span> | <span data-ttu-id="ef9b7-316">Uwagi</span><span class="sxs-lookup"><span data-stu-id="ef9b7-316">Notes</span></span> |
| --- | --- |
| `unix2dos -b INFILE` |<span data-ttu-id="ef9b7-317">Kopii zapasowej oryginalnego pliku z. Rozszerzeniem BAK</span><span class="sxs-lookup"><span data-stu-id="ef9b7-317">The original file is backed up with a .BAK extension</span></span> |
| `tr -d '\r' < INFILE > OUTFILE` |<span data-ttu-id="ef9b7-318">PLIKWYJŚCIOWY zawiera wersję z tylko LF zakończenia</span><span class="sxs-lookup"><span data-stu-id="ef9b7-318">OUTFILE contains a version with only LF endings</span></span> |
| `perl -pi -e 's/\r\n/\n/g' INFILE` | <span data-ttu-id="ef9b7-319">Modyfikuje plik bezpośrednio</span><span class="sxs-lookup"><span data-stu-id="ef9b7-319">Modifies the file directly</span></span> |
| ```sed 's/$'"/`echo \\\r`/" INFILE > OUTFILE``` |<span data-ttu-id="ef9b7-320">PLIKWYJŚCIOWY zawiera wersję z tylko LF zakończenia.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-320">OUTFILE contains a version with only LF endings.</span></span> |

<span data-ttu-id="ef9b7-321">**Błąd**: `line 1: #!/usr/bin/env: No such file or directory`.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-321">**Error**: `line 1: #!/usr/bin/env: No such file or directory`.</span></span>

<span data-ttu-id="ef9b7-322">*Przyczyna*: ten błąd występuje, gdy skrypt został zapisany jako UTF-8 z znacznik kolejności bajtów (BOM).</span><span class="sxs-lookup"><span data-stu-id="ef9b7-322">*Cause*: This error occurs when the script was saved as UTF-8 with a Byte Order Mark (BOM).</span></span>

<span data-ttu-id="ef9b7-323">*Rozdzielczość*: Zapisz plik w formacie ASCII lub jako UTF-8 bez BOM.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-323">*Resolution*: Save the file either as ASCII, or as UTF-8 without a BOM.</span></span> <span data-ttu-id="ef9b7-324">Aby utworzyć plik bez BOM może także użyć następującego polecenia w systemie Linux lub Unix:</span><span class="sxs-lookup"><span data-stu-id="ef9b7-324">You may also use the following command on a Linux or Unix system to create a file without the BOM:</span></span>

    awk 'NR==1{sub(/^\xef\xbb\xbf/,"")}{print}' INFILE > OUTFILE

<span data-ttu-id="ef9b7-325">Zastąp `INFILE` z pliku zawierającego BOM.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-325">Replace `INFILE` with the file containing the BOM.</span></span> <span data-ttu-id="ef9b7-326">`OUTFILE`powinien być nową nazwę pliku, który zawiera skrypt bez BOM.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-326">`OUTFILE` should be a new file name, which contains the script without the BOM.</span></span>

## <span data-ttu-id="ef9b7-327"><a name="seeAlso"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ef9b7-327"><a name="seeAlso"></a>Next steps</span></span>

* <span data-ttu-id="ef9b7-328">Dowiedz się, jak [HDInsight dostosować klastry za pomocą akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md)</span><span class="sxs-lookup"><span data-stu-id="ef9b7-328">Learn how to [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>
* <span data-ttu-id="ef9b7-329">Użyj [odwołania do zestawu SDK .NET usługi HDInsight](https://msdn.microsoft.com/library/mt271028.aspx) Aby dowiedzieć się więcej o tworzeniu aplikacji .NET, które zarządzają HDInsight</span><span class="sxs-lookup"><span data-stu-id="ef9b7-329">Use the [HDInsight .NET SDK reference](https://msdn.microsoft.com/library/mt271028.aspx) to learn more about creating .NET applications that manage HDInsight</span></span>
* <span data-ttu-id="ef9b7-330">Użyj [interfejsu API REST usługi HDInsight](https://msdn.microsoft.com/library/azure/mt622197.aspx) więcej informacji na temat używania REST do wykonywania akcji związanych z zarządzaniem w klastrach usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ef9b7-330">Use the [HDInsight REST API](https://msdn.microsoft.com/library/azure/mt622197.aspx) to learn how to use REST to perform management actions on HDInsight clusters.</span></span>
