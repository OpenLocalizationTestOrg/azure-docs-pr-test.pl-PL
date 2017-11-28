---
title: "Tworzenie - Azure klastra aaaAdd bibliotek technologii Hive w usłudze HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak bibliotek technologii Hive tooadd (pliki jar) tooan HDInsight klastra podczas tworzenia klastra."
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
ms.openlocfilehash: 2e028a07c3248205def0789af2c262a0774a8f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-custom-hive-libraries-when-creating-your-hdinsight-cluster"></a><span data-ttu-id="ce1d4-103">Dodawanie niestandardowych bibliotek technologii Hive, podczas tworzenia klastra usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="ce1d4-103">Add custom Hive libraries when creating your HDInsight cluster</span></span>

<span data-ttu-id="ce1d4-104">Jeśli masz bibliotek, które są często używane z Hive w usłudze HDInsight ten dokument zawiera informacji na temat używania biblioteki hello obciążenia toopre akcji skryptu podczas tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="ce1d4-104">If you have libraries that you use frequently with Hive on HDInsight, this document contains information on using a Script Action toopre-load hello libraries during cluster creation.</span></span> <span data-ttu-id="ce1d4-105">Biblioteki dodane przy użyciu hello kroków w tym dokumencie są globalnie dostępną w gałęzi — nie toouse bez konieczności [dodać JAR](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Cli) tooload je.</span><span class="sxs-lookup"><span data-stu-id="ce1d4-105">Libraries added using hello steps in this document are globally available in Hive - there is no need toouse [ADD JAR](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Cli) tooload them.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="ce1d4-106">Jak to działa</span><span class="sxs-lookup"><span data-stu-id="ce1d4-106">How it works</span></span>

<span data-ttu-id="ce1d4-107">Podczas tworzenia klastra, można opcjonalnie określić akcję skryptu, który uruchamia skrypt w węzłach klastra hello podczas ich tworzenia.</span><span class="sxs-lookup"><span data-stu-id="ce1d4-107">When creating a cluster, you can optionally specify a Script Action that runs a script on hello cluster nodes while they are being created.</span></span> <span data-ttu-id="ce1d4-108">skrypt Hello w tym dokumencie akceptuje pojedynczy parametr to lokalizacja WASB zawierający toobe bibliotek (przechowywane jako pliki jar) hello wstępnie załadowane.</span><span class="sxs-lookup"><span data-stu-id="ce1d4-108">hello script in this document accepts a single parameter, which is a WASB location that contains hello libraries (stored as jar files) toobe pre-loaded.</span></span>

<span data-ttu-id="ce1d4-109">Podczas tworzenia klastra skryptu hello wylicza hello pliki, kopiuje je toohello `/usr/lib/customhivelibs/` katalogu w węzłach head i proces roboczy, następnie dodanie ich toohello `hive.aux.jars.path` właściwości w hello `core-site.xml` pliku.</span><span class="sxs-lookup"><span data-stu-id="ce1d4-109">During cluster creation, hello script enumerates hello files, copies them toohello `/usr/lib/customhivelibs/` directory on head and worker nodes, then adds them toohello `hive.aux.jars.path` property in hello `core-site.xml` file.</span></span> <span data-ttu-id="ce1d4-110">W klastrach opartych na systemie Linux, aktualizuje również hello `hive-env.sh` pliku z lokalizacji hello hello plików.</span><span class="sxs-lookup"><span data-stu-id="ce1d4-110">On Linux-based clusters, it also updates hello `hive-env.sh` file with hello location of hello files.</span></span>

