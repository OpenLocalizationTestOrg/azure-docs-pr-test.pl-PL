---
title: "Dodawanie bibliotek technologii Hive podczas tworzenia klastra usługi HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak dodać biblioteki gałąź (pliki jar), do klastra usługi HDInsight podczas tworzenia klastra."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 2fd74b8d-c006-45c6-a9e2-72ff5d2d978a
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 3412864384961e8820d6700c1bf22a4cae64ba4b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="add-custom-hive-libraries-when-creating-your-hdinsight-cluster"></a><span data-ttu-id="0fd63-103">Dodawanie niestandardowych bibliotek technologii Hive, podczas tworzenia klastra usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="0fd63-103">Add custom Hive libraries when creating your HDInsight cluster</span></span>

<span data-ttu-id="0fd63-104">Jeśli masz bibliotek, które są często używane z Hive w usłudze HDInsight ten dokument zawiera informacje o wstępnie załadować biblioteki podczas tworzenia klastra przy użyciu akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="0fd63-104">If you have libraries that you use frequently with Hive on HDInsight, this document contains information on using a Script Action to pre-load the libraries during cluster creation.</span></span> <span data-ttu-id="0fd63-105">Biblioteki dodane przy użyciu kroków w tym dokumencie są globalnie dostępną w gałęzi — nie trzeba używać [dodać JAR](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Cli) załadować je.</span><span class="sxs-lookup"><span data-stu-id="0fd63-105">Libraries added using the steps in this document are globally available in Hive - there is no need to use [ADD JAR](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Cli) to load them.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="0fd63-106">Jak to działa</span><span class="sxs-lookup"><span data-stu-id="0fd63-106">How it works</span></span>

<span data-ttu-id="0fd63-107">Podczas tworzenia klastra, można opcjonalnie określić akcję skryptu, który uruchamia skrypt w węzłach klastra podczas ich tworzenia.</span><span class="sxs-lookup"><span data-stu-id="0fd63-107">When creating a cluster, you can optionally specify a Script Action that runs a script on the cluster nodes while they are being created.</span></span> <span data-ttu-id="0fd63-108">Skrypt w tym dokumencie akceptuje pojedynczy parametr to lokalizacja WASB zawierający bibliotek (przechowywane jako pliki jar), aby być wstępnie ładowane.</span><span class="sxs-lookup"><span data-stu-id="0fd63-108">The script in this document accepts a single parameter, which is a WASB location that contains the libraries (stored as jar files) to be pre-loaded.</span></span>

<span data-ttu-id="0fd63-109">Podczas tworzenia klastra, skrypt wylicza pliki, kopiuje je do `/usr/lib/customhivelibs/` katalogu w węzłach head i proces roboczy, następnie dodanie ich do `hive.aux.jars.path` właściwości w `core-site.xml` pliku.</span><span class="sxs-lookup"><span data-stu-id="0fd63-109">During cluster creation, the script enumerates the files, copies them to the `/usr/lib/customhivelibs/` directory on head and worker nodes, then adds them to the `hive.aux.jars.path` property in the `core-site.xml` file.</span></span> <span data-ttu-id="0fd63-110">W klastrach opartych na systemie Linux, aktualizuje również `hive-env.sh` pliku z lokalizacji plików.</span><span class="sxs-lookup"><span data-stu-id="0fd63-110">On Linux-based clusters, it also updates the `hive-env.sh` file with the location of the files.</span></span>

> [!NOTE]
> <span data-ttu-id="0fd63-111">Za pomocą akcji skryptu w tym artykule udostępnia biblioteki w następujących scenariuszach:</span><span class="sxs-lookup"><span data-stu-id="0fd63-111">Using the script actions in this article makes the libraries available in the following scenarios:</span></span>
>
> * <span data-ttu-id="0fd63-112">**HDInsight opartych na systemie Linux** — w przypadku korzystania z klienta Hive, **WebHCat**, i **serwera HiveServer2**.</span><span class="sxs-lookup"><span data-stu-id="0fd63-112">**Linux-based HDInsight** - when using the a Hive client, **WebHCat**, and **HiveServer2**.</span></span>
> * <span data-ttu-id="0fd63-113">**HDInsight opartych na systemie Windows** — za pomocą klienta programu Hive i **WebHCat**.</span><span class="sxs-lookup"><span data-stu-id="0fd63-113">**Windows-based HDInsight** - when using the Hive client and **WebHCat**.</span></span>

## <a name="the-script"></a><span data-ttu-id="0fd63-114">Skrypt</span><span class="sxs-lookup"><span data-stu-id="0fd63-114">The script</span></span>

<span data-ttu-id="0fd63-115">**Lokalizacja skryptu**</span><span class="sxs-lookup"><span data-stu-id="0fd63-115">**Script location**</span></span>

<span data-ttu-id="0fd63-116">Aby uzyskać **opartych na systemie Linux klastrów**: [https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh)</span><span class="sxs-lookup"><span data-stu-id="0fd63-116">For **Linux-based clusters**: [https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh)</span></span>

