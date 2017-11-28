---
title: "aaaInstall lub zaktualizuj Mono w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse określonej wersji Mono z klastrem usługi HDInsight. Mono jest toorun używanych aplikacji .NET w klastrach HDInsight opartych na systemie Linux."
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.custom: hdinsightactive
ms.openlocfilehash: 1e8a8aaeff231c93a9e232379448517b326da965
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-or-update-mono-on-hdinsight"></a><span data-ttu-id="b5cde-104">Zainstaluj lub zaktualizuj Mono w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="b5cde-104">Install or update Mono on HDInsight</span></span>

<span data-ttu-id="b5cde-105">Dowiedz się, jak tooinstall określonej wersji programu [Mono](https://www.mono-project.com) HDInsight 3.4 lub nowszego.</span><span class="sxs-lookup"><span data-stu-id="b5cde-105">Learn how tooinstall a specific version of [Mono](https://www.mono-project.com) on HDInsight 3.4 or higher.</span></span>

<span data-ttu-id="b5cde-106">Mono jest zainstalowany w wersji 3.4 HDInsight lub nowszym i jest używany toorun aplikacji .NET.</span><span class="sxs-lookup"><span data-stu-id="b5cde-106">Mono is installed on HDInsight 3.4 and higher, and is used toorun .NET applications.</span></span> <span data-ttu-id="b5cde-107">Uzyskać informacji o wersji hello Mono dołączone do każdej wersji usługi HDInsight, zobacz [przechowywanie wersji składnika usługi HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="b5cde-107">For information on hello version of Mono included with each HDInsight version, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="b5cde-108">tooinstall inną wersję w klastrze, użyj akcji skryptu hello w tym dokumencie.</span><span class="sxs-lookup"><span data-stu-id="b5cde-108">tooinstall a different version on your cluster, use hello script action in this document.</span></span> 

## <a name="how-it-works"></a><span data-ttu-id="b5cde-109">Jak to działa</span><span class="sxs-lookup"><span data-stu-id="b5cde-109">How it works</span></span>

<span data-ttu-id="b5cde-110">Ten skrypt akceptuje hello następującego parametru:</span><span class="sxs-lookup"><span data-stu-id="b5cde-110">This script accepts hello following parameter:</span></span>

* <span data-ttu-id="b5cde-111">__Numer wersji mono__: wersja hello Mono tooinstall.</span><span class="sxs-lookup"><span data-stu-id="b5cde-111">__Mono version number__: hello version of Mono tooinstall.</span></span> <span data-ttu-id="b5cde-112">Wersja Hello musi być dostępny z [https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/](https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/).</span><span class="sxs-lookup"><span data-stu-id="b5cde-112">hello version must be available from [https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/](https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/).</span></span>

<span data-ttu-id="b5cde-113">skrypt Hello instaluje powitania po Mono pakiety:</span><span class="sxs-lookup"><span data-stu-id="b5cde-113">hello script installs hello following Mono packages:</span></span>

* <span data-ttu-id="b5cde-114">__Zakończenie mono__</span><span class="sxs-lookup"><span data-stu-id="b5cde-114">__mono-complete__</span></span>

* <span data-ttu-id="b5cde-115">__Urząd certyfikacji — certyfikaty — mono__</span><span class="sxs-lookup"><span data-stu-id="b5cde-115">__ca-certificates-mono__</span></span>

## <a name="hello-script"></a><span data-ttu-id="b5cde-116">Witaj skryptu</span><span class="sxs-lookup"><span data-stu-id="b5cde-116">hello script</span></span>

<span data-ttu-id="b5cde-117">__Lokalizacja skryptu__: [https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash](https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash)</span><span class="sxs-lookup"><span data-stu-id="b5cde-117">__Script location__: [https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash](https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash)</span></span>

<span data-ttu-id="b5cde-118">__Wymagania dotyczące__:</span><span class="sxs-lookup"><span data-stu-id="b5cde-118">__Requirements__:</span></span>

* <span data-ttu-id="b5cde-119">Witaj skryptu muszą być stosowane na powitania __węzły główne__ i __węzłów procesu roboczego__.</span><span class="sxs-lookup"><span data-stu-id="b5cde-119">hello script must be applied on hello __head nodes__ and __worker nodes__.</span></span>

## <a name="toouse-hello-script"></a><span data-ttu-id="b5cde-120">toouse hello skryptu</span><span class="sxs-lookup"><span data-stu-id="b5cde-120">toouse hello script</span></span>

<span data-ttu-id="b5cde-121">Aby uzyskać informacje dotyczące toouse ten skrypt z usługą HDInsight, zobacz temat hello [klastrów usługi HDInsight opartej na dostosowanie systemu Linux przy użyciu akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="b5cde-121">For information on how toouse this script with HDInsight, see hello [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) document.</span></span> <span data-ttu-id="b5cde-122">Można użyć skryptu hello za pomocą hello portalu Azure, programu Azure PowerShell lub hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b5cde-122">You can use hello script through hello Azure portal, Azure PowerShell, or hello Azure CLI.</span></span>

<span data-ttu-id="b5cde-123">Gdy następujące hello dokument akcji skryptu, użyj hello następującego identyfikatora URI:</span><span class="sxs-lookup"><span data-stu-id="b5cde-123">While following hello script action document, use hello following URI:</span></span>

    https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash

> [!NOTE]
> <span data-ttu-id="b5cde-124">Podczas konfigurowania usługi HDInsight za pomocą tego skryptu, należy oznaczyć skrypt hello jako __Persisted__.</span><span class="sxs-lookup"><span data-stu-id="b5cde-124">When configuring HDInsight with this script, mark hello script as __Persisted__.</span></span> <span data-ttu-id="b5cde-125">To ustawienie umożliwia HDInsight tooapply węzłów tooworker skryptu hello dodanych do skalowania operacji.</span><span class="sxs-lookup"><span data-stu-id="b5cde-125">This setting allows HDInsight tooapply hello script tooworker nodes added through scaling operations.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b5cde-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b5cde-126">Next steps</span></span>

<span data-ttu-id="b5cde-127">Wiesz już, jak tooupgrade lub zainstaluj określonej wersji Mono w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b5cde-127">You have learned how tooupgrade or install a specific version of Mono on HDInsight.</span></span> <span data-ttu-id="b5cde-128">Aby uzyskać więcej informacji na temat używania aplikacji .NET z Mono w usłudze HDInsight Zobacz hello w następujących dokumentach:</span><span class="sxs-lookup"><span data-stu-id="b5cde-128">For more information on using .NET applications with Mono on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="b5cde-129">Użyj .NET do przesyłania strumieniowego MapReduce w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="b5cde-129">Use .NET for streaming MapReduce on HDInsight</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)
* [<span data-ttu-id="b5cde-130">.NET za pomocą technologii Hive i Pig w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="b5cde-130">Use .NET with Hive and Pig on HDInsight</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)
* [<span data-ttu-id="b5cde-131">Tworzenie rozwiązań C# z systemu Storm w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="b5cde-131">Develop C# solutions with Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="b5cde-132">Migracja rozwiązań platformy .NET usługi HDInsight opartej na tooLinux</span><span class="sxs-lookup"><span data-stu-id="b5cde-132">Migrate .NET solutions tooLinux-based HDInsight</span></span>](hdinsight-hadoop-migrate-dotnet-to-linux.md)

<span data-ttu-id="b5cde-133">Aby uzyskać więcej informacji dotyczących za pomocą akcji skryptu, zobacz [klastrów usługi HDInsight opartej na dostosowanie systemu Linux przy użyciu akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md)</span><span class="sxs-lookup"><span data-stu-id="b5cde-133">For more information on using script actions, see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>