> [!NOTE]
> <span data-ttu-id="ce1d4-111">Za pomocą akcji skryptu hello w tym artykule udostępnia biblioteki hello w hello następujące scenariusze:</span><span class="sxs-lookup"><span data-stu-id="ce1d4-111">Using hello script actions in this article makes hello libraries available in hello following scenarios:</span></span>
>
> * <span data-ttu-id="ce1d4-112">**HDInsight opartych na systemie Linux** — przy użyciu hello klientowi Hive **WebHCat**, i **serwera HiveServer2**.</span><span class="sxs-lookup"><span data-stu-id="ce1d4-112">**Linux-based HDInsight** - when using hello a Hive client, **WebHCat**, and **HiveServer2**.</span></span>
> * <span data-ttu-id="ce1d4-113">**HDInsight opartych na systemie Windows** — za pomocą powitania klienta Hive i **WebHCat**.</span><span class="sxs-lookup"><span data-stu-id="ce1d4-113">**Windows-based HDInsight** - when using hello Hive client and **WebHCat**.</span></span>

## <a name="hello-script"></a><span data-ttu-id="ce1d4-114">Witaj skryptu</span><span class="sxs-lookup"><span data-stu-id="ce1d4-114">hello script</span></span>

<span data-ttu-id="ce1d4-115">**Lokalizacja skryptu**</span><span class="sxs-lookup"><span data-stu-id="ce1d4-115">**Script location**</span></span>

<span data-ttu-id="ce1d4-116">Aby uzyskać **opartych na systemie Linux klastrów**: [https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh)</span><span class="sxs-lookup"><span data-stu-id="ce1d4-116">For **Linux-based clusters**: [https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh)</span></span>

