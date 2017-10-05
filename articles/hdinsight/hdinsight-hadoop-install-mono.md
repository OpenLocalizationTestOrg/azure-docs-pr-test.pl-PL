---
title: "Zainstaluj lub zaktualizuj Mono w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać określonej wersji Mono z klastrem usługi HDInsight. Mono służy do uruchamiania aplikacji .NET w klastrach HDInsight opartych na systemie Linux."
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
ms.openlocfilehash: fd284542e1de65f323f1e3a092689f847e025be6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="install-or-update-mono-on-hdinsight"></a><span data-ttu-id="4f847-104">Zainstaluj lub zaktualizuj Mono w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="4f847-104">Install or update Mono on HDInsight</span></span>

<span data-ttu-id="4f847-105">Dowiedz się, jak zainstalować określoną wersję [Mono](https://www.mono-project.com) HDInsight 3.4 lub nowszego.</span><span class="sxs-lookup"><span data-stu-id="4f847-105">Learn how to install a specific version of [Mono](https://www.mono-project.com) on HDInsight 3.4 or higher.</span></span>

<span data-ttu-id="4f847-106">Mono jest zainstalowany w wersji 3.4 HDInsight lub nowszy i służy do uruchamiania aplikacji .NET.</span><span class="sxs-lookup"><span data-stu-id="4f847-106">Mono is installed on HDInsight 3.4 and higher, and is used to run .NET applications.</span></span> <span data-ttu-id="4f847-107">Uzyskać informacji o wersji Mono dołączone do każdej wersji usługi HDInsight, zobacz [przechowywanie wersji składnika usługi HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="4f847-107">For information on the version of Mono included with each HDInsight version, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="4f847-108">Aby zainstalować w innej wersji w klastrze, należy użyć akcji skryptu w tym dokumencie.</span><span class="sxs-lookup"><span data-stu-id="4f847-108">To install a different version on your cluster, use the script action in this document.</span></span> 

## <a name="how-it-works"></a><span data-ttu-id="4f847-109">Jak to działa</span><span class="sxs-lookup"><span data-stu-id="4f847-109">How it works</span></span>

<span data-ttu-id="4f847-110">Ten skrypt akceptuje następującego parametru:</span><span class="sxs-lookup"><span data-stu-id="4f847-110">This script accepts the following parameter:</span></span>

* <span data-ttu-id="4f847-111">__Numer wersji mono__: wersja Mono do zainstalowania.</span><span class="sxs-lookup"><span data-stu-id="4f847-111">__Mono version number__: The version of Mono to install.</span></span> <span data-ttu-id="4f847-112">Wersja musi być dostępny z [https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/](https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/).</span><span class="sxs-lookup"><span data-stu-id="4f847-112">The version must be available from [https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/](https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/).</span></span>

<span data-ttu-id="4f847-113">Skrypt instaluje Mono następujących pakietów:</span><span class="sxs-lookup"><span data-stu-id="4f847-113">The script installs the following Mono packages:</span></span>

* <span data-ttu-id="4f847-114">__Zakończenie mono__</span><span class="sxs-lookup"><span data-stu-id="4f847-114">__mono-complete__</span></span>

* <span data-ttu-id="4f847-115">__Urząd certyfikacji — certyfikaty — mono__</span><span class="sxs-lookup"><span data-stu-id="4f847-115">__ca-certificates-mono__</span></span>

## <a name="the-script"></a><span data-ttu-id="4f847-116">Skrypt</span><span class="sxs-lookup"><span data-stu-id="4f847-116">The script</span></span>

<span data-ttu-id="4f847-117">__Lokalizacja skryptu__: [https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash](https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash)</span><span class="sxs-lookup"><span data-stu-id="4f847-117">__Script location__: [https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash](https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash)</span></span>

<span data-ttu-id="4f847-118">__Wymagania dotyczące__:</span><span class="sxs-lookup"><span data-stu-id="4f847-118">__Requirements__:</span></span>

* <span data-ttu-id="4f847-119">Skrypt musi zostać zastosowana na __węzły główne__ i __węzłów procesu roboczego__.</span><span class="sxs-lookup"><span data-stu-id="4f847-119">The script must be applied on the __head nodes__ and __worker nodes__.</span></span>

## <a name="to-use-the-script"></a><span data-ttu-id="4f847-120">Aby użyć skryptu</span><span class="sxs-lookup"><span data-stu-id="4f847-120">To use the script</span></span>

<span data-ttu-id="4f847-121">Aby uzyskać informacje dotyczące sposobu używania tego skryptu z usługą HDInsight, zobacz [klastrów usługi HDInsight opartej na dostosowanie systemu Linux przy użyciu akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="4f847-121">For information on how to use this script with HDInsight, see the [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) document.</span></span> <span data-ttu-id="4f847-122">Możesz użyć skryptu, za pośrednictwem portalu Azure, programu Azure PowerShell lub wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4f847-122">You can use the script through the Azure portal, Azure PowerShell, or the Azure CLI.</span></span>

<span data-ttu-id="4f847-123">Podczas dokument akcji skryptu, użyj następującego identyfikatora URI:</span><span class="sxs-lookup"><span data-stu-id="4f847-123">While following the script action document, use the following URI:</span></span>

    https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash

> [!NOTE]
> <span data-ttu-id="4f847-124">Podczas konfigurowania usługi HDInsight za pomocą tego skryptu należy oznaczyć skrypt jako __Persisted__.</span><span class="sxs-lookup"><span data-stu-id="4f847-124">When configuring HDInsight with this script, mark the script as __Persisted__.</span></span> <span data-ttu-id="4f847-125">To ustawienie umożliwia HDInsight zastosować skrypt do węzłów procesu roboczego dodanych do skalowania operacji.</span><span class="sxs-lookup"><span data-stu-id="4f847-125">This setting allows HDInsight to apply the script to worker nodes added through scaling operations.</span></span>


## <a name="next-steps"></a><span data-ttu-id="4f847-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4f847-126">Next steps</span></span>

<span data-ttu-id="4f847-127">Zapoznaniu uaktualnić lub zainstalować określoną wersję Mono w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4f847-127">You have learned how to upgrade or install a specific version of Mono on HDInsight.</span></span> <span data-ttu-id="4f847-128">Aby uzyskać więcej informacji na temat używania aplikacji .NET z Mono w usłudze HDInsight można znaleźć w następujących dokumentach:</span><span class="sxs-lookup"><span data-stu-id="4f847-128">For more information on using .NET applications with Mono on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="4f847-129">Użyj .NET do przesyłania strumieniowego MapReduce w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="4f847-129">Use .NET for streaming MapReduce on HDInsight</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)
* [<span data-ttu-id="4f847-130">.NET za pomocą technologii Hive i Pig w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="4f847-130">Use .NET with Hive and Pig on HDInsight</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)
* [<span data-ttu-id="4f847-131">Tworzenie rozwiązań C# z systemu Storm w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="4f847-131">Develop C# solutions with Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="4f847-132">Migracja rozwiązań platformy .NET do usługi HDInsight opartej na systemie Linux</span><span class="sxs-lookup"><span data-stu-id="4f847-132">Migrate .NET solutions to Linux-based HDInsight</span></span>](hdinsight-hadoop-migrate-dotnet-to-linux.md)

<span data-ttu-id="4f847-133">Aby uzyskać więcej informacji dotyczących za pomocą akcji skryptu, zobacz [klastrów usługi HDInsight opartej na dostosowanie systemu Linux przy użyciu akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md)</span><span class="sxs-lookup"><span data-stu-id="4f847-133">For more information on using script actions, see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>