<span data-ttu-id="0fd63-117">Aby uzyskać **klastry z systemem Windows**: [https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1](https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1)</span><span class="sxs-lookup"><span data-stu-id="0fd63-117">For **Windows-based clusters**: [https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1](https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0fd63-118">Linux jest jedynym systemem operacyjnym używanym w połączeniu z usługą HDInsight w wersji 3.4 lub nowszą.</span><span class="sxs-lookup"><span data-stu-id="0fd63-118">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="0fd63-119">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="0fd63-119">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="0fd63-120">**Wymagania**</span><span class="sxs-lookup"><span data-stu-id="0fd63-120">**Requirements**</span></span>

* <span data-ttu-id="0fd63-121">Skrypty należy zastosować do obu **węzły główne** i **węzłów procesu roboczego**.</span><span class="sxs-lookup"><span data-stu-id="0fd63-121">The scripts must be applied to both the **Head nodes** and **Worker nodes**.</span></span>

* <span data-ttu-id="0fd63-122">Słoików chcesz zainstalować musi być przechowywany w magazynie obiektów Blob Azure w **jeden kontener**.</span><span class="sxs-lookup"><span data-stu-id="0fd63-122">The jars you wish to install must be stored in Azure Blob Storage in a **single container**.</span></span>

* <span data-ttu-id="0fd63-123">Konto magazynu zawierające biblioteki pliki jar **musi** można połączyć się z klastrem usługi HDInsight podczas tworzenia.</span><span class="sxs-lookup"><span data-stu-id="0fd63-123">The storage account containing the library of jar files **must** be linked to the HDInsight cluster during creation.</span></span> <span data-ttu-id="0fd63-124">Musi być domyślne konto magazynu, lub dodać konta za pośrednictwem __konfiguracji opcjonalnej__.</span><span class="sxs-lookup"><span data-stu-id="0fd63-124">It must either be the default storage account, or an account added through __optional configuration__.</span></span>

* <span data-ttu-id="0fd63-125">Jako parametr akcji skryptu można określić ścieżkę WASB do kontenera.</span><span class="sxs-lookup"><span data-stu-id="0fd63-125">The WASB path to the container must be specified as a parameter to the Script Action.</span></span> <span data-ttu-id="0fd63-126">Na przykład, jeśli słoików są przechowywane w kontenerze o nazwie **libs** na konto magazynu o nazwie **mystorage**, będzie parametr  **wasb://libs@mystorage.blob.core.windows.net/** .</span><span class="sxs-lookup"><span data-stu-id="0fd63-126">For example, if the jars are stored in a container named **libs** on a storage account named **mystorage**, the parameter would be **wasb://libs@mystorage.blob.core.windows.net/**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="0fd63-127">Tym dokumencie przyjęto założenie, masz już tworzenia konta magazynu, kontenera obiektów blob i przekazać pliki do niego.</span><span class="sxs-lookup"><span data-stu-id="0fd63-127">This document assumes that you have already create a storage account, blob container, and uploaded the files to it.</span></span>
  >
  > <span data-ttu-id="0fd63-128">Jeśli nie utworzono konto magazynu, możesz to zrobić za pomocą programu tak [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0fd63-128">If you have not created a storage account, you can do so through the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="0fd63-129">Następnie można użyć narzędzia takie jak [Eksploratora usługi Storage Azure](http://storageexplorer.com/) utworzyć kontener w ramach konta i przekazać pliki do niego.</span><span class="sxs-lookup"><span data-stu-id="0fd63-129">You can then use a utility such as [Azure Storage Explorer](http://storageexplorer.com/) to create a container in the account and upload files to it.</span></span>

## <a name="create-a-cluster-using-the-script"></a><span data-ttu-id="0fd63-130">Tworzenie klastra przy użyciu skryptu</span><span class="sxs-lookup"><span data-stu-id="0fd63-130">Create a cluster using the script</span></span>

> [!NOTE]
> <span data-ttu-id="0fd63-131">Poniższe kroki tworzenia klastra usługi HDInsight opartej na systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="0fd63-131">The following steps create a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="0fd63-132">Do utworzenia klastra z systemem Windows, zaznacz **Windows** jako klaster systemu operacyjnego podczas tworzenia klastra, a następnie użyj skryptu systemu Windows (PowerShell) zamiast skryptu bash.</span><span class="sxs-lookup"><span data-stu-id="0fd63-132">To create a Windows-based cluster, select **Windows** as the cluster OS when creating the cluster, and use the Windows (PowerShell) script instead of the bash script.</span></span>
>
> <span data-ttu-id="0fd63-133">Aby utworzyć klaster przy użyciu tego skryptu, można użyć programu Azure PowerShell lub zestawu .NET SDK usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0fd63-133">You can also use Azure PowerShell or the HDInsight .NET SDK to create a cluster using this script.</span></span> <span data-ttu-id="0fd63-134">Aby uzyskać więcej informacji o używaniu tych metod, zobacz [Dostosowywanie klastrów usługi HDInsight z akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="0fd63-134">For more information on using these methods, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

1. <span data-ttu-id="0fd63-135">Uruchom inicjowania obsługi klastra, wykonując kroki opisane w [Obsługa administracyjna klastrów HDInsight w systemie Linux](hdinsight-hadoop-provision-linux-clusters.md), kroków inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="0fd63-135">Start provisioning a cluster by using the steps in [Provision HDInsight clusters on Linux](hdinsight-hadoop-provision-linux-clusters.md), but do not complete provisioning.</span></span>

2. <span data-ttu-id="0fd63-136">Na **konfiguracji opcjonalnej** bloku, wybierz opcję **akcji skryptu**i podaj następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="0fd63-136">On the **Optional Configuration** blade, select **Script Actions**, and provide the following information:</span></span>

   * <span data-ttu-id="0fd63-137">**Nazwa**: Wprowadź przyjazną nazwę dla akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="0fd63-137">**NAME**: Enter a friendly name for the script action.</span></span>

   * <span data-ttu-id="0fd63-138">**Identyfikator URI skryptu**: https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh</span><span class="sxs-lookup"><span data-stu-id="0fd63-138">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh</span></span>

   * <span data-ttu-id="0fd63-139">**HEAD**: Zaznaczenie tego pola wyboru.</span><span class="sxs-lookup"><span data-stu-id="0fd63-139">**HEAD**: Check this option.</span></span>

   * <span data-ttu-id="0fd63-140">**Proces ROBOCZY**: Zaznaczenie tego pola wyboru.</span><span class="sxs-lookup"><span data-stu-id="0fd63-140">**WORKER**: Check this option.</span></span>

   * <span data-ttu-id="0fd63-141">**DOZORCY**: to pole pozostanie puste.</span><span class="sxs-lookup"><span data-stu-id="0fd63-141">**ZOOKEEPER**: Leave this blank.</span></span>

   * <span data-ttu-id="0fd63-142">**Parametry**: Wprowadź adres WASB do wybranego konta magazynu i kontenera zawiera słoików.</span><span class="sxs-lookup"><span data-stu-id="0fd63-142">**PARAMETERS**: Enter the WASB address to the container and storage account that contains the jars.</span></span> <span data-ttu-id="0fd63-143">Na przykład  **wasb://libs@mystorage.blob.core.windows.net/** .</span><span class="sxs-lookup"><span data-stu-id="0fd63-143">For example, **wasb://libs@mystorage.blob.core.windows.net/**.</span></span>

3. <span data-ttu-id="0fd63-144">W dolnej części **akcji skryptu**, użyj **wybierz** przycisk, aby zapisać konfigurację.</span><span class="sxs-lookup"><span data-stu-id="0fd63-144">At the bottom of the **Script Actions**, use the **Select** button to save the configuration.</span></span>

4. <span data-ttu-id="0fd63-145">Na **konfiguracji opcjonalnej** bloku, wybierz opcję **połączonych kontach magazynu** i wybierz **Dodaj klucz magazynu** łącza.</span><span class="sxs-lookup"><span data-stu-id="0fd63-145">On the **Optional Configuration** blade, select **Linked Storage Accounts** and select the **Add a storage key** link.</span></span> <span data-ttu-id="0fd63-146">Wybierz konto magazynu, który zawiera słoików, a następnie użyj **wybierz** przycisków, aby zapisać ustawienia i wrócić **konfiguracji opcjonalnej** bloku.</span><span class="sxs-lookup"><span data-stu-id="0fd63-146">Select the storage account that contains the jars, and then use the **select** buttons to save settings and return the **Optional Configuration** blade.</span></span>

5. <span data-ttu-id="0fd63-147">Użyj **wybierz** przycisk w dolnej części **konfiguracji opcjonalnej** bloku, aby zapisać informacje o konfiguracji opcjonalnej.</span><span class="sxs-lookup"><span data-stu-id="0fd63-147">Use the **Select** button at the bottom of the **Optional Configuration** blade to save the optional configuration information.</span></span>

6. <span data-ttu-id="0fd63-148">Kontynuuj, inicjowania obsługi klastra, zgodnie z opisem w [Obsługa administracyjna klastrów HDInsight w systemie Linux](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="0fd63-148">Continue provisioning the cluster as described in [Provision HDInsight clusters on Linux](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

<span data-ttu-id="0fd63-149">Po zakończeniu tworzenia klastra, będą mogli używać słoików dodane za pomocą tego skryptu z Hive, bez konieczności używania `ADD JAR` instrukcji.</span><span class="sxs-lookup"><span data-stu-id="0fd63-149">Once cluster creation finishes, you are able to use the jars added through this script from Hive without having to use the `ADD JAR` statement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0fd63-150">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0fd63-150">Next steps</span></span>

<span data-ttu-id="0fd63-151">Aby uzyskać więcej informacji na temat pracy z Hive, zobacz [używanie Hive z usługą HDInsight](hdinsight-use-hive.md)</span><span class="sxs-lookup"><span data-stu-id="0fd63-151">For more information on working with Hive, see [Use Hive with HDInsight](hdinsight-use-hive.md)</span></span>