<span data-ttu-id="ce1d4-117">Aby uzyskać **klastry z systemem Windows**: [https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1](https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1)</span><span class="sxs-lookup"><span data-stu-id="ce1d4-117">For **Windows-based clusters**: [https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1](https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ce1d4-118">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="ce1d4-118">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ce1d4-119">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="ce1d4-119">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="ce1d4-120">**Wymagania**</span><span class="sxs-lookup"><span data-stu-id="ce1d4-120">**Requirements**</span></span>

* <span data-ttu-id="ce1d4-121">skrypty Hello musi być zastosowany tooboth hello **węzły główne** i **węzłów procesu roboczego**.</span><span class="sxs-lookup"><span data-stu-id="ce1d4-121">hello scripts must be applied tooboth hello **Head nodes** and **Worker nodes**.</span></span>

* <span data-ttu-id="ce1d4-122">Witaj słoików mają tooinstall musi być przechowywany w magazynie obiektów Blob Azure w **jeden kontener**.</span><span class="sxs-lookup"><span data-stu-id="ce1d4-122">hello jars you wish tooinstall must be stored in Azure Blob Storage in a **single container**.</span></span>

* <span data-ttu-id="ce1d4-123">Konto magazynu Hello zawierające biblioteki hello plików jar **musi** się podczas tworzenia klastra usługi HDInsight toohello połączone.</span><span class="sxs-lookup"><span data-stu-id="ce1d4-123">hello storage account containing hello library of jar files **must** be linked toohello HDInsight cluster during creation.</span></span> <span data-ttu-id="ce1d4-124">Musi być hello domyślne konto magazynu lub dodać konta za pośrednictwem __konfiguracji opcjonalnej__.</span><span class="sxs-lookup"><span data-stu-id="ce1d4-124">It must either be hello default storage account, or an account added through __optional configuration__.</span></span>

* <span data-ttu-id="ce1d4-125">Witaj WASB ścieżka toohello kontenera muszą być określone jako parametr toohello akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="ce1d4-125">hello WASB path toohello container must be specified as a parameter toohello Script Action.</span></span> <span data-ttu-id="ce1d4-126">Na przykład, jeśli hello słoików są przechowywane w kontenerze o nazwie **libs** na konto magazynu o nazwie **mystorage**, będzie parametru hello  **wasb://libs@mystorage.blob.core.windows.net/** .</span><span class="sxs-lookup"><span data-stu-id="ce1d4-126">For example, if hello jars are stored in a container named **libs** on a storage account named **mystorage**, hello parameter would be **wasb://libs@mystorage.blob.core.windows.net/**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="ce1d4-127">Tym dokumencie przyjęto założenie, ma już utworzenie konta magazynu, kontenera obiektów blob i przekazane hello tooit plików.</span><span class="sxs-lookup"><span data-stu-id="ce1d4-127">This document assumes that you have already create a storage account, blob container, and uploaded hello files tooit.</span></span>
  >
  > <span data-ttu-id="ce1d4-128">Jeśli nie utworzono konto magazynu, możesz to zrobić za pomocą hello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ce1d4-128">If you have not created a storage account, you can do so through hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="ce1d4-129">Następnie można użyć narzędzia takie jak [Eksploratora usługi Storage Azure](http://storageexplorer.com/) toocreate kontenera w hello konta i przekazywanie plików tooit.</span><span class="sxs-lookup"><span data-stu-id="ce1d4-129">You can then use a utility such as [Azure Storage Explorer](http://storageexplorer.com/) toocreate a container in hello account and upload files tooit.</span></span>

## <a name="create-a-cluster-using-hello-script"></a><span data-ttu-id="ce1d4-130">Tworzenie klastra przy użyciu skryptu hello</span><span class="sxs-lookup"><span data-stu-id="ce1d4-130">Create a cluster using hello script</span></span>

> [!NOTE]
> <span data-ttu-id="ce1d4-131">Hello następujące kroki tworzenia klastra usługi HDInsight opartej na systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="ce1d4-131">hello following steps create a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="ce1d4-132">Wybierz toocreate klastra z systemem Windows, **Windows** jako hello klastra systemu operacyjnego, podczas tworzenia klastra hello, a następnie użyć skryptu systemu Windows (PowerShell) hello zamiast hello bash skryptu.</span><span class="sxs-lookup"><span data-stu-id="ce1d4-132">toocreate a Windows-based cluster, select **Windows** as hello cluster OS when creating hello cluster, and use hello Windows (PowerShell) script instead of hello bash script.</span></span>
>
> <span data-ttu-id="ce1d4-133">Można również użyć programu Azure PowerShell lub hello zestawu .NET SDK HDInsight toocreate klastra przy użyciu tego skryptu.</span><span class="sxs-lookup"><span data-stu-id="ce1d4-133">You can also use Azure PowerShell or hello HDInsight .NET SDK toocreate a cluster using this script.</span></span> <span data-ttu-id="ce1d4-134">Aby uzyskać więcej informacji o używaniu tych metod, zobacz [Dostosowywanie klastrów usługi HDInsight z akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="ce1d4-134">For more information on using these methods, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

1. <span data-ttu-id="ce1d4-135">Uruchom inicjowania obsługi klastra za pomocą kroków hello w [Obsługa administracyjna klastrów HDInsight w systemie Linux](hdinsight-hadoop-provision-linux-clusters.md), kroków inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="ce1d4-135">Start provisioning a cluster by using hello steps in [Provision HDInsight clusters on Linux](hdinsight-hadoop-provision-linux-clusters.md), but do not complete provisioning.</span></span>

2. <span data-ttu-id="ce1d4-136">Na powitania **konfiguracji opcjonalnej** bloku, wybierz opcję **akcji skryptu**i podaj hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="ce1d4-136">On hello **Optional Configuration** blade, select **Script Actions**, and provide hello following information:</span></span>

   * <span data-ttu-id="ce1d4-137">**Nazwa**: Wprowadź przyjazną nazwę dla hello akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="ce1d4-137">**NAME**: Enter a friendly name for hello script action.</span></span>

   * <span data-ttu-id="ce1d4-138">**Identyfikator URI skryptu**: https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh</span><span class="sxs-lookup"><span data-stu-id="ce1d4-138">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh</span></span>

   * <span data-ttu-id="ce1d4-139">**HEAD**: Zaznaczenie tego pola wyboru.</span><span class="sxs-lookup"><span data-stu-id="ce1d4-139">**HEAD**: Check this option.</span></span>

   * <span data-ttu-id="ce1d4-140">**Proces ROBOCZY**: Zaznaczenie tego pola wyboru.</span><span class="sxs-lookup"><span data-stu-id="ce1d4-140">**WORKER**: Check this option.</span></span>

   * <span data-ttu-id="ce1d4-141">**DOZORCY**: to pole pozostanie puste.</span><span class="sxs-lookup"><span data-stu-id="ce1d4-141">**ZOOKEEPER**: Leave this blank.</span></span>

   * <span data-ttu-id="ce1d4-142">**Parametry**: Wprowadź hello WASB adres toohello kontenera i konto magazynu zawierającego słoików hello.</span><span class="sxs-lookup"><span data-stu-id="ce1d4-142">**PARAMETERS**: Enter hello WASB address toohello container and storage account that contains hello jars.</span></span> <span data-ttu-id="ce1d4-143">Na przykład  **wasb://libs@mystorage.blob.core.windows.net/** .</span><span class="sxs-lookup"><span data-stu-id="ce1d4-143">For example, **wasb://libs@mystorage.blob.core.windows.net/**.</span></span>

3. <span data-ttu-id="ce1d4-144">U dołu hello hello **akcji skryptu**, użyj hello **wybierz** przycisk toosave hello konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="ce1d4-144">At hello bottom of hello **Script Actions**, use hello **Select** button toosave hello configuration.</span></span>

4. <span data-ttu-id="ce1d4-145">Na powitania **konfiguracji opcjonalnej** bloku, wybierz opcję **połączonych kontach magazynu** i wybierz hello **Dodaj klucz magazynu** łącza.</span><span class="sxs-lookup"><span data-stu-id="ce1d4-145">On hello **Optional Configuration** blade, select **Linked Storage Accounts** and select hello **Add a storage key** link.</span></span> <span data-ttu-id="ce1d4-146">Wybierz konto magazynu hello, który zawiera słoików hello, a następnie użyj hello **wybierz** ustawienia toosave przycisków i zwracany hello **konfiguracji opcjonalnej** bloku.</span><span class="sxs-lookup"><span data-stu-id="ce1d4-146">Select hello storage account that contains hello jars, and then use hello **select** buttons toosave settings and return hello **Optional Configuration** blade.</span></span>

5. <span data-ttu-id="ce1d4-147">Użyj hello **wybierz** u dołu hello hello **konfiguracji opcjonalnej** bloku toosave hello konfiguracji opcjonalnej informacji.</span><span class="sxs-lookup"><span data-stu-id="ce1d4-147">Use hello **Select** button at hello bottom of hello **Optional Configuration** blade toosave hello optional configuration information.</span></span>

6. <span data-ttu-id="ce1d4-148">Kontynuuj, inicjowania obsługi klastra hello zgodnie z opisem w [Obsługa administracyjna klastrów HDInsight w systemie Linux](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="ce1d4-148">Continue provisioning hello cluster as described in [Provision HDInsight clusters on Linux](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

<span data-ttu-id="ce1d4-149">Po zakończeniu tworzenia klastra są słoików hello toouse stanie dodane za pomocą tego skryptu z gałęzi bez konieczności toouse hello `ADD JAR` instrukcji.</span><span class="sxs-lookup"><span data-stu-id="ce1d4-149">Once cluster creation finishes, you are able toouse hello jars added through this script from Hive without having toouse hello `ADD JAR` statement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce1d4-150">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ce1d4-150">Next steps</span></span>

<span data-ttu-id="ce1d4-151">Aby uzyskać więcej informacji na temat pracy z Hive, zobacz [używanie Hive z usługą HDInsight](hdinsight-use-hive.md)</span><span class="sxs-lookup"><span data-stu-id="ce1d4-151">For more information on working with Hive, see [Use Hive with HDInsight](hdinsight-use-hive.md)</span></span